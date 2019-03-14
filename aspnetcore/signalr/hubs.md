---
title: 在 ASP.NET Core SignalR 使用中心
author: bradygaster
description: 了解如何在 ASP.NET Core SignalR 中使用中心。
monikerRange: '>= aspnetcore-2.1'
ms.author: bradyg
ms.custom: mvc
ms.date: 11/20/2018
uid: signalr/hubs
ms.openlocfilehash: 9bc74079235338c75c47e06bde2b78dc1c466bd6
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57030244"
---
# <a name="use-hubs-in-signalr-for-aspnet-core"></a>ASP.NET Core 使用 SignalR 中的中心

通过[Rachel Appel](https://twitter.com/rachelappel)和[Kevin Griffin](https://twitter.com/1kevgriff)

[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/hubs/sample/ ) [（如何下载）](xref:index#how-to-download-a-sample)

## <a name="what-is-a-signalr-hub"></a>SignalR 中心是什么

SignalR 中心 API，可从服务器在连接的客户端上调用方法。 在服务器代码中，定义客户端调用的方法。 在客户端代码中，定义从服务器调用的方法。 SignalR 负责在后台实现实时的客户端到服务器和服务器到客户端通信的所有内容。

## <a name="configure-signalr-hubs"></a>配置 SignalR 集线器

SignalR 中间件需要一些服务，这些服务通过调用`services.AddSignalR`来配置。

[!code-csharp[Configure service](hubs/sample/startup.cs?range=38)]

将 SignalR 功能添加到 ASP.NET Core 应用程序时，通过在`Startup.Configure`方法中调用`app.UseSignalR`来设置 SignalR 路由。

[!code-csharp[Configure routes to hubs](hubs/sample/startup.cs?range=57-60)]

## <a name="create-and-use-hubs"></a>创建和使用中心

通过声明从`Hub`继承的类来创建中心，并向其添加公共方法。 客户端可以调用定义为`public`的方法。

```csharp
public class ChatHub : Hub
{
    public Task SendMessage(string user, string message)
    {
        return Clients.All.SendAsync("ReceiveMessage", user, message);
    }
}
```

您可以指定返回类型和参数，包括复杂类型和数组，就像在任何 C# 方法中。 SignalR 处理序列化和反序列化复杂对象和数组中参数和返回值。

> [!NOTE]
> 中心是暂时的：
> * 不要将状态存储在 hub 类的属性中。 每个 hub 方法调用都在新的 hub 实例上执行。  
> * 使用`await`调用取决于中心保持活动状态的异步方法时。 例如，如方法`Clients.All.SendAsync(...)`如果调用，但不可能会失败`await`和集线器方法完成之前`SendAsync`完成。

## <a name="the-context-object"></a>上下文对象

`Hub`类具有`Context`属性，其中包含以下属性与连接有关的信息：

| 属性 | 描述 |
| ------ | ----------- |
| `ConnectionId` | 获取用于此连接，由 SignalR 分配的唯一 ID。 没有为每个连接的一个连接 ID。|
| `UserIdentifier` | 获取[用户标识符](xref:signalr/groups)。 默认情况下，使用 SignalR`ClaimTypes.NameIdentifier`从`ClaimsPrincipal`与作为用户标识符连接相关联。 |
| `User` | 获取`ClaimsPrincipal`与当前用户相关联。 |
| `Items` | 获取可用于共享此连接的作用域内的数据的键/值集合。 数据可以存储在此集合中，它将连接在不同的集线器方法调用中保持原样。 |
| `Features` | 获取在连接上的可用功能的集合。 现在，此集合不需要在大多数情况下，因此它不尚未记录在详细信息。 |
| `ConnectionAborted` | 获取`CancellationToken`，时连接中止通知。 |

`Hub.Context` 此外包含以下方法：

| 方法 | 描述 |
| ------ | ----------- |
| `GetHttpContext` | 返回`HttpContext`用于此连接，或`null`如果连接不是与 HTTP 请求相关联。 对于 HTTP 连接，可以使用此方法以获取 HTTP 标头和查询字符串等信息。 |
| `Abort` | 中止的连接。 |

## <a name="the-clients-object"></a>客户端对象

`Hub`类具有`Clients`属性，其中包含服务器和客户端之间通信的以下属性：

| 属性 | 描述 |
| ------ | ----------- |
| `All` | 在所有连接的客户端上调用的方法 |
| `Caller` | 在客户端调用集线器方法调用的方法 |
| `Others` | 除调用该方法的客户端的所有已连接客户端上调用的方法 |

`Hub.Clients` 此外包含以下方法：

| 方法 | 描述 |
| ------ | ----------- |
| `AllExcept` | 除了指定连接的所有已连接客户端上调用的方法 |
| `Client` | 调用特定连接的客户端上的方法 |
| `Clients` | 调用特定连接的客户端上的方法 |
| `Group` | 指定的组中的所有连接上调用的方法  |
| `GroupExcept` | 在指定组中，指定的连接除外的所有连接上调用的方法 |
| `Groups` | 在多个组的连接上调用的方法  |
| `OthersInGroup` | 上一组连接，不包括客户端调用集线器方法调用的方法  |
| `User` | 与特定用户关联的所有连接上调用的方法 |
| `Users` | 使用指定的用户关联的所有连接上调用的方法 |

每个属性或方法上表中的返回一个包含对象`SendAsync`方法。 `SendAsync`方法允许您提供的名称和要调用的客户端方法的参数。

## <a name="send-messages-to-clients"></a>将消息发送到客户端

若要使对特定的客户端的调用，使用的属性`Clients`对象。 在以下示例中，有三个中心的方法：

* `SendMessage` 将消息发送到所有已连接客户端，使用`Clients.All`。
* `SendMessageToCaller` 将消息发送回调用方，使用`Clients.Caller`。
* `SendMessageToGroups` 将消息发送到中的所有客户端`SignalR Users`组。

[!code-csharp[Send messages](hubs/sample/hubs/chathub.cs?name=HubMethods)]

## <a name="strongly-typed-hubs"></a>强类型化的中心

使用的一个缺点`SendAsync`是依赖于使用魔幻字符串来指定客户端方法调用。 这将使运行时错误，如果方法名称的拼写错误的代码打开或缺少从客户端。

使用的替代方法`SendAsync`是强类型化`Hub`与<xref:Microsoft.AspNetCore.SignalR.Hub`1>。 在以下示例中，`ChatHub`客户端方法具有出提取到一个接口，称为`IChatClient`。  

[!code-csharp[Interface for IChatClient](hubs/sample/hubs/ichatclient.cs?name=snippet_IChatClient)]

此接口可用于重构前面`ChatHub`示例。

[!code-csharp[Strongly typed ChatHub](hubs/sample/hubs/StronglyTypedChatHub.cs?range=8-18,36)]

使用`Hub<IChatClient>`启用编译时检查的客户端方法。 这可以防止由于使用魔幻字符串导致的问题`Hub<T>`可以仅提供访问权限在接口中定义的方法。

使用强类型化`Hub<T>`禁用的功能使用`SendAsync`。 该接口上定义的任何方法仍可以定义为异步。 实际上，每种方法应返回`Task`。 由于它是一个接口，不要使用`async`关键字。 例如：

```csharp
public interface IClient
{
    Task ClientMethod();
}
```

> [!NOTE]
> `Async`后缀不从方法名称中去除。 除非客户端方法使用定义`.on('MyMethodAsync')`，则不应使用`MyMethodAsync`作为名称。

## <a name="change-the-name-of-a-hub-method"></a>将集线器方法的名称更改

默认情况下，服务器中心方法名称为.NET 方法的名称。 但是，可以使用[HubMethodName](xref:Microsoft.AspNetCore.SignalR.HubMethodNameAttribute)属性来更改此默认设置，并手动指定方法的名称。 调用该方法时，客户端应而不是.NET 方法名称，使用此名称。

[!code-csharp[HubMethodName attribute](hubs/sample/hubs/chathub.cs?name=HubMethodName&highlight=1)]

## <a name="handle-events-for-a-connection"></a>处理连接事件

SignalR 中心 API 提供了`OnConnectedAsync`和`OnDisconnectedAsync`管理和跟踪连接的虚拟方法。 重写`OnConnectedAsync`虚拟方法，客户端连接到中心，如将其添加到组时，执行操作。

[!code-csharp[Handle connection](hubs/sample/hubs/chathub.cs?name=OnConnectedAsync)]

重写`OnDisconnectedAsync`虚拟方法，当客户端断开连接时执行的操作。 如果客户端有意断开连接 (通过调用`connection.stop()`，例如)，则`exception`参数将为`null`。 但是，如果客户端已断开连接错误 （例如网络故障），由于`exception`参数将包含描述失败的异常。

[!code-csharp[Handle disconnection](hubs/sample/hubs/chathub.cs?name=OnDisconnectedAsync)]

## <a name="handle-errors"></a>处理错误

集线器方法中引发的异常将发送到的客户端的调用的方法。 在 JavaScript 客户端`invoke`方法将返回[JavaScript Promise](https://developer.mozilla.org/docs/Web/JavaScript/Guide/Using_promises)。 当客户端收到的错误处理程序附加到承诺使用`catch`，它具有调用，并且作为 JavaScript 传递`Error`对象。

[!code-javascript[Error](hubs/sample/wwwroot/js/chat.js?range=23)]

如果你的中心引发了异常，不会关闭连接。 默认情况下，SignalR 返回到客户端的一般性错误消息。 例如：

```
Microsoft.AspNetCore.SignalR.HubException: An unexpected error occurred invoking 'MethodName' on the server.
```

意外的异常通常包含敏感信息，例如触发数据库连接失败时引发异常的数据库服务器的名称。 SignalR 并不作为一种安全措施，默认情况下公开这些详细的错误消息。 请参阅[安全注意事项文章](xref:signalr/security#exceptions)异常详细信息所抑制的原因的详细信息。

如果有异常条件您*做*想要传播到客户端，则可以使用`HubException`类。 如果引发`HubException`从中心方法，SignalR**将**将整个消息发送到客户端，以未经修改的。

[!code-csharp[ThrowHubException](hubs/sample/hubs/chathub.cs?name=ThrowHubException&highlight=3)]

> [!NOTE]
> SignalR 只发送`Message`到客户端异常的属性。 堆栈跟踪和异常上的其他属性不是可用于客户端。

## <a name="related-resources"></a>相关资源

* [ASP.NET Core SignalR 简介](xref:signalr/introduction)
* [JavaScript 客户端](xref:signalr/javascript-client)
* [发布到 Azure](xref:signalr/publish-to-azure-web-app)

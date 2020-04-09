---
uid: signalr/overview/guide-to-the-api/hubs-api-guide-server
title: ASP.NET信号器集线器 API 指南 - 服务器 （C#） |微软文档
author: bradygaster
description: 本文档介绍了为 SignalR 版本 2 编写ASP.NET信号R 集线器 API 的服务器端，并演示了代码示例...
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: b19913e5-cd8a-4e4b-a872-5ac7a858a934
msc.legacyurl: /signalr/overview/guide-to-the-api/hubs-api-guide-server
msc.type: authoredcontent
ms.openlocfilehash: c681b104b15bfc4a04587c7abf685dcf20def2ca
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675801"
---
# <a name="aspnet-signalr-hubs-api-guide---server-c"></a>ASP.NET信号器集线器 API 指南 - 服务器 （C#）

由[帕特里克·弗莱彻](https://github.com/pfletcher)，[汤姆·戴克斯特拉](https://github.com/tdykstra)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 本文档介绍了为 SignalR 版本 2 编写ASP.NET信号R 集线器 API 的服务器端，并演示了常见选项的代码示例。
> 
> SignalR 集线器 API 使您能够从服务器对连接的客户端以及从客户端到服务器进行远程过程调用 （RPC）。 在服务器代码中，定义客户端可以调用的方法，并调用在客户端上运行的方法。 在客户端代码中，定义可以从服务器调用的方法，并调用在服务器上运行的方法。 SignalR 为您处理所有客户端到服务器管道。
> 
> SignalR 还提供称为持久连接的较低级别的 API。 有关信号R、集线器和持久连接的介绍，请参阅[信号R 2 简介](../getting-started/introduction-to-signalr.md)。
> 
> ## <a name="software-versions-used-in-this-topic"></a>本主题中使用的软件版本
> 
> 
> - [Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - .NET 4.5
> - 信号R版本 2
>   
> 
> 
> ## <a name="topic-versions"></a>主题版本
> 
> 有关早期版本的 SignalR 的信息，请参阅[SignalR 旧版本](../older-versions/index.md)。
> 
> ## <a name="questions-and-comments"></a>问题和评论
> 
> 请留下反馈，关于你喜欢本教程的方式，以及我们可以在页面底部的评论中改进什么。 如果您有与本教程没有直接关系的问题，您可以将它们发布到[ASP.NET SignalR 论坛](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com/)。

## <a name="overview"></a>概述

本文档包含以下各节：

- [如何注册SignalR中间件](#route)

    - [/信号器 URL](#signalrurl)
    - [配置信号R选项](#options)
- [如何创建和使用中心类](#hubclass)

    - [中心对象生存期](#transience)
    - [JavaScript 客户端中中心名称的骆驼大小写](#hubnames)
    - [多个中心](#multiplehubs)
    - [强类型集线器](#stronglytypedhubs)
- [如何在中心类中定义客户端可以调用的方法](#hubmethods)

    - [JavaScript 客户端中方法名称的骆驼大小写](#methodnames)
    - [何时异步执行](#asyncmethods)
    - [定义重载](#overloads)
    - [报告中心方法调用的进度](#progress)
- [如何从中心类调用客户端方法](#callfromhub)

    - [选择哪些客户端将收到 RPC](#selectingclients)
    - [方法名称没有编译时间验证](#dynamicmethodnames)
    - [区分大小写的方法名称匹配](#caseinsensitive)
    - [异步执行](#asyncclient)
- [如何从中心类管理组成员身份](#groupsfromhub)

    - [添加和删除方法的异步执行](#asyncgroupmethods)
    - [组成员身份持久性](#grouppersistence)
    - [单用户组](#singleusergroups)
- [如何处理集线器类中的连接生存期事件](#connectionlifetime)

    - [当"连接"时，打开断开状态，并调用"重新连接"](#onreconnected)
    - [未填充的呼叫者状态](#nocallerstate)
- [如何从上下文属性获取有关客户端的信息](#contextproperty)
- [如何在客户端和中心类之间传递状态](#passstate)
- [如何处理中心类中的错误](#handleErrors)
- [如何调用客户端方法并管理来自中心类外部的组](#callfromoutsidehub)

    - [调用客户端方法](#callingclientsoutsidehub)
    - [管理组成员身份](#managinggroupsoutsidehub)
- [如何启用跟踪](#tracing)
- [如何自定义中心管道](#hubpipeline)

有关如何对客户端进行编程的文档，请参阅以下资源：

- [信号器中心 API 指南 - JavaScript 客户端](hubs-api-guide-javascript-client.md)
- [信号器集线器 API 指南 - .NET 客户端](hubs-api-guide-net-client.md)

SignalR 2 的服务器组件仅在 .NET 4.5 中可用。 运行 .NET 4.0 的服务器必须使用 SignalR v1.x。

<a id="route"></a>

## <a name="how-to-register-signalr-middleware"></a>如何注册SignalR中间件

要定义客户端将用于连接到集线器的路由，请在`MapSignalR`应用程序启动时调用 方法。 `MapSignalR`是类的`OwinExtensions`[扩展方法](https://msdn.microsoft.com/library/vstudio/bb383977.aspx)。 下面的示例演示如何使用 OWIN 启动类定义 SignalR 中心路由。

[!code-csharp[Main](hubs-api-guide-server/samples/sample1.cs)]

如果要将 SignalR 功能添加到ASP.NET MVC 应用程序，请确保在其他路由之前添加 SignalR 路由。 有关详细信息，请参阅[教程：开始使用 SignalR 2 和 MVC 5](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)。

<a id="signalrurl"></a>

### <a name="the-signalr-url"></a>/信号器 URL

默认情况下，客户端将用于连接到集线器的路由 URL 为"/信号器"。 （不要将此 URL 与"/信号器/集线器"URL 混淆，该 URL 适用于自动生成的 JavaScript 文件。 有关生成的代理的详细信息，请参阅[SignalR 中心 API 指南 - JavaScript 客户端 - 生成的代理及其为您做什么](hubs-api-guide-javascript-client.md#genproxy)。

可能存在异常情况，使此基 URL 不适用于 SignalR;例如，项目中有一个名为*信号器*的文件夹，并且不想更改名称。 在这种情况下，您可以更改基本 URL，如以下示例所示（将示例代码中的"/信号器"替换为所需的 URL）。

**指定 URL 的服务器代码**

[!code-csharp[Main](hubs-api-guide-server/samples/sample2.cs?highlight=1)]

**指定 URL 的 JavaScript 客户端代码（使用生成的代理）**

[!code-javascript[Main](hubs-api-guide-server/samples/sample3.js?highlight=1)]

**指定 URL 的 JavaScript 客户端代码（没有生成的代理）**

[!code-javascript[Main](hubs-api-guide-server/samples/sample4.js?highlight=1)]

**指定 URL 的 .NET 客户端代码**

[!code-csharp[Main](hubs-api-guide-server/samples/sample5.cs?highlight=1)]

<a id="options"></a>

### <a name="configuring-signalr-options"></a>配置信号灯选项

`MapSignalR`方法的重载使您能够指定自定义 URL、自定义依赖项解析器以及以下选项：

- 使用浏览器客户端的 CORS 或 JSONP 启用跨域调用。

    通常，如果浏览器从`http://contoso.com`加载页面，则 SignalR 连接位于同一域中`http://contoso.com/signalr`，在 。 如果 中的`http://contoso.com`页面与`http://fabrikam.com/signalr`断开连接，则为跨域连接。 出于安全原因，默认情况下禁用跨域连接。 有关详细信息，请参阅[ASP.NET信号R中心 API 指南 - JavaScript 客户端 - 如何建立跨域连接](hubs-api-guide-javascript-client.md#crossdomain)。
- 启用详细的错误消息。

    发生错误时，SignalR 的默认行为是向客户端发送通知消息，而不详细说明发生的情况。 在生产中不建议向客户端发送详细的错误信息，因为恶意用户可能能够在针对应用程序的攻击中使用该信息。 对于故障排除，可以使用此选项暂时启用信息量更大的错误报告。
- 禁用自动生成的 JavaScript 代理文件。

    默认情况下，将生成具有中心类代理的 JavaScript 文件，以响应 URL"/信号器/集线器"。 如果不想使用 JavaScript 代理，或者要手动生成此文件并引用客户端中的物理文件，则可以使用此选项禁用代理生成。 有关详细信息，请参阅[SignalR 中心 API 指南 - JavaScript 客户端 - 如何为 SignalR 生成的代理创建物理文件](hubs-api-guide-javascript-client.md#manualproxy)。

下面的示例演示如何在调用`MapSignalR`方法中指定 SignalR 连接 URL 和这些选项。 要指定自定义 URL，请将示例中的"/信号器"替换为要使用的 URL。

[!code-csharp[Main](hubs-api-guide-server/samples/sample6.cs)]

<a id="hubclass"></a>

## <a name="how-to-create-and-use-hub-classes"></a>如何创建和使用中心类

要创建集线器，请创建一个派生自[Microsoft 的类。](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx) 下面的示例显示了聊天应用程序的简单中心类。

[!code-csharp[Main](hubs-api-guide-server/samples/sample7.cs)]

在此示例中，连接的客户端可以调用`NewContosoChatMessage`方法，当它调用时，接收的数据将广播到所有连接的客户端。

<a id="transience"></a>

### <a name="hub-object-lifetime"></a>中心对象生存期

您不会实例化 Hub 类，也不会从服务器上自己的代码调用其方法;否则，您就不会实例化 Hub 类，所有由 SignalR 中心管道为您完成。 SignalR 在每次需要处理集线器操作（例如客户端连接、断开连接或对服务器进行方法调用时）时，都会创建 Hub 类的新实例。

由于 Hub 类的实例是暂时性的，因此不能使用它们来维护从一个方法调用到下一个方法的状态。 每次服务器收到来自客户端的方法调用时，Hub 类的新实例都会处理该消息。 要通过多个连接和方法调用维护状态，请使用其他方法，如数据库或 Hub 类上的静态变量，或者不派生自`Hub`的不同类。 如果在内存中保留数据，使用 Hub 类上静态变量等方法，则当应用域回收时，数据将丢失。

如果要从在 Hub 类之外运行的您自己的代码向客户端发送消息，不能通过实例化 Hub 类实例来执行此操作，但可以通过获取对 Hub 类的 SignalR 上下文对象的引用来执行此操作。 有关详细信息，请参阅本主题稍后在[中心类外部调用客户端方法和管理组](#callfromoutsidehub)。

<a id="hubnames"></a>

### <a name="camel-casing-of-hub-names-in-javascript-clients"></a>JavaScript 客户端中中心名称的骆驼大小写

默认情况下，JavaScript 客户端使用类名称的骆驼大小写版本引用集线器。 SignalR 会自动进行此更改，以便 JavaScript 代码可以符合 JavaScript 约定。 前面的示例将称为`contosoChatHub`JavaScript 代码。

**Server**

[!code-csharp[Main](hubs-api-guide-server/samples/sample8.cs?highlight=1)]

**使用生成的代理的 JavaScript 客户端**

[!code-javascript[Main](hubs-api-guide-server/samples/sample9.js?highlight=1)]

如果要为客户端指定要使用的其他名称，请添加该`HubName`属性。 使用`HubName`属性时，JavaScript 客户端上不会更改骆驼大小写的名称。

**Server**

[!code-csharp[Main](hubs-api-guide-server/samples/sample10.cs?highlight=1)]

**使用生成的代理的 JavaScript 客户端**

[!code-javascript[Main](hubs-api-guide-server/samples/sample11.js?highlight=1)]

<a id="multiplehubs"></a>

### <a name="multiple-hubs"></a>多个中心

您可以在应用程序中定义多个中心类。 执行此操作时，连接是共享的，但组是独立的：

- 所有客户端都将使用相同的 URL 与服务建立 SignalR 连接（"/信号器"或自定义 URL（如果您指定了一个），并且该连接用于服务定义的所有中心。

    与在单个类中定义所有中心功能相比，多个中心的性能差异没有差异。
- 所有中心都获取相同的 HTTP 请求信息。

    由于所有集线器共享相同的连接，因此服务器获得的唯一 HTTP 请求信息是建立 SignalR 连接的原始 HTTP 请求中的内容。 如果使用连接请求通过指定查询字符串将信息从客户端传递到服务器，则不能向不同的中心提供不同的查询字符串。 所有中心都将收到相同的信息。
- 生成的 JavaScript 代理文件将包含一个文件中所有中心代理。

    有关 JavaScript 代理的信息，请参阅[SignalR 中心 API 指南 - JavaScript 客户端 - 生成的代理及其为您做什么](hubs-api-guide-javascript-client.md#genproxy)。
- 组在中心内定义。

    在 SignalR 中，您可以定义要广播到连接客户端子集的命名组。 每个中心分别维护组。 例如，名为"管理员"的组将包含类`ContosoChatHub`的一组客户端，而相同的组名称将引用类`StockTickerHub`的不同客户端集。

<a id="stronglytypedhubs"></a>
### <a name="strongly-typed-hubs"></a>强类型集线器

要为客户端可以引用的集线器方法定义接口（并在集线器方法上启用 Intellisense），请从`Hub<T>`（在 SignalR 2.1 中`Hub`引入） 而不是 派生中心。

[!code-csharp[Main](hubs-api-guide-server/samples/sample12.cs)]

<a id="hubmethods"></a>

## <a name="how-to-define-methods-in-the-hub-class-that-clients-can-call"></a>如何在中心类中定义客户端可以调用的方法

要在 Hub 上公开要从客户端调用的方法，请声明公共方法，如以下示例所示。

[!code-csharp[Main](hubs-api-guide-server/samples/sample13.cs?highlight=3)]

[!code-csharp[Main](hubs-api-guide-server/samples/sample14.cs?highlight=3)]

您可以指定返回类型和参数，包括复杂类型和数组，就像在任何 C# 方法中一样。 使用 JSON 在客户端和服务器之间通信以参数接收或返回到调用方的任何数据，SignalR 会自动处理复杂对象和对象数组的绑定。

<a id="methodnames"></a>

### <a name="camel-casing-of-method-names-in-javascript-clients"></a>JavaScript 客户端中方法名称的骆驼大小写

默认情况下，JavaScript 客户端使用方法名称的骆驼大小写版本引用 Hub 方法。 SignalR 会自动进行此更改，以便 JavaScript 代码可以符合 JavaScript 约定。

**Server**

[!code-csharp[Main](hubs-api-guide-server/samples/sample15.cs?highlight=1)]

**使用生成的代理的 JavaScript 客户端**

[!code-javascript[Main](hubs-api-guide-server/samples/sample16.js?highlight=1)]

如果要为客户端指定要使用的其他名称，请添加该`HubMethodName`属性。

**Server**

[!code-csharp[Main](hubs-api-guide-server/samples/sample17.cs?highlight=1)]

**使用生成的代理的 JavaScript 客户端**

[!code-javascript[Main](hubs-api-guide-server/samples/sample18.js?highlight=1)]

<a id="asyncmethods"></a>

### <a name="when-to-execute-asynchronously"></a>何时异步执行

如果该方法将长时间运行或必须执行需要等待的工作（如数据库查找或 Web 服务调用），则通过返回[任务](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx)（代替`void`返回）或[Task&lt;T&gt;](https://msdn.microsoft.com/library/dd321424.aspx)对象（代替`T`返回类型）使 Hub 方法异步。 当您从 方法`Task`返回对象时，SignalR 会等待`Task`完成，然后它将未包装的结果发送回客户端，因此在客户端中编写方法调用的代码没有区别。

使集线器方法异步可避免在使用 WebSocket 传输时阻塞连接。 当集线器方法同步执行且传输为 WebSocket 时，从同一客户端在集线器上调用方法将被阻止，直到中心方法完成。

下面的示例显示编码为同步或异步运行的相同方法，然后是适用于调用任一版本的 JavaScript 客户端代码。

**同步**

[!code-csharp[Main](hubs-api-guide-server/samples/sample19.cs)]

**异步**

[!code-csharp[Main](hubs-api-guide-server/samples/sample20.cs?highlight=1,7-8)]

**使用生成的代理的 JavaScript 客户端**

[!code-javascript[Main](hubs-api-guide-server/samples/sample21.js)]

有关如何在 ASP.NET 4.5 中使用异步方法的详细信息，请参阅[在 mVC 4 中使用异步方法ASP.NET](../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md)。

<a id="overloads"></a>

### <a name="defining-overloads"></a>定义重载

如果要为方法定义重载，则每个重载中的参数数必须不同。 如果仅通过指定不同的参数类型来区分重载，则 Hub 类将编译，但当客户端尝试调用其中一个重载时，SignalR 服务将在运行时引发异常。

<a id="progress"></a>
### <a name="reporting-progress-from-hub-method-invocations"></a>报告中心方法调用的进度

SignalR 2.1 添加了对 .NET 4.5 中引入[的进度报告模式](https://blogs.msdn.com/b/dotnet/archive/2012/06/06/async-in-4-5-enabling-progress-and-cancellation-in-async-apis.aspx)的支持。 要实现进度报告，请为`IProgress<T>`客户端可以访问的集线器方法定义参数：

[!code-csharp[Main](hubs-api-guide-server/samples/sample22.cs)]

编写长时间运行的服务器方法时，使用异步编程模式（如 Async/Await）而不是阻止中心线程非常重要。

<a id="callfromhub"></a>

## <a name="how-to-call-client-methods-from-the-hub-class"></a>如何从中心类调用客户端方法

要从服务器调用客户端方法，`Clients`请使用 Hub 类中方法中的 属性。 下面的示例显示调用`addNewMessageToPage`所有连接的客户端的服务器代码，以及定义 JavaScript 客户端中方法的客户端代码。

**Server**

[!code-csharp[Main](hubs-api-guide-server/samples/sample23.cs?highlight=5)]

调用客户端方法是异步操作，并返回 。 `Task` 使用 `await`：

* 确保消息发送时没有错误。 
* 启用在尝试捕获块中捕获和处理错误。

**使用生成的代理的 JavaScript 客户端**

[!code-html[Main](hubs-api-guide-server/samples/sample24.html?highlight=1)]

无法从客户端方法获取返回值;因此，无法从客户端方法获取返回值。语法，如`int x = Clients.All.add(1,1)`不工作。

您可以为参数指定复杂的类型和数组。 下面的示例将复杂类型传递给方法参数中的客户端。

**使用复杂对象调用客户端方法的服务器代码**

[!code-csharp[Main](hubs-api-guide-server/samples/sample25.cs?highlight=3)]

**定义复杂对象的服务器代码**

[!code-csharp[Main](hubs-api-guide-server/samples/sample26.cs?highlight=1)]

**使用生成的代理的 JavaScript 客户端**

[!code-javascript[Main](hubs-api-guide-server/samples/sample27.js?highlight=2-3)]

<a id="selectingclients"></a>

### <a name="selecting-which-clients-will-receive-the-rpc"></a>选择哪些客户端将收到 RPC

客户端属性返回一个[HubConnectionConnection 对象](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx)，该对象提供了多个选项来指定哪些客户端将接收 RPC：

- 所有已连接的客户端。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample28.cs)]
- 仅调用客户端。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample29.cs)]
- 除调用客户端之外的所有客户端。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample30.cs)]
- 由连接 ID 标识的特定客户端。

    [!code-css[Main](hubs-api-guide-server/samples/sample31.css)]

    此示例调用`addContosoChatMessageToPage`调用客户端，并且与 使用`Clients.Caller`具有相同的效果。
- 除指定客户端外的所有连接客户端，由连接 ID 标识。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample32.cs)]
- 指定组中的所有连接客户端。

    [!code-css[Main](hubs-api-guide-server/samples/sample33.css)]
- 指定组中的所有连接客户端（指定客户端除外），由连接 ID 标识。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample34.cs)]
- 指定组中的所有已连接客户端（调用客户端除外）。

    [!code-css[Main](hubs-api-guide-server/samples/sample35.css)]
- 用户 Id 标识的特定用户。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample36.cs)]

    默认情况下，这是`IPrincipal.Identity.Name`，但可以通过[向全局主机注册 IUserIdProvider 的实现](mapping-users-to-connections.md#IUserIdProvider)来更改。
- 连接指示列表中的所有客户端和组。

    [!code-css[Main](hubs-api-guide-server/samples/sample37.css)]
- 组的列表。

    [!code-css[Main](hubs-api-guide-server/samples/sample38.css)]
- 按名称命名的用户。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample39.cs)]
- 用户名列表（在 SignalR 2.1 中介绍）。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample40.cs)]

<a id="dynamicmethodnames"></a>

### <a name="no-compile-time-validation-for-method-names"></a>方法名称没有编译时间验证

您指定的方法名称被解释为动态对象，这意味着没有 IntelliSense 或编译时间验证。 表达式在运行时计算。 当方法调用执行时，SignalR 会将方法名称和参数值发送到客户端，如果客户端具有与该名称匹配的方法，则调用该方法并将参数值传递给它。 如果在客户端上找不到匹配方法，则不引发错误。 有关 SignalR 调用客户端方法时在后台传输到客户端的数据格式的信息，请参阅[SignalR 简介](../getting-started/introduction-to-signalr.md)。

<a id="caseinsensitive"></a>

### <a name="case-insensitive-method-name-matching"></a>区分大小写的方法名称匹配

方法名称匹配不区分大小写。 例如，`Clients.All.addContosoChatMessageToPage`在服务器上将执行`AddContosoChatMessageToPage`、`addcontosochatmessagetopage`或`addContosoChatMessageToPage`在客户端上。

<a id="asyncclient"></a>

### <a name="asynchronous-execution"></a>异步执行

调用的方法以异步方式执行。 对客户端进行方法调用后出现的任何代码将立即执行，而无需等待 SignalR 完成向客户端传输数据，除非您指定后续代码行应等待方法完成。 下面的代码示例演示如何按顺序执行两个客户端方法。

**使用 Await （.NET 4.5）**

[!code-csharp[Main](hubs-api-guide-server/samples/sample41.cs?highlight=1,3)]

如果使用等待`await`客户端方法在下一行代码执行之前完成，这并不意味着客户端将在执行下一行代码之前实际收到消息。 客户端方法调用的"完成"仅意味着 SignalR 已执行发送消息所需的一切。 如果您需要验证客户端是否收到该消息，您必须自己对该机制进行编程。 例如，您可以在 Hub 上`MessageReceived`编写方法代码，在客户端上`addContosoChatMessageToPage`编写方法后，您可以在执行需要在客户端`MessageReceived`上执行的任何工作后调用。 在`MessageReceived`Hub 中，您可以执行依赖于原始方法调用的实际客户端接收和处理的任何工作。

### <a name="how-to-use-a-string-variable-as-the-method-name"></a>如何使用字符串变量作为方法名称

如果要使用字符串变量作为方法名称调用客户端方法，则强制`Clients.All`（或`Clients.Others`、等`Clients.Caller`）调用`IClientProxy` [Invoke（方法名称、args...）](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.iclientproxy.invoke(v=vs.111).aspx)。

[!code-csharp[Main](hubs-api-guide-server/samples/sample42.cs)]

<a id="groupsfromhub"></a>

## <a name="how-to-manage-group-membership-from-the-hub-class"></a>如何从中心类管理组成员身份

SignalR 中的组提供了一种将消息广播到连接客户端的指定子集的方法。 组可以具有任意数量的客户端，并且客户端可以是任意数量的组的成员。

要管理组成员身份，请使用中心类`Groups`的属性提供的["添加](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx)[和删除"](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx)方法。 下面的示例显示了由客户端`Groups.Add`代码`Groups.Remove`调用的 Hub 方法中使用的 和 方法，然后是调用它们的 JavaScript 客户端代码。

**Server**

[!code-csharp[Main](hubs-api-guide-server/samples/sample43.cs?highlight=5,10)]

**使用生成的代理的 JavaScript 客户端**

[!code-javascript[Main](hubs-api-guide-server/samples/sample44.js)]

[!code-javascript[Main](hubs-api-guide-server/samples/sample45.js)]

您不必显式创建组。 实际上，在调用`Groups.Add`中首次指定其名称时会自动创建组，并且当您从其成员身份中删除最后一个连接时，该组将被删除。

没有用于获取组成员身份列表或组列表的 API。 SignalR 根据[pub/子模型](http://en.wikipedia.org/wiki/Publish/subscribe)向客户端和组发送消息，并且服务器不维护组或组成员身份的列表。 这有助于最大化可伸缩性，因为每当将节点添加到 Web 场时，SignalR 维护的任何状态都必须传播到新节点。

<a id="asyncgroupmethods"></a>

### <a name="asynchronous-execution-of-add-and-remove-methods"></a>添加和删除方法的异步执行

`Groups.Add`和`Groups.Remove`方法以异步方式执行。 如果要将客户端添加到组，然后使用 组立即向客户端发送消息，则必须确保`Groups.Add`该方法首先完成。 下面的代码示例演示如何执行此操作。

**将客户端添加到组，然后向该客户端发送消息**

[!code-csharp[Main](hubs-api-guide-server/samples/sample46.cs?highlight=1,3)]

<a id="grouppersistence"></a>

### <a name="group-membership-persistence"></a>组成员身份持久性

SignalR 跟踪连接，而不是用户，因此，如果您希望用户每次建立连接时都位于同一组中，则每次用户建立新连接时都必须调用`Groups.Add`。

在暂时失去连接后，有时 SignalR 可以自动恢复连接。 在这种情况下，SignalR 正在还原相同的连接，而不是建立新连接，因此客户端的组成员身份将自动还原。 即使临时中断是服务器重新启动或失败的结果，也是可能的，因为每个客户端（包括组成员身份）的连接状态都向客户端四舍五入。 如果服务器在连接超时之前出现故障并由新服务器替换，则客户端可以自动重新连接到新服务器，并重新注册其成员的组。

当连接在失去连接后或连接超时或客户端断开连接（例如，当浏览器导航到新页面时）无法自动恢复时，组成员身份将丢失。 用户下次连接时将是一个新连接。 要在同一用户建立新连接时维护组成员身份，应用程序必须跟踪用户和组之间的关联，并在每次用户建立新连接时还原组成员身份。

有关连接和重新连接的详细信息，请参阅本主题后面的["集线器"类中如何处理连接生存期事件](#connectionlifetime)。

<a id="singleusergroups"></a>

### <a name="single-user-groups"></a>单用户组

使用 SignalR 的应用程序通常必须跟踪用户和连接之间的关联，以便知道哪个用户发送消息以及应该接收哪些用户。 组用于执行此操作的两个常用模式之一。

- 单用户组。

    您可以将用户名指定为组名称，并在每次用户连接或重新连接时将当前连接 ID 添加到组。 向发送给组的用户发送消息。 此方法的缺点是，组不为您提供一种方法来了解用户是联机还是脱机。
- 跟踪用户名和连接指示之间的关联。

    您可以将每个用户名与字典或数据库中的一个或多个连接 I 之间的关联存储，并在每次用户连接或断开连接时更新存储的数据。 要向用户发送消息，请指定连接指示。 此方法的缺点是它需要更多的内存。

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events-in-the-hub-class"></a>如何处理集线器类中的连接生存期事件

处理连接生存期事件的典型原因是跟踪用户是否已连接，并跟踪用户名和连接令牌之间的关联。 要在客户端连接或断开连接时运行自己的代码，请重写`OnConnected` `OnDisconnected`Hub`OnReconnected`类 的 和 和 虚拟方法，如以下示例所示。

[!code-csharp[Main](hubs-api-guide-server/samples/sample47.cs?highlight=3,14,22)]

<a id="onreconnected"></a>

### <a name="when-onconnected-ondisconnected-and-onreconnected-are-called"></a>当"连接"时，打开断开状态，并调用"重新连接"

每次浏览器导航到新页面时，都必须建立一个新连接，这意味着 SignalR 将执行方法后跟`OnDisconnected``OnConnected`的方法。 建立新连接时，SignalR 始终创建新的连接 ID。

当`OnReconnected`SignalR 可以自动恢复的连接出现暂时中断时调用该方法，例如电缆在连接超时之前暂时断开并重新连接时。当`OnDisconnected`客户端断开连接且 SignalR 无法自动重新连接时，如浏览器导航到新页面时，将调用该方法。 因此，给定客户端的可能事件序列为`OnConnected`，和`OnReconnected``OnDisconnected`或`OnConnected` `OnDisconnected`。 对于给定的连接，`OnConnected``OnDisconnected`您将看不到序列，。 `OnReconnected`

在某些情况下`OnDisconnected`，例如服务器出现故障或 App Domain 被回收时，不会调用该方法。 当另一台服务器上线或 App Domain 完成其回收时，某些客户端可能能够重新连接并触发`OnReconnected`事件。

有关详细信息，请参阅在[SignalR 中了解和处理连接生存期事件](handling-connection-lifetime-events.md)。

<a id="nocallerstate"></a>

### <a name="caller-state-not-populated"></a>未填充的呼叫者状态

连接生存期事件处理程序方法从服务器调用，这意味着您在`state`客户端上的对象中放置的任何状态将不会填充在服务器上`Caller`的属性中。 有关`state`对象和`Caller`属性的信息，请参阅本主题后面的["如何在客户端和中心类之间传递状态](#passstate)"。

<a id="contextproperty"></a>

## <a name="how-to-get-information-about-the-client-from-the-context-property"></a>如何从上下文属性获取有关客户端的信息

要获取有关客户端的信息，`Context`请使用 Hub 类的属性。 该`Context`属性返回一个[HubCallerContext](https://msdn.microsoft.com/library/jj890883(v=vs.111).aspx)对象，该对象提供对以下信息的访问：

- 调用客户端的连接 ID。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample48.cs?highlight=1)]

    连接 ID 是由 SignalR 分配的 GUID（您无法在自己的代码中指定值）。 每个连接都有一个连接 ID，如果应用程序中有多个集线器，则所有集线器都使用相同的连接 ID。
- HTTP 标头数据。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample49.cs?highlight=1)]

    还可以从`Context.Headers`获取 HTTP 标头。 对同一事物`Context.Headers`的多次引用的原因是首先创建，`Context.Request`该属性在以后添加，并`Context.Headers`保留为向后兼容性。
- 查询字符串数据。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample50.cs?highlight=1)]

    还可以从`Context.QueryString`获取查询字符串数据。

    在此属性中获取的查询字符串是与建立 SignalR 连接的 HTTP 请求一起使用的查询字符串。 您可以通过配置连接在客户端中添加查询字符串参数，这是将有关客户端的数据从客户端传递到服务器的便捷方法。 下面的示例显示了在使用生成的代理时在 JavaScript 客户端中添加查询字符串的一种方法。

    [!code-javascript[Main](hubs-api-guide-server/samples/sample51.js?highlight=1)]

    有关设置查询字符串参数的详细信息，请参阅[JavaScript](hubs-api-guide-javascript-client.md)和[.NET](hubs-api-guide-net-client.md)客户端的 API 指南。

    您可以在查询字符串数据中找到用于连接的传输方法，以及 SignalR 内部使用的一些其他值：

    [!code-csharp[Main](hubs-api-guide-server/samples/sample52.cs)]

    的值`transportMethod`将是"webSocket"、"服务器发送事件"、"永久帧"或"长轮询"。 请注意，如果在`OnConnected`事件处理程序方法中检查此值，在某些情况下，最初可能会获取传输值，该值不是连接的最终协商传输方法。 在这种情况下，该方法将引发异常，并在建立最终传输方法时稍后再次调用。
- Cookie。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample53.cs?highlight=1)]

    您也可以从`Context.RequestCookies`获取 Cookie。
- 用户信息。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample54.cs?highlight=1)]
- 请求的 HttpContext 对象 ：

    [!code-csharp[Main](hubs-api-guide-server/samples/sample55.cs?highlight=1)]

    使用此方法，而不是获取`HttpContext.Current`SignalR`HttpContext`连接的对象。

<a id="passstate"></a>

## <a name="how-to-pass-state-between-clients-and-the-hub-class"></a>如何在客户端和中心类之间传递状态

客户端代理提供一个`state`对象，您可以在其中存储要通过每个方法调用传输到服务器的数据。 在服务器上，您可以在客户端调用的`Clients.Caller`Hub 方法中的属性中访问此数据。 不会`Clients.Caller`为连接生存期事件处理程序填充`OnConnected`属性 ，`OnDisconnected`和`OnReconnected`。

在`state`对象中创建或更新数据，`Clients.Caller`属性在两个方向上工作。 您可以更新服务器中的值，并将它们传回客户端。

下面的示例显示 JavaScript 客户端代码，该代码存储状态，以便通过每个方法调用传输到服务器。

[!code-javascript[Main](hubs-api-guide-server/samples/sample56.js?highlight=1-2)]

下面的示例显示了 .NET 客户端中的等效代码。

[!code-csharp[Main](hubs-api-guide-server/samples/sample57.cs?highlight=1-2)]

在 Hub 类中，您可以在`Clients.Caller`属性中访问此数据。 下面的示例显示检索上一个示例中引用的状态的代码。

[!code-csharp[Main](hubs-api-guide-server/samples/sample58.cs?highlight=3-4)]

> [!NOTE]
> 此持久状态机制不适用于大量数据，因为在`state`或`Clients.Caller`属性中放置的所有内容都随每个方法调用一起循环。 它对于较小的项目（如用户名或计数器）很有用。

在VB.NET或强类型中心中，无法通过`Clients.Caller`而是使用`Clients.CallerState`（在信号R 2.1 中介绍）：

**在 C 中使用调用方状态#**

[!code-csharp[Main](hubs-api-guide-server/samples/sample59.cs?highlight=3-4)]

**在可视化基础中使用调用方状态**

[!code-vb[Main](hubs-api-guide-server/samples/sample60.vb)]

<a id="handleErrors"></a>

## <a name="how-to-handle-errors-in-the-hub-class"></a>如何处理中心类中的错误

要处理在 Hub 类方法中发生的错误，首先请确保使用`await`"观察"异步操作（如调用客户端方法）中的任何异常。 然后使用以下一种或多种方法：

- 将方法代码包装在 try-catch 块中并记录异常对象。 出于调试目的，您可以将异常发送给客户端，但出于安全原因，不建议向生产中的客户端发送详细信息。
- 创建处理[On 传入错误](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubpipelinemodule.onincomingerror(v=vs.111).aspx)方法的集线器管道模块。 下面的示例显示了一个管道模块，该模块记录错误，然后是Startup.cs中的代码，该代码将模块注入到集线器管道中。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample61.cs)]

    [!code-csharp[Main](hubs-api-guide-server/samples/sample62.cs?highlight=4)]
- 使用类`HubException`（在 SignalR 2 中介绍）。 可以从任何集线器调用引发此错误。 构造`HubError`函数获取字符串消息和用于存储额外错误数据的对象。 SignalR 将自动序列化异常并将其发送到客户端，客户端将用于拒绝或失败集线器方法调用。

    以下代码示例演示如何在中心调用期间引发`HubException`，以及如何处理 JavaScript 和 .NET 客户端上的异常。

    **演示 HubException 类的服务器代码**

    [!code-csharp[Main](hubs-api-guide-server/samples/sample63.cs)]

    **JavaScript 客户端代码演示对在中心中引发 HubException 的响应**

    [!code-html[Main](hubs-api-guide-server/samples/sample64.html)]

    **.NET 客户端代码，用于响应在中心中引发 HubException**

    [!code-csharp[Main](hubs-api-guide-server/samples/sample65.cs)]

有关集线器管道模块的详细信息，请参阅本主题后面的[如何自定义中心管道](#hubpipeline)。

<a id="tracing"></a>

## <a name="how-to-enable-tracing"></a>如何启用跟踪

要启用服务器端跟踪，请向 Web.config 文件添加 system.诊断元素，如以下示例所示：

[!code-html[Main](hubs-api-guide-server/samples/sample66.html?highlight=17-72)]

在 Visual Studio 中运行应用程序时，可以在 **"输出"** 窗口中查看日志。

<a id="callfromoutsidehub"></a>

## <a name="how-to-call-client-methods-and-manage-groups-from-outside-the-hub-class"></a>如何调用客户端方法并管理来自中心类外部的组

要从与 Hub 类不同的类调用客户端方法，请获取对集线器的 SignalR 上下文对象的引用，并用它来调用客户端或管理组上的方法。

以下示例`StockTicker`类获取上下文对象，将其存储在类的实例中，将类实例存储在静态属性中，并使用 singleton 类实例中的上下文调用连接到名为`updateStockPrice``StockTickerHub`的 Hub 的客户端上的方法。

[!code-csharp[Main](hubs-api-guide-server/samples/sample67.cs?highlight=8,24)]

如果需要在长寿命对象中多次使用上下文，获取引用一次并保存它，而不是每次都再次获取它。 获取上下文一次可确保 SignalR 以与集线器方法进行客户端方法调用的顺序相同的顺序向客户端发送消息。 有关演示如何对集线器使用 SignalR 上下文的教程，请参阅[使用 ASP.NET SignalR 的服务器广播](../getting-started/tutorial-server-broadcast-with-signalr.md)。

<a id="callingclientsoutsidehub"></a>

### <a name="calling-client-methods"></a>调用客户端方法

您可以指定哪些客户端将收到 RPC，但与从中心类调用时相比，选项更少。 原因是上下文与来自客户端的特定调用不相关联，因此任何需要了解当前连接 ID 的方法（如`Clients.Others`或`Clients.Caller`或`Clients.OthersInGroup`或 ） 都不可用。 提供了以下选项：

- 所有已连接的客户端。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample68.cs)]
- 由连接 ID 标识的特定客户端。

    [!code-css[Main](hubs-api-guide-server/samples/sample69.css)]
- 除指定客户端外的所有连接客户端，由连接 ID 标识。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample70.cs)]
- 指定组中的所有连接客户端。

    [!code-css[Main](hubs-api-guide-server/samples/sample71.css)]
- 指定组中的所有连接客户端（指定客户端除外），由连接 ID 标识。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample72.cs)]

如果要从 Hub 类中的方法调用非 Hub 类，则可以将当前连接 ID`Clients.Client`传递，并将其用于 ，`Clients.AllExcept`或`Clients.Group`模拟`Clients.Caller`或`Clients.Others`。 `Clients.OthersInGroup` 在下面的示例中`MoveShapeHub`，类将连接 ID 传递给`Broadcaster`类，以便`Broadcaster`类可以模拟`Clients.Others`。

[!code-csharp[Main](hubs-api-guide-server/samples/sample73.cs?highlight=12,36)]

<a id="managinggroupsoutsidehub"></a>

### <a name="managing-group-membership"></a>管理组成员身份

对于管理组，您具有与在中心类中相同的选项。

- 将客户端添加到组

    [!code-csharp[Main](hubs-api-guide-server/samples/sample74.cs)]
- 从组中删除客户端

    [!code-css[Main](hubs-api-guide-server/samples/sample75.css)]

<a id="hubpipeline"></a>

## <a name="how-to-customize-the-hubs-pipeline"></a>如何自定义中心管道

SignalR 使您能够将您自己的代码注入集线器管道。 下面的示例显示了一个自定义 Hub 管道模块，该模块记录从客户端和在客户端上调用的传出方法调用收到的每个传入方法调用：

[!code-csharp[Main](hubs-api-guide-server/samples/sample76.cs)]

*Startup.cs*文件中的以下代码注册要在集线器管道中运行的模块：

[!code-csharp[Main](hubs-api-guide-server/samples/sample77.cs?highlight=3)]

您可以重写许多不同的方法。 有关完整列表，请参阅[HubPipeline 模块方法](https://msdn.microsoft.com/library/jj918633(v=vs.111).aspx)。

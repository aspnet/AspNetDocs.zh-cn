---
uid: signalr/overview/guide-to-the-api/hubs-api-guide-server
title: 'ASP.NET SignalR Hub API 指南-Server (c # ) |Microsoft Docs'
author: bradygaster
description: 本文档介绍如何对 SignalR 版本2的 ASP.NET SignalR Hub API 的服务器端进行编程，并提供代码示例演示 .。。
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: b19913e5-cd8a-4e4b-a872-5ac7a858a934
msc.legacyurl: /signalr/overview/guide-to-the-api/hubs-api-guide-server
msc.type: authoredcontent
ms.openlocfilehash: c681b104b15bfc4a04587c7abf685dcf20def2ca
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345373"
---
# <a name="aspnet-signalr-hubs-api-guide---server-c"></a>ASP.NET SignalR Hub API 指南-Server (c # ) 

作者： [Fletcher](https://github.com/pfletcher)， [Tom Dykstra](https://github.com/tdykstra)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 本文档介绍了如何对 SignalR 版本2的 ASP.NET SignalR Hub API 的服务器端编程，其中的代码示例演示了常见选项。
> 
> 通过 SignalR 中心 API，你可以 (Rpc) 从服务器连接到连接的客户端和从客户端到服务器的远程过程调用。 在服务器代码中，你将定义可由客户端调用的方法，并调用在客户端上运行的方法。 在客户端代码中，定义可从服务器调用的方法，并调用在服务器上运行的方法。 SignalR 负责处理所有的客户端到服务器的操作。
> 
> SignalR 还提供名为持久性连接的较低级别 API。 有关 SignalR、集线器和持续连接的简介，请参阅 [SignalR 2 简介](../getting-started/introduction-to-signalr.md)。
> 
> ## <a name="software-versions-used-in-this-topic"></a>本主题中使用的软件版本
> 
> 
> - [Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - .NET 4.5
> - SignalR 版本2
>   
> 
> 
> ## <a name="topic-versions"></a>主题版本
> 
> 有关早期版本的 SignalR 的信息，请参阅 [SignalR 旧版本](../older-versions/index.md)。
> 
> ## <a name="questions-and-comments"></a>问题和注释
> 
> 请提供有关你喜欢本教程的方式的反馈，并在页面底部的评论中留下反馈。 如果你有与本教程不直接相关的问题，则可以将其发布到 [ASP.NET SignalR 论坛](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 或 [StackOverflow.com](http://stackoverflow.com/)。

## <a name="overview"></a>概述

本文档包含以下各节：

- [如何注册 SignalR 中间件](#route)

    - [/Signalr URL](#signalrurl)
    - [配置 SignalR 选项](#options)
- [如何创建和使用集线器类](#hubclass)

    - [中心对象生存期](#transience)
    - [JavaScript 客户端中集线器名称的大小写大小写](#hubnames)
    - [多个中心](#multiplehubs)
    - [强类型中心](#stronglytypedhubs)
- [如何在 Hub 类中定义客户端可以调用的方法](#hubmethods)

    - [JavaScript 客户端中方法名称的大小写大小写](#methodnames)
    - [何时异步执行](#asyncmethods)
    - [定义重载](#overloads)
    - [报告集线器方法调用的进度](#progress)
- [如何从中心类调用客户端方法](#callfromhub)

    - [选择将接收 RPC 的客户端](#selectingclients)
    - [没有方法名称的编译时验证](#dynamicmethodnames)
    - [不区分大小写的方法名称匹配](#caseinsensitive)
    - [异步执行](#asyncclient)
- [如何从中心类管理组成员身份](#groupsfromhub)

    - [异步执行添加和移除方法](#asyncgroupmethods)
    - [组成员持久性](#grouppersistence)
    - [单用户组](#singleusergroups)
- [如何处理中心类中的连接生存期事件](#connectionlifetime)

    - [如果调用 OnConnected、OnDisconnected 和 OnReconnected](#onreconnected)
    - [未填充调用方状态](#nocallerstate)
- [如何从上下文属性获取有关客户端的信息](#contextproperty)
- [如何在客户端和中心类之间传递状态](#passstate)
- [如何处理中心类中的错误](#handleErrors)
- [如何从中心类的外部调用客户端方法和管理组](#callfromoutsidehub)

    - [调用客户端方法](#callingclientsoutsidehub)
    - [管理组成员身份](#managinggroupsoutsidehub)
- [如何启用跟踪](#tracing)
- [如何自定义集线器管道](#hubpipeline)

有关如何对客户端进行编程的文档，请参阅以下资源：

- [SignalR 中心 API 指南-JavaScript 客户端](hubs-api-guide-javascript-client.md)
- [SignalR 中心 API 指南-.NET 客户端](hubs-api-guide-net-client.md)

SignalR 2 的服务器组件只在 .NET 4.5 中提供。 运行 .NET 4.0 的服务器必须使用 SignalR v1. x。

<a id="route"></a>

## <a name="how-to-register-signalr-middleware"></a>如何注册 SignalR 中间件

若要定义客户端将用于连接到中心的路由，请 `MapSignalR` 在应用程序启动时调用方法。 `MapSignalR` 是类的 [扩展方法](https://msdn.microsoft.com/library/vstudio/bb383977.aspx) `OwinExtensions` 。 下面的示例演示如何使用 OWIN startup 类定义 SignalR Hub 路由。

[!code-csharp[Main](hubs-api-guide-server/samples/sample1.cs)]

如果要将 SignalR 功能添加到 ASP.NET MVC 应用程序，请确保将 SignalR 路由添加到其他路由之前。 有关详细信息，请参阅 [教程：入门与 SignalR 2 和 MVC 5 结合](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)。

<a id="signalrurl"></a>

### <a name="the-signalr-url"></a>/Signalr URL

默认情况下，客户端将用于连接到中心的路由 URL 为 "/signalr"。  (请勿将此 URL 与自动生成的 JavaScript 文件的 "/signalr/hubs" URL 混淆。 有关生成的代理的详细信息，请参阅 [SignalR 中心 API 指南-JavaScript 客户端-生成的代理及其功能](hubs-api-guide-javascript-client.md#genproxy)。 ) 

可能会出现一些特殊情况，使此基 URL 无法用于 SignalR;例如，你的项目中有一个名为 *signalr* 的文件夹，并且你不希望更改该名称。 在这种情况下，可以更改基 URL，如以下示例中所示 (将示例代码中的 "/signalr" 替换为所需 URL) 。

**指定 URL 的服务器代码**

[!code-csharp[Main](hubs-api-guide-server/samples/sample2.cs?highlight=1)]

**指定与生成的代理 (的 URL 的 JavaScript 客户端代码) **

[!code-javascript[Main](hubs-api-guide-server/samples/sample3.js?highlight=1)]

**用于指定 URL 的 JavaScript 客户端代码 (没有生成的代理) **

[!code-javascript[Main](hubs-api-guide-server/samples/sample4.js?highlight=1)]

**指定 URL 的 .NET 客户端代码**

[!code-csharp[Main](hubs-api-guide-server/samples/sample5.cs?highlight=1)]

<a id="options"></a>

### <a name="configuring-signalr-options"></a>配置 SignalR 选项

使用方法的重载 `MapSignalR` 可指定自定义 URL、自定义依赖关系解析程序和以下选项：

- 从浏览器客户端使用 CORS 或 JSONP 启用跨域调用。

    通常，当浏览器从加载页面时 `http://contoso.com` ，SignalR 连接位于同一域中 `http://contoso.com/signalr` 。 如果中的页 `http://contoso.com` 建立了到的连接 `http://fabrikam.com/signalr` ，则这是一个跨域连接。 出于安全原因，在默认情况下将禁用跨域连接。 有关详细信息，请参阅 [ASP.NET SignalR HUB API 指南-JavaScript 客户端-如何建立跨域连接](hubs-api-guide-javascript-client.md#crossdomain)。
- 启用详细的错误消息。

    出现错误时，SignalR 的默认行为是向客户端发送一条通知消息，而不会详细说明发生了什么情况。 不建议在生产环境中向客户端发送详细的错误信息，因为恶意用户可能会对你的应用程序使用该信息。 若要进行故障排除，可以使用此选项来暂时启用更丰富的错误报告。
- 禁用自动生成的 JavaScript 代理文件。

    默认情况下，会生成一个带有中心类代理的 JavaScript 文件，以响应 URL "/signalr/hubs"。 如果你不想使用 JavaScript 代理，或者要手动生成此文件并在客户端中引用物理文件，则可以使用此选项来禁用代理生成。 有关详细信息，请参阅 [SignalR 中心 API 指南-JavaScript 客户端-如何为 SignalR 生成的代理创建物理文件](hubs-api-guide-javascript-client.md#manualproxy)。

下面的示例演示如何在对方法的调用中指定 SignalR 连接 URL 和这些选项 `MapSignalR` 。 若要指定自定义 URL，请将示例中的 "/signalr" 替换为要使用的 URL。

[!code-csharp[Main](hubs-api-guide-server/samples/sample6.cs)]

<a id="hubclass"></a>

## <a name="how-to-create-and-use-hub-classes"></a>如何创建和使用集线器类

若要创建集线器，请创建一个从 [Signalr](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx)派生的类。 下面的示例演示了聊天应用程序的简单集线器类。

[!code-csharp[Main](hubs-api-guide-server/samples/sample7.cs)]

在此示例中，连接的客户端可以调用 `NewContosoChatMessage` 方法，在此情况下，接收的数据将广播到所有连接的客户端。

<a id="transience"></a>

### <a name="hub-object-lifetime"></a>中心对象生存期

不会在服务器上实例化 Hub 类或从自己的代码中调用其方法;SignalR 中心管道完成的所有操作。 SignalR 创建中心类的新实例，每次需要处理集线器操作时，例如客户端连接、断开连接或对服务器进行方法调用时。

由于 Hub 类的实例是暂时性的，因此不能使用它们来维护对下一个方法调用的状态。 每次服务器接收来自客户端的方法调用时，中心类的新实例就会处理该消息。 若要通过多个连接和方法调用来维护状态，请使用一些其他方法（如数据库）或中心类上的静态变量，或不是从派生的不同类 `Hub` 。 如果在内存中保留数据，则使用方法（如中心类上的静态变量）将在应用程序域回收时丢失数据。

如果要将消息从你自己的运行中心类的代码中发送到客户端，则无法通过实例化集线器类实例来执行此操作，但可以通过获取中心类的 SignalR 上下文对象的引用来执行此操作。 有关详细信息，请参阅本主题后面的 [如何从此中心类外部调用客户端方法和管理组](#callfromoutsidehub) 。

<a id="hubnames"></a>

### <a name="camel-casing-of-hub-names-in-javascript-clients"></a>JavaScript 客户端中集线器名称的大小写大小写

默认情况下，JavaScript 客户端使用类名的 camel 大小写形式引用中心。 SignalR 会自动进行此更改，以便 JavaScript 代码可以符合 JavaScript 约定。 前面的示例称为 `contosoChatHub` JavaScript 代码中的。

**服务器**

[!code-csharp[Main](hubs-api-guide-server/samples/sample8.cs?highlight=1)]

**使用生成的代理的 JavaScript 客户端**

[!code-javascript[Main](hubs-api-guide-server/samples/sample9.js?highlight=1)]

若要为客户端指定不同的名称，请添加 `HubName` 属性。 使用 `HubName` 属性时，JavaScript 客户端上不会更改为 camel 大小写的名称。

**服务器**

[!code-csharp[Main](hubs-api-guide-server/samples/sample10.cs?highlight=1)]

**使用生成的代理的 JavaScript 客户端**

[!code-javascript[Main](hubs-api-guide-server/samples/sample11.js?highlight=1)]

<a id="multiplehubs"></a>

### <a name="multiple-hubs"></a>多个中心

可以在一个应用程序中定义多个集线器类。 当你执行此操作时，将共享连接，但组是不同的：

- 如果你指定了一个) ，则所有客户端都将使用相同的 URL 来建立 SignalR 与你的 ( 服务的连接，并且该连接将用于该服务定义的所有中心。

    与定义单个类中的所有集线器功能相比，多个中心没有性能差异。
- 所有中心获取相同的 HTTP 请求信息。

    由于所有中心共享相同的连接，因此服务器获取的 HTTP 请求信息仅是建立 SignalR 连接的原始 HTTP 请求的信息。 如果使用连接请求通过指定查询字符串将信息从客户端传递到服务器，则不能向不同的中心提供不同的查询字符串。 所有集线器都将接收相同的信息。
- 生成的 JavaScript 代理文件将包含一个文件中所有中心的代理。

    有关 JavaScript 代理的信息，请参阅 [SignalR 中心 API 指南-JavaScript 客户端-生成的代理及其功能](hubs-api-guide-javascript-client.md#genproxy)。
- 组在中心内定义。

    在 SignalR 中，可以定义要广播到已连接的客户端子集的命名组。 为每个中心单独维护组。 例如，名为 "Administrators" 的组将包括类的一组客户端 `ContosoChatHub` ，相同的组名将为类引用一组不同的客户端 `StockTickerHub` 。

<a id="stronglytypedhubs"></a>
### <a name="strongly-typed-hubs"></a>Strongly-Typed 中心

若要为你的中心方法定义一个接口，使客户端可以引用 (并在中心方法上启用 Intellisense) ，请从 `Hub<T>` SignalR 2.1) 引入 (派生集线器，而不是 `Hub` ：

[!code-csharp[Main](hubs-api-guide-server/samples/sample12.cs)]

<a id="hubmethods"></a>

## <a name="how-to-define-methods-in-the-hub-class-that-clients-can-call"></a>如何在 Hub 类中定义客户端可以调用的方法

若要在要从客户端调用的中心公开方法，请声明一个公共方法，如以下示例中所示。

[!code-csharp[Main](hubs-api-guide-server/samples/sample13.cs?highlight=3)]

[!code-csharp[Main](hubs-api-guide-server/samples/sample14.cs?highlight=3)]

可以指定返回类型和参数（包括复杂类型和数组），就像在任何 c # 方法中一样。 您在参数中接收或返回到调用方的任何数据都通过使用 JSON 在客户端和服务器之间进行通信，而 SignalR 会自动处理复杂对象和对象数组的绑定。

<a id="methodnames"></a>

### <a name="camel-casing-of-method-names-in-javascript-clients"></a>JavaScript 客户端中方法名称的大小写大小写

默认情况下，JavaScript 客户端通过使用方法名称的 camel 大小写形式来引用中心方法。 SignalR 会自动进行此更改，以便 JavaScript 代码可以符合 JavaScript 约定。

**服务器**

[!code-csharp[Main](hubs-api-guide-server/samples/sample15.cs?highlight=1)]

**使用生成的代理的 JavaScript 客户端**

[!code-javascript[Main](hubs-api-guide-server/samples/sample16.js?highlight=1)]

若要为客户端指定不同的名称，请添加 `HubMethodName` 属性。

**服务器**

[!code-csharp[Main](hubs-api-guide-server/samples/sample17.cs?highlight=1)]

**使用生成的代理的 JavaScript 客户端**

[!code-javascript[Main](hubs-api-guide-server/samples/sample18.js?highlight=1)]

<a id="asyncmethods"></a>

### <a name="when-to-execute-asynchronously"></a>何时异步执行

如果该方法将是长时间运行的，或者必须执行涉及等待的工作（如数据库查找或 web 服务调用），则通过返回[任务](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx)来使中心方法异步， (替换返回 `void`) 或[任务 &lt; T &gt; ](https://msdn.microsoft.com/library/dd321424.aspx)对象， (替代 `T` 返回类型) 。 当你 `Task` 从方法返回对象时，SignalR 会等待 `Task` 完成，然后将已解包的结果发送回客户端，因此在客户端中编写方法调用的方式没有差别。

使中心方法异步可避免在使用 WebSocket 传输时阻止连接。 当集线器方法同步执行且传输为 WebSocket 时，将阻止来自同一客户端的集线器上的方法的后续调用，直到集线器方法完成。

下面的示例演示了编码为同步或异步运行的同一方法，后跟用于调用任一版本的 JavaScript 客户端代码。

**Synchronous**

[!code-csharp[Main](hubs-api-guide-server/samples/sample19.cs)]

**异步**

[!code-csharp[Main](hubs-api-guide-server/samples/sample20.cs?highlight=1,7-8)]

**使用生成的代理的 JavaScript 客户端**

[!code-javascript[Main](hubs-api-guide-server/samples/sample21.js)]

有关如何在 ASP.NET 4.5 中使用异步方法的详细信息，请参阅 [在 ASP.NET MVC 4 中使用异步方法](../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md)。

<a id="overloads"></a>

### <a name="defining-overloads"></a>定义重载

如果要定义方法的重载，每个重载中的参数数量必须不同。 如果只是通过指定不同的参数类型来区分重载，则中心类将编译，但当客户端尝试调用某个重载时，SignalR 服务将在运行时引发异常。

<a id="progress"></a>
### <a name="reporting-progress-from-hub-method-invocations"></a>报告集线器方法调用的进度

SignalR 2.1 添加了对 .NET 4.5 中引入的 [进度报告模式](https://blogs.msdn.com/b/dotnet/archive/2012/06/06/async-in-4-5-enabling-progress-and-cancellation-in-async-apis.aspx) 的支持。 若要实现进度报告，请 `IProgress<T>` 为你的客户端可以访问的中心方法定义一个参数：

[!code-csharp[Main](hubs-api-guide-server/samples/sample22.cs)]

编写长时间运行的服务器方法时，应使用异步编程模式（如 Async/Await），而不是阻止集线器线程。

<a id="callfromhub"></a>

## <a name="how-to-call-client-methods-from-the-hub-class"></a>如何从中心类调用客户端方法

若要从服务器调用客户端方法，请在 `Clients` 中心类的方法中使用属性。 下面的示例演示了 `addNewMessageToPage` 在所有连接的客户端上调用的服务器代码，以及在 JavaScript 客户端中定义方法的客户端代码。

**服务器**

[!code-csharp[Main](hubs-api-guide-server/samples/sample23.cs?highlight=5)]

调用客户端方法是异步操作，并返回 `Task` 。 使用 `await`：

* 确保消息发送时不出错。 
* 启用捕获和处理 try-catch 块中的错误。

**使用生成的代理的 JavaScript 客户端**

[!code-html[Main](hubs-api-guide-server/samples/sample24.html?highlight=1)]

无法从客户端方法获取返回值;等语法 `int x = Clients.All.add(1,1)` 不起作用。

可以指定复杂类型和参数的数组。 下面的示例将一个复杂类型传递给方法参数中的客户端。

**使用复杂对象调用客户端方法的服务器代码**

[!code-csharp[Main](hubs-api-guide-server/samples/sample25.cs?highlight=3)]

**定义复杂对象的服务器代码**

[!code-csharp[Main](hubs-api-guide-server/samples/sample26.cs?highlight=1)]

**使用生成的代理的 JavaScript 客户端**

[!code-javascript[Main](hubs-api-guide-server/samples/sample27.js?highlight=2-3)]

<a id="selectingclients"></a>

### <a name="selecting-which-clients-will-receive-the-rpc"></a>选择将接收 RPC 的客户端

Clients 属性返回一个 [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx) 对象，该对象提供几个选项用于指定哪些客户端将接收 RPC：

- 所有已连接的客户端。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample28.cs)]
- 仅调用客户端。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample29.cs)]
- 除调用客户端之外的所有客户端。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample30.cs)]
- 由连接 ID 标识的特定客户端。

    [!code-css[Main](hubs-api-guide-server/samples/sample31.css)]

    此示例 `addContosoChatMessageToPage` 在调用客户端上调用，其效果与使用相同 `Clients.Caller` 。
- 除指定客户端之外的所有连接的客户端，由连接 ID 标识。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample32.cs)]
- 指定组中的所有连接的客户端。

    [!code-css[Main](hubs-api-guide-server/samples/sample33.css)]
- 指定组中除指定的客户端之外的所有连接的客户端，由连接 ID 标识。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample34.cs)]
- 指定组中除调用客户端之外的所有连接的客户端。

    [!code-css[Main](hubs-api-guide-server/samples/sample35.css)]
- 由 userId 标识的特定用户。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample36.cs)]

    默认情况下，此为 `IPrincipal.Identity.Name` ，但可以通过 [向全局主机注册 IUserIdProvider 的实现](mapping-users-to-connections.md#IUserIdProvider)来更改此值。
- 连接 Id 列表中的所有客户端和组。

    [!code-css[Main](hubs-api-guide-server/samples/sample37.css)]
- 组的列表。

    [!code-css[Main](hubs-api-guide-server/samples/sample38.css)]
- 按名称的用户。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample39.cs)]
-  (在 SignalR 2.1) 中引入的用户名列表。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample40.cs)]

<a id="dynamicmethodnames"></a>

### <a name="no-compile-time-validation-for-method-names"></a>没有方法名称的编译时验证

指定的方法名称被解释为动态对象，这意味着它没有 IntelliSense 或编译时验证。 在运行时计算表达式。 当执行方法调用时，SignalR 会将方法名称和参数值发送到客户端，如果客户端具有与名称匹配的方法，则调用该方法，并将参数值传递给该方法。 如果在客户端上找不到匹配的方法，则不会引发错误。 有关在调用客户端方法时 SignalR 传输到后台客户端的数据格式的信息，请参阅 [SignalR 简介](../getting-started/introduction-to-signalr.md)。

<a id="caseinsensitive"></a>

### <a name="case-insensitive-method-name-matching"></a>不区分大小写的方法名称匹配

方法名称匹配不区分大小写。 例如， `Clients.All.addContosoChatMessageToPage` 在服务器上，将在 `AddContosoChatMessageToPage` 客户端上执行、 `addcontosochatmessagetopage` 或 `addContosoChatMessageToPage` 。

<a id="asyncclient"></a>

### <a name="asynchronous-execution"></a>异步执行

调用的方法以异步方式执行。 对客户端调用方法之后的任何代码都将立即执行，而无需等待 SignalR 完成将数据传输到客户端的操作，除非指定后续代码行应等待方法完成。 下面的代码示例演示如何按顺序执行两个客户端方法。

**使用 Await ( .NET 4.5) **

[!code-csharp[Main](hubs-api-guide-server/samples/sample41.cs?highlight=1,3)]

如果你使用 `await` 等待，直到客户端方法在下一行代码执行之前完成，这并不意味着客户端将在执行下一行代码之前实际接收消息。 仅客户端方法调用的 "完成" 表示 SignalR 已完成发送消息所需的所有操作。 如果需要客户端接收消息的验证，则必须自行编写该机制。 例如，你可以在 `MessageReceived` 中心上编写方法的代码，并在你 `addContosoChatMessageToPage` `MessageReceived` 执行需要在客户端上执行的任何工作的客户端上的方法中调用。 在 `MessageReceived` 中心的中，你可以执行任何操作，具体取决于原始方法调用的实际客户端接收和处理。

### <a name="how-to-use-a-string-variable-as-the-method-name"></a>如何使用字符串变量作为方法名称

如果要通过使用字符串变量作为方法名称来调用客户端方法，请 `Clients.All` `Clients.Others` 将 )  (或、等， `Clients.Caller` `IClientProxy` 然后调用， [ (方法名称，参数 ... ) ](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.iclientproxy.invoke(v=vs.111).aspx)。

[!code-csharp[Main](hubs-api-guide-server/samples/sample42.cs)]

<a id="groupsfromhub"></a>

## <a name="how-to-manage-group-membership-from-the-hub-class"></a>如何从中心类管理组成员身份

SignalR 中的组提供一种方法，用于将消息广播到连接的已连接客户端的指定子集。 一个组可以具有任意数量的客户端，客户端可以是任意数量的组的成员。

若要管理组成员身份，请使用 Hub 类的属性提供的 [添加](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) 和 [移除](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) 方法 `Groups` 。 下面的示例演示了 `Groups.Add` `Groups.Remove` 在由客户端代码调用的集线器方法中使用的和方法，并后跟了调用它们的 JavaScript 客户端代码。

**服务器**

[!code-csharp[Main](hubs-api-guide-server/samples/sample43.cs?highlight=5,10)]

**使用生成的代理的 JavaScript 客户端**

[!code-javascript[Main](hubs-api-guide-server/samples/sample44.js)]

[!code-javascript[Main](hubs-api-guide-server/samples/sample45.js)]

无需显式创建组。 实际上，在对的调用中首次指定组的名称时，会自动创建一个组 `Groups.Add` ，并在从其成员身份中删除最后一个连接时将其删除。

没有用于获取组成员身份列表或组列表的 API。 SignalR 基于发布 [/订阅模型](http://en.wikipedia.org/wiki/Publish/subscribe)将消息发送到客户端和组，并且服务器不维护组或组成员身份列表。 这有助于最大程度地提高可伸缩性，因为每次将节点添加到 web 场时，SignalR 维护的任何状态都必须传播到新节点。

<a id="asyncgroupmethods"></a>

### <a name="asynchronous-execution-of-add-and-remove-methods"></a>异步执行添加和移除方法

`Groups.Add`和 `Groups.Remove` 方法以异步方式执行。 如果要将客户端添加到组，并使用组立即将消息发送到客户端，必须确保 `Groups.Add` 方法首先完成。 下面的代码示例演示如何执行此操作。

**将客户端添加到组，然后将客户端发送到客户端**

[!code-csharp[Main](hubs-api-guide-server/samples/sample46.cs?highlight=1,3)]

<a id="grouppersistence"></a>

### <a name="group-membership-persistence"></a>组成员持久性

SignalR 跟踪连接，而不是用户，因此，如果希望用户在每次建立连接时都位于同一个组中，则必须在 `Groups.Add` 每次用户建立新连接时调用。

暂时断开连接后，SignalR 可能会自动恢复连接。 在这种情况下，SignalR 将还原相同的连接，而不建立新的连接，因此客户端的组成员身份将自动还原。 即使暂时中断是服务器重启或失败的结果，也可能出现这种情况，因为每个客户端（包括组成员身份）的连接状态都将往返给客户端。 如果服务器发生故障，并且在连接超时之前被新服务器替换，则客户端可以自动重新连接到新的服务器并重新注册其所属的组。

当连接丢失或连接超时时，或者当客户端断开连接时，如果无法自动还原连接 (例如，当浏览器导航到新页面) 时，组成员身份将丢失。 用户下次连接时将是新连接。 若要在同一个用户建立新连接时维护组成员身份，你的应用程序必须跟踪用户和组之间的关联，并在每次用户建立新连接时还原组成员身份。

有关连接和重新连接的详细信息，请参阅本主题后面的 [如何处理 Hub 类中的连接生存期事件](#connectionlifetime) 。

<a id="singleusergroups"></a>

### <a name="single-user-groups"></a>单用户组

使用 SignalR 的应用程序通常需要跟踪用户和连接之间的关联，以便知道哪个用户已发送消息，哪些用户 () 应接收消息。 组用于执行此操作的两种常用模式之一。

- 单用户组。

    你可以指定用户名作为组名称，并在每次用户连接或重新连接时将当前连接 ID 添加到组。 向发送到组的用户发送消息。 此方法的缺点是，组不会提供一种方法来找出用户处于联机还是脱机状态。
- 跟踪用户名和连接 Id 之间的关联。

    你可以在每个用户名与字典或数据库中的一个或多个连接 Id 之间存储关联，并在每次用户连接或断开连接时更新存储的数据。 若要向用户发送消息，请指定连接 Id。 此方法的一个缺点是它会占用更多内存。

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events-in-the-hub-class"></a>如何处理中心类中的连接生存期事件

处理连接生存期事件的典型原因是跟踪用户是否已连接，以及跟踪用户名和连接 Id 之间的关联。 若要在客户端连接或断开连接时运行你自己的代码，请重写 `OnConnected` `OnDisconnected` Hub 类的、和 `OnReconnected` 虚方法，如以下示例中所示。

[!code-csharp[Main](hubs-api-guide-server/samples/sample47.cs?highlight=3,14,22)]

<a id="onreconnected"></a>

### <a name="when-onconnected-ondisconnected-and-onreconnected-are-called"></a>如果调用 OnConnected、OnDisconnected 和 OnReconnected

每次浏览器导航到新页时，必须建立新的连接，这意味着 SignalR 将执行方法， `OnDisconnected` 然后执行 `OnConnected` 方法。 建立新连接时，SignalR 始终创建新的连接 ID。

`OnReconnected`当连接中存在临时中断时，SignalR 可以自动从中恢复，如在连接超时之前，电缆暂时断开连接并重新连接。`OnDisconnected`当客户端断开连接并且 SignalR 无法自动重新连接时（例如，当浏览器导航到新页面时），将调用方法。 因此，给定客户端的可能的事件序列为 `OnConnected` 、 `OnReconnected` 、、 `OnDisconnected` 或 `OnConnected` `OnDisconnected` 。 `OnConnected` `OnDisconnected` 对于给定的连接，不会显示序列 `OnReconnected` 。

`OnDisconnected`在某些情况下（例如服务器出现故障或应用程序域回收时）不会调用方法。 当另一个服务器联机或应用程序域完成其回收时，某些客户端可能能够重新连接并激发该 `OnReconnected` 事件。

有关详细信息，请参阅 [了解和处理 SignalR 中的连接生存期事件](handling-connection-lifetime-events.md)。

<a id="nocallerstate"></a>

### <a name="caller-state-not-populated"></a>未填充调用方状态

连接生存期事件处理程序方法是从服务器调用的，这意味着你在客户端上的对象中放置的任何状态 `state` 不会在 `Caller` 服务器上的属性中填充。 有关 `state` 对象和属性的信息 `Caller` ，请参阅本主题后面的 [如何在客户端和中心类之间传递状态](#passstate) 。

<a id="contextproperty"></a>

## <a name="how-to-get-information-about-the-client-from-the-context-property"></a>如何从上下文属性获取有关客户端的信息

若要获取有关客户端的信息，请使用 `Context` Hub 类的属性。 `Context`属性返回一个[HubCallerContext](https://msdn.microsoft.com/library/jj890883(v=vs.111).aspx)对象，该对象提供对以下信息的访问：

- 调用客户端的连接 ID。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample48.cs?highlight=1)]

    连接 ID 是 SignalR 分配的 GUID， (您不能在自己的代码) 中指定该值。 每个连接都有一个连接 ID，如果应用程序中有多个中心，则所有中心都将使用相同的连接 ID。
- HTTP 标头数据。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample49.cs?highlight=1)]

    你还可以从获取 HTTP 标头 `Context.Headers` 。 对同一项的多个引用的原因是： `Context.Headers` 首先创建了属性， `Context.Request` 后来添加了该属性，并保留该属性 `Context.Headers` 以实现向后兼容性。
- 查询字符串数据。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample50.cs?highlight=1)]

    您还可以从获取查询字符串数据 `Context.QueryString` 。

    在此属性中获取的查询字符串是与建立 SignalR 连接的 HTTP 请求一起使用的查询字符串。 您可以通过配置连接在客户端中添加查询字符串参数，这是将客户端的数据从客户端传递到服务器的一种简便方法。 下面的示例演示了在使用生成的代理时在 JavaScript 客户端中添加查询字符串的一种方法。

    [!code-javascript[Main](hubs-api-guide-server/samples/sample51.js?highlight=1)]

    有关设置查询字符串参数的详细信息，请参阅 [JavaScript](hubs-api-guide-javascript-client.md) 和 [.net](hubs-api-guide-net-client.md) 客户端的 API 指南。

    可以在查询字符串数据中找到用于连接的传输方法，还可以在 SignalR 内部使用某些其他值：

    [!code-csharp[Main](hubs-api-guide-server/samples/sample52.cs)]

    的值 `transportMethod` 将为 "websocket"、"serverSentEvents"、"foreverFrame" 或 "longPolling"。 请注意，如果在 `OnConnected` 事件处理程序方法中检查此值，则在某些情况下，最初可能会获得一个传输值，该值不是连接的最终协商传输方法。 在这种情况下，方法将引发异常，稍后在建立最终传输方法时将再次调用该方法。
- Cookie。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample53.cs?highlight=1)]

    你还可以从获取 cookie `Context.RequestCookies` 。
- 用户信息。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample54.cs?highlight=1)]
- 请求的 HttpContext 对象：

    [!code-csharp[Main](hubs-api-guide-server/samples/sample55.cs?highlight=1)]

    使用此方法，而不是获取 `HttpContext.Current` 以获取 `HttpContext` SignalR 连接的对象。

<a id="passstate"></a>

## <a name="how-to-pass-state-between-clients-and-the-hub-class"></a>如何在客户端和中心类之间传递状态

客户端代理提供一个 `state` 对象，您可以在其中存储要使用每个方法调用传输到服务器的数据。 在服务器上，可以 `Clients.Caller` 通过客户端调用的集线器方法中的属性访问此数据。 `Clients.Caller`对于连接生存期事件处理程序方法 `OnConnected` （和），不填充属性 `OnDisconnected` `OnReconnected` 。

创建或更新对象中的数据 `state` ， `Clients.Caller` 属性在这两个方向上都有效。 您可以更新服务器中的值，并将这些值传递回客户端。

下面的示例演示了 JavaScript 客户端代码，该代码存储每个方法调用的用于传输到服务器的状态。

[!code-javascript[Main](hubs-api-guide-server/samples/sample56.js?highlight=1-2)]

下面的示例演示 .NET 客户端中的等效代码。

[!code-csharp[Main](hubs-api-guide-server/samples/sample57.cs?highlight=1-2)]

在你的中心类中，你可以在属性中访问此数据 `Clients.Caller` 。 下面的示例演示了检索上一示例中引用的状态的代码。

[!code-csharp[Main](hubs-api-guide-server/samples/sample58.cs?highlight=3-4)]

> [!NOTE]
> 用于保持状态的这种机制不适用于大量数据，因为在或属性中放置的所有 `state` 内容 `Clients.Caller` 都将随每个方法调用一起往返。 它适用于较小的项，例如用户名或计数器。

在 VB.NET 中或在强类型的中心内，无法通过访问调用方状态对象 `Clients.Caller` ; 而是使用 `Clients.CallerState` SignalR 2.1 中引入的 () ：

**在 C 中使用 CallerState#**

[!code-csharp[Main](hubs-api-guide-server/samples/sample59.cs?highlight=3-4)]

**在 Visual Basic 中使用 CallerState**

[!code-vb[Main](hubs-api-guide-server/samples/sample60.vb)]

<a id="handleErrors"></a>

## <a name="how-to-handle-errors-in-the-hub-class"></a>如何处理中心类中的错误

若要处理中心类方法中发生的错误，请首先确保 "观察" 异步操作的任何异常 (如通过使用调用客户端方法) `await` 。 然后，使用以下一种或多种方法：

- 在 try-catch 块中包装方法代码，并记录 exception 对象。 出于调试目的，您可以将异常发送到客户端，但出于安全原因，不建议将详细信息发送到生产中的客户端。
- 创建处理 [OnIncomingError](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubpipelinemodule.onincomingerror(v=vs.111).aspx) 方法的集线器管道模块。 下面的示例演示一个管道模块，该模块记录错误，然后是 Startup.cs 中的代码，该模块将模块注入集线器管道。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample61.cs)]

    [!code-csharp[Main](hubs-api-guide-server/samples/sample62.cs?highlight=4)]
- 使用 `HubException` SignalR 2) 中引入的类 (。 任何集线器调用都可能会引发此错误。 `HubError`构造函数采用字符串消息和用于存储额外错误数据的对象。 SignalR 会自动将异常序列化，并将其发送到客户端，该客户端将用于拒绝或拒绝集线器方法调用。

    下面的代码示例演示如何在 `HubException` 中心调用期间引发，以及如何在 JavaScript 和 .net 客户端上处理异常。

    **演示 HubException 类的服务器代码**

    [!code-csharp[Main](hubs-api-guide-server/samples/sample63.cs)]

    **JavaScript 客户端代码演示在中心引发 HubException 的响应**

    [!code-html[Main](hubs-api-guide-server/samples/sample64.html)]

    **.NET 客户端代码演示在中心引发 HubException 的响应**

    [!code-csharp[Main](hubs-api-guide-server/samples/sample65.cs)]

有关集线器管道模块的详细信息，请参阅本主题后面的 [如何自定义集线器管道](#hubpipeline) 。

<a id="tracing"></a>

## <a name="how-to-enable-tracing"></a>如何启用跟踪

若要启用服务器端跟踪，请将一个 "诊断" 元素添加到 Web.config 文件中，如以下示例中所示：

[!code-html[Main](hubs-api-guide-server/samples/sample66.html?highlight=17-72)]

在 Visual Studio 中运行应用程序时，可以在 " **输出** " 窗口中查看日志。

<a id="callfromoutsidehub"></a>

## <a name="how-to-call-client-methods-and-manage-groups-from-outside-the-hub-class"></a>如何从中心类的外部调用客户端方法和管理组

若要从不同于中心类的类调用客户端方法，请获取对中心的 SignalR 上下文对象的引用，并使用该对象调用客户端上的方法或管理组。

下面的示例 `StockTicker` 类获取上下文对象，将其存储在类的实例中，将类实例存储在静态属性中，并使用 singleton 类实例中的上下文在 `updateStockPrice` 连接到名为的集线器的客户端上调用方法 `StockTickerHub` 。

[!code-csharp[Main](hubs-api-guide-server/samples/sample67.cs?highlight=8,24)]

如果需要在长生存期的对象中多次使用上下文，请获取引用一次并保存，而不是每次都重新获取。 只要获取上下文，就可以确保 SignalR 将消息以集线器方法发出客户端方法调用的相同顺序发送到客户端。 有关演示如何使用集线器的 SignalR 上下文的教程，请参阅 [使用 ASP.NET SignalR 进行服务器广播](../getting-started/tutorial-server-broadcast-with-signalr.md)。

<a id="callingclientsoutsidehub"></a>

### <a name="calling-client-methods"></a>调用客户端方法

您可以指定将接收 RPC 的客户端，但选择的选项比从集线器类调用时更少。 出现这种情况的原因是上下文未与客户端的特定调用相关联，因此，任何需要了解当前连接 ID 的方法（如 `Clients.Others` 、或）都不可 `Clients.Caller` `Clients.OthersInGroup` 用。 提供了以下选项：

- 所有已连接的客户端。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample68.cs)]
- 由连接 ID 标识的特定客户端。

    [!code-css[Main](hubs-api-guide-server/samples/sample69.css)]
- 除指定客户端之外的所有连接的客户端，由连接 ID 标识。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample70.cs)]
- 指定组中的所有连接的客户端。

    [!code-css[Main](hubs-api-guide-server/samples/sample71.css)]
- 指定组中除指定的客户端之外的所有连接的客户端，由连接 ID 标识。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample72.cs)]

如果要从中心类中的方法调用到非集线器类，可以传入当前连接 ID 并将其与 `Clients.Client` 、或一起使用 `Clients.AllExcept` `Clients.Group` 来模拟 `Clients.Caller` 、 `Clients.Others` 或 `Clients.OthersInGroup` 。 在下面的示例中， `MoveShapeHub` 类将连接 ID 传递到 `Broadcaster` 类，以便 `Broadcaster` 该类可以进行模拟 `Clients.Others` 。

[!code-csharp[Main](hubs-api-guide-server/samples/sample73.cs?highlight=12,36)]

<a id="managinggroupsoutsidehub"></a>

### <a name="managing-group-membership"></a>管理组成员身份

对于管理组，你具有与在 Hub 类中相同的选项。

- 将客户端添加到组

    [!code-csharp[Main](hubs-api-guide-server/samples/sample74.cs)]
- 从组中删除客户端

    [!code-css[Main](hubs-api-guide-server/samples/sample75.css)]

<a id="hubpipeline"></a>

## <a name="how-to-customize-the-hubs-pipeline"></a>如何自定义集线器管道

SignalR 使你能够将自己的代码注入中心管道。 下面的示例演示一个自定义中心管道模块，该模块记录从客户端接收的每个传入方法调用，以及在客户端上调用的传出方法调用：

[!code-csharp[Main](hubs-api-guide-server/samples/sample76.cs)]

*Startup.cs*文件中的以下代码将在中心管道中注册要运行的模块：

[!code-csharp[Main](hubs-api-guide-server/samples/sample77.cs?highlight=3)]

有许多不同的方法可以重写。 有关完整列表，请参阅 [HubPipelineModule 方法](https://msdn.microsoft.com/library/jj918633(v=vs.111).aspx)。

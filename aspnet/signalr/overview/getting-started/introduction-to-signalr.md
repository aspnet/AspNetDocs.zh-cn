---
uid: signalr/overview/getting-started/introduction-to-signalr
title: SignalR 简介 |Microsoft Docs
author: bradygaster
description: 本文介绍了什么是 SignalR 以及它旨在创建的一些解决方案。
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 0fab5e35-8c1f-43d4-8635-b8aba8766a71
msc.legacyurl: /signalr/overview/getting-started/introduction-to-signalr
msc.type: authoredcontent
ms.openlocfilehash: 76e8fd03292eafa4b0b579ee1746fb54b57ac66b
ms.sourcegitcommit: 45754124123403520b9fa2e706a4d1292494159b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/10/2020
ms.locfileid: "89643678"
---
# <a name="introduction-to-signalr"></a>SignalR 简介

作者： [Fletcher](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 本文介绍了什么是 SignalR 以及它旨在创建的一些解决方案。 
> 
> ## <a name="questions-and-comments"></a>问题和注释
> 
> 请提供有关你喜欢本教程的方式的反馈，并在页面底部的评论中留下反馈。 如果你有与本教程不直接相关的问题，则可以将其发布到 [ASP.NET SignalR 论坛](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 或 [StackOverflow.com](https://stackoverflow.com/questions/tagged/signalr)。

## <a name="what-is-signalr"></a>什么是 SignalR？

ASP.NET SignalR 是 ASP.NET 开发人员的库，可简化将实时 web 功能添加到应用程序的过程。 实时 web 功能使服务器代码能够在可用时立即将内容推送到连接的客户端，而不是让服务器等待客户端请求新的数据。

SignalR 可用于将任何种类的 "实时" web 功能添加到 ASP.NET 应用程序。 尽管聊天通常用作示例，但你可以执行更多操作。 用户每次刷新网页以查看新数据，或者页面实现 [长轮询](http://en.wikipedia.org/wiki/Push_technology#Long_polling) 来检索新数据时，都是使用 SignalR 的候选项。 示例包括仪表板和监视应用程序、协作应用程序 (例如同步编辑文档) 、作业进度更新和实时窗体。

SignalR 还启用了全新类型的 web 应用程序，这些应用程序需要服务器中的高频率更新，例如，实时游戏。

SignalR 提供了一个简单的 API，用于创建 (RPC) 的服务器到客户端远程过程调用，该程序调用客户端浏览器中的 JavaScript 函数 (和从服务器端 .NET 代码) 的其他客户端平台。 SignalR 还包括用于连接管理的 API (例如，连接和断开连接事件) ，以及对连接进行分组。

![通过 SignalR 调用方法](introduction-to-signalr/_static/image1.png)

SignalR 自动处理连接管理，让你可同时向所有连接的客户端广播消息，就像聊天室一样。 也可以向特定客户端发送消息。 客户端和服务器之间的连接是持久的，不同于传统的 HTTP 连接，后者针对每次通信重新建立。

SignalR 支持 "服务器推送" 功能，在该功能中，服务器代码可以使用远程过程调用来调用浏览器中的客户端代码 (RPC) ，而不是目前在 web 上通用的请求-响应模式。

使用内置和第三方横向扩展提供程序，SignalR 应用程序可以向外扩展到数千个客户端。

内置提供程序包括：
* [服务总线](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.ServiceBus3)
* [SQL Server](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.SqlServer)
* [Redis](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.Redis)

第三方提供程序包括：
* [NCache](https://www.alachisoft.com/ncache/asp-net-core-signalr.html)。

SignalR 是开放源代码，可通过 [GitHub](https://github.com/signalr)访问。

## <a name="signalr-and-websocket"></a>SignalR 和 WebSocket

SignalR 使用新的 WebSocket 传输（如果可用），并在必要时回退到较旧的传输。 虽然当然，你可以直接使用 WebSocket 编写应用，但使用 SignalR 意味着你需要实现的很多额外功能都已完成。 最重要的是，这意味着您可以对应用程序进行编码，以便利用 WebSocket，而不必担心为较旧的客户端创建单独的代码路径。 SignalR 还会使你不必担心对 WebSocket 的更新，因为 SignalR 会更新为支持基础传输中的更改，从而为你的应用程序提供跨 WebSocket 版本的一致接口。

<a id="transports"></a>

## <a name="transports-and-fallbacks"></a>传输和回退

SignalR 是对在客户端和服务器之间进行实时工作所需的某些传输的抽象。 如果可能，SignalR 将首先尝试建立 WebSocket 连接。 WebSocket 是 SignalR 的最佳传输，因为它具有以下内容：

* 最有效地使用服务器内存。
* 延迟最低。
* 最底层的功能，如客户端和服务器之间的全双工通信。
* 最严格的要求是，WebSocket 需要服务器：
  * 在 Windows Server 2012 或 Windows 8 上运行。
  * .NET Framework 4.5。

如果未满足这些要求，则 SignalR 会尝试使用其他传输进行连接。

### <a name="html-5-transports"></a>HTML 5 传输

这些传输依赖于对 [HTML 5](http://en.wikipedia.org/wiki/HTML5)的支持。 如果客户端浏览器不支持 HTML 5 标准版，将使用较旧的传输。

- **Websocket** (如果服务器和浏览器都指示它们可以支持 WebSocket) 。 WebSocket 是在客户端与服务器之间建立真正持久的双向连接的唯一传输。 但是，WebSocket 还具有最严格的要求;它仅在最新版本的 Microsoft Internet Explorer、Google Chrome 和 Mozilla Firefox 中完全受支持，并且在某些浏览器（如 Opera 和 Safari）中仅有部分实现。
- 如果浏览器支持服务器发送事件（基本上是 Internet Explorer 之外的所有浏览器），**服务器发送事件**（也称为 EventSource (）。 ) 

### <a name="comet-transports"></a>Comet 传输

以下传输基于 [Comet](http://en.wikipedia.org/wiki/Comet_(programming)) web 应用程序模型，在该模型中，浏览器或其他客户端维护长时间的 HTTP 请求，服务器可以使用该模型将数据推送到客户端，而客户端无需专门请求它。

- 仅) Internet Explorer (的 "**永久帧**"。 永久帧创建一个隐藏的 IFrame，该 IFrame 向服务器上不能完成的终结点发出请求。 服务器随后会持续向客户端发送脚本，该脚本会立即执行，提供从服务器到客户端的单向实时连接。 从客户端到服务器的连接使用与服务器之间的单独连接连接到客户端连接，与标准 HTTP 请求一样，为需要发送的每个数据段创建新连接。
- **Ajax 长轮询**。 长轮询不会创建持续性连接，而是使用保持打开状态的请求轮询服务器，直到服务器响应为止，此时连接将关闭，并立即请求新连接。 在连接重置时，这可能会导致一些延迟。

有关在哪些配置下支持哪些传输的详细信息，请参阅 [支持的平台](supported-platforms.md)。

### <a name="transport-selection-process"></a>传输选择过程

以下列表显示了 SignalR 用于确定要使用的传输的步骤。

1. 如果浏览器是 Internet Explorer 8 或更早版本，则使用长轮询。
2. 如果 JSONP 配置为 (即，则在 `jsonp` `true` 启动连接) 时，参数设置为，使用长轮询。
3. 如果正在建立跨域连接 (即，如果 SignalR 终结点与托管页) 不在同一域中，则在满足以下条件时将使用 WebSocket：

   - 客户端支持 CORS (跨域资源共享) 。 有关哪些客户端支持 CORS 的详细信息，请参阅 [caniuse.com 上的 cors](http://www.caniuse.com/CORS)。
   - 客户端支持 WebSocket
   - 服务器支持 WebSocket

     如果未满足这些条件中的任何一个，将使用长轮询。 有关跨域连接的详细信息，请参阅 [如何建立跨域连接](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)。
4. 如果未配置 JSONP 并且连接不跨域，则在客户端和服务器均支持时，将使用 WebSocket。
5. 如果客户端或服务器不支持 WebSocket，则使用服务器发送事件（如果可用）。
6. 如果 "服务器发送事件" 不可用，则将尝试永久帧。
7. 如果永久帧失败，则使用长轮询。

<a id="MonitoringTransports"></a>
### <a name="monitoring-transports"></a>监视传输

可以通过在中心启用日志记录，并在浏览器中打开控制台窗口，来确定应用程序使用的传输方式。

若要在浏览器中为中心的事件启用日志记录，请将以下命令添加到客户端应用程序：

`$.connection.hub.logging = true;`

- 在 Internet Explorer 中，按 F12 打开开发人员工具，然后单击 "控制台" 选项卡。

    ![Microsoft Internet Explorer 中的控制台](introduction-to-signalr/_static/image2.png)
- 在 Chrome 中，按 Ctrl + Shift + J 打开控制台。

    ![Google Chrome 中的控制台](introduction-to-signalr/_static/image3.png)

启用控制台打开并启用日志记录后，你将能够查看 SignalR 所使用的传输。

![Internet Explorer 中显示 WebSocket 传输的控制台](introduction-to-signalr/_static/image4.png)

### <a name="specifying-a-transport"></a>指定传输

协商传输会占用一定的时间和客户端/服务器资源。 如果客户端功能已知，则可以在启动客户端连接时指定传输。 下面的代码段演示如何使用 Ajax 长轮询传输开始连接，如果已知客户端不支持任何其他协议，则使用该连接：

`connection.start({ transport: 'longPolling' });`

如果希望客户端按顺序尝试特定传输，可以指定回退顺序。 下面的代码片段演示了如何尝试 WebSocket，并失败了，这将直接转到长轮询。

`connection.start({ transport: ['webSockets','longPolling'] });`

用于指定传输的字符串常量定义如下：

- `webSockets`
- `foreverFrame`
- `serverSentEvents`
- `longPolling`

## <a name="connections-and-hubs"></a>连接和集线器

SignalR API 包含两种用于在客户端和服务器之间进行通信的模型：持久性连接和中心。

连接表示用于发送单接收方、分组或广播消息的简单终结点。 持久性连接 API (在 .NET 代码中由 PersistentConnection 类表示) 使开发人员能够直接访问 SignalR 公开的低级别通信协议。 使用基于连接的 Api （如 Windows Communication Foundation）的开发人员将对使用连接通信模型非常熟悉。

中心是一种基于连接 API 构建的更高级别管道，它允许客户端和服务器直接调用方法。 SignalR 按魔术处理跨计算机边界的调度，使客户端能够像本地方法一样轻松地调用服务器上的方法，反之亦然。 如果开发人员已使用远程调用 Api （如 .NET 远程处理），则将对使用中心通信模型非常熟悉。 使用集线器还可以将强类型参数传递给方法，从而启用模型绑定。

### <a name="architecture-diagram"></a>体系结构关系图

下图显示了集线器、永久性连接和用于传输的底层技术之间的关系。

![显示 Api、传输和客户端的 SignalR 体系结构图](introduction-to-signalr/_static/image5.png)

### <a name="how-hubs-work"></a>集线器的工作方式

当服务器端代码在客户端上调用方法时，会在包含要调用的方法的名称和参数的活动传输中发送一个数据包 (当对象作为方法参数发送时，将使用 JSON) 对该对象进行序列化。 然后，客户端将方法名称与在客户端代码中定义的方法相匹配。 如果存在匹配项，则将使用反序列化的参数数据执行客户端方法。

可以使用 Fiddler 等工具监视此方法调用 [。](http://fiddler2.com/) 下图显示了在 Fiddler 的 "日志" 窗格中从 SignalR 服务器发送到 web 浏览器客户端的方法调用。 正在从名为的中心发送方法调用 `MoveShapeHub` ，并且调用被调用的方法 `updateShape` 。

![显示 SignalR 流量的 Fiddler 日志的视图](introduction-to-signalr/_static/image6.png)

在此示例中，通过参数标识中心名称 `H` ; 方法名用 `M` 参数标识，发送到方法的数据用 `A` 参数标识。 生成此消息的应用程序将在 [高频实时](tutorial-high-frequency-realtime-with-signalr.md) 教程中创建。

### <a name="choosing-a-communication-model"></a>选择通信模型

大多数应用程序应使用中心 API。 连接 API 可用于以下情况：

- 需要指定所发送的实际邮件的格式。
- 开发人员首选使用消息传递和调度模型，而不使用远程调用模型。
- 使用消息传送模型的现有应用程序正在移植，以使用 SignalR。

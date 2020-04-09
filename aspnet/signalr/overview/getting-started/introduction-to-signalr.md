---
uid: signalr/overview/getting-started/introduction-to-signalr
title: 信号R简介 |微软文档
author: bradygaster
description: 本文介绍了 SignalR 是什么，以及它旨在创建的一些解决方案。
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 0fab5e35-8c1f-43d4-8635-b8aba8766a71
msc.legacyurl: /signalr/overview/getting-started/introduction-to-signalr
msc.type: authoredcontent
ms.openlocfilehash: 8dbc31a5c8d59fa55dc5b513c1a51d24d18a685f
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675939"
---
# <a name="introduction-to-signalr"></a>SignalR 简介

由[帕特里克·弗莱彻](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 本文介绍了 SignalR 是什么，以及它旨在创建的一些解决方案。 
> 
> ## <a name="questions-and-comments"></a>问题和评论
> 
> 请留下反馈，关于你喜欢本教程的方式，以及我们可以在页面底部的评论中改进什么。 如果您有与本教程没有直接关系的问题，您可以将它们发布到[ASP.NET SignalR 论坛](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](https://stackoverflow.com/questions/tagged/signalr)。

## <a name="what-is-signalr"></a>什么是信号R？

ASP.NET SignalR 是一个面向ASP.NET开发人员的库，它简化了向应用程序添加实时 Web 功能的过程。 实时 Web 功能是让服务器代码在可用时立即将内容推送到连接的客户端，而不是让服务器等待客户端请求新数据的能力。

SignalR 可用于向ASP.NET应用程序添加任何类型的"实时"Web 功能。 虽然聊天通常用作示例，但您可以执行更多操作。 每当用户刷新网页以查看新数据，或者该页实现[长轮询](http://en.wikipedia.org/wiki/Push_technology#Long_polling)以检索新数据时，它都是使用 SignalR 的候选数据库。 示例包括仪表板和监视应用程序、协作应用程序（如同时编辑文档）、作业进度更新和实时表单。

SignalR 还支持需要服务器进行高频更新（例如实时游戏）的全新 Web 应用程序类型。

SignalR 提供了一个简单的 API，用于创建服务器到客户端的远程过程调用 （RPC），该调用从服务器端 .NET 代码调用客户端浏览器（和其他客户端平台）中的 JavaScript 函数。 SignalR 还包括用于连接管理的 API（例如，连接和断开连接事件）和分组连接。

![使用信号R调用方法](introduction-to-signalr/_static/image1.png)

SignalR 自动处理连接管理，让你可同时向所有连接的客户端广播消息，就像聊天室一样。 也可以向特定客户端发送消息。 客户端和服务器之间的连接是持久的，不同于传统的 HTTP 连接，后者针对每次通信重新建立。

SignalR 支持"服务器推送"功能，即服务器代码可以使用远程过程调用 （RPC） 向浏览器中的客户端代码调用，而不是站点上常见的请求-响应模型。

SignalR 应用程序可以使用内置和第三方横向扩展提供程序扩展到数千个客户端。

内置提供商包括：
* [服务总线](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.ServiceBus3)
* [SQL Server](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.SqlServer)
* [Redis](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.Redis)

第三方提供商包括：
* [NCache](https://www.alachisoft.com/ncache/asp-net-core-signalr.html).

信号R是开源的，可通过[GitHub](https://github.com/signalr)访问。

## <a name="signalr-and-websocket"></a>信号R和网络插座

SignalR 在可用时使用新的 WebSocket 传输，并在必要时回退到较旧的传输。 虽然您肯定可以使用 WebSocket 直接编写应用，但使用 SignalR 意味着您需要实现的大部分额外功能已经为您完成。 最重要的是，这意味着您可以编写应用代码以利用 WebSocket，而无需担心为较旧的客户端创建单独的代码路径。 SignalR 还保护您不必担心 WebSocket 的更新，因为 SignalR 已更新以支持基础传输中的更改，从而为您的应用程序提供跨 WebSocket 版本的一致的接口。

<a id="transports"></a>

## <a name="transports-and-fallbacks"></a>传输和回退

SignalR 是一种对在客户端和服务器之间执行实时工作所需的一些传输的抽象。 SignalR 连接以 HTTP 开头，然后将其提升为 WebSocket 连接（如果可用）。 WebSocket 是 SignalR 的理想传输方式，因为它最有效地使用服务器内存，具有最低的延迟，并具有最基本的功能（如客户端和服务器之间的全双工通信），但它也具有最严格的要求：WebSocket 要求服务器使用 Windows Server 2012 或 Windows 8 以及 .NET 框架 4.5。 如果不符合这些要求，SignalR 将尝试使用其他传输来建立连接。

### <a name="html-5-transports"></a>HTML 5 传输

这些传输依赖于对 HTML [5](http://en.wikipedia.org/wiki/HTML5)的支持。 如果客户端浏览器不支持 HTML 5 标准，将使用较旧的传输。

- **WebSocket（** 如果服务器和浏览器都表示它们可以支持 Websocket）。 WebSocket 是建立客户端和服务器之间真正持久双向连接的唯一传输。 但是，WebSocket 也有最严格的要求;它仅在最新版本的微软浏览器、谷歌 Chrome 和 Mozilla Firefox 中得到充分支持，并且仅在其他浏览器（如 Opera 和 Safari）中具有部分实现。
- **服务器发送事件**，也称为事件源（如果浏览器支持服务器发送事件，这基本上是除 Internet 资源管理器之外的所有浏览器。

### <a name="comet-transports"></a>彗星运输

以下传输基于[Comet](http://en.wikipedia.org/wiki/Comet_(programming)) Web 应用程序模型，其中浏览器或其他客户端维护长期持有的 HTTP 请求，服务器可以使用该请求将数据推送到客户端，而无需客户端专门请求该请求。

- **永久帧**（仅适用于 Internet 资源管理器）。 永久帧创建一个隐藏的 IFrame，该 IFrame 向服务器上未完成终结点的请求。 然后，服务器不断向客户端发送脚本，并立即执行该脚本，提供从服务器到客户端的单向实时连接。 从客户端到服务器的连接使用从服务器到客户端连接的单独连接，并且与标准 HTTP 请求一样，为需要发送的每个数据段创建新连接。
- **阿贾克斯长轮询**。 长轮询不会创建持久连接，而是轮询服务器的请求，该请求保持打开状态，直到服务器响应，此时连接将关闭，并立即请求新连接。 这可能会在连接重置时引入一些延迟。

有关支持哪些传输的配置的详细信息，请参阅[支持的平台](supported-platforms.md)。

### <a name="transport-selection-process"></a>传输选择过程

下面的列表显示了 SignalR 用来决定要使用的传输的步骤。

1. 如果浏览器是 Internet 资源管理器 8 或更早版本，则使用长轮询。
2. 如果配置了 JSONP（即参数`jsonp`设置为`true`启动连接时），则使用长轮询。
3. 如果进行跨域连接（即，如果 SignalR 终结点与托管页不在同一域中），则如果满足以下条件，将使用 WebSocket：

   - 客户端支持 CORS（跨源资源共享）。 有关哪些客户端支持 CORS 的详细信息，请参阅[caniuse.com 上的 CORS。](http://www.caniuse.com/CORS)
   - 客户端支持 WebSocket
   - 服务器支持 Web 插座

     如果未满足上述任何条件，将使用长轮询。 有关跨域连接的详细信息，请参阅[如何建立跨域连接](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)。
4. 如果未配置 JSONP 并且连接不是跨域，则如果客户端和服务器都支持它，将使用 WebSocket。
5. 如果客户端或服务器不支持 WebSocket，则使用服务器发送事件（如果可用）。
6. 如果服务器发送事件不可用，则尝试"永久帧"。
7. 如果"永久帧"失败，则使用长轮询。

<a id="MonitoringTransports"></a>
### <a name="monitoring-transports"></a>监控运输

通过在集线器上启用日志记录，并在浏览器中打开控制台窗口，可以确定应用程序正在使用什么传输。

要在浏览器中启用中心事件日志记录，请向客户端应用程序添加以下命令：

`$.connection.hub.logging = true;`

- 在 Internet 资源管理器中，通过按 F12 打开开发人员工具，然后单击"控制台"选项卡。

    ![微软互联网浏览器中的控制台](introduction-to-signalr/_static/image2.png)
- 在 Chrome 中，通过按 Ctrl_Shift_J 打开控制台。

    ![谷歌浏览器中的控制台](introduction-to-signalr/_static/image3.png)

启用控制台并启用日志记录后，您将能够看到 SignalR 正在使用哪种传输。

![显示 WebSocket 传输的 Internet 资源管理器中的控制台](introduction-to-signalr/_static/image4.png)

### <a name="specifying-a-transport"></a>指定传输

协商传输需要一定的时间和客户端/服务器资源。 如果客户端功能已知，则可以在启动客户端连接时指定传输。 以下代码段演示使用 Ajax Long 轮询传输启动连接，如果已知客户端不支持任何其他协议，则使用该传输：

`connection.start({ transport: 'longPolling' });`

如果希望客户端按顺序尝试特定传输，则可以指定回退顺序。 以下代码段演示了尝试 WebSocket，如果失败，请直接访问长轮询。

`connection.start({ transport: ['webSockets','longPolling'] });`

用于指定传输的字符串常量定义如下：

- `webSockets`
- `foreverFrame`
- `serverSentEvents`
- `longPolling`

## <a name="connections-and-hubs"></a>连接和集线器

SignalR API 包含两种用于客户端和服务器之间通信的模型：持久连接和集线器。

连接表示用于发送单收件人、分组消息或广播消息的简单终结点。 持久连接 API（由持久连接类在 .NET 代码中表示）使开发人员能够直接访问 SignalR 公开的低级通信协议。 使用连接通信模型对于使用基于连接的 API（如 Windows 通信基础）的开发人员来说，是熟悉的。

集线器是一个基于连接 API 构建的更高级管道，允许客户端和服务器直接调用彼此的方法。 SignalR 处理跨计算机边界的调度，就像通过魔术一样，允许客户端像本地方法一样轻松地调用服务器上的方法，反之亦然。 使用中心通信模型对于使用远程调用 API（如 .NET 远程处理）的开发人员来说，是熟悉的。 使用集线器还允许您将强类型参数传递给方法，从而启用模型绑定。

### <a name="architecture-diagram"></a>体系结构关系图

下图显示了集线器、持久连接和用于传输的基础技术之间的关系。

![显示 API、传输和客户端的信号R体系结构图](introduction-to-signalr/_static/image5.png)

### <a name="how-hubs-work"></a>中心的工作原理

当服务器端代码在客户端上调用方法时，数据包将跨活动传输发送，该传输包含要调用的方法的名称和参数（当对象作为方法参数发送时，使用 JSON 对其进行序列化）。 然后，客户端将方法名称与客户端代码中定义的方法匹配。 如果存在匹配项，将使用反序列化参数数据执行客户端方法。

可以使用[Fiddler](http://fiddler2.com/)等工具监视方法调用。 下图显示了 Fiddler 的 Logs 窗格中从 SignalR 服务器发送到 Web 浏览器客户端的方法调用。 方法调用是从称为`MoveShapeHub`的中心发送的，并且调用的方法称为`updateShape`。

![显示信号R流量的 Fiddler 日志视图](introduction-to-signalr/_static/image6.png)

在此示例中，中心名称与 参数一`H`起标识;因此，使用 参数标识中心名称。方法名称与`M`参数一起标识，发送到方法的数据用 参数`A`标识。 生成此消息的应用程序在[高频实时](tutorial-high-frequency-realtime-with-signalr.md)教程中创建。

### <a name="choosing-a-communication-model"></a>选择通信模型

大多数应用程序应使用集线器 API。 连接 API 可用于以下情况：

- 需要指定发送的实际消息的格式。
- 开发人员更喜欢使用消息传递和调度模型，而不是远程调用模型。
- 正在移植使用消息传递模型的现有应用程序以使用 SignalR。

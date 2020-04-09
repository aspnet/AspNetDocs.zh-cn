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
# <a name="introduction-to-signalr"></a><span data-ttu-id="58db4-103">SignalR 简介</span><span class="sxs-lookup"><span data-stu-id="58db4-103">Introduction to SignalR</span></span>

<span data-ttu-id="58db4-104">由[帕特里克·弗莱彻](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="58db4-104">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="58db4-105">本文介绍了 SignalR 是什么，以及它旨在创建的一些解决方案。</span><span class="sxs-lookup"><span data-stu-id="58db4-105">This article describes what SignalR is, and some of the solutions it was designed to create.</span></span> 
> 
> ## <a name="questions-and-comments"></a><span data-ttu-id="58db4-106">问题和评论</span><span class="sxs-lookup"><span data-stu-id="58db4-106">Questions and comments</span></span>
> 
> <span data-ttu-id="58db4-107">请留下反馈，关于你喜欢本教程的方式，以及我们可以在页面底部的评论中改进什么。</span><span class="sxs-lookup"><span data-stu-id="58db4-107">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="58db4-108">如果您有与本教程没有直接关系的问题，您可以将它们发布到[ASP.NET SignalR 论坛](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](https://stackoverflow.com/questions/tagged/signalr)。</span><span class="sxs-lookup"><span data-stu-id="58db4-108">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](https://stackoverflow.com/questions/tagged/signalr).</span></span>

## <a name="what-is-signalr"></a><span data-ttu-id="58db4-109">什么是信号R？</span><span class="sxs-lookup"><span data-stu-id="58db4-109">What is SignalR?</span></span>

<span data-ttu-id="58db4-110">ASP.NET SignalR 是一个面向ASP.NET开发人员的库，它简化了向应用程序添加实时 Web 功能的过程。</span><span class="sxs-lookup"><span data-stu-id="58db4-110">ASP.NET SignalR is a library for ASP.NET developers that simplifies the process of adding real-time web functionality to applications.</span></span> <span data-ttu-id="58db4-111">实时 Web 功能是让服务器代码在可用时立即将内容推送到连接的客户端，而不是让服务器等待客户端请求新数据的能力。</span><span class="sxs-lookup"><span data-stu-id="58db4-111">Real-time web functionality is the ability to have server code push content to connected clients instantly as it becomes available, rather than having the server wait for a client to request new data.</span></span>

<span data-ttu-id="58db4-112">SignalR 可用于向ASP.NET应用程序添加任何类型的"实时"Web 功能。</span><span class="sxs-lookup"><span data-stu-id="58db4-112">SignalR can be used to add any sort of "real-time" web functionality to your ASP.NET application.</span></span> <span data-ttu-id="58db4-113">虽然聊天通常用作示例，但您可以执行更多操作。</span><span class="sxs-lookup"><span data-stu-id="58db4-113">While chat is often used as an example, you can do a whole lot more.</span></span> <span data-ttu-id="58db4-114">每当用户刷新网页以查看新数据，或者该页实现[长轮询](http://en.wikipedia.org/wiki/Push_technology#Long_polling)以检索新数据时，它都是使用 SignalR 的候选数据库。</span><span class="sxs-lookup"><span data-stu-id="58db4-114">Any time a user refreshes a web page to see new data, or the page implements [long polling](http://en.wikipedia.org/wiki/Push_technology#Long_polling) to retrieve new data, it is a candidate for using SignalR.</span></span> <span data-ttu-id="58db4-115">示例包括仪表板和监视应用程序、协作应用程序（如同时编辑文档）、作业进度更新和实时表单。</span><span class="sxs-lookup"><span data-stu-id="58db4-115">Examples include dashboards and monitoring applications, collaborative applications (such as simultaneous editing of documents), job progress updates, and real-time forms.</span></span>

<span data-ttu-id="58db4-116">SignalR 还支持需要服务器进行高频更新（例如实时游戏）的全新 Web 应用程序类型。</span><span class="sxs-lookup"><span data-stu-id="58db4-116">SignalR also enables completely new types of web applications that require high frequency updates from the server, for example, real-time gaming.</span></span>

<span data-ttu-id="58db4-117">SignalR 提供了一个简单的 API，用于创建服务器到客户端的远程过程调用 （RPC），该调用从服务器端 .NET 代码调用客户端浏览器（和其他客户端平台）中的 JavaScript 函数。</span><span class="sxs-lookup"><span data-stu-id="58db4-117">SignalR provides a simple API for creating server-to-client remote procedure calls (RPC) that call JavaScript functions in client browsers (and other client platforms) from server-side .NET code.</span></span> <span data-ttu-id="58db4-118">SignalR 还包括用于连接管理的 API（例如，连接和断开连接事件）和分组连接。</span><span class="sxs-lookup"><span data-stu-id="58db4-118">SignalR also includes API for connection management (for instance, connect and disconnect events), and grouping connections.</span></span>

![使用信号R调用方法](introduction-to-signalr/_static/image1.png)

<span data-ttu-id="58db4-120">SignalR 自动处理连接管理，让你可同时向所有连接的客户端广播消息，就像聊天室一样。</span><span class="sxs-lookup"><span data-stu-id="58db4-120">SignalR handles connection management automatically, and lets you broadcast messages to all connected clients simultaneously, like a chat room.</span></span> <span data-ttu-id="58db4-121">也可以向特定客户端发送消息。</span><span class="sxs-lookup"><span data-stu-id="58db4-121">You can also send messages to specific clients.</span></span> <span data-ttu-id="58db4-122">客户端和服务器之间的连接是持久的，不同于传统的 HTTP 连接，后者针对每次通信重新建立。</span><span class="sxs-lookup"><span data-stu-id="58db4-122">The connection between the client and server is persistent, unlike a classic HTTP connection, which is re-established for each communication.</span></span>

<span data-ttu-id="58db4-123">SignalR 支持"服务器推送"功能，即服务器代码可以使用远程过程调用 （RPC） 向浏览器中的客户端代码调用，而不是站点上常见的请求-响应模型。</span><span class="sxs-lookup"><span data-stu-id="58db4-123">SignalR supports "server push" functionality, in which server code can call out to client code in the browser using Remote Procedure Calls (RPC), rather than the request-response model common on the web today.</span></span>

<span data-ttu-id="58db4-124">SignalR 应用程序可以使用内置和第三方横向扩展提供程序扩展到数千个客户端。</span><span class="sxs-lookup"><span data-stu-id="58db4-124">SignalR applications can scale out to thousands of clients using built-in, and third-party scale-out providers.</span></span>

<span data-ttu-id="58db4-125">内置提供商包括：</span><span class="sxs-lookup"><span data-stu-id="58db4-125">Built-in providers include:</span></span>
* [<span data-ttu-id="58db4-126">服务总线</span><span class="sxs-lookup"><span data-stu-id="58db4-126">Service Bus</span></span>](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.ServiceBus3)
* [<span data-ttu-id="58db4-127">SQL Server</span><span class="sxs-lookup"><span data-stu-id="58db4-127">SQL Server</span></span>](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.SqlServer)
* [<span data-ttu-id="58db4-128">Redis</span><span class="sxs-lookup"><span data-stu-id="58db4-128">Redis</span></span>](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.Redis)

<span data-ttu-id="58db4-129">第三方提供商包括：</span><span class="sxs-lookup"><span data-stu-id="58db4-129">Third-party providers include:</span></span>
* <span data-ttu-id="58db4-130">[NCache](https://www.alachisoft.com/ncache/asp-net-core-signalr.html).</span><span class="sxs-lookup"><span data-stu-id="58db4-130">[NCache](https://www.alachisoft.com/ncache/asp-net-core-signalr.html).</span></span>

<span data-ttu-id="58db4-131">信号R是开源的，可通过[GitHub](https://github.com/signalr)访问。</span><span class="sxs-lookup"><span data-stu-id="58db4-131">SignalR is open-source, accessible through [GitHub](https://github.com/signalr).</span></span>

## <a name="signalr-and-websocket"></a><span data-ttu-id="58db4-132">信号R和网络插座</span><span class="sxs-lookup"><span data-stu-id="58db4-132">SignalR and WebSocket</span></span>

<span data-ttu-id="58db4-133">SignalR 在可用时使用新的 WebSocket 传输，并在必要时回退到较旧的传输。</span><span class="sxs-lookup"><span data-stu-id="58db4-133">SignalR uses the new WebSocket transport where available and falls back to older transports where necessary.</span></span> <span data-ttu-id="58db4-134">虽然您肯定可以使用 WebSocket 直接编写应用，但使用 SignalR 意味着您需要实现的大部分额外功能已经为您完成。</span><span class="sxs-lookup"><span data-stu-id="58db4-134">While you could certainly write your app using WebSocket directly, using SignalR means that a lot of the extra functionality you would need to implement is already done for you.</span></span> <span data-ttu-id="58db4-135">最重要的是，这意味着您可以编写应用代码以利用 WebSocket，而无需担心为较旧的客户端创建单独的代码路径。</span><span class="sxs-lookup"><span data-stu-id="58db4-135">Most importantly, this means that you can code your app to take advantage of WebSocket without having to worry about creating a separate code path for older clients.</span></span> <span data-ttu-id="58db4-136">SignalR 还保护您不必担心 WebSocket 的更新，因为 SignalR 已更新以支持基础传输中的更改，从而为您的应用程序提供跨 WebSocket 版本的一致的接口。</span><span class="sxs-lookup"><span data-stu-id="58db4-136">SignalR also shields you from having to worry about updates to WebSocket, since SignalR is updated to support changes in the underlying transport, providing your application a consistent interface across versions of WebSocket.</span></span>

<a id="transports"></a>

## <a name="transports-and-fallbacks"></a><span data-ttu-id="58db4-137">传输和回退</span><span class="sxs-lookup"><span data-stu-id="58db4-137">Transports and fallbacks</span></span>

<span data-ttu-id="58db4-138">SignalR 是一种对在客户端和服务器之间执行实时工作所需的一些传输的抽象。</span><span class="sxs-lookup"><span data-stu-id="58db4-138">SignalR is an abstraction over some of the transports that are required to do real-time work between client and server.</span></span> <span data-ttu-id="58db4-139">SignalR 连接以 HTTP 开头，然后将其提升为 WebSocket 连接（如果可用）。</span><span class="sxs-lookup"><span data-stu-id="58db4-139">A SignalR connection starts as HTTP, and is then promoted to a WebSocket connection if it is available.</span></span> <span data-ttu-id="58db4-140">WebSocket 是 SignalR 的理想传输方式，因为它最有效地使用服务器内存，具有最低的延迟，并具有最基本的功能（如客户端和服务器之间的全双工通信），但它也具有最严格的要求：WebSocket 要求服务器使用 Windows Server 2012 或 Windows 8 以及 .NET 框架 4.5。</span><span class="sxs-lookup"><span data-stu-id="58db4-140">WebSocket is the ideal transport for SignalR, since it makes the most efficient use of server memory, has the lowest latency, and has the most underlying features (such as full duplex communication between client and server), but it also has the most stringent requirements: WebSocket requires the server to be using Windows Server 2012 or Windows 8, and .NET Framework 4.5.</span></span> <span data-ttu-id="58db4-141">如果不符合这些要求，SignalR 将尝试使用其他传输来建立连接。</span><span class="sxs-lookup"><span data-stu-id="58db4-141">If these requirements are not met, SignalR will attempt to use other transports to make its connections.</span></span>

### <a name="html-5-transports"></a><span data-ttu-id="58db4-142">HTML 5 传输</span><span class="sxs-lookup"><span data-stu-id="58db4-142">HTML 5 transports</span></span>

<span data-ttu-id="58db4-143">这些传输依赖于对 HTML [5](http://en.wikipedia.org/wiki/HTML5)的支持。</span><span class="sxs-lookup"><span data-stu-id="58db4-143">These transports depend on support for [HTML 5](http://en.wikipedia.org/wiki/HTML5).</span></span> <span data-ttu-id="58db4-144">如果客户端浏览器不支持 HTML 5 标准，将使用较旧的传输。</span><span class="sxs-lookup"><span data-stu-id="58db4-144">If the client browser does not support the HTML 5 standard, older transports will be used.</span></span>

- <span data-ttu-id="58db4-145">**WebSocket（** 如果服务器和浏览器都表示它们可以支持 Websocket）。</span><span class="sxs-lookup"><span data-stu-id="58db4-145">**WebSocket** (if both the server and browser indicate they can support Websocket).</span></span> <span data-ttu-id="58db4-146">WebSocket 是建立客户端和服务器之间真正持久双向连接的唯一传输。</span><span class="sxs-lookup"><span data-stu-id="58db4-146">WebSocket is the only transport that establishes a true persistent, two-way connection between client and server.</span></span> <span data-ttu-id="58db4-147">但是，WebSocket 也有最严格的要求;它仅在最新版本的微软浏览器、谷歌 Chrome 和 Mozilla Firefox 中得到充分支持，并且仅在其他浏览器（如 Opera 和 Safari）中具有部分实现。</span><span class="sxs-lookup"><span data-stu-id="58db4-147">However, WebSocket also has the most stringent requirements; it is fully supported only in the latest versions of Microsoft Internet Explorer, Google Chrome, and Mozilla Firefox, and only has a partial implementation in other browsers such as Opera and Safari.</span></span>
- <span data-ttu-id="58db4-148">**服务器发送事件**，也称为事件源（如果浏览器支持服务器发送事件，这基本上是除 Internet 资源管理器之外的所有浏览器。</span><span class="sxs-lookup"><span data-stu-id="58db4-148">**Server Sent Events**, also known as EventSource (if the browser supports Server Sent Events, which is basically all browsers except Internet Explorer.)</span></span>

### <a name="comet-transports"></a><span data-ttu-id="58db4-149">彗星运输</span><span class="sxs-lookup"><span data-stu-id="58db4-149">Comet transports</span></span>

<span data-ttu-id="58db4-150">以下传输基于[Comet](http://en.wikipedia.org/wiki/Comet_(programming)) Web 应用程序模型，其中浏览器或其他客户端维护长期持有的 HTTP 请求，服务器可以使用该请求将数据推送到客户端，而无需客户端专门请求该请求。</span><span class="sxs-lookup"><span data-stu-id="58db4-150">The following transports are based on the [Comet](http://en.wikipedia.org/wiki/Comet_(programming)) web application model, in which a browser or other client maintains a long-held HTTP request, which the server can use to push data to the client without the client specifically requesting it.</span></span>

- <span data-ttu-id="58db4-151">**永久帧**（仅适用于 Internet 资源管理器）。</span><span class="sxs-lookup"><span data-stu-id="58db4-151">**Forever Frame** (for Internet Explorer only).</span></span> <span data-ttu-id="58db4-152">永久帧创建一个隐藏的 IFrame，该 IFrame 向服务器上未完成终结点的请求。</span><span class="sxs-lookup"><span data-stu-id="58db4-152">Forever Frame creates a hidden IFrame which makes a request to an endpoint on the server that does not complete.</span></span> <span data-ttu-id="58db4-153">然后，服务器不断向客户端发送脚本，并立即执行该脚本，提供从服务器到客户端的单向实时连接。</span><span class="sxs-lookup"><span data-stu-id="58db4-153">The server then continually sends script to the client which is immediately executed, providing a one-way realtime connection from server to client.</span></span> <span data-ttu-id="58db4-154">从客户端到服务器的连接使用从服务器到客户端连接的单独连接，并且与标准 HTTP 请求一样，为需要发送的每个数据段创建新连接。</span><span class="sxs-lookup"><span data-stu-id="58db4-154">The connection from client to server uses a separate connection from the server to client connection, and like a standard HTTP request, a new connection is created for each piece of data that needs to be sent.</span></span>
- <span data-ttu-id="58db4-155">**阿贾克斯长轮询**。</span><span class="sxs-lookup"><span data-stu-id="58db4-155">**Ajax long polling**.</span></span> <span data-ttu-id="58db4-156">长轮询不会创建持久连接，而是轮询服务器的请求，该请求保持打开状态，直到服务器响应，此时连接将关闭，并立即请求新连接。</span><span class="sxs-lookup"><span data-stu-id="58db4-156">Long polling does not create a persistent connection, but instead polls the server with a request that stays open until the server responds, at which point the connection closes, and a new connection is requested immediately.</span></span> <span data-ttu-id="58db4-157">这可能会在连接重置时引入一些延迟。</span><span class="sxs-lookup"><span data-stu-id="58db4-157">This may introduce some latency while the connection resets.</span></span>

<span data-ttu-id="58db4-158">有关支持哪些传输的配置的详细信息，请参阅[支持的平台](supported-platforms.md)。</span><span class="sxs-lookup"><span data-stu-id="58db4-158">For more information on what transports are supported under which configurations, see [Supported Platforms](supported-platforms.md).</span></span>

### <a name="transport-selection-process"></a><span data-ttu-id="58db4-159">传输选择过程</span><span class="sxs-lookup"><span data-stu-id="58db4-159">Transport selection process</span></span>

<span data-ttu-id="58db4-160">下面的列表显示了 SignalR 用来决定要使用的传输的步骤。</span><span class="sxs-lookup"><span data-stu-id="58db4-160">The following list shows the steps that SignalR uses to decide which transport to use.</span></span>

1. <span data-ttu-id="58db4-161">如果浏览器是 Internet 资源管理器 8 或更早版本，则使用长轮询。</span><span class="sxs-lookup"><span data-stu-id="58db4-161">If the browser is Internet Explorer 8 or earlier, Long Polling is used.</span></span>
2. <span data-ttu-id="58db4-162">如果配置了 JSONP（即参数`jsonp`设置为`true`启动连接时），则使用长轮询。</span><span class="sxs-lookup"><span data-stu-id="58db4-162">If JSONP is configured (that is, the `jsonp` parameter is set to `true` when the connection is started), Long Polling is used.</span></span>
3. <span data-ttu-id="58db4-163">如果进行跨域连接（即，如果 SignalR 终结点与托管页不在同一域中），则如果满足以下条件，将使用 WebSocket：</span><span class="sxs-lookup"><span data-stu-id="58db4-163">If a cross-domain connection is being made (that is, if the SignalR endpoint is not in the same domain as the hosting page), then WebSocket will be used if the following criteria are met:</span></span>

   - <span data-ttu-id="58db4-164">客户端支持 CORS（跨源资源共享）。</span><span class="sxs-lookup"><span data-stu-id="58db4-164">The client supports CORS (Cross-Origin Resource Sharing).</span></span> <span data-ttu-id="58db4-165">有关哪些客户端支持 CORS 的详细信息，请参阅[caniuse.com 上的 CORS。](http://www.caniuse.com/CORS)</span><span class="sxs-lookup"><span data-stu-id="58db4-165">For details on which clients support CORS, see [CORS at caniuse.com](http://www.caniuse.com/CORS).</span></span>
   - <span data-ttu-id="58db4-166">客户端支持 WebSocket</span><span class="sxs-lookup"><span data-stu-id="58db4-166">The client supports WebSocket</span></span>
   - <span data-ttu-id="58db4-167">服务器支持 Web 插座</span><span class="sxs-lookup"><span data-stu-id="58db4-167">The server supports WebSocket</span></span>

     <span data-ttu-id="58db4-168">如果未满足上述任何条件，将使用长轮询。</span><span class="sxs-lookup"><span data-stu-id="58db4-168">If any of these criteria are not met, Long Polling will be used.</span></span> <span data-ttu-id="58db4-169">有关跨域连接的详细信息，请参阅[如何建立跨域连接](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)。</span><span class="sxs-lookup"><span data-stu-id="58db4-169">For more information on cross-domain connections, see [How to establish a cross-domain connection](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).</span></span>
4. <span data-ttu-id="58db4-170">如果未配置 JSONP 并且连接不是跨域，则如果客户端和服务器都支持它，将使用 WebSocket。</span><span class="sxs-lookup"><span data-stu-id="58db4-170">If JSONP is not configured and the connection is not cross-domain, WebSocket will be used if both the client and server support it.</span></span>
5. <span data-ttu-id="58db4-171">如果客户端或服务器不支持 WebSocket，则使用服务器发送事件（如果可用）。</span><span class="sxs-lookup"><span data-stu-id="58db4-171">If either the client or server do not support WebSocket, Server Sent Events is used if it is available.</span></span>
6. <span data-ttu-id="58db4-172">如果服务器发送事件不可用，则尝试"永久帧"。</span><span class="sxs-lookup"><span data-stu-id="58db4-172">If Server Sent Events is not available, Forever Frame is attempted.</span></span>
7. <span data-ttu-id="58db4-173">如果"永久帧"失败，则使用长轮询。</span><span class="sxs-lookup"><span data-stu-id="58db4-173">If Forever Frame fails, Long Polling is used.</span></span>

<a id="MonitoringTransports"></a>
### <a name="monitoring-transports"></a><span data-ttu-id="58db4-174">监控运输</span><span class="sxs-lookup"><span data-stu-id="58db4-174">Monitoring transports</span></span>

<span data-ttu-id="58db4-175">通过在集线器上启用日志记录，并在浏览器中打开控制台窗口，可以确定应用程序正在使用什么传输。</span><span class="sxs-lookup"><span data-stu-id="58db4-175">You can determine what transport your application is using by enabling logging on your hub, and opening the console window in your browser.</span></span>

<span data-ttu-id="58db4-176">要在浏览器中启用中心事件日志记录，请向客户端应用程序添加以下命令：</span><span class="sxs-lookup"><span data-stu-id="58db4-176">To enable logging for your hub's events in a browser, add the following command to your client application:</span></span>

`$.connection.hub.logging = true;`

- <span data-ttu-id="58db4-177">在 Internet 资源管理器中，通过按 F12 打开开发人员工具，然后单击"控制台"选项卡。</span><span class="sxs-lookup"><span data-stu-id="58db4-177">In Internet Explorer, open the developer tools by pressing F12, and click the Console tab.</span></span>

    ![微软互联网浏览器中的控制台](introduction-to-signalr/_static/image2.png)
- <span data-ttu-id="58db4-179">在 Chrome 中，通过按 Ctrl_Shift_J 打开控制台。</span><span class="sxs-lookup"><span data-stu-id="58db4-179">In Chrome, open the console by pressing Ctrl+Shift+J.</span></span>

    ![谷歌浏览器中的控制台](introduction-to-signalr/_static/image3.png)

<span data-ttu-id="58db4-181">启用控制台并启用日志记录后，您将能够看到 SignalR 正在使用哪种传输。</span><span class="sxs-lookup"><span data-stu-id="58db4-181">With the console open and logging enabled, you'll be able to see which transport is being used by SignalR.</span></span>

![显示 WebSocket 传输的 Internet 资源管理器中的控制台](introduction-to-signalr/_static/image4.png)

### <a name="specifying-a-transport"></a><span data-ttu-id="58db4-183">指定传输</span><span class="sxs-lookup"><span data-stu-id="58db4-183">Specifying a transport</span></span>

<span data-ttu-id="58db4-184">协商传输需要一定的时间和客户端/服务器资源。</span><span class="sxs-lookup"><span data-stu-id="58db4-184">Negotiating a transport takes a certain amount of time and client/server resources.</span></span> <span data-ttu-id="58db4-185">如果客户端功能已知，则可以在启动客户端连接时指定传输。</span><span class="sxs-lookup"><span data-stu-id="58db4-185">If the client capabilities are known, then a transport can be specified when the client connection is started.</span></span> <span data-ttu-id="58db4-186">以下代码段演示使用 Ajax Long 轮询传输启动连接，如果已知客户端不支持任何其他协议，则使用该传输：</span><span class="sxs-lookup"><span data-stu-id="58db4-186">The following code snippet demonstrates starting a connection using the Ajax Long Polling transport, as would be used if it was known that the client did not support any other protocol:</span></span>

`connection.start({ transport: 'longPolling' });`

<span data-ttu-id="58db4-187">如果希望客户端按顺序尝试特定传输，则可以指定回退顺序。</span><span class="sxs-lookup"><span data-stu-id="58db4-187">You can specify a fallback order if you want a client to try specific transports in order.</span></span> <span data-ttu-id="58db4-188">以下代码段演示了尝试 WebSocket，如果失败，请直接访问长轮询。</span><span class="sxs-lookup"><span data-stu-id="58db4-188">The following code snippet demonstrates trying WebSocket, and failing that, going directly to Long Polling.</span></span>

`connection.start({ transport: ['webSockets','longPolling'] });`

<span data-ttu-id="58db4-189">用于指定传输的字符串常量定义如下：</span><span class="sxs-lookup"><span data-stu-id="58db4-189">The string constants for specifying transports are defined as follows:</span></span>

- `webSockets`
- `foreverFrame`
- `serverSentEvents`
- `longPolling`

## <a name="connections-and-hubs"></a><span data-ttu-id="58db4-190">连接和集线器</span><span class="sxs-lookup"><span data-stu-id="58db4-190">Connections and Hubs</span></span>

<span data-ttu-id="58db4-191">SignalR API 包含两种用于客户端和服务器之间通信的模型：持久连接和集线器。</span><span class="sxs-lookup"><span data-stu-id="58db4-191">The SignalR API contains two models for communicating between clients and servers: Persistent Connections and Hubs.</span></span>

<span data-ttu-id="58db4-192">连接表示用于发送单收件人、分组消息或广播消息的简单终结点。</span><span class="sxs-lookup"><span data-stu-id="58db4-192">A Connection represents a simple endpoint for sending single-recipient, grouped, or broadcast messages.</span></span> <span data-ttu-id="58db4-193">持久连接 API（由持久连接类在 .NET 代码中表示）使开发人员能够直接访问 SignalR 公开的低级通信协议。</span><span class="sxs-lookup"><span data-stu-id="58db4-193">The Persistent Connection API (represented in .NET code by the PersistentConnection class) gives the developer direct access to the low-level communication protocol that SignalR exposes.</span></span> <span data-ttu-id="58db4-194">使用连接通信模型对于使用基于连接的 API（如 Windows 通信基础）的开发人员来说，是熟悉的。</span><span class="sxs-lookup"><span data-stu-id="58db4-194">Using the Connections communication model will be familiar to developers who have used connection-based APIs such as Windows Communication Foundation.</span></span>

<span data-ttu-id="58db4-195">集线器是一个基于连接 API 构建的更高级管道，允许客户端和服务器直接调用彼此的方法。</span><span class="sxs-lookup"><span data-stu-id="58db4-195">A Hub is a more high-level pipeline built upon the Connection API that allows your client and server to call methods on each other directly.</span></span> <span data-ttu-id="58db4-196">SignalR 处理跨计算机边界的调度，就像通过魔术一样，允许客户端像本地方法一样轻松地调用服务器上的方法，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="58db4-196">SignalR handles the dispatching across machine boundaries as if by magic, allowing clients to call methods on the server as easily as local methods, and vice versa.</span></span> <span data-ttu-id="58db4-197">使用中心通信模型对于使用远程调用 API（如 .NET 远程处理）的开发人员来说，是熟悉的。</span><span class="sxs-lookup"><span data-stu-id="58db4-197">Using the Hubs communication model will be familiar to developers who have used remote invocation APIs such as .NET Remoting.</span></span> <span data-ttu-id="58db4-198">使用集线器还允许您将强类型参数传递给方法，从而启用模型绑定。</span><span class="sxs-lookup"><span data-stu-id="58db4-198">Using a Hub also allows you to pass strongly typed parameters to methods, enabling model binding.</span></span>

### <a name="architecture-diagram"></a><span data-ttu-id="58db4-199">体系结构关系图</span><span class="sxs-lookup"><span data-stu-id="58db4-199">Architecture diagram</span></span>

<span data-ttu-id="58db4-200">下图显示了集线器、持久连接和用于传输的基础技术之间的关系。</span><span class="sxs-lookup"><span data-stu-id="58db4-200">The following diagram shows the relationship between Hubs, Persistent Connections, and the underlying technologies used for transports.</span></span>

![显示 API、传输和客户端的信号R体系结构图](introduction-to-signalr/_static/image5.png)

### <a name="how-hubs-work"></a><span data-ttu-id="58db4-202">中心的工作原理</span><span class="sxs-lookup"><span data-stu-id="58db4-202">How Hubs work</span></span>

<span data-ttu-id="58db4-203">当服务器端代码在客户端上调用方法时，数据包将跨活动传输发送，该传输包含要调用的方法的名称和参数（当对象作为方法参数发送时，使用 JSON 对其进行序列化）。</span><span class="sxs-lookup"><span data-stu-id="58db4-203">When server-side code calls a method on the client, a packet is sent across the active transport that contains the name and parameters of the method to be called (when an object is sent as a method parameter, it is serialized using JSON).</span></span> <span data-ttu-id="58db4-204">然后，客户端将方法名称与客户端代码中定义的方法匹配。</span><span class="sxs-lookup"><span data-stu-id="58db4-204">The client then matches the method name to methods defined in client-side code.</span></span> <span data-ttu-id="58db4-205">如果存在匹配项，将使用反序列化参数数据执行客户端方法。</span><span class="sxs-lookup"><span data-stu-id="58db4-205">If there is a match, the client method will be executed using the deserialized parameter data.</span></span>

<span data-ttu-id="58db4-206">可以使用[Fiddler](http://fiddler2.com/)等工具监视方法调用。</span><span class="sxs-lookup"><span data-stu-id="58db4-206">The method call can be monitored using tools like [Fiddler.](http://fiddler2.com/)</span></span> <span data-ttu-id="58db4-207">下图显示了 Fiddler 的 Logs 窗格中从 SignalR 服务器发送到 Web 浏览器客户端的方法调用。</span><span class="sxs-lookup"><span data-stu-id="58db4-207">The following image shows a method call sent from a SignalR server to a web browser client in the Logs pane of Fiddler.</span></span> <span data-ttu-id="58db4-208">方法调用是从称为`MoveShapeHub`的中心发送的，并且调用的方法称为`updateShape`。</span><span class="sxs-lookup"><span data-stu-id="58db4-208">The method call is being sent from a hub called `MoveShapeHub`, and the method being invoked is called `updateShape`.</span></span>

![显示信号R流量的 Fiddler 日志视图](introduction-to-signalr/_static/image6.png)

<span data-ttu-id="58db4-210">在此示例中，中心名称与 参数一`H`起标识;因此，使用 参数标识中心名称。方法名称与`M`参数一起标识，发送到方法的数据用 参数`A`标识。</span><span class="sxs-lookup"><span data-stu-id="58db4-210">In this example, the hub name is identified with the `H` parameter; the method name is identified with the `M` parameter, and the data being sent to the method is identified with the `A` parameter.</span></span> <span data-ttu-id="58db4-211">生成此消息的应用程序在[高频实时](tutorial-high-frequency-realtime-with-signalr.md)教程中创建。</span><span class="sxs-lookup"><span data-stu-id="58db4-211">The application that generated this message is created in the [High-Frequency Realtime](tutorial-high-frequency-realtime-with-signalr.md) tutorial.</span></span>

### <a name="choosing-a-communication-model"></a><span data-ttu-id="58db4-212">选择通信模型</span><span class="sxs-lookup"><span data-stu-id="58db4-212">Choosing a communication model</span></span>

<span data-ttu-id="58db4-213">大多数应用程序应使用集线器 API。</span><span class="sxs-lookup"><span data-stu-id="58db4-213">Most applications should use the Hubs API.</span></span> <span data-ttu-id="58db4-214">连接 API 可用于以下情况：</span><span class="sxs-lookup"><span data-stu-id="58db4-214">The Connections API could be used in the following circumstances:</span></span>

- <span data-ttu-id="58db4-215">需要指定发送的实际消息的格式。</span><span class="sxs-lookup"><span data-stu-id="58db4-215">The format of the actual message sent needs to be specified.</span></span>
- <span data-ttu-id="58db4-216">开发人员更喜欢使用消息传递和调度模型，而不是远程调用模型。</span><span class="sxs-lookup"><span data-stu-id="58db4-216">The developer prefers to work with a messaging and dispatching model rather than a remote invocation model.</span></span>
- <span data-ttu-id="58db4-217">正在移植使用消息传递模型的现有应用程序以使用 SignalR。</span><span class="sxs-lookup"><span data-stu-id="58db4-217">An existing application that uses a messaging model is being ported to use SignalR.</span></span>

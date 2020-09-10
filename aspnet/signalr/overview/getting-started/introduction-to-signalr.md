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
# <a name="introduction-to-signalr"></a><span data-ttu-id="5bc42-103">SignalR 简介</span><span class="sxs-lookup"><span data-stu-id="5bc42-103">Introduction to SignalR</span></span>

<span data-ttu-id="5bc42-104">作者： [Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="5bc42-104">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="5bc42-105">本文介绍了什么是 SignalR 以及它旨在创建的一些解决方案。</span><span class="sxs-lookup"><span data-stu-id="5bc42-105">This article describes what SignalR is, and some of the solutions it was designed to create.</span></span> 
> 
> ## <a name="questions-and-comments"></a><span data-ttu-id="5bc42-106">问题和注释</span><span class="sxs-lookup"><span data-stu-id="5bc42-106">Questions and comments</span></span>
> 
> <span data-ttu-id="5bc42-107">请提供有关你喜欢本教程的方式的反馈，并在页面底部的评论中留下反馈。</span><span class="sxs-lookup"><span data-stu-id="5bc42-107">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="5bc42-108">如果你有与本教程不直接相关的问题，则可以将其发布到 [ASP.NET SignalR 论坛](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 或 [StackOverflow.com](https://stackoverflow.com/questions/tagged/signalr)。</span><span class="sxs-lookup"><span data-stu-id="5bc42-108">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](https://stackoverflow.com/questions/tagged/signalr).</span></span>

## <a name="what-is-signalr"></a><span data-ttu-id="5bc42-109">什么是 SignalR？</span><span class="sxs-lookup"><span data-stu-id="5bc42-109">What is SignalR?</span></span>

<span data-ttu-id="5bc42-110">ASP.NET SignalR 是 ASP.NET 开发人员的库，可简化将实时 web 功能添加到应用程序的过程。</span><span class="sxs-lookup"><span data-stu-id="5bc42-110">ASP.NET SignalR is a library for ASP.NET developers that simplifies the process of adding real-time web functionality to applications.</span></span> <span data-ttu-id="5bc42-111">实时 web 功能使服务器代码能够在可用时立即将内容推送到连接的客户端，而不是让服务器等待客户端请求新的数据。</span><span class="sxs-lookup"><span data-stu-id="5bc42-111">Real-time web functionality is the ability to have server code push content to connected clients instantly as it becomes available, rather than having the server wait for a client to request new data.</span></span>

<span data-ttu-id="5bc42-112">SignalR 可用于将任何种类的 "实时" web 功能添加到 ASP.NET 应用程序。</span><span class="sxs-lookup"><span data-stu-id="5bc42-112">SignalR can be used to add any sort of "real-time" web functionality to your ASP.NET application.</span></span> <span data-ttu-id="5bc42-113">尽管聊天通常用作示例，但你可以执行更多操作。</span><span class="sxs-lookup"><span data-stu-id="5bc42-113">While chat is often used as an example, you can do a whole lot more.</span></span> <span data-ttu-id="5bc42-114">用户每次刷新网页以查看新数据，或者页面实现 [长轮询](http://en.wikipedia.org/wiki/Push_technology#Long_polling) 来检索新数据时，都是使用 SignalR 的候选项。</span><span class="sxs-lookup"><span data-stu-id="5bc42-114">Any time a user refreshes a web page to see new data, or the page implements [long polling](http://en.wikipedia.org/wiki/Push_technology#Long_polling) to retrieve new data, it is a candidate for using SignalR.</span></span> <span data-ttu-id="5bc42-115">示例包括仪表板和监视应用程序、协作应用程序 (例如同步编辑文档) 、作业进度更新和实时窗体。</span><span class="sxs-lookup"><span data-stu-id="5bc42-115">Examples include dashboards and monitoring applications, collaborative applications (such as simultaneous editing of documents), job progress updates, and real-time forms.</span></span>

<span data-ttu-id="5bc42-116">SignalR 还启用了全新类型的 web 应用程序，这些应用程序需要服务器中的高频率更新，例如，实时游戏。</span><span class="sxs-lookup"><span data-stu-id="5bc42-116">SignalR also enables completely new types of web applications that require high frequency updates from the server, for example, real-time gaming.</span></span>

<span data-ttu-id="5bc42-117">SignalR 提供了一个简单的 API，用于创建 (RPC) 的服务器到客户端远程过程调用，该程序调用客户端浏览器中的 JavaScript 函数 (和从服务器端 .NET 代码) 的其他客户端平台。</span><span class="sxs-lookup"><span data-stu-id="5bc42-117">SignalR provides a simple API for creating server-to-client remote procedure calls (RPC) that call JavaScript functions in client browsers (and other client platforms) from server-side .NET code.</span></span> <span data-ttu-id="5bc42-118">SignalR 还包括用于连接管理的 API (例如，连接和断开连接事件) ，以及对连接进行分组。</span><span class="sxs-lookup"><span data-stu-id="5bc42-118">SignalR also includes API for connection management (for instance, connect and disconnect events), and grouping connections.</span></span>

![通过 SignalR 调用方法](introduction-to-signalr/_static/image1.png)

<span data-ttu-id="5bc42-120">SignalR 自动处理连接管理，让你可同时向所有连接的客户端广播消息，就像聊天室一样。</span><span class="sxs-lookup"><span data-stu-id="5bc42-120">SignalR handles connection management automatically, and lets you broadcast messages to all connected clients simultaneously, like a chat room.</span></span> <span data-ttu-id="5bc42-121">也可以向特定客户端发送消息。</span><span class="sxs-lookup"><span data-stu-id="5bc42-121">You can also send messages to specific clients.</span></span> <span data-ttu-id="5bc42-122">客户端和服务器之间的连接是持久的，不同于传统的 HTTP 连接，后者针对每次通信重新建立。</span><span class="sxs-lookup"><span data-stu-id="5bc42-122">The connection between the client and server is persistent, unlike a classic HTTP connection, which is re-established for each communication.</span></span>

<span data-ttu-id="5bc42-123">SignalR 支持 "服务器推送" 功能，在该功能中，服务器代码可以使用远程过程调用来调用浏览器中的客户端代码 (RPC) ，而不是目前在 web 上通用的请求-响应模式。</span><span class="sxs-lookup"><span data-stu-id="5bc42-123">SignalR supports "server push" functionality, in which server code can call out to client code in the browser using Remote Procedure Calls (RPC), rather than the request-response model common on the web today.</span></span>

<span data-ttu-id="5bc42-124">使用内置和第三方横向扩展提供程序，SignalR 应用程序可以向外扩展到数千个客户端。</span><span class="sxs-lookup"><span data-stu-id="5bc42-124">SignalR applications can scale out to thousands of clients using built-in, and third-party scale-out providers.</span></span>

<span data-ttu-id="5bc42-125">内置提供程序包括：</span><span class="sxs-lookup"><span data-stu-id="5bc42-125">Built-in providers include:</span></span>
* [<span data-ttu-id="5bc42-126">服务总线</span><span class="sxs-lookup"><span data-stu-id="5bc42-126">Service Bus</span></span>](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.ServiceBus3)
* [<span data-ttu-id="5bc42-127">SQL Server</span><span class="sxs-lookup"><span data-stu-id="5bc42-127">SQL Server</span></span>](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.SqlServer)
* [<span data-ttu-id="5bc42-128">Redis</span><span class="sxs-lookup"><span data-stu-id="5bc42-128">Redis</span></span>](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.Redis)

<span data-ttu-id="5bc42-129">第三方提供程序包括：</span><span class="sxs-lookup"><span data-stu-id="5bc42-129">Third-party providers include:</span></span>
* <span data-ttu-id="5bc42-130">[NCache](https://www.alachisoft.com/ncache/asp-net-core-signalr.html)。</span><span class="sxs-lookup"><span data-stu-id="5bc42-130">[NCache](https://www.alachisoft.com/ncache/asp-net-core-signalr.html).</span></span>

<span data-ttu-id="5bc42-131">SignalR 是开放源代码，可通过 [GitHub](https://github.com/signalr)访问。</span><span class="sxs-lookup"><span data-stu-id="5bc42-131">SignalR is open-source, accessible through [GitHub](https://github.com/signalr).</span></span>

## <a name="signalr-and-websocket"></a><span data-ttu-id="5bc42-132">SignalR 和 WebSocket</span><span class="sxs-lookup"><span data-stu-id="5bc42-132">SignalR and WebSocket</span></span>

<span data-ttu-id="5bc42-133">SignalR 使用新的 WebSocket 传输（如果可用），并在必要时回退到较旧的传输。</span><span class="sxs-lookup"><span data-stu-id="5bc42-133">SignalR uses the new WebSocket transport where available and falls back to older transports where necessary.</span></span> <span data-ttu-id="5bc42-134">虽然当然，你可以直接使用 WebSocket 编写应用，但使用 SignalR 意味着你需要实现的很多额外功能都已完成。</span><span class="sxs-lookup"><span data-stu-id="5bc42-134">While you could certainly write your app using WebSocket directly, using SignalR means that a lot of the extra functionality you would need to implement is already done for you.</span></span> <span data-ttu-id="5bc42-135">最重要的是，这意味着您可以对应用程序进行编码，以便利用 WebSocket，而不必担心为较旧的客户端创建单独的代码路径。</span><span class="sxs-lookup"><span data-stu-id="5bc42-135">Most importantly, this means that you can code your app to take advantage of WebSocket without having to worry about creating a separate code path for older clients.</span></span> <span data-ttu-id="5bc42-136">SignalR 还会使你不必担心对 WebSocket 的更新，因为 SignalR 会更新为支持基础传输中的更改，从而为你的应用程序提供跨 WebSocket 版本的一致接口。</span><span class="sxs-lookup"><span data-stu-id="5bc42-136">SignalR also shields you from having to worry about updates to WebSocket, since SignalR is updated to support changes in the underlying transport, providing your application a consistent interface across versions of WebSocket.</span></span>

<a id="transports"></a>

## <a name="transports-and-fallbacks"></a><span data-ttu-id="5bc42-137">传输和回退</span><span class="sxs-lookup"><span data-stu-id="5bc42-137">Transports and fallbacks</span></span>

<span data-ttu-id="5bc42-138">SignalR 是对在客户端和服务器之间进行实时工作所需的某些传输的抽象。</span><span class="sxs-lookup"><span data-stu-id="5bc42-138">SignalR is an abstraction over some of the transports that are required to do real-time work between client and server.</span></span> <span data-ttu-id="5bc42-139">如果可能，SignalR 将首先尝试建立 WebSocket 连接。</span><span class="sxs-lookup"><span data-stu-id="5bc42-139">SignalR first attempts to establish a WebSocket connection if possible.</span></span> <span data-ttu-id="5bc42-140">WebSocket 是 SignalR 的最佳传输，因为它具有以下内容：</span><span class="sxs-lookup"><span data-stu-id="5bc42-140">WebSocket is the optimal transport for SignalR because it has:</span></span>

* <span data-ttu-id="5bc42-141">最有效地使用服务器内存。</span><span class="sxs-lookup"><span data-stu-id="5bc42-141">The most efficient use of server memory.</span></span>
* <span data-ttu-id="5bc42-142">延迟最低。</span><span class="sxs-lookup"><span data-stu-id="5bc42-142">The lowest latency.</span></span>
* <span data-ttu-id="5bc42-143">最底层的功能，如客户端和服务器之间的全双工通信。</span><span class="sxs-lookup"><span data-stu-id="5bc42-143">The most underlying features, such as full duplex communication between client and server.</span></span>
* <span data-ttu-id="5bc42-144">最严格的要求是，WebSocket 需要服务器：</span><span class="sxs-lookup"><span data-stu-id="5bc42-144">The most stringent requirements, WebSocket requires the server:</span></span>
  * <span data-ttu-id="5bc42-145">在 Windows Server 2012 或 Windows 8 上运行。</span><span class="sxs-lookup"><span data-stu-id="5bc42-145">Run on Windows Server 2012 or Windows 8.</span></span>
  * <span data-ttu-id="5bc42-146">.NET Framework 4.5。</span><span class="sxs-lookup"><span data-stu-id="5bc42-146">.NET Framework 4.5.</span></span>

<span data-ttu-id="5bc42-147">如果未满足这些要求，则 SignalR 会尝试使用其他传输进行连接。</span><span class="sxs-lookup"><span data-stu-id="5bc42-147">If these requirements are not met, SignalR attempts to use other transports to make its connections.</span></span>

### <a name="html-5-transports"></a><span data-ttu-id="5bc42-148">HTML 5 传输</span><span class="sxs-lookup"><span data-stu-id="5bc42-148">HTML 5 transports</span></span>

<span data-ttu-id="5bc42-149">这些传输依赖于对 [HTML 5](http://en.wikipedia.org/wiki/HTML5)的支持。</span><span class="sxs-lookup"><span data-stu-id="5bc42-149">These transports depend on support for [HTML 5](http://en.wikipedia.org/wiki/HTML5).</span></span> <span data-ttu-id="5bc42-150">如果客户端浏览器不支持 HTML 5 标准版，将使用较旧的传输。</span><span class="sxs-lookup"><span data-stu-id="5bc42-150">If the client browser does not support the HTML 5 standard, older transports will be used.</span></span>

- <span data-ttu-id="5bc42-151">**Websocket** (如果服务器和浏览器都指示它们可以支持 WebSocket) 。</span><span class="sxs-lookup"><span data-stu-id="5bc42-151">**WebSocket** (if both the server and browser indicate they can support Websocket).</span></span> <span data-ttu-id="5bc42-152">WebSocket 是在客户端与服务器之间建立真正持久的双向连接的唯一传输。</span><span class="sxs-lookup"><span data-stu-id="5bc42-152">WebSocket is the only transport that establishes a true persistent, two-way connection between client and server.</span></span> <span data-ttu-id="5bc42-153">但是，WebSocket 还具有最严格的要求;它仅在最新版本的 Microsoft Internet Explorer、Google Chrome 和 Mozilla Firefox 中完全受支持，并且在某些浏览器（如 Opera 和 Safari）中仅有部分实现。</span><span class="sxs-lookup"><span data-stu-id="5bc42-153">However, WebSocket also has the most stringent requirements; it is fully supported only in the latest versions of Microsoft Internet Explorer, Google Chrome, and Mozilla Firefox, and only has a partial implementation in other browsers such as Opera and Safari.</span></span>
- <span data-ttu-id="5bc42-154">如果浏览器支持服务器发送事件（基本上是 Internet Explorer 之外的所有浏览器），**服务器发送事件**（也称为 EventSource (）。 ) </span><span class="sxs-lookup"><span data-stu-id="5bc42-154">**Server Sent Events**, also known as EventSource (if the browser supports Server Sent Events, which is basically all browsers except Internet Explorer.)</span></span>

### <a name="comet-transports"></a><span data-ttu-id="5bc42-155">Comet 传输</span><span class="sxs-lookup"><span data-stu-id="5bc42-155">Comet transports</span></span>

<span data-ttu-id="5bc42-156">以下传输基于 [Comet](http://en.wikipedia.org/wiki/Comet_(programming)) web 应用程序模型，在该模型中，浏览器或其他客户端维护长时间的 HTTP 请求，服务器可以使用该模型将数据推送到客户端，而客户端无需专门请求它。</span><span class="sxs-lookup"><span data-stu-id="5bc42-156">The following transports are based on the [Comet](http://en.wikipedia.org/wiki/Comet_(programming)) web application model, in which a browser or other client maintains a long-held HTTP request, which the server can use to push data to the client without the client specifically requesting it.</span></span>

- <span data-ttu-id="5bc42-157">仅) Internet Explorer (的 "**永久帧**"。</span><span class="sxs-lookup"><span data-stu-id="5bc42-157">**Forever Frame** (for Internet Explorer only).</span></span> <span data-ttu-id="5bc42-158">永久帧创建一个隐藏的 IFrame，该 IFrame 向服务器上不能完成的终结点发出请求。</span><span class="sxs-lookup"><span data-stu-id="5bc42-158">Forever Frame creates a hidden IFrame which makes a request to an endpoint on the server that does not complete.</span></span> <span data-ttu-id="5bc42-159">服务器随后会持续向客户端发送脚本，该脚本会立即执行，提供从服务器到客户端的单向实时连接。</span><span class="sxs-lookup"><span data-stu-id="5bc42-159">The server then continually sends script to the client which is immediately executed, providing a one-way realtime connection from server to client.</span></span> <span data-ttu-id="5bc42-160">从客户端到服务器的连接使用与服务器之间的单独连接连接到客户端连接，与标准 HTTP 请求一样，为需要发送的每个数据段创建新连接。</span><span class="sxs-lookup"><span data-stu-id="5bc42-160">The connection from client to server uses a separate connection from the server to client connection, and like a standard HTTP request, a new connection is created for each piece of data that needs to be sent.</span></span>
- <span data-ttu-id="5bc42-161">**Ajax 长轮询**。</span><span class="sxs-lookup"><span data-stu-id="5bc42-161">**Ajax long polling**.</span></span> <span data-ttu-id="5bc42-162">长轮询不会创建持续性连接，而是使用保持打开状态的请求轮询服务器，直到服务器响应为止，此时连接将关闭，并立即请求新连接。</span><span class="sxs-lookup"><span data-stu-id="5bc42-162">Long polling does not create a persistent connection, but instead polls the server with a request that stays open until the server responds, at which point the connection closes, and a new connection is requested immediately.</span></span> <span data-ttu-id="5bc42-163">在连接重置时，这可能会导致一些延迟。</span><span class="sxs-lookup"><span data-stu-id="5bc42-163">This may introduce some latency while the connection resets.</span></span>

<span data-ttu-id="5bc42-164">有关在哪些配置下支持哪些传输的详细信息，请参阅 [支持的平台](supported-platforms.md)。</span><span class="sxs-lookup"><span data-stu-id="5bc42-164">For more information on what transports are supported under which configurations, see [Supported Platforms](supported-platforms.md).</span></span>

### <a name="transport-selection-process"></a><span data-ttu-id="5bc42-165">传输选择过程</span><span class="sxs-lookup"><span data-stu-id="5bc42-165">Transport selection process</span></span>

<span data-ttu-id="5bc42-166">以下列表显示了 SignalR 用于确定要使用的传输的步骤。</span><span class="sxs-lookup"><span data-stu-id="5bc42-166">The following list shows the steps that SignalR uses to decide which transport to use.</span></span>

1. <span data-ttu-id="5bc42-167">如果浏览器是 Internet Explorer 8 或更早版本，则使用长轮询。</span><span class="sxs-lookup"><span data-stu-id="5bc42-167">If the browser is Internet Explorer 8 or earlier, Long Polling is used.</span></span>
2. <span data-ttu-id="5bc42-168">如果 JSONP 配置为 (即，则在 `jsonp` `true` 启动连接) 时，参数设置为，使用长轮询。</span><span class="sxs-lookup"><span data-stu-id="5bc42-168">If JSONP is configured (that is, the `jsonp` parameter is set to `true` when the connection is started), Long Polling is used.</span></span>
3. <span data-ttu-id="5bc42-169">如果正在建立跨域连接 (即，如果 SignalR 终结点与托管页) 不在同一域中，则在满足以下条件时将使用 WebSocket：</span><span class="sxs-lookup"><span data-stu-id="5bc42-169">If a cross-domain connection is being made (that is, if the SignalR endpoint is not in the same domain as the hosting page), then WebSocket will be used if the following criteria are met:</span></span>

   - <span data-ttu-id="5bc42-170">客户端支持 CORS (跨域资源共享) 。</span><span class="sxs-lookup"><span data-stu-id="5bc42-170">The client supports CORS (Cross-Origin Resource Sharing).</span></span> <span data-ttu-id="5bc42-171">有关哪些客户端支持 CORS 的详细信息，请参阅 [caniuse.com 上的 cors](http://www.caniuse.com/CORS)。</span><span class="sxs-lookup"><span data-stu-id="5bc42-171">For details on which clients support CORS, see [CORS at caniuse.com](http://www.caniuse.com/CORS).</span></span>
   - <span data-ttu-id="5bc42-172">客户端支持 WebSocket</span><span class="sxs-lookup"><span data-stu-id="5bc42-172">The client supports WebSocket</span></span>
   - <span data-ttu-id="5bc42-173">服务器支持 WebSocket</span><span class="sxs-lookup"><span data-stu-id="5bc42-173">The server supports WebSocket</span></span>

     <span data-ttu-id="5bc42-174">如果未满足这些条件中的任何一个，将使用长轮询。</span><span class="sxs-lookup"><span data-stu-id="5bc42-174">If any of these criteria are not met, Long Polling will be used.</span></span> <span data-ttu-id="5bc42-175">有关跨域连接的详细信息，请参阅 [如何建立跨域连接](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)。</span><span class="sxs-lookup"><span data-stu-id="5bc42-175">For more information on cross-domain connections, see [How to establish a cross-domain connection](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).</span></span>
4. <span data-ttu-id="5bc42-176">如果未配置 JSONP 并且连接不跨域，则在客户端和服务器均支持时，将使用 WebSocket。</span><span class="sxs-lookup"><span data-stu-id="5bc42-176">If JSONP is not configured and the connection is not cross-domain, WebSocket will be used if both the client and server support it.</span></span>
5. <span data-ttu-id="5bc42-177">如果客户端或服务器不支持 WebSocket，则使用服务器发送事件（如果可用）。</span><span class="sxs-lookup"><span data-stu-id="5bc42-177">If either the client or server do not support WebSocket, Server Sent Events is used if it is available.</span></span>
6. <span data-ttu-id="5bc42-178">如果 "服务器发送事件" 不可用，则将尝试永久帧。</span><span class="sxs-lookup"><span data-stu-id="5bc42-178">If Server Sent Events is not available, Forever Frame is attempted.</span></span>
7. <span data-ttu-id="5bc42-179">如果永久帧失败，则使用长轮询。</span><span class="sxs-lookup"><span data-stu-id="5bc42-179">If Forever Frame fails, Long Polling is used.</span></span>

<a id="MonitoringTransports"></a>
### <a name="monitoring-transports"></a><span data-ttu-id="5bc42-180">监视传输</span><span class="sxs-lookup"><span data-stu-id="5bc42-180">Monitoring transports</span></span>

<span data-ttu-id="5bc42-181">可以通过在中心启用日志记录，并在浏览器中打开控制台窗口，来确定应用程序使用的传输方式。</span><span class="sxs-lookup"><span data-stu-id="5bc42-181">You can determine what transport your application is using by enabling logging on your hub, and opening the console window in your browser.</span></span>

<span data-ttu-id="5bc42-182">若要在浏览器中为中心的事件启用日志记录，请将以下命令添加到客户端应用程序：</span><span class="sxs-lookup"><span data-stu-id="5bc42-182">To enable logging for your hub's events in a browser, add the following command to your client application:</span></span>

`$.connection.hub.logging = true;`

- <span data-ttu-id="5bc42-183">在 Internet Explorer 中，按 F12 打开开发人员工具，然后单击 "控制台" 选项卡。</span><span class="sxs-lookup"><span data-stu-id="5bc42-183">In Internet Explorer, open the developer tools by pressing F12, and click the Console tab.</span></span>

    ![Microsoft Internet Explorer 中的控制台](introduction-to-signalr/_static/image2.png)
- <span data-ttu-id="5bc42-185">在 Chrome 中，按 Ctrl + Shift + J 打开控制台。</span><span class="sxs-lookup"><span data-stu-id="5bc42-185">In Chrome, open the console by pressing Ctrl+Shift+J.</span></span>

    ![Google Chrome 中的控制台](introduction-to-signalr/_static/image3.png)

<span data-ttu-id="5bc42-187">启用控制台打开并启用日志记录后，你将能够查看 SignalR 所使用的传输。</span><span class="sxs-lookup"><span data-stu-id="5bc42-187">With the console open and logging enabled, you'll be able to see which transport is being used by SignalR.</span></span>

![Internet Explorer 中显示 WebSocket 传输的控制台](introduction-to-signalr/_static/image4.png)

### <a name="specifying-a-transport"></a><span data-ttu-id="5bc42-189">指定传输</span><span class="sxs-lookup"><span data-stu-id="5bc42-189">Specifying a transport</span></span>

<span data-ttu-id="5bc42-190">协商传输会占用一定的时间和客户端/服务器资源。</span><span class="sxs-lookup"><span data-stu-id="5bc42-190">Negotiating a transport takes a certain amount of time and client/server resources.</span></span> <span data-ttu-id="5bc42-191">如果客户端功能已知，则可以在启动客户端连接时指定传输。</span><span class="sxs-lookup"><span data-stu-id="5bc42-191">If the client capabilities are known, then a transport can be specified when the client connection is started.</span></span> <span data-ttu-id="5bc42-192">下面的代码段演示如何使用 Ajax 长轮询传输开始连接，如果已知客户端不支持任何其他协议，则使用该连接：</span><span class="sxs-lookup"><span data-stu-id="5bc42-192">The following code snippet demonstrates starting a connection using the Ajax Long Polling transport, as would be used if it was known that the client did not support any other protocol:</span></span>

`connection.start({ transport: 'longPolling' });`

<span data-ttu-id="5bc42-193">如果希望客户端按顺序尝试特定传输，可以指定回退顺序。</span><span class="sxs-lookup"><span data-stu-id="5bc42-193">You can specify a fallback order if you want a client to try specific transports in order.</span></span> <span data-ttu-id="5bc42-194">下面的代码片段演示了如何尝试 WebSocket，并失败了，这将直接转到长轮询。</span><span class="sxs-lookup"><span data-stu-id="5bc42-194">The following code snippet demonstrates trying WebSocket, and failing that, going directly to Long Polling.</span></span>

`connection.start({ transport: ['webSockets','longPolling'] });`

<span data-ttu-id="5bc42-195">用于指定传输的字符串常量定义如下：</span><span class="sxs-lookup"><span data-stu-id="5bc42-195">The string constants for specifying transports are defined as follows:</span></span>

- `webSockets`
- `foreverFrame`
- `serverSentEvents`
- `longPolling`

## <a name="connections-and-hubs"></a><span data-ttu-id="5bc42-196">连接和集线器</span><span class="sxs-lookup"><span data-stu-id="5bc42-196">Connections and Hubs</span></span>

<span data-ttu-id="5bc42-197">SignalR API 包含两种用于在客户端和服务器之间进行通信的模型：持久性连接和中心。</span><span class="sxs-lookup"><span data-stu-id="5bc42-197">The SignalR API contains two models for communicating between clients and servers: Persistent Connections and Hubs.</span></span>

<span data-ttu-id="5bc42-198">连接表示用于发送单接收方、分组或广播消息的简单终结点。</span><span class="sxs-lookup"><span data-stu-id="5bc42-198">A Connection represents a simple endpoint for sending single-recipient, grouped, or broadcast messages.</span></span> <span data-ttu-id="5bc42-199">持久性连接 API (在 .NET 代码中由 PersistentConnection 类表示) 使开发人员能够直接访问 SignalR 公开的低级别通信协议。</span><span class="sxs-lookup"><span data-stu-id="5bc42-199">The Persistent Connection API (represented in .NET code by the PersistentConnection class) gives the developer direct access to the low-level communication protocol that SignalR exposes.</span></span> <span data-ttu-id="5bc42-200">使用基于连接的 Api （如 Windows Communication Foundation）的开发人员将对使用连接通信模型非常熟悉。</span><span class="sxs-lookup"><span data-stu-id="5bc42-200">Using the Connections communication model will be familiar to developers who have used connection-based APIs such as Windows Communication Foundation.</span></span>

<span data-ttu-id="5bc42-201">中心是一种基于连接 API 构建的更高级别管道，它允许客户端和服务器直接调用方法。</span><span class="sxs-lookup"><span data-stu-id="5bc42-201">A Hub is a more high-level pipeline built upon the Connection API that allows your client and server to call methods on each other directly.</span></span> <span data-ttu-id="5bc42-202">SignalR 按魔术处理跨计算机边界的调度，使客户端能够像本地方法一样轻松地调用服务器上的方法，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="5bc42-202">SignalR handles the dispatching across machine boundaries as if by magic, allowing clients to call methods on the server as easily as local methods, and vice versa.</span></span> <span data-ttu-id="5bc42-203">如果开发人员已使用远程调用 Api （如 .NET 远程处理），则将对使用中心通信模型非常熟悉。</span><span class="sxs-lookup"><span data-stu-id="5bc42-203">Using the Hubs communication model will be familiar to developers who have used remote invocation APIs such as .NET Remoting.</span></span> <span data-ttu-id="5bc42-204">使用集线器还可以将强类型参数传递给方法，从而启用模型绑定。</span><span class="sxs-lookup"><span data-stu-id="5bc42-204">Using a Hub also allows you to pass strongly typed parameters to methods, enabling model binding.</span></span>

### <a name="architecture-diagram"></a><span data-ttu-id="5bc42-205">体系结构关系图</span><span class="sxs-lookup"><span data-stu-id="5bc42-205">Architecture diagram</span></span>

<span data-ttu-id="5bc42-206">下图显示了集线器、永久性连接和用于传输的底层技术之间的关系。</span><span class="sxs-lookup"><span data-stu-id="5bc42-206">The following diagram shows the relationship between Hubs, Persistent Connections, and the underlying technologies used for transports.</span></span>

![显示 Api、传输和客户端的 SignalR 体系结构图](introduction-to-signalr/_static/image5.png)

### <a name="how-hubs-work"></a><span data-ttu-id="5bc42-208">集线器的工作方式</span><span class="sxs-lookup"><span data-stu-id="5bc42-208">How Hubs work</span></span>

<span data-ttu-id="5bc42-209">当服务器端代码在客户端上调用方法时，会在包含要调用的方法的名称和参数的活动传输中发送一个数据包 (当对象作为方法参数发送时，将使用 JSON) 对该对象进行序列化。</span><span class="sxs-lookup"><span data-stu-id="5bc42-209">When server-side code calls a method on the client, a packet is sent across the active transport that contains the name and parameters of the method to be called (when an object is sent as a method parameter, it is serialized using JSON).</span></span> <span data-ttu-id="5bc42-210">然后，客户端将方法名称与在客户端代码中定义的方法相匹配。</span><span class="sxs-lookup"><span data-stu-id="5bc42-210">The client then matches the method name to methods defined in client-side code.</span></span> <span data-ttu-id="5bc42-211">如果存在匹配项，则将使用反序列化的参数数据执行客户端方法。</span><span class="sxs-lookup"><span data-stu-id="5bc42-211">If there is a match, the client method will be executed using the deserialized parameter data.</span></span>

<span data-ttu-id="5bc42-212">可以使用 Fiddler 等工具监视此方法调用 [。](http://fiddler2.com/)</span><span class="sxs-lookup"><span data-stu-id="5bc42-212">The method call can be monitored using tools like [Fiddler.](http://fiddler2.com/)</span></span> <span data-ttu-id="5bc42-213">下图显示了在 Fiddler 的 "日志" 窗格中从 SignalR 服务器发送到 web 浏览器客户端的方法调用。</span><span class="sxs-lookup"><span data-stu-id="5bc42-213">The following image shows a method call sent from a SignalR server to a web browser client in the Logs pane of Fiddler.</span></span> <span data-ttu-id="5bc42-214">正在从名为的中心发送方法调用 `MoveShapeHub` ，并且调用被调用的方法 `updateShape` 。</span><span class="sxs-lookup"><span data-stu-id="5bc42-214">The method call is being sent from a hub called `MoveShapeHub`, and the method being invoked is called `updateShape`.</span></span>

![显示 SignalR 流量的 Fiddler 日志的视图](introduction-to-signalr/_static/image6.png)

<span data-ttu-id="5bc42-216">在此示例中，通过参数标识中心名称 `H` ; 方法名用 `M` 参数标识，发送到方法的数据用 `A` 参数标识。</span><span class="sxs-lookup"><span data-stu-id="5bc42-216">In this example, the hub name is identified with the `H` parameter; the method name is identified with the `M` parameter, and the data being sent to the method is identified with the `A` parameter.</span></span> <span data-ttu-id="5bc42-217">生成此消息的应用程序将在 [高频实时](tutorial-high-frequency-realtime-with-signalr.md) 教程中创建。</span><span class="sxs-lookup"><span data-stu-id="5bc42-217">The application that generated this message is created in the [High-Frequency Realtime](tutorial-high-frequency-realtime-with-signalr.md) tutorial.</span></span>

### <a name="choosing-a-communication-model"></a><span data-ttu-id="5bc42-218">选择通信模型</span><span class="sxs-lookup"><span data-stu-id="5bc42-218">Choosing a communication model</span></span>

<span data-ttu-id="5bc42-219">大多数应用程序应使用中心 API。</span><span class="sxs-lookup"><span data-stu-id="5bc42-219">Most applications should use the Hubs API.</span></span> <span data-ttu-id="5bc42-220">连接 API 可用于以下情况：</span><span class="sxs-lookup"><span data-stu-id="5bc42-220">The Connections API could be used in the following circumstances:</span></span>

- <span data-ttu-id="5bc42-221">需要指定所发送的实际邮件的格式。</span><span class="sxs-lookup"><span data-stu-id="5bc42-221">The format of the actual message sent needs to be specified.</span></span>
- <span data-ttu-id="5bc42-222">开发人员首选使用消息传递和调度模型，而不使用远程调用模型。</span><span class="sxs-lookup"><span data-stu-id="5bc42-222">The developer prefers to work with a messaging and dispatching model rather than a remote invocation model.</span></span>
- <span data-ttu-id="5bc42-223">使用消息传送模型的现有应用程序正在移植，以使用 SignalR。</span><span class="sxs-lookup"><span data-stu-id="5bc42-223">An existing application that uses a messaging model is being ported to use SignalR.</span></span>

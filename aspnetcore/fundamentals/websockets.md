---
title: ASP.NET Core 中的 WebSocket 支持
author: rick-anderson
description: 了解如何在 ASP.NET Core 中开始使用 WebSocket。
monikerRange: '>= aspnetcore-1.1'
ms.author: tdykstra
ms.custom: mvc
ms.date: 01/17/2019
uid: fundamentals/websockets
ms.openlocfilehash: 76acb9c96ed5e8bbbaf39eeb6cb23307bb44fb8d
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57031404"
---
# <a name="websockets-support-in-aspnet-core"></a><span data-ttu-id="a2147-103">ASP.NET Core 中的 WebSocket 支持</span><span class="sxs-lookup"><span data-stu-id="a2147-103">WebSockets support in ASP.NET Core</span></span>

<span data-ttu-id="a2147-104">作者：[Tom Dykstra](https://github.com/tdykstra) 和 [Andrew Stanton-Nurse](https://github.com/anurse)</span><span class="sxs-lookup"><span data-stu-id="a2147-104">By [Tom Dykstra](https://github.com/tdykstra) and [Andrew Stanton-Nurse](https://github.com/anurse)</span></span>

<span data-ttu-id="a2147-105">本文介绍 ASP.NET Core 中 WebSocket 的入门方法。</span><span class="sxs-lookup"><span data-stu-id="a2147-105">This article explains how to get started with WebSockets in ASP.NET Core.</span></span> <span data-ttu-id="a2147-106">[WebSocket](https://wikipedia.org/wiki/WebSocket) ([RFC 6455](https://tools.ietf.org/html/rfc6455)) 是一个协议，支持通过 TCP 连接建立持久的双向信道。</span><span class="sxs-lookup"><span data-stu-id="a2147-106">[WebSocket](https://wikipedia.org/wiki/WebSocket) ([RFC 6455](https://tools.ietf.org/html/rfc6455)) is a protocol that enables two-way persistent communication channels over TCP connections.</span></span> <span data-ttu-id="a2147-107">它用于从快速实时通信中获益的应用，如聊天、仪表板和游戏应用。</span><span class="sxs-lookup"><span data-stu-id="a2147-107">It's used in apps that benefit from fast, real-time communication, such as chat, dashboard, and game apps.</span></span>

<span data-ttu-id="a2147-108">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/websockets/samples)（[如何下载](xref:index#how-to-download-a-sample)）。</span><span class="sxs-lookup"><span data-stu-id="a2147-108">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/websockets/samples) ([how to download](xref:index#how-to-download-a-sample)).</span></span> <span data-ttu-id="a2147-109">有关详细信息，请参阅[后续步骤](#next-steps)部分。</span><span class="sxs-lookup"><span data-stu-id="a2147-109">See the [Next steps](#next-steps) section for more information.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a2147-110">系统必备</span><span class="sxs-lookup"><span data-stu-id="a2147-110">Prerequisites</span></span>

* <span data-ttu-id="a2147-111">ASP.NET Core 1.1 或更高版本</span><span class="sxs-lookup"><span data-stu-id="a2147-111">ASP.NET Core 1.1 or later</span></span>
* <span data-ttu-id="a2147-112">支持 ASP.NET Core 的任何操作系统：</span><span class="sxs-lookup"><span data-stu-id="a2147-112">Any OS that supports ASP.NET Core:</span></span>
  
  * <span data-ttu-id="a2147-113">Windows 7/Windows Server 2008 或更高版本</span><span class="sxs-lookup"><span data-stu-id="a2147-113">Windows 7 / Windows Server 2008 or later</span></span>
  * <span data-ttu-id="a2147-114">Linux</span><span class="sxs-lookup"><span data-stu-id="a2147-114">Linux</span></span>
  * <span data-ttu-id="a2147-115">macOS</span><span class="sxs-lookup"><span data-stu-id="a2147-115">macOS</span></span>
  
* <span data-ttu-id="a2147-116">如果应用在安装了 IIS 的 Windows 上运行：</span><span class="sxs-lookup"><span data-stu-id="a2147-116">If the app runs on Windows with IIS:</span></span>

  * <span data-ttu-id="a2147-117">Windows 8 / Windows Server 2012 及更高版本</span><span class="sxs-lookup"><span data-stu-id="a2147-117">Windows 8 / Windows Server 2012 or later</span></span>
  * <span data-ttu-id="a2147-118">IIS 8 / IIS 8 Express</span><span class="sxs-lookup"><span data-stu-id="a2147-118">IIS 8 / IIS 8 Express</span></span>
  * <span data-ttu-id="a2147-119">必须启用 WebSocket（请参阅 [IIS/IIS Express 支持](#iisiis-express-support)部分。）。</span><span class="sxs-lookup"><span data-stu-id="a2147-119">WebSockets must be enabled (See the [IIS/IIS Express support](#iisiis-express-support) section.).</span></span>
  
* <span data-ttu-id="a2147-120">如果应用在 [HTTP.sys](xref:fundamentals/servers/httpsys) 上运行：</span><span class="sxs-lookup"><span data-stu-id="a2147-120">If the app runs on [HTTP.sys](xref:fundamentals/servers/httpsys):</span></span>

  * <span data-ttu-id="a2147-121">Windows 8 / Windows Server 2012 及更高版本</span><span class="sxs-lookup"><span data-stu-id="a2147-121">Windows 8 / Windows Server 2012 or later</span></span>

* <span data-ttu-id="a2147-122">有关支持的浏览器，请参阅 https://caniuse.com/#feat=websockets。</span><span class="sxs-lookup"><span data-stu-id="a2147-122">For supported browsers, see https://caniuse.com/#feat=websockets.</span></span>

## <a name="when-to-use-websockets"></a><span data-ttu-id="a2147-123">何时使用 WebSocket</span><span class="sxs-lookup"><span data-stu-id="a2147-123">When to use WebSockets</span></span>

<span data-ttu-id="a2147-124">通过 WebSocket 可直接使用套接字连接。</span><span class="sxs-lookup"><span data-stu-id="a2147-124">Use WebSockets to work directly with a socket connection.</span></span> <span data-ttu-id="a2147-125">例如，使用 WebSocket 可以让实时游戏达到最佳性能。</span><span class="sxs-lookup"><span data-stu-id="a2147-125">For example, use WebSockets for the best possible performance with a real-time game.</span></span>

<span data-ttu-id="a2147-126">[ASP.NET Core SignalR](xref:signalr/introduction) 是一个库，可用于简化向应用添加实时 Web 功能。</span><span class="sxs-lookup"><span data-stu-id="a2147-126">[ASP.NET Core SignalR](xref:signalr/introduction) is a library that simplifies adding real-time web functionality to apps.</span></span> <span data-ttu-id="a2147-127">它会尽可能地使用 WebSocket。</span><span class="sxs-lookup"><span data-stu-id="a2147-127">It uses WebSockets whenever possible.</span></span>

## <a name="how-to-use-websockets"></a><span data-ttu-id="a2147-128">如何使用 Websocket</span><span class="sxs-lookup"><span data-stu-id="a2147-128">How to use WebSockets</span></span>

* <span data-ttu-id="a2147-129">安装 [Microsoft.AspNetCore.WebSockets](https://www.nuget.org/packages/Microsoft.AspNetCore.WebSockets/) 包。</span><span class="sxs-lookup"><span data-stu-id="a2147-129">Install the [Microsoft.AspNetCore.WebSockets](https://www.nuget.org/packages/Microsoft.AspNetCore.WebSockets/) package.</span></span>
* <span data-ttu-id="a2147-130">配置中间件。</span><span class="sxs-lookup"><span data-stu-id="a2147-130">Configure the middleware.</span></span>
* <span data-ttu-id="a2147-131">接受 WebSocket 请求。</span><span class="sxs-lookup"><span data-stu-id="a2147-131">Accept WebSocket requests.</span></span>
* <span data-ttu-id="a2147-132">发送和接收消息。</span><span class="sxs-lookup"><span data-stu-id="a2147-132">Send and receive messages.</span></span>

### <a name="configure-the-middleware"></a><span data-ttu-id="a2147-133">配置中间件</span><span class="sxs-lookup"><span data-stu-id="a2147-133">Configure the middleware</span></span>

<span data-ttu-id="a2147-134">在 `Startup` 类的 `Configure` 方法中添加 WebSocket 中间件：</span><span class="sxs-lookup"><span data-stu-id="a2147-134">Add the WebSockets middleware in the `Configure` method of the `Startup` class:</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](websockets/samples/2.x/WebSocketsSample/Startup.cs?name=UseWebSockets)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](websockets/samples/1.x/WebSocketsSample/Startup.cs?name=UseWebSockets)]

::: moniker-end

::: moniker range="< aspnetcore-2.2"

<span data-ttu-id="a2147-135">可配置以下设置：</span><span class="sxs-lookup"><span data-stu-id="a2147-135">The following settings can be configured:</span></span>

* <span data-ttu-id="a2147-136">`KeepAliveInterval` - 向客户端发送“ping”帧的频率，以确保代理保持连接处于打开状态。</span><span class="sxs-lookup"><span data-stu-id="a2147-136">`KeepAliveInterval` - How frequently to send "ping" frames to the client to ensure proxies keep the connection open.</span></span> <span data-ttu-id="a2147-137">默认值为 2 分钟。</span><span class="sxs-lookup"><span data-stu-id="a2147-137">The default is two minutes.</span></span>
* <span data-ttu-id="a2147-138">`ReceiveBufferSize` - 用于接收数据的缓冲区的大小。</span><span class="sxs-lookup"><span data-stu-id="a2147-138">`ReceiveBufferSize` - The size of the buffer used to receive data.</span></span> <span data-ttu-id="a2147-139">高级用户可能需要对其进行更改，以便根据数据大小调整性能。</span><span class="sxs-lookup"><span data-stu-id="a2147-139">Advanced users may need to change this for performance tuning based on the size of the data.</span></span> <span data-ttu-id="a2147-140">默认值为 4 KB。</span><span class="sxs-lookup"><span data-stu-id="a2147-140">The default is 4 KB.</span></span>

::: moniker-end

::: moniker range=">= aspnetcore-2.2"

<span data-ttu-id="a2147-141">可配置以下设置：</span><span class="sxs-lookup"><span data-stu-id="a2147-141">The following settings can be configured:</span></span>

* <span data-ttu-id="a2147-142">`KeepAliveInterval` - 向客户端发送“ping”帧的频率，以确保代理保持连接处于打开状态。</span><span class="sxs-lookup"><span data-stu-id="a2147-142">`KeepAliveInterval` - How frequently to send "ping" frames to the client to ensure proxies keep the connection open.</span></span> <span data-ttu-id="a2147-143">默认值为 2 分钟。</span><span class="sxs-lookup"><span data-stu-id="a2147-143">The default is two minutes.</span></span>
* <span data-ttu-id="a2147-144">`ReceiveBufferSize` - 用于接收数据的缓冲区的大小。</span><span class="sxs-lookup"><span data-stu-id="a2147-144">`ReceiveBufferSize` - The size of the buffer used to receive data.</span></span> <span data-ttu-id="a2147-145">高级用户可能需要对其进行更改，以便根据数据大小调整性能。</span><span class="sxs-lookup"><span data-stu-id="a2147-145">Advanced users may need to change this for performance tuning based on the size of the data.</span></span> <span data-ttu-id="a2147-146">默认值为 4 KB。</span><span class="sxs-lookup"><span data-stu-id="a2147-146">The default is 4 KB.</span></span>
* <span data-ttu-id="a2147-147">`AllowedOrigins` - 用于 WebSocket 请求的允许的 Origin 标头值列表。</span><span class="sxs-lookup"><span data-stu-id="a2147-147">`AllowedOrigins` - A list of allowed Origin header values for WebSocket requests.</span></span> <span data-ttu-id="a2147-148">默认情况下，允许使用所有源。</span><span class="sxs-lookup"><span data-stu-id="a2147-148">By default, all origins are allowed.</span></span> <span data-ttu-id="a2147-149">有关详细信息，请参阅以下“WebSocket 源限制”。</span><span class="sxs-lookup"><span data-stu-id="a2147-149">See "WebSocket origin restriction" below for details.</span></span>

::: moniker-end

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](websockets/samples/2.x/WebSocketsSample/Startup.cs?name=UseWebSocketsOptions)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](websockets/samples/1.x/WebSocketsSample/Startup.cs?name=UseWebSocketsOptions)]

::: moniker-end

### <a name="accept-websocket-requests"></a><span data-ttu-id="a2147-150">接受 WebSocket 请求</span><span class="sxs-lookup"><span data-stu-id="a2147-150">Accept WebSocket requests</span></span>

<span data-ttu-id="a2147-151">在请求生命周期后期（例如在 `Configure` 方法或 MVC 操作的后期），检查它是否是 WebSocket 请求并接受 WebSocket 请求。</span><span class="sxs-lookup"><span data-stu-id="a2147-151">Somewhere later in the request life cycle (later in the `Configure` method or in an MVC action, for example) check if it's a WebSocket request and accept the WebSocket request.</span></span>

<span data-ttu-id="a2147-152">以下示例来自 `Configure` 方法的后期：</span><span class="sxs-lookup"><span data-stu-id="a2147-152">The following example is from later in the `Configure` method:</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](websockets/samples/2.x/WebSocketsSample/Startup.cs?name=AcceptWebSocket&highlight=7)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](websockets/samples/1.x/WebSocketsSample/Startup.cs?name=AcceptWebSocket&highlight=7)]

::: moniker-end

<span data-ttu-id="a2147-153">WebSocket 请求可以来自任何 URL，但此示例代码只接受 `/ws` 的请求。</span><span class="sxs-lookup"><span data-stu-id="a2147-153">A WebSocket request could come in on any URL, but this sample code only accepts requests for `/ws`.</span></span>

### <a name="send-and-receive-messages"></a><span data-ttu-id="a2147-154">发送和接收消息</span><span class="sxs-lookup"><span data-stu-id="a2147-154">Send and receive messages</span></span>

<span data-ttu-id="a2147-155">`AcceptWebSocketAsync` 方法将 TCP 连接升级到 WebSocket 连接，并提供 [WebSocket](/dotnet/core/api/system.net.websockets.websocket) 对象。</span><span class="sxs-lookup"><span data-stu-id="a2147-155">The `AcceptWebSocketAsync` method upgrades the TCP connection to a WebSocket connection and provides a [WebSocket](/dotnet/core/api/system.net.websockets.websocket) object.</span></span> <span data-ttu-id="a2147-156">使用 `WebSocket` 对象发送和接收消息。</span><span class="sxs-lookup"><span data-stu-id="a2147-156">Use the `WebSocket` object to send and receive messages.</span></span>

<span data-ttu-id="a2147-157">之前显示的接受 WebSocket 请求的代码将 `WebSocket` 对象传递给 `Echo` 方法。</span><span class="sxs-lookup"><span data-stu-id="a2147-157">The code shown earlier that accepts the WebSocket request passes the `WebSocket` object to an `Echo` method.</span></span> <span data-ttu-id="a2147-158">代码接收消息并立即发回相同的消息。</span><span class="sxs-lookup"><span data-stu-id="a2147-158">The code receives a message and immediately sends back the same message.</span></span> <span data-ttu-id="a2147-159">循环发送和接收消息，直到客户端关闭连接：</span><span class="sxs-lookup"><span data-stu-id="a2147-159">Messages are sent and received in a loop until the client closes the connection:</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](websockets/samples/2.x/WebSocketsSample/Startup.cs?name=Echo)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](websockets/samples/1.x/WebSocketsSample/Startup.cs?name=Echo)]

::: moniker-end

<span data-ttu-id="a2147-160">如果在开始循环之前接受 WebSocket 连接，中间件管道会结束。</span><span class="sxs-lookup"><span data-stu-id="a2147-160">When accepting the WebSocket connection before beginning the loop, the middleware pipeline ends.</span></span> <span data-ttu-id="a2147-161">关闭套接字后，管道展开。</span><span class="sxs-lookup"><span data-stu-id="a2147-161">Upon closing the socket, the pipeline unwinds.</span></span> <span data-ttu-id="a2147-162">即接受 WebSocket 时，请求停止在管道中推进。</span><span class="sxs-lookup"><span data-stu-id="a2147-162">That is, the request stops moving forward in the pipeline when the WebSocket is accepted.</span></span> <span data-ttu-id="a2147-163">循环结束且套接字关闭时，请求继续回到管道。</span><span class="sxs-lookup"><span data-stu-id="a2147-163">When the loop is finished and the socket is closed, the request proceeds back up the pipeline.</span></span>

::: moniker range=">= aspnetcore-2.2"

### <a name="handle-client-disconnects"></a><span data-ttu-id="a2147-164">处理客户端连接断开</span><span class="sxs-lookup"><span data-stu-id="a2147-164">Handle client disconnects</span></span>

<span data-ttu-id="a2147-165">当客户端由于失去连接而断开连接时不会自动向服务器发送通知。</span><span class="sxs-lookup"><span data-stu-id="a2147-165">The server is not automatically informed when the client disconnects due to loss of connectivity.</span></span> <span data-ttu-id="a2147-166">服务器只有在客户端发送通知时才会收到断开连接消息，而此操作无法在失去 Internet 连接的情况下进行。</span><span class="sxs-lookup"><span data-stu-id="a2147-166">The server receives a disconnect message only if the client sends it, which can't be done if the internet connection is lost.</span></span> <span data-ttu-id="a2147-167">如果想要在发生此情况时采取某个操作，在特定时间范围内未收到来自客户端的任何消息后设置超时。</span><span class="sxs-lookup"><span data-stu-id="a2147-167">If you want to take some action when that happens, set a timeout after nothing is received from the client within a certain time window.</span></span>

<span data-ttu-id="a2147-168">如果客户端并非总是发送消息且不希望仅由于连接进入空闲状态就设置超时，则让客户端使用一个计时器并每隔 X 秒发送一条 ping 消息。</span><span class="sxs-lookup"><span data-stu-id="a2147-168">If the client isn't always sending messages and you don't want to timeout just because the connection goes idle, have the client use a timer to send a ping message every X seconds.</span></span> <span data-ttu-id="a2147-169">在服务器上，如果某条消息在上一条消息发出后的 2\*X 秒内尚未到达，则终止连接并报告客户端已断开连接。</span><span class="sxs-lookup"><span data-stu-id="a2147-169">On the server, if a message hasn't arrived within 2\*X seconds after the previous one, terminate the connection and report that the client disconnected.</span></span> <span data-ttu-id="a2147-170">等待两次预测的时间间隔，以便为可能延迟 ping 消息的网络延迟提供额外的时间。</span><span class="sxs-lookup"><span data-stu-id="a2147-170">Wait for twice the expected time interval to leave extra time for network delays that might hold up the ping message.</span></span>

### <a name="websocket-origin-restriction"></a><span data-ttu-id="a2147-171">WebSocket 源限制</span><span class="sxs-lookup"><span data-stu-id="a2147-171">WebSocket origin restriction</span></span>

<span data-ttu-id="a2147-172">CORS 提供的保护不适用于 WebSocket。</span><span class="sxs-lookup"><span data-stu-id="a2147-172">The protections provided by CORS don't apply to WebSockets.</span></span> <span data-ttu-id="a2147-173">浏览器不会：</span><span class="sxs-lookup"><span data-stu-id="a2147-173">Browsers do **not**:</span></span>

* <span data-ttu-id="a2147-174">执行 CORS 预检请求。</span><span class="sxs-lookup"><span data-stu-id="a2147-174">Perform CORS pre-flight requests.</span></span>
* <span data-ttu-id="a2147-175">在发出 WebSocket 请求时，遵守 `Access-Control` 标头中指定的限制。</span><span class="sxs-lookup"><span data-stu-id="a2147-175">Respect the restrictions specified in `Access-Control` headers when making WebSocket requests.</span></span>

<span data-ttu-id="a2147-176">但是，浏览器在发出 WebSocket 请求时会发送 `Origin` 标头。</span><span class="sxs-lookup"><span data-stu-id="a2147-176">However, browsers do send the `Origin` header when issuing WebSocket requests.</span></span> <span data-ttu-id="a2147-177">应将应用程序配置为验证这些标头，以确保只允许来自预期来源的 WebSocket。</span><span class="sxs-lookup"><span data-stu-id="a2147-177">Applications should be configured to validate these headers to ensure that only WebSockets coming from the expected origins are allowed.</span></span>

<span data-ttu-id="a2147-178">如果在“https://server.com”上托管服务器并在“https://client.com”上托管客户端，请将“https://client.com”添加到 `AllowedOrigins` 列表以验证 WebSocket。</span><span class="sxs-lookup"><span data-stu-id="a2147-178">If you're hosting your server on "https://server.com" and hosting your client on "https://client.com", add "https://client.com" to the `AllowedOrigins` list for WebSockets to verify.</span></span>

[!code-csharp[](websockets/samples/2.x/WebSocketsSample/Startup.cs?name=UseWebSocketsOptionsAO&highlight=6-7)]

> [!NOTE]
> <span data-ttu-id="a2147-179">与 `Referer` 标头一样，`Origin` 标头由客户端控制，并可以伪造。</span><span class="sxs-lookup"><span data-stu-id="a2147-179">The `Origin` header is controlled by the client and, like the `Referer` header, can be faked.</span></span> <span data-ttu-id="a2147-180">请勿将这些标头用作身份验证机制。</span><span class="sxs-lookup"><span data-stu-id="a2147-180">Do **not** use these headers as an authentication mechanism.</span></span>

::: moniker-end

## <a name="iisiis-express-support"></a><span data-ttu-id="a2147-181">IIS/IIS Express 支持</span><span class="sxs-lookup"><span data-stu-id="a2147-181">IIS/IIS Express support</span></span>

<span data-ttu-id="a2147-182">安装了 IIS/IIS Express 8 或更高版本的 Windows Server 2012 或更高版本以及 Windows 8 或更高版本支持 WebSocket 协议。</span><span class="sxs-lookup"><span data-stu-id="a2147-182">Windows Server 2012 or later and Windows 8 or later with IIS/IIS Express 8 or later has support for the WebSocket protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="a2147-183">使用 IIS Express 时始终启用 WebSocket。</span><span class="sxs-lookup"><span data-stu-id="a2147-183">WebSockets are always enabled when using IIS Express.</span></span>

### <a name="enabling-websockets-on-iis"></a><span data-ttu-id="a2147-184">在 IIS 上启用 Websocket</span><span class="sxs-lookup"><span data-stu-id="a2147-184">Enabling WebSockets on IIS</span></span>

<span data-ttu-id="a2147-185">在 Windows Server 2012 或更高版本上启用对 WebSocket 协议的支持：</span><span class="sxs-lookup"><span data-stu-id="a2147-185">To enable support for the WebSocket protocol on Windows Server 2012 or later:</span></span>

> [!NOTE]
> <span data-ttu-id="a2147-186">使用 IIS Express 时无需执行这些步骤</span><span class="sxs-lookup"><span data-stu-id="a2147-186">These steps are not required when using IIS Express</span></span>

1. <span data-ttu-id="a2147-187">通过“管理”菜单或“服务器管理器”中的链接使用“添加角色和功能”向导。</span><span class="sxs-lookup"><span data-stu-id="a2147-187">Use the **Add Roles and Features** wizard from the **Manage** menu or the link in **Server Manager**.</span></span>
1. <span data-ttu-id="a2147-188">选择“基于角色或基于功能的安装”。</span><span class="sxs-lookup"><span data-stu-id="a2147-188">Select **Role-based or Feature-based Installation**.</span></span> <span data-ttu-id="a2147-189">选择“下一步”。</span><span class="sxs-lookup"><span data-stu-id="a2147-189">Select **Next**.</span></span>
1. <span data-ttu-id="a2147-190">选择适当的服务器（默认情况下选择本地服务器）。</span><span class="sxs-lookup"><span data-stu-id="a2147-190">Select the appropriate server (the local server is selected by default).</span></span> <span data-ttu-id="a2147-191">选择“下一步”。</span><span class="sxs-lookup"><span data-stu-id="a2147-191">Select **Next**.</span></span>
1. <span data-ttu-id="a2147-192">在“角色”树中展开“Web 服务器 (IIS)”、然后依次展开“Web 服务器”和“应用程序开发”。</span><span class="sxs-lookup"><span data-stu-id="a2147-192">Expand **Web Server (IIS)** in the **Roles** tree, expand **Web Server**, and then expand **Application Development**.</span></span>
1. <span data-ttu-id="a2147-193">选择“WebSocket 协议”。</span><span class="sxs-lookup"><span data-stu-id="a2147-193">Select **WebSocket Protocol**.</span></span> <span data-ttu-id="a2147-194">选择“下一步”。</span><span class="sxs-lookup"><span data-stu-id="a2147-194">Select **Next**.</span></span>
1. <span data-ttu-id="a2147-195">如果无需其他功能，请选择“下一步”。</span><span class="sxs-lookup"><span data-stu-id="a2147-195">If additional features aren't needed, select **Next**.</span></span>
1. <span data-ttu-id="a2147-196">选择“安装” 。</span><span class="sxs-lookup"><span data-stu-id="a2147-196">Select **Install**.</span></span>
1. <span data-ttu-id="a2147-197">安装完成后，选择“关闭”以退出向导。</span><span class="sxs-lookup"><span data-stu-id="a2147-197">When the installation completes, select **Close** to exit the wizard.</span></span>

<span data-ttu-id="a2147-198">在 Windows 8 或更高版本上启用对 WebSocket 协议的支持：</span><span class="sxs-lookup"><span data-stu-id="a2147-198">To enable support for the WebSocket protocol on Windows 8 or later:</span></span>

> [!NOTE]
> <span data-ttu-id="a2147-199">使用 IIS Express 时无需执行这些步骤</span><span class="sxs-lookup"><span data-stu-id="a2147-199">These steps are not required when using IIS Express</span></span>

1. <span data-ttu-id="a2147-200">导航到“控制面板” > “程序” > “程序和功能” > “打开或关闭 Windows 功能”（位于屏幕左侧）。</span><span class="sxs-lookup"><span data-stu-id="a2147-200">Navigate to **Control Panel** > **Programs** > **Programs and Features** > **Turn Windows features on or off** (left side of the screen).</span></span>
1. <span data-ttu-id="a2147-201">打开以下节点：“Internet Information Services” > “万维网服务” > “应用程序开发功能”。</span><span class="sxs-lookup"><span data-stu-id="a2147-201">Open the following nodes: **Internet Information Services** > **World Wide Web Services** > **Application Development Features**.</span></span>
1. <span data-ttu-id="a2147-202">选择“WebSocket 协议”功能。</span><span class="sxs-lookup"><span data-stu-id="a2147-202">Select the **WebSocket Protocol** feature.</span></span> <span data-ttu-id="a2147-203">选择 **确定**。</span><span class="sxs-lookup"><span data-stu-id="a2147-203">Select **OK**.</span></span>

### <a name="disable-websocket-when-using-socketio-on-nodejs"></a><span data-ttu-id="a2147-204">在 Node.js 上使用 socket.io 时禁用 WebSocket</span><span class="sxs-lookup"><span data-stu-id="a2147-204">Disable WebSocket when using socket.io on Node.js</span></span>

<span data-ttu-id="a2147-205">如果在 [Node.js](https://nodejs.org/) 的 [socket.io](https://socket.io/) 中使用 WebSocket 支持，请使用 web.config 或 applicationHost.config 中的 `webSocket` 元素禁用默认的 IIS WebSocket 模块。如果不执行此步骤，IIS WebSocket 模块将尝试处理 WebSocket 通信而不是 Node.js 和应用。</span><span class="sxs-lookup"><span data-stu-id="a2147-205">If using the WebSocket support in [socket.io](https://socket.io/) on [Node.js](https://nodejs.org/), disable the default IIS WebSocket module using the `webSocket` element in *web.config* or *applicationHost.config*. If this step isn't performed, the IIS WebSocket module attempts to handle the WebSocket communication rather than Node.js and the app.</span></span>

```xml
<system.webServer>
  <webSocket enabled="false" />
</system.webServer>
```

## <a name="next-steps"></a><span data-ttu-id="a2147-206">后续步骤</span><span class="sxs-lookup"><span data-stu-id="a2147-206">Next steps</span></span>

<span data-ttu-id="a2147-207">本文附带的[示例应用](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/websockets/samples)是一个 echo 应用。</span><span class="sxs-lookup"><span data-stu-id="a2147-207">The [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/websockets/samples) that accompanies this article is an echo app.</span></span> <span data-ttu-id="a2147-208">它有一个可建立 WebSocket 连接的网页，且服务器将其收到的消息重新发回到客户端。</span><span class="sxs-lookup"><span data-stu-id="a2147-208">It has a web page that makes WebSocket connections, and the server resends any messages it receives back to the client.</span></span> <span data-ttu-id="a2147-209">从命令提示符运行该应用（它未设置为在安装了 IIS Express 的 Visual Studio 中运行）并导航到 http://localhost:5000。</span><span class="sxs-lookup"><span data-stu-id="a2147-209">Run the app from a command prompt (it's not set up to run from Visual Studio with IIS Express) and navigate to http://localhost:5000.</span></span> <span data-ttu-id="a2147-210">该网页的左上方显示连接状态：</span><span class="sxs-lookup"><span data-stu-id="a2147-210">The web page shows the connection status in the upper left:</span></span>

![网页的初始状态](websockets/_static/start.png)

<span data-ttu-id="a2147-212">选择“连接”，向显示的 URL 发送 WebSocket 请求。</span><span class="sxs-lookup"><span data-stu-id="a2147-212">Select **Connect** to send a WebSocket request to the URL shown.</span></span> <span data-ttu-id="a2147-213">输入测试消息并选择“发送”。</span><span class="sxs-lookup"><span data-stu-id="a2147-213">Enter a test message and select **Send**.</span></span> <span data-ttu-id="a2147-214">完成后，请选择“关闭套接字”。</span><span class="sxs-lookup"><span data-stu-id="a2147-214">When done, select **Close Socket**.</span></span> <span data-ttu-id="a2147-215">“通信日志”部分会报告每一个发生的“打开”、“发送”和“关闭”操作。</span><span class="sxs-lookup"><span data-stu-id="a2147-215">The **Communication Log** section reports each open, send, and close action as it happens.</span></span>

![网页的初始状态](websockets/_static/end.png)

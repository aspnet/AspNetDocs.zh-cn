---
uid: signalr/overview/performance/signalr-performance
title: 信号器性能 |微软文档
author: bradygaster
description: SignalR 性能
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 3751f5e7-59db-4be0-a290-50abc24e5c84
msc.legacyurl: /signalr/overview/performance/signalr-performance
msc.type: authoredcontent
ms.openlocfilehash: b8a44f4c924c94cdfff1ce7630539b45fe269bbf
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675717"
---
# <a name="signalr-performance"></a><span data-ttu-id="5d650-103">SignalR 性能</span><span class="sxs-lookup"><span data-stu-id="5d650-103">SignalR Performance</span></span>

<span data-ttu-id="5d650-104">由[帕特里克·弗莱彻](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="5d650-104">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="5d650-105">本主题介绍如何为 SignalR 应用程序中的设计、测量和改进性能。</span><span class="sxs-lookup"><span data-stu-id="5d650-105">This topic describes how to design for, measure, and improve performance in a SignalR application.</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="5d650-106">本主题中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="5d650-106">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="5d650-107">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="5d650-107">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="5d650-108">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="5d650-108">.NET 4.5</span></span>
> - <span data-ttu-id="5d650-109">信号R版本 2</span><span class="sxs-lookup"><span data-stu-id="5d650-109">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="5d650-110">本主题的早期版本</span><span class="sxs-lookup"><span data-stu-id="5d650-110">Previous versions of this topic</span></span>
>
> <span data-ttu-id="5d650-111">有关早期版本的 SignalR 的信息，请参阅[SignalR 旧版本](../older-versions/index.md)。</span><span class="sxs-lookup"><span data-stu-id="5d650-111">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="5d650-112">问题和评论</span><span class="sxs-lookup"><span data-stu-id="5d650-112">Questions and comments</span></span>
>
> <span data-ttu-id="5d650-113">请留下反馈，关于你喜欢本教程的方式，以及我们可以在页面底部的评论中改进什么。</span><span class="sxs-lookup"><span data-stu-id="5d650-113">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="5d650-114">如果您有与本教程没有直接关系的问题，您可以将它们发布到[ASP.NET SignalR 论坛](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com/)。</span><span class="sxs-lookup"><span data-stu-id="5d650-114">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

<span data-ttu-id="5d650-115">有关 SignalR 性能和缩放的最新演示文稿，请参阅[使用ASP.NET信号R 缩放实时 Web。](https://channel9.msdn.com/Events/Build/2013/3-502)</span><span class="sxs-lookup"><span data-stu-id="5d650-115">For a recent presentation on SignalR performance and scaling, see [Scaling the Real-time Web with ASP.NET SignalR](https://channel9.msdn.com/Events/Build/2013/3-502).</span></span>

<span data-ttu-id="5d650-116">本主题包含以下各节：</span><span class="sxs-lookup"><span data-stu-id="5d650-116">This topic contains the following sections:</span></span>

- [<span data-ttu-id="5d650-117">设计注意事项</span><span class="sxs-lookup"><span data-stu-id="5d650-117">Design considerations</span></span>](#design)
- [<span data-ttu-id="5d650-118">调整 SignalR 服务器的性能</span><span class="sxs-lookup"><span data-stu-id="5d650-118">Tuning your SignalR server for performance</span></span>](#tuning)
- [<span data-ttu-id="5d650-119">性能问题故障排除</span><span class="sxs-lookup"><span data-stu-id="5d650-119">Troubleshooting performance issues</span></span>](#troubleshooting)
- [<span data-ttu-id="5d650-120">使用信号R性能计数器</span><span class="sxs-lookup"><span data-stu-id="5d650-120">Using SignalR performance counters</span></span>](#perfcounters)
- [<span data-ttu-id="5d650-121">使用其他性能计数器</span><span class="sxs-lookup"><span data-stu-id="5d650-121">Using other performance counters</span></span>](#othercounters)
- [<span data-ttu-id="5d650-122">其他资源</span><span class="sxs-lookup"><span data-stu-id="5d650-122">Other resources</span></span>](#otherresources)

<a id="design"></a>

## <a name="design-considerations"></a><span data-ttu-id="5d650-123">设计注意事项</span><span class="sxs-lookup"><span data-stu-id="5d650-123">Design considerations</span></span>

<span data-ttu-id="5d650-124">本节介绍在设计 SignalR 应用程序期间可以实现的模式，以确保不会因生成不必要的网络流量而妨碍性能。</span><span class="sxs-lookup"><span data-stu-id="5d650-124">This section describes patterns that can be implemented during the design of a SignalR application, to ensure that performance is not being hindered by generating unnecessary network traffic.</span></span>

### <a name="throttling-message-frequency"></a><span data-ttu-id="5d650-125">限制消息频率</span><span class="sxs-lookup"><span data-stu-id="5d650-125">Throttling message frequency</span></span>

<span data-ttu-id="5d650-126">即使在以高频率发送消息的应用程序（如实时游戏应用程序）中，大多数应用程序也不需要每秒发送多条消息。</span><span class="sxs-lookup"><span data-stu-id="5d650-126">Even in an application that sends out messages at a high frequency (such as a realtime gaming application), most applications don't need to send more than a few messages a second.</span></span> <span data-ttu-id="5d650-127">为了减少每个客户端生成的流量，可以实现一个消息循环，该队列和发送消息的频率不会超过固定速率（也就是说，如果该时间间隔内有要发送的消息，每秒最多发送一定数量的消息）。</span><span class="sxs-lookup"><span data-stu-id="5d650-127">To reduce the amount of traffic that each client generates, a message loop can be implemented that queues and sends out messages no more frequently than a fixed rate (that is, up to a certain number of messages will be sent every second, if there are messages in that time interval to be sent).</span></span> <span data-ttu-id="5d650-128">有关将消息限制到特定速率（来自客户端和服务器）的示例应用程序，请参阅[使用 SignalR 的高频实时](../getting-started/tutorial-high-frequency-realtime-with-signalr.md)。</span><span class="sxs-lookup"><span data-stu-id="5d650-128">For a sample application that throttles messages to a certain rate (from both client and server), see [High-Frequency Realtime with SignalR](../getting-started/tutorial-high-frequency-realtime-with-signalr.md).</span></span>

### <a name="reducing-message-size"></a><span data-ttu-id="5d650-129">减小消息大小</span><span class="sxs-lookup"><span data-stu-id="5d650-129">Reducing message size</span></span>

<span data-ttu-id="5d650-130">您可以通过减小序列化对象的大小来减小 SignalR 消息的大小。</span><span class="sxs-lookup"><span data-stu-id="5d650-130">You can reduce the size of a SignalR message by reducing the size of your serialized objects.</span></span> <span data-ttu-id="5d650-131">在服务器代码中，如果发送的对象包含不需要传输的属性，则防止使用 属性`JsonIgnore`序列化这些属性。</span><span class="sxs-lookup"><span data-stu-id="5d650-131">In server code, if you're sending an object that contains properties that don't need to be transmitted, prevent those properties from being serialized by using the `JsonIgnore` attribute.</span></span> <span data-ttu-id="5d650-132">属性的名称也存储在消息中;可以使用 属性缩短`JsonProperty`属性的名称。</span><span class="sxs-lookup"><span data-stu-id="5d650-132">The names of properties are also stored in the message; the names of properties can be shortened using the `JsonProperty` attribute.</span></span> <span data-ttu-id="5d650-133">以下代码示例演示如何排除属性发送到客户端，以及如何缩短属性名称：</span><span class="sxs-lookup"><span data-stu-id="5d650-133">The following code sample demonstrates how to exclude a property from being sent to the client, and how to shorten property names:</span></span>

<span data-ttu-id="5d650-134">**.NET 服务器代码，用于演示 JsonIgnore 属性，以排除发送到客户端的数据，以及用于减小消息大小的 JsonProperty 属性**</span><span class="sxs-lookup"><span data-stu-id="5d650-134">**.NET server code that demonstrates the JsonIgnore attribute to exclude data from being sent to the client, and the JsonProperty attribute to reduce message size**</span></span>

[!code-csharp[Main](signalr-performance/samples/sample1.cs?highlight=5,7,10)]

<span data-ttu-id="5d650-135">为了在客户端代码中保持可读性/可维护性，在收到消息后，可以将缩写属性名称重新映射到人友好名称。</span><span class="sxs-lookup"><span data-stu-id="5d650-135">In order to retain readability/ maintainability in the client code, the abbreviated property names can be remapped to human-friendly names after the message is received.</span></span> <span data-ttu-id="5d650-136">以下代码示例演示了一种通过将缩短的名称重新映射到较长的名称的方法，方法是定义消息协定（映射），并使用 函数`reMap`将协定应用于优化的消息类：</span><span class="sxs-lookup"><span data-stu-id="5d650-136">The following code sample demonstrates one possible way of remapping shortened names to longer ones, by defining a message contract (mapping), and using the `reMap` function to apply the contract to the optimized message class:</span></span>

<span data-ttu-id="5d650-137">**客户端 JavaScript 代码将缩短的属性名称重新映射到人可读名称**</span><span class="sxs-lookup"><span data-stu-id="5d650-137">**Client-side JavaScript code that remaps shortened property names to human-readable names**</span></span>

[!code-javascript[Main](signalr-performance/samples/sample2.js)]

<span data-ttu-id="5d650-138">名称也可以使用相同的方法在从客户端到服务器的电子邮件中缩短。</span><span class="sxs-lookup"><span data-stu-id="5d650-138">Names can be shortened in messages from the client to the server as well, using the same method.</span></span>

<span data-ttu-id="5d650-139">减少消息对象的内存占用空间（即用于消息的内存量）也可以提高性能。</span><span class="sxs-lookup"><span data-stu-id="5d650-139">Reducing the memory footprint (that is, the amount of memory used for the message) of the message object can also improve performance.</span></span> <span data-ttu-id="5d650-140">例如，如果不需要全部范围的 ，`int`则可以改用 或`short``byte`。</span><span class="sxs-lookup"><span data-stu-id="5d650-140">For example, if the full range of an `int` is not needed, a `short` or `byte` can be used instead.</span></span>

<span data-ttu-id="5d650-141">由于邮件存储在服务器内存中的消息总线中，因此减小消息大小还可以解决服务器内存问题。</span><span class="sxs-lookup"><span data-stu-id="5d650-141">Since messages are stored in the message bus in server memory, reducing the size of messages can also address server memory issues.</span></span>

<a id="tuning"></a>

### <a name="tuning-your-signalr-server-for-performance"></a><span data-ttu-id="5d650-142">调整 SignalR 服务器的性能</span><span class="sxs-lookup"><span data-stu-id="5d650-142">Tuning your SignalR server for performance</span></span>

<span data-ttu-id="5d650-143">以下配置设置可用于调整服务器，以便在 SignalR 应用程序中获得更好的性能。</span><span class="sxs-lookup"><span data-stu-id="5d650-143">The following configuration settings can be used to tune your server for better performance in a SignalR application.</span></span> <span data-ttu-id="5d650-144">有关如何提高ASP.NET应用程序中性能的一般信息，请参阅[改进ASP.NET性能](https://msdn.microsoft.com/library/ff647787.aspx)。</span><span class="sxs-lookup"><span data-stu-id="5d650-144">For general information on how to improve performance in an ASP.NET application, see [Improving ASP.NET Performance](https://msdn.microsoft.com/library/ff647787.aspx).</span></span>

<span data-ttu-id="5d650-145">**信号R配置设置**</span><span class="sxs-lookup"><span data-stu-id="5d650-145">**SignalR configuration settings**</span></span>

- <span data-ttu-id="5d650-146">**默认消息缓冲区大小**：默认情况下，SignalR 每个连接的内存中保留 1000 条消息。</span><span class="sxs-lookup"><span data-stu-id="5d650-146">**DefaultMessageBufferSize**: By default, SignalR retains 1000 messages in memory per hub per connection.</span></span> <span data-ttu-id="5d650-147">如果使用大型消息，则可能会产生内存问题，通过减小此值来缓解这些问题。</span><span class="sxs-lookup"><span data-stu-id="5d650-147">If large messages are being used, this may create memory issues which can be alleviated by reducing this value.</span></span> <span data-ttu-id="5d650-148">此设置可以在ASP.NET应用程序中`Application_Start`的事件处理程序中设置，也可以在自托管应用程序中的 OWIN 启动类`Configuration`方法中设置。</span><span class="sxs-lookup"><span data-stu-id="5d650-148">This setting can be set in the `Application_Start` event handler in an ASP.NET application, or in the `Configuration` method of an OWIN startup class in a self-hosted application.</span></span> <span data-ttu-id="5d650-149">以下示例演示如何减小此值以减少应用程序的内存占用量，以减少使用的服务器内存量：</span><span class="sxs-lookup"><span data-stu-id="5d650-149">The following sample demonstrates how to reduce this value in order to reduce the memory footprint of your application in order to reduce the amount of server memory used:</span></span>

    <span data-ttu-id="5d650-150">**Startup.cs 中的 .NET 服务器代码，用于减小默认邮件缓冲区大小**</span><span class="sxs-lookup"><span data-stu-id="5d650-150">**.NET server code in Startup.cs for decreasing default message buffer size**</span></span>

    [!code-csharp[Main](signalr-performance/samples/sample3.cs)]

<span data-ttu-id="5d650-151">**IIS 配置设置**</span><span class="sxs-lookup"><span data-stu-id="5d650-151">**IIS configuration settings**</span></span>

- <span data-ttu-id="5d650-152">**每个应用程序的最多并发请求**：增加并发 IIS 请求的数量将增加可用于服务请求的服务器资源。</span><span class="sxs-lookup"><span data-stu-id="5d650-152">**Max concurrent requests per application**: Increasing the number of concurrent IIS requests will increase server resources available for serving requests.</span></span> <span data-ttu-id="5d650-153">默认值为 5000;要增加此设置，请在提升的命令提示符中执行以下命令：</span><span class="sxs-lookup"><span data-stu-id="5d650-153">The default value is 5000; to increase this setting, execute the following commands in an elevated command prompt:</span></span>

    [!code-console[Main](signalr-performance/samples/sample4.cmd)]
- <span data-ttu-id="5d650-154">**应用程序池队列长度**：这是 Http.sys 为应用程序池排队的最大请求数。</span><span class="sxs-lookup"><span data-stu-id="5d650-154">**ApplicationPool QueueLength**: This is the maximum number of requests that Http.sys queues for the application pool.</span></span> <span data-ttu-id="5d650-155">队列已满时，新请求将收到 503"服务不可用"响应。</span><span class="sxs-lookup"><span data-stu-id="5d650-155">When the queue is full, new requests receive a 503 "Service Unavailable" response.</span></span> <span data-ttu-id="5d650-156">默认值为 1000。</span><span class="sxs-lookup"><span data-stu-id="5d650-156">The default value is 1000.</span></span>

    <span data-ttu-id="5d650-157">缩短应用程序托管的应用程序池中工作进程的队列长度将节省内存资源。</span><span class="sxs-lookup"><span data-stu-id="5d650-157">Shortening the queue length for the worker process in the application pool hosting your application will conserve memory resources.</span></span> <span data-ttu-id="5d650-158">有关详细信息，请参阅[管理、调整和配置应用程序池](https://technet.microsoft.com/library/cc745955.aspx)。</span><span class="sxs-lookup"><span data-stu-id="5d650-158">For more information, see [Managing, Tuning, and Configuring Application Pools](https://technet.microsoft.com/library/cc745955.aspx).</span></span>

<span data-ttu-id="5d650-159">**ASP.NET配置设置**</span><span class="sxs-lookup"><span data-stu-id="5d650-159">**ASP.NET configuration settings**</span></span>

<span data-ttu-id="5d650-160">本节包括可在文件中设置的`aspnet.config`配置设置。</span><span class="sxs-lookup"><span data-stu-id="5d650-160">This section includes configuration settings that can be set in the `aspnet.config` file.</span></span> <span data-ttu-id="5d650-161">此文件位于两个位置之一，具体取决于平台：</span><span class="sxs-lookup"><span data-stu-id="5d650-161">This file is found in one of two locations, depending on platform:</span></span>

- `%windir%\Microsoft.NET\Framework\v4.0.30319\aspnet.config`
- `%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet.config`

<span data-ttu-id="5d650-162">可能提高 SignalR 性能ASP.NET设置包括：</span><span class="sxs-lookup"><span data-stu-id="5d650-162">ASP.NET settings that may improve SignalR performance include the following:</span></span>

- <span data-ttu-id="5d650-163">**每个 CPU 的最大并发请求**：增加此设置可能会缓解性能瓶颈。</span><span class="sxs-lookup"><span data-stu-id="5d650-163">**Maximum concurrent requests per CPU**: Increasing this setting may alleviate performance bottlenecks.</span></span> <span data-ttu-id="5d650-164">要增加此设置，向`aspnet.config`文件添加以下配置设置：</span><span class="sxs-lookup"><span data-stu-id="5d650-164">To increase this setting, add the following configuration setting to the `aspnet.config` file:</span></span>

    [!code-xml[Main](signalr-performance/samples/sample5.xml?highlight=4)]
- <span data-ttu-id="5d650-165">**请求队列限制**：当连接总数超过`maxConcurrentRequestsPerCPU`设置时，ASP.NET将使用队列开始限制请求。</span><span class="sxs-lookup"><span data-stu-id="5d650-165">**Request Queue Limit**: When the total number of connections exceeds the `maxConcurrentRequestsPerCPU` setting, ASP.NET will start throttling requests using a queue.</span></span> <span data-ttu-id="5d650-166">要增加队列的大小，可以增加`requestQueueLimit`设置。</span><span class="sxs-lookup"><span data-stu-id="5d650-166">To increase the size of the queue, you can increase the `requestQueueLimit` setting.</span></span> <span data-ttu-id="5d650-167">为此，向 中的`processModel``config/machine.config`节点添加以下配置设置（而不是`aspnet.config`）：</span><span class="sxs-lookup"><span data-stu-id="5d650-167">To do this, add the following configuration setting to the `processModel` node in `config/machine.config` (rather than `aspnet.config`):</span></span>

    [!code-xml[Main](signalr-performance/samples/sample6.xml)]

<a id="troubleshooting"></a>

## <a name="troubleshooting-performance-issues"></a><span data-ttu-id="5d650-168">性能问题故障排除</span><span class="sxs-lookup"><span data-stu-id="5d650-168">Troubleshooting performance issues</span></span>

<span data-ttu-id="5d650-169">本节介绍查找应用程序中的性能瓶颈的方法。</span><span class="sxs-lookup"><span data-stu-id="5d650-169">This section describes ways to find performance bottlenecks in your application.</span></span>

### <a name="verifying-that-websocket-is-being-used"></a><span data-ttu-id="5d650-170">验证是否正在使用 WebSocket</span><span class="sxs-lookup"><span data-stu-id="5d650-170">Verifying that WebSocket is being used</span></span>

<span data-ttu-id="5d650-171">虽然 SignalR 可以使用各种传输在客户端和服务器之间通信，但 WebSocket 具有显著的性能优势，如果客户端和服务器支持它，则应使用它。</span><span class="sxs-lookup"><span data-stu-id="5d650-171">While SignalR can use a variety of transports for communication between client and server, WebSocket offers a significant performance advantage, and should be used if the client and server support it.</span></span> <span data-ttu-id="5d650-172">要确定客户端和服务器是否满足 WebSocket 的要求，请参阅[传输和回退](../getting-started/introduction-to-signalr.md#transports)。</span><span class="sxs-lookup"><span data-stu-id="5d650-172">To determine if your client and server meet the requirements for WebSocket, see [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span> <span data-ttu-id="5d650-173">要确定应用程序中正在使用哪些传输，可以使用浏览器开发人员工具，并检查日志以查看用于连接的传输。</span><span class="sxs-lookup"><span data-stu-id="5d650-173">To determine what transport is being used in your application, you can use the browser developer tools, and examine the logs to see what transport is being used for the connection.</span></span> <span data-ttu-id="5d650-174">有关在 Internet 资源管理器和 Chrome 中使用浏览器开发工具的信息，请参阅[传输和回退](../getting-started/introduction-to-signalr.md#transports)。</span><span class="sxs-lookup"><span data-stu-id="5d650-174">For information on using the browser development tools in Internet Explorer and Chrome, see [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span>

<a id="perfcounters"></a>

## <a name="using-signalr-performance-counters"></a><span data-ttu-id="5d650-175">使用信号R性能计数器</span><span class="sxs-lookup"><span data-stu-id="5d650-175">Using SignalR performance counters</span></span>

<span data-ttu-id="5d650-176">本节介绍如何在`Microsoft.AspNet.SignalR.Utils`封装中找到的启用和使用 SignalR 性能计数器。</span><span class="sxs-lookup"><span data-stu-id="5d650-176">This section describes how to enable and use SignalR performance counters, found in the `Microsoft.AspNet.SignalR.Utils` package.</span></span>

### <a name="installing-signalrexe"></a><span data-ttu-id="5d650-177">安装信号器.exe</span><span class="sxs-lookup"><span data-stu-id="5d650-177">Installing signalr.exe</span></span>

<span data-ttu-id="5d650-178">可以使用称为 SignalR.exe 的实用程序将性能计数器添加到服务器。</span><span class="sxs-lookup"><span data-stu-id="5d650-178">Performance counters can be added to the server using a utility called SignalR.exe.</span></span> <span data-ttu-id="5d650-179">要安装此实用程序，请按照以下步骤操作：</span><span class="sxs-lookup"><span data-stu-id="5d650-179">To install this utility, follow these steps:</span></span>

1. <span data-ttu-id="5d650-180">在可视化工作室中，选择**工具** > **NuGet 包管理器** > **管理 NuGet 包以进行解决方案**</span><span class="sxs-lookup"><span data-stu-id="5d650-180">In Visual Studio, select **Tools** > **NuGet Package Manager** > **Manage NuGet Packages for Solution**</span></span>
2. <span data-ttu-id="5d650-181">搜索**信号器.utils，** 然后选择"安装"。</span><span class="sxs-lookup"><span data-stu-id="5d650-181">Search for **signalr.utils**, and select Install.</span></span>

    ![](signalr-performance/_static/image1.png)
3. <span data-ttu-id="5d650-182">接受安装包的许可协议。</span><span class="sxs-lookup"><span data-stu-id="5d650-182">Accept the license agreement to install the package.</span></span>
4. <span data-ttu-id="5d650-183">SignalR.exe 将安装到`<project folder>/packages/Microsoft.AspNet.SignalR.Utils.<version>/tools`。</span><span class="sxs-lookup"><span data-stu-id="5d650-183">SignalR.exe will be installed to `<project folder>/packages/Microsoft.AspNet.SignalR.Utils.<version>/tools`.</span></span>

### <a name="installing-performance-counters-with-signalrexe"></a><span data-ttu-id="5d650-184">使用 SignalR.exe 安装性能计数器</span><span class="sxs-lookup"><span data-stu-id="5d650-184">Installing performance counters with SignalR.exe</span></span>

<span data-ttu-id="5d650-185">要安装 SignalR 性能计数器，请使用以下参数在提升的命令提示符中运行 SignalR.exe：</span><span class="sxs-lookup"><span data-stu-id="5d650-185">To install SignalR performance counters, run SignalR.exe in an elevated command prompt with the following parameter:</span></span>

[!code-console[Main](signalr-performance/samples/sample7.cmd)]

<span data-ttu-id="5d650-186">要删除 SignalR 性能计数器，请使用以下参数在提升的命令提示符中运行 SignalR.exe：</span><span class="sxs-lookup"><span data-stu-id="5d650-186">To remove SignalR performance counters, run SignalR.exe in an elevated command prompt with the following parameter:</span></span>

[!code-console[Main](signalr-performance/samples/sample8.cmd)]

### <a name="signalr-performance-counters"></a><span data-ttu-id="5d650-187">信号R性能计数器</span><span class="sxs-lookup"><span data-stu-id="5d650-187">SignalR Performance counters</span></span>

<span data-ttu-id="5d650-188">实用程序包安装以下性能计数器。</span><span class="sxs-lookup"><span data-stu-id="5d650-188">The utilities package installs the following performance counters.</span></span> <span data-ttu-id="5d650-189">"总计"计数器测量自上次应用程序池或服务器重新启动以来的事件数。</span><span class="sxs-lookup"><span data-stu-id="5d650-189">The "Total" counters measure the number of events since the last application pool or server restart.</span></span>

<span data-ttu-id="5d650-190">**连接指标**</span><span class="sxs-lookup"><span data-stu-id="5d650-190">**Connection metrics**</span></span>

<span data-ttu-id="5d650-191">以下指标衡量发生的连接生存期事件。</span><span class="sxs-lookup"><span data-stu-id="5d650-191">The following metrics measure the connection lifetime events that occur.</span></span> <span data-ttu-id="5d650-192">有关详细信息，请参阅[了解和处理连接生存期事件](../guide-to-the-api/handling-connection-lifetime-events.md)。</span><span class="sxs-lookup"><span data-stu-id="5d650-192">For more information, see [Understanding and Handling Connection Lifetime Events](../guide-to-the-api/handling-connection-lifetime-events.md).</span></span>

- <span data-ttu-id="5d650-193">**连接已连接**</span><span class="sxs-lookup"><span data-stu-id="5d650-193">**Connections Connected**</span></span>
- <span data-ttu-id="5d650-194">**连接重新连接**</span><span class="sxs-lookup"><span data-stu-id="5d650-194">**Connections Reconnected**</span></span>
- <span data-ttu-id="5d650-195">**连接已断开连接**</span><span class="sxs-lookup"><span data-stu-id="5d650-195">**Connections Disconnected**</span></span>
- <span data-ttu-id="5d650-196">**连接电流**</span><span class="sxs-lookup"><span data-stu-id="5d650-196">**Connections Current**</span></span>

<span data-ttu-id="5d650-197">**消息指标**</span><span class="sxs-lookup"><span data-stu-id="5d650-197">**Message metrics**</span></span>

<span data-ttu-id="5d650-198">以下指标测量 SignalR 生成的消息流量。</span><span class="sxs-lookup"><span data-stu-id="5d650-198">The following metrics measure the message traffic generated by SignalR.</span></span>

- <span data-ttu-id="5d650-199">**接收的连接消息总数**</span><span class="sxs-lookup"><span data-stu-id="5d650-199">**Connection Messages Received Total**</span></span>
- <span data-ttu-id="5d650-200">**连接消息发送总数**</span><span class="sxs-lookup"><span data-stu-id="5d650-200">**Connection Messages Sent Total**</span></span>
- <span data-ttu-id="5d650-201">**已接收/秒的连接消息**</span><span class="sxs-lookup"><span data-stu-id="5d650-201">**Connection Messages Received/Sec**</span></span>
- <span data-ttu-id="5d650-202">**已发送/秒的连接消息**</span><span class="sxs-lookup"><span data-stu-id="5d650-202">**Connection Messages Sent/Sec**</span></span>

<span data-ttu-id="5d650-203">**消息总线指标**</span><span class="sxs-lookup"><span data-stu-id="5d650-203">**Message bus metrics**</span></span>

<span data-ttu-id="5d650-204">以下指标测量通过内部 SignalR 消息总线（放置所有传入和传出 SignalR 消息的队列）的流量。</span><span class="sxs-lookup"><span data-stu-id="5d650-204">The following metrics measure traffic through the internal SignalR message bus, the queue in which all incoming and outgoing SignalR messages are placed.</span></span> <span data-ttu-id="5d650-205">消息在发送或广播时**已发布**。</span><span class="sxs-lookup"><span data-stu-id="5d650-205">A message is **Published** when it is sent or broadcast.</span></span> <span data-ttu-id="5d650-206">此上下文中的**订阅服务器**是消息总线上的订阅;这应该等于客户端数加上服务器本身。</span><span class="sxs-lookup"><span data-stu-id="5d650-206">A **Subscriber** in this context is a subscription on the message bus; this should equal the number of clients plus the server itself.</span></span> <span data-ttu-id="5d650-207">**已分配的工作线程**是将数据发送到活动连接的组件;**忙工作人员**是主动发送消息的工作人员。</span><span class="sxs-lookup"><span data-stu-id="5d650-207">An **Allocated Worker** is a component that sends data to active connections; a **Busy Worker** is one that is actively sending a message.</span></span>

- <span data-ttu-id="5d650-208">**收到的消息总线消息总计**</span><span class="sxs-lookup"><span data-stu-id="5d650-208">**Message Bus Messages Received Total**</span></span>
- <span data-ttu-id="5d650-209">**收到/秒的消息总线消息**</span><span class="sxs-lookup"><span data-stu-id="5d650-209">**Message Bus Messages Received/Sec**</span></span>
- <span data-ttu-id="5d650-210">**消息总线消息已发布总计**</span><span class="sxs-lookup"><span data-stu-id="5d650-210">**Message Bus Messages Published Total**</span></span>
- <span data-ttu-id="5d650-211">**已发布/秒的消息总线消息**</span><span class="sxs-lookup"><span data-stu-id="5d650-211">**Message Bus Messages Published/Sec**</span></span>
- <span data-ttu-id="5d650-212">**消息总线订阅服务器当前**</span><span class="sxs-lookup"><span data-stu-id="5d650-212">**Message Bus Subscribers Current**</span></span>
- <span data-ttu-id="5d650-213">**消息总线订阅者总计**</span><span class="sxs-lookup"><span data-stu-id="5d650-213">**Message Bus Subscribers Total**</span></span>
- <span data-ttu-id="5d650-214">**消息总线订阅者/秒**</span><span class="sxs-lookup"><span data-stu-id="5d650-214">**Message Bus Subscribers/Sec**</span></span>
- <span data-ttu-id="5d650-215">**消息总线分配工作**</span><span class="sxs-lookup"><span data-stu-id="5d650-215">**Message Bus Allocated Workers**</span></span>
- <span data-ttu-id="5d650-216">**消息总线忙工作人员**</span><span class="sxs-lookup"><span data-stu-id="5d650-216">**Message Bus Busy Workers**</span></span>
- <span data-ttu-id="5d650-217">**邮件总线主题当前**</span><span class="sxs-lookup"><span data-stu-id="5d650-217">**Message Bus Topics Current**</span></span>

<span data-ttu-id="5d650-218">**错误指标**</span><span class="sxs-lookup"><span data-stu-id="5d650-218">**Error metrics**</span></span>

<span data-ttu-id="5d650-219">以下指标测量由 SignalR 消息流量生成的错误。</span><span class="sxs-lookup"><span data-stu-id="5d650-219">The following metrics measure errors generated by SignalR message traffic.</span></span> <span data-ttu-id="5d650-220">当无法解析中心或中心方法时，就会发生**中心解析**错误。</span><span class="sxs-lookup"><span data-stu-id="5d650-220">**Hub Resolution** errors occur when a hub or hub method cannot be resolved.</span></span> <span data-ttu-id="5d650-221">**中心调用**错误是在调用集线器方法时引发的异常。</span><span class="sxs-lookup"><span data-stu-id="5d650-221">**Hub Invocation** errors are exceptions thrown while invoking a hub method.</span></span> <span data-ttu-id="5d650-222">**传输**错误是在 HTTP 请求或响应期间引发的连接错误。</span><span class="sxs-lookup"><span data-stu-id="5d650-222">**Transport** errors are connection errors thrown during an HTTP request or response.</span></span>

- <span data-ttu-id="5d650-223">**错误：全部总计**</span><span class="sxs-lookup"><span data-stu-id="5d650-223">**Errors: All Total**</span></span>
- <span data-ttu-id="5d650-224">**错误：全部/秒**</span><span class="sxs-lookup"><span data-stu-id="5d650-224">**Errors: All/Sec**</span></span>
- <span data-ttu-id="5d650-225">**错误：中心分辨率总计**</span><span class="sxs-lookup"><span data-stu-id="5d650-225">**Errors: Hub Resolution Total**</span></span>
- <span data-ttu-id="5d650-226">**错误：集线器分辨率/秒**</span><span class="sxs-lookup"><span data-stu-id="5d650-226">**Errors: Hub Resolution/Sec**</span></span>
- <span data-ttu-id="5d650-227">**错误：集线器调用总计**</span><span class="sxs-lookup"><span data-stu-id="5d650-227">**Errors: Hub Invocation Total**</span></span>
- <span data-ttu-id="5d650-228">**错误：集线器调用/秒**</span><span class="sxs-lookup"><span data-stu-id="5d650-228">**Errors: Hub Invocation/Sec**</span></span>
- <span data-ttu-id="5d650-229">**错误：传输总计**</span><span class="sxs-lookup"><span data-stu-id="5d650-229">**Errors: Transport Total**</span></span>
- <span data-ttu-id="5d650-230">**错误：传输/秒**</span><span class="sxs-lookup"><span data-stu-id="5d650-230">**Errors: Transport/Sec**</span></span>

<a id="scaleout_metrics"></a>

<span data-ttu-id="5d650-231">**横向扩展指标**</span><span class="sxs-lookup"><span data-stu-id="5d650-231">**Scaleout metrics**</span></span>

<span data-ttu-id="5d650-232">以下指标衡量横向扩展提供程序生成的流量和错误。</span><span class="sxs-lookup"><span data-stu-id="5d650-232">The following metrics measure traffic and errors generated by the scaleout provider.</span></span> <span data-ttu-id="5d650-233">此上下文中的**流**是横向扩展提供程序使用的缩放单位;如果使用 SQL Server，则这是表;使用服务总线时的主题;如果使用 Redis，则为订阅。</span><span class="sxs-lookup"><span data-stu-id="5d650-233">A **Stream** in this context is a scale unit used by the scaleout provider; this is a table if SQL Server is used, a Topic if Service Bus is used, and a Subscription if Redis is used.</span></span> <span data-ttu-id="5d650-234">每个流确保有序的读取和写入操作;单个流是潜在的规模瓶颈，因此可以增加流的数量，以帮助减少该瓶颈。</span><span class="sxs-lookup"><span data-stu-id="5d650-234">Each stream ensures ordered read and write operations; a single stream is a potential scale bottleneck, so the number of streams can be increased to help reduce that bottleneck.</span></span> <span data-ttu-id="5d650-235">如果使用多个流，SignalR 将自动在这些流中分发（分片）消息，以确保从任何给定连接发送的消息按顺序排列。</span><span class="sxs-lookup"><span data-stu-id="5d650-235">If multiple streams are used, SignalR will automatically distribute (shard) messages across these streams in a way that ensures messages sent from any given connection are in order.</span></span>

<span data-ttu-id="5d650-236">["最大队列长度](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx)"设置控制 SignalR 维护的横向扩展发送队列的长度。</span><span class="sxs-lookup"><span data-stu-id="5d650-236">The [MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx) setting controls the length of the scaleout send queue maintained by SignalR.</span></span> <span data-ttu-id="5d650-237">将其设置为大于 0 的值将使发送队列中的所有消息一次发送到配置的消息背板。</span><span class="sxs-lookup"><span data-stu-id="5d650-237">Setting it to a value greater than 0 will place all messages in a send queue to be sent one at a time to the configured messaging backplane.</span></span> <span data-ttu-id="5d650-238">如果队列的大小高于配置的长度，则后续发送的呼叫将立即失败，使用[InvalidTheAa，](https://msdn.microsoft.com/library/system.invalidoperationexception(v=vs.118).aspx)直到队列中的消息数再次小于设置。</span><span class="sxs-lookup"><span data-stu-id="5d650-238">If the size of the queue goes above the configured length, subsequent calls to send will fail immediately with an [InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception(v=vs.118).aspx) until the number of messages in the queue is less than the setting again.</span></span> <span data-ttu-id="5d650-239">默认情况下禁用排队，因为实现的背板通常有自己的队列或流控制。</span><span class="sxs-lookup"><span data-stu-id="5d650-239">Queueing is disabled by default because the implemented backplanes generally have their own queuing or flow-control in place.</span></span> <span data-ttu-id="5d650-240">对于 SQL Server，连接池有效地限制了任何一次进行发送的次数。</span><span class="sxs-lookup"><span data-stu-id="5d650-240">In the case of SQL Server, connection pooling effectively limits the number of sends going on at any one time.</span></span>

<span data-ttu-id="5d650-241">默认情况下，只有一个流用于 SQL Server 和 Redis，五个流用于服务总线，并且禁用排队，但这些设置可以通过 SQL Server 和服务总线上的配置更改：</span><span class="sxs-lookup"><span data-stu-id="5d650-241">By default, only one stream is used for SQL Server and Redis, five streams are used for Service Bus, and queueing is disabled, but these settings can be changed through configuration on SQL Server and Service Bus:</span></span>

<span data-ttu-id="5d650-242">**.NET 服务器代码，用于配置 SQL Server 背板的表计数和队列长度**</span><span class="sxs-lookup"><span data-stu-id="5d650-242">**.NET Server Code for configuring table count and queue length for SQL Server backplane**</span></span>

[!code-csharp[Main](signalr-performance/samples/sample9.cs)]

<span data-ttu-id="5d650-243">**.NET 服务器代码，用于配置服务总线背板的主题计数和队列长度**</span><span class="sxs-lookup"><span data-stu-id="5d650-243">**.NET Server Code for configuring topic count and queue length for Service Bus backplane**</span></span>

[!code-csharp[Main](signalr-performance/samples/sample10.cs)]

<span data-ttu-id="5d650-244">**缓冲**流是已进入错误状态的流流;当流处于故障状态时，发送到背板的所有消息将立即失败，直到流不再出现故障。</span><span class="sxs-lookup"><span data-stu-id="5d650-244">A **Buffering** stream is one that has entered a faulted state; when the stream is in the faulted state, all messages sent to the backplane will fail immediately until the stream is no longer faulting.</span></span> <span data-ttu-id="5d650-245">**发送队列长度**是已过帐但尚未发送的邮件数。</span><span class="sxs-lookup"><span data-stu-id="5d650-245">The **Send Queue Length** is the number of messages that have been posted but not yet sent.</span></span>

- <span data-ttu-id="5d650-246">**已接收/秒的横向扩展消息总线消息**</span><span class="sxs-lookup"><span data-stu-id="5d650-246">**Scaleout Message Bus Messages Received/Sec**</span></span>
- <span data-ttu-id="5d650-247">**横向扩展流总计**</span><span class="sxs-lookup"><span data-stu-id="5d650-247">**Scaleout Streams Total**</span></span>
- <span data-ttu-id="5d650-248">**展开扩展流**</span><span class="sxs-lookup"><span data-stu-id="5d650-248">**Scaleout Streams Open**</span></span>
- <span data-ttu-id="5d650-249">**横向扩展流缓冲**</span><span class="sxs-lookup"><span data-stu-id="5d650-249">**Scaleout Streams Buffering**</span></span>
- <span data-ttu-id="5d650-250">**横向扩展错误总计**</span><span class="sxs-lookup"><span data-stu-id="5d650-250">**Scaleout Errors Total**</span></span>
- <span data-ttu-id="5d650-251">**横向扩展错误/秒**</span><span class="sxs-lookup"><span data-stu-id="5d650-251">**Scaleout Errors/Sec**</span></span>
- <span data-ttu-id="5d650-252">**横向扩展发送队列长度**</span><span class="sxs-lookup"><span data-stu-id="5d650-252">**Scaleout Send Queue Length**</span></span>

<span data-ttu-id="5d650-253">有关这些计数器正在测量的内容的详细信息，请参阅[使用 Azure 服务总线 进行信号R横向扩展](scaleout-with-windows-azure-service-bus.md)。</span><span class="sxs-lookup"><span data-stu-id="5d650-253">For more information on what these counters are measuring, see [SignalR Scaleout with Azure Service Bus](scaleout-with-windows-azure-service-bus.md).</span></span>

<a id="othercounters"></a>

## <a name="using-other-performance-counters"></a><span data-ttu-id="5d650-254">使用其他性能计数器</span><span class="sxs-lookup"><span data-stu-id="5d650-254">Using other performance counters</span></span>

<span data-ttu-id="5d650-255">以下性能计数器在监视应用程序的性能时可能也很有用。</span><span class="sxs-lookup"><span data-stu-id="5d650-255">The following performance counters may also be useful in monitoring your application's performance.</span></span>

<span data-ttu-id="5d650-256">**内存**</span><span class="sxs-lookup"><span data-stu-id="5d650-256">**Memory**</span></span>

- <span data-ttu-id="5d650-257">.NET CLR\\内存 = 所有堆中的字节（对于 w3wp）</span><span class="sxs-lookup"><span data-stu-id="5d650-257">.NET CLR Memory\\# bytes in all Heaps (for w3wp)</span></span>

<span data-ttu-id="5d650-258">**ASP.NET**</span><span class="sxs-lookup"><span data-stu-id="5d650-258">**ASP.NET**</span></span>

- <span data-ttu-id="5d650-259">ASP.NET_请求当前</span><span class="sxs-lookup"><span data-stu-id="5d650-259">ASP.NET\Requests Current</span></span>
- <span data-ttu-id="5d650-260">ASP.NET_已排队</span><span class="sxs-lookup"><span data-stu-id="5d650-260">ASP.NET\Queued</span></span>
- <span data-ttu-id="5d650-261">ASP.NET_已拒绝</span><span class="sxs-lookup"><span data-stu-id="5d650-261">ASP.NET\Rejected</span></span>

<span data-ttu-id="5d650-262">CPU\*\*\*\*</span><span class="sxs-lookup"><span data-stu-id="5d650-262">**CPU**</span></span>

- <span data-ttu-id="5d650-263">处理器信息+处理器时间</span><span class="sxs-lookup"><span data-stu-id="5d650-263">Processor Information\Processor Time</span></span>

<span data-ttu-id="5d650-264">**TCP/IP**</span><span class="sxs-lookup"><span data-stu-id="5d650-264">**TCP/IP**</span></span>

- <span data-ttu-id="5d650-265">TCPv6/已建立连接</span><span class="sxs-lookup"><span data-stu-id="5d650-265">TCPv6/Connections Established</span></span>
- <span data-ttu-id="5d650-266">TCPv4/已建立连接</span><span class="sxs-lookup"><span data-stu-id="5d650-266">TCPv4/Connections Established</span></span>

<span data-ttu-id="5d650-267">**网络服务**</span><span class="sxs-lookup"><span data-stu-id="5d650-267">**Web Service**</span></span>

- <span data-ttu-id="5d650-268">Web 服务\当前连接</span><span class="sxs-lookup"><span data-stu-id="5d650-268">Web Service\Current Connections</span></span>
- <span data-ttu-id="5d650-269">Web 服务= 最大连接</span><span class="sxs-lookup"><span data-stu-id="5d650-269">Web Service\Maximum Connections</span></span>

<span data-ttu-id="5d650-270">**线程**</span><span class="sxs-lookup"><span data-stu-id="5d650-270">**Threading**</span></span>

- <span data-ttu-id="5d650-271">.NET CLR 锁\\和线程 # 当前逻辑线程</span><span class="sxs-lookup"><span data-stu-id="5d650-271">.NET CLR Locks And Threads\\# of current logical Threads</span></span>
- <span data-ttu-id="5d650-272">.NET CLR 锁\\和线程 # 当前物理线程</span><span class="sxs-lookup"><span data-stu-id="5d650-272">.NET CLR Locks And Threads\\# of current physical Threads</span></span>

<a id="otherresources"></a>

## <a name="other-resources"></a><span data-ttu-id="5d650-273">其他资源</span><span class="sxs-lookup"><span data-stu-id="5d650-273">Other Resources</span></span>

<span data-ttu-id="5d650-274">有关ASP.NET性能监视和调优的详细信息，请参阅以下主题：</span><span class="sxs-lookup"><span data-stu-id="5d650-274">For more information on ASP.NET performance monitoring and tuning, see the following topics:</span></span>

- <span data-ttu-id="5d650-275">[ASP.NET 性能概述](https://msdn.microsoft.com/library/cc668225(v=vs.100).aspx)</span><span class="sxs-lookup"><span data-stu-id="5d650-275">[ASP.NET Performance Overview](https://msdn.microsoft.com/library/cc668225(v=vs.100).aspx)</span></span>
- [<span data-ttu-id="5d650-276">iIS 7.5、IIS 7.0 和 IIS 6.0 上的ASP.NET线程使用情况</span><span class="sxs-lookup"><span data-stu-id="5d650-276">ASP.NET Thread Usage on IIS 7.5, IIS 7.0, and IIS 6.0</span></span>](https://blogs.msdn.com/b/tmarq/archive/2007/07/21/asp-net-thread-usage-on-iis-7-0-and-6-0.aspx)
- [<span data-ttu-id="5d650-277">&lt;应用程序池&gt;元素（Web 设置）</span><span class="sxs-lookup"><span data-stu-id="5d650-277">&lt;applicationPool&gt; Element (Web Settings)</span></span>](https://msdn.microsoft.com/library/dd560842.aspx)

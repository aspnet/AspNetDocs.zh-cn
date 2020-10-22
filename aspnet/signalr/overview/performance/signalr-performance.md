---
uid: signalr/overview/performance/signalr-performance
title: SignalR 性能 |Microsoft Docs
author: bradygaster
description: SignalR 性能
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 3751f5e7-59db-4be0-a290-50abc24e5c84
msc.legacyurl: /signalr/overview/performance/signalr-performance
msc.type: authoredcontent
ms.openlocfilehash: b8a44f4c924c94cdfff1ce7630539b45fe269bbf
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345269"
---
# <a name="signalr-performance"></a><span data-ttu-id="10e38-103">SignalR 性能</span><span class="sxs-lookup"><span data-stu-id="10e38-103">SignalR Performance</span></span>

<span data-ttu-id="10e38-104">作者： [Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="10e38-104">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="10e38-105">本主题介绍如何在 SignalR 应用程序中设计、度量和提高性能。</span><span class="sxs-lookup"><span data-stu-id="10e38-105">This topic describes how to design for, measure, and improve performance in a SignalR application.</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="10e38-106">本主题中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="10e38-106">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="10e38-107">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="10e38-107">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="10e38-108">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="10e38-108">.NET 4.5</span></span>
> - <span data-ttu-id="10e38-109">SignalR 版本2</span><span class="sxs-lookup"><span data-stu-id="10e38-109">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="10e38-110">本主题的早期版本</span><span class="sxs-lookup"><span data-stu-id="10e38-110">Previous versions of this topic</span></span>
>
> <span data-ttu-id="10e38-111">有关早期版本的 SignalR 的信息，请参阅 [SignalR 旧版本](../older-versions/index.md)。</span><span class="sxs-lookup"><span data-stu-id="10e38-111">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="10e38-112">问题和注释</span><span class="sxs-lookup"><span data-stu-id="10e38-112">Questions and comments</span></span>
>
> <span data-ttu-id="10e38-113">请提供有关你喜欢本教程的方式的反馈，并在页面底部的评论中留下反馈。</span><span class="sxs-lookup"><span data-stu-id="10e38-113">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="10e38-114">如果你有与本教程不直接相关的问题，则可以将其发布到 [ASP.NET SignalR 论坛](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 或 [StackOverflow.com](http://stackoverflow.com/)。</span><span class="sxs-lookup"><span data-stu-id="10e38-114">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

<span data-ttu-id="10e38-115">有关 SignalR 性能和缩放的最新演示，请参阅 [使用 ASP.NET SignalR 缩放实时 Web](https://channel9.msdn.com/Events/Build/2013/3-502)。</span><span class="sxs-lookup"><span data-stu-id="10e38-115">For a recent presentation on SignalR performance and scaling, see [Scaling the Real-time Web with ASP.NET SignalR](https://channel9.msdn.com/Events/Build/2013/3-502).</span></span>

<span data-ttu-id="10e38-116">本主题包含以下各节：</span><span class="sxs-lookup"><span data-stu-id="10e38-116">This topic contains the following sections:</span></span>

- [<span data-ttu-id="10e38-117">设计注意事项</span><span class="sxs-lookup"><span data-stu-id="10e38-117">Design considerations</span></span>](#design)
- [<span data-ttu-id="10e38-118">优化 SignalR 服务器的性能</span><span class="sxs-lookup"><span data-stu-id="10e38-118">Tuning your SignalR server for performance</span></span>](#tuning)
- [<span data-ttu-id="10e38-119">性能问题疑难解答</span><span class="sxs-lookup"><span data-stu-id="10e38-119">Troubleshooting performance issues</span></span>](#troubleshooting)
- [<span data-ttu-id="10e38-120">使用 SignalR 性能计数器</span><span class="sxs-lookup"><span data-stu-id="10e38-120">Using SignalR performance counters</span></span>](#perfcounters)
- [<span data-ttu-id="10e38-121">使用其他性能计数器</span><span class="sxs-lookup"><span data-stu-id="10e38-121">Using other performance counters</span></span>](#othercounters)
- [<span data-ttu-id="10e38-122">其他资源</span><span class="sxs-lookup"><span data-stu-id="10e38-122">Other resources</span></span>](#otherresources)

<a id="design"></a>

## <a name="design-considerations"></a><span data-ttu-id="10e38-123">设计注意事项</span><span class="sxs-lookup"><span data-stu-id="10e38-123">Design considerations</span></span>

<span data-ttu-id="10e38-124">本部分介绍在设计 SignalR 应用程序的过程中可以实现的模式，以确保不会通过生成不必要的网络流量来影响性能。</span><span class="sxs-lookup"><span data-stu-id="10e38-124">This section describes patterns that can be implemented during the design of a SignalR application, to ensure that performance is not being hindered by generating unnecessary network traffic.</span></span>

### <a name="throttling-message-frequency"></a><span data-ttu-id="10e38-125">限制消息频率</span><span class="sxs-lookup"><span data-stu-id="10e38-125">Throttling message frequency</span></span>

<span data-ttu-id="10e38-126">即使在以高频率发送消息 (如实时游戏应用程序) 的应用程序中，大多数应用程序也不需要发送多条消息。</span><span class="sxs-lookup"><span data-stu-id="10e38-126">Even in an application that sends out messages at a high frequency (such as a realtime gaming application), most applications don't need to send more than a few messages a second.</span></span> <span data-ttu-id="10e38-127">若要减少每个客户端生成的流量，可以实现消息循环，使队列和发送消息的频率不高于固定速率 (也就是说，如果在该时间间隔内发送的消息) ，则每秒发送的消息数将为每秒发送的消息数。</span><span class="sxs-lookup"><span data-stu-id="10e38-127">To reduce the amount of traffic that each client generates, a message loop can be implemented that queues and sends out messages no more frequently than a fixed rate (that is, up to a certain number of messages will be sent every second, if there are messages in that time interval to be sent).</span></span> <span data-ttu-id="10e38-128">有关将消息限制为从客户端和服务器)  (的示例应用程序，请参阅 [使用 SignalR 的高频率实时](../getting-started/tutorial-high-frequency-realtime-with-signalr.md)。</span><span class="sxs-lookup"><span data-stu-id="10e38-128">For a sample application that throttles messages to a certain rate (from both client and server), see [High-Frequency Realtime with SignalR](../getting-started/tutorial-high-frequency-realtime-with-signalr.md).</span></span>

### <a name="reducing-message-size"></a><span data-ttu-id="10e38-129">减小消息大小</span><span class="sxs-lookup"><span data-stu-id="10e38-129">Reducing message size</span></span>

<span data-ttu-id="10e38-130">可以通过减小序列化对象的大小来减小 SignalR 消息的大小。</span><span class="sxs-lookup"><span data-stu-id="10e38-130">You can reduce the size of a SignalR message by reducing the size of your serialized objects.</span></span> <span data-ttu-id="10e38-131">在服务器代码中，如果要发送的对象包含不需要传输的属性，则通过使用属性防止这些属性进行序列化 `JsonIgnore` 。</span><span class="sxs-lookup"><span data-stu-id="10e38-131">In server code, if you're sending an object that contains properties that don't need to be transmitted, prevent those properties from being serialized by using the `JsonIgnore` attribute.</span></span> <span data-ttu-id="10e38-132">属性的名称也存储在消息中;使用特性可以缩短属性的名称 `JsonProperty` 。</span><span class="sxs-lookup"><span data-stu-id="10e38-132">The names of properties are also stored in the message; the names of properties can be shortened using the `JsonProperty` attribute.</span></span> <span data-ttu-id="10e38-133">下面的代码示例演示如何排除将某个属性发送到客户端，以及如何缩短属性名称：</span><span class="sxs-lookup"><span data-stu-id="10e38-133">The following code sample demonstrates how to exclude a property from being sent to the client, and how to shorten property names:</span></span>

<span data-ttu-id="10e38-134">**.NET 服务器代码，该代码演示了用于排除发送到客户端的数据的 JsonIgnore 特性，以及用于减小消息大小的 JsonProperty 特性**</span><span class="sxs-lookup"><span data-stu-id="10e38-134">**.NET server code that demonstrates the JsonIgnore attribute to exclude data from being sent to the client, and the JsonProperty attribute to reduce message size**</span></span>

[!code-csharp[Main](signalr-performance/samples/sample1.cs?highlight=5,7,10)]

<span data-ttu-id="10e38-135">若要在客户端代码中保留可读性/可维护性，在收到消息后，可将缩略属性名称重新映射到友好名称。</span><span class="sxs-lookup"><span data-stu-id="10e38-135">In order to retain readability/ maintainability in the client code, the abbreviated property names can be remapped to human-friendly names after the message is received.</span></span> <span data-ttu-id="10e38-136">下面的代码示例演示了一种可能的方法：将缩短的名称重新映射到较长的名称，方法是：定义消息协定 (映射) ，并使用 `reMap` 函数将协定应用到优化的消息类：</span><span class="sxs-lookup"><span data-stu-id="10e38-136">The following code sample demonstrates one possible way of remapping shortened names to longer ones, by defining a message contract (mapping), and using the `reMap` function to apply the contract to the optimized message class:</span></span>

<span data-ttu-id="10e38-137">**将简化的属性名称重新映射到用户可读名称的客户端 JavaScript 代码**</span><span class="sxs-lookup"><span data-stu-id="10e38-137">**Client-side JavaScript code that remaps shortened property names to human-readable names**</span></span>

[!code-javascript[Main](signalr-performance/samples/sample2.js)]

<span data-ttu-id="10e38-138">使用相同的方法，还可以将客户端的消息中的名称缩写给服务器。</span><span class="sxs-lookup"><span data-stu-id="10e38-138">Names can be shortened in messages from the client to the server as well, using the same method.</span></span>

<span data-ttu-id="10e38-139">减少内存占用量 (也就是说，消息对象的消息) 所使用的内存量也会提高性能。</span><span class="sxs-lookup"><span data-stu-id="10e38-139">Reducing the memory footprint (that is, the amount of memory used for the message) of the message object can also improve performance.</span></span> <span data-ttu-id="10e38-140">例如，如果不需要的完整范围 `int` ， `short` `byte` 可以改为使用或。</span><span class="sxs-lookup"><span data-stu-id="10e38-140">For example, if the full range of an `int` is not needed, a `short` or `byte` can be used instead.</span></span>

<span data-ttu-id="10e38-141">由于消息存储在服务器内存中的消息总线上，因此减少消息大小也可能解决服务器内存问题。</span><span class="sxs-lookup"><span data-stu-id="10e38-141">Since messages are stored in the message bus in server memory, reducing the size of messages can also address server memory issues.</span></span>

<a id="tuning"></a>

### <a name="tuning-your-signalr-server-for-performance"></a><span data-ttu-id="10e38-142">优化 SignalR 服务器的性能</span><span class="sxs-lookup"><span data-stu-id="10e38-142">Tuning your SignalR server for performance</span></span>

<span data-ttu-id="10e38-143">以下配置设置可用于优化服务器，以在 SignalR 应用程序中获得更好的性能。</span><span class="sxs-lookup"><span data-stu-id="10e38-143">The following configuration settings can be used to tune your server for better performance in a SignalR application.</span></span> <span data-ttu-id="10e38-144">有关如何在 ASP.NET 应用程序中提高性能的常规信息，请参阅 [改善 ASP.NET 性能](https://msdn.microsoft.com/library/ff647787.aspx)。</span><span class="sxs-lookup"><span data-stu-id="10e38-144">For general information on how to improve performance in an ASP.NET application, see [Improving ASP.NET Performance](https://msdn.microsoft.com/library/ff647787.aspx).</span></span>

<span data-ttu-id="10e38-145">**SignalR 配置设置**</span><span class="sxs-lookup"><span data-stu-id="10e38-145">**SignalR configuration settings**</span></span>

- <span data-ttu-id="10e38-146">**DefaultMessageBufferSize**：默认情况下，SignalR 每次连接时在内存中保留1000消息。</span><span class="sxs-lookup"><span data-stu-id="10e38-146">**DefaultMessageBufferSize**: By default, SignalR retains 1000 messages in memory per hub per connection.</span></span> <span data-ttu-id="10e38-147">如果正在使用大消息，这可能会产生内存问题，可以通过减少该值来缓解此问题。</span><span class="sxs-lookup"><span data-stu-id="10e38-147">If large messages are being used, this may create memory issues which can be alleviated by reducing this value.</span></span> <span data-ttu-id="10e38-148">此设置可在 `Application_Start` ASP.NET 应用程序中的事件处理程序中设置，或在 `Configuration` 自承载应用程序中的 OWIN startup 类的方法中设置。</span><span class="sxs-lookup"><span data-stu-id="10e38-148">This setting can be set in the `Application_Start` event handler in an ASP.NET application, or in the `Configuration` method of an OWIN startup class in a self-hosted application.</span></span> <span data-ttu-id="10e38-149">下面的示例演示如何减小此值以便减少应用程序的内存占用量，以减少使用的服务器内存量：</span><span class="sxs-lookup"><span data-stu-id="10e38-149">The following sample demonstrates how to reduce this value in order to reduce the memory footprint of your application in order to reduce the amount of server memory used:</span></span>

    <span data-ttu-id="10e38-150">**Startup.cs 中用于减小默认消息缓冲区大小的 .NET server 代码**</span><span class="sxs-lookup"><span data-stu-id="10e38-150">**.NET server code in Startup.cs for decreasing default message buffer size**</span></span>

    [!code-csharp[Main](signalr-performance/samples/sample3.cs)]

<span data-ttu-id="10e38-151">**IIS 配置设置**</span><span class="sxs-lookup"><span data-stu-id="10e38-151">**IIS configuration settings**</span></span>

- <span data-ttu-id="10e38-152">**每个应用程序的最大并发请求**数：增加并发 IIS 请求数将增加可用于为请求提供服务的服务器资源。</span><span class="sxs-lookup"><span data-stu-id="10e38-152">**Max concurrent requests per application**: Increasing the number of concurrent IIS requests will increase server resources available for serving requests.</span></span> <span data-ttu-id="10e38-153">默认值为 5000;若要增加此设置，请在提升的命令提示符下执行以下命令：</span><span class="sxs-lookup"><span data-stu-id="10e38-153">The default value is 5000; to increase this setting, execute the following commands in an elevated command prompt:</span></span>

    [!code-console[Main](signalr-performance/samples/sample4.cmd)]
- <span data-ttu-id="10e38-154">**ApplicationPool QueueLength**：这是为应用程序池 Http.sys 队列的最大请求数。</span><span class="sxs-lookup"><span data-stu-id="10e38-154">**ApplicationPool QueueLength**: This is the maximum number of requests that Http.sys queues for the application pool.</span></span> <span data-ttu-id="10e38-155">如果队列已满，则新请求将收到 503 "服务不可用" 响应。</span><span class="sxs-lookup"><span data-stu-id="10e38-155">When the queue is full, new requests receive a 503 "Service Unavailable" response.</span></span> <span data-ttu-id="10e38-156">默认值为 1000。</span><span class="sxs-lookup"><span data-stu-id="10e38-156">The default value is 1000.</span></span>

    <span data-ttu-id="10e38-157">缩短承载应用程序的应用程序池中的工作进程的队列长度将节省内存资源。</span><span class="sxs-lookup"><span data-stu-id="10e38-157">Shortening the queue length for the worker process in the application pool hosting your application will conserve memory resources.</span></span> <span data-ttu-id="10e38-158">有关详细信息，请参阅 [管理、优化和配置应用程序池](https://technet.microsoft.com/library/cc745955.aspx)。</span><span class="sxs-lookup"><span data-stu-id="10e38-158">For more information, see [Managing, Tuning, and Configuring Application Pools](https://technet.microsoft.com/library/cc745955.aspx).</span></span>

<span data-ttu-id="10e38-159">**ASP.NET 配置设置**</span><span class="sxs-lookup"><span data-stu-id="10e38-159">**ASP.NET configuration settings**</span></span>

<span data-ttu-id="10e38-160">本部分包括可以在文件中设置的配置设置 `aspnet.config` 。</span><span class="sxs-lookup"><span data-stu-id="10e38-160">This section includes configuration settings that can be set in the `aspnet.config` file.</span></span> <span data-ttu-id="10e38-161">此文件位于以下两个位置之一，具体取决于平台：</span><span class="sxs-lookup"><span data-stu-id="10e38-161">This file is found in one of two locations, depending on platform:</span></span>

- `%windir%\Microsoft.NET\Framework\v4.0.30319\aspnet.config`
- `%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet.config`

<span data-ttu-id="10e38-162">可提高 SignalR 性能的 ASP.NET 设置包括：</span><span class="sxs-lookup"><span data-stu-id="10e38-162">ASP.NET settings that may improve SignalR performance include the following:</span></span>

- <span data-ttu-id="10e38-163">**每 CPU 的最大并发请求**数：增加此设置可以缓解性能瓶颈。</span><span class="sxs-lookup"><span data-stu-id="10e38-163">**Maximum concurrent requests per CPU**: Increasing this setting may alleviate performance bottlenecks.</span></span> <span data-ttu-id="10e38-164">若要增加此设置，请将以下配置设置添加到 `aspnet.config` 文件中：</span><span class="sxs-lookup"><span data-stu-id="10e38-164">To increase this setting, add the following configuration setting to the `aspnet.config` file:</span></span>

    [!code-xml[Main](signalr-performance/samples/sample5.xml?highlight=4)]
- <span data-ttu-id="10e38-165">**请求队列限制**：当连接总数超过设置值时 `maxConcurrentRequestsPerCPU` ，ASP.NET 将使用队列开始限制请求。</span><span class="sxs-lookup"><span data-stu-id="10e38-165">**Request Queue Limit**: When the total number of connections exceeds the `maxConcurrentRequestsPerCPU` setting, ASP.NET will start throttling requests using a queue.</span></span> <span data-ttu-id="10e38-166">若要增加队列的大小，可以增加 `requestQueueLimit` 设置。</span><span class="sxs-lookup"><span data-stu-id="10e38-166">To increase the size of the queue, you can increase the `requestQueueLimit` setting.</span></span> <span data-ttu-id="10e38-167">为此，请将以下配置设置添加到 `processModel` (中的节点， `config/machine.config` 而不是 `aspnet.config`) ：</span><span class="sxs-lookup"><span data-stu-id="10e38-167">To do this, add the following configuration setting to the `processModel` node in `config/machine.config` (rather than `aspnet.config`):</span></span>

    [!code-xml[Main](signalr-performance/samples/sample6.xml)]

<a id="troubleshooting"></a>

## <a name="troubleshooting-performance-issues"></a><span data-ttu-id="10e38-168">性能问题故障排除</span><span class="sxs-lookup"><span data-stu-id="10e38-168">Troubleshooting performance issues</span></span>

<span data-ttu-id="10e38-169">本部分介绍在应用程序中查找性能瓶颈的方法。</span><span class="sxs-lookup"><span data-stu-id="10e38-169">This section describes ways to find performance bottlenecks in your application.</span></span>

### <a name="verifying-that-websocket-is-being-used"></a><span data-ttu-id="10e38-170">验证是否正在使用 WebSocket</span><span class="sxs-lookup"><span data-stu-id="10e38-170">Verifying that WebSocket is being used</span></span>

<span data-ttu-id="10e38-171">尽管 SignalR 可以使用各种传输来实现客户端与服务器之间的通信，但 WebSocket 提供了显著的性能优势，如果客户端和服务器支持，则应使用这些传输。</span><span class="sxs-lookup"><span data-stu-id="10e38-171">While SignalR can use a variety of transports for communication between client and server, WebSocket offers a significant performance advantage, and should be used if the client and server support it.</span></span> <span data-ttu-id="10e38-172">若要确定客户端和服务器是否满足 WebSocket 的要求，请参阅 [传输和回退](../getting-started/introduction-to-signalr.md#transports)。</span><span class="sxs-lookup"><span data-stu-id="10e38-172">To determine if your client and server meet the requirements for WebSocket, see [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span> <span data-ttu-id="10e38-173">若要确定应用程序中使用的传输，可以使用浏览器开发人员工具，并检查日志以查看连接所使用的传输。</span><span class="sxs-lookup"><span data-stu-id="10e38-173">To determine what transport is being used in your application, you can use the browser developer tools, and examine the logs to see what transport is being used for the connection.</span></span> <span data-ttu-id="10e38-174">有关在 Internet Explorer 和 Chrome 中使用浏览器开发工具的信息，请参阅 [传输和回退](../getting-started/introduction-to-signalr.md#transports)。</span><span class="sxs-lookup"><span data-stu-id="10e38-174">For information on using the browser development tools in Internet Explorer and Chrome, see [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span>

<a id="perfcounters"></a>

## <a name="using-signalr-performance-counters"></a><span data-ttu-id="10e38-175">使用 SignalR 性能计数器</span><span class="sxs-lookup"><span data-stu-id="10e38-175">Using SignalR performance counters</span></span>

<span data-ttu-id="10e38-176">本部分介绍如何启用和使用在包中找到的 SignalR 性能计数器 `Microsoft.AspNet.SignalR.Utils` 。</span><span class="sxs-lookup"><span data-stu-id="10e38-176">This section describes how to enable and use SignalR performance counters, found in the `Microsoft.AspNet.SignalR.Utils` package.</span></span>

### <a name="installing-signalrexe"></a><span data-ttu-id="10e38-177">安装 signalr.exe</span><span class="sxs-lookup"><span data-stu-id="10e38-177">Installing signalr.exe</span></span>

<span data-ttu-id="10e38-178">可以使用名为 SignalR.exe 的实用程序将性能计数器添加到服务器。</span><span class="sxs-lookup"><span data-stu-id="10e38-178">Performance counters can be added to the server using a utility called SignalR.exe.</span></span> <span data-ttu-id="10e38-179">若要安装此实用程序，请执行以下步骤：</span><span class="sxs-lookup"><span data-stu-id="10e38-179">To install this utility, follow these steps:</span></span>

1. <span data-ttu-id="10e38-180">在 Visual Studio 中，选择 "**工具**" "  >  **nuget 包管理器**" "  >  **管理解决方案的 NuGet 包**"</span><span class="sxs-lookup"><span data-stu-id="10e38-180">In Visual Studio, select **Tools** > **NuGet Package Manager** > **Manage NuGet Packages for Solution**</span></span>
2. <span data-ttu-id="10e38-181">搜索 **signalr. utils**，并选择 "安装"。</span><span class="sxs-lookup"><span data-stu-id="10e38-181">Search for **signalr.utils**, and select Install.</span></span>

    ![](signalr-performance/_static/image1.png)
3. <span data-ttu-id="10e38-182">接受许可协议以安装包。</span><span class="sxs-lookup"><span data-stu-id="10e38-182">Accept the license agreement to install the package.</span></span>
4. <span data-ttu-id="10e38-183">SignalR.exe 将安装到 `<project folder>/packages/Microsoft.AspNet.SignalR.Utils.<version>/tools` 。</span><span class="sxs-lookup"><span data-stu-id="10e38-183">SignalR.exe will be installed to `<project folder>/packages/Microsoft.AspNet.SignalR.Utils.<version>/tools`.</span></span>

### <a name="installing-performance-counters-with-signalrexe"></a><span data-ttu-id="10e38-184">SignalR.exe 安装性能计数器</span><span class="sxs-lookup"><span data-stu-id="10e38-184">Installing performance counters with SignalR.exe</span></span>

<span data-ttu-id="10e38-185">若要安装 SignalR 性能计数器，请使用以下参数在提升的命令提示符下运行 SignalR.exe：</span><span class="sxs-lookup"><span data-stu-id="10e38-185">To install SignalR performance counters, run SignalR.exe in an elevated command prompt with the following parameter:</span></span>

[!code-console[Main](signalr-performance/samples/sample7.cmd)]

<span data-ttu-id="10e38-186">若要删除 SignalR 性能计数器，请使用以下参数在提升的命令提示符下运行 SignalR.exe：</span><span class="sxs-lookup"><span data-stu-id="10e38-186">To remove SignalR performance counters, run SignalR.exe in an elevated command prompt with the following parameter:</span></span>

[!code-console[Main](signalr-performance/samples/sample8.cmd)]

### <a name="signalr-performance-counters"></a><span data-ttu-id="10e38-187">SignalR 性能计数器</span><span class="sxs-lookup"><span data-stu-id="10e38-187">SignalR Performance counters</span></span>

<span data-ttu-id="10e38-188">实用工具包将安装下列性能计数器。</span><span class="sxs-lookup"><span data-stu-id="10e38-188">The utilities package installs the following performance counters.</span></span> <span data-ttu-id="10e38-189">"Total" 计数器测量自上次应用程序池或服务器重新启动后发生的事件数。</span><span class="sxs-lookup"><span data-stu-id="10e38-189">The "Total" counters measure the number of events since the last application pool or server restart.</span></span>

<span data-ttu-id="10e38-190">**连接指标**</span><span class="sxs-lookup"><span data-stu-id="10e38-190">**Connection metrics**</span></span>

<span data-ttu-id="10e38-191">以下度量值测量发生的连接生存期事件。</span><span class="sxs-lookup"><span data-stu-id="10e38-191">The following metrics measure the connection lifetime events that occur.</span></span> <span data-ttu-id="10e38-192">有关详细信息，请参阅 [了解和处理连接生存期事件](../guide-to-the-api/handling-connection-lifetime-events.md)。</span><span class="sxs-lookup"><span data-stu-id="10e38-192">For more information, see [Understanding and Handling Connection Lifetime Events](../guide-to-the-api/handling-connection-lifetime-events.md).</span></span>

- <span data-ttu-id="10e38-193">**连接已连接**</span><span class="sxs-lookup"><span data-stu-id="10e38-193">**Connections Connected**</span></span>
- <span data-ttu-id="10e38-194">**连接已重新连接**</span><span class="sxs-lookup"><span data-stu-id="10e38-194">**Connections Reconnected**</span></span>
- <span data-ttu-id="10e38-195">**断开连接**</span><span class="sxs-lookup"><span data-stu-id="10e38-195">**Connections Disconnected**</span></span>
- <span data-ttu-id="10e38-196">**当前连接数**</span><span class="sxs-lookup"><span data-stu-id="10e38-196">**Connections Current**</span></span>

<span data-ttu-id="10e38-197">**消息指标**</span><span class="sxs-lookup"><span data-stu-id="10e38-197">**Message metrics**</span></span>

<span data-ttu-id="10e38-198">以下度量值测量由 SignalR 生成的消息流量。</span><span class="sxs-lookup"><span data-stu-id="10e38-198">The following metrics measure the message traffic generated by SignalR.</span></span>

- <span data-ttu-id="10e38-199">**接收的连接消息总数**</span><span class="sxs-lookup"><span data-stu-id="10e38-199">**Connection Messages Received Total**</span></span>
- <span data-ttu-id="10e38-200">**已发送的连接消息总数**</span><span class="sxs-lookup"><span data-stu-id="10e38-200">**Connection Messages Sent Total**</span></span>
- <span data-ttu-id="10e38-201">**每秒接收的连接消息数**</span><span class="sxs-lookup"><span data-stu-id="10e38-201">**Connection Messages Received/Sec**</span></span>
- <span data-ttu-id="10e38-202">**发送的连接消息/秒**</span><span class="sxs-lookup"><span data-stu-id="10e38-202">**Connection Messages Sent/Sec**</span></span>

<span data-ttu-id="10e38-203">**消息总线指标**</span><span class="sxs-lookup"><span data-stu-id="10e38-203">**Message bus metrics**</span></span>

<span data-ttu-id="10e38-204">以下度量值度量通过内部 SignalR 消息总线的流量，其中放置了所有传入和传出 SignalR 消息的队列。</span><span class="sxs-lookup"><span data-stu-id="10e38-204">The following metrics measure traffic through the internal SignalR message bus, the queue in which all incoming and outgoing SignalR messages are placed.</span></span> <span data-ttu-id="10e38-205">发送或广播消息时，会将其 **发布** 。</span><span class="sxs-lookup"><span data-stu-id="10e38-205">A message is **Published** when it is sent or broadcast.</span></span> <span data-ttu-id="10e38-206">在此上下文中， **订阅服务器** 是对消息总线的订阅;这应该等于客户端数量加上服务器本身。</span><span class="sxs-lookup"><span data-stu-id="10e38-206">A **Subscriber** in this context is a subscription on the message bus; this should equal the number of clients plus the server itself.</span></span> <span data-ttu-id="10e38-207">已 **分配的工作线程** 是将数据发送到活动连接的组件; **繁忙辅助角色** 是指主动发送消息的辅助角色。</span><span class="sxs-lookup"><span data-stu-id="10e38-207">An **Allocated Worker** is a component that sends data to active connections; a **Busy Worker** is one that is actively sending a message.</span></span>

- <span data-ttu-id="10e38-208">**消息总线接收消息总数**</span><span class="sxs-lookup"><span data-stu-id="10e38-208">**Message Bus Messages Received Total**</span></span>
- <span data-ttu-id="10e38-209">**每秒接收的消息总线消息数**</span><span class="sxs-lookup"><span data-stu-id="10e38-209">**Message Bus Messages Received/Sec**</span></span>
- <span data-ttu-id="10e38-210">**消息总线消息已发布总计**</span><span class="sxs-lookup"><span data-stu-id="10e38-210">**Message Bus Messages Published Total**</span></span>
- <span data-ttu-id="10e38-211">**发布的消息总线消息数/秒**</span><span class="sxs-lookup"><span data-stu-id="10e38-211">**Message Bus Messages Published/Sec**</span></span>
- <span data-ttu-id="10e38-212">**消息总线订阅服务器当前**</span><span class="sxs-lookup"><span data-stu-id="10e38-212">**Message Bus Subscribers Current**</span></span>
- <span data-ttu-id="10e38-213">**消息总线订阅服务器总数**</span><span class="sxs-lookup"><span data-stu-id="10e38-213">**Message Bus Subscribers Total**</span></span>
- <span data-ttu-id="10e38-214">**消息总线订阅者数/秒**</span><span class="sxs-lookup"><span data-stu-id="10e38-214">**Message Bus Subscribers/Sec**</span></span>
- <span data-ttu-id="10e38-215">**消息总线分配的工作线程**</span><span class="sxs-lookup"><span data-stu-id="10e38-215">**Message Bus Allocated Workers**</span></span>
- <span data-ttu-id="10e38-216">**消息总线繁忙辅助角色**</span><span class="sxs-lookup"><span data-stu-id="10e38-216">**Message Bus Busy Workers**</span></span>
- <span data-ttu-id="10e38-217">**消息总线主题当前**</span><span class="sxs-lookup"><span data-stu-id="10e38-217">**Message Bus Topics Current**</span></span>

<span data-ttu-id="10e38-218">**错误度量值**</span><span class="sxs-lookup"><span data-stu-id="10e38-218">**Error metrics**</span></span>

<span data-ttu-id="10e38-219">以下度量值度量 SignalR 消息流量生成的错误。</span><span class="sxs-lookup"><span data-stu-id="10e38-219">The following metrics measure errors generated by SignalR message traffic.</span></span> <span data-ttu-id="10e38-220">集线器**解析**错误发生在无法解析集线器或集线器方法时。</span><span class="sxs-lookup"><span data-stu-id="10e38-220">**Hub Resolution** errors occur when a hub or hub method cannot be resolved.</span></span> <span data-ttu-id="10e38-221">**中心调用** 错误是调用集线器方法时引发的异常。</span><span class="sxs-lookup"><span data-stu-id="10e38-221">**Hub Invocation** errors are exceptions thrown while invoking a hub method.</span></span> <span data-ttu-id="10e38-222">**传输** 错误是 HTTP 请求或响应期间引发的连接错误。</span><span class="sxs-lookup"><span data-stu-id="10e38-222">**Transport** errors are connection errors thrown during an HTTP request or response.</span></span>

- <span data-ttu-id="10e38-223">**错误：全部总计**</span><span class="sxs-lookup"><span data-stu-id="10e38-223">**Errors: All Total**</span></span>
- <span data-ttu-id="10e38-224">**错误：全部/秒**</span><span class="sxs-lookup"><span data-stu-id="10e38-224">**Errors: All/Sec**</span></span>
- <span data-ttu-id="10e38-225">**错误：集线器解析总数**</span><span class="sxs-lookup"><span data-stu-id="10e38-225">**Errors: Hub Resolution Total**</span></span>
- <span data-ttu-id="10e38-226">**错误：集线器分辨率/秒**</span><span class="sxs-lookup"><span data-stu-id="10e38-226">**Errors: Hub Resolution/Sec**</span></span>
- <span data-ttu-id="10e38-227">**错误：集线器调用总数**</span><span class="sxs-lookup"><span data-stu-id="10e38-227">**Errors: Hub Invocation Total**</span></span>
- <span data-ttu-id="10e38-228">**错误：集线器调用数/秒**</span><span class="sxs-lookup"><span data-stu-id="10e38-228">**Errors: Hub Invocation/Sec**</span></span>
- <span data-ttu-id="10e38-229">**错误：传输总数**</span><span class="sxs-lookup"><span data-stu-id="10e38-229">**Errors: Transport Total**</span></span>
- <span data-ttu-id="10e38-230">**错误：传输数/秒**</span><span class="sxs-lookup"><span data-stu-id="10e38-230">**Errors: Transport/Sec**</span></span>

<a id="scaleout_metrics"></a>

<span data-ttu-id="10e38-231">**扩展指标**</span><span class="sxs-lookup"><span data-stu-id="10e38-231">**Scaleout metrics**</span></span>

<span data-ttu-id="10e38-232">以下度量值度量扩展提供程序生成的流量和错误。</span><span class="sxs-lookup"><span data-stu-id="10e38-232">The following metrics measure traffic and errors generated by the scaleout provider.</span></span> <span data-ttu-id="10e38-233">此上下文中的 **流** 是扩展提供程序使用的缩放单位;如果使用 SQL Server，则这是一个表; 如果使用了服务总线，则为一个主题，如果使用了 Redis，则为一个订阅。</span><span class="sxs-lookup"><span data-stu-id="10e38-233">A **Stream** in this context is a scale unit used by the scaleout provider; this is a table if SQL Server is used, a Topic if Service Bus is used, and a Subscription if Redis is used.</span></span> <span data-ttu-id="10e38-234">每个流都确保按顺序进行读写操作;单个流是潜在的缩放瓶颈，因此可以增加流数量以帮助减少瓶颈。</span><span class="sxs-lookup"><span data-stu-id="10e38-234">Each stream ensures ordered read and write operations; a single stream is a potential scale bottleneck, so the number of streams can be increased to help reduce that bottleneck.</span></span> <span data-ttu-id="10e38-235">如果使用多个流，则 SignalR 会自动在这些流上分发 (分片) 消息，从而确保按顺序发送从任何给定连接发送的消息。</span><span class="sxs-lookup"><span data-stu-id="10e38-235">If multiple streams are used, SignalR will automatically distribute (shard) messages across these streams in a way that ensures messages sent from any given connection are in order.</span></span>

<span data-ttu-id="10e38-236">[MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx)设置控制 SignalR 维护的扩展发送队列的长度。</span><span class="sxs-lookup"><span data-stu-id="10e38-236">The [MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx) setting controls the length of the scaleout send queue maintained by SignalR.</span></span> <span data-ttu-id="10e38-237">如果将其设置为大于0的值，则会将发送队列中的所有消息一次发送到配置的消息传送底板。</span><span class="sxs-lookup"><span data-stu-id="10e38-237">Setting it to a value greater than 0 will place all messages in a send queue to be sent one at a time to the configured messaging backplane.</span></span> <span data-ttu-id="10e38-238">如果队列的大小超过配置的长度，则后续的发送调用将立即失败并返回 [InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception(v=vs.118).aspx) ，直到队列中的消息数小于设置。</span><span class="sxs-lookup"><span data-stu-id="10e38-238">If the size of the queue goes above the configured length, subsequent calls to send will fail immediately with an [InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception(v=vs.118).aspx) until the number of messages in the queue is less than the setting again.</span></span> <span data-ttu-id="10e38-239">默认情况下，队列处于禁用状态，因为实现的底板通常具有自己的队列或流控制。</span><span class="sxs-lookup"><span data-stu-id="10e38-239">Queueing is disabled by default because the implemented backplanes generally have their own queuing or flow-control in place.</span></span> <span data-ttu-id="10e38-240">在 SQL Server 情况下，连接池会有效地限制每次发送的发送的次数。</span><span class="sxs-lookup"><span data-stu-id="10e38-240">In the case of SQL Server, connection pooling effectively limits the number of sends going on at any one time.</span></span>

<span data-ttu-id="10e38-241">默认情况下，只有一个流用于 SQL Server 和 Redis，5个流用于服务总线，而队列被禁用，但这些设置可以通过 SQL Server 和服务总线上的配置进行更改：</span><span class="sxs-lookup"><span data-stu-id="10e38-241">By default, only one stream is used for SQL Server and Redis, five streams are used for Service Bus, and queueing is disabled, but these settings can be changed through configuration on SQL Server and Service Bus:</span></span>

<span data-ttu-id="10e38-242">**用于配置 SQL Server 底板的表计数和队列长度的 .NET Server 代码**</span><span class="sxs-lookup"><span data-stu-id="10e38-242">**.NET Server Code for configuring table count and queue length for SQL Server backplane**</span></span>

[!code-csharp[Main](signalr-performance/samples/sample9.cs)]

<span data-ttu-id="10e38-243">**用于配置服务总线背板的主题计数和队列长度的 .NET Server 代码**</span><span class="sxs-lookup"><span data-stu-id="10e38-243">**.NET Server Code for configuring topic count and queue length for Service Bus backplane**</span></span>

[!code-csharp[Main](signalr-performance/samples/sample10.cs)]

<span data-ttu-id="10e38-244">**缓冲**流是进入出错状态的流;当流处于出错状态时，发送到底板的所有消息都将立即失败，直到流不再出错。</span><span class="sxs-lookup"><span data-stu-id="10e38-244">A **Buffering** stream is one that has entered a faulted state; when the stream is in the faulted state, all messages sent to the backplane will fail immediately until the stream is no longer faulting.</span></span> <span data-ttu-id="10e38-245">**发送队列长度**是已发布但尚未发送的消息数。</span><span class="sxs-lookup"><span data-stu-id="10e38-245">The **Send Queue Length** is the number of messages that have been posted but not yet sent.</span></span>

- <span data-ttu-id="10e38-246">**扩展消息总线消息数/秒**</span><span class="sxs-lookup"><span data-stu-id="10e38-246">**Scaleout Message Bus Messages Received/Sec**</span></span>
- <span data-ttu-id="10e38-247">**扩展流总数**</span><span class="sxs-lookup"><span data-stu-id="10e38-247">**Scaleout Streams Total**</span></span>
- <span data-ttu-id="10e38-248">**扩展流打开**</span><span class="sxs-lookup"><span data-stu-id="10e38-248">**Scaleout Streams Open**</span></span>
- <span data-ttu-id="10e38-249">**扩展流缓冲**</span><span class="sxs-lookup"><span data-stu-id="10e38-249">**Scaleout Streams Buffering**</span></span>
- <span data-ttu-id="10e38-250">**扩展错误总数**</span><span class="sxs-lookup"><span data-stu-id="10e38-250">**Scaleout Errors Total**</span></span>
- <span data-ttu-id="10e38-251">**扩展错误数/秒**</span><span class="sxs-lookup"><span data-stu-id="10e38-251">**Scaleout Errors/Sec**</span></span>
- <span data-ttu-id="10e38-252">**扩展发送队列长度**</span><span class="sxs-lookup"><span data-stu-id="10e38-252">**Scaleout Send Queue Length**</span></span>

<span data-ttu-id="10e38-253">有关这些计数器度量的详细信息，请参阅 [SignalR 扩展 With Azure Service Bus](scaleout-with-windows-azure-service-bus.md)。</span><span class="sxs-lookup"><span data-stu-id="10e38-253">For more information on what these counters are measuring, see [SignalR Scaleout with Azure Service Bus](scaleout-with-windows-azure-service-bus.md).</span></span>

<a id="othercounters"></a>

## <a name="using-other-performance-counters"></a><span data-ttu-id="10e38-254">使用其他性能计数器</span><span class="sxs-lookup"><span data-stu-id="10e38-254">Using other performance counters</span></span>

<span data-ttu-id="10e38-255">以下性能计数器对于监视应用程序的性能可能也很有用。</span><span class="sxs-lookup"><span data-stu-id="10e38-255">The following performance counters may also be useful in monitoring your application's performance.</span></span>

<span data-ttu-id="10e38-256">**内存**</span><span class="sxs-lookup"><span data-stu-id="10e38-256">**Memory**</span></span>

- <span data-ttu-id="10e38-257">\\W3wp.exe) 的所有堆中的 .NET CLR 内存 # 字节 (</span><span class="sxs-lookup"><span data-stu-id="10e38-257">.NET CLR Memory\\# bytes in all Heaps (for w3wp)</span></span>

<span data-ttu-id="10e38-258">**ASP.NET**</span><span class="sxs-lookup"><span data-stu-id="10e38-258">**ASP.NET**</span></span>

- <span data-ttu-id="10e38-259">ASP. NET\Requests Current</span><span class="sxs-lookup"><span data-stu-id="10e38-259">ASP.NET\Requests Current</span></span>
- <span data-ttu-id="10e38-260">NET\Queued</span><span class="sxs-lookup"><span data-stu-id="10e38-260">ASP.NET\Queued</span></span>
- <span data-ttu-id="10e38-261">NET\Rejected</span><span class="sxs-lookup"><span data-stu-id="10e38-261">ASP.NET\Rejected</span></span>

<span data-ttu-id="10e38-262">**CPU**</span><span class="sxs-lookup"><span data-stu-id="10e38-262">**CPU**</span></span>

- <span data-ttu-id="10e38-263">处理器 Information\Processor 时间</span><span class="sxs-lookup"><span data-stu-id="10e38-263">Processor Information\Processor Time</span></span>

<span data-ttu-id="10e38-264">**TCP/IP**</span><span class="sxs-lookup"><span data-stu-id="10e38-264">**TCP/IP**</span></span>

- <span data-ttu-id="10e38-265">已建立 TCPv6/连接</span><span class="sxs-lookup"><span data-stu-id="10e38-265">TCPv6/Connections Established</span></span>
- <span data-ttu-id="10e38-266">已建立 TCPv4/连接</span><span class="sxs-lookup"><span data-stu-id="10e38-266">TCPv4/Connections Established</span></span>

<span data-ttu-id="10e38-267">**Web 服务**</span><span class="sxs-lookup"><span data-stu-id="10e38-267">**Web Service**</span></span>

- <span data-ttu-id="10e38-268">Web Service\current connections 连接</span><span class="sxs-lookup"><span data-stu-id="10e38-268">Web Service\Current Connections</span></span>
- <span data-ttu-id="10e38-269">Web Service\Maximum 连接</span><span class="sxs-lookup"><span data-stu-id="10e38-269">Web Service\Maximum Connections</span></span>

<span data-ttu-id="10e38-270">**线程处理**</span><span class="sxs-lookup"><span data-stu-id="10e38-270">**Threading**</span></span>

- <span data-ttu-id="10e38-271">.NET CLR 锁和线程 \\ # 个当前逻辑线程</span><span class="sxs-lookup"><span data-stu-id="10e38-271">.NET CLR Locks And Threads\\# of current logical Threads</span></span>
- <span data-ttu-id="10e38-272">.NET CLR 锁和线程 \\ # 个当前物理线程</span><span class="sxs-lookup"><span data-stu-id="10e38-272">.NET CLR Locks And Threads\\# of current physical Threads</span></span>

<a id="otherresources"></a>

## <a name="other-resources"></a><span data-ttu-id="10e38-273">其他资源</span><span class="sxs-lookup"><span data-stu-id="10e38-273">Other Resources</span></span>

<span data-ttu-id="10e38-274">有关 ASP.NET 性能监视和优化的详细信息，请参阅以下主题：</span><span class="sxs-lookup"><span data-stu-id="10e38-274">For more information on ASP.NET performance monitoring and tuning, see the following topics:</span></span>

- <span data-ttu-id="10e38-275">[ASP.NET 性能概述](https://msdn.microsoft.com/library/cc668225(v=vs.100).aspx)</span><span class="sxs-lookup"><span data-stu-id="10e38-275">[ASP.NET Performance Overview](https://msdn.microsoft.com/library/cc668225(v=vs.100).aspx)</span></span>
- [<span data-ttu-id="10e38-276">IIS 7.5、IIS 7.0 和 IIS 6.0 上的 ASP.NET 线程使用情况</span><span class="sxs-lookup"><span data-stu-id="10e38-276">ASP.NET Thread Usage on IIS 7.5, IIS 7.0, and IIS 6.0</span></span>](https://blogs.msdn.com/b/tmarq/archive/2007/07/21/asp-net-thread-usage-on-iis-7-0-and-6-0.aspx)
- [<span data-ttu-id="10e38-277">&lt;&gt; (Web 设置的 applicationPool 元素) </span><span class="sxs-lookup"><span data-stu-id="10e38-277">&lt;applicationPool&gt; Element (Web Settings)</span></span>](https://msdn.microsoft.com/library/dd560842.aspx)

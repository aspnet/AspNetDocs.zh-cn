---
uid: signalr/overview/guide-to-the-api/hubs-api-guide-net-client
title: 'ASP.NET SignalR 中心 API 指南-.NET 客户端 (c # ) |Microsoft Docs'
author: bradygaster
description: 本文档介绍了如何在 .NET 客户端中使用适用于 SignalR 版本2的中心 API，例如 Windows 应用商店 (WinRT) 、WPF、Silverlight 和缺点 .。。
ms.author: bradyg
ms.date: 01/15/2019
ms.assetid: 6d02d9f7-94e5-4140-9f51-5a6040f274f6
msc.legacyurl: /signalr/overview/guide-to-the-api/hubs-api-guide-net-client
msc.type: authoredcontent
ms.openlocfilehash: d3536f1c15cd7dad7cd660becf0577e5c131f707
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345553"
---
# <a name="aspnet-signalr-hubs-api-guide---net-client-c"></a><span data-ttu-id="89267-103">ASP.NET SignalR 中心 API 指南-.NET 客户端 (c # ) </span><span class="sxs-lookup"><span data-stu-id="89267-103">ASP.NET SignalR Hubs API Guide - .NET Client (C#)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="89267-104">本文档介绍了如何在 .NET 客户端中使用适用于 SignalR 版本2的中心 API，例如 Windows 应用商店 (WinRT) 、WPF、Silverlight 和控制台应用程序。</span><span class="sxs-lookup"><span data-stu-id="89267-104">This document provides an introduction to using the Hubs API for SignalR version 2 in .NET clients, such as Windows Store (WinRT), WPF, Silverlight, and console applications.</span></span>
>
> <span data-ttu-id="89267-105">通过 SignalR 中心 API，你可以 (Rpc) 从服务器连接到连接的客户端和从客户端到服务器的远程过程调用。</span><span class="sxs-lookup"><span data-stu-id="89267-105">The SignalR Hubs API enables you to make remote procedure calls (RPCs) from a server to connected clients and from clients to the server.</span></span> <span data-ttu-id="89267-106">在服务器代码中，你将定义可由客户端调用的方法，并调用在客户端上运行的方法。</span><span class="sxs-lookup"><span data-stu-id="89267-106">In server code, you define methods that can be called by clients, and you call methods that run on the client.</span></span> <span data-ttu-id="89267-107">在客户端代码中，定义可从服务器调用的方法，并调用在服务器上运行的方法。</span><span class="sxs-lookup"><span data-stu-id="89267-107">In client code, you define methods that can be called from the server, and you call methods that run on the server.</span></span> <span data-ttu-id="89267-108">SignalR 负责处理所有的客户端到服务器的操作。</span><span class="sxs-lookup"><span data-stu-id="89267-108">SignalR takes care of all of the client-to-server plumbing for you.</span></span>
>
> <span data-ttu-id="89267-109">SignalR 还提供名为持久性连接的较低级别 API。</span><span class="sxs-lookup"><span data-stu-id="89267-109">SignalR also offers a lower-level API called Persistent Connections.</span></span> <span data-ttu-id="89267-110">有关 SignalR、集线器和持久性连接的简介，或有关演示如何生成完整 SignalR 应用程序的教程，请参阅 [SignalR-入门](../getting-started/index.md)。</span><span class="sxs-lookup"><span data-stu-id="89267-110">For an introduction to SignalR, Hubs, and Persistent Connections, or for a tutorial that shows how to build a complete SignalR application, see [SignalR - Getting Started](../getting-started/index.md).</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="89267-111">本主题中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="89267-111">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="89267-112">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="89267-112">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/)
> - <span data-ttu-id="89267-113">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="89267-113">.NET 4.5</span></span>
> - <span data-ttu-id="89267-114">SignalR 版本2</span><span class="sxs-lookup"><span data-stu-id="89267-114">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="89267-115">本主题的早期版本</span><span class="sxs-lookup"><span data-stu-id="89267-115">Previous versions of this topic</span></span>
>
> <span data-ttu-id="89267-116">有关早期版本的 SignalR 的信息，请参阅 [SignalR 旧版本](../older-versions/index.md)。</span><span class="sxs-lookup"><span data-stu-id="89267-116">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="89267-117">问题和注释</span><span class="sxs-lookup"><span data-stu-id="89267-117">Questions and comments</span></span>
>
> <span data-ttu-id="89267-118">请提供有关你喜欢本教程的方式的反馈，并在页面底部的评论中留下反馈。</span><span class="sxs-lookup"><span data-stu-id="89267-118">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="89267-119">如果你有与本教程不直接相关的问题，则可以将其发布到 [ASP.NET SignalR 论坛](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 或 [StackOverflow.com](http://stackoverflow.com/)。</span><span class="sxs-lookup"><span data-stu-id="89267-119">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="overview"></a><span data-ttu-id="89267-120">概述</span><span class="sxs-lookup"><span data-stu-id="89267-120">Overview</span></span>

<span data-ttu-id="89267-121">本文档包含以下各节：</span><span class="sxs-lookup"><span data-stu-id="89267-121">This document contains the following sections:</span></span>

- [<span data-ttu-id="89267-122">客户端设置</span><span class="sxs-lookup"><span data-stu-id="89267-122">Client Setup</span></span>](#clientsetup)
- [<span data-ttu-id="89267-123">如何建立连接</span><span class="sxs-lookup"><span data-stu-id="89267-123">How to establish a connection</span></span>](#establishconnection)

    - [<span data-ttu-id="89267-124">来自 Silverlight 客户端的跨域连接</span><span class="sxs-lookup"><span data-stu-id="89267-124">Cross-domain connections from Silverlight clients</span></span>](#slcrossdomain)
- [<span data-ttu-id="89267-125">如何配置连接</span><span class="sxs-lookup"><span data-stu-id="89267-125">How to configure the connection</span></span>](#configureconnection)

    - [<span data-ttu-id="89267-126">如何设置 WPF 客户端中的最大并发连接数</span><span class="sxs-lookup"><span data-stu-id="89267-126">How to set the maximum number of concurrent connections in WPF clients</span></span>](#maxconnections)
    - [<span data-ttu-id="89267-127">如何指定查询字符串参数</span><span class="sxs-lookup"><span data-stu-id="89267-127">How to specify query string parameters</span></span>](#querystring)
    - [<span data-ttu-id="89267-128">如何指定传输方法</span><span class="sxs-lookup"><span data-stu-id="89267-128">How to specify the transport method</span></span>](#transport)
    - [<span data-ttu-id="89267-129">如何指定 HTTP 标头</span><span class="sxs-lookup"><span data-stu-id="89267-129">How to specify HTTP headers</span></span>](#httpheaders)
    - [<span data-ttu-id="89267-130">如何指定客户端证书</span><span class="sxs-lookup"><span data-stu-id="89267-130">How to specify client certificates</span></span>](#clientcertificate)
- [<span data-ttu-id="89267-131">如何创建中心代理</span><span class="sxs-lookup"><span data-stu-id="89267-131">How to create the Hub proxy</span></span>](#proxy)
- [<span data-ttu-id="89267-132">如何在客户端上定义服务器可以调用的方法</span><span class="sxs-lookup"><span data-stu-id="89267-132">How to define methods on the client that the server can call</span></span>](#callclient)

    - [<span data-ttu-id="89267-133">不带参数的方法</span><span class="sxs-lookup"><span data-stu-id="89267-133">Methods without parameters</span></span>](#clientmethodswithoutparms)
    - [<span data-ttu-id="89267-134">带参数的方法，指定参数类型</span><span class="sxs-lookup"><span data-stu-id="89267-134">Methods with parameters, specifying parameter types</span></span>](#clientmethodswithparmtypes)
    - [<span data-ttu-id="89267-135">带参数的方法，指定参数的动态对象</span><span class="sxs-lookup"><span data-stu-id="89267-135">Methods with parameters, specifying dynamic objects for the parameters</span></span>](#clientmethodswithdynamparms)
    - [<span data-ttu-id="89267-136">如何删除处理程序</span><span class="sxs-lookup"><span data-stu-id="89267-136">How to remove a handler</span></span>](#removehandler)
- [<span data-ttu-id="89267-137">如何从客户端调用服务器方法</span><span class="sxs-lookup"><span data-stu-id="89267-137">How to call server methods from the client</span></span>](#callserver)
- [<span data-ttu-id="89267-138">如何处理连接生存期事件</span><span class="sxs-lookup"><span data-stu-id="89267-138">How to handle connection lifetime events</span></span>](#connectionlifetime)
- [<span data-ttu-id="89267-139">如何处理错误</span><span class="sxs-lookup"><span data-stu-id="89267-139">How to handle errors</span></span>](#handleerrors)
- [<span data-ttu-id="89267-140">如何启用客户端日志记录</span><span class="sxs-lookup"><span data-stu-id="89267-140">How to enable client-side logging</span></span>](#logging)
- [<span data-ttu-id="89267-141">服务器可以调用的客户端方法的 WPF、Silverlight 和控制台应用程序代码示例</span><span class="sxs-lookup"><span data-stu-id="89267-141">WPF, Silverlight, and console application code samples for client methods that the server can call</span></span>](#wpfsl)

<span data-ttu-id="89267-142">对于 .NET 客户端项目示例，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="89267-142">For a sample .NET client projects, see the following resources:</span></span>

- <span data-ttu-id="89267-143">[gustavo-GitHub.com 上的 armenta/SignalR](https://github.com/gustavo-armenta/SignalR-Samples) (WinRT、Silverlight、控制台应用程序示例) 。</span><span class="sxs-lookup"><span data-stu-id="89267-143">[gustavo-armenta / SignalR-Samples](https://github.com/gustavo-armenta/SignalR-Samples) on GitHub.com (WinRT, Silverlight, console app examples).</span></span>
- <span data-ttu-id="89267-144">GitHub.com 上的[DamianEdwards/SignalR-MoveShapeDemo/MoveShape](https://github.com/DamianEdwards/SignalR-MoveShapeDemo/tree/master/MoveShape/MoveShape.Desktop) (WPF 示例) 。</span><span class="sxs-lookup"><span data-stu-id="89267-144">[DamianEdwards / SignalR-MoveShapeDemo / MoveShape.Desktop](https://github.com/DamianEdwards/SignalR-MoveShapeDemo/tree/master/MoveShape/MoveShape.Desktop) on GitHub.com (WPF example).</span></span>
- <span data-ttu-id="89267-145">GitHub.com 上的[SignalR/SignalR](https://github.com/SignalR/SignalR/tree/master/samples/Microsoft.AspNet.SignalR.Client.Samples) (控制台应用程序示例) 。</span><span class="sxs-lookup"><span data-stu-id="89267-145">[SignalR / Microsoft.AspNet.SignalR.Client.Samples](https://github.com/SignalR/SignalR/tree/master/samples/Microsoft.AspNet.SignalR.Client.Samples) on GitHub.com (Console app example).</span></span>

<span data-ttu-id="89267-146">有关如何对服务器或 JavaScript 客户端进行编程的文档，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="89267-146">For documentation on how to program the server or JavaScript clients, see the following resources:</span></span>

- [<span data-ttu-id="89267-147">SignalR 中心 API 指南-服务器</span><span class="sxs-lookup"><span data-stu-id="89267-147">SignalR Hubs API Guide - Server</span></span>](hubs-api-guide-server.md)
- [<span data-ttu-id="89267-148">SignalR 中心 API 指南-JavaScript 客户端</span><span class="sxs-lookup"><span data-stu-id="89267-148">SignalR Hubs API Guide - JavaScript Client</span></span>](hubs-api-guide-javascript-client.md)

<span data-ttu-id="89267-149">API 参考主题的链接适用于 .NET 4.5 版本的 API。</span><span class="sxs-lookup"><span data-stu-id="89267-149">Links to API Reference topics are to the .NET 4.5 version of the API.</span></span> <span data-ttu-id="89267-150">如果使用的是 .NET 4，请参阅 [.net 4 版本的 API 主题](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx)。</span><span class="sxs-lookup"><span data-stu-id="89267-150">If you're using .NET 4, see [the .NET 4 version of the API topics](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx).</span></span>

<a id="clientsetup"></a>

## <a name="client-setup"></a><span data-ttu-id="89267-151">客户端设置</span><span class="sxs-lookup"><span data-stu-id="89267-151">Client setup</span></span>

<span data-ttu-id="89267-152">安装 [SignalR](http://nuget.org/packages/Microsoft.AspNet.SignalR.Client) NuGet 包， (不是 [SignalR](http://nuget.org/packages/microsoft.aspnet.signalr) 包) 的。</span><span class="sxs-lookup"><span data-stu-id="89267-152">Install the [Microsoft.AspNet.SignalR.Client](http://nuget.org/packages/Microsoft.AspNet.SignalR.Client) NuGet package (not the [Microsoft.AspNet.SignalR](http://nuget.org/packages/microsoft.aspnet.signalr) package).</span></span> <span data-ttu-id="89267-153">对于 .NET 4 和 .NET 4.5，此包支持 WinRT、Silverlight、WPF、控制台应用程序和 Windows Phone 客户端。</span><span class="sxs-lookup"><span data-stu-id="89267-153">This package supports WinRT, Silverlight, WPF, console application, and Windows Phone clients, for both .NET 4 and .NET 4.5.</span></span>

<span data-ttu-id="89267-154">如果客户端上的 SignalR 版本与服务器上的版本不同，则 SignalR 通常能够适应不同之处。</span><span class="sxs-lookup"><span data-stu-id="89267-154">If the version of SignalR that you have on the client is different from the version that you have on the server, SignalR is often able to adapt to the difference.</span></span> <span data-ttu-id="89267-155">例如，运行 SignalR 版本2的服务器将支持安装了 1.1. x 的客户端，以及安装了版本2的客户端。</span><span class="sxs-lookup"><span data-stu-id="89267-155">For example, a server running SignalR version 2 will support clients that have 1.1.x installed as well as clients that have version 2 installed.</span></span> <span data-ttu-id="89267-156">如果服务器上的版本与客户端上的版本之间的差异太大，或者客户端比服务器更新，则 `InvalidOperationException` 当客户端尝试建立连接时，SignalR 将引发异常。</span><span class="sxs-lookup"><span data-stu-id="89267-156">If the difference between the version on the server and the version on the client is too great, or if the client is newer than the server, SignalR throws an `InvalidOperationException` exception when the client tries to establish a connection.</span></span> <span data-ttu-id="89267-157">错误消息为 " `You are using a version of the client that isn't compatible with the server. Client version X.X, server version X.X` "。</span><span class="sxs-lookup"><span data-stu-id="89267-157">The error message is "`You are using a version of the client that isn't compatible with the server. Client version X.X, server version X.X`".</span></span>

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a><span data-ttu-id="89267-158">如何建立连接</span><span class="sxs-lookup"><span data-stu-id="89267-158">How to establish a connection</span></span>

<span data-ttu-id="89267-159">建立连接之前，必须先创建 `HubConnection` 对象并创建代理。</span><span class="sxs-lookup"><span data-stu-id="89267-159">Before you can establish a connection, you have to create a `HubConnection` object and create a proxy.</span></span> <span data-ttu-id="89267-160">若要建立连接，请对 `Start` 对象调用方法 `HubConnection` 。</span><span class="sxs-lookup"><span data-stu-id="89267-160">To establish the connection, call the `Start` method on the `HubConnection` object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample1.cs?highlight=1,5)]

> [!NOTE]
> <span data-ttu-id="89267-161">对于 JavaScript 客户端，必须在调用方法之前注册至少一个事件处理程序 `Start` 以建立连接。</span><span class="sxs-lookup"><span data-stu-id="89267-161">For JavaScript clients you have to register at least one event handler before calling the `Start` method to establish the connection.</span></span> <span data-ttu-id="89267-162">这不是 .NET 客户端所必需的。</span><span class="sxs-lookup"><span data-stu-id="89267-162">This is not necessary for .NET clients.</span></span> <span data-ttu-id="89267-163">对于 JavaScript 客户端，生成的代理代码会自动为服务器上存在的所有中心创建代理，并注册处理程序，以指示客户端打算使用哪些集线器。</span><span class="sxs-lookup"><span data-stu-id="89267-163">For JavaScript clients, the generated proxy code automatically creates proxies for all Hubs that exist on the server, and registering a handler is how you indicate which Hubs your client intends to use.</span></span> <span data-ttu-id="89267-164">但对于 .NET 客户端，你可以手动创建中心代理，因此 SignalR 假定你将使用为创建代理的任何集线器。</span><span class="sxs-lookup"><span data-stu-id="89267-164">But for a .NET client you create Hub proxies manually, so SignalR assumes that you will be using any Hub that you create a proxy for.</span></span>

<span data-ttu-id="89267-165">示例代码使用默认的 "/signalr" URL 连接到 SignalR 服务。</span><span class="sxs-lookup"><span data-stu-id="89267-165">The sample code uses the default "/signalr" URL to connect to your SignalR service.</span></span> <span data-ttu-id="89267-166">有关如何指定其他基 URL 的信息，请参阅 [ASP.NET SignalR HUB API 指南-Server-/SIGNALR URL](hubs-api-guide-server.md#signalrurl)。</span><span class="sxs-lookup"><span data-stu-id="89267-166">For information about how to specify a different base URL, see [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](hubs-api-guide-server.md#signalrurl).</span></span>

<span data-ttu-id="89267-167">`Start`方法以异步方式执行。</span><span class="sxs-lookup"><span data-stu-id="89267-167">The `Start` method executes asynchronously.</span></span> <span data-ttu-id="89267-168">若要确保后续代码行在建立连接之前不会执行，请 `await` 在 ASP.NET 4.5 异步方法或同步方法中使用 `.Wait()` 。</span><span class="sxs-lookup"><span data-stu-id="89267-168">To make sure that subsequent lines of code don't execute until after the connection is established, use `await` in an ASP.NET 4.5 asynchronous method or `.Wait()` in a synchronous method.</span></span> <span data-ttu-id="89267-169">请勿 `.Wait()` 在 WinRT 客户端中使用。</span><span class="sxs-lookup"><span data-stu-id="89267-169">Don't use `.Wait()` in a WinRT client.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample2.cs?highlight=1)]

[!code-css[Main](hubs-api-guide-net-client/samples/sample3.css?highlight=1)]

<a id="slcrossdomain"></a>

### <a name="cross-domain-connections-from-silverlight-clients"></a><span data-ttu-id="89267-170">来自 Silverlight 客户端的跨域连接</span><span class="sxs-lookup"><span data-stu-id="89267-170">Cross-domain connections from Silverlight clients</span></span>

<span data-ttu-id="89267-171">有关如何从 Silverlight 客户端启用跨域连接的信息，请参阅 [使服务跨域边界可用](https://msdn.microsoft.com/library/cc197955(v=vs.95).aspx)。</span><span class="sxs-lookup"><span data-stu-id="89267-171">For information about how to enable cross-domain connections from Silverlight clients, see [Making a Service Available Across Domain Boundaries](https://msdn.microsoft.com/library/cc197955(v=vs.95).aspx).</span></span>

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a><span data-ttu-id="89267-172">如何配置连接</span><span class="sxs-lookup"><span data-stu-id="89267-172">How to configure the connection</span></span>

<span data-ttu-id="89267-173">在建立连接之前，您可以指定以下任一选项：</span><span class="sxs-lookup"><span data-stu-id="89267-173">Before you establish a connection, you can specify any of the following options:</span></span>

- <span data-ttu-id="89267-174">并发连接限制。</span><span class="sxs-lookup"><span data-stu-id="89267-174">Concurrent connections limit.</span></span>
- <span data-ttu-id="89267-175">查询字符串参数。</span><span class="sxs-lookup"><span data-stu-id="89267-175">Query string parameters.</span></span>
- <span data-ttu-id="89267-176">传输方法。</span><span class="sxs-lookup"><span data-stu-id="89267-176">The transport method.</span></span>
- <span data-ttu-id="89267-177">HTTP 标头。</span><span class="sxs-lookup"><span data-stu-id="89267-177">HTTP headers.</span></span>
- <span data-ttu-id="89267-178">客户端证书。</span><span class="sxs-lookup"><span data-stu-id="89267-178">Client certificates.</span></span>

<a id="maxconnections"></a>

### <a name="how-to-set-the-maximum-number-of-concurrent-connections-in-wpf-clients"></a><span data-ttu-id="89267-179">如何设置 WPF 客户端中的最大并发连接数</span><span class="sxs-lookup"><span data-stu-id="89267-179">How to set the maximum number of concurrent connections in WPF clients</span></span>

<span data-ttu-id="89267-180">在 WPF 客户端中，你可能必须将最大并发连接数从其默认值2增加到最大值。</span><span class="sxs-lookup"><span data-stu-id="89267-180">In WPF clients, you might have to increase the maximum number of concurrent connections from its default value of 2.</span></span> <span data-ttu-id="89267-181">建议值为10。</span><span class="sxs-lookup"><span data-stu-id="89267-181">The recommended value is 10.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample4.cs?highlight=5)]

<span data-ttu-id="89267-182">有关详细信息，请参阅 [ServicePointManager. servicepointmanager.defaultconnectionlimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx)。</span><span class="sxs-lookup"><span data-stu-id="89267-182">For more information, see [ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx).</span></span>

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a><span data-ttu-id="89267-183">如何指定查询字符串参数</span><span class="sxs-lookup"><span data-stu-id="89267-183">How to specify query string parameters</span></span>

<span data-ttu-id="89267-184">如果要在客户端连接时将数据发送到服务器，则可以将查询字符串参数添加到连接对象。</span><span class="sxs-lookup"><span data-stu-id="89267-184">If you want to send data to the server when the client connects, you can add query string parameters to the connection object.</span></span> <span data-ttu-id="89267-185">下面的示例演示如何在客户端代码中设置查询字符串参数。</span><span class="sxs-lookup"><span data-stu-id="89267-185">The following example shows how to set a query string parameter in client code.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample5.cs)]

<span data-ttu-id="89267-186">下面的示例演示如何读取服务器代码中的查询字符串参数。</span><span class="sxs-lookup"><span data-stu-id="89267-186">The following example shows how to read a query string parameter in server code.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample6.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a><span data-ttu-id="89267-187">如何指定传输方法</span><span class="sxs-lookup"><span data-stu-id="89267-187">How to specify the transport method</span></span>

<span data-ttu-id="89267-188">作为连接过程的一部分，SignalR 客户端通常与服务器协商以确定服务器和客户端支持的最佳传输。</span><span class="sxs-lookup"><span data-stu-id="89267-188">As part of the process of connecting, a SignalR client normally negotiates with the server to determine the best transport that is supported by both server and client.</span></span> <span data-ttu-id="89267-189">如果已知道要使用的传输，可以绕过此协商过程。</span><span class="sxs-lookup"><span data-stu-id="89267-189">If you already know which transport you want to use, you can bypass this negotiation process.</span></span> <span data-ttu-id="89267-190">若要指定传输方法，请将传输对象传入到 Start 方法。</span><span class="sxs-lookup"><span data-stu-id="89267-190">To specify the transport method, pass in a transport object to the Start method.</span></span> <span data-ttu-id="89267-191">下面的示例演示如何在客户端代码中指定传输方法。</span><span class="sxs-lookup"><span data-stu-id="89267-191">The following example shows how to specify the transport method in client code.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample7.cs?highlight=5)]

<span data-ttu-id="89267-192">[SignalR](https://msdn.microsoft.com/library/jj918090(v=vs.111).aspx)命名空间包含可用于指定传输的以下类。 "的命名空间可用于指定传输。</span><span class="sxs-lookup"><span data-stu-id="89267-192">The [Microsoft.AspNet.SignalR.Client.Transports](https://msdn.microsoft.com/library/jj918090(v=vs.111).aspx) namespace includes the following classes that you can use to specify the transport.</span></span>

- <span data-ttu-id="89267-193">[LongPollingTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.longpollingtransport(v=vs.111).aspx)</span><span class="sxs-lookup"><span data-stu-id="89267-193">[LongPollingTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.longpollingtransport(v=vs.111).aspx)</span></span>
- <span data-ttu-id="89267-194">[ServerSentEventsTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.serversenteventstransport(v=vs.111).aspx)</span><span class="sxs-lookup"><span data-stu-id="89267-194">[ServerSentEventsTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.serversenteventstransport(v=vs.111).aspx)</span></span>
- <span data-ttu-id="89267-195">只有服务器和客户端都使用 .NET 4.5 时， [WebSocketTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.websockettransport(v=vs.111).aspx) (才可用。 ) </span><span class="sxs-lookup"><span data-stu-id="89267-195">[WebSocketTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.websockettransport(v=vs.111).aspx) (Available only when both server and client use .NET 4.5.)</span></span>
- <span data-ttu-id="89267-196">[AutoTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.autotransport(v=vs.111).aspx) (自动选择客户端和服务器支持的最佳传输。</span><span class="sxs-lookup"><span data-stu-id="89267-196">[AutoTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.autotransport(v=vs.111).aspx) (Automatically chooses the best transport that is supported by both the client and the server.</span></span> <span data-ttu-id="89267-197">这是默认传输。</span><span class="sxs-lookup"><span data-stu-id="89267-197">This is the default transport.</span></span> <span data-ttu-id="89267-198">将此传入到 `Start` 方法与不传入任何内容相同。 ) </span><span class="sxs-lookup"><span data-stu-id="89267-198">Passing this in to the `Start` method has the same effect as not passing in anything.)</span></span>

<span data-ttu-id="89267-199">此列表中不包含 ForeverFrame 传输，因为它仅由浏览器使用。</span><span class="sxs-lookup"><span data-stu-id="89267-199">The ForeverFrame transport is not included in this list because it is used only by browsers.</span></span>

<span data-ttu-id="89267-200">有关如何在服务器代码中检查传输方法的信息，请参阅 [ASP.NET SignalR HUB API 指南-服务器-如何从上下文属性获取有关客户端的信息](hubs-api-guide-server.md#contextproperty)。</span><span class="sxs-lookup"><span data-stu-id="89267-200">For information about how to check the transport method in server code, see [ASP.NET SignalR Hubs API Guide - Server - How to get information about the client from the Context property](hubs-api-guide-server.md#contextproperty).</span></span> <span data-ttu-id="89267-201">有关传输和回退的详细信息，请参阅 [SignalR-传输和回退简介](../getting-started/introduction-to-signalr.md#transports)。</span><span class="sxs-lookup"><span data-stu-id="89267-201">For more information about transports and fallbacks, see [Introduction to SignalR - Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span>

<a id="httpheaders"></a>

### <a name="how-to-specify-http-headers"></a><span data-ttu-id="89267-202">如何指定 HTTP 标头</span><span class="sxs-lookup"><span data-stu-id="89267-202">How to specify HTTP headers</span></span>

<span data-ttu-id="89267-203">若要设置 HTTP 标头，请 `Headers` 在连接对象上使用属性。</span><span class="sxs-lookup"><span data-stu-id="89267-203">To set HTTP headers, use the `Headers` property on the connection object.</span></span> <span data-ttu-id="89267-204">下面的示例演示如何添加 HTTP 标头。</span><span class="sxs-lookup"><span data-stu-id="89267-204">The following example shows how to add an HTTP header.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample8.cs?highlight=2)]

<a id="clientcertificate"></a>

### <a name="how-to-specify-client-certificates"></a><span data-ttu-id="89267-205">如何指定客户端证书</span><span class="sxs-lookup"><span data-stu-id="89267-205">How to specify client certificates</span></span>

<span data-ttu-id="89267-206">若要添加客户端证书，请 `AddClientCertificate` 对连接对象使用方法。</span><span class="sxs-lookup"><span data-stu-id="89267-206">To add client certificates, use the `AddClientCertificate` method on the connection object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample9.cs?highlight=2)]

<a id="proxy"></a>

## <a name="how-to-create-the-hub-proxy"></a><span data-ttu-id="89267-207">如何创建中心代理</span><span class="sxs-lookup"><span data-stu-id="89267-207">How to create the Hub proxy</span></span>

<span data-ttu-id="89267-208">若要在客户端上定义集线器可以从服务器调用的方法，并在服务器上调用集线器上的方法，请通过对连接对象调用来创建中心的代理 `CreateHubProxy` 。</span><span class="sxs-lookup"><span data-stu-id="89267-208">In order to define methods on the client that a Hub can call from the server, and to invoke methods on a Hub at the server, create a proxy for the Hub by calling `CreateHubProxy` on the connection object.</span></span> <span data-ttu-id="89267-209">传递给的字符串 `CreateHubProxy` 是中心类的名称，或属性指定的名称（ `HubName` 如果服务器上使用了一个名称）。</span><span class="sxs-lookup"><span data-stu-id="89267-209">The string you pass in to `CreateHubProxy` is the name of your Hub class, or the name specified by the `HubName` attribute if one was used on the server.</span></span> <span data-ttu-id="89267-210">名称匹配不区分大小写。</span><span class="sxs-lookup"><span data-stu-id="89267-210">Name matching is case-insensitive.</span></span>

<span data-ttu-id="89267-211">**服务器上的中心类**</span><span class="sxs-lookup"><span data-stu-id="89267-211">**Hub class on server**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample10.cs?highlight=1)]

<span data-ttu-id="89267-212">**创建中心类的客户端代理**</span><span class="sxs-lookup"><span data-stu-id="89267-212">**Create client proxy for the Hub class**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample11.cs?highlight=3)]

<span data-ttu-id="89267-213">如果使用属性修饰中心类 `HubName` ，请使用该名称。</span><span class="sxs-lookup"><span data-stu-id="89267-213">If you decorate your Hub class with a `HubName` attribute, use that name.</span></span>

<span data-ttu-id="89267-214">**服务器上的中心类**</span><span class="sxs-lookup"><span data-stu-id="89267-214">**Hub class on server**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample12.cs)]

<span data-ttu-id="89267-215">**创建中心类的客户端代理**</span><span class="sxs-lookup"><span data-stu-id="89267-215">**Create client proxy for the Hub class**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample13.cs?highlight=3)]

<span data-ttu-id="89267-216">如果多次调用 `HubConnection.CreateHubProxy` 相同的 `hubName` ，则会获得相同的缓存 `IHubProxy` 对象。</span><span class="sxs-lookup"><span data-stu-id="89267-216">If you call `HubConnection.CreateHubProxy` multiple times with the same `hubName`, you get the same cached `IHubProxy` object.</span></span>

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a><span data-ttu-id="89267-217">如何在客户端上定义服务器可以调用的方法</span><span class="sxs-lookup"><span data-stu-id="89267-217">How to define methods on the client that the server can call</span></span>

<span data-ttu-id="89267-218">若要定义服务器可以调用的方法，请使用代理的 `On` 方法注册事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="89267-218">To define a method that the server can call, use the proxy's `On` method to register an event handler.</span></span>

<span data-ttu-id="89267-219">方法名称匹配不区分大小写。</span><span class="sxs-lookup"><span data-stu-id="89267-219">Method name matching is case-insensitive.</span></span> <span data-ttu-id="89267-220">例如， `Clients.All.UpdateStockPrice` 在服务器上，将在 `updateStockPrice` 客户端上执行、 `updatestockprice` 或 `UpdateStockPrice` 。</span><span class="sxs-lookup"><span data-stu-id="89267-220">For example, `Clients.All.UpdateStockPrice` on the server will execute `updateStockPrice`, `updatestockprice`, or `UpdateStockPrice` on the client.</span></span>

<span data-ttu-id="89267-221">不同的客户端平台对于你编写方法代码以更新 UI 的方式有不同的要求。</span><span class="sxs-lookup"><span data-stu-id="89267-221">Different client platforms have different requirements for how you write method code to update the UI.</span></span> <span data-ttu-id="89267-222">显示的示例适用于 WinRT (Windows 应用商店 .NET) 客户端。</span><span class="sxs-lookup"><span data-stu-id="89267-222">The examples shown are for WinRT (Windows Store .NET) clients.</span></span> <span data-ttu-id="89267-223">WPF、Silverlight 和控制台应用程序示例在 [本主题后面的单独章节](#wpfsl)中提供。</span><span class="sxs-lookup"><span data-stu-id="89267-223">WPF, Silverlight, and console application examples are provided in [a separate section later in this topic](#wpfsl).</span></span>

<a id="clientmethodswithoutparms"></a>

### <a name="methods-without-parameters"></a><span data-ttu-id="89267-224">不带参数的方法</span><span class="sxs-lookup"><span data-stu-id="89267-224">Methods without parameters</span></span>

<span data-ttu-id="89267-225">如果正在处理的方法没有参数，请使用方法的非泛型重载 `On` ：</span><span class="sxs-lookup"><span data-stu-id="89267-225">If the method you're handling does not have parameters, use the non-generic overload of the `On` method:</span></span>

<span data-ttu-id="89267-226">**调用不带参数的客户端方法的服务器代码**</span><span class="sxs-lookup"><span data-stu-id="89267-226">**Server code calling client method without parameters**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample14.cs?highlight=5)]

<span data-ttu-id="89267-227">\*\*从没有参数的服务器中调用的方法的 WinRT 客户端代码 ([参阅本主题后面的 WPF 和 Silverlight 示例](#wpfsl)) \*\*</span><span class="sxs-lookup"><span data-stu-id="89267-227">**WinRT Client code for method called from server without parameters ([see WPF and Silverlight examples later in this topic](#wpfsl))**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample15.cs)]

<a id="clientmethodswithparmtypes"></a>

### <a name="methods-with-parameters-specifying-the-parameter-types"></a><span data-ttu-id="89267-228">带参数的方法，指定参数类型</span><span class="sxs-lookup"><span data-stu-id="89267-228">Methods with parameters, specifying the parameter types</span></span>

<span data-ttu-id="89267-229">如果正在处理的方法具有参数，请将参数的类型指定为方法的泛型类型 `On` 。</span><span class="sxs-lookup"><span data-stu-id="89267-229">If the method you're handling has parameters, specify the types of the parameters as the generic types of the `On` method.</span></span> <span data-ttu-id="89267-230">方法的泛型重载 `On` 使你能够在 Windows Phone 7) 上最多 (4 指定8个参数。</span><span class="sxs-lookup"><span data-stu-id="89267-230">There are generic overloads of the `On` method to enable you to specify up to 8 parameters (4 on Windows Phone 7).</span></span> <span data-ttu-id="89267-231">在下面的示例中，向方法发送一个参数 `UpdateStockPrice` 。</span><span class="sxs-lookup"><span data-stu-id="89267-231">In the following example, one parameter is sent to the `UpdateStockPrice` method.</span></span>

<span data-ttu-id="89267-232">**使用参数调用客户端方法的服务器代码**</span><span class="sxs-lookup"><span data-stu-id="89267-232">**Server code calling client method with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample16.cs?highlight=3)]

<span data-ttu-id="89267-233">**用于参数的 Stock 类**</span><span class="sxs-lookup"><span data-stu-id="89267-233">**The Stock class used for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample17.cs)]

<span data-ttu-id="89267-234">\*\*从具有参数的服务器中调用的方法的 WinRT 客户端代码 ([参阅本主题后面的 WPF 和 Silverlight 示例](#wpfsl)) \*\*</span><span class="sxs-lookup"><span data-stu-id="89267-234">**WinRT Client code for a method called from server with a parameter ([see WPF and Silverlight examples later in this topic](#wpfsl))**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample18.cs?highlight=1,5)]

<a id="clientmethodswithdynamparms"></a>

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a><span data-ttu-id="89267-235">带参数的方法，指定参数的动态对象</span><span class="sxs-lookup"><span data-stu-id="89267-235">Methods with parameters, specifying dynamic objects for the parameters</span></span>

<span data-ttu-id="89267-236">作为将参数指定为方法的泛型类型的替代 `On` 方法，可以将参数指定为动态对象：</span><span class="sxs-lookup"><span data-stu-id="89267-236">As an alternative to specifying parameters as generic types of the `On` method, you can specify parameters as dynamic objects:</span></span>

<span data-ttu-id="89267-237">**使用参数调用客户端方法的服务器代码**</span><span class="sxs-lookup"><span data-stu-id="89267-237">**Server code calling client method with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample19.cs?highlight=3)]

<span data-ttu-id="89267-238">**用于参数的 Stock 类**</span><span class="sxs-lookup"><span data-stu-id="89267-238">**The Stock class used for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample20.cs)]

<span data-ttu-id="89267-239">\*\*从具有参数的服务器中调用的方法的 WinRT 客户端代码，对参数使用动态对象 ([参阅本主题后面的 WPF 和 Silverlight 示例](#wpfsl)) \*\*</span><span class="sxs-lookup"><span data-stu-id="89267-239">**WinRT Client code for a method called from server with a parameter, using a dynamic object for the parameter ([see WPF and Silverlight examples later in this topic](#wpfsl))**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample21.cs?highlight=1,5)]

<a id="removehandler"></a>

### <a name="how-to-remove-a-handler"></a><span data-ttu-id="89267-240">如何删除处理程序</span><span class="sxs-lookup"><span data-stu-id="89267-240">How to remove a handler</span></span>

<span data-ttu-id="89267-241">若要删除处理程序，请调用其 `Dispose` 方法。</span><span class="sxs-lookup"><span data-stu-id="89267-241">To remove a handler, call its `Dispose` method.</span></span>

<span data-ttu-id="89267-242">**从服务器调用的方法的客户端代码**</span><span class="sxs-lookup"><span data-stu-id="89267-242">**Client code for a method called from server**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample22.cs?highlight=1)]

<span data-ttu-id="89267-243">**用于删除处理程序的客户端代码**</span><span class="sxs-lookup"><span data-stu-id="89267-243">**Client code to remove the handler**</span></span>

[!code-css[Main](hubs-api-guide-net-client/samples/sample23.css?highlight=1)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a><span data-ttu-id="89267-244">如何从客户端调用服务器方法</span><span class="sxs-lookup"><span data-stu-id="89267-244">How to call server methods from the client</span></span>

<span data-ttu-id="89267-245">若要在服务器上调用方法，请 `Invoke` 在中心代理上使用方法。</span><span class="sxs-lookup"><span data-stu-id="89267-245">To call a method on the server, use the `Invoke` method on the Hub proxy.</span></span>

<span data-ttu-id="89267-246">如果服务器方法没有返回值，请使用方法的非泛型重载 `Invoke` 。</span><span class="sxs-lookup"><span data-stu-id="89267-246">If the server method has no return value, use the non-generic overload of the `Invoke` method.</span></span>

<span data-ttu-id="89267-247">**没有返回值的方法的服务器代码**</span><span class="sxs-lookup"><span data-stu-id="89267-247">**Server code for a method that has no return value**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample24.cs?highlight=3)]

<span data-ttu-id="89267-248">**调用没有返回值的方法的客户端代码**</span><span class="sxs-lookup"><span data-stu-id="89267-248">**Client code calling a method that has no return value**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample25.cs?highlight=1)]

<span data-ttu-id="89267-249">如果服务器方法具有返回值，则将返回类型指定为方法的泛型类型 `Invoke` 。</span><span class="sxs-lookup"><span data-stu-id="89267-249">If the server method has a return value, specify the return type as the generic type of the `Invoke` method.</span></span>

<span data-ttu-id="89267-250">**具有返回值并采用复杂类型参数的方法的服务器代码**</span><span class="sxs-lookup"><span data-stu-id="89267-250">**Server code for a method that has a return value and takes a complex type parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample26.cs?highlight=1)]

<span data-ttu-id="89267-251">**用于参数和返回值的 Stock 类**</span><span class="sxs-lookup"><span data-stu-id="89267-251">**The Stock class used for the parameter and return value**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample27.cs)]

<span data-ttu-id="89267-252">**在 ASP.NET 4.5 异步方法中调用具有返回值并采用复杂类型参数的方法的客户端代码**</span><span class="sxs-lookup"><span data-stu-id="89267-252">**Client code calling a method that has a return value and takes a complex type parameter, in an ASP.NET 4.5 async method**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample28.cs?highlight=1-2)]

<span data-ttu-id="89267-253">**在同步方法中调用具有返回值并采用复杂类型参数的方法的客户端代码**</span><span class="sxs-lookup"><span data-stu-id="89267-253">**Client code calling a method that has a return value and takes a complex type parameter, in a synchronous method**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample29.cs?highlight=1-2)]

<span data-ttu-id="89267-254">`Invoke`方法异步执行并返回一个 `Task` 对象。</span><span class="sxs-lookup"><span data-stu-id="89267-254">The `Invoke` method executes asynchronously and returns a `Task` object.</span></span> <span data-ttu-id="89267-255">如果未指定 `await` 或，则在 `.Wait()` 调用的方法完成执行之前，将执行下一行代码。</span><span class="sxs-lookup"><span data-stu-id="89267-255">If you don't specify `await` or `.Wait()`, the next line of code will execute before the method that you invoke has finished executing.</span></span>

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a><span data-ttu-id="89267-256">如何处理连接生存期事件</span><span class="sxs-lookup"><span data-stu-id="89267-256">How to handle connection lifetime events</span></span>

<span data-ttu-id="89267-257">SignalR 提供以下连接生存期事件，你可以处理这些事件：</span><span class="sxs-lookup"><span data-stu-id="89267-257">SignalR provides the following connection lifetime events that you can handle:</span></span>

- <span data-ttu-id="89267-258">`Received`：在连接上接收到任何数据时引发。</span><span class="sxs-lookup"><span data-stu-id="89267-258">`Received`: Raised when any data is received on the connection.</span></span> <span data-ttu-id="89267-259">提供接收的数据。</span><span class="sxs-lookup"><span data-stu-id="89267-259">Provides the received data.</span></span>
- <span data-ttu-id="89267-260">`ConnectionSlow`：当客户端检测到连接缓慢或频繁断开时引发。</span><span class="sxs-lookup"><span data-stu-id="89267-260">`ConnectionSlow`: Raised when the client detects a slow or frequently dropping connection.</span></span>
- <span data-ttu-id="89267-261">`Reconnecting`：基础传输开始重新连接时引发。</span><span class="sxs-lookup"><span data-stu-id="89267-261">`Reconnecting`: Raised when the underlying transport begins reconnecting.</span></span>
- <span data-ttu-id="89267-262">`Reconnected`：当基础传输重新连接时引发。</span><span class="sxs-lookup"><span data-stu-id="89267-262">`Reconnected`: Raised when the underlying transport has reconnected.</span></span>
- <span data-ttu-id="89267-263">`StateChanged`：连接状态更改时引发。</span><span class="sxs-lookup"><span data-stu-id="89267-263">`StateChanged`: Raised when the connection state changes.</span></span> <span data-ttu-id="89267-264">提供旧状态和新状态。</span><span class="sxs-lookup"><span data-stu-id="89267-264">Provides the old state and the new state.</span></span> <span data-ttu-id="89267-265">有关连接状态值的信息，请参阅 [ConnectionState 枚举](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connectionstate(v=vs.111).aspx)。</span><span class="sxs-lookup"><span data-stu-id="89267-265">For information about connection state values see [ConnectionState Enumeration](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connectionstate(v=vs.111).aspx).</span></span>
- <span data-ttu-id="89267-266">`Closed`：连接断开连接时引发。</span><span class="sxs-lookup"><span data-stu-id="89267-266">`Closed`: Raised when the connection has disconnected.</span></span>

<span data-ttu-id="89267-267">例如，如果想要显示不是致命错误的警告消息，但会导致间歇连接问题（如缓慢或频繁断开连接），请处理 `ConnectionSlow` 事件。</span><span class="sxs-lookup"><span data-stu-id="89267-267">For example, if you want to display warning messages for errors that are not fatal but cause intermittent connection problems, such as slowness or frequent dropping of the connection, handle the `ConnectionSlow` event.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample30.cs)]

<span data-ttu-id="89267-268">有关详细信息，请参阅 [了解和处理 SignalR 中的连接生存期事件](handling-connection-lifetime-events.md)。</span><span class="sxs-lookup"><span data-stu-id="89267-268">For more information, see [Understanding and Handling Connection Lifetime Events in SignalR](handling-connection-lifetime-events.md).</span></span>

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a><span data-ttu-id="89267-269">如何处理错误</span><span class="sxs-lookup"><span data-stu-id="89267-269">How to handle errors</span></span>

<span data-ttu-id="89267-270">如果未在服务器上显式启用详细的错误消息，则在出现错误后 SignalR 返回的异常对象包含有关错误的最小信息。</span><span class="sxs-lookup"><span data-stu-id="89267-270">If you don't explicitly enable detailed error messages on the server, the exception object that SignalR returns after an error contains minimal information about the error.</span></span> <span data-ttu-id="89267-271">例如，如果对的调用 `newContosoChatMessage` 失败，则出于安全原因，不建议将错误对象中的错误消息包含 " `There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.` " 向生产中的客户端发送详细的错误消息，但如果你想要启用详细的错误消息以进行故障排除，请在服务器上使用以下代码。</span><span class="sxs-lookup"><span data-stu-id="89267-271">For example, if a call to `newContosoChatMessage` fails, the error message in the error object contains "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" Sending detailed error messages to clients in production is not recommended for security reasons, but if you want to enable detailed error messages for troubleshooting purposes, use the following code on the server.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample31.cs?highlight=2)]

<a id="handleerrors"></a>

<span data-ttu-id="89267-272">若要处理 SignalR 引发的错误，可以为 `Error` connection 对象上的事件添加处理程序。</span><span class="sxs-lookup"><span data-stu-id="89267-272">To handle errors that SignalR raises, you can add a handler for the `Error` event on the connection object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample32.cs)]

<span data-ttu-id="89267-273">若要处理方法调用中的错误，请将代码包装在 try-catch 块中。</span><span class="sxs-lookup"><span data-stu-id="89267-273">To handle errors from method invocations, wrap the code in a try-catch block.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample33.cs)]

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a><span data-ttu-id="89267-274">如何启用客户端日志记录</span><span class="sxs-lookup"><span data-stu-id="89267-274">How to enable client-side logging</span></span>

<span data-ttu-id="89267-275">若要启用客户端日志记录，请 `TraceLevel` 设置 `TraceWriter` 连接对象的和属性。</span><span class="sxs-lookup"><span data-stu-id="89267-275">To enable client-side logging, set the `TraceLevel` and `TraceWriter` properties on the connection object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample34.cs?highlight=3-4)]

<a id="wpfsl"></a>

## <a name="wpf-silverlight-and-console-application-code-samples-for-client-methods-that-the-server-can-call"></a><span data-ttu-id="89267-276">服务器可以调用的客户端方法的 WPF、Silverlight 和控制台应用程序代码示例</span><span class="sxs-lookup"><span data-stu-id="89267-276">WPF, Silverlight, and console application code samples for client methods that the server can call</span></span>

<span data-ttu-id="89267-277">前面所示的代码示例用于定义服务器可以调用的客户端方法。</span><span class="sxs-lookup"><span data-stu-id="89267-277">The code samples shown earlier for defining client methods that the server can call apply to WinRT clients.</span></span> <span data-ttu-id="89267-278">以下示例显示了适用于 WPF、Silverlight 和控制台应用程序客户端的等效代码。</span><span class="sxs-lookup"><span data-stu-id="89267-278">The following samples show the equivalent code for WPF, Silverlight, and console application clients.</span></span>

### <a name="methods-without-parameters"></a><span data-ttu-id="89267-279">不带参数的方法</span><span class="sxs-lookup"><span data-stu-id="89267-279">Methods without parameters</span></span>

<span data-ttu-id="89267-280">**从没有参数的服务器中调用的方法的 WPF 客户端代码**</span><span class="sxs-lookup"><span data-stu-id="89267-280">**WPF client code for method called from server without parameters**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample35.cs?highlight=1)]

<span data-ttu-id="89267-281">**从没有参数的服务器中调用的方法的 Silverlight 客户端代码**</span><span class="sxs-lookup"><span data-stu-id="89267-281">**Silverlight client code for method called from server without parameters**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample36.cs?highlight=1)]

<span data-ttu-id="89267-282">**不带参数的服务器中调用的方法的控制台应用程序客户端代码**</span><span class="sxs-lookup"><span data-stu-id="89267-282">**Console application client code for method called from server without parameters**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample37.cs?highlight=1)]

### <a name="methods-with-parameters-specifying-the-parameter-types"></a><span data-ttu-id="89267-283">带参数的方法，指定参数类型</span><span class="sxs-lookup"><span data-stu-id="89267-283">Methods with parameters, specifying the parameter types</span></span>

<span data-ttu-id="89267-284">**从具有参数的服务器中调用的方法的 WPF 客户端代码**</span><span class="sxs-lookup"><span data-stu-id="89267-284">**WPF client code for a method called from server with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample38.cs?highlight=1,4)]

<span data-ttu-id="89267-285">**从具有参数的服务器中调用的方法的 Silverlight 客户端代码**</span><span class="sxs-lookup"><span data-stu-id="89267-285">**Silverlight client code for a method called from server with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample39.cs?highlight=1,5)]

<span data-ttu-id="89267-286">**从具有参数的服务器中调用的方法的控制台应用程序客户端代码**</span><span class="sxs-lookup"><span data-stu-id="89267-286">**Console application client code for a method called from server with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample40.cs?highlight=1-2)]

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a><span data-ttu-id="89267-287">带参数的方法，指定参数的动态对象</span><span class="sxs-lookup"><span data-stu-id="89267-287">Methods with parameters, specifying dynamic objects for the parameters</span></span>

<span data-ttu-id="89267-288">**从具有参数的服务器中调用的方法的 WPF 客户端代码，对参数使用动态对象**</span><span class="sxs-lookup"><span data-stu-id="89267-288">**WPF client code for a method called from server with a parameter, using a dynamic object for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample41.cs?highlight=1,4)]

<span data-ttu-id="89267-289">**从具有参数的服务器中调用的方法的 Silverlight 客户端代码，对参数使用动态对象**</span><span class="sxs-lookup"><span data-stu-id="89267-289">**Silverlight client code for a method called from server with a parameter, using a dynamic object for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample42.cs?highlight=1,5)]

<span data-ttu-id="89267-290">**从具有参数的服务器中调用的方法的控制台应用程序客户端代码，对参数使用动态对象**</span><span class="sxs-lookup"><span data-stu-id="89267-290">**Console application client code for a method called from server with a parameter, using a dynamic object for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample43.cs?highlight=1-2)]

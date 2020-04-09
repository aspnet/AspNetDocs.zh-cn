---
uid: signalr/overview/guide-to-the-api/hubs-api-guide-net-client
title: ASP.NET信号器集线器 API 指南 - .NET 客户端 （C#） |微软文档
author: bradygaster
description: 本文档介绍了在 .NET 客户端（如 Windows 应用商店 （WinRT）、WPF、Silverlight 和 cons...
ms.author: bradyg
ms.date: 01/15/2019
ms.assetid: 6d02d9f7-94e5-4140-9f51-5a6040f274f6
msc.legacyurl: /signalr/overview/guide-to-the-api/hubs-api-guide-net-client
msc.type: authoredcontent
ms.openlocfilehash: d3536f1c15cd7dad7cd660becf0577e5c131f707
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675927"
---
# <a name="aspnet-signalr-hubs-api-guide---net-client-c"></a><span data-ttu-id="ee3bd-103">ASP.NET信号器集线器 API 指南 - .NET 客户端 （C#）</span><span class="sxs-lookup"><span data-stu-id="ee3bd-103">ASP.NET SignalR Hubs API Guide - .NET Client (C#)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="ee3bd-104">本文档介绍了在 .NET 客户端（如 Windows 应用商店 （WinRT）、WPF、Silverlight 和控制台应用程序）中为 SignalR 版本 2 使用集线器 API 的简介。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-104">This document provides an introduction to using the Hubs API for SignalR version 2 in .NET clients, such as Windows Store (WinRT), WPF, Silverlight, and console applications.</span></span>
>
> <span data-ttu-id="ee3bd-105">SignalR 集线器 API 使您能够从服务器对连接的客户端以及从客户端到服务器进行远程过程调用 （RPC）。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-105">The SignalR Hubs API enables you to make remote procedure calls (RPCs) from a server to connected clients and from clients to the server.</span></span> <span data-ttu-id="ee3bd-106">在服务器代码中，定义客户端可以调用的方法，并调用在客户端上运行的方法。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-106">In server code, you define methods that can be called by clients, and you call methods that run on the client.</span></span> <span data-ttu-id="ee3bd-107">在客户端代码中，定义可以从服务器调用的方法，并调用在服务器上运行的方法。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-107">In client code, you define methods that can be called from the server, and you call methods that run on the server.</span></span> <span data-ttu-id="ee3bd-108">SignalR 为您处理所有客户端到服务器管道。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-108">SignalR takes care of all of the client-to-server plumbing for you.</span></span>
>
> <span data-ttu-id="ee3bd-109">SignalR 还提供称为持久连接的较低级别的 API。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-109">SignalR also offers a lower-level API called Persistent Connections.</span></span> <span data-ttu-id="ee3bd-110">有关 SignalR、集线器和持久连接的介绍，或者有关如何构建完整的 SignalR 应用程序的教程，请参阅[SignalR - 入门](../getting-started/index.md)。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-110">For an introduction to SignalR, Hubs, and Persistent Connections, or for a tutorial that shows how to build a complete SignalR application, see [SignalR - Getting Started](../getting-started/index.md).</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="ee3bd-111">本主题中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="ee3bd-111">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="ee3bd-112">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="ee3bd-112">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/)
> - <span data-ttu-id="ee3bd-113">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="ee3bd-113">.NET 4.5</span></span>
> - <span data-ttu-id="ee3bd-114">信号R版本 2</span><span class="sxs-lookup"><span data-stu-id="ee3bd-114">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="ee3bd-115">本主题的早期版本</span><span class="sxs-lookup"><span data-stu-id="ee3bd-115">Previous versions of this topic</span></span>
>
> <span data-ttu-id="ee3bd-116">有关早期版本的 SignalR 的信息，请参阅[SignalR 旧版本](../older-versions/index.md)。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-116">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="ee3bd-117">问题和评论</span><span class="sxs-lookup"><span data-stu-id="ee3bd-117">Questions and comments</span></span>
>
> <span data-ttu-id="ee3bd-118">请留下反馈，关于你喜欢本教程的方式，以及我们可以在页面底部的评论中改进什么。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-118">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="ee3bd-119">如果您有与本教程没有直接关系的问题，您可以将它们发布到[ASP.NET SignalR 论坛](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com/)。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-119">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="overview"></a><span data-ttu-id="ee3bd-120">概述</span><span class="sxs-lookup"><span data-stu-id="ee3bd-120">Overview</span></span>

<span data-ttu-id="ee3bd-121">本文档包含以下各节：</span><span class="sxs-lookup"><span data-stu-id="ee3bd-121">This document contains the following sections:</span></span>

- [<span data-ttu-id="ee3bd-122">客户端设置</span><span class="sxs-lookup"><span data-stu-id="ee3bd-122">Client Setup</span></span>](#clientsetup)
- [<span data-ttu-id="ee3bd-123">如何建立连接</span><span class="sxs-lookup"><span data-stu-id="ee3bd-123">How to establish a connection</span></span>](#establishconnection)

    - [<span data-ttu-id="ee3bd-124">来自银光客户端的跨域连接</span><span class="sxs-lookup"><span data-stu-id="ee3bd-124">Cross-domain connections from Silverlight clients</span></span>](#slcrossdomain)
- [<span data-ttu-id="ee3bd-125">如何配置连接</span><span class="sxs-lookup"><span data-stu-id="ee3bd-125">How to configure the connection</span></span>](#configureconnection)

    - [<span data-ttu-id="ee3bd-126">如何设置 WPF 客户端中的最大并发连接数</span><span class="sxs-lookup"><span data-stu-id="ee3bd-126">How to set the maximum number of concurrent connections in WPF clients</span></span>](#maxconnections)
    - [<span data-ttu-id="ee3bd-127">如何指定查询字符串参数</span><span class="sxs-lookup"><span data-stu-id="ee3bd-127">How to specify query string parameters</span></span>](#querystring)
    - [<span data-ttu-id="ee3bd-128">如何指定传输方法</span><span class="sxs-lookup"><span data-stu-id="ee3bd-128">How to specify the transport method</span></span>](#transport)
    - [<span data-ttu-id="ee3bd-129">如何指定 HTTP 标头</span><span class="sxs-lookup"><span data-stu-id="ee3bd-129">How to specify HTTP headers</span></span>](#httpheaders)
    - [<span data-ttu-id="ee3bd-130">如何指定客户端证书</span><span class="sxs-lookup"><span data-stu-id="ee3bd-130">How to specify client certificates</span></span>](#clientcertificate)
- [<span data-ttu-id="ee3bd-131">如何创建中心代理</span><span class="sxs-lookup"><span data-stu-id="ee3bd-131">How to create the Hub proxy</span></span>](#proxy)
- [<span data-ttu-id="ee3bd-132">如何在客户端上定义服务器可以调用的方法</span><span class="sxs-lookup"><span data-stu-id="ee3bd-132">How to define methods on the client that the server can call</span></span>](#callclient)

    - [<span data-ttu-id="ee3bd-133">没有参数的方法</span><span class="sxs-lookup"><span data-stu-id="ee3bd-133">Methods without parameters</span></span>](#clientmethodswithoutparms)
    - [<span data-ttu-id="ee3bd-134">具有参数的方法，指定参数类型</span><span class="sxs-lookup"><span data-stu-id="ee3bd-134">Methods with parameters, specifying parameter types</span></span>](#clientmethodswithparmtypes)
    - [<span data-ttu-id="ee3bd-135">具有参数的方法，为参数指定动态对象</span><span class="sxs-lookup"><span data-stu-id="ee3bd-135">Methods with parameters, specifying dynamic objects for the parameters</span></span>](#clientmethodswithdynamparms)
    - [<span data-ttu-id="ee3bd-136">如何删除处理程序</span><span class="sxs-lookup"><span data-stu-id="ee3bd-136">How to remove a handler</span></span>](#removehandler)
- [<span data-ttu-id="ee3bd-137">如何从客户端调用服务器方法</span><span class="sxs-lookup"><span data-stu-id="ee3bd-137">How to call server methods from the client</span></span>](#callserver)
- [<span data-ttu-id="ee3bd-138">如何处理连接生存期事件</span><span class="sxs-lookup"><span data-stu-id="ee3bd-138">How to handle connection lifetime events</span></span>](#connectionlifetime)
- [<span data-ttu-id="ee3bd-139">如何处理错误</span><span class="sxs-lookup"><span data-stu-id="ee3bd-139">How to handle errors</span></span>](#handleerrors)
- [<span data-ttu-id="ee3bd-140">如何启用客户端日志记录</span><span class="sxs-lookup"><span data-stu-id="ee3bd-140">How to enable client-side logging</span></span>](#logging)
- [<span data-ttu-id="ee3bd-141">WPF、Silverlight 和控制台应用程序代码示例，用于服务器可以调用的客户端方法</span><span class="sxs-lookup"><span data-stu-id="ee3bd-141">WPF, Silverlight, and console application code samples for client methods that the server can call</span></span>](#wpfsl)

<span data-ttu-id="ee3bd-142">有关示例 .NET 客户端项目，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="ee3bd-142">For a sample .NET client projects, see the following resources:</span></span>

- <span data-ttu-id="ee3bd-143">[古斯塔沃-阿尔门塔 / 信号R-样本](https://github.com/gustavo-armenta/SignalR-Samples)GitHub.com（WinRT，银光，控制台应用程序示例）。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-143">[gustavo-armenta / SignalR-Samples](https://github.com/gustavo-armenta/SignalR-Samples) on GitHub.com (WinRT, Silverlight, console app examples).</span></span>
- <span data-ttu-id="ee3bd-144">[达米安爱德华兹 / 信号R-移动形状演示 / 移动形状.桌面](https://github.com/DamianEdwards/SignalR-MoveShapeDemo/tree/master/MoveShape/MoveShape.Desktop)GitHub.com （WPF 示例）。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-144">[DamianEdwards / SignalR-MoveShapeDemo / MoveShape.Desktop](https://github.com/DamianEdwards/SignalR-MoveShapeDemo/tree/master/MoveShape/MoveShape.Desktop) on GitHub.com (WPF example).</span></span>
- <span data-ttu-id="ee3bd-145">[信号R / 微软.AspNet.SignalR.客户端.GitHub.com上的样本](https://github.com/SignalR/SignalR/tree/master/samples/Microsoft.AspNet.SignalR.Client.Samples)（控制台应用示例）。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-145">[SignalR / Microsoft.AspNet.SignalR.Client.Samples](https://github.com/SignalR/SignalR/tree/master/samples/Microsoft.AspNet.SignalR.Client.Samples) on GitHub.com (Console app example).</span></span>

<span data-ttu-id="ee3bd-146">有关如何对服务器或 JavaScript 客户端进行编程的文档，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="ee3bd-146">For documentation on how to program the server or JavaScript clients, see the following resources:</span></span>

- [<span data-ttu-id="ee3bd-147">信号器集线器 API 指南 - 服务器</span><span class="sxs-lookup"><span data-stu-id="ee3bd-147">SignalR Hubs API Guide - Server</span></span>](hubs-api-guide-server.md)
- [<span data-ttu-id="ee3bd-148">信号器中心 API 指南 - JavaScript 客户端</span><span class="sxs-lookup"><span data-stu-id="ee3bd-148">SignalR Hubs API Guide - JavaScript Client</span></span>](hubs-api-guide-javascript-client.md)

<span data-ttu-id="ee3bd-149">指向 API 参考主题的链接指向 API 的 .NET 4.5 版本。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-149">Links to API Reference topics are to the .NET 4.5 version of the API.</span></span> <span data-ttu-id="ee3bd-150">如果使用 .NET 4，请参阅[API 主题的 .NET 4 版本](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx)。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-150">If you're using .NET 4, see [the .NET 4 version of the API topics](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx).</span></span>

<a id="clientsetup"></a>

## <a name="client-setup"></a><span data-ttu-id="ee3bd-151">客户端设置</span><span class="sxs-lookup"><span data-stu-id="ee3bd-151">Client setup</span></span>

<span data-ttu-id="ee3bd-152">安装[微软.AspNet.SignalR.客户端](http://nuget.org/packages/Microsoft.AspNet.SignalR.Client)NuGet 包（不是[微软.AspNet.SignalR](http://nuget.org/packages/microsoft.aspnet.signalr)包）。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-152">Install the [Microsoft.AspNet.SignalR.Client](http://nuget.org/packages/Microsoft.AspNet.SignalR.Client) NuGet package (not the [Microsoft.AspNet.SignalR](http://nuget.org/packages/microsoft.aspnet.signalr) package).</span></span> <span data-ttu-id="ee3bd-153">此包支持 WinRT、Silverlight、WPF、控制台应用程序和 Windows Phone 客户端，适用于 .NET 4 和 .NET 4.5。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-153">This package supports WinRT, Silverlight, WPF, console application, and Windows Phone clients, for both .NET 4 and .NET 4.5.</span></span>

<span data-ttu-id="ee3bd-154">如果客户端上的 SignalR 版本与服务器上的版本不同，则 SignalR 通常能够适应差异。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-154">If the version of SignalR that you have on the client is different from the version that you have on the server, SignalR is often able to adapt to the difference.</span></span> <span data-ttu-id="ee3bd-155">例如，运行 SignalR 版本 2 的服务器将支持安装了 1.1.x 的客户端以及安装了版本 2 的客户端。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-155">For example, a server running SignalR version 2 will support clients that have 1.1.x installed as well as clients that have version 2 installed.</span></span> <span data-ttu-id="ee3bd-156">如果服务器上的版本和客户端上的版本之间的差异太大，或者如果客户端比服务器新，则在客户端尝试建立连接时，SignalR 会引发`InvalidOperationException`异常。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-156">If the difference between the version on the server and the version on the client is too great, or if the client is newer than the server, SignalR throws an `InvalidOperationException` exception when the client tries to establish a connection.</span></span> <span data-ttu-id="ee3bd-157">错误消息为""。`You are using a version of the client that isn't compatible with the server. Client version X.X, server version X.X`</span><span class="sxs-lookup"><span data-stu-id="ee3bd-157">The error message is "`You are using a version of the client that isn't compatible with the server. Client version X.X, server version X.X`".</span></span>

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a><span data-ttu-id="ee3bd-158">如何建立连接</span><span class="sxs-lookup"><span data-stu-id="ee3bd-158">How to establish a connection</span></span>

<span data-ttu-id="ee3bd-159">在建立连接之前，必须创建对象`HubConnection`并创建代理。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-159">Before you can establish a connection, you have to create a `HubConnection` object and create a proxy.</span></span> <span data-ttu-id="ee3bd-160">要建立连接，请`Start`调用`HubConnection`对象上的方法。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-160">To establish the connection, call the `Start` method on the `HubConnection` object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample1.cs?highlight=1,5)]

> [!NOTE]
> <span data-ttu-id="ee3bd-161">对于 JavaScript 客户端，在调用方法建立连接之前，`Start`您必须至少注册一个事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-161">For JavaScript clients you have to register at least one event handler before calling the `Start` method to establish the connection.</span></span> <span data-ttu-id="ee3bd-162">对于 .NET 客户端，这不需要。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-162">This is not necessary for .NET clients.</span></span> <span data-ttu-id="ee3bd-163">对于 JavaScript 客户端，生成的代理代码会自动为服务器上存在的所有中心创建代理，注册处理程序是指示客户端打算使用哪个集线器的方式。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-163">For JavaScript clients, the generated proxy code automatically creates proxies for all Hubs that exist on the server, and registering a handler is how you indicate which Hubs your client intends to use.</span></span> <span data-ttu-id="ee3bd-164">但对于 .NET 客户端，您可以手动创建集线器代理，因此 SignalR 假定您将使用为其创建代理的任何集线器。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-164">But for a .NET client you create Hub proxies manually, so SignalR assumes that you will be using any Hub that you create a proxy for.</span></span>

<span data-ttu-id="ee3bd-165">示例代码使用默认的"/信号器"URL 连接到您的 SignalR 服务。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-165">The sample code uses the default "/signalr" URL to connect to your SignalR service.</span></span> <span data-ttu-id="ee3bd-166">有关如何指定其他基本 URL 的信息，请参阅[ASP.NET信号R中心 API 指南 - 服务器 - /signalr URL](hubs-api-guide-server.md#signalrurl)。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-166">For information about how to specify a different base URL, see [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](hubs-api-guide-server.md#signalrurl).</span></span>

<span data-ttu-id="ee3bd-167">该方法`Start`以异步方式执行。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-167">The `Start` method executes asynchronously.</span></span> <span data-ttu-id="ee3bd-168">为了确保后续代码行在建立连接之前不会执行，请使用`await`ASP.NET 4.5 异步方法或`.Wait()`同步方法。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-168">To make sure that subsequent lines of code don't execute until after the connection is established, use `await` in an ASP.NET 4.5 asynchronous method or `.Wait()` in a synchronous method.</span></span> <span data-ttu-id="ee3bd-169">不要在 WinRT`.Wait()`客户端中使用。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-169">Don't use `.Wait()` in a WinRT client.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample2.cs?highlight=1)]

[!code-css[Main](hubs-api-guide-net-client/samples/sample3.css?highlight=1)]

<a id="slcrossdomain"></a>

### <a name="cross-domain-connections-from-silverlight-clients"></a><span data-ttu-id="ee3bd-170">来自银光客户端的跨域连接</span><span class="sxs-lookup"><span data-stu-id="ee3bd-170">Cross-domain connections from Silverlight clients</span></span>

<span data-ttu-id="ee3bd-171">有关如何启用来自 Silverlight 客户端的跨域连接的信息，请参阅[使服务跨域边界可用](https://msdn.microsoft.com/library/cc197955(v=vs.95).aspx)。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-171">For information about how to enable cross-domain connections from Silverlight clients, see [Making a Service Available Across Domain Boundaries](https://msdn.microsoft.com/library/cc197955(v=vs.95).aspx).</span></span>

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a><span data-ttu-id="ee3bd-172">如何配置连接</span><span class="sxs-lookup"><span data-stu-id="ee3bd-172">How to configure the connection</span></span>

<span data-ttu-id="ee3bd-173">在建立连接之前，可以指定以下任一选项：</span><span class="sxs-lookup"><span data-stu-id="ee3bd-173">Before you establish a connection, you can specify any of the following options:</span></span>

- <span data-ttu-id="ee3bd-174">并发连接限制。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-174">Concurrent connections limit.</span></span>
- <span data-ttu-id="ee3bd-175">查询字符串参数。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-175">Query string parameters.</span></span>
- <span data-ttu-id="ee3bd-176">传输方法。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-176">The transport method.</span></span>
- <span data-ttu-id="ee3bd-177">HTTP 标头。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-177">HTTP headers.</span></span>
- <span data-ttu-id="ee3bd-178">客户端证书。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-178">Client certificates.</span></span>

<a id="maxconnections"></a>

### <a name="how-to-set-the-maximum-number-of-concurrent-connections-in-wpf-clients"></a><span data-ttu-id="ee3bd-179">如何设置 WPF 客户端中的最大并发连接数</span><span class="sxs-lookup"><span data-stu-id="ee3bd-179">How to set the maximum number of concurrent connections in WPF clients</span></span>

<span data-ttu-id="ee3bd-180">在 WPF 客户端中，您可能需要从默认值 2 增加并发连接的最大数量。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-180">In WPF clients, you might have to increase the maximum number of concurrent connections from its default value of 2.</span></span> <span data-ttu-id="ee3bd-181">建议的值为 10。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-181">The recommended value is 10.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample4.cs?highlight=5)]

<span data-ttu-id="ee3bd-182">有关详细信息，请参阅[服务点管理器.默认连接限制](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-182">For more information, see [ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx).</span></span>

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a><span data-ttu-id="ee3bd-183">如何指定查询字符串参数</span><span class="sxs-lookup"><span data-stu-id="ee3bd-183">How to specify query string parameters</span></span>

<span data-ttu-id="ee3bd-184">如果要在客户端连接时将数据发送到服务器，则可以向连接对象添加查询字符串参数。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-184">If you want to send data to the server when the client connects, you can add query string parameters to the connection object.</span></span> <span data-ttu-id="ee3bd-185">下面的示例演示如何在客户端代码中设置查询字符串参数。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-185">The following example shows how to set a query string parameter in client code.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample5.cs)]

<span data-ttu-id="ee3bd-186">下面的示例演示如何读取服务器代码中的查询字符串参数。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-186">The following example shows how to read a query string parameter in server code.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample6.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a><span data-ttu-id="ee3bd-187">如何指定传输方法</span><span class="sxs-lookup"><span data-stu-id="ee3bd-187">How to specify the transport method</span></span>

<span data-ttu-id="ee3bd-188">作为连接过程的一部分，SignalR 客户端通常与服务器协商以确定服务器和客户端支持的最佳传输。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-188">As part of the process of connecting, a SignalR client normally negotiates with the server to determine the best transport that is supported by both server and client.</span></span> <span data-ttu-id="ee3bd-189">如果您已经知道要使用的传输，可以绕过此协商过程。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-189">If you already know which transport you want to use, you can bypass this negotiation process.</span></span> <span data-ttu-id="ee3bd-190">要指定传输方法，请将传输对象传递给 Start 方法。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-190">To specify the transport method, pass in a transport object to the Start method.</span></span> <span data-ttu-id="ee3bd-191">下面的示例演示如何在客户端代码中指定传输方法。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-191">The following example shows how to specify the transport method in client code.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample7.cs?highlight=5)]

<span data-ttu-id="ee3bd-192">[Microsoft.AspNet.SignalR.Client.传输](https://msdn.microsoft.com/library/jj918090(v=vs.111).aspx)命名空间包括以下类，可用于指定传输。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-192">The [Microsoft.AspNet.SignalR.Client.Transports](https://msdn.microsoft.com/library/jj918090(v=vs.111).aspx) namespace includes the following classes that you can use to specify the transport.</span></span>

- <span data-ttu-id="ee3bd-193">[长轮询传输](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.longpollingtransport(v=vs.111).aspx)</span><span class="sxs-lookup"><span data-stu-id="ee3bd-193">[LongPollingTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.longpollingtransport(v=vs.111).aspx)</span></span>
- <span data-ttu-id="ee3bd-194">[服务器发送事件传输](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.serversenteventstransport(v=vs.111).aspx)</span><span class="sxs-lookup"><span data-stu-id="ee3bd-194">[ServerSentEventsTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.serversenteventstransport(v=vs.111).aspx)</span></span>
- <span data-ttu-id="ee3bd-195">[WebSocket 传输](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.websockettransport(v=vs.111).aspx)（仅在服务器和客户端使用 .NET 4.5 时可用。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-195">[WebSocketTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.websockettransport(v=vs.111).aspx) (Available only when both server and client use .NET 4.5.)</span></span>
- <span data-ttu-id="ee3bd-196">[自动传输](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.autotransport(v=vs.111).aspx)（自动选择客户端和服务器支持的最佳传输。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-196">[AutoTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.autotransport(v=vs.111).aspx) (Automatically chooses the best transport that is supported by both the client and the server.</span></span> <span data-ttu-id="ee3bd-197">这是默认传输。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-197">This is the default transport.</span></span> <span data-ttu-id="ee3bd-198">将此传递给`Start`方法的效果与不传入任何内容的效果相同。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-198">Passing this in to the `Start` method has the same effect as not passing in anything.)</span></span>

<span data-ttu-id="ee3bd-199">ForeverFrame 传输不包括在此列表中，因为它仅由浏览器使用。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-199">The ForeverFrame transport is not included in this list because it is used only by browsers.</span></span>

<span data-ttu-id="ee3bd-200">有关如何在服务器代码中检查传输方法的信息，请参阅[ASP.NET SignalR 集线器 API 指南 - 服务器 - 如何从 Context 属性获取有关客户端的信息](hubs-api-guide-server.md#contextproperty)。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-200">For information about how to check the transport method in server code, see [ASP.NET SignalR Hubs API Guide - Server - How to get information about the client from the Context property](hubs-api-guide-server.md#contextproperty).</span></span> <span data-ttu-id="ee3bd-201">有关传输和回退的详细信息，请参阅[信号R - 传输和回退简介](../getting-started/introduction-to-signalr.md#transports)。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-201">For more information about transports and fallbacks, see [Introduction to SignalR - Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span>

<a id="httpheaders"></a>

### <a name="how-to-specify-http-headers"></a><span data-ttu-id="ee3bd-202">如何指定 HTTP 标头</span><span class="sxs-lookup"><span data-stu-id="ee3bd-202">How to specify HTTP headers</span></span>

<span data-ttu-id="ee3bd-203">要设置 HTTP 标头，`Headers`请使用连接对象上的属性。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-203">To set HTTP headers, use the `Headers` property on the connection object.</span></span> <span data-ttu-id="ee3bd-204">下面的示例演示如何添加 HTTP 标头。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-204">The following example shows how to add an HTTP header.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample8.cs?highlight=2)]

<a id="clientcertificate"></a>

### <a name="how-to-specify-client-certificates"></a><span data-ttu-id="ee3bd-205">如何指定客户端证书</span><span class="sxs-lookup"><span data-stu-id="ee3bd-205">How to specify client certificates</span></span>

<span data-ttu-id="ee3bd-206">要添加客户端证书，`AddClientCertificate`请使用连接对象上的方法。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-206">To add client certificates, use the `AddClientCertificate` method on the connection object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample9.cs?highlight=2)]

<a id="proxy"></a>

## <a name="how-to-create-the-hub-proxy"></a><span data-ttu-id="ee3bd-207">如何创建中心代理</span><span class="sxs-lookup"><span data-stu-id="ee3bd-207">How to create the Hub proxy</span></span>

<span data-ttu-id="ee3bd-208">为了在客户端上定义集线器可以从服务器调用的方法，并在服务器上的集线器上调用方法，请通过调用`CreateHubProxy`连接对象为集线器创建代理。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-208">In order to define methods on the client that a Hub can call from the server, and to invoke methods on a Hub at the server, create a proxy for the Hub by calling `CreateHubProxy` on the connection object.</span></span> <span data-ttu-id="ee3bd-209">传递给的字符串`CreateHubProxy`是 Hub 类的名称，或者`HubName`属性指定的名称（如果在服务器上使用）。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-209">The string you pass in to `CreateHubProxy` is the name of your Hub class, or the name specified by the `HubName` attribute if one was used on the server.</span></span> <span data-ttu-id="ee3bd-210">名称匹配不区分大小写。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-210">Name matching is case-insensitive.</span></span>

<span data-ttu-id="ee3bd-211">**服务器上的集线器类**</span><span class="sxs-lookup"><span data-stu-id="ee3bd-211">**Hub class on server**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample10.cs?highlight=1)]

<span data-ttu-id="ee3bd-212">**为中心类创建客户端代理**</span><span class="sxs-lookup"><span data-stu-id="ee3bd-212">**Create client proxy for the Hub class**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample11.cs?highlight=3)]

<span data-ttu-id="ee3bd-213">如果使用`HubName`属性修饰 Hub 类，请使用该名称。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-213">If you decorate your Hub class with a `HubName` attribute, use that name.</span></span>

<span data-ttu-id="ee3bd-214">**服务器上的集线器类**</span><span class="sxs-lookup"><span data-stu-id="ee3bd-214">**Hub class on server**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample12.cs)]

<span data-ttu-id="ee3bd-215">**为中心类创建客户端代理**</span><span class="sxs-lookup"><span data-stu-id="ee3bd-215">**Create client proxy for the Hub class**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample13.cs?highlight=3)]

<span data-ttu-id="ee3bd-216">如果使用相同的`HubConnection.CreateHubProxy``hubName`调用多次 ，则会获取相同的缓存`IHubProxy`对象。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-216">If you call `HubConnection.CreateHubProxy` multiple times with the same `hubName`, you get the same cached `IHubProxy` object.</span></span>

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a><span data-ttu-id="ee3bd-217">如何在客户端上定义服务器可以调用的方法</span><span class="sxs-lookup"><span data-stu-id="ee3bd-217">How to define methods on the client that the server can call</span></span>

<span data-ttu-id="ee3bd-218">要定义服务器可以调用的方法，请使用代理`On`的方法注册事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-218">To define a method that the server can call, use the proxy's `On` method to register an event handler.</span></span>

<span data-ttu-id="ee3bd-219">方法名称匹配不区分大小写。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-219">Method name matching is case-insensitive.</span></span> <span data-ttu-id="ee3bd-220">例如，`Clients.All.UpdateStockPrice`在服务器上将执行`updateStockPrice`、`updatestockprice`或`UpdateStockPrice`在客户端上。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-220">For example, `Clients.All.UpdateStockPrice` on the server will execute `updateStockPrice`, `updatestockprice`, or `UpdateStockPrice` on the client.</span></span>

<span data-ttu-id="ee3bd-221">不同的客户端平台对如何编写方法来更新 UI 有不同的要求。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-221">Different client platforms have different requirements for how you write method code to update the UI.</span></span> <span data-ttu-id="ee3bd-222">显示的示例适用于 WinRT （Windows 应用商店 .NET） 客户端。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-222">The examples shown are for WinRT (Windows Store .NET) clients.</span></span> <span data-ttu-id="ee3bd-223">WPF、Silverlight 和控制台应用程序示例在本[主题后面的单独部分](#wpfsl)提供。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-223">WPF, Silverlight, and console application examples are provided in [a separate section later in this topic](#wpfsl).</span></span>

<a id="clientmethodswithoutparms"></a>

### <a name="methods-without-parameters"></a><span data-ttu-id="ee3bd-224">没有参数的方法</span><span class="sxs-lookup"><span data-stu-id="ee3bd-224">Methods without parameters</span></span>

<span data-ttu-id="ee3bd-225">如果正在处理的方法没有参数，请使用`On`方法的非泛型重载：</span><span class="sxs-lookup"><span data-stu-id="ee3bd-225">If the method you're handling does not have parameters, use the non-generic overload of the `On` method:</span></span>

<span data-ttu-id="ee3bd-226">**服务器代码调用没有参数的客户端方法**</span><span class="sxs-lookup"><span data-stu-id="ee3bd-226">**Server code calling client method without parameters**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample14.cs?highlight=5)]

<span data-ttu-id="ee3bd-227">**WinRT 客户端代码用于从服务器调用没有参数的方法（[请参阅本主题后面的 WPF 和 Silverlight 示例](#wpfsl)）**</span><span class="sxs-lookup"><span data-stu-id="ee3bd-227">**WinRT Client code for method called from server without parameters ([see WPF and Silverlight examples later in this topic](#wpfsl))**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample15.cs)]

<a id="clientmethodswithparmtypes"></a>

### <a name="methods-with-parameters-specifying-the-parameter-types"></a><span data-ttu-id="ee3bd-228">具有参数的方法，指定参数类型</span><span class="sxs-lookup"><span data-stu-id="ee3bd-228">Methods with parameters, specifying the parameter types</span></span>

<span data-ttu-id="ee3bd-229">如果要处理的方法具有参数，请指定参数的类型作为`On`方法的泛型类型。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-229">If the method you're handling has parameters, specify the types of the parameters as the generic types of the `On` method.</span></span> <span data-ttu-id="ee3bd-230">`On`该方法有泛型重载，使您能够指定最多 8 个参数（Windows Phone 7 上的 4 个参数）。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-230">There are generic overloads of the `On` method to enable you to specify up to 8 parameters (4 on Windows Phone 7).</span></span> <span data-ttu-id="ee3bd-231">在下面的示例中，一个参数发送到`UpdateStockPrice`方法。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-231">In the following example, one parameter is sent to the `UpdateStockPrice` method.</span></span>

<span data-ttu-id="ee3bd-232">**使用参数调用客户端方法的服务器代码**</span><span class="sxs-lookup"><span data-stu-id="ee3bd-232">**Server code calling client method with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample16.cs?highlight=3)]

<span data-ttu-id="ee3bd-233">**用于参数的 Stock 类**</span><span class="sxs-lookup"><span data-stu-id="ee3bd-233">**The Stock class used for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample17.cs)]

<span data-ttu-id="ee3bd-234">**WinRT 客户端代码用于从具有参数的服务器调用的方法（[请参阅本主题后面的 WPF 和 Silverlight 示例](#wpfsl)）**</span><span class="sxs-lookup"><span data-stu-id="ee3bd-234">**WinRT Client code for a method called from server with a parameter ([see WPF and Silverlight examples later in this topic](#wpfsl))**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample18.cs?highlight=1,5)]

<a id="clientmethodswithdynamparms"></a>

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a><span data-ttu-id="ee3bd-235">具有参数的方法，为参数指定动态对象</span><span class="sxs-lookup"><span data-stu-id="ee3bd-235">Methods with parameters, specifying dynamic objects for the parameters</span></span>

<span data-ttu-id="ee3bd-236">作为将参数指定为`On`方法的泛型类型的替代方法，可以将参数指定为动态对象：</span><span class="sxs-lookup"><span data-stu-id="ee3bd-236">As an alternative to specifying parameters as generic types of the `On` method, you can specify parameters as dynamic objects:</span></span>

<span data-ttu-id="ee3bd-237">**使用参数调用客户端方法的服务器代码**</span><span class="sxs-lookup"><span data-stu-id="ee3bd-237">**Server code calling client method with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample19.cs?highlight=3)]

<span data-ttu-id="ee3bd-238">**用于参数的 Stock 类**</span><span class="sxs-lookup"><span data-stu-id="ee3bd-238">**The Stock class used for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample20.cs)]

<span data-ttu-id="ee3bd-239">**WinRT 客户端代码用于使用参数从服务器调用的方法，使用参数的动态对象（[请参阅本主题后面的 WPF 和 Silverlight 示例](#wpfsl)）**</span><span class="sxs-lookup"><span data-stu-id="ee3bd-239">**WinRT Client code for a method called from server with a parameter, using a dynamic object for the parameter ([see WPF and Silverlight examples later in this topic](#wpfsl))**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample21.cs?highlight=1,5)]

<a id="removehandler"></a>

### <a name="how-to-remove-a-handler"></a><span data-ttu-id="ee3bd-240">如何删除处理程序</span><span class="sxs-lookup"><span data-stu-id="ee3bd-240">How to remove a handler</span></span>

<span data-ttu-id="ee3bd-241">要删除处理程序，请调用其`Dispose`方法。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-241">To remove a handler, call its `Dispose` method.</span></span>

<span data-ttu-id="ee3bd-242">**从服务器调用的方法的客户端代码**</span><span class="sxs-lookup"><span data-stu-id="ee3bd-242">**Client code for a method called from server**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample22.cs?highlight=1)]

<span data-ttu-id="ee3bd-243">**客户端代码以删除处理程序**</span><span class="sxs-lookup"><span data-stu-id="ee3bd-243">**Client code to remove the handler**</span></span>

[!code-css[Main](hubs-api-guide-net-client/samples/sample23.css?highlight=1)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a><span data-ttu-id="ee3bd-244">如何从客户端调用服务器方法</span><span class="sxs-lookup"><span data-stu-id="ee3bd-244">How to call server methods from the client</span></span>

<span data-ttu-id="ee3bd-245">要在服务器上调用方法，`Invoke`请使用集线器代理上的方法。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-245">To call a method on the server, use the `Invoke` method on the Hub proxy.</span></span>

<span data-ttu-id="ee3bd-246">如果服务器方法没有返回值，请使用`Invoke`方法的非泛型重载。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-246">If the server method has no return value, use the non-generic overload of the `Invoke` method.</span></span>

<span data-ttu-id="ee3bd-247">**没有返回值的方法的服务器代码**</span><span class="sxs-lookup"><span data-stu-id="ee3bd-247">**Server code for a method that has no return value**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample24.cs?highlight=3)]

<span data-ttu-id="ee3bd-248">**调用没有返回值的方法的客户端代码**</span><span class="sxs-lookup"><span data-stu-id="ee3bd-248">**Client code calling a method that has no return value**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample25.cs?highlight=1)]

<span data-ttu-id="ee3bd-249">如果服务器方法具有返回值，请指定返回类型作为`Invoke`方法的泛型类型。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-249">If the server method has a return value, specify the return type as the generic type of the `Invoke` method.</span></span>

<span data-ttu-id="ee3bd-250">**具有返回值并采用复杂类型参数的方法的服务器代码**</span><span class="sxs-lookup"><span data-stu-id="ee3bd-250">**Server code for a method that has a return value and takes a complex type parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample26.cs?highlight=1)]

<span data-ttu-id="ee3bd-251">**用于参数和返回值的 Stock 类**</span><span class="sxs-lookup"><span data-stu-id="ee3bd-251">**The Stock class used for the parameter and return value**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample27.cs)]

<span data-ttu-id="ee3bd-252">**客户端代码调用具有返回值并采用复杂类型参数的方法，在 ASP.NET 4.5 异步方法中调用**</span><span class="sxs-lookup"><span data-stu-id="ee3bd-252">**Client code calling a method that has a return value and takes a complex type parameter, in an ASP.NET 4.5 async method**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample28.cs?highlight=1-2)]

<span data-ttu-id="ee3bd-253">**客户端代码调用具有返回值并采用复杂类型参数的方法（在同步方法中）**</span><span class="sxs-lookup"><span data-stu-id="ee3bd-253">**Client code calling a method that has a return value and takes a complex type parameter, in a synchronous method**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample29.cs?highlight=1-2)]

<span data-ttu-id="ee3bd-254">该方法`Invoke`异步执行并返回对象`Task`。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-254">The `Invoke` method executes asynchronously and returns a `Task` object.</span></span> <span data-ttu-id="ee3bd-255">如果不指定`await`或`.Wait()`，则下一行代码将在调用的方法完成执行之前执行。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-255">If you don't specify `await` or `.Wait()`, the next line of code will execute before the method that you invoke has finished executing.</span></span>

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a><span data-ttu-id="ee3bd-256">如何处理连接生存期事件</span><span class="sxs-lookup"><span data-stu-id="ee3bd-256">How to handle connection lifetime events</span></span>

<span data-ttu-id="ee3bd-257">SignalR 提供您可以处理的以下连接生存期事件：</span><span class="sxs-lookup"><span data-stu-id="ee3bd-257">SignalR provides the following connection lifetime events that you can handle:</span></span>

- <span data-ttu-id="ee3bd-258">`Received`：在连接上收到任何数据时引发。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-258">`Received`: Raised when any data is received on the connection.</span></span> <span data-ttu-id="ee3bd-259">提供接收的数据。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-259">Provides the received data.</span></span>
- <span data-ttu-id="ee3bd-260">`ConnectionSlow`：当客户端检测到连接缓慢或频繁断开时引发。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-260">`ConnectionSlow`: Raised when the client detects a slow or frequently dropping connection.</span></span>
- <span data-ttu-id="ee3bd-261">`Reconnecting`：当基础传输开始重新连接时引发。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-261">`Reconnecting`: Raised when the underlying transport begins reconnecting.</span></span>
- <span data-ttu-id="ee3bd-262">`Reconnected`：在基础传输重新连接时引发。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-262">`Reconnected`: Raised when the underlying transport has reconnected.</span></span>
- <span data-ttu-id="ee3bd-263">`StateChanged`：当连接状态更改时引发。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-263">`StateChanged`: Raised when the connection state changes.</span></span> <span data-ttu-id="ee3bd-264">提供旧状态和新状态。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-264">Provides the old state and the new state.</span></span> <span data-ttu-id="ee3bd-265">有关连接状态值的信息，请参阅[连接状态枚举](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connectionstate(v=vs.111).aspx)。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-265">For information about connection state values see [ConnectionState Enumeration](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connectionstate(v=vs.111).aspx).</span></span>
- <span data-ttu-id="ee3bd-266">`Closed`：连接断开连接时引发。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-266">`Closed`: Raised when the connection has disconnected.</span></span>

<span data-ttu-id="ee3bd-267">例如，如果要显示未致命但会导致间歇性连接问题（如连接速度慢或频繁断开）的错误的警告消息，则处理该`ConnectionSlow`事件。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-267">For example, if you want to display warning messages for errors that are not fatal but cause intermittent connection problems, such as slowness or frequent dropping of the connection, handle the `ConnectionSlow` event.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample30.cs)]

<span data-ttu-id="ee3bd-268">有关详细信息，请参阅在[SignalR 中了解和处理连接生存期事件](handling-connection-lifetime-events.md)。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-268">For more information, see [Understanding and Handling Connection Lifetime Events in SignalR](handling-connection-lifetime-events.md).</span></span>

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a><span data-ttu-id="ee3bd-269">如何处理错误</span><span class="sxs-lookup"><span data-stu-id="ee3bd-269">How to handle errors</span></span>

<span data-ttu-id="ee3bd-270">如果未在服务器上显式启用详细的错误消息，则 SignalR 在错误后返回的异常对象包含有关该错误的最少信息。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-270">If you don't explicitly enable detailed error messages on the server, the exception object that SignalR returns after an error contains minimal information about the error.</span></span> <span data-ttu-id="ee3bd-271">例如，如果调用`newContosoChatMessage`失败，错误对象中的错误消息包含"`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`出于安全原因不建议向生产中的客户端发送详细的错误消息，但如果要启用详细的错误消息以进行故障排除，请使用服务器上的以下代码。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-271">For example, if a call to `newContosoChatMessage` fails, the error message in the error object contains "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" Sending detailed error messages to clients in production is not recommended for security reasons, but if you want to enable detailed error messages for troubleshooting purposes, use the following code on the server.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample31.cs?highlight=2)]

<a id="handleerrors"></a>

<span data-ttu-id="ee3bd-272">要处理 SignalR 引发的错误，可以在连接对象上为`Error`事件添加处理程序。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-272">To handle errors that SignalR raises, you can add a handler for the `Error` event on the connection object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample32.cs)]

<span data-ttu-id="ee3bd-273">要处理方法调用中的错误，请将代码包装在 try-catch 块中。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-273">To handle errors from method invocations, wrap the code in a try-catch block.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample33.cs)]

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a><span data-ttu-id="ee3bd-274">如何启用客户端日志记录</span><span class="sxs-lookup"><span data-stu-id="ee3bd-274">How to enable client-side logging</span></span>

<span data-ttu-id="ee3bd-275">要启用客户端日志记录，在连接对象上`TraceLevel`设置`TraceWriter`和 属性。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-275">To enable client-side logging, set the `TraceLevel` and `TraceWriter` properties on the connection object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample34.cs?highlight=3-4)]

<a id="wpfsl"></a>

## <a name="wpf-silverlight-and-console-application-code-samples-for-client-methods-that-the-server-can-call"></a><span data-ttu-id="ee3bd-276">WPF、Silverlight 和控制台应用程序代码示例，用于服务器可以调用的客户端方法</span><span class="sxs-lookup"><span data-stu-id="ee3bd-276">WPF, Silverlight, and console application code samples for client methods that the server can call</span></span>

<span data-ttu-id="ee3bd-277">前面显示的代码示例用于定义服务器可以调用的客户端方法，应用于 WinRT 客户端。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-277">The code samples shown earlier for defining client methods that the server can call apply to WinRT clients.</span></span> <span data-ttu-id="ee3bd-278">以下示例显示了 WPF、Silverlight 和控制台应用程序客户端的等效代码。</span><span class="sxs-lookup"><span data-stu-id="ee3bd-278">The following samples show the equivalent code for WPF, Silverlight, and console application clients.</span></span>

### <a name="methods-without-parameters"></a><span data-ttu-id="ee3bd-279">没有参数的方法</span><span class="sxs-lookup"><span data-stu-id="ee3bd-279">Methods without parameters</span></span>

<span data-ttu-id="ee3bd-280">**WPF 客户端代码，用于从服务器调用无参数的方法**</span><span class="sxs-lookup"><span data-stu-id="ee3bd-280">**WPF client code for method called from server without parameters**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample35.cs?highlight=1)]

<span data-ttu-id="ee3bd-281">**银光客户端代码，用于从服务器调用无参数的方法**</span><span class="sxs-lookup"><span data-stu-id="ee3bd-281">**Silverlight client code for method called from server without parameters**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample36.cs?highlight=1)]

<span data-ttu-id="ee3bd-282">**控制台应用程序客户端代码，用于从服务器调用无参数的方法**</span><span class="sxs-lookup"><span data-stu-id="ee3bd-282">**Console application client code for method called from server without parameters**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample37.cs?highlight=1)]

### <a name="methods-with-parameters-specifying-the-parameter-types"></a><span data-ttu-id="ee3bd-283">具有参数的方法，指定参数类型</span><span class="sxs-lookup"><span data-stu-id="ee3bd-283">Methods with parameters, specifying the parameter types</span></span>

<span data-ttu-id="ee3bd-284">**WPF 客户端代码，用于从具有参数的服务器调用的方法**</span><span class="sxs-lookup"><span data-stu-id="ee3bd-284">**WPF client code for a method called from server with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample38.cs?highlight=1,4)]

<span data-ttu-id="ee3bd-285">**使用参数从服务器调用的方法的 Silverlight 客户端代码**</span><span class="sxs-lookup"><span data-stu-id="ee3bd-285">**Silverlight client code for a method called from server with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample39.cs?highlight=1,5)]

<span data-ttu-id="ee3bd-286">**控制台应用程序客户端代码，用于从具有参数的服务器调用的方法**</span><span class="sxs-lookup"><span data-stu-id="ee3bd-286">**Console application client code for a method called from server with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample40.cs?highlight=1-2)]

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a><span data-ttu-id="ee3bd-287">具有参数的方法，为参数指定动态对象</span><span class="sxs-lookup"><span data-stu-id="ee3bd-287">Methods with parameters, specifying dynamic objects for the parameters</span></span>

<span data-ttu-id="ee3bd-288">**使用参数的动态对象从服务器调用的方法的 WPF 客户端代码**</span><span class="sxs-lookup"><span data-stu-id="ee3bd-288">**WPF client code for a method called from server with a parameter, using a dynamic object for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample41.cs?highlight=1,4)]

<span data-ttu-id="ee3bd-289">**使用参数的动态对象从服务器调用的方法的 Silverlight 客户端代码**</span><span class="sxs-lookup"><span data-stu-id="ee3bd-289">**Silverlight client code for a method called from server with a parameter, using a dynamic object for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample42.cs?highlight=1,5)]

<span data-ttu-id="ee3bd-290">**使用参数的动态对象从服务器调用的方法的控制台应用程序客户端代码**</span><span class="sxs-lookup"><span data-stu-id="ee3bd-290">**Console application client code for a method called from server with a parameter, using a dynamic object for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample43.cs?highlight=1-2)]

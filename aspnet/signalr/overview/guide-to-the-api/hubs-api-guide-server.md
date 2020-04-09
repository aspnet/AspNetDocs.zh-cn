---
uid: signalr/overview/guide-to-the-api/hubs-api-guide-server
title: ASP.NET信号器集线器 API 指南 - 服务器 （C#） |微软文档
author: bradygaster
description: 本文档介绍了为 SignalR 版本 2 编写ASP.NET信号R 集线器 API 的服务器端，并演示了代码示例...
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: b19913e5-cd8a-4e4b-a872-5ac7a858a934
msc.legacyurl: /signalr/overview/guide-to-the-api/hubs-api-guide-server
msc.type: authoredcontent
ms.openlocfilehash: c681b104b15bfc4a04587c7abf685dcf20def2ca
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675801"
---
# <a name="aspnet-signalr-hubs-api-guide---server-c"></a><span data-ttu-id="2c251-103">ASP.NET信号器集线器 API 指南 - 服务器 （C#）</span><span class="sxs-lookup"><span data-stu-id="2c251-103">ASP.NET SignalR Hubs API Guide - Server (C#)</span></span>

<span data-ttu-id="2c251-104">由[帕特里克·弗莱彻](https://github.com/pfletcher)，[汤姆·戴克斯特拉](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="2c251-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom Dykstra](https://github.com/tdykstra)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="2c251-105">本文档介绍了为 SignalR 版本 2 编写ASP.NET信号R 集线器 API 的服务器端，并演示了常见选项的代码示例。</span><span class="sxs-lookup"><span data-stu-id="2c251-105">This document provides an introduction to programming the server side of the ASP.NET SignalR Hubs API for SignalR version 2, with code samples demonstrating common options.</span></span>
> 
> <span data-ttu-id="2c251-106">SignalR 集线器 API 使您能够从服务器对连接的客户端以及从客户端到服务器进行远程过程调用 （RPC）。</span><span class="sxs-lookup"><span data-stu-id="2c251-106">The SignalR Hubs API enables you to make remote procedure calls (RPCs) from a server to connected clients and from clients to the server.</span></span> <span data-ttu-id="2c251-107">在服务器代码中，定义客户端可以调用的方法，并调用在客户端上运行的方法。</span><span class="sxs-lookup"><span data-stu-id="2c251-107">In server code, you define methods that can be called by clients, and you call methods that run on the client.</span></span> <span data-ttu-id="2c251-108">在客户端代码中，定义可以从服务器调用的方法，并调用在服务器上运行的方法。</span><span class="sxs-lookup"><span data-stu-id="2c251-108">In client code, you define methods that can be called from the server, and you call methods that run on the server.</span></span> <span data-ttu-id="2c251-109">SignalR 为您处理所有客户端到服务器管道。</span><span class="sxs-lookup"><span data-stu-id="2c251-109">SignalR takes care of all of the client-to-server plumbing for you.</span></span>
> 
> <span data-ttu-id="2c251-110">SignalR 还提供称为持久连接的较低级别的 API。</span><span class="sxs-lookup"><span data-stu-id="2c251-110">SignalR also offers a lower-level API called Persistent Connections.</span></span> <span data-ttu-id="2c251-111">有关信号R、集线器和持久连接的介绍，请参阅[信号R 2 简介](../getting-started/introduction-to-signalr.md)。</span><span class="sxs-lookup"><span data-stu-id="2c251-111">For an introduction to SignalR, Hubs, and Persistent Connections, see [Introduction to SignalR 2](../getting-started/introduction-to-signalr.md).</span></span>
> 
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="2c251-112">本主题中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="2c251-112">Software versions used in this topic</span></span>
> 
> 
> - [<span data-ttu-id="2c251-113">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="2c251-113">Visual Studio 2013</span></span>](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - <span data-ttu-id="2c251-114">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="2c251-114">.NET 4.5</span></span>
> - <span data-ttu-id="2c251-115">信号R版本 2</span><span class="sxs-lookup"><span data-stu-id="2c251-115">SignalR version 2</span></span>
>   
> 
> 
> ## <a name="topic-versions"></a><span data-ttu-id="2c251-116">主题版本</span><span class="sxs-lookup"><span data-stu-id="2c251-116">Topic versions</span></span>
> 
> <span data-ttu-id="2c251-117">有关早期版本的 SignalR 的信息，请参阅[SignalR 旧版本](../older-versions/index.md)。</span><span class="sxs-lookup"><span data-stu-id="2c251-117">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
> 
> ## <a name="questions-and-comments"></a><span data-ttu-id="2c251-118">问题和评论</span><span class="sxs-lookup"><span data-stu-id="2c251-118">Questions and comments</span></span>
> 
> <span data-ttu-id="2c251-119">请留下反馈，关于你喜欢本教程的方式，以及我们可以在页面底部的评论中改进什么。</span><span class="sxs-lookup"><span data-stu-id="2c251-119">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="2c251-120">如果您有与本教程没有直接关系的问题，您可以将它们发布到[ASP.NET SignalR 论坛](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com/)。</span><span class="sxs-lookup"><span data-stu-id="2c251-120">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="overview"></a><span data-ttu-id="2c251-121">概述</span><span class="sxs-lookup"><span data-stu-id="2c251-121">Overview</span></span>

<span data-ttu-id="2c251-122">本文档包含以下各节：</span><span class="sxs-lookup"><span data-stu-id="2c251-122">This document contains the following sections:</span></span>

- [<span data-ttu-id="2c251-123">如何注册SignalR中间件</span><span class="sxs-lookup"><span data-stu-id="2c251-123">How to register SignalR middleware</span></span>](#route)

    - [<span data-ttu-id="2c251-124">/信号器 URL</span><span class="sxs-lookup"><span data-stu-id="2c251-124">The /signalr URL</span></span>](#signalrurl)
    - [<span data-ttu-id="2c251-125">配置信号R选项</span><span class="sxs-lookup"><span data-stu-id="2c251-125">Configuring SignalR options</span></span>](#options)
- [<span data-ttu-id="2c251-126">如何创建和使用中心类</span><span class="sxs-lookup"><span data-stu-id="2c251-126">How to create and use Hub classes</span></span>](#hubclass)

    - [<span data-ttu-id="2c251-127">中心对象生存期</span><span class="sxs-lookup"><span data-stu-id="2c251-127">Hub object lifetime</span></span>](#transience)
    - [<span data-ttu-id="2c251-128">JavaScript 客户端中中心名称的骆驼大小写</span><span class="sxs-lookup"><span data-stu-id="2c251-128">Camel-casing of Hub names in JavaScript clients</span></span>](#hubnames)
    - [<span data-ttu-id="2c251-129">多个中心</span><span class="sxs-lookup"><span data-stu-id="2c251-129">Multiple Hubs</span></span>](#multiplehubs)
    - [<span data-ttu-id="2c251-130">强类型集线器</span><span class="sxs-lookup"><span data-stu-id="2c251-130">Strongly-Typed Hubs</span></span>](#stronglytypedhubs)
- [<span data-ttu-id="2c251-131">如何在中心类中定义客户端可以调用的方法</span><span class="sxs-lookup"><span data-stu-id="2c251-131">How to define methods in the Hub class that clients can call</span></span>](#hubmethods)

    - [<span data-ttu-id="2c251-132">JavaScript 客户端中方法名称的骆驼大小写</span><span class="sxs-lookup"><span data-stu-id="2c251-132">Camel-casing of method names in JavaScript clients</span></span>](#methodnames)
    - [<span data-ttu-id="2c251-133">何时异步执行</span><span class="sxs-lookup"><span data-stu-id="2c251-133">When to execute asynchronously</span></span>](#asyncmethods)
    - [<span data-ttu-id="2c251-134">定义重载</span><span class="sxs-lookup"><span data-stu-id="2c251-134">Defining overloads</span></span>](#overloads)
    - [<span data-ttu-id="2c251-135">报告中心方法调用的进度</span><span class="sxs-lookup"><span data-stu-id="2c251-135">Reporting progress from hub method invocations</span></span>](#progress)
- [<span data-ttu-id="2c251-136">如何从中心类调用客户端方法</span><span class="sxs-lookup"><span data-stu-id="2c251-136">How to call client methods from the Hub class</span></span>](#callfromhub)

    - [<span data-ttu-id="2c251-137">选择哪些客户端将收到 RPC</span><span class="sxs-lookup"><span data-stu-id="2c251-137">Selecting which clients will receive the RPC</span></span>](#selectingclients)
    - [<span data-ttu-id="2c251-138">方法名称没有编译时间验证</span><span class="sxs-lookup"><span data-stu-id="2c251-138">No compile-time validation for method names</span></span>](#dynamicmethodnames)
    - [<span data-ttu-id="2c251-139">区分大小写的方法名称匹配</span><span class="sxs-lookup"><span data-stu-id="2c251-139">Case-insensitive method name matching</span></span>](#caseinsensitive)
    - [<span data-ttu-id="2c251-140">异步执行</span><span class="sxs-lookup"><span data-stu-id="2c251-140">Asynchronous execution</span></span>](#asyncclient)
- [<span data-ttu-id="2c251-141">如何从中心类管理组成员身份</span><span class="sxs-lookup"><span data-stu-id="2c251-141">How to manage group membership from the Hub class</span></span>](#groupsfromhub)

    - [<span data-ttu-id="2c251-142">添加和删除方法的异步执行</span><span class="sxs-lookup"><span data-stu-id="2c251-142">Asynchronous execution of Add and Remove methods</span></span>](#asyncgroupmethods)
    - [<span data-ttu-id="2c251-143">组成员身份持久性</span><span class="sxs-lookup"><span data-stu-id="2c251-143">Group membership persistence</span></span>](#grouppersistence)
    - [<span data-ttu-id="2c251-144">单用户组</span><span class="sxs-lookup"><span data-stu-id="2c251-144">Single-user groups</span></span>](#singleusergroups)
- [<span data-ttu-id="2c251-145">如何处理集线器类中的连接生存期事件</span><span class="sxs-lookup"><span data-stu-id="2c251-145">How to handle connection lifetime events in the Hub class</span></span>](#connectionlifetime)

    - [<span data-ttu-id="2c251-146">当"连接"时，打开断开状态，并调用"重新连接"</span><span class="sxs-lookup"><span data-stu-id="2c251-146">When OnConnected, OnDisconnected, and OnReconnected are called</span></span>](#onreconnected)
    - [<span data-ttu-id="2c251-147">未填充的呼叫者状态</span><span class="sxs-lookup"><span data-stu-id="2c251-147">Caller state not populated</span></span>](#nocallerstate)
- [<span data-ttu-id="2c251-148">如何从上下文属性获取有关客户端的信息</span><span class="sxs-lookup"><span data-stu-id="2c251-148">How to get information about the client from the Context property</span></span>](#contextproperty)
- [<span data-ttu-id="2c251-149">如何在客户端和中心类之间传递状态</span><span class="sxs-lookup"><span data-stu-id="2c251-149">How to pass state between clients and the Hub class</span></span>](#passstate)
- [<span data-ttu-id="2c251-150">如何处理中心类中的错误</span><span class="sxs-lookup"><span data-stu-id="2c251-150">How to handle errors in the Hub class</span></span>](#handleErrors)
- [<span data-ttu-id="2c251-151">如何调用客户端方法并管理来自中心类外部的组</span><span class="sxs-lookup"><span data-stu-id="2c251-151">How to call client methods and manage groups from outside the Hub class</span></span>](#callfromoutsidehub)

    - [<span data-ttu-id="2c251-152">调用客户端方法</span><span class="sxs-lookup"><span data-stu-id="2c251-152">Calling client methods</span></span>](#callingclientsoutsidehub)
    - [<span data-ttu-id="2c251-153">管理组成员身份</span><span class="sxs-lookup"><span data-stu-id="2c251-153">Managing group membership</span></span>](#managinggroupsoutsidehub)
- [<span data-ttu-id="2c251-154">如何启用跟踪</span><span class="sxs-lookup"><span data-stu-id="2c251-154">How to enable tracing</span></span>](#tracing)
- [<span data-ttu-id="2c251-155">如何自定义中心管道</span><span class="sxs-lookup"><span data-stu-id="2c251-155">How to customize the Hubs pipeline</span></span>](#hubpipeline)

<span data-ttu-id="2c251-156">有关如何对客户端进行编程的文档，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="2c251-156">For documentation on how to program clients, see the following resources:</span></span>

- [<span data-ttu-id="2c251-157">信号器中心 API 指南 - JavaScript 客户端</span><span class="sxs-lookup"><span data-stu-id="2c251-157">SignalR Hubs API Guide - JavaScript Client</span></span>](hubs-api-guide-javascript-client.md)
- [<span data-ttu-id="2c251-158">信号器集线器 API 指南 - .NET 客户端</span><span class="sxs-lookup"><span data-stu-id="2c251-158">SignalR Hubs API Guide - .NET Client</span></span>](hubs-api-guide-net-client.md)

<span data-ttu-id="2c251-159">SignalR 2 的服务器组件仅在 .NET 4.5 中可用。</span><span class="sxs-lookup"><span data-stu-id="2c251-159">The server components for SignalR 2 are only available in .NET 4.5.</span></span> <span data-ttu-id="2c251-160">运行 .NET 4.0 的服务器必须使用 SignalR v1.x。</span><span class="sxs-lookup"><span data-stu-id="2c251-160">Servers running .NET 4.0 must use SignalR v1.x.</span></span>

<a id="route"></a>

## <a name="how-to-register-signalr-middleware"></a><span data-ttu-id="2c251-161">如何注册SignalR中间件</span><span class="sxs-lookup"><span data-stu-id="2c251-161">How to register SignalR middleware</span></span>

<span data-ttu-id="2c251-162">要定义客户端将用于连接到集线器的路由，请在`MapSignalR`应用程序启动时调用 方法。</span><span class="sxs-lookup"><span data-stu-id="2c251-162">To define the route that clients will use to connect to your Hub, call the `MapSignalR` method when the application starts.</span></span> <span data-ttu-id="2c251-163">`MapSignalR`是类的`OwinExtensions`[扩展方法](https://msdn.microsoft.com/library/vstudio/bb383977.aspx)。</span><span class="sxs-lookup"><span data-stu-id="2c251-163">`MapSignalR` is an [extension method](https://msdn.microsoft.com/library/vstudio/bb383977.aspx) for the `OwinExtensions` class.</span></span> <span data-ttu-id="2c251-164">下面的示例演示如何使用 OWIN 启动类定义 SignalR 中心路由。</span><span class="sxs-lookup"><span data-stu-id="2c251-164">The following example shows how to define the SignalR Hubs route using an OWIN startup class.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample1.cs)]

<span data-ttu-id="2c251-165">如果要将 SignalR 功能添加到ASP.NET MVC 应用程序，请确保在其他路由之前添加 SignalR 路由。</span><span class="sxs-lookup"><span data-stu-id="2c251-165">If you are adding SignalR functionality to an ASP.NET MVC application, make sure that the SignalR route is added before the other routes.</span></span> <span data-ttu-id="2c251-166">有关详细信息，请参阅[教程：开始使用 SignalR 2 和 MVC 5](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)。</span><span class="sxs-lookup"><span data-stu-id="2c251-166">For more information, see [Tutorial: Getting Started with SignalR 2 and MVC 5](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md).</span></span>

<a id="signalrurl"></a>

### <a name="the-signalr-url"></a><span data-ttu-id="2c251-167">/信号器 URL</span><span class="sxs-lookup"><span data-stu-id="2c251-167">The /signalr URL</span></span>

<span data-ttu-id="2c251-168">默认情况下，客户端将用于连接到集线器的路由 URL 为"/信号器"。</span><span class="sxs-lookup"><span data-stu-id="2c251-168">By default, the route URL which clients will use to connect to your Hub is "/signalr".</span></span> <span data-ttu-id="2c251-169">（不要将此 URL 与"/信号器/集线器"URL 混淆，该 URL 适用于自动生成的 JavaScript 文件。</span><span class="sxs-lookup"><span data-stu-id="2c251-169">(Don't confuse this URL with the "/signalr/hubs" URL, which is for the automatically generated JavaScript file.</span></span> <span data-ttu-id="2c251-170">有关生成的代理的详细信息，请参阅[SignalR 中心 API 指南 - JavaScript 客户端 - 生成的代理及其为您做什么](hubs-api-guide-javascript-client.md#genproxy)。</span><span class="sxs-lookup"><span data-stu-id="2c251-170">For more information about the generated proxy, see [SignalR Hubs API Guide - JavaScript Client - The generated proxy and what it does for you](hubs-api-guide-javascript-client.md#genproxy).)</span></span>

<span data-ttu-id="2c251-171">可能存在异常情况，使此基 URL 不适用于 SignalR;例如，项目中有一个名为*信号器*的文件夹，并且不想更改名称。</span><span class="sxs-lookup"><span data-stu-id="2c251-171">There might be extraordinary circumstances that make this base URL not usable for SignalR; for example, you have a folder in your project named *signalr* and you don't want to change the name.</span></span> <span data-ttu-id="2c251-172">在这种情况下，您可以更改基本 URL，如以下示例所示（将示例代码中的"/信号器"替换为所需的 URL）。</span><span class="sxs-lookup"><span data-stu-id="2c251-172">In that case, you can change the base URL, as shown in the following examples (replace "/signalr" in the sample code with your desired URL).</span></span>

<span data-ttu-id="2c251-173">**指定 URL 的服务器代码**</span><span class="sxs-lookup"><span data-stu-id="2c251-173">**Server code that specifies the URL**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample2.cs?highlight=1)]

<span data-ttu-id="2c251-174">**指定 URL 的 JavaScript 客户端代码（使用生成的代理）**</span><span class="sxs-lookup"><span data-stu-id="2c251-174">**JavaScript client code that specifies the URL (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample3.js?highlight=1)]

<span data-ttu-id="2c251-175">**指定 URL 的 JavaScript 客户端代码（没有生成的代理）**</span><span class="sxs-lookup"><span data-stu-id="2c251-175">**JavaScript client code that specifies the URL (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample4.js?highlight=1)]

<span data-ttu-id="2c251-176">**指定 URL 的 .NET 客户端代码**</span><span class="sxs-lookup"><span data-stu-id="2c251-176">**.NET client code that specifies the URL**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample5.cs?highlight=1)]

<a id="options"></a>

### <a name="configuring-signalr-options"></a><span data-ttu-id="2c251-177">配置信号灯选项</span><span class="sxs-lookup"><span data-stu-id="2c251-177">Configuring SignalR Options</span></span>

<span data-ttu-id="2c251-178">`MapSignalR`方法的重载使您能够指定自定义 URL、自定义依赖项解析器以及以下选项：</span><span class="sxs-lookup"><span data-stu-id="2c251-178">Overloads of the `MapSignalR` method enable you to specify a custom URL, a custom dependency resolver, and the following options:</span></span>

- <span data-ttu-id="2c251-179">使用浏览器客户端的 CORS 或 JSONP 启用跨域调用。</span><span class="sxs-lookup"><span data-stu-id="2c251-179">Enable cross-domain calls using CORS or JSONP from browser clients.</span></span>

    <span data-ttu-id="2c251-180">通常，如果浏览器从`http://contoso.com`加载页面，则 SignalR 连接位于同一域中`http://contoso.com/signalr`，在 。</span><span class="sxs-lookup"><span data-stu-id="2c251-180">Typically if the browser loads a page from `http://contoso.com`, the SignalR connection is in the same domain, at `http://contoso.com/signalr`.</span></span> <span data-ttu-id="2c251-181">如果 中的`http://contoso.com`页面与`http://fabrikam.com/signalr`断开连接，则为跨域连接。</span><span class="sxs-lookup"><span data-stu-id="2c251-181">If the page from `http://contoso.com` makes a connection to `http://fabrikam.com/signalr`, that is a cross-domain connection.</span></span> <span data-ttu-id="2c251-182">出于安全原因，默认情况下禁用跨域连接。</span><span class="sxs-lookup"><span data-stu-id="2c251-182">For security reasons, cross-domain connections are disabled by default.</span></span> <span data-ttu-id="2c251-183">有关详细信息，请参阅[ASP.NET信号R中心 API 指南 - JavaScript 客户端 - 如何建立跨域连接](hubs-api-guide-javascript-client.md#crossdomain)。</span><span class="sxs-lookup"><span data-stu-id="2c251-183">For more information, see [ASP.NET SignalR Hubs API Guide - JavaScript Client - How to establish a cross-domain connection](hubs-api-guide-javascript-client.md#crossdomain).</span></span>
- <span data-ttu-id="2c251-184">启用详细的错误消息。</span><span class="sxs-lookup"><span data-stu-id="2c251-184">Enable detailed error messages.</span></span>

    <span data-ttu-id="2c251-185">发生错误时，SignalR 的默认行为是向客户端发送通知消息，而不详细说明发生的情况。</span><span class="sxs-lookup"><span data-stu-id="2c251-185">When errors occur, the default behavior of SignalR is to send to clients a notification message without details about what happened.</span></span> <span data-ttu-id="2c251-186">在生产中不建议向客户端发送详细的错误信息，因为恶意用户可能能够在针对应用程序的攻击中使用该信息。</span><span class="sxs-lookup"><span data-stu-id="2c251-186">Sending detailed error information to clients is not recommended in production, because malicious users might be able to use the information in attacks against your application.</span></span> <span data-ttu-id="2c251-187">对于故障排除，可以使用此选项暂时启用信息量更大的错误报告。</span><span class="sxs-lookup"><span data-stu-id="2c251-187">For troubleshooting, you can use this option to temporarily enable more informative error reporting.</span></span>
- <span data-ttu-id="2c251-188">禁用自动生成的 JavaScript 代理文件。</span><span class="sxs-lookup"><span data-stu-id="2c251-188">Disable automatically generated JavaScript proxy files.</span></span>

    <span data-ttu-id="2c251-189">默认情况下，将生成具有中心类代理的 JavaScript 文件，以响应 URL"/信号器/集线器"。</span><span class="sxs-lookup"><span data-stu-id="2c251-189">By default, a JavaScript file with proxies for your Hub classes is generated in response to the URL "/signalr/hubs".</span></span> <span data-ttu-id="2c251-190">如果不想使用 JavaScript 代理，或者要手动生成此文件并引用客户端中的物理文件，则可以使用此选项禁用代理生成。</span><span class="sxs-lookup"><span data-stu-id="2c251-190">If you don't want to use the JavaScript proxies, or if you want to generate this file manually and refer to a physical file in your clients, you can use this option to disable proxy generation.</span></span> <span data-ttu-id="2c251-191">有关详细信息，请参阅[SignalR 中心 API 指南 - JavaScript 客户端 - 如何为 SignalR 生成的代理创建物理文件](hubs-api-guide-javascript-client.md#manualproxy)。</span><span class="sxs-lookup"><span data-stu-id="2c251-191">For more information, see [SignalR Hubs API Guide - JavaScript Client - How to create a physical file for the SignalR generated proxy](hubs-api-guide-javascript-client.md#manualproxy).</span></span>

<span data-ttu-id="2c251-192">下面的示例演示如何在调用`MapSignalR`方法中指定 SignalR 连接 URL 和这些选项。</span><span class="sxs-lookup"><span data-stu-id="2c251-192">The following example shows how to specify the SignalR connection URL and these options in a call to the `MapSignalR` method.</span></span> <span data-ttu-id="2c251-193">要指定自定义 URL，请将示例中的"/信号器"替换为要使用的 URL。</span><span class="sxs-lookup"><span data-stu-id="2c251-193">To specify a custom URL, replace "/signalr" in the example with the URL that you want to use.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample6.cs)]

<a id="hubclass"></a>

## <a name="how-to-create-and-use-hub-classes"></a><span data-ttu-id="2c251-194">如何创建和使用中心类</span><span class="sxs-lookup"><span data-stu-id="2c251-194">How to create and use Hub classes</span></span>

<span data-ttu-id="2c251-195">要创建集线器，请创建一个派生自[Microsoft 的类。](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx)</span><span class="sxs-lookup"><span data-stu-id="2c251-195">To create a Hub, create a class that derives from [Microsoft.Aspnet.Signalr.Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx).</span></span> <span data-ttu-id="2c251-196">下面的示例显示了聊天应用程序的简单中心类。</span><span class="sxs-lookup"><span data-stu-id="2c251-196">The following example shows a simple Hub class for a chat application.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample7.cs)]

<span data-ttu-id="2c251-197">在此示例中，连接的客户端可以调用`NewContosoChatMessage`方法，当它调用时，接收的数据将广播到所有连接的客户端。</span><span class="sxs-lookup"><span data-stu-id="2c251-197">In this example, a connected client can call the `NewContosoChatMessage` method, and when it does, the data received is broadcasted to all connected clients.</span></span>

<a id="transience"></a>

### <a name="hub-object-lifetime"></a><span data-ttu-id="2c251-198">中心对象生存期</span><span class="sxs-lookup"><span data-stu-id="2c251-198">Hub object lifetime</span></span>

<span data-ttu-id="2c251-199">您不会实例化 Hub 类，也不会从服务器上自己的代码调用其方法;否则，您就不会实例化 Hub 类，所有由 SignalR 中心管道为您完成。</span><span class="sxs-lookup"><span data-stu-id="2c251-199">You don't instantiate the Hub class or call its methods from your own code on the server; all that is done for you by the SignalR Hubs pipeline.</span></span> <span data-ttu-id="2c251-200">SignalR 在每次需要处理集线器操作（例如客户端连接、断开连接或对服务器进行方法调用时）时，都会创建 Hub 类的新实例。</span><span class="sxs-lookup"><span data-stu-id="2c251-200">SignalR creates a new instance of your Hub class each time it needs to handle a Hub operation such as when a client connects, disconnects, or makes a method call to the server.</span></span>

<span data-ttu-id="2c251-201">由于 Hub 类的实例是暂时性的，因此不能使用它们来维护从一个方法调用到下一个方法的状态。</span><span class="sxs-lookup"><span data-stu-id="2c251-201">Because instances of the Hub class are transient, you can't use them to maintain state from one method call to the next.</span></span> <span data-ttu-id="2c251-202">每次服务器收到来自客户端的方法调用时，Hub 类的新实例都会处理该消息。</span><span class="sxs-lookup"><span data-stu-id="2c251-202">Each time the server receives a method call from a client, a new instance of your Hub class processes the message.</span></span> <span data-ttu-id="2c251-203">要通过多个连接和方法调用维护状态，请使用其他方法，如数据库或 Hub 类上的静态变量，或者不派生自`Hub`的不同类。</span><span class="sxs-lookup"><span data-stu-id="2c251-203">To maintain state through multiple connections and method calls, use some other method such as a database, or a static variable on the Hub class, or a different class that does not derive from `Hub`.</span></span> <span data-ttu-id="2c251-204">如果在内存中保留数据，使用 Hub 类上静态变量等方法，则当应用域回收时，数据将丢失。</span><span class="sxs-lookup"><span data-stu-id="2c251-204">If you persist data in memory, using a method such as a static variable on the Hub class, the data will be lost when the app domain recycles.</span></span>

<span data-ttu-id="2c251-205">如果要从在 Hub 类之外运行的您自己的代码向客户端发送消息，不能通过实例化 Hub 类实例来执行此操作，但可以通过获取对 Hub 类的 SignalR 上下文对象的引用来执行此操作。</span><span class="sxs-lookup"><span data-stu-id="2c251-205">If you want to send messages to clients from your own code that runs outside the Hub class, you can't do it by instantiating a Hub class instance, but you can do it by getting a reference to the SignalR context object for your Hub class.</span></span> <span data-ttu-id="2c251-206">有关详细信息，请参阅本主题稍后在[中心类外部调用客户端方法和管理组](#callfromoutsidehub)。</span><span class="sxs-lookup"><span data-stu-id="2c251-206">For more information, see [How to call client methods and manage groups from outside the Hub class](#callfromoutsidehub) later in this topic.</span></span>

<a id="hubnames"></a>

### <a name="camel-casing-of-hub-names-in-javascript-clients"></a><span data-ttu-id="2c251-207">JavaScript 客户端中中心名称的骆驼大小写</span><span class="sxs-lookup"><span data-stu-id="2c251-207">Camel-casing of Hub names in JavaScript clients</span></span>

<span data-ttu-id="2c251-208">默认情况下，JavaScript 客户端使用类名称的骆驼大小写版本引用集线器。</span><span class="sxs-lookup"><span data-stu-id="2c251-208">By default, JavaScript clients refer to Hubs by using a camel-cased version of the class name.</span></span> <span data-ttu-id="2c251-209">SignalR 会自动进行此更改，以便 JavaScript 代码可以符合 JavaScript 约定。</span><span class="sxs-lookup"><span data-stu-id="2c251-209">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span> <span data-ttu-id="2c251-210">前面的示例将称为`contosoChatHub`JavaScript 代码。</span><span class="sxs-lookup"><span data-stu-id="2c251-210">The previous example would be referred to as `contosoChatHub` in JavaScript code.</span></span>

<span data-ttu-id="2c251-211">**Server**</span><span class="sxs-lookup"><span data-stu-id="2c251-211">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample8.cs?highlight=1)]

<span data-ttu-id="2c251-212">**使用生成的代理的 JavaScript 客户端**</span><span class="sxs-lookup"><span data-stu-id="2c251-212">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample9.js?highlight=1)]

<span data-ttu-id="2c251-213">如果要为客户端指定要使用的其他名称，请添加该`HubName`属性。</span><span class="sxs-lookup"><span data-stu-id="2c251-213">If you want to specify a different name for clients to use, add the `HubName` attribute.</span></span> <span data-ttu-id="2c251-214">使用`HubName`属性时，JavaScript 客户端上不会更改骆驼大小写的名称。</span><span class="sxs-lookup"><span data-stu-id="2c251-214">When you use a `HubName` attribute, there is no name change to camel case on JavaScript clients.</span></span>

<span data-ttu-id="2c251-215">**Server**</span><span class="sxs-lookup"><span data-stu-id="2c251-215">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample10.cs?highlight=1)]

<span data-ttu-id="2c251-216">**使用生成的代理的 JavaScript 客户端**</span><span class="sxs-lookup"><span data-stu-id="2c251-216">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample11.js?highlight=1)]

<a id="multiplehubs"></a>

### <a name="multiple-hubs"></a><span data-ttu-id="2c251-217">多个中心</span><span class="sxs-lookup"><span data-stu-id="2c251-217">Multiple Hubs</span></span>

<span data-ttu-id="2c251-218">您可以在应用程序中定义多个中心类。</span><span class="sxs-lookup"><span data-stu-id="2c251-218">You can define multiple Hub classes in an application.</span></span> <span data-ttu-id="2c251-219">执行此操作时，连接是共享的，但组是独立的：</span><span class="sxs-lookup"><span data-stu-id="2c251-219">When you do that, the connection is shared but groups are separate:</span></span>

- <span data-ttu-id="2c251-220">所有客户端都将使用相同的 URL 与服务建立 SignalR 连接（"/信号器"或自定义 URL（如果您指定了一个），并且该连接用于服务定义的所有中心。</span><span class="sxs-lookup"><span data-stu-id="2c251-220">All clients will use the same URL to establish a SignalR connection with your service ("/signalr" or your custom URL if you specified one), and that connection is used for all Hubs defined by the service.</span></span>

    <span data-ttu-id="2c251-221">与在单个类中定义所有中心功能相比，多个中心的性能差异没有差异。</span><span class="sxs-lookup"><span data-stu-id="2c251-221">There is no performance difference for multiple Hubs compared to defining all Hub functionality in a single class.</span></span>
- <span data-ttu-id="2c251-222">所有中心都获取相同的 HTTP 请求信息。</span><span class="sxs-lookup"><span data-stu-id="2c251-222">All Hubs get the same HTTP request information.</span></span>

    <span data-ttu-id="2c251-223">由于所有集线器共享相同的连接，因此服务器获得的唯一 HTTP 请求信息是建立 SignalR 连接的原始 HTTP 请求中的内容。</span><span class="sxs-lookup"><span data-stu-id="2c251-223">Since all Hubs share the same connection, the only HTTP request information that the server gets is what comes in the original HTTP request that establishes the SignalR connection.</span></span> <span data-ttu-id="2c251-224">如果使用连接请求通过指定查询字符串将信息从客户端传递到服务器，则不能向不同的中心提供不同的查询字符串。</span><span class="sxs-lookup"><span data-stu-id="2c251-224">If you use the connection request to pass information from the client to the server by specifying a query string, you can't provide different query strings to different Hubs.</span></span> <span data-ttu-id="2c251-225">所有中心都将收到相同的信息。</span><span class="sxs-lookup"><span data-stu-id="2c251-225">All Hubs will receive the same information.</span></span>
- <span data-ttu-id="2c251-226">生成的 JavaScript 代理文件将包含一个文件中所有中心代理。</span><span class="sxs-lookup"><span data-stu-id="2c251-226">The generated JavaScript proxies file will contain proxies for all Hubs in one file.</span></span>

    <span data-ttu-id="2c251-227">有关 JavaScript 代理的信息，请参阅[SignalR 中心 API 指南 - JavaScript 客户端 - 生成的代理及其为您做什么](hubs-api-guide-javascript-client.md#genproxy)。</span><span class="sxs-lookup"><span data-stu-id="2c251-227">For information about JavaScript proxies, see [SignalR Hubs API Guide - JavaScript Client - The generated proxy and what it does for you](hubs-api-guide-javascript-client.md#genproxy).</span></span>
- <span data-ttu-id="2c251-228">组在中心内定义。</span><span class="sxs-lookup"><span data-stu-id="2c251-228">Groups are defined within Hubs.</span></span>

    <span data-ttu-id="2c251-229">在 SignalR 中，您可以定义要广播到连接客户端子集的命名组。</span><span class="sxs-lookup"><span data-stu-id="2c251-229">In SignalR you can define named groups to broadcast to subsets of connected clients.</span></span> <span data-ttu-id="2c251-230">每个中心分别维护组。</span><span class="sxs-lookup"><span data-stu-id="2c251-230">Groups are maintained separately for each Hub.</span></span> <span data-ttu-id="2c251-231">例如，名为"管理员"的组将包含类`ContosoChatHub`的一组客户端，而相同的组名称将引用类`StockTickerHub`的不同客户端集。</span><span class="sxs-lookup"><span data-stu-id="2c251-231">For example, a group named "Administrators" would include one set of clients for your `ContosoChatHub` class, and the same group name would refer to a different set of clients for your `StockTickerHub` class.</span></span>

<a id="stronglytypedhubs"></a>
### <a name="strongly-typed-hubs"></a><span data-ttu-id="2c251-232">强类型集线器</span><span class="sxs-lookup"><span data-stu-id="2c251-232">Strongly-Typed Hubs</span></span>

<span data-ttu-id="2c251-233">要为客户端可以引用的集线器方法定义接口（并在集线器方法上启用 Intellisense），请从`Hub<T>`（在 SignalR 2.1 中`Hub`引入） 而不是 派生中心。</span><span class="sxs-lookup"><span data-stu-id="2c251-233">To define an interface for your hub methods that your client can reference (and enable Intellisense on your hub methods), derive your hub from `Hub<T>` (introduced in SignalR 2.1) rather than `Hub`:</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample12.cs)]

<a id="hubmethods"></a>

## <a name="how-to-define-methods-in-the-hub-class-that-clients-can-call"></a><span data-ttu-id="2c251-234">如何在中心类中定义客户端可以调用的方法</span><span class="sxs-lookup"><span data-stu-id="2c251-234">How to define methods in the Hub class that clients can call</span></span>

<span data-ttu-id="2c251-235">要在 Hub 上公开要从客户端调用的方法，请声明公共方法，如以下示例所示。</span><span class="sxs-lookup"><span data-stu-id="2c251-235">To expose a method on the Hub that you want to be callable from the client, declare a public method, as shown in the following examples.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample13.cs?highlight=3)]

[!code-csharp[Main](hubs-api-guide-server/samples/sample14.cs?highlight=3)]

<span data-ttu-id="2c251-236">您可以指定返回类型和参数，包括复杂类型和数组，就像在任何 C# 方法中一样。</span><span class="sxs-lookup"><span data-stu-id="2c251-236">You can specify a return type and parameters, including complex types and arrays, as you would in any C# method.</span></span> <span data-ttu-id="2c251-237">使用 JSON 在客户端和服务器之间通信以参数接收或返回到调用方的任何数据，SignalR 会自动处理复杂对象和对象数组的绑定。</span><span class="sxs-lookup"><span data-stu-id="2c251-237">Any data that you receive in parameters or return to the caller is communicated between the client and the server by using JSON, and SignalR handles the binding of complex objects and arrays of objects automatically.</span></span>

<a id="methodnames"></a>

### <a name="camel-casing-of-method-names-in-javascript-clients"></a><span data-ttu-id="2c251-238">JavaScript 客户端中方法名称的骆驼大小写</span><span class="sxs-lookup"><span data-stu-id="2c251-238">Camel-casing of method names in JavaScript clients</span></span>

<span data-ttu-id="2c251-239">默认情况下，JavaScript 客户端使用方法名称的骆驼大小写版本引用 Hub 方法。</span><span class="sxs-lookup"><span data-stu-id="2c251-239">By default, JavaScript clients refer to Hub methods by using a camel-cased version of the method name.</span></span> <span data-ttu-id="2c251-240">SignalR 会自动进行此更改，以便 JavaScript 代码可以符合 JavaScript 约定。</span><span class="sxs-lookup"><span data-stu-id="2c251-240">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span>

<span data-ttu-id="2c251-241">**Server**</span><span class="sxs-lookup"><span data-stu-id="2c251-241">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample15.cs?highlight=1)]

<span data-ttu-id="2c251-242">**使用生成的代理的 JavaScript 客户端**</span><span class="sxs-lookup"><span data-stu-id="2c251-242">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample16.js?highlight=1)]

<span data-ttu-id="2c251-243">如果要为客户端指定要使用的其他名称，请添加该`HubMethodName`属性。</span><span class="sxs-lookup"><span data-stu-id="2c251-243">If you want to specify a different name for clients to use, add the `HubMethodName` attribute.</span></span>

<span data-ttu-id="2c251-244">**Server**</span><span class="sxs-lookup"><span data-stu-id="2c251-244">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample17.cs?highlight=1)]

<span data-ttu-id="2c251-245">**使用生成的代理的 JavaScript 客户端**</span><span class="sxs-lookup"><span data-stu-id="2c251-245">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample18.js?highlight=1)]

<a id="asyncmethods"></a>

### <a name="when-to-execute-asynchronously"></a><span data-ttu-id="2c251-246">何时异步执行</span><span class="sxs-lookup"><span data-stu-id="2c251-246">When to execute asynchronously</span></span>

<span data-ttu-id="2c251-247">如果该方法将长时间运行或必须执行需要等待的工作（如数据库查找或 Web 服务调用），则通过返回[任务](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx)（代替`void`返回）或[Task&lt;T&gt;](https://msdn.microsoft.com/library/dd321424.aspx)对象（代替`T`返回类型）使 Hub 方法异步。</span><span class="sxs-lookup"><span data-stu-id="2c251-247">If the method will be long-running or has to do work that would involve waiting, such as a database lookup or a web service call, make the Hub method asynchronous by returning a [Task](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) (in place of `void` return) or [Task&lt;T&gt;](https://msdn.microsoft.com/library/dd321424.aspx) object (in place of `T` return type).</span></span> <span data-ttu-id="2c251-248">当您从 方法`Task`返回对象时，SignalR 会等待`Task`完成，然后它将未包装的结果发送回客户端，因此在客户端中编写方法调用的代码没有区别。</span><span class="sxs-lookup"><span data-stu-id="2c251-248">When you return a `Task` object from the method, SignalR waits for the `Task` to complete, and then it sends the unwrapped result back to the client, so there is no difference in how you code the method call in the client.</span></span>

<span data-ttu-id="2c251-249">使集线器方法异步可避免在使用 WebSocket 传输时阻塞连接。</span><span class="sxs-lookup"><span data-stu-id="2c251-249">Making a Hub method asynchronous avoids blocking the connection when it uses the WebSocket transport.</span></span> <span data-ttu-id="2c251-250">当集线器方法同步执行且传输为 WebSocket 时，从同一客户端在集线器上调用方法将被阻止，直到中心方法完成。</span><span class="sxs-lookup"><span data-stu-id="2c251-250">When a Hub method executes synchronously and the transport is WebSocket, subsequent invocations of methods on the Hub from the same client are blocked until the Hub method completes.</span></span>

<span data-ttu-id="2c251-251">下面的示例显示编码为同步或异步运行的相同方法，然后是适用于调用任一版本的 JavaScript 客户端代码。</span><span class="sxs-lookup"><span data-stu-id="2c251-251">The following example shows the same method coded to run synchronously or asynchronously, followed by JavaScript client code that works for calling either version.</span></span>

<span data-ttu-id="2c251-252">**同步**</span><span class="sxs-lookup"><span data-stu-id="2c251-252">**Synchronous**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample19.cs)]

<span data-ttu-id="2c251-253">**异步**</span><span class="sxs-lookup"><span data-stu-id="2c251-253">**Asynchronous**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample20.cs?highlight=1,7-8)]

<span data-ttu-id="2c251-254">**使用生成的代理的 JavaScript 客户端**</span><span class="sxs-lookup"><span data-stu-id="2c251-254">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample21.js)]

<span data-ttu-id="2c251-255">有关如何在 ASP.NET 4.5 中使用异步方法的详细信息，请参阅[在 mVC 4 中使用异步方法ASP.NET](../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md)。</span><span class="sxs-lookup"><span data-stu-id="2c251-255">For more information about how to use asynchronous methods in ASP.NET 4.5, see [Using Asynchronous Methods in ASP.NET MVC 4](../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md).</span></span>

<a id="overloads"></a>

### <a name="defining-overloads"></a><span data-ttu-id="2c251-256">定义重载</span><span class="sxs-lookup"><span data-stu-id="2c251-256">Defining Overloads</span></span>

<span data-ttu-id="2c251-257">如果要为方法定义重载，则每个重载中的参数数必须不同。</span><span class="sxs-lookup"><span data-stu-id="2c251-257">If you want to define overloads for a method, the number of parameters in each overload must be different.</span></span> <span data-ttu-id="2c251-258">如果仅通过指定不同的参数类型来区分重载，则 Hub 类将编译，但当客户端尝试调用其中一个重载时，SignalR 服务将在运行时引发异常。</span><span class="sxs-lookup"><span data-stu-id="2c251-258">If you differentiate an overload just by specifying different parameter types, your Hub class will compile but the SignalR service will throw an exception at run time when clients try to call one of the overloads.</span></span>

<a id="progress"></a>
### <a name="reporting-progress-from-hub-method-invocations"></a><span data-ttu-id="2c251-259">报告中心方法调用的进度</span><span class="sxs-lookup"><span data-stu-id="2c251-259">Reporting progress from hub method invocations</span></span>

<span data-ttu-id="2c251-260">SignalR 2.1 添加了对 .NET 4.5 中引入[的进度报告模式](https://blogs.msdn.com/b/dotnet/archive/2012/06/06/async-in-4-5-enabling-progress-and-cancellation-in-async-apis.aspx)的支持。</span><span class="sxs-lookup"><span data-stu-id="2c251-260">SignalR 2.1 adds support for the [progress reporting pattern](https://blogs.msdn.com/b/dotnet/archive/2012/06/06/async-in-4-5-enabling-progress-and-cancellation-in-async-apis.aspx) introduced in .NET 4.5.</span></span> <span data-ttu-id="2c251-261">要实现进度报告，请为`IProgress<T>`客户端可以访问的集线器方法定义参数：</span><span class="sxs-lookup"><span data-stu-id="2c251-261">To implement progress reporting, define an `IProgress<T>` parameter for your hub method that your client can access:</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample22.cs)]

<span data-ttu-id="2c251-262">编写长时间运行的服务器方法时，使用异步编程模式（如 Async/Await）而不是阻止中心线程非常重要。</span><span class="sxs-lookup"><span data-stu-id="2c251-262">When writing a long-running server method, it is important to use an asynchronous programming pattern like Async/ Await rather than blocking the hub thread.</span></span>

<a id="callfromhub"></a>

## <a name="how-to-call-client-methods-from-the-hub-class"></a><span data-ttu-id="2c251-263">如何从中心类调用客户端方法</span><span class="sxs-lookup"><span data-stu-id="2c251-263">How to call client methods from the Hub class</span></span>

<span data-ttu-id="2c251-264">要从服务器调用客户端方法，`Clients`请使用 Hub 类中方法中的 属性。</span><span class="sxs-lookup"><span data-stu-id="2c251-264">To call client methods from the server, use the `Clients` property in a method in your Hub class.</span></span> <span data-ttu-id="2c251-265">下面的示例显示调用`addNewMessageToPage`所有连接的客户端的服务器代码，以及定义 JavaScript 客户端中方法的客户端代码。</span><span class="sxs-lookup"><span data-stu-id="2c251-265">The following example shows server code that calls `addNewMessageToPage` on all connected clients, and client code that defines the method in a JavaScript client.</span></span>

<span data-ttu-id="2c251-266">**Server**</span><span class="sxs-lookup"><span data-stu-id="2c251-266">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample23.cs?highlight=5)]

<span data-ttu-id="2c251-267">调用客户端方法是异步操作，并返回 。 `Task`</span><span class="sxs-lookup"><span data-stu-id="2c251-267">Invoking a client method is an asynchronous operation and returns a `Task`.</span></span> <span data-ttu-id="2c251-268">使用 `await`：</span><span class="sxs-lookup"><span data-stu-id="2c251-268">Use `await`:</span></span>

* <span data-ttu-id="2c251-269">确保消息发送时没有错误。</span><span class="sxs-lookup"><span data-stu-id="2c251-269">To ensure the message is sent without error.</span></span> 
* <span data-ttu-id="2c251-270">启用在尝试捕获块中捕获和处理错误。</span><span class="sxs-lookup"><span data-stu-id="2c251-270">To enable catching and handling errors in a try-catch block.</span></span>

<span data-ttu-id="2c251-271">**使用生成的代理的 JavaScript 客户端**</span><span class="sxs-lookup"><span data-stu-id="2c251-271">**JavaScript client using generated proxy**</span></span>

[!code-html[Main](hubs-api-guide-server/samples/sample24.html?highlight=1)]

<span data-ttu-id="2c251-272">无法从客户端方法获取返回值;因此，无法从客户端方法获取返回值。语法，如`int x = Clients.All.add(1,1)`不工作。</span><span class="sxs-lookup"><span data-stu-id="2c251-272">You can't get a return value from a client method; syntax such as `int x = Clients.All.add(1,1)` does not work.</span></span>

<span data-ttu-id="2c251-273">您可以为参数指定复杂的类型和数组。</span><span class="sxs-lookup"><span data-stu-id="2c251-273">You can specify complex types and arrays for the parameters.</span></span> <span data-ttu-id="2c251-274">下面的示例将复杂类型传递给方法参数中的客户端。</span><span class="sxs-lookup"><span data-stu-id="2c251-274">The following example passes a complex type to the client in a method parameter.</span></span>

<span data-ttu-id="2c251-275">**使用复杂对象调用客户端方法的服务器代码**</span><span class="sxs-lookup"><span data-stu-id="2c251-275">**Server code that calls a client method using a complex object**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample25.cs?highlight=3)]

<span data-ttu-id="2c251-276">**定义复杂对象的服务器代码**</span><span class="sxs-lookup"><span data-stu-id="2c251-276">**Server code that defines the complex object**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample26.cs?highlight=1)]

<span data-ttu-id="2c251-277">**使用生成的代理的 JavaScript 客户端**</span><span class="sxs-lookup"><span data-stu-id="2c251-277">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample27.js?highlight=2-3)]

<a id="selectingclients"></a>

### <a name="selecting-which-clients-will-receive-the-rpc"></a><span data-ttu-id="2c251-278">选择哪些客户端将收到 RPC</span><span class="sxs-lookup"><span data-stu-id="2c251-278">Selecting which clients will receive the RPC</span></span>

<span data-ttu-id="2c251-279">客户端属性返回一个[HubConnectionConnection 对象](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx)，该对象提供了多个选项来指定哪些客户端将接收 RPC：</span><span class="sxs-lookup"><span data-stu-id="2c251-279">The Clients property returns a [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx) object that provides several options for specifying which clients will receive the RPC:</span></span>

- <span data-ttu-id="2c251-280">所有已连接的客户端。</span><span class="sxs-lookup"><span data-stu-id="2c251-280">All connected clients.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample28.cs)]
- <span data-ttu-id="2c251-281">仅调用客户端。</span><span class="sxs-lookup"><span data-stu-id="2c251-281">Only the calling client.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample29.cs)]
- <span data-ttu-id="2c251-282">除调用客户端之外的所有客户端。</span><span class="sxs-lookup"><span data-stu-id="2c251-282">All clients except the calling client.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample30.cs)]
- <span data-ttu-id="2c251-283">由连接 ID 标识的特定客户端。</span><span class="sxs-lookup"><span data-stu-id="2c251-283">A specific client identified by connection ID.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample31.css)]

    <span data-ttu-id="2c251-284">此示例调用`addContosoChatMessageToPage`调用客户端，并且与 使用`Clients.Caller`具有相同的效果。</span><span class="sxs-lookup"><span data-stu-id="2c251-284">This example calls `addContosoChatMessageToPage` on the calling client and has the same effect as using `Clients.Caller`.</span></span>
- <span data-ttu-id="2c251-285">除指定客户端外的所有连接客户端，由连接 ID 标识。</span><span class="sxs-lookup"><span data-stu-id="2c251-285">All connected clients except the specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample32.cs)]
- <span data-ttu-id="2c251-286">指定组中的所有连接客户端。</span><span class="sxs-lookup"><span data-stu-id="2c251-286">All connected clients in a specified group.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample33.css)]
- <span data-ttu-id="2c251-287">指定组中的所有连接客户端（指定客户端除外），由连接 ID 标识。</span><span class="sxs-lookup"><span data-stu-id="2c251-287">All connected clients in a specified group except the specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample34.cs)]
- <span data-ttu-id="2c251-288">指定组中的所有已连接客户端（调用客户端除外）。</span><span class="sxs-lookup"><span data-stu-id="2c251-288">All connected clients in a specified group except the calling client.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample35.css)]
- <span data-ttu-id="2c251-289">用户 Id 标识的特定用户。</span><span class="sxs-lookup"><span data-stu-id="2c251-289">A specific user, identified by userId.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample36.cs)]

    <span data-ttu-id="2c251-290">默认情况下，这是`IPrincipal.Identity.Name`，但可以通过[向全局主机注册 IUserIdProvider 的实现](mapping-users-to-connections.md#IUserIdProvider)来更改。</span><span class="sxs-lookup"><span data-stu-id="2c251-290">By default, this is `IPrincipal.Identity.Name`, but this can be changed by [registering an implementation of IUserIdProvider with the global host](mapping-users-to-connections.md#IUserIdProvider).</span></span>
- <span data-ttu-id="2c251-291">连接指示列表中的所有客户端和组。</span><span class="sxs-lookup"><span data-stu-id="2c251-291">All clients and groups in a list of connection IDs.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample37.css)]
- <span data-ttu-id="2c251-292">组的列表。</span><span class="sxs-lookup"><span data-stu-id="2c251-292">A list of groups.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample38.css)]
- <span data-ttu-id="2c251-293">按名称命名的用户。</span><span class="sxs-lookup"><span data-stu-id="2c251-293">A user by name.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample39.cs)]
- <span data-ttu-id="2c251-294">用户名列表（在 SignalR 2.1 中介绍）。</span><span class="sxs-lookup"><span data-stu-id="2c251-294">A list of user names (introduced in SignalR 2.1).</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample40.cs)]

<a id="dynamicmethodnames"></a>

### <a name="no-compile-time-validation-for-method-names"></a><span data-ttu-id="2c251-295">方法名称没有编译时间验证</span><span class="sxs-lookup"><span data-stu-id="2c251-295">No compile-time validation for method names</span></span>

<span data-ttu-id="2c251-296">您指定的方法名称被解释为动态对象，这意味着没有 IntelliSense 或编译时间验证。</span><span class="sxs-lookup"><span data-stu-id="2c251-296">The method name that you specify is interpreted as a dynamic object, which means there is no IntelliSense or compile-time validation for it.</span></span> <span data-ttu-id="2c251-297">表达式在运行时计算。</span><span class="sxs-lookup"><span data-stu-id="2c251-297">The expression is evaluated at run time.</span></span> <span data-ttu-id="2c251-298">当方法调用执行时，SignalR 会将方法名称和参数值发送到客户端，如果客户端具有与该名称匹配的方法，则调用该方法并将参数值传递给它。</span><span class="sxs-lookup"><span data-stu-id="2c251-298">When the method call executes, SignalR sends the method name and the parameter values to the client, and if the client has a method that matches the name, that method is called and the parameter values are passed to it.</span></span> <span data-ttu-id="2c251-299">如果在客户端上找不到匹配方法，则不引发错误。</span><span class="sxs-lookup"><span data-stu-id="2c251-299">If no matching method is found on the client, no error is raised.</span></span> <span data-ttu-id="2c251-300">有关 SignalR 调用客户端方法时在后台传输到客户端的数据格式的信息，请参阅[SignalR 简介](../getting-started/introduction-to-signalr.md)。</span><span class="sxs-lookup"><span data-stu-id="2c251-300">For information about the format of the data that SignalR transmits to the client behind the scenes when you call a client method, see [Introduction to SignalR](../getting-started/introduction-to-signalr.md).</span></span>

<a id="caseinsensitive"></a>

### <a name="case-insensitive-method-name-matching"></a><span data-ttu-id="2c251-301">区分大小写的方法名称匹配</span><span class="sxs-lookup"><span data-stu-id="2c251-301">Case-insensitive method name matching</span></span>

<span data-ttu-id="2c251-302">方法名称匹配不区分大小写。</span><span class="sxs-lookup"><span data-stu-id="2c251-302">Method name matching is case-insensitive.</span></span> <span data-ttu-id="2c251-303">例如，`Clients.All.addContosoChatMessageToPage`在服务器上将执行`AddContosoChatMessageToPage`、`addcontosochatmessagetopage`或`addContosoChatMessageToPage`在客户端上。</span><span class="sxs-lookup"><span data-stu-id="2c251-303">For example, `Clients.All.addContosoChatMessageToPage` on the server will execute `AddContosoChatMessageToPage`, `addcontosochatmessagetopage`, or `addContosoChatMessageToPage` on the client.</span></span>

<a id="asyncclient"></a>

### <a name="asynchronous-execution"></a><span data-ttu-id="2c251-304">异步执行</span><span class="sxs-lookup"><span data-stu-id="2c251-304">Asynchronous execution</span></span>

<span data-ttu-id="2c251-305">调用的方法以异步方式执行。</span><span class="sxs-lookup"><span data-stu-id="2c251-305">The method that you call executes asynchronously.</span></span> <span data-ttu-id="2c251-306">对客户端进行方法调用后出现的任何代码将立即执行，而无需等待 SignalR 完成向客户端传输数据，除非您指定后续代码行应等待方法完成。</span><span class="sxs-lookup"><span data-stu-id="2c251-306">Any code that comes after a method call to a client will execute immediately without waiting for SignalR to finish transmitting data to clients unless you specify that the subsequent lines of code should wait for method completion.</span></span> <span data-ttu-id="2c251-307">下面的代码示例演示如何按顺序执行两个客户端方法。</span><span class="sxs-lookup"><span data-stu-id="2c251-307">The following code example shows how to execute two client methods sequentially.</span></span>

<span data-ttu-id="2c251-308">**使用 Await （.NET 4.5）**</span><span class="sxs-lookup"><span data-stu-id="2c251-308">**Using Await (.NET 4.5)**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample41.cs?highlight=1,3)]

<span data-ttu-id="2c251-309">如果使用等待`await`客户端方法在下一行代码执行之前完成，这并不意味着客户端将在执行下一行代码之前实际收到消息。</span><span class="sxs-lookup"><span data-stu-id="2c251-309">If you use `await` to wait until a client method finishes before the next line of code executes, that does not mean that clients will actually receive the message before the next line of code executes.</span></span> <span data-ttu-id="2c251-310">客户端方法调用的"完成"仅意味着 SignalR 已执行发送消息所需的一切。</span><span class="sxs-lookup"><span data-stu-id="2c251-310">"Completion" of a client method call only means that SignalR has done everything necessary to send the message.</span></span> <span data-ttu-id="2c251-311">如果您需要验证客户端是否收到该消息，您必须自己对该机制进行编程。</span><span class="sxs-lookup"><span data-stu-id="2c251-311">If you need verification that clients received the message, you have to program that mechanism yourself.</span></span> <span data-ttu-id="2c251-312">例如，您可以在 Hub 上`MessageReceived`编写方法代码，在客户端上`addContosoChatMessageToPage`编写方法后，您可以在执行需要在客户端`MessageReceived`上执行的任何工作后调用。</span><span class="sxs-lookup"><span data-stu-id="2c251-312">For example, you could code a `MessageReceived` method on the Hub, and in the `addContosoChatMessageToPage` method on the client you could call `MessageReceived` after you do whatever work you need to do on the client.</span></span> <span data-ttu-id="2c251-313">在`MessageReceived`Hub 中，您可以执行依赖于原始方法调用的实际客户端接收和处理的任何工作。</span><span class="sxs-lookup"><span data-stu-id="2c251-313">In `MessageReceived` in the Hub you can do whatever work depends on actual client reception and processing of the original method call.</span></span>

### <a name="how-to-use-a-string-variable-as-the-method-name"></a><span data-ttu-id="2c251-314">如何使用字符串变量作为方法名称</span><span class="sxs-lookup"><span data-stu-id="2c251-314">How to use a string variable as the method name</span></span>

<span data-ttu-id="2c251-315">如果要使用字符串变量作为方法名称调用客户端方法，则强制`Clients.All`（或`Clients.Others`、等`Clients.Caller`）调用`IClientProxy` [Invoke（方法名称、args...）](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.iclientproxy.invoke(v=vs.111).aspx)。</span><span class="sxs-lookup"><span data-stu-id="2c251-315">If you want to invoke a client method by using a string variable as the method name, cast `Clients.All` (or `Clients.Others`, `Clients.Caller`, etc.) to `IClientProxy` and then call [Invoke(methodName, args...)](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.iclientproxy.invoke(v=vs.111).aspx).</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample42.cs)]

<a id="groupsfromhub"></a>

## <a name="how-to-manage-group-membership-from-the-hub-class"></a><span data-ttu-id="2c251-316">如何从中心类管理组成员身份</span><span class="sxs-lookup"><span data-stu-id="2c251-316">How to manage group membership from the Hub class</span></span>

<span data-ttu-id="2c251-317">SignalR 中的组提供了一种将消息广播到连接客户端的指定子集的方法。</span><span class="sxs-lookup"><span data-stu-id="2c251-317">Groups in SignalR provide a method for broadcasting messages to specified subsets of connected clients.</span></span> <span data-ttu-id="2c251-318">组可以具有任意数量的客户端，并且客户端可以是任意数量的组的成员。</span><span class="sxs-lookup"><span data-stu-id="2c251-318">A group can have any number of clients, and a client can be a member of any number of groups.</span></span>

<span data-ttu-id="2c251-319">要管理组成员身份，请使用中心类`Groups`的属性提供的["添加](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx)[和删除"](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx)方法。</span><span class="sxs-lookup"><span data-stu-id="2c251-319">To manage group membership, use the [Add](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) and [Remove](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) methods provided by the `Groups` property of the Hub class.</span></span> <span data-ttu-id="2c251-320">下面的示例显示了由客户端`Groups.Add`代码`Groups.Remove`调用的 Hub 方法中使用的 和 方法，然后是调用它们的 JavaScript 客户端代码。</span><span class="sxs-lookup"><span data-stu-id="2c251-320">The following example shows the `Groups.Add` and `Groups.Remove` methods used in Hub methods that are called by client code, followed by JavaScript client code that calls them.</span></span>

<span data-ttu-id="2c251-321">**Server**</span><span class="sxs-lookup"><span data-stu-id="2c251-321">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample43.cs?highlight=5,10)]

<span data-ttu-id="2c251-322">**使用生成的代理的 JavaScript 客户端**</span><span class="sxs-lookup"><span data-stu-id="2c251-322">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample44.js)]

[!code-javascript[Main](hubs-api-guide-server/samples/sample45.js)]

<span data-ttu-id="2c251-323">您不必显式创建组。</span><span class="sxs-lookup"><span data-stu-id="2c251-323">You don't have to explicitly create groups.</span></span> <span data-ttu-id="2c251-324">实际上，在调用`Groups.Add`中首次指定其名称时会自动创建组，并且当您从其成员身份中删除最后一个连接时，该组将被删除。</span><span class="sxs-lookup"><span data-stu-id="2c251-324">In effect a group is automatically created the first time you specify its name in a call to `Groups.Add`, and it is deleted when you remove the last connection from membership in it.</span></span>

<span data-ttu-id="2c251-325">没有用于获取组成员身份列表或组列表的 API。</span><span class="sxs-lookup"><span data-stu-id="2c251-325">There is no API for getting a group membership list or a list of groups.</span></span> <span data-ttu-id="2c251-326">SignalR 根据[pub/子模型](http://en.wikipedia.org/wiki/Publish/subscribe)向客户端和组发送消息，并且服务器不维护组或组成员身份的列表。</span><span class="sxs-lookup"><span data-stu-id="2c251-326">SignalR sends messages to clients and groups based on a [pub/sub model](http://en.wikipedia.org/wiki/Publish/subscribe), and the server does not maintain lists of groups or group memberships.</span></span> <span data-ttu-id="2c251-327">这有助于最大化可伸缩性，因为每当将节点添加到 Web 场时，SignalR 维护的任何状态都必须传播到新节点。</span><span class="sxs-lookup"><span data-stu-id="2c251-327">This helps maximize scalability, because whenever you add a node to a web farm, any state that SignalR maintains has to be propagated to the new node.</span></span>

<a id="asyncgroupmethods"></a>

### <a name="asynchronous-execution-of-add-and-remove-methods"></a><span data-ttu-id="2c251-328">添加和删除方法的异步执行</span><span class="sxs-lookup"><span data-stu-id="2c251-328">Asynchronous execution of Add and Remove methods</span></span>

<span data-ttu-id="2c251-329">`Groups.Add`和`Groups.Remove`方法以异步方式执行。</span><span class="sxs-lookup"><span data-stu-id="2c251-329">The `Groups.Add` and `Groups.Remove` methods execute asynchronously.</span></span> <span data-ttu-id="2c251-330">如果要将客户端添加到组，然后使用 组立即向客户端发送消息，则必须确保`Groups.Add`该方法首先完成。</span><span class="sxs-lookup"><span data-stu-id="2c251-330">If you want to add a client to a group and immediately send a message to the client by using the group, you have to make sure that the `Groups.Add` method finishes first.</span></span> <span data-ttu-id="2c251-331">下面的代码示例演示如何执行此操作。</span><span class="sxs-lookup"><span data-stu-id="2c251-331">The following code example shows how to do that.</span></span>

<span data-ttu-id="2c251-332">**将客户端添加到组，然后向该客户端发送消息**</span><span class="sxs-lookup"><span data-stu-id="2c251-332">**Adding a client to a group and then messaging that client**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample46.cs?highlight=1,3)]

<a id="grouppersistence"></a>

### <a name="group-membership-persistence"></a><span data-ttu-id="2c251-333">组成员身份持久性</span><span class="sxs-lookup"><span data-stu-id="2c251-333">Group membership persistence</span></span>

<span data-ttu-id="2c251-334">SignalR 跟踪连接，而不是用户，因此，如果您希望用户每次建立连接时都位于同一组中，则每次用户建立新连接时都必须调用`Groups.Add`。</span><span class="sxs-lookup"><span data-stu-id="2c251-334">SignalR tracks connections, not users, so if you want a user to be in the same group every time the user establishes a connection, you have to call `Groups.Add` every time the user establishes a new connection.</span></span>

<span data-ttu-id="2c251-335">在暂时失去连接后，有时 SignalR 可以自动恢复连接。</span><span class="sxs-lookup"><span data-stu-id="2c251-335">After a temporary loss of connectivity, sometimes SignalR can restore the connection automatically.</span></span> <span data-ttu-id="2c251-336">在这种情况下，SignalR 正在还原相同的连接，而不是建立新连接，因此客户端的组成员身份将自动还原。</span><span class="sxs-lookup"><span data-stu-id="2c251-336">In that case, SignalR is restoring the same connection, not establishing a new connection, and so the client's group membership is automatically restored.</span></span> <span data-ttu-id="2c251-337">即使临时中断是服务器重新启动或失败的结果，也是可能的，因为每个客户端（包括组成员身份）的连接状态都向客户端四舍五入。</span><span class="sxs-lookup"><span data-stu-id="2c251-337">This is possible even when the temporary break is the result of a server reboot or failure, because connection state for each client, including group memberships, is round-tripped to the client.</span></span> <span data-ttu-id="2c251-338">如果服务器在连接超时之前出现故障并由新服务器替换，则客户端可以自动重新连接到新服务器，并重新注册其成员的组。</span><span class="sxs-lookup"><span data-stu-id="2c251-338">If a server goes down and is replaced by a new server before the connection times out, a client can reconnect automatically to the new server and re-enroll in groups it is a member of.</span></span>

<span data-ttu-id="2c251-339">当连接在失去连接后或连接超时或客户端断开连接（例如，当浏览器导航到新页面时）无法自动恢复时，组成员身份将丢失。</span><span class="sxs-lookup"><span data-stu-id="2c251-339">When a connection can't be restored automatically after a loss of connectivity, or when the connection times out, or when the client disconnects (for example, when a browser navigates to a new page), group memberships are lost.</span></span> <span data-ttu-id="2c251-340">用户下次连接时将是一个新连接。</span><span class="sxs-lookup"><span data-stu-id="2c251-340">The next time the user connects will be a new connection.</span></span> <span data-ttu-id="2c251-341">要在同一用户建立新连接时维护组成员身份，应用程序必须跟踪用户和组之间的关联，并在每次用户建立新连接时还原组成员身份。</span><span class="sxs-lookup"><span data-stu-id="2c251-341">To maintain group memberships when the same user establishes a new connection, your application has to track the associations between users and groups, and restore group memberships each time a user establishes a new connection.</span></span>

<span data-ttu-id="2c251-342">有关连接和重新连接的详细信息，请参阅本主题后面的["集线器"类中如何处理连接生存期事件](#connectionlifetime)。</span><span class="sxs-lookup"><span data-stu-id="2c251-342">For more information about connections and reconnections, see [How to handle connection lifetime events in the Hub class](#connectionlifetime) later in this topic.</span></span>

<a id="singleusergroups"></a>

### <a name="single-user-groups"></a><span data-ttu-id="2c251-343">单用户组</span><span class="sxs-lookup"><span data-stu-id="2c251-343">Single-user groups</span></span>

<span data-ttu-id="2c251-344">使用 SignalR 的应用程序通常必须跟踪用户和连接之间的关联，以便知道哪个用户发送消息以及应该接收哪些用户。</span><span class="sxs-lookup"><span data-stu-id="2c251-344">Applications that use SignalR typically have to keep track of the associations between users and connections in order to know which user has sent a message and which user(s) should be receiving a message.</span></span> <span data-ttu-id="2c251-345">组用于执行此操作的两个常用模式之一。</span><span class="sxs-lookup"><span data-stu-id="2c251-345">Groups are used in one of the two commonly used patterns for doing that.</span></span>

- <span data-ttu-id="2c251-346">单用户组。</span><span class="sxs-lookup"><span data-stu-id="2c251-346">Single-user groups.</span></span>

    <span data-ttu-id="2c251-347">您可以将用户名指定为组名称，并在每次用户连接或重新连接时将当前连接 ID 添加到组。</span><span class="sxs-lookup"><span data-stu-id="2c251-347">You can specify the user name as the group name, and add the current connection ID to the group every time the user connects or reconnects.</span></span> <span data-ttu-id="2c251-348">向发送给组的用户发送消息。</span><span class="sxs-lookup"><span data-stu-id="2c251-348">To send messages to the user you send to the group.</span></span> <span data-ttu-id="2c251-349">此方法的缺点是，组不为您提供一种方法来了解用户是联机还是脱机。</span><span class="sxs-lookup"><span data-stu-id="2c251-349">A disadvantage of this method is that the group doesn't provide you with a way to find out if the user is online or offline.</span></span>
- <span data-ttu-id="2c251-350">跟踪用户名和连接指示之间的关联。</span><span class="sxs-lookup"><span data-stu-id="2c251-350">Track associations between user names and connection IDs.</span></span>

    <span data-ttu-id="2c251-351">您可以将每个用户名与字典或数据库中的一个或多个连接 I 之间的关联存储，并在每次用户连接或断开连接时更新存储的数据。</span><span class="sxs-lookup"><span data-stu-id="2c251-351">You can store an association between each user name and one or more connection IDs in a dictionary or database, and update the stored data each time the user connects or disconnects.</span></span> <span data-ttu-id="2c251-352">要向用户发送消息，请指定连接指示。</span><span class="sxs-lookup"><span data-stu-id="2c251-352">To send messages to the user you specify the connection IDs.</span></span> <span data-ttu-id="2c251-353">此方法的缺点是它需要更多的内存。</span><span class="sxs-lookup"><span data-stu-id="2c251-353">A disadvantage of this method is that it takes more memory.</span></span>

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events-in-the-hub-class"></a><span data-ttu-id="2c251-354">如何处理集线器类中的连接生存期事件</span><span class="sxs-lookup"><span data-stu-id="2c251-354">How to handle connection lifetime events in the Hub class</span></span>

<span data-ttu-id="2c251-355">处理连接生存期事件的典型原因是跟踪用户是否已连接，并跟踪用户名和连接令牌之间的关联。</span><span class="sxs-lookup"><span data-stu-id="2c251-355">Typical reasons for handling connection lifetime events are to keep track of whether a user is connected or not, and to keep track of the association between user names and connection IDs.</span></span> <span data-ttu-id="2c251-356">要在客户端连接或断开连接时运行自己的代码，请重写`OnConnected` `OnDisconnected`Hub`OnReconnected`类 的 和 和 虚拟方法，如以下示例所示。</span><span class="sxs-lookup"><span data-stu-id="2c251-356">To run your own code when clients connect or disconnect, override the `OnConnected`, `OnDisconnected`, and `OnReconnected` virtual methods of the Hub class, as shown in the following example.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample47.cs?highlight=3,14,22)]

<a id="onreconnected"></a>

### <a name="when-onconnected-ondisconnected-and-onreconnected-are-called"></a><span data-ttu-id="2c251-357">当"连接"时，打开断开状态，并调用"重新连接"</span><span class="sxs-lookup"><span data-stu-id="2c251-357">When OnConnected, OnDisconnected, and OnReconnected are called</span></span>

<span data-ttu-id="2c251-358">每次浏览器导航到新页面时，都必须建立一个新连接，这意味着 SignalR 将执行方法后跟`OnDisconnected``OnConnected`的方法。</span><span class="sxs-lookup"><span data-stu-id="2c251-358">Each time a browser navigates to a new page, a new connection has to be established, which means SignalR will execute the `OnDisconnected` method followed by the `OnConnected` method.</span></span> <span data-ttu-id="2c251-359">建立新连接时，SignalR 始终创建新的连接 ID。</span><span class="sxs-lookup"><span data-stu-id="2c251-359">SignalR always creates a new connection ID when a new connection is established.</span></span>

<span data-ttu-id="2c251-360">当`OnReconnected`SignalR 可以自动恢复的连接出现暂时中断时调用该方法，例如电缆在连接超时之前暂时断开并重新连接时。当`OnDisconnected`客户端断开连接且 SignalR 无法自动重新连接时，如浏览器导航到新页面时，将调用该方法。</span><span class="sxs-lookup"><span data-stu-id="2c251-360">The `OnReconnected` method is called when there has been a temporary break in connectivity that SignalR can automatically recover from, such as when a cable is temporarily disconnected and reconnected before the connection times out. The `OnDisconnected` method is called when the client is disconnected and SignalR can't automatically reconnect, such as when a browser navigates to a new page.</span></span> <span data-ttu-id="2c251-361">因此，给定客户端的可能事件序列为`OnConnected`，和`OnReconnected``OnDisconnected`或`OnConnected` `OnDisconnected`。</span><span class="sxs-lookup"><span data-stu-id="2c251-361">Therefore, a possible sequence of events for a given client is `OnConnected`, `OnReconnected`, `OnDisconnected`; or `OnConnected`, `OnDisconnected`.</span></span> <span data-ttu-id="2c251-362">对于给定的连接，`OnConnected``OnDisconnected`您将看不到序列，。 `OnReconnected`</span><span class="sxs-lookup"><span data-stu-id="2c251-362">You won't see the sequence `OnConnected`, `OnDisconnected`, `OnReconnected` for a given connection.</span></span>

<span data-ttu-id="2c251-363">在某些情况下`OnDisconnected`，例如服务器出现故障或 App Domain 被回收时，不会调用该方法。</span><span class="sxs-lookup"><span data-stu-id="2c251-363">The `OnDisconnected` method doesn't get called in some scenarios, such as when a server goes down or the App Domain gets recycled.</span></span> <span data-ttu-id="2c251-364">当另一台服务器上线或 App Domain 完成其回收时，某些客户端可能能够重新连接并触发`OnReconnected`事件。</span><span class="sxs-lookup"><span data-stu-id="2c251-364">When another server comes on line or the App Domain completes its recycle, some clients may be able to reconnect and fire the `OnReconnected` event.</span></span>

<span data-ttu-id="2c251-365">有关详细信息，请参阅在[SignalR 中了解和处理连接生存期事件](handling-connection-lifetime-events.md)。</span><span class="sxs-lookup"><span data-stu-id="2c251-365">For more information, see [Understanding and Handling Connection Lifetime Events in SignalR](handling-connection-lifetime-events.md).</span></span>

<a id="nocallerstate"></a>

### <a name="caller-state-not-populated"></a><span data-ttu-id="2c251-366">未填充的呼叫者状态</span><span class="sxs-lookup"><span data-stu-id="2c251-366">Caller state not populated</span></span>

<span data-ttu-id="2c251-367">连接生存期事件处理程序方法从服务器调用，这意味着您在`state`客户端上的对象中放置的任何状态将不会填充在服务器上`Caller`的属性中。</span><span class="sxs-lookup"><span data-stu-id="2c251-367">The connection lifetime event handler methods are called from the server, which means that any state that you put in the `state` object on the client will not be populated in the `Caller` property on the server.</span></span> <span data-ttu-id="2c251-368">有关`state`对象和`Caller`属性的信息，请参阅本主题后面的["如何在客户端和中心类之间传递状态](#passstate)"。</span><span class="sxs-lookup"><span data-stu-id="2c251-368">For information about the `state` object and the `Caller` property, see [How to pass state between clients and the Hub class](#passstate) later in this topic.</span></span>

<a id="contextproperty"></a>

## <a name="how-to-get-information-about-the-client-from-the-context-property"></a><span data-ttu-id="2c251-369">如何从上下文属性获取有关客户端的信息</span><span class="sxs-lookup"><span data-stu-id="2c251-369">How to get information about the client from the Context property</span></span>

<span data-ttu-id="2c251-370">要获取有关客户端的信息，`Context`请使用 Hub 类的属性。</span><span class="sxs-lookup"><span data-stu-id="2c251-370">To get information about the client, use the `Context` property of the Hub class.</span></span> <span data-ttu-id="2c251-371">该`Context`属性返回一个[HubCallerContext](https://msdn.microsoft.com/library/jj890883(v=vs.111).aspx)对象，该对象提供对以下信息的访问：</span><span class="sxs-lookup"><span data-stu-id="2c251-371">The `Context` property returns a [HubCallerContext](https://msdn.microsoft.com/library/jj890883(v=vs.111).aspx) object which provides access to the following information:</span></span>

- <span data-ttu-id="2c251-372">调用客户端的连接 ID。</span><span class="sxs-lookup"><span data-stu-id="2c251-372">The connection ID of the calling client.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample48.cs?highlight=1)]

    <span data-ttu-id="2c251-373">连接 ID 是由 SignalR 分配的 GUID（您无法在自己的代码中指定值）。</span><span class="sxs-lookup"><span data-stu-id="2c251-373">The connection ID is a GUID that is assigned by SignalR (you can't specify the value in your own code).</span></span> <span data-ttu-id="2c251-374">每个连接都有一个连接 ID，如果应用程序中有多个集线器，则所有集线器都使用相同的连接 ID。</span><span class="sxs-lookup"><span data-stu-id="2c251-374">There is one connection ID for each connection, and the same connection ID is used by all Hubs if you have multiple Hubs in your application.</span></span>
- <span data-ttu-id="2c251-375">HTTP 标头数据。</span><span class="sxs-lookup"><span data-stu-id="2c251-375">HTTP header data.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample49.cs?highlight=1)]

    <span data-ttu-id="2c251-376">还可以从`Context.Headers`获取 HTTP 标头。</span><span class="sxs-lookup"><span data-stu-id="2c251-376">You can also get HTTP headers from `Context.Headers`.</span></span> <span data-ttu-id="2c251-377">对同一事物`Context.Headers`的多次引用的原因是首先创建，`Context.Request`该属性在以后添加，并`Context.Headers`保留为向后兼容性。</span><span class="sxs-lookup"><span data-stu-id="2c251-377">The reason for multiple references to the same thing is that `Context.Headers` was created first, the `Context.Request` property was added later, and `Context.Headers` was retained for backward compatibility.</span></span>
- <span data-ttu-id="2c251-378">查询字符串数据。</span><span class="sxs-lookup"><span data-stu-id="2c251-378">Query string data.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample50.cs?highlight=1)]

    <span data-ttu-id="2c251-379">还可以从`Context.QueryString`获取查询字符串数据。</span><span class="sxs-lookup"><span data-stu-id="2c251-379">You can also get query string data from `Context.QueryString`.</span></span>

    <span data-ttu-id="2c251-380">在此属性中获取的查询字符串是与建立 SignalR 连接的 HTTP 请求一起使用的查询字符串。</span><span class="sxs-lookup"><span data-stu-id="2c251-380">The query string that you get in this property is the one that was used with the HTTP request that established the SignalR connection.</span></span> <span data-ttu-id="2c251-381">您可以通过配置连接在客户端中添加查询字符串参数，这是将有关客户端的数据从客户端传递到服务器的便捷方法。</span><span class="sxs-lookup"><span data-stu-id="2c251-381">You can add query string parameters in the client by configuring the connection, which is a convenient way to pass data about the client from the client to the server.</span></span> <span data-ttu-id="2c251-382">下面的示例显示了在使用生成的代理时在 JavaScript 客户端中添加查询字符串的一种方法。</span><span class="sxs-lookup"><span data-stu-id="2c251-382">The following example shows one way to add a query string in a JavaScript client when you use the generated proxy.</span></span>

    [!code-javascript[Main](hubs-api-guide-server/samples/sample51.js?highlight=1)]

    <span data-ttu-id="2c251-383">有关设置查询字符串参数的详细信息，请参阅[JavaScript](hubs-api-guide-javascript-client.md)和[.NET](hubs-api-guide-net-client.md)客户端的 API 指南。</span><span class="sxs-lookup"><span data-stu-id="2c251-383">For more information about setting query string parameters, see the API guides for the [JavaScript](hubs-api-guide-javascript-client.md) and [.NET](hubs-api-guide-net-client.md) clients.</span></span>

    <span data-ttu-id="2c251-384">您可以在查询字符串数据中找到用于连接的传输方法，以及 SignalR 内部使用的一些其他值：</span><span class="sxs-lookup"><span data-stu-id="2c251-384">You can find the transport method used for the connection in the query string data, along with some other values used internally by SignalR:</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample52.cs)]

    <span data-ttu-id="2c251-385">的值`transportMethod`将是"webSocket"、"服务器发送事件"、"永久帧"或"长轮询"。</span><span class="sxs-lookup"><span data-stu-id="2c251-385">The value of `transportMethod` will be "webSockets", "serverSentEvents", "foreverFrame" or "longPolling".</span></span> <span data-ttu-id="2c251-386">请注意，如果在`OnConnected`事件处理程序方法中检查此值，在某些情况下，最初可能会获取传输值，该值不是连接的最终协商传输方法。</span><span class="sxs-lookup"><span data-stu-id="2c251-386">Note that if you check this value in the `OnConnected` event handler method, in some scenarios you might initially get a transport value that is not the final negotiated transport method for the connection.</span></span> <span data-ttu-id="2c251-387">在这种情况下，该方法将引发异常，并在建立最终传输方法时稍后再次调用。</span><span class="sxs-lookup"><span data-stu-id="2c251-387">In that case the method will throw an exception and will be called again later when the final transport method is established.</span></span>
- <span data-ttu-id="2c251-388">Cookie。</span><span class="sxs-lookup"><span data-stu-id="2c251-388">Cookies.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample53.cs?highlight=1)]

    <span data-ttu-id="2c251-389">您也可以从`Context.RequestCookies`获取 Cookie。</span><span class="sxs-lookup"><span data-stu-id="2c251-389">You can also get cookies from `Context.RequestCookies`.</span></span>
- <span data-ttu-id="2c251-390">用户信息。</span><span class="sxs-lookup"><span data-stu-id="2c251-390">User information.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample54.cs?highlight=1)]
- <span data-ttu-id="2c251-391">请求的 HttpContext 对象 ：</span><span class="sxs-lookup"><span data-stu-id="2c251-391">The HttpContext object for the request :</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample55.cs?highlight=1)]

    <span data-ttu-id="2c251-392">使用此方法，而不是获取`HttpContext.Current`SignalR`HttpContext`连接的对象。</span><span class="sxs-lookup"><span data-stu-id="2c251-392">Use this method instead of getting `HttpContext.Current` to get the `HttpContext` object for the SignalR connection.</span></span>

<a id="passstate"></a>

## <a name="how-to-pass-state-between-clients-and-the-hub-class"></a><span data-ttu-id="2c251-393">如何在客户端和中心类之间传递状态</span><span class="sxs-lookup"><span data-stu-id="2c251-393">How to pass state between clients and the Hub class</span></span>

<span data-ttu-id="2c251-394">客户端代理提供一个`state`对象，您可以在其中存储要通过每个方法调用传输到服务器的数据。</span><span class="sxs-lookup"><span data-stu-id="2c251-394">The client proxy provides a `state` object in which you can store data that you want to be transmitted to the server with each method call.</span></span> <span data-ttu-id="2c251-395">在服务器上，您可以在客户端调用的`Clients.Caller`Hub 方法中的属性中访问此数据。</span><span class="sxs-lookup"><span data-stu-id="2c251-395">On the server you can access this data in the `Clients.Caller` property in Hub methods that are called by clients.</span></span> <span data-ttu-id="2c251-396">不会`Clients.Caller`为连接生存期事件处理程序填充`OnConnected`属性 ，`OnDisconnected`和`OnReconnected`。</span><span class="sxs-lookup"><span data-stu-id="2c251-396">The `Clients.Caller` property is not populated for the connection lifetime event handler methods `OnConnected`, `OnDisconnected`, and `OnReconnected`.</span></span>

<span data-ttu-id="2c251-397">在`state`对象中创建或更新数据，`Clients.Caller`属性在两个方向上工作。</span><span class="sxs-lookup"><span data-stu-id="2c251-397">Creating or updating data in the `state` object and the `Clients.Caller` property works in both directions.</span></span> <span data-ttu-id="2c251-398">您可以更新服务器中的值，并将它们传回客户端。</span><span class="sxs-lookup"><span data-stu-id="2c251-398">You can update values in the server and they are passed back to the client.</span></span>

<span data-ttu-id="2c251-399">下面的示例显示 JavaScript 客户端代码，该代码存储状态，以便通过每个方法调用传输到服务器。</span><span class="sxs-lookup"><span data-stu-id="2c251-399">The following example shows JavaScript client code that stores state for transmission to the server with every method call.</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample56.js?highlight=1-2)]

<span data-ttu-id="2c251-400">下面的示例显示了 .NET 客户端中的等效代码。</span><span class="sxs-lookup"><span data-stu-id="2c251-400">The following example shows the equivalent code in a .NET client.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample57.cs?highlight=1-2)]

<span data-ttu-id="2c251-401">在 Hub 类中，您可以在`Clients.Caller`属性中访问此数据。</span><span class="sxs-lookup"><span data-stu-id="2c251-401">In your Hub class, you can access this data in the `Clients.Caller` property.</span></span> <span data-ttu-id="2c251-402">下面的示例显示检索上一个示例中引用的状态的代码。</span><span class="sxs-lookup"><span data-stu-id="2c251-402">The following example shows code that retrieves the state referred to in the previous example.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample58.cs?highlight=3-4)]

> [!NOTE]
> <span data-ttu-id="2c251-403">此持久状态机制不适用于大量数据，因为在`state`或`Clients.Caller`属性中放置的所有内容都随每个方法调用一起循环。</span><span class="sxs-lookup"><span data-stu-id="2c251-403">This mechanism for persisting state is not intended for large amounts of data, since everything you put in the `state` or `Clients.Caller` property is round-tripped with every method invocation.</span></span> <span data-ttu-id="2c251-404">它对于较小的项目（如用户名或计数器）很有用。</span><span class="sxs-lookup"><span data-stu-id="2c251-404">It's useful for smaller items such as user names or counters.</span></span>

<span data-ttu-id="2c251-405">在VB.NET或强类型中心中，无法通过`Clients.Caller`而是使用`Clients.CallerState`（在信号R 2.1 中介绍）：</span><span class="sxs-lookup"><span data-stu-id="2c251-405">In VB.NET or in a strongly-typed hub, the caller state object can't be accessed through `Clients.Caller`; instead, use `Clients.CallerState` (introduced in SignalR 2.1):</span></span>

<span data-ttu-id="2c251-406">**在 C 中使用调用方状态#**</span><span class="sxs-lookup"><span data-stu-id="2c251-406">**Using CallerState in C#**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample59.cs?highlight=3-4)]

<span data-ttu-id="2c251-407">**在可视化基础中使用调用方状态**</span><span class="sxs-lookup"><span data-stu-id="2c251-407">**Using CallerState in Visual Basic**</span></span>

[!code-vb[Main](hubs-api-guide-server/samples/sample60.vb)]

<a id="handleErrors"></a>

## <a name="how-to-handle-errors-in-the-hub-class"></a><span data-ttu-id="2c251-408">如何处理中心类中的错误</span><span class="sxs-lookup"><span data-stu-id="2c251-408">How to handle errors in the Hub class</span></span>

<span data-ttu-id="2c251-409">要处理在 Hub 类方法中发生的错误，首先请确保使用`await`"观察"异步操作（如调用客户端方法）中的任何异常。</span><span class="sxs-lookup"><span data-stu-id="2c251-409">To handle errors that occur in your Hub class methods, first ensure you "observe" any exceptions from async operations (such as invoking client methods) by using `await`.</span></span> <span data-ttu-id="2c251-410">然后使用以下一种或多种方法：</span><span class="sxs-lookup"><span data-stu-id="2c251-410">Then use one or more of the following methods:</span></span>

- <span data-ttu-id="2c251-411">将方法代码包装在 try-catch 块中并记录异常对象。</span><span class="sxs-lookup"><span data-stu-id="2c251-411">Wrap your method code in try-catch blocks and log the exception object.</span></span> <span data-ttu-id="2c251-412">出于调试目的，您可以将异常发送给客户端，但出于安全原因，不建议向生产中的客户端发送详细信息。</span><span class="sxs-lookup"><span data-stu-id="2c251-412">For debugging purposes you can send the exception to the client, but for security reasons sending detailed information to clients in production is not recommended.</span></span>
- <span data-ttu-id="2c251-413">创建处理[On 传入错误](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubpipelinemodule.onincomingerror(v=vs.111).aspx)方法的集线器管道模块。</span><span class="sxs-lookup"><span data-stu-id="2c251-413">Create a Hubs pipeline module that handles the [OnIncomingError](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubpipelinemodule.onincomingerror(v=vs.111).aspx) method.</span></span> <span data-ttu-id="2c251-414">下面的示例显示了一个管道模块，该模块记录错误，然后是Startup.cs中的代码，该代码将模块注入到集线器管道中。</span><span class="sxs-lookup"><span data-stu-id="2c251-414">The following example shows a pipeline module that logs errors, followed by code in Startup.cs that injects the module into the Hubs pipeline.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample61.cs)]

    [!code-csharp[Main](hubs-api-guide-server/samples/sample62.cs?highlight=4)]
- <span data-ttu-id="2c251-415">使用类`HubException`（在 SignalR 2 中介绍）。</span><span class="sxs-lookup"><span data-stu-id="2c251-415">Use the `HubException` class (introduced in SignalR 2).</span></span> <span data-ttu-id="2c251-416">可以从任何集线器调用引发此错误。</span><span class="sxs-lookup"><span data-stu-id="2c251-416">This error can be thrown from any hub invocation.</span></span> <span data-ttu-id="2c251-417">构造`HubError`函数获取字符串消息和用于存储额外错误数据的对象。</span><span class="sxs-lookup"><span data-stu-id="2c251-417">The `HubError` constructor takes a string message, and an object for storing extra error data.</span></span> <span data-ttu-id="2c251-418">SignalR 将自动序列化异常并将其发送到客户端，客户端将用于拒绝或失败集线器方法调用。</span><span class="sxs-lookup"><span data-stu-id="2c251-418">SignalR will auto-serialize the exception and send it to the client, where it will be used to reject or fail the hub method invocation.</span></span>

    <span data-ttu-id="2c251-419">以下代码示例演示如何在中心调用期间引发`HubException`，以及如何处理 JavaScript 和 .NET 客户端上的异常。</span><span class="sxs-lookup"><span data-stu-id="2c251-419">The following code samples demonstrate how to throw a `HubException` during a Hub invocation, and how to handle the exception on JavaScript and .NET clients.</span></span>

    <span data-ttu-id="2c251-420">**演示 HubException 类的服务器代码**</span><span class="sxs-lookup"><span data-stu-id="2c251-420">**Server code demonstrating the HubException class**</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample63.cs)]

    <span data-ttu-id="2c251-421">**JavaScript 客户端代码演示对在中心中引发 HubException 的响应**</span><span class="sxs-lookup"><span data-stu-id="2c251-421">**JavaScript client code demonstrating response to throwing a HubException in a hub**</span></span>

    [!code-html[Main](hubs-api-guide-server/samples/sample64.html)]

    <span data-ttu-id="2c251-422">**.NET 客户端代码，用于响应在中心中引发 HubException**</span><span class="sxs-lookup"><span data-stu-id="2c251-422">**.NET client code demonstrating response to throwing a HubException in a hub**</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample65.cs)]

<span data-ttu-id="2c251-423">有关集线器管道模块的详细信息，请参阅本主题后面的[如何自定义中心管道](#hubpipeline)。</span><span class="sxs-lookup"><span data-stu-id="2c251-423">For more information about Hub pipeline modules, see [How to customize the Hubs pipeline](#hubpipeline) later in this topic.</span></span>

<a id="tracing"></a>

## <a name="how-to-enable-tracing"></a><span data-ttu-id="2c251-424">如何启用跟踪</span><span class="sxs-lookup"><span data-stu-id="2c251-424">How to enable tracing</span></span>

<span data-ttu-id="2c251-425">要启用服务器端跟踪，请向 Web.config 文件添加 system.诊断元素，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="2c251-425">To enable server-side tracing, add a system.diagnostics element to your Web.config file, as shown in this example:</span></span>

[!code-html[Main](hubs-api-guide-server/samples/sample66.html?highlight=17-72)]

<span data-ttu-id="2c251-426">在 Visual Studio 中运行应用程序时，可以在 **"输出"** 窗口中查看日志。</span><span class="sxs-lookup"><span data-stu-id="2c251-426">When you run the application in Visual Studio, you can view the logs in the **Output** window.</span></span>

<a id="callfromoutsidehub"></a>

## <a name="how-to-call-client-methods-and-manage-groups-from-outside-the-hub-class"></a><span data-ttu-id="2c251-427">如何调用客户端方法并管理来自中心类外部的组</span><span class="sxs-lookup"><span data-stu-id="2c251-427">How to call client methods and manage groups from outside the Hub class</span></span>

<span data-ttu-id="2c251-428">要从与 Hub 类不同的类调用客户端方法，请获取对集线器的 SignalR 上下文对象的引用，并用它来调用客户端或管理组上的方法。</span><span class="sxs-lookup"><span data-stu-id="2c251-428">To call client methods from a different class than your Hub class, get a reference to the SignalR context object for the Hub and use that to call methods on the client or manage groups.</span></span>

<span data-ttu-id="2c251-429">以下示例`StockTicker`类获取上下文对象，将其存储在类的实例中，将类实例存储在静态属性中，并使用 singleton 类实例中的上下文调用连接到名为`updateStockPrice``StockTickerHub`的 Hub 的客户端上的方法。</span><span class="sxs-lookup"><span data-stu-id="2c251-429">The following sample `StockTicker` class gets the context object, stores it in an instance of the class, stores the class instance in a static property, and uses the context from the singleton class instance to call the `updateStockPrice` method on clients that are connected to a Hub named `StockTickerHub`.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample67.cs?highlight=8,24)]

<span data-ttu-id="2c251-430">如果需要在长寿命对象中多次使用上下文，获取引用一次并保存它，而不是每次都再次获取它。</span><span class="sxs-lookup"><span data-stu-id="2c251-430">If you need to use the context multiple-times in a long-lived object, get the reference once and save it rather than getting it again each time.</span></span> <span data-ttu-id="2c251-431">获取上下文一次可确保 SignalR 以与集线器方法进行客户端方法调用的顺序相同的顺序向客户端发送消息。</span><span class="sxs-lookup"><span data-stu-id="2c251-431">Getting the context once ensures that SignalR sends messages to clients in the same sequence in which your Hub methods make client method invocations.</span></span> <span data-ttu-id="2c251-432">有关演示如何对集线器使用 SignalR 上下文的教程，请参阅[使用 ASP.NET SignalR 的服务器广播](../getting-started/tutorial-server-broadcast-with-signalr.md)。</span><span class="sxs-lookup"><span data-stu-id="2c251-432">For a tutorial that shows how to use the SignalR context for a Hub, see [Server Broadcast with ASP.NET SignalR](../getting-started/tutorial-server-broadcast-with-signalr.md).</span></span>

<a id="callingclientsoutsidehub"></a>

### <a name="calling-client-methods"></a><span data-ttu-id="2c251-433">调用客户端方法</span><span class="sxs-lookup"><span data-stu-id="2c251-433">Calling client methods</span></span>

<span data-ttu-id="2c251-434">您可以指定哪些客户端将收到 RPC，但与从中心类调用时相比，选项更少。</span><span class="sxs-lookup"><span data-stu-id="2c251-434">You can specify which clients will receive the RPC, but you have fewer options than when you call from a Hub class.</span></span> <span data-ttu-id="2c251-435">原因是上下文与来自客户端的特定调用不相关联，因此任何需要了解当前连接 ID 的方法（如`Clients.Others`或`Clients.Caller`或`Clients.OthersInGroup`或 ） 都不可用。</span><span class="sxs-lookup"><span data-stu-id="2c251-435">The reason for this is that the context is not associated with a particular call from a client, so any methods that require knowledge of the current connection ID, such as `Clients.Others`, or `Clients.Caller`, or `Clients.OthersInGroup`, are not available.</span></span> <span data-ttu-id="2c251-436">提供了以下选项：</span><span class="sxs-lookup"><span data-stu-id="2c251-436">The following options are available:</span></span>

- <span data-ttu-id="2c251-437">所有已连接的客户端。</span><span class="sxs-lookup"><span data-stu-id="2c251-437">All connected clients.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample68.cs)]
- <span data-ttu-id="2c251-438">由连接 ID 标识的特定客户端。</span><span class="sxs-lookup"><span data-stu-id="2c251-438">A specific client identified by connection ID.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample69.css)]
- <span data-ttu-id="2c251-439">除指定客户端外的所有连接客户端，由连接 ID 标识。</span><span class="sxs-lookup"><span data-stu-id="2c251-439">All connected clients except the specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample70.cs)]
- <span data-ttu-id="2c251-440">指定组中的所有连接客户端。</span><span class="sxs-lookup"><span data-stu-id="2c251-440">All connected clients in a specified group.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample71.css)]
- <span data-ttu-id="2c251-441">指定组中的所有连接客户端（指定客户端除外），由连接 ID 标识。</span><span class="sxs-lookup"><span data-stu-id="2c251-441">All connected clients in a specified group except specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample72.cs)]

<span data-ttu-id="2c251-442">如果要从 Hub 类中的方法调用非 Hub 类，则可以将当前连接 ID`Clients.Client`传递，并将其用于 ，`Clients.AllExcept`或`Clients.Group`模拟`Clients.Caller`或`Clients.Others`。 `Clients.OthersInGroup`</span><span class="sxs-lookup"><span data-stu-id="2c251-442">If you are calling into your non-Hub class from methods in your Hub class, you can pass in the current connection ID and use that with `Clients.Client`, `Clients.AllExcept`, or `Clients.Group` to simulate `Clients.Caller`, `Clients.Others`, or `Clients.OthersInGroup`.</span></span> <span data-ttu-id="2c251-443">在下面的示例中`MoveShapeHub`，类将连接 ID 传递给`Broadcaster`类，以便`Broadcaster`类可以模拟`Clients.Others`。</span><span class="sxs-lookup"><span data-stu-id="2c251-443">In the following example, the `MoveShapeHub` class passes the connection ID to the `Broadcaster` class so that the `Broadcaster` class can simulate `Clients.Others`.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample73.cs?highlight=12,36)]

<a id="managinggroupsoutsidehub"></a>

### <a name="managing-group-membership"></a><span data-ttu-id="2c251-444">管理组成员身份</span><span class="sxs-lookup"><span data-stu-id="2c251-444">Managing group membership</span></span>

<span data-ttu-id="2c251-445">对于管理组，您具有与在中心类中相同的选项。</span><span class="sxs-lookup"><span data-stu-id="2c251-445">For managing groups you have the same options as you do in a Hub class.</span></span>

- <span data-ttu-id="2c251-446">将客户端添加到组</span><span class="sxs-lookup"><span data-stu-id="2c251-446">Add a client to a group</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample74.cs)]
- <span data-ttu-id="2c251-447">从组中删除客户端</span><span class="sxs-lookup"><span data-stu-id="2c251-447">Remove a client from a group</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample75.css)]

<a id="hubpipeline"></a>

## <a name="how-to-customize-the-hubs-pipeline"></a><span data-ttu-id="2c251-448">如何自定义中心管道</span><span class="sxs-lookup"><span data-stu-id="2c251-448">How to customize the Hubs pipeline</span></span>

<span data-ttu-id="2c251-449">SignalR 使您能够将您自己的代码注入集线器管道。</span><span class="sxs-lookup"><span data-stu-id="2c251-449">SignalR enables you to inject your own code into the Hub pipeline.</span></span> <span data-ttu-id="2c251-450">下面的示例显示了一个自定义 Hub 管道模块，该模块记录从客户端和在客户端上调用的传出方法调用收到的每个传入方法调用：</span><span class="sxs-lookup"><span data-stu-id="2c251-450">The following example shows a custom Hub pipeline module that logs each incoming method call received from the client and outgoing method call invoked on the client:</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample76.cs)]

<span data-ttu-id="2c251-451">*Startup.cs*文件中的以下代码注册要在集线器管道中运行的模块：</span><span class="sxs-lookup"><span data-stu-id="2c251-451">The following code in the *Startup.cs* file registers the module to run in the Hub pipeline:</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample77.cs?highlight=3)]

<span data-ttu-id="2c251-452">您可以重写许多不同的方法。</span><span class="sxs-lookup"><span data-stu-id="2c251-452">There are many different methods that you can override.</span></span> <span data-ttu-id="2c251-453">有关完整列表，请参阅[HubPipeline 模块方法](https://msdn.microsoft.com/library/jj918633(v=vs.111).aspx)。</span><span class="sxs-lookup"><span data-stu-id="2c251-453">For a complete list, see [HubPipelineModule Methods](https://msdn.microsoft.com/library/jj918633(v=vs.111).aspx).</span></span>

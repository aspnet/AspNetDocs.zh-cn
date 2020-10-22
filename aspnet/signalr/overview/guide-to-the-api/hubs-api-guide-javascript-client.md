---
uid: signalr/overview/guide-to-the-api/hubs-api-guide-javascript-client
title: ASP.NET SignalR 中心 API 指南-JavaScript 客户端 |Microsoft Docs
author: bradygaster
description: 本文档介绍了如何使用 JavaScript 客户端（如浏览器和 Windows 应用商店 (WinJS) applicat .。。
ms.author: bradyg
ms.date: 01/15/2019
ms.assetid: a9fd4dc0-1b96-4443-82ca-932a5b4a8ea4
msc.legacyurl: /signalr/overview/guide-to-the-api/hubs-api-guide-javascript-client
msc.type: authoredcontent
ms.openlocfilehash: 8befe133c3627dac1f7d011959c68e2054d345da
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345434"
---
# <a name="aspnet-signalr-hubs-api-guide---javascript-client"></a><span data-ttu-id="86532-103">ASP.NET SignalR 中心 API 指南-JavaScript 客户端</span><span class="sxs-lookup"><span data-stu-id="86532-103">ASP.NET SignalR Hubs API Guide - JavaScript Client</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="86532-104">本文档介绍了如何在 JavaScript 客户端（如浏览器和 Windows 应用商店 (WinJS) 应用程序）中使用适用于 SignalR 版本2的中心 API。</span><span class="sxs-lookup"><span data-stu-id="86532-104">This document provides an introduction to using the Hubs API for SignalR version 2 in JavaScript clients, such as browsers and Windows Store (WinJS) applications.</span></span>
>
> <span data-ttu-id="86532-105">通过 SignalR 中心 API，你可以 (Rpc) 从服务器连接到连接的客户端和从客户端到服务器的远程过程调用。</span><span class="sxs-lookup"><span data-stu-id="86532-105">The SignalR Hubs API enables you to make remote procedure calls (RPCs) from a server to connected clients and from clients to the server.</span></span> <span data-ttu-id="86532-106">在服务器代码中，你将定义可由客户端调用的方法，并调用在客户端上运行的方法。</span><span class="sxs-lookup"><span data-stu-id="86532-106">In server code, you define methods that can be called by clients, and you call methods that run on the client.</span></span> <span data-ttu-id="86532-107">在客户端代码中，定义可从服务器调用的方法，并调用在服务器上运行的方法。</span><span class="sxs-lookup"><span data-stu-id="86532-107">In client code, you define methods that can be called from the server, and you call methods that run on the server.</span></span> <span data-ttu-id="86532-108">SignalR 负责处理所有的客户端到服务器的操作。</span><span class="sxs-lookup"><span data-stu-id="86532-108">SignalR takes care of all of the client-to-server plumbing for you.</span></span>
>
> <span data-ttu-id="86532-109">SignalR 还提供名为持久性连接的较低级别 API。</span><span class="sxs-lookup"><span data-stu-id="86532-109">SignalR also offers a lower-level API called Persistent Connections.</span></span> <span data-ttu-id="86532-110">有关 SignalR、集线器和持续连接的简介，请参阅 [SignalR 简介](../getting-started/introduction-to-signalr.md)。</span><span class="sxs-lookup"><span data-stu-id="86532-110">For an introduction to SignalR, Hubs, and Persistent Connections, see [Introduction to SignalR](../getting-started/introduction-to-signalr.md).</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="86532-111">本主题中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="86532-111">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="86532-112">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="86532-112">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/)
> - <span data-ttu-id="86532-113">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="86532-113">.NET 4.5</span></span>
> - <span data-ttu-id="86532-114">SignalR 版本2</span><span class="sxs-lookup"><span data-stu-id="86532-114">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="86532-115">本主题的早期版本</span><span class="sxs-lookup"><span data-stu-id="86532-115">Previous versions of this topic</span></span>
>
> <span data-ttu-id="86532-116">有关早期版本的 SignalR 的信息，请参阅 [SignalR 旧版本](../older-versions/index.md)。</span><span class="sxs-lookup"><span data-stu-id="86532-116">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="86532-117">问题和注释</span><span class="sxs-lookup"><span data-stu-id="86532-117">Questions and comments</span></span>
>
> <span data-ttu-id="86532-118">请提供有关你喜欢本教程的方式的反馈，并在页面底部的评论中留下反馈。</span><span class="sxs-lookup"><span data-stu-id="86532-118">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="86532-119">如果你有与本教程不直接相关的问题，则可以将其发布到 [ASP.NET SignalR 论坛](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 或 [StackOverflow.com](http://stackoverflow.com/)。</span><span class="sxs-lookup"><span data-stu-id="86532-119">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="overview"></a><span data-ttu-id="86532-120">概述</span><span class="sxs-lookup"><span data-stu-id="86532-120">Overview</span></span>

<span data-ttu-id="86532-121">本文档包含以下各节：</span><span class="sxs-lookup"><span data-stu-id="86532-121">This document contains the following sections:</span></span>

- [<span data-ttu-id="86532-122">生成的代理以及它为你执行的操作</span><span class="sxs-lookup"><span data-stu-id="86532-122">The generated proxy and what it does for you</span></span>](#genproxy)

    - [<span data-ttu-id="86532-123">何时使用生成的代理</span><span class="sxs-lookup"><span data-stu-id="86532-123">When to use the generated proxy</span></span>](#cantusegenproxy)
- [<span data-ttu-id="86532-124">客户端设置</span><span class="sxs-lookup"><span data-stu-id="86532-124">Client Setup</span></span>](#clientsetup)

    - [<span data-ttu-id="86532-125">如何引用动态生成的代理</span><span class="sxs-lookup"><span data-stu-id="86532-125">How to reference the dynamically generated proxy</span></span>](#dynamicproxy)
    - [<span data-ttu-id="86532-126">如何为 SignalR 生成的代理创建物理文件</span><span class="sxs-lookup"><span data-stu-id="86532-126">How to create a physical file for the SignalR generated proxy</span></span>](#manualproxy)
- [<span data-ttu-id="86532-127">如何建立连接</span><span class="sxs-lookup"><span data-stu-id="86532-127">How to establish a connection</span></span>](#establishconnection)

    - [<span data-ttu-id="86532-128">$. 连接中心是与 hubConnection ( # A1 创建的对象相同的对象。</span><span class="sxs-lookup"><span data-stu-id="86532-128">$.connection.hub is the same object that $.hubConnection() creates</span></span>](#connequivalence)
    - [<span data-ttu-id="86532-129">开始方法的异步执行</span><span class="sxs-lookup"><span data-stu-id="86532-129">Asynchronous execution of the start method</span></span>](#asyncstart)
- [<span data-ttu-id="86532-130">如何建立跨域连接</span><span class="sxs-lookup"><span data-stu-id="86532-130">How to establish a cross-domain connection</span></span>](#crossdomain)
- [<span data-ttu-id="86532-131">如何配置连接</span><span class="sxs-lookup"><span data-stu-id="86532-131">How to configure the connection</span></span>](#configureconnection)

    - [<span data-ttu-id="86532-132">如何指定查询字符串参数</span><span class="sxs-lookup"><span data-stu-id="86532-132">How to specify query string parameters</span></span>](#querystring)
    - [<span data-ttu-id="86532-133">如何指定传输方法</span><span class="sxs-lookup"><span data-stu-id="86532-133">How to specify the transport method</span></span>](#transport)
- [<span data-ttu-id="86532-134">如何获取集线器类的代理</span><span class="sxs-lookup"><span data-stu-id="86532-134">How to get a proxy for a Hub class</span></span>](#getproxy)
- [<span data-ttu-id="86532-135">如何在客户端上定义服务器可以调用的方法</span><span class="sxs-lookup"><span data-stu-id="86532-135">How to define methods on the client that the server can call</span></span>](#callclient)
- [<span data-ttu-id="86532-136">如何从客户端调用服务器方法</span><span class="sxs-lookup"><span data-stu-id="86532-136">How to call server methods from the client</span></span>](#callserver)
- [<span data-ttu-id="86532-137">如何处理连接生存期事件</span><span class="sxs-lookup"><span data-stu-id="86532-137">How to handle connection lifetime events</span></span>](#connectionlifetime)
- [<span data-ttu-id="86532-138">如何处理错误</span><span class="sxs-lookup"><span data-stu-id="86532-138">How to handle errors</span></span>](#handleerrors)
- [<span data-ttu-id="86532-139">如何启用客户端日志记录</span><span class="sxs-lookup"><span data-stu-id="86532-139">How to enable client-side logging</span></span>](#logging)

<span data-ttu-id="86532-140">有关如何对服务器或 .NET 客户端进行编程的文档，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="86532-140">For documentation on how to program the server or .NET clients, see the following resources:</span></span>

- [<span data-ttu-id="86532-141">SignalR 中心 API 指南-服务器</span><span class="sxs-lookup"><span data-stu-id="86532-141">SignalR Hubs API Guide - Server</span></span>](hubs-api-guide-server.md)
- [<span data-ttu-id="86532-142">SignalR 中心 API 指南-.NET 客户端</span><span class="sxs-lookup"><span data-stu-id="86532-142">SignalR Hubs API Guide - .NET Client</span></span>](hubs-api-guide-net-client.md)

<span data-ttu-id="86532-143">SignalR 2 服务器组件仅适用于 .NET 4.5 (但 .net 4.0) 上有一个用于 SignalR 2 的 .NET 客户端。</span><span class="sxs-lookup"><span data-stu-id="86532-143">The SignalR 2 server component is only available on .NET 4.5 (though there is a .NET client for SignalR 2 on .NET 4.0).</span></span>

<a id="genproxy"></a>

## <a name="the-generated-proxy-and-what-it-does-for-you"></a><span data-ttu-id="86532-144">生成的代理以及它为你执行的操作</span><span class="sxs-lookup"><span data-stu-id="86532-144">The generated proxy and what it does for you</span></span>

<span data-ttu-id="86532-145">你可以对 JavaScript 客户端进行编程，以便使用或不使用 SignalR 生成的代理来与 SignalR 服务进行通信。</span><span class="sxs-lookup"><span data-stu-id="86532-145">You can program a JavaScript client to communicate with a SignalR service with or without a proxy that SignalR generates for you.</span></span> <span data-ttu-id="86532-146">代理的作用是简化用于连接的代码的语法，编写服务器调用的方法，并在服务器上调用方法。</span><span class="sxs-lookup"><span data-stu-id="86532-146">What the proxy does for you is simplify the syntax of the code you use to connect, write methods that the server calls, and call methods on the server.</span></span>

<span data-ttu-id="86532-147">当你编写代码来调用服务器方法时，生成的代理使你能够使用类似于你执行本地函数的语法：你可以编写 `serverMethod(arg1, arg2)` 而不是 `invoke('serverMethod', arg1, arg2)` 。</span><span class="sxs-lookup"><span data-stu-id="86532-147">When you write code to call server methods, the generated proxy enables you to use syntax that looks as though you were executing a local function: you can write `serverMethod(arg1, arg2)` instead of `invoke('serverMethod', arg1, arg2)`.</span></span> <span data-ttu-id="86532-148">如果错误键入服务器方法名称，生成的代理语法还会启用立即和可识别的客户端错误。</span><span class="sxs-lookup"><span data-stu-id="86532-148">The generated proxy syntax also enables an immediate and intelligible client-side error if you mistype a server method name.</span></span> <span data-ttu-id="86532-149">如果手动创建定义代理的文件，还可以获取对编写调用服务器方法的代码的 IntelliSense 支持。</span><span class="sxs-lookup"><span data-stu-id="86532-149">And if you manually create the file that defines the proxies, you can also get IntelliSense support for writing code that calls server methods.</span></span>

<span data-ttu-id="86532-150">例如，假设您在服务器上具有以下中心类：</span><span class="sxs-lookup"><span data-stu-id="86532-150">For example, suppose you have the following Hub class on the server:</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample1.cs?highlight=1,3,5)]

<span data-ttu-id="86532-151">下面的代码示例演示了 `NewContosoChatMessage` 在服务器上调用方法以及从服务器接收方法调用时，JavaScript 代码的外观 `addContosoChatMessageToPage` 。</span><span class="sxs-lookup"><span data-stu-id="86532-151">The following code examples show what JavaScript code looks like for invoking the `NewContosoChatMessage` method on the server and receiving invocations of the `addContosoChatMessageToPage` method from the server.</span></span>

<span data-ttu-id="86532-152">**与生成的代理**</span><span class="sxs-lookup"><span data-stu-id="86532-152">**With the generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample2.js?highlight=1-2,8)]

<span data-ttu-id="86532-153">**没有生成的代理**</span><span class="sxs-lookup"><span data-stu-id="86532-153">**Without the generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample3.js?highlight=2-3,9)]

<a id="cantusegenproxy"></a>

### <a name="when-to-use-the-generated-proxy"></a><span data-ttu-id="86532-154">何时使用生成的代理</span><span class="sxs-lookup"><span data-stu-id="86532-154">When to use the generated proxy</span></span>

<span data-ttu-id="86532-155">如果要为服务器调用的客户端方法注册多个事件处理程序，则不能使用生成的代理。</span><span class="sxs-lookup"><span data-stu-id="86532-155">If you want to register multiple event handlers for a client method that the server calls, you can't use the generated proxy.</span></span> <span data-ttu-id="86532-156">否则，你可以选择使用生成的代理，而不是基于编码首选项。</span><span class="sxs-lookup"><span data-stu-id="86532-156">Otherwise, you can choose to use the generated proxy or not based on your coding preference.</span></span> <span data-ttu-id="86532-157">如果选择不使用此方法，则无需在 `script` 客户端代码中引用元素中的 "signalr/hub" URL。</span><span class="sxs-lookup"><span data-stu-id="86532-157">If you choose not to use it, you don't have to reference the "signalr/hubs" URL in a `script` element in your client code.</span></span>

<a id="clientsetup"></a>

## <a name="client-setup"></a><span data-ttu-id="86532-158">客户端设置</span><span class="sxs-lookup"><span data-stu-id="86532-158">Client setup</span></span>

<span data-ttu-id="86532-159">JavaScript 客户端需要引用 jQuery 和 SignalR core JavaScript 文件。</span><span class="sxs-lookup"><span data-stu-id="86532-159">A JavaScript client requires references to jQuery and the SignalR core JavaScript file.</span></span> <span data-ttu-id="86532-160">JQuery 版本必须是1.6.4 或主要版本，如1.7.2、1.8.2 或1.9.1。</span><span class="sxs-lookup"><span data-stu-id="86532-160">The jQuery version must be 1.6.4 or major later versions, such as 1.7.2, 1.8.2, or 1.9.1.</span></span> <span data-ttu-id="86532-161">如果决定使用生成的代理，则还需要引用 SignalR 生成的代理 JavaScript 文件。</span><span class="sxs-lookup"><span data-stu-id="86532-161">If you decide to use the generated proxy, you also need a reference to the SignalR generated proxy JavaScript file.</span></span> <span data-ttu-id="86532-162">下面的示例演示在使用生成的代理的 HTML 页中，引用可能如下所示。</span><span class="sxs-lookup"><span data-stu-id="86532-162">The following example shows what the references might look like in an HTML page that uses the generated proxy.</span></span>

[!code-html[Main](hubs-api-guide-javascript-client/samples/sample4.html)]

<span data-ttu-id="86532-163">这些引用必须按以下顺序包含： jQuery first、SignalR core 之后，以及 SignalR 代理 last。</span><span class="sxs-lookup"><span data-stu-id="86532-163">These references must be included in this order: jQuery first, SignalR core after that, and SignalR proxies last.</span></span>

<a id="dynamicproxy"></a>

### <a name="how-to-reference-the-dynamically-generated-proxy"></a><span data-ttu-id="86532-164">如何引用动态生成的代理</span><span class="sxs-lookup"><span data-stu-id="86532-164">How to reference the dynamically generated proxy</span></span>

<span data-ttu-id="86532-165">在前面的示例中，对 SignalR 生成的代理的引用是动态生成的 JavaScript 代码，而不是物理文件。</span><span class="sxs-lookup"><span data-stu-id="86532-165">In the preceding example, the reference to the SignalR generated proxy is to dynamically generated JavaScript code, not to a physical file.</span></span> <span data-ttu-id="86532-166">SignalR 会动态地为代理创建 JavaScript 代码，并将其提供给客户端，以响应 "/signalr/hubs" URL。</span><span class="sxs-lookup"><span data-stu-id="86532-166">SignalR creates the JavaScript code for the proxy on the fly and serves it to the client in response to the "/signalr/hubs" URL.</span></span> <span data-ttu-id="86532-167">如果你在方法中为服务器上的 SignalR 连接指定了不同的基 URL `MapSignalR` ，则动态生成的代理文件的 url 是自定义 url，后面追加了 "/hubs"。</span><span class="sxs-lookup"><span data-stu-id="86532-167">If you specified a different base URL for SignalR connections on the server in your `MapSignalR` method, the URL for the dynamically generated proxy file is your custom URL with "/hubs" appended to it.</span></span>

> [!NOTE]
> <span data-ttu-id="86532-168">对于 Windows 8 (Windows 应用商店) JavaScript 客户端，请使用物理代理文件而不是动态生成的文件。</span><span class="sxs-lookup"><span data-stu-id="86532-168">For Windows 8 (Windows Store) JavaScript clients, use the physical proxy file instead of the dynamically generated one.</span></span> <span data-ttu-id="86532-169">有关详细信息，请参阅本主题后面的 [如何为 SignalR 生成的代理创建物理文件](#manualproxy) 。</span><span class="sxs-lookup"><span data-stu-id="86532-169">For more information, see [How to create a physical file for the SignalR generated proxy](#manualproxy) later in this topic.</span></span>

<span data-ttu-id="86532-170">在 ASP.NET MVC 4 或 5 Razor 视图中，使用波形符在代理文件引用中引用应用程序根目录：</span><span class="sxs-lookup"><span data-stu-id="86532-170">In an ASP.NET MVC 4 or 5 Razor view, use the tilde to refer to the application root in your proxy file reference:</span></span>

[!code-html[Main](hubs-api-guide-javascript-client/samples/sample5.html)]

<span data-ttu-id="86532-171">有关在 MVC 5 中使用 SignalR 的详细信息，请参阅 [使用 SignalR 和 MVC 5 入门](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)。</span><span class="sxs-lookup"><span data-stu-id="86532-171">For more information about using SignalR in MVC 5, see [Getting Started with SignalR and MVC 5](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md).</span></span>

<span data-ttu-id="86532-172">在 ASP.NET MVC 3 Razor 视图中，将用作 `Url.Content` 代理文件参考：</span><span class="sxs-lookup"><span data-stu-id="86532-172">In an ASP.NET MVC 3 Razor view, use `Url.Content` for your proxy file reference:</span></span>

[!code-cshtml[Main](hubs-api-guide-javascript-client/samples/sample6.cshtml)]

<span data-ttu-id="86532-173">在 ASP.NET Web 窗体应用程序中， `ResolveClientUrl` 为代理文件引用使用，或使用应用根相对路径通过 ScriptManager 注册它， (以颚化) 开头：</span><span class="sxs-lookup"><span data-stu-id="86532-173">In an ASP.NET Web Forms application, use `ResolveClientUrl` for your proxies file reference or register it via the ScriptManager using an app root relative path (starting with a tilde):</span></span>

[!code-aspx[Main](hubs-api-guide-javascript-client/samples/sample7.aspx)]

<span data-ttu-id="86532-174">作为一般规则，请使用与指定用于 CSS 或 JavaScript 文件的 "/signalr/hubs" URL 相同的方法。</span><span class="sxs-lookup"><span data-stu-id="86532-174">As a general rule, use the same method for specifying the "/signalr/hubs" URL that you use for CSS or JavaScript files.</span></span> <span data-ttu-id="86532-175">如果在不使用波形符的情况下指定 URL，则在 Visual Studio 中使用 IIS Express 进行测试时，应用程序将正常工作，但在部署到完整 IIS 时将失败并出现404错误。</span><span class="sxs-lookup"><span data-stu-id="86532-175">If you specify a URL without using a tilde, in some scenarios your application will work correctly when you test in Visual Studio using IIS Express but will fail with a 404 error when you deploy to full IIS.</span></span> <span data-ttu-id="86532-176">有关详细信息，请参阅 MSDN 网站上的在[Visual Studio for ASP.NET Web 项目的 Web 服务器中](https://msdn.microsoft.com/library/58wxa9w5.aspx)**解析对 Root-Level 资源的引用**。</span><span class="sxs-lookup"><span data-stu-id="86532-176">For more information, see **Resolving References to Root-Level Resources** in [Web Servers in Visual Studio for ASP.NET Web Projects](https://msdn.microsoft.com/library/58wxa9w5.aspx) on the MSDN site.</span></span>

<span data-ttu-id="86532-177">在调试模式下运行 Visual Studio 2017 中的 web 项目时，如果使用 Internet Explorer 作为浏览器，则可以在 "**脚本**" 下的**解决方案资源管理器**中查看该代理文件。</span><span class="sxs-lookup"><span data-stu-id="86532-177">When you run a web project in Visual Studio 2017 in debug mode, and if you use Internet Explorer as your browser, you can see the proxy file in **Solution Explorer** under **Scripts**.</span></span>

<span data-ttu-id="86532-178">若要查看文件的内容，请双击 " **中心**"。</span><span class="sxs-lookup"><span data-stu-id="86532-178">To see the contents of the file, double-click **hubs**.</span></span> <span data-ttu-id="86532-179">如果使用的不是 Visual Studio 2012 或2013和 Internet Explorer，或者不处于调试模式，还可以通过浏览到 "/signalR/hubs" URL 来获取文件的内容。</span><span class="sxs-lookup"><span data-stu-id="86532-179">If you are not using Visual Studio 2012 or 2013 and Internet Explorer, or if you are not in debug mode, you can also get the contents of the file by browsing to the "/signalR/hubs" URL.</span></span> <span data-ttu-id="86532-180">例如，如果你的站点运行于 `http://localhost:56699` ，请 `http://localhost:56699/SignalR/hubs` 在浏览器中转到。</span><span class="sxs-lookup"><span data-stu-id="86532-180">For example, if your site is running at `http://localhost:56699`, go to `http://localhost:56699/SignalR/hubs` in your browser.</span></span>

<a id="manualproxy"></a>

### <a name="how-to-create-a-physical-file-for-the-signalr-generated-proxy"></a><span data-ttu-id="86532-181">如何为 SignalR 生成的代理创建物理文件</span><span class="sxs-lookup"><span data-stu-id="86532-181">How to create a physical file for the SignalR generated proxy</span></span>

<span data-ttu-id="86532-182">作为动态生成的代理的替代方法，可以创建包含代理代码的物理文件，并引用该文件。</span><span class="sxs-lookup"><span data-stu-id="86532-182">As an alternative to the dynamically generated proxy, you can create a physical file that has the proxy code and reference that file.</span></span> <span data-ttu-id="86532-183">您可能想要执行此操作以控制缓存或绑定行为，或者在编码对服务器方法的调用时获取 IntelliSense。</span><span class="sxs-lookup"><span data-stu-id="86532-183">You might want to do that for control over caching or bundling behavior, or to get IntelliSense when you are coding calls to server methods.</span></span>

<span data-ttu-id="86532-184">若要创建代理文件，请执行以下步骤：</span><span class="sxs-lookup"><span data-stu-id="86532-184">To create a proxy file, perform the following steps:</span></span>

1. <span data-ttu-id="86532-185">安装 [SignalR. Utils](https://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/) NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="86532-185">Install the [Microsoft.AspNet.SignalR.Utils](https://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/) NuGet package.</span></span>
2. <span data-ttu-id="86532-186">打开命令提示符，浏览到包含 SignalR.exe 文件的 " *工具* " 文件夹。</span><span class="sxs-lookup"><span data-stu-id="86532-186">Open a command prompt and browse to the *tools* folder that contains the SignalR.exe file.</span></span> <span data-ttu-id="86532-187">"工具" 文件夹位于以下位置：</span><span class="sxs-lookup"><span data-stu-id="86532-187">The tools folder is at the following location:</span></span>

    `[your solution folder]\packages\Microsoft.AspNet.SignalR.Utils.2.1.0\tools`
3. <span data-ttu-id="86532-188">输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="86532-188">Enter the following command:</span></span>

    `signalr ghp /path:[path to the .dll that contains your Hub class]`

    <span data-ttu-id="86532-189">*.Dll*的路径通常为项目文件夹中的*bin*文件夹。</span><span class="sxs-lookup"><span data-stu-id="86532-189">The path to your *.dll* is typically the *bin* folder in your project folder.</span></span>

    <span data-ttu-id="86532-190">此命令在*signalr.exe*所在的文件夹中创建一个名为*server.js*的文件。</span><span class="sxs-lookup"><span data-stu-id="86532-190">This command creates a file named *server.js* in the same folder as *signalr.exe*.</span></span>
4. <span data-ttu-id="86532-191">将 *server.js* 文件放在项目中的适当文件夹中，将其重命名为适用于你的应用程序的，并在 "signalr/hub" 引用的位置添加对该文件的引用。</span><span class="sxs-lookup"><span data-stu-id="86532-191">Put the *server.js* file in an appropriate folder in your project, rename it as appropriate for your application, and add a reference to it in place of the "signalr/hubs" reference.</span></span>

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a><span data-ttu-id="86532-192">如何建立连接</span><span class="sxs-lookup"><span data-stu-id="86532-192">How to establish a connection</span></span>

<span data-ttu-id="86532-193">建立连接之前，必须先创建连接对象、创建代理，并为可从服务器调用的方法注册事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="86532-193">Before you can establish a connection, you have to create a connection object, create a proxy, and register event handlers for methods that can be called from the server.</span></span> <span data-ttu-id="86532-194">如果设置了代理和事件处理程序，则通过调用方法来建立连接 `start` 。</span><span class="sxs-lookup"><span data-stu-id="86532-194">When the proxy and event handlers are set up, establish the connection by calling the `start` method.</span></span>

<span data-ttu-id="86532-195">如果使用生成的代理，则无需在自己的代码中创建连接对象，因为生成的代理代码会为你执行该连接。</span><span class="sxs-lookup"><span data-stu-id="86532-195">If you are using the generated proxy, you don't have to create the connection object in your own code because the generated proxy code does it for you.</span></span>

<a id="nogenconnection"></a>

<span data-ttu-id="86532-196">\*\*使用生成的代理建立连接 () \*\*</span><span class="sxs-lookup"><span data-stu-id="86532-196">**Establish a connection (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample8.js?highlight=5)]

<span data-ttu-id="86532-197">\*\*建立连接 (没有生成的代理) \*\*</span><span class="sxs-lookup"><span data-stu-id="86532-197">**Establish a connection (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample9.js?highlight=1,6)]

<span data-ttu-id="86532-198">示例代码使用默认的 "/signalr" URL 连接到 SignalR 服务。</span><span class="sxs-lookup"><span data-stu-id="86532-198">The sample code uses the default "/signalr" URL to connect to your SignalR service.</span></span> <span data-ttu-id="86532-199">有关如何指定其他基 URL 的信息，请参阅 [ASP.NET SignalR HUB API 指南-Server-/SIGNALR URL](hubs-api-guide-server.md#signalrurl)。</span><span class="sxs-lookup"><span data-stu-id="86532-199">For information about how to specify a different base URL, see [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](hubs-api-guide-server.md#signalrurl).</span></span>

<span data-ttu-id="86532-200">默认情况下，中心位置是当前服务器;如果要连接到其他服务器，请在调用方法之前指定 URL `start` ，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="86532-200">By default, the hub location is the current server; if you are connecting to a different server, specify the URL before calling the `start` method, as shown in the following example:</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample10.js)]

> [!NOTE]
> <span data-ttu-id="86532-201">通常，在调用方法之前注册事件处理程序 `start` 以建立连接。</span><span class="sxs-lookup"><span data-stu-id="86532-201">Normally you register event handlers before calling the `start` method to establish the connection.</span></span> <span data-ttu-id="86532-202">如果要在建立连接后注册某些事件处理程序，则可以这样做，但必须在调用方法之前注册至少一个 () 事件处理程序 `start` 。</span><span class="sxs-lookup"><span data-stu-id="86532-202">If you want to register some event handlers after establishing the connection, you can do that, but you must register at least one of your event handler(s) before calling the `start` method.</span></span> <span data-ttu-id="86532-203">导致这种情况的原因之一是，应用程序中可以有很多的中心，但 `OnConnected` 如果只打算使用其中一种，则不希望在每个中心触发事件。</span><span class="sxs-lookup"><span data-stu-id="86532-203">One reason for this is that there can be many Hubs in an application, but you wouldn't want to trigger the `OnConnected` event on every Hub if you are only going to use to one of them.</span></span> <span data-ttu-id="86532-204">建立连接后，在集线器代理上存在客户端方法会告诉 SignalR 触发 `OnConnected` 事件。</span><span class="sxs-lookup"><span data-stu-id="86532-204">When the connection is established, the presence of a client method on a Hub's proxy is what tells SignalR to trigger the `OnConnected` event.</span></span> <span data-ttu-id="86532-205">如果在调用方法之前未注册任何事件处理程序 `start` ，则可以在中心调用方法，但不会调用中心的方法，也 `OnConnected` 不会从服务器中调用任何客户端方法。</span><span class="sxs-lookup"><span data-stu-id="86532-205">If you don't register any event handlers before calling the `start` method, you will be able to invoke methods on the Hub, but the Hub's `OnConnected` method won't be called and no client methods will be invoked from the server.</span></span>

<a id="connequivalence"></a>

### <a name="connectionhub-is-the-same-object-that-hubconnection-creates"></a><span data-ttu-id="86532-206">$. 连接中心是与 hubConnection ( # A1 创建的对象相同的对象。</span><span class="sxs-lookup"><span data-stu-id="86532-206">$.connection.hub is the same object that $.hubConnection() creates</span></span>

<span data-ttu-id="86532-207">如示例中所示，当你使用生成的代理时， `$.connection.hub` 引用连接对象。</span><span class="sxs-lookup"><span data-stu-id="86532-207">As you can see from the examples, when you use the generated proxy, `$.connection.hub` refers to the connection object.</span></span> <span data-ttu-id="86532-208">这是你在 `$.hubConnection()` 不使用生成的代理时调用的相同对象。</span><span class="sxs-lookup"><span data-stu-id="86532-208">This is the same object that you get by calling `$.hubConnection()` when you aren't using the generated proxy.</span></span> <span data-ttu-id="86532-209">生成的代理代码通过执行以下语句来创建连接：</span><span class="sxs-lookup"><span data-stu-id="86532-209">The generated proxy code creates the connection for you by executing the following statement:</span></span>

![在生成的代理文件中创建连接](hubs-api-guide-javascript-client/_static/image3.png)

<span data-ttu-id="86532-211">当你使用生成的代理时，你可以对使用连接对象执行的任何操作进行操作， `$.connection.hub` 而不是使用生成的代理。</span><span class="sxs-lookup"><span data-stu-id="86532-211">When you're using the generated proxy, you can do anything with `$.connection.hub` that you can do with a connection object when you're not using the generated proxy.</span></span>

<a id="asyncstart"></a>

### <a name="asynchronous-execution-of-the-start-method"></a><span data-ttu-id="86532-212">开始方法的异步执行</span><span class="sxs-lookup"><span data-stu-id="86532-212">Asynchronous execution of the start method</span></span>

<span data-ttu-id="86532-213">`start`方法以异步方式执行。</span><span class="sxs-lookup"><span data-stu-id="86532-213">The `start` method executes asynchronously.</span></span> <span data-ttu-id="86532-214">它返回 [JQuery 延迟的对象](http://api.jquery.com/category/deferred-object/)，这意味着你可以通过调用、和等方法添加回调函数 `pipe` `done` `fail` 。</span><span class="sxs-lookup"><span data-stu-id="86532-214">It returns a [jQuery Deferred object](http://api.jquery.com/category/deferred-object/), which means that you can add callback functions by calling methods such as `pipe`, `done`, and `fail`.</span></span> <span data-ttu-id="86532-215">如果你有想要在建立连接后执行的代码（例如，对服务器方法的调用），请将该代码放入回调函数或从回调函数调用它。</span><span class="sxs-lookup"><span data-stu-id="86532-215">If you have code that you want to execute after the connection is established, such as a call to a server method, put that code in a callback function or call it from a callback function.</span></span> <span data-ttu-id="86532-216">在 `.done` 建立连接后，以及在 `OnConnected` 服务器上的事件处理程序方法中的任何代码执行完毕后，将执行该回调方法。</span><span class="sxs-lookup"><span data-stu-id="86532-216">The `.done` callback method is executed after the connection has been established, and after any code that you have in your `OnConnected` event handler method on the server finishes executing.</span></span>

<span data-ttu-id="86532-217">如果将前面的示例中的 "现在连接的" 语句作为方法调用之后的下一行代码 `start` (不在 `.done` 回调) 中，则在 `console.log` 建立连接之前，将执行该行，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="86532-217">If you put the "Now connected" statement from the preceding example as the next line of code after the `start` method call (not in a `.done` callback), the `console.log` line will execute before the connection is established, as shown in the following example:</span></span>

![编写在建立连接后运行的代码的错误方法](hubs-api-guide-javascript-client/_static/image5.png)

<a id="crossdomain"></a>

## <a name="how-to-establish-a-cross-domain-connection"></a><span data-ttu-id="86532-219">如何建立跨域连接</span><span class="sxs-lookup"><span data-stu-id="86532-219">How to establish a cross-domain connection</span></span>

<span data-ttu-id="86532-220">通常，当浏览器从加载页面时 `http://contoso.com` ，SignalR 连接位于同一域中 `http://contoso.com/signalr` 。</span><span class="sxs-lookup"><span data-stu-id="86532-220">Typically if the browser loads a page from `http://contoso.com`, the SignalR connection is in the same domain, at `http://contoso.com/signalr`.</span></span> <span data-ttu-id="86532-221">如果中的页 `http://contoso.com` 建立了到的连接 `http://fabrikam.com/signalr` ，则这是一个跨域连接。</span><span class="sxs-lookup"><span data-stu-id="86532-221">If the page from `http://contoso.com` makes a connection to `http://fabrikam.com/signalr`, that is a cross-domain connection.</span></span> <span data-ttu-id="86532-222">出于安全原因，在默认情况下将禁用跨域连接。</span><span class="sxs-lookup"><span data-stu-id="86532-222">For security reasons, cross-domain connections are disabled by default.</span></span>

<span data-ttu-id="86532-223">在 SignalR 1.x 中，跨域请求由单个 EnableCrossDomain 标志控制。</span><span class="sxs-lookup"><span data-stu-id="86532-223">In SignalR 1.x, cross domain requests were controlled by a single EnableCrossDomain flag.</span></span> <span data-ttu-id="86532-224">此标志控制 JSONP 和 CORS 请求。</span><span class="sxs-lookup"><span data-stu-id="86532-224">This flag controlled both JSONP and CORS requests.</span></span> <span data-ttu-id="86532-225">为了获得更大的灵活性，已从 SignalR 的服务器组件中删除了所有 CORS 支持 (JavaScript 客户端在检测到浏览器支持它) 时仍使用 CORS，并提供新的 OWIN 中间件以支持这些方案。</span><span class="sxs-lookup"><span data-stu-id="86532-225">For greater flexibility, all CORS support has been removed from the server component of SignalR (JavaScript clients still use CORS normally if it is detected that the browser supports it), and new OWIN middleware has been made available to support these scenarios.</span></span>

<span data-ttu-id="86532-226">如果客户端 (需要 JSONP 以支持较早浏览器) 中的跨域请求，则需要通过将对象上的设置为来显式启用此功能 `EnableJSONP` `HubConfiguration` `true` ，如下所示。</span><span class="sxs-lookup"><span data-stu-id="86532-226">If JSONP is required on the client (to support cross-domain requests in older browsers), it will need to be enabled explicitly by setting `EnableJSONP` on the `HubConfiguration` object to `true`, as shown below.</span></span> <span data-ttu-id="86532-227">默认情况下，JSONP 处于禁用状态，因为它的安全性低于 CORS。</span><span class="sxs-lookup"><span data-stu-id="86532-227">JSONP is disabled by default, as it is less secure than CORS.</span></span>

<span data-ttu-id="86532-228">**将 Owin 添加到你的项目：** 若要安装此库，请在包管理器控制台中运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="86532-228">**Adding Microsoft.Owin.Cors to your project:** To install this library, run the following command in the Package Manager Console:</span></span>

`Install-Package Microsoft.Owin.Cors`

<span data-ttu-id="86532-229">此命令会将2.1.0 版本的包添加到你的项目。</span><span class="sxs-lookup"><span data-stu-id="86532-229">This command will add the 2.1.0 version of the package to your project.</span></span>

### <a name="calling-usecors"></a><span data-ttu-id="86532-230">调用 UseCors</span><span class="sxs-lookup"><span data-stu-id="86532-230">Calling UseCors</span></span>

 <span data-ttu-id="86532-231">下面的代码段演示如何在 SignalR 2 中实现跨域连接。</span><span class="sxs-lookup"><span data-stu-id="86532-231">The following code snippet demonstrates how to implement cross-domain connections in SignalR 2.</span></span>

<span data-ttu-id="86532-232">**在 SignalR 2 中实现跨域请求**</span><span class="sxs-lookup"><span data-stu-id="86532-232">**Implementing cross-domain requests in SignalR 2**</span></span>

<span data-ttu-id="86532-233">下面的代码演示如何在 SignalR 2 项目中启用 CORS 或 JSONP。</span><span class="sxs-lookup"><span data-stu-id="86532-233">The following code demonstrates how to enable CORS or JSONP in a SignalR 2 project.</span></span> <span data-ttu-id="86532-234">此代码示例使用 `Map` 和 `RunSignalR` 而不是 `MapSignalR` ，因此，CORS 中间件仅针对需要 CORS 支持 (而不是对中指定的路径中的所有流量运行的 SignalR 请求运行 `MapSignalR` 。 ) 映射还可用于需要针对特定 URL 前缀运行的任何其他中间件，而不是针对整个应用程序。</span><span class="sxs-lookup"><span data-stu-id="86532-234">This code sample uses `Map` and `RunSignalR` instead of `MapSignalR`, so that the CORS middleware runs only for the SignalR requests that require CORS support (rather than for all traffic at the path specified in `MapSignalR`.) Map can also be used for any other middleware that needs to run for a specific URL prefix, rather than for the entire application.</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample11.cs)]

> [!NOTE]
>
> - <span data-ttu-id="86532-235">不要 `jQuery.support.cors` 在代码中将设置为 true。</span><span class="sxs-lookup"><span data-stu-id="86532-235">Don't set `jQuery.support.cors` to true in your code.</span></span>
>
>     ![请勿将 jQuery. 支持 cors 设置为 true](hubs-api-guide-javascript-client/_static/image7.png)
>
>     <span data-ttu-id="86532-237">SignalR 处理 CORS 的使用。</span><span class="sxs-lookup"><span data-stu-id="86532-237">SignalR handles the use of CORS.</span></span> <span data-ttu-id="86532-238">如果将设置 `jQuery.support.cors` 为 true，则将禁用 JSONP，因为它会导致 SignalR 假定浏览器支持 CORS。</span><span class="sxs-lookup"><span data-stu-id="86532-238">Setting `jQuery.support.cors` to true disables JSONP because it causes SignalR to assume the browser supports CORS.</span></span>
> - <span data-ttu-id="86532-239">当你连接到 localhost URL 时，Internet Explorer 10 不会将其视为跨域连接，因此，即使你未在服务器上启用跨域连接，应用程序也会在本地使用 IE 10。</span><span class="sxs-lookup"><span data-stu-id="86532-239">When you're connecting to a localhost URL, Internet Explorer 10 won't consider it a cross-domain connection, so the application will work locally with IE 10 even if you haven't enabled cross-domain connections on the server.</span></span>
> - <span data-ttu-id="86532-240">有关使用 Internet Explorer 9 的跨域连接的信息，请参阅 [此 StackOverflow 线程](http://stackoverflow.com/questions/13573397/siganlr-ie9-cross-domain-request-dont-work)。</span><span class="sxs-lookup"><span data-stu-id="86532-240">For information about using cross-domain connections with Internet Explorer 9, see [this StackOverflow thread](http://stackoverflow.com/questions/13573397/siganlr-ie9-cross-domain-request-dont-work).</span></span>
> - <span data-ttu-id="86532-241">有关将跨域连接与 Chrome 一起使用的信息，请参阅 [此 StackOverflow 线程](http://stackoverflow.com/questions/15467373/signalr-1-0-1-cross-domain-request-cors-with-chrome)。</span><span class="sxs-lookup"><span data-stu-id="86532-241">For information about using cross-domain connections with Chrome, see [this StackOverflow thread](http://stackoverflow.com/questions/15467373/signalr-1-0-1-cross-domain-request-cors-with-chrome).</span></span>
> - <span data-ttu-id="86532-242">示例代码使用默认的 "/signalr" URL 连接到 SignalR 服务。</span><span class="sxs-lookup"><span data-stu-id="86532-242">The sample code uses the default "/signalr" URL to connect to your SignalR service.</span></span> <span data-ttu-id="86532-243">有关如何指定其他基 URL 的信息，请参阅 [ASP.NET SignalR HUB API 指南-Server-/SIGNALR URL](hubs-api-guide-server.md#signalrurl)。</span><span class="sxs-lookup"><span data-stu-id="86532-243">For information about how to specify a different base URL, see [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](hubs-api-guide-server.md#signalrurl).</span></span>

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a><span data-ttu-id="86532-244">如何配置连接</span><span class="sxs-lookup"><span data-stu-id="86532-244">How to configure the connection</span></span>

<span data-ttu-id="86532-245">在建立连接之前，您可以指定查询字符串参数或指定传输方法。</span><span class="sxs-lookup"><span data-stu-id="86532-245">Before you establish a connection, you can specify query string parameters or specify the transport method.</span></span>

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a><span data-ttu-id="86532-246">如何指定查询字符串参数</span><span class="sxs-lookup"><span data-stu-id="86532-246">How to specify query string parameters</span></span>

<span data-ttu-id="86532-247">如果要在客户端连接时将数据发送到服务器，则可以将查询字符串参数添加到连接对象。</span><span class="sxs-lookup"><span data-stu-id="86532-247">If you want to send data to the server when the client connects, you can add query string parameters to the connection object.</span></span> <span data-ttu-id="86532-248">下面的示例演示如何在客户端代码中设置查询字符串参数。</span><span class="sxs-lookup"><span data-stu-id="86532-248">The following examples show how to set a query string parameter in client code.</span></span>

<span data-ttu-id="86532-249">\*\*在调用 start 方法 (与生成的代理) 之前设置查询字符串值 \*\*</span><span class="sxs-lookup"><span data-stu-id="86532-249">**Set a query string value before calling the start method (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample12.js?highlight=1)]

<span data-ttu-id="86532-250">\*\*在调用 start 方法之前设置查询字符串值，不 (生成的代理) \*\*</span><span class="sxs-lookup"><span data-stu-id="86532-250">**Set a query string value before calling the start method (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample13.js?highlight=2)]

<span data-ttu-id="86532-251">下面的示例演示如何读取服务器代码中的查询字符串参数。</span><span class="sxs-lookup"><span data-stu-id="86532-251">The following example shows how to read a query string parameter in server code.</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample14.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a><span data-ttu-id="86532-252">如何指定传输方法</span><span class="sxs-lookup"><span data-stu-id="86532-252">How to specify the transport method</span></span>

<span data-ttu-id="86532-253">作为连接过程的一部分，SignalR 客户端通常与服务器协商以确定服务器和客户端支持的最佳传输。</span><span class="sxs-lookup"><span data-stu-id="86532-253">As part of the process of connecting, a SignalR client normally negotiates with the server to determine the best transport that is supported by both server and client.</span></span> <span data-ttu-id="86532-254">如果已知道要使用的传输，则可以在调用方法时指定传输方法，绕过此协商过程 `start` 。</span><span class="sxs-lookup"><span data-stu-id="86532-254">If you already know which transport you want to use, you can bypass this negotiation process by specifying the transport method when you call the `start` method.</span></span>

<span data-ttu-id="86532-255">\*\*指定传输方法与生成的代理 (的客户端代码) \*\*</span><span class="sxs-lookup"><span data-stu-id="86532-255">**Client code that specifies the transport method (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample15.js?highlight=1)]

<span data-ttu-id="86532-256">\*\*指定传输方法的客户端代码 (没有生成的代理) \*\*</span><span class="sxs-lookup"><span data-stu-id="86532-256">**Client code that specifies the transport method (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample16.js?highlight=2)]

<span data-ttu-id="86532-257">作为替代方法，你可以按你希望 SignalR 尝试的顺序指定多个传输方法：</span><span class="sxs-lookup"><span data-stu-id="86532-257">As an alternative, you can specify multiple transport methods in the order in which you want SignalR to try them:</span></span>

<span data-ttu-id="86532-258">\*\*指定自定义传输回退方案 (与生成的代理) 的客户端代码 \*\*</span><span class="sxs-lookup"><span data-stu-id="86532-258">**Client code that specifies a custom transport fallback scheme (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample17.js?highlight=1)]

<span data-ttu-id="86532-259">\*\*指定自定义传输回退方案 (的客户端代码，不包含生成的代理) \*\*</span><span class="sxs-lookup"><span data-stu-id="86532-259">**Client code that specifies a custom transport fallback scheme (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample18.js?highlight=2)]

<span data-ttu-id="86532-260">您可以使用以下值来指定传输方法：</span><span class="sxs-lookup"><span data-stu-id="86532-260">You can use the following values for specifying the transport method:</span></span>

- <span data-ttu-id="86532-261">Websocket</span><span class="sxs-lookup"><span data-stu-id="86532-261">"webSockets"</span></span>
- <span data-ttu-id="86532-262">"foreverFrame"</span><span class="sxs-lookup"><span data-stu-id="86532-262">"foreverFrame"</span></span>
- <span data-ttu-id="86532-263">"serverSentEvents"</span><span class="sxs-lookup"><span data-stu-id="86532-263">"serverSentEvents"</span></span>
- <span data-ttu-id="86532-264">"longPolling"</span><span class="sxs-lookup"><span data-stu-id="86532-264">"longPolling"</span></span>

<span data-ttu-id="86532-265">下面的示例演示如何查明某个连接正在使用哪种传输方法。</span><span class="sxs-lookup"><span data-stu-id="86532-265">The following examples show how to find out which transport method is being used by a connection.</span></span>

<span data-ttu-id="86532-266">\*\*显示连接所使用的传输方法的客户端代码 (与生成的代理) \*\*</span><span class="sxs-lookup"><span data-stu-id="86532-266">**Client code that displays the transport method used by a connection (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample19.js?highlight=2)]

<span data-ttu-id="86532-267">\*\*显示连接 (使用的传输方法的客户端代码，不包含生成的代理) \*\*</span><span class="sxs-lookup"><span data-stu-id="86532-267">**Client code that displays the transport method used by a connection (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample20.js?highlight=3)]

<span data-ttu-id="86532-268">有关如何在服务器代码中检查传输方法的信息，请参阅 [ASP.NET SignalR HUB API 指南-服务器-如何从上下文属性获取有关客户端的信息](hubs-api-guide-server.md#contextproperty)。</span><span class="sxs-lookup"><span data-stu-id="86532-268">For information about how to check the transport method in server code, see [ASP.NET SignalR Hubs API Guide - Server - How to get information about the client from the Context property](hubs-api-guide-server.md#contextproperty).</span></span> <span data-ttu-id="86532-269">有关传输和回退的详细信息，请参阅 [SignalR-传输和回退简介](../getting-started/introduction-to-signalr.md#transports)。</span><span class="sxs-lookup"><span data-stu-id="86532-269">For more information about transports and fallbacks, see [Introduction to SignalR - Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span>

<a id="getproxy"></a>

## <a name="how-to-get-a-proxy-for-a-hub-class"></a><span data-ttu-id="86532-270">如何获取集线器类的代理</span><span class="sxs-lookup"><span data-stu-id="86532-270">How to get a proxy for a Hub class</span></span>

<span data-ttu-id="86532-271">你创建的每个连接对象将封装有关与包含一个或多个中心类的 SignalR 服务的连接的信息。</span><span class="sxs-lookup"><span data-stu-id="86532-271">Each connection object that you create encapsulates information about a connection to a SignalR service that contains one or more Hub classes.</span></span> <span data-ttu-id="86532-272">若要与 Hub 类通信，可以使用自己创建的代理对象 (如果你未使用生成的代理) 或为你生成。</span><span class="sxs-lookup"><span data-stu-id="86532-272">To communicate with a Hub class, you use a proxy object which you create yourself (if you're not using the generated proxy) or which is generated for you.</span></span>

<span data-ttu-id="86532-273">在客户端上，代理名称为集线器类名的 camel 大小写形式。</span><span class="sxs-lookup"><span data-stu-id="86532-273">On the client the proxy name is a camel-cased version of the Hub class name.</span></span> <span data-ttu-id="86532-274">SignalR 会自动进行此更改，以便 JavaScript 代码可以符合 JavaScript 约定。</span><span class="sxs-lookup"><span data-stu-id="86532-274">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span>

<span data-ttu-id="86532-275">**服务器上的中心类**</span><span class="sxs-lookup"><span data-stu-id="86532-275">**Hub class on server**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample21.cs?highlight=1)]

<span data-ttu-id="86532-276">**获取对中心生成的客户端代理的引用**</span><span class="sxs-lookup"><span data-stu-id="86532-276">**Get a reference to the generated client proxy for the Hub**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample22.js?highlight=1)]

<span data-ttu-id="86532-277">\*\*为集线器类 (创建客户端代理，但不生成代理) \*\*</span><span class="sxs-lookup"><span data-stu-id="86532-277">**Create client proxy for the Hub class (without generated proxy)**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample23.cs?highlight=1)]

<span data-ttu-id="86532-278">如果使用属性修饰中心类 `HubName` ，请使用完全相同的名称，但不更改大小写。</span><span class="sxs-lookup"><span data-stu-id="86532-278">If you decorate your Hub class with a `HubName` attribute, use the exact name without changing case.</span></span>

<span data-ttu-id="86532-279">**服务器上具有 HubName 属性的中心类**</span><span class="sxs-lookup"><span data-stu-id="86532-279">**Hub class on server with HubName attribute**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample24.cs?highlight=1)]

<span data-ttu-id="86532-280">**获取对中心生成的客户端代理的引用**</span><span class="sxs-lookup"><span data-stu-id="86532-280">**Get a reference to the generated client proxy for the Hub**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample25.js?highlight=1)]

<span data-ttu-id="86532-281">\*\*为集线器类 (创建客户端代理，但不生成代理) \*\*</span><span class="sxs-lookup"><span data-stu-id="86532-281">**Create client proxy for the Hub class (without generated proxy)**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample26.cs?highlight=1)]

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a><span data-ttu-id="86532-282">如何在客户端上定义服务器可以调用的方法</span><span class="sxs-lookup"><span data-stu-id="86532-282">How to define methods on the client that the server can call</span></span>

<span data-ttu-id="86532-283">若要定义服务器可从集线器调用的方法，请使用生成的代理的属性向中心代理添加事件处理程序 `client` ， `on` 如果不使用生成的代理，则调用方法。</span><span class="sxs-lookup"><span data-stu-id="86532-283">To define a method that the server can call from a Hub, add an event handler to the Hub proxy by using the `client` property of the generated proxy, or call the `on` method if you aren't using the generated proxy.</span></span> <span data-ttu-id="86532-284">参数可以是复杂对象。</span><span class="sxs-lookup"><span data-stu-id="86532-284">The parameters can be complex objects.</span></span>

<span data-ttu-id="86532-285">在调用方法之前添加事件处理程序 `start` 以建立连接。</span><span class="sxs-lookup"><span data-stu-id="86532-285">Add the event handler before you call the `start` method to establish the connection.</span></span> <span data-ttu-id="86532-286"> (如果要在调用方法后添加事件处理程序 `start` ，请参阅本文档前面 [如何建立连接](#establishconnection) 中的说明，并使用所示的语法来定义方法，而不使用生成的代理。 ) </span><span class="sxs-lookup"><span data-stu-id="86532-286">(If you want to add event handlers after calling the `start` method, see the note in [How to establish a connection](#establishconnection) earlier in this document, and use the syntax shown for defining a method without using the generated proxy.)</span></span>

<span data-ttu-id="86532-287">方法名称匹配不区分大小写。</span><span class="sxs-lookup"><span data-stu-id="86532-287">Method name matching is case-insensitive.</span></span> <span data-ttu-id="86532-288">例如， `Clients.All.addContosoChatMessageToPage` 在服务器上，将在 `AddContosoChatMessageToPage` 客户端上执行、 `addContosoChatMessageToPage` 或 `addcontosochatmessagetopage` 。</span><span class="sxs-lookup"><span data-stu-id="86532-288">For example, `Clients.All.addContosoChatMessageToPage` on the server will execute `AddContosoChatMessageToPage`, `addContosoChatMessageToPage`, or `addcontosochatmessagetopage` on the client.</span></span>

<span data-ttu-id="86532-289">\*\*用生成的代理定义客户端 (的方法) \*\*</span><span class="sxs-lookup"><span data-stu-id="86532-289">**Define method on client (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample27.js?highlight=2)]

<span data-ttu-id="86532-290">\*\*用生成的代理定义客户端 (方法的替代方法) \*\*</span><span class="sxs-lookup"><span data-stu-id="86532-290">**Alternate way to define method on client (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample28.js?highlight=1-2)]

<span data-ttu-id="86532-291">\*\*在没有生成的代理的客户端 (上定义方法，或在调用 start 方法后添加) \*\*</span><span class="sxs-lookup"><span data-stu-id="86532-291">**Define method on client (without the generated proxy, or when adding after calling the start method)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample29.js?highlight=3)]

<span data-ttu-id="86532-292">**调用客户端方法的服务器代码**</span><span class="sxs-lookup"><span data-stu-id="86532-292">**Server code that calls the client method**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample30.cs?highlight=5)]

<span data-ttu-id="86532-293">下面的示例包含一个作为方法参数的复杂对象。</span><span class="sxs-lookup"><span data-stu-id="86532-293">The following examples include a complex object as a method parameter.</span></span>

<span data-ttu-id="86532-294">\*\*在客户端上定义 (使用生成的代理的复杂对象的方法) \*\*</span><span class="sxs-lookup"><span data-stu-id="86532-294">**Define method on client that takes a complex object (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample31.js?highlight=2-3)]

<span data-ttu-id="86532-295">\*\*在不使用生成的代理的情况下使用 (复杂对象的客户端上的定义方法) \*\*</span><span class="sxs-lookup"><span data-stu-id="86532-295">**Define method on client that takes a complex object (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample32.js?highlight=3-4)]

<span data-ttu-id="86532-296">**定义复杂对象的服务器代码**</span><span class="sxs-lookup"><span data-stu-id="86532-296">**Server code that defines the complex object**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample33.cs?highlight=1)]

<span data-ttu-id="86532-297">**使用复杂对象调用客户端方法的服务器代码**</span><span class="sxs-lookup"><span data-stu-id="86532-297">**Server code that calls the client method using a complex object**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample34.cs?highlight=3)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a><span data-ttu-id="86532-298">如何从客户端调用服务器方法</span><span class="sxs-lookup"><span data-stu-id="86532-298">How to call server methods from the client</span></span>

<span data-ttu-id="86532-299">若要从客户端调用服务器方法，请在 `server` 不使用生成的代理的情况下，使用生成的代理或 `invoke` 中心代理上的方法的属性。</span><span class="sxs-lookup"><span data-stu-id="86532-299">To call a server method from the client, use the `server` property of the generated proxy or the `invoke` method on the Hub proxy if you aren't using the generated proxy.</span></span> <span data-ttu-id="86532-300">返回值可以是复杂对象。</span><span class="sxs-lookup"><span data-stu-id="86532-300">The return value or parameters can be complex objects.</span></span>

<span data-ttu-id="86532-301">在集线器上传入方法名称的 camel 大小写形式。</span><span class="sxs-lookup"><span data-stu-id="86532-301">Pass in a camel-case version of the method name on the Hub.</span></span> <span data-ttu-id="86532-302">SignalR 会自动进行此更改，以便 JavaScript 代码可以符合 JavaScript 约定。</span><span class="sxs-lookup"><span data-stu-id="86532-302">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span>

<span data-ttu-id="86532-303">下面的示例演示如何调用没有返回值的服务器方法，以及如何调用具有返回值的服务器方法。</span><span class="sxs-lookup"><span data-stu-id="86532-303">The following examples show how to call a server method that doesn't have a return value and how to call a server method that does have a return value.</span></span>

<span data-ttu-id="86532-304">**不带 HubMethodName 属性的服务器方法**</span><span class="sxs-lookup"><span data-stu-id="86532-304">**Server method with no HubMethodName attribute**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample35.cs?highlight=3)]

<span data-ttu-id="86532-305">**定义在参数中传递的复杂对象的服务器代码**</span><span class="sxs-lookup"><span data-stu-id="86532-305">**Server code that defines the complex object passed in a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample36.cs)]

<span data-ttu-id="86532-306">\*\*调用服务器方法的客户端代码与生成的代理 () \*\*</span><span class="sxs-lookup"><span data-stu-id="86532-306">**Client code that invokes the server method (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample37.js?highlight=1)]

<span data-ttu-id="86532-307">\*\*在没有生成的代理) 的情况下调用服务器方法 (的客户端代码 \*\*</span><span class="sxs-lookup"><span data-stu-id="86532-307">**Client code that invokes the server method (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample38.js?highlight=1)]

<span data-ttu-id="86532-308">如果使用属性修饰了 Hub 方法 `HubMethodName` ，请在不更改大小写的情况下使用该名称。</span><span class="sxs-lookup"><span data-stu-id="86532-308">If you decorated the Hub method with a `HubMethodName` attribute, use that name without changing case.</span></span>

<span data-ttu-id="86532-309">具有 HubMethodName 属性的**服务器方法**</span><span class="sxs-lookup"><span data-stu-id="86532-309">**Server method** with a HubMethodName attribute</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample39.cs?highlight=3)]

<span data-ttu-id="86532-310">\*\*调用服务器方法的客户端代码与生成的代理 () \*\*</span><span class="sxs-lookup"><span data-stu-id="86532-310">**Client code that invokes the server method (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample40.js?highlight=1)]

<span data-ttu-id="86532-311">\*\*在没有生成的代理) 的情况下调用服务器方法 (的客户端代码 \*\*</span><span class="sxs-lookup"><span data-stu-id="86532-311">**Client code that invokes the server method (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample41.js?highlight=1)]

<span data-ttu-id="86532-312">前面的示例演示如何调用没有返回值的服务器方法。</span><span class="sxs-lookup"><span data-stu-id="86532-312">The preceding examples show how to call a server method that has no return value.</span></span> <span data-ttu-id="86532-313">下面的示例演示如何调用具有返回值的服务器方法。</span><span class="sxs-lookup"><span data-stu-id="86532-313">The following examples show how to call a server method that has a return value.</span></span>

<span data-ttu-id="86532-314">**具有返回值的方法的服务器代码**</span><span class="sxs-lookup"><span data-stu-id="86532-314">**Server code for a method that has a return value**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample42.cs?highlight=3)]

<span data-ttu-id="86532-315">用于返回值的**Stock 类**</span><span class="sxs-lookup"><span data-stu-id="86532-315">**The Stock class used for the** return value</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample43.cs?highlight=1)]

<span data-ttu-id="86532-316">\*\*调用服务器方法的客户端代码与生成的代理 () \*\*</span><span class="sxs-lookup"><span data-stu-id="86532-316">**Client code that invokes the server method (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample44.js?highlight=2,4-5)]

<span data-ttu-id="86532-317">\*\*在没有生成的代理) 的情况下调用服务器方法 (的客户端代码 \*\*</span><span class="sxs-lookup"><span data-stu-id="86532-317">**Client code that invokes the server method (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample45.js?highlight=2,4-5)]

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a><span data-ttu-id="86532-318">如何处理连接生存期事件</span><span class="sxs-lookup"><span data-stu-id="86532-318">How to handle connection lifetime events</span></span>

<span data-ttu-id="86532-319">SignalR 提供以下连接生存期事件，你可以处理这些事件：</span><span class="sxs-lookup"><span data-stu-id="86532-319">SignalR provides the following connection lifetime events that you can handle:</span></span>

- <span data-ttu-id="86532-320">`starting`：在通过连接发送任何数据之前引发。</span><span class="sxs-lookup"><span data-stu-id="86532-320">`starting`: Raised before any data is sent over the connection.</span></span>
- <span data-ttu-id="86532-321">`received`：在连接上接收到任何数据时引发。</span><span class="sxs-lookup"><span data-stu-id="86532-321">`received`: Raised when any data is received on the connection.</span></span> <span data-ttu-id="86532-322">提供接收的数据。</span><span class="sxs-lookup"><span data-stu-id="86532-322">Provides the received data.</span></span>
- <span data-ttu-id="86532-323">`connectionSlow`：当客户端检测到连接缓慢或频繁断开时引发。</span><span class="sxs-lookup"><span data-stu-id="86532-323">`connectionSlow`: Raised when the client detects a slow or frequently dropping connection.</span></span>
- <span data-ttu-id="86532-324">`reconnecting`：基础传输开始重新连接时引发。</span><span class="sxs-lookup"><span data-stu-id="86532-324">`reconnecting`: Raised when the underlying transport begins reconnecting.</span></span>
- <span data-ttu-id="86532-325">`reconnected`：当基础传输重新连接时引发。</span><span class="sxs-lookup"><span data-stu-id="86532-325">`reconnected`: Raised when the underlying transport has reconnected.</span></span>
- <span data-ttu-id="86532-326">`stateChanged`：连接状态更改时引发。</span><span class="sxs-lookup"><span data-stu-id="86532-326">`stateChanged`: Raised when the connection state changes.</span></span> <span data-ttu-id="86532-327">提供旧状态和新状态， (连接、连接、重新连接或断开连接) 。</span><span class="sxs-lookup"><span data-stu-id="86532-327">Provides the old state and the new state (Connecting, Connected, Reconnecting, or Disconnected).</span></span>
- <span data-ttu-id="86532-328">`disconnected`：连接断开连接时引发。</span><span class="sxs-lookup"><span data-stu-id="86532-328">`disconnected`: Raised when the connection has disconnected.</span></span>

<span data-ttu-id="86532-329">例如，如果要在存在可能导致明显延迟的连接问题时显示警告消息，请处理 `connectionSlow` 事件。</span><span class="sxs-lookup"><span data-stu-id="86532-329">For example, if you want to display warning messages when there are connection problems that might cause noticeable delays, handle the `connectionSlow` event.</span></span>

<span data-ttu-id="86532-330">\*\*处理 connectionSlow 事件 (与生成的代理) \*\*</span><span class="sxs-lookup"><span data-stu-id="86532-330">**Handle the connectionSlow event (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample46.js?highlight=1)]

<span data-ttu-id="86532-331">**在没有生成的代理) 的情况下处理 connectionSlow 事件 (**</span><span class="sxs-lookup"><span data-stu-id="86532-331">**Handle the connectionSlow event (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample47.js?highlight=2)]

<span data-ttu-id="86532-332">有关详细信息，请参阅 [了解和处理 SignalR 中的连接生存期事件](handling-connection-lifetime-events.md)。</span><span class="sxs-lookup"><span data-stu-id="86532-332">For more information, see [Understanding and Handling Connection Lifetime Events in SignalR](handling-connection-lifetime-events.md).</span></span>

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a><span data-ttu-id="86532-333">如何处理错误</span><span class="sxs-lookup"><span data-stu-id="86532-333">How to handle errors</span></span>

<span data-ttu-id="86532-334">SignalR JavaScript 客户端提供 `error` 可为其添加处理程序的事件。</span><span class="sxs-lookup"><span data-stu-id="86532-334">The SignalR JavaScript client provides an `error` event that you can add a handler for.</span></span> <span data-ttu-id="86532-335">还可以使用 fail 方法为服务器方法调用导致的错误添加处理程序。</span><span class="sxs-lookup"><span data-stu-id="86532-335">You can also use the fail method to add a handler for errors that result from a server method invocation.</span></span>

<span data-ttu-id="86532-336">如果未在服务器上显式启用详细的错误消息，则在出现错误后 SignalR 返回的异常对象包含有关错误的最小信息。</span><span class="sxs-lookup"><span data-stu-id="86532-336">If you don't explicitly enable detailed error messages on the server, the exception object that SignalR returns after an error contains minimal information about the error.</span></span> <span data-ttu-id="86532-337">例如，如果对的调用 `newContosoChatMessage` 失败，则出于安全原因，不建议将错误对象中的错误消息包含 " `There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.` " 向生产中的客户端发送详细的错误消息，但如果你想要启用详细的错误消息以进行故障排除，请在服务器上使用以下代码。</span><span class="sxs-lookup"><span data-stu-id="86532-337">For example, if a call to `newContosoChatMessage` fails, the error message in the error object contains "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" Sending detailed error messages to clients in production is not recommended for security reasons, but if you want to enable detailed error messages for troubleshooting purposes, use the following code on the server.</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample48.cs?highlight=2)]

<span data-ttu-id="86532-338">下面的示例演示如何为错误事件添加处理程序。</span><span class="sxs-lookup"><span data-stu-id="86532-338">The following example shows how to add a handler for the error event.</span></span>

<span data-ttu-id="86532-339">\*\*添加一个错误处理程序 (与生成的代理) \*\*</span><span class="sxs-lookup"><span data-stu-id="86532-339">**Add an error handler (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample49.js?highlight=1)]

<span data-ttu-id="86532-340">\*\*添加一个错误处理程序， (没有生成的代理) \*\*</span><span class="sxs-lookup"><span data-stu-id="86532-340">**Add an error handler (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample50.js?highlight=2)]

<span data-ttu-id="86532-341">下面的示例演示如何处理方法调用中的错误。</span><span class="sxs-lookup"><span data-stu-id="86532-341">The following example shows how to handle an error from a method invocation.</span></span>

<span data-ttu-id="86532-342">\*\*使用生成的代理从方法调用 (处理错误) \*\*</span><span class="sxs-lookup"><span data-stu-id="86532-342">**Handle an error from a method invocation (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample51.js?highlight=2)]

<span data-ttu-id="86532-343">\*\*处理方法调用中的错误， (没有生成的代理) \*\*</span><span class="sxs-lookup"><span data-stu-id="86532-343">**Handle an error from a method invocation (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample52.js?highlight=2)]

<span data-ttu-id="86532-344">如果方法调用失败，则 `error` 还会引发事件，因此将 `error` 执行方法处理程序和方法回调中的代码 `.fail` 。</span><span class="sxs-lookup"><span data-stu-id="86532-344">If a method invocation fails, the `error` event is also raised, so your code in the `error` method handler and in the `.fail` method callback would execute.</span></span>

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a><span data-ttu-id="86532-345">如何启用客户端日志记录</span><span class="sxs-lookup"><span data-stu-id="86532-345">How to enable client-side logging</span></span>

<span data-ttu-id="86532-346">若要对连接启用客户端日志记录，请在 `logging` 调用方法之前设置连接对象的属性， `start` 以建立连接。</span><span class="sxs-lookup"><span data-stu-id="86532-346">To enable client-side logging on a connection, set the `logging` property on the connection object before you call the `start` method to establish the connection.</span></span>

<span data-ttu-id="86532-347">\*\*使用生成的代理启用日志记录 () \*\*</span><span class="sxs-lookup"><span data-stu-id="86532-347">**Enable logging (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample53.js?highlight=1)]

<span data-ttu-id="86532-348">\*\*启用没有生成的代理)  (日志记录 \*\*</span><span class="sxs-lookup"><span data-stu-id="86532-348">**Enable logging (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample54.js?highlight=2)]

<span data-ttu-id="86532-349">若要查看日志，请打开浏览器的开发人员工具，并切换到 "控制台" 选项卡。有关显示如何执行此操作的分步说明和屏幕截图的教程，请参阅 [使用 ASP.NET Signalr 进行服务器广播-启用日志记录](../getting-started/tutorial-server-broadcast-with-signalr.md#enable-logging)。</span><span class="sxs-lookup"><span data-stu-id="86532-349">To see the logs, open your browser's developer tools and go to the Console tab. For a tutorial that shows step-by-step instructions and screen shots that show how to do this, see [Server Broadcast with ASP.NET Signalr - Enable Logging](../getting-started/tutorial-server-broadcast-with-signalr.md#enable-logging).</span></span>

---
uid: signalr/overview/older-versions/troubleshooting
title: 信号R故障排除（信号R 1.x） |微软文档
author: bradygaster
description: 本文介绍了开发SignalR应用的常见问题。
ms.author: bradyg
ms.date: 06/05/2013
ms.assetid: 347210ba-c452-4feb-886f-b51d89f58971
msc.legacyurl: /signalr/overview/older-versions/troubleshooting
msc.type: authoredcontent
ms.openlocfilehash: e65ce086d28cff2a36c609f47a05af632081be63
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543088"
---
# <a name="signalr-troubleshooting-signalr-1x"></a><span data-ttu-id="ffa79-103">SignalR 疑难解答 (SignalR 1.x)</span><span class="sxs-lookup"><span data-stu-id="ffa79-103">SignalR Troubleshooting (SignalR 1.x)</span></span>

<span data-ttu-id="ffa79-104">由[帕特里克·弗莱彻](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="ffa79-104">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="ffa79-105">本文档介绍 SignalR 的常见故障排除问题。</span><span class="sxs-lookup"><span data-stu-id="ffa79-105">This document describes common troubleshooting issues with SignalR.</span></span>

<span data-ttu-id="ffa79-106">本文档包含以下部分。</span><span class="sxs-lookup"><span data-stu-id="ffa79-106">This document contains the following sections.</span></span>

- [<span data-ttu-id="ffa79-107">客户端和服务器之间的调用方法以静默方式失败</span><span class="sxs-lookup"><span data-stu-id="ffa79-107">Calling methods between the client and server silently fails</span></span>](#connection)
- [<span data-ttu-id="ffa79-108">其他连接问题</span><span class="sxs-lookup"><span data-stu-id="ffa79-108">Other connection issues</span></span>](#other)
- [<span data-ttu-id="ffa79-109">编译和服务器端错误</span><span class="sxs-lookup"><span data-stu-id="ffa79-109">Compilation and server-side errors</span></span>](#server)
- [<span data-ttu-id="ffa79-110">视觉工作室问题</span><span class="sxs-lookup"><span data-stu-id="ffa79-110">Visual Studio issues</span></span>](#vs)
- [<span data-ttu-id="ffa79-111">互联网信息服务问题</span><span class="sxs-lookup"><span data-stu-id="ffa79-111">Internet Information Services issues</span></span>](#iis)
- [<span data-ttu-id="ffa79-112">Azure 问题</span><span class="sxs-lookup"><span data-stu-id="ffa79-112">Azure issues</span></span>](#azure)

<a id="connection"></a>

## <a name="calling-methods-between-the-client-and-server-silently-fails"></a><span data-ttu-id="ffa79-113">客户端和服务器之间的调用方法以静默方式失败</span><span class="sxs-lookup"><span data-stu-id="ffa79-113">Calling methods between the client and server silently fails</span></span>

<span data-ttu-id="ffa79-114">本节介绍客户端和服务器之间的方法调用失败而不出现有意义的错误消息的可能原因。</span><span class="sxs-lookup"><span data-stu-id="ffa79-114">This section describes possible causes for a method call between client and server to fail without a meaningful error message.</span></span> <span data-ttu-id="ffa79-115">在 SignalR 应用程序中，服务器没有关于客户端实现的方法的信息;因此，服务器没有实现的方法。当服务器调用客户端方法时，方法名称和参数数据将发送到客户端，并且仅当该方法以服务器指定的格式存在时才执行该方法。</span><span class="sxs-lookup"><span data-stu-id="ffa79-115">In a SignalR application, the server has no information about the methods that the client implements; when the server invokes a client method, the method name and parameter data are sent to the client, and the method is executed only if it exists in the format that the server specified.</span></span> <span data-ttu-id="ffa79-116">如果在客户端上找不到匹配方法，则不发生任何操作，并且服务器上不引发错误消息。</span><span class="sxs-lookup"><span data-stu-id="ffa79-116">If no matching method is found on the client, nothing happens, and no error message is raised on the server.</span></span>

<span data-ttu-id="ffa79-117">要进一步调查未被调用的客户端方法，可以在调用集线器上的 start 方法之前打开日志记录，以查看来自服务器的调用。</span><span class="sxs-lookup"><span data-stu-id="ffa79-117">To further investigate client methods not getting called, you can turn on logging before calling the start method on the hub to see what calls are coming from the server.</span></span> <span data-ttu-id="ffa79-118">要在 JavaScript 应用程序中启用日志记录，请参阅[如何启用客户端日志记录（JavaScript 客户端版本）。](../guide-to-the-api/hubs-api-guide-javascript-client.md#logging)</span><span class="sxs-lookup"><span data-stu-id="ffa79-118">To enable logging in a JavaScript application, see [How to enable client-side logging (JavaScript client version)](../guide-to-the-api/hubs-api-guide-javascript-client.md#logging).</span></span> <span data-ttu-id="ffa79-119">要在 .NET 客户端应用程序中启用日志记录，请参阅[如何启用客户端日志记录 （.NET 客户端版本）。](../guide-to-the-api/hubs-api-guide-net-client.md#logging)</span><span class="sxs-lookup"><span data-stu-id="ffa79-119">To enable logging in a .NET client application, see [How to enable client-side logging (.NET Client version)](../guide-to-the-api/hubs-api-guide-net-client.md#logging).</span></span>

### <a name="misspelled-method-incorrect-method-signature-or-incorrect-hub-name"></a><span data-ttu-id="ffa79-120">拼写错误的方法、不正确的方法签名或不正确的中心名称</span><span class="sxs-lookup"><span data-stu-id="ffa79-120">Misspelled method, incorrect method signature, or incorrect hub name</span></span>

<span data-ttu-id="ffa79-121">如果被调用方法的名称或签名与客户端上的适当方法不完全匹配，则调用将失败。</span><span class="sxs-lookup"><span data-stu-id="ffa79-121">If the name or signature of a called method does not exactly match an appropriate method on the client, the call will fail.</span></span> <span data-ttu-id="ffa79-122">验证服务器调用的方法名称是否与客户端上的方法的名称匹配。</span><span class="sxs-lookup"><span data-stu-id="ffa79-122">Verify that the method name called by the server matches the name of the method on the client.</span></span> <span data-ttu-id="ffa79-123">此外，SignalR 使用骆驼大小写方法创建集线器代理，这在 JavaScript 中是合适的`SendMessage`，因此在客户端代理中`sendMessage`调用服务器上调用的方法。</span><span class="sxs-lookup"><span data-stu-id="ffa79-123">Also, SignalR creates the hub proxy using camel-cased methods, as is appropriate in JavaScript, so a method called `SendMessage` on the server would be called `sendMessage` in the client proxy.</span></span> <span data-ttu-id="ffa79-124">如果在服务器端代码`HubName`中使用该属性，请验证所使用的名称是否与在客户端上创建中心的名称匹配。</span><span class="sxs-lookup"><span data-stu-id="ffa79-124">If you use the `HubName` attribute in your server-side code, verify that the name used matches the name used to create the hub on the client.</span></span> <span data-ttu-id="ffa79-125">如果不使用 该`HubName`属性，请验证 JavaScript 客户端中中心的名称是否为骆驼大小写，例如聊天Hub而不是 ChatHub。</span><span class="sxs-lookup"><span data-stu-id="ffa79-125">If you do not use the `HubName` attribute, verify that the name of the hub in a JavaScript client is camel-cased, such as chatHub instead of ChatHub.</span></span>

### <a name="duplicate-method-name-on-client"></a><span data-ttu-id="ffa79-126">客户端上的重复方法名称</span><span class="sxs-lookup"><span data-stu-id="ffa79-126">Duplicate method name on client</span></span>

<span data-ttu-id="ffa79-127">验证客户端上没有仅因大小写而异的重复方法。</span><span class="sxs-lookup"><span data-stu-id="ffa79-127">Verify that you do not have a duplicate method on the client that differs only by case.</span></span> <span data-ttu-id="ffa79-128">如果客户端应用程序具有称为`sendMessage`的方法，请验证是否也没有调用`SendMessage`的方法。</span><span class="sxs-lookup"><span data-stu-id="ffa79-128">If your client application has a method called `sendMessage`, verify that there isn't also a method called `SendMessage` as well.</span></span>

### <a name="missing-json-parser-on-the-client"></a><span data-ttu-id="ffa79-129">客户端上缺少 JSON 解析器</span><span class="sxs-lookup"><span data-stu-id="ffa79-129">Missing JSON parser on the client</span></span>

<span data-ttu-id="ffa79-130">SignalR 需要 JSON 解析器存在以序列化服务器和客户端之间的呼叫。</span><span class="sxs-lookup"><span data-stu-id="ffa79-130">SignalR requires a JSON parser to be present to serialize calls between the server and the client.</span></span> <span data-ttu-id="ffa79-131">如果客户端没有内置的 JSON 解析器（如 Internet Explorer 7），则需要在应用程序中包含一个。</span><span class="sxs-lookup"><span data-stu-id="ffa79-131">If your client doesn't have a built-in JSON parser (such as Internet Explorer 7), you'll need to include one in your application.</span></span> <span data-ttu-id="ffa79-132">你可以[在这里](http://nuget.org/packages/json2)下载JSON解析器。</span><span class="sxs-lookup"><span data-stu-id="ffa79-132">You can download the JSON parser [here](http://nuget.org/packages/json2).</span></span>

### <a name="mixing-hub-and-persistentconnection-syntax"></a><span data-ttu-id="ffa79-133">混合集线器和持久连接语法</span><span class="sxs-lookup"><span data-stu-id="ffa79-133">Mixing Hub and PersistentConnection syntax</span></span>

<span data-ttu-id="ffa79-134">SignalR 使用两种通信模型：集线器和持久连接。</span><span class="sxs-lookup"><span data-stu-id="ffa79-134">SignalR uses two communication models: Hubs and PersistentConnections.</span></span> <span data-ttu-id="ffa79-135">调用这两种通信模型的语法在客户端代码中是不同的。</span><span class="sxs-lookup"><span data-stu-id="ffa79-135">The syntax for calling these two communication models is different in the client code.</span></span> <span data-ttu-id="ffa79-136">如果在服务器代码中添加了中心，请验证所有客户端代码是否使用正确的中心语法。</span><span class="sxs-lookup"><span data-stu-id="ffa79-136">If you have added a hub in your server code, verify that all of your client code uses the proper hub syntax.</span></span>

<span data-ttu-id="ffa79-137">**在 JavaScript 客户端中创建持久连接的 JavaScript 客户端代码**</span><span class="sxs-lookup"><span data-stu-id="ffa79-137">**JavaScript client code that creates a PersistentConnection in a JavaScript client**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample1.js)]

<span data-ttu-id="ffa79-138">**在 Javascript 客户端中创建中心代理的 JavaScript 客户端代码**</span><span class="sxs-lookup"><span data-stu-id="ffa79-138">**JavaScript client code that creates a Hub Proxy in a Javascript client**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample2.js)]

<span data-ttu-id="ffa79-139">**将路由映射到持久连接的 C# 服务器代码**</span><span class="sxs-lookup"><span data-stu-id="ffa79-139">**C# server code that maps a route to a PersistentConnection**</span></span>

[!code-csharp[Main](troubleshooting/samples/sample3.cs)]

<span data-ttu-id="ffa79-140">**C# 服务器代码，用于将路由映射到集线器，或者如果您有多个应用程序，则映射到多个集线器**</span><span class="sxs-lookup"><span data-stu-id="ffa79-140">**C# server code that maps a route to a Hub, or to multiple hubs if you have multiple applications**</span></span>

[!code-csharp[Main](troubleshooting/samples/sample4.cs)]

### <a name="connection-started-before-subscriptions-are-added"></a><span data-ttu-id="ffa79-141">添加订阅之前启动的连接</span><span class="sxs-lookup"><span data-stu-id="ffa79-141">Connection started before subscriptions are added</span></span>

<span data-ttu-id="ffa79-142">如果在将可以从服务器调用的方法添加到代理之前启动中心连接，将不会接收消息。</span><span class="sxs-lookup"><span data-stu-id="ffa79-142">If the Hub's connection is started before methods that can be called from the server are added to the proxy, messages will not be received.</span></span> <span data-ttu-id="ffa79-143">以下 JavaScript 代码将无法正确启动中心：</span><span class="sxs-lookup"><span data-stu-id="ffa79-143">The following JavaScript code will not start the hub properly:</span></span>

<span data-ttu-id="ffa79-144">**不正确的 JavaScript 客户端代码，不允许接收中心消息**</span><span class="sxs-lookup"><span data-stu-id="ffa79-144">**Incorrect JavaScript client code that will not allow Hubs messages to be received**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample5.js)]

<span data-ttu-id="ffa79-145">而是在调用"开始"之前添加方法订阅：</span><span class="sxs-lookup"><span data-stu-id="ffa79-145">Instead, add the method subscriptions before calling Start:</span></span>

<span data-ttu-id="ffa79-146">**正确将订阅添加到中心的 JavaScript 客户端代码**</span><span class="sxs-lookup"><span data-stu-id="ffa79-146">**JavaScript client code that correctly adds subscriptions to a hub**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample6.js)]

### <a name="missing-method-name-on-the-hub-proxy"></a><span data-ttu-id="ffa79-147">中心代理上缺少方法名称</span><span class="sxs-lookup"><span data-stu-id="ffa79-147">Missing method name on the hub proxy</span></span>

<span data-ttu-id="ffa79-148">验证在服务器上定义的方法是否订阅在客户端上。</span><span class="sxs-lookup"><span data-stu-id="ffa79-148">Verify that the method defined on the server is subscribed to on the client.</span></span> <span data-ttu-id="ffa79-149">即使服务器定义了该方法，仍必须将其添加到客户端代理中。</span><span class="sxs-lookup"><span data-stu-id="ffa79-149">Even though the server defines the method, it must still be added to the client proxy.</span></span> <span data-ttu-id="ffa79-150">方法可以通过以下方式添加到客户端代理（请注意，该方法已添加到中心`client`成员，而不是直接添加到中心）：</span><span class="sxs-lookup"><span data-stu-id="ffa79-150">Methods can be added to the client proxy in the following ways (Note that the method is added to the `client` member of the hub, not the hub directly):</span></span>

<span data-ttu-id="ffa79-151">**将方法添加到中心代理的 JavaScript 客户端代码**</span><span class="sxs-lookup"><span data-stu-id="ffa79-151">**JavaScript client code that adds methods to a hub proxy**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample7.js)]

### <a name="hub-or-hub-methods-not-declared-as-public"></a><span data-ttu-id="ffa79-152">未声明为公共的集线器或中心方法</span><span class="sxs-lookup"><span data-stu-id="ffa79-152">Hub or hub methods not declared as Public</span></span>

<span data-ttu-id="ffa79-153">要在客户端上可见，必须将中心实现和方法声明为`public`。</span><span class="sxs-lookup"><span data-stu-id="ffa79-153">To be visible on the client, the hub implementation and methods must be declared as `public`.</span></span>

### <a name="accessing-hub-from-a-different-application"></a><span data-ttu-id="ffa79-154">从其他应用程序访问集线器</span><span class="sxs-lookup"><span data-stu-id="ffa79-154">Accessing hub from a different application</span></span>

<span data-ttu-id="ffa79-155">信号R中心只能通过实现SignalR客户端的应用程序进行访问。</span><span class="sxs-lookup"><span data-stu-id="ffa79-155">SignalR Hubs can only be accessed through applications that implement SignalR clients.</span></span> <span data-ttu-id="ffa79-156">SignalR 不能与其他通信库（如 SOAP 或 WCF Web 服务）互操作。如果目标平台没有可用的 SignalR 客户端，则无法直接访问服务器的终结点。</span><span class="sxs-lookup"><span data-stu-id="ffa79-156">SignalR cannot interoperate with other communication libraries (like SOAP or WCF web services.) If there is no SignalR client available for your target platform, you cannot access the server's endpoint directly.</span></span>

### <a name="manually-serializing-data"></a><span data-ttu-id="ffa79-157">手动序列化数据</span><span class="sxs-lookup"><span data-stu-id="ffa79-157">Manually serializing data</span></span>

<span data-ttu-id="ffa79-158">SignalR 将自动使用 JSON 来序列化方法参数 - 无需自行执行。</span><span class="sxs-lookup"><span data-stu-id="ffa79-158">SignalR will automatically use JSON to serialize your method parameters- there's no need to do it yourself.</span></span>

### <a name="remote-hub-method-not-executed-on-client-in-ondisconnected-function"></a><span data-ttu-id="ffa79-159">在 OnDisconnected 函数中的客户端上未执行远程中心方法</span><span class="sxs-lookup"><span data-stu-id="ffa79-159">Remote Hub method not executed on client in OnDisconnected function</span></span>

<span data-ttu-id="ffa79-160">这是设计的行为。</span><span class="sxs-lookup"><span data-stu-id="ffa79-160">This behavior is by design.</span></span> <span data-ttu-id="ffa79-161">调用`OnDisconnected`时，中心已进入状态`Disconnected`，不允许调用其他集线器方法。</span><span class="sxs-lookup"><span data-stu-id="ffa79-161">When `OnDisconnected` is called, the hub has already entered the `Disconnected` state, which does not allow further hub methods to be called.</span></span>

<span data-ttu-id="ffa79-162">**C# 服务器代码，在"不断开"事件中正确执行代码**</span><span class="sxs-lookup"><span data-stu-id="ffa79-162">**C# server code that correctly executes code in the OnDisconnected event**</span></span>

[!code-csharp[Main](troubleshooting/samples/sample8.cs)]

### <a name="connection-limit-reached"></a><span data-ttu-id="ffa79-163">达到连接限制</span><span class="sxs-lookup"><span data-stu-id="ffa79-163">Connection limit reached</span></span>

<span data-ttu-id="ffa79-164">在 Windows 7 等客户端操作系统上使用完整版本的 IIS 时，将强制实施 10 个连接限制。</span><span class="sxs-lookup"><span data-stu-id="ffa79-164">When using the full version of IIS on a client operating system like Windows 7, a 10-connection limit is imposed.</span></span> <span data-ttu-id="ffa79-165">使用客户端操作系统时，请使用 IIS Express 来避免此限制。</span><span class="sxs-lookup"><span data-stu-id="ffa79-165">When using a client OS, use IIS Express instead to avoid this limit.</span></span>

### <a name="cross-domain-connection-not-set-up-properly"></a><span data-ttu-id="ffa79-166">跨域连接设置不正确</span><span class="sxs-lookup"><span data-stu-id="ffa79-166">Cross-domain connection not set up properly</span></span>

<span data-ttu-id="ffa79-167">如果跨域连接（SignalR URL 与托管页不在同一域中的连接）设置不正确，则连接可能会失败，而不会出现错误消息。</span><span class="sxs-lookup"><span data-stu-id="ffa79-167">If a cross-domain connection (a connection for which the SignalR URL is not in the same domain as the hosting page) is not set up correctly, the connection may fail without an error message.</span></span> <span data-ttu-id="ffa79-168">有关如何启用跨域通信的信息，请参阅[如何建立跨域连接](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)。</span><span class="sxs-lookup"><span data-stu-id="ffa79-168">For information on how to enable cross-domain communication, see [How to establish a cross-domain connection](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).</span></span>

### <a name="connection-using-ntlm-active-directory-not-working-in-net-client"></a><span data-ttu-id="ffa79-169">使用 NTLM（活动目录）在 .NET 客户端中不起作用的连接</span><span class="sxs-lookup"><span data-stu-id="ffa79-169">Connection using NTLM (Active Directory) not working in .NET client</span></span>

<span data-ttu-id="ffa79-170">如果连接配置不正确，则使用域安全的 .NET 客户端应用程序中的连接可能会失败。</span><span class="sxs-lookup"><span data-stu-id="ffa79-170">A connection in a .NET client application that uses Domain security may fail if the connection is not configured properly.</span></span> <span data-ttu-id="ffa79-171">要在域环境中使用 SignalR，请使用如下方式设置所需的连接属性：</span><span class="sxs-lookup"><span data-stu-id="ffa79-171">To use SignalR in a domain environment, set the requisite connection property as follows:</span></span>

<span data-ttu-id="ffa79-172">**实现连接凭据的 C# 客户端代码**</span><span class="sxs-lookup"><span data-stu-id="ffa79-172">**C# client code that implements connection credentials**</span></span>

[!code-csharp[Main](troubleshooting/samples/sample9.cs)]

<a id="other"></a>

## <a name="other-connection-issues"></a><span data-ttu-id="ffa79-173">其他连接问题</span><span class="sxs-lookup"><span data-stu-id="ffa79-173">Other connection issues</span></span>

<span data-ttu-id="ffa79-174">本节介绍连接过程中发生的特定症状或错误消息的原因和解决方案。</span><span class="sxs-lookup"><span data-stu-id="ffa79-174">This section describes the causes and solutions for specific symptoms or error messages that occur during a connection.</span></span>

### <a name="start-must-be-called-before-data-can-be-sent-error"></a><span data-ttu-id="ffa79-175">"必须先调用开始才能发送数据"错误</span><span class="sxs-lookup"><span data-stu-id="ffa79-175">"Start must be called before data can be sent" error</span></span>

<span data-ttu-id="ffa79-176">如果代码在连接启动之前引用 SignalR 对象，则通常可以看到此错误。</span><span class="sxs-lookup"><span data-stu-id="ffa79-176">This error is commonly seen if code references SignalR objects before the connection is started.</span></span> <span data-ttu-id="ffa79-177">必须在连接完成后添加处理程序的布线等调用服务器上定义的调用方法。</span><span class="sxs-lookup"><span data-stu-id="ffa79-177">The wireup for handlers and the like that will call methods defined on the server must be added after the connection completes.</span></span> <span data-ttu-id="ffa79-178">请注意，调用`Start`是异步的，因此在调用完成之前可以执行调用后的代码。</span><span class="sxs-lookup"><span data-stu-id="ffa79-178">Note that the call to `Start` is asynchronous, so code after the call may be executed before it completes.</span></span> <span data-ttu-id="ffa79-179">在连接完全启动后添加处理程序的最佳方法是将它们放入回调函数中，该函数作为参数传递给 start 方法：</span><span class="sxs-lookup"><span data-stu-id="ffa79-179">The best way to add handlers after a connection starts completely is to put them into a callback function that is passed as a parameter to the start method:</span></span>

<span data-ttu-id="ffa79-180">**正确添加引用 SignalR 对象的事件处理程序的 JavaScript 客户端代码**</span><span class="sxs-lookup"><span data-stu-id="ffa79-180">**JavaScript client code that correctly adds event handlers that reference SignalR objects**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample10.js?highlight=1)]

<span data-ttu-id="ffa79-181">如果连接在仍在引用 SignalR 对象时停止，也会看到此错误。</span><span class="sxs-lookup"><span data-stu-id="ffa79-181">This error will also be seen if a connection stops while SignalR objects are still being referenced.</span></span>

### <a name="301-moved-permanently-or-302-moved-temporarily-error"></a><span data-ttu-id="ffa79-182">"301 永久移动"或"302 临时移动"错误</span><span class="sxs-lookup"><span data-stu-id="ffa79-182">"301 Moved Permanently" or "302 Moved Temporarily" error</span></span>

<span data-ttu-id="ffa79-183">如果项目包含名为 SignalR 的文件夹，则可能会看到此错误，这将干扰自动创建的代理。</span><span class="sxs-lookup"><span data-stu-id="ffa79-183">This error may be seen if the project contains a folder called SignalR, which will interfere with the automatically-created proxy.</span></span> <span data-ttu-id="ffa79-184">为了避免此错误，请勿使用应用程序中调用`SignalR`的文件夹，或关闭自动代理生成。</span><span class="sxs-lookup"><span data-stu-id="ffa79-184">To avoid this error, do not use a folder called `SignalR` in your application, or turn automatic proxy generation off.</span></span> <span data-ttu-id="ffa79-185">有关详细信息[，请参阅生成的代理及其为您做什么](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy)。</span><span class="sxs-lookup"><span data-stu-id="ffa79-185">See [The Generated Proxy and what it does for you](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy) for more details.</span></span>

### <a name="403-forbidden-error-in-net-or-silverlight-client"></a><span data-ttu-id="ffa79-186">.NET 或银光客户端中的"403 禁止"错误</span><span class="sxs-lookup"><span data-stu-id="ffa79-186">"403 Forbidden" error in .NET or Silverlight client</span></span>

<span data-ttu-id="ffa79-187">此错误可能发生在跨域环境中，其中跨域通信未正确启用。</span><span class="sxs-lookup"><span data-stu-id="ffa79-187">This error may occur in cross-domain environments where cross-domain communication is not properly enabled.</span></span> <span data-ttu-id="ffa79-188">有关如何启用跨域通信的信息，请参阅[如何建立跨域连接](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)。</span><span class="sxs-lookup"><span data-stu-id="ffa79-188">For information on how to enable cross-domain communication, see [How to establish a cross-domain connection](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).</span></span> <span data-ttu-id="ffa79-189">要在 Silverlight 客户端中建立跨域连接，请参阅[来自 Silverlight 客户端的跨域连接](../guide-to-the-api/hubs-api-guide-net-client.md#slcrossdomain)。</span><span class="sxs-lookup"><span data-stu-id="ffa79-189">To establish a cross-domain connection in a Silverlight client, see [Cross-domain connections from Silverlight clients](../guide-to-the-api/hubs-api-guide-net-client.md#slcrossdomain).</span></span>

### <a name="404-not-found-error"></a><span data-ttu-id="ffa79-190">"404 未找到"错误</span><span class="sxs-lookup"><span data-stu-id="ffa79-190">"404 Not Found" error</span></span>

<span data-ttu-id="ffa79-191">此问题有多种原因。</span><span class="sxs-lookup"><span data-stu-id="ffa79-191">There are several causes for this issue.</span></span> <span data-ttu-id="ffa79-192">验证以下所有情况：</span><span class="sxs-lookup"><span data-stu-id="ffa79-192">Verify all of the following:</span></span>

- <span data-ttu-id="ffa79-193">**中心代理地址引用格式不正确：** 如果对生成的中心代理地址的引用格式不正确，则通常可以看到此错误。</span><span class="sxs-lookup"><span data-stu-id="ffa79-193">**Hub proxy address reference not formatted correctly:** This error is commonly seen if the reference to the generated hub proxy address is not formatted correctly.</span></span> <span data-ttu-id="ffa79-194">验证对中心地址的引用是否正确。</span><span class="sxs-lookup"><span data-stu-id="ffa79-194">Verify that the reference to the hub address is made properly.</span></span> <span data-ttu-id="ffa79-195">有关详细信息[，请参阅如何引用动态生成的代理](../guide-to-the-api/hubs-api-guide-javascript-client.md#dynamicproxy)。</span><span class="sxs-lookup"><span data-stu-id="ffa79-195">See [How to reference the dynamically generated proxy](../guide-to-the-api/hubs-api-guide-javascript-client.md#dynamicproxy) for details.</span></span>
- <span data-ttu-id="ffa79-196">**在添加中心路由之前向应用程序添加路由：** 如果应用程序使用其他路由，请验证添加的第一个路由是否调用`MapHubs`。</span><span class="sxs-lookup"><span data-stu-id="ffa79-196">**Adding routes to application before adding the hub route:** If your application uses other routes, verify that the first route added is the call to `MapHubs`.</span></span>

### <a name="500-internal-server-error"></a><span data-ttu-id="ffa79-197">"500 内部服务器错误"</span><span class="sxs-lookup"><span data-stu-id="ffa79-197">"500 Internal Server Error"</span></span>

<span data-ttu-id="ffa79-198">这是一个非常通用的错误，可能有各种各样的原因。</span><span class="sxs-lookup"><span data-stu-id="ffa79-198">This is a very generic error that could have a wide variety of causes.</span></span> <span data-ttu-id="ffa79-199">错误的详细信息应出现在服务器的事件日志中，或者可以通过调试服务器找到。</span><span class="sxs-lookup"><span data-stu-id="ffa79-199">The details of the error should appear in the server's event log, or can be found through debugging the server.</span></span> <span data-ttu-id="ffa79-200">通过在服务器上打开详细的错误，可以获得更详细的错误信息。</span><span class="sxs-lookup"><span data-stu-id="ffa79-200">More detailed error information may be obtained by turning on detailed errors on the server.</span></span> <span data-ttu-id="ffa79-201">有关详细信息，请参阅如何处理[Hub 类中的错误](../guide-to-the-api/hubs-api-guide-server.md#handleErrors)。</span><span class="sxs-lookup"><span data-stu-id="ffa79-201">For more information, see [How to handle errors in the Hub class](../guide-to-the-api/hubs-api-guide-server.md#handleErrors).</span></span>

### <a name="typeerror-lthubtypegt-is-undefined-error"></a><span data-ttu-id="ffa79-202">"类型错误：&lt;中心类型&gt;未定义"错误</span><span class="sxs-lookup"><span data-stu-id="ffa79-202">"TypeError: &lt;hubType&gt; is undefined" error</span></span>

<span data-ttu-id="ffa79-203">如果调用`MapHubs`不正确，将导致此错误。</span><span class="sxs-lookup"><span data-stu-id="ffa79-203">This error will result if the call to `MapHubs` is not made properly.</span></span> <span data-ttu-id="ffa79-204">有关详细信息[，请参阅如何注册 SignalR 路由和配置 SignalR 选项](../guide-to-the-api/hubs-api-guide-server.md#route)。</span><span class="sxs-lookup"><span data-stu-id="ffa79-204">See [How to register the SignalR route and configure SignalR options](../guide-to-the-api/hubs-api-guide-server.md#route) for more information.</span></span>

### <a name="jsonserializationexception-was-unhandled-by-user-code"></a><span data-ttu-id="ffa79-205">用户代码未处理 Json 序列化异常</span><span class="sxs-lookup"><span data-stu-id="ffa79-205">JsonSerializationException was unhandled by user code</span></span>

<span data-ttu-id="ffa79-206">验证发送到方法的参数是否不包括不可序列化的类型（如文件句柄或数据库连接）。</span><span class="sxs-lookup"><span data-stu-id="ffa79-206">Verify that the parameters you send to your methods do not include non-serializable types (like file handles or database connections).</span></span> <span data-ttu-id="ffa79-207">如果需要在不希望发送到客户端的服务器端对象上使用成员（出于安全性或序列化原因），请使用 该`JSONIgnore`属性。</span><span class="sxs-lookup"><span data-stu-id="ffa79-207">If you need to use members on a server-side object that you don't want to be sent to the client (either for security or for reasons of serialization), use the `JSONIgnore` attribute.</span></span>

### <a name="protocol-error-unknown-transport-error"></a><span data-ttu-id="ffa79-208">"协议错误：未知传输"错误</span><span class="sxs-lookup"><span data-stu-id="ffa79-208">"Protocol error: Unknown transport" error</span></span>

<span data-ttu-id="ffa79-209">如果客户端不支持 SignalR 使用的传输，则可能发生此错误。</span><span class="sxs-lookup"><span data-stu-id="ffa79-209">This error may occur if the client does not support the transports that SignalR uses.</span></span> <span data-ttu-id="ffa79-210">有关哪些浏览器可与 SignalR 一起使用的信息，请参阅[传输和回退](../getting-started/introduction-to-signalr.md#transports)。</span><span class="sxs-lookup"><span data-stu-id="ffa79-210">See [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports) for information on which browsers can be used with SignalR.</span></span>

### <a name="javascript-hub-proxy-generation-has-been-disabled"></a><span data-ttu-id="ffa79-211">"JavaScript 中心代理生成已被禁用。</span><span class="sxs-lookup"><span data-stu-id="ffa79-211">"JavaScript Hub proxy generation has been disabled."</span></span>

<span data-ttu-id="ffa79-212">如果`DisableJavaScriptProxies`设置时将发生此错误，同时还包括对 动态生成的代理的`signalr/hubs`引用。</span><span class="sxs-lookup"><span data-stu-id="ffa79-212">This error will occur if `DisableJavaScriptProxies` is set while also including a reference to the dynamically generated proxy at `signalr/hubs`.</span></span> <span data-ttu-id="ffa79-213">有关手动创建代理的详细信息，请参阅[生成的代理及其为您做什么](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy)。</span><span class="sxs-lookup"><span data-stu-id="ffa79-213">For more information on creating the proxy manually, see [The generated proxy and what it does for you](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy).</span></span>

### <a name="the-connection-id-is-in-the-incorrect-format-or-the-user-identity-cannot-change-during-an-active-signalr-connection-error"></a><span data-ttu-id="ffa79-214">"连接 ID 格式不正确"或"用户身份在活动 SignalR 连接期间无法更改"错误</span><span class="sxs-lookup"><span data-stu-id="ffa79-214">"The connection ID is in the incorrect format" or "The user identity cannot change during an active SignalR connection" error</span></span>

<span data-ttu-id="ffa79-215">如果正在使用身份验证，并且客户端在停止连接之前注销，则可能会看到此错误。</span><span class="sxs-lookup"><span data-stu-id="ffa79-215">This error may be seen if authentication is being used, and the client is logged out before the connection is stopped.</span></span> <span data-ttu-id="ffa79-216">解决方案是在注销客户端之前停止 SignalR 连接。</span><span class="sxs-lookup"><span data-stu-id="ffa79-216">The solution is to stop the SignalR connection before logging the client out.</span></span>

### <a name="uncaught-error-signalr-jquery-not-found-please-ensure-jquery-is-referenced-before-the-signalrjs-file-error"></a><span data-ttu-id="ffa79-217">"未捕获错误：信号R：找不到 jQuery。</span><span class="sxs-lookup"><span data-stu-id="ffa79-217">"Uncaught Error: SignalR: jQuery not found.</span></span> <span data-ttu-id="ffa79-218">请确保在 SignalR.js 文件"错误之前引用 jQuery</span><span class="sxs-lookup"><span data-stu-id="ffa79-218">Please ensure jQuery is referenced before the SignalR.js file" error</span></span>

<span data-ttu-id="ffa79-219">SignalR JavaScript 客户端需要 jQuery 才能运行。</span><span class="sxs-lookup"><span data-stu-id="ffa79-219">The SignalR JavaScript client requires jQuery to run.</span></span> <span data-ttu-id="ffa79-220">验证对 jQuery 的引用是否正确，使用的路径是否有效，以及对 jQuery 的引用是否位于对 SignalR 的引用之前。</span><span class="sxs-lookup"><span data-stu-id="ffa79-220">Verify that your reference to jQuery is correct, that the path used is valid, and that the reference to jQuery is before the reference to SignalR.</span></span>

### <a name="uncaught-typeerror-cannot-read-property-ltpropertygt-of-undefined-error"></a><span data-ttu-id="ffa79-221">"未捕获的类型错误：无法读取属性'&lt;属性&gt;'未定义"错误</span><span class="sxs-lookup"><span data-stu-id="ffa79-221">"Uncaught TypeError: Cannot read property '&lt;property&gt;' of undefined" error</span></span>

<span data-ttu-id="ffa79-222">此错误导致没有正确引用 jQuery 或中心代理。</span><span class="sxs-lookup"><span data-stu-id="ffa79-222">This error results from not having jQuery or the hubs proxy referenced properly.</span></span> <span data-ttu-id="ffa79-223">验证对 jQuery 和集线器代理的引用是否正确，使用的路径是否有效，以及对 jQuery 的引用是否位于对集线器代理的引用之前。</span><span class="sxs-lookup"><span data-stu-id="ffa79-223">Verify that your reference to jQuery and the hubs proxy is correct, that the path used is valid, and that the reference to jQuery is before the reference to the hubs proxy.</span></span> <span data-ttu-id="ffa79-224">对集线器代理的默认引用应如下所示：</span><span class="sxs-lookup"><span data-stu-id="ffa79-224">The default reference to the hubs proxy should look like the following:</span></span>

<span data-ttu-id="ffa79-225">**正确引用中心代理的 HTML 客户端代码**</span><span class="sxs-lookup"><span data-stu-id="ffa79-225">**HTML client-side code that correctly references the Hubs proxy**</span></span>

[!code-html[Main](troubleshooting/samples/sample11.html)]

### <a name="runtimebinderexception-was-unhandled-by-user-code-error"></a><span data-ttu-id="ffa79-226">"运行时Binder异常未由用户代码处理"错误</span><span class="sxs-lookup"><span data-stu-id="ffa79-226">"RuntimeBinderException was unhandled by user code" error</span></span>

<span data-ttu-id="ffa79-227">当使用不正确的重载`Hub.On`时，可能会出现此错误。</span><span class="sxs-lookup"><span data-stu-id="ffa79-227">This error may occur when the incorrect overload of `Hub.On` is used.</span></span> <span data-ttu-id="ffa79-228">如果方法具有返回值，则必须将返回类型指定为泛型类型参数：</span><span class="sxs-lookup"><span data-stu-id="ffa79-228">If the method has a return value, the return type must be specified as a generic type parameter:</span></span>

<span data-ttu-id="ffa79-229">**在客户端上定义的方法（没有生成的代理）**</span><span class="sxs-lookup"><span data-stu-id="ffa79-229">**Method defined on the client (without generated proxy)**</span></span>

[!code-html[Main](troubleshooting/samples/sample12.html?highlight=1)]

### <a name="connection-id-is-inconsistent-or-connection-breaks-between-page-loads"></a><span data-ttu-id="ffa79-230">连接 ID 不一致或页面加载之间的连接中断</span><span class="sxs-lookup"><span data-stu-id="ffa79-230">Connection ID is inconsistent or connection breaks between page loads</span></span>

<span data-ttu-id="ffa79-231">这是设计的行为。</span><span class="sxs-lookup"><span data-stu-id="ffa79-231">This behavior is by design.</span></span> <span data-ttu-id="ffa79-232">由于中心对象托管在页面对象中，因此在页面刷新时将销毁中心。</span><span class="sxs-lookup"><span data-stu-id="ffa79-232">Since the hub object is hosted in the page object, the hub is destroyed when the page refreshes.</span></span> <span data-ttu-id="ffa79-233">多页应用程序需要维护用户和连接指示之间的关联，以便它们在页面加载之间保持一致。</span><span class="sxs-lookup"><span data-stu-id="ffa79-233">A multi-page application needs to maintain the association between users and connection IDs so that they will be consistent between page loads.</span></span> <span data-ttu-id="ffa79-234">连接指示可以存储在`ConcurrentDictionary`对象或数据库中的服务器上。</span><span class="sxs-lookup"><span data-stu-id="ffa79-234">The connection IDs can be stored on the server in either a `ConcurrentDictionary` object or a database.</span></span>

### <a name="value-cannot-be-null-error"></a><span data-ttu-id="ffa79-235">"值不能为空"错误</span><span class="sxs-lookup"><span data-stu-id="ffa79-235">"Value cannot be null" error</span></span>

<span data-ttu-id="ffa79-236">当前不支持具有可选参数的服务器端方法;如果省略可选参数，该方法将失败。</span><span class="sxs-lookup"><span data-stu-id="ffa79-236">Server-side methods with optional parameters are not currently supported; if the optional parameter is omitted, the method will fail.</span></span> <span data-ttu-id="ffa79-237">有关详细信息，请参阅[可选参数](https://github.com/SignalR/SignalR/issues/324)。</span><span class="sxs-lookup"><span data-stu-id="ffa79-237">For more information, see [Optional Parameters](https://github.com/SignalR/SignalR/issues/324).</span></span>

### <a name="firefox-cant-establish-a-connection-to-the-server-at-ltaddressgt-error-in-firebug"></a><span data-ttu-id="ffa79-238">"Firefox 无法在&lt;地址&gt;建立与服务器的连接"Firebug 中的错误</span><span class="sxs-lookup"><span data-stu-id="ffa79-238">"Firefox can't establish a connection to the server at &lt;address&gt;" error in Firebug</span></span>

<span data-ttu-id="ffa79-239">如果 WebSocket 传输协商失败，并且使用另一个传输，可以在 Firebug 中看到此错误消息。</span><span class="sxs-lookup"><span data-stu-id="ffa79-239">This error message can be seen in Firebug if negotiation of the WebSocket transport fails and another transport is used instead.</span></span> <span data-ttu-id="ffa79-240">这是设计的行为。</span><span class="sxs-lookup"><span data-stu-id="ffa79-240">This behavior is by design.</span></span>

### <a name="the-remote-certificate-is-invalid-according-to-the-validation-procedure-error-in-net-client-application"></a><span data-ttu-id="ffa79-241">.NET 客户端应用程序中的"远程证书根据验证过程无效"错误</span><span class="sxs-lookup"><span data-stu-id="ffa79-241">"The remote certificate is invalid according to the validation procedure" error in .NET client application</span></span>

<span data-ttu-id="ffa79-242">如果服务器需要自定义客户端证书，则可以在发出请求之前向连接添加 x509 证书。</span><span class="sxs-lookup"><span data-stu-id="ffa79-242">If your server requires custom client certificates, then you can add an x509certificate to the connection before the request is made.</span></span> <span data-ttu-id="ffa79-243">使用 将证书添加到连接中`Connection.AddClientCertificate`。</span><span class="sxs-lookup"><span data-stu-id="ffa79-243">Add the certificate to the connection using `Connection.AddClientCertificate`.</span></span>

### <a name="connection-drops-after-authentication-times-out"></a><span data-ttu-id="ffa79-244">身份验证超时后连接断开</span><span class="sxs-lookup"><span data-stu-id="ffa79-244">Connection drops after authentication times out</span></span>

<span data-ttu-id="ffa79-245">这是设计的行为。</span><span class="sxs-lookup"><span data-stu-id="ffa79-245">This behavior is by design.</span></span> <span data-ttu-id="ffa79-246">当连接处于活动状态时，无法修改身份验证凭据;要刷新凭据，必须停止并重新启动连接。</span><span class="sxs-lookup"><span data-stu-id="ffa79-246">Authentication credentials cannot be modified while a connection is active; to refresh credentials, the connection must be stopped and restarted.</span></span>

### <a name="onconnected-gets-called-twice-when-using-jquery-mobile"></a><span data-ttu-id="ffa79-247">使用 jQuery 移动时，OnConnected 被调用两次</span><span class="sxs-lookup"><span data-stu-id="ffa79-247">OnConnected gets called twice when using jQuery Mobile</span></span>

<span data-ttu-id="ffa79-248">jQuery Mobile`initializePage`的功能强制重新执行每个页面中的脚本，从而创建第二个连接。</span><span class="sxs-lookup"><span data-stu-id="ffa79-248">jQuery Mobile's `initializePage` function forces the scripts in each page to be re-executed, thus creating a second connection.</span></span> <span data-ttu-id="ffa79-249">此问题的解决方案包括：</span><span class="sxs-lookup"><span data-stu-id="ffa79-249">Solutions for this issue include:</span></span>

- <span data-ttu-id="ffa79-250">在 JavaScript 文件之前包括对 jQuery 移动的引用。</span><span class="sxs-lookup"><span data-stu-id="ffa79-250">Include the reference to jQuery Mobile before your JavaScript file.</span></span>
- <span data-ttu-id="ffa79-251">通过设置`initializePage``$.mobile.autoInitializePage = false`禁用 函数。</span><span class="sxs-lookup"><span data-stu-id="ffa79-251">Disable the `initializePage` function by setting `$.mobile.autoInitializePage = false`.</span></span>
- <span data-ttu-id="ffa79-252">在开始连接之前，等待页面完成初始化。</span><span class="sxs-lookup"><span data-stu-id="ffa79-252">Wait for the page to finish initializing before starting the connection.</span></span>

### <a name="messages-are-delayed-in-silverlight-applications-using-server-sent-events"></a><span data-ttu-id="ffa79-253">使用服务器发送事件在 Silverlight 应用程序中延迟消息</span><span class="sxs-lookup"><span data-stu-id="ffa79-253">Messages are delayed in Silverlight applications using Server Sent Events</span></span>

<span data-ttu-id="ffa79-254">在 Silverlight 上使用服务器发送的事件时，消息会延迟。</span><span class="sxs-lookup"><span data-stu-id="ffa79-254">Messages are delayed when using server sent events on Silverlight.</span></span> <span data-ttu-id="ffa79-255">要强制使用长轮询，在启动连接时使用以下内容：</span><span class="sxs-lookup"><span data-stu-id="ffa79-255">To force long polling to be used instead, use the following when starting the connection:</span></span>

[!code-css[Main](troubleshooting/samples/sample13.css)]

### <a name="permission-denied-using-forever-frame-protocol"></a><span data-ttu-id="ffa79-256">使用永久帧协议"拒绝权限"</span><span class="sxs-lookup"><span data-stu-id="ffa79-256">"Permission Denied" using Forever Frame protocol</span></span>

<span data-ttu-id="ffa79-257">这是一个已知的问题，[此处](https://github.com/SignalR/SignalR/issues/1963)描述。</span><span class="sxs-lookup"><span data-stu-id="ffa79-257">This is a known issue, described [here](https://github.com/SignalR/SignalR/issues/1963).</span></span> <span data-ttu-id="ffa79-258">可以使用最新的 JQuery 库看到此症状;解决方法是将应用程序降级为 JQuery 1.8.2。</span><span class="sxs-lookup"><span data-stu-id="ffa79-258">This symptom may be seen using the latest JQuery library; the workaround is to downgrade your application to JQuery 1.8.2.</span></span>

<a id="server"></a>

## <a name="compilation-and-server-side-errors"></a><span data-ttu-id="ffa79-259">编译和服务器端错误</span><span class="sxs-lookup"><span data-stu-id="ffa79-259">Compilation and server-side errors</span></span>

 <span data-ttu-id="ffa79-260">以下部分包含编译器和服务器端运行时错误的可能解决方案。</span><span class="sxs-lookup"><span data-stu-id="ffa79-260">The following section contains possible solutions to compiler and server-side runtime errors.</span></span> 

### <a name="reference-to-hub-instance-is-null"></a><span data-ttu-id="ffa79-261">对中心实例的引用为空</span><span class="sxs-lookup"><span data-stu-id="ffa79-261">Reference to Hub instance is null</span></span>

<span data-ttu-id="ffa79-262">由于为每个连接创建了一个中心实例，因此无法自己在代码中创建集线器的实例。</span><span class="sxs-lookup"><span data-stu-id="ffa79-262">Since a hub instance is created for each connection, you can't create an instance of a hub in your code yourself.</span></span> <span data-ttu-id="ffa79-263">要从中心外部调用方法，请参阅[如何调用客户端方法并从中心类外部管理组](../guide-to-the-api/hubs-api-guide-server.md#callfromoutsidehub)，了解如何获取对中心上下文的引用。</span><span class="sxs-lookup"><span data-stu-id="ffa79-263">To call methods on a hub from outside the hub itself, see [How to call client methods and manage groups from outside the Hub class](../guide-to-the-api/hubs-api-guide-server.md#callfromoutsidehub) for how to obtain a reference to the hub context.</span></span>

### <a name="httpcontextcurrentsession-is-null"></a><span data-ttu-id="ffa79-264">HTTPContext.当前.会话为空</span><span class="sxs-lookup"><span data-stu-id="ffa79-264">HTTPContext.Current.Session is null</span></span>

<span data-ttu-id="ffa79-265">这是设计的行为。</span><span class="sxs-lookup"><span data-stu-id="ffa79-265">This behavior is by design.</span></span> <span data-ttu-id="ffa79-266">SignalR 不支持ASP.NET会话状态，因为启用会话状态将中断双工消息。</span><span class="sxs-lookup"><span data-stu-id="ffa79-266">SignalR does not support the ASP.NET session state, since enabling the session state would break duplex messaging.</span></span>

### <a name="no-suitable-method-to-override"></a><span data-ttu-id="ffa79-267">没有合适的方法可以重写</span><span class="sxs-lookup"><span data-stu-id="ffa79-267">No suitable method to override</span></span>

<span data-ttu-id="ffa79-268">如果您使用的是来自旧文档或博客的代码，则可能会看到此错误。</span><span class="sxs-lookup"><span data-stu-id="ffa79-268">You may see this error if you are using code from older documentation or blogs.</span></span> <span data-ttu-id="ffa79-269">验证您没有引用已更改或弃用的方法的名称（如`OnConnectedAsync`）。</span><span class="sxs-lookup"><span data-stu-id="ffa79-269">Verify that you are not referencing names of methods that have been changed or deprecated (like `OnConnectedAsync`).</span></span>

### <a name="hostcontextextensionswebsocketserverurl-is-null"></a><span data-ttu-id="ffa79-270">主机上下文扩展.WebSocket服务器Url为空</span><span class="sxs-lookup"><span data-stu-id="ffa79-270">HostContextExtensions.WebSocketServerUrl is null</span></span>

<span data-ttu-id="ffa79-271">这是设计的行为。</span><span class="sxs-lookup"><span data-stu-id="ffa79-271">This behavior is by design.</span></span> <span data-ttu-id="ffa79-272">此成员已弃用，不应使用。</span><span class="sxs-lookup"><span data-stu-id="ffa79-272">This member is deprecated and should not be used.</span></span>

### <a name="a-route-named-signalrhubs-is-already-in-the-route-collection-error"></a><span data-ttu-id="ffa79-273">"名为"Signalr.hubs"的路由已在路由集合中"错误</span><span class="sxs-lookup"><span data-stu-id="ffa79-273">"A route named 'signalr.hubs' is already in the route collection" error</span></span>

<span data-ttu-id="ffa79-274">如果`MapHubs`应用程序调用了两次，则将看到此错误。</span><span class="sxs-lookup"><span data-stu-id="ffa79-274">This error will be seen if `MapHubs` is called twice by your application.</span></span> <span data-ttu-id="ffa79-275">一些示例应用程序`MapHubs`直接调用全局应用程序文件中;其他人在包装类中进行调用。</span><span class="sxs-lookup"><span data-stu-id="ffa79-275">Some example applications call `MapHubs` directly in the global application file; others make the call in a wrapper class.</span></span> <span data-ttu-id="ffa79-276">确保应用程序不同时执行这两种操作。</span><span class="sxs-lookup"><span data-stu-id="ffa79-276">Ensure that your application does not do both.</span></span>

<a id="vs"></a>

## <a name="visual-studio-issues"></a><span data-ttu-id="ffa79-277">视觉工作室问题</span><span class="sxs-lookup"><span data-stu-id="ffa79-277">Visual Studio issues</span></span>

<span data-ttu-id="ffa79-278">本节介绍视觉工作室中遇到的问题。</span><span class="sxs-lookup"><span data-stu-id="ffa79-278">This section describes issues encountered in Visual Studio.</span></span>

### <a name="script-documents-node-does-not-appear-in-solution-explorer"></a><span data-ttu-id="ffa79-279">脚本文档节点未显示在解决方案资源管理器中</span><span class="sxs-lookup"><span data-stu-id="ffa79-279">Script Documents node does not appear in Solution Explorer</span></span>

<span data-ttu-id="ffa79-280">我们的一些教程将引导您到解决方案资源管理器中的"脚本文档"节点进行调试。</span><span class="sxs-lookup"><span data-stu-id="ffa79-280">Some of our tutorials direct you to the "Script Documents" node in Solution Explorer while debugging.</span></span> <span data-ttu-id="ffa79-281">此节点由 JavaScript 调试器生成，仅在 Internet 资源管理器中调试浏览器客户端时出现;如果使用 Chrome 或 Firefox，将不会显示该节点。</span><span class="sxs-lookup"><span data-stu-id="ffa79-281">This node is produced by the JavaScript debugger, and will only appear while debugging browser clients in Internet Explorer; the node will not appear if Chrome or Firefox are used.</span></span> <span data-ttu-id="ffa79-282">如果运行了另一个客户端调试器（如 Silverlight 调试器），JavaScript 调试器也不会运行。</span><span class="sxs-lookup"><span data-stu-id="ffa79-282">The JavaScript debugger will also not run if another client debugger is running, such as the Silverlight debugger.</span></span>

### <a name="signalr-does-not-work-on-visual-studio-2008-or-earlier"></a><span data-ttu-id="ffa79-283">信号R在视觉工作室 2008 或更早版本上不起作用</span><span class="sxs-lookup"><span data-stu-id="ffa79-283">SignalR does not work on Visual Studio 2008 or earlier</span></span>

<span data-ttu-id="ffa79-284">这是设计的行为。</span><span class="sxs-lookup"><span data-stu-id="ffa79-284">This behavior is by design.</span></span> <span data-ttu-id="ffa79-285">信号R需要 .NET 框架 4 或更高版本;这要求在 Visual Studio 2010 或更高版本中开发 SignalR 应用程序。</span><span class="sxs-lookup"><span data-stu-id="ffa79-285">SignalR requires .NET Framework 4 or later; this requires that SignalR applications be developed in Visual Studio 2010 or later.</span></span>

<a id="iis"></a>

## <a name="iis-issues"></a><span data-ttu-id="ffa79-286">IIS 问题</span><span class="sxs-lookup"><span data-stu-id="ffa79-286">IIS issues</span></span>

<span data-ttu-id="ffa79-287">本节包含互联网信息服务的问题。</span><span class="sxs-lookup"><span data-stu-id="ffa79-287">This section contains issues with Internet Information Services.</span></span>

### <a name="web-site-crashes-after-maphubs-call"></a><span data-ttu-id="ffa79-288">地图中心调用后网站崩溃</span><span class="sxs-lookup"><span data-stu-id="ffa79-288">Web site crashes after MapHubs call</span></span>

<span data-ttu-id="ffa79-289">此问题已在最新版本的 SignalR 中修复。</span><span class="sxs-lookup"><span data-stu-id="ffa79-289">This issue has been fixed in the latest version of SignalR.</span></span> <span data-ttu-id="ffa79-290">使用 NuGet 更新安装，验证您使用的是最新版本的 SignalR。</span><span class="sxs-lookup"><span data-stu-id="ffa79-290">Verify that you are using the latest released version of SignalR by updating your installation using NuGet.</span></span>

<a id="azure"></a>

## <a name="azure-issues"></a><span data-ttu-id="ffa79-291">Azure 问题</span><span class="sxs-lookup"><span data-stu-id="ffa79-291">Azure issues</span></span>

<span data-ttu-id="ffa79-292">本节包含 Microsoft Azure 的问题。</span><span class="sxs-lookup"><span data-stu-id="ffa79-292">This section contains issues with Microsoft Azure.</span></span>

### <a name="messages-are-not-received-through-the-azure-backplane-after-altering-topic-names"></a><span data-ttu-id="ffa79-293">更改主题名称后，不会通过 Azure 背板接收消息</span><span class="sxs-lookup"><span data-stu-id="ffa79-293">Messages are not received through the Azure backplane after altering topic names</span></span>

<span data-ttu-id="ffa79-294">Azure 背板使用的主题不用于用户配置。</span><span class="sxs-lookup"><span data-stu-id="ffa79-294">The topics used by the Azure backplane are not intended to be user-configurable.</span></span>

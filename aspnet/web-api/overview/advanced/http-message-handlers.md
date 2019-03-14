---
uid: web-api/overview/advanced/http-message-handlers
title: ASP.NET Web API 中的 HTTP 消息处理程序 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 02/13/2012
ms.assetid: 9002018b-3aa3-4358-bb1c-fbb5bc751d01
msc.legacyurl: /web-api/overview/advanced/http-message-handlers
msc.type: authoredcontent
ms.openlocfilehash: 0b0d7b4c543dc4e597c6c472083898f3a8095a83
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57043204"
---
<a name="http-message-handlers-in-aspnet-web-api"></a><span data-ttu-id="b275b-102">ASP.NET Web API 中的 HTTP 消息处理程序</span><span class="sxs-lookup"><span data-stu-id="b275b-102">HTTP Message Handlers in ASP.NET Web API</span></span>
====================
<span data-ttu-id="b275b-103">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="b275b-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="b275b-104">一个*消息处理程序*是收到 HTTP 请求并返回 HTTP 响应的类。</span><span class="sxs-lookup"><span data-stu-id="b275b-104">A *message handler* is a class that receives an HTTP request and returns an HTTP response.</span></span> <span data-ttu-id="b275b-105">消息处理程序派生自抽象**HttpMessageHandler**类。</span><span class="sxs-lookup"><span data-stu-id="b275b-105">Message handlers derive from the abstract **HttpMessageHandler** class.</span></span>

<span data-ttu-id="b275b-106">通常情况下，消息处理程序的一系列链接在一起。</span><span class="sxs-lookup"><span data-stu-id="b275b-106">Typically, a series of message handlers are chained together.</span></span> <span data-ttu-id="b275b-107">第一个处理程序收到 HTTP 请求、 执行某些处理，并提供请求下一个处理程序。</span><span class="sxs-lookup"><span data-stu-id="b275b-107">The first handler receives an HTTP request, does some processing, and gives the request to the next handler.</span></span> <span data-ttu-id="b275b-108">在某些时候，响应创建，并将返回链。</span><span class="sxs-lookup"><span data-stu-id="b275b-108">At some point, the response is created and goes back up the chain.</span></span> <span data-ttu-id="b275b-109">此模式称为*委派*处理程序。</span><span class="sxs-lookup"><span data-stu-id="b275b-109">This pattern is called a *delegating* handler.</span></span>

![](http-message-handlers/_static/image1.png)

## <a name="server-side-message-handlers"></a><span data-ttu-id="b275b-110">服务器端消息处理程序</span><span class="sxs-lookup"><span data-stu-id="b275b-110">Server-Side Message Handlers</span></span>

<span data-ttu-id="b275b-111">在服务器端 Web API 管道使用一些内置消息处理程序：</span><span class="sxs-lookup"><span data-stu-id="b275b-111">On the server side, the Web API pipeline uses some built-in message handlers:</span></span>

- <span data-ttu-id="b275b-112">**HttpServer**从主机获取该请求。</span><span class="sxs-lookup"><span data-stu-id="b275b-112">**HttpServer** gets the request from the host.</span></span>
- <span data-ttu-id="b275b-113">**HttpRoutingDispatcher**调度基于路由的请求。</span><span class="sxs-lookup"><span data-stu-id="b275b-113">**HttpRoutingDispatcher** dispatches the request based on the route.</span></span>
- <span data-ttu-id="b275b-114">**HttpControllerDispatcher**将请求发送到 Web API 控制器。</span><span class="sxs-lookup"><span data-stu-id="b275b-114">**HttpControllerDispatcher** sends the request to a Web API controller.</span></span>

<span data-ttu-id="b275b-115">您可以向管道添加自定义处理程序。</span><span class="sxs-lookup"><span data-stu-id="b275b-115">You can add custom handlers to the pipeline.</span></span> <span data-ttu-id="b275b-116">消息处理程序非常适用于在 HTTP 消息 （而非控制器操作） 的级别运行的横切关注点。</span><span class="sxs-lookup"><span data-stu-id="b275b-116">Message handlers are good for cross-cutting concerns that operate at the level of HTTP messages (rather than controller actions).</span></span> <span data-ttu-id="b275b-117">例如，消息处理程序可能：</span><span class="sxs-lookup"><span data-stu-id="b275b-117">For example, a message handler might:</span></span>

- <span data-ttu-id="b275b-118">读取或修改请求标头。</span><span class="sxs-lookup"><span data-stu-id="b275b-118">Read or modify request headers.</span></span>
- <span data-ttu-id="b275b-119">将响应标头添加到响应。</span><span class="sxs-lookup"><span data-stu-id="b275b-119">Add a response header to responses.</span></span>
- <span data-ttu-id="b275b-120">到达控制器之前，请验证的请求。</span><span class="sxs-lookup"><span data-stu-id="b275b-120">Validate requests before they reach the controller.</span></span>

<span data-ttu-id="b275b-121">此图显示了插入到管道的两个自定义处理程序：</span><span class="sxs-lookup"><span data-stu-id="b275b-121">This diagram shows two custom handlers inserted into the pipeline:</span></span>

![](http-message-handlers/_static/image2.png)

> [!NOTE]
> <span data-ttu-id="b275b-122">在客户端，HttpClient 还使用消息处理程序。</span><span class="sxs-lookup"><span data-stu-id="b275b-122">On the client side, HttpClient also uses message handlers.</span></span> <span data-ttu-id="b275b-123">有关详细信息，请参阅[HttpClient 消息处理程序](httpclient-message-handlers.md)。</span><span class="sxs-lookup"><span data-stu-id="b275b-123">For more information, see [HttpClient Message Handlers](httpclient-message-handlers.md).</span></span>


## <a name="custom-message-handlers"></a><span data-ttu-id="b275b-124">自定义消息处理程序</span><span class="sxs-lookup"><span data-stu-id="b275b-124">Custom Message Handlers</span></span>

<span data-ttu-id="b275b-125">若要编写自定义消息处理程序，从派生**System.Net.Http.DelegatingHandler**并重写**SendAsync**方法。</span><span class="sxs-lookup"><span data-stu-id="b275b-125">To write a custom message handler, derive from **System.Net.Http.DelegatingHandler** and override the **SendAsync** method.</span></span> <span data-ttu-id="b275b-126">此方法具有以下签名：</span><span class="sxs-lookup"><span data-stu-id="b275b-126">This method has the following signature:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample1.cs)]

<span data-ttu-id="b275b-127">该方法采用**HttpRequestMessage**作为输入，并以异步方式返回**HttpResponseMessage**。</span><span class="sxs-lookup"><span data-stu-id="b275b-127">The method takes an **HttpRequestMessage** as input and asynchronously returns an **HttpResponseMessage**.</span></span> <span data-ttu-id="b275b-128">典型实现执行以下任务：</span><span class="sxs-lookup"><span data-stu-id="b275b-128">A typical implementation does the following:</span></span>

1. <span data-ttu-id="b275b-129">处理请求消息。</span><span class="sxs-lookup"><span data-stu-id="b275b-129">Process the request message.</span></span>
2. <span data-ttu-id="b275b-130">调用`base.SendAsync`将请求发送到的内部处理程序。</span><span class="sxs-lookup"><span data-stu-id="b275b-130">Call `base.SendAsync` to send the request to the inner handler.</span></span>
3. <span data-ttu-id="b275b-131">内部处理程序返回响应消息。</span><span class="sxs-lookup"><span data-stu-id="b275b-131">The inner handler returns a response message.</span></span> <span data-ttu-id="b275b-132">（此步骤是异步的。）</span><span class="sxs-lookup"><span data-stu-id="b275b-132">(This step is asynchronous.)</span></span>
4. <span data-ttu-id="b275b-133">处理响应并将其返回给调用方。</span><span class="sxs-lookup"><span data-stu-id="b275b-133">Process the response and return it to the caller.</span></span>

<span data-ttu-id="b275b-134">下面是一个简单示例：</span><span class="sxs-lookup"><span data-stu-id="b275b-134">Here is a trivial example:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample2.cs)]

> [!NOTE]
> <span data-ttu-id="b275b-135">对调用`base.SendAsync`是异步的。</span><span class="sxs-lookup"><span data-stu-id="b275b-135">The call to `base.SendAsync` is asynchronous.</span></span> <span data-ttu-id="b275b-136">如果此调用后，该处理程序执行任何工作，使用**await**关键字，如所示。</span><span class="sxs-lookup"><span data-stu-id="b275b-136">If the handler does any work after this call, use the **await** keyword, as shown.</span></span>


<span data-ttu-id="b275b-137">一个委派处理程序可以跳过内部处理程序，并直接创建响应：</span><span class="sxs-lookup"><span data-stu-id="b275b-137">A delegating handler can also skip the inner handler and directly create the response:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample3.cs)]

<span data-ttu-id="b275b-138">如果委托处理程序将创建无需调用响应`base.SendAsync`，请求将跳过管道的其余部分。</span><span class="sxs-lookup"><span data-stu-id="b275b-138">If a delegating handler creates the response without calling `base.SendAsync`, the request skips the rest of the pipeline.</span></span> <span data-ttu-id="b275b-139">这可用于验证请求 （创建错误响应） 的处理程序。</span><span class="sxs-lookup"><span data-stu-id="b275b-139">This can be useful for a handler that validates the request (creating an error response).</span></span>

![](http-message-handlers/_static/image3.png)

## <a name="adding-a-handler-to-the-pipeline"></a><span data-ttu-id="b275b-140">向管道添加一个处理程序</span><span class="sxs-lookup"><span data-stu-id="b275b-140">Adding a Handler to the Pipeline</span></span>

<span data-ttu-id="b275b-141">若要在服务器端添加消息处理程序，请将添加到处理程序**HttpConfiguration.MessageHandlers**集合。</span><span class="sxs-lookup"><span data-stu-id="b275b-141">To add a message handler on the server side, add the handler to the **HttpConfiguration.MessageHandlers** collection.</span></span> <span data-ttu-id="b275b-142">如果您使用"ASP.NET MVC 4 Web 应用程序"模板创建项目，则可以执行此内部**WebApiConfig**类：</span><span class="sxs-lookup"><span data-stu-id="b275b-142">If you used the "ASP.NET MVC 4 Web Application" template to create the project, you can do this inside the **WebApiConfig** class:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample4.cs)]

<span data-ttu-id="b275b-143">消息处理程序调用中出现的相同顺序**MessageHandlers**集合。</span><span class="sxs-lookup"><span data-stu-id="b275b-143">Message handlers are called in the same order that they appear in **MessageHandlers** collection.</span></span> <span data-ttu-id="b275b-144">因为它们嵌套的在另一个方向传输时响应消息。</span><span class="sxs-lookup"><span data-stu-id="b275b-144">Because they are nested, the response message travels in the other direction.</span></span> <span data-ttu-id="b275b-145">也就是说，最后一个处理程序是获取响应消息的第一个。</span><span class="sxs-lookup"><span data-stu-id="b275b-145">That is, the last handler is the first to get the response message.</span></span>

<span data-ttu-id="b275b-146">请注意，不需要设置内部处理程序;Web API 框架会自动连接消息处理程序。</span><span class="sxs-lookup"><span data-stu-id="b275b-146">Notice that you don't need to set the inner handlers; the Web API framework automatically connects the message handlers.</span></span>

<span data-ttu-id="b275b-147">你是否[自我托管](../older-versions/self-host-a-web-api.md)，创建的实例**HttpSelfHostConfiguration**类，并添加到处理程序**MessageHandlers**集合。</span><span class="sxs-lookup"><span data-stu-id="b275b-147">If you are [self-hosting](../older-versions/self-host-a-web-api.md), create an instance of the **HttpSelfHostConfiguration** class and add the handlers to the **MessageHandlers** collection.</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample5.cs)]

<span data-ttu-id="b275b-148">现在让我们看看一些示例自定义消息处理程序。</span><span class="sxs-lookup"><span data-stu-id="b275b-148">Now let's look at some examples of custom message handlers.</span></span>

## <a name="example-x-http-method-override"></a><span data-ttu-id="b275b-149">示例:X-HTTP-Method-Override</span><span class="sxs-lookup"><span data-stu-id="b275b-149">Example: X-HTTP-Method-Override</span></span>

<span data-ttu-id="b275b-150">X HTTP 的方法重写为非标准 HTTP 标头。</span><span class="sxs-lookup"><span data-stu-id="b275b-150">X-HTTP-Method-Override is a non-standard HTTP header.</span></span> <span data-ttu-id="b275b-151">它专为不能发送特定 HTTP 请求类型，例如 PUT 或 DELETE 的客户端。</span><span class="sxs-lookup"><span data-stu-id="b275b-151">It is designed for clients that cannot send certain HTTP request types, such as PUT or DELETE.</span></span> <span data-ttu-id="b275b-152">相反，客户端发送 POST 请求，且 X HTTP 的方法重写标头设置为所需的方法。</span><span class="sxs-lookup"><span data-stu-id="b275b-152">Instead, the client sends a POST request and sets the X-HTTP-Method-Override header to the desired method.</span></span> <span data-ttu-id="b275b-153">例如：</span><span class="sxs-lookup"><span data-stu-id="b275b-153">For example:</span></span>

[!code-console[Main](http-message-handlers/samples/sample6.cmd)]

<span data-ttu-id="b275b-154">下面是添加了对 X HTTP 的方法重写支持的消息处理程序：</span><span class="sxs-lookup"><span data-stu-id="b275b-154">Here is a message handler that adds support for X-HTTP-Method-Override:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample7.cs)]

<span data-ttu-id="b275b-155">在中**SendAsync**方法，该处理程序检查请求消息是否是 POST 请求，以及它是否包含 X HTTP 的方法重写标头。</span><span class="sxs-lookup"><span data-stu-id="b275b-155">In the **SendAsync** method, the handler checks whether the request message is a POST request, and whether it contains the X-HTTP-Method-Override header.</span></span> <span data-ttu-id="b275b-156">如果是这样，它将验证标头值，然后修改请求方法。</span><span class="sxs-lookup"><span data-stu-id="b275b-156">If so, it validates the header value, and then modifies the request method.</span></span> <span data-ttu-id="b275b-157">最后，该处理程序调用`base.SendAsync`若要将消息传递到下一个处理程序。</span><span class="sxs-lookup"><span data-stu-id="b275b-157">Finally, the handler calls `base.SendAsync` to pass the message to the next handler.</span></span>

<span data-ttu-id="b275b-158">当请求到达**HttpControllerDispatcher**类， **HttpControllerDispatcher**基于更新的请求方法请求将路由。</span><span class="sxs-lookup"><span data-stu-id="b275b-158">When the request reaches the **HttpControllerDispatcher** class, **HttpControllerDispatcher** will route the request based on the updated request method.</span></span>

## <a name="example-adding-a-custom-response-header"></a><span data-ttu-id="b275b-159">示例:添加自定义响应标头</span><span class="sxs-lookup"><span data-stu-id="b275b-159">Example: Adding a Custom Response Header</span></span>

<span data-ttu-id="b275b-160">下面是将自定义标头添加到每个响应消息的消息处理程序：</span><span class="sxs-lookup"><span data-stu-id="b275b-160">Here is a message handler that adds a custom header to every response message:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample8.cs)]

<span data-ttu-id="b275b-161">首先，该处理程序调用`base.SendAsync`将请求传递给内部消息处理程序。</span><span class="sxs-lookup"><span data-stu-id="b275b-161">First, the handler calls `base.SendAsync` to pass the request to the inner message handler.</span></span> <span data-ttu-id="b275b-162">内部处理程序返回响应消息，但它不使用因此以异步方式**任务&lt;T&gt;** 对象。</span><span class="sxs-lookup"><span data-stu-id="b275b-162">The inner handler returns a response message, but it does so asynchronously using a **Task&lt;T&gt;** object.</span></span> <span data-ttu-id="b275b-163">响应消息不是后才可`base.SendAsync`以异步方式完成。</span><span class="sxs-lookup"><span data-stu-id="b275b-163">The response message is not available until `base.SendAsync` completes asynchronously.</span></span>

<span data-ttu-id="b275b-164">此示例使用**await**关键字来执行工作后，将异步`SendAsync`完成。</span><span class="sxs-lookup"><span data-stu-id="b275b-164">This example uses the **await** keyword to perform work asynchronously after `SendAsync` completes.</span></span> <span data-ttu-id="b275b-165">如果你面向的.NET Framework 4.0，使用**任务**&lt;T&gt;**。ContinueWith**方法：</span><span class="sxs-lookup"><span data-stu-id="b275b-165">If you are targeting .NET Framework 4.0, use the **Task**&lt;T&gt;**.ContinueWith** method:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample9.cs)]

## <a name="example-checking-for-an-api-key"></a><span data-ttu-id="b275b-166">示例:正在检查的 API 密钥</span><span class="sxs-lookup"><span data-stu-id="b275b-166">Example: Checking for an API Key</span></span>

<span data-ttu-id="b275b-167">某些 web 服务要求客户端在其请求中包含的 API 密钥。</span><span class="sxs-lookup"><span data-stu-id="b275b-167">Some web services require clients to include an API key in their request.</span></span> <span data-ttu-id="b275b-168">下面的示例演示消息处理程序可以检查有效的 API 密钥的请求的方式：</span><span class="sxs-lookup"><span data-stu-id="b275b-168">The following example shows how a message handler can check requests for a valid API key:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample10.cs)]

<span data-ttu-id="b275b-169">此处理程序将查找在 URI 查询字符串中的 API 密钥。</span><span class="sxs-lookup"><span data-stu-id="b275b-169">This handler looks for the API key in the URI query string.</span></span> <span data-ttu-id="b275b-170">（对于此示例中，我们假定该密钥是静态字符串。</span><span class="sxs-lookup"><span data-stu-id="b275b-170">(For this example, we assume that the key is a static string.</span></span> <span data-ttu-id="b275b-171">真正的实现可能需要使用更复杂的验证。）如果查询字符串包含的密钥，该处理程序会将请求传递给内部处理程序。</span><span class="sxs-lookup"><span data-stu-id="b275b-171">A real implementation would probably use more complex validation.) If the query string contains the key, the handler passes the request to the inner handler.</span></span>

<span data-ttu-id="b275b-172">如果请求没有有效的密钥，该处理程序创建响应消息与状态 403，禁止访问。</span><span class="sxs-lookup"><span data-stu-id="b275b-172">If the request does not have a valid key, the handler creates a response message with status 403, Forbidden.</span></span> <span data-ttu-id="b275b-173">在这种情况下，该处理程序不会调用`base.SendAsync`，因此内部处理程序永远不会收到请求时，也不在控制器。</span><span class="sxs-lookup"><span data-stu-id="b275b-173">In this case, the handler does not call `base.SendAsync`, so the inner handler never receives the request, nor does the controller.</span></span> <span data-ttu-id="b275b-174">因此，控制器可以假定所有传入请求具有有效的 API 密钥。</span><span class="sxs-lookup"><span data-stu-id="b275b-174">Therefore, the controller can assume that all incoming requests have a valid API key.</span></span>

> [!NOTE]
> <span data-ttu-id="b275b-175">如果 API 密钥仅适用于特定控制器操作，请考虑使用操作筛选器而不消息处理程序。</span><span class="sxs-lookup"><span data-stu-id="b275b-175">If the API key applies only to certain controller actions, consider using an action filter instead of a message handler.</span></span> <span data-ttu-id="b275b-176">操作筛选器运行 URI 路由执行后。</span><span class="sxs-lookup"><span data-stu-id="b275b-176">Action filters run after URI routing is performed.</span></span>


## <a name="per-route-message-handlers"></a><span data-ttu-id="b275b-177">每个路由的消息处理程序</span><span class="sxs-lookup"><span data-stu-id="b275b-177">Per-Route Message Handlers</span></span>

<span data-ttu-id="b275b-178">中的处理程序**HttpConfiguration.MessageHandlers**集合执行全局应用。</span><span class="sxs-lookup"><span data-stu-id="b275b-178">Handlers in the **HttpConfiguration.MessageHandlers** collection apply globally.</span></span>

<span data-ttu-id="b275b-179">或者，可以将消息处理程序添加到特定的路由时定义的路由,：</span><span class="sxs-lookup"><span data-stu-id="b275b-179">Alternatively, you can add a message handler to a specific route when you define the route:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample11.cs?highlight=16)]

<span data-ttu-id="b275b-180">在此示例中，如果在请求 URI 与匹配"Route2"，请求将被调度到`MessageHandler2`。</span><span class="sxs-lookup"><span data-stu-id="b275b-180">In this example, if the request URI matches "Route2", the request is dispatched to `MessageHandler2`.</span></span> <span data-ttu-id="b275b-181">下图显示了这两个路由的管道：</span><span class="sxs-lookup"><span data-stu-id="b275b-181">The following diagram shows the pipeline for these two routes:</span></span>

![](http-message-handlers/_static/image4.png)

<span data-ttu-id="b275b-182">请注意，`MessageHandler2`替换的默认值**HttpControllerDispatcher**。</span><span class="sxs-lookup"><span data-stu-id="b275b-182">Notice that `MessageHandler2` replaces the default **HttpControllerDispatcher**.</span></span> <span data-ttu-id="b275b-183">在此示例中，`MessageHandler2`创建响应，并的匹配"Route2"永远不会转到控制器的请求。</span><span class="sxs-lookup"><span data-stu-id="b275b-183">In this example, `MessageHandler2` creates the response, and requests that match "Route2" never go to a controller.</span></span> <span data-ttu-id="b275b-184">这使您的整个 Web API 控制器机制替换为你自己的自定义终结点。</span><span class="sxs-lookup"><span data-stu-id="b275b-184">This lets you replace the entire Web API controller mechanism with your own custom endpoint.</span></span>

<span data-ttu-id="b275b-185">或者，可以每个路由消息处理程序委托给**HttpControllerDispatcher**，后者随后将调度到的控制器。</span><span class="sxs-lookup"><span data-stu-id="b275b-185">Alternatively, a per-route message handler can delegate to **HttpControllerDispatcher**, which then dispatches to a controller.</span></span>

![](http-message-handlers/_static/image5.png)

<span data-ttu-id="b275b-186">下面的代码演示如何配置此路由：</span><span class="sxs-lookup"><span data-stu-id="b275b-186">The following code shows how to configure this route:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample12.cs)]

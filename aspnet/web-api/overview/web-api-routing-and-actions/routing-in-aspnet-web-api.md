---
uid: web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api
title: ASP.NET Web API 中的路由 |微软文档
author: MikeWasson
description: ''
ms.author: riande
ms.date: 10/29/2018
ms.assetid: 0675bdc7-282f-4f47-b7f3-7e02133940ca
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 85862c094cc54365267b1f21e68d235a15519cda
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675753"
---
# <a name="routing-in-aspnet-web-api"></a><span data-ttu-id="dfa7a-102">Routing in ASP.NET Web API（在 ASP.NET Web API 中路由）</span><span class="sxs-lookup"><span data-stu-id="dfa7a-102">Routing in ASP.NET Web API</span></span>

<span data-ttu-id="dfa7a-103">由[迈克·瓦森](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="dfa7a-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="dfa7a-104">本文介绍ASP.NET Web API 如何将 HTTP 请求路由到控制器。</span><span class="sxs-lookup"><span data-stu-id="dfa7a-104">This article describes how ASP.NET Web API routes HTTP requests to controllers.</span></span>

> [!NOTE]
> <span data-ttu-id="dfa7a-105">如果您熟悉ASP.NET MVC，则 Web API 路由与 MVC 路由非常相似。</span><span class="sxs-lookup"><span data-stu-id="dfa7a-105">If you are familiar with ASP.NET MVC, Web API routing is very similar to MVC routing.</span></span> <span data-ttu-id="dfa7a-106">主要区别是 Web API 使用 HTTP 谓词（而不是 URI 路径）来选择操作。</span><span class="sxs-lookup"><span data-stu-id="dfa7a-106">The main difference is that Web API uses the HTTP verb, not the URI path, to select the action.</span></span> <span data-ttu-id="dfa7a-107">您还可以在 Web API 中使用 MVC 样式路由。</span><span class="sxs-lookup"><span data-stu-id="dfa7a-107">You can also use MVC-style routing in Web API.</span></span> <span data-ttu-id="dfa7a-108">本文不假定任何有关ASP.NET MVC 的知识。</span><span class="sxs-lookup"><span data-stu-id="dfa7a-108">This article does not assume any knowledge of ASP.NET MVC.</span></span>

## <a name="routing-tables"></a><span data-ttu-id="dfa7a-109">路由表</span><span class="sxs-lookup"><span data-stu-id="dfa7a-109">Routing Tables</span></span>

<span data-ttu-id="dfa7a-110">在 Web API ASP.NET，*控制器*是处理 HTTP 请求的类。</span><span class="sxs-lookup"><span data-stu-id="dfa7a-110">In ASP.NET Web API, a *controller* is a class that handles HTTP requests.</span></span> <span data-ttu-id="dfa7a-111">控制器的公共方法称为*操作方法*或简单的*操作*。</span><span class="sxs-lookup"><span data-stu-id="dfa7a-111">The public methods of the controller are called *action methods* or simply *actions*.</span></span> <span data-ttu-id="dfa7a-112">当 Web API 框架收到请求时，它将请求路由到操作。</span><span class="sxs-lookup"><span data-stu-id="dfa7a-112">When the Web API framework receives a request, it routes the request to an action.</span></span>

<span data-ttu-id="dfa7a-113">要确定要调用的操作，框架使用*路由表*。</span><span class="sxs-lookup"><span data-stu-id="dfa7a-113">To determine which action to invoke, the framework uses a *routing table*.</span></span> <span data-ttu-id="dfa7a-114">Web API 的可视化工作室项目模板创建默认路由：</span><span class="sxs-lookup"><span data-stu-id="dfa7a-114">The Visual Studio project template for Web API creates a default route:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample1.cs)]

<span data-ttu-id="dfa7a-115">此路由在*WebApiConfig.cs*文件中定义，该文件放置在 *"\_应用开始"* 目录中：</span><span class="sxs-lookup"><span data-stu-id="dfa7a-115">This route is defined in the *WebApiConfig.cs* file, which is placed in the *App\_Start* directory:</span></span>

![](routing-in-aspnet-web-api/_static/image1.png)

<span data-ttu-id="dfa7a-116">有关该类的详细信息，`WebApiConfig`请参阅[配置ASP.NET Web API](../advanced/configuring-aspnet-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="dfa7a-116">For more information about the `WebApiConfig` class, see [Configuring ASP.NET Web API](../advanced/configuring-aspnet-web-api.md).</span></span>

<span data-ttu-id="dfa7a-117">如果自承载 Web API，则必须直接在`HttpSelfHostConfiguration`对象上设置路由表。</span><span class="sxs-lookup"><span data-stu-id="dfa7a-117">If you self-host Web API, you must set the routing table directly on the `HttpSelfHostConfiguration` object.</span></span> <span data-ttu-id="dfa7a-118">有关详细信息，请参阅[自主机 Web API](../older-versions/self-host-a-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="dfa7a-118">For more information, see [Self-Host a Web API](../older-versions/self-host-a-web-api.md).</span></span>

<span data-ttu-id="dfa7a-119">路由表中的每个条目都包含*一个路由模板*。</span><span class="sxs-lookup"><span data-stu-id="dfa7a-119">Each entry in the routing table contains a *route template*.</span></span> <span data-ttu-id="dfa7a-120">Web API 的默认路由模板&quot;是 api/{控制器}/{id}。&quot;</span><span class="sxs-lookup"><span data-stu-id="dfa7a-120">The default route template for Web API is &quot;api/{controller}/{id}&quot;.</span></span> <span data-ttu-id="dfa7a-121">在此模板中&quot;，api&quot;是文本路径段，[控制器] 和 {id} 是占位符变量。</span><span class="sxs-lookup"><span data-stu-id="dfa7a-121">In this template, &quot;api&quot; is a literal path segment, and {controller} and {id} are placeholder variables.</span></span>

<span data-ttu-id="dfa7a-122">当 Web API 框架收到 HTTP 请求时，它会尝试将 URI 与路由表中的路由模板之一匹配。</span><span class="sxs-lookup"><span data-stu-id="dfa7a-122">When the Web API framework receives an HTTP request, it tries to match the URI against one of the route templates in the routing table.</span></span> <span data-ttu-id="dfa7a-123">如果没有路由匹配，客户端将收到 404 错误。</span><span class="sxs-lookup"><span data-stu-id="dfa7a-123">If no route matches, the client receives a 404 error.</span></span> <span data-ttu-id="dfa7a-124">例如，以下 URI 与默认路由匹配：</span><span class="sxs-lookup"><span data-stu-id="dfa7a-124">For example, the following URIs match the default route:</span></span>

- <span data-ttu-id="dfa7a-125">/api/触点</span><span class="sxs-lookup"><span data-stu-id="dfa7a-125">/api/contacts</span></span>
- <span data-ttu-id="dfa7a-126">/api/触点/1</span><span class="sxs-lookup"><span data-stu-id="dfa7a-126">/api/contacts/1</span></span>
- <span data-ttu-id="dfa7a-127">/api/产品/gizmo1</span><span class="sxs-lookup"><span data-stu-id="dfa7a-127">/api/products/gizmo1</span></span>

<span data-ttu-id="dfa7a-128">但是，以下 URI 不匹配，因为它缺少&quot;api&quot;段：</span><span class="sxs-lookup"><span data-stu-id="dfa7a-128">However, the following URI does not match, because it lacks the &quot;api&quot; segment:</span></span>

- <span data-ttu-id="dfa7a-129">/触点/1</span><span class="sxs-lookup"><span data-stu-id="dfa7a-129">/contacts/1</span></span>

> [!NOTE]
> <span data-ttu-id="dfa7a-130">在路由中使用"api"的原因是为了避免与ASP.NET MVC 路由发生冲突。</span><span class="sxs-lookup"><span data-stu-id="dfa7a-130">The reason for using "api" in the route is to avoid collisions with ASP.NET MVC routing.</span></span> <span data-ttu-id="dfa7a-131">这样&quot;，您可以让 /联系人&quot;转到 MVC 控制器，/api/&quot;联系人&quot;转到 Web API 控制器。</span><span class="sxs-lookup"><span data-stu-id="dfa7a-131">That way, you can have &quot;/contacts&quot; go to an MVC controller, and &quot;/api/contacts&quot; go to a Web API controller.</span></span> <span data-ttu-id="dfa7a-132">当然，如果您不喜欢此约定，则可以更改默认路由表。</span><span class="sxs-lookup"><span data-stu-id="dfa7a-132">Of course, if you don't like this convention, you can change the default route table.</span></span>

<span data-ttu-id="dfa7a-133">找到匹配路由后，Web API 将选择控制器和操作：</span><span class="sxs-lookup"><span data-stu-id="dfa7a-133">Once a matching route is found, Web API selects the controller and the action:</span></span>

- <span data-ttu-id="dfa7a-134">要查找控制器，Web API&quot;将&quot;控制器添加到 *[控制器]* 变量的值。</span><span class="sxs-lookup"><span data-stu-id="dfa7a-134">To find the controller, Web API adds &quot;Controller&quot; to the value of the *{controller}* variable.</span></span>
- <span data-ttu-id="dfa7a-135">要查找操作，Web API 将查看 HTTP 谓词，然后查找名称以该 HTTP 谓词名称开头的操作。</span><span class="sxs-lookup"><span data-stu-id="dfa7a-135">To find the action, Web API looks at the HTTP verb, and then looks for an action whose name begins with that HTTP verb name.</span></span> <span data-ttu-id="dfa7a-136">例如，对于 GET 请求，Web &quot;API 会查找使用 Get&quot;预置的操作&quot;，例如&quot;获取&quot;联系人或获取&quot;所有联系人。</span><span class="sxs-lookup"><span data-stu-id="dfa7a-136">For example, with a GET request, Web API looks for an action prefixed with &quot;Get&quot;, such as &quot;GetContact&quot; or &quot;GetAllContacts&quot;.</span></span> <span data-ttu-id="dfa7a-137">此约定仅适用于 GET、POST、PUT、DELETE、头、选项和 PATCH 谓词。</span><span class="sxs-lookup"><span data-stu-id="dfa7a-137">This convention applies only to GET, POST, PUT, DELETE, HEAD, OPTIONS, and PATCH verbs.</span></span> <span data-ttu-id="dfa7a-138">您可以使用控制器上的属性启用其他 HTTP 谓词。</span><span class="sxs-lookup"><span data-stu-id="dfa7a-138">You can enable other HTTP verbs by using attributes on your controller.</span></span> <span data-ttu-id="dfa7a-139">稍后我们将看到示例。</span><span class="sxs-lookup"><span data-stu-id="dfa7a-139">We'll see an example of that later.</span></span>
- <span data-ttu-id="dfa7a-140">工艺路线模板中的其他占位符变量（如 *{id}）* 映射到操作参数。</span><span class="sxs-lookup"><span data-stu-id="dfa7a-140">Other placeholder variables in the route template, such as *{id},* are mapped to action parameters.</span></span>

<span data-ttu-id="dfa7a-141">接下来举例说明。</span><span class="sxs-lookup"><span data-stu-id="dfa7a-141">Let's look at an example.</span></span> <span data-ttu-id="dfa7a-142">假设您定义了以下控制器：</span><span class="sxs-lookup"><span data-stu-id="dfa7a-142">Suppose that you define the following controller:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample2.cs)]

<span data-ttu-id="dfa7a-143">下面是一些可能的 HTTP 请求，以及为每个请求调用的操作：</span><span class="sxs-lookup"><span data-stu-id="dfa7a-143">Here are some possible HTTP requests, along with the action that gets invoked for each:</span></span>

| <span data-ttu-id="dfa7a-144">HTTP 谓词</span><span class="sxs-lookup"><span data-stu-id="dfa7a-144">HTTP Verb</span></span> | <span data-ttu-id="dfa7a-145">URI 路径</span><span class="sxs-lookup"><span data-stu-id="dfa7a-145">URI Path</span></span> | <span data-ttu-id="dfa7a-146">操作</span><span class="sxs-lookup"><span data-stu-id="dfa7a-146">Action</span></span> | <span data-ttu-id="dfa7a-147">参数</span><span class="sxs-lookup"><span data-stu-id="dfa7a-147">Parameter</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="dfa7a-148">GET</span><span class="sxs-lookup"><span data-stu-id="dfa7a-148">GET</span></span> | <span data-ttu-id="dfa7a-149">api/产品</span><span class="sxs-lookup"><span data-stu-id="dfa7a-149">api/products</span></span> | <span data-ttu-id="dfa7a-150">获取所有产品</span><span class="sxs-lookup"><span data-stu-id="dfa7a-150">GetAllProducts</span></span> | <span data-ttu-id="dfa7a-151">*（无）*</span><span class="sxs-lookup"><span data-stu-id="dfa7a-151">*(none)*</span></span> |
| <span data-ttu-id="dfa7a-152">GET</span><span class="sxs-lookup"><span data-stu-id="dfa7a-152">GET</span></span> | <span data-ttu-id="dfa7a-153">api/产品/4</span><span class="sxs-lookup"><span data-stu-id="dfa7a-153">api/products/4</span></span> | <span data-ttu-id="dfa7a-154">获取产品 ById</span><span class="sxs-lookup"><span data-stu-id="dfa7a-154">GetProductById</span></span> | <span data-ttu-id="dfa7a-155">4</span><span class="sxs-lookup"><span data-stu-id="dfa7a-155">4</span></span> |
| <span data-ttu-id="dfa7a-156">DELETE</span><span class="sxs-lookup"><span data-stu-id="dfa7a-156">DELETE</span></span> | <span data-ttu-id="dfa7a-157">api/产品/4</span><span class="sxs-lookup"><span data-stu-id="dfa7a-157">api/products/4</span></span> | <span data-ttu-id="dfa7a-158">删除产品</span><span class="sxs-lookup"><span data-stu-id="dfa7a-158">DeleteProduct</span></span> | <span data-ttu-id="dfa7a-159">4</span><span class="sxs-lookup"><span data-stu-id="dfa7a-159">4</span></span> |
| <span data-ttu-id="dfa7a-160">POST</span><span class="sxs-lookup"><span data-stu-id="dfa7a-160">POST</span></span> | <span data-ttu-id="dfa7a-161">api/产品</span><span class="sxs-lookup"><span data-stu-id="dfa7a-161">api/products</span></span> | <span data-ttu-id="dfa7a-162">*（不匹配）*</span><span class="sxs-lookup"><span data-stu-id="dfa7a-162">*(no match)*</span></span> |  |

<span data-ttu-id="dfa7a-163">请注意，URI 的 *[id]* 段（如果存在）映射到操作的*id*参数。</span><span class="sxs-lookup"><span data-stu-id="dfa7a-163">Notice that the *{id}* segment of the URI, if present, is mapped to the *id* parameter of the action.</span></span> <span data-ttu-id="dfa7a-164">在此示例中，控制器定义了两个 GET 方法，一个使用*id*参数，另一个没有参数。</span><span class="sxs-lookup"><span data-stu-id="dfa7a-164">In this example, the controller defines two GET methods, one with an *id* parameter and one with no parameters.</span></span>

<span data-ttu-id="dfa7a-165">此外，请注意，POST 请求将失败，因为控制器未定义&quot;Post...&quot;方法。</span><span class="sxs-lookup"><span data-stu-id="dfa7a-165">Also, note that the POST request will fail, because the controller does not define a &quot;Post...&quot; method.</span></span>

## <a name="routing-variations"></a><span data-ttu-id="dfa7a-166">路由变体</span><span class="sxs-lookup"><span data-stu-id="dfa7a-166">Routing Variations</span></span>

<span data-ttu-id="dfa7a-167">上一节介绍了ASP.NET Web API 的基本路由机制。</span><span class="sxs-lookup"><span data-stu-id="dfa7a-167">The previous section described the basic routing mechanism for ASP.NET Web API.</span></span> <span data-ttu-id="dfa7a-168">本节介绍一些变体。</span><span class="sxs-lookup"><span data-stu-id="dfa7a-168">This section describes some variations.</span></span>

### <a name="http-verbs"></a><span data-ttu-id="dfa7a-169">HTTP 谓词</span><span class="sxs-lookup"><span data-stu-id="dfa7a-169">HTTP verbs</span></span>

<span data-ttu-id="dfa7a-170">无需对 HTTP 谓词使用命名约定，还可以通过使用以下属性之一来修饰操作方法之一，显式指定操作的 HTTP 谓词：</span><span class="sxs-lookup"><span data-stu-id="dfa7a-170">Instead of using the naming convention for HTTP verbs, you can explicitly specify the HTTP verb for an action by decorating the action method with one of the following attributes:</span></span>

- `[HttpGet]`
- `[HttpPut]`
- `[HttpPost]`
- `[HttpDelete]`
- `[HttpHead]`
- `[HttpOptions]`
- `[HttpPatch]`

<span data-ttu-id="dfa7a-171">在下面的示例中，`FindProduct`该方法映射到 GET 请求：</span><span class="sxs-lookup"><span data-stu-id="dfa7a-171">In the following example, the `FindProduct` method is mapped to GET requests:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample3.cs)]

<span data-ttu-id="dfa7a-172">要允许多个 HTTP 谓词用于某个操作，或允许除 GET、PUT、POST、DELETE、HEAD、OPTIONS 和 PATCH 以外的 HTTP`[AcceptVerbs]`谓词，请使用该属性，该属性采用 HTTP 谓词的列表。</span><span class="sxs-lookup"><span data-stu-id="dfa7a-172">To allow multiple HTTP verbs for an action, or to allow HTTP verbs other than GET, PUT, POST, DELETE, HEAD, OPTIONS, and PATCH, use the `[AcceptVerbs]` attribute, which takes a list of HTTP verbs.</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample4.cs)]

<a id="routing_by_action_name"></a>
### <a name="routing-by-action-name"></a><span data-ttu-id="dfa7a-173">按操作名称路由</span><span class="sxs-lookup"><span data-stu-id="dfa7a-173">Routing by Action Name</span></span>

<span data-ttu-id="dfa7a-174">使用默认路由模板，Web API 使用 HTTP 谓词选择操作。</span><span class="sxs-lookup"><span data-stu-id="dfa7a-174">With the default routing template, Web API uses the HTTP verb to select the action.</span></span> <span data-ttu-id="dfa7a-175">但是，您还可以创建一个路由，其中操作名称包含在 URI 中：</span><span class="sxs-lookup"><span data-stu-id="dfa7a-175">However, you can also create a route where the action name is included in the URI:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample5.cs)]

<span data-ttu-id="dfa7a-176">在此路由模板中 *，[操作]* 参数在控制器上命名操作方法。</span><span class="sxs-lookup"><span data-stu-id="dfa7a-176">In this route template, the *{action}* parameter names the action method on the controller.</span></span> <span data-ttu-id="dfa7a-177">使用此路由样式，使用属性指定允许的 HTTP 谓词。</span><span class="sxs-lookup"><span data-stu-id="dfa7a-177">With this style of routing, use attributes to specify the allowed HTTP verbs.</span></span> <span data-ttu-id="dfa7a-178">例如，假设您的控制器具有以下方法：</span><span class="sxs-lookup"><span data-stu-id="dfa7a-178">For example, suppose your controller has the following method:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample6.cs)]

<span data-ttu-id="dfa7a-179">在这种情况下，GET 请求的"api/产品/详细信息/1"将映射到`Details`该方法。</span><span class="sxs-lookup"><span data-stu-id="dfa7a-179">In this case, a GET request for "api/products/details/1" would map to the `Details` method.</span></span> <span data-ttu-id="dfa7a-180">这种路由样式类似于 mVC ASP.NET，可能适用于 RPC 样式的 API。</span><span class="sxs-lookup"><span data-stu-id="dfa7a-180">This style of routing is similar to ASP.NET MVC, and may be appropriate for an RPC-style API.</span></span>

<span data-ttu-id="dfa7a-181">可以使用 属性重写操作名称`[ActionName]`。</span><span class="sxs-lookup"><span data-stu-id="dfa7a-181">You can override the action name by using the `[ActionName]` attribute.</span></span> <span data-ttu-id="dfa7a-182">在下面的示例中，有两个操作映射到&quot;api/产品/缩略图/*id*。一个支持 GET，另一个支持 POST：</span><span class="sxs-lookup"><span data-stu-id="dfa7a-182">In the following example, there are two actions that map to &quot;api/products/thumbnail/*id*. One supports GET and the other supports POST:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample7.cs)]

### <a name="non-actions"></a><span data-ttu-id="dfa7a-183">非操作</span><span class="sxs-lookup"><span data-stu-id="dfa7a-183">Non-Actions</span></span>

<span data-ttu-id="dfa7a-184">要防止将方法作为操作调用，请使用 属性`[NonAction]`。</span><span class="sxs-lookup"><span data-stu-id="dfa7a-184">To prevent a method from getting invoked as an action, use the `[NonAction]` attribute.</span></span> <span data-ttu-id="dfa7a-185">这向框架发出信号，说明该方法不是操作，即使它以其他方式与路由规则匹配也是如此。</span><span class="sxs-lookup"><span data-stu-id="dfa7a-185">This signals to the framework that the method is not an action, even if it would otherwise match the routing rules.</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample8.cs)]

## <a name="further-reading"></a><span data-ttu-id="dfa7a-186">延伸阅读</span><span class="sxs-lookup"><span data-stu-id="dfa7a-186">Further Reading</span></span>

<span data-ttu-id="dfa7a-187">本主题提供了路由的高级视图。</span><span class="sxs-lookup"><span data-stu-id="dfa7a-187">This topic provided a high-level view of routing.</span></span> <span data-ttu-id="dfa7a-188">有关详细信息，请参阅[路由和操作选择](routing-and-action-selection.md)，它准确描述框架如何将 URI 与路由匹配，选择控制器，然后选择要调用的操作。</span><span class="sxs-lookup"><span data-stu-id="dfa7a-188">For more detail, see [Routing and Action Selection](routing-and-action-selection.md), which describes exactly how the framework matches a URI to a route, selects a controller, and then selects the action to invoke.</span></span>

---
uid: web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2
title: ASP.NET Web API 2 中的属性路由 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 01/20/2014
ms.assetid: 979d6c9f-0129-4e5b-ae56-4507b281b86d
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2
msc.type: authoredcontent
ms.openlocfilehash: 7da1805d8a7066e82743dc9bd7e024cc9813ee89
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78446996"
---
# <a name="attribute-routing-in-aspnet-web-api-2"></a><span data-ttu-id="2f594-102">ASP.NET Web API 2 中的属性路由</span><span class="sxs-lookup"><span data-stu-id="2f594-102">Attribute Routing in ASP.NET Web API 2</span></span>

<span data-ttu-id="2f594-103">作者： [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="2f594-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="2f594-104">*路由*是 Web API 与操作的 URI 匹配的方式。</span><span class="sxs-lookup"><span data-stu-id="2f594-104">*Routing* is how Web API matches a URI to an action.</span></span> <span data-ttu-id="2f594-105">Web API 2 支持一种新的路由类型，称为*属性路由*。</span><span class="sxs-lookup"><span data-stu-id="2f594-105">Web API 2 supports a new type of routing, called *attribute routing*.</span></span> <span data-ttu-id="2f594-106">顾名思义，特性路由使用特性来定义路由。</span><span class="sxs-lookup"><span data-stu-id="2f594-106">As the name implies, attribute routing uses attributes to define routes.</span></span> <span data-ttu-id="2f594-107">特性路由使你可以更好地控制 web API 中的 Uri。</span><span class="sxs-lookup"><span data-stu-id="2f594-107">Attribute routing gives you more control over the URIs in your web API.</span></span> <span data-ttu-id="2f594-108">例如，你可以轻松地创建用于描述资源层次结构的 Uri。</span><span class="sxs-lookup"><span data-stu-id="2f594-108">For example, you can easily create URIs that describe hierarchies of resources.</span></span>

<span data-ttu-id="2f594-109">仍完全支持早期的路由样式，称为基于约定的路由。</span><span class="sxs-lookup"><span data-stu-id="2f594-109">The earlier style of routing, called convention-based routing, is still fully supported.</span></span> <span data-ttu-id="2f594-110">事实上，您可以将这两种技术组合到同一个项目中。</span><span class="sxs-lookup"><span data-stu-id="2f594-110">In fact, you can combine both techniques in the same project.</span></span>

<span data-ttu-id="2f594-111">本主题演示如何启用属性路由，并介绍了用于属性路由的各种选项。</span><span class="sxs-lookup"><span data-stu-id="2f594-111">This topic shows how to enable attribute routing and describes the various options for attribute routing.</span></span> <span data-ttu-id="2f594-112">有关使用属性路由的端到端教程，请参阅使用[WEB API 2 中的属性路由创建 REST API](create-a-rest-api-with-attribute-routing.md)。</span><span class="sxs-lookup"><span data-stu-id="2f594-112">For an end-to-end tutorial that uses attribute routing, see [Create a REST API with Attribute Routing in Web API 2](create-a-rest-api-with-attribute-routing.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2f594-113">系统必备</span><span class="sxs-lookup"><span data-stu-id="2f594-113">Prerequisites</span></span>

<span data-ttu-id="2f594-114">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)社区版、专业版或企业版</span><span class="sxs-lookup"><span data-stu-id="2f594-114">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community, Professional, or Enterprise edition</span></span>

<span data-ttu-id="2f594-115">或者，使用 NuGet 包管理器来安装所需的包。</span><span class="sxs-lookup"><span data-stu-id="2f594-115">Alternatively, use NuGet Package Manager to install the necessary packages.</span></span> <span data-ttu-id="2f594-116">在 Visual Studio 的 "**工具**" 菜单中，选择 " **NuGet 包管理器**"，然后选择 "**程序包管理器控制台**"。</span><span class="sxs-lookup"><span data-stu-id="2f594-116">From the **Tools** menu in Visual Studio, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="2f594-117">在 "包管理器控制台" 窗口中输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="2f594-117">Enter the following command in the Package Manager Console window:</span></span>

`Install-Package Microsoft.AspNet.WebApi.WebHost`

<a id="why"></a>
## <a name="why-attribute-routing"></a><span data-ttu-id="2f594-118">为什么选择属性？</span><span class="sxs-lookup"><span data-stu-id="2f594-118">Why Attribute Routing?</span></span>

<span data-ttu-id="2f594-119">Web API 使用的第一版*基于约定*的路由。</span><span class="sxs-lookup"><span data-stu-id="2f594-119">The first release of Web API used *convention-based* routing.</span></span> <span data-ttu-id="2f594-120">在该类型的路由中，可以定义一个或多个路由模板，它们基本上是参数化字符串。</span><span class="sxs-lookup"><span data-stu-id="2f594-120">In that type of routing, you define one or more route templates, which are basically parameterized strings.</span></span> <span data-ttu-id="2f594-121">当框架收到请求时，它会将 URI 与路由模板进行匹配。</span><span class="sxs-lookup"><span data-stu-id="2f594-121">When the framework receives a request, it matches the URI against the route template.</span></span> <span data-ttu-id="2f594-122">（有关基于约定的路由的详细信息，请参阅[ASP.NET Web API 中的路由](routing-in-aspnet-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="2f594-122">(For more information about convention-based routing, see [Routing in ASP.NET Web API](routing-in-aspnet-web-api.md).</span></span>

<span data-ttu-id="2f594-123">基于约定的路由的优点之一是，在单个位置定义模板，并且在所有控制器上一致地应用路由规则。</span><span class="sxs-lookup"><span data-stu-id="2f594-123">One advantage of convention-based routing is that templates are defined in a single place, and the routing rules are applied consistently across all controllers.</span></span> <span data-ttu-id="2f594-124">遗憾的是，基于约定的路由使支持 RESTful Api 中常见的某些 URI 模式变得很困难。</span><span class="sxs-lookup"><span data-stu-id="2f594-124">Unfortunately, convention-based routing makes it hard to support certain URI patterns that are common in RESTful APIs.</span></span> <span data-ttu-id="2f594-125">例如，资源通常包含子资源：客户具有订单、电影具有参与者、书籍具有作者等。</span><span class="sxs-lookup"><span data-stu-id="2f594-125">For example, resources often contain child resources: Customers have orders, movies have actors, books have authors, and so forth.</span></span> <span data-ttu-id="2f594-126">创建反映这些关系的 Uri 很自然：</span><span class="sxs-lookup"><span data-stu-id="2f594-126">It's natural to create URIs that reflect these relations:</span></span>

`/customers/1/orders`

<span data-ttu-id="2f594-127">使用基于约定的路由很难创建这种类型的 URI。</span><span class="sxs-lookup"><span data-stu-id="2f594-127">This type of URI is difficult to create using convention-based routing.</span></span> <span data-ttu-id="2f594-128">尽管可以完成此操作，但如果有多个控制器或资源类型，结果不会很好地进行缩放。</span><span class="sxs-lookup"><span data-stu-id="2f594-128">Although it can be done, the results don't scale well if you have many controllers or resource types.</span></span>

<span data-ttu-id="2f594-129">使用属性路由，为此 URI 定义路由很简单。</span><span class="sxs-lookup"><span data-stu-id="2f594-129">With attribute routing, it's trivial to define a route for this URI.</span></span> <span data-ttu-id="2f594-130">只需将属性添加到控制器操作即可：</span><span class="sxs-lookup"><span data-stu-id="2f594-130">You simply add an attribute to the controller action:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample1.cs)]

<span data-ttu-id="2f594-131">下面是一些其他模式，属性路由非常简单。</span><span class="sxs-lookup"><span data-stu-id="2f594-131">Here are some other patterns that attribute routing makes easy.</span></span>

<span data-ttu-id="2f594-132">**API 版本控制**</span><span class="sxs-lookup"><span data-stu-id="2f594-132">**API versioning**</span></span>

<span data-ttu-id="2f594-133">在此示例中，"/api/v1/products" 将路由到与 "/api/v2/products" 不同的控制器。</span><span class="sxs-lookup"><span data-stu-id="2f594-133">In this example, "/api/v1/products" would be routed to a different controller than "/api/v2/products".</span></span>

`/api/v1/products`
`/api/v2/products`

<span data-ttu-id="2f594-134">**重载的 URI 段**</span><span class="sxs-lookup"><span data-stu-id="2f594-134">**Overloaded URI segments**</span></span>

<span data-ttu-id="2f594-135">在此示例中，"1" 是订单号，但 "挂起" 映射到集合。</span><span class="sxs-lookup"><span data-stu-id="2f594-135">In this example, "1" is an order number, but "pending" maps to a collection.</span></span>

`/orders/1`
`/orders/pending`

<span data-ttu-id="2f594-136">**多个参数类型**</span><span class="sxs-lookup"><span data-stu-id="2f594-136">**Multiple parameter types**</span></span>

<span data-ttu-id="2f594-137">在此示例中，"1" 是订单号，而 "2013/06/16" 指定日期。</span><span class="sxs-lookup"><span data-stu-id="2f594-137">In this example, "1" is an order number, but "2013/06/16" specifies a date.</span></span>

`/orders/1`
`/orders/2013/06/16`

<a id="enable"></a>
## <a name="enabling-attribute-routing"></a><span data-ttu-id="2f594-138">启用属性路由</span><span class="sxs-lookup"><span data-stu-id="2f594-138">Enabling Attribute Routing</span></span>

<span data-ttu-id="2f594-139">若要启用属性路由，请在配置过程中调用**MapHttpAttributeRoutes** 。</span><span class="sxs-lookup"><span data-stu-id="2f594-139">To enable attribute routing, call **MapHttpAttributeRoutes** during configuration.</span></span> <span data-ttu-id="2f594-140">此扩展方法在**HttpConfigurationExtensions**类中定义。</span><span class="sxs-lookup"><span data-stu-id="2f594-140">This extension method is defined in the **System.Web.Http.HttpConfigurationExtensions** class.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample2.cs)]

<span data-ttu-id="2f594-141">属性路由可以与[基于约定](routing-in-aspnet-web-api.md)的路由结合。</span><span class="sxs-lookup"><span data-stu-id="2f594-141">Attribute routing can be combined with [convention-based](routing-in-aspnet-web-api.md) routing.</span></span> <span data-ttu-id="2f594-142">若要定义基于约定的路由，请调用**MapHttpRoute**方法。</span><span class="sxs-lookup"><span data-stu-id="2f594-142">To define convention-based routes, call the **MapHttpRoute** method.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample3.cs)]

<span data-ttu-id="2f594-143">有关配置 Web API 的详细信息，请参阅[配置 ASP.NET Web API 2](../advanced/configuring-aspnet-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="2f594-143">For more information about configuring Web API, see [Configuring ASP.NET Web API 2](../advanced/configuring-aspnet-web-api.md).</span></span>

<a id="config"></a>
### <a name="note-migrating-from-web-api-1"></a><span data-ttu-id="2f594-144">注意：从 Web API 进行迁移</span><span class="sxs-lookup"><span data-stu-id="2f594-144">Note: Migrating From Web API 1</span></span>

<span data-ttu-id="2f594-145">在 Web API 2 之前，Web API 项目模板生成的代码如下所示：</span><span class="sxs-lookup"><span data-stu-id="2f594-145">Prior to Web API 2, the Web API project templates generated code like this:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample4.cs)]

<span data-ttu-id="2f594-146">如果启用了属性路由，则此代码将引发异常。</span><span class="sxs-lookup"><span data-stu-id="2f594-146">If attribute routing is enabled, this code will throw an exception.</span></span> <span data-ttu-id="2f594-147">如果升级现有 Web API 项目以使用属性路由，请确保将此配置代码更新为以下内容：</span><span class="sxs-lookup"><span data-stu-id="2f594-147">If you upgrade an existing Web API project to use attribute routing, make sure to update this configuration code to the following:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample5.cs?highlight=4)]

> [!NOTE]
> <span data-ttu-id="2f594-148">有关详细信息，请参阅[配置包含 ASP.NET 托管的 WEB API](../advanced/configuring-aspnet-web-api.md#webhost)。</span><span class="sxs-lookup"><span data-stu-id="2f594-148">For more information, see [Configuring Web API with ASP.NET Hosting](../advanced/configuring-aspnet-web-api.md#webhost).</span></span>

<a id="add-routes"></a>
## <a name="adding-route-attributes"></a><span data-ttu-id="2f594-149">添加路由属性</span><span class="sxs-lookup"><span data-stu-id="2f594-149">Adding Route Attributes</span></span>

<span data-ttu-id="2f594-150">下面是使用属性定义的路由示例：</span><span class="sxs-lookup"><span data-stu-id="2f594-150">Here is an example of a route defined using an attribute:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample6.cs)]

<span data-ttu-id="2f594-151">String &quot;customers/{customerId}/orders&quot; 是路由的 URI 模板。</span><span class="sxs-lookup"><span data-stu-id="2f594-151">The string &quot;customers/{customerId}/orders&quot; is the URI template for the route.</span></span> <span data-ttu-id="2f594-152">Web API 尝试将请求 URI 与模板匹配。</span><span class="sxs-lookup"><span data-stu-id="2f594-152">Web API tries to match the request URI to the template.</span></span> <span data-ttu-id="2f594-153">在此示例中，"customers" 和 "orders" 是文本段，而 "{customerId}" 是变量参数。</span><span class="sxs-lookup"><span data-stu-id="2f594-153">In this example, "customers" and "orders" are literal segments, and "{customerId}" is a variable parameter.</span></span> <span data-ttu-id="2f594-154">以下 Uri 将与此模板匹配：</span><span class="sxs-lookup"><span data-stu-id="2f594-154">The following URIs would match this template:</span></span>

- `http://localhost/customers/1/orders`
- `http://localhost/customers/bob/orders`
- `http://localhost/customers/1234-5678/orders`

<span data-ttu-id="2f594-155">您可以使用[约束](#constraints)（本主题后面所述）限制匹配。</span><span class="sxs-lookup"><span data-stu-id="2f594-155">You can restrict the matching by using [constraints](#constraints), described later in this topic.</span></span>

<span data-ttu-id="2f594-156">请注意，路由模板中的 &quot;{customerId}&quot; 参数与方法中的*customerId*参数的名称匹配。</span><span class="sxs-lookup"><span data-stu-id="2f594-156">Notice that the &quot;{customerId}&quot; parameter in the route template matches the name of the *customerId* parameter in the method.</span></span> <span data-ttu-id="2f594-157">当 Web API 调用控制器操作时，它会尝试绑定路由参数。</span><span class="sxs-lookup"><span data-stu-id="2f594-157">When Web API invokes the controller action, it tries to bind the route parameters.</span></span> <span data-ttu-id="2f594-158">例如，如果 URI 是 `http://example.com/customers/1/orders`的，Web API 将尝试将值 "1" 绑定到操作中的*customerId*参数。</span><span class="sxs-lookup"><span data-stu-id="2f594-158">For example, if the URI is `http://example.com/customers/1/orders`, Web API tries to bind the value "1" to the *customerId* parameter in the action.</span></span>

<span data-ttu-id="2f594-159">URI 模板可以有多个参数：</span><span class="sxs-lookup"><span data-stu-id="2f594-159">A URI template can have several parameters:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample7.cs)]

<span data-ttu-id="2f594-160">没有路由属性的任何控制器方法都使用基于约定的路由。</span><span class="sxs-lookup"><span data-stu-id="2f594-160">Any controller methods that do not have a route attribute use convention-based routing.</span></span> <span data-ttu-id="2f594-161">这样，便可以在同一个项目中组合这两种类型的路由。</span><span class="sxs-lookup"><span data-stu-id="2f594-161">That way, you can combine both types of routing in the same project.</span></span>

## <a name="http-methods"></a><span data-ttu-id="2f594-162">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="2f594-162">HTTP Methods</span></span>

<span data-ttu-id="2f594-163">Web API 还会根据请求的 HTTP 方法（GET、POST 等）来选择操作。</span><span class="sxs-lookup"><span data-stu-id="2f594-163">Web API also selects actions based on the HTTP method of the request (GET, POST, etc).</span></span> <span data-ttu-id="2f594-164">默认情况下，Web API 将查找与控制器方法名称开头的不区分大小写的匹配项。</span><span class="sxs-lookup"><span data-stu-id="2f594-164">By default, Web API looks for a case-insensitive match with the start of the controller method name.</span></span> <span data-ttu-id="2f594-165">例如，名为 `PutCustomers` 的控制器方法匹配 HTTP PUT 请求。</span><span class="sxs-lookup"><span data-stu-id="2f594-165">For example, a controller method named `PutCustomers` matches an HTTP PUT request.</span></span>

<span data-ttu-id="2f594-166">可以通过使用以下任何属性修饰方法来重写此约定：</span><span class="sxs-lookup"><span data-stu-id="2f594-166">You can override this convention by decorating the method with any the following attributes:</span></span>

- <span data-ttu-id="2f594-167">**HttpDelete**</span><span class="sxs-lookup"><span data-stu-id="2f594-167">**[HttpDelete]**</span></span>
- <span data-ttu-id="2f594-168">**[HttpGet]**</span><span class="sxs-lookup"><span data-stu-id="2f594-168">**[HttpGet]**</span></span>
- <span data-ttu-id="2f594-169">**[HttpHead]**</span><span class="sxs-lookup"><span data-stu-id="2f594-169">**[HttpHead]**</span></span>
- <span data-ttu-id="2f594-170">**HttpOptions**</span><span class="sxs-lookup"><span data-stu-id="2f594-170">**[HttpOptions]**</span></span>
- <span data-ttu-id="2f594-171">**[HttpPatch]**</span><span class="sxs-lookup"><span data-stu-id="2f594-171">**[HttpPatch]**</span></span>
- <span data-ttu-id="2f594-172">**HttpPost**</span><span class="sxs-lookup"><span data-stu-id="2f594-172">**[HttpPost]**</span></span>
- <span data-ttu-id="2f594-173">**HttpPut**</span><span class="sxs-lookup"><span data-stu-id="2f594-173">**[HttpPut]**</span></span>

<span data-ttu-id="2f594-174">下面的示例将 CreateBook 方法映射到 HTTP POST 请求。</span><span class="sxs-lookup"><span data-stu-id="2f594-174">The following example maps the CreateBook method to HTTP POST requests.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample8.cs)]

<span data-ttu-id="2f594-175">对于所有其他 HTTP 方法（包括非标准方法），请使用**AcceptVerbs**属性，该属性采用 HTTP 方法的列表。</span><span class="sxs-lookup"><span data-stu-id="2f594-175">For all other HTTP methods, including non-standard methods, use the **AcceptVerbs** attribute, which takes a list of HTTP methods.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample9.cs)]

<a id="prefixes"></a>
## <a name="route-prefixes"></a><span data-ttu-id="2f594-176">路由前缀</span><span class="sxs-lookup"><span data-stu-id="2f594-176">Route Prefixes</span></span>

<span data-ttu-id="2f594-177">通常，控制器中的路由都以相同的前缀开头。</span><span class="sxs-lookup"><span data-stu-id="2f594-177">Often, the routes in a controller all start with the same prefix.</span></span> <span data-ttu-id="2f594-178">例如:</span><span class="sxs-lookup"><span data-stu-id="2f594-178">For example:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample10.cs)]

<span data-ttu-id="2f594-179">可以使用 **[RoutePrefix]** 属性为整个控制器设置公共前缀：</span><span class="sxs-lookup"><span data-stu-id="2f594-179">You can set a common prefix for an entire controller by using the **[RoutePrefix]** attribute:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample11.cs)]

<span data-ttu-id="2f594-180">在方法特性上使用波形符（~）来重写路由前缀：</span><span class="sxs-lookup"><span data-stu-id="2f594-180">Use a tilde (~) on the method attribute to override the route prefix:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample12.cs)]

<span data-ttu-id="2f594-181">路由前缀可以包含参数：</span><span class="sxs-lookup"><span data-stu-id="2f594-181">The route prefix can include parameters:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample13.cs)]

<a id="constraints"></a>
## <a name="route-constraints"></a><span data-ttu-id="2f594-182">路由约束</span><span class="sxs-lookup"><span data-stu-id="2f594-182">Route Constraints</span></span>

<span data-ttu-id="2f594-183">路由约束允许您限制路由模板中的参数的匹配方式。</span><span class="sxs-lookup"><span data-stu-id="2f594-183">Route constraints let you restrict how the parameters in the route template are matched.</span></span> <span data-ttu-id="2f594-184">一般语法为 &quot;{parameter： constraint}&quot;。</span><span class="sxs-lookup"><span data-stu-id="2f594-184">The general syntax is &quot;{parameter:constraint}&quot;.</span></span> <span data-ttu-id="2f594-185">例如:</span><span class="sxs-lookup"><span data-stu-id="2f594-185">For example:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample14.cs)]

<span data-ttu-id="2f594-186">此处，如果 URI &quot;id&quot; 段是一个整数，则仅选择第一个路由。</span><span class="sxs-lookup"><span data-stu-id="2f594-186">Here, the first route will only be selected if the &quot;id&quot; segment of the URI is an integer.</span></span> <span data-ttu-id="2f594-187">否则，将选择第二个路由。</span><span class="sxs-lookup"><span data-stu-id="2f594-187">Otherwise, the second route will be chosen.</span></span>

<span data-ttu-id="2f594-188">下表列出了支持的约束。</span><span class="sxs-lookup"><span data-stu-id="2f594-188">The following table lists the constraints that are supported.</span></span>

| <span data-ttu-id="2f594-189">约束</span><span class="sxs-lookup"><span data-stu-id="2f594-189">Constraint</span></span> | <span data-ttu-id="2f594-190">说明</span><span class="sxs-lookup"><span data-stu-id="2f594-190">Description</span></span> | <span data-ttu-id="2f594-191">示例</span><span class="sxs-lookup"><span data-stu-id="2f594-191">Example</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2f594-192">alpha</span><span class="sxs-lookup"><span data-stu-id="2f594-192">alpha</span></span> | <span data-ttu-id="2f594-193">匹配大写或小写拉丁字母字符（a-z、a-z）</span><span class="sxs-lookup"><span data-stu-id="2f594-193">Matches uppercase or lowercase Latin alphabet characters (a-z, A-Z)</span></span> | <span data-ttu-id="2f594-194">{x:alpha}</span><span class="sxs-lookup"><span data-stu-id="2f594-194">{x:alpha}</span></span> |
| <span data-ttu-id="2f594-195">bool</span><span class="sxs-lookup"><span data-stu-id="2f594-195">bool</span></span> | <span data-ttu-id="2f594-196">与布尔值匹配。</span><span class="sxs-lookup"><span data-stu-id="2f594-196">Matches a Boolean value.</span></span> | <span data-ttu-id="2f594-197">{x:bool}</span><span class="sxs-lookup"><span data-stu-id="2f594-197">{x:bool}</span></span> |
| <span data-ttu-id="2f594-198">datetime</span><span class="sxs-lookup"><span data-stu-id="2f594-198">datetime</span></span> | <span data-ttu-id="2f594-199">与**DateTime**值匹配。</span><span class="sxs-lookup"><span data-stu-id="2f594-199">Matches a **DateTime** value.</span></span> | <span data-ttu-id="2f594-200">{x:datetime}</span><span class="sxs-lookup"><span data-stu-id="2f594-200">{x:datetime}</span></span> |
| <span data-ttu-id="2f594-201">decimal</span><span class="sxs-lookup"><span data-stu-id="2f594-201">decimal</span></span> | <span data-ttu-id="2f594-202">匹配十进制值。</span><span class="sxs-lookup"><span data-stu-id="2f594-202">Matches a decimal value.</span></span> | <span data-ttu-id="2f594-203">{x:decimal}</span><span class="sxs-lookup"><span data-stu-id="2f594-203">{x:decimal}</span></span> |
| <span data-ttu-id="2f594-204">double</span><span class="sxs-lookup"><span data-stu-id="2f594-204">double</span></span> | <span data-ttu-id="2f594-205">匹配64位浮点值。</span><span class="sxs-lookup"><span data-stu-id="2f594-205">Matches a 64-bit floating-point value.</span></span> | <span data-ttu-id="2f594-206">x：double</span><span class="sxs-lookup"><span data-stu-id="2f594-206">{x:double}</span></span> |
| <span data-ttu-id="2f594-207">浮点数</span><span class="sxs-lookup"><span data-stu-id="2f594-207">float</span></span> | <span data-ttu-id="2f594-208">匹配32位浮点值。</span><span class="sxs-lookup"><span data-stu-id="2f594-208">Matches a 32-bit floating-point value.</span></span> | <span data-ttu-id="2f594-209">{x:float}</span><span class="sxs-lookup"><span data-stu-id="2f594-209">{x:float}</span></span> |
| <span data-ttu-id="2f594-210">guid</span><span class="sxs-lookup"><span data-stu-id="2f594-210">guid</span></span> | <span data-ttu-id="2f594-211">匹配 GUID 值。</span><span class="sxs-lookup"><span data-stu-id="2f594-211">Matches a GUID value.</span></span> | <span data-ttu-id="2f594-212">{x:guid}</span><span class="sxs-lookup"><span data-stu-id="2f594-212">{x:guid}</span></span> |
| <span data-ttu-id="2f594-213">int</span><span class="sxs-lookup"><span data-stu-id="2f594-213">int</span></span> | <span data-ttu-id="2f594-214">匹配32位整数值。</span><span class="sxs-lookup"><span data-stu-id="2f594-214">Matches a 32-bit integer value.</span></span> | <span data-ttu-id="2f594-215">{x:int}</span><span class="sxs-lookup"><span data-stu-id="2f594-215">{x:int}</span></span> |
| <span data-ttu-id="2f594-216">length</span><span class="sxs-lookup"><span data-stu-id="2f594-216">length</span></span> | <span data-ttu-id="2f594-217">与指定长度或指定长度范围内的字符串匹配。</span><span class="sxs-lookup"><span data-stu-id="2f594-217">Matches a string with the specified length or within a specified range of lengths.</span></span> | <span data-ttu-id="2f594-218">{x:length （6）}{x:length （1，20）}</span><span class="sxs-lookup"><span data-stu-id="2f594-218">{x:length(6)} {x:length(1,20)}</span></span> |
| <span data-ttu-id="2f594-219">long</span><span class="sxs-lookup"><span data-stu-id="2f594-219">long</span></span> | <span data-ttu-id="2f594-220">匹配64位整数值。</span><span class="sxs-lookup"><span data-stu-id="2f594-220">Matches a 64-bit integer value.</span></span> | <span data-ttu-id="2f594-221">{x:long}</span><span class="sxs-lookup"><span data-stu-id="2f594-221">{x:long}</span></span> |
| <span data-ttu-id="2f594-222">max</span><span class="sxs-lookup"><span data-stu-id="2f594-222">max</span></span> | <span data-ttu-id="2f594-223">匹配整数和最大值。</span><span class="sxs-lookup"><span data-stu-id="2f594-223">Matches an integer with a maximum value.</span></span> | <span data-ttu-id="2f594-224">{x:max(10)}</span><span class="sxs-lookup"><span data-stu-id="2f594-224">{x:max(10)}</span></span> |
| <span data-ttu-id="2f594-225">长度</span><span class="sxs-lookup"><span data-stu-id="2f594-225">maxlength</span></span> | <span data-ttu-id="2f594-226">匹配最大长度的字符串。</span><span class="sxs-lookup"><span data-stu-id="2f594-226">Matches a string with a maximum length.</span></span> | <span data-ttu-id="2f594-227">{x:maxlength （10）}</span><span class="sxs-lookup"><span data-stu-id="2f594-227">{x:maxlength(10)}</span></span> |
| <span data-ttu-id="2f594-228">min</span><span class="sxs-lookup"><span data-stu-id="2f594-228">min</span></span> | <span data-ttu-id="2f594-229">匹配整数和最小值。</span><span class="sxs-lookup"><span data-stu-id="2f594-229">Matches an integer with a minimum value.</span></span> | <span data-ttu-id="2f594-230">{x:min （10）}</span><span class="sxs-lookup"><span data-stu-id="2f594-230">{x:min(10)}</span></span> |
| <span data-ttu-id="2f594-231">minlength</span><span class="sxs-lookup"><span data-stu-id="2f594-231">minlength</span></span> | <span data-ttu-id="2f594-232">匹配最小长度的字符串。</span><span class="sxs-lookup"><span data-stu-id="2f594-232">Matches a string with a minimum length.</span></span> | <span data-ttu-id="2f594-233">{x:minlength （10）}</span><span class="sxs-lookup"><span data-stu-id="2f594-233">{x:minlength(10)}</span></span> |
| <span data-ttu-id="2f594-234">range</span><span class="sxs-lookup"><span data-stu-id="2f594-234">range</span></span> | <span data-ttu-id="2f594-235">匹配某个值范围内的一个整数。</span><span class="sxs-lookup"><span data-stu-id="2f594-235">Matches an integer within a range of values.</span></span> | <span data-ttu-id="2f594-236">{x:range （10，50）}</span><span class="sxs-lookup"><span data-stu-id="2f594-236">{x:range(10,50)}</span></span> |
| <span data-ttu-id="2f594-237">正则表达式</span><span class="sxs-lookup"><span data-stu-id="2f594-237">regex</span></span> | <span data-ttu-id="2f594-238">匹配正则表达式。</span><span class="sxs-lookup"><span data-stu-id="2f594-238">Matches a regular expression.</span></span> | <span data-ttu-id="2f594-239">{x:regex （^ \d{3}-\d{3}-\d{4}$）}</span><span class="sxs-lookup"><span data-stu-id="2f594-239">{x:regex(^\d{3}-\d{3}-\d{4}$)}</span></span> |

<span data-ttu-id="2f594-240">请注意，某些约束（如 &quot;min&quot;）采用括号中的参数。</span><span class="sxs-lookup"><span data-stu-id="2f594-240">Notice that some of the constraints, such as &quot;min&quot;, take arguments in parentheses.</span></span> <span data-ttu-id="2f594-241">可以将多个约束应用于参数，并以冒号分隔。</span><span class="sxs-lookup"><span data-stu-id="2f594-241">You can apply multiple constraints to a parameter, separated by a colon.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample15.cs)]

### <a name="custom-route-constraints"></a><span data-ttu-id="2f594-242">自定义路由约束</span><span class="sxs-lookup"><span data-stu-id="2f594-242">Custom Route Constraints</span></span>

<span data-ttu-id="2f594-243">可以通过实现**IHttpRouteConstraint**接口创建自定义路由约束。</span><span class="sxs-lookup"><span data-stu-id="2f594-243">You can create custom route constraints by implementing the **IHttpRouteConstraint** interface.</span></span> <span data-ttu-id="2f594-244">例如，下面的约束将参数限制为一个非零的整数值。</span><span class="sxs-lookup"><span data-stu-id="2f594-244">For example, the following constraint restricts a parameter to a non-zero integer value.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample16.cs)]

<span data-ttu-id="2f594-245">下面的代码演示如何注册约束：</span><span class="sxs-lookup"><span data-stu-id="2f594-245">The following code shows how to register the constraint:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample17.cs)]

<span data-ttu-id="2f594-246">现在，你可以在路由中应用约束：</span><span class="sxs-lookup"><span data-stu-id="2f594-246">Now you can apply the constraint in your routes:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample18.cs)]

<span data-ttu-id="2f594-247">还可以通过实现**IInlineConstraintResolver**接口来替换整个**DefaultInlineConstraintResolver**类。</span><span class="sxs-lookup"><span data-stu-id="2f594-247">You can also replace the entire **DefaultInlineConstraintResolver** class by implementing the **IInlineConstraintResolver** interface.</span></span> <span data-ttu-id="2f594-248">这样做将替换所有内置约束，除非**IInlineConstraintResolver**的实现专门添加它们。</span><span class="sxs-lookup"><span data-stu-id="2f594-248">Doing so will replace all of the built-in constraints, unless your implementation of **IInlineConstraintResolver** specifically adds them.</span></span>

<a id="optional"></a>
## <a name="optional-uri-parameters-and-default-values"></a><span data-ttu-id="2f594-249">可选 URI 参数和默认值</span><span class="sxs-lookup"><span data-stu-id="2f594-249">Optional URI Parameters and Default Values</span></span>

<span data-ttu-id="2f594-250">可以通过向 route 参数添加问号来使 URI 参数成为可选的。</span><span class="sxs-lookup"><span data-stu-id="2f594-250">You can make a URI parameter optional by adding a question mark to the route parameter.</span></span> <span data-ttu-id="2f594-251">如果路由参数是可选的，则必须为 method 参数定义默认值。</span><span class="sxs-lookup"><span data-stu-id="2f594-251">If a route parameter is optional, you must define a default value for the method parameter.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample19.cs)]

<span data-ttu-id="2f594-252">在此示例中，`/api/books/locale/1033` 和 `/api/books/locale` 返回相同资源。</span><span class="sxs-lookup"><span data-stu-id="2f594-252">In this example, `/api/books/locale/1033` and `/api/books/locale` return the same resource.</span></span>

<span data-ttu-id="2f594-253">另外，还可以在路由模板中指定默认值，如下所示：</span><span class="sxs-lookup"><span data-stu-id="2f594-253">Alternatively, you can specify a default value inside the route template, as follows:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample20.cs)]

<span data-ttu-id="2f594-254">这与前面的示例几乎相同，但在应用默认值时，行为存在细微的差异。</span><span class="sxs-lookup"><span data-stu-id="2f594-254">This is almost the same as the previous example, but there is a slight difference of behavior when the default value is applied.</span></span>

- <span data-ttu-id="2f594-255">在第一个示例（"{lcid： int？}"）中，默认值1033将直接分配给 method 参数，因此参数将具有此精确值。</span><span class="sxs-lookup"><span data-stu-id="2f594-255">In the first example ("{lcid:int?}"), the default value of 1033 is assigned directly to the method parameter, so the parameter will have this exact value.</span></span>
- <span data-ttu-id="2f594-256">在第二个示例（"{lcid： int = 1033}"）中，默认值 "1033" 通过模型绑定过程。</span><span class="sxs-lookup"><span data-stu-id="2f594-256">In the second example ("{lcid:int=1033}"), the default value of "1033" goes through the model-binding process.</span></span> <span data-ttu-id="2f594-257">默认的模型联编程序会将 "1033" 转换为数值1033。</span><span class="sxs-lookup"><span data-stu-id="2f594-257">The default model-binder will convert "1033" to the numeric value 1033.</span></span> <span data-ttu-id="2f594-258">但是，可以插入自定义模型绑定器，这可能会执行其他操作。</span><span class="sxs-lookup"><span data-stu-id="2f594-258">However, you could plug in a custom model binder, which might do something different.</span></span>

<span data-ttu-id="2f594-259">（在大多数情况下，除非管道中有自定义模型联编程序，否则两个窗体将是等效的。）</span><span class="sxs-lookup"><span data-stu-id="2f594-259">(In most cases, unless you have custom model binders in your pipeline, the two forms will be equivalent.)</span></span>

<a id="route-names"></a>
## <a name="route-names"></a><span data-ttu-id="2f594-260">路由名称</span><span class="sxs-lookup"><span data-stu-id="2f594-260">Route Names</span></span>

<span data-ttu-id="2f594-261">在 Web API 中，每个路由都有一个名称。</span><span class="sxs-lookup"><span data-stu-id="2f594-261">In Web API, every route has a name.</span></span> <span data-ttu-id="2f594-262">路由名称用于生成链接，以便可以在 HTTP 响应中包含链接。</span><span class="sxs-lookup"><span data-stu-id="2f594-262">Route names are useful for generating links, so that you can include a link in an HTTP response.</span></span>

<span data-ttu-id="2f594-263">若要指定路由名称，请设置属性的**name**属性。</span><span class="sxs-lookup"><span data-stu-id="2f594-263">To specify the route name, set the **Name** property on the attribute.</span></span> <span data-ttu-id="2f594-264">下面的示例演示如何设置路由名称，以及如何在生成链接时使用路由名称。</span><span class="sxs-lookup"><span data-stu-id="2f594-264">The following example shows how to set the route name, and also how to use the route name when generating a link.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample21.cs)]

<a id="order"></a>
## <a name="route-order"></a><span data-ttu-id="2f594-265">路由顺序</span><span class="sxs-lookup"><span data-stu-id="2f594-265">Route Order</span></span>

<span data-ttu-id="2f594-266">当框架尝试将 URI 与某个路由匹配时，它将按特定顺序计算路由。</span><span class="sxs-lookup"><span data-stu-id="2f594-266">When the framework tries to match a URI with a route, it evaluates the routes in a particular order.</span></span> <span data-ttu-id="2f594-267">若要指定顺序，请设置路由属性的**order**属性。</span><span class="sxs-lookup"><span data-stu-id="2f594-267">To specify the order, set the **Order** property on the route attribute.</span></span> <span data-ttu-id="2f594-268">首先计算较小的值。</span><span class="sxs-lookup"><span data-stu-id="2f594-268">Lower values are evaluated first.</span></span> <span data-ttu-id="2f594-269">默认顺序值为零。</span><span class="sxs-lookup"><span data-stu-id="2f594-269">The default order value is zero.</span></span>

<span data-ttu-id="2f594-270">下面介绍如何确定总计排序：</span><span class="sxs-lookup"><span data-stu-id="2f594-270">Here is how the total ordering is determined:</span></span>

1. <span data-ttu-id="2f594-271">比较路由属性的**Order**属性。</span><span class="sxs-lookup"><span data-stu-id="2f594-271">Compare the **Order** property of the route attribute.</span></span>
2. <span data-ttu-id="2f594-272">查看路由模板中的每个 URI 段。</span><span class="sxs-lookup"><span data-stu-id="2f594-272">Look at each URI segment in the route template.</span></span> <span data-ttu-id="2f594-273">对于每个段，按以下顺序排序：</span><span class="sxs-lookup"><span data-stu-id="2f594-273">For each segment, order as follows:</span></span>

    1. <span data-ttu-id="2f594-274">文本段。</span><span class="sxs-lookup"><span data-stu-id="2f594-274">Literal segments.</span></span>
    2. <span data-ttu-id="2f594-275">具有约束的路由参数。</span><span class="sxs-lookup"><span data-stu-id="2f594-275">Route parameters with constraints.</span></span>
    3. <span data-ttu-id="2f594-276">不带约束的路由参数。</span><span class="sxs-lookup"><span data-stu-id="2f594-276">Route parameters without constraints.</span></span>
    4. <span data-ttu-id="2f594-277">带有约束的通配符参数段。</span><span class="sxs-lookup"><span data-stu-id="2f594-277">Wildcard parameter segments with constraints.</span></span>
    5. <span data-ttu-id="2f594-278">没有约束的通配符参数段。</span><span class="sxs-lookup"><span data-stu-id="2f594-278">Wildcard parameter segments without constraints.</span></span>
3. <span data-ttu-id="2f594-279">对于并列，路由按路由模板的不区分大小写的序号字符串比较（[stringcomparison.ordinalignorecase](https://msdn.microsoft.com/library/system.stringcomparer.ordinalignorecase.aspx)）进行排序。</span><span class="sxs-lookup"><span data-stu-id="2f594-279">In the case of a tie, routes are ordered by a case-insensitive ordinal string comparison ([OrdinalIgnoreCase](https://msdn.microsoft.com/library/system.stringcomparer.ordinalignorecase.aspx)) of the route template.</span></span>

<span data-ttu-id="2f594-280">这是一个示例。</span><span class="sxs-lookup"><span data-stu-id="2f594-280">Here is an example.</span></span> <span data-ttu-id="2f594-281">假设您定义了以下控制器：</span><span class="sxs-lookup"><span data-stu-id="2f594-281">Suppose you define the following controller:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample22.cs)]

<span data-ttu-id="2f594-282">这些路由顺序如下所示。</span><span class="sxs-lookup"><span data-stu-id="2f594-282">These routes are ordered as follows.</span></span>

1. <span data-ttu-id="2f594-283">订单/详细信息</span><span class="sxs-lookup"><span data-stu-id="2f594-283">orders/details</span></span>
2. <span data-ttu-id="2f594-284">orders/{id}</span><span class="sxs-lookup"><span data-stu-id="2f594-284">orders/{id}</span></span>
3. <span data-ttu-id="2f594-285">orders/{customerName}</span><span class="sxs-lookup"><span data-stu-id="2f594-285">orders/{customerName}</span></span>
4. <span data-ttu-id="2f594-286">订单/{\*日期}</span><span class="sxs-lookup"><span data-stu-id="2f594-286">orders/{\*date}</span></span>
5. <span data-ttu-id="2f594-287">订单/挂起</span><span class="sxs-lookup"><span data-stu-id="2f594-287">orders/pending</span></span>

<span data-ttu-id="2f594-288">请注意，"详细信息" 是文本段，出现在 "{id}" 之前，但 "挂起" 显示在最后，因为**Order**属性为1。</span><span class="sxs-lookup"><span data-stu-id="2f594-288">Notice that "details" is a literal segment and appears before "{id}", but "pending" appears last because the **Order** property is 1.</span></span> <span data-ttu-id="2f594-289">（此示例假定不存在名为 "详细信息" 或 "挂起" 的客户。</span><span class="sxs-lookup"><span data-stu-id="2f594-289">(This example assumes there are no customers named "details" or "pending".</span></span> <span data-ttu-id="2f594-290">一般情况下，请尽量避免出现不明确的路由。</span><span class="sxs-lookup"><span data-stu-id="2f594-290">In general, try to avoid ambiguous routes.</span></span> <span data-ttu-id="2f594-291">在此示例中，`GetByCustomer` 的更好的路由模板为 "customers/{customerName}"）</span><span class="sxs-lookup"><span data-stu-id="2f594-291">In this example, a better route template for `GetByCustomer` is "customers/{customerName}" )</span></span>

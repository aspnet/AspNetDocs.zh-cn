---
uid: web-api/overview/formats-and-model-binding/parameter-binding-in-aspnet-web-api
title: ASP.NET Web API-ASP.NET 4.x 中的参数绑定
author: MikeWasson
description: 描述 Web API 如何绑定参数，以及如何在 ASP.NET 4.x 中自定义绑定过程。
ms.author: riande
ms.date: 07/11/2013
ms.custom: seoapril2019
ms.assetid: e42c8388-04ed-4341-9fdb-41b1b4c06320
msc.legacyurl: /web-api/overview/formats-and-model-binding/parameter-binding-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: da79a01b8493d489aced016d46e228b7f8186127
ms.sourcegitcommit: d4e2a07eeb2cdf19f0bfbfab4a469970bc7e1c99
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/12/2021
ms.locfileid: "98105255"
---
# <a name="parameter-binding-in-aspnet-web-api"></a><span data-ttu-id="a8230-103">ASP.NET Web API 中的参数绑定</span><span class="sxs-lookup"><span data-stu-id="a8230-103">Parameter Binding in ASP.NET Web API</span></span>

<span data-ttu-id="a8230-104">作者： [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="a8230-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[!INCLUDE[](~/includes/coreWebAPI.md)]

<span data-ttu-id="a8230-105">本文介绍了 Web API 如何绑定参数，以及如何自定义绑定过程。</span><span class="sxs-lookup"><span data-stu-id="a8230-105">This article describes how Web API binds parameters, and how you can customize the binding process.</span></span> <span data-ttu-id="a8230-106">当 Web API 在控制器上调用方法时，它必须设置参数的值，这是一个称为 " *绑定*" 的进程。</span><span class="sxs-lookup"><span data-stu-id="a8230-106">When Web API calls a method on a controller, it must set values for the parameters, a process called *binding*.</span></span>

<span data-ttu-id="a8230-107">默认情况下，Web API 使用以下规则来绑定参数：</span><span class="sxs-lookup"><span data-stu-id="a8230-107">By default, Web API uses the following rules to bind parameters:</span></span>

- <span data-ttu-id="a8230-108">如果该参数为 "simple" 类型，则 Web API 会尝试从 URI 获取值。</span><span class="sxs-lookup"><span data-stu-id="a8230-108">If the parameter is a "simple" type, Web API tries to get the value from the URI.</span></span> <span data-ttu-id="a8230-109">简单类型包括 .NET [基元类型](https://msdn.microsoft.com/library/system.type.isprimitive.aspx) (**int**、 **bool**、 **double** 等) ，以及 **TimeSpan**、 **DateTime**、 **Guid**、 **decimal** 和 **string**，以及具有可从字符串转换的类型转换器 *的任何类型* 。</span><span class="sxs-lookup"><span data-stu-id="a8230-109">Simple types include the .NET [primitive types](https://msdn.microsoft.com/library/system.type.isprimitive.aspx) (**int**, **bool**, **double**, and so forth), plus **TimeSpan**, **DateTime**, **Guid**, **decimal**, and **string**, *plus* any type with a type converter that can convert from a string.</span></span> <span data-ttu-id="a8230-110">稍后 (有关类型转换器的详细信息。 ) </span><span class="sxs-lookup"><span data-stu-id="a8230-110">(More about type converters later.)</span></span>
- <span data-ttu-id="a8230-111">对于复杂类型，Web API 会尝试使用 [媒体类型格式化程序](media-formatters.md)从消息正文中读取值。</span><span class="sxs-lookup"><span data-stu-id="a8230-111">For complex types, Web API tries to read the value from the message body, using a [media-type formatter](media-formatters.md).</span></span>

<span data-ttu-id="a8230-112">例如，下面是典型的 Web API 控制器方法：</span><span class="sxs-lookup"><span data-stu-id="a8230-112">For example, here is a typical Web API controller method:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample1.cs)]

<span data-ttu-id="a8230-113">*Id* 参数是 &quot; 简单 &quot; 类型，因此 Web API 会尝试从请求 URI 获取值。</span><span class="sxs-lookup"><span data-stu-id="a8230-113">The *id* parameter is a &quot;simple&quot; type, so Web API tries to get the value from the request URI.</span></span> <span data-ttu-id="a8230-114">*Item* 参数是复杂类型，因此 Web API 使用媒体类型格式化程序从请求正文中读取值。</span><span class="sxs-lookup"><span data-stu-id="a8230-114">The *item* parameter is a complex type, so Web API uses a media-type formatter to read the value from the request body.</span></span>

<span data-ttu-id="a8230-115">为了从 URI 获取值，Web API 将查找路由数据和 URI 查询字符串。</span><span class="sxs-lookup"><span data-stu-id="a8230-115">To get a value from the URI, Web API looks in the route data and the URI query string.</span></span> <span data-ttu-id="a8230-116">当路由系统分析 URI 并将其与路由匹配时，将填充路由数据。</span><span class="sxs-lookup"><span data-stu-id="a8230-116">The route data is populated when the routing system parses the URI and matches it to a route.</span></span> <span data-ttu-id="a8230-117">有关详细信息，请参阅 [路由和操作选择](../web-api-routing-and-actions/routing-and-action-selection.md)。</span><span class="sxs-lookup"><span data-stu-id="a8230-117">For more information, see [Routing and Action Selection](../web-api-routing-and-actions/routing-and-action-selection.md).</span></span>

<span data-ttu-id="a8230-118">本文的其余部分将介绍如何自定义模型绑定过程。</span><span class="sxs-lookup"><span data-stu-id="a8230-118">In the rest of this article, I'll show how you can customize the model binding process.</span></span> <span data-ttu-id="a8230-119">但对于复杂类型，请考虑尽可能使用媒体类型格式化程序。</span><span class="sxs-lookup"><span data-stu-id="a8230-119">For complex types, however, consider using media-type formatters whenever possible.</span></span> <span data-ttu-id="a8230-120">HTTP 的一项关键原则是，使用内容协商指定资源的表示形式，在消息正文中发送资源。</span><span class="sxs-lookup"><span data-stu-id="a8230-120">A key principle of HTTP is that resources are sent in the message body, using content negotiation to specify the representation of the resource.</span></span> <span data-ttu-id="a8230-121">媒体类型格式化程序旨在实现此目的。</span><span class="sxs-lookup"><span data-stu-id="a8230-121">Media-type formatters were designed for exactly this purpose.</span></span>

## <a name="using-fromuri"></a><span data-ttu-id="a8230-122">使用 [FromUri]</span><span class="sxs-lookup"><span data-stu-id="a8230-122">Using [FromUri]</span></span>

<span data-ttu-id="a8230-123">若要强制 Web API 从 URI 读取复杂类型，请将 **[FromUri]** 特性添加到参数中。</span><span class="sxs-lookup"><span data-stu-id="a8230-123">To force Web API to read a complex type from the URI, add the **[FromUri]** attribute to the parameter.</span></span> <span data-ttu-id="a8230-124">下面的示例定义了一个 `GeoPoint` 类型以及从 URI 获取的控制器方法 `GeoPoint` 。</span><span class="sxs-lookup"><span data-stu-id="a8230-124">The following example defines a `GeoPoint` type, along with a controller method that gets the `GeoPoint` from the URI.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample2.cs)]

<span data-ttu-id="a8230-125">客户端可以将纬度和经度值放在查询字符串中，Web API 将使用这些值来构造 `GeoPoint` 。</span><span class="sxs-lookup"><span data-stu-id="a8230-125">The client can put the Latitude and Longitude values in the query string and Web API will use them to construct a `GeoPoint`.</span></span> <span data-ttu-id="a8230-126">例如：</span><span class="sxs-lookup"><span data-stu-id="a8230-126">For example:</span></span>

`http://localhost/api/values/?Latitude=47.678558&Longitude=-122.130989`

## <a name="using-frombody"></a><span data-ttu-id="a8230-127">使用 [FromBody]</span><span class="sxs-lookup"><span data-stu-id="a8230-127">Using [FromBody]</span></span>

<span data-ttu-id="a8230-128">若要强制 Web API 从请求正文读取简单类型，请将 **[FromBody]** 特性添加到参数：</span><span class="sxs-lookup"><span data-stu-id="a8230-128">To force Web API to read a simple type from the request body, add the **[FromBody]** attribute to the parameter:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample3.cs)]

<span data-ttu-id="a8230-129">在此示例中，Web API 将使用媒体类型格式化程序从请求正文中读取 *名称* 的值。</span><span class="sxs-lookup"><span data-stu-id="a8230-129">In this example, Web API will use a media-type formatter to read the value of *name* from the request body.</span></span> <span data-ttu-id="a8230-130">下面是一个示例客户端请求。</span><span class="sxs-lookup"><span data-stu-id="a8230-130">Here is an example client request.</span></span>

[!code-console[Main](parameter-binding-in-aspnet-web-api/samples/sample4.cmd)]

<span data-ttu-id="a8230-131">当参数具有 [FromBody] 时，Web API 使用 Content-type 标头来选择格式化程序。</span><span class="sxs-lookup"><span data-stu-id="a8230-131">When a parameter has [FromBody], Web API uses the Content-Type header to select a formatter.</span></span> <span data-ttu-id="a8230-132">在此示例中，内容类型为 &quot; application/json， &quot; 请求正文是原始 json 字符串 (不是) 的 json 对象。</span><span class="sxs-lookup"><span data-stu-id="a8230-132">In this example, the content type is &quot;application/json&quot; and the request body is a raw JSON string (not a JSON object).</span></span>

<span data-ttu-id="a8230-133">最多允许一个参数读取消息正文。</span><span class="sxs-lookup"><span data-stu-id="a8230-133">At most one parameter is allowed to read from the message body.</span></span> <span data-ttu-id="a8230-134">这不起作用：</span><span class="sxs-lookup"><span data-stu-id="a8230-134">So this will not work:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample5.cs)]

<span data-ttu-id="a8230-135">此规则的原因是请求正文可能存储在只能读取一次的非缓冲流中。</span><span class="sxs-lookup"><span data-stu-id="a8230-135">The reason for this rule is that the request body might be stored in a non-buffered stream that can only be read once.</span></span>

## <a name="type-converters"></a><span data-ttu-id="a8230-136">类型转换器</span><span class="sxs-lookup"><span data-stu-id="a8230-136">Type Converters</span></span>

<span data-ttu-id="a8230-137">可以使 Web API 将某个类视为简单类型 (，以便 Web API 通过创建 **TypeConverter** 并提供字符串转换来尝试将其从 URI) 绑定。</span><span class="sxs-lookup"><span data-stu-id="a8230-137">You can make Web API treat a class as a simple type (so that Web API will try to bind it from the URI) by creating a **TypeConverter** and providing a string conversion.</span></span>

<span data-ttu-id="a8230-138">下面的代码演示一个 `GeoPoint` 表示地理点的类，以及一个从字符串转换为实例的 TypeConverter `GeoPoint` 。</span><span class="sxs-lookup"><span data-stu-id="a8230-138">The following code shows a `GeoPoint` class that represents a geographical point, plus a **TypeConverter** that converts from strings to `GeoPoint` instances.</span></span> <span data-ttu-id="a8230-139">`GeoPoint`使用 **[TypeConverter]** 特性修饰类来指定类型转换器。</span><span class="sxs-lookup"><span data-stu-id="a8230-139">The `GeoPoint` class is decorated with a **[TypeConverter]** attribute to specify the type converter.</span></span> <span data-ttu-id="a8230-140"> (此示例由 Mike 卡住的博客文章中的灵感， [如何绑定到 MVC/WebAPI 中的操作签名中的自定义对象](https://blogs.msdn.com/b/jmstall/archive/2012/04/20/how-to-bind-to-custom-objects-in-action-signatures-in-mvc-webapi.aspx)。 ) </span><span class="sxs-lookup"><span data-stu-id="a8230-140">(This example was inspired by Mike Stall's blog post [How to bind to custom objects in action signatures in MVC/WebAPI](https://blogs.msdn.com/b/jmstall/archive/2012/04/20/how-to-bind-to-custom-objects-in-action-signatures-in-mvc-webapi.aspx).)</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample6.cs)]

<span data-ttu-id="a8230-141">现在，Web API 将 `GeoPoint` 作为简单类型处理，这意味着它将尝试 `GeoPoint` 从 URI 绑定参数。</span><span class="sxs-lookup"><span data-stu-id="a8230-141">Now Web API will treat `GeoPoint` as a simple type, meaning it will try to bind `GeoPoint` parameters from the URI.</span></span> <span data-ttu-id="a8230-142">不需要在参数上包含 **[FromUri]** 。</span><span class="sxs-lookup"><span data-stu-id="a8230-142">You don't need to include **[FromUri]** on the parameter.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample7.cs)]

<span data-ttu-id="a8230-143">客户端可以使用如下所示的 URI 调用方法：</span><span class="sxs-lookup"><span data-stu-id="a8230-143">The client can invoke the method with a URI like this:</span></span>

`http://localhost/api/values/?location=47.678558,-122.130989`

## <a name="model-binders"></a><span data-ttu-id="a8230-144">模型联编程序</span><span class="sxs-lookup"><span data-stu-id="a8230-144">Model Binders</span></span>

<span data-ttu-id="a8230-145">比类型转换器更灵活的选项是创建自定义模型联编程序。</span><span class="sxs-lookup"><span data-stu-id="a8230-145">A more flexible option than a type converter is to create a custom model binder.</span></span> <span data-ttu-id="a8230-146">通过模型绑定器，你可以访问来自路由数据的 HTTP 请求、操作说明和原始值等项。</span><span class="sxs-lookup"><span data-stu-id="a8230-146">With a model binder, you have access to things like the HTTP request, the action description, and the raw values from the route data.</span></span>

<span data-ttu-id="a8230-147">若要创建模型联编程序，请实现 **IModelBinder** 接口。</span><span class="sxs-lookup"><span data-stu-id="a8230-147">To create a model binder, implement the **IModelBinder** interface.</span></span> <span data-ttu-id="a8230-148">此接口定义单个方法 **BindModel**：</span><span class="sxs-lookup"><span data-stu-id="a8230-148">This interface defines a single method, **BindModel**:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample8.cs)]

<span data-ttu-id="a8230-149">下面是对象的模型联编程序 `GeoPoint` 。</span><span class="sxs-lookup"><span data-stu-id="a8230-149">Here is a model binder for `GeoPoint` objects.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample9.cs)]

<span data-ttu-id="a8230-150">模型联编 *程序从值提供程序* 获取原始输入值。</span><span class="sxs-lookup"><span data-stu-id="a8230-150">A model binder gets raw input values from a *value provider*.</span></span> <span data-ttu-id="a8230-151">此设计将两个不同的函数隔开：</span><span class="sxs-lookup"><span data-stu-id="a8230-151">This design separates two distinct functions:</span></span>

- <span data-ttu-id="a8230-152">值提供程序获取 HTTP 请求并填充键值对字典。</span><span class="sxs-lookup"><span data-stu-id="a8230-152">The value provider takes the HTTP request and populates a dictionary of key-value pairs.</span></span>
- <span data-ttu-id="a8230-153">模型联编程序使用此字典填充模型。</span><span class="sxs-lookup"><span data-stu-id="a8230-153">The model binder uses this dictionary to populate the model.</span></span>

<span data-ttu-id="a8230-154">Web API 中的默认值提供程序从路由数据和查询字符串中获取值。</span><span class="sxs-lookup"><span data-stu-id="a8230-154">The default value provider in Web API gets values from the route data and the query string.</span></span> <span data-ttu-id="a8230-155">例如，如果 URI 为 `http://localhost/api/values/1?location=48,-122` ，则值提供程序将创建以下键值对：</span><span class="sxs-lookup"><span data-stu-id="a8230-155">For example, if the URI is `http://localhost/api/values/1?location=48,-122`, the value provider creates the following key-value pairs:</span></span>

- <span data-ttu-id="a8230-156">id = &quot; 1&quot;</span><span class="sxs-lookup"><span data-stu-id="a8230-156">id = &quot;1&quot;</span></span>
- <span data-ttu-id="a8230-157">location = &quot; 48，-122&quot;</span><span class="sxs-lookup"><span data-stu-id="a8230-157">location = &quot;48,-122&quot;</span></span>

<span data-ttu-id="a8230-158"> (我假设默认路由模板为 &quot; api/{controller}/{id} &quot; 。 ) </span><span class="sxs-lookup"><span data-stu-id="a8230-158">(I'm assuming the default route template, which is &quot;api/{controller}/{id}&quot;.)</span></span>

<span data-ttu-id="a8230-159">要绑定的参数的名称存储在 **ModelBindingContext. ModelName** 属性中。</span><span class="sxs-lookup"><span data-stu-id="a8230-159">The name of the parameter to bind is stored in the **ModelBindingContext.ModelName** property.</span></span> <span data-ttu-id="a8230-160">模型联编程序将在字典中查找具有此值的键。</span><span class="sxs-lookup"><span data-stu-id="a8230-160">The model binder looks for a key with this value in the dictionary.</span></span> <span data-ttu-id="a8230-161">如果该值存在并且可以转换为 `GeoPoint` ，则模型联编程序会将绑定值分配给 **ModelBindingContext** 属性。</span><span class="sxs-lookup"><span data-stu-id="a8230-161">If the value exists and can be converted into a `GeoPoint`, the model binder assigns the bound value to the **ModelBindingContext.Model** property.</span></span>

<span data-ttu-id="a8230-162">请注意，模型绑定器并不局限于简单的类型转换。</span><span class="sxs-lookup"><span data-stu-id="a8230-162">Notice that the model binder is not limited to a simple type conversion.</span></span> <span data-ttu-id="a8230-163">在此示例中，模型绑定器首先查找已知位置表，如果失败，则使用类型转换。</span><span class="sxs-lookup"><span data-stu-id="a8230-163">In this example, the model binder first looks in a table of known locations, and if that fails, it uses type conversion.</span></span>

<span data-ttu-id="a8230-164">**设置模型联编程序**</span><span class="sxs-lookup"><span data-stu-id="a8230-164">**Setting the Model Binder**</span></span>

<span data-ttu-id="a8230-165">有多种方法可以设置模型联编程序。</span><span class="sxs-lookup"><span data-stu-id="a8230-165">There are several ways to set a model binder.</span></span> <span data-ttu-id="a8230-166">首先，可以向参数添加 **[ModelBinder]** 特性。</span><span class="sxs-lookup"><span data-stu-id="a8230-166">First, you can add a **[ModelBinder]** attribute to the parameter.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample10.cs)]

<span data-ttu-id="a8230-167">你还可以将 **[ModelBinder]** 特性添加到该类型。</span><span class="sxs-lookup"><span data-stu-id="a8230-167">You can also add a **[ModelBinder]** attribute to the type.</span></span> <span data-ttu-id="a8230-168">Web API 将为该类型的所有参数使用指定的模型绑定器。</span><span class="sxs-lookup"><span data-stu-id="a8230-168">Web API will use the specified model binder for all parameters of that type.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample11.cs)]

<span data-ttu-id="a8230-169">最后，可以将模型联编程序提供程序添加到 **HttpConfiguration**。</span><span class="sxs-lookup"><span data-stu-id="a8230-169">Finally, you can add a model-binder provider to the **HttpConfiguration**.</span></span> <span data-ttu-id="a8230-170">模型联编程序提供程序只是创建模型联编程序的工厂类。</span><span class="sxs-lookup"><span data-stu-id="a8230-170">A model-binder provider is simply a factory class that creates a model binder.</span></span> <span data-ttu-id="a8230-171">可以通过从 [ModelBinderProvider](https://msdn.microsoft.com/library/system.web.http.modelbinding.modelbinderprovider.aspx) 类派生来创建提供程序。</span><span class="sxs-lookup"><span data-stu-id="a8230-171">You can create a provider by deriving from the [ModelBinderProvider](https://msdn.microsoft.com/library/system.web.http.modelbinding.modelbinderprovider.aspx) class.</span></span> <span data-ttu-id="a8230-172">但是，如果您的模型绑定器处理单个类型，则使用内置的 **SimpleModelBinderProvider**（专为此目的而设计）会更容易。</span><span class="sxs-lookup"><span data-stu-id="a8230-172">However, if your model binder handles a single type, it's easier to use the built-in **SimpleModelBinderProvider**, which is designed for this purpose.</span></span> <span data-ttu-id="a8230-173">下面的代码演示如何执行此操作。</span><span class="sxs-lookup"><span data-stu-id="a8230-173">The following code shows how to do this.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample12.cs)]

<span data-ttu-id="a8230-174">对于模型绑定提供程序，仍需要将 **[ModelBinder]** 特性添加到参数，以指示 Web API 应使用模型绑定器，而不是媒体类型格式化程序。</span><span class="sxs-lookup"><span data-stu-id="a8230-174">With a model-binding provider, you still need to add the **[ModelBinder]** attribute to the parameter, to tell Web API that it should use a model binder and not a media-type formatter.</span></span> <span data-ttu-id="a8230-175">但现在无需在属性中指定模型绑定器的类型：</span><span class="sxs-lookup"><span data-stu-id="a8230-175">But now you don't need to specify the type of model binder in the attribute:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample13.cs)]

## <a name="value-providers"></a><span data-ttu-id="a8230-176">值提供程序</span><span class="sxs-lookup"><span data-stu-id="a8230-176">Value Providers</span></span>

<span data-ttu-id="a8230-177">我提到，模型联编程序从值提供程序中获取值。</span><span class="sxs-lookup"><span data-stu-id="a8230-177">I mentioned that a model binder gets values from a value provider.</span></span> <span data-ttu-id="a8230-178">若要编写自定义值提供程序，请实现 **ivalueprovider 必需** 接口。</span><span class="sxs-lookup"><span data-stu-id="a8230-178">To write a custom value provider, implement the **IValueProvider** interface.</span></span> <span data-ttu-id="a8230-179">下面是从请求中的 cookie 拉取值的示例：</span><span class="sxs-lookup"><span data-stu-id="a8230-179">Here is an example that pulls values from the cookies in the request:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample14.cs)]

<span data-ttu-id="a8230-180">还需要通过从 **ValueProviderFactory** 类派生来创建值提供程序工厂。</span><span class="sxs-lookup"><span data-stu-id="a8230-180">You also need to create a value provider factory by deriving from the **ValueProviderFactory** class.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample15.cs)]

<span data-ttu-id="a8230-181">将值提供程序工厂添加到 **HttpConfiguration** ，如下所示。</span><span class="sxs-lookup"><span data-stu-id="a8230-181">Add the value provider factory to the **HttpConfiguration** as follows.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample16.cs)]

<span data-ttu-id="a8230-182">Web API 撰写了所有值提供程序，因此，当模型绑定器调用 **ValueProvider** 时，模型绑定器会从能够生成它的第一个值提供程序接收值。</span><span class="sxs-lookup"><span data-stu-id="a8230-182">Web API composes all of the value providers, so when a model binder calls **ValueProvider.GetValue**, the model binder receives the value from the first value provider that is able to produce it.</span></span>

<span data-ttu-id="a8230-183">或者，可以使用 **ValueProvider** 属性在参数级别设置值提供程序工厂，如下所示：</span><span class="sxs-lookup"><span data-stu-id="a8230-183">Alternatively, you can set the value provider factory at the parameter level by using the **ValueProvider** attribute, as follows:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample17.cs)]

<span data-ttu-id="a8230-184">这会告知 Web API 使用具有指定值提供程序工厂的模型绑定，而不是使用任何其他已注册的值提供程序。</span><span class="sxs-lookup"><span data-stu-id="a8230-184">This tells Web API to use model binding with the specified value provider factory, and not to use any of the other registered value providers.</span></span>

## <a name="httpparameterbinding"></a><span data-ttu-id="a8230-185">HttpParameterBinding</span><span class="sxs-lookup"><span data-stu-id="a8230-185">HttpParameterBinding</span></span>

<span data-ttu-id="a8230-186">模型联编是更为通用的机制的特定实例。</span><span class="sxs-lookup"><span data-stu-id="a8230-186">Model binders are a specific instance of a more general mechanism.</span></span> <span data-ttu-id="a8230-187">如果查看 **[ModelBinder]** 属性，您将看到它派生自 abstract **ParameterBindingAttribute** 类。</span><span class="sxs-lookup"><span data-stu-id="a8230-187">If you look at the **[ModelBinder]** attribute, you will see that it derives from the abstract **ParameterBindingAttribute** class.</span></span> <span data-ttu-id="a8230-188">此类定义了单一方法 **GetBinding**，该方法返回 **HttpParameterBinding** 对象：</span><span class="sxs-lookup"><span data-stu-id="a8230-188">This class defines a single method, **GetBinding**, which returns an **HttpParameterBinding** object:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample18.cs)]

<span data-ttu-id="a8230-189">**HttpParameterBinding** 负责将参数绑定到某个值。</span><span class="sxs-lookup"><span data-stu-id="a8230-189">An **HttpParameterBinding** is responsible for binding a parameter to a value.</span></span> <span data-ttu-id="a8230-190">对于 **[ModelBinder]**，该属性将返回一个 **HttpParameterBinding** 实现，该实现使用 **IModelBinder** 来执行实际绑定。</span><span class="sxs-lookup"><span data-stu-id="a8230-190">In the case of **[ModelBinder]**, the attribute returns an **HttpParameterBinding** implementation that uses an **IModelBinder** to perform the actual binding.</span></span> <span data-ttu-id="a8230-191">你还可以实现自己的 **HttpParameterBinding**。</span><span class="sxs-lookup"><span data-stu-id="a8230-191">You can also implement your own **HttpParameterBinding**.</span></span>

<span data-ttu-id="a8230-192">例如，假设要从请求中获取 Etag `if-match` 和 `if-none-match` 标头。</span><span class="sxs-lookup"><span data-stu-id="a8230-192">For example, suppose you want to get ETags from `if-match` and `if-none-match` headers in the request.</span></span> <span data-ttu-id="a8230-193">首先，我们将定义一个表示 Etag 的类。</span><span class="sxs-lookup"><span data-stu-id="a8230-193">We'll start by defining a class to represent ETags.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample19.cs)]

<span data-ttu-id="a8230-194">我们还将定义一个枚举，指示是否从 `if-match` 标头或 `if-none-match` 标头获取 ETag。</span><span class="sxs-lookup"><span data-stu-id="a8230-194">We'll also define an enumeration to indicate whether to get the ETag from the `if-match` header or the `if-none-match` header.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample20.cs)]

<span data-ttu-id="a8230-195">下面是一个 **HttpParameterBinding** ，它从所需的标头获取 ETag，并将其绑定到类型为 ETag 的参数：</span><span class="sxs-lookup"><span data-stu-id="a8230-195">Here is an **HttpParameterBinding** that gets the ETag from the desired header and binds it to a parameter of type ETag:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample21.cs)]

<span data-ttu-id="a8230-196">**ExecuteBindingAsync** 方法进行绑定。</span><span class="sxs-lookup"><span data-stu-id="a8230-196">The **ExecuteBindingAsync** method does the binding.</span></span> <span data-ttu-id="a8230-197">在此方法中，将绑定参数值添加到 **HttpActionContext** 中的 **ActionArgument** 字典中。</span><span class="sxs-lookup"><span data-stu-id="a8230-197">Within this method, add the bound parameter value to the **ActionArgument** dictionary in the **HttpActionContext**.</span></span>

> [!NOTE]
> <span data-ttu-id="a8230-198">如果 **ExecuteBindingAsync** 方法读取请求消息的正文，请重写 **WillReadBody** 属性以返回 true。</span><span class="sxs-lookup"><span data-stu-id="a8230-198">If your **ExecuteBindingAsync** method reads the body of the request message, override the **WillReadBody** property to return true.</span></span> <span data-ttu-id="a8230-199">请求正文可能是一次只能读取一次的未缓冲流，因此 Web API 强制执行最多一个绑定可以读取消息正文的规则。</span><span class="sxs-lookup"><span data-stu-id="a8230-199">The request body might be an unbuffered stream that can only be read once, so Web API enforces a rule that at most one binding can read the message body.</span></span>

<span data-ttu-id="a8230-200">若要应用自定义 **HttpParameterBinding**，可以定义派生自 **ParameterBindingAttribute** 的属性。</span><span class="sxs-lookup"><span data-stu-id="a8230-200">To apply a custom **HttpParameterBinding**, you can define an attribute that derives from **ParameterBindingAttribute**.</span></span> <span data-ttu-id="a8230-201">对于 `ETagParameterBinding` ，我们将定义两个属性，一个用于 `if-match` 标头，一个用于 `if-none-match` 标头。</span><span class="sxs-lookup"><span data-stu-id="a8230-201">For `ETagParameterBinding`, we'll define two attributes, one for `if-match` headers and one for `if-none-match` headers.</span></span> <span data-ttu-id="a8230-202">两者均派生自抽象基类。</span><span class="sxs-lookup"><span data-stu-id="a8230-202">Both derive from an abstract base class.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample22.cs)]

<span data-ttu-id="a8230-203">下面是使用属性的控制器方法 `[IfNoneMatch]` 。</span><span class="sxs-lookup"><span data-stu-id="a8230-203">Here is a controller method that uses the `[IfNoneMatch]` attribute.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample23.cs)]

<span data-ttu-id="a8230-204">除了 **ParameterBindingAttribute** 以外，还有另一个挂钩用于添加自定义 **HttpParameterBinding**。</span><span class="sxs-lookup"><span data-stu-id="a8230-204">Besides **ParameterBindingAttribute**, there is another hook for adding a custom **HttpParameterBinding**.</span></span> <span data-ttu-id="a8230-205">在 **HttpConfiguration** 对象上， **ParameterBindingRules** 属性是 (**HttpParameterDescriptor**  - &gt; **HttpParameterBinding**) 类型的匿名函数的集合。</span><span class="sxs-lookup"><span data-stu-id="a8230-205">On the **HttpConfiguration** object, the **ParameterBindingRules** property is a collection of anonymous functions of type (**HttpParameterDescriptor** -&gt; **HttpParameterBinding**).</span></span> <span data-ttu-id="a8230-206">例如，可以添加 GET 方法上的任何 ETag 参数使用 `ETagParameterBinding` 的规则 `if-none-match` ：</span><span class="sxs-lookup"><span data-stu-id="a8230-206">For example, you could add a rule that any ETag parameter on a GET method uses `ETagParameterBinding` with `if-none-match`:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample24.cs)]

<span data-ttu-id="a8230-207">`null`对于绑定不适用的参数，函数应返回。</span><span class="sxs-lookup"><span data-stu-id="a8230-207">The function should return `null` for parameters where the binding is not applicable.</span></span>

## <a name="iactionvaluebinder"></a><span data-ttu-id="a8230-208">IActionValueBinder</span><span class="sxs-lookup"><span data-stu-id="a8230-208">IActionValueBinder</span></span>

<span data-ttu-id="a8230-209">整个参数绑定过程由可插入服务 **IActionValueBinder** 控制。</span><span class="sxs-lookup"><span data-stu-id="a8230-209">The entire parameter-binding process is controlled by a pluggable service, **IActionValueBinder**.</span></span> <span data-ttu-id="a8230-210">**IActionValueBinder** 的默认实现执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="a8230-210">The default implementation of **IActionValueBinder** does the following:</span></span>

1. <span data-ttu-id="a8230-211">在参数上查找 **ParameterBindingAttribute** 。</span><span class="sxs-lookup"><span data-stu-id="a8230-211">Look for a **ParameterBindingAttribute** on the parameter.</span></span> <span data-ttu-id="a8230-212">这包括 **[FromBody]**、 **[FromUri]** 和 **[ModelBinder]** 或自定义属性。</span><span class="sxs-lookup"><span data-stu-id="a8230-212">This includes **[FromBody]**, **[FromUri]**, and **[ModelBinder]**, or custom attributes.</span></span>
2. <span data-ttu-id="a8230-213">否则，请在 **HttpConfiguration. ParameterBindingRules** 中查找返回非 null **HttpParameterBinding** 的函数。</span><span class="sxs-lookup"><span data-stu-id="a8230-213">Otherwise, look in **HttpConfiguration.ParameterBindingRules** for a function that returns a non-null **HttpParameterBinding**.</span></span>
3. <span data-ttu-id="a8230-214">否则，请使用前面介绍的默认规则。</span><span class="sxs-lookup"><span data-stu-id="a8230-214">Otherwise, use the default rules that I described previously.</span></span> 

    - <span data-ttu-id="a8230-215">如果参数类型为 "simple" 或具有类型转换器，请从 URI 进行绑定。</span><span class="sxs-lookup"><span data-stu-id="a8230-215">If the parameter type is "simple"or has a type converter, bind from the URI.</span></span> <span data-ttu-id="a8230-216">这等效于将 **[FromUri]** 特性置于参数上。</span><span class="sxs-lookup"><span data-stu-id="a8230-216">This is equivalent to putting the **[FromUri]** attribute on the parameter.</span></span>
    - <span data-ttu-id="a8230-217">否则，请尝试从消息正文读取参数。</span><span class="sxs-lookup"><span data-stu-id="a8230-217">Otherwise, try to read the parameter from the message body.</span></span> <span data-ttu-id="a8230-218">这等效于将 **[FromBody]** 放置在参数上。</span><span class="sxs-lookup"><span data-stu-id="a8230-218">This is equivalent to putting **[FromBody]** on the parameter.</span></span>

<span data-ttu-id="a8230-219">如果需要，可以将整个 **IActionValueBinder** 服务替换为自定义实现。</span><span class="sxs-lookup"><span data-stu-id="a8230-219">If you wanted, you could replace the entire **IActionValueBinder** service with a custom implementation.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a8230-220">其他资源</span><span class="sxs-lookup"><span data-stu-id="a8230-220">Additional Resources</span></span>

[<span data-ttu-id="a8230-221">自定义参数绑定示例</span><span class="sxs-lookup"><span data-stu-id="a8230-221">Custom Parameter Binding Sample</span></span>](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/CustomParameterBinding)

<span data-ttu-id="a8230-222">Mike 停止了撰写有关 Web API 参数绑定的一系列优秀博客文章：</span><span class="sxs-lookup"><span data-stu-id="a8230-222">Mike Stall wrote a good series of blog posts about Web API parameter binding:</span></span>

- [<span data-ttu-id="a8230-223">Web API 执行参数绑定的方式</span><span class="sxs-lookup"><span data-stu-id="a8230-223">How Web API does Parameter Binding</span></span>](https://blogs.msdn.com/b/jmstall/archive/2012/04/16/how-webapi-does-parameter-binding.aspx)
- [<span data-ttu-id="a8230-224">Web API 的 MVC 样式参数绑定</span><span class="sxs-lookup"><span data-stu-id="a8230-224">MVC Style parameter binding for Web API</span></span>](https://blogs.msdn.com/b/jmstall/archive/2012/04/18/mvc-style-parameter-binding-for-webapi.aspx)
- [<span data-ttu-id="a8230-225">如何绑定到 MVC/Web API 中的操作签名中的自定义对象</span><span class="sxs-lookup"><span data-stu-id="a8230-225">How to bind to custom objects in action signatures in MVC/Web API</span></span>](https://blogs.msdn.com/b/jmstall/archive/2012/04/20/how-to-bind-to-custom-objects-in-action-signatures-in-mvc-webapi.aspx)
- [<span data-ttu-id="a8230-226">如何在 Web API 中创建自定义值提供程序</span><span class="sxs-lookup"><span data-stu-id="a8230-226">How to create a custom value provider in Web API</span></span>](https://blogs.msdn.com/b/jmstall/archive/2012/04/23/how-to-create-a-custom-value-provider-in-webapi.aspx)
- [<span data-ttu-id="a8230-227">后台的 Web API 参数绑定</span><span class="sxs-lookup"><span data-stu-id="a8230-227">Web API Parameter binding under the hood</span></span>](https://blogs.msdn.com/b/jmstall/archive/2012/05/11/webapi-parameter-binding-under-the-hood.aspx)

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
# <a name="parameter-binding-in-aspnet-web-api"></a>ASP.NET Web API 中的参数绑定

作者： [Mike Wasson](https://github.com/MikeWasson)

[!INCLUDE[](~/includes/coreWebAPI.md)]

本文介绍了 Web API 如何绑定参数，以及如何自定义绑定过程。 当 Web API 在控制器上调用方法时，它必须设置参数的值，这是一个称为 " *绑定*" 的进程。

默认情况下，Web API 使用以下规则来绑定参数：

- 如果该参数为 "simple" 类型，则 Web API 会尝试从 URI 获取值。 简单类型包括 .NET [基元类型](https://msdn.microsoft.com/library/system.type.isprimitive.aspx) (**int**、 **bool**、 **double** 等) ，以及 **TimeSpan**、 **DateTime**、 **Guid**、 **decimal** 和 **string**，以及具有可从字符串转换的类型转换器 *的任何类型* 。 稍后 (有关类型转换器的详细信息。 ) 
- 对于复杂类型，Web API 会尝试使用 [媒体类型格式化程序](media-formatters.md)从消息正文中读取值。

例如，下面是典型的 Web API 控制器方法：

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample1.cs)]

*Id* 参数是 &quot; 简单 &quot; 类型，因此 Web API 会尝试从请求 URI 获取值。 *Item* 参数是复杂类型，因此 Web API 使用媒体类型格式化程序从请求正文中读取值。

为了从 URI 获取值，Web API 将查找路由数据和 URI 查询字符串。 当路由系统分析 URI 并将其与路由匹配时，将填充路由数据。 有关详细信息，请参阅 [路由和操作选择](../web-api-routing-and-actions/routing-and-action-selection.md)。

本文的其余部分将介绍如何自定义模型绑定过程。 但对于复杂类型，请考虑尽可能使用媒体类型格式化程序。 HTTP 的一项关键原则是，使用内容协商指定资源的表示形式，在消息正文中发送资源。 媒体类型格式化程序旨在实现此目的。

## <a name="using-fromuri"></a>使用 [FromUri]

若要强制 Web API 从 URI 读取复杂类型，请将 **[FromUri]** 特性添加到参数中。 下面的示例定义了一个 `GeoPoint` 类型以及从 URI 获取的控制器方法 `GeoPoint` 。

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample2.cs)]

客户端可以将纬度和经度值放在查询字符串中，Web API 将使用这些值来构造 `GeoPoint` 。 例如：

`http://localhost/api/values/?Latitude=47.678558&Longitude=-122.130989`

## <a name="using-frombody"></a>使用 [FromBody]

若要强制 Web API 从请求正文读取简单类型，请将 **[FromBody]** 特性添加到参数：

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample3.cs)]

在此示例中，Web API 将使用媒体类型格式化程序从请求正文中读取 *名称* 的值。 下面是一个示例客户端请求。

[!code-console[Main](parameter-binding-in-aspnet-web-api/samples/sample4.cmd)]

当参数具有 [FromBody] 时，Web API 使用 Content-type 标头来选择格式化程序。 在此示例中，内容类型为 &quot; application/json， &quot; 请求正文是原始 json 字符串 (不是) 的 json 对象。

最多允许一个参数读取消息正文。 这不起作用：

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample5.cs)]

此规则的原因是请求正文可能存储在只能读取一次的非缓冲流中。

## <a name="type-converters"></a>类型转换器

可以使 Web API 将某个类视为简单类型 (，以便 Web API 通过创建 **TypeConverter** 并提供字符串转换来尝试将其从 URI) 绑定。

下面的代码演示一个 `GeoPoint` 表示地理点的类，以及一个从字符串转换为实例的 TypeConverter `GeoPoint` 。 `GeoPoint`使用 **[TypeConverter]** 特性修饰类来指定类型转换器。  (此示例由 Mike 卡住的博客文章中的灵感， [如何绑定到 MVC/WebAPI 中的操作签名中的自定义对象](https://blogs.msdn.com/b/jmstall/archive/2012/04/20/how-to-bind-to-custom-objects-in-action-signatures-in-mvc-webapi.aspx)。 ) 

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample6.cs)]

现在，Web API 将 `GeoPoint` 作为简单类型处理，这意味着它将尝试 `GeoPoint` 从 URI 绑定参数。 不需要在参数上包含 **[FromUri]** 。

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample7.cs)]

客户端可以使用如下所示的 URI 调用方法：

`http://localhost/api/values/?location=47.678558,-122.130989`

## <a name="model-binders"></a>模型联编程序

比类型转换器更灵活的选项是创建自定义模型联编程序。 通过模型绑定器，你可以访问来自路由数据的 HTTP 请求、操作说明和原始值等项。

若要创建模型联编程序，请实现 **IModelBinder** 接口。 此接口定义单个方法 **BindModel**：

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample8.cs)]

下面是对象的模型联编程序 `GeoPoint` 。

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample9.cs)]

模型联编 *程序从值提供程序* 获取原始输入值。 此设计将两个不同的函数隔开：

- 值提供程序获取 HTTP 请求并填充键值对字典。
- 模型联编程序使用此字典填充模型。

Web API 中的默认值提供程序从路由数据和查询字符串中获取值。 例如，如果 URI 为 `http://localhost/api/values/1?location=48,-122` ，则值提供程序将创建以下键值对：

- id = &quot; 1&quot;
- location = &quot; 48，-122&quot;

 (我假设默认路由模板为 &quot; api/{controller}/{id} &quot; 。 ) 

要绑定的参数的名称存储在 **ModelBindingContext. ModelName** 属性中。 模型联编程序将在字典中查找具有此值的键。 如果该值存在并且可以转换为 `GeoPoint` ，则模型联编程序会将绑定值分配给 **ModelBindingContext** 属性。

请注意，模型绑定器并不局限于简单的类型转换。 在此示例中，模型绑定器首先查找已知位置表，如果失败，则使用类型转换。

**设置模型联编程序**

有多种方法可以设置模型联编程序。 首先，可以向参数添加 **[ModelBinder]** 特性。

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample10.cs)]

你还可以将 **[ModelBinder]** 特性添加到该类型。 Web API 将为该类型的所有参数使用指定的模型绑定器。

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample11.cs)]

最后，可以将模型联编程序提供程序添加到 **HttpConfiguration**。 模型联编程序提供程序只是创建模型联编程序的工厂类。 可以通过从 [ModelBinderProvider](https://msdn.microsoft.com/library/system.web.http.modelbinding.modelbinderprovider.aspx) 类派生来创建提供程序。 但是，如果您的模型绑定器处理单个类型，则使用内置的 **SimpleModelBinderProvider**（专为此目的而设计）会更容易。 下面的代码演示如何执行此操作。

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample12.cs)]

对于模型绑定提供程序，仍需要将 **[ModelBinder]** 特性添加到参数，以指示 Web API 应使用模型绑定器，而不是媒体类型格式化程序。 但现在无需在属性中指定模型绑定器的类型：

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample13.cs)]

## <a name="value-providers"></a>值提供程序

我提到，模型联编程序从值提供程序中获取值。 若要编写自定义值提供程序，请实现 **ivalueprovider 必需** 接口。 下面是从请求中的 cookie 拉取值的示例：

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample14.cs)]

还需要通过从 **ValueProviderFactory** 类派生来创建值提供程序工厂。

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample15.cs)]

将值提供程序工厂添加到 **HttpConfiguration** ，如下所示。

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample16.cs)]

Web API 撰写了所有值提供程序，因此，当模型绑定器调用 **ValueProvider** 时，模型绑定器会从能够生成它的第一个值提供程序接收值。

或者，可以使用 **ValueProvider** 属性在参数级别设置值提供程序工厂，如下所示：

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample17.cs)]

这会告知 Web API 使用具有指定值提供程序工厂的模型绑定，而不是使用任何其他已注册的值提供程序。

## <a name="httpparameterbinding"></a>HttpParameterBinding

模型联编是更为通用的机制的特定实例。 如果查看 **[ModelBinder]** 属性，您将看到它派生自 abstract **ParameterBindingAttribute** 类。 此类定义了单一方法 **GetBinding**，该方法返回 **HttpParameterBinding** 对象：

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample18.cs)]

**HttpParameterBinding** 负责将参数绑定到某个值。 对于 **[ModelBinder]**，该属性将返回一个 **HttpParameterBinding** 实现，该实现使用 **IModelBinder** 来执行实际绑定。 你还可以实现自己的 **HttpParameterBinding**。

例如，假设要从请求中获取 Etag `if-match` 和 `if-none-match` 标头。 首先，我们将定义一个表示 Etag 的类。

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample19.cs)]

我们还将定义一个枚举，指示是否从 `if-match` 标头或 `if-none-match` 标头获取 ETag。

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample20.cs)]

下面是一个 **HttpParameterBinding** ，它从所需的标头获取 ETag，并将其绑定到类型为 ETag 的参数：

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample21.cs)]

**ExecuteBindingAsync** 方法进行绑定。 在此方法中，将绑定参数值添加到 **HttpActionContext** 中的 **ActionArgument** 字典中。

> [!NOTE]
> 如果 **ExecuteBindingAsync** 方法读取请求消息的正文，请重写 **WillReadBody** 属性以返回 true。 请求正文可能是一次只能读取一次的未缓冲流，因此 Web API 强制执行最多一个绑定可以读取消息正文的规则。

若要应用自定义 **HttpParameterBinding**，可以定义派生自 **ParameterBindingAttribute** 的属性。 对于 `ETagParameterBinding` ，我们将定义两个属性，一个用于 `if-match` 标头，一个用于 `if-none-match` 标头。 两者均派生自抽象基类。

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample22.cs)]

下面是使用属性的控制器方法 `[IfNoneMatch]` 。

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample23.cs)]

除了 **ParameterBindingAttribute** 以外，还有另一个挂钩用于添加自定义 **HttpParameterBinding**。 在 **HttpConfiguration** 对象上， **ParameterBindingRules** 属性是 (**HttpParameterDescriptor**  - &gt; **HttpParameterBinding**) 类型的匿名函数的集合。 例如，可以添加 GET 方法上的任何 ETag 参数使用 `ETagParameterBinding` 的规则 `if-none-match` ：

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample24.cs)]

`null`对于绑定不适用的参数，函数应返回。

## <a name="iactionvaluebinder"></a>IActionValueBinder

整个参数绑定过程由可插入服务 **IActionValueBinder** 控制。 **IActionValueBinder** 的默认实现执行以下操作：

1. 在参数上查找 **ParameterBindingAttribute** 。 这包括 **[FromBody]**、 **[FromUri]** 和 **[ModelBinder]** 或自定义属性。
2. 否则，请在 **HttpConfiguration. ParameterBindingRules** 中查找返回非 null **HttpParameterBinding** 的函数。
3. 否则，请使用前面介绍的默认规则。 

    - 如果参数类型为 "simple" 或具有类型转换器，请从 URI 进行绑定。 这等效于将 **[FromUri]** 特性置于参数上。
    - 否则，请尝试从消息正文读取参数。 这等效于将 **[FromBody]** 放置在参数上。

如果需要，可以将整个 **IActionValueBinder** 服务替换为自定义实现。

## <a name="additional-resources"></a>其他资源

[自定义参数绑定示例](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/CustomParameterBinding)

Mike 停止了撰写有关 Web API 参数绑定的一系列优秀博客文章：

- [Web API 执行参数绑定的方式](https://blogs.msdn.com/b/jmstall/archive/2012/04/16/how-webapi-does-parameter-binding.aspx)
- [Web API 的 MVC 样式参数绑定](https://blogs.msdn.com/b/jmstall/archive/2012/04/18/mvc-style-parameter-binding-for-webapi.aspx)
- [如何绑定到 MVC/Web API 中的操作签名中的自定义对象](https://blogs.msdn.com/b/jmstall/archive/2012/04/20/how-to-bind-to-custom-objects-in-action-signatures-in-mvc-webapi.aspx)
- [如何在 Web API 中创建自定义值提供程序](https://blogs.msdn.com/b/jmstall/archive/2012/04/23/how-to-create-a-custom-value-provider-in-webapi.aspx)
- [后台的 Web API 参数绑定](https://blogs.msdn.com/b/jmstall/archive/2012/05/11/webapi-parameter-binding-under-the-hood.aspx)

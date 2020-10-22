---
uid: web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api
title: ASP.NET Web API 中的路由 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 10/29/2018
ms.assetid: 0675bdc7-282f-4f47-b7f3-7e02133940ca
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 85862c094cc54365267b1f21e68d235a15519cda
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345192"
---
# <a name="routing-in-aspnet-web-api"></a>Routing in ASP.NET Web API（在 ASP.NET Web API 中路由）

作者： [Mike Wasson](https://github.com/MikeWasson)

本文介绍 ASP.NET Web API 如何将 HTTP 请求路由到控制器。

> [!NOTE]
> 如果你熟悉 ASP.NET MVC，Web API 路由非常类似于 MVC 路由。 主要区别是 Web API 使用 HTTP 谓词（而非 URI 路径）来选择操作。 你还可以在 Web API 中使用 MVC 样式的路由。 本文不会假设 ASP.NET MVC 的任何知识。

## <a name="routing-tables"></a>路由表

在 ASP.NET Web API 中， *控制器* 是处理 HTTP 请求的类。 控制器的公共方法称为 *操作方法* 或简单的 *操作*。 当 Web API 框架收到请求时，它会将请求路由到某个操作。

为了确定要调用的操作，框架使用 *路由表*。 Web API 的 Visual Studio 项目模板创建默认路由：

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample1.cs)]

此路由是在 *WebApiConfig.cs* 文件中定义的，该文件放置在 *应用程序 \_ 启动* 目录中：

![](routing-in-aspnet-web-api/_static/image1.png)

有关类的详细信息 `WebApiConfig` ，请参阅 [配置 ASP.NET Web API](../advanced/configuring-aspnet-web-api.md)。

如果你自承载 Web API，则必须在对象上直接设置路由表 `HttpSelfHostConfiguration` 。 有关详细信息，请参阅 [自承载 WEB API](../older-versions/self-host-a-web-api.md)。

路由表中的每个条目都包含一个 *路由模板*。 Web API 的默认路由模板为 &quot; API/{controller}/{id} &quot; 。 在此模板中， &quot; api &quot; 是文本路径段，{controller} 和 {id} 是占位符变量。

当 Web API 框架收到 HTTP 请求时，它会尝试将 URI 与路由表中的某个路由模板匹配。 如果没有路由匹配，则客户端将收到404错误。 例如，以下 Uri 与默认路由匹配：

- /api/contacts
- /api/contacts/1
- /api/products/gizmo1

但是，以下 URI 不匹配，因为它缺少 &quot; api &quot; 段：

- /contacts/1

> [!NOTE]
> 在路由中使用 "api" 的原因是为了避免与 ASP.NET MVC 路由发生冲突。 这样一来，你就可以让 &quot; /contacts &quot; 转向 MVC 控制器， &quot; /Api/contacts 会 &quot; 转向 Web api 控制器。 当然，如果不喜欢此约定，可以更改默认路由表。

找到匹配的路由后，Web API 将选择控制器和操作：

- 若要查找控制器，Web API &quot; 需要将控制器添加 &quot; 到 *{controller}* 变量的值。
- 若要查找该操作，Web API 将查看 HTTP 谓词，然后查找名称以该 HTTP 谓词名称开头的操作。 例如，对于 GET 请求，Web API 将查找以 get 作为前缀的操作 &quot; &quot; ，如 &quot; GetContact &quot; 或 &quot; GetAllContacts &quot; 。 此约定仅适用于 GET、POST、PUT、DELETE、HEAD、OPTIONS 和 PATCH 动词。 可以通过使用控制器上的属性来启用其他 HTTP 谓词。 稍后我们将会看到一个示例。
- 路由模板中的其他占位符变量（如 *{id}* ）将映射到操作参数。

接下来举例说明。 假设您定义了以下控制器：

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample2.cs)]

下面是一些可能的 HTTP 请求，以及为每个请求调用的操作：

| HTTP 谓词 | URI 路径 | 操作 | 参数 |
| --- | --- | --- | --- |
| GET | api/产品 | GetAllProducts | * 无 () * |
| GET | api/产品/4 | GetProductById | 4 |
| DELETE | api/产品/4 | DeleteProduct | 4 |
| POST | api/产品 | * 不 (匹配) * |  |

请注意，URI 的 *{id}* 段（如果存在）映射到操作的 *id* 参数。 在此示例中，控制器定义了两个 GET 方法，一个带有 *id* 参数，另一个不包含参数。

另请注意，POST 请求将失败，因为控制器不定义 &quot; POST ... &quot; 方法。

## <a name="routing-variations"></a>路由变体

上一部分介绍了 ASP.NET Web API 的基本路由机制。 本部分介绍一些变化形式。

### <a name="http-verbs"></a>HTTP 谓词

可以通过使用以下属性之一来修饰操作方法，以显式指定操作的 HTTP 谓词，而不是使用 HTTP 谓词的命名约定：

- `[HttpGet]`
- `[HttpPut]`
- `[HttpPost]`
- `[HttpDelete]`
- `[HttpHead]`
- `[HttpOptions]`
- `[HttpPatch]`

在下面的示例中， `FindProduct` 方法映射到 GET 请求：

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample3.cs)]

若要允许操作使用多个 HTTP 谓词，或允许除 GET、PUT、POST、DELETE、HEAD、OPTIONS 和 PATCH 之外的 HTTP 谓词，请使用 `[AcceptVerbs]` 属性，该属性采用 HTTP 谓词的列表。

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample4.cs)]

<a id="routing_by_action_name"></a>
### <a name="routing-by-action-name"></a>按操作名称路由

使用默认路由模板，Web API 使用 HTTP 谓词来选择操作。 但是，你还可以创建一个在 URI 中包含操作名称的路由：

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample5.cs)]

在此路由模板中， *{action}* 参数在控制器上命名操作方法。 使用这种形式的路由，请使用属性指定允许的 HTTP 谓词。 例如，假设控制器具有以下方法：

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample6.cs)]

在这种情况下，"api/products/details/1" 的 GET 请求会映射到 `Details` 方法。 这种形式的路由类似于 ASP.NET MVC，可能适用于 RPC 样式的 API。

您可以使用属性重写操作名称 `[ActionName]` 。 在下面的示例中，有两个映射到 &quot; api/产品/缩略图/*id*的操作。一个支持 GET，另一个支持 POST：

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample7.cs)]

### <a name="non-actions"></a>非操作

若要防止方法被调用为操作，请使用 `[NonAction]` 特性。 这会向框架发出信号，指示该方法不是一个操作，即使它将与路由规则匹配也是如此。

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample8.cs)]

## <a name="further-reading"></a>深入阅读

本主题提供了路由的概要视图。 有关更多详细信息，请参阅 [路由和操作选择](routing-and-action-selection.md)，其中准确描述了框架如何将 URI 与路由匹配，选择控制器，然后选择要调用的操作。

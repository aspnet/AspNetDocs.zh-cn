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
# <a name="routing-in-aspnet-web-api"></a>Routing in ASP.NET Web API（在 ASP.NET Web API 中路由）

由[迈克·瓦森](https://github.com/MikeWasson)

本文介绍ASP.NET Web API 如何将 HTTP 请求路由到控制器。

> [!NOTE]
> 如果您熟悉ASP.NET MVC，则 Web API 路由与 MVC 路由非常相似。 主要区别是 Web API 使用 HTTP 谓词（而不是 URI 路径）来选择操作。 您还可以在 Web API 中使用 MVC 样式路由。 本文不假定任何有关ASP.NET MVC 的知识。

## <a name="routing-tables"></a>路由表

在 Web API ASP.NET，*控制器*是处理 HTTP 请求的类。 控制器的公共方法称为*操作方法*或简单的*操作*。 当 Web API 框架收到请求时，它将请求路由到操作。

要确定要调用的操作，框架使用*路由表*。 Web API 的可视化工作室项目模板创建默认路由：

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample1.cs)]

此路由在*WebApiConfig.cs*文件中定义，该文件放置在 *"\_应用开始"* 目录中：

![](routing-in-aspnet-web-api/_static/image1.png)

有关该类的详细信息，`WebApiConfig`请参阅[配置ASP.NET Web API](../advanced/configuring-aspnet-web-api.md)。

如果自承载 Web API，则必须直接在`HttpSelfHostConfiguration`对象上设置路由表。 有关详细信息，请参阅[自主机 Web API](../older-versions/self-host-a-web-api.md)。

路由表中的每个条目都包含*一个路由模板*。 Web API 的默认路由模板&quot;是 api/{控制器}/{id}。&quot; 在此模板中&quot;，api&quot;是文本路径段，[控制器] 和 {id} 是占位符变量。

当 Web API 框架收到 HTTP 请求时，它会尝试将 URI 与路由表中的路由模板之一匹配。 如果没有路由匹配，客户端将收到 404 错误。 例如，以下 URI 与默认路由匹配：

- /api/触点
- /api/触点/1
- /api/产品/gizmo1

但是，以下 URI 不匹配，因为它缺少&quot;api&quot;段：

- /触点/1

> [!NOTE]
> 在路由中使用"api"的原因是为了避免与ASP.NET MVC 路由发生冲突。 这样&quot;，您可以让 /联系人&quot;转到 MVC 控制器，/api/&quot;联系人&quot;转到 Web API 控制器。 当然，如果您不喜欢此约定，则可以更改默认路由表。

找到匹配路由后，Web API 将选择控制器和操作：

- 要查找控制器，Web API&quot;将&quot;控制器添加到 *[控制器]* 变量的值。
- 要查找操作，Web API 将查看 HTTP 谓词，然后查找名称以该 HTTP 谓词名称开头的操作。 例如，对于 GET 请求，Web &quot;API 会查找使用 Get&quot;预置的操作&quot;，例如&quot;获取&quot;联系人或获取&quot;所有联系人。 此约定仅适用于 GET、POST、PUT、DELETE、头、选项和 PATCH 谓词。 您可以使用控制器上的属性启用其他 HTTP 谓词。 稍后我们将看到示例。
- 工艺路线模板中的其他占位符变量（如 *{id}）* 映射到操作参数。

接下来举例说明。 假设您定义了以下控制器：

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample2.cs)]

下面是一些可能的 HTTP 请求，以及为每个请求调用的操作：

| HTTP 谓词 | URI 路径 | 操作 | 参数 |
| --- | --- | --- | --- |
| GET | api/产品 | 获取所有产品 | *（无）* |
| GET | api/产品/4 | 获取产品 ById | 4 |
| DELETE | api/产品/4 | 删除产品 | 4 |
| POST | api/产品 | *（不匹配）* |  |

请注意，URI 的 *[id]* 段（如果存在）映射到操作的*id*参数。 在此示例中，控制器定义了两个 GET 方法，一个使用*id*参数，另一个没有参数。

此外，请注意，POST 请求将失败，因为控制器未定义&quot;Post...&quot;方法。

## <a name="routing-variations"></a>路由变体

上一节介绍了ASP.NET Web API 的基本路由机制。 本节介绍一些变体。

### <a name="http-verbs"></a>HTTP 谓词

无需对 HTTP 谓词使用命名约定，还可以通过使用以下属性之一来修饰操作方法之一，显式指定操作的 HTTP 谓词：

- `[HttpGet]`
- `[HttpPut]`
- `[HttpPost]`
- `[HttpDelete]`
- `[HttpHead]`
- `[HttpOptions]`
- `[HttpPatch]`

在下面的示例中，`FindProduct`该方法映射到 GET 请求：

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample3.cs)]

要允许多个 HTTP 谓词用于某个操作，或允许除 GET、PUT、POST、DELETE、HEAD、OPTIONS 和 PATCH 以外的 HTTP`[AcceptVerbs]`谓词，请使用该属性，该属性采用 HTTP 谓词的列表。

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample4.cs)]

<a id="routing_by_action_name"></a>
### <a name="routing-by-action-name"></a>按操作名称路由

使用默认路由模板，Web API 使用 HTTP 谓词选择操作。 但是，您还可以创建一个路由，其中操作名称包含在 URI 中：

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample5.cs)]

在此路由模板中 *，[操作]* 参数在控制器上命名操作方法。 使用此路由样式，使用属性指定允许的 HTTP 谓词。 例如，假设您的控制器具有以下方法：

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample6.cs)]

在这种情况下，GET 请求的"api/产品/详细信息/1"将映射到`Details`该方法。 这种路由样式类似于 mVC ASP.NET，可能适用于 RPC 样式的 API。

可以使用 属性重写操作名称`[ActionName]`。 在下面的示例中，有两个操作映射到&quot;api/产品/缩略图/*id*。一个支持 GET，另一个支持 POST：

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample7.cs)]

### <a name="non-actions"></a>非操作

要防止将方法作为操作调用，请使用 属性`[NonAction]`。 这向框架发出信号，说明该方法不是操作，即使它以其他方式与路由规则匹配也是如此。

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample8.cs)]

## <a name="further-reading"></a>延伸阅读

本主题提供了路由的高级视图。 有关详细信息，请参阅[路由和操作选择](routing-and-action-selection.md)，它准确描述框架如何将 URI 与路由匹配，选择控制器，然后选择要调用的操作。

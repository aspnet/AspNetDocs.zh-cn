---
uid: web-api/overview/getting-started-with-aspnet-web-api/action-results
title: 操作会导致 Web API 2 的 ASP.NET 4.x
author: MikeWasson
description: 描述如何 ASP.NET Web API 将返回值转换到 ASP.NET 中的 HTTP 响应消息的控制器操作从 4.x。
ms.author: riande
ms.date: 02/03/2014
ms.custom: seoapril2019
ms.assetid: 2fc4797c-38ef-4cc7-926c-ca431c4739e8
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/action-results
msc.type: authoredcontent
ms.openlocfilehash: 87f71938a5c5f38d3a456ba9339540f67e236e1a
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/09/2019
ms.locfileid: "59400888"
---
# <a name="action-results-in-web-api-2"></a>Web API 2 的操作结果

通过[Mike Wasson](https://github.com/MikeWasson)

本主题介绍如何 ASP.NET Web API 都将转换为 HTTP 响应消息的控制器操作的返回值。

Web API 控制器操作可以返回以下任一项：

1. void
2. **HttpResponseMessage**
3. **IHttpActionResult**
4. 某些其他类型

具体取决于以下哪种返回时，Web API 使用另一种机制来创建 HTTP 响应。

| 返回类型 | Web API 创建响应的方式 |
| --- | --- |
| void | 返回空 204 （无内容） |
| **HttpResponseMessage** | 转换为直接 HTTP 响应消息。 |
| **IHttpActionResult** | 调用**ExecuteAsync**来创建**HttpResponseMessage**，然后将转换为 HTTP 响应消息。 |
| 其他类型 | 将序列化的返回值写入到响应正文中;返回 200 （正常）。 |

本主题的其余部分将介绍更多详细信息中的每个选项。

## <a name="void"></a>void

如果返回类型为`void`，Web API 仅返回状态代码 204 （无内容） 的空 HTTP 响应。

示例控制器：

[!code-csharp[Main](action-results/samples/sample1.cs)]

HTTP 响应：

[!code-console[Main](action-results/samples/sample2.cmd)]

## <a name="httpresponsemessage"></a>HttpResponseMessage

如果操作返回[HttpResponseMessage](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.aspx)，Web API 的返回值直接将转换为 HTTP 响应消息中，使用的属性**HttpResponseMessage**要填充对象响应。

此选项可提供大量控制的响应消息。 例如，以下控制器操作设置的缓存控制标头。

[!code-csharp[Main](action-results/samples/sample3.cs)]

响应：

[!code-console[Main](action-results/samples/sample4.cmd?highlight=2)]

如果传递到的域模型**CreateResponse**方法中，Web API 使用[媒体格式化程序](../formats-and-model-binding/media-formatters.md)将写入响应正文的序列化的模型。

[!code-csharp[Main](action-results/samples/sample5.cs)]

Web API 使用 Accept 标头中请求选择格式化程序。 有关详细信息，请参阅[内容协商](../formats-and-model-binding/content-negotiation.md)。

## <a name="ihttpactionresult"></a>IHttpActionResult

**IHttpActionResult** Web API 2 中引入了接口。 从根本上来说，它定义**HttpResponseMessage**工厂。 以下是使用的一些优势**IHttpActionResult**接口：

- 可简化[单元测试](../testing-and-debugging/unit-testing-controllers-in-web-api.md)你的控制器。
- 将移动到单独的类创建 HTTP 响应的常见逻辑。
- 隐藏构造响应的低级别的详细信息，从而使更清晰，控制器操作的目的。

**IHttpActionResult**包含一个方法**ExecuteAsync**，以便以异步方式创建**HttpResponseMessage**实例。

[!code-csharp[Main](action-results/samples/sample6.cs)]

如果控制器操作返回**IHttpActionResult**，Web API 调用**ExecuteAsync**方法创建**HttpResponseMessage**。 然后它会将转换**HttpResponseMessage**到 HTTP 响应消息。

下面是一个简单的实现**IHttpActionResult**创建纯文本响应：

[!code-csharp[Main](action-results/samples/sample7.cs)]

示例控制器操作：

[!code-csharp[Main](action-results/samples/sample8.cs)]

响应：

[!code-console[Main](action-results/samples/sample9.cmd)]

更多时候，您将使用**IHttpActionResult**中定义的实现**[System.Web.Http.Results](https://msdn.microsoft.com/library/system.web.http.results.aspx)** 命名空间。 **ApiController**类定义返回这些内置操作结果的帮助程序方法。

在以下示例中，如果请求不匹配现有的产品 ID，在控制器调用[ApiController.NotFound](https://msdn.microsoft.com/library/system.web.http.apicontroller.notfound.aspx)创建 404 （未找到） 响应。 否则，控制器会调用[ApiController.OK](https://msdn.microsoft.com/library/dn314591.aspx)，用于创建 200 （正常） 响应，包含该产品。

[!code-csharp[Main](action-results/samples/sample10.cs)]

## <a name="other-return-types"></a>其他的返回类型

对于所有其他返回类型，Web API 使用[媒体格式化程序](../formats-and-model-binding/media-formatters.md)要序列化的返回值。 Web API 将序列化的值写入到响应正文。 响应状态代码为 200 （正常）。

[!code-csharp[Main](action-results/samples/sample11.cs)]

此方法的缺点是，不能直接返回错误代码，如 404。 但是，您可能会引发**HttpResponseException**的错误代码。 有关详细信息，请参阅[ASP.NET Web API 中的异常处理](../error-handling/exception-handling.md)。

Web API 使用 Accept 标头中请求选择格式化程序。 有关详细信息，请参阅[内容协商](../formats-and-model-binding/content-negotiation.md)。

示例请求

[!code-console[Main](action-results/samples/sample12.cmd)]

示例响应：

[!code-console[Main](action-results/samples/sample13.cmd)]

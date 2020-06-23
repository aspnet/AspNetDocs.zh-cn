---
uid: web-api/overview/testing-and-debugging/unit-testing-controllers-in-web-api
title: ASP.NET Web API 2 中的单元测试控制器 |Microsoft Docs
author: MikeWasson
description: 本主题介绍了 Web API 2 中的单元测试控制器的一些特定技术。 阅读本主题之前，您可能需要阅读教程单元 .。。
ms.author: riande
ms.date: 06/11/2014
ms.assetid: 43a6cce7-a3ef-42aa-ad06-90d36d49f098
msc.legacyurl: /web-api/overview/testing-and-debugging/unit-testing-controllers-in-web-api
msc.type: authoredcontent
ms.openlocfilehash: ee933cfc736a07b91c8f7feea2c4a2c64d200942
ms.sourcegitcommit: 0cf7d06071a8ff986e6c028ac9daf0c0e7490412
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/23/2020
ms.locfileid: "85240660"
---
# <a name="unit-testing-controllers-in-aspnet-web-api-2"></a>ASP.NET Web API 2 中的单元测试控制器

作者： [Mike Wasson](https://github.com/MikeWasson)

> 本主题介绍了 Web API 2 中的单元测试控制器的一些特定技术。 阅读本主题之前，您可能需要阅读教程[单元测试 ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md)，其中演示了如何将单元测试项目添加到您的解决方案中。
>
> ## <a name="software-versions-used-in-the-tutorial"></a>本教程中使用的软件版本
>
> - [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
> - Web API 2
> - [Moq](https://github.com/Moq) 4.5.30

> [!NOTE]
> 我使用的是 Moq，但也适用于任何模拟框架。 Moq 4.5.30 （及更高版本）支持 Visual Studio 2017、Roslyn 和 .NET 4.5 及更高版本。

单元测试中的一种常见模式是 "按操作 &quot; 断言" &quot; ：

- 排列：为要运行的测试设置任何先决条件。
- Act：执行测试。
- 断言：验证测试是否成功。

在 "排列" 步骤中，您将经常使用 mock 或存根对象。 这可最大程度地减少依赖项的数量，因此，测试重点在于测试一项内容。

下面是一些应在 Web API 控制器中进行单元测试的事项：

- 操作返回正确类型的响应。
- 无效参数返回正确的错误响应。
- 操作对存储库或服务层调用正确的方法。
- 如果响应包含域模型，请验证模型类型。

下面是一些要测试的一般内容，具体取决于控制器实现情况。 具体来说，无论控制器操作返回**HttpResponseMessage**还是**IHttpActionResult**，它都有很大的区别。 有关这些结果类型的详细信息，请参阅[Web Api 2 中的操作结果](../getting-started-with-aspnet-web-api/action-results.md)。

## <a name="testing-actions-that-return-httpresponsemessage"></a>返回 HttpResponseMessage 的测试操作

下面是其操作返回**HttpResponseMessage**的控制器的示例。

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample1.cs)]

请注意，控制器使用依赖关系注入来注入 `IProductRepository` 。 这会使控制器更具可测试性，因为你可以注入 mock 存储库。 下面的单元测试将验证方法是否将 `Get` 写入 `Product` 响应正文。 假设 `repository` 是模拟 `IProductRepository` 。

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample2.cs)]

必须在控制器上设置**请求**和**配置**。 否则，测试将失败，并出现**system.argumentnullexception**或**InvalidOperationException**。

## <a name="testing-link-generation"></a>测试链接生成

`Post`方法调用**UrlHelper**以在响应中创建链接。 这需要在单元测试中进行更多的设置：

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample3.cs)]

**UrlHelper**类需要请求 URL 和路由数据，因此测试必须为这些值设置值。 另一种方法是 mock 或存根**UrlHelper**。 使用此方法时，请将[ApiController](https://msdn.microsoft.com/library/system.web.http.apicontroller.url.aspx)的默认值替换为返回固定值的 mock 或存根版本。

让我们使用[Moq](https://github.com/Moq)框架重写测试。 `Moq`在测试项目中安装 NuGet 包。

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample4.cs)]

在此版本中，无需设置任何路由数据，因为模拟**UrlHelper**返回常量字符串。

## <a name="testing-actions-that-return-ihttpactionresult"></a>返回 IHttpActionResult 的测试操作

在 Web API 2 中，控制器操作可以返回**IHttpActionResult**，这类似于 ASP.NET MVC 中的**ActionResult** 。 **IHttpActionResult**接口定义用于创建 HTTP 响应的命令模式。 控制器返回**IHttpActionResult**，而不是直接创建响应。 稍后，管道将调用**IHttpActionResult**来创建响应。 这种方法可以更轻松地编写单元测试，因为可以跳过**HttpResponseMessage**所需的大量设置。

下面是一个示例控制器，其操作返回**IHttpActionResult**。

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample5.cs)]

此示例显示了使用**IHttpActionResult**的一些常用模式。 让我们看看如何对它们进行单元测试。

### <a name="action-returns-200-ok-with-a-response-body"></a>操作返回200（正常），其中包含响应正文

`Get`如果找到该产品，则方法将调用 `Ok(product)` 。 在单元测试中，确保返回类型为**OkNegotiatedContentResult** ，并且返回的产品具有正确的 ID。

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample6.cs)]

请注意，单元测试不执行操作结果。 可以假设操作结果正确地创建 HTTP 响应。 （这就是 Web API 框架有自己的单元测试的原因！）

### <a name="action-returns-404-not-found"></a>操作返回404（未找到）

`Get`如果找不到该产品，则方法将调用 `NotFound()` 。 在这种情况下，单元测试仅检查返回类型是否为**NotFoundResult**。

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample7.cs)]

### <a name="action-returns-200-ok-with-no-response-body"></a>操作返回200（正常），没有响应正文

`Delete`方法调用 `Ok()` 来返回空的 HTTP 200 响应。 与前面的示例一样，单元测试检查返回类型，在本例中为**OkResult**。

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample8.cs)]

### <a name="action-returns-201-created-with-a-location-header"></a>操作返回带有 Location 标头的201（已创建）

`Post`方法调用 `CreatedAtRoute` 以返回带有 Location 标头中的 URI 的 HTTP 201 响应。 在单元测试中，验证操作是否设置了正确的路由值。

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample9.cs)]

### <a name="action-returns-another-2xx-with-a-response-body"></a>操作返回包含响应正文的另一个2xx

`Put`方法调用 `Content` 以返回带有响应正文的 HTTP 202 （可接受）响应。 这种情况类似于返回200（正常），但单元测试还应检查状态代码。

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample10.cs)]

## <a name="additional-resources"></a>其他资源

- [单元测试 ASP.NET Web API 2 时的模拟实体框架](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md)
- [为 ASP.NET Web API 服务编写测试](https://docs.microsoft.com/archive/blogs/youssefm/writing-tests-for-an-asp-net-web-api-service)（Youssef Moussaoui 的博客文章）。
- [Debugging ASP.NET Web API with Route Debugger（使用路由调试器调试 ASP.NET Web API）](https://blogs.msdn.com/b/webdev/archive/2013/04/04/debugging-asp-net-web-api-with-route-debugger.aspx)

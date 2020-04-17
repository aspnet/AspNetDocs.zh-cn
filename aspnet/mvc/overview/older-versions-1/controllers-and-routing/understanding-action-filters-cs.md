---
uid: mvc/overview/older-versions-1/controllers-and-routing/understanding-action-filters-cs
title: 了解操作筛选器 （C#） |微软文档
author: rick-anderson
description: 本教程的目的是解释操作筛选器。 操作筛选器是一个属性，您可以应用于控制器操作或整个控制器...
ms.author: riande
ms.date: 10/16/2008
ms.assetid: a94e4e81-40c1-47b7-8613-126a1a6cc93d
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/understanding-action-filters-cs
msc.type: authoredcontent
ms.openlocfilehash: 75ba7b1dce280a45cd092de97c464eade5f49838
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542178"
---
# <a name="understanding-action-filters-c"></a>了解操作筛选器 (C#)

由[微软](https://github.com/microsoft)

[下载 PDF](https://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_14_CS.pdf)

> 本教程的目的是解释操作筛选器。 操作筛选器是一个属性，您可以应用于控制器操作（或整个控制器），该属性修改操作的执行方式。

## <a name="understanding-action-filters"></a>了解操作筛选器

本教程的目的是解释操作筛选器。 操作筛选器是一个属性，您可以应用于控制器操作（或整个控制器），该属性修改操作的执行方式。 ASP.NET MVC 框架包括多个操作筛选器：

- 输出缓存 - 此操作筛选器缓存控制器操作的输出，以指定的时间进行。
- 句柄错误 - 此操作筛选器处理执行控制器操作时引发的错误。
- 授权 – 此操作筛选器使您能够限制对特定用户或角色的访问。

您还可以创建自己的自定义操作筛选器。 例如，您可能希望创建自定义操作筛选器以实现自定义身份验证系统。 或者，您可能希望创建一个操作筛选器，用于修改控制器操作返回的视图数据。

在本教程中，您将了解如何从开始构建操作筛选器。 我们创建一个 Log 操作筛选器，将操作处理的不同阶段记录到可视化工作室输出窗口。

### <a name="using-an-action-filter"></a>使用操作筛选器

操作筛选器是属性。 您可以将大多数操作筛选器应用于单个控制器操作或整个控制器。

例如，清单 1 中的数据控制器公开名为`Index()`返回当前时间的操作。 此操作使用`OutputCache`操作筛选器进行修饰。 此筛选器会导致将操作返回的值缓存 10 秒。

**清单1 |`Controllers\DataController.cs`**

[!code-csharp[Main](understanding-action-filters-cs/samples/sample1.cs)]

如果通过将 URL/`Index()`数据/索引输入浏览器的地址栏并多次点击"刷新"按钮来重复调用该操作，则您将在 10 秒内看到相同的时间。 操作的`Index()`输出缓存 10 秒（参见图 1）。

[![缓存时间](understanding-action-filters-cs/_static/image2.png)](understanding-action-filters-cs/_static/image1.png)

**图 01**： 缓存时间 （[单击以查看全尺寸图像](understanding-action-filters-cs/_static/image3.png)）

在清单 1 中，单个操作筛选器`OutputCache`（操作筛选器）应用于`Index()`该方法。 如果需要，可以将多个操作筛选器应用于同一操作。 例如，您可能希望将 和`OutputCache``HandleError`操作筛选器应用于同一操作。

在清单 1`OutputCache`中，操作筛选器应用于操作`Index()`。 您还可以将此属性应用于`DataController`类本身。 在这种情况下，控制器公开的任何操作返回的结果将被缓存 10 秒。

### <a name="the-different-types-of-filters"></a>不同类型的过滤器

ASP.NET MVC 框架支持四种不同类型的筛选器：

1. 授权筛选器 = 实现`IAuthorizationFilter`属性。
2. 操作筛选器 = 实现`IActionFilter`属性。
3. 结果筛选器 = 实现`IResultFilter`属性。
4. 异常筛选器 = 实现`IExceptionFilter`属性。

筛选器按上面列出的顺序执行。 例如，授权筛选器始终在操作筛选器和异常筛选器始终在每一种其他类型的筛选器之后执行。

授权筛选器用于实现控制器操作的身份验证和授权。 例如，"授权"筛选器是授权筛选器的示例。

操作筛选器包含在控制器操作执行之前和之后执行的逻辑。 例如，可以使用操作筛选器修改控制器操作返回的视图数据。

结果筛选器包含在执行视图结果之前和之后执行的逻辑。 例如，您可能希望在视图呈现给浏览器之前修改视图结果。

异常筛选器是要运行的最后一种筛选器类型。 可以使用异常筛选器来处理控制器操作或控制器操作结果引发的错误。 您还可以使用异常筛选器来记录错误。

每种不同类型的筛选器都按特定顺序执行。 如果要控制执行相同类型的筛选器的顺序，则可以设置筛选器的 Order 属性。

所有操作筛选器的基类是类`System.Web.Mvc.FilterAttribute`。 如果要实现特定类型的筛选器，则需要创建从基本筛选器类继承的类，并实现一个或多个`IAuthorizationFilter`、 `IActionFilter`、或`IResultFilter``IExceptionFilter`接口。

### <a name="the-base-actionfilterattribute-class"></a>基本操作筛选器属性类

为了更轻松地实现自定义操作筛选器，ASP.NET MVC 框架包括一`ActionFilterAttribute`个基本类。 此类实现 和`IActionFilter``IResultFilter`接口并从`Filter`类继承。

此处的术语并不完全一致。 从技术上讲，从 ActionFilterAttribute 类继承的类既是操作筛选器，也是结果筛选器。 但是，在松散的意义上，单词操作筛选器用于引用 mVC 框架中的任何类型的筛选器ASP.NET。

基`ActionFilterAttribute`类具有您可以重写的以下方法：

- OnAction 执行 – 在执行控制器操作之前调用此方法。
- 执行执行时 - 在执行控制器操作后调用此方法。
- OnResult 执行 – 在执行控制器操作结果之前调用此方法。
- OnResult 执行 - 在执行控制器操作结果后调用此方法。

在下一节中，我们将了解如何实现每种不同方法。

### <a name="creating-a-log-action-filter"></a>创建日志操作筛选器

为了说明如何构建自定义操作筛选器，我们将创建一个自定义操作筛选器，将处理控制器操作的各个阶段记录到 Visual Studio 输出窗口。 我们的`LogActionFilter`包含在清单2中。

**清单2 |`ActionFilters\LogActionFilter.cs`**

[!code-csharp[Main](understanding-action-filters-cs/samples/sample2.cs)]

在清单 2`OnActionExecuting()`中`OnActionExecuted()``OnResultExecuting()`，、、`OnResultExecuted()`和 方法都`Log()`调用 方法。 方法的名称和当前路由数据将传递给 方法`Log()`。 该方法`Log()`将消息写入可视化工作室输出窗口（参见图 2）。

[![写入可视化工作室输出窗口](understanding-action-filters-cs/_static/image5.png)](understanding-action-filters-cs/_static/image4.png)

**图 02**： 写入可视化工作室输出窗口 （[单击以查看全尺寸图像](understanding-action-filters-cs/_static/image6.png)）

清单3中的主控制器说明了如何将 Log 操作筛选器应用于整个控制器类。 每当调用主控制器公开的任何操作（`Index()`方法或`About()`方法），处理操作的各个阶段都会记录到 Visual Studio 输出窗口。

**清单3 |`Controllers\HomeController.cs`**

[!code-csharp[Main](understanding-action-filters-cs/samples/sample3.cs)]

### <a name="summary"></a>总结

在本教程中，您将被介绍到ASP.NET MVC 操作筛选器。 您了解了四种不同类型的筛选器：授权筛选器、操作筛选器、结果筛选器和异常筛选器。 您还了解了基`ActionFilterAttribute`类。

最后，您学习了如何实现简单的操作筛选器。 我们创建了一个 Log 操作筛选器，将处理控制器操作的各个阶段记录到可视化工作室输出窗口。

> [!div class="step-by-step"]
> [上一页](asp-net-mvc-routing-overview-cs.md)
> [下一页](improving-performance-with-output-caching-cs.md)

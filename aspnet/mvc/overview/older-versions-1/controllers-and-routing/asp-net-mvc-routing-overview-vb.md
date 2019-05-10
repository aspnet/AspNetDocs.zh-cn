---
uid: mvc/overview/older-versions-1/controllers-and-routing/asp-net-mvc-routing-overview-vb
title: ASP.NET MVC 路由概述 (VB) |Microsoft Docs
author: StephenWalther
description: 在本教程中，Stephen Walther 显示 ASP.NET MVC 框架将浏览器请求映射到控制器操作的方式。
ms.author: riande
ms.date: 08/19/2008
ms.assetid: 4bc8d19a-80f1-44b4-adbf-95ed22d691ca
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/asp-net-mvc-routing-overview-vb
msc.type: authoredcontent
ms.openlocfilehash: ed043d76b89ce31945cf3423b0c5afca9383cc21
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/06/2019
ms.locfileid: "65123648"
---
# <a name="aspnet-mvc-routing-overview-vb"></a>ASP.NET MVC 路由概述 (VB)

通过[Stephen Walther](https://github.com/StephenWalther)

> 在本教程中，Stephen Walther 显示 ASP.NET MVC 框架将浏览器请求映射到控制器操作的方式。

在本教程中，为您介绍了名为每个 ASP.NET MVC 应用程序的一个重要特性*ASP.NET 路由*。 ASP.NET 路由模块负责将传入的浏览器请求映射到特定的 MVC 控制器操作。 本教程结束时，你将了解如何在标准的路由表将请求映射到控制器操作。

## <a name="using-the-default-route-table"></a>使用默认路由表

在创建新的 ASP.NET MVC 应用程序时，应用程序已配置为使用 ASP.NET 路由。 ASP.NET 路由是在两个位置设置的。

首先，应用程序的 Web 配置文件（Web.config 文件）启用了 ASP.NET 路由。 配置文件中有四个部分与路由相关：system.web.httpModules 节、system.web.httpHandlers 节、system.webserver.modules 节和 system.webserver.handlers 节。 请注意不要删除这些节，因为如果没有这些节，路由将不再起作用。

其次，更重要的是，路由表是在应用程序的 Global.asax 文件中创建的。 Global.asax 文件是一个特殊文件，其中包含 ASP.NET 应用程序生命周期事件的事件处理程序。 路由表在 Application Start 事件中创建。

在列表 1 中的文件包含为 ASP.NET MVC 应用程序的默认 Global.asax 文件。

**Listing 1 - Global.asax.vb**

[!code-vb[Main](asp-net-mvc-routing-overview-vb/samples/sample1.vb)]

MVC 应用程序第一次启动时，会调用 Application\_Start() 方法。 此方法反过来会调用 RegisterRoutes() 方法。 RegisterRoutes() 方法负责创建路由表。

默认路由表包含一个路由（名为 Default）。 Default 路由将 URL 的第一个段映射到控制器名称、第二个段映射到控制器操作，第三个段映射到名为 **id** 的参数。

假设在 web 浏览器地址栏中输入以下 URL:

/ 主页/索引/3

默认路由将此 URL 映射到以下参数：

- 控制器 = 主页

- 操作 = 索引

- id = 3

在请求 URL /Home/索引/3，执行以下代码：

HomeController.Index(3)

Default 路由包括所有三个参数的默认值。 如果不提供控制器，控制器参数将默认为 **Home**。 如果不提供操作，action 参数将默认为 **Index**。 最后，如果不提供 id，id 参数将默认为空字符串。

让我们看一下几个示例的默认路由将 Url 映射到控制器操作的方式。 假设你在浏览器地址栏中输入以下 URL:

/Home

由于 Default 路由参数存在默认值，输入此 URL 将导致 HomeController 类的 Index() 方法在列表 2 中被调用。

**代码清单 2-HomeController.vb**

[!code-vb[Main](asp-net-mvc-routing-overview-vb/samples/sample2.vb)]

列表 2 中 HomeController 类包括一个名为 index 的接受单个参数名为 id。 （） 方法URL /Home 导致 index （） 方法调用的值作为 Id 参数的值执行任何操作。

由于 MVC 框架调用控制器操作的方式，URL /Home 也匹配清单 3 中的 HomeController 类的 index （） 方法。

**代码清单 3-HomeController.vb （不使用任何参数的索引操作）**

[!code-vb[Main](asp-net-mvc-routing-overview-vb/samples/sample3.vb)]

列表 3 中的 index （） 方法不接受任何参数。 URL /Home 将导致此 index （） 方法调用。 URL /Home/索引/3 还调用此方法 （Id 将被忽略）。

URL /Home 也匹配 HomeController 类列表 4 中的 index （） 方法。

**列表 4-HomeController.vb （使用可以为 null 的参数的索引操作）**

[!code-vb[Main](asp-net-mvc-routing-overview-vb/samples/sample4.vb)]

列表 4 中 index （） 方法具有一个整数参数。 由于该参数是可以为 null 的参数 （可以具有值执行任何操作），index （） 可以调用不会生成错误。

最后，调用使用 URL /Home 列表 5 中的 index （） 方法则会引发异常的 Id 参数以来*不是*可以为 null 的参数。 如果你尝试调用 index （） 方法，获取显示在图 1 中的错误。

**列表 5-HomeController.vb （索引操作使用 Id 参数）**

[!code-vb[Main](asp-net-mvc-routing-overview-vb/samples/sample5.vb)]

[![调用控制器操作所需的参数值](asp-net-mvc-routing-overview-vb/_static/image1.jpg)](asp-net-mvc-routing-overview-vb/_static/image1.png)

**图 01**:调用控制器操作所需的参数值 ([单击此项可查看原尺寸图像](asp-net-mvc-routing-overview-vb/_static/image2.png))

URL /Home/索引/3 另一方面，与列表 5 中的索引控制器操作就可以正常工作。 请求 /Home/Index/3 会导致使用 Id 参数具有值 3 调用 index （） 方法。

## <a name="summary"></a>总结

本教程的目标是为你提供简要介绍了 ASP.NET 路由。 获取与新的 ASP.NET MVC 应用程序的默认路由表，我们探讨。 您学习了如何默认路由将 Url 映射到控制器操作。

> [!div class="step-by-step"]
> [上一页](creating-an-action-cs.md)
> [下一页](understanding-action-filters-vb.md)

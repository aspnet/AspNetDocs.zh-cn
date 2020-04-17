---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-cs
title: 创建自定义路由 （C#） |微软文档
author: rick-anderson
description: 了解如何向ASP.NET MVC 应用程序添加自定义路由。 在本教程中，您将了解如何修改 Global.asax 文件中的默认路由表。
ms.author: riande
ms.date: 02/16/2009
ms.assetid: 3cd08f02-8763-490a-b625-2ac96a24b73f
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-cs
msc.type: authoredcontent
ms.openlocfilehash: b66ccc5e0cd4f6d7e5884394c2b7555b76382d3d
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542750"
---
# <a name="creating-custom-routes-c"></a>创建自定义路由 (C#)

由[微软](https://github.com/microsoft)

> 了解如何向ASP.NET MVC 应用程序添加自定义路由。 在本教程中，您将了解如何修改 Global.asax 文件中的默认路由表。

在本教程中，您将了解如何向ASP.NET MVC 应用程序添加自定义路由。 您将了解如何使用自定义路由修改 Global.asax 文件中的默认路由表。

对于许多简单的ASP.NET MVC 应用程序，默认路由表将工作正常。 但是，您可能会发现您有专门的路由需求。 在这种情况下，您可以创建自定义路由。

例如，假设您正在构建一个博客应用程序。 您可能需要处理如下所示的传入请求：

/存档/12-25-2009

当用户输入此请求时，您希望返回与日期 12/25/2009 对应的博客条目。 为了处理这种类型的请求，您需要创建自定义路由。

清单1中的 Global.asax 文件包含一个名为 Blog 的新自定义路由，它处理看起来像 /存档/*条目日期*的请求。

**清单 1 - 全局.asax（带自定义路由）**

[!code-csharp[Main](creating-custom-routes-cs/samples/sample1.cs)]

添加到工艺路线表的路由的顺序很重要。 我们新的自定义博客路由在现有默认路由之前添加。 如果颠倒了订单，则默认路由将始终被调用，而不是自定义路由。

自定义博客路由匹配以 /存档/开头的任何请求。 因此，它与以下 URL 匹配：

- /存档/12-25-2009

- /存档/10-6-2004

- /存档/苹果

自定义路由将传入请求映射到名为"存档"的控制器，并调用 Entry（） 操作。 调用 entry（） 方法时，条目日期将作为名为 entryDate 的参数传递。

您可以将博客自定义路由与清单 2 中的控制器一起使用。

**清单2 - ArchiveController.cs**

[!code-csharp[Main](creating-custom-routes-cs/samples/sample2.cs)]

请注意，清单 2 中的 entry（） 方法接受 DateTime 类型的参数。 MVC 框架足够智能，可以自动将 URL 的输入日期转换为 DateTime 值。 如果 URL 中的输入日期参数无法转换为 DateTime，则引发错误（参见图 1）。

**图 1 - 转换参数时出错**

[![“新建项目”对话框](creating-custom-routes-cs/_static/image1.jpg)](creating-custom-routes-cs/_static/image1.png)

**图 01**： 转换参数时出错 （[单击以查看全尺寸图像](creating-custom-routes-cs/_static/image2.png)）

## <a name="summary"></a>总结

本教程的目的是演示如何创建自定义路由。 您学习了如何在表示博客条目的 Global.asax 文件中向路由表添加自定义路由。 我们讨论了如何将博客条目的请求映射到名为 ArchiveController 的控制器和名为 entry（） 的控制器操作。

> [!div class="step-by-step"]
> [上一页](aspnet-mvc-controllers-overview-cs.md)
> [下一页](creating-a-route-constraint-cs.md)

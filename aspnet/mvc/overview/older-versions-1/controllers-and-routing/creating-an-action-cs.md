---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-cs
title: 创建操作 （C#） |微软文档
author: rick-anderson
description: 了解如何向ASP.NET MVC 控制器添加新操作。 了解方法为操作的要求。
ms.author: riande
ms.date: 03/02/2009
ms.assetid: cb33b28c-3025-4bd1-a1fa-eaa3af7bb56f
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-cs
msc.type: authoredcontent
ms.openlocfilehash: 1c1edfbab41afa58c7cb2c0d306995e9fe491c90
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542269"
---
# <a name="creating-an-action-c"></a>创建操作 (C#)

由[微软](https://github.com/microsoft)

> 了解如何向ASP.NET MVC 控制器添加新操作。 了解方法为操作的要求。

本教程的目的是解释如何创建新的控制器操作。 了解操作方法的要求。 您还学习如何防止方法作为操作公开。

## <a name="adding-an-action-to-a-controller"></a>向控制器添加操作

通过将新方法添加到控制器，向控制器添加新操作。 例如，清单 1 中的控制器包含名为 Index（） 的操作和名为 SayHello（） 的操作。 这两种方法都公开为操作。

**清单1 - 控制器\主控制器.cs**

[!code-csharp[Main](creating-an-action-cs/samples/sample1.cs)]

为了作为一种行动暴露在宇宙中，一种方法必须满足某些要求：

- 该方法必须为公共。
- 该方法不能是静态方法。
- 该方法不能是扩展方法。
- 该方法不能是构造函数、getter 或 setter。
- 该方法不能具有打开的泛型类型。
- 该方法不是控制器基类的方法。
- 该方法不能包含**ref**或**out**参数。

请注意，对控制器操作的返回类型没有限制。 控制器操作可以返回字符串、DateTime、Random 类的实例或 void。 ASP.NET MVC 框架将任何不是操作结果的返回类型转换为字符串，并将字符串呈现给浏览器。

将不违反这些要求的任何方法添加到控制器时，该方法将作为控制器操作公开。 这里要小心。 连接到 Internet 的任何人都可以调用控制器操作。 例如，不要创建"删除 My网站"控制器操作。

## <a name="preventing-a-public-method-from-being-invoked"></a>防止调用公共方法

如果需要在控制器类中创建公共方法，并且不希望将该方法公开为控制器操作，则可以通过使用 [NonAction] 属性阻止调用该方法。 例如，清单 2 中的控制器包含一种名为"公司机密（）"的公共方法，该方法使用 [非操作] 属性进行修饰。

**清单2 - 控制器_工作控制器.cs**

[!code-csharp[Main](creating-an-action-cs/samples/sample2.cs)]

如果您尝试通过在浏览器的地址栏中键入 /Work/公司机密来调用公司机密（） 控制器操作，则会收到图 1 中的错误消息。

[![调用非操作方法](creating-an-action-cs/_static/image1.jpg)](creating-an-action-cs/_static/image1.png)

**图 01**：调用非操作方法（[单击以查看全尺寸图像](creating-an-action-cs/_static/image2.png)）

> [!div class="step-by-step"]
> [上一页](creating-a-controller-cs.md)
> [下一页](asp-net-mvc-routing-overview-vb.md)

---
uid: mvc/overview/older-versions-1/views/passing-data-to-view-master-pages-cs
title: 将数据传递到查看母版页 （C#） |微软文档
author: rick-anderson
description: 本教程的目的是解释如何将数据从控制器传递到视图母版页。 我们检查将数据传递到视图的两种策略...
ms.author: riande
ms.date: 10/16/2008
ms.assetid: 5fee879b-8bde-42a9-a434-60ba6b1cf747
msc.legacyurl: /mvc/overview/older-versions-1/views/passing-data-to-view-master-pages-cs
msc.type: authoredcontent
ms.openlocfilehash: 7a934f93d89e6530becc114fe455c8b3ab2968de
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542477"
---
# <a name="passing-data-to-view-master-pages-c"></a>向视图母版页传递数据 (C#)

由[微软](https://github.com/microsoft)

[下载 PDF](https://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_13_CS.pdf)

> 本教程的目的是解释如何将数据从控制器传递到视图母版页。 我们检查将数据传递到视图母版页的两种策略。 首先，我们讨论一个简单的解决方案，该解决方案会导致应用程序难以维护。 接下来，我们将研究一个更好的解决方案，它需要更多的初始工作，但会产生一个更可维护的应用程序。

## <a name="passing-data-to-view-master-pages"></a>将数据传递到查看母版页

本教程的目的是解释如何将数据从控制器传递到视图母版页。 我们检查将数据传递到视图母版页的两种策略。 首先，我们讨论一个简单的解决方案，该解决方案会导致应用程序难以维护。 接下来，我们将研究一个更好的解决方案，它需要更多的初始工作，但会产生一个更可维护的应用程序。

### <a name="the-problem"></a>问题

假设您正在构建一个影片数据库应用程序，并且您想要在应用程序的每一页上显示影片类别列表（参见图 1）。 此外，假设影片类别列表存储在数据库表中。 在这种情况下，从数据库中检索类别并在视图母版页中呈现影片类别列表是有意义的。

[![在视图母版页中显示影片类别](passing-data-to-view-master-pages-cs/_static/image2.png)](passing-data-to-view-master-pages-cs/_static/image1.png)

**图 01**： 在视图母版页中显示影片类别 （[单击以查看全尺寸图像](passing-data-to-view-master-pages-cs/_static/image3.png)）

这就是问题所在。 如何检索母版页中的电影类别列表？ 在母版页中直接调用模型类的方法是很有诱惑力的。 换句话说，最好在母版页中包含从数据库检索数据的代码。 但是，绕过 MVC 控制器访问数据库将违反完全分离问题是构建 MVC 应用程序的主要好处之一。

在 MVC 应用程序中，您希望 MVC 视图和 MVC 模型之间的所有交互都由 MVC 控制器处理。 这种关注点的分离产生了更可维护、适应性强和可测试的应用。

在 MVC 应用程序中，传递给视图的所有数据（包括视图母版页）都应通过控制器操作传递到视图。 此外，数据应利用视图数据传递。 在本教程的其余部分中，我将检查将视图数据传递到视图母版页的两种方法。

### <a name="the-simple-solution"></a>简单解决方案

让我们从将视图数据从控制器传递到视图母版页的最简单的解决方案开始。 最简单的解决方案是在每个控制器操作中传递母版页的视图数据。

考虑清单 1 中的控制器。 它公开名为`Index()`和`Details()`的两个操作。 操作`Index()`方法返回"影片"数据库表中的每个影片。 操作`Details()`方法返回特定影片类别中的每部电影。

**清单1 |`Controllers\HomeController.cs`**

[!code-csharp[Main](passing-data-to-view-master-pages-cs/samples/sample1.cs)]

请注意，Index（） 和详细信息（）操作都会添加两个项来查看数据。 索引（） 操作添加了两个键：类别和影片。 类别键表示视图母版页显示的电影类别列表。 影片键表示"索引"视图页显示的影片列表。

"详细信息"操作还添加了两个名为类别和影片的键。 类别键再次表示视图母版页显示的电影类别列表。 影片键表示"详细信息"视图页显示的特定类别中的电影列表（参见图 2）。

[!["详细信息"视图](passing-data-to-view-master-pages-cs/_static/image5.png)](passing-data-to-view-master-pages-cs/_static/image4.png)

**图 02**： "详细信息"视图 （[单击以查看全尺寸图像](passing-data-to-view-master-pages-cs/_static/image6.png)）

索引视图包含在清单 2 中。 它只是遍达视图数据中由影片项表示的电影列表。

**清单2 |`Views\Home\Index.aspx`**

[!code-aspx[Main](passing-data-to-view-master-pages-cs/samples/sample2.aspx)]

视图母版页包含在清单 3 中。 视图母版页从视图数据中参数地表示并呈现类别项表示的所有影片类别。

**清单3 |`Views\Shared\Site.master`**

[!code-aspx[Main](passing-data-to-view-master-pages-cs/samples/sample3.aspx)]

所有数据都通过视图数据传递到视图和视图母版页。 这是将数据传递到母版页的正确方法。

那么，这个解决方案有什么问题呢？ 问题是，此解决方案违反了 DRY（不要重复自己）原则。 每个控制器操作都必须添加完全相同的影片类别列表才能查看数据。 应用程序中具有重复的代码会使应用程序更难维护、调整和修改。

### <a name="the-good-solution"></a>良好的解决方案

在本节中，我们将检查将数据从控制器操作传递到视图母版页的替代方法和更好的解决方案。 我们不是在每个控制器操作中添加母版页的影片类别，而是仅将影片类别添加到视图数据一次。 视图母版页使用的所有视图数据都添加到应用程序控制器中。

应用程序控制器类包含在清单 4 中。

**清单4 |`Controllers\ApplicationController.cs`**

[!code-csharp[Main](passing-data-to-view-master-pages-cs/samples/sample4.cs)]

关于清单4中的应用程序控制器，您应该注意三件事。 首先，请注意，类从基 System.Web.Mvc.Controller 类继承。 应用程序控制器是控制器类。

其次，请注意应用程序控制器类是一个抽象类。 抽象类是必须由具体类实现的类。 由于应用程序控制器是抽象类，因此不能直接调用类中定义的任何方法。 如果尝试直接调用应用程序类，则会收到"找不到资源"错误消息。

第三，请注意，应用程序控制器包含一个构造函数，该构造函数添加要查看数据的影片类别列表。 从应用程序控制器继承的每个控制器类都会自动调用应用程序控制器的构造函数。 每当对从应用程序控制器继承的任何控制器调用任何操作时，影片类别将自动包含在视图数据中。

清单 5 中的影片控制器从应用程序控制器继承。

**清单5 |`Controllers\MoviesController.cs`**

[!code-csharp[Main](passing-data-to-view-master-pages-cs/samples/sample5.cs)]

与上一节中讨论的"家庭控制器"一样，电影控制器公开了名为`Index()`和`Details()`的两种操作方法。 请注意，视图母版页显示的影片类别列表不会添加以查看 或`Index()``Details()`方法中的数据。 由于"影片"控制器从应用程序控制器继承，因此将添加影片类别列表以自动查看数据。

请注意，此为视图母版页添加视图数据的解决方案并不违反 DRY（不要重复自己）原则。 添加要查看数据的影片类别列表的代码仅包含在一个位置：应用程序控制器的构造函数。

### <a name="summary"></a>总结

在本教程中，我们讨论了将视图数据从控制器传递到视图母版页的两种方法。 首先，我们研究了一种简单但难以维持的方法。 在第一部分中，我们讨论了如何在应用程序中的每个控制器操作中为视图母版页添加视图数据。 我们的结论是，这是一个糟糕的方法，因为它违反了DRY（不要重复自己）的原则。

接下来，我们研究了添加视图母版页所需的数据以查看数据更好的策略。 我们不是在每个控制器操作中添加视图数据，而是在应用程序控制器中只添加一次视图数据。 这样，当将数据传递到ASP.NET MVC 应用程序中的视图母版页时，可以避免重复的代码。

> [!div class="step-by-step"]
> [上一页](creating-page-layouts-with-view-master-pages-cs.md)
> [下一页](asp-net-mvc-views-overview-vb.md)

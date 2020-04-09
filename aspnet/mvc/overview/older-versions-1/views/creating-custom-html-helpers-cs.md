---
uid: mvc/overview/older-versions-1/views/creating-custom-html-helpers-cs
title: 创建自定义 HTML 帮助器 （C#） |微软文档
author: microsoft
description: 本教程的目标是演示如何创建自定义 HTML 帮助器，您可以在 MVC 视图中使用。 通过利用 HTML 帮助程序...
ms.author: riande
ms.date: 10/07/2008
ms.assetid: e454c67d-a86e-4119-a858-eb04bbec2dff
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-custom-html-helpers-cs
msc.type: authoredcontent
ms.openlocfilehash: 7a2e5a5b42aa5bf267a42fef2fcad7022001ce6f
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675331"
---
# <a name="creating-custom-html-helpers-c"></a>创建自定义 HTML 帮助程序 (C#)

由[微软](https://github.com/microsoft)

[下载 PDF](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_9_CS.pdf)

> 本教程的目标是演示如何创建自定义 HTML 帮助器，您可以在 MVC 视图中使用。 通过使用 HTML 帮助器，可以减少创建标准 HTML 页必须执行的繁琐键入 HTML 标记的数量。

本教程的目标是演示如何创建自定义 HTML 帮助器，您可以在 MVC 视图中使用。 通过使用 HTML 帮助器，可以减少创建标准 HTML 页必须执行的繁琐键入 HTML 标记的数量。

在本教程的第一部分中，我描述了 ASP.NET MVC 框架中包含的一些现有 HTML 帮助器。 接下来，我描述了创建自定义 HTML 帮助器的两种方法：我解释如何通过创建静态方法和创建扩展方法来创建自定义 HTML 帮助程序。

## <a name="understanding-html-helpers"></a>了解 HTML 帮助器

HTML 帮助程序只是返回字符串的方法。 字符串可以表示所需的任何类型的内容。 例如，可以使用 HTML 帮助器呈现标准 HTML 标记（如`<input>` `<img>` HTML 和标记）。 您还可以使用 HTML 帮助器呈现更复杂的内容，如选项卡条或数据库数据的 HTML 表。

mVC 框架ASP.NET包括以下一组标准 HTML 帮助器（这不是完整的列表）：

- Html.操作链接（）
- Html.开始形式（）
- Html.复选框（）
- Html.下拉列表（）
- Html.结束形式（）
- Html.隐藏（）
- Html.列表框（）
- Html.密码（）
- Html.收音机按钮（）
- Html.文本区域（）
- Html.TextBox（）

例如，请考虑清单 1 中的窗体。 此表单是在两个标准 HTML 帮助器的帮助下呈现的（参见图 1）。 此窗体使用`Html.BeginForm()`和`Html.TextBox()`帮助器方法呈现简单的 HTML 窗体。

[![使用 HTML 帮助器呈现的页面](creating-custom-html-helpers-cs/_static/image2.png)](creating-custom-html-helpers-cs/_static/image1.png)

**图 01**： 使用 HTML 帮助器呈现的页面 （[单击以查看全尺寸图像](creating-custom-html-helpers-cs/_static/image3.png)）

**清单1 |`Views\Home\Index.aspx`**

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample1.aspx)]

Html.BeginForm（） 帮助器方法用于创建打开和关闭 HTML`<form>`标记。 请注意，该方法`Html.BeginForm()`是在 using 语句中调用的。 using 语句可确保标记在`<form>`using 块的末尾关闭。

如果您愿意，可以调用 Html.EndForm（） 帮助器方法来关闭`<form>`标记，而不是创建 using 块。 使用任何方法创建您最直观的开始和结束`<form>`标记。

在`Html.TextBox()`清单1中使用帮助器方法来呈现 HTML`<input>`标记。 如果在浏览器中选择视图源，则会在清单 2 中看到 HTML 源。 请注意，源包含标准 HTML 标记。

> [!IMPORTANT]
> 请注意 -HTML`Html.TextBox()`帮助程序使用`<%= %>`标记而不是`<% %>`标记呈现。 如果未包含等号，则不会向浏览器呈现任何内容。

mVC ASP.NET框架包含一小组帮助器。 最有可能的是，您需要使用自定义 HTML 帮助程序扩展 MVC 框架。 在本教程的其余部分中，您将学习创建自定义 HTML 帮助器的两种方法。

**清单2 |`Index.aspx Source`**

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample2.aspx)]

### <a name="creating-html-helpers-with-static-methods"></a>使用静态方法创建 HTML 帮助器

创建新 HTML 帮助器的最简单方法是创建返回字符串的静态方法。 例如，假设您决定创建一个呈现 HTML`<label>`标记的新 HTML 帮助程序。 可以使用清单 2 中的类来呈现 。 `<label>`

**清单2 |`Helpers\LabelHelper.cs`**

[!code-csharp[Main](creating-custom-html-helpers-cs/samples/sample3.cs)]

清单2中的类没有什么特别之处。 该方法`Label()`只需返回一个字符串。

清单3中修改后的索引视图使用`LabelHelper`来呈现 HTML`<label>`标记。 请注意，视图包含导入命名`<%@ imports %>`空间的`Application1.Helpers`指令。

**清单2 |`Views\Home\Index2.aspx`**

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample4.aspx)]

### <a name="creating-html-helpers-with-extension-methods"></a>使用扩展方法创建 HTML 帮助程序

如果要创建与 ASP.NET mVC 框架中包含的标准 HTML 帮助程序相同的 HTML 帮助程序，则需要创建扩展方法。 扩展方法使您能够向现有类添加新方法。 创建 HTML 帮助器方法时，向由视图的 Html 属性表示的 HtmlHelper 类添加新方法。

清单3中的类向名为 的`HtmlHelper``Label()`类添加了扩展方法。 关于这个类，你应该注意一些事情。 首先，请注意类是静态类。 必须使用静态类定义扩展方法。

其次，请注意，`Label()`方法的第一个参数前面是关键字`this`。 扩展方法的第一个参数指示扩展方法扩展的类。

**清单3 |`Helpers\LabelExtensions.cs`**

[!code-csharp[Main](creating-custom-html-helpers-cs/samples/sample5.cs)]

创建扩展方法并成功构建应用程序后，扩展方法与类的所有其他方法一样显示在 Visual Studio Intellisense 中（参见图 2）。 唯一的区别是扩展方法旁边出现一个特殊符号（向下箭头的图标）。

[![使用 Html.label（） 扩展方法](creating-custom-html-helpers-cs/_static/image5.png)](creating-custom-html-helpers-cs/_static/image4.png)

**图 02**： 使用 Html.label（） 扩展方法 （[单击以查看全尺寸图像](creating-custom-html-helpers-cs/_static/image6.png)）

清单4中修改后的索引视图使用 Html.label（） 扩展方法呈现其所有`<label>`标记。

**清单4 |`Views\Home\Index3.aspx`**

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample6.aspx)]

## <a name="summary"></a>总结

在本教程中，您学习了创建自定义 HTML 帮助器的两种方法。 首先，您学习了如何通过创建返回字符串`Label()`的静态方法来创建自定义 HTML 帮助程序。 接下来，您学习了如何通过在`Label()``HtmlHelper`类上创建扩展方法来创建自定义 HTML 帮助器方法。

在本教程中，我重点讨论了构建一个非常简单的 HTML 帮助器方法。 意识到 HTML 帮助程序可能非常复杂。 可以生成 HTML 帮助程序，这些帮助程序呈现丰富的内容，如树视图、菜单或数据库数据表。

> [!div class="step-by-step"]
> [上一页](asp-net-mvc-views-overview-cs.md)
> [下一页](using-the-tagbuilder-class-to-build-html-helpers-cs.md)

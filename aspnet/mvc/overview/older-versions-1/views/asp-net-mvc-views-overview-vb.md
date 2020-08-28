---
uid: mvc/overview/older-versions-1/views/asp-net-mvc-views-overview-vb
title: ASP.NET MVC 视图 (VB) 概述 |Microsoft Docs
author: StephenWalther
description: 什么是 ASP.NET MVC 视图，它与 HTML 页面有何不同？ 在本教程中，Stephen Walther 介绍了如何进行查看，并演示了如何
ms.author: riande
ms.date: 02/16/2008
ms.assetid: c28ba88d-3a93-47f5-a306-049bd766714d
msc.legacyurl: /mvc/overview/older-versions-1/views/asp-net-mvc-views-overview-vb
msc.type: authoredcontent
ms.openlocfilehash: a07d15cb14e9ef90b62c5a8702dee53f1a0a6032
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89044659"
---
# <a name="aspnet-mvc-views-overview-vb"></a>ASP.NET MVC 视图概述 (VB)

作者： [Stephen Walther](https://github.com/StephenWalther)

> 什么是 ASP.NET MVC 视图，它与 HTML 页面有何不同？ 在本教程中，Stephen Walther 介绍了如何在视图中利用查看数据和 HTML 帮助器。

本教程的目的是提供 ASP.NET MVC 视图、视图数据和 HTML 帮助器的简要介绍。 在本教程结束时，应了解如何创建新视图，将数据从控制器传递到视图，以及使用 HTML 帮助器在视图中生成内容。

## <a name="understanding-views"></a>了解视图

与 ASP.NET 或 Active Server Pages 不同，ASP.NET MVC 不包含任何直接对应于页面的内容。 在 ASP.NET MVC 应用程序中，磁盘上没有对应于你在浏览器的地址栏中键入的 URL 中的路径的页面。 ASP.NET MVC 应用程序中最接近的一页是称为 " *视图*"。

在 ASP.NET MVC 应用程序中，传入的浏览器请求会映射到控制器操作。 控制器操作可能会返回视图。 但是，控制器操作可能会执行其他某种类型的操作，例如，将您重定向到另一个控制器操作。

列表1包含一个名为 "HomeController" 的简单控制器。 HomeController 公开了两个名为 Index ( 控制器操作： # A1，详细信息 ( # A3。

**列表 1-HomeController**

[!code-vb[Main](asp-net-mvc-views-overview-vb/samples/sample1.vb)]

通过在浏览器地址栏中键入以下 URL，可以调用第一个操作（索引 ( # A1 操作）：

/Home/Index

可以通过在浏览器中键入此地址来调用第二个操作，详细信息 ( # A1 操作：

/Home/Details

索引 ( # A1 操作返回视图。 你创建的大多数操作都将返回视图。 不过，操作可以返回其他类型的操作结果。 例如，详细信息 ( # A1 操作返回将传入请求重定向到索引 ( # A3 操作的 RedirectToActionResult。

索引 ( # A1 操作包含以下代码行：

查看 ( # A1

下面这行代码将返回一个视图，该视图必须位于 web 服务器上的以下路径：

\Views\Home\Index.aspx

将从控制器的名称和控制器操作的名称推断视图的路径。

如果您愿意，您可以清楚了解视图。 下面的代码行返回一个名为 Fred 的视图：

查看 ( Fred ) 

执行此代码行时，将从以下路径返回视图：

\Views\Home\Fred.aspx

> [!NOTE] 
> 
> 如果计划为 ASP.NET MVC 应用程序创建单元测试，则最好是显式了解视图名称。 这样，便可以创建单元测试来验证控制器操作是否返回了预期视图。

## <a name="adding-content-to-a-view"></a>向视图添加内容

视图是可以包含脚本的标准 (X) HTML 文档。 您可以使用脚本向视图中添加动态内容。

例如，"列表 2" 中的视图显示当前日期和时间。

**列表 2-\Views\Home\Index.aspx**

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample2.aspx)]

请注意，列表2中的 HTML 页面的正文包含以下脚本：

&lt;% 响应。写入 (日期时间。现在) %&gt;

使用脚本分隔符 &lt; % 和% &gt; 来标记脚本的开头和结尾。 此脚本是用 Visual basic 编写的。 它通过调用响应来显示当前日期和时间。写入 ( # A1 方法，以将内容呈现到浏览器。 脚本分隔符 &lt; % 和% &gt; 可用于执行一个或多个语句。

由于你调用了响应。请经常编写 ( # A1，Microsoft 将为你提供调用响应的快捷方式。编写 ( # A3 方法。 列表3中的视图使用分隔符 &lt; % = 和% &gt; 作为调用响应的快捷方式。写入 ( # A1。

**列表 3-Views\Home\Index2.aspx**

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample3.aspx)]

您可以使用任何 .NET 语言在视图中生成动态内容。 通常，你将使用 Visual Basic .NET 或 c # 来编写控制器和视图。

## <a name="using-html-helpers-to-generate-view-content"></a>使用 HTML 帮助器生成视图内容

为了更轻松地向视图添加内容，你可以利用称为 *HTML 帮助器*的内容。 通常，HTML 帮助器是生成字符串的方法。 您可以使用 HTML 帮助器生成标准 HTML 元素，例如文本框、链接、下拉列表和列表框。

例如，列表4中的视图利用三个 HTML 帮助器--Html.beginform ( # A1，文本框 ( # A3 和 Password ( # A5 帮助程序--生成登录窗体 (参阅图 1) 。

**列表 4--\Views\Home\Login.aspx**

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample4.aspx)]

[![“新建项目”对话框](asp-net-mvc-views-overview-vb/_static/image1.jpg)](asp-net-mvc-views-overview-vb/_static/image1.png)

**图 01**：标准登录表单 ([单击查看全尺寸图像](asp-net-mvc-views-overview-vb/_static/image2.png)) 

所有 HTML 帮助器方法都是在视图的 Html 属性上调用的。 例如，通过调用 Html. TextBox ( # A1 方法呈现 TextBox。

请注意，在 &lt; 调用 Html. TextBox 时，使用脚本分隔符% = 和% &gt; ( # A1 和 html ( # A3 帮助程序。 这些帮助程序只返回一个字符串。 需要调用响应。写入 ( # A1，以便将字符串呈现到浏览器。

使用 HTML 帮助器方法是可选的。 通过减少需要编写的 HTML 和脚本数量，使你的生活变得更加轻松。 列表5中的视图在不使用 HTML 帮助器的情况下，将与列表4中的视图呈现完全相同的窗体。

**列表 5--\Views\Home\Login.aspx**

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample5.aspx)]

你还可以选择创建你自己的 HTML 帮助器。 例如，可以创建一个 GridView ( # A1 helper 方法，该方法在 HTML 表中自动显示一组数据库记录。 本主题介绍了如何 **创建自定义 HTML 帮助**程序。

## <a name="using-view-data-to-pass-data-to-a-view"></a>使用视图数据将数据传递给视图

您可以使用 "查看数据" 将数据从控制器传递到视图。 请考虑视图数据，如通过邮件发送的包。 必须使用此包发送从控制器传递到视图的所有数据。 例如，清单6中的控制器添加了用于查看数据的消息。

**列表 6-ProductController**

[!code-vb[Main](asp-net-mvc-views-overview-vb/samples/sample6.vb)]

控制器 ViewData 属性表示名称和值对的集合。 在列表6中，索引 ( # A1 方法将项添加到名为 message 的视图数据集合中，值 Hello World！。 当索引 ( # A1 方法返回视图时，会自动将视图数据传递给视图。

列表7中的视图从查看数据中检索消息，并将消息呈现到浏览器。

**列表 7--\Views\Product\Index.aspx**

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample7.aspx)]

请注意，视图利用 Html. 在呈现消息时， ( # A1 HTML Helper 方法进行编码。 Html 编码 ( # A1 HTML 帮助器将特殊字符（例如和）编码为可 &lt; &gt; 安全显示在网页中的字符。 每当你呈现用户提交到网站的内容时，你应该对内容进行编码，以防出现 JavaScript 注入攻击。

 (因为我们在 ProductController 中创建了自己的消息，所以我们不需要对消息进行编码。 但是，在显示从视图中的视图数据检索到的内容时，始终调用 Html. 编码 ( # A1 方法是一种很好的习惯。 ) 

在列表7中，我们利用了视图数据将简单字符串消息从控制器传递到视图。 你还可以使用 "查看数据" 将其他类型的数据（如数据库记录集合）从控制器传递到视图。 例如，如果您想要在视图中显示 Products 数据库表的内容，则可以在视图数据中传递数据库记录的集合。

你还可以选择将强类型视图数据从控制器传递到视图。 本主题介绍了 **了解强类型视图数据和视图**的教程。

## <a name="summary"></a>摘要

本教程简要介绍了 ASP.NET MVC 视图、视图数据和 HTML 帮助器。 在第一部分中，您学习了如何向项目中添加新视图。 您已经了解到，您必须将视图添加到正确的文件夹中，以便从特定控制器调用它。 接下来，我们讨论了 HTML 帮助器的主题。 您学习了 HTML 帮助程序如何使您能够轻松地生成标准 HTML 内容。 最后，您学习了如何利用视图数据将数据从控制器传递到视图。

> [!div class="step-by-step"]
> [上一页](passing-data-to-view-master-pages-cs.md)
> [下一页](creating-custom-html-helpers-vb.md)

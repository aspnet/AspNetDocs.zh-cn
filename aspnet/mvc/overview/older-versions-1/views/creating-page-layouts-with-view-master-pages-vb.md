---
uid: mvc/overview/older-versions-1/views/creating-page-layouts-with-view-master-pages-vb
title: 使用查看母版页 （VB） 创建页面布局 |微软文档
author: rick-anderson
description: 在本教程中，您将了解如何利用视图母版页为应用程序中的多个页面创建通用页面布局。 您可以使用...
ms.author: riande
ms.date: 10/16/2008
ms.assetid: d34f90a1-6de3-482a-a326-f87fdcbaaaff
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-page-layouts-with-view-master-pages-vb
msc.type: authoredcontent
ms.openlocfilehash: 37b8d858c72357ebbe51458f76511a9672b01b4d
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542490"
---
# <a name="creating-page-layouts-with-view-master-pages-vb"></a>使用视图母版页创建页面布局 (VB)

由[微软](https://github.com/microsoft)

[下载 PDF](https://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_12_VB.pdf)

> 在本教程中，您将了解如何利用视图母版页为应用程序中的多个页面创建通用页面布局。 例如，可以使用视图母版页定义两列页面布局，并为 Web 应用程序中的所有页面使用两列布局。

## <a name="creating-page-layouts-with-view-master-pages"></a>使用查看母版页创建页面布局

在本教程中，您将了解如何利用视图母版页为应用程序中的多个页面创建通用页面布局。 例如，可以使用视图母版页定义两列页面布局，并为 Web 应用程序中的所有页面使用两列布局。

您还可以利用查看母版页在应用程序中多个页面之间共享常见内容。 例如，您可以将网站徽标、导航链接和横幅广告放在视图母版页中。 这样，应用程序中的每个页面都会自动显示此内容。

在本教程中，您将了解如何创建新的视图母版页，并根据母版页创建新的视图内容页。

### <a name="creating-a-view-master-page"></a>创建视图母版页

让我们首先创建定义两列布局的视图母版页。 通过右键单击"视图+共享"文件夹、选择菜单选项 **"添加、新建项目**"以及选择 MVC 视图母版页模板（参见图 1），将新的视图母版页添加到 MVC 项目。

[![添加视图母版页](creating-page-layouts-with-view-master-pages-vb/_static/image2.png)](creating-page-layouts-with-view-master-pages-vb/_static/image1.png)

**图 01**： 添加视图母版页 （[单击以查看全尺寸图像](creating-page-layouts-with-view-master-pages-vb/_static/image3.png)）

您可以在应用程序中创建多个视图母版页。 每个视图母版页可以定义不同的页面布局。 例如，您可能希望某些页面具有两列布局和其他页面具有三列布局。

视图母版页看起来非常类似于标准ASP.NET MVC 视图。 但是，与普通视图不同，视图母版页包含一个或多个`<asp:ContentPlaceHolder>`标记。 这些`<contentplaceholder>`标记用于标记可在单个内容页中重写的母版页区域。

例如，清单 1 中的视图母版页定义两列布局。 它包含两`<contentplaceholder>`个标记。 每`<ContentPlaceHolder>`列一列。

**清单1 |`Views\Shared\Site.master`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample1.aspx)]

清单1中的视图母版页的正文包含两`<div>`个对应于两列的标记。 "级联样式表"列类应用于这两个`<div>`标记。 此类在母版页顶部声明的样式表中定义。 您可以通过切换到"设计"视图来预览视图母版页的呈现方式。 单击源代码编辑器左下角的"设计"选项卡（参见图 2）。

[![在设计器中预览母版页](creating-page-layouts-with-view-master-pages-vb/_static/image5.png)](creating-page-layouts-with-view-master-pages-vb/_static/image4.png)

**图 02**： 预览设计器中的母版页 （[单击以查看全尺寸图像](creating-page-layouts-with-view-master-pages-vb/_static/image6.png)）

### <a name="creating-a-view-content-page"></a>创建查看内容页面

创建视图母版页后，可以基于视图母版页创建一个或多个视图内容页。 例如，您可以通过右键单击"视图+主页"文件夹、选择 **"添加、新建项目"、** 选择**MVC 查看内容页**模板、输入名称 Index.aspx 以及单击"添加"按钮（参见图 3）为主控制器创建索引视图内容页。

[![添加视图内容页](creating-page-layouts-with-view-master-pages-vb/_static/image8.png)](creating-page-layouts-with-view-master-pages-vb/_static/image7.png)

**图 03**： 添加视图内容页 （[单击以查看全尺寸图像](creating-page-layouts-with-view-master-pages-vb/_static/image9.png)）

单击"添加"按钮后，将出现一个新对话框，使您能够选择视图母版页以与视图内容页关联（参见图 4）。 您可以导航到我们在上一节中创建的 Site.master 视图母版页。

[![选择母版页](creating-page-layouts-with-view-master-pages-vb/_static/image11.png)](creating-page-layouts-with-view-master-pages-vb/_static/image10.png)

**图 04**： 选择母版页 （[单击以查看全尺寸图像](creating-page-layouts-with-view-master-pages-vb/_static/image12.png)）

基于 Site.master 母版页创建新的视图内容页后，您将在清单 2 中获取该文件。

**清单2 |`Views\Home\Index.aspx`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample2.aspx)]

请注意，此视图包含一个`<asp:Content>`对应于视图母版页中每个`<asp:ContentPlaceHolder>`标记的标记。 每个`<asp:Content>`标记都包含一个 ContentPlaceHolderID 属性，`<asp:ContentPlaceHolder>`该属性指向它覆盖的特定。

此外，请注意，清单 2 中的内容视图页不包含任何正常的打开和关闭 HTML 标记。 例如，它不包含打开和关闭`<html>`或`<head>`标记。 所有正常的打开和关闭标记都包含在视图母版页中。

要在视图内容页中显示的任何内容都必须放置在`<asp:Content>`标记中。 如果将这些标记之外放置任何 HTML 或其他内容，则当您尝试查看页面时，将出现错误。

您无需覆盖内容视图页中母`<asp:ContentPlaceHolder>`版页中的每个标记。 仅当要将`<asp:ContentPlaceHolder>`标记替换为特定内容时，才需要覆盖标记。

例如，清单 3 中修改的索引视图仅包含两`<asp:Content>`个标记。 每个`<asp:Content>`标记都包含一些文本。

**清单3 |`Views\Home\Index.aspx (modified)`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample3.aspx)]

当请求清单 3 中的视图时，它将呈现图 5 中的页面。 请注意，视图呈现具有两列的页面。 此外，请注意，视图内容页中的内容将与视图母版页中的内容合并。

[![索引视图内容页](creating-page-layouts-with-view-master-pages-vb/_static/image14.png)](creating-page-layouts-with-view-master-pages-vb/_static/image13.png)

**图 05**： 索引视图内容页 （[单击以查看全尺寸图像](creating-page-layouts-with-view-master-pages-vb/_static/image15.png)）

### <a name="modifying-view-master-page-content"></a>修改查看母版页内容

在使用视图母版页时，您几乎立即遇到的一个问题是，当请求不同的视图内容页时，会修改视图母版页内容。 例如，您希望 Web 应用程序中的每个页面都有唯一的标题。 但是，标题在视图母版页中声明，而不是在视图内容页中声明。 那么，如何为每个视图内容页面自定义页面标题？

有两种方法可以修改视图内容页显示的标题。 首先，您可以将页面标题分配给视图内容页顶部声明的`<%@ page %>`指令的标题属性。 例如，如果要将页面标题"超级大网站"分配给索引视图，则可以在 Index 视图的顶部包括以下指令：

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample4.aspx)]

当"索引"视图呈现给浏览器时，所需的标题将显示在浏览器标题栏中：

[![浏览器标题栏](creating-page-layouts-with-view-master-pages-vb/_static/image17.png)](creating-page-layouts-with-view-master-pages-vb/_static/image16.png)

主视图页必须满足一个重要要求，以便标题属性正常工作。 视图母版页必须包含`<head runat="server">`标记，而不是其标题的正常`<head>`标记。 如果`<head>`标记不包含 runat_"server"属性，则标题将不会显示。 默认视图母版页包括所需的`<head runat="server">`标记。

从单个视图内容页修改母版页内容的另一种方法是包装要在`<asp:ContentPlaceHolder>`标记中修改的区域。 例如，假设您不仅希望更改标题，还要更改由母版视图页呈现的元标记。 清单4中的主视图页在其`<asp:ContentPlaceHolder>``<head>`标记中包含一个标记。

**清单4 |`Views\Shared\Site2.master`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample5.aspx)]

请注意，`<asp:ContentPlaceHolder>`清单 4 中的标记包括默认内容：默认标题和默认元标记。 如果不在单个视图内容页中`<asp:ContentPlaceHolder>`覆盖此标记，则将显示默认内容。

清单5中的内容视图页将覆盖`<asp:ContentPlaceHolder>`标记，以便显示自定义标题和自定义元标记。

**清单5 |`Views\Home\Index2.aspx`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample6.aspx)]

### <a name="summary"></a>总结

本教程为您提供查看母版页和查看内容页的基本介绍。 您学习了如何创建新的视图母版页，并基于它们创建视图内容页。 我们还研究了如何从特定视图内容页修改视图母版页的内容。

> [!div class="step-by-step"]
> [上一页](using-the-tagbuilder-class-to-build-html-helpers-vb.md)
> [下一页](passing-data-to-view-master-pages-vb.md)

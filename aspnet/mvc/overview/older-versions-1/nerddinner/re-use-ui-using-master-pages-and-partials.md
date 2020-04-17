---
uid: mvc/overview/older-versions-1/nerddinner/re-use-ui-using-master-pages-and-partials
title: 使用母版页和部分重用 UI |微软文档
author: rick-anderson
description: 步骤 7 探讨了在视图模板中应用"DRY 原则"的方法，以便使用部分视图模板和母版页来消除代码重复。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: d4243a4a-e91c-4116-9ae0-5c08e5285677
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/re-use-ui-using-master-pages-and-partials
msc.type: authoredcontent
ms.openlocfilehash: f381c4424a9fa0718cd234beeb01ce41bc4ca61e
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542594"
---
# <a name="re-use-ui-using-master-pages-and-partials"></a>使用母版页和部分重用 UI

由[微软](https://github.com/microsoft)

[下载 PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 这是一个免费的["NerdDinner"应用程序教程](introducing-the-nerddinner-tutorial.md)的第7步，该教程演示如何使用ASP.NET MVC 1 构建小型但完整的 Web 应用程序。
> 
> 步骤 7 探讨了在视图模板中应用"DRY 原则"的方法，以便使用部分视图模板和母版页来消除代码重复。
> 
> 如果您使用的是ASP.NET MVC 3，我们建议您按照[MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC 音乐商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程进行操作。

## <a name="nerddinner-step-7-partials-and-master-pages"></a>神经晚餐步骤 7：部分和母版页

MVC 拥抱ASP.NET的设计理念之一是"不要重复自己"原则（通常称为"DRY"）。 DRY 设计有助于消除代码和逻辑的重复，最终使应用程序构建速度更快，更易于维护。

我们已经看到 DRY 原则应用于我们的一些 NerdDinner 方案。 举几个例子：我们的验证逻辑在我们的模型层中实现，这使得它可以在控制器中编辑和创建方案之间强制执行;我们正在跨"编辑"、"详细信息"和"删除"操作方法重用"未找到"视图模板;我们使用具有视图模板的约定命名模式，这样无需在调用 View（） 帮助器方法时显式指定名称;我们正在重新使用 DinnerFormViewModel 类进行编辑和创建操作方案。

现在，让我们来看看如何在我们的视图模板中应用"DRY 原则"，以消除代码重复。

### <a name="re-visiting-our-edit-and-create-view-templates"></a>重新访问我们的编辑和创建视图模板

目前，我们使用两个不同的视图模板 - "Edit.aspx"和"Create.aspx" - 以显示我们的晚餐表单 UI。 快速直观地比较它们，突出显示它们有多相似。 下面是创建窗体的外观：

![](re-use-ui-using-master-pages-and-partials/_static/image1.png)

下面是我们的"编辑"窗体的外观：

![](re-use-ui-using-master-pages-and-partials/_static/image2.png)

没有什么区别吗？ 除了标题和标题文本之外，窗体布局和输入控件是相同的。

如果我们打开"Edit.aspx"和"Create.aspx"视图模板，我们会发现它们包含相同的表单布局和输入控制代码。 这种重复意味着我们最终必须作出两次更改，每当我们介绍或改变一个新的晚餐属性 - 这是不好的。

### <a name="using-partial-view-templates"></a>使用部分视图模板

mVC ASP.NET支持定义可用于封装页面子部分的视图呈现逻辑的"部分视图"模板的能力。 "部分"提供了一种有用的方法来定义一次视图呈现逻辑，然后在应用程序之间的多个位置重用它。

为了帮助"DRYup"我们的 Edit.aspx 和 Create.aspx 视图模板复制，我们可以创建名为"DinnerForm.ascx"的部分视图模板，该模板封装了两者共有的窗体布局和输入元素。 我们将通过右键单击 /Views/Dinners 目录并选择"添加-&gt;视图"菜单命令来执行此操作：

![](re-use-ui-using-master-pages-and-partials/_static/image3.png)

这将显示"添加视图"对话框。 我们将命名要创建"DinnerForm"的新视图，在对话框中选择"创建部分视图"复选框，并指示我们将传递一个 DinnerFormViewModel 类：

![](re-use-ui-using-master-pages-and-partials/_static/image4.png)

当我们单击"添加"按钮时，Visual Studio 将在"@Views_Dinners"目录中为我们创建新的"DinnerForm.ascx"视图模板。

然后，我们可以将重复的表单布局/输入控制代码从我们的 Edit.aspx/ Create.aspx 视图模板复制/粘贴到新的"DinnerForm.ascx"部分视图模板中：

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample1.aspx)]

然后，我们可以更新我们的"编辑"和"创建"视图模板，以调用 DinnerForm 部分模板并消除表单复制。 我们可以在视图模板中调用 Html.Render 部分（"DinnerForm"）来执行此操作：

##### <a name="createaspx"></a>创建.aspx

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample2.aspx)]

##### <a name="editaspx"></a>编辑.aspx

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample3.aspx)]

在调用 Html.Render 部分（例如：*视图/Dinners/DinnerForm.ascx）时，您可以显式限定所需的部分模板的路径。 但是，在上面的代码中，我们利用了 mVC ASP.NET中基于约定的命名模式，并将"DinnerForm"指定为要呈现的部分名称。 当我们这样做时ASP.NET MVC 将首先查看基于约定的视图目录（对于 DinnerSController，这将是 /视图/晚餐）。 如果找不到部分模板，它将在 /Views/共享目录中查找它。

当仅使用部分视图的名称调用 Html.Render 部分（）时，ASP.NET MVC 将传递给调用视图模板使用的相同模型和 ViewData 字典对象。 或者，有重载版本的 Html.Render偏（）使您能够传递备用模型对象和/或 ViewData 字典供部分视图使用。 这对于只想传递完整模型/视图模型子集的方案非常有用。

| **侧主题：为什么&lt;%&gt;而不是&lt;%=&gt;% ？** |
| --- |
| 使用上述代码您可能注意到的一个微妙事情是，在调用 Html.Render.Render&lt;部分（） 时，&lt;我们使用的是&gt;% 块&gt;而不是 %% 块。 &lt;%=&gt; %ASP.NET 块表示开发人员想要呈现指定值（例如：%= &lt;"你好"百分比&gt;将呈现"你好"）。 &lt;%&gt; % 块相反表示开发人员想要执行代码，并且其中的任何呈现输出都必须显式完成（例如：&lt;百分比响应.Write（"你好"）%&gt;。 我们使用&lt;上述 Html.Render 部分&gt;代码的 % 块的原因是 Html.Render 部分（） 方法不返回字符串，而是将内容直接输出到调用视图模板的输出流。 这样做是出于性能效率的原因，并且这样做可以避免创建（可能非常大的）临时字符串对象。 这减少了内存使用量，并提高了应用程序的总体吞吐量。 使用 Html.Render 部分（）时，一个常见的错误是忘记在呼叫结束时添加分号，而该分号在&lt;% 块&gt;内。 例如，此代码将导致编译器错误：% &lt;Html.Render 部分（"DinnerForm"）您&gt;需要编写： &lt;% html.render部分（"DinnerForm"）;%&gt;这是因为&lt;%&gt; % 块是自包含的代码语句，并且使用 C# 代码语句时需要用分号终止。 |

### <a name="using-partial-view-templates-to-clarify-code"></a>使用部分视图模板来澄清代码

我们创建了"DinnerForm"部分视图模板，以避免在多个位置复制视图呈现逻辑。 这是创建部分视图模板的最常见原因。

有时，即使只在单个位置调用部分视图，创建部分视图仍然有意义。 非常复杂的视图模板在提取视图呈现逻辑并将其分区为一个或多个命名良好的部分模板时，通常更容易阅读。

例如，在我们的项目中考虑 Site.master 文件中的以下代码段（我们稍后将查看）。 代码相对直接读取 - 部分是因为在屏幕右上角显示登录/注销链接的逻辑封装在"LogOnUserControl"部分：

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample4.aspx)]

每当您发现自己试图了解视图模板中的 html/代码标记时感到困惑，请考虑如果提取某些标记并将其重构为命名良好的部分视图，是否不清楚。

### <a name="master-pages"></a>母版页

除了支持部分视图外，ASP.NET MVC 还支持创建可用于定义网站通用布局和顶级 html 的"母版页"模板的功能。 然后，可以将内容占位符控件添加到母版页，以标识视图可以覆盖或"填充"的可替换区域。 这提供了一种非常有效（和 DRY）的方法，用于跨应用程序应用通用布局。

默认情况下，新的ASP.NET MVC 项目会自动向其添加母版页模板。 此母版页名为"Site.master"，位于 [视图] 共享] 文件夹中：

![](re-use-ui-using-master-pages-and-partials/_static/image5.png)

默认的 Site.master 文件如下所示。 它定义网站的外层 html，以及顶部导航菜单。 它包含两个可替换的内容占位符控件 - 一个用于标题，另一个用于应替换页面的主要内容的位置：

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample5.aspx)]

我们为 NerdDinner 应用程序创建的所有视图模板（"列表"、"详细信息"、"编辑"、"创建"、"未找到"等）都基于此 Site.master 模板。 当我们使用"添加视图"对话框创建视图时，默认情况下添加到顶部&lt;% = 页面 %&gt;指令的"MasterPageFile"属性指示此指示：

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample6.aspx)]

这意味着我们可以更改 Site.master 内容，并在呈现任何视图模板时自动应用和使用更改。

让我们更新我们的网站.master 的标头部分，以便我们的应用程序的标头是"NerdDinner"而不是"我的 MVC 应用程序"。 让我们还更新我们的导航菜单，以便第一个选项卡是"查找晚餐"（由 HomeController 的 Index（） 操作方法处理），并且让我们添加一个名为"主持晚餐"的新选项卡（由 DinnersController 的 Create（） 操作方法处理）：

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample7.aspx)]

当我们保存 Site.master 文件并刷新浏览器时，我们将看到我们的标头更改显示在应用程序中的所有视图中。 例如：

![](re-use-ui-using-master-pages-and-partials/_static/image6.png)

使用 */Dinners/编辑/[id]* URL：

![](re-use-ui-using-master-pages-and-partials/_static/image7.png)

### <a name="next-step"></a>下一步

部分页和母版页提供了非常灵活的选项，使您能够干净地组织视图。 您会发现，它们可帮助您避免复制视图内容/代码，并使视图模板更易于阅读和维护。

现在，让我们重新访问我们之前构建的列表方案，并启用可扩展的分页支持。

> [!div class="step-by-step"]
> [上一页](use-viewdata-and-implement-viewmodel-classes.md)
> [下一页](implement-efficient-data-paging.md)

---
uid: mvc/overview/views/using-page-inspector-in-aspnet-mvc
title: 在 ASP.NET MVC 中使用 Page Inspector |Microsoft Docs
author: rick-anderson
description: Visual Studio 2012 中的 Page Inspector 是一种使用集成浏览器的 web 开发工具。 在集成浏览器中选择任意元素，并 Page Inspector .。。
ms.author: riande
ms.date: 08/15/2012
ms.assetid: c7e4e1ab-4932-4614-9f53-aaf7c706d498
msc.legacyurl: /mvc/overview/views/using-page-inspector-in-aspnet-mvc
msc.type: authoredcontent
ms.openlocfilehash: 42d5683ce75467a159c9d13edf302bd6bf24a11d
ms.sourcegitcommit: 45754124123403520b9fa2e706a4d1292494159b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/10/2020
ms.locfileid: "89643698"
---
# <a name="using-page-inspector-in-aspnet-mvc"></a>在 ASP.NET MVC 中使用 Page Inspector

通过 Tim Ammann

> Visual Studio 2012 中的 Page Inspector 是一种使用集成浏览器的 web 开发工具。 在集成浏览器中选择任意元素，Page Inspector 会立即突出显示该元素的源和 CSS。 您可以浏览任意 MVC 视图，快速找到所呈现标记的源，并直接在 Visual Studio 环境中使用浏览器工具。
> 
> [观看视频](../../videos/mvc-4/using-page-inspector-in-aspnet-mvc.md)
> 
> 本教程演示如何启用检查模式，然后在你的 web 项目中快速查找和编辑标记和 CSS。 本教程使用 MVC 项目，但你也可以将 Page Inspector 用于 [Web 窗体](https://go.microsoft.com/?linkid=9802001) 和其他 ASP.NET 应用程序。
> 
> 本教程包含以下部分：
> 
> - [先决条件](#_1_prerequisites)
> - [创建 Web 应用程序](#_2_creating_a)
> - [使用 Page Inspector 浏览到视图](#_3_using_page)
> - [启用检查模式](#_4_inspection_mode)
> - [使用 Page Inspector 对标记进行更改](#_5_using_page)
> - [检查模式和 HTML 窗口](#_6_inspection_mode)
> - [在 "样式" 窗口中预览 CSS 更改](#_7_previewing_css)
> - [CSS 自动同步](#css_auto_sync)
> - [使用 CSS 颜色选取器](#css_color_picker)
> - [将动态页面元素映射到 JavaScript](#map_dynamic_elements)

<a id="_prerequisites"></a><a id="_1_prerequisites"></a>

## <a name="prerequisites"></a>先决条件

- [用于 Web 的](https://www.microsoft.com/visualstudio/11/downloads#express-web) [Visual Studio 2012](https://www.microsoft.com/visualstudio/11)或 Visual Studio Express 2012。

> [!NOTE]
> 若要获取最新版本的 Page Inspector，请使用 [Web 平台安装程序](https://go.microsoft.com/fwlink/?LinkId=255386) 安装适用于 .net 2.0 的 MICROSOFT Azure SDK。

Page Inspector 与 Microsoft Web 开发人员工具捆绑在一起。 最新版本为1.3。 若要检查你的版本，请运行 Visual Studio，然后从 "**帮助**" 菜单中选择 "**关于 Microsoft Visual Studio** 。

<a id="_creating_a_web"></a><a id="_2_creating_a"></a>

## <a name="create-a-web-application"></a>创建 Web 应用程序

首先，创建将 Page Inspector 使用的 web 应用程序。 在 Visual Studio 中，依次选择“文件”**“新建项目”** &gt; ****。 在左侧，展开 " **Visual c #**"，选择 " **Web**"，然后选择 " **ASP.NET MVC4 Web 应用程序**"。

![New ASP.NET MVC 应用程序](using-page-inspector-in-aspnet-mvc/_static/image2.png)

单击“确定”。 

在 " **新建 ASP.NET MVC 4 项目** " 对话框中，选择 " **Internet 应用程序**"。 保留 **Razor** 作为默认视图引擎。

![New ASP.NET MVC 项目-Internet 应用程序](using-page-inspector-in-aspnet-mvc/_static/image4.png)

应用程序将在 " **源** " 视图中打开。

![源视图中的新 ASP.NET MVC 应用程序](using-page-inspector-in-aspnet-mvc/_static/image6.png)

现在，你已经有了要使用的应用程序，可以使用 Page Inspector 来检查和修改它。

<a id="_starting_page_inspector"></a><a id="_3_using_page"></a>

## <a name="use-page-inspector-to-browse-to-a-view"></a>使用 Page Inspector 浏览到视图

在 Visual Studio 2012 中，可以右键单击项目中的任何视图， **在 Page Inspector**中选择 "查看"，然后 Page Inspector 将找出路由并显示页面。

在 **解决方案资源管理器**中，展开 " **Views** " 文件夹，然后展开 " **主** 文件夹"。 右键单击 "索引 ..." 文件，然后选择 **"在 Page Inspector 中查看**"。

![Page Inspector 中查看索引 .。。](using-page-inspector-in-aspnet-mvc/_static/image8.png)

默认情况下，Page Inspector 作为窗口停靠在 Visual Studio 环境的左侧。 如果需要，可以将其固定到其他位置，或取消停靠窗口。 请参阅 [如何：排列和停靠窗口](https://msdn.microsoft.com/library/z4y0hsax.aspx)。

"Page Inspector" 窗口的顶部窗格显示浏览器窗口中的当前页。 下窗格显示 HTML 标记中的页面，以及一些选项卡，可用于检查页面的不同方面。 底部窗格类似于 Internet Explorer 中的 [F12 开发人员工具](https://msdn.microsoft.com/ie/aa740478) 。

![Page Inspector 中的 ASP.NET MVC 应用程序](using-page-inspector-in-aspnet-mvc/_static/image10.png)

在本教程中，您将使用 " **HTML** " 和 " **样式** " 选项卡快速导航并对应用程序进行更改。

<a id="_examining_(&quot;decomposing&quot;)_the"></a><a id="_inspection_mode_and"></a><a id="_4_inspection_mode"></a>

## <a name="enableinspection-mode"></a>EnableInspection 模式

若要将 Page Inspector 放入检查模式中，请单击 " **检查** " 按钮。 在检查模式中，当您将鼠标指针悬停在呈现的页的任何部分时，相应的源标记或代码会突出显示。

![切换检查模式](using-page-inspector-in-aspnet-mvc/_static/image12.png)

现在，将鼠标移动到 Page Inspector 内页面的不同部分。 正如你所做的那样，鼠标指针将更改为大加号，并突出显示下面的元素：

![悬停在 div 上。内容包装](using-page-inspector-in-aspnet-mvc/_static/image14.png)

移动鼠标指针时，Visual Studio 会突出显示源文件中的相应 Razor 语法。 如果 HTML 元素来自其他源文件，则 Visual Studio 会自动打开该文件。

在 Page Inspector 中， **html** 选项卡显示从 Razor 语法生成的 html。 移动鼠标指针时，会突出显示 HTML 元素。 " **样式** " 选项卡显示元素的 CSS 规则。

<a id="_5_using_page"></a>

## <a name="use-page-inspector-to-make-changes-to-markup"></a>使用 Page Inspector 对标记进行更改

Page Inspector 允许你查找位置可能不明显的标记。 然后，可以修改标记并查看生成的更改。

若要查看此项，请单击 " **检查** "，然后滚动到页面底部的 "Page Inspector" 窗口。

将鼠标指针移动到页脚区时，Page Inspector 打开 "layout" \_ 文件并突出显示所选布局页的部分。 正如您所看到的，页脚区域是在布局文件中定义的，而不是在视图本身中定义的。

![脚注](using-page-inspector-in-aspnet-mvc/_static/image16.png)

现在，将鼠标指针移动到带有版权声明的行上 <a id="a"></a> 。 在 \_ Layout 页面中，将突出显示相应的行。

![突出显示了页脚版权行](using-page-inspector-in-aspnet-mvc/_static/image18.png)

将一些文本添加到布局 cshtml 文件中行的末尾 \_ 。

&lt;p &gt; &amp; copy; @DateTime.Now.Year -我的 ASP.NET MVC 应用程序 Rocks！ &lt;/p&gt;

现在，按 Ctrl + Alt + Enter，或单击 "更新" 栏以在 "Page Inspector 浏览器" 窗口中查看结果。

![我的 ASP.NET 应用程序 Rocks！](using-page-inspector-in-aspnet-mvc/_static/image20.png)

您可能认为在索引中定义了注脚，但它已在 \_ Layout 中提供，并 Page Inspector 找到了它。

<a id="_inspection_mode_and_1"></a><a id="_6_inspection_mode"></a>

## <a name="inspection-mode-and-the-html-window"></a>检查模式和 HTML 窗口

接下来，您将快速了解 HTML 窗口以及它如何为您映射元素。

单击 " **检查** " 以将 Page Inspector 置于检查模式。

单击 "此处显示徽标" 页面的顶部部分。 您将更详细地检查特定元素，因此，在浏览器窗口中显示的内容将不再随着鼠标指针的移动而改变。

现在，将鼠标指针移动到 **HTML** 窗口。 移动鼠标指针时，Page Inspector 在 **HTML** 窗口中勾勒元素，并在浏览器窗口中突出显示相应的元素。

![HTML 窗口](using-page-inspector-in-aspnet-mvc/_static/image22.png)

与之前一样，Page Inspector 将 \_ 在临时选项卡中打开 layout 文件。单击 "布局" " \_ 临时" 选项卡，将在 &lt; 标头部分中突出显示相应的标记 &gt; ：

![突出显示标记](using-page-inspector-in-aspnet-mvc/_static/image24.png)

<a id="_using_page_inspector"></a><a id="_7_previewing_css"></a>

## <a name="preview-css-changes-in-the-styles-window"></a>在 "样式" 窗口中预览 CSS 更改

接下来，您将使用 "Page Inspector **样式** " 窗口来预览 CSS 的更改。

单击 " **检查** " 以将 Page Inspector 置于检查模式。

在 "Page Inspector 浏览器" 窗口中，将鼠标指针移动到 "主页" 部分，直到显示 " **div. 内容包装** 器" 标签。

![悬停在 div 上。内容包装](using-page-inspector-in-aspnet-mvc/_static/image26.png)

在 div. 内容包装部分中单击一次，然后将鼠标指针移动到 " **样式** " 窗口。 " **样式** " 窗口显示此元素的所有 CSS 规则。 向下滚动以查找 ""。 现在清除背景色属性的复选框。

![清除背景色](using-page-inspector-in-aspnet-mvc/_static/image28.png)

请注意如何在 Page Inspector 浏览器窗口中立即更改预览。

再次选中此复选框，然后双击属性值并将其更改为红色。 更改将立即显示：

![红色背景色](using-page-inspector-in-aspnet-mvc/_static/image30.png)

在将更改提交到样式表本身之前，" **样式** " 窗口可让你轻松地测试和预览 CSS 更改。

<a id="css_auto_sync"></a>
## <a name="css-auto-sync"></a>CSS 自动同步

> [!NOTE]
> 此功能需要 Page Inspector 1.3 版。

使用 CSS 自动同步功能，可以直接编辑 CSS 文件，并立即在 Page Inspector 浏览器中查看更改。

单击 " **检查** " 以将 Page Inspector 置于检查模式。

在 "Page Inspector 浏览器" 中，将鼠标指针移动到 "主页" 部分，直到显示 " **div. 内容包装** 器" 标签。 单击 "一次" 以选择此元素。

" **样式** " 窗口显示此元素的所有 CSS 规则。 向下滚动以查找 ""。 单击 "."。 Page Inspector 打开定义此样式的 CSS 文件 ("站点导航) 并突出显示相应的 CSS 样式。

![](using-page-inspector-in-aspnet-mvc/_static/image32.png)

现在，将的值更改 `background-color` 为 "red"。 更改会立即显示在 Page Inspector 浏览器中。

![](using-page-inspector-in-aspnet-mvc/_static/image34.png)

<a id="css_color_picker"></a>
## <a name="using-the-css-color-picker"></a>使用 CSS 颜色选取器

Visual Studio 2012 中的 CSS 编辑器提供了一个颜色选取器，使您可以轻松地选择和插入颜色。 颜色选取器包含一种标准颜色调色板，支持标准颜色名称、哈希代码、RGB、RGBA、HSL 和 HSLA 颜色，并维护最近在文档中使用的颜色的列表。

在上一部分中，你更改了属性的值 `background-color` 。 若要调用颜色选取器，请将插入点放在属性名称和类型 **#** 或 **rgb (** 后面。

![CSS 颜色选取器栏](using-page-inspector-in-aspnet-mvc/_static/image36.png)

单击某一颜色以将其选中，或按向下箭头键，然后使用向左箭头和向右箭头键来遍历这些颜色。 访问颜色时，会预览相应的十六进制值：

![已预览背景色属性值](using-page-inspector-in-aspnet-mvc/_static/image38.png)

如果颜色条没有您所需的确切颜色，可以使用 "颜色选取器" 弹出窗口。 若要打开它，请单击颜色栏右端的双 v 形 v 形，或在键盘上按向下键一次或两次。

![CSS 颜色选取器弹出窗口](using-page-inspector-in-aspnet-mvc/_static/image40.png)

单击右侧垂直条中的颜色。 这会在主窗口中显示该颜色的渐变。 按 Enter 键直接从竖线中选择一种颜色，或单击主窗口中的任何点以选择更高的精度。

如果计算机屏幕上有一种要使用的颜色 (它不必位于 Visual Studio 用户界面) 中，则可以使用右下方的吸管工具捕获其值。

还可以通过移动颜色选取器底部的滑块来更改颜色的不透明度。 这样做会将颜色值更改为 RGBA 值，因为 RGBA 格式可以表示不透明度。

选择一种颜色后，按 Enter，然后键入一个分号来完成 *站点导航* 文件中的背景色项。

<a id="_the_update_bar"></a>

### <a name="the-page-inspector-update-bar"></a>Page Inspector 更新栏

Page Inspector 立即检测到对 *web.config* 文件所做的更改，并在更新栏中显示警报。

![更新栏](using-page-inspector-in-aspnet-mvc/_static/image42.png)

若要保存所有文件并刷新 Page Inspector 浏览器，请按 Ctrl + Alt + Enter，或单击更新栏。 突出显示颜色的更改会显示在浏览器中。

<a id="map_dynamic_elements"></a>
## <a name="mapping-dynamic-page-elements-to-javascript"></a>将动态页面元素映射到 JavaScript

在新式 web 应用程序中，通常会动态地利用 JavaScript 生成页面中的元素。 这意味着与这些页面元素对应的 HTML 或 Razor)  (没有静态标记。

利用版本1.3，Page Inspector 现在可以将动态添加到页面的项映射回相应的 JavaScript 代码。 为了演示此功能，我们将使用 [单一页面应用程序 (SPA) 模板](../../../single-page-application/overview/introduction/knockoutjs-template.md)。

> [!NOTE]
> SPA 模板需要 [ASP.NET 和 Web 工具 2012.2](https://go.microsoft.com/fwlink/?LinkId=282650) 更新。

在 Visual Studio 中，依次选择“文件”**“新建项目”** &gt; ****。 在左侧，展开 " **Visual c #**"，选择 " **Web**"，然后选择 " **ASP.NET MVC4 Web 应用程序**"。 单击“确定”。 

在 " **新建 ASP.NET MVC 4 项目** " 对话框中，选择 " **单页面应用程序**"。

在解决方案资源管理器中，展开 " **Views** " 文件夹，然后展开 " **主** 文件夹"。 右键单击 "索引 ..." 文件，然后选择 **"在 Page Inspector 中查看**"。

Page Inspector 浏览器中显示的第一件事是登录页。 单击 "注册"，创建用户名和密码。 注册后，应用程序会将你登录，并创建待办事项列表，其中包含一些示例项。

单击 " **检查** " 以将 Page Inspector 置于检查模式。 在 Page Inspector 浏览器中，单击其中一个待办事项。 请注意，元素以橙色突出显示，而不是以蓝色突出显示，元素名称旁边有 "JS"。 这表明该元素是通过脚本动态创建的。

![](using-page-inspector-in-aspnet-mvc/_static/image44.png)

此外，" **调用堆栈** " 选项卡上会显示橙色下划线。这指示 " **调用堆栈** " 窗格包含有关元素的详细信息。

单击 " **调用堆栈** " 选项卡。" **调用堆栈** " 窗格显示创建元素的 JavaScript 调用的调用堆栈。 对诸如 jQuery 的外部库的调用会折叠，因此你可以轻松地查看对应用程序脚本的调用。

![](using-page-inspector-in-aspnet-mvc/_static/image46.png)

若要查看完整的堆栈（包括对外部库的调用），可以展开标记为 "外部库" 的节点：

![](using-page-inspector-in-aspnet-mvc/_static/image48.png)

如果单击调用堆栈中的某个项，则 Visual Studio 将打开该代码文件并突出显示相应的脚本。

![](using-page-inspector-in-aspnet-mvc/_static/image50.png)

## <a name="see-also"></a>另请参阅

介绍[如何将 ASP.NET MVC 4 与 Visual Studio](../older-versions/getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4.md) (ASP.net 网站) 

 (第9频道[Page Inspector 简介](https://channel9.msdn.com/posts/visual-studio-vnext-introducing-page-inspector/)) 

 (MSDN) [Page Inspector 错误消息](https://go.microsoft.com/?linkid=9813062)

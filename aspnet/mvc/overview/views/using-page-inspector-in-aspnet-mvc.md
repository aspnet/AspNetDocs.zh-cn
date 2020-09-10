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
# <a name="using-page-inspector-in-aspnet-mvc"></a><span data-ttu-id="d5df0-104">在 ASP.NET MVC 中使用 Page Inspector</span><span class="sxs-lookup"><span data-stu-id="d5df0-104">Using Page Inspector in ASP.NET MVC</span></span>

<span data-ttu-id="d5df0-105">通过 Tim Ammann</span><span class="sxs-lookup"><span data-stu-id="d5df0-105">by Tim Ammann</span></span>

> <span data-ttu-id="d5df0-106">Visual Studio 2012 中的 Page Inspector 是一种使用集成浏览器的 web 开发工具。</span><span class="sxs-lookup"><span data-stu-id="d5df0-106">Page Inspector in Visual Studio 2012 is a web development tool with an integrated browser.</span></span> <span data-ttu-id="d5df0-107">在集成浏览器中选择任意元素，Page Inspector 会立即突出显示该元素的源和 CSS。</span><span class="sxs-lookup"><span data-stu-id="d5df0-107">Select any element in the integrated browser, and Page Inspector instantly highlights the element's source and CSS.</span></span> <span data-ttu-id="d5df0-108">您可以浏览任意 MVC 视图，快速找到所呈现标记的源，并直接在 Visual Studio 环境中使用浏览器工具。</span><span class="sxs-lookup"><span data-stu-id="d5df0-108">You can browse any MVC view, quickly find the sources of rendered markup, and use browser tools right within the Visual Studio environment.</span></span>
> 
> [<span data-ttu-id="d5df0-109">观看视频</span><span class="sxs-lookup"><span data-stu-id="d5df0-109">Watch the Video</span></span>](../../videos/mvc-4/using-page-inspector-in-aspnet-mvc.md)
> 
> <span data-ttu-id="d5df0-110">本教程演示如何启用检查模式，然后在你的 web 项目中快速查找和编辑标记和 CSS。</span><span class="sxs-lookup"><span data-stu-id="d5df0-110">This tutorial shows how to enable Inspection Mode, and then quickly locate and edit markup and CSS within your web project.</span></span> <span data-ttu-id="d5df0-111">本教程使用 MVC 项目，但你也可以将 Page Inspector 用于 [Web 窗体](https://go.microsoft.com/?linkid=9802001) 和其他 ASP.NET 应用程序。</span><span class="sxs-lookup"><span data-stu-id="d5df0-111">The tutorial uses an MVC Project, but you can also use Page Inspector for [Web Forms](https://go.microsoft.com/?linkid=9802001) and other ASP.NET applications.</span></span>
> 
> <span data-ttu-id="d5df0-112">本教程包含以下部分：</span><span class="sxs-lookup"><span data-stu-id="d5df0-112">The tutorial has the following sections:</span></span>
> 
> - [<span data-ttu-id="d5df0-113">先决条件</span><span class="sxs-lookup"><span data-stu-id="d5df0-113">Prerequisites</span></span>](#_1_prerequisites)
> - [<span data-ttu-id="d5df0-114">创建 Web 应用程序</span><span class="sxs-lookup"><span data-stu-id="d5df0-114">Create a Web Application</span></span>](#_2_creating_a)
> - [<span data-ttu-id="d5df0-115">使用 Page Inspector 浏览到视图</span><span class="sxs-lookup"><span data-stu-id="d5df0-115">Use Page Inspector to Browse to a View</span></span>](#_3_using_page)
> - [<span data-ttu-id="d5df0-116">启用检查模式</span><span class="sxs-lookup"><span data-stu-id="d5df0-116">Enable Inspection Mode</span></span>](#_4_inspection_mode)
> - [<span data-ttu-id="d5df0-117">使用 Page Inspector 对标记进行更改</span><span class="sxs-lookup"><span data-stu-id="d5df0-117">Use Page Inspector to Make Changes to Markup</span></span>](#_5_using_page)
> - [<span data-ttu-id="d5df0-118">检查模式和 HTML 窗口</span><span class="sxs-lookup"><span data-stu-id="d5df0-118">Inspection Mode and the HTML Window</span></span>](#_6_inspection_mode)
> - [<span data-ttu-id="d5df0-119">在 "样式" 窗口中预览 CSS 更改</span><span class="sxs-lookup"><span data-stu-id="d5df0-119">Preview CSS Changes in the Styles window</span></span>](#_7_previewing_css)
> - [<span data-ttu-id="d5df0-120">CSS 自动同步</span><span class="sxs-lookup"><span data-stu-id="d5df0-120">CSS Auto Sync</span></span>](#css_auto_sync)
> - [<span data-ttu-id="d5df0-121">使用 CSS 颜色选取器</span><span class="sxs-lookup"><span data-stu-id="d5df0-121">Using the CSS Color Picker</span></span>](#css_color_picker)
> - [<span data-ttu-id="d5df0-122">将动态页面元素映射到 JavaScript</span><span class="sxs-lookup"><span data-stu-id="d5df0-122">Mapping Dynamic Page Elements to JavaScript</span></span>](#map_dynamic_elements)

<a id="_prerequisites"></a><a id="_1_prerequisites"></a>

## <a name="prerequisites"></a><span data-ttu-id="d5df0-123">先决条件</span><span class="sxs-lookup"><span data-stu-id="d5df0-123">Prerequisites</span></span>

- <span data-ttu-id="d5df0-124">[用于 Web 的](https://www.microsoft.com/visualstudio/11/downloads#express-web) [Visual Studio 2012](https://www.microsoft.com/visualstudio/11)或 Visual Studio Express 2012。</span><span class="sxs-lookup"><span data-stu-id="d5df0-124">[Visual Studio 2012](https://www.microsoft.com/visualstudio/11) or [Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web).</span></span>

> [!NOTE]
> <span data-ttu-id="d5df0-125">若要获取最新版本的 Page Inspector，请使用 [Web 平台安装程序](https://go.microsoft.com/fwlink/?LinkId=255386) 安装适用于 .net 2.0 的 MICROSOFT Azure SDK。</span><span class="sxs-lookup"><span data-stu-id="d5df0-125">To get the latest version of Page Inspector, use [Web Platform Installer](https://go.microsoft.com/fwlink/?LinkId=255386) to install the Windows Azure SDK for .NET 2.0.</span></span>

<span data-ttu-id="d5df0-126">Page Inspector 与 Microsoft Web 开发人员工具捆绑在一起。</span><span class="sxs-lookup"><span data-stu-id="d5df0-126">Page Inspector is bundled with Microsoft Web Developer Tools.</span></span> <span data-ttu-id="d5df0-127">最新版本为1.3。</span><span class="sxs-lookup"><span data-stu-id="d5df0-127">The latest version is 1.3.</span></span> <span data-ttu-id="d5df0-128">若要检查你的版本，请运行 Visual Studio，然后从 "**帮助**" 菜单中选择 "**关于 Microsoft Visual Studio** 。</span><span class="sxs-lookup"><span data-stu-id="d5df0-128">To check which version you have, run Visual Studio and select **About Microsoft Visual Studio** from the **Help** menu.</span></span>

<a id="_creating_a_web"></a><a id="_2_creating_a"></a>

## <a name="create-a-web-application"></a><span data-ttu-id="d5df0-129">创建 Web 应用程序</span><span class="sxs-lookup"><span data-stu-id="d5df0-129">Create a Web Application</span></span>

<span data-ttu-id="d5df0-130">首先，创建将 Page Inspector 使用的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="d5df0-130">First, create a web application that you will use Page Inspector with.</span></span> <span data-ttu-id="d5df0-131">在 Visual Studio 中，依次选择“文件”**“新建项目”** &gt; \*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="d5df0-131">In Visual Studio, choose **File** &gt; **New Project**.</span></span> <span data-ttu-id="d5df0-132">在左侧，展开 " **Visual c #**"，选择 " **Web**"，然后选择 " **ASP.NET MVC4 Web 应用程序**"。</span><span class="sxs-lookup"><span data-stu-id="d5df0-132">On the left, expand **Visual C#**, select **Web**, and then select **ASP.NET MVC4 Web Application**.</span></span>

![New ASP.NET MVC 应用程序](using-page-inspector-in-aspnet-mvc/_static/image2.png)

<span data-ttu-id="d5df0-134">单击“确定”。 </span><span class="sxs-lookup"><span data-stu-id="d5df0-134">Click **OK**.</span></span>

<span data-ttu-id="d5df0-135">在 " **新建 ASP.NET MVC 4 项目** " 对话框中，选择 " **Internet 应用程序**"。</span><span class="sxs-lookup"><span data-stu-id="d5df0-135">In the **New ASP.NET MVC 4 Project** dialog box, select **Internet Application**.</span></span> <span data-ttu-id="d5df0-136">保留 **Razor** 作为默认视图引擎。</span><span class="sxs-lookup"><span data-stu-id="d5df0-136">Leave **Razor** as the default view engine.</span></span>

![New ASP.NET MVC 项目-Internet 应用程序](using-page-inspector-in-aspnet-mvc/_static/image4.png)

<span data-ttu-id="d5df0-138">应用程序将在 " **源** " 视图中打开。</span><span class="sxs-lookup"><span data-stu-id="d5df0-138">The application opens in **Source** view.</span></span>

![源视图中的新 ASP.NET MVC 应用程序](using-page-inspector-in-aspnet-mvc/_static/image6.png)

<span data-ttu-id="d5df0-140">现在，你已经有了要使用的应用程序，可以使用 Page Inspector 来检查和修改它。</span><span class="sxs-lookup"><span data-stu-id="d5df0-140">Now that you have an application to work with, you can use Page Inspector to examine and modify it.</span></span>

<a id="_starting_page_inspector"></a><a id="_3_using_page"></a>

## <a name="use-page-inspector-to-browse-to-a-view"></a><span data-ttu-id="d5df0-141">使用 Page Inspector 浏览到视图</span><span class="sxs-lookup"><span data-stu-id="d5df0-141">Use Page Inspector to Browse to a View</span></span>

<span data-ttu-id="d5df0-142">在 Visual Studio 2012 中，可以右键单击项目中的任何视图， **在 Page Inspector**中选择 "查看"，然后 Page Inspector 将找出路由并显示页面。</span><span class="sxs-lookup"><span data-stu-id="d5df0-142">In Visual Studio 2012, you can right-click any view in your project, select **View in Page Inspector**, and Page Inspector will figure out the route and display the page.</span></span>

<span data-ttu-id="d5df0-143">在 **解决方案资源管理器**中，展开 " **Views** " 文件夹，然后展开 " **主** 文件夹"。</span><span class="sxs-lookup"><span data-stu-id="d5df0-143">In **Solution Explorer**, expand the **Views** folder and then the **Home** folder.</span></span> <span data-ttu-id="d5df0-144">右键单击 "索引 ..." 文件，然后选择 **"在 Page Inspector 中查看**"。</span><span class="sxs-lookup"><span data-stu-id="d5df0-144">Right click the Index.cshtml file and choose **View in Page Inspector**.</span></span>

![Page Inspector 中查看索引 .。。](using-page-inspector-in-aspnet-mvc/_static/image8.png)

<span data-ttu-id="d5df0-146">默认情况下，Page Inspector 作为窗口停靠在 Visual Studio 环境的左侧。</span><span class="sxs-lookup"><span data-stu-id="d5df0-146">By default, Page Inspector is docked as a window on the left side of the Visual Studio environment.</span></span> <span data-ttu-id="d5df0-147">如果需要，可以将其固定到其他位置，或取消停靠窗口。</span><span class="sxs-lookup"><span data-stu-id="d5df0-147">If you prefer, you can dock it elsewhere, or undock the window.</span></span> <span data-ttu-id="d5df0-148">请参阅 [如何：排列和停靠窗口](https://msdn.microsoft.com/library/z4y0hsax.aspx)。</span><span class="sxs-lookup"><span data-stu-id="d5df0-148">See [How to: Arrange and Dock Windows](https://msdn.microsoft.com/library/z4y0hsax.aspx).</span></span>

<span data-ttu-id="d5df0-149">"Page Inspector" 窗口的顶部窗格显示浏览器窗口中的当前页。</span><span class="sxs-lookup"><span data-stu-id="d5df0-149">The top pane of the Page Inspector window shows the current page in a browser window.</span></span> <span data-ttu-id="d5df0-150">下窗格显示 HTML 标记中的页面，以及一些选项卡，可用于检查页面的不同方面。</span><span class="sxs-lookup"><span data-stu-id="d5df0-150">The bottom pane shows the page in HTML markup, along with some tabs that let you inspect different aspects of the page.</span></span> <span data-ttu-id="d5df0-151">底部窗格类似于 Internet Explorer 中的 [F12 开发人员工具](https://msdn.microsoft.com/ie/aa740478) 。</span><span class="sxs-lookup"><span data-stu-id="d5df0-151">The bottom pane is similar to the [F12 Developer Tools](https://msdn.microsoft.com/ie/aa740478) in Internet Explorer.</span></span>

![Page Inspector 中的 ASP.NET MVC 应用程序](using-page-inspector-in-aspnet-mvc/_static/image10.png)

<span data-ttu-id="d5df0-153">在本教程中，您将使用 " **HTML** " 和 " **样式** " 选项卡快速导航并对应用程序进行更改。</span><span class="sxs-lookup"><span data-stu-id="d5df0-153">In this tutorial, you will use the **HTML** and **Styles** tabs to navigate quickly and make changes to the application.</span></span>

<a id="_examining_(&quot;decomposing&quot;)_the"></a><a id="_inspection_mode_and"></a><a id="_4_inspection_mode"></a>

## <a name="enableinspection-mode"></a><span data-ttu-id="d5df0-154">EnableInspection 模式</span><span class="sxs-lookup"><span data-stu-id="d5df0-154">EnableInspection Mode</span></span>

<span data-ttu-id="d5df0-155">若要将 Page Inspector 放入检查模式中，请单击 " **检查** " 按钮。</span><span class="sxs-lookup"><span data-stu-id="d5df0-155">To put Page Inspector into Inspection Mode, click the **Inspect** button.</span></span> <span data-ttu-id="d5df0-156">在检查模式中，当您将鼠标指针悬停在呈现的页的任何部分时，相应的源标记或代码会突出显示。</span><span class="sxs-lookup"><span data-stu-id="d5df0-156">In Inspection Mode, when you hold the mouse pointer over any part of the rendered page, the corresponding source markup or code is highlighted.</span></span>

![切换检查模式](using-page-inspector-in-aspnet-mvc/_static/image12.png)

<span data-ttu-id="d5df0-158">现在，将鼠标移动到 Page Inspector 内页面的不同部分。</span><span class="sxs-lookup"><span data-stu-id="d5df0-158">Now move your mouse over different parts of the page within Page Inspector.</span></span> <span data-ttu-id="d5df0-159">正如你所做的那样，鼠标指针将更改为大加号，并突出显示下面的元素：</span><span class="sxs-lookup"><span data-stu-id="d5df0-159">As you do, the mouse pointer changes to a large plus sign, and the element underneath is highlighted:</span></span>

![悬停在 div 上。内容包装](using-page-inspector-in-aspnet-mvc/_static/image14.png)

<span data-ttu-id="d5df0-161">移动鼠标指针时，Visual Studio 会突出显示源文件中的相应 Razor 语法。</span><span class="sxs-lookup"><span data-stu-id="d5df0-161">As you move the mouse pointer, Visual Studio highlights the corresponding Razor syntax in the source file.</span></span> <span data-ttu-id="d5df0-162">如果 HTML 元素来自其他源文件，则 Visual Studio 会自动打开该文件。</span><span class="sxs-lookup"><span data-stu-id="d5df0-162">If the HTML element comes from another source file, Visual Studio automatically opens the file.</span></span>

<span data-ttu-id="d5df0-163">在 Page Inspector 中， **html** 选项卡显示从 Razor 语法生成的 html。</span><span class="sxs-lookup"><span data-stu-id="d5df0-163">In Page Inspector, the **HTML** tab shows the HTML that was generated from the Razor syntax.</span></span> <span data-ttu-id="d5df0-164">移动鼠标指针时，会突出显示 HTML 元素。</span><span class="sxs-lookup"><span data-stu-id="d5df0-164">As you move the mouse pointer, the HTML elements are highlighted.</span></span> <span data-ttu-id="d5df0-165">" **样式** " 选项卡显示元素的 CSS 规则。</span><span class="sxs-lookup"><span data-stu-id="d5df0-165">The **Styles** tab shows the CSS rules for the element.</span></span>

<a id="_5_using_page"></a>

## <a name="use-page-inspector-to-make-changes-to-markup"></a><span data-ttu-id="d5df0-166">使用 Page Inspector 对标记进行更改</span><span class="sxs-lookup"><span data-stu-id="d5df0-166">Use Page Inspector to Make Changes to Markup</span></span>

<span data-ttu-id="d5df0-167">Page Inspector 允许你查找位置可能不明显的标记。</span><span class="sxs-lookup"><span data-stu-id="d5df0-167">Page Inspector lets you find markup whose location might not be obvious.</span></span> <span data-ttu-id="d5df0-168">然后，可以修改标记并查看生成的更改。</span><span class="sxs-lookup"><span data-stu-id="d5df0-168">Then you can modify the markup and see the resulting changes.</span></span>

<span data-ttu-id="d5df0-169">若要查看此项，请单击 " **检查** "，然后滚动到页面底部的 "Page Inspector" 窗口。</span><span class="sxs-lookup"><span data-stu-id="d5df0-169">To see this, click **Inspect** and then scroll to the bottom of the page in the Page Inspector window.</span></span>

<span data-ttu-id="d5df0-170">将鼠标指针移动到页脚区时，Page Inspector 打开 "layout" \_ 文件并突出显示所选布局页的部分。</span><span class="sxs-lookup"><span data-stu-id="d5df0-170">When you move the mouse pointer into the footer area, Page Inspector opens the \_Layout.cshtml file and highlights the section of the layout page that you have selected.</span></span> <span data-ttu-id="d5df0-171">正如您所看到的，页脚区域是在布局文件中定义的，而不是在视图本身中定义的。</span><span class="sxs-lookup"><span data-stu-id="d5df0-171">As you can see, the footer area is defined in the layout file, and not the view itself.</span></span>

![脚注](using-page-inspector-in-aspnet-mvc/_static/image16.png)

<span data-ttu-id="d5df0-173">现在，将鼠标指针移动到带有版权声明的行上 <a id="a"></a> 。</span><span class="sxs-lookup"><span data-stu-id="d5df0-173">Now move your mouse pointer over the line with the copyright <a id="a"></a>notice.</span></span> <span data-ttu-id="d5df0-174">在 \_ Layout 页面中，将突出显示相应的行。</span><span class="sxs-lookup"><span data-stu-id="d5df0-174">In the \_Layout.cshtml page, the corresponding line is highlighted.</span></span>

![突出显示了页脚版权行](using-page-inspector-in-aspnet-mvc/_static/image18.png)

<span data-ttu-id="d5df0-176">将一些文本添加到布局 cshtml 文件中行的末尾 \_ 。</span><span class="sxs-lookup"><span data-stu-id="d5df0-176">Add some text to the end of the line in the \_Layout.cshtml file.</span></span>

<span data-ttu-id="d5df0-177">&lt;p &gt; &amp; copy; @DateTime.Now.Year -我的 ASP.NET MVC 应用程序 Rocks！ &lt;/p&gt;</span><span class="sxs-lookup"><span data-stu-id="d5df0-177">&lt;p&gt;&amp;copy; @DateTime.Now.Year - My ASP.NET MVC Application Rocks!&lt;/p&gt;</span></span>

<span data-ttu-id="d5df0-178">现在，按 Ctrl + Alt + Enter，或单击 "更新" 栏以在 "Page Inspector 浏览器" 窗口中查看结果。</span><span class="sxs-lookup"><span data-stu-id="d5df0-178">Now, press Ctrl+Alt+Enter or click the Update Bar to see the results in the Page Inspector browser window.</span></span>

![我的 ASP.NET 应用程序 Rocks！](using-page-inspector-in-aspnet-mvc/_static/image20.png)

<span data-ttu-id="d5df0-180">您可能认为在索引中定义了注脚，但它已在 \_ Layout 中提供，并 Page Inspector 找到了它。</span><span class="sxs-lookup"><span data-stu-id="d5df0-180">You might have thought that the footer defined in Index.cshtml, but it turned out to be in the \_Layout.cshtml, and Page Inspector found it for you.</span></span>

<a id="_inspection_mode_and_1"></a><a id="_6_inspection_mode"></a>

## <a name="inspection-mode-and-the-html-window"></a><span data-ttu-id="d5df0-181">检查模式和 HTML 窗口</span><span class="sxs-lookup"><span data-stu-id="d5df0-181">Inspection Mode and the HTML Window</span></span>

<span data-ttu-id="d5df0-182">接下来，您将快速了解 HTML 窗口以及它如何为您映射元素。</span><span class="sxs-lookup"><span data-stu-id="d5df0-182">Next, you will have a quick look at the HTML window and how it maps elements for you.</span></span>

<span data-ttu-id="d5df0-183">单击 " **检查** " 以将 Page Inspector 置于检查模式。</span><span class="sxs-lookup"><span data-stu-id="d5df0-183">Click **Inspect** to put Page Inspector in Inspection Mode.</span></span>

<span data-ttu-id="d5df0-184">单击 "此处显示徽标" 页面的顶部部分。</span><span class="sxs-lookup"><span data-stu-id="d5df0-184">Click the top part of the page that says "Your logo here".</span></span> <span data-ttu-id="d5df0-185">您将更详细地检查特定元素，因此，在浏览器窗口中显示的内容将不再随着鼠标指针的移动而改变。</span><span class="sxs-lookup"><span data-stu-id="d5df0-185">You are examining a particular element in more detail, so the display in the browser window no longer changes as you move the mouse pointer.</span></span>

<span data-ttu-id="d5df0-186">现在，将鼠标指针移动到 **HTML** 窗口。</span><span class="sxs-lookup"><span data-stu-id="d5df0-186">Now move the mouse pointer to the **HTML** window.</span></span> <span data-ttu-id="d5df0-187">移动鼠标指针时，Page Inspector 在 **HTML** 窗口中勾勒元素，并在浏览器窗口中突出显示相应的元素。</span><span class="sxs-lookup"><span data-stu-id="d5df0-187">As you move the mouse pointer, Page Inspector outlines the element within the **HTML** window and highlights the corresponding element in the browser window.</span></span>

![HTML 窗口](using-page-inspector-in-aspnet-mvc/_static/image22.png)

<span data-ttu-id="d5df0-189">与之前一样，Page Inspector 将 \_ 在临时选项卡中打开 layout 文件。单击 "布局" " \_ 临时" 选项卡，将在 &lt; 标头部分中突出显示相应的标记 &gt; ：</span><span class="sxs-lookup"><span data-stu-id="d5df0-189">As before, Page Inspector opens the \_Layout.cshtml file for you in a temporary tab. Click the \_Layout.cshtml temporary tab, and the corresponding markup will be highlighted in the &lt;header&gt; section for you:</span></span>

![突出显示标记](using-page-inspector-in-aspnet-mvc/_static/image24.png)

<a id="_using_page_inspector"></a><a id="_7_previewing_css"></a>

## <a name="preview-css-changes-in-the-styles-window"></a><span data-ttu-id="d5df0-191">在 "样式" 窗口中预览 CSS 更改</span><span class="sxs-lookup"><span data-stu-id="d5df0-191">Preview CSS Changes in the Styles Window</span></span>

<span data-ttu-id="d5df0-192">接下来，您将使用 "Page Inspector **样式** " 窗口来预览 CSS 的更改。</span><span class="sxs-lookup"><span data-stu-id="d5df0-192">Next, you will use the Page Inspector **Styles** window to preview changes to CSS.</span></span>

<span data-ttu-id="d5df0-193">单击 " **检查** " 以将 Page Inspector 置于检查模式。</span><span class="sxs-lookup"><span data-stu-id="d5df0-193">Click **Inspect** to put Page Inspector in Inspection Mode.</span></span>

<span data-ttu-id="d5df0-194">在 "Page Inspector 浏览器" 窗口中，将鼠标指针移动到 "主页" 部分，直到显示 " **div. 内容包装** 器" 标签。</span><span class="sxs-lookup"><span data-stu-id="d5df0-194">In the Page Inspector browser window, move the mouse pointer over the "Home Page" section until the **div.content-wrapper** label appears.</span></span>

![悬停在 div 上。内容包装](using-page-inspector-in-aspnet-mvc/_static/image26.png)

<span data-ttu-id="d5df0-196">在 div. 内容包装部分中单击一次，然后将鼠标指针移动到 " **样式** " 窗口。</span><span class="sxs-lookup"><span data-stu-id="d5df0-196">Click within the div.content-wrapper section once, and then move the mouse pointer to the **Styles** window.</span></span> <span data-ttu-id="d5df0-197">" **样式** " 窗口显示此元素的所有 CSS 规则。</span><span class="sxs-lookup"><span data-stu-id="d5df0-197">The **Styles** window shows all of the CSS rules for this element.</span></span> <span data-ttu-id="d5df0-198">向下滚动以查找 ""。</span><span class="sxs-lookup"><span data-stu-id="d5df0-198">Scroll down to find the .featured .content-wrapper class selector.</span></span> <span data-ttu-id="d5df0-199">现在清除背景色属性的复选框。</span><span class="sxs-lookup"><span data-stu-id="d5df0-199">Now clear the checkbox for the background-color property.</span></span>

![清除背景色](using-page-inspector-in-aspnet-mvc/_static/image28.png)

<span data-ttu-id="d5df0-201">请注意如何在 Page Inspector 浏览器窗口中立即更改预览。</span><span class="sxs-lookup"><span data-stu-id="d5df0-201">Notice how the change previews instantly in the Page Inspector browser window.</span></span>

<span data-ttu-id="d5df0-202">再次选中此复选框，然后双击属性值并将其更改为红色。</span><span class="sxs-lookup"><span data-stu-id="d5df0-202">Select the checkbox again, then double-click the property value and change it to red.</span></span> <span data-ttu-id="d5df0-203">更改将立即显示：</span><span class="sxs-lookup"><span data-stu-id="d5df0-203">The change shows immediately:</span></span>

![红色背景色](using-page-inspector-in-aspnet-mvc/_static/image30.png)

<span data-ttu-id="d5df0-205">在将更改提交到样式表本身之前，" **样式** " 窗口可让你轻松地测试和预览 CSS 更改。</span><span class="sxs-lookup"><span data-stu-id="d5df0-205">The **Styles** window makes it easy to test and preview CSS changes before you commit the changes to the style sheet itself.</span></span>

<a id="css_auto_sync"></a>
## <a name="css-auto-sync"></a><span data-ttu-id="d5df0-206">CSS 自动同步</span><span class="sxs-lookup"><span data-stu-id="d5df0-206">CSS Auto Sync</span></span>

> [!NOTE]
> <span data-ttu-id="d5df0-207">此功能需要 Page Inspector 1.3 版。</span><span class="sxs-lookup"><span data-stu-id="d5df0-207">This feature requires version 1.3 of Page Inspector.</span></span>

<span data-ttu-id="d5df0-208">使用 CSS 自动同步功能，可以直接编辑 CSS 文件，并立即在 Page Inspector 浏览器中查看更改。</span><span class="sxs-lookup"><span data-stu-id="d5df0-208">The CSS Auto-Sync feature allows you to edit a CSS file directly, and see the changes immediately in the Page Inspector browser.</span></span>

<span data-ttu-id="d5df0-209">单击 " **检查** " 以将 Page Inspector 置于检查模式。</span><span class="sxs-lookup"><span data-stu-id="d5df0-209">Click **Inspect** to put Page Inspector in Inspection Mode.</span></span>

<span data-ttu-id="d5df0-210">在 "Page Inspector 浏览器" 中，将鼠标指针移动到 "主页" 部分，直到显示 " **div. 内容包装** 器" 标签。</span><span class="sxs-lookup"><span data-stu-id="d5df0-210">In the Page Inspector browser, move the mouse pointer over the "Home Page" section until the **div.content-wrapper** label appears.</span></span> <span data-ttu-id="d5df0-211">单击 "一次" 以选择此元素。</span><span class="sxs-lookup"><span data-stu-id="d5df0-211">Click once to select this element.</span></span>

<span data-ttu-id="d5df0-212">" **样式** " 窗口显示此元素的所有 CSS 规则。</span><span class="sxs-lookup"><span data-stu-id="d5df0-212">The **Styles** window shows all of the CSS rules for this element.</span></span> <span data-ttu-id="d5df0-213">向下滚动以查找 ""。</span><span class="sxs-lookup"><span data-stu-id="d5df0-213">Scroll down to find the .featured .content-wrapper class selector.</span></span> <span data-ttu-id="d5df0-214">单击 "."。</span><span class="sxs-lookup"><span data-stu-id="d5df0-214">Click on ".featured .content-wrapper".</span></span> <span data-ttu-id="d5df0-215">Page Inspector 打开定义此样式的 CSS 文件 ("站点导航) 并突出显示相应的 CSS 样式。</span><span class="sxs-lookup"><span data-stu-id="d5df0-215">Page Inspector opens the CSS file that defines this style (Site.css) and highlights the corresponding CSS style.</span></span>

![](using-page-inspector-in-aspnet-mvc/_static/image32.png)

<span data-ttu-id="d5df0-216">现在，将的值更改 `background-color` 为 "red"。</span><span class="sxs-lookup"><span data-stu-id="d5df0-216">Now change the value for `background-color` to "red".</span></span> <span data-ttu-id="d5df0-217">更改会立即显示在 Page Inspector 浏览器中。</span><span class="sxs-lookup"><span data-stu-id="d5df0-217">The change appears immediately in the Page Inspector browser.</span></span>

![](using-page-inspector-in-aspnet-mvc/_static/image34.png)

<a id="css_color_picker"></a>
## <a name="using-the-css-color-picker"></a><span data-ttu-id="d5df0-218">使用 CSS 颜色选取器</span><span class="sxs-lookup"><span data-stu-id="d5df0-218">Using the CSS Color Picker</span></span>

<span data-ttu-id="d5df0-219">Visual Studio 2012 中的 CSS 编辑器提供了一个颜色选取器，使您可以轻松地选择和插入颜色。</span><span class="sxs-lookup"><span data-stu-id="d5df0-219">The CSS editor in Visual Studio 2012 has a color picker that makes it easy to choose and insert colors.</span></span> <span data-ttu-id="d5df0-220">颜色选取器包含一种标准颜色调色板，支持标准颜色名称、哈希代码、RGB、RGBA、HSL 和 HSLA 颜色，并维护最近在文档中使用的颜色的列表。</span><span class="sxs-lookup"><span data-stu-id="d5df0-220">The color picker includes a standard palette of colors, supports standard color names, hash codes, RGB, RGBA, HSL, and HSLA colors, and maintains a list of the colors you've used most recently in the document.</span></span>

<span data-ttu-id="d5df0-221">在上一部分中，你更改了属性的值 `background-color` 。</span><span class="sxs-lookup"><span data-stu-id="d5df0-221">In the previous section, you changed the value of the `background-color` property.</span></span> <span data-ttu-id="d5df0-222">若要调用颜色选取器，请将插入点放在属性名称和类型 **#** 或 **rgb (** 后面。</span><span class="sxs-lookup"><span data-stu-id="d5df0-222">To invoke the color picker, place the insertion point after the property name and type **#** or **rgb(**.</span></span>

![CSS 颜色选取器栏](using-page-inspector-in-aspnet-mvc/_static/image36.png)

<span data-ttu-id="d5df0-224">单击某一颜色以将其选中，或按向下箭头键，然后使用向左箭头和向右箭头键来遍历这些颜色。</span><span class="sxs-lookup"><span data-stu-id="d5df0-224">Click on a color to select it, or press the down arrow key and then use the left and right arrow keys to traverse the colors.</span></span> <span data-ttu-id="d5df0-225">访问颜色时，会预览相应的十六进制值：</span><span class="sxs-lookup"><span data-stu-id="d5df0-225">When you visit a color, the corresponding hex value is previewed:</span></span>

![已预览背景色属性值](using-page-inspector-in-aspnet-mvc/_static/image38.png)

<span data-ttu-id="d5df0-227">如果颜色条没有您所需的确切颜色，可以使用 "颜色选取器" 弹出窗口。</span><span class="sxs-lookup"><span data-stu-id="d5df0-227">If the color bar doesn't have the exact color you want, you can use the color picker pop-down.</span></span> <span data-ttu-id="d5df0-228">若要打开它，请单击颜色栏右端的双 v 形 v 形，或在键盘上按向下键一次或两次。</span><span class="sxs-lookup"><span data-stu-id="d5df0-228">To open it, click the double chevron at the right end of the color bar, or press the Down Arrow once or twice on the keyboard.</span></span>

![CSS 颜色选取器弹出窗口](using-page-inspector-in-aspnet-mvc/_static/image40.png)

<span data-ttu-id="d5df0-230">单击右侧垂直条中的颜色。</span><span class="sxs-lookup"><span data-stu-id="d5df0-230">Click a color from the vertical bar on the right.</span></span> <span data-ttu-id="d5df0-231">这会在主窗口中显示该颜色的渐变。</span><span class="sxs-lookup"><span data-stu-id="d5df0-231">This shows a gradient for that color in the main window.</span></span> <span data-ttu-id="d5df0-232">按 Enter 键直接从竖线中选择一种颜色，或单击主窗口中的任何点以选择更高的精度。</span><span class="sxs-lookup"><span data-stu-id="d5df0-232">Choose a color directly from the vertical bar by pressing Enter, or click any point in the main window to choose with greater precision.</span></span>

<span data-ttu-id="d5df0-233">如果计算机屏幕上有一种要使用的颜色 (它不必位于 Visual Studio 用户界面) 中，则可以使用右下方的吸管工具捕获其值。</span><span class="sxs-lookup"><span data-stu-id="d5df0-233">If there is a color on your computer screen that you want to use (it doesn't have to be inside the Visual Studio user interface), you can capture its value by using the eyedropper tool on the lower right.</span></span>

<span data-ttu-id="d5df0-234">还可以通过移动颜色选取器底部的滑块来更改颜色的不透明度。</span><span class="sxs-lookup"><span data-stu-id="d5df0-234">You also can change the opacity of a color by moving the slider at the bottom of the color picker.</span></span> <span data-ttu-id="d5df0-235">这样做会将颜色值更改为 RGBA 值，因为 RGBA 格式可以表示不透明度。</span><span class="sxs-lookup"><span data-stu-id="d5df0-235">Doing so changes color values to RGBA values, because the RGBA format can represent opacity.</span></span>

<span data-ttu-id="d5df0-236">选择一种颜色后，按 Enter，然后键入一个分号来完成 *站点导航* 文件中的背景色项。</span><span class="sxs-lookup"><span data-stu-id="d5df0-236">After you have chosen a color, press Enter, and then type a semicolon to complete the background-color entry in the *Site.css* file.</span></span>

<a id="_the_update_bar"></a>

### <a name="the-page-inspector-update-bar"></a><span data-ttu-id="d5df0-237">Page Inspector 更新栏</span><span class="sxs-lookup"><span data-stu-id="d5df0-237">The Page Inspector Update Bar</span></span>

<span data-ttu-id="d5df0-238">Page Inspector 立即检测到对 *web.config* 文件所做的更改，并在更新栏中显示警报。</span><span class="sxs-lookup"><span data-stu-id="d5df0-238">Page Inspector immediately detects the change to the *Site.css* file and displays an alert in an update bar.</span></span>

![更新栏](using-page-inspector-in-aspnet-mvc/_static/image42.png)

<span data-ttu-id="d5df0-240">若要保存所有文件并刷新 Page Inspector 浏览器，请按 Ctrl + Alt + Enter，或单击更新栏。</span><span class="sxs-lookup"><span data-stu-id="d5df0-240">To save all your files and refresh the Page Inspector browser, press Ctrl+Alt+Enter or click the update bar.</span></span> <span data-ttu-id="d5df0-241">突出显示颜色的更改会显示在浏览器中。</span><span class="sxs-lookup"><span data-stu-id="d5df0-241">The change in the highlight color appears in the browser.</span></span>

<a id="map_dynamic_elements"></a>
## <a name="mapping-dynamic-page-elements-to-javascript"></a><span data-ttu-id="d5df0-242">将动态页面元素映射到 JavaScript</span><span class="sxs-lookup"><span data-stu-id="d5df0-242">Mapping Dynamic Page Elements to JavaScript</span></span>

<span data-ttu-id="d5df0-243">在新式 web 应用程序中，通常会动态地利用 JavaScript 生成页面中的元素。</span><span class="sxs-lookup"><span data-stu-id="d5df0-243">In modern web applications, elements in the page are often generated dynamically with JavaScript.</span></span> <span data-ttu-id="d5df0-244">这意味着与这些页面元素对应的 HTML 或 Razor)  (没有静态标记。</span><span class="sxs-lookup"><span data-stu-id="d5df0-244">That means there is no static markup (either HTML or Razor) that corresponds to these page elements.</span></span>

<span data-ttu-id="d5df0-245">利用版本1.3，Page Inspector 现在可以将动态添加到页面的项映射回相应的 JavaScript 代码。</span><span class="sxs-lookup"><span data-stu-id="d5df0-245">With version 1.3, Page Inspector can now map items that were dynamically added to the page back to the corresponding JavaScript code.</span></span> <span data-ttu-id="d5df0-246">为了演示此功能，我们将使用 [单一页面应用程序 (SPA) 模板](../../../single-page-application/overview/introduction/knockoutjs-template.md)。</span><span class="sxs-lookup"><span data-stu-id="d5df0-246">To demonstrate this feature, we'll use the [Single Page Application (SPA) template](../../../single-page-application/overview/introduction/knockoutjs-template.md).</span></span>

> [!NOTE]
> <span data-ttu-id="d5df0-247">SPA 模板需要 [ASP.NET 和 Web 工具 2012.2](https://go.microsoft.com/fwlink/?LinkId=282650) 更新。</span><span class="sxs-lookup"><span data-stu-id="d5df0-247">The SPA template requires the [ASP.NET and Web Tools 2012.2](https://go.microsoft.com/fwlink/?LinkId=282650) update.</span></span>

<span data-ttu-id="d5df0-248">在 Visual Studio 中，依次选择“文件”**“新建项目”** &gt; \*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="d5df0-248">In Visual Studio, choose **File** &gt; **New Project**.</span></span> <span data-ttu-id="d5df0-249">在左侧，展开 " **Visual c #**"，选择 " **Web**"，然后选择 " **ASP.NET MVC4 Web 应用程序**"。</span><span class="sxs-lookup"><span data-stu-id="d5df0-249">On the left, expand **Visual C#**, select **Web**, and then select **ASP.NET MVC4 Web Application**.</span></span> <span data-ttu-id="d5df0-250">单击“确定”。 </span><span class="sxs-lookup"><span data-stu-id="d5df0-250">Click **OK**.</span></span>

<span data-ttu-id="d5df0-251">在 " **新建 ASP.NET MVC 4 项目** " 对话框中，选择 " **单页面应用程序**"。</span><span class="sxs-lookup"><span data-stu-id="d5df0-251">In the **New ASP.NET MVC 4 Project** dialog, select **Single Page Application**.</span></span>

<span data-ttu-id="d5df0-252">在解决方案资源管理器中，展开 " **Views** " 文件夹，然后展开 " **主** 文件夹"。</span><span class="sxs-lookup"><span data-stu-id="d5df0-252">In Solution Explorer, expand the **Views** folder and then the **Home** folder.</span></span> <span data-ttu-id="d5df0-253">右键单击 "索引 ..." 文件，然后选择 **"在 Page Inspector 中查看**"。</span><span class="sxs-lookup"><span data-stu-id="d5df0-253">Right click the Index.cshtml file and choose **View in Page Inspector**.</span></span>

<span data-ttu-id="d5df0-254">Page Inspector 浏览器中显示的第一件事是登录页。</span><span class="sxs-lookup"><span data-stu-id="d5df0-254">The first thing that is displayed in the Page Inspector browser is a login page.</span></span> <span data-ttu-id="d5df0-255">单击 "注册"，创建用户名和密码。</span><span class="sxs-lookup"><span data-stu-id="d5df0-255">Click "Sign Up" and create a user name and password.</span></span> <span data-ttu-id="d5df0-256">注册后，应用程序会将你登录，并创建待办事项列表，其中包含一些示例项。</span><span class="sxs-lookup"><span data-stu-id="d5df0-256">Once you sign up, the application logs you in and creates a to-do list with some sample items.</span></span>

<span data-ttu-id="d5df0-257">单击 " **检查** " 以将 Page Inspector 置于检查模式。</span><span class="sxs-lookup"><span data-stu-id="d5df0-257">Click **Inspect** to put Page Inspector in Inspection Mode.</span></span> <span data-ttu-id="d5df0-258">在 Page Inspector 浏览器中，单击其中一个待办事项。</span><span class="sxs-lookup"><span data-stu-id="d5df0-258">In the Page Inspector browser, click on one of the to-do items.</span></span> <span data-ttu-id="d5df0-259">请注意，元素以橙色突出显示，而不是以蓝色突出显示，元素名称旁边有 "JS"。</span><span class="sxs-lookup"><span data-stu-id="d5df0-259">Notice that instead of being highlighted in blue, the element is highlighted in orange, with "JS" next to the element name.</span></span> <span data-ttu-id="d5df0-260">这表明该元素是通过脚本动态创建的。</span><span class="sxs-lookup"><span data-stu-id="d5df0-260">This indicates that the element was created dynamically through script.</span></span>

![](using-page-inspector-in-aspnet-mvc/_static/image44.png)

<span data-ttu-id="d5df0-261">此外，" **调用堆栈** " 选项卡上会显示橙色下划线。这指示 " **调用堆栈** " 窗格包含有关元素的详细信息。</span><span class="sxs-lookup"><span data-stu-id="d5df0-261">In addition, an orange underline appears on the **Call Stack** tab. This indicates that the **Call Stack** pane has more information about the element.</span></span>

<span data-ttu-id="d5df0-262">单击 " **调用堆栈** " 选项卡。" **调用堆栈** " 窗格显示创建元素的 JavaScript 调用的调用堆栈。</span><span class="sxs-lookup"><span data-stu-id="d5df0-262">Click on the **Call Stack** tab. The **Call Stack** pane shows the call stack for the JavaScript call that created the element.</span></span> <span data-ttu-id="d5df0-263">对诸如 jQuery 的外部库的调用会折叠，因此你可以轻松地查看对应用程序脚本的调用。</span><span class="sxs-lookup"><span data-stu-id="d5df0-263">Calls to external libraries such as jQuery are collapsed, so that you can easily see the calls to your application script.</span></span>

![](using-page-inspector-in-aspnet-mvc/_static/image46.png)

<span data-ttu-id="d5df0-264">若要查看完整的堆栈（包括对外部库的调用），可以展开标记为 "外部库" 的节点：</span><span class="sxs-lookup"><span data-stu-id="d5df0-264">To see the full stack, including calls to external libraries, you can expand the nodes labeled "External Libraries":</span></span>

![](using-page-inspector-in-aspnet-mvc/_static/image48.png)

<span data-ttu-id="d5df0-265">如果单击调用堆栈中的某个项，则 Visual Studio 将打开该代码文件并突出显示相应的脚本。</span><span class="sxs-lookup"><span data-stu-id="d5df0-265">If you click an item in the call stack, Visual Studio opens the code file and highlights the corresponding script.</span></span>

![](using-page-inspector-in-aspnet-mvc/_static/image50.png)

## <a name="see-also"></a><span data-ttu-id="d5df0-266">另请参阅</span><span class="sxs-lookup"><span data-stu-id="d5df0-266">See Also</span></span>

<span data-ttu-id="d5df0-267">介绍[如何将 ASP.NET MVC 4 与 Visual Studio](../older-versions/getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4.md) (ASP.net 网站) </span><span class="sxs-lookup"><span data-stu-id="d5df0-267">[Intro to ASP.NET MVC 4 with Visual Studio](../older-versions/getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4.md) (ASP.net website)</span></span>

<span data-ttu-id="d5df0-268"> (第9频道[Page Inspector 简介](https://channel9.msdn.com/posts/visual-studio-vnext-introducing-page-inspector/)) </span><span class="sxs-lookup"><span data-stu-id="d5df0-268">[Introducing Page Inspector](https://channel9.msdn.com/posts/visual-studio-vnext-introducing-page-inspector/) (Channel 9 video)</span></span>

<span data-ttu-id="d5df0-269"> (MSDN) [Page Inspector 错误消息](https://go.microsoft.com/?linkid=9813062)</span><span class="sxs-lookup"><span data-stu-id="d5df0-269">[Page Inspector Error Messages](https://go.microsoft.com/?linkid=9813062) (MSDN)</span></span>

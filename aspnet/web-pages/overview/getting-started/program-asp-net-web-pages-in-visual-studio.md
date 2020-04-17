---
uid: web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
title: 使用可视化工作室编程ASP.NET网页 （Razor） |微软文档
author: Rick-Anderson
description: 本附录说明如何使用 Visual Studio 2010 或可视化 Web 开发人员 2010 Express 使用 Razor 语法对 ASP.NET 网页进行编程。
ms.author: riande
ms.date: 02/13/2014
ms.assetid: 0acfec5a-48f2-4766-a801-a0f426966f0a
msc.legacyurl: /web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
msc.type: authoredcontent
ms.openlocfilehash: e586a116fc48a797bdd40befad5851a548282ce6
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542893"
---
# <a name="programming-aspnet-web-pages-razor-using-visual-studio"></a><span data-ttu-id="e5098-103">使用可视化工作室ASP.NET网页 （Razor） 编程</span><span class="sxs-lookup"><span data-stu-id="e5098-103">Programming ASP.NET Web Pages (Razor) Using Visual Studio</span></span>

<span data-ttu-id="e5098-104"> 作者 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="e5098-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="e5098-105">本文介绍如何使用可视化工作室或可视化 Web 开发人员快速程序ASP.NET网页 （Razor） 网站。</span><span class="sxs-lookup"><span data-stu-id="e5098-105">This article explains how you can use Visual Studio or Visual Web Developer Express to program ASP.NET Web Pages (Razor) websites.</span></span>
>
> <span data-ttu-id="e5098-106">学习内容</span><span class="sxs-lookup"><span data-stu-id="e5098-106">What you'll learn</span></span>
>
> - <span data-ttu-id="e5098-107">您需要安装的内容（如果有的话）才能在 Visual Studio 版本中使用ASP.NET网页。</span><span class="sxs-lookup"><span data-stu-id="e5098-107">What you need to install (if anything) to work with ASP.NET Web Pages in your version of Visual Studio.</span></span>
> - <span data-ttu-id="e5098-108">如何向可视化 Web 开发人员 2010 Express 添加对ASP.NET网页的支持。</span><span class="sxs-lookup"><span data-stu-id="e5098-108">How to add support for ASP.NET Web Pages to Visual Web Developer 2010 Express.</span></span>
> - <span data-ttu-id="e5098-109">如何使用 Visual Studio 中的功能使用ASP.NET Razor 页面，包括 IntelliSense 和调试器。</span><span class="sxs-lookup"><span data-stu-id="e5098-109">How to use features in Visual Studio to work with ASP.NET Razor pages, including IntelliSense and the debugger.</span></span>
>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="e5098-110">本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="e5098-110">Software versions used in the tutorial</span></span>
>
>
> - <span data-ttu-id="e5098-111">ASP.NET网页 （剃须刀） 3</span><span class="sxs-lookup"><span data-stu-id="e5098-111">ASP.NET Web Pages (Razor) 3</span></span>
> - <span data-ttu-id="e5098-112">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="e5098-112">Visual Studio 2013</span></span>
> - <span data-ttu-id="e5098-113">Web矩阵 3</span><span class="sxs-lookup"><span data-stu-id="e5098-113">WebMatrix 3</span></span>
>
>
> <span data-ttu-id="e5098-114">本教程还适用于ASP.NET网页 2、Visual Studio 2012、Visual Studio 2010 和 WebMatrix 2。</span><span class="sxs-lookup"><span data-stu-id="e5098-114">This tutorial also works with ASP.NET Web Pages 2, Visual Studio 2012, Visual Studio 2010, and WebMatrix 2.</span></span>

<span data-ttu-id="e5098-115">您可以使用 WebMatrix 或许多其他代码编辑器使用 Razor 语法对ASP.NET网页进行编程。</span><span class="sxs-lookup"><span data-stu-id="e5098-115">You can program ASP.NET Web pages with Razor syntax using WebMatrix or many other code editors.</span></span> <span data-ttu-id="e5098-116">您还可以使用 Microsoft Visual Studio，这是一个功能齐全的集成开发环境 （IDE），它提供了一组功能强大的工具来创建多种类型的应用程序（而不仅仅是网站）。</span><span class="sxs-lookup"><span data-stu-id="e5098-116">You can also use Microsoft Visual Studio which is a full-featured integrated development environment (IDE) that provides a powerful set of tools for creating many types of applications (not just websites).</span></span> <span data-ttu-id="e5098-117">要使用ASP.NET Razor 页面，您可以使用[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)。</span><span class="sxs-lookup"><span data-stu-id="e5098-117">To work with ASP.NET Razor pages, you can use [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017).</span></span>

<span data-ttu-id="e5098-118">Visual Studio 为使用 ASP.NET Razor 网页进行编程提供的两个特别有用的功能是：</span><span class="sxs-lookup"><span data-stu-id="e5098-118">Two particularly useful features that Visual Studio provides for programming with ASP.NET Razor web pages are:</span></span>

- <span data-ttu-id="e5098-119">*内泰利感知*。</span><span class="sxs-lookup"><span data-stu-id="e5098-119">*IntelliSense*.</span></span> <span data-ttu-id="e5098-120">视觉工作室内置的 IntelliSense 功能比 WebMatrix 中的 IntelliSense 更为全面。</span><span class="sxs-lookup"><span data-stu-id="e5098-120">The IntelliSense feature built into Visual Studio is more comprehensive than IntelliSense in WebMatrix.</span></span>
- <span data-ttu-id="e5098-121">*调试器*。</span><span class="sxs-lookup"><span data-stu-id="e5098-121">*Debugger*.</span></span> <span data-ttu-id="e5098-122">调试器允许您在程序运行时停止程序、检查变量和逐行执行代码，从而对代码进行故障排除。</span><span class="sxs-lookup"><span data-stu-id="e5098-122">The debugger lets you troubleshoot your code by stopping a program while it's running, examining variables, and stepping through the code line by line.</span></span>

## <a name="using-visual-studio-with-different-versions-of-aspnet-web-pages"></a><span data-ttu-id="e5098-123">将视觉工作室与不同版本的ASP.NET网页使用</span><span class="sxs-lookup"><span data-stu-id="e5098-123">Using Visual Studio with Different Versions of ASP.NET Web Pages</span></span>

<span data-ttu-id="e5098-124">要在 Visual Studio 2017 中开发ASP.NET Web 应用，请安装**ASP.NET和 Web 开发**工作负载。</span><span class="sxs-lookup"><span data-stu-id="e5098-124">To develop ASP.NET web apps in Visual Studio 2017, install the **ASP.NET and web development** workload.</span></span>

<span data-ttu-id="e5098-125">Visual Studio 2012 和 Visual Studio 2013 包括对ASP.NET网页的支持。</span><span class="sxs-lookup"><span data-stu-id="e5098-125">Visual Studio 2012 and Visual Studio 2013 include support for ASP.NET Web Pages.</span></span> <span data-ttu-id="e5098-126">（安装 Visual Studio 时，将安装支持ASP.NET网页所需的软件包。</span><span class="sxs-lookup"><span data-stu-id="e5098-126">(The packages that are required in order to support ASP.NET Web Pages are installed when you install Visual Studio.)</span></span>

<span data-ttu-id="e5098-127">默认情况下，Visual Studio 2010 不包括对 ASP.NET 网页的支持。</span><span class="sxs-lookup"><span data-stu-id="e5098-127">Visual Studio 2010 does not include support by default for ASP.NET Web Pages.</span></span> <span data-ttu-id="e5098-128">要将 ASP.NET 网页与 Visual Studio 2010 一起使用，您必须安装ASP.NET MVC 软件包。</span><span class="sxs-lookup"><span data-stu-id="e5098-128">To use ASP.NET Web Pages with Visual Studio 2010, you must install the ASP.NET MVC package.</span></span> <span data-ttu-id="e5098-129">要获取 ASP.NET网页 2，请安装ASP.NET MVC 4。</span><span class="sxs-lookup"><span data-stu-id="e5098-129">To get ASP.NET Web Pages 2, you install ASP.NET MVC 4.</span></span>

<span data-ttu-id="e5098-130">下表总结了不同版本的 Visual Studio 中对 ASP.NET 网页的支持。</span><span class="sxs-lookup"><span data-stu-id="e5098-130">The following table summarizes the support for ASP.NET Web Pages in different versions of Visual Studio.</span></span>

|  | <span data-ttu-id="e5098-131">Visual Studio 2010</span><span class="sxs-lookup"><span data-stu-id="e5098-131">Visual Studio 2010</span></span> | <span data-ttu-id="e5098-132">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="e5098-132">Visual Studio 2012</span></span> | <span data-ttu-id="e5098-133">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="e5098-133">Visual Studio 2013</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e5098-134">**ASP.NET 网页 2**</span><span class="sxs-lookup"><span data-stu-id="e5098-134">**ASP.NET Web Pages 2**</span></span> | <span data-ttu-id="e5098-135">安装ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="e5098-135">Install ASP.NET MVC 4</span></span> | <span data-ttu-id="e5098-136">（包括）</span><span class="sxs-lookup"><span data-stu-id="e5098-136">(Included)</span></span> | <span data-ttu-id="e5098-137">（包括）</span><span class="sxs-lookup"><span data-stu-id="e5098-137">(Included)</span></span> |
| <span data-ttu-id="e5098-138">**ASP.NET 网页 3**</span><span class="sxs-lookup"><span data-stu-id="e5098-138">**ASP.NET Web Pages 3**</span></span> |  | <span data-ttu-id="e5098-139">通过 NuGet 更新到ASP.NET网页 3</span><span class="sxs-lookup"><span data-stu-id="e5098-139">Update to ASP.NET Web Pages 3 through NuGet</span></span> | <span data-ttu-id="e5098-140">（包括）</span><span class="sxs-lookup"><span data-stu-id="e5098-140">(Included)</span></span> |

<span data-ttu-id="e5098-141">要使用 Visual Studio 2010，请参阅[在 Visual Studio 2010 中安装支持ASP.NET网页](#vs2010support)。</span><span class="sxs-lookup"><span data-stu-id="e5098-141">To work with Visual Studio 2010, see [Installing Support for ASP.NET Web Pages in Visual Studio 2010](#vs2010support).</span></span>

## <a name="launching-visual-studio-from-webmatrix"></a><span data-ttu-id="e5098-142">从 WebMatrix 启动可视化工作室</span><span class="sxs-lookup"><span data-stu-id="e5098-142">Launching Visual Studio from WebMatrix</span></span>

<span data-ttu-id="e5098-143">如果您在 WebMatrix 中启动了一个项目，并希望切换到 Visual Studio，WebMatrix 提供了一个按钮，用于在 Visual Studio 中轻松打开项目。</span><span class="sxs-lookup"><span data-stu-id="e5098-143">If you have started a project in WebMatrix and want to switch to Visual Studio, WebMatrix provides a button to easily open the project in Visual Studio.</span></span> <span data-ttu-id="e5098-144">您必须在计算机上安装 Visual Studio 才能启用此按钮。</span><span class="sxs-lookup"><span data-stu-id="e5098-144">You must have Visual Studio installed on your computer for this button to be enabled.</span></span> <span data-ttu-id="e5098-145">下图显示了 WebMatrix 中的按钮。</span><span class="sxs-lookup"><span data-stu-id="e5098-145">The following image shows the button in WebMatrix.</span></span>

![启动视觉工作室](program-asp-net-web-pages-in-visual-studio/_static/image1.png)

<span data-ttu-id="e5098-147">单击该按钮时，项目在可视化工作室中打开。</span><span class="sxs-lookup"><span data-stu-id="e5098-147">When you click the button, the project is opened in Visual Studio.</span></span> <span data-ttu-id="e5098-148">您可以在 WebMatrix 和 Visual Studio 之间来回切换，没有任何问题。</span><span class="sxs-lookup"><span data-stu-id="e5098-148">You can switch back and forth between WebMatrix and Visual Studio without any problems.</span></span> <span data-ttu-id="e5098-149">如果其他环境中的任何文件已更改，需要重新加载以获取最新更改，您将收到通知。</span><span class="sxs-lookup"><span data-stu-id="e5098-149">You will be notified if any files have changed in the other environment and need to be reloaded to get the latest changes.</span></span>

## <a name="creating-aspnet-razor-site-in-visual-studio"></a><span data-ttu-id="e5098-150">在视觉工作室创建ASP.NET剃刀网站</span><span class="sxs-lookup"><span data-stu-id="e5098-150">Creating ASP.NET Razor Site in Visual Studio</span></span>

<span data-ttu-id="e5098-151">要在视觉工作室中创建ASP.NET剃刀网站：</span><span class="sxs-lookup"><span data-stu-id="e5098-151">To create an ASP.NET Razor website in Visual Studio:</span></span>

1. <span data-ttu-id="e5098-152">打开 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="e5098-152">Open Visual Studio.</span></span>
2. <span data-ttu-id="e5098-153">在 **"文件**"菜单中，单击 **"新建网站**"。</span><span class="sxs-lookup"><span data-stu-id="e5098-153">In the **File** menu, click **New Web Site**.</span></span>

    ![创建新网站](program-asp-net-web-pages-in-visual-studio/_static/image2.png)
3. <span data-ttu-id="e5098-155">在 **"新建网站"** 对话框中，选择要使用的语言（可视 C# 或可视基本）。</span><span class="sxs-lookup"><span data-stu-id="e5098-155">In the **New Web Site** dialog box, select the language to use (Visual C# or Visual Basic).</span></span>
4. <span data-ttu-id="e5098-156">选择**ASP.NET网站（Razor）** 模板。</span><span class="sxs-lookup"><span data-stu-id="e5098-156">Select the **ASP.NET Web Site (Razor)** template.</span></span>

    ![剃须刀网站](program-asp-net-web-pages-in-visual-studio/_static/image3.png)
5. <span data-ttu-id="e5098-158">单击 **“确定”** 。</span><span class="sxs-lookup"><span data-stu-id="e5098-158">Click **OK**.</span></span>

<span data-ttu-id="e5098-159">新项目存在，并且填充了一些默认网页，以帮助您入门。</span><span class="sxs-lookup"><span data-stu-id="e5098-159">Your new project exists and is populated with some default web pages to help you get started.</span></span>

### <a name="using-intellisense"></a><span data-ttu-id="e5098-160">Using IntelliSense</span><span class="sxs-lookup"><span data-stu-id="e5098-160">Using IntelliSense</span></span>

<span data-ttu-id="e5098-161">现在，您已经创建了一个网站，您可以看到 IntelliSense 在视觉工作室中是如何工作的。</span><span class="sxs-lookup"><span data-stu-id="e5098-161">Now that you've created a site, you can see how IntelliSense works in Visual Studio.</span></span>

1. <span data-ttu-id="e5098-162">在您刚刚创建的网站中，打开*Default.cshtml*页面。</span><span class="sxs-lookup"><span data-stu-id="e5098-162">In the website you just created, open the *Default.cshtml* page.</span></span>
2. <span data-ttu-id="e5098-163">在页面`<h3>`中的标记之后，键入`@ServerInfo.`（包括点）。</span><span class="sxs-lookup"><span data-stu-id="e5098-163">After the `<h3>` tags in the page, type `@ServerInfo.` (including the dot).</span></span> <span data-ttu-id="e5098-164">请注意 IntelliSense 如何在下拉列表中显示`ServerInfo`帮助程序的可用方法。</span><span class="sxs-lookup"><span data-stu-id="e5098-164">Notice how IntelliSense displays the available methods for the `ServerInfo` helper in a drop-down list.</span></span>

    ![intellisense](program-asp-net-web-pages-in-visual-studio/_static/image4.png)
3. <span data-ttu-id="e5098-166">从`GetHtml`列表中选择方法，然后按 Enter。</span><span class="sxs-lookup"><span data-stu-id="e5098-166">Select the `GetHtml` method from the list and then press Enter.</span></span> <span data-ttu-id="e5098-167">IntelliSense 会自动填充该方法。</span><span class="sxs-lookup"><span data-stu-id="e5098-167">IntelliSense automatically fills in the method.</span></span> <span data-ttu-id="e5098-168">（与 C# 中的任何方法一样，必须在`()`方法之后添加字符。方法的`GetHtml`已完成代码类似于以下示例：</span><span class="sxs-lookup"><span data-stu-id="e5098-168">(As with any method in C#, you must add `()` characters after the method.) The completed code for the `GetHtml` method looks like the following example:</span></span>

    [!code-cshtml[Main](program-asp-net-web-pages-in-visual-studio/samples/sample1.cshtml)]
4. <span data-ttu-id="e5098-169">按 Ctrl+F5 以运行该页。</span><span class="sxs-lookup"><span data-stu-id="e5098-169">Press Ctrl+F5 to run the page.</span></span> <span data-ttu-id="e5098-170">这是页面在浏览器中显示时的外观：</span><span class="sxs-lookup"><span data-stu-id="e5098-170">This is what the page looks like when displayed in a browser:</span></span>

    ![浏览器中的默认页面](program-asp-net-web-pages-in-visual-studio/_static/image5.png)
5. <span data-ttu-id="e5098-172">关闭浏览器。</span><span class="sxs-lookup"><span data-stu-id="e5098-172">Close the browser.</span></span>

### <a name="using-the-debugger"></a><span data-ttu-id="e5098-173">使用调试器</span><span class="sxs-lookup"><span data-stu-id="e5098-173">Using the Debugger</span></span>

1. <span data-ttu-id="e5098-174">在*Default.cshtml*页面的顶部，以`Page.Title`开头的行后添加以下代码行：</span><span class="sxs-lookup"><span data-stu-id="e5098-174">At the top of the *Default.cshtml* page, after the line that begins with `Page.Title`, add the following line of code:</span></span>

    [!code-csharp[Main](program-asp-net-web-pages-in-visual-studio/samples/sample2.cs)]
2. <span data-ttu-id="e5098-175">在代码左侧编辑器的灰色边距中，单击此新行的旁边以添加*断点*。</span><span class="sxs-lookup"><span data-stu-id="e5098-175">In the gray margin of the editor to the left of the code, click next to this new line in order to add a *breakpoint*.</span></span> <span data-ttu-id="e5098-176">断点是一个标记，它告诉调试器在此时停止运行程序，以便您可以看到发生了什么。</span><span class="sxs-lookup"><span data-stu-id="e5098-176">A breakpoint is a marker that tells the debugger to stop running the program at that point so you can see what's happening.</span></span>

    ![设置断点](program-asp-net-web-pages-in-visual-studio/_static/image6.png)
3. <span data-ttu-id="e5098-178">删除对 方法的`ServerInfo.GetHtml`调用，并将调用添加到`@myTime`变量的位置。</span><span class="sxs-lookup"><span data-stu-id="e5098-178">Remove the call to the `ServerInfo.GetHtml` method, and add a call to the `@myTime` variable in its place.</span></span> <span data-ttu-id="e5098-179">此调用显示新代码行返回的当前时间值。</span><span class="sxs-lookup"><span data-stu-id="e5098-179">This call displays the current time value that's returned by the new line of code.</span></span>
4. <span data-ttu-id="e5098-180">按 F5 以在调试器中运行页面。</span><span class="sxs-lookup"><span data-stu-id="e5098-180">Press F5 to run the page in the debugger.</span></span> <span data-ttu-id="e5098-181">页面在您设置的断点上停止。</span><span class="sxs-lookup"><span data-stu-id="e5098-181">The page stops on the breakpoint that you set.</span></span> <span data-ttu-id="e5098-182">下图显示了具有断点（黄色）的编辑器中页面的外观。</span><span class="sxs-lookup"><span data-stu-id="e5098-182">The following image shows what the page looks like in the editor with the breakpoint (in yellow).</span></span>

    ![调试断点](program-asp-net-web-pages-in-visual-studio/_static/image7.png)
5. <span data-ttu-id="e5098-184">在"调试"工具栏中，单击 **"进入"** 按钮（或按 F11）以运行下一行代码。</span><span class="sxs-lookup"><span data-stu-id="e5098-184">In the Debug toolbar, click the **Step Into** button (or press F11) to run the next line of code.</span></span> <span data-ttu-id="e5098-185">每次单击此按钮时，都会将执行提前到下一行代码。</span><span class="sxs-lookup"><span data-stu-id="e5098-185">Each time you click this button, you advance the execution to the next line of code.</span></span>

    ![单步进入按钮](program-asp-net-web-pages-in-visual-studio/_static/image8.png)
6. <span data-ttu-id="e5098-187">通过将鼠标指针放在变量`myTime`上或通过检查 **"局部变量**"和 **"调用堆栈**"窗口中显示的值来检查变量的值。</span><span class="sxs-lookup"><span data-stu-id="e5098-187">Examine the value of the `myTime` variable by holding your mouse pointer over it or by inspecting the values displayed in the **Locals** and **Call Stack** windows.</span></span> <span data-ttu-id="e5098-188">可视化工作室显示变量的值。</span><span class="sxs-lookup"><span data-stu-id="e5098-188">Visual Studio display the value of the variable.</span></span>

    ![显示时间值](program-asp-net-web-pages-in-visual-studio/_static/image9.png)
7. <span data-ttu-id="e5098-190">检查完变量并单步执行代码后，按 F5 继续运行页面，而无需在每行停止。</span><span class="sxs-lookup"><span data-stu-id="e5098-190">When you're done examining the variable and stepping through code, press F5 to continue running the page without stopping at each line.</span></span> <span data-ttu-id="e5098-191">完成所有代码后，浏览器将显示页面。</span><span class="sxs-lookup"><span data-stu-id="e5098-191">When you've finished stepping through all the code, the browser displays the page.</span></span>

<span data-ttu-id="e5098-192">要了解有关调试器以及如何在 Visual Studio 中调试代码的信息，请参阅[演练：在可视化 Web 开发人员中调试网页](https://msdn.microsoft.com/library/z9e7w6cs.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e5098-192">To learn more about the debugger and about how to debug code in Visual Studio, see [Walkthrough: Debugging Web Pages in Visual Web Developer](https://msdn.microsoft.com/library/z9e7w6cs.aspx).</span></span>

## <a name="using-razor-in-aspnet-mvc-projects-with-visual-studio"></a><span data-ttu-id="e5098-193">使用 Razor 在 ASP.NET MVC 项目中使用 Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e5098-193">Using Razor in ASP.NET MVC projects with Visual Studio</span></span>

<span data-ttu-id="e5098-194">Razor 语法还广泛用于ASP.NET MVC 项目中。</span><span class="sxs-lookup"><span data-stu-id="e5098-194">The Razor syntax is also used extensively in ASP.NET MVC projects.</span></span> <span data-ttu-id="e5098-195">MVC 是构建动态网站的强大、基于模式的方法。</span><span class="sxs-lookup"><span data-stu-id="e5098-195">MVC is a powerful, patterns-based way to build dynamic websites.</span></span> <span data-ttu-id="e5098-196">如果ASP.NET网页网站变得难以维护，您可能需要考虑将其转换为ASP.NET MVC 应用程序。</span><span class="sxs-lookup"><span data-stu-id="e5098-196">If your ASP.NET Web Pages site becomes difficult to maintain, you might want to consider converting it to an ASP.NET MVC application.</span></span> <span data-ttu-id="e5098-197">有关创建 MVC 应用程序的示例，请参阅[使用 mVC 5 ASP.NET 入门](../../../mvc/overview/getting-started/introduction/getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="e5098-197">For an example of creating an MVC application, see [Getting Started with ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md).</span></span>

<a id="vs2010support"></a>
## <a name="installing-support-for-aspnet-web-pages-in-visual-studio-2010"></a><span data-ttu-id="e5098-198">2010 年在可视化工作室安装对 ASP.NET 网页的支持</span><span class="sxs-lookup"><span data-stu-id="e5098-198">Installing Support for ASP.NET Web Pages in Visual Studio 2010</span></span>

<span data-ttu-id="e5098-199">本节演示如何安装 Visual Web 开发人员 Express 2010 和可视化工作室的ASP.NET网页工具。</span><span class="sxs-lookup"><span data-stu-id="e5098-199">This section shows how to install Visual Web Developer Express 2010 and the ASP.NET Web Pages Tools for Visual Studio.</span></span>

1. <span data-ttu-id="e5098-200">如果您还没有 Web 平台安装程序，请从以下 URL 下载它：</span><span class="sxs-lookup"><span data-stu-id="e5098-200">If you don't already have the Web Platform Installer, download it from the following URL:</span></span>

    [https://www.microsoft.com/web/downloads/platform.aspx](https://www.microsoft.com/web/downloads/platform.aspx)
2. <span data-ttu-id="e5098-201">运行 Web 平台安装程序。</span><span class="sxs-lookup"><span data-stu-id="e5098-201">Run the Web Platform Installer.</span></span>
3. <span data-ttu-id="e5098-202">单击"**产品**"选项卡。</span><span class="sxs-lookup"><span data-stu-id="e5098-202">Click the **Products** tab.</span></span>

    ![WebPI 产品选项卡](program-asp-net-web-pages-in-visual-studio/_static/image10.png)
4. <span data-ttu-id="e5098-204">搜索**ASP.NET MVC 4（ASP.NET**网页 2），然后单击"**添加**"。</span><span class="sxs-lookup"><span data-stu-id="e5098-204">Search for **ASP.NET MVC 4** (for ASP.NET Web Pages 2) and then click **Add**.</span></span> <span data-ttu-id="e5098-205">这些产品包括用于构建ASP.NET Razor 网站的视觉工作室工具。</span><span class="sxs-lookup"><span data-stu-id="e5098-205">These products include Visual Studio tools for building ASP.NET Razor websites.</span></span>

    ![WebPi 安装选项](program-asp-net-web-pages-in-visual-studio/_static/image11.png)
5. <span data-ttu-id="e5098-207">单击"**安装**"以完成安装。</span><span class="sxs-lookup"><span data-stu-id="e5098-207">Click **Install** to complete the installation.</span></span>

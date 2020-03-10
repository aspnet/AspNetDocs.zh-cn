---
uid: aspnet/web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
title: 使用 Visual Studio 进行编程 ASP.NET 网页（Razor） |Microsoft Docs
author: Rick-Anderson
description: 本附录介绍了如何使用 Visual Studio 2010 或 Visual Web Developer 2010 Express 通过 Razor 语法来编程 ASP.NET 网页。
ms.author: riande
ms.date: 02/13/2014
ms.assetid: 0acfec5a-48f2-4766-a801-a0f426966f0a
msc.legacyurl: /web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
msc.type: authoredcontent
ms.openlocfilehash: 1a76098779d05912bf7bdf2de5fdce024770752c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78514292"
---
# <a name="programming-aspnet-web-pages-razor-using-visual-studio"></a><span data-ttu-id="3ae14-103">使用 Visual Studio 的编程 ASP.NET 网页（Razor）</span><span class="sxs-lookup"><span data-stu-id="3ae14-103">Programming ASP.NET Web Pages (Razor) Using Visual Studio</span></span>

<span data-ttu-id="3ae14-104">作者： [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="3ae14-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="3ae14-105">本文介绍如何使用 Visual Studio 或 Visual Web Developer Express 来计划 ASP.NET 网页（Razor）网站。</span><span class="sxs-lookup"><span data-stu-id="3ae14-105">This article explains how you can use Visual Studio or Visual Web Developer Express to program ASP.NET Web Pages (Razor) websites.</span></span>
>
> <span data-ttu-id="3ae14-106">学习内容</span><span class="sxs-lookup"><span data-stu-id="3ae14-106">What you'll learn</span></span>
>
> - <span data-ttu-id="3ae14-107">需要安装的内容（如果有），才能使用版本的 Visual Studio 中的 ASP.NET 网页。</span><span class="sxs-lookup"><span data-stu-id="3ae14-107">What you need to install (if anything) to work with ASP.NET Web Pages in your version of Visual Studio.</span></span>
> - <span data-ttu-id="3ae14-108">如何向 Visual Web Developer 2010 Express 添加对 ASP.NET 网页的支持。</span><span class="sxs-lookup"><span data-stu-id="3ae14-108">How to add support for ASP.NET Web Pages to Visual Web Developer 2010 Express.</span></span>
> - <span data-ttu-id="3ae14-109">如何使用 Visual Studio 中的功能来处理 ASP.NET Razor 页面，包括 IntelliSense 和调试器。</span><span class="sxs-lookup"><span data-stu-id="3ae14-109">How to use features in Visual Studio to work with ASP.NET Razor pages, including IntelliSense and the debugger.</span></span>
>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="3ae14-110">本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="3ae14-110">Software versions used in the tutorial</span></span>
>
>
> - <span data-ttu-id="3ae14-111">ASP.NET 网页（Razor）3</span><span class="sxs-lookup"><span data-stu-id="3ae14-111">ASP.NET Web Pages (Razor) 3</span></span>
> - <span data-ttu-id="3ae14-112">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="3ae14-112">Visual Studio 2013</span></span>
> - <span data-ttu-id="3ae14-113">WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="3ae14-113">WebMatrix 3</span></span>
>
>
> <span data-ttu-id="3ae14-114">本教程还适用于 ASP.NET 网页2、Visual Studio 2012、Visual Studio 2010 和 WebMatrix 2。</span><span class="sxs-lookup"><span data-stu-id="3ae14-114">This tutorial also works with ASP.NET Web Pages 2, Visual Studio 2012, Visual Studio 2010, and WebMatrix 2.</span></span>

<span data-ttu-id="3ae14-115">您可以使用 WebMatrix 或许多其他代码编辑器通过 Razor 语法来编写 ASP.NET 网页。</span><span class="sxs-lookup"><span data-stu-id="3ae14-115">You can program ASP.NET Web pages with Razor syntax using WebMatrix or many other code editors.</span></span> <span data-ttu-id="3ae14-116">你还可以使用 Microsoft Visual Studio 功能齐全的集成开发环境（IDE），它提供了一组功能强大的工具，可用于创建许多类型的应用程序（而不仅仅是网站）。</span><span class="sxs-lookup"><span data-stu-id="3ae14-116">You can also use Microsoft Visual Studio which is a full-featured integrated development environment (IDE) that provides a powerful set of tools for creating many types of applications (not just websites).</span></span> <span data-ttu-id="3ae14-117">若要使用 ASP.NET Razor 页面，可以使用[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)。</span><span class="sxs-lookup"><span data-stu-id="3ae14-117">To work with ASP.NET Razor pages, you can use [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017).</span></span>

<span data-ttu-id="3ae14-118">Visual Studio 提供的两个特别有用的功能可用于通过 ASP.NET Razor 网页进行编程：</span><span class="sxs-lookup"><span data-stu-id="3ae14-118">Two particularly useful features that Visual Studio provides for programming with ASP.NET Razor web pages are:</span></span>

- <span data-ttu-id="3ae14-119">*IntelliSense*。</span><span class="sxs-lookup"><span data-stu-id="3ae14-119">*IntelliSense*.</span></span> <span data-ttu-id="3ae14-120">Visual Studio 中内置的 IntelliSense 功能比 WebMatrix 中的 IntelliSense 更为全面。</span><span class="sxs-lookup"><span data-stu-id="3ae14-120">The IntelliSense feature built into Visual Studio is more comprehensive than IntelliSense in WebMatrix.</span></span>
- <span data-ttu-id="3ae14-121">*调试器*。</span><span class="sxs-lookup"><span data-stu-id="3ae14-121">*Debugger*.</span></span> <span data-ttu-id="3ae14-122">调试器允许您通过在程序运行、检查变量和逐行执行代码行的过程中停止程序来对代码进行故障排除。</span><span class="sxs-lookup"><span data-stu-id="3ae14-122">The debugger lets you troubleshoot your code by stopping a program while it's running, examining variables, and stepping through the code line by line.</span></span>

## <a name="using-visual-studio-with-different-versions-of-aspnet-web-pages"></a><span data-ttu-id="3ae14-123">将 Visual Studio 与不同版本的 ASP.NET 网页一起使用</span><span class="sxs-lookup"><span data-stu-id="3ae14-123">Using Visual Studio with Different Versions of ASP.NET Web Pages</span></span>

<span data-ttu-id="3ae14-124">若要在 Visual Studio 2017 中开发 ASP.NET web 应用，请安装**ASP.NET 和 web 开发**工作负荷。</span><span class="sxs-lookup"><span data-stu-id="3ae14-124">To develop ASP.NET web apps in Visual Studio 2017, install the **ASP.NET and web development** workload.</span></span>

<span data-ttu-id="3ae14-125">Visual Studio 2012 和 Visual Studio 2013 包括对 ASP.NET 网页的支持。</span><span class="sxs-lookup"><span data-stu-id="3ae14-125">Visual Studio 2012 and Visual Studio 2013 include support for ASP.NET Web Pages.</span></span> <span data-ttu-id="3ae14-126">（安装 Visual Studio 时，会安装支持 ASP.NET 网页所需的包。）</span><span class="sxs-lookup"><span data-stu-id="3ae14-126">(The packages that are required in order to support ASP.NET Web Pages are installed when you install Visual Studio.)</span></span>

<span data-ttu-id="3ae14-127">默认情况下，Visual Studio 2010 不支持 ASP.NET 网页。</span><span class="sxs-lookup"><span data-stu-id="3ae14-127">Visual Studio 2010 does not include support by default for ASP.NET Web Pages.</span></span> <span data-ttu-id="3ae14-128">若要将 ASP.NET 网页与 Visual Studio 2010 一起使用，必须安装 ASP.NET MVC 包。</span><span class="sxs-lookup"><span data-stu-id="3ae14-128">To use ASP.NET Web Pages with Visual Studio 2010, you must install the ASP.NET MVC package.</span></span> <span data-ttu-id="3ae14-129">若要获取 ASP.NET 网页2，请安装 ASP.NET MVC 4。</span><span class="sxs-lookup"><span data-stu-id="3ae14-129">To get ASP.NET Web Pages 2, you install ASP.NET MVC 4.</span></span>

<span data-ttu-id="3ae14-130">下表汇总了对不同版本的 Visual Studio 中 ASP.NET 网页的支持。</span><span class="sxs-lookup"><span data-stu-id="3ae14-130">The following table summarizes the support for ASP.NET Web Pages in different versions of Visual Studio.</span></span>

|  | <span data-ttu-id="3ae14-131">Visual Studio 2010</span><span class="sxs-lookup"><span data-stu-id="3ae14-131">Visual Studio 2010</span></span> | <span data-ttu-id="3ae14-132">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="3ae14-132">Visual Studio 2012</span></span> | <span data-ttu-id="3ae14-133">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="3ae14-133">Visual Studio 2013</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3ae14-134">**ASP.NET 网页2**</span><span class="sxs-lookup"><span data-stu-id="3ae14-134">**ASP.NET Web Pages 2**</span></span> | <span data-ttu-id="3ae14-135">安装 ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="3ae14-135">Install ASP.NET MVC 4</span></span> | <span data-ttu-id="3ae14-136">处于</span><span class="sxs-lookup"><span data-stu-id="3ae14-136">(Included)</span></span> | <span data-ttu-id="3ae14-137">处于</span><span class="sxs-lookup"><span data-stu-id="3ae14-137">(Included)</span></span> |
| <span data-ttu-id="3ae14-138">**ASP.NET 网页3**</span><span class="sxs-lookup"><span data-stu-id="3ae14-138">**ASP.NET Web Pages 3**</span></span> |  | <span data-ttu-id="3ae14-139">通过 NuGet 更新到 ASP.NET 网页3</span><span class="sxs-lookup"><span data-stu-id="3ae14-139">Update to ASP.NET Web Pages 3 through NuGet</span></span> | <span data-ttu-id="3ae14-140">处于</span><span class="sxs-lookup"><span data-stu-id="3ae14-140">(Included)</span></span> |

<span data-ttu-id="3ae14-141">若要使用 Visual Studio 2010，请参阅[安装 Visual studio 2010 中的 ASP.NET 网页支持](#vs2010support)。</span><span class="sxs-lookup"><span data-stu-id="3ae14-141">To work with Visual Studio 2010, see [Installing Support for ASP.NET Web Pages in Visual Studio 2010](#vs2010support).</span></span>

## <a name="launching-visual-studio-from-webmatrix"></a><span data-ttu-id="3ae14-142">从 WebMatrix 启动 Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3ae14-142">Launching Visual Studio from WebMatrix</span></span>

<span data-ttu-id="3ae14-143">如果已在 WebMatrix 中启动项目，并且想要切换到 Visual Studio，WebMatrix 提供了一个按钮，可以在 Visual Studio 中轻松打开项目。</span><span class="sxs-lookup"><span data-stu-id="3ae14-143">If you have started a project in WebMatrix and want to switch to Visual Studio, WebMatrix provides a button to easily open the project in Visual Studio.</span></span> <span data-ttu-id="3ae14-144">若要启用此按钮，您必须在计算机上安装 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="3ae14-144">You must have Visual Studio installed on your computer for this button to be enabled.</span></span> <span data-ttu-id="3ae14-145">下图显示了 WebMatrix 中的按钮。</span><span class="sxs-lookup"><span data-stu-id="3ae14-145">The following image shows the button in WebMatrix.</span></span>

![启动 Visual Studio](program-asp-net-web-pages-in-visual-studio/_static/image1.png)

<span data-ttu-id="3ae14-147">单击该按钮时，将在 Visual Studio 中打开该项目。</span><span class="sxs-lookup"><span data-stu-id="3ae14-147">When you click the button, the project is opened in Visual Studio.</span></span> <span data-ttu-id="3ae14-148">您可以在 WebMatrix 和 Visual Studio 之间来回切换，而不会出现任何问题。</span><span class="sxs-lookup"><span data-stu-id="3ae14-148">You can switch back and forth between WebMatrix and Visual Studio without any problems.</span></span> <span data-ttu-id="3ae14-149">如果其他环境中的任何文件发生了更改，则会收到通知，需要重新加载才能获得最新的更改。</span><span class="sxs-lookup"><span data-stu-id="3ae14-149">You will be notified if any files have changed in the other environment and need to be reloaded to get the latest changes.</span></span>

## <a name="creating-aspnet-razor-site-in-visual-studio"></a><span data-ttu-id="3ae14-150">在 Visual Studio 中创建 ASP.NET Razor 网站</span><span class="sxs-lookup"><span data-stu-id="3ae14-150">Creating ASP.NET Razor Site in Visual Studio</span></span>

<span data-ttu-id="3ae14-151">若要在 Visual Studio 中创建 ASP.NET Razor 网站：</span><span class="sxs-lookup"><span data-stu-id="3ae14-151">To create an ASP.NET Razor website in Visual Studio:</span></span>

1. <span data-ttu-id="3ae14-152">打开 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="3ae14-152">Open Visual Studio.</span></span>
2. <span data-ttu-id="3ae14-153">在 "**文件**" 菜单中，单击 "**新建**网站"。</span><span class="sxs-lookup"><span data-stu-id="3ae14-153">In the **File** menu, click **New Web Site**.</span></span>

    ![创建新网站](program-asp-net-web-pages-in-visual-studio/_static/image2.png)
3. <span data-ttu-id="3ae14-155">在 "**新建**网站" 对话框中，选择要使用的语言（视觉C#对象或 Visual Basic）。</span><span class="sxs-lookup"><span data-stu-id="3ae14-155">In the **New Web Site** dialog box, select the language to use (Visual C# or Visual Basic).</span></span>
4. <span data-ttu-id="3ae14-156">选择**ASP.NET 网站（Razor）** 模板。</span><span class="sxs-lookup"><span data-stu-id="3ae14-156">Select the **ASP.NET Web Site (Razor)** template.</span></span>

    ![razor 网站](program-asp-net-web-pages-in-visual-studio/_static/image3.png)
5. <span data-ttu-id="3ae14-158">单击“确定”。</span><span class="sxs-lookup"><span data-stu-id="3ae14-158">Click **OK**.</span></span>

<span data-ttu-id="3ae14-159">你的新项目存在，并填充了一些默认网页来帮助你入门。</span><span class="sxs-lookup"><span data-stu-id="3ae14-159">Your new project exists and is populated with some default web pages to help you get started.</span></span>

### <a name="using-intellisense"></a><span data-ttu-id="3ae14-160">Using IntelliSense</span><span class="sxs-lookup"><span data-stu-id="3ae14-160">Using IntelliSense</span></span>

<span data-ttu-id="3ae14-161">现在，你已创建了一个网站，可以在 Visual Studio 中了解 IntelliSense 的工作方式。</span><span class="sxs-lookup"><span data-stu-id="3ae14-161">Now that you've created a site, you can see how IntelliSense works in Visual Studio.</span></span>

1. <span data-ttu-id="3ae14-162">在刚创建的网站中，打开 "*默认.* #" 页。</span><span class="sxs-lookup"><span data-stu-id="3ae14-162">In the website you just created, open the *Default.cshtml* page.</span></span>
2. <span data-ttu-id="3ae14-163">在页面的 `<h3>` 标记后，键入 `@ServerInfo.` （包括点）。</span><span class="sxs-lookup"><span data-stu-id="3ae14-163">After the `<h3>` tags in the page, type `@ServerInfo.` (including the dot).</span></span> <span data-ttu-id="3ae14-164">请注意 IntelliSense 如何在下拉列表中显示 `ServerInfo` 帮助器的可用方法。</span><span class="sxs-lookup"><span data-stu-id="3ae14-164">Notice how IntelliSense displays the available methods for the `ServerInfo` helper in a drop-down list.</span></span>

    ![intellisense](program-asp-net-web-pages-in-visual-studio/_static/image4.png)
3. <span data-ttu-id="3ae14-166">从列表中选择 `GetHtml` 方法，然后按 Enter。</span><span class="sxs-lookup"><span data-stu-id="3ae14-166">Select the `GetHtml` method from the list and then press Enter.</span></span> <span data-ttu-id="3ae14-167">IntelliSense 自动填充方法。</span><span class="sxs-lookup"><span data-stu-id="3ae14-167">IntelliSense automatically fills in the method.</span></span> <span data-ttu-id="3ae14-168">（与中C#的任何方法一样，必须在方法之后添加 `()` 字符。）已完成的 `GetHtml` 方法代码类似于以下示例：</span><span class="sxs-lookup"><span data-stu-id="3ae14-168">(As with any method in C#, you must add `()` characters after the method.) The completed code for the `GetHtml` method looks like the following example:</span></span>

    [!code-cshtml[Main](program-asp-net-web-pages-in-visual-studio/samples/sample1.cshtml)]
4. <span data-ttu-id="3ae14-169">按 Ctrl + F5 运行页面。</span><span class="sxs-lookup"><span data-stu-id="3ae14-169">Press Ctrl+F5 to run the page.</span></span> <span data-ttu-id="3ae14-170">这是在浏览器中显示页面时的样子：</span><span class="sxs-lookup"><span data-stu-id="3ae14-170">This is what the page looks like when displayed in a browser:</span></span>

    ![浏览器中的默认页](program-asp-net-web-pages-in-visual-studio/_static/image5.png)
5. <span data-ttu-id="3ae14-172">关闭浏览器。</span><span class="sxs-lookup"><span data-stu-id="3ae14-172">Close the browser.</span></span>

### <a name="using-the-debugger"></a><span data-ttu-id="3ae14-173">使用调试器</span><span class="sxs-lookup"><span data-stu-id="3ae14-173">Using the Debugger</span></span>

1. <span data-ttu-id="3ae14-174">在默认的 " *cshtml* " 页的顶部，在 "`Page.Title`开头的行后添加以下代码行：</span><span class="sxs-lookup"><span data-stu-id="3ae14-174">At the top of the *Default.cshtml* page, after the line that begins with `Page.Title`, add the following line of code:</span></span>

    [!code-csharp[Main](program-asp-net-web-pages-in-visual-studio/samples/sample2.cs)]
2. <span data-ttu-id="3ae14-175">在编辑器的灰色边距中，单击此新行旁边的，以便添加*断点*。</span><span class="sxs-lookup"><span data-stu-id="3ae14-175">In the gray margin of the editor to the left of the code, click next to this new line in order to add a *breakpoint*.</span></span> <span data-ttu-id="3ae14-176">断点是通知调试器在该点停止运行程序的标记，这样您就可以看到发生了什么情况。</span><span class="sxs-lookup"><span data-stu-id="3ae14-176">A breakpoint is a marker that tells the debugger to stop running the program at that point so you can see what's happening.</span></span>

    ![设置断点](program-asp-net-web-pages-in-visual-studio/_static/image6.png)
3. <span data-ttu-id="3ae14-178">删除对 `ServerInfo.GetHtml` 方法的调用，并在其位置添加对 `@myTime` 变量的调用。</span><span class="sxs-lookup"><span data-stu-id="3ae14-178">Remove the call to the `ServerInfo.GetHtml` method, and add a call to the `@myTime` variable in its place.</span></span> <span data-ttu-id="3ae14-179">此调用显示新代码行返回的当前时间值。</span><span class="sxs-lookup"><span data-stu-id="3ae14-179">This call displays the current time value that's returned by the new line of code.</span></span>
4. <span data-ttu-id="3ae14-180">按 F5 在调试器中运行该页面。</span><span class="sxs-lookup"><span data-stu-id="3ae14-180">Press F5 to run the page in the debugger.</span></span> <span data-ttu-id="3ae14-181">该页在你设置的断点处停止。</span><span class="sxs-lookup"><span data-stu-id="3ae14-181">The page stops on the breakpoint that you set.</span></span> <span data-ttu-id="3ae14-182">下图显示了在具有断点（黄色）的编辑器中，页面的外观。</span><span class="sxs-lookup"><span data-stu-id="3ae14-182">The following image shows what the page looks like in the editor with the breakpoint (in yellow).</span></span>

    ![调试断点](program-asp-net-web-pages-in-visual-studio/_static/image7.png)
5. <span data-ttu-id="3ae14-184">在 "调试" 工具栏中，单击 "**单步**执行" 按钮（或按 F11）以运行下一行代码。</span><span class="sxs-lookup"><span data-stu-id="3ae14-184">In the Debug toolbar, click the **Step Into** button (or press F11) to run the next line of code.</span></span> <span data-ttu-id="3ae14-185">每次单击此按钮时，会将执行前进到下一行代码。</span><span class="sxs-lookup"><span data-stu-id="3ae14-185">Each time you click this button, you advance the execution to the next line of code.</span></span>

    !["单步执行" 按钮](program-asp-net-web-pages-in-visual-studio/_static/image8.png)
6. <span data-ttu-id="3ae14-187">通过将鼠标指针悬停在 `myTime` 变量上，或通过检查在 "**局部变量**" 和 "**调用堆栈**" 窗口中显示的值来检查变量的值。</span><span class="sxs-lookup"><span data-stu-id="3ae14-187">Examine the value of the `myTime` variable by holding your mouse pointer over it or by inspecting the values displayed in the **Locals** and **Call Stack** windows.</span></span> <span data-ttu-id="3ae14-188">Visual Studio 将显示变量的值。</span><span class="sxs-lookup"><span data-stu-id="3ae14-188">Visual Studio display the value of the variable.</span></span>

    ![显示时间值](program-asp-net-web-pages-in-visual-studio/_static/image9.png)
7. <span data-ttu-id="3ae14-190">完成检查变量并单步执行代码后，按 F5 继续运行页面，而不会在每一行停止。</span><span class="sxs-lookup"><span data-stu-id="3ae14-190">When you're done examining the variable and stepping through code, press F5 to continue running the page without stopping at each line.</span></span> <span data-ttu-id="3ae14-191">完成所有代码的逐句后，浏览器将显示该页。</span><span class="sxs-lookup"><span data-stu-id="3ae14-191">When you've finished stepping through all the code, the browser displays the page.</span></span>

<span data-ttu-id="3ae14-192">若要了解有关调试器以及如何在 Visual Studio 中调试代码的详细信息，请参阅[演练：在 Visual Web Developer 中调试网页](https://msdn.microsoft.com/library/z9e7w6cs.aspx)。</span><span class="sxs-lookup"><span data-stu-id="3ae14-192">To learn more about the debugger and about how to debug code in Visual Studio, see [Walkthrough: Debugging Web Pages in Visual Web Developer](https://msdn.microsoft.com/library/z9e7w6cs.aspx).</span></span>

## <a name="using-razor-in-aspnet-mvc-projects-with-visual-studio"></a><span data-ttu-id="3ae14-193">使用 Visual Studio 在 ASP.NET MVC 项目中使用 Razor</span><span class="sxs-lookup"><span data-stu-id="3ae14-193">Using Razor in ASP.NET MVC projects with Visual Studio</span></span>

<span data-ttu-id="3ae14-194">Razor 语法还广泛地用于 ASP.NET MVC 项目。</span><span class="sxs-lookup"><span data-stu-id="3ae14-194">The Razor syntax is also used extensively in ASP.NET MVC projects.</span></span> <span data-ttu-id="3ae14-195">MVC 是一种功能强大的基于模式的方式，用于生成动态网站。</span><span class="sxs-lookup"><span data-stu-id="3ae14-195">MVC is a powerful, patterns-based way to build dynamic websites.</span></span> <span data-ttu-id="3ae14-196">如果 ASP.NET 网页站点难以维护，则可以考虑将其转换为 ASP.NET MVC 应用程序。</span><span class="sxs-lookup"><span data-stu-id="3ae14-196">If your ASP.NET Web Pages site becomes difficult to maintain, you might want to consider converting it to an ASP.NET MVC application.</span></span> <span data-ttu-id="3ae14-197">有关创建 MVC 应用程序的示例，请参阅[入门 with ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="3ae14-197">For an example of creating an MVC application, see [Getting Started with ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md).</span></span>

<a id="vs2010support"></a>
## <a name="installing-support-for-aspnet-web-pages-in-visual-studio-2010"></a><span data-ttu-id="3ae14-198">在 Visual Studio 2010 中安装 ASP.NET 网页支持</span><span class="sxs-lookup"><span data-stu-id="3ae14-198">Installing Support for ASP.NET Web Pages in Visual Studio 2010</span></span>

<span data-ttu-id="3ae14-199">本部分介绍如何安装 Visual Web Developer Express 2010 和适用于 Visual Studio 的 ASP.NET 网页工具。</span><span class="sxs-lookup"><span data-stu-id="3ae14-199">This section shows how to install Visual Web Developer Express 2010 and the ASP.NET Web Pages Tools for Visual Studio.</span></span>

1. <span data-ttu-id="3ae14-200">如果还没有 Web 平台安装程序，请从以下 URL 下载：</span><span class="sxs-lookup"><span data-stu-id="3ae14-200">If you don't already have the Web Platform Installer, download it from the following URL:</span></span>

    [https://www.microsoft.com/web/downloads/platform.aspx](https://www.microsoft.com/web/downloads/platform.aspx)
2. <span data-ttu-id="3ae14-201">运行 Web 平台安装程序。</span><span class="sxs-lookup"><span data-stu-id="3ae14-201">Run the Web Platform Installer.</span></span>
3. <span data-ttu-id="3ae14-202">单击 "**产品**" 选项卡。</span><span class="sxs-lookup"><span data-stu-id="3ae14-202">Click the **Products** tab.</span></span>

    ![WebPI 产品选项卡](program-asp-net-web-pages-in-visual-studio/_static/image10.png)
4. <span data-ttu-id="3ae14-204">搜索**ASP.NET MVC 4** （对于 ASP.NET 网页2），然后单击 "**添加**"。</span><span class="sxs-lookup"><span data-stu-id="3ae14-204">Search for **ASP.NET MVC 4** (for ASP.NET Web Pages 2) and then click **Add**.</span></span> <span data-ttu-id="3ae14-205">这些产品包括用于生成 ASP.NET Razor 网站的 Visual Studio 工具。</span><span class="sxs-lookup"><span data-stu-id="3ae14-205">These products include Visual Studio tools for building ASP.NET Razor websites.</span></span>

    ![WebPi 安装选项](program-asp-net-web-pages-in-visual-studio/_static/image11.png)
5. <span data-ttu-id="3ae14-207">单击 "**安装**" 以完成安装。</span><span class="sxs-lookup"><span data-stu-id="3ae14-207">Click **Install** to complete the installation.</span></span>

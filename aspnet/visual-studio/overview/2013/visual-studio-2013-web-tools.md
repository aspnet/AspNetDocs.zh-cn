---
uid: visual-studio/overview/2013/visual-studio-2013-web-tools
title: 动手实验： Visual Studio 2013 Web Tools |Microsoft Docs
author: rick-anderson
description: Visual Studio 是的优秀开发环境。基于网络的 Windows 和 web 项目。 它包含一个功能强大的文本编辑器，可轻松用于 。
ms.author: riande
ms.date: 07/16/2014
ms.assetid: 09e82351-816b-402d-acd1-0f9ac6901d16
msc.legacyurl: /visual-studio/overview/2013/visual-studio-2013-web-tools
msc.type: authoredcontent
ms.openlocfilehash: 2fb987dd9b26ad9f0e8a88fd881bde4505ec4148
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78505004"
---
# <a name="hands-on-lab-visual-studio-2013-web-tools"></a><span data-ttu-id="6b910-104">动手实验： Visual Studio 2013 Web 工具</span><span class="sxs-lookup"><span data-stu-id="6b910-104">Hands On Lab: Visual Studio 2013 Web Tools</span></span>

<span data-ttu-id="6b910-105">由[Web 训练营团队](https://twitter.com/webcamps)使用</span><span class="sxs-lookup"><span data-stu-id="6b910-105">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="6b910-106">下载 Web 训练营培训工具包</span><span class="sxs-lookup"><span data-stu-id="6b910-106">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

> <span data-ttu-id="6b910-107">Visual Studio 是的优秀开发环境。基于网络的 Windows 和 web 项目。</span><span class="sxs-lookup"><span data-stu-id="6b910-107">Visual Studio is an excellent development environment for .NET-based Windows and web projects.</span></span> <span data-ttu-id="6b910-108">它包括一个功能强大的文本编辑器，可轻松地在没有项目的情况下编辑独立的文件。</span><span class="sxs-lookup"><span data-stu-id="6b910-108">It includes a powerful text editor that can easily be used to edit standalone files without a project.</span></span>
> 
> <span data-ttu-id="6b910-109">编辑每个文件时，Visual Studio 将保留功能完备的分析树。</span><span class="sxs-lookup"><span data-stu-id="6b910-109">Visual Studio maintains a full-featured parse tree as you edit each file.</span></span> <span data-ttu-id="6b910-110">这使 Visual Studio 能够提供无与伦比的自动完成功能和基于文档的操作，同时使开发体验变得更快、更愉快。</span><span class="sxs-lookup"><span data-stu-id="6b910-110">This allows Visual Studio to provide unparalleled auto-completion and document-based actions while making the development experience much faster and more pleasant.</span></span> <span data-ttu-id="6b910-111">这些功能在 HTML 和 CSS 文档中尤其有用。</span><span class="sxs-lookup"><span data-stu-id="6b910-111">These features are especially powerful in HTML and CSS documents.</span></span>
> 
> <span data-ttu-id="6b910-112">此功能的所有功能也可用于扩展，这使得使用强大的新功能扩展编辑器以满足你的需求。</span><span class="sxs-lookup"><span data-stu-id="6b910-112">All of this power is also available for extensions, making it simple to extend the editors with powerful new features to suit your needs.</span></span> <span data-ttu-id="6b910-113">Web Essentials 是（主要是） Visual Studio 的 web 相关增强功能的集合。</span><span class="sxs-lookup"><span data-stu-id="6b910-113">Web Essentials is a collection of (mostly) web-related enhancements to Visual Studio.</span></span> <span data-ttu-id="6b910-114">它包括许多新的 IntelliSense 完成（特别是对于 CSS）、新的浏览器链接功能、适用于 JavaScript 文件的自动 JSHint、HTML 和 CSS 的新警告以及对新式 web 开发所必需的许多其他功能。</span><span class="sxs-lookup"><span data-stu-id="6b910-114">It includes lots of new IntelliSense completions (especially for CSS), new Browser Link features, automatic JSHint for JavaScript files, new warnings for HTML and CSS, and many other features that are essential to modern web development.</span></span>
> 
> <span data-ttu-id="6b910-115">所有示例代码和代码段都包含在 Web 训练营培训工具包中， [https://aka.ms/webcamps-training-kit](https://aka.ms/webcamps-training-kit)提供。</span><span class="sxs-lookup"><span data-stu-id="6b910-115">All sample code and snippets are included in the Web Camps Training Kit, available at [https://aka.ms/webcamps-training-kit](https://aka.ms/webcamps-training-kit).</span></span>

<a id="Overview"></a>
## <a name="overview"></a><span data-ttu-id="6b910-116">概述</span><span class="sxs-lookup"><span data-stu-id="6b910-116">Overview</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="6b910-117">目标</span><span class="sxs-lookup"><span data-stu-id="6b910-117">Objectives</span></span>

<span data-ttu-id="6b910-118">在本动手实验中，您将了解如何：</span><span class="sxs-lookup"><span data-stu-id="6b910-118">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="6b910-119">使用 Web Essentials 中包含的新 HTML 编辑器功能，如丰富的 HTML5 代码段和 Zen 编码</span><span class="sxs-lookup"><span data-stu-id="6b910-119">Use new HTML editor features included in Web Essentials such as rich HTML5 code snippets and Zen coding</span></span>
- <span data-ttu-id="6b910-120">使用 Web Essentials 中包含的新 CSS 编辑器功能，如颜色选取器和浏览器矩阵工具提示</span><span class="sxs-lookup"><span data-stu-id="6b910-120">Use new CSS editor features included in Web Essentials such as the Color picker and Browser matrix tooltip</span></span>
- <span data-ttu-id="6b910-121">使用 Web Essentials 中包含的新 JavaScript 编辑器功能，如 "提取到文件" 和 "适用于所有 HTML 元素的 IntelliSense"</span><span class="sxs-lookup"><span data-stu-id="6b910-121">Use new JavaScript editor features included in Web Essentials such as Extract to File and IntelliSense for all HTML elements</span></span>
- <span data-ttu-id="6b910-122">使用浏览器链接在浏览器和 Visual Studio 之间交换数据</span><span class="sxs-lookup"><span data-stu-id="6b910-122">Exchange data between your browser and Visual Studio using Browser Link</span></span>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="6b910-123">系统必备</span><span class="sxs-lookup"><span data-stu-id="6b910-123">Prerequisites</span></span>

<span data-ttu-id="6b910-124">完成本动手实验需要以下各项：</span><span class="sxs-lookup"><span data-stu-id="6b910-124">The following is required to complete this hands-on lab:</span></span>

- <span data-ttu-id="6b910-125">[Microsoft Visual Studio Professional 2013](https://www.microsoft.com/visualstudio/)或更高版本</span><span class="sxs-lookup"><span data-stu-id="6b910-125">[Microsoft Visual Studio Professional 2013](https://www.microsoft.com/visualstudio/) or greater</span></span>
- [<span data-ttu-id="6b910-126">Web Essentials 2013</span><span class="sxs-lookup"><span data-stu-id="6b910-126">Web Essentials 2013</span></span>](http://vswebessentials.com/)
- [<span data-ttu-id="6b910-127">Google Chrome</span><span class="sxs-lookup"><span data-stu-id="6b910-127">Google Chrome</span></span>](https://www.google.com/chrome/)

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="6b910-128">安装</span><span class="sxs-lookup"><span data-stu-id="6b910-128">Setup</span></span>

<span data-ttu-id="6b910-129">若要运行此动手实验中的练习，您需要先设置您的环境。</span><span class="sxs-lookup"><span data-stu-id="6b910-129">In order to run the exercises in this hands-on lab, you will need to set up your environment first.</span></span>

1. <span data-ttu-id="6b910-130">打开 Windows 资源管理器窗口并浏览到实验室的**源**文件夹。</span><span class="sxs-lookup"><span data-stu-id="6b910-130">Open a Windows Explorer window and browse to the lab's **Source** folder.</span></span>
2. <span data-ttu-id="6b910-131">右键单击 " **setup.exe** "，然后选择 "以**管理员身份运行**" 以启动安装过程，该过程将配置环境并安装 Visual Studio code 代码段。</span><span class="sxs-lookup"><span data-stu-id="6b910-131">Right-click **Setup.cmd** and select **Run as administrator** to launch the setup process that will configure your environment and install the Visual Studio code snippets for this lab.</span></span>
3. <span data-ttu-id="6b910-132">如果显示了 "用户帐户控制" 对话框，请确认操作以继续。</span><span class="sxs-lookup"><span data-stu-id="6b910-132">If the User Account Control dialog box is shown, confirm the action to proceed.</span></span>

> [!NOTE]
> <span data-ttu-id="6b910-133">确保在运行安装过程之前，您已检查本实验的所有依赖项。</span><span class="sxs-lookup"><span data-stu-id="6b910-133">Make sure you have checked all the dependencies for this lab before running the setup.</span></span>

<a id="CodeSnippets"></a>
### <a name="using-the-code-snippets"></a><span data-ttu-id="6b910-134">使用代码段</span><span class="sxs-lookup"><span data-stu-id="6b910-134">Using the Code Snippets</span></span>

<span data-ttu-id="6b910-135">在整个实验文档中，将指示您插入代码块。</span><span class="sxs-lookup"><span data-stu-id="6b910-135">Throughout the lab document, you will be instructed to insert code blocks.</span></span> <span data-ttu-id="6b910-136">为方便起见，此代码的大部分作为 Visual Studio Code 代码段提供，你可以从 Visual Studio 2013 中访问这些代码段，以避免手动添加它。</span><span class="sxs-lookup"><span data-stu-id="6b910-136">For your convenience, most of this code is provided as Visual Studio Code Snippets, which you can access from within Visual Studio 2013 to avoid having to add it manually.</span></span>

> [!NOTE]
> <span data-ttu-id="6b910-137">每个练习都附带了一个起始解决方案，该解决方案位于练习的 "**开始**" 文件夹中，使您可以单独执行每个练习。</span><span class="sxs-lookup"><span data-stu-id="6b910-137">Each exercise is accompanied by a starting solution located in the **Begin** folder of the exercise that allows you to follow each exercise independently of the others.</span></span> <span data-ttu-id="6b910-138">请注意，这些开始解决方案中缺少在练习中添加的代码段，并且在完成此练习之前，可能无法工作。</span><span class="sxs-lookup"><span data-stu-id="6b910-138">Please be aware that the code snippets that are added during an exercise are missing from these starting solutions and may not work until you have completed the exercise.</span></span> <span data-ttu-id="6b910-139">在练习的源代码中，还会找到一个包含 Visual Studio 解决方案的**结束**文件夹，该解决方案的代码是完成相应练习中的步骤所产生的。</span><span class="sxs-lookup"><span data-stu-id="6b910-139">Inside the source code for an exercise, you will also find an **End** folder containing a Visual Studio solution with the code that results from completing the steps in the corresponding exercise.</span></span> <span data-ttu-id="6b910-140">如果您在演练本动手实验时需要其他帮助，则可以使用这些解决方案作为指南。</span><span class="sxs-lookup"><span data-stu-id="6b910-140">You can use these solutions as guidance if you need additional help as you work through this hands-on lab.</span></span>

---

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="6b910-141">练习</span><span class="sxs-lookup"><span data-stu-id="6b910-141">Exercises</span></span>

<span data-ttu-id="6b910-142">本动手实验包括以下练习：</span><span class="sxs-lookup"><span data-stu-id="6b910-142">This hands-on lab includes the following exercises:</span></span>

1. [<span data-ttu-id="6b910-143">使用浏览器链接和 Web Essentials</span><span class="sxs-lookup"><span data-stu-id="6b910-143">Working with Browser Link and Web Essentials</span></span>](#Exercise1)
2. [<span data-ttu-id="6b910-144">利用代码片段和 IntelliSense</span><span class="sxs-lookup"><span data-stu-id="6b910-144">Taking Advantage of Code Snippets and IntelliSense</span></span>](#Exercise2)

> [!NOTE]
> <span data-ttu-id="6b910-145">首次启动 Visual Studio 时，必须选择一个预定义的设置集合。</span><span class="sxs-lookup"><span data-stu-id="6b910-145">When you first start Visual Studio, you must select one of the predefined settings collections.</span></span> <span data-ttu-id="6b910-146">每个预定义的集合都设计为与特定的开发风格相匹配，并确定窗口布局、编辑器行为、IntelliSense 代码段和对话框选项。</span><span class="sxs-lookup"><span data-stu-id="6b910-146">Each predefined collection is designed to match a particular development style and determines window layouts, editor behavior, IntelliSense code snippets, and dialog box options.</span></span> <span data-ttu-id="6b910-147">此实验室中的过程描述在使用**常规开发设置**集合时，在 Visual Studio 中完成给定任务所需执行的操作。</span><span class="sxs-lookup"><span data-stu-id="6b910-147">The procedures in this lab describe the actions necessary to accomplish a given task in Visual Studio when using the **General Development Settings** collection.</span></span> <span data-ttu-id="6b910-148">如果为开发环境选择了其他设置集合，则需要考虑的步骤可能会有所不同。</span><span class="sxs-lookup"><span data-stu-id="6b910-148">If you choose a different settings collection for your development environment, there may be differences in the steps that you should take into account.</span></span>

<a id="Exercise1"></a>
### <a name="exercise-1-working-with-browser-link-and-web-essentials"></a><span data-ttu-id="6b910-149">练习1：使用浏览器链接和 Web Essentials</span><span class="sxs-lookup"><span data-stu-id="6b910-149">Exercise 1: Working with Browser Link and Web Essentials</span></span>

<span data-ttu-id="6b910-150">**Web Essentials**是一个 Visual Studio 扩展，它为新式 web 开发添加了各种有用的功能，主要侧重于使 web 开发体验变得更快、更愉快。</span><span class="sxs-lookup"><span data-stu-id="6b910-150">**Web Essentials** is a Visual Studio extension that adds a variety of useful features for modern web development, mostly focused on making the web development experience much faster and more pleasant.</span></span> <span data-ttu-id="6b910-151">你可以从 Visual Studio 中的扩展库安装 Web Essentials。</span><span class="sxs-lookup"><span data-stu-id="6b910-151">You can install Web Essentials from the Extension Gallery in Visual Studio.</span></span>

<span data-ttu-id="6b910-152">**Browser Link**是 Visual Studio 2013 中包含的一项新功能，它在 VISUAL studio IDE 和任何打开的浏览器之间提供通道，以在 web 应用程序和 Visual Studio 之间交换数据。</span><span class="sxs-lookup"><span data-stu-id="6b910-152">**Browser Link** is a new feature included in Visual Studio 2013 that provides a channel between the Visual Studio IDE and any open browser to exchange data between your web application and Visual Studio.</span></span> <span data-ttu-id="6b910-153">Web Essentials 通过工具扩展浏览器链接，直接从浏览器中操作您的网页的 DOM 对象模型和 CSS 样式。</span><span class="sxs-lookup"><span data-stu-id="6b910-153">Web Essentials extends Browser Link with tools to manipulate the DOM object model and the CSS styles of your web pages directly from the browser.</span></span>

<span data-ttu-id="6b910-154">在此练习中，您将探讨**Web Essentials**和**浏览器链接**支持的一些功能，以增强简单的测验页面。</span><span class="sxs-lookup"><span data-stu-id="6b910-154">In this exercise, you will explore some of the features supported by **Web Essentials** and **Browser Link** to enhance a simple quiz page.</span></span>

<a id="Ex1Task1"></a>
#### <a name="task-1---running-the-project-in-multiple-browsers"></a><span data-ttu-id="6b910-155">任务 1-在多个浏览器中运行项目</span><span class="sxs-lookup"><span data-stu-id="6b910-155">Task 1 - Running the Project in Multiple Browsers</span></span>

<span data-ttu-id="6b910-156">在此任务中，你要将 web 应用程序配置为一次在多个浏览器中运行，这对于跨浏览器测试非常有用。</span><span class="sxs-lookup"><span data-stu-id="6b910-156">In this task, you will configure your web application to run in multiple browsers at once, which is useful for cross-browser testing.</span></span>

1. <span data-ttu-id="6b910-157">打开**Microsoft Visual Studio**。</span><span class="sxs-lookup"><span data-stu-id="6b910-157">Open **Microsoft Visual Studio**.</span></span>
2. <span data-ttu-id="6b910-158">在 "**文件**" 菜单中选择 "**打开 |项目/解决方案 ...** 并浏览到实验室的**源**文件夹中的**Ex1-WorkingwithBrowserLinkandWebEssentials\Begin** （C:\WebCampsTK\HOL\VSWebTooling\Source）。</span><span class="sxs-lookup"><span data-stu-id="6b910-158">In the **File** menu, select **Open | Project/Solution...** and browse to **Ex1-WorkingwithBrowserLinkandWebEssentials\Begin** in the **Source** folder of the lab (C:\WebCampsTK\HOL\VSWebTooling\Source).</span></span> <span data-ttu-id="6b910-159">选择 "**开始**"，然后单击 "**打开**"。</span><span class="sxs-lookup"><span data-stu-id="6b910-159">Select **Begin.sln** and click **Open**.</span></span>
3. <span data-ttu-id="6b910-160">在 Visual Studio 工具栏中，展开浏览器菜单，然后选择 "**浏览方式**..."。</span><span class="sxs-lookup"><span data-stu-id="6b910-160">In the Visual Studio toolbar, expand the browser menu and select **Browse With...**.</span></span>

    <span data-ttu-id="6b910-161">!["浏览方式" 菜单选项](visual-studio-2013-web-tools/_static/image1.png "浏览方式 。浏览器菜单")</span><span class="sxs-lookup"><span data-stu-id="6b910-161">![Browse With menu option](visual-studio-2013-web-tools/_static/image1.png "Browse with... in browser menu")</span></span>

    <span data-ttu-id="6b910-162">*"浏览方式" 菜单选项*</span><span class="sxs-lookup"><span data-stu-id="6b910-162">*Browse With menu option*</span></span>
4. <span data-ttu-id="6b910-163">在 "**浏览方式**" 对话框中，通过按住**CTRL**键并单击 "**设为默认值**"，选择**Google Chrome**和**Internet Explorer** 。</span><span class="sxs-lookup"><span data-stu-id="6b910-163">In the **Browse With** dialog box, select both **Google Chrome** and **Internet Explorer** by holding down the **CTRL** key and click **Set as Default**.</span></span>

    <span data-ttu-id="6b910-164">!["浏览方式" 对话框](visual-studio-2013-web-tools/_static/image2.png ""浏览方式" 对话框")</span><span class="sxs-lookup"><span data-stu-id="6b910-164">![Browse with dialog box](visual-studio-2013-web-tools/_static/image2.png "Browse with dialog box")</span></span>

    <span data-ttu-id="6b910-165">*选择多个默认浏览器*</span><span class="sxs-lookup"><span data-stu-id="6b910-165">*Selecting multiple default browsers*</span></span>
5. <span data-ttu-id="6b910-166">Google Chrome 和 Internet Explorer 现在应显示为默认浏览器。</span><span class="sxs-lookup"><span data-stu-id="6b910-166">Both Google Chrome and Internet Explorer should now appear as the default browsers.</span></span> <span data-ttu-id="6b910-167">单击“取消”以关闭对话框。</span><span class="sxs-lookup"><span data-stu-id="6b910-167">Click **Cancel** to close the dialog box.</span></span>

    <span data-ttu-id="6b910-168">![作为默认浏览器的 Google Chrome 和 Internet Explorer](visual-studio-2013-web-tools/_static/image3.png "Google Chrome 和 Internet Explorer 默认浏览器")</span><span class="sxs-lookup"><span data-stu-id="6b910-168">![Google Chrome and Internet Explorer as default browsers](visual-studio-2013-web-tools/_static/image3.png "Google Chrome and Internet Explorer default browsers")</span></span>

    <span data-ttu-id="6b910-169">*作为默认浏览器的 Google Chrome 和 Internet Explorer*</span><span class="sxs-lookup"><span data-stu-id="6b910-169">*Google Chrome and Internet Explorer as default browsers*</span></span>

    > [!NOTE]
    > <span data-ttu-id="6b910-170">配置默认浏览器后，会在浏览器菜单中选择 "**多个浏览器**" 选项。</span><span class="sxs-lookup"><span data-stu-id="6b910-170">After configuring the default browsers, the **Multiple Browsers** option is selected in the browser menu.</span></span>
    > 
    > <span data-ttu-id="6b910-171">![多个浏览器](visual-studio-2013-web-tools/_static/image4.png "多个浏览器")</span><span class="sxs-lookup"><span data-stu-id="6b910-171">![Multiple browsers](visual-studio-2013-web-tools/_static/image4.png "Multiple browsers")</span></span>
6. <span data-ttu-id="6b910-172">按**CTRL** + **F5**运行应用程序而不进行调试。</span><span class="sxs-lookup"><span data-stu-id="6b910-172">Press **CTRL** + **F5** to run the application without debugging.</span></span>
7. <span data-ttu-id="6b910-173">当浏览器窗口打开时，将其中一个窗口放置在另一台上，以便同时查看两个浏览器上的更新。</span><span class="sxs-lookup"><span data-stu-id="6b910-173">When both browser windows open, place one of them above the other in order to see the updates on both browsers simultaneously.</span></span> <span data-ttu-id="6b910-174">浏览器应显示带有浅蓝色矩形的网页。</span><span class="sxs-lookup"><span data-stu-id="6b910-174">The browsers should display a web page with a light-blue rectangle.</span></span>

    <span data-ttu-id="6b910-175">![将一个浏览器放置在另一个浏览器之上](visual-studio-2013-web-tools/_static/image5.png "将一个浏览器放置在另一个浏览器之上")</span><span class="sxs-lookup"><span data-stu-id="6b910-175">![Placing one browser above the other](visual-studio-2013-web-tools/_static/image5.png "Placing one browser above the other")</span></span>

    <span data-ttu-id="6b910-176">*将一个浏览器放置在另一个浏览器之上*</span><span class="sxs-lookup"><span data-stu-id="6b910-176">*Placing one browser above the other*</span></span>
8. <span data-ttu-id="6b910-177">不要关闭浏览器。</span><span class="sxs-lookup"><span data-stu-id="6b910-177">Do not close the browsers.</span></span> <span data-ttu-id="6b910-178">你将在下一任务中使用它们。</span><span class="sxs-lookup"><span data-stu-id="6b910-178">You will use them in the next task.</span></span>

<a id="Ex1Task2"></a>
#### <a name="task-2---using-zen-coding-to-create-html-elements"></a><span data-ttu-id="6b910-179">任务 2-使用 Zen 编码创建 HTML 元素</span><span class="sxs-lookup"><span data-stu-id="6b910-179">Task 2 - Using Zen Coding to Create HTML Elements</span></span>

<span data-ttu-id="6b910-180">**Zen 编码**是用于高速 HTML、XML、XSL （或任何其他结构化代码格式）编码和编辑的编辑器插件。</span><span class="sxs-lookup"><span data-stu-id="6b910-180">**Zen Coding** is an editor plugin for high-speed HTML, XML, XSL (or any other structured code format) coding and editing.</span></span> <span data-ttu-id="6b910-181">此插件的核心是一个功能强大的缩写引擎，可用于将类似于 CSS 选择器的表达式展开为 HTML 代码。</span><span class="sxs-lookup"><span data-stu-id="6b910-181">The core of this plugin is a powerful abbreviation engine which allows you to expand expressions -similar to CSS selectors- into HTML code.</span></span> <span data-ttu-id="6b910-182">Zen 编码是一种使用 CSS 样式选择器语法编写 HTML 的快捷方法。</span><span class="sxs-lookup"><span data-stu-id="6b910-182">Zen Coding is a fast way to write HTML using a CSS style selector syntax.</span></span>

<span data-ttu-id="6b910-183">在此练习中，您将使用 Web Essentials 提供的 Zen 编码功能生成表示问题的选项的 HTML 按钮。</span><span class="sxs-lookup"><span data-stu-id="6b910-183">In this exercise, you will use the Zen Coding feature provided by Web Essentials to generate the HTML buttons that represent the options of the question.</span></span>

1. <span data-ttu-id="6b910-184">切换回 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="6b910-184">Switch back to Visual Studio.</span></span>
2. <span data-ttu-id="6b910-185">打开位于 | **Home**文件夹中的**视图**的**索引.**</span><span class="sxs-lookup"><span data-stu-id="6b910-185">Open the **Index.cshtml** file located in the **Views** | **Home** folder.</span></span>
3. <span data-ttu-id="6b910-186">**将&lt;!--TODO：在此处添加选项--&gt;** 注释替换为以下代码，然后按**tab**。</span><span class="sxs-lookup"><span data-stu-id="6b910-186">Replace the **&lt;!-- TODO: add options here--&gt;** comment with the following code, and press **TAB**.</span></span>

    [!code-css[Main](visual-studio-2013-web-tools/samples/sample1.css)]
4. <span data-ttu-id="6b910-187">应将代码扩展到 HTML。</span><span class="sxs-lookup"><span data-stu-id="6b910-187">The code should be expanded to HTML.</span></span>

    <span data-ttu-id="6b910-188">![扩展 HTML](visual-studio-2013-web-tools/_static/image6.png "扩展 HTML")</span><span class="sxs-lookup"><span data-stu-id="6b910-188">![Expanded HTML](visual-studio-2013-web-tools/_static/image6.png "Expanded HTML")</span></span>

    <span data-ttu-id="6b910-189">*扩展 HTML*</span><span class="sxs-lookup"><span data-stu-id="6b910-189">*Expanded HTML*</span></span>

    > [!NOTE]
    > <span data-ttu-id="6b910-190">若要了解有关 Zen 编码语法的详细信息，请参阅以下[文章](http://www.johnpapa.net/zen-coding-in-visual-studio-2012/)。</span><span class="sxs-lookup"><span data-stu-id="6b910-190">To learn more about Zen Coding syntax, see the following [article](http://www.johnpapa.net/zen-coding-in-visual-studio-2012/).</span></span>
5. <span data-ttu-id="6b910-191">单击 "**刷新链接浏览器**" 按钮可更新这两个浏览器。</span><span class="sxs-lookup"><span data-stu-id="6b910-191">Click the **Refresh linked browsers** button to update both browsers.</span></span>

    <span data-ttu-id="6b910-192">![刷新链接的浏览器](visual-studio-2013-web-tools/_static/image7.png "刷新链接的浏览器")</span><span class="sxs-lookup"><span data-stu-id="6b910-192">![Refresh linked browsers](visual-studio-2013-web-tools/_static/image7.png "Refresh linked browsers")</span></span>

    <span data-ttu-id="6b910-193">*刷新链接的浏览器*</span><span class="sxs-lookup"><span data-stu-id="6b910-193">*Refresh linked browsers*</span></span>

    <span data-ttu-id="6b910-194">![Internet Explorer-通过四个按钮更新页面](visual-studio-2013-web-tools/_static/image8.png "Internet Explorer-通过四个按钮更新页面")</span><span class="sxs-lookup"><span data-stu-id="6b910-194">![Internet Explorer - Page updated with four buttons](visual-studio-2013-web-tools/_static/image8.png "Internet Explorer - Page updated with four buttons")</span></span>

    <span data-ttu-id="6b910-195">*Internet Explorer-通过四个按钮更新页面*</span><span class="sxs-lookup"><span data-stu-id="6b910-195">*Internet Explorer - Page updated with four buttons*</span></span>

    <span data-ttu-id="6b910-196">![Google Chrome-已通过四个按钮更新页面](visual-studio-2013-web-tools/_static/image9.png "Google Chrome-已通过四个按钮更新页面")</span><span class="sxs-lookup"><span data-stu-id="6b910-196">![Google Chrome - Page updated with four buttons](visual-studio-2013-web-tools/_static/image9.png "Google Chrome - Page updated with four buttons")</span></span>

    <span data-ttu-id="6b910-197">*Google Chrome-已通过四个按钮更新页面*</span><span class="sxs-lookup"><span data-stu-id="6b910-197">*Google Chrome - Page updated with four buttons*</span></span>
6. <span data-ttu-id="6b910-198">切换回 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="6b910-198">Switch back to Visual Studio.</span></span>
7. <span data-ttu-id="6b910-199">您已将这些按钮添加到页面中，但仍需要添加一个模板问题。</span><span class="sxs-lookup"><span data-stu-id="6b910-199">You have added the buttons to the page, but you still need to add a template question.</span></span> <span data-ttu-id="6b910-200">为此，你将使用 Web Essentials 中名为**Lorem Ipsum 生成器**的新功能。</span><span class="sxs-lookup"><span data-stu-id="6b910-200">To do so, you will use a new feature in Web Essentials called **Lorem Ipsum generator**.</span></span> <span data-ttu-id="6b910-201">找到具有**类**属性 "**前部**" 的**div**元素。</span><span class="sxs-lookup"><span data-stu-id="6b910-201">Locate the **div** element with the **class** attribute **front**.</span></span>
8. <span data-ttu-id="6b910-202">添加以下代码作为**div**的第一个子元素，然后按**tab**。</span><span class="sxs-lookup"><span data-stu-id="6b910-202">Add the following code as the first child element of the **div**, and press **TAB**.</span></span>

    [!code-css[Main](visual-studio-2013-web-tools/samples/sample2.css)]
9. <span data-ttu-id="6b910-203">应将代码扩展到 HTML。</span><span class="sxs-lookup"><span data-stu-id="6b910-203">The code should be expanded to HTML.</span></span>

    <span data-ttu-id="6b910-204">![Lorem Ipsum 自动生成](visual-studio-2013-web-tools/_static/image10.png "Lorem Ipsum 自动生成")</span><span class="sxs-lookup"><span data-stu-id="6b910-204">![Lorem Ipsum autogenerated](visual-studio-2013-web-tools/_static/image10.png "Lorem Ipsum autogenerated")</span></span>

    <span data-ttu-id="6b910-205">*Lorem Ipsum 自动生成*</span><span class="sxs-lookup"><span data-stu-id="6b910-205">*Lorem Ipsum autogenerated*</span></span>

    > [!NOTE]
    > <span data-ttu-id="6b910-206">作为 Zen 编码的一部分，现在可以直接在 HTML 编辑器中生成 Lorem Ipsum 代码。</span><span class="sxs-lookup"><span data-stu-id="6b910-206">As part of Zen Coding, you can now generate Lorem Ipsum code directly in the HTML editor.</span></span> <span data-ttu-id="6b910-207">只需键入 "lorem **" 和 "命中" 选项卡**，将插入一个30个 word lorem Ipsum 文本。</span><span class="sxs-lookup"><span data-stu-id="6b910-207">Simply type **lorem** and hit **TAB** and a 30 word Lorem Ipsum text will be inserted.</span></span> <span data-ttu-id="6b910-208">例如，</span><span class="sxs-lookup"><span data-stu-id="6b910-208">E.g.</span></span> <span data-ttu-id="6b910-209">*lorem10*插入10个 Lorem Ipsum 词。</span><span class="sxs-lookup"><span data-stu-id="6b910-209">*lorem10* inserts 10 Lorem Ipsum words.</span></span>
10. <span data-ttu-id="6b910-210">你将在问题的顶部添加徽标，方法是使用名为**Lorem 像素生成器**的 Web Essentials 中的另一个新功能。</span><span class="sxs-lookup"><span data-stu-id="6b910-210">You will add a logo at the top of the question by using another new feature in Web Essentials called **Lorem Pixel generator**.</span></span> <span data-ttu-id="6b910-211">将以下代码添加为**div**元素的第一个子元素，并将**容器**作为**类**值，并按**tab**。</span><span class="sxs-lookup"><span data-stu-id="6b910-211">Add the following code as the first child element of the **div** element with **container** as **class** value, and press **TAB**.</span></span>

    [!code-css[Main](visual-studio-2013-web-tools/samples/sample3.css)]
11. <span data-ttu-id="6b910-212">代码应扩展到 HTML。</span><span class="sxs-lookup"><span data-stu-id="6b910-212">The code should expand to HTML.</span></span>

    <span data-ttu-id="6b910-213">![自动生成 Lorem 像素](visual-studio-2013-web-tools/_static/image11.png "自动生成 Lorem 像素")</span><span class="sxs-lookup"><span data-stu-id="6b910-213">![Lorem Pixel autogenerated](visual-studio-2013-web-tools/_static/image11.png "Lorem Pixel autogenerated")</span></span>

    <span data-ttu-id="6b910-214">*自动生成 Lorem 像素*</span><span class="sxs-lookup"><span data-stu-id="6b910-214">*Lorem Pixel autogenerated*</span></span>

    > [!NOTE]
    > <span data-ttu-id="6b910-215">作为 Zen 编码的一部分，还可以在 HTML 编辑器中直接生成 Lorem 像素代码。</span><span class="sxs-lookup"><span data-stu-id="6b910-215">As part of Zen Coding, you can also generate Lorem Pixel code directly in the HTML editor.</span></span> <span data-ttu-id="6b910-216">只需键入 " **200X200 大小"-** "动物 **" 和 "点击" 选项卡**，即可插入带有动物200x200 大小图像的**img**标记。</span><span class="sxs-lookup"><span data-stu-id="6b910-216">Simply type **pix-200x200-animals** and hit **TAB** and an **img** tag with a 200x200 image of an animal will be inserted.</span></span> <span data-ttu-id="6b910-217">有关详细信息，请参阅[Lorem 像素](http://www.lorempixel.com)。</span><span class="sxs-lookup"><span data-stu-id="6b910-217">For more information, refer to [Lorem Pixel](http://www.lorempixel.com).</span></span>
12. <span data-ttu-id="6b910-218">单击 "**刷新链接浏览器**" 按钮可更新这两个浏览器。</span><span class="sxs-lookup"><span data-stu-id="6b910-218">Click the **Refresh linked browsers** button to update both browsers.</span></span>

    <span data-ttu-id="6b910-219">![Internet Explorer-自动生成的图像和文本](visual-studio-2013-web-tools/_static/image12.png "Internet Explorer-自动生成的图像和文本")</span><span class="sxs-lookup"><span data-stu-id="6b910-219">![Internet Explorer - Autogenerated image and text](visual-studio-2013-web-tools/_static/image12.png "Internet Explorer - Autogenerated image and text")</span></span>

    <span data-ttu-id="6b910-220">*Internet Explorer-自动生成的图像和文本*</span><span class="sxs-lookup"><span data-stu-id="6b910-220">*Internet Explorer - Autogenerated image and text*</span></span>

    <span data-ttu-id="6b910-221">![Google Chrome-自动生成的图像和文本](visual-studio-2013-web-tools/_static/image13.png "Google Chrome-自动生成的图像和文本")</span><span class="sxs-lookup"><span data-stu-id="6b910-221">![Google Chrome - Autogenerated image and text](visual-studio-2013-web-tools/_static/image13.png "Google Chrome - Autogenerated image and text")</span></span>

    <span data-ttu-id="6b910-222">*Google Chrome-自动生成的图像和文本*</span><span class="sxs-lookup"><span data-stu-id="6b910-222">*Google Chrome - Autogenerated image and text*</span></span>

    > [!NOTE]
    > <span data-ttu-id="6b910-223">由于添加代码段时，会随机选择图像，因此浏览器中显示的图像可能会有所不同。</span><span class="sxs-lookup"><span data-stu-id="6b910-223">Because the image is selected randomly when adding the code snippet, the image shown in the browsers may differ.</span></span>
13. <span data-ttu-id="6b910-224">不要关闭浏览器。</span><span class="sxs-lookup"><span data-stu-id="6b910-224">Do not close the browsers.</span></span> <span data-ttu-id="6b910-225">你将在下一任务中使用它们。</span><span class="sxs-lookup"><span data-stu-id="6b910-225">You will use them in the next task.</span></span>

<a id="Ex1Task3"></a>
#### <a name="task-3---updating-a-style-property"></a><span data-ttu-id="6b910-226">任务 3-更新样式属性</span><span class="sxs-lookup"><span data-stu-id="6b910-226">Task 3 - Updating a Style Property</span></span>

<span data-ttu-id="6b910-227">在此任务中，您将使用浏览器链接的**检查模式**功能来检测生成特定 DOM 元素的确切位置，然后使用 Web Essentials 提供的颜色选取器更新该元素的颜色属性。</span><span class="sxs-lookup"><span data-stu-id="6b910-227">In this task, you will use the Browser Link's **Inspect Mode** feature to detect the exact location where the specific DOM element is generated and then update the color property of that element using a color picker provided by Web Essentials.</span></span>

1. <span data-ttu-id="6b910-228">在 Internet Explorer 浏览器中，按**CTRL** + **ALT** + **I**启用检查模式。</span><span class="sxs-lookup"><span data-stu-id="6b910-228">In the Internet Explorer browser, press **CTRL** + **ALT** + **I** to enable Inspect Mode.</span></span>
2. <span data-ttu-id="6b910-229">将指针移到浅蓝色边框上，然后单击。</span><span class="sxs-lookup"><span data-stu-id="6b910-229">Move the pointer over the light blue border and click.</span></span>

    <span data-ttu-id="6b910-230">![将指针移到浅蓝色边框上](visual-studio-2013-web-tools/_static/image14.png "将指针移到浅蓝色边框上")</span><span class="sxs-lookup"><span data-stu-id="6b910-230">![Moving the pointer over the light blue border](visual-studio-2013-web-tools/_static/image14.png "Moving the pointer over the light blue border")</span></span>

    <span data-ttu-id="6b910-231">*将指针移到浅蓝色边框上*</span><span class="sxs-lookup"><span data-stu-id="6b910-231">*Moving the pointer over the light blue border*</span></span>
3. <span data-ttu-id="6b910-232">切换回 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="6b910-232">Switch back to Visual Studio.</span></span> <span data-ttu-id="6b910-233">请注意，在浏览器中选择的 HTML 元素也会在 Visual Studio HTML 编辑器中进行选择。</span><span class="sxs-lookup"><span data-stu-id="6b910-233">Notice how the HTML element that you selected in the browser is also selected in the Visual Studio HTML editor.</span></span>

    <span data-ttu-id="6b910-234">![Visual Studio HTML 编辑器中选定的 HTML 元素](visual-studio-2013-web-tools/_static/image15.png "Visual Studio HTML 编辑器中选定的 HTML 元素")</span><span class="sxs-lookup"><span data-stu-id="6b910-234">![HTML element selected in the Visual Studio HTML editor](visual-studio-2013-web-tools/_static/image15.png "HTML element selected in the Visual Studio HTML editor")</span></span>

    <span data-ttu-id="6b910-235">*Visual Studio HTML 编辑器中选定的 HTML 元素*</span><span class="sxs-lookup"><span data-stu-id="6b910-235">*HTML element selected in the Visual Studio HTML editor*</span></span>
4. <span data-ttu-id="6b910-236">现在，您将更新**前**一个 CSS 类，以便更改所选元素的样式。</span><span class="sxs-lookup"><span data-stu-id="6b910-236">You will now update the **front** CSS class in order to change the styling of the selected element.</span></span> <span data-ttu-id="6b910-237">为此，请按**CTRL** + **打开**"**导航到**搜索" 框。</span><span class="sxs-lookup"><span data-stu-id="6b910-237">To do so, press **CTRL** + **,** to open the **Navigate To** search box.</span></span> <span data-ttu-id="6b910-238">键入 **"** "，然后按**enter**以打开文件。</span><span class="sxs-lookup"><span data-stu-id="6b910-238">Type **site.css** and press **ENTER** to open the file.</span></span>

    <span data-ttu-id="6b910-239">![正在打开文件站点 css](visual-studio-2013-web-tools/_static/image16.png "正在打开文件站点 css")</span><span class="sxs-lookup"><span data-stu-id="6b910-239">![Opening file Site.css](visual-studio-2013-web-tools/_static/image16.png "Opening file Site.css")</span></span>

    <span data-ttu-id="6b910-240">*正在打开文件站点 css*</span><span class="sxs-lookup"><span data-stu-id="6b910-240">*Opening file Site.css*</span></span>
5. <span data-ttu-id="6b910-241">按**CTRL** + **F** ，然后**键入，** 查找 CSS 选择器。</span><span class="sxs-lookup"><span data-stu-id="6b910-241">Press **CTRL** + **F** and type **.flip-container .front** to find the CSS selector.</span></span>
6. <span data-ttu-id="6b910-242">在类的 border 属性中单击浅蓝色正方形，以打开颜色选取器。</span><span class="sxs-lookup"><span data-stu-id="6b910-242">Click the light blue square in the border property of the class to open the Color Picker.</span></span>

    <span data-ttu-id="6b910-243">![打开颜色选取器](visual-studio-2013-web-tools/_static/image17.png "打开颜色选取器")</span><span class="sxs-lookup"><span data-stu-id="6b910-243">![Opening the Color Picker](visual-studio-2013-web-tools/_static/image17.png "Opening the Color Picker")</span></span>

    <span data-ttu-id="6b910-244">*打开颜色选取器*</span><span class="sxs-lookup"><span data-stu-id="6b910-244">*Opening the Color Picker*</span></span>
7. <span data-ttu-id="6b910-245">通过单击 v 形按钮展开颜色选取器，然后选择一种新颜色。</span><span class="sxs-lookup"><span data-stu-id="6b910-245">Expand the Color Picker by clicking the chevron button and select a new color.</span></span>

    <span data-ttu-id="6b910-246">![展开颜色选取器](visual-studio-2013-web-tools/_static/image18.png "展开颜色选取器")</span><span class="sxs-lookup"><span data-stu-id="6b910-246">![Expanding the Color Picker](visual-studio-2013-web-tools/_static/image18.png "Expanding the Color Picker")</span></span>

    <span data-ttu-id="6b910-247">*展开颜色选取器*</span><span class="sxs-lookup"><span data-stu-id="6b910-247">*Expanding the Color Picker*</span></span>
8. <span data-ttu-id="6b910-248">按**CTRL** + **ALT** + **enter**以刷新链接的浏览器。</span><span class="sxs-lookup"><span data-stu-id="6b910-248">Press **CTRL** + **ALT** + **ENTER** to refresh linked browsers.</span></span>
9. <span data-ttu-id="6b910-249">切换到 Internet Explorer，并注意边框的颜色如何变化。</span><span class="sxs-lookup"><span data-stu-id="6b910-249">Switch to Internet Explorer and notice how the color of the border has changed.</span></span>

    <span data-ttu-id="6b910-250">![Internet Explorer-已更新边框颜色](visual-studio-2013-web-tools/_static/image19.png "Internet Explorer-已更新边框颜色")</span><span class="sxs-lookup"><span data-stu-id="6b910-250">![Internet Explorer - Border color updated](visual-studio-2013-web-tools/_static/image19.png "Internet Explorer - Border color updated")</span></span>

    <span data-ttu-id="6b910-251">*Internet Explorer-已更新边框颜色*</span><span class="sxs-lookup"><span data-stu-id="6b910-251">*Internet Explorer - Border color updated*</span></span>
10. <span data-ttu-id="6b910-252">切换到 Google Chrome 并注意边框的颜色如何变化。</span><span class="sxs-lookup"><span data-stu-id="6b910-252">Switch to Google Chrome and notice how the color of the border has changed.</span></span>

    <span data-ttu-id="6b910-253">![Google Chrome-已更新边框颜色](visual-studio-2013-web-tools/_static/image20.png "Google Chrome-已更新边框颜色")</span><span class="sxs-lookup"><span data-stu-id="6b910-253">![Google Chrome - Border color updated](visual-studio-2013-web-tools/_static/image20.png "Google Chrome - Border color updated")</span></span>

    <span data-ttu-id="6b910-254">*Google Chrome-已更新边框颜色*</span><span class="sxs-lookup"><span data-stu-id="6b910-254">*Google Chrome - Border color updated*</span></span>
11. <span data-ttu-id="6b910-255">切换回 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="6b910-255">Switch back to Visual Studio.</span></span>
12. <span data-ttu-id="6b910-256">请在**web.config**文件的末尾，按**CTRL** + **F**查找**btn**选择器。</span><span class="sxs-lookup"><span data-stu-id="6b910-256">Go to the end of the **Site.css** file and press **CTRL** + **F** to locate the **.btn** selector.</span></span>
13. <span data-ttu-id="6b910-257">请注意， **-webkit**属性以绿色下划线表示。</span><span class="sxs-lookup"><span data-stu-id="6b910-257">Notice that the **-webkit-border-radius** property is underlined in green.</span></span>

    <span data-ttu-id="6b910-258">![-btn 选择器的 webkit-radius 属性](visual-studio-2013-web-tools/_static/image21.png "-btn 选择器的 webkit-radius 属性")</span><span class="sxs-lookup"><span data-stu-id="6b910-258">![-webkit-border-radius property of the btn selector](visual-studio-2013-web-tools/_static/image21.png "-webkit-border-radius property of the btn selector")</span></span>

    <span data-ttu-id="6b910-259">*-btn 选择器的 webkit-radius 属性*</span><span class="sxs-lookup"><span data-stu-id="6b910-259">*-webkit-border-radius property of the btn selector*</span></span>
14. <span data-ttu-id="6b910-260">将插入符号放置在 **-webkit**属性中。</span><span class="sxs-lookup"><span data-stu-id="6b910-260">Place the caret in the **-webkit-border-radius** property.</span></span> <span data-ttu-id="6b910-261">该属性的第一个单词的第一个字母下应显示一条蓝线。</span><span class="sxs-lookup"><span data-stu-id="6b910-261">A blue line should appear under the first letter of the first word of the property.</span></span> <span data-ttu-id="6b910-262">这是**智能标记**。</span><span class="sxs-lookup"><span data-stu-id="6b910-262">This is the **smart tag**.</span></span>
15. <span data-ttu-id="6b910-263">按**CTRL** +  **。**</span><span class="sxs-lookup"><span data-stu-id="6b910-263">Press **CTRL** + **.**</span></span> <span data-ttu-id="6b910-264">打开 "建议" 菜单，并单击 "**添加缺少的标准属性（边框-半径）** "。</span><span class="sxs-lookup"><span data-stu-id="6b910-264">to open the suggestions menu and click **Add missing standard property (border-radius)**.</span></span>

    <span data-ttu-id="6b910-265">![添加缺少的标准属性建议](visual-studio-2013-web-tools/_static/image22.png "添加缺少的标准属性建议")</span><span class="sxs-lookup"><span data-stu-id="6b910-265">![Add missing standard property suggestion](visual-studio-2013-web-tools/_static/image22.png "Add missing standard property suggestion")</span></span>

    <span data-ttu-id="6b910-266">*添加缺少的标准属性建议*</span><span class="sxs-lookup"><span data-stu-id="6b910-266">*Add missing standard property suggestion*</span></span>
16. <span data-ttu-id="6b910-267">**边框-radius**属性会自动添加到 CSS 规则。</span><span class="sxs-lookup"><span data-stu-id="6b910-267">The **border-radius** property is automatically added to the CSS rule.</span></span>

    <span data-ttu-id="6b910-268">![缺少添加的标准属性](visual-studio-2013-web-tools/_static/image23.png "缺少添加的标准属性")</span><span class="sxs-lookup"><span data-stu-id="6b910-268">![Missing standard property added](visual-studio-2013-web-tools/_static/image23.png "Missing standard property added")</span></span>

    <span data-ttu-id="6b910-269">*缺少添加的标准属性*</span><span class="sxs-lookup"><span data-stu-id="6b910-269">*Missing standard property added*</span></span>
17. <span data-ttu-id="6b910-270">将指针移到**边框-半径**属性上以显示**浏览器矩阵工具提示**。</span><span class="sxs-lookup"><span data-stu-id="6b910-270">Move the pointer over the **border-radius** property to display the **Browser matrix tooltip**.</span></span> <span data-ttu-id="6b910-271">**Browser matrix 工具提示**在每个浏览器中显示属性的可用性。</span><span class="sxs-lookup"><span data-stu-id="6b910-271">The **Browser matrix tooltip** shows the availability of the property in each browser.</span></span>

    <span data-ttu-id="6b910-272">![浏览器矩阵工具提示](visual-studio-2013-web-tools/_static/image24.png "浏览器矩阵工具提示")</span><span class="sxs-lookup"><span data-stu-id="6b910-272">![Browser matrix tooltip](visual-studio-2013-web-tools/_static/image24.png "Browser matrix tooltip")</span></span>

    <span data-ttu-id="6b910-273">*浏览器矩阵工具提示*</span><span class="sxs-lookup"><span data-stu-id="6b910-273">*Browser matrix tooltip*</span></span>
18. <span data-ttu-id="6b910-274">请注意，**边框-radius**属性的值仍带有下划线。</span><span class="sxs-lookup"><span data-stu-id="6b910-274">Notice that the value of the **border-radius** property is still underlined.</span></span> <span data-ttu-id="6b910-275">将指针移到值上可查看警告消息。</span><span class="sxs-lookup"><span data-stu-id="6b910-275">Move the pointer over the value to see the warning message.</span></span>

    <span data-ttu-id="6b910-276">![边框-radius 属性值警告](visual-studio-2013-web-tools/_static/image25.png "边框-radius 属性值警告")</span><span class="sxs-lookup"><span data-stu-id="6b910-276">![Border-radius property value warning](visual-studio-2013-web-tools/_static/image25.png "Border-radius property value warning")</span></span>

    <span data-ttu-id="6b910-277">*边框-radius 属性值警告*</span><span class="sxs-lookup"><span data-stu-id="6b910-277">*Border-radius property value warning*</span></span>
19. <span data-ttu-id="6b910-278">如工具提示所建议，删除**边框-radius**属性值的单位。</span><span class="sxs-lookup"><span data-stu-id="6b910-278">Remove the unit of the **border-radius** property value as suggested by the tooltip.</span></span>
20. <span data-ttu-id="6b910-279">作为**边框-半径**是用于定义圆角边框的的标准属性，您可以从 CSS 规则中删除 **-webkit-radius**属性和值。</span><span class="sxs-lookup"><span data-stu-id="6b910-279">As **border-radius** is the standard property for defining how rounded border corners are, you can remove the **-webkit-border-radius** property and value from the CSS rule.</span></span>
21. <span data-ttu-id="6b910-280">将插入符号放置在**自动换行**属性中，可以看到智能标记也显示在下方。</span><span class="sxs-lookup"><span data-stu-id="6b910-280">Place the caret in the **word-wrap** property and notice that the smart tag also appears below.</span></span>
22. <span data-ttu-id="6b910-281">打开菜单，然后单击 "**添加缺少的供应商详细信息**"。</span><span class="sxs-lookup"><span data-stu-id="6b910-281">Open the menu and click **Add missing vendor specifics**.</span></span>

    <span data-ttu-id="6b910-282">![添加缺少的供应商详细信息建议](visual-studio-2013-web-tools/_static/image26.png "添加缺少的供应商详细信息建议")</span><span class="sxs-lookup"><span data-stu-id="6b910-282">![Add missing vendor specifics suggestion](visual-studio-2013-web-tools/_static/image26.png "Add missing vendor specifics suggestion")</span></span>

    <span data-ttu-id="6b910-283">*添加缺少的供应商详细信息建议*</span><span class="sxs-lookup"><span data-stu-id="6b910-283">*Add missing vendor specifics suggestion*</span></span>
23. <span data-ttu-id="6b910-284">**-Ms 自动换行**属性会自动添加到 CSS 规则。</span><span class="sxs-lookup"><span data-stu-id="6b910-284">The **-ms-word-wrap** property is automatically added to the CSS rule.</span></span>

    <span data-ttu-id="6b910-285">![添加的供应商特定属性](visual-studio-2013-web-tools/_static/image27.png "添加的供应商特定属性")</span><span class="sxs-lookup"><span data-stu-id="6b910-285">![Vendor specific property added](visual-studio-2013-web-tools/_static/image27.png "Vendor specific property added")</span></span>

    <span data-ttu-id="6b910-286">*添加的供应商特定属性*</span><span class="sxs-lookup"><span data-stu-id="6b910-286">*Vendor specific property added*</span></span>

<a id="Ex1Task4"></a>
#### <a name="task-4---updating-the-html-code-from-the-browser"></a><span data-ttu-id="6b910-287">任务 4-从浏览器更新 HTML 代码</span><span class="sxs-lookup"><span data-stu-id="6b910-287">Task 4 - Updating the HTML Code from the Browser</span></span>

<span data-ttu-id="6b910-288">在此任务中，您将使用浏览器链接的**设计模式**功能在浏览器中编辑 DOM 对象，并将更改传输到 Visual Studio 中的 HTML 源文件。</span><span class="sxs-lookup"><span data-stu-id="6b910-288">In this task, you will use the Browser Link's **Design Mode** feature to edit the DOM object from the browser and transfer the changes to the HTML source file in Visual Studio.</span></span>

1. <span data-ttu-id="6b910-289">在 Google Chrome 中，按**CTRL** + **ALT** + **D**启用设计模式。</span><span class="sxs-lookup"><span data-stu-id="6b910-289">In Google Chrome, press **CTRL** + **ALT** + **D** to enable Design Mode.</span></span>
2. <span data-ttu-id="6b910-290">将指针移到**Lorem Ipsum dolor sit amet**标签上，然后单击。</span><span class="sxs-lookup"><span data-stu-id="6b910-290">Move the pointer over the **Lorem Ipsum dolor sit amet** label and click.</span></span>

    <span data-ttu-id="6b910-291">![编辑问题](visual-studio-2013-web-tools/_static/image28.png "编辑问题")</span><span class="sxs-lookup"><span data-stu-id="6b910-291">![Editing the question](visual-studio-2013-web-tools/_static/image28.png "Editing the question")</span></span>

    <span data-ttu-id="6b910-292">*编辑问题*</span><span class="sxs-lookup"><span data-stu-id="6b910-292">*Editing the question*</span></span>
3. <span data-ttu-id="6b910-293">应显示一个游标。</span><span class="sxs-lookup"><span data-stu-id="6b910-293">A cursor should appear.</span></span> <span data-ttu-id="6b910-294">将原始文本替换为*写入更长问题时的外观*，然后按**ESC**退出设计模式。</span><span class="sxs-lookup"><span data-stu-id="6b910-294">Replace the original text with *What does it look like when I write a longer question?*, and then press **ESC** to exit Design Mode.</span></span>

    <span data-ttu-id="6b910-295">![已编辑问题](visual-studio-2013-web-tools/_static/image29.png "已编辑问题")</span><span class="sxs-lookup"><span data-stu-id="6b910-295">![Question edited](visual-studio-2013-web-tools/_static/image29.png "Question edited")</span></span>

    <span data-ttu-id="6b910-296">*已编辑问题*</span><span class="sxs-lookup"><span data-stu-id="6b910-296">*Question edited*</span></span>
4. <span data-ttu-id="6b910-297">如果尚未打开，请切换回 Visual Studio 并打开 "**索引"。**</span><span class="sxs-lookup"><span data-stu-id="6b910-297">Switch back to Visual Studio and open **Index.cshtml**, if not already opened.</span></span> <span data-ttu-id="6b910-298">请注意，已更新 **&lt;p&gt;** 元素的内部文本。</span><span class="sxs-lookup"><span data-stu-id="6b910-298">Notice that the inner text of the **&lt;p&gt;** element has been updated.</span></span>

    <span data-ttu-id="6b910-299">![HTML 页中已更新的问题](visual-studio-2013-web-tools/_static/image30.png "HTML 页中已更新的问题")</span><span class="sxs-lookup"><span data-stu-id="6b910-299">![Updated question in the HTML page](visual-studio-2013-web-tools/_static/image30.png "Updated question in the HTML page")</span></span>

    <span data-ttu-id="6b910-300">*HTML 页中已更新的问题*</span><span class="sxs-lookup"><span data-stu-id="6b910-300">*Updated question in the HTML page*</span></span>

<a id="Ex1Task5"></a>
#### <a name="task-5---reviewing-seo-related-warnings"></a><span data-ttu-id="6b910-301">任务 5-查看 SEO 相关警告</span><span class="sxs-lookup"><span data-stu-id="6b910-301">Task 5 - Reviewing SEO Related Warnings</span></span>

<span data-ttu-id="6b910-302">**搜索引擎优化**（SEO）是在搜索引擎的结果列表中使网站排名更高的过程。</span><span class="sxs-lookup"><span data-stu-id="6b910-302">**Search Engine Optimization** (SEO) is the process of making a website rank higher on a search engine's list of results.</span></span> <span data-ttu-id="6b910-303">站点排名越高，列出的一致性越多，该站点从该搜索引擎获得的访问者就越多。</span><span class="sxs-lookup"><span data-stu-id="6b910-303">The higher the site ranks and the more consistently it is listed, the more visitors the site will get from that search engine.</span></span> <span data-ttu-id="6b910-304">Web Essentials 包含一个分析工具，该工具可检查 HTML、报告发现的问题并为修复这些问题提供帮助。</span><span class="sxs-lookup"><span data-stu-id="6b910-304">Web Essentials incorporates an analytical tool that examines HTML, reports the issues found and provides assistance to fix them.</span></span>

1. <span data-ttu-id="6b910-305">中转到 "**视图**" 菜单，然后单击 "**错误列表**" 打开 "**错误列表**" 窗口。</span><span class="sxs-lookup"><span data-stu-id="6b910-305">Go to the **View** menu and click **Error List** to open the **Error List** window.</span></span>

    <span data-ttu-id="6b910-306">!["视图" 菜单中的错误列表](visual-studio-2013-web-tools/_static/image31.png ""视图" 菜单中的错误列表")</span><span class="sxs-lookup"><span data-stu-id="6b910-306">![Error List in View menu](visual-studio-2013-web-tools/_static/image31.png "Error List in View menu")</span></span>

    <span data-ttu-id="6b910-307">*"视图" 菜单中的错误列表*</span><span class="sxs-lookup"><span data-stu-id="6b910-307">*Error List in View menu*</span></span>
2. <span data-ttu-id="6b910-308">请注意，会出现一个 SEO 警告，通知缺少页面说明 **&lt;元&gt;** 标记。</span><span class="sxs-lookup"><span data-stu-id="6b910-308">Notice that there is an SEO warning notifying that a **&lt;meta&gt;** tag for the page description is missing.</span></span> <span data-ttu-id="6b910-309">双击 "SEO 警告" 项以修复它。</span><span class="sxs-lookup"><span data-stu-id="6b910-309">Double-click the SEO warning entry to fix it.</span></span>

    <span data-ttu-id="6b910-310">![“错误列表”窗口](visual-studio-2013-web-tools/_static/image32.png "“错误列表”窗口")</span><span class="sxs-lookup"><span data-stu-id="6b910-310">![Error List window](visual-studio-2013-web-tools/_static/image32.png "Error List window")</span></span>

    <span data-ttu-id="6b910-311">*“错误列表”窗口*</span><span class="sxs-lookup"><span data-stu-id="6b910-311">*Error List window*</span></span>
3. <span data-ttu-id="6b910-312">在 " **Web Essentials** " 对话框中，单击 **"是"** 以 &lt;meta&gt; 标记插入描述。</span><span class="sxs-lookup"><span data-stu-id="6b910-312">In the **Web Essentials** dialog box, click **Yes** to insert a description &lt;meta&gt; tag.</span></span>

    <span data-ttu-id="6b910-313">!["Web Essentials" 对话框](visual-studio-2013-web-tools/_static/image33.png ""Web Essentials" 对话框")</span><span class="sxs-lookup"><span data-stu-id="6b910-313">![Web Essentials dialog box](visual-studio-2013-web-tools/_static/image33.png "Web Essentials dialog box")</span></span>

    <span data-ttu-id="6b910-314">*"Web Essentials" 对话框*</span><span class="sxs-lookup"><span data-stu-id="6b910-314">*Web Essentials dialog box*</span></span>
4. <span data-ttu-id="6b910-315">将打开 **\_布局**的编辑器，并将 **&lt;meta&gt;** 标记自动添加到 HTML 文件的**head**部分。</span><span class="sxs-lookup"><span data-stu-id="6b910-315">The editor for **\_Layout.cshtml** opens and the **&lt;meta&gt;** tag is automatically added to the **head** section of the HTML file.</span></span>

    <span data-ttu-id="6b910-316">![_Layout 页中自动添加的 Meta 标记](visual-studio-2013-web-tools/_static/image34.png "_Layout 页中自动添加的 Meta 标记")</span><span class="sxs-lookup"><span data-stu-id="6b910-316">![Meta tag automatically added in _Layout page](visual-studio-2013-web-tools/_static/image34.png "Meta tag automatically added in _Layout page")</span></span>

    <span data-ttu-id="6b910-317">*已自动添加到 \_布局页的元标记*</span><span class="sxs-lookup"><span data-stu-id="6b910-317">*Meta tag automatically added to \_Layout page*</span></span>
5. <span data-ttu-id="6b910-318">将**content**特性的值更改为*GeekQuiz* ，并保存该文件。</span><span class="sxs-lookup"><span data-stu-id="6b910-318">Change the value of the **content** attribute to *GeekQuiz* and save the file.</span></span>

<a id="Exercise2"></a>
### <a name="exercise-2-taking-advantage-of-code-snippets-and-intellisense"></a><span data-ttu-id="6b910-319">练习2：利用代码片段和 IntelliSense</span><span class="sxs-lookup"><span data-stu-id="6b910-319">Exercise 2: Taking Advantage of Code Snippets and IntelliSense</span></span>

<span data-ttu-id="6b910-320">在 Web Essentials 中，HTML 编辑器已通过额外功能进行了扩展。</span><span class="sxs-lookup"><span data-stu-id="6b910-320">With Web Essentials, the HTML editor has been extended with extra functionality.</span></span> <span data-ttu-id="6b910-321">在此练习中，你将看到一些新功能，这些功能在开发 web 应用程序时非常有用。</span><span class="sxs-lookup"><span data-stu-id="6b910-321">In this exercise, you will see some new features that are helpful when developing web applications.</span></span>

<a id="Ex2Task1"></a>
#### <a name="task-1---using-intellisense-in-html-documents"></a><span data-ttu-id="6b910-322">任务 1-在 HTML 文档中使用 IntelliSense</span><span class="sxs-lookup"><span data-stu-id="6b910-322">Task 1 - Using IntelliSense in HTML Documents</span></span>

<span data-ttu-id="6b910-323">你将在此任务中看到的第一个新功能称为**动态 IntelliSense**。</span><span class="sxs-lookup"><span data-stu-id="6b910-323">The first new feature you will see in this task is called **Dynamic IntelliSense**.</span></span> <span data-ttu-id="6b910-324">动态 IntelliSense 读取其他标记和特性，以推断你将使用的可能 id。</span><span class="sxs-lookup"><span data-stu-id="6b910-324">Dynamic IntelliSense reads other tags and attributes to infer the possible ids you will use.</span></span>

<span data-ttu-id="6b910-325">在此任务中，您将创建一个新的 HTML form 元素，该元素包含一个标签和一个输入字段。</span><span class="sxs-lookup"><span data-stu-id="6b910-325">In this task, you will create a new HTML form element which contains a label and an input field.</span></span> <span data-ttu-id="6b910-326">然后，您将向该标签添加一个**for**属性以将其绑定到输入，并且您将看到基于范围中输入的 Id 的 IntelliSense 建议。</span><span class="sxs-lookup"><span data-stu-id="6b910-326">Then you will add a **for** attribute to the label to bind it to the input, and you will see IntelliSense suggestions based on the ids of the inputs in scope.</span></span>

1. <span data-ttu-id="6b910-327">打开**Visual Studio Express 2013 For Web** ，并打开位于**TakingAdvantageofCodeSnippetsandIntelliSense/begin**文件夹**中的 buildingappswithcachingservice-ex2-getproducts latency-cs 解决方案。**</span><span class="sxs-lookup"><span data-stu-id="6b910-327">Open **Visual Studio Express 2013 for Web** and the **Begin.sln** solution located in the **Source/Ex2-TakingAdvantageofCodeSnippetsandIntelliSense/Begin** folder.</span></span> <span data-ttu-id="6b910-328">或者，你可以继续学习你在上一练习中获得的解决方案。</span><span class="sxs-lookup"><span data-stu-id="6b910-328">Alternatively, you can continue with the solution that you obtained in the previous exercise.</span></span>
2. <span data-ttu-id="6b910-329">在**解决方案资源管理器**中，打开位于 "**主**文件夹" | "**视图**" 中的 "**索引 ...** " 文件。</span><span class="sxs-lookup"><span data-stu-id="6b910-329">In **Solution Explorer**, open the **Index.cshtml** file located in the **Views** | **Home** folder.</span></span>
3. <span data-ttu-id="6b910-330">将以下窗体添加&gt;元素的 **&lt;节**中。</span><span class="sxs-lookup"><span data-stu-id="6b910-330">Add the following form inside the **&lt;section&gt;** element.</span></span>

    <span data-ttu-id="6b910-331">（代码段- *VisualStudio2013WebTooling* - *Buildingappswithcachingservice-ex2-getproducts latency-cs* - *窗体*）</span><span class="sxs-lookup"><span data-stu-id="6b910-331">(Code Snippet - *VisualStudio2013WebTooling* - *Ex2* - *Form*)</span></span>

    [!code-html[Main](visual-studio-2013-web-tools/samples/sample4.html)]
4. <span data-ttu-id="6b910-332">输入标记前面应带有字段说明的标签。</span><span class="sxs-lookup"><span data-stu-id="6b910-332">The input tag should be preceded by a label with some description of the field.</span></span> <span data-ttu-id="6b910-333">在输入标记前面添加以下标签。</span><span class="sxs-lookup"><span data-stu-id="6b910-333">Add the following label before the input tag.</span></span>

    [!code-html[Main](visual-studio-2013-web-tools/samples/sample5.html)]
5. <span data-ttu-id="6b910-334">**&lt;标签&gt;** 的属性指定标签绑定**到的窗**体元素。</span><span class="sxs-lookup"><span data-stu-id="6b910-334">The **for** attribute of a **&lt;label&gt;** specifies which form element a label is bound to.</span></span> <span data-ttu-id="6b910-335">特性的值应等于相关元素的 id。</span><span class="sxs-lookup"><span data-stu-id="6b910-335">The attribute's value should be equal to the id of the related element.</span></span> <span data-ttu-id="6b910-336">将**for**特性添加到 **&lt;标签&gt;** 元素。</span><span class="sxs-lookup"><span data-stu-id="6b910-336">Add the **for** attribute to the **&lt;label&gt;** element.</span></span> <span data-ttu-id="6b910-337">如下图中所示，&quot;名称&quot; 值基于同一范围内的元素的 id （括 **&lt;窗体&gt;** ）在 "IntelliSense" 框中弹出。</span><span class="sxs-lookup"><span data-stu-id="6b910-337">As shown in the following figure, the &quot;name&quot; value pops up in the IntelliSense box, based on the id of the elements within the same scope (the enclosing **&lt;form&gt;**).</span></span>

    <span data-ttu-id="6b910-338">![在 IntelliSense 中显示 id](visual-studio-2013-web-tools/_static/image35.png "在 IntelliSense 中显示 id")</span><span class="sxs-lookup"><span data-stu-id="6b910-338">![Showing the id in IntelliSense](visual-studio-2013-web-tools/_static/image35.png "Showing the id in IntelliSense")</span></span>

    <span data-ttu-id="6b910-339">*在 IntelliSense 中显示 id*</span><span class="sxs-lookup"><span data-stu-id="6b910-339">*Showing the id in IntelliSense*</span></span>
6. <span data-ttu-id="6b910-340">删除最近添加的 **&lt;表单&gt;** 元素及其内容。</span><span class="sxs-lookup"><span data-stu-id="6b910-340">Delete the recently added **&lt;form&gt;** element and its content.</span></span>

<a id="Ex2Task2"></a>
#### <a name="task-2---using-html-code-snippets"></a><span data-ttu-id="6b910-341">任务 2-使用 HTML 代码片段</span><span class="sxs-lookup"><span data-stu-id="6b910-341">Task 2 - Using HTML Code Snippets</span></span>

<span data-ttu-id="6b910-342">HTML5 引入了25个以上的新语义标记。</span><span class="sxs-lookup"><span data-stu-id="6b910-342">HTML5 introduced more than 25 new semantic tags.</span></span> <span data-ttu-id="6b910-343">Visual Studio 已经具有这些标记的 IntelliSense 支持，但通过添加新的代码段，Visual Studio 2013 可以更快、更轻松地编写标记。</span><span class="sxs-lookup"><span data-stu-id="6b910-343">Visual Studio already had IntelliSense support for these tags, but Visual Studio 2013 makes it faster and easier to write markup by adding new code snippets.</span></span> <span data-ttu-id="6b910-344">尽管这些标记并不复杂，但它们附带了几个小微妙之处，例如为*音频*标记添加正确的编解码器回退。</span><span class="sxs-lookup"><span data-stu-id="6b910-344">Though these tags are not complicated, they come with a few small subtleties, such as adding the correct codec fallbacks for the *audio* tag.</span></span> <span data-ttu-id="6b910-345">在此任务中，您将看到音频标记的 HTML 代码段。</span><span class="sxs-lookup"><span data-stu-id="6b910-345">In this task, you will see the HTML code snippets for the audio tag.</span></span>

1. <span data-ttu-id="6b910-346">在 "**索引 ...** " 文件中，在 "&lt;"**部分&gt;** 元素内键入 **&lt;aud** ，如下图所示。</span><span class="sxs-lookup"><span data-stu-id="6b910-346">In the **Index.cshtml** file, type **&lt;aud** inside the **&lt;section&gt;** element as shown in the following figure.</span></span>

    <span data-ttu-id="6b910-347">![插入音频元素](visual-studio-2013-web-tools/_static/image36.png "插入音频元素")</span><span class="sxs-lookup"><span data-stu-id="6b910-347">![Inserting an audio element](visual-studio-2013-web-tools/_static/image36.png "Inserting an audio element")</span></span>

    <span data-ttu-id="6b910-348">*插入音频元素*</span><span class="sxs-lookup"><span data-stu-id="6b910-348">*Inserting an audio element*</span></span>
2. <span data-ttu-id="6b910-349">按**tab**两次，并注意如何在页上添加以下代码，并将光标放在第一个源的**src**属性上。</span><span class="sxs-lookup"><span data-stu-id="6b910-349">Press **TAB** twice and notice how the following code is added on the page and the cursor is placed on the **src** attribute of the first source.</span></span>

    [!code-html[Main](visual-studio-2013-web-tools/samples/sample6.html)]

    > [!NOTE]
    > <span data-ttu-id="6b910-350">按**tab**键两次，将插入代码段。</span><span class="sxs-lookup"><span data-stu-id="6b910-350">By pressing the **TAB** key twice, the code snippet is inserted.</span></span> <span data-ttu-id="6b910-351">"音频" 代码片段显示*音频*标记的标准用法，其中包含两个源文件以改进支持。</span><span class="sxs-lookup"><span data-stu-id="6b910-351">The audio snippet shows the standard usage of the *audio* tag, with two source files for improved support.</span></span>
3. <span data-ttu-id="6b910-352">删除第二行并更新第一行的源，并将以下链接更新到 WebCampsTV Katana show： [http://media.ch9.ms/ch9/11d8/604b8163-fad3-4f12-9607-b404201211d8/KatanaProject.mp3](http://media.ch9.ms/ch9/11d8/604b8163-fad3-4f12-9607-b404201211d8/KatanaProject.mp3)。</span><span class="sxs-lookup"><span data-stu-id="6b910-352">Delete the second line and update the source of the first line with the following link to the WebCampsTV Katana show: [http://media.ch9.ms/ch9/11d8/604b8163-fad3-4f12-9607-b404201211d8/KatanaProject.mp3](http://media.ch9.ms/ch9/11d8/604b8163-fad3-4f12-9607-b404201211d8/KatanaProject.mp3).</span></span> <span data-ttu-id="6b910-353">生成的代码如下所示。</span><span class="sxs-lookup"><span data-stu-id="6b910-353">The resulting code is shown below.</span></span>

    [!code-html[Main](visual-studio-2013-web-tools/samples/sample7.html)]

    > [!NOTE]
    > <span data-ttu-id="6b910-354">使用源文件*KatanaProject*作为示例。</span><span class="sxs-lookup"><span data-stu-id="6b910-354">The source file *KatanaProject.mp3* is used as an example.</span></span> <span data-ttu-id="6b910-355">如果愿意，可以使用其他源。</span><span class="sxs-lookup"><span data-stu-id="6b910-355">You can use another source if you prefer.</span></span>
4. <span data-ttu-id="6b910-356">按**CTRL** + **S**以保存文件。</span><span class="sxs-lookup"><span data-stu-id="6b910-356">Press **CTRL** + **S** to save the file.</span></span>
5. <span data-ttu-id="6b910-357">按**CTRL** + **F5**启动应用程序。</span><span class="sxs-lookup"><span data-stu-id="6b910-357">Press **CTRL** + **F5** to start the application.</span></span>
6. <span data-ttu-id="6b910-358">请注意，音频播放器已添加到应用程序。</span><span class="sxs-lookup"><span data-stu-id="6b910-358">Notice that an audio player was added to the application.</span></span>

    <span data-ttu-id="6b910-359">![Internet Explorer 中的音频播放器](visual-studio-2013-web-tools/_static/image37.png "Internet Explorer 中的音频播放器")</span><span class="sxs-lookup"><span data-stu-id="6b910-359">![Audio player in Internet Explorer](visual-studio-2013-web-tools/_static/image37.png "Audio player in Internet Explorer")</span></span>

    <span data-ttu-id="6b910-360">*Internet Explorer 中的音频播放器*</span><span class="sxs-lookup"><span data-stu-id="6b910-360">*Audio player in Internet Explorer*</span></span>

    <span data-ttu-id="6b910-361">![Google Chrome 中的音频播放器](visual-studio-2013-web-tools/_static/image38.png "Google Chrome 中的音频播放器")</span><span class="sxs-lookup"><span data-stu-id="6b910-361">![Audio player in Google Chrome](visual-studio-2013-web-tools/_static/image38.png "Audio player in Google Chrome")</span></span>

    <span data-ttu-id="6b910-362">*Google Chrome 中的音频播放器*</span><span class="sxs-lookup"><span data-stu-id="6b910-362">*Audio player in Google Chrome*</span></span>
7. <span data-ttu-id="6b910-363">不要关闭浏览器。</span><span class="sxs-lookup"><span data-stu-id="6b910-363">Do not close the browsers.</span></span> <span data-ttu-id="6b910-364">你将在下一任务中使用它们。</span><span class="sxs-lookup"><span data-stu-id="6b910-364">You will use them in the next task.</span></span>

<a id="Ex2Task3"></a>
#### <a name="task-3---using-intellisense-in-javascript-documents"></a><span data-ttu-id="6b910-365">任务 3-使用 JavaScript 文档中的 IntelliSense</span><span class="sxs-lookup"><span data-stu-id="6b910-365">Task 3 - Using IntelliSense in JavaScript Documents</span></span>

<span data-ttu-id="6b910-366">使用 Web Essentials 2013，样式表和 HTML 页面生成 Id 和类名称的列表。</span><span class="sxs-lookup"><span data-stu-id="6b910-366">With Web Essentials 2013, style sheets and HTML pages produce a list of IDs and class names.</span></span> <span data-ttu-id="6b910-367">在此任务中，你将了解这些列表如何改进 Web Essentials 2013 中的 JavaScript IntelliSense 支持。</span><span class="sxs-lookup"><span data-stu-id="6b910-367">In this task, you will learn how those lists improve JavaScript IntelliSense support in Web Essentials 2013.</span></span>

1. <span data-ttu-id="6b910-368">在**索引 cshtml**文件中，添加以下代码以定义 JavaScript 代码的**脚本**标记。</span><span class="sxs-lookup"><span data-stu-id="6b910-368">In the **Index.cshtml** file, add the following code to define a **script** tag for JavaScript code.</span></span>

    [!code-cshtml[Main](visual-studio-2013-web-tools/samples/sample8.cshtml)]
2. <span data-ttu-id="6b910-369">在**script**标记中添加以下代码，以定义就绪回调函数。</span><span class="sxs-lookup"><span data-stu-id="6b910-369">Add the following code inside the **script** tag to define the ready callback function.</span></span>

    <span data-ttu-id="6b910-370">（代码段- *VisualStudio2013WebTooling* - *buildingappswithcachingservice-ex2-getproducts latency-cs* - *ReadyFunction*）</span><span class="sxs-lookup"><span data-stu-id="6b910-370">(Code Snippet - *VisualStudio2013WebTooling* - *Ex2* - *ReadyFunction*)</span></span>

    [!code-javascript[Main](visual-studio-2013-web-tools/samples/sample9.js)]
3. <span data-ttu-id="6b910-371">将插入符号置于**script**标记中，然后按**CTRL** +  **。**</span><span class="sxs-lookup"><span data-stu-id="6b910-371">Place the caret in the **script** tag and press **CTRL** + **.**</span></span> <span data-ttu-id="6b910-372">打开 "建议" 菜单。</span><span class="sxs-lookup"><span data-stu-id="6b910-372">to open the suggestion menu.</span></span>
4. <span data-ttu-id="6b910-373">单击 "**提取到文件**"。</span><span class="sxs-lookup"><span data-stu-id="6b910-373">Click **Extract To File**.</span></span>

    <span data-ttu-id="6b910-374">![JavaScript 提取到文件建议](visual-studio-2013-web-tools/_static/image39.png "JavaScript 提取到文件建议")</span><span class="sxs-lookup"><span data-stu-id="6b910-374">![JavaScript extract to file suggestion](visual-studio-2013-web-tools/_static/image39.png "JavaScript extract to file suggestion")</span></span>

    <span data-ttu-id="6b910-375">*JavaScript 提取到文件建议*</span><span class="sxs-lookup"><span data-stu-id="6b910-375">*JavaScript extract to file suggestion*</span></span>
5. <span data-ttu-id="6b910-376">在 "**另存为**" 窗口中，选择 "**脚本**" 文件夹，将文件命名为**Init** ，然后单击 "**保存**"。</span><span class="sxs-lookup"><span data-stu-id="6b910-376">In the **Save As** window, select the **Scripts** folder, name the file **init.js** and click **Save**.</span></span>

    <span data-ttu-id="6b910-377">![另存为窗口](visual-studio-2013-web-tools/_static/image40.png "另存为窗口")</span><span class="sxs-lookup"><span data-stu-id="6b910-377">![Save As window](visual-studio-2013-web-tools/_static/image40.png "Save As window")</span></span>

    <span data-ttu-id="6b910-378">*另存为窗口*</span><span class="sxs-lookup"><span data-stu-id="6b910-378">*Save As window*</span></span>

    > [!NOTE]
    > <span data-ttu-id="6b910-379">将创建**init**文件，并将脚本的内容移动到该文件。</span><span class="sxs-lookup"><span data-stu-id="6b910-379">The **init.js** file is created and the content of the script is moved to the file.</span></span>
    > 
    > <span data-ttu-id="6b910-380">![用包含的内容创建的 Init node.js 文件](visual-studio-2013-web-tools/_static/image41.png "用包含的内容创建的 Init node.js 文件")</span><span class="sxs-lookup"><span data-stu-id="6b910-380">![Init.js file created with the content included](visual-studio-2013-web-tools/_static/image41.png "Init.js file created with the content included")</span></span>
    > 
    > <span data-ttu-id="6b910-381">*用包含的内容创建的 Init node.js 文件*</span><span class="sxs-lookup"><span data-stu-id="6b910-381">*Init.js file created with the content included*</span></span>
6. <span data-ttu-id="6b910-382">打开**索引. cshtml**文件，并检查是否已将脚本标记替换为对**init .js**文件的引用。</span><span class="sxs-lookup"><span data-stu-id="6b910-382">Open the **Index.cshtml** file and check that the script tag was replaced with a reference to the **init.js** file.</span></span>

    <span data-ttu-id="6b910-383">![Init .js html 参考](visual-studio-2013-web-tools/_static/image42.png "Init .js html 参考")</span><span class="sxs-lookup"><span data-stu-id="6b910-383">![Init.js html reference](visual-studio-2013-web-tools/_static/image42.png "Init.js html reference")</span></span>

    <span data-ttu-id="6b910-384">*Init .js html 参考*</span><span class="sxs-lookup"><span data-stu-id="6b910-384">*Init.js html reference*</span></span>
7. <span data-ttu-id="6b910-385">请参阅**解决方案资源管理器**，并注意**init node.js**文件已自动包含在解决方案中。</span><span class="sxs-lookup"><span data-stu-id="6b910-385">Go to the **Solution Explorer** and notice that the **init.js** file was included automatically in the solution.</span></span>

    <span data-ttu-id="6b910-386">![解决方案中包含的 Init .js 文件](visual-studio-2013-web-tools/_static/image43.png "解决方案中包含的 Init .js 文件")</span><span class="sxs-lookup"><span data-stu-id="6b910-386">![Init.js file included in solution](visual-studio-2013-web-tools/_static/image43.png "Init.js file included in solution")</span></span>

    <span data-ttu-id="6b910-387">*解决方案中包含的 Init .js 文件*</span><span class="sxs-lookup"><span data-stu-id="6b910-387">*Init.js file included in solution*</span></span>
8. <span data-ttu-id="6b910-388">切换回**init .js**文件以更新**ready**函数回调。</span><span class="sxs-lookup"><span data-stu-id="6b910-388">Switch back to the **init.js** file to update the **ready** function callback.</span></span>
9. <span data-ttu-id="6b910-389">在传递到*ready*的函数回调定义中，添加以下代码以按特定类特性获取所有元素。</span><span class="sxs-lookup"><span data-stu-id="6b910-389">Inside the function callback definition that is passed to *ready*, add the following code to get all the elements by a specific class attribute.</span></span>

    [!code-javascript[Main](visual-studio-2013-web-tools/samples/sample10.js)]
10. <span data-ttu-id="6b910-390">按**CTRL** + **getElementsByClassName**函数调用内引号之间的**空格**。</span><span class="sxs-lookup"><span data-stu-id="6b910-390">Press **CTRL** + **Space** between the quotes inside the **getElementsByClassName** function call.</span></span>

    <span data-ttu-id="6b910-391">![显示 getElementsByClassName 函数的 IntelliSense](visual-studio-2013-web-tools/_static/image44.png "显示 getElementsByClassName 函数的 IntelliSense")</span><span class="sxs-lookup"><span data-stu-id="6b910-391">![Showing IntelliSense for the getElementsByClassName function](visual-studio-2013-web-tools/_static/image44.png "Showing IntelliSense for the getElementsByClassName function")</span></span>

    <span data-ttu-id="6b910-392">*显示 getElementsByClassName 函数的 IntelliSense*</span><span class="sxs-lookup"><span data-stu-id="6b910-392">*Showing IntelliSense for the getElementsByClassName function*</span></span>

    > [!NOTE]
    > <span data-ttu-id="6b910-393">请注意，IntelliSense 显示了项目样式表中定义的类。</span><span class="sxs-lookup"><span data-stu-id="6b910-393">Notice that IntelliSense shows the classes defined in the project style sheets.</span></span>
11. <span data-ttu-id="6b910-394">将创建的行替换为下面的代码。</span><span class="sxs-lookup"><span data-stu-id="6b910-394">Replace the line that you have created with the following code.</span></span>

    [!code-javascript[Main](visual-studio-2013-web-tools/samples/sample11.js)]
12. <span data-ttu-id="6b910-395">将光标放在**getElementsByTagName**函数中的**引号内，** 并按**CTRL** + **Space**"。</span><span class="sxs-lookup"><span data-stu-id="6b910-395">Position the cursor after **au** inside the quotes in the **getElementsByTagName** function and press **CTRL** + **Space**.</span></span>

    <span data-ttu-id="6b910-396">![显示 getElementByTagName 方法的 IntelliSense](visual-studio-2013-web-tools/_static/image45.png "显示 getElementByTagName 方法的 IntelliSense")</span><span class="sxs-lookup"><span data-stu-id="6b910-396">![Showing IntelliSense for the getElementByTagName method](visual-studio-2013-web-tools/_static/image45.png "Showing IntelliSense for the getElementByTagName method")</span></span>

    <span data-ttu-id="6b910-397">*显示 getElementsByTagName 方法的 IntelliSense*</span><span class="sxs-lookup"><span data-stu-id="6b910-397">*Showing IntelliSense for the getElementsByTagName method*</span></span>
13. <span data-ttu-id="6b910-398">从列表中选择 **&quot;音频&quot;** ，然后按**enter**。</span><span class="sxs-lookup"><span data-stu-id="6b910-398">Select **&quot;audio&quot;** from the list and press **ENTER**.</span></span> <span data-ttu-id="6b910-399">结果如下图所示。</span><span class="sxs-lookup"><span data-stu-id="6b910-399">The result is shown in the following figure.</span></span>

    <span data-ttu-id="6b910-400">![检索音频元素](visual-studio-2013-web-tools/_static/image46.png "检索音频元素")</span><span class="sxs-lookup"><span data-stu-id="6b910-400">![Retrieving Audio Elements](visual-studio-2013-web-tools/_static/image46.png "Retrieving Audio Elements")</span></span>

    <span data-ttu-id="6b910-401">*检索音频元素*</span><span class="sxs-lookup"><span data-stu-id="6b910-401">*Retrieving Audio Elements*</span></span>
14. <span data-ttu-id="6b910-402">在**解决方案资源管理器**中，右键单击**Scripts**文件夹中的缩小文件，然后从**Web Essentials**菜单中**选择 "** **JavaScript 文件**"。</span><span class="sxs-lookup"><span data-stu-id="6b910-402">In **Solution Explorer**, right-click the **init.js** file in the **Scripts** folder and select **Minify JavaScript file(s)** from the **Web Essentials** menu.</span></span>

    <span data-ttu-id="6b910-403">![缩小 JavaScript 文件](visual-studio-2013-web-tools/_static/image47.png "缩小 JavaScript 文件")</span><span class="sxs-lookup"><span data-stu-id="6b910-403">![Minify JavaScript file(s)](visual-studio-2013-web-tools/_static/image47.png "Minify JavaScript files")</span></span>

    <span data-ttu-id="6b910-404">*缩小 JavaScript 文件*</span><span class="sxs-lookup"><span data-stu-id="6b910-404">*Minify JavaScript file(s)*</span></span>
15. <span data-ttu-id="6b910-405">当系统提示在源文件更改时启用自动缩减时，请单击 **"是"** 。</span><span class="sxs-lookup"><span data-stu-id="6b910-405">When prompted to enable automatic minification when the source file changes click **Yes**.</span></span>

    <span data-ttu-id="6b910-406">![启用自动缩减警告](visual-studio-2013-web-tools/_static/image48.png "启用自动缩减警告")</span><span class="sxs-lookup"><span data-stu-id="6b910-406">![Enabling automatic minification warning](visual-studio-2013-web-tools/_static/image48.png "Enabling automatic minification warning")</span></span>

    <span data-ttu-id="6b910-407">*启用自动缩减警告*</span><span class="sxs-lookup"><span data-stu-id="6b910-407">*Enabling automatic minification warning*</span></span>

    > [!NOTE]
    > <span data-ttu-id="6b910-408">将创建**init. node.js** ，并将其添加为**init .js**文件的依赖项。</span><span class="sxs-lookup"><span data-stu-id="6b910-408">The **init.min.js** is created and is added as a dependency of the **init.js** file.</span></span>
    > 
    > <span data-ttu-id="6b910-409">![已创建最小的 .js 文件](visual-studio-2013-web-tools/_static/image49.png "已创建最小的 .js 文件")</span><span class="sxs-lookup"><span data-stu-id="6b910-409">![Init.min.js file created](visual-studio-2013-web-tools/_static/image49.png "Init.min.js file created")</span></span>
    > 
    > <span data-ttu-id="6b910-410">*已创建最小的 .js 文件*</span><span class="sxs-lookup"><span data-stu-id="6b910-410">*Init.min.js file created*</span></span>
16. <span data-ttu-id="6b910-411">打开**init. .js**文件，并注意该文件为缩小。</span><span class="sxs-lookup"><span data-stu-id="6b910-411">Open the **init.min.js** file and notice that the file is minified.</span></span>

    <span data-ttu-id="6b910-412">![Init. .js 文件内容](visual-studio-2013-web-tools/_static/image50.png "Init. .js 文件内容")</span><span class="sxs-lookup"><span data-stu-id="6b910-412">![Init.min.js file content](visual-studio-2013-web-tools/_static/image50.png "Init.min.js file content")</span></span>

    <span data-ttu-id="6b910-413">*Init. .js 文件内容*</span><span class="sxs-lookup"><span data-stu-id="6b910-413">*Init.min.js file content*</span></span>
17. <span data-ttu-id="6b910-414">在**init .js**文件中，将以下代码添加到**getElementsByTagName**函数调用下以播放所有音频元素。</span><span class="sxs-lookup"><span data-stu-id="6b910-414">In the **init.js** file, add the following code below the **getElementsByTagName** function call to play all the audio elements.</span></span>

    <span data-ttu-id="6b910-415">（代码段- *VisualStudio2013WebTooling* - *buildingappswithcachingservice-ex2-getproducts latency-cs* - *PlayAudioElements*）</span><span class="sxs-lookup"><span data-stu-id="6b910-415">(Code Snippet - *VisualStudio2013WebTooling* - *Ex2* - *PlayAudioElements*)</span></span>

    [!code-csharp[Main](visual-studio-2013-web-tools/samples/sample12.cs)]
18. <span data-ttu-id="6b910-416">单击 " **CTRL** + **S**以保存文件。</span><span class="sxs-lookup"><span data-stu-id="6b910-416">Click **CTRL** + **S** to save the file.</span></span> <span data-ttu-id="6b910-417">由于已打开缩小文件，因此你将看到一个对话框，指出该文件已在源编辑器之外进行了修改。</span><span class="sxs-lookup"><span data-stu-id="6b910-417">Since the minified file is already opened, you will see a dialog box saying that the file was modified outside of the source editor.</span></span> <span data-ttu-id="6b910-418">单击 **“是”** 。</span><span class="sxs-lookup"><span data-stu-id="6b910-418">Click **Yes**.</span></span>

    <span data-ttu-id="6b910-419">![Microsoft Visual Studio 警告](visual-studio-2013-web-tools/_static/image51.png "Microsoft Visual Studio 警告")</span><span class="sxs-lookup"><span data-stu-id="6b910-419">![Microsoft Visual Studio warning](visual-studio-2013-web-tools/_static/image51.png "Microsoft Visual Studio warning")</span></span>

    <span data-ttu-id="6b910-420">*Microsoft Visual Studio 警告*</span><span class="sxs-lookup"><span data-stu-id="6b910-420">*Microsoft Visual Studio warning*</span></span>
19. <span data-ttu-id="6b910-421">切换回**init .** 文件，以验证该文件是否已用新代码进行更新。</span><span class="sxs-lookup"><span data-stu-id="6b910-421">Switch back to the **init.min.js** file to verify that the file was updated with the new code.</span></span>

    <span data-ttu-id="6b910-422">![已更新初始. js 文件](visual-studio-2013-web-tools/_static/image52.png "已更新初始. js 文件")</span><span class="sxs-lookup"><span data-stu-id="6b910-422">![Init.min.js file updated](visual-studio-2013-web-tools/_static/image52.png "Init.min.js file updated")</span></span>

    <span data-ttu-id="6b910-423">*已更新初始. js 文件*</span><span class="sxs-lookup"><span data-stu-id="6b910-423">*Init.min.js file updated*</span></span>
20. <span data-ttu-id="6b910-424">单击**浏览器链接刷新**按钮。</span><span class="sxs-lookup"><span data-stu-id="6b910-424">Click the **Browser Link Refresh** button.</span></span>
21. <span data-ttu-id="6b910-425">两个浏览器刷新后，你在上一任务中看到的音频播放机将自动开始播放。</span><span class="sxs-lookup"><span data-stu-id="6b910-425">Once both browsers are refreshed the audio players you saw in the previous task will start playing automatically.</span></span>

    <span data-ttu-id="6b910-426">![音频播放器包含在视图中](visual-studio-2013-web-tools/_static/image53.png "音频播放器包含在视图中")</span><span class="sxs-lookup"><span data-stu-id="6b910-426">![Audio player included in view](visual-studio-2013-web-tools/_static/image53.png "Audio player included in view")</span></span>

    <span data-ttu-id="6b910-427">*音频播放器包含在视图中*</span><span class="sxs-lookup"><span data-stu-id="6b910-427">*Audio player included in view*</span></span>

---

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="6b910-428">摘要</span><span class="sxs-lookup"><span data-stu-id="6b910-428">Summary</span></span>

<span data-ttu-id="6b910-429">通过完成本动手实验，你学习了如何：</span><span class="sxs-lookup"><span data-stu-id="6b910-429">By completing this hands-on lab you have learned how to:</span></span>

- <span data-ttu-id="6b910-430">使用 Web Essentials 中包含的新 HTML 编辑器功能，如丰富的 HTML5 代码段和 Zen 编码</span><span class="sxs-lookup"><span data-stu-id="6b910-430">Use new HTML editor features included in Web Essentials such as rich HTML5 code snippets and Zen coding</span></span>
- <span data-ttu-id="6b910-431">使用 Web Essentials 中包含的新 CSS 编辑器功能，如颜色选取器和浏览器矩阵工具提示</span><span class="sxs-lookup"><span data-stu-id="6b910-431">Use new CSS editor features included in Web Essentials such as the Color picker and Browser matrix tooltip</span></span>
- <span data-ttu-id="6b910-432">使用 Web Essentials 中包含的新 JavaScript 编辑器功能，如 "提取到文件" 和 "适用于所有 HTML 元素的 IntelliSense"</span><span class="sxs-lookup"><span data-stu-id="6b910-432">Use new JavaScript editor features included in Web Essentials such as Extract to File and IntelliSense for all HTML elements</span></span>
- <span data-ttu-id="6b910-433">使用浏览器链接在浏览器和 Visual Studio 之间交换数据</span><span class="sxs-lookup"><span data-stu-id="6b910-433">Exchange data between your browser and Visual Studio using Browser Link</span></span>

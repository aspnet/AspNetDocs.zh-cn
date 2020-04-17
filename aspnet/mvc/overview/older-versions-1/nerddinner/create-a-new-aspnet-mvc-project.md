---
uid: mvc/overview/older-versions-1/nerddinner/create-a-new-aspnet-mvc-project
title: 创建新ASP.NET MVC 项目 |微软文档
author: rick-anderson
description: 步骤 1 演示如何将基本的 NerdDinner 应用程序结构放在原位。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 7e0e9928-8fdc-4b74-9882-55fac0976628
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/create-a-new-aspnet-mvc-project
msc.type: authoredcontent
ms.openlocfilehash: 240c8a04cec3c07f434182775d1c519aab029761
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541476"
---
# <a name="create-a-new-aspnet-mvc-project"></a><span data-ttu-id="13de7-103">新建 ASP.NET MVC 项目</span><span class="sxs-lookup"><span data-stu-id="13de7-103">Create a New ASP.NET MVC Project</span></span>

<span data-ttu-id="13de7-104">由[微软](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="13de7-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="13de7-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="13de7-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="13de7-106">这是一个免费的["NerdDinner"应用程序教程](introducing-the-nerddinner-tutorial.md)的第 1 步，该教程演示如何使用 ASP.NET MVC 1 构建小型但完整的 Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="13de7-106">This is step 1 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="13de7-107">步骤 1 演示如何将基本的 NerdDinner 应用程序结构放在原位。</span><span class="sxs-lookup"><span data-stu-id="13de7-107">Step 1 shows you how to put the basic NerdDinner application structure in place.</span></span>
> 
> <span data-ttu-id="13de7-108">如果您使用的是ASP.NET MVC 3，我们建议您按照[MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC 音乐商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程进行操作。</span><span class="sxs-lookup"><span data-stu-id="13de7-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-1-file-gtnew-project"></a><span data-ttu-id="13de7-109">神经晚餐步骤 1： 文件&gt;- 新项目</span><span class="sxs-lookup"><span data-stu-id="13de7-109">NerdDinner Step 1: File-&gt;New Project</span></span>

<span data-ttu-id="13de7-110">我们将通过在 Visual Studio 2008 或免费的可视化 Web 开发人员 2008 Express 中选择 **"文件-&gt;新项目**"菜单项来开始我们的 NerdDinner 应用程序。</span><span class="sxs-lookup"><span data-stu-id="13de7-110">We'll begin our NerdDinner application by selecting the **File-&gt;New Project** menu item within either Visual Studio 2008 or the free Visual Web Developer 2008 Express.</span></span>

<span data-ttu-id="13de7-111">这将弹出"新项目"对话框。</span><span class="sxs-lookup"><span data-stu-id="13de7-111">This will bring up the "New Project" dialog.</span></span> <span data-ttu-id="13de7-112">要创建新ASP.NET MVC 应用程序，我们将选择对话框左侧的"Web"节点，然后在右侧选择"ASP.NET MVC Web 应用程序"项目模板：</span><span class="sxs-lookup"><span data-stu-id="13de7-112">To create a new ASP.NET MVC application, we'll select the "Web" node on the left-hand side of the dialog and then choose the "ASP.NET MVC Web Application" project template on the right:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image1.png)

<span data-ttu-id="13de7-113">*重要提示：请确保已下载并安装 ASP.NET MVC - 否则它不会显示在"新项目"对话框中。如果您尚未安装[Microsoft Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)的 V2（ASP.NET MVC 在"Web 平台-&gt;框架和运行时"部分中可用）。*</span><span class="sxs-lookup"><span data-stu-id="13de7-113">*Important: Make sure you've downloaded and installed ASP.NET MVC - otherwise it won't show up in the New Project dialog. You can use V2 of the [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx) if you haven't installed it yet (ASP.NET MVC is available within the "Web Platform-&gt;Frameworks and Runtimes" section).*</span></span>

<span data-ttu-id="13de7-114">我们将命名要创建"NerdDinner"的新项目，然后单击"确定"按钮创建它。</span><span class="sxs-lookup"><span data-stu-id="13de7-114">We'll name the new project we are going to create "NerdDinner" and then click the "ok" button to create it.</span></span>

<span data-ttu-id="13de7-115">当我们单击"OK"Visual Studio 时，将弹出一个附加对话框，提示我们为新应用程序选择创建单元测试项目。</span><span class="sxs-lookup"><span data-stu-id="13de7-115">When we click "ok" Visual Studio will bring up an additional dialog that prompts us to optionally create a unit test project for the new application as well.</span></span> <span data-ttu-id="13de7-116">此单元测试项目使我们能够创建自动测试，以验证应用程序的功能和行为（本教程稍后将介绍如何操作）。</span><span class="sxs-lookup"><span data-stu-id="13de7-116">This unit test project enables us to create automated tests that verify the functionality and behavior of our application (something we'll cover how to-do later in this tutorial).</span></span>

![](create-a-new-aspnet-mvc-project/_static/image2.png)

<span data-ttu-id="13de7-117">上面对话框中的"测试框架"下拉列表填充了所有可用的ASP.NET MVC 单元测试项目模板安装在计算机上。</span><span class="sxs-lookup"><span data-stu-id="13de7-117">The "Test framework" dropdown in the above dialog is populated with all available ASP.NET MVC unit test project templates installed on the machine.</span></span> <span data-ttu-id="13de7-118">可以为 NUnit、MBUnit 和 XUnit 下载版本。</span><span class="sxs-lookup"><span data-stu-id="13de7-118">Versions can be downloaded for NUnit, MBUnit, and XUnit.</span></span> <span data-ttu-id="13de7-119">还支持内置的可视化工作室单元测试框架。</span><span class="sxs-lookup"><span data-stu-id="13de7-119">The built-in Visual Studio Unit Test framework is also supported.</span></span>

<span data-ttu-id="13de7-120">*注意：可视化工作室单元测试框架仅适用于 Visual Studio 2008 专业版和更高版本。如果您使用的是 VS 2008 标准版或可视化 Web 开发人员 2008 Express，则需要下载并安装 nUnit、MBUnit 或 XUnit 扩展，以便ASP.NET MVC 才能显示此对话框。如果没有安装任何测试框架，将不会显示该对话框。*</span><span class="sxs-lookup"><span data-stu-id="13de7-120">*Note: The Visual Studio Unit Test Framework is only available with Visual Studio 2008 Professional and higher versions. If you are using VS 2008 Standard Edition or Visual Web Developer 2008 Express you will need to download and install the NUnit, MBUnit or XUnit extensions for ASP.NET MVC in order for this dialog to be shown. The dialog will not display if there aren't any test frameworks installed.*</span></span>

<span data-ttu-id="13de7-121">我们将为我们创建的测试项目使用默认的"NerdDinner.Test"名称，并使用"可视化工作室单元测试"框架选项。</span><span class="sxs-lookup"><span data-stu-id="13de7-121">We'll use the default "NerdDinner.Tests" name for the test project we create, and use the "Visual Studio Unit Test" framework option.</span></span> <span data-ttu-id="13de7-122">当我们点击"ok"按钮 Visual Studio 将为我们创建一个解决方案，其中包含两个项目 - 一个用于我们的 Web 应用程序，一个用于我们的单元测试：</span><span class="sxs-lookup"><span data-stu-id="13de7-122">When we click the "ok" button Visual Studio will create a solution for us with two projects in it - one for our web application and one for our unit tests:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image3.png)

### <a name="examining-the-nerddinner-directory-structure"></a><span data-ttu-id="13de7-123">检查 NerdDinner 目录结构</span><span class="sxs-lookup"><span data-stu-id="13de7-123">Examining the NerdDinner directory structure</span></span>

<span data-ttu-id="13de7-124">当您使用 Visual Studio 创建新ASP.NET MVC 应用程序时，它会自动向项目添加许多文件和目录：</span><span class="sxs-lookup"><span data-stu-id="13de7-124">When you create a new ASP.NET MVC application with Visual Studio, it automatically adds a number of files and directories to the project:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image4.png)

<span data-ttu-id="13de7-125">默认情况下ASP.NET MVC 项目有六个顶级目录：</span><span class="sxs-lookup"><span data-stu-id="13de7-125">ASP.NET MVC projects by default have six top-level directories:</span></span>

| <span data-ttu-id="13de7-126">**目录**</span><span class="sxs-lookup"><span data-stu-id="13de7-126">**Directory**</span></span> | <span data-ttu-id="13de7-127">**目标**</span><span class="sxs-lookup"><span data-stu-id="13de7-127">**Purpose**</span></span> |
| --- | --- |
| <span data-ttu-id="13de7-128">**/控制器**</span><span class="sxs-lookup"><span data-stu-id="13de7-128">**/Controllers**</span></span> | <span data-ttu-id="13de7-129">放置处理 URL 请求的控制器类的位置</span><span class="sxs-lookup"><span data-stu-id="13de7-129">Where you put Controller classes that handle URL requests</span></span> |
| <span data-ttu-id="13de7-130">**/型号**</span><span class="sxs-lookup"><span data-stu-id="13de7-130">**/Models**</span></span> | <span data-ttu-id="13de7-131">放置表示和操作数据的类的位置</span><span class="sxs-lookup"><span data-stu-id="13de7-131">Where you put classes that represent and manipulate data</span></span> |
| <span data-ttu-id="13de7-132">**/视图**</span><span class="sxs-lookup"><span data-stu-id="13de7-132">**/Views**</span></span> | <span data-ttu-id="13de7-133">放置负责呈现输出的 UI 模板文件的位置</span><span class="sxs-lookup"><span data-stu-id="13de7-133">Where you put UI template files that are responsible for rendering output</span></span> |
| <span data-ttu-id="13de7-134">**/脚本**</span><span class="sxs-lookup"><span data-stu-id="13de7-134">**/Scripts**</span></span> | <span data-ttu-id="13de7-135">放置 JavaScript 库文件和脚本的位置 （.js）</span><span class="sxs-lookup"><span data-stu-id="13de7-135">Where you put JavaScript library files and scripts (.js)</span></span> |
| <span data-ttu-id="13de7-136">**/内容**</span><span class="sxs-lookup"><span data-stu-id="13de7-136">**/Content**</span></span> | <span data-ttu-id="13de7-137">放置 CSS 和图像文件以及其他非动态/非 JavaScript 内容的位置</span><span class="sxs-lookup"><span data-stu-id="13de7-137">Where you put CSS and image files, and other non-dynamic/non-JavaScript content</span></span> |
| <span data-ttu-id="13de7-138">**/应用程序\_数据**</span><span class="sxs-lookup"><span data-stu-id="13de7-138">**/App\_Data**</span></span> | <span data-ttu-id="13de7-139">存储要读取/写入的数据文件的位置。</span><span class="sxs-lookup"><span data-stu-id="13de7-139">Where you store data files you want to read/write.</span></span> |

<span data-ttu-id="13de7-140">ASP.NET MVC 不需要此结构。</span><span class="sxs-lookup"><span data-stu-id="13de7-140">ASP.NET MVC does not require this structure.</span></span> <span data-ttu-id="13de7-141">事实上，处理大型应用程序的开发人员通常会跨多个项目对应用程序进行分区，使其更易于管理（例如：数据模型类通常位于与 Web 应用程序不同的类库项目中）。</span><span class="sxs-lookup"><span data-stu-id="13de7-141">In fact, developers working on large applications will typically partition the application up across multiple projects to make it more manageable (for example: data model classes often go in a separate class library project from the web application).</span></span> <span data-ttu-id="13de7-142">但是，默认项目结构确实提供了一个不错的默认目录约定，我们可以用它来保持应用程序问题清洁。</span><span class="sxs-lookup"><span data-stu-id="13de7-142">The default project structure, however, does provide a nice default directory convention that we can use to keep our application concerns clean.</span></span>

<span data-ttu-id="13de7-143">当我们展开 /控制器目录时，我们会发现 Visual Studio 默认为项目添加了两个控制器类 - 主控制器和帐户控制器：</span><span class="sxs-lookup"><span data-stu-id="13de7-143">When we expand the /Controllers directory we'll find that Visual Studio added two controller classes – HomeController and AccountController – by default to the project:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image5.png)

<span data-ttu-id="13de7-144">当我们展开 /Views 目录时，我们会发现三个子目录 - /Home，//帐户和 /共享 - 以及其中的几个模板文件也添加到项目中，默认情况下：</span><span class="sxs-lookup"><span data-stu-id="13de7-144">When we expand the /Views directory, we'll find three sub-directories – /Home, /Account and /Shared – as well as several template files within them were also added to the project by default:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image6.png)

<span data-ttu-id="13de7-145">当我们展开 /内容和 /脚本目录时，我们将找到一个 Site.css 文件，该文件用于设置网站上所有 HTML 的样式，以及可在应用程序中启用ASP.NET AJAX 和 jQuery 支持的 JavaScript 库：</span><span class="sxs-lookup"><span data-stu-id="13de7-145">When we expand the /Content and /Scripts directories, we'll find a Site.css file that is used to style all HTML on the site, as well as JavaScript libraries that can enable ASP.NET AJAX and jQuery support within the application:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image7.png)

<span data-ttu-id="13de7-146">当我们扩展 NerdDinner.测试项目时，我们将找到两个类，其中包含控制器类的单元测试：</span><span class="sxs-lookup"><span data-stu-id="13de7-146">When we expand the NerdDinner.Tests project we'll find two classes that contain unit tests for our controller classes:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image8.png)

<span data-ttu-id="13de7-147">Visual Studio 添加的这些默认文件为我们提供了工作应用程序的基本结构 - 完整的主页，关于页面，帐户登录/注销/注册页，和未处理的错误页面（所有有线和开箱即用）。</span><span class="sxs-lookup"><span data-stu-id="13de7-147">These default files added by Visual Studio provide us with a basic structure for a working application - complete with home page, about page, account login/logout/registration pages, and an unhandled error page (all wired-up and working out of the box).</span></span>

### <a name="running-the-nerddinner-application"></a><span data-ttu-id="13de7-148">运行内德晚餐应用程序</span><span class="sxs-lookup"><span data-stu-id="13de7-148">Running the NerdDinner Application</span></span>

<span data-ttu-id="13de7-149">我们可以通过选择**调试-&gt;启动调试**或**调试 -&gt;不调试菜单项来**运行项目：</span><span class="sxs-lookup"><span data-stu-id="13de7-149">We can run the project by choosing either the **Debug-&gt;Start Debugging** or **Debug-&gt;Start Without Debugging** menu items:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image9.png)

<span data-ttu-id="13de7-150">这将启动 Visual Studio 附带的内置ASP.NET Web 服务器，并运行我们的应用程序：</span><span class="sxs-lookup"><span data-stu-id="13de7-150">This will launch the built-in ASP.NET Web-server that comes with Visual Studio, and run our application:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image10.png)

<span data-ttu-id="13de7-151">以下是我们新项目的主页（URL："/"）运行时：</span><span class="sxs-lookup"><span data-stu-id="13de7-151">Below is the home page for our new project (URL: "/") when it runs:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image11.png)

<span data-ttu-id="13de7-152">单击"关于"选项卡将显示一个有关页面（URL："/主页/关于"）：</span><span class="sxs-lookup"><span data-stu-id="13de7-152">Clicking the "About" tab displays an about page (URL: "/Home/About"):</span></span>

![](create-a-new-aspnet-mvc-project/_static/image12.png)

<span data-ttu-id="13de7-153">单击右上角的"登录"链接将我们带到登录页面（URL："/帐户/登录"）</span><span class="sxs-lookup"><span data-stu-id="13de7-153">Clicking the "Log On" link on the top-right takes us to a Login page (URL: "/Account/LogOn")</span></span>

![](create-a-new-aspnet-mvc-project/_static/image13.png)

<span data-ttu-id="13de7-154">如果我们没有登录帐户，我们可以单击注册链接（URL："/帐户/注册"）创建一个：</span><span class="sxs-lookup"><span data-stu-id="13de7-154">If we don't have a login account we can click the register link (URL: "/Account/Register") to create one:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image14.png)

<span data-ttu-id="13de7-155">在创建新项目时，默认情况下添加了实现上述主页、关于和注销/寄存器功能的代码。</span><span class="sxs-lookup"><span data-stu-id="13de7-155">The code to implement the above home, about, and logout/ register functionality was added by default when we created our new project.</span></span> <span data-ttu-id="13de7-156">我们将使用它作为应用程序的起点。</span><span class="sxs-lookup"><span data-stu-id="13de7-156">We'll use it as the starting point of our application.</span></span>

### <a name="testing-the-nerddinner-application"></a><span data-ttu-id="13de7-157">测试内德晚餐应用程序</span><span class="sxs-lookup"><span data-stu-id="13de7-157">Testing the NerdDinner Application</span></span>

<span data-ttu-id="13de7-158">如果我们使用 Visual Studio 2008 的专业版或更高版本，我们可以在 Visual Studio 中使用内置单元测试 IDE 支持来测试项目：</span><span class="sxs-lookup"><span data-stu-id="13de7-158">If we are using the Professional Edition or higher version of Visual Studio 2008, we can use the built-in unit testing IDE support within Visual Studio to test the project:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image15.png)

<span data-ttu-id="13de7-159">选择上述选项之一将在 IDE 中打开"测试结果"窗格，并在新项目中包含的 27 个单元测试中提供通过/失败状态，这些测试涵盖内置功能：</span><span class="sxs-lookup"><span data-stu-id="13de7-159">Choosing one of the above options will open the "Test Results" pane within the IDE and provide us with pass/fail status on the 27 unit tests included in our new project that cover the built-in functionality:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image16.png)

<span data-ttu-id="13de7-160">在本教程的后面部分，我们将介绍有关自动测试的更多信息，并添加其他单元测试，这些测试涵盖了我们实现的应用程序功能。</span><span class="sxs-lookup"><span data-stu-id="13de7-160">Later in this tutorial we'll talk more about automated testing and add additional unit tests that cover the application functionality we implement.</span></span>

### <a name="next-step"></a><span data-ttu-id="13de7-161">下一步</span><span class="sxs-lookup"><span data-stu-id="13de7-161">Next Step</span></span>

<span data-ttu-id="13de7-162">现在，我们已经有了一个基本的应用程序结构。</span><span class="sxs-lookup"><span data-stu-id="13de7-162">We've now got a basic application structure in place.</span></span> <span data-ttu-id="13de7-163">现在，让我们[创建一个数据库来存储我们的应用程序数据](create-a-database.md)。</span><span class="sxs-lookup"><span data-stu-id="13de7-163">Let's now [create a database to store our application data](create-a-database.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="13de7-164">[上一页](introducing-the-nerddinner-tutorial.md)
> [下一页](create-a-database.md)</span><span class="sxs-lookup"><span data-stu-id="13de7-164">[Previous](introducing-the-nerddinner-tutorial.md)
[Next](create-a-database.md)</span></span>

---
uid: mvc/mvc3
title: ASP.NET MVC 3 | Microsoft Docs
author: rick-anderson
description: (包括 2011 年 4 月工具更新)ASP.NET MVC 3 是一个框架，用于构建可缩放的基于标准的 web 应用程序使用成熟设计模式...
ms.author: riande
ms.date: 10/05/2010
ms.assetid: dddc8812-a0bc-49f9-aafb-caf2064c2b8c
msc.legacyurl: /mvc/mvc3
msc.type: content
ms.openlocfilehash: 82d18865815568c5df9768fd9dd403f11ebd1714
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57045424"
---
<a name="aspnet-mvc-3"></a><span data-ttu-id="ac12c-103">ASP.NET MVC 3</span><span class="sxs-lookup"><span data-stu-id="ac12c-103">ASP.NET MVC 3</span></span>
====================
> <span data-ttu-id="ac12c-104">*(包括 2011 年 4 月工具更新)*</span><span class="sxs-lookup"><span data-stu-id="ac12c-104">*(includes April 2011 Tools Update)*</span></span>
> 
> <span data-ttu-id="ac12c-105">ASP.NET MVC 3 是一个框架，用于构建可缩放的基于标准的 web 应用程序使用成熟设计模式和 ASP.NET 和.NET Framework 的强大功能。</span><span class="sxs-lookup"><span data-stu-id="ac12c-105">ASP.NET MVC 3 is a framework for building scalable, standards-based web applications using well-established design patterns and the power of ASP.NET and the .NET Framework.</span></span>
> 
> <span data-ttu-id="ac12c-106">它将通过并行安装通过 ASP.NET MVC 2，以便开始立即使用 ！</span><span class="sxs-lookup"><span data-stu-id="ac12c-106">It installs side-by-side with ASP.NET MVC 2, so get started using it today!</span></span>
> 
> <span data-ttu-id="ac12c-107">下载[此处安装程序](https://go.microsoft.com/fwlink/?LinkID=208140)</span><span class="sxs-lookup"><span data-stu-id="ac12c-107">Download the [installer here](https://go.microsoft.com/fwlink/?LinkID=208140)</span></span>


## <a name="top-features"></a><span data-ttu-id="ac12c-108">常用功能</span><span class="sxs-lookup"><span data-stu-id="ac12c-108">Top Features</span></span>

- <span data-ttu-id="ac12c-109">通过 NuGet 可扩展集成搭建基架系统</span><span class="sxs-lookup"><span data-stu-id="ac12c-109">Integrated Scaffolding system extensible via NuGet</span></span>
- <span data-ttu-id="ac12c-110">HTML 5 的启用了的项目模板</span><span class="sxs-lookup"><span data-stu-id="ac12c-110">HTML 5 enabled project templates</span></span>
- <span data-ttu-id="ac12c-111">表达视图包括新的 Razor 视图引擎</span><span class="sxs-lookup"><span data-stu-id="ac12c-111">Expressive Views including the new Razor View Engine</span></span>
- <span data-ttu-id="ac12c-112">使用依赖关系注入和全局操作筛选器的功能强大挂钩</span><span class="sxs-lookup"><span data-stu-id="ac12c-112">Powerful hooks with Dependency Injection and Global Action Filters</span></span>
- <span data-ttu-id="ac12c-113">丰富的 JavaScript 支持非介入式 JavaScript、 jQuery 验证，以及 JSON 绑定</span><span class="sxs-lookup"><span data-stu-id="ac12c-113">Rich JavaScript support with unobtrusive JavaScript, jQuery Validation, and JSON binding</span></span>
- <span data-ttu-id="ac12c-114">*读取完整功能列表[如下](#overview)*</span><span class="sxs-lookup"><span data-stu-id="ac12c-114">*Read the full feature list [below](#overview)*</span></span>

## <a name="top-links"></a><span data-ttu-id="ac12c-115">顶部的链接</span><span class="sxs-lookup"><span data-stu-id="ac12c-115">Top Links</span></span>

<span data-ttu-id="ac12c-116">什么是 ASP.NET MVC 3 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="ac12c-116">What's New in ASP.NET MVC 3</span></span>

- <span data-ttu-id="ac12c-117">Phil Haack:[ASP.NET MVC 3 已发布](http://haacked.com/archive/2011/01/13/aspnetmvc3-released.aspx)</span><span class="sxs-lookup"><span data-stu-id="ac12c-117">Phil Haack: [ASP.NET MVC 3 Released](http://haacked.com/archive/2011/01/13/aspnetmvc3-released.aspx)</span></span>
- <span data-ttu-id="ac12c-118">Scott Hanselman:[ASP.NET MVC3 WebMatrix、 NuGet、 IIS Express 和 Orchard 发布的上下文中的 Microsoft 年 1 月 Web 版本](http://www.hanselman.com/blog/ASPNETMVC3WebMatrixNuGetIISExpressAndOrchardReleasedTheMicrosoftJanuaryWebReleaseInContext.aspx)</span><span class="sxs-lookup"><span data-stu-id="ac12c-118">Scott Hanselman: [ASP.NET MVC3, WebMatrix, NuGet, IIS Express and Orchard released - The Microsoft January Web Release in Context](http://www.hanselman.com/blog/ASPNETMVC3WebMatrixNuGetIISExpressAndOrchardReleasedTheMicrosoftJanuaryWebReleaseInContext.aspx)</span></span>
- <span data-ttu-id="ac12c-119">Scott Guthrie:[宣布发布 ASP.NET MVC 3、 IIS Express、 SQL CE 4、 Web 场框架、 Orchard、 WebMatrix](https://weblogs.asp.net/scottgu/archive/2011/01/13/announcing-release-of-asp-net-mvc-3-iis-express-sql-ce-4-web-farm-framework-orchard-webmatrix.aspx)</span><span class="sxs-lookup"><span data-stu-id="ac12c-119">Scott Guthrie: [Announcing release of ASP.NET MVC 3, IIS Express, SQL CE 4, Web Farm Framework, Orchard, WebMatrix](https://weblogs.asp.net/scottgu/archive/2011/01/13/announcing-release-of-asp-net-mvc-3-iis-express-sql-ce-4-web-farm-framework-orchard-webmatrix.aspx)</span></span>
- [<span data-ttu-id="ac12c-120">ASP.NET MVC 3 的发行说明</span><span class="sxs-lookup"><span data-stu-id="ac12c-120">Release Notes for ASP.NET MVC 3</span></span>](../whitepapers/mvc3-release-notes.md)

<span data-ttu-id="ac12c-121">安装和帮助</span><span class="sxs-lookup"><span data-stu-id="ac12c-121">Installation and Help</span></span>

- <span data-ttu-id="ac12c-122">安装 ASP.NET MVC 3 使用[Web 平台安装程序 （推荐）](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MVC3)</span><span class="sxs-lookup"><span data-stu-id="ac12c-122">Install ASP.NET MVC 3 using the [Web Platform Installer (recommended)](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MVC3)</span></span>
- <span data-ttu-id="ac12c-123">安装 ASP.NET MVC 3 使用[安装程序可执行文件](https://go.microsoft.com/fwlink/?LinkID=208140)</span><span class="sxs-lookup"><span data-stu-id="ac12c-123">Install ASP.NET MVC 3 using the [installer executable](https://go.microsoft.com/fwlink/?LinkID=208140)</span></span>
- <span data-ttu-id="ac12c-124">安装[适用于 Visual Studio 11 开发者预览版的 ASP.NET MVC 3](https://go.microsoft.com/fwlink/?LinkID=208140)</span><span class="sxs-lookup"><span data-stu-id="ac12c-124">Install [ASP.NET MVC 3 for Visual Studio 11 Developer Preview](https://go.microsoft.com/fwlink/?LinkID=208140)</span></span>
- <span data-ttu-id="ac12c-125">读取[对 ASP.NET MVC 3 教程简介](overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)</span><span class="sxs-lookup"><span data-stu-id="ac12c-125">Read the [Intro to ASP.NET MVC 3 tutorial](overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)</span></span>
- <span data-ttu-id="ac12c-126">获取帮助和讨论中的 ASP.NET MVC 3[论坛](https://forums.asp.net/1146.aspx)</span><span class="sxs-lookup"><span data-stu-id="ac12c-126">Get help and discuss ASP.NET MVC 3 in the [forums](https://forums.asp.net/1146.aspx)</span></span>

<a id="overview"></a>
## <a name="aspnet-mvc-3-overview"></a><span data-ttu-id="ac12c-127">ASP.NET MVC 3 概述</span><span class="sxs-lookup"><span data-stu-id="ac12c-127">ASP.NET MVC 3 Overview</span></span>

<span data-ttu-id="ac12c-128">ASP.NET MVC 3 上的 ASP.NET MVC 1 和 2，生成添加强大的功能，同时简化你的代码，并允许更深入的可扩展性。</span><span class="sxs-lookup"><span data-stu-id="ac12c-128">ASP.NET MVC 3 builds on ASP.NET MVC 1 and 2, adding great features that both simplify your code and allow deeper extensibility.</span></span> <span data-ttu-id="ac12c-129">本主题提供许多新功能包括在此版本中，划分为以下部分的概述：</span><span class="sxs-lookup"><span data-stu-id="ac12c-129">This topic provides an overview of many of the new features that are included in this release, organized into the following sections:</span></span>

- [<span data-ttu-id="ac12c-130">使用 MvcScaffold 集成可扩展基架</span><span class="sxs-lookup"><span data-stu-id="ac12c-130">Extensible Scaffolding with MvcScaffold integration</span></span>](#BM_MvcScaffolding)
- [<span data-ttu-id="ac12c-131">HTML 5 的启用了的项目模板</span><span class="sxs-lookup"><span data-stu-id="ac12c-131">HTML 5 enabled project templates</span></span>](#BM_HTML5)
- [<span data-ttu-id="ac12c-132">Razor 视图引擎</span><span class="sxs-lookup"><span data-stu-id="ac12c-132">The Razor View Engine</span></span>](#BM_TheRazorViewEngine)
- [<span data-ttu-id="ac12c-133">对多个视图引擎的支持</span><span class="sxs-lookup"><span data-stu-id="ac12c-133">Support for Multiple View Engines</span></span>](#BM_Support_for_Multiple_View_Engines)
- [<span data-ttu-id="ac12c-134">控制器的改进</span><span class="sxs-lookup"><span data-stu-id="ac12c-134">Controller Improvements</span></span>](#BM_Controller_Improvements)
- [<span data-ttu-id="ac12c-135">JavaScript 和 Ajax</span><span class="sxs-lookup"><span data-stu-id="ac12c-135">JavaScript and Ajax</span></span>](#BM_JavaScript_and_Ajax_Improvements)
- [<span data-ttu-id="ac12c-136">模型验证改进</span><span class="sxs-lookup"><span data-stu-id="ac12c-136">Model Validation Improvements</span></span>](#BM_Model_Validation_Improvements)
- [<span data-ttu-id="ac12c-137">依赖关系注入的改进</span><span class="sxs-lookup"><span data-stu-id="ac12c-137">Dependency Injection Improvements</span></span>](#BM_Dependency_Injection_Improvements)
- [<span data-ttu-id="ac12c-138">其他新增功能</span><span class="sxs-lookup"><span data-stu-id="ac12c-138">Other New Features</span></span>](#BM_Other_New_Features)

<a id="BM_MvcScaffolding"></a>

## <a name="extensible-scaffolding-with-mvcscaffold-integration"></a><span data-ttu-id="ac12c-139">使用 MvcScaffold 集成可扩展基架</span><span class="sxs-lookup"><span data-stu-id="ac12c-139">Extensible Scaffolding with MvcScaffold integration</span></span>

<span data-ttu-id="ac12c-140">新搭建基架系统轻松选择并开始高效地使用，如果你是全新到框架，还可以自动执行常见开发任务，如果您是经验丰富和已经知道自己在做什么。</span><span class="sxs-lookup"><span data-stu-id="ac12c-140">The new Scaffolding system makes it easier to pick up and start using productively if you're entirely new to the framework, and to automate common development tasks if you're experienced and already know what you're doing.</span></span>

<span data-ttu-id="ac12c-141">这新的 NuGet 支持*基架*名为包**MvcScaffolding**。</span><span class="sxs-lookup"><span data-stu-id="ac12c-141">This is supported by new NuGet *scaffolding* package called **MvcScaffolding**.</span></span> <span data-ttu-id="ac12c-142">术语"搭建基架"由许多软件技术来表示"快速生成可以在软件的基本概述然后编辑和自定义"。</span><span class="sxs-lookup"><span data-stu-id="ac12c-142">The term "Scaffolding" is used by many software technologies to mean "quickly generating a basic outline of your software that you can then edit and customize".</span></span> <span data-ttu-id="ac12c-143">我们正在创建 ASP.NET mvc 基架包是大有裨益几个方案中：</span><span class="sxs-lookup"><span data-stu-id="ac12c-143">The scaffolding package we're creating for ASP.NET MVC is greatly beneficial in several scenarios:</span></span>

- <span data-ttu-id="ac12c-144">**如果你第一次了解 ASP.NET MVC**，因为这样可以快速获取一些有用的工作代码，然后可以编辑，并根据需要调整。</span><span class="sxs-lookup"><span data-stu-id="ac12c-144">**If you're learning ASP.NET MVC for the first time**, because it gives you a fast way to get some useful, working code, that you can then edit and adapt according to your needs.</span></span> <span data-ttu-id="ac12c-145">它使您的查看空白页并不知道从何处着手缩短 ！</span><span class="sxs-lookup"><span data-stu-id="ac12c-145">It saves you from the trauma of looking at a blank page and having no idea where to start!</span></span>
- <span data-ttu-id="ac12c-146">**如果您非常熟悉 ASP.NET MVC，而且现在浏览外接程序的新的技术**如对象关系映射器、 视图引擎、 一个测试库等，因为这项技术的创建者可能还创建了基架程序包它。</span><span class="sxs-lookup"><span data-stu-id="ac12c-146">**If you know ASP.NET MVC well and are now exploring some new add-on technology** such as an object-relational mapper, a view engine, a testing library, etc., because the creator of that technology may have also created a scaffolding package for it.</span></span>
- <span data-ttu-id="ac12c-147">**如果您的工作涉及到反复创建相似的类或某种类型的文件**，因为您可以创建自定义输出测试装置、 部署脚本或任何其他所需的基架。</span><span class="sxs-lookup"><span data-stu-id="ac12c-147">**If your work involves repeatedly creating similar classes or files of some sort**, because you can create custom scaffolders that output test fixtures, deployment scripts, or whatever else you need.</span></span> <span data-ttu-id="ac12c-148">你的团队中的所有人也可以使用您自定义基架。</span><span class="sxs-lookup"><span data-stu-id="ac12c-148">Everyone on your team can use your custom scaffolders, too.</span></span>

<span data-ttu-id="ac12c-149">MvcScaffolding 中的其他功能包括：</span><span class="sxs-lookup"><span data-stu-id="ac12c-149">Other features in MvcScaffolding include:</span></span>

- <span data-ttu-id="ac12c-150">对 C# 和 VB 项目的支持</span><span class="sxs-lookup"><span data-stu-id="ac12c-150">Support for C# and VB projects</span></span>
- <span data-ttu-id="ac12c-151">支持 Razor 和 ASPX 视图引擎</span><span class="sxs-lookup"><span data-stu-id="ac12c-151">Support for the Razor and ASPX view engines</span></span>
- <span data-ttu-id="ac12c-152">支持为 ASP.NET MVC 区域的基架和使用自定义视图布局/母版</span><span class="sxs-lookup"><span data-stu-id="ac12c-152">Supports scaffolding into ASP.NET MVC areas and using custom view layouts/masters</span></span>
- <span data-ttu-id="ac12c-153">您可以轻松地将输出通过编辑自定义 T4 模板</span><span class="sxs-lookup"><span data-stu-id="ac12c-153">You can easily customize the output by editing T4 templates</span></span>
- <span data-ttu-id="ac12c-154">您可以添加全新的基架使用 PowerShell 的自定义逻辑和自定义 T4 模板。</span><span class="sxs-lookup"><span data-stu-id="ac12c-154">You can add entirely new scaffolders using custom PowerShell logic and custom T4 templates.</span></span> <span data-ttu-id="ac12c-155">这些 （并向用户提供任何自定义参数） 会自动出现在控制台 tab 自动补全列表。</span><span class="sxs-lookup"><span data-stu-id="ac12c-155">These (and any custom parameters you've given them) automatically appear in the console tab-completion list.</span></span>
- <span data-ttu-id="ac12c-156">可以获取包含用于不同技术的其他框架的 NuGet 包 （例如，目前的概念一个 linq to SQL） 和混合和匹配它们一起</span><span class="sxs-lookup"><span data-stu-id="ac12c-156">You can get NuGet packages containing additional scaffolders for different technologies (e.g., there's a proof-of-concept one for LINQ to SQL now) and mix and match them together</span></span>

<span data-ttu-id="ac12c-157">ASP.NET MVC 3 Tools Update 包括强大的 Visual Studio 支持此基架系统，如：</span><span class="sxs-lookup"><span data-stu-id="ac12c-157">The ASP.NET MVC 3 Tools Update includes great Visual Studio support for this scaffolding system, such as:</span></span>

- <span data-ttu-id="ac12c-158">添加控制器对话框现在支持创建、 读取、 更新和删除控制器操作和相应的视图的完整自动基架。</span><span class="sxs-lookup"><span data-stu-id="ac12c-158">Add Controller Dialog now supports full automatic scaffolding of Create, Read, Update, and Delete controller actions and corresponding views.</span></span> <span data-ttu-id="ac12c-159">默认情况下，这搭建基架以使用 EF Code First 数据访问代码。</span><span class="sxs-lookup"><span data-stu-id="ac12c-159">By default, this scaffolds data access code using EF Code First.</span></span>
- <span data-ttu-id="ac12c-160">添加控制器对话框支持*可扩展的基架*如通过 NuGet 包*MvcScaffolding*。</span><span class="sxs-lookup"><span data-stu-id="ac12c-160">Add Controller Dialog supports *extensible scaffolds* via NuGet packages such as *MvcScaffolding*.</span></span> <span data-ttu-id="ac12c-161">这允许插入到对话框，以允许你创建使用适用于 ODBCDirect 的其他数据访问技术，如 NHibernate 或甚至 JET 的基架，如果地自定义基架 ！</span><span class="sxs-lookup"><span data-stu-id="ac12c-161">This allows plugging in custom scaffolds into the dialog which would allow you to create scaffolds for other data access technologies such as NHibernate or even JET with ODBCDirect if you're so inclined!</span></span>

<span data-ttu-id="ac12c-162">有关在 ASP.NET MVC 3 中的基架的详细信息，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="ac12c-162">For more information about Scaffolding in ASP.NET MVC 3, see the following resources:</span></span>

- <span data-ttu-id="ac12c-163">Steve Sanderson 文章系列，包括：</span><span class="sxs-lookup"><span data-stu-id="ac12c-163">Steve Sanderson's post series, including:</span></span> 

    1. [<span data-ttu-id="ac12c-164">简介：创建 ASP.NET MVC 3 项目与 MvcScaffolding 包的基架</span><span class="sxs-lookup"><span data-stu-id="ac12c-164">Introduction: Scaffold your ASP.NET MVC 3 project with the MvcScaffolding package</span></span>](http://blog.stevensanderson.com/2011/01/13/scaffold-your-aspnet-mvc-3-project-with-the-mvcscaffolding-package/)
    2. [<span data-ttu-id="ac12c-165">标准使用情况：典型用例和选项</span><span class="sxs-lookup"><span data-stu-id="ac12c-165">Standard usage: Typical use cases and options</span></span>](http://blog.stevensanderson.com/2011/01/13/mvcscaffolding-standard-usage/)
    3. [<span data-ttu-id="ac12c-166">一个对多关系</span><span class="sxs-lookup"><span data-stu-id="ac12c-166">One-to-Many Relationships</span></span>](http://blog.stevensanderson.com/2011/01/28/mvcscaffolding-one-to-many-relationships/)
    4. [<span data-ttu-id="ac12c-167">基架操作和单元测试</span><span class="sxs-lookup"><span data-stu-id="ac12c-167">Scaffolding Actions and Unit Tests</span></span>](http://blog.stevensanderson.com/2011/03/28/scaffolding-actions-and-unit-tests-with-mvcscaffolding/)
    5. [<span data-ttu-id="ac12c-168">重写的 T4 模板</span><span class="sxs-lookup"><span data-stu-id="ac12c-168">Overriding the T4 templates</span></span>](http://blog.stevensanderson.com/2011/04/06/mvcscaffolding-overriding-the-t4-templates/)
    6. [<span data-ttu-id="ac12c-169">此文章：创建自定义基架</span><span class="sxs-lookup"><span data-stu-id="ac12c-169">This post: Creating custom scaffolders</span></span>](http://blog.stevensanderson.com/2011/04/07/mvcscaffolding-creating-custom-scaffolders/)
- <span data-ttu-id="ac12c-170">来自 PDC 2010 会话的 Scott Hanselman 的博文[构建与 Microsoft"未命名包的 Web Love"博客](http://www.hanselman.com/blog/PDC10BuildingABlogWithMicrosoftUnnamedPackageOfWebLove.aspx)</span><span class="sxs-lookup"><span data-stu-id="ac12c-170">Scott Hanselman's post from his PDC 2010 session [Building a Blog with Microsoft "Unnamed Package of Web Love"](http://www.hanselman.com/blog/PDC10BuildingABlogWithMicrosoftUnnamedPackageOfWebLove.aspx)</span></span>
- [<span data-ttu-id="ac12c-171">MVC 3 发行说明</span><span class="sxs-lookup"><span data-stu-id="ac12c-171">MVC 3 Release Notes</span></span>](../whitepapers/mvc3-release-notes.md)

<a id="BM_HTML5"></a>

## <a name="html-5-project-templates"></a><span data-ttu-id="ac12c-172">HTML 5 项目模板</span><span class="sxs-lookup"><span data-stu-id="ac12c-172">HTML 5 Project Templates</span></span>

<span data-ttu-id="ac12c-173">新建项目对话框中包括项目模板的复选框启用 HTML 5 版本。</span><span class="sxs-lookup"><span data-stu-id="ac12c-173">The New Project dialog includes a checkbox enable HTML 5 versions of project templates.</span></span> <span data-ttu-id="ac12c-174">这些模板利用 Modernizr 1.7，以提供对 HTML 和 CSS 3 在低级别浏览器中的兼容性支持。</span><span class="sxs-lookup"><span data-stu-id="ac12c-174">These templates leverage Modernizr 1.7 to provide compatibility support for HTML 5 and CSS 3 in down-level browsers.</span></span>

<a id="BM_TheRazorViewEngine"></a>

## <a name="the-razor-view-engine"></a><span data-ttu-id="ac12c-175">Razor 视图引擎</span><span class="sxs-lookup"><span data-stu-id="ac12c-175">The Razor View Engine</span></span>

<span data-ttu-id="ac12c-176">ASP.NET MVC 3 附带的新视图引擎名为 Razor 提供了以下好处：</span><span class="sxs-lookup"><span data-stu-id="ac12c-176">ASP.NET MVC 3 comes with a new view engine named Razor that offers the following benefits:</span></span>

- <span data-ttu-id="ac12c-177">Razor 语法是干净且简洁，要求最小击键次数。</span><span class="sxs-lookup"><span data-stu-id="ac12c-177">Razor syntax is clean and concise, requiring a minimum number of keystrokes.</span></span>
- <span data-ttu-id="ac12c-178">Razor 是易于学习，部分因为它基于现有 C# 和 Visual Basic 等语言。</span><span class="sxs-lookup"><span data-stu-id="ac12c-178">Razor is easy to learn, in part because it's based on existing languages like C# and Visual Basic.</span></span>
- <span data-ttu-id="ac12c-179">Visual Studio 包含 Razor 语法的 IntelliSense 和代码着色。</span><span class="sxs-lookup"><span data-stu-id="ac12c-179">Visual Studio includes IntelliSense and code colorization for Razor syntax.</span></span>
- <span data-ttu-id="ac12c-180">Razor 视图可以进行单元测试而无需运行该应用程序，或启动 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="ac12c-180">Razor views can be unit tested without requiring that you run the application or launch a web server.</span></span>

<span data-ttu-id="ac12c-181">一些新 Razor 功能包括：</span><span class="sxs-lookup"><span data-stu-id="ac12c-181">Some new Razor features include the following:</span></span>

- <span data-ttu-id="ac12c-182">`@model` 指定传递给视图的类型的语法。</span><span class="sxs-lookup"><span data-stu-id="ac12c-182">`@model` syntax for specifying the type being passed to the view.</span></span>
- <span data-ttu-id="ac12c-183">`@* *@` 注释语法。</span><span class="sxs-lookup"><span data-stu-id="ac12c-183">`@* *@` comment syntax.</span></span>
- <span data-ttu-id="ac12c-184">若要指定默认值的功能 (如`layoutpage`) 为整个站点一次。</span><span class="sxs-lookup"><span data-stu-id="ac12c-184">The ability to specify defaults (such as `layoutpage`) once for an entire site.</span></span>
- <span data-ttu-id="ac12c-185">`Html.Raw`方法而无需 HTML 编码的文本显示它。</span><span class="sxs-lookup"><span data-stu-id="ac12c-185">The `Html.Raw` method for displaying text without HTML-encoding it.</span></span>
- <span data-ttu-id="ac12c-186">对多个视图之间共享代码的支持 (*\_viewstart.cshtml*或 *\_viewstart.vbhtml*文件)。</span><span class="sxs-lookup"><span data-stu-id="ac12c-186">Support for sharing code among multiple views (*\_viewstart.cshtml* or *\_viewstart.vbhtml* files).</span></span>

<span data-ttu-id="ac12c-187">Razor 还包括新的 HTML 帮助器，如下所示：</span><span class="sxs-lookup"><span data-stu-id="ac12c-187">Razor also includes  new HTML helpers, such as the following:</span></span>

- <span data-ttu-id="ac12c-188">`Chart`。</span><span class="sxs-lookup"><span data-stu-id="ac12c-188">`Chart`.</span></span> <span data-ttu-id="ac12c-189">呈现的图表，产品/服务与 ASP.NET 4 中的图表控件相同的功能。</span><span class="sxs-lookup"><span data-stu-id="ac12c-189">Renders a chart, offering the same features as the chart control in ASP.NET 4.</span></span>
- <span data-ttu-id="ac12c-190">`WebGrid`。</span><span class="sxs-lookup"><span data-stu-id="ac12c-190">`WebGrid`.</span></span> <span data-ttu-id="ac12c-191">呈现数据网格中，完成，但分页和排序功能。</span><span class="sxs-lookup"><span data-stu-id="ac12c-191">Renders a data grid, complete with paging and sorting functionality.</span></span>
- <span data-ttu-id="ac12c-192">`Crypto`。</span><span class="sxs-lookup"><span data-stu-id="ac12c-192">`Crypto`.</span></span> <span data-ttu-id="ac12c-193">使用哈希算法来创建正确加盐，哈希处理密码。</span><span class="sxs-lookup"><span data-stu-id="ac12c-193">Uses hashing algorithms to create properly salted and hashed passwords.</span></span>
- <span data-ttu-id="ac12c-194">`WebImage`。</span><span class="sxs-lookup"><span data-stu-id="ac12c-194">`WebImage`.</span></span> <span data-ttu-id="ac12c-195">呈现图像。</span><span class="sxs-lookup"><span data-stu-id="ac12c-195">Renders an image.</span></span>
- <span data-ttu-id="ac12c-196">`WebMail`。</span><span class="sxs-lookup"><span data-stu-id="ac12c-196">`WebMail`.</span></span> <span data-ttu-id="ac12c-197">发送电子邮件。</span><span class="sxs-lookup"><span data-stu-id="ac12c-197">Sends an email message.</span></span>

<span data-ttu-id="ac12c-198">有关 Razor 的详细信息，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="ac12c-198">For more information about Razor, see the following resources:</span></span>

- [<span data-ttu-id="ac12c-199">Introducing Razor Scott Guthrie 的博客文章</span><span class="sxs-lookup"><span data-stu-id="ac12c-199">Scott Guthrie's blog post introducing Razor</span></span>](https://weblogs.asp.net/scottgu/archive/2010/07/02/introducing-razor.aspx)
- [<span data-ttu-id="ac12c-200">Scott Guthrie 的博客文章介绍@model关键字</span><span class="sxs-lookup"><span data-stu-id="ac12c-200">Scott Guthrie's blog post introducing the @model keyword</span></span>](https://weblogs.asp.net/scottgu/archive/2010/10/19/asp-net-mvc-3-new-model-directive-support-in-razor.aspx)
- [<span data-ttu-id="ac12c-201">Scott Guthrie 的博客文章介绍 Razor 布局</span><span class="sxs-lookup"><span data-stu-id="ac12c-201">Scott Guthrie's blog post introducing Razor layouts</span></span>](https://weblogs.asp.net/scottgu/archive/2010/10/22/asp-net-mvc-3-layouts.aspx)
- [<span data-ttu-id="ac12c-202">Razor API 快速参考</span><span class="sxs-lookup"><span data-stu-id="ac12c-202">Razor API Quick Reference</span></span>](../web-pages/overview/api-reference/asp-net-web-pages-api-reference.md)
- [<span data-ttu-id="ac12c-203">MVC 3 发行说明</span><span class="sxs-lookup"><span data-stu-id="ac12c-203">MVC 3 Release Notes</span></span>](../whitepapers/mvc3-release-notes.md)

<a id="BM_Support_for_Multiple_View_Engines"></a>

## <a name="support-for-multiple-view-engines"></a><span data-ttu-id="ac12c-204">对多个视图引擎的支持</span><span class="sxs-lookup"><span data-stu-id="ac12c-204">Support for Multiple View Engines</span></span>

<span data-ttu-id="ac12c-205">**添加视图**对话框在 ASP.NET MVC 3 中的，可以选择你想要使用的视图引擎并**新项目**对话框可以指定一个项目的默认视图引擎。</span><span class="sxs-lookup"><span data-stu-id="ac12c-205">The **Add View** dialog box in ASP.NET MVC 3 lets you choose the view engine you want to work with, and the **New Project** dialog box lets you specify the default view engine for a project.</span></span> <span data-ttu-id="ac12c-206">您可以如选择 Web 窗体视图引擎 (ASPX)、 Razor 或开放源代码视图引擎[Spark](http://sparkviewengine.com/)， [NHaml](https://code.google.com/p/nhaml/)，或[NDjango](http://ndjango.org/)。</span><span class="sxs-lookup"><span data-stu-id="ac12c-206">You can choose the Web Forms view engine (ASPX), Razor, or an open-source view engine such as [Spark](http://sparkviewengine.com/), [NHaml](https://code.google.com/p/nhaml/), or [NDjango](http://ndjango.org/).</span></span>

<a id="BM_Controller_Improvements"></a>

## <a name="controller-improvements"></a><span data-ttu-id="ac12c-207">控制器的改进</span><span class="sxs-lookup"><span data-stu-id="ac12c-207">Controller Improvements</span></span>

### <a name="global-action-filters"></a><span data-ttu-id="ac12c-208">全局操作筛选器</span><span class="sxs-lookup"><span data-stu-id="ac12c-208">Global Action Filters</span></span>

<span data-ttu-id="ac12c-209">有时你想要执行的逻辑操作方法运行之前或之后运行操作方法。</span><span class="sxs-lookup"><span data-stu-id="ac12c-209">Sometimes you want to perform logic either before an action method runs or after an action method runs.</span></span> <span data-ttu-id="ac12c-210">若要支持此功能，ASP.NET MVC 2 提供操作筛选器。</span><span class="sxs-lookup"><span data-stu-id="ac12c-210">To support this, ASP.NET MVC 2 provided action filters.</span></span> <span data-ttu-id="ac12c-211">操作筛选器是提供一种声明性方式将操作前和操作后行为添加到特定控制器操作方法的自定义属性。</span><span class="sxs-lookup"><span data-stu-id="ac12c-211">Action filters are custom attributes that provide a declarative means to add pre-action and post-action behavior to specific controller action methods.</span></span> <span data-ttu-id="ac12c-212">但是，在某些情况下您可能想要指定应用于所有操作方法的操作前或后操作行为。</span><span class="sxs-lookup"><span data-stu-id="ac12c-212">However, in some cases you might want to specify pre-action or post-action behavior that applies to all action methods.</span></span> <span data-ttu-id="ac12c-213">MVC 3，可以通过将它们添加到指定的全局筛选器`GlobalFilters`集合。</span><span class="sxs-lookup"><span data-stu-id="ac12c-213">MVC 3 lets you specify global filters by adding them to the `GlobalFilters` collection.</span></span> <span data-ttu-id="ac12c-214">有关全局操作筛选器的详细信息，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="ac12c-214">For more information about global action filters, see the following resources:</span></span>

- [<span data-ttu-id="ac12c-215">MVC 3 Preview 上 Scott Guthrie 的博客</span><span class="sxs-lookup"><span data-stu-id="ac12c-215">Scott Guthrie's blog on the MVC 3 Preview</span></span>](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx)
- <span data-ttu-id="ac12c-216">[在 ASP.NET MVC 中进行筛选](https://msdn.microsoft.com/library/gg416513(VS.98).aspx)</span><span class="sxs-lookup"><span data-stu-id="ac12c-216">[Filtering in ASP.NET MVC](https://msdn.microsoft.com/library/gg416513(VS.98).aspx)</span></span>

### <a name="new-viewbag-property"></a><span data-ttu-id="ac12c-217">新的"ViewBag"属性</span><span class="sxs-lookup"><span data-stu-id="ac12c-217">New "ViewBag" Property</span></span>

<span data-ttu-id="ac12c-218">MVC 2 控制器支持`ViewData`属性，可用于将数据传递给视图模板使用后期绑定字典 API。</span><span class="sxs-lookup"><span data-stu-id="ac12c-218">MVC 2 controllers support a `ViewData` property that enables you to pass data to a view template using a late-bound dictionary API.</span></span> <span data-ttu-id="ac12c-219">在 MVC 3 中，您还可以使用稍微简单一些语法与`ViewBag`属性来完成相同的目的。</span><span class="sxs-lookup"><span data-stu-id="ac12c-219">In MVC 3, you can also use somewhat simpler syntax with the `ViewBag` property to accomplish the same purpose.</span></span> <span data-ttu-id="ac12c-220">例如，而不是编写`ViewData["Message"]="text"`，可以编写`ViewBag.Message="text"`。</span><span class="sxs-lookup"><span data-stu-id="ac12c-220">For example, instead of writing `ViewData["Message"]="text"`, you can write `ViewBag.Message="text"`.</span></span> <span data-ttu-id="ac12c-221">不需要定义要使用任何强类型化的类`ViewBag`属性。</span><span class="sxs-lookup"><span data-stu-id="ac12c-221">You do not need to define any strongly-typed classes to use the `ViewBag` property.</span></span> <span data-ttu-id="ac12c-222">因为它是动态属性，而是，可以只需获取或设置属性并将它们动态在运行时解析。</span><span class="sxs-lookup"><span data-stu-id="ac12c-222">Because it is a dynamic property, you can instead just get or set properties and it will resolve them dynamically at run time.</span></span> <span data-ttu-id="ac12c-223">在内部，`ViewBag`属性存储为名称/值对中`ViewData`字典。</span><span class="sxs-lookup"><span data-stu-id="ac12c-223">Internally, `ViewBag` properties are stored as name/value pairs in the `ViewData` dictionary.</span></span> <span data-ttu-id="ac12c-224">(注意： 在 MVC 3 的大多数预发布版本`ViewBag`属性的名称为`ViewModel`属性。)</span><span class="sxs-lookup"><span data-stu-id="ac12c-224">(Note: in most pre-release versions of MVC 3, the `ViewBag` property was named the `ViewModel` property.)</span></span>

### <a name="new-actionresult-types"></a><span data-ttu-id="ac12c-225">新的"ActionResult"类型</span><span class="sxs-lookup"><span data-stu-id="ac12c-225">New "ActionResult" Types</span></span>

<span data-ttu-id="ac12c-226">以下`ActionResult`类型和相应的帮助器方法是 MVC 3 中新增或增强：</span><span class="sxs-lookup"><span data-stu-id="ac12c-226">The following `ActionResult` types and corresponding helper methods are new or enhanced in MVC 3:</span></span>

- <span data-ttu-id="ac12c-227">[HttpNotFoundResult](https://msdn.microsoft.com/library/system.web.mvc.httpnotfoundresult(v=vs.98).aspx)。</span><span class="sxs-lookup"><span data-stu-id="ac12c-227">[HttpNotFoundResult](https://msdn.microsoft.com/library/system.web.mvc.httpnotfoundresult(v=vs.98).aspx).</span></span> <span data-ttu-id="ac12c-228">返回到客户端的 HTTP 状态代码为 404。</span><span class="sxs-lookup"><span data-stu-id="ac12c-228">Returns a 404 HTTP status code to the client.</span></span>
- <span data-ttu-id="ac12c-229">[RedirectResult](https://msdn.microsoft.com/library/system.web.mvc.redirectresult(v=VS.98).aspx)。</span><span class="sxs-lookup"><span data-stu-id="ac12c-229">[RedirectResult](https://msdn.microsoft.com/library/system.web.mvc.redirectresult(v=VS.98).aspx).</span></span> <span data-ttu-id="ac12c-230">返回临时重定向 （HTTP 302 状态代码） 或根据布尔参数的永久重定向 （HTTP 301 状态代码）。</span><span class="sxs-lookup"><span data-stu-id="ac12c-230">Returns a temporary redirect (HTTP 302 status code) or a permanent redirect (HTTP 301 status code), depending on a Boolean parameter.</span></span> <span data-ttu-id="ac12c-231">与此更改后，结合[控制器](https://msdn.microsoft.com/library/system.web.mvc.controller(v=VS.98).aspx)类现在有三种方法来执行永久重定向： `RedirectPermanent`， `RedirectToRoutePermanent`，和`RedirectToActionPermanent`。</span><span class="sxs-lookup"><span data-stu-id="ac12c-231">In conjunction with this change, the [Controller](https://msdn.microsoft.com/library/system.web.mvc.controller(v=VS.98).aspx) class now has three methods for performing permanent redirects: `RedirectPermanent`, `RedirectToRoutePermanent`, and `RedirectToActionPermanent`.</span></span> <span data-ttu-id="ac12c-232">这些方法返回的实例`RedirectResult`与`Permanent`属性设置为`true`。</span><span class="sxs-lookup"><span data-stu-id="ac12c-232">These methods return an instance of `RedirectResult` with the `Permanent` property set to `true`.</span></span>
- <span data-ttu-id="ac12c-233">[HttpStatusCodeResult](https://msdn.microsoft.com/library/system.web.mvc.httpstatuscoderesult(v=VS.98).aspx)。</span><span class="sxs-lookup"><span data-stu-id="ac12c-233">[HttpStatusCodeResult](https://msdn.microsoft.com/library/system.web.mvc.httpstatuscoderesult(v=VS.98).aspx).</span></span> <span data-ttu-id="ac12c-234">返回用户指定的 HTTP 状态代码。</span><span class="sxs-lookup"><span data-stu-id="ac12c-234">Returns a user-specified HTTP status code.</span></span>

<a id="BM_JavaScript_and_Ajax_Improvements"></a>

## <a name="javascript-and-ajax-improvements"></a><span data-ttu-id="ac12c-235">JavaScript 和 Ajax 改进</span><span class="sxs-lookup"><span data-stu-id="ac12c-235">JavaScript and Ajax Improvements</span></span>

<span data-ttu-id="ac12c-236">默认情况下，在 MVC 3 中的 Ajax 和验证帮助程序使用的非介入式 JavaScript 方法。</span><span class="sxs-lookup"><span data-stu-id="ac12c-236">By default, Ajax and validation helpers in MVC 3 use an unobtrusive JavaScript approach.</span></span> <span data-ttu-id="ac12c-237">非介入式 JavaScript 可避免将内联 JavaScript 注入到 HTML。</span><span class="sxs-lookup"><span data-stu-id="ac12c-237">Unobtrusive JavaScript avoids injecting inline JavaScript into HTML.</span></span> <span data-ttu-id="ac12c-238">这使您的 HTML 较小，越小混乱，并使其更轻松地换出或自定义 JavaScript 库。</span><span class="sxs-lookup"><span data-stu-id="ac12c-238">This makes your HTML smaller and less cluttered, and makes it easier to swap out or customize JavaScript libraries.</span></span> <span data-ttu-id="ac12c-239">在 MVC 3 中的验证帮助程序还使用`jQueryValidate`默认情况下的插件。</span><span class="sxs-lookup"><span data-stu-id="ac12c-239">Validation helpers in MVC 3 also use the `jQueryValidate` plugin by default.</span></span> <span data-ttu-id="ac12c-240">如果要使用 MVC 2 行为，则可以禁用非介入式 JavaScript 使用*web.config*文件设置。</span><span class="sxs-lookup"><span data-stu-id="ac12c-240">If you want MVC 2 behavior, you can disable unobtrusive JavaScript using a *web.config* file setting.</span></span> <span data-ttu-id="ac12c-241">有关 JavaScript 和 Ajax 改进的详细信息，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="ac12c-241">For more information about JavaScript and Ajax improvements, see the following resources:</span></span>

- [<span data-ttu-id="ac12c-242">维基百科网站上的非介入式 JavaScript 的基本简介</span><span class="sxs-lookup"><span data-stu-id="ac12c-242">Basic introduction to unobtrusive JavaScript on the Wikipedia site</span></span>](http://en.wikipedia.org/wiki/Unobtrusive_JavaScript)
- [<span data-ttu-id="ac12c-243">Brad Wilson 的非介入式 JavaScript Post</span><span class="sxs-lookup"><span data-stu-id="ac12c-243">Brad Wilson's Unobtrusive JavaScript Post</span></span>](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-ajax.html)
- [<span data-ttu-id="ac12c-244">Brad Wilson 的非介入式 JavaScript 验证 Post</span><span class="sxs-lookup"><span data-stu-id="ac12c-244">Brad Wilson's Unobtrusive JavaScript Validation Post</span></span>](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html)
- <span data-ttu-id="ac12c-245">[使用 Razor 和非介入式 JavaScript 创建 MVC 3 应用程序](overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript.md)（ASP.NET 网站教程）</span><span class="sxs-lookup"><span data-stu-id="ac12c-245">[Creating a MVC 3 Application with Razor and Unobtrusive JavaScript](overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript.md) (tutorial on the ASP.NET site)</span></span>
- [<span data-ttu-id="ac12c-246">MVC 3 发行说明</span><span class="sxs-lookup"><span data-stu-id="ac12c-246">MVC 3 Release Notes</span></span>](../whitepapers/mvc3-release-notes.md)

### <a name="client-side-validation-enabled-by-default"></a><span data-ttu-id="ac12c-247">默认情况下启用的客户端验证</span><span class="sxs-lookup"><span data-stu-id="ac12c-247">Client-Side Validation Enabled by Default</span></span>

<span data-ttu-id="ac12c-248">在早期版本的 MVC，您需要显式调用`Html.EnableClientValidation`从一个视图，以启用客户端验证的方法。</span><span class="sxs-lookup"><span data-stu-id="ac12c-248">In earlier versions of MVC, you need to explicitly call the `Html.EnableClientValidation` method from a view in order to enable client-side validation.</span></span> <span data-ttu-id="ac12c-249">在 MVC 3 中这是不再需要因为默认情况下启用客户端验证。</span><span class="sxs-lookup"><span data-stu-id="ac12c-249">In MVC 3 this is no longer required because client-side validation is enabled by default.</span></span> <span data-ttu-id="ac12c-250">(您可以禁用此使用中的设置*web.config*文件。)</span><span class="sxs-lookup"><span data-stu-id="ac12c-250">(You can disable this using a setting in the *web.config* file.)</span></span>

<span data-ttu-id="ac12c-251">为了使客户端端验证正常工作，仍然需要引用相应 jQuery 和 jQuery 验证站点中的库。</span><span class="sxs-lookup"><span data-stu-id="ac12c-251">In order for client-side validation to work, you still need to reference the appropriate jQuery and jQuery Validation libraries in your site.</span></span> <span data-ttu-id="ac12c-252">可以在你自己的服务器上托管这些库，也可以从 Microsoft 或 Google Cdn 等内容分发网络 (CDN) 中引用它们。</span><span class="sxs-lookup"><span data-stu-id="ac12c-252">You can host those libraries on your own server or reference them from a content delivery network (CDN) like the CDNs from Microsoft or Google.</span></span>

### <a name="remote-validator"></a><span data-ttu-id="ac12c-253">远程验证程序</span><span class="sxs-lookup"><span data-stu-id="ac12c-253">Remote Validator</span></span>

<span data-ttu-id="ac12c-254">ASP.NET MVC 3 支持新[RemoteAttribute](https://msdn.microsoft.com/library/system.web.mvc.remoteattribute(v=VS.98).aspx)类，可用于利用 jQuery 验证插件中的远程验证程序的支持。</span><span class="sxs-lookup"><span data-stu-id="ac12c-254">ASP.NET MVC 3 supports the new [RemoteAttribute](https://msdn.microsoft.com/library/system.web.mvc.remoteattribute(v=VS.98).aspx) class that enables you to take advantage of the jQuery Validation plug-in's remote validator support.</span></span> <span data-ttu-id="ac12c-255">这使客户端验证库，可自动调用服务器端的服务器定义以执行才可进行的验证逻辑的自定义方法。</span><span class="sxs-lookup"><span data-stu-id="ac12c-255">This enables the client-side validation library to automatically call a custom method that you define on the server in order to perform validation logic that can only be done server-side.</span></span>

<span data-ttu-id="ac12c-256">在以下示例中，`Remote`属性指定客户端验证将调用名为操作`UserNameAvailable`上`UsersController`类使用，以便验证`UserName`字段。</span><span class="sxs-lookup"><span data-stu-id="ac12c-256">In the following example, the `Remote` attribute specifies that client validation will call an action named `UserNameAvailable` on the `UsersController` class in order to validate the `UserName` field.</span></span>

[!code-csharp[Main](mvc3/samples/sample1.cs)]

<span data-ttu-id="ac12c-257">下面的示例显示了相应的控制器。</span><span class="sxs-lookup"><span data-stu-id="ac12c-257">The following example shows the corresponding controller.</span></span>

[!code-csharp[Main](mvc3/samples/sample2.cs)]

<span data-ttu-id="ac12c-258">有关如何使用详细信息`Remote`属性，请参阅[如何：在 ASP.NET MVC 中实现远程验证](https://msdn.microsoft.com/library/gg508808(VS.98).aspx)MSDN 库中。</span><span class="sxs-lookup"><span data-stu-id="ac12c-258">For more information about how to use the `Remote` attribute, see [How to: Implement Remote Validation in ASP.NET MVC](https://msdn.microsoft.com/library/gg508808(VS.98).aspx) in the MSDN library.</span></span>

### <a name="json-binding-support"></a><span data-ttu-id="ac12c-259">JSON 绑定支持</span><span class="sxs-lookup"><span data-stu-id="ac12c-259">JSON Binding Support</span></span>

<span data-ttu-id="ac12c-260">ASP.NET MVC 3 包括使操作方法来接收 JSON 编码数据和模型绑定其操作方法参数的内置 JSON 绑定支持。</span><span class="sxs-lookup"><span data-stu-id="ac12c-260">ASP.NET MVC 3 includes built-in JSON binding support that enables action methods to receive JSON-encoded data and model-bind it to action-method parameters.</span></span> <span data-ttu-id="ac12c-261">此功能是在涉及客户端模板和数据绑定方案中有用。</span><span class="sxs-lookup"><span data-stu-id="ac12c-261">This capability is useful in scenarios involving client templates and data binding.</span></span> <span data-ttu-id="ac12c-262">（客户端模板，您可以格式化和显示单个数据项组使用客户端执行的模板。）MVC 3 可轻松地将客户端模板连接在服务器上的发送和接收 JSON 数据的操作方法。</span><span class="sxs-lookup"><span data-stu-id="ac12c-262">(Client templates enable you to format and display a single data item or set of data items by using templates that execute on the client.) MVC 3 enables you to easily connect client templates with action methods on the server that send and receive JSON data.</span></span> <span data-ttu-id="ac12c-263">有关 JSON 绑定支持的详细信息，请参阅**JavaScript 和 AJAX 改进**一部分[Scott Guthrie 的 MVC 3 预览版博客文章](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ac12c-263">For more information about JSON binding support, see the **JavaScript and AJAX Improvements** section of [Scott Guthrie's MVC 3 Preview blog post](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx).</span></span>

<a id="BM_Model_Validation_Improvements"></a>

## <a name="model-validation-improvements"></a><span data-ttu-id="ac12c-264">模型验证改进</span><span class="sxs-lookup"><span data-stu-id="ac12c-264">Model Validation Improvements</span></span>

### <a name="dataannotations-metadata-attributes"></a><span data-ttu-id="ac12c-265">"DataAnnotations"元数据属性</span><span class="sxs-lookup"><span data-stu-id="ac12c-265">"DataAnnotations" Metadata Attributes</span></span>

<span data-ttu-id="ac12c-266">ASP.NET MVC 3 支持`DataAnnotations`元数据属性，如`DisplayAttribute`。</span><span class="sxs-lookup"><span data-stu-id="ac12c-266">ASP.NET MVC 3 supports `DataAnnotations` metadata attributes such as `DisplayAttribute`.</span></span>

### <a name="validationattribute-class"></a><span data-ttu-id="ac12c-267">"ValidationAttribute"类</span><span class="sxs-lookup"><span data-stu-id="ac12c-267">"ValidationAttribute" Class</span></span>

<span data-ttu-id="ac12c-268">`ValidationAttribute`类在.NET Framework 4，以支持新改进了`IsValid`重载提供了有关当前验证上下文，如哪些对象正在进行验证的详细信息。</span><span class="sxs-lookup"><span data-stu-id="ac12c-268">The `ValidationAttribute` class was improved in the .NET Framework 4 to support a new `IsValid` overload that provides more information about the current validation context, such as what object is being validated.</span></span> <span data-ttu-id="ac12c-269">这使您可以在其中验证基于模型的另一个属性的当前值更丰富的方案。</span><span class="sxs-lookup"><span data-stu-id="ac12c-269">This enables richer scenarios where you can validate the current value based on another property of the model.</span></span> <span data-ttu-id="ac12c-270">例如，新`CompareAttribute`属性可用于比较两个模型的属性的值。</span><span class="sxs-lookup"><span data-stu-id="ac12c-270">For example, the new `CompareAttribute` attribute lets you compare the values of two properties of a model.</span></span> <span data-ttu-id="ac12c-271">在以下示例中，`ComparePassword`属性必须与匹配`Password`是有效的字段。</span><span class="sxs-lookup"><span data-stu-id="ac12c-271">In the following example, the `ComparePassword` property must match the `Password` field in order to be valid.</span></span>

[!code-csharp[Main](mvc3/samples/sample3.cs)]

### <a name="validation-interfaces"></a><span data-ttu-id="ac12c-272">验证接口</span><span class="sxs-lookup"><span data-stu-id="ac12c-272">Validation Interfaces</span></span>

<span data-ttu-id="ac12c-273">[IValidatableObject](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.ivalidatableobject.aspx)接口可用于执行模型级别验证，并允许您以提供特定于整个模型，或在模型中的两个属性之间的状态的错误消息的验证.</span><span class="sxs-lookup"><span data-stu-id="ac12c-273">The [IValidatableObject](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.ivalidatableobject.aspx) interface enables you to perform model-level validation, and it enables you to provide validation error messages that are specific to the state of the overall model, or between two properties within the model.</span></span> <span data-ttu-id="ac12c-274">MVC 3 现在将检索来自错误`IValidatableObject`接口时模型绑定和自动标志或突出显示受影响的字段中使用内置的 HTML 窗体帮助器的视图。</span><span class="sxs-lookup"><span data-stu-id="ac12c-274">MVC 3 now retrieves errors from the `IValidatableObject` interface when model binding, and automatically flags or highlights affected fields within a view using the built-in HTML form helpers.</span></span>

<span data-ttu-id="ac12c-275">[IClientValidatable](https://msdn.microsoft.com/library/system.web.mvc.iclientvalidatable(v=VS.98).aspx)接口使 ASP.NET MVC，若要在运行时发现验证程序是否对客户端验证的支持。</span><span class="sxs-lookup"><span data-stu-id="ac12c-275">The [IClientValidatable](https://msdn.microsoft.com/library/system.web.mvc.iclientvalidatable(v=VS.98).aspx) interface enables ASP.NET MVC to discover at run time whether a validator has support for client validation.</span></span> <span data-ttu-id="ac12c-276">此接口设计，以便它可以与多种验证框架集成。</span><span class="sxs-lookup"><span data-stu-id="ac12c-276">This interface has been designed so that it can be integrated with a variety of validation frameworks.</span></span>

<span data-ttu-id="ac12c-277">有关验证接口的详细信息，请参阅**模型验证改进**一部分[Scott Guthrie 的 MVC 3 预览版博客文章](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ac12c-277">For more information about validation interfaces, see the **Model Validation Improvements** section of [Scott Guthrie's MVC 3 Preview blog post](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx).</span></span> <span data-ttu-id="ac12c-278">（但是，请注意，对"IValidateObject"博客中的引用应"IValidatableObject"。）</span><span class="sxs-lookup"><span data-stu-id="ac12c-278">(However, note that the reference to "IValidateObject" in the blog should be "IValidatableObject".)</span></span>

<a id="BM_Dependency_Injection_Improvements"></a>

## <a name="dependency-injection-improvements"></a><span data-ttu-id="ac12c-279">依赖关系注入的改进</span><span class="sxs-lookup"><span data-stu-id="ac12c-279">Dependency Injection Improvements</span></span>

<span data-ttu-id="ac12c-280">ASP.NET MVC 3 应用依赖关系注入 (DI) 和将与依赖关系注入或控制反转 (IOC) 容器提供更好的支持。</span><span class="sxs-lookup"><span data-stu-id="ac12c-280">ASP.NET MVC 3 provides better support for applying Dependency Injection (DI) and for integrating with Dependency Injection or Inversion of Control (IOC) containers.</span></span> <span data-ttu-id="ac12c-281">在以下区域中添加了对 DI 支持：</span><span class="sxs-lookup"><span data-stu-id="ac12c-281">Support for DI has been added in the following areas:</span></span>

- <span data-ttu-id="ac12c-282">控制器 （注册和注入控制器工厂，将注入控制器）。</span><span class="sxs-lookup"><span data-stu-id="ac12c-282">Controllers (registering and injecting controller factories, injecting controllers).</span></span>
- <span data-ttu-id="ac12c-283">视图 （注册和注入视图引擎，将依赖项注入到视图页）。</span><span class="sxs-lookup"><span data-stu-id="ac12c-283">Views (registering and injecting view engines, injecting dependencies into view pages).</span></span>
- <span data-ttu-id="ac12c-284">操作筛选器 （定位和注入筛选器）。</span><span class="sxs-lookup"><span data-stu-id="ac12c-284">Action filters (locating and injecting filters).</span></span>
- <span data-ttu-id="ac12c-285">模型联编程序 （注册和注入）。</span><span class="sxs-lookup"><span data-stu-id="ac12c-285">Model binders (registering and injecting).</span></span>
- <span data-ttu-id="ac12c-286">模型验证程序提供程序 （注册和注入）。</span><span class="sxs-lookup"><span data-stu-id="ac12c-286">Model validation providers (registering and injecting).</span></span>
- <span data-ttu-id="ac12c-287">模型元数据提供程序 （注册和注入）。</span><span class="sxs-lookup"><span data-stu-id="ac12c-287">Model metadata providers (registering and injecting).</span></span>
- <span data-ttu-id="ac12c-288">值提供程序 （注册和注入）。</span><span class="sxs-lookup"><span data-stu-id="ac12c-288">Value providers (registering and injecting).</span></span>

<span data-ttu-id="ac12c-289">MVC 3 支持[Common Service Locator](https://github.com/unitycontainer/commonservicelocator)库并支持该库的任何 DI 容器`IServiceLocator`接口。</span><span class="sxs-lookup"><span data-stu-id="ac12c-289">MVC 3 supports the [Common Service Locator](https://github.com/unitycontainer/commonservicelocator) library and any DI container that supports that library's `IServiceLocator` interface.</span></span> <span data-ttu-id="ac12c-290">它还支持新`IDependencyResolver`的界面，可轻松地集成 DI 框架。</span><span class="sxs-lookup"><span data-stu-id="ac12c-290">It also supports a new `IDependencyResolver` interface that makes it easier to integrate DI frameworks.</span></span>

<span data-ttu-id="ac12c-291">有关 MVC 3 中的 DI 的详细信息，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="ac12c-291">For more information about DI in MVC 3, see the following resources:</span></span>

- [<span data-ttu-id="ac12c-292">Brad Wilson 的系列的服务位置上的博客文章</span><span class="sxs-lookup"><span data-stu-id="ac12c-292">Brad Wilson's series of blog posts on Service Location</span></span>](http://bradwilson.typepad.com/blog/2010/07/service-location-pt1-introduction.html)
- [<span data-ttu-id="ac12c-293">MVC 3 发行说明</span><span class="sxs-lookup"><span data-stu-id="ac12c-293">MVC 3 Release Notes</span></span>](../whitepapers/mvc3-release-notes.md)

<a id="BM_Other_New_Features"></a>

## <a name="other-new-features"></a><span data-ttu-id="ac12c-294">其他新增功能</span><span class="sxs-lookup"><span data-stu-id="ac12c-294">Other New Features</span></span>

### <a name="nuget-integration"></a><span data-ttu-id="ac12c-295">NuGet 集成</span><span class="sxs-lookup"><span data-stu-id="ac12c-295">NuGet Integration</span></span>

<span data-ttu-id="ac12c-296">ASP.NET MVC 3 会自动安装，并为其安装程序的一部分启用 NuGet。</span><span class="sxs-lookup"><span data-stu-id="ac12c-296">ASP.NET MVC 3 automatically installs and enables NuGet as part of its setup.</span></span> <span data-ttu-id="ac12c-297">NuGet 是免费的开放源代码程序包管理器，轻松地查找、 安装和在项目中使用.NET 库和工具。</span><span class="sxs-lookup"><span data-stu-id="ac12c-297">NuGet is a free open-source package manager that makes it easy to find, install, and use .NET libraries and tools in your projects.</span></span> <span data-ttu-id="ac12c-298">它适用于所有 Visual Studio 项目类型 （包括 ASP.NET Web 窗体和 ASP.NET MVC）。</span><span class="sxs-lookup"><span data-stu-id="ac12c-298">It works with all Visual Studio project types (including ASP.NET Web Forms and ASP.NET MVC).</span></span>

<span data-ttu-id="ac12c-299">NuGet 支持开发人员维护的开放源代码项目 （例如，像 Moq、 NHibernate、 Ninject、 StructureMap、 NUnit、 Windsor、 RhinoMocks 和 Elmah 的项目） 其库打包并在联机库中注册它们。</span><span class="sxs-lookup"><span data-stu-id="ac12c-299">NuGet enables developers who maintain open source projects (for example, projects like Moq, NHibernate, Ninject, StructureMap, NUnit, Windsor, RhinoMocks, and Elmah) to package their libraries and register them in an online gallery.</span></span> <span data-ttu-id="ac12c-300">这样，它将简单的.NET 开发人员想要使用这些库之一来查找包并将其安装在他们正在处理的项目中。</span><span class="sxs-lookup"><span data-stu-id="ac12c-300">It is then easy for .NET developers who want to use one of these libraries to find the package and install it in projects they are working on.</span></span>

<span data-ttu-id="ac12c-301">ASP.NET 3 工具更新后，项目模板包含 JavaScript 库预安装的 NuGet 包，因此它们可通过 NuGet 更新。</span><span class="sxs-lookup"><span data-stu-id="ac12c-301">With the ASP.NET 3 Tools Update, project templates include JavaScript libraries pre-installed NuGet packages, so they are updatable via NuGet.</span></span> <span data-ttu-id="ac12c-302">Entity Framework 代码优先也会预安装 NuGet 包的形式。</span><span class="sxs-lookup"><span data-stu-id="ac12c-302">Entity Framework Code First is also pre-installed as a NuGet package.</span></span>

<span data-ttu-id="ac12c-303">有关 NuGet 的详细信息，请参阅 [NuGet 文档](https://docs.microsoft.com/nuget/)。</span><span class="sxs-lookup"><span data-stu-id="ac12c-303">For more information about NuGet, see the [NuGet documentation](https://docs.microsoft.com/nuget/).</span></span>

### <a name="partial-page-output-caching"></a><span data-ttu-id="ac12c-304">部分页面输出缓存</span><span class="sxs-lookup"><span data-stu-id="ac12c-304">Partial-Page Output Caching</span></span>

<span data-ttu-id="ac12c-305">ASP.NET MVC 具有支持输出缓存的整页响应之后的版本 1。</span><span class="sxs-lookup"><span data-stu-id="ac12c-305">ASP.NET MVC has supported output caching of full page responses since version 1.</span></span> <span data-ttu-id="ac12c-306">MVC 3 还支持部分页面输出缓存，使您能够轻松地缓存区域或响应的片段。</span><span class="sxs-lookup"><span data-stu-id="ac12c-306">MVC 3 also supports partial-page output caching, which allows you to easily cache regions or fragments of a response.</span></span> <span data-ttu-id="ac12c-307">有关缓存的详细信息，请参阅**部分页面输出缓存**一部分[Scott Guthrie 的博客文章在 MVC 3 候选发布版](https://weblogs.asp.net/scottgu/archive/2010/11/09/announcing-the-asp-net-mvc-3-release-candidate.aspx)和**子操作输出缓存**一部分[MVC 3 发行说明](../whitepapers/mvc3-release-notes.md)。</span><span class="sxs-lookup"><span data-stu-id="ac12c-307">For more information about caching, see the **Partial Page Output Caching** section of [Scott Guthrie's blog post on the MVC 3 release candidate](https://weblogs.asp.net/scottgu/archive/2010/11/09/announcing-the-asp-net-mvc-3-release-candidate.aspx) and the **Child Action Output Caching** section of the [MVC 3 Release Notes](../whitepapers/mvc3-release-notes.md).</span></span>

### <a name="granular-control-over-request-validation"></a><span data-ttu-id="ac12c-308">精细地控制请求验证</span><span class="sxs-lookup"><span data-stu-id="ac12c-308">Granular Control over Request Validation</span></span>

<span data-ttu-id="ac12c-309">ASP.NET MVC 的自动帮助防范 XSS 和 HTML 注入攻击的内置请求验证。</span><span class="sxs-lookup"><span data-stu-id="ac12c-309">ASP.NET MVC has built-in request validation that automatically helps protect against XSS and HTML injection attacks.</span></span> <span data-ttu-id="ac12c-310">但是，有时要显式禁用请求验证，例如，如果你想要允许用户发布 HTML 内容 （例如，在博客文章或 CMS 内容）。</span><span class="sxs-lookup"><span data-stu-id="ac12c-310">However, sometimes you want to explicitly disable request validation, such as if you want to let users post HTML content (for example, in blog entries or CMS content).</span></span> <span data-ttu-id="ac12c-311">现在，您可以添加[AllowHtml](https://msdn.microsoft.com/library/system.web.mvc.allowhtmlattribute(v=VS.98).aspx)到模型属性，或查看模型，从而禁用基于每个属性在模型绑定期间请求验证。</span><span class="sxs-lookup"><span data-stu-id="ac12c-311">You can now add an [AllowHtml](https://msdn.microsoft.com/library/system.web.mvc.allowhtmlattribute(v=VS.98).aspx) attribute to models or view models to disable request validation on a per-property basis during model binding.</span></span> <span data-ttu-id="ac12c-312">有关请求验证的详细信息，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="ac12c-312">For more information about request validation, see the following resources:</span></span>

- <span data-ttu-id="ac12c-313">**非介入式 JavaScript 和验证**主题中[Scott Guthrie 的博客文章在 MVC 3 候选发布版](https://weblogs.asp.net/scottgu/archive/2010/11/09/announcing-the-asp-net-mvc-3-release-candidate.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ac12c-313">The **Unobtrusive JavaScript and Validation** section in [Scott Guthrie's blog post on the MVC 3 release candidate](https://weblogs.asp.net/scottgu/archive/2010/11/09/announcing-the-asp-net-mvc-3-release-candidate.aspx).</span></span>
- [<span data-ttu-id="ac12c-314">MVC 3 发行说明</span><span class="sxs-lookup"><span data-stu-id="ac12c-314">MVC 3 Release Notes</span></span>](../whitepapers/mvc3-release-notes.md)

### <a name="extensible-new-project-dialog-box"></a><span data-ttu-id="ac12c-315">可扩展的"新建项目"对话框</span><span class="sxs-lookup"><span data-stu-id="ac12c-315">Extensible "New Project" Dialog Box</span></span>

<span data-ttu-id="ac12c-316">可以在 ASP.NET MVC 3 中添加项目模板，视图引擎和单元测试项目到框架**新的项目**对话框。</span><span class="sxs-lookup"><span data-stu-id="ac12c-316">In ASP.NET MVC 3 you can add project templates, view engines, and unit test project frameworks to the **New Project** dialog box.</span></span>

### <a name="template-scaffolding-improvements"></a><span data-ttu-id="ac12c-317">模板基架的改进</span><span class="sxs-lookup"><span data-stu-id="ac12c-317">Template Scaffolding Improvements</span></span>

<span data-ttu-id="ac12c-318">ASP.NET MVC 3 基架模板更好地确定模型上的主键属性并适当地比在早期版本的 MVC 处理。</span><span class="sxs-lookup"><span data-stu-id="ac12c-318">ASP.NET MVC 3 scaffolding templates do a better job of identifying primary-key properties on models and handling them appropriately than in earlier versions of MVC.</span></span> <span data-ttu-id="ac12c-319">（例如，基架模板现在请确保主键不基架为可编辑窗体字段。）</span><span class="sxs-lookup"><span data-stu-id="ac12c-319">(For example, the scaffolding templates now make sure that the primary key is not scaffolded as an editable form field.)</span></span>

<span data-ttu-id="ac12c-320">默认情况下，现在使用的创建和编辑基架`Html.EditorFor`帮助器而不是`Html.TextBoxFor`帮助器。</span><span class="sxs-lookup"><span data-stu-id="ac12c-320">By default, the Create and Edit scaffolds now use the `Html.EditorFor` helper instead of the `Html.TextBoxFor` helper.</span></span> <span data-ttu-id="ac12c-321">这提高了支持的数据窗体中的模型的元数据批注特性何时**添加视图**对话框将生成一个视图。</span><span class="sxs-lookup"><span data-stu-id="ac12c-321">This improves support for metadata on the model in the form of data annotation attributes when the **Add View** dialog box generates a view.</span></span>

### <a name="new-overloads-for-htmllabelfor-and-htmllabelformodel"></a><span data-ttu-id="ac12c-322">"Html.LabelFor"和"Html.LabelForModel"的新重载</span><span class="sxs-lookup"><span data-stu-id="ac12c-322">New Overloads for "Html.LabelFor" and "Html.LabelForModel"</span></span>

<span data-ttu-id="ac12c-323">已添加的新方法重载`LabelFor`和`LabelForModel`帮助器方法。</span><span class="sxs-lookup"><span data-stu-id="ac12c-323">New method overloads have been added for the `LabelFor` and `LabelForModel` helper methods.</span></span> <span data-ttu-id="ac12c-324">新重载，可指定或重写的标签文本。</span><span class="sxs-lookup"><span data-stu-id="ac12c-324">The new overloads enable you to specify or override the label text.</span></span>

### <a name="sessionless-controller-support"></a><span data-ttu-id="ac12c-325">无会话控制器支持</span><span class="sxs-lookup"><span data-stu-id="ac12c-325">Sessionless Controller Support</span></span>

<span data-ttu-id="ac12c-326">在 ASP.NET MVC 3 中可以指示是否想要使用会话状态，控制器类，如果是，是否会话状态应为读/写或只读的。</span><span class="sxs-lookup"><span data-stu-id="ac12c-326">In ASP.NET MVC 3 you can indicate whether you want a controller class to use session state, and if so, whether session state should be read/write or read-only.</span></span> <span data-ttu-id="ac12c-327">有关无会话控制器支持的详细信息，请参阅[MVC 3 发行说明](../whitepapers/mvc3-release-notes.md)。</span><span class="sxs-lookup"><span data-stu-id="ac12c-327">For more information about sessionless controller support, see [MVC 3 Release Notes](../whitepapers/mvc3-release-notes.md).</span></span>

### <a name="new-additionalmetadataattribute-class"></a><span data-ttu-id="ac12c-328">"AdditionalMetadataAttribute"的新类</span><span class="sxs-lookup"><span data-stu-id="ac12c-328">New "AdditionalMetadataAttribute" Class</span></span>

<span data-ttu-id="ac12c-329">可以使用[AdditionalMetadata](https://msdn.microsoft.com/library/system.web.mvc.additionalmetadataattribute(v=VS.98).aspx)属性来填充`ModelMetadata.AdditionalValues`模型属性的字典。</span><span class="sxs-lookup"><span data-stu-id="ac12c-329">You can use the [AdditionalMetadata](https://msdn.microsoft.com/library/system.web.mvc.additionalmetadataattribute(v=VS.98).aspx) attribute to populate the `ModelMetadata.AdditionalValues` dictionary for a model property.</span></span> <span data-ttu-id="ac12c-330">例如，如果视图模型具有一个属性，它应仅向管理员显示，你可以批注该属性，如下面的示例中所示：</span><span class="sxs-lookup"><span data-stu-id="ac12c-330">For example, if a view model has a property that should be displayed only to an administrator, you can annotate that property as shown in the following example:</span></span>

[!code-csharp[Main](mvc3/samples/sample4.cs)]

<span data-ttu-id="ac12c-331">呈现产品视图模型时，此元数据将提供到任何显示或编辑器的模板。</span><span class="sxs-lookup"><span data-stu-id="ac12c-331">This metadata is made available to any display or editor template when a product view model is rendered.</span></span> <span data-ttu-id="ac12c-332">它是由您来解释元数据信息。</span><span class="sxs-lookup"><span data-stu-id="ac12c-332">It is up to you to interpret the metadata information.</span></span>

### <a name="accountcontroller-improvements"></a><span data-ttu-id="ac12c-333">AccountController 的改进</span><span class="sxs-lookup"><span data-stu-id="ac12c-333">AccountController improvements</span></span>

<span data-ttu-id="ac12c-334">AccountController Internet 项目模板中的得到了显著改善。</span><span class="sxs-lookup"><span data-stu-id="ac12c-334">The AccountController in the Internet project template has been greatly improved.</span></span>

### <a name="new-intranet-project-template"></a><span data-ttu-id="ac12c-335">新建 Intranet 项目模板</span><span class="sxs-lookup"><span data-stu-id="ac12c-335">New Intranet Project Template</span></span>

<span data-ttu-id="ac12c-336">一个新的 Intranet 项目模板，包括其启用 Windows 身份验证，并删除 AccountController。</span><span class="sxs-lookup"><span data-stu-id="ac12c-336">A new Intranet Project Template is included which enables Windows Authentication and removes the AccountController.</span></span>

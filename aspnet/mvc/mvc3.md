---
uid: mvc/mvc3
title: ASP.NET MVC 3
author: rick-anderson
description: （包括 2011 年 4 月工具更新）ASP.NET MVC 3 是一个框架，用于使用成熟的设计模式构建可扩展的、基于标准的 Web 应用程序...
ms.author: riande
ms.date: 10/05/2010
ms.assetid: dddc8812-a0bc-49f9-aafb-caf2064c2b8c
msc.legacyurl: /mvc/mvc3
msc.type: content
ms.openlocfilehash: 6fe734dc0d0106bb346df154e1e03f97b307567a
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675141"
---
# <a name="aspnet-mvc-3"></a><span data-ttu-id="439d4-103">ASP.NET MVC 3</span><span class="sxs-lookup"><span data-stu-id="439d4-103">ASP.NET MVC 3</span></span>

> <span data-ttu-id="439d4-104">*（包括 2011 年 4 月工具更新）*</span><span class="sxs-lookup"><span data-stu-id="439d4-104">*(includes April 2011 Tools Update)*</span></span>
> 
> <span data-ttu-id="439d4-105">ASP.NET MVC 3 是一个框架，用于使用成熟的设计模式以及 ASP.NET 和 .NET 框架的强大功能构建可扩展的、基于标准的 Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="439d4-105">ASP.NET MVC 3 is a framework for building scalable, standards-based web applications using well-established design patterns and the power of ASP.NET and the .NET Framework.</span></span>
> 
> <span data-ttu-id="439d4-106">它与mVC ASP.NET并行安装，所以立即开始使用它！</span><span class="sxs-lookup"><span data-stu-id="439d4-106">It installs side-by-side with ASP.NET MVC 2, so get started using it today!</span></span>
> 
> <span data-ttu-id="439d4-107">在此处下载[安装程序](https://microsoft.com/download/details.aspx?id=4211)</span><span class="sxs-lookup"><span data-stu-id="439d4-107">Download the [installer here](https://microsoft.com/download/details.aspx?id=4211)</span></span>

## <a name="top-features"></a><span data-ttu-id="439d4-108">热门功能</span><span class="sxs-lookup"><span data-stu-id="439d4-108">Top Features</span></span>

- <span data-ttu-id="439d4-109">集成脚手架系统可通过 NuGet 进行扩展</span><span class="sxs-lookup"><span data-stu-id="439d4-109">Integrated Scaffolding system extensible via NuGet</span></span>
- <span data-ttu-id="439d4-110">启用 HTML 5 的项目模板</span><span class="sxs-lookup"><span data-stu-id="439d4-110">HTML 5 enabled project templates</span></span>
- <span data-ttu-id="439d4-111">表现性视图，包括新的剃刀视图引擎</span><span class="sxs-lookup"><span data-stu-id="439d4-111">Expressive Views including the new Razor View Engine</span></span>
- <span data-ttu-id="439d4-112">具有依赖项注入和全局操作筛选器的强大挂钩</span><span class="sxs-lookup"><span data-stu-id="439d4-112">Powerful hooks with Dependency Injection and Global Action Filters</span></span>
- <span data-ttu-id="439d4-113">具有不显眼的 JavaScript、jQuery 验证和 JSON 绑定的丰富 JavaScript 支持</span><span class="sxs-lookup"><span data-stu-id="439d4-113">Rich JavaScript support with unobtrusive JavaScript, jQuery Validation, and JSON binding</span></span>
- <span data-ttu-id="439d4-114">*阅读[下面的](#overview)完整功能列表*</span><span class="sxs-lookup"><span data-stu-id="439d4-114">*Read the full feature list [below](#overview)*</span></span>

## <a name="top-links"></a><span data-ttu-id="439d4-115">热门链接</span><span class="sxs-lookup"><span data-stu-id="439d4-115">Top Links</span></span>

<span data-ttu-id="439d4-116">ASP.NET MVC 3 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="439d4-116">What's New in ASP.NET MVC 3</span></span>

- <span data-ttu-id="439d4-117">菲尔·哈克[：ASP.NET MVC 3 发布](http://haacked.com/archive/2011/01/13/aspnetmvc3-released.aspx)</span><span class="sxs-lookup"><span data-stu-id="439d4-117">Phil Haack: [ASP.NET MVC 3 Released](http://haacked.com/archive/2011/01/13/aspnetmvc3-released.aspx)</span></span>
- <span data-ttu-id="439d4-118">斯科特·汉塞尔曼[：ASP.NET MVC3、WebMatrix、NuGet、IIS 快递和果园发布 - 微软 1 月 Web 发布上下文](http://www.hanselman.com/blog/ASPNETMVC3WebMatrixNuGetIISExpressAndOrchardReleasedTheMicrosoftJanuaryWebReleaseInContext.aspx)</span><span class="sxs-lookup"><span data-stu-id="439d4-118">Scott Hanselman: [ASP.NET MVC3, WebMatrix, NuGet, IIS Express and Orchard released - The Microsoft January Web Release in Context](http://www.hanselman.com/blog/ASPNETMVC3WebMatrixNuGetIISExpressAndOrchardReleasedTheMicrosoftJanuaryWebReleaseInContext.aspx)</span></span>
- <span data-ttu-id="439d4-119">斯科特·古斯里：[宣布发布ASP.NET MVC 3，IIS 快递，SQL CE 4，网络农场框架，果园，WebMatrix](https://weblogs.asp.net/scottgu/archive/2011/01/13/announcing-release-of-asp-net-mvc-3-iis-express-sql-ce-4-web-farm-framework-orchard-webmatrix.aspx)</span><span class="sxs-lookup"><span data-stu-id="439d4-119">Scott Guthrie: [Announcing release of ASP.NET MVC 3, IIS Express, SQL CE 4, Web Farm Framework, Orchard, WebMatrix](https://weblogs.asp.net/scottgu/archive/2011/01/13/announcing-release-of-asp-net-mvc-3-iis-express-sql-ce-4-web-farm-framework-orchard-webmatrix.aspx)</span></span>
- [<span data-ttu-id="439d4-120">ASP.NET MVC 3 的发行说明</span><span class="sxs-lookup"><span data-stu-id="439d4-120">Release Notes for ASP.NET MVC 3</span></span>](../whitepapers/mvc3-release-notes.md)

<span data-ttu-id="439d4-121">安装和帮助</span><span class="sxs-lookup"><span data-stu-id="439d4-121">Installation and Help</span></span>

- <span data-ttu-id="439d4-122">使用 Web 平台安装程序安装ASP.NET MVC [3（建议）](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MVC3)</span><span class="sxs-lookup"><span data-stu-id="439d4-122">Install ASP.NET MVC 3 using the [Web Platform Installer (recommended)](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MVC3)</span></span>
- <span data-ttu-id="439d4-123">使用[安装程序可执行文件](https://go.microsoft.com/fwlink/?LinkID=208140)安装ASP.NET MVC 3</span><span class="sxs-lookup"><span data-stu-id="439d4-123">Install ASP.NET MVC 3 using the [installer executable](https://go.microsoft.com/fwlink/?LinkID=208140)</span></span>
- <span data-ttu-id="439d4-124">安装[ASP.NET MVC 3 用于可视化工作室 11 开发人员预览](https://go.microsoft.com/fwlink/?LinkID=208140)</span><span class="sxs-lookup"><span data-stu-id="439d4-124">Install [ASP.NET MVC 3 for Visual Studio 11 Developer Preview](https://go.microsoft.com/fwlink/?LinkID=208140)</span></span>
- <span data-ttu-id="439d4-125">阅读[简介以ASP.NET MVC 3 教程](overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)</span><span class="sxs-lookup"><span data-stu-id="439d4-125">Read the [Intro to ASP.NET MVC 3 tutorial](overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)</span></span>
- <span data-ttu-id="439d4-126">在[论坛](https://forums.asp.net/1146.aspx)中获取有关 MVC 3 ASP.NET帮助和讨论</span><span class="sxs-lookup"><span data-stu-id="439d4-126">Get help and discuss ASP.NET MVC 3 in the [forums](https://forums.asp.net/1146.aspx)</span></span>

<a id="overview"></a>
## <a name="aspnet-mvc-3-overview"></a><span data-ttu-id="439d4-127">ASP.NET MVC 3 Overview（ASP.NET MVC 3 概述）</span><span class="sxs-lookup"><span data-stu-id="439d4-127">ASP.NET MVC 3 Overview</span></span>

<span data-ttu-id="439d4-128">ASP.NET MVC 3 建立在 ASP.NET MVC 1 和 2 的基础上，增加了既简化了代码又允许更深度扩展性的伟大功能。</span><span class="sxs-lookup"><span data-stu-id="439d4-128">ASP.NET MVC 3 builds on ASP.NET MVC 1 and 2, adding great features that both simplify your code and allow deeper extensibility.</span></span> <span data-ttu-id="439d4-129">本主题概述了此版本中包括的许多新功能，这些功能分为以下各节：</span><span class="sxs-lookup"><span data-stu-id="439d4-129">This topic provides an overview of many of the new features that are included in this release, organized into the following sections:</span></span>

- [<span data-ttu-id="439d4-130">通过 Mvc Scaffold 集成扩展脚手架</span><span class="sxs-lookup"><span data-stu-id="439d4-130">Extensible Scaffolding with MvcScaffold integration</span></span>](#BM_MvcScaffolding)
- [<span data-ttu-id="439d4-131">启用 HTML 5 的项目模板</span><span class="sxs-lookup"><span data-stu-id="439d4-131">HTML 5 enabled project templates</span></span>](#BM_HTML5)
- [<span data-ttu-id="439d4-132">剃刀视图引擎</span><span class="sxs-lookup"><span data-stu-id="439d4-132">The Razor View Engine</span></span>](#BM_TheRazorViewEngine)
- [<span data-ttu-id="439d4-133">支持多视图引擎</span><span class="sxs-lookup"><span data-stu-id="439d4-133">Support for Multiple View Engines</span></span>](#BM_Support_for_Multiple_View_Engines)
- [<span data-ttu-id="439d4-134">控制器改进</span><span class="sxs-lookup"><span data-stu-id="439d4-134">Controller Improvements</span></span>](#BM_Controller_Improvements)
- [<span data-ttu-id="439d4-135">JavaScript 和 Ajax</span><span class="sxs-lookup"><span data-stu-id="439d4-135">JavaScript and Ajax</span></span>](#BM_JavaScript_and_Ajax_Improvements)
- [<span data-ttu-id="439d4-136">模型验证改进</span><span class="sxs-lookup"><span data-stu-id="439d4-136">Model Validation Improvements</span></span>](#BM_Model_Validation_Improvements)
- [<span data-ttu-id="439d4-137">依赖项注入改进</span><span class="sxs-lookup"><span data-stu-id="439d4-137">Dependency Injection Improvements</span></span>](#BM_Dependency_Injection_Improvements)
- [<span data-ttu-id="439d4-138">其他新功能</span><span class="sxs-lookup"><span data-stu-id="439d4-138">Other New Features</span></span>](#BM_Other_New_Features)

<a id="BM_MvcScaffolding"></a>

## <a name="extensible-scaffolding-with-mvcscaffold-integration"></a><span data-ttu-id="439d4-139">通过 Mvc Scaffold 集成扩展脚手架</span><span class="sxs-lookup"><span data-stu-id="439d4-139">Extensible Scaffolding with MvcScaffold integration</span></span>

<span data-ttu-id="439d4-140">新的 Scaffoldsing 系统使您能够更轻松地拿起并开始高效使用，如果您是框架的完全新，并且如果您经验丰富且已经知道正在做什么，则自动执行常见开发任务。</span><span class="sxs-lookup"><span data-stu-id="439d4-140">The new Scaffolding system makes it easier to pick up and start using productively if you're entirely new to the framework, and to automate common development tasks if you're experienced and already know what you're doing.</span></span>

<span data-ttu-id="439d4-141">这是由新的NuGet*脚手架*包支持，称为**Mvc脚手架**。</span><span class="sxs-lookup"><span data-stu-id="439d4-141">This is supported by new NuGet *scaffolding* package called **MvcScaffolding**.</span></span> <span data-ttu-id="439d4-142">许多软件技术使用术语"Scaffolding"表示"快速生成软件的基本大纲，然后您可以编辑和自定义"。</span><span class="sxs-lookup"><span data-stu-id="439d4-142">The term "Scaffolding" is used by many software technologies to mean "quickly generating a basic outline of your software that you can then edit and customize".</span></span> <span data-ttu-id="439d4-143">我们为ASP.NET MVC 创建的脚手架包在几个方案中非常有用：</span><span class="sxs-lookup"><span data-stu-id="439d4-143">The scaffolding package we're creating for ASP.NET MVC is greatly beneficial in several scenarios:</span></span>

- <span data-ttu-id="439d4-144">**如果你第一次学习ASP.NETMVC，** 因为它为您提供了一种快速的方式来获得一些有用的工作代码，然后你可以根据您的需要进行编辑和调整。</span><span class="sxs-lookup"><span data-stu-id="439d4-144">**If you're learning ASP.NET MVC for the first time**, because it gives you a fast way to get some useful, working code, that you can then edit and adapt according to your needs.</span></span> <span data-ttu-id="439d4-145">它为您从看着空白页面的创伤中拯救，并且不知道从哪里开始！</span><span class="sxs-lookup"><span data-stu-id="439d4-145">It saves you from the trauma of looking at a blank page and having no idea where to start!</span></span>
- <span data-ttu-id="439d4-146">**如果您对 MVC ASP.NET非常了解，并且正在探索一些新的附加技术**，如对象关系映射器、视图引擎、测试库等，因为该技术的创建者可能也为它创建了一个基架包。</span><span class="sxs-lookup"><span data-stu-id="439d4-146">**If you know ASP.NET MVC well and are now exploring some new add-on technology** such as an object-relational mapper, a view engine, a testing library, etc., because the creator of that technology may have also created a scaffolding package for it.</span></span>
- <span data-ttu-id="439d4-147">**如果工作涉及重复创建类似类或某种文件**，因为您可以创建自定义基架，以输出测试夹具、部署脚本或其他任何需要。</span><span class="sxs-lookup"><span data-stu-id="439d4-147">**If your work involves repeatedly creating similar classes or files of some sort**, because you can create custom scaffolders that output test fixtures, deployment scripts, or whatever else you need.</span></span> <span data-ttu-id="439d4-148">团队中的每个人都可以使用自定义脚手架。</span><span class="sxs-lookup"><span data-stu-id="439d4-148">Everyone on your team can use your custom scaffolders, too.</span></span>

<span data-ttu-id="439d4-149">MvcScaffoldsing 中的其他功能包括：</span><span class="sxs-lookup"><span data-stu-id="439d4-149">Other features in MvcScaffolding include:</span></span>

- <span data-ttu-id="439d4-150">支持 C# 和 VB 项目</span><span class="sxs-lookup"><span data-stu-id="439d4-150">Support for C# and VB projects</span></span>
- <span data-ttu-id="439d4-151">支持剃刀和 ASPX 视图引擎</span><span class="sxs-lookup"><span data-stu-id="439d4-151">Support for the Razor and ASPX view engines</span></span>
- <span data-ttu-id="439d4-152">支持将脚手架放入ASP.NET MVC 区域并使用自定义视图布局/主机</span><span class="sxs-lookup"><span data-stu-id="439d4-152">Supports scaffolding into ASP.NET MVC areas and using custom view layouts/masters</span></span>
- <span data-ttu-id="439d4-153">您可以通过编辑 T4 模板轻松自定义输出</span><span class="sxs-lookup"><span data-stu-id="439d4-153">You can easily customize the output by editing T4 templates</span></span>
- <span data-ttu-id="439d4-154">您可以使用自定义 PowerShell 逻辑和自定义 T4 模板添加全新的基架。</span><span class="sxs-lookup"><span data-stu-id="439d4-154">You can add entirely new scaffolders using custom PowerShell logic and custom T4 templates.</span></span> <span data-ttu-id="439d4-155">这些参数（以及您提供给它们的任何自定义参数）会自动显示在控制台选项卡完成列表中。</span><span class="sxs-lookup"><span data-stu-id="439d4-155">These (and any custom parameters you've given them) automatically appear in the console tab-completion list.</span></span>
- <span data-ttu-id="439d4-156">您可以获取包含不同技术的其他基架支架的 NuGet 包（例如，现在 LINQ 到 SQL 都有一个概念验证包），并将它们混合并匹配在一起</span><span class="sxs-lookup"><span data-stu-id="439d4-156">You can get NuGet packages containing additional scaffolders for different technologies (e.g., there's a proof-of-concept one for LINQ to SQL now) and mix and match them together</span></span>

<span data-ttu-id="439d4-157">ASP.NET MVC 3 工具更新包括针对此基架系统的巨大 Visual Studio 支持，例如：</span><span class="sxs-lookup"><span data-stu-id="439d4-157">The ASP.NET MVC 3 Tools Update includes great Visual Studio support for this scaffolding system, such as:</span></span>

- <span data-ttu-id="439d4-158">添加控制器对话框现在支持创建、读取、更新和删除控制器操作和相应视图的完整自动基架。</span><span class="sxs-lookup"><span data-stu-id="439d4-158">Add Controller Dialog now supports full automatic scaffolding of Create, Read, Update, and Delete controller actions and corresponding views.</span></span> <span data-ttu-id="439d4-159">默认情况下，此基架数据访问代码使用 EF 代码优先。</span><span class="sxs-lookup"><span data-stu-id="439d4-159">By default, this scaffolds data access code using EF Code First.</span></span>
- <span data-ttu-id="439d4-160">添加控制器对话框支持通过 NuGet 包（如*MvcScaffold）\*\*进行扩展基架*。</span><span class="sxs-lookup"><span data-stu-id="439d4-160">Add Controller Dialog supports *extensible scaffolds* via NuGet packages such as *MvcScaffolding*.</span></span> <span data-ttu-id="439d4-161">这允许将自定义基架插入对话框中，这样，如果您倾向于的话，您可以为其他数据访问技术（如 NHibernate）创建基架，甚至使用 ODBCDirect 的 JET！</span><span class="sxs-lookup"><span data-stu-id="439d4-161">This allows plugging in custom scaffolds into the dialog which would allow you to create scaffolds for other data access technologies such as NHibernate or even JET with ODBCDirect if you're so inclined!</span></span>

<span data-ttu-id="439d4-162">有关 ASP.NET MVC 3 中的基架的详细信息，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="439d4-162">For more information about Scaffolding in ASP.NET MVC 3, see the following resources:</span></span>

- <span data-ttu-id="439d4-163">史蒂夫·桑德森的系列帖子，包括：</span><span class="sxs-lookup"><span data-stu-id="439d4-163">Steve Sanderson's post series, including:</span></span> 

    1. [<span data-ttu-id="439d4-164">简介： 使用 MvcScaffoldss 封装，ASP.NET MVC 3 项目脚手架</span><span class="sxs-lookup"><span data-stu-id="439d4-164">Introduction: Scaffold your ASP.NET MVC 3 project with the MvcScaffolding package</span></span>](http://blog.stevensanderson.com/2011/01/13/scaffold-your-aspnet-mvc-3-project-with-the-mvcscaffolding-package/)
    2. [<span data-ttu-id="439d4-165">标准用法：典型用例和选项</span><span class="sxs-lookup"><span data-stu-id="439d4-165">Standard usage: Typical use cases and options</span></span>](http://blog.stevensanderson.com/2011/01/13/mvcscaffolding-standard-usage/)
    3. [<span data-ttu-id="439d4-166">一对多关系</span><span class="sxs-lookup"><span data-stu-id="439d4-166">One-to-Many Relationships</span></span>](http://blog.stevensanderson.com/2011/01/28/mvcscaffolding-one-to-many-relationships/)
    4. [<span data-ttu-id="439d4-167">脚手架操作和单元测试</span><span class="sxs-lookup"><span data-stu-id="439d4-167">Scaffolding Actions and Unit Tests</span></span>](http://blog.stevensanderson.com/2011/03/28/scaffolding-actions-and-unit-tests-with-mvcscaffolding/)
    5. [<span data-ttu-id="439d4-168">覆盖 T4 模板</span><span class="sxs-lookup"><span data-stu-id="439d4-168">Overriding the T4 templates</span></span>](http://blog.stevensanderson.com/2011/04/06/mvcscaffolding-overriding-the-t4-templates/)
    6. [<span data-ttu-id="439d4-169">这篇文章：创建自定义脚手架</span><span class="sxs-lookup"><span data-stu-id="439d4-169">This post: Creating custom scaffolders</span></span>](http://blog.stevensanderson.com/2011/04/07/mvcscaffolding-creating-custom-scaffolders/)
- <span data-ttu-id="439d4-170">斯科特·汉塞尔曼的帖子从他的PDC 2010会话[建立博客与微软"未命名的网络爱包"](http://www.hanselman.com/blog/PDC10BuildingABlogWithMicrosoftUnnamedPackageOfWebLove.aspx)</span><span class="sxs-lookup"><span data-stu-id="439d4-170">Scott Hanselman's post from his PDC 2010 session [Building a Blog with Microsoft "Unnamed Package of Web Love"](http://www.hanselman.com/blog/PDC10BuildingABlogWithMicrosoftUnnamedPackageOfWebLove.aspx)</span></span>
- [<span data-ttu-id="439d4-171">MVC 3 发行说明</span><span class="sxs-lookup"><span data-stu-id="439d4-171">MVC 3 Release Notes</span></span>](../whitepapers/mvc3-release-notes.md)

<a id="BM_HTML5"></a>

## <a name="html-5-project-templates"></a><span data-ttu-id="439d4-172">HTML 5 项目模板</span><span class="sxs-lookup"><span data-stu-id="439d4-172">HTML 5 Project Templates</span></span>

<span data-ttu-id="439d4-173">"新项目"对话框包括一个复选框，该复选框启用 HTML 5 版本的项目模板。</span><span class="sxs-lookup"><span data-stu-id="439d4-173">The New Project dialog includes a checkbox enable HTML 5 versions of project templates.</span></span> <span data-ttu-id="439d4-174">这些模板利用 Modernizr 1.7 在低级浏览器中为 HTML 5 和 CSS 3 提供兼容性支持。</span><span class="sxs-lookup"><span data-stu-id="439d4-174">These templates leverage Modernizr 1.7 to provide compatibility support for HTML 5 and CSS 3 in down-level browsers.</span></span>

<a id="BM_TheRazorViewEngine"></a>

## <a name="the-razor-view-engine"></a><span data-ttu-id="439d4-175">剃刀视图引擎</span><span class="sxs-lookup"><span data-stu-id="439d4-175">The Razor View Engine</span></span>

<span data-ttu-id="439d4-176">ASP.NET MVC 3 附带了名为 Razor 的新视图引擎，具有以下优点：</span><span class="sxs-lookup"><span data-stu-id="439d4-176">ASP.NET MVC 3 comes with a new view engine named Razor that offers the following benefits:</span></span>

- <span data-ttu-id="439d4-177">剃刀语法简洁简洁，需要最少的击键次数。</span><span class="sxs-lookup"><span data-stu-id="439d4-177">Razor syntax is clean and concise, requiring a minimum number of keystrokes.</span></span>
- <span data-ttu-id="439d4-178">Razor 易于学习，部分原因在于它基于现有语言（如 C# 和 Visual Basic）。</span><span class="sxs-lookup"><span data-stu-id="439d4-178">Razor is easy to learn, in part because it's based on existing languages like C# and Visual Basic.</span></span>
- <span data-ttu-id="439d4-179">可视化工作室包括用于 Razor 语法的 IntelliSense 和代码着色。</span><span class="sxs-lookup"><span data-stu-id="439d4-179">Visual Studio includes IntelliSense and code colorization for Razor syntax.</span></span>
- <span data-ttu-id="439d4-180">Razor 视图可以进行单元测试，而无需运行应用程序或启动 Web 服务器。</span><span class="sxs-lookup"><span data-stu-id="439d4-180">Razor views can be unit tested without requiring that you run the application or launch a web server.</span></span>

<span data-ttu-id="439d4-181">一些新的 Razor 功能包括：</span><span class="sxs-lookup"><span data-stu-id="439d4-181">Some new Razor features include the following:</span></span>

- <span data-ttu-id="439d4-182">`@model`用于指定传递给视图的类型的语法。</span><span class="sxs-lookup"><span data-stu-id="439d4-182">`@model` syntax for specifying the type being passed to the view.</span></span>
- <span data-ttu-id="439d4-183">`@* *@`注释语法。</span><span class="sxs-lookup"><span data-stu-id="439d4-183">`@* *@` comment syntax.</span></span>
- <span data-ttu-id="439d4-184">为整个站点指定默认值（如`layoutpage`） 一次的能力。</span><span class="sxs-lookup"><span data-stu-id="439d4-184">The ability to specify defaults (such as `layoutpage`) once for an entire site.</span></span>
- <span data-ttu-id="439d4-185">显示`Html.Raw`文本而不进行 HTML 编码的方法。</span><span class="sxs-lookup"><span data-stu-id="439d4-185">The `Html.Raw` method for displaying text without HTML-encoding it.</span></span>
- <span data-ttu-id="439d4-186">支持在多个视图之间共享代码（*\_视图 start.cshtml*或*\_viewstart.vbhtml*文件）。</span><span class="sxs-lookup"><span data-stu-id="439d4-186">Support for sharing code among multiple views (*\_viewstart.cshtml* or *\_viewstart.vbhtml* files).</span></span>

<span data-ttu-id="439d4-187">Razor 还包括新的 HTML 帮助器，如下所示：</span><span class="sxs-lookup"><span data-stu-id="439d4-187">Razor also includes  new HTML helpers, such as the following:</span></span>

- <span data-ttu-id="439d4-188">`Chart`.</span><span class="sxs-lookup"><span data-stu-id="439d4-188">`Chart`.</span></span> <span data-ttu-id="439d4-189">渲染图表，提供与 ASP.NET 4 中的图表控件相同的要素。</span><span class="sxs-lookup"><span data-stu-id="439d4-189">Renders a chart, offering the same features as the chart control in ASP.NET 4.</span></span>
- <span data-ttu-id="439d4-190">`WebGrid`.</span><span class="sxs-lookup"><span data-stu-id="439d4-190">`WebGrid`.</span></span> <span data-ttu-id="439d4-191">渲染数据网格，完成分页和排序功能。</span><span class="sxs-lookup"><span data-stu-id="439d4-191">Renders a data grid, complete with paging and sorting functionality.</span></span>
- <span data-ttu-id="439d4-192">`Crypto`.</span><span class="sxs-lookup"><span data-stu-id="439d4-192">`Crypto`.</span></span> <span data-ttu-id="439d4-193">使用哈希算法创建正确加盐和哈希密码。</span><span class="sxs-lookup"><span data-stu-id="439d4-193">Uses hashing algorithms to create properly salted and hashed passwords.</span></span>
- <span data-ttu-id="439d4-194">`WebImage`.</span><span class="sxs-lookup"><span data-stu-id="439d4-194">`WebImage`.</span></span> <span data-ttu-id="439d4-195">渲染图像。</span><span class="sxs-lookup"><span data-stu-id="439d4-195">Renders an image.</span></span>
- <span data-ttu-id="439d4-196">`WebMail`.</span><span class="sxs-lookup"><span data-stu-id="439d4-196">`WebMail`.</span></span> <span data-ttu-id="439d4-197">发送电子邮件。</span><span class="sxs-lookup"><span data-stu-id="439d4-197">Sends an email message.</span></span>

<span data-ttu-id="439d4-198">有关 Razor 的详细信息，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="439d4-198">For more information about Razor, see the following resources:</span></span>

- [<span data-ttu-id="439d4-199">斯科特·古斯里的博客文章介绍剃刀</span><span class="sxs-lookup"><span data-stu-id="439d4-199">Scott Guthrie's blog post introducing Razor</span></span>](https://weblogs.asp.net/scottgu/archive/2010/07/02/introducing-razor.aspx)
- [<span data-ttu-id="439d4-200">斯科特·古斯里的博客文章介绍关键字@model</span><span class="sxs-lookup"><span data-stu-id="439d4-200">Scott Guthrie's blog post introducing the @model keyword</span></span>](https://weblogs.asp.net/scottgu/archive/2010/10/19/asp-net-mvc-3-new-model-directive-support-in-razor.aspx)
- [<span data-ttu-id="439d4-201">斯科特·古斯里的博客文章介绍剃刀布局</span><span class="sxs-lookup"><span data-stu-id="439d4-201">Scott Guthrie's blog post introducing Razor layouts</span></span>](https://weblogs.asp.net/scottgu/archive/2010/10/22/asp-net-mvc-3-layouts.aspx)
- [<span data-ttu-id="439d4-202">剃刀 API 快速参考</span><span class="sxs-lookup"><span data-stu-id="439d4-202">Razor API Quick Reference</span></span>](../web-pages/overview/api-reference/asp-net-web-pages-api-reference.md)
- [<span data-ttu-id="439d4-203">MVC 3 发行说明</span><span class="sxs-lookup"><span data-stu-id="439d4-203">MVC 3 Release Notes</span></span>](../whitepapers/mvc3-release-notes.md)

<a id="BM_Support_for_Multiple_View_Engines"></a>

## <a name="support-for-multiple-view-engines"></a><span data-ttu-id="439d4-204">支持多视图引擎</span><span class="sxs-lookup"><span data-stu-id="439d4-204">Support for Multiple View Engines</span></span>

<span data-ttu-id="439d4-205">ASP.NET MVC 3 中的 **"添加视图"** 对话框允许您选择要使用的视图引擎，而 **"新项目**"对话框允许您为项目指定默认视图引擎。</span><span class="sxs-lookup"><span data-stu-id="439d4-205">The **Add View** dialog box in ASP.NET MVC 3 lets you choose the view engine you want to work with, and the **New Project** dialog box lets you specify the default view engine for a project.</span></span> <span data-ttu-id="439d4-206">您可以选择 Web 窗体视图引擎 （ASPX）、Razor 或开源视图引擎（如[Spark、NHaml](https://code.google.com/p/nhaml/)或[Spark](http://sparkviewengine.com/)[NDjango）。](http://ndjango.org/)</span><span class="sxs-lookup"><span data-stu-id="439d4-206">You can choose the Web Forms view engine (ASPX), Razor, or an open-source view engine such as [Spark](http://sparkviewengine.com/), [NHaml](https://code.google.com/p/nhaml/), or [NDjango](http://ndjango.org/).</span></span>

<a id="BM_Controller_Improvements"></a>

## <a name="controller-improvements"></a><span data-ttu-id="439d4-207">控制器改进</span><span class="sxs-lookup"><span data-stu-id="439d4-207">Controller Improvements</span></span>

### <a name="global-action-filters"></a><span data-ttu-id="439d4-208">全局操作筛选器</span><span class="sxs-lookup"><span data-stu-id="439d4-208">Global Action Filters</span></span>

<span data-ttu-id="439d4-209">有时，您希望在操作方法运行之前或操作方法运行之前执行逻辑。</span><span class="sxs-lookup"><span data-stu-id="439d4-209">Sometimes you want to perform logic either before an action method runs or after an action method runs.</span></span> <span data-ttu-id="439d4-210">为了支持这一点，ASP.NET MVC 2 提供了操作筛选器。</span><span class="sxs-lookup"><span data-stu-id="439d4-210">To support this, ASP.NET MVC 2 provided action filters.</span></span> <span data-ttu-id="439d4-211">操作筛选器是自定义属性，提供声明性方法，将操作前和操作后行为添加到特定的控制器操作方法。</span><span class="sxs-lookup"><span data-stu-id="439d4-211">Action filters are custom attributes that provide a declarative means to add pre-action and post-action behavior to specific controller action methods.</span></span> <span data-ttu-id="439d4-212">但是，在某些情况下，您可能希望指定适用于所有操作方法的操作前或行动后行为。</span><span class="sxs-lookup"><span data-stu-id="439d4-212">However, in some cases you might want to specify pre-action or post-action behavior that applies to all action methods.</span></span> <span data-ttu-id="439d4-213">MVC 3 允许您通过将全局筛选器添加到`GlobalFilters`集合来指定全局筛选器。</span><span class="sxs-lookup"><span data-stu-id="439d4-213">MVC 3 lets you specify global filters by adding them to the `GlobalFilters` collection.</span></span> <span data-ttu-id="439d4-214">有关全局操作筛选器的详细信息，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="439d4-214">For more information about global action filters, see the following resources:</span></span>

- [<span data-ttu-id="439d4-215">斯科特·古斯里在MVC 3预览的博客</span><span class="sxs-lookup"><span data-stu-id="439d4-215">Scott Guthrie's blog on the MVC 3 Preview</span></span>](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx)
- <span data-ttu-id="439d4-216">[ASP.NET MVC 中的筛选](https://msdn.microsoft.com/library/gg416513(VS.98).aspx)</span><span class="sxs-lookup"><span data-stu-id="439d4-216">[Filtering in ASP.NET MVC](https://msdn.microsoft.com/library/gg416513(VS.98).aspx)</span></span>

### <a name="new-viewbag-property"></a><span data-ttu-id="439d4-217">新的"视图袋"属性</span><span class="sxs-lookup"><span data-stu-id="439d4-217">New "ViewBag" Property</span></span>

<span data-ttu-id="439d4-218">MVC 2 控制器`ViewData`支持一个属性，该属性使您能够使用后期绑定字典 API 将数据传递到视图模板。</span><span class="sxs-lookup"><span data-stu-id="439d4-218">MVC 2 controllers support a `ViewData` property that enables you to pass data to a view template using a late-bound dictionary API.</span></span> <span data-ttu-id="439d4-219">在 MVC 3 中，还可以对属性使用更简单`ViewBag`的语法来实现相同的目的。</span><span class="sxs-lookup"><span data-stu-id="439d4-219">In MVC 3, you can also use somewhat simpler syntax with the `ViewBag` property to accomplish the same purpose.</span></span> <span data-ttu-id="439d4-220">例如，可以写入 而不是`ViewData["Message"]="text"`写入`ViewBag.Message="text"`。</span><span class="sxs-lookup"><span data-stu-id="439d4-220">For example, instead of writing `ViewData["Message"]="text"`, you can write `ViewBag.Message="text"`.</span></span> <span data-ttu-id="439d4-221">不需要定义任何强类型类来使用 属性`ViewBag`。</span><span class="sxs-lookup"><span data-stu-id="439d4-221">You do not need to define any strongly-typed classes to use the `ViewBag` property.</span></span> <span data-ttu-id="439d4-222">因为它是动态属性，因此只需获取或设置属性，它将在运行时动态解析它们。</span><span class="sxs-lookup"><span data-stu-id="439d4-222">Because it is a dynamic property, you can instead just get or set properties and it will resolve them dynamically at run time.</span></span> <span data-ttu-id="439d4-223">在内部`ViewBag`，属性在`ViewData`字典中存储为名称/值对。</span><span class="sxs-lookup"><span data-stu-id="439d4-223">Internally, `ViewBag` properties are stored as name/value pairs in the `ViewData` dictionary.</span></span> <span data-ttu-id="439d4-224">（注意：在大多数预发行版本的 MVC 3 中，`ViewBag`属性被命名为属性`ViewModel`。</span><span class="sxs-lookup"><span data-stu-id="439d4-224">(Note: in most pre-release versions of MVC 3, the `ViewBag` property was named the `ViewModel` property.)</span></span>

### <a name="new-actionresult-types"></a><span data-ttu-id="439d4-225">新的"操作结果"类型</span><span class="sxs-lookup"><span data-stu-id="439d4-225">New "ActionResult" Types</span></span>

<span data-ttu-id="439d4-226">以下`ActionResult`类型和相应的帮助器方法在 MVC 3 中是新的或增强的：</span><span class="sxs-lookup"><span data-stu-id="439d4-226">The following `ActionResult` types and corresponding helper methods are new or enhanced in MVC 3:</span></span>

- <span data-ttu-id="439d4-227">[HttpNotFoundResult](https://msdn.microsoft.com/library/system.web.mvc.httpnotfoundresult(v=vs.98).aspx)。</span><span class="sxs-lookup"><span data-stu-id="439d4-227">[HttpNotFoundResult](https://msdn.microsoft.com/library/system.web.mvc.httpnotfoundresult(v=vs.98).aspx).</span></span> <span data-ttu-id="439d4-228">将 404 HTTP 状态代码返回给客户端。</span><span class="sxs-lookup"><span data-stu-id="439d4-228">Returns a 404 HTTP status code to the client.</span></span>
- <span data-ttu-id="439d4-229">[重定向结果](https://msdn.microsoft.com/library/system.web.mvc.redirectresult(v=VS.98).aspx)。</span><span class="sxs-lookup"><span data-stu-id="439d4-229">[RedirectResult](https://msdn.microsoft.com/library/system.web.mvc.redirectresult(v=VS.98).aspx).</span></span> <span data-ttu-id="439d4-230">返回临时重定向 （HTTP 302 状态代码） 或永久重定向 （HTTP 301 状态代码），具体取决于布尔参数。</span><span class="sxs-lookup"><span data-stu-id="439d4-230">Returns a temporary redirect (HTTP 302 status code) or a permanent redirect (HTTP 301 status code), depending on a Boolean parameter.</span></span> <span data-ttu-id="439d4-231">结合此更改[，Controller](https://msdn.microsoft.com/library/system.web.mvc.controller(v=VS.98).aspx)类现在有三种执行永久重定向的方法：、`RedirectPermanent``RedirectToRoutePermanent`和`RedirectToActionPermanent`。</span><span class="sxs-lookup"><span data-stu-id="439d4-231">In conjunction with this change, the [Controller](https://msdn.microsoft.com/library/system.web.mvc.controller(v=VS.98).aspx) class now has three methods for performing permanent redirects: `RedirectPermanent`, `RedirectToRoutePermanent`, and `RedirectToActionPermanent`.</span></span> <span data-ttu-id="439d4-232">这些方法返回`RedirectResult`属性`Permanent`设置为`true`的 实例。</span><span class="sxs-lookup"><span data-stu-id="439d4-232">These methods return an instance of `RedirectResult` with the `Permanent` property set to `true`.</span></span>
- <span data-ttu-id="439d4-233">[HttpStatusCodeResult](https://msdn.microsoft.com/library/system.web.mvc.httpstatuscoderesult(v=VS.98).aspx).</span><span class="sxs-lookup"><span data-stu-id="439d4-233">[HttpStatusCodeResult](https://msdn.microsoft.com/library/system.web.mvc.httpstatuscoderesult(v=VS.98).aspx).</span></span> <span data-ttu-id="439d4-234">返回用户指定的 HTTP 状态代码。</span><span class="sxs-lookup"><span data-stu-id="439d4-234">Returns a user-specified HTTP status code.</span></span>

<a id="BM_JavaScript_and_Ajax_Improvements"></a>

## <a name="javascript-and-ajax-improvements"></a><span data-ttu-id="439d4-235">JavaScript 和 Ajax 改进</span><span class="sxs-lookup"><span data-stu-id="439d4-235">JavaScript and Ajax Improvements</span></span>

<span data-ttu-id="439d4-236">默认情况下，MVC 3 中的 Ajax 和验证帮助程序使用不显眼的 JavaScript 方法。</span><span class="sxs-lookup"><span data-stu-id="439d4-236">By default, Ajax and validation helpers in MVC 3 use an unobtrusive JavaScript approach.</span></span> <span data-ttu-id="439d4-237">不显眼的 JavaScript 避免将内联 JavaScript 注入 HTML。</span><span class="sxs-lookup"><span data-stu-id="439d4-237">Unobtrusive JavaScript avoids injecting inline JavaScript into HTML.</span></span> <span data-ttu-id="439d4-238">这使得您的 HTML 更小且不太混乱，并且更易于交换或自定义 JavaScript 库。</span><span class="sxs-lookup"><span data-stu-id="439d4-238">This makes your HTML smaller and less cluttered, and makes it easier to swap out or customize JavaScript libraries.</span></span> <span data-ttu-id="439d4-239">默认情况下，MVC `jQueryValidate` 3 中的验证帮助程序也使用该插件。</span><span class="sxs-lookup"><span data-stu-id="439d4-239">Validation helpers in MVC 3 also use the `jQueryValidate` plugin by default.</span></span> <span data-ttu-id="439d4-240">如果需要 MVC 2 行为，可以使用*Web.config*文件设置禁用不显眼的 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="439d4-240">If you want MVC 2 behavior, you can disable unobtrusive JavaScript using a *web.config* file setting.</span></span> <span data-ttu-id="439d4-241">有关 JavaScript 和 Ajax 改进的详细信息，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="439d4-241">For more information about JavaScript and Ajax improvements, see the following resources:</span></span>

- [<span data-ttu-id="439d4-242">维基百科网站上不显眼的JavaScript的基本介绍</span><span class="sxs-lookup"><span data-stu-id="439d4-242">Basic introduction to unobtrusive JavaScript on the Wikipedia site</span></span>](http://en.wikipedia.org/wiki/Unobtrusive_JavaScript)
- [<span data-ttu-id="439d4-243">布拉德·威尔逊的《不显眼的JavaScript》帖子</span><span class="sxs-lookup"><span data-stu-id="439d4-243">Brad Wilson's Unobtrusive JavaScript Post</span></span>](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-ajax.html)
- [<span data-ttu-id="439d4-244">布拉德·威尔逊的《不显眼的Java脚本验证帖》</span><span class="sxs-lookup"><span data-stu-id="439d4-244">Brad Wilson's Unobtrusive JavaScript Validation Post</span></span>](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html)
- <span data-ttu-id="439d4-245">[使用 Razor 和不显眼的 JavaScript 创建 MVC 3 应用程序](overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript.md)（ASP.NET网站上的教程）</span><span class="sxs-lookup"><span data-stu-id="439d4-245">[Creating a MVC 3 Application with Razor and Unobtrusive JavaScript](overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript.md) (tutorial on the ASP.NET site)</span></span>
- [<span data-ttu-id="439d4-246">MVC 3 发行说明</span><span class="sxs-lookup"><span data-stu-id="439d4-246">MVC 3 Release Notes</span></span>](../whitepapers/mvc3-release-notes.md)

### <a name="client-side-validation-enabled-by-default"></a><span data-ttu-id="439d4-247">默认情况下启用客户端验证</span><span class="sxs-lookup"><span data-stu-id="439d4-247">Client-Side Validation Enabled by Default</span></span>

<span data-ttu-id="439d4-248">在早期版本的 MVC 中，需要从视图中显式调用`Html.EnableClientValidation`方法，以便启用客户端验证。</span><span class="sxs-lookup"><span data-stu-id="439d4-248">In earlier versions of MVC, you need to explicitly call the `Html.EnableClientValidation` method from a view in order to enable client-side validation.</span></span> <span data-ttu-id="439d4-249">在 MVC 3 中，这不再需要，因为默认情况下启用客户端验证。</span><span class="sxs-lookup"><span data-stu-id="439d4-249">In MVC 3 this is no longer required because client-side validation is enabled by default.</span></span> <span data-ttu-id="439d4-250">（您可以使用*Web.config*文件中的设置禁用此功能。</span><span class="sxs-lookup"><span data-stu-id="439d4-250">(You can disable this using a setting in the *web.config* file.)</span></span>

<span data-ttu-id="439d4-251">为了使客户端验证正常工作，您仍然需要引用站点中相应的 jQuery 和 jQuery 验证库。</span><span class="sxs-lookup"><span data-stu-id="439d4-251">In order for client-side validation to work, you still need to reference the appropriate jQuery and jQuery Validation libraries in your site.</span></span> <span data-ttu-id="439d4-252">您可以在自己的服务器上托管这些库，也可以从内容交付网络 （CDN）（如 Microsoft 或 Google 的 CDN）中引用它们。</span><span class="sxs-lookup"><span data-stu-id="439d4-252">You can host those libraries on your own server or reference them from a content delivery network (CDN) like the CDNs from Microsoft or Google.</span></span>

### <a name="remote-validator"></a><span data-ttu-id="439d4-253">远程验证器</span><span class="sxs-lookup"><span data-stu-id="439d4-253">Remote Validator</span></span>

<span data-ttu-id="439d4-254">ASP.NET MVC 3 支持新的[RemoteAttribute](https://msdn.microsoft.com/library/system.web.mvc.remoteattribute(v=VS.98).aspx)类，使您能够利用 jQuery 验证插件的远程验证器支持。</span><span class="sxs-lookup"><span data-stu-id="439d4-254">ASP.NET MVC 3 supports the new [RemoteAttribute](https://msdn.microsoft.com/library/system.web.mvc.remoteattribute(v=VS.98).aspx) class that enables you to take advantage of the jQuery Validation plug-in's remote validator support.</span></span> <span data-ttu-id="439d4-255">这使客户端验证库能够自动调用您在服务器上定义的自定义方法，以便执行只能执行服务器端的验证逻辑。</span><span class="sxs-lookup"><span data-stu-id="439d4-255">This enables the client-side validation library to automatically call a custom method that you define on the server in order to perform validation logic that can only be done server-side.</span></span>

<span data-ttu-id="439d4-256">`Remote`在下面的示例中，该属性指定客户端验证将调用`UserNameAvailable``UsersController`类上命名的操作以验证该`UserName`字段。</span><span class="sxs-lookup"><span data-stu-id="439d4-256">In the following example, the `Remote` attribute specifies that client validation will call an action named `UserNameAvailable` on the `UsersController` class in order to validate the `UserName` field.</span></span>

[!code-csharp[Main](mvc3/samples/sample1.cs)]

<span data-ttu-id="439d4-257">下面的示例显示了相应的控制器。</span><span class="sxs-lookup"><span data-stu-id="439d4-257">The following example shows the corresponding controller.</span></span>

[!code-csharp[Main](mvc3/samples/sample2.cs)]

<span data-ttu-id="439d4-258">有关如何使用`Remote`该属性的详细信息，请参阅如何：在 MSDN 库中[ASP.NET MVC 中实现远程验证](https://msdn.microsoft.com/library/gg508808(VS.98).aspx)。</span><span class="sxs-lookup"><span data-stu-id="439d4-258">For more information about how to use the `Remote` attribute, see [How to: Implement Remote Validation in ASP.NET MVC](https://msdn.microsoft.com/library/gg508808(VS.98).aspx) in the MSDN library.</span></span>

### <a name="json-binding-support"></a><span data-ttu-id="439d4-259">JSON 绑定支持</span><span class="sxs-lookup"><span data-stu-id="439d4-259">JSON Binding Support</span></span>

<span data-ttu-id="439d4-260">ASP.NET MVC 3 包括内置的 JSON 绑定支持，使操作方法能够接收 JSON 编码的数据，并将其模型绑定到操作方法参数。</span><span class="sxs-lookup"><span data-stu-id="439d4-260">ASP.NET MVC 3 includes built-in JSON binding support that enables action methods to receive JSON-encoded data and model-bind it to action-method parameters.</span></span> <span data-ttu-id="439d4-261">此功能在涉及客户端模板和数据绑定的方案中非常有用。</span><span class="sxs-lookup"><span data-stu-id="439d4-261">This capability is useful in scenarios involving client templates and data binding.</span></span> <span data-ttu-id="439d4-262">（客户端模板使您能够使用在客户端上执行的模板格式化和显示单个数据项或数据项集。MVC 3 使您能够轻松地将客户端模板与发送和接收 JSON 数据的服务器上的操作方法连接。</span><span class="sxs-lookup"><span data-stu-id="439d4-262">(Client templates enable you to format and display a single data item or set of data items by using templates that execute on the client.) MVC 3 enables you to easily connect client templates with action methods on the server that send and receive JSON data.</span></span> <span data-ttu-id="439d4-263">有关 JSON 绑定支持的详细信息，请参阅[Scott Guthrie 的 MVC 3 预览博客文章的](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx) **JavaScript 和 AJAX 改进**部分。</span><span class="sxs-lookup"><span data-stu-id="439d4-263">For more information about JSON binding support, see the **JavaScript and AJAX Improvements** section of [Scott Guthrie's MVC 3 Preview blog post](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx).</span></span>

<a id="BM_Model_Validation_Improvements"></a>

## <a name="model-validation-improvements"></a><span data-ttu-id="439d4-264">模型验证改进</span><span class="sxs-lookup"><span data-stu-id="439d4-264">Model Validation Improvements</span></span>

### <a name="dataannotations-metadata-attributes"></a><span data-ttu-id="439d4-265">"数据注释"元数据属性</span><span class="sxs-lookup"><span data-stu-id="439d4-265">"DataAnnotations" Metadata Attributes</span></span>

<span data-ttu-id="439d4-266">ASP.NET MVC `DataAnnotations` 3 支持元数据`DisplayAttribute`属性，如 。</span><span class="sxs-lookup"><span data-stu-id="439d4-266">ASP.NET MVC 3 supports `DataAnnotations` metadata attributes such as `DisplayAttribute`.</span></span>

### <a name="validationattribute-class"></a><span data-ttu-id="439d4-267">"验证属性"类</span><span class="sxs-lookup"><span data-stu-id="439d4-267">"ValidationAttribute" Class</span></span>

<span data-ttu-id="439d4-268">在`ValidationAttribute`.NET 框架 4 中改进了该类`IsValid`，以支持新的重载，该重载提供有关当前验证上下文的详细信息，例如正在验证的对象。</span><span class="sxs-lookup"><span data-stu-id="439d4-268">The `ValidationAttribute` class was improved in the .NET Framework 4 to support a new `IsValid` overload that provides more information about the current validation context, such as what object is being validated.</span></span> <span data-ttu-id="439d4-269">这支持更丰富的方案，您可以在其中根据模型的另一个属性验证当前值。</span><span class="sxs-lookup"><span data-stu-id="439d4-269">This enables richer scenarios where you can validate the current value based on another property of the model.</span></span> <span data-ttu-id="439d4-270">例如，新`CompareAttribute`属性允许您比较模型的两个属性的值。</span><span class="sxs-lookup"><span data-stu-id="439d4-270">For example, the new `CompareAttribute` attribute lets you compare the values of two properties of a model.</span></span> <span data-ttu-id="439d4-271">在下面的示例中，`ComparePassword`属性必须匹配`Password`该字段才能有效。</span><span class="sxs-lookup"><span data-stu-id="439d4-271">In the following example, the `ComparePassword` property must match the `Password` field in order to be valid.</span></span>

[!code-csharp[Main](mvc3/samples/sample3.cs)]

### <a name="validation-interfaces"></a><span data-ttu-id="439d4-272">验证接口</span><span class="sxs-lookup"><span data-stu-id="439d4-272">Validation Interfaces</span></span>

<span data-ttu-id="439d4-273">[IValidaobject 接口](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.ivalidatableobject.aspx)使您能够执行模型级验证，并且它使您能够提供特定于整个模型状态的验证错误消息，或在模型中的两个属性之间。</span><span class="sxs-lookup"><span data-stu-id="439d4-273">The [IValidatableObject](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.ivalidatableobject.aspx) interface enables you to perform model-level validation, and it enables you to provide validation error messages that are specific to the state of the overall model, or between two properties within the model.</span></span> <span data-ttu-id="439d4-274">MVC 3 现在从`IValidatableObject`模型绑定时从接口检索错误，并使用内置的 HTML 表单帮助器自动标记或突出显示视图中受影响的字段。</span><span class="sxs-lookup"><span data-stu-id="439d4-274">MVC 3 now retrieves errors from the `IValidatableObject` interface when model binding, and automatically flags or highlights affected fields within a view using the built-in HTML form helpers.</span></span>

<span data-ttu-id="439d4-275">[IClientValidaa 可界面](https://msdn.microsoft.com/library/system.web.mvc.iclientvalidatable(v=VS.98).aspx)使ASP.NET MVC 能够在运行时发现验证器是否支持客户端验证。</span><span class="sxs-lookup"><span data-stu-id="439d4-275">The [IClientValidatable](https://msdn.microsoft.com/library/system.web.mvc.iclientvalidatable(v=VS.98).aspx) interface enables ASP.NET MVC to discover at run time whether a validator has support for client validation.</span></span> <span data-ttu-id="439d4-276">此接口的设计使其可以与各种验证框架集成。</span><span class="sxs-lookup"><span data-stu-id="439d4-276">This interface has been designed so that it can be integrated with a variety of validation frameworks.</span></span>

<span data-ttu-id="439d4-277">有关验证接口的详细信息，请参阅[Scott Guthrie 的 MVC 3 预览博客文章的](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx)**模型验证改进**部分。</span><span class="sxs-lookup"><span data-stu-id="439d4-277">For more information about validation interfaces, see the **Model Validation Improvements** section of [Scott Guthrie's MVC 3 Preview blog post](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx).</span></span> <span data-ttu-id="439d4-278">（但是，请注意，博客中对"IValidateObject"的引用应为"IValidaaobject"。</span><span class="sxs-lookup"><span data-stu-id="439d4-278">(However, note that the reference to "IValidateObject" in the blog should be "IValidatableObject".)</span></span>

<a id="BM_Dependency_Injection_Improvements"></a>

## <a name="dependency-injection-improvements"></a><span data-ttu-id="439d4-279">依赖项注入改进</span><span class="sxs-lookup"><span data-stu-id="439d4-279">Dependency Injection Improvements</span></span>

<span data-ttu-id="439d4-280">ASP.NET MVC 3 为应用依赖项注入 （DI） 和与依赖项注入或控制反转 （IOC） 容器集成提供更好的支持。</span><span class="sxs-lookup"><span data-stu-id="439d4-280">ASP.NET MVC 3 provides better support for applying Dependency Injection (DI) and for integrating with Dependency Injection or Inversion of Control (IOC) containers.</span></span> <span data-ttu-id="439d4-281">在以下领域添加了对 DI 的支持：</span><span class="sxs-lookup"><span data-stu-id="439d4-281">Support for DI has been added in the following areas:</span></span>

- <span data-ttu-id="439d4-282">控制器（注册和注入控制器工厂，注入控制器）。</span><span class="sxs-lookup"><span data-stu-id="439d4-282">Controllers (registering and injecting controller factories, injecting controllers).</span></span>
- <span data-ttu-id="439d4-283">视图（注册和注入视图引擎，将依赖项注入视图页）。</span><span class="sxs-lookup"><span data-stu-id="439d4-283">Views (registering and injecting view engines, injecting dependencies into view pages).</span></span>
- <span data-ttu-id="439d4-284">操作筛选器（定位和注入过滤器）。</span><span class="sxs-lookup"><span data-stu-id="439d4-284">Action filters (locating and injecting filters).</span></span>
- <span data-ttu-id="439d4-285">模型活页夹（注册和注入）。</span><span class="sxs-lookup"><span data-stu-id="439d4-285">Model binders (registering and injecting).</span></span>
- <span data-ttu-id="439d4-286">模型验证提供程序（注册和注入）。</span><span class="sxs-lookup"><span data-stu-id="439d4-286">Model validation providers (registering and injecting).</span></span>
- <span data-ttu-id="439d4-287">建模元数据提供程序（注册和注入）。</span><span class="sxs-lookup"><span data-stu-id="439d4-287">Model metadata providers (registering and injecting).</span></span>
- <span data-ttu-id="439d4-288">价值提供者（注册和注入）。</span><span class="sxs-lookup"><span data-stu-id="439d4-288">Value providers (registering and injecting).</span></span>

<span data-ttu-id="439d4-289">MVC 3 支持[通用服务定位器](https://github.com/unitycontainer/commonservicelocator)库和支持该库`IServiceLocator`接口的任何 DI 容器。</span><span class="sxs-lookup"><span data-stu-id="439d4-289">MVC 3 supports the [Common Service Locator](https://github.com/unitycontainer/commonservicelocator) library and any DI container that supports that library's `IServiceLocator` interface.</span></span> <span data-ttu-id="439d4-290">它还支持一个新的`IDependencyResolver`接口，使集成 DI 框架变得更加容易。</span><span class="sxs-lookup"><span data-stu-id="439d4-290">It also supports a new `IDependencyResolver` interface that makes it easier to integrate DI frameworks.</span></span>

<span data-ttu-id="439d4-291">有关 MVC 3 中的 DI 的详细信息，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="439d4-291">For more information about DI in MVC 3, see the following resources:</span></span>

- [<span data-ttu-id="439d4-292">布拉德·威尔逊关于服务地点的一系列博客文章</span><span class="sxs-lookup"><span data-stu-id="439d4-292">Brad Wilson's series of blog posts on Service Location</span></span>](http://bradwilson.typepad.com/blog/2010/07/service-location-pt1-introduction.html)
- [<span data-ttu-id="439d4-293">MVC 3 发行说明</span><span class="sxs-lookup"><span data-stu-id="439d4-293">MVC 3 Release Notes</span></span>](../whitepapers/mvc3-release-notes.md)

<a id="BM_Other_New_Features"></a>

## <a name="other-new-features"></a><span data-ttu-id="439d4-294">其他新功能</span><span class="sxs-lookup"><span data-stu-id="439d4-294">Other New Features</span></span>

### <a name="nuget-integration"></a><span data-ttu-id="439d4-295">NuGet 集成</span><span class="sxs-lookup"><span data-stu-id="439d4-295">NuGet Integration</span></span>

<span data-ttu-id="439d4-296">ASP.NET MVC 3 自动安装并启用 NuGet 作为其设置的一部分。</span><span class="sxs-lookup"><span data-stu-id="439d4-296">ASP.NET MVC 3 automatically installs and enables NuGet as part of its setup.</span></span> <span data-ttu-id="439d4-297">NuGet 是一个免费的开源包管理器，可让您在项目中轻松查找、安装和使用 .NET 库和工具。</span><span class="sxs-lookup"><span data-stu-id="439d4-297">NuGet is a free open-source package manager that makes it easy to find, install, and use .NET libraries and tools in your projects.</span></span> <span data-ttu-id="439d4-298">它适用于所有 Visual Studio 项目类型（包括ASP.NET Web 窗体和ASP.NET MVC）。</span><span class="sxs-lookup"><span data-stu-id="439d4-298">It works with all Visual Studio project types (including ASP.NET Web Forms and ASP.NET MVC).</span></span>

<span data-ttu-id="439d4-299">NuGet 使维护开源项目的开发人员（例如，像 Moq、NHibernate、Ninject、结构映射、NUnit、温莎、RhinoMocks 和 Elmah）的项目）能够打包其库并将其注册到在线库中。</span><span class="sxs-lookup"><span data-stu-id="439d4-299">NuGet enables developers who maintain open source projects (for example, projects like Moq, NHibernate, Ninject, StructureMap, NUnit, Windsor, RhinoMocks, and Elmah) to package their libraries and register them in an online gallery.</span></span> <span data-ttu-id="439d4-300">然后，想要使用这些库之一的 .NET 开发人员可以轻松查找包并将其安装在他们正在处理的项目中。</span><span class="sxs-lookup"><span data-stu-id="439d4-300">It is then easy for .NET developers who want to use one of these libraries to find the package and install it in projects they are working on.</span></span>

<span data-ttu-id="439d4-301">通过ASP.NET 3 工具更新，项目模板包括预安装的 NuGet 包的 JavaScript 库，因此它们可以通过 NuGet 进行更新。</span><span class="sxs-lookup"><span data-stu-id="439d4-301">With the ASP.NET 3 Tools Update, project templates include JavaScript libraries pre-installed NuGet packages, so they are updatable via NuGet.</span></span> <span data-ttu-id="439d4-302">实体框架代码优先也预装为 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="439d4-302">Entity Framework Code First is also pre-installed as a NuGet package.</span></span>

<span data-ttu-id="439d4-303">有关 NuGet 的详细信息，请参阅 [NuGet 文档](https://docs.microsoft.com/nuget/)。</span><span class="sxs-lookup"><span data-stu-id="439d4-303">For more information about NuGet, see the [NuGet documentation](https://docs.microsoft.com/nuget/).</span></span>

### <a name="partial-page-output-caching"></a><span data-ttu-id="439d4-304">部分页面输出缓存</span><span class="sxs-lookup"><span data-stu-id="439d4-304">Partial-Page Output Caching</span></span>

<span data-ttu-id="439d4-305">自版本 1 以来ASP.NET MVC 都支持整页响应的输出缓存。</span><span class="sxs-lookup"><span data-stu-id="439d4-305">ASP.NET MVC has supported output caching of full page responses since version 1.</span></span> <span data-ttu-id="439d4-306">MVC 3 还支持部分页面输出缓存，这允许您轻松缓存响应的区域或片段。</span><span class="sxs-lookup"><span data-stu-id="439d4-306">MVC 3 also supports partial-page output caching, which allows you to easily cache regions or fragments of a response.</span></span> <span data-ttu-id="439d4-307">有关缓存的详细信息，请参阅[Scott Guthrie 在 MVC 3 版本候选版和 MVC](https://weblogs.asp.net/scottgu/archive/2010/11/09/announcing-the-asp-net-mvc-3-release-candidate.aspx) [3 发行说明](../whitepapers/mvc3-release-notes.md)的 **"子操作输出缓存**"部分部分页面**输出缓存**部分。</span><span class="sxs-lookup"><span data-stu-id="439d4-307">For more information about caching, see the **Partial Page Output Caching** section of [Scott Guthrie's blog post on the MVC 3 release candidate](https://weblogs.asp.net/scottgu/archive/2010/11/09/announcing-the-asp-net-mvc-3-release-candidate.aspx) and the **Child Action Output Caching** section of the [MVC 3 Release Notes](../whitepapers/mvc3-release-notes.md).</span></span>

### <a name="granular-control-over-request-validation"></a><span data-ttu-id="439d4-308">对请求验证的精细控制</span><span class="sxs-lookup"><span data-stu-id="439d4-308">Granular Control over Request Validation</span></span>

<span data-ttu-id="439d4-309">ASP.NET MVC 具有内置请求验证，可自动帮助抵御 XSS 和 HTML 注入攻击。</span><span class="sxs-lookup"><span data-stu-id="439d4-309">ASP.NET MVC has built-in request validation that automatically helps protect against XSS and HTML injection attacks.</span></span> <span data-ttu-id="439d4-310">但是，有时您希望显式禁用请求验证，例如，如果您希望允许用户发布 HTML 内容（例如，在博客条目或 CMS 内容中）。</span><span class="sxs-lookup"><span data-stu-id="439d4-310">However, sometimes you want to explicitly disable request validation, such as if you want to let users post HTML content (for example, in blog entries or CMS content).</span></span> <span data-ttu-id="439d4-311">现在，您可以将[AllowHtml](https://msdn.microsoft.com/library/system.web.mvc.allowhtmlattribute(v=VS.98).aspx)属性添加到模型或视图模型，以便在模型绑定期间禁用基于每个属性的请求验证。</span><span class="sxs-lookup"><span data-stu-id="439d4-311">You can now add an [AllowHtml](https://msdn.microsoft.com/library/system.web.mvc.allowhtmlattribute(v=VS.98).aspx) attribute to models or view models to disable request validation on a per-property basis during model binding.</span></span> <span data-ttu-id="439d4-312">有关请求验证的详细信息，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="439d4-312">For more information about request validation, see the following resources:</span></span>

- <span data-ttu-id="439d4-313">[斯科特·古斯里关于MVC 3版本候选的博客文章](https://weblogs.asp.net/scottgu/archive/2010/11/09/announcing-the-asp-net-mvc-3-release-candidate.aspx)中的 **"不显眼的JavaScript和验证**"部分。</span><span class="sxs-lookup"><span data-stu-id="439d4-313">The **Unobtrusive JavaScript and Validation** section in [Scott Guthrie's blog post on the MVC 3 release candidate](https://weblogs.asp.net/scottgu/archive/2010/11/09/announcing-the-asp-net-mvc-3-release-candidate.aspx).</span></span>
- [<span data-ttu-id="439d4-314">MVC 3 发行说明</span><span class="sxs-lookup"><span data-stu-id="439d4-314">MVC 3 Release Notes</span></span>](../whitepapers/mvc3-release-notes.md)

### <a name="extensible-new-project-dialog-box"></a><span data-ttu-id="439d4-315">可扩展的"新项目"对话框</span><span class="sxs-lookup"><span data-stu-id="439d4-315">Extensible "New Project" Dialog Box</span></span>

<span data-ttu-id="439d4-316">在 mVC 3 ASP.NET，您可以将项目模板、视图引擎和单元测试项目框架添加到 **"新项目**"对话框中。</span><span class="sxs-lookup"><span data-stu-id="439d4-316">In ASP.NET MVC 3 you can add project templates, view engines, and unit test project frameworks to the **New Project** dialog box.</span></span>

### <a name="template-scaffolding-improvements"></a><span data-ttu-id="439d4-317">模板基架改进</span><span class="sxs-lookup"><span data-stu-id="439d4-317">Template Scaffolding Improvements</span></span>

<span data-ttu-id="439d4-318">ASP.NET MVC 3 基架模板比早期版本的 MVC 更好地识别模型上的主键属性并适当地处理它们。</span><span class="sxs-lookup"><span data-stu-id="439d4-318">ASP.NET MVC 3 scaffolding templates do a better job of identifying primary-key properties on models and handling them appropriately than in earlier versions of MVC.</span></span> <span data-ttu-id="439d4-319">（例如，基架模板现在确保主键不是基架作为可编辑的表单字段。</span><span class="sxs-lookup"><span data-stu-id="439d4-319">(For example, the scaffolding templates now make sure that the primary key is not scaffolded as an editable form field.)</span></span>

<span data-ttu-id="439d4-320">默认情况下，"创建和编辑"基架现在使用`Html.EditorFor`帮助器而不是`Html.TextBoxFor`帮助程序。</span><span class="sxs-lookup"><span data-stu-id="439d4-320">By default, the Create and Edit scaffolds now use the `Html.EditorFor` helper instead of the `Html.TextBoxFor` helper.</span></span> <span data-ttu-id="439d4-321">这在 **"添加视图"** 对话框生成视图时，改进了对模型上以数据注释属性形式对元数据的支持。</span><span class="sxs-lookup"><span data-stu-id="439d4-321">This improves support for metadata on the model in the form of data annotation attributes when the **Add View** dialog box generates a view.</span></span>

### <a name="new-overloads-for-htmllabelfor-and-htmllabelformodel"></a><span data-ttu-id="439d4-322">"Html.Labelfor"和"Html.LabelFormodel"的新重载</span><span class="sxs-lookup"><span data-stu-id="439d4-322">New Overloads for "Html.LabelFor" and "Html.LabelForModel"</span></span>

<span data-ttu-id="439d4-323">已为`LabelFor`和`LabelForModel`帮助器方法添加了新方法重载。</span><span class="sxs-lookup"><span data-stu-id="439d4-323">New method overloads have been added for the `LabelFor` and `LabelForModel` helper methods.</span></span> <span data-ttu-id="439d4-324">新的重载使您能够指定或覆盖标签文本。</span><span class="sxs-lookup"><span data-stu-id="439d4-324">The new overloads enable you to specify or override the label text.</span></span>

### <a name="sessionless-controller-support"></a><span data-ttu-id="439d4-325">无会话控制器支持</span><span class="sxs-lookup"><span data-stu-id="439d4-325">Sessionless Controller Support</span></span>

<span data-ttu-id="439d4-326">在 mVC 3 ASP.NET 中，可以指示是否希望控制器类使用会话状态，如果是，会话状态应是读/写还是只读。</span><span class="sxs-lookup"><span data-stu-id="439d4-326">In ASP.NET MVC 3 you can indicate whether you want a controller class to use session state, and if so, whether session state should be read/write or read-only.</span></span> <span data-ttu-id="439d4-327">有关无会话控制器支持的详细信息，请参阅[MVC 3 发行说明](../whitepapers/mvc3-release-notes.md)。</span><span class="sxs-lookup"><span data-stu-id="439d4-327">For more information about sessionless controller support, see [MVC 3 Release Notes](../whitepapers/mvc3-release-notes.md).</span></span>

### <a name="new-additionalmetadataattribute-class"></a><span data-ttu-id="439d4-328">新的"附加元数据属性"类</span><span class="sxs-lookup"><span data-stu-id="439d4-328">New "AdditionalMetadataAttribute" Class</span></span>

<span data-ttu-id="439d4-329">可以使用["附加元数据"](https://msdn.microsoft.com/library/system.web.mvc.additionalmetadataattribute(v=VS.98).aspx)属性填充模型属性的`ModelMetadata.AdditionalValues`字典。</span><span class="sxs-lookup"><span data-stu-id="439d4-329">You can use the [AdditionalMetadata](https://msdn.microsoft.com/library/system.web.mvc.additionalmetadataattribute(v=VS.98).aspx) attribute to populate the `ModelMetadata.AdditionalValues` dictionary for a model property.</span></span> <span data-ttu-id="439d4-330">例如，如果视图模型具有仅应向管理员显示的属性，则可以对该属性进行加带，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="439d4-330">For example, if a view model has a property that should be displayed only to an administrator, you can annotate that property as shown in the following example:</span></span>

[!code-csharp[Main](mvc3/samples/sample4.cs)]

<span data-ttu-id="439d4-331">呈现产品视图模型时，此元数据可用于任何显示或编辑器模板。</span><span class="sxs-lookup"><span data-stu-id="439d4-331">This metadata is made available to any display or editor template when a product view model is rendered.</span></span> <span data-ttu-id="439d4-332">由您解释元数据信息。</span><span class="sxs-lookup"><span data-stu-id="439d4-332">It is up to you to interpret the metadata information.</span></span>

### <a name="accountcontroller-improvements"></a><span data-ttu-id="439d4-333">帐户控制器改进</span><span class="sxs-lookup"><span data-stu-id="439d4-333">AccountController improvements</span></span>

<span data-ttu-id="439d4-334">互联网项目模板中的帐户控制器已大为改善。</span><span class="sxs-lookup"><span data-stu-id="439d4-334">The AccountController in the Internet project template has been greatly improved.</span></span>

### <a name="new-intranet-project-template"></a><span data-ttu-id="439d4-335">新的内联网项目模板</span><span class="sxs-lookup"><span data-stu-id="439d4-335">New Intranet Project Template</span></span>

<span data-ttu-id="439d4-336">包含新的 Intranet 项目模板，该模板启用 Windows 身份验证并删除帐户控制器。</span><span class="sxs-lookup"><span data-stu-id="439d4-336">A new Intranet Project Template is included which enables Windows Authentication and removes the AccountController.</span></span>

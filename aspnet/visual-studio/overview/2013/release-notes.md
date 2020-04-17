---
uid: visual-studio/overview/2013/release-notes
title: 视觉工作室ASP.NET和网络工具 2013 发行说明 |微软文档
author: rick-anderson
description: 本文档介绍了 2013 年可视化工作室的ASP.NET和网络工具的发布。
ms.author: riande
ms.date: 10/17/2013
ms.assetid: 08815768-2702-42ae-ae85-0a59934a11d1
msc.legacyurl: /visual-studio/overview/2013/release-notes
msc.type: authoredcontent
ms.openlocfilehash: 4494b4acdd30384e1def89b7fff9bad30933e38e
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543491"
---
# <a name="aspnet-and-web-tools-for-visual-studio-2013-release-notes"></a><span data-ttu-id="cea65-103">适用于 Visual Studio 2013 的 ASP.NET 和 Web 工具发行说明</span><span class="sxs-lookup"><span data-stu-id="cea65-103">ASP.NET and Web Tools for Visual Studio 2013 Release Notes</span></span>

<span data-ttu-id="cea65-104">由[微软](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="cea65-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="cea65-105">本文档介绍了 2013 年可视化工作室的ASP.NET和网络工具的发布。</span><span class="sxs-lookup"><span data-stu-id="cea65-105">This document describes the release of ASP.NET and Web Tools for Visual Studio 2013.</span></span>

## <a name="contents"></a><span data-ttu-id="cea65-106">目录</span><span class="sxs-lookup"><span data-stu-id="cea65-106">Contents</span></span>

- [<span data-ttu-id="cea65-107">安装说明</span><span class="sxs-lookup"><span data-stu-id="cea65-107">Installation Notes</span></span>](#TOC1)
- [<span data-ttu-id="cea65-108">文档</span><span class="sxs-lookup"><span data-stu-id="cea65-108">Documentation</span></span>](#TOC2)
- [<span data-ttu-id="cea65-109">软件要求</span><span class="sxs-lookup"><span data-stu-id="cea65-109">Software Requirements</span></span>](#TOC4)

### <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-2013"></a><span data-ttu-id="cea65-110">2013年可视化工作室ASP.NET和网络工具的新功能</span><span class="sxs-lookup"><span data-stu-id="cea65-110">New Features in ASP.NET and Web Tools for Visual Studio 2013</span></span>

- [<span data-ttu-id="cea65-111">一ASP.NET</span><span class="sxs-lookup"><span data-stu-id="cea65-111">One ASP.NET</span></span>](#TOC6)
- [<span data-ttu-id="cea65-112">新的 Web 项目体验</span><span class="sxs-lookup"><span data-stu-id="cea65-112">New Web Project Experience</span></span>](#newproj)
- [<span data-ttu-id="cea65-113">ASP.NET脚手架</span><span class="sxs-lookup"><span data-stu-id="cea65-113">ASP.NET Scaffolding</span></span>](#scaffold)
- [<span data-ttu-id="cea65-114">浏览器链接</span><span class="sxs-lookup"><span data-stu-id="cea65-114">Browser Link</span></span>](#browser-link)
- [<span data-ttu-id="cea65-115">可视化工作室 Web 编辑器增强功能</span><span class="sxs-lookup"><span data-stu-id="cea65-115">Visual Studio Web Editor Enhancements</span></span>](#web-editor)
- [<span data-ttu-id="cea65-116">Visual Studio 中的 Azure 应用服务 Web 应用支持</span><span class="sxs-lookup"><span data-stu-id="cea65-116">Azure App Service Web Apps Support in Visual Studio</span></span>](#waws)
- [<span data-ttu-id="cea65-117">Web 发布增强功能</span><span class="sxs-lookup"><span data-stu-id="cea65-117">Web Publish Enhancements</span></span>](#publish)
- [<span data-ttu-id="cea65-118">NuGet 2.7</span><span class="sxs-lookup"><span data-stu-id="cea65-118">NuGet 2.7</span></span>](#nuget)
- [<span data-ttu-id="cea65-119">ASP.NET Web 表单</span><span class="sxs-lookup"><span data-stu-id="cea65-119">ASP.NET Web Forms</span></span>](#TOC9)
- [<span data-ttu-id="cea65-120">ASP.NET MVC 5</span><span class="sxs-lookup"><span data-stu-id="cea65-120">ASP.NET MVC 5</span></span>](#TOC10)
- [<span data-ttu-id="cea65-121">ASP.NET Web API 2</span><span class="sxs-lookup"><span data-stu-id="cea65-121">ASP.NET Web API 2</span></span>](#TOC11)
- [<span data-ttu-id="cea65-122">ASP.NET SignalR</span><span class="sxs-lookup"><span data-stu-id="cea65-122">ASP.NET SignalR</span></span>](#TOC13)
- [<span data-ttu-id="cea65-123">ASP.NET 标识</span><span class="sxs-lookup"><span data-stu-id="cea65-123">ASP.NET Identity</span></span>](#TOC8)
- [<span data-ttu-id="cea65-124">Microsoft OWIN 组件</span><span class="sxs-lookup"><span data-stu-id="cea65-124">Microsoft OWIN Components</span></span>](#TOC7)
- [<span data-ttu-id="cea65-125">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="cea65-125">Entity Framework 6</span></span>](#ef6)
- [<span data-ttu-id="cea65-126">ASP.NET剃刀 3</span><span class="sxs-lookup"><span data-stu-id="cea65-126">ASP.NET Razor 3</span></span>](#TOC14)
- [<span data-ttu-id="cea65-127">ASP.NET应用挂起</span><span class="sxs-lookup"><span data-stu-id="cea65-127">ASP.NET App Suspend</span></span>](#TOC15)
- [<span data-ttu-id="cea65-128">已知问题和重大更改</span><span class="sxs-lookup"><span data-stu-id="cea65-128">Known Issues and Breaking Changes</span></span>](#knownissues)

<a id="TOC1"></a>
## <a name="installation-notes"></a><span data-ttu-id="cea65-129">安装说明</span><span class="sxs-lookup"><span data-stu-id="cea65-129">Installation Notes</span></span>

<span data-ttu-id="cea65-130">ASP.NET和Web工具为可视化工作室2013捆绑在主安装程序，可以[在这里](https://www.asp.net/downloads)下载。</span><span class="sxs-lookup"><span data-stu-id="cea65-130">ASP.NET and Web Tools for Visual Studio 2013 are bundled in the main installer and can be downloaded [here](https://www.asp.net/downloads).</span></span>

<a id="TOC2"></a>
## <a name="documentation"></a><span data-ttu-id="cea65-131">文档</span><span class="sxs-lookup"><span data-stu-id="cea65-131">Documentation</span></span>

<span data-ttu-id="cea65-132">有关 visual Studio 2013 的ASP.NET和 Web 工具的教程和其他信息可从[ASP.NET网站](https://www.asp.net/)获得。</span><span class="sxs-lookup"><span data-stu-id="cea65-132">Tutorials and other information about ASP.NET and Web Tools for Visual Studio 2013 are available from the [ASP.NET web site](https://www.asp.net/).</span></span>

<a id="TOC4"></a>
## <a name="software-requirements"></a><span data-ttu-id="cea65-133">软件要求</span><span class="sxs-lookup"><span data-stu-id="cea65-133">Software Requirements</span></span>

<span data-ttu-id="cea65-134">ASP.NET和网络工具需要可视化工作室 2013。</span><span class="sxs-lookup"><span data-stu-id="cea65-134">ASP.NET and Web Tools requires Visual Studio 2013.</span></span>

<a id="TOC5"></a>
## <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-2013"></a><span data-ttu-id="cea65-135">2013年可视化工作室ASP.NET和网络工具的新功能</span><span class="sxs-lookup"><span data-stu-id="cea65-135">New Features in ASP.NET and Web Tools for Visual Studio 2013</span></span>

<span data-ttu-id="cea65-136">以下各节介绍版本中引入的功能。</span><span class="sxs-lookup"><span data-stu-id="cea65-136">The following sections describe the features that have been introduced in the release.</span></span>

<a id="TOC6"></a>
## <a name="one-aspnet"></a><span data-ttu-id="cea65-137">一ASP.NET</span><span class="sxs-lookup"><span data-stu-id="cea65-137">One ASP.NET</span></span>

<span data-ttu-id="cea65-138">随着 Visual Studio 2013 的发布，我们朝着统一使用ASP.NET技术的经验迈出了一步，以便您可以轻松混合和匹配所需的技术。</span><span class="sxs-lookup"><span data-stu-id="cea65-138">With the release of Visual Studio 2013, we have taken a step towards unifying the experience of using ASP.NET technologies, so that you can easily mix and match the ones you want.</span></span> <span data-ttu-id="cea65-139">例如，可以使用 MVC 启动项目，并在以后轻松地将 Web 窗体页添加到项目，或在 Web 窗体项目中基架 Web API 中。</span><span class="sxs-lookup"><span data-stu-id="cea65-139">For example, you can start a project using MVC and easily add Web Forms pages to the project later, or scaffold Web APIs in a Web Forms project.</span></span> <span data-ttu-id="cea65-140">一ASP.NET就是让你作为开发人员更容易在ASP.NET中做你喜欢的事情。</span><span class="sxs-lookup"><span data-stu-id="cea65-140">One ASP.NET is all about making it easier for you as a developer to do the things you love in ASP.NET.</span></span> <span data-ttu-id="cea65-141">无论您选择何种技术，您都可以确信自己正在构建"一ASP.NET"的可信底层框架。</span><span class="sxs-lookup"><span data-stu-id="cea65-141">No matter what technology you choose, you can have confidence that you are building on the trusted underlying framework of One ASP.NET.</span></span>

<a id="newproj"></a>
## <a name="new-web-project-experience"></a><span data-ttu-id="cea65-142">新的 Web 项目体验</span><span class="sxs-lookup"><span data-stu-id="cea65-142">New Web Project Experience</span></span>

<span data-ttu-id="cea65-143">我们在 Visual Studio 2013 中增强了创建新 Web 项目的经验。</span><span class="sxs-lookup"><span data-stu-id="cea65-143">We have enhanced the experience of creating new web projects in Visual Studio 2013.</span></span> <span data-ttu-id="cea65-144">在 **"新建ASP.NET Web 项目**"对话框中，您可以选择所需的项目类型、配置任何技术组合（Web 窗体、MVC、Web API）、配置身份验证选项以及添加单元测试项目。</span><span class="sxs-lookup"><span data-stu-id="cea65-144">In the **New ASP.NET Web Project** dialog you can select the project type you want, configure any combination of technologies (Web Forms, MVC, Web API), configure authentication options, and add a unit test project.</span></span>

![新ASP.NET项目](release-notes/_static/image1.png)

<span data-ttu-id="cea65-146">新的对话框使您能够更改许多模板的默认身份验证选项。</span><span class="sxs-lookup"><span data-stu-id="cea65-146">The new dialog enables you to change the default authentication options for many of the templates.</span></span> <span data-ttu-id="cea65-147">例如，在创建ASP.NET Web 窗体项目时，您可以选择以下任一选项：</span><span class="sxs-lookup"><span data-stu-id="cea65-147">For example, when you create an ASP.NET Web Forms project you can select any of the following options:</span></span>

- <span data-ttu-id="cea65-148">无身份验证</span><span class="sxs-lookup"><span data-stu-id="cea65-148">No Authentication</span></span>
- <span data-ttu-id="cea65-149">个人用户帐户（ASP.NET会员身份或社交提供商登录）</span><span class="sxs-lookup"><span data-stu-id="cea65-149">Individual User Accounts (ASP.NET membership or social provider log in)</span></span>
- <span data-ttu-id="cea65-150">组织帐户（互联网应用程序中的活动目录）</span><span class="sxs-lookup"><span data-stu-id="cea65-150">Organizational Accounts (Active Directory in an internet application)</span></span>
- <span data-ttu-id="cea65-151">Windows 身份验证（Intranet 应用程序中的活动目录）</span><span class="sxs-lookup"><span data-stu-id="cea65-151">Windows Authentication (Active Directory in an intranet application)</span></span>

![身份验证选项](release-notes/_static/image2.png)

<span data-ttu-id="cea65-153">有关创建 Web 项目的新流程的详细信息，请参阅在[Visual Studio 2013 中创建ASP.NET Web 项目](creating-web-projects-in-visual-studio.md)。</span><span class="sxs-lookup"><span data-stu-id="cea65-153">For more information about the new process for creating web projects, see [Creating ASP.NET Web Projects in Visual Studio 2013](creating-web-projects-in-visual-studio.md).</span></span> <span data-ttu-id="cea65-154">有关新身份验证选项的详细信息，请参阅本文档后面的[ASP.NET标识](#TOC8)。</span><span class="sxs-lookup"><span data-stu-id="cea65-154">For more information about the new authentication options, see [ASP.NET Identity](#TOC8) later in this document.</span></span>

<a id="scaffold"></a>
## <a name="aspnet-scaffolding"></a><span data-ttu-id="cea65-155">ASP.NET脚手架</span><span class="sxs-lookup"><span data-stu-id="cea65-155">ASP.NET Scaffolding</span></span>

<span data-ttu-id="cea65-156">ASP.NET基架是ASP.NET Web 应用程序的代码生成框架。</span><span class="sxs-lookup"><span data-stu-id="cea65-156">ASP.NET Scaffolding is a code generation framework for ASP.NET Web applications.</span></span> <span data-ttu-id="cea65-157">它可以轻松地向与数据模型交互的项目添加样板代码。</span><span class="sxs-lookup"><span data-stu-id="cea65-157">It makes it easy to add boilerplate code to your project that interacts with a data model.</span></span>

<span data-ttu-id="cea65-158">在 Visual Studio 的早期版本中，基架仅限于ASP.NET MVC 项目。</span><span class="sxs-lookup"><span data-stu-id="cea65-158">In previous versions of Visual Studio, scaffolding was limited to ASP.NET MVC projects.</span></span> <span data-ttu-id="cea65-159">借助 Visual Studio 2013，您现在可以对任何ASP.NET项目（包括 Web 窗体）使用基架。</span><span class="sxs-lookup"><span data-stu-id="cea65-159">With Visual Studio 2013, you can now use scaffolding for any ASP.NET project, including Web Forms.</span></span> <span data-ttu-id="cea65-160">Visual Studio 2013 目前不支持为 Web 窗体项目生成页面，但您仍可以通过向项目添加 MVC 依赖项来使用 Web 窗体的脚手架。</span><span class="sxs-lookup"><span data-stu-id="cea65-160">Visual Studio 2013 does not currently support generating pages for a Web Forms project, but you can still use scaffolding with Web Forms by adding MVC dependencies to the project.</span></span> <span data-ttu-id="cea65-161">将在将来的更新中添加对生成 Web 窗体页面的支持。</span><span class="sxs-lookup"><span data-stu-id="cea65-161">Support for generating pages for Web Forms will be added in a future update.</span></span>

<span data-ttu-id="cea65-162">使用基架时，我们确保在项目中安装了所有必需的依赖项。</span><span class="sxs-lookup"><span data-stu-id="cea65-162">When using scaffolding, we ensure that all required dependencies are installed in the project.</span></span> <span data-ttu-id="cea65-163">例如，如果从ASP.NET Web 窗体项目开始，然后使用基架添加 Web API 控制器，则所需的 NuGet 包和引用将自动添加到项目中。</span><span class="sxs-lookup"><span data-stu-id="cea65-163">For example, if you start with an ASP.NET Web Forms project and then use scaffolding to add a Web API Controller, the required NuGet packages and references are added to your project automatically.</span></span>

<span data-ttu-id="cea65-164">要将 MVC 基架添加到 Web 窗体项目，请添加新**的脚手架项**，并在对话框窗口中选择**MVC 5 依赖项**。</span><span class="sxs-lookup"><span data-stu-id="cea65-164">To add MVC scaffolding to a Web Forms project, add a **New Scaffolded Item** and select **MVC 5 Dependencies** in the dialog window.</span></span> <span data-ttu-id="cea65-165">基架 MVC 有两个选项;最小和完整。</span><span class="sxs-lookup"><span data-stu-id="cea65-165">There are two options for scaffolding MVC; Minimal and Full.</span></span> <span data-ttu-id="cea65-166">如果选择"最小"，则只有 ASP.NET MVC 的 NuGet 包和引用添加到项目中。</span><span class="sxs-lookup"><span data-stu-id="cea65-166">If you select Minimal, only the NuGet packages and references for ASP.NET MVC are added to your project.</span></span> <span data-ttu-id="cea65-167">如果选择"完整"选项，则添加最小依赖项以及 MVC 项目所需的内容文件。</span><span class="sxs-lookup"><span data-stu-id="cea65-167">If you select the Full option, the Minimal dependencies are added, as well as the required content files for an MVC project.</span></span>

<span data-ttu-id="cea65-168">支持基架异步控制器使用实体框架 6 中的新异步功能。</span><span class="sxs-lookup"><span data-stu-id="cea65-168">Support for scaffolding async controllers uses the new async features from Entity Framework 6.</span></span>

<span data-ttu-id="cea65-169">有关详细信息和教程，请参阅[ASP.NET脚手架概述](aspnet-scaffolding-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="cea65-169">For more information and tutorials, see [ASP.NET Scaffolding Overview](aspnet-scaffolding-overview.md).</span></span>

<a id="browser-link"></a>
## <a name="browser-link--signalr-channel-between-browser-and-visual-studio"></a><span data-ttu-id="cea65-170">浏览器链接 + 浏览器和可视化工作室之间的信号R通道</span><span class="sxs-lookup"><span data-stu-id="cea65-170">Browser Link – SignalR channel between browser and Visual Studio</span></span>

<span data-ttu-id="cea65-171">新的[浏览器链接](using-browser-link.md)功能允许您将多个浏览器连接到 Visual Studio，并通过单击工具栏中的按钮刷新所有浏览器。</span><span class="sxs-lookup"><span data-stu-id="cea65-171">The new [Browser Link](using-browser-link.md) feature lets you connect multiple browsers to Visual Studio and refresh them all by clicking a button in the toolbar.</span></span> <span data-ttu-id="cea65-172">您可以将多个浏览器连接到开发站点（包括移动仿真程序），然后单击刷新以同时刷新所有浏览器。</span><span class="sxs-lookup"><span data-stu-id="cea65-172">You can connect multiple browsers to your development site, including mobile emulators, and click refresh to refresh all the browsers all at the same time.</span></span> <span data-ttu-id="cea65-173">浏览器链接还公开 API，使开发人员能够编写浏览器链接扩展。</span><span class="sxs-lookup"><span data-stu-id="cea65-173">Browser Link also exposes an API to enable developers to write Browser Link extensions.</span></span>

![](release-notes/_static/image3.png)

<span data-ttu-id="cea65-174">通过使开发人员能够利用浏览器链接 API，可以创建非常高级的方案，这些方案跨越 Visual Studio 和任何已连接的浏览器之间的边界。</span><span class="sxs-lookup"><span data-stu-id="cea65-174">By enabling developers to take advantage of the Browser Link API, it becomes possible to create very advanced scenarios that crosses boundaries between Visual Studio and any browser that's connected.</span></span> <span data-ttu-id="cea65-175">Web Essentials 利用 API 在 Visual Studio 和浏览器的开发人员工具、远程控制移动仿真器等之间创建集成体验。</span><span class="sxs-lookup"><span data-stu-id="cea65-175">Web Essentials takes advantage of the API to create an integrated experience between Visual Studio and the browser's developer tools, remote controlling mobile emulators and a lot more.</span></span>

<a id="web-editor"></a>
## <a name="visual-studio-web-editor-enhancements"></a><span data-ttu-id="cea65-176">可视化工作室 Web 编辑器增强功能</span><span class="sxs-lookup"><span data-stu-id="cea65-176">Visual Studio Web Editor Enhancements</span></span>

<span data-ttu-id="cea65-177">Visual Studio 2013 包括用于 Web 应用程序中 Razor 文件和 HTML 文件的新 HTML 编辑器。</span><span class="sxs-lookup"><span data-stu-id="cea65-177">Visual Studio 2013 includes a new HTML editor for Razor files and HTML files in web applications.</span></span> <span data-ttu-id="cea65-178">新的 HTML 编辑器提供基于 HTML5 的单个统一架构。</span><span class="sxs-lookup"><span data-stu-id="cea65-178">The new HTML editor provides a single unified schema based on HTML5.</span></span> <span data-ttu-id="cea65-179">它有自动大括号完成，jQuery UI和AngularJS属性IntelliSense，属性IntelliSense分组，ID和类名Intellisense，和其他改进，包括更好的性能，格式和智能标签。</span><span class="sxs-lookup"><span data-stu-id="cea65-179">It has automatic brace completion, jQuery UI and AngularJS attribute IntelliSense, attribute IntelliSense Grouping, ID and class name Intellisense, and other improvements including better performance, formatting and SmartTags.</span></span>

<span data-ttu-id="cea65-180">以下屏幕截图演示如何在 HTML 编辑器中使用 Bootstrap 属性 IntelliSense。</span><span class="sxs-lookup"><span data-stu-id="cea65-180">The following screenshot demonstrates using Bootstrap attribute IntelliSense in the HTML editor.</span></span>

![HTML 编辑器中的感知](release-notes/_static/image4.png)

<span data-ttu-id="cea65-182">Visual Studio 2013 还附带了内置的咖啡脚本和 LESS 编辑器。</span><span class="sxs-lookup"><span data-stu-id="cea65-182">Visual Studio 2013 also comes with both CoffeeScript and LESS editors built in.</span></span> <span data-ttu-id="cea65-183">LESS 编辑器附带了 CSS 编辑器中的所有很酷的功能，并具有针对@import链中所有 LESS 文档中的变量和混合值的特定 Intellisense。</span><span class="sxs-lookup"><span data-stu-id="cea65-183">The LESS editor comes with all the cool features from the CSS editor and has specific Intellisense for variables and mixins across all the LESS documents in the @import chain.</span></span>

<a id="waws"></a>
## <a name="azure-app-service-web-apps-support-in-visual-studio"></a><span data-ttu-id="cea65-184">Visual Studio 中的 Azure 应用服务 Web 应用支持</span><span class="sxs-lookup"><span data-stu-id="cea65-184">Azure App Service Web Apps Support in Visual Studio</span></span>

<span data-ttu-id="cea65-185">在 Visual Studio 2013 中，使用用于 .NET 2.2 的 Azure SDK，可以使用**服务器资源管理器**直接与远程 Web 应用进行交互。</span><span class="sxs-lookup"><span data-stu-id="cea65-185">In Visual Studio 2013 with the Azure SDK for .NET 2.2, you can use **Server Explorer** to interact directly with your remote web apps.</span></span> <span data-ttu-id="cea65-186">您可以登录到 Azure 帐户、创建新的 Web 应用、配置应用、查看实时日志等。</span><span class="sxs-lookup"><span data-stu-id="cea65-186">You can sign in to your Azure account, create new web apps, configure apps, view real-time logs, and more.</span></span> <span data-ttu-id="cea65-187">SDK 2.2 发布后不久，您将能够在 Azure 中远程在调试模式下运行。</span><span class="sxs-lookup"><span data-stu-id="cea65-187">Coming soon after SDK 2.2 is released, you'll be able to run in debug mode remotely in Azure.</span></span> <span data-ttu-id="cea65-188">安装 .NET 的 Azure SDK 当前版本时，Azure 应用服务 Web 应用的大多数新功能在 Visual Studio 2012 中也起作用。</span><span class="sxs-lookup"><span data-stu-id="cea65-188">Most of the new features for Azure App Service Web Apps also work in Visual Studio 2012 when you install the current release of the Azure SDK for .NET.</span></span>

<span data-ttu-id="cea65-189">有关更多信息，请参见以下资源：</span><span class="sxs-lookup"><span data-stu-id="cea65-189">For more information, see the following resources:</span></span>

- [<span data-ttu-id="cea65-190">在 Azure 应用服务中创建 ASP.NET Web 应用</span><span class="sxs-lookup"><span data-stu-id="cea65-190">Create an ASP.NET web app in Azure App Service</span></span>](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/)
- [<span data-ttu-id="cea65-191">使用 Visual Studio 对 Azure 应用服务中的 Web 应用进行故障排除</span><span class="sxs-lookup"><span data-stu-id="cea65-191">Troubleshoot a web app in Azure App Service using Visual Studio</span></span>](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/)

<a id="publish"></a>
## <a name="web-publish-enhancements"></a><span data-ttu-id="cea65-192">Web 发布增强功能</span><span class="sxs-lookup"><span data-stu-id="cea65-192">Web Publish Enhancements</span></span>

<span data-ttu-id="cea65-193">Visual Studio 2013 包括新的和增强的 Web 发布功能。</span><span class="sxs-lookup"><span data-stu-id="cea65-193">Visual Studio 2013 includes new and enhanced Web Publish features.</span></span> <span data-ttu-id="cea65-194">下面是其中几个示例：</span><span class="sxs-lookup"><span data-stu-id="cea65-194">Here are a few of them:</span></span>

- <span data-ttu-id="cea65-195">轻松[自动进行 Web.config 文件加密](https://go.microsoft.com/fwlink/?LinkId=325529)。</span><span class="sxs-lookup"><span data-stu-id="cea65-195">Easily [automate Web.config file encryption](https://go.microsoft.com/fwlink/?LinkId=325529).</span></span> <span data-ttu-id="cea65-196">（此链接和以下两个指向 MSDN 上的文档，这些文档可能直到 10 月 17 日深夜才可用。</span><span class="sxs-lookup"><span data-stu-id="cea65-196">(This link and the following two point to documentation on MSDN that might not be available until late in the day on 10/17.)</span></span>
- <span data-ttu-id="cea65-197">在[部署期间轻松自动使应用程序脱机](https://go.microsoft.com/fwlink/?LinkId=325530)。</span><span class="sxs-lookup"><span data-stu-id="cea65-197">Easily [automate taking an application offline during deployment](https://go.microsoft.com/fwlink/?LinkId=325530).</span></span>
- <span data-ttu-id="cea65-198">将 Web 部署配置为[使用文件校验和，而不是上次更改的日期](https://go.microsoft.com/fwlink/?LinkId=325531)，以确定应复制到服务器的文件。</span><span class="sxs-lookup"><span data-stu-id="cea65-198">Configure Web Deploy to [use file checksum instead of last-changed date](https://go.microsoft.com/fwlink/?LinkId=325531) for determining which files should be copied to the server.</span></span>
- <span data-ttu-id="cea65-199">使用 FTP 或文件系统发布方法以及 Web 部署时，快速发布单个选定文件（包括 Web.config）。</span><span class="sxs-lookup"><span data-stu-id="cea65-199">Quickly publish individual selected files (including Web.config) when you're using the FTP or file system publish methods as well as with Web Deploy.</span></span>

<span data-ttu-id="cea65-200">有关ASP.NET Web 部署的详细信息，请参阅[ASP.NET网站](https://go.microsoft.com/fwlink/?LinkId=322027)。</span><span class="sxs-lookup"><span data-stu-id="cea65-200">For more information about ASP.NET web deployment, see [the ASP.NET site](https://go.microsoft.com/fwlink/?LinkId=322027).</span></span>

<a id="nuget"></a>
## <a name="nuget-27"></a><span data-ttu-id="cea65-201">NuGet 2.7</span><span class="sxs-lookup"><span data-stu-id="cea65-201">NuGet 2.7</span></span>

<span data-ttu-id="cea65-202">NuGet 2.7 包含一组丰富的新功能，在[NuGet 2.7 发行说明](http://docs.nuget.org/docs/release-notes/nuget-2.7)中对此进行了详细介绍。</span><span class="sxs-lookup"><span data-stu-id="cea65-202">NuGet 2.7 includes a rich set of new features which are described in detail at [NuGet 2.7 Release Notes](http://docs.nuget.org/docs/release-notes/nuget-2.7).</span></span>

<span data-ttu-id="cea65-203">此版本的 NuGet 还无需为 NuGet 的包还原功能提供下载包的明确同意。</span><span class="sxs-lookup"><span data-stu-id="cea65-203">This version of NuGet also removes the need to provide explicit consent for NuGet's package restore feature to download packages.</span></span> <span data-ttu-id="cea65-204">现在通过安装 NuGet 授予同意（以及 NuGet 首选项对话框中的关联复选框）。</span><span class="sxs-lookup"><span data-stu-id="cea65-204">Consent (and the associated checkbox in NuGet's preferences dialog) is now granted by installing NuGet.</span></span> <span data-ttu-id="cea65-205">现在，默认情况下，包还原只是工作。</span><span class="sxs-lookup"><span data-stu-id="cea65-205">Now package restore simply works by default.</span></span>

<a id="TOC9"></a>
## <a name="aspnet-web-forms"></a><span data-ttu-id="cea65-206">ASP.NET Web 窗体</span><span class="sxs-lookup"><span data-stu-id="cea65-206">ASP.NET Web Forms</span></span>

### <a name="one-aspnet"></a><span data-ttu-id="cea65-207">一ASP.NET</span><span class="sxs-lookup"><span data-stu-id="cea65-207">One ASP.NET</span></span>

<span data-ttu-id="cea65-208">Web 窗体项目模板与新 one ASP.NET 体验无缝集成。</span><span class="sxs-lookup"><span data-stu-id="cea65-208">The Web Forms project templates integrate seamlessly with the new One ASP.NET experience.</span></span> <span data-ttu-id="cea65-209">您可以将 MVC 和 Web API 支持添加到 Web 窗体项目中，并且可以使用"一ASP.NET项目创建向导配置身份验证。</span><span class="sxs-lookup"><span data-stu-id="cea65-209">You can add MVC and Web API support to your Web Forms project, and you can configure authentication using the One ASP.NET project creation wizard.</span></span> <span data-ttu-id="cea65-210">有关详细信息，请参阅在[Visual Studio 2013 中创建ASP.NET Web 项目](creating-web-projects-in-visual-studio.md)。</span><span class="sxs-lookup"><span data-stu-id="cea65-210">For more information, see [Creating ASP.NET Web Projects in Visual Studio 2013](creating-web-projects-in-visual-studio.md).</span></span>

### <a name="aspnet-identity"></a><span data-ttu-id="cea65-211">ASP.NET 标识</span><span class="sxs-lookup"><span data-stu-id="cea65-211">ASP.NET Identity</span></span>

<span data-ttu-id="cea65-212">Web 窗体项目模板支持新的ASP.NET标识框架。</span><span class="sxs-lookup"><span data-stu-id="cea65-212">The Web Forms project templates support the new ASP.NET Identity framework.</span></span> <span data-ttu-id="cea65-213">此外，模板现在支持创建 Web 窗体 Intranet 项目。</span><span class="sxs-lookup"><span data-stu-id="cea65-213">In addition, the templates now support creation of a Web Forms intranet project.</span></span> <span data-ttu-id="cea65-214">有关详细信息，请参阅在**Visual Studio 2013 中创建ASP.NET Web 项目的**[身份验证方法](creating-web-projects-in-visual-studio.md#auth)。</span><span class="sxs-lookup"><span data-stu-id="cea65-214">For more information, see [Authentication Methods](creating-web-projects-in-visual-studio.md#auth) in **Creating ASP.NET Web Projects in Visual Studio 2013**.</span></span>

### <a name="bootstrap"></a><span data-ttu-id="cea65-215">Bootstrap</span><span class="sxs-lookup"><span data-stu-id="cea65-215">Bootstrap</span></span>

<span data-ttu-id="cea65-216">Web 窗体模板使用[Bootstrap](http://twitter.github.io/bootstrap/)提供时尚且响应迅速的外观，让您轻松自定义。</span><span class="sxs-lookup"><span data-stu-id="cea65-216">The Web Forms templates use [Bootstrap](http://twitter.github.io/bootstrap/) to provide a sleek and responsive look and feel that you can easily customize.</span></span> <span data-ttu-id="cea65-217">有关详细信息，请参阅[Visual Studio 2013 Web 项目模板中的 Bootstrap。](creating-web-projects-in-visual-studio.md#bootstrap)</span><span class="sxs-lookup"><span data-stu-id="cea65-217">For more information, see [Bootstrap in the Visual Studio 2013 web project templates](creating-web-projects-in-visual-studio.md#bootstrap).</span></span>

<a id="TOC10"></a>
## <a name="aspnet-mvc-5"></a><span data-ttu-id="cea65-218">ASP.NET MVC 5</span><span class="sxs-lookup"><span data-stu-id="cea65-218">ASP.NET MVC 5</span></span>

### <a name="one-aspnet"></a><span data-ttu-id="cea65-219">一ASP.NET</span><span class="sxs-lookup"><span data-stu-id="cea65-219">One ASP.NET</span></span>

<span data-ttu-id="cea65-220">Web MVC 项目模板与新一ASP.NET体验无缝集成。</span><span class="sxs-lookup"><span data-stu-id="cea65-220">The Web MVC project templates integrate seamlessly with the new One ASP.NET experience.</span></span> <span data-ttu-id="cea65-221">您可以使用"一ASP.NET项目创建向导自定义 MVC 项目并配置身份验证。</span><span class="sxs-lookup"><span data-stu-id="cea65-221">You can customize your MVC project and configure authentication using the One ASP.NET project creation wizard.</span></span> <span data-ttu-id="cea65-222">ASP.NET MVC 5 的入门教程可以在[ASP.NET MVC 5 入门](../../../mvc/overview/getting-started/introduction/getting-started.md)中找到。</span><span class="sxs-lookup"><span data-stu-id="cea65-222">An introductory tutorial to ASP.NET MVC 5 can be found at [Getting Started with ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md).</span></span>

<span data-ttu-id="cea65-223">有关将 MVC 4 项目升级到 MVC 5 的信息，请参阅[如何将ASP.NET MVC 4 和 Web API 项目升级到ASP.NET MVC 5 和 Web API 2](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md)。</span><span class="sxs-lookup"><span data-stu-id="cea65-223">For information on upgrading MVC 4 projects to MVC 5, see [How to Upgrade an ASP.NET MVC 4 and Web API Project to ASP.NET MVC 5 and Web API 2](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md).</span></span>

### <a name="aspnet-identity"></a><span data-ttu-id="cea65-224">ASP.NET 标识</span><span class="sxs-lookup"><span data-stu-id="cea65-224">ASP.NET Identity</span></span>

<span data-ttu-id="cea65-225">MVC 项目模板已更新，用于ASP.NET标识进行身份验证和标识管理。</span><span class="sxs-lookup"><span data-stu-id="cea65-225">The MVC project templates have been updated to use ASP.NET Identity for authentication and identity management.</span></span> <span data-ttu-id="cea65-226">一个教程，包括Facebook和谷歌认证和新的会员API可以在[创建一个ASP.NETMVC 5应用程序与Facebook和谷歌OAuth2和OpenID登录](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)，[并创建一个ASP.NETMVC应用程序与auth和SQL DB，并部署到Azure应用程序服务](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/)。</span><span class="sxs-lookup"><span data-stu-id="cea65-226">A tutorial featuring Facebook and Google authentication and the new membership API can be found at [Create an ASP.NET MVC 5 App with Facebook and Google OAuth2 and OpenID Sign-on](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) and [Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/).</span></span>

### <a name="bootstrap"></a><span data-ttu-id="cea65-227">Bootstrap</span><span class="sxs-lookup"><span data-stu-id="cea65-227">Bootstrap</span></span>

<span data-ttu-id="cea65-228">MVC 项目模板已更新，可使用[Bootstrap](http://getbootstrap.com/)提供时尚且响应迅速的外观，让您轻松自定义。</span><span class="sxs-lookup"><span data-stu-id="cea65-228">The MVC project template has been updated to use [Bootstrap](http://getbootstrap.com/) to provide a sleek and responsive look and feel that you can easily customize.</span></span> <span data-ttu-id="cea65-229">有关详细信息，请参阅[Visual Studio 2013 Web 项目模板中的 Bootstrap。](creating-web-projects-in-visual-studio.md#bootstrap)</span><span class="sxs-lookup"><span data-stu-id="cea65-229">For more information, see [Bootstrap in the Visual Studio 2013 web project templates](creating-web-projects-in-visual-studio.md#bootstrap).</span></span>

### <a name="authentication-filters"></a><span data-ttu-id="cea65-230">身份验证筛选器</span><span class="sxs-lookup"><span data-stu-id="cea65-230">Authentication filters</span></span>

<span data-ttu-id="cea65-231">身份验证筛选器是 ASP.NET MVC 中一种新型筛选器，在 ASP.NET MVC 管道中的授权筛选器之前运行，允许您为所有控制器指定每个操作、每个控制器或全局的身份验证逻辑。</span><span class="sxs-lookup"><span data-stu-id="cea65-231">Authentication filters are a new kind of filter in ASP.NET MVC that run prior to authorization filters in the ASP.NET MVC pipeline and allow you to specify authentication logic per-action, per-controller, or globally for all controllers.</span></span> <span data-ttu-id="cea65-232">身份验证筛选器处理请求中的凭据并提供相应的主体。</span><span class="sxs-lookup"><span data-stu-id="cea65-232">Authentication filters process credentials in the request and provide a corresponding principal.</span></span> <span data-ttu-id="cea65-233">身份验证筛选器还可以添加身份验证质询以响应未经授权的请求。</span><span class="sxs-lookup"><span data-stu-id="cea65-233">Authentication filters can also add authentication challenges in response to unauthorized requests.</span></span>

### <a name="filter-overrides"></a><span data-ttu-id="cea65-234">筛选器覆盖</span><span class="sxs-lookup"><span data-stu-id="cea65-234">Filter overrides</span></span>

<span data-ttu-id="cea65-235">现在，可以通过指定覆盖筛选器来覆盖应用于给定操作方法或控制器的筛选器。</span><span class="sxs-lookup"><span data-stu-id="cea65-235">You can now override which filters apply to a given action method or controller by specifying an override filter.</span></span> <span data-ttu-id="cea65-236">覆盖筛选器指定一组不应为给定作用域（操作或控制器）运行的筛选器类型。</span><span class="sxs-lookup"><span data-stu-id="cea65-236">Override filters specify a set of filter types that should not be run for a given scope (action or controller).</span></span> <span data-ttu-id="cea65-237">这允许您配置全局应用的筛选器，但随后排除某些全局筛选器应用于特定操作或控制器。</span><span class="sxs-lookup"><span data-stu-id="cea65-237">This allows you to configure filters that apply globally but then exclude certain global filters from applying to specific actions or controllers.</span></span>

### <a name="attribute-routing"></a><span data-ttu-id="cea65-238">属性路由</span><span class="sxs-lookup"><span data-stu-id="cea65-238">Attribute routing</span></span>

<span data-ttu-id="cea65-239">ASP.NET MVC 现在支持属性路由，这要归功于[http://attributerouting.net](http://attributerouting.net)Tim McCall（作者）的贡献。</span><span class="sxs-lookup"><span data-stu-id="cea65-239">ASP.NET MVC now supports attribute routing, thanks to a contribution by Tim McCall, the author of [http://attributerouting.net](http://attributerouting.net).</span></span> <span data-ttu-id="cea65-240">使用属性路由，您可以通过对操作和控制器进行说明来指定路由。</span><span class="sxs-lookup"><span data-stu-id="cea65-240">With attribute routing you can specify your routes by annotating your actions and controllers.</span></span>

<a id="TOC11"></a>
## <a name="aspnet-web-api-2"></a><span data-ttu-id="cea65-241">ASP.NET Web API 2</span><span class="sxs-lookup"><span data-stu-id="cea65-241">ASP.NET Web API 2</span></span>

### <a name="attribute-routing"></a><span data-ttu-id="cea65-242">属性路由</span><span class="sxs-lookup"><span data-stu-id="cea65-242">Attribute routing</span></span>

<span data-ttu-id="cea65-243">ASP.NET Web API 现在支持属性路由，这要归功于[http://attributerouting.net](http://attributerouting.net)Tim McCall（作者）的贡献。</span><span class="sxs-lookup"><span data-stu-id="cea65-243">ASP.NET Web API now supports attribute routing, thanks to a contribution by Tim McCall, the author of [http://attributerouting.net](http://attributerouting.net).</span></span> <span data-ttu-id="cea65-244">使用属性路由，您可以通过指定操作和控制器来指定 Web API 路由，如下所示：</span><span class="sxs-lookup"><span data-stu-id="cea65-244">With attribute routing you can specify your Web API routes by annotating your actions and controllers like this:</span></span>

[!code-csharp[Main](release-notes/samples/sample1.cs)]

<span data-ttu-id="cea65-245">属性路由使您能够对 Web API 中的 URI 进行更多控制。</span><span class="sxs-lookup"><span data-stu-id="cea65-245">Attribute routing gives you more control over the URIs in your web API.</span></span> <span data-ttu-id="cea65-246">例如，您可以使用单个 API 控制器轻松定义资源层次结构：</span><span class="sxs-lookup"><span data-stu-id="cea65-246">For example, you can easily define a resource hierarchy using a single API controller:</span></span>

[!code-csharp[Main](release-notes/samples/sample2.cs)]

<span data-ttu-id="cea65-247">属性路由还提供用于指定可选参数、默认值和路由约束的便捷语法：</span><span class="sxs-lookup"><span data-stu-id="cea65-247">Attribute routing also provides a convenient syntax for specifying optional parameters, default values, and route constraints:</span></span>

[!code-csharp[Main](release-notes/samples/sample3.cs)]

<span data-ttu-id="cea65-248">有关属性路由的详细信息，请参阅[Web API 2 中的属性路由](../../../web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2.md)。</span><span class="sxs-lookup"><span data-stu-id="cea65-248">For more information about attribute routing, see [Attribute Routing in Web API 2](../../../web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2.md).</span></span>

### <a name="oauth-20"></a><span data-ttu-id="cea65-249">OAuth 2.0</span><span class="sxs-lookup"><span data-stu-id="cea65-249">OAuth 2.0</span></span>

<span data-ttu-id="cea65-250">Web API 和单页应用程序项目模板现在支持使用 OAuth 2.0 进行授权。</span><span class="sxs-lookup"><span data-stu-id="cea65-250">The Web API and Single Page Application project templates now support authorization using OAuth 2.0.</span></span> <span data-ttu-id="cea65-251">OAuth 2.0 是一个用于授权客户端访问受保护资源的框架。</span><span class="sxs-lookup"><span data-stu-id="cea65-251">OAuth 2.0 is a framework for authorizing client access to protected resources.</span></span> <span data-ttu-id="cea65-252">它适用于各种客户端，包括浏览器和移动设备。</span><span class="sxs-lookup"><span data-stu-id="cea65-252">It works for a variety of clients including browsers and mobile devices.</span></span>

<span data-ttu-id="cea65-253">对 OAuth 2.0 的支持基于 Microsoft OWIN 组件为承载身份验证和实现授权服务器角色而提供的新安全中间件。</span><span class="sxs-lookup"><span data-stu-id="cea65-253">Support for OAuth 2.0 is based on new security middleware provided by the Microsoft OWIN Components for bearer authentication and implementing the authorization server role.</span></span> <span data-ttu-id="cea65-254">或者，可以使用组织授权服务器（如 Windows Server 2012 R2 中的 Azure 活动目录或 ADFS）授权客户端。</span><span class="sxs-lookup"><span data-stu-id="cea65-254">Alternatively, clients can be authorized using an organizational authorization server, such as Azure Active Directory or ADFS in Windows Server 2012 R2.</span></span>

### <a name="odata-improvements"></a><span data-ttu-id="cea65-255">O数据改进</span><span class="sxs-lookup"><span data-stu-id="cea65-255">OData Improvements</span></span>

<span data-ttu-id="cea65-256">**支持$select、$expand、$batch和$value**</span><span class="sxs-lookup"><span data-stu-id="cea65-256">**Support for $select, $expand, $batch, and $value**</span></span>

<span data-ttu-id="cea65-257">ASP.NET Web API OData 现在完全支持$select、$expand和$value。</span><span class="sxs-lookup"><span data-stu-id="cea65-257">ASP.NET Web API OData now has full support for $select, $expand, and $value.</span></span> <span data-ttu-id="cea65-258">您还可以使用$batch请求批处理和处理更改集。</span><span class="sxs-lookup"><span data-stu-id="cea65-258">You can also use $batch for request batching and processing of change sets.</span></span>

<span data-ttu-id="cea65-259">$select和$expand选项允许您更改从 OData 终结点返回的数据的形状。</span><span class="sxs-lookup"><span data-stu-id="cea65-259">The $select and $expand options let you change the shape of the data that is returned from an OData endpoint.</span></span> <span data-ttu-id="cea65-260">有关详细信息，请参阅在[Web API OData 中介绍$select和$expand支持](../../../web-api/overview/odata-support-in-aspnet-web-api/using-select-expand-and-value.md)。</span><span class="sxs-lookup"><span data-stu-id="cea65-260">For more information, see [Introducing $select and $expand support in Web API OData](../../../web-api/overview/odata-support-in-aspnet-web-api/using-select-expand-and-value.md).</span></span>

<span data-ttu-id="cea65-261">**提高可扩展性**</span><span class="sxs-lookup"><span data-stu-id="cea65-261">**Improved extensibility**</span></span>

<span data-ttu-id="cea65-262">OData for 物质现在可扩展。</span><span class="sxs-lookup"><span data-stu-id="cea65-262">The OData formatters are now extensible.</span></span> <span data-ttu-id="cea65-263">您可以添加 Atom 条目元数据、支持命名流和媒体链接条目、添加实例注释以及自定义链接的生成方式。</span><span class="sxs-lookup"><span data-stu-id="cea65-263">You can add Atom entry metadata, support named stream and media link entries, add instance annotations, and customize how links are generated.</span></span>

<span data-ttu-id="cea65-264">**无类型支持**</span><span class="sxs-lookup"><span data-stu-id="cea65-264">**Type-less support**</span></span>

<span data-ttu-id="cea65-265">现在，您可以构建 OData 服务，而无需为实体类型定义 CLR 类型。</span><span class="sxs-lookup"><span data-stu-id="cea65-265">You can now build OData services without needing to define CLR types for your entity types.</span></span> <span data-ttu-id="cea65-266">相反，您的 OData 控制器可以获取或返回**IEdmObject**的实例 ，这是用于序列化/反序列化的 OData 实例。</span><span class="sxs-lookup"><span data-stu-id="cea65-266">Instead, your OData controllers can take or return instances of **IEdmObject**, which are the OData formatters serialize/deserialize.</span></span>

<span data-ttu-id="cea65-267">**重用现有模型**</span><span class="sxs-lookup"><span data-stu-id="cea65-267">**Reuse an existing model**</span></span>

<span data-ttu-id="cea65-268">如果您已有现有的实体数据模型 （EDM），现在可以直接重用它，而不必构建新的实体数据模型。</span><span class="sxs-lookup"><span data-stu-id="cea65-268">If you already have an existing entity data model (EDM), you can now reuse it directly, instead of having to build a new one.</span></span> <span data-ttu-id="cea65-269">例如，如果您使用的是实体框架，则可以使用 EF 为您生成的 EDM。</span><span class="sxs-lookup"><span data-stu-id="cea65-269">For example, if you are using Entity Framework, you can use the EDM that EF builds for you.</span></span>

### <a name="request-batching"></a><span data-ttu-id="cea65-270">请求批处理</span><span class="sxs-lookup"><span data-stu-id="cea65-270">Request Batching</span></span>

<span data-ttu-id="cea65-271">请求批处理将多个操作合并到单个 HTTP POST 请求中，以减少网络流量并提供更顺畅、更不健谈的用户界面。</span><span class="sxs-lookup"><span data-stu-id="cea65-271">Request batching combines multiple operations into a single HTTP POST request, to reduce network traffic and provide a smoother, less chatty user interface.</span></span> <span data-ttu-id="cea65-272">ASP.NET Web API 现在支持几种请求批处理策略：</span><span class="sxs-lookup"><span data-stu-id="cea65-272">ASP.NET Web API now supports several strategies for request batching:</span></span>

- <span data-ttu-id="cea65-273">使用 OData 服务$batch终结点。</span><span class="sxs-lookup"><span data-stu-id="cea65-273">Use the $batch endpoint of an OData service.</span></span>
- <span data-ttu-id="cea65-274">将多个请求打包到单个 MIME 多部分请求中。</span><span class="sxs-lookup"><span data-stu-id="cea65-274">Package multiple requests into a single MIME multipart request.</span></span>
- <span data-ttu-id="cea65-275">使用自定义批处理格式。</span><span class="sxs-lookup"><span data-stu-id="cea65-275">Use a custom batching format.</span></span>

<span data-ttu-id="cea65-276">要启用请求批处理，只需将具有批处理处理程序的路由添加到 Web API 配置中：</span><span class="sxs-lookup"><span data-stu-id="cea65-276">To enable request batching, simply add a route with a batching handler to your Web API configuration:</span></span>

[!code-csharp[Main](release-notes/samples/sample4.cs)]

<span data-ttu-id="cea65-277">您还可以控制请求或按顺序执行，还是按任何顺序执行。</span><span class="sxs-lookup"><span data-stu-id="cea65-277">You can also control whether requests or executed sequentially or in any order.</span></span>

### <a name="portable-aspnet-web-api-client"></a><span data-ttu-id="cea65-278">可移植ASP.NET Web API 客户端</span><span class="sxs-lookup"><span data-stu-id="cea65-278">Portable ASP.NET Web API Client</span></span>

<span data-ttu-id="cea65-279">现在，可以使用 ASP.NET Web API 客户端创建跨 Windows 应用商店和 Windows Phone 8 应用程序的便携式类库。</span><span class="sxs-lookup"><span data-stu-id="cea65-279">You can now use the ASP.NET Web API Client to create portable class libraries that work across your Windows Store and Windows Phone 8 applications.</span></span> <span data-ttu-id="cea65-280">您还可以创建可在客户端和服务器之间共享的可移植的要件。</span><span class="sxs-lookup"><span data-stu-id="cea65-280">You can also create portable formatters that can be shared across client and server.</span></span>

### <a name="improved-testability"></a><span data-ttu-id="cea65-281">提高可测试性</span><span class="sxs-lookup"><span data-stu-id="cea65-281">Improved Testability</span></span>

<span data-ttu-id="cea65-282">Web API 2 使单元测试 API 控制器变得更加容易。</span><span class="sxs-lookup"><span data-stu-id="cea65-282">Web API 2 makes it much easier to unit test your API controllers.</span></span> <span data-ttu-id="cea65-283">只需使用请求消息和配置实例化 API 控制器，然后调用要测试的操作方法。</span><span class="sxs-lookup"><span data-stu-id="cea65-283">Just instantiate your API controller with your request message and configuration, and then call the action method you wish to test.</span></span> <span data-ttu-id="cea65-284">对于执行链接生成的操作方法，也很容易模拟**UrlHelper**类。</span><span class="sxs-lookup"><span data-stu-id="cea65-284">It is also easy to mock the **UrlHelper** class, for action methods that perform link generation.</span></span>

### <a name="ihttpactionresult"></a><span data-ttu-id="cea65-285">IHttpAction 结果</span><span class="sxs-lookup"><span data-stu-id="cea65-285">IHttpActionResult</span></span>

<span data-ttu-id="cea65-286">现在，您可以实现 IHttpActionResult 来封装 Web API 操作方法的结果。</span><span class="sxs-lookup"><span data-stu-id="cea65-286">You can now implement IHttpActionResult to encapsulate the result of your Web API action methods.</span></span> <span data-ttu-id="cea65-287">从 Web API 操作方法返回的 IHttpActionResult 由 ASP.NET Web API 运行时执行，以生成产生的响应消息。</span><span class="sxs-lookup"><span data-stu-id="cea65-287">An IHttpActionResult returned from a Web API action method is executed by the ASP.NET Web API runtime to produce the resultant response message.</span></span> <span data-ttu-id="cea65-288">可以从任何 Web API 操作返回 IHttpActionResult，以简化 Web API 实现单元测试。</span><span class="sxs-lookup"><span data-stu-id="cea65-288">An IHttpActionResult can be returned from any Web API action to simplify unit testing of your Web API implementation.</span></span> <span data-ttu-id="cea65-289">为方便起见，一些 IHttpActionResult 实现在开箱即用，包括用于返回特定状态代码、格式化内容或内容协商响应的结果。</span><span class="sxs-lookup"><span data-stu-id="cea65-289">For convenience a number of IHttpActionResult implementations are provided out of the box including results for returning specific status codes, formatted content or content-negotiated responses.</span></span>

### <a name="httprequestcontext"></a><span data-ttu-id="cea65-290">HttpRequestContext</span><span class="sxs-lookup"><span data-stu-id="cea65-290">HttpRequestContext</span></span>

<span data-ttu-id="cea65-291">新的**HttpRequestContext**跟踪与请求关联的任何状态，但无法立即从请求中获取。</span><span class="sxs-lookup"><span data-stu-id="cea65-291">The new **HttpRequestContext** tracks any state that is tied to the request but is not immediately available from the request.</span></span> <span data-ttu-id="cea65-292">例如，可以使用**HttpRequestContext**获取路由数据、与请求关联的主体、客户端证书 **、UrlHelper**和虚拟路径根。</span><span class="sxs-lookup"><span data-stu-id="cea65-292">For example, you can use the **HttpRequestContext** to get route data, the principal associated with the request, the client certificate, the **UrlHelper** and the virtual path root.</span></span> <span data-ttu-id="cea65-293">您可以轻松地为单元测试目的创建**HttpRequestContext。**</span><span class="sxs-lookup"><span data-stu-id="cea65-293">You can easily create an **HttpRequestContext** for unit testing purposes.</span></span>

<span data-ttu-id="cea65-294">由于请求的主体随请求一起流动，而不是依赖于**Thread.CurrentThe，** 因此主体现在在请求在 Web API 管道中时在请求的整个生存期内可用。</span><span class="sxs-lookup"><span data-stu-id="cea65-294">Because the principal for the request is flowed with the request instead of relying on **Thread.CurrentPrincipal**, the principal is now available throughout the lifetime of the request while it is in the Web API pipeline.</span></span>

### <a name="cors"></a><span data-ttu-id="cea65-295">CORS</span><span class="sxs-lookup"><span data-stu-id="cea65-295">CORS</span></span>

<span data-ttu-id="cea65-296">多亏了布罗克·艾伦的另一个巨大贡献，ASP.NET现在完全支持跨原请求共享 （CORS）。</span><span class="sxs-lookup"><span data-stu-id="cea65-296">Thanks to another great contribution from Brock Allen, ASP.NET now fully supports Cross Origin Request Sharing (CORS).</span></span>

<span data-ttu-id="cea65-297">浏览器安全性将阻止网页向另一个域发出 AJAX 请求。</span><span class="sxs-lookup"><span data-stu-id="cea65-297">Browser security prevents a web page from making AJAX requests to another domain.</span></span> <span data-ttu-id="cea65-298">[CORS](http://www.w3.org/TR/cors/)是一种 W3C 标准，允许服务器放松同源策略。</span><span class="sxs-lookup"><span data-stu-id="cea65-298">[CORS](http://www.w3.org/TR/cors/) is a W3C standard that allows a server to relax the same-origin policy.</span></span> <span data-ttu-id="cea65-299">使用 CORS，服务器可以显式允许某些跨域请求，同时拒绝另一些跨域请求。</span><span class="sxs-lookup"><span data-stu-id="cea65-299">Using CORS, a server can explicitly allow some cross-origin requests while rejecting others.</span></span>

<span data-ttu-id="cea65-300">Web API 2 现在支持 CORS，包括自动处理预检请求。</span><span class="sxs-lookup"><span data-stu-id="cea65-300">Web API 2 now supports CORS, including automatic handling of preflight requests.</span></span> <span data-ttu-id="cea65-301">有关详细信息，请参阅在[web API 中启用跨源请求ASP.NET](../../../web-api/overview/security/enabling-cross-origin-requests-in-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="cea65-301">For more information, see [Enabling Cross-Origin Requests in ASP.NET Web API](../../../web-api/overview/security/enabling-cross-origin-requests-in-web-api.md).</span></span>

### <a name="authentication-filters"></a><span data-ttu-id="cea65-302">身份验证筛选器</span><span class="sxs-lookup"><span data-stu-id="cea65-302">Authentication Filters</span></span>

<span data-ttu-id="cea65-303">身份验证筛选器是 web API 中ASP.NET一种新型筛选器，在ASP.NET Web API 管道中授权筛选器之前运行，允许您为所有控制器指定每个操作、每个控制器或全局的身份验证逻辑。</span><span class="sxs-lookup"><span data-stu-id="cea65-303">Authentication filters are a new kind of filter in ASP.NET Web API that run prior to authorization filters in the ASP.NET Web API pipeline and allow you to specify authentication logic per-action, per-controller, or globally for all controllers.</span></span> <span data-ttu-id="cea65-304">身份验证筛选器处理请求中的凭据并提供相应的主体。</span><span class="sxs-lookup"><span data-stu-id="cea65-304">Authentication filters process credentials in the request and provide a corresponding principal.</span></span> <span data-ttu-id="cea65-305">身份验证筛选器还可以添加身份验证质询以响应未经授权的请求。</span><span class="sxs-lookup"><span data-stu-id="cea65-305">Authentication filters can also add authentication challenges in response to unauthorized requests.</span></span>

### <a name="filter-overrides"></a><span data-ttu-id="cea65-306">筛选器覆盖</span><span class="sxs-lookup"><span data-stu-id="cea65-306">Filter Overrides</span></span>

<span data-ttu-id="cea65-307">现在，可以通过指定重写筛选器来覆盖应用于给定操作方法或控制器的筛选器。</span><span class="sxs-lookup"><span data-stu-id="cea65-307">You can now override which filters apply to a given action method or controller, by specifying an override filter.</span></span> <span data-ttu-id="cea65-308">覆盖筛选器指定一组不应为给定作用域（操作或控制器）运行的筛选器类型。</span><span class="sxs-lookup"><span data-stu-id="cea65-308">Override filters specify a set of filter types that should not run for a given scope (action or controller).</span></span> <span data-ttu-id="cea65-309">这允许您添加全局筛选器，但随后从特定操作或控制器中排除某些筛选器。</span><span class="sxs-lookup"><span data-stu-id="cea65-309">This allows you to add global filters, but then exclude some from specific actions or controllers.</span></span>

### <a name="owin-integration"></a><span data-ttu-id="cea65-310">OWIN 集成</span><span class="sxs-lookup"><span data-stu-id="cea65-310">OWIN Integration</span></span>

<span data-ttu-id="cea65-311">ASP.NET Web API 现在完全支持 OWIN，可以在任何支持 OWIN 的主机上运行。</span><span class="sxs-lookup"><span data-stu-id="cea65-311">ASP.NET Web API now fully supports OWIN and can be run on any OWIN capable host.</span></span> <span data-ttu-id="cea65-312">还包括一个**主机身份验证筛选器**，它提供与 OWIN 身份验证系统的集成。</span><span class="sxs-lookup"><span data-stu-id="cea65-312">Also included is a **HostAuthenticationFilter** that provides integration with the OWIN authentication system.</span></span>

<span data-ttu-id="cea65-313">通过 OWIN 集成，您可以与其他 OWIN 中间件（如 SignalR）一起，在您自己的进程中自行托管 Web API。</span><span class="sxs-lookup"><span data-stu-id="cea65-313">With OWIN integration, you can self-host Web API in your own process alongside other OWIN middleware, such as SignalR.</span></span> <span data-ttu-id="cea65-314">有关详细信息，请参阅使用[OWIN ASP.NET Web API 进行自托管](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)。</span><span class="sxs-lookup"><span data-stu-id="cea65-314">For more information, see [Use OWIN to Self-Host ASP.NET Web API](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).</span></span>

<a id="TOC13"></a>
## <a name="aspnet-signalr-20"></a><span data-ttu-id="cea65-315">ASP.NET信号R 2.0</span><span class="sxs-lookup"><span data-stu-id="cea65-315">ASP.NET SignalR 2.0</span></span>

<span data-ttu-id="cea65-316">以下各节介绍 SignalR 2.0 的功能。</span><span class="sxs-lookup"><span data-stu-id="cea65-316">The following sections describe features of SignalR 2.0.</span></span>

- [<span data-ttu-id="cea65-317">基于 OWIN 构建</span><span class="sxs-lookup"><span data-stu-id="cea65-317">Built on OWIN</span></span>](#builtonowin)
- [<span data-ttu-id="cea65-318">地图集线和地图连接现在是映射信号R</span><span class="sxs-lookup"><span data-stu-id="cea65-318">MapHubs and MapConnection are now MapSignalR</span></span>](#MapSignalR)
- [<span data-ttu-id="cea65-319">跨域支持</span><span class="sxs-lookup"><span data-stu-id="cea65-319">Cross-Domain Support</span></span>](#crossdomain)
- [<span data-ttu-id="cea65-320">通过单点触控和单体机器人支持 iOS 和 Android</span><span class="sxs-lookup"><span data-stu-id="cea65-320">iOS and Android support via MonoTouch and MonoDroid</span></span>](#mobile)
- [<span data-ttu-id="cea65-321">便携式 .NET 客户端</span><span class="sxs-lookup"><span data-stu-id="cea65-321">Portable .NET Client</span></span>](#portable)
- [<span data-ttu-id="cea65-322">新的自主机包</span><span class="sxs-lookup"><span data-stu-id="cea65-322">New Self-Host Package</span></span>](#selfhost)
- [<span data-ttu-id="cea65-323">向后兼容的服务器支持</span><span class="sxs-lookup"><span data-stu-id="cea65-323">Backward-compatible server support</span></span>](#backwardcompat)
- [<span data-ttu-id="cea65-324">已删除对 .NET 4.0 的服务器支持</span><span class="sxs-lookup"><span data-stu-id="cea65-324">Removed server support for .NET 4.0</span></span>](#remove40)
- [<span data-ttu-id="cea65-325">将消息发送到客户端和组列表</span><span class="sxs-lookup"><span data-stu-id="cea65-325">Sending a message to a list of clients and groups</span></span>](#messagelist)
- [<span data-ttu-id="cea65-326">向特定用户发送消息</span><span class="sxs-lookup"><span data-stu-id="cea65-326">Sending a message to a specific user</span></span>](#sendtouser)
- [<span data-ttu-id="cea65-327">更好的错误处理支持</span><span class="sxs-lookup"><span data-stu-id="cea65-327">Better error handling support</span></span>](#errorhandling)
- [<span data-ttu-id="cea65-328">更简便的集线器单元测试</span><span class="sxs-lookup"><span data-stu-id="cea65-328">Easier unit testing of hubs</span></span>](#unittesting)
- [<span data-ttu-id="cea65-329">JavaScript 错误处理</span><span class="sxs-lookup"><span data-stu-id="cea65-329">JavaScript error handling</span></span>](#javascripterror)

<span data-ttu-id="cea65-330">有关如何将现有的 1.x 项目升级到 SignalR 2.0 的示例，请参阅[升级 SignalR 1.x 项目](../../../signalr/overview/releases/upgrading-signalr-1x-projects-to-20.md)。</span><span class="sxs-lookup"><span data-stu-id="cea65-330">For an example of how to upgrade an existing 1.x project to SignalR 2.0, see [Upgrading a SignalR 1.x Project](../../../signalr/overview/releases/upgrading-signalr-1x-projects-to-20.md).</span></span>

<a id="builtonowin"></a>
### <a name="built-on-owin"></a><span data-ttu-id="cea65-331">基于 OWIN 构建</span><span class="sxs-lookup"><span data-stu-id="cea65-331">Built on OWIN</span></span>

<span data-ttu-id="cea65-332">SignalR 2.0 完全基于[OWIN（.NET 的开放 Web 界面）](http://owin.org/)构建。</span><span class="sxs-lookup"><span data-stu-id="cea65-332">SignalR 2.0 is built completely on [OWIN (the Open Web Interface for .NET)](http://owin.org/).</span></span> <span data-ttu-id="cea65-333">此更改使 SignalR 的设置过程在 Web 托管和自托管 SignalR 应用程序之间更加一致，但还需要多次 API 更改。</span><span class="sxs-lookup"><span data-stu-id="cea65-333">This change makes the setup process for SignalR much more consistent between web-hosted and self-hosted SignalR applications, but has also required a number of API changes.</span></span>

<a id="MapSignalR"></a>

### <a name="maphubs-and-mapconnection-are-now-mapsignalr"></a><span data-ttu-id="cea65-334">地图集线和地图连接现在是映射信号R</span><span class="sxs-lookup"><span data-stu-id="cea65-334">MapHubs and MapConnection are now MapSignalR</span></span>

<span data-ttu-id="cea65-335">为了与 OWIN 标准兼容，这些方法已重命名为`MapSignalR`。</span><span class="sxs-lookup"><span data-stu-id="cea65-335">For compatibility with OWIN standards, these methods have been renamed to `MapSignalR`.</span></span> <span data-ttu-id="cea65-336">`MapSignalR`在没有参数的情况下调用将映射所有中心（如`MapHubs`版本 1.x）;映射单个**持久连接**对象，将连接类型指定为类型参数，并将连接的 URL 扩展作为第一个参数。</span><span class="sxs-lookup"><span data-stu-id="cea65-336">`MapSignalR` called without parameters will map all hubs (as `MapHubs` does in version 1.x); to map individual **PersistentConnection** objects, specify the connection type as the type parameter, and the URL extension for the connection as the first argument.</span></span>

<span data-ttu-id="cea65-337">该方法`MapSignalR`在 Owin 启动类中调用。</span><span class="sxs-lookup"><span data-stu-id="cea65-337">The `MapSignalR` method is called in an Owin startup class.</span></span> <span data-ttu-id="cea65-338">Visual Studio 2013 包含 Owin 启动类的新模板;要使用此模板，请使用以下操作：</span><span class="sxs-lookup"><span data-stu-id="cea65-338">Visual Studio 2013 contains a new template for an Owin startup class; to use this template, do the following:</span></span>

1. <span data-ttu-id="cea65-339">右键单击项目</span><span class="sxs-lookup"><span data-stu-id="cea65-339">Right-click on the project</span></span>
2. <span data-ttu-id="cea65-340">选择 **"添加\*\*\*\*"，新项目...**</span><span class="sxs-lookup"><span data-stu-id="cea65-340">Select **Add**, **New Item...**</span></span>
3. <span data-ttu-id="cea65-341">选择**Owin 启动类**。</span><span class="sxs-lookup"><span data-stu-id="cea65-341">Select **Owin Startup class**.</span></span> <span data-ttu-id="cea65-342">Startup.cs命名**新类。**</span><span class="sxs-lookup"><span data-stu-id="cea65-342">Name the new class **Startup.cs**.</span></span>

<span data-ttu-id="cea65-343">在**Web 应用程序中，** 包含该方法`MapSignalR`的 Owin 启动类随后使用 Web.Config 文件的应用程序设置节点中的条目添加到 Owin 的启动过程中，如下所示。</span><span class="sxs-lookup"><span data-stu-id="cea65-343">In a **Web application,** the Owin startup class containing the `MapSignalR` method is then added to Owin's startup process using an entry in the application settings node of the Web.Config file, as shown below.</span></span>

<span data-ttu-id="cea65-344">在**自托管应用程序中**，启动类作为`WebApp.Start`方法的类型参数传递。</span><span class="sxs-lookup"><span data-stu-id="cea65-344">In a **Self-hosted application**, the Startup class is passed as the type parameter of the `WebApp.Start` method.</span></span>

<span data-ttu-id="cea65-345">**映射 SignalR 1.x 中的集线器和连接（来自 Web 应用程序中的全局应用程序文件）：**</span><span class="sxs-lookup"><span data-stu-id="cea65-345">**Mapping hubs and connections in SignalR 1.x (from the global application file in a web application):**</span></span> 

[!code-csharp[Main](release-notes/samples/sample5.cs)]

<span data-ttu-id="cea65-346">**映射 SignalR 2.0 中的集线器和连接（来自 Owin 启动类文件）：**</span><span class="sxs-lookup"><span data-stu-id="cea65-346">**Mapping hubs and connections in SignalR 2.0 (from an Owin Startup class file):**</span></span> 

[!code-csharp[Main](release-notes/samples/sample6.cs)]

<span data-ttu-id="cea65-347">在**自托管应用程序中**，启动类作为`WebApp.Start`方法的类型参数传递，如下所示。</span><span class="sxs-lookup"><span data-stu-id="cea65-347">In a **Self-hosted application**, the Startup class is passed as the type parameter for the `WebApp.Start` method, as shown below.</span></span>

[!code-csharp[Main](release-notes/samples/sample7.cs)]

<a id="crossdomain"></a>

### <a name="cross-domain-support"></a><span data-ttu-id="cea65-348">跨域支持</span><span class="sxs-lookup"><span data-stu-id="cea65-348">Cross-Domain Support</span></span>

<span data-ttu-id="cea65-349">在 SignalR 1.x 中，跨域请求由单个启用CrossDomain 标志控制。</span><span class="sxs-lookup"><span data-stu-id="cea65-349">In SignalR 1.x, cross domain requests were controlled by a single EnableCrossDomain flag.</span></span> <span data-ttu-id="cea65-350">此标志同时控制 JSONP 和 CORS 请求。</span><span class="sxs-lookup"><span data-stu-id="cea65-350">This flag controlled both JSONP and CORS requests.</span></span> <span data-ttu-id="cea65-351">为了更灵活，所有 CORS 支持都从 SignalR 的服务器组件中删除（如果检测到浏览器支持它，JavaScript 客户端仍通常使用 CORS），并且新的 OWIN 中间件已可用于支持这些方案。</span><span class="sxs-lookup"><span data-stu-id="cea65-351">For greater flexibility, all CORS support has been removed from the server component of SignalR (JavaScript clients still use CORS normally if it is detected that the browser supports it), and new OWIN middleware has been made available to support these scenarios.</span></span>

<span data-ttu-id="cea65-352">在 SignalR 2.0 中，如果客户端上需要 JSONP（以支持旧浏览器中的跨域请求），则需要通过在`EnableJSONP``HubConfiguration`对象`true`上设置为 （如下所示）显式启用它。</span><span class="sxs-lookup"><span data-stu-id="cea65-352">In SignalR 2.0, If JSONP is required on the client (to support cross-domain requests in older browsers), it will need to be enabled explicitly by setting `EnableJSONP` on the `HubConfiguration` object to `true`, as shown below.</span></span> <span data-ttu-id="cea65-353">默认情况下禁用 JSONP，因为它的安全性低于 CORS。</span><span class="sxs-lookup"><span data-stu-id="cea65-353">JSONP is disabled by default, as it is less secure than CORS.</span></span>

<span data-ttu-id="cea65-354">要在 SignalR 2.0 中添加新的 CORS`Microsoft.Owin.Cors`中间件，请将库添加到`UseCors`项目中，并在 SignalR 中间件之前调用，如下节所示。</span><span class="sxs-lookup"><span data-stu-id="cea65-354">To add the new CORS middleware in SignalR 2.0, add the `Microsoft.Owin.Cors` library to your project, and call `UseCors` before your SignalR middleware, as shown in the section below.</span></span>

<span data-ttu-id="cea65-355">**将 Microsoft.Owin.Cors 添加到您的项目**：要安装此库，请在包管理器控制台中运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="cea65-355">**Adding Microsoft.Owin.Cors to your project**: To install this library, run the following command in the Package Manager Console:</span></span>

[!code-powershell[Main](release-notes/samples/sample8.ps1)]

<span data-ttu-id="cea65-356">此命令会将包的 2.0.0 版本添加到项目中。</span><span class="sxs-lookup"><span data-stu-id="cea65-356">This command will add the 2.0.0 version of the package to your project.</span></span>

<span data-ttu-id="cea65-357">**调用使用参数**</span><span class="sxs-lookup"><span data-stu-id="cea65-357">**Calling UseCors**</span></span>

<span data-ttu-id="cea65-358">以下代码段演示如何在 SignalR 1.x 和 2.0 中实现跨域连接。</span><span class="sxs-lookup"><span data-stu-id="cea65-358">The following code snippets demonstrate how to implement cross-domain connections in SignalR 1.x and 2.0.</span></span>

<span data-ttu-id="cea65-359">**在 SignalR 1.x 中实现跨域请求（来自全局应用程序文件）**</span><span class="sxs-lookup"><span data-stu-id="cea65-359">**Implementing cross-domain requests in SignalR 1.x (from the global application file)**</span></span>

[!code-csharp[Main](release-notes/samples/sample9.cs)]

<span data-ttu-id="cea65-360">**在 SignalR 2.0 中实现跨域请求（来自 C# 代码文件）**</span><span class="sxs-lookup"><span data-stu-id="cea65-360">**Implementing cross-domain requests in SignalR 2.0 (from a C# code file)**</span></span>

<span data-ttu-id="cea65-361">以下代码演示如何在 SignalR 2.0 项目中启用 CORS 或 JSONP。</span><span class="sxs-lookup"><span data-stu-id="cea65-361">The following code demonstrates how to enable CORS or JSONP in a SignalR 2.0 project.</span></span> <span data-ttu-id="cea65-362">此代码示例使用`Map``RunSignalR`而不是`MapSignalR`，以便 CORS 中间件仅运行需要 CORS 支持的 SignalR 请求（而不是针对 中`MapSignalR`指定的路径上的所有流量）。`Map`还可用于需要为特定 URL 前缀运行的任何其他中间件，而不是整个应用程序。</span><span class="sxs-lookup"><span data-stu-id="cea65-362">This code sample uses `Map` and `RunSignalR` instead of `MapSignalR`, so that the CORS middleware runs only for the SignalR requests that require CORS support (rather than for all traffic at the path specified in `MapSignalR`.) `Map` can also be used for any other middleware that needs to run for a specific URL prefix, rather than for the entire application.</span></span>

[!code-csharp[Main](release-notes/samples/sample10.cs)]

<a id="mobile"></a>

### <a name="ios-and-android-support-via-monotouch-and-monodroid"></a><span data-ttu-id="cea65-363">通过单点触控和单体机器人支持 iOS 和 Android</span><span class="sxs-lookup"><span data-stu-id="cea65-363">iOS and Android support via MonoTouch and MonoDroid</span></span>

<span data-ttu-id="cea65-364">已使用[Xamarin 库中](https://xamarin.com/)的 MonoTouch 和 MonoDroid 组件为 iOS 和 Android 客户端添加了支持。</span><span class="sxs-lookup"><span data-stu-id="cea65-364">Support has been added for iOS and Android clients using MonoTouch and MonoDroid components from the [Xamarin library](https://xamarin.com/).</span></span> <span data-ttu-id="cea65-365">有关如何使用它们的详细信息，请参阅[使用 Xamarin 组件](https://github.com/SignalR/SignalR/wiki/Building-Mono.Mobile.sln)。</span><span class="sxs-lookup"><span data-stu-id="cea65-365">For more information on how to use them, see [Using Xamarin Components](https://github.com/SignalR/SignalR/wiki/Building-Mono.Mobile.sln).</span></span> <span data-ttu-id="cea65-366">当 SignalR RTW 版本可用时，这些组件将在[Xamarin 存储](https://store.xamarin.com/)中可用。</span><span class="sxs-lookup"><span data-stu-id="cea65-366">These components will be available in the [Xamarin Store](https://store.xamarin.com/) when the SignalR RTW release is available.</span></span>

<a id="portable"></a><span data-ttu-id="cea65-367">• 可移植 .NET 客户端</span><span class="sxs-lookup"><span data-stu-id="cea65-367">### Portable .NET client</span></span>

<span data-ttu-id="cea65-368">为了更好地促进跨平台开发，Silverlight、WinRT 和 Windows Phone 客户端已替换为支持以下平台的单个便携式 .NET 客户端：</span><span class="sxs-lookup"><span data-stu-id="cea65-368">To better facilitate cross-platform development, the Silverlight, WinRT and Windows Phone clients have been replaced with a single portable .NET client that supports the following platforms:</span></span>

- <span data-ttu-id="cea65-369">净 4.5</span><span class="sxs-lookup"><span data-stu-id="cea65-369">NET 4.5</span></span>
- <span data-ttu-id="cea65-370">Silverlight 5</span><span class="sxs-lookup"><span data-stu-id="cea65-370">Silverlight 5</span></span>
- <span data-ttu-id="cea65-371">WinRT （.NET 用于 Windows 应用商店应用）</span><span class="sxs-lookup"><span data-stu-id="cea65-371">WinRT (.NET for Windows Store Apps)</span></span>
- <span data-ttu-id="cea65-372">Windows Phone 8</span><span class="sxs-lookup"><span data-stu-id="cea65-372">Windows Phone 8</span></span>

<a id="selfhost"></a>

### <a name="new-self-host-package"></a><span data-ttu-id="cea65-373">新的自主机包</span><span class="sxs-lookup"><span data-stu-id="cea65-373">New Self-Host Package</span></span>

<span data-ttu-id="cea65-374">现在有一个 NuGet 包，以便更轻松地开始使用 SignalR 自主机（托管在进程或其他应用程序中的 SignalR 应用程序，而不是托管在 Web 服务器中）。</span><span class="sxs-lookup"><span data-stu-id="cea65-374">There is now a NuGet package to make it easier to get started with SignalR Self-Host (SignalR applications that are hosted in a process or other application, rather than being hosted in a web server).</span></span> <span data-ttu-id="cea65-375">要升级使用 SignalR 1.x 构建的自主机项目，请删除 Microsoft.AspNet.SignalR.Owin 包，然后添加 Microsoft.AspNet.SignalR.SelfHost 包。</span><span class="sxs-lookup"><span data-stu-id="cea65-375">To upgrade a self-host project built with SignalR 1.x, remove the Microsoft.AspNet.SignalR.Owin package, and add the Microsoft.AspNet.SignalR.SelfHost package.</span></span> <span data-ttu-id="cea65-376">有关开始使用自主机包的详细信息，请参阅[教程：SignalR 自主机](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)。</span><span class="sxs-lookup"><span data-stu-id="cea65-376">For more information on getting started with the self-host package, see [Tutorial: SignalR Self-Host](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).</span></span>

<a id="backwardcompat"></a>

### <a name="backward-compatible-server-support"></a><span data-ttu-id="cea65-377">向后兼容的服务器支持</span><span class="sxs-lookup"><span data-stu-id="cea65-377">Backward-compatible server support</span></span>

<span data-ttu-id="cea65-378">在早期版本的 SignalR 中，客户端和服务器中使用的 SignalR 包版本需要相同。</span><span class="sxs-lookup"><span data-stu-id="cea65-378">In previous versions of SignalR, the versions of the SignalR package used in the client and the server needed to be identical.</span></span> <span data-ttu-id="cea65-379">为了支持难以更新的粗客户端应用程序，SignalR 2.0 现在支持使用较新的服务器版本与较旧的客户端。</span><span class="sxs-lookup"><span data-stu-id="cea65-379">In order to support thick-client applications that would be difficult to update, SignalR 2.0 now supports using a newer server version with an older client.</span></span> <span data-ttu-id="cea65-380">**注意：SignalR 2.0 不支持使用较旧版本的较旧客户端构建的服务器。**</span><span class="sxs-lookup"><span data-stu-id="cea65-380">**Note: SignalR 2.0 does not support servers built with older versions with newer clients.**</span></span>

<a id="remove40"></a>

### <a name="removed-server-support-for-net-40"></a><span data-ttu-id="cea65-381">已删除对 .NET 4.0 的服务器支持</span><span class="sxs-lookup"><span data-stu-id="cea65-381">Removed server support for .NET 4.0</span></span>

<span data-ttu-id="cea65-382">SignalR 2.0 已放弃对服务器与 .NET 4.0 的互操作性的支持。</span><span class="sxs-lookup"><span data-stu-id="cea65-382">SignalR 2.0 has dropped support for server interoperability with .NET 4.0.</span></span> <span data-ttu-id="cea65-383">.NET 4.5 必须与 SignalR 2.0 服务器一起使用。</span><span class="sxs-lookup"><span data-stu-id="cea65-383">.NET 4.5 must be used with SignalR 2.0 servers.</span></span> <span data-ttu-id="cea65-384">信号R 2.0 仍有 .NET 4.0 客户端。</span><span class="sxs-lookup"><span data-stu-id="cea65-384">There is still a .NET 4.0 client for SignalR 2.0.</span></span>

<a id="messagelist"></a>

### <a name="sending-a-message-to-a-list-of-clients-and-groups"></a><span data-ttu-id="cea65-385">将消息发送到客户端和组列表</span><span class="sxs-lookup"><span data-stu-id="cea65-385">Sending a message to a list of clients and groups</span></span>

<span data-ttu-id="cea65-386">在 SignalR 2.0 中，可以使用客户端和组 IT 的列表发送消息。</span><span class="sxs-lookup"><span data-stu-id="cea65-386">In SignalR 2.0, it's possible to send a message using a list of client and group IDs.</span></span> <span data-ttu-id="cea65-387">以下代码段演示如何执行此操作。</span><span class="sxs-lookup"><span data-stu-id="cea65-387">The following code snippets demonstrate how to do this.</span></span>

<span data-ttu-id="cea65-388">**使用持久连接将消息发送到客户端和组的列表**</span><span class="sxs-lookup"><span data-stu-id="cea65-388">**Sending a message to a list of clients and groups using PersistentConnection**</span></span>

[!code-csharp[Main](release-notes/samples/sample11.cs)]

<span data-ttu-id="cea65-389">**使用中心向客户端和组列表发送消息**</span><span class="sxs-lookup"><span data-stu-id="cea65-389">**Sending a message to a list of clients and groups using Hubs**</span></span>

[!code-csharp[Main](release-notes/samples/sample12.cs)]

<a id="sendtouser"></a>

### <a name="sending-a-message-to-a-specific-user"></a><span data-ttu-id="cea65-390">向特定用户发送消息</span><span class="sxs-lookup"><span data-stu-id="cea65-390">Sending a message to a specific user</span></span>

<span data-ttu-id="cea65-391">此功能允许用户通过新接口 IUserIdProvider 指定用户 Id 基于 IRequest 的内容：</span><span class="sxs-lookup"><span data-stu-id="cea65-391">This feature allows users to specify what the userId is based on an IRequest via a new interface IUserIdProvider:</span></span>

<span data-ttu-id="cea65-392">**IUserId提供程序接口**</span><span class="sxs-lookup"><span data-stu-id="cea65-392">**The IUserIdProvider interface**</span></span>

[!code-csharp[Main](release-notes/samples/sample13.cs)]

<span data-ttu-id="cea65-393">默认情况下，将有一个使用用户IPrincipal.Identity.Name作为用户名的实现。</span><span class="sxs-lookup"><span data-stu-id="cea65-393">By default there will be an implementation that uses the user's IPrincipal.Identity.Name as the user name.</span></span>

<span data-ttu-id="cea65-394">在集线器中，您可以通过新的 API 向这些用户发送消息：</span><span class="sxs-lookup"><span data-stu-id="cea65-394">In hubs, you'll be able to send messages to these users via a new API:</span></span>

<span data-ttu-id="cea65-395">**使用客户端.用户 API**</span><span class="sxs-lookup"><span data-stu-id="cea65-395">**Using the Clients.User API**</span></span>

[!code-csharp[Main](release-notes/samples/sample14.cs)]

<a id="errorhandling"></a>

### <a name="better-error-handling-support"></a><span data-ttu-id="cea65-396">更好的错误处理支持</span><span class="sxs-lookup"><span data-stu-id="cea65-396">Better Error Handling Support</span></span>

<span data-ttu-id="cea65-397">用户现在可以从任何中心调用中引发**HubException。**</span><span class="sxs-lookup"><span data-stu-id="cea65-397">Users can now throw **HubException** from any hub invocation.</span></span> <span data-ttu-id="cea65-398">**HubException**的构造函数可以获取字符串消息和对象额外的错误数据。</span><span class="sxs-lookup"><span data-stu-id="cea65-398">The constructor of the **HubException** can take a string message and an object extra error data.</span></span> <span data-ttu-id="cea65-399">SignalR 将自动序列化异常并将其发送到客户端，其中它将用于拒绝/拒绝中心方法调用。</span><span class="sxs-lookup"><span data-stu-id="cea65-399">SignalR will auto-serialize the exception and send it to the client where it will be used to reject/fail the hub method invocation.</span></span>

<span data-ttu-id="cea65-400">**显示详细的集线器异常**设置与**HubException**被发送回客户端无关;它总是发送。</span><span class="sxs-lookup"><span data-stu-id="cea65-400">The **show detailed hub exceptions** setting has no bearing on **HubException** being sent back to the client or not; it is always sent.</span></span>

<span data-ttu-id="cea65-401">**显示向客户端发送 Hubexception 的服务器端代码**</span><span class="sxs-lookup"><span data-stu-id="cea65-401">**Server-side code demonstrating sending a HubException to the client**</span></span>

[!code-csharp[Main](release-notes/samples/sample15.cs)]

<span data-ttu-id="cea65-402">**显示响应从服务器发送的 HubException 的 JavaScript 客户端代码**</span><span class="sxs-lookup"><span data-stu-id="cea65-402">**JavaScript client code demonstrating responding to a HubException sent from the server**</span></span>

[!code-html[Main](release-notes/samples/sample16.html)]

<span data-ttu-id="cea65-403">**.NET 客户端代码，用于响应从服务器发送的 HubException**</span><span class="sxs-lookup"><span data-stu-id="cea65-403">**.NET client code demonstrating responding to a HubException sent from the server**</span></span>

[!code-csharp[Main](release-notes/samples/sample17.cs)]

<a id="unittesting"></a>

### <a name="easier-unit-testing-of-hubs"></a><span data-ttu-id="cea65-404">更简便的集线器单元测试</span><span class="sxs-lookup"><span data-stu-id="cea65-404">Easier unit testing of hubs</span></span>

<span data-ttu-id="cea65-405">SignalR 2.0 包括一`IHubCallerConnectionContext`个在集线器上调用的接口，该接口使创建模拟客户端调用变得更加容易。</span><span class="sxs-lookup"><span data-stu-id="cea65-405">SignalR 2.0 includes an interface called `IHubCallerConnectionContext` on Hubs that makes it easier to create mock client side invocations.</span></span> <span data-ttu-id="cea65-406">以下代码段演示使用此接口与流行的测试工具[xUnit.net](https://github.com/xunit/xunit)和[moq](https://code.google.com/p/moq/)。</span><span class="sxs-lookup"><span data-stu-id="cea65-406">The following code snippets demonstrate using this interface with popular test harnesses [xUnit.net](https://github.com/xunit/xunit) and [moq](https://code.google.com/p/moq/).</span></span>

<span data-ttu-id="cea65-407">**带xUnit.net的单元测试信号R**</span><span class="sxs-lookup"><span data-stu-id="cea65-407">**Unit testing SignalR with xUnit.net**</span></span>

[!code-csharp[Main](release-notes/samples/sample18.cs)]

<span data-ttu-id="cea65-408">**使用 moq 进行单元测试信号R**</span><span class="sxs-lookup"><span data-stu-id="cea65-408">**Unit testing SignalR with moq**</span></span>

[!code-csharp[Main](release-notes/samples/sample19.cs)]

<a id="javascripterror"></a>

### <a name="javascript-error-handling"></a><span data-ttu-id="cea65-409">JavaScript 错误处理</span><span class="sxs-lookup"><span data-stu-id="cea65-409">JavaScript error handling</span></span>

<span data-ttu-id="cea65-410">在 SignalR 2.0 中，所有 JavaScript 错误处理回调返回 JavaScript 错误对象，而不是原始字符串。</span><span class="sxs-lookup"><span data-stu-id="cea65-410">In SignalR 2.0, all JavaScript error handling callbacks return JavaScript error objects instead of raw strings.</span></span> <span data-ttu-id="cea65-411">这允许 SignalR 将更丰富的信息流向错误处理程序。</span><span class="sxs-lookup"><span data-stu-id="cea65-411">This allows SignalR to flow richer information to your error handlers.</span></span> <span data-ttu-id="cea65-412">可以从错误的`source`属性中获取内部异常。</span><span class="sxs-lookup"><span data-stu-id="cea65-412">You can get the inner exception from the `source` property of the error.</span></span>

<span data-ttu-id="cea65-413">**处理 Start.Fail 异常的 JavaScript 客户端代码**</span><span class="sxs-lookup"><span data-stu-id="cea65-413">**JavaScript client code that handles the Start.Fail exception**</span></span>

[!code-javascript[Main](release-notes/samples/sample20.js)]

<a id="TOC8"></a>
## <a name="aspnet-identity"></a><span data-ttu-id="cea65-414">ASP.NET 标识</span><span class="sxs-lookup"><span data-stu-id="cea65-414">ASP.NET Identity</span></span>

### <a name="new-aspnet-membership-system"></a><span data-ttu-id="cea65-415">新的ASP.NET会员制</span><span class="sxs-lookup"><span data-stu-id="cea65-415">New ASP.NET Membership System</span></span>

<span data-ttu-id="cea65-416">ASP.NET身份是ASP.NET应用程序的新成员资格系统。</span><span class="sxs-lookup"><span data-stu-id="cea65-416">ASP.NET Identity is the new membership system for ASP.NET applications.</span></span> <span data-ttu-id="cea65-417">ASP.NET标识使用户特定的配置文件数据与应用程序数据集成变得容易。</span><span class="sxs-lookup"><span data-stu-id="cea65-417">ASP.NET Identity makes it easy to integrate user-specific profile data with application data.</span></span> <span data-ttu-id="cea65-418">ASP.NET标识还允许您为应用程序中的用户配置文件选择持久性模型。</span><span class="sxs-lookup"><span data-stu-id="cea65-418">ASP.NET Identity also allows you to choose the persistence model for user profiles in your application.</span></span> <span data-ttu-id="cea65-419">你可以将数据存储在 SQL Server 数据库或其他数据存储中，包括 Azure 存储表等 NoSQL 数据存储。</span><span class="sxs-lookup"><span data-stu-id="cea65-419">You can store the data in a SQL Server database or another data store, including NoSQL data stores such as Azure Storage Tables.</span></span> <span data-ttu-id="cea65-420">有关详细信息，请参阅**可视化工作室 2013 中创建ASP.NET Web 项目的**[单个用户帐户](creating-web-projects-in-visual-studio.md#indauth)。</span><span class="sxs-lookup"><span data-stu-id="cea65-420">For more information, see [Individual User Accounts](creating-web-projects-in-visual-studio.md#indauth) in **Creating ASP.NET Web Projects in Visual Studio 2013**.</span></span>

### <a name="claims-based-authentication"></a><span data-ttu-id="cea65-421">基于声明的身份验证</span><span class="sxs-lookup"><span data-stu-id="cea65-421">Claims-based authentication</span></span>

<span data-ttu-id="cea65-422">ASP.NET现在支持基于声明的身份验证，其中用户的身份表示为来自受信任颁发者的一组声明。</span><span class="sxs-lookup"><span data-stu-id="cea65-422">ASP.NET now supports claims-based authentication, where the user's identity is represented as a set of claims from a trusted issuer.</span></span> <span data-ttu-id="cea65-423">用户可以使用应用程序数据库中维护的用户名和密码进行身份验证，或使用社交身份提供商（例如：微软帐户、Facebook、Google、Twitter），或者通过 Azure 活动目录或活动目录联合服务 （ADFS） 使用组织帐户。</span><span class="sxs-lookup"><span data-stu-id="cea65-423">Users can be authenticated using a username and password maintained in an application database, or using social identity providers (for example: Microsoft Accounts, Facebook, Google, Twitter), or using organizational accounts through Azure Active Directory or Active Directory Federation Services (ADFS).</span></span>

### <a name="integration-with-azure-active-directory-and-windows-server-active-directory"></a><span data-ttu-id="cea65-424">与 Azure 活动目录和 Windows 服务器活动目录集成</span><span class="sxs-lookup"><span data-stu-id="cea65-424">Integration with Azure Active Directory and Windows Server Active Directory</span></span>

<span data-ttu-id="cea65-425">现在，您可以创建ASP.NET使用 Azure 活动目录或 Windows 服务器活动目录 （AD） 进行身份验证的项目。</span><span class="sxs-lookup"><span data-stu-id="cea65-425">You can now create ASP.NET projects that use Azure Active Directory or Windows Server Active Directory (AD) for authentication.</span></span> <span data-ttu-id="cea65-426">有关详细信息，请参阅在**Visual Studio 2013 中创建ASP.NET Web 项目的**[组织帐户](creating-web-projects-in-visual-studio.md#orgauth)。</span><span class="sxs-lookup"><span data-stu-id="cea65-426">For more information, see [Organizational Accounts](creating-web-projects-in-visual-studio.md#orgauth) in **Creating ASP.NET Web Projects in Visual Studio 2013**.</span></span>

### <a name="owin-integration"></a><span data-ttu-id="cea65-427">OWIN 集成</span><span class="sxs-lookup"><span data-stu-id="cea65-427">OWIN Integration</span></span>

<span data-ttu-id="cea65-428">ASP.NET身份验证现在基于 OWIN 中间件，可用于任何基于 OWIN 的主机。</span><span class="sxs-lookup"><span data-stu-id="cea65-428">ASP.NET authentication is now based on OWIN middleware that can be used on any OWIN-based host.</span></span> <span data-ttu-id="cea65-429">有关 OWIN 的详细信息，请参阅以下[Microsoft OWIN 组件](#TOC7)部分。</span><span class="sxs-lookup"><span data-stu-id="cea65-429">For more information about OWIN, see the following [Microsoft OWIN Components](#TOC7) section.</span></span>

<a id="TOC7"></a>
## <a name="microsoft-owin-components"></a><span data-ttu-id="cea65-430">Microsoft OWIN 组件</span><span class="sxs-lookup"><span data-stu-id="cea65-430">Microsoft OWIN Components</span></span>

<span data-ttu-id="cea65-431">[.NET](http://owin.org/) （OWIN） 的开放 Web 界面定义 .NET Web 服务器和 Web 应用程序之间的抽象。</span><span class="sxs-lookup"><span data-stu-id="cea65-431">[Open Web Interface for .NET](http://owin.org/) (OWIN) defines an abstraction between .NET web servers and web applications.</span></span> <span data-ttu-id="cea65-432">OWIN 将 Web 应用程序与服务器分离，使 Web 应用程序与主机无关。</span><span class="sxs-lookup"><span data-stu-id="cea65-432">OWIN decouples the web application from the server, making web applications host-agnostic.</span></span> <span data-ttu-id="cea65-433">例如，您可以在 IIS 中托管基于 OWIN 的 Web 应用程序，也可以在自定义进程中自承载它。</span><span class="sxs-lookup"><span data-stu-id="cea65-433">For example, you can host an OWIN-based web application in IIS or self-host it in a custom process.</span></span>

<span data-ttu-id="cea65-434">Microsoft OWIN 组件（也称为 Katana 项目）中引入的更改包括新的服务器和主机组件、新的帮助器库和中间件以及新的身份验证中间件。</span><span class="sxs-lookup"><span data-stu-id="cea65-434">Changes introduced in the Microsoft OWIN components (also known as the Katana project) include new server and host components, new helper libraries and middleware, and new authentication middleware.</span></span>

<span data-ttu-id="cea65-435">有关 OWIN 和卡塔纳的更多信息，请参阅[OWIN 和卡塔纳中的新增功能](../../../aspnet/overview/owin-and-katana/index.md)。</span><span class="sxs-lookup"><span data-stu-id="cea65-435">For more information about OWIN and Katana, see [What's new in OWIN and Katana](../../../aspnet/overview/owin-and-katana/index.md).</span></span>

<span data-ttu-id="cea65-436">**注意[：OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)应用程序无法在 IIS 经典模式下运行;它们必须在集成模式下运行。**</span><span class="sxs-lookup"><span data-stu-id="cea65-436">**Note: [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) applications cannot run in IIS classic mode; they must be run in integrated mode.**</span></span>

<span data-ttu-id="cea65-437">**注意[：OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)应用程序必须完全信任地运行。**</span><span class="sxs-lookup"><span data-stu-id="cea65-437">**Note: [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) applications must be run in full trust.**</span></span>

### <a name="new-servers-and-hosts"></a><span data-ttu-id="cea65-438">新服务器和主机</span><span class="sxs-lookup"><span data-stu-id="cea65-438">New Servers and Hosts</span></span>

<span data-ttu-id="cea65-439">使用此版本，添加了新的组件以启用自承载方案。</span><span class="sxs-lookup"><span data-stu-id="cea65-439">With this release, new components were added to enable self-host scenarios.</span></span> <span data-ttu-id="cea65-440">这些组件包括以下 NuGet 包：</span><span class="sxs-lookup"><span data-stu-id="cea65-440">These components include the following NuGet packages:</span></span>

- <span data-ttu-id="cea65-441">**微软.Owin.Host.httpListener**.</span><span class="sxs-lookup"><span data-stu-id="cea65-441">**Microsoft.Owin.Host.HttpListener**.</span></span> <span data-ttu-id="cea65-442">提供一个 OWIN 服务器，该服务器使用**HttpListener**侦听 HTTP 请求并将其定向到 OWIN 管道中。</span><span class="sxs-lookup"><span data-stu-id="cea65-442">Provides an OWIN server that uses **HttpListener** to listen for HTTP requests and direct them into the OWIN pipeline.</span></span>
- <span data-ttu-id="cea65-443">**Microsoft.Owin.Hosting**为希望在自定义进程中自承载 OWIN 管道（如控制台应用程序或 Windows 服务）的开发人员提供一个库。</span><span class="sxs-lookup"><span data-stu-id="cea65-443">**Microsoft.Owin.Hosting** Provides a library for developers who wish to self-host an OWIN pipeline in a custom process, such as a console application or Windows service.</span></span>
- <span data-ttu-id="cea65-444">**奥温霍斯**。</span><span class="sxs-lookup"><span data-stu-id="cea65-444">**OwinHost**.</span></span> <span data-ttu-id="cea65-445">提供一个独立的可执行文件，用于包装`Microsoft.Owin.Hosting`并允许您自承载 OWIN 管道，而无需编写自定义主机应用程序。</span><span class="sxs-lookup"><span data-stu-id="cea65-445">Provides a stand-alone executable that wraps `Microsoft.Owin.Hosting` and lets you self-host an OWIN pipeline without having to write a custom host application.</span></span>

<span data-ttu-id="cea65-446">此外，`Microsoft.Owin.Host.SystemWeb`该包现在使中间件能够向**SystemWeb**服务器提供提示，指示应在特定的ASP.NET管道阶段调用中间件。</span><span class="sxs-lookup"><span data-stu-id="cea65-446">In addition, the `Microsoft.Owin.Host.SystemWeb` package now enables middleware to provide hints to the **SystemWeb** server, indicating that the middleware should be called during a specific ASP.NET pipeline stage.</span></span> <span data-ttu-id="cea65-447">此功能对于身份验证中间件特别有用，该中间件应在ASP.NET管道中早期运行。</span><span class="sxs-lookup"><span data-stu-id="cea65-447">This feature is particularly useful for authentication middleware, which should run early in the ASP.NET pipeline.</span></span>

### <a name="helper-libraries-and-middleware"></a><span data-ttu-id="cea65-448">帮助库和中间件</span><span class="sxs-lookup"><span data-stu-id="cea65-448">Helper Libraries and Middleware</span></span>

<span data-ttu-id="cea65-449">尽管只能使用 OWIN 规范中的函数和类型定义编写 OWIN 组件，但新`Microsoft.Owin`包提供了一组更用户友好的抽象。</span><span class="sxs-lookup"><span data-stu-id="cea65-449">Although you can write OWIN components using only the function and type definitions from the OWIN specification, the new `Microsoft.Owin` package provides a more user-friendly set of abstractions.</span></span> <span data-ttu-id="cea65-450">此包将几个较早的包（例如 ，）`Owin.Extensions``Owin.Types`合并到单个结构良好的对象模型中，然后其他 OWIN 组件可以轻松地使用该模型。</span><span class="sxs-lookup"><span data-stu-id="cea65-450">This package combines several earlier packages (e.g., `Owin.Extensions`, `Owin.Types`) into a single, well-structured object model that can then be easily used by other OWIN components.</span></span> <span data-ttu-id="cea65-451">事实上，大多数 Microsoft OWIN 组件现在都使用此包。</span><span class="sxs-lookup"><span data-stu-id="cea65-451">In fact, the majority of Microsoft OWIN components now use this package.</span></span>

> [!NOTE]
> <span data-ttu-id="cea65-452">[OWIN](http://www.owin.org)应用程序无法在 IIS 经典模式下运行;它们必须在集成模式下运行。</span><span class="sxs-lookup"><span data-stu-id="cea65-452">[OWIN](http://www.owin.org) applications cannot run in IIS classic mode; they must be run in integrated mode.</span></span>

> [!NOTE]
> <span data-ttu-id="cea65-453">[OWIN](http://www.owin.org)应用程序必须完全信任地运行。</span><span class="sxs-lookup"><span data-stu-id="cea65-453">[OWIN](http://www.owin.org) applications must be run in full trust.</span></span>

<span data-ttu-id="cea65-454">此版本还包括 Microsoft.Owin.诊断包，其中包括用于验证正在运行的 OWIN 应用程序的中间件，以及帮助调查故障的错误页中间件。</span><span class="sxs-lookup"><span data-stu-id="cea65-454">This release also includes the Microsoft.Owin.Diagnostics package, which includes middleware to validate a running OWIN application, plus error-page middleware to help investigate failures.</span></span>

### <a name="authentication-components"></a><span data-ttu-id="cea65-455">身份验证组件</span><span class="sxs-lookup"><span data-stu-id="cea65-455">Authentication Components</span></span>

<span data-ttu-id="cea65-456">以下身份验证组件可用。</span><span class="sxs-lookup"><span data-stu-id="cea65-456">The following authentication components are available.</span></span>

- <span data-ttu-id="cea65-457">**微软.Owin.安全.主动目录**.</span><span class="sxs-lookup"><span data-stu-id="cea65-457">**Microsoft.Owin.Security.ActiveDirectory**.</span></span> <span data-ttu-id="cea65-458">使用内部部署或基于云的目录服务启用身份验证。</span><span class="sxs-lookup"><span data-stu-id="cea65-458">Enables authentication using on-premise or cloud-based directory services.</span></span>
- <span data-ttu-id="cea65-459">**微软.Owin.Security.cookies**支持使用Cookie进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="cea65-459">**Microsoft.Owin.Security.Cookies** Enables authentication using cookies.</span></span> <span data-ttu-id="cea65-460">此包以前命名为`Microsoft.Owin.Security.Forms`。</span><span class="sxs-lookup"><span data-stu-id="cea65-460">This package was previously named `Microsoft.Owin.Security.Forms`.</span></span>
- <span data-ttu-id="cea65-461">**微软.Owin.Security.Facebook**使用Facebook基于OAuth的服务启用身份验证。</span><span class="sxs-lookup"><span data-stu-id="cea65-461">**Microsoft.Owin.Security.Facebook** Enables authentication using Facebook's OAuth-based service.</span></span>
- <span data-ttu-id="cea65-462">**微软.Owin.Security.谷歌**使用谷歌基于OpenID的服务启用身份验证。</span><span class="sxs-lookup"><span data-stu-id="cea65-462">**Microsoft.Owin.Security.Google** Enables authentication using Google's OpenID-based service.</span></span>
- <span data-ttu-id="cea65-463">**微软.Owin.Security.Jwt**启用使用 JWT 令牌的身份验证。</span><span class="sxs-lookup"><span data-stu-id="cea65-463">**Microsoft.Owin.Security.Jwt** Enables authentication using JWT tokens.</span></span>
- <span data-ttu-id="cea65-464">**微软.Owin.Security.微软帐户**启用使用微软帐户进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="cea65-464">**Microsoft.Owin.Security.MicrosoftAccount** Enables authentication using Microsoft accounts.</span></span>
- <span data-ttu-id="cea65-465">**微软.奥温.安全.奥乌斯**.</span><span class="sxs-lookup"><span data-stu-id="cea65-465">**Microsoft.Owin.Security.OAuth**.</span></span> <span data-ttu-id="cea65-466">提供 OAuth 授权服务器以及用于验证无记名令牌的中间件。</span><span class="sxs-lookup"><span data-stu-id="cea65-466">Provides an OAuth authorization server as well as middleware for authenticating bearer tokens.</span></span>
- <span data-ttu-id="cea65-467">**微软.Owin.Security.Twitter**使用Twitter基于OAuth的服务进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="cea65-467">**Microsoft.Owin.Security.Twitter** Enables authentication using Twitter's OAuth-based service.</span></span>

<span data-ttu-id="cea65-468">此版本还包括包`Microsoft.Owin.Cors`，其中包含用于处理跨源 HTTP 请求的中间件。</span><span class="sxs-lookup"><span data-stu-id="cea65-468">This release also includes the `Microsoft.Owin.Cors` package, which contains middleware for processing cross-origin HTTP requests.</span></span>

> [!NOTE]
> <span data-ttu-id="cea65-469">在 Visual Studio 2013 的最终版本中删除了对 JWT 签名的支持。</span><span class="sxs-lookup"><span data-stu-id="cea65-469">Support for JWT signing has been removed in the final version of Visual Studio 2013.</span></span>

<a id="ef6"></a>
## <a name="entity-framework-6"></a><span data-ttu-id="cea65-470">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="cea65-470">Entity Framework 6</span></span>

<span data-ttu-id="cea65-471">有关实体框架 6 中的新功能和其他更改的列表，请参阅[实体框架版本历史记录](https://msdn.com/data/jj574253)。</span><span class="sxs-lookup"><span data-stu-id="cea65-471">For a list of new features and other changes in Entity Framework 6, see [Entity Framework Version History](https://msdn.com/data/jj574253).</span></span>

<a id="TOC14"></a>
## <a name="aspnet-razor-3"></a><span data-ttu-id="cea65-472">ASP.NET剃刀 3</span><span class="sxs-lookup"><span data-stu-id="cea65-472">ASP.NET Razor 3</span></span>

<span data-ttu-id="cea65-473">ASP.NET Razor 3 包括以下新功能：</span><span class="sxs-lookup"><span data-stu-id="cea65-473">ASP.NET Razor 3 includes the following new features:</span></span>

- <span data-ttu-id="cea65-474">支持选项卡编辑。</span><span class="sxs-lookup"><span data-stu-id="cea65-474">Support for Tab editing.</span></span> <span data-ttu-id="cea65-475">以前，使用"**保留选项卡**"选项时，Visual Studio 中的 **"格式文档**"命令、自动缩进和自动格式设置无法正常工作。</span><span class="sxs-lookup"><span data-stu-id="cea65-475">Previously, the **Format Document** command, auto indenting, and auto formatting in Visual Studio did not work correctly when using the **Keep Tabs** option.</span></span> <span data-ttu-id="cea65-476">此更改纠正了用于选项卡格式的 Razor 代码的可视化工作室格式。</span><span class="sxs-lookup"><span data-stu-id="cea65-476">This change corrects Visual Studio formatting for Razor code for tab formatting.</span></span>
- <span data-ttu-id="cea65-477">生成链接时支持 URL 重写规则。</span><span class="sxs-lookup"><span data-stu-id="cea65-477">Support for URL Rewrite rules when generating links.</span></span>
- <span data-ttu-id="cea65-478">删除安全透明属性。</span><span class="sxs-lookup"><span data-stu-id="cea65-478">Removal of security transparent attribute.</span></span>
  > [!NOTE]
  > <span data-ttu-id="cea65-479">这是一个重大更改，使 Razor 3 与 MVC4 和更早版本不兼容，而 Razor 2 与 MVC5 或针对 MVC5 编译的程序集不兼容。</span><span class="sxs-lookup"><span data-stu-id="cea65-479">This is a breaking change, and makes Razor 3 incompatible with MVC4 and earlier, while Razor 2 is incompatible with MVC5 or assemblies compiled against MVC5.</span></span>

<span data-ttu-id="cea65-480">Razor 3 问题修复在 Visual Studio 2013 从预发行版本可以[在这里](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Resolved%7cClosed&type=All&priority=All&release=All%7cv5.0%2bPreview%7cv5.0%2bRC%7cv5.0%2bRTM&assignedTo=All&component=Web%2bPages%252fRazor&reasonClosed=Fixed&sortField=LastUpdatedDate&sortDirection=Descending&page=0)找到.</span><span class="sxs-lookup"><span data-stu-id="cea65-480">Razor 3 issues fixed in Visual Studio 2013 from pre-release versions can be found [here](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Resolved%7cClosed&type=All&priority=All&release=All%7cv5.0%2bPreview%7cv5.0%2bRC%7cv5.0%2bRTM&assignedTo=All&component=Web%2bPages%252fRazor&reasonClosed=Fixed&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

<a id="TOC15"></a>
## <a name="aspnet-app-suspend"></a><span data-ttu-id="cea65-481">ASP.NET应用挂起</span><span class="sxs-lookup"><span data-stu-id="cea65-481">ASP.NET App Suspend</span></span>

<span data-ttu-id="cea65-482">ASP.NET应用程序挂起是 .NET Framework 4.5.1 中的一项改变游戏规则的功能，它从根本上改变了在一台计算机上托管大量ASP.NET站点的用户体验和经济模型。</span><span class="sxs-lookup"><span data-stu-id="cea65-482">ASP.NET App Suspend is a game-changing feature in the .NET Framework 4.5.1 that radically changes the user experience and economic model for hosting large numbers of ASP.NET sites on a single machine.</span></span> <span data-ttu-id="cea65-483">有关详细信息，请参阅[ASP.NET应用程序挂起 – 响应式共享 .NET Web 托管](https://blogs.msdn.com/b/dotnet/archive/2013/10/09/asp-net-app-suspend-responsive-shared-net-web-hosting.aspx)。</span><span class="sxs-lookup"><span data-stu-id="cea65-483">For more information, see [ASP.NET App Suspend – responsive shared .NET web hosting](https://blogs.msdn.com/b/dotnet/archive/2013/10/09/asp-net-app-suspend-responsive-shared-net-web-hosting.aspx).</span></span>

<a id="knownissues"></a>
## <a name="known-issues-and-breaking-changes"></a><span data-ttu-id="cea65-484">已知问题和重大更改</span><span class="sxs-lookup"><span data-stu-id="cea65-484">Known Issues and Breaking Changes</span></span>

<span data-ttu-id="cea65-485">本节介绍视觉工作室 2013 ASP.NET和 Web 工具中的已知问题和重大更改。</span><span class="sxs-lookup"><span data-stu-id="cea65-485">This section describes known issues and breaking changes in the ASP.NET and Web Tools for Visual Studio 2013.</span></span>

### <a name="nuget"></a><span data-ttu-id="cea65-486">NuGet</span><span class="sxs-lookup"><span data-stu-id="cea65-486">NuGet</span></span>

- <span data-ttu-id="cea65-487">[使用 SLN 文件时，新包还原在 Mono 上不起作用](https://nuget.codeplex.com/workitem/3596)， 将在即将进行的 nuget.exe 下载和[NuGet.CommandLine 包](http://www.nuget.org/packages/NuGet.CommandLine/)更新中修复。</span><span class="sxs-lookup"><span data-stu-id="cea65-487">[New package restore doesn't work on Mono when using SLN file](https://nuget.codeplex.com/workitem/3596) – will be fixed in an upcoming nuget.exe download and [NuGet.CommandLine package](http://www.nuget.org/packages/NuGet.CommandLine/) update.</span></span>
- <span data-ttu-id="cea65-488">[新的包还原与 Wix 项目不起作用](https://nuget.codeplex.com/workitem/3598)- 将在即将进行的 nuget.exe 下载和[NuGet.CommandLine 包](http://www.nuget.org/packages/NuGet.CommandLine/)更新中修复。</span><span class="sxs-lookup"><span data-stu-id="cea65-488">[New package restore doesn't work with Wix projects](https://nuget.codeplex.com/workitem/3598) – will be fixed in an upcoming nuget.exe download and [NuGet.CommandLine package](http://www.nuget.org/packages/NuGet.CommandLine/) update.</span></span>
- <span data-ttu-id="cea65-489">[自动包还原在解决方案文件夹下的项目不起作用](https://nuget.codeplex.com/workitem/3625)， 将在 NuGet 2.8 中修复。</span><span class="sxs-lookup"><span data-stu-id="cea65-489">[Automatic Package restore doesn't work for projects under a solution folder](https://nuget.codeplex.com/workitem/3625) – will be fixed in NuGet 2.8.</span></span>

### <a name="aspnet-web-api"></a><span data-ttu-id="cea65-490">ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="cea65-490">ASP.NET Web API</span></span>

1. <span data-ttu-id="cea65-491">`ODataQueryOptions<T>.ApplyTo(IQueryable)`不会总是返回`IQueryable<T>`，因为我们添加了 对`$select`和`$expand`的支持。</span><span class="sxs-lookup"><span data-stu-id="cea65-491">`ODataQueryOptions<T>.ApplyTo(IQueryable)` doesn't return `IQueryable<T>` always, as we added support for `$select` and `$expand`.</span></span>

    <span data-ttu-id="cea65-492">我们以前的样本`ODataQueryOptions<T>`总是将返回值从`ApplyTo`转换为`IQueryable<T>`。</span><span class="sxs-lookup"><span data-stu-id="cea65-492">Our earlier samples for `ODataQueryOptions<T>` always casted the return value from `ApplyTo` to `IQueryable<T>`.</span></span> <span data-ttu-id="cea65-493">这在早期`$filter`起作用，因为我们支持之前的查询选项 （、、、、）`$orderby``$skip``$top`不会更改查询的形状。</span><span class="sxs-lookup"><span data-stu-id="cea65-493">This worked earlier because the query options that we supported earlier (`$filter`, `$orderby`, `$skip`, `$top`) do not change the shape of the query.</span></span> <span data-ttu-id="cea65-494">`$select`现在，我们支持`$expand`，并从`ApplyTo`返回值将`IQueryable<T>`并不总是。</span><span class="sxs-lookup"><span data-stu-id="cea65-494">Now that we support `$select` and `$expand` the return value from `ApplyTo` will not be `IQueryable<T>` always.</span></span>

    [!code-csharp[Main](release-notes/samples/sample21.cs)]

    <span data-ttu-id="cea65-495">如果使用之前的示例代码，则如果客户端未发送`$select`和`$expand`，它将继续工作。</span><span class="sxs-lookup"><span data-stu-id="cea65-495">If you are using the sample code from earlier, it will continue working if the client does not send `$select` and `$expand`.</span></span> <span data-ttu-id="cea65-496">但是，如果您希望支持`$select`，并且`$expand`必须将该代码更改为此代码。</span><span class="sxs-lookup"><span data-stu-id="cea65-496">However, if you wish to support `$select` and `$expand` you have to change that code to this.</span></span>

    [!code-csharp[Main](release-notes/samples/sample22.cs)]
2. <span data-ttu-id="cea65-497">**请求.Url 或请求上下文.Url 在批处理请求期间为空**</span><span class="sxs-lookup"><span data-stu-id="cea65-497">**Request.Url or RequestContext.Url is null during a batch request**</span></span>

    <span data-ttu-id="cea65-498">在批处理方案中 **，UrlHelper**从**请求.Url**或**请求上下文.Url**访问时为空。</span><span class="sxs-lookup"><span data-stu-id="cea65-498">In a batching scenario, **UrlHelper** is null when accessed from **Request.Url** or **RequestContext.Url**.</span></span>

    <span data-ttu-id="cea65-499">此问题当前在此处跟踪[：BatchRequestContext.Url 对于批处理请求为空](http://aspnetwebstack.codeplex.com/workitem/1301)。</span><span class="sxs-lookup"><span data-stu-id="cea65-499">This issue is currently tracked here: [BatchRequestContext.Url is null for batching request](http://aspnetwebstack.codeplex.com/workitem/1301).</span></span>

    <span data-ttu-id="cea65-500">此问题的解决方法是创建**UrlHelper**的新实例，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="cea65-500">The workaround for this issue is to create a new instance of **UrlHelper**, as in the following example:</span></span>

    <span data-ttu-id="cea65-501">**创建 UrlHelper 的新实例**</span><span class="sxs-lookup"><span data-stu-id="cea65-501">**Creating a new instance of UrlHelper**</span></span>

    [!code-csharp[Main](release-notes/samples/sample23.cs)]

### <a name="aspnet-mvc"></a><span data-ttu-id="cea65-502">ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="cea65-502">ASP.NET MVC</span></span>

1. <span data-ttu-id="cea65-503">使用 MVC5 和 OrgAuth 时，如果您有执行 AntiForgerToken 验证的视图，则当您将数据发布到视图时，可能会遇到以下错误：</span><span class="sxs-lookup"><span data-stu-id="cea65-503">When using MVC5 and OrgAuth, if you have views which do AntiForgerToken validation, you might come across the following error when you post data to the view:</span></span>

    <span data-ttu-id="cea65-504">**错误**：</span><span class="sxs-lookup"><span data-stu-id="cea65-504">**Error**:</span></span>

    <span data-ttu-id="cea65-505">*'/' 应用程序中出现服务器错误。*</span><span class="sxs-lookup"><span data-stu-id="cea65-505">*Server Error in '/' Application.*</span></span>

    <span data-ttu-id="cea65-506"><em>所提供的索赔身份上不存在<http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier>类型""<https://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider>或""的索赔。要使用基于声明的身份验证启用反伪造令牌支持，请验证已配置的声明提供程序是否在它生成的声明标识实例上同时提供这两种声明。如果配置的声明提供程序使用不同的声明类型作为唯一标识符，则可以通过设置静态属性 AntiForgeryConfig.唯一ClaimType标识符来配置它。</em></span><span class="sxs-lookup"><span data-stu-id="cea65-506"><em>A claim of type '<http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier>' or '<https://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider>' was not present on the provided ClaimsIdentity. To enable anti-forgery token support with claims-based authentication, please verify that the configured claims provider is providing both of these claims on the ClaimsIdentity instances it generates. If the configured claims provider instead uses a different claim type as a unique identifier, it can be configured by setting the static property AntiForgeryConfig.UniqueClaimTypeIdentifier.</em></span></span>

    <span data-ttu-id="cea65-507">**解决方法**：</span><span class="sxs-lookup"><span data-stu-id="cea65-507">**Workaround**:</span></span>

    <span data-ttu-id="cea65-508">在 Global.asax 中添加以下行以修复它：</span><span class="sxs-lookup"><span data-stu-id="cea65-508">Add the following line in Global.asax to fix it:</span></span>

    `AntiForgeryConfig.UniqueClaimTypeIdentifier = ClaimTypes.Name;`

    <span data-ttu-id="cea65-509">这将在下一个版本中修复。</span><span class="sxs-lookup"><span data-stu-id="cea65-509">This will be fixed for the next release.</span></span>
2. <span data-ttu-id="cea65-510">将 MVC4 应用升级到 MVC5 后，生成解决方案并启动它。</span><span class="sxs-lookup"><span data-stu-id="cea65-510">After upgrading an MVC4 app to MVC5, build the solution and launch it.</span></span> <span data-ttu-id="cea65-511">您应该会看到以下错误：</span><span class="sxs-lookup"><span data-stu-id="cea65-511">You should see the following error:</span></span>

    <span data-ttu-id="cea65-512">[A]系统.Web.WebPages.Razor.配置.Host节不能强制转换为 [B_system.Web.Web.WebPages.Razor.配置.主机节。</span><span class="sxs-lookup"><span data-stu-id="cea65-512">[A]System.Web.WebPages.Razor.Configuration.HostSection cannot be cast to [B]System.Web.WebPages.Razor.Configuration.HostSection.</span></span> <span data-ttu-id="cea65-513">类型 A 源自 "系统.Web.WebPages.Razor" 版本=2.0.0.0，区域性=中性，PublicKeyToken=31bf3856ad364e35"在上下文"默认"的位置\_"C：_windows.Net_大会_GAC MSIL_System.WebPages.Razor_v4.0.0\_\_\_31bf3856ad36e35_系统.WebPages.剃须刀.剃须刀。"</span><span class="sxs-lookup"><span data-stu-id="cea65-513">Type A originates from 'System.Web.WebPages.Razor, Version=2.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' in the context 'Default' at location 'C:\windows\Microsoft.Net\assembly\GAC\_MSIL\System.Web.WebPages.Razor\v4.0\_2.0.0.0\_\_31bf3856ad364e35\System.Web.WebPages.Razor.dll'.</span></span> <span data-ttu-id="cea65-514">类型 B 源自 'System.Web.WebPages.Razor， 版本=3.0.0.0， 区域性= 中性， PublicKeyToken_31bf3856ad364e35"在上下文"默认"的位置"C：_Windows_Microsoft.NET_Framework_v4.0.30319\临时ASP.NET文件\root_6d 05bbd0_e8b5908e_assembly_dl3_c9cbca63_f8910382\_6273ce01_System.WebPages.Razor.dll'。</span><span class="sxs-lookup"><span data-stu-id="cea65-514">Type B originates from 'System.Web.WebPages.Razor, Version=3.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' in the context 'Default' at location 'C:\Windows\Microsoft.NET\Framework\v4.0.30319\Temporary ASP.NET Files\root\6d05bbd0\e8b5908e\assembly\dl3\c9cbca63\f8910382\_6273ce01\System.Web.WebPages.Razor.dll'.</span></span>

    <span data-ttu-id="cea65-515">要修复上述错误，请打开项目中*的所有*Web.config 文件（包括"视图"文件夹中的文件），并执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="cea65-515">To fix the above error, open *all* the Web.config files (including the ones in the Views folder) in your project and do the following:</span></span>

   1. <span data-ttu-id="cea65-516">将"System.Web.Mvc"版本"4.0.0.0"的所有匹配项更新为"5.0.0.0"。</span><span class="sxs-lookup"><span data-stu-id="cea65-516">Update all occurrences of version "4.0.0.0" of "System.Web.Mvc" to "5.0.0.0".</span></span>
   2. <span data-ttu-id="cea65-517">更新&quot;"系统.Web.Helpers"、系统.Web.WebPages&quot;和&quot;系统.Web.WebPages.Razor&quot;到"3.0.0.0"版本的所有匹配项</span><span class="sxs-lookup"><span data-stu-id="cea65-517">Update all occurrences of version "2.0.0.0" of "System.Web.Helpers", &quot;System.Web.WebPages&quot; and &quot;System.Web.WebPages.Razor&quot; to "3.0.0.0"</span></span>

      <span data-ttu-id="cea65-518">例如，在进行上述更改后，程序集绑定应如下所示：</span><span class="sxs-lookup"><span data-stu-id="cea65-518">For example, after you make the above changes, the assembly bindings should look like this:</span></span>

      [!code-xml[Main](release-notes/samples/sample24.xml)]

      <span data-ttu-id="cea65-519">有关将 MVC 4 项目升级到 MVC 5 的信息，请参阅[如何将ASP.NET MVC 4 和 Web API 项目升级到ASP.NET MVC 5 和 Web API 2](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md)。</span><span class="sxs-lookup"><span data-stu-id="cea65-519">For information on upgrading MVC 4 projects to MVC 5, see [How to Upgrade an ASP.NET MVC 4 and Web API Project to ASP.NET MVC 5 and Web API 2](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md).</span></span>
3. <span data-ttu-id="cea65-520">当将客户端验证与 jQuery 不显眼验证一起使用时，对于类型="数字"的 HTML 输入元素，验证消息有时不正确。</span><span class="sxs-lookup"><span data-stu-id="cea65-520">When using client-side validation with jQuery Unobtrusive Validation, the validation message is sometimes incorrect for an HTML input element with type='number'.</span></span> <span data-ttu-id="cea65-521">输入无效号码时将显示所需值的验证错误（"需要"年龄字段），而不是需要有效编号的正确消息。</span><span class="sxs-lookup"><span data-stu-id="cea65-521">The validation error for a required value ("The Age field is required") is shown when an invalid number is entered instead of the correct message that a valid number is required.</span></span>

    <span data-ttu-id="cea65-522">在"创建"和"编辑"视图中具有整数属性的模型的脚手架代码通常会产生此问题。</span><span class="sxs-lookup"><span data-stu-id="cea65-522">This issue is commonly found with scaffolded code for a model with an integer property on the Create and Edit views.</span></span>

    <span data-ttu-id="cea65-523">要解决此问题，从以下方面更改编辑器帮助程序：</span><span class="sxs-lookup"><span data-stu-id="cea65-523">To work around this issue, change the editor helper from:</span></span>

    `@Html.EditorFor(person => person.Age)`

    <span data-ttu-id="cea65-524">更改为：</span><span class="sxs-lookup"><span data-stu-id="cea65-524">To:</span></span>

    `@Html.TextBoxFor(person => person.Age)`
4. <span data-ttu-id="cea65-525">ASP.NET MVC 5 不再支持部分信任。</span><span class="sxs-lookup"><span data-stu-id="cea65-525">ASP.NET MVC 5 no longer supports partial trust.</span></span> <span data-ttu-id="cea65-526">链接到 MVC 或 WebAPI 二进制文件的项目应删除[安全透明](https://msdn.microsoft.com/library/system.security.securitytransparentattribute.aspx)属性和["允许部分受信任的呼叫者"](https://msdn.microsoft.com/library/system.security.allowpartiallytrustedcallersattribute.aspx)属性。</span><span class="sxs-lookup"><span data-stu-id="cea65-526">Projects linking to the MVC or WebAPI binaries should remove the [SecurityTransparent](https://msdn.microsoft.com/library/system.security.securitytransparentattribute.aspx) attribute and the [AllowPartiallyTrustedCallers](https://msdn.microsoft.com/library/system.security.allowpartiallytrustedcallersattribute.aspx) attribute.</span></span> <span data-ttu-id="cea65-527">删除这些属性将消除编译器错误，如下所示。</span><span class="sxs-lookup"><span data-stu-id="cea65-527">Removing these attributes will eliminate compiler errors such as the following.</span></span>

    `Attempt by security transparent method ‘MyComponent' to access security critical type 'System.Web.Mvc.MvcHtmlString' failed. Assembly 'PagedList.Mvc, Version=4.3.0.0, Culture=neutral, PublicKeyToken=abbb863e9397c5e1' is marked with the AllowPartiallyTrustedCallersAttribute, and uses the level 2 security transparency model. Level 2 transparency causes all methods in AllowPartiallyTrustedCallers assemblies to become security transparent by default, which may be the cause of this exception.`

    > <span data-ttu-id="cea65-528">请注意，作为副作用，您不能在同一应用程序中使用 4.0 和 5.0 程序集。</span><span class="sxs-lookup"><span data-stu-id="cea65-528">Note, as a side effect of this you cannot use 4.0 and 5.0 assemblies in the same application.</span></span> <span data-ttu-id="cea65-529">您需要将所有它们更新为 5.0。</span><span class="sxs-lookup"><span data-stu-id="cea65-529">You need to update all of them to 5.0.</span></span>

### <a name="spa-template-with-facebook-authorization-may-cause-instability-in-ie-while-the-web-site-is-hosted-in-intranet-zone"></a><span data-ttu-id="cea65-530">具有 Facebook 授权的 SPA 模板可能会导致 IE 不稳定，而网站托管在 Intranet 区域中</span><span class="sxs-lookup"><span data-stu-id="cea65-530">SPA Template with Facebook authorization may cause instability in IE while the web site is hosted in intranet zone</span></span>

<span data-ttu-id="cea65-531">SPA 模板提供带 Facebook 的外部登录。</span><span class="sxs-lookup"><span data-stu-id="cea65-531">The SPA template provides external log in with Facebook.</span></span> <span data-ttu-id="cea65-532">当使用模板创建的项目在本地运行时，登录可能会导致 IE 崩溃。</span><span class="sxs-lookup"><span data-stu-id="cea65-532">When the project created with the template is running locally, signing in may cause IE to crash.</span></span>

<span data-ttu-id="cea65-533">解决方案：</span><span class="sxs-lookup"><span data-stu-id="cea65-533">Solution:</span></span>

1. <span data-ttu-id="cea65-534">在互联网区域托管网站;或</span><span class="sxs-lookup"><span data-stu-id="cea65-534">Host the web site in internet zone; or</span></span>

2. <span data-ttu-id="cea65-535">在 IE 以外的浏览器中测试方案。</span><span class="sxs-lookup"><span data-stu-id="cea65-535">Test the scenario in a browser other than IE.</span></span>

### <a name="web-forms-scaffolding"></a><span data-ttu-id="cea65-536">Web 窗体基架</span><span class="sxs-lookup"><span data-stu-id="cea65-536">Web Forms Scaffolding</span></span>

<span data-ttu-id="cea65-537">Web 窗体基架已从 VS2013 中删除，将来将更新为 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="cea65-537">Web Forms Scaffolding has been removed from VS2013 and will be available in a future update to Visual Studio.</span></span> <span data-ttu-id="cea65-538">但是，您仍可以通过添加 MVC 依赖项和生成 MVC 基架来在 Web 窗体项目中使用基架。</span><span class="sxs-lookup"><span data-stu-id="cea65-538">However, you can still use scaffolding within a Web Forms project by adding MVC dependencies and generating scaffolding for MVC.</span></span> <span data-ttu-id="cea65-539">您的项目将包含 Web 窗体和 MVC 的组合。</span><span class="sxs-lookup"><span data-stu-id="cea65-539">Your project will contain a combination of Web Forms and MVC.</span></span>

<span data-ttu-id="cea65-540">要将 MVC 添加到 Web 窗体项目，请添加新的脚手架项，然后选择**MVC 5 依赖项**。</span><span class="sxs-lookup"><span data-stu-id="cea65-540">To add MVC to your Web Forms project, add a new scaffolded item and select **MVC 5 Dependencies**.</span></span> <span data-ttu-id="cea65-541">根据是否需要所有内容文件（如脚本）选择"最小"或"完整"。</span><span class="sxs-lookup"><span data-stu-id="cea65-541">Select either Minimal or Full depending on whether you need all of the content files, such as scripts.</span></span> <span data-ttu-id="cea65-542">然后，为 MVC 添加一个基架项，这将在项目中创建视图和控制器。</span><span class="sxs-lookup"><span data-stu-id="cea65-542">Then, add a scaffolded item for MVC, which will create views and a controller in your project.</span></span>

### <a name="mvc-and-web-api-scaffolding---http-404-not-found-error"></a><span data-ttu-id="cea65-543">MVC 和 Web API 基架 - HTTP 404，未找到错误</span><span class="sxs-lookup"><span data-stu-id="cea65-543">MVC and Web API Scaffolding - HTTP 404, Not Found error</span></span>

<span data-ttu-id="cea65-544">如果在向项目添加基架项时遇到错误，则项目可能会处于不一致状态。</span><span class="sxs-lookup"><span data-stu-id="cea65-544">If an error is encountered when adding a scaffolded item to a project, it is possible your project will be left in an inconsistent state.</span></span> <span data-ttu-id="cea65-545">对基架所做的一些更改将回滚，但其他更改（如已安装的 NuGet 包）将不会回滚。</span><span class="sxs-lookup"><span data-stu-id="cea65-545">Some of the changes made be scaffolding will be rolled back but other changes, such as the installed NuGet packages, will not be rolled back.</span></span> <span data-ttu-id="cea65-546">如果路由配置更改回滚，则用户在导航到基架项目时将收到 HTTP 404 错误。</span><span class="sxs-lookup"><span data-stu-id="cea65-546">If the routing configuration changes are rolled back, users will receive an HTTP 404 error when navigating to scaffolded items.</span></span>

<span data-ttu-id="cea65-547">解决方法：</span><span class="sxs-lookup"><span data-stu-id="cea65-547">Workaround:</span></span>

- <span data-ttu-id="cea65-548">要修复 MVC 的此错误，请添加新的脚手架项并选择 MVC 5 依赖项（最小或完整）。</span><span class="sxs-lookup"><span data-stu-id="cea65-548">To fix this error for MVC, add a new scaffolded item and select MVC 5 Dependencies (either Minimal or Full).</span></span> <span data-ttu-id="cea65-549">此过程将添加项目所需的所有更改。</span><span class="sxs-lookup"><span data-stu-id="cea65-549">This process will add all of the required changes to your project.</span></span>
- <span data-ttu-id="cea65-550">要修复 Web API 的此错误，本文：</span><span class="sxs-lookup"><span data-stu-id="cea65-550">To fix this error for Web API:</span></span>

  1. <span data-ttu-id="cea65-551">将 WebApiConfig 类添加到项目中。</span><span class="sxs-lookup"><span data-stu-id="cea65-551">Add the WebApiConfig class to your project.</span></span>

      [!code-csharp[Main](release-notes/samples/sample25.cs)]

      [!code-vb[Main](release-notes/samples/sample26.vb)]
  2. <span data-ttu-id="cea65-552">在 Global.asax 中的应用程序\_启动方法中配置 WebApiConfig.注册，如下所示：</span><span class="sxs-lookup"><span data-stu-id="cea65-552">Configure WebApiConfig.Register in the Application\_Start method in Global.asax as follows:</span></span>

      [!code-csharp[Main](release-notes/samples/sample27.cs)]

      [!code-vb[Main](release-notes/samples/sample28.vb)]

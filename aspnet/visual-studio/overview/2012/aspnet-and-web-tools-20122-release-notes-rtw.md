---
uid: visual-studio/overview/2012/aspnet-and-web-tools-20122-release-notes-rtw
title: ASP.NET和网络工具 2012.2 发行说明 |微软文档
author: rick-anderson
description: ASP.NET和网络工具 2012.2 的发行说明。
ms.author: riande
ms.date: 02/14/2013
ms.assetid: 9534e58b-1d15-4f1d-b04c-10c79b9d8227
msc.legacyurl: /visual-studio/overview/2012/aspnet-and-web-tools-20122-release-notes-rtw
msc.type: content
ms.openlocfilehash: abd6d8ce0646852a194369589cb730fc98ecb3ad
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675903"
---
# <a name="aspnet-and-web-tools-20122-release-notes"></a><span data-ttu-id="316c0-103">ASP.NET 和 Web 工具 2012.2 发行说明</span><span class="sxs-lookup"><span data-stu-id="316c0-103">ASP.NET and Web Tools 2012.2 Release Notes</span></span>

> <span data-ttu-id="316c0-104">本文档介绍 ASP.NET 和 Web 工具 2012.2 的发布。</span><span class="sxs-lookup"><span data-stu-id="316c0-104">This document describes the release of ASP.NET and Web Tools 2012.2.</span></span> <span data-ttu-id="316c0-105">它是可视化工作室 Web 工具和ASP.NET的更新。</span><span class="sxs-lookup"><span data-stu-id="316c0-105">It is an update to Visual Studio Web Tooling and ASP.NET.</span></span>

- [<span data-ttu-id="316c0-106">安装说明</span><span class="sxs-lookup"><span data-stu-id="316c0-106">Installation Notes</span></span>](#_Installation)
- [<span data-ttu-id="316c0-107">文档</span><span class="sxs-lookup"><span data-stu-id="316c0-107">Documentation</span></span>](#_Documentation)
- [<span data-ttu-id="316c0-108">支持</span><span class="sxs-lookup"><span data-stu-id="316c0-108">Support</span></span>](#_Support)
- [<span data-ttu-id="316c0-109">软件要求</span><span class="sxs-lookup"><span data-stu-id="316c0-109">Software Requirements</span></span>](#_Software_Requirements)
- [<span data-ttu-id="316c0-110">ASP.NET和 Web 工具中的新功能 2012.2</span><span class="sxs-lookup"><span data-stu-id="316c0-110">New Features in ASP.NET and Web Tools 2012.2</span></span>](#_New_Features_in)

    - [<span data-ttu-id="316c0-111">工具</span><span class="sxs-lookup"><span data-stu-id="316c0-111">Tooling</span></span>](#_Tooling)
    - [<span data-ttu-id="316c0-112">Web 发布</span><span class="sxs-lookup"><span data-stu-id="316c0-112">Web Publishing</span></span>](#_Web_Publishing)
    - [<span data-ttu-id="316c0-113">ASP.NET MVC 模板</span><span class="sxs-lookup"><span data-stu-id="316c0-113">ASP.NET MVC Templates</span></span>](#_Templates)
    - [<span data-ttu-id="316c0-114">ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="316c0-114">ASP.NET Web API</span></span>](#_ASP.NET_Web_API)

    - [<span data-ttu-id="316c0-115">ASP.NET SignalR</span><span class="sxs-lookup"><span data-stu-id="316c0-115">ASP.NET SignalR</span></span>](#_ASP.NET_SignalR)
    - [<span data-ttu-id="316c0-116">ASP.NET 友好 URL</span><span class="sxs-lookup"><span data-stu-id="316c0-116">ASP.NET Friendly URLs</span></span>](#_ASP.NET_Friendly_URLs)
- [<span data-ttu-id="316c0-117">已知问题和重大更改</span><span class="sxs-lookup"><span data-stu-id="316c0-117">Known Issues and Breaking Changes</span></span>](#_Known_Issues_and)

<a id="_Installation"></a>
## <a name="installation-notes"></a><span data-ttu-id="316c0-118">安装说明</span><span class="sxs-lookup"><span data-stu-id="316c0-118">Installation Notes</span></span>

<span data-ttu-id="316c0-119">ASP.NET和Web工具2012.2为可视化工作室2012可以使用[Web平台安装程序](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=ASPDOTNETandWebTools2012_2)安装。</span><span class="sxs-lookup"><span data-stu-id="316c0-119">ASP.NET and Web Tools 2012.2 for Visual Studio 2012 can be installed using [Web Platform installer](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=ASPDOTNETandWebTools2012_2).</span></span> <span data-ttu-id="316c0-120">这是 Visual Studio 2012 或 Visual Studio Express 2012 Web 的更新，这是必要的。</span><span class="sxs-lookup"><span data-stu-id="316c0-120">This is an update to Visual Studio 2012 or Visual Studio Express 2012 for Web, which is required.</span></span> <span data-ttu-id="316c0-121">如果您未安装 Visual Studio，则将安装适用于 Web 的 Visual Studio Express 2012。</span><span class="sxs-lookup"><span data-stu-id="316c0-121">If you do not have Visual Studio installed, Visual Studio Express 2012 for Web will be installed.</span></span>

<span data-ttu-id="316c0-122">您还可以手动安装ASP.NET和 Web 工具 2012.2。</span><span class="sxs-lookup"><span data-stu-id="316c0-122">You can also install ASP.NET and Web Tools 2012.2 manually.</span></span> <span data-ttu-id="316c0-123">您必须安装 Visual Studio 2012 或 Visual Studio Express 2012 以安装 Web。</span><span class="sxs-lookup"><span data-stu-id="316c0-123">You must have Visual Studio 2012 or Visual Studio Express 2012 for Web installed.</span></span> <span data-ttu-id="316c0-124">然后使用以下说明：</span><span class="sxs-lookup"><span data-stu-id="316c0-124">Then use the following instructions:</span></span> 

1. <span data-ttu-id="316c0-125">从下载中心下载[ASP.NET和 Web 框架 2012.2](https://download.microsoft.com/download/6/5/6/6562AFBE-9503-4E64-970C-1427133FCD73/AspNetWebTools2012Setup.exe)安装程序。</span><span class="sxs-lookup"><span data-stu-id="316c0-125">Download [ASP.NET and Web Frameworks 2012.2](https://download.microsoft.com/download/6/5/6/6562AFBE-9503-4E64-970C-1427133FCD73/AspNetWebTools2012Setup.exe) installer from Download Center.</span></span>
2. <span data-ttu-id="316c0-126">当提示时，单击"运行"。</span><span class="sxs-lookup"><span data-stu-id="316c0-126">When prompted click Run.</span></span> <span data-ttu-id="316c0-127">您还可以保存该文件以稍后运行该文件。</span><span class="sxs-lookup"><span data-stu-id="316c0-127">You can also save the file to run it later.</span></span>
3. <span data-ttu-id="316c0-128">验证您将要更新的可视化工作室版本。</span><span class="sxs-lookup"><span data-stu-id="316c0-128">Verify the version of Visual Studio you will update.</span></span> <span data-ttu-id="316c0-129">您可以通过启动要更新的可视化工作室来执行此操作。</span><span class="sxs-lookup"><span data-stu-id="316c0-129">You can do this by launching the Visual Studio you wish to update.</span></span> <span data-ttu-id="316c0-130">然后单击"帮助"菜单项。</span><span class="sxs-lookup"><span data-stu-id="316c0-130">Then click the Help menu item.</span></span>   
    ![](aspnet-and-web-tools-20122-release-notes-rtw/_static/image1.jpg)
4. <span data-ttu-id="316c0-131">如果你看到关于微软视觉工作室&quot;2012网页的菜单项&quot;，然后下载[网络开发人员工具2012.2 - Visual Studio Express 2012为Web。](https://go.microsoft.com/fwlink/?LinkID=282228)</span><span class="sxs-lookup"><span data-stu-id="316c0-131">If you see the menu item &quot;About Microsoft Visual Studio 2012 for Web&quot; then download [Web Developer Tools 2012.2 - Visual Studio Express 2012 for Web](https://go.microsoft.com/fwlink/?LinkID=282228).</span></span> <span data-ttu-id="316c0-132">否则下载[网络开发人员工具 2012.2 - 视觉工作室 2012](https://go.microsoft.com/fwlink/?LinkID=282228).</span><span class="sxs-lookup"><span data-stu-id="316c0-132">Otherwise download [Web Developer Tools 2012.2 - Visual Studio 2012](https://go.microsoft.com/fwlink/?LinkID=282228).</span></span>
5. <span data-ttu-id="316c0-133">当提示时，单击"运行"。</span><span class="sxs-lookup"><span data-stu-id="316c0-133">When prompted click Run.</span></span> <span data-ttu-id="316c0-134">您还可以保存该文件以稍后运行该文件。</span><span class="sxs-lookup"><span data-stu-id="316c0-134">You can also save the file to run it later.</span></span>

> [!NOTE]
> <span data-ttu-id="316c0-135">ASP.NET和 Web 工具 2012.2 版本不包括 SQL Server 数据工具。</span><span class="sxs-lookup"><span data-stu-id="316c0-135">ASP.NET and Web Tools 2012.2 release does not include SQL Server Data Tools.</span></span> <span data-ttu-id="316c0-136">SQL Server 和 Windows Azure SQL 数据库提供了一组更丰富的数据库工具，包括脱机项目支持的开发、架构比较和增强的数据库部署功能。</span><span class="sxs-lookup"><span data-stu-id="316c0-136">SQL Server and Windows Azure SQL Databases provides a richer set of database tooling including offline project-backed development, schema comparison and enhanced database deployment capabilities.</span></span> <span data-ttu-id="316c0-137">有关详细信息或安装 SQL 服务器数据工具，请访问[https://go.microsoft.com/fwlink/?LinkID=237127](https://go.microsoft.com/fwlink/?LinkID=237127)。</span><span class="sxs-lookup"><span data-stu-id="316c0-137">For more information or to install SQL Server Data Tools visit [https://go.microsoft.com/fwlink/?LinkID=237127](https://go.microsoft.com/fwlink/?LinkID=237127).</span></span>

<a id="_Documentation"></a>
## <a name="documentation"></a><span data-ttu-id="316c0-138">文档</span><span class="sxs-lookup"><span data-stu-id="316c0-138">Documentation</span></span>

<span data-ttu-id="316c0-139">有关ASP.NET和 Web 工具 2012.2 的教程和其他信息可从ASP.NET网站https://www.asp.net)（） 获得。</span><span class="sxs-lookup"><span data-stu-id="316c0-139">Tutorials and other information about ASP.NET and Web Tools 2012.2 are available from ASP.NET web site ( https://www.asp.net).</span></span>

<a id="_Support"></a>
## <a name="support"></a><span data-ttu-id="316c0-140">支持</span><span class="sxs-lookup"><span data-stu-id="316c0-140">Support</span></span>

<span data-ttu-id="316c0-141">ASP.NET和网络工具 2012.2 正式发布和支持。</span><span class="sxs-lookup"><span data-stu-id="316c0-141">ASP.NET and Web Tools 2012.2 is officially released and supported.</span></span> <span data-ttu-id="316c0-142">您可以使用正常的支持通道。</span><span class="sxs-lookup"><span data-stu-id="316c0-142">You can use your normal support channel.</span></span> <span data-ttu-id="316c0-143">您还可以向ASP.NET论坛 （）[https://forums.asp.net/](https://forums.asp.net/)发布问题，ASP.NET社区成员经常能够提供非正式支持。</span><span class="sxs-lookup"><span data-stu-id="316c0-143">You can also post questions to the ASP.NET forums ([https://forums.asp.net/](https://forums.asp.net/)), where members of the ASP.NET community are frequently able to provide informal support.</span></span>

<a id="_Software_Requirements"></a>
## <a name="software-requirements"></a><span data-ttu-id="316c0-144">软件要求</span><span class="sxs-lookup"><span data-stu-id="316c0-144">Software Requirements</span></span>

<span data-ttu-id="316c0-145">ASP.NET和网络工具 2012.2 要求 Visual Studio 2012 或 Visual Studio Express 2012 用于 Web。</span><span class="sxs-lookup"><span data-stu-id="316c0-145">The ASP.NET and Web Tools 2012.2 requires Visual Studio 2012 or Visual Studio Express 2012 for Web.</span></span>

<a id="_New_Features_in"></a>
## <a name="new-features-in-aspnet-and-web-tools-20122"></a><span data-ttu-id="316c0-146">ASP.NET和 Web 工具中的新功能 2012.2</span><span class="sxs-lookup"><span data-stu-id="316c0-146">New Features in ASP.NET and Web Tools 2012.2</span></span>

<span data-ttu-id="316c0-147">本节介绍在ASP.NET和 Web 工具 2012.2 版本中引入的功能。</span><span class="sxs-lookup"><span data-stu-id="316c0-147">This section describes features that have been introduced in the ASP.NET and Web Tools 2012.2 release.</span></span>

<a id="_Tooling"></a>
### <a name="tooling"></a><span data-ttu-id="316c0-148">工具</span><span class="sxs-lookup"><span data-stu-id="316c0-148">Tooling</span></span>

- <span data-ttu-id="316c0-149">Page Inspector</span><span class="sxs-lookup"><span data-stu-id="316c0-149">Page Inspector</span></span> 

    - <span data-ttu-id="316c0-150">支持 JavaScript 选择映射，允许页面检查器将动态添加到页面的项目映射回相应的 JavaScript 代码。</span><span class="sxs-lookup"><span data-stu-id="316c0-150">Support JavaScript selection mapping allowing Page Inspector to map items that were dynamically added to the page back to the corresponding JavaScript code.</span></span>
    - <span data-ttu-id="316c0-151">实时查看 CSS 更新的能力。</span><span class="sxs-lookup"><span data-stu-id="316c0-151">The ability to see CSS updates in real-time.</span></span>
    - <span data-ttu-id="316c0-152">有关详细信息，请阅读[页面检查器 中的 CSS 自动同步和 JavaScript 选择映射](https://blogs.msdn.com/b/webdev/archive/2012/12/14/css-auto-sync-and-javascript-selection-mapping-in-page-inspector.aspx)。</span><span class="sxs-lookup"><span data-stu-id="316c0-152">For more information, read [CSS Auto-Sync and JavaScript Selection Mapping in Page Inspector](https://blogs.msdn.com/b/webdev/archive/2012/12/14/css-auto-sync-and-javascript-selection-mapping-in-page-inspector.aspx).</span></span>
- <span data-ttu-id="316c0-153">编辑器</span><span class="sxs-lookup"><span data-stu-id="316c0-153">Editor</span></span> 

    - <span data-ttu-id="316c0-154">支持咖啡脚本、胡须、手柄和 JsRender 的语法突出显示。</span><span class="sxs-lookup"><span data-stu-id="316c0-154">Support syntax highlighting for CoffeeScript, Mustache, Handlebars, and JsRender.</span></span>
    - <span data-ttu-id="316c0-155">HTML 编辑器为挖空绑定提供"感知"。</span><span class="sxs-lookup"><span data-stu-id="316c0-155">The HTML editor provides Intellisense for Knockout bindings.</span></span>
    - <span data-ttu-id="316c0-156">减少编辑和编译器支持，以便使用 LESS 构建动态 CSS。</span><span class="sxs-lookup"><span data-stu-id="316c0-156">LESS editing and compiler support to enable building dynamic CSS using LESS.</span></span>
    - <span data-ttu-id="316c0-157">将 JSON 粘贴为 .NET 类。</span><span class="sxs-lookup"><span data-stu-id="316c0-157">Paste JSON as a .NET class.</span></span> <span data-ttu-id="316c0-158">使用此特殊粘贴命令将 JSON 粘贴到 C# 或VB.NET代码文件中，Visual Studio 将自动生成从 JSON 推断的 .NET 类。</span><span class="sxs-lookup"><span data-stu-id="316c0-158">Using this Special Paste command to paste JSON into a C# or VB.NET code file, and Visual Studio will automatically generate .NET classes inferred from the JSON.</span></span>
- <span data-ttu-id="316c0-159">移动仿真器支持增加了扩展性挂钩，以便第三方仿真器可以作为 VSIX 安装。</span><span class="sxs-lookup"><span data-stu-id="316c0-159">Mobile Emulator support adds extensibility hooks so that third-party emulators can be installed as a VSIX.</span></span> <span data-ttu-id="316c0-160">已安装的仿真器将显示在 F5 下拉列表中，以便开发人员可以在各种移动设备上预览其网站。</span><span class="sxs-lookup"><span data-stu-id="316c0-160">The installed emulators will show up in the F5 dropdown, so that developers can preview their websites on a variety of mobile devices.</span></span> <span data-ttu-id="316c0-161">阅读更多有关此功能在斯科特汉塞尔曼的博客条目与[视觉工作室新的浏览器堆栈集成](http://www.hanselman.com/blog/CrossBrowserDebuggingIntegratedIntoVisualStudioWithBrowserStack.aspx)。</span><span class="sxs-lookup"><span data-stu-id="316c0-161">Read more about this feature in Scott Hanselman's blog entry on [the new BrowserStack integration with Visual Studio](http://www.hanselman.com/blog/CrossBrowserDebuggingIntegratedIntoVisualStudioWithBrowserStack.aspx).</span></span>

<a id="_Web_Publishing"></a>
### <a name="web-publishing"></a><span data-ttu-id="316c0-162">Web 发布</span><span class="sxs-lookup"><span data-stu-id="316c0-162">Web Publishing</span></span>

- <span data-ttu-id="316c0-163">网站项目现在具有与 Web 应用程序项目相同的发布体验，包括发布到 Windows Azure 网站。</span><span class="sxs-lookup"><span data-stu-id="316c0-163">Web site projects now have the same publishing experience as Web Application projects including publishing to Windows Azure Web Sites.</span></span>
- <span data-ttu-id="316c0-164">选择性发布&#8211;一个或多个文件，您可以执行以下操作（发布到 Web 部署终结点后）：</span><span class="sxs-lookup"><span data-stu-id="316c0-164">Selective publish &#8211; for one or more files you can perform the following actions (after publishing to a Web Deploy endpoint):</span></span> 

    - <span data-ttu-id="316c0-165">发布选定的文件。</span><span class="sxs-lookup"><span data-stu-id="316c0-165">Publish selected files.</span></span>
    - <span data-ttu-id="316c0-166">查看本地文件和远程文件之间的区别。</span><span class="sxs-lookup"><span data-stu-id="316c0-166">See the difference between a local file and a remote file.</span></span>
    - <span data-ttu-id="316c0-167">使用远程文件更新本地文件或使用本地文件更新远程文件。</span><span class="sxs-lookup"><span data-stu-id="316c0-167">Update the local file with the remote file or update the remote file with the local file.</span></span>

<a id="_Templates"></a>
### <a name="aspnet-mvc-templates"></a><span data-ttu-id="316c0-168">ASP.NET MVC 模板</span><span class="sxs-lookup"><span data-stu-id="316c0-168">ASP.NET MVC Templates</span></span>

- <span data-ttu-id="316c0-169">新的 Facebook 应用程序模板可帮助你轻松编写 Facebook Canvas 应用程序。</span><span class="sxs-lookup"><span data-stu-id="316c0-169">The new Facebook Application template makes writing Facebook Canvas applications easy.</span></span> <span data-ttu-id="316c0-170">只需执行几个简单步骤，即可创建一个 Facebook 应用程序，从已登录用户获取数据并与其好友集成。</span><span class="sxs-lookup"><span data-stu-id="316c0-170">In a few simple steps, you can create a Facebook application that gets data from a logged in user and integrates with their friends.</span></span> <span data-ttu-id="316c0-171">该模板包含一个新库，可维护构建 Facebook 应用程序时涉及的所有管道（包括身份验证、权限、访问 Facebook 数据等），</span><span class="sxs-lookup"><span data-stu-id="316c0-171">The template includes a new library to take care of all the plumbing involved in building a Facebook app, including authentication, permissions, accessing Facebook data and more.</span></span> <span data-ttu-id="316c0-172">有关使用 Facebook 应用程序模板的详细信息，请参阅[https://go.microsoft.com/fwlink/?LinkID=269921](https://go.microsoft.com/fwlink/?LinkID=269921)。</span><span class="sxs-lookup"><span data-stu-id="316c0-172">For more information on using the Facebook Application template see [https://go.microsoft.com/fwlink/?LinkID=269921](https://go.microsoft.com/fwlink/?LinkID=269921).</span></span>
- <span data-ttu-id="316c0-173">使用新的单页应用程序 MVC 模板，开发人员可以在 ASP.NET Web API 之上使用 HTML 5、CSS 3 以及常用的 Knockout 和 jQuery JavaScript 库构建交互式客户端 Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="316c0-173">A new Single Page Application MVC template allows developers to build interactive client-side web apps using HTML 5, CSS 3, and the popular Knockout and jQuery JavaScript libraries, on top of ASP.NET Web API.</span></span> <span data-ttu-id="316c0-174">该模板包括一个"待办事项"列表应用程序，该应用程序演示了构建使用 RESTful 服务器 API 的 JavaScript HTML5 应用程序的常见做法。</span><span class="sxs-lookup"><span data-stu-id="316c0-174">The template includes a "todo" list application that demonstrates common practices for building a JavaScript HTML5 application that uses a RESTful server API.</span></span> <span data-ttu-id="316c0-175">您可以在 上阅读更多内容[https://www.asp.net/single-page-application](../../../single-page-application/index.md)。</span><span class="sxs-lookup"><span data-stu-id="316c0-175">You can read more at [https://www.asp.net/single-page-application](../../../single-page-application/index.md).</span></span>
- <span data-ttu-id="316c0-176">您现在可以创建一个 VSIX，将新模板添加到ASP.NET MVC 新项目对话框。</span><span class="sxs-lookup"><span data-stu-id="316c0-176">You can now create a VSIX that adds new templates to the ASP.NET MVC New Project dialog.</span></span> <span data-ttu-id="316c0-177">了解如何在此处：[https://go.microsoft.com/fwlink/?LinkId=275019](https://go.microsoft.com/fwlink/?LinkId=275019)</span><span class="sxs-lookup"><span data-stu-id="316c0-177">Learn how here: [https://go.microsoft.com/fwlink/?LinkId=275019](https://go.microsoft.com/fwlink/?LinkId=275019)</span></span>
- <span data-ttu-id="316c0-178">已更新 &#8211; MVC 项目模板的固定显示模式包，以包括新的"固定显示模式"NuGet 包，该包包含 MVC 4 中 Bug 的解决方法。</span><span class="sxs-lookup"><span data-stu-id="316c0-178">FixedDisplayModes package &#8211; MVC project templates have been updated to include the new ‘FixedDisplayModes' NuGet package, which contains a workaround for a bug in MVC 4.</span></span> <span data-ttu-id="316c0-179">有关包中包含的修复程序的详细信息，请参阅 MVC 团队的此博客文章 （[https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx](https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx)）。</span><span class="sxs-lookup"><span data-stu-id="316c0-179">For more information on the fix contained in the package, refer to this blog post ([https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx](https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx)) from the MVC team.</span></span>

<a id="_ASP.NET_Web_API"></a>
### <a name="aspnet-web-api"></a><span data-ttu-id="316c0-180">ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="316c0-180">ASP.NET Web API</span></span>

<span data-ttu-id="316c0-181">ASP.NET Web API 已通过以下几个新功能进行了增强：</span><span class="sxs-lookup"><span data-stu-id="316c0-181">ASP.NET Web API has been enhanced with several new features:</span></span>

- <span data-ttu-id="316c0-182">ASP.NET Web API OData</span><span class="sxs-lookup"><span data-stu-id="316c0-182">ASP.NET Web API OData</span></span>
- <span data-ttu-id="316c0-183">ASP.NET Web API 跟踪</span><span class="sxs-lookup"><span data-stu-id="316c0-183">ASP.NET Web API Tracing</span></span>
- <span data-ttu-id="316c0-184">ASP.NET Web API 帮助页</span><span class="sxs-lookup"><span data-stu-id="316c0-184">ASP.NET Web API Help Page</span></span>

#### <a name="aspnet-web-api-odata"></a><span data-ttu-id="316c0-185">ASP.NET Web API OData</span><span class="sxs-lookup"><span data-stu-id="316c0-185">ASP.NET Web API OData</span></span>

<span data-ttu-id="316c0-186">ASP.NET Web API OData 使您能够灵活地构建具有丰富业务逻辑的 OData 终结点，而不是任何数据源。</span><span class="sxs-lookup"><span data-stu-id="316c0-186">ASP.NET Web API OData gives you the flexibility you need to build OData endpoints with rich business logic over any data source.</span></span> <span data-ttu-id="316c0-187">使用ASP.NET Web API OData，您可以控制要公开的 OData 语义量。</span><span class="sxs-lookup"><span data-stu-id="316c0-187">With ASP.NET Web API OData you control the amount of OData semantics that you want to expose.</span></span> <span data-ttu-id="316c0-188">ASP.NET Web API OData 包含在mVC 4ASP.NET项目模板中，也可从 NuGet[http://www.nuget.org/packages/microsoft.aspnet.webapi.odata](http://www.nuget.org/packages/microsoft.aspnet.webapi.odata)（） 获得。</span><span class="sxs-lookup"><span data-stu-id="316c0-188">ASP.NET Web API OData is included with the ASP.NET MVC 4 project templates and is also available from NuGet ([http://www.nuget.org/packages/microsoft.aspnet.webapi.odata](http://www.nuget.org/packages/microsoft.aspnet.webapi.odata)).</span></span>

<span data-ttu-id="316c0-189">ASP.NET Web API OData 目前支持以下功能：</span><span class="sxs-lookup"><span data-stu-id="316c0-189">ASP.NET Web API OData currently supports the following features:</span></span>

- <span data-ttu-id="316c0-190">通过应用 [可查询] 属性启用 OData 查询语义。</span><span class="sxs-lookup"><span data-stu-id="316c0-190">Enable OData query semantics by applying the [Queryable] attribute.</span></span>
- <span data-ttu-id="316c0-191">轻松验证 OData 查询并限制支持的查询选项、运算符和函数集。</span><span class="sxs-lookup"><span data-stu-id="316c0-191">Easily validate OData queries and restrict the set of supported query options, operators and functions.</span></span>
- <span data-ttu-id="316c0-192">参数直接绑定到 ODataQueryOptions，以获得查询的抽象语法树表示形式，然后可以验证并应用于可查询或 IE500。</span><span class="sxs-lookup"><span data-stu-id="316c0-192">Parameter bind to ODataQueryOptions directly to get an abstract syntax tree representation of the query that can then be validated and applied to an IQueryable or IEnumerable.</span></span>
- <span data-ttu-id="316c0-193">通过在 [可查询] 属性上指定结果限制，启用服务驱动的分页和下一页链接生成。</span><span class="sxs-lookup"><span data-stu-id="316c0-193">Enable service-driven paging and next page link generation by specifying result limits on [Queryable] attribute.</span></span>
- <span data-ttu-id="316c0-194">使用$inlinecount请求匹配资源总数的内联计数。</span><span class="sxs-lookup"><span data-stu-id="316c0-194">Request an inlined count of the total number of matching resources using $inlinecount.</span></span>
- <span data-ttu-id="316c0-195">控制无效传播。</span><span class="sxs-lookup"><span data-stu-id="316c0-195">Control null propagation.</span></span>
- <span data-ttu-id="316c0-196">$filter中的任何/所有运算符。</span><span class="sxs-lookup"><span data-stu-id="316c0-196">Any/All operators in $filter.</span></span>
- <span data-ttu-id="316c0-197">按约定推断实体数据模型，或以类似于实体框架代码优先的方式显式自定义模型。</span><span class="sxs-lookup"><span data-stu-id="316c0-197">Infer an entity data model by convention or explicitly customize a model in a manner similar to Entity Framework Code-First.</span></span>
- <span data-ttu-id="316c0-198">通过从实体集控制器派生来公开实体集。</span><span class="sxs-lookup"><span data-stu-id="316c0-198">Expose entity sets by deriving from EntitySetController.</span></span>
- <span data-ttu-id="316c0-199">用于公开导航属性、操作链接和实现 OData 操作的简单可自定义约定。</span><span class="sxs-lookup"><span data-stu-id="316c0-199">Simple, customizable conventions for exposing navigation properties, manipulating links and implementing OData actions.</span></span>
- <span data-ttu-id="316c0-200">使用 MapODataRoute 扩展方法简化路由。</span><span class="sxs-lookup"><span data-stu-id="316c0-200">Simplified routing using the MapODataRoute extension method.</span></span>
- <span data-ttu-id="316c0-201">通过公开多个 EDM 模型来支持版本控制。</span><span class="sxs-lookup"><span data-stu-id="316c0-201">Support for versioning by exposing multiple EDM models.</span></span>
- <span data-ttu-id="316c0-202">公开服务文档和$metadata，以便为 Web API 生成客户端（.NET、Windows Phone、Windows 应用商店等）。</span><span class="sxs-lookup"><span data-stu-id="316c0-202">Expose service document and $metadata so you can generate clients (.NET, Windows Phone, Windows Store, etc.) for your Web API.</span></span>
- <span data-ttu-id="316c0-203">支持 OData Atom、JSON 和 JSON 详细格式。</span><span class="sxs-lookup"><span data-stu-id="316c0-203">Support for the OData Atom, JSON, and JSON verbose formats.</span></span>
- <span data-ttu-id="316c0-204">创建、更新、部分更新（PATCH）和删除实体。</span><span class="sxs-lookup"><span data-stu-id="316c0-204">Create, update, partially update (PATCH) and delete entities.</span></span>
- <span data-ttu-id="316c0-205">查询和操作实体之间的关系。</span><span class="sxs-lookup"><span data-stu-id="316c0-205">Query and manipulate relationships between entities.</span></span>
- <span data-ttu-id="316c0-206">创建连接到您的路线的关系链接。</span><span class="sxs-lookup"><span data-stu-id="316c0-206">Create relationship links that wire up to your routes.</span></span>
- <span data-ttu-id="316c0-207">复杂类型。</span><span class="sxs-lookup"><span data-stu-id="316c0-207">Complex types.</span></span>
- <span data-ttu-id="316c0-208">实体类型继承。</span><span class="sxs-lookup"><span data-stu-id="316c0-208">Entity Type Inheritance.</span></span>
- <span data-ttu-id="316c0-209">集合属性。</span><span class="sxs-lookup"><span data-stu-id="316c0-209">Collection properties.</span></span>
- <span data-ttu-id="316c0-210">枚举。</span><span class="sxs-lookup"><span data-stu-id="316c0-210">Enums.</span></span>
- <span data-ttu-id="316c0-211">OData 操作。</span><span class="sxs-lookup"><span data-stu-id="316c0-211">OData actions.</span></span>
- <span data-ttu-id="316c0-212">建立与 WCF 数据服务相同的基础，即 ODataLib[http://www.nuget.org/packages/microsoft.data.odata](http://www.nuget.org/packages/microsoft.data.odata)（）。</span><span class="sxs-lookup"><span data-stu-id="316c0-212">Built upon the same foundation as WCF Data Services, namely ODataLib ([http://www.nuget.org/packages/microsoft.data.odata](http://www.nuget.org/packages/microsoft.data.odata)).</span></span>

<span data-ttu-id="316c0-213">有关web API OData ASP.NET的详细信息[https://go.microsoft.com/fwlink/?LinkId=271141](https://go.microsoft.com/fwlink/?LinkId=271141)，请参阅。</span><span class="sxs-lookup"><span data-stu-id="316c0-213">For more information on ASP.NET Web API OData see [https://go.microsoft.com/fwlink/?LinkId=271141](https://go.microsoft.com/fwlink/?LinkId=271141).</span></span>

#### <a name="aspnet-web-api-tracing"></a><span data-ttu-id="316c0-214">ASP.NET Web API 跟踪</span><span class="sxs-lookup"><span data-stu-id="316c0-214">ASP.NET Web API Tracing</span></span>

<span data-ttu-id="316c0-215">ASP.NET Web API 跟踪将从 Web API 的跟踪数据集成到 .NET 跟踪中。</span><span class="sxs-lookup"><span data-stu-id="316c0-215">ASP.NET Web API Tracing integrates tracing data from your web APIs with .NET Tracing.</span></span> <span data-ttu-id="316c0-216">默认情况下，它在 Web API 项目模板中启用。</span><span class="sxs-lookup"><span data-stu-id="316c0-216">It is now enabled by default in the Web API project template.</span></span> <span data-ttu-id="316c0-217">Web API 的跟踪数据将发送到输出窗口，并通过 IntelliTrace 提供。</span><span class="sxs-lookup"><span data-stu-id="316c0-217">Tracing data for your web APIs is sent to the Output window and is made available through IntelliTrace.</span></span> <span data-ttu-id="316c0-218">ASP.NET Web API 跟踪使您能够通过与[Windows Azure 诊断](https://msdn.microsoft.com/library/windowsazure/hh411529.aspx)集成在 Windows Azure 上托管时跟踪有关 Web API 的信息。</span><span class="sxs-lookup"><span data-stu-id="316c0-218">ASP.NET Web API Tracing enables you to trace information about your Web API when hosted on Windows Azure through integration with [Windows Azure Diagnostics](https://msdn.microsoft.com/library/windowsazure/hh411529.aspx).</span></span> <span data-ttu-id="316c0-219">您还可以使用ASP.NET Web API 跟踪 NuGet 包 （）[http://www.nuget.org/packages/microsoft.aspnet.webapi.tracing](http://www.nuget.org/packages/microsoft.aspnet.webapi.tracing)在任何应用程序中安装和启用ASP.NET Web API 跟踪。</span><span class="sxs-lookup"><span data-stu-id="316c0-219">You can also install and enable ASP.NET Web API Tracing in any application using the ASP.NET Web API Tracing NuGet package ([http://www.nuget.org/packages/microsoft.aspnet.webapi.tracing](http://www.nuget.org/packages/microsoft.aspnet.webapi.tracing)).</span></span>

<span data-ttu-id="316c0-220">有关配置和使用ASP.NET Web API 跟踪的详细信息，请参阅[https://go.microsoft.com/fwlink/?LinkID=269874](https://go.microsoft.com/fwlink/?LinkID=269874)。</span><span class="sxs-lookup"><span data-stu-id="316c0-220">For more information on configuring and using ASP.NET Web API Tracing see [https://go.microsoft.com/fwlink/?LinkID=269874](https://go.microsoft.com/fwlink/?LinkID=269874).</span></span>

#### <a name="aspnet-web-api-help-page"></a><span data-ttu-id="316c0-221">ASP.NET Web API 帮助页</span><span class="sxs-lookup"><span data-stu-id="316c0-221">ASP.NET Web API Help Page</span></span>

<span data-ttu-id="316c0-222">默认情况下，Web API 帮助页ASP.NET包含在 Web API 项目模板中。</span><span class="sxs-lookup"><span data-stu-id="316c0-222">The ASP.NET Web API Help Page is now included by default in the Web API project template.</span></span> <span data-ttu-id="316c0-223">ASP.NET Web API 帮助页会自动为 Web API 生成文档，包括 HTTP 终结点、支持的 HTTP 方法、参数以及示例请求和响应消息负载。</span><span class="sxs-lookup"><span data-stu-id="316c0-223">The ASP.NET Web API Help Page automatically generates documentation for web APIs including the HTTP endpoints, the supported HTTP methods, parameters and example request and response message payloads.</span></span> <span data-ttu-id="316c0-224">文档会自动从代码中的注释中提取。</span><span class="sxs-lookup"><span data-stu-id="316c0-224">Documentation is automatically pulled from comments in your code.</span></span> <span data-ttu-id="316c0-225">您还可以使用ASP.NET Web API 帮助页 NuGet 包 （）[http://www.nuget.org/packages/microsoft.aspnet.webapi.helppage](http://www.nuget.org/packages/microsoft.aspnet.webapi.helppage)将ASP.NET Web API 帮助页添加到任何应用程序。</span><span class="sxs-lookup"><span data-stu-id="316c0-225">You can also add the ASP.NET Web API Help Page to any application using the ASP.NET Web API Help Page NuGet package ([http://www.nuget.org/packages/microsoft.aspnet.webapi.helppage](http://www.nuget.org/packages/microsoft.aspnet.webapi.helppage)).</span></span>

<span data-ttu-id="316c0-226">有关设置和自定义ASP.NET Web API 帮助页的详细信息，请参阅[https://go.microsoft.com/fwlink/?LinkId=271140](https://go.microsoft.com/fwlink/?LinkId=271140)。</span><span class="sxs-lookup"><span data-stu-id="316c0-226">For more information on setting up and customizing the ASP.NET Web API Help Page see [https://go.microsoft.com/fwlink/?LinkId=271140](https://go.microsoft.com/fwlink/?LinkId=271140).</span></span>

<a id="_ASP.NET_SignalR"></a>
### <a name="aspnet-signalr"></a><span data-ttu-id="316c0-227">ASP.NET SignalR</span><span class="sxs-lookup"><span data-stu-id="316c0-227">ASP.NET SignalR</span></span>

<span data-ttu-id="316c0-228">ASP.NET SignalR 使将实时 Web 功能添加到ASP.NET应用程序中变得简单，如果使用 WebSocket（如果可用），则在不可用时自动回归到其他技术。</span><span class="sxs-lookup"><span data-stu-id="316c0-228">ASP.NET SignalR makes it simple to add real-time web capabilities to your ASP.NET application, using WebSockets if available and automatically falling back to other techniques when it isn't.</span></span>

<span data-ttu-id="316c0-229">有关使用ASP.NET信号R的详细信息，请参阅[https://go.microsoft.com/fwlink/?LinkId=271271](https://go.microsoft.com/fwlink/?LinkId=271271)。</span><span class="sxs-lookup"><span data-stu-id="316c0-229">For more information on using ASP.NET SignalR see [https://go.microsoft.com/fwlink/?LinkId=271271](https://go.microsoft.com/fwlink/?LinkId=271271).</span></span>

<a id="_ASP.NET_Friendly_URLs"></a>
### <a name="aspnet-friendly-urls"></a><span data-ttu-id="316c0-230">ASP.NET 友好 URL</span><span class="sxs-lookup"><span data-stu-id="316c0-230">ASP.NET Friendly URLs</span></span>

<span data-ttu-id="316c0-231">ASP.NET友好 URL 使 Web 表单开发人员能够非常轻松地生成外观更简洁的 URL（没有 .aspx 扩展）。</span><span class="sxs-lookup"><span data-stu-id="316c0-231">ASP.NET FriendlyURLs makes it very easy for web forms developers to generate cleaner looking URLs(without the .aspx extension).</span></span> <span data-ttu-id="316c0-232">它只需要很少或不需要配置，并且可用于现有的ASP.NET v4.0 应用程序。</span><span class="sxs-lookup"><span data-stu-id="316c0-232">It requires little to no configuration and can be used with existing ASP.NET v4.0 applications.</span></span> <span data-ttu-id="316c0-233">友好 URL 功能还支持桌面视图和移动视图之间的切换，使开发人员能够更轻松地向其应用程序添加移动支持。</span><span class="sxs-lookup"><span data-stu-id="316c0-233">The FriendlyURLs feature also makes it easier for developers to add mobile support to their applications, by supporting switching between desktop and mobile views.</span></span>

<span data-ttu-id="316c0-234">有关安装和使用ASP.NET友好 URL 的详细信息，请参阅[http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx](http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx)。</span><span class="sxs-lookup"><span data-stu-id="316c0-234">For more information on installing and using ASP.NET Friendly URLs see [http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx](http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx).</span></span>

<a id="_Known_Issues_and"></a>
## <a name="known-issues-and-breaking-changes"></a><span data-ttu-id="316c0-235">已知问题和重大更改</span><span class="sxs-lookup"><span data-stu-id="316c0-235">Known Issues and Breaking Changes</span></span>

<span data-ttu-id="316c0-236">本节介绍 ASP.NET 和 Web 工具 2012.2 版本中的已知问题和重大更改。</span><span class="sxs-lookup"><span data-stu-id="316c0-236">This section describes known issues and breaking changes that are in the ASP.NET and Web Tools 2012.2 release.</span></span>

### <a name="installation-issues"></a><span data-ttu-id="316c0-237">安装问题</span><span class="sxs-lookup"><span data-stu-id="316c0-237">Installation Issues</span></span>

#### <a name="out-of-order-installs-of-visual-studio-2012"></a><span data-ttu-id="316c0-238">视觉工作室 2012 的有序安装</span><span class="sxs-lookup"><span data-stu-id="316c0-238">Out of order installs of Visual Studio 2012</span></span>

<span data-ttu-id="316c0-239">安装ASP.NET和 Web 工具 2012.2 后安装 Visual Studio 2012 的额外 SKU 将需要修复操作。</span><span class="sxs-lookup"><span data-stu-id="316c0-239">Installing an additional SKU of Visual Studio 2012 after installing the ASP.NET and Web Tools 2012.2 will require a repair operation.</span></span> <span data-ttu-id="316c0-240">考虑以下序列：</span><span class="sxs-lookup"><span data-stu-id="316c0-240">Consider the following sequence:</span></span>

1. <span data-ttu-id="316c0-241">安装可视化工作室 2012 快速网页</span><span class="sxs-lookup"><span data-stu-id="316c0-241">Install Visual Studio 2012 Express for Web</span></span>
2. <span data-ttu-id="316c0-242">安装ASP.NET和 Web 工具 2012.2</span><span class="sxs-lookup"><span data-stu-id="316c0-242">Install ASP.NET and Web Tools 2012.2</span></span>
3. <span data-ttu-id="316c0-243">安装视觉工作室 2012 专业， 高级或终极</span><span class="sxs-lookup"><span data-stu-id="316c0-243">Install Visual Studio 2012 Professional, Premium or Ultimate</span></span>

<span data-ttu-id="316c0-244">步骤 2 仅会导致为 Web 安装 Express 的更新。</span><span class="sxs-lookup"><span data-stu-id="316c0-244">Step 2 would only result in installing updates for Express for Web.</span></span> <span data-ttu-id="316c0-245">为了确保在步骤 3 中安装的其他 SKU 包含更新，您需要修复 ASP.NET 和 Web 工具 2012.2 才能安装上次安装的 SKU 的更新。</span><span class="sxs-lookup"><span data-stu-id="316c0-245">To ensure that the additional SKU installed during step 3 contains the update you will need to repair the ASP.NET and Web Tools 2012.2 to install the updates for the last SKU installed.</span></span> <span data-ttu-id="316c0-246">如果步骤 1 和步骤 3 中的 SKU 颠倒，则这也适用于。</span><span class="sxs-lookup"><span data-stu-id="316c0-246">This also applies if the SKUs in Step 1 and 3 are reversed.</span></span>

#### <a name="installing-microsoft-aspnet-and-web-tools-20122-when-visual-studio-is-open"></a><span data-ttu-id="316c0-247">安装微软ASP.NET和网络工具 2012.2 当可视化工作室打开</span><span class="sxs-lookup"><span data-stu-id="316c0-247">Installing Microsoft ASP.NET and Web Tools 2012.2 when Visual Studio is open</span></span>

<span data-ttu-id="316c0-248">如果在安装 Microsoft ASP.NET 和 Web 工具 2012.2 期间打开 VS，则 Visual Studio 可能最终处于不良状态。</span><span class="sxs-lookup"><span data-stu-id="316c0-248">If VS is open during installation of Microsoft ASP.NET and Web Tools 2012.2, Visual Studio might end up in a bad state.</span></span> <span data-ttu-id="316c0-249">建议用户在继续安装之前关闭 Visual Studio 的所有实例。</span><span class="sxs-lookup"><span data-stu-id="316c0-249">It is recommended that users close all instances of Visual Studio before proceeding with install.</span></span>

#### <a name="canceling-aspnet-and-web-tools-20122-setup-in-the-middle-of-installation"></a><span data-ttu-id="316c0-250">在安装中取消ASP.NET和 Web 工具 2012.2 设置</span><span class="sxs-lookup"><span data-stu-id="316c0-250">Canceling ASP.NET and Web Tools 2012.2 setup in the middle of installation</span></span>

<span data-ttu-id="316c0-251">取消ASP.NET和 Web 工具 2012.2 安装将会使 Visual Studio 处于不良状态。</span><span class="sxs-lookup"><span data-stu-id="316c0-251">Canceling ASP.NET and Web Tools 2012.2 setup in the middle of installation will leave Visual Studio in a bad state.</span></span> <span data-ttu-id="316c0-252">要解决此问题，请执行以下步骤：</span><span class="sxs-lookup"><span data-stu-id="316c0-252">To address this problem follow these steps:</span></span> 

- <span data-ttu-id="316c0-253">转到“添加/删除程序”</span><span class="sxs-lookup"><span data-stu-id="316c0-253">Go to Add Remove Programs</span></span>
- <span data-ttu-id="316c0-254">卸载 Microsoft ASP.NET 和 Web 工具 2012.2（如果存在）。</span><span class="sxs-lookup"><span data-stu-id="316c0-254">Uninstall Microsoft ASP.NET and Web Tools 2012.2, if present.</span></span>
- <span data-ttu-id="316c0-255">重新安装微软ASP.NET和网络工具 2012.2</span><span class="sxs-lookup"><span data-stu-id="316c0-255">Reinstall Microsoft ASP.NET and Web Tools 2012.2</span></span>

#### <a name="after-uninstalling-aspnet-and-web-tools-20122-the-aspnet-mvc-4-templates-and-razor-v2-web-site-templates-are-missing"></a><span data-ttu-id="316c0-256">卸载ASP.NET和 Web 工具 2012.2 后，缺少ASP.NET MVC 4 模板和 Razor v2 网站模板</span><span class="sxs-lookup"><span data-stu-id="316c0-256">After uninstalling ASP.NET and Web Tools 2012.2 the ASP.NET MVC 4 templates and Razor v2 Web Site templates are missing</span></span>

<span data-ttu-id="316c0-257">卸载ASP.NET和 Web 工具 2012.2 还将从 Visual Studio 2012 卸载所有ASP.NET MVC 4 和 Razor v2 网站模板。</span><span class="sxs-lookup"><span data-stu-id="316c0-257">Uninstalling ASP.NET and Web Tools 2012.2 will also uninstall all of ASP.NET MVC 4 and Razor v2 Web Site templates from Visual Studio 2012.</span></span>

<span data-ttu-id="316c0-258">解决方法是修复 Visual Studio 2012 安装，以重新安装ASP.NET MVC 4 和 Razor v2 网站模板。</span><span class="sxs-lookup"><span data-stu-id="316c0-258">The workaround is to repair your Visual Studio 2012 installation to reinstall ASP.NET MVC 4 and Razor v2 Web Site templates.</span></span>

### <a name="tooling-issues"></a><span data-ttu-id="316c0-259">工具问题</span><span class="sxs-lookup"><span data-stu-id="316c0-259">Tooling Issues</span></span>

#### <a name="nuget-error-reported-during-project-creation"></a><span data-ttu-id="316c0-260">项目创建期间报告的 NuGet 错误</span><span class="sxs-lookup"><span data-stu-id="316c0-260">NuGet error reported during project creation</span></span>

<span data-ttu-id="316c0-261">安装ASP.NET和 Web 工具 2012.2 后，在创建 MVC 4 项目时可能会看到以下错误</span><span class="sxs-lookup"><span data-stu-id="316c0-261">After installing ASP.NET and Web Tools 2012.2 you may see the following error when creating an MVC 4 project</span></span>

![](aspnet-and-web-tools-20122-release-notes-rtw/_static/image1.png)

<span data-ttu-id="316c0-262">ASP.NET和网络工具 2012.2 船舶 NuGet 2.1，并将升级 Visual Studio 2012 中的扩展。</span><span class="sxs-lookup"><span data-stu-id="316c0-262">The ASP.NET and Web Tools 2012.2 ships NuGet 2.1 and will upgrade the extension in Visual Studio 2012.</span></span> <span data-ttu-id="316c0-263">在某些情况下，VSIX 安装程序将无法正确更新 VSIX。</span><span class="sxs-lookup"><span data-stu-id="316c0-263">In some cases, the VSIX installer will fail to correctly update the VSIX.</span></span> <span data-ttu-id="316c0-264">以下步骤将允许您解决此问题：</span><span class="sxs-lookup"><span data-stu-id="316c0-264">The following steps will allow you to address this problem:</span></span>

1. <span data-ttu-id="316c0-265">以管理员身份开始视觉工作室 2012</span><span class="sxs-lookup"><span data-stu-id="316c0-265">Start Visual Studio 2012 as an Administrator</span></span>
2. <span data-ttu-id="316c0-266">转到工具 -&gt;扩展和更新，卸载 NuGet。</span><span class="sxs-lookup"><span data-stu-id="316c0-266">Go to Tools-&gt;Extensions and Updates and uninstall NuGet.</span></span>
3. <span data-ttu-id="316c0-267">关闭 Visual Studio</span><span class="sxs-lookup"><span data-stu-id="316c0-267">Close Visual Studio</span></span>
4. <span data-ttu-id="316c0-268">导航到ASP.NET和 Web 工具 2012.2 安装文件夹：</span><span class="sxs-lookup"><span data-stu-id="316c0-268">Navigate to the ASP.NET and Web Tools 2012.2 installation folder:</span></span>

    1. <span data-ttu-id="316c0-269">对于视觉工作室 2012：**程序文件_微软 ASP.NET_ASP.NET 网络堆栈_视觉工作室 2012**</span><span class="sxs-lookup"><span data-stu-id="316c0-269">For Visual Studio 2012: **Program Files\Microsoft ASP.NET\ASP.NET Web Stack\Visual Studio 2012**</span></span>
    2. <span data-ttu-id="316c0-270">对于 Visual Studio 2012 Web 快讯：**程序文件_微软 ASP.NET_ASP.NET Web 堆栈_Visual Studio Express 2012 网页**</span><span class="sxs-lookup"><span data-stu-id="316c0-270">For Visual Studio 2012 Express for Web: **Program Files\Microsoft ASP.NET\ASP.NET Web Stack\Visual Studio Express 2012 for Web**</span></span>
5. <span data-ttu-id="316c0-271">双击 NuGet.Tools.vsix 重新安装 NuGet</span><span class="sxs-lookup"><span data-stu-id="316c0-271">Double click on the NuGet.Tools.vsix to reinstall NuGet</span></span>

### <a name="web-api-issues"></a><span data-ttu-id="316c0-272">Web API 问题</span><span class="sxs-lookup"><span data-stu-id="316c0-272">Web API Issues</span></span>

#### <a name="parsing-issues-in-filter-and-datetime-literals"></a><span data-ttu-id="316c0-273">分析$filter和 DateTime 文本中的问题</span><span class="sxs-lookup"><span data-stu-id="316c0-273">Parsing issues in $filter and DateTime literals</span></span>

<span data-ttu-id="316c0-274">OData URI 解析器无法正确解析部分日期时间文本。</span><span class="sxs-lookup"><span data-stu-id="316c0-274">The OData URI parser fails to parse partial datetime literals properly.</span></span> <span data-ttu-id="316c0-275">例如，$filter_开始 eq 日期时间'2012-12-31T12：00' 无法正确解析。</span><span class="sxs-lookup"><span data-stu-id="316c0-275">For example, $filter=start eq datetime'2012-12-31T12:00' fails to parse properly.</span></span> <span data-ttu-id="316c0-276">解决方法是使用完整的文本，$filter_开始 eq 日期时间'2012-12-31T12：00：00'。</span><span class="sxs-lookup"><span data-stu-id="316c0-276">A workaround is to use the full literal, $filter=start eq datetime'2012-12-31T12:00:00'.</span></span>

#### <a name="odata-doesnt-support-case-insensitive-property-names"></a><span data-ttu-id="316c0-277">OData 不支持不区分大小写的属性名称。</span><span class="sxs-lookup"><span data-stu-id="316c0-277">OData doesn't support case-insensitive property names.</span></span>

<span data-ttu-id="316c0-278">OData 不支持 OData 查询和 odata 路径中不区分大小写的属性名称。</span><span class="sxs-lookup"><span data-stu-id="316c0-278">OData doesn't support case-insensitive property names in OData queries and odata path.</span></span> <span data-ttu-id="316c0-279">请参阅工作项：</span><span class="sxs-lookup"><span data-stu-id="316c0-279">See workitems:</span></span>

- [http://aspnetwebstack.codeplex.com/workitem/366](http://aspnetwebstack.codeplex.com/workitem/366)
- [http://aspnetwebstack.codeplex.com/workitem/704](http://aspnetwebstack.codeplex.com/workitem/704)

<span data-ttu-id="316c0-280">如果用户在 javascript 客户端和服务器端具有不同的大小写，他们可能会遇到此问题。</span><span class="sxs-lookup"><span data-stu-id="316c0-280">If users have different casing on javascript client side and server side, they probably will encounter this issue.</span></span> <span data-ttu-id="316c0-281">此问题是在 odata 协议中设计的问题。</span><span class="sxs-lookup"><span data-stu-id="316c0-281">This issue is by design in odata protocol.</span></span> <span data-ttu-id="316c0-282">但是，许多用户报告此问题。</span><span class="sxs-lookup"><span data-stu-id="316c0-282">However, many users reports this issue.</span></span> <span data-ttu-id="316c0-283">要解决此问题，用户必须更正 URL 中的情况。</span><span class="sxs-lookup"><span data-stu-id="316c0-283">To work around it, users have to correct their cases in URL.</span></span>

#### <a name="default-odata-routing-conventions-doesnt-support-postput-on-navigation-property"></a><span data-ttu-id="316c0-284">默认 OData 路由约定不支持导航属性上的 POST/PUT。</span><span class="sxs-lookup"><span data-stu-id="316c0-284">Default OData routing conventions doesn't support POST/PUT on navigation property.</span></span>

<span data-ttu-id="316c0-285">默认 OData 路由约定不支持导航属性上的 POST/PUT。</span><span class="sxs-lookup"><span data-stu-id="316c0-285">Default OData routing conventions doesn't support POST/PUT on navigation property.</span></span> <span data-ttu-id="316c0-286">请参阅工作项[http://aspnetwebstack.codeplex.com/workitem/366](http://aspnetwebstack.codeplex.com/workitem/366)。</span><span class="sxs-lookup"><span data-stu-id="316c0-286">See workitem [http://aspnetwebstack.codeplex.com/workitem/366](http://aspnetwebstack.codeplex.com/workitem/366).</span></span> <span data-ttu-id="316c0-287">在默认约定中，我们缺少此常用约定。</span><span class="sxs-lookup"><span data-stu-id="316c0-287">We are missing this commonly used convention in default conventions.</span></span>

<span data-ttu-id="316c0-288">要解决它，用户需要扩展新的路由约定来支持它。</span><span class="sxs-lookup"><span data-stu-id="316c0-288">To work around it, users need to extend new routing convention to support it.</span></span>

### <a name="facebook-template-issues"></a><span data-ttu-id="316c0-289">Facebook 模板问题</span><span class="sxs-lookup"><span data-stu-id="316c0-289">Facebook Template Issues</span></span>

#### <a name="facebook-application-template-only-works-using-net-45"></a><span data-ttu-id="316c0-290">Facebook 应用程序模板仅适用于 .NET 4.5</span><span class="sxs-lookup"><span data-stu-id="316c0-290">Facebook Application template only works using .NET 4.5</span></span>

<span data-ttu-id="316c0-291">您必须在"新项目"对话框的框架下拉列表中选择 .NET 4.5，才能在 mVC 4 ASP.NET中查看 Facebook 应用程序模板。</span><span class="sxs-lookup"><span data-stu-id="316c0-291">You must select .NET 4.5 in the framework dropdown list in the New Project dialog to see the Facebook Application template in ASP.NET MVC 4.</span></span>

#### <a name="real-time-update-controller"></a><span data-ttu-id="316c0-292">实时更新控制器</span><span class="sxs-lookup"><span data-stu-id="316c0-292">Real-time Update Controller</span></span>

<span data-ttu-id="316c0-293">Facebook 应用程序模板允许用户轻松创建 Web API 控制器来处理来自 Facebook 的实时更新。</span><span class="sxs-lookup"><span data-stu-id="316c0-293">The Facebook Application template allows user easily create a Web API Controller to handle real-time updates from Facebook.</span></span> <span data-ttu-id="316c0-294">如果开发计算机位于 NAT 之后，则如果没有进一步的网络配置，控制器可能无法工作。</span><span class="sxs-lookup"><span data-stu-id="316c0-294">If your development machine is behind NAT, your Controller may not work without further network configuration.</span></span> <span data-ttu-id="316c0-295">有关详细信息，请参阅此处：[http://facebook.stackoverflow.com/questions/5259467/can-a-computer-behind-a-nat-router-receive-realtime-updates-from-facebook](http://facebook.stackoverflow.com/questions/5259467/can-a-computer-behind-a-nat-router-receive-realtime-updates-from-facebook)</span><span class="sxs-lookup"><span data-stu-id="316c0-295">See here for details: [http://facebook.stackoverflow.com/questions/5259467/can-a-computer-behind-a-nat-router-receive-realtime-updates-from-facebook](http://facebook.stackoverflow.com/questions/5259467/can-a-computer-behind-a-nat-router-receive-realtime-updates-from-facebook)</span></span>

#### <a name="query-string-values-conflict-with-facebook-oauth-parameters"></a><span data-ttu-id="316c0-296">查询字符串值与 Facebook OAuth 参数冲突</span><span class="sxs-lookup"><span data-stu-id="316c0-296">Query string values conflict with Facebook OAuth parameters</span></span>

<span data-ttu-id="316c0-297">以下字段与 Facebook OAuth 对话框的回调 URL 冲突。</span><span class="sxs-lookup"><span data-stu-id="316c0-297">The following fields conflict with Facebook OAuth dialog's call back URL.</span></span> <span data-ttu-id="316c0-298">不要添加具有以下名称的查询字符串值：代码、错误、错误\_描述、错误\_原因。</span><span class="sxs-lookup"><span data-stu-id="316c0-298">Do not add your own query string values with the following names: code, error, error\_description, error\_reason.</span></span>

#### <a name="using-page-inspector-with-facebook-template"></a><span data-ttu-id="316c0-299">使用带有 Facebook 模板的页面检查器</span><span class="sxs-lookup"><span data-stu-id="316c0-299">Using Page Inspector with Facebook Template</span></span>

<span data-ttu-id="316c0-300">调试 Facebook 应用程序时，不能在 Visual Studio 2012 中使用页面检查器功能。</span><span class="sxs-lookup"><span data-stu-id="316c0-300">You can't use the Page Inspector feature in Visual Studio 2012 while debugging your Facebook Application.</span></span> <span data-ttu-id="316c0-301">页面检查器当前不支持 iframe。</span><span class="sxs-lookup"><span data-stu-id="316c0-301">The Page Inspector does not currently support iframes.</span></span>

### <a name="single-page-application-template-issues"></a><span data-ttu-id="316c0-302">单页应用程序模板问题</span><span class="sxs-lookup"><span data-stu-id="316c0-302">Single Page Application Template Issues</span></span>

#### <a name="with-jquery-19knockout-221-update-when-running-default-mvc-spa-project-new-todo-item-edit-enter-focus-event-is-not-handled-properly"></a><span data-ttu-id="316c0-303">使用 JQuery 1.9/挖空 2.2.1 更新时，在运行默认 MVC SPA 项目时，新的 todo 项编辑输入焦点事件处理不正确。</span><span class="sxs-lookup"><span data-stu-id="316c0-303">With JQuery 1.9/Knockout 2.2.1 update, when running default MVC SPA project, new todo item edit enter focus event is not handled properly.</span></span>

<span data-ttu-id="316c0-304">使用 JQuery 1.9/挖空 2.2.1 更新，在运行默认 MVC SPA 项目时，新待办事项编辑在进入待办事项列表的新待办事项后不再聚焦到新的待办事项编辑框。</span><span class="sxs-lookup"><span data-stu-id="316c0-304">With JQuery 1.9/Knockout 2.2.1 update, when running default MVC SPA project, new todo item edit enter no longer focus back to the new todo item edit box after entering the new todo item to the todo list.</span></span>

<span data-ttu-id="316c0-305">要进行解决方法引用[http://knockoutjs.com/documentation/hasfocus-binding.html](http://knockoutjs.com/documentation/hasfocus-binding.html)，并针对以下示例代码进行类似的修复：</span><span class="sxs-lookup"><span data-stu-id="316c0-305">To workaround reference [http://knockoutjs.com/documentation/hasfocus-binding.html](http://knockoutjs.com/documentation/hasfocus-binding.html), and make similar fix to the following sample code:</span></span>

<span data-ttu-id="316c0-306">文件 todo.model.js</span><span class="sxs-lookup"><span data-stu-id="316c0-306">File todo.model.js</span></span>  
 <span data-ttu-id="316c0-307">函数待办事项（数据），添加以下内容：</span><span class="sxs-lookup"><span data-stu-id="316c0-307">function todolist(data), add following:</span></span>  
 <span data-ttu-id="316c0-308">**自我.is选定 = ko.可观察（假）;**</span><span class="sxs-lookup"><span data-stu-id="316c0-308">**self.isSelected = ko.observable(false);**</span></span>

<span data-ttu-id="316c0-309">函数 todoList.原型.addTodo，添加以下黑色文本：</span><span class="sxs-lookup"><span data-stu-id="316c0-309">function todoList.prototype.addTodo, add the following blacked text:</span></span>  
 <span data-ttu-id="316c0-310">**自我.是选择（真）;**</span><span class="sxs-lookup"><span data-stu-id="316c0-310">**self.isSelected(true);**</span></span>  
 <span data-ttu-id="316c0-311">自我.新托多标题（）;&quot;&quot;</span><span class="sxs-lookup"><span data-stu-id="316c0-311">self.newTodoTitle(&quot;&quot;);</span></span>

<span data-ttu-id="316c0-312">文件索引.cshtml，添加以下黑色文本：</span><span class="sxs-lookup"><span data-stu-id="316c0-312">File index.cshtml, add the following blacked text:</span></span>  
 <span data-ttu-id="316c0-313">&lt;表单数据绑定\*&quot;提交：添加Todo&quot;&gt;</span><span class="sxs-lookup"><span data-stu-id="316c0-313">&lt;form data-bind=&quot;submit: addTodo&quot;&gt;</span></span>  
 <span data-ttu-id="316c0-314">&lt;输入类=&quot;addTodo&quot; &quot;类型&quot;= 文本数据&quot;绑定= 值：newTodoTitle，占位符："在此处键入添加"，模糊OnEnter：true，**有焦点：是选定**，事件：[模糊：添加Todo]&quot; /&gt;</span><span class="sxs-lookup"><span data-stu-id="316c0-314">&lt;input class=&quot;addTodo&quot; type=&quot;text&quot; data-bind=&quot;value: newTodoTitle, placeholder: 'Type here to add', blurOnEnter: true, **hasfocus: isSelected**, event: { blur: addTodo }&quot; /&gt;</span></span>  
 <span data-ttu-id="316c0-315">&lt;/形式&gt;</span><span class="sxs-lookup"><span data-stu-id="316c0-315">&lt;/form&gt;</span></span>

---
uid: visual-studio/overview/2012/aspnet-and-web-tools-20122-release-notes-rtw
title: ASP.NET 和 Web 工具2012.2 发行说明 |Microsoft Docs
author: rick-anderson
description: ASP.NET 和 Web 工具2012.2 的发行说明。
ms.author: riande
ms.date: 02/14/2013
ms.assetid: 9534e58b-1d15-4f1d-b04c-10c79b9d8227
msc.legacyurl: /visual-studio/overview/2012/aspnet-and-web-tools-20122-release-notes-rtw
msc.type: content
ms.openlocfilehash: abd6d8ce0646852a194369589cb730fc98ecb3ad
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345589"
---
# <a name="aspnet-and-web-tools-20122-release-notes"></a><span data-ttu-id="c484a-103">ASP.NET 和 Web 工具 2012.2 发行说明</span><span class="sxs-lookup"><span data-stu-id="c484a-103">ASP.NET and Web Tools 2012.2 Release Notes</span></span>

> <span data-ttu-id="c484a-104">本文档介绍 ASP.NET 和 Web 工具2012.2 的版本。</span><span class="sxs-lookup"><span data-stu-id="c484a-104">This document describes the release of ASP.NET and Web Tools 2012.2.</span></span> <span data-ttu-id="c484a-105">它是 Visual Studio Web 工具和 ASP.NET 的更新。</span><span class="sxs-lookup"><span data-stu-id="c484a-105">It is an update to Visual Studio Web Tooling and ASP.NET.</span></span>

- [<span data-ttu-id="c484a-106">安装说明</span><span class="sxs-lookup"><span data-stu-id="c484a-106">Installation Notes</span></span>](#_Installation)
- [<span data-ttu-id="c484a-107">文档</span><span class="sxs-lookup"><span data-stu-id="c484a-107">Documentation</span></span>](#_Documentation)
- [<span data-ttu-id="c484a-108">支持</span><span class="sxs-lookup"><span data-stu-id="c484a-108">Support</span></span>](#_Support)
- [<span data-ttu-id="c484a-109">软件要求</span><span class="sxs-lookup"><span data-stu-id="c484a-109">Software Requirements</span></span>](#_Software_Requirements)
- [<span data-ttu-id="c484a-110">ASP.NET 和 Web 工具2012.2 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="c484a-110">New Features in ASP.NET and Web Tools 2012.2</span></span>](#_New_Features_in)

    - [<span data-ttu-id="c484a-111">工具</span><span class="sxs-lookup"><span data-stu-id="c484a-111">Tooling</span></span>](#_Tooling)
    - [<span data-ttu-id="c484a-112">Web 发布</span><span class="sxs-lookup"><span data-stu-id="c484a-112">Web Publishing</span></span>](#_Web_Publishing)
    - [<span data-ttu-id="c484a-113">ASP.NET MVC 模板</span><span class="sxs-lookup"><span data-stu-id="c484a-113">ASP.NET MVC Templates</span></span>](#_Templates)
    - [<span data-ttu-id="c484a-114">ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="c484a-114">ASP.NET Web API</span></span>](#_ASP.NET_Web_API)

    - [<span data-ttu-id="c484a-115">ASP.NET SignalR</span><span class="sxs-lookup"><span data-stu-id="c484a-115">ASP.NET SignalR</span></span>](#_ASP.NET_SignalR)
    - [<span data-ttu-id="c484a-116">ASP.NET 友好 URL</span><span class="sxs-lookup"><span data-stu-id="c484a-116">ASP.NET Friendly URLs</span></span>](#_ASP.NET_Friendly_URLs)
- [<span data-ttu-id="c484a-117">已知问题和重大更改</span><span class="sxs-lookup"><span data-stu-id="c484a-117">Known Issues and Breaking Changes</span></span>](#_Known_Issues_and)

<a id="_Installation"></a>
## <a name="installation-notes"></a><span data-ttu-id="c484a-118">安装说明</span><span class="sxs-lookup"><span data-stu-id="c484a-118">Installation Notes</span></span>

<span data-ttu-id="c484a-119">可使用 [Web 平台安装程序](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=ASPDOTNETandWebTools2012_2)安装 Visual Studio 2012 的 ASP.NET 和 Web 工具2012.2。</span><span class="sxs-lookup"><span data-stu-id="c484a-119">ASP.NET and Web Tools 2012.2 for Visual Studio 2012 can be installed using [Web Platform installer](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=ASPDOTNETandWebTools2012_2).</span></span> <span data-ttu-id="c484a-120">这是对 Visual Studio 2012 或 Visual Studio Express 2012 for Web 的更新，这是必需的。</span><span class="sxs-lookup"><span data-stu-id="c484a-120">This is an update to Visual Studio 2012 or Visual Studio Express 2012 for Web, which is required.</span></span> <span data-ttu-id="c484a-121">如果尚未安装 Visual Studio，将安装适用于 Web 的 Visual Studio Express 2012。</span><span class="sxs-lookup"><span data-stu-id="c484a-121">If you do not have Visual Studio installed, Visual Studio Express 2012 for Web will be installed.</span></span>

<span data-ttu-id="c484a-122">你还可以手动安装 ASP.NET 和 Web 工具2012.2。</span><span class="sxs-lookup"><span data-stu-id="c484a-122">You can also install ASP.NET and Web Tools 2012.2 manually.</span></span> <span data-ttu-id="c484a-123">必须安装 Visual Studio 2012 或 Visual Studio Express 2012 for Web。</span><span class="sxs-lookup"><span data-stu-id="c484a-123">You must have Visual Studio 2012 or Visual Studio Express 2012 for Web installed.</span></span> <span data-ttu-id="c484a-124">然后，使用以下说明：</span><span class="sxs-lookup"><span data-stu-id="c484a-124">Then use the following instructions:</span></span> 

1. <span data-ttu-id="c484a-125">从下载中心下载 [ASP.NET 和 Web framework 2012.2](https://download.microsoft.com/download/6/5/6/6562AFBE-9503-4E64-970C-1427133FCD73/AspNetWebTools2012Setup.exe) 安装程序。</span><span class="sxs-lookup"><span data-stu-id="c484a-125">Download [ASP.NET and Web Frameworks 2012.2](https://download.microsoft.com/download/6/5/6/6562AFBE-9503-4E64-970C-1427133FCD73/AspNetWebTools2012Setup.exe) installer from Download Center.</span></span>
2. <span data-ttu-id="c484a-126">出现提示时，请单击 "运行"。</span><span class="sxs-lookup"><span data-stu-id="c484a-126">When prompted click Run.</span></span> <span data-ttu-id="c484a-127">你还可以保存该文件，以便稍后运行。</span><span class="sxs-lookup"><span data-stu-id="c484a-127">You can also save the file to run it later.</span></span>
3. <span data-ttu-id="c484a-128">验证要更新的 Visual Studio 版本。</span><span class="sxs-lookup"><span data-stu-id="c484a-128">Verify the version of Visual Studio you will update.</span></span> <span data-ttu-id="c484a-129">可以通过启动要更新的 Visual Studio 来实现此目的。</span><span class="sxs-lookup"><span data-stu-id="c484a-129">You can do this by launching the Visual Studio you wish to update.</span></span> <span data-ttu-id="c484a-130">然后单击 "帮助" 菜单项。</span><span class="sxs-lookup"><span data-stu-id="c484a-130">Then click the Help menu item.</span></span>   
    ![](aspnet-and-web-tools-20122-release-notes-rtw/_static/image1.jpg)
4. <span data-ttu-id="c484a-131">如果你看到 &quot; 有关 web Microsoft Visual Studio 2012 的菜单项，请 &quot; 下载 [web 开发人员工具 2012.2-Visual Studio Express 2012 for web](https://go.microsoft.com/fwlink/?LinkID=282228)。</span><span class="sxs-lookup"><span data-stu-id="c484a-131">If you see the menu item &quot;About Microsoft Visual Studio 2012 for Web&quot; then download [Web Developer Tools 2012.2 - Visual Studio Express 2012 for Web](https://go.microsoft.com/fwlink/?LinkID=282228).</span></span> <span data-ttu-id="c484a-132">否则 [，下载 Web 开发人员工具 2012.2-Visual Studio 2012](https://go.microsoft.com/fwlink/?LinkID=282228)。</span><span class="sxs-lookup"><span data-stu-id="c484a-132">Otherwise download [Web Developer Tools 2012.2 - Visual Studio 2012](https://go.microsoft.com/fwlink/?LinkID=282228).</span></span>
5. <span data-ttu-id="c484a-133">出现提示时，请单击 "运行"。</span><span class="sxs-lookup"><span data-stu-id="c484a-133">When prompted click Run.</span></span> <span data-ttu-id="c484a-134">你还可以保存该文件，以便稍后运行。</span><span class="sxs-lookup"><span data-stu-id="c484a-134">You can also save the file to run it later.</span></span>

> [!NOTE]
> <span data-ttu-id="c484a-135">ASP.NET 和 Web 工具2012.2 版不包括 SQL Server Data Tools。</span><span class="sxs-lookup"><span data-stu-id="c484a-135">ASP.NET and Web Tools 2012.2 release does not include SQL Server Data Tools.</span></span> <span data-ttu-id="c484a-136">SQL Server 和 Microsoft Azure SQL 数据库提供了一组丰富的数据库工具，包括脱机项目支持的开发、架构比较和增强的数据库部署功能。</span><span class="sxs-lookup"><span data-stu-id="c484a-136">SQL Server and Windows Azure SQL Databases provides a richer set of database tooling including offline project-backed development, schema comparison and enhanced database deployment capabilities.</span></span> <span data-ttu-id="c484a-137">有关详细信息或安装 SQL Server Data Tools 访问 [https://go.microsoft.com/fwlink/?LinkID=237127](https://go.microsoft.com/fwlink/?LinkID=237127) 。</span><span class="sxs-lookup"><span data-stu-id="c484a-137">For more information or to install SQL Server Data Tools visit [https://go.microsoft.com/fwlink/?LinkID=237127](https://go.microsoft.com/fwlink/?LinkID=237127).</span></span>

<a id="_Documentation"></a>
## <a name="documentation"></a><span data-ttu-id="c484a-138">文档</span><span class="sxs-lookup"><span data-stu-id="c484a-138">Documentation</span></span>

<span data-ttu-id="c484a-139">ASP.NET 网站 ( 提供了有关 ASP.NET 和 Web 工具2012.2 的教程和其他信息 https://www.asp.net) 。</span><span class="sxs-lookup"><span data-stu-id="c484a-139">Tutorials and other information about ASP.NET and Web Tools 2012.2 are available from ASP.NET web site ( https://www.asp.net).</span></span>

<a id="_Support"></a>
## <a name="support"></a><span data-ttu-id="c484a-140">支持</span><span class="sxs-lookup"><span data-stu-id="c484a-140">Support</span></span>

<span data-ttu-id="c484a-141">ASP.NET 和 Web 工具2012.2 正式发布并受支持。</span><span class="sxs-lookup"><span data-stu-id="c484a-141">ASP.NET and Web Tools 2012.2 is officially released and supported.</span></span> <span data-ttu-id="c484a-142">你可以使用正常的支持渠道。</span><span class="sxs-lookup"><span data-stu-id="c484a-142">You can use your normal support channel.</span></span> <span data-ttu-id="c484a-143">你还可以将问题发布到 ASP.NET 论坛 ([https://forums.asp.net/](https://forums.asp.net/)) ，其中 ASP.NET 社区的成员经常能够提供非正式支持。</span><span class="sxs-lookup"><span data-stu-id="c484a-143">You can also post questions to the ASP.NET forums ([https://forums.asp.net/](https://forums.asp.net/)), where members of the ASP.NET community are frequently able to provide informal support.</span></span>

<a id="_Software_Requirements"></a>
## <a name="software-requirements"></a><span data-ttu-id="c484a-144">软件要求</span><span class="sxs-lookup"><span data-stu-id="c484a-144">Software Requirements</span></span>

<span data-ttu-id="c484a-145">ASP.NET 和 Web 工具2012.2 需要适用于 Web 的 Visual Studio 2012 或 Visual Studio Express 2012。</span><span class="sxs-lookup"><span data-stu-id="c484a-145">The ASP.NET and Web Tools 2012.2 requires Visual Studio 2012 or Visual Studio Express 2012 for Web.</span></span>

<a id="_New_Features_in"></a>
## <a name="new-features-in-aspnet-and-web-tools-20122"></a><span data-ttu-id="c484a-146">ASP.NET 和 Web 工具2012.2 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="c484a-146">New Features in ASP.NET and Web Tools 2012.2</span></span>

<span data-ttu-id="c484a-147">本部分介绍 ASP.NET 和 Web 工具2012.2 发行版中引入的功能。</span><span class="sxs-lookup"><span data-stu-id="c484a-147">This section describes features that have been introduced in the ASP.NET and Web Tools 2012.2 release.</span></span>

<a id="_Tooling"></a>
### <a name="tooling"></a><span data-ttu-id="c484a-148">工具</span><span class="sxs-lookup"><span data-stu-id="c484a-148">Tooling</span></span>

- <span data-ttu-id="c484a-149">Page Inspector</span><span class="sxs-lookup"><span data-stu-id="c484a-149">Page Inspector</span></span> 

    - <span data-ttu-id="c484a-150">支持 JavaScript 选择映射，Page Inspector 允许将动态添加到页面的项映射回相应的 JavaScript 代码。</span><span class="sxs-lookup"><span data-stu-id="c484a-150">Support JavaScript selection mapping allowing Page Inspector to map items that were dynamically added to the page back to the corresponding JavaScript code.</span></span>
    - <span data-ttu-id="c484a-151">能够实时查看 CSS 更新。</span><span class="sxs-lookup"><span data-stu-id="c484a-151">The ability to see CSS updates in real-time.</span></span>
    - <span data-ttu-id="c484a-152">有关详细信息，请参阅 [Page Inspector 中的 CSS 自动同步和 JavaScript 选择映射](https://blogs.msdn.com/b/webdev/archive/2012/12/14/css-auto-sync-and-javascript-selection-mapping-in-page-inspector.aspx)。</span><span class="sxs-lookup"><span data-stu-id="c484a-152">For more information, read [CSS Auto-Sync and JavaScript Selection Mapping in Page Inspector](https://blogs.msdn.com/b/webdev/archive/2012/12/14/css-auto-sync-and-javascript-selection-mapping-in-page-inspector.aspx).</span></span>
- <span data-ttu-id="c484a-153">编辑器</span><span class="sxs-lookup"><span data-stu-id="c484a-153">Editor</span></span> 

    - <span data-ttu-id="c484a-154">支持对 CoffeeScript、Mustache、Handlebars 和 JsRender 进行语法突出显示。</span><span class="sxs-lookup"><span data-stu-id="c484a-154">Support syntax highlighting for CoffeeScript, Mustache, Handlebars, and JsRender.</span></span>
    - <span data-ttu-id="c484a-155">HTML 编辑器为挖空绑定提供 Intellisense。</span><span class="sxs-lookup"><span data-stu-id="c484a-155">The HTML editor provides Intellisense for Knockout bindings.</span></span>
    - <span data-ttu-id="c484a-156">使用较少的可以更少的编辑和编译器支持构建动态 CSS。</span><span class="sxs-lookup"><span data-stu-id="c484a-156">LESS editing and compiler support to enable building dynamic CSS using LESS.</span></span>
    - <span data-ttu-id="c484a-157">将 JSON 粘贴为 .NET 类。</span><span class="sxs-lookup"><span data-stu-id="c484a-157">Paste JSON as a .NET class.</span></span> <span data-ttu-id="c484a-158">使用此特殊的 "粘贴" 命令将 JSON 粘贴到 c # 或 VB.NET 代码文件中，Visual Studio 将自动生成从 JSON 推断出的 .NET 类。</span><span class="sxs-lookup"><span data-stu-id="c484a-158">Using this Special Paste command to paste JSON into a C# or VB.NET code file, and Visual Studio will automatically generate .NET classes inferred from the JSON.</span></span>
- <span data-ttu-id="c484a-159">移动模拟器支持添加扩展性挂钩，以便可以将第三方模拟器安装为 VSIX。</span><span class="sxs-lookup"><span data-stu-id="c484a-159">Mobile Emulator support adds extensibility hooks so that third-party emulators can be installed as a VSIX.</span></span> <span data-ttu-id="c484a-160">在 F5 下拉列表中将显示已安装的仿真器，以便开发人员可以在各种移动设备上预览其网站。</span><span class="sxs-lookup"><span data-stu-id="c484a-160">The installed emulators will show up in the F5 dropdown, so that developers can preview their websites on a variety of mobile devices.</span></span> <span data-ttu-id="c484a-161">有关此功能的详细信息，请参阅 Scott Hanselman 的博客文章 [BrowserStack Visual Studio 的新的集成](http://www.hanselman.com/blog/CrossBrowserDebuggingIntegratedIntoVisualStudioWithBrowserStack.aspx)。</span><span class="sxs-lookup"><span data-stu-id="c484a-161">Read more about this feature in Scott Hanselman's blog entry on [the new BrowserStack integration with Visual Studio](http://www.hanselman.com/blog/CrossBrowserDebuggingIntegratedIntoVisualStudioWithBrowserStack.aspx).</span></span>

<a id="_Web_Publishing"></a>
### <a name="web-publishing"></a><span data-ttu-id="c484a-162">Web 发布</span><span class="sxs-lookup"><span data-stu-id="c484a-162">Web Publishing</span></span>

- <span data-ttu-id="c484a-163">网站项目现在具有与 Web 应用程序项目相同的发布体验，包括发布到 Microsoft Azure 网站。</span><span class="sxs-lookup"><span data-stu-id="c484a-163">Web site projects now have the same publishing experience as Web Application projects including publishing to Windows Azure Web Sites.</span></span>
- <span data-ttu-id="c484a-164">选择性发布 &#8211; 对于一个或多个文件，你可以在发布到 Web 部署终结点) 后 (执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="c484a-164">Selective publish &#8211; for one or more files you can perform the following actions (after publishing to a Web Deploy endpoint):</span></span> 

    - <span data-ttu-id="c484a-165">发布选定的文件。</span><span class="sxs-lookup"><span data-stu-id="c484a-165">Publish selected files.</span></span>
    - <span data-ttu-id="c484a-166">请参阅本地文件和远程文件之间的差异。</span><span class="sxs-lookup"><span data-stu-id="c484a-166">See the difference between a local file and a remote file.</span></span>
    - <span data-ttu-id="c484a-167">用远程文件更新本地文件，或用本地文件更新远程文件。</span><span class="sxs-lookup"><span data-stu-id="c484a-167">Update the local file with the remote file or update the remote file with the local file.</span></span>

<a id="_Templates"></a>
### <a name="aspnet-mvc-templates"></a><span data-ttu-id="c484a-168">ASP.NET MVC 模板</span><span class="sxs-lookup"><span data-stu-id="c484a-168">ASP.NET MVC Templates</span></span>

- <span data-ttu-id="c484a-169">新的 Facebook 应用程序模板可帮助你轻松编写 Facebook Canvas 应用程序。</span><span class="sxs-lookup"><span data-stu-id="c484a-169">The new Facebook Application template makes writing Facebook Canvas applications easy.</span></span> <span data-ttu-id="c484a-170">只需执行几个简单步骤，即可创建一个 Facebook 应用程序，从已登录用户获取数据并与其好友集成。</span><span class="sxs-lookup"><span data-stu-id="c484a-170">In a few simple steps, you can create a Facebook application that gets data from a logged in user and integrates with their friends.</span></span> <span data-ttu-id="c484a-171">该模板包含一个新库，可维护构建 Facebook 应用程序时涉及的所有管道（包括身份验证、权限、访问 Facebook 数据等），</span><span class="sxs-lookup"><span data-stu-id="c484a-171">The template includes a new library to take care of all the plumbing involved in building a Facebook app, including authentication, permissions, accessing Facebook data and more.</span></span> <span data-ttu-id="c484a-172">有关使用 Facebook 应用程序模板的详细信息，请参阅 [https://go.microsoft.com/fwlink/?LinkID=269921](https://go.microsoft.com/fwlink/?LinkID=269921) 。</span><span class="sxs-lookup"><span data-stu-id="c484a-172">For more information on using the Facebook Application template see [https://go.microsoft.com/fwlink/?LinkID=269921](https://go.microsoft.com/fwlink/?LinkID=269921).</span></span>
- <span data-ttu-id="c484a-173">使用新的单页应用程序 MVC 模板，开发人员可以在 ASP.NET Web API 之上使用 HTML 5、CSS 3 以及常用的 Knockout 和 jQuery JavaScript 库构建交互式客户端 Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="c484a-173">A new Single Page Application MVC template allows developers to build interactive client-side web apps using HTML 5, CSS 3, and the popular Knockout and jQuery JavaScript libraries, on top of ASP.NET Web API.</span></span> <span data-ttu-id="c484a-174">该模板包含一个 "todo" 列表应用程序，该应用程序演示了用于生成使用 RESTful server API 的 JavaScript HTML5 应用程序的常见做法。</span><span class="sxs-lookup"><span data-stu-id="c484a-174">The template includes a "todo" list application that demonstrates common practices for building a JavaScript HTML5 application that uses a RESTful server API.</span></span> <span data-ttu-id="c484a-175">有关详细信息，请参阅 [https://www.asp.net/single-page-application](../../../single-page-application/index.md) 。</span><span class="sxs-lookup"><span data-stu-id="c484a-175">You can read more at [https://www.asp.net/single-page-application](../../../single-page-application/index.md).</span></span>
- <span data-ttu-id="c484a-176">你现在可以创建一个将新模板添加到 "ASP.NET MVC 新项目" 对话框中的 VSIX。</span><span class="sxs-lookup"><span data-stu-id="c484a-176">You can now create a VSIX that adds new templates to the ASP.NET MVC New Project dialog.</span></span> <span data-ttu-id="c484a-177">了解以下操作： [https://go.microsoft.com/fwlink/?LinkId=275019](https://go.microsoft.com/fwlink/?LinkId=275019)</span><span class="sxs-lookup"><span data-stu-id="c484a-177">Learn how here: [https://go.microsoft.com/fwlink/?LinkId=275019](https://go.microsoft.com/fwlink/?LinkId=275019)</span></span>
- <span data-ttu-id="c484a-178">FixedDisplayModes 包 &#8211; MVC 项目模板已更新为包含新的 "FixedDisplayModes" NuGet 包，其中包含 MVC 4 中 bug 的解决方法。</span><span class="sxs-lookup"><span data-stu-id="c484a-178">FixedDisplayModes package &#8211; MVC project templates have been updated to include the new ‘FixedDisplayModes' NuGet package, which contains a workaround for a bug in MVC 4.</span></span> <span data-ttu-id="c484a-179">有关包中包含的修复的详细信息，请参阅此博客文章 ([https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx](https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx)) MVC 团队。</span><span class="sxs-lookup"><span data-stu-id="c484a-179">For more information on the fix contained in the package, refer to this blog post ([https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx](https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx)) from the MVC team.</span></span>

<a id="_ASP.NET_Web_API"></a>
### <a name="aspnet-web-api"></a><span data-ttu-id="c484a-180">ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="c484a-180">ASP.NET Web API</span></span>

<span data-ttu-id="c484a-181">利用几项新功能增强了 ASP.NET Web API：</span><span class="sxs-lookup"><span data-stu-id="c484a-181">ASP.NET Web API has been enhanced with several new features:</span></span>

- <span data-ttu-id="c484a-182">ASP.NET Web API OData</span><span class="sxs-lookup"><span data-stu-id="c484a-182">ASP.NET Web API OData</span></span>
- <span data-ttu-id="c484a-183">ASP.NET Web API 跟踪</span><span class="sxs-lookup"><span data-stu-id="c484a-183">ASP.NET Web API Tracing</span></span>
- <span data-ttu-id="c484a-184">ASP.NET Web API 帮助页</span><span class="sxs-lookup"><span data-stu-id="c484a-184">ASP.NET Web API Help Page</span></span>

#### <a name="aspnet-web-api-odata"></a><span data-ttu-id="c484a-185">ASP.NET Web API OData</span><span class="sxs-lookup"><span data-stu-id="c484a-185">ASP.NET Web API OData</span></span>

<span data-ttu-id="c484a-186">ASP.NET Web API OData 使你可以灵活地在任何数据源上构建具有丰富业务逻辑的 OData 终结点。</span><span class="sxs-lookup"><span data-stu-id="c484a-186">ASP.NET Web API OData gives you the flexibility you need to build OData endpoints with rich business logic over any data source.</span></span> <span data-ttu-id="c484a-187">通过 ASP.NET Web API OData 控制要公开的 OData 语义量。</span><span class="sxs-lookup"><span data-stu-id="c484a-187">With ASP.NET Web API OData you control the amount of OData semantics that you want to expose.</span></span> <span data-ttu-id="c484a-188">ASP.NET MVC 4 项目模板附带了 ASP.NET Web API OData，还可从 NuGet ([http://www.nuget.org/packages/microsoft.aspnet.webapi.odata](http://www.nuget.org/packages/microsoft.aspnet.webapi.odata)) 获得。</span><span class="sxs-lookup"><span data-stu-id="c484a-188">ASP.NET Web API OData is included with the ASP.NET MVC 4 project templates and is also available from NuGet ([http://www.nuget.org/packages/microsoft.aspnet.webapi.odata](http://www.nuget.org/packages/microsoft.aspnet.webapi.odata)).</span></span>

<span data-ttu-id="c484a-189">ASP.NET Web API OData 当前支持以下功能：</span><span class="sxs-lookup"><span data-stu-id="c484a-189">ASP.NET Web API OData currently supports the following features:</span></span>

- <span data-ttu-id="c484a-190">通过应用 [可查询] 属性启用 OData 查询语义。</span><span class="sxs-lookup"><span data-stu-id="c484a-190">Enable OData query semantics by applying the [Queryable] attribute.</span></span>
- <span data-ttu-id="c484a-191">轻松验证 OData 查询，并限制支持的查询选项、运算符和函数集。</span><span class="sxs-lookup"><span data-stu-id="c484a-191">Easily validate OData queries and restrict the set of supported query options, operators and functions.</span></span>
- <span data-ttu-id="c484a-192">参数直接绑定到 ODataQueryOptions，以获取查询的抽象语法树表示形式，然后可以对其进行验证并将其应用于 IQueryable 或 IEnumerable。</span><span class="sxs-lookup"><span data-stu-id="c484a-192">Parameter bind to ODataQueryOptions directly to get an abstract syntax tree representation of the query that can then be validated and applied to an IQueryable or IEnumerable.</span></span>
- <span data-ttu-id="c484a-193">通过在 [可查询] 特性上指定结果限制，启用服务驱动分页和下一页链接生成。</span><span class="sxs-lookup"><span data-stu-id="c484a-193">Enable service-driven paging and next page link generation by specifying result limits on [Queryable] attribute.</span></span>
- <span data-ttu-id="c484a-194">使用 $inlinecount 请求匹配资源总数的内联计数。</span><span class="sxs-lookup"><span data-stu-id="c484a-194">Request an inlined count of the total number of matching resources using $inlinecount.</span></span>
- <span data-ttu-id="c484a-195">控制 null 传播。</span><span class="sxs-lookup"><span data-stu-id="c484a-195">Control null propagation.</span></span>
- <span data-ttu-id="c484a-196">$Filter 中的任何/所有运算符。</span><span class="sxs-lookup"><span data-stu-id="c484a-196">Any/All operators in $filter.</span></span>
- <span data-ttu-id="c484a-197">按约定推理实体数据模型，或以类似于实体框架代码优先的方式显式自定义模型。</span><span class="sxs-lookup"><span data-stu-id="c484a-197">Infer an entity data model by convention or explicitly customize a model in a manner similar to Entity Framework Code-First.</span></span>
- <span data-ttu-id="c484a-198">通过从 EntitySetController 派生来公开实体集。</span><span class="sxs-lookup"><span data-stu-id="c484a-198">Expose entity sets by deriving from EntitySetController.</span></span>
- <span data-ttu-id="c484a-199">简单、可自定义的约定，用于公开导航属性、操作链接和实现 OData 操作。</span><span class="sxs-lookup"><span data-stu-id="c484a-199">Simple, customizable conventions for exposing navigation properties, manipulating links and implementing OData actions.</span></span>
- <span data-ttu-id="c484a-200">使用 MapODataRoute 扩展方法简化路由。</span><span class="sxs-lookup"><span data-stu-id="c484a-200">Simplified routing using the MapODataRoute extension method.</span></span>
- <span data-ttu-id="c484a-201">支持通过公开多个 EDM 模型进行版本控制。</span><span class="sxs-lookup"><span data-stu-id="c484a-201">Support for versioning by exposing multiple EDM models.</span></span>
- <span data-ttu-id="c484a-202">公开服务文档和 $metadata 以便可以为 Web API ( .NET、Windows Phone、Windows 应用商店等 ) 生成客户端。</span><span class="sxs-lookup"><span data-stu-id="c484a-202">Expose service document and $metadata so you can generate clients (.NET, Windows Phone, Windows Store, etc.) for your Web API.</span></span>
- <span data-ttu-id="c484a-203">支持 OData Atom、JSON 和 JSON 详细格式。</span><span class="sxs-lookup"><span data-stu-id="c484a-203">Support for the OData Atom, JSON, and JSON verbose formats.</span></span>
- <span data-ttu-id="c484a-204">创建、更新、部分更新 (修补程序) 和删除实体。</span><span class="sxs-lookup"><span data-stu-id="c484a-204">Create, update, partially update (PATCH) and delete entities.</span></span>
- <span data-ttu-id="c484a-205">查询和操作实体之间的关系。</span><span class="sxs-lookup"><span data-stu-id="c484a-205">Query and manipulate relationships between entities.</span></span>
- <span data-ttu-id="c484a-206">创建连接到路由的关系链接。</span><span class="sxs-lookup"><span data-stu-id="c484a-206">Create relationship links that wire up to your routes.</span></span>
- <span data-ttu-id="c484a-207">复杂类型。</span><span class="sxs-lookup"><span data-stu-id="c484a-207">Complex types.</span></span>
- <span data-ttu-id="c484a-208">实体类型继承。</span><span class="sxs-lookup"><span data-stu-id="c484a-208">Entity Type Inheritance.</span></span>
- <span data-ttu-id="c484a-209">集合属性。</span><span class="sxs-lookup"><span data-stu-id="c484a-209">Collection properties.</span></span>
- <span data-ttu-id="c484a-210">枚举.</span><span class="sxs-lookup"><span data-stu-id="c484a-210">Enums.</span></span>
- <span data-ttu-id="c484a-211">OData 操作。</span><span class="sxs-lookup"><span data-stu-id="c484a-211">OData actions.</span></span>
- <span data-ttu-id="c484a-212">建立在与 WCF 数据服务相同的基础上，即 ODataLib ([http://www.nuget.org/packages/microsoft.data.odata](http://www.nuget.org/packages/microsoft.data.odata)) 。</span><span class="sxs-lookup"><span data-stu-id="c484a-212">Built upon the same foundation as WCF Data Services, namely ODataLib ([http://www.nuget.org/packages/microsoft.data.odata](http://www.nuget.org/packages/microsoft.data.odata)).</span></span>

<span data-ttu-id="c484a-213">有关 ASP.NET Web API OData 的详细信息，请参阅 [https://go.microsoft.com/fwlink/?LinkId=271141](https://go.microsoft.com/fwlink/?LinkId=271141) 。</span><span class="sxs-lookup"><span data-stu-id="c484a-213">For more information on ASP.NET Web API OData see [https://go.microsoft.com/fwlink/?LinkId=271141](https://go.microsoft.com/fwlink/?LinkId=271141).</span></span>

#### <a name="aspnet-web-api-tracing"></a><span data-ttu-id="c484a-214">ASP.NET Web API 跟踪</span><span class="sxs-lookup"><span data-stu-id="c484a-214">ASP.NET Web API Tracing</span></span>

<span data-ttu-id="c484a-215">ASP.NET Web API 跟踪通过 .NET 跟踪集成 Web Api 中的跟踪数据。</span><span class="sxs-lookup"><span data-stu-id="c484a-215">ASP.NET Web API Tracing integrates tracing data from your web APIs with .NET Tracing.</span></span> <span data-ttu-id="c484a-216">它现在默认在 Web API 项目模板中启用。</span><span class="sxs-lookup"><span data-stu-id="c484a-216">It is now enabled by default in the Web API project template.</span></span> <span data-ttu-id="c484a-217">Web Api 的跟踪数据将发送到 "输出" 窗口，并通过 IntelliTrace 提供。</span><span class="sxs-lookup"><span data-stu-id="c484a-217">Tracing data for your web APIs is sent to the Output window and is made available through IntelliTrace.</span></span> <span data-ttu-id="c484a-218">ASP.NET Web API 跟踪，你可以通过与 [windows Azure 诊断](https://msdn.microsoft.com/library/windowsazure/hh411529.aspx)的集成，在 windows Azure 上托管时跟踪有关 Web API 的信息。</span><span class="sxs-lookup"><span data-stu-id="c484a-218">ASP.NET Web API Tracing enables you to trace information about your Web API when hosted on Windows Azure through integration with [Windows Azure Diagnostics](https://msdn.microsoft.com/library/windowsazure/hh411529.aspx).</span></span> <span data-ttu-id="c484a-219">你还可以使用 ASP.NET Web API 跟踪 NuGet 包 () 在任何应用程序中安装和启用 ASP.NET Web API 跟踪 [http://www.nuget.org/packages/microsoft.aspnet.webapi.tracing](http://www.nuget.org/packages/microsoft.aspnet.webapi.tracing) 。</span><span class="sxs-lookup"><span data-stu-id="c484a-219">You can also install and enable ASP.NET Web API Tracing in any application using the ASP.NET Web API Tracing NuGet package ([http://www.nuget.org/packages/microsoft.aspnet.webapi.tracing](http://www.nuget.org/packages/microsoft.aspnet.webapi.tracing)).</span></span>

<span data-ttu-id="c484a-220">有关配置和使用 ASP.NET Web API 跟踪的详细信息，请参阅 [https://go.microsoft.com/fwlink/?LinkID=269874](https://go.microsoft.com/fwlink/?LinkID=269874) 。</span><span class="sxs-lookup"><span data-stu-id="c484a-220">For more information on configuring and using ASP.NET Web API Tracing see [https://go.microsoft.com/fwlink/?LinkID=269874](https://go.microsoft.com/fwlink/?LinkID=269874).</span></span>

#### <a name="aspnet-web-api-help-page"></a><span data-ttu-id="c484a-221">ASP.NET Web API 帮助页</span><span class="sxs-lookup"><span data-stu-id="c484a-221">ASP.NET Web API Help Page</span></span>

<span data-ttu-id="c484a-222">默认情况下，"ASP.NET Web API 帮助" 页包含在 Web API 项目模板中。</span><span class="sxs-lookup"><span data-stu-id="c484a-222">The ASP.NET Web API Help Page is now included by default in the Web API project template.</span></span> <span data-ttu-id="c484a-223">ASP.NET Web API 帮助页自动生成 Web Api 的文档，包括 HTTP 终结点、支持的 HTTP 方法、参数以及示例请求和响应消息负载。</span><span class="sxs-lookup"><span data-stu-id="c484a-223">The ASP.NET Web API Help Page automatically generates documentation for web APIs including the HTTP endpoints, the supported HTTP methods, parameters and example request and response message payloads.</span></span> <span data-ttu-id="c484a-224">文档自动从代码中的注释提取。</span><span class="sxs-lookup"><span data-stu-id="c484a-224">Documentation is automatically pulled from comments in your code.</span></span> <span data-ttu-id="c484a-225">还可以使用 ASP.NET Web API 帮助页 NuGet 包 () 将 ASP.NET Web API 帮助页添加到任何应用程序 [http://www.nuget.org/packages/microsoft.aspnet.webapi.helppage](http://www.nuget.org/packages/microsoft.aspnet.webapi.helppage) 。</span><span class="sxs-lookup"><span data-stu-id="c484a-225">You can also add the ASP.NET Web API Help Page to any application using the ASP.NET Web API Help Page NuGet package ([http://www.nuget.org/packages/microsoft.aspnet.webapi.helppage](http://www.nuget.org/packages/microsoft.aspnet.webapi.helppage)).</span></span>

<span data-ttu-id="c484a-226">有关设置和自定义 ASP.NET Web API 帮助页的详细信息，请参阅 [https://go.microsoft.com/fwlink/?LinkId=271140](https://go.microsoft.com/fwlink/?LinkId=271140) 。</span><span class="sxs-lookup"><span data-stu-id="c484a-226">For more information on setting up and customizing the ASP.NET Web API Help Page see [https://go.microsoft.com/fwlink/?LinkId=271140](https://go.microsoft.com/fwlink/?LinkId=271140).</span></span>

<a id="_ASP.NET_SignalR"></a>
### <a name="aspnet-signalr"></a><span data-ttu-id="c484a-227">ASP.NET SignalR</span><span class="sxs-lookup"><span data-stu-id="c484a-227">ASP.NET SignalR</span></span>

<span data-ttu-id="c484a-228">ASP.NET SignalR 可让你轻松地将实时 web 功能添加到你的 ASP.NET 应用程序，使用 Websocket （如果可用），并在不使用时自动回退到其他技术。</span><span class="sxs-lookup"><span data-stu-id="c484a-228">ASP.NET SignalR makes it simple to add real-time web capabilities to your ASP.NET application, using WebSockets if available and automatically falling back to other techniques when it isn't.</span></span>

<span data-ttu-id="c484a-229">有关使用 ASP.NET SignalR 的详细信息，请参阅 [https://go.microsoft.com/fwlink/?LinkId=271271](https://go.microsoft.com/fwlink/?LinkId=271271) 。</span><span class="sxs-lookup"><span data-stu-id="c484a-229">For more information on using ASP.NET SignalR see [https://go.microsoft.com/fwlink/?LinkId=271271](https://go.microsoft.com/fwlink/?LinkId=271271).</span></span>

<a id="_ASP.NET_Friendly_URLs"></a>
### <a name="aspnet-friendly-urls"></a><span data-ttu-id="c484a-230">ASP.NET 友好 URL</span><span class="sxs-lookup"><span data-stu-id="c484a-230">ASP.NET Friendly URLs</span></span>

<span data-ttu-id="c484a-231">ASP.NET Microsoft.aspnet.friendlyurls 使得 web 窗体开发人员能够轻松地生成外观清晰的 Url (不) .aspx 扩展。</span><span class="sxs-lookup"><span data-stu-id="c484a-231">ASP.NET FriendlyURLs makes it very easy for web forms developers to generate cleaner looking URLs(without the .aspx extension).</span></span> <span data-ttu-id="c484a-232">它几乎不需要任何配置，并且可以与现有的 ASP.NET v4.0 应用程序一起使用。</span><span class="sxs-lookup"><span data-stu-id="c484a-232">It requires little to no configuration and can be used with existing ASP.NET v4.0 applications.</span></span> <span data-ttu-id="c484a-233">借助 Microsoft.aspnet.friendlyurls 功能，开发人员可以更轻松地向应用程序添加移动支持，方法是支持在桌面和移动视图之间切换。</span><span class="sxs-lookup"><span data-stu-id="c484a-233">The FriendlyURLs feature also makes it easier for developers to add mobile support to their applications, by supporting switching between desktop and mobile views.</span></span>

<span data-ttu-id="c484a-234">有关安装和使用 ASP.NET 友好 Url 的详细信息，请参阅 [http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx](http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="c484a-234">For more information on installing and using ASP.NET Friendly URLs see [http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx](http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx).</span></span>

<a id="_Known_Issues_and"></a>
## <a name="known-issues-and-breaking-changes"></a><span data-ttu-id="c484a-235">已知问题和重大更改</span><span class="sxs-lookup"><span data-stu-id="c484a-235">Known Issues and Breaking Changes</span></span>

<span data-ttu-id="c484a-236">本部分介绍 ASP.NET 和 Web 工具2012.2 发行版中的已知问题和重大更改。</span><span class="sxs-lookup"><span data-stu-id="c484a-236">This section describes known issues and breaking changes that are in the ASP.NET and Web Tools 2012.2 release.</span></span>

### <a name="installation-issues"></a><span data-ttu-id="c484a-237">安装问题</span><span class="sxs-lookup"><span data-stu-id="c484a-237">Installation Issues</span></span>

#### <a name="out-of-order-installs-of-visual-studio-2012"></a><span data-ttu-id="c484a-238">Visual Studio 2012 的顺序安装</span><span class="sxs-lookup"><span data-stu-id="c484a-238">Out of order installs of Visual Studio 2012</span></span>

<span data-ttu-id="c484a-239">安装 ASP.NET 和 Web 工具2012.2 后安装 Visual Studio 2012 的附加 SKU 需要修复操作。</span><span class="sxs-lookup"><span data-stu-id="c484a-239">Installing an additional SKU of Visual Studio 2012 after installing the ASP.NET and Web Tools 2012.2 will require a repair operation.</span></span> <span data-ttu-id="c484a-240">考虑以下序列：</span><span class="sxs-lookup"><span data-stu-id="c484a-240">Consider the following sequence:</span></span>

1. <span data-ttu-id="c484a-241">安装 Visual Studio 2012 Express for Web</span><span class="sxs-lookup"><span data-stu-id="c484a-241">Install Visual Studio 2012 Express for Web</span></span>
2. <span data-ttu-id="c484a-242">安装 ASP.NET 和 Web 工具2012。2</span><span class="sxs-lookup"><span data-stu-id="c484a-242">Install ASP.NET and Web Tools 2012.2</span></span>
3. <span data-ttu-id="c484a-243">安装 Visual Studio 2012 Professional、Premium 或旗舰版</span><span class="sxs-lookup"><span data-stu-id="c484a-243">Install Visual Studio 2012 Professional, Premium or Ultimate</span></span>

<span data-ttu-id="c484a-244">步骤2只会导致为 Express for Web 安装更新。</span><span class="sxs-lookup"><span data-stu-id="c484a-244">Step 2 would only result in installing updates for Express for Web.</span></span> <span data-ttu-id="c484a-245">若要确保在步骤3中安装的其他 SKU 包含更新，你将需要修复 ASP.NET 和 Web 工具2012.2 以安装最后安装的 SKU 的更新。</span><span class="sxs-lookup"><span data-stu-id="c484a-245">To ensure that the additional SKU installed during step 3 contains the update you will need to repair the ASP.NET and Web Tools 2012.2 to install the updates for the last SKU installed.</span></span> <span data-ttu-id="c484a-246">如果步骤1和3中的 Sku 反转，这同样适用。</span><span class="sxs-lookup"><span data-stu-id="c484a-246">This also applies if the SKUs in Step 1 and 3 are reversed.</span></span>

#### <a name="installing-microsoft-aspnet-and-web-tools-20122-when-visual-studio-is-open"></a><span data-ttu-id="c484a-247">Visual Studio 打开时安装 Microsoft ASP.NET 和 Web 工具2012。2</span><span class="sxs-lookup"><span data-stu-id="c484a-247">Installing Microsoft ASP.NET and Web Tools 2012.2 when Visual Studio is open</span></span>

<span data-ttu-id="c484a-248">如果在 Microsoft ASP.NET 和 Web 工具2012.2 的安装过程中打开了 VS，则 Visual Studio 可能会在错误的状态下结束。</span><span class="sxs-lookup"><span data-stu-id="c484a-248">If VS is open during installation of Microsoft ASP.NET and Web Tools 2012.2, Visual Studio might end up in a bad state.</span></span> <span data-ttu-id="c484a-249">建议用户在继续安装前关闭 Visual Studio 的所有实例。</span><span class="sxs-lookup"><span data-stu-id="c484a-249">It is recommended that users close all instances of Visual Studio before proceeding with install.</span></span>

#### <a name="canceling-aspnet-and-web-tools-20122-setup-in-the-middle-of-installation"></a><span data-ttu-id="c484a-250">在安装过程中取消 ASP.NET 和 Web 工具2012.2 安装程序</span><span class="sxs-lookup"><span data-stu-id="c484a-250">Canceling ASP.NET and Web Tools 2012.2 setup in the middle of installation</span></span>

<span data-ttu-id="c484a-251">如果在安装过程中取消 ASP.NET 和 Web 工具2012.2 安装程序，则 Visual Studio 将处于错误状态。</span><span class="sxs-lookup"><span data-stu-id="c484a-251">Canceling ASP.NET and Web Tools 2012.2 setup in the middle of installation will leave Visual Studio in a bad state.</span></span> <span data-ttu-id="c484a-252">若要解决此问题，请执行以下步骤：</span><span class="sxs-lookup"><span data-stu-id="c484a-252">To address this problem follow these steps:</span></span> 

- <span data-ttu-id="c484a-253">转到“添加/删除程序”</span><span class="sxs-lookup"><span data-stu-id="c484a-253">Go to Add Remove Programs</span></span>
- <span data-ttu-id="c484a-254">卸载 Microsoft ASP.NET 和 Web 工具2012.2 （如果存在）。</span><span class="sxs-lookup"><span data-stu-id="c484a-254">Uninstall Microsoft ASP.NET and Web Tools 2012.2, if present.</span></span>
- <span data-ttu-id="c484a-255">重新安装 Microsoft ASP.NET 和 Web 工具2012。2</span><span class="sxs-lookup"><span data-stu-id="c484a-255">Reinstall Microsoft ASP.NET and Web Tools 2012.2</span></span>

#### <a name="after-uninstalling-aspnet-and-web-tools-20122-the-aspnet-mvc-4-templates-and-razor-v2-web-site-templates-are-missing"></a><span data-ttu-id="c484a-256">卸载 ASP.NET 和 Web 工具2012.2 后，ASP.NET MVC 4 模板和 Razor v2 网站模板缺失</span><span class="sxs-lookup"><span data-stu-id="c484a-256">After uninstalling ASP.NET and Web Tools 2012.2 the ASP.NET MVC 4 templates and Razor v2 Web Site templates are missing</span></span>

<span data-ttu-id="c484a-257">卸载 ASP.NET 和 Web 工具2012.2 还将从 Visual Studio 2012 中卸载所有 ASP.NET MVC 4 和 Razor v2 网站模板。</span><span class="sxs-lookup"><span data-stu-id="c484a-257">Uninstalling ASP.NET and Web Tools 2012.2 will also uninstall all of ASP.NET MVC 4 and Razor v2 Web Site templates from Visual Studio 2012.</span></span>

<span data-ttu-id="c484a-258">解决方法是修复 Visual Studio 2012 安装，重新安装 ASP.NET MVC 4 和 Razor v2 网站模板。</span><span class="sxs-lookup"><span data-stu-id="c484a-258">The workaround is to repair your Visual Studio 2012 installation to reinstall ASP.NET MVC 4 and Razor v2 Web Site templates.</span></span>

### <a name="tooling-issues"></a><span data-ttu-id="c484a-259">工具问题</span><span class="sxs-lookup"><span data-stu-id="c484a-259">Tooling Issues</span></span>

#### <a name="nuget-error-reported-during-project-creation"></a><span data-ttu-id="c484a-260">项目创建过程中报告的 NuGet 错误</span><span class="sxs-lookup"><span data-stu-id="c484a-260">NuGet error reported during project creation</span></span>

<span data-ttu-id="c484a-261">安装 ASP.NET 和 Web 工具2012.2 后，创建 MVC 4 项目时可能会看到以下错误</span><span class="sxs-lookup"><span data-stu-id="c484a-261">After installing ASP.NET and Web Tools 2012.2 you may see the following error when creating an MVC 4 project</span></span>

![](aspnet-and-web-tools-20122-release-notes-rtw/_static/image1.png)

<span data-ttu-id="c484a-262">ASP.NET 和 Web 工具2012.2 随附了 NuGet 2.1，并将在 Visual Studio 2012 中升级扩展。</span><span class="sxs-lookup"><span data-stu-id="c484a-262">The ASP.NET and Web Tools 2012.2 ships NuGet 2.1 and will upgrade the extension in Visual Studio 2012.</span></span> <span data-ttu-id="c484a-263">在某些情况下，VSIX 安装程序将无法正确更新 VSIX。</span><span class="sxs-lookup"><span data-stu-id="c484a-263">In some cases, the VSIX installer will fail to correctly update the VSIX.</span></span> <span data-ttu-id="c484a-264">以下步骤可用于解决此问题：</span><span class="sxs-lookup"><span data-stu-id="c484a-264">The following steps will allow you to address this problem:</span></span>

1. <span data-ttu-id="c484a-265">以管理员身份启动 Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="c484a-265">Start Visual Studio 2012 as an Administrator</span></span>
2. <span data-ttu-id="c484a-266">请参阅 "工具"-" &gt; 扩展和更新" 和 "卸载 NuGet"。</span><span class="sxs-lookup"><span data-stu-id="c484a-266">Go to Tools-&gt;Extensions and Updates and uninstall NuGet.</span></span>
3. <span data-ttu-id="c484a-267">关闭 Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c484a-267">Close Visual Studio</span></span>
4. <span data-ttu-id="c484a-268">导航到 ASP.NET 和 Web 工具2012.2 安装文件夹：</span><span class="sxs-lookup"><span data-stu-id="c484a-268">Navigate to the ASP.NET and Web Tools 2012.2 installation folder:</span></span>

    1. <span data-ttu-id="c484a-269">对于 Visual Studio 2012： **Program FILES\MICROSOFT NET\ASP.NET Web Stack\Visual Studio 2012**</span><span class="sxs-lookup"><span data-stu-id="c484a-269">For Visual Studio 2012: **Program Files\Microsoft ASP.NET\ASP.NET Web Stack\Visual Studio 2012**</span></span>
    2. <span data-ttu-id="c484a-270">对于 Visual Studio 2012 Express for Web： **Program FILES\MICROSOFT NET\ASP.NET web Stack\Visual Studio Express 2012 For web**</span><span class="sxs-lookup"><span data-stu-id="c484a-270">For Visual Studio 2012 Express for Web: **Program Files\Microsoft ASP.NET\ASP.NET Web Stack\Visual Studio Express 2012 for Web**</span></span>
5. <span data-ttu-id="c484a-271">双击 "NuGet" 以重新安装 NuGet</span><span class="sxs-lookup"><span data-stu-id="c484a-271">Double click on the NuGet.Tools.vsix to reinstall NuGet</span></span>

### <a name="web-api-issues"></a><span data-ttu-id="c484a-272">Web API 问题</span><span class="sxs-lookup"><span data-stu-id="c484a-272">Web API Issues</span></span>

#### <a name="parsing-issues-in-filter-and-datetime-literals"></a><span data-ttu-id="c484a-273">分析 $filter 和日期时间文本中的问题</span><span class="sxs-lookup"><span data-stu-id="c484a-273">Parsing issues in $filter and DateTime literals</span></span>

<span data-ttu-id="c484a-274">OData URI 分析器无法正确分析部分日期时间文本。</span><span class="sxs-lookup"><span data-stu-id="c484a-274">The OData URI parser fails to parse partial datetime literals properly.</span></span> <span data-ttu-id="c484a-275">例如，$filter = start eq datetime ' 2012-12-31T12： 00 ' 无法正确分析。</span><span class="sxs-lookup"><span data-stu-id="c484a-275">For example, $filter=start eq datetime'2012-12-31T12:00' fails to parse properly.</span></span> <span data-ttu-id="c484a-276">解决方法是使用完整文本，$filter = start eq datetime ' 2012-12-31T12：00： 00 '。</span><span class="sxs-lookup"><span data-stu-id="c484a-276">A workaround is to use the full literal, $filter=start eq datetime'2012-12-31T12:00:00'.</span></span>

#### <a name="odata-doesnt-support-case-insensitive-property-names"></a><span data-ttu-id="c484a-277">OData 不支持不区分大小写的属性名。</span><span class="sxs-lookup"><span data-stu-id="c484a-277">OData doesn't support case-insensitive property names.</span></span>

<span data-ttu-id="c484a-278">Odata 在 OData 查询和 OData 路径中不支持不区分大小写的属性名。</span><span class="sxs-lookup"><span data-stu-id="c484a-278">OData doesn't support case-insensitive property names in OData queries and odata path.</span></span> <span data-ttu-id="c484a-279">请参阅工作项：</span><span class="sxs-lookup"><span data-stu-id="c484a-279">See workitems:</span></span>

- [http://aspnetwebstack.codeplex.com/workitem/366](http://aspnetwebstack.codeplex.com/workitem/366)
- [http://aspnetwebstack.codeplex.com/workitem/704](http://aspnetwebstack.codeplex.com/workitem/704)

<span data-ttu-id="c484a-280">如果用户在 javascript 客户端和服务器端具有不同的大小写，则可能会遇到此问题。</span><span class="sxs-lookup"><span data-stu-id="c484a-280">If users have different casing on javascript client side and server side, they probably will encounter this issue.</span></span> <span data-ttu-id="c484a-281">此问题是在 odata 协议中设计的。</span><span class="sxs-lookup"><span data-stu-id="c484a-281">This issue is by design in odata protocol.</span></span> <span data-ttu-id="c484a-282">但是，许多用户会报告此问题。</span><span class="sxs-lookup"><span data-stu-id="c484a-282">However, many users reports this issue.</span></span> <span data-ttu-id="c484a-283">若要解决此情况，用户必须在 URL 中更正其事例。</span><span class="sxs-lookup"><span data-stu-id="c484a-283">To work around it, users have to correct their cases in URL.</span></span>

#### <a name="default-odata-routing-conventions-doesnt-support-postput-on-navigation-property"></a><span data-ttu-id="c484a-284">默认 OData 路由约定不支持对导航属性进行 POST/PUT。</span><span class="sxs-lookup"><span data-stu-id="c484a-284">Default OData routing conventions doesn't support POST/PUT on navigation property.</span></span>

<span data-ttu-id="c484a-285">默认 OData 路由约定不支持对导航属性进行 POST/PUT。</span><span class="sxs-lookup"><span data-stu-id="c484a-285">Default OData routing conventions doesn't support POST/PUT on navigation property.</span></span> <span data-ttu-id="c484a-286">请参阅工作项 [http://aspnetwebstack.codeplex.com/workitem/366](http://aspnetwebstack.codeplex.com/workitem/366) 。</span><span class="sxs-lookup"><span data-stu-id="c484a-286">See workitem [http://aspnetwebstack.codeplex.com/workitem/366](http://aspnetwebstack.codeplex.com/workitem/366).</span></span> <span data-ttu-id="c484a-287">我们在默认约定中缺少此常用约定。</span><span class="sxs-lookup"><span data-stu-id="c484a-287">We are missing this commonly used convention in default conventions.</span></span>

<span data-ttu-id="c484a-288">若要解决此情况，用户需要扩展新的路由约定以支持它。</span><span class="sxs-lookup"><span data-stu-id="c484a-288">To work around it, users need to extend new routing convention to support it.</span></span>

### <a name="facebook-template-issues"></a><span data-ttu-id="c484a-289">Facebook 模板问题</span><span class="sxs-lookup"><span data-stu-id="c484a-289">Facebook Template Issues</span></span>

#### <a name="facebook-application-template-only-works-using-net-45"></a><span data-ttu-id="c484a-290">Facebook 应用程序模板仅适用于使用 .NET 4。5</span><span class="sxs-lookup"><span data-stu-id="c484a-290">Facebook Application template only works using .NET 4.5</span></span>

<span data-ttu-id="c484a-291">必须在 "新建项目" 对话框的 "框架" 下拉列表中选择 ".NET 4.5"，才能在 ASP.NET MVC 4 中查看 Facebook 应用程序模板。</span><span class="sxs-lookup"><span data-stu-id="c484a-291">You must select .NET 4.5 in the framework dropdown list in the New Project dialog to see the Facebook Application template in ASP.NET MVC 4.</span></span>

#### <a name="real-time-update-controller"></a><span data-ttu-id="c484a-292">实时更新控制器</span><span class="sxs-lookup"><span data-stu-id="c484a-292">Real-time Update Controller</span></span>

<span data-ttu-id="c484a-293">Facebook 应用程序模板允许用户轻松创建一个 Web API 控制器来处理 Facebook 的实时更新。</span><span class="sxs-lookup"><span data-stu-id="c484a-293">The Facebook Application template allows user easily create a Web API Controller to handle real-time updates from Facebook.</span></span> <span data-ttu-id="c484a-294">如果开发计算机位于 NAT 后面，则在没有进一步的网络配置的情况下，控制器可能不起作用。</span><span class="sxs-lookup"><span data-stu-id="c484a-294">If your development machine is behind NAT, your Controller may not work without further network configuration.</span></span> <span data-ttu-id="c484a-295">有关详细信息，请参阅此处： [http://facebook.stackoverflow.com/questions/5259467/can-a-computer-behind-a-nat-router-receive-realtime-updates-from-facebook](http://facebook.stackoverflow.com/questions/5259467/can-a-computer-behind-a-nat-router-receive-realtime-updates-from-facebook)</span><span class="sxs-lookup"><span data-stu-id="c484a-295">See here for details: [http://facebook.stackoverflow.com/questions/5259467/can-a-computer-behind-a-nat-router-receive-realtime-updates-from-facebook](http://facebook.stackoverflow.com/questions/5259467/can-a-computer-behind-a-nat-router-receive-realtime-updates-from-facebook)</span></span>

#### <a name="query-string-values-conflict-with-facebook-oauth-parameters"></a><span data-ttu-id="c484a-296">查询字符串值与 Facebook OAuth 参数冲突</span><span class="sxs-lookup"><span data-stu-id="c484a-296">Query string values conflict with Facebook OAuth parameters</span></span>

<span data-ttu-id="c484a-297">以下字段与 Facebook OAuth 对话的回调 URL 冲突。</span><span class="sxs-lookup"><span data-stu-id="c484a-297">The following fields conflict with Facebook OAuth dialog's call back URL.</span></span> <span data-ttu-id="c484a-298">不要添加您自己的具有以下名称的查询字符串值：代码、错误、错误 \_ 说明、错误 \_ 原因。</span><span class="sxs-lookup"><span data-stu-id="c484a-298">Do not add your own query string values with the following names: code, error, error\_description, error\_reason.</span></span>

#### <a name="using-page-inspector-with-facebook-template"></a><span data-ttu-id="c484a-299">将 Page Inspector 与 Facebook 模板结合使用</span><span class="sxs-lookup"><span data-stu-id="c484a-299">Using Page Inspector with Facebook Template</span></span>

<span data-ttu-id="c484a-300">调试 Facebook 应用程序时，不能使用 Visual Studio 2012 中的 Page Inspector 功能。</span><span class="sxs-lookup"><span data-stu-id="c484a-300">You can't use the Page Inspector feature in Visual Studio 2012 while debugging your Facebook Application.</span></span> <span data-ttu-id="c484a-301">Page Inspector 当前不支持 iframe。</span><span class="sxs-lookup"><span data-stu-id="c484a-301">The Page Inspector does not currently support iframes.</span></span>

### <a name="single-page-application-template-issues"></a><span data-ttu-id="c484a-302">单页应用程序模板问题</span><span class="sxs-lookup"><span data-stu-id="c484a-302">Single Page Application Template Issues</span></span>

#### <a name="with-jquery-19knockout-221-update-when-running-default-mvc-spa-project-new-todo-item-edit-enter-focus-event-is-not-handled-properly"></a><span data-ttu-id="c484a-303">通过 JQuery 1.9/挖空2.2.1 更新时，在运行默认 MVC SPA 项目时，不会正确处理新的 todo 项 "编辑输入焦点事件"。</span><span class="sxs-lookup"><span data-stu-id="c484a-303">With JQuery 1.9/Knockout 2.2.1 update, when running default MVC SPA project, new todo item edit enter focus event is not handled properly.</span></span>

<span data-ttu-id="c484a-304">通过 JQuery 1.9/挖空2.2.1 更新时，在运行默认 MVC SPA 项目时，在将新的 todo 项输入到 todo 列表中后，新的 todo 项 "编辑" 将不再焦点返回到 "新建 todo 项" 编辑框。</span><span class="sxs-lookup"><span data-stu-id="c484a-304">With JQuery 1.9/Knockout 2.2.1 update, when running default MVC SPA project, new todo item edit enter no longer focus back to the new todo item edit box after entering the new todo item to the todo list.</span></span>

<span data-ttu-id="c484a-305">若要解决 [http://knockoutjs.com/documentation/hasfocus-binding.html](http://knockoutjs.com/documentation/hasfocus-binding.html) 此问题，请参考下面的示例代码：</span><span class="sxs-lookup"><span data-stu-id="c484a-305">To workaround reference [http://knockoutjs.com/documentation/hasfocus-binding.html](http://knockoutjs.com/documentation/hasfocus-binding.html), and make similar fix to the following sample code:</span></span>

<span data-ttu-id="c484a-306">文件 todo.model.js</span><span class="sxs-lookup"><span data-stu-id="c484a-306">File todo.model.js</span></span>  
 <span data-ttu-id="c484a-307">函数 todolist (数据) ，添加以下内容：</span><span class="sxs-lookup"><span data-stu-id="c484a-307">function todolist(data), add following:</span></span>  
 <span data-ttu-id="c484a-308">**isSelected = ko (false) ;**</span><span class="sxs-lookup"><span data-stu-id="c484a-308">**self.isSelected = ko.observable(false);**</span></span>

<span data-ttu-id="c484a-309">函数 todoList，添加以下涂黑文本：</span><span class="sxs-lookup"><span data-stu-id="c484a-309">function todoList.prototype.addTodo, add the following blacked text:</span></span>  
 <span data-ttu-id="c484a-310">**isSelected (true) ;**</span><span class="sxs-lookup"><span data-stu-id="c484a-310">**self.isSelected(true);**</span></span>  
 <span data-ttu-id="c484a-311">newTodoTitle (&quot; &quot;) ;</span><span class="sxs-lookup"><span data-stu-id="c484a-311">self.newTodoTitle(&quot;&quot;);</span></span>

<span data-ttu-id="c484a-312">文件索引 cshtml，添加以下涂黑文本：</span><span class="sxs-lookup"><span data-stu-id="c484a-312">File index.cshtml, add the following blacked text:</span></span>  
 <span data-ttu-id="c484a-313">&lt;表单数据-bind = &quot; submit： addTodo&quot;&gt;</span><span class="sxs-lookup"><span data-stu-id="c484a-313">&lt;form data-bind=&quot;submit: addTodo&quot;&gt;</span></span>  
 <span data-ttu-id="c484a-314">&lt;输入类 = &quot; addTodo &quot; 类型 = &quot; 文本 &quot; 数据-Bind = &quot; 值： newTodoTitle，占位符： "在此处添加的类型"，blurOnEnter： true， **hasfocus： isSelected**，事件： {模糊： addTodo}&quot; /&gt;</span><span class="sxs-lookup"><span data-stu-id="c484a-314">&lt;input class=&quot;addTodo&quot; type=&quot;text&quot; data-bind=&quot;value: newTodoTitle, placeholder: 'Type here to add', blurOnEnter: true, **hasfocus: isSelected**, event: { blur: addTodo }&quot; /&gt;</span></span>  
 <span data-ttu-id="c484a-315">&lt;/form&gt;</span><span class="sxs-lookup"><span data-stu-id="c484a-315">&lt;/form&gt;</span></span>

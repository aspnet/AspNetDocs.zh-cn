---
uid: web-pages/overview/getting-started/aspnet-web-pages-razor-faq
title: ASP.NET网页（剃须刀）常见问题 |微软文档
author: Rick-Anderson
description: 本文列出了一些关于ASP.NET网页（Razor）和WebMatrix的常见问题。 教程中使用的软件版本ASP.NET网页 （R...
ms.author: riande
ms.date: 02/07/2014
ms.assetid: b137bd04-25e1-47cb-9d96-ef2e179ecf1f
msc.legacyurl: /web-pages/overview/getting-started/aspnet-web-pages-razor-faq
msc.type: authoredcontent
ms.openlocfilehash: a312d1327bc88e721bf7fc7459e420e3f582c88d
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543699"
---
# <a name="aspnet-web-pages-razor-faq"></a><span data-ttu-id="899fe-104">ASP.NET 网页 (Razor) 常见问题解答</span><span class="sxs-lookup"><span data-stu-id="899fe-104">ASP.NET Web Pages (Razor) FAQ</span></span>

<span data-ttu-id="899fe-105"> 作者 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="899fe-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> > [!NOTE] 
> > <span data-ttu-id="899fe-106">不再建议将 WebMatrix 作为ASP.NET网页的集成开发环境。</span><span class="sxs-lookup"><span data-stu-id="899fe-106">WebMatrix is no longer recommended as an integrated development environment for ASP.NET Web Pages.</span></span> <span data-ttu-id="899fe-107">使用[视觉工作室](xref:web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio)或[视觉工作室代码](https://code.visualstudio.com/)。</span><span class="sxs-lookup"><span data-stu-id="899fe-107">Use [Visual Studio](xref:web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio) or [Visual Studio Code](https://code.visualstudio.com/).</span></span>
>
> <span data-ttu-id="899fe-108">本文列出了一些关于ASP.NET网页（Razor）和WebMatrix的常见问题。</span><span class="sxs-lookup"><span data-stu-id="899fe-108">This article lists some frequently asked questions about ASP.NET Web Pages (Razor) and WebMatrix.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="899fe-109">本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="899fe-109">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="899fe-110">ASP.NET网页 （剃须刀） 3</span><span class="sxs-lookup"><span data-stu-id="899fe-110">ASP.NET Web Pages (Razor) 3</span></span>
> - <span data-ttu-id="899fe-111">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="899fe-111">Visual Studio 2013</span></span>
> - <span data-ttu-id="899fe-112">Web矩阵 3</span><span class="sxs-lookup"><span data-stu-id="899fe-112">WebMatrix 3</span></span>
>   
> 
> <span data-ttu-id="899fe-113">本教程还适用于ASP.NET网页 2、WebMatrix 2 和 Visual Studio 2012。</span><span class="sxs-lookup"><span data-stu-id="899fe-113">This tutorial also works with ASP.NET Web Pages 2, WebMatrix 2, and Visual Studio 2012.</span></span>

- [<span data-ttu-id="899fe-114">ASP.NET网页、ASP.NET Web 窗体和 ASP.NET MVC 之间的区别是什么？</span><span class="sxs-lookup"><span data-stu-id="899fe-114">What's the difference between ASP.NET Web Pages, ASP.NET Web Forms, and ASP.NET MVC?</span></span>](#Whats_the_difference_between_ASP.NET_Web_Pages,_ASP.NET_Web_Forms,_and_ASP.NET_MVC)
- [<span data-ttu-id="899fe-115">我需要 WebMatrix 才能处理网页吗？</span><span class="sxs-lookup"><span data-stu-id="899fe-115">Do I need WebMatrix in order to work with Web Pages?</span></span>](#Do_I_need_WebMatrix_in_order_to_work_with_Web_Pages)
- [<span data-ttu-id="899fe-116">我可以在网页页面上使用ASP.NET Web 窗体控件吗？</span><span class="sxs-lookup"><span data-stu-id="899fe-116">Can I use ASP.NET Web Forms controls on a Web Pages page?</span></span>](#Can_I_use_ASP.NET_Web_Forms_controls_on_a_Web_Pages_page)
- [<span data-ttu-id="899fe-117">是否可以不使用 WebMatrix 部署ASP.NET网页网站？</span><span class="sxs-lookup"><span data-stu-id="899fe-117">Can I deploy an ASP.NET Web Pages site without using WebMatrix?</span></span>](#Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix)
- [<span data-ttu-id="899fe-118">我是否要使用 Web 安全帮助程序来支持登录？</span><span class="sxs-lookup"><span data-stu-id="899fe-118">Do I have to use the WebSecurity helper to support logins?</span></span>](#Do_I_have_to_use_the_WebSecurity_helper_to_support_logins)
- [<span data-ttu-id="899fe-119">ASP.NET网页是否支持 HTML5？</span><span class="sxs-lookup"><span data-stu-id="899fe-119">Does ASP.NET Web Pages support HTML5?</span></span>](#Does_ASP.NET_Web_Pages_support_HTML5)
- [<span data-ttu-id="899fe-120">我可以将 JavaScript 和 jQuery 与网页一起使用吗？</span><span class="sxs-lookup"><span data-stu-id="899fe-120">Can I use JavaScript and jQuery with Web Pages?</span></span>](#Can_I_use_JavaScript_and_jQuery_with_Web_Pages)
- [<span data-ttu-id="899fe-121">其他资源</span><span class="sxs-lookup"><span data-stu-id="899fe-121">Additional Resources</span></span>](#AdditionalResources)

<span data-ttu-id="899fe-122">有关错误和其他问题的问题，请参阅[ASP.NET网页 （Razor） 故障排除指南](https://go.microsoft.com/fwlink/?LinkId=253001)。</span><span class="sxs-lookup"><span data-stu-id="899fe-122">For questions about errors and other issues, see the [ASP.NET Web Pages (Razor) Troubleshooting Guide](https://go.microsoft.com/fwlink/?LinkId=253001).</span></span>

<a id="Whats_the_difference_between_ASP.NET_Web_Pages,_ASP.NET_Web_Forms,_and_ASP.NET_MVC"></a>
## <a name="whats-the-difference-between-aspnet-web-pages-aspnet-web-forms-and-aspnet-mvc"></a><span data-ttu-id="899fe-123">ASP.NET网页、ASP.NET Web 窗体和 ASP.NET MVC 之间的区别是什么？</span><span class="sxs-lookup"><span data-stu-id="899fe-123">What's the difference between ASP.NET Web Pages, ASP.NET Web Forms, and ASP.NET MVC?</span></span>

<span data-ttu-id="899fe-124">这三种技术都是创建动态 Web 应用程序的ASP.NET技术：</span><span class="sxs-lookup"><span data-stu-id="899fe-124">All three are ASP.NET technologies for creating dynamic web applications:</span></span>

- <span data-ttu-id="899fe-125">ASP.NET网页侧重于添加对 HTML 页的动态（服务器端）代码和数据库访问，并具有简单和轻量级的语法。</span><span class="sxs-lookup"><span data-stu-id="899fe-125">ASP.NET Web Pages focuses on adding dynamic (server-side) code and database access to HTML pages, and features simple and lightweight syntax.</span></span>
- <span data-ttu-id="899fe-126">ASP.NET Web 窗体基于页面对象模型和传统的窗口类型控件（按钮、列表等）。</span><span class="sxs-lookup"><span data-stu-id="899fe-126">ASP.NET Web Forms is based on a page object model and traditional window-type controls (buttons, lists, etc.).</span></span> <span data-ttu-id="899fe-127">Web 窗体使用基于事件的模型，这些模型是熟悉那些使用基于客户端（Windows 窗体）开发的人所熟悉的。</span><span class="sxs-lookup"><span data-stu-id="899fe-127">Web Forms uses an event-based model that's familiar to those who've worked with client-based (Windows forms) development.</span></span>
- <span data-ttu-id="899fe-128">ASP.NET MVC 实现ASP.NET的模型视图控制器模式。</span><span class="sxs-lookup"><span data-stu-id="899fe-128">ASP.NET MVC implements the model-view-controller pattern for ASP.NET.</span></span> <span data-ttu-id="899fe-129">重点是"关注点分离"（处理、数据和 UI 层）。</span><span class="sxs-lookup"><span data-stu-id="899fe-129">The emphasis is on "separation of concerns" (processing, data, and UI layers).</span></span>

<span data-ttu-id="899fe-130">所有三个框架都得到ASP.NET团队的充分支持，并继续得到开发。</span><span class="sxs-lookup"><span data-stu-id="899fe-130">All three frameworks are fully supported and continue to be developed by the ASP.NET team.</span></span> <span data-ttu-id="899fe-131">通常，选择使用哪个框架取决于您的背景和ASP.NET的经验。</span><span class="sxs-lookup"><span data-stu-id="899fe-131">In general, the choice of which framework to use depends on your background and experience with ASP.NET.</span></span>

<span data-ttu-id="899fe-132">ASP.NET网页是为了让那些已经了解 HTML 的用户轻松地将服务器处理添加到其页面。</span><span class="sxs-lookup"><span data-stu-id="899fe-132">ASP.NET Web Pages in particular was designed to make it easy for people who already know HTML to add server processing to their pages.</span></span> <span data-ttu-id="899fe-133">对于学生、业余爱好者、一般对编程新近的人来说，这是一个不错的选择。</span><span class="sxs-lookup"><span data-stu-id="899fe-133">It's a good choice for students, hobbyists, people in general who are new to programming.</span></span> <span data-ttu-id="899fe-134">对于具有non-ASP.NET Web 技术经验的开发人员来说，这也是一个不错的选择。</span><span class="sxs-lookup"><span data-stu-id="899fe-134">It can also be a good choice for developers who have experience with non-ASP.NET web technologies.</span></span>

<a id="Do_I_need_WebMatrix_in_order_to_work_with_Web_Pages"></a>
## <a name="do-i-need-webmatrix-in-order-to-work-with-web-pages"></a><span data-ttu-id="899fe-135">我需要 WebMatrix 才能处理网页吗？</span><span class="sxs-lookup"><span data-stu-id="899fe-135">Do I need WebMatrix in order to work with Web Pages?</span></span>

<span data-ttu-id="899fe-136">不是。</span><span class="sxs-lookup"><span data-stu-id="899fe-136">No.</span></span> <span data-ttu-id="899fe-137">不再建议将 WebMatrix 作为ASP.NET网页的集成开发环境。</span><span class="sxs-lookup"><span data-stu-id="899fe-137">WebMatrix is no longer recommended as an integrated development environment for ASP.NET Web Pages.</span></span> <span data-ttu-id="899fe-138">使用[视觉工作室](program-asp-net-web-pages-in-visual-studio.md)或[视觉工作室代码](https://code.visualstudio.com/)。</span><span class="sxs-lookup"><span data-stu-id="899fe-138">Use [Visual Studio](program-asp-net-web-pages-in-visual-studio.md) or [Visual Studio Code](https://code.visualstudio.com/).</span></span>

<span data-ttu-id="899fe-139">如果不想使用 Visual Studio 或 Visual Studio 代码，则可以使用[Microsoft Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)单独安装组件产品。</span><span class="sxs-lookup"><span data-stu-id="899fe-139">If you don't want to use either Visual Studio or Visual Studio Code, you can install the component products individually using [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx).</span></span> <span data-ttu-id="899fe-140">您需要以下产品：</span><span class="sxs-lookup"><span data-stu-id="899fe-140">You need the following products:</span></span>

- <span data-ttu-id="899fe-141">Microsoft .NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="899fe-141">Microsoft .NET Framework 4.5</span></span>
- <span data-ttu-id="899fe-142">ASP.NET MVC 5（也安装ASP.NET网页框架）</span><span class="sxs-lookup"><span data-stu-id="899fe-142">ASP.NET MVC 5 (which installs the ASP.NET Web Pages framework as well)</span></span>
- <span data-ttu-id="899fe-143">IIS 快递（网络服务器）</span><span class="sxs-lookup"><span data-stu-id="899fe-143">IIS Express (the web server)</span></span>
- <span data-ttu-id="899fe-144">微软 SQL 服务器紧凑型 4.0（数据库）</span><span class="sxs-lookup"><span data-stu-id="899fe-144">Microsoft SQL Server Compact 4.0 (the database)</span></span>

<span data-ttu-id="899fe-145">您可以使用文本编辑器编辑 *.cshtml* （或 *.vbhtml*） 页。</span><span class="sxs-lookup"><span data-stu-id="899fe-145">You can use a text editor to edit *.cshtml* (or *.vbhtml*) pages.</span></span>

<span data-ttu-id="899fe-146">在没有工具的情况下管理 SQL Server 紧凑数据库 *（.sdf*文件） 有点困难。</span><span class="sxs-lookup"><span data-stu-id="899fe-146">Managing SQL Server Compact databases (*.sdf* files) without a tool is a bit harder.</span></span> <span data-ttu-id="899fe-147">可视化工作室包含用于管理 *.sdf*数据库的工具。</span><span class="sxs-lookup"><span data-stu-id="899fe-147">Visual Studio containds tools for managing *.sdf* databases.</span></span> <span data-ttu-id="899fe-148">您还可以在代码中运行 SQL 命令以执行许多 SQL Server 管理任务。</span><span class="sxs-lookup"><span data-stu-id="899fe-148">You can also run SQL commands in code to perform many SQL Server management tasks.</span></span>

<span data-ttu-id="899fe-149">要测试 *.cshtml*页面而不使用集成开发环境 （IDE），可以将它们部署到实时服务器。</span><span class="sxs-lookup"><span data-stu-id="899fe-149">To test *.cshtml* pages without using an integrated development environment (IDE), you can deploy them to a live server.</span></span> <span data-ttu-id="899fe-150">（请参阅[不使用 WebMatrix 即可部署ASP.NET网页网站吗？](#Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix)</span><span class="sxs-lookup"><span data-stu-id="899fe-150">(See [Can I deploy an ASP.NET Web Pages site without using WebMatrix?](#Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix))</span></span>

### <a name="running-iis-express-without-using-an-ide"></a><span data-ttu-id="899fe-151">运行 IIS 快递而不使用 IDE</span><span class="sxs-lookup"><span data-stu-id="899fe-151">Running IIS Express without using an IDE</span></span>

<span data-ttu-id="899fe-152">如果在计算机上将 IIS Express 安装为 Web 服务器，则可以使用它来测试页面。</span><span class="sxs-lookup"><span data-stu-id="899fe-152">If you install IIS Express on your computer as a web server, you can use that to test the pages.</span></span> <span data-ttu-id="899fe-153">可以从命令行运行 IIS Express 并将其与特定的端口号相关联。</span><span class="sxs-lookup"><span data-stu-id="899fe-153">You can run IIS Express from the command line and associate it with a specific port number.</span></span> <span data-ttu-id="899fe-154">然后在浏览器中请求 *.cshtml*文件时指定该端口。</span><span class="sxs-lookup"><span data-stu-id="899fe-154">You then specify that port when you request *.cshtml* files in your browser.</span></span>

<span data-ttu-id="899fe-155">在 Windows 中，打开具有管理员权限的命令提示符，然后更改为*C：*程序文件_IIS Express。\*</span><span class="sxs-lookup"><span data-stu-id="899fe-155">In Windows, open a command prompt with administrator privileges and change to *C:\Program Files\IIS Express.*</span></span> <span data-ttu-id="899fe-156">（对于 64 位系统，请使用文件夹*C：*程序文件 （x86）\IIS Express。\* 然后输入以下命令，使用站点的实际路径：</span><span class="sxs-lookup"><span data-stu-id="899fe-156">(For 64-bit systems, use the folder *C:\Program Files (x86)\IIS Express.)* Then enter the following command, using the actual path to your site:</span></span>

`iisexpress.exe /port:35896 /path:C:\BasicWebSite`

<span data-ttu-id="899fe-157">您可以使用任何其他进程尚未保留的任何端口号。</span><span class="sxs-lookup"><span data-stu-id="899fe-157">You can use any port number that isn't already reserved by some other process.</span></span> <span data-ttu-id="899fe-158">（1024 以上的端口号通常是免费的。对于该`path`值，请使用 *.cshtml*文件所在的网站文件夹的路径。</span><span class="sxs-lookup"><span data-stu-id="899fe-158">(Port numbers above 1024 are typically free.) For the `path` value, use the path of the website folder where the *.cshtml* files are.</span></span>

<span data-ttu-id="899fe-159">运行此命令以设置 IIS Express 为页面提供服务后，可以打开浏览器并浏览到 *.cshtml*文件。</span><span class="sxs-lookup"><span data-stu-id="899fe-159">After you run this command to set up IIS Express to serve your pages, you can open a browser and browse to a *.cshtml* file.</span></span> <span data-ttu-id="899fe-160">使用如下所示的 URL：</span><span class="sxs-lookup"><span data-stu-id="899fe-160">Use a URL like the following:</span></span>

`http://localhost:35896/default.cshtml`

<span data-ttu-id="899fe-161">有关 IIS Express 命令行选项的帮助`iisexpress.exe /?`，请在命令行处输入。</span><span class="sxs-lookup"><span data-stu-id="899fe-161">For help with IIS Express command line options, enter `iisexpress.exe /?` at the command line.</span></span>

<a id="Can_I_use_ASP.NET_Web_Forms_controls_on_a_Web_Pages_page"></a>
## <a name="can-i-use-aspnet-web-forms-controls-on-a-web-pages-page"></a><span data-ttu-id="899fe-162">我可以在网页页面上使用ASP.NET Web 窗体控件吗？</span><span class="sxs-lookup"><span data-stu-id="899fe-162">Can I use ASP.NET Web Forms controls on a Web Pages page?</span></span>

<span data-ttu-id="899fe-163">不是。</span><span class="sxs-lookup"><span data-stu-id="899fe-163">No.</span></span> <span data-ttu-id="899fe-164">Web 窗体控件（如[CheckBox 控件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.checkbox)、[验证控件](https://msdn.microsoft.com/library/bwd43d0x)）和[GridView](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview)控件仅在 Web 窗体页 *（.aspx*文件）中工作。</span><span class="sxs-lookup"><span data-stu-id="899fe-164">Web Forms controls like the [CheckBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.checkbox) control, the [validation controls](https://msdn.microsoft.com/library/bwd43d0x), and the [GridView](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview) control only work in Web Forms pages (*.aspx* files).</span></span> <span data-ttu-id="899fe-165">这些控件需要 Web 窗体页面框架。</span><span class="sxs-lookup"><span data-stu-id="899fe-165">These controls require the Web Forms page framework.</span></span>

<a id="Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix"></a>
## <a name="can-i-deploy-an-aspnet-web-pages-site-without-using-webmatrix"></a><span data-ttu-id="899fe-166">是否可以不使用 WebMatrix 部署ASP.NET网页网站？</span><span class="sxs-lookup"><span data-stu-id="899fe-166">Can I deploy an ASP.NET Web Pages site without using WebMatrix?</span></span>

<span data-ttu-id="899fe-167">是的。</span><span class="sxs-lookup"><span data-stu-id="899fe-167">Yes.</span></span> <span data-ttu-id="899fe-168">您可以手动将网站文件复制到服务器（通常使用 FTP）。</span><span class="sxs-lookup"><span data-stu-id="899fe-168">You can manually copy website files to a server (typically by using FTP).</span></span> <span data-ttu-id="899fe-169">如果执行手动复制，还必须复制支持 SQL Server 压缩（数据库）的文件。</span><span class="sxs-lookup"><span data-stu-id="899fe-169">If you perform a manual copy, you also have to copy the files that support SQL Server Compact (the database).</span></span> <span data-ttu-id="899fe-170">有关详细信息，请参阅[没有工具部署网页应用程序的](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2317)博客条目。</span><span class="sxs-lookup"><span data-stu-id="899fe-170">For details, see the blog entry [Deploying Web Pages applications without a tool](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2317).</span></span>

<a id="Do_I_have_to_use_the_WebSecurity_helper_to_support_logins"></a>
## <a name="do-i-have-to-use-the-websecurity-helper-to-support-logins"></a><span data-ttu-id="899fe-171">我是否要使用 Web 安全帮助程序来支持登录？</span><span class="sxs-lookup"><span data-stu-id="899fe-171">Do I have to use the WebSecurity helper to support logins?</span></span>

<span data-ttu-id="899fe-172">不是。</span><span class="sxs-lookup"><span data-stu-id="899fe-172">No.</span></span> <span data-ttu-id="899fe-173">属于`SimpleMembership`ASP.NET网页的提供程序是一个选项。</span><span class="sxs-lookup"><span data-stu-id="899fe-173">The `SimpleMembership` provider that is part of ASP.NET Web Pages is one option.</span></span> <span data-ttu-id="899fe-174">属于ASP.NET（您可能习惯于在 Web 窗体中使用）的安全提供程序也可用。</span><span class="sxs-lookup"><span data-stu-id="899fe-174">The security providers that are part of ASP.NET (that you might be used to working with in Web Forms) are also available.</span></span> <span data-ttu-id="899fe-175">例如，您可以在ASP.NET网页中使用窗体身份验证，就像在 Web 窗体中一样。</span><span class="sxs-lookup"><span data-stu-id="899fe-175">For example, you can use forms authentication in ASP.NET Web Pages just as you would in Web Forms.</span></span> <span data-ttu-id="899fe-176">有关如何使用表单身份验证的一个示例，请参阅 Microsoft 支持文章["如何使用 C_.NET 在ASP.NET应用程序中实现基于表单的身份验证](https://support.microsoft.com/kb/301240)。</span><span class="sxs-lookup"><span data-stu-id="899fe-176">For one example of how to use forms authentication, see the Microsoft Support article [How To Implement Forms-Based Authentication in Your ASP.NET Application by Using C#.NET](https://support.microsoft.com/kb/301240).</span></span> <span data-ttu-id="899fe-177">要下载一个简单的示例，请参阅[ASP.NET版本的"登录&amp;密码](http://www.codeguru.com/csharp/.net/net_asp/scripting/article.php/c19295/ASPNET-version-of-Login--Password.htm)"。</span><span class="sxs-lookup"><span data-stu-id="899fe-177">To download a simple example, see [ASP.NET version of "Login &amp; Password](http://www.codeguru.com/csharp/.net/net_asp/scripting/article.php/c19295/ASPNET-version-of-Login--Password.htm).</span></span>

<span data-ttu-id="899fe-178">有关如何使用 Windows 身份验证的信息，请参阅[ASP.NET 网页中使用 Windows 身份验证的](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2298)博客文章。</span><span class="sxs-lookup"><span data-stu-id="899fe-178">For information about how to use Windows authentication, see the blog post [Using Windows authentication in ASP.NET Web Pages](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2298).</span></span>

<a id="Does_ASP.NET_Web_Pages_support_HTML5"></a>
## <a name="does-aspnet-web-pages-support-html5"></a><span data-ttu-id="899fe-179">ASP.NET网页是否支持 HTML5？</span><span class="sxs-lookup"><span data-stu-id="899fe-179">Does ASP.NET Web Pages support HTML5?</span></span>

<span data-ttu-id="899fe-180">是的。</span><span class="sxs-lookup"><span data-stu-id="899fe-180">Yes.</span></span> <span data-ttu-id="899fe-181">使用ASP.NET网页 *（.cshtml*或 *.vbhtml*页）创建的页面本质上是 HTML 页面，这些页面还包含在呈现页面之前在服务器上运行的代码。</span><span class="sxs-lookup"><span data-stu-id="899fe-181">The pages you create with ASP.NET Web Pages (*.cshtml* or *.vbhtml* pages) are essentially HTML pages that also contain code that runs on the server, before the page is rendered.</span></span> <span data-ttu-id="899fe-182">只要用户的浏览器支持 HTML5，就可以在 *.cshtml*或 *.vbhtml*页面中使用 HTML5 元素。</span><span class="sxs-lookup"><span data-stu-id="899fe-182">As long as the user's browser supports HTML5, you can use HTML5 elements in a *.cshtml* or *.vbhtml* page.</span></span>

<a id="Can_I_use_JavaScript_and_jQuery_with_Web_Pages"></a>
## <a name="can-i-use-javascript-and-jquery-with-web-pages"></a><span data-ttu-id="899fe-183">我可以将 JavaScript 和 jQuery 与网页一起使用吗？</span><span class="sxs-lookup"><span data-stu-id="899fe-183">Can I use JavaScript and jQuery with Web Pages?</span></span>

<span data-ttu-id="899fe-184">绝对是。</span><span class="sxs-lookup"><span data-stu-id="899fe-184">Absolutely.</span></span> <span data-ttu-id="899fe-185">使用ASP.NET网页 *（.cshtml*或 *.vbhtml*页）创建的页面只是包含服务器代码的 HTML 页。</span><span class="sxs-lookup"><span data-stu-id="899fe-185">The pages you create with ASP.NET Web Pages (*.cshtml* or *.vbhtml* pages) are just HTML pages with server code in them.</span></span> <span data-ttu-id="899fe-186">因此，使用 JavaScript 或 jQuery 可以在普通 HTML 页中执行的任何操作，您也可以在 *.cshtml*或 *.vbhtml*页中执行。</span><span class="sxs-lookup"><span data-stu-id="899fe-186">Therefore, anything you can do in a normal HTML page by using JavaScript or jQuery you can also do in a *.cshtml* or *.vbhtml* page.</span></span>

<span data-ttu-id="899fe-187">WebMatrix 中的**初学者网站**模板包含许多 jQuery 库。</span><span class="sxs-lookup"><span data-stu-id="899fe-187">The **Starter Site** template in WebMatrix contains a number of jQuery libraries.</span></span> <span data-ttu-id="899fe-188">如果使用该模板创建网站，*脚本*文件夹包含 jQuery 核心库 *（jquery-1.6.2.js）* 和 jQuery 验证库 *（jquery.validate.js*等）。</span><span class="sxs-lookup"><span data-stu-id="899fe-188">If you create a site by using that template, the *Scripts* folder contains a jQuery core library (*jquery-1.6.2.js)* and libraries for jQuery validation (*jquery.validate.js*, etc.).</span></span>

<span data-ttu-id="899fe-189">下面是一些博客文章，说明如何使用 jQuery 与ASP.NET网页：</span><span class="sxs-lookup"><span data-stu-id="899fe-189">Here are some blog posts that illustrate ways to use jQuery with ASP.NET Web Pages:</span></span>

- <span data-ttu-id="899fe-190">[将 jQuery 善用添加到 ASP.NET 网页，使用](http://rachelappel.com/jquery/adding-jquery-goodness-to-asp-net-web-pages-using-webmatrix/)Rachel Appel 的 WebMatrix</span><span class="sxs-lookup"><span data-stu-id="899fe-190">[Adding jQuery Goodness to ASP.NET Web Pages using WebMatrix](http://rachelappel.com/jquery/adding-jquery-goodness-to-asp-net-web-pages-using-webmatrix/) by Rachel Appel</span></span>
- <span data-ttu-id="899fe-191">[5分钟： WebMatrix + jQuery UI + json + jQuery模板](http://joeriks.com/2011/01/30/5-min-webmatrix-jquery-ui-json-jquery-templates/)由乔纳斯·埃里克森</span><span class="sxs-lookup"><span data-stu-id="899fe-191">[5 min: WebMatrix + jQuery UI + json + jQuery templates](http://joeriks.com/2011/01/30/5-min-webmatrix-jquery-ui-json-jquery-templates/) by Jonas Eriksson</span></span>
- <span data-ttu-id="899fe-192">迈克·布林德的[WebMatrix 和 jQuery 表单](http://mikesdotnetting.com/Article/155/WebMatrix-And-jQuery-Forms)</span><span class="sxs-lookup"><span data-stu-id="899fe-192">[WebMatrix And jQuery Forms](http://mikesdotnetting.com/Article/155/WebMatrix-And-jQuery-Forms) by Mike Brind</span></span>

<a id="AdditionalResources"></a>
## <a name="additional-resources"></a><span data-ttu-id="899fe-193">其他资源</span><span class="sxs-lookup"><span data-stu-id="899fe-193">Additional Resources</span></span>

[<span data-ttu-id="899fe-194">ASP.NET 网页 (Razor) 疑难解答指南</span><span class="sxs-lookup"><span data-stu-id="899fe-194">ASP.NET Web Pages (Razor) Troubleshooting Guide</span></span>](https://go.microsoft.com/fwlink/?LinkId=253001)

<span data-ttu-id="899fe-195">[网站网站WebMatrix和ASP.NET网页论坛](https://forums.asp.net/1224.aspx/1?WebMatrix)ASP.NET</span><span class="sxs-lookup"><span data-stu-id="899fe-195">[WebMatrix and ASP.NET Web Pages forum](https://forums.asp.net/1224.aspx/1?WebMatrix) on the ASP.NET website</span></span>

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
# <a name="aspnet-web-pages-razor-faq"></a>ASP.NET 网页 (Razor) 常见问题解答

 作者 [Tom FitzMacken](https://github.com/tfitzmac)

> > [!NOTE] 
> > 不再建议将 WebMatrix 作为ASP.NET网页的集成开发环境。 使用[视觉工作室](xref:web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio)或[视觉工作室代码](https://code.visualstudio.com/)。
>
> 本文列出了一些关于ASP.NET网页（Razor）和WebMatrix的常见问题。
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>本教程中使用的软件版本
> 
> 
> - ASP.NET网页 （剃须刀） 3
> - Visual Studio 2013
> - Web矩阵 3
>   
> 
> 本教程还适用于ASP.NET网页 2、WebMatrix 2 和 Visual Studio 2012。

- [ASP.NET网页、ASP.NET Web 窗体和 ASP.NET MVC 之间的区别是什么？](#Whats_the_difference_between_ASP.NET_Web_Pages,_ASP.NET_Web_Forms,_and_ASP.NET_MVC)
- [我需要 WebMatrix 才能处理网页吗？](#Do_I_need_WebMatrix_in_order_to_work_with_Web_Pages)
- [我可以在网页页面上使用ASP.NET Web 窗体控件吗？](#Can_I_use_ASP.NET_Web_Forms_controls_on_a_Web_Pages_page)
- [是否可以不使用 WebMatrix 部署ASP.NET网页网站？](#Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix)
- [我是否要使用 Web 安全帮助程序来支持登录？](#Do_I_have_to_use_the_WebSecurity_helper_to_support_logins)
- [ASP.NET网页是否支持 HTML5？](#Does_ASP.NET_Web_Pages_support_HTML5)
- [我可以将 JavaScript 和 jQuery 与网页一起使用吗？](#Can_I_use_JavaScript_and_jQuery_with_Web_Pages)
- [其他资源](#AdditionalResources)

有关错误和其他问题的问题，请参阅[ASP.NET网页 （Razor） 故障排除指南](https://go.microsoft.com/fwlink/?LinkId=253001)。

<a id="Whats_the_difference_between_ASP.NET_Web_Pages,_ASP.NET_Web_Forms,_and_ASP.NET_MVC"></a>
## <a name="whats-the-difference-between-aspnet-web-pages-aspnet-web-forms-and-aspnet-mvc"></a>ASP.NET网页、ASP.NET Web 窗体和 ASP.NET MVC 之间的区别是什么？

这三种技术都是创建动态 Web 应用程序的ASP.NET技术：

- ASP.NET网页侧重于添加对 HTML 页的动态（服务器端）代码和数据库访问，并具有简单和轻量级的语法。
- ASP.NET Web 窗体基于页面对象模型和传统的窗口类型控件（按钮、列表等）。 Web 窗体使用基于事件的模型，这些模型是熟悉那些使用基于客户端（Windows 窗体）开发的人所熟悉的。
- ASP.NET MVC 实现ASP.NET的模型视图控制器模式。 重点是"关注点分离"（处理、数据和 UI 层）。

所有三个框架都得到ASP.NET团队的充分支持，并继续得到开发。 通常，选择使用哪个框架取决于您的背景和ASP.NET的经验。

ASP.NET网页是为了让那些已经了解 HTML 的用户轻松地将服务器处理添加到其页面。 对于学生、业余爱好者、一般对编程新近的人来说，这是一个不错的选择。 对于具有non-ASP.NET Web 技术经验的开发人员来说，这也是一个不错的选择。

<a id="Do_I_need_WebMatrix_in_order_to_work_with_Web_Pages"></a>
## <a name="do-i-need-webmatrix-in-order-to-work-with-web-pages"></a>我需要 WebMatrix 才能处理网页吗？

不是。 不再建议将 WebMatrix 作为ASP.NET网页的集成开发环境。 使用[视觉工作室](program-asp-net-web-pages-in-visual-studio.md)或[视觉工作室代码](https://code.visualstudio.com/)。

如果不想使用 Visual Studio 或 Visual Studio 代码，则可以使用[Microsoft Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)单独安装组件产品。 您需要以下产品：

- Microsoft .NET Framework 4.5
- ASP.NET MVC 5（也安装ASP.NET网页框架）
- IIS 快递（网络服务器）
- 微软 SQL 服务器紧凑型 4.0（数据库）

您可以使用文本编辑器编辑 *.cshtml* （或 *.vbhtml*） 页。

在没有工具的情况下管理 SQL Server 紧凑数据库 *（.sdf*文件） 有点困难。 可视化工作室包含用于管理 *.sdf*数据库的工具。 您还可以在代码中运行 SQL 命令以执行许多 SQL Server 管理任务。

要测试 *.cshtml*页面而不使用集成开发环境 （IDE），可以将它们部署到实时服务器。 （请参阅[不使用 WebMatrix 即可部署ASP.NET网页网站吗？](#Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix)

### <a name="running-iis-express-without-using-an-ide"></a>运行 IIS 快递而不使用 IDE

如果在计算机上将 IIS Express 安装为 Web 服务器，则可以使用它来测试页面。 可以从命令行运行 IIS Express 并将其与特定的端口号相关联。 然后在浏览器中请求 *.cshtml*文件时指定该端口。

在 Windows 中，打开具有管理员权限的命令提示符，然后更改为*C：*程序文件_IIS Express。* （对于 64 位系统，请使用文件夹*C：*程序文件 （x86）\IIS Express。* 然后输入以下命令，使用站点的实际路径：

`iisexpress.exe /port:35896 /path:C:\BasicWebSite`

您可以使用任何其他进程尚未保留的任何端口号。 （1024 以上的端口号通常是免费的。对于该`path`值，请使用 *.cshtml*文件所在的网站文件夹的路径。

运行此命令以设置 IIS Express 为页面提供服务后，可以打开浏览器并浏览到 *.cshtml*文件。 使用如下所示的 URL：

`http://localhost:35896/default.cshtml`

有关 IIS Express 命令行选项的帮助`iisexpress.exe /?`，请在命令行处输入。

<a id="Can_I_use_ASP.NET_Web_Forms_controls_on_a_Web_Pages_page"></a>
## <a name="can-i-use-aspnet-web-forms-controls-on-a-web-pages-page"></a>我可以在网页页面上使用ASP.NET Web 窗体控件吗？

不是。 Web 窗体控件（如[CheckBox 控件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.checkbox)、[验证控件](https://msdn.microsoft.com/library/bwd43d0x)）和[GridView](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview)控件仅在 Web 窗体页 *（.aspx*文件）中工作。 这些控件需要 Web 窗体页面框架。

<a id="Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix"></a>
## <a name="can-i-deploy-an-aspnet-web-pages-site-without-using-webmatrix"></a>是否可以不使用 WebMatrix 部署ASP.NET网页网站？

是的。 您可以手动将网站文件复制到服务器（通常使用 FTP）。 如果执行手动复制，还必须复制支持 SQL Server 压缩（数据库）的文件。 有关详细信息，请参阅[没有工具部署网页应用程序的](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2317)博客条目。

<a id="Do_I_have_to_use_the_WebSecurity_helper_to_support_logins"></a>
## <a name="do-i-have-to-use-the-websecurity-helper-to-support-logins"></a>我是否要使用 Web 安全帮助程序来支持登录？

不是。 属于`SimpleMembership`ASP.NET网页的提供程序是一个选项。 属于ASP.NET（您可能习惯于在 Web 窗体中使用）的安全提供程序也可用。 例如，您可以在ASP.NET网页中使用窗体身份验证，就像在 Web 窗体中一样。 有关如何使用表单身份验证的一个示例，请参阅 Microsoft 支持文章["如何使用 C_.NET 在ASP.NET应用程序中实现基于表单的身份验证](https://support.microsoft.com/kb/301240)。 要下载一个简单的示例，请参阅[ASP.NET版本的"登录&amp;密码](http://www.codeguru.com/csharp/.net/net_asp/scripting/article.php/c19295/ASPNET-version-of-Login--Password.htm)"。

有关如何使用 Windows 身份验证的信息，请参阅[ASP.NET 网页中使用 Windows 身份验证的](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2298)博客文章。

<a id="Does_ASP.NET_Web_Pages_support_HTML5"></a>
## <a name="does-aspnet-web-pages-support-html5"></a>ASP.NET网页是否支持 HTML5？

是的。 使用ASP.NET网页 *（.cshtml*或 *.vbhtml*页）创建的页面本质上是 HTML 页面，这些页面还包含在呈现页面之前在服务器上运行的代码。 只要用户的浏览器支持 HTML5，就可以在 *.cshtml*或 *.vbhtml*页面中使用 HTML5 元素。

<a id="Can_I_use_JavaScript_and_jQuery_with_Web_Pages"></a>
## <a name="can-i-use-javascript-and-jquery-with-web-pages"></a>我可以将 JavaScript 和 jQuery 与网页一起使用吗？

绝对是。 使用ASP.NET网页 *（.cshtml*或 *.vbhtml*页）创建的页面只是包含服务器代码的 HTML 页。 因此，使用 JavaScript 或 jQuery 可以在普通 HTML 页中执行的任何操作，您也可以在 *.cshtml*或 *.vbhtml*页中执行。

WebMatrix 中的**初学者网站**模板包含许多 jQuery 库。 如果使用该模板创建网站，*脚本*文件夹包含 jQuery 核心库 *（jquery-1.6.2.js）* 和 jQuery 验证库 *（jquery.validate.js*等）。

下面是一些博客文章，说明如何使用 jQuery 与ASP.NET网页：

- [将 jQuery 善用添加到 ASP.NET 网页，使用](http://rachelappel.com/jquery/adding-jquery-goodness-to-asp-net-web-pages-using-webmatrix/)Rachel Appel 的 WebMatrix
- [5分钟： WebMatrix + jQuery UI + json + jQuery模板](http://joeriks.com/2011/01/30/5-min-webmatrix-jquery-ui-json-jquery-templates/)由乔纳斯·埃里克森
- 迈克·布林德的[WebMatrix 和 jQuery 表单](http://mikesdotnetting.com/Article/155/WebMatrix-And-jQuery-Forms)

<a id="AdditionalResources"></a>
## <a name="additional-resources"></a>其他资源

[ASP.NET 网页 (Razor) 疑难解答指南](https://go.microsoft.com/fwlink/?LinkId=253001)

[网站网站WebMatrix和ASP.NET网页论坛](https://forums.asp.net/1224.aspx/1?WebMatrix)ASP.NET

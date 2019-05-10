---
uid: web-pages/readme/beta3
title: Web Matrix 和 ASP.NET 网页 (Razor) Beta 3 版本自述文件 |Microsoft Docs
author: rick-anderson
description: Web Matrix 和 ASP.NET 网页 (Razor) Beta 3 版本自述文件
ms.author: riande
ms.date: 01/10/2011
ms.assetid: ffa3d5c9-91e5-4da3-b409-560b0c7fbbf0
msc.legacyurl: /web-pages/readme/beta3
msc.type: content
ms.openlocfilehash: dc1d9237c04a7fcdbf4db6ccc8c36d255f6de003
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/06/2019
ms.locfileid: "65124117"
---
# <a name="web-matrix-and-aspnet-web-pages-razor-beta-3-release-readme"></a>Web Matrix 和 ASP.NET 网页 (Razor) Beta 3 版本自述文件

> Web Matrix 和 ASP.NET 网页 (Razor) Beta 3 版本自述文件

2010 年 11 月 9日

## <a name="contents"></a>内容

- [概述](#Overview)
- [安装](#Installation_Notes)
- [新功能、 更改和 Beta 3 版本中的已知问题](#Known_Issues)

    - [WebMatrix 安装问题](#Known_Issues_Installation)
    - [ASP.NET 网页](#Known_Issues_ASPNET)
    - [SQL Server Compact](#Known_Issues_SQL_Server_Compact)
    - [安装应用程序](#Known_Issues_Installing_Applications)
    - [发布应用程序](#Known_Issues_Publishing_Applications)
    - [其他问题](#Known_Issues_Other_Issues)
- [更多信息](#More_Info)

<a id="Overview"></a>

## <a name="overview"></a>概述

> Microsoft WebMatrix Beta 是在几分钟内将安装免费的 web 开发堆栈。 它与数据库和编程框架用于创建单一的集成体验集成的 web 服务器。 你可以使用 WebMatrix Beta 来简化代码、 测试和发布自己的 ASP.NET 或 PHP 网站的方式或使用 WebMatrix Beta 启动新的网站使用 DotNetNuke、 Umbraco、 WordPress 或 Joomla 等受欢迎的开源应用。 WebMatrix beta 版使用相同的功能强大的 web 服务器、 数据库引擎和框架环境，将在 internet 上，这使从开发过渡到生产顺畅、 无缝运行你的网站。

<a id="Installation_Notes"></a>

## <a name="installation"></a>安装

> 若要安装 WebMatrix Beta 3，你可以使用[Microsoft Web 平台安装程序 3.0](https://go.microsoft.com/fwlink/?LinkID=194638)。 安装 Web 平台安装程序后，可用于安装 WebMatrix Beta 3。
> 
> 如果在安装过程中遇到问题，请参阅[问题的 Microsoft Web 平台安装程序疑难解答](https://go.microsoft.com/fwlink/?LinkId=196212)。

<a id="Installation_Notes0"></a>

## <a name="instructions-for-publishing-applications"></a>有关发布应用程序的说明

> 请参阅[发布应用程序的分步说明](https://go.microsoft.com/fwlink/?LinkID=196149)

<a id="Known_Issues"></a>

## <a name="new-features-changes-andknown-issues"></a>新功能、 更改 andKnown 问题

<a id="Known_Issues_Installation"></a>

### <a name="webmatrix-beta-3-installation"></a>WebMatrix Beta 3 安装

#### <a name="issue-webmatrix-beta-3-is-only-available-on-platforms-that-support-microsoft-net-framework-4"></a>问题：WebMatrix Beta 3 上才支持 Microsoft.NET Framework 4 的平台

> WebMatrix beta 版本需要.NET Framework 版本 4。 在某些情况下，WebMatrix beta 版安装程序会让您尝试安装不受支持的配置集的一部分的平台上。 具体而言，Windows Vista SP1 更新将允许您开始安装 WebMatrix beta 版，但.NET Framework 4 组件将失败并且阻止您的安装。
> 
> **解决方法**  
> 安装在受支持的平台，其中包括：
> 
> - Windows 7
> - Windows Server 2008
> - Windows Server 2008 R2
> - Windows Vista SP1 或更高版本
> - Windows XP SP3
> - Windows Server 2003 SP2

#### <a name="issue-cannot-install-webmatrix-beta-3-if-microsoft-visual-studio-2008-is-installed-without-microsoft-visual-studio-2008-sp1"></a>问题：如果没有 Microsoft Visual Studio 2008 SP1 的情况下安装 Microsoft Visual Studio 2008 不能安装 WebMatrix Beta 3

> **解决方法**  
> 安装[Microsoft Visual Studio 2008 SP1](https://www.microsoft.com/downloads/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en)从 Microsoft 下载中心获得。

#### <a name="issue-some-assemblies-for-sql-server-compact-40-are-not-installed-in-the-gac"></a>问题：SQL Server Compact 4.0 某些程序集未安装在 GAC 中

> 在 64 位计算机上安装 SQL Server Compact 4.0 和计算机具有仅.NET Framework 3.5 SP1 客户端安装了配置文件时，SQL Server Compact 4.0 的托管程序集不会放在全局程序集缓存 (GAC) 中。 未安装在 GAC 中的托管程序集是：
> 
> - *System.Data.SqlServerCe.dll* （ADO.NET 提供程序）
> - *System.Data.SqlServerCe.Entity.dll* （ADO.NET 实体框架）
> 
> **解决方法**  
> 卸载 SQL Server Compact 4.0。 下载并安装.NET Framework 3.5 SP1 的完整版本，从以下位置：  
>   
> [Microsoft.NET Framework 3.5 Service pack 1 （完整程序包）](https://go.microsoft.com/fwlink/?LinkId=194828)  
>   
> 然后重新安装 SQL Server Compact 4.0。

#### <a name="issue-cannot-uninstall-sql-server-compact-using-the-command-line"></a>问题：无法卸载 SQL Server Compact 使用命令行

> 卸载 SQL Server Compact 使用命令行选项不适用于此版本。
> 
> **解决方法**  
> 使用*程序和功能*Windows 控制面板卸载 Microsoft SQL Server Compact 4.0 中。

<a id="Known_Issues_ASPNET"></a>

### <a name="aspnet-web-pages"></a>ASP.NET 网页

文档的本节介绍新功能、 更改和使用 Razor 语法的 Beta 3 版本的 ASP.NET Web Pages 的已知的问题。

- [新增功能](#NewFeatures)
- [更改](#Changes)
- [问题](#Issues)

<a id="NewFeatures"></a>

#### <a name="new-features-in-beta-3-for-aspnet-web-pages-with-razor-syntax"></a>Beta 3 ASP.NET Web pages with Razor Syntax 中的新增功能

#### <a name="new-htmlraw-method-renders-unencoded-markup"></a>新增日期："Html.Raw"方法将呈现未编码的标记

> 新`Html.Raw`方法可呈现 HTML 标记作为标记而不是呈现编码的输出。 （默认情况下，ASP.NET Razor 将编码字符串呈现它们之前。）语法为：
> 
> `Html.Raw(value)`
> 
> 下面的示例演示如何使用 `Html.Raw`：
> 
> [!code-cshtml[Main](beta3/samples/sample1.cshtml)]

<a id="Changes"></a>

#### <a name="changes-in-beta-3-for-aspnet-web-pages-with-razor-syntax"></a>在 Beta 3 中 ASP.NET Web pages with Razor Syntax 的更改

#### <a name="change-hrefattribute-method-removed"></a>更改："HrefAttribute"方法已移除

> `HrefAttribute`方法的`WebPage`类已删除。 此帮助器用于对 Url 中的不安全字符进行编码。 它是不再需要，因为 ASP.NET Razor 自动对字符串进行编码。 (使用新`Html.Raw`方法以呈现未编码的字符串。)

#### <a name="change-syntax-for-declarative-helper-helpers-changed"></a>更改：语法声明性"@helper"更改帮助程序

> 在 Beta 3 版本中，ASP.NET 更改它将帮助程序，使用创建的解析`@helper`语法。 从本质上讲，`@helper`语法现在分析为一个代码块而不是作为一个的标记可以包含代码块。 因此，帮助器代码不需要用`@{ }`块。 相反，标记帮助器必须显式包含在 HTML 元素或 ASP.NET Razor`<text></text>`标记。
> 
> 例如，以下`@helper`语法适用于 Beta 3 版本：
> 
> [!code-cshtml[Main](beta3/samples/sample2.cshtml)]
> 
> 在 Beta 3 版本中，必须将此帮助器更改为如以下示例所示：
> 
> [!code-cshtml[Main](beta3/samples/sample3.cshtml)]
> 
> 请注意，`@{ }`不再使用的帮助程序中的初始代码周围的字符。 这是因为帮助程序的内容被视为默认情况下一个代码块。 帮助器将呈现标记，开始在打开`<a>`标记。 如果帮助者必须呈现的纯文本或标记，其中不包含结束标记 (例如，`<meta>`标记)，要呈现的内容必须在`<text></text>`标记。

#### <a name="change-webpagecontexthttpcontext-removed"></a>更改："WebPageContext.HttpContext"中删除

> `WebPageContext.HttpContext`删除属性。 请改用 `HttpContext.Current`。 (`WebPageContext.HttpContext`属性只是包装这。)

#### <a name="change-facebook-helper-moved-to-new-package"></a>更改："Facebook"帮助程序移动到新的包

> `Facebook`帮助器已移至*Facebook.Helper*库，其中包括`Facebook`帮助器和其他功能。 您必须安装此库作为单独的包，在"安装帮助程序使用程序包管理器"中所述在本教程[开始使用 ASP.NET 页面](https://go.microsoft.com/fwlink/?LinkId=202889)。

#### <a name="change-membership-role-and-security-types-moves-to-new-assembly"></a>更改：成员资格、 角色和安全类型移动到新的程序集

> 以下类型都已移动到`WebMatrix.WebData`程序集：
> 
> - `ExtendedMembershipProvider`
> - `SimpleMembershipProvider`
> - `SimpleRoleProvider`
> - `WebSecurity`

#### <a name="change-tagbuilder-class-moved-to-systemwebwebpagesdll-assembly"></a>更改：移动到 System.Web.WebPages.dll 程序集的"TagBuilder"类

> `TagBuilde` R 类已被移动到 System.Web.WebPages.dll 程序集。 以前，这是 ASP.NET MVC 的一部分的程序集中。 此更改意味着，不需要安装 ASP.NET MVC，以便使用`TagBuilder`类。
> 
> 但是，此类是仍在`System.Web.Mvc`命名空间。 若要使用`TagBuilder`类 （例如，在一个自定义 ASP.NET Razor 帮助器），必须引用的命名空间 (例如，通过添加`@using System.Web.Mvc`到你的代码)。

#### <a name="change-request-validation-syntax-changed-validation-class-removed"></a>更改：请求验证语法已发生更改;"验证"类中删除

> 在 Beta 3 版本中，若要禁用验证的一个单独的字段或一组字段，您可以调用`Validation.Exclude`方法，传入的名称或排除在验证之外的字段的名称。 跳过验证的 Beta 3 版本中提供了一种新语法。 `Validation` Beta 3 中使用的方法已删除。
> 
> > [!NOTE]
> > 如果用户尝试将 HTML 标记 （例如，通过在页面上使用富文本编辑器） 上传未禁用请求验证，如果网站将报告之类的错误*从客户端检测到潜在危险的Request.Form值*都不接受用户输入。 如果禁用请求验证，你必须手动检查用户输入，以确保它不包含具有潜在危险的标记或脚本使用类似[Microsoft 防跨站点脚本库 V4.0](https://www.microsoft.com/downloads/en/details.aspx?FamilyID=f4cd231b-7e06-445b-bec7-343e5884e651)。
> 
> 
> 若要禁用自动请求验证，请调用`Request.Unvalidated`方法，并向其传递该字段或你要绕过请求验证的其他文章对象的名称。 可以使用此方法以跳过验证对于中的任何项`Form`， `QueryString`， `Cookies`，和`ServerVariables`集合。 下面的示例演示如何使用`Unvalidated`方法：
> 
> [!code-csharp[Main](beta3/samples/sample4.cs)]

<a id="Issues"></a>

#### <a name="known-issues-for-aspnet-web-pages-with-razor-syntax"></a>ASP.NET Web Pages with Razor Syntax 的已知的问题

#### <a name="issue-unexpected-behavior-when-using-a-custom-user-table-for-membership"></a>问题：使用自定义用户表的成员身份时出现意外的行为

> 若要初始化 ASP.NET Razor 网站成员资格提供程序，请调用`WebSecurity.InitializeDatabaseConnection`方法。 (在 WebMatrix 中，入门网站模板包括对在此方法的调用 *\_AppStart.cshtml*文件。)如果`autoCreateTables`此方法的参数设置为 true (默认情况下它设置为 true 入门网站模板中)，并且如果一个无法识别的表名称传递给方法 （第二个参数），该方法不会引发错误。 相反，它会自动创建的表。
> 
> 如果你想要使用自定义用户表的成员身份，但将传递到的错误的表名称，这可能是问题`WebSecurity.InitializeDatabaseConnection`方法。 由于该方法不会默认情况下引发错误如果指定的表不存在，并且它改为创建一个新表，该应用程序可以似乎无法正常工作。 但是，依赖于自定义用户表 （和在其中的字段） 的应用程序代码可以最终失败并出现意外错误。
> 
> **解决方法**  
> 请确保名称传入`InitializeDatabaseConnection`方法匹配项的用户配置文件表中的成员资格数据库，或请确保`autoCreateTables`参数设置为 false。

#### <a name="issue-failed-to-generate-a-user-instance-of-sql-server-error"></a>问题："无法生成 SQL Server 的用户实例"错误

> 如果 WebMatrix Web 应用程序使用 SQL Server Express，并且在 Windows 7 或 Windows Server 2008 R2 上运行 IIS 7.5，你可能会看到一个错误，指示 SQL Server 不能在运行时检索用户的本地应用程序路径。
> 
> **解决方法**请确保应用程序 (通常为 NETWORK SERVICE) 下运行的 Windows 帐户，包含读/写权限的应用程序的根文件夹和子文件夹，例如*应用\_数据*. 知识库文章中提供了更多详细的信息[SQL Server Express 用户实例化和 ASP.net Web 应用程序项目的问题](https://support.microsoft.com/kb/2002980)。

#### <a name="issue-in-visual-studio-namespaces-for-custom-assemblies-dlls-are-not-imported-automatically"></a>问题：在 Visual Studio 中，自定义程序集 (Dll) 的命名空间不自动导入

> 如果在 Visual Studio 中的项目中使用自定义程序集，这些程序集中声明的命名空间将不自动导入在设计时。 因此，对自定义类型的引用可能无法在设计时识别并标记为不能识别 Visual Studio 中 （使用"波形曲线"）。 仅在设计时在 Visual Studio; 中出现此问题应用程序本身能够正常运行。
> 
> **解决方法**  
> 包括`using`语句 (`imports`在 Visual Basic 中)，它引用在设计时无法识别的实体。

#### <a name="issue-visual-studio-intellisense-and-project-templates-available-only-in-aspnet-mvc-version-3"></a>问题：Visual Studio IntelliSense 模板和项目模板仅在 ASP.NET MVC 版本 3 中可用

> 安装 ASP.NET Web Pages 不同时安装工具用于 Visual Studio 的 ASP.NET Web Pages 应用程序的智能感知和项目模板等。
> 
> **解决方法**若要使用 Visual Studio 中的 ASP.NET Web Pages 应用程序的智能感知和项目模板，ASP.NET MVC 3 RC 通过 Web 平台安装程序的安装或[独立安装程序](https://go.microsoft.com/fwlink/?LinkID=191797)。

#### <a name="issue-lthelpergt-class-cannot-be-found-error"></a>问题:"&lt;帮助器&gt;找不到类"错误

> 升级到 Beta 3 后，可能会看到错误的帮助器类 (例如，`Facebook`类) 不能找不到。 在 Beta 2 开始，一直在 Beta 3 中，帮助程序已被移到必须显式安装的包。 不升级现有的站点中包含这些包;这包括中的站点 *\My Documents\IISExpress* 或 *\My Documents\My 网站* 文件夹。 具体而言，您会看到此错误，如果使用中的默认站点*我的网站* (WebSite1)，其中包括对引用`Twitter`帮助器。
> 
> **解决方法**  
> 注释掉对运行的站点中任何帮助程序调用 *\_管理员* 页，并安装包或包含你想要使用的帮助器的包。 安装此包后，可以取消注释引用帮助程序的行。

#### <a name="issue-deploying-beta-3-aspnet-razor-assemblies-to-the-bin-folder-might-not-work-on-hosting-sites"></a>问题：Beta 3 ASP.NET Razor 程序集部署到 Bin 文件夹可能不适用于托管站点

> 如果将 ASP.NET Web Pages 网站部署到托管站点，并将 ASP.NET Razor Beta 3 程序集部署到的站点*Bin*文件夹中，你可能会遇到错误，包括以下：
> 
> `Could not load type 'Microsoft.Web.Infrastructure.DynamicModuleHelper.DynamicModuleUtility' from assembly 'Microsoft.Web.Infrastructure, Version=1.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35'.`
> 
> 如果宿主提供程序已安装到服务器的全局应用程序缓存 (GAC) 的 ASP.NET Web Pages Beta 1 程序集，则可能发生此问题。 程序集位于 gac 中本地安装的程序集通过获取优先*Bin*文件夹。
> 
> **解决方法**联系托管提供商，以确认你看到的错误是由于提供程序的版本之间发生冲突的程序集和你们的。 如果是这样，请求托管提供商更新服务器的 GAC 中的程序集。

#### <a name="issue-reading-feeds-or-other-external-data-via-a-proxy-server"></a>问题：读取源或其他外部数据通过代理服务器

> 如果运行该站点的服务器位于代理服务器后面，可能需要配置中的代理信息*Web.config*以便能够读取来自你的站点之外的信息的文件。 例如，如果您使用`ReCaptcha`帮助器，帮助者与 reCAPTCHA 服务通信，但可能无法通过代理服务器。 同样，使用 ASP.NET Web Pages 中，如包管理器，使用源的馈送可能需要代理服务器配置。
> 
> 如果使用外部服务或使用包源中的问题，将以下元素放入应用程序的根*Web.config*文件：
> 
> [!code-xml[Main](beta3/samples/sample5.xml)]
> 
> 有关配置代理服务器的详细信息，请参阅[&lt;代理&gt;元素 （网络设置）](https://msdn.microsoft.com/library/sa91de1e.aspx) MSDN 网站上。

#### <a name="issue-microsoftwebinfrastructuredll-cannot-be-loaded-error"></a>问题："无法加载 Microsoft.Web.Infrastructure.dll"错误

> 如果您以前安装的 Beta 1 版本的 ASP.NET Web Pages 使用 Razor 语法，然后再安装 Beta 3 版本，所有适当的程序集安装在 gac 中除*Microsoft.Web.Infrastructure.dll*。 因此，在运行 ASP.NET Razor 页时，您看到错误，指示*Microsoft.Web.Infrastructure.dll*无法加载。
> 
> 如果加载的干净计算机上的 Beta 3 版本不会出现此问题。
> 
> **解决方法**  
> 在控制面板中，卸载 ASP.NET Web Pages。 然后重新安装 Beta 3 版本。

#### <a name="issue-uninstalling-the-net-framework-version-4-disables-aspnet-web-pages-with-razor-syntax"></a>问题：卸载.NET Framework 版本 4 禁用使用 Razor 语法的 ASP.NET Web Pages

> 如果卸载.NET Framework 版本 4，然后重新安装它，则禁用使用 Razor 语法的 ASP.NET Web Pages。 与页 *.cshtml*扩展不能正确运行。 ASP.NET 网页机根目录中注册程序集*Web.config*文件，并删除.NET Framework 中删除该文件。 重新安装.NET Framework 安装的配置文件的新版本，但不会将引用添加 ASP.NET Web Pages 的程序集。
> 
> **解决方法**后重新安装.NET Framework，请重新安装 ASP.NET Web Pages 使用 Razor 语法。 这将添加到下面的元素*Web.config*机根目录，这通常是在以下位置中的文件：  
> 
> `C:\Windows\Microsoft.NET\Framework\v4.0.30319\Config (32-bit)`  
> 
> `C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config (64-bit)`
> 
> [!code-xml[Main](beta3/samples/sample6.xml)]

#### <a name="issue-applications-previously-deployed-with-aspnet-assemblies-in-the-bin-folder-experience-errors"></a>问题：使用 ASP.NET 的 Bin 文件夹中的程序集之前部署的应用程序遇到错误

> 在部署期间，ASP.NET Web Pages 程序集的副本 (例如， *Microsoft.WebPages.dll*) 到*Bin*的服务器上的网站的文件夹。 (可能在部署期间自动发生这或者是因为开发人员显式复制程序集。)但是，当安装 Beta 3 版本，则错误时，如找不到某些类型的错误。 这是因为多个 ASP.NET Web Pages 类型移动到不同的命名空间对于 Beta 3 版本。
> 
> **解决方法**   
> 清除*Bin*文件夹部署的应用程序的新程序集复制到的文件夹 （或重新部署应用程序），然后重新启动该应用程序。

#### <a name="issue-extensionless-urls-do-not-find-cshtmlvbhtml-files-on-iis-7-or-iis-75"></a>问题：无扩展名 Url 找不到在 IIS 7 或 IIS 7.5 上的.cshtml/.vbhtml 文件

> 在 IIS 7 或 IIS 7.5 上，使用类似于以下 URL 的请求不能将查找具有的页 *.cshtml*或 *.vbhtml*扩展：  
> 
> `http://www.example.com/ExampleSite/ExampleFile`  
> 
> 由于 URL 重写未启用默认情况下为 IIS 7 或 IIS 7.5，则会产生问题。 很可能方案是使用本地 IIS Express，测试时未看到该问题，但在你的网站部署到托管网站时遇到。
> 
> **解决方法**
> 
> - 如果你可以控制在服务器计算机，在服务器计算机上安装的更新中所述[更新可启用某些 IIS 7.0 或 IIS 7.5 处理程序来处理请求的 Url 不以句点结尾](https://support.microsoft.com/kb/980368)。
> - 如果您没有对服务器计算机的控制 （例如，要部署到托管的网站），将以下代码添加到该网站*Web.config*文件：
> 
> 
> [!code-xml[Main](beta3/samples/sample7.xml)]

#### <a name="issue-using-web-application-project-or-aspnet-mvc-and-aspnet-web-pages-in-the-same-application"></a>问题：在同一个应用程序中使用 Web 应用程序项目或 ASP.NET MVC 和 ASP.NET 网页

> 如果在 Web 应用程序项目或 ASP.NET MVC 应用程序中使用的 ASP.NET Web Pages，可能会看到错误， *WebPageHttpApplication*找不到。
> 
> **解决方法**  
> 如果收到此错误，将更改应用程序所派生的基类。 在中*Global.asax*文件中，将以下行：
> 
> [!code-csharp[Main](beta3/samples/sample8.cs)]
> 
> 更改为：
> 
> [!code-csharp[Main](beta3/samples/sample9.cs)]
> 
> 这实际上会反转更改引入了使用 Razor 语法的 Beta 1 版本的 ASP.NET Web Pages。

#### <a name="issue-deploying-an-application-to-a-computer-that-does-not-have-sql-server-compact-installed"></a>问题：应用程序部署到不具有 SQL Server Compact 安装的计算机

> SQL Server Compact 未安装在计算机上可以运行包含 SQL Server Compact 数据库的应用程序。 Microsoft WebMatrix Beta 3 中自动将这些二进制文件复制，并执行适当*Web.config*文件转换。
> 
> **解决方法**如果你需要将这些文件复制并使*Web.config*文件更改手动，执行以下操作：
> 
> 1. 将复制到的数据库引擎程序集*Bin*目标计算机上的应用程序文件夹 （和子文件夹）： 
> 
>     - Copy *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Desktop\System.Data.SqlServerCe.dll* **to** *\Bin*
>     - 复制*C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\x86\\** **到** *\Bin\x86*
>     - 复制*C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\amd64\\** **到** *\Bin\amd64*
> 2. 在该网站的根文件夹中创建或打开*Web.config*文件。 (此文件类型是在 WebMatrix Beta 3 中，单击**所有**中**选择文件类型**对话框。)
> 3. 将以下元素添加为的子 **&lt;配置&gt;** 元素 (而不是在 **&lt;system.web&gt;** 元素):
> 
> 
> [!code-xml[Main](beta3/samples/sample10.xml)]

#### <a name="issue-database-and-webgrid-helpers-do-not-work-in-medium-trust-in-visual-basic"></a>问题：数据库和 WebGrid 帮助器在中等信任在 Visual Basic 中不起作用

> 如果使用的 Visual Basic (创建 *.vbhtml*文件)，则`Database`和`WebGrid`如果应用程序设置为使用中等信任级别，帮助程序将无法工作。
> 
> **解决方法**  
> 暂时将设置应用程序以使用完全信任。

<a id="Known_Issues_SQL_Server_Compact"></a>
### <a name="sql-server-compact"></a>SQL Server Compact

#### <a name="issue-encrypt-property-is-not-recognized"></a>问题：无法识别"加密"属性

> SQL Server Compact 4.0 不能识别`Encrypt`属性的`SqlCeConnection`类。 不应使用此属性来加密数据库文件。 `Encrypt`属性在 SQL Server Compact 3.5 版本中已弃用，并且仅为向后兼容性保留了。 
> 
> **解决方法**  
> 使用`Encryption Mode`属性的`SqlCeConnection`类来加密 SQL Server Compact 4.0 数据库文件。 下面的示例演示如何创建加密的 SQL Server Compact 4.0 数据库使用`Encryption Mode`属性：
> 
> [!code-csharp[Main](beta3/samples/sample11.cs)]
> 
> [!code-vb[Main](beta3/samples/sample12.vb)]
> 
> 若要更改现有的 SQL Server Compact 4.0 数据库的加密模式，请执行以下操作：
> 
> [!code-csharp[Main](beta3/samples/sample13.cs)]
> 
> [!code-vb[Main](beta3/samples/sample14.vb)]
> 
> 若要加密的未加密的 SQL Server Compact 4.0 数据库，执行以下操作：
> 
> [!code-csharp[Main](beta3/samples/sample15.cs)]
> 
> [!code-vb[Main](beta3/samples/sample16.vb)]

#### <a name="issue-microsoft-visual-c-2008-runtime-libraries-are-required"></a>问题：Microsoft Visual C++ 2008年运行时库是必需的

> 本机 Dll 的 SQL Server Compact 4.0 需要 Microsoft Visual C++ 2008年运行时库 （x86、 IA64 和 x64）、 Service Pack 1。
> 
> **解决方法**  
> 安装.NET Framework 3.5 SP1。 这还会安装该视觉对象C++2008 运行时库 SP1。 可以从以下位置下载库：   
>   
> [Microsoft Visual C++ 2008 Service Pack 1 可再发行组件包 ATL 安全更新](https://go.microsoft.com/fwlink/?LinkId=194827)
> 
> [!NOTE]
> 请注意，安装.NET Framework 2.0，3.0，或 4*不*安装视觉对象C++2008 运行时库 SP1。

#### <a name="issue-if-sql-server-compact-is-installed-prior-to-installing-net-framework-on-the-computer-its-provider-invariant-name-is-not-registered-in-the-net-framework-machineconfig-file"></a>问题：如果 SQL Server Compact 安装的计算机上安装.NET Framework 之前，其提供程序固定名称未注册.NET Framework machine.config 文件中

> SQL Server Compact 可以安装在未安装.NET Framework 安装，因为 SQL Server Compact 确实需要.NET framework 的计算机上。 如果既没有.NET Framework 版本 3.5 和 4 安装在安装 SQL Server Compact 之前，SQL Server Compact 安装程序不会注册在其提供程序固定名称*machine.config*文件。 任何应用程序都依赖于中的 SQL Server Compact 条目*machine.config*文件将会失败。 中的固定名称注册条目*machine.config*如以下示例所示：
> 
> [!code-xml[Main](beta3/samples/sample17.xml)]
> 
> **解决方法**  
> 卸载 SQL Server Compact 4.0 CTP1。 下载并安装.NET Framework 的完整版本，从以下位置：
> 
> [Microsoft.NET Framework 3.5 Service pack 1 （完整程序包）](https://go.microsoft.com/fwlink/?LinkId=194828)  
> [Microsoft.NET Framework 4.0 版本 （完整程序包）](https://www.microsoft.com/downloads/details.aspx?FamilyID=9cfb2d51-5ff4-4491-b0e5-b386f32c0992&amp;displaylang=en)
> 
> 然后重新安装[SQL Server Compact 4.0 CTP1](https://www.microsoft.com/downloads/details.aspx?FamilyID=0d2357ea-324f-46fd-88fc-7364c80e4fdb&amp;displaylang=en)。

<a id="Known_Issues_Installing_Applications"></a>

### <a name="installing-applications"></a>安装应用程序

#### <a name="issue-installing-an-application-can-take-a-long-time-if-the-users-my-documents-folder-is-redirected-to-a-network-share"></a>问题：安装应用程序可能需要很长时间，如果用户的 My Documents 文件夹重定向到网络共享

> **解决方法**  
> 无。 应用程序可能需要一段时间才能安装，但将正确安装。

<a id="Known_Issues_Publishing_Applications"></a>

### <a name="publishing-applications"></a>发布应用程序

#### <a name="issue-site-might-not-work-after-publishing-if-the-destination-url-field-is-not-prefixed-with-http-or-https"></a>问题：如果将"目标 URL"字段不 http:// 或 https:// 开头的前缀发布后，站点可能无法工作

> 在中**发布设置**对话框中，如果目标 URL 不以开头`http://`或`https://`，部署后，该站点可能无法工作。
> 
> **解决方法**  
> 请确保在发布的站点中的目标 URL 前**发布设置**对话框的开头`http://`或`https://`。

#### <a name="issue-publishing-a-mysql-database-fails-with-the-error-failed-to-publish-the-database-this-can-happen-if-the-remote-database-cannot-run-the-script"></a>问题：发布的 MySQL 数据库将失败并出现错误"无法将数据库发布。 这可以是远程数据库不能运行脚本。"

> 多种原因可能出现此错误。 可以看到此错误的原因之一是，如果数据库脚本中包含单引号字符 （'），并且目标 MySQL 数据库的默认字符集为 utf-8。
> 
> **解决方法**  
> 设置为远程的 MySQL 数据库设置为 utf-8 的默认字符。

<a id="Known_Issues_Other_Issues"></a>

### <a name="other-issues"></a>其他问题

#### <a name="issue-searchfilter-does-not-work-in-reports-for-group-by-issue-type"></a>问题：搜索/筛选器不适合在报表中分组依据：问题类型

> 当运行网站的报告，如果输入中的文本*按 URL 筛选*框，然后单击*搜索*，没有任何反应。 这是因为此控件不起作用时*Group By*报表的状态设置为*问题类型*，这是默认设置。
> 
> **解决方法**中*分组依据*选项卡的功能区中，单击*URL*进行分组的项按其源 URL。 文本框和按钮，用于筛选条目都能运行时处于此状态。

#### <a name="issue-wcf-applications-fail-to-run-with-iis-express"></a>问题：WCF 应用程序无法使用 IIS Express 运行

> 浏览到 WCF 应用程序会导致类似于以下错误：
> 
> *无法加载文件或程序集 Microsoft.Web.Administration，版本 = 7.0.0.0，区域性 = 中性，PublicKeyToken = 31bf3856ad364e35 或其某个依赖项。系统找不到指定的文件。*
> 
> 发生这种情况是因为默认情况下，IIS Express 的 Beta 版本不支持 WCF。
> 
> **解决方法**使用下列解决方法之一 (解决方法 2 要求 Microsoft Windows Vista 或更高版本):
> 
> 
> 1. 复制*Microsoft.Web.dll*并*Microsoft.Web.Administration.dll*到 WebMatrix 安装位置中的程序集*bin* WCF 的目录应用程序。 默认情况下，在安装 WebMatrix *Microsoft WebMatrix*系统的下的子文件夹*Program Files*文件夹。
> 2. Microsoft Windows Vista 或更高版本，创建中的程序集的符号链接*bin*目录中使用以下命令。 （这种方法的优点它不会创建一份程序集。）
> 
>     [!code-console[Main](beta3/samples/sample18.cmd)]
> 3. 在 GAC 中安装两个程序集。 从提升的提示符下运行以下命令：
> 
>     [!code-console[Main](beta3/samples/sample19.cmd)]

#### <a name="issue-webmatrix-beta-3-is-unable-to-perform-certain-tasks-that-require-elevation"></a>问题：WebMatrix Beta 3 不能执行某些任务需要提升

> WebMatrix Beta 3 不能执行某些任务需要提升，例如，在以下情况下安装其他组件：
> 
> - 在 Windows Vista 或 Windows 7 中，使用不具有管理权限的帐户登录并禁用用户帐户控制 (UAC)。
> - 使用 Microsoft Windows XP 或 Microsoft Windows Server 2003。
> 
> **解决方法**  
> 在 WebMatrix Beta 3 中的大多数任务不需要管理权限。 对于那些确实可以执行的操作以管理员身份，或请执行以下步骤：
> 
> - 在 Windows Vista 或 Windows 7，启用 UAC。
> - 在 Windows XP 中，将用户添加到管理员安全组。

#### <a name="issue-site-from-web-gallery-is-disabled"></a>问题："从 Web 库创建网站"已禁用

> **站点从 Web 库**如果未安装 Web 平台安装程序 3.0 选项被禁用。
> 
> **解决方法**  
> 安装[Microsoft Web 平台安装程序 3.0](https://go.microsoft.com/fwlink/?LinkID=194638)。

#### <a name="issue-on-windows-server-2003-iis-express-does-not-start-for-a-non-administrative-user"></a>问题：在 Windows Server 2003、 IIS Express 不会启动非管理用户

> Windows Server 2003 上启动的页或启动 IIS Express，IIS Express 不会启动。 对于 Web 页面，错误将显示，指示某个非管理用户，启动该应用程序。
> 
> **解决方法**  
> 启动 WebMatrix Beta 3 作为管理用户。 有关更多详细信息，请参阅以下知识库文章：  
>   
> [由非管理用户启动的应用程序无法侦听到 Windows Vista、 Windows Server 2003 或 Windows XP 中运行应用程序的计算机的 HTTP 流量。](https://support.microsoft.com/kb/939786)

#### <a name="issue-google-chrome-is-not-available-as-a-run-option"></a>问题：Google Chrome 不可用作运行选项

> 在浏览器的列表中不显示 Google Chrome**运行**上**主页**选项卡。
> 
> **解决方法**  
> 某些版本的 Google Chrome 并不能注册正确地与 Windows 中的默认程序功能。 解决此问题，启动 Google Chrome 中，单击*自定义和控制 Google Chrome*菜单上，单击*选项*，然后单击*使 Google Chrome 我的默认浏览器*。

#### <a name="issue-the-foreign-key-dialog-box-doesnt-allow-entering-a-primary-key"></a>问题："外键"对话框中不允许输入主键

> **外键**对话框不允许您输入从主键表的主键名称。
> 
> **解决方法**  
> 这是有意为之。 不需要输入主键表的主键的名称。

#### <a name="issue-the-relationships-button-is-disabled"></a>问题："关系"按钮处于禁用状态

> **关系**按钮下**表**选项卡中**数据库**禁用 SQL Server Compact 数据库的工作区。
> 
> **解决方法**  
> 无。 SQL Server Compact 不支持表之间的关系。

#### <a name="issue-parameterized-sql-queries-throw-exceptions"></a>问题：参数化的 SQL 查询引发异常

> 在 SQL Server Compact 4.0 中，如果不会如指定的数据类型`SqlDbType`或`DbType`对于参数化查询中的参数，在查询运行时引发异常。
> 
> **解决方法**  
> 显式设置参数的数据类型，如`SqlDbType`或`DbType`。 这是关键的 BLOB 数据类型 (`image`和`ntext`)。 使用如下所示的代码：
> 
> [!code-sql[Main](beta3/samples/sample20.sql)]
> 
> [!code-vb[Main](beta3/samples/sample21.vb)]

<a id="More_Info"></a>

## <a name="for-more-information"></a>更多信息

有关 WebMatrix Beta 3 的详细信息，请参阅以下网站：

- [IIS.net](http://iis.net/)
- [ASP.NET 2.0](https://asp.net/webmatrix)
- [Microsoft.com/web](https://www.microsoft.com/web)

---

© 2010 Microsoft Corporation. 保留所有权利。 [使用条款](https://msdn.microsoft.cos/cc300389.aspx)。

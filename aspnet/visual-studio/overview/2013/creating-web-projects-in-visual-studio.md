---
uid: visual-studio/overview/2013/creating-web-projects-in-visual-studio
title: 在 Visual Studio 2013 中创建 ASP.NET Web 项目 |Microsoft Docs
author: tdykstra
description: 本主题介绍用于在 Visual Studio 2013 中创建 ASP.NET web 项目的选项。在 Update 3 中，这里是一些用于 web 开发的新功能 c .。。
ms.author: riande
ms.date: 12/01/2014
ms.assetid: 61941e64-0c0d-4996-9270-cb8ccfd0cabc
msc.legacyurl: /visual-studio/overview/2013/creating-web-projects-in-visual-studio
msc.type: authoredcontent
ms.openlocfilehash: fbb4cd7afa2506879d47bce980bf0164aad40c2c
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345476"
---
# <a name="creating-aspnet-web-projects-in-visual-studio-2013"></a>在 Visual Studio 2013 中创建 ASP.NET Web 项目

作者： [Tom Dykstra](https://github.com/tdykstra)

> 本主题介绍用于在 Update 3 Visual Studio 2013 中创建 ASP.NET web 项目的选项
> 
> 下面是与 Visual Studio 早期版本相比，web 开发的一些新功能：
> 
> - 用于创建项目的简单 UI，该 UI (Web 窗体、MVC 和 Web API) 提供 [对多个 ASP.NET 框架的支持](#add) 。
> - [ASP.NET Identity](#indauth)，这是一个新的 ASP.NET 成员资格系统，该系统在所有 ASP.NET 框架中运行相同的功能，并且适用于除 IIS 之外的 web 托管软件。
> - 使用 [启动](#bootstrap) 来提供响应式设计和主题功能。
> - Web 窗体的新功能，仅用于 MVC，如 [自动测试项目创建](#testproj) 和 [Intranet 站点模板](#winauth)。
> 
> 有关如何为 Azure 云服务或 Azure 移动服务创建 web 项目的信息，请参阅 [Azure 云服务和 ASP.NET 入门](https://azure.microsoft.com/documentation/articles/cloud-services-dotnet-get-started/) 和 [使用 azure 移动服务 .Net 后端创建排行榜应用程序](https://azure.microsoft.com/documentation/articles/mobile-services-dotnet-backend-windows-store-dotnet-leaderboard/)。

<a id="prerequisites"></a>
## <a name="prerequisites"></a>必备条件

本文适用于安装了[Update 3](https://go.microsoft.com/fwlink/?linkid=397827&amp;clcid=0x409)的[Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566) 。

<a id="wap"></a>
## <a name="web-application-projects-versus-web-site-projects"></a>Web 应用程序项目与网站项目

ASP.NET 提供了两种 web 项目之间的选择： *web 应用程序项目* 和 *网站项目*。 建议用于新开发的 web 应用程序项目，本文仅适用于 web 应用程序项目。 有关详细信息，请参阅 MSDN 网站上的 [Web 应用程序项目与 Visual Studio 中](https://msdn.microsoft.com/library/dd547590(v=vs.120).aspx) 的网站项目。

<a id="overview"></a>
## <a name="overview-of-web-application-project-creation"></a>Web 应用程序项目创建概述

以下步骤演示如何创建 web 项目：

1. 单击**起始**页或 "**文件**" 菜单中的 "**新建项目**"。
2. 在 " **新建项目** " 对话框的左窗格中，单击 " **web** "，并在中间窗格中单击 " **ASP.NET web 应用程序** "。

    ![“新建项目”对话框](creating-web-projects-in-visual-studio/_static/image1.png)

    可以在左窗格中选择 " **云** "，创建 [azure 云服务](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy)、 [Azure 移动服务](https://msdn.microsoft.com/library/windows/apps/dn629482.aspx)或 [azure WebJob](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-webjobs)。 本主题不涵盖这些模板。
3. 如果需要应用程序的运行状况监视和使用情况监视，请在右窗格中单击 " **将 Application Insights 添加到项目** " 复选框。 有关详细信息，请参阅[在 Web 应用程序中监视性能](https://azure.microsoft.com/documentation/articles/app-insights-web-monitor-performance/)。
4. 指定项目 **名称**、 **位置**和其他选项，然后单击 **"确定"**。

    此时将出现 **“新建 ASP.NET 项目”** 对话框。

    ![“新建项目”对话框](creating-web-projects-in-visual-studio/_static/image2.png)
5. 单击模板。

    ![选择模板](creating-web-projects-in-visual-studio/_static/image3.png)
6. 如果要添加对模板中未包含的其他框架的支持，请单击相应的复选框。  (显示的示例中，可以将 MVC 和/或 Web API 添加到 Web 窗体项目中。 ) 

    ![添加框架](creating-web-projects-in-visual-studio/_static/image4.png)
7. <a id="testproj"></a>如果要添加单元测试项目，请单击 " **添加单元测试**"。

    ![添加单元测试](creating-web-projects-in-visual-studio/_static/image5.png)
8. 如果希望默认情况下使用模板提供的不同身份验证方法，请单击 " **更改身份验证**"。

    ![配置身份验证按钮](creating-web-projects-in-visual-studio/_static/image6.png)

    ![配置身份验证对话框](creating-web-projects-in-visual-studio/_static/image7.png)

<a id="azurenewproj"></a>
### <a name="create-a-web-app-or-virtual-machine-in-azure"></a>在 Azure 中创建 web 应用或虚拟机

Visual Studio 提供的功能可让你轻松地使用 Azure 服务来托管 web 应用程序。 例如，你可以从 Visual Studio IDE 执行以下所有操作：

- 创建和管理 web 应用或虚拟机，使你的应用程序可通过 Internet 使用。
- 查看应用程序在云中运行时创建的日志。
- 当应用程序在云中运行时，在调试模式下远程运行。
- 查看和管理其他 Azure 服务（如 SQL 数据库）。

你可以 [创建一个 Azure 帐户](https://www.windowsazure.com/pricing/free-trial/) ，其中包含免费的基本服务（如 web 应用），如果你是 MSDN 订户，则可以激活可向你提供额外 Azure 服务的每月信用额度的 [权益](https://azure.microsoft.com/pricing/member-offers/visual-studio-subscriptions/) 。 

默认情况下，" **新建 ASP.NET 项目** " 对话框允许您为新的 web 项目创建 web 应用程序或虚拟机。 如果不想创建新的 web 应用或虚拟机，请清除 " **在云中托管** " 复选框。

![创建远程资源](creating-web-projects-in-visual-studio/_static/image8.png)

复选框标题可能是 **云中的主机** 或 **创建远程资源**，这两种情况下的结果都是相同的。 如果选中该复选框，则默认情况下，Visual Studio 会在 Azure App Service 中创建一个 web 应用。 如果愿意，可以使用下拉框将其更改为 **虚拟机** 。 如果尚未登录到 Azure，系统会提示输入 Azure 凭据。 登录后，你可以使用一个对话框来配置 Visual Studio 将为你的项目创建的资源。 下图显示了 web 应用的对话框;如果你选择创建虚拟机，将显示不同的选项。

![配置 Azure 应用设置](creating-web-projects-in-visual-studio/_static/image9.png)

有关如何使用此过程创建 Azure 资源的详细信息，请参阅 [azure 和 ASP.NET 入门](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet) 和 [使用 Visual Studio 创建网站的虚拟机](https://azure.microsoft.com/documentation/articles/virtual-machines-dotnet-create-visual-studio-powershell/)。

本文的其余部分提供了有关可用模板及其选项的详细信息。 本文还介绍了如何在模板中使用的 "启动"、"布局" 和 "主题" 框架。

<a id="vs2013"></a>
## <a name="visual-studio-2013-web-project-templates"></a>Visual Studio 2013 Web 项目模板

Visual Studio 使用模板创建 web 项目。 项目模板可以创建新项目中的文件和文件夹，安装 NuGet 包，并为基本工作应用程序提供示例代码。 模板实现最新的 web 标准，旨在演示如何使用 ASP.NET 技术的最佳实践，并提供创建自己的应用程序的快速入门。

Visual Studio 2013 为面向 .NET 4.5 或更高版本的 .NET framework 的项目提供以下 web 项目模板选项：

- [空模板](#empty)
- [Web 窗体模板](#wf)
- [MVC 模板](#mvc)
- [Web API 模板](#webapi)
- [单页应用程序模板](#spa)
- [Azure 移动服务模板](https://azure.microsoft.com/documentation/articles/mobile-services-dotnet-backend-windows-store-dotnet-leaderboard/)
- [Visual Studio 2012 模板](#vs2012)

还可以安装提供 [Facebook 模板](#facebook)的 Visual Studio 扩展。

有关如何创建面向 .NET 4 的项目的信息，请参阅本主题后面的 [Visual Studio 2012 模板](#vs2012) 。

有关如何为移动客户端创建 ASP.NET 应用程序的信息，请参阅 [ASP.NET 中的移动支持](../../../mobile/overview.md)。

<a id="empty"></a>
### <a name="empty-template"></a>空模板

空模板提供 ASP.NET web 应用的最小文件夹和文件，例如 (*.csproj* 或的项目文件。*.vbproj*) 和 *Web.config* 文件。 通过使用 " **添加文件夹" 和 "核心引用：** 标签" 下的复选框，可以添加对 Web 窗体、MVC 和/或 web API 的支持。

对于空模板，无可用的身份验证选项。 身份验证功能在示例应用程序中实现，空模板不创建示例应用程序。

<a id="wf"></a>
### <a name="web-forms-template"></a>Web 窗体模板

Web 窗体框架提供了以下功能，使你能够快速构建丰富的 UI 和数据访问功能的网站：

- Visual Studio 中的 WYSIWYG 设计器。
- 呈现 HTML 和可以通过设置属性和样式进行自定义的服务器控件。
- 用于数据访问和数据显示的丰富控件分类。
- 公开事件的事件模型，你可以像处理 WPF 这样的方式对客户端应用程序进行编程。
- 自动保留状态 (HTTP 请求之间的数据) 。

通常，创建 Web 窗体应用程序所需的编程工作量比使用 ASP.NET MVC 框架创建相同的应用程序更少。 不过，Web 窗体不仅仅用于开发应用程序。 Web 窗体上构建了很多复杂的商业应用程序和框架。

由于 Web 窗体页和页上的控件自动生成许多发送到浏览器的标记，因此您不能对 ASP.NET MVC 提供的 HTML 进行精细的控制。 用于配置页和控件的声明性模型最大程度地减少了您必须编写的代码量，但隐藏了 HTML 和 HTTP 的某些行为。 例如，并不总是能够准确指定控件可能生成的标记。

Web 窗体框架本身并不能作为 ASP.NET 的 MVC 到基于模式的开发实践，如 [测试驱动开发](http://en.wikipedia.org/wiki/Test-driven_development)、 [问题分离](http://en.wikipedia.org/wiki/Separation_of_concerns)、 [控制反转](http://en.wikipedia.org/wiki/Inversion_of_control)和 [依赖关系注入](http://en.wikipedia.org/wiki/Dependency_injection)。 如果要以这种方式编写代码，可以：它不像在 ASP.NET MVC 框架中那样自动。 [ASP.NET Web 窗体 MVP](http://webformsmvp.com/)项目显示了一种方法，该方法有助于分离关注点和可测试性，同时保持 Web 窗体的快速开发交付。 Microsoft SharePoint 基于 Web 窗体 MVP 构建。

Web 窗体模板创建一个示例 Web 窗体应用程序，该应用程序使用 [启动](#bootstrap) 来提供响应式设计和主题功能。 下图显示了主页。

![Web 窗体模板应用主页](creating-web-projects-in-visual-studio/_static/image10.png)

有关 Web 窗体的详细信息，请参阅 [ASP.NET Web forms](https://asp.net/web-forms)。 有关 Web 窗体模板的作用的信息，请参阅 [使用 Visual Studio 2013 构建基本 Web 窗体应用程序](https://blogs.msdn.com/b/webdev/archive/2013/12/19/building-a-basic-web-forms-application-using-visual-studio-2013.aspx)。

<a id="mvc"></a>
### <a name="mvc-template"></a>MVC 模板

ASP.NET MVC 旨在促进基于模式的开发实践，例如 [测试驱动的开发](http://en.wikipedia.org/wiki/Test-driven_development)、 [问题分离](http://en.wikipedia.org/wiki/Separation_of_concerns)、 [控制反转](http://en.wikipedia.org/wiki/Inversion_of_control)和 [依赖关系注入](http://en.wikipedia.org/wiki/Dependency_injection)。 该框架鼓励 web 应用程序的业务逻辑层与其表示层之间分离。 通过将应用程序划分为 (M) 的模型、视图 (V) 和控制器 (C) ，ASP.NET MVC 可以更轻松地管理更大应用程序的复杂性。

借助 ASP.NET MVC，你可以比在 Web 窗体中更直接地使用 HTML 和 HTTP。 例如，Web 窗体可以自动保留 HTTP 请求之间的状态，但必须在 MVC 中显式编写代码。 MVC 模型的优点是，您可以完全控制您的应用程序正在执行的操作以及它在 web 环境中的行为方式。 缺点是必须编写更多的代码。

MVC 设计为可扩展，使 power 开发人员能够根据应用程序需要自定义框架。 此外，ASP.NET MVC 源代码可从 OSI 许可证获取。

MVC 模板创建一个示例 MVC 5 应用程序，该应用程序使用 [启动](#bootstrap) 来提供响应式设计和主题功能。 下图显示了主页。

![MVC 示例应用程序](creating-web-projects-in-visual-studio/_static/image11.png)

有关 MVC 的详细信息，请参阅 [ASP.NET MVC](https://asp.net/mvc)。 有关如何选择 MVC 4 模板的信息，请参阅本文后面的 [Visual Studio 2012 模板](#vs2012) 。

<a id="webapi"></a>
### <a name="web-api-template"></a>Web API 模板

Web API 模板基于 Web API 创建一个示例 web 服务，其中包括基于 MVC 的 API 帮助页。

ASP.NET Web API 是一种框架，用于轻松构建可以访问多种客户端（包括浏览器和移动设备）的 HTTP 服务。 ASP.NET Web API 是用于在 .NET Framework 上生成 RESTful 服务的理想平台。

Web API 模板创建了一个示例 Web 服务。 下图显示了示例帮助页。

![Web API 帮助页](creating-web-projects-in-visual-studio/_static/image12.png)

![获取 API 的 Web API 帮助页](creating-web-projects-in-visual-studio/_static/image13.png)

有关 Web API 的详细信息，请参阅 [ASP.NET Web API](https://asp.net/web-api)。

<a id="spa"></a>
### <a name="single-page-application-template"></a>Single Page Application Template（单页应用程序模板）

单页面应用程序 (SPA) 模板会创建一个在客户端上使用 JavaScript、HTML 5 和 [KnockoutJS](http://knockoutjs.com/) 的示例应用程序，并 ASP.NET Web API 服务器上。

SPA 模板的唯一身份验证选项是 [单独的用户帐户](#indauth)。

下图显示了 SPA 模板生成的示例应用程序的初始状态。

![SPA 示例应用程序](creating-web-projects-in-visual-studio/_static/image14.png)

有关如何使用 SPA 模板创建应用程序的信息，请参阅 [WEB API-外部身份验证服务](../../../web-api/overview/security/external-authentication-services.md)。

有关 ASP.NET 单页面应用程序的详细信息，以及有关使用 KnockoutJS 以外的 JavaScript 框架的其他 SPA 模板的详细信息，请参阅以下资源：

- [ASP.NET 单页面应用程序](../../../single-page-application/index.md)。
- [了解适用于 VS2013 RC 的 SPA 模板中的安全功能](https://blogs.msdn.com/b/webdev/archive/2013/09/20/understanding-security-features-in-spa-template.aspx)
- [单页应用程序：通过 ASP.NET 生成新式的响应式 Web 应用](https://msdn.microsoft.com/magazine/dn463786.aspx)

<a id="facebook"></a>
### <a name="facebook-template"></a>Facebook 模板

可以安装 [提供 Facebook 模板的 Visual Studio 扩展](https://go.microsoft.com/fwlink/?LinkID=509965&amp;clcid=0x409)。 此模板创建一个设计为在 Facebook 网站内运行的示例应用程序。 它基于 ASP.NET MVC，并使用 Web API 来进行实时更新。

Facebook 模板不能使用任何身份验证选项，因为 Facebook 应用程序在 Facebook 站点内运行，并依赖 Facebook 的身份验证。

有关 ASP.NET Facebook 应用程序的详细信息，请参阅 [更新 MVC FACEBOOK API](https://blogs.msdn.com/b/webdev/archive/2014/06/10/updating-the-mvc-facebook-api.aspx)。

<a id="vs2012"></a>
### <a name="visual-studio-2012-templates"></a>Visual Studio 2012 模板

Visual Studio 2013 web 项目创建对话框不提供对 Visual Studio 2012 中提供的某些模板的访问权限。 如果要使用这些模板之一，可以在 Visual Studio 的 "新建项目" 对话框的左窗格中单击 "Visual Studio 2012" 节点。

![Visual Studio 2012 模板](creating-web-projects-in-visual-studio/_static/image15.png)

利用 **Visual Studio 2012** 节点，你可以在 Visual Studio 2013 的模板的默认列表中选择无法访问的以下 web 模板：

- ASP.NET MVC 4 Web 应用程序
- ASP.NET 动态数据实体 Web 应用程序
- ASP.NET AJAX 服务器控件
- ASP.NET AJAX 服务器控件扩展程序
- ASP.NET 服务器控件

<a id="bootstrap"></a>
## <a name="bootstrap-in-the-visual-studio-2013-web-project-templates"></a>Visual Studio 2013 web 项目模板中的启动

Visual Studio 2013 项目模板使用由 Twitter 创建的 [启动](http://getbootstrap.com/)、布局和主题框架。 启动使用 CSS3 来提供响应式设计，这意味着布局可以动态适应不同的浏览器窗口大小。 例如，在宽度浏览器窗口中，Web 窗体模板创建的主页如下图所示：

![Web 窗体模板应用主页](creating-web-projects-in-visual-studio/_static/image16.png)

使窗口变窄，水平排列的列会转换为垂直排列：

![启动垂直列排列](creating-web-projects-in-visual-studio/_static/image17.png)

稍微缩小窗口，水平顶部菜单将变成一个图标，单击该图标可将其展开为垂直方向的菜单：

!["启动" 菜单图标](creating-web-projects-in-visual-studio/_static/image18.png)

![启动垂直菜单](creating-web-projects-in-visual-studio/_static/image19.png)

你还可以使用启动的主题功能轻松地对应用程序的外观进行更改。 例如，你可以执行以下步骤来更改主题。

1. 在浏览器中，依次 [http://Bootswatch.com](http://Bootswatch.com) 单击 ""、"主题"，然后单击 " **下载**"。 默认情况下 (*此下载*如果要检查 CSS 代码，请获取缩小版本而不是*版本。 ) *
2. 复制已下载的 CSS 文件的内容。
3. 在 Visual Studio 的 " *Content* " 文件夹中创建一个名为*Bootstrap-theme*的新**样式表**文件，然后将下载的 css 代码粘贴到该文件中。
4. 打开 "*应用 \_ 启动/Bundle.config* "，并将 " *bootstrap-theme* *" 更改为*""。

再次运行该项目，并且该应用程序具有新的外观。 下图显示了 Amelia 主题的效果：

![启动 Amelia 主题](creating-web-projects-in-visual-studio/_static/image20.png)

许多启动主题都可用，包括免费版和高级版。 "启动" 还提供各种 UI 组件，例如[下拉](http://twitter.github.io/bootstrap/components.html#dropdowns)[按钮、按钮组](http://twitter.github.io/bootstrap/components.html#buttonGroups)和[图标](http://twitter.github.io/bootstrap/base-css.html#images)。 有关引导的详细信息，请参阅 [启动站点](http://twitter.github.io/bootstrap/)。

如果你在 Visual Studio 中使用 Web 窗体设计器，请注意，设计器不支持 CSS3，因此它不能准确地显示启动主题的所有影响或响应式布局更改。 但是，在使用浏览器进行查看时，Web 窗体页会正确显示。

<a id="add"></a>
## <a name="adding-support-for-additional-frameworks"></a>添加对其他框架的支持

选择模板时，会自动选择该模板所使用的框架 () 的复选框。 例如，如果选择 **"web 窗体" 模板，** 则会选中 " **web 窗体** " 复选框，因此无法将其清除。

![选择模板](creating-web-projects-in-visual-studio/_static/image21.png)

![添加框架](creating-web-projects-in-visual-studio/_static/image22.png)

您可以为未包含在模板中的框架选中此复选框，以便在创建项目时添加对该框架的支持。 例如，若要启用 Web Forms *.aspx* 页，请在选择 MVC 模板时选中 " **Web 窗体** " 复选框。 若要在使用 Web 窗体模板时启用 MVC，请单击 " **mvc** " 复选框。 添加框架可启用设计时和运行时支持。 例如，如果将 MVC 支持添加到 Web 窗体项目，将能够基架控制器和视图。

如果将 Web 窗体和 MVC 合并到项目中并在 Web 窗体中启用 [友好 url](http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx) ，可能会出现意外的路由问题，其中一个 URL 具有多个可能的目标。 首先定义的路由将优先。 例如，如果你有一个 `Home` 控制器和一个 "*主页*" 页，则在调用 `http://contoso.com/home` RouteConfig.cs 中的方法之前调用方法时，url 将会跳到 "*主页*"; `EnableFriendlyUrls` `MapRoute` *RouteConfig.cs* `Home` 如果你在之前调用，则该 url 将为控制器的默认视图 `MapRoute` `EnableFriendlyUrls` 。

添加框架不会添加任何示例应用程序功能。 例如，如果在选择 MVC 模板时添加 Web 窗体支持，则不会创建任何 *default.aspx* 主页文件。 仅添加支持框架所需的文件夹、文件和引用。 出于此原因，添加框架不会更改身份验证选项，这些选项由模板创建的示例应用程序中的代码来实现。 例如，如果选择空模板并添加 Web 窗体或 MVC 支持，则仍将禁用 " **配置身份验证** " 按钮。

以下各节简要说明了每个复选框的效果。

### <a name="add-web-forms-support"></a>添加 Web 窗体支持

创建空的 *应用 \_ 数据* 和 *模型* 文件夹以及 *global.asax* 文件。 这些模板已由除空模板之外的所有模板创建，因此，选择 "Web 窗体" 复选框对其他模板没有任何区别。

默认情况下，Web 窗体模板启用友好 Url，但当你通过选中 "Web 窗体" 复选框来向其他模板添加 Web 窗体支持时，不会自动启用友好 Url。

### <a name="add-mvc-support"></a>添加 MVC 支持

安装 MVC、Razor 和网页 NuGet 包，创建空的*应用 \_ 数据*、*控制器*、*模型*和*视图*文件夹，创建包含*RouteConfig.cs*文件的*应用 \_ 启动*文件夹，并创建*global.asax*文件。

### <a name="add-web-api-support"></a>添加 Web API 支持

在 NuGet 包上安装 WebApi 和 Newtonsoft.Js，创建空的*应用 \_ 数据*、*控制器*和*模型*文件夹，创建包含*WebApiConfig.cs*文件的*应用 \_ 启动*文件夹，并创建*global.asax*文件。

<a id="auth"></a>
## <a name="authentication-methods"></a>身份验证方法

Visual Studio 2013 为 Web 窗体、MVC 和 Web API 模板提供多种身份验证选项：

- [无身份验证](#noauth)
- [单个用户帐户](#indauth) (ASP.NET Identity （以前称为 ASP.NET 成员身份）) 
- [组织帐户](#orgauth) (Windows Server Active Directory 或 Azure Active Directory) 
- [Windows 身份验证](#winauth) (Intranet) 

![配置身份验证对话框](creating-web-projects-in-visual-studio/_static/image23.png)

<a id="noauth"></a>

### <a name="no-authentication"></a>无身份验证

如果你选择 " **无身份验证**"，则示例应用程序将不包含用于登录的 web 页，无指示登录者的 UI，没有成员资格数据库的实体类，并且没有成员资格数据库的连接字符串。

<a id="indauth"></a>
### <a name="individual-user-accounts"></a>单个用户帐户

如果选择 **单个用户帐户**，示例应用程序将配置为使用 ASP.NET Identity (以前称为用户身份验证) 的 ASP.NET 成员身份。 ASP.NET Identity 允许用户通过在网站上创建用户名和密码，或使用社交提供程序（如 Facebook、Google、Microsoft 帐户或 Twitter）登录来注册帐户。 ASP.NET Identity 中用户配置文件的默认数据存储是 SQL Server 的 LocalDB 数据库，可以将其部署到生产站点 SQL Server 或 Azure SQL 数据库。

Visual Studio 2013 中，这些功能与在 Visual Studio 2012 中相同，但已重新编写 ASP.NET 成员资格系统的基础代码。 新基本代码的优点包括：

- 新的成员资格系统基于 [OWIN](http://owin.org/) 而不是 ASP.NET Forms 身份验证模块。 这意味着，无论你使用的是 IIS 中的 Web 窗体或 MVC，还是自托管 Web API 或 SignalR，都可以使用相同的身份验证机制。
- 新的成员资格数据库由实体框架的 Code First 进行管理，所有表均由可修改的实体类表示。 这意味着你可以轻松地自定义数据库架构和与配置文件相关的 web UI，以满足你自己的需求，并且你可以使用 Code First 迁移轻松部署更新。

新的成员资格系统是在新模板中自动实现的，可在面向 .NET 4.5 或更高版本的任何项目中手动实现。

如果要创建主要用于外部客户的 Internet 网站，ASP.NET Identity 是一个不错的选择。 如果你的组织使用 Active Directory 或 Office 365，并且你想要创建为员工和业务合作伙伴启用单一登录的项目，则 " **组织帐户** " 选项可能是更好的选择。

有关各个用户帐户选项的详细信息，请参阅以下资源：

- [www.asp.net/identity](../../../identity/index.md)。 ASP.NET 网站上有关 ASP.NET Identity 的文档。
- [使用 Facebook 和 Google OAuth2 和 OpenID 登录创建 ASP.NET MVC 5 应用](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)。 还介绍如何自定义用户配置文件数据。
- [Web API-外部身份验证服务](../../../web-api/overview/security/external-authentication-services.md)
- [将外部登录名添加到 Visual Studio 2013 中的 ASP.NET 应用程序](https://blogs.msdn.com/b/webdev/archive/2013/06/27/adding-external-logins-to-your-asp-net-application-in-visual-studio-2013.aspx)

<a id="orgauth"></a>
### <a name="organizational-accounts"></a>组织帐户

如果选择 " **组织帐户**"，则会将示例应用程序配置为使用 Windows Identity FOUNDATION (WIF) ，以根据 Azure Active Directory (Azure AD 中的用户帐户进行身份验证，其中包括 Office 365) 或 Windows Server Active Directory。 有关详细信息，请参阅本主题后面的 [组织帐户身份验证选项](#orgauthoptions) 。

<a id="winauth"></a>
### <a name="windows-authentication"></a>Windows 身份验证

如果选择 **Windows 身份验证**，示例应用程序将配置为使用 Windows 身份验证 IIS 模块进行身份验证。 应用程序将显示登录到 Windows 中的 Active directory 或本地计算机帐户的域和用户 ID，但不包括用户注册或登录 UI。 此选项适用于 Intranet 网站。

或者，你可以通过选择 " [组织帐户" 下](#orgauthonprem)的 "本地" 选项来创建使用 AD 身份验证的 Intranet 站点。 本地选项使用 Windows Identity Foundation (WIF) 而不是 Windows 身份验证模块。 若要设置本地选项，需要执行一些其他步骤，但 WIF 会启用 Windows 身份验证模块不可用的功能。 例如，使用 WIF 可以在 Active Directory 和查询目录数据中配置应用程序访问。

<a id="orgauthoptions"></a>
## <a name="organizational-account-authentication-options"></a>组织帐户身份验证选项

" **配置身份验证** " 对话框提供了 Azure Active Directory (Azure AD 的几个选项，其中包括 Office 365) 或 Windows Server ACTIVE DIRECTORY (AD) 帐户身份验证：

- 使用与 Azure AD 的目录集成 (Azure AD 或 AD[的云单一组织](#orgauthsingle)) 
- [云-多个组织](#orgauthmulti) (Azure AD，或使用与 Azure AD 的目录集成的 AD) 
- [本地](#orgauthonprem) (AD) 

如果要尝试 Azure AD 选项之一但还没有帐户，请 [单击此处注册 Azure AD 帐户](https://go.microsoft.com/fwlink/?LinkId=309942)。

> [!NOTE]
> 如果选择 Azure AD 选项之一，则项目需要一个数据库，并且必须登录到 Azure AD 租户的全局管理员帐户。 输入组织帐户的 "名称" 和 "密码" (例如， admin@contoso.onmicrosoft.com) ，该帐户具有 Azure AD 租户的管理权限。
> 
> **请勿输入 Microsoft 帐户的凭据 (例如， contoso@hotmail.com 在 "登录" 对话框中) 。**

<a id="orgauthsingle"></a>
### <a name="cloud---single-organization-authentication"></a>云-单一组织身份验证

![单个组织身份验证](creating-web-projects-in-visual-studio/_static/image24.png)

如果要为在一个 Azure AD [租户](https://technet.microsoft.com/library/jj573650.aspx)中定义的用户帐户启用身份验证，请选择此选项。 例如，该站点是 contoso.com 的，它将可供 Contoso 公司的员工在 contoso.onmicrosoft.com 租户中使用。 无法将 Azure AD 配置为允许其他租户的用户访问该应用程序。

#### <a name="domain"></a>Domain

输入要在其中安装应用程序的 Azure AD 域，例如： `contoso.onmicrosoft.com` 。 如果你有 [自定义域](http://www.cloudidentity.com/blog/2013/04/14/adding-a-custom-domain-to-your-windows-azure-ad/)，如 `contoso.com` 而不是 `contoso.onmicrosoft.com` ，则可以在此处输入。

#### <a name="access-level"></a>访问级别

如果应用程序需要使用图形 API 查询或更新目录信息，请选择 " **单一登录"、"读取目录数据"** 或 **"单一登录"、"读取和写入目录数据"**。 否则，请选择 " **单一登录**"。 有关详细信息，请参阅 [应用程序访问级别](https://msdn.microsoft.com/library/windowsazure/b08d91fa-6a64-4deb-92f4-f5857add9ed8#BKMK_AccessLevels) 和 [使用图形 API 查询 Azure AD](https://msdn.microsoft.com/library/windowsazure/dn151791.aspx)。

#### <a name="application-id-uri"></a>应用程序 ID URI

默认情况下，模板会通过将项目名称追加到 Azure AD 域，为你创建一个应用程序 ID URI。 例如，如果项目名称为， `Example` 且域为 `contoso.onmicrosoft.com` ，则应用程序 ID URI 将变为 `https://contoso.onmicrosoft.com/Example` 。 如果要手动指定应用程序 ID URI，请展开 " **更多选项** " 部分，然后在文本框中输入应用程序 id uri。 应用程序 ID URI 必须以开头 `https://` 。

默认情况下，如果已在 Azure AD 中预配的应用程序与 Visual Studio 用于该项目的应用程序 ID URI 相同，则该项目将连接到现有应用程序，而不是预配新应用程序。 如果希望在这种情况下预配新应用程序，请清除 " **如果已存在具有相同 ID 的应用程序项** " 复选框。

如果清除了 " **覆盖** " 复选框，并且 Visual Studio 查找具有相同应用程序 ID URI 的现有应用程序，则它会通过向要使用的 uri 追加一个数字来创建一个新的 uri。 例如，假设项目名称为 `Example` ，您将文本框留空，则清除 " **覆盖** " 复选框，并且 Azure AD 租户已经有一个具有 URI 的应用程序 `https://contoso.onmicrosoft.com/Example` 。 在这种情况下，将使用类似的应用程序 ID URI 来预配新应用程序 `https://contoso.onmicrosoft.com/Example_20130619330903` 。

#### <a name="provisioning-the-application-in-azure-ad"></a>在 Azure AD 中设置应用程序

若要在 Azure AD 中设置应用程序，或将项目连接到现有应用程序，Visual Studio 需要域的全局管理员凭据。 当你在 "**配置身份验证**" 对话框中单击 **"确定"** 时，系统将提示你输入指定域的全局管理员的用户名和密码。 稍后，当你在 "**新建 ASP.NET 项目**" 对话框中单击 "**创建项目**" 时，Visual Studio 会在 Azure AD 中预配应用程序。 请注意，在此过程中，Visual Studio 会将客户端机密值嵌入到 Web.config 文件中，该文件在创建后的一年后过期。

有关如何创建使用 **云单一组织** 身份验证的应用程序的信息，请参阅以下资源：

- [Azure 身份验证](../2012/windows-azure-authentication.md)
- [使用 Azure AD 将登录名添加到 Web 应用程序中](https://msdn.microsoft.com/library/windowsazure/dn151790.aspx)
- [借助 Azure Active Directory 开发 ASP.NET 应用](../../../identity/overview/getting-started/developing-aspnet-apps-with-windows-azure-active-directory.md)
- [安全 ASP.NET Web API 与 Azure AD 和 Microsoft OWIN 组件](https://msdn.microsoft.com/magazine/dn463788.aspx)

尚未更新 Visual Studio 2013 的教程;其中一些指导您手动执行的操作将在 Visual Studio 2013 自动执行。

<a id="orgauthmulti"></a>
### <a name="cloud---multi-organization-authentication"></a>云-多组织身份验证

![多组织身份验证](creating-web-projects-in-visual-studio/_static/image25.png)

如果要为多个 Azure AD [租户](https://technet.microsoft.com/library/jj573650.aspx)中定义的用户帐户启用身份验证，请选择此选项。 例如，该站点是 contoso.com 的，它将可供 Contoso 公司的员工在 contoso.onmicrosoft.com 租户中使用，并可供在 fabrikam.onmicrosoft.com 租户中的 Fabrikam 公司的员工使用。

输入的设置与应用程序预配步骤类似于 [单个组织身份验证](#orgauthsingle)。

有关如何创建使用 **云多组织** 身份验证的应用程序的信息，请参阅以下资源：

- [简单的 Web 应用与 Azure Active Directory、ASP.NET &amp; 的集成](https://blogs.msdn.com/b/active_directory_team_blog/archive/2013/06/26/improved-windows-azure-active-directory-integration-with-asp-net-amp-visual-studio.aspx) Active Directory 团队博客上的 Visual Studio。
- [Azure AD 教程开发多租户 Web 应用程序](https://msdn.microsoft.com/library/windowsazure/dn151789.aspx) 。 本教程尚未针对 Visual Studio 2013 进行更新;本教程中的一些操作可在 Visual Studio 2013 自动执行。
- 在[登录之前，必须注册你自己的多组织 ASP.NET 应用](http://www.cloudidentity.com/blog/2013/10/26/you-have-to-sign-up-with-your-own-multiple-organizations-asp-net-app-before-you-can-sign-in/)。 Vittorio Bertocci 的博客，介绍如何解决用户在创建使用多组织身份验证的项目时遇到的常见问题。

<a id="orgauthonprem"></a>
### <a name="on-premises-organizational-authentication"></a>本地组织身份验证

![本地组织身份验证](creating-web-projects-in-visual-studio/_static/image26.png)

如果要为 Windows Server Active Directory (AD) 中定义的用户帐户启用身份验证，并且不希望使用 Azure AD，请选择此选项。 可以使用此选项创建 Intranet 站点或 Internet 站点。 对于 Internet 站点，使用 Active Directory 联合身份验证服务 (ADFS) 提供对 AD 的访问权限。 有关详细信息，请参阅在 [Visual Studio 2013 中 (ADFS) 与 ASP.NET 配合使用](http://www.cloudidentity.com/blog/2014/02/12/use-the-on-premises-organizational-authentication-option-adfs-with-asp-net-in-visual-studio-2013/)。

对于 Intranet 站点，作为替代方法，你可以选择 " [Windows 身份验证](#winauth) "，而不是使用此选项。 对于 Windows 身份验证选项，无需提供元数据文档 URL。 但是，Windows 身份验证不允许在 Active Directory 或查询目录数据的情况下控制应用程序访问。

#### <a name="on-premises-authority"></a>本地颁发机构

输入指向元数据文档的 URL。 元数据文档包含机构的坐标。 应用程序将使用这些坐标来驱动 web 登录流。

#### <a name="application-id-uri"></a>应用程序 ID URI

提供一个可供 AD 用来标识此应用程序的唯一 URI，或留空以让 Visual Studio 创建一个。

<a id="nextsteps"></a>
## <a name="next-steps"></a>后续步骤

本文档提供了一些在 Visual Studio 2013 中创建新的 ASP.NET web 项目的基本帮助。 有关使用 for Visual Studio 进行 web 开发的详细信息，请参阅 [https://www.asp.net/visual-studio/](../../index.md) 。

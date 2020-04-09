---
uid: visual-studio/overview/2013/creating-web-projects-in-visual-studio
title: 在可视化工作室创建ASP.NET Web 项目 2013 |微软文档
author: tdykstra
description: 本主题介绍在 Visual Studio 2013 中创建ASP.NET Web 项目的选项，其中介绍了 Web 开发中的一些新功能。
ms.author: riande
ms.date: 12/01/2014
ms.assetid: 61941e64-0c0d-4996-9270-cb8ccfd0cabc
msc.legacyurl: /visual-studio/overview/2013/creating-web-projects-in-visual-studio
msc.type: authoredcontent
ms.openlocfilehash: fbb4cd7afa2506879d47bce980bf0164aad40c2c
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675681"
---
# <a name="creating-aspnet-web-projects-in-visual-studio-2013"></a>在 Visual Studio 2013 中创建 ASP.NET Web 项目

汤姆[·戴克斯特拉](https://github.com/tdykstra)

> 本主题介绍使用 Update 3 在 Visual Studio 2013 中创建ASP.NET Web 项目的选项
> 
> 与早期版本的 Visual Studio 相比，以下是 Web 开发中的一些新功能：
> 
> - 用于创建支持[多个ASP.NET框架](#add)（Web 窗体、MVC 和 Web API）的项目的简单 UI。
> - [ASP.NET标识](#indauth)，一个新的ASP.NET成员系统，在所有ASP.NET框架中都工作相同，并且与IIS以外的Web托管软件配合使用。
> - 使用[Bootstrap](#bootstrap)提供响应式设计和准备功能。
> - 以前只为 MVC 提供的 Web 窗体的新功能，例如[自动测试项目创建](#testproj)和 Intranet[网站模板](#winauth)。
> 
> 有关如何为 Azure 云服务或 Azure 移动服务创建 Web 项目的信息，请参阅[使用 Azure 云服务开始使用"ASP.NET"](https://azure.microsoft.com/documentation/articles/cloud-services-dotnet-get-started/)以及[使用 Azure 移动服务 .NET 后端创建排行榜应用](https://azure.microsoft.com/documentation/articles/mobile-services-dotnet-backend-windows-store-dotnet-leaderboard/)。

<a id="prerequisites"></a>
## <a name="prerequisites"></a>先决条件

本文适用于安装了[更新 3](https://go.microsoft.com/fwlink/?linkid=397827&amp;clcid=0x409)的 Visual [Studio 2013。](https://go.microsoft.com/fwlink/?LinkId=306566)

<a id="wap"></a>
## <a name="web-application-projects-versus-web-site-projects"></a>Web 应用程序项目与网站项目

ASP.NET在两种Web项目之间做出选择 *：Web应用程序*项目和*网站项目*。 我们建议 Web 应用程序项目用于新开发，本文仅适用于 Web 应用程序项目。 有关详细信息，请参阅 MSDN 网站上的[Visual Studio 中的 Web 应用程序项目与网站项目](https://msdn.microsoft.com/library/dd547590(v=vs.120).aspx)。

<a id="overview"></a>
## <a name="overview-of-web-application-project-creation"></a>Web 应用程序项目创建概述

以下步骤演示如何创建 Web 项目：

1. 单击 **"开始"** 页或 **"文件**"菜单中的 **"新项目**"。
2. 在 **"新项目"** 对话框中，单击左侧窗格中的**Web，** 并在中间窗格**中单击 ASP.NET Web 应用程序**。

    ![“新建项目”对话框](creating-web-projects-in-visual-studio/_static/image1.png)

    可以选择左侧窗格中的 **"云**"来创建[Azure 云服务](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy)[、Azure 移动服务](https://msdn.microsoft.com/library/windows/apps/dn629482.aspx)或[Azure WebJob](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-webjobs)。 本主题不包括这些模板。
3. 在右侧窗格中，如果希望对应用程序进行运行状况和使用情况监视，请单击"**将应用程序见解添加到项目**"复选框。 有关详细信息，请参阅[在 Web 应用程序中监视性能](https://azure.microsoft.com/documentation/articles/app-insights-web-monitor-performance/)。
4. 指定项目**名称**、**位置**和其他选项，然后单击 **"确定**"。

    此时将出现 **“新建 ASP.NET 项目”** 对话框。

    ![“新建项目”对话框](creating-web-projects-in-visual-studio/_static/image2.png)
5. 单击模板。

    ![选择模板](creating-web-projects-in-visual-studio/_static/image3.png)
6. 如果要添加对模板中未包括的其他框架的支持，请单击相应的复选框。 （在所示示例中，您可以将 MVC 和/或 Web API 添加到 Web 窗体项目中。

    ![添加框架](creating-web-projects-in-visual-studio/_static/image4.png)
7. <a id="testproj"></a>如果要添加单元测试项目，请单击"**添加单元测试**"。

    ![添加单元测试](creating-web-projects-in-visual-studio/_static/image5.png)
8. 如果想要与模板默认提供的身份验证方法不同的身份验证方法，请单击"**更改身份验证**"。

    ![配置身份验证按钮](creating-web-projects-in-visual-studio/_static/image6.png)

    ![配置身份验证对话框](creating-web-projects-in-visual-studio/_static/image7.png)

<a id="azurenewproj"></a>
### <a name="create-a-web-app-or-virtual-machine-in-azure"></a>在 Azure 中创建 Web 应用或虚拟机

Visual Studio 包含的功能，使使用 Azure 服务轻松托管 Web 应用程序。 例如，您可以在 Visual Studio IDE 中执行以下所有操作：

- 创建和管理 Web 应用或虚拟机，使应用程序在 Internet 上可用。
- 查看应用程序在云中运行时创建的日志。
- 应用程序在云中运行时，在调试模式下远程运行。
- 查看和管理其他 Azure 服务，如 SQL 数据库。

您可以创建包含基本服务（如免费 Web 应用）的[Azure 帐户](https://www.windowsazure.com/pricing/free-trial/)，如果您是 MSDN 订阅者，则可以[激活每月](https://azure.microsoft.com/pricing/member-offers/visual-studio-subscriptions/)为其他 Azure 服务提供积分的好处。 

默认情况下，"**新建ASP.NET项目"** 对话框使您能够为新 Web 项目创建 Web 应用或虚拟机。 如果不想创建新的 Web 应用或虚拟机，请清除**云中的"主机**"复选框。

![创建远程资源](creating-web-projects-in-visual-studio/_static/image8.png)

复选框标题可能是**云中的主机**或**创建远程资源**，在这两种情况下效果都相同。 如果选中选中该复选框，Visual Studio 默认情况下会在 Azure 应用服务中创建 Web 应用。 如果您愿意，可以使用下拉框将该框更改为**虚拟机**。 如果您尚未登录到 Azure，系统将提示您输入 Azure 凭据。 登录后，一个对话框允许您配置 Visual Studio 将为项目创建的资源。 下图显示了 Web 应用的对话框;如果选择创建虚拟机，则会出现不同的选项。

![配置 Azure 应用设置](creating-web-projects-in-visual-studio/_static/image9.png)

有关如何使用此过程创建 Azure 资源的详细信息，请参阅使用 Azure[启动和ASP.NET](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet)以及[使用 Visual Studio 为网站创建虚拟机](https://azure.microsoft.com/documentation/articles/virtual-machines-dotnet-create-visual-studio-powershell/)。

本文的其余部分提供了有关可用模板及其选项的详细信息。 本文还介绍了模板中使用的 Bootstrap、布局和准备框架。

<a id="vs2013"></a>
## <a name="visual-studio-2013-web-project-templates"></a>可视化工作室 2013 Web 项目模板

Visual Studio 使用模板创建 Web 项目。 项目模板可以在新项目中创建文件和文件夹，安装 NuGet 包，并为基本工作应用程序提供示例代码。 模板实现最新的 Web 标准，旨在演示如何使用ASP.NET技术的最佳做法，并让您开始创建自己的应用程序。

Visual Studio 2013 为针对 .NET 4.5 或更高版本的 .NET 框架的项目提供了以下 Web 项目模板选项：

- [空模板](#empty)
- [Web 表单模板](#wf)
- [MVC 模板](#mvc)
- [Web API 模板](#webapi)
- [单页应用程序模板](#spa)
- [Azure 移动服务模板](https://azure.microsoft.com/documentation/articles/mobile-services-dotnet-backend-windows-store-dotnet-leaderboard/)
- [视觉工作室 2012 模板](#vs2012)

您还可以安装提供[Facebook 模板](#facebook)的视觉工作室扩展。

有关如何创建面向 .NET 4 的项目的信息，请参阅本主题后面的[Visual Studio 2012 模板](#vs2012)。

有关如何为移动客户端创建ASP.NET应用程序的信息，请参阅 ASP.NET[中的移动支持](../../../mobile/overview.md)。

<a id="empty"></a>
### <a name="empty-template"></a>空模板

"空"模板为ASP.NET Web 应用（如项目文件 *（.csproj*或 ）提供最少的文件夹和文件。*vbproj*） 和*Web.config*文件。 您可以使用"**添加文件夹"下的复选框和核心引用**：标签，添加对 Web 窗体、MVC 和/或 Web API 的支持。

对于空模板，没有可用的身份验证选项。 身份验证功能在示例应用程序中实现，空模板不创建示例应用程序。

<a id="wf"></a>
### <a name="web-forms-template"></a>Web 表单模板

Web 窗体框架提供了以下功能，使您能够快速生成具有丰富 UI 和数据访问功能的网站：

- 视觉工作室的 WYSIWYG 设计师。
- 呈现 HTML 的服务器控件，以及可以通过设置属性和样式进行自定义的服务器控件。
- 用于数据访问和数据显示的丰富类型控件。
- 公开事件的事件模型，您可以像对客户端应用程序（如 WPF）进行编程一样进行编程。
- 自动在 HTTP 请求之间保留状态（数据）。

通常，与使用ASP.NET MVC 框架创建同一应用程序相比，创建 Web 窗体应用程序所需的编程工作量更少。 但是，Web 窗体并不仅仅用于快速应用程序开发。 有许多复杂的商业应用程序和框架建立在 Web 窗体之上。

由于 Web 窗体页和页面上的控件会自动生成发送到浏览器的大部分标记，因此您没有 ASP.NET MVC 提供的 HTML 的细粒度控制。 用于配置页面和控件的声明性模型最大限度地减少了必须编写的代码量，但隐藏了 HTML 和 HTTP 的某些行为。 例如，并不总是能够准确指定控件可能生成哪些标记。

Web 窗体框架不像 MVC ASP.NET一样容易适应基于模式的开发实践，例如[测试驱动开发](http://en.wikipedia.org/wiki/Test-driven_development)、[关注分离](http://en.wikipedia.org/wiki/Separation_of_concerns)、[控制反转](http://en.wikipedia.org/wiki/Inversion_of_control)和[依赖注入](http://en.wikipedia.org/wiki/Dependency_injection)。 如果要用这种方式编写分解的代码，可以;它只是不像ASP.NETMVC框架那样自动。 [ASP.NET Web 窗体 MVP](http://webformsmvp.com/)项目展示了一种有助于区分关注点和可测试性的方法，同时保持 Web 窗体为交付而构建的快速开发。 微软 SharePoint 建立在 Web 表单 MVP 之上。

Web 窗体模板创建一个示例 Web 窗体应用程序，该应用程序使用[Bootstrap](#bootstrap)提供响应式设计和主发功能。 下图显示了主页。

![Web 表单模板应用主页](creating-web-projects-in-visual-studio/_static/image10.png)

有关 Web 窗体的详细信息，请参阅[ASP.NET Web 窗体](https://asp.net/web-forms)。 有关 Web 表单模板为您做什么的信息，请参阅使用[Visual Studio 2013 构建基本 Web 表单应用程序](https://blogs.msdn.com/b/webdev/archive/2013/12/19/building-a-basic-web-forms-application-using-visual-studio-2013.aspx)。

<a id="mvc"></a>
### <a name="mvc-template"></a>MVC 模板

ASP.NET MVC 旨在促进基于模式的开发实践，例如[测试驱动开发](http://en.wikipedia.org/wiki/Test-driven_development)、[关注分离](http://en.wikipedia.org/wiki/Separation_of_concerns)、[控制反转](http://en.wikipedia.org/wiki/Inversion_of_control)和[依赖注入](http://en.wikipedia.org/wiki/Dependency_injection)。 该框架鼓励将 Web 应用程序的业务逻辑层与其表示层分开。 通过将应用程序划分为模型 （M）、视图 （V） 和控制器 （C），ASP.NET MVC 可以更轻松地管理较大应用程序中的复杂性。

使用ASP.NET MVC，您更直接地使用 HTML 和 HTTP 而不是 Web 窗体。 例如，Web 窗体可以在 HTTP 请求之间自动保留状态，但您必须在 MVC 中显式编写代码。 MVC 模型的优点是，它使您能够完全控制应用程序正在执行的操作以及它在 Web 环境中的表现。 缺点是您必须编写更多的代码。

MVC 设计为可扩展，使电力开发人员能够根据他们的应用程序需求自定义框架。 此外，ASP.NET MVC 源代码在 OSI 许可证下可用。

MVC 模板创建一个示例 MVC 5 应用程序，该应用程序使用[Bootstrap](#bootstrap)提供响应式设计和主旋律功能。 下图显示了主页。

![MVC 示例应用](creating-web-projects-in-visual-studio/_static/image11.png)

有关 MVC 的详细信息，请参阅[ASP.NET MVC](https://asp.net/mvc)。 有关如何选择 MVC 4 模板的信息，请参阅本文后面的[Visual Studio 2012 模板](#vs2012)。

<a id="webapi"></a>
### <a name="web-api-template"></a>Web API 模板

Web API 模板基于 Web API 创建示例 Web 服务，包括基于 MVC 的 API 帮助页。

ASP.NET Web API 是一种框架，用于轻松构建可以访问多种客户端（包括浏览器和移动设备）的 HTTP 服务。 ASP.NET Web API 是在 .NET 框架上构建 RESTful 服务的理想平台。

Web API 模板创建示例 Web 服务。 下图显示了示例帮助页。

![Web API 帮助页](creating-web-projects-in-visual-studio/_static/image12.png)

![用于 GET API 的 Web API 帮助页](creating-web-projects-in-visual-studio/_static/image13.png)

有关 Web API 的详细信息，请参阅[ASP.NET Web API](https://asp.net/web-api)。

<a id="spa"></a>
### <a name="single-page-application-template"></a>Single Page Application Template（单页应用程序模板）

单页应用程序 （SPA） 模板创建一个示例应用程序，该应用程序在客户端上使用 JavaScript、HTML 5 和[挖空JS，](http://knockoutjs.com/)并在服务器上ASP.NET Web API。

SPA 模板的唯一身份验证选项是[个人用户帐户](#indauth)。

下图显示了 SPA 模板生成的示例应用程序的初始状态。

![SPA 示例应用](creating-web-projects-in-visual-studio/_static/image14.png)

有关如何使用 SPA 模板创建应用程序的信息，请参阅[Web API - 外部身份验证服务](../../../web-api/overview/security/external-authentication-services.md)。

有关ASP.NET单页应用程序以及使用 JavaScript 框架（而不是挖空JS）的其他 SPA 模板的详细信息，请参阅以下资源：

- [ASP.NET单页应用程序](../../../single-page-application/index.md)。
- [了解 VS2013 RC SPA 模板中的安全功能](https://blogs.msdn.com/b/webdev/archive/2013/09/20/understanding-security-features-in-spa-template.aspx)
- [单页应用程序：使用ASP.NET构建现代、响应迅速的 Web 应用程序](https://msdn.microsoft.com/magazine/dn463786.aspx)

<a id="facebook"></a>
### <a name="facebook-template"></a>Facebook 模板

您可以安装一个[视觉工作室扩展，提供一个Facebook模板](https://go.microsoft.com/fwlink/?LinkID=509965&amp;clcid=0x409)。 此模板创建一个示例应用程序，该应用程序旨在在 Facebook 网站内运行。 它基于ASP.NET MVC，并使用 Web API 进行实时更新功能。

Facebook 模板没有可用的身份验证选项，因为 Facebook 应用程序在 Facebook 网站内运行，并且依赖于 Facebook 的身份验证。

有关ASP.NET Facebook 应用程序的详细信息，请参阅[更新 MVC Facebook API](https://blogs.msdn.com/b/webdev/archive/2014/06/10/updating-the-mvc-facebook-api.aspx)。

<a id="vs2012"></a>
### <a name="visual-studio-2012-templates"></a>视觉工作室 2012 模板

Visual Studio 2013 Web 项目创建对话框不提供对 Visual Studio 2012 中提供的某些模板的访问。 如果要使用这些模板之一，可以单击"可视化工作室新项目"对话框左侧窗格中的 Visual Studio 2012 节点。

![可视化工作室 2012 模板](creating-web-projects-in-visual-studio/_static/image15.png)

**Visual Studio 2012**节点允许您在 Visual Studio 2013 的默认模板列表中选择您无法访问的以下 Web 模板：

- ASP.NET MVC 4 Web 应用程序
- ASP.NET 动态数据实体 Web 应用程序
- ASP.NET AJAX 服务器控制
- ASP.NET AJAX 服务器控制扩展器
- ASP.NET服务器控制

<a id="bootstrap"></a>
## <a name="bootstrap-in-the-visual-studio-2013-web-project-templates"></a>可视化工作室 2013 Web 项目模板中的引导

Visual Studio 2013 项目模板使用[Bootstrap，](http://getbootstrap.com/)这是一个由 Twitter 创建的布局和主框。 Bootstrap 使用 CSS3 提供响应式设计，这意味着布局可以动态适应不同的浏览器窗口大小。 例如，在宽浏览器窗口中，Web 窗体模板创建的主页如下所示：

![Web 表单模板应用主页](creating-web-projects-in-visual-studio/_static/image16.png)

使窗口变窄，水平排列的列移动到垂直排列中：

![引导垂直柱排列](creating-web-projects-in-visual-studio/_static/image17.png)

稍微缩小窗口范围，水平顶部菜单将变为一个图标，您可以单击该图标以展开为垂直方向的菜单：

![引导菜单图标](creating-web-projects-in-visual-studio/_static/image18.png)

![引导垂直菜单](creating-web-projects-in-visual-studio/_static/image19.png)

您还可以使用 Bootstrap 的"主"功能轻松影响应用程序的外观和感觉的变化。 例如，您可以执行以下步骤来更改主题。

1. 在浏览器中，转到[http://Bootswatch.com](http://Bootswatch.com)，选择主题，然后单击"**下载**"。 （默认情况下，此下载*引导.min.css;* 如果要检查 CSS 代码，请获取*引导.css*而不是小版本。
2. 复制下载的 CSS 文件的内容。
3. 在 Visual Studio 中，在*内容*文件夹中创建名为*bootstrap-thethe.css*的新**样式表**文件，并将下载的 CSS 代码粘贴到其中。
4. 打开*应用程序\_开始/捆绑.配置*和更改*引导.css*到*引导主题.css*.

再次运行项目，应用程序具有新外观。 下图显示了阿米莉亚主题的效果：

![靴子阿米莉亚主题](creating-web-projects-in-visual-studio/_static/image20.png)

许多引导主题是可用的，无论是免费和高级版本。 Bootstrap 还提供多种 UI 组件，如[下拉](http://twitter.github.io/bootstrap/components.html#dropdowns)、[按钮组](http://twitter.github.io/bootstrap/components.html#buttonGroups)和[图标](http://twitter.github.io/bootstrap/base-css.html#images)。 有关引导器的详细信息，请参阅[引导站点](http://twitter.github.io/bootstrap/)。

如果在 Visual Studio 中使用 Web 窗体设计器，请注意，设计器不支持 CSS3，因此无法准确显示 Bootstrap 主题或响应式布局更改的所有效果。 但是，使用浏览器查看时，Web 窗体页面将正确显示。

<a id="add"></a>
## <a name="adding-support-for-additional-frameworks"></a>添加对附加框架的支持

选择模板时，将自动选择模板所使用的框架的复选框。 例如，如果选择 **"Web 窗体"** 模板，则选中 **"Web 窗体"** 复选框，但无法清除该模板。

![选择模板](creating-web-projects-in-visual-studio/_static/image21.png)

![添加框架](creating-web-projects-in-visual-studio/_static/image22.png)

可以为模板中未包含的框架选择复选框，以便在创建项目时添加对该框架的支持。 例如，要在选择 MVC 模板时启用 Web 窗体 *.aspx*页面的使用，请选择 **"Web 窗体"** 复选框。 或者，要在使用 Web 窗体模板时启用 MVC，请单击**MVC**复选框。 添加框架可实现设计时和运行时支持。 例如，如果将 MVC 支持添加到 Web 窗体项目，则可以对控制器和视图进行基架。

如果在项目中组合 Web 窗体和 MVC 并在 Web 窗体中启用[友好 URL，](http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx)则可能存在意外的路由问题，其中一个 URL 具有多个可能的目标。 首先定义的路由将优先。 例如`Home`，如果您有控制器和*Home.aspx*页，则如果在`http://contoso.com/home` *RouteConfig.cs*调用`Home``MapRoute``EnableFriendlyUrls``EnableFriendlyUrls``MapRoute`该方法之前调用 该方法，则 URL 将转到*Home.aspx，* 或者，如果之前调用，则相同的 URL 将转到控制器的默认视图。

添加框架不会添加任何示例应用程序功能。 例如，如果在选择 MVC 模板时添加 Web 窗体支持，则不会创建*Default.aspx*主页文件。 仅添加支持框架所需的文件夹、文件和引用。 因此，添加框架不会更改身份验证选项，这些选项由模板创建的示例应用程序中的代码实现。 例如，如果选择"空模板"并添加 Web 窗体或 MVC 支持，则仍将禁用 **"配置身份验证"** 按钮。

以下各节简要描述每个复选框的效果。

### <a name="add-web-forms-support"></a>添加 Web 表单支持

创建空*的应用\_数据和**模型*文件夹和*全局.asax*文件。 这些模板已由空模板以外的所有模板创建，因此选择"Web 窗体"复选框对其他模板没有影响。

默认情况下，Web 窗体模板启用友好 URL，但当您通过选择"Web 窗体"复选框将 Web 窗体支持添加到其他模板时，不会自动启用"友好 URL"。

### <a name="add-mvc-support"></a>添加 MVC 支持

安装 MVC、Razor 和 WebPages NuGet 包，创建空*的应用\_数据*、*控制器*、*模型*和*视图*文件夹，使用*RouteConfig.cs*文件创建*应用\_启动*文件夹，并创建*Global.asax*文件。

### <a name="add-web-api-support"></a>添加 Web API 支持

安装 WebApi 和 Newtonsoft.Json NuGet 包，创建空*的应用程序\_数据*、*控制器*和*模型*文件夹，创建包含*WebApiConfig.cs*文件*的应用程序\_启动*文件夹，并创建*Global.asax*文件。

<a id="auth"></a>
## <a name="authentication-methods"></a>身份验证方法

Visual Studio 2013 为 Web 窗体、MVC 和 Web API 模板提供了多个身份验证选项：

- [无身份验证](#noauth)
- [个人用户帐户](#indauth)（ASP.NET标识，以前称为ASP.NET成员资格）
- [组织帐户](#orgauth)（Windows 服务器活动目录或 Azure 活动目录）
- [窗口身份验证](#winauth)（内联网）

![配置身份验证对话框](creating-web-projects-in-visual-studio/_static/image23.png)

<a id="noauth"></a>

### <a name="no-authentication"></a>无身份验证

如果选择 **"无身份验证"，** 则示例应用程序将不包含用于登录的网页、指示登录者使用的 UI、成员资格数据库的实体类以及成员资格数据库的连接字符串。

<a id="indauth"></a>
### <a name="individual-user-accounts"></a>单个用户帐户

如果选择 **"个人用户帐户**"，则示例应用程序将配置为使用ASP.NET标识（以前称为ASP.NET成员资格）进行用户身份验证。 ASP.NET身份允许用户通过在网站上创建用户名和密码或与 Facebook、Google、微软帐户或 Twitter 等社交提供商登录来注册帐户。 ASP.NET标识中用户配置文件的默认数据存储是 SQL Server LocalDB 数据库，您可以将该数据库部署到生产站点的 SQL Server 或 Azure SQL 数据库。

在 Visual Studio 2013 中，这些功能与 Visual Studio 2012 中的功能相同，但ASP.NET成员资格系统的基础代码已被重写。 新代码库的优点包括：

- 新的成员资格系统基于[OWIN](http://owin.org/)而不是ASP.NET窗体身份验证模块。 这意味着无论您是在 IIS 中使用 Web 窗体还是 MVC，还是自托管 Web API 或 SignalR，您都可以使用相同的身份验证机制。
- 新的成员资格数据库由实体框架代码优先管理，所有表都由可以修改的实体类表示。 这意味着您可以轻松地自定义数据库架构和配置文件相关的 Web UI 以满足您自己的需求，并且可以使用代码优先迁移轻松部署更新。

新的成员资格系统在新模板中自动实现，可以在以 .NET 4.5 或更高版本为目标的任何项目中手动实现。

ASP.NET身份是一个不错的选择，如果你正在创建一个互联网网站，主要是为外部客户。 如果您的组织使用 Active Directory 或 Office 365，并且希望创建一个为员工和业务合作伙伴启用单一登录的项目，则 **"组织帐户"** 选项可能是一个更好的选择。

有关"个人用户帐户"选项的详细信息，请参阅以下资源：

- [www.asp.net/identity](../../../identity/index.md). 有关ASP.NET网站上ASP.NET标识的文档。
- [创建一个ASP.NETMVC 5应用程序与Facebook和谷歌Auth2和开放ID登录](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)。 还演示如何自定义用户配置文件数据。
- [Web API - 外部身份验证服务](../../../web-api/overview/security/external-authentication-services.md)
- [在 Visual Studio 2013 中向ASP.NET应用程序添加外部登录](https://blogs.msdn.com/b/webdev/archive/2013/06/27/adding-external-logins-to-your-asp-net-application-in-visual-studio-2013.aspx)

<a id="orgauth"></a>
### <a name="organizational-accounts"></a>组织帐户

如果选择 **"组织帐户**"，则示例应用程序将配置为使用 Windows 标识基础 （WIF） 根据 Azure 活动目录（Azure AD，包括 Office 365）或 Windows 服务器活动目录中的用户帐户进行身份验证。 有关详细信息，请参阅本主题后面的[组织帐户身份验证选项](#orgauthoptions)。

<a id="winauth"></a>
### <a name="windows-authentication"></a>Windows 身份验证

如果选择**Windows 身份验证**，则示例应用程序将配置为使用 Windows 身份验证 IIS 模块进行身份验证。 应用程序将显示登录到 Windows 但不包括用户注册或登录 UI 的 Active 目录或本地计算机帐户的域和用户 ID。 此选项适用于 Intranet 网站。

或者，您可以通过在[组织帐户下选择"本地"选项](#orgauthonprem)来创建使用 AD 身份验证的 Intranet 站点。 "本地"选项使用 Windows 标识基础 （WIF） 而不是 Windows 身份验证模块。 需要执行一些其他步骤才能设置"本地"选项，但 WIF 启用 Windows 身份验证模块中不可用的功能。 例如，使用 WIF 可以在 Active Directory 和查询目录数据中配置应用程序访问。

<a id="orgauthoptions"></a>
## <a name="organizational-account-authentication-options"></a>组织帐户身份验证选项

**"配置身份验证"** 对话框为 Azure 活动目录（Azure AD，包括 Office 365）或 Windows 服务器活动目录 （AD） 帐户身份验证提供了多个选项：

- [云 - 单个组织](#orgauthsingle)（使用与 Azure AD 的目录集成的 Azure AD 或 AD）
- [云 - 多组织](#orgauthmulti)（使用目录与 Azure AD 集成的 Azure AD 或 AD）
- [内部（AD）](#orgauthonprem)

如果要尝试 Azure AD 选项之一，但尚未拥有帐户，[请单击此处注册 Azure AD 帐户](https://go.microsoft.com/fwlink/?LinkId=309942)。

> [!NOTE]
> 如果选择 Azure AD 选项之一，则项目需要数据库，并且必须登录到 Azure AD 租户的全局管理员帐户。 输入具有 Azure AD 租户管理权限的组织帐户的名称admin@contoso.onmicrosoft.com和密码。
> 
> **不要在登录对话框中输入 Microsoft 帐户的凭据（例如contoso@hotmail.com）。**

<a id="orgauthsingle"></a>
### <a name="cloud---single-organization-authentication"></a>云 - 单一组织身份验证

![单一组织身份验证](creating-web-projects-in-visual-studio/_static/image24.png)

如果要为一个 Azure AD[租户](https://technet.microsoft.com/library/jj573650.aspx)中定义的用户帐户启用身份验证，请选择此选项。 例如，该网站contoso.com，它将提供给 Contoso 公司位于租户contoso.onmicrosoft.com的员工。 您将无法将 Azure AD 配置为允许其他租户的用户访问应用程序。

#### <a name="domain"></a>域

输入要在 中设置应用程序的 Azure AD 域，例如： `contoso.onmicrosoft.com` 如果您有[自定义域](http://www.cloudidentity.com/blog/2013/04/14/adding-a-custom-domain-to-your-windows-azure-ad/)，例如`contoso.com`，`contoso.onmicrosoft.com`可以在此处输入该域。

#### <a name="access-level"></a>访问级别

如果应用程序需要使用图形 API 查询或更新目录信息，请选择**单一登录、读取目录数据**或**单一登录、读取和写入目录数据**。 否则，请选择**单一登录**。 有关详细信息，请参阅[应用程序访问级别](https://msdn.microsoft.com/library/windowsazure/b08d91fa-6a64-4deb-92f4-f5857add9ed8#BKMK_AccessLevels)和使用图形[API 查询 Azure AD](https://msdn.microsoft.com/library/windowsazure/dn151791.aspx)。

#### <a name="application-id-uri"></a>应用程序 ID URI

默认情况下，模板通过将项目名称追加到 Azure AD 域，为您创建应用程序 ID URI。 例如，如果项目名称为`Example`，并且域为`contoso.onmicrosoft.com`，则应用程序 ID URI`https://contoso.onmicrosoft.com/Example`变为 。 如果要手动指定应用程序 ID URI，请展开 **"更多选项"** 部分，并在文本框中输入应用程序 ID URI。 应用程序 ID URI 必须`https://`以 开头。

默认情况下，如果已在 Azure AD 中预配的应用程序具有与 Visual Studio 用于项目的应用程序 ID URI 相同的应用程序 ID URI，则项目将连接到现有应用程序，而不是预配新应用程序。 如果希望在这种情况下预配新应用程序，**请清除"覆盖应用程序条目"（如果具有相同 ID 的应用程序条目已存在**）复选框。

如果清除 **"覆盖**"复选框，并且 Visual Studio 查找具有相同应用程序 ID URI 的现有应用程序，则通过将数字追加到要使用的 URI 来创建新 URI。 例如，假设项目名称为`Example`，您将文本框留空，清除**覆盖**复选框，Azure AD 租户已具有带有 URI`https://contoso.onmicrosoft.com/Example`的应用程序。 在这种情况下，将预配一个新应用程序，并设置应用程序 ID URI，如`https://contoso.onmicrosoft.com/Example_20130619330903`。

#### <a name="provisioning-the-application-in-azure-ad"></a>在 Azure AD 中预配应用程序

为了在 Azure AD 中预配应用程序或将项目连接到现有应用程序，Visual Studio 需要域的全局管理员的凭据。 在"**配置身份验证**"对话框中单击 **"确定"** 时，系统会提示您输入您指定的域的全局管理员的用户名和密码。 稍后，当您单击 **"新建ASP.NET项目**"对话框中**创建项目**时，Visual Studio 在 Azure AD 中提供应用程序。 请注意，作为此过程的一部分，Visual Studio 会在 Web.config 文件中嵌入客户端机密值，该文件在创建一年后过期。

有关如何创建使用**云 - 单一组织**身份验证的应用程序的信息，请参阅以下资源：

- [Azure 身份验证](../2012/windows-azure-authentication.md)
- [使用 Azure AD 将登录名添加到 Web 应用程序中](https://msdn.microsoft.com/library/windowsazure/dn151790.aspx)
- [借助 Azure Active Directory 开发 ASP.NET 应用](../../../identity/overview/getting-started/developing-aspnet-apps-with-windows-azure-active-directory.md)
- [使用 Azure AD 和 Microsoft OWIN 组件ASP.NET Web API 安全](https://msdn.microsoft.com/magazine/dn463788.aspx)

Visual Studio 2013 的教程尚未更新;教程指导您手动执行的一些操作在 Visual Studio 2013 中是自动化的。

<a id="orgauthmulti"></a>
### <a name="cloud---multi-organization-authentication"></a>云 - 多组织身份验证

![多个组织身份验证](creating-web-projects-in-visual-studio/_static/image25.png)

如果要为多个 Azure AD[租户](https://technet.microsoft.com/library/jj573650.aspx)中定义的用户帐户启用身份验证，请选择此选项。 例如，该站点contoso.com，它将提供给 contoso 公司位于contoso.onmicrosoft.com租户的员工以及法布里卡姆公司fabrikam.onmicrosoft.com租户的员工。

输入的设置和应用程序预配步骤类似于[单个组织身份验证](#orgauthsingle)。

有关如何创建使用**云 - 多组织**身份验证的应用程序的信息，请参阅以下资源：

- [轻松 Web 应用与 Azure 活动&amp;目录集成，ASP.NET活动目录团队博客上的可视化工作室](https://blogs.msdn.com/b/active_directory_team_blog/archive/2013/06/26/improved-windows-azure-active-directory-integration-with-asp-net-amp-visual-studio.aspx)。
- [使用 Azure AD 教程开发多租户 Web 应用程序](https://msdn.microsoft.com/library/windowsazure/dn151789.aspx)。 本教程尚未更新为 Visual Studio 2013;本教程指导您手动执行的一些操作在 Visual Studio 2013 中是自动化的。
- [您必须在应用程序ASP.NET使用自己的多个组织注册，然后才能登录](http://www.cloudidentity.com/blog/2013/10/26/you-have-to-sign-up-with-your-own-multiple-organizations-asp-net-app-before-you-can-sign-in/)。 Vittorio Bertocci 的博客，解释如何解决人们在创建使用多组织身份验证的项目时遇到的常见问题。

<a id="orgauthonprem"></a>
### <a name="on-premises-organizational-authentication"></a>本地组织身份验证

![本地组织身份验证](creating-web-projects-in-visual-studio/_static/image26.png)

如果要为 Windows 服务器活动目录 （AD） 中定义的用户帐户启用身份验证，并且不想使用 Azure AD，请选择此选项。 您可以使用此选项创建 Intranet 站点或 Internet 站点。 对于 Internet 站点，请使用活动目录联合服务 （ADFS） 提供对 AD 的访问。 有关详细信息，请参阅在[Visual Studio 2013 中使用具有ASP.NET的本地组织身份验证选项 （ADFS）。](http://www.cloudidentity.com/blog/2014/02/12/use-the-on-premises-organizational-authentication-option-adfs-with-asp-net-in-visual-studio-2013/)

对于 Intranet 站点，作为替代方法，您可以选择[Windows 身份验证](#winauth)而不是此选项。 对于 Windows 身份验证选项，您不必提供元数据文档 URL。 但是，Windows 身份验证无法控制活动目录中的应用程序访问或查询目录数据。

#### <a name="on-premises-authority"></a>内部管理局

输入指向元数据文档的 URL。 元数据文档包含权限的坐标。 应用程序将使用这些坐标来驱动 Web 登录流。

#### <a name="application-id-uri"></a>应用程序 ID URI

提供 AD 可用于标识此应用程序的唯一 URI，或留空以让 Visual Studio 创建一个。

<a id="nextsteps"></a>
## <a name="next-steps"></a>后续步骤

本文档为在 Visual Studio 2013 中创建新ASP.NET Web 项目提供了一些基本帮助。 有关将 Visual Studio 用于 Web 开发的详细信息[https://www.asp.net/visual-studio/](../../index.md)，请参阅。

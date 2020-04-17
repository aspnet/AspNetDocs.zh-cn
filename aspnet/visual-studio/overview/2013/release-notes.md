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
# <a name="aspnet-and-web-tools-for-visual-studio-2013-release-notes"></a>适用于 Visual Studio 2013 的 ASP.NET 和 Web 工具发行说明

由[微软](https://github.com/microsoft)

> 本文档介绍了 2013 年可视化工作室的ASP.NET和网络工具的发布。

## <a name="contents"></a>目录

- [安装说明](#TOC1)
- [文档](#TOC2)
- [软件要求](#TOC4)

### <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-2013"></a>2013年可视化工作室ASP.NET和网络工具的新功能

- [一ASP.NET](#TOC6)
- [新的 Web 项目体验](#newproj)
- [ASP.NET脚手架](#scaffold)
- [浏览器链接](#browser-link)
- [可视化工作室 Web 编辑器增强功能](#web-editor)
- [Visual Studio 中的 Azure 应用服务 Web 应用支持](#waws)
- [Web 发布增强功能](#publish)
- [NuGet 2.7](#nuget)
- [ASP.NET Web 表单](#TOC9)
- [ASP.NET MVC 5](#TOC10)
- [ASP.NET Web API 2](#TOC11)
- [ASP.NET SignalR](#TOC13)
- [ASP.NET 标识](#TOC8)
- [Microsoft OWIN 组件](#TOC7)
- [Entity Framework 6](#ef6)
- [ASP.NET剃刀 3](#TOC14)
- [ASP.NET应用挂起](#TOC15)
- [已知问题和重大更改](#knownissues)

<a id="TOC1"></a>
## <a name="installation-notes"></a>安装说明

ASP.NET和Web工具为可视化工作室2013捆绑在主安装程序，可以[在这里](https://www.asp.net/downloads)下载。

<a id="TOC2"></a>
## <a name="documentation"></a>文档

有关 visual Studio 2013 的ASP.NET和 Web 工具的教程和其他信息可从[ASP.NET网站](https://www.asp.net/)获得。

<a id="TOC4"></a>
## <a name="software-requirements"></a>软件要求

ASP.NET和网络工具需要可视化工作室 2013。

<a id="TOC5"></a>
## <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-2013"></a>2013年可视化工作室ASP.NET和网络工具的新功能

以下各节介绍版本中引入的功能。

<a id="TOC6"></a>
## <a name="one-aspnet"></a>一ASP.NET

随着 Visual Studio 2013 的发布，我们朝着统一使用ASP.NET技术的经验迈出了一步，以便您可以轻松混合和匹配所需的技术。 例如，可以使用 MVC 启动项目，并在以后轻松地将 Web 窗体页添加到项目，或在 Web 窗体项目中基架 Web API 中。 一ASP.NET就是让你作为开发人员更容易在ASP.NET中做你喜欢的事情。 无论您选择何种技术，您都可以确信自己正在构建"一ASP.NET"的可信底层框架。

<a id="newproj"></a>
## <a name="new-web-project-experience"></a>新的 Web 项目体验

我们在 Visual Studio 2013 中增强了创建新 Web 项目的经验。 在 **"新建ASP.NET Web 项目**"对话框中，您可以选择所需的项目类型、配置任何技术组合（Web 窗体、MVC、Web API）、配置身份验证选项以及添加单元测试项目。

![新ASP.NET项目](release-notes/_static/image1.png)

新的对话框使您能够更改许多模板的默认身份验证选项。 例如，在创建ASP.NET Web 窗体项目时，您可以选择以下任一选项：

- 无身份验证
- 个人用户帐户（ASP.NET会员身份或社交提供商登录）
- 组织帐户（互联网应用程序中的活动目录）
- Windows 身份验证（Intranet 应用程序中的活动目录）

![身份验证选项](release-notes/_static/image2.png)

有关创建 Web 项目的新流程的详细信息，请参阅在[Visual Studio 2013 中创建ASP.NET Web 项目](creating-web-projects-in-visual-studio.md)。 有关新身份验证选项的详细信息，请参阅本文档后面的[ASP.NET标识](#TOC8)。

<a id="scaffold"></a>
## <a name="aspnet-scaffolding"></a>ASP.NET脚手架

ASP.NET基架是ASP.NET Web 应用程序的代码生成框架。 它可以轻松地向与数据模型交互的项目添加样板代码。

在 Visual Studio 的早期版本中，基架仅限于ASP.NET MVC 项目。 借助 Visual Studio 2013，您现在可以对任何ASP.NET项目（包括 Web 窗体）使用基架。 Visual Studio 2013 目前不支持为 Web 窗体项目生成页面，但您仍可以通过向项目添加 MVC 依赖项来使用 Web 窗体的脚手架。 将在将来的更新中添加对生成 Web 窗体页面的支持。

使用基架时，我们确保在项目中安装了所有必需的依赖项。 例如，如果从ASP.NET Web 窗体项目开始，然后使用基架添加 Web API 控制器，则所需的 NuGet 包和引用将自动添加到项目中。

要将 MVC 基架添加到 Web 窗体项目，请添加新**的脚手架项**，并在对话框窗口中选择**MVC 5 依赖项**。 基架 MVC 有两个选项;最小和完整。 如果选择"最小"，则只有 ASP.NET MVC 的 NuGet 包和引用添加到项目中。 如果选择"完整"选项，则添加最小依赖项以及 MVC 项目所需的内容文件。

支持基架异步控制器使用实体框架 6 中的新异步功能。

有关详细信息和教程，请参阅[ASP.NET脚手架概述](aspnet-scaffolding-overview.md)。

<a id="browser-link"></a>
## <a name="browser-link--signalr-channel-between-browser-and-visual-studio"></a>浏览器链接 + 浏览器和可视化工作室之间的信号R通道

新的[浏览器链接](using-browser-link.md)功能允许您将多个浏览器连接到 Visual Studio，并通过单击工具栏中的按钮刷新所有浏览器。 您可以将多个浏览器连接到开发站点（包括移动仿真程序），然后单击刷新以同时刷新所有浏览器。 浏览器链接还公开 API，使开发人员能够编写浏览器链接扩展。

![](release-notes/_static/image3.png)

通过使开发人员能够利用浏览器链接 API，可以创建非常高级的方案，这些方案跨越 Visual Studio 和任何已连接的浏览器之间的边界。 Web Essentials 利用 API 在 Visual Studio 和浏览器的开发人员工具、远程控制移动仿真器等之间创建集成体验。

<a id="web-editor"></a>
## <a name="visual-studio-web-editor-enhancements"></a>可视化工作室 Web 编辑器增强功能

Visual Studio 2013 包括用于 Web 应用程序中 Razor 文件和 HTML 文件的新 HTML 编辑器。 新的 HTML 编辑器提供基于 HTML5 的单个统一架构。 它有自动大括号完成，jQuery UI和AngularJS属性IntelliSense，属性IntelliSense分组，ID和类名Intellisense，和其他改进，包括更好的性能，格式和智能标签。

以下屏幕截图演示如何在 HTML 编辑器中使用 Bootstrap 属性 IntelliSense。

![HTML 编辑器中的感知](release-notes/_static/image4.png)

Visual Studio 2013 还附带了内置的咖啡脚本和 LESS 编辑器。 LESS 编辑器附带了 CSS 编辑器中的所有很酷的功能，并具有针对@import链中所有 LESS 文档中的变量和混合值的特定 Intellisense。

<a id="waws"></a>
## <a name="azure-app-service-web-apps-support-in-visual-studio"></a>Visual Studio 中的 Azure 应用服务 Web 应用支持

在 Visual Studio 2013 中，使用用于 .NET 2.2 的 Azure SDK，可以使用**服务器资源管理器**直接与远程 Web 应用进行交互。 您可以登录到 Azure 帐户、创建新的 Web 应用、配置应用、查看实时日志等。 SDK 2.2 发布后不久，您将能够在 Azure 中远程在调试模式下运行。 安装 .NET 的 Azure SDK 当前版本时，Azure 应用服务 Web 应用的大多数新功能在 Visual Studio 2012 中也起作用。

有关更多信息，请参见以下资源：

- [在 Azure 应用服务中创建 ASP.NET Web 应用](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/)
- [使用 Visual Studio 对 Azure 应用服务中的 Web 应用进行故障排除](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/)

<a id="publish"></a>
## <a name="web-publish-enhancements"></a>Web 发布增强功能

Visual Studio 2013 包括新的和增强的 Web 发布功能。 下面是其中几个示例：

- 轻松[自动进行 Web.config 文件加密](https://go.microsoft.com/fwlink/?LinkId=325529)。 （此链接和以下两个指向 MSDN 上的文档，这些文档可能直到 10 月 17 日深夜才可用。
- 在[部署期间轻松自动使应用程序脱机](https://go.microsoft.com/fwlink/?LinkId=325530)。
- 将 Web 部署配置为[使用文件校验和，而不是上次更改的日期](https://go.microsoft.com/fwlink/?LinkId=325531)，以确定应复制到服务器的文件。
- 使用 FTP 或文件系统发布方法以及 Web 部署时，快速发布单个选定文件（包括 Web.config）。

有关ASP.NET Web 部署的详细信息，请参阅[ASP.NET网站](https://go.microsoft.com/fwlink/?LinkId=322027)。

<a id="nuget"></a>
## <a name="nuget-27"></a>NuGet 2.7

NuGet 2.7 包含一组丰富的新功能，在[NuGet 2.7 发行说明](http://docs.nuget.org/docs/release-notes/nuget-2.7)中对此进行了详细介绍。

此版本的 NuGet 还无需为 NuGet 的包还原功能提供下载包的明确同意。 现在通过安装 NuGet 授予同意（以及 NuGet 首选项对话框中的关联复选框）。 现在，默认情况下，包还原只是工作。

<a id="TOC9"></a>
## <a name="aspnet-web-forms"></a>ASP.NET Web 窗体

### <a name="one-aspnet"></a>一ASP.NET

Web 窗体项目模板与新 one ASP.NET 体验无缝集成。 您可以将 MVC 和 Web API 支持添加到 Web 窗体项目中，并且可以使用"一ASP.NET项目创建向导配置身份验证。 有关详细信息，请参阅在[Visual Studio 2013 中创建ASP.NET Web 项目](creating-web-projects-in-visual-studio.md)。

### <a name="aspnet-identity"></a>ASP.NET 标识

Web 窗体项目模板支持新的ASP.NET标识框架。 此外，模板现在支持创建 Web 窗体 Intranet 项目。 有关详细信息，请参阅在**Visual Studio 2013 中创建ASP.NET Web 项目的**[身份验证方法](creating-web-projects-in-visual-studio.md#auth)。

### <a name="bootstrap"></a>Bootstrap

Web 窗体模板使用[Bootstrap](http://twitter.github.io/bootstrap/)提供时尚且响应迅速的外观，让您轻松自定义。 有关详细信息，请参阅[Visual Studio 2013 Web 项目模板中的 Bootstrap。](creating-web-projects-in-visual-studio.md#bootstrap)

<a id="TOC10"></a>
## <a name="aspnet-mvc-5"></a>ASP.NET MVC 5

### <a name="one-aspnet"></a>一ASP.NET

Web MVC 项目模板与新一ASP.NET体验无缝集成。 您可以使用"一ASP.NET项目创建向导自定义 MVC 项目并配置身份验证。 ASP.NET MVC 5 的入门教程可以在[ASP.NET MVC 5 入门](../../../mvc/overview/getting-started/introduction/getting-started.md)中找到。

有关将 MVC 4 项目升级到 MVC 5 的信息，请参阅[如何将ASP.NET MVC 4 和 Web API 项目升级到ASP.NET MVC 5 和 Web API 2](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md)。

### <a name="aspnet-identity"></a>ASP.NET 标识

MVC 项目模板已更新，用于ASP.NET标识进行身份验证和标识管理。 一个教程，包括Facebook和谷歌认证和新的会员API可以在[创建一个ASP.NETMVC 5应用程序与Facebook和谷歌OAuth2和OpenID登录](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)，[并创建一个ASP.NETMVC应用程序与auth和SQL DB，并部署到Azure应用程序服务](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/)。

### <a name="bootstrap"></a>Bootstrap

MVC 项目模板已更新，可使用[Bootstrap](http://getbootstrap.com/)提供时尚且响应迅速的外观，让您轻松自定义。 有关详细信息，请参阅[Visual Studio 2013 Web 项目模板中的 Bootstrap。](creating-web-projects-in-visual-studio.md#bootstrap)

### <a name="authentication-filters"></a>身份验证筛选器

身份验证筛选器是 ASP.NET MVC 中一种新型筛选器，在 ASP.NET MVC 管道中的授权筛选器之前运行，允许您为所有控制器指定每个操作、每个控制器或全局的身份验证逻辑。 身份验证筛选器处理请求中的凭据并提供相应的主体。 身份验证筛选器还可以添加身份验证质询以响应未经授权的请求。

### <a name="filter-overrides"></a>筛选器覆盖

现在，可以通过指定覆盖筛选器来覆盖应用于给定操作方法或控制器的筛选器。 覆盖筛选器指定一组不应为给定作用域（操作或控制器）运行的筛选器类型。 这允许您配置全局应用的筛选器，但随后排除某些全局筛选器应用于特定操作或控制器。

### <a name="attribute-routing"></a>属性路由

ASP.NET MVC 现在支持属性路由，这要归功于[http://attributerouting.net](http://attributerouting.net)Tim McCall（作者）的贡献。 使用属性路由，您可以通过对操作和控制器进行说明来指定路由。

<a id="TOC11"></a>
## <a name="aspnet-web-api-2"></a>ASP.NET Web API 2

### <a name="attribute-routing"></a>属性路由

ASP.NET Web API 现在支持属性路由，这要归功于[http://attributerouting.net](http://attributerouting.net)Tim McCall（作者）的贡献。 使用属性路由，您可以通过指定操作和控制器来指定 Web API 路由，如下所示：

[!code-csharp[Main](release-notes/samples/sample1.cs)]

属性路由使您能够对 Web API 中的 URI 进行更多控制。 例如，您可以使用单个 API 控制器轻松定义资源层次结构：

[!code-csharp[Main](release-notes/samples/sample2.cs)]

属性路由还提供用于指定可选参数、默认值和路由约束的便捷语法：

[!code-csharp[Main](release-notes/samples/sample3.cs)]

有关属性路由的详细信息，请参阅[Web API 2 中的属性路由](../../../web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2.md)。

### <a name="oauth-20"></a>OAuth 2.0

Web API 和单页应用程序项目模板现在支持使用 OAuth 2.0 进行授权。 OAuth 2.0 是一个用于授权客户端访问受保护资源的框架。 它适用于各种客户端，包括浏览器和移动设备。

对 OAuth 2.0 的支持基于 Microsoft OWIN 组件为承载身份验证和实现授权服务器角色而提供的新安全中间件。 或者，可以使用组织授权服务器（如 Windows Server 2012 R2 中的 Azure 活动目录或 ADFS）授权客户端。

### <a name="odata-improvements"></a>O数据改进

**支持$select、$expand、$batch和$value**

ASP.NET Web API OData 现在完全支持$select、$expand和$value。 您还可以使用$batch请求批处理和处理更改集。

$select和$expand选项允许您更改从 OData 终结点返回的数据的形状。 有关详细信息，请参阅在[Web API OData 中介绍$select和$expand支持](../../../web-api/overview/odata-support-in-aspnet-web-api/using-select-expand-and-value.md)。

**提高可扩展性**

OData for 物质现在可扩展。 您可以添加 Atom 条目元数据、支持命名流和媒体链接条目、添加实例注释以及自定义链接的生成方式。

**无类型支持**

现在，您可以构建 OData 服务，而无需为实体类型定义 CLR 类型。 相反，您的 OData 控制器可以获取或返回**IEdmObject**的实例 ，这是用于序列化/反序列化的 OData 实例。

**重用现有模型**

如果您已有现有的实体数据模型 （EDM），现在可以直接重用它，而不必构建新的实体数据模型。 例如，如果您使用的是实体框架，则可以使用 EF 为您生成的 EDM。

### <a name="request-batching"></a>请求批处理

请求批处理将多个操作合并到单个 HTTP POST 请求中，以减少网络流量并提供更顺畅、更不健谈的用户界面。 ASP.NET Web API 现在支持几种请求批处理策略：

- 使用 OData 服务$batch终结点。
- 将多个请求打包到单个 MIME 多部分请求中。
- 使用自定义批处理格式。

要启用请求批处理，只需将具有批处理处理程序的路由添加到 Web API 配置中：

[!code-csharp[Main](release-notes/samples/sample4.cs)]

您还可以控制请求或按顺序执行，还是按任何顺序执行。

### <a name="portable-aspnet-web-api-client"></a>可移植ASP.NET Web API 客户端

现在，可以使用 ASP.NET Web API 客户端创建跨 Windows 应用商店和 Windows Phone 8 应用程序的便携式类库。 您还可以创建可在客户端和服务器之间共享的可移植的要件。

### <a name="improved-testability"></a>提高可测试性

Web API 2 使单元测试 API 控制器变得更加容易。 只需使用请求消息和配置实例化 API 控制器，然后调用要测试的操作方法。 对于执行链接生成的操作方法，也很容易模拟**UrlHelper**类。

### <a name="ihttpactionresult"></a>IHttpAction 结果

现在，您可以实现 IHttpActionResult 来封装 Web API 操作方法的结果。 从 Web API 操作方法返回的 IHttpActionResult 由 ASP.NET Web API 运行时执行，以生成产生的响应消息。 可以从任何 Web API 操作返回 IHttpActionResult，以简化 Web API 实现单元测试。 为方便起见，一些 IHttpActionResult 实现在开箱即用，包括用于返回特定状态代码、格式化内容或内容协商响应的结果。

### <a name="httprequestcontext"></a>HttpRequestContext

新的**HttpRequestContext**跟踪与请求关联的任何状态，但无法立即从请求中获取。 例如，可以使用**HttpRequestContext**获取路由数据、与请求关联的主体、客户端证书 **、UrlHelper**和虚拟路径根。 您可以轻松地为单元测试目的创建**HttpRequestContext。**

由于请求的主体随请求一起流动，而不是依赖于**Thread.CurrentThe，** 因此主体现在在请求在 Web API 管道中时在请求的整个生存期内可用。

### <a name="cors"></a>CORS

多亏了布罗克·艾伦的另一个巨大贡献，ASP.NET现在完全支持跨原请求共享 （CORS）。

浏览器安全性将阻止网页向另一个域发出 AJAX 请求。 [CORS](http://www.w3.org/TR/cors/)是一种 W3C 标准，允许服务器放松同源策略。 使用 CORS，服务器可以显式允许某些跨域请求，同时拒绝另一些跨域请求。

Web API 2 现在支持 CORS，包括自动处理预检请求。 有关详细信息，请参阅在[web API 中启用跨源请求ASP.NET](../../../web-api/overview/security/enabling-cross-origin-requests-in-web-api.md)。

### <a name="authentication-filters"></a>身份验证筛选器

身份验证筛选器是 web API 中ASP.NET一种新型筛选器，在ASP.NET Web API 管道中授权筛选器之前运行，允许您为所有控制器指定每个操作、每个控制器或全局的身份验证逻辑。 身份验证筛选器处理请求中的凭据并提供相应的主体。 身份验证筛选器还可以添加身份验证质询以响应未经授权的请求。

### <a name="filter-overrides"></a>筛选器覆盖

现在，可以通过指定重写筛选器来覆盖应用于给定操作方法或控制器的筛选器。 覆盖筛选器指定一组不应为给定作用域（操作或控制器）运行的筛选器类型。 这允许您添加全局筛选器，但随后从特定操作或控制器中排除某些筛选器。

### <a name="owin-integration"></a>OWIN 集成

ASP.NET Web API 现在完全支持 OWIN，可以在任何支持 OWIN 的主机上运行。 还包括一个**主机身份验证筛选器**，它提供与 OWIN 身份验证系统的集成。

通过 OWIN 集成，您可以与其他 OWIN 中间件（如 SignalR）一起，在您自己的进程中自行托管 Web API。 有关详细信息，请参阅使用[OWIN ASP.NET Web API 进行自托管](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)。

<a id="TOC13"></a>
## <a name="aspnet-signalr-20"></a>ASP.NET信号R 2.0

以下各节介绍 SignalR 2.0 的功能。

- [基于 OWIN 构建](#builtonowin)
- [地图集线和地图连接现在是映射信号R](#MapSignalR)
- [跨域支持](#crossdomain)
- [通过单点触控和单体机器人支持 iOS 和 Android](#mobile)
- [便携式 .NET 客户端](#portable)
- [新的自主机包](#selfhost)
- [向后兼容的服务器支持](#backwardcompat)
- [已删除对 .NET 4.0 的服务器支持](#remove40)
- [将消息发送到客户端和组列表](#messagelist)
- [向特定用户发送消息](#sendtouser)
- [更好的错误处理支持](#errorhandling)
- [更简便的集线器单元测试](#unittesting)
- [JavaScript 错误处理](#javascripterror)

有关如何将现有的 1.x 项目升级到 SignalR 2.0 的示例，请参阅[升级 SignalR 1.x 项目](../../../signalr/overview/releases/upgrading-signalr-1x-projects-to-20.md)。

<a id="builtonowin"></a>
### <a name="built-on-owin"></a>基于 OWIN 构建

SignalR 2.0 完全基于[OWIN（.NET 的开放 Web 界面）](http://owin.org/)构建。 此更改使 SignalR 的设置过程在 Web 托管和自托管 SignalR 应用程序之间更加一致，但还需要多次 API 更改。

<a id="MapSignalR"></a>

### <a name="maphubs-and-mapconnection-are-now-mapsignalr"></a>地图集线和地图连接现在是映射信号R

为了与 OWIN 标准兼容，这些方法已重命名为`MapSignalR`。 `MapSignalR`在没有参数的情况下调用将映射所有中心（如`MapHubs`版本 1.x）;映射单个**持久连接**对象，将连接类型指定为类型参数，并将连接的 URL 扩展作为第一个参数。

该方法`MapSignalR`在 Owin 启动类中调用。 Visual Studio 2013 包含 Owin 启动类的新模板;要使用此模板，请使用以下操作：

1. 右键单击项目
2. 选择 **"添加****"，新项目...**
3. 选择**Owin 启动类**。 Startup.cs命名**新类。**

在**Web 应用程序中，** 包含该方法`MapSignalR`的 Owin 启动类随后使用 Web.Config 文件的应用程序设置节点中的条目添加到 Owin 的启动过程中，如下所示。

在**自托管应用程序中**，启动类作为`WebApp.Start`方法的类型参数传递。

**映射 SignalR 1.x 中的集线器和连接（来自 Web 应用程序中的全局应用程序文件）：** 

[!code-csharp[Main](release-notes/samples/sample5.cs)]

**映射 SignalR 2.0 中的集线器和连接（来自 Owin 启动类文件）：** 

[!code-csharp[Main](release-notes/samples/sample6.cs)]

在**自托管应用程序中**，启动类作为`WebApp.Start`方法的类型参数传递，如下所示。

[!code-csharp[Main](release-notes/samples/sample7.cs)]

<a id="crossdomain"></a>

### <a name="cross-domain-support"></a>跨域支持

在 SignalR 1.x 中，跨域请求由单个启用CrossDomain 标志控制。 此标志同时控制 JSONP 和 CORS 请求。 为了更灵活，所有 CORS 支持都从 SignalR 的服务器组件中删除（如果检测到浏览器支持它，JavaScript 客户端仍通常使用 CORS），并且新的 OWIN 中间件已可用于支持这些方案。

在 SignalR 2.0 中，如果客户端上需要 JSONP（以支持旧浏览器中的跨域请求），则需要通过在`EnableJSONP``HubConfiguration`对象`true`上设置为 （如下所示）显式启用它。 默认情况下禁用 JSONP，因为它的安全性低于 CORS。

要在 SignalR 2.0 中添加新的 CORS`Microsoft.Owin.Cors`中间件，请将库添加到`UseCors`项目中，并在 SignalR 中间件之前调用，如下节所示。

**将 Microsoft.Owin.Cors 添加到您的项目**：要安装此库，请在包管理器控制台中运行以下命令：

[!code-powershell[Main](release-notes/samples/sample8.ps1)]

此命令会将包的 2.0.0 版本添加到项目中。

**调用使用参数**

以下代码段演示如何在 SignalR 1.x 和 2.0 中实现跨域连接。

**在 SignalR 1.x 中实现跨域请求（来自全局应用程序文件）**

[!code-csharp[Main](release-notes/samples/sample9.cs)]

**在 SignalR 2.0 中实现跨域请求（来自 C# 代码文件）**

以下代码演示如何在 SignalR 2.0 项目中启用 CORS 或 JSONP。 此代码示例使用`Map``RunSignalR`而不是`MapSignalR`，以便 CORS 中间件仅运行需要 CORS 支持的 SignalR 请求（而不是针对 中`MapSignalR`指定的路径上的所有流量）。`Map`还可用于需要为特定 URL 前缀运行的任何其他中间件，而不是整个应用程序。

[!code-csharp[Main](release-notes/samples/sample10.cs)]

<a id="mobile"></a>

### <a name="ios-and-android-support-via-monotouch-and-monodroid"></a>通过单点触控和单体机器人支持 iOS 和 Android

已使用[Xamarin 库中](https://xamarin.com/)的 MonoTouch 和 MonoDroid 组件为 iOS 和 Android 客户端添加了支持。 有关如何使用它们的详细信息，请参阅[使用 Xamarin 组件](https://github.com/SignalR/SignalR/wiki/Building-Mono.Mobile.sln)。 当 SignalR RTW 版本可用时，这些组件将在[Xamarin 存储](https://store.xamarin.com/)中可用。

<a id="portable"></a>• 可移植 .NET 客户端

为了更好地促进跨平台开发，Silverlight、WinRT 和 Windows Phone 客户端已替换为支持以下平台的单个便携式 .NET 客户端：

- 净 4.5
- Silverlight 5
- WinRT （.NET 用于 Windows 应用商店应用）
- Windows Phone 8

<a id="selfhost"></a>

### <a name="new-self-host-package"></a>新的自主机包

现在有一个 NuGet 包，以便更轻松地开始使用 SignalR 自主机（托管在进程或其他应用程序中的 SignalR 应用程序，而不是托管在 Web 服务器中）。 要升级使用 SignalR 1.x 构建的自主机项目，请删除 Microsoft.AspNet.SignalR.Owin 包，然后添加 Microsoft.AspNet.SignalR.SelfHost 包。 有关开始使用自主机包的详细信息，请参阅[教程：SignalR 自主机](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)。

<a id="backwardcompat"></a>

### <a name="backward-compatible-server-support"></a>向后兼容的服务器支持

在早期版本的 SignalR 中，客户端和服务器中使用的 SignalR 包版本需要相同。 为了支持难以更新的粗客户端应用程序，SignalR 2.0 现在支持使用较新的服务器版本与较旧的客户端。 **注意：SignalR 2.0 不支持使用较旧版本的较旧客户端构建的服务器。**

<a id="remove40"></a>

### <a name="removed-server-support-for-net-40"></a>已删除对 .NET 4.0 的服务器支持

SignalR 2.0 已放弃对服务器与 .NET 4.0 的互操作性的支持。 .NET 4.5 必须与 SignalR 2.0 服务器一起使用。 信号R 2.0 仍有 .NET 4.0 客户端。

<a id="messagelist"></a>

### <a name="sending-a-message-to-a-list-of-clients-and-groups"></a>将消息发送到客户端和组列表

在 SignalR 2.0 中，可以使用客户端和组 IT 的列表发送消息。 以下代码段演示如何执行此操作。

**使用持久连接将消息发送到客户端和组的列表**

[!code-csharp[Main](release-notes/samples/sample11.cs)]

**使用中心向客户端和组列表发送消息**

[!code-csharp[Main](release-notes/samples/sample12.cs)]

<a id="sendtouser"></a>

### <a name="sending-a-message-to-a-specific-user"></a>向特定用户发送消息

此功能允许用户通过新接口 IUserIdProvider 指定用户 Id 基于 IRequest 的内容：

**IUserId提供程序接口**

[!code-csharp[Main](release-notes/samples/sample13.cs)]

默认情况下，将有一个使用用户IPrincipal.Identity.Name作为用户名的实现。

在集线器中，您可以通过新的 API 向这些用户发送消息：

**使用客户端.用户 API**

[!code-csharp[Main](release-notes/samples/sample14.cs)]

<a id="errorhandling"></a>

### <a name="better-error-handling-support"></a>更好的错误处理支持

用户现在可以从任何中心调用中引发**HubException。** **HubException**的构造函数可以获取字符串消息和对象额外的错误数据。 SignalR 将自动序列化异常并将其发送到客户端，其中它将用于拒绝/拒绝中心方法调用。

**显示详细的集线器异常**设置与**HubException**被发送回客户端无关;它总是发送。

**显示向客户端发送 Hubexception 的服务器端代码**

[!code-csharp[Main](release-notes/samples/sample15.cs)]

**显示响应从服务器发送的 HubException 的 JavaScript 客户端代码**

[!code-html[Main](release-notes/samples/sample16.html)]

**.NET 客户端代码，用于响应从服务器发送的 HubException**

[!code-csharp[Main](release-notes/samples/sample17.cs)]

<a id="unittesting"></a>

### <a name="easier-unit-testing-of-hubs"></a>更简便的集线器单元测试

SignalR 2.0 包括一`IHubCallerConnectionContext`个在集线器上调用的接口，该接口使创建模拟客户端调用变得更加容易。 以下代码段演示使用此接口与流行的测试工具[xUnit.net](https://github.com/xunit/xunit)和[moq](https://code.google.com/p/moq/)。

**带xUnit.net的单元测试信号R**

[!code-csharp[Main](release-notes/samples/sample18.cs)]

**使用 moq 进行单元测试信号R**

[!code-csharp[Main](release-notes/samples/sample19.cs)]

<a id="javascripterror"></a>

### <a name="javascript-error-handling"></a>JavaScript 错误处理

在 SignalR 2.0 中，所有 JavaScript 错误处理回调返回 JavaScript 错误对象，而不是原始字符串。 这允许 SignalR 将更丰富的信息流向错误处理程序。 可以从错误的`source`属性中获取内部异常。

**处理 Start.Fail 异常的 JavaScript 客户端代码**

[!code-javascript[Main](release-notes/samples/sample20.js)]

<a id="TOC8"></a>
## <a name="aspnet-identity"></a>ASP.NET 标识

### <a name="new-aspnet-membership-system"></a>新的ASP.NET会员制

ASP.NET身份是ASP.NET应用程序的新成员资格系统。 ASP.NET标识使用户特定的配置文件数据与应用程序数据集成变得容易。 ASP.NET标识还允许您为应用程序中的用户配置文件选择持久性模型。 你可以将数据存储在 SQL Server 数据库或其他数据存储中，包括 Azure 存储表等 NoSQL 数据存储。 有关详细信息，请参阅**可视化工作室 2013 中创建ASP.NET Web 项目的**[单个用户帐户](creating-web-projects-in-visual-studio.md#indauth)。

### <a name="claims-based-authentication"></a>基于声明的身份验证

ASP.NET现在支持基于声明的身份验证，其中用户的身份表示为来自受信任颁发者的一组声明。 用户可以使用应用程序数据库中维护的用户名和密码进行身份验证，或使用社交身份提供商（例如：微软帐户、Facebook、Google、Twitter），或者通过 Azure 活动目录或活动目录联合服务 （ADFS） 使用组织帐户。

### <a name="integration-with-azure-active-directory-and-windows-server-active-directory"></a>与 Azure 活动目录和 Windows 服务器活动目录集成

现在，您可以创建ASP.NET使用 Azure 活动目录或 Windows 服务器活动目录 （AD） 进行身份验证的项目。 有关详细信息，请参阅在**Visual Studio 2013 中创建ASP.NET Web 项目的**[组织帐户](creating-web-projects-in-visual-studio.md#orgauth)。

### <a name="owin-integration"></a>OWIN 集成

ASP.NET身份验证现在基于 OWIN 中间件，可用于任何基于 OWIN 的主机。 有关 OWIN 的详细信息，请参阅以下[Microsoft OWIN 组件](#TOC7)部分。

<a id="TOC7"></a>
## <a name="microsoft-owin-components"></a>Microsoft OWIN 组件

[.NET](http://owin.org/) （OWIN） 的开放 Web 界面定义 .NET Web 服务器和 Web 应用程序之间的抽象。 OWIN 将 Web 应用程序与服务器分离，使 Web 应用程序与主机无关。 例如，您可以在 IIS 中托管基于 OWIN 的 Web 应用程序，也可以在自定义进程中自承载它。

Microsoft OWIN 组件（也称为 Katana 项目）中引入的更改包括新的服务器和主机组件、新的帮助器库和中间件以及新的身份验证中间件。

有关 OWIN 和卡塔纳的更多信息，请参阅[OWIN 和卡塔纳中的新增功能](../../../aspnet/overview/owin-and-katana/index.md)。

**注意[：OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)应用程序无法在 IIS 经典模式下运行;它们必须在集成模式下运行。**

**注意[：OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)应用程序必须完全信任地运行。**

### <a name="new-servers-and-hosts"></a>新服务器和主机

使用此版本，添加了新的组件以启用自承载方案。 这些组件包括以下 NuGet 包：

- **微软.Owin.Host.httpListener**. 提供一个 OWIN 服务器，该服务器使用**HttpListener**侦听 HTTP 请求并将其定向到 OWIN 管道中。
- **Microsoft.Owin.Hosting**为希望在自定义进程中自承载 OWIN 管道（如控制台应用程序或 Windows 服务）的开发人员提供一个库。
- **奥温霍斯**。 提供一个独立的可执行文件，用于包装`Microsoft.Owin.Hosting`并允许您自承载 OWIN 管道，而无需编写自定义主机应用程序。

此外，`Microsoft.Owin.Host.SystemWeb`该包现在使中间件能够向**SystemWeb**服务器提供提示，指示应在特定的ASP.NET管道阶段调用中间件。 此功能对于身份验证中间件特别有用，该中间件应在ASP.NET管道中早期运行。

### <a name="helper-libraries-and-middleware"></a>帮助库和中间件

尽管只能使用 OWIN 规范中的函数和类型定义编写 OWIN 组件，但新`Microsoft.Owin`包提供了一组更用户友好的抽象。 此包将几个较早的包（例如 ，）`Owin.Extensions``Owin.Types`合并到单个结构良好的对象模型中，然后其他 OWIN 组件可以轻松地使用该模型。 事实上，大多数 Microsoft OWIN 组件现在都使用此包。

> [!NOTE]
> [OWIN](http://www.owin.org)应用程序无法在 IIS 经典模式下运行;它们必须在集成模式下运行。

> [!NOTE]
> [OWIN](http://www.owin.org)应用程序必须完全信任地运行。

此版本还包括 Microsoft.Owin.诊断包，其中包括用于验证正在运行的 OWIN 应用程序的中间件，以及帮助调查故障的错误页中间件。

### <a name="authentication-components"></a>身份验证组件

以下身份验证组件可用。

- **微软.Owin.安全.主动目录**. 使用内部部署或基于云的目录服务启用身份验证。
- **微软.Owin.Security.cookies**支持使用Cookie进行身份验证。 此包以前命名为`Microsoft.Owin.Security.Forms`。
- **微软.Owin.Security.Facebook**使用Facebook基于OAuth的服务启用身份验证。
- **微软.Owin.Security.谷歌**使用谷歌基于OpenID的服务启用身份验证。
- **微软.Owin.Security.Jwt**启用使用 JWT 令牌的身份验证。
- **微软.Owin.Security.微软帐户**启用使用微软帐户进行身份验证。
- **微软.奥温.安全.奥乌斯**. 提供 OAuth 授权服务器以及用于验证无记名令牌的中间件。
- **微软.Owin.Security.Twitter**使用Twitter基于OAuth的服务进行身份验证。

此版本还包括包`Microsoft.Owin.Cors`，其中包含用于处理跨源 HTTP 请求的中间件。

> [!NOTE]
> 在 Visual Studio 2013 的最终版本中删除了对 JWT 签名的支持。

<a id="ef6"></a>
## <a name="entity-framework-6"></a>Entity Framework 6

有关实体框架 6 中的新功能和其他更改的列表，请参阅[实体框架版本历史记录](https://msdn.com/data/jj574253)。

<a id="TOC14"></a>
## <a name="aspnet-razor-3"></a>ASP.NET剃刀 3

ASP.NET Razor 3 包括以下新功能：

- 支持选项卡编辑。 以前，使用"**保留选项卡**"选项时，Visual Studio 中的 **"格式文档**"命令、自动缩进和自动格式设置无法正常工作。 此更改纠正了用于选项卡格式的 Razor 代码的可视化工作室格式。
- 生成链接时支持 URL 重写规则。
- 删除安全透明属性。
  > [!NOTE]
  > 这是一个重大更改，使 Razor 3 与 MVC4 和更早版本不兼容，而 Razor 2 与 MVC5 或针对 MVC5 编译的程序集不兼容。

Razor 3 问题修复在 Visual Studio 2013 从预发行版本可以[在这里](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Resolved%7cClosed&type=All&priority=All&release=All%7cv5.0%2bPreview%7cv5.0%2bRC%7cv5.0%2bRTM&assignedTo=All&component=Web%2bPages%252fRazor&reasonClosed=Fixed&sortField=LastUpdatedDate&sortDirection=Descending&page=0)找到.

<a id="TOC15"></a>
## <a name="aspnet-app-suspend"></a>ASP.NET应用挂起

ASP.NET应用程序挂起是 .NET Framework 4.5.1 中的一项改变游戏规则的功能，它从根本上改变了在一台计算机上托管大量ASP.NET站点的用户体验和经济模型。 有关详细信息，请参阅[ASP.NET应用程序挂起 – 响应式共享 .NET Web 托管](https://blogs.msdn.com/b/dotnet/archive/2013/10/09/asp-net-app-suspend-responsive-shared-net-web-hosting.aspx)。

<a id="knownissues"></a>
## <a name="known-issues-and-breaking-changes"></a>已知问题和重大更改

本节介绍视觉工作室 2013 ASP.NET和 Web 工具中的已知问题和重大更改。

### <a name="nuget"></a>NuGet

- [使用 SLN 文件时，新包还原在 Mono 上不起作用](https://nuget.codeplex.com/workitem/3596)， 将在即将进行的 nuget.exe 下载和[NuGet.CommandLine 包](http://www.nuget.org/packages/NuGet.CommandLine/)更新中修复。
- [新的包还原与 Wix 项目不起作用](https://nuget.codeplex.com/workitem/3598)- 将在即将进行的 nuget.exe 下载和[NuGet.CommandLine 包](http://www.nuget.org/packages/NuGet.CommandLine/)更新中修复。
- [自动包还原在解决方案文件夹下的项目不起作用](https://nuget.codeplex.com/workitem/3625)， 将在 NuGet 2.8 中修复。

### <a name="aspnet-web-api"></a>ASP.NET Web API

1. `ODataQueryOptions<T>.ApplyTo(IQueryable)`不会总是返回`IQueryable<T>`，因为我们添加了 对`$select`和`$expand`的支持。

    我们以前的样本`ODataQueryOptions<T>`总是将返回值从`ApplyTo`转换为`IQueryable<T>`。 这在早期`$filter`起作用，因为我们支持之前的查询选项 （、、、、）`$orderby``$skip``$top`不会更改查询的形状。 `$select`现在，我们支持`$expand`，并从`ApplyTo`返回值将`IQueryable<T>`并不总是。

    [!code-csharp[Main](release-notes/samples/sample21.cs)]

    如果使用之前的示例代码，则如果客户端未发送`$select`和`$expand`，它将继续工作。 但是，如果您希望支持`$select`，并且`$expand`必须将该代码更改为此代码。

    [!code-csharp[Main](release-notes/samples/sample22.cs)]
2. **请求.Url 或请求上下文.Url 在批处理请求期间为空**

    在批处理方案中 **，UrlHelper**从**请求.Url**或**请求上下文.Url**访问时为空。

    此问题当前在此处跟踪[：BatchRequestContext.Url 对于批处理请求为空](http://aspnetwebstack.codeplex.com/workitem/1301)。

    此问题的解决方法是创建**UrlHelper**的新实例，如以下示例所示：

    **创建 UrlHelper 的新实例**

    [!code-csharp[Main](release-notes/samples/sample23.cs)]

### <a name="aspnet-mvc"></a>ASP.NET MVC

1. 使用 MVC5 和 OrgAuth 时，如果您有执行 AntiForgerToken 验证的视图，则当您将数据发布到视图时，可能会遇到以下错误：

    **错误**：

    *'/' 应用程序中出现服务器错误。*

    <em>所提供的索赔身份上不存在<http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier>类型""<https://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider>或""的索赔。要使用基于声明的身份验证启用反伪造令牌支持，请验证已配置的声明提供程序是否在它生成的声明标识实例上同时提供这两种声明。如果配置的声明提供程序使用不同的声明类型作为唯一标识符，则可以通过设置静态属性 AntiForgeryConfig.唯一ClaimType标识符来配置它。</em>

    **解决方法**：

    在 Global.asax 中添加以下行以修复它：

    `AntiForgeryConfig.UniqueClaimTypeIdentifier = ClaimTypes.Name;`

    这将在下一个版本中修复。
2. 将 MVC4 应用升级到 MVC5 后，生成解决方案并启动它。 您应该会看到以下错误：

    [A]系统.Web.WebPages.Razor.配置.Host节不能强制转换为 [B_system.Web.Web.WebPages.Razor.配置.主机节。 类型 A 源自 "系统.Web.WebPages.Razor" 版本=2.0.0.0，区域性=中性，PublicKeyToken=31bf3856ad364e35"在上下文"默认"的位置\_"C：_windows.Net_大会_GAC MSIL_System.WebPages.Razor_v4.0.0\_\_\_31bf3856ad36e35_系统.WebPages.剃须刀.剃须刀。" 类型 B 源自 'System.Web.WebPages.Razor， 版本=3.0.0.0， 区域性= 中性， PublicKeyToken_31bf3856ad364e35"在上下文"默认"的位置"C：_Windows_Microsoft.NET_Framework_v4.0.30319\临时ASP.NET文件\root_6d 05bbd0_e8b5908e_assembly_dl3_c9cbca63_f8910382\_6273ce01_System.WebPages.Razor.dll'。

    要修复上述错误，请打开项目中*的所有*Web.config 文件（包括"视图"文件夹中的文件），并执行以下操作：

   1. 将"System.Web.Mvc"版本"4.0.0.0"的所有匹配项更新为"5.0.0.0"。
   2. 更新&quot;"系统.Web.Helpers"、系统.Web.WebPages&quot;和&quot;系统.Web.WebPages.Razor&quot;到"3.0.0.0"版本的所有匹配项

      例如，在进行上述更改后，程序集绑定应如下所示：

      [!code-xml[Main](release-notes/samples/sample24.xml)]

      有关将 MVC 4 项目升级到 MVC 5 的信息，请参阅[如何将ASP.NET MVC 4 和 Web API 项目升级到ASP.NET MVC 5 和 Web API 2](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md)。
3. 当将客户端验证与 jQuery 不显眼验证一起使用时，对于类型="数字"的 HTML 输入元素，验证消息有时不正确。 输入无效号码时将显示所需值的验证错误（"需要"年龄字段），而不是需要有效编号的正确消息。

    在"创建"和"编辑"视图中具有整数属性的模型的脚手架代码通常会产生此问题。

    要解决此问题，从以下方面更改编辑器帮助程序：

    `@Html.EditorFor(person => person.Age)`

    更改为：

    `@Html.TextBoxFor(person => person.Age)`
4. ASP.NET MVC 5 不再支持部分信任。 链接到 MVC 或 WebAPI 二进制文件的项目应删除[安全透明](https://msdn.microsoft.com/library/system.security.securitytransparentattribute.aspx)属性和["允许部分受信任的呼叫者"](https://msdn.microsoft.com/library/system.security.allowpartiallytrustedcallersattribute.aspx)属性。 删除这些属性将消除编译器错误，如下所示。

    `Attempt by security transparent method ‘MyComponent' to access security critical type 'System.Web.Mvc.MvcHtmlString' failed. Assembly 'PagedList.Mvc, Version=4.3.0.0, Culture=neutral, PublicKeyToken=abbb863e9397c5e1' is marked with the AllowPartiallyTrustedCallersAttribute, and uses the level 2 security transparency model. Level 2 transparency causes all methods in AllowPartiallyTrustedCallers assemblies to become security transparent by default, which may be the cause of this exception.`

    > 请注意，作为副作用，您不能在同一应用程序中使用 4.0 和 5.0 程序集。 您需要将所有它们更新为 5.0。

### <a name="spa-template-with-facebook-authorization-may-cause-instability-in-ie-while-the-web-site-is-hosted-in-intranet-zone"></a>具有 Facebook 授权的 SPA 模板可能会导致 IE 不稳定，而网站托管在 Intranet 区域中

SPA 模板提供带 Facebook 的外部登录。 当使用模板创建的项目在本地运行时，登录可能会导致 IE 崩溃。

解决方案：

1. 在互联网区域托管网站;或

2. 在 IE 以外的浏览器中测试方案。

### <a name="web-forms-scaffolding"></a>Web 窗体基架

Web 窗体基架已从 VS2013 中删除，将来将更新为 Visual Studio。 但是，您仍可以通过添加 MVC 依赖项和生成 MVC 基架来在 Web 窗体项目中使用基架。 您的项目将包含 Web 窗体和 MVC 的组合。

要将 MVC 添加到 Web 窗体项目，请添加新的脚手架项，然后选择**MVC 5 依赖项**。 根据是否需要所有内容文件（如脚本）选择"最小"或"完整"。 然后，为 MVC 添加一个基架项，这将在项目中创建视图和控制器。

### <a name="mvc-and-web-api-scaffolding---http-404-not-found-error"></a>MVC 和 Web API 基架 - HTTP 404，未找到错误

如果在向项目添加基架项时遇到错误，则项目可能会处于不一致状态。 对基架所做的一些更改将回滚，但其他更改（如已安装的 NuGet 包）将不会回滚。 如果路由配置更改回滚，则用户在导航到基架项目时将收到 HTTP 404 错误。

解决方法：

- 要修复 MVC 的此错误，请添加新的脚手架项并选择 MVC 5 依赖项（最小或完整）。 此过程将添加项目所需的所有更改。
- 要修复 Web API 的此错误，本文：

  1. 将 WebApiConfig 类添加到项目中。

      [!code-csharp[Main](release-notes/samples/sample25.cs)]

      [!code-vb[Main](release-notes/samples/sample26.vb)]
  2. 在 Global.asax 中的应用程序\_启动方法中配置 WebApiConfig.注册，如下所示：

      [!code-csharp[Main](release-notes/samples/sample27.cs)]

      [!code-vb[Main](release-notes/samples/sample28.vb)]

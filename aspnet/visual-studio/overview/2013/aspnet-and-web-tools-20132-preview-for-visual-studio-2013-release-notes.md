---
uid: visual-studio/overview/2013/aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes
title: ASP.NET和网络工具 2013.2 用于视觉工作室 2013 发行说明 |微软文档
author: rick-anderson
description: ''
ms.author: riande
ms.date: 03/06/2014
ms.assetid: 7ef5f73c-ca60-43c1-bdb2-702800347e7e
msc.legacyurl: /visual-studio/overview/2013/aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes
msc.type: authoredcontent
ms.openlocfilehash: 41b0f3ad43846bc5799ecd398188b0f6ffcc0d66
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543621"
---
# <a name="aspnet-and-web-tools-20132--for-visual-studio-2013-release-notes"></a>适用于 Visual Studio 2013 的 ASP.NET 和 Web 工具 2013.2 发行说明

由[微软](https://github.com/microsoft)

## <a name="installation-notes"></a>安装说明

visual Studio 2013.2 的ASP.NET和 Web 工具捆绑在主安装程序中，可以作为[Visual Studio 2013 更新 2](https://go.microsoft.com/fwlink/?LinkId=390521)的一部分下载。

## <a name="documentation"></a>文档

有关 visual Studio 2013.2 的ASP.NET和 Web 工具的教程和其他信息可从[ASP.NET网站](https://www.asp.net/)获得。

## <a name="software-requirements"></a>软件要求

视觉工作室2013.2ASP.NET和网络工具需要视觉工作室2013。

## <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-20132"></a>Visual Studio ASP.NET和 Web 工具中的新功能 2013.2

以下各节介绍版本中引入的功能。

- [一个ASP.NET项目模板](#oneaspnet)
- [在 IIS Express 上启动 Web 应用程序时支持 SSL](#ssl)
- [可视化工作室 Web 编辑器增强功能](#vswebeditor)
- [浏览器链接](#browserlink)
- [在可视化工作室中支持 Azure 应用服务 Web 应用](#waws)
- [创建新 Web 项目时创建远程 Azure 资源](#AzureResources)
- [Web 发布增强功能](#webpublish)
- [ASP.NET脚手架](#scaffolding)
- [NuGet 2.8.1](#nuget)
- [ASP.NET Web 表单](#webforms)
- [ASP.NET MVC 5.1.2](#mvc)
- [ASP.NET Web API 2.1.2](#webapi)
- [ASP.NET网页 3.1.2](#webpages)
- [实体框架 6.1](#ef)
- [ASP.NET 标识 2.0.0](#identity)
- [微软 OWIN 组件](#owin)
- [ASP.NET信号R 2.0.2](#signalr)

<a id="oneaspnet"></a>
### <a name="one-aspnet-project-templates"></a>一个ASP.NET项目模板

- 更新ASP.NET项目模板以支持帐户确认和密码重置。
- 更新ASP.NET Web API 模板以支持使用内部组织帐户进行身份验证。
- ASP.NET SPA 模板现在包含基于 MVC 和服务器端视图的身份验证。 该模板具有一个 WebAPI 控制器，该控制器只能由经过身份验证的用户访问。

<a id="ssl"></a>
### <a name="support-ssl-when-launching-web-applications-on-iis-express"></a>在 IIS Express 上启动 Web 应用程序时支持 SSL

为了消除本地主机上浏览和调试 HTTPS 时的安全警告，我们添加了一个对话框，允许 Internet Explorer 和 Chrome 信任自签名的 IIS Express SSL 证书。

例如，可以将 Web 项目属性设置为使用 SSL。 单击 F4 可弹出属性对话框。 将**启用 SSL 更改为**true。 复制 SSL URL。

![启用 SSL 属性](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image1.png)

将 Web 项目属性页 Web 选项卡设置为使用基于 HTTPS 的 URL（SSL URL 将是`https://localhost:44300/`，除非您以前创建了 SSL 网站。

![设置项目 URL （HTTPS）](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image2.png)

按 Ctrl+F5 运行应用程序。 遵照说明信任 IIS Express 生成的自我签署证书。

![SSL 警告](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image3.png)

阅读**安全警告**对话框，然后单击"**是**"，如果要安装表示本地主机的证书。

![安全警告](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image4.png)

该网站将以 IE 或 Chrome 显示，浏览器中没有证书警告。

![没有警告的 HTTPS 页面](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image5.png)

Firefox 会使用自己的证书存储区，因此会显示警告。

<a id="vswebeditor"></a>
### <a name="visual-studio-web-editor-enhancements"></a>可视化工作室 Web 编辑器增强功能

- **新的JSON项目项目和编辑器**：我们已经添加了一个JSON项目项目和编辑器到可视化工作室。 当前 JSON 编辑器功能包括着色、语法验证、大括号完成、大纲、工具选项设置等。

    ![JSON 编辑器](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image6.png)

    IntelliSense 现在支持[JSON 架构](http://json-schema.org/)v3 和 v4。 有一个架构组合框用于选择现有架构、编辑本地架构路径，或者只需将项目 JSON 文件拖放到它以获取相对路径即可。

    ![JSON 感知](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image7.png)    ![JSON 架构编辑器](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image8.png)
- **新Sass （SCSS） 编辑器**： 我们在 VS2013 RTM 中添加了 LESS，现在我们有一个 Sass 项目项目和编辑器。 Sass 编辑器功能可与 LESS 编辑器类似，包括着色、变量和 Mixins IntelliSense、注释/注释、快速信息、格式设置、语法验证、大纲、goto 定义、颜色选取器、工具选项设置等。

    ![添加新项：SCSS 样式表](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image9.png)    ![样式表编辑器](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image10.png)
- **HTML、剃刀、CSS、LESS 和 Sas 文档中的新 URL 选取器：** VS 2013 在 Web 窗体页面之外没有 URL 选取器。 用于 HTML、Razor、CSS、LESS 和 Sas 编辑器的新 URL 选取器是一个无对话、流畅的键入选取器，可理解 ". 并适当筛选 img 标记和链接的文件列表。

    ![用于图像标记的 URL 选取器](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image11.png)    ![用于视图的 URL 选取器](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image12.png)    ![用于 CSS 的 URL 选取器](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image13.png)
- **通过添加更多功能更新 LESS 编辑器**
- **挖空智能感知升级**：我们为 VS IntelliSense 添加了非标准的"敲击"语法，"ko-vs-编辑视图模型："语法。 它可用于使用表单中的注释绑定到页面上的多个视图模型：

    ![挖空感知](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image14.png)

    我们还添加了对嵌套视图模型智能感知的支持，因此您可以深入到视图模型上的深嵌套对象。

    `<div data-bind="text: foo.bar.baz.etc" />`

    显示的智能感知是 JavaScript 对象的完整智能感知。

    ![显示完整 JavaScript 对象的智能感知](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image15.png)
- **HTML、Razor、CSS、LESS 和 Sass 文档中的新 URL 选取器**： VS 2013 在 Web 窗体页面之外没有 URL 选取器。 用于 HTML、Razor、CSS、LESS 和 Sas 编辑器的新 URL 选取器是一个无对话、流畅的键入选取器，可理解 ". 并适当筛选 img 标记和链接的文件列表。

    ![用于图像标记的 URL 选取器](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image16.png)    ![用于视图的 URL 选取器](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image17.png)    ![用于 CSS 的 URL 选取器](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image18.png)

<a id="browserlink"></a>
### <a name="browser-link"></a>浏览器链接

- 浏览器链接现在支持 HTTPS 连接，并且将在仪表板中列出具有其他连接，只要浏览器信任证书。
- 静态 HTML 源映射
- SPA 支持映射数据
- 自动更新映射数据

<a id="waws"></a>
### <a name="support-for-azure-app-service-web-apps-in-visual-studio"></a>在可视化工作室中支持 Azure 应用服务 Web 应用

- **支持 Azure 登录。**
- **Web 应用的远程调试和远程视图**：我们现在支持[Azure 应用服务中的 Web 应用的远程调试](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio)和服务器资源管理器中 Web 应用内容文件的远程视图。

<a id="AzureResources"></a>
### <a name="create-remote-azure-resources-when-creating-a-new-web-project"></a>创建新 Web 项目时创建远程 Azure 资源

我们在新的 Web 应用程序对话框上添加了[Azure"创建远程资源"](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet)复选框。 通过选择它，您将能够集成创建新 Web 应用程序、设置 Azure 发布网站进行测试以及通过几个简单步骤创建发布配置文件的体验。

![具有 Azure 资源的新项目](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image19.png)![发布到 Azure](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image20.png)

<a id="webpublish"></a>
### <a name="web-publish-enhancements"></a>Web 发布增强功能

- 改善发布用户体验。

<a id="scaffolding"></a>
### <a name="aspnet-scaffolding"></a>ASP.NET脚手架

- **枚举支持：** 如果您的模型使用枚举，则 MVC 基架将生成枚举的下拉。 这使用 MVC 中的枚举帮助器。
- **引导支持**：更新了 MVC 基架中的编辑器模板，以便它们使用引导类。
- **包支持**：MVC 和 Web API 基架将为 MVC 和 Web API 添加 5.1 包

以下屏幕截图演示了基架模型。

- 型号代码：

     ![模型代码](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image21.png)
- 编译模型代码，右键单击，然后选择 **"添加****"，新建基架项目**。

     ![添加新的脚手架项目](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image22.png)
- **使用实体框架选择具有视图的 MVC5 控制器**：

     ![添加带视图的新 MVC5 控制器](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image23.png)
- 使用模型**添加控制器**：

    ![](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image24.png)
- 检查生成的代码，例如视图/工作日模型/Edit.cshtml 包含`@Html.EnumDropDownListFor`：![包含 EnumDropDownList 的视图](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image25.png)
- 运行页面以查看生成的枚举组合框，请注意，如果值可以为 null，则可以为组合框选择一个空字符串。 例如，"**创建"** 页显示以下内容：

    ![允许空字符串的组合框](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image26.png)

<a id="nuget"></a>
### <a name="nuget-281"></a>NuGet 2.8.1

NuGet 2.8.1 RTM 将于 2014 年 4 月发布。 以下是发行说明的要点，但请查看[完整发行说明](http://docs.nuget.org/docs/release-notes/nuget-2.8)，了解有关这些更改的详细信息。

- **目标 Windows Phone 8.1 应用程序**： NuGet 2.8.1 现在支持使用目标框架名字"WindowsPhoneApp"，"WPA"，"WindowsPhoneApp81"和"WPA81"定位 Windows Phone 8.1 应用程序。

- **依赖项的修补程序解析**：在解决包依赖项时，NuGet 历来实施了选择满足包依赖项的最低主包和次要包版本的策略。 但是，与主要版本和次要版本不同，修补程序版本始终解析为最高版本。 尽管该行为是善意的，但它造成了安装具有依赖关系的包缺乏确定性。
- **依赖项版本交换机**：虽然 NuGet 2.8 更改了解析依赖项的*默认*行为，但它也通过包管理器控制台中的 -依赖项版本开关增加了对依赖项解析过程的更精确控制。 该交换机允许解析对低可能版本（默认行为）、可能的最高版本或最高次要版本或修补程序版本的依赖项。 此开关仅适用于电源壳命令中的安装包。
- **依赖项版本属性**：除了上面详述的 -依赖版本开关外，NuGet 还允许在 nuget.config 文件中设置新属性，定义默认值是什么，如果 -依赖项版本开关未在安装包的调用中指定。 对于任何安装包操作，NuGet 包管理器对话框也会尊重此值。 要设置此值，请将下面的属性添加到 nuget.config 文件：

    `<config> <add key="dependencyversion" value="Highest" /> </config>`
- **使用 -WhatIf**预览 NuGet 操作 ：某些 NuGet 包可以具有深层依赖项图，因此，在安装、卸载或更新操作期间，它可以很有帮助，以便首先看到将会发生什么。 NuGet 2.8 添加了标准 PowerShell - 如果切换到安装包、卸载包和更新包命令，以便可视化将应用该命令的包的整个关闭。
- **降级包**：安装包的预发布版本以调查新功能，然后决定回滚到最后的稳定版本的情况并不少见。 在 NuGet 2.8 之前，这是卸载预发布包及其依赖项，然后安装早期版本的多步骤过程。 但是，使用 NuGet 2.8，更新包现在会将整个包关闭（例如包的依赖项树）回滚到以前的版本。
- **开发依赖项**：许多不同类型的功能可以作为 NuGet 包提供， 包括用于优化开发过程的工具。 这些组件虽然在开发新包方面可以发挥作用，但在以后发布新包时，不应被视为新包的依赖项。 NuGet 2.8 使包能够在 .nuspec 文件中将自己标识为开发依赖项。 安装后，此元数据也将添加到包. 稍后在 nuget.exe 包期间分析该包.config 文件以分析 NuGet 依赖项时，它将排除标记为开发依赖项的这些依赖项。
- **单个包.为不同平台配置文件**：在为多个目标平台开发应用程序时，为每个不同的生成环境使用不同的项目文件是很常见的。 在不同的项目文件中使用不同的 NuGet 包也很常见，因为包对不同平台的支持级别不同。 NuGet 2.8 通过为不同的平台特定项目文件创建不同的包.config 文件，为该方案提供了改进的支持。
- **回退到本地缓存**：虽然 NuGet 包通常使用远程库（如使用网络连接的[NuGet 库](http://www.nuget.org)）使用，但在许多情况下，客户端未连接。 如果没有网络连接，NuGet 客户端将无法成功安装包 - 即使这些包已在客户端的计算机上本地 NuGet 缓存中。 NuGet 2.8 将自动缓存回退到包管理器控制台。

    缓存回退功能不需要任何特定的命令参数。 此外，缓存回退目前仅在包管理器控制台中工作 - 该行为当前在包管理器对话框中不起作用。
- **错误修复**：所做的主要错误修复之一是更新包 -重新安装命令的性能改进。

    除了这些功能和上述性能修复之外，NuGet 的此版本还包括许多其他错误修复。 在新闻稿中共处理了 181 个问题。 有关 NuGet 2.8 中固定的工作项的完整列表，请查看此版本的[NuGet 问题跟踪器](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all)。

<a id="webforms"></a>
### <a name="aspnet-web-forms"></a>ASP.NET Web 窗体

- Web 窗体模板现在演示如何对ASP.NET身份进行帐户确认和密码重置。
- 实体数据源控件和实体框架的动态数据提供程序 6。 有关详细信息，请参阅以下 MSDN 博客：[实体框架 6 的动态数据提供程序和实体数据源控件](https://blogs.msdn.com/b/webdev/archive/2014/01/30/announcing-preview-of-dynamic-data-provider-and-entitydatasource-control-for-entity-framework-6.aspx)。

<a id="mvc"></a>
### <a name="aspnet-mvc-512"></a>ASP.NET MVC 5.1.2

- [属性路由改进](../../../mvc/overview/releases/mvc51-release-notes.md#AttributeRouting)
- [对编辑器模板的引导支持](../../../mvc/overview/releases/mvc51-release-notes.md#Bootstrap)
- [视图中的枚举支持](../../../mvc/overview/releases/mvc51-release-notes.md#Enum)
- [对最小长度/最大长度属性的不显眼支持](../../../mvc/overview/releases/mvc51-release-notes.md#Unobtrusive)
- [在不显眼的 Ajax 中支持"此"上下文](../../../mvc/overview/releases/mvc51-release-notes.md#thisContext)
- 各种[错误修复](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=v5.1%20Preview%7cv5.1%20RTM&assignedTo=All&component=MVC&sortField=AssignedTo&sortDirection=Ascending&page=0&reasonClosed=Fixed)

<a id="webapi"></a>
### <a name="aspnet-web-api-212"></a>ASP.NET Web API 2.1.2

- [全局错误处理](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#global-error)
- [属性路由增强功能](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#attribute-routing)
- [帮助页面改进](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#help-page)
- [忽略路由支持](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#ignoreroute)
- [BSON 介质类型物质](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#bson)
- [更好地支持异步滤波器](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#async-filters)
- [客户端格式库的查询解析](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#query-parsing)
- 各种[错误修复](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=v5.1%20Preview%7cv5.1%20RTM&assignedTo=All&component=Web%20API%7cWeb%20API%20OData&sortField=AssignedTo&sortDirection=Ascending&page=0&reasonClosed=Fixed)

<a id="webpages"></a>
### <a name="aspnet-web-pages-312"></a>ASP.NET网页 3.1.2

- 各种[错误修复](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=v5.1%20Preview%7cv5.1%20RTM&assignedTo=All&component=Web%20Pages/Razor&sortField=AssignedTo&sortDirection=Ascending&page=0&reasonClosed=Fixed)

<a id="ef"></a>
### <a name="entity-framework-61"></a>实体框架 6.1

实体框架已更新为 6.1 版，用于运行时和工具。 实体框架 （EF） 6.1 是实体框架 6 的一个小更新，包括许多错误修复和新功能。 有关 EF6.1 的详细信息（包括指向新功能的文档的链接），请参阅[实体框架版本历史记录](https://msdn.microsoft.com/data/jj574253)。 此版本中的新功能包括：

- **工具整合**提供了创建新 EF 模型的一致方法。 此功能扩展了ADO.NET实体数据模型向导，以支持创建代码优先模型，包括从现有数据库进行反向工程。 这些功能以前在 EF 电动工具中以测试版质量提供。
- **处理事务提交失败**提供了新的[系统.Data.Entity.基础结构.提交失败处理，](https://msdn.microsoft.com/library/system.data.entity.infrastructure.commitfailurehandler(v=vs.113).aspx)它利用新引入的拦截事务操作的能力。 **提交失败处理程序**允许在提交事务时自动从连接故障中恢复。
- **IndexAttribute**允许在 Code First 模型中的属性（或属性）上放置属性来指定索引。 然后，代码优先将在数据库中创建相应的索引。
- **公共映射 API**提供对 EF 对属性和类型如何映射到数据库中的列和表的信息的访问。 在以前的版本中，此 API 是内部的。
- **能够通过 App/Web.config 文件配置拦截器**（允许在不重新编译应用程序的情况下添加拦截器）。
- **DatabaseLogger**是一种新的拦截器，它可以轻松地将所有数据库操作记录到文件中。 与前一个功能结合使用，这允许您轻松打开已部署应用程序的数据库操作日志记录，而无需重新编译。
- **迁移模型更改检测**已改进，以便更精确地迁移基架;更改检测过程的性能也得到了极大的提高。
- **性能改进**包括初始化期间数据库操作减少、LINQ 查询中无效相等比较的优化、更多方案中更快的视图生成（模型创建）以及具有多个关联的跟踪实体的更高效具体化。

<a id="identity"></a>
### <a name="aspnet-identity-200"></a>ASP.NET 标识 2.0.0

- **双重身份验证**：ASP.NET标识现在支持双重身份验证。 在密码泄露的情况下，双重身份验证为用户帐户提供了额外的安全层。 此外，还保护暴力攻击两个因子代码。
- **帐户锁定：** 提供一种在用户输入密码或双因素代码不正确时锁定用户的方法。 可以配置无效尝试的次数和锁定用户的时间跨度。 开发人员可以选择关闭某些用户帐户的帐户锁定，以便他们在需要时关闭。
- **账户确认：** ASP.NET身份系统现在支持帐户确认。 这是当今大多数网站中相当常见的情况，当您在网站上注册新帐户时，您需要确认电子邮件，然后才能在网站中执行任何操作。 电子邮件确认是有用的，因为它可以防止创建虚假帐户。 如果您使用电子邮件作为与网站用户（如论坛网站、银行、电子商务或社交网站）通信的方法，则此功能非常有用。
- **密码重置：** 密码重置是一项功能，用户可以重置其密码，如果他们忘记了他们的密码。
- **安全戳（随处可见）：** 支持在用户更改密码或任何其他安全相关信息（如删除关联的登录名（如 Facebook、Google、微软帐户等）时为用户重新生成安全令牌的方法。 这是必需的，以确保使用旧密码生成的任何令牌都失效。 在示例项目中，如果更改用户的密码，则会为用户生成新令牌，并且任何以前的令牌都失效。 此功能为应用程序提供了额外的安全层，因为当您更改密码时，您将从登录到此应用程序的任何地方（所有其他浏览器）注销。
- **使主键的类型对用户和角色具有扩展性**：在ASP.NET标识 1.0 中，表用户和角色的主键类型是字符串。 这意味着当使用实体框架在 SQL Server 中保留ASP.NET标识系统时，我们使用 nvarchar。 围绕堆栈溢出的此默认实现，并根据传入的反馈进行了许多讨论。 我们提供了一个扩展性挂钩，您可以在其中指定用户和角色表的主键。 如果要迁移应用程序，并且应用程序正在存储 UserId 是 GUID 或 int，则此扩展性挂钩特别有用。
- **支持用户和角色上的"可查询"：** 在 UsersStore 和 RolesStore 上添加了对 IQuery 的支持，您可以轻松地获取用户和角色列表。
- **支持通过用户管理器删除操作**
- **对用户名进行索引**：在ASP.NET标识实体框架实现中，我们使用 EF 6.1.0 中的新 Index 属性在用户名上添加了唯一索引。 这可确保用户名始终是唯一的，并且没有种族条件，您可以最终使用重复的用户名。
- **增强的密码验证器：** 在标识 1.0 ASP.NET中附带的密码验证器是一个相当基本的密码验证器，它只验证了最小长度。 有一个新的密码验证器，使您能够对密码的复杂性进行更多的控制。 请注意，即使您打开此密码中的所有设置，我们也鼓励您为用户帐户启用双重身份验证。
- **标识工厂中间件/创建PerOwin上下文**：

    - **用户管理器**：您可以使用工厂实现从 OWIN 上下文中获取用户管理器的实例。 此模式类似于我们用于从 OWIN 上下文中获取 SignIn 和 SignOut 的身份验证管理器。 这是为应用程序获取每个请求的 UserManager 实例的推荐方法。
    - **DbContextFactory**：ASP.NET标识使用实体框架在 SQL Server 中持久化标识系统。 为此，标识系统具有对应用程序 DbContext 的引用。 DbContextFactory 中间件返回应用程序中每个请求的应用程序 DbContext 实例，您可以在应用程序中使用。
- **ASP.NET标识示例 NuGet 包**： 示例 NuGet 包可以使安装和运行ASP.NET标识的样本变得更容易，并遵循最佳实践。 这是 MVC 应用程序ASP.NET示例。 请在生产中部署代码之前修改代码以适合您的应用程序。 该示例应安装在空ASP.NET应用程序中。 有关该包的详细信息，请访问以下博客文章：[宣布ASP.NET标识 2.0.0 的 RTM](https://blogs.msdn.com/b/webdev/archive/2014/03/20/test-announcing-rtm-of-asp-net-identity-2-0-0.aspx)

<a id="owin"></a>
### <a name="microsoft-owin-components"></a>微软 OWIN 组件

此版本中修复了许多错误。 有关详细信息，请参阅[2.1.0 版本的发行说明](https://katanaproject.codeplex.com/releases/view/113281)。

<a id="signalr"></a>
### <a name="aspnet-signalr-202"></a>ASP.NET信号R 2.0.2

此版本中修复了许多错误。 有关详细信息，请参阅[2.0.2 版本的发行说明](https://github.com/SignalR/SignalR/releases/tag/2.0.2)。

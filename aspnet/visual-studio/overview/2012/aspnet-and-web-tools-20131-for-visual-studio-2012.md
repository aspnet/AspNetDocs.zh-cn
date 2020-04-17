---
uid: visual-studio/overview/2012/aspnet-and-web-tools-20131-for-visual-studio-2012
title: ASP.NET和网络工具发行说明 2013.1 可视化工作室 2012 |微软文档
author: rick-anderson
description: 本文档介绍了 Visual Studio 2012 的 ASP.NET和网络工具 2013.1 的发布。
ms.author: riande
ms.date: 11/13/2013
ms.assetid: ca26e5bb-630e-41d2-8512-2a9386c431cb
msc.legacyurl: /visual-studio/overview/2012/aspnet-and-web-tools-20131-for-visual-studio-2012
msc.type: authoredcontent
ms.openlocfilehash: d4aced4e77a150d52358c2d2513ff79e6594a9de
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543569"
---
# <a name="release-notes-for-aspnet-and-web-tools-20131-for-visual-studio-2012"></a>适用于 Visual Studio 2012 的 ASP.NET 和 Web 工具 2013.1 发行说明

由[微软](https://github.com/microsoft)

> 本文档介绍了 Visual Studio 2012 的 ASP.NET和网络工具 2013.1 的发布。

## <a name="contents"></a>目录

- [安装说明](#install)
- [软件要求](#requirements)
- 视觉工作室 2012 年 ASP.NET 和网络工具 2013.1 中的新功能

    - [Bootstrap](#bootstrap)
    - [模板](#templates)

        - [ASP.NET MVC 5 模板](#mvc5template)
        - [ASP.NET Web API 2 模板](#apitemplate)
        - [项目模板](#itemtemplate)
    - [Entity Framework 6](#ef6)
    - [ASP.NET脚手架](#scaffold)
    - [剃刀编辑器](#razor)
    - [NuGet 2.7](#nuget)
- 已知问题和重大更改

    - [ASP.NET脚手架](#issuescaffolding)

        - [MVC 和 Web API 基架 - HTTP 404，未找到错误](#404issue)
        - [Visual Studio Express 2012 用于 Web 在添加脚手架项目后停止工作](#expressissue)
    - [ASP.NET剃刀 3](#issuerazor)

        - [使用"使用"或"F5"查看 cshtml 文件会导致服务器错误](#browseissue)
        - [Url 重写和蒂尔德 （*）](#rewriteissue)
    - [模板](#templateissue)

<a id="install"></a>
## <a name="installation-notes"></a>安装说明

[安装](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WebNode11Pack.appids)ASP.NET和网络工具 2013.1 用于视觉工作室 2012。

<a id="requirements"></a>
## <a name="software-requirements"></a>软件要求

您必须有 Visual Studio 2012 或 Visual Studio Express 2012 用于 Web。

## <a name="new-features-in-aspnet-and-web-tools-20131-for-visual-studio-2012"></a>视觉工作室 2012 年 ASP.NET 和网络工具 2013.1 中的新功能

<a id="bootstrap"></a>
### <a name="bootstrap"></a>Bootstrap

当您脚手架 MVC 5 控制器和视图时，视图的标记使用[Bootstrap](http://getbootstrap.com/)。

<a id="templates"></a>
### <a name="templates"></a>模板

<a id="mvc5template"></a>
#### <a name="aspnet-mvc-5-template"></a>ASP.NET MVC 5 模板

我们添加了一个新的 MVC 5 模板。 它引用最新的 MVC 5 NuGet 包，您可以使用基架添加控制器和视图。

<a id="apitemplate"></a>
#### <a name="aspnet-web-api-2-template"></a>ASP.NET Web API 2 模板

我们添加了一个新的 Web API 2 模板。 它引用最新的 Web API 2 NuGet 包，您可以使用基架添加控制器和视图。

<a id="itemtemplate"></a>
#### <a name="item-templates"></a>项模板

我们为 MVC 5 视图、网页 （Razor 3） 和 Web API 2 控制器添加了新的项目模板。 他们在添加新项的同时，将相关的 NuGet 包安装到项目中。

<a id="ef6"></a>
### <a name="entity-framework-6"></a>Entity Framework 6

当您使用实体框架构建 MVC 或 Web API 控制器时，我们使用框架 6。 有关实体框架的详细信息，请参阅[实体框架版本历史记录](https://msdn.com/data/jj574253)。

您还可以下载并安装可视化工作室的实体框架 6 工具 2012。 请参阅[获取实体框架](https://msdn.com/data/ee712906#tooling)。

<a id="scaffold"></a>
### <a name="aspnet-scaffolding"></a>ASP.NET脚手架

ASP.NET基架是ASP.NET Web 应用程序的代码生成框架。 它可以轻松地向与数据模型交互的项目添加样板代码。

在 Visual Studio 的早期版本中，基架仅限于ASP.NET MVC 项目。 使用此更新，您现在可以对任何ASP.NET项目（包括 Web 窗体）使用基架。 此更新不支持为 Web 窗体项目生成页面，但仍可以通过向项目添加 MVC 依赖项来使用 Web 窗体的脚手架。 将在将来的更新中添加对生成 Web 窗体页面的支持。

使用基架时，我们确保在项目中安装了所有必需的依赖项。 例如，如果从ASP.NET Web 窗体项目开始，然后使用基架添加 Web API 控制器，则所需的 NuGet 包和引用将自动添加到项目中。

要将 MVC 基架添加到 Web 窗体项目，请添加新**的脚手架项**，并在对话框窗口中选择**MVC 5 依赖项**。 基架 MVC 有两个选项;最小和完整。 如果选择"最小"，则只有 ASP.NET MVC 的 NuGet 包和引用添加到项目中。 如果选择"完整"选项，则添加最小依赖项以及 MVC 项目所需的内容文件。

支持基架异步控制器使用实体框架 6 中的新异步功能。

有关详细信息和教程，请参阅[ASP.NET脚手架概述](../2013/aspnet-scaffolding-overview.md)。 这些教程显示了视觉工作室 2013 的脚手架，但它们也适用于 Visual Studio 2012 的ASP.NET和网络工具 2013.1。

<a id="razor"></a>
### <a name="razor-editor"></a>剃刀编辑器

有了这个更新，Visual Studio 2012 现在支持 Razor 3 工具/编辑。

<a id="nuget"></a>
### <a name="nuget-27"></a>NuGet 2.7

NuGet 2.7 包含一组丰富的新功能，在[NuGet 2.7 发行说明](http://docs.nuget.org/docs/release-notes/nuget-2.7)中对此进行了详细介绍。

此版本的 NuGet 消除了用户显式允许 NuGet 还原缺少的包的需要。 安装 NuGet 2.7 时，用户隐式同意自动还原丢失的包。 用户可以通过 Visual Studio 中的 NuGet 设置明确选择退出包恢复。 此更改简化了包还原的工作方式。

## <a name="known-issues-and-breaking-changes"></a>已知问题和重大更改

<a id="issuescaffolding"></a>
### <a name="aspnet-scaffolding"></a>ASP.NET脚手架

<a id="404issue"></a>
#### <a name="mvc-and-web-api-scaffolding---http-404-not-found-error"></a>MVC 和 Web API 基架 - HTTP 404，未找到错误

如果在向项目添加基架项时遇到错误，则项目可能会处于不一致状态。 对基架所做的一些更改将回滚，但其他更改（如已安装的 NuGet 包）将不会回滚。 如果路由配置更改回滚，则用户在导航到基架项目时将收到 HTTP 404 错误。

要修复 MVC 的此错误，请添加新的脚手架项并选择 MVC 5 依赖项（最小或完整）。 此过程将添加项目所需的所有更改。

要修复 Web API 的此错误，本文：

1. 将以下 WebApiConfig 类添加到项目中。

    [!code-csharp[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample1.cs)]

    [!code-vb[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample2.vb)]
2. 在 Global.asax 中的应用程序\_启动方法中配置 WebApiConfig.注册，如下所示：

    [!code-csharp[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample3.cs)]

    [!code-vb[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample4.vb)]

<a id="expressissue"></a>
#### <a name="visual-studio-express-2012-for-web-stops-working-after-adding-a-scaffolded-item"></a>Visual Studio Express 2012 用于 Web 在添加脚手架项目后停止工作

如果 Web 的 Visual Studio Express 2012 在使用实体框架添加基架项目（例如 Web API 2 控制器具有操作的操作，使用实体框架）后停止工作，则 Visual Studio Express 可能无法加载依赖于 System.Web.扩展的程序集的本机映像。

要更正此问题，请将 Visual Studio Express 配置为使用 System.Web.扩展的 MSIL 映像：

1. 在管理员模式下打开命令提示。
2. 转到 %程序文件%\微软视觉工作室 11.0_Common7_IDE 或 %程序文件 （x86）%\微软视觉工作室 11.0_Common7_IDE （对于 64 位窗口）。
3. 在文本编辑器中打开 VWDExpress.exe.config。
4. 在&lt;&gt;/配置&lt;运行时&gt;元素下添加以下行：  

    [!code-xml[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample5.xml)]
5. 重新启动可视化工作室快速 2012 为 Web.

<a id="issuerazor"></a>
### <a name="aspnet-razor-3"></a>ASP.NET剃刀 3

<a id="browseissue"></a>
#### <a name="viewing-cshtml-file-with-browse-with-or-f5-causes-a-server-error"></a>使用"使用"或"F5"查看 cshtml 文件会导致服务器错误

当您在 Visual Studio 2012 中创建 MVC 5 项目（或在 Visual Studio 2012 中打开在 Visual Studio 2013 中创建的 MVC 5 项目）并尝试使用"浏览"或 F5 查看 cshtml 文件时，您将收到一个错误，指出 **"/' 应用程序中的服务器错误**"。 服务器尝试导航到`http://localhost:XXXX/Views/../XXXX.cshtml`

要解决此问题，请将项目中的 **"开始操作"** 设置更改为 **"特定页面**"。 您无需为页面提供值。

![](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image1.png)

进行此更改后，选择 F5 将导航到应用程序的根目录`http://localhost:XXXX`（ 。 此行为与 Visual Studio 2013 中的 MVC 5 项目的行为不同，其中 **"当前页面"** 设置将启动打开页面。

<a id="rewriteissue"></a>
#### <a name="url-rewrite-and-tilde"></a>Url 重写和蒂尔德 （*）

升级到ASP.NET Razor 3 或 ASP.NET MVC 5 后，如果使用 URL 重写，则波浪（*）表示法可能不再正常工作。 URL 重写会影响 HTML&lt;元素（如 A/、SCRIPT/、LINK/&gt;&lt;&gt;&lt;&gt;等）中的波浪线（*）表示法，因此波浪线不再映射到根目录。

例如，如果将**asp.net/content**请求重写为**asp.net，**&lt;则 a href_"/内容/"中的 href 属性将&gt;解析为 **/内容/内容/** 而不是**/**。 要禁止此更改，可以在每个网页或 Global.asax 中的**\_应用程序 BeginRequest**中将**IIS\_WasUrl 重写**上下文设置为 false。

<a id="templateissue"></a>
### <a name="templates"></a>模板

当您在 Windows 8.1 或 Windows Server 2012 R2 上使用 Visual Studio 2012 创建 ASP.NET MVC 项目时，Visual Studio 会显示一条错误消息，指出"为 ASP.NET 4.5 配置 Web [url] 失败"。

![配置错误](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image2.png)

您会看到此错误，因为 Visual Studio 2012 在 Windows 这些版本上安装时不会启用ASP.NET 4.5 功能。 要启用 ASP.NET 4.5，请执行打开[或关闭"打开"Windows 功能](https://windows.microsoft.com/windows-8/turn-windows-features-on-off)中描述的步骤。

![打开或关闭 Windows 功能](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image3.png)

或者，您可以通过命令行启用ASP.NET 4.5。

1. 在管理员模式下打开命令提示。
2. 运行以下命令以启用 ASP.NET 4.5。  
    `dism /Online /Enable-Feature /FeatureName:NetFx4Extended-ASPNET45 /Quiet /NoRestart`

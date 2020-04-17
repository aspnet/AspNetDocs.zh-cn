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
# <a name="release-notes-for-aspnet-and-web-tools-20131-for-visual-studio-2012"></a><span data-ttu-id="bad06-103">适用于 Visual Studio 2012 的 ASP.NET 和 Web 工具 2013.1 发行说明</span><span class="sxs-lookup"><span data-stu-id="bad06-103">Release Notes for ASP.NET and Web Tools 2013.1 for Visual Studio 2012</span></span>

<span data-ttu-id="bad06-104">由[微软](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="bad06-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="bad06-105">本文档介绍了 Visual Studio 2012 的 ASP.NET和网络工具 2013.1 的发布。</span><span class="sxs-lookup"><span data-stu-id="bad06-105">This document describes the release of ASP.NET and Web Tools 2013.1 for Visual Studio 2012.</span></span>

## <a name="contents"></a><span data-ttu-id="bad06-106">目录</span><span class="sxs-lookup"><span data-stu-id="bad06-106">Contents</span></span>

- [<span data-ttu-id="bad06-107">安装说明</span><span class="sxs-lookup"><span data-stu-id="bad06-107">Installation Notes</span></span>](#install)
- [<span data-ttu-id="bad06-108">软件要求</span><span class="sxs-lookup"><span data-stu-id="bad06-108">Software Requirements</span></span>](#requirements)
- <span data-ttu-id="bad06-109">视觉工作室 2012 年 ASP.NET 和网络工具 2013.1 中的新功能</span><span class="sxs-lookup"><span data-stu-id="bad06-109">New Features in ASP.NET and Web Tools 2013.1 for Visual Studio 2012</span></span>

    - [<span data-ttu-id="bad06-110">Bootstrap</span><span class="sxs-lookup"><span data-stu-id="bad06-110">Bootstrap</span></span>](#bootstrap)
    - [<span data-ttu-id="bad06-111">模板</span><span class="sxs-lookup"><span data-stu-id="bad06-111">Templates</span></span>](#templates)

        - [<span data-ttu-id="bad06-112">ASP.NET MVC 5 模板</span><span class="sxs-lookup"><span data-stu-id="bad06-112">ASP.NET MVC 5 template</span></span>](#mvc5template)
        - [<span data-ttu-id="bad06-113">ASP.NET Web API 2 模板</span><span class="sxs-lookup"><span data-stu-id="bad06-113">ASP.NET Web API 2 template</span></span>](#apitemplate)
        - [<span data-ttu-id="bad06-114">项目模板</span><span class="sxs-lookup"><span data-stu-id="bad06-114">Item Templates</span></span>](#itemtemplate)
    - [<span data-ttu-id="bad06-115">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="bad06-115">Entity Framework 6</span></span>](#ef6)
    - [<span data-ttu-id="bad06-116">ASP.NET脚手架</span><span class="sxs-lookup"><span data-stu-id="bad06-116">ASP.NET Scaffolding</span></span>](#scaffold)
    - [<span data-ttu-id="bad06-117">剃刀编辑器</span><span class="sxs-lookup"><span data-stu-id="bad06-117">Razor Editor</span></span>](#razor)
    - [<span data-ttu-id="bad06-118">NuGet 2.7</span><span class="sxs-lookup"><span data-stu-id="bad06-118">NuGet 2.7</span></span>](#nuget)
- <span data-ttu-id="bad06-119">已知问题和重大更改</span><span class="sxs-lookup"><span data-stu-id="bad06-119">Known Issues and Breaking Changes</span></span>

    - [<span data-ttu-id="bad06-120">ASP.NET脚手架</span><span class="sxs-lookup"><span data-stu-id="bad06-120">ASP.NET Scaffolding</span></span>](#issuescaffolding)

        - [<span data-ttu-id="bad06-121">MVC 和 Web API 基架 - HTTP 404，未找到错误</span><span class="sxs-lookup"><span data-stu-id="bad06-121">MVC and Web API Scaffolding - HTTP 404, Not Found error</span></span>](#404issue)
        - [<span data-ttu-id="bad06-122">Visual Studio Express 2012 用于 Web 在添加脚手架项目后停止工作</span><span class="sxs-lookup"><span data-stu-id="bad06-122">Visual Studio Express 2012 for Web stops working after adding a scaffolded item</span></span>](#expressissue)
    - [<span data-ttu-id="bad06-123">ASP.NET剃刀 3</span><span class="sxs-lookup"><span data-stu-id="bad06-123">ASP.NET Razor 3</span></span>](#issuerazor)

        - [<span data-ttu-id="bad06-124">使用"使用"或"F5"查看 cshtml 文件会导致服务器错误</span><span class="sxs-lookup"><span data-stu-id="bad06-124">Viewing cshtml file with Browse With or F5 causes a server error</span></span>](#browseissue)
        - [<span data-ttu-id="bad06-125">Url 重写和蒂尔德 （\*）</span><span class="sxs-lookup"><span data-stu-id="bad06-125">Url Rewrite and Tilde(~)</span></span>](#rewriteissue)
    - [<span data-ttu-id="bad06-126">模板</span><span class="sxs-lookup"><span data-stu-id="bad06-126">Templates</span></span>](#templateissue)

<a id="install"></a>
## <a name="installation-notes"></a><span data-ttu-id="bad06-127">安装说明</span><span class="sxs-lookup"><span data-stu-id="bad06-127">Installation Notes</span></span>

<span data-ttu-id="bad06-128">[安装](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WebNode11Pack.appids)ASP.NET和网络工具 2013.1 用于视觉工作室 2012。</span><span class="sxs-lookup"><span data-stu-id="bad06-128">[Install](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WebNode11Pack.appids) ASP.NET and Web Tools 2013.1 for Visual Studio 2012.</span></span>

<a id="requirements"></a>
## <a name="software-requirements"></a><span data-ttu-id="bad06-129">软件要求</span><span class="sxs-lookup"><span data-stu-id="bad06-129">Software Requirements</span></span>

<span data-ttu-id="bad06-130">您必须有 Visual Studio 2012 或 Visual Studio Express 2012 用于 Web。</span><span class="sxs-lookup"><span data-stu-id="bad06-130">You must have either Visual Studio 2012 or Visual Studio Express 2012 for Web.</span></span>

## <a name="new-features-in-aspnet-and-web-tools-20131-for-visual-studio-2012"></a><span data-ttu-id="bad06-131">视觉工作室 2012 年 ASP.NET 和网络工具 2013.1 中的新功能</span><span class="sxs-lookup"><span data-stu-id="bad06-131">New Features in ASP.NET and Web Tools 2013.1 for Visual Studio 2012</span></span>

<a id="bootstrap"></a>
### <a name="bootstrap"></a><span data-ttu-id="bad06-132">Bootstrap</span><span class="sxs-lookup"><span data-stu-id="bad06-132">Bootstrap</span></span>

<span data-ttu-id="bad06-133">当您脚手架 MVC 5 控制器和视图时，视图的标记使用[Bootstrap](http://getbootstrap.com/)。</span><span class="sxs-lookup"><span data-stu-id="bad06-133">When you scaffold MVC 5 controllers and views, the markup for the views uses [Bootstrap](http://getbootstrap.com/).</span></span>

<a id="templates"></a>
### <a name="templates"></a><span data-ttu-id="bad06-134">模板</span><span class="sxs-lookup"><span data-stu-id="bad06-134">Templates</span></span>

<a id="mvc5template"></a>
#### <a name="aspnet-mvc-5-template"></a><span data-ttu-id="bad06-135">ASP.NET MVC 5 模板</span><span class="sxs-lookup"><span data-stu-id="bad06-135">ASP.NET MVC 5 template</span></span>

<span data-ttu-id="bad06-136">我们添加了一个新的 MVC 5 模板。</span><span class="sxs-lookup"><span data-stu-id="bad06-136">We added a new MVC 5 template.</span></span> <span data-ttu-id="bad06-137">它引用最新的 MVC 5 NuGet 包，您可以使用基架添加控制器和视图。</span><span class="sxs-lookup"><span data-stu-id="bad06-137">It references the latest MVC 5 NuGet packages, and you can use scaffolding to add controllers and views.</span></span>

<a id="apitemplate"></a>
#### <a name="aspnet-web-api-2-template"></a><span data-ttu-id="bad06-138">ASP.NET Web API 2 模板</span><span class="sxs-lookup"><span data-stu-id="bad06-138">ASP.NET Web API 2 template</span></span>

<span data-ttu-id="bad06-139">我们添加了一个新的 Web API 2 模板。</span><span class="sxs-lookup"><span data-stu-id="bad06-139">We added a new Web API 2 template.</span></span> <span data-ttu-id="bad06-140">它引用最新的 Web API 2 NuGet 包，您可以使用基架添加控制器和视图。</span><span class="sxs-lookup"><span data-stu-id="bad06-140">It references the latest Web API 2 NuGet packages, and you can use scaffolding to add controllers and views.</span></span>

<a id="itemtemplate"></a>
#### <a name="item-templates"></a><span data-ttu-id="bad06-141">项模板</span><span class="sxs-lookup"><span data-stu-id="bad06-141">Item Templates</span></span>

<span data-ttu-id="bad06-142">我们为 MVC 5 视图、网页 （Razor 3） 和 Web API 2 控制器添加了新的项目模板。</span><span class="sxs-lookup"><span data-stu-id="bad06-142">We added new item templates for MVC 5 views, Web Pages (Razor 3), and Web API 2 controllers.</span></span> <span data-ttu-id="bad06-143">他们在添加新项的同时，将相关的 NuGet 包安装到项目中。</span><span class="sxs-lookup"><span data-stu-id="bad06-143">They install the related NuGet packages to the project while adding new items.</span></span>

<a id="ef6"></a>
### <a name="entity-framework-6"></a><span data-ttu-id="bad06-144">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="bad06-144">Entity Framework 6</span></span>

<span data-ttu-id="bad06-145">当您使用实体框架构建 MVC 或 Web API 控制器时，我们使用框架 6。</span><span class="sxs-lookup"><span data-stu-id="bad06-145">When you scaffold an MVC or Web API controller using Entity Framework, we use Framework 6.</span></span> <span data-ttu-id="bad06-146">有关实体框架的详细信息，请参阅[实体框架版本历史记录](https://msdn.com/data/jj574253)。</span><span class="sxs-lookup"><span data-stu-id="bad06-146">For more information about Entity Framework, see the [Entity Framework Version History](https://msdn.com/data/jj574253).</span></span>

<span data-ttu-id="bad06-147">您还可以下载并安装可视化工作室的实体框架 6 工具 2012。</span><span class="sxs-lookup"><span data-stu-id="bad06-147">You can also download and install the Entity Framework 6 Tools for Visual Studio 2012.</span></span> <span data-ttu-id="bad06-148">请参阅[获取实体框架](https://msdn.com/data/ee712906#tooling)。</span><span class="sxs-lookup"><span data-stu-id="bad06-148">See the [Get Entity Framework](https://msdn.com/data/ee712906#tooling).</span></span>

<a id="scaffold"></a>
### <a name="aspnet-scaffolding"></a><span data-ttu-id="bad06-149">ASP.NET脚手架</span><span class="sxs-lookup"><span data-stu-id="bad06-149">ASP.NET Scaffolding</span></span>

<span data-ttu-id="bad06-150">ASP.NET基架是ASP.NET Web 应用程序的代码生成框架。</span><span class="sxs-lookup"><span data-stu-id="bad06-150">ASP.NET Scaffolding is a code generation framework for ASP.NET Web applications.</span></span> <span data-ttu-id="bad06-151">它可以轻松地向与数据模型交互的项目添加样板代码。</span><span class="sxs-lookup"><span data-stu-id="bad06-151">It makes it easy to add boilerplate code to your project that interacts with a data model.</span></span>

<span data-ttu-id="bad06-152">在 Visual Studio 的早期版本中，基架仅限于ASP.NET MVC 项目。</span><span class="sxs-lookup"><span data-stu-id="bad06-152">In previous versions of Visual Studio, scaffolding was limited to ASP.NET MVC projects.</span></span> <span data-ttu-id="bad06-153">使用此更新，您现在可以对任何ASP.NET项目（包括 Web 窗体）使用基架。</span><span class="sxs-lookup"><span data-stu-id="bad06-153">With this update, you can now use scaffolding for any ASP.NET project, including Web Forms.</span></span> <span data-ttu-id="bad06-154">此更新不支持为 Web 窗体项目生成页面，但仍可以通过向项目添加 MVC 依赖项来使用 Web 窗体的脚手架。</span><span class="sxs-lookup"><span data-stu-id="bad06-154">This update does not support generating pages for a Web Forms project, but you can still use scaffolding with Web Forms by adding MVC dependencies to the project.</span></span> <span data-ttu-id="bad06-155">将在将来的更新中添加对生成 Web 窗体页面的支持。</span><span class="sxs-lookup"><span data-stu-id="bad06-155">Support for generating pages for Web Forms will be added in a future update.</span></span>

<span data-ttu-id="bad06-156">使用基架时，我们确保在项目中安装了所有必需的依赖项。</span><span class="sxs-lookup"><span data-stu-id="bad06-156">When using scaffolding, we ensure that all required dependencies are installed in the project.</span></span> <span data-ttu-id="bad06-157">例如，如果从ASP.NET Web 窗体项目开始，然后使用基架添加 Web API 控制器，则所需的 NuGet 包和引用将自动添加到项目中。</span><span class="sxs-lookup"><span data-stu-id="bad06-157">For example, if you start with an ASP.NET Web Forms project and then use scaffolding to add a Web API Controller, the required NuGet packages and references are added to your project automatically.</span></span>

<span data-ttu-id="bad06-158">要将 MVC 基架添加到 Web 窗体项目，请添加新**的脚手架项**，并在对话框窗口中选择**MVC 5 依赖项**。</span><span class="sxs-lookup"><span data-stu-id="bad06-158">To add MVC scaffolding to a Web Forms project, add a **New Scaffolded Item** and select **MVC 5 Dependencies** in the dialog window.</span></span> <span data-ttu-id="bad06-159">基架 MVC 有两个选项;最小和完整。</span><span class="sxs-lookup"><span data-stu-id="bad06-159">There are two options for scaffolding MVC; Minimal and Full.</span></span> <span data-ttu-id="bad06-160">如果选择"最小"，则只有 ASP.NET MVC 的 NuGet 包和引用添加到项目中。</span><span class="sxs-lookup"><span data-stu-id="bad06-160">If you select Minimal, only the NuGet packages and references for ASP.NET MVC are added to your project.</span></span> <span data-ttu-id="bad06-161">如果选择"完整"选项，则添加最小依赖项以及 MVC 项目所需的内容文件。</span><span class="sxs-lookup"><span data-stu-id="bad06-161">If you select the Full option, the Minimal dependencies are added, as well as the required content files for an MVC project.</span></span>

<span data-ttu-id="bad06-162">支持基架异步控制器使用实体框架 6 中的新异步功能。</span><span class="sxs-lookup"><span data-stu-id="bad06-162">Support for scaffolding async controllers uses the new async features from Entity Framework 6.</span></span>

<span data-ttu-id="bad06-163">有关详细信息和教程，请参阅[ASP.NET脚手架概述](../2013/aspnet-scaffolding-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="bad06-163">For more information and tutorials, see [ASP.NET Scaffolding Overview](../2013/aspnet-scaffolding-overview.md).</span></span> <span data-ttu-id="bad06-164">这些教程显示了视觉工作室 2013 的脚手架，但它们也适用于 Visual Studio 2012 的ASP.NET和网络工具 2013.1。</span><span class="sxs-lookup"><span data-stu-id="bad06-164">These tutorials show scaffolding with Visual Studio 2013, but they are also applicable to ASP.NET and Web Tools 2013.1 for Visual Studio 2012.</span></span>

<a id="razor"></a>
### <a name="razor-editor"></a><span data-ttu-id="bad06-165">剃刀编辑器</span><span class="sxs-lookup"><span data-stu-id="bad06-165">Razor Editor</span></span>

<span data-ttu-id="bad06-166">有了这个更新，Visual Studio 2012 现在支持 Razor 3 工具/编辑。</span><span class="sxs-lookup"><span data-stu-id="bad06-166">With this update, Visual Studio 2012 now supports Razor 3 tooling/editing.</span></span>

<a id="nuget"></a>
### <a name="nuget-27"></a><span data-ttu-id="bad06-167">NuGet 2.7</span><span class="sxs-lookup"><span data-stu-id="bad06-167">NuGet 2.7</span></span>

<span data-ttu-id="bad06-168">NuGet 2.7 包含一组丰富的新功能，在[NuGet 2.7 发行说明](http://docs.nuget.org/docs/release-notes/nuget-2.7)中对此进行了详细介绍。</span><span class="sxs-lookup"><span data-stu-id="bad06-168">NuGet 2.7 includes a rich set of new features which are described in detail at [NuGet 2.7 Release Notes](http://docs.nuget.org/docs/release-notes/nuget-2.7).</span></span>

<span data-ttu-id="bad06-169">此版本的 NuGet 消除了用户显式允许 NuGet 还原缺少的包的需要。</span><span class="sxs-lookup"><span data-stu-id="bad06-169">This version of NuGet removes the need for users to explicitly allow NuGet to restore missing packages.</span></span> <span data-ttu-id="bad06-170">安装 NuGet 2.7 时，用户隐式同意自动还原丢失的包。</span><span class="sxs-lookup"><span data-stu-id="bad06-170">When installing NuGet 2.7, users implicitly consent to automatically restoring missing packages.</span></span> <span data-ttu-id="bad06-171">用户可以通过 Visual Studio 中的 NuGet 设置明确选择退出包恢复。</span><span class="sxs-lookup"><span data-stu-id="bad06-171">Users can explicitly opt out of package restoration through the NuGet settings in Visual Studio.</span></span> <span data-ttu-id="bad06-172">此更改简化了包还原的工作方式。</span><span class="sxs-lookup"><span data-stu-id="bad06-172">This change simplifies how package restoration works.</span></span>

## <a name="known-issues-and-breaking-changes"></a><span data-ttu-id="bad06-173">已知问题和重大更改</span><span class="sxs-lookup"><span data-stu-id="bad06-173">Known Issues and Breaking Changes</span></span>

<a id="issuescaffolding"></a>
### <a name="aspnet-scaffolding"></a><span data-ttu-id="bad06-174">ASP.NET脚手架</span><span class="sxs-lookup"><span data-stu-id="bad06-174">ASP.NET Scaffolding</span></span>

<a id="404issue"></a>
#### <a name="mvc-and-web-api-scaffolding---http-404-not-found-error"></a><span data-ttu-id="bad06-175">MVC 和 Web API 基架 - HTTP 404，未找到错误</span><span class="sxs-lookup"><span data-stu-id="bad06-175">MVC and Web API Scaffolding - HTTP 404, Not Found error</span></span>

<span data-ttu-id="bad06-176">如果在向项目添加基架项时遇到错误，则项目可能会处于不一致状态。</span><span class="sxs-lookup"><span data-stu-id="bad06-176">If you encounter an error when adding a scaffolded item to a project, it is possible your project will be left in an inconsistent state.</span></span> <span data-ttu-id="bad06-177">对基架所做的一些更改将回滚，但其他更改（如已安装的 NuGet 包）将不会回滚。</span><span class="sxs-lookup"><span data-stu-id="bad06-177">Some of the changes made be scaffolding will be rolled back but other changes, such as the installed NuGet packages, will not be rolled back.</span></span> <span data-ttu-id="bad06-178">如果路由配置更改回滚，则用户在导航到基架项目时将收到 HTTP 404 错误。</span><span class="sxs-lookup"><span data-stu-id="bad06-178">If the routing configuration changes are rolled back, users will receive an HTTP 404 error when navigating to scaffolded items.</span></span>

<span data-ttu-id="bad06-179">要修复 MVC 的此错误，请添加新的脚手架项并选择 MVC 5 依赖项（最小或完整）。</span><span class="sxs-lookup"><span data-stu-id="bad06-179">To fix this error for MVC, add a new scaffolded item and select MVC 5 Dependencies (either Minimal or Full).</span></span> <span data-ttu-id="bad06-180">此过程将添加项目所需的所有更改。</span><span class="sxs-lookup"><span data-stu-id="bad06-180">This process will add all of the required changes to your project.</span></span>

<span data-ttu-id="bad06-181">要修复 Web API 的此错误，本文：</span><span class="sxs-lookup"><span data-stu-id="bad06-181">To fix this error for Web API:</span></span>

1. <span data-ttu-id="bad06-182">将以下 WebApiConfig 类添加到项目中。</span><span class="sxs-lookup"><span data-stu-id="bad06-182">Add the following WebApiConfig class to your project.</span></span>

    [!code-csharp[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample1.cs)]

    [!code-vb[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample2.vb)]
2. <span data-ttu-id="bad06-183">在 Global.asax 中的应用程序\_启动方法中配置 WebApiConfig.注册，如下所示：</span><span class="sxs-lookup"><span data-stu-id="bad06-183">Configure WebApiConfig.Register in the Application\_Start method in Global.asax as follows:</span></span>

    [!code-csharp[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample3.cs)]

    [!code-vb[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample4.vb)]

<a id="expressissue"></a>
#### <a name="visual-studio-express-2012-for-web-stops-working-after-adding-a-scaffolded-item"></a><span data-ttu-id="bad06-184">Visual Studio Express 2012 用于 Web 在添加脚手架项目后停止工作</span><span class="sxs-lookup"><span data-stu-id="bad06-184">Visual Studio Express 2012 for Web stops working after adding a scaffolded item</span></span>

<span data-ttu-id="bad06-185">如果 Web 的 Visual Studio Express 2012 在使用实体框架添加基架项目（例如 Web API 2 控制器具有操作的操作，使用实体框架）后停止工作，则 Visual Studio Express 可能无法加载依赖于 System.Web.扩展的程序集的本机映像。</span><span class="sxs-lookup"><span data-stu-id="bad06-185">If Visual Studio Express 2012 for Web stops working after adding scaffolded item with Entity Framework (such as Web API 2 Controller with actions, using Entity Framework), it is possible that Visual Studio Express failed to load the native image of an assembly dependent on System.Web.Extensions.</span></span>

<span data-ttu-id="bad06-186">要更正此问题，请将 Visual Studio Express 配置为使用 System.Web.扩展的 MSIL 映像：</span><span class="sxs-lookup"><span data-stu-id="bad06-186">To correct this problem, configure Visual Studio Express to work with the MSIL image of System.Web.Extensions:</span></span>

1. <span data-ttu-id="bad06-187">在管理员模式下打开命令提示。</span><span class="sxs-lookup"><span data-stu-id="bad06-187">Open Command Prompt in the Administrator mode.</span></span>
2. <span data-ttu-id="bad06-188">转到 %程序文件%\微软视觉工作室 11.0_Common7_IDE 或 %程序文件 （x86）%\微软视觉工作室 11.0_Common7_IDE （对于 64 位窗口）。</span><span class="sxs-lookup"><span data-stu-id="bad06-188">Go to %ProgramFiles%\Microsoft Visual Studio 11.0\Common7\IDE or %ProgramFiles(x86)%\Microsoft Visual Studio 11.0\Common7\IDE (for 64 bit Windows).</span></span>
3. <span data-ttu-id="bad06-189">在文本编辑器中打开 VWDExpress.exe.config。</span><span class="sxs-lookup"><span data-stu-id="bad06-189">Open VWDExpress.exe.config in a text editor.</span></span>
4. <span data-ttu-id="bad06-190">在&lt;&gt;/配置&lt;运行时&gt;元素下添加以下行：</span><span class="sxs-lookup"><span data-stu-id="bad06-190">Add the following line under the &lt;configuration&gt;/&lt;runtime&gt; element:</span></span>  

    [!code-xml[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample5.xml)]
5. <span data-ttu-id="bad06-191">重新启动可视化工作室快速 2012 为 Web.</span><span class="sxs-lookup"><span data-stu-id="bad06-191">Restart Visual Studio Express 2012 for Web.</span></span>

<a id="issuerazor"></a>
### <a name="aspnet-razor-3"></a><span data-ttu-id="bad06-192">ASP.NET剃刀 3</span><span class="sxs-lookup"><span data-stu-id="bad06-192">ASP.NET Razor 3</span></span>

<a id="browseissue"></a>
#### <a name="viewing-cshtml-file-with-browse-with-or-f5-causes-a-server-error"></a><span data-ttu-id="bad06-193">使用"使用"或"F5"查看 cshtml 文件会导致服务器错误</span><span class="sxs-lookup"><span data-stu-id="bad06-193">Viewing cshtml file with Browse With or F5 causes a server error</span></span>

<span data-ttu-id="bad06-194">当您在 Visual Studio 2012 中创建 MVC 5 项目（或在 Visual Studio 2012 中打开在 Visual Studio 2013 中创建的 MVC 5 项目）并尝试使用"浏览"或 F5 查看 cshtml 文件时，您将收到一个错误，指出 **"/' 应用程序中的服务器错误**"。</span><span class="sxs-lookup"><span data-stu-id="bad06-194">When you create an MVC 5 project in Visual Studio 2012 (or open in Visual Studio 2012 an MVC 5 project that was created in Visual Studio 2013) and attempt to view a cshtml file by using Browse With or F5, you will receive an error that states - **Server Error in '/' Application**.</span></span> <span data-ttu-id="bad06-195">服务器尝试导航到`http://localhost:XXXX/Views/../XXXX.cshtml`</span><span class="sxs-lookup"><span data-stu-id="bad06-195">The server attempts to navigate to `http://localhost:XXXX/Views/../XXXX.cshtml`</span></span>

<span data-ttu-id="bad06-196">要解决此问题，请将项目中的 **"开始操作"** 设置更改为 **"特定页面**"。</span><span class="sxs-lookup"><span data-stu-id="bad06-196">To resolve this issue, change the **Start Action** setting in your project to **Specific Page**.</span></span> <span data-ttu-id="bad06-197">您无需为页面提供值。</span><span class="sxs-lookup"><span data-stu-id="bad06-197">You do not need to provide a value for the page.</span></span>

![](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image1.png)

<span data-ttu-id="bad06-198">进行此更改后，选择 F5 将导航到应用程序的根目录`http://localhost:XXXX`（ 。</span><span class="sxs-lookup"><span data-stu-id="bad06-198">After making this change, selecting F5 navigates to the root of your application (`http://localhost:XXXX`).</span></span> <span data-ttu-id="bad06-199">此行为与 Visual Studio 2013 中的 MVC 5 项目的行为不同，其中 **"当前页面"** 设置将启动打开页面。</span><span class="sxs-lookup"><span data-stu-id="bad06-199">This behavior is not the same as the behavior for MVC 5 projects in Visual Studio 2013, where the **Current Page** setting launches the open page.</span></span>

<a id="rewriteissue"></a>
#### <a name="url-rewrite-and-tilde"></a><span data-ttu-id="bad06-200">Url 重写和蒂尔德 （\*）</span><span class="sxs-lookup"><span data-stu-id="bad06-200">Url Rewrite and Tilde(~)</span></span>

<span data-ttu-id="bad06-201">升级到ASP.NET Razor 3 或 ASP.NET MVC 5 后，如果使用 URL 重写，则波浪（\*）表示法可能不再正常工作。</span><span class="sxs-lookup"><span data-stu-id="bad06-201">After upgrading to ASP.NET Razor 3 or ASP.NET MVC 5, the tilde(~) notation may no longer work correctly if you are using URL rewrites.</span></span> <span data-ttu-id="bad06-202">URL 重写会影响 HTML&lt;元素（如 A/、SCRIPT/、LINK/&gt;&lt;&gt;&lt;&gt;等）中的波浪线（\*）表示法，因此波浪线不再映射到根目录。</span><span class="sxs-lookup"><span data-stu-id="bad06-202">The URL rewrite affects the tilde(~) notation in HTML elements such as &lt;A/&gt;, &lt;SCRIPT/&gt;, &lt;LINK/&gt;, and as a result the tilde no longer maps to the root directory.</span></span>

<span data-ttu-id="bad06-203">例如，如果将**asp.net/content**请求重写为**asp.net，**&lt;则 a href_"/内容/"中的 href 属性将&gt;解析为 **/内容/内容/** 而不是**/**。</span><span class="sxs-lookup"><span data-stu-id="bad06-203">For example, if you rewrite requests for **asp.net/content** to **asp.net**, the href attribute in &lt;A href="~/content/"/&gt; resolves to **/content/content/** instead of **/**.</span></span> <span data-ttu-id="bad06-204">要禁止此更改，可以在每个网页或 Global.asax 中的**\_应用程序 BeginRequest**中将**IIS\_WasUrl 重写**上下文设置为 false。</span><span class="sxs-lookup"><span data-stu-id="bad06-204">To suppress this change, you can set the **IIS\_WasUrlRewritten** context to false in each Web Page or in **Application\_BeginRequest** in Global.asax.</span></span>

<a id="templateissue"></a>
### <a name="templates"></a><span data-ttu-id="bad06-205">模板</span><span class="sxs-lookup"><span data-stu-id="bad06-205">Templates</span></span>

<span data-ttu-id="bad06-206">当您在 Windows 8.1 或 Windows Server 2012 R2 上使用 Visual Studio 2012 创建 ASP.NET MVC 项目时，Visual Studio 会显示一条错误消息，指出"为 ASP.NET 4.5 配置 Web [url] 失败"。</span><span class="sxs-lookup"><span data-stu-id="bad06-206">When you create ASP.NET MVC projects with Visual Studio 2012 on Windows 8.1 or Windows Server 2012 R2, Visual Studio displays an error message that states "Configuring Web [url] for ASP.NET 4.5 failed."</span></span>

![配置错误](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image2.png)

<span data-ttu-id="bad06-208">您会看到此错误，因为 Visual Studio 2012 在 Windows 这些版本上安装时不会启用ASP.NET 4.5 功能。</span><span class="sxs-lookup"><span data-stu-id="bad06-208">You see this error because Visual Studio 2012 does not enable the ASP.NET 4.5 feature when it is installed on those releases of Windows.</span></span> <span data-ttu-id="bad06-209">要启用 ASP.NET 4.5，请执行打开[或关闭"打开"Windows 功能](https://windows.microsoft.com/windows-8/turn-windows-features-on-off)中描述的步骤。</span><span class="sxs-lookup"><span data-stu-id="bad06-209">To enable ASP.NET 4.5, perform the steps described in [Turn Windows features on or off](https://windows.microsoft.com/windows-8/turn-windows-features-on-off).</span></span>

![打开或关闭 Windows 功能](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image3.png)

<span data-ttu-id="bad06-211">或者，您可以通过命令行启用ASP.NET 4.5。</span><span class="sxs-lookup"><span data-stu-id="bad06-211">Alternatively, you can enable ASP.NET 4.5 through the command line.</span></span>

1. <span data-ttu-id="bad06-212">在管理员模式下打开命令提示。</span><span class="sxs-lookup"><span data-stu-id="bad06-212">Open Command Prompt in the Administrator mode.</span></span>
2. <span data-ttu-id="bad06-213">运行以下命令以启用 ASP.NET 4.5。</span><span class="sxs-lookup"><span data-stu-id="bad06-213">Run the following command to enable ASP.NET 4.5.</span></span>  
    `dism /Online /Enable-Feature /FeatureName:NetFx4Extended-ASPNET45 /Quiet /NoRestart`

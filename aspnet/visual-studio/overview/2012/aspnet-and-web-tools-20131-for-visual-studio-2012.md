---
uid: visual-studio/overview/2012/aspnet-and-web-tools-20131-for-visual-studio-2012
title: 适用于 ASP.NET 和 Web 工具 2013.1 适用于 Visual Studio 2012 发行说明 |Microsoft Docs
author: microsoft
description: 本文档介绍 ASP.NET 和 Web 工具 2013.1 for Visual Studio 2012 的版本。
ms.author: riande
ms.date: 11/13/2013
ms.assetid: ca26e5bb-630e-41d2-8512-2a9386c431cb
msc.legacyurl: /visual-studio/overview/2012/aspnet-and-web-tools-20131-for-visual-studio-2012
msc.type: authoredcontent
ms.openlocfilehash: 260af1018064d60d80cbb1002001f28c4daffffd
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/06/2019
ms.locfileid: "65126159"
---
# <a name="release-notes-for-aspnet-and-web-tools-20131-for-visual-studio-2012"></a><span data-ttu-id="c261e-103">适用于 Visual Studio 2012 的 ASP.NET 和 Web 工具 2013.1 发行说明</span><span class="sxs-lookup"><span data-stu-id="c261e-103">Release Notes for ASP.NET and Web Tools 2013.1 for Visual Studio 2012</span></span>

<span data-ttu-id="c261e-104">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="c261e-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="c261e-105">本文档介绍 ASP.NET 和 Web 工具 2013.1 for Visual Studio 2012 的版本。</span><span class="sxs-lookup"><span data-stu-id="c261e-105">This document describes the release of ASP.NET and Web Tools 2013.1 for Visual Studio 2012.</span></span>

## <a name="contents"></a><span data-ttu-id="c261e-106">内容</span><span class="sxs-lookup"><span data-stu-id="c261e-106">Contents</span></span>

- [<span data-ttu-id="c261e-107">安装说明</span><span class="sxs-lookup"><span data-stu-id="c261e-107">Installation Notes</span></span>](#install)
- [<span data-ttu-id="c261e-108">软件要求</span><span class="sxs-lookup"><span data-stu-id="c261e-108">Software Requirements</span></span>](#requirements)
- <span data-ttu-id="c261e-109">ASP.NET 和 Web 工具 2013.1 适用于 Visual Studio 2012 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="c261e-109">New Features in ASP.NET and Web Tools 2013.1 for Visual Studio 2012</span></span>

    - [<span data-ttu-id="c261e-110">Bootstrap</span><span class="sxs-lookup"><span data-stu-id="c261e-110">Bootstrap</span></span>](#bootstrap)
    - [<span data-ttu-id="c261e-111">模板</span><span class="sxs-lookup"><span data-stu-id="c261e-111">Templates</span></span>](#templates)

        - [<span data-ttu-id="c261e-112">ASP.NET MVC 5 模板</span><span class="sxs-lookup"><span data-stu-id="c261e-112">ASP.NET MVC 5 template</span></span>](#mvc5template)
        - [<span data-ttu-id="c261e-113">ASP.NET Web API 2 模板</span><span class="sxs-lookup"><span data-stu-id="c261e-113">ASP.NET Web API 2 template</span></span>](#apitemplate)
        - [<span data-ttu-id="c261e-114">项模板</span><span class="sxs-lookup"><span data-stu-id="c261e-114">Item Templates</span></span>](#itemtemplate)
    - [<span data-ttu-id="c261e-115">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="c261e-115">Entity Framework 6</span></span>](#ef6)
    - [<span data-ttu-id="c261e-116">ASP.NET 基架</span><span class="sxs-lookup"><span data-stu-id="c261e-116">ASP.NET Scaffolding</span></span>](#scaffold)
    - [<span data-ttu-id="c261e-117">Razor Editor</span><span class="sxs-lookup"><span data-stu-id="c261e-117">Razor Editor</span></span>](#razor)
    - [<span data-ttu-id="c261e-118">NuGet 2.7</span><span class="sxs-lookup"><span data-stu-id="c261e-118">NuGet 2.7</span></span>](#nuget)
- <span data-ttu-id="c261e-119">已知的问题和重大更改</span><span class="sxs-lookup"><span data-stu-id="c261e-119">Known Issues and Breaking Changes</span></span>

    - [<span data-ttu-id="c261e-120">ASP.NET 基架</span><span class="sxs-lookup"><span data-stu-id="c261e-120">ASP.NET Scaffolding</span></span>](#issuescaffolding)

        - [<span data-ttu-id="c261e-121">MVC 和 Web API 基架-HTTP 404 找不到错误</span><span class="sxs-lookup"><span data-stu-id="c261e-121">MVC and Web API Scaffolding - HTTP 404, Not Found error</span></span>](#404issue)
        - [<span data-ttu-id="c261e-122">Visual Studio Express 2012 for Web 添加基架的项后停止工作</span><span class="sxs-lookup"><span data-stu-id="c261e-122">Visual Studio Express 2012 for Web stops working after adding a scaffolded item</span></span>](#expressissue)
    - [<span data-ttu-id="c261e-123">ASP.NET Razor 3</span><span class="sxs-lookup"><span data-stu-id="c261e-123">ASP.NET Razor 3</span></span>](#issuerazor)

        - [<span data-ttu-id="c261e-124">查看使用浏览方式或 F5 的 cshtml 文件会导致服务器错误</span><span class="sxs-lookup"><span data-stu-id="c261e-124">Viewing cshtml file with Browse With or F5 causes a server error</span></span>](#browseissue)
        - [<span data-ttu-id="c261e-125">Url 重写和 Tilde(~)</span><span class="sxs-lookup"><span data-stu-id="c261e-125">Url Rewrite and Tilde(~)</span></span>](#rewriteissue)
    - [<span data-ttu-id="c261e-126">模板</span><span class="sxs-lookup"><span data-stu-id="c261e-126">Templates</span></span>](#templateissue)

<a id="install"></a>
## <a name="installation-notes"></a><span data-ttu-id="c261e-127">安装说明</span><span class="sxs-lookup"><span data-stu-id="c261e-127">Installation Notes</span></span>

<span data-ttu-id="c261e-128">[安装](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WebNode11Pack.appids)ASP.NET 和 Web 工具 2013.1 适用于 Visual Studio 2012。</span><span class="sxs-lookup"><span data-stu-id="c261e-128">[Install](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WebNode11Pack.appids) ASP.NET and Web Tools 2013.1 for Visual Studio 2012.</span></span>

<a id="requirements"></a>
## <a name="software-requirements"></a><span data-ttu-id="c261e-129">软件要求</span><span class="sxs-lookup"><span data-stu-id="c261e-129">Software Requirements</span></span>

<span data-ttu-id="c261e-130">您必须具有 Visual Studio 2012 或 Visual Studio Express 2012 for Web。</span><span class="sxs-lookup"><span data-stu-id="c261e-130">You must have either Visual Studio 2012 or Visual Studio Express 2012 for Web.</span></span>

## <a name="new-features-in-aspnet-and-web-tools-20131-for-visual-studio-2012"></a><span data-ttu-id="c261e-131">ASP.NET 和 Web 工具 2013.1 适用于 Visual Studio 2012 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="c261e-131">New Features in ASP.NET and Web Tools 2013.1 for Visual Studio 2012</span></span>

<a id="bootstrap"></a>
### <a name="bootstrap"></a><span data-ttu-id="c261e-132">Bootstrap</span><span class="sxs-lookup"><span data-stu-id="c261e-132">Bootstrap</span></span>

<span data-ttu-id="c261e-133">当你创建的基架 MVC 5 控制器和视图时，视图的标记使用[Bootstrap](http://getbootstrap.com/)。</span><span class="sxs-lookup"><span data-stu-id="c261e-133">When you scaffold MVC 5 controllers and views, the markup for the views uses [Bootstrap](http://getbootstrap.com/).</span></span>

<a id="templates"></a>
### <a name="templates"></a><span data-ttu-id="c261e-134">模板</span><span class="sxs-lookup"><span data-stu-id="c261e-134">Templates</span></span>

<a id="mvc5template"></a>
#### <a name="aspnet-mvc-5-template"></a><span data-ttu-id="c261e-135">ASP.NET MVC 5 模板</span><span class="sxs-lookup"><span data-stu-id="c261e-135">ASP.NET MVC 5 template</span></span>

<span data-ttu-id="c261e-136">我们添加了新的 MVC 5 模板。</span><span class="sxs-lookup"><span data-stu-id="c261e-136">We added a new MVC 5 template.</span></span> <span data-ttu-id="c261e-137">它引用最新的 MVC 5 NuGet 包，并可以使用基架添加控制器和视图。</span><span class="sxs-lookup"><span data-stu-id="c261e-137">It references the latest MVC 5 NuGet packages, and you can use scaffolding to add controllers and views.</span></span>

<a id="apitemplate"></a>
#### <a name="aspnet-web-api-2-template"></a><span data-ttu-id="c261e-138">ASP.NET Web API 2 模板</span><span class="sxs-lookup"><span data-stu-id="c261e-138">ASP.NET Web API 2 template</span></span>

<span data-ttu-id="c261e-139">我们添加了新的 Web API 2 模板。</span><span class="sxs-lookup"><span data-stu-id="c261e-139">We added a new Web API 2 template.</span></span> <span data-ttu-id="c261e-140">它引用最新的 Web API 2 NuGet 包，并可以使用基架添加控制器和视图。</span><span class="sxs-lookup"><span data-stu-id="c261e-140">It references the latest Web API 2 NuGet packages, and you can use scaffolding to add controllers and views.</span></span>

<a id="itemtemplate"></a>
#### <a name="item-templates"></a><span data-ttu-id="c261e-141">项模板</span><span class="sxs-lookup"><span data-stu-id="c261e-141">Item Templates</span></span>

<span data-ttu-id="c261e-142">我们添加了新项模板的 MVC 5 视图、 网页 (Razor 3) 和 Web API 2 控制器。</span><span class="sxs-lookup"><span data-stu-id="c261e-142">We added new item templates for MVC 5 views, Web Pages (Razor 3), and Web API 2 controllers.</span></span> <span data-ttu-id="c261e-143">在添加新项时相关的 NuGet 包安装到项目。</span><span class="sxs-lookup"><span data-stu-id="c261e-143">They install the related NuGet packages to the project while adding new items.</span></span>

<a id="ef6"></a>
### <a name="entity-framework-6"></a><span data-ttu-id="c261e-144">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="c261e-144">Entity Framework 6</span></span>

<span data-ttu-id="c261e-145">当您创建基架 MVC 或 Web API 控制器使用 Entity Framework 时，我们使用 Framework 6。</span><span class="sxs-lookup"><span data-stu-id="c261e-145">When you scaffold an MVC or Web API controller using Entity Framework, we use Framework 6.</span></span> <span data-ttu-id="c261e-146">有关实体框架的详细信息，请参阅[Entity Framework 版本历史记录](https://msdn.com/data/jj574253)。</span><span class="sxs-lookup"><span data-stu-id="c261e-146">For more information about Entity Framework, see the [Entity Framework Version History](https://msdn.com/data/jj574253).</span></span>

<span data-ttu-id="c261e-147">您还可以下载并安装用于 Visual Studio 2012 的 Entity Framework 6 工具。</span><span class="sxs-lookup"><span data-stu-id="c261e-147">You can also download and install the Entity Framework 6 Tools for Visual Studio 2012.</span></span> <span data-ttu-id="c261e-148">请参阅[获取实体框架](https://msdn.com/data/ee712906#tooling)。</span><span class="sxs-lookup"><span data-stu-id="c261e-148">See the [Get Entity Framework](https://msdn.com/data/ee712906#tooling).</span></span>

<a id="scaffold"></a>
### <a name="aspnet-scaffolding"></a><span data-ttu-id="c261e-149">ASP.NET 基架</span><span class="sxs-lookup"><span data-stu-id="c261e-149">ASP.NET Scaffolding</span></span>

<span data-ttu-id="c261e-150">ASP.NET 基架是用于 ASP.NET Web 应用程序的代码生成框架。</span><span class="sxs-lookup"><span data-stu-id="c261e-150">ASP.NET Scaffolding is a code generation framework for ASP.NET Web applications.</span></span> <span data-ttu-id="c261e-151">它可以轻松地将样板代码添加到项目中使用的数据模型进行交互。</span><span class="sxs-lookup"><span data-stu-id="c261e-151">It makes it easy to add boilerplate code to your project that interacts with a data model.</span></span>

<span data-ttu-id="c261e-152">在以前版本的 Visual Studio 中，基架被限制为 ASP.NET MVC 项目。</span><span class="sxs-lookup"><span data-stu-id="c261e-152">In previous versions of Visual Studio, scaffolding was limited to ASP.NET MVC projects.</span></span> <span data-ttu-id="c261e-153">利用此更新，现在可以用于任何 ASP.NET 项目，包括 Web 窗体中使用基架。</span><span class="sxs-lookup"><span data-stu-id="c261e-153">With this update, you can now use scaffolding for any ASP.NET project, including Web Forms.</span></span> <span data-ttu-id="c261e-154">此更新不支持的 Web 窗体项目，生成页，但您仍可以使用基架，Web 窗体通过向项目添加 MVC 依赖项。</span><span class="sxs-lookup"><span data-stu-id="c261e-154">This update does not support generating pages for a Web Forms project, but you can still use scaffolding with Web Forms by adding MVC dependencies to the project.</span></span> <span data-ttu-id="c261e-155">将在未来更新中添加对生成的 Web 窗体页的支持。</span><span class="sxs-lookup"><span data-stu-id="c261e-155">Support for generating pages for Web Forms will be added in a future update.</span></span>

<span data-ttu-id="c261e-156">在使用基架，我们确保所有必需的依赖项安装在项目中。</span><span class="sxs-lookup"><span data-stu-id="c261e-156">When using scaffolding, we ensure that all required dependencies are installed in the project.</span></span> <span data-ttu-id="c261e-157">例如，如果您开始创建 ASP.NET Web 窗体项目，然后使用基架添加 Web API 控制器，所需的 NuGet 包和引用将自动添加到你的项目。</span><span class="sxs-lookup"><span data-stu-id="c261e-157">For example, if you start with an ASP.NET Web Forms project and then use scaffolding to add a Web API Controller, the required NuGet packages and references are added to your project automatically.</span></span>

<span data-ttu-id="c261e-158">若要将 MVC 基架添加到 Web 窗体项目，添加**新基架项**，然后选择**MVC 5 依赖项**在对话框窗口中。</span><span class="sxs-lookup"><span data-stu-id="c261e-158">To add MVC scaffolding to a Web Forms project, add a **New Scaffolded Item** and select **MVC 5 Dependencies** in the dialog window.</span></span> <span data-ttu-id="c261e-159">有两个选项基架 MVC;最小和完全。</span><span class="sxs-lookup"><span data-stu-id="c261e-159">There are two options for scaffolding MVC; Minimal and Full.</span></span> <span data-ttu-id="c261e-160">如果你选择最小，NuGet 包和 ASP.NET MVC 的引用添加到你的项目。</span><span class="sxs-lookup"><span data-stu-id="c261e-160">If you select Minimal, only the NuGet packages and references for ASP.NET MVC are added to your project.</span></span> <span data-ttu-id="c261e-161">如果选择完全选项，添加最小依赖项，以及对于 MVC 项目所需的内容文件。</span><span class="sxs-lookup"><span data-stu-id="c261e-161">If you select the Full option, the Minimal dependencies are added, as well as the required content files for an MVC project.</span></span>

<span data-ttu-id="c261e-162">对基架异步控制器的支持使用从 Entity Framework 6 的新异步功能。</span><span class="sxs-lookup"><span data-stu-id="c261e-162">Support for scaffolding async controllers uses the new async features from Entity Framework 6.</span></span>

<span data-ttu-id="c261e-163">有关详细信息和教程，请参阅[ASP.NET 基架概述](../2013/aspnet-scaffolding-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="c261e-163">For more information and tutorials, see [ASP.NET Scaffolding Overview](../2013/aspnet-scaffolding-overview.md).</span></span> <span data-ttu-id="c261e-164">这些教程介绍基架使用 Visual Studio 2013，但它们也适用于 ASP.NET 和 Web 工具 2013.1 适用于 Visual Studio 2012。</span><span class="sxs-lookup"><span data-stu-id="c261e-164">These tutorials show scaffolding with Visual Studio 2013, but they are also applicable to ASP.NET and Web Tools 2013.1 for Visual Studio 2012.</span></span>

<a id="razor"></a>
### <a name="razor-editor"></a><span data-ttu-id="c261e-165">Razor Editor</span><span class="sxs-lookup"><span data-stu-id="c261e-165">Razor Editor</span></span>

<span data-ttu-id="c261e-166">利用此更新，Visual Studio 2012 现在支持 Razor 3 工具/编辑。</span><span class="sxs-lookup"><span data-stu-id="c261e-166">With this update, Visual Studio 2012 now supports Razor 3 tooling/editing.</span></span>

<a id="nuget"></a>
### <a name="nuget-27"></a><span data-ttu-id="c261e-167">NuGet 2.7</span><span class="sxs-lookup"><span data-stu-id="c261e-167">NuGet 2.7</span></span>

<span data-ttu-id="c261e-168">NuGet 2.7 包括一套丰富的新功能描述了这些详细的介绍[NuGet 2.7 发行说明](http://docs.nuget.org/docs/release-notes/nuget-2.7)。</span><span class="sxs-lookup"><span data-stu-id="c261e-168">NuGet 2.7 includes a rich set of new features which are described in detail at [NuGet 2.7 Release Notes](http://docs.nuget.org/docs/release-notes/nuget-2.7).</span></span>

<span data-ttu-id="c261e-169">此版本的 NuGet 不再需要用户显式允许 NuGet 还原缺失的包。</span><span class="sxs-lookup"><span data-stu-id="c261e-169">This version of NuGet removes the need for users to explicitly allow NuGet to restore missing packages.</span></span> <span data-ttu-id="c261e-170">在安装时 NuGet 2.7，用户隐式同意自动还原缺失的包。</span><span class="sxs-lookup"><span data-stu-id="c261e-170">When installing NuGet 2.7, users implicitly consent to automatically restoring missing packages.</span></span> <span data-ttu-id="c261e-171">用户可以显式选择不通过 Visual Studio 中的 NuGet 设置包还原。</span><span class="sxs-lookup"><span data-stu-id="c261e-171">Users can explicitly opt out of package restoration through the NuGet settings in Visual Studio.</span></span> <span data-ttu-id="c261e-172">此更改，简化了包还原的工作原理。</span><span class="sxs-lookup"><span data-stu-id="c261e-172">This change simplifies how package restoration works.</span></span>

## <a name="known-issues-and-breaking-changes"></a><span data-ttu-id="c261e-173">已知的问题和重大更改</span><span class="sxs-lookup"><span data-stu-id="c261e-173">Known Issues and Breaking Changes</span></span>

<a id="issuescaffolding"></a>
### <a name="aspnet-scaffolding"></a><span data-ttu-id="c261e-174">ASP.NET 基架</span><span class="sxs-lookup"><span data-stu-id="c261e-174">ASP.NET Scaffolding</span></span>

<a id="404issue"></a>
#### <a name="mvc-and-web-api-scaffolding---http-404-not-found-error"></a><span data-ttu-id="c261e-175">MVC 和 Web API 基架-HTTP 404 找不到错误</span><span class="sxs-lookup"><span data-stu-id="c261e-175">MVC and Web API Scaffolding - HTTP 404, Not Found error</span></span>

<span data-ttu-id="c261e-176">如果将基架的项添加到项目时遇到错误，，则可能你的项目将会处于不一致的状态。</span><span class="sxs-lookup"><span data-stu-id="c261e-176">If you encounter an error when adding a scaffolded item to a project, it is possible your project will be left in an inconsistent state.</span></span> <span data-ttu-id="c261e-177">一些将基架所做的更改将被回滚，但其他更改，例如已安装的 NuGet 包，将不会回滚。</span><span class="sxs-lookup"><span data-stu-id="c261e-177">Some of the changes made be scaffolding will be rolled back but other changes, such as the installed NuGet packages, will not be rolled back.</span></span> <span data-ttu-id="c261e-178">如果回滚路由的配置更改，用户将收到 HTTP 404 错误时导航到已搭建基架的项。</span><span class="sxs-lookup"><span data-stu-id="c261e-178">If the routing configuration changes are rolled back, users will receive an HTTP 404 error when navigating to scaffolded items.</span></span>

<span data-ttu-id="c261e-179">若要对 MVC 修复此错误，请添加一个新的基架的项，然后选择 MVC 5 依赖项 （最小或完整）。</span><span class="sxs-lookup"><span data-stu-id="c261e-179">To fix this error for MVC, add a new scaffolded item and select MVC 5 Dependencies (either Minimal or Full).</span></span> <span data-ttu-id="c261e-180">此过程将向你的项目添加所有所需的更改。</span><span class="sxs-lookup"><span data-stu-id="c261e-180">This process will add all of the required changes to your project.</span></span>

<span data-ttu-id="c261e-181">若要对 Web API 来修复此错误：</span><span class="sxs-lookup"><span data-stu-id="c261e-181">To fix this error for Web API:</span></span>

1. <span data-ttu-id="c261e-182">将以下 WebApiConfig 类添加到你的项目。</span><span class="sxs-lookup"><span data-stu-id="c261e-182">Add the following WebApiConfig class to your project.</span></span>

    [!code-csharp[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample1.cs)]

    [!code-vb[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample2.vb)]
2. <span data-ttu-id="c261e-183">应用程序中配置 WebApiConfig.Register\_Global.asax 中的 Start 方法，如下所示：</span><span class="sxs-lookup"><span data-stu-id="c261e-183">Configure WebApiConfig.Register in the Application\_Start method in Global.asax as follows:</span></span>

    [!code-csharp[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample3.cs)]

    [!code-vb[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample4.vb)]

<a id="expressissue"></a>
#### <a name="visual-studio-express-2012-for-web-stops-working-after-adding-a-scaffolded-item"></a><span data-ttu-id="c261e-184">Visual Studio Express 2012 for Web 添加基架的项后停止工作</span><span class="sxs-lookup"><span data-stu-id="c261e-184">Visual Studio Express 2012 for Web stops working after adding a scaffolded item</span></span>

<span data-ttu-id="c261e-185">如果 Visual Studio Express 2012 for Web 添加与实体框架 （例如 Web API 2 控制器的操作，使用实体框架） 的基架的项后停止工作，就可以，Visual Studio 速成版无法加载程序集的本机映像依赖于 System.Web.Extensions。</span><span class="sxs-lookup"><span data-stu-id="c261e-185">If Visual Studio Express 2012 for Web stops working after adding scaffolded item with Entity Framework (such as Web API 2 Controller with actions, using Entity Framework), it is possible that Visual Studio Express failed to load the native image of an assembly dependent on System.Web.Extensions.</span></span>

<span data-ttu-id="c261e-186">若要更正此问题，请配置 Visual Studio Express 使用 System.Web.Extensions MSIL 映像：</span><span class="sxs-lookup"><span data-stu-id="c261e-186">To correct this problem, configure Visual Studio Express to work with the MSIL image of System.Web.Extensions:</span></span>

1. <span data-ttu-id="c261e-187">在管理员模式下打开命令提示符。</span><span class="sxs-lookup"><span data-stu-id="c261e-187">Open Command Prompt in the Administrator mode.</span></span>
2. <span data-ttu-id="c261e-188">转到 %ProgramFiles%\Microsoft Visual Studio 11.0\Common7\IDE 或 %programfiles(x86) %\Microsoft Visual Studio 11.0\Common7\IDE （适用于 64 位 Windows）。</span><span class="sxs-lookup"><span data-stu-id="c261e-188">Go to %ProgramFiles%\Microsoft Visual Studio 11.0\Common7\IDE or %ProgramFiles(x86)%\Microsoft Visual Studio 11.0\Common7\IDE (for 64 bit Windows).</span></span>
3. <span data-ttu-id="c261e-189">在文本编辑器中打开 VWDExpress.exe.config。</span><span class="sxs-lookup"><span data-stu-id="c261e-189">Open VWDExpress.exe.config in a text editor.</span></span>
4. <span data-ttu-id="c261e-190">添加以下行下的&lt;配置&gt;/&lt;运行时&gt;元素：</span><span class="sxs-lookup"><span data-stu-id="c261e-190">Add the following line under the &lt;configuration&gt;/&lt;runtime&gt; element:</span></span>  

    [!code-xml[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample5.xml)]
5. <span data-ttu-id="c261e-191">重新启动 Visual Studio Express 2012 for Web。</span><span class="sxs-lookup"><span data-stu-id="c261e-191">Restart Visual Studio Express 2012 for Web.</span></span>

<a id="issuerazor"></a>
### <a name="aspnet-razor-3"></a><span data-ttu-id="c261e-192">ASP.NET Razor 3</span><span class="sxs-lookup"><span data-stu-id="c261e-192">ASP.NET Razor 3</span></span>

<a id="browseissue"></a>
#### <a name="viewing-cshtml-file-with-browse-with-or-f5-causes-a-server-error"></a><span data-ttu-id="c261e-193">查看使用浏览方式或 F5 的 cshtml 文件会导致服务器错误</span><span class="sxs-lookup"><span data-stu-id="c261e-193">Viewing cshtml file with Browse With or F5 causes a server error</span></span>

<span data-ttu-id="c261e-194">当您在 Visual Studio 2012 （或在 Visual Studio 2013 中创建的 Visual Studio 2012 MVC 5 项目中打开） 中创建的 MVC 5 项目，并尝试通过浏览方式或 F5 查看 cshtml 文件时，将收到一个错误，指明-**中的服务器错误'/' 应用程序**。</span><span class="sxs-lookup"><span data-stu-id="c261e-194">When you create an MVC 5 project in Visual Studio 2012 (or open in Visual Studio 2012 an MVC 5 project that was created in Visual Studio 2013) and attempt to view a cshtml file by using Browse With or F5, you will receive an error that states - **Server Error in '/' Application**.</span></span> <span data-ttu-id="c261e-195">服务器将尝试导航到 `http://localhost:XXXX/Views/../XXXX.cshtml`</span><span class="sxs-lookup"><span data-stu-id="c261e-195">The server attempts to navigate to `http://localhost:XXXX/Views/../XXXX.cshtml`</span></span>

<span data-ttu-id="c261e-196">若要解决此问题，请更改**启动操作**在您的项目中设置**特定页**。</span><span class="sxs-lookup"><span data-stu-id="c261e-196">To resolve this issue, change the **Start Action** setting in your project to **Specific Page**.</span></span> <span data-ttu-id="c261e-197">不需要为页面提供一个值。</span><span class="sxs-lookup"><span data-stu-id="c261e-197">You do not need to provide a value for the page.</span></span>

![](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image1.png)

<span data-ttu-id="c261e-198">此更改后，选择 f5 键导航到你的应用程序的根目录 (`http://localhost:XXXX`)。</span><span class="sxs-lookup"><span data-stu-id="c261e-198">After making this change, selecting F5 navigates to the root of your application (`http://localhost:XXXX`).</span></span> <span data-ttu-id="c261e-199">此行为不是相同的行为对于 MVC 5 项目在 Visual Studio 2013 中，其中**当前页**设置启动打开页。</span><span class="sxs-lookup"><span data-stu-id="c261e-199">This behavior is not the same as the behavior for MVC 5 projects in Visual Studio 2013, where the **Current Page** setting launches the open page.</span></span>

<a id="rewriteissue"></a>
#### <a name="url-rewrite-and-tilde"></a><span data-ttu-id="c261e-200">Url 重写和 Tilde(~)</span><span class="sxs-lookup"><span data-stu-id="c261e-200">Url Rewrite and Tilde(~)</span></span>

<span data-ttu-id="c261e-201">升级到 ASP.NET Razor 3 或 ASP.NET MVC 5 后，tilde(~) 表示法可能无法再正常工作如果您使用的 URL 重写。</span><span class="sxs-lookup"><span data-stu-id="c261e-201">After upgrading to ASP.NET Razor 3 or ASP.NET MVC 5, the tilde(~) notation may no longer work correctly if you are using URL rewrites.</span></span> <span data-ttu-id="c261e-202">URL 重写会影响 tilde(~) 表示法中的 HTML 元素，如&lt;A /&gt;，&lt;脚本 /&gt;，&lt;链接 /&gt;，并因此颚化符不再将映射到的根目录。</span><span class="sxs-lookup"><span data-stu-id="c261e-202">The URL rewrite affects the tilde(~) notation in HTML elements such as &lt;A/&gt;, &lt;SCRIPT/&gt;, &lt;LINK/&gt;, and as a result the tilde no longer maps to the root directory.</span></span>

<span data-ttu-id="c261e-203">例如，如果您重写的请求**asp.net/content**到**asp.net**中的 href 属性&lt;href ="~/content/"/&gt;解析为 **/content/内容 /** 而不是 **/** 。</span><span class="sxs-lookup"><span data-stu-id="c261e-203">For example, if you rewrite requests for **asp.net/content** to **asp.net**, the href attribute in &lt;A href="~/content/"/&gt; resolves to **/content/content/** instead of **/**.</span></span> <span data-ttu-id="c261e-204">若要禁止显示此更改，可以设置 **IIS\_WasUrlRewritten** 为 false，在每个网页中或在上下文 **应用程序\_BeginRequest** Global.asax 中。</span><span class="sxs-lookup"><span data-stu-id="c261e-204">To suppress this change, you can set the **IIS\_WasUrlRewritten** context to false in each Web Page or in **Application\_BeginRequest** in Global.asax.</span></span>

<a id="templateissue"></a>
### <a name="templates"></a><span data-ttu-id="c261e-205">模板</span><span class="sxs-lookup"><span data-stu-id="c261e-205">Templates</span></span>

<span data-ttu-id="c261e-206">当您创建 ASP.NET MVC 项目使用 Visual Studio 2012 Windows 8.1 或 Windows Server 2012 R2，Visual Studio 上显示错误消息，指出"配置 Web [url] 用于 ASP.NET 4.5 失败。"</span><span class="sxs-lookup"><span data-stu-id="c261e-206">When you create ASP.NET MVC projects with Visual Studio 2012 on Windows 8.1 or Windows Server 2012 R2, Visual Studio displays an error message that states "Configuring Web [url] for ASP.NET 4.5 failed."</span></span>

![配置错误](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image2.png)

<span data-ttu-id="c261e-208">因为 Visual Studio 2012 不会启用 ASP.NET 4.5 功能，这些版本的 Windows 上安装时看到此错误。</span><span class="sxs-lookup"><span data-stu-id="c261e-208">You see this error because Visual Studio 2012 does not enable the ASP.NET 4.5 feature when it is installed on those releases of Windows.</span></span> <span data-ttu-id="c261e-209">若要启用 ASP.NET 4.5，请执行中所述的步骤[打开或关闭打开的 Windows 功能](https://windows.microsoft.com/windows-8/turn-windows-features-on-off)。</span><span class="sxs-lookup"><span data-stu-id="c261e-209">To enable ASP.NET 4.5, perform the steps described in [Turn Windows features on or off](https://windows.microsoft.com/windows-8/turn-windows-features-on-off).</span></span>

![打开或关闭 Windows 功能](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image3.png)

<span data-ttu-id="c261e-211">或者，您可以通过命令行启用 ASP.NET 4.5。</span><span class="sxs-lookup"><span data-stu-id="c261e-211">Alternatively, you can enable ASP.NET 4.5 through the command line.</span></span>

1. <span data-ttu-id="c261e-212">在管理员模式下打开命令提示符。</span><span class="sxs-lookup"><span data-stu-id="c261e-212">Open Command Prompt in the Administrator mode.</span></span>
2. <span data-ttu-id="c261e-213">运行以下命令以启用 ASP.NET 4.5。</span><span class="sxs-lookup"><span data-stu-id="c261e-213">Run the following command to enable ASP.NET 4.5.</span></span>  
    `dism /Online /Enable-Feature /FeatureName:NetFx4Extended-ASPNET45 /Quiet /NoRestart`

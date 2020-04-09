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
# <a name="creating-aspnet-web-projects-in-visual-studio-2013"></a><span data-ttu-id="e8298-103">在 Visual Studio 2013 中创建 ASP.NET Web 项目</span><span class="sxs-lookup"><span data-stu-id="e8298-103">Creating ASP.NET Web Projects in Visual Studio 2013</span></span>

<span data-ttu-id="e8298-104">汤姆[·戴克斯特拉](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="e8298-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

> <span data-ttu-id="e8298-105">本主题介绍使用 Update 3 在 Visual Studio 2013 中创建ASP.NET Web 项目的选项</span><span class="sxs-lookup"><span data-stu-id="e8298-105">This topic explains the options for creating ASP.NET web projects in Visual Studio 2013 with Update 3</span></span>
> 
> <span data-ttu-id="e8298-106">与早期版本的 Visual Studio 相比，以下是 Web 开发中的一些新功能：</span><span class="sxs-lookup"><span data-stu-id="e8298-106">Here are some of the new features for web development compared to earlier versions of Visual Studio:</span></span>
> 
> - <span data-ttu-id="e8298-107">用于创建支持[多个ASP.NET框架](#add)（Web 窗体、MVC 和 Web API）的项目的简单 UI。</span><span class="sxs-lookup"><span data-stu-id="e8298-107">A simple UI for creating projects that offer [support for multiple ASP.NET frameworks](#add) (Web Forms, MVC, and Web API).</span></span>
> - <span data-ttu-id="e8298-108">[ASP.NET标识](#indauth)，一个新的ASP.NET成员系统，在所有ASP.NET框架中都工作相同，并且与IIS以外的Web托管软件配合使用。</span><span class="sxs-lookup"><span data-stu-id="e8298-108">[ASP.NET Identity](#indauth), a new ASP.NET membership system that works the same in all ASP.NET frameworks and works with web hosting software other than IIS.</span></span>
> - <span data-ttu-id="e8298-109">使用[Bootstrap](#bootstrap)提供响应式设计和准备功能。</span><span class="sxs-lookup"><span data-stu-id="e8298-109">The use of [Bootstrap](#bootstrap) to provide responsive design and theming capabilities.</span></span>
> - <span data-ttu-id="e8298-110">以前只为 MVC 提供的 Web 窗体的新功能，例如[自动测试项目创建](#testproj)和 Intranet[网站模板](#winauth)。</span><span class="sxs-lookup"><span data-stu-id="e8298-110">New features for Web Forms that used to be offered only for MVC, such as [automatic test project creation](#testproj) and an [Intranet site template](#winauth).</span></span>
> 
> <span data-ttu-id="e8298-111">有关如何为 Azure 云服务或 Azure 移动服务创建 Web 项目的信息，请参阅[使用 Azure 云服务开始使用"ASP.NET"](https://azure.microsoft.com/documentation/articles/cloud-services-dotnet-get-started/)以及[使用 Azure 移动服务 .NET 后端创建排行榜应用](https://azure.microsoft.com/documentation/articles/mobile-services-dotnet-backend-windows-store-dotnet-leaderboard/)。</span><span class="sxs-lookup"><span data-stu-id="e8298-111">For information about how to create web projects for Azure Cloud Services or Azure Mobile Services, see [Get Started with Azure Cloud Services and ASP.NET](https://azure.microsoft.com/documentation/articles/cloud-services-dotnet-get-started/) and [Creating a Leaderboard App with Azure Mobile Services .NET Backend](https://azure.microsoft.com/documentation/articles/mobile-services-dotnet-backend-windows-store-dotnet-leaderboard/).</span></span>

<a id="prerequisites"></a>
## <a name="prerequisites"></a><span data-ttu-id="e8298-112">先决条件</span><span class="sxs-lookup"><span data-stu-id="e8298-112">Prerequisites</span></span>

<span data-ttu-id="e8298-113">本文适用于安装了[更新 3](https://go.microsoft.com/fwlink/?linkid=397827&amp;clcid=0x409)的 Visual [Studio 2013。](https://go.microsoft.com/fwlink/?LinkId=306566)</span><span class="sxs-lookup"><span data-stu-id="e8298-113">This article applies to [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566) with [Update 3](https://go.microsoft.com/fwlink/?linkid=397827&amp;clcid=0x409) installed.</span></span>

<a id="wap"></a>
## <a name="web-application-projects-versus-web-site-projects"></a><span data-ttu-id="e8298-114">Web 应用程序项目与网站项目</span><span class="sxs-lookup"><span data-stu-id="e8298-114">Web application projects versus web site projects</span></span>

<span data-ttu-id="e8298-115">ASP.NET在两种Web项目之间做出选择 *：Web应用程序*项目和*网站项目*。</span><span class="sxs-lookup"><span data-stu-id="e8298-115">ASP.NET gives you a choice between two kinds of web projects: *web application projects* and *web site projects*.</span></span> <span data-ttu-id="e8298-116">我们建议 Web 应用程序项目用于新开发，本文仅适用于 Web 应用程序项目。</span><span class="sxs-lookup"><span data-stu-id="e8298-116">We recommend web application projects for new development, and this article applies only to web application projects.</span></span> <span data-ttu-id="e8298-117">有关详细信息，请参阅 MSDN 网站上的[Visual Studio 中的 Web 应用程序项目与网站项目](https://msdn.microsoft.com/library/dd547590(v=vs.120).aspx)。</span><span class="sxs-lookup"><span data-stu-id="e8298-117">For more information, see [Web Application Projects versus Web Site Projects in Visual Studio](https://msdn.microsoft.com/library/dd547590(v=vs.120).aspx) on the MSDN site.</span></span>

<a id="overview"></a>
## <a name="overview-of-web-application-project-creation"></a><span data-ttu-id="e8298-118">Web 应用程序项目创建概述</span><span class="sxs-lookup"><span data-stu-id="e8298-118">Overview of web application project creation</span></span>

<span data-ttu-id="e8298-119">以下步骤演示如何创建 Web 项目：</span><span class="sxs-lookup"><span data-stu-id="e8298-119">The following steps show how to create a web project:</span></span>

1. <span data-ttu-id="e8298-120">单击 **"开始"** 页或 **"文件**"菜单中的 **"新项目**"。</span><span class="sxs-lookup"><span data-stu-id="e8298-120">Click **New Project** in the **Start** page or in the **File** menu.</span></span>
2. <span data-ttu-id="e8298-121">在 **"新项目"** 对话框中，单击左侧窗格中的**Web，** 并在中间窗格**中单击 ASP.NET Web 应用程序**。</span><span class="sxs-lookup"><span data-stu-id="e8298-121">In the **New Project** dialog, click **Web** in the left pane and **ASP.NET Web Application** in the middle pane.</span></span>

    ![“新建项目”对话框](creating-web-projects-in-visual-studio/_static/image1.png)

    <span data-ttu-id="e8298-123">可以选择左侧窗格中的 **"云**"来创建[Azure 云服务](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy)[、Azure 移动服务](https://msdn.microsoft.com/library/windows/apps/dn629482.aspx)或[Azure WebJob](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-webjobs)。</span><span class="sxs-lookup"><span data-stu-id="e8298-123">You can choose **Cloud** in the left pane to create an [Azure Cloud Service](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy), [Azure Mobile Service](https://msdn.microsoft.com/library/windows/apps/dn629482.aspx), or [Azure WebJob](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-webjobs).</span></span> <span data-ttu-id="e8298-124">本主题不包括这些模板。</span><span class="sxs-lookup"><span data-stu-id="e8298-124">This topic doesn't cover those templates.</span></span>
3. <span data-ttu-id="e8298-125">在右侧窗格中，如果希望对应用程序进行运行状况和使用情况监视，请单击"**将应用程序见解添加到项目**"复选框。</span><span class="sxs-lookup"><span data-stu-id="e8298-125">In the right pane, click the **Add Application Insights to Project** check box if you want health and usage monitoring for your application.</span></span> <span data-ttu-id="e8298-126">有关详细信息，请参阅[在 Web 应用程序中监视性能](https://azure.microsoft.com/documentation/articles/app-insights-web-monitor-performance/)。</span><span class="sxs-lookup"><span data-stu-id="e8298-126">For more information, see [Monitor performance in web applications](https://azure.microsoft.com/documentation/articles/app-insights-web-monitor-performance/).</span></span>
4. <span data-ttu-id="e8298-127">指定项目**名称**、**位置**和其他选项，然后单击 **"确定**"。</span><span class="sxs-lookup"><span data-stu-id="e8298-127">Specify project **Name**, **Location**, and other options, and then click **OK**.</span></span>

    <span data-ttu-id="e8298-128">此时将出现 **“新建 ASP.NET 项目”** 对话框。</span><span class="sxs-lookup"><span data-stu-id="e8298-128">The **New ASP.NET Project** dialog appears.</span></span>

    ![“新建项目”对话框](creating-web-projects-in-visual-studio/_static/image2.png)
5. <span data-ttu-id="e8298-130">单击模板。</span><span class="sxs-lookup"><span data-stu-id="e8298-130">Click a template.</span></span>

    ![选择模板](creating-web-projects-in-visual-studio/_static/image3.png)
6. <span data-ttu-id="e8298-132">如果要添加对模板中未包括的其他框架的支持，请单击相应的复选框。</span><span class="sxs-lookup"><span data-stu-id="e8298-132">If you want to add support for additional frameworks not included in the template, click the appropriate check box.</span></span> <span data-ttu-id="e8298-133">（在所示示例中，您可以将 MVC 和/或 Web API 添加到 Web 窗体项目中。</span><span class="sxs-lookup"><span data-stu-id="e8298-133">(In the example shown, you could add MVC and/or Web API to a Web Forms project.)</span></span>

    ![添加框架](creating-web-projects-in-visual-studio/_static/image4.png)
7. <a id="testproj"></a><span data-ttu-id="e8298-135">如果要添加单元测试项目，请单击"**添加单元测试**"。</span><span class="sxs-lookup"><span data-stu-id="e8298-135">If you want to add a unit test project, click **Add unit tests**.</span></span>

    ![添加单元测试](creating-web-projects-in-visual-studio/_static/image5.png)
8. <span data-ttu-id="e8298-137">如果想要与模板默认提供的身份验证方法不同的身份验证方法，请单击"**更改身份验证**"。</span><span class="sxs-lookup"><span data-stu-id="e8298-137">If you want a different authentication method than what the template provides by default, click **Change Authentication**.</span></span>

    ![配置身份验证按钮](creating-web-projects-in-visual-studio/_static/image6.png)

    ![配置身份验证对话框](creating-web-projects-in-visual-studio/_static/image7.png)

<a id="azurenewproj"></a>
### <a name="create-a-web-app-or-virtual-machine-in-azure"></a><span data-ttu-id="e8298-140">在 Azure 中创建 Web 应用或虚拟机</span><span class="sxs-lookup"><span data-stu-id="e8298-140">Create a web app or virtual machine in Azure</span></span>

<span data-ttu-id="e8298-141">Visual Studio 包含的功能，使使用 Azure 服务轻松托管 Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="e8298-141">Visual Studio includes features that make it easy to work with Azure services for hosting web applications.</span></span> <span data-ttu-id="e8298-142">例如，您可以在 Visual Studio IDE 中执行以下所有操作：</span><span class="sxs-lookup"><span data-stu-id="e8298-142">For example, you can do all of the following right from the Visual Studio IDE:</span></span>

- <span data-ttu-id="e8298-143">创建和管理 Web 应用或虚拟机，使应用程序在 Internet 上可用。</span><span class="sxs-lookup"><span data-stu-id="e8298-143">Create and manage web apps or virtual machines that make your application available over the Internet.</span></span>
- <span data-ttu-id="e8298-144">查看应用程序在云中运行时创建的日志。</span><span class="sxs-lookup"><span data-stu-id="e8298-144">View logs created by the application as it runs in the cloud.</span></span>
- <span data-ttu-id="e8298-145">应用程序在云中运行时，在调试模式下远程运行。</span><span class="sxs-lookup"><span data-stu-id="e8298-145">Run in debug mode remotely while the application runs in the cloud.</span></span>
- <span data-ttu-id="e8298-146">查看和管理其他 Azure 服务，如 SQL 数据库。</span><span class="sxs-lookup"><span data-stu-id="e8298-146">View and manage other Azure services such as SQL databases.</span></span>

<span data-ttu-id="e8298-147">您可以创建包含基本服务（如免费 Web 应用）的[Azure 帐户](https://www.windowsazure.com/pricing/free-trial/)，如果您是 MSDN 订阅者，则可以[激活每月](https://azure.microsoft.com/pricing/member-offers/visual-studio-subscriptions/)为其他 Azure 服务提供积分的好处。</span><span class="sxs-lookup"><span data-stu-id="e8298-147">You can [create an Azure account](https://www.windowsazure.com/pricing/free-trial/) that includes basic services such as web apps for free, and if you are an MSDN subscriber you can [activate benefits](https://azure.microsoft.com/pricing/member-offers/visual-studio-subscriptions/) that give you monthly credits toward additional Azure services.</span></span> 

<span data-ttu-id="e8298-148">默认情况下，"**新建ASP.NET项目"** 对话框使您能够为新 Web 项目创建 Web 应用或虚拟机。</span><span class="sxs-lookup"><span data-stu-id="e8298-148">By default the **New ASP.NET Project** dialog box enables you to create a web app or virtual machine for a new web project.</span></span> <span data-ttu-id="e8298-149">如果不想创建新的 Web 应用或虚拟机，请清除**云中的"主机**"复选框。</span><span class="sxs-lookup"><span data-stu-id="e8298-149">If you don't want to create a new web app or virtual machine, clear the **Host in the cloud** check box.</span></span>

![创建远程资源](creating-web-projects-in-visual-studio/_static/image8.png)

<span data-ttu-id="e8298-151">复选框标题可能是**云中的主机**或**创建远程资源**，在这两种情况下效果都相同。</span><span class="sxs-lookup"><span data-stu-id="e8298-151">The check box caption might be **Host in the cloud** or **Create remote resources**, and in either case the effect is the same.</span></span> <span data-ttu-id="e8298-152">如果选中选中该复选框，Visual Studio 默认情况下会在 Azure 应用服务中创建 Web 应用。</span><span class="sxs-lookup"><span data-stu-id="e8298-152">If you leave the check box selected, Visual Studio creates a web app in Azure App Service by default.</span></span> <span data-ttu-id="e8298-153">如果您愿意，可以使用下拉框将该框更改为**虚拟机**。</span><span class="sxs-lookup"><span data-stu-id="e8298-153">You can use the drop-down box to change that to a **Virtual Machine** if you prefer.</span></span> <span data-ttu-id="e8298-154">如果您尚未登录到 Azure，系统将提示您输入 Azure 凭据。</span><span class="sxs-lookup"><span data-stu-id="e8298-154">If you're not already signed in to Azure, you're prompted for Azure credentials.</span></span> <span data-ttu-id="e8298-155">登录后，一个对话框允许您配置 Visual Studio 将为项目创建的资源。</span><span class="sxs-lookup"><span data-stu-id="e8298-155">After you sign in, a dialog box enables you to configure the resources that Visual Studio will create for your project.</span></span> <span data-ttu-id="e8298-156">下图显示了 Web 应用的对话框;如果选择创建虚拟机，则会出现不同的选项。</span><span class="sxs-lookup"><span data-stu-id="e8298-156">The following illustration shows the dialog for a web app; different options appear if you choose to create a virtual machine.</span></span>

![配置 Azure 应用设置](creating-web-projects-in-visual-studio/_static/image9.png)

<span data-ttu-id="e8298-158">有关如何使用此过程创建 Azure 资源的详细信息，请参阅使用 Azure[启动和ASP.NET](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet)以及[使用 Visual Studio 为网站创建虚拟机](https://azure.microsoft.com/documentation/articles/virtual-machines-dotnet-create-visual-studio-powershell/)。</span><span class="sxs-lookup"><span data-stu-id="e8298-158">For more information about how to use this process for creating Azure resources, see [Get Started with Azure and ASP.NET](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet) and [Creating a virtual machine for a web site with Visual Studio](https://azure.microsoft.com/documentation/articles/virtual-machines-dotnet-create-visual-studio-powershell/).</span></span>

<span data-ttu-id="e8298-159">本文的其余部分提供了有关可用模板及其选项的详细信息。</span><span class="sxs-lookup"><span data-stu-id="e8298-159">The remainder of this article provides more information about the available templates and their options.</span></span> <span data-ttu-id="e8298-160">本文还介绍了模板中使用的 Bootstrap、布局和准备框架。</span><span class="sxs-lookup"><span data-stu-id="e8298-160">The article also introduces Bootstrap, the layout and theming framework used in the templates.</span></span>

<a id="vs2013"></a>
## <a name="visual-studio-2013-web-project-templates"></a><span data-ttu-id="e8298-161">可视化工作室 2013 Web 项目模板</span><span class="sxs-lookup"><span data-stu-id="e8298-161">Visual Studio 2013 Web Project Templates</span></span>

<span data-ttu-id="e8298-162">Visual Studio 使用模板创建 Web 项目。</span><span class="sxs-lookup"><span data-stu-id="e8298-162">Visual Studio uses templates to create web projects.</span></span> <span data-ttu-id="e8298-163">项目模板可以在新项目中创建文件和文件夹，安装 NuGet 包，并为基本工作应用程序提供示例代码。</span><span class="sxs-lookup"><span data-stu-id="e8298-163">A project template can create files and folders in the new project, install NuGet packages, and provide sample code for a rudimentary working application.</span></span> <span data-ttu-id="e8298-164">模板实现最新的 Web 标准，旨在演示如何使用ASP.NET技术的最佳做法，并让您开始创建自己的应用程序。</span><span class="sxs-lookup"><span data-stu-id="e8298-164">Templates implement the latest web standards and are intended to demonstrate best practices for how to use ASP.NET technologies as well as give you a jump start on creating your own application.</span></span>

<span data-ttu-id="e8298-165">Visual Studio 2013 为针对 .NET 4.5 或更高版本的 .NET 框架的项目提供了以下 Web 项目模板选项：</span><span class="sxs-lookup"><span data-stu-id="e8298-165">Visual Studio 2013 provides the following choices for web project templates for projects that target .NET 4.5 or later versions of the .NET framework:</span></span>

- [<span data-ttu-id="e8298-166">空模板</span><span class="sxs-lookup"><span data-stu-id="e8298-166">Empty template</span></span>](#empty)
- [<span data-ttu-id="e8298-167">Web 表单模板</span><span class="sxs-lookup"><span data-stu-id="e8298-167">Web Forms template</span></span>](#wf)
- [<span data-ttu-id="e8298-168">MVC 模板</span><span class="sxs-lookup"><span data-stu-id="e8298-168">MVC template</span></span>](#mvc)
- [<span data-ttu-id="e8298-169">Web API 模板</span><span class="sxs-lookup"><span data-stu-id="e8298-169">Web API template</span></span>](#webapi)
- [<span data-ttu-id="e8298-170">单页应用程序模板</span><span class="sxs-lookup"><span data-stu-id="e8298-170">Single Page Application template</span></span>](#spa)
- [<span data-ttu-id="e8298-171">Azure 移动服务模板</span><span class="sxs-lookup"><span data-stu-id="e8298-171">Azure Mobile Service template</span></span>](https://azure.microsoft.com/documentation/articles/mobile-services-dotnet-backend-windows-store-dotnet-leaderboard/)
- [<span data-ttu-id="e8298-172">视觉工作室 2012 模板</span><span class="sxs-lookup"><span data-stu-id="e8298-172">Visual Studio 2012 Templates</span></span>](#vs2012)

<span data-ttu-id="e8298-173">您还可以安装提供[Facebook 模板](#facebook)的视觉工作室扩展。</span><span class="sxs-lookup"><span data-stu-id="e8298-173">You can also install a Visual Studio extension that provides a [Facebook template](#facebook).</span></span>

<span data-ttu-id="e8298-174">有关如何创建面向 .NET 4 的项目的信息，请参阅本主题后面的[Visual Studio 2012 模板](#vs2012)。</span><span class="sxs-lookup"><span data-stu-id="e8298-174">For information about how to create projects that target .NET 4, see [Visual Studio 2012 Templates](#vs2012) later in this topic.</span></span>

<span data-ttu-id="e8298-175">有关如何为移动客户端创建ASP.NET应用程序的信息，请参阅 ASP.NET[中的移动支持](../../../mobile/overview.md)。</span><span class="sxs-lookup"><span data-stu-id="e8298-175">For information about how to create ASP.NET applications for mobile clients, see [Mobile Support in ASP.NET](../../../mobile/overview.md).</span></span>

<a id="empty"></a>
### <a name="empty-template"></a><span data-ttu-id="e8298-176">空模板</span><span class="sxs-lookup"><span data-stu-id="e8298-176">Empty Template</span></span>

<span data-ttu-id="e8298-177">"空"模板为ASP.NET Web 应用（如项目文件 *（.csproj*或 ）提供最少的文件夹和文件。*vbproj*） 和*Web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="e8298-177">The Empty template provides the bare minimum folders and files for an ASP.NET web app, such as a project file (*.csproj* or .*vbproj*) and a *Web.config* file.</span></span> <span data-ttu-id="e8298-178">您可以使用"**添加文件夹"下的复选框和核心引用**：标签，添加对 Web 窗体、MVC 和/或 Web API 的支持。</span><span class="sxs-lookup"><span data-stu-id="e8298-178">You can add support for Web Forms, MVC, and/or Web API by using the check boxes under the **Add folders and core references for:** label.</span></span>

<span data-ttu-id="e8298-179">对于空模板，没有可用的身份验证选项。</span><span class="sxs-lookup"><span data-stu-id="e8298-179">For the Empty template no authentication options are available.</span></span> <span data-ttu-id="e8298-180">身份验证功能在示例应用程序中实现，空模板不创建示例应用程序。</span><span class="sxs-lookup"><span data-stu-id="e8298-180">Authentication functionality is implemented in sample applications, and the Empty template does not create a sample application.</span></span>

<a id="wf"></a>
### <a name="web-forms-template"></a><span data-ttu-id="e8298-181">Web 表单模板</span><span class="sxs-lookup"><span data-stu-id="e8298-181">Web Forms Template</span></span>

<span data-ttu-id="e8298-182">Web 窗体框架提供了以下功能，使您能够快速生成具有丰富 UI 和数据访问功能的网站：</span><span class="sxs-lookup"><span data-stu-id="e8298-182">The Web Forms framework provides the following features that let you rapidly build web sites that are rich in UI and data access features:</span></span>

- <span data-ttu-id="e8298-183">视觉工作室的 WYSIWYG 设计师。</span><span class="sxs-lookup"><span data-stu-id="e8298-183">A WYSIWYG designer in Visual Studio.</span></span>
- <span data-ttu-id="e8298-184">呈现 HTML 的服务器控件，以及可以通过设置属性和样式进行自定义的服务器控件。</span><span class="sxs-lookup"><span data-stu-id="e8298-184">Server controls that render HTML and that you can customize by setting properties and styles.</span></span>
- <span data-ttu-id="e8298-185">用于数据访问和数据显示的丰富类型控件。</span><span class="sxs-lookup"><span data-stu-id="e8298-185">A rich assortment of controls for data access and data display.</span></span>
- <span data-ttu-id="e8298-186">公开事件的事件模型，您可以像对客户端应用程序（如 WPF）进行编程一样进行编程。</span><span class="sxs-lookup"><span data-stu-id="e8298-186">An event model that exposes events which you can program like you would program a client application such as WPF.</span></span>
- <span data-ttu-id="e8298-187">自动在 HTTP 请求之间保留状态（数据）。</span><span class="sxs-lookup"><span data-stu-id="e8298-187">Automatic preservation of state (data) between HTTP requests.</span></span>

<span data-ttu-id="e8298-188">通常，与使用ASP.NET MVC 框架创建同一应用程序相比，创建 Web 窗体应用程序所需的编程工作量更少。</span><span class="sxs-lookup"><span data-stu-id="e8298-188">In general, creating a Web Forms application requires less programming effort than creating the same application by using the ASP.NET MVC framework.</span></span> <span data-ttu-id="e8298-189">但是，Web 窗体并不仅仅用于快速应用程序开发。</span><span class="sxs-lookup"><span data-stu-id="e8298-189">However, Web Forms is not just for rapid application development.</span></span> <span data-ttu-id="e8298-190">有许多复杂的商业应用程序和框架建立在 Web 窗体之上。</span><span class="sxs-lookup"><span data-stu-id="e8298-190">There are many complex commercial applications and frameworks built on top of Web Forms.</span></span>

<span data-ttu-id="e8298-191">由于 Web 窗体页和页面上的控件会自动生成发送到浏览器的大部分标记，因此您没有 ASP.NET MVC 提供的 HTML 的细粒度控制。</span><span class="sxs-lookup"><span data-stu-id="e8298-191">Because a Web Forms page and the controls on the page automatically generate much of the markup that's sent to the browser, you don't have the kind of fine-grained control over the HTML that ASP.NET MVC offers.</span></span> <span data-ttu-id="e8298-192">用于配置页面和控件的声明性模型最大限度地减少了必须编写的代码量，但隐藏了 HTML 和 HTTP 的某些行为。</span><span class="sxs-lookup"><span data-stu-id="e8298-192">The declarative model for configuring pages and controls minimizes the amount of code you have to write but hides some of the behavior of HTML and HTTP.</span></span> <span data-ttu-id="e8298-193">例如，并不总是能够准确指定控件可能生成哪些标记。</span><span class="sxs-lookup"><span data-stu-id="e8298-193">For example, it's not always possible to specify exactly what markup might be generated by a control.</span></span>

<span data-ttu-id="e8298-194">Web 窗体框架不像 MVC ASP.NET一样容易适应基于模式的开发实践，例如[测试驱动开发](http://en.wikipedia.org/wiki/Test-driven_development)、[关注分离](http://en.wikipedia.org/wiki/Separation_of_concerns)、[控制反转](http://en.wikipedia.org/wiki/Inversion_of_control)和[依赖注入](http://en.wikipedia.org/wiki/Dependency_injection)。</span><span class="sxs-lookup"><span data-stu-id="e8298-194">The Web Forms framework doesn't lend itself as readily as ASP.NET MVC to patterns-based development practices such as [test-driven development](http://en.wikipedia.org/wiki/Test-driven_development), [separation of concerns](http://en.wikipedia.org/wiki/Separation_of_concerns), [inversion of control](http://en.wikipedia.org/wiki/Inversion_of_control), and [dependency injection](http://en.wikipedia.org/wiki/Dependency_injection).</span></span> <span data-ttu-id="e8298-195">如果要用这种方式编写分解的代码，可以;它只是不像ASP.NETMVC框架那样自动。</span><span class="sxs-lookup"><span data-stu-id="e8298-195">If you want to write code factored that way, you can; it's just not as automatic as it is in the ASP.NET MVC framework.</span></span> <span data-ttu-id="e8298-196">[ASP.NET Web 窗体 MVP](http://webformsmvp.com/)项目展示了一种有助于区分关注点和可测试性的方法，同时保持 Web 窗体为交付而构建的快速开发。</span><span class="sxs-lookup"><span data-stu-id="e8298-196">The [ASP.NET Web Forms MVP](http://webformsmvp.com/) project shows an approach that facilitates separation of concerns and testability while maintaining the rapid development that Web Forms was built to deliver.</span></span> <span data-ttu-id="e8298-197">微软 SharePoint 建立在 Web 表单 MVP 之上。</span><span class="sxs-lookup"><span data-stu-id="e8298-197">Microsoft SharePoint is built on Web Forms MVP.</span></span>

<span data-ttu-id="e8298-198">Web 窗体模板创建一个示例 Web 窗体应用程序，该应用程序使用[Bootstrap](#bootstrap)提供响应式设计和主发功能。</span><span class="sxs-lookup"><span data-stu-id="e8298-198">The Web Forms template creates a sample Web Forms application that uses [Bootstrap](#bootstrap) to provide responsive design and theming features.</span></span> <span data-ttu-id="e8298-199">下图显示了主页。</span><span class="sxs-lookup"><span data-stu-id="e8298-199">The following illustration shows the home page.</span></span>

![Web 表单模板应用主页](creating-web-projects-in-visual-studio/_static/image10.png)

<span data-ttu-id="e8298-201">有关 Web 窗体的详细信息，请参阅[ASP.NET Web 窗体](https://asp.net/web-forms)。</span><span class="sxs-lookup"><span data-stu-id="e8298-201">For more information about Web Forms, see [ASP.NET Web Forms](https://asp.net/web-forms).</span></span> <span data-ttu-id="e8298-202">有关 Web 表单模板为您做什么的信息，请参阅使用[Visual Studio 2013 构建基本 Web 表单应用程序](https://blogs.msdn.com/b/webdev/archive/2013/12/19/building-a-basic-web-forms-application-using-visual-studio-2013.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e8298-202">For information about what the Web Forms template does for you, see [Building a basic Web Forms application using Visual Studio 2013](https://blogs.msdn.com/b/webdev/archive/2013/12/19/building-a-basic-web-forms-application-using-visual-studio-2013.aspx).</span></span>

<a id="mvc"></a>
### <a name="mvc-template"></a><span data-ttu-id="e8298-203">MVC 模板</span><span class="sxs-lookup"><span data-stu-id="e8298-203">MVC Template</span></span>

<span data-ttu-id="e8298-204">ASP.NET MVC 旨在促进基于模式的开发实践，例如[测试驱动开发](http://en.wikipedia.org/wiki/Test-driven_development)、[关注分离](http://en.wikipedia.org/wiki/Separation_of_concerns)、[控制反转](http://en.wikipedia.org/wiki/Inversion_of_control)和[依赖注入](http://en.wikipedia.org/wiki/Dependency_injection)。</span><span class="sxs-lookup"><span data-stu-id="e8298-204">ASP.NET MVC was designed to facilitate patterns-based development practices such as [test-driven development](http://en.wikipedia.org/wiki/Test-driven_development), [separation of concerns](http://en.wikipedia.org/wiki/Separation_of_concerns), [inversion of control](http://en.wikipedia.org/wiki/Inversion_of_control), and [dependency injection](http://en.wikipedia.org/wiki/Dependency_injection).</span></span> <span data-ttu-id="e8298-205">该框架鼓励将 Web 应用程序的业务逻辑层与其表示层分开。</span><span class="sxs-lookup"><span data-stu-id="e8298-205">The framework encourages separating the business logic layer of a web application from its presentation layer.</span></span> <span data-ttu-id="e8298-206">通过将应用程序划分为模型 （M）、视图 （V） 和控制器 （C），ASP.NET MVC 可以更轻松地管理较大应用程序中的复杂性。</span><span class="sxs-lookup"><span data-stu-id="e8298-206">By dividing the application into models (M), views (V), and controllers (C), ASP.NET MVC can make it easier to manage complexity in larger applications.</span></span>

<span data-ttu-id="e8298-207">使用ASP.NET MVC，您更直接地使用 HTML 和 HTTP 而不是 Web 窗体。</span><span class="sxs-lookup"><span data-stu-id="e8298-207">With ASP.NET MVC, you work more directly with HTML and HTTP than in Web Forms.</span></span> <span data-ttu-id="e8298-208">例如，Web 窗体可以在 HTTP 请求之间自动保留状态，但您必须在 MVC 中显式编写代码。</span><span class="sxs-lookup"><span data-stu-id="e8298-208">For example, Web Forms can automatically preserve state between HTTP requests, but you have to code that explicitly in MVC.</span></span> <span data-ttu-id="e8298-209">MVC 模型的优点是，它使您能够完全控制应用程序正在执行的操作以及它在 Web 环境中的表现。</span><span class="sxs-lookup"><span data-stu-id="e8298-209">The advantage of the MVC model is that it enables you to take complete control over exactly what your application is doing and how it behaves in the web environment.</span></span> <span data-ttu-id="e8298-210">缺点是您必须编写更多的代码。</span><span class="sxs-lookup"><span data-stu-id="e8298-210">The disadvantage is that you have to write more code.</span></span>

<span data-ttu-id="e8298-211">MVC 设计为可扩展，使电力开发人员能够根据他们的应用程序需求自定义框架。</span><span class="sxs-lookup"><span data-stu-id="e8298-211">MVC was designed to be extensible, providing power developers the ability to customize the framework for their application needs.</span></span> <span data-ttu-id="e8298-212">此外，ASP.NET MVC 源代码在 OSI 许可证下可用。</span><span class="sxs-lookup"><span data-stu-id="e8298-212">In addition, the ASP.NET MVC source code is available under an OSI license.</span></span>

<span data-ttu-id="e8298-213">MVC 模板创建一个示例 MVC 5 应用程序，该应用程序使用[Bootstrap](#bootstrap)提供响应式设计和主旋律功能。</span><span class="sxs-lookup"><span data-stu-id="e8298-213">The MVC template creates a sample MVC 5 application that uses [Bootstrap](#bootstrap) to provide responsive design and theming features.</span></span> <span data-ttu-id="e8298-214">下图显示了主页。</span><span class="sxs-lookup"><span data-stu-id="e8298-214">The following illustration shows the home page.</span></span>

![MVC 示例应用](creating-web-projects-in-visual-studio/_static/image11.png)

<span data-ttu-id="e8298-216">有关 MVC 的详细信息，请参阅[ASP.NET MVC](https://asp.net/mvc)。</span><span class="sxs-lookup"><span data-stu-id="e8298-216">For more information about MVC, see [ASP.NET MVC](https://asp.net/mvc).</span></span> <span data-ttu-id="e8298-217">有关如何选择 MVC 4 模板的信息，请参阅本文后面的[Visual Studio 2012 模板](#vs2012)。</span><span class="sxs-lookup"><span data-stu-id="e8298-217">For information about how to select the MVC 4 template, see [Visual Studio 2012 templates](#vs2012) later in this article.</span></span>

<a id="webapi"></a>
### <a name="web-api-template"></a><span data-ttu-id="e8298-218">Web API 模板</span><span class="sxs-lookup"><span data-stu-id="e8298-218">Web API Template</span></span>

<span data-ttu-id="e8298-219">Web API 模板基于 Web API 创建示例 Web 服务，包括基于 MVC 的 API 帮助页。</span><span class="sxs-lookup"><span data-stu-id="e8298-219">The Web API template creates a sample web service based on Web API, including API help pages based on MVC.</span></span>

<span data-ttu-id="e8298-220">ASP.NET Web API 是一种框架，用于轻松构建可以访问多种客户端（包括浏览器和移动设备）的 HTTP 服务。</span><span class="sxs-lookup"><span data-stu-id="e8298-220">ASP.NET Web API is a framework that makes it easy to build HTTP services that reach a broad range of clients, including browsers and mobile devices.</span></span> <span data-ttu-id="e8298-221">ASP.NET Web API 是在 .NET 框架上构建 RESTful 服务的理想平台。</span><span class="sxs-lookup"><span data-stu-id="e8298-221">ASP.NET Web API is an ideal platform for building RESTful services on the .NET Framework.</span></span>

<span data-ttu-id="e8298-222">Web API 模板创建示例 Web 服务。</span><span class="sxs-lookup"><span data-stu-id="e8298-222">The Web API template creates a sample web service.</span></span> <span data-ttu-id="e8298-223">下图显示了示例帮助页。</span><span class="sxs-lookup"><span data-stu-id="e8298-223">The following illustrations show sample help pages.</span></span>

![Web API 帮助页](creating-web-projects-in-visual-studio/_static/image12.png)

![用于 GET API 的 Web API 帮助页](creating-web-projects-in-visual-studio/_static/image13.png)

<span data-ttu-id="e8298-226">有关 Web API 的详细信息，请参阅[ASP.NET Web API](https://asp.net/web-api)。</span><span class="sxs-lookup"><span data-stu-id="e8298-226">For more information about Web API, see [ASP.NET Web API](https://asp.net/web-api).</span></span>

<a id="spa"></a>
### <a name="single-page-application-template"></a><span data-ttu-id="e8298-227">Single Page Application Template（单页应用程序模板）</span><span class="sxs-lookup"><span data-stu-id="e8298-227">Single Page Application Template</span></span>

<span data-ttu-id="e8298-228">单页应用程序 （SPA） 模板创建一个示例应用程序，该应用程序在客户端上使用 JavaScript、HTML 5 和[挖空JS，](http://knockoutjs.com/)并在服务器上ASP.NET Web API。</span><span class="sxs-lookup"><span data-stu-id="e8298-228">The Single Page Application (SPA) template creates a sample application that uses JavaScript, HTML 5, and [KnockoutJS](http://knockoutjs.com/) on the client, and ASP.NET Web API on the server.</span></span>

<span data-ttu-id="e8298-229">SPA 模板的唯一身份验证选项是[个人用户帐户](#indauth)。</span><span class="sxs-lookup"><span data-stu-id="e8298-229">The only authentication option for the SPA template is [Individual User Accounts](#indauth).</span></span>

<span data-ttu-id="e8298-230">下图显示了 SPA 模板生成的示例应用程序的初始状态。</span><span class="sxs-lookup"><span data-stu-id="e8298-230">The following illustration shows the initial state of the sample application that the SPA template builds.</span></span>

![SPA 示例应用](creating-web-projects-in-visual-studio/_static/image14.png)

<span data-ttu-id="e8298-232">有关如何使用 SPA 模板创建应用程序的信息，请参阅[Web API - 外部身份验证服务](../../../web-api/overview/security/external-authentication-services.md)。</span><span class="sxs-lookup"><span data-stu-id="e8298-232">For information about how to create an application by using the SPA template, see [Web API - External Authentication Services](../../../web-api/overview/security/external-authentication-services.md).</span></span>

<span data-ttu-id="e8298-233">有关ASP.NET单页应用程序以及使用 JavaScript 框架（而不是挖空JS）的其他 SPA 模板的详细信息，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="e8298-233">For more information about ASP.NET Single Page Applications, and about additional SPA templates that use JavaScript frameworks other than KnockoutJS, see the following resources:</span></span>

- <span data-ttu-id="e8298-234">[ASP.NET单页应用程序](../../../single-page-application/index.md)。</span><span class="sxs-lookup"><span data-stu-id="e8298-234">[ASP.NET Single Page Application](../../../single-page-application/index.md).</span></span>
- [<span data-ttu-id="e8298-235">了解 VS2013 RC SPA 模板中的安全功能</span><span class="sxs-lookup"><span data-stu-id="e8298-235">Understanding Security Features in the SPA Template for VS2013 RC</span></span>](https://blogs.msdn.com/b/webdev/archive/2013/09/20/understanding-security-features-in-spa-template.aspx)
- [<span data-ttu-id="e8298-236">单页应用程序：使用ASP.NET构建现代、响应迅速的 Web 应用程序</span><span class="sxs-lookup"><span data-stu-id="e8298-236">Single-Page Applications: Build Modern, Responsive Web Apps with ASP.NET</span></span>](https://msdn.microsoft.com/magazine/dn463786.aspx)

<a id="facebook"></a>
### <a name="facebook-template"></a><span data-ttu-id="e8298-237">Facebook 模板</span><span class="sxs-lookup"><span data-stu-id="e8298-237">Facebook Template</span></span>

<span data-ttu-id="e8298-238">您可以安装一个[视觉工作室扩展，提供一个Facebook模板](https://go.microsoft.com/fwlink/?LinkID=509965&amp;clcid=0x409)。</span><span class="sxs-lookup"><span data-stu-id="e8298-238">You can install a [Visual Studio extension that provides a Facebook template](https://go.microsoft.com/fwlink/?LinkID=509965&amp;clcid=0x409).</span></span> <span data-ttu-id="e8298-239">此模板创建一个示例应用程序，该应用程序旨在在 Facebook 网站内运行。</span><span class="sxs-lookup"><span data-stu-id="e8298-239">This template creates a sample application that is designed to run inside the Facebook web site.</span></span> <span data-ttu-id="e8298-240">它基于ASP.NET MVC，并使用 Web API 进行实时更新功能。</span><span class="sxs-lookup"><span data-stu-id="e8298-240">It is based on ASP.NET MVC and uses Web API for real-time update functionality.</span></span>

<span data-ttu-id="e8298-241">Facebook 模板没有可用的身份验证选项，因为 Facebook 应用程序在 Facebook 网站内运行，并且依赖于 Facebook 的身份验证。</span><span class="sxs-lookup"><span data-stu-id="e8298-241">No authentication options are available for the Facebook template because Facebook applications run within the Facebook site and rely on Facebook's authentication.</span></span>

<span data-ttu-id="e8298-242">有关ASP.NET Facebook 应用程序的详细信息，请参阅[更新 MVC Facebook API](https://blogs.msdn.com/b/webdev/archive/2014/06/10/updating-the-mvc-facebook-api.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e8298-242">For more information about ASP.NET Facebook applications, see [Updating the MVC Facebook API](https://blogs.msdn.com/b/webdev/archive/2014/06/10/updating-the-mvc-facebook-api.aspx).</span></span>

<a id="vs2012"></a>
### <a name="visual-studio-2012-templates"></a><span data-ttu-id="e8298-243">视觉工作室 2012 模板</span><span class="sxs-lookup"><span data-stu-id="e8298-243">Visual Studio 2012 Templates</span></span>

<span data-ttu-id="e8298-244">Visual Studio 2013 Web 项目创建对话框不提供对 Visual Studio 2012 中提供的某些模板的访问。</span><span class="sxs-lookup"><span data-stu-id="e8298-244">The Visual Studio 2013 web project creation dialog does not provide access to some templates that were available in Visual Studio 2012.</span></span> <span data-ttu-id="e8298-245">如果要使用这些模板之一，可以单击"可视化工作室新项目"对话框左侧窗格中的 Visual Studio 2012 节点。</span><span class="sxs-lookup"><span data-stu-id="e8298-245">If you want to use one of these templates, you can click the Visual Studio 2012 node in the left pane of the Visual Studio New Project dialog box.</span></span>

![可视化工作室 2012 模板](creating-web-projects-in-visual-studio/_static/image15.png)

<span data-ttu-id="e8298-247">**Visual Studio 2012**节点允许您在 Visual Studio 2013 的默认模板列表中选择您无法访问的以下 Web 模板：</span><span class="sxs-lookup"><span data-stu-id="e8298-247">The **Visual Studio 2012** node lets you choose the following web templates that you don't have access to in the default list of templates for Visual Studio 2013:</span></span>

- <span data-ttu-id="e8298-248">ASP.NET MVC 4 Web 应用程序</span><span class="sxs-lookup"><span data-stu-id="e8298-248">ASP.NET MVC 4 Web Application</span></span>
- <span data-ttu-id="e8298-249">ASP.NET 动态数据实体 Web 应用程序</span><span class="sxs-lookup"><span data-stu-id="e8298-249">ASP.NET Dynamic Data Entities Web Application</span></span>
- <span data-ttu-id="e8298-250">ASP.NET AJAX 服务器控制</span><span class="sxs-lookup"><span data-stu-id="e8298-250">ASP.NET AJAX Server Control</span></span>
- <span data-ttu-id="e8298-251">ASP.NET AJAX 服务器控制扩展器</span><span class="sxs-lookup"><span data-stu-id="e8298-251">ASP.NET AJAX Server Control Extender</span></span>
- <span data-ttu-id="e8298-252">ASP.NET服务器控制</span><span class="sxs-lookup"><span data-stu-id="e8298-252">ASP.NET Server Control</span></span>

<a id="bootstrap"></a>
## <a name="bootstrap-in-the-visual-studio-2013-web-project-templates"></a><span data-ttu-id="e8298-253">可视化工作室 2013 Web 项目模板中的引导</span><span class="sxs-lookup"><span data-stu-id="e8298-253">Bootstrap in the Visual Studio 2013 web project templates</span></span>

<span data-ttu-id="e8298-254">Visual Studio 2013 项目模板使用[Bootstrap，](http://getbootstrap.com/)这是一个由 Twitter 创建的布局和主框。</span><span class="sxs-lookup"><span data-stu-id="e8298-254">The Visual Studio 2013 project templates use [Bootstrap](http://getbootstrap.com/), a layout and theming framework created by Twitter.</span></span> <span data-ttu-id="e8298-255">Bootstrap 使用 CSS3 提供响应式设计，这意味着布局可以动态适应不同的浏览器窗口大小。</span><span class="sxs-lookup"><span data-stu-id="e8298-255">Bootstrap uses CSS3 to provide responsive design, which means layouts can dynamically adapt to different browser window sizes.</span></span> <span data-ttu-id="e8298-256">例如，在宽浏览器窗口中，Web 窗体模板创建的主页如下所示：</span><span class="sxs-lookup"><span data-stu-id="e8298-256">For example, in a wide browser window the home page created by the Web Forms template looks like the following illustration:</span></span>

![Web 表单模板应用主页](creating-web-projects-in-visual-studio/_static/image16.png)

<span data-ttu-id="e8298-258">使窗口变窄，水平排列的列移动到垂直排列中：</span><span class="sxs-lookup"><span data-stu-id="e8298-258">Make the window narrower, and the horizontally arranged columns move into vertical arrangement:</span></span>

![引导垂直柱排列](creating-web-projects-in-visual-studio/_static/image17.png)

<span data-ttu-id="e8298-260">稍微缩小窗口范围，水平顶部菜单将变为一个图标，您可以单击该图标以展开为垂直方向的菜单：</span><span class="sxs-lookup"><span data-stu-id="e8298-260">Narrow the window a little more, and the horizontal top menu turns into an icon that you can click to expand into a vertically oriented menu:</span></span>

![引导菜单图标](creating-web-projects-in-visual-studio/_static/image18.png)

![引导垂直菜单](creating-web-projects-in-visual-studio/_static/image19.png)

<span data-ttu-id="e8298-263">您还可以使用 Bootstrap 的"主"功能轻松影响应用程序的外观和感觉的变化。</span><span class="sxs-lookup"><span data-stu-id="e8298-263">You can also use Bootstrap's theming feature to easily effect a change in the application's look and feel.</span></span> <span data-ttu-id="e8298-264">例如，您可以执行以下步骤来更改主题。</span><span class="sxs-lookup"><span data-stu-id="e8298-264">For example, you can do the following steps to change the theme.</span></span>

1. <span data-ttu-id="e8298-265">在浏览器中，转到[http://Bootswatch.com](http://Bootswatch.com)，选择主题，然后单击"**下载**"。</span><span class="sxs-lookup"><span data-stu-id="e8298-265">In your browser, go to [http://Bootswatch.com](http://Bootswatch.com), choose a theme, and then click **Download**.</span></span> <span data-ttu-id="e8298-266">（默认情况下，此下载*引导.min.css;* 如果要检查 CSS 代码，请获取*引导.css*而不是小版本。</span><span class="sxs-lookup"><span data-stu-id="e8298-266">(This downloads *bootstrap.min.css* by default; if you want to examine the CSS code, get *bootstrap.css* instead of the minified version.)</span></span>
2. <span data-ttu-id="e8298-267">复制下载的 CSS 文件的内容。</span><span class="sxs-lookup"><span data-stu-id="e8298-267">Copy the contents of the downloaded CSS file.</span></span>
3. <span data-ttu-id="e8298-268">在 Visual Studio 中，在*内容*文件夹中创建名为*bootstrap-thethe.css*的新**样式表**文件，并将下载的 CSS 代码粘贴到其中。</span><span class="sxs-lookup"><span data-stu-id="e8298-268">In Visual Studio, create a new **Style Sheet** file named *bootstrap-theme.css* in the *Content* folder and paste the downloaded CSS code into it.</span></span>
4. <span data-ttu-id="e8298-269">打开*应用程序\_开始/捆绑.配置*和更改*引导.css*到*引导主题.css*.</span><span class="sxs-lookup"><span data-stu-id="e8298-269">Open *App\_Start/Bundle.config* and change *bootstrap.css* to *bootstrap-theme.css*.</span></span>

<span data-ttu-id="e8298-270">再次运行项目，应用程序具有新外观。</span><span class="sxs-lookup"><span data-stu-id="e8298-270">Run the project again, and the application has a new look.</span></span> <span data-ttu-id="e8298-271">下图显示了阿米莉亚主题的效果：</span><span class="sxs-lookup"><span data-stu-id="e8298-271">The following illustration shows the effect of the Amelia theme:</span></span>

![靴子阿米莉亚主题](creating-web-projects-in-visual-studio/_static/image20.png)

<span data-ttu-id="e8298-273">许多引导主题是可用的，无论是免费和高级版本。</span><span class="sxs-lookup"><span data-stu-id="e8298-273">Many Bootstrap themes are available, both free and premium versions.</span></span> <span data-ttu-id="e8298-274">Bootstrap 还提供多种 UI 组件，如[下拉](http://twitter.github.io/bootstrap/components.html#dropdowns)、[按钮组](http://twitter.github.io/bootstrap/components.html#buttonGroups)和[图标](http://twitter.github.io/bootstrap/base-css.html#images)。</span><span class="sxs-lookup"><span data-stu-id="e8298-274">Bootstrap also offers a wide variety of UI components, such as [drop-downs](http://twitter.github.io/bootstrap/components.html#dropdowns), [button groups](http://twitter.github.io/bootstrap/components.html#buttonGroups), and [icons](http://twitter.github.io/bootstrap/base-css.html#images).</span></span> <span data-ttu-id="e8298-275">有关引导器的详细信息，请参阅[引导站点](http://twitter.github.io/bootstrap/)。</span><span class="sxs-lookup"><span data-stu-id="e8298-275">For more information about Bootstrap, see [the Bootstrap site](http://twitter.github.io/bootstrap/).</span></span>

<span data-ttu-id="e8298-276">如果在 Visual Studio 中使用 Web 窗体设计器，请注意，设计器不支持 CSS3，因此无法准确显示 Bootstrap 主题或响应式布局更改的所有效果。</span><span class="sxs-lookup"><span data-stu-id="e8298-276">If you use the Web Forms designer in Visual Studio, note that the designer doesn't support CSS3, so it doesn't accurately show all the effects of Bootstrap themes or responsive layout changes.</span></span> <span data-ttu-id="e8298-277">但是，使用浏览器查看时，Web 窗体页面将正确显示。</span><span class="sxs-lookup"><span data-stu-id="e8298-277">However, the Web Forms pages will display correctly when viewed with a browser.</span></span>

<a id="add"></a>
## <a name="adding-support-for-additional-frameworks"></a><span data-ttu-id="e8298-278">添加对附加框架的支持</span><span class="sxs-lookup"><span data-stu-id="e8298-278">Adding Support for Additional Frameworks</span></span>

<span data-ttu-id="e8298-279">选择模板时，将自动选择模板所使用的框架的复选框。</span><span class="sxs-lookup"><span data-stu-id="e8298-279">When you select a template, the check box for the framework(s) used by the template is automatically selected.</span></span> <span data-ttu-id="e8298-280">例如，如果选择 **"Web 窗体"** 模板，则选中 **"Web 窗体"** 复选框，但无法清除该模板。</span><span class="sxs-lookup"><span data-stu-id="e8298-280">For example, if you select the **Web Forms** template, the **Web Forms** check box is selected and you can't clear it.</span></span>

![选择模板](creating-web-projects-in-visual-studio/_static/image21.png)

![添加框架](creating-web-projects-in-visual-studio/_static/image22.png)

<span data-ttu-id="e8298-283">可以为模板中未包含的框架选择复选框，以便在创建项目时添加对该框架的支持。</span><span class="sxs-lookup"><span data-stu-id="e8298-283">You can select the check box for a framework that isn't included in the template in order to add support for that framework when the project is created.</span></span> <span data-ttu-id="e8298-284">例如，要在选择 MVC 模板时启用 Web 窗体 *.aspx*页面的使用，请选择 **"Web 窗体"** 复选框。</span><span class="sxs-lookup"><span data-stu-id="e8298-284">For example, to enable the use of Web Forms *.aspx* pages when you've selected the MVC template, select the **Web Forms** check box.</span></span> <span data-ttu-id="e8298-285">或者，要在使用 Web 窗体模板时启用 MVC，请单击**MVC**复选框。</span><span class="sxs-lookup"><span data-stu-id="e8298-285">Or to enable MVC when you're using the Web Forms template, click the **MVC** check box.</span></span> <span data-ttu-id="e8298-286">添加框架可实现设计时和运行时支持。</span><span class="sxs-lookup"><span data-stu-id="e8298-286">Adding a framework enables design-time as well as run-time support.</span></span> <span data-ttu-id="e8298-287">例如，如果将 MVC 支持添加到 Web 窗体项目，则可以对控制器和视图进行基架。</span><span class="sxs-lookup"><span data-stu-id="e8298-287">For example, if you add MVC support to a Web Forms project, you will be able to scaffold controllers and views.</span></span>

<span data-ttu-id="e8298-288">如果在项目中组合 Web 窗体和 MVC 并在 Web 窗体中启用[友好 URL，](http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx)则可能存在意外的路由问题，其中一个 URL 具有多个可能的目标。</span><span class="sxs-lookup"><span data-stu-id="e8298-288">If you combine Web Forms and MVC in a project and enable [Friendly URLs](http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx) in Web Forms, there might be unexpected routing problems where one URL has multiple possible targets.</span></span> <span data-ttu-id="e8298-289">首先定义的路由将优先。</span><span class="sxs-lookup"><span data-stu-id="e8298-289">The routes that are defined first will take precedence.</span></span> <span data-ttu-id="e8298-290">例如`Home`，如果您有控制器和*Home.aspx*页，则如果在`http://contoso.com/home` *RouteConfig.cs*调用`Home``MapRoute``EnableFriendlyUrls``EnableFriendlyUrls``MapRoute`该方法之前调用 该方法，则 URL 将转到*Home.aspx，* 或者，如果之前调用，则相同的 URL 将转到控制器的默认视图。</span><span class="sxs-lookup"><span data-stu-id="e8298-290">For example, if you have a `Home` controller and a *Home.aspx* page, the `http://contoso.com/home` URL will go to *Home.aspx* if you call the `EnableFriendlyUrls` method before you call the `MapRoute` method in *RouteConfig.cs*, or the same URL will go to the default view for your `Home` controller if you call `MapRoute` before `EnableFriendlyUrls`.</span></span>

<span data-ttu-id="e8298-291">添加框架不会添加任何示例应用程序功能。</span><span class="sxs-lookup"><span data-stu-id="e8298-291">Adding a framework does not add any sample application functionality.</span></span> <span data-ttu-id="e8298-292">例如，如果在选择 MVC 模板时添加 Web 窗体支持，则不会创建*Default.aspx*主页文件。</span><span class="sxs-lookup"><span data-stu-id="e8298-292">For example, if you add Web Forms support when you've selected the MVC template, no *Default.aspx* home page file is created.</span></span> <span data-ttu-id="e8298-293">仅添加支持框架所需的文件夹、文件和引用。</span><span class="sxs-lookup"><span data-stu-id="e8298-293">Only the folders, files, and references required to support the framework are added.</span></span> <span data-ttu-id="e8298-294">因此，添加框架不会更改身份验证选项，这些选项由模板创建的示例应用程序中的代码实现。</span><span class="sxs-lookup"><span data-stu-id="e8298-294">For that reason, adding frameworks doesn't change authentication options, which are implemented by code in sample applications created by the templates.</span></span> <span data-ttu-id="e8298-295">例如，如果选择"空模板"并添加 Web 窗体或 MVC 支持，则仍将禁用 **"配置身份验证"** 按钮。</span><span class="sxs-lookup"><span data-stu-id="e8298-295">For example, if you select the Empty template and add Web Forms or MVC support, the **Configure Authentication** button will still be disabled.</span></span>

<span data-ttu-id="e8298-296">以下各节简要描述每个复选框的效果。</span><span class="sxs-lookup"><span data-stu-id="e8298-296">The following sections describe briefly the effect of each check box.</span></span>

### <a name="add-web-forms-support"></a><span data-ttu-id="e8298-297">添加 Web 表单支持</span><span class="sxs-lookup"><span data-stu-id="e8298-297">Add Web Forms Support</span></span>

<span data-ttu-id="e8298-298">创建空*的应用\_数据和\*\*模型*文件夹和*全局.asax*文件。</span><span class="sxs-lookup"><span data-stu-id="e8298-298">Creates empty *App\_Data* and *Models* folders and a *Global.asax* file.</span></span> <span data-ttu-id="e8298-299">这些模板已由空模板以外的所有模板创建，因此选择"Web 窗体"复选框对其他模板没有影响。</span><span class="sxs-lookup"><span data-stu-id="e8298-299">These are already created by all templates other than the Empty template, so selecting the Web Forms check box makes no difference for other templates.</span></span>

<span data-ttu-id="e8298-300">默认情况下，Web 窗体模板启用友好 URL，但当您通过选择"Web 窗体"复选框将 Web 窗体支持添加到其他模板时，不会自动启用"友好 URL"。</span><span class="sxs-lookup"><span data-stu-id="e8298-300">The Web Forms template enables Friendly URLs by default, but when you add Web Forms support to other templates by selecting the Web Forms check box Friendly URLs are not automatically enabled.</span></span>

### <a name="add-mvc-support"></a><span data-ttu-id="e8298-301">添加 MVC 支持</span><span class="sxs-lookup"><span data-stu-id="e8298-301">Add MVC Support</span></span>

<span data-ttu-id="e8298-302">安装 MVC、Razor 和 WebPages NuGet 包，创建空*的应用\_数据*、*控制器*、*模型*和*视图*文件夹，使用*RouteConfig.cs*文件创建*应用\_启动*文件夹，并创建*Global.asax*文件。</span><span class="sxs-lookup"><span data-stu-id="e8298-302">Installs MVC, Razor, and WebPages NuGet packages, creates empty *App\_Data*, *Controllers*, *Models*, and *Views* folders, creates *App\_Start* folder with *RouteConfig.cs* file, and creates *Global.asax* file.</span></span>

### <a name="add-web-api-support"></a><span data-ttu-id="e8298-303">添加 Web API 支持</span><span class="sxs-lookup"><span data-stu-id="e8298-303">Add Web API Support</span></span>

<span data-ttu-id="e8298-304">安装 WebApi 和 Newtonsoft.Json NuGet 包，创建空*的应用程序\_数据*、*控制器*和*模型*文件夹，创建包含*WebApiConfig.cs*文件*的应用程序\_启动*文件夹，并创建*Global.asax*文件。</span><span class="sxs-lookup"><span data-stu-id="e8298-304">Installs WebApi and Newtonsoft.Json NuGet packages, creates empty *App\_Data*, *Controllers*, and *Models* folders, creates *App\_Start* folder with *WebApiConfig.cs* file, and creates *Global.asax* file.</span></span>

<a id="auth"></a>
## <a name="authentication-methods"></a><span data-ttu-id="e8298-305">身份验证方法</span><span class="sxs-lookup"><span data-stu-id="e8298-305">Authentication Methods</span></span>

<span data-ttu-id="e8298-306">Visual Studio 2013 为 Web 窗体、MVC 和 Web API 模板提供了多个身份验证选项：</span><span class="sxs-lookup"><span data-stu-id="e8298-306">Visual Studio 2013 offers several authentication options for the Web Forms, MVC, and Web API templates:</span></span>

- [<span data-ttu-id="e8298-307">无身份验证</span><span class="sxs-lookup"><span data-stu-id="e8298-307">No Authentication</span></span>](#noauth)
- <span data-ttu-id="e8298-308">[个人用户帐户](#indauth)（ASP.NET标识，以前称为ASP.NET成员资格）</span><span class="sxs-lookup"><span data-stu-id="e8298-308">[Individual User Accounts](#indauth) (ASP.NET Identity, formerly known as ASP.NET membership)</span></span>
- <span data-ttu-id="e8298-309">[组织帐户](#orgauth)（Windows 服务器活动目录或 Azure 活动目录）</span><span class="sxs-lookup"><span data-stu-id="e8298-309">[Organizational Accounts](#orgauth) (Windows Server Active Directory or Azure Active Directory)</span></span>
- <span data-ttu-id="e8298-310">[窗口身份验证](#winauth)（内联网）</span><span class="sxs-lookup"><span data-stu-id="e8298-310">[Windows Authentication](#winauth) (Intranet)</span></span>

![配置身份验证对话框](creating-web-projects-in-visual-studio/_static/image23.png)

<a id="noauth"></a>

### <a name="no-authentication"></a><span data-ttu-id="e8298-312">无身份验证</span><span class="sxs-lookup"><span data-stu-id="e8298-312">No Authentication</span></span>

<span data-ttu-id="e8298-313">如果选择 **"无身份验证"，** 则示例应用程序将不包含用于登录的网页、指示登录者使用的 UI、成员资格数据库的实体类以及成员资格数据库的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="e8298-313">If you select **No Authentication**, the sample application will contain no web pages for logging in, no UI indicating who is logged in, no entity classes for a membership database, and no connection string for a membership database.</span></span>

<a id="indauth"></a>
### <a name="individual-user-accounts"></a><span data-ttu-id="e8298-314">单个用户帐户</span><span class="sxs-lookup"><span data-stu-id="e8298-314">Individual User Accounts</span></span>

<span data-ttu-id="e8298-315">如果选择 **"个人用户帐户**"，则示例应用程序将配置为使用ASP.NET标识（以前称为ASP.NET成员资格）进行用户身份验证。</span><span class="sxs-lookup"><span data-stu-id="e8298-315">If you select **Individual User Accounts**, the sample application will be configured to use ASP.NET Identity (formerly known as ASP.NET membership) for user authentication.</span></span> <span data-ttu-id="e8298-316">ASP.NET身份允许用户通过在网站上创建用户名和密码或与 Facebook、Google、微软帐户或 Twitter 等社交提供商登录来注册帐户。</span><span class="sxs-lookup"><span data-stu-id="e8298-316">ASP.NET Identity enables a user to register an account, by creating a username and password on the site or by signing in with social providers such as Facebook, Google, Microsoft Account, or Twitter.</span></span> <span data-ttu-id="e8298-317">ASP.NET标识中用户配置文件的默认数据存储是 SQL Server LocalDB 数据库，您可以将该数据库部署到生产站点的 SQL Server 或 Azure SQL 数据库。</span><span class="sxs-lookup"><span data-stu-id="e8298-317">The default data store for user profiles in ASP.NET Identity is a SQL Server LocalDB database, which you can deploy to SQL Server or Azure SQL Database for the production site.</span></span>

<span data-ttu-id="e8298-318">在 Visual Studio 2013 中，这些功能与 Visual Studio 2012 中的功能相同，但ASP.NET成员资格系统的基础代码已被重写。</span><span class="sxs-lookup"><span data-stu-id="e8298-318">In Visual Studio 2013 these features are the same as in Visual Studio 2012, but the underlying code for the ASP.NET membership system has been rewritten.</span></span> <span data-ttu-id="e8298-319">新代码库的优点包括：</span><span class="sxs-lookup"><span data-stu-id="e8298-319">Advantages of the new code base include the following:</span></span>

- <span data-ttu-id="e8298-320">新的成员资格系统基于[OWIN](http://owin.org/)而不是ASP.NET窗体身份验证模块。</span><span class="sxs-lookup"><span data-stu-id="e8298-320">The new membership system is based on [OWIN](http://owin.org/) rather than the ASP.NET Forms Authentication module.</span></span> <span data-ttu-id="e8298-321">这意味着无论您是在 IIS 中使用 Web 窗体还是 MVC，还是自托管 Web API 或 SignalR，您都可以使用相同的身份验证机制。</span><span class="sxs-lookup"><span data-stu-id="e8298-321">This means that you can use the same authentication mechanism whether you're using Web Forms or MVC in IIS, or you're self-hosting Web API or SignalR.</span></span>
- <span data-ttu-id="e8298-322">新的成员资格数据库由实体框架代码优先管理，所有表都由可以修改的实体类表示。</span><span class="sxs-lookup"><span data-stu-id="e8298-322">The new membership database is managed by Entity Framework Code First, and all of the tables are represented by entity classes that you can modify.</span></span> <span data-ttu-id="e8298-323">这意味着您可以轻松地自定义数据库架构和配置文件相关的 Web UI 以满足您自己的需求，并且可以使用代码优先迁移轻松部署更新。</span><span class="sxs-lookup"><span data-stu-id="e8298-323">This means that you can easily customize the database schema and profile-related web UI to fit your own needs, and you can easily deploy your updates using Code First Migrations.</span></span>

<span data-ttu-id="e8298-324">新的成员资格系统在新模板中自动实现，可以在以 .NET 4.5 或更高版本为目标的任何项目中手动实现。</span><span class="sxs-lookup"><span data-stu-id="e8298-324">The new membership system is implemented automatically in the new templates, and it can be implemented manually in any project that targets .NET 4.5 or later.</span></span>

<span data-ttu-id="e8298-325">ASP.NET身份是一个不错的选择，如果你正在创建一个互联网网站，主要是为外部客户。</span><span class="sxs-lookup"><span data-stu-id="e8298-325">ASP.NET Identity is a good choice if you are creating an Internet web site which is mainly for external customers.</span></span> <span data-ttu-id="e8298-326">如果您的组织使用 Active Directory 或 Office 365，并且希望创建一个为员工和业务合作伙伴启用单一登录的项目，则 **"组织帐户"** 选项可能是一个更好的选择。</span><span class="sxs-lookup"><span data-stu-id="e8298-326">If your organization uses Active Directory or Office 365 and you want to create a project that enables single-sign-on for employees and business partners, the **Organizational Accounts** option might be a better choice.</span></span>

<span data-ttu-id="e8298-327">有关"个人用户帐户"选项的详细信息，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="e8298-327">For more information about the Individual User Accounts option, see the following resources:</span></span>

- <span data-ttu-id="e8298-328">[www.asp.net/identity](../../../identity/index.md).</span><span class="sxs-lookup"><span data-stu-id="e8298-328">[www.asp.net/identity](../../../identity/index.md).</span></span> <span data-ttu-id="e8298-329">有关ASP.NET网站上ASP.NET标识的文档。</span><span class="sxs-lookup"><span data-stu-id="e8298-329">Documentation about ASP.NET Identity on the ASP.NET web site.</span></span>
- <span data-ttu-id="e8298-330">[创建一个ASP.NETMVC 5应用程序与Facebook和谷歌Auth2和开放ID登录](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)。</span><span class="sxs-lookup"><span data-stu-id="e8298-330">[Create an ASP.NET MVC 5 App with Facebook and Google OAuth2 and OpenID Sign-on](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md).</span></span> <span data-ttu-id="e8298-331">还演示如何自定义用户配置文件数据。</span><span class="sxs-lookup"><span data-stu-id="e8298-331">Also shows how to customize user profile data.</span></span>
- [<span data-ttu-id="e8298-332">Web API - 外部身份验证服务</span><span class="sxs-lookup"><span data-stu-id="e8298-332">Web API - External Authentication Services</span></span>](../../../web-api/overview/security/external-authentication-services.md)
- [<span data-ttu-id="e8298-333">在 Visual Studio 2013 中向ASP.NET应用程序添加外部登录</span><span class="sxs-lookup"><span data-stu-id="e8298-333">Adding External Logins to your ASP.NET application in Visual Studio 2013</span></span>](https://blogs.msdn.com/b/webdev/archive/2013/06/27/adding-external-logins-to-your-asp-net-application-in-visual-studio-2013.aspx)

<a id="orgauth"></a>
### <a name="organizational-accounts"></a><span data-ttu-id="e8298-334">组织帐户</span><span class="sxs-lookup"><span data-stu-id="e8298-334">Organizational Accounts</span></span>

<span data-ttu-id="e8298-335">如果选择 **"组织帐户**"，则示例应用程序将配置为使用 Windows 标识基础 （WIF） 根据 Azure 活动目录（Azure AD，包括 Office 365）或 Windows 服务器活动目录中的用户帐户进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="e8298-335">If you select **Organizational Accounts**, the sample application will be configured to use Windows Identity Foundation (WIF) for authentication based on user accounts in Azure Active Directory (Azure AD, which includes Office 365) or Windows Server Active Directory.</span></span> <span data-ttu-id="e8298-336">有关详细信息，请参阅本主题后面的[组织帐户身份验证选项](#orgauthoptions)。</span><span class="sxs-lookup"><span data-stu-id="e8298-336">For more information, see [Organizational account authentication options](#orgauthoptions) later in this topic.</span></span>

<a id="winauth"></a>
### <a name="windows-authentication"></a><span data-ttu-id="e8298-337">Windows 身份验证</span><span class="sxs-lookup"><span data-stu-id="e8298-337">Windows Authentication</span></span>

<span data-ttu-id="e8298-338">如果选择**Windows 身份验证**，则示例应用程序将配置为使用 Windows 身份验证 IIS 模块进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="e8298-338">If you select **Windows Authentication**, the sample application will be configured to use the Windows Authentication IIS module for authentication.</span></span> <span data-ttu-id="e8298-339">应用程序将显示登录到 Windows 但不包括用户注册或登录 UI 的 Active 目录或本地计算机帐户的域和用户 ID。</span><span class="sxs-lookup"><span data-stu-id="e8298-339">The application will display the domain and user ID of the Active directory or local machine account that is logged into Windows but won't include user registration or log-in UI.</span></span> <span data-ttu-id="e8298-340">此选项适用于 Intranet 网站。</span><span class="sxs-lookup"><span data-stu-id="e8298-340">This option is intended for Intranet web sites.</span></span>

<span data-ttu-id="e8298-341">或者，您可以通过在[组织帐户下选择"本地"选项](#orgauthonprem)来创建使用 AD 身份验证的 Intranet 站点。</span><span class="sxs-lookup"><span data-stu-id="e8298-341">Alternatively, you can create an Intranet site that uses AD authentication by choosing the [On-Premises option under Organizational Accounts](#orgauthonprem).</span></span> <span data-ttu-id="e8298-342">"本地"选项使用 Windows 标识基础 （WIF） 而不是 Windows 身份验证模块。</span><span class="sxs-lookup"><span data-stu-id="e8298-342">The On-Premises option uses Windows Identity Foundation (WIF) instead of the Windows Authentication module.</span></span> <span data-ttu-id="e8298-343">需要执行一些其他步骤才能设置"本地"选项，但 WIF 启用 Windows 身份验证模块中不可用的功能。</span><span class="sxs-lookup"><span data-stu-id="e8298-343">Some additional steps are required in order to set up the On-Premises option, but WIF enables features that aren't available with the Windows Authentication module.</span></span> <span data-ttu-id="e8298-344">例如，使用 WIF 可以在 Active Directory 和查询目录数据中配置应用程序访问。</span><span class="sxs-lookup"><span data-stu-id="e8298-344">For example, with WIF you can configure application access in Active Directory and query directory data.</span></span>

<a id="orgauthoptions"></a>
## <a name="organizational-account-authentication-options"></a><span data-ttu-id="e8298-345">组织帐户身份验证选项</span><span class="sxs-lookup"><span data-stu-id="e8298-345">Organizational account authentication options</span></span>

<span data-ttu-id="e8298-346">**"配置身份验证"** 对话框为 Azure 活动目录（Azure AD，包括 Office 365）或 Windows 服务器活动目录 （AD） 帐户身份验证提供了多个选项：</span><span class="sxs-lookup"><span data-stu-id="e8298-346">The **Configure Authentication** dialog gives you several options for Azure Active Directory (Azure AD, which includes Office 365) or Windows Server Active Directory (AD) account authentication:</span></span>

- <span data-ttu-id="e8298-347">[云 - 单个组织](#orgauthsingle)（使用与 Azure AD 的目录集成的 Azure AD 或 AD）</span><span class="sxs-lookup"><span data-stu-id="e8298-347">[Cloud - Single Organization](#orgauthsingle) (Azure AD, or AD using directory integration with Azure AD)</span></span>
- <span data-ttu-id="e8298-348">[云 - 多组织](#orgauthmulti)（使用目录与 Azure AD 集成的 Azure AD 或 AD）</span><span class="sxs-lookup"><span data-stu-id="e8298-348">[Cloud - Multi Organization](#orgauthmulti) (Azure AD, or AD using directory integration with Azure AD)</span></span>
- <span data-ttu-id="e8298-349">[内部（AD）](#orgauthonprem)</span><span class="sxs-lookup"><span data-stu-id="e8298-349">[On-Premises](#orgauthonprem) (AD)</span></span>

<span data-ttu-id="e8298-350">如果要尝试 Azure AD 选项之一，但尚未拥有帐户，[请单击此处注册 Azure AD 帐户](https://go.microsoft.com/fwlink/?LinkId=309942)。</span><span class="sxs-lookup"><span data-stu-id="e8298-350">If you want to try one of the Azure AD options but don't have an account yet, [click here to sign up for a Azure AD account](https://go.microsoft.com/fwlink/?LinkId=309942).</span></span>

> [!NOTE]
> <span data-ttu-id="e8298-351">如果选择 Azure AD 选项之一，则项目需要数据库，并且必须登录到 Azure AD 租户的全局管理员帐户。</span><span class="sxs-lookup"><span data-stu-id="e8298-351">If you choose one of the Azure AD options, your project requires a database and you have to sign in to a global administrator account for your Azure AD tenant.</span></span> <span data-ttu-id="e8298-352">输入具有 Azure AD 租户管理权限的组织帐户的名称admin@contoso.onmicrosoft.com和密码。</span><span class="sxs-lookup"><span data-stu-id="e8298-352">Enter the name and password for an organizational account (for example, admin@contoso.onmicrosoft.com) that has administrative permissions for your Azure AD tenant.</span></span>
> 
> <span data-ttu-id="e8298-353">**不要在登录对话框中输入 Microsoft 帐户的凭据（例如contoso@hotmail.com）。**</span><span class="sxs-lookup"><span data-stu-id="e8298-353">**Don't enter credentials for a Microsoft account (for example, contoso@hotmail.com) in the sign-in dialog box.**</span></span>

<a id="orgauthsingle"></a>
### <a name="cloud---single-organization-authentication"></a><span data-ttu-id="e8298-354">云 - 单一组织身份验证</span><span class="sxs-lookup"><span data-stu-id="e8298-354">Cloud - Single Organization Authentication</span></span>

![单一组织身份验证](creating-web-projects-in-visual-studio/_static/image24.png)

<span data-ttu-id="e8298-356">如果要为一个 Azure AD[租户](https://technet.microsoft.com/library/jj573650.aspx)中定义的用户帐户启用身份验证，请选择此选项。</span><span class="sxs-lookup"><span data-stu-id="e8298-356">Choose this option if you want to enable authentication for user accounts that are defined in one Azure AD [tenant](https://technet.microsoft.com/library/jj573650.aspx).</span></span> <span data-ttu-id="e8298-357">例如，该网站contoso.com，它将提供给 Contoso 公司位于租户contoso.onmicrosoft.com的员工。</span><span class="sxs-lookup"><span data-stu-id="e8298-357">For example, the site is contoso.com and it will be made available to employees of the Contoso Company who are in the contoso.onmicrosoft.com tenant.</span></span> <span data-ttu-id="e8298-358">您将无法将 Azure AD 配置为允许其他租户的用户访问应用程序。</span><span class="sxs-lookup"><span data-stu-id="e8298-358">You won't be able to configure Azure AD to allow users from other tenants to access the application.</span></span>

#### <a name="domain"></a><span data-ttu-id="e8298-359">域</span><span class="sxs-lookup"><span data-stu-id="e8298-359">Domain</span></span>

<span data-ttu-id="e8298-360">输入要在 中设置应用程序的 Azure AD 域，例如： `contoso.onmicrosoft.com`</span><span class="sxs-lookup"><span data-stu-id="e8298-360">Enter the Azure AD domain that you want to set up the application in, for example: `contoso.onmicrosoft.com`.</span></span> <span data-ttu-id="e8298-361">如果您有[自定义域](http://www.cloudidentity.com/blog/2013/04/14/adding-a-custom-domain-to-your-windows-azure-ad/)，例如`contoso.com`，`contoso.onmicrosoft.com`可以在此处输入该域。</span><span class="sxs-lookup"><span data-stu-id="e8298-361">If you have a [custom domain](http://www.cloudidentity.com/blog/2013/04/14/adding-a-custom-domain-to-your-windows-azure-ad/), such as `contoso.com` instead of `contoso.onmicrosoft.com`, you can enter that here.</span></span>

#### <a name="access-level"></a><span data-ttu-id="e8298-362">访问级别</span><span class="sxs-lookup"><span data-stu-id="e8298-362">Access Level</span></span>

<span data-ttu-id="e8298-363">如果应用程序需要使用图形 API 查询或更新目录信息，请选择**单一登录、读取目录数据**或**单一登录、读取和写入目录数据**。</span><span class="sxs-lookup"><span data-stu-id="e8298-363">If the application needs to query or update directory information by using the Graph API, choose **Single Sign-On, Read Directory Data** or **Single Sign-On, Read and Write Directory Data**.</span></span> <span data-ttu-id="e8298-364">否则，请选择**单一登录**。</span><span class="sxs-lookup"><span data-stu-id="e8298-364">Otherwise, choose **Single Sign-On**.</span></span> <span data-ttu-id="e8298-365">有关详细信息，请参阅[应用程序访问级别](https://msdn.microsoft.com/library/windowsazure/b08d91fa-6a64-4deb-92f4-f5857add9ed8#BKMK_AccessLevels)和使用图形[API 查询 Azure AD](https://msdn.microsoft.com/library/windowsazure/dn151791.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e8298-365">For more information, see [Application Access Levels](https://msdn.microsoft.com/library/windowsazure/b08d91fa-6a64-4deb-92f4-f5857add9ed8#BKMK_AccessLevels) and [Using the Graph API to Query Azure AD](https://msdn.microsoft.com/library/windowsazure/dn151791.aspx).</span></span>

#### <a name="application-id-uri"></a><span data-ttu-id="e8298-366">应用程序 ID URI</span><span class="sxs-lookup"><span data-stu-id="e8298-366">Application ID URI</span></span>

<span data-ttu-id="e8298-367">默认情况下，模板通过将项目名称追加到 Azure AD 域，为您创建应用程序 ID URI。</span><span class="sxs-lookup"><span data-stu-id="e8298-367">By default, the template creates an application ID URI for you by appending the project name to the Azure AD domain.</span></span> <span data-ttu-id="e8298-368">例如，如果项目名称为`Example`，并且域为`contoso.onmicrosoft.com`，则应用程序 ID URI`https://contoso.onmicrosoft.com/Example`变为 。</span><span class="sxs-lookup"><span data-stu-id="e8298-368">For example, if the project name is `Example` and the domain is `contoso.onmicrosoft.com`, the application ID URI becomes `https://contoso.onmicrosoft.com/Example`.</span></span> <span data-ttu-id="e8298-369">如果要手动指定应用程序 ID URI，请展开 **"更多选项"** 部分，并在文本框中输入应用程序 ID URI。</span><span class="sxs-lookup"><span data-stu-id="e8298-369">If you want to manually specify the application ID URI, expand the **More Options** section and enter the application ID URI in the text box.</span></span> <span data-ttu-id="e8298-370">应用程序 ID URI 必须`https://`以 开头。</span><span class="sxs-lookup"><span data-stu-id="e8298-370">The application ID URI must begin with `https://`.</span></span>

<span data-ttu-id="e8298-371">默认情况下，如果已在 Azure AD 中预配的应用程序具有与 Visual Studio 用于项目的应用程序 ID URI 相同的应用程序 ID URI，则项目将连接到现有应用程序，而不是预配新应用程序。</span><span class="sxs-lookup"><span data-stu-id="e8298-371">By default, if an application that is already provisioned in Azure AD has the same application ID URI as the one that Visual Studio is using for the project, the project will be connected to the existing application instead of provisioning a new one.</span></span> <span data-ttu-id="e8298-372">如果希望在这种情况下预配新应用程序，**请清除"覆盖应用程序条目"（如果具有相同 ID 的应用程序条目已存在**）复选框。</span><span class="sxs-lookup"><span data-stu-id="e8298-372">If you want a new application to be provisioned in that case, clear the **Overwrite the application entry if one with the same ID already exists** check box.</span></span>

<span data-ttu-id="e8298-373">如果清除 **"覆盖**"复选框，并且 Visual Studio 查找具有相同应用程序 ID URI 的现有应用程序，则通过将数字追加到要使用的 URI 来创建新 URI。</span><span class="sxs-lookup"><span data-stu-id="e8298-373">If the **Overwrite** check box is cleared, and Visual Studio finds an existing application with the same application ID URI, it creates a new URI by appending a number to the URI it was going to use.</span></span> <span data-ttu-id="e8298-374">例如，假设项目名称为`Example`，您将文本框留空，清除**覆盖**复选框，Azure AD 租户已具有带有 URI`https://contoso.onmicrosoft.com/Example`的应用程序。</span><span class="sxs-lookup"><span data-stu-id="e8298-374">For example, suppose the project name is `Example`, you leave the text box blank, you clear the **Overwrite** check box, and the Azure AD tenant already has an application with the URI `https://contoso.onmicrosoft.com/Example`.</span></span> <span data-ttu-id="e8298-375">在这种情况下，将预配一个新应用程序，并设置应用程序 ID URI，如`https://contoso.onmicrosoft.com/Example_20130619330903`。</span><span class="sxs-lookup"><span data-stu-id="e8298-375">In that case, a new application will be provisioned with an application ID URI like `https://contoso.onmicrosoft.com/Example_20130619330903`.</span></span>

#### <a name="provisioning-the-application-in-azure-ad"></a><span data-ttu-id="e8298-376">在 Azure AD 中预配应用程序</span><span class="sxs-lookup"><span data-stu-id="e8298-376">Provisioning the application in Azure AD</span></span>

<span data-ttu-id="e8298-377">为了在 Azure AD 中预配应用程序或将项目连接到现有应用程序，Visual Studio 需要域的全局管理员的凭据。</span><span class="sxs-lookup"><span data-stu-id="e8298-377">In order to provision the application in Azure AD or connect the project to an existing application, Visual Studio needs the credentials of a global administrator for the domain.</span></span> <span data-ttu-id="e8298-378">在"**配置身份验证**"对话框中单击 **"确定"** 时，系统会提示您输入您指定的域的全局管理员的用户名和密码。</span><span class="sxs-lookup"><span data-stu-id="e8298-378">When you click **OK** in the **Configure Authentication** dialog box, you are prompted for the user name and password of a global administrator for the domain you specified.</span></span> <span data-ttu-id="e8298-379">稍后，当您单击 **"新建ASP.NET项目**"对话框中**创建项目**时，Visual Studio 在 Azure AD 中提供应用程序。</span><span class="sxs-lookup"><span data-stu-id="e8298-379">Later, when you click **Create Project** in the **New ASP.NET Project** dialog, Visual Studio provisions the application in Azure AD.</span></span> <span data-ttu-id="e8298-380">请注意，作为此过程的一部分，Visual Studio 会在 Web.config 文件中嵌入客户端机密值，该文件在创建一年后过期。</span><span class="sxs-lookup"><span data-stu-id="e8298-380">Note that as part of this process Visual Studio embeds client secret values in the Web.config file that expire one year after creation.</span></span>

<span data-ttu-id="e8298-381">有关如何创建使用**云 - 单一组织**身份验证的应用程序的信息，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="e8298-381">For information about how to create applications that use **Cloud - Single Organization** authentication, see the following resources:</span></span>

- [<span data-ttu-id="e8298-382">Azure 身份验证</span><span class="sxs-lookup"><span data-stu-id="e8298-382">Azure Authentication</span></span>](../2012/windows-azure-authentication.md)
- [<span data-ttu-id="e8298-383">使用 Azure AD 将登录名添加到 Web 应用程序中</span><span class="sxs-lookup"><span data-stu-id="e8298-383">Adding Sign-On to Your Web Application Using Azure AD</span></span>](https://msdn.microsoft.com/library/windowsazure/dn151790.aspx)
- [<span data-ttu-id="e8298-384">借助 Azure Active Directory 开发 ASP.NET 应用</span><span class="sxs-lookup"><span data-stu-id="e8298-384">Developing ASP.NET Apps with Azure Active Directory</span></span>](../../../identity/overview/getting-started/developing-aspnet-apps-with-windows-azure-active-directory.md)
- [<span data-ttu-id="e8298-385">使用 Azure AD 和 Microsoft OWIN 组件ASP.NET Web API 安全</span><span class="sxs-lookup"><span data-stu-id="e8298-385">Secure ASP.NET Web API with Azure AD and Microsoft OWIN Components</span></span>](https://msdn.microsoft.com/magazine/dn463788.aspx)

<span data-ttu-id="e8298-386">Visual Studio 2013 的教程尚未更新;教程指导您手动执行的一些操作在 Visual Studio 2013 中是自动化的。</span><span class="sxs-lookup"><span data-stu-id="e8298-386">The tutorials have not yet been updated for Visual Studio 2013; some of what the tutorials direct you to do manually is automated in Visual Studio 2013.</span></span>

<a id="orgauthmulti"></a>
### <a name="cloud---multi-organization-authentication"></a><span data-ttu-id="e8298-387">云 - 多组织身份验证</span><span class="sxs-lookup"><span data-stu-id="e8298-387">Cloud - Multi Organization Authentication</span></span>

![多个组织身份验证](creating-web-projects-in-visual-studio/_static/image25.png)

<span data-ttu-id="e8298-389">如果要为多个 Azure AD[租户](https://technet.microsoft.com/library/jj573650.aspx)中定义的用户帐户启用身份验证，请选择此选项。</span><span class="sxs-lookup"><span data-stu-id="e8298-389">Choose this option if you want to enable authentication for user accounts that are defined in multiple Azure AD [tenants](https://technet.microsoft.com/library/jj573650.aspx).</span></span> <span data-ttu-id="e8298-390">例如，该站点contoso.com，它将提供给 contoso 公司位于contoso.onmicrosoft.com租户的员工以及法布里卡姆公司fabrikam.onmicrosoft.com租户的员工。</span><span class="sxs-lookup"><span data-stu-id="e8298-390">For example, the site is contoso.com and it will be made available to employees of the Contoso Company who are in the contoso.onmicrosoft.com tenant, and employees of the Fabrikam Company who are in the fabrikam.onmicrosoft.com tenant.</span></span>

<span data-ttu-id="e8298-391">输入的设置和应用程序预配步骤类似于[单个组织身份验证](#orgauthsingle)。</span><span class="sxs-lookup"><span data-stu-id="e8298-391">The settings that you enter and the application provisioning step are similar to [single organization authentication](#orgauthsingle).</span></span>

<span data-ttu-id="e8298-392">有关如何创建使用**云 - 多组织**身份验证的应用程序的信息，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="e8298-392">For information about how to create applications that use **Cloud - Multi Organization** authentication, see the following resources:</span></span>

- <span data-ttu-id="e8298-393">[轻松 Web 应用与 Azure 活动&amp;目录集成，ASP.NET活动目录团队博客上的可视化工作室](https://blogs.msdn.com/b/active_directory_team_blog/archive/2013/06/26/improved-windows-azure-active-directory-integration-with-asp-net-amp-visual-studio.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e8298-393">[Easy Web App Integration with Azure Active Directory, ASP.NET &amp; Visual Studio](https://blogs.msdn.com/b/active_directory_team_blog/archive/2013/06/26/improved-windows-azure-active-directory-integration-with-asp-net-amp-visual-studio.aspx) on the Active Directory Team blog.</span></span>
- <span data-ttu-id="e8298-394">[使用 Azure AD 教程开发多租户 Web 应用程序](https://msdn.microsoft.com/library/windowsazure/dn151789.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e8298-394">[Developing Multi-Tenant Web Applications with Azure AD](https://msdn.microsoft.com/library/windowsazure/dn151789.aspx) tutorial.</span></span> <span data-ttu-id="e8298-395">本教程尚未更新为 Visual Studio 2013;本教程指导您手动执行的一些操作在 Visual Studio 2013 中是自动化的。</span><span class="sxs-lookup"><span data-stu-id="e8298-395">The tutorial hasn't yet been updated for Visual Studio 2013; some of what the tutorial directs you to do manually is automated in Visual Studio 2013.</span></span>
- <span data-ttu-id="e8298-396">[您必须在应用程序ASP.NET使用自己的多个组织注册，然后才能登录](http://www.cloudidentity.com/blog/2013/10/26/you-have-to-sign-up-with-your-own-multiple-organizations-asp-net-app-before-you-can-sign-in/)。</span><span class="sxs-lookup"><span data-stu-id="e8298-396">[You Have to Sign Up With Your Own Multiple Organizations ASP.NET App Before You Can Sign In](http://www.cloudidentity.com/blog/2013/10/26/you-have-to-sign-up-with-your-own-multiple-organizations-asp-net-app-before-you-can-sign-in/).</span></span> <span data-ttu-id="e8298-397">Vittorio Bertocci 的博客，解释如何解决人们在创建使用多组织身份验证的项目时遇到的常见问题。</span><span class="sxs-lookup"><span data-stu-id="e8298-397">Blog by Vittorio Bertocci that explains how to resolve a common problem people encounter when creating a project that uses multi-organization authentication.</span></span>

<a id="orgauthonprem"></a>
### <a name="on-premises-organizational-authentication"></a><span data-ttu-id="e8298-398">本地组织身份验证</span><span class="sxs-lookup"><span data-stu-id="e8298-398">On-Premises Organizational Authentication</span></span>

![本地组织身份验证](creating-web-projects-in-visual-studio/_static/image26.png)

<span data-ttu-id="e8298-400">如果要为 Windows 服务器活动目录 （AD） 中定义的用户帐户启用身份验证，并且不想使用 Azure AD，请选择此选项。</span><span class="sxs-lookup"><span data-stu-id="e8298-400">Choose this option if you want to enable authentication for user accounts that are defined in Windows Server Active Directory (AD), and you don't want to use Azure AD.</span></span> <span data-ttu-id="e8298-401">您可以使用此选项创建 Intranet 站点或 Internet 站点。</span><span class="sxs-lookup"><span data-stu-id="e8298-401">You can use this option to create an Intranet site or an Internet site.</span></span> <span data-ttu-id="e8298-402">对于 Internet 站点，请使用活动目录联合服务 （ADFS） 提供对 AD 的访问。</span><span class="sxs-lookup"><span data-stu-id="e8298-402">For an Internet site, use Active Directory Federation Services (ADFS) to provide access to AD.</span></span> <span data-ttu-id="e8298-403">有关详细信息，请参阅在[Visual Studio 2013 中使用具有ASP.NET的本地组织身份验证选项 （ADFS）。](http://www.cloudidentity.com/blog/2014/02/12/use-the-on-premises-organizational-authentication-option-adfs-with-asp-net-in-visual-studio-2013/)</span><span class="sxs-lookup"><span data-stu-id="e8298-403">For more information, see [Use the On-Premises Organizational Authentication Option (ADFS) With ASP.NET in Visual Studio 2013](http://www.cloudidentity.com/blog/2014/02/12/use-the-on-premises-organizational-authentication-option-adfs-with-asp-net-in-visual-studio-2013/).</span></span>

<span data-ttu-id="e8298-404">对于 Intranet 站点，作为替代方法，您可以选择[Windows 身份验证](#winauth)而不是此选项。</span><span class="sxs-lookup"><span data-stu-id="e8298-404">For an Intranet site, as an alternative you can choose [Windows Authentication](#winauth) instead of this option.</span></span> <span data-ttu-id="e8298-405">对于 Windows 身份验证选项，您不必提供元数据文档 URL。</span><span class="sxs-lookup"><span data-stu-id="e8298-405">For the Windows Authentication option you don't have to provide a metadata document URL.</span></span> <span data-ttu-id="e8298-406">但是，Windows 身份验证无法控制活动目录中的应用程序访问或查询目录数据。</span><span class="sxs-lookup"><span data-stu-id="e8298-406">However, Windows Authentication does not give you the ability to control application access in Active Directory or to query directory data.</span></span>

#### <a name="on-premises-authority"></a><span data-ttu-id="e8298-407">内部管理局</span><span class="sxs-lookup"><span data-stu-id="e8298-407">On-Premises Authority</span></span>

<span data-ttu-id="e8298-408">输入指向元数据文档的 URL。</span><span class="sxs-lookup"><span data-stu-id="e8298-408">Enter a URL that points to the metadata document.</span></span> <span data-ttu-id="e8298-409">元数据文档包含权限的坐标。</span><span class="sxs-lookup"><span data-stu-id="e8298-409">The metadata document contains the coordinates of the authority.</span></span> <span data-ttu-id="e8298-410">应用程序将使用这些坐标来驱动 Web 登录流。</span><span class="sxs-lookup"><span data-stu-id="e8298-410">The application will use those coordinates to drive the web sign-on flow.</span></span>

#### <a name="application-id-uri"></a><span data-ttu-id="e8298-411">应用程序 ID URI</span><span class="sxs-lookup"><span data-stu-id="e8298-411">Application ID URI</span></span>

<span data-ttu-id="e8298-412">提供 AD 可用于标识此应用程序的唯一 URI，或留空以让 Visual Studio 创建一个。</span><span class="sxs-lookup"><span data-stu-id="e8298-412">Provide a unique URI that AD can use to identify this application, or leave blank to let Visual Studio create one.</span></span>

<a id="nextsteps"></a>
## <a name="next-steps"></a><span data-ttu-id="e8298-413">后续步骤</span><span class="sxs-lookup"><span data-stu-id="e8298-413">Next steps</span></span>

<span data-ttu-id="e8298-414">本文档为在 Visual Studio 2013 中创建新ASP.NET Web 项目提供了一些基本帮助。</span><span class="sxs-lookup"><span data-stu-id="e8298-414">This document has provided some basic help for creating a new ASP.NET web project in Visual Studio 2013.</span></span> <span data-ttu-id="e8298-415">有关将 Visual Studio 用于 Web 开发的详细信息[https://www.asp.net/visual-studio/](../../index.md)，请参阅。</span><span class="sxs-lookup"><span data-stu-id="e8298-415">For more information about using for Visual Studio for web development, see [https://www.asp.net/visual-studio/](../../index.md).</span></span>

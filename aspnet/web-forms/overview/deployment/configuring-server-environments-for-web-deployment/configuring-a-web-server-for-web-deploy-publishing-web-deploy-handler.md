---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler
title: 配置用于 Web 部署发布的 Web 服务器（Web 部署处理程序）
author: jrjlee
description: 本主题介绍如何配置 Internet Information Services (IIS) web 服务器，以支持使用 IIS Web 部署汉语 .。。
ms.author: riande
ms.date: 01/29/2017
ms.assetid: 90ebf911-1c46-4470-b876-1335bd0f590f
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler
msc.type: authoredcontent
ms.openlocfilehash: af46b5a74309fbae4b5db072363e71d965445f9a
ms.sourcegitcommit: 4ed0b65ae32d9f35e42ee6296b877747e063df4d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/16/2020
ms.locfileid: "90609683"
---
# <a name="configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler"></a><span data-ttu-id="b5a4b-103">配置用于 Web 部署发布的 Web 服务器（Web 部署处理程序）</span><span class="sxs-lookup"><span data-stu-id="b5a4b-103">Configuring a Web Server for Web Deploy Publishing (Web Deploy Handler)</span></span>

[<span data-ttu-id="b5a4b-104">PDF 下载</span><span class="sxs-lookup"><span data-stu-id="b5a4b-104">PDF Download</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="b5a4b-105">本主题介绍如何使用 IIS Web 部署处理程序将 Internet Information Services (IIS) web 服务器配置为支持 web 发布和部署。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-105">This topic describes how to configure an Internet Information Services (IIS) web server to support web publishing and deployment using the IIS Web Deploy Handler.</span></span>
> 
> <span data-ttu-id="b5a4b-106">使用 Web 部署2.0 或更高版本时，有三种主要方法可用于将应用程序或站点获取到 Web 服务器。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-106">When you work with Web Deploy 2.0 or later, there are three main approaches you can use to get your applications or sites onto a web server.</span></span> <span data-ttu-id="b5a4b-107">你可以：</span><span class="sxs-lookup"><span data-stu-id="b5a4b-107">You can:</span></span>
> 
> - <span data-ttu-id="b5a4b-108">使用 *Web 部署远程代理服务*。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-108">Use the *Web Deploy Remote Agent Service*.</span></span> <span data-ttu-id="b5a4b-109">此方法需要较少的 web 服务器配置，但你需要提供本地服务器管理员的凭据才能将任何内容部署到服务器。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-109">This approach requires less configuration of the web server, but you need to provide the credentials of a local server administrator in order to deploy anything to the server.</span></span>
> - <span data-ttu-id="b5a4b-110">使用 *Web 部署处理程序*。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-110">Use the *Web Deploy Handler*.</span></span> <span data-ttu-id="b5a4b-111">这种方法更复杂，需要进行更多初始工作才能设置 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-111">This approach is a lot more complex and requires more initial effort to set up the web server.</span></span> <span data-ttu-id="b5a4b-112">但是，在使用此方法时，可以将 IIS 配置为允许非管理员用户执行部署。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-112">However, when you use this approach, you can configure IIS to allow non-administrator users to perform the deployment.</span></span> <span data-ttu-id="b5a4b-113">Web 部署处理程序仅在 IIS 版本7或更高版本中可用。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-113">The Web Deploy Handler is only available in IIS version 7 or later.</span></span>
> - <span data-ttu-id="b5a4b-114">使用 *脱机部署*。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-114">Use *offline deployment*.</span></span> <span data-ttu-id="b5a4b-115">此方法需要最少的 web 服务器配置，但服务器管理员必须手动将 web 包复制到服务器上，并通过 IIS 管理器将其导入。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-115">This approach requires the least configuration of the web server, but a server administrator must manually copy the web package onto the server and import it through IIS Manager.</span></span>
> 
> <span data-ttu-id="b5a4b-116">有关这些方法的主要功能、优点和缺点的详细信息，请参阅 [选择正确的 Web 部署方法](choosing-the-right-approach-to-web-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-116">For more information on the key features, advantages, and disadvantages of these approaches, see [Choosing the Right Approach to Web Deployment](choosing-the-right-approach-to-web-deployment.md).</span></span>

<span data-ttu-id="b5a4b-117">是，如果你希望允许非管理员用户将内容部署到特定的 IIS 网站。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-117">Yes, if you want to allow non-administrator users to deploy content to specific IIS websites.</span></span> <span data-ttu-id="b5a4b-118">此方法在以下类型的方案中通常是必需的：</span><span class="sxs-lookup"><span data-stu-id="b5a4b-118">This approach is often desirable in these types of scenarios:</span></span>

- <span data-ttu-id="b5a4b-119">过渡环境或生产环境，其中触发远程部署的人员或服务帐户不可能有权访问服务器管理员的凭据。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-119">Staging or production environments, where the person or service account that triggers the remote deployment is unlikely to have access to the credentials of a server administrator.</span></span>
- <span data-ttu-id="b5a4b-120">托管环境：你希望使远程用户能够更新其网站，而无需为他们提供对 web 服务器的完全控制权限， (或访问其他用户的网站) 。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-120">Hosted environments, where you want to give remote users the ability to update their websites without giving them full control of your web servers (or access to anyone else's websites).</span></span>

<span data-ttu-id="b5a4b-121">在开发或测试方案中，或在小型组织中，使用服务器管理员凭据部署内容通常不会争用资源。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-121">In development or test scenarios, or in smaller organizations, deploying content using server administrator credentials is often less contentious.</span></span> <span data-ttu-id="b5a4b-122">在这些情况下，将 web 服务器配置为支持使用 [Web 部署远程代理服务](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md) 进行部署，提供了更简单的方法。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-122">In these scenarios, configuring your web servers to support deployment using the [Web Deploy Remote Agent Service](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md) offers a more straightforward approach.</span></span>

## <a name="task-overview"></a><span data-ttu-id="b5a4b-123">任务概述</span><span class="sxs-lookup"><span data-stu-id="b5a4b-123">Task Overview</span></span>

<span data-ttu-id="b5a4b-124">若要将 web 服务器配置为使用 Web 部署处理程序方法从远程计算机接受和部署 web 包，需执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="b5a4b-124">To configure the web server to accept and deploy web packages from a remote computer using the Web Deploy Handler approach, you'll need to:</span></span>

- <span data-ttu-id="b5a4b-125">创建或选择一个域用户帐户 (要用于执行部署的凭据的 "非管理员用户" ) 。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-125">Create, or choose, a domain user account (the "non-administrator user") whose credentials you'll use to perform deployments.</span></span>
- <span data-ttu-id="b5a4b-126">安装 IIS 7.5，包括 Web 管理服务和基本身份验证模块。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-126">Install IIS 7.5, including the Web Management Service and the Basic Authentication module.</span></span>
- <span data-ttu-id="b5a4b-127">安装 Web 部署2.1 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-127">Install Web Deploy 2.1 or later.</span></span>
- <span data-ttu-id="b5a4b-128">将 Web 管理服务配置为允许远程连接，并启动服务。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-128">Configure the Web Management Service to allow remote connections, and start the service.</span></span>
- <span data-ttu-id="b5a4b-129">创建一个 IIS 网站来托管已部署的内容。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-129">Create an IIS website to host the deployed content.</span></span>
- <span data-ttu-id="b5a4b-130">在 IIS 管理器中为你的网站授予非管理员用户权限。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-130">Grant your non-administrator user permissions on your website in IIS Manager.</span></span>
- <span data-ttu-id="b5a4b-131">确保 Web 管理服务委派规则允许服务使用您的非管理员用户帐户添加和更改网站内容。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-131">Ensure that the Web Management Service delegation rules permit the service to add and change website content using your non-administrator user account.</span></span>
- <span data-ttu-id="b5a4b-132">配置任何防火墙以允许端口8172上的传入连接。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-132">Configure any firewalls to allow incoming connections on port 8172.</span></span>

<span data-ttu-id="b5a4b-133">若要专门托管 ContactManager 示例解决方案，还需要：</span><span class="sxs-lookup"><span data-stu-id="b5a4b-133">To host the ContactManager sample solution specifically, you'll also need to:</span></span>

- <span data-ttu-id="b5a4b-134">安装 .NET Framework 4.0。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-134">Install the .NET Framework 4.0.</span></span>
- <span data-ttu-id="b5a4b-135">安装 ASP.NET MVC 3。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-135">Install ASP.NET MVC 3.</span></span>

<span data-ttu-id="b5a4b-136">本主题将演示如何执行上述每个过程。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-136">This topic will show you how to perform each of these procedures.</span></span> <span data-ttu-id="b5a4b-137">本主题中的任务和演练假设你开始使用运行 Windows Server 2016 的干净服务器版本。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-137">The tasks and walkthroughs in this topic assume that you're starting with a clean server build running Windows Server 2016.</span></span> <span data-ttu-id="b5a4b-138">继续之前，请确保：</span><span class="sxs-lookup"><span data-stu-id="b5a4b-138">Before you continue, ensure that:</span></span>

- <span data-ttu-id="b5a4b-139">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="b5a4b-139">Windows Server 2016</span></span>
- <span data-ttu-id="b5a4b-140">服务器已加入域。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-140">The server is domain-joined.</span></span>
- <span data-ttu-id="b5a4b-141">服务器具有静态 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-141">The server has a static IP address.</span></span>

> [!NOTE]
> <span data-ttu-id="b5a4b-142">有关将计算机加入域的详细信息，请参阅将 [计算机加入到域并登录](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx)。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-142">For more information on joining computers to a domain, see [Joining Computers to the Domain and Logging On](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx).</span></span> <span data-ttu-id="b5a4b-143">有关配置静态 IP 地址的详细信息，请参阅 [配置静态 Ip 地址](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx)。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-143">For more information on configuring static IP addresses, see [Configure a Static IP Address](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx).</span></span>

## <a name="install-products-and-components"></a><span data-ttu-id="b5a4b-144">安装产品和组件</span><span class="sxs-lookup"><span data-stu-id="b5a4b-144">Install Products and Components</span></span>

<span data-ttu-id="b5a4b-145">本部分将指导你完成在 web 服务器上安装所需的产品和组件。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-145">This section will guide you through installing the required products and components on the web server.</span></span> <span data-ttu-id="b5a4b-146">在开始之前，好的做法是运行 Windows 更新以确保服务器完全处于最新状态。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-146">Before you begin, a good practice is to run Windows Update to ensure that your server is fully up to date.</span></span>

<span data-ttu-id="b5a4b-147">在这种情况下，需要安装以下内容：</span><span class="sxs-lookup"><span data-stu-id="b5a4b-147">In this case, you need to install these things:</span></span>

- <span data-ttu-id="b5a4b-148">**IIS 7 建议的配置**。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-148">**IIS 7 Recommended Configuration**.</span></span> <span data-ttu-id="b5a4b-149">这会使 **Web 服务器 (** web 服务器上的 iis) 角色，并安装承载 ASP.NET 应用程序所需的一组 iis 模块和组件。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-149">This enables the **Web Server (IIS)** role on your web server and installs the set of IIS modules and components that you need in order to host an ASP.NET application.</span></span>
- <span data-ttu-id="b5a4b-150">**IIS：管理服务**。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-150">**IIS: Management Service**.</span></span> <span data-ttu-id="b5a4b-151">这会在 IIS 中安装 (WMSvc) 的 Web 管理服务。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-151">This installs the Web Management Service (WMSvc) in IIS.</span></span> <span data-ttu-id="b5a4b-152">此服务启用 IIS 网站的远程管理，并向客户端公开 Web 部署处理程序终结点。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-152">This service enables remote management of IIS websites and exposes the Web Deploy Handler endpoint to clients.</span></span>
- <span data-ttu-id="b5a4b-153">**IIS：基本身份验证**。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-153">**IIS: Basic Authentication**.</span></span> <span data-ttu-id="b5a4b-154">这会安装 IIS 基本身份验证模块。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-154">This installs the IIS Basic Authentication module.</span></span> <span data-ttu-id="b5a4b-155">这使 Web 管理服务 (WMSvc) 验证你提供的凭据。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-155">This lets the Web Management Service (WMSvc) authenticate the credentials you provide.</span></span>
- <span data-ttu-id="b5a4b-156">**Web 部署工具2.1 或更高版本**。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-156">**Web Deployment Tool 2.1 or later**.</span></span> <span data-ttu-id="b5a4b-157">这会在服务器上安装 Web 部署 (及其基础可执行文件 MSDeploy.exe) 。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-157">This installs Web Deploy (and its underlying executable, MSDeploy.exe) on your server.</span></span> <span data-ttu-id="b5a4b-158">作为此过程的一部分，它将安装 Web 部署处理程序，并将其与 Web 管理服务集成。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-158">As part of this process, it installs the Web Deploy Handler and integrates it with the Web Management Service.</span></span>
- <span data-ttu-id="b5a4b-159">**.NET Framework 4.0**。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-159">**.NET Framework 4.0**.</span></span> <span data-ttu-id="b5a4b-160">这是运行在此版本的 .NET Framework 上构建的应用程序所必需的。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-160">This is required to run applications that were built on this version of the .NET Framework.</span></span>
- <span data-ttu-id="b5a4b-161">**ASP.NET MVC 3**。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-161">**ASP.NET MVC 3**.</span></span> <span data-ttu-id="b5a4b-162">这将安装运行 MVC 3 应用程序所需的程序集。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-162">This installs the assemblies you need to run MVC 3 applications.</span></span>

> [!NOTE]
> <span data-ttu-id="b5a4b-163">本演练介绍了如何使用 Web 平台安装程序来安装和配置各种组件。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-163">This walkthrough describes the use of the Web Platform Installer to install and configure various components.</span></span> <span data-ttu-id="b5a4b-164">尽管无需使用 Web 平台安装程序，但它可以通过自动检测依赖项并确保始终获取最新的产品版本来简化安装过程。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-164">Although you don't have to use the Web Platform Installer, it simplifies the installation process by automatically detecting dependencies and ensuring that you always get the latest product versions.</span></span> <span data-ttu-id="b5a4b-165">有关详细信息，请参阅 [Microsoft Web 平台安装程序](https://go.microsoft.com/?linkid=9805118)。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-165">For more information, see [Microsoft Web Platform Installer](https://go.microsoft.com/?linkid=9805118).</span></span>

<span data-ttu-id="b5a4b-166">**安装所需的产品和组件**</span><span class="sxs-lookup"><span data-stu-id="b5a4b-166">**To install the required products and components**</span></span>

1. <span data-ttu-id="b5a4b-167">下载并安装 [Web 平台安装程序](https://go.microsoft.com/?linkid=9805118)。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-167">Download and install the [Web Platform Installer](https://go.microsoft.com/?linkid=9805118).</span></span>
2. <span data-ttu-id="b5a4b-168">安装完成后，Web 平台安装程序将自动启动。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-168">When installation is complete, the Web Platform Installer will launch automatically.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b5a4b-169">你现在可以从 " **开始** " 菜单启动 Web 平台安装程序。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-169">You can now launch the Web Platform Installer at any time from the **Start** menu.</span></span> <span data-ttu-id="b5a4b-170">为此，请在 " **开始** " 菜单上，单击 " **所有程序**"，然后单击 " **Microsoft Web 平台安装程序**"。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-170">To do this, on the **Start** menu, click **All Programs**, and then click **Microsoft Web Platform Installer**.</span></span>
3. <span data-ttu-id="b5a4b-171">在“Web 平台安装程序”\*\*\*\* 窗口的顶部，单击“产品”\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-171">At the top of the **Web Platform Installer** window, click **Products**.</span></span>
4. <span data-ttu-id="b5a4b-172">在窗口左侧的导航窗格中，单击 " **框架**"。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-172">On the left side of the window, in the navigation pane, click **Frameworks**.</span></span>
5. <span data-ttu-id="b5a4b-173">在 **Microsoft .NET Framework 4** "行中，如果尚未安装 .NET Framework，请单击" **添加**"。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-173">In the **Microsoft .NET Framework 4** row, if the .NET Framework is not already installed, click **Add**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b5a4b-174">可能已通过 Windows 更新安装 .NET Framework 4.0。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-174">You may have already installed the .NET Framework 4.0 through Windows Update.</span></span> <span data-ttu-id="b5a4b-175">如果产品或组件已安装，Web 平台安装程序将通过将 " **添加** " 按钮替换为 **安装**的文本来指示这一点。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-175">If a product or component is already installed, the Web Platform Installer will indicate this by replacing the **Add** button with the text **Installed**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image1.png)
6. <span data-ttu-id="b5a4b-176">在 \*\*ASP.NET MVC 3 (Visual Studio 2010) \*\* 行中，单击 " **添加**"。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-176">In the **ASP.NET MVC 3 (Visual Studio 2010)** row, click **Add**.</span></span>
7. <span data-ttu-id="b5a4b-177">在导航窗格中，单击 " **服务器**"。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-177">In the navigation pane, click **Server**.</span></span>
8. <span data-ttu-id="b5a4b-178">在 " **IIS 7 推荐的配置** " 行中，单击 " **添加**"。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-178">In the **IIS 7 Recommended Configuration** row, click **Add**.</span></span>
9. <span data-ttu-id="b5a4b-179">在 **Web 部署工具 2.1** 行中，单击 " **添加**"。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-179">In the **Web Deployment Tool 2.1** row, click **Add**.</span></span>
10. <span data-ttu-id="b5a4b-180">在 " **IIS：基本身份验证** " 行中，单击 " **添加**"。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-180">In the **IIS: Basic Authentication** row, click **Add**.</span></span>
11. <span data-ttu-id="b5a4b-181">在 " **IIS：管理服务** " 行中，单击 " **添加**"。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-181">In the **IIS: Management Service** row, click **Add**.</span></span>
12. <span data-ttu-id="b5a4b-182">单击“安装” 。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-182">Click **Install**.</span></span> <span data-ttu-id="b5a4b-183">Web 平台安装程序将向你显示一个产品列表，其中包含要安装的任何关联依赖项&#x2014;&#x2014;，并将提示你接受许可条款。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-183">The Web Platform Installer will show you a list of products&#x2014;together with any associated dependencies&#x2014;to be installed and will prompt you to accept the license terms.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image2.png)
13. <span data-ttu-id="b5a4b-184">查看许可条款，如果同意条款，请单击 " **我接受**"。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-184">Review the license terms, and if you consent to the terms, click **I Accept**.</span></span>
14. <span data-ttu-id="b5a4b-185">安装完成后，单击 " **完成**"，然后关闭 " **Web 平台安装程序** " 窗口。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-185">When the installation is complete, click **Finish**, and then close the **Web Platform Installer** window.</span></span>

<span data-ttu-id="b5a4b-186">如果在安装 IIS 之前安装了 .NET Framework 4.0，则需要运行 [ASP.NET Iis 注册工具](https://msdn.microsoft.com/library/k6h9cz8h(v=VS.100).aspx) (aspnet \_regiis.exe) 向 IIS 注册 ASP.NET 的最新版本。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-186">If you installed the .NET Framework 4.0 before you installed IIS, you'll need to run the [ASP.NET IIS Registration Tool](https://msdn.microsoft.com/library/k6h9cz8h(v=VS.100).aspx) (aspnet\_regiis.exe) to register the latest version of ASP.NET with IIS.</span></span> <span data-ttu-id="b5a4b-187">如果不这样做，你会发现，IIS 将 (的静态内容提供) HTML 文件，但不会有任何问题，但在你尝试浏览到 ASP.NET 内容时，它将返回 **HTTP 错误404.0 –找不** 到。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-187">If you don't do this, you'll find that IIS will serve static content (like HTML files) without any problems, but it will return **HTTP Error 404.0 – Not Found** when you attempt to browse to ASP.NET content.</span></span> <span data-ttu-id="b5a4b-188">您可以使用下一个过程来确保 ASP.NET 4.0 已注册。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-188">You can use the next procedure to ensure that ASP.NET 4.0 is registered.</span></span>

<span data-ttu-id="b5a4b-189">**向 IIS 注册 ASP.NET 4。0**</span><span class="sxs-lookup"><span data-stu-id="b5a4b-189">**To register ASP.NET 4.0 with IIS**</span></span>

1. <span data-ttu-id="b5a4b-190">单击 " **开始**"，然后键入 **命令提示符**。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-190">Click **Start**, and then type **Command Prompt**.</span></span>
2. <span data-ttu-id="b5a4b-191">在搜索结果中，右键单击 " **命令提示符**"，然后单击 " **以管理员身份运行**"。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-191">In the search results, right-click **Command Prompt**, and then click **Run as administrator**.</span></span>
3. <span data-ttu-id="b5a4b-192">在命令提示符窗口中，导航到 " **%windir%\microsoft.net\framework\v4.0.30319 (对于** " 目录。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-192">In the Command Prompt window, navigate to the **%WINDIR%\Microsoft.NET\Framework\v4.0.30319** directory.</span></span>
4. <span data-ttu-id="b5a4b-193">键入以下命令，然后按 Enter：</span><span class="sxs-lookup"><span data-stu-id="b5a4b-193">Type this command, and then press Enter:</span></span>

    [!code-console[Main](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/samples/sample1.cmd)]
5. <span data-ttu-id="b5a4b-194">如果你打算随时托管64位 web 应用程序，则还应将 ASP.NET 的64位版本注册到 IIS。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-194">If you plan to host 64-bit web applications at any point, you should also register the 64-bit version of ASP.NET with IIS.</span></span> <span data-ttu-id="b5a4b-195">为此，请在命令提示符窗口中导航到 **%windir%\microsoft.net\framework64\v4.0.30319 (对于** 目录。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-195">To do this, in the Command Prompt window, navigate to the **%WINDIR%\Microsoft.NET\Framework64\v4.0.30319** directory.</span></span>
6. <span data-ttu-id="b5a4b-196">键入以下命令，然后按 Enter：</span><span class="sxs-lookup"><span data-stu-id="b5a4b-196">Type this command, and then press Enter:</span></span>

    [!code-console[Main](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/samples/sample2.cmd)]

<span data-ttu-id="b5a4b-197">作为一种很好的做法，请再次使用 Windows 更新，下载并安装适用于已安装的新产品和组件的任何可用更新。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-197">As a good practice, use Windows Update again at this point to download and install any available updates for the new products and components you've installed.</span></span>

## <a name="configure-the-web-management-service"></a><span data-ttu-id="b5a4b-198">配置 Web 管理服务</span><span class="sxs-lookup"><span data-stu-id="b5a4b-198">Configure the Web Management Service</span></span>

<span data-ttu-id="b5a4b-199">现在，你已安装了所需的一切，接下来的步骤是在 IIS 中配置 Web 管理服务。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-199">Now that you've installed everything you need, the next step is to configure the Web Management Service in IIS.</span></span> <span data-ttu-id="b5a4b-200">在高级别上，需要完成以下任务：</span><span class="sxs-lookup"><span data-stu-id="b5a4b-200">At a high level, you'll need to complete these tasks:</span></span>

- <span data-ttu-id="b5a4b-201">在服务器级别启用基本身份验证。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-201">Enable basic authentication at the server level.</span></span>
- <span data-ttu-id="b5a4b-202">将 Web 管理服务配置为接受远程连接。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-202">Configure the Web Management Service to accept remote connections.</span></span>
- <span data-ttu-id="b5a4b-203">启动 Web 管理服务。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-203">Start the Web Management Service.</span></span>
- <span data-ttu-id="b5a4b-204">检查所需的 Web 管理服务委派规则是否已就位。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-204">Check that the required Web Management Service delegation rules are in place.</span></span>

<span data-ttu-id="b5a4b-205">**配置 Web 管理服务**</span><span class="sxs-lookup"><span data-stu-id="b5a4b-205">**To configure the Web Management Service**</span></span>

1. <span data-ttu-id="b5a4b-206">在 " **开始** " 菜单上，指向 " **管理工具**"，然后单击 " **Internet Information Services (IIS) 管理器**"。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-206">On the **Start** menu, point to **Administrative Tools**, and then click **Internet Information Services (IIS) Manager**.</span></span>
2. <span data-ttu-id="b5a4b-207">在 IIS 管理器的 " **连接** " 窗格中，单击 "服务器" 节点 (例如 **STAGEWEB1**) 。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-207">In IIS Manager, in the **Connections** pane, click the server node (for example, **STAGEWEB1**).</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image3.png)
3. <span data-ttu-id="b5a4b-208">在中心窗格中的 " **IIS**" 下，双击 " **身份验证**"。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-208">In the center pane, under **IIS**, double-click **Authentication**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image20.png)
4. <span data-ttu-id="b5a4b-209">右键单击 " **基本身份验证**"，然后单击 " **启用**"。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-209">Right-click **Basic Authentication**, and then click **Enable**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image5.png)
5. <span data-ttu-id="b5a4b-210">在 " **连接** " 窗格中，再次单击服务器节点以返回到顶级设置。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-210">In the **Connections** pane, click the server node again to return to the top-level settings.</span></span>
6. <span data-ttu-id="b5a4b-211">在中心窗格中的 " **管理**" 下，双击 " **管理服务**"。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-211">In the center pane, under **Management**, double-click **Management Service**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image6.png)
7. <span data-ttu-id="b5a4b-212">在中心窗格中，选择 " **启用远程连接**"。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-212">In the center pane, select **Enable remote connections**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b5a4b-213">如果 Web 管理服务已经在运行，则需要先将其停止。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-213">If the Web Management Service is already running, you'll need to stop it first.</span></span>
8. <span data-ttu-id="b5a4b-214">在 " **操作** " 窗格中，单击 " **启动** " 以启动 Web 管理服务。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-214">In the **Actions** pane, click **Start** to start the Web Management Service.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image7.png)
9. <span data-ttu-id="b5a4b-215">如果系统提示你保存设置，请单击 **"是"**。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-215">If you're prompted to save your settings, click **Yes**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b5a4b-216">你可能还想要将服务配置为自动启动。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-216">You may also want to configure the service to start automatically.</span></span> <span data-ttu-id="b5a4b-217">为此，请打开 "服务" 控制台，右键单击 " **Web 管理服务**"，然后单击 " **属性**"。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-217">To do this, open the Services console, right-click **Web Management Service**, and then click **Properties**.</span></span> <span data-ttu-id="b5a4b-218">在 " **启动类型** " 下拉列表中，选择 " **自动**"，然后单击 **"确定"**。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-218">In the **Startup type** dropdown list, select **Automatic**, and then click **OK**.</span></span>
10. <span data-ttu-id="b5a4b-219">在 " **连接** " 窗格中，再次单击服务器节点以返回到顶级设置。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-219">In the **Connections** pane, click the server node again to return to the top-level settings.</span></span>
11. <span data-ttu-id="b5a4b-220">在中心窗格中的 " **管理**" 下，双击 " **管理服务委托**"。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-220">In the center pane, under **Management**, double-click **Management Service Delegation**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image8.png)
12. <span data-ttu-id="b5a4b-221">验证中心窗格是否包含一组规则。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-221">Verify that the center pane contains a set of rules.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image9.png)

    <span data-ttu-id="b5a4b-222">这些规则允许授权 Web 管理服务用户使用各种 Web 部署提供程序。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-222">These rules allow authorized Web Management Service users to use various Web Deploy providers.</span></span> <span data-ttu-id="b5a4b-223">例如，若要通过 Web 部署处理程序将 web 应用程序和内容部署到 IIS，则必须有一个委派规则，该规则允许所有经过身份**验证的 Web**管理**iisApp**服务用户 (可在屏幕快照) 中看到的最后一个规则。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-223">For example, to deploy web applications and content to IIS through the Web Deploy Handler, there must be a delegation rule that allows all authenticated Web Management Service users to use the **contentPath** and **iisApp** providers (the last rule that you can see in the screenshot).</span></span>

    <span data-ttu-id="b5a4b-224">如果按照本主题中所述的顺序安装了产品和组件，最新版本的 Web 部署应自动向 Web 管理服务添加所有必需的委派规则。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-224">If you installed products and components in the order described in this topic, the latest version of Web Deploy should automatically add all the required delegation rules to the Web Management Service.</span></span> <span data-ttu-id="b5a4b-225">如果 "管理服务委派" 页没有显示任何规则，则需要自行创建。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-225">If the Management Service Delegation page does not show any rules, you'll need to create them yourself.</span></span> <span data-ttu-id="b5a4b-226">有关如何执行此操作的说明，请参阅 [配置 Web 部署处理程序](https://go.microsoft.com/?linkid=9805124)。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-226">For instructions on how to do this, see [Configure the Web Deployment Handler](https://go.microsoft.com/?linkid=9805124).</span></span>
13. <span data-ttu-id="b5a4b-227">在 " **连接** " 窗格中，再次单击服务器节点以返回到顶级设置。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-227">In the **Connections** pane, click the server node again to return to the top-level settings.</span></span>

## <a name="create-and-configure-an-iis-website"></a><span data-ttu-id="b5a4b-228">创建和配置 IIS 网站</span><span class="sxs-lookup"><span data-stu-id="b5a4b-228">Create and Configure an IIS Website</span></span>

<span data-ttu-id="b5a4b-229">你需要创建并配置一个 IIS 网站来托管内容，然后才能将 web 内容部署到你的服务器。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-229">Before you can deploy web content to your server, you need to create and configure an IIS website to host the content.</span></span> <span data-ttu-id="b5a4b-230">Web 部署只能将 web 包部署到现有 IIS 网站;它无法为你创建网站。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-230">Web Deploy can only deploy web packages to an existing IIS website; it can't create the website for you.</span></span> <span data-ttu-id="b5a4b-231">还需要执行一些额外的配置，以允许非管理员帐户远程部署内容。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-231">You also need to do a little extra configuration to allow your non-administrator account to deploy content remotely.</span></span> <span data-ttu-id="b5a4b-232">在高级别上，需要完成以下任务：</span><span class="sxs-lookup"><span data-stu-id="b5a4b-232">At a high level, you'll need to complete these tasks:</span></span>

- <span data-ttu-id="b5a4b-233">在文件系统上创建一个文件夹以托管你的内容。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-233">Create a folder on the file system to host your content.</span></span>
- <span data-ttu-id="b5a4b-234">创建一个 IIS 网站来提供内容，并将其与本地文件夹关联。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-234">Create an IIS website to serve the content, and associate it with the local folder.</span></span>
- <span data-ttu-id="b5a4b-235">向本地文件夹上的应用程序池标识授予读取权限。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-235">Grant read permissions to the application pool identity on the local folder.</span></span>
- <span data-ttu-id="b5a4b-236">向将部署你的 web 应用程序的域帐户授予必要的 IIS 权限。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-236">Grant the necessary IIS permissions to the domain account that will deploy your web application.</span></span>

<span data-ttu-id="b5a4b-237">尽管不会阻止你将内容部署到 IIS 中的默认网站，但对于除测试或演示方案之外的任何内容，不建议使用此方法。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-237">Although there's nothing stopping you from deploying content to the default website in IIS, this approach is not recommended for anything other than test or demonstration scenarios.</span></span> <span data-ttu-id="b5a4b-238">若要模拟生产环境，应该创建一个新的 IIS 网站，其中包含特定于应用程序要求的设置。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-238">To simulate a production environment, you should create a new IIS website with settings that are specific to the requirements of your application.</span></span>

<span data-ttu-id="b5a4b-239">**创建 IIS 网站**</span><span class="sxs-lookup"><span data-stu-id="b5a4b-239">**To create an IIS website**</span></span>

1. <span data-ttu-id="b5a4b-240">在本地文件系统上，创建一个文件夹以存储内容 (例如 **C:\DemoSite**) 。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-240">On the local file system, create a folder to store your content (for example, **C:\DemoSite**).</span></span>
2. <span data-ttu-id="b5a4b-241">在 " **开始** " 菜单上，指向 " **管理工具**"，然后单击 " **Internet Information Services (IIS) 管理器**"。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-241">On the **Start** menu, point to **Administrative Tools**, and then click **Internet Information Services (IIS) Manager**.</span></span>
3. <span data-ttu-id="b5a4b-242">在 IIS 管理器的 " **连接** " 窗格中，展开 "服务器" 节点 (例如 **STAGEWEB1**) 。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-242">In IIS Manager, in the **Connections** pane, expand the server node (for example, **STAGEWEB1**).</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image10.png)
4. <span data-ttu-id="b5a4b-243">右键单击 " **站点** " 节点，然后单击 " **添加网站**"。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-243">Right-click the **Sites** node, and then click **Add Web Site**.</span></span>
5. <span data-ttu-id="b5a4b-244">在 " **站点名称** " 框中，键入 IIS 网站的名称 (例如， **DemoSite**) 。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-244">In the **Site name** box, type a name for the IIS website (for example, **DemoSite**).</span></span>
6. <span data-ttu-id="b5a4b-245">在 " **物理路径** " 框中，键入 (或浏览) 本地文件夹 (路径，例如 **C:\DemoSite**) 。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-245">In the **Physical path** box, type (or browse to) the path to your local folder (for example, **C:\DemoSite**).</span></span>
7. <span data-ttu-id="b5a4b-246">在 " **端口** " 框中，键入要在其上托管网站 (的端口号，例如 **85**) 。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-246">In the **Port** box, type the port number on which you want to host the website (for example, **85**).</span></span>

    > [!NOTE]
    > <span data-ttu-id="b5a4b-247">对于 HTTP，标准端口号为80，对于 HTTPS 则为443。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-247">The standard port numbers are 80 for HTTP and 443 for HTTPS.</span></span> <span data-ttu-id="b5a4b-248">但是，如果你在端口80上托管此网站，你将需要停止默认网站，然后才能访问你的站点。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-248">However, if you host this website on port 80, you'll need to stop the default website before you can access your site.</span></span>
8. <span data-ttu-id="b5a4b-249">将 " **主机名** " 框留空，除非要为网站配置域名系统 (DNS) 记录，然后单击 **"确定"**。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-249">Leave the **Host name** box blank, unless you want to configure a Domain Name System (DNS) record for the website, and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image11.png)

    > [!NOTE]
    > <span data-ttu-id="b5a4b-250">在生产环境中，你可能想要在端口80上托管你的网站，并配置主机标头和匹配的 DNS 记录。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-250">In a production environment, you'll likely want to host your website on port 80 and configure a host header, together with matching DNS records.</span></span> <span data-ttu-id="b5a4b-251">有关在 IIS 7 中配置主机标头的详细信息，请参阅 [配置网站的主机标头 (IIS 7) ](https://technet.microsoft.com/library/cc753195(WS.10).aspx)。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-251">For more information on configuring host headers in IIS 7, see [Configure a Host Header for a Web Site (IIS 7)](https://technet.microsoft.com/library/cc753195(WS.10).aspx).</span></span> <span data-ttu-id="b5a4b-252">有关 Windows Server 中的 DNS 服务器角色的详细信息，请参阅 [Dns 服务器概述](https://technet.microsoft.com/library/cc770392.aspx) 和 [dns 服务器](https://technet.microsoft.com/windowsserver/dd448607)。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-252">For more information on the DNS Server role in Windows Server, see [DNS Server Overview](https://technet.microsoft.com/library/cc770392.aspx) and [DNS Server](https://technet.microsoft.com/windowsserver/dd448607).</span></span>
9. <span data-ttu-id="b5a4b-253">在“操作” \*\*\*\* 窗格中的“编辑站点” \*\*\*\* 之下，单击“绑定” \*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-253">In the **Actions** pane, under **Edit Site**, click **Bindings**.</span></span>
10. <span data-ttu-id="b5a4b-254">在“网站绑定”\*\*\*\* 对话框中，单击“添加”\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-254">In the **Site Bindings** dialog box, click **Add**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image12.png)
11. <span data-ttu-id="b5a4b-255">在 " **添加站点绑定** " 对话框中，将 " **IP 地址** " 和 " **端口** " 设置为与现有站点配置匹配。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-255">In the **Add Site Binding** dialog box, set the **IP address** and **Port** to match your existing site configuration.</span></span>
12. <span data-ttu-id="b5a4b-256">在 " **主机名** " 框中，键入 web 服务器的名称 (例如 **STAGEWEB1**) ，然后单击 **"确定"**。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-256">In the **Host name** box, type the name of your web server (for example, **STAGEWEB1**), and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image13.png)

    > [!NOTE]
    > <span data-ttu-id="b5a4b-257">第一个站点绑定允许使用 IP 地址和端口或在本地访问站点 `http://localhost:85` 。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-257">The first site binding allows you to access the site locally using the IP address and port or `http://localhost:85`.</span></span> <span data-ttu-id="b5a4b-258">第二个站点绑定允许使用计算机名称从域中的其他计算机访问站点 (例如， http://stageweb1:85) 。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-258">The second site binding allows you to access the site from other computers on the domain using the machine name (for example, http://stageweb1:85).</span></span>
13. <span data-ttu-id="b5a4b-259">在 **“网站绑定”** 对话框中，单击 **“关闭”**。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-259">In the **Site Bindings** dialog box, click **Close**.</span></span>
14. <span data-ttu-id="b5a4b-260">在“连接”\*\*\*\* 窗格中，单击“应用程序池”\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-260">In the **Connections** pane, click **Application Pools**.</span></span>
15. <span data-ttu-id="b5a4b-261">在 " **应用程序池** " 窗格中，右键单击应用程序池的名称，然后单击 " **基本设置**"。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-261">In the **Application Pools** pane, right-click the name of your application pool, and then click **Basic Settings**.</span></span> <span data-ttu-id="b5a4b-262">默认情况下，应用程序池的名称将与网站的名称相匹配 (例如 **DemoSite**) 。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-262">By default, the name of your application pool will match the name of your website (for example, **DemoSite**).</span></span>
16. <span data-ttu-id="b5a4b-263">在 " **.NET clr 版本** " 列表中，选择 " **.net clr 4.0.30319**"，然后单击 **"确定"**。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-263">In the **.NET CLR version** list, select **.NET CLR v4.0.30319**, and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image21.png)

    > [!NOTE]
    > <span data-ttu-id="b5a4b-264">示例解决方案需要 .NET Framework 4.0。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-264">The sample solution requires .NET Framework 4.0.</span></span> <span data-ttu-id="b5a4b-265">这并不是对 Web 部署一般的要求。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-265">This is not a requirement for Web Deploy in general.</span></span>

<span data-ttu-id="b5a4b-266">为了使你的网站提供内容，应用程序池标识必须对存储内容的本地文件夹具有读取权限。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-266">In order for your website to serve content, the application pool identity must have read permissions on the local folder that stores the content.</span></span> <span data-ttu-id="b5a4b-267">在 IIS 7.5 中，应用程序池默认情况下使用唯一的应用程序池标识运行，与以前版本的 IIS 不同 (，应用程序池通常使用网络服务帐户) 运行。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-267">In IIS 7.5, application pools run with a unique application pool identity by default (in contrast to previous versions of IIS, where application pools would typically run using the Network Service account).</span></span> <span data-ttu-id="b5a4b-268">应用程序池标识不是真实的用户帐户，并且不会显示在&#x2014;的任何用户或组列表中，而是在启动应用程序池时动态创建。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-268">The application pool identity is not a real user account and does not show up on any lists of users or groups&#x2014;instead, it's created dynamically when the application pool is started.</span></span> <span data-ttu-id="b5a4b-269">每个应用程序池标识都作为隐藏项添加到本地 **IIS \_ iis-iusrs** 安全组。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-269">Each application pool identity is added to the local **IIS\_IUSRS** security group as a hidden item.</span></span>

<span data-ttu-id="b5a4b-270">若要授予对文件或文件夹上的应用程序池标识的权限，可以使用两个选项：</span><span class="sxs-lookup"><span data-stu-id="b5a4b-270">To grant permissions to an application pool identity on a file or folder, you have two options:</span></span>

- <span data-ttu-id="b5a4b-271">通过使用 \*\*Iis AppPool \( 应用程序池名称格式) \*\* (例如 **iis AppPool\DemoSite**) ，来直接将权限分配给应用程序池标识。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-271">Assign permissions to the application pool identity directly, using the format **IIS AppPool\(application pool name)** (for example, **IIS AppPool\DemoSite**).</span></span>
- <span data-ttu-id="b5a4b-272">将权限分配给 **IIS \_ iis-iusrs** 组。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-272">Assign permissions to the **IIS\_IUSRS** group.</span></span>

<span data-ttu-id="b5a4b-273">最常见的方法是将权限分配给本地 **IIS \_ iis-iusrs** 组，因为此方法允许你在不重新配置文件系统权限的情况下更改应用程序池。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-273">The most common approach is to assign permissions to the local **IIS\_IUSRS** group, because this approach lets you change application pools without reconfiguring file system permissions.</span></span> <span data-ttu-id="b5a4b-274">下一过程使用此基于组的方法。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-274">The next procedure uses this group-based approach.</span></span>

> [!NOTE]
> <span data-ttu-id="b5a4b-275">有关 IIS 7.5 中的应用程序池标识的详细信息，请参阅 [应用程序池标识](https://go.microsoft.com/?linkid=9805123)。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-275">For more information on application pool identities in IIS 7.5, see [Application Pool Identities](https://go.microsoft.com/?linkid=9805123).</span></span>

<span data-ttu-id="b5a4b-276">**配置 IIS 网站的文件夹权限**</span><span class="sxs-lookup"><span data-stu-id="b5a4b-276">**To configure folder permissions for an IIS website**</span></span>

1. <span data-ttu-id="b5a4b-277">在 Windows 资源管理器中，浏览到本地文件夹的位置。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-277">In Windows Explorer, browse to the location of your local folder.</span></span>
2. <span data-ttu-id="b5a4b-278">右键单击该文件夹，然后单击 **“属性”**。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-278">Right-click the folder, and then click **Properties**.</span></span>
3. <span data-ttu-id="b5a4b-279">在“**Security**”选项卡上，依次单击“**Edit**”、“**Add**”。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-279">On the **Security** tab, click **Edit**, and then click **Add**.</span></span>
4. <span data-ttu-id="b5a4b-280">单击“位置”。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-280">Click **Locations**.</span></span> <span data-ttu-id="b5a4b-281">在 " **位置** " 对话框中，选择本地服务器，然后单击 **"确定"**。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-281">In the **Locations** dialog box, select the local server, and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image15.png)
5. <span data-ttu-id="b5a4b-282">在 " **选择用户或组** " 对话框中，键入 **IIS \_ Iis-iusrs**，单击 " **检查名称**"，然后单击 **"确定"**。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-282">In the **Select Users or Groups** dialog box, type **IIS\_IUSRS**, click **Check Names**, and then click **OK**.</span></span>
6. <span data-ttu-id="b5a4b-283">在 " \*\* (文件夹名称) 的权限 \*\* " 对话框中，请注意，默认情况下已为新组分配了 " **读取 &amp; 执行**"、" **列出文件夹内容**" 和 " **读取** " 权限。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-283">In the **Permissions for (folder name)** dialog box, notice that the new group has been assigned the **Read &amp; execute**, **List folder contents**, and **Read** permissions by default.</span></span> <span data-ttu-id="b5a4b-284">保持不变，并单击 **"确定"**。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-284">Leave this unchanged and click **OK**.</span></span>
7. <span data-ttu-id="b5a4b-285">单击 **"确定"** 以关闭 "属性" 对话框 \*\* (文件夹) 名称\*\* 。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-285">Click **OK** to close the **(folder name) Properties** dialog box.</span></span>

<span data-ttu-id="b5a4b-286">作为最终任务，您必须向非管理员用户授予适当的权限，该用户的凭据将用于部署内容。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-286">As a final task, you must grant the appropriate permissions to the non-administrator user whose credentials you'll use to deploy content.</span></span> <span data-ttu-id="b5a4b-287">此用户需要权限以远程方式将内容部署到你的网站。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-287">This user requires the permissions to deploy content remotely to your website.</span></span>

<span data-ttu-id="b5a4b-288">**为非管理员域用户配置 IIS 网站权限**</span><span class="sxs-lookup"><span data-stu-id="b5a4b-288">**To configure IIS website permissions for a non-administrator domain user**</span></span>

1. <span data-ttu-id="b5a4b-289">在 IIS 管理器的 " **连接** " 窗格中，右键单击你的网站节点 (例如， **DemoSite**) "，指向" **部署**"，然后单击" **配置 "Web 部署发布**。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-289">In IIS Manager, in the **Connections** pane, right-click your website node (for example, **DemoSite**), point to **Deploy**, and then click **Configure Web Deploy Publishing**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image16.png)
2. <span data-ttu-id="b5a4b-290">在 " **配置 Web 部署发布** " 对话框中，在 " **选择要向其授予发布权限的用户** " 列表右侧，单击省略号按钮。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-290">In the **Configure Web Deploy Publishing** dialog box, to the right of the **Select a user to give publishing permissions** list, click the ellipsis button.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image17.png)
3. <span data-ttu-id="b5a4b-291">在 " **允许用户** " 对话框中，键入要用于部署内容的帐户的域和用户名，然后单击 **"确定"**。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-291">In the **Allow User** dialog box, type the domain and user name of the account you want to use to deploy content, and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image18.png)
4. <span data-ttu-id="b5a4b-292">在 " **配置 Web 部署发布** " 对话框中，单击 " **设置**"。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-292">In the **Configure Web Deploy Publishing** dialog box, click **Setup**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image19.png)

    > [!NOTE]
    > <span data-ttu-id="b5a4b-293">此操作在一个步骤中执行两项关键功能。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-293">This operation performs two key functions in one step.</span></span> <span data-ttu-id="b5a4b-294">首先，它授予用户通过 Web 管理服务远程修改网站的权限，具体取决于你在上一部分中检查的委派规则。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-294">First, it grants the user permission to modify the website remotely through the Web Management Service, according to the delegation rules you examined in the previous section.</span></span> <span data-ttu-id="b5a4b-295">其次，它向用户授予网站的源文件夹的完全控制权限，这允许用户对网站内容添加、修改和设置权限。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-295">Second, it grants the user full control of the source folder for the website, which allows the user to add, modify, and set permissions on the website content.</span></span>
5. <span data-ttu-id="b5a4b-296">在 " **配置 Web 部署发布** " 对话框中，单击 " **关闭**"。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-296">In the **Configure Web Deploy Publishing** dialog box, click **Close**.</span></span>

## <a name="configure-firewall-exceptions"></a><span data-ttu-id="b5a4b-297">配置防火墙例外</span><span class="sxs-lookup"><span data-stu-id="b5a4b-297">Configure Firewall Exceptions</span></span>

<span data-ttu-id="b5a4b-298">默认情况下，IIS Web 管理服务在 TCP 端口8172上进行侦听。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-298">By default, the IIS Web Management Service listens on TCP port 8172.</span></span> <span data-ttu-id="b5a4b-299">如果在 web 服务器上启用了 Windows 防火墙，则需要创建新的入站规则，以允许端口8172上的 TCP 流量 (默认情况下，Windows 防火墙) 中允许所有出站流量。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-299">If Windows Firewall is enabled on your web server, you'll need to create a new inbound rule to allow TCP traffic on port 8172 (all outbound traffic is permitted by default in Windows Firewall).</span></span> <span data-ttu-id="b5a4b-300">如果使用第三方防火墙，则需要创建允许流量的规则。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-300">If you use a third-party firewall, you'll need to create rules to allow traffic.</span></span>

| <span data-ttu-id="b5a4b-301">方向</span><span class="sxs-lookup"><span data-stu-id="b5a4b-301">Direction</span></span> | <span data-ttu-id="b5a4b-302">从端口</span><span class="sxs-lookup"><span data-stu-id="b5a4b-302">From Port</span></span> | <span data-ttu-id="b5a4b-303">到端口</span><span class="sxs-lookup"><span data-stu-id="b5a4b-303">To Port</span></span> | <span data-ttu-id="b5a4b-304">端口类型</span><span class="sxs-lookup"><span data-stu-id="b5a4b-304">Port Type</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b5a4b-305">入站</span><span class="sxs-lookup"><span data-stu-id="b5a4b-305">Inbound</span></span> | <span data-ttu-id="b5a4b-306">任意</span><span class="sxs-lookup"><span data-stu-id="b5a4b-306">Any</span></span> | <span data-ttu-id="b5a4b-307">8172</span><span class="sxs-lookup"><span data-stu-id="b5a4b-307">8172</span></span> | <span data-ttu-id="b5a4b-308">TCP</span><span class="sxs-lookup"><span data-stu-id="b5a4b-308">TCP</span></span> |
| <span data-ttu-id="b5a4b-309">出站</span><span class="sxs-lookup"><span data-stu-id="b5a4b-309">Outbound</span></span> | <span data-ttu-id="b5a4b-310">8172</span><span class="sxs-lookup"><span data-stu-id="b5a4b-310">8172</span></span> | <span data-ttu-id="b5a4b-311">任意</span><span class="sxs-lookup"><span data-stu-id="b5a4b-311">Any</span></span> | <span data-ttu-id="b5a4b-312">TCP</span><span class="sxs-lookup"><span data-stu-id="b5a4b-312">TCP</span></span> |

<span data-ttu-id="b5a4b-313">有关在 Windows 防火墙中配置规则的详细信息，请参阅 [配置防火墙规则](https://technet.microsoft.com/library/dd448559(WS.10).aspx)。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-313">For more information on configuring rules in Windows Firewall, see [Configuring Firewall Rules](https://technet.microsoft.com/library/dd448559(WS.10).aspx).</span></span> <span data-ttu-id="b5a4b-314">对于第三方防火墙，请查阅你的产品文档。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-314">For third-party firewalls, please consult your product documentation.</span></span>

## <a name="conclusion"></a><span data-ttu-id="b5a4b-315">结论</span><span class="sxs-lookup"><span data-stu-id="b5a4b-315">Conclusion</span></span>

<span data-ttu-id="b5a4b-316">你的 web 服务器现在应该已准备好通过 Web 管理服务接受到 Web 部署处理程序的远程部署。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-316">Your web server should now be ready to accept remote deployments to the Web Deploy Handler through the Web Management Service.</span></span> <span data-ttu-id="b5a4b-317">尝试将 web 应用程序部署到服务器之前，可能需要检查以下要点：</span><span class="sxs-lookup"><span data-stu-id="b5a4b-317">Before you attempt to deploy a web application to the server, you may want to check these key points:</span></span>

- <span data-ttu-id="b5a4b-318">是否在 IIS 中的服务器级别启用了基本身份验证？</span><span class="sxs-lookup"><span data-stu-id="b5a4b-318">Have you enabled basic authentication at the server level in IIS?</span></span>
- <span data-ttu-id="b5a4b-319">是否启用了到 Web 管理服务的远程连接？</span><span class="sxs-lookup"><span data-stu-id="b5a4b-319">Have you enabled remote connections to the Web Management Service?</span></span>
- <span data-ttu-id="b5a4b-320">是否已启动 Web 管理服务？</span><span class="sxs-lookup"><span data-stu-id="b5a4b-320">Have you started the Web Management Service?</span></span>
- <span data-ttu-id="b5a4b-321">是否有管理服务委派规则？</span><span class="sxs-lookup"><span data-stu-id="b5a4b-321">Are there management service delegation rules in place?</span></span>
- <span data-ttu-id="b5a4b-322">应用程序池标识是否具有对你的网站的源文件夹的 "读取" 访问权限？</span><span class="sxs-lookup"><span data-stu-id="b5a4b-322">Does the application pool identity have read access to the source folder for your website?</span></span>
- <span data-ttu-id="b5a4b-323">非管理员用户帐户在 IIS 中是否有站点级权限？</span><span class="sxs-lookup"><span data-stu-id="b5a4b-323">Does the non-administrator user account have site-level permissions in IIS?</span></span>
- <span data-ttu-id="b5a4b-324">防火墙是否允许在 TCP 端口8172上传入连接到服务器？</span><span class="sxs-lookup"><span data-stu-id="b5a4b-324">Does your firewall allow incoming connections to the server on TCP port 8172?</span></span>

## <a name="further-reading"></a><span data-ttu-id="b5a4b-325">深入阅读</span><span class="sxs-lookup"><span data-stu-id="b5a4b-325">Further Reading</span></span>

<span data-ttu-id="b5a4b-326">有关如何配置自定义 Microsoft 生成引擎 (MSBuild) 项目文件以将 web 包部署到 Web 部署处理程序的指南，请参阅 [配置目标环境的部署属性](configuring-deployment-properties-for-a-target-environment.md)。</span><span class="sxs-lookup"><span data-stu-id="b5a4b-326">For guidance on how to configure custom Microsoft Build Engine (MSBuild) project files to deploy web packages to the Web Deploy Handler, see [Configuring Deployment Properties for a Target Environment](configuring-deployment-properties-for-a-target-environment.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="b5a4b-327">[上一页](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)
> [下一页](configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)</span><span class="sxs-lookup"><span data-stu-id="b5a4b-327">[Previous](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)
[Next](configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)</span></span>

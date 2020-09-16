---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-remote-agent
title: 为 Web 部署发布 (远程代理) 配置 Web 服务器 |Microsoft Docs
author: jrjlee
description: 本主题介绍如何使用 IIS Web 部署将 Internet Information Services (IIS) web 服务器配置为支持 web 发布和部署 .。。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 239c7aa8-d09a-4d02-9c0e-6bd52be5f0d5
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-remote-agent
msc.type: authoredcontent
ms.openlocfilehash: 39064045bccfe01d00ded60df17f1e152e5c1190
ms.sourcegitcommit: 4ed0b65ae32d9f35e42ee6296b877747e063df4d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/16/2020
ms.locfileid: "90609681"
---
# <a name="configuring-a-web-server-for-web-deploy-publishing-remote-agent"></a><span data-ttu-id="60627-103">配置用于 Web 部署发布的 Web 服务器（远程代理）</span><span class="sxs-lookup"><span data-stu-id="60627-103">Configuring a Web Server for Web Deploy Publishing (Remote Agent)</span></span>

<span data-ttu-id="60627-104">作者： [Jason](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="60627-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="60627-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="60627-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="60627-106">本主题介绍如何使用 IIS Web 部署工具 (Web 部署远程代理服务，将 Internet Information Services (IIS) web 服务器配置为支持 web 发布和部署。</span><span class="sxs-lookup"><span data-stu-id="60627-106">This topic describes how to configure an Internet Information Services (IIS) web server to support web publishing and deployment using the IIS Web Deployment Tool (Web Deploy) Remote Agent Service.</span></span>
> 
> <span data-ttu-id="60627-107">使用 Web 部署2.0 或更高版本时，有三种主要方法可用于将应用程序或站点获取到 Web 服务器。</span><span class="sxs-lookup"><span data-stu-id="60627-107">When you work with Web Deploy 2.0 or later, there are three main approaches you can use to get your applications or sites onto a web server.</span></span> <span data-ttu-id="60627-108">你可以：</span><span class="sxs-lookup"><span data-stu-id="60627-108">You can:</span></span>
> 
> - <span data-ttu-id="60627-109">使用 *Web 部署远程代理服务*。</span><span class="sxs-lookup"><span data-stu-id="60627-109">Use the *Web Deploy Remote Agent Service*.</span></span> <span data-ttu-id="60627-110">此方法需要较少的 web 服务器配置，但你需要提供本地服务器管理员的凭据才能将任何内容部署到服务器。</span><span class="sxs-lookup"><span data-stu-id="60627-110">This approach requires less configuration of the web server, but you need to provide the credentials of a local server administrator in order to deploy anything to the server.</span></span>
> - <span data-ttu-id="60627-111">使用 *Web 部署处理程序*。</span><span class="sxs-lookup"><span data-stu-id="60627-111">Use the *Web Deploy Handler*.</span></span> <span data-ttu-id="60627-112">这种方法更复杂，需要进行更多初始工作才能设置 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="60627-112">This approach is a lot more complex and requires more initial effort to set up the web server.</span></span> <span data-ttu-id="60627-113">但是，在使用此方法时，可以将 IIS 配置为允许非管理员用户执行部署。</span><span class="sxs-lookup"><span data-stu-id="60627-113">However, when you use this approach, you can configure IIS to allow non-administrator users to perform the deployment.</span></span> <span data-ttu-id="60627-114">Web 部署处理程序仅在 IIS 版本7或更高版本中可用。</span><span class="sxs-lookup"><span data-stu-id="60627-114">The Web Deploy Handler is only available in IIS version 7 or later.</span></span>
> - <span data-ttu-id="60627-115">使用 *脱机部署*。</span><span class="sxs-lookup"><span data-stu-id="60627-115">Use *offline deployment*.</span></span> <span data-ttu-id="60627-116">此方法需要最少的 web 服务器配置，但服务器管理员必须手动将 web 包复制到服务器上，并通过 IIS 管理器将其导入。</span><span class="sxs-lookup"><span data-stu-id="60627-116">This approach requires the least configuration of the web server, but a server administrator must manually copy the web package onto the server and import it through IIS Manager.</span></span>
> 
> <span data-ttu-id="60627-117">有关这些方法的主要功能、优点和缺点的详细信息，请参阅 [选择正确的 Web 部署方法](choosing-the-right-approach-to-web-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="60627-117">For more information on the key features, advantages, and disadvantages of these approaches, see [Choosing the Right Approach to Web Deployment](choosing-the-right-approach-to-web-deployment.md).</span></span>

## <a name="is-the-web-deploy-remote-agent-the-right-approach-for-you"></a><span data-ttu-id="60627-118">Web 部署远程代理是否适合你？</span><span class="sxs-lookup"><span data-stu-id="60627-118">Is the Web Deploy Remote Agent the Right Approach for You?</span></span>

<span data-ttu-id="60627-119">是的，如果要部署内容的用户可以在目标服务器上提供管理员凭据。</span><span class="sxs-lookup"><span data-stu-id="60627-119">Yes, if the user who will deploy the content can supply the credentials of an administrator on the destination server.</span></span> <span data-ttu-id="60627-120">此方法在以下类型的方案中通常是必需的：</span><span class="sxs-lookup"><span data-stu-id="60627-120">This approach is often desirable in these types of scenarios:</span></span>

- <span data-ttu-id="60627-121">开发或测试环境，开发人员可以完全控制目标 web 服务器和数据库服务器。</span><span class="sxs-lookup"><span data-stu-id="60627-121">Development or test environments, where the developer has full control over the destination web server and database server.</span></span>
- <span data-ttu-id="60627-122">小型组织，其中单个用户或一小组用户可以控制整个应用程序生命周期。</span><span class="sxs-lookup"><span data-stu-id="60627-122">Smaller organizations in which a single user or a small group of users has control over the entire application lifecycle.</span></span>

<span data-ttu-id="60627-123">在许多大型组织中，特别是在过渡环境或生产环境中，向用户授予对 web 服务器的管理员权限通常是不现实的。</span><span class="sxs-lookup"><span data-stu-id="60627-123">In lots of larger organizations, and particularly for staging or production environments, it's often not realistic to give users administrator rights on web servers.</span></span> <span data-ttu-id="60627-124">对于托管的 web 服务器，这种情况尤其不可能出现。</span><span class="sxs-lookup"><span data-stu-id="60627-124">In the case of hosted web servers, this is especially unlikely to be the case.</span></span> <span data-ttu-id="60627-125">此外，如果计划从生成服务器自动进行部署，则可能不希望使用管理员凭据来完成部署过程。</span><span class="sxs-lookup"><span data-stu-id="60627-125">In addition, if you're planning to automate deployment from a build server, you may not want to use administrator credentials for the deployment process.</span></span> <span data-ttu-id="60627-126">在这些情况下，将 web 服务器配置为支持使用 [Web 部署处理程序](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md) 的部署可能会提供更好的选择。</span><span class="sxs-lookup"><span data-stu-id="60627-126">In these scenarios, configuring your web servers to support deployment using the [Web Deploy Handler](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md) may provide a more satisfactory choice.</span></span>

## <a name="task-overview"></a><span data-ttu-id="60627-127">任务概述</span><span class="sxs-lookup"><span data-stu-id="60627-127">Task Overview</span></span>

<span data-ttu-id="60627-128">本主题介绍如何配置 Internet Information Services (IIS) 7.5 web 服务器使用 Web 部署远程代理方法从远程计算机接受和部署 web 包。</span><span class="sxs-lookup"><span data-stu-id="60627-128">This topic describes how to configure an Internet Information Services (IIS) 7.5 web server to accept and deploy web packages from a remote computer using the Web Deploy Remote Agent approach.</span></span> <span data-ttu-id="60627-129">你需要：</span><span class="sxs-lookup"><span data-stu-id="60627-129">You'll need to:</span></span>

- <span data-ttu-id="60627-130">安装 IIS 7.5 和 IIS 7 建议的配置。</span><span class="sxs-lookup"><span data-stu-id="60627-130">Install IIS 7.5 and the IIS 7 recommended configuration.</span></span>
- <span data-ttu-id="60627-131">安装 Web 部署2.1 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="60627-131">Install Web Deploy 2.1 or later.</span></span>
- <span data-ttu-id="60627-132">创建一个 IIS 网站来托管已部署的内容。</span><span class="sxs-lookup"><span data-stu-id="60627-132">Create an IIS website to host the deployed content.</span></span>
- <span data-ttu-id="60627-133">确保 Web 部署代理服务正在运行。</span><span class="sxs-lookup"><span data-stu-id="60627-133">Ensure that the Web Deployment Agent Service is running.</span></span>

<span data-ttu-id="60627-134">若要专门托管示例解决方案，还需要：</span><span class="sxs-lookup"><span data-stu-id="60627-134">To host the sample solution specifically, you'll also need to:</span></span>

- <span data-ttu-id="60627-135">安装 .NET Framework 4.0。</span><span class="sxs-lookup"><span data-stu-id="60627-135">Install the .NET Framework 4.0.</span></span>
- <span data-ttu-id="60627-136">安装 ASP.NET MVC 3。</span><span class="sxs-lookup"><span data-stu-id="60627-136">Install ASP.NET MVC 3.</span></span>

<span data-ttu-id="60627-137">本主题将演示如何执行上述每个过程。</span><span class="sxs-lookup"><span data-stu-id="60627-137">This topic will show you how to perform each of these procedures.</span></span> <span data-ttu-id="60627-138">本主题中的任务和演练假设你开始使用运行 Windows Server 2008 R2 的干净服务器版本。</span><span class="sxs-lookup"><span data-stu-id="60627-138">The tasks and walkthroughs in this topic assume that you're starting with a clean server build running Windows Server 2008 R2.</span></span> <span data-ttu-id="60627-139">继续之前，请确保：</span><span class="sxs-lookup"><span data-stu-id="60627-139">Before you continue, ensure that:</span></span>

- <span data-ttu-id="60627-140">Windows Server 2008 R2 Service Pack 1 和所有可用更新均已安装。</span><span class="sxs-lookup"><span data-stu-id="60627-140">Windows Server 2008 R2 Service Pack 1 and all available updates are installed.</span></span>
- <span data-ttu-id="60627-141">服务器已加入域。</span><span class="sxs-lookup"><span data-stu-id="60627-141">The server is domain-joined.</span></span>
- <span data-ttu-id="60627-142">服务器具有静态 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="60627-142">The server has a static IP address.</span></span>

> [!NOTE]
> <span data-ttu-id="60627-143">有关将计算机加入域的详细信息，请参阅将 [计算机加入到域并登录](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx)。</span><span class="sxs-lookup"><span data-stu-id="60627-143">For more information on joining computers to a domain, see [Joining Computers to the Domain and Logging On](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx).</span></span> <span data-ttu-id="60627-144">有关配置静态 IP 地址的详细信息，请参阅 [配置静态 Ip 地址](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx)。</span><span class="sxs-lookup"><span data-stu-id="60627-144">For more information on configuring static IP addresses, see [Configure a Static IP Address](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx).</span></span> <span data-ttu-id="60627-145">远程代理服务支持 IIS 6，无需加入到域。</span><span class="sxs-lookup"><span data-stu-id="60627-145">The Remote Agent service is supported by IIS 6 onwards and does not require you to be joined to a domain.</span></span> <span data-ttu-id="60627-146">不过，本教程中的步骤是在 IIS 7.5 上进行开发和测试的，其他版本的过程可能会有所不同。</span><span class="sxs-lookup"><span data-stu-id="60627-146">However, the steps in this tutorial were developed and tested on IIS 7.5 and procedures for other versions may vary.</span></span>

## <a name="install-products-and-components"></a><span data-ttu-id="60627-147">安装产品和组件</span><span class="sxs-lookup"><span data-stu-id="60627-147">Install Products and Components</span></span>

<span data-ttu-id="60627-148">本部分将指导你完成在 web 服务器上安装所需的产品和组件。</span><span class="sxs-lookup"><span data-stu-id="60627-148">This section will guide you through installing the required products and components on the web server.</span></span> <span data-ttu-id="60627-149">在开始之前，好的做法是运行 Windows 更新以确保服务器完全处于最新状态。</span><span class="sxs-lookup"><span data-stu-id="60627-149">Before you begin, a good practice is to run Windows Update to ensure that your server is fully up to date.</span></span>

<span data-ttu-id="60627-150">在这种情况下，需要安装以下内容：</span><span class="sxs-lookup"><span data-stu-id="60627-150">In this case, you need to install these things:</span></span>

- <span data-ttu-id="60627-151">**IIS 7 建议的配置**。</span><span class="sxs-lookup"><span data-stu-id="60627-151">**IIS 7 Recommended Configuration**.</span></span> <span data-ttu-id="60627-152">这会使 **Web 服务器 (** web 服务器上的 iis) 角色，并安装承载 ASP.NET 应用程序所需的一组 iis 模块和组件。</span><span class="sxs-lookup"><span data-stu-id="60627-152">This enables the **Web Server (IIS)** role on your web server and installs the set of IIS modules and components that you need in order to host an ASP.NET application.</span></span>
- <span data-ttu-id="60627-153">**.NET Framework 4.0**。</span><span class="sxs-lookup"><span data-stu-id="60627-153">**.NET Framework 4.0**.</span></span> <span data-ttu-id="60627-154">这是运行在此版本的 .NET Framework 上构建的应用程序所必需的。</span><span class="sxs-lookup"><span data-stu-id="60627-154">This is required to run applications that were built on this version of the .NET Framework.</span></span>
- <span data-ttu-id="60627-155">**Web 部署工具2.1 或更高版本**。</span><span class="sxs-lookup"><span data-stu-id="60627-155">**Web Deployment Tool 2.1 or later**.</span></span> <span data-ttu-id="60627-156">这会在服务器上安装 Web 部署 (及其基础可执行文件 MSDeploy.exe) 。</span><span class="sxs-lookup"><span data-stu-id="60627-156">This installs Web Deploy (and its underlying executable, MSDeploy.exe) on your server.</span></span> <span data-ttu-id="60627-157">在此过程中，它将安装并启动 Web 部署代理服务。</span><span class="sxs-lookup"><span data-stu-id="60627-157">As part of this process, it installs and starts the Web Deployment Agent Service.</span></span> <span data-ttu-id="60627-158">此服务允许你从远程计算机部署 web 包。</span><span class="sxs-lookup"><span data-stu-id="60627-158">This service lets you deploy web packages from a remote computer.</span></span>
- <span data-ttu-id="60627-159">**ASP.NET MVC 3**。</span><span class="sxs-lookup"><span data-stu-id="60627-159">**ASP.NET MVC 3**.</span></span> <span data-ttu-id="60627-160">这将安装运行 MVC 3 应用程序所需的程序集。</span><span class="sxs-lookup"><span data-stu-id="60627-160">This installs the assemblies you need to run MVC 3 applications.</span></span>

> [!NOTE]
> <span data-ttu-id="60627-161">本演练介绍了如何使用 Web 平台安装程序来安装和配置所需的组件。</span><span class="sxs-lookup"><span data-stu-id="60627-161">This walkthrough describes the use of the Web Platform Installer to install and configure the required components.</span></span> <span data-ttu-id="60627-162">尽管无需使用 Web 平台安装程序，但它可以通过自动检测依赖项并确保始终获取最新的产品版本来简化安装过程。</span><span class="sxs-lookup"><span data-stu-id="60627-162">Although you don't have to use the Web Platform Installer, it simplifies the installation process by automatically detecting dependencies and ensuring that you always get the latest product versions.</span></span> <span data-ttu-id="60627-163">有关详细信息，请参阅 [Microsoft Web 平台安装程序 3.0](https://go.microsoft.com/?linkid=9805118)。</span><span class="sxs-lookup"><span data-stu-id="60627-163">For more information, see [Microsoft Web Platform Installer 3.0](https://go.microsoft.com/?linkid=9805118).</span></span>

<span data-ttu-id="60627-164">**安装所需的产品和组件**</span><span class="sxs-lookup"><span data-stu-id="60627-164">**To install the required products and components**</span></span>

1. <span data-ttu-id="60627-165">下载并安装 [Web 平台安装程序](https://go.microsoft.com/?linkid=9805118)。</span><span class="sxs-lookup"><span data-stu-id="60627-165">Download and install the [Web Platform Installer](https://go.microsoft.com/?linkid=9805118).</span></span>
2. <span data-ttu-id="60627-166">安装完成后，Web 平台安装程序将自动启动。</span><span class="sxs-lookup"><span data-stu-id="60627-166">When installation is complete, the Web Platform Installer will launch automatically.</span></span>

    > [!NOTE]
    > <span data-ttu-id="60627-167">你现在可以从 " **开始** " 菜单启动 Web 平台安装程序。</span><span class="sxs-lookup"><span data-stu-id="60627-167">You can now launch the Web Platform Installer at any time from the **Start** menu.</span></span> <span data-ttu-id="60627-168">为此，请在 " **开始** " 菜单上，单击 " **所有程序**"，然后单击 " **Microsoft Web 平台安装程序**"。</span><span class="sxs-lookup"><span data-stu-id="60627-168">To do this, on the **Start** menu, click **All Programs**, and then click **Microsoft Web Platform Installer**.</span></span>
3. <span data-ttu-id="60627-169">在 **Web 平台安装程序 3.0** 窗口的顶部，单击 " **产品**"。</span><span class="sxs-lookup"><span data-stu-id="60627-169">At the top of the **Web Platform Installer 3.0** window, click **Products**.</span></span>
4. <span data-ttu-id="60627-170">在窗口左侧的导航窗格中，单击 " **框架**"。</span><span class="sxs-lookup"><span data-stu-id="60627-170">On the left side of the window, in the navigation pane, click **Frameworks**.</span></span>
5. <span data-ttu-id="60627-171">在 **Microsoft .NET Framework 4** "行中，如果尚未安装 .NET Framework，请单击" **添加**"。</span><span class="sxs-lookup"><span data-stu-id="60627-171">In the **Microsoft .NET Framework 4** row, if the .NET Framework is not already installed, click **Add**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="60627-172">可能已通过 Windows 更新安装 .NET Framework 4.0。</span><span class="sxs-lookup"><span data-stu-id="60627-172">You may have already installed the .NET Framework 4.0 through Windows Update.</span></span> <span data-ttu-id="60627-173">如果产品或组件已安装，Web 平台安装程序将通过将 " **添加** " 按钮替换为 **安装**的文本来指示这一点。</span><span class="sxs-lookup"><span data-stu-id="60627-173">If a product or component is already installed, the Web Platform Installer will indicate this by replacing the **Add** button with the text **Installed**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image1.png)
6. <span data-ttu-id="60627-174">在 \*\*ASP.NET MVC 3 (Visual Studio 2010) \*\* 行中，单击 " **添加**"。</span><span class="sxs-lookup"><span data-stu-id="60627-174">In the **ASP.NET MVC 3 (Visual Studio 2010)** row, click **Add**.</span></span>
7. <span data-ttu-id="60627-175">在导航窗格中，单击 " **服务器**"。</span><span class="sxs-lookup"><span data-stu-id="60627-175">In the navigation pane, click **Server**.</span></span>
8. <span data-ttu-id="60627-176">在 " **IIS 7 推荐的配置** " 行中，单击 " **添加**"。</span><span class="sxs-lookup"><span data-stu-id="60627-176">In the **IIS 7 Recommended Configuration** row, click **Add**.</span></span>
9. <span data-ttu-id="60627-177">在 **Web 部署工具 2.1** 行中，单击 " **添加**"。</span><span class="sxs-lookup"><span data-stu-id="60627-177">In the **Web Deployment Tool 2.1** row, click **Add**.</span></span>
10. <span data-ttu-id="60627-178">单击“安装” 。</span><span class="sxs-lookup"><span data-stu-id="60627-178">Click **Install**.</span></span> <span data-ttu-id="60627-179">Web 平台安装程序将向你显示一个产品列表，其中包含要安装的任何关联依赖项&#x2014;&#x2014;，并将提示你接受许可条款。</span><span class="sxs-lookup"><span data-stu-id="60627-179">The Web Platform Installer will show you a list of products&#x2014;together with any associated dependencies&#x2014;to be installed and will prompt you to accept the license terms.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image2.png)
11. <span data-ttu-id="60627-180">查看许可条款，如果同意条款，请单击 " **我接受**"。</span><span class="sxs-lookup"><span data-stu-id="60627-180">Review the license terms, and if you consent to the terms, click **I Accept**.</span></span>
12. <span data-ttu-id="60627-181">安装完成后，单击 " **完成**"，然后关闭 " **Web 平台安装程序 3.0** " 窗口。</span><span class="sxs-lookup"><span data-stu-id="60627-181">When the installation is complete, click **Finish**, and then close the **Web Platform Installer 3.0** window.</span></span>

<span data-ttu-id="60627-182">如果在安装 IIS 之前安装了 .NET Framework 4.0，则需要运行 [ASP.NET Iis 注册工具](https://msdn.microsoft.com/library/k6h9cz8h(v=VS.100).aspx) (aspnet \_regiis.exe) 向 IIS 注册 ASP.NET 的最新版本。</span><span class="sxs-lookup"><span data-stu-id="60627-182">If you installed the .NET Framework 4.0 before you installed IIS, you'll need to run the [ASP.NET IIS Registration Tool](https://msdn.microsoft.com/library/k6h9cz8h(v=VS.100).aspx) (aspnet\_regiis.exe) to register the latest version of ASP.NET with IIS.</span></span> <span data-ttu-id="60627-183">如果不这样做，你会发现，IIS 将 (的静态内容提供) HTML 文件，但不会有任何问题，但在你尝试浏览到 ASP.NET 内容时，它将返回 **HTTP 错误404.0 –找不** 到。</span><span class="sxs-lookup"><span data-stu-id="60627-183">If you don't do this, you'll find that IIS will serve static content (like HTML files) without any problems, but it will return **HTTP Error 404.0 – Not Found** when you attempt to browse to ASP.NET content.</span></span> <span data-ttu-id="60627-184">您可以使用此过程来确保 ASP.NET 4.0 已注册。</span><span class="sxs-lookup"><span data-stu-id="60627-184">You can use this procedure to ensure that ASP.NET 4.0 is registered.</span></span>

<span data-ttu-id="60627-185">**向 IIS 注册 ASP.NET 4。0**</span><span class="sxs-lookup"><span data-stu-id="60627-185">**To register ASP.NET 4.0 with IIS**</span></span>

1. <span data-ttu-id="60627-186">单击 " **开始**"，然后键入 **命令提示符**。</span><span class="sxs-lookup"><span data-stu-id="60627-186">Click **Start**, and then type **Command Prompt**.</span></span>
2. <span data-ttu-id="60627-187">在搜索结果中，右键单击 " **命令提示符**"，然后单击 " **以管理员身份运行**"。</span><span class="sxs-lookup"><span data-stu-id="60627-187">In the search results, right-click **Command Prompt**, and then click **Run as administrator**.</span></span>
3. <span data-ttu-id="60627-188">在命令提示符窗口中，导航到 " **%windir%\microsoft.net\framework\v4.0.30319 (对于** " 目录。</span><span class="sxs-lookup"><span data-stu-id="60627-188">In the Command Prompt window, navigate to the **%WINDIR%\Microsoft.NET\Framework\v4.0.30319** directory.</span></span>
4. <span data-ttu-id="60627-189">键入以下命令，然后按 Enter：</span><span class="sxs-lookup"><span data-stu-id="60627-189">Type this command, and then press Enter:</span></span>

    [!code-console[Main](configuring-a-web-server-for-web-deploy-publishing-remote-agent/samples/sample1.cmd)]
5. <span data-ttu-id="60627-190">如果你打算随时托管64位 web 应用程序，则还应将 ASP.NET 的64位版本注册到 IIS。</span><span class="sxs-lookup"><span data-stu-id="60627-190">If you plan to host 64-bit web applications at any point, you should also register the 64-bit version of ASP.NET with IIS.</span></span> <span data-ttu-id="60627-191">为此，请在命令提示符窗口中导航到 **%windir%\microsoft.net\framework64\v4.0.30319 (对于** 目录。</span><span class="sxs-lookup"><span data-stu-id="60627-191">To do this, in the Command Prompt window, navigate to the **%WINDIR%\Microsoft.NET\Framework64\v4.0.30319** directory.</span></span>
6. <span data-ttu-id="60627-192">键入以下命令，然后按 Enter：</span><span class="sxs-lookup"><span data-stu-id="60627-192">Type this command, and then press Enter:</span></span>

    [!code-console[Main](configuring-a-web-server-for-web-deploy-publishing-remote-agent/samples/sample2.cmd)]

<span data-ttu-id="60627-193">作为一种很好的做法，请再次使用 Windows 更新，下载并安装适用于已安装的新产品和组件的任何可用更新。</span><span class="sxs-lookup"><span data-stu-id="60627-193">As a good practice, use Windows Update again at this point to download and install any available updates for the new products and components you've installed.</span></span>

## <a name="configure-the-iis-website"></a><span data-ttu-id="60627-194">配置 IIS 网站</span><span class="sxs-lookup"><span data-stu-id="60627-194">Configure the IIS Website</span></span>

<span data-ttu-id="60627-195">你需要创建并配置一个 IIS 网站来托管内容，然后才能将 web 内容部署到你的服务器。</span><span class="sxs-lookup"><span data-stu-id="60627-195">Before you can deploy web content to your server, you need to create and configure an IIS website to host the content.</span></span> <span data-ttu-id="60627-196">Web 部署只能将 web 包部署到现有 IIS 网站;它无法为你创建网站。</span><span class="sxs-lookup"><span data-stu-id="60627-196">Web Deploy can only deploy web packages to an existing IIS website; it can't create the website for you.</span></span> <span data-ttu-id="60627-197">在高级别上，需要完成以下任务：</span><span class="sxs-lookup"><span data-stu-id="60627-197">At a high level, you'll need to complete these tasks:</span></span>

- <span data-ttu-id="60627-198">在文件系统上创建一个文件夹以托管你的内容。</span><span class="sxs-lookup"><span data-stu-id="60627-198">Create a folder on the file system to host your content.</span></span>
- <span data-ttu-id="60627-199">创建一个 IIS 网站来提供内容，并将其与本地文件夹关联。</span><span class="sxs-lookup"><span data-stu-id="60627-199">Create an IIS website to serve the content, and associate it with the local folder.</span></span>
- <span data-ttu-id="60627-200">向本地文件夹上的应用程序池标识授予读取权限。</span><span class="sxs-lookup"><span data-stu-id="60627-200">Grant read permissions to the application pool identity on the local folder.</span></span>

<span data-ttu-id="60627-201">尽管不会阻止你将内容部署到 IIS 中的默认网站，但对于除测试或演示方案之外的任何内容，不建议使用此方法。</span><span class="sxs-lookup"><span data-stu-id="60627-201">Although there's nothing stopping you from deploying content to the default website in IIS, this approach is not recommended for anything other than test or demonstration scenarios.</span></span> <span data-ttu-id="60627-202">若要模拟生产环境，应该创建一个新的 IIS 网站，其中包含特定于应用程序要求的设置。</span><span class="sxs-lookup"><span data-stu-id="60627-202">To simulate a production environment, you should create a new IIS website with settings that are specific to the requirements of your application.</span></span>

<span data-ttu-id="60627-203">**创建和配置 IIS 网站**</span><span class="sxs-lookup"><span data-stu-id="60627-203">**To create and configure an IIS website**</span></span>

1. <span data-ttu-id="60627-204">在本地文件系统上，创建一个文件夹以存储内容 (例如 **C:\DemoSite**) 。</span><span class="sxs-lookup"><span data-stu-id="60627-204">On the local file system, create a folder to store your content (for example, **C:\DemoSite**).</span></span>
2. <span data-ttu-id="60627-205">在 " **开始** " 菜单上，指向 " **管理工具**"，然后单击 " **Internet Information Services (IIS) 管理器**"。</span><span class="sxs-lookup"><span data-stu-id="60627-205">On the **Start** menu, point to **Administrative Tools**, and then click **Internet Information Services (IIS) Manager**.</span></span>
3. <span data-ttu-id="60627-206">在 IIS 管理器的 " **连接** " 窗格中，展开 "服务器" 节点 (例如 **TESTWEB1**) 。</span><span class="sxs-lookup"><span data-stu-id="60627-206">In IIS Manager, in the **Connections** pane, expand the server node (for example, **TESTWEB1**).</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image3.png)
4. <span data-ttu-id="60627-207">右键单击 " **站点** " 节点，然后单击 " **添加网站**"。</span><span class="sxs-lookup"><span data-stu-id="60627-207">Right-click the **Sites** node, and then click **Add Web Site**.</span></span>
5. <span data-ttu-id="60627-208">在 " **站点名称** " 框中，键入 IIS 网站的名称 (例如， **DemoSite**) 。</span><span class="sxs-lookup"><span data-stu-id="60627-208">In the **Site name** box, type a name for the IIS website (for example, **DemoSite**).</span></span>
6. <span data-ttu-id="60627-209">在 " **物理路径** " 框中，键入 (或浏览) 本地文件夹 (路径，例如 **C:\DemoSite**) 。</span><span class="sxs-lookup"><span data-stu-id="60627-209">In the **Physical path** box, type (or browse to) the path to your local folder (for example, **C:\DemoSite**).</span></span>
7. <span data-ttu-id="60627-210">在 " **端口** " 框中，键入要在其上托管网站 (的端口号，例如 **85**) 。</span><span class="sxs-lookup"><span data-stu-id="60627-210">In the **Port** box, type the port number on which you want to host the website (for example, **85**).</span></span>

    > [!NOTE]
    > <span data-ttu-id="60627-211">对于 HTTP，标准端口号为80，对于 HTTPS 则为443。</span><span class="sxs-lookup"><span data-stu-id="60627-211">The standard port numbers are 80 for HTTP and 443 for HTTPS.</span></span> <span data-ttu-id="60627-212">但是，如果你在端口80上托管此网站，你将需要停止默认网站，然后才能访问你的站点。</span><span class="sxs-lookup"><span data-stu-id="60627-212">However, if you host this website on port 80, you'll need to stop the default website before you can access your site.</span></span>
8. <span data-ttu-id="60627-213">将 " **主机名** " 框留空，除非要为网站配置域名系统 (DNS) 记录，然后单击 **"确定"**。</span><span class="sxs-lookup"><span data-stu-id="60627-213">Leave the **Host name** box blank, unless you want to configure a Domain Name System (DNS) record for the website, and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image4.png)

    > [!NOTE]
    > <span data-ttu-id="60627-214">在生产环境中，你可能想要在端口80上托管你的网站，并配置主机标头和匹配的 DNS 记录。</span><span class="sxs-lookup"><span data-stu-id="60627-214">In a production environment, you'll likely want to host your website on port 80 and configure a host header, together with matching DNS records.</span></span> <span data-ttu-id="60627-215">有关在 IIS 7 中配置主机标头的详细信息，请参阅 [配置网站的主机标头 (IIS 7) ](https://technet.microsoft.com/library/cc753195(WS.10).aspx)。</span><span class="sxs-lookup"><span data-stu-id="60627-215">For more information on configuring host headers in IIS 7, see [Configure a Host Header for a Web Site (IIS 7)](https://technet.microsoft.com/library/cc753195(WS.10).aspx).</span></span> <span data-ttu-id="60627-216">有关 Windows Server 2008 R2 中的 DNS 服务器角色的详细信息，请参阅 [Dns 服务器概述](https://technet.microsoft.com/library/cc770392.aspx) 和 [dns 服务器](https://technet.microsoft.com/windowsserver/dd448607)。</span><span class="sxs-lookup"><span data-stu-id="60627-216">For more information on the DNS Server role in Windows Server 2008 R2, see [DNS Server Overview](https://technet.microsoft.com/library/cc770392.aspx) and [DNS Server](https://technet.microsoft.com/windowsserver/dd448607).</span></span>
9. <span data-ttu-id="60627-217">在“操作” \*\*\*\* 窗格中的“编辑站点” \*\*\*\* 之下，单击“绑定” \*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="60627-217">In the **Actions** pane, under **Edit Site**, click **Bindings**.</span></span>
10. <span data-ttu-id="60627-218">在“网站绑定”\*\*\*\* 对话框中，单击“添加”\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="60627-218">In the **Site Bindings** dialog box, click **Add**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image5.png)
11. <span data-ttu-id="60627-219">在 " **添加站点绑定** " 对话框中，将 " **IP 地址** " 和 " **端口** " 设置为与现有站点配置匹配。</span><span class="sxs-lookup"><span data-stu-id="60627-219">In the **Add Site Binding** dialog box, set the **IP address** and **Port** to match your existing site configuration.</span></span>
12. <span data-ttu-id="60627-220">在 " **主机名** " 框中，键入 web 服务器的名称 (例如 **TESTWEB1**) ，然后单击 **"确定"**。</span><span class="sxs-lookup"><span data-stu-id="60627-220">In the **Host name** box, type the name of your web server (for example, **TESTWEB1**), and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image6.png)

    > [!NOTE]
    > <span data-ttu-id="60627-221">第一个站点绑定允许使用 IP 地址和端口或在本地访问站点 `http://localhost:85` 。</span><span class="sxs-lookup"><span data-stu-id="60627-221">The first site binding allows you to access the site locally using the IP address and port or `http://localhost:85`.</span></span> <span data-ttu-id="60627-222">第二个站点绑定允许使用计算机名称从域中的其他计算机访问站点 (例如， http://testweb1:85) 。</span><span class="sxs-lookup"><span data-stu-id="60627-222">The second site binding allows you to access the site from other computers on the domain using the machine name (for example, http://testweb1:85).</span></span>
13. <span data-ttu-id="60627-223">在 **“网站绑定”** 对话框中，单击 **“关闭”**。</span><span class="sxs-lookup"><span data-stu-id="60627-223">In the **Site Bindings** dialog box, click **Close**.</span></span>
14. <span data-ttu-id="60627-224">在“连接”\*\*\*\* 窗格中，单击“应用程序池”\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="60627-224">In the **Connections** pane, click **Application Pools**.</span></span>
15. <span data-ttu-id="60627-225">在 " **应用程序池** " 窗格中，右键单击应用程序池的名称，然后单击 " **基本设置**"。</span><span class="sxs-lookup"><span data-stu-id="60627-225">In the **Application Pools** pane, right-click the name of your application pool, and then click **Basic Settings**.</span></span> <span data-ttu-id="60627-226">默认情况下，应用程序池的名称将与网站的名称相匹配 (例如 **DemoSite**) 。</span><span class="sxs-lookup"><span data-stu-id="60627-226">By default, the name of your application pool will match the name of your website (for example, **DemoSite**).</span></span>
16. <span data-ttu-id="60627-227">在 **.NET Framework 版本** "列表中，选择" **.NET Framework v 4.0.30319**"，然后单击 **" 确定 "**。</span><span class="sxs-lookup"><span data-stu-id="60627-227">In the **.NET Framework version** list, select **.NET Framework v4.0.30319**, and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image7.png)

    > [!NOTE]
    > <span data-ttu-id="60627-228">示例解决方案需要 .NET Framework 4.0。</span><span class="sxs-lookup"><span data-stu-id="60627-228">The sample solution requires .NET Framework 4.0.</span></span> <span data-ttu-id="60627-229">这并不是对 Web 部署一般的要求。</span><span class="sxs-lookup"><span data-stu-id="60627-229">This is not a requirement for Web Deploy in general.</span></span>

<span data-ttu-id="60627-230">为了使你的网站提供内容，应用程序池标识必须对存储内容的本地文件夹具有读取权限。</span><span class="sxs-lookup"><span data-stu-id="60627-230">In order for your website to serve content, the application pool identity must have read permissions on the local folder that stores the content.</span></span> <span data-ttu-id="60627-231">在 IIS 7.5 中，应用程序池默认情况下使用唯一的应用程序池标识运行，与以前版本的 IIS 不同 (，应用程序池通常使用网络服务帐户) 运行。</span><span class="sxs-lookup"><span data-stu-id="60627-231">In IIS 7.5, application pools run with a unique application pool identity by default (in contrast to previous versions of IIS, where application pools would typically run using the Network Service account).</span></span> <span data-ttu-id="60627-232">应用程序池标识不是真实的用户帐户，并且不会显示在&#x2014;的任何用户或组列表中，而是在启动应用程序池时动态创建。</span><span class="sxs-lookup"><span data-stu-id="60627-232">The application pool identity is not a real user account and does not show up on any lists of users or groups&#x2014;instead, it's created dynamically when the application pool is started.</span></span> <span data-ttu-id="60627-233">每个应用程序池标识都作为隐藏项添加到本地 **IIS \_ iis-iusrs** 安全组。</span><span class="sxs-lookup"><span data-stu-id="60627-233">Each application pool identity is added to the local **IIS\_IUSRS** security group as a hidden item.</span></span>

<span data-ttu-id="60627-234">若要授予对文件或文件夹上的应用程序池标识的权限，可以使用两个选项：</span><span class="sxs-lookup"><span data-stu-id="60627-234">To grant permissions to an application pool identity on a file or folder, you have two options:</span></span>

- <span data-ttu-id="60627-235">使用 **Iis AppPool \[ 应用程序池名称** 格式将权限直接分配给应用程序池标识 (例如， **iis AppPool\DemoSite**) 。</span><span class="sxs-lookup"><span data-stu-id="60627-235">Assign permissions to the application pool identity directly, using the format **IIS AppPool\[application pool name]** (for example, **IIS AppPool\DemoSite**).</span></span>
- <span data-ttu-id="60627-236">将权限分配给 **IIS \_ iis-iusrs** 组。</span><span class="sxs-lookup"><span data-stu-id="60627-236">Assign permissions to the **IIS\_IUSRS** group.</span></span>

<span data-ttu-id="60627-237">最常见的方法是将权限分配给本地 **IIS \_ iis-iusrs** 组，因为此方法允许你在不重新配置文件系统权限的情况下更改应用程序池。</span><span class="sxs-lookup"><span data-stu-id="60627-237">The most common approach is to assign permissions to the local **IIS\_IUSRS** group because this approach lets you change application pools without reconfiguring file system permissions.</span></span> <span data-ttu-id="60627-238">下一过程使用此基于组的方法。</span><span class="sxs-lookup"><span data-stu-id="60627-238">The next procedure uses this group-based approach.</span></span>

> [!NOTE]
> <span data-ttu-id="60627-239">有关 IIS 7.5 中的应用程序池标识的详细信息，请参阅 [应用程序池标识](https://go.microsoft.com/?linkid=9805123)。</span><span class="sxs-lookup"><span data-stu-id="60627-239">For more information on application pool identities in IIS 7.5, see [Application Pool Identities](https://go.microsoft.com/?linkid=9805123).</span></span>

<span data-ttu-id="60627-240">**配置 IIS 网站的文件夹权限**</span><span class="sxs-lookup"><span data-stu-id="60627-240">**To configure folder permissions for an IIS website**</span></span>

1. <span data-ttu-id="60627-241">在 Windows 资源管理器中，浏览到本地文件夹的位置。</span><span class="sxs-lookup"><span data-stu-id="60627-241">In Windows Explorer, browse to the location of your local folder.</span></span>
2. <span data-ttu-id="60627-242">右键单击该文件夹，然后单击 **“属性”**。</span><span class="sxs-lookup"><span data-stu-id="60627-242">Right-click the folder, and then click **Properties**.</span></span>
3. <span data-ttu-id="60627-243">在“**Security**”选项卡上，依次单击“**Edit**”、“**Add**”。</span><span class="sxs-lookup"><span data-stu-id="60627-243">On the **Security** tab, click **Edit**, and then click **Add**.</span></span>
4. <span data-ttu-id="60627-244">单击“位置”。</span><span class="sxs-lookup"><span data-stu-id="60627-244">Click **Locations**.</span></span> <span data-ttu-id="60627-245">在 " **位置** " 对话框中，选择本地服务器，然后单击 **"确定"**。</span><span class="sxs-lookup"><span data-stu-id="60627-245">In the **Locations** dialog box, select the local server, and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image8.png)
5. <span data-ttu-id="60627-246">在 " **选择用户或组** " 对话框中，键入 **IIS \_ Iis-iusrs**，单击 " **检查名称**"，然后单击 **"确定"**。</span><span class="sxs-lookup"><span data-stu-id="60627-246">In the **Select Users or Groups** dialog box, type **IIS\_IUSRS**, click **Check Names**, and then click **OK**.</span></span>
6. <span data-ttu-id="60627-247">在 " \*\* (文件夹名称) 的权限" 对话框\*\*中，请注意，默认情况下已为新组分配 " **读取 & 执行**"、" **列出文件夹内容**" 和 " **读取** " 权限。</span><span class="sxs-lookup"><span data-stu-id="60627-247">In the **Permissions for (folder name) dialog box**, notice that the new group has been assigned the **Read & execute**, **List folder contents**, and **Read** permissions by default.</span></span> <span data-ttu-id="60627-248">保持不变，并单击 **"确定"**。</span><span class="sxs-lookup"><span data-stu-id="60627-248">Leave this unchanged and click **OK**.</span></span>
7. <span data-ttu-id="60627-249">单击 **"确定"** 以关闭 "属性" 对话框 \*\* (文件夹) 名称\*\* 。</span><span class="sxs-lookup"><span data-stu-id="60627-249">Click **OK** to close the **(folder name) Properties** dialog box.</span></span>

<span data-ttu-id="60627-250">作为最终任务，在尝试将任何 web 包部署到服务器之前，应确保 Web 部署代理服务正在运行。</span><span class="sxs-lookup"><span data-stu-id="60627-250">As a final task before you attempt to deploy any web packages to your server, you should ensure that the Web Deployment Agent Service is running.</span></span> <span data-ttu-id="60627-251">从远程计算机部署包时，Web 部署代理服务负责提取和安装包的内容。</span><span class="sxs-lookup"><span data-stu-id="60627-251">When you deploy a package from a remote computer, the Web Deployment Agent Service is responsible for extracting and installing the contents of the package.</span></span> <span data-ttu-id="60627-252">默认情况下，当你安装 Web 部署工具并在网络服务标识下运行时，将启动该服务。</span><span class="sxs-lookup"><span data-stu-id="60627-252">The service is started by default when you install the Web Deployment Tool and runs under the Network Service identity.</span></span>

<span data-ttu-id="60627-253">你可以使用各种命令行实用工具或 Windows PowerShell cmdlet 来检查服务是否以多种不同的方式运行。</span><span class="sxs-lookup"><span data-stu-id="60627-253">You can check whether a service is running in multiple different ways, using various command-line utilities or Windows PowerShell cmdlets.</span></span> <span data-ttu-id="60627-254">此过程描述了一个简单的基于 UI 的方法。</span><span class="sxs-lookup"><span data-stu-id="60627-254">This procedure describes a straightforward UI-based approach.</span></span>

<span data-ttu-id="60627-255">**检查 Web 部署代理服务是否正在运行**</span><span class="sxs-lookup"><span data-stu-id="60627-255">**To check that the Web Deployment Agent Service is running**</span></span>

1. <span data-ttu-id="60627-256">在“开始”  菜单上，指向“管理工具”  ，然后单击“服务”  。</span><span class="sxs-lookup"><span data-stu-id="60627-256">On the **Start** menu, point to **Administrative Tools**, and then click **Services**.</span></span>
2. <span data-ttu-id="60627-257">找到 " **Web 部署代理服务** " 行，然后验证 " **状态** " 是否设置为 " **已启动**"。</span><span class="sxs-lookup"><span data-stu-id="60627-257">Locate the **Web Deployment Agent Service** row, and verify that the **Status** is set to **Started**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image9.png)
3. <span data-ttu-id="60627-258">如果该服务尚未启动，则单击 " **启动**"。</span><span class="sxs-lookup"><span data-stu-id="60627-258">If the service is not already started, click **Start**.</span></span>

## <a name="configure-firewall-exceptions"></a><span data-ttu-id="60627-259">配置防火墙例外</span><span class="sxs-lookup"><span data-stu-id="60627-259">Configure Firewall Exceptions</span></span>

<span data-ttu-id="60627-260">默认情况下，远程代理服务在 TCP 端口80上侦听，网址为：</span><span class="sxs-lookup"><span data-stu-id="60627-260">By default, the Remote Agent Service listens on TCP port 80, at this URL:</span></span>

<http://servername.com/MSDEPLOYAGENTSERVICE>

<span data-ttu-id="60627-261">在大多数情况下，你无需为远程代理服务配置任何其他防火墙规则，因为 web 服务器通常在端口80上侦听 HTTP 请求。</span><span class="sxs-lookup"><span data-stu-id="60627-261">In most cases, you won't need to configure any additional firewall rules for the Remote Agent Service because web servers typically listen for HTTP requests on port 80.</span></span> <span data-ttu-id="60627-262">如果自定义安装以侦听非标准端口，则需要根据需要配置防火墙例外。</span><span class="sxs-lookup"><span data-stu-id="60627-262">If you customized your installation to listen on a nonstandard port, you'll need to configure firewall exceptions as required.</span></span>

## <a name="conclusion"></a><span data-ttu-id="60627-263">结论</span><span class="sxs-lookup"><span data-stu-id="60627-263">Conclusion</span></span>

<span data-ttu-id="60627-264">此时，web 服务器已准备好接受并安装远程计算机上的 web 包。</span><span class="sxs-lookup"><span data-stu-id="60627-264">At this point, your web server is ready to accept and install web packages from a remote computer.</span></span> <span data-ttu-id="60627-265">尝试将 web 应用程序部署到服务器之前，可能需要检查以下要点：</span><span class="sxs-lookup"><span data-stu-id="60627-265">Before you attempt to deploy a web application to the server, you may want to check these key points:</span></span>

- <span data-ttu-id="60627-266">是否已向 IIS 注册 ASP.NET 4.0？</span><span class="sxs-lookup"><span data-stu-id="60627-266">Have you registered ASP.NET 4.0 with IIS?</span></span>
- <span data-ttu-id="60627-267">应用程序池标识是否具有对你的网站的源文件夹的 "读取" 访问权限？</span><span class="sxs-lookup"><span data-stu-id="60627-267">Does the application pool identity have read access to the source folder for your website?</span></span>
- <span data-ttu-id="60627-268">Web 部署代理服务是否正在运行？</span><span class="sxs-lookup"><span data-stu-id="60627-268">Is the Web Deployment Agent Service running?</span></span>

## <a name="further-reading"></a><span data-ttu-id="60627-269">深入阅读</span><span class="sxs-lookup"><span data-stu-id="60627-269">Further Reading</span></span>

<span data-ttu-id="60627-270">有关如何配置自定义 Microsoft 生成引擎 (MSBuild) 项目文件以将 web 包部署到远程代理服务的指南，请参阅 [配置目标环境的部署属性](configuring-deployment-properties-for-a-target-environment.md)。</span><span class="sxs-lookup"><span data-stu-id="60627-270">For guidance on how to configure custom Microsoft Build Engine (MSBuild) project files to deploy web packages to the Remote Agent Service, see [Configuring Deployment Properties for a Target Environment](configuring-deployment-properties-for-a-target-environment.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="60627-271">[上一页](scenario-configuring-a-production-environment-for-web-deployment.md)
> [下一页](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)</span><span class="sxs-lookup"><span data-stu-id="60627-271">[Previous](scenario-configuring-a-production-environment-for-web-deployment.md)
[Next](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)</span></span>

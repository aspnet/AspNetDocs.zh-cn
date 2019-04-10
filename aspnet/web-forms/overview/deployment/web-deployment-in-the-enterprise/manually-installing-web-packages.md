---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/manually-installing-web-packages
title: 手动安装 Web 程序包 |Microsoft Docs
author: jrjlee
description: 本主题介绍如何手动导入 web 部署包到 Internet 信息服务 (IIS)。 主题构建和打包 Web 应用程序...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: f11d22a7-5d32-4ad0-8a9b-276460a61c06
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/manually-installing-web-packages
msc.type: authoredcontent
ms.openlocfilehash: 9d0e57eb85242a0d6fa8ca9eef7f6c741862069d
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/09/2019
ms.locfileid: "59408792"
---
# <a name="manually-installing-web-packages"></a><span data-ttu-id="93c91-104">手动安装 Web 程序包</span><span class="sxs-lookup"><span data-stu-id="93c91-104">Manually Installing Web Packages</span></span>

<span data-ttu-id="93c91-105">通过[Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="93c91-105">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="93c91-106">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="93c91-106">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="93c91-107">本主题介绍如何手动导入 web 部署包到 Internet 信息服务 (IIS)。</span><span class="sxs-lookup"><span data-stu-id="93c91-107">This topic describes how to manually import a web deployment package into Internet Information Services (IIS).</span></span>
> 
> <span data-ttu-id="93c91-108">本主题[构建和打包 Web 应用程序项目](building-and-packaging-web-application-projects.md)所述 IIS Web 部署工具 （Web 部署），与 Microsoft Build Engine (MSBuild) 和 Web 发布管道 (WPP) 结合使用，可以如何打包应用web 应用程序项目转换单个 zip 文件。</span><span class="sxs-lookup"><span data-stu-id="93c91-108">The topic [Building and Packaging Web Application Projects](building-and-packaging-web-application-projects.md) described how the IIS Web Deployment Tool (Web Deploy), in conjunction with the Microsoft Build Engine (MSBuild) and the Web Publishing Pipeline (WPP), lets you package your web application projects into a single zip file.</span></span> <span data-ttu-id="93c91-109">此文件中，通常称为 web 部署包 （或只需部署包），包含需要 IIS，以便重新创建 web 应用程序的 web 服务器上的所有内容和配置信息。</span><span class="sxs-lookup"><span data-stu-id="93c91-109">This file, commonly known as a web deployment package (or simply a deployment package), contains all the content and configuration information that IIS needs in order to re-create your web application on a web server.</span></span>
> 
> <span data-ttu-id="93c91-110">一旦你创建 web 部署包，可以将其发布到 IIS 服务器以各种方式。</span><span class="sxs-lookup"><span data-stu-id="93c91-110">Once you've created a web deployment package, you can publish it to an IIS server in various ways.</span></span> <span data-ttu-id="93c91-111">在很多情况下，你将想要充分利用 MSBuild、 WPP，和 Web 部署可以创建和自动或单步执行生成和部署过程的一部分的远程安装 web 程序包之间的集成点。</span><span class="sxs-lookup"><span data-stu-id="93c91-111">In a lot of scenarios, you'll want to take advantage of the integration points between MSBuild, the WPP, and Web Deploy to create and install web packages remotely as part of an automated or single-step build and deployment process.</span></span> <span data-ttu-id="93c91-112">此过程所述[部署 Web 包](deploying-web-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="93c91-112">This process is described in [Deploying Web Packages](deploying-web-packages.md).</span></span> <span data-ttu-id="93c91-113">但是，这并不总是可行。</span><span class="sxs-lookup"><span data-stu-id="93c91-113">However, this isn't always possible.</span></span> <span data-ttu-id="93c91-114">假设你想要部署 web 应用程序到面向 Internet 的生产环境。</span><span class="sxs-lookup"><span data-stu-id="93c91-114">Suppose you want to deploy a web application to an Internet-facing production environment.</span></span> <span data-ttu-id="93c91-115">出于安全原因，生产环境中此类是在非常最不可能是独立于生成服务器，在外围网络 （也称为 DMZ、 外围安全区域和外围子网） 中的子网防火墙后面。</span><span class="sxs-lookup"><span data-stu-id="93c91-115">For security reasons, such a production environment is at the very least likely to be behind a firewall on a subnet that is separate from the build server, in a perimeter network (also known as DMZ, demilitarized zone, and screened subnet).</span></span> <span data-ttu-id="93c91-116">在很多情况下，在生产环境将在单独的域或以物理方式隔离网络上。</span><span class="sxs-lookup"><span data-stu-id="93c91-116">In lots of cases, the production environment will be on a separate domain or on a physically isolated network.</span></span>
> 
> <span data-ttu-id="93c91-117">在这些情况下，唯一的选项可能是端口到目标服务器上的 web 包，并手动将其导入 IIS。</span><span class="sxs-lookup"><span data-stu-id="93c91-117">In these scenarios, your only option may be to port the web package onto the destination server and manually import it into IIS.</span></span> <span data-ttu-id="93c91-118">尽管这种方法可以阻止自动的部署，但它仍是一种 web 应用程序发布的高效方法&#x2014;只需将单个 zip 文件复制到你的 web 服务器并使用向导来引导您完成导入过程。</span><span class="sxs-lookup"><span data-stu-id="93c91-118">Although this approach precludes automated deployment, it's still a highly effective technique for publishing a web application&#x2014;you simply copy a single zip file to your web server and use a wizard to guide you through the import process.</span></span>


<span data-ttu-id="93c91-119">本主题窗体的一系列教程基于虚构公司 Fabrikam，Inc.的企业部署要求的一部分本系列教程将使用的示例解决方案&#x2014; [Contact Manager 解决方案](the-contact-manager-solution.md)&#x2014;来表示真实级别的复杂性，包括 ASP.NET MVC 3 应用程序，Windows 通信的 web 应用程序Foundation (WCF) 服务和数据库项目。</span><span class="sxs-lookup"><span data-stu-id="93c91-119">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

## <a name="task-overview"></a><span data-ttu-id="93c91-120">任务概述</span><span class="sxs-lookup"><span data-stu-id="93c91-120">Task Overview</span></span>

<span data-ttu-id="93c91-121">你将需要完成以下高级任务，以导入 IIS web 部署包：</span><span class="sxs-lookup"><span data-stu-id="93c91-121">You'll need to complete these high-level tasks to import a web deployment package into IIS:</span></span>

- <span data-ttu-id="93c91-122">创建使用 MSBuild 命令行、 Team Build 或 Visual Studio 2010 web 部署包。</span><span class="sxs-lookup"><span data-stu-id="93c91-122">Create a web deployment package using the MSBuild command line, Team Build, or Visual Studio 2010.</span></span>
- <span data-ttu-id="93c91-123">将 web 包复制到目标 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="93c91-123">Copy the web package to the destination web server.</span></span>
- <span data-ttu-id="93c91-124">使用导入应用程序包向导在 IIS 管理器安装的 web 包并为变量，如连接字符串和服务终结点提供的值。</span><span class="sxs-lookup"><span data-stu-id="93c91-124">Use the Import Application Package Wizard in IIS Manager to install the web package and provide values for variables like connection strings and service endpoints.</span></span>

<span data-ttu-id="93c91-125">本主题将演示如何执行这些过程。</span><span class="sxs-lookup"><span data-stu-id="93c91-125">This topic will show you how to perform these procedures.</span></span> <span data-ttu-id="93c91-126">任务和本主题中的演练假定您已经熟悉 web 包、 Web 部署和 WPP 背后的概念。</span><span class="sxs-lookup"><span data-stu-id="93c91-126">The tasks and walkthroughs in this topic assume that you're already familiar with the concepts behind web packages, Web Deploy, and the WPP.</span></span> <span data-ttu-id="93c91-127">有关详细信息，请参阅[构建和打包 Web 应用程序项目](building-and-packaging-web-application-projects.md)。</span><span class="sxs-lookup"><span data-stu-id="93c91-127">For more information, see [Building and Packaging Web Application Projects](building-and-packaging-web-application-projects.md).</span></span>

> [!NOTE]
> <span data-ttu-id="93c91-128">本主题最适合使用结合[Web 服务器配置用于 Web 部署发布 （脱机部署）](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)，其中解释了如何安装所需的组件，并为程序包导入准备的 IIS 网站。</span><span class="sxs-lookup"><span data-stu-id="93c91-128">This topic is best used in conjunction with [Configure a Web Server for Web Deploy Publishing (Offline Deployment)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md), which explains how to install the required components and prepare an IIS website for package import.</span></span>


## <a name="create-a-web-deployment-package"></a><span data-ttu-id="93c91-129">创建 Web 部署包</span><span class="sxs-lookup"><span data-stu-id="93c91-129">Create a Web Deployment Package</span></span>

<span data-ttu-id="93c91-130">第一个任务是创建你想要部署的 web 应用程序的 web 部署包。</span><span class="sxs-lookup"><span data-stu-id="93c91-130">The first task is to create a web deployment package for the web application project you want to deploy.</span></span> <span data-ttu-id="93c91-131">可以在不同的方式来创建 web 包。</span><span class="sxs-lookup"><span data-stu-id="93c91-131">You can create web packages in a variety of ways.</span></span>

**<span data-ttu-id="93c91-132">方法 1:使用 Visual Studio 创建生成过程的一部分的包</span><span class="sxs-lookup"><span data-stu-id="93c91-132">Approach 1: Create a package as part of the build process with Visual Studio</span></span>**

<span data-ttu-id="93c91-133">您可以将 web 应用程序项目配置为通过每次生成后创建 web 部署包**打包/发布 Web**项目属性页上的选项卡。</span><span class="sxs-lookup"><span data-stu-id="93c91-133">You can configure your web application project to create a web deployment package after every build through the **Package/Publish Web** tab on the project property pages.</span></span> <span data-ttu-id="93c91-134">此过程所述[构建和打包 Web 应用程序项目](building-and-packaging-web-application-projects.md)。</span><span class="sxs-lookup"><span data-stu-id="93c91-134">This process is described in [Building and Packaging Web Application Projects](building-and-packaging-web-application-projects.md).</span></span>

**<span data-ttu-id="93c91-135">方法 2:使用 MSBuild 创建生成过程的一部分的包</span><span class="sxs-lookup"><span data-stu-id="93c91-135">Approach 2: Create a package as part of the build process with MSBuild</span></span>**

<span data-ttu-id="93c91-136">如果您在 web 应用程序项目使用 MSBuild 生成直接通过自定义的 MSBuild 项目文件或从命令行中，您可以创建 web 部署包生成过程的一部分通过包括**DeployOnBuild = true**并**DeployTarget = 包**在命令中的属性。</span><span class="sxs-lookup"><span data-stu-id="93c91-136">If you build your web application project by using MSBuild directly, either through a custom MSBuild project file or from the command line, you can create a web deployment package as part of the build process by including the **DeployOnBuild=true** and **DeployTarget=Package** properties in your command.</span></span> <span data-ttu-id="93c91-137">此过程所述[了解构建过程](understanding-the-build-process.md)。</span><span class="sxs-lookup"><span data-stu-id="93c91-137">This process is described in [Understanding the Build Process](understanding-the-build-process.md).</span></span>

**<span data-ttu-id="93c91-138">方法 3:在 Visual Studio 中按需创建包</span><span class="sxs-lookup"><span data-stu-id="93c91-138">Approach 3: Create a package on demand in Visual Studio</span></span>**

<span data-ttu-id="93c91-139">可以随时在 Visual Studio 2010 中创建 web 应用程序项目的 web 部署包。</span><span class="sxs-lookup"><span data-stu-id="93c91-139">You can create a web deployment package for a web application project at any time in Visual Studio 2010.</span></span> <span data-ttu-id="93c91-140">若要执行此操作，在**解决方案资源管理器**窗口中，右键单击 web 应用程序项目，然后依次**生成部署包**。</span><span class="sxs-lookup"><span data-stu-id="93c91-140">To do this, in the **Solution Explorer** window, right-click your web application project, and then click **Build Deployment Package**.</span></span>

![](manually-installing-web-packages/_static/image1.png)

**<span data-ttu-id="93c91-141">方法 4:按需从命令行创建包</span><span class="sxs-lookup"><span data-stu-id="93c91-141">Approach 4: Create a package on demand from the command line</span></span>**

<span data-ttu-id="93c91-142">可以从命令行创建 web 部署包，通过调用**包**上 web 应用程序项目使用 MSBuild 目标。</span><span class="sxs-lookup"><span data-stu-id="93c91-142">You can create a web deployment package from the command line by invoking the **Package** target on your web application project using MSBuild.</span></span> <span data-ttu-id="93c91-143">该命令应类似如下：</span><span class="sxs-lookup"><span data-stu-id="93c91-143">The command should resemble this:</span></span>


[!code-console[Main](manually-installing-web-packages/samples/sample1.cmd)]


<span data-ttu-id="93c91-144">无论何种方法使用，最终结果相同。</span><span class="sxs-lookup"><span data-stu-id="93c91-144">Whichever approach you use, the end result is the same.</span></span> <span data-ttu-id="93c91-145">WPP 为 zip 文件，以及各种支持资源，你的 web 应用程序项目的输出文件夹中创建 web 部署包。</span><span class="sxs-lookup"><span data-stu-id="93c91-145">The WPP creates a web deployment package as a zip file, together with various supporting resources, in the output folder for your web application project.</span></span>

![](manually-installing-web-packages/_static/image2.png)

<span data-ttu-id="93c91-146">您计划手动导入 web 包，即是要求只有 zip 文件。</span><span class="sxs-lookup"><span data-stu-id="93c91-146">When you're planning to import the web package manually, you require only the zip file.</span></span> <span data-ttu-id="93c91-147">将此文件复制到目标 web 服务器，可以开始导入过程。</span><span class="sxs-lookup"><span data-stu-id="93c91-147">Copy this file to your target web server and you can begin the import process.</span></span>

## <a name="import-a-web-package-into-iis"></a><span data-ttu-id="93c91-148">将 Web 包导入 IIS</span><span class="sxs-lookup"><span data-stu-id="93c91-148">Import a Web Package into IIS</span></span>

<span data-ttu-id="93c91-149">下一步过程可用于从本地文件系统的 web 部署包导入 IIS 网站。</span><span class="sxs-lookup"><span data-stu-id="93c91-149">You can use the next procedure to import a web deployment package from the local file system into an IIS website.</span></span> <span data-ttu-id="93c91-150">执行此过程之前，请确保您有：</span><span class="sxs-lookup"><span data-stu-id="93c91-150">Before you perform this procedure, ensure that you have:</span></span>

- <span data-ttu-id="93c91-151">复制到 web 服务器的 web 部署包。</span><span class="sxs-lookup"><span data-stu-id="93c91-151">Copied the web deployment package to the web server.</span></span>
- <span data-ttu-id="93c91-152">配置 IIS web 服务器以承载应用程序。</span><span class="sxs-lookup"><span data-stu-id="93c91-152">Configured an IIS web server to host your application.</span></span>

<span data-ttu-id="93c91-153">有关配置 IIS web 服务器以支持 web 部署包的详细信息，请参阅[Web 服务器配置用于 Web 部署发布 （脱机部署）](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="93c91-153">For more information on configuring an IIS web server to support web deployment packages, see [Configure a Web Server for Web Deploy Publishing (Offline Deployment)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md).</span></span>

**<span data-ttu-id="93c91-154">若要导入使用 IIS 管理器的 web 部署包</span><span class="sxs-lookup"><span data-stu-id="93c91-154">To import a web deployment package using IIS Manager</span></span>**

1. <span data-ttu-id="93c91-155">在 IIS 管理器中，在**连接**窗格中，右键单击你的 IIS 网站，依次指向**部署**，然后单击**导入应用程序**。</span><span class="sxs-lookup"><span data-stu-id="93c91-155">In IIS Manager, in the **Connections** pane, right-click your IIS website, point to **Deploy**, and then click **Import Application**.</span></span>

    ![](manually-installing-web-packages/_static/image3.png)
2. <span data-ttu-id="93c91-156">在导入应用程序的包向导中，在**选择的包**页上，浏览到 web 部署包的位置，然后单击**下一步**。</span><span class="sxs-lookup"><span data-stu-id="93c91-156">In the Import Application Package Wizard, on the **Select the Package** page, browse to the location of your web deployment package, and then click **Next**.</span></span>
3. <span data-ttu-id="93c91-157">上**选择包的内容**页上，清除任何内容，您不需要，然后单击**下一步**。</span><span class="sxs-lookup"><span data-stu-id="93c91-157">On the **Select the Contents of the Package** page, clear any content that you don't require, and then click **Next**.</span></span>

    ![](manually-installing-web-packages/_static/image4.png)

    > [!NOTE]
    > <span data-ttu-id="93c91-158">在许多情况下，您可能不想要导入的所有操作与 web 部署包。</span><span class="sxs-lookup"><span data-stu-id="93c91-158">In a lot of cases, you may not want to import everything that comes with a web deployment package.</span></span> <span data-ttu-id="93c91-159">例如，可能不想要允许 Web 部署可以替换为关联的数据库。</span><span class="sxs-lookup"><span data-stu-id="93c91-159">For example, you may not want to allow Web Deploy to replace the associated database.</span></span>  
    > <span data-ttu-id="93c91-160">**授予的权限**条目设置目标文件系统，以确保应用程序池标识可以访问存储网站内容的物理文件夹的权限。</span><span class="sxs-lookup"><span data-stu-id="93c91-160">The **Grant permissions** entries set permissions on the destination file system to ensure that the application pool identity can access the physical folder that stores the website content.</span></span> <span data-ttu-id="93c91-161">此外，匿名身份验证用户授予读取到的文件夹的权限允许应用程序提供多用途 Internet 邮件扩展 (MIME) 类型的文件。</span><span class="sxs-lookup"><span data-stu-id="93c91-161">In addition, the anonymous authentication user is granted read permission to the folder to let the application serve Multipurpose Internet Mail Extensions (MIME) type files.</span></span> <span data-ttu-id="93c91-162">如果您愿意，可以删除这些条目，并手动配置的权限。</span><span class="sxs-lookup"><span data-stu-id="93c91-162">If you prefer, you can remove these entries and configure permissions manually.</span></span>
4. <span data-ttu-id="93c91-163">上**输入应用程序包信息**页上，提供所需的信息。</span><span class="sxs-lookup"><span data-stu-id="93c91-163">On the **Enter Application Package Information** page, provide the requested information.</span></span>

    ![](manually-installing-web-packages/_static/image5.png)
5. <span data-ttu-id="93c91-164">当创建 web 包时，WPP 分析你的应用程序的配置文件，并检测任何变量，如连接字符串和服务终结点。</span><span class="sxs-lookup"><span data-stu-id="93c91-164">When you create a web package, the WPP analyzes the configuration file for your application and detects any variables, like connection strings and service endpoints.</span></span> <span data-ttu-id="93c91-165">这种情况下：</span><span class="sxs-lookup"><span data-stu-id="93c91-165">In this case:</span></span>

    1. <span data-ttu-id="93c91-166">**应用程序路径**是你想要安装应用程序的 IIS 路径。</span><span class="sxs-lookup"><span data-stu-id="93c91-166">**Application Path** is the IIS path where you want to install your application.</span></span> <span data-ttu-id="93c91-167">此设置是通用的 WPP 创建的所有部署包。</span><span class="sxs-lookup"><span data-stu-id="93c91-167">This setting is common to all deployment packages that the WPP creates.</span></span>
    2. <span data-ttu-id="93c91-168">**ContactService 服务终结点地址**是应用程序应使用与已部署的 WCF 服务进行通信的地址。</span><span class="sxs-lookup"><span data-stu-id="93c91-168">**ContactService Service Endpoint Address** is the address that the application should use to communicate with the deployed WCF service.</span></span> <span data-ttu-id="93c91-169">此设置对应于中的条目*web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="93c91-169">This setting corresponds to an entry in the *web.config* file.</span></span>
    3. <span data-ttu-id="93c91-170">第一个**连接字符串**设置是 Web 部署应使用来部署应用程序 （在这种情况下 ASP.NET 成员资格数据库中） 与关联的数据库的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="93c91-170">The first **Connection String** setting is the connection string that Web Deploy should use to deploy the database associated with the application (in this case an ASP.NET membership database).</span></span> <span data-ttu-id="93c91-171">此设置对应于上的设置**打包/发布 SQL** Visual Studio 中的选项卡。</span><span class="sxs-lookup"><span data-stu-id="93c91-171">This setting corresponds to the setting on the **Package/Publish SQL** tab in Visual Studio.</span></span>
    4. <span data-ttu-id="93c91-172">第二个**连接字符串**设置是你的应用程序实际上将用于启动和运行时与数据库通信的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="93c91-172">The second **Connection String** setting is the connection string that your application will actually use to communicate with the database when it's up and running.</span></span> <span data-ttu-id="93c91-173">这对应于在一个连接字符串条目*web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="93c91-173">This corresponds to a connection string entry in the *web.config* file.</span></span>

        > [!NOTE]
        > <span data-ttu-id="93c91-174">有关这些参数是从哪里来的详细信息，请参阅[为 Web 程序包部署配置参数](configuring-parameters-for-web-package-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="93c91-174">For more information on where these parameters come from, see [Configuring Parameters for Web Package Deployment](configuring-parameters-for-web-package-deployment.md).</span></span>
6. <span data-ttu-id="93c91-175">单击 **“下一步”**。</span><span class="sxs-lookup"><span data-stu-id="93c91-175">Click **Next**.</span></span>
7. <span data-ttu-id="93c91-176">如果这不是已部署到此网站的应用程序第一次，将提示您指定是否要删除在安装之前的所有现有内容。</span><span class="sxs-lookup"><span data-stu-id="93c91-176">If this is not the first time you've deployed the application to this website, you'll be prompted to specify whether you want to delete all existing content prior to installation.</span></span> <span data-ttu-id="93c91-177">选择适合于您的需求，然后依次**下一步**。</span><span class="sxs-lookup"><span data-stu-id="93c91-177">Choose the option that's appropriate for your requirements, and then click **Next**.</span></span>

    ![](manually-installing-web-packages/_static/image6.png)
8. <span data-ttu-id="93c91-178">完成 IIS 已安装的包，请单击**完成**。</span><span class="sxs-lookup"><span data-stu-id="93c91-178">When IIS has finished installing the package, click **Finish**.</span></span>

    ![](manually-installing-web-packages/_static/image7.png)

<span data-ttu-id="93c91-179">此时，已成功发布到 IIS web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="93c91-179">At this point, you've successfully published your web application to IIS.</span></span>

## <a name="conclusion"></a><span data-ttu-id="93c91-180">结束语</span><span class="sxs-lookup"><span data-stu-id="93c91-180">Conclusion</span></span>

<span data-ttu-id="93c91-181">本主题介绍了如何将 web 部署包导入为使用 IIS 管理器中的 IIS 网站。</span><span class="sxs-lookup"><span data-stu-id="93c91-181">This topic described how to import a web deployment package into an IIS website using IIS Manager.</span></span> <span data-ttu-id="93c91-182">安全或基础结构限制使得远程部署，不可能或不需要时相应 web 应用程序发布到这种方法。</span><span class="sxs-lookup"><span data-stu-id="93c91-182">This approach to web application publishing is appropriate when security or infrastructure constraints make remote deployment impossible or undesirable.</span></span>

## <a name="further-reading"></a><span data-ttu-id="93c91-183">其他阅读材料</span><span class="sxs-lookup"><span data-stu-id="93c91-183">Further Reading</span></span>

<span data-ttu-id="93c91-184">有关如何配置 IIS web 服务器以支持手动导入 web 包的指南，请参阅[Web 服务器配置用于 Web 部署发布 （脱机部署）](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="93c91-184">For guidance on how to configure an IIS web server to support manually importing a web package, see [Configure a Web Server for Web Deploy Publishing (Offline Deployment)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md).</span></span> <span data-ttu-id="93c91-185">有关部署 web 包的更多常规指南，请参阅[演练：部署使用 Web 部署包 （第 1，共 4 部分） 的 Web 应用程序项目](https://msdn.microsoft.com/library/dd483479.aspx)。</span><span class="sxs-lookup"><span data-stu-id="93c91-185">For more general guidance on deploying web packages, see [Walkthrough: Deploying a Web Application Project Using a Web Deployment Package (Part 1 of 4)](https://msdn.microsoft.com/library/dd483479.aspx).</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="93c91-186">上一个</span><span class="sxs-lookup"><span data-stu-id="93c91-186">Previous</span></span>](creating-and-running-a-deployment-command-file.md)

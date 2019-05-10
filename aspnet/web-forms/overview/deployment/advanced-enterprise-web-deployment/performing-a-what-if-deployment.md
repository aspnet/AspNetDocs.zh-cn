---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/performing-a-what-if-deployment
title: 如果执行什么部署 |Microsoft Docs
author: jrjlee
description: 本主题介绍如何执行假设 （或模拟） 使用 Internet 信息服务 (IIS) Web 部署工具 （Web 部署） 和 V 部署...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: c711b453-01ac-4e65-a48c-93d99bf22e58
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/performing-a-what-if-deployment
msc.type: authoredcontent
ms.openlocfilehash: 73a0e038cc0d4ebae0ffc8ed3fd2de4c9dad673c
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/06/2019
ms.locfileid: "65127082"
---
# <a name="performing-a-what-if-deployment"></a><span data-ttu-id="7416b-103">执行“What If”部署</span><span class="sxs-lookup"><span data-stu-id="7416b-103">Performing a "What If" Deployment</span></span>

<span data-ttu-id="7416b-104">通过[Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="7416b-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="7416b-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="7416b-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="7416b-106">本主题介绍如何执行"假设"（或模拟） 使用 Internet 信息服务 (IIS) Web 部署工具 （Web 部署） 和 VSDBCMD 的部署。</span><span class="sxs-lookup"><span data-stu-id="7416b-106">This topic describes how to perform "what if" (or simulated) deployments using the Internet Information Services (IIS) Web Deployment Tool (Web Deploy) and VSDBCMD.</span></span> <span data-ttu-id="7416b-107">这样可以在实际部署你的应用程序之前确定部署逻辑对特定目标环境的影响。</span><span class="sxs-lookup"><span data-stu-id="7416b-107">This lets you determine the effects of your deployment logic on a particular target environment before you actually deploy your application.</span></span>

<span data-ttu-id="7416b-108">本主题窗体的一系列教程基于虚构公司 Fabrikam，Inc.的企业部署要求的一部分本系列教程将使用的示例解决方案&#x2014; [Contact Manager 解决方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;来表示真实级别的复杂性，包括 ASP.NET MVC 3 应用程序，Windows 通信的 web 应用程序Foundation (WCF) 服务和数据库项目。</span><span class="sxs-lookup"><span data-stu-id="7416b-108">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

<span data-ttu-id="7416b-109">这些教程的核心部署方法取决于拆分项目文件方法中所述[了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)，两个项目文件中生成和部署过程由控制的&#x2014;一个包含适用于每个目标环境，并包含特定于环境的生成和部署设置的生成说明。</span><span class="sxs-lookup"><span data-stu-id="7416b-109">The deployment method at the heart of these tutorials is based on the split project file approach described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md), in which the build and deployment process is controlled by two project files&#x2014;one containing build instructions that apply to every destination environment, and one containing environment-specific build and deployment settings.</span></span> <span data-ttu-id="7416b-110">在生成时，特定于环境的项目文件合并到不限环境的项目文件，以形成一组完整的生成说明。</span><span class="sxs-lookup"><span data-stu-id="7416b-110">At build time, the environment-specific project file is merged into the environment-agnostic project file to form a complete set of build instructions.</span></span>

## <a name="performing-a-what-if-deployment-for-web-packages"></a><span data-ttu-id="7416b-111">执行"假设"部署 Web 包</span><span class="sxs-lookup"><span data-stu-id="7416b-111">Performing a "What If" Deployment for Web Packages</span></span>

<span data-ttu-id="7416b-112">Web 部署包括使你能够执行"假设"中的部署的功能 （或试用版） 模式。</span><span class="sxs-lookup"><span data-stu-id="7416b-112">Web Deploy includes functionality that lets you perform deployments in "what if" (or trial) mode.</span></span> <span data-ttu-id="7416b-113">在部署中"假设"模式下的项目时，Web 部署生成一个日志文件，像执行了部署，但它实际上不会更改目标服务器上的任何内容。</span><span class="sxs-lookup"><span data-stu-id="7416b-113">When you deploy artifacts in "what if" mode, Web Deploy generates a log file as if you had performed the deployment, but it doesn't actually change anything on the destination server.</span></span> <span data-ttu-id="7416b-114">查看日志文件可帮助你了解你的部署将特别是对目标服务器上，产生的影响：</span><span class="sxs-lookup"><span data-stu-id="7416b-114">Reviewing the log file can help you to understand what impact your deployment will have on the destination server, in particular:</span></span>

- <span data-ttu-id="7416b-115">获取添加内容。</span><span class="sxs-lookup"><span data-stu-id="7416b-115">What will get added.</span></span>
- <span data-ttu-id="7416b-116">获取更新内容。</span><span class="sxs-lookup"><span data-stu-id="7416b-116">What will get updated.</span></span>
- <span data-ttu-id="7416b-117">什么会被删除。</span><span class="sxs-lookup"><span data-stu-id="7416b-117">What will get deleted.</span></span>

<span data-ttu-id="7416b-118">因为"假设"部署实际上不会更改内容始终不能在目标服务器上的任何内容是预测是否会成功部署。</span><span class="sxs-lookup"><span data-stu-id="7416b-118">Because a "what if" deployment doesn't actually change anything on the destination server, what it can't always do is predict whether a deployment will succeed.</span></span>

<span data-ttu-id="7416b-119">如中所述[部署 Web 包](../web-deployment-in-the-enterprise/deploying-web-packages.md)，你可以部署两种方式使用 Web 部署的 web 包&#x2014;使用 MSDeploy.exe 命令行实用程序直接或通过运行 *。 deploy.cmd*文件将生成的生成过程。</span><span class="sxs-lookup"><span data-stu-id="7416b-119">As described in [Deploying Web Packages](../web-deployment-in-the-enterprise/deploying-web-packages.md), you can deploy web packages using Web Deploy in two ways&#x2014;by using the MSDeploy.exe command-line utility directly or by running the *.deploy.cmd* file that the build process generates.</span></span>

<span data-ttu-id="7416b-120">如果您直接使用 MSDeploy.exe，则可以通过添加运行"假设"部署 **– whatif**到命令中的标志。</span><span class="sxs-lookup"><span data-stu-id="7416b-120">If you're using MSDeploy.exe directly, you can run a "what if" deployment by adding the **–whatif** flag to your command.</span></span> <span data-ttu-id="7416b-121">例如，若要评估如果 ContactManager.Mvc.zip 包部署到过渡环境，会发生什么情况，MSDeploy 命令应类似如下：</span><span class="sxs-lookup"><span data-stu-id="7416b-121">For example, to evaluate what would happen if you deployed the ContactManager.Mvc.zip package to a staging environment, the MSDeploy command should resemble this:</span></span>

[!code-console[Main](performing-a-what-if-deployment/samples/sample1.cmd)]

<span data-ttu-id="7416b-122">"假设"部署的结果感到满意后，可以删除 **– whatif**标志来运行实时部署。</span><span class="sxs-lookup"><span data-stu-id="7416b-122">When you're satisfied with the results of your "what if" deployment, you can remove the **–whatif** flag to run a live deployment.</span></span>

> [!NOTE]
> <span data-ttu-id="7416b-123">有关 MSDeploy.exe 命令行选项的详细信息，请参阅[Web 部署操作设置](https://technet.microsoft.com/library/dd569089(WS.10).aspx)。</span><span class="sxs-lookup"><span data-stu-id="7416b-123">For more information on command-line options for MSDeploy.exe, see [Web Deploy Operation Settings](https://technet.microsoft.com/library/dd569089(WS.10).aspx).</span></span>

<span data-ttu-id="7416b-124">如果您使用的 *。 deploy.cmd*文件中，您可以通过包含运行"假设"部署 **/t**标志 （试用模式） 而不是标志 **/y**中的标志 （"是，"或更新模式）你的命令。</span><span class="sxs-lookup"><span data-stu-id="7416b-124">If you're using the *.deploy.cmd* file, you can run a "what if" deployment by including the **/t** flag (trial mode) flag instead of the **/y** flag ("yes," or update mode) in your command.</span></span> <span data-ttu-id="7416b-125">例如，若要评估如果 ContactManager.Mvc.zip 包部署的运行，会发生什么情况 *。 deploy.cmd*文件中，您的命令应类似于下面：</span><span class="sxs-lookup"><span data-stu-id="7416b-125">For example, to evaluate what would happen if you deployed the ContactManager.Mvc.zip package by running the *.deploy.cmd* file, your command should resemble this:</span></span>

[!code-console[Main](performing-a-what-if-deployment/samples/sample2.cmd)]

<span data-ttu-id="7416b-126">"试用模式"部署的结果感到满意后，您可以替换 **/t**与标志 **/y**标志来运行实时部署：</span><span class="sxs-lookup"><span data-stu-id="7416b-126">When you're satisfied with the results of your "trial mode" deployment, you can replace the **/t** flag with a **/y** flag to run a live deployment:</span></span>

[!code-console[Main](performing-a-what-if-deployment/samples/sample3.cmd)]

> [!NOTE]
> <span data-ttu-id="7416b-127">有关详细信息的命令行选项 *。 deploy.cmd*文件，请参阅[如何：安装部署包使用 deploy.cmd 文件](https://msdn.microsoft.com/library/ff356104.aspx)。</span><span class="sxs-lookup"><span data-stu-id="7416b-127">For more information on command-line options for *.deploy.cmd* files, see [How to: Install a Deployment Package Using the deploy.cmd File](https://msdn.microsoft.com/library/ff356104.aspx).</span></span> <span data-ttu-id="7416b-128">如果在运行 *。 deploy.cmd*文件而无需指定任何标志，命令提示符将显示可用标志的列表。</span><span class="sxs-lookup"><span data-stu-id="7416b-128">If you run the *.deploy.cmd* file without specifying any flags, the command prompt will display a list of available flags.</span></span>

## <a name="performing-a-what-if-deployment-for-databases"></a><span data-ttu-id="7416b-129">执行"假设"部署的数据库</span><span class="sxs-lookup"><span data-stu-id="7416b-129">Performing a "What If" Deployment for Databases</span></span>

<span data-ttu-id="7416b-130">本部分假设你使用的 VSDBCMD 实用程序来执行增量备份，基于架构的数据库部署。</span><span class="sxs-lookup"><span data-stu-id="7416b-130">This section assumes that you're using the VSDBCMD utility to perform incremental, schema-based database deployment.</span></span> <span data-ttu-id="7416b-131">此方法进行了更详细地[部署数据库项目](../web-deployment-in-the-enterprise/deploying-database-projects.md)。</span><span class="sxs-lookup"><span data-stu-id="7416b-131">This approach is described in more detail in [Deploying Database Projects](../web-deployment-in-the-enterprise/deploying-database-projects.md).</span></span> <span data-ttu-id="7416b-132">我们建议你了解与本主题之前应用此处所述的概念。</span><span class="sxs-lookup"><span data-stu-id="7416b-132">We recommend that you familiarize yourself with this topic before you apply the concepts described here.</span></span>

<span data-ttu-id="7416b-133">当你使用在 VSDBCMD**部署**模式下，可以使用 **/dd** (或 **/DeployToDatabase**) 标记，用于控制是否 VSDBCMD 实际部署数据库或只是生成部署脚本。</span><span class="sxs-lookup"><span data-stu-id="7416b-133">When you use VSDBCMD in **Deploy** mode, you can use the **/dd** (or **/DeployToDatabase**) flag to control whether VSDBCMD actually deploys the database or just generates a deployment script.</span></span> <span data-ttu-id="7416b-134">如果你正在部署.dbschema 文件，这是行为：</span><span class="sxs-lookup"><span data-stu-id="7416b-134">If you're deploying a .dbschema file, this is the behavior:</span></span>

- <span data-ttu-id="7416b-135">如果指定 **/dd+** 或 **/dd**，VSDBCMD 将生成部署脚本和部署数据库。</span><span class="sxs-lookup"><span data-stu-id="7416b-135">If you specify **/dd+** or **/dd**, VSDBCMD will generate a deployment script and deploy the database.</span></span>
- <span data-ttu-id="7416b-136">如果指定 **/dd-** 或省略开关，VSDBCMD 将生成部署脚本。</span><span class="sxs-lookup"><span data-stu-id="7416b-136">If you specify **/dd-** or omit the switch, VSDBCMD will generate a deployment script only.</span></span>

> [!NOTE]
> <span data-ttu-id="7416b-137">如果你正在部署.deploymanifest 文件而不是.dbschema 文件的行为 **/dd**开关是复杂得多。</span><span class="sxs-lookup"><span data-stu-id="7416b-137">If you're deploying a .deploymanifest file rather than a .dbschema file, the behavior of the **/dd** switch is a lot more complicated.</span></span> <span data-ttu-id="7416b-138">VSDBCMD 实质上，将忽略的值 **/dd**切换如果.deploymanifest 文件包含**DeployToDatabase**的值元素**True**。</span><span class="sxs-lookup"><span data-stu-id="7416b-138">Essentially, VSDBCMD will ignore the value of the **/dd** switch if the .deploymanifest file includes a **DeployToDatabase** element with a value of **True**.</span></span> <span data-ttu-id="7416b-139">[部署数据库项目](../web-deployment-in-the-enterprise/deploying-database-projects.md)描述完整此行为。</span><span class="sxs-lookup"><span data-stu-id="7416b-139">[Deploying Database Projects](../web-deployment-in-the-enterprise/deploying-database-projects.md) describes this behavior in full.</span></span>

<span data-ttu-id="7416b-140">例如，若要生成的部署脚本**ContactManager**数据库而不实际部署的数据库，VSDBCMD 命令应类似于下面：</span><span class="sxs-lookup"><span data-stu-id="7416b-140">For example, to generate a deployment script for the **ContactManager** database without actually deploying the database, your VSDBCMD command should resemble this:</span></span>

[!code-console[Main](performing-a-what-if-deployment/samples/sample4.cmd)]

<span data-ttu-id="7416b-141">VSDBCMD 是差异数据库部署工具，并且这种情况下部署脚本动态生成以包含所有更新当前数据库中，如果存在，为指定的架构所需的 SQL 命令。</span><span class="sxs-lookup"><span data-stu-id="7416b-141">VSDBCMD is a differential database deployment tool, and as such the deployment script is dynamically generated to contain all the SQL commands necessary to update the current database, if one exists, to the specified schema.</span></span> <span data-ttu-id="7416b-142">查看部署脚本是有用的方式来确定有何影响你的部署将对当前数据库和它所包含的数据。</span><span class="sxs-lookup"><span data-stu-id="7416b-142">Reviewing the deployment script is a useful way to determine what impact your deployment will have on the current database and the data it contains.</span></span> <span data-ttu-id="7416b-143">例如，你可能想要确定：</span><span class="sxs-lookup"><span data-stu-id="7416b-143">For example, you might want to determine:</span></span>

- <span data-ttu-id="7416b-144">是否将删除任何现有的表，并且是否这会导致数据丢失。</span><span class="sxs-lookup"><span data-stu-id="7416b-144">Whether any existing tables will be removed, and whether that will result in data loss.</span></span>
- <span data-ttu-id="7416b-145">无论操作的顺序中会带来风险的数据丢失，例如，如果你拆分或合并表。</span><span class="sxs-lookup"><span data-stu-id="7416b-145">Whether the order of operations carries a risk of data loss, for example, if you're splitting or merging tables.</span></span>

<span data-ttu-id="7416b-146">如果您愿意使用部署脚本，您可以重复使用 VSDBCMD **/dd+** 标志来进行更改。</span><span class="sxs-lookup"><span data-stu-id="7416b-146">If you're happy with the deployment script, you can repeat the VSDBCMD with a **/dd+** flag to make the changes.</span></span> <span data-ttu-id="7416b-147">或者，可以编辑部署脚本来满足您的要求，然后在数据库服务器上手动执行。</span><span class="sxs-lookup"><span data-stu-id="7416b-147">Alternatively, you can edit the deployment script to meet your requirements and then execute it manually on the database server.</span></span>

## <a name="integrating-what-if-functionality-into-custom-project-files"></a><span data-ttu-id="7416b-148">将"假设"功能集成到自定义项目文件</span><span class="sxs-lookup"><span data-stu-id="7416b-148">Integrating "What If" Functionality into Custom Project Files</span></span>

<span data-ttu-id="7416b-149">在更复杂的部署方案中，你将想要使用自定义的 Microsoft Build Engine (MSBuild) 项目文件来封装你生成和部署的逻辑，如中所述[了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)。</span><span class="sxs-lookup"><span data-stu-id="7416b-149">In more complex deployment scenarios, you'll want to use a custom Microsoft Build Engine (MSBuild) project file to encapsulate your build and deployment logic, as described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md).</span></span> <span data-ttu-id="7416b-150">例如，在[联系人管理器](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)示例解决方案， *Publish.proj*文件：</span><span class="sxs-lookup"><span data-stu-id="7416b-150">For example, in the [Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) sample solution, the *Publish.proj* file:</span></span>

- <span data-ttu-id="7416b-151">生成解决方案。</span><span class="sxs-lookup"><span data-stu-id="7416b-151">Builds the solution.</span></span>
- <span data-ttu-id="7416b-152">使用 Web 部署来打包和部署 ContactManager.Mvc 应用程序。</span><span class="sxs-lookup"><span data-stu-id="7416b-152">Uses Web Deploy to package and deploy the ContactManager.Mvc application.</span></span>
- <span data-ttu-id="7416b-153">使用 Web 部署来打包和部署 ContactManager.Service 应用程序。</span><span class="sxs-lookup"><span data-stu-id="7416b-153">Uses Web Deploy to package and deploy the ContactManager.Service application.</span></span>
- <span data-ttu-id="7416b-154">部署**ContactManager**数据库。</span><span class="sxs-lookup"><span data-stu-id="7416b-154">Deploys the **ContactManager** database.</span></span>

<span data-ttu-id="7416b-155">集成时的多个 web 包和/或数据库部署到单步执行进程以这种方式，您还可以在"假设"模式下执行整个部署的选项。</span><span class="sxs-lookup"><span data-stu-id="7416b-155">When you integrate the deployment of multiple web packages and/or databases into a single-step process in this way, you may also want the option of performing the entire deployment in a "what if" mode.</span></span>

<span data-ttu-id="7416b-156">*Publish.proj*文件演示了如何执行此操作。</span><span class="sxs-lookup"><span data-stu-id="7416b-156">The *Publish.proj* file demonstrates how you can do this.</span></span> <span data-ttu-id="7416b-157">首先，需要创建用于存储"假设"值的属性：</span><span class="sxs-lookup"><span data-stu-id="7416b-157">First, you need to create a property to store the "what if" value:</span></span>

[!code-xml[Main](performing-a-what-if-deployment/samples/sample5.xml)]

<span data-ttu-id="7416b-158">在这种情况下，创建名为的属性**WhatIf**默认值为**false**。</span><span class="sxs-lookup"><span data-stu-id="7416b-158">In this case, you've created a property named **WhatIf** with a default value of **false**.</span></span> <span data-ttu-id="7416b-159">用户可通过将属性设置为覆盖此值 **，则返回 true**在命令行参数中，你很快将会介绍。</span><span class="sxs-lookup"><span data-stu-id="7416b-159">Users can override this value by setting the property to **true** in a command-line parameter, as you'll see shortly.</span></span>

<span data-ttu-id="7416b-160">下一阶段是参数化任何 Web 部署和 VSDBCMD 命令，以便反映标志**WhatIf**属性值。</span><span class="sxs-lookup"><span data-stu-id="7416b-160">The next stage is to parameterize any Web Deploy and VSDBCMD commands so that the flags reflect the **WhatIf** property value.</span></span> <span data-ttu-id="7416b-161">例如下, 一个目标 (摘自*Publish.proj*文件，并简化) 运行 *。 deploy.cmd*文件来部署 web 包。</span><span class="sxs-lookup"><span data-stu-id="7416b-161">For example, the next target (taken from the *Publish.proj* file and simplified) runs the *.deploy.cmd* file to deploy a web package.</span></span> <span data-ttu-id="7416b-162">默认情况下，该命令包含 **/Y**开关 （"是，"或更新模式）。</span><span class="sxs-lookup"><span data-stu-id="7416b-162">By default, the command includes a **/Y** switch ("yes," or update mode).</span></span> <span data-ttu-id="7416b-163">如果**WhatIf**设置为**true**，这将替换为 **/T**开关 （试用版或"假设"模式下）。</span><span class="sxs-lookup"><span data-stu-id="7416b-163">If **WhatIf** is set to **true**, this is replaced by a **/T** switch (trial, or "what if" mode).</span></span>

[!code-xml[Main](performing-a-what-if-deployment/samples/sample6.xml)]

<span data-ttu-id="7416b-164">同样下, 一步目标使用 VSDBCMD 实用程序来部署数据库。</span><span class="sxs-lookup"><span data-stu-id="7416b-164">Similarly, the next target uses the VSDBCMD utility to deploy a database.</span></span> <span data-ttu-id="7416b-165">默认情况下 **/dd**不包含开关。</span><span class="sxs-lookup"><span data-stu-id="7416b-165">By default, a **/dd** switch is not included.</span></span> <span data-ttu-id="7416b-166">这意味着 VSDBCMD 将生成部署脚本，但不是会将数据库部署&#x2014;换而言之，"假设"方案。</span><span class="sxs-lookup"><span data-stu-id="7416b-166">This means that VSDBCMD will generate a deployment script but will not deploy the database&#x2014;in other words, a "what if" scenario.</span></span> <span data-ttu-id="7416b-167">如果**WhatIf**属性未设置为**true**即 **/dd**添加开关并将其 VSDBCMD 将部署数据库。</span><span class="sxs-lookup"><span data-stu-id="7416b-167">If the **WhatIf** property is not set to **true**, a **/dd** switch is added and VSDBCMD will deploy the database.</span></span>

[!code-xml[Main](performing-a-what-if-deployment/samples/sample7.xml)]

<span data-ttu-id="7416b-168">相同的方法可用于所有相关的命令参数化在项目文件中。</span><span class="sxs-lookup"><span data-stu-id="7416b-168">You can use the same approach to parameterize all the relevant commands in your project file.</span></span> <span data-ttu-id="7416b-169">当你想要运行"假设"部署时，然后，可以只需提供**WhatIf**属性值从命令行：</span><span class="sxs-lookup"><span data-stu-id="7416b-169">When you want to run a "what if" deployment, you can then simply provide a **WhatIf** property value from the command line:</span></span>

[!code-console[Main](performing-a-what-if-deployment/samples/sample8.cmd)]

<span data-ttu-id="7416b-170">这样一来，可以运行"假设"部署，以在单个步骤中的所有项目组件。</span><span class="sxs-lookup"><span data-stu-id="7416b-170">In this way, you can run a "what if" deployment for all your project components in a single step.</span></span>

## <a name="conclusion"></a><span data-ttu-id="7416b-171">结束语</span><span class="sxs-lookup"><span data-stu-id="7416b-171">Conclusion</span></span>

<span data-ttu-id="7416b-172">本主题介绍了如何运行"假设"使用 Web 部署、 VSDBCMD 和 MSBuild 的部署。</span><span class="sxs-lookup"><span data-stu-id="7416b-172">This topic described how to run "what if" deployments using Web Deploy, VSDBCMD, and MSBuild.</span></span> <span data-ttu-id="7416b-173">"假设"部署可让你实际上到目标环境进行任何更改之前评估建议的部署的影响。</span><span class="sxs-lookup"><span data-stu-id="7416b-173">A "what if" deployment lets you evaluate the impact of a proposed deployment before you actually make any changes to the destination environment.</span></span>

## <a name="further-reading"></a><span data-ttu-id="7416b-174">其他阅读材料</span><span class="sxs-lookup"><span data-stu-id="7416b-174">Further Reading</span></span>

<span data-ttu-id="7416b-175">Web 部署命令行语法的详细信息，请参阅[Web 部署操作设置](https://technet.microsoft.com/library/dd569089(WS.10).aspx)。</span><span class="sxs-lookup"><span data-stu-id="7416b-175">For more information on Web Deploy command-line syntax, see [Web Deploy Operation Settings](https://technet.microsoft.com/library/dd569089(WS.10).aspx).</span></span> <span data-ttu-id="7416b-176">有关当你使用的命令行选项的指导 *。 deploy.cmd*文件，请参阅[如何：安装部署包使用 deploy.cmd 文件](https://msdn.microsoft.com/library/ff356104.aspx)。</span><span class="sxs-lookup"><span data-stu-id="7416b-176">For guidance on command-line options when you use the *.deploy.cmd* file, see [How to: Install a Deployment Package Using the deploy.cmd File](https://msdn.microsoft.com/library/ff356104.aspx).</span></span> <span data-ttu-id="7416b-177">有关 VSDBCMD 命令行语法的指导，请参阅[VSDBCMD 的命令行参考。EXE （部署和架构导入）](https://msdn.microsoft.com/library/dd193283.aspx)。</span><span class="sxs-lookup"><span data-stu-id="7416b-177">For guidance on VSDBCMD command-line syntax, see [Command-Line Reference for VSDBCMD.EXE (Deployment and Schema Import)](https://msdn.microsoft.com/library/dd193283.aspx).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="7416b-178">[上一页](advanced-enterprise-web-deployment.md)
> [下一页](customizing-database-deployments-for-multiple-environments.md)</span><span class="sxs-lookup"><span data-stu-id="7416b-178">[Previous](advanced-enterprise-web-deployment.md)
[Next](customizing-database-deployments-for-multiple-environments.md)</span></span>

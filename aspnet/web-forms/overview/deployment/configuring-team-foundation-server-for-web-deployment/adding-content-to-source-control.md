---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/adding-content-to-source-control
title: 向源代码管理添加内容 |Microsoft Docs
author: jrjlee
description: 本主题说明如何在 Team Foundation Server （TFS）2010中将内容添加到源代码管理。 其中介绍了如何将解决方案和项目添加到团队项目 。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 86c14aab-c2dd-4f73-b40c-c6d52fa44950
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/adding-content-to-source-control
msc.type: authoredcontent
ms.openlocfilehash: 16073dd2fb0ea1cc4ddbc94c843181933dc174c1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78515108"
---
# <a name="adding-content-to-source-control"></a><span data-ttu-id="d3970-104">向源代码管理添加内容</span><span class="sxs-lookup"><span data-stu-id="d3970-104">Adding Content to Source Control</span></span>

<span data-ttu-id="d3970-105">作者： [Jason](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="d3970-105">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="d3970-106">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="d3970-106">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="d3970-107">本主题说明如何在 Team Foundation Server （TFS）2010中将内容添加到源代码管理。</span><span class="sxs-lookup"><span data-stu-id="d3970-107">This topic explains how to add content to source control in Team Foundation Server (TFS) 2010.</span></span> <span data-ttu-id="d3970-108">它介绍如何将解决方案和项目添加到 TFS 中的团队项目，并说明如何将外部依赖项（如框架或程序集）添加到源代码管理。</span><span class="sxs-lookup"><span data-stu-id="d3970-108">It describes how to add solutions and projects to a team project in TFS, and it explains how to add external dependencies like frameworks or assemblies to source control.</span></span>

<span data-ttu-id="d3970-109">本主题介绍一系列教程的一部分，这些教程基于名为 Fabrikam，Inc. 的虚构公司的企业部署要求。本教程系列使用一个示例解决方案&#x2014;，该解决方案使用[联系人管理器解决方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;来表示具有真实复杂性级别的 web 应用程序，包括 ASP.NET MVC 3 应用程序、Windows Communication Foundation （WCF）服务和数据库项目。</span><span class="sxs-lookup"><span data-stu-id="d3970-109">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

## <a name="task-overview"></a><span data-ttu-id="d3970-110">任务概述</span><span class="sxs-lookup"><span data-stu-id="d3970-110">Task Overview</span></span>

<span data-ttu-id="d3970-111">在大多数情况下，开发人员团队的每个成员都应该能够向源代码管理添加内容。</span><span class="sxs-lookup"><span data-stu-id="d3970-111">In most cases, every member of the developer team should be able to add content to source control.</span></span> <span data-ttu-id="d3970-112">若要将解决方案添加到 TFS 中的源代码管理，需要完成以下高级步骤：</span><span class="sxs-lookup"><span data-stu-id="d3970-112">To add a solution to source control in TFS, you'll need to complete these high-level steps:</span></span>

- <span data-ttu-id="d3970-113">连接到团队项目。</span><span class="sxs-lookup"><span data-stu-id="d3970-113">Connect to a team project.</span></span>
- <span data-ttu-id="d3970-114">将服务器上的团队项目文件夹结构映射到本地计算机上的文件夹结构。</span><span class="sxs-lookup"><span data-stu-id="d3970-114">Map the team project folder structure on the server to a folder structure on your local computer.</span></span>
- <span data-ttu-id="d3970-115">将解决方案及其内容添加到源代码管理。</span><span class="sxs-lookup"><span data-stu-id="d3970-115">Add the solution and its contents to source control.</span></span>
- <span data-ttu-id="d3970-116">向源代码管理添加任何外部依赖项。</span><span class="sxs-lookup"><span data-stu-id="d3970-116">Add any external dependencies to source control.</span></span>

<span data-ttu-id="d3970-117">本主题将演示如何执行这些过程。</span><span class="sxs-lookup"><span data-stu-id="d3970-117">This topic will show you how to perform these procedures.</span></span>

<span data-ttu-id="d3970-118">本主题中的任务和演练假设已创建一个新的 TFS 团队项目来管理内容。</span><span class="sxs-lookup"><span data-stu-id="d3970-118">The tasks and walkthroughs in this topic assume that you've already created a new TFS team project to manage your content.</span></span> <span data-ttu-id="d3970-119">有关创建新团队项目的详细信息，请参阅[在 TFS 中创建团队项目](creating-a-team-project-in-tfs.md)。</span><span class="sxs-lookup"><span data-stu-id="d3970-119">For more information on creating a new team project, see [Creating a Team Project in TFS](creating-a-team-project-in-tfs.md).</span></span>

### <a name="who-performs-these-procedures"></a><span data-ttu-id="d3970-120">谁执行这些过程？</span><span class="sxs-lookup"><span data-stu-id="d3970-120">Who Performs These Procedures?</span></span>

<span data-ttu-id="d3970-121">在大多数情况下，开发人员团队的每个成员都应该能够在特定团队项目中添加和修改内容。</span><span class="sxs-lookup"><span data-stu-id="d3970-121">In most cases, every member of the developer team should be able to add and modify content within specific team projects.</span></span>

## <a name="connect-to-a-team-project-and-create-a-folder-mapping"></a><span data-ttu-id="d3970-122">连接到团队项目并创建文件夹映射</span><span class="sxs-lookup"><span data-stu-id="d3970-122">Connect to a Team Project and Create a Folder Mapping</span></span>

<span data-ttu-id="d3970-123">在将任何内容添加到源代码管理之前，需要连接到团队项目，并在服务器上的文件夹结构和本地计算机上的文件系统之间创建映射。</span><span class="sxs-lookup"><span data-stu-id="d3970-123">Before you add any content to source control, you need to connect to a team project and create a mapping between the folder structure on the server and the file system on your local machine.</span></span>

<span data-ttu-id="d3970-124">**连接到团队项目并映射本地路径**</span><span class="sxs-lookup"><span data-stu-id="d3970-124">**To connect to a team project and map a local path**</span></span>

1. <span data-ttu-id="d3970-125">在开发人员工作站上，打开 Visual Studio 2010。</span><span class="sxs-lookup"><span data-stu-id="d3970-125">On your developer workstation, open Visual Studio 2010.</span></span>
2. <span data-ttu-id="d3970-126">在 Visual Studio 的 "**团队**" 菜单上，单击 "**连接到 Team Foundation Server**"。</span><span class="sxs-lookup"><span data-stu-id="d3970-126">In Visual Studio, on the **Team** menu, click **Connect to Team Foundation Server**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d3970-127">如果已配置到 TFS 服务器的连接，则可以省略步骤3-6。</span><span class="sxs-lookup"><span data-stu-id="d3970-127">If you have already configured a connection to a TFS server, you can omit steps 3-6.</span></span>
3. <span data-ttu-id="d3970-128">在 "**连接到团队项目**" 对话框中，单击 "**服务器**"。</span><span class="sxs-lookup"><span data-stu-id="d3970-128">In the **Connection to Team Project** dialog box, click **Servers**.</span></span>
4. <span data-ttu-id="d3970-129">在 "**添加/删除 Team Foundation Server** " 对话框中，单击 "**添加**"。</span><span class="sxs-lookup"><span data-stu-id="d3970-129">In the **Add/Remove Team Foundation Server** dialog box, click **Add**.</span></span>
5. <span data-ttu-id="d3970-130">在 "**添加 Team Foundation Server** " 对话框中，提供 TFS 实例的详细信息，然后单击 **"确定"** 。</span><span class="sxs-lookup"><span data-stu-id="d3970-130">In the **Add Team Foundation Server** dialog box, provide the details of your TFS instance, and then click **OK**.</span></span>

    ![](adding-content-to-source-control/_static/image1.png)
6. <span data-ttu-id="d3970-131">在 "**添加/删除 Team Foundation Server** " 对话框中，单击 "**关闭**"。</span><span class="sxs-lookup"><span data-stu-id="d3970-131">In the **Add/Remove Team Foundation Server** dialog box, click **Close**.</span></span>
7. <span data-ttu-id="d3970-132">在 "**连接到团队项目**" 对话框中，选择要连接到的 TFS 实例，选择 "团队项目集合"，选择要添加到的团队项目，然后单击 "**连接**"。</span><span class="sxs-lookup"><span data-stu-id="d3970-132">In the **Connect to Team Project** dialog box, select the TFS instance you want to connect to, select the team project collection, select the team project you want to add to, and then click **Connect**.</span></span>

    ![](adding-content-to-source-control/_static/image2.png)
8. <span data-ttu-id="d3970-133">在 "**团队资源管理器**" 窗口中，展开你的团队项目，然后双击 "**源代码管理**"。</span><span class="sxs-lookup"><span data-stu-id="d3970-133">In the **Team Explorer** window, expand your team project, and then double-click **Source Control**.</span></span>

    ![](adding-content-to-source-control/_static/image3.png)
9. <span data-ttu-id="d3970-134">在 "**源代码管理器**" 选项卡上，单击 "**未映射**"。</span><span class="sxs-lookup"><span data-stu-id="d3970-134">On the **Source Control Explorer** tab, click **Not mapped**.</span></span>

    ![](adding-content-to-source-control/_static/image4.png)
10. <span data-ttu-id="d3970-135">在 "**映射**" 对话框中的 "**本地文件夹**" 框中，浏览到（或创建）一个本地文件夹，将其用作团队项目的根文件夹，然后单击 "**映射**"。</span><span class="sxs-lookup"><span data-stu-id="d3970-135">In the **Map** dialog box, in the **Local folder** box, browse to (or create) a local folder to act as the root folder for the team project, and then click **Map**.</span></span>

    ![](adding-content-to-source-control/_static/image5.png)
11. <span data-ttu-id="d3970-136">如果系统提示你下载源文件，请单击 **"是"** 。</span><span class="sxs-lookup"><span data-stu-id="d3970-136">When you're prompted to download source files, click **Yes**.</span></span>

    ![](adding-content-to-source-control/_static/image6.png)

<span data-ttu-id="d3970-137">此时，已将团队项目的服务器端文件夹映射到开发人员工作站上的本地文件夹。</span><span class="sxs-lookup"><span data-stu-id="d3970-137">At this point, you have mapped the server-side folder for the team project to a local folder on your developer workstation.</span></span> <span data-ttu-id="d3970-138">你还将团队项目中的任何现有内容下载到本地文件夹结构。</span><span class="sxs-lookup"><span data-stu-id="d3970-138">You've also downloaded any existing content from the team project to your local folder structure.</span></span> <span data-ttu-id="d3970-139">你现在可以开始将自己的内容添加到源代码管理。</span><span class="sxs-lookup"><span data-stu-id="d3970-139">You can now start to add your own content to source control.</span></span>

## <a name="add-projects-and-solutions-to-source-control"></a><span data-ttu-id="d3970-140">向源代码管理添加项目和解决方案</span><span class="sxs-lookup"><span data-stu-id="d3970-140">Add Projects and Solutions to Source Control</span></span>

<span data-ttu-id="d3970-141">若要将项目和解决方案添加到源代码管理，首先需要将它们移到本地计算机上的团队项目的映射文件夹中。</span><span class="sxs-lookup"><span data-stu-id="d3970-141">To add projects and solutions to source control, you first need to move them to the mapped folder for the team project on your local machine.</span></span> <span data-ttu-id="d3970-142">然后，你可以签入内容以将添加的内容与服务器同步。</span><span class="sxs-lookup"><span data-stu-id="d3970-142">You can then check in the content to synchronize your additions with the server.</span></span>

<span data-ttu-id="d3970-143">**向源代码管理添加项目**</span><span class="sxs-lookup"><span data-stu-id="d3970-143">**To add projects to source control**</span></span>

1. <span data-ttu-id="d3970-144">在开发人员工作站上，将项目和解决方案移动到团队项目的映射文件夹结构内的适当位置。</span><span class="sxs-lookup"><span data-stu-id="d3970-144">On your developer workstation, move your projects and solutions to an appropriate location within the mapped folder structure for the team project.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d3970-145">很多组织都有一个首选方法，即如何在源代码管理中组织项目和解决方案。</span><span class="sxs-lookup"><span data-stu-id="d3970-145">Many organizations will have a preferred approach to how projects and solutions should be organized in source control.</span></span> <span data-ttu-id="d3970-146">有关如何构造文件夹的指导，请参阅[如何：在 Team Foundation Server 中构造源代码管理文件夹](https://msdn.microsoft.com/library/bb668992.aspx)。</span><span class="sxs-lookup"><span data-stu-id="d3970-146">For guidance on how to structure folders, see [How To: Structure Your Source Control Folders in Team Foundation Server](https://msdn.microsoft.com/library/bb668992.aspx).</span></span>
2. <span data-ttu-id="d3970-147">在 Visual Studio 2010 中打开解决方案。</span><span class="sxs-lookup"><span data-stu-id="d3970-147">Open the solution in Visual Studio 2010.</span></span>
3. <span data-ttu-id="d3970-148">在 "**解决方案资源管理器**" 窗口中，右键单击解决方案，然后单击 "**将解决方案添加到源代码管理**"。</span><span class="sxs-lookup"><span data-stu-id="d3970-148">In the **Solution Explorer** window, right-click the solution, and then click **Add Solution to Source Control**.</span></span>

    ![](adding-content-to-source-control/_static/image7.png)

    > [!NOTE]
    > <span data-ttu-id="d3970-149">在某些情况下，你可能需要将项目单独添加到源代码管理中，以便更精确地控制对源代码的组织方式，这在某些情况下，具体取决于你的组织对 TFS 中的内容进行结构控制的方式。</span><span class="sxs-lookup"><span data-stu-id="d3970-149">In some cases, depending on how your organization likes to structure content in TFS, you may need to add projects to source control individually to provide more fine-grained control over how your source code is organized.</span></span>
4. <span data-ttu-id="d3970-150">验证 "**源代码管理器**" 选项卡是否显示已在团队项目的服务器文件夹结构中添加的内容。</span><span class="sxs-lookup"><span data-stu-id="d3970-150">Verify that the **Source Control Explorer** tab displays the content you've added within the server folder structure for the team project.</span></span>

    ![](adding-content-to-source-control/_static/image8.png)

    > [!NOTE]
    > <span data-ttu-id="d3970-151">"**源代码管理器**" 选项卡显示你的内容，而无需进一步提示，因为你已将解决方案添加到本地文件系统上的映射文件夹中。</span><span class="sxs-lookup"><span data-stu-id="d3970-151">The **Source Control Explorer** tab displays your content with no further prompting because you added your solution to a mapped folder on the local file system.</span></span> <span data-ttu-id="d3970-152">如果你的解决方案在未映射的位置，则系统会提示你指定 TFS 和本地文件系统中的文件夹位置。</span><span class="sxs-lookup"><span data-stu-id="d3970-152">If your solution was in an unmapped location, you'd be prompted to specify folder locations in both TFS and your local file system.</span></span>
5. <span data-ttu-id="d3970-153">在 "**源代码管理器**" 选项卡上的 "**文件夹**" 窗格中，右键单击团队项目（例如**ContactManager**），然后单击 "**签入挂起的更改**"。</span><span class="sxs-lookup"><span data-stu-id="d3970-153">On the **Source Control Explorer** tab, in the **Folders** pane, right-click the team project (for example, **ContactManager**), and then click **Check In Pending Changes**.</span></span>
6. <span data-ttu-id="d3970-154">在 "**签入-源文件**" 对话框中，键入注释，然后单击 "**签入**"。</span><span class="sxs-lookup"><span data-stu-id="d3970-154">In the **Check In – Source Files** dialog box, type a comment, and then click **Check In**.</span></span>

    ![](adding-content-to-source-control/_static/image9.png)

<span data-ttu-id="d3970-155">此时，已将解决方案添加到 TFS 中的源代码管理。</span><span class="sxs-lookup"><span data-stu-id="d3970-155">At this point you have added your solution to source control in TFS.</span></span>

## <a name="add-external-dependencies-to-source-control"></a><span data-ttu-id="d3970-156">向源代码管理添加外部依赖项</span><span class="sxs-lookup"><span data-stu-id="d3970-156">Add External Dependencies to Source Control</span></span>

<span data-ttu-id="d3970-157">向源代码管理添加项目或解决方案时，还将添加项目或解决方案中的所有文件和文件夹。</span><span class="sxs-lookup"><span data-stu-id="d3970-157">When you add a project or solution to source control, any files and folders within your project or solution will also be added.</span></span> <span data-ttu-id="d3970-158">但是，在很多情况下，项目和解决方案也依赖于外部依赖项（如本地程序集）才能正常工作。</span><span class="sxs-lookup"><span data-stu-id="d3970-158">However, in a lot of cases, projects and solutions also rely on external dependencies, like local assemblies, to function properly.</span></span> <span data-ttu-id="d3970-159">你需要将任何此类资源添加到源代码管理中，以允许团队生成和开发人员团队的其他成员成功生成你的代码。</span><span class="sxs-lookup"><span data-stu-id="d3970-159">You need to add any such resources to source control to let both Team Build and other members of the developer team build your code successfully.</span></span>

<span data-ttu-id="d3970-160">例如，联系人管理器示例解决方案的文件夹结构包含一个名为 "包" 的文件夹。</span><span class="sxs-lookup"><span data-stu-id="d3970-160">For example, the folder structure for the Contact Manager sample solution includes a folder named packages.</span></span> <span data-ttu-id="d3970-161">其中包含 ADO.NET 实体框架4.1 的程序集和各种支持资源。</span><span class="sxs-lookup"><span data-stu-id="d3970-161">This contains the assembly and various supporting resources for the ADO.NET Entity Framework 4.1.</span></span> <span data-ttu-id="d3970-162">"包" 文件夹不是 "联系人管理器" 解决方案的一部分，但是如果没有该文件夹，该解决方案将无法成功生成。</span><span class="sxs-lookup"><span data-stu-id="d3970-162">The packages folder is not part of the Contact Manager solution, but the solution will not build successfully without it.</span></span> <span data-ttu-id="d3970-163">若要启用 Team Build 来生成解决方案，需要将 "包" 文件夹添加到源代码管理中。</span><span class="sxs-lookup"><span data-stu-id="d3970-163">To enable Team Build to build the solution, you need to add the packages folder to source control.</span></span>

> [!NOTE]
> <span data-ttu-id="d3970-164">包含 "包" 文件夹的典型情况是，使用适用于 Visual Studio 2010 的 NuGet 扩展向解决方案添加实体框架或类似资源时，会发生什么情况。</span><span class="sxs-lookup"><span data-stu-id="d3970-164">The inclusion of a packages folder is typical of what happens when you add the Entity Framework, or similar resources, to your solution using the NuGet extension for Visual Studio 2010.</span></span>

<span data-ttu-id="d3970-165">**向源代码管理添加非项目内容**</span><span class="sxs-lookup"><span data-stu-id="d3970-165">**To add non-project content to source control**</span></span>

1. <span data-ttu-id="d3970-166">确保要添加的项（例如，包文件夹）位于本地文件系统的映射文件夹中的适当位置。</span><span class="sxs-lookup"><span data-stu-id="d3970-166">Ensure that the items you want to add (for example, the packages folder) are in an appropriate location within a mapped folder on your local file system.</span></span>
2. <span data-ttu-id="d3970-167">在 Visual Studio 2010 的 "**团队资源管理器**" 窗口中，展开你的团队项目，然后双击 "**源代码管理**"。</span><span class="sxs-lookup"><span data-stu-id="d3970-167">In Visual Studio 2010, In the **Team Explorer** window, expand your team project, and then double-click **Source Control**.</span></span>

    ![](adding-content-to-source-control/_static/image10.png)
3. <span data-ttu-id="d3970-168">在 "**源代码管理器**" 选项卡上的 "**文件夹**" 窗格中，选择包含要添加的项的文件夹。</span><span class="sxs-lookup"><span data-stu-id="d3970-168">On the **Source Control Explorer** tab, in the **Folders** pane, select the folder that contains the item or items you want to add.</span></span>
4. <span data-ttu-id="d3970-169">单击 "**将项目添加到文件夹**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="d3970-169">Click the **Add Items to Folder** button.</span></span>

    ![](adding-content-to-source-control/_static/image11.png)
5. <span data-ttu-id="d3970-170">在 "**添加到源代码管理**" 对话框中，选择要添加的文件夹，然后单击 "**下一步**"。</span><span class="sxs-lookup"><span data-stu-id="d3970-170">In the **Add to Source Control** dialog box, select the folder or items you want to add, and then click **Next**.</span></span>

    ![](adding-content-to-source-control/_static/image12.png)
6. <span data-ttu-id="d3970-171">在 "已**排除的项**" 选项卡上，选择已自动排除的所有必需项（例如，程序集），然后单击 "**包括项**"。</span><span class="sxs-lookup"><span data-stu-id="d3970-171">On the **Excluded items** tab, select any required items that have been automatically excluded (for example, assemblies), and then click **Include item(s)**.</span></span>

    ![](adding-content-to-source-control/_static/image13.png)
7. <span data-ttu-id="d3970-172">在 "**要添加的项**" 选项卡上，验证是否列出了要包含的所有文件，然后单击 "**完成**"。</span><span class="sxs-lookup"><span data-stu-id="d3970-172">On the **Items to add** tab, verify that all the files you want to include are listed, and then click **Finish**.</span></span>

    ![](adding-content-to-source-control/_static/image14.png)
8. <span data-ttu-id="d3970-173">在 "**源代码管理器**" 窗口中，单击 "**签入**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="d3970-173">In the **Source Control Explorer** window, click the **Check In** button.</span></span>

    ![](adding-content-to-source-control/_static/image15.png)
9. <span data-ttu-id="d3970-174">在 "**签入-源文件**" 对话框中，键入注释，然后单击 "**签入**"。</span><span class="sxs-lookup"><span data-stu-id="d3970-174">In the **Check In – Source Files** dialog box, type a comment, and then click **Check In**.</span></span>

<span data-ttu-id="d3970-175">此时，已将解决方案的外部依赖项添加到源代码管理中。</span><span class="sxs-lookup"><span data-stu-id="d3970-175">At this point, you have added the external dependencies for your solution to source control.</span></span>

## <a name="conclusion"></a><span data-ttu-id="d3970-176">结束语</span><span class="sxs-lookup"><span data-stu-id="d3970-176">Conclusion</span></span>

<span data-ttu-id="d3970-177">本主题介绍了如何连接到团队项目、映射文件夹结构，以及如何将内容添加到源代码管理。</span><span class="sxs-lookup"><span data-stu-id="d3970-177">This topic described how to connect to a team project, map a folder structure, and add content to source control.</span></span> <span data-ttu-id="d3970-178">有关如何处理源代码管理下的项的详细信息，请参阅[使用版本控制](https://msdn.microsoft.com/library/ms181368.aspx)。</span><span class="sxs-lookup"><span data-stu-id="d3970-178">For more information on how to work with items under source control, see [Using Version Control](https://msdn.microsoft.com/library/ms181368.aspx).</span></span>

<span data-ttu-id="d3970-179">下一主题：[配置用于 Web 部署的 Tfs 生成服务器](configuring-a-tfs-build-server-for-web-deployment.md)，介绍如何准备 Tfs Team build 服务器来构建和部署解决方案。</span><span class="sxs-lookup"><span data-stu-id="d3970-179">The next topic, [Configuring a TFS Build Server for Web Deployment](configuring-a-tfs-build-server-for-web-deployment.md), describes how to prepare a TFS Team Build server to build and deploy your solution.</span></span>

## <a name="further-reading"></a><span data-ttu-id="d3970-180">其他阅读材料</span><span class="sxs-lookup"><span data-stu-id="d3970-180">Further Reading</span></span>

<span data-ttu-id="d3970-181">有关在 TFS 中使用源代码管理的更全面的信息，请参阅[使用版本控制](https://msdn.microsoft.com/library/ms181368.aspx)。</span><span class="sxs-lookup"><span data-stu-id="d3970-181">For more comprehensive information on working with source control in TFS, see [Using Version Control](https://msdn.microsoft.com/library/ms181368.aspx).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="d3970-182">[上一页](creating-a-team-project-in-tfs.md)
> [下一页](configuring-a-tfs-build-server-for-web-deployment.md)</span><span class="sxs-lookup"><span data-stu-id="d3970-182">[Previous](creating-a-team-project-in-tfs.md)
[Next](configuring-a-tfs-build-server-for-web-deployment.md)</span></span>

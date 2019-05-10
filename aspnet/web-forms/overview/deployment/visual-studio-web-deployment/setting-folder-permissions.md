---
uid: web-forms/overview/deployment/visual-studio-web-deployment/setting-folder-permissions
title: 使用 Visual Studio 的 ASP.NET Web 部署：设置文件夹权限 |Microsoft Docs
author: tdykstra
description: 本系列教程演示如何部署 （发布） ASP.NET web 应用程序到 Azure 应用服务 Web 应用或第三方托管提供商，通过使用...
ms.author: riande
ms.date: 02/15/2013
ms.assetid: 9715a121-fa55-4f1b-a5d2-fb3f6cd8be8f
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/setting-folder-permissions
msc.type: authoredcontent
ms.openlocfilehash: f25182f3f841c963866319dd934c0c28b4eb95b0
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/06/2019
ms.locfileid: "65112894"
---
# <a name="aspnet-web-deployment-using-visual-studio-setting-folder-permissions"></a><span data-ttu-id="809fa-103">使用 Visual Studio 的 ASP.NET Web 部署：设置文件夹权限</span><span class="sxs-lookup"><span data-stu-id="809fa-103">ASP.NET Web Deployment using Visual Studio: Setting Folder Permissions</span></span>

<span data-ttu-id="809fa-104">通过[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="809fa-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="809fa-105">下载初学者项目</span><span class="sxs-lookup"><span data-stu-id="809fa-105">Download Starter Project</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=282627)

> <span data-ttu-id="809fa-106">本系列教程演示如何部署 （发布） ASP.NET web 应用程序到 Azure 应用服务 Web 应用或第三方托管提供商，通过使用 Visual Studio 2012 或 Visual Studio 2010。</span><span class="sxs-lookup"><span data-stu-id="809fa-106">This tutorial series shows you how to deploy (publish) an ASP.NET web application to Azure App Service Web Apps or to a third-party hosting provider, by using Visual Studio 2012 or Visual Studio 2010.</span></span> <span data-ttu-id="809fa-107">有关序列的信息，请参阅[系列中的第一个教程](introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="809fa-107">For information about the series, see [the first tutorial in the series](introduction.md).</span></span>

## <a name="overview"></a><span data-ttu-id="809fa-108">概述</span><span class="sxs-lookup"><span data-stu-id="809fa-108">Overview</span></span>

<span data-ttu-id="809fa-109">在本教程中，设置文件夹的权限*Elmah*文件夹中已部署的 web 站点，以便应用程序可以在该文件夹中创建日志文件。</span><span class="sxs-lookup"><span data-stu-id="809fa-109">In this tutorial, you set folder permissions for the *Elmah* folder in the deployed web site so that the application can create log files in that folder.</span></span>

<span data-ttu-id="809fa-110">在 Visual Studio 中使用 Visual Studio 开发服务器 (Cassini) 或 IIS Express 测试 web 应用程序时，应用程序在你的身份下运行。</span><span class="sxs-lookup"><span data-stu-id="809fa-110">When you test a web application in Visual Studio using the Visual Studio Development Server (Cassini) or IIS Express, the application runs under your identity.</span></span> <span data-ttu-id="809fa-111">在开发计算机上最有可能是管理员并具有完整权限对任何文件夹中的任何文件执行任何操作。</span><span class="sxs-lookup"><span data-stu-id="809fa-111">You are most likely an administrator on your development computer and have full authority to do anything to any file in any folder.</span></span> <span data-ttu-id="809fa-112">但在 IIS 下运行应用程序，它将运行下定义为站点分配给应用程序池的标识。</span><span class="sxs-lookup"><span data-stu-id="809fa-112">But when an application runs under IIS, it runs under the identity defined for the application pool that the site is assigned to.</span></span> <span data-ttu-id="809fa-113">这通常是具有有限的权限的系统定义的帐户。</span><span class="sxs-lookup"><span data-stu-id="809fa-113">This is typically a system-defined account that has limited permissions.</span></span> <span data-ttu-id="809fa-114">默认情况下它具有读取和执行权限，对 web 应用程序的文件和文件夹，但它没有写访问权限。</span><span class="sxs-lookup"><span data-stu-id="809fa-114">By default it has read and execute permissions on your web application's files and folders, but it doesn't have write access.</span></span>

<span data-ttu-id="809fa-115">如果你的应用程序创建或更新文件，这是一种常见需要在 web 应用程序中，这将成为一个问题。</span><span class="sxs-lookup"><span data-stu-id="809fa-115">This becomes an issue if your application creates or updates files, which is a common need in web applications.</span></span> <span data-ttu-id="809fa-116">在 Contoso 大学应用程序，Elmah 将创建 XML 文件中的*Elmah*文件夹，以便保存有关错误的详细信息。</span><span class="sxs-lookup"><span data-stu-id="809fa-116">In the Contoso University application, Elmah creates XML files in the *Elmah* folder in order to save details about errors.</span></span> <span data-ttu-id="809fa-117">即使不使用类似于 Elmah 的内容，你的站点可能会让用户将文件上传或执行其他任务将数据写入到你网站的文件夹中。</span><span class="sxs-lookup"><span data-stu-id="809fa-117">Even if you don't use something like Elmah, your site might let users upload files or perform other tasks that write data to a folder in your site.</span></span>

<span data-ttu-id="809fa-118">提醒：如果收到错误消息或某些操作无法按完成以下教程，请务必检查[故障排除页](troubleshooting.md)。</span><span class="sxs-lookup"><span data-stu-id="809fa-118">Reminder: If you get an error message or something doesn't work as you go through the tutorial, be sure to check the [troubleshooting page](troubleshooting.md).</span></span>

## <a name="test-error-logging-and-reporting"></a><span data-ttu-id="809fa-119">测试错误日志记录和报告</span><span class="sxs-lookup"><span data-stu-id="809fa-119">Test error logging and reporting</span></span>

<span data-ttu-id="809fa-120">若要查看如何应用程序不能正常工作在 IIS 中 （尽管它未在 Visual Studio 中测试时），可能会导致一个错误，通常会由 Elmah 记录，然后打开 Elmah 错误日志，以查看详细信息。</span><span class="sxs-lookup"><span data-stu-id="809fa-120">To see how the application doesn't work correctly in IIS (although it did when you tested it in Visual Studio), you can cause an error that would normally be logged by Elmah, and then open the Elmah error log to see the details.</span></span> <span data-ttu-id="809fa-121">如果 Elmah 不能创建一个 XML 文件和存储的错误详细信息，您将看到一个空的错误报告。</span><span class="sxs-lookup"><span data-stu-id="809fa-121">If Elmah was unable to create an XML file and store the error details, you see an empty error report.</span></span>

<span data-ttu-id="809fa-122">打开浏览器并转到`http://localhost/ContosoUniversity`，然后请求无效的 URL，如*Studentsxxx.aspx*。</span><span class="sxs-lookup"><span data-stu-id="809fa-122">Open a browser and go to `http://localhost/ContosoUniversity`, and then request an invalid URL like *Studentsxxx.aspx*.</span></span> <span data-ttu-id="809fa-123">请参阅而不是系统生成的错误页面*GenericErrorPage.aspx*页，因为`customErrors`Web.config 文件中的设置为"RemoteOnly"并本地运行 IIS:</span><span class="sxs-lookup"><span data-stu-id="809fa-123">You see a system-generated error page instead of the *GenericErrorPage.aspx* page because the `customErrors` setting in the Web.config file is "RemoteOnly" and you are running IIS locally:</span></span>

![HTTP 404 错误页面](setting-folder-permissions/_static/image1.png)

<span data-ttu-id="809fa-125">现在，运行*Elmah.axd*以查看错误报告。</span><span class="sxs-lookup"><span data-stu-id="809fa-125">Now run *Elmah.axd* to see the error report.</span></span> <span data-ttu-id="809fa-126">使用管理员帐户凭据登录之后 (&quot;管理员&quot;并&quot;devpwd&quot;)，因为 Elmah 无法创建 XML 文件中的，您会看到一个空错误日志页面*Elmah*文件夹：</span><span class="sxs-lookup"><span data-stu-id="809fa-126">After you log in with the administrator account credentials (&quot;admin&quot; and &quot;devpwd&quot;), you see an empty error log page because Elmah was unable to create an XML file in the *Elmah* folder:</span></span>

![错误日志为空](setting-folder-permissions/_static/image2.png)

## <a name="set-write-permission-on-the-elmah-folder"></a><span data-ttu-id="809fa-128">Elmah 文件夹上设置的写入权限</span><span class="sxs-lookup"><span data-stu-id="809fa-128">Set write permission on the Elmah folder</span></span>

<span data-ttu-id="809fa-129">可以手动设置文件夹权限，或使其自动部署过程的一部分。</span><span class="sxs-lookup"><span data-stu-id="809fa-129">You can set folder permissions manually or you can make it an automatic part of the deployment process.</span></span> <span data-ttu-id="809fa-130">使其自动需要复杂的 MSBuild 代码，以及由于仅需要执行此操作，第一次部署，以下的步骤如何手动执行该操作。</span><span class="sxs-lookup"><span data-stu-id="809fa-130">Making it automatic requires complex MSBuild code, and since you only have to do this the first time you deploy, the following steps how to do it manually.</span></span> <span data-ttu-id="809fa-131">(有关如何使部署过程的此部分的信息，请参阅[设置文件夹权限 Web 发布](http://sedodream.com/2011/11/08/SettingFolderPermissionsOnWebPublish.aspx)Sayed Hashimi 的博客上。)</span><span class="sxs-lookup"><span data-stu-id="809fa-131">(For information about how to make this part of the deployment process, see [Setting Folder Permissions on Web Publish](http://sedodream.com/2011/11/08/SettingFolderPermissionsOnWebPublish.aspx) on Sayed Hashimi's blog.)</span></span>

1. <span data-ttu-id="809fa-132">在中**文件资源管理器**，导航到*C:\inetpub\wwwroot\ContosoUniversity*。</span><span class="sxs-lookup"><span data-stu-id="809fa-132">In **File Explorer**, navigate to *C:\inetpub\wwwroot\ContosoUniversity*.</span></span> <span data-ttu-id="809fa-133">右键单击*Elmah*文件夹，选择**属性**，然后选择**安全**选项卡。</span><span class="sxs-lookup"><span data-stu-id="809fa-133">Right-click the *Elmah* folder, select **Properties**, and then select the **Security** tab.</span></span>
2. <span data-ttu-id="809fa-134">单击“编辑” 。</span><span class="sxs-lookup"><span data-stu-id="809fa-134">Click **Edit**.</span></span>
3. <span data-ttu-id="809fa-135">在中**Elmah 的权限**对话框中，选择**DefaultAppPool**，然后选择**编写**中的复选框**允许**列。</span><span class="sxs-lookup"><span data-stu-id="809fa-135">In the **Permissions for Elmah** dialog box, select **DefaultAppPool**, and then select the **Write** check box in the **Allow** column.</span></span>

    ![ELMAH 文件夹的权限](setting-folder-permissions/_static/image3.png)

    <span data-ttu-id="809fa-137">(如果看不到**DefaultAppPool**中**组或用户名**列表中，您大概是用一个指定在本教程中的其他某种方法在您的计算机上设置了 IIS 和 ASP.NET 4。</span><span class="sxs-lookup"><span data-stu-id="809fa-137">(If you don't see **DefaultAppPool** in the **Group or user names** list, you probably used some other method than the one specified in this tutorial to set up IIS and ASP.NET 4 on your computer.</span></span> <span data-ttu-id="809fa-138">在这种情况下，找出哪些标识由分配给 Contoso 大学应用程序，并向该标识授予写入权限的应用程序池。</span><span class="sxs-lookup"><span data-stu-id="809fa-138">In that case, find out what identity is used by the application pool assigned to the Contoso University application, and grant write permission to that identity.</span></span> <span data-ttu-id="809fa-139">请参阅有关应用程序池标识链接在本教程末尾。）单击**确定**中这两个对话框。</span><span class="sxs-lookup"><span data-stu-id="809fa-139">See the links about application pool identities at the end of this tutorial.) Click **OK** in both dialog boxes.</span></span>

## <a name="retest-error-logging-and-reporting"></a><span data-ttu-id="809fa-140">重新测试错误日志记录和报告</span><span class="sxs-lookup"><span data-stu-id="809fa-140">Retest error logging and reporting</span></span>

<span data-ttu-id="809fa-141">通过再次导致错误 （请求错误 URL） 的相同方式来测试和运行**错误日志**页。</span><span class="sxs-lookup"><span data-stu-id="809fa-141">Test by causing an error again in the same way (request a bad URL) and run the **Error Log** page.</span></span> <span data-ttu-id="809fa-142">这一次在页面上会出现错误。</span><span class="sxs-lookup"><span data-stu-id="809fa-142">This time the error appears on the page.</span></span>

![ELMAH 错误日志页](setting-folder-permissions/_static/image4.png)

## <a name="summary"></a><span data-ttu-id="809fa-144">总结</span><span class="sxs-lookup"><span data-stu-id="809fa-144">Summary</span></span>

<span data-ttu-id="809fa-145">您现在已经完成全部的 Contoso University 所需的任务在 IIS 中正常运行在本地计算机上。</span><span class="sxs-lookup"><span data-stu-id="809fa-145">You have now completed all of the tasks necessary to get Contoso University working correctly in IIS on your local computer.</span></span> <span data-ttu-id="809fa-146">在下一步的教程中，将在站点公开用于通过将其部署到 Azure。</span><span class="sxs-lookup"><span data-stu-id="809fa-146">In the next tutorial, you will make the site publicly available by deploying it to Azure.</span></span>

## <a name="more-information"></a><span data-ttu-id="809fa-147">详细信息</span><span class="sxs-lookup"><span data-stu-id="809fa-147">More information</span></span>

<span data-ttu-id="809fa-148">在此示例中，Elmah 为何无法保存日志文件的原因是相当明显。</span><span class="sxs-lookup"><span data-stu-id="809fa-148">In this example, the reason why Elmah was unable to save log files was fairly obvious.</span></span> <span data-ttu-id="809fa-149">可以在不那么明显; 问题原因的情况下使用 IIS 跟踪请参阅[故障排除失败的请求使用跟踪在 IIS 7 中](https://www.iis.net/learn/troubleshoot/using-failed-request-tracing/troubleshooting-failed-requests-using-tracing-in-iis)IIS.net 站点上。</span><span class="sxs-lookup"><span data-stu-id="809fa-149">You can use IIS tracing in cases where the cause of the problem is not so obvious; see [Troubleshooting Failed Requests Using Tracing in IIS 7](https://www.iis.net/learn/troubleshoot/using-failed-request-tracing/troubleshooting-failed-requests-using-tracing-in-iis) on the IIS.net site.</span></span>

<span data-ttu-id="809fa-150">有关如何向应用程序池标识授予权限的详细信息，请参阅[应用程序池标识](https://www.iis.net/learn/manage/configuring-security/application-pool-identities)并[在文件系统 Acl 通过 IIS 安全内容](https://www.iis.net/learn/get-started/planning-for-security/secure-content-in-iis-through-file-system-acls)IIS.net 站点上。</span><span class="sxs-lookup"><span data-stu-id="809fa-150">For more information about how to grant permissions to application pool identities, see [Application Pool Identities](https://www.iis.net/learn/manage/configuring-security/application-pool-identities) and [Secure Content in IIS Through File System ACLs](https://www.iis.net/learn/get-started/planning-for-security/secure-content-in-iis-through-file-system-acls) on the IIS.net site.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="809fa-151">[上一页](deploying-to-iis.md)
> [下一页](deploying-to-production.md)</span><span class="sxs-lookup"><span data-stu-id="809fa-151">[Previous](deploying-to-iis.md)
[Next](deploying-to-production.md)</span></span>

---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-to-production
title: 使用 Visual Studio 的 ASP.NET Web 部署：部署到生产 |Microsoft Docs
author: tdykstra
description: 本系列教程介绍了如何通过来将 ASP.NET web 应用程序部署（发布）到 Azure App Service Web 应用或第三方托管提供程序。
ms.author: riande
ms.date: 02/15/2013
ms.assetid: 416438a1-3b2f-4d27-bf53-6b76223c33bf
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-to-production
msc.type: authoredcontent
ms.openlocfilehash: ec025e757d00cbfbfbcda9408739d2593908bc07
ms.sourcegitcommit: 0cf7d06071a8ff986e6c028ac9daf0c0e7490412
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/23/2020
ms.locfileid: "85240627"
---
# <a name="aspnet-web-deployment-using-visual-studio-deploying-to-production"></a><span data-ttu-id="4cd97-103">使用 Visual Studio 的 ASP.NET Web 部署：部署到生产环境</span><span class="sxs-lookup"><span data-stu-id="4cd97-103">ASP.NET Web Deployment using Visual Studio: Deploying to Production</span></span>

<span data-ttu-id="4cd97-104">作者： [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="4cd97-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="4cd97-105">下载初学者项目</span><span class="sxs-lookup"><span data-stu-id="4cd97-105">Download Starter Project</span></span>](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> <span data-ttu-id="4cd97-106">本系列教程介绍了如何使用 Visual Studio 2012 或 Visual Studio 2010，将 ASP.NET web 应用程序部署（发布）到 Azure App Service Web 应用或第三方托管提供商。</span><span class="sxs-lookup"><span data-stu-id="4cd97-106">This tutorial series shows you how to deploy (publish) an ASP.NET web application to Azure App Service Web Apps or to a third-party hosting provider, by using Visual Studio 2012 or Visual Studio 2010.</span></span> <span data-ttu-id="4cd97-107">有关序列的信息，请参阅本[系列中的第一个教程](introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="4cd97-107">For information about the series, see [the first tutorial in the series](introduction.md).</span></span>

## <a name="overview"></a><span data-ttu-id="4cd97-108">概述</span><span class="sxs-lookup"><span data-stu-id="4cd97-108">Overview</span></span>

<span data-ttu-id="4cd97-109">在本教程中，您将设置一个 Microsoft Azure 帐户，创建过渡和生产环境，并使用 Visual Studio 一键式发布功能将 ASP.NET web 应用程序部署到过渡环境和生产环境。</span><span class="sxs-lookup"><span data-stu-id="4cd97-109">In this tutorial, you set up a Microsoft Azure account, create staging and production environments, and deploy your ASP.NET web application to the staging and production environments by using the Visual Studio one-click publish feature.</span></span>

<span data-ttu-id="4cd97-110">如果愿意，可以部署到第三方托管提供商。</span><span class="sxs-lookup"><span data-stu-id="4cd97-110">If you prefer, you can deploy to a third-party hosting provider.</span></span> <span data-ttu-id="4cd97-111">本教程中所述的大多数过程对于宿主提供程序或 Azure 都是相同的，只不过每个提供程序都有自己的用户界面用于帐户和网站管理。</span><span class="sxs-lookup"><span data-stu-id="4cd97-111">Most of the procedures described in this tutorial are the same for a hosting provider or for Azure, except that each provider has its own user interface for account and web site management.</span></span> <span data-ttu-id="4cd97-112">可以在 Microsoft.com 网站上的[提供程序库](https://www.microsoft.com/web/hosting)中找到宿主提供程序。</span><span class="sxs-lookup"><span data-stu-id="4cd97-112">You can find a hosting provider in the [gallery of providers](https://www.microsoft.com/web/hosting) on the Microsoft.com web site.</span></span>

<span data-ttu-id="4cd97-113">提醒：如果你收到一条错误消息或在你完成本教程时无法正常工作，请务必查看本系列教程中的故障排除页。</span><span class="sxs-lookup"><span data-stu-id="4cd97-113">Reminder: If you get an error message or something doesn't work as you go through the tutorial, be sure to check the Troubleshooting page in this tutorial series.</span></span>

## <a name="get-a-microsoft-azure-account"></a><span data-ttu-id="4cd97-114">获取 Microsoft Azure 帐户</span><span class="sxs-lookup"><span data-stu-id="4cd97-114">Get a Microsoft Azure account</span></span>

<span data-ttu-id="4cd97-115">如果还没有 Azure 帐户，只需花费几分钟就能创建一个免费试用帐户。</span><span class="sxs-lookup"><span data-stu-id="4cd97-115">If you don't already have an Azure account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="4cd97-116">有关详细信息，请参阅 [Azure 免费试用](https://azure.microsoft.com/free/dotnet/)。</span><span class="sxs-lookup"><span data-stu-id="4cd97-116">For details, see [Azure Free Trial](https://azure.microsoft.com/free/dotnet/).</span></span>

## <a name="create-a-staging-environment"></a><span data-ttu-id="4cd97-117">创建过渡环境</span><span class="sxs-lookup"><span data-stu-id="4cd97-117">Create a staging environment</span></span>

> [!NOTE]
> <span data-ttu-id="4cd97-118">由于本教程已编写，因此 Azure App Service 添加了一项新功能来自动执行许多创建过渡和生产环境的过程。</span><span class="sxs-lookup"><span data-stu-id="4cd97-118">Since this tutorial was written, Azure App Service added a new feature to automate many of the processes for creating staging and production environments.</span></span> <span data-ttu-id="4cd97-119">请参阅[在 Azure App Service 中设置 web 应用的过渡环境](https://azure.microsoft.com/documentation/articles/web-sites-staged-publishing/)。</span><span class="sxs-lookup"><span data-stu-id="4cd97-119">See [Set up staging environments for web apps in Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-staged-publishing/).</span></span>

<span data-ttu-id="4cd97-120">如[部署到测试环境教程](deploying-to-iis.md)中所述，最可靠的测试环境是托管提供商的网站，就像生产网站一样。</span><span class="sxs-lookup"><span data-stu-id="4cd97-120">As explained in the [Deploy to the Test Environment tutorial](deploying-to-iis.md), the most reliable test environment is a web site at the hosting provider that's just like the production web site.</span></span> <span data-ttu-id="4cd97-121">在许多托管提供商上，你必须权衡此项的优势以增加额外成本，但在 Azure 中，可以创建其他免费的 web 应用作为暂存应用。</span><span class="sxs-lookup"><span data-stu-id="4cd97-121">At many hosting providers you would have to weigh the benefits of this against significant additional cost, but in Azure you can create an additional free web app as your staging app.</span></span> <span data-ttu-id="4cd97-122">你还需要一个数据库，而超出生产数据库的费用的额外费用将是 "无" 或 "最小"。</span><span class="sxs-lookup"><span data-stu-id="4cd97-122">You also need a database, and the additional expense for that over the expense of your production database will be either none or minimal.</span></span> <span data-ttu-id="4cd97-123">在 Azure 中，你需要为你使用的数据库存储量（而不是每个数据库）付费，并且你将在暂存中使用的额外存储量将是最小值。</span><span class="sxs-lookup"><span data-stu-id="4cd97-123">In Azure you pay for the amount of database storage you use rather than for each database, and the amount of additional storage you'll use in staging will be minimal.</span></span>

<span data-ttu-id="4cd97-124">如[部署到测试环境教程](deploying-to-iis.md)中所述，在过渡和生产环境中，你要将两个数据库部署到一个数据库中。</span><span class="sxs-lookup"><span data-stu-id="4cd97-124">As explained in the [Deploy to the Test Environment tutorial](deploying-to-iis.md), in staging and production you're going to deploy your two databases into one database.</span></span> <span data-ttu-id="4cd97-125">如果您想要将它们分开，则该过程是相同的，只是您为每个环境创建了一个附加数据库，并在创建发布配置文件时为每个数据库选择正确的目标字符串。</span><span class="sxs-lookup"><span data-stu-id="4cd97-125">If you wanted to keep them separate, the process would be the same except that you'd create an additional database for each environment and you would select the correct destination string for each database when you create the publish profile.</span></span>

<span data-ttu-id="4cd97-126">在本教程的此部分中，你将创建用于过渡环境的 web 应用和数据库，并在创建并部署到生产环境之前，部署到此处进行过渡和测试。</span><span class="sxs-lookup"><span data-stu-id="4cd97-126">In this section of the tutorial you'll create a web app and database to use for the staging environment, and you'll deploy to staging and test there before creating and deploying to the production environment.</span></span>

> [!NOTE]
> <span data-ttu-id="4cd97-127">以下步骤演示如何使用 Azure 管理门户在 Azure App Service 中创建 web 应用。</span><span class="sxs-lookup"><span data-stu-id="4cd97-127">The following steps show how to create a web app in Azure App Service by using the Azure management portal.</span></span> <span data-ttu-id="4cd97-128">在最新版本的 Azure SDK 中，你还可以通过使用服务器资源管理器，无需离开 Visual Studio 即可实现此目的。</span><span class="sxs-lookup"><span data-stu-id="4cd97-128">In the latest version of the Azure SDK, you can also do this without leaving Visual Studio, by using Server Explorer.</span></span> <span data-ttu-id="4cd97-129">在 Visual Studio 2013 中，还可以直接从 "发布" 对话框创建一个 web 应用。</span><span class="sxs-lookup"><span data-stu-id="4cd97-129">In Visual Studio 2013, you can also create a web app directly from the Publish dialog.</span></span> <span data-ttu-id="4cd97-130">有关详细信息，请参阅[在 Azure App Service 中创建 ASP.NET web 应用。](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet)</span><span class="sxs-lookup"><span data-stu-id="4cd97-130">For more information, see [Create an ASP.NET web app in Azure App Service.](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet)</span></span>

1. <span data-ttu-id="4cd97-131">在[Azure 管理门户](https://manage.windowsazure.com/)中，单击 "**网站**"，然后单击 "**新建**"。</span><span class="sxs-lookup"><span data-stu-id="4cd97-131">In the [Azure Management Portal](https://manage.windowsazure.com/), click **Websites**, and then click **New**.</span></span>
2. <span data-ttu-id="4cd97-132">单击 "**网站**"，然后单击 "**自定义创建**"。</span><span class="sxs-lookup"><span data-stu-id="4cd97-132">Click **Website**, and then click **Custom Create**.</span></span>

    <span data-ttu-id="4cd97-133">**新网站-"自定义创建**" 向导将打开。</span><span class="sxs-lookup"><span data-stu-id="4cd97-133">The **New Website - Custom Create** wizard opens.</span></span> <span data-ttu-id="4cd97-134">使用 "**自定义创建**" 向导，您可以同时创建网站和数据库。</span><span class="sxs-lookup"><span data-stu-id="4cd97-134">The **Custom Create** wizard enables you to create a web site and a database at the same time.</span></span>
3. <span data-ttu-id="4cd97-135">在向导的 "**创建网站**" 步骤中，在 " **URL** " 框中输入一个字符串，用作应用程序过渡环境的唯一 URL。</span><span class="sxs-lookup"><span data-stu-id="4cd97-135">In the **Create Website** step of the wizard, enter a string in the **URL** box to use as the unique URL for your application's staging environment.</span></span> <span data-ttu-id="4cd97-136">例如，输入 ContosoUniversity-staging123 （在末尾添加随机数，以使其在 ContosoUniversity 的情况下是唯一的）。</span><span class="sxs-lookup"><span data-stu-id="4cd97-136">For example, enter ContosoUniversity-staging123 (including random numbers at the end to make it unique in case ContosoUniversity-staging is taken).</span></span>

    <span data-ttu-id="4cd97-137">完整的 URL 将包含你在此处输入的内容和你在文本框旁边看到的后缀。</span><span class="sxs-lookup"><span data-stu-id="4cd97-137">The complete URL will consist of what you enter here plus the suffix that you see next to the text box.</span></span>
4. <span data-ttu-id="4cd97-138">在 "**区域**" 下拉列表中，选择离你最近的区域。</span><span class="sxs-lookup"><span data-stu-id="4cd97-138">In the **Region** drop-down list, choose the region that is closest to you.</span></span>

    <span data-ttu-id="4cd97-139">此设置指定 web 应用将在哪个数据中心运行。</span><span class="sxs-lookup"><span data-stu-id="4cd97-139">This setting specifies which data center your web app will run in.</span></span>
5. <span data-ttu-id="4cd97-140">在 "**数据库**" 下拉列表中，选择 "**创建新的 SQL 数据库**"。</span><span class="sxs-lookup"><span data-stu-id="4cd97-140">In the **Database** drop-down list, choose **Create a new SQL database**.</span></span>
6. <span data-ttu-id="4cd97-141">在 "**数据库连接字符串名称**" 框中，保留默认值*DefaultConnection*。</span><span class="sxs-lookup"><span data-stu-id="4cd97-141">In the **DB Connection String Name** box, leave the default value, *DefaultConnection*.</span></span>
7. <span data-ttu-id="4cd97-142">单击对话框底部的向右箭头。</span><span class="sxs-lookup"><span data-stu-id="4cd97-142">Click the arrow that points to the right at the bottom of the box.</span></span>

    <span data-ttu-id="4cd97-143">下图显示了 "**创建网站**" 对话框，其中包含示例值。</span><span class="sxs-lookup"><span data-stu-id="4cd97-143">The following illustration shows the **Create Website** dialog with sample values in it.</span></span> <span data-ttu-id="4cd97-144">你输入的 URL 和区域将不同。</span><span class="sxs-lookup"><span data-stu-id="4cd97-144">The URL and Region that you have entered will be different.</span></span>

    ![创建网站步骤](deploying-to-production/_static/image1.png)

    <span data-ttu-id="4cd97-146">向导转到 "**指定数据库设置**" 步骤。</span><span class="sxs-lookup"><span data-stu-id="4cd97-146">The wizard advances to the **Specify database settings** step.</span></span>
8. <span data-ttu-id="4cd97-147">在 "**名称**" 框中，输入*ContosoUniversity*和随机数以使其唯一，例如*ContosoUniversity123*。</span><span class="sxs-lookup"><span data-stu-id="4cd97-147">In the **Name** box, enter *ContosoUniversity* plus a random number to make it unique, for example *ContosoUniversity123*.</span></span>
9. <span data-ttu-id="4cd97-148">在 "**服务器**" 框中，选择 "**新建 SQL 数据库服务器**"。</span><span class="sxs-lookup"><span data-stu-id="4cd97-148">In the **Server** box, select **New SQL Database Server**.</span></span>
10. <span data-ttu-id="4cd97-149">输入管理员名称和密码。</span><span class="sxs-lookup"><span data-stu-id="4cd97-149">Enter an administrator name and password.</span></span>

    <span data-ttu-id="4cd97-150">此处未输入现有名称和密码。</span><span class="sxs-lookup"><span data-stu-id="4cd97-150">You aren't entering an existing name and password here.</span></span> <span data-ttu-id="4cd97-151">需要输入新的名称和密码，这些名称和密码需要现在定义，供以后访问数据库时使用。</span><span class="sxs-lookup"><span data-stu-id="4cd97-151">You're entering a new name and password that you're defining now to use later when you access the database.</span></span>
11. <span data-ttu-id="4cd97-152">在 "**区域**" 框中，选择为 web 应用选择的相同区域。</span><span class="sxs-lookup"><span data-stu-id="4cd97-152">In the **Region** box, choose the same region that you chose for the web app.</span></span>

    <span data-ttu-id="4cd97-153">将 web 服务器和数据库服务器保留在同一区域可以获得最佳性能并最大限度地减少费用。</span><span class="sxs-lookup"><span data-stu-id="4cd97-153">Keeping the web server and the database server in the same region gives you the best performance and minimizes expenses.</span></span>
12. <span data-ttu-id="4cd97-154">单击框底部的复选标记以指示你已完成。</span><span class="sxs-lookup"><span data-stu-id="4cd97-154">Click the check mark at the bottom of the box to indicate that you're finished.</span></span>

    <span data-ttu-id="4cd97-155">下图显示了 "**指定数据库设置**" 对话框，其中包含示例值。</span><span class="sxs-lookup"><span data-stu-id="4cd97-155">The following illustration shows the **Specify database settings** dialog with sample values in it.</span></span> <span data-ttu-id="4cd97-156">输入的值可能不同。</span><span class="sxs-lookup"><span data-stu-id="4cd97-156">The values you have entered may be different.</span></span>

    !["新建网站-与数据库一起创建" 向导的 "数据库设置" 步骤](deploying-to-production/_static/image2.png)

    <span data-ttu-id="4cd97-158">管理门户返回到 "网站" 页面，"**状态**" 列显示正在创建的 web 应用。</span><span class="sxs-lookup"><span data-stu-id="4cd97-158">The Management Portal returns to the Websites page, and the **Status** column shows that the web app is being created.</span></span> <span data-ttu-id="4cd97-159">经过一段时间（通常不到一分钟），"**状态**" 列会显示已成功创建 web 应用。</span><span class="sxs-lookup"><span data-stu-id="4cd97-159">After a while (typically less than a minute), the **Status** column shows that the web app was successfully created.</span></span> <span data-ttu-id="4cd97-160">在左侧的导航栏中，在 "**网站**" 图标旁边会显示你的帐户中拥有的 web 应用的数目，并且数据库的数目将显示在 " **SQL 数据库**" 图标旁边。</span><span class="sxs-lookup"><span data-stu-id="4cd97-160">In the navigation bar at the left, the number of web apps you have in your account appears next to the **Websites** icon, and the number of databases appears next to the **SQL Databases** icon.</span></span>

    ![管理门户的网站页面，网站已创建](deploying-to-production/_static/image3.png)

    <span data-ttu-id="4cd97-162">你的 web 应用名称将不同于图中的示例应用。</span><span class="sxs-lookup"><span data-stu-id="4cd97-162">Your web app name will be different from the example app in the illustration.</span></span>

## <a name="deploy-the-application-to-staging"></a><span data-ttu-id="4cd97-163">将应用程序部署到过渡环境</span><span class="sxs-lookup"><span data-stu-id="4cd97-163">Deploy the application to staging</span></span>

<span data-ttu-id="4cd97-164">现在，你已创建用于过渡环境的 web 应用和数据库，接下来可以将项目部署到该环境中。</span><span class="sxs-lookup"><span data-stu-id="4cd97-164">Now that you have created a web app and database for the staging environment, you can deploy the project to it.</span></span>

> [!NOTE]
> <span data-ttu-id="4cd97-165">这些说明演示如何通过下载 *.publishsettings*文件来创建发布配置文件，该文件不仅适用于 Azure，还适用于第三方托管提供商。</span><span class="sxs-lookup"><span data-stu-id="4cd97-165">These instructions show how to create a publish profile by downloading a *.publishsettings* file, which works not only for Azure but also for third-party hosting providers.</span></span> <span data-ttu-id="4cd97-166">使用最新的 Azure SDK，你还可以从 Visual Studio 直接连接到 Azure，并从你的 Azure 帐户中的 web 应用列表中进行选择。</span><span class="sxs-lookup"><span data-stu-id="4cd97-166">The latest Azure SDK also enables you to connect directly to Azure from Visual Studio, and choose from a list of web apps that you have in your Azure account.</span></span> <span data-ttu-id="4cd97-167">在 Visual Studio 2013 中，可以从**Web 发布**对话框或从**服务器资源管理器**窗口登录到 Azure。</span><span class="sxs-lookup"><span data-stu-id="4cd97-167">In Visual Studio 2013, you can sign in to Azure from the **Web Publish** dialog or from the **Server Explorer** window.</span></span> <span data-ttu-id="4cd97-168">有关详细信息，请参阅[在 Azure App Service 中创建 ASP.NET web 应用](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet)。</span><span class="sxs-lookup"><span data-stu-id="4cd97-168">For more information, see [Create an ASP.NET web app in Azure App Service](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet).</span></span>

### <a name="download-the-publishsettings-file"></a><span data-ttu-id="4cd97-169">下载 .publishsettings 文件</span><span class="sxs-lookup"><span data-stu-id="4cd97-169">Download the .publishsettings file</span></span>

1. <span data-ttu-id="4cd97-170">单击刚刚创建的 web 应用的名称。</span><span class="sxs-lookup"><span data-stu-id="4cd97-170">Click the name of the web app that you just created.</span></span>

    ![单击该站点以切换到仪表板](deploying-to-production/_static/image4.png)
2. <span data-ttu-id="4cd97-172">在 "**仪表板**" 选项卡的 "**速览**" 下，单击 "**下载发布配置文件**"。</span><span class="sxs-lookup"><span data-stu-id="4cd97-172">Under **Quick glance** in the **Dashboard** tab, click **Download publish profile**.</span></span>

    ![下载发布配置文件链接](deploying-to-production/_static/image5.png)

    <span data-ttu-id="4cd97-174">此步骤将下载一个文件，其中包含将应用程序部署到 web 应用所需的所有设置。</span><span class="sxs-lookup"><span data-stu-id="4cd97-174">This step downloads a file that contains all of the settings that you need in order to deploy an application to your web app.</span></span> <span data-ttu-id="4cd97-175">您将此文件导入到 Visual Studio 中，这样您就不必手动输入此信息。</span><span class="sxs-lookup"><span data-stu-id="4cd97-175">You'll import this file into Visual Studio so you don't have to enter this information manually.</span></span>
3. <span data-ttu-id="4cd97-176">将 *.publishsettings*文件保存在可从 Visual Studio 访问的文件夹中。</span><span class="sxs-lookup"><span data-stu-id="4cd97-176">Save the *.publishsettings* file in a folder that you can access from Visual Studio.</span></span>

    ![保存 .publishsettings 文件](deploying-to-production/_static/image6.png)

    > [!WARNING]
    > <span data-ttu-id="4cd97-178">安全性- *.publishsettings*文件包含用于管理 Azure 订阅和服务的凭据（未编码）。</span><span class="sxs-lookup"><span data-stu-id="4cd97-178">Security - The *.publishsettings* file contains your credentials (unencoded) that are used to administer your Azure subscriptions and services.</span></span> <span data-ttu-id="4cd97-179">确保此文件安全的最佳做法是，将其暂时存储在源目录的外部（例如存储在 Libraries\Documents 文件夹中），然后在完成导入后将其删除。</span><span class="sxs-lookup"><span data-stu-id="4cd97-179">The security best practice for this file is to store it temporarily outside your source directories (for example in the Libraries\Documents folder), and then delete it once the import has completed.</span></span> <span data-ttu-id="4cd97-180">获得 *.publishsettings*文件访问权的恶意用户可以编辑、创建和删除你的 Azure 服务。</span><span class="sxs-lookup"><span data-stu-id="4cd97-180">A malicious user who gains access to the *.publishsettings* file can edit, create, and delete your Azure services.</span></span>

### <a name="create-a-publish-profile"></a><span data-ttu-id="4cd97-181">创建发布配置文件</span><span class="sxs-lookup"><span data-stu-id="4cd97-181">Create a publish profile</span></span>

1. <span data-ttu-id="4cd97-182">在 Visual Studio 中，右键单击**解决方案资源管理器**中的 ContosoUniversity 项目，然后从上下文菜单中选择 "**发布**"。</span><span class="sxs-lookup"><span data-stu-id="4cd97-182">In Visual Studio, right-click the ContosoUniversity project in **Solution Explorer** and select **Publish** from the context menu.</span></span>

    <span data-ttu-id="4cd97-183">“发布 Web”向导随即打开。\*\*\*\*</span><span class="sxs-lookup"><span data-stu-id="4cd97-183">The **Publish Web** wizard opens.</span></span>
2. <span data-ttu-id="4cd97-184">单击“配置文件”选项卡。\*\*\*\*</span><span class="sxs-lookup"><span data-stu-id="4cd97-184">Click the **Profile** tab.</span></span>
3. <span data-ttu-id="4cd97-185">单击“导入”。</span><span class="sxs-lookup"><span data-stu-id="4cd97-185">Click **Import**.</span></span>
4. <span data-ttu-id="4cd97-186">导航到之前下载的 *.publishsettings*文件，然后单击 "**打开**"。</span><span class="sxs-lookup"><span data-stu-id="4cd97-186">Navigate to the *.publishsettings* file you downloaded earlier, and then click **Open**.</span></span>

    !["导入发布设置" 对话框](deploying-to-production/_static/image7.png)
5. <span data-ttu-id="4cd97-188">在 "**连接**" 选项卡中，单击 "**验证连接**" 确保设置正确。</span><span class="sxs-lookup"><span data-stu-id="4cd97-188">In the **Connection** tab, click **Validate Connection** to make sure that the settings are correct.</span></span>

    <span data-ttu-id="4cd97-189">验证连接后，"**验证连接**" 按钮旁边会显示一个绿色复选标记。</span><span class="sxs-lookup"><span data-stu-id="4cd97-189">When the connection has been validated, a green check mark is shown next to the **Validate Connection** button.</span></span>

    <span data-ttu-id="4cd97-190">对于某些宿主提供程序，单击 "**验证连接**" 时，可能会看到 "**证书错误**" 对话框。</span><span class="sxs-lookup"><span data-stu-id="4cd97-190">For some hosting providers, when you click **Validate Connection**, you might see a **Certificate Error** dialog box.</span></span> <span data-ttu-id="4cd97-191">如果执行此操作，请验证服务器名称是否与预期的相同。</span><span class="sxs-lookup"><span data-stu-id="4cd97-191">If you do, verify that the server name is what you expect.</span></span> <span data-ttu-id="4cd97-192">如果服务器名称正确，请选择 "**为 Visual Studio 的未来会话保存此证书**"，然后单击 "**接受**"。</span><span class="sxs-lookup"><span data-stu-id="4cd97-192">If the server name is correct, select **Save this certificate for future sessions of Visual Studio** and click **Accept**.</span></span> <span data-ttu-id="4cd97-193">（此错误意味着宿主提供程序已选择避免为你要部署到的 URL 购买 SSL 证书。</span><span class="sxs-lookup"><span data-stu-id="4cd97-193">(This error means that the hosting provider has chosen to avoid the expense of purchasing an SSL certificate for the URL that you are deploying to.</span></span> <span data-ttu-id="4cd97-194">如果你希望使用有效的证书建立安全连接，请与你的托管提供商联系。）</span><span class="sxs-lookup"><span data-stu-id="4cd97-194">If you prefer to establish a secure connection by using a valid certificate, contact your hosting provider.)</span></span>
6. <span data-ttu-id="4cd97-195">单击“下一步”。</span><span class="sxs-lookup"><span data-stu-id="4cd97-195">Click **Next**.</span></span>

    ![“连接”选项卡中的连接成功图标和“下一步”按钮](deploying-to-production/_static/image8.png)
7. <span data-ttu-id="4cd97-197">在 "**设置**" 选项卡中，展开 "**文件发布选项**"，然后**从 "应用程序 \_ 数据" 文件夹中选择 "排除文件"**。</span><span class="sxs-lookup"><span data-stu-id="4cd97-197">In the **Settings** tab, expand **File Publish Options**, and then select **Exclude files from the App\_Data folder**.</span></span>

    <span data-ttu-id="4cd97-198">有关 "**文件发布选项**" 下的其他选项的信息，请参阅[部署到 IIS](deploying-to-iis.md)教程。</span><span class="sxs-lookup"><span data-stu-id="4cd97-198">For information about the other options under **File Publish Options**, see the [deploying to IIS](deploying-to-iis.md) tutorial.</span></span> <span data-ttu-id="4cd97-199">在数据库配置步骤结束时，显示此步骤的结果和以下数据库配置步骤的屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="4cd97-199">The screen shot that shows the result of this step and the following database configuration steps is at the end of the database configuration steps.</span></span>
8. <span data-ttu-id="4cd97-200">在 "**数据库**" 部分的 " **DefaultConnection** " 下，为成员资格数据库配置数据库部署。</span><span class="sxs-lookup"><span data-stu-id="4cd97-200">Under **DefaultConnection** in the **Databases** section, configure database deployment for the membership database.</span></span>
9. 1. <span data-ttu-id="4cd97-201">选择 "**更新数据库**"。</span><span class="sxs-lookup"><span data-stu-id="4cd97-201">Select **Update database**.</span></span>

        <span data-ttu-id="4cd97-202">直接在**DefaultConnection**下的 "**远程连接字符串**" 框中填充了来自 .publishsettings 文件的连接字符串。连接字符串包含 SQL Server 凭据，这些凭据以纯文本形式存储在 *.pubxml*文件中。</span><span class="sxs-lookup"><span data-stu-id="4cd97-202">The **Remote connection string** box directly below **DefaultConnection** is filled in with the connection string from the .publishsettings file.The connection string includes SQL Server credentials, which are stored in plain text in the *.pubxml* file.</span></span> <span data-ttu-id="4cd97-203">如果不想将它们永久存储在该数据库中，则可以在部署数据库后将它们从发布配置文件中删除并将其存储在 Azure 中。</span><span class="sxs-lookup"><span data-stu-id="4cd97-203">If you prefer not to store them permanently there, you can remove them from the publish profile after the database is deployed and store them in Azure instead.</span></span> <span data-ttu-id="4cd97-204">有关详细信息，请参阅在 Scott Hanselman 的博客上[从 ASP.NET 部署到 Azure 时如何保证你的数据库连接字符串的安全性](http://www.hanselman.com/blog/HowToKeepYourASPNETDatabaseConnectionStringsSecureWhenDeployingToAzureFromSource.aspx)。</span><span class="sxs-lookup"><span data-stu-id="4cd97-204">For more information, see [How to keep your ASP.NET database connection strings secure when deploying to Azure from Source](http://www.hanselman.com/blog/HowToKeepYourASPNETDatabaseConnectionStringsSecureWhenDeployingToAzureFromSource.aspx) on Scott Hanselman's blog.</span></span>
      2. <span data-ttu-id="4cd97-205">单击 "**配置数据库更新**"。</span><span class="sxs-lookup"><span data-stu-id="4cd97-205">Click **Configure database updates**.</span></span>
      3. <span data-ttu-id="4cd97-206">在 "**配置数据库更新**" 对话框中，单击 "**添加 SQL 脚本**"。</span><span class="sxs-lookup"><span data-stu-id="4cd97-206">In the **Configure Database Updates** dialog box, click **Add SQL Script**.</span></span>
      4. <span data-ttu-id="4cd97-207">在 "**添加 SQL 脚本**" 框中，导航到之前在 "解决方案" 文件夹中保存的*aspnet-data-prod*脚本，然后单击 "**打开**"。</span><span class="sxs-lookup"><span data-stu-id="4cd97-207">In the **Add SQL Script** box, navigate to the *aspnet-data-prod.sql* script that you saved earlier in the solution folder, and then click **Open**.</span></span>
      5. <span data-ttu-id="4cd97-208">关闭 "**配置数据库更新**" 对话框。</span><span class="sxs-lookup"><span data-stu-id="4cd97-208">Close the **Configure Database Updates** dialog box.</span></span>
10. <span data-ttu-id="4cd97-209">在 "**数据库**" 部分的 " **SchoolContext** " 下，选择 "**执行 Code First 迁移（在应用程序启动时运行）**。</span><span class="sxs-lookup"><span data-stu-id="4cd97-209">Under **SchoolContext** in the **Databases** section, select **Execute Code First Migrations (runs on application start)**.</span></span>

    <span data-ttu-id="4cd97-210">Visual Studio 显示**Execute Code First 迁移**，而不是类的**Update 数据库** `DbContext` 。</span><span class="sxs-lookup"><span data-stu-id="4cd97-210">Visual Studio displays **Execute Code First Migrations** instead of **Update Database** for `DbContext` classes.</span></span> <span data-ttu-id="4cd97-211">如果要使用 dbDacFx 提供程序（而不是迁移）来部署通过使用类访问的数据库 `DbContext` ，请参阅 MSDN 上的 Visual Studio 的 Web 部署常见问题和 ASP.NET 中的[如何实现部署不迁移的 Code First 数据库？](https://msdn.microsoft.com/library/ee942158.aspx#deploy_code_first_without_migrations)</span><span class="sxs-lookup"><span data-stu-id="4cd97-211">If you want to use the dbDacFx provider instead of Migrations to deploy a database that you access by using a `DbContext` class, see [How do I deploy a Code First database without Migrations?](https://msdn.microsoft.com/library/ee942158.aspx#deploy_code_first_without_migrations) in the Web Deployment FAQ for Visual Studio and ASP.NET on MSDN.</span></span>

    <span data-ttu-id="4cd97-212">"**设置**" 选项卡现在类似于以下示例：</span><span class="sxs-lookup"><span data-stu-id="4cd97-212">The **Settings** tab now looks like the following example:</span></span>

    ![暂存的 "设置" 选项卡](deploying-to-production/_static/image9.png)
11. <span data-ttu-id="4cd97-214">执行以下步骤以保存配置文件并将其重命名为*暂存*：</span><span class="sxs-lookup"><span data-stu-id="4cd97-214">Perform the following steps to save the profile and rename it to *Staging*:</span></span>

    1. <span data-ttu-id="4cd97-215">单击 "**配置文件**" 选项卡，然后单击 "**管理配置文件**"。</span><span class="sxs-lookup"><span data-stu-id="4cd97-215">Click the **Profile** tab, and then click **Manage Profiles**.</span></span>
    2. <span data-ttu-id="4cd97-216">导入创建了两个新配置文件，一个用于 FTP，另一个用于 Web 部署。</span><span class="sxs-lookup"><span data-stu-id="4cd97-216">The import created two new profiles, one for FTP and one for Web Deploy.</span></span> <span data-ttu-id="4cd97-217">你已配置 Web 部署配置文件：将此配置文件重命名为 "*暂存*"。</span><span class="sxs-lookup"><span data-stu-id="4cd97-217">You configured the Web Deploy profile: rename this profile to *Staging*.</span></span>

        ![将配置文件重命名为暂存](deploying-to-production/_static/image10.png)
    3. <span data-ttu-id="4cd97-219">关闭 "**编辑 Web 发布配置文件**" 对话框。</span><span class="sxs-lookup"><span data-stu-id="4cd97-219">Close the **Edit Web Publish Profiles** dialog box.</span></span>
    4. <span data-ttu-id="4cd97-220">关闭 "**发布 Web** " 向导。</span><span class="sxs-lookup"><span data-stu-id="4cd97-220">Close the **Publish Web** wizard.</span></span>

### <a name="configure-a-publish-profile-transform-for-the-environment-indicator"></a><span data-ttu-id="4cd97-221">为环境指示器配置发布配置文件转换</span><span class="sxs-lookup"><span data-stu-id="4cd97-221">Configure a publish profile transform for the environment indicator</span></span>

> [!NOTE]
> <span data-ttu-id="4cd97-222">本部分说明如何设置环境指示器的 Web.config 转换。</span><span class="sxs-lookup"><span data-stu-id="4cd97-222">This section shows how to set up a Web.config transform for the environment indicator.</span></span> <span data-ttu-id="4cd97-223">因为指示器位于元素中，所以在 `<appSettings>` 部署到 Azure App Service 时，可以使用另一种方法来指定转换。</span><span class="sxs-lookup"><span data-stu-id="4cd97-223">Because the indicator is in the `<appSettings>` element, you have another alternative for specifying the transformation when you're deploying to Azure App Service.</span></span> <span data-ttu-id="4cd97-224">有关详细信息，请参阅[在 Azure 中指定 Web.config 设置](web-config-transformations.md#watransforms)。</span><span class="sxs-lookup"><span data-stu-id="4cd97-224">For more information, see [Specifying Web.config settings in Azure](web-config-transformations.md#watransforms).</span></span>

1. <span data-ttu-id="4cd97-225">在**解决方案资源管理器**中，展开 "**属性**"，然后展开**PublishProfiles**。</span><span class="sxs-lookup"><span data-stu-id="4cd97-225">In **Solution Explorer**, expand **Properties**, and then expand **PublishProfiles**.</span></span>
2. <span data-ttu-id="4cd97-226">右键单击 " *.pubxml*"，然后单击 "**添加配置转换**"。</span><span class="sxs-lookup"><span data-stu-id="4cd97-226">Right-click *Staging.pubxml*, and then click **Add Config Transform**.</span></span>

    ![为暂存添加配置转换](deploying-to-production/_static/image11.png)

    <span data-ttu-id="4cd97-228">Visual Studio 将创建*Web.Staging.config*转换文件并将其打开。</span><span class="sxs-lookup"><span data-stu-id="4cd97-228">Visual Studio creates the *Web.Staging.config* transform file and opens it.</span></span>
3. <span data-ttu-id="4cd97-229">在*Web.Staging.config*转换文件中，将以下代码插入到紧随开始 `configuration` 标记的后面。</span><span class="sxs-lookup"><span data-stu-id="4cd97-229">In the *Web.Staging.config* transform file, insert the following code immediately after the opening `configuration` tag.</span></span>

    [!code-xml[Main](deploying-to-production/samples/sample1.xml)]

    <span data-ttu-id="4cd97-230">当使用过渡发布配置文件时，此转换会将环境指示器设置为 "生产"。</span><span class="sxs-lookup"><span data-stu-id="4cd97-230">When you use the Staging publish profile, this transform sets the environment indicator to "Prod".</span></span> <span data-ttu-id="4cd97-231">在已部署的 web 应用中，你将看不到任何后缀，如 "Contoso 大学" H1 标题后面的 "（开发人员）" 或 "（测试）"。</span><span class="sxs-lookup"><span data-stu-id="4cd97-231">In the deployed web app, you won't see any suffix such as "(Dev)" or "(Test)" after the "Contoso University" H1 heading.</span></span>
4. <span data-ttu-id="4cd97-232">右键单击*Web.Staging.config*文件，然后单击 "**预览转换**"，以确保编码的转换会生成预期的更改。</span><span class="sxs-lookup"><span data-stu-id="4cd97-232">Right-click the *Web.Staging.config* file and click **Preview Transform** to make sure that the transform you coded produces the expected changes.</span></span>

    <span data-ttu-id="4cd97-233">**Web.config 预览**"窗口显示应用*Web.Release.config*转换和*Web.Staging.config*转换的结果。</span><span class="sxs-lookup"><span data-stu-id="4cd97-233">The **Web.config Preview** window shows the result of applying both the *Web.Release.config* transforms and the *Web.Staging.config* transforms.</span></span>

### <a name="prevent-public-use-of-the-test-app"></a><span data-ttu-id="4cd97-234">阻止公共使用测试应用</span><span class="sxs-lookup"><span data-stu-id="4cd97-234">Prevent public use of the test app</span></span>

<span data-ttu-id="4cd97-235">过渡应用程序的一个重要注意事项是它将在 Internet 上出现，但您不希望公开使用它。</span><span class="sxs-lookup"><span data-stu-id="4cd97-235">An important consideration for the staging app is that it will be live on the Internet, but you don't want the public to use it.</span></span> <span data-ttu-id="4cd97-236">若要最大程度地减少用户查找和使用它的可能性，可以使用以下一种或多种方法：</span><span class="sxs-lookup"><span data-stu-id="4cd97-236">To minimize the likelihood that people will find and use it, you can use one or more of the following methods:</span></span>

- <span data-ttu-id="4cd97-237">设置防火墙规则，仅允许从用于测试暂存的 IP 地址访问过渡应用。</span><span class="sxs-lookup"><span data-stu-id="4cd97-237">Set firewall rules that allow access to the staging app only from IP addresses that you use to test staging.</span></span>
- <span data-ttu-id="4cd97-238">使用不可能猜到的经过模糊处理的 URL。</span><span class="sxs-lookup"><span data-stu-id="4cd97-238">Use an obfuscated URL that would be impossible to guess.</span></span>
- <span data-ttu-id="4cd97-239">创建一个*robots.txt*文件，以确保搜索引擎不会对测试应用进行爬网，并在搜索结果中向其报告链接。</span><span class="sxs-lookup"><span data-stu-id="4cd97-239">Create a *robots.txt* file to ensure that search engines will not crawl the test app and report links to it in search results.</span></span>

<span data-ttu-id="4cd97-240">这些方法中的第一种方法是最有效的，但在本教程中不涉及，因为这将要求你部署到 Azure 云服务而不是 Azure App Service。</span><span class="sxs-lookup"><span data-stu-id="4cd97-240">The first of these methods is the most effective but is not covered in this tutorial because it would require that you deploy to an Azure Cloud Service instead of Azure App Service.</span></span> <span data-ttu-id="4cd97-241">有关 Azure 中的云服务和 IP 限制的详细信息，请参阅[Azure 提供的计算托管选项](https://docs.microsoft.com/azure/cloud-services/cloud-services-choose-me)和[阻止特定 IP 地址访问 Web 角色](https://msdn.microsoft.com/library/windowsazure/jj154098.aspx)。</span><span class="sxs-lookup"><span data-stu-id="4cd97-241">For more information about Cloud Services and IP restrictions in Azure, see [Compute Hosting Options Provided by Azure](https://docs.microsoft.com/azure/cloud-services/cloud-services-choose-me) and [Block Specific IP Addresses from Accessing a Web Role](https://msdn.microsoft.com/library/windowsazure/jj154098.aspx).</span></span> <span data-ttu-id="4cd97-242">如果要部署到第三方托管提供商，请与提供商联系，以了解如何实现 IP 限制。</span><span class="sxs-lookup"><span data-stu-id="4cd97-242">If you are deploying to a third-party hosting provider, contact the provider to find out how to implement IP restrictions.</span></span>

<span data-ttu-id="4cd97-243">在本教程中，您将创建一个*robots.txt*文件。</span><span class="sxs-lookup"><span data-stu-id="4cd97-243">For this tutorial, you'll create a *robots.txt* file.</span></span>

1. <span data-ttu-id="4cd97-244">在**解决方案资源管理器**中，右键单击 ContosoUniversity 项目，然后单击 "**添加新项**"。</span><span class="sxs-lookup"><span data-stu-id="4cd97-244">In **Solution Explorer**, right-click the ContosoUniversity project and click **Add New Item**.</span></span>
2. <span data-ttu-id="4cd97-245">创建一个名为 " *robots.txt*" 的新**文本文件**，并在其中添加以下文本：</span><span class="sxs-lookup"><span data-stu-id="4cd97-245">Create a new **Text File** named *robots.txt*, and put the following text in it:</span></span>

    [!code-console[Main](deploying-to-production/samples/sample2.cmd)]

    <span data-ttu-id="4cd97-246">`User-agent`该行通知搜索引擎文件中的规则适用于所有搜索引擎 web 爬网程序（机器人）， `Disallow` 行指定不应爬网网站上的任何页面。</span><span class="sxs-lookup"><span data-stu-id="4cd97-246">The `User-agent` line tells search engines that the rules in the file apply to all search engine web crawlers (robots), and the `Disallow` line specifies that no pages on the site should be crawled.</span></span>

    <span data-ttu-id="4cd97-247">你确实希望搜索引擎为你的生产应用程序编目，因此你需要从生产部署中排除此文件。</span><span class="sxs-lookup"><span data-stu-id="4cd97-247">You do want search engines to catalog your production app, so you need to exclude this file from production deployment.</span></span> <span data-ttu-id="4cd97-248">为此，你将在创建生产发布配置文件时配置其设置。</span><span class="sxs-lookup"><span data-stu-id="4cd97-248">To do that, you'll configure a setting in the Production publish profile when you create it.</span></span>

### <a name="deploy-to-staging"></a><span data-ttu-id="4cd97-249">部署到过渡环境</span><span class="sxs-lookup"><span data-stu-id="4cd97-249">Deploy to staging</span></span>

1. <span data-ttu-id="4cd97-250">右键单击 Contoso 大学项目，然后单击 "**发布**"，打开 "**发布 Web** " 向导。</span><span class="sxs-lookup"><span data-stu-id="4cd97-250">Open the **Publish Web** wizard by right-clicking the Contoso University project and clicking **Publish**.</span></span>
2. <span data-ttu-id="4cd97-251">请确保选择了**暂存**配置文件。</span><span class="sxs-lookup"><span data-stu-id="4cd97-251">Make sure that the **Staging** profile is selected.</span></span>
3. <span data-ttu-id="4cd97-252">单击“发布” 。</span><span class="sxs-lookup"><span data-stu-id="4cd97-252">Click **Publish**.</span></span>

    <span data-ttu-id="4cd97-253">“输出”窗口会显示已执行的部署操作并报告部署的成功完成。\*\*\*\*</span><span class="sxs-lookup"><span data-stu-id="4cd97-253">The **Output** window shows what deployment actions were taken and reports successful completion of the deployment.</span></span> <span data-ttu-id="4cd97-254">默认浏览器会自动打开到已部署的 web 应用的 URL。</span><span class="sxs-lookup"><span data-stu-id="4cd97-254">The default browser automatically opens to the URL of the deployed web app.</span></span>

## <a name="test-in-the-staging-environment"></a><span data-ttu-id="4cd97-255">在过渡环境中测试</span><span class="sxs-lookup"><span data-stu-id="4cd97-255">Test in the staging environment</span></span>

<span data-ttu-id="4cd97-256">请注意，环境指示器不存在（"（测试）" 或 "（Dev）" 在 H1 标题之后，这表明环境指示器的*Web.config*转换已成功。</span><span class="sxs-lookup"><span data-stu-id="4cd97-256">Notice that the environment indicator is absent (there is no "(Test)" or "(Dev)" after the H1 heading, which shows that the *Web.config* transformation for the environment indicator was successful.</span></span>

![主页过渡](deploying-to-production/_static/image12.png)

<span data-ttu-id="4cd97-258">运行 "**学生**" 页，验证部署的数据库是否没有学生。</span><span class="sxs-lookup"><span data-stu-id="4cd97-258">Run the **Students** page to verify that the deployed database has no students.</span></span>

<span data-ttu-id="4cd97-259">运行**讲师**页，验证 Code First 用指导员数据对数据库进行种子设定：</span><span class="sxs-lookup"><span data-stu-id="4cd97-259">Run the **Instructors** page to verify that Code First seeded the database with instructor data:</span></span>

<span data-ttu-id="4cd97-260">从 "**学生**" 菜单中选择 "**添加学生**"，添加一个学生，然后在 "**学生**" 页中查看新学生，验证是否可以成功写入到数据库。</span><span class="sxs-lookup"><span data-stu-id="4cd97-260">Select **Add Students** from the **Students** menu, add a student, and then view the new student in the **Students** page to verify that you can successfully write to the database.</span></span>

<span data-ttu-id="4cd97-261">在 "**课程**" 页上，单击 "**更新信用**"。</span><span class="sxs-lookup"><span data-stu-id="4cd97-261">From the **Courses** page, click **Update Credits**.</span></span> <span data-ttu-id="4cd97-262">**更新信用**页面需要管理员权限，因此将显示 "**登录**" 页。</span><span class="sxs-lookup"><span data-stu-id="4cd97-262">The **Update Credits** page requires administrator permissions, so the **Log In** page is displayed.</span></span> <span data-ttu-id="4cd97-263">输入先前创建的管理员帐户凭据（"admin" 和 "prodpwd"）。</span><span class="sxs-lookup"><span data-stu-id="4cd97-263">Enter the administrator account credentials that you created earlier ("admin" and "prodpwd").</span></span> <span data-ttu-id="4cd97-264">此时将显示 "**更新信用**" 页，该页面验证你在上一教程中创建的管理员帐户是否已正确部署到测试环境中。</span><span class="sxs-lookup"><span data-stu-id="4cd97-264">The **Update Credits** page is displayed, which verifies that the administrator account that you created in the previous tutorial was correctly deployed to the test environment.</span></span>

<span data-ttu-id="4cd97-265">请求一个无效的 URL 来导致 ELMAH 将跟踪的错误，然后请求 ELMAH 错误报告。</span><span class="sxs-lookup"><span data-stu-id="4cd97-265">Request an invalid URL to cause an error that ELMAH will track, and then request the ELMAH error report.</span></span> <span data-ttu-id="4cd97-266">如果要部署到第三方托管提供程序，则可能会发现报表为空，原因是在上一教程中，此报表为空。</span><span class="sxs-lookup"><span data-stu-id="4cd97-266">If you are deploying to a third-party hosting provider, you will probably find that the report is empty for the same reason that it was empty in the previous tutorial.</span></span> <span data-ttu-id="4cd97-267">你将需要使用宿主提供程序的帐户管理工具来配置文件夹权限，以允许 ELMAH 写入日志文件夹。</span><span class="sxs-lookup"><span data-stu-id="4cd97-267">You will have to use the hosting provider's account management tools to configure folder permissions to enable ELMAH to write to the log folder.</span></span>

<span data-ttu-id="4cd97-268">你创建的应用程序现在在云中的 web 应用中运行，就像你将用于生产的应用程序一样。</span><span class="sxs-lookup"><span data-stu-id="4cd97-268">The application that you created is now running in the cloud in a web app that is just like what you will use for production.</span></span> <span data-ttu-id="4cd97-269">由于一切都能正常运行，因此下一步是部署到生产环境。</span><span class="sxs-lookup"><span data-stu-id="4cd97-269">Since everything is working correctly, the next step is to deploy to production.</span></span>

## <a name="deploy-to-production"></a><span data-ttu-id="4cd97-270">部署到生产</span><span class="sxs-lookup"><span data-stu-id="4cd97-270">Deploy to production</span></span>

<span data-ttu-id="4cd97-271">除了需要从部署中排除*robots.txt*之外，创建生产 web 应用并将其部署到生产的过程与用于过渡的过程相同。</span><span class="sxs-lookup"><span data-stu-id="4cd97-271">The process for creating a production web app and deploying to production is the same as for staging, except that you need to exclude the *robots.txt* from deployment.</span></span> <span data-ttu-id="4cd97-272">为此，你将编辑发布配置文件。</span><span class="sxs-lookup"><span data-stu-id="4cd97-272">To do that you'll edit the publish profile file.</span></span>

### <a name="create-the-production-environment-and-the-production-publish-profile"></a><span data-ttu-id="4cd97-273">创建生产环境和生产发布配置文件</span><span class="sxs-lookup"><span data-stu-id="4cd97-273">Create the production environment and the production publish profile</span></span>

1. <span data-ttu-id="4cd97-274">按照用于过渡的相同过程，在 Azure 中创建生产 web 应用和数据库。</span><span class="sxs-lookup"><span data-stu-id="4cd97-274">Create the production web app and database in Azure, following the same procedure that you used for staging.</span></span>

    <span data-ttu-id="4cd97-275">创建数据库时，可以选择将其放在之前创建的同一服务器上，或创建新服务器。</span><span class="sxs-lookup"><span data-stu-id="4cd97-275">When you create the database, you can choose to put it on the same server you created earlier, or create a new server.</span></span>
2. <span data-ttu-id="4cd97-276">下载 *.publishsettings*文件。</span><span class="sxs-lookup"><span data-stu-id="4cd97-276">Download the *.publishsettings* file.</span></span>
3. <span data-ttu-id="4cd97-277">通过导入 *.publishsettings*文件来创建发布配置文件，遵循用于过渡的相同过程。</span><span class="sxs-lookup"><span data-stu-id="4cd97-277">Create the publish profile by importing the production *.publishsettings* file, following the same procedure that you used for staging.</span></span>

    <span data-ttu-id="4cd97-278">别忘了在 "**设置**" 选项卡的 "**数据库**" 部分中的**DefaultConnection**下配置数据部署脚本。</span><span class="sxs-lookup"><span data-stu-id="4cd97-278">Don't forget to configure the data deployment script under **DefaultConnection** in the **Databases** section of the **Settings** tab.</span></span>
4. <span data-ttu-id="4cd97-279">将发布配置文件重命名为 "*生产*"。</span><span class="sxs-lookup"><span data-stu-id="4cd97-279">Rename the publish profile to *Production*.</span></span>
5. <span data-ttu-id="4cd97-280">按照用于过渡的相同过程，为环境指示器配置发布配置文件转换。</span><span class="sxs-lookup"><span data-stu-id="4cd97-280">Configure a publish profile transform for the environment indicator, following the same procedure that you used for staging..</span></span>

### <a name="edit-the-pubxml-file-to-exclude-robotstxt"></a><span data-ttu-id="4cd97-281">编辑 .pubxml 文件以排除 robots.txt</span><span class="sxs-lookup"><span data-stu-id="4cd97-281">Edit the .pubxml file to exclude robots.txt</span></span>

<span data-ttu-id="4cd97-282">发布配置文件的名称为 &lt; profilename &gt; *. .Pubxml* ，位于*PublishProfiles*文件夹中。</span><span class="sxs-lookup"><span data-stu-id="4cd97-282">Publish profile files are named &lt;profilename&gt;*.pubxml* and are located in the *PublishProfiles* folder.</span></span> <span data-ttu-id="4cd97-283">*PublishProfiles*文件夹位于 c # web 应用程序项目中的 "*属性*" 文件夹下、VB web 应用程序项目的 "*我的项目*" 文件夹下或 Web 应用项目中的 "*应用 \_ 数据*" 文件夹下。</span><span class="sxs-lookup"><span data-stu-id="4cd97-283">The *PublishProfiles* folder is under the *Properties* folder in a C# web application project, under the *My Project* folder in a VB web application project, or under the *App\_Data* folder in a web app project.</span></span> <span data-ttu-id="4cd97-284">每个 *.pubxml*文件都包含适用于一个发布配置文件的设置。</span><span class="sxs-lookup"><span data-stu-id="4cd97-284">Each *.pubxml* file contains settings that apply to one publish profile.</span></span> <span data-ttu-id="4cd97-285">您在 "发布 Web" 向导中输入的值存储在这些文件中，您可以对其进行编辑以创建或更改不能在 Visual Studio UI 中使用的设置。</span><span class="sxs-lookup"><span data-stu-id="4cd97-285">The values you enter in the Publish Web wizard are stored in these files, and you can edit them to create or change settings that aren't made available in the Visual Studio UI.</span></span>

<span data-ttu-id="4cd97-286">默认情况下，当你创建发布配置文件时， *.pubxml*文件包含在项目中，但你可以将其从项目中排除，Visual Studio 仍将使用它们。</span><span class="sxs-lookup"><span data-stu-id="4cd97-286">By default, *.pubxml* files are included in the project when you create a publish profile, but you can exclude them from the project and Visual Studio will still use them.</span></span> <span data-ttu-id="4cd97-287">Visual Studio 将在*PublishProfiles*文件夹中查找 *.pubxml*文件，无论它们是否包含在项目中。</span><span class="sxs-lookup"><span data-stu-id="4cd97-287">Visual Studio looks in the *PublishProfiles* folder for *.pubxml* files, regardless of whether they are included in the project.</span></span>

<span data-ttu-id="4cd97-288">对于每个 *.pubxml*文件，都有一个 *.pubxml*文件。</span><span class="sxs-lookup"><span data-stu-id="4cd97-288">For each *.pubxml* file there is a *.pubxml.user* file.</span></span> <span data-ttu-id="4cd97-289">如果选择了 "**保存密码**" 选项，则 *.pubxml*文件将包含加密密码，并且默认情况下会将其从项目中排除。</span><span class="sxs-lookup"><span data-stu-id="4cd97-289">The *.pubxml.user* file contains the encrypted password if you selected the **Save password** option, and by default it is excluded from the project.</span></span>

<span data-ttu-id="4cd97-290">*.Pubxml*文件包含与特定发布配置文件相关的设置。</span><span class="sxs-lookup"><span data-stu-id="4cd97-290">A *.pubxml* file contains the settings that pertain to a specific publish profile.</span></span> <span data-ttu-id="4cd97-291">如果要配置适用于所有配置文件的设置，则可以创建一个 *. .targets*文件。</span><span class="sxs-lookup"><span data-stu-id="4cd97-291">If you want to configure settings that apply to all profiles, you can create a *.wpp.targets* file.</span></span> <span data-ttu-id="4cd97-292">生成过程会将这些文件导入 *.csproj*或 *.vbproj*项目文件中，因此可以在这些文件中配置可在项目文件中配置的大多数设置。</span><span class="sxs-lookup"><span data-stu-id="4cd97-292">The build process imports these files into the *.csproj* or *.vbproj* project file, so most settings that you can configure in the project file can be configured in these files.</span></span> <span data-ttu-id="4cd97-293">有关 *.pubxml* *文件和 .pubxml 文件的*详细信息，请参阅[如何：在发布配置文件中编辑部署设置（.）文件和 Visual Studio Web 项目中的文件](https://msdn.microsoft.com/library/ff398069.aspx)。</span><span class="sxs-lookup"><span data-stu-id="4cd97-293">For more information about *.pubxml* files and *.wpp.targets* files, see [How to: Edit Deployment Settings in Publish Profile (.pubxml) Files and the .wpp.targets File in Visual Studio Web Projects](https://msdn.microsoft.com/library/ff398069.aspx).</span></span>

1. <span data-ttu-id="4cd97-294">在**解决方案资源管理器**中，展开 "**属性**"，然后展开**PublishProfiles**。</span><span class="sxs-lookup"><span data-stu-id="4cd97-294">In **Solution Explorer**, expand **Properties** and expand **PublishProfiles**.</span></span>
2. <span data-ttu-id="4cd97-295">右键单击 " *.pubxml* "，然后单击 "**打开**"。</span><span class="sxs-lookup"><span data-stu-id="4cd97-295">Right-click *Production.pubxml* and click **Open**.</span></span>

    ![打开 .pubxml 文件](deploying-to-production/_static/image13.png)
3. <span data-ttu-id="4cd97-297">右键单击 " *.pubxml* "，然后单击 "**打开**"。</span><span class="sxs-lookup"><span data-stu-id="4cd97-297">Right-click *Production.pubxml* and click **Open**.</span></span>
4. <span data-ttu-id="4cd97-298">紧靠在结束元素之前添加以下行 `PropertyGroup` ：</span><span class="sxs-lookup"><span data-stu-id="4cd97-298">Add the following lines immediately before the closing `PropertyGroup` element:</span></span>

    [!code-xml[Main](deploying-to-production/samples/sample3.xml)]

    <span data-ttu-id="4cd97-299">.Pubxml 文件现在如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="4cd97-299">The .pubxml file now looks like the following example:</span></span>

    [!code-xml[Main](deploying-to-production/samples/sample4.xml?highlight=18-20)]

    <span data-ttu-id="4cd97-300">有关如何排除文件和文件夹的详细信息，请参阅 MSDN 上的**Visual Studio 和 ASP.NET 的 Web 部署常见问题解答**中的 "[能否从部署中排除特定文件或文件夹"](https://msdn.microsoft.com/library/ee942158.aspx#can_i_exclude_specific_files_or_folders_from_deployment) 。</span><span class="sxs-lookup"><span data-stu-id="4cd97-300">For more information about how to exclude files and folders, see [Can I exclude specific files or folders from deployment?](https://msdn.microsoft.com/library/ee942158.aspx#can_i_exclude_specific_files_or_folders_from_deployment) in the **Web Deployment FAQ for Visual Studio and ASP.NET** on MSDN.</span></span>

### <a name="deploy-to-production"></a><span data-ttu-id="4cd97-301">部署到生产</span><span class="sxs-lookup"><span data-stu-id="4cd97-301">Deploy to production</span></span>

1. <span data-ttu-id="4cd97-302">打开 "**发布 Web** " 向导，确保已选择 "**生产**发布配置文件"，然后单击 "**预览**" 选项卡上的 "**开始预览**" 以验证是否不会将*robots.txt*文件复制到生产应用。</span><span class="sxs-lookup"><span data-stu-id="4cd97-302">Open the **Publish Web** wizard make sure that the **Production** publish profile is selected, and then click **Start Preview** on the **Preview** tab to verify that the *robots.txt* file will not be copied to the production app.</span></span>

    ![要发布到生产的文件预览](deploying-to-production/_static/image14.png)

    <span data-ttu-id="4cd97-304">查看要复制的文件的列表。</span><span class="sxs-lookup"><span data-stu-id="4cd97-304">Review the list of files that will be copied.</span></span> <span data-ttu-id="4cd97-305">你将看到所有 *.cs*文件，包括*aspx.cs*、 *. aspx.designer.cs*、 *Master.cs*和*Master.designer.cs*文件。</span><span class="sxs-lookup"><span data-stu-id="4cd97-305">You'll see that all of the *.cs* files, including *.aspx.cs*, *.aspx.designer.cs*, *Master.cs*, and *Master.designer.cs* files are omitted.</span></span> <span data-ttu-id="4cd97-306">所有此代码都已编译到*ContosoUniversity.dll*和*ContosoUniversity*文件中，这些文件将在*bin*文件夹中找到。</span><span class="sxs-lookup"><span data-stu-id="4cd97-306">All of this code has been compiled into the *ContosoUniversity.dll* and *ContosoUniversity.pdb* files that you'll find in the *bin* folder.</span></span> <span data-ttu-id="4cd97-307">由于只需要 *.dll*来运行应用程序，并且您之前指定仅应部署运行应用程序所需的文件，因此，不会将 *.cs*文件复制到目标环境。</span><span class="sxs-lookup"><span data-stu-id="4cd97-307">Because only the *.dll* is needed to run the application, and you specified earlier that only files needed to run the application should be deployed, no *.cs* files were copied to the destination environment.</span></span> <span data-ttu-id="4cd97-308">由于相同的原因，将省略*obj*文件夹和*ContosoUniversity*和 *.csproj*文件。</span><span class="sxs-lookup"><span data-stu-id="4cd97-308">The *obj* folder and the *ContosoUniversity.csproj* and *.csproj.user* files are omitted for the same reason.</span></span>

    <span data-ttu-id="4cd97-309">单击 "**发布**" 以部署到生产环境。</span><span class="sxs-lookup"><span data-stu-id="4cd97-309">Click **Publish** to deploy to the production environment.</span></span>
2. <span data-ttu-id="4cd97-310">在生产环境中测试，遵循用于过渡的相同过程。</span><span class="sxs-lookup"><span data-stu-id="4cd97-310">Test in production, following the same procedure you used for staging.</span></span>

    <span data-ttu-id="4cd97-311">除了 URL 和缺少*robots.txt*文件，所有内容都与过渡完全相同。</span><span class="sxs-lookup"><span data-stu-id="4cd97-311">Everything is identical to staging except for the URL and the absence of the *robots.txt* file.</span></span>

## <a name="summary"></a><span data-ttu-id="4cd97-312">总结</span><span class="sxs-lookup"><span data-stu-id="4cd97-312">Summary</span></span>

<span data-ttu-id="4cd97-313">现在，你已成功部署并测试了 web 应用，并且该应用可通过 Internet 公开使用。</span><span class="sxs-lookup"><span data-stu-id="4cd97-313">You have now successfully deployed and tested your web app and it is available publicly over the Internet.</span></span>

![主页生产](deploying-to-production/_static/image15.png)

<span data-ttu-id="4cd97-315">在下一教程中，你将更新应用程序代码并将更改部署到测试、过渡和生产环境。</span><span class="sxs-lookup"><span data-stu-id="4cd97-315">In the next tutorial, you'll update application code and deploy the change to the test, staging, and production environments.</span></span>

> [!NOTE]
> <span data-ttu-id="4cd97-316">当应用程序在生产环境中使用时，应实施恢复计划。</span><span class="sxs-lookup"><span data-stu-id="4cd97-316">While your application is in use in the production environment you should be implementing a recovery plan.</span></span> <span data-ttu-id="4cd97-317">也就是说，应定期将数据库从生产应用备份到安全存储位置，并且应保留多代此类备份。</span><span class="sxs-lookup"><span data-stu-id="4cd97-317">That is, you should be periodically backing up your databases from the production app to a secure storage location, and you should be keeping several generations of such backups.</span></span> <span data-ttu-id="4cd97-318">更新数据库时，应立即从更改之前创建备份副本。</span><span class="sxs-lookup"><span data-stu-id="4cd97-318">When you update the database, you should make a backup copy from immediately before the change.</span></span> <span data-ttu-id="4cd97-319">然后，如果您在将其部署到生产环境之前，不会发现该错误，则您仍然能够将数据库恢复到其损坏之前的状态。</span><span class="sxs-lookup"><span data-stu-id="4cd97-319">Then, if you make a mistake and don't discover it until after you have deployed it to production, you will still be able to recover the database to the state it was in before it became corrupted.</span></span> <span data-ttu-id="4cd97-320">有关详细信息，请参阅 [Azure SQL 数据库备份和还原](https://msdn.microsoft.com/library/windowsazure/jj650016.aspx)。</span><span class="sxs-lookup"><span data-stu-id="4cd97-320">For more information, see [Azure SQL Database Backup and Restore](https://msdn.microsoft.com/library/windowsazure/jj650016.aspx).</span></span>
> 
> 
> [!NOTE]
> <span data-ttu-id="4cd97-321">在本教程中，你要部署到的 SQL Server 版本是 Azure SQL 数据库。</span><span class="sxs-lookup"><span data-stu-id="4cd97-321">In this tutorial the SQL Server edition that you are deploying to is Azure SQL Database.</span></span> <span data-ttu-id="4cd97-322">尽管部署过程与 SQL Server 的其他版本类似，但在某些情况下，实际生产应用程序可能需要 Azure SQL 数据库的特殊代码。</span><span class="sxs-lookup"><span data-stu-id="4cd97-322">While the deployment process is similar to other editions of SQL Server, a real production application might require special code for Azure SQL Database in some scenarios.</span></span> <span data-ttu-id="4cd97-323">有关详细信息，请参阅使用[AZURE Sql 数据库](../../../../whitepapers/aspnet-data-access-content-map.md#ssdb)和[在 SQL SERVER 和 Azure SQL 数据库之间进行选择](../../../../whitepapers/aspnet-data-access-content-map.md#ssdbchoosing)。</span><span class="sxs-lookup"><span data-stu-id="4cd97-323">For more information, see [Working with Azure SQL Database](../../../../whitepapers/aspnet-data-access-content-map.md#ssdb) and [Choosing between SQL Server and Azure SQL Database](../../../../whitepapers/aspnet-data-access-content-map.md#ssdbchoosing).</span></span>
> 
> [!div class="step-by-step"]
> <span data-ttu-id="4cd97-324">[上一页](setting-folder-permissions.md)
> [下一页](deploying-a-code-update.md)</span><span class="sxs-lookup"><span data-stu-id="4cd97-324">[Previous](setting-folder-permissions.md)
[Next](deploying-a-code-update.md)</span></span>

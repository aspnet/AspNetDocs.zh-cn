---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/publishing
title: 简介 ASP.NET 网页-通过使用 WebMatrix 发布站点 |Microsoft Docs
author: Rick-Anderson
description: 本教程是介绍 ASP.NET 网页和 Microsoft WebMatrix 的教程集的最后一部分。 本文介绍了如何发布站点 t .。。
ms.author: riande
ms.date: 05/28/2015
ms.assetid: 7e85c70e-1a88-4408-8b3d-29611c7713ed
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/publishing
msc.type: authoredcontent
ms.openlocfilehash: a09339a833ea0b4a2d3c3a9323cce777577ea048
ms.sourcegitcommit: 0cf7d06071a8ff986e6c028ac9daf0c0e7490412
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/23/2020
ms.locfileid: "85240593"
---
# <a name="introducing-aspnet-web-pages---publishing-a-site-by-using-webmatrix"></a><span data-ttu-id="165e8-104">简介 ASP.NET 网页-通过使用 WebMatrix 发布站点</span><span class="sxs-lookup"><span data-stu-id="165e8-104">Introducing ASP.NET Web Pages - Publishing a Site by Using WebMatrix</span></span>

<span data-ttu-id="165e8-105"> 作者 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="165e8-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="165e8-106">本教程是介绍 ASP.NET 网页和 Microsoft WebMatrix 的教程集的最后一部分。</span><span class="sxs-lookup"><span data-stu-id="165e8-106">This tutorial is the final installment in the tutorial set that introduces ASP.NET Web Pages and Microsoft WebMatrix.</span></span> <span data-ttu-id="165e8-107">本文介绍如何将站点发布到 Internet，以便其他人可以使用它。</span><span class="sxs-lookup"><span data-stu-id="165e8-107">It discusses how to publish your site to the Internet so that others can work with it.</span></span> <span data-ttu-id="165e8-108">它假定您已经完成了如何[为 ASP.NET 网页网站创建一致的外观](https://go.microsoft.com/fwlink/?LinkId=251585)。</span><span class="sxs-lookup"><span data-stu-id="165e8-108">It assumes you have completed the series through [Creating a Consistent Look for ASP.NET Web Pages Sites](https://go.microsoft.com/fwlink/?LinkId=251585).</span></span>
> 
> <span data-ttu-id="165e8-109">你将了解如何使用发布网站：</span><span class="sxs-lookup"><span data-stu-id="165e8-109">You'll learn how to publish your site using:</span></span>
> 
> - <span data-ttu-id="165e8-110">Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="165e8-110">Microsoft Azure</span></span>
> - <span data-ttu-id="165e8-111">Web 托管公司</span><span class="sxs-lookup"><span data-stu-id="165e8-111">Web Hosting Company</span></span>

## <a name="about-publishing-your-site"></a><span data-ttu-id="165e8-112">关于发布网站</span><span class="sxs-lookup"><span data-stu-id="165e8-112">About Publishing Your Site</span></span>

<span data-ttu-id="165e8-113">至此，你已完成了本地计算机上的所有工作，包括测试页面。</span><span class="sxs-lookup"><span data-stu-id="165e8-113">Up to now, you've done all your work on a local computer, including testing your pages.</span></span> <span data-ttu-id="165e8-114">若要运行你的<em>cshtml</em>页面，你使用了内置于 WebMatrix 的 web 服务器，即 IIS Express。</span><span class="sxs-lookup"><span data-stu-id="165e8-114">To run your<em>.cshtml</em> pages, you've used the web server that's built into WebMatrix, namely IIS Express.</span></span> <span data-ttu-id="165e8-115">当然，除了您以外，没有人可以查看您创建的站点。</span><span class="sxs-lookup"><span data-stu-id="165e8-115">But of course no one can see the site you've created except you.</span></span> <span data-ttu-id="165e8-116">若要让其他人使用你的网站，你必须将其发布到 Internet。</span><span class="sxs-lookup"><span data-stu-id="165e8-116">To let others work with your site, you have to publish it to the Internet.</span></span>

<span data-ttu-id="165e8-117">如果你已经拥有公共 web 服务器的访问权限，则发布意味着你需要具有*云平台*或*托管提供程序*的帐户。</span><span class="sxs-lookup"><span data-stu-id="165e8-117">Unless you have access to a public web server already, publishing means that you have to have an account with a *cloud platform* or a *hosting provider*.</span></span> <span data-ttu-id="165e8-118">云平台（如 Microsoft Azure）为应用程序提供按需的基础结构。</span><span class="sxs-lookup"><span data-stu-id="165e8-118">A cloud platform, such as Microsoft Azure, provides on-demand infrastructure for your applications.</span></span> <span data-ttu-id="165e8-119">托管提供商是拥有可公开访问的 web 服务器并且将为你的站点提供空间的公司。</span><span class="sxs-lookup"><span data-stu-id="165e8-119">A hosting provider is a company that owns publicly accessible web servers and that will rent you space for your site.</span></span> <span data-ttu-id="165e8-120">对于大容量商业网站，托管计划每月从几个月（甚至免费）对小型站点运行一次，每月有数百美元的资金。</span><span class="sxs-lookup"><span data-stu-id="165e8-120">Hosting plans run from a few dollars a month (or even free) for small sites to many hundreds of dollars a month for high-volume commercial websites.</span></span>

> [!NOTE]
> <span data-ttu-id="165e8-121">你可能有权通过 internet 服务提供商（ISP）访问公共 web 服务器，你可以在家里获取 internet 服务。</span><span class="sxs-lookup"><span data-stu-id="165e8-121">You might have access to a public web server via the internet service provider (ISP) that you use to get internet service at home.</span></span> <span data-ttu-id="165e8-122">但是，宿主提供程序必须支持 ASP.NET 网页。</span><span class="sxs-lookup"><span data-stu-id="165e8-122">However, your hosting provider must support ASP.NET Web Pages.</span></span> <span data-ttu-id="165e8-123">许多 Isp 不是，但一定要进行检查。</span><span class="sxs-lookup"><span data-stu-id="165e8-123">Many ISPs don't, but it's always worth checking.</span></span>

<span data-ttu-id="165e8-124">在本教程中，我们将简要介绍如何发布。</span><span class="sxs-lookup"><span data-stu-id="165e8-124">In this tutorial, we'll give you an overview of how to publish.</span></span> <span data-ttu-id="165e8-125">提供所有内容的详细信息并不可行，因为每个托管提供程序的过程各不相同。</span><span class="sxs-lookup"><span data-stu-id="165e8-125">It's not practical to provide exact details for everything, because the process differs a bit for every hosting provider.</span></span> <span data-ttu-id="165e8-126">不过，您可以很好地了解该过程的工作方式。</span><span class="sxs-lookup"><span data-stu-id="165e8-126">But you'll get a good idea of how the process works.</span></span>

<span data-ttu-id="165e8-127">本教程包含四个部分：</span><span class="sxs-lookup"><span data-stu-id="165e8-127">This tutorial contains four sections:</span></span>

1. [<span data-ttu-id="165e8-128">设置默认页</span><span class="sxs-lookup"><span data-stu-id="165e8-128">Setting up the default page</span></span>](#defaultpage)
2. <span data-ttu-id="165e8-129">发布（选择以下项之一）</span><span class="sxs-lookup"><span data-stu-id="165e8-129">Publishing (choose one of the following)</span></span>  
 <span data-ttu-id="165e8-130">a.</span><span class="sxs-lookup"><span data-stu-id="165e8-130">a.</span></span> [<span data-ttu-id="165e8-131">将站点发布到 Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="165e8-131">Publishing Your Site to Microsoft Azure</span></span>](#azure)  
 <span data-ttu-id="165e8-132">b.</span><span class="sxs-lookup"><span data-stu-id="165e8-132">b.</span></span> [<span data-ttu-id="165e8-133">将网站发布到 Web 托管公司</span><span class="sxs-lookup"><span data-stu-id="165e8-133">Publishing Your Site to a Web Hosting Company</span></span>](#host)
3. [<span data-ttu-id="165e8-134">更新实时站点：重新发布</span><span class="sxs-lookup"><span data-stu-id="165e8-134">Updating the Live Site: Republishing</span></span>](#update)

<a id="defaultpage"></a>
## <a name="setting-up-the-default-page"></a><span data-ttu-id="165e8-135">设置默认页</span><span class="sxs-lookup"><span data-stu-id="165e8-135">Setting up the default page</span></span>

<span data-ttu-id="165e8-136">当用户导航到网站的基址时，将向用户显示站点的默认页面。</span><span class="sxs-lookup"><span data-stu-id="165e8-136">When a user navigates to the base address for your web site, the default page for your site is displayed to the user.</span></span> <span data-ttu-id="165e8-137">例如，将*Default.htm*设置为站点的默认页面时 `www.contoso.com` ，导航到与 `www.contoso.com` 导航到相同的页面 `www.contoso.com/Default.htm` 。</span><span class="sxs-lookup"><span data-stu-id="165e8-137">For example, when *Default.htm* is set as the default page for the site at `www.contoso.com`, then navigating to `www.contoso.com` is the same as navigating to `www.contoso.com/Default.htm`.</span></span>

<span data-ttu-id="165e8-138">当前，你的网站使用**默认的. cshtml**作为默认页。</span><span class="sxs-lookup"><span data-stu-id="165e8-138">Currently, your site uses **Default.cshtml** as the default page.</span></span> <span data-ttu-id="165e8-139">此页可用于你的默认页面，但在本教程中，你没有将任何内容添加到该页面，因此它将显示一个空白页面。</span><span class="sxs-lookup"><span data-stu-id="165e8-139">This page is fine for your default page, but in this tutorial you have not added any content to that page so it would display a blank page.</span></span> <span data-ttu-id="165e8-140">打开默认的 cshtml，并将内容替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="165e8-140">Open Default.cshtml and replace the content with the following code.</span></span>

[!code-cshtml[Main](publishing/samples/sample1.cshtml)]

<span data-ttu-id="165e8-141">现在，你的网站已准备好进行发布。</span><span class="sxs-lookup"><span data-stu-id="165e8-141">Now your site is ready for publication.</span></span> <span data-ttu-id="165e8-142">首先，您将了解如何将网站部署到 Azure，以及如何将其部署到 web 托管公司。</span><span class="sxs-lookup"><span data-stu-id="165e8-142">First, you will see how to deploy the site to Azure, and then how to deploy it to a web hosting company.</span></span> <span data-ttu-id="165e8-143">这两个选项都适用于你的网站，你只需遵循一个部署选项。</span><span class="sxs-lookup"><span data-stu-id="165e8-143">Either option works for your web site, and you only need to follow one of the deployment options.</span></span>

<a id="azure"></a>
## <a name="publishing-your-site-to-microsoft-azure"></a><span data-ttu-id="165e8-144">将站点发布到 Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="165e8-144">Publishing Your Site to Microsoft Azure</span></span>

<span data-ttu-id="165e8-145">本教程将首先介绍如何将网站部署到 Microsoft Azure。</span><span class="sxs-lookup"><span data-stu-id="165e8-145">This tutorial will first show you how to deploy your site to Microsoft Azure.</span></span> <span data-ttu-id="165e8-146">通过使用 Microsoft 帐户登录，你可以在 Azure 上创建最多10个免费网站。</span><span class="sxs-lookup"><span data-stu-id="165e8-146">By signing in with a Microsoft account, you can create up to 10 free sites on Azure.</span></span> <span data-ttu-id="165e8-147">这些免费网站提供了一种方便的方法来测试您的站点。</span><span class="sxs-lookup"><span data-stu-id="165e8-147">These free sites provide a convenient way to test your sites.</span></span> <span data-ttu-id="165e8-148">稍后，你始终可以删除此示例网站，以避免使用所有免费网站。</span><span class="sxs-lookup"><span data-stu-id="165e8-148">You can always delete this example site later to avoid using all of your free sites.</span></span> <span data-ttu-id="165e8-149">只需几分钟即可创建一个免费试用帐户。</span><span class="sxs-lookup"><span data-stu-id="165e8-149">You can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="165e8-150">有关详细信息，请参阅 [Azure 免费试用](https://azure.microsoft.com/free/dotnet/)。</span><span class="sxs-lookup"><span data-stu-id="165e8-150">For details, see [Azure Free Trial](https://azure.microsoft.com/free/dotnet/).</span></span>

<span data-ttu-id="165e8-151">在 WebMatrix 功能区中，单击 "**发布**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="165e8-151">In the WebMatrix ribbon, click the **Publish** button.</span></span>

![WebMatrix 功能区中的 "发布" 按钮](publishing/_static/image1.png)

<span data-ttu-id="165e8-153">随即显示 "**发布网站**" 对话框。</span><span class="sxs-lookup"><span data-stu-id="165e8-153">The **Publish Your Site** dialog box is displayed.</span></span> <span data-ttu-id="165e8-154">如果尚未登录到 Microsoft 帐户，则对话框将包含 " **Azure 入门**" 链接。</span><span class="sxs-lookup"><span data-stu-id="165e8-154">If you have not signed in to your Microsoft account, the dialog box will contain a **Get started with Azure** link.</span></span> <span data-ttu-id="165e8-155">单击此链接。</span><span class="sxs-lookup"><span data-stu-id="165e8-155">Click this link.</span></span>

![发布你的网站](publishing/_static/image2.png)

<span data-ttu-id="165e8-157">如果尚未登录到 Microsoft 帐户，则会再次获得登录机会。</span><span class="sxs-lookup"><span data-stu-id="165e8-157">If you have not signed in to a Microsoft account, you are again given the opportunity to sign in.</span></span> <span data-ttu-id="165e8-158">你必须登录到 Microsoft 帐户才能在 Azure 上发布你的网站。</span><span class="sxs-lookup"><span data-stu-id="165e8-158">You must sign in to a Microsoft account to publish your site on Azure.</span></span>

![登录](publishing/_static/image3.png)

<span data-ttu-id="165e8-160">登录到 Microsoft 帐户后，该对话框包含用于在 Azure 上创建新网站或连接到 Azure 上的现有网站之一的链接。</span><span class="sxs-lookup"><span data-stu-id="165e8-160">After signing in to your Microsoft account, the dialog box contains links to create a new site on Azure or connect to one of your existing sites on Azure.</span></span>

![创建新站点](publishing/_static/image4.png)

<span data-ttu-id="165e8-162">选择 "**创建新站点**"。</span><span class="sxs-lookup"><span data-stu-id="165e8-162">Select **Create a new site**.</span></span>

<span data-ttu-id="165e8-163">如果你将项目命名为**WebPagesMovies**，则网站的默认名称将为**webpagesmovies.azurewebsites.net**。</span><span class="sxs-lookup"><span data-stu-id="165e8-163">If you named your project **WebPagesMovies**, the default name for your site will be **webpagesmovies.azurewebsites.net**.</span></span> <span data-ttu-id="165e8-164">此默认名称很可能不可用，如红色惊叹号所示。</span><span class="sxs-lookup"><span data-stu-id="165e8-164">This default name is most likely not available, as indicated by the red exclamation mark.</span></span>

![默认网站名称](publishing/_static/image5.png)

<span data-ttu-id="165e8-166">将 "站点名称" 更改为 "可用"，然后选择靠近你所在位置的位置。</span><span class="sxs-lookup"><span data-stu-id="165e8-166">Change the site name to something that is available, and select a location that is close to your location.</span></span>

![更改的站点名称](publishing/_static/image6.png)

<span data-ttu-id="165e8-168">单击“确定”。</span><span class="sxs-lookup"><span data-stu-id="165e8-168">Click **OK**.</span></span>

<span data-ttu-id="165e8-169">WebMatrix performss 一种测试来确定服务器是否与站点兼容。</span><span class="sxs-lookup"><span data-stu-id="165e8-169">WebMatrix performss a test to determine if the server is compatible with your site.</span></span>

![兼容性测试](publishing/_static/image7.png)

<span data-ttu-id="165e8-171">选择“继续”。</span><span class="sxs-lookup"><span data-stu-id="165e8-171">Select **Continue**.</span></span>

<span data-ttu-id="165e8-172">将显示兼容性测试的结果。</span><span class="sxs-lookup"><span data-stu-id="165e8-172">The results of the compatibility test are displayed.</span></span>

![兼容性结果](publishing/_static/image8.png)

<span data-ttu-id="165e8-174">选择“继续”。</span><span class="sxs-lookup"><span data-stu-id="165e8-174">Select **Continue**.</span></span>

<span data-ttu-id="165e8-175">WebMatrix 显示将发布到站点的文件和数据库。</span><span class="sxs-lookup"><span data-stu-id="165e8-175">WebMatrix displays the files and databases that will be published to the site.</span></span> <span data-ttu-id="165e8-176">由于这是你首次发布网站，因此会列出所有文件。</span><span class="sxs-lookup"><span data-stu-id="165e8-176">Since this is the first time you are publishing the site, all of the files are listed.</span></span> <span data-ttu-id="165e8-177">您可以取消选中未准备好进行发布的文件。</span><span class="sxs-lookup"><span data-stu-id="165e8-177">You can uncheck a file that is not ready to be published.</span></span> <span data-ttu-id="165e8-178">在后续发布中，只显示已更改的文件。</span><span class="sxs-lookup"><span data-stu-id="165e8-178">In the subsequent publications, only the files that have changed will be displayed.</span></span> <span data-ttu-id="165e8-179">请参阅[更新实时网站：重新发布](#update)。</span><span class="sxs-lookup"><span data-stu-id="165e8-179">See [Updating the Live Site: Republishing](#update).</span></span>

![发布预览](publishing/_static/image9.png)

<span data-ttu-id="165e8-181">选择“继续”。</span><span class="sxs-lookup"><span data-stu-id="165e8-181">Select **Continue**.</span></span>

<span data-ttu-id="165e8-182">将站点部署到 Azure 之后，会显示一条消息，指示部署已完成。</span><span class="sxs-lookup"><span data-stu-id="165e8-182">After the site has been deployed to Azure, a message is displayed that indicates the deployment has completed.</span></span>

![发布完成](publishing/_static/image10.png)

<span data-ttu-id="165e8-184">你的网站和数据库已发布到 Azure，现在可供公众使用。</span><span class="sxs-lookup"><span data-stu-id="165e8-184">Your site and database have been published to Azure, and are now available to the public.</span></span> <span data-ttu-id="165e8-185">单击消息中指示发布已完成的链接，此时将显示已部署的站点。</span><span class="sxs-lookup"><span data-stu-id="165e8-185">Click the link in the message indicating publishing has completed, and you will now see your deployed site.</span></span> <span data-ttu-id="165e8-186">你或拥有 Internet 访问权限的任何人都可以添加或修改数据库中的记录。</span><span class="sxs-lookup"><span data-stu-id="165e8-186">You or anyone with Internet access can add or modify records in the database.</span></span>

![](publishing/_static/image11.png)

<a id="host"></a>
## <a name="publishing-your-site-to-a-web-hosting-company"></a><span data-ttu-id="165e8-187">将网站发布到 Web 托管公司</span><span class="sxs-lookup"><span data-stu-id="165e8-187">Publishing Your Site to a Web Hosting Company</span></span>

<span data-ttu-id="165e8-188">如果决定不发布到 Azure，可以改为将网站发布到 web 托管公司。</span><span class="sxs-lookup"><span data-stu-id="165e8-188">If you decide to not publish to Azure, you can instead publish your site to a web hosting company.</span></span>

<span data-ttu-id="165e8-189">单击 "**查找 web 托管**" 链接。</span><span class="sxs-lookup"><span data-stu-id="165e8-189">Click the **Find web hosting** link.</span></span>

!["发布设置" 对话框中的 "查找 web 宿主" 按钮](publishing/_static/image12.png)

<span data-ttu-id="165e8-191">请访问 Microsoft 网站上的页面，其中列出了支持 ASP.NET 的托管提供商。</span><span class="sxs-lookup"><span data-stu-id="165e8-191">You go to a page on the Microsoft site that lists hosting providers that support ASP.NET.</span></span>

![列出托管提供商的 Microsoft 网站上的页面](publishing/_static/image13.png)

<span data-ttu-id="165e8-193">很明显，现在很难知道您可能需要的长期托管功能。</span><span class="sxs-lookup"><span data-stu-id="165e8-193">Obviously, it can be difficult to know now exactly what hosting features you might require over the long term.</span></span> <span data-ttu-id="165e8-194">下面是几个需要注意的事项：</span><span class="sxs-lookup"><span data-stu-id="165e8-194">Here are a couple of things to consider:</span></span>

- <span data-ttu-id="165e8-195">对于 WebPagesMovies 站点，无需为 SQL Server 提供单独的外接程序，这通常会产生额外的成本。</span><span class="sxs-lookup"><span data-stu-id="165e8-195">For purposes of the WebPagesMovies site, you don't have to have a separate add-on for SQL Server, which often costs extra.</span></span> <span data-ttu-id="165e8-196">在您的网站中，您使用的是自包含 SQL Server Compact 版本。</span><span class="sxs-lookup"><span data-stu-id="165e8-196">In your site, you're using SQL Server Compact Edition, which is self-contained.</span></span> <span data-ttu-id="165e8-197">但是，你可能需要 SQL Server 的访问权限，才能执行某些后续的网站工作。</span><span class="sxs-lookup"><span data-stu-id="165e8-197">However, you might need SQL Server access for some future website work you do.</span></span> <span data-ttu-id="165e8-198">如果你认为可能，请确保稍后可以添加 SQL Server 功能。</span><span class="sxs-lookup"><span data-stu-id="165e8-198">If you think you might, make sure that you can add SQL Server capability later.</span></span>
- <span data-ttu-id="165e8-199">检查宿主提供程序是否支持 Web 部署发布协议。</span><span class="sxs-lookup"><span data-stu-id="165e8-199">Check whether the hosting provider supports the Web Deploy publishing protocol.</span></span> <span data-ttu-id="165e8-200">您可以使用 FTP 协议进行发布，但使用 Web 部署更为方便。</span><span class="sxs-lookup"><span data-stu-id="165e8-200">You can publish by using FTP protocol, but it's more convenient to use Web Deploy.</span></span>

<span data-ttu-id="165e8-201">某些站点提供免费试用期。</span><span class="sxs-lookup"><span data-stu-id="165e8-201">Some sites offer a free trial period.</span></span> <span data-ttu-id="165e8-202">免费试用版是尝试发布和托管的好方法，同时你仍在使用 WebMatrix 和 ASP.NET 网页。</span><span class="sxs-lookup"><span data-stu-id="165e8-202">A free trial is a good way to try publishing and hosting while you're still experimenting with WebMatrix and ASP.NET Web Pages.</span></span>

<span data-ttu-id="165e8-203">选择你喜欢的一个。</span><span class="sxs-lookup"><span data-stu-id="165e8-203">Pick one that you like.</span></span> <span data-ttu-id="165e8-204">对于本教程，我们选择了 "DiscountASP.NET"，因为在创建本教程的过程中，该公司的促销活动允许用户在数月内免费托管站点。</span><span class="sxs-lookup"><span data-stu-id="165e8-204">For this tutorial, we selected DiscountASP.NET, because while we were creating the tutorial, that company had a promotion that let people host a site free for a few months.</span></span>

> [!NOTE]
> <span data-ttu-id="165e8-205">对于本教程，我们选择的托管提供商不应将其解释为对该公司的认可。</span><span class="sxs-lookup"><span data-stu-id="165e8-205">Our choice of a hosting provider for this tutorial shouldn't be interpreted as an endorsement of that company over any other.</span></span> <span data-ttu-id="165e8-206">但我们必须选择一个用于说明，而 DiscountASP.NET 是支持 ASP.NET 网页的众多公司之一和发布的 Web 部署协议。</span><span class="sxs-lookup"><span data-stu-id="165e8-206">But we had to pick one for illustration, and DiscountASP.NET is one of the many companies that supports ASP.NET Web Pages and the Web Deploy protocol for publishing.</span></span>

<span data-ttu-id="165e8-207">通常，在注册托管提供程序后，公司会向你发送一封电子邮件，其中包含用户名和密码、web 服务器的 URL 等。</span><span class="sxs-lookup"><span data-stu-id="165e8-207">Typically, after you've signed up with the hosting provider, the company sends you an email that contains a user name and password, the URL of the web server, and so on.</span></span> <span data-ttu-id="165e8-208">如果托管公司支持 Web 部署协议，则他们可能会向您发送包含发布设置的文件，或让您下载一个文件。</span><span class="sxs-lookup"><span data-stu-id="165e8-208">If the hosting company supports Web Deploy protocol, they might send you a file that contains publish settings, or let you download one.</span></span> <span data-ttu-id="165e8-209">发布设置文件简化了过程。</span><span class="sxs-lookup"><span data-stu-id="165e8-209">A publish settings file simplifies the process for you.</span></span>

<span data-ttu-id="165e8-210">注册并准备好发布后，请单击 "WebMatrix" 功能区中的 "**发布**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="165e8-210">When you've signed up and are ready to publish, click the **Publish** button in the WebMatrix ribbon.</span></span> <span data-ttu-id="165e8-211">随即显示 "**发布设置**" 对话框。</span><span class="sxs-lookup"><span data-stu-id="165e8-211">The **Publish Settings** dialog box is displayed.</span></span>

<span data-ttu-id="165e8-212">如果宿主提供程序发送了发布设置文件，请单击 "**导入发布设置**" 链接，然后导入该文件。</span><span class="sxs-lookup"><span data-stu-id="165e8-212">If the hosting provider sent you a publish settings file, click the **Import publish settings** link and import the file.</span></span> <span data-ttu-id="165e8-213">如果没有发布设置文件，请使用托管公司通过电子邮件发送给您的值填写字段。</span><span class="sxs-lookup"><span data-stu-id="165e8-213">If you don't have a publish settings file, fill in the fields by using the values that the hosting company sent you in email.</span></span> <span data-ttu-id="165e8-214">完成后，"**发布设置**" 对话框如下所示：</span><span class="sxs-lookup"><span data-stu-id="165e8-214">Here's what the **Publish Settings** dialog box might look like when you're done:</span></span>

![在 "发布设置" 对话框中填写的发布设置](publishing/_static/image14.png)

<span data-ttu-id="165e8-216">单击 "**验证连接**"。</span><span class="sxs-lookup"><span data-stu-id="165e8-216">Click **Validate Connection**.</span></span> <span data-ttu-id="165e8-217">如果一切正常，对话框将报告**成功连接**，这意味着它可以与宿主提供商的服务器进行通信。</span><span class="sxs-lookup"><span data-stu-id="165e8-217">If everything is ok, the dialog box reports **Connected successfully**, which means it can communicate with the hosting provider's server.</span></span>

![发布设置正确时的成功消息](publishing/_static/image15.png)

<span data-ttu-id="165e8-219">如果出现问题，WebMatrix 会尽力告诉您问题是什么：</span><span class="sxs-lookup"><span data-stu-id="165e8-219">If there's a problem, WebMatrix does its best to tell you what the problem is:</span></span>

![发布设置出现问题时出现错误消息](publishing/_static/image16.png)

<span data-ttu-id="165e8-221">单击“保存”\*\*\*\* 以保存设置。</span><span class="sxs-lookup"><span data-stu-id="165e8-221">Click **Save** to save your settings.</span></span> <span data-ttu-id="165e8-222">WebMatrix 提供执行测试以确保它能够与宿主站点正确通信：</span><span class="sxs-lookup"><span data-stu-id="165e8-222">WebMatrix offers to perform a test to make sure that it can communicate correctly with the hosting site:</span></span>

![用于执行发布过程测试的消息服务](publishing/_static/image17.png)

<span data-ttu-id="165e8-224">单击 **“是”** 。</span><span class="sxs-lookup"><span data-stu-id="165e8-224">Click **Yes**.</span></span> <span data-ttu-id="165e8-225">WebMatrix 将一些示例文件上传到宿主提供程序。</span><span class="sxs-lookup"><span data-stu-id="165e8-225">WebMatrix uploads some sample files to the hosting provider.</span></span> <span data-ttu-id="165e8-226">兼容性测试完成后，WebMatrix 会报告结果：</span><span class="sxs-lookup"><span data-stu-id="165e8-226">When the compatibility test is done, WebMatrix reports the results:</span></span>

![发布测试的结果](publishing/_static/image18.png)

<span data-ttu-id="165e8-228">如果已准备就绪，请继续操作，并单击 "**继续**" 以启动真实的发布过程。</span><span class="sxs-lookup"><span data-stu-id="165e8-228">If you're ready to go, go ahead and click **Continue** to start the publish process for real.</span></span> <span data-ttu-id="165e8-229">WebMatrix 指出了站点中有哪些文件，并且这些文件已位于主机服务器上（目前为 "无"），并提供发布过程的预览：</span><span class="sxs-lookup"><span data-stu-id="165e8-229">WebMatrix figures out what files are in your site and are already on the host server (right now, none) and gives you a preview of the publish process:</span></span>

![发布进程将上传的文件的预览](publishing/_static/image19.png)

<span data-ttu-id="165e8-231">要发布的文件的列表包含您创建的网页 *，如：*</span><span class="sxs-lookup"><span data-stu-id="165e8-231">The list of files to publish includes the web pages that you've created like *Movies.cshtml*.</span></span> <span data-ttu-id="165e8-232">此列表还包括已安装的帮助程序的文件、为数据库 SQL Server Compact 版本运行的文件等。</span><span class="sxs-lookup"><span data-stu-id="165e8-232">The list also includes files for helpers that you've installed, the files to run SQL Server Compact Edition for your database, and so on.</span></span> <span data-ttu-id="165e8-233">因此，初始发布过程可能很重要。</span><span class="sxs-lookup"><span data-stu-id="165e8-233">As a result, the initial publish process can be substantial.</span></span>

<span data-ttu-id="165e8-234">单击“继续” 。</span><span class="sxs-lookup"><span data-stu-id="165e8-234">Click **Continue**.</span></span> <span data-ttu-id="165e8-235">WebMatrix 将文件复制到托管提供商的服务器。</span><span class="sxs-lookup"><span data-stu-id="165e8-235">WebMatrix copies your files to the hosting provider's server.</span></span> <span data-ttu-id="165e8-236">完成后，会在状态栏中报告结果：</span><span class="sxs-lookup"><span data-stu-id="165e8-236">When it's done, the results are reported in the status bar:</span></span>

![发布过程成功完成后的状态栏消息](publishing/_static/image20.png)

<span data-ttu-id="165e8-238">若要查看实时网站，请单击状态栏中的链接。</span><span class="sxs-lookup"><span data-stu-id="165e8-238">To see your live site, click the link in the status bar.</span></span> <span data-ttu-id="165e8-239">将*电影*添加到 URL，你将看到你创建的 "*电影*" 文件：</span><span class="sxs-lookup"><span data-stu-id="165e8-239">Add *Movies* to the URL, and you'll see the *Movies.cshtml* file that you created:</span></span>

![显示电影页面的实时站点](publishing/_static/image21.png)

<a id="update"></a>
## <a name="updating-the-live-site-republishing"></a><span data-ttu-id="165e8-241">更新实时站点：重新发布</span><span class="sxs-lookup"><span data-stu-id="165e8-241">Updating the Live Site: Republishing</span></span>

<span data-ttu-id="165e8-242">发布站点（到 Azure 或 web 托管公司）后， &mdash; 计算机上的版本和服务提供商的版本中都有两个副本。</span><span class="sxs-lookup"><span data-stu-id="165e8-242">Once you've published your site (to either Azure or a web hosting company), there are two copies of it &mdash; the version on your computer and the version on the service provider.</span></span> <span data-ttu-id="165e8-243">你可能想要继续开发站点（如果没有其他任何内容，作为下一个教程集的一部分）。</span><span class="sxs-lookup"><span data-stu-id="165e8-243">You'll probably want to continue developing the site (if nothing else, as part of the next tutorial set).</span></span> <span data-ttu-id="165e8-244">当你执行此操作时，必须重新发布网站才能将更改从计算机复制到服务提供商。</span><span class="sxs-lookup"><span data-stu-id="165e8-244">When you do, you have to republish your site in order to copy changes from your computer to the service provider.</span></span> <span data-ttu-id="165e8-245">WebMatrix 中的发布过程可以确定站点上已更改的文件，并仅发布这些文件。</span><span class="sxs-lookup"><span data-stu-id="165e8-245">The publish process in WebMatrix can determine what files have changed on your site and publish just those files.</span></span>

<span data-ttu-id="165e8-246">若要查看重新发布的工作原理，请打开 "*电影*" 站点，进行一些小的更改，然后保存该文件。</span><span class="sxs-lookup"><span data-stu-id="165e8-246">To see how republishing works, open the *Movies.cshtml* site, make some small change, and then save the file.</span></span> <span data-ttu-id="165e8-247">例如，将标题更改为 `Movies - Updated` 。</span><span class="sxs-lookup"><span data-stu-id="165e8-247">For example, change the title to `Movies - Updated`.</span></span>

<span data-ttu-id="165e8-248">单击功能区中的 "**发布**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="165e8-248">Click the **Publish** button in the ribbon.</span></span> <span data-ttu-id="165e8-249">WebMatrix 确定要更改的内容，并为你显示要发布的文件的预览。</span><span class="sxs-lookup"><span data-stu-id="165e8-249">WebMatrix determines what's changed and shows you a preview of the files it will publish.</span></span>

![显示已更改的文件以进行重新发布的 "发布" 对话框](publishing/_static/image22.png)

> [!IMPORTANT] 
> 
> <span data-ttu-id="165e8-251">默认情况下，WebMatrix 仅在第一次发布站点时发布数据库（*.sdf*文件）。</span><span class="sxs-lookup"><span data-stu-id="165e8-251">By default, WebMatrix publishes your database (*.sdf* file) only the first time you publish the site.</span></span> <span data-ttu-id="165e8-252">一旦你的网站发布并且用户与网站交互后，实时站点上的数据库通常会包含该站点的真实数据。</span><span class="sxs-lookup"><span data-stu-id="165e8-252">Once your site is published and people are interacting with the website, the database on the live site typically has the site's real data.</span></span> <span data-ttu-id="165e8-253">您必须小心地不要使用计算机上的 *.sdf*文件（通常只包含测试数据）来覆盖实时数据库。</span><span class="sxs-lookup"><span data-stu-id="165e8-253">You have to be very careful not to overwrite the live database with the *.sdf* file that's on your computer, which usually contains only test data.</span></span> <span data-ttu-id="165e8-254">这就是为什么会出现警告**发布将覆盖任何远程数据库**以及默认情况下清除*WebPagesMovies*的复选框的原因。</span><span class="sxs-lookup"><span data-stu-id="165e8-254">That's why you see the warning **Publishing will overwrite any remote databases**, and why the check box for *WebPagesMovies.sdf* is cleared by default.</span></span>

<span data-ttu-id="165e8-255">单击“继续” 。</span><span class="sxs-lookup"><span data-stu-id="165e8-255">Click **Continue**.</span></span> <span data-ttu-id="165e8-256">WebMatrix 发布已更改的文件，并显示一条成功消息，就像第一次发布时所做的那样。</span><span class="sxs-lookup"><span data-stu-id="165e8-256">WebMatrix publishes the changed files and shows you a success message, like it did the first time you published.</span></span>

<span data-ttu-id="165e8-257">转到活动站点（如果它仍显示，你可以单击成功消息中的链接）并验证你的更改是否已发布。</span><span class="sxs-lookup"><span data-stu-id="165e8-257">Go to the live site (you can click the link in the success message if it's still showing) and verify that your change has been published.</span></span>

> [!TIP] 
> 
> <span data-ttu-id="165e8-258">**远程编辑文件**</span><span class="sxs-lookup"><span data-stu-id="165e8-258">**Editing Files Remotely**</span></span>
> 
> <span data-ttu-id="165e8-259">作为更改站点和重新发布的替代方法，可以直接在 WebMatrix 中编辑远程文件。</span><span class="sxs-lookup"><span data-stu-id="165e8-259">As an alternative to changing your site and then republishing, you can edit remote files directly in WebMatrix.</span></span> <span data-ttu-id="165e8-260">在此方案中，你将打开服务提供商上的一个文件，WebMatrix 会下载该文件的副本供你编辑。</span><span class="sxs-lookup"><span data-stu-id="165e8-260">In this scenario, you open a file that's on the service provider, and WebMatrix downloads a copy of it for you to edit.</span></span> <span data-ttu-id="165e8-261">每次保存文件时，WebMatrix 都会将更改发送到站点。</span><span class="sxs-lookup"><span data-stu-id="165e8-261">Every time you save the file, WebMatrix sends the changes to the site.</span></span>
> 
> <span data-ttu-id="165e8-262">远程编辑是对您的实时网站进行更改的一种简单方法。</span><span class="sxs-lookup"><span data-stu-id="165e8-262">Remote editing is an easy way to make changes to your live site.</span></span> <span data-ttu-id="165e8-263">但是，以这种方式进行的更改不会与本地站点中的文件同步。</span><span class="sxs-lookup"><span data-stu-id="165e8-263">However, the changes you make this way aren't synchronized with the files in your local site.</span></span> <span data-ttu-id="165e8-264">若要将本地文件与远程站点同步，可以下载远程文件。</span><span class="sxs-lookup"><span data-stu-id="165e8-264">To synchronize the local files with the remote site, you can download the remote files.</span></span> <span data-ttu-id="165e8-265">除了反向，此过程的工作方式非常类似于发布。</span><span class="sxs-lookup"><span data-stu-id="165e8-265">This process works much like publishing, except in reverse.</span></span>
> 
> <span data-ttu-id="165e8-266">本文不会详细介绍 WebMatrix 的远程编辑和远程下载功能。</span><span class="sxs-lookup"><span data-stu-id="165e8-266">We won't describe more about the remote-editing and remote-download facilities of WebMatrix here.</span></span> <span data-ttu-id="165e8-267">如果多人必须在不同计算机上的同一站点上工作，则它们非常有用。</span><span class="sxs-lookup"><span data-stu-id="165e8-267">They're quite useful if multiple people have to work on the same site on different computers.</span></span> <span data-ttu-id="165e8-268">有关详细信息，请参阅[使用 WebMatrix 2 Beta 发布和编辑远程站点](https://go.microsoft.com/fwlink/?LinkId=251591)。</span><span class="sxs-lookup"><span data-stu-id="165e8-268">For more information, see [Publish and Edit a Remote Site with WebMatrix 2 Beta](https://go.microsoft.com/fwlink/?LinkId=251591).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="165e8-269">其他资源</span><span class="sxs-lookup"><span data-stu-id="165e8-269">Additional Resources</span></span>

- <span data-ttu-id="165e8-270">[ASP.NET WebMatrix ASP.NET 网页论坛](https://forums.asp.net/1224.aspx/1?WebMatrix+and+ASP+NET+Web+Pages)，是提出问题并获得答案的好地方。</span><span class="sxs-lookup"><span data-stu-id="165e8-270">[ASP.NET WebMatrix ASP.NET Web Pages forum](https://forums.asp.net/1224.aspx/1?WebMatrix+and+ASP+NET+Web+Pages), a great place to post questions and get answers.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="165e8-271">上一篇</span><span class="sxs-lookup"><span data-stu-id="165e8-271">Previous</span></span>](layouts.md)

---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/getting-started
title: 入门 | Microsoft Docs
author: Rick-Anderson
description: WebMatrix 不再建议作为 ASP.NET 网页的集成开发环境。 使用 Visual Studio 或 Visual Studio Code。 本指南 .。。
ms.author: riande
ms.date: 05/28/2015
ms.assetid: a36d3bdf-ef1b-47a4-b932-3a0cf4cad716
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/getting-started
msc.type: authoredcontent
ms.openlocfilehash: ac2111980e6393388a0530375fb9ef78dbbfaff6
ms.sourcegitcommit: 0cf7d06071a8ff986e6c028ac9daf0c0e7490412
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/23/2020
ms.locfileid: "85240763"
---
# <a name="getting-started"></a><span data-ttu-id="4bab9-105">入门</span><span class="sxs-lookup"><span data-stu-id="4bab9-105">Getting Started</span></span>

<span data-ttu-id="4bab9-106"> 作者 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="4bab9-106">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE[](~/includes/rp.md)]

> > [!NOTE] 
> > 
> > <span data-ttu-id="4bab9-107">WebMatrix 不再建议作为 ASP.NET 网页的集成开发环境。</span><span class="sxs-lookup"><span data-stu-id="4bab9-107">WebMatrix is no longer recommended as an integrated development environment for ASP.NET Web Pages.</span></span> <span data-ttu-id="4bab9-108">使用[Visual Studio](../program-asp-net-web-pages-in-visual-studio.md)或[Visual Studio Code](https://code.visualstudio.com/)。</span><span class="sxs-lookup"><span data-stu-id="4bab9-108">Use [Visual Studio](../program-asp-net-web-pages-in-visual-studio.md) or [Visual Studio Code](https://code.visualstudio.com/).</span></span>
> 
> 
> <span data-ttu-id="4bab9-109">本指南和应用程序提供 ASP.NET 网页（版本2或更高版本）和 Razor 语法（用于创建动态网站的轻型框架）的概述。</span><span class="sxs-lookup"><span data-stu-id="4bab9-109">This guidance and application gives you an overview of ASP.NET Web Pages (version 2 or later) and Razor syntax, a lightweight framework for creating dynamic websites.</span></span> <span data-ttu-id="4bab9-110">它还引入了 WebMatrix，这是用于创建页面和站点的工具。</span><span class="sxs-lookup"><span data-stu-id="4bab9-110">It also introduces WebMatrix, a tool for creating pages and sites.</span></span>
> 
> <span data-ttu-id="4bab9-111">**Level**： New to ASP.NET 网页。</span><span class="sxs-lookup"><span data-stu-id="4bab9-111">**Level**: New to ASP.NET Web Pages.</span></span>  
> <span data-ttu-id="4bab9-112">**假定的技能**： HTML、基本级联样式表（CSS）。</span><span class="sxs-lookup"><span data-stu-id="4bab9-112">**Skills assumed**: HTML, basic cascading style sheets (CSS).</span></span>
> 
> <span data-ttu-id="4bab9-113">你将在该集的第一个教程中学习以下内容：</span><span class="sxs-lookup"><span data-stu-id="4bab9-113">What you'll learn in the first tutorial of the set:</span></span>
> 
> - <span data-ttu-id="4bab9-114">什么是 ASP.NET 网页技术，它的作用是什么。</span><span class="sxs-lookup"><span data-stu-id="4bab9-114">What ASP.NET Web Pages technology is and what it's for.</span></span>
> - <span data-ttu-id="4bab9-115">WebMatrix 是什么。</span><span class="sxs-lookup"><span data-stu-id="4bab9-115">What WebMatrix is.</span></span>
> - <span data-ttu-id="4bab9-116">如何安装所有内容。</span><span class="sxs-lookup"><span data-stu-id="4bab9-116">How to install everything.</span></span>
> - <span data-ttu-id="4bab9-117">如何使用 WebMatrix 创建网站。</span><span class="sxs-lookup"><span data-stu-id="4bab9-117">How to create a website by using WebMatrix.</span></span>
>   
> 
> <span data-ttu-id="4bab9-118">介绍的功能/技术：</span><span class="sxs-lookup"><span data-stu-id="4bab9-118">Features/technologies discussed:</span></span>
> 
> - <span data-ttu-id="4bab9-119">Microsoft Web 平台安装程序。</span><span class="sxs-lookup"><span data-stu-id="4bab9-119">Microsoft Web Platform Installer.</span></span>
> - <span data-ttu-id="4bab9-120">WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="4bab9-120">WebMatrix.</span></span>
> - <span data-ttu-id="4bab9-121">*cshtml*页</span><span class="sxs-lookup"><span data-stu-id="4bab9-121">*.cshtml* pages</span></span>
>   
> 
> <span data-ttu-id="4bab9-122">Mike Pope 最初编写本教程。</span><span class="sxs-lookup"><span data-stu-id="4bab9-122">Mike Pope originally wrote this tutorial.</span></span> <span data-ttu-id="4bab9-123">Tom FitzMacken 对 Microsoft WebMatrix 3 进行了更新。</span><span class="sxs-lookup"><span data-stu-id="4bab9-123">Tom FitzMacken updated it for Microsoft WebMatrix 3.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="4bab9-124">本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="4bab9-124">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="4bab9-125">ASP.NET 网页（Razor）2</span><span class="sxs-lookup"><span data-stu-id="4bab9-125">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="4bab9-126">WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="4bab9-126">WebMatrix 3</span></span>

## <a name="what-should-you-know"></a><span data-ttu-id="4bab9-127">你应该知道哪些内容？</span><span class="sxs-lookup"><span data-stu-id="4bab9-127">What Should You Know?</span></span>

<span data-ttu-id="4bab9-128">假设你熟悉以下内容：</span><span class="sxs-lookup"><span data-stu-id="4bab9-128">We're assuming that you're familiar with:</span></span>

- <span data-ttu-id="4bab9-129">**HTML**。</span><span class="sxs-lookup"><span data-stu-id="4bab9-129">**HTML**.</span></span> <span data-ttu-id="4bab9-130">不需要深入的专业技能。</span><span class="sxs-lookup"><span data-stu-id="4bab9-130">No in-depth expertise is required.</span></span> <span data-ttu-id="4bab9-131">我们不会解释 HTML，但也不会使用任何复杂的内容。</span><span class="sxs-lookup"><span data-stu-id="4bab9-131">We won't explain HTML, but we also don't use anything complex.</span></span> <span data-ttu-id="4bab9-132">我们将提供 HTML 教程的链接，在这些教程中，我们认为它们非常有用。</span><span class="sxs-lookup"><span data-stu-id="4bab9-132">We'll provide links to HTML tutorials where we think they're useful.</span></span>
- <span data-ttu-id="4bab9-133">**级联样式表（CSS）**。</span><span class="sxs-lookup"><span data-stu-id="4bab9-133">**Cascading style sheets (CSS)**.</span></span> <span data-ttu-id="4bab9-134">与 HTML 相同。</span><span class="sxs-lookup"><span data-stu-id="4bab9-134">Same as with HTML.</span></span>
- <span data-ttu-id="4bab9-135">**基本数据库思想**。</span><span class="sxs-lookup"><span data-stu-id="4bab9-135">**Basic database ideas**.</span></span> <span data-ttu-id="4bab9-136">如果你使用了电子表格进行数据的排序和筛选，那么这就是我们通常为本教程设置的专业知识水平。</span><span class="sxs-lookup"><span data-stu-id="4bab9-136">If you've used a spreadsheet for data and sorted and filtered the data, that's the level of expertise we're generally assuming for this tutorial set.</span></span>

<span data-ttu-id="4bab9-137">我们还假定你对学习基本编程感兴趣。</span><span class="sxs-lookup"><span data-stu-id="4bab9-137">We're also assuming that you're interested in learning basic programming.</span></span> <span data-ttu-id="4bab9-138">ASP.NET 网页使用称为 c # 的编程语言。</span><span class="sxs-lookup"><span data-stu-id="4bab9-138">ASP.NET Web Pages use a programming language called C#.</span></span> <span data-ttu-id="4bab9-139">您无需在编程中使用任何背景，只需对其感兴趣。</span><span class="sxs-lookup"><span data-stu-id="4bab9-139">You don't have to have any background in programming, just an interest in it.</span></span> <span data-ttu-id="4bab9-140">如果你以前在网页中编写了任何 JavaScript，则会有许多背景知识。</span><span class="sxs-lookup"><span data-stu-id="4bab9-140">If you've ever written any JavaScript in a web page before, you've got plenty of background.</span></span>

<span data-ttu-id="4bab9-141">请注意，如果你熟悉编程，你可能会发现，此教程最初会缓慢移动，同时我们会使新的程序员保持速度缓慢。</span><span class="sxs-lookup"><span data-stu-id="4bab9-141">Note that if you are familiar with programming, you might find that this tutorial set initially moves slowly while we bring new programmers up to speed.</span></span> <span data-ttu-id="4bab9-142">不过，在我们过去的几个教程中，将会有更少的基本编程说明，并将以更快的速度移动。</span><span class="sxs-lookup"><span data-stu-id="4bab9-142">As we get past the first few tutorials, though, there will be less basic programming to explain and things will move along at a faster clip.</span></span>

## <a name="what-do-you-need"></a><span data-ttu-id="4bab9-143">你需要什么？</span><span class="sxs-lookup"><span data-stu-id="4bab9-143">What Do You Need?</span></span>

<span data-ttu-id="4bab9-144">以下是需要做好的准备：</span><span class="sxs-lookup"><span data-stu-id="4bab9-144">Here's what you'll need:</span></span>

- <span data-ttu-id="4bab9-145">运行 Windows 8、Windows 7、Windows Server 2008 或 Windows Server 2012 的计算机。</span><span class="sxs-lookup"><span data-stu-id="4bab9-145">A computer that is running Windows 8, Windows 7, Windows Server 2008, or Windows Server 2012.</span></span>
- <span data-ttu-id="4bab9-146">动态 internet 连接。</span><span class="sxs-lookup"><span data-stu-id="4bab9-146">A live internet connection.</span></span>
- <span data-ttu-id="4bab9-147">管理员权限（安装过程所必需的）。</span><span class="sxs-lookup"><span data-stu-id="4bab9-147">Administrator privileges (required for the installation process).</span></span>

## <a name="what-is-aspnet-web-pages"></a><span data-ttu-id="4bab9-148">什么是 ASP.NET 网页？</span><span class="sxs-lookup"><span data-stu-id="4bab9-148">What Is ASP.NET Web Pages?</span></span>

<span data-ttu-id="4bab9-149">ASP.NET 网页是一个框架，可用于创建动态网页。</span><span class="sxs-lookup"><span data-stu-id="4bab9-149">ASP.NET Web Pages is a framework that you can use to create dynamic web pages.</span></span> <span data-ttu-id="4bab9-150">简单的 HTML 网页是静态的;其内容取决于页面中的固定 HTML 标记。</span><span class="sxs-lookup"><span data-stu-id="4bab9-150">A simple HTML web page is static; its content is determined by the fixed HTML markup that's in the page.</span></span> <span data-ttu-id="4bab9-151">动态页面与使用 ASP.NET 网页创建的动态页面使你可以通过使用代码动态创建页面内容。</span><span class="sxs-lookup"><span data-stu-id="4bab9-151">Dynamic pages like those you create with ASP.NET Web Pages let you create the page content on the fly, by using code.</span></span>

<span data-ttu-id="4bab9-152">动态页面使你可以执行各种操作。</span><span class="sxs-lookup"><span data-stu-id="4bab9-152">Dynamic pages let you do all sorts of things.</span></span> <span data-ttu-id="4bab9-153">您可以使用窗体向用户提供输入，然后更改页面显示的内容或外观。</span><span class="sxs-lookup"><span data-stu-id="4bab9-153">You can ask a user for input by using a form and then change what the page displays or how it looks.</span></span> <span data-ttu-id="4bab9-154">你可以从用户处获取信息，将其保存在数据库中，然后在以后列出。</span><span class="sxs-lookup"><span data-stu-id="4bab9-154">You can take information from a user, save it in a database, and then list it later.</span></span> <span data-ttu-id="4bab9-155">你可以从你的站点发送电子邮件。</span><span class="sxs-lookup"><span data-stu-id="4bab9-155">You can send email from your site.</span></span> <span data-ttu-id="4bab9-156">你可以与 web 上的其他服务（例如，映射服务）进行交互，并生成集成这些源中的信息的页面。</span><span class="sxs-lookup"><span data-stu-id="4bab9-156">You can interact with other services on the web (for example, a mapping service) and produce pages that integrate information from those sources.</span></span>

## <a name="what-is-webmatrix"></a><span data-ttu-id="4bab9-157">什么是 WebMatrix？</span><span class="sxs-lookup"><span data-stu-id="4bab9-157">What is WebMatrix?</span></span>

<span data-ttu-id="4bab9-158">WebMatrix 是一种工具，可集成网页编辑器、数据库实用工具、用于测试页面的 web 服务器，以及用于将网站发布到 Internet 的功能。</span><span class="sxs-lookup"><span data-stu-id="4bab9-158">WebMatrix is a tool that integrates a web page editor, a database utility, a web server for testing pages, and features for publishing your website to the Internet.</span></span> <span data-ttu-id="4bab9-159">WebMatrix 是免费的，易于安装和使用。</span><span class="sxs-lookup"><span data-stu-id="4bab9-159">WebMatrix is free, and it's easy to install and easy to use.</span></span> <span data-ttu-id="4bab9-160">（它还适用于纯 HTML 页面以及 PHP 等其他技术。）</span><span class="sxs-lookup"><span data-stu-id="4bab9-160">(It also works for just plain HTML pages, as well as for other technologies like PHP.)</span></span>

<span data-ttu-id="4bab9-161">你实际上不*需要*使用 WebMatrix 来处理 ASP.NET 网页。</span><span class="sxs-lookup"><span data-stu-id="4bab9-161">You don't actually *have* to use WebMatrix to work with ASP.NET Web Pages.</span></span> <span data-ttu-id="4bab9-162">例如，您可以使用文本编辑器创建页面，并使用您有权访问的 web 服务器来测试页面。</span><span class="sxs-lookup"><span data-stu-id="4bab9-162">You can create pages by using a text editor, for example, and test pages by using a web server that you have access to.</span></span> <span data-ttu-id="4bab9-163">不过，WebMatrix 使其变得非常简单，因此这些教程将在整个过程中使用 WebMatrix。</span><span class="sxs-lookup"><span data-stu-id="4bab9-163">However, WebMatrix makes it all very easy, so these tutorials will use WebMatrix throughout.</span></span>

## <a name="about-these-tutorials"></a><span data-ttu-id="4bab9-164">关于这些教程</span><span class="sxs-lookup"><span data-stu-id="4bab9-164">About These Tutorials</span></span>

<span data-ttu-id="4bab9-165">本教程集介绍了如何使用 ASP.NET 网页。</span><span class="sxs-lookup"><span data-stu-id="4bab9-165">This tutorial set is an introduction to how to use ASP.NET Web Pages.</span></span> <span data-ttu-id="4bab9-166">此介绍性教程集中有9个教程总计。</span><span class="sxs-lookup"><span data-stu-id="4bab9-166">There are 9 tutorials total in this introductory tutorial set.</span></span> <span data-ttu-id="4bab9-167">这是一系列教程集的一部分，可让你从 ASP.NET 网页初级网站创建真实的、具有专业外观的网站。</span><span class="sxs-lookup"><span data-stu-id="4bab9-167">It's part of a series of tutorial sets that takes you from ASP.NET Web Pages novice to creating real, professional-looking websites.</span></span>

<span data-ttu-id="4bab9-168">这首个教程集重点介绍了如何使用 ASP.NET 网页的基础知识。</span><span class="sxs-lookup"><span data-stu-id="4bab9-168">This first tutorial set concentrates on showing you the basics of how to work with ASP.NET Web Pages.</span></span> <span data-ttu-id="4bab9-169">完成此操作后，可以使用额外的教程集，该教程集选择该程序集的结尾，更深入地浏览网页。</span><span class="sxs-lookup"><span data-stu-id="4bab9-169">When you're done, you can work with additional tutorial sets that pick up where this one ends and that explore Web Pages in more depth.</span></span>

<span data-ttu-id="4bab9-170">我们特意了解更深入的说明。</span><span class="sxs-lookup"><span data-stu-id="4bab9-170">We deliberately go easy on the in-depth explanations.</span></span> <span data-ttu-id="4bab9-171">无论何时，对于本教程，我们始终都选择最容易理解的方式。</span><span class="sxs-lookup"><span data-stu-id="4bab9-171">And whenever we show something, for this tutorial set we always choose the way that we think is easiest to understand.</span></span> <span data-ttu-id="4bab9-172">稍后的教程集将深入了解更多，并显示更高效或更灵活的方法（也更有趣）。</span><span class="sxs-lookup"><span data-stu-id="4bab9-172">Later tutorial sets go into more depth and show you more efficient or more flexible approaches (also more fun).</span></span> <span data-ttu-id="4bab9-173">但这些教程要求首先了解基础知识。</span><span class="sxs-lookup"><span data-stu-id="4bab9-173">But those tutorials require you to understand the basics first.</span></span>

<span data-ttu-id="4bab9-174">刚开始的教程集介绍了 ASP.NET 网页的这些功能：</span><span class="sxs-lookup"><span data-stu-id="4bab9-174">The tutorial set you've just started covers these features of ASP.NET Web Pages:</span></span>

- <span data-ttu-id="4bab9-175">简介并获取安装的所有内容。</span><span class="sxs-lookup"><span data-stu-id="4bab9-175">Introduction and getting everything installed.</span></span> <span data-ttu-id="4bab9-176">（在阅读教程中。）</span><span class="sxs-lookup"><span data-stu-id="4bab9-176">(That's in the tutorial you're reading.)</span></span>
- <span data-ttu-id="4bab9-177">ASP.NET 网页编程的基础知识。</span><span class="sxs-lookup"><span data-stu-id="4bab9-177">The basics of ASP.NET Web Pages programming.</span></span>
- <span data-ttu-id="4bab9-178">创建数据库。</span><span class="sxs-lookup"><span data-stu-id="4bab9-178">Creating a database.</span></span>
- <span data-ttu-id="4bab9-179">创建和处理用户输入窗体。</span><span class="sxs-lookup"><span data-stu-id="4bab9-179">Creating and processing a user input form.</span></span>
- <span data-ttu-id="4bab9-180">添加、更新和删除数据库中的数据。</span><span class="sxs-lookup"><span data-stu-id="4bab9-180">Adding, updating, and deleting data in the database.</span></span>

## <a name="what-will-you-create"></a><span data-ttu-id="4bab9-181">你将创建哪些内容？</span><span class="sxs-lookup"><span data-stu-id="4bab9-181">What Will You Create?</span></span>

<span data-ttu-id="4bab9-182">本教程集和后续教程将在网站上进行旋转，你可以在其中列出你喜欢的电影。</span><span class="sxs-lookup"><span data-stu-id="4bab9-182">This tutorial set and subsequent ones revolve around a website where you can list movies that you like.</span></span> <span data-ttu-id="4bab9-183">你将能够输入电影、进行编辑并列出它们。</span><span class="sxs-lookup"><span data-stu-id="4bab9-183">You'll be able to enter movies, edit them, and list them.</span></span> <span data-ttu-id="4bab9-184">下面是要在本教程集中创建的几个页面。</span><span class="sxs-lookup"><span data-stu-id="4bab9-184">Here are a couple of the pages you'll create in this tutorial set.</span></span> <span data-ttu-id="4bab9-185">第一个示例显示要创建的电影列表页：</span><span class="sxs-lookup"><span data-stu-id="4bab9-185">The first one shows the movie listing page that you'll create:</span></span>

![显示电影列表的已完成影片应用](getting-started/_static/image1.png)

<span data-ttu-id="4bab9-187">以下页面使你能够将新电影信息添加到你的网站：</span><span class="sxs-lookup"><span data-stu-id="4bab9-187">And here's the page that lets you add new movie information to your site:</span></span>

![已完成显示 "添加电影" 页面的电影应用](getting-started/_static/image2.png)

<span data-ttu-id="4bab9-189">后续教程将基于此集进行构建并添加更多功能，如上传图片、让用户登录、发送电子邮件以及与社交媒体集成。</span><span class="sxs-lookup"><span data-stu-id="4bab9-189">Subsequent tutorial sets build on this set and add more functionality, like uploading pictures, letting people log in, sending email, and integrating with social media.</span></span>

## <a name="see-this-app-running-on-azure"></a><span data-ttu-id="4bab9-190">查看此应用在 Azure 上运行</span><span class="sxs-lookup"><span data-stu-id="4bab9-190">See this App Running on Azure</span></span>

<span data-ttu-id="4bab9-191">要查看作为实时 web 应用运行的已完成站点吗？</span><span class="sxs-lookup"><span data-stu-id="4bab9-191">Would you like to see the finished site running as a live web app?</span></span> <span data-ttu-id="4bab9-192">只需单击以下按钮，即可将应用程序的完整版本部署到 Azure 帐户。</span><span class="sxs-lookup"><span data-stu-id="4bab9-192">You can deploy a complete version of the app to your Azure account by simply clicking the following button.</span></span>

[![](http://azuredeploy.net/deploybutton.png)](https://azuredeploy.net/?WT.mc_id=deploy_azure_aspnet&repository=https://github.com/tfitzmac/WebPagesMovies)

<span data-ttu-id="4bab9-193">需要一个 Azure 帐户才能将此解决方案部署到 Azure。</span><span class="sxs-lookup"><span data-stu-id="4bab9-193">You need an Azure account to deploy this solution to Azure.</span></span> <span data-ttu-id="4bab9-194">如果还没有帐户，可以使用以下选项：</span><span class="sxs-lookup"><span data-stu-id="4bab9-194">If you do not already have an account, you have the following options:</span></span>

- <span data-ttu-id="4bab9-195">[免费打开 Azure 帐户](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604)-获取可用来试用付费版 Azure 服务的信用额度，甚至在用完信用额度后，你仍可以保留帐户和使用免费的 azure 服务。</span><span class="sxs-lookup"><span data-stu-id="4bab9-195">[Open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) - You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services.</span></span>
- <span data-ttu-id="4bab9-196">[激活 msdn 订户权益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604)-msdn 订阅每月提供可用于付费 Azure 服务的信用额度。</span><span class="sxs-lookup"><span data-stu-id="4bab9-196">[Activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) - Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>

## <a name="installing-everything"></a><span data-ttu-id="4bab9-197">安装一切</span><span class="sxs-lookup"><span data-stu-id="4bab9-197">Installing Everything</span></span>

<span data-ttu-id="4bab9-198">你可以使用 Microsoft 的 Web 平台安装程序安装所有内容。</span><span class="sxs-lookup"><span data-stu-id="4bab9-198">You can install everything by using the Web Platform Installer from Microsoft.</span></span> <span data-ttu-id="4bab9-199">实际上，你安装了安装程序，然后使用它来安装其他所有内容。</span><span class="sxs-lookup"><span data-stu-id="4bab9-199">In effect, you install the installer, and then use it to install everything else.</span></span>

<span data-ttu-id="4bab9-200">若要使用网页，至少需要安装 Windows XP SP3 或 Windows Server 2008 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="4bab9-200">To use Web Pages, you have to be have at least Windows XP with SP3 installed, or Windows Server 2008 or later.</span></span>

<span data-ttu-id="4bab9-201">在 ASP.NET 网站的 "网页"[页](../../../index.md)上，单击 "**安装**"。</span><span class="sxs-lookup"><span data-stu-id="4bab9-201">On the [Web Pages page](../../../index.md) of the ASP.NET website, click **Install**.</span></span>

![显示 " &quot; 安装 WebMatrix" 按钮的 ASP.NET 网站 &quot;](getting-started/_static/image3.png)

<span data-ttu-id="4bab9-203">安装 WebMatrix 之前，系统会要求你接受许可条款和隐私声明。</span><span class="sxs-lookup"><span data-stu-id="4bab9-203">You are asked to accept the license terms and privacy statement before installing WebMatrix.</span></span>

![接受字词开始安装](getting-started/_static/image4.png)

<span data-ttu-id="4bab9-205">单击 "**运行**" 以启动安装。</span><span class="sxs-lookup"><span data-stu-id="4bab9-205">Click **Run** to start the installation.</span></span> <span data-ttu-id="4bab9-206">（如果要保存该安装程序，请单击 "**保存**"，然后从保存该安装程序的文件夹运行该安装程序。）</span><span class="sxs-lookup"><span data-stu-id="4bab9-206">(If you want to save the installer, click **Save** and then run the installer from the folder where you saved it.)</span></span>

![](getting-started/_static/image5.png)

<span data-ttu-id="4bab9-207">此时会显示 "Web 平台安装程序"，可以安装 WebMatrix 了。</span><span class="sxs-lookup"><span data-stu-id="4bab9-207">The Web Platform Installer appears, ready to install WebMatrix.</span></span> <span data-ttu-id="4bab9-208">单击“安装”。</span><span class="sxs-lookup"><span data-stu-id="4bab9-208">Click **Install**.</span></span>

![](getting-started/_static/image6.png)

<span data-ttu-id="4bab9-209">安装过程将找出必须在计算机上安装的内容，然后启动该过程。</span><span class="sxs-lookup"><span data-stu-id="4bab9-209">The installation process figures out what it has to install on your computer and starts the process.</span></span> <span data-ttu-id="4bab9-210">根据确切安装的内容，该过程可能需要几分钟到几分钟的时间。</span><span class="sxs-lookup"><span data-stu-id="4bab9-210">Depending on what exactly has to be installed, the process can take anywhere from a few moments to several minutes.</span></span> <span data-ttu-id="4bab9-211">选择 "**我接受**" 接受许可条款。</span><span class="sxs-lookup"><span data-stu-id="4bab9-211">Select **I Accept** to accept the license terms.</span></span>

## <a name="hello-webmatrix"></a><span data-ttu-id="4bab9-212">你好，WebMatrix</span><span class="sxs-lookup"><span data-stu-id="4bab9-212">Hello, WebMatrix</span></span>

<span data-ttu-id="4bab9-213">完成后，安装过程可以自动启动 WebMatrix。</span><span class="sxs-lookup"><span data-stu-id="4bab9-213">When it's done, the installation process can launch WebMatrix automatically.</span></span> <span data-ttu-id="4bab9-214">如果不是，在 Windows 中，从 "**开始**" 菜单启动 " **Microsoft WebMatrix**"。</span><span class="sxs-lookup"><span data-stu-id="4bab9-214">If it doesn't, in Windows, from the **Start** menu, launch **Microsoft WebMatrix**.</span></span>

<span data-ttu-id="4bab9-215">首次启动 WebMatrix 时，有机会使用 Microsoft 帐户登录到 Microsoft Azure。</span><span class="sxs-lookup"><span data-stu-id="4bab9-215">When you launch WebMatrix for the first time, you are given a chance to sign in to Microsoft Azure with your Microsoft account.</span></span> <span data-ttu-id="4bab9-216">登录后，你将通过 Azure 接收10个免费的 web 应用。</span><span class="sxs-lookup"><span data-stu-id="4bab9-216">By signing in, you will receive 10 free web apps through Azure.</span></span> <span data-ttu-id="4bab9-217">这些免费的 web 应用提供了一种方便的方法来测试你的应用。</span><span class="sxs-lookup"><span data-stu-id="4bab9-217">These free web apps provide a convenient way to test your apps.</span></span> <span data-ttu-id="4bab9-218">如果还没有 Azure 帐户，但有 MSDN 订阅，则可以[激活 msdn 订阅权益](https://www.windowsazure.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604)。</span><span class="sxs-lookup"><span data-stu-id="4bab9-218">If you don't already have an Azure account, but you do have an MSDN subscription, you can [activate your MSDN subscription benefits](https://www.windowsazure.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604).</span></span> <span data-ttu-id="4bab9-219">否则，只需花费几分钟就能创建一个免费试用帐户。</span><span class="sxs-lookup"><span data-stu-id="4bab9-219">Otherwise, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="4bab9-220">有关详细信息，请参阅 [Azure 免费试用](https://azure.microsoft.com/free/dotnet/)。</span><span class="sxs-lookup"><span data-stu-id="4bab9-220">For details, see [Azure Free Trial](https://azure.microsoft.com/free/dotnet/).</span></span>

<span data-ttu-id="4bab9-221">你现在无需登录即可继续学习本教程。</span><span class="sxs-lookup"><span data-stu-id="4bab9-221">You do not have to sign in right now to continue with this tutorial.</span></span> <span data-ttu-id="4bab9-222">如果你现在不登录，则你仍可以选择在以后登录。</span><span class="sxs-lookup"><span data-stu-id="4bab9-222">If you do not sign in now, you will still have the option to sign in later.</span></span> <span data-ttu-id="4bab9-223">本系列教程的最后一个[主题](publishing.md)介绍如何将网站部署到 Azure;因此，您需要登录才能完成该主题。</span><span class="sxs-lookup"><span data-stu-id="4bab9-223">The last [topic](publishing.md) in this tutorial series covers how to deploy your website to Azure; therefore, you would need to sign in to complete that topic.</span></span>

<span data-ttu-id="4bab9-224">此时，请用 Microsoft 帐户登录，或在右下角选择 "**不**是"。</span><span class="sxs-lookup"><span data-stu-id="4bab9-224">At this point, either sign in with your Microsoft account or select **Not Now** in the lower right corner.</span></span>

![登录](getting-started/_static/image7.png)

<span data-ttu-id="4bab9-226">首先，你将创建一个空白网站并添加一个页面。</span><span class="sxs-lookup"><span data-stu-id="4bab9-226">To begin, you'll create a blank website and add a page.</span></span> <span data-ttu-id="4bab9-227">在后面的教程中，你将使用一个内置的网站模板。</span><span class="sxs-lookup"><span data-stu-id="4bab9-227">In a later tutorial in this set you'll play with one of the built-in website templates.</span></span>

<span data-ttu-id="4bab9-228">在 "开始" 窗口中，单击 "**新建**"。</span><span class="sxs-lookup"><span data-stu-id="4bab9-228">In the start window, click **New**.</span></span>

![WebMatrix 启动屏幕](getting-started/_static/image8.png)

<span data-ttu-id="4bab9-230">模板是为不同类型的网站预先构建的文件和页。</span><span class="sxs-lookup"><span data-stu-id="4bab9-230">Templates are prebuilt files and pages for different types of websites.</span></span> <span data-ttu-id="4bab9-231">若要查看默认情况下可用的所有模板，请选择 "模板库" 选项。</span><span class="sxs-lookup"><span data-stu-id="4bab9-231">To see all of the templates that are available by default, select the Template Gallery option.</span></span>

![选择模板库](getting-started/_static/image9.png)

<span data-ttu-id="4bab9-233">在 "**快速入门**" 窗口中，从**ASP.NET**组中选择 "**空站点**"，并将新站点命名为 "WebPagesMovies"。</span><span class="sxs-lookup"><span data-stu-id="4bab9-233">In the **Quick Start** window, select **Empty Site** from the **ASP.NET** group and name the new site "WebPagesMovies".</span></span>

![选定了空站点模板的 WebMatrix 快速入门窗口](getting-started/_static/image10.png)

<span data-ttu-id="4bab9-235">单击“下一步”。</span><span class="sxs-lookup"><span data-stu-id="4bab9-235">Click **Next**.</span></span>

<span data-ttu-id="4bab9-236">如果已登录到 Microsoft 帐户，则可以在 Azure 上创建网站。</span><span class="sxs-lookup"><span data-stu-id="4bab9-236">If you have signed in to your Microsoft account, you will be given the opportunity to create the site on Azure.</span></span> <span data-ttu-id="4bab9-237">根据你的站点的名称，建议默认名称**WebPagesMovies.azurewebsites.net** ;但是，感叹号表示此名称在 Windows Azure 上不可用。</span><span class="sxs-lookup"><span data-stu-id="4bab9-237">Based on the name of your site, the default name of **WebPagesMovies.azurewebsites.net** is suggested; however, the exclamation point indicates that this name is not available on Windows Azure.</span></span> <span data-ttu-id="4bab9-238">为简单起见，请选择 "**跳过**" 以跳过在 Azure 上立即创建网站。</span><span class="sxs-lookup"><span data-stu-id="4bab9-238">For simplicity, select **Skip** to bypass creating the web site on Azure right now.</span></span> <span data-ttu-id="4bab9-239">稍后在本系列中，我们会将该站点发布到 Azure。</span><span class="sxs-lookup"><span data-stu-id="4bab9-239">Later in this series, we will publish the site to Azure.</span></span>

![创建 azure 站点](getting-started/_static/image11.png)

<span data-ttu-id="4bab9-241">WebMatrix 创建并打开站点：</span><span class="sxs-lookup"><span data-stu-id="4bab9-241">WebMatrix creates and opens the site:</span></span>

![在 WebMatrix 中打开的新 WebPagesMovies 网站](getting-started/_static/image12.png)

<span data-ttu-id="4bab9-243">顶部有一个快速访问工具栏和一个功能区。</span><span class="sxs-lookup"><span data-stu-id="4bab9-243">At the top, there's a Quick Access Toolbar and a ribbon.</span></span> <span data-ttu-id="4bab9-244">左下角显示工作区选择器，可在其中切换任务（**站点**、**文件**、**数据库**、**报表**）。</span><span class="sxs-lookup"><span data-stu-id="4bab9-244">At the bottom left, you see the workspace selector where you switch between tasks (**Site**, **Files**, **Databases**, **Reports**).</span></span> <span data-ttu-id="4bab9-245">右侧是编辑器和报表的内容窗格。</span><span class="sxs-lookup"><span data-stu-id="4bab9-245">On the right is the content pane for the editor and for reports.</span></span> <span data-ttu-id="4bab9-246">在底部，你将偶尔看到消息的通知栏。</span><span class="sxs-lookup"><span data-stu-id="4bab9-246">And across the bottom you'll occasionally see a notification bar for messages.</span></span>

<span data-ttu-id="4bab9-247">完成这些教程后，你将了解有关 WebMatrix 及其功能的详细信息。</span><span class="sxs-lookup"><span data-stu-id="4bab9-247">You'll learn more about WebMatrix and its features as you go through these tutorials.</span></span>

## <a name="creating-a-web-page"></a><span data-ttu-id="4bab9-248">创建网页</span><span class="sxs-lookup"><span data-stu-id="4bab9-248">Creating a Web Page</span></span>

<span data-ttu-id="4bab9-249">为了熟悉 WebMatrix 和 ASP.NET 网页，你将创建一个简单的页面。</span><span class="sxs-lookup"><span data-stu-id="4bab9-249">To become familiar with WebMatrix and ASP.NET Web Pages, you'll create a simple page.</span></span>

<span data-ttu-id="4bab9-250">在工作区选择器中，选择 "**文件**" 工作区。</span><span class="sxs-lookup"><span data-stu-id="4bab9-250">In the workspace selector, select the **Files** workspace.</span></span> <span data-ttu-id="4bab9-251">使用此工作区可以处理文件和文件夹。</span><span class="sxs-lookup"><span data-stu-id="4bab9-251">This workspace lets you work with files and folders.</span></span> <span data-ttu-id="4bab9-252">左窗格显示了站点的文件结构。</span><span class="sxs-lookup"><span data-stu-id="4bab9-252">The left pane shows the file structure of your site.</span></span> <span data-ttu-id="4bab9-253">功能区更改为显示与文件相关的任务。</span><span class="sxs-lookup"><span data-stu-id="4bab9-253">The ribbon changes to show file-related tasks.</span></span>

![WebMatrix 中的文件工作区](getting-started/_static/image13.png)

<span data-ttu-id="4bab9-255">在功能区中，单击 "**新建**" 下的箭头，然后单击 "**新建文件**"。</span><span class="sxs-lookup"><span data-stu-id="4bab9-255">In the ribbon, click the arrow under **New** and then click **New File**.</span></span>

![使用 &quot; 功能区中的 "新建" &quot; 命令创建新文件](getting-started/_static/image14.png)

<span data-ttu-id="4bab9-257">WebMatrix 显示文件类型的列表。</span><span class="sxs-lookup"><span data-stu-id="4bab9-257">WebMatrix displays a list of file types.</span></span> <span data-ttu-id="4bab9-258">选择 " **CSHTML**"，然后在 "**名称**" 框中，键入 "HelloWorld"。</span><span class="sxs-lookup"><span data-stu-id="4bab9-258">Select **CSHTML**, and in the **Name** box, type "HelloWorld".</span></span> <span data-ttu-id="4bab9-259">CSHTML 页面是 ASP.NET 网页页面。</span><span class="sxs-lookup"><span data-stu-id="4bab9-259">A CSHTML page is an ASP.NET Web Pages page.</span></span>

![创建名为 HelloWorld 的新 CSHTML 页](getting-started/_static/image15.png)

<span data-ttu-id="4bab9-261">单击“确定”。</span><span class="sxs-lookup"><span data-stu-id="4bab9-261">Click **OK**.</span></span>

<span data-ttu-id="4bab9-262">WebMatrix 创建页面并在编辑器中打开它。</span><span class="sxs-lookup"><span data-stu-id="4bab9-262">WebMatrix creates the page and opens it in the editor.</span></span>

![WebMatrix 编辑器中的新 "HelloWorld" 页](getting-started/_static/image16.png)

<span data-ttu-id="4bab9-264">正如您所看到的，页面通常包含普通的 HTML 标记，其中顶部的块如下所示：</span><span class="sxs-lookup"><span data-stu-id="4bab9-264">As you can see, the page contains mostly ordinary HTML markup, except for a block at the top that looks like this:</span></span>

[!code-cshtml[Main](getting-started/samples/sample1.cshtml)]

<span data-ttu-id="4bab9-265">这就是添加代码的，正如您很快所见。</span><span class="sxs-lookup"><span data-stu-id="4bab9-265">That's for adding code, as you'll see shortly.</span></span>

<span data-ttu-id="4bab9-266">请注意， &mdash; 元素名称、属性和文本以及顶部块的不同部分均采用不同的颜色。</span><span class="sxs-lookup"><span data-stu-id="4bab9-266">Notice that the different parts of the page &mdash; the element names, attributes, and text, plus the block at the top — are all in different colors.</span></span> <span data-ttu-id="4bab9-267">这称为*语法突出显示*，使所有内容保持清晰。</span><span class="sxs-lookup"><span data-stu-id="4bab9-267">This is called *syntax highlighting*, and it makes it easier to keep everything clear.</span></span> <span data-ttu-id="4bab9-268">这是一项功能，使用它可以轻松地在 WebMatrix 中使用网页。</span><span class="sxs-lookup"><span data-stu-id="4bab9-268">It's one of the features that makes it easy to work with web pages in WebMatrix.</span></span>

<span data-ttu-id="4bab9-269">为 `<head>` 和元素添加内容， `<body>` 如以下示例中所示。</span><span class="sxs-lookup"><span data-stu-id="4bab9-269">Add content for the `<head>` and `<body>` elements like in the following example.</span></span> <span data-ttu-id="4bab9-270">（如果需要，可以只复制以下块，并将整个现有页面替换为此代码。）</span><span class="sxs-lookup"><span data-stu-id="4bab9-270">(If you want, you can just copy the following block and replace the entire existing page with this code.)</span></span>

[!code-cshtml[Main](getting-started/samples/sample2.cshtml)]

<span data-ttu-id="4bab9-271">在快速访问工具栏或 "**文件**" 菜单中，单击 "**保存**"。</span><span class="sxs-lookup"><span data-stu-id="4bab9-271">In the Quick Access Toolbar or in the **File** menu, click **Save**.</span></span>

![WebMatrix 快速访问工具栏中的 "保存" 按钮](getting-started/_static/image17.png)

## <a name="testing-the-page"></a><span data-ttu-id="4bab9-273">测试页面</span><span class="sxs-lookup"><span data-stu-id="4bab9-273">Testing the Page</span></span>

<span data-ttu-id="4bab9-274">在 "**文件**" 工作区中，右键单击 " *HelloWorld* " 页，然后单击 "**在浏览器中启动**"。</span><span class="sxs-lookup"><span data-stu-id="4bab9-274">In the **Files** workspace, right-click the *HelloWorld.cshtml* page and then click **Launch in browser**.</span></span>

![使用 WebMatrix 功能区中的 "运行" 按钮运行页面](getting-started/_static/image18.png)

<span data-ttu-id="4bab9-276">WebMatrix 启动可用于在计算机上测试页面的内置 web 服务器（IIS Express）。</span><span class="sxs-lookup"><span data-stu-id="4bab9-276">WebMatrix starts a built-in web server (IIS Express) that you can use to test pages on your computer.</span></span> <span data-ttu-id="4bab9-277">（无需在 WebMatrix 中 IIS Express，你必须将页面发布到 web 服务器上的某个位置，然后才能对其进行测试。）页面将显示在默认浏览器中。</span><span class="sxs-lookup"><span data-stu-id="4bab9-277">(Without IIS Express in WebMatrix, you'd have to publish your page to a web server somewhere before you could test it.) The page is displayed in your default browser.</span></span>

![&quot;&quot;在浏览器中运行的 Hello World 页面](getting-started/_static/image19.png)

<span data-ttu-id="4bab9-279">请注意，当你在 WebMatrix 中测试某个页面时，浏览器中的 URL 类似于 `http://localhost:33651/HelloWorld.cshtml.` 名称*localhost* ，这就是指本地服务器，这意味着该页由你自己的计算机上的 web 服务器提供服务。</span><span class="sxs-lookup"><span data-stu-id="4bab9-279">Notice that when you test a page in WebMatrix, the URL in the browser is something like `http://localhost:33651/HelloWorld.cshtml.` The name *localhost* refers to a local server, meaning that the page is served by a web server that's on your own computer.</span></span> <span data-ttu-id="4bab9-280">如上所述，WebMatrix 包含一个名为 IIS Express 的 web 服务器程序，该程序在启动页面时运行。</span><span class="sxs-lookup"><span data-stu-id="4bab9-280">As noted, WebMatrix includes a web server program named IIS Express that runs when you launch a page.</span></span>

<span data-ttu-id="4bab9-281">*Localhost*后面的数字（例如*localhost： 33651*）是指计算机上的*端口号*。</span><span class="sxs-lookup"><span data-stu-id="4bab9-281">The number after *localhost* (for example, *localhost:33651*) refers to a *port number* on your computer.</span></span> <span data-ttu-id="4bab9-282">这是 IIS Express 用于此特定网站的 "通道" 号。</span><span class="sxs-lookup"><span data-stu-id="4bab9-282">This is the number of the "channel" that IIS Express uses for this particular website.</span></span> <span data-ttu-id="4bab9-283">创建站点时，从1024到65536的范围内随机选择端口号，而创建的每个站点都是不同的。</span><span class="sxs-lookup"><span data-stu-id="4bab9-283">The port number is selected at random from the range 1024 through 65536 when you create your site, and it's different for every site that you create.</span></span> <span data-ttu-id="4bab9-284">（测试自己的站点时，端口号几乎肯定会与33561不同。）通过为每个网站使用不同的端口，IIS Express 可以使其与你的站点直接通信。</span><span class="sxs-lookup"><span data-stu-id="4bab9-284">(When you test your own site, the port number will almost certainly be a different number than 33561.) By using a different port for each website, IIS Express can keep straight which of your sites it's talking to.</span></span>

<span data-ttu-id="4bab9-285">稍后，当你将站点发布到公共 web 服务器时，你将不会再看到 URL 中的*localhost* 。</span><span class="sxs-lookup"><span data-stu-id="4bab9-285">Later when you publish your site to a public web server, you no longer see *localhost* in the URL.</span></span> <span data-ttu-id="4bab9-286">此时，您将看到更典型的 URL，例如 `http://myhostingsite/mywebsite/HelloWorld.cshtml` 或页面的任何内容。</span><span class="sxs-lookup"><span data-stu-id="4bab9-286">At that point, you'll see a more typical URL like `http://myhostingsite/mywebsite/HelloWorld.cshtml` or whatever the page is.</span></span> <span data-ttu-id="4bab9-287">你将在本系列教程的后面部分了解有关发布站点的详细信息。</span><span class="sxs-lookup"><span data-stu-id="4bab9-287">You'll learn more about publishing a site later in this tutorial series.</span></span>

## <a name="adding-some-server-side-code"></a><span data-ttu-id="4bab9-288">添加一些服务器端代码</span><span class="sxs-lookup"><span data-stu-id="4bab9-288">Adding Some Server-Side Code</span></span>

<span data-ttu-id="4bab9-289">关闭浏览器并返回到 WebMatrix 中的页面。</span><span class="sxs-lookup"><span data-stu-id="4bab9-289">Close the browser and go back to the page in WebMatrix.</span></span>

<span data-ttu-id="4bab9-290">在代码块中添加一行，使其类似于以下代码：</span><span class="sxs-lookup"><span data-stu-id="4bab9-290">Add a line to the code block so that it looks like the following code:</span></span>

[!code-cshtml[Main](getting-started/samples/sample3.cshtml)]

<span data-ttu-id="4bab9-291">这只是一些 Razor 代码。</span><span class="sxs-lookup"><span data-stu-id="4bab9-291">This is a little bit of Razor code.</span></span> <span data-ttu-id="4bab9-292">很明显，它会获取当前日期和时间，并将该值放入名为的*变量*中 `currentDateTime` 。</span><span class="sxs-lookup"><span data-stu-id="4bab9-292">It's probably clear that it gets the current date and time and puts that value into a *variable* named `currentDateTime`.</span></span> <span data-ttu-id="4bab9-293">你将在下一教程中详细了解 Razor 语法。</span><span class="sxs-lookup"><span data-stu-id="4bab9-293">You'll read more about Razor syntax in the next tutorial.</span></span>

<span data-ttu-id="4bab9-294">在页面的正文中，在元素后面 `<p>Hello World!</p>` 添加以下内容：</span><span class="sxs-lookup"><span data-stu-id="4bab9-294">In the body of the page, after the `<p>Hello World!</p>` element, add the following:</span></span>

[!code-html[Main](getting-started/samples/sample4.html)]

<span data-ttu-id="4bab9-295">此代码将获取在顶部置于变量中的值 `currentDateTime` ，并将其插入到页面的标记中。</span><span class="sxs-lookup"><span data-stu-id="4bab9-295">This code gets the value that you put into the `currentDateTime` variable at the top and inserts it into the markup of the page.</span></span> <span data-ttu-id="4bab9-296">`@`字符标记页面中的 ASP.NET 网页代码。</span><span class="sxs-lookup"><span data-stu-id="4bab9-296">The `@` character marks the ASP.NET Web Pages code in the page.</span></span>

<span data-ttu-id="4bab9-297">再次运行页面（WebMatrix 会在运行页面之前保存更改）。</span><span class="sxs-lookup"><span data-stu-id="4bab9-297">Run the page again (WebMatrix saves the changes for you before it runs the page).</span></span> <span data-ttu-id="4bab9-298">此时会在页面中看到日期和时间。</span><span class="sxs-lookup"><span data-stu-id="4bab9-298">This time you see the date and time in the page.</span></span>

![&quot;&quot;在浏览器中运行的 Hello World 页面，其中包含动态生成的时间显示](getting-started/_static/image20.png)

<span data-ttu-id="4bab9-300">稍等片刻，然后在浏览器中刷新页面。</span><span class="sxs-lookup"><span data-stu-id="4bab9-300">Wait a few moments and then refresh the page in the browser.</span></span> <span data-ttu-id="4bab9-301">更新日期和时间。</span><span class="sxs-lookup"><span data-stu-id="4bab9-301">The date and time display is updated.</span></span>

<span data-ttu-id="4bab9-302">在浏览器中，查看页面源。</span><span class="sxs-lookup"><span data-stu-id="4bab9-302">In the browser, look at the page source.</span></span> <span data-ttu-id="4bab9-303">它类似于以下标记：</span><span class="sxs-lookup"><span data-stu-id="4bab9-303">It looks like the following markup:</span></span>

[!code-html[Main](getting-started/samples/sample5.html)]

<span data-ttu-id="4bab9-304">请注意， `@{ }` 顶部的块不存在。</span><span class="sxs-lookup"><span data-stu-id="4bab9-304">Notice that the `@{ }` block at the top isn't there.</span></span> <span data-ttu-id="4bab9-305">另请注意，"日期和时间" 显示将显示实际的字符串（ `1/18/2012 2:49:50 PM` 或任何内容），而不是 `@currentDateTime` 像在 *.* # 页中一样。</span><span class="sxs-lookup"><span data-stu-id="4bab9-305">Also notice that the date and time display shows an actual string of characters (`1/18/2012 2:49:50 PM` or whatever), not `@currentDateTime` like you had in the *.cshtml* page.</span></span> <span data-ttu-id="4bab9-306">这里发生的情况是，当你运行页面时，ASP.NET 处理了标记为的所有代码（在此例中很少） `@` 。</span><span class="sxs-lookup"><span data-stu-id="4bab9-306">What happened here is that when you ran the page, ASP.NET processed all the code (very little in this case) that was marked with `@`.</span></span> <span data-ttu-id="4bab9-307">此代码生成输出，并将输出插入到页面中。</span><span class="sxs-lookup"><span data-stu-id="4bab9-307">The code produces output, and that output was inserted into the page.</span></span>

## <a name="this-is-what-aspnet-web-pages-are-about"></a><span data-ttu-id="4bab9-308">这就是 ASP.NET 网页的内容</span><span class="sxs-lookup"><span data-stu-id="4bab9-308">This Is What ASP.NET Web Pages Are About</span></span>

<span data-ttu-id="4bab9-309">当你阅读该 ASP.NET 网页生成动态 Web 内容时，你在这里看到的就是这种想法。</span><span class="sxs-lookup"><span data-stu-id="4bab9-309">When you read that ASP.NET Web Pages produces dynamic web content, what you've seen here is the idea.</span></span> <span data-ttu-id="4bab9-310">刚创建的页面包含之前看到的相同 HTML 标记。</span><span class="sxs-lookup"><span data-stu-id="4bab9-310">The page you just created contains the same HTML markup that you've seen before.</span></span> <span data-ttu-id="4bab9-311">它还可以包含可执行各种任务的代码。</span><span class="sxs-lookup"><span data-stu-id="4bab9-311">It can also contain code that can perform all sorts of tasks.</span></span> <span data-ttu-id="4bab9-312">在此示例中，它是获取当前日期和时间的简单任务。</span><span class="sxs-lookup"><span data-stu-id="4bab9-312">In this example, it did the trivial task of getting the current date and time.</span></span> <span data-ttu-id="4bab9-313">正如您所看到的，可以在页面中点播带有 HTML 的代码以生成输出。</span><span class="sxs-lookup"><span data-stu-id="4bab9-313">As you saw, you can intersperse code with the HTML to produce output in the page.</span></span> <span data-ttu-id="4bab9-314">当某个人请求浏览器中的*ASP.NET 页时*，会在该页面仍处于 web 服务器时对其进行处理。</span><span class="sxs-lookup"><span data-stu-id="4bab9-314">When someone requests a *.cshtml* page in the browser, ASP.NET processes the page while it's still in the hands of the web server.</span></span> <span data-ttu-id="4bab9-315">ASP.NET 将代码（如果有）的输出作为 HTML 插入到页面中。</span><span class="sxs-lookup"><span data-stu-id="4bab9-315">ASP.NET inserts the output of the code (if any) into the page as HTML.</span></span> <span data-ttu-id="4bab9-316">完成代码处理后，ASP.NET 会将生成的页发送到浏览器。</span><span class="sxs-lookup"><span data-stu-id="4bab9-316">When the code processing is done, ASP.NET sends the resulting page to the browser.</span></span> <span data-ttu-id="4bab9-317">所有浏览器都是 HTML。</span><span class="sxs-lookup"><span data-stu-id="4bab9-317">All the browser ever gets is HTML.</span></span> <span data-ttu-id="4bab9-318">下面是一个关系图：</span><span class="sxs-lookup"><span data-stu-id="4bab9-318">Here's a diagram:</span></span>

![ASP.NET 如何动态生成 HTML 的概念流](getting-started/_static/image21.png)

<span data-ttu-id="4bab9-320">思路很简单，但代码可以执行很多有趣的任务，并且可以通过许多有趣的方式将 HTML 内容动态添加到页面中。</span><span class="sxs-lookup"><span data-stu-id="4bab9-320">The idea is simple, but there are many interesting tasks that the code can perform, and there are many interesting ways in which you can dynamically add HTML content to the page.</span></span> <span data-ttu-id="4bab9-321">和 ASP.NET 页面（如任何*HTML 页面）* 也可以包含在浏览器中运行的代码（JavaScript 和 jQuery 代码）。</span><span class="sxs-lookup"><span data-stu-id="4bab9-321">And ASP.NET *.cshtml* pages, like any HTML page, can also include code that runs in the browser itself (JavaScript and jQuery code).</span></span> <span data-ttu-id="4bab9-322">你将在本教程集中以及后续项目中浏览所有这些功能。</span><span class="sxs-lookup"><span data-stu-id="4bab9-322">You'll explore all of these things in this tutorial set and in subsequent ones.</span></span>

## <a name="coming-up-next"></a><span data-ttu-id="4bab9-323">下一步</span><span class="sxs-lookup"><span data-stu-id="4bab9-323">Coming Up Next</span></span>

<span data-ttu-id="4bab9-324">在本系列的下一个教程中，您将探讨 ASP.NET 网页编程。</span><span class="sxs-lookup"><span data-stu-id="4bab9-324">In the next tutorial in this series, you explore ASP.NET Web Pages programming a little more.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4bab9-325">其他资源</span><span class="sxs-lookup"><span data-stu-id="4bab9-325">Additional Resources</span></span>

<span data-ttu-id="4bab9-326">[从头开始创建 ASP.NET 网站](https://www.microsoft.com/web/post/create-an-aspnet-website-from-scratch)。</span><span class="sxs-lookup"><span data-stu-id="4bab9-326">[Create an ASP.NET website from scratch](https://www.microsoft.com/web/post/create-an-aspnet-website-from-scratch).</span></span> <span data-ttu-id="4bab9-327">本教程专门介绍如何使用 WebMatrix （不 ASP.NET 网页）。</span><span class="sxs-lookup"><span data-stu-id="4bab9-327">This is a tutorial that's specifically about using WebMatrix (not ASP.NET Web Pages).</span></span> <span data-ttu-id="4bab9-328">本文更详细地介绍了 WebMatrix 的一些其他功能，我们不会在本教程集中介绍。</span><span class="sxs-lookup"><span data-stu-id="4bab9-328">It goes into a little more detail about some of the additional features of WebMatrix that we won't cover in this tutorial set.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="4bab9-329">下一页</span><span class="sxs-lookup"><span data-stu-id="4bab9-329">Next</span></span>](intro-to-web-pages-programming.md)

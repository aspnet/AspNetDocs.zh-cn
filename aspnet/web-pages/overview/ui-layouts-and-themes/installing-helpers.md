---
uid: web-pages/overview/ui-layouts-and-themes/installing-helpers
title: 安装帮助程序在 ASP.NET Web Pages (Razor) 站点 |Microsoft Docs
author: Rick-Anderson
description: 本文介绍如何在 ASP.NET Web Pages (Razor) 的网站中安装一个帮助程序。 帮助器是包含代码和每个标记的可重用组件...
ms.author: riande
ms.date: 02/18/2014
ms.assetid: 5e968ead-906a-45ea-ac2a-c70e57e1a9b1
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/installing-helpers
msc.type: authoredcontent
ms.openlocfilehash: 3ffb2f88fd8d2ad32fb8ea7d476ca10fdd9ac430
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2019
ms.locfileid: "59398327"
---
# <a name="installing-a-helper-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="3fc33-104">在 ASP.NET Web Pages (Razor) 站点中安装一个帮助程序</span><span class="sxs-lookup"><span data-stu-id="3fc33-104">Installing a Helper in an ASP.NET Web Pages (Razor) Site</span></span>

<span data-ttu-id="3fc33-105">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="3fc33-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="3fc33-106">本文介绍如何在 ASP.NET Web Pages (Razor) 的网站中安装一个帮助程序。</span><span class="sxs-lookup"><span data-stu-id="3fc33-106">This article describes how to install a helper in an ASP.NET Web Pages (Razor) website.</span></span> <span data-ttu-id="3fc33-107">一个*帮助器*是一个可重用的组件，包括代码和标记来执行可能繁琐或复杂的任务。</span><span class="sxs-lookup"><span data-stu-id="3fc33-107">A *helper* is a reusable component that includes code and markup to perform a task that might be tedious or complex.</span></span>
> 
> <span data-ttu-id="3fc33-108">你将学习：</span><span class="sxs-lookup"><span data-stu-id="3fc33-108">What you'll learn:</span></span>
> 
> - <span data-ttu-id="3fc33-109">如何使用 WebMatrix 3 创建的网站中安装一个帮助程序。</span><span class="sxs-lookup"><span data-stu-id="3fc33-109">How to install a helper in a website created using WebMatrix 3.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="3fc33-110">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="3fc33-110">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="3fc33-111">WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="3fc33-111">WebMatrix 3</span></span>


## <a name="overview-of-helpers"></a><span data-ttu-id="3fc33-112">帮助程序的概述</span><span class="sxs-lookup"><span data-stu-id="3fc33-112">Overview of Helpers</span></span>

<span data-ttu-id="3fc33-113">人们通常希望为在网页上某些任务需要大量的代码，或需要额外知识。</span><span class="sxs-lookup"><span data-stu-id="3fc33-113">Some tasks that people often want to do on web pages require a lot of code or require extra knowledge.</span></span> <span data-ttu-id="3fc33-114">示例包括显示的图的数据;在页上; 中放置一个 Twitter"关注"按钮从你的网站; 发送电子邮件裁剪或调整图像; 的大小为您的网站使用 PayPal。</span><span class="sxs-lookup"><span data-stu-id="3fc33-114">Examples include displaying a chart for data; putting a Twitter "Follow" button on a page; sending email from your website; cropping or resizing images; using PayPal for your site.</span></span> <span data-ttu-id="3fc33-115">若要能够轻松执行此类目的，ASP.NET Web Pages 使您可以使用*帮助程序*。</span><span class="sxs-lookup"><span data-stu-id="3fc33-115">To make it easy to do these kinds of things, ASP.NET Web Pages lets you use *helpers*.</span></span> <span data-ttu-id="3fc33-116">帮助器是组件，安装适用于站点和，可让你使用只需一两行或 Razor 代码的两个执行的典型任务。</span><span class="sxs-lookup"><span data-stu-id="3fc33-116">Helpers are components that you install for a site and that let you perform typical tasks by using just a line or two of Razor code.</span></span>

<span data-ttu-id="3fc33-117">ASP.NET Web Pages 具有内置的几个帮助程序。</span><span class="sxs-lookup"><span data-stu-id="3fc33-117">ASP.NET Web Pages has a few helpers built in.</span></span> <span data-ttu-id="3fc33-118">但是，使用 NuGet 包管理器提供的包 （加载项） 中提供了许多帮助程序。</span><span class="sxs-lookup"><span data-stu-id="3fc33-118">However, many helpers are available in packages (add-ins) that are provided using the NuGet package manager.</span></span> <span data-ttu-id="3fc33-119">NuGet，可以选择要安装的程序包，然后它就会完成安装的所有详细信息。</span><span class="sxs-lookup"><span data-stu-id="3fc33-119">NuGet lets you select a package to install and then it takes care of all the details of the installation.</span></span>

## <a name="installing-a-helper-in-webmatrix-3"></a><span data-ttu-id="3fc33-120">在 WebMatrix 3 中安装帮助程序</span><span class="sxs-lookup"><span data-stu-id="3fc33-120">Installing a Helper in WebMatrix 3</span></span>

1. <span data-ttu-id="3fc33-121">在 WebMatrix 3 中，单击**NuGet**按钮。</span><span class="sxs-lookup"><span data-stu-id="3fc33-121">In WebMatrix 3, click the **NuGet** button.</span></span>

    ![在 WebMatrix 中的 NuGet 库对话框](installing-helpers/_static/image1.png)
2. <span data-ttu-id="3fc33-123">这会启动 NuGet 包管理器，并显示可用的包。</span><span class="sxs-lookup"><span data-stu-id="3fc33-123">This launches the NuGet package manager and displays available packages.</span></span> <span data-ttu-id="3fc33-124">在搜索框中，输入你想要安装的帮助器关键字。</span><span class="sxs-lookup"><span data-stu-id="3fc33-124">In the search box, enter a keyword for the helper you want to install.</span></span>

    ![在 WebMatrix 中的 NuGet 库对话框](installing-helpers/_static/image2.png)
3. <span data-ttu-id="3fc33-126">选择包，然后单击**安装**。</span><span class="sxs-lookup"><span data-stu-id="3fc33-126">Select the package and then click **Install**.</span></span> <span data-ttu-id="3fc33-127">单击**是**当系统询问你是否想要安装包，并指示接受条款。</span><span class="sxs-lookup"><span data-stu-id="3fc33-127">Click **Yes** when asked if you want to install the package and indicate that you accept the terms.</span></span>

     <span data-ttu-id="3fc33-128">如果这是首次安装一个帮助程序，NuGet 在您的网站用于组成帮助程序的代码中创建文件夹。</span><span class="sxs-lookup"><span data-stu-id="3fc33-128">If this is the first time you've installed a helper, NuGet creates folders in your website for the code that makes up the helper.</span></span>
4. <span data-ttu-id="3fc33-129">若要卸载程序的帮助程序，请单击**库**按钮，再单击**已安装**选项卡，然后选择你想要卸载的程序包。</span><span class="sxs-lookup"><span data-stu-id="3fc33-129">To uninstall a helper, click the **Gallery** button, click the **Installed** tab, and pick the package you want to uninstall.</span></span>

## <a name="installing-the-twitter-helper"></a><span data-ttu-id="3fc33-130">安装 Twitter 帮助程序</span><span class="sxs-lookup"><span data-stu-id="3fc33-130">Installing the Twitter helper</span></span>

<span data-ttu-id="3fc33-131">Twitter API 的最新版本不兼容与 Twitter 帮助程序通过 NuGet 安装。</span><span class="sxs-lookup"><span data-stu-id="3fc33-131">The latest version of the Twitter API is not compatible with the Twitter helper you install through NuGet.</span></span> <span data-ttu-id="3fc33-132">相反，请参阅[Twitter 帮助程序使用 WebMatrix](twitter-helper.md)主题，了解有关如何设置你的项目中的 Twitter 帮助程序的信息。</span><span class="sxs-lookup"><span data-stu-id="3fc33-132">Instead, see the [Twitter Helper with WebMatrix](twitter-helper.md) topic for information about how to set up the Twitter helper in your project.</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="3fc33-133">其他资源</span><span class="sxs-lookup"><span data-stu-id="3fc33-133">Additional Resources</span></span>


[<span data-ttu-id="3fc33-134">Introducing ASP.NET Web Pages 2-编程基础知识</span><span class="sxs-lookup"><span data-stu-id="3fc33-134">Introducing ASP.NET Web Pages 2 - Programming Basics</span></span>](../getting-started/introducing-razor-syntax-c.md)

[<span data-ttu-id="3fc33-135">Twitter WebMatrix 帮助的器</span><span class="sxs-lookup"><span data-stu-id="3fc33-135">Twitter Helper with WebMatrix</span></span>](twitter-helper.md)

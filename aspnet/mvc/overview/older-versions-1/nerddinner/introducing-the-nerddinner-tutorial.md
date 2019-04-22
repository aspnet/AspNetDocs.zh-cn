---
uid: mvc/overview/older-versions-1/nerddinner/introducing-the-nerddinner-tutorial
title: NerdDinner 的简介教程 |Microsoft Docs
author: shanselman
description: 若要了解新框架的最佳方式是生成内容进行处理。 本教程将指导完成如何构建很小，但完成后，应用程序使用 ASP.NE...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 397522d5-0402-4b94-b810-a2fb564f869d
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/introducing-the-nerddinner-tutorial
msc.type: authoredcontent
ms.openlocfilehash: ebd49295ea165ba4ef1a25398cff7dddcfa54f11
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2019
ms.locfileid: "59392191"
---
# <a name="introducing-the-nerddinner-tutorial"></a><span data-ttu-id="c10ee-104">NerdDinner 教程简介</span><span class="sxs-lookup"><span data-stu-id="c10ee-104">Introducing the NerdDinner Tutorial</span></span>

<span data-ttu-id="c10ee-105">通过[Scott Hanselman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="c10ee-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

[<span data-ttu-id="c10ee-106">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="c10ee-106">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="c10ee-107">若要了解新框架的最佳方式是生成内容进行处理。</span><span class="sxs-lookup"><span data-stu-id="c10ee-107">The best way to learn a new framework is to build something with it.</span></span> <span data-ttu-id="c10ee-108">本教程将指导完成如何生成一个较小，但完成，使用 ASP.NET MVC 1 中，应用程序，并介绍了一些重要概念。</span><span class="sxs-lookup"><span data-stu-id="c10ee-108">This tutorial walks through how to build a small, but complete, application using ASP.NET MVC 1, and introduces some of the core concepts behind it.</span></span>
> 
> <span data-ttu-id="c10ee-109">如果使用的 ASP.NET MVC 3，我们建议你遵循[获取启动使用 MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC Music 商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程。</span><span class="sxs-lookup"><span data-stu-id="c10ee-109">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>


## <a name="nerddinner-tutorial"></a><span data-ttu-id="c10ee-110">NerdDinner 教程</span><span class="sxs-lookup"><span data-stu-id="c10ee-110">NerdDinner Tutorial</span></span>

<span data-ttu-id="c10ee-111">若要了解新框架的最佳方式是生成内容进行处理。</span><span class="sxs-lookup"><span data-stu-id="c10ee-111">The best way to learn a new framework is to build something with it.</span></span> <span data-ttu-id="c10ee-112">本教程将指导完成如何生成一个较小，但完成，使用 ASP.NET MVC 应用程序，并介绍了一些重要概念。</span><span class="sxs-lookup"><span data-stu-id="c10ee-112">This tutorial walks through how to build a small, but complete, application using ASP.NET MVC, and introduces some of the core concepts behind it.</span></span>

<span data-ttu-id="c10ee-113">我们要生成应用程序被称为"NerdDinner"。</span><span class="sxs-lookup"><span data-stu-id="c10ee-113">The application we are going to build is called "NerdDinner".</span></span> <span data-ttu-id="c10ee-114">NerdDinner 提供方便人们查找和整理 dinners 联机：</span><span class="sxs-lookup"><span data-stu-id="c10ee-114">NerdDinner provides an easy way for people to find and organize dinners online:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image1.png)

<span data-ttu-id="c10ee-115">NerdDinner，已注册的用户可以创建、 编辑和删除 dinners。</span><span class="sxs-lookup"><span data-stu-id="c10ee-115">NerdDinner enables registered users to create, edit and delete dinners.</span></span> <span data-ttu-id="c10ee-116">它在应用程序强制实施一组一致的验证和业务规则：</span><span class="sxs-lookup"><span data-stu-id="c10ee-116">It enforces a consistent set of validation and business rules across the application:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image2.png)

<span data-ttu-id="c10ee-117">访问者可以使用基于 AJAX 的映射来搜索即将推出 dinners 接近的人们正在挂起：</span><span class="sxs-lookup"><span data-stu-id="c10ee-117">Visitors can use an AJAX-based map to search for upcoming dinners being held near them:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image3.png)

<span data-ttu-id="c10ee-118">单击 dinner 会将他们到详细信息页，以了解有关它的详细信息：</span><span class="sxs-lookup"><span data-stu-id="c10ee-118">Clicking a dinner will take them to a details page where they can learn more about it:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image4.png)

<span data-ttu-id="c10ee-119">如果他们感兴趣参加 dinner 他们可以登录，或在网站注册：</span><span class="sxs-lookup"><span data-stu-id="c10ee-119">If they are interested in attending the dinner they can login or register on the site:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image5.png)

<span data-ttu-id="c10ee-120">然后，他们可以单击来参与活动的基于 AJAX 的 RSVP 链接：</span><span class="sxs-lookup"><span data-stu-id="c10ee-120">They can then click an AJAX-based RSVP link to attend the event:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image6.png)

![](introducing-the-nerddinner-tutorial/_static/image7.png)

### <a name="implementing-nerddinner"></a><span data-ttu-id="c10ee-121">实现 NerdDinner</span><span class="sxs-lookup"><span data-stu-id="c10ee-121">Implementing NerdDinner</span></span>

<span data-ttu-id="c10ee-122">我们将首先我们 NerdDinner 的应用程序使用的文件-&gt;Visual Studio 中的新项目命令以创建一个全新的 ASP.NET MVC 项目。</span><span class="sxs-lookup"><span data-stu-id="c10ee-122">We are going to begin our NerdDinner application by using the File-&gt;New Project command within Visual Studio to create a brand new ASP.NET MVC project.</span></span> <span data-ttu-id="c10ee-123">然后以增量方式将功能和特性。</span><span class="sxs-lookup"><span data-stu-id="c10ee-123">We will then incrementally add functionality and features.</span></span> <span data-ttu-id="c10ee-124">在此过程中，我们将介绍：</span><span class="sxs-lookup"><span data-stu-id="c10ee-124">Along the way we'll cover:</span></span>

1. [<span data-ttu-id="c10ee-125">如何创建新的 ASP.NET MVC 项目</span><span class="sxs-lookup"><span data-stu-id="c10ee-125">How to create a new ASP.NET MVC Project</span></span>](create-a-new-aspnet-mvc-project.md)
2. [<span data-ttu-id="c10ee-126">如何创建数据库</span><span class="sxs-lookup"><span data-stu-id="c10ee-126">How to create a database</span></span>](create-a-database.md)
3. [<span data-ttu-id="c10ee-127">如何生成具有业务规则验证功能的模型</span><span class="sxs-lookup"><span data-stu-id="c10ee-127">How to build a model with business rule validations</span></span>](build-a-model-with-business-rule-validations.md)
4. [<span data-ttu-id="c10ee-128">如何使用控制器和视图实现列表/详细信息 UI</span><span class="sxs-lookup"><span data-stu-id="c10ee-128">How to use controllers and views to implement a listing/details UI</span></span>](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
5. [<span data-ttu-id="c10ee-129">如何提供 CRUD （创建、 读取、 更新、 删除） 数据窗体输入支持</span><span class="sxs-lookup"><span data-stu-id="c10ee-129">How to provide CRUD (create, read, update, delete) data form entry support</span></span>](provide-crud-create-read-update-delete-data-form-entry-support.md)
6. [<span data-ttu-id="c10ee-130">如何使用 ViewData 和实现 ViewModel 类</span><span class="sxs-lookup"><span data-stu-id="c10ee-130">How to use ViewData and implement ViewModel classes</span></span>](use-viewdata-and-implement-viewmodel-classes.md)
7. [<span data-ttu-id="c10ee-131">如何重新使用 UI 使用母版页和部分</span><span class="sxs-lookup"><span data-stu-id="c10ee-131">How to re-use UI using master pages and partials</span></span>](re-use-ui-using-master-pages-and-partials.md)
8. [<span data-ttu-id="c10ee-132">如何实现高效数据分页</span><span class="sxs-lookup"><span data-stu-id="c10ee-132">How to implement efficient data paging</span></span>](implement-efficient-data-paging.md)
9. [<span data-ttu-id="c10ee-133">如何使用身份验证和授权保护应用程序</span><span class="sxs-lookup"><span data-stu-id="c10ee-133">How to secure applications using authentication and authorization</span></span>](secure-applications-using-authentication-and-authorization.md)
10. [<span data-ttu-id="c10ee-134">如何使用 AJAX 提供动态更新</span><span class="sxs-lookup"><span data-stu-id="c10ee-134">How to use AJAX to deliver dynamic updates</span></span>](use-ajax-to-deliver-dynamic-updates.md)
11. [<span data-ttu-id="c10ee-135">如何使用 AJAX 实现映射方案</span><span class="sxs-lookup"><span data-stu-id="c10ee-135">How to use AJAX to implement mapping scenarios</span></span>](use-ajax-to-implement-mapping-scenarios.md)
12. [<span data-ttu-id="c10ee-136">如何启用自动化的单元测试</span><span class="sxs-lookup"><span data-stu-id="c10ee-136">How to enable automated unit testing</span></span>](enable-automated-unit-testing.md)

<span data-ttu-id="c10ee-137">您可以构建您自己的 NerdDinner 副本从零开始通过完成每个步骤我们的这一章中的演练。</span><span class="sxs-lookup"><span data-stu-id="c10ee-137">You can build your own copy of NerdDinner from scratch by completing each step we walkthrough in this chapter.</span></span> <span data-ttu-id="c10ee-138">或者，可以下载下面的源代码的完整的版本：[GitHub 上的 NerdDinner](https://github.com/AspNetMVPSamples/NerdDinner)。</span><span class="sxs-lookup"><span data-stu-id="c10ee-138">Alternatively, you can download a completed version of the source code here: [NerdDinner on GitHub](https://github.com/AspNetMVPSamples/NerdDinner).</span></span> <span data-ttu-id="c10ee-139">也可以选择性地[下载本教程的免费 PDF 版本](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)如果你想要阅读教程脱机。</span><span class="sxs-lookup"><span data-stu-id="c10ee-139">You can also optionally also [download a free PDF version of this tutorial](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf) if you want to read the tutorial offline.</span></span>

<span data-ttu-id="c10ee-140">可以使用 Visual Studio 2008 或免费 Visual Web Developer 2008 速成版构建应用程序。</span><span class="sxs-lookup"><span data-stu-id="c10ee-140">You can use either Visual Studio 2008 or the free Visual Web Developer 2008 Express to build the application.</span></span> <span data-ttu-id="c10ee-141">您可以使用 SQL Server 或免费 SQL Server Express 数据库。</span><span class="sxs-lookup"><span data-stu-id="c10ee-141">You can use either SQL Server or the free SQL Server Express for the database.</span></span>

<span data-ttu-id="c10ee-142">你可以安装 ASP.NET MVC，Visual Web Developer 2008 速成版，和 SQL Server Express （所有免费） 使用 V2 的[Microsoft Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)</span><span class="sxs-lookup"><span data-stu-id="c10ee-142">You can install ASP.NET MVC, Visual Web Developer 2008 Express, and SQL Server Express (all free) using V2 of the [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)</span></span>

### <a name="now-lets-get-started"></a><span data-ttu-id="c10ee-143">现在让我们开始吧...</span><span class="sxs-lookup"><span data-stu-id="c10ee-143">Now let's get started....</span></span>

<span data-ttu-id="c10ee-144">现在，我们已经介绍了 NerdDinner 的是，让我们卷起袖子，编写一些代码。</span><span class="sxs-lookup"><span data-stu-id="c10ee-144">Now that we've covered what NerdDinner is, let's roll up our sleeves and write some code.</span></span>

<span data-ttu-id="c10ee-145">我们将首先使用文件-&gt;Visual Studio 创建 NerdDinner 应用程序中的新项目。</span><span class="sxs-lookup"><span data-stu-id="c10ee-145">We'll begin by using File-&gt;New Project within Visual Studio to create the NerdDinner application.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="c10ee-146">下一页</span><span class="sxs-lookup"><span data-stu-id="c10ee-146">Next</span></span>](create-a-new-aspnet-mvc-project.md)

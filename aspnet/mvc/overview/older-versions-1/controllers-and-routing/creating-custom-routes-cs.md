---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-cs
title: 创建自定义路由 （C#） |微软文档
author: rick-anderson
description: 了解如何向ASP.NET MVC 应用程序添加自定义路由。 在本教程中，您将了解如何修改 Global.asax 文件中的默认路由表。
ms.author: riande
ms.date: 02/16/2009
ms.assetid: 3cd08f02-8763-490a-b625-2ac96a24b73f
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-cs
msc.type: authoredcontent
ms.openlocfilehash: b66ccc5e0cd4f6d7e5884394c2b7555b76382d3d
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542750"
---
# <a name="creating-custom-routes-c"></a><span data-ttu-id="3406e-104">创建自定义路由 (C#)</span><span class="sxs-lookup"><span data-stu-id="3406e-104">Creating Custom Routes (C#)</span></span>

<span data-ttu-id="3406e-105">由[微软](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="3406e-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="3406e-106">了解如何向ASP.NET MVC 应用程序添加自定义路由。</span><span class="sxs-lookup"><span data-stu-id="3406e-106">Learn how to add custom routes to an ASP.NET MVC application.</span></span> <span data-ttu-id="3406e-107">在本教程中，您将了解如何修改 Global.asax 文件中的默认路由表。</span><span class="sxs-lookup"><span data-stu-id="3406e-107">In this tutorial, you learn how to modify the default route table in the Global.asax file.</span></span>

<span data-ttu-id="3406e-108">在本教程中，您将了解如何向ASP.NET MVC 应用程序添加自定义路由。</span><span class="sxs-lookup"><span data-stu-id="3406e-108">In this tutorial, you learn how to add a custom route to an ASP.NET MVC application.</span></span> <span data-ttu-id="3406e-109">您将了解如何使用自定义路由修改 Global.asax 文件中的默认路由表。</span><span class="sxs-lookup"><span data-stu-id="3406e-109">You learn how to modify the default route table in the Global.asax file with a custom route.</span></span>

<span data-ttu-id="3406e-110">对于许多简单的ASP.NET MVC 应用程序，默认路由表将工作正常。</span><span class="sxs-lookup"><span data-stu-id="3406e-110">For many simple ASP.NET MVC applications, the default route table will work just fine.</span></span> <span data-ttu-id="3406e-111">但是，您可能会发现您有专门的路由需求。</span><span class="sxs-lookup"><span data-stu-id="3406e-111">However, you might discover that you have specialized routing needs.</span></span> <span data-ttu-id="3406e-112">在这种情况下，您可以创建自定义路由。</span><span class="sxs-lookup"><span data-stu-id="3406e-112">In that case, you can create a custom route.</span></span>

<span data-ttu-id="3406e-113">例如，假设您正在构建一个博客应用程序。</span><span class="sxs-lookup"><span data-stu-id="3406e-113">Imagine, for example, that you are building a blog application.</span></span> <span data-ttu-id="3406e-114">您可能需要处理如下所示的传入请求：</span><span class="sxs-lookup"><span data-stu-id="3406e-114">You might want to handle incoming requests that look like this:</span></span>

<span data-ttu-id="3406e-115">/存档/12-25-2009</span><span class="sxs-lookup"><span data-stu-id="3406e-115">/Archive/12-25-2009</span></span>

<span data-ttu-id="3406e-116">当用户输入此请求时，您希望返回与日期 12/25/2009 对应的博客条目。</span><span class="sxs-lookup"><span data-stu-id="3406e-116">When a user enters this request, you want to return the blog entry that corresponds to the date 12/25/2009.</span></span> <span data-ttu-id="3406e-117">为了处理这种类型的请求，您需要创建自定义路由。</span><span class="sxs-lookup"><span data-stu-id="3406e-117">In order to handle this type of request, you need to create a custom route.</span></span>

<span data-ttu-id="3406e-118">清单1中的 Global.asax 文件包含一个名为 Blog 的新自定义路由，它处理看起来像 /存档/*条目日期*的请求。</span><span class="sxs-lookup"><span data-stu-id="3406e-118">The Global.asax file in Listing 1 contains a new custom route, named Blog, which handles requests that look like /Archive/*entry date*.</span></span>

<span data-ttu-id="3406e-119">**清单 1 - 全局.asax（带自定义路由）**</span><span class="sxs-lookup"><span data-stu-id="3406e-119">**Listing 1 - Global.asax (with custom route)**</span></span>

[!code-csharp[Main](creating-custom-routes-cs/samples/sample1.cs)]

<span data-ttu-id="3406e-120">添加到工艺路线表的路由的顺序很重要。</span><span class="sxs-lookup"><span data-stu-id="3406e-120">The order of the routes that you add to the route table is important.</span></span> <span data-ttu-id="3406e-121">我们新的自定义博客路由在现有默认路由之前添加。</span><span class="sxs-lookup"><span data-stu-id="3406e-121">Our new custom Blog route is added before the existing Default route.</span></span> <span data-ttu-id="3406e-122">如果颠倒了订单，则默认路由将始终被调用，而不是自定义路由。</span><span class="sxs-lookup"><span data-stu-id="3406e-122">If you reversed the order, then the Default route always will get called instead of the custom route.</span></span>

<span data-ttu-id="3406e-123">自定义博客路由匹配以 /存档/开头的任何请求。</span><span class="sxs-lookup"><span data-stu-id="3406e-123">The custom Blog route matches any request that starts with /Archive/.</span></span> <span data-ttu-id="3406e-124">因此，它与以下 URL 匹配：</span><span class="sxs-lookup"><span data-stu-id="3406e-124">So, it matches all of the following URLs:</span></span>

- <span data-ttu-id="3406e-125">/存档/12-25-2009</span><span class="sxs-lookup"><span data-stu-id="3406e-125">/Archive/12-25-2009</span></span>

- <span data-ttu-id="3406e-126">/存档/10-6-2004</span><span class="sxs-lookup"><span data-stu-id="3406e-126">/Archive/10-6-2004</span></span>

- <span data-ttu-id="3406e-127">/存档/苹果</span><span class="sxs-lookup"><span data-stu-id="3406e-127">/Archive/apple</span></span>

<span data-ttu-id="3406e-128">自定义路由将传入请求映射到名为"存档"的控制器，并调用 Entry（） 操作。</span><span class="sxs-lookup"><span data-stu-id="3406e-128">The custom route maps the incoming request to a controller named Archive and invokes the Entry() action.</span></span> <span data-ttu-id="3406e-129">调用 entry（） 方法时，条目日期将作为名为 entryDate 的参数传递。</span><span class="sxs-lookup"><span data-stu-id="3406e-129">When the Entry() method is called, the entry date is passed as a parameter named entryDate.</span></span>

<span data-ttu-id="3406e-130">您可以将博客自定义路由与清单 2 中的控制器一起使用。</span><span class="sxs-lookup"><span data-stu-id="3406e-130">You can use the Blog custom route with the controller in Listing 2.</span></span>

<span data-ttu-id="3406e-131">**清单2 - ArchiveController.cs**</span><span class="sxs-lookup"><span data-stu-id="3406e-131">**Listing 2 - ArchiveController.cs**</span></span>

[!code-csharp[Main](creating-custom-routes-cs/samples/sample2.cs)]

<span data-ttu-id="3406e-132">请注意，清单 2 中的 entry（） 方法接受 DateTime 类型的参数。</span><span class="sxs-lookup"><span data-stu-id="3406e-132">Notice that the Entry() method in Listing 2 accepts a parameter of type DateTime.</span></span> <span data-ttu-id="3406e-133">MVC 框架足够智能，可以自动将 URL 的输入日期转换为 DateTime 值。</span><span class="sxs-lookup"><span data-stu-id="3406e-133">The MVC framework is smart enough to convert the entry date from the URL into a DateTime value automatically.</span></span> <span data-ttu-id="3406e-134">如果 URL 中的输入日期参数无法转换为 DateTime，则引发错误（参见图 1）。</span><span class="sxs-lookup"><span data-stu-id="3406e-134">If the entry date parameter from the URL cannot be converted to a DateTime, an error is raised (see Figure 1).</span></span>

<span data-ttu-id="3406e-135">**图 1 - 转换参数时出错**</span><span class="sxs-lookup"><span data-stu-id="3406e-135">**Figure 1 - Error from converting parameter**</span></span>

<span data-ttu-id="3406e-136">[![“新建项目”对话框](creating-custom-routes-cs/_static/image1.jpg)](creating-custom-routes-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="3406e-136">[![The New Project dialog box](creating-custom-routes-cs/_static/image1.jpg)](creating-custom-routes-cs/_static/image1.png)</span></span>

<span data-ttu-id="3406e-137">**图 01**： 转换参数时出错 （[单击以查看全尺寸图像](creating-custom-routes-cs/_static/image2.png)）</span><span class="sxs-lookup"><span data-stu-id="3406e-137">**Figure 01**: Error from converting parameter ([Click to view full-size image](creating-custom-routes-cs/_static/image2.png))</span></span>

## <a name="summary"></a><span data-ttu-id="3406e-138">总结</span><span class="sxs-lookup"><span data-stu-id="3406e-138">Summary</span></span>

<span data-ttu-id="3406e-139">本教程的目的是演示如何创建自定义路由。</span><span class="sxs-lookup"><span data-stu-id="3406e-139">The goal of this tutorial was to demonstrate how you can create a custom route.</span></span> <span data-ttu-id="3406e-140">您学习了如何在表示博客条目的 Global.asax 文件中向路由表添加自定义路由。</span><span class="sxs-lookup"><span data-stu-id="3406e-140">You learned how to add a custom route to the route table in the Global.asax file that represents blog entries.</span></span> <span data-ttu-id="3406e-141">我们讨论了如何将博客条目的请求映射到名为 ArchiveController 的控制器和名为 entry（） 的控制器操作。</span><span class="sxs-lookup"><span data-stu-id="3406e-141">We discussed how to map requests for blog entries to a controller named ArchiveController and a controller action named Entry().</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="3406e-142">[上一页](aspnet-mvc-controllers-overview-cs.md)
> [下一页](creating-a-route-constraint-cs.md)</span><span class="sxs-lookup"><span data-stu-id="3406e-142">[Previous](aspnet-mvc-controllers-overview-cs.md)
[Next](creating-a-route-constraint-cs.md)</span></span>

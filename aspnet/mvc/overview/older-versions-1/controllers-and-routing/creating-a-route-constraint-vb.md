---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-a-route-constraint-vb
title: 创建路由约束 (VB) |Microsoft Docs
author: StephenWalther
description: 在本教程中，Stephen Walther 演示了如何控制如何浏览器请求的匹配路由通过使用正则表达式中创建路由约束。
ms.author: riande
ms.date: 02/16/2009
ms.assetid: b7cce113-c82c-45bf-b97b-357e5d9f7f56
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-a-route-constraint-vb
msc.type: authoredcontent
ms.openlocfilehash: 205742dd8f866c8828008c8aac7ab3f98b173ceb
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/06/2019
ms.locfileid: "65123421"
---
# <a name="creating-a-route-constraint-vb"></a><span data-ttu-id="645ea-103">创建路由约束 (VB)</span><span class="sxs-lookup"><span data-stu-id="645ea-103">Creating a Route Constraint (VB)</span></span>

<span data-ttu-id="645ea-104">通过[Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="645ea-104">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="645ea-105">在本教程中，Stephen Walther 演示了如何控制如何浏览器请求的匹配路由通过使用正则表达式中创建路由约束。</span><span class="sxs-lookup"><span data-stu-id="645ea-105">In this tutorial, Stephen Walther demonstrates how you can control how browser requests match routes by creating route constraints with regular expressions.</span></span>

<span data-ttu-id="645ea-106">使用路由约束来限制相匹配的特定路由的浏览器请求。</span><span class="sxs-lookup"><span data-stu-id="645ea-106">You use route constraints to restrict the browser requests that match a particular route.</span></span> <span data-ttu-id="645ea-107">可以使用正则表达式来指定路由约束。</span><span class="sxs-lookup"><span data-stu-id="645ea-107">You can use a regular expression to specify a route constraint.</span></span>

<span data-ttu-id="645ea-108">例如，假设您具有路由中定义列表 1 中在 Global.asax 文件中。</span><span class="sxs-lookup"><span data-stu-id="645ea-108">For example, imagine that you have defined the route in Listing 1 in your Global.asax file.</span></span>

<span data-ttu-id="645ea-109">**Listing 1 - Global.asax.vb**</span><span class="sxs-lookup"><span data-stu-id="645ea-109">**Listing 1 - Global.asax.vb**</span></span>

[!code-vb[Main](creating-a-route-constraint-vb/samples/sample1.vb)]

<span data-ttu-id="645ea-110">代码清单 1 包含名为产品的路由。</span><span class="sxs-lookup"><span data-stu-id="645ea-110">Listing 1 contains a route named Product.</span></span> <span data-ttu-id="645ea-111">产品路由可用于将浏览器请求映射到包含在代码清单 2 ProductController。</span><span class="sxs-lookup"><span data-stu-id="645ea-111">You can use the Product route to map browser requests to the ProductController contained in Listing 2.</span></span>

<span data-ttu-id="645ea-112">**Listing 2 - Controllers\ProductController.vb**</span><span class="sxs-lookup"><span data-stu-id="645ea-112">**Listing 2 - Controllers\ProductController.vb**</span></span>

[!code-vb[Main](creating-a-route-constraint-vb/samples/sample2.vb)]

<span data-ttu-id="645ea-113">请注意，产品控制器公开的 Details() 操作接受一个名为产品 id 的单个参数。</span><span class="sxs-lookup"><span data-stu-id="645ea-113">Notice that the Details() action exposed by the Product controller accepts a single parameter named productId.</span></span> <span data-ttu-id="645ea-114">此参数是一个整数参数。</span><span class="sxs-lookup"><span data-stu-id="645ea-114">This parameter is an integer parameter.</span></span>

<span data-ttu-id="645ea-115">在列表 1 中定义的路由将与任何以下 Url:</span><span class="sxs-lookup"><span data-stu-id="645ea-115">The route defined in Listing 1 will match any of the following URLs:</span></span>

- <span data-ttu-id="645ea-116">/Product/23</span><span class="sxs-lookup"><span data-stu-id="645ea-116">/Product/23</span></span>
- <span data-ttu-id="645ea-117">/Product/7</span><span class="sxs-lookup"><span data-stu-id="645ea-117">/Product/7</span></span>

<span data-ttu-id="645ea-118">遗憾的是，路由也会匹配以下 Url:</span><span class="sxs-lookup"><span data-stu-id="645ea-118">Unfortunately, the route will also match the following URLs:</span></span>

- <span data-ttu-id="645ea-119">/ 产品/被废弃</span><span class="sxs-lookup"><span data-stu-id="645ea-119">/Product/blah</span></span>
- <span data-ttu-id="645ea-120">/Product/apple</span><span class="sxs-lookup"><span data-stu-id="645ea-120">/Product/apple</span></span>

<span data-ttu-id="645ea-121">因为 Details() 操作需要的一个整数参数，则发出请求，其中包含一个整数值以外的内容会导致错误。</span><span class="sxs-lookup"><span data-stu-id="645ea-121">Because the Details() action expects an integer parameter, making a request that contains something other than an integer value will cause an error.</span></span> <span data-ttu-id="645ea-122">例如，如果你的浏览器中键入 URL /Product/apple 然后将图 1 中显示错误页。</span><span class="sxs-lookup"><span data-stu-id="645ea-122">For example, if you type the URL /Product/apple into your browser then you will get the error page in Figure 1.</span></span>

<span data-ttu-id="645ea-123">[![新建项目对话框](creating-a-route-constraint-vb/_static/image1.jpg)](creating-a-route-constraint-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="645ea-123">[![The New Project dialog box](creating-a-route-constraint-vb/_static/image1.jpg)](creating-a-route-constraint-vb/_static/image1.png)</span></span>

<span data-ttu-id="645ea-124">**图 01**:看到 explode 页面 ([单击此项可查看原尺寸图像](creating-a-route-constraint-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="645ea-124">**Figure 01**: Seeing a page explode ([Click to view full-size image](creating-a-route-constraint-vb/_static/image2.png))</span></span>

<span data-ttu-id="645ea-125">您真正想要做什么是仅匹配包含正确的整数 productId 的 Url。</span><span class="sxs-lookup"><span data-stu-id="645ea-125">What you really want to do is only match URLs that contain a proper integer productId.</span></span> <span data-ttu-id="645ea-126">您可以使用约束定义路由时以限制与路由匹配的 Url。</span><span class="sxs-lookup"><span data-stu-id="645ea-126">You can use a constraint when defining a route to restrict the URLs that match the route.</span></span> <span data-ttu-id="645ea-127">列表 3 中的已修改的产品路由包含仅与整数相匹配的正则表达式约束。</span><span class="sxs-lookup"><span data-stu-id="645ea-127">The modified Product route in Listing 3 contains a regular expression constraint that only matches integers.</span></span>

<span data-ttu-id="645ea-128">**Listing 3 - Global.asax.vb**</span><span class="sxs-lookup"><span data-stu-id="645ea-128">**Listing 3 - Global.asax.vb**</span></span>

[!code-vb[Main](creating-a-route-constraint-vb/samples/sample3.vb)]

<span data-ttu-id="645ea-129">正则表达式 \d+ 匹配一个或多个整数。</span><span class="sxs-lookup"><span data-stu-id="645ea-129">The regular expression \d+ matches one or more integers.</span></span> <span data-ttu-id="645ea-130">此约束会导致产品路由，以匹配以下 Url:</span><span class="sxs-lookup"><span data-stu-id="645ea-130">This constraint causes the Product route to match the following URLs:</span></span>

- <span data-ttu-id="645ea-131">/Product/3</span><span class="sxs-lookup"><span data-stu-id="645ea-131">/Product/3</span></span>
- <span data-ttu-id="645ea-132">/Product/8999</span><span class="sxs-lookup"><span data-stu-id="645ea-132">/Product/8999</span></span>

<span data-ttu-id="645ea-133">但不是允许以下 Url:</span><span class="sxs-lookup"><span data-stu-id="645ea-133">But not the following URLs:</span></span>

- <span data-ttu-id="645ea-134">/Product/apple</span><span class="sxs-lookup"><span data-stu-id="645ea-134">/Product/apple</span></span>
- <span data-ttu-id="645ea-135">/Product</span><span class="sxs-lookup"><span data-stu-id="645ea-135">/Product</span></span>

<span data-ttu-id="645ea-136">这些浏览器请求将由另一个路由或如果没有匹配的路由*找不到资源*将返回错误。</span><span class="sxs-lookup"><span data-stu-id="645ea-136">These browser requests will be handled by another route or, if there are no matching routes, a *The resource could not be found* error will be returned.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="645ea-137">[上一页](creating-custom-routes-vb.md)
> [下一页](creating-a-custom-route-constraint-vb.md)</span><span class="sxs-lookup"><span data-stu-id="645ea-137">[Previous](creating-custom-routes-vb.md)
[Next](creating-a-custom-route-constraint-vb.md)</span></span>

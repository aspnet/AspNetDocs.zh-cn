---
uid: mvc/overview/older-versions-1/controllers-and-routing/adding-dynamic-content-to-a-cached-page-vb
title: 将动态内容添加到缓存页面 （VB） |微软文档
author: rick-anderson
description: 了解如何在同一页中混合动态和缓存的内容。 缓存后替换使您能够显示动态内容，如横幅播发。
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 68acd884-fb57-4486-a1be-aaa93e380780
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/adding-dynamic-content-to-a-cached-page-vb
msc.type: authoredcontent
ms.openlocfilehash: 1ed022fc560becbd21722b94f2428cf7b32f2635
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542256"
---
# <a name="adding-dynamic-content-to-a-cached-page-vb"></a><span data-ttu-id="0a709-104">向缓存页添加动态内容 (VB)</span><span class="sxs-lookup"><span data-stu-id="0a709-104">Adding Dynamic Content to a Cached Page (VB)</span></span>

<span data-ttu-id="0a709-105">由[微软](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="0a709-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="0a709-106">了解如何在同一页中混合动态和缓存的内容。</span><span class="sxs-lookup"><span data-stu-id="0a709-106">Learn how to mix dynamic and cached content in the same page.</span></span> <span data-ttu-id="0a709-107">缓存后替换使您能够在已缓存的页面中显示动态内容，如横幅播发或新闻项目。</span><span class="sxs-lookup"><span data-stu-id="0a709-107">Post-cache substitution enables you to display dynamic content, such as banner advertisements or news items, within a page that has been output cached.</span></span>

<span data-ttu-id="0a709-108">通过利用输出缓存，您可以显著提高ASP.NET MVC 应用程序的性能。</span><span class="sxs-lookup"><span data-stu-id="0a709-108">By taking advantage of output caching, you can dramatically improve the performance of an ASP.NET MVC application.</span></span> <span data-ttu-id="0a709-109">在每次请求页面时，该页可以生成一次，并缓存在多个用户的内存中，而不是每次请求页面时重新生成页面。</span><span class="sxs-lookup"><span data-stu-id="0a709-109">Instead of regenerating a page each and every time the page is requested, the page can be generated once and cached in memory for multiple users.</span></span>

<span data-ttu-id="0a709-110">但有一个问题。</span><span class="sxs-lookup"><span data-stu-id="0a709-110">But there is a problem.</span></span> <span data-ttu-id="0a709-111">如果您需要在页面中显示动态内容，该怎么办？</span><span class="sxs-lookup"><span data-stu-id="0a709-111">What if you need to display dynamic content in the page?</span></span> <span data-ttu-id="0a709-112">例如，假设您要在页面中显示横幅广告。</span><span class="sxs-lookup"><span data-stu-id="0a709-112">For example, imagine that you want to display a banner advertisement in the page.</span></span> <span data-ttu-id="0a709-113">您不希望缓存横幅播发，以便每个用户看到相同的播发。</span><span class="sxs-lookup"><span data-stu-id="0a709-113">You don't want the banner advertisement to be cached so that every user sees the very same advertisement.</span></span> <span data-ttu-id="0a709-114">你不会这样赚钱的！</span><span class="sxs-lookup"><span data-stu-id="0a709-114">You wouldn't make any money that way!</span></span>

<span data-ttu-id="0a709-115">幸运的是，有一个简单的解决方案。</span><span class="sxs-lookup"><span data-stu-id="0a709-115">Fortunately, there is an easy solution.</span></span> <span data-ttu-id="0a709-116">您可以利用称为*缓存后替换*ASP.NET框架的功能。</span><span class="sxs-lookup"><span data-stu-id="0a709-116">You can take advantage of a feature of the ASP.NET framework called *post-cache substitution*.</span></span> <span data-ttu-id="0a709-117">缓存后替换使您能够替换已缓存在内存中的页面中的动态内容。</span><span class="sxs-lookup"><span data-stu-id="0a709-117">Post-cache substitution enables you to substitute dynamic content in a page that has been cached in memory.</span></span>

<span data-ttu-id="0a709-118">通常，当您使用&lt;OutputCache&gt;属性输出缓存页面时，该页将缓存在服务器和客户端（Web 浏览器）上。</span><span class="sxs-lookup"><span data-stu-id="0a709-118">Normally, when you output cache a page by using the &lt;OutputCache&gt; attribute, the page is cached on both the server and the client (the web browser).</span></span> <span data-ttu-id="0a709-119">使用缓存后替换时，页面仅缓存在服务器上。</span><span class="sxs-lookup"><span data-stu-id="0a709-119">When you use post-cache substitution, a page is cached only on the server.</span></span>

#### <a name="using-post-cache-substitution"></a><span data-ttu-id="0a709-120">使用缓存后替换</span><span class="sxs-lookup"><span data-stu-id="0a709-120">Using Post-Cache Substitution</span></span>

<span data-ttu-id="0a709-121">使用缓存后替换需要两个步骤。</span><span class="sxs-lookup"><span data-stu-id="0a709-121">Using post-cache substitution requires two steps.</span></span> <span data-ttu-id="0a709-122">首先，您需要定义一个方法，该方法返回表示要在缓存页中显示的动态内容的字符串。</span><span class="sxs-lookup"><span data-stu-id="0a709-122">First, you need to define a method that returns a string that represents the dynamic content that you want to display in the cached page.</span></span> <span data-ttu-id="0a709-123">接下来，调用 HttpResponse.Write 替代（） 方法将动态内容注入页面。</span><span class="sxs-lookup"><span data-stu-id="0a709-123">Next, you call the HttpResponse.WriteSubstitution() method to inject the dynamic content into the page.</span></span>

<span data-ttu-id="0a709-124">例如，假设您要在缓存的页面中随机显示不同的新闻项目。</span><span class="sxs-lookup"><span data-stu-id="0a709-124">Imagine, for example, that you want to randomly display different news items in a cached page.</span></span> <span data-ttu-id="0a709-125">清单 1 中的类公开一个名为 RenderNews（）的方法，该方法从三个新闻项列表中随机返回一个新闻项。</span><span class="sxs-lookup"><span data-stu-id="0a709-125">The class in Listing 1 exposes a single method, named RenderNews(), that randomly returns one news item from a list of three news items.</span></span>

<span data-ttu-id="0a709-126">**清单1 = 模型\新闻.vb**</span><span class="sxs-lookup"><span data-stu-id="0a709-126">**Listing 1 – Models\News.vb**</span></span>

[!code-vb[Main](adding-dynamic-content-to-a-cached-page-vb/samples/sample1.vb)]

<span data-ttu-id="0a709-127">要利用缓存后替换，请致电 HttpResponse.Write 替代（）方法。</span><span class="sxs-lookup"><span data-stu-id="0a709-127">To take advantage of post-cache substitution, you call the HttpResponse.WriteSubstitution() method.</span></span> <span data-ttu-id="0a709-128">Write替代（）方法设置代码，以动态内容替换缓存页的区域。</span><span class="sxs-lookup"><span data-stu-id="0a709-128">The WriteSubstitution() method sets up the code to replace a region of the cached page with dynamic content.</span></span> <span data-ttu-id="0a709-129">Write替代（）方法用于在清单2的视图中显示随机新闻项。</span><span class="sxs-lookup"><span data-stu-id="0a709-129">The WriteSubstitution() method is used to display the random news item in the view in Listing 2.</span></span>

<span data-ttu-id="0a709-130">**清单 2 = 视图\home_Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="0a709-130">**Listing 2 – Views\Home\Index.aspx**</span></span>

[!code-aspx[Main](adding-dynamic-content-to-a-cached-page-vb/samples/sample2.aspx)]

<span data-ttu-id="0a709-131">渲染新闻方法传递给写入替换（） 方法。</span><span class="sxs-lookup"><span data-stu-id="0a709-131">The RenderNews method is passed to the WriteSubstitution() method.</span></span> <span data-ttu-id="0a709-132">请注意，不调用 RenderNews 方法。</span><span class="sxs-lookup"><span data-stu-id="0a709-132">Notice that the RenderNews method is not called.</span></span> <span data-ttu-id="0a709-133">相反，在 AddressOf 运算符的帮助下，对该方法的引用传递给 Write 替代（）。</span><span class="sxs-lookup"><span data-stu-id="0a709-133">Instead a reference to the method is passed to WriteSubstitution() with the help of the AddressOf operator.</span></span>

<span data-ttu-id="0a709-134">已缓存索引视图。</span><span class="sxs-lookup"><span data-stu-id="0a709-134">The Index view is cached.</span></span> <span data-ttu-id="0a709-135">视图由清单 3 中的控制器返回。</span><span class="sxs-lookup"><span data-stu-id="0a709-135">The view is returned by the controller in Listing 3.</span></span> <span data-ttu-id="0a709-136">请注意，Index（） 操作使用&lt;OutputCache&gt;属性进行修饰，该属性会导致索引视图缓存 60 秒。</span><span class="sxs-lookup"><span data-stu-id="0a709-136">Notice that the Index() action is decorated with an &lt;OutputCache&gt; attribute that causes the Index view to be cached for 60 seconds.</span></span>

<span data-ttu-id="0a709-137">**清单3 = 控制器\主控制器.vb**</span><span class="sxs-lookup"><span data-stu-id="0a709-137">**Listing 3 – Controllers\HomeController.vb**</span></span>

[!code-vb[Main](adding-dynamic-content-to-a-cached-page-vb/samples/sample3.vb)]

<span data-ttu-id="0a709-138">即使缓存了 Index 视图，当您请求"索引"页时，也会显示不同的随机新闻项。</span><span class="sxs-lookup"><span data-stu-id="0a709-138">Even though the Index view is cached, different random news items are displayed when you request the Index page.</span></span> <span data-ttu-id="0a709-139">请求"索引"页时，页面显示的时间在 60 秒内不会更改（参见图 1）。</span><span class="sxs-lookup"><span data-stu-id="0a709-139">When you request the Index page, the time displayed by the page does not change for 60 seconds (see Figure 1).</span></span> <span data-ttu-id="0a709-140">时间不变的事实证明页面被缓存了。</span><span class="sxs-lookup"><span data-stu-id="0a709-140">The fact that the time does not change proves that the page is cached.</span></span> <span data-ttu-id="0a709-141">但是，Write替代（）方法（随机新闻项）注入的内容随每个请求而变化。</span><span class="sxs-lookup"><span data-stu-id="0a709-141">However, the content injected by the WriteSubstitution() method – the random news item – changes with each request .</span></span>

<span data-ttu-id="0a709-142">**图 1 = 在缓存的页面中注入动态新闻项目**</span><span class="sxs-lookup"><span data-stu-id="0a709-142">**Figure 1 – Injecting dynamic news items in a cached page**</span></span>

![clip_image002](adding-dynamic-content-to-a-cached-page-vb/_static/image1.jpg)

#### <a name="using-post-cache-substitution-in-helper-methods"></a><span data-ttu-id="0a709-144">在帮助器方法中使用缓存后替换</span><span class="sxs-lookup"><span data-stu-id="0a709-144">Using Post-Cache Substitution in Helper Methods</span></span>

<span data-ttu-id="0a709-145">利用缓存后替换的一种更简单的方法是在自定义帮助器方法中封装对 Write 替代（） 方法的调用。</span><span class="sxs-lookup"><span data-stu-id="0a709-145">An easier way to take advantage of post-cache substitution is to encapsulate the call to the WriteSubstitution() method within a custom helper method.</span></span> <span data-ttu-id="0a709-146">清单4中的帮助方法说明了此方法。</span><span class="sxs-lookup"><span data-stu-id="0a709-146">This approach is illustrated by the helper method in Listing 4.</span></span>

<span data-ttu-id="0a709-147">**清单4 = 帮助者\AdHelper.vb**</span><span class="sxs-lookup"><span data-stu-id="0a709-147">**Listing 4 – Helpers\AdHelper.vb**</span></span>

[!code-vb[Main](adding-dynamic-content-to-a-cached-page-vb/samples/sample4.vb)]

<span data-ttu-id="0a709-148">清单4包含一个可视化基本模块，该模块公开了两种方法：渲染横幅（）和渲染横幅内部（）。</span><span class="sxs-lookup"><span data-stu-id="0a709-148">Listing 4 contains a Visual Basic module that exposes two methods: RenderBanner() and RenderBannerInternal().</span></span> <span data-ttu-id="0a709-149">RenderBanner（） 方法表示实际帮助器方法。</span><span class="sxs-lookup"><span data-stu-id="0a709-149">The RenderBanner() method represents the actual helper method.</span></span> <span data-ttu-id="0a709-150">此方法扩展了标准ASP.NET MVC HtmlHelper 类，以便您可以像任何其他帮助器方法一样在视图中调用 Html.RenderBanner（）。</span><span class="sxs-lookup"><span data-stu-id="0a709-150">This method extends the standard ASP.NET MVC HtmlHelper class so that you can call Html.RenderBanner() in a view just like any other helper method.</span></span>

<span data-ttu-id="0a709-151">renderBanner（） 方法调用将 RenderBanner 内部（） 方法传递给 Write 替换（） 方法的 HttpResponse.Write 替换（） 方法。</span><span class="sxs-lookup"><span data-stu-id="0a709-151">The RenderBanner() method calls the HttpResponse.WriteSubstitution() method passing the RenderBannerInternal() method to the WriteSubstitution() method.</span></span>

<span data-ttu-id="0a709-152">RenderBanner 内部（） 方法是一种私有方法。</span><span class="sxs-lookup"><span data-stu-id="0a709-152">The RenderBannerInternal() method is a private method.</span></span> <span data-ttu-id="0a709-153">此方法不会作为帮助器方法公开。</span><span class="sxs-lookup"><span data-stu-id="0a709-153">This method won't be exposed as a helper method.</span></span> <span data-ttu-id="0a709-154">RenderBanner 内部（） 方法从三个横幅广告图像列表中随机返回一个横幅广告图像。</span><span class="sxs-lookup"><span data-stu-id="0a709-154">The RenderBannerInternal() method randomly returns one banner advertisement image from a list of three banner advertisement images.</span></span>

<span data-ttu-id="0a709-155">清单5中修改后的索引视图说明了如何使用 RenderBanner（） 帮助器方法。</span><span class="sxs-lookup"><span data-stu-id="0a709-155">The modified Index view in Listing 5 illustrates how you can use the RenderBanner() helper method.</span></span> <span data-ttu-id="0a709-156">请注意，在视图&lt;顶部包含额外的&gt;%@ 导入 % 指令，用于导入 MvcApplication1.Helpers 命名空间。</span><span class="sxs-lookup"><span data-stu-id="0a709-156">Notice that an additional &lt;%@ Import %&gt; directive is included at the top of the view to import the MvcApplication1.Helpers namespace.</span></span> <span data-ttu-id="0a709-157">如果忽略导入此命名空间，则 RenderBanner（） 方法将不会显示为 Html 属性上的方法。</span><span class="sxs-lookup"><span data-stu-id="0a709-157">If you neglect to import this namespace, then the RenderBanner() method won't appear as a method on the Html property.</span></span>

<span data-ttu-id="0a709-158">**清单 5 = 视图\home_Index.aspx（使用 RenderBanner（） 方法）**</span><span class="sxs-lookup"><span data-stu-id="0a709-158">**Listing 5 – Views\Home\Index.aspx (with RenderBanner() method)**</span></span>

[!code-aspx[Main](adding-dynamic-content-to-a-cached-page-vb/samples/sample5.aspx)]

<span data-ttu-id="0a709-159">请求清单 5 中由视图呈现的页面时，每个请求都会显示不同的横幅播发（参见图 2）。</span><span class="sxs-lookup"><span data-stu-id="0a709-159">When you request the page rendered by the view in Listing 5, a different banner advertisement is displayed with each request (see Figure 2).</span></span> <span data-ttu-id="0a709-160">页面被缓存，但横幅播发由 RenderBanner（） 帮助器方法动态注入。</span><span class="sxs-lookup"><span data-stu-id="0a709-160">The page is cached, but the banner advertisement is injected dynamically by the RenderBanner() helper method.</span></span>

<span data-ttu-id="0a709-161">**图 2 = 显示随机横幅播发的索引视图**</span><span class="sxs-lookup"><span data-stu-id="0a709-161">**Figure 2 – The Index view displaying a random banner advertisement**</span></span>

![clip_image004](adding-dynamic-content-to-a-cached-page-vb/_static/image2.jpg)

#### <a name="summary"></a><span data-ttu-id="0a709-163">总结</span><span class="sxs-lookup"><span data-stu-id="0a709-163">Summary</span></span>

<span data-ttu-id="0a709-164">本教程介绍了如何动态更新缓存页中的内容。</span><span class="sxs-lookup"><span data-stu-id="0a709-164">This tutorial explained how you can dynamically update content in a cached page.</span></span> <span data-ttu-id="0a709-165">您学习了如何使用 HttpResponse.Write 替代（） 方法，以便将动态内容注入缓存页面。</span><span class="sxs-lookup"><span data-stu-id="0a709-165">You learned how to use the HttpResponse.WriteSubstitution() method to enable dynamic content to be injected in a cached page.</span></span> <span data-ttu-id="0a709-166">您还学习了如何在 HTML 帮助器方法中封装对 Write 替代（） 方法的调用。</span><span class="sxs-lookup"><span data-stu-id="0a709-166">You also learned how to encapsulate the call to the WriteSubstitution() method within an HTML helper method.</span></span>

<span data-ttu-id="0a709-167">尽可能利用缓存 ， 会对 Web 应用程序的性能产生显著影响。</span><span class="sxs-lookup"><span data-stu-id="0a709-167">Take advantage of caching whenever possible – it can have a dramatic impact on the performance of your web applications.</span></span> <span data-ttu-id="0a709-168">如本教程中所述，即使您需要在页面中显示动态内容，您也可以利用缓存。</span><span class="sxs-lookup"><span data-stu-id="0a709-168">As explained in this tutorial, you can take advantage of caching even when you need to display dynamic content in your pages.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="0a709-169">[上一页](improving-performance-with-output-caching-vb.md)
> [下一页](creating-a-controller-vb.md)</span><span class="sxs-lookup"><span data-stu-id="0a709-169">[Previous](improving-performance-with-output-caching-vb.md)
[Next](creating-a-controller-vb.md)</span></span>

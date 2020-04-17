---
uid: mvc/overview/older-versions-1/controllers-and-routing/improving-performance-with-output-caching-cs
title: 通过输出缓存 （C#） 提高性能 |微软文档
author: rick-anderson
description: 在本教程中，您将了解如何利用输出缓存来显著提高ASP.NET MVC Web 应用程序的性能。 你。。。
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 521c9117-81cd-4d8d-9d96-0256dc7bf50f
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/improving-performance-with-output-caching-cs
msc.type: authoredcontent
ms.openlocfilehash: a6dd43320117e235d12a13aa894302bbc767727c
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542711"
---
# <a name="improving-performance-with-output-caching-c"></a><span data-ttu-id="7190d-104">通过输出缓存提升性能 (C#)</span><span class="sxs-lookup"><span data-stu-id="7190d-104">Improving Performance with Output Caching (C#)</span></span>

<span data-ttu-id="7190d-105">由[微软](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="7190d-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="7190d-106">在本教程中，您将了解如何利用输出缓存来显著提高ASP.NET MVC Web 应用程序的性能。</span><span class="sxs-lookup"><span data-stu-id="7190d-106">In this tutorial, you learn how you can dramatically improve the performance of your ASP.NET MVC web applications by taking advantage of output caching.</span></span> <span data-ttu-id="7190d-107">您将了解如何缓存从控制器操作返回的结果，以便在每次新用户调用该操作时都不需要创建相同的内容。</span><span class="sxs-lookup"><span data-stu-id="7190d-107">You learn how to cache the result returned from a controller action so that the same content does not need to be created each and every time a new user invokes the action.</span></span>

<span data-ttu-id="7190d-108">本教程的目的是说明如何通过利用输出缓存显著提高ASP.NET MVC 应用程序的性能。</span><span class="sxs-lookup"><span data-stu-id="7190d-108">The goal of this tutorial is to explain how you can dramatically improve the performance of an ASP.NET MVC application by taking advantage of the output cache.</span></span> <span data-ttu-id="7190d-109">输出缓存使您能够缓存控制器操作返回的内容。</span><span class="sxs-lookup"><span data-stu-id="7190d-109">The output cache enables you to cache the content returned by a controller action.</span></span> <span data-ttu-id="7190d-110">这样，每次调用相同的控制器操作时，不需要生成相同的内容。</span><span class="sxs-lookup"><span data-stu-id="7190d-110">That way, the same content does not need to be generated each and every time the same controller action is invoked.</span></span>

<span data-ttu-id="7190d-111">例如，假设您ASP.NET MVC 应用程序在名为 Index 的视图中显示数据库记录的列表。</span><span class="sxs-lookup"><span data-stu-id="7190d-111">Imagine, for example, that your ASP.NET MVC application displays a list of database records in a view named Index.</span></span> <span data-ttu-id="7190d-112">通常，每次用户调用返回 Index 视图的控制器操作时，必须通过执行数据库查询从数据库检索数据库记录集。</span><span class="sxs-lookup"><span data-stu-id="7190d-112">Normally, each and every time that a user invokes the controller action that returns the Index view, the set of database records must be retrieved from the database by executing a database query.</span></span>

<span data-ttu-id="7190d-113">另一方面，如果利用输出缓存，则可以避免在每次任何用户调用相同的控制器操作时执行数据库查询。</span><span class="sxs-lookup"><span data-stu-id="7190d-113">If, on the other hand, you take advantage of the output cache then you can avoid executing a database query every time any user invokes the same controller action.</span></span> <span data-ttu-id="7190d-114">可以从缓存中检索视图，而不是从控制器操作中重新生成视图。</span><span class="sxs-lookup"><span data-stu-id="7190d-114">The view can be retrieved from the cache instead of being regenerated from the controller action.</span></span> <span data-ttu-id="7190d-115">缓存使您能够避免在服务器上执行冗余工作。</span><span class="sxs-lookup"><span data-stu-id="7190d-115">Caching enables you to avoid performing redundant work on the server.</span></span>

## <a name="enabling-output-caching"></a><span data-ttu-id="7190d-116">启用输出缓存</span><span class="sxs-lookup"><span data-stu-id="7190d-116">Enabling Output Caching</span></span>

<span data-ttu-id="7190d-117">通过将 [OutputCache] 属性添加到单个控制器操作或整个控制器类来启用输出缓存。</span><span class="sxs-lookup"><span data-stu-id="7190d-117">You enable output caching by adding an [OutputCache] attribute to either an individual controller action or an entire controller class.</span></span> <span data-ttu-id="7190d-118">例如，清单 1 中的控制器公开名为 Index（） 的操作。</span><span class="sxs-lookup"><span data-stu-id="7190d-118">For example, the controller in Listing 1 exposes an action named Index().</span></span> <span data-ttu-id="7190d-119">索引（） 操作的输出缓存 10 秒。</span><span class="sxs-lookup"><span data-stu-id="7190d-119">The output of the Index() action is cached for 10 seconds.</span></span>

<span data-ttu-id="7190d-120">**清单1 = 控制器\主控制器.cs**</span><span class="sxs-lookup"><span data-stu-id="7190d-120">**Listing 1 – Controllers\HomeController.cs**</span></span>

[!code-csharp[Main](improving-performance-with-output-caching-cs/samples/sample1.cs)]

<span data-ttu-id="7190d-121">在 ASP.NET MVC 的 Beta 版本中，输出缓存不适用于像[http://www.MySite.com/](http://www.mysite.com/)的 URL。</span><span class="sxs-lookup"><span data-stu-id="7190d-121">In the Beta versions of ASP.NET MVC, output caching does not work for a URL like [http://www.MySite.com/](http://www.mysite.com/).</span></span> <span data-ttu-id="7190d-122">相反，您必须输入像[http://www.MySite.com/Home/Index](http://www.mysite.com/Home/Index)的 URL。</span><span class="sxs-lookup"><span data-stu-id="7190d-122">Instead, you must enter a URL like [http://www.MySite.com/Home/Index](http://www.mysite.com/Home/Index).</span></span> 

<span data-ttu-id="7190d-123">在清单 1 中，索引（） 操作的输出缓存 10 秒。</span><span class="sxs-lookup"><span data-stu-id="7190d-123">In Listing 1, the output of the Index() action is cached for 10 seconds.</span></span> <span data-ttu-id="7190d-124">如果您愿意，可以指定更长的缓存持续时间。</span><span class="sxs-lookup"><span data-stu-id="7190d-124">If you prefer, you can specify a much longer cache duration.</span></span> <span data-ttu-id="7190d-125">例如，如果要缓存控制器操作的输出一天，则可以指定 86400 秒（60 秒\*60 分钟\*24 小时）的缓存持续时间。</span><span class="sxs-lookup"><span data-stu-id="7190d-125">For example, if you want to cache the output of a controller action for one day then you can specify a cache duration of 86400 seconds (60 seconds \* 60 minutes \* 24 hours).</span></span>

<span data-ttu-id="7190d-126">不能保证内容将在您指定的时间量内缓存。</span><span class="sxs-lookup"><span data-stu-id="7190d-126">There is no guarantee that content will be cached for the amount of time that you specify.</span></span> <span data-ttu-id="7190d-127">当内存资源变低时，缓存将自动开始驱逐内容。</span><span class="sxs-lookup"><span data-stu-id="7190d-127">When memory resources become low, the cache starts evicting content automatically.</span></span>

<span data-ttu-id="7190d-128">清单 1 中的主控制器返回清单 2 中的索引视图。</span><span class="sxs-lookup"><span data-stu-id="7190d-128">The Home controller in Listing 1 returns the Index view in Listing 2.</span></span> <span data-ttu-id="7190d-129">这个观点没有什么特别之处。</span><span class="sxs-lookup"><span data-stu-id="7190d-129">There is nothing special about this view.</span></span> <span data-ttu-id="7190d-130">索引视图仅显示当前时间（参见图 1）。</span><span class="sxs-lookup"><span data-stu-id="7190d-130">The Index view simply displays the current time (see Figure 1).</span></span>

<span data-ttu-id="7190d-131">**清单 2 = 视图\home_Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="7190d-131">**Listing 2 – Views\Home\Index.aspx**</span></span>

[!code-aspx[Main](improving-performance-with-output-caching-cs/samples/sample2.aspx)]

<span data-ttu-id="7190d-132">**图 1 = 缓存索引视图**</span><span class="sxs-lookup"><span data-stu-id="7190d-132">**Figure 1 – Cached Index view**</span></span>

![clip_image002](improving-performance-with-output-caching-cs/_static/image1.jpg)

<span data-ttu-id="7190d-134">如果通过在浏览器的地址栏中输入 URL /Home/Index 并反复点击浏览器中的"刷新/重新加载"按钮来多次调用 Index（） 操作，则 Index 视图显示的时间在 10 秒内不会更改。</span><span class="sxs-lookup"><span data-stu-id="7190d-134">If you invoke the Index() action multiple times by entering the URL /Home/Index in the address bar of your browser and hitting the Refresh/Reload button in your browser repeatedly, then the time displayed by the Index view won't change for 10 seconds.</span></span> <span data-ttu-id="7190d-135">将显示相同的时间，因为视图是缓存的。</span><span class="sxs-lookup"><span data-stu-id="7190d-135">The same time is displayed because the view is cached.</span></span>

<span data-ttu-id="7190d-136">请务必了解，对于访问应用程序的每个人，缓存相同的视图。</span><span class="sxs-lookup"><span data-stu-id="7190d-136">It is important to understand that the same view is cached for everyone who visits your application.</span></span> <span data-ttu-id="7190d-137">调用 Index（） 操作的任何人都可以获得相同的索引视图缓存版本。</span><span class="sxs-lookup"><span data-stu-id="7190d-137">Anyone who invokes the Index() action will get the same cached version of the Index view.</span></span> <span data-ttu-id="7190d-138">这意味着 Web 服务器为索引视图提供服务而必须执行的工作量将大大减少。</span><span class="sxs-lookup"><span data-stu-id="7190d-138">This means that the amount of work that the web server must perform to serve the Index view is dramatically reduced.</span></span>

<span data-ttu-id="7190d-139">清单2中的视图碰巧在做一些非常简单的事情。</span><span class="sxs-lookup"><span data-stu-id="7190d-139">The view in Listing 2 happens to be doing something really simple.</span></span> <span data-ttu-id="7190d-140">视图仅显示当前时间。</span><span class="sxs-lookup"><span data-stu-id="7190d-140">The view just displays the current time.</span></span> <span data-ttu-id="7190d-141">但是，您可以同样轻松地缓存显示一组数据库记录的视图。</span><span class="sxs-lookup"><span data-stu-id="7190d-141">However, you could just as easily cache a view that displays a set of database records.</span></span> <span data-ttu-id="7190d-142">在这种情况下，每次调用返回视图的控制器操作时，就不需要从数据库中检索数据库记录集。</span><span class="sxs-lookup"><span data-stu-id="7190d-142">In that case, the set of database records would not need to be retrieved from the database each and every time the controller action that returns the view is invoked.</span></span> <span data-ttu-id="7190d-143">缓存可以减少 Web 服务器和数据库服务器必须执行的工作量。</span><span class="sxs-lookup"><span data-stu-id="7190d-143">Caching can reduce the amount of work that both your web server and database server must perform.</span></span>

<span data-ttu-id="7190d-144">不要在 MVC 视图中&lt;使用页面 %@&gt;输出缓存 % 指令。</span><span class="sxs-lookup"><span data-stu-id="7190d-144">Don't use the page &lt;%@ OutputCache %&gt; directive in an MVC view.</span></span> <span data-ttu-id="7190d-145">此指令正在从 Web 窗体世界中出血，不应在 mVC 应用程序中ASP.NET中使用。</span><span class="sxs-lookup"><span data-stu-id="7190d-145">This directive is bleeding over from the Web Forms world and should not be used in an ASP.NET MVC application.</span></span>

## <a name="where-content-is-cached"></a><span data-ttu-id="7190d-146">缓存内容的位置</span><span class="sxs-lookup"><span data-stu-id="7190d-146">Where Content is Cached</span></span>

<span data-ttu-id="7190d-147">默认情况下，当您使用 [OutputCache] 属性时，内容缓存在三个位置：Web 服务器、任何代理服务器和 Web 浏览器。</span><span class="sxs-lookup"><span data-stu-id="7190d-147">By default, when you use the [OutputCache] attribute, content is cached in three locations: the web server, any proxy servers, and the web browser.</span></span> <span data-ttu-id="7190d-148">您可以通过修改 [OutputCache] 属性的位置属性来准确控制内容的缓存位置。</span><span class="sxs-lookup"><span data-stu-id="7190d-148">You can control exactly where content is cached by modifying the Location property of the [OutputCache] attribute.</span></span>

<span data-ttu-id="7190d-149">您可以将"位置"属性设置为以下任一值：</span><span class="sxs-lookup"><span data-stu-id="7190d-149">You can set the Location property to any one of the following values:</span></span>

> <span data-ttu-id="7190d-150">·任何</span><span class="sxs-lookup"><span data-stu-id="7190d-150">· Any</span></span>
> 
> <span data-ttu-id="7190d-151">·客户</span><span class="sxs-lookup"><span data-stu-id="7190d-151">· Client</span></span>
> 
> <span data-ttu-id="7190d-152">·下游</span><span class="sxs-lookup"><span data-stu-id="7190d-152">· Downstream</span></span>
> 
> <span data-ttu-id="7190d-153">·服务器</span><span class="sxs-lookup"><span data-stu-id="7190d-153">· Server</span></span>
> 
> <span data-ttu-id="7190d-154">·没有</span><span class="sxs-lookup"><span data-stu-id="7190d-154">· None</span></span>
> 
> <span data-ttu-id="7190d-155">·服务器和客户端</span><span class="sxs-lookup"><span data-stu-id="7190d-155">· ServerAndClient</span></span>

<span data-ttu-id="7190d-156">默认情况下，"位置"属性具有"Any"的值。</span><span class="sxs-lookup"><span data-stu-id="7190d-156">By default, the Location property has the value Any.</span></span> <span data-ttu-id="7190d-157">但是，在某些情况下，您可能只想在浏览器或服务器上缓存。</span><span class="sxs-lookup"><span data-stu-id="7190d-157">However, there are situations in which you might want to cache only on the browser or only on the server.</span></span> <span data-ttu-id="7190d-158">例如，如果要缓存针对每个用户进行个性化的信息，则不应在服务器上缓存信息。</span><span class="sxs-lookup"><span data-stu-id="7190d-158">For example, if you are caching information that is personalized for each user then you should not cache the information on the server.</span></span> <span data-ttu-id="7190d-159">如果要向不同的用户显示不同的信息，则应仅在客户端上缓存信息。</span><span class="sxs-lookup"><span data-stu-id="7190d-159">If you are displaying different information to different users then you should cache the information only on the client.</span></span>

<span data-ttu-id="7190d-160">例如，清单 3 中的控制器公开名为 GetName（） 的操作，该操作返回当前用户名。</span><span class="sxs-lookup"><span data-stu-id="7190d-160">For example, the controller in Listing 3 exposes an action named GetName() that returns the current user name.</span></span> <span data-ttu-id="7190d-161">如果 Jack 登录到网站并调用 GetName（） 操作，则该操作将返回字符串"嗨杰克"。</span><span class="sxs-lookup"><span data-stu-id="7190d-161">If Jack logs into the website and invokes the GetName() action then the action returns the string "Hi Jack".</span></span> <span data-ttu-id="7190d-162">如果，随后，Jill登录到网站并调用 GetName（） 操作，那么她也将得到字符串"嗨杰克"。</span><span class="sxs-lookup"><span data-stu-id="7190d-162">If, subsequently, Jill logs into the website and invokes the GetName() action then she also will get the string "Hi Jack".</span></span> <span data-ttu-id="7190d-163">在 Jack 最初调用控制器操作后，字符串将缓存在 Web 服务器上，供所有用户使用。</span><span class="sxs-lookup"><span data-stu-id="7190d-163">The string is cached on the web server for all users after Jack initially invokes the controller action.</span></span>

<span data-ttu-id="7190d-164">**清单3 = 控制器\BadUserController.cs**</span><span class="sxs-lookup"><span data-stu-id="7190d-164">**Listing 3 – Controllers\BadUserController.cs**</span></span>

[!code-csharp[Main](improving-performance-with-output-caching-cs/samples/sample3.cs)]

<span data-ttu-id="7190d-165">最有可能的是，清单 3 中的控制器不能以您想要的方式工作。</span><span class="sxs-lookup"><span data-stu-id="7190d-165">Most likely, the controller in Listing 3 does not work the way that you want.</span></span> <span data-ttu-id="7190d-166">您不想向吉尔显示"嗨杰克"的消息。</span><span class="sxs-lookup"><span data-stu-id="7190d-166">You don't want to display the message "Hi Jack" to Jill.</span></span>

<span data-ttu-id="7190d-167">不应在服务器缓存中缓存个性化内容。</span><span class="sxs-lookup"><span data-stu-id="7190d-167">You should never cache personalized content in the server cache.</span></span> <span data-ttu-id="7190d-168">但是，您可能希望在浏览器缓存中缓存个性化内容以提高性能。</span><span class="sxs-lookup"><span data-stu-id="7190d-168">However, you might want to cache the personalized content in the browser cache to improve performance.</span></span> <span data-ttu-id="7190d-169">如果在浏览器中缓存内容，并且用户多次调用同一控制器操作，则可以从浏览器缓存而不是服务器检索内容。</span><span class="sxs-lookup"><span data-stu-id="7190d-169">If you cache content in the browser, and a user invokes the same controller action multiple times, then the content can be retrieved from the browser cache instead of the server.</span></span>

<span data-ttu-id="7190d-170">清单 4 中修改后的控制器缓存 GetName（） 操作的输出。</span><span class="sxs-lookup"><span data-stu-id="7190d-170">The modified controller in Listing 4 caches the output of the GetName() action.</span></span> <span data-ttu-id="7190d-171">但是，内容仅缓存在浏览器上，而不是服务器上。</span><span class="sxs-lookup"><span data-stu-id="7190d-171">However, the content is cached only on the browser and not on the server.</span></span> <span data-ttu-id="7190d-172">这样，当多个用户调用 GetName（） 方法时，每个人都会获得自己的用户名，而不是其他人的用户名。</span><span class="sxs-lookup"><span data-stu-id="7190d-172">That way, when multiple users invoke the GetName() method, each person gets their own user name and not another person's user name.</span></span>

<span data-ttu-id="7190d-173">**清单4 = 控制器\用户控制器.cs**</span><span class="sxs-lookup"><span data-stu-id="7190d-173">**Listing 4 – Controllers\UserController.cs**</span></span>

[!code-csharp[Main](improving-performance-with-output-caching-cs/samples/sample4.cs)]

<span data-ttu-id="7190d-174">请注意，清单 4 中的 [OutputCache] 属性包含一个位置属性设置为值输出缓存位置.客户端。</span><span class="sxs-lookup"><span data-stu-id="7190d-174">Notice that the [OutputCache] attribute in Listing 4 includes a Location property set to the value OutputCacheLocation.Client.</span></span> <span data-ttu-id="7190d-175">[输出缓存] 属性还包括 NoStore 属性。</span><span class="sxs-lookup"><span data-stu-id="7190d-175">The [OutputCache] attribute also includes a NoStore property.</span></span> <span data-ttu-id="7190d-176">NoStore 属性用于通知代理服务器和浏览器它们不应存储缓存内容的永久副本。</span><span class="sxs-lookup"><span data-stu-id="7190d-176">The NoStore property is used to inform proxy servers and browser that they should not store a permanent copy of the cached content.</span></span>

## <a name="varying-the-output-cache"></a><span data-ttu-id="7190d-177">更改输出缓存</span><span class="sxs-lookup"><span data-stu-id="7190d-177">Varying the Output Cache</span></span>

<span data-ttu-id="7190d-178">在某些情况下，您可能需要相同内容的不同缓存版本。</span><span class="sxs-lookup"><span data-stu-id="7190d-178">In some situations, you might want different cached versions of the very same content.</span></span> <span data-ttu-id="7190d-179">例如，假设您正在创建一个母版/详细信息页。</span><span class="sxs-lookup"><span data-stu-id="7190d-179">Imagine, for example, that you are creating a master/detail page.</span></span> <span data-ttu-id="7190d-180">母版页显示电影标题的列表。</span><span class="sxs-lookup"><span data-stu-id="7190d-180">The master page displays a list of movie titles.</span></span> <span data-ttu-id="7190d-181">单击标题时，您将获得所选影片的详细信息。</span><span class="sxs-lookup"><span data-stu-id="7190d-181">When you click a title, you get details for the selected movie.</span></span>

<span data-ttu-id="7190d-182">如果缓存详细信息页，则无论单击哪个影片，都会显示同一影片的详细信息。</span><span class="sxs-lookup"><span data-stu-id="7190d-182">If you cache the details page, then the details for the same movie will be displayed no matter which movie you click.</span></span> <span data-ttu-id="7190d-183">第一个用户选择的第一个影片将显示给所有将来的用户。</span><span class="sxs-lookup"><span data-stu-id="7190d-183">The first movie selected by the first user will be displayed to all future users.</span></span>

<span data-ttu-id="7190d-184">您可以通过利用 [OutputCache] 属性的 VaryByParam 属性来解决此问题。</span><span class="sxs-lookup"><span data-stu-id="7190d-184">You can fix this problem by taking advantage of the VaryByParam property of the [OutputCache] attribute.</span></span> <span data-ttu-id="7190d-185">此属性使您能够在窗体参数或查询字符串参数不同时创建相同内容的不同缓存版本。</span><span class="sxs-lookup"><span data-stu-id="7190d-185">This property enables you to create different cached versions of the very same content when a form parameter or query string parameter varies.</span></span>

<span data-ttu-id="7190d-186">例如，清单 5 中的控制器公开名为 Master（） 和详细信息（） 的两个操作。</span><span class="sxs-lookup"><span data-stu-id="7190d-186">For example, the controller in Listing 5 exposes two actions named Master() and Details().</span></span> <span data-ttu-id="7190d-187">Master（） 操作返回影片标题列表，详细信息（） 操作返回所选影片的详细信息。</span><span class="sxs-lookup"><span data-stu-id="7190d-187">The Master() action returns a list of movie titles and the Details() action returns the details for the selected movie.</span></span>

<span data-ttu-id="7190d-188">**清单5 = 控制器\电影控制器.cs**</span><span class="sxs-lookup"><span data-stu-id="7190d-188">**Listing 5 – Controllers\MoviesController.cs**</span></span>

[!code-csharp[Main](improving-performance-with-output-caching-cs/samples/sample5.cs)]

<span data-ttu-id="7190d-189">Master（） 操作包括一个具有值"无"的 VaryByParam 属性。</span><span class="sxs-lookup"><span data-stu-id="7190d-189">The Master() action includes a VaryByParam property with the value "none".</span></span> <span data-ttu-id="7190d-190">调用 Master（） 操作时，将返回主视图的相同缓存版本。</span><span class="sxs-lookup"><span data-stu-id="7190d-190">When the Master() action is invoked, the same cached version of the Master view is returned.</span></span> <span data-ttu-id="7190d-191">忽略任何窗体参数或查询字符串参数（参见图 2）。</span><span class="sxs-lookup"><span data-stu-id="7190d-191">Any form parameters or query string parameters are ignored (see Figure 2).</span></span>

<span data-ttu-id="7190d-192">**图 2 = /电影/主视图**</span><span class="sxs-lookup"><span data-stu-id="7190d-192">**Figure 2 – The /Movies/Master view**</span></span>

![clip_image004](improving-performance-with-output-caching-cs/_static/image2.jpg)

<span data-ttu-id="7190d-194">**图 3 = /电影/详细信息视图**</span><span class="sxs-lookup"><span data-stu-id="7190d-194">**Figure 3 – The /Movies/Details view**</span></span>

![clip_image006](improving-performance-with-output-caching-cs/_static/image3.jpg)

<span data-ttu-id="7190d-196">详细信息（） 操作包括一个带值"Id"的 VaryByParam 属性。</span><span class="sxs-lookup"><span data-stu-id="7190d-196">The Details() action includes a VaryByParam property with the value "Id".</span></span> <span data-ttu-id="7190d-197">当将 Id 参数的不同值传递给控制器操作时，将生成"详细信息"视图的不同缓存版本。</span><span class="sxs-lookup"><span data-stu-id="7190d-197">When different values of the Id parameter are passed to the controller action, different cached versions of the Details view are generated.</span></span>

<span data-ttu-id="7190d-198">请务必了解，使用 VaryByParam 属性会导致缓存更多，而不是更少。</span><span class="sxs-lookup"><span data-stu-id="7190d-198">It is important to understand that using the VaryByParam property results in more caching and not less.</span></span> <span data-ttu-id="7190d-199">为 Id 参数的每个不同版本创建"详细信息"视图的不同缓存版本。</span><span class="sxs-lookup"><span data-stu-id="7190d-199">A different cached version of the Details view is created for each different version of the Id parameter.</span></span>

<span data-ttu-id="7190d-200">您可以将 VaryByParam 属性设置为以下值：</span><span class="sxs-lookup"><span data-stu-id="7190d-200">You can set the VaryByParam property to the following values:</span></span>

> <span data-ttu-id="7190d-201">\*• 每当窗体或查询字符串参数发生变化时，都会创建不同的缓存版本。</span><span class="sxs-lookup"><span data-stu-id="7190d-201">\* = Create a different cached version whenever a form or query string parameter varies.</span></span>
> 
> <span data-ttu-id="7190d-202">无 = 从不创建不同的缓存版本</span><span class="sxs-lookup"><span data-stu-id="7190d-202">none = Never create different cached versions</span></span>
> 
> <span data-ttu-id="7190d-203">参数的分号列表 = 每当列表中的任何窗体或查询字符串参数发生变化时，创建不同的缓存版本</span><span class="sxs-lookup"><span data-stu-id="7190d-203">Semicolon list of parameters = Create different cached versions whenever any of the form or query string parameters in the list varies</span></span>

## <a name="creating-a-cache-profile"></a><span data-ttu-id="7190d-204">创建缓存配置文件</span><span class="sxs-lookup"><span data-stu-id="7190d-204">Creating a Cache Profile</span></span>

<span data-ttu-id="7190d-205">作为通过修改 [OutputCache] 属性的属性来配置输出缓存属性的替代方法，您可以在 Web 配置 （web.config） 文件中创建缓存配置文件。</span><span class="sxs-lookup"><span data-stu-id="7190d-205">As an alternative to configuring output cache properties by modifying properties of the [OutputCache] attribute, you can create a cache profile in the web configuration (web.config) file.</span></span> <span data-ttu-id="7190d-206">在 Web 配置文件中创建缓存配置文件具有几个重要优势。</span><span class="sxs-lookup"><span data-stu-id="7190d-206">Creating a cache profile in the web configuration file offers a couple of important advantages.</span></span>

<span data-ttu-id="7190d-207">首先，通过在 Web 配置文件中配置输出缓存，可以控制控制器操作如何在一个中心位置缓存内容。</span><span class="sxs-lookup"><span data-stu-id="7190d-207">First, by configuring output caching in the web configuration file, you can control how controller actions cache content in one central location.</span></span> <span data-ttu-id="7190d-208">您可以创建一个缓存配置文件，并将配置文件应用于多个控制器或控制器操作。</span><span class="sxs-lookup"><span data-stu-id="7190d-208">You can create one cache profile and apply the profile to several controllers or controller actions.</span></span>

<span data-ttu-id="7190d-209">其次，您可以修改 Web 配置文件，而无需重新编译应用程序。</span><span class="sxs-lookup"><span data-stu-id="7190d-209">Second, you can modify the web configuration file without recompiling your application.</span></span> <span data-ttu-id="7190d-210">如果需要禁用已部署到生产中的应用程序的缓存，则只需修改 Web 配置文件中定义的缓存配置文件即可。</span><span class="sxs-lookup"><span data-stu-id="7190d-210">If you need to disable caching for an application that has already been deployed to production, then you can simply modify the cache profiles defined in the web configuration file.</span></span> <span data-ttu-id="7190d-211">将自动检测并应用对 Web 配置文件的任何更改。</span><span class="sxs-lookup"><span data-stu-id="7190d-211">Any changes to the web configuration file will be detected automatically and applied.</span></span>

<span data-ttu-id="7190d-212">例如，清单&lt;6&gt;中的缓存 Web 配置部分定义名为 Cache1Hour 的缓存配置文件。</span><span class="sxs-lookup"><span data-stu-id="7190d-212">For example, the &lt;caching&gt; web configuration section in Listing 6 defines a cache profile named Cache1Hour.</span></span> <span data-ttu-id="7190d-213">&lt;缓存&gt;部分必须出现在 Web 配置文件&lt;的 system.web&gt;部分中。</span><span class="sxs-lookup"><span data-stu-id="7190d-213">The &lt;caching&gt; section must appear within the &lt;system.web&gt; section of a web configuration file.</span></span>

<span data-ttu-id="7190d-214">**清单6 = Web.config 的缓存部分**</span><span class="sxs-lookup"><span data-stu-id="7190d-214">**Listing 6 – Caching section for web.config**</span></span>

[!code-xml[Main](improving-performance-with-output-caching-cs/samples/sample6.xml)]

<span data-ttu-id="7190d-215">清单7中的控制器说明了如何将 Cache1Hour 配置文件应用于具有 [OutputCache] 属性的控制器操作。</span><span class="sxs-lookup"><span data-stu-id="7190d-215">The controller in Listing 7 illustrates how you can apply the Cache1Hour profile to a controller action with the [OutputCache] attribute.</span></span>

<span data-ttu-id="7190d-216">**清单7 = 控制器\配置文件控制器.cs**</span><span class="sxs-lookup"><span data-stu-id="7190d-216">**Listing 7 – Controllers\ProfileController.cs**</span></span>

[!code-csharp[Main](improving-performance-with-output-caching-cs/samples/sample7.cs)]

<span data-ttu-id="7190d-217">如果调用清单 7 中控制器公开的 Index（） 操作，则将返回相同的时间 1 小时。</span><span class="sxs-lookup"><span data-stu-id="7190d-217">If you invoke the Index() action exposed by the controller in Listing 7 then the same time will be returned for 1 hour.</span></span>

## <a name="summary"></a><span data-ttu-id="7190d-218">总结</span><span class="sxs-lookup"><span data-stu-id="7190d-218">Summary</span></span>

<span data-ttu-id="7190d-219">输出缓存为您提供了一种非常简单的方法来显著提高ASP.NET MVC 应用程序的性能。</span><span class="sxs-lookup"><span data-stu-id="7190d-219">Output caching provides you with a very easy method of dramatically improving the performance of your ASP.NET MVC applications.</span></span> <span data-ttu-id="7190d-220">在本教程中，您学习了如何使用 [OutputCache] 属性来缓存控制器操作的输出。</span><span class="sxs-lookup"><span data-stu-id="7190d-220">In this tutorial, you learned how to use the [OutputCache] attribute to cache the output of controller actions.</span></span> <span data-ttu-id="7190d-221">您还学习了如何修改 [OutputCache] 属性的属性，如持续时间和 VaryByParam 属性，以修改内容的缓存方式。</span><span class="sxs-lookup"><span data-stu-id="7190d-221">You also learned how to modify properties of the [OutputCache] attribute such as the Duration and VaryByParam properties to modify how content gets cached.</span></span> <span data-ttu-id="7190d-222">最后，您学习了如何在 Web 配置文件中定义缓存配置文件。</span><span class="sxs-lookup"><span data-stu-id="7190d-222">Finally, you learned how to define cache profiles in the web configuration file.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="7190d-223">[上一页](understanding-action-filters-cs.md)
> [下一页](adding-dynamic-content-to-a-cached-page-cs.md)</span><span class="sxs-lookup"><span data-stu-id="7190d-223">[Previous](understanding-action-filters-cs.md)
[Next](adding-dynamic-content-to-a-cached-page-cs.md)</span></span>

---
uid: mvc/overview/older-versions-1/views/passing-data-to-view-master-pages-vb
title: 将数据传递到查看母版页 （VB） |微软文档
author: rick-anderson
description: 本教程的目的是解释如何将数据从控制器传递到视图母版页。 我们检查将数据传递到视图的两种策略...
ms.author: riande
ms.date: 10/16/2008
ms.assetid: 37a1ebae-8773-408f-8645-d21da7ff9ae1
msc.legacyurl: /mvc/overview/older-versions-1/views/passing-data-to-view-master-pages-vb
msc.type: authoredcontent
ms.openlocfilehash: ef65541a5f2297414f923e2f8108a14de67531e5
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542464"
---
# <a name="passing-data-to-view-master-pages-vb"></a><span data-ttu-id="e5169-104">向视图母版页传递数据 (VB)</span><span class="sxs-lookup"><span data-stu-id="e5169-104">Passing Data to View Master Pages (VB)</span></span>

<span data-ttu-id="e5169-105">由[微软](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="e5169-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="e5169-106">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="e5169-106">Download PDF</span></span>](https://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_13_VB.pdf)

> <span data-ttu-id="e5169-107">本教程的目的是解释如何将数据从控制器传递到视图母版页。</span><span class="sxs-lookup"><span data-stu-id="e5169-107">The goal of this tutorial is to explain how you can pass data from a controller to a view master page.</span></span> <span data-ttu-id="e5169-108">我们检查将数据传递到视图母版页的两种策略。</span><span class="sxs-lookup"><span data-stu-id="e5169-108">We examine two strategies for passing data to a view master page.</span></span> <span data-ttu-id="e5169-109">首先，我们讨论一个简单的解决方案，该解决方案会导致应用程序难以维护。</span><span class="sxs-lookup"><span data-stu-id="e5169-109">First, we discuss an easy solution that results in an application that is difficult to maintain.</span></span> <span data-ttu-id="e5169-110">接下来，我们将研究一个更好的解决方案，它需要更多的初始工作，但会产生一个更可维护的应用程序。</span><span class="sxs-lookup"><span data-stu-id="e5169-110">Next, we examine a much better solution that requires a little more initial work but results in a much more maintainable application.</span></span>

## <a name="passing-data-to-view-master-pages"></a><span data-ttu-id="e5169-111">将数据传递到查看母版页</span><span class="sxs-lookup"><span data-stu-id="e5169-111">Passing Data to View Master Pages</span></span>

<span data-ttu-id="e5169-112">本教程的目的是解释如何将数据从控制器传递到视图母版页。</span><span class="sxs-lookup"><span data-stu-id="e5169-112">The goal of this tutorial is to explain how you can pass data from a controller to a view master page.</span></span> <span data-ttu-id="e5169-113">我们检查将数据传递到视图母版页的两种策略。</span><span class="sxs-lookup"><span data-stu-id="e5169-113">We examine two strategies for passing data to a view master page.</span></span> <span data-ttu-id="e5169-114">首先，我们讨论一个简单的解决方案，该解决方案会导致应用程序难以维护。</span><span class="sxs-lookup"><span data-stu-id="e5169-114">First, we discuss an easy solution that results in an application that is difficult to maintain.</span></span> <span data-ttu-id="e5169-115">接下来，我们将研究一个更好的解决方案，它需要更多的初始工作，但会产生一个更可维护的应用程序。</span><span class="sxs-lookup"><span data-stu-id="e5169-115">Next, we examine a much better solution that requires a little more initial work but results in a much more maintainable application.</span></span>

### <a name="the-problem"></a><span data-ttu-id="e5169-116">问题</span><span class="sxs-lookup"><span data-stu-id="e5169-116">The Problem</span></span>

<span data-ttu-id="e5169-117">假设您正在构建一个影片数据库应用程序，并且您想要在应用程序的每一页上显示影片类别列表（参见图 1）。</span><span class="sxs-lookup"><span data-stu-id="e5169-117">Imagine that you are building a movie database application and you want to display the list of movie categories on every page in your application (see Figure 1).</span></span> <span data-ttu-id="e5169-118">此外，假设影片类别列表存储在数据库表中。</span><span class="sxs-lookup"><span data-stu-id="e5169-118">Imagine, furthermore, that the list of movie categories is stored in a database table.</span></span> <span data-ttu-id="e5169-119">在这种情况下，从数据库中检索类别并在视图母版页中呈现影片类别列表是有意义的。</span><span class="sxs-lookup"><span data-stu-id="e5169-119">In that case, it would make sense to retrieve the categories from the database and render the list of movie categories within a view master page.</span></span>

<span data-ttu-id="e5169-120">[![在视图母版页中显示影片类别](passing-data-to-view-master-pages-vb/_static/image2.png)](passing-data-to-view-master-pages-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="e5169-120">[![Displaying movie categories in a view master page](passing-data-to-view-master-pages-vb/_static/image2.png)](passing-data-to-view-master-pages-vb/_static/image1.png)</span></span>

<span data-ttu-id="e5169-121">**图 01**： 在视图母版页中显示影片类别 （[单击以查看全尺寸图像](passing-data-to-view-master-pages-vb/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="e5169-121">**Figure 01**: Displaying movie categories in a view master page ([Click to view full-size image](passing-data-to-view-master-pages-vb/_static/image3.png))</span></span>

<span data-ttu-id="e5169-122">这就是问题所在。</span><span class="sxs-lookup"><span data-stu-id="e5169-122">Here's the problem.</span></span> <span data-ttu-id="e5169-123">如何检索母版页中的电影类别列表？</span><span class="sxs-lookup"><span data-stu-id="e5169-123">How do you retrieve the list of movie categories in the master page?</span></span> <span data-ttu-id="e5169-124">在母版页中直接调用模型类的方法是很有诱惑力的。</span><span class="sxs-lookup"><span data-stu-id="e5169-124">It is tempting to call methods of your model classes in the master page directly.</span></span> <span data-ttu-id="e5169-125">换句话说，最好在母版页中包含从数据库检索数据的代码。</span><span class="sxs-lookup"><span data-stu-id="e5169-125">In other words, it is tempting to include the code for retrieving the data from the database right in your master page.</span></span> <span data-ttu-id="e5169-126">但是，绕过 MVC 控制器访问数据库将违反完全分离问题是构建 MVC 应用程序的主要好处之一。</span><span class="sxs-lookup"><span data-stu-id="e5169-126">However, bypassing your MVC controllers to access the database would violate the clean separation of concerns that is one of the primary benefits of building an MVC application.</span></span>

<span data-ttu-id="e5169-127">在 MVC 应用程序中，您希望 MVC 视图和 MVC 模型之间的所有交互都由 MVC 控制器处理。</span><span class="sxs-lookup"><span data-stu-id="e5169-127">In an MVC application, you want all interaction between your MVC views and your MVC model to be handled by your MVC controllers.</span></span> <span data-ttu-id="e5169-128">这种关注点的分离产生了更可维护、适应性强和可测试的应用。</span><span class="sxs-lookup"><span data-stu-id="e5169-128">This separation of concerns results in a more maintainable, adaptable, and testable application.</span></span>

<span data-ttu-id="e5169-129">在 MVC 应用程序中，传递给视图的所有数据（包括视图母版页）都应通过控制器操作传递到视图。</span><span class="sxs-lookup"><span data-stu-id="e5169-129">In an MVC application, all data passed to a view – including a view master page – should be passed to a view by a controller action.</span></span> <span data-ttu-id="e5169-130">此外，数据应利用视图数据传递。</span><span class="sxs-lookup"><span data-stu-id="e5169-130">Furthermore, the data should be passed by taking advantage of view data.</span></span> <span data-ttu-id="e5169-131">在本教程的其余部分中，我将检查将视图数据传递到视图母版页的两种方法。</span><span class="sxs-lookup"><span data-stu-id="e5169-131">In the remainder of this tutorial, I examine two methods of passing view data to a view master page.</span></span>

### <a name="the-simple-solution"></a><span data-ttu-id="e5169-132">简单解决方案</span><span class="sxs-lookup"><span data-stu-id="e5169-132">The Simple Solution</span></span>

<span data-ttu-id="e5169-133">让我们从将视图数据从控制器传递到视图母版页的最简单的解决方案开始。</span><span class="sxs-lookup"><span data-stu-id="e5169-133">Let's start with the simplest solution to passing view data from a controller to a view master page.</span></span> <span data-ttu-id="e5169-134">最简单的解决方案是在每个控制器操作中传递母版页的视图数据。</span><span class="sxs-lookup"><span data-stu-id="e5169-134">The simplest solution is to pass the view data for the master page in each and every controller action.</span></span>

<span data-ttu-id="e5169-135">考虑清单 1 中的控制器。</span><span class="sxs-lookup"><span data-stu-id="e5169-135">Consider the controller in Listing 1.</span></span> <span data-ttu-id="e5169-136">它公开名为`Index()`和`Details()`的两个操作。</span><span class="sxs-lookup"><span data-stu-id="e5169-136">It exposes two actions named `Index()` and `Details()`.</span></span> <span data-ttu-id="e5169-137">操作`Index()`方法返回"影片"数据库表中的每个影片。</span><span class="sxs-lookup"><span data-stu-id="e5169-137">The `Index()` action method returns every movie in the Movies database table.</span></span> <span data-ttu-id="e5169-138">操作`Details()`方法返回特定影片类别中的每部电影。</span><span class="sxs-lookup"><span data-stu-id="e5169-138">The `Details()` action method returns every movie in a particular movie category.</span></span>

<span data-ttu-id="e5169-139">**清单1 |`Controllers\HomeController.vb`**</span><span class="sxs-lookup"><span data-stu-id="e5169-139">**Listing 1 – `Controllers\HomeController.vb`**</span></span>

[!code-vb[Main](passing-data-to-view-master-pages-vb/samples/sample1.vb)]

<span data-ttu-id="e5169-140">请注意，和`Index()``Details()`操作都添加两个项以查看数据。</span><span class="sxs-lookup"><span data-stu-id="e5169-140">Notice that both the `Index()` and the `Details()` actions add two items to view data.</span></span> <span data-ttu-id="e5169-141">该`Index()`操作添加了两个键：类别和影片。</span><span class="sxs-lookup"><span data-stu-id="e5169-141">The `Index()` action adds two keys: categories and movies.</span></span> <span data-ttu-id="e5169-142">类别键表示视图母版页显示的电影类别列表。</span><span class="sxs-lookup"><span data-stu-id="e5169-142">The categories key represents the list of movie categories displayed by the view master page.</span></span> <span data-ttu-id="e5169-143">影片键表示"索引"视图页显示的影片列表。</span><span class="sxs-lookup"><span data-stu-id="e5169-143">The movies key represents the list of movies displayed by the Index view page.</span></span>

<span data-ttu-id="e5169-144">该`Details()`操作还添加了两个名为类别和影片的键。</span><span class="sxs-lookup"><span data-stu-id="e5169-144">The `Details()` action also adds two keys named categories and movies.</span></span> <span data-ttu-id="e5169-145">类别键再次表示视图母版页显示的电影类别列表。</span><span class="sxs-lookup"><span data-stu-id="e5169-145">The categories key, once again, represents the list of movie categories displayed by the view master page.</span></span> <span data-ttu-id="e5169-146">影片键表示"详细信息"视图页显示的特定类别中的电影列表（参见图 2）。</span><span class="sxs-lookup"><span data-stu-id="e5169-146">The movies key represents the list of movies in a particular category displayed by the Details view page (see Figure 2).</span></span>

<span data-ttu-id="e5169-147">[!["详细信息"视图](passing-data-to-view-master-pages-vb/_static/image5.png)](passing-data-to-view-master-pages-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="e5169-147">[![The Details view](passing-data-to-view-master-pages-vb/_static/image5.png)](passing-data-to-view-master-pages-vb/_static/image4.png)</span></span>

<span data-ttu-id="e5169-148">**图 02**： "详细信息"视图 （[单击以查看全尺寸图像](passing-data-to-view-master-pages-vb/_static/image6.png)）</span><span class="sxs-lookup"><span data-stu-id="e5169-148">**Figure 02**: The Details view ([Click to view full-size image](passing-data-to-view-master-pages-vb/_static/image6.png))</span></span>

<span data-ttu-id="e5169-149">索引视图包含在清单 2 中。</span><span class="sxs-lookup"><span data-stu-id="e5169-149">The Index view is contained in Listing 2.</span></span> <span data-ttu-id="e5169-150">它只是遍达视图数据中由影片项表示的电影列表。</span><span class="sxs-lookup"><span data-stu-id="e5169-150">It simply iterates through the list of movies represented by the movies item in view data.</span></span>

<span data-ttu-id="e5169-151">**清单2 |`Views\Home\Index.aspx`**</span><span class="sxs-lookup"><span data-stu-id="e5169-151">**Listing 2 – `Views\Home\Index.aspx`**</span></span>

[!code-aspx[Main](passing-data-to-view-master-pages-vb/samples/sample2.aspx)]

<span data-ttu-id="e5169-152">视图母版页包含在清单 3 中。</span><span class="sxs-lookup"><span data-stu-id="e5169-152">The view master page is contained in Listing 3.</span></span> <span data-ttu-id="e5169-153">视图母版页从视图数据中参数地表示并呈现类别项表示的所有影片类别。</span><span class="sxs-lookup"><span data-stu-id="e5169-153">The view master page iterates and renders all of the movie categories represented by the categories item from view data.</span></span>

<span data-ttu-id="e5169-154">**清单3 |`Views\Shared\Site.master`**</span><span class="sxs-lookup"><span data-stu-id="e5169-154">**Listing 3 – `Views\Shared\Site.master`**</span></span>

[!code-aspx[Main](passing-data-to-view-master-pages-vb/samples/sample3.aspx)]

<span data-ttu-id="e5169-155">所有数据都通过视图数据传递到视图和视图母版页。</span><span class="sxs-lookup"><span data-stu-id="e5169-155">All data is passed to the view and the view master page through view data.</span></span> <span data-ttu-id="e5169-156">这是将数据传递到母版页的正确方法。</span><span class="sxs-lookup"><span data-stu-id="e5169-156">That is the correct way to pass data to the master page.</span></span>

<span data-ttu-id="e5169-157">那么，这个解决方案有什么问题呢？</span><span class="sxs-lookup"><span data-stu-id="e5169-157">So, what's wrong with this solution?</span></span> <span data-ttu-id="e5169-158">问题是，此解决方案违反了 DRY（不要重复自己）原则。</span><span class="sxs-lookup"><span data-stu-id="e5169-158">The problem is that this solution violates the DRY (Don't Repeat Yourself) principle.</span></span> <span data-ttu-id="e5169-159">每个控制器操作都必须添加完全相同的影片类别列表才能查看数据。</span><span class="sxs-lookup"><span data-stu-id="e5169-159">Each and every controller action must add the very same list of movie categories to view data.</span></span> <span data-ttu-id="e5169-160">应用程序中具有重复的代码会使应用程序更难维护、调整和修改。</span><span class="sxs-lookup"><span data-stu-id="e5169-160">Having duplicate code in your application makes your application much more difficult to maintain, adapt, and modify.</span></span>

### <a name="the-good-solution"></a><span data-ttu-id="e5169-161">良好的解决方案</span><span class="sxs-lookup"><span data-stu-id="e5169-161">The Good Solution</span></span>

<span data-ttu-id="e5169-162">在本节中，我们将检查将数据从控制器操作传递到视图母版页的替代方法和更好的解决方案。</span><span class="sxs-lookup"><span data-stu-id="e5169-162">In this section, we examine an alternative, and better, solution to passing data from a controller action to a view master page.</span></span> <span data-ttu-id="e5169-163">我们不是在每个控制器操作中添加母版页的影片类别，而是仅将影片类别添加到视图数据一次。</span><span class="sxs-lookup"><span data-stu-id="e5169-163">Instead of adding the movie categories for the master page in each and every controller action, we add the movie categories to the view data only once.</span></span> <span data-ttu-id="e5169-164">视图母版页使用的所有视图数据都添加到应用程序控制器中。</span><span class="sxs-lookup"><span data-stu-id="e5169-164">All view data used by the view master page is added in an Application controller.</span></span>

<span data-ttu-id="e5169-165">应用程序控制器类包含在清单 4 中。</span><span class="sxs-lookup"><span data-stu-id="e5169-165">The ApplicationController class is contained in Listing 4.</span></span>

<span data-ttu-id="e5169-166">应用程序控制器类包含在清单 4 中。</span><span class="sxs-lookup"><span data-stu-id="e5169-166">The ApplicationController class is contained in Listing 4.</span></span>

<span data-ttu-id="e5169-167">**清单4 |`Controllers\ApplicationController.vb`**</span><span class="sxs-lookup"><span data-stu-id="e5169-167">**Listing 4 – `Controllers\ApplicationController.vb`**</span></span>

[!code-vb[Main](passing-data-to-view-master-pages-vb/samples/sample4.vb)]

<span data-ttu-id="e5169-168">关于清单4中的应用程序控制器，您应该注意三件事。</span><span class="sxs-lookup"><span data-stu-id="e5169-168">There are three things that you should notice about the Application controller in Listing 4.</span></span> <span data-ttu-id="e5169-169">首先，请注意，类从基 System.Web.Mvc.Controller 类继承。</span><span class="sxs-lookup"><span data-stu-id="e5169-169">First, notice that the class inherits from the base System.Web.Mvc.Controller class.</span></span> <span data-ttu-id="e5169-170">应用程序控制器是控制器类。</span><span class="sxs-lookup"><span data-stu-id="e5169-170">The Application controller is a controller class.</span></span>

<span data-ttu-id="e5169-171">其次，请注意应用程序控制器类是必继承类。</span><span class="sxs-lookup"><span data-stu-id="e5169-171">Second, notice that the Application controller class is a MustInherit class.</span></span> <span data-ttu-id="e5169-172">MustInherit 类是一个必须由具体类实现的类。</span><span class="sxs-lookup"><span data-stu-id="e5169-172">An MustInherit class is a class that must be implemented by a concrete class.</span></span> <span data-ttu-id="e5169-173">由于应用程序控制器是 MustInherit 类，因此不能直接调用类中定义的任何方法。</span><span class="sxs-lookup"><span data-stu-id="e5169-173">Because the Application controller is an MustInherit class, you cannot not invoke any methods defined in the class directly.</span></span> <span data-ttu-id="e5169-174">如果尝试直接调用应用程序类，则会收到"找不到资源"错误消息。</span><span class="sxs-lookup"><span data-stu-id="e5169-174">If you attempt to invoke the Application class directly then you'll get a Resource Cannot Be Found error message.</span></span>

<span data-ttu-id="e5169-175">第三，请注意，应用程序控制器包含一个构造函数，该构造函数添加要查看数据的影片类别列表。</span><span class="sxs-lookup"><span data-stu-id="e5169-175">Third, notice that the Application controller contains a constructor that adds the list of movie categories to view data.</span></span> <span data-ttu-id="e5169-176">从应用程序控制器继承的每个控制器类都会自动调用应用程序控制器的构造函数。</span><span class="sxs-lookup"><span data-stu-id="e5169-176">Every controller class that inherits from the Application controller calls the Application controller's constructor automatically.</span></span> <span data-ttu-id="e5169-177">每当对从应用程序控制器继承的任何控制器调用任何操作时，影片类别将自动包含在视图数据中。</span><span class="sxs-lookup"><span data-stu-id="e5169-177">Whenever you call any action on any controller that inherits from the Application controller, the movie categories is included in the view data automatically.</span></span>

<span data-ttu-id="e5169-178">清单 5 中的影片控制器从应用程序控制器继承。</span><span class="sxs-lookup"><span data-stu-id="e5169-178">The Movies controller in Listing 5 inherits from the Application controller.</span></span>

<span data-ttu-id="e5169-179">**清单5 |`Controllers\MoviesController.vb`**</span><span class="sxs-lookup"><span data-stu-id="e5169-179">**Listing 5 – `Controllers\MoviesController.vb`**</span></span>

[!code-vb[Main](passing-data-to-view-master-pages-vb/samples/sample5.vb)]

<span data-ttu-id="e5169-180">与上一节中讨论的"家庭控制器"一样，电影控制器公开了名为`Index()`和`Details()`的两种操作方法。</span><span class="sxs-lookup"><span data-stu-id="e5169-180">The Movies controller, just like the Home controller discussed in the previous section, exposes two action methods named `Index()` and `Details()`.</span></span> <span data-ttu-id="e5169-181">请注意，视图母版页显示的影片类别列表不会添加以查看 或`Index()``Details()`方法中的数据。</span><span class="sxs-lookup"><span data-stu-id="e5169-181">Notice that the list of movie categories displayed by the view master page is not added to view data in either the `Index()` or `Details()` method.</span></span> <span data-ttu-id="e5169-182">由于"影片"控制器从应用程序控制器继承，因此将添加影片类别列表以自动查看数据。</span><span class="sxs-lookup"><span data-stu-id="e5169-182">Because the Movies controller inherits from the Application controller, the list of movie categories is added to view data automatically.</span></span>

<span data-ttu-id="e5169-183">请注意，此为视图母版页添加视图数据的解决方案并不违反 DRY（不要重复自己）原则。</span><span class="sxs-lookup"><span data-stu-id="e5169-183">Notice that this solution to adding view data for a view master page does not violate the DRY (Don't Repeat Yourself) principle.</span></span> <span data-ttu-id="e5169-184">添加要查看数据的影片类别列表的代码仅包含在一个位置：应用程序控制器的构造函数。</span><span class="sxs-lookup"><span data-stu-id="e5169-184">The code for adding the list of movie categories to view data is contained in only one location: the constructor for the Application controller.</span></span>

### <a name="summary"></a><span data-ttu-id="e5169-185">总结</span><span class="sxs-lookup"><span data-stu-id="e5169-185">Summary</span></span>

<span data-ttu-id="e5169-186">在本教程中，我们讨论了将视图数据从控制器传递到视图母版页的两种方法。</span><span class="sxs-lookup"><span data-stu-id="e5169-186">In this tutorial, we discussed two approaches to passing view data from a controller to a view master page.</span></span> <span data-ttu-id="e5169-187">首先，我们研究了一种简单但难以维持的方法。</span><span class="sxs-lookup"><span data-stu-id="e5169-187">First, we examined a simple, but difficult to maintain approach.</span></span> <span data-ttu-id="e5169-188">在第一部分中，我们讨论了如何在应用程序中的每个控制器操作中为视图母版页添加视图数据。</span><span class="sxs-lookup"><span data-stu-id="e5169-188">In the first section, we discussed how you can add view data for a view master page in each every controller action in your application.</span></span> <span data-ttu-id="e5169-189">我们的结论是，这是一个糟糕的方法，因为它违反了DRY（不要重复自己）的原则。</span><span class="sxs-lookup"><span data-stu-id="e5169-189">We concluded that this was a bad approach because it violates the DRY (Don't Repeat Yourself) principle.</span></span>

<span data-ttu-id="e5169-190">接下来，我们研究了添加视图母版页所需的数据以查看数据更好的策略。</span><span class="sxs-lookup"><span data-stu-id="e5169-190">Next, we examined a much better strategy for adding data required by a view master page to view data.</span></span> <span data-ttu-id="e5169-191">我们不是在每个控制器操作中添加视图数据，而是在应用程序控制器中只添加一次视图数据。</span><span class="sxs-lookup"><span data-stu-id="e5169-191">Instead of adding the view data in each and every controller action, we added the view data only once within an Application controller.</span></span> <span data-ttu-id="e5169-192">这样，当将数据传递到ASP.NET MVC 应用程序中的视图母版页时，可以避免重复的代码。</span><span class="sxs-lookup"><span data-stu-id="e5169-192">That way, you can avoid duplicate code when passing data to a view master page in an ASP.NET MVC application.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="e5169-193">上一篇</span><span class="sxs-lookup"><span data-stu-id="e5169-193">Previous</span></span>](creating-page-layouts-with-view-master-pages-vb.md)

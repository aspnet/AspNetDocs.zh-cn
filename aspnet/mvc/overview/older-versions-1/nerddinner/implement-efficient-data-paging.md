---
uid: mvc/overview/older-versions-1/nerddinner/implement-efficient-data-paging
title: 实现高效的数据分页 |微软文档
author: rick-anderson
description: 步骤 8 演示如何向 /Dinners URL 添加寻呼支持，以便我们一次不显示 1000 份晚餐，我们仅在...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: adea836d-dbc2-4005-94ea-53aef09e9e34
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/implement-efficient-data-paging
msc.type: authoredcontent
ms.openlocfilehash: a833553fe44b62b136f7eb55c7e00eca0b0462c6
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541320"
---
# <a name="implement-efficient-data-paging"></a><span data-ttu-id="37fdc-103">实现高效数据分页</span><span class="sxs-lookup"><span data-stu-id="37fdc-103">Implement Efficient Data Paging</span></span>

<span data-ttu-id="37fdc-104">由[微软](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="37fdc-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="37fdc-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="37fdc-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="37fdc-106">这是一个免费的["NerdDinner"应用程序教程](introducing-the-nerddinner-tutorial.md)的第8步，该教程演示如何使用ASP.NET MVC 1 构建小型但完整的 Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="37fdc-106">This is step 8 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="37fdc-107">步骤 8 演示如何向我们的 /Dinners URL 添加寻呼支持，以便我们一次只显示 10 份即将举办的晚餐，并且允许最终用户以 SEO 友好的方式回传整个列表。</span><span class="sxs-lookup"><span data-stu-id="37fdc-107">Step 8 shows how to add paging support to our /Dinners URL so that instead of displaying 1000s of dinners at once, we'll only display 10 upcoming dinners at a time - and allow end-users to page back and forward through the entire list in an SEO friendly way.</span></span>
> 
> <span data-ttu-id="37fdc-108">如果您使用的是ASP.NET MVC 3，我们建议您按照[MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC 音乐商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程进行操作。</span><span class="sxs-lookup"><span data-stu-id="37fdc-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-8-paging-support"></a><span data-ttu-id="37fdc-109">神经晚餐步骤 8： 寻呼支持</span><span class="sxs-lookup"><span data-stu-id="37fdc-109">NerdDinner Step 8: Paging Support</span></span>

<span data-ttu-id="37fdc-110">如果我们的网站成功，它将有成千上万的即将到来的晚餐。</span><span class="sxs-lookup"><span data-stu-id="37fdc-110">If our site is successful, it will have thousands of upcoming dinners.</span></span> <span data-ttu-id="37fdc-111">我们需要确保我们的 UI 扩展以处理所有这些晚餐，并允许用户浏览它们。</span><span class="sxs-lookup"><span data-stu-id="37fdc-111">We need to make sure that our UI scales to handle all of these dinners, and allows users to browse them.</span></span> <span data-ttu-id="37fdc-112">为了启用这一点，我们将添加分页支持到我们的 */Dinners* URL，以便我们不是一次显示 1000 份晚餐，而是一次只显示 10 份即将举办的晚餐 -并允许最终用户以 SEO 友好的方式回传和转发整个列表。</span><span class="sxs-lookup"><span data-stu-id="37fdc-112">To enable this, we'll add paging support to our */Dinners* URL so that instead of displaying 1000s of dinners at once, we'll only display 10 upcoming dinners at a time - and allow end-users to page back and forward through the entire list in an SEO friendly way.</span></span>

### <a name="index-action-method-recap"></a><span data-ttu-id="37fdc-113">索引（） 操作方法回顾</span><span class="sxs-lookup"><span data-stu-id="37fdc-113">Index() Action Method Recap</span></span>

<span data-ttu-id="37fdc-114">我们的 DinnersController 类中的 Index（） 操作方法当前如下所示：</span><span class="sxs-lookup"><span data-stu-id="37fdc-114">The Index() action method within our DinnersController class currently looks like below:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample1.cs)]

<span data-ttu-id="37fdc-115">当对 */Dinners* URL 发出请求时，它会检索所有即将举办的晚宴的列表，然后呈现所有这些晚宴的列表：</span><span class="sxs-lookup"><span data-stu-id="37fdc-115">When a request is made to the */Dinners* URL, it retrieves a list of all upcoming dinners and then renders a listing of all of them out:</span></span>

![](implement-efficient-data-paging/_static/image1.png)

### <a name="understanding-iqueryablelttgt"></a><span data-ttu-id="37fdc-116">了解可&lt;查询 T&gt;</span><span class="sxs-lookup"><span data-stu-id="37fdc-116">Understanding IQueryable&lt;T&gt;</span></span>

<span data-ttu-id="37fdc-117">*IQuery&lt;T&gt;* 是 LINQ 作为 .NET 3.5 的一部分引入的接口。</span><span class="sxs-lookup"><span data-stu-id="37fdc-117">*IQueryable&lt;T&gt;* is an interface that was introduced with LINQ as part of .NET 3.5.</span></span> <span data-ttu-id="37fdc-118">它支持强大的"延迟执行"方案，我们可以利用这些场景来实现分页支持。</span><span class="sxs-lookup"><span data-stu-id="37fdc-118">It enables powerful "deferred execution" scenarios that we can take advantage of to implement paging support.</span></span>

<span data-ttu-id="37fdc-119">在我们的晚餐存储库中，我们将从我们的"查找晚餐&lt;"&gt;方法返回一个可查询的晚餐序列：</span><span class="sxs-lookup"><span data-stu-id="37fdc-119">In our DinnerRepository we are returning an IQueryable&lt;Dinner&gt; sequence from our FindUpcomingDinners() method:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample2.cs)]

<span data-ttu-id="37fdc-120">我们的 Find对&lt;托&gt;晚餐（） 方法返回的 I 可查询晚餐对象封装了一个查询，以便使用 LINQ 从我们的数据库中检索 Dinner 对象，使用 LINQ 到 SQL。</span><span class="sxs-lookup"><span data-stu-id="37fdc-120">The IQueryable&lt;Dinner&gt; object returned by our FindUpcomingDinners() method encapsulates a query to retrieve Dinner objects from our database using LINQ to SQL.</span></span> <span data-ttu-id="37fdc-121">重要的是，在我们尝试访问/迭代查询中的数据之前，或者直到我们调用查询上的 ToList（） 方法之前，它不会对数据库执行查询。</span><span class="sxs-lookup"><span data-stu-id="37fdc-121">Importantly, it won't execute the query against the database until we attempt to access/iterate over the data in the query, or until we call the ToList() method on it.</span></span> <span data-ttu-id="37fdc-122">调用我们的 Find对兴晚餐（） 方法的代码可以选择在执行查询之前向 IQuery&lt;Dinner&gt;对象添加其他"链接"操作/筛选器。</span><span class="sxs-lookup"><span data-stu-id="37fdc-122">The code calling our FindUpcomingDinners() method can optionally choose to add additional "chained" operations/filters to the IQueryable&lt;Dinner&gt; object before executing the query.</span></span> <span data-ttu-id="37fdc-123">然后，LINQ 到 SQL 足够智能，在请求数据时对数据库执行组合查询。</span><span class="sxs-lookup"><span data-stu-id="37fdc-123">LINQ to SQL is then smart enough to execute the combined query against the database when the data is requested.</span></span>

<span data-ttu-id="37fdc-124">为了实现分页逻辑，我们可以更新我们的 DinnersController Index（） 操作方法，以便它在调用 ToList（） 之前，将其他"跳过"和"&lt;获取&gt;"运算符应用于返回的可查询晚餐序列：</span><span class="sxs-lookup"><span data-stu-id="37fdc-124">To implement paging logic we can update our DinnersController's Index() action method so that it applies additional "Skip" and "Take" operators to the returned IQueryable&lt;Dinner&gt; sequence before calling ToList() on it:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample3.cs)]

<span data-ttu-id="37fdc-125">上述代码跳过数据库中即将进行的 10 份晚餐，然后返回 20 份晚餐。</span><span class="sxs-lookup"><span data-stu-id="37fdc-125">The above code skips over the first 10 upcoming dinners in the database, and then returns back 20 dinners.</span></span> <span data-ttu-id="37fdc-126">LINQ 到 SQL 足够智能，可以构造优化的 SQL 查询，该查询在 SQL 数据库中执行此跳过逻辑，而不是在 Web 服务器中执行此跳过逻辑。</span><span class="sxs-lookup"><span data-stu-id="37fdc-126">LINQ to SQL is smart enough to construct an optimized SQL query that performs this skipping logic in the SQL database – and not in the web-server.</span></span> <span data-ttu-id="37fdc-127">这意味着，即使我们数据库中有数百万个即将推出的 Dinner，也只能检索我们想要的 10 个，作为此请求的一部分（使其高效且可扩展）。</span><span class="sxs-lookup"><span data-stu-id="37fdc-127">This means that even if we have millions of upcoming Dinners in the database, only the 10 we want will be retrieved as part of this request (making it efficient and scalable).</span></span>

### <a name="adding-a-page-value-to-the-url"></a><span data-ttu-id="37fdc-128">向 URL 添加"页面"值</span><span class="sxs-lookup"><span data-stu-id="37fdc-128">Adding a "page" value to the URL</span></span>

<span data-ttu-id="37fdc-129">我们希望我们的 URL 包含一个"页面"参数，指示用户请求的"晚餐范围"，而不是对特定页面范围进行硬编码。</span><span class="sxs-lookup"><span data-stu-id="37fdc-129">Instead of hard-coding a specific page range, we'll want our URLs to include a "page" parameter that indicates which Dinner range a user is requesting.</span></span>

#### <a name="using-a-querystring-value"></a><span data-ttu-id="37fdc-130">使用查询字符串值</span><span class="sxs-lookup"><span data-stu-id="37fdc-130">Using a Querystring value</span></span>

<span data-ttu-id="37fdc-131">下面的代码演示如何更新我们的 Index（） 操作方法以支持查询字符串参数，并启用 URL，如 */Dinners？page_2*：</span><span class="sxs-lookup"><span data-stu-id="37fdc-131">The code below demonstrates how we can update our Index() action method to support a querystring parameter and enable URLs like */Dinners?page=2*:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample4.cs)]

<span data-ttu-id="37fdc-132">上面的 Index（） 操作方法具有名为"页"的参数。</span><span class="sxs-lookup"><span data-stu-id="37fdc-132">The Index() action method above has a parameter named "page".</span></span> <span data-ttu-id="37fdc-133">参数声明为空整数（即 int？ 指示）。</span><span class="sxs-lookup"><span data-stu-id="37fdc-133">The parameter is declared as a nullable integer (that is what int? indicates).</span></span> <span data-ttu-id="37fdc-134">这意味着 */Dinners？page_2* URL 将导致将值"2"作为参数值传递。</span><span class="sxs-lookup"><span data-stu-id="37fdc-134">This means that the */Dinners?page=2* URL will cause a value of "2" to be passed as the parameter value.</span></span> <span data-ttu-id="37fdc-135">*/Dinners* URL（没有查询字符串值）将导致传递空值。</span><span class="sxs-lookup"><span data-stu-id="37fdc-135">The */Dinners* URL (without a querystring value) will cause a null value to be passed.</span></span>

<span data-ttu-id="37fdc-136">我们将页面值乘以页面大小（本例中为 10 行），以确定要跳过的晚餐数。</span><span class="sxs-lookup"><span data-stu-id="37fdc-136">We are multiplying the page value by the page size (in this case 10 rows) to determine how many dinners to skip over.</span></span> <span data-ttu-id="37fdc-137">我们使用[C# null"合并"运算符 （？），](https://weblogs.asp.net/scottgu/archive/2007/09/20/the-new-c-null-coalescing-operator-and-using-it-with-linq.aspx)在处理可无类型时非常有用。</span><span class="sxs-lookup"><span data-stu-id="37fdc-137">We are using the [C# null "coalescing" operator (??)](https://weblogs.asp.net/scottgu/archive/2007/09/20/the-new-c-null-coalescing-operator-and-using-it-with-linq.aspx) which is useful when dealing with nullable types.</span></span> <span data-ttu-id="37fdc-138">如果页面参数为空，上述代码将值为 0 分配给页。</span><span class="sxs-lookup"><span data-stu-id="37fdc-138">The code above assigns page the value of 0 if the page parameter is null.</span></span>

#### <a name="using-embedded-url-values"></a><span data-ttu-id="37fdc-139">使用嵌入式 URL 值</span><span class="sxs-lookup"><span data-stu-id="37fdc-139">Using Embedded URL values</span></span>

<span data-ttu-id="37fdc-140">使用查询字符串值的替代方法是将页面参数嵌入到实际 URL 本身中。</span><span class="sxs-lookup"><span data-stu-id="37fdc-140">An alternative to using a querystring value would be to embed the page parameter within the actual URL itself.</span></span> <span data-ttu-id="37fdc-141">例如 *：/晚餐/页/2*或 */Dinner/2*。</span><span class="sxs-lookup"><span data-stu-id="37fdc-141">For example: */Dinners/Page/2* or */Dinners/2*.</span></span> <span data-ttu-id="37fdc-142">ASP.NET MVC 包含强大的 URL 路由引擎，便于支持类似方案。</span><span class="sxs-lookup"><span data-stu-id="37fdc-142">ASP.NET MVC includes a powerful URL routing engine that makes it easy to support scenarios like this.</span></span>

<span data-ttu-id="37fdc-143">我们可以注册自定义路由规则，将任何传入 URL 或 URL 格式映射到所需的任何控制器类或操作方法。</span><span class="sxs-lookup"><span data-stu-id="37fdc-143">We can register custom routing rules that map any incoming URL or URL format to any controller class or action method we want.</span></span> <span data-ttu-id="37fdc-144">我们只需要在我们的项目中打开 Global.asax 文件：</span><span class="sxs-lookup"><span data-stu-id="37fdc-144">All we need to-do is to open the Global.asax file within our project:</span></span>

![](implement-efficient-data-paging/_static/image2.png)

<span data-ttu-id="37fdc-145">然后使用 MapRoute（） 帮助器方法注册新的映射规则，如对路由的第一次调用。地图路线（） 如下：</span><span class="sxs-lookup"><span data-stu-id="37fdc-145">And then register a new mapping rule using the MapRoute() helper method like the first call to routes.MapRoute() below:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample5.cs)]

<span data-ttu-id="37fdc-146">上图，我们正在注册一个名为"即将推出的晚餐"的新路由规则。</span><span class="sxs-lookup"><span data-stu-id="37fdc-146">Above we are registering a new routing rule named "UpcomingDinners".</span></span> <span data-ttu-id="37fdc-147">我们指示它有 URL 格式"Dinners/page/{页面}" - 其中 [页面] 是嵌入在 URL 中的参数值。</span><span class="sxs-lookup"><span data-stu-id="37fdc-147">We are indicating it has the URL format "Dinners/Page/{page}" – where {page} is a parameter value embedded within the URL.</span></span> <span data-ttu-id="37fdc-148">MapRoute（） 方法的第三个参数指示我们应该映射此格式与 DinnersController 类上的 Index（） 操作方法相匹配的 URL。</span><span class="sxs-lookup"><span data-stu-id="37fdc-148">The third parameter to the MapRoute() method indicates that we should map URLs that match this format to the Index() action method on the DinnersController class.</span></span>

<span data-ttu-id="37fdc-149">我们可以在查询字符串方案中使用我们以前完全相同的 Index（） 代码 ，除非现在我们的"页面"参数将来自 URL 而不是查询字符串：</span><span class="sxs-lookup"><span data-stu-id="37fdc-149">We can use the exact same Index() code we had before with our Querystring scenario – except now our "page" parameter will come from the URL and not the querystring:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample6.cs)]

<span data-ttu-id="37fdc-150">现在，当我们运行应用程序并输入 */Dinner 时*，我们将看到前 10 场即将举办的晚宴：</span><span class="sxs-lookup"><span data-stu-id="37fdc-150">And now when we run the application and type in */Dinners* we'll see the first 10 upcoming dinners:</span></span>

![](implement-efficient-data-paging/_static/image3.png)

<span data-ttu-id="37fdc-151">当我们输入 */Dinner/Page/1*时，我们将看到晚餐的下一页：</span><span class="sxs-lookup"><span data-stu-id="37fdc-151">And when we type in */Dinners/Page/1* we'll see the next page of dinners:</span></span>

![](implement-efficient-data-paging/_static/image4.png)

### <a name="adding-page-navigation-ui"></a><span data-ttu-id="37fdc-152">添加页面导航 UI</span><span class="sxs-lookup"><span data-stu-id="37fdc-152">Adding page navigation UI</span></span>

<span data-ttu-id="37fdc-153">完成寻呼方案的最后一步是在我们的视图模板中实现"下一步"和"上一个"导航 UI，以便用户轻松跳过 Dinner 数据。</span><span class="sxs-lookup"><span data-stu-id="37fdc-153">The last step to complete our paging scenario will be to implement "next" and "previous" navigation UI within our view template to enable users to easily skip over the Dinner data.</span></span>

<span data-ttu-id="37fdc-154">要正确实现这一点，我们需要知道数据库中的 Dinner 的总数，以及它转换为的数据页数。</span><span class="sxs-lookup"><span data-stu-id="37fdc-154">To implement this correctly, we'll need to know the total number of Dinners in the database, as well as how many pages of data this translates to.</span></span> <span data-ttu-id="37fdc-155">然后，我们需要计算当前请求的"页面"值是在数据开头还是结尾，并相应地显示或隐藏"上一个"和"下一个"UI。</span><span class="sxs-lookup"><span data-stu-id="37fdc-155">We'll then need to calculate whether the currently requested "page" value is at the beginning or end of the data, and show or hide the "previous" and "next" UI accordingly.</span></span> <span data-ttu-id="37fdc-156">我们可以在 Index（） 操作方法中实现此逻辑。</span><span class="sxs-lookup"><span data-stu-id="37fdc-156">We could implement this logic within our Index() action method.</span></span> <span data-ttu-id="37fdc-157">或者，我们可以向项目添加帮助器类，以更可重用的方式封装此逻辑。</span><span class="sxs-lookup"><span data-stu-id="37fdc-157">Alternatively we can add a helper class to our project that encapsulates this logic in a more re-usable way.</span></span>

<span data-ttu-id="37fdc-158">下面是一个简单的"分页列表"帮助器类，派生自内置于 .NET&lt;&gt;框架中的列表 T 集合类。</span><span class="sxs-lookup"><span data-stu-id="37fdc-158">Below is a simple "PaginatedList" helper class that derives from the List&lt;T&gt; collection class built-into the .NET Framework.</span></span> <span data-ttu-id="37fdc-159">它实现了一个可重用的集合类，可用于分页任何 IQuery 数据序列。</span><span class="sxs-lookup"><span data-stu-id="37fdc-159">It implements a re-usable collection class that can be used to paginate any sequence of IQueryable data.</span></span> <span data-ttu-id="37fdc-160">在我们的 NerdDinner&lt;应用程序中，我们将针对 IQuery Dinner&gt;结果进行工作，但它在其他应用程序方案中可以同样轻松地用于 I可&lt;查询&gt;产品或可&lt;查询客户&gt;结果：</span><span class="sxs-lookup"><span data-stu-id="37fdc-160">In our NerdDinner application we'll have it work over IQueryable&lt;Dinner&gt; results, but it could just as easily be used against IQueryable&lt;Product&gt; or IQueryable&lt;Customer&gt; results in other application scenarios:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample7.cs)]

<span data-ttu-id="37fdc-161">请注意，它如何计算，然后公开属性，如"页面索引"，"页面大小"，"总计数"和"总页"。</span><span class="sxs-lookup"><span data-stu-id="37fdc-161">Notice above how it calculates and then exposes properties like "PageIndex", "PageSize", "TotalCount", and "TotalPages".</span></span> <span data-ttu-id="37fdc-162">然后，它还公开两个帮助属性"Has上页"和"HasNextPage"，指示集合中的数据页是原始序列的开头还是结尾。</span><span class="sxs-lookup"><span data-stu-id="37fdc-162">It also then exposes two helper properties "HasPreviousPage" and "HasNextPage" that indicate whether the page of data in the collection is at the beginning or end of the original sequence.</span></span> <span data-ttu-id="37fdc-163">上述代码将导致运行两个 SQL 查询 - 第一个查询检索 Dinner 对象总数的计数（这不会返回对象- 而是执行返回整数的"SELECT COUNT"语句），第二个代码将仅从数据库中检索当前数据页所需的数据行。</span><span class="sxs-lookup"><span data-stu-id="37fdc-163">The above code will cause two SQL queries to be run - the first to retrieve the count of the total number of Dinner objects (this doesn't return the objects – rather it performs a "SELECT COUNT" statement that returns an integer), and the second to retrieve just the rows of data we need from our database for the current page of data.</span></span>

<span data-ttu-id="37fdc-164">然后，我们可以更新我们的晚餐控制器.Index（） 帮助方法，从我们的晚餐存储库创建一个&lt;&gt; PaginatedList 晚餐。</span><span class="sxs-lookup"><span data-stu-id="37fdc-164">We can then update our DinnersController.Index() helper method to create a PaginatedList&lt;Dinner&gt; from our DinnerRepository.FindUpcomingDinners() result, and pass it to our view template:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample8.cs)]

<span data-ttu-id="37fdc-165">然后，我们可以更新 [Views_Dinners_Index.aspx 视图模板》，以便从&lt;ViewPage NerdDinner.Helpers.PaginatedList&lt;&gt;&gt;晚餐&lt;而不是 ViewPage&lt;&gt;&gt;IE500s 晚宴上继承，然后将以下代码添加到视图模板的底部，以显示或隐藏下一个和以前的导航 UI：</span><span class="sxs-lookup"><span data-stu-id="37fdc-165">We can then update the \Views\Dinners\Index.aspx view template to inherit from ViewPage&lt;NerdDinner.Helpers.PaginatedList&lt;Dinner&gt;&gt; instead of ViewPage&lt;IEnumerable&lt;Dinner&gt;&gt;, and then add the following code to the bottom of our view-template to show or hide next and previous navigation UI:</span></span>

[!code-aspx[Main](implement-efficient-data-paging/samples/sample9.aspx)]

<span data-ttu-id="37fdc-166">请注意，我们使用 Html.RouteLink（） 帮助器方法生成超链接的方式。</span><span class="sxs-lookup"><span data-stu-id="37fdc-166">Notice above how we are using the Html.RouteLink() helper method to generate our hyperlinks.</span></span> <span data-ttu-id="37fdc-167">此方法类似于我们以前使用过的 Html.ActionLink（） 帮助程序方法。</span><span class="sxs-lookup"><span data-stu-id="37fdc-167">This method is similar to the Html.ActionLink() helper method we've used previously.</span></span> <span data-ttu-id="37fdc-168">区别在于，我们使用在 Global.asax 文件中设置的"即将到达的晚餐"路由规则生成 URL。</span><span class="sxs-lookup"><span data-stu-id="37fdc-168">The difference is that we are generating the URL using the "UpcomingDinners" routing rule we setup within our Global.asax file.</span></span> <span data-ttu-id="37fdc-169">这可确保我们将生成索引（） 操作方法的 URL，该方法的格式为 *：/Dinners/page/{page}* - 其中 [page] 值是我们基于当前 PageIndex 提供上述变量。</span><span class="sxs-lookup"><span data-stu-id="37fdc-169">This ensures that we'll generate URLs to our Index() action method that have the format: */Dinners/Page/{page}* – where the {page} value is a variable we are providing above based on the current PageIndex.</span></span>

<span data-ttu-id="37fdc-170">现在，当我们再次运行应用程序时，我们将在浏览器中一次看到 10 份晚餐：</span><span class="sxs-lookup"><span data-stu-id="37fdc-170">And now when we run our application again we'll see 10 dinners at a time in our browser:</span></span>

![](implement-efficient-data-paging/_static/image5.png)

<span data-ttu-id="37fdc-171">我们还在页面&lt;&lt;&lt;底部&gt;&gt;&gt;具有和导航 UI，允许我们使用搜索引擎可访问的 URL 向前和向后跳过数据：</span><span class="sxs-lookup"><span data-stu-id="37fdc-171">We also have &lt;&lt;&lt; and &gt;&gt;&gt; navigation UI at the bottom of the page that allows us to skip forwards and backwards over our data using search engine accessible URLs:</span></span>

![](implement-efficient-data-paging/_static/image6.png)

| <span data-ttu-id="37fdc-172">**侧主题：了解可&lt;查询 T 的含义&gt;**</span><span class="sxs-lookup"><span data-stu-id="37fdc-172">**Side Topic: Understanding the implications of IQueryable&lt;T&gt;**</span></span> |
| --- |
| <span data-ttu-id="37fdc-173">IQueryable&lt;&gt; T 是一个非常强大的功能，支持各种有趣的延迟执行方案（如分页和基于合成的查询）。</span><span class="sxs-lookup"><span data-stu-id="37fdc-173">IQueryable&lt;T&gt; is a very powerful feature that enables a variety of interesting deferred execution scenarios (like paging and composition based queries).</span></span> <span data-ttu-id="37fdc-174">与所有强大的功能一样，您希望小心如何使用它，并确保它不受滥用。</span><span class="sxs-lookup"><span data-stu-id="37fdc-174">As with all powerful features, you want to be careful with how you use it and make sure it is not abused.</span></span> <span data-ttu-id="37fdc-175">请务必认识到，从存储库返回 IQuery 可&lt;查询&gt;T 结果可以调用代码来追加到它上的链式运算符方法，从而参与最终查询执行。</span><span class="sxs-lookup"><span data-stu-id="37fdc-175">It is important to recognize that returning an IQueryable&lt;T&gt; result from your repository enables calling code to append on chained operator methods to it, and so participate in the ultimate query execution.</span></span> <span data-ttu-id="37fdc-176">如果不想提供此能力的调用代码，则应&lt;返回 IList T&gt;或 IE55ble&lt;T&gt;结果 - 其中包含已执行的查询的结果。</span><span class="sxs-lookup"><span data-stu-id="37fdc-176">If you do not want to provide calling code this ability, then you should return back IList&lt;T&gt; or IEnumerable&lt;T&gt; results - which contain the results of a query that has already executed.</span></span> <span data-ttu-id="37fdc-177">对于分页方案，这将要求您将实际数据暂停逻辑推送到被调用的存储库方法中。</span><span class="sxs-lookup"><span data-stu-id="37fdc-177">For pagination scenarios this would require you to push the actual data pagination logic into the repository method being called.</span></span> <span data-ttu-id="37fdc-178">在此方案中，我们可能会更新我们的 Find对价晚餐（） 查找方法，以有一个签名，该签名要么返回一个分页列表&lt;&gt;：paginatedList 晚餐查找要约晚餐（int pageIndex，int page_info=2>）=或&lt;返回 IList 晚餐&gt;，并使用"总计数"外参数返回晚餐的&lt;总数&gt;：Ilist 晚餐查找要约晚餐（int 页索引，int 页大小）</span><span class="sxs-lookup"><span data-stu-id="37fdc-178">In this scenario we might update our FindUpcomingDinners() finder method to have a signature that either returned a PaginatedList: PaginatedList&lt; Dinner&gt; FindUpcomingDinners(int pageIndex, int pageSize) { } Or return back an IList&lt;Dinner&gt;, and use a "totalCount" out param to return the total count of Dinners: IList&lt;Dinner&gt; FindUpcomingDinners(int pageIndex, int pageSize, out int totalCount) { }</span></span> |

### <a name="next-step"></a><span data-ttu-id="37fdc-179">下一步</span><span class="sxs-lookup"><span data-stu-id="37fdc-179">Next Step</span></span>

<span data-ttu-id="37fdc-180">现在，让我们来看看如何向应用程序添加身份验证和授权支持。</span><span class="sxs-lookup"><span data-stu-id="37fdc-180">Let's now look at how we can add authentication and authorization support to our application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="37fdc-181">[上一页](re-use-ui-using-master-pages-and-partials.md)
> [下一页](secure-applications-using-authentication-and-authorization.md)</span><span class="sxs-lookup"><span data-stu-id="37fdc-181">[Previous](re-use-ui-using-master-pages-and-partials.md)
[Next](secure-applications-using-authentication-and-authorization.md)</span></span>

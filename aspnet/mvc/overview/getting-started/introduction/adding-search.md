---
uid: mvc/overview/getting-started/introduction/adding-search
title: 搜索 |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/17/2019
ms.assetid: df001954-18bf-4550-b03d-43911a0ea186
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-search
msc.type: authoredcontent
ms.openlocfilehash: f6d6d32a648fed453be924790a1b55698c9cf209
ms.sourcegitcommit: 0d583ed9253103f3e50b6d729276e667591cdd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/10/2020
ms.locfileid: "86211472"
---
# <a name="search"></a><span data-ttu-id="82929-102">搜索</span><span class="sxs-lookup"><span data-stu-id="82929-102">Search</span></span>

[!INCLUDE [Tutorial Note](index.md)]

## <a name="adding-a-search-method-and-search-view"></a><span data-ttu-id="82929-103">添加搜索方法和搜索视图</span><span class="sxs-lookup"><span data-stu-id="82929-103">Adding a Search Method and Search View</span></span>

<span data-ttu-id="82929-104">在本部分中，你将向操作方法添加搜索功能 `Index` ，以允许你按流派或名称搜索电影。</span><span class="sxs-lookup"><span data-stu-id="82929-104">In this section you'll add search capability to the `Index` action method that lets you search movies by genre or name.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="82929-105">必备条件</span><span class="sxs-lookup"><span data-stu-id="82929-105">Prerequisites</span></span>

<span data-ttu-id="82929-106">若要匹配此部分的屏幕截图，需要运行应用程序 (F5) 并将以下电影添加到数据库中。</span><span class="sxs-lookup"><span data-stu-id="82929-106">To match this section's screenshots, you need to run the application (F5) and add the following movies to the database.</span></span>

| <span data-ttu-id="82929-107">标题</span><span class="sxs-lookup"><span data-stu-id="82929-107">Title</span></span> | <span data-ttu-id="82929-108">发布日期</span><span class="sxs-lookup"><span data-stu-id="82929-108">Release Date</span></span> | <span data-ttu-id="82929-109">流派</span><span class="sxs-lookup"><span data-stu-id="82929-109">Genre</span></span> | <span data-ttu-id="82929-110">价格</span><span class="sxs-lookup"><span data-stu-id="82929-110">Price</span></span> |
| ----- | ------------ | ----- | ----- |
| <span data-ttu-id="82929-111">Ghostbusters</span><span class="sxs-lookup"><span data-stu-id="82929-111">Ghostbusters</span></span> | <span data-ttu-id="82929-112">6/8/1984</span><span class="sxs-lookup"><span data-stu-id="82929-112">6/8/1984</span></span> | <span data-ttu-id="82929-113">喜剧</span><span class="sxs-lookup"><span data-stu-id="82929-113">Comedy</span></span> | <span data-ttu-id="82929-114">6.99</span><span class="sxs-lookup"><span data-stu-id="82929-114">6.99</span></span> |
| <span data-ttu-id="82929-115">Ghostbusters II</span><span class="sxs-lookup"><span data-stu-id="82929-115">Ghostbusters II</span></span> | <span data-ttu-id="82929-116">6/16/1989</span><span class="sxs-lookup"><span data-stu-id="82929-116">6/16/1989</span></span> | <span data-ttu-id="82929-117">喜剧</span><span class="sxs-lookup"><span data-stu-id="82929-117">Comedy</span></span> | <span data-ttu-id="82929-118">6.99</span><span class="sxs-lookup"><span data-stu-id="82929-118">6.99</span></span> |
| <span data-ttu-id="82929-119">Apes 的世界</span><span class="sxs-lookup"><span data-stu-id="82929-119">Planet of the Apes</span></span> | <span data-ttu-id="82929-120">3/27/1986</span><span class="sxs-lookup"><span data-stu-id="82929-120">3/27/1986</span></span> | <span data-ttu-id="82929-121">操作</span><span class="sxs-lookup"><span data-stu-id="82929-121">Action</span></span> | <span data-ttu-id="82929-122">5.99</span><span class="sxs-lookup"><span data-stu-id="82929-122">5.99</span></span> |

## <a name="updating-the-index-form"></a><span data-ttu-id="82929-123">更新索引窗体</span><span class="sxs-lookup"><span data-stu-id="82929-123">Updating the Index Form</span></span>

<span data-ttu-id="82929-124">首先将 `Index` 操作方法更新到现有 `MoviesController` 类。</span><span class="sxs-lookup"><span data-stu-id="82929-124">Start by updating the `Index` action method to the existing `MoviesController` class.</span></span> <span data-ttu-id="82929-125">代码如下：</span><span class="sxs-lookup"><span data-stu-id="82929-125">Here's the code:</span></span>

[!code-csharp[Main](adding-search/samples/sample1.cs?highlight=1,6-9)]

<span data-ttu-id="82929-126">方法的第一行 `Index` 创建以下[LINQ](https://msdn.microsoft.com/library/bb397926.aspx)查询来选择电影：</span><span class="sxs-lookup"><span data-stu-id="82929-126">The first line of the `Index` method creates the following [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) query to select the movies:</span></span>

[!code-csharp[Main](adding-search/samples/sample2.cs)]

<span data-ttu-id="82929-127">此时将定义该查询，但尚未对该数据库运行该查询。</span><span class="sxs-lookup"><span data-stu-id="82929-127">The query is defined at this point, but hasn't yet been run against the database.</span></span>

<span data-ttu-id="82929-128">如果 `searchString` 参数包含一个字符串，则使用以下代码修改电影查询以筛选搜索字符串的值：</span><span class="sxs-lookup"><span data-stu-id="82929-128">If the `searchString` parameter contains a string, the movies query is modified to filter on the value of the search string, using the following code:</span></span>

[!code-csharp[Main](adding-search/samples/sample3.cs)]

<span data-ttu-id="82929-129">上面的 `s => s.Title` 代码是 [Lambda 表达式](https://msdn.microsoft.com/library/bb397687.aspx)。</span><span class="sxs-lookup"><span data-stu-id="82929-129">The `s => s.Title` code above is a [Lambda Expression](https://msdn.microsoft.com/library/bb397687.aspx).</span></span> <span data-ttu-id="82929-130">Lambda 在基于方法的[LINQ](https://msdn.microsoft.com/library/bb397926.aspx)查询中用作标准查询运算符方法的参数，如以上代码中使用的[Where](https://msdn.microsoft.com/library/system.linq.enumerable.where.aspx)方法。</span><span class="sxs-lookup"><span data-stu-id="82929-130">Lambdas are used in method-based [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) queries as arguments to standard query operator methods such as the [Where](https://msdn.microsoft.com/library/system.linq.enumerable.where.aspx) method used in the above code.</span></span> <span data-ttu-id="82929-131">LINQ 查询在定义或通过调用方法（如或）进行修改时，不会执行 `Where` `OrderBy` 。</span><span class="sxs-lookup"><span data-stu-id="82929-131">LINQ queries are not executed when they are defined or when they are modified by calling a method such as `Where` or `OrderBy`.</span></span> <span data-ttu-id="82929-132">相反，查询执行延迟，这意味着表达式的计算会延迟，直到实际循环访问它的实际值或 [`ToList`](https://msdn.microsoft.com/library/bb342261.aspx) 调用方法。</span><span class="sxs-lookup"><span data-stu-id="82929-132">Instead, query execution is deferred, which means that the evaluation of an expression is delayed until its realized value is actually iterated over or the [`ToList`](https://msdn.microsoft.com/library/bb342261.aspx) method is called.</span></span> <span data-ttu-id="82929-133">在此 `Search` 示例中，将在 "*索引*" 视图中执行查询。</span><span class="sxs-lookup"><span data-stu-id="82929-133">In the `Search` sample, the query is executed in the *Index.cshtml* view.</span></span> <span data-ttu-id="82929-134">有关延迟执行查询的详细信息，请参阅[Query Execution](https://msdn.microsoft.com/library/bb738633.aspx)（查询执行）。</span><span class="sxs-lookup"><span data-stu-id="82929-134">For more information about deferred query execution, see [Query Execution](https://msdn.microsoft.com/library/bb738633.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="82929-135">[Contains](https://msdn.microsoft.com/library/bb155125.aspx)方法在数据库上运行，而不是上面的 c # 代码。</span><span class="sxs-lookup"><span data-stu-id="82929-135">The [Contains](https://msdn.microsoft.com/library/bb155125.aspx) method is run on the database, not the c# code above.</span></span> <span data-ttu-id="82929-136">在数据库上，[包含](https://msdn.microsoft.com/library/bb155125.aspx)映射到[SQL LIKE](https://msdn.microsoft.com/library/ms179859.aspx)，这是不区分大小写的。</span><span class="sxs-lookup"><span data-stu-id="82929-136">On the database, [Contains](https://msdn.microsoft.com/library/bb155125.aspx) maps to [SQL LIKE](https://msdn.microsoft.com/library/ms179859.aspx), which is case insensitive.</span></span>

<span data-ttu-id="82929-137">现在可以更新 `Index` 将向用户显示窗体的视图。</span><span class="sxs-lookup"><span data-stu-id="82929-137">Now you can update the `Index` view that will display the form to the user.</span></span>

<span data-ttu-id="82929-138">运行应用程序并导航到 */Movies/Index*。</span><span class="sxs-lookup"><span data-stu-id="82929-138">Run the application and navigate to */Movies/Index*.</span></span> <span data-ttu-id="82929-139">将查询字符串（如 `?searchString=ghost`）追加到 URL。</span><span class="sxs-lookup"><span data-stu-id="82929-139">Append a query string such as `?searchString=ghost` to the URL.</span></span> <span data-ttu-id="82929-140">筛选的电影将显示出来。</span><span class="sxs-lookup"><span data-stu-id="82929-140">The filtered movies are displayed.</span></span>

![SearchQryStr](adding-search/_static/image1.png)

<span data-ttu-id="82929-142">如果将方法的签名更改 `Index` 为具有一个名为的参数 `id` ，则该 `id` 参数将与 `{id}` *应用 \_ Start\RouteConfig.cs*文件中设置的默认路由的占位符匹配。</span><span class="sxs-lookup"><span data-stu-id="82929-142">If you change the signature of the `Index` method to have a parameter named `id`, the `id` parameter will match the `{id}` placeholder for the default routes set in the *App\_Start\RouteConfig.cs* file.</span></span>

[!code-json[Main](adding-search/samples/sample4.json)]

<span data-ttu-id="82929-143">原始方法如下所 `Index` 示：</span><span class="sxs-lookup"><span data-stu-id="82929-143">The original `Index` method looks like this::</span></span>

[!code-csharp[Main](adding-search/samples/sample5.cs)]

<span data-ttu-id="82929-144">修改后的 `Index` 方法如下所示：</span><span class="sxs-lookup"><span data-stu-id="82929-144">The modified `Index` method would look as follows:</span></span>

[!code-csharp[Main](adding-search/samples/sample6.cs?highlight=1,3)]

<span data-ttu-id="82929-145">现可将搜索标题作为路由数据（ URL 段）而非查询字符串值进行传递。</span><span class="sxs-lookup"><span data-stu-id="82929-145">You can now pass the search title as route data (a URL segment) instead of as a query string value.</span></span>

![](adding-search/_static/image2.png)

<span data-ttu-id="82929-146">但是，不能指望用户在每次要搜索电影时都修改 URL。</span><span class="sxs-lookup"><span data-stu-id="82929-146">However, you can't expect users to modify the URL every time they want to search for a movie.</span></span> <span data-ttu-id="82929-147">因此需要添加 UI 来帮助他们筛选电影。</span><span class="sxs-lookup"><span data-stu-id="82929-147">So now you'll add UI to help them filter movies.</span></span> <span data-ttu-id="82929-148">如果更改了方法的签名 `Index` 以测试如何传递路由绑定 ID 参数，请将其更改回，使 `Index` 方法使用名为的字符串参数 `searchString` ：</span><span class="sxs-lookup"><span data-stu-id="82929-148">If you changed the signature of the `Index` method to test how to pass the route-bound ID parameter, change it back so that your `Index` method takes a string parameter named `searchString`:</span></span>

[!code-csharp[Main](adding-search/samples/sample7.cs)]

<span data-ttu-id="82929-149">打开*Views\Movies\Index.cshtml*文件，并在后面 `@Html.ActionLink("Create New", "Create")` 添加以下突出显示的窗体标记：</span><span class="sxs-lookup"><span data-stu-id="82929-149">Open the *Views\Movies\Index.cshtml* file, and just after `@Html.ActionLink("Create New", "Create")`, add the form markup highlighted below:</span></span>

[!code-cshtml[Main](adding-search/samples/sample8.cshtml?highlight=12-15)]

<span data-ttu-id="82929-150">`Html.BeginForm`帮助器创建开始 `<form>` 标记。</span><span class="sxs-lookup"><span data-stu-id="82929-150">The `Html.BeginForm` helper creates an opening `<form>` tag.</span></span> <span data-ttu-id="82929-151">`Html.BeginForm`当用户通过单击 "**筛选器**" 按钮提交窗体时，帮助器会使窗体发布到其自身。</span><span class="sxs-lookup"><span data-stu-id="82929-151">The `Html.BeginForm` helper causes the form to post to itself when the user submits the form by clicking the **Filter** button.</span></span>

<span data-ttu-id="82929-152">Visual Studio 2013 在显示和编辑视图文件时具有良好的改善。</span><span class="sxs-lookup"><span data-stu-id="82929-152">Visual Studio 2013 has a nice improvement when displaying and editing View files.</span></span> <span data-ttu-id="82929-153">当你运行应用程序时打开了一个视图文件，Visual Studio 2013 会调用正确的控制器操作方法来显示视图。</span><span class="sxs-lookup"><span data-stu-id="82929-153">When you run the application with a view file open, Visual Studio 2013 invokes the correct controller action method to display the view.</span></span>

![](adding-search/_static/image3.png)

<span data-ttu-id="82929-154">在 Visual Studio 中打开索引视图 (如上图) 中所示），点击 Ctr F5 或 F5 运行应用程序，然后尝试搜索电影。</span><span class="sxs-lookup"><span data-stu-id="82929-154">With the Index view open in Visual Studio (as shown in the image above), tap Ctr F5 or F5 to run the application and then try searching for a movie.</span></span>

![](adding-search/_static/image4.png)

<span data-ttu-id="82929-155">`HttpPost`方法没有重载 `Index` 。</span><span class="sxs-lookup"><span data-stu-id="82929-155">There's no `HttpPost` overload of the `Index` method.</span></span> <span data-ttu-id="82929-156">不需要该方法，因为该方法不会更改应用程序的状态，只是对数据进行筛选。</span><span class="sxs-lookup"><span data-stu-id="82929-156">You don't need it, because the method isn't changing the state of the application, just filtering data.</span></span>

<span data-ttu-id="82929-157">可添加以下 `HttpPost Index` 方法。</span><span class="sxs-lookup"><span data-stu-id="82929-157">You could add the following `HttpPost Index` method.</span></span> <span data-ttu-id="82929-158">在这种情况下，操作调用程序将与 `HttpPost Index` 方法匹配， `HttpPost Index` 方法将运行，如下图所示。</span><span class="sxs-lookup"><span data-stu-id="82929-158">In that case, the action invoker would match the `HttpPost Index` method, and the `HttpPost Index` method would run as shown in the image below.</span></span>

[!code-csharp[Main](adding-search/samples/sample9.cs)]

![SearchPostGhost](adding-search/_static/image5.png)

<span data-ttu-id="82929-160">但是，即使添加 `Index` 方法的 `HttpPost` 版本，其实现方式也受到限制。</span><span class="sxs-lookup"><span data-stu-id="82929-160">However, even if you add this `HttpPost` version of the `Index` method, there's a limitation in how this has all been implemented.</span></span> <span data-ttu-id="82929-161">假设你想要将特定搜索加入书签，或向朋友发送一个链接，让他们单击链接即可查看筛选出的相同电影列表。</span><span class="sxs-lookup"><span data-stu-id="82929-161">Imagine that you want to bookmark a particular search or you want to send a link to friends that they can click in order to see the same filtered list of movies.</span></span> <span data-ttu-id="82929-162">请注意，HTTP POST 请求的 URL 与 GET 请求的 URL (localhost： xxxxx/电影/索引) 相同--URL 本身中没有搜索信息。</span><span class="sxs-lookup"><span data-stu-id="82929-162">Notice that the URL for the HTTP POST request is the same as the URL for the GET request (localhost:xxxxx/Movies/Index) -- there's no search information in the URL itself.</span></span> <span data-ttu-id="82929-163">目前，搜索字符串信息将作为窗体字段值发送到服务器。</span><span class="sxs-lookup"><span data-stu-id="82929-163">Right now, the search string information is sent to the server as a form field value.</span></span> <span data-ttu-id="82929-164">这意味着你无法捕获该搜索信息以在 URL 中将其书签或发送给朋友。</span><span class="sxs-lookup"><span data-stu-id="82929-164">This means you can't capture that search information to bookmark or send to friends in a URL.</span></span>

<span data-ttu-id="82929-165">解决方案是使用 `BeginForm` 的重载，该重载指定 POST 请求应将搜索信息添加到 URL，并且应将其路由到该 `HttpGet` 方法的版本 `Index` 。</span><span class="sxs-lookup"><span data-stu-id="82929-165">The solution is to use an overload of `BeginForm` that specifies that the POST request should add the search information to the URL and that it should be routed to the `HttpGet` version of the `Index` method.</span></span> <span data-ttu-id="82929-166">将现有的无参数 `BeginForm` 方法替换为以下标记：</span><span class="sxs-lookup"><span data-stu-id="82929-166">Replace the existing parameterless `BeginForm` method with the following markup:</span></span>

[!code-cshtml[Main](adding-search/samples/sample10.cshtml)]

![BeginFormPost_SM](adding-search/_static/image6.png)

<span data-ttu-id="82929-168">现在，在提交搜索时，URL 包含搜索查询字符串。</span><span class="sxs-lookup"><span data-stu-id="82929-168">Now when you submit a search, the URL contains a search query string.</span></span> <span data-ttu-id="82929-169">即使具备 `HttpPost Index` 方法，搜索也将转到 `HttpGet Index` 操作方法。</span><span class="sxs-lookup"><span data-stu-id="82929-169">Searching will also go to the `HttpGet Index` action method, even if you have a `HttpPost Index` method.</span></span>

![IndexWithGetURL](adding-search/_static/image7.png)

## <a name="adding-search-by-genre"></a><span data-ttu-id="82929-171">按流派添加搜索</span><span class="sxs-lookup"><span data-stu-id="82929-171">Adding Search by Genre</span></span>

<span data-ttu-id="82929-172">如果已添加该 `HttpPost` 方法的版本 `Index` ，请立即将其删除。</span><span class="sxs-lookup"><span data-stu-id="82929-172">If you added the `HttpPost` version of the `Index` method, delete it now.</span></span>

<span data-ttu-id="82929-173">接下来，你将添加一项功能，使用户能够按流派搜索电影。</span><span class="sxs-lookup"><span data-stu-id="82929-173">Next, you'll add a feature to let users search for movies by genre.</span></span> <span data-ttu-id="82929-174">将 `Index` 方法替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="82929-174">Replace the `Index` method with the following code:</span></span>

[!code-csharp[Main](adding-search/samples/sample11.cs)]

<span data-ttu-id="82929-175">此版本的 `Index` 方法采用其他参数，即 `movieGenre` 。</span><span class="sxs-lookup"><span data-stu-id="82929-175">This version of the `Index` method takes an additional parameter, namely `movieGenre`.</span></span> <span data-ttu-id="82929-176">前几行代码创建一个 `List` 对象，用于保存数据库中的电影流派。</span><span class="sxs-lookup"><span data-stu-id="82929-176">The first few lines of code create a `List` object to hold movie genres from the database.</span></span>

<span data-ttu-id="82929-177">下面的代码是一种 LINQ 查询，可从数据库中检索所有流派。</span><span class="sxs-lookup"><span data-stu-id="82929-177">The following code is a LINQ query that retrieves all the genres from the database.</span></span>

[!code-csharp[Main](adding-search/samples/sample12.cs)]

<span data-ttu-id="82929-178">该代码使用 `AddRange` 泛型集合的方法 `List` 将所有不同的流派添加到列表中。</span><span class="sxs-lookup"><span data-stu-id="82929-178">The code uses the `AddRange` method of the generic `List` collection to add all the distinct genres to the list.</span></span> <span data-ttu-id="82929-179"> (没有 `Distinct` 修饰符，将添加重复的流派，例如，在我们的示例) 中添加了两次。</span><span class="sxs-lookup"><span data-stu-id="82929-179">(Without the `Distinct` modifier, duplicate genres would be added — for example, comedy would be added twice in our sample).</span></span> <span data-ttu-id="82929-180">然后，代码会在对象中存储流派列表 `ViewBag.MovieGenre` 。</span><span class="sxs-lookup"><span data-stu-id="82929-180">The code then stores the list of genres in the `ViewBag.MovieGenre` object.</span></span> <span data-ttu-id="82929-181">将类别数据 (此类电影流派) 为中的[SelectList](https://msdn.microsoft.cus/library/system.web.mvc.selectlist(v=vs.108).aspx)对象 `ViewBag` ，然后访问下拉列表框中的类别数据是 MVC 应用程序的典型方法。</span><span class="sxs-lookup"><span data-stu-id="82929-181">Storing category data (such a movie genres) as a [SelectList](https://msdn.microsoft.cus/library/system.web.mvc.selectlist(v=vs.108).aspx) object in a `ViewBag`, then accessing the category data in a dropdown list box is a typical approach for MVC applications.</span></span>

<span data-ttu-id="82929-182">下面的代码演示如何检查 `movieGenre` 参数。</span><span class="sxs-lookup"><span data-stu-id="82929-182">The following code shows how to check the `movieGenre` parameter.</span></span> <span data-ttu-id="82929-183">如果不为空，则代码会进一步限制影片查询，以将所选电影限制为指定的流派。</span><span class="sxs-lookup"><span data-stu-id="82929-183">If it's not empty, the code further constrains the movies query to limit the selected movies to the specified genre.</span></span>

[!code-csharp[Main](adding-search/samples/sample13.cs)]

<span data-ttu-id="82929-184">如前文所述，此查询不会在数据库上运行，直到在该 `Index` 操作方法返回) 后，将电影列表循环访问后 (会发生在视图中。</span><span class="sxs-lookup"><span data-stu-id="82929-184">As stated previously, the query is not run on the database until the movie list is iterated over (which happens in the View, after the `Index` action method returns).</span></span>

## <a name="adding-markup-to-the-index-view-to-support-search-by-genre"></a><span data-ttu-id="82929-185">将标记添加到索引视图以支持按流派搜索</span><span class="sxs-lookup"><span data-stu-id="82929-185">Adding Markup to the Index View to Support Search by Genre</span></span>

<span data-ttu-id="82929-186">将 `Html.DropDownList` helper 添加到*Views\Movies\Index.cshtml*文件中的 `TextBox` 帮助器之前。</span><span class="sxs-lookup"><span data-stu-id="82929-186">Add an `Html.DropDownList` helper to the *Views\Movies\Index.cshtml* file, just before the `TextBox` helper.</span></span> <span data-ttu-id="82929-187">完成的标记如下所示：</span><span class="sxs-lookup"><span data-stu-id="82929-187">The completed markup is shown below:</span></span>

[!code-cshtml[Main](adding-search/samples/sample14.cshtml?highlight=11)]

<span data-ttu-id="82929-188">在以下代码中：</span><span class="sxs-lookup"><span data-stu-id="82929-188">In the following code:</span></span>

[!code-cshtml[Main](adding-search/samples/sample15.cshtml)]

<span data-ttu-id="82929-189">参数 "MovieGenre" 为 `DropDownList` 帮助器提供用于在中查找的键 `IEnumerable<SelectListItem>` `ViewBag` 。</span><span class="sxs-lookup"><span data-stu-id="82929-189">The parameter "MovieGenre" provides the key for the `DropDownList` helper to find a `IEnumerable<SelectListItem>` in the `ViewBag`.</span></span> <span data-ttu-id="82929-190">在 `ViewBag` 操作方法中填充：</span><span class="sxs-lookup"><span data-stu-id="82929-190">The `ViewBag` was populated in the action method:</span></span>

[!code-csharp[Main](adding-search/samples/sample16.cs?highlight=10)]

<span data-ttu-id="82929-191">参数 "All" 提供选项标签。</span><span class="sxs-lookup"><span data-stu-id="82929-191">The parameter "All" provides an option label.</span></span> <span data-ttu-id="82929-192">如果在浏览器中检查该选项，将看到其 "value" 属性为空。</span><span class="sxs-lookup"><span data-stu-id="82929-192">If you inspect that choice in your browser, you'll see that its "value" attribute is empty.</span></span> <span data-ttu-id="82929-193">由于控制器仅筛选 `if` 字符串不为 `null` 或空，因此提交的空值将 `movieGenre` 显示所有流派。</span><span class="sxs-lookup"><span data-stu-id="82929-193">Since our controller only filters `if` the string is not `null` or empty, submitting an empty value for `movieGenre` shows all genres.</span></span>

<span data-ttu-id="82929-194">还可以设置默认情况下选择的选项。</span><span class="sxs-lookup"><span data-stu-id="82929-194">You can also set an option to be selected by default.</span></span> <span data-ttu-id="82929-195">如果需要将 "喜剧" 作为默认选项，可以更改控制器中的代码，如下所示：</span><span class="sxs-lookup"><span data-stu-id="82929-195">If you wanted "Comedy" as your default option, you would change the code in the Controller like so:</span></span>

[!code-cshtml[Main](adding-search/samples/sample17.cshtml)]

<span data-ttu-id="82929-196">运行应用程序并浏览到 */Movies/Index*。</span><span class="sxs-lookup"><span data-stu-id="82929-196">Run the application and browse to */Movies/Index*.</span></span> <span data-ttu-id="82929-197">尝试按流派、电影名称和这两个条件进行搜索。</span><span class="sxs-lookup"><span data-stu-id="82929-197">Try a search by genre, by movie name, and by both criteria.</span></span>

![](adding-search/_static/image8.png)

<span data-ttu-id="82929-198">在本部分中，你创建了一个搜索操作方法和视图，让用户按电影标题和流派进行搜索。</span><span class="sxs-lookup"><span data-stu-id="82929-198">In this section you created a search action method and view that let users search by movie title and genre.</span></span> <span data-ttu-id="82929-199">在下一部分中，你将了解如何将属性添加到 `Movie` 模型，以及如何添加将自动创建测试数据库的初始化表达式。</span><span class="sxs-lookup"><span data-stu-id="82929-199">In the next section, you'll look at how to add a property to the `Movie` model and how to add an initializer that will automatically create a test database.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="82929-200">[上一页](examining-the-edit-methods-and-edit-view.md)
> [下一页](adding-a-new-field.md)</span><span class="sxs-lookup"><span data-stu-id="82929-200">[Previous](examining-the-edit-methods-and-edit-view.md)
[Next](adding-a-new-field.md)</span></span>

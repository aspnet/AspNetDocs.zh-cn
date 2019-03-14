---
title: 将搜索添加到 ASP.NET Core Razor 页面
author: rick-anderson
description: 演示如何将搜索添加到 ASP.NET Core Razor 页面
ms.author: riande
ms.date: 12/3/2018
uid: tutorials/razor-pages/search
ms.openlocfilehash: 3900b33f31fef79327d01b0579208355b0bce90c
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57061514"
---
# <a name="add-search-to-aspnet-core-razor-pages"></a><span data-ttu-id="67ed9-103">将搜索添加到 ASP.NET Core Razor 页面</span><span class="sxs-lookup"><span data-stu-id="67ed9-103">Add search to ASP.NET Core Razor Pages</span></span>

<span data-ttu-id="67ed9-104">作者：[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="67ed9-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[!INCLUDE[](~/includes/rp/download.md)]

<span data-ttu-id="67ed9-105">在以下部分中，添加了按流派或名称搜索电影。</span><span class="sxs-lookup"><span data-stu-id="67ed9-105">In the following sections, searching movies by *genre* or *name* is added.</span></span>

<span data-ttu-id="67ed9-106">将以下突出显示的属性添加到 Pages/Movies/Index.cshtml.cs：</span><span class="sxs-lookup"><span data-stu-id="67ed9-106">Add the following highlighted properties to *Pages/Movies/Index.cshtml.cs*:</span></span>

[!code-csharp[](razor-pages-start/sample/RazorPagesMovie22/Pages/Movies/Index.cshtml.cs?name=snippet_newProps&highlight=11-999)]

* <span data-ttu-id="67ed9-107">`SearchString`：包含用户在搜索文本框中输入的文本。</span><span class="sxs-lookup"><span data-stu-id="67ed9-107">`SearchString`: contains the text users enter in the search text box.</span></span> <span data-ttu-id="67ed9-108">`SearchString` 使用 [`[BindProperty]`](/dotnet/api/microsoft.aspnetcore.mvc.bindpropertyattribute) 特性进行修饰。</span><span class="sxs-lookup"><span data-stu-id="67ed9-108">`SearchString` is decorated with the [`[BindProperty]`](/dotnet/api/microsoft.aspnetcore.mvc.bindpropertyattribute) attribute.</span></span> <span data-ttu-id="67ed9-109">`[BindProperty]` 会绑定名称与属性相同的表单值和查询字符串。</span><span class="sxs-lookup"><span data-stu-id="67ed9-109">`[BindProperty]` binds form values and query strings with the same name as the property.</span></span> <span data-ttu-id="67ed9-110">在 GET 请求中进行绑定需要 `(SupportsGet = true)`。</span><span class="sxs-lookup"><span data-stu-id="67ed9-110">`(SupportsGet = true)` is required for binding on GET requests.</span></span>
* <span data-ttu-id="67ed9-111">`Genres`：包含流派列表。</span><span class="sxs-lookup"><span data-stu-id="67ed9-111">`Genres`: contains the list of genres.</span></span> <span data-ttu-id="67ed9-112">`Genres` 使用户能够从列表中选择一种流派。</span><span class="sxs-lookup"><span data-stu-id="67ed9-112">`Genres` allows the user to select a genre from the list.</span></span> <span data-ttu-id="67ed9-113">`SelectList` 需要 `using Microsoft.AspNetCore.Mvc.Rendering;`</span><span class="sxs-lookup"><span data-stu-id="67ed9-113">`SelectList` requires `using Microsoft.AspNetCore.Mvc.Rendering;`</span></span>
* <span data-ttu-id="67ed9-114">`MovieGenre`：包含用户选择的特定流派（例如“西部”）。</span><span class="sxs-lookup"><span data-stu-id="67ed9-114">`MovieGenre`: contains the specific genre the user selects (for example, "Western").</span></span>
* <span data-ttu-id="67ed9-115">`Genres` 和 `MovieGenre` 会在本教程的后续部分中使用。</span><span class="sxs-lookup"><span data-stu-id="67ed9-115">`Genres` and `MovieGenre` are used later in this tutorial.</span></span>

[!INCLUDE[](~/includes/bind-get.md)]

<span data-ttu-id="67ed9-116">使用以下代码更新索引页面的 `OnGetAsync` 方法：</span><span class="sxs-lookup"><span data-stu-id="67ed9-116">Update the Index page's `OnGetAsync` method with the following code:</span></span>

[!code-csharp[](razor-pages-start/sample/RazorPagesMovie22/Pages/Movies/Index.cshtml.cs?name=snippet_1stSearch)]

<span data-ttu-id="67ed9-117">`OnGetAsync` 方法的第一行创建了 [LINQ](/dotnet/csharp/programming-guide/concepts/linq/) 查询用于选择电影：</span><span class="sxs-lookup"><span data-stu-id="67ed9-117">The first line of the `OnGetAsync` method creates a [LINQ](/dotnet/csharp/programming-guide/concepts/linq/) query to select the movies:</span></span>

```csharp
// using System.Linq;
var movies = from m in _context.Movie
             select m;
```

<span data-ttu-id="67ed9-118">此时仅对查询进行了定义，它还不会针对数据库运行。</span><span class="sxs-lookup"><span data-stu-id="67ed9-118">The query is *only* defined at this point, it has **not** been run against the database.</span></span>

<span data-ttu-id="67ed9-119">如果 `SearchString` 属性不为 null 或空，则电影查询会修改为根据搜索字符串进行筛选：</span><span class="sxs-lookup"><span data-stu-id="67ed9-119">If the `SearchString` property is not null or empty, the movies query is modified to filter on the search string:</span></span>

[!code-csharp[](razor-pages-start/sample/RazorPagesMovie22/Pages/Movies/Index.cshtml.cs?name=snippet_SearchNull)]

<span data-ttu-id="67ed9-120">`s => s.Title.Contains()` 代码是 [Lambda 表达式](/dotnet/csharp/programming-guide/statements-expressions-operators/lambda-expressions)。</span><span class="sxs-lookup"><span data-stu-id="67ed9-120">The `s => s.Title.Contains()` code is a [Lambda Expression](/dotnet/csharp/programming-guide/statements-expressions-operators/lambda-expressions).</span></span> <span data-ttu-id="67ed9-121">Lambda 在基于方法的 [LINQ](/dotnet/csharp/programming-guide/concepts/linq/) 查询中用作标准查询运算符方法的参数，如 [Where](/dotnet/csharp/programming-guide/concepts/linq/query-syntax-and-method-syntax-in-linq) 方法或 `Contains`（前面的代码中所使用的）。</span><span class="sxs-lookup"><span data-stu-id="67ed9-121">Lambdas are used in method-based [LINQ](/dotnet/csharp/programming-guide/concepts/linq/) queries as arguments to standard query operator methods such as the [Where](/dotnet/csharp/programming-guide/concepts/linq/query-syntax-and-method-syntax-in-linq) method or `Contains` (used in the preceding code).</span></span> <span data-ttu-id="67ed9-122">在对 LINQ 查询进行定义或通过调用方法（如 `Where`、`Contains` 或 `OrderBy`）进行修改后，此查询不会被执行。</span><span class="sxs-lookup"><span data-stu-id="67ed9-122">LINQ queries are not executed when they're defined or when they're modified by calling a method (such as `Where`, `Contains`  or `OrderBy`).</span></span> <span data-ttu-id="67ed9-123">相反，会延迟执行查询。</span><span class="sxs-lookup"><span data-stu-id="67ed9-123">Rather, query execution is deferred.</span></span> <span data-ttu-id="67ed9-124">这意味着表达式的计算会延迟，直到循环访问其实现的值或者调用 `ToListAsync` 方法为止。</span><span class="sxs-lookup"><span data-stu-id="67ed9-124">That means the evaluation of an expression is delayed until its realized value is iterated over or the `ToListAsync` method is called.</span></span> <span data-ttu-id="67ed9-125">有关详细信息，请参阅 [Query Execution](/dotnet/framework/data/adonet/ef/language-reference/query-execution)（查询执行）。</span><span class="sxs-lookup"><span data-stu-id="67ed9-125">See [Query Execution](/dotnet/framework/data/adonet/ef/language-reference/query-execution) for more information.</span></span>

<span data-ttu-id="67ed9-126">**注意：**[Contains](/dotnet/api/system.data.objects.dataclasses.entitycollection-1.contains) 方法在数据库中运行，而不是在 C# 代码中运行。</span><span class="sxs-lookup"><span data-stu-id="67ed9-126">**Note:** The [Contains](/dotnet/api/system.data.objects.dataclasses.entitycollection-1.contains) method is run on the database, not in the C# code.</span></span> <span data-ttu-id="67ed9-127">查询是否区分大小写取决于数据库和排序规则。</span><span class="sxs-lookup"><span data-stu-id="67ed9-127">The case sensitivity on the query depends on the database and the collation.</span></span> <span data-ttu-id="67ed9-128">在 SQL Server 上，`Contains` 映射到 [SQL LIKE](/sql/t-sql/language-elements/like-transact-sql)，这是不区分大小写的。</span><span class="sxs-lookup"><span data-stu-id="67ed9-128">On SQL Server, `Contains` maps to [SQL LIKE](/sql/t-sql/language-elements/like-transact-sql), which is case insensitive.</span></span> <span data-ttu-id="67ed9-129">在 SQLite 中，由于使用了默认排序规则，因此需要区分大小写。</span><span class="sxs-lookup"><span data-stu-id="67ed9-129">In SQLite, with the default collation, it's case sensitive.</span></span>

<span data-ttu-id="67ed9-130">导航到电影页面，并向 URL追加一个如 `?searchString=Ghost` 的查询字符串（例如 `https://localhost:5001/Movies?searchString=Ghost`）。</span><span class="sxs-lookup"><span data-stu-id="67ed9-130">Navigate to the Movies page and append a query string such as `?searchString=Ghost` to the URL (for example, `https://localhost:5001/Movies?searchString=Ghost`).</span></span> <span data-ttu-id="67ed9-131">筛选的电影将显示出来。</span><span class="sxs-lookup"><span data-stu-id="67ed9-131">The filtered movies are displayed.</span></span>

![索引视图](search/_static/ghost.png)

<span data-ttu-id="67ed9-133">如果向索引页面添加了以下路由模板，搜索字符串则可作为 URL 段传递（例如 `https://localhost:5001/Movies/Ghost`）。</span><span class="sxs-lookup"><span data-stu-id="67ed9-133">If the following route template is added to the Index page, the search string can be passed as a URL segment (for example, `https://localhost:5001/Movies/Ghost`).</span></span>

```cshtml
@page "{searchString?}"
```

<span data-ttu-id="67ed9-134">前面的路由约束允许按路由数据（URL 段）搜索标题，而不是按查询字符串值进行搜索。</span><span class="sxs-lookup"><span data-stu-id="67ed9-134">The preceding route constraint allows searching the title as route data (a URL segment) instead of as a query string value.</span></span>  <span data-ttu-id="67ed9-135">`"{searchString?}"` 中的 `?` 表示这是可选路由参数。</span><span class="sxs-lookup"><span data-stu-id="67ed9-135">The `?` in `"{searchString?}"` means this is an optional route parameter.</span></span>

![索引视图，显示添加到 URL 的“ghost”一词以及返回的两部电影（Ghostbusters 和 Ghostbusters 2）的电影列表](search/_static/g2.png)

<span data-ttu-id="67ed9-137">ASP.NET Core 运行时使用[模型绑定](xref:mvc/models/model-binding)，通过查询字符串 (`?searchString=Ghost`) 或路由数据 (`https://localhost:5001/Movies/Ghost`) 设置 `SearchString` 属性的值。</span><span class="sxs-lookup"><span data-stu-id="67ed9-137">The ASP.NET Core runtime uses [model binding](xref:mvc/models/model-binding) to set the value of the `SearchString` property from the query string (`?searchString=Ghost`) or route data (`https://localhost:5001/Movies/Ghost`).</span></span> <span data-ttu-id="67ed9-138">模型绑定搜索不区分大小写。</span><span class="sxs-lookup"><span data-stu-id="67ed9-138">Model binding is not case sensitive.</span></span>

<span data-ttu-id="67ed9-139">但是，不能指望用户修改 URL 来搜索电影。</span><span class="sxs-lookup"><span data-stu-id="67ed9-139">However, you can't expect users to modify the URL to search for a movie.</span></span> <span data-ttu-id="67ed9-140">在此步骤中，会添加 UI 来筛选电影。</span><span class="sxs-lookup"><span data-stu-id="67ed9-140">In this step, UI is added to filter movies.</span></span> <span data-ttu-id="67ed9-141">如果已添加路由约束 `"{searchString?}"`，请将它删除。</span><span class="sxs-lookup"><span data-stu-id="67ed9-141">If you added the route constraint `"{searchString?}"`, remove it.</span></span>

<span data-ttu-id="67ed9-142">打开 Pages/Movies/Index.cshtml 文件，并添加以下代码中突出显示的 `<form>` 标记：</span><span class="sxs-lookup"><span data-stu-id="67ed9-142">Open the *Pages/Movies/Index.cshtml* file, and add the `<form>` markup highlighted in the following code:</span></span>

[!code-cshtml[](razor-pages-start/sample/RazorPagesMovie22/Pages/Movies/Index2.cshtml?highlight=14-19&range=1-22)]

<span data-ttu-id="67ed9-143">HTML `<form>` 标记使用以下[标记帮助程序](xref:mvc/views/tag-helpers/intro)：</span><span class="sxs-lookup"><span data-stu-id="67ed9-143">The HTML `<form>` tag uses the following [Tag Helpers](xref:mvc/views/tag-helpers/intro):</span></span>

* <span data-ttu-id="67ed9-144">[表单标记帮助程序](xref:mvc/views/working-with-forms#the-form-tag-helper)。</span><span class="sxs-lookup"><span data-stu-id="67ed9-144">[Form Tag Helper](xref:mvc/views/working-with-forms#the-form-tag-helper).</span></span> <span data-ttu-id="67ed9-145">提交表单时，筛选器字符串将通过查询字符串发送到 Pages/Movies/Index 页面。</span><span class="sxs-lookup"><span data-stu-id="67ed9-145">When the form is submitted, the filter string is sent to the *Pages/Movies/Index* page via query string.</span></span>
* [<span data-ttu-id="67ed9-146">输入标记帮助程序</span><span class="sxs-lookup"><span data-stu-id="67ed9-146">Input Tag Helper</span></span>](xref:mvc/views/working-with-forms#the-input-tag-helper)

<span data-ttu-id="67ed9-147">保存更改并测试筛选器。</span><span class="sxs-lookup"><span data-stu-id="67ed9-147">Save the changes and test the filter.</span></span>

![显示标题筛选器文本框中键入了 ghost 一词的索引视图](search/_static/filter.png)

## <a name="search-by-genre"></a><span data-ttu-id="67ed9-149">按流派搜索</span><span class="sxs-lookup"><span data-stu-id="67ed9-149">Search by genre</span></span>

<span data-ttu-id="67ed9-150">使用以下代码更新 `OnGetAsync` 方法：</span><span class="sxs-lookup"><span data-stu-id="67ed9-150">Update the `OnGetAsync` method with the following code:</span></span>

[!code-csharp[](razor-pages-start/sample/RazorPagesMovie22/Pages/Movies/Index.cshtml.cs?name=snippet_SearchGenre)]

<span data-ttu-id="67ed9-151">下面的代码是一种 LINQ 查询，可从数据库中检索所有流派。</span><span class="sxs-lookup"><span data-stu-id="67ed9-151">The following code is a LINQ query that retrieves all the genres from the database.</span></span>

[!code-csharp[](razor-pages-start/sample/RazorPagesMovie22/Pages/Movies/Index.cshtml.cs?name=snippet_LINQ)]

<span data-ttu-id="67ed9-152">流派的 `SelectList` 是通过投影截然不同的流派创建的。</span><span class="sxs-lookup"><span data-stu-id="67ed9-152">The `SelectList` of genres is created by projecting the distinct genres.</span></span>

[!code-csharp[](razor-pages-start/sample/RazorPagesMovie22/Pages/Movies/Index.cshtml.cs?name=snippet_SelectList)]

### <a name="add-search-by-genre-to-the-razor-page"></a><span data-ttu-id="67ed9-153">将按流派搜索添加到 Razor 页面</span><span class="sxs-lookup"><span data-stu-id="67ed9-153">Add search by genre to the Razor Page</span></span>

<span data-ttu-id="67ed9-154">更新 Index.cshtml，如下所示：</span><span class="sxs-lookup"><span data-stu-id="67ed9-154">Update *Index.cshtml* as follows:</span></span>

[!code-cshtml[](razor-pages-start/sample/RazorPagesMovie22/Pages/Movies/IndexFormGenreNoRating.cshtml?highlight=16-18&range=1-26)]

<span data-ttu-id="67ed9-155">通过按流派或/和电影标题搜索来测试应用。</span><span class="sxs-lookup"><span data-stu-id="67ed9-155">Test the app by searching by genre, by movie title, and by both.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="67ed9-156">[上一篇：更新页面](xref:tutorials/razor-pages/da1)
> [下一篇：添加新字段](xref:tutorials/razor-pages/new-field)</span><span class="sxs-lookup"><span data-stu-id="67ed9-156">[Previous: Updating the pages](xref:tutorials/razor-pages/da1)
[Next: Adding a new field](xref:tutorials/razor-pages/new-field)</span></span>

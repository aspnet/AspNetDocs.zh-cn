---
uid: mvc/overview/getting-started/introduction/accessing-your-models-data-from-a-controller
title: 从控制器访问模型的数据 |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 10/17/2013
ms.assetid: caa1ba4a-f9f0-4181-ba21-042e3997861d
msc.legacyurl: /mvc/overview/getting-started/introduction/accessing-your-models-data-from-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 26d1a66cbc022664af14e4dfe4c4b4892d409b95
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045164"
---
# <a name="accessing-your-models-data-from-a-controller"></a><span data-ttu-id="3c5fb-102">从控制器访问模型的数据</span><span class="sxs-lookup"><span data-stu-id="3c5fb-102">Accessing Your Model's Data from a Controller</span></span>

<span data-ttu-id="3c5fb-103">作者： [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="3c5fb-103">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[!INCLUDE [consider RP](~/includes/razor.md)]

<span data-ttu-id="3c5fb-104">在本部分中，您将创建一个新 `MoviesController` 类并编写代码来检索电影数据，并使用视图模板在浏览器中显示该数据。</span><span class="sxs-lookup"><span data-stu-id="3c5fb-104">In this section, you'll create a new `MoviesController` class and write code that retrieves the movie data and displays it in the browser using a view template.</span></span>

<span data-ttu-id="3c5fb-105">在继续执行下一步之前，请**生成应用程序**。</span><span class="sxs-lookup"><span data-stu-id="3c5fb-105">**Build the application** before going on to the next step.</span></span> <span data-ttu-id="3c5fb-106">如果不生成应用程序，则会在添加控制器时出现错误。</span><span class="sxs-lookup"><span data-stu-id="3c5fb-106">If you don't build the application, you'll get an error adding a controller.</span></span>

<span data-ttu-id="3c5fb-107">在解决方案资源管理器中，右键单击 " *控制器* " 文件夹，然后依次单击 " **添加**"、" **控制器**"。</span><span class="sxs-lookup"><span data-stu-id="3c5fb-107">In Solution Explorer, right-click the *Controllers* folder and then click **Add**, then **Controller**.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image1.png)

<span data-ttu-id="3c5fb-108">在 " **添加基架** " 对话框中，单击 " **包含视图的 MVC 5 控制器，使用实体框架**"，然后单击 " **添加**"。</span><span class="sxs-lookup"><span data-stu-id="3c5fb-108">In the **Add Scaffold** dialog box, click **MVC 5 Controller with views, using Entity Framework**, and then click **Add**.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image2.png)

- <span data-ttu-id="3c5fb-109">为 Model 类选择 " \*\*电影 (MvcMovie") \*\* 。</span><span class="sxs-lookup"><span data-stu-id="3c5fb-109">Select **Movie (MvcMovie.Models)** for the Model class.</span></span>
- <span data-ttu-id="3c5fb-110">为数据上下文类选择 \*\*MovieDBContext (MvcMovie) \*\* 。</span><span class="sxs-lookup"><span data-stu-id="3c5fb-110">Select **MovieDBContext (MvcMovie.Models)** for the Data context class.</span></span>
- <span data-ttu-id="3c5fb-111">对于控制器名称，请输入 **MoviesController**。</span><span class="sxs-lookup"><span data-stu-id="3c5fb-111">For the Controller name enter **MoviesController**.</span></span>

  <span data-ttu-id="3c5fb-112">下图显示了 "已完成" 对话框。</span><span class="sxs-lookup"><span data-stu-id="3c5fb-112">The image below shows the completed dialog.</span></span>  
  
![](accessing-your-models-data-from-a-controller/_static/image3.png)   

<span data-ttu-id="3c5fb-113">单击“添加”。</span><span class="sxs-lookup"><span data-stu-id="3c5fb-113">Click **Add**.</span></span> <span data-ttu-id="3c5fb-114"> (如果出现错误，则可能不会在开始添加控制器之前构建应用程序。 ) Visual Studio 会创建以下文件和文件夹：</span><span class="sxs-lookup"><span data-stu-id="3c5fb-114">(If you get an error, you probably didn't build the application before starting adding the controller.) Visual Studio creates the following files and folders:</span></span>

- <span data-ttu-id="3c5fb-115">"*控制器*" 文件夹中的*MoviesController.cs*文件。</span><span class="sxs-lookup"><span data-stu-id="3c5fb-115">*A MoviesController.cs* file in the *Controllers* folder.</span></span>
- <span data-ttu-id="3c5fb-116">一个 *Views\Movies* 文件夹。</span><span class="sxs-lookup"><span data-stu-id="3c5fb-116">A *Views\Movies* folder.</span></span>
- <span data-ttu-id="3c5fb-117">在新的*Views\Movies* *文件夹中\*\*创建. cshtml、Delete （* cshtml）、Details、</span><span class="sxs-lookup"><span data-stu-id="3c5fb-117">*Create.cshtml, Delete.cshtml, Details.cshtml, Edit.cshtml*, and *Index.cshtml* in the new *Views\Movies* folder.</span></span>

<span data-ttu-id="3c5fb-118">Visual Studio 会自动创建 [crud](http://en.wikipedia.org/wiki/Create,_read,_update_and_delete) (创建、读取、更新和删除) 操作方法和视图， (自动创建 crud 操作方法和视图称为基架) 。</span><span class="sxs-lookup"><span data-stu-id="3c5fb-118">Visual Studio automatically created the [CRUD](http://en.wikipedia.org/wiki/Create,_read,_update_and_delete) (create, read, update, and delete) action methods and views for you (the automatic creation of CRUD action methods and views is known as scaffolding).</span></span> <span data-ttu-id="3c5fb-119">现在，你有了一个功能完备的 web 应用程序，它允许你创建、列出、编辑和删除电影条目。</span><span class="sxs-lookup"><span data-stu-id="3c5fb-119">You now have a fully functional web application that lets you create, list, edit, and delete movie entries.</span></span>

<span data-ttu-id="3c5fb-120">运行应用程序，单击 " **MVC 电影** " 链接 (或 `Movies` 通过将 */Movies* 追加到浏览器的地址栏中的 URL 来浏览到控制器) 。</span><span class="sxs-lookup"><span data-stu-id="3c5fb-120">Run the application and click on the **MVC Movie** link (or browse to the `Movies` controller by appending */Movies* to the URL in the address bar of your browser).</span></span> <span data-ttu-id="3c5fb-121">由于应用程序依赖于 *应用 \_ Start\RouteConfig.cs* 文件) 中定义的默认路由 (，因此浏览器请求 `http://localhost:xxxxx/Movies` 将路由到控制器的默认 `Index` 操作方法 `Movies` 。</span><span class="sxs-lookup"><span data-stu-id="3c5fb-121">Because the application is relying on the default routing (defined in the *App\_Start\RouteConfig.cs* file), the browser request `http://localhost:xxxxx/Movies` is routed to the default `Index` action method of the `Movies` controller.</span></span> <span data-ttu-id="3c5fb-122">换句话说，浏览器请求实际上与 `http://localhost:xxxxx/Movies` 浏览器请求相同 `http://localhost:xxxxx/Movies/Index` 。</span><span class="sxs-lookup"><span data-stu-id="3c5fb-122">In other words, the browser request `http://localhost:xxxxx/Movies` is effectively the same as the browser request `http://localhost:xxxxx/Movies/Index`.</span></span> <span data-ttu-id="3c5fb-123">结果为空电影列表，因为尚未添加任何影片。</span><span class="sxs-lookup"><span data-stu-id="3c5fb-123">The result is an empty list of movies, because you haven't added any yet.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image4.png)

### <a name="creating-a-movie"></a><span data-ttu-id="3c5fb-124">创建电影</span><span class="sxs-lookup"><span data-stu-id="3c5fb-124">Creating a Movie</span></span>

<span data-ttu-id="3c5fb-125">选择“新建”链接。</span><span class="sxs-lookup"><span data-stu-id="3c5fb-125">Select the **Create New** link.</span></span> <span data-ttu-id="3c5fb-126">输入有关电影的一些详细信息，然后单击 " **创建** " 按钮。</span><span class="sxs-lookup"><span data-stu-id="3c5fb-126">Enter some details about a movie and then click the **Create** button.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image5.png)

> [!NOTE]
> <span data-ttu-id="3c5fb-127">您可能无法在 "价格" 字段中输入小数点或逗号。</span><span class="sxs-lookup"><span data-stu-id="3c5fb-127">You may not be able to enter decimal points or commas in the Price field.</span></span> <span data-ttu-id="3c5fb-128">若要支持使用逗号 (的非英语区域设置的 jQuery 验证 &quot; 、 &quot;) 用于小数点和非美国英语日期格式，你必须将 *globalize.js* 和特定 *区域性/globalize.cultures.js* 文件从 [https://github.com/jquery/globalize](https://github.com/jquery/globalize) (和 JavaScript ) 到使用 `Globalize.parseFloat` 。</span><span class="sxs-lookup"><span data-stu-id="3c5fb-128">To support jQuery validation for non-English locales that use a comma (&quot;,&quot;) for a decimal point, and non US-English date formats, you must include *globalize.js* and your specific *cultures/globalize.cultures.js* file(from [https://github.com/jquery/globalize](https://github.com/jquery/globalize) ) and JavaScript to use `Globalize.parseFloat`.</span></span> <span data-ttu-id="3c5fb-129">下一教程将演示如何执行此操作。</span><span class="sxs-lookup"><span data-stu-id="3c5fb-129">I'll show how to do this in the next tutorial.</span></span> <span data-ttu-id="3c5fb-130">目前，只能输入整数，例如 10。</span><span class="sxs-lookup"><span data-stu-id="3c5fb-130">For now, just enter whole numbers like 10.</span></span>

<span data-ttu-id="3c5fb-131">单击 " **创建** " 按钮会将窗体发布到服务器，在该窗体中，电影信息保存在数据库中。</span><span class="sxs-lookup"><span data-stu-id="3c5fb-131">Clicking the **Create** button causes the form to be posted to the server, where the movie information is saved in the database.</span></span> <span data-ttu-id="3c5fb-132">然后，你会被重定向到 */Movies* URL，在该 URL 中，你可以在列表中看到新创建的电影。</span><span class="sxs-lookup"><span data-stu-id="3c5fb-132">You're then redirected to the */Movies* URL, where you can see the newly created movie in the listing.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image6.png)

<span data-ttu-id="3c5fb-133">再创建几个其他的电影条目。</span><span class="sxs-lookup"><span data-stu-id="3c5fb-133">Create a couple more movie entries.</span></span> <span data-ttu-id="3c5fb-134">试用“编辑”\*\*\*\*、“详细信息”\*\*\*\* 和“删除”\*\*\*\* 链接，它们均可正常工作。</span><span class="sxs-lookup"><span data-stu-id="3c5fb-134">Try the **Edit**, **Details**, and **Delete** links, which are all functional.</span></span>

## <a name="examining-the-generated-code"></a><span data-ttu-id="3c5fb-135">检查生成的代码</span><span class="sxs-lookup"><span data-stu-id="3c5fb-135">Examining the Generated Code</span></span>

<span data-ttu-id="3c5fb-136">打开 *Controllers\MoviesController.cs* 文件并检查生成的 `Index` 方法。</span><span class="sxs-lookup"><span data-stu-id="3c5fb-136">Open the *Controllers\MoviesController.cs* file and examine the generated `Index` method.</span></span> <span data-ttu-id="3c5fb-137">下面显示了包含方法的影片控制器的部分 `Index` 。</span><span class="sxs-lookup"><span data-stu-id="3c5fb-137">A portion of the movie controller with the `Index` method is shown below.</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample1.cs)]

<span data-ttu-id="3c5fb-138">对控制器的请求将 `Movies` 返回表中的所有条目 `Movies` ，然后将结果传递给 `Index` 视图。</span><span class="sxs-lookup"><span data-stu-id="3c5fb-138">A request to the `Movies` controller returns all the entries in the `Movies` table and then passes the results to the `Index` view.</span></span> <span data-ttu-id="3c5fb-139">`MoviesController`如前文所述，类中的以下行将实例化电影数据库上下文。</span><span class="sxs-lookup"><span data-stu-id="3c5fb-139">The following line from the `MoviesController` class instantiates a movie database context, as described previously.</span></span> <span data-ttu-id="3c5fb-140">可以使用影片数据库上下文来查询、编辑和删除影片。</span><span class="sxs-lookup"><span data-stu-id="3c5fb-140">You can use the movie database context to query, edit, and delete movies.</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample2.cs)]

## <a name="strongly-typed-models-and-the-model-keyword"></a><span data-ttu-id="3c5fb-141">强类型模型和 @model 关键字</span><span class="sxs-lookup"><span data-stu-id="3c5fb-141">Strongly Typed Models and the @model Keyword</span></span>

<span data-ttu-id="3c5fb-142">在本教程的前面部分，你已了解控制器如何使用对象将数据或对象传递到视图模板 `ViewBag` 。</span><span class="sxs-lookup"><span data-stu-id="3c5fb-142">Earlier in this tutorial, you saw how a controller can pass data or objects to a view template using the `ViewBag` object.</span></span> <span data-ttu-id="3c5fb-143">`ViewBag`是一个动态对象，它提供了一种用于向视图传递信息的后期绑定方法。</span><span class="sxs-lookup"><span data-stu-id="3c5fb-143">The `ViewBag` is a dynamic object that provides a convenient late-bound way to pass information to a view.</span></span>

<span data-ttu-id="3c5fb-144">MVC 还提供将 *强* 类型对象传递到视图模板的功能。</span><span class="sxs-lookup"><span data-stu-id="3c5fb-144">MVC also provides the ability to pass *strongly* typed objects to a view template.</span></span> <span data-ttu-id="3c5fb-145">此强类型方法可在 Visual Studio 编辑器中更好地编译代码和更丰富的 [IntelliSense](https://msdn.microsoft.com/library/hcw1s69b(v=vs.120).aspx) 。</span><span class="sxs-lookup"><span data-stu-id="3c5fb-145">This strongly typed approach enables better compile-time checking of your code and richer [IntelliSense](https://msdn.microsoft.com/library/hcw1s69b(v=vs.120).aspx) in the Visual Studio editor.</span></span> <span data-ttu-id="3c5fb-146">Visual Studio 中的基架机制使用这种方法 (也就是说，在创建方法和视图时，传递 *强* 类型化模型) `MoviesController` 和类和视图模板。</span><span class="sxs-lookup"><span data-stu-id="3c5fb-146">The scaffolding mechanism in Visual Studio used this approach (that is, passing a *strongly* typed model) with the `MoviesController` class and view templates when it created the methods and views.</span></span>

<span data-ttu-id="3c5fb-147">在 *Controllers\MoviesController.cs* 文件中，检查生成的 `Details` 方法。</span><span class="sxs-lookup"><span data-stu-id="3c5fb-147">In the *Controllers\MoviesController.cs* file examine the generated `Details` method.</span></span> <span data-ttu-id="3c5fb-148">此 `Details` 方法如下所示。</span><span class="sxs-lookup"><span data-stu-id="3c5fb-148">The `Details` method is shown below.</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample3.cs)]

<span data-ttu-id="3c5fb-149">`id`参数通常作为路由数据传递，例如， `http://localhost:1234/movies/details/1` 将控制器设置为电影控制器，将操作设置为 `details` 并将设置为 `id` 1。</span><span class="sxs-lookup"><span data-stu-id="3c5fb-149">The `id` parameter is generally passed as route data, for example `http://localhost:1234/movies/details/1` will set the controller to the movie controller, the action to `details` and the `id` to 1.</span></span> <span data-ttu-id="3c5fb-150">你还可以使用查询字符串传入 id，如下所示：</span><span class="sxs-lookup"><span data-stu-id="3c5fb-150">You could also pass in the id with a query string as follows:</span></span>

`http://localhost:1234/movies/details?id=1`

<span data-ttu-id="3c5fb-151">如果找到了，则会将 `Movie` 模型的实例 `Movie` 传递给 `Details` 视图：</span><span class="sxs-lookup"><span data-stu-id="3c5fb-151">If a `Movie` is found, an instance of the `Movie` model is passed to the `Details` view:</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample4.cs)]

<span data-ttu-id="3c5fb-152">检查 *Views\Movies\Details.cshtml* 文件的内容：</span><span class="sxs-lookup"><span data-stu-id="3c5fb-152">Examine the contents of the *Views\Movies\Details.cshtml* file:</span></span>

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample5.cshtml?highlight=1-2)]

<span data-ttu-id="3c5fb-153">通过将 `@model` 语句包含在视图模板文件的顶部，可以指定视图所需的对象类型。</span><span class="sxs-lookup"><span data-stu-id="3c5fb-153">By including a `@model` statement at the top of the view template file, you can specify the type of object that the view expects.</span></span> <span data-ttu-id="3c5fb-154">创建电影控制器时，Visual Studio 会自动在 Details.cshtml 文件的顶端包括以下 `@model` 语句\*\*：</span><span class="sxs-lookup"><span data-stu-id="3c5fb-154">When you created the movie controller, Visual Studio automatically included the following `@model` statement at the top of the *Details.cshtml* file:</span></span>

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample6.cshtml)]

<span data-ttu-id="3c5fb-155">此 `@model` 指令使你能够使用强类型的 `Model` 对象访问控制器传递给视图的电影。</span><span class="sxs-lookup"><span data-stu-id="3c5fb-155">This `@model` directive allows you to access the movie that the controller passed to the view by using a `Model` object that's strongly typed.</span></span> <span data-ttu-id="3c5fb-156">例如，在 *详细信息* 模板中，代码将每个电影字段传递给 `DisplayNameFor` 强类型化对象的和 [DisplayFor](https://msdn.microsoft.com/library/system.web.mvc.html.displayextensions.displayfor(VS.98).aspx) HTML 帮助程序 `Model` 。</span><span class="sxs-lookup"><span data-stu-id="3c5fb-156">For example, in the *Details.cshtml* template, the code passes each movie field to the `DisplayNameFor` and [DisplayFor](https://msdn.microsoft.com/library/system.web.mvc.html.displayextensions.displayfor(VS.98).aspx) HTML Helpers with the strongly typed `Model` object.</span></span> <span data-ttu-id="3c5fb-157">`Create`和 `Edit` 方法和视图模板也会传递影片模型对象。</span><span class="sxs-lookup"><span data-stu-id="3c5fb-157">The `Create` and `Edit` methods and view templates also pass a movie model object.</span></span>

<span data-ttu-id="3c5fb-158">检查 MoviesController.cs 文件中的*索引 cshtml*视图模板和 `Index` 方法。 *MoviesController.cs*</span><span class="sxs-lookup"><span data-stu-id="3c5fb-158">Examine the *Index.cshtml* view template and the `Index` method in the *MoviesController.cs* file.</span></span> <span data-ttu-id="3c5fb-159">请注意，代码在 [`List`](https://msdn.microsoft.com/library/6sh2ey19.aspx) `View` 操作方法中调用帮助程序方法时如何创建对象 `Index` 。</span><span class="sxs-lookup"><span data-stu-id="3c5fb-159">Notice how the code creates a [`List`](https://msdn.microsoft.com/library/6sh2ey19.aspx) object when it calls the `View` helper method in the `Index` action method.</span></span> <span data-ttu-id="3c5fb-160">然后，该代码将此 `Movies` 列表从 `Index` 操作方法传递给视图：</span><span class="sxs-lookup"><span data-stu-id="3c5fb-160">The code then passes this `Movies` list from the `Index` action method to the view:</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample7.cs?highlight=3)]

<span data-ttu-id="3c5fb-161">创建影片控制器时，Visual Studio 会自动将以下语句包含 `@model` 在 *索引 cshtml* 文件的顶部：</span><span class="sxs-lookup"><span data-stu-id="3c5fb-161">When you created the movie controller, Visual Studio automatically included the following `@model` statement at the top of the *Index.cshtml* file:</span></span>

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample8.cshtml)]

<span data-ttu-id="3c5fb-162">此 `@model` 指令允许使用强类型的对象访问控制器传递给视图的电影列表 `Model` 。</span><span class="sxs-lookup"><span data-stu-id="3c5fb-162">This `@model` directive allows you to access the list of movies that the controller passed to the view by using a `Model` object that's strongly typed.</span></span> <span data-ttu-id="3c5fb-163">例如，在 *索引 cshtml* 模板中，代码通过对 `foreach` 强类型对象执行语句来循环播放电影 `Model` ：</span><span class="sxs-lookup"><span data-stu-id="3c5fb-163">For example, in the *Index.cshtml* template, the code loops through the movies by doing a `foreach` statement over the strongly typed `Model` object:</span></span>

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample9.cshtml?highlight=1,4,7,10,13,16,19-21)]

<span data-ttu-id="3c5fb-164">由于 `Model` 对象已强类型化 (作为 `IEnumerable<Movie>` 对象) ，因此循环中的每个 `item` 对象都被类型化为 `Movie` 。</span><span class="sxs-lookup"><span data-stu-id="3c5fb-164">Because the `Model` object is strongly typed (as an `IEnumerable<Movie>` object), each `item` object in the loop is typed as `Movie`.</span></span> <span data-ttu-id="3c5fb-165">除此之外，这意味着您可以在代码编辑器中对代码进行编译时检查，并获得完整的 IntelliSense 支持：</span><span class="sxs-lookup"><span data-stu-id="3c5fb-165">Among other benefits, this means that you get compile-time checking of the code and full IntelliSense support in the code editor:</span></span>

![ModelIntelliSense](accessing-your-models-data-from-a-controller/_static/image8.png)

## <a name="working-with-sql-server-localdb"></a><span data-ttu-id="3c5fb-167">使用 SQL Server LocalDB</span><span class="sxs-lookup"><span data-stu-id="3c5fb-167">Working with SQL Server LocalDB</span></span>

<span data-ttu-id="3c5fb-168">实体框架 Code First 检测到提供的数据库连接字符串指向的 `Movies` 数据库尚不存在，因此 Code First 自动创建数据库。</span><span class="sxs-lookup"><span data-stu-id="3c5fb-168">Entity Framework Code First detected that the database connection string that was provided pointed to a `Movies` database that didn't exist yet, so Code First created the database automatically.</span></span> <span data-ttu-id="3c5fb-169">可以通过查看 *应用 \_ 数据* 文件夹来验证是否已创建。</span><span class="sxs-lookup"><span data-stu-id="3c5fb-169">You can verify that it's been created by looking in the *App\_Data* folder.</span></span> <span data-ttu-id="3c5fb-170">如果看不到 "*电影 .mdf* " 文件，请单击 "**解决方案资源管理器**" 工具栏中的 "**显示所有文件**" 按钮，单击 "**刷新**" 按钮，然后展开 "*应用程序 \_ 数据*" 文件夹。</span><span class="sxs-lookup"><span data-stu-id="3c5fb-170">If you don't see the *Movies.mdf* file, click the **Show All Files** button in the **Solution Explorer** toolbar, click the **Refresh** button, and then expand the *App\_Data* folder.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image9.png)

<span data-ttu-id="3c5fb-171">双击 *""，以打开* " **服务器资源管理器**"，然后展开 " **表** " 文件夹以查看 "电影" 表。</span><span class="sxs-lookup"><span data-stu-id="3c5fb-171">Double-click *Movies.mdf* to open **SERVER EXPLORER**, then expand the **Tables** folder to see the Movies table.</span></span> <span data-ttu-id="3c5fb-172">请注意 ID 旁边的密钥图标。</span><span class="sxs-lookup"><span data-stu-id="3c5fb-172">Note the key icon next to ID.</span></span> <span data-ttu-id="3c5fb-173">默认情况下，EF 会将名为 ID 的属性设置为主键。</span><span class="sxs-lookup"><span data-stu-id="3c5fb-173">By default, EF will make a property named ID the primary key.</span></span> <span data-ttu-id="3c5fb-174">有关 [EF 和 mvc](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)的详细信息，请参阅 Tom Dykstra 的绝佳教程。</span><span class="sxs-lookup"><span data-stu-id="3c5fb-174">For more information on EF and MVC, see Tom Dykstra's excellent tutorial on [MVC and EF](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>

<span data-ttu-id="3c5fb-175">![DB_explorer](accessing-your-models-data-from-a-controller/_static/image10.png "DB_explorer")</span><span class="sxs-lookup"><span data-stu-id="3c5fb-175">![DB_explorer](accessing-your-models-data-from-a-controller/_static/image10.png "DB_explorer")</span></span>

<span data-ttu-id="3c5fb-176">右键单击 `Movies` 该表，然后选择 " **显示表数据** " 以查看创建的数据。</span><span class="sxs-lookup"><span data-stu-id="3c5fb-176">Right-click the `Movies` table and select **Show Table Data** to see the data you created.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image11.png) 

![](accessing-your-models-data-from-a-controller/_static/image12.png)

<span data-ttu-id="3c5fb-177">右键单击 `Movies` 该表，然后选择 " **打开表定义** "，查看实体框架 Code First 创建的表结构。</span><span class="sxs-lookup"><span data-stu-id="3c5fb-177">Right-click the `Movies` table and select **Open Table Definition** to see the table structure that Entity Framework Code First created for you.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image13.png)

![](accessing-your-models-data-from-a-controller/_static/image14.png)

<span data-ttu-id="3c5fb-178">请注意，表的架构如何 `Movies` 映射到 `Movie` 前面创建的类。</span><span class="sxs-lookup"><span data-stu-id="3c5fb-178">Notice how the schema of the `Movies` table maps to the `Movie` class you created earlier.</span></span> <span data-ttu-id="3c5fb-179">实体框架 Code First 会根据你的类自动为你创建此架构 `Movie` 。</span><span class="sxs-lookup"><span data-stu-id="3c5fb-179">Entity Framework Code First automatically created this schema for you based on your `Movie` class.</span></span>

<span data-ttu-id="3c5fb-180">完成后，请通过右键单击 *MovieDBContext* 并选择 " **关闭连接**" 来关闭连接。</span><span class="sxs-lookup"><span data-stu-id="3c5fb-180">When you're finished, close the connection by right clicking *MovieDBContext* and selecting **Close Connection**.</span></span> <span data-ttu-id="3c5fb-181"> (如果未关闭连接，则在下次运行项目时可能会收到错误) 。</span><span class="sxs-lookup"><span data-stu-id="3c5fb-181">(If you don't close the connection, you might get an error the next time you run the project).</span></span>

![](accessing-your-models-data-from-a-controller/_static/image15.png "CloseConnection")

<span data-ttu-id="3c5fb-182">现在你已拥有用于显示、编辑、更新和删除数据的数据库和页面。</span><span class="sxs-lookup"><span data-stu-id="3c5fb-182">You now have a database and pages to display, edit, update and delete data.</span></span> <span data-ttu-id="3c5fb-183">在下一教程中，我们将研究基架代码的其余部分并添加 `SearchIndex` 方法和 `SearchIndex` 视图，以便在此数据库中搜索电影。</span><span class="sxs-lookup"><span data-stu-id="3c5fb-183">In the next tutorial, we'll examine the rest of the scaffolded code and add a `SearchIndex` method and a `SearchIndex` view that lets you search for movies in this database.</span></span> <span data-ttu-id="3c5fb-184">有关将实体框架与 MVC 结合使用的详细信息，请参阅为 [ASP.NET MVC 应用程序创建实体框架数据模型](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。</span><span class="sxs-lookup"><span data-stu-id="3c5fb-184">For more information on using Entity Framework with MVC, see [Creating an Entity Framework Data Model for an ASP.NET MVC Application](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="3c5fb-185">[上一页](creating-a-connection-string.md)
> [下一页](examining-the-edit-methods-and-edit-view.md)</span><span class="sxs-lookup"><span data-stu-id="3c5fb-185">[Previous](creating-a-connection-string.md)
[Next](examining-the-edit-methods-and-edit-view.md)</span></span>

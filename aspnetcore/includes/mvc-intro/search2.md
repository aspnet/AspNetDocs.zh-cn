---
ms.openlocfilehash: d5d902a2a6fcae3155c23d0040a8026ed5808dff
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57047954"
---
<!--
[!code-html[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Views/Shared/_Layout.cshtml?highlight=7,31)]


[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Controllers/MoviesController.cs?name=snippet_1stSearch)]

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Controllers/MoviesController.cs?name=snippet_SearchNull)]

![Index view](~/tutorials/first-mvc-app/search/_static/ghost.png)


[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Startup.cs?highlight=5&name=snippet_1)]

--> 

<span data-ttu-id="b9fd0-101">之前的 `Index` 方法：</span><span class="sxs-lookup"><span data-stu-id="b9fd0-101">The previous `Index` method:</span></span>

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Controllers/MoviesController.cs?highlight=1,8&name=snippet_1stSearch)]

<span data-ttu-id="b9fd0-102">更新后带 `id` 参数的 `Index` 方法：</span><span class="sxs-lookup"><span data-stu-id="b9fd0-102">The updated `Index` method with `id` parameter:</span></span>

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Controllers/MoviesController.cs?highlight=1,8&name=snippet_SearchID)]

<span data-ttu-id="b9fd0-103">现可将搜索标题作为路由数据（ URL 段）而非查询字符串值进行传递。</span><span class="sxs-lookup"><span data-stu-id="b9fd0-103">You can now pass the search title as route data (a URL segment) instead of as a query string value.</span></span>

![索引视图，显示添加到 URL 的“ghost”一词以及返回的两部电影（Ghostbusters 和 Ghostbusters 2）的电影列表](~/tutorials/first-mvc-app/search/_static/g2.png)

<span data-ttu-id="b9fd0-105">但是，不能指望用户在每次要搜索电影时都修改 URL。</span><span class="sxs-lookup"><span data-stu-id="b9fd0-105">However, you can't expect users to modify the URL every time they want to search for a movie.</span></span> <span data-ttu-id="b9fd0-106">因此需要添加 UI 元素来帮助他们筛选电影。</span><span class="sxs-lookup"><span data-stu-id="b9fd0-106">So now you'll add UI elements to help them filter movies.</span></span> <span data-ttu-id="b9fd0-107">若已更改 `Index` 方法的签名，以测试如何传递绑定路由的 `ID` 参数，请改回原样，使其采用名为 `searchString` 的参数：</span><span class="sxs-lookup"><span data-stu-id="b9fd0-107">If you changed the signature of the `Index` method to test how to pass the route-bound `ID` parameter, change it back so that it takes a parameter named `searchString`:</span></span>

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Controllers/MoviesController.cs?highlight=1&name=snippet_1stSearch)]

<span data-ttu-id="b9fd0-108">打开“Views/Movies/Index.cshtml”文件，并添加以下突出显示的 `<form>` 标记：</span><span class="sxs-lookup"><span data-stu-id="b9fd0-108">Open the *Views/Movies/Index.cshtml* file, and add the `<form>` markup highlighted below:</span></span>

[!code-HTML[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Views/Movies/IndexForm1.cshtml?highlight=10-16&range=4-21)]

<span data-ttu-id="b9fd0-109">此 HTML `<form>` 标记使用[表单标记帮助程序](xref:mvc/views/working-with-forms)，因此提交表单时，筛选器字符串会发布到电影控制器的 `Index` 操作。</span><span class="sxs-lookup"><span data-stu-id="b9fd0-109">The HTML `<form>` tag uses the [Form Tag Helper](xref:mvc/views/working-with-forms), so when you submit the form, the filter string is posted to the `Index` action of the movies controller.</span></span> <span data-ttu-id="b9fd0-110">保存更改，然后测试筛选器。</span><span class="sxs-lookup"><span data-stu-id="b9fd0-110">Save your changes and then test the filter.</span></span>

![显示标题筛选器文本框中键入了 ghost 一词的索引视图](~/tutorials/first-mvc-app/search/_static/filter.png)

<span data-ttu-id="b9fd0-112">如你所料，不存在 `Index` 方法的 `[HttpPost]` 重载。</span><span class="sxs-lookup"><span data-stu-id="b9fd0-112">There's no `[HttpPost]` overload of the `Index` method as you might expect.</span></span> <span data-ttu-id="b9fd0-113">无需重载，因为该方法不更改应用的状态，仅筛选数据。</span><span class="sxs-lookup"><span data-stu-id="b9fd0-113">You don't need it, because the method isn't changing the state of the app, just filtering data.</span></span>

<span data-ttu-id="b9fd0-114">可添加以下 `[HttpPost] Index` 方法。</span><span class="sxs-lookup"><span data-stu-id="b9fd0-114">You could add the following `[HttpPost] Index` method.</span></span>

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Controllers/MoviesController.cs?highlight=1&name=snippet_SearchPost)]

<span data-ttu-id="b9fd0-115">`notUsed` 参数用于创建 `Index` 方法的重载。</span><span class="sxs-lookup"><span data-stu-id="b9fd0-115">The `notUsed` parameter is used to create an overload for the `Index` method.</span></span> <span data-ttu-id="b9fd0-116">本教程稍后将对此进行探讨。</span><span class="sxs-lookup"><span data-stu-id="b9fd0-116">We'll talk about that later in the tutorial.</span></span>

<span data-ttu-id="b9fd0-117">如果添加此方法，则操作调用程序将与 `[HttpPost] Index` 方法匹配，且将运行 `[HttpPost] Index` 方法，如下图所示。</span><span class="sxs-lookup"><span data-stu-id="b9fd0-117">If you add this method, the action invoker would match the `[HttpPost] Index` method, and the `[HttpPost] Index` method would run as shown in the image below.</span></span>

![显示“来自 HttpPost 索引: 筛选 ghost”应用程序响应的浏览器窗口](~/tutorials/first-mvc-app/search/_static/fo.png)

<span data-ttu-id="b9fd0-119">但是，即使添加 `Index` 方法的 `[HttpPost]` 版本，其实现方式也受到限制。</span><span class="sxs-lookup"><span data-stu-id="b9fd0-119">However, even if you add this `[HttpPost]` version of the `Index` method, there's a limitation in how this has all been implemented.</span></span> <span data-ttu-id="b9fd0-120">假设你想要将特定搜索加入书签，或向朋友发送一个链接，让他们单击链接即可查看筛选出的相同电影列表。</span><span class="sxs-lookup"><span data-stu-id="b9fd0-120">Imagine that you want to bookmark a particular search or you want to send a link to friends that they can click in order to see the same filtered list of movies.</span></span> <span data-ttu-id="b9fd0-121">请注意，HTTP POST 请求的 URL 与 GET 请求的 URL 相同 (localhost:xxxxx/Movies/Index)，其中不包含搜索信息。</span><span class="sxs-lookup"><span data-stu-id="b9fd0-121">Notice that the URL for the HTTP POST request is the same as the URL for the GET request (localhost:xxxxx/Movies/Index) -- there's no search information in the URL.</span></span> <span data-ttu-id="b9fd0-122">搜索字符串信息作为[表单域值](https://developer.mozilla.org/docs/Learn/HTML/Forms/Sending_and_retrieving_form_data)发送给服务器。</span><span class="sxs-lookup"><span data-stu-id="b9fd0-122">The search string information is sent to the server as a [form field value](https://developer.mozilla.org/docs/Learn/HTML/Forms/Sending_and_retrieving_form_data).</span></span> <span data-ttu-id="b9fd0-123">可使用浏览器开发人员工具或出色的 [Fiddler 工具](http://www.telerik.com/fiddler)对其进行验证。</span><span class="sxs-lookup"><span data-stu-id="b9fd0-123">You can verify that with the browser Developer tools or the excellent [Fiddler tool](http://www.telerik.com/fiddler).</span></span> <span data-ttu-id="b9fd0-124">下图展示了 Chrome 浏览器开发人员工具：</span><span class="sxs-lookup"><span data-stu-id="b9fd0-124">The image below shows the Chrome browser Developer tools:</span></span>

![Microsoft Edge 中开发人员工具的“网络”选项卡，显示了 ghost 的 searchString 值的请求正文](~/tutorials/first-mvc-app/search/_static/f12_rb.png)

<span data-ttu-id="b9fd0-126">在请求正文中，可看到搜索参数和 [XSRF](xref:security/anti-request-forgery) 标记。</span><span class="sxs-lookup"><span data-stu-id="b9fd0-126">You can see the search parameter and [XSRF](xref:security/anti-request-forgery) token in the request body.</span></span> <span data-ttu-id="b9fd0-127">请注意，正如之前教程所述，[表单标记帮助程序](xref:mvc/views/working-with-forms) 会生成一个 [XSRF](xref:security/anti-request-forgery) 防伪标记。</span><span class="sxs-lookup"><span data-stu-id="b9fd0-127">Note, as mentioned in the previous tutorial, the [Form Tag Helper](xref:mvc/views/working-with-forms) generates an [XSRF](xref:security/anti-request-forgery) anti-forgery token.</span></span> <span data-ttu-id="b9fd0-128">不会修改数据，因此无需验证控制器方法中的标记。</span><span class="sxs-lookup"><span data-stu-id="b9fd0-128">We're not modifying data, so we don't need to validate the token in the controller method.</span></span>

<span data-ttu-id="b9fd0-129">搜索参数位于请求正文而非 URL 中，因此无法捕获该搜索信息进行书签设定或与他人共享。</span><span class="sxs-lookup"><span data-stu-id="b9fd0-129">Because the search parameter is in the request body and not the URL, you can't capture that search information to bookmark or share with others.</span></span> <span data-ttu-id="b9fd0-130">将通过指定请求为 `HTTP GET` 进行修复。</span><span class="sxs-lookup"><span data-stu-id="b9fd0-130">We'll fix this by specifying the request should be `HTTP GET`.</span></span>

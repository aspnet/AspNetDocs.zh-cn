---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-controller
title: 添加控制器 |Microsoft Docs
author: Rick-Anderson
description: 注意：本教程的更新版本可在此处使用 ASP.NET MVC 5 和 Visual Studio 2013。 更安全、更简单的操作和演示 。
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 0267d31c-892f-49a1-9e7a-3ae8cc12b2ca
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-controller
msc.type: authoredcontent
ms.openlocfilehash: f528c56435976c7f31fce453c834ef9eaebe6244
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78485444"
---
# <a name="adding-a-controller"></a><span data-ttu-id="1cf2b-104">添加控制器</span><span class="sxs-lookup"><span data-stu-id="1cf2b-104">Adding a Controller</span></span>

<span data-ttu-id="1cf2b-105">作者： [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="1cf2b-105">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> > [!NOTE]
> > <span data-ttu-id="1cf2b-106">[此处](../../getting-started/introduction/getting-started.md)提供了本教程的更新版本，其中使用 ASP.NET MVC 5 和 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="1cf2b-106">An updated version of this tutorial is available [here](../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="1cf2b-107">更安全的方法是遵循更多功能，并演示更多的功能。</span><span class="sxs-lookup"><span data-stu-id="1cf2b-107">It's more secure, much simpler to follow and demonstrates more features.</span></span>

<span data-ttu-id="1cf2b-108">MVC 代表*模型-视图-控制器*。</span><span class="sxs-lookup"><span data-stu-id="1cf2b-108">MVC stands for *model-view-controller*.</span></span> <span data-ttu-id="1cf2b-109">MVC 是用于开发应用程序的一种模式，该模式设计良好、可测试且易于维护。</span><span class="sxs-lookup"><span data-stu-id="1cf2b-109">MVC is a pattern for developing applications that are well architected, testable and easy to maintain.</span></span> <span data-ttu-id="1cf2b-110">基于 MVC 的应用程序包含：</span><span class="sxs-lookup"><span data-stu-id="1cf2b-110">MVC-based applications contain:</span></span>

- <span data-ttu-id="1cf2b-111">**M**模式：类，这些类表示应用程序的数据，并使用验证逻辑来强制执行该数据的业务规则。</span><span class="sxs-lookup"><span data-stu-id="1cf2b-111">**M** odels: Classes that represent the data of the application and that use validation logic to enforce business rules for that data.</span></span>
- <span data-ttu-id="1cf2b-112">**V**视图：应用程序用于动态生成 HTML 响应的模板文件。</span><span class="sxs-lookup"><span data-stu-id="1cf2b-112">**V** iews: Template files that your application uses to dynamically generate HTML responses.</span></span>
- <span data-ttu-id="1cf2b-113">**C**控制器：用于处理传入浏览器请求、检索模型数据，然后指定将响应返回到浏览器的视图模板的类。</span><span class="sxs-lookup"><span data-stu-id="1cf2b-113">**C** ontrollers: Classes that handle incoming browser requests, retrieve model data, and then specify view templates that return a response to the browser.</span></span>

<span data-ttu-id="1cf2b-114">我们将在本系列教程中介绍所有这些概念，并向您演示如何使用它们来生成应用程序。</span><span class="sxs-lookup"><span data-stu-id="1cf2b-114">We'll be covering all these concepts in this tutorial series and show you how to use them to build an application.</span></span>

<span data-ttu-id="1cf2b-115">首先，让我们创建一个控制器类。</span><span class="sxs-lookup"><span data-stu-id="1cf2b-115">Let's begin by creating a controller class.</span></span> <span data-ttu-id="1cf2b-116">在**解决方案资源管理器**中，右键单击 "*控制器*" 文件夹，然后选择 "**添加控制器**"。</span><span class="sxs-lookup"><span data-stu-id="1cf2b-116">In **Solution Explorer**, right-click the *Controllers* folder and then select **Add Controller**.</span></span>

![](adding-a-controller/_static/image1.png)

<span data-ttu-id="1cf2b-117">将新控制器命名 &quot;HelloWorldController&quot;。</span><span class="sxs-lookup"><span data-stu-id="1cf2b-117">Name your new controller &quot;HelloWorldController&quot;.</span></span> <span data-ttu-id="1cf2b-118">保留默认模板为**空 MVC 控制器**，并单击 "**添加**"。</span><span class="sxs-lookup"><span data-stu-id="1cf2b-118">Leave the default template as **Empty MVC controller** and click **Add**.</span></span>

![添加控制器](adding-a-controller/_static/image2.png)

<span data-ttu-id="1cf2b-120">请注意，**解决方案资源管理器**已创建名为*HelloWorldController.cs*的新文件。</span><span class="sxs-lookup"><span data-stu-id="1cf2b-120">Notice in **Solution Explorer** that a new file has been created named *HelloWorldController.cs*.</span></span> <span data-ttu-id="1cf2b-121">文件在 IDE 中处于打开状态。</span><span class="sxs-lookup"><span data-stu-id="1cf2b-121">The file is open in the IDE.</span></span>

![](adding-a-controller/_static/image3.png)

<span data-ttu-id="1cf2b-122">将文件的内容替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="1cf2b-122">Replace the contents of the file with the following code.</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample1.cs)]

<span data-ttu-id="1cf2b-123">控制器方法将以 HTML 形式返回一个字符串作为示例。</span><span class="sxs-lookup"><span data-stu-id="1cf2b-123">The controller methods will return a string of HTML as an example.</span></span> <span data-ttu-id="1cf2b-124">控制器名为 `HelloWorldController`，上面的第一个方法名为 `Index`。</span><span class="sxs-lookup"><span data-stu-id="1cf2b-124">The controller is named `HelloWorldController` and the first method above is named `Index`.</span></span> <span data-ttu-id="1cf2b-125">让我们从浏览器中调用它。</span><span class="sxs-lookup"><span data-stu-id="1cf2b-125">Let's invoke it from a browser.</span></span> <span data-ttu-id="1cf2b-126">运行应用程序（按 F5 或 Ctrl + F5）。</span><span class="sxs-lookup"><span data-stu-id="1cf2b-126">Run the application (press F5 or Ctrl+F5).</span></span> <span data-ttu-id="1cf2b-127">在浏览器中，将 &quot;HelloWorld&quot; 追加到地址栏中的路径。</span><span class="sxs-lookup"><span data-stu-id="1cf2b-127">In the browser, append &quot;HelloWorld&quot; to the path in the address bar.</span></span> <span data-ttu-id="1cf2b-128">（例如，在下图中，它 `http://localhost:1234/HelloWorld.`）浏览器中的页面将类似于以下屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="1cf2b-128">(For example, in the illustration below, it's `http://localhost:1234/HelloWorld.`) The page in the browser will look like the following screenshot.</span></span> <span data-ttu-id="1cf2b-129">在上面的方法中，代码直接返回了一个字符串。</span><span class="sxs-lookup"><span data-stu-id="1cf2b-129">In the method above, the code returned a string directly.</span></span> <span data-ttu-id="1cf2b-130">你已告诉系统只返回了一些 HTML，但确实返回了！</span><span class="sxs-lookup"><span data-stu-id="1cf2b-130">You told the system to just return some HTML, and it did!</span></span>

![](adding-a-controller/_static/image4.png)

<span data-ttu-id="1cf2b-131">ASP.NET MVC 根据传入 URL 调用不同的控制器类（以及其中的不同操作方法）。</span><span class="sxs-lookup"><span data-stu-id="1cf2b-131">ASP.NET MVC invokes different controller classes (and different action methods within them) depending on the incoming URL.</span></span> <span data-ttu-id="1cf2b-132">ASP.NET MVC 使用的默认 URL 路由逻辑使用如下格式来确定要调用的代码：</span><span class="sxs-lookup"><span data-stu-id="1cf2b-132">The default URL routing logic used by ASP.NET MVC uses a format like this to determine what code to invoke:</span></span>

`/[Controller]/[ActionName]/[Parameters]`

<span data-ttu-id="1cf2b-133">URL 的第一部分确定要执行的控制器类。</span><span class="sxs-lookup"><span data-stu-id="1cf2b-133">The first part of the URL determines the controller class to execute.</span></span> <span data-ttu-id="1cf2b-134">因此， */HelloWorld*映射到 `HelloWorldController` 类。</span><span class="sxs-lookup"><span data-stu-id="1cf2b-134">So */HelloWorld* maps to the `HelloWorldController` class.</span></span> <span data-ttu-id="1cf2b-135">URL 的第二部分确定要执行的类的操作方法。</span><span class="sxs-lookup"><span data-stu-id="1cf2b-135">The second part of the URL determines the action method on the class to execute.</span></span> <span data-ttu-id="1cf2b-136">因此， */HelloWorld/Index*将导致执行 `HelloWorldController` 类的 `Index` 方法。</span><span class="sxs-lookup"><span data-stu-id="1cf2b-136">So */HelloWorld/Index* would cause the `Index` method of the `HelloWorldController` class to execute.</span></span> <span data-ttu-id="1cf2b-137">请注意，我们只需要浏览到 */HelloWorld* ，并且默认使用 `Index` 方法。</span><span class="sxs-lookup"><span data-stu-id="1cf2b-137">Notice that we only had to browse to */HelloWorld* and the `Index` method was used by default.</span></span> <span data-ttu-id="1cf2b-138">这是因为，名为 `Index` 的方法是将在控制器上调用的默认方法，如果未显式指定一个方法。</span><span class="sxs-lookup"><span data-stu-id="1cf2b-138">This is because a method named `Index` is the default method that will be called on a controller if one is not explicitly specified.</span></span>

<span data-ttu-id="1cf2b-139">浏览到 `http://localhost:xxxx/HelloWorld/Welcome`。</span><span class="sxs-lookup"><span data-stu-id="1cf2b-139">Browse to `http://localhost:xxxx/HelloWorld/Welcome`.</span></span> <span data-ttu-id="1cf2b-140">`Welcome` 方法将运行并返回字符串 &quot;这是欢迎操作方法 ...&quot;。</span><span class="sxs-lookup"><span data-stu-id="1cf2b-140">The `Welcome` method runs and returns the string &quot;This is the Welcome action method...&quot;.</span></span> <span data-ttu-id="1cf2b-141">默认 MVC 映射 `/[Controller]/[ActionName]/[Parameters]`。</span><span class="sxs-lookup"><span data-stu-id="1cf2b-141">The default MVC mapping is `/[Controller]/[ActionName]/[Parameters]`.</span></span> <span data-ttu-id="1cf2b-142">对于此 URL，采用 `HelloWorld` 控制器和 `Welcome` 操作方法。</span><span class="sxs-lookup"><span data-stu-id="1cf2b-142">For this URL, the controller is `HelloWorld` and `Welcome` is the action method.</span></span> <span data-ttu-id="1cf2b-143">目前尚未使用 URL 的 `[Parameters]` 部分。</span><span class="sxs-lookup"><span data-stu-id="1cf2b-143">You haven't used the `[Parameters]` part of the URL yet.</span></span>

![](adding-a-controller/_static/image5.png)

<span data-ttu-id="1cf2b-144">让我们略微修改示例，以便可以将一些参数信息从 URL 传递到控制器（例如， */HelloWorld/Welcome？ name = Scott&amp;numtimes = 4*）。</span><span class="sxs-lookup"><span data-stu-id="1cf2b-144">Let's modify the example slightly so that you can pass some parameter information from the URL to the controller (for example, */HelloWorld/Welcome?name=Scott&amp;numtimes=4*).</span></span> <span data-ttu-id="1cf2b-145">将 `Welcome` 方法更改为包含两个参数，如下所示。</span><span class="sxs-lookup"><span data-stu-id="1cf2b-145">Change your `Welcome` method to include two parameters as shown below.</span></span> <span data-ttu-id="1cf2b-146">请注意，该代码使用C#可选的参数功能，指示如果没有为该参数传递值，则 `numTimes` 参数应默认为1。</span><span class="sxs-lookup"><span data-stu-id="1cf2b-146">Note that the code uses the C# optional-parameter feature to indicate that the `numTimes` parameter should default to 1 if no value is passed for that parameter.</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample2.cs)]

<span data-ttu-id="1cf2b-147">运行应用程序并浏览到示例 URL （`http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4)`。</span><span class="sxs-lookup"><span data-stu-id="1cf2b-147">Run your application and browse to the example URL (`http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4)`.</span></span> <span data-ttu-id="1cf2b-148">可在 URL 中对 `name` 和 `numtimes` 使用其他值。</span><span class="sxs-lookup"><span data-stu-id="1cf2b-148">You can try different values for `name` and `numtimes` in the URL.</span></span> <span data-ttu-id="1cf2b-149">[ASP.NET MVC 模型绑定系统](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx)自动将命名参数从地址栏中的查询字符串映射到方法中的参数。</span><span class="sxs-lookup"><span data-stu-id="1cf2b-149">The [ASP.NET MVC model binding system](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx) automatically maps the named parameters from the query string in the address bar to parameters in your method.</span></span>

![](adding-a-controller/_static/image6.png)

<span data-ttu-id="1cf2b-150">在这两个示例中，控制器都在 &quot;的 VC&quot; 部分，即视图和控制器工作。</span><span class="sxs-lookup"><span data-stu-id="1cf2b-150">In both these examples the controller has been doing the &quot;VC&quot; portion of MVC — that is, the view and controller work.</span></span> <span data-ttu-id="1cf2b-151">控制器将直接返回 HTML。</span><span class="sxs-lookup"><span data-stu-id="1cf2b-151">The controller is returning HTML directly.</span></span> <span data-ttu-id="1cf2b-152">通常情况下，你不希望控制器直接返回 HTML，因为这会对代码非常麻烦。</span><span class="sxs-lookup"><span data-stu-id="1cf2b-152">Ordinarily you don't want controllers returning HTML directly, since that becomes very cumbersome to code.</span></span> <span data-ttu-id="1cf2b-153">我们通常会使用单独的视图模板文件来帮助生成 HTML 响应。</span><span class="sxs-lookup"><span data-stu-id="1cf2b-153">Instead we'll typically use a separate view template file to help generate the HTML response.</span></span> <span data-ttu-id="1cf2b-154">接下来，我们来看看如何实现此目的。</span><span class="sxs-lookup"><span data-stu-id="1cf2b-154">Let's look next at how we can do this.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="1cf2b-155">[上一页](intro-to-aspnet-mvc-4.md)
> [下一页](adding-a-view.md)</span><span class="sxs-lookup"><span data-stu-id="1cf2b-155">[Previous](intro-to-aspnet-mvc-4.md)
[Next](adding-a-view.md)</span></span>

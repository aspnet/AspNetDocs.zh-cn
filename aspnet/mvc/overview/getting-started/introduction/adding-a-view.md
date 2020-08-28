---
title: 将视图添加到 MVC 应用
author: Rick-Anderson
description: 将视图添加到 MVC 应用
ms.author: riande
ms.date: 01/23/2019
uid: mvc/overview/getting-started/introduction/adding-a-view
ms.openlocfilehash: b8400036cc689d3cd2fec54b3191252d296ade41
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045008"
---
# <a name="adding-a-view"></a><span data-ttu-id="41a6b-103">添加视图</span><span class="sxs-lookup"><span data-stu-id="41a6b-103">Adding a View</span></span>

<span data-ttu-id="41a6b-104">作者： [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="41a6b-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[!INCLUDE [consider RP](~/includes/razor.md)]

<span data-ttu-id="41a6b-105">在本部分中，您将修改 `HelloWorldController` 类以使用视图模板文件来将生成 HTML 响应的过程清晰地封装到客户端。</span><span class="sxs-lookup"><span data-stu-id="41a6b-105">In this section you're going to modify the `HelloWorldController` class to use view template files to cleanly encapsulate the process of generating HTML responses to a client.</span></span> 

<span data-ttu-id="41a6b-106">使用 [Razor 视图引擎](../../../../web-pages/overview/getting-started/introducing-razor-syntax-c.md)可以创建视图模板文件。</span><span class="sxs-lookup"><span data-stu-id="41a6b-106">You'll create a view template file using the [Razor view engine](../../../../web-pages/overview/getting-started/introducing-razor-syntax-c.md).</span></span> <span data-ttu-id="41a6b-107">基于 Razor 的视图模板的文件扩展名为 *cshtml* ，并提供使用 c # 创建 HTML 输出的简洁方法。</span><span class="sxs-lookup"><span data-stu-id="41a6b-107">Razor-based view templates have a *.cshtml* file extension, and provide an elegant way to create HTML output using C#.</span></span> <span data-ttu-id="41a6b-108">Razor 最大程度地减少了编写视图模板时所需的字符和击键数量，并启用了快速、流畅的编码工作流。</span><span class="sxs-lookup"><span data-stu-id="41a6b-108">Razor minimizes the number of characters and keystrokes required when writing a view template, and enables a fast, fluid coding workflow.</span></span>

<span data-ttu-id="41a6b-109">当前，`Index` 方法返回带有在控制器类中硬编码的消息的字符串。</span><span class="sxs-lookup"><span data-stu-id="41a6b-109">Currently the `Index` method returns a string with a message that is hard-coded in the controller class.</span></span> <span data-ttu-id="41a6b-110">更改 `Index` 方法以调用控制器 [视图](/dotnet/api/microsoft.aspnetcore.mvc.controller.view#Microsoft_AspNetCore_Mvc_Controller_View) 方法，如以下代码所示：</span><span class="sxs-lookup"><span data-stu-id="41a6b-110">Change the `Index` method to call the controllers [View](/dotnet/api/microsoft.aspnetcore.mvc.controller.view#Microsoft_AspNetCore_Mvc_Controller_View) method, as shown in the following code:</span></span>

[!code-csharp[Main](adding-a-view/samples/sample1.cs?highlight=1,3)]

<span data-ttu-id="41a6b-111">`Index`上面的方法使用视图模板生成浏览器的 HTML 响应。</span><span class="sxs-lookup"><span data-stu-id="41a6b-111">The `Index` method above uses a view template to generate an HTML response to the browser.</span></span> <span data-ttu-id="41a6b-112">控制器方法 (也称为 [操作方法](http://rachelappel.com/asp.net-mvc-actionresults-explained)) （如 `Index` 上面的方法）通常返回 [ActionResult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx) (或派生自 [ActionResult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx)) 的类，而不是字符串等基元类型。</span><span class="sxs-lookup"><span data-stu-id="41a6b-112">Controller methods (also known as [action methods](http://rachelappel.com/asp.net-mvc-actionresults-explained)), such as the `Index` method above, generally return an [ActionResult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx) (or a class derived from [ActionResult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx)), not primitive types like string.</span></span>

<span data-ttu-id="41a6b-113">右键单击 *Views\HelloWorld* 文件夹，然后单击 " **添加**"，然后单击 " \*\* (Razor) 的布局" 的 "MVC 5 视图页 \*\*"。</span><span class="sxs-lookup"><span data-stu-id="41a6b-113">Right click the *Views\HelloWorld* folder and click **Add**, then click **MVC 5 View Page with Layout (Razor)**.</span></span>
  
![](adding-a-view/_static/image1.png)   
  
<span data-ttu-id="41a6b-114">在 " **指定项目的名称** " 对话框中，输入 *Index*，然后单击 **"确定"**。</span><span class="sxs-lookup"><span data-stu-id="41a6b-114">In the **Specify Name for Item** dialog box, enter *Index*, and then click **OK**.</span></span>  
  
![](adding-a-view/_static/image2.png)  
  
<span data-ttu-id="41a6b-115">在 "**选择布局页**" 对话框中，接受默认的\*\* \_ 布局 Cshtml\*\* ，然后单击 **"确定"**。</span><span class="sxs-lookup"><span data-stu-id="41a6b-115">In the **Select a Layout Page** dialog, accept the default **\_Layout.cshtml** and click **OK**.</span></span>  
  
![](adding-a-view/_static/image3.png)  
  
<span data-ttu-id="41a6b-116">在上面的对话框中，在左窗格中选择了 " *Views\Shared* " 文件夹。</span><span class="sxs-lookup"><span data-stu-id="41a6b-116">In the dialog above, the *Views\Shared* folder is selected in the left pane.</span></span> <span data-ttu-id="41a6b-117">如果在其他文件夹中有自定义的布局文件，则可以选择它。</span><span class="sxs-lookup"><span data-stu-id="41a6b-117">If you had a custom layout file in another folder, you could select it.</span></span> <span data-ttu-id="41a6b-118">我们稍后将在本教程中讨论布局文件</span><span class="sxs-lookup"><span data-stu-id="41a6b-118">We'll talk about the layout file later in the tutorial</span></span>

<span data-ttu-id="41a6b-119">将创建 *MvcMovie\Views\HelloWorld\Index.cshtml* 文件。</span><span class="sxs-lookup"><span data-stu-id="41a6b-119">The *MvcMovie\Views\HelloWorld\Index.cshtml* file is created.</span></span>

![](adding-a-view/_static/image4.png)

<span data-ttu-id="41a6b-120">添加以下突出显示的标记。</span><span class="sxs-lookup"><span data-stu-id="41a6b-120">Add the following highlighted markup.</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample2.cshtml?highlight=4-11)]

<span data-ttu-id="41a6b-121">右键单击该 *索引的 cshtml* 文件，然后选择 **"在浏览器中查看"**。</span><span class="sxs-lookup"><span data-stu-id="41a6b-121">Right click the *Index.cshtml* file and select **View in Browser**.</span></span>

![PI](adding-a-view/_static/image5.png)

<span data-ttu-id="41a6b-123">您还可以右键单击该 *索引的 cshtml* 文件，然后 **在 Page Inspector 中选择 "查看"。**</span><span class="sxs-lookup"><span data-stu-id="41a6b-123">You can also right click the *Index.cshtml* file and select **View in Page Inspector.**</span></span> <span data-ttu-id="41a6b-124">有关详细信息，请参阅 [Page Inspector 教程](../../views/using-page-inspector-in-aspnet-mvc.md) 。</span><span class="sxs-lookup"><span data-stu-id="41a6b-124">See the [Page Inspector tutorial](../../views/using-page-inspector-in-aspnet-mvc.md) for more information.</span></span>

<span data-ttu-id="41a6b-125">或者，运行应用程序并浏览到 `HelloWorld` 控制器 (`http://localhost:xxxx/HelloWorld`) 。</span><span class="sxs-lookup"><span data-stu-id="41a6b-125">Alternatively, run the application and browse to the `HelloWorld` controller (`http://localhost:xxxx/HelloWorld`).</span></span> <span data-ttu-id="41a6b-126">`Index`控制器中的方法不做很多工作; 它只是运行了语句，该语句 `return View()` 指定方法应使用视图模板文件来呈现对浏览器的响应。</span><span class="sxs-lookup"><span data-stu-id="41a6b-126">The `Index` method in your controller didn't do much work; it simply ran the statement `return View()`, which specified that the method should use a view template file to render a response to the browser.</span></span> <span data-ttu-id="41a6b-127">由于未显式指定要使用的视图模板文件的名称，因此 ASP.NET MVC 默认使用*\Views\HelloWorld*文件夹中的*视图文件。*</span><span class="sxs-lookup"><span data-stu-id="41a6b-127">Because you didn't explicitly specify the name of the view template file to use, ASP.NET MVC defaulted to using the *Index.cshtml* view file in the *\Views\HelloWorld* folder.</span></span> <span data-ttu-id="41a6b-128">下图显示了视图 &quot; 模板中的字符串 Hello！ &quot; 在视图中进行了硬编码。</span><span class="sxs-lookup"><span data-stu-id="41a6b-128">The image below shows the string &quot;Hello from our View Template!&quot; hard-coded in the view.</span></span>

![](adding-a-view/_static/image6.png)

<span data-ttu-id="41a6b-129">看起来不错。</span><span class="sxs-lookup"><span data-stu-id="41a6b-129">Looks pretty good.</span></span> <span data-ttu-id="41a6b-130">但请注意，浏览器的标题栏显示 "Index-My ASP.NET 应用程序"，页面顶部的大链接显示 "应用程序名称"。</span><span class="sxs-lookup"><span data-stu-id="41a6b-130">However, notice that the browser's title bar shows "Index - My ASP.NET Application," and the big link at the top of the page says "Application name."</span></span> <span data-ttu-id="41a6b-131">根据浏览器窗口的大小，可能需要单击右上角的三个栏才能看到 " **主页**"、" **关于**"、" **联系人**"、" **注册** " 和 **"登录** " 链接。</span><span class="sxs-lookup"><span data-stu-id="41a6b-131">Depending on how small you make your browser window, you might need to click the three bars in the upper right to see the to the **Home**, **About**, **Contact**, **Register** and **Log in** links.</span></span>

## <a name="changing-views-and-layout-pages"></a><span data-ttu-id="41a6b-132">更改视图和布局页</span><span class="sxs-lookup"><span data-stu-id="41a6b-132">Changing Views and Layout Pages</span></span>

<span data-ttu-id="41a6b-133">首先，您需要更改 &quot; 页面顶部的 "应用程序名称" &quot; 链接。</span><span class="sxs-lookup"><span data-stu-id="41a6b-133">First, you want to change the &quot;Application name&quot; link at the top of the page.</span></span> <span data-ttu-id="41a6b-134">该文本对于每个页面都是通用的。</span><span class="sxs-lookup"><span data-stu-id="41a6b-134">That text is common to every page.</span></span> <span data-ttu-id="41a6b-135">它实际上只在项目中的一个位置实现，即使它显示在应用程序的每一页上也是如此。</span><span class="sxs-lookup"><span data-stu-id="41a6b-135">It's actually implemented in only one place in the project, even though it appears on every page in the application.</span></span> <span data-ttu-id="41a6b-136">中转到**解决方案资源管理器**中的 */Views/Shared*文件夹，然后打开 " \* \_ Layout\* " 文件。</span><span class="sxs-lookup"><span data-stu-id="41a6b-136">Go to the */Views/Shared* folder in **Solution Explorer** and open the *\_Layout.cshtml* file.</span></span> <span data-ttu-id="41a6b-137">此文件称为 *布局页面* ，位于所有其他页面都使用的共享文件夹中。</span><span class="sxs-lookup"><span data-stu-id="41a6b-137">This file is called a *layout page* and it's in the shared folder that all other pages use.</span></span>

![_LayoutCshtml](adding-a-view/_static/image7.png)

<span data-ttu-id="41a6b-139">布局模板使你能够在一个位置指定网站的 HTML 容器布局，然后将它应用到网站中的多个页面。</span><span class="sxs-lookup"><span data-stu-id="41a6b-139">Layout templates allow you to specify the HTML container layout of your site in one place and then apply it across multiple pages in your site.</span></span> <span data-ttu-id="41a6b-140">查找 `@RenderBody()` 行。</span><span class="sxs-lookup"><span data-stu-id="41a6b-140">Find the `@RenderBody()` line.</span></span> <span data-ttu-id="41a6b-141">`RenderBody` 是显示创建的所有特定于视图的页面的占位符，已包装在布局页面中&quot;&quot;。</span><span class="sxs-lookup"><span data-stu-id="41a6b-141">`RenderBody` is a placeholder where all the view-specific pages you create show up, &quot;wrapped&quot; in the layout page.</span></span> <span data-ttu-id="41a6b-142">例如，如果选择 " **关于** " 链接，则会在方法中呈现 *Views\Home\About.cshtml* 视图 `RenderBody` 。</span><span class="sxs-lookup"><span data-stu-id="41a6b-142">For example, if you select the **About** link, the *Views\Home\About.cshtml* view is rendered inside the `RenderBody` method.</span></span>

<span data-ttu-id="41a6b-143">更改标题元素的内容。</span><span class="sxs-lookup"><span data-stu-id="41a6b-143">Change the contents of the title element.</span></span> <span data-ttu-id="41a6b-144">将布局模板中的 [html.actionlink](https://msdn.microsoft.com/library/dd504972(v=vs.108).aspx) 从 &quot; 应用程序名称更改 &quot; 为 &quot; MVC 电影 &quot; ，并将控制器从更改 `Home` 为 `Movies` 。</span><span class="sxs-lookup"><span data-stu-id="41a6b-144">Change the [ActionLink](https://msdn.microsoft.com/library/dd504972(v=vs.108).aspx) in the layout template from &quot;Application name&quot; to &quot;MVC Movie&quot; and the controller from `Home` to `Movies`.</span></span> <span data-ttu-id="41a6b-145">完整的布局文件如下所示：</span><span class="sxs-lookup"><span data-stu-id="41a6b-145">The complete layout file is shown below:</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample3.cshtml?highlight=6,20)]

<span data-ttu-id="41a6b-146">运行该应用程序，请注意，它现在显示 &quot; MVC 电影 &quot; 。</span><span class="sxs-lookup"><span data-stu-id="41a6b-146">Run the application and notice that it now says &quot;MVC Movie &quot;.</span></span> <span data-ttu-id="41a6b-147">单击 " **关于** " 链接，你将看到该页面也会显示 &quot; MVC 电影 &quot; 。</span><span class="sxs-lookup"><span data-stu-id="41a6b-147">Click the **About** link, and you see how that page shows &quot;MVC Movie&quot;, too.</span></span> <span data-ttu-id="41a6b-148">我们能够在布局模板中进行一次更改，并让网站上的所有页面都反映新标题。</span><span class="sxs-lookup"><span data-stu-id="41a6b-148">We were able to make the change once in the layout template and have all pages on the site reflect the new title.</span></span>

![](adding-a-view/_static/image8.png)

<span data-ttu-id="41a6b-149">首次创建 *Views\HelloWorld\Index.cshtml* 文件时，它包含以下代码：</span><span class="sxs-lookup"><span data-stu-id="41a6b-149">When we first created the *Views\HelloWorld\Index.cshtml* file, it contained the following code:</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample4.cshtml)]

<span data-ttu-id="41a6b-150">上述 Razor 代码显式设置布局页。</span><span class="sxs-lookup"><span data-stu-id="41a6b-150">The Razor code above is explicitly setting the layout page.</span></span> <span data-ttu-id="41a6b-151">检查 \* \\ _ViewStart cshtml\* 文件的视图，它包含的 Razor 标记完全相同。</span><span class="sxs-lookup"><span data-stu-id="41a6b-151">Examine the *Views\\_ViewStart.cshtml* file, it contains the exact same Razor markup.</span></span> <span data-ttu-id="41a6b-152">*[视图 \\ _ViewStart 的视图](https://weblogs.asp.net/scottgu/archive/2010/10/22/asp-net-mvc-3-layouts.aspx)* 用于定义所有视图都将使用的通用布局，因此你可以从*Views\HelloWorld\Index.cshtml*文件中注释掉或删除该代码。</span><span class="sxs-lookup"><span data-stu-id="41a6b-152">The *[Views\\_ViewStart.cshtml](https://weblogs.asp.net/scottgu/archive/2010/10/22/asp-net-mvc-3-layouts.aspx)* file defines the common layout that all views will use, therefore you can comment out or remove that code from the *Views\HelloWorld\Index.cshtml* file.</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample5.cshtml?highlight=1-3)]

<span data-ttu-id="41a6b-153">可以使用 `Layout` 属性设置不同的布局视图，或将它设置为 `null`，这样将不会使用任何布局文件。</span><span class="sxs-lookup"><span data-stu-id="41a6b-153">You can use the `Layout` property to set a different layout view, or set it to `null` so no layout file will be used.</span></span>

<span data-ttu-id="41a6b-154">现在，让我们更改索引视图的标题。</span><span class="sxs-lookup"><span data-stu-id="41a6b-154">Now, let's change the title of the Index view.</span></span>

<span data-ttu-id="41a6b-155">打开 *MvcMovie\Views\HelloWorld\Index.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="41a6b-155">Open *MvcMovie\Views\HelloWorld\Index.cshtml*.</span></span> <span data-ttu-id="41a6b-156">有两个位置可进行更改：第一项是在浏览器标题中显示的文本，然后在辅助标题中 (`<h2>` 元素) 。</span><span class="sxs-lookup"><span data-stu-id="41a6b-156">There are two places to make a change: first, the text that appears in the title of the browser, and then in the secondary header (the `<h2>` element).</span></span> <span data-ttu-id="41a6b-157">稍稍对它们进行一些更改，这样可以看出哪一段代码更改了应用的哪部分。</span><span class="sxs-lookup"><span data-stu-id="41a6b-157">You'll make them slightly different so you can see which bit of code changes which part of the app.</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample6.cshtml?highlight=2,5)]

<span data-ttu-id="41a6b-158">若要指示要显示的 HTML 标题，以上代码将设置 `Title` `ViewBag` (的对象的属性，该对象位于*Index.cshtml*) 的</span><span class="sxs-lookup"><span data-stu-id="41a6b-158">To indicate the HTML title to display, the code above sets a `Title` property of the `ViewBag` object (which is in the *Index.cshtml* view template).</span></span> <span data-ttu-id="41a6b-159">请注意，布局模板 ( *Views\Shared \\ _Layout* ) 将此值 `<title>` 作为 `<head>` 之前修改的 HTML 部分的一部分使用。</span><span class="sxs-lookup"><span data-stu-id="41a6b-159">Notice that the layout template ( *Views\Shared\\_Layout.cshtml* ) uses this value in the `<title>` element as part of the `<head>` section of the HTML that we modified previously.</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample7.cshtml?highlight=6)]

<span data-ttu-id="41a6b-160">使用此 `ViewBag` 方法，您可以轻松地在视图模板和布局文件之间传递其他参数。</span><span class="sxs-lookup"><span data-stu-id="41a6b-160">Using this `ViewBag` approach, you can easily pass other parameters between your view template and your layout file.</span></span>

<span data-ttu-id="41a6b-161">运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="41a6b-161">Run the application.</span></span> <span data-ttu-id="41a6b-162">请注意，浏览器标题、主标题和辅助标题已更改。</span><span class="sxs-lookup"><span data-stu-id="41a6b-162">Notice that the browser title, the primary heading, and the secondary headings have changed.</span></span> <span data-ttu-id="41a6b-163">（如果没有在浏览器中看到更改，则可能正在查看缓存的内容。</span><span class="sxs-lookup"><span data-stu-id="41a6b-163">(If you don't see changes in the browser, you might be viewing cached content.</span></span> <span data-ttu-id="41a6b-164">在浏览器中按 Ctrl + F5 来强制加载来自服务器的响应。 ) 浏览器标题是通过在 `ViewBag.Title` *Index. cshtml*视图模板中设置的，以及在布局文件中添加的附加 &quot; 电影应用来创建的。 &quot;</span><span class="sxs-lookup"><span data-stu-id="41a6b-164">Press Ctrl+F5 in your browser to force the response from the server to be loaded.) The browser title is created with the `ViewBag.Title` we set in the *Index.cshtml* view template and the additional &quot;- Movie App&quot; added in the layout file.</span></span>

<span data-ttu-id="41a6b-165">另请注意， *Index.* view 模板中的内容如何与\* \_ Layout\*视图模板合并，并向浏览器发送单个 HTML 响应。</span><span class="sxs-lookup"><span data-stu-id="41a6b-165">Also notice how the content in the *Index.cshtml* view template was merged with the *\_Layout.cshtml* view template and a single HTML response was sent to the browser.</span></span> <span data-ttu-id="41a6b-166">凭借布局模板可以很容易地对应用程序中所有页面进行更改。</span><span class="sxs-lookup"><span data-stu-id="41a6b-166">Layout templates make it really easy to make changes that apply across all of the pages in your application.</span></span>

![](adding-a-view/_static/image9.png)

<span data-ttu-id="41a6b-167">&quot; &quot; 在这种情况下，我们的一些数据 (在这种情况下 &quot; ，我们的视图模板中的 Hello！ &quot; 消息) 是硬编码的。</span><span class="sxs-lookup"><span data-stu-id="41a6b-167">Our little bit of &quot;data&quot; (in this case the &quot;Hello from our View Template!&quot; message) is hard-coded, though.</span></span> <span data-ttu-id="41a6b-168">MVC 应用程序具有一个 &quot; &quot; (视图) ，并且您有一个 &quot; C &quot; (控制器) ，但没有 (&quot; &quot;) 模型。</span><span class="sxs-lookup"><span data-stu-id="41a6b-168">The MVC application has a &quot;V&quot; (view) and you've got a &quot;C&quot; (controller), but no &quot;M&quot; (model) yet.</span></span> <span data-ttu-id="41a6b-169">稍后，我们将演练如何创建数据库并从中检索模型数据。</span><span class="sxs-lookup"><span data-stu-id="41a6b-169">Shortly, we'll walk through how to create a database and retrieve model data from it.</span></span>

## <a name="passing-data-from-the-controller-to-the-view"></a><span data-ttu-id="41a6b-170">将数据从控制器传递给视图</span><span class="sxs-lookup"><span data-stu-id="41a6b-170">Passing Data from the Controller to the View</span></span>

<span data-ttu-id="41a6b-171">不过，在开始使用数据库并讨论模型之前，首先请讨论将信息从控制器传递到视图。</span><span class="sxs-lookup"><span data-stu-id="41a6b-171">Before we go to a database and talk about models, though, let's first talk about passing information from the controller to a view.</span></span> <span data-ttu-id="41a6b-172">为了响应传入 URL 请求，将调用控制器类。</span><span class="sxs-lookup"><span data-stu-id="41a6b-172">Controller classes are invoked in response to an incoming URL request.</span></span> <span data-ttu-id="41a6b-173">通过控制器类，您可以编写处理传入浏览器请求的代码，从数据库中检索数据，并最终决定要发送回浏览器的响应类型。</span><span class="sxs-lookup"><span data-stu-id="41a6b-173">A controller class is where you write the code that handles the incoming browser requests, retrieves data from a database, and ultimately decides what type of response to send back to the browser.</span></span> <span data-ttu-id="41a6b-174">然后，可以从控制器使用视图模板来生成 HTML 响应并设置其格式。</span><span class="sxs-lookup"><span data-stu-id="41a6b-174">View templates can then be used from a controller to generate and format an HTML response to the browser.</span></span>

<span data-ttu-id="41a6b-175">控制器负责提供所需的任何数据或对象，以便视图模板呈现对浏览器的响应。</span><span class="sxs-lookup"><span data-stu-id="41a6b-175">Controllers are responsible for providing whatever data or objects are required in order for a view template to render a response to the browser.</span></span> <span data-ttu-id="41a6b-176">最佳做法： **视图模板不应执行业务逻辑或直接与数据库交互**。</span><span class="sxs-lookup"><span data-stu-id="41a6b-176">A best practice: **A view template should never perform business logic or interact with a database directly**.</span></span> <span data-ttu-id="41a6b-177">相反，视图模板应仅适用于控制器为其提供的数据。</span><span class="sxs-lookup"><span data-stu-id="41a6b-177">Instead, a view template should work only with the data that's provided to it by the controller.</span></span> <span data-ttu-id="41a6b-178">维护这 &quot; 一问题分离 &quot; 有助于使你的代码更干净、可测试、更易于维护。</span><span class="sxs-lookup"><span data-stu-id="41a6b-178">Maintaining this &quot;separation of concerns&quot; helps keep your code clean, testable and more maintainable.</span></span>

<span data-ttu-id="41a6b-179">目前， `Welcome` 类中的操作方法 `HelloWorldController` 采用 `name` 和 `numTimes` 参数，然后将值直接输出到浏览器。</span><span class="sxs-lookup"><span data-stu-id="41a6b-179">Currently, the `Welcome` action method in the `HelloWorldController` class takes a `name` and a `numTimes` parameter and then outputs the values directly to the browser.</span></span> <span data-ttu-id="41a6b-180">不要让控制器将此响应呈现为字符串，而是将控制器改为使用视图模板。</span><span class="sxs-lookup"><span data-stu-id="41a6b-180">Rather than have the controller render this response as a string, let's change the controller to use a view template instead.</span></span> <span data-ttu-id="41a6b-181">视图模板将生成动态响应，这意味着你需要将适当的数据位从控制器传递给视图以生成响应。</span><span class="sxs-lookup"><span data-stu-id="41a6b-181">The view template will generate a dynamic response, which means that you need to pass appropriate bits of data from the controller to the view in order to generate the response.</span></span> <span data-ttu-id="41a6b-182">为此，可以让控制器将动态数据 (参数) 在 `ViewBag` 视图模板可以访问的对象中的视图模板需要的参数。</span><span class="sxs-lookup"><span data-stu-id="41a6b-182">You can do this by having the controller put the dynamic data (parameters) that the view template needs in a `ViewBag` object that the view template can then access.</span></span>

<span data-ttu-id="41a6b-183">返回到 *HelloWorldController.cs* 文件，然后更改 `Welcome` 方法，将 `Message` 和值添加 `NumTimes` 到 `ViewBag` 对象。</span><span class="sxs-lookup"><span data-stu-id="41a6b-183">Return to the *HelloWorldController.cs* file and change the `Welcome` method to add a `Message` and `NumTimes` value to the `ViewBag` object.</span></span> <span data-ttu-id="41a6b-184">`ViewBag` 是动态对象，这意味着你可以将所需的任何内容放在其中;在 `ViewBag` 将对象放入其中之前，对象没有定义的属性。</span><span class="sxs-lookup"><span data-stu-id="41a6b-184">`ViewBag` is a dynamic object, which means you can put whatever you want in to it; the `ViewBag` object has no defined properties until you put something inside it.</span></span> <span data-ttu-id="41a6b-185">[ASP.NET MVC 模型绑定系统](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx)自动将命名参数 `name` `numTimes` 从地址栏中的查询字符串映射到方法中的参数 (和) 。</span><span class="sxs-lookup"><span data-stu-id="41a6b-185">The [ASP.NET MVC model binding system](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx) automatically maps the named parameters (`name` and `numTimes`) from the query string in the address bar to parameters in your method.</span></span> <span data-ttu-id="41a6b-186">完整的 HelloWorldController.cs 文件如下所示：</span><span class="sxs-lookup"><span data-stu-id="41a6b-186">The complete *HelloWorldController.cs* file looks like this:</span></span>

[!code-csharp[Main](adding-a-view/samples/sample8.cs)]

<span data-ttu-id="41a6b-187">现在， `ViewBag` 对象包含将自动传递到视图的数据。</span><span class="sxs-lookup"><span data-stu-id="41a6b-187">Now the `ViewBag` object contains data that will be passed to the view automatically.</span></span> <span data-ttu-id="41a6b-188">接下来，需要一个欢迎视图模板！</span><span class="sxs-lookup"><span data-stu-id="41a6b-188">Next, you need a Welcome view template!</span></span> <span data-ttu-id="41a6b-189">在 " **生成** " 菜单中，选择 " **生成解决方案** " (或按 Ctrl + Shift + B) 以确保编译项目。</span><span class="sxs-lookup"><span data-stu-id="41a6b-189">In the **Build** menu, select **Build Solution** (or Ctrl+Shift+B) to make sure the project is compiled.</span></span> <span data-ttu-id="41a6b-190">右键单击 *Views\HelloWorld* 文件夹，然后单击 " **添加**"，然后单击 " \*\* (Razor) 的布局" 的 "MVC 5 视图页 \*\*"。</span><span class="sxs-lookup"><span data-stu-id="41a6b-190">Right click the *Views\HelloWorld* folder and click **Add**, then click **MVC 5 View Page with Layout (Razor)**.</span></span>
  
![](adding-a-view/_static/image10.png)   
  
<span data-ttu-id="41a6b-191">在 " **指定项目的名称** " 对话框中，输入 " *欢迎*"，然后单击 **"确定"**。</span><span class="sxs-lookup"><span data-stu-id="41a6b-191">In the **Specify Name for Item** dialog box, enter *Welcome*, and then click **OK**.</span></span>   
  
<span data-ttu-id="41a6b-192">在 "**选择布局页**" 对话框中，接受默认的\*\* \_ 布局 Cshtml\*\* ，然后单击 **"确定"**。</span><span class="sxs-lookup"><span data-stu-id="41a6b-192">In the **Select a Layout Page** dialog, accept the default **\_Layout.cshtml** and click **OK**.</span></span>  
  
![](adding-a-view/_static/image11.png)   

<span data-ttu-id="41a6b-193">将创建 *MvcMovie\Views\HelloWorld\Welcome.cshtml* 文件。</span><span class="sxs-lookup"><span data-stu-id="41a6b-193">The *MvcMovie\Views\HelloWorld\Welcome.cshtml* file is created.</span></span>

<span data-ttu-id="41a6b-194">替换 *欢迎的 cshtml* 文件中的标记。</span><span class="sxs-lookup"><span data-stu-id="41a6b-194">Replace the markup in the *Welcome.cshtml* file.</span></span> <span data-ttu-id="41a6b-195">你将创建一个循环，该循环显示 &quot; &quot; 的是用户所应的时间。</span><span class="sxs-lookup"><span data-stu-id="41a6b-195">You'll create a loop that says &quot;Hello&quot; as many times as the user says it should.</span></span> <span data-ttu-id="41a6b-196">下面显示了完整的 *欢迎. cshtml* 文件。</span><span class="sxs-lookup"><span data-stu-id="41a6b-196">The complete *Welcome.cshtml* file is shown below.</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample9.cshtml)]

<span data-ttu-id="41a6b-197">运行应用程序并浏览到以下 URL：</span><span class="sxs-lookup"><span data-stu-id="41a6b-197">Run the application and browse to the following URL:</span></span>

`http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4`

<span data-ttu-id="41a6b-198">现在，数据是从 URL 获取的，并使用 [模型绑定](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx)器传递到控制器。</span><span class="sxs-lookup"><span data-stu-id="41a6b-198">Now data is taken from the URL and passed to the controller using the [model binder](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx).</span></span> <span data-ttu-id="41a6b-199">控制器将数据打包到一个 `ViewBag` 对象中，并将该对象传递给视图。</span><span class="sxs-lookup"><span data-stu-id="41a6b-199">The controller packages the data into a `ViewBag` object and passes that object to the view.</span></span> <span data-ttu-id="41a6b-200">然后，视图将以 HTML 格式向用户显示数据。</span><span class="sxs-lookup"><span data-stu-id="41a6b-200">The view then displays the data as HTML to the user.</span></span>

![](adding-a-view/_static/image12.png)

<span data-ttu-id="41a6b-201">在上面的示例中，我们使用 `ViewBag` 对象将数据从控制器传递到视图。</span><span class="sxs-lookup"><span data-stu-id="41a6b-201">In the sample above, we used a `ViewBag` object to pass data from the controller to a view.</span></span> <span data-ttu-id="41a6b-202">稍后在本教程中，我们将使用视图模型将数据从控制器传递给视图。</span><span class="sxs-lookup"><span data-stu-id="41a6b-202">Later in the tutorial, we will use a view model to pass data from a controller to a view.</span></span> <span data-ttu-id="41a6b-203">用于传递数据的视图模型方法通常比查看包方法更可取。</span><span class="sxs-lookup"><span data-stu-id="41a6b-203">The view model approach to passing data is generally much preferred over the view bag approach.</span></span> <span data-ttu-id="41a6b-204">有关详细信息，请参阅博客文章 [动态 V 强类型视图](https://blogs.msdn.com/b/rickandy/archive/2011/01/28/dynamic-v-strongly-typed-views.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="41a6b-204">See the blog entry [Dynamic V Strongly Typed Views](https://blogs.msdn.com/b/rickandy/archive/2011/01/28/dynamic-v-strongly-typed-views.aspx) for more information.</span></span> 

<span data-ttu-id="41a6b-205">这种情况下，这是 &quot; 模型的 M 类型 &quot; ，而不是数据库类型。</span><span class="sxs-lookup"><span data-stu-id="41a6b-205">Well, that was a kind of an &quot;M&quot; for model, but not the database kind.</span></span> <span data-ttu-id="41a6b-206">让我们用学到的内容来创建一个电影数据库。</span><span class="sxs-lookup"><span data-stu-id="41a6b-206">Let's take what we've learned and create a database of movies.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="41a6b-207">[上一页](adding-a-controller.md)
> [下一页](adding-a-model.md)</span><span class="sxs-lookup"><span data-stu-id="41a6b-207">[Previous](adding-a-controller.md)
[Next](adding-a-model.md)</span></span>

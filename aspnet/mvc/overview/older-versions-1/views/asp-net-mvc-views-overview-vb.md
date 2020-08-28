---
uid: mvc/overview/older-versions-1/views/asp-net-mvc-views-overview-vb
title: ASP.NET MVC 视图 (VB) 概述 |Microsoft Docs
author: StephenWalther
description: 什么是 ASP.NET MVC 视图，它与 HTML 页面有何不同？ 在本教程中，Stephen Walther 介绍了如何进行查看，并演示了如何
ms.author: riande
ms.date: 02/16/2008
ms.assetid: c28ba88d-3a93-47f5-a306-049bd766714d
msc.legacyurl: /mvc/overview/older-versions-1/views/asp-net-mvc-views-overview-vb
msc.type: authoredcontent
ms.openlocfilehash: a07d15cb14e9ef90b62c5a8702dee53f1a0a6032
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89044659"
---
# <a name="aspnet-mvc-views-overview-vb"></a><span data-ttu-id="d4406-104">ASP.NET MVC 视图概述 (VB)</span><span class="sxs-lookup"><span data-stu-id="d4406-104">ASP.NET MVC Views Overview (VB)</span></span>

<span data-ttu-id="d4406-105">作者： [Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="d4406-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="d4406-106">什么是 ASP.NET MVC 视图，它与 HTML 页面有何不同？</span><span class="sxs-lookup"><span data-stu-id="d4406-106">What is an ASP.NET MVC View and how does it differ from a HTML page?</span></span> <span data-ttu-id="d4406-107">在本教程中，Stephen Walther 介绍了如何在视图中利用查看数据和 HTML 帮助器。</span><span class="sxs-lookup"><span data-stu-id="d4406-107">In this tutorial, Stephen Walther introduces you to Views and demonstrates how you can take advantage of View Data and HTML Helpers within a View.</span></span>

<span data-ttu-id="d4406-108">本教程的目的是提供 ASP.NET MVC 视图、视图数据和 HTML 帮助器的简要介绍。</span><span class="sxs-lookup"><span data-stu-id="d4406-108">The purpose of this tutorial is to provide you with a brief introduction to ASP.NET MVC views, view data, and HTML Helpers.</span></span> <span data-ttu-id="d4406-109">在本教程结束时，应了解如何创建新视图，将数据从控制器传递到视图，以及使用 HTML 帮助器在视图中生成内容。</span><span class="sxs-lookup"><span data-stu-id="d4406-109">By the end of this tutorial, you should understand how to create new views, pass data from a controller to a view, and use HTML Helpers to generate content in a view.</span></span>

## <a name="understanding-views"></a><span data-ttu-id="d4406-110">了解视图</span><span class="sxs-lookup"><span data-stu-id="d4406-110">Understanding Views</span></span>

<span data-ttu-id="d4406-111">与 ASP.NET 或 Active Server Pages 不同，ASP.NET MVC 不包含任何直接对应于页面的内容。</span><span class="sxs-lookup"><span data-stu-id="d4406-111">Unlike ASP.NET or Active Server Pages, ASP.NET MVC does not include anything that directly corresponds to a page.</span></span> <span data-ttu-id="d4406-112">在 ASP.NET MVC 应用程序中，磁盘上没有对应于你在浏览器的地址栏中键入的 URL 中的路径的页面。</span><span class="sxs-lookup"><span data-stu-id="d4406-112">In an ASP.NET MVC application, there is not a page on disk that corresponds to the path in the URL that you type into the address bar of your browser.</span></span> <span data-ttu-id="d4406-113">ASP.NET MVC 应用程序中最接近的一页是称为 " *视图*"。</span><span class="sxs-lookup"><span data-stu-id="d4406-113">The closest thing to a page in an ASP.NET MVC application is something called a *view*.</span></span>

<span data-ttu-id="d4406-114">在 ASP.NET MVC 应用程序中，传入的浏览器请求会映射到控制器操作。</span><span class="sxs-lookup"><span data-stu-id="d4406-114">In an ASP.NET MVC application, incoming browser requests are mapped to controller actions.</span></span> <span data-ttu-id="d4406-115">控制器操作可能会返回视图。</span><span class="sxs-lookup"><span data-stu-id="d4406-115">A controller action might return a view.</span></span> <span data-ttu-id="d4406-116">但是，控制器操作可能会执行其他某种类型的操作，例如，将您重定向到另一个控制器操作。</span><span class="sxs-lookup"><span data-stu-id="d4406-116">However, a controller action might perform some other type of action such as redirecting you to another controller action.</span></span>

<span data-ttu-id="d4406-117">列表1包含一个名为 "HomeController" 的简单控制器。</span><span class="sxs-lookup"><span data-stu-id="d4406-117">Listing 1 contains a simple controller named the HomeController.</span></span> <span data-ttu-id="d4406-118">HomeController 公开了两个名为 Index ( 控制器操作： # A1，详细信息 ( # A3。</span><span class="sxs-lookup"><span data-stu-id="d4406-118">The HomeController exposes two controller actions named Index() and Details().</span></span>

<span data-ttu-id="d4406-119">**列表 1-HomeController**</span><span class="sxs-lookup"><span data-stu-id="d4406-119">**Listing 1 - HomeController.vb**</span></span>

[!code-vb[Main](asp-net-mvc-views-overview-vb/samples/sample1.vb)]

<span data-ttu-id="d4406-120">通过在浏览器地址栏中键入以下 URL，可以调用第一个操作（索引 ( # A1 操作）：</span><span class="sxs-lookup"><span data-stu-id="d4406-120">You can invoke the first action, the Index() action, by typing the following URL into your browser address bar:</span></span>

<span data-ttu-id="d4406-121">/Home/Index</span><span class="sxs-lookup"><span data-stu-id="d4406-121">/Home/Index</span></span>

<span data-ttu-id="d4406-122">可以通过在浏览器中键入此地址来调用第二个操作，详细信息 ( # A1 操作：</span><span class="sxs-lookup"><span data-stu-id="d4406-122">You can invoke the second action, the Details() action, by typing this address into your browser:</span></span>

<span data-ttu-id="d4406-123">/Home/Details</span><span class="sxs-lookup"><span data-stu-id="d4406-123">/Home/Details</span></span>

<span data-ttu-id="d4406-124">索引 ( # A1 操作返回视图。</span><span class="sxs-lookup"><span data-stu-id="d4406-124">The Index() action returns a view.</span></span> <span data-ttu-id="d4406-125">你创建的大多数操作都将返回视图。</span><span class="sxs-lookup"><span data-stu-id="d4406-125">Most actions that you create will return views.</span></span> <span data-ttu-id="d4406-126">不过，操作可以返回其他类型的操作结果。</span><span class="sxs-lookup"><span data-stu-id="d4406-126">However, an action can return other types of action results.</span></span> <span data-ttu-id="d4406-127">例如，详细信息 ( # A1 操作返回将传入请求重定向到索引 ( # A3 操作的 RedirectToActionResult。</span><span class="sxs-lookup"><span data-stu-id="d4406-127">For example, the Details() action returns a RedirectToActionResult that redirects incoming request to the Index() action.</span></span>

<span data-ttu-id="d4406-128">索引 ( # A1 操作包含以下代码行：</span><span class="sxs-lookup"><span data-stu-id="d4406-128">The Index() action contains the following single line of code:</span></span>

<span data-ttu-id="d4406-129">查看 ( # A1</span><span class="sxs-lookup"><span data-stu-id="d4406-129">View()</span></span>

<span data-ttu-id="d4406-130">下面这行代码将返回一个视图，该视图必须位于 web 服务器上的以下路径：</span><span class="sxs-lookup"><span data-stu-id="d4406-130">This line of code returns a view that must be located at the following path on your web server:</span></span>

<span data-ttu-id="d4406-131">\Views\Home\Index.aspx</span><span class="sxs-lookup"><span data-stu-id="d4406-131">\Views\Home\Index.aspx</span></span>

<span data-ttu-id="d4406-132">将从控制器的名称和控制器操作的名称推断视图的路径。</span><span class="sxs-lookup"><span data-stu-id="d4406-132">The path to the view is inferred from the name of the controller and the name of the controller action.</span></span>

<span data-ttu-id="d4406-133">如果您愿意，您可以清楚了解视图。</span><span class="sxs-lookup"><span data-stu-id="d4406-133">If you prefer, you can be explicit about the view.</span></span> <span data-ttu-id="d4406-134">下面的代码行返回一个名为 Fred 的视图：</span><span class="sxs-lookup"><span data-stu-id="d4406-134">The following line of code returns a view named Fred :</span></span>

<span data-ttu-id="d4406-135">查看 ( Fred ) </span><span class="sxs-lookup"><span data-stu-id="d4406-135">View( Fred )</span></span>

<span data-ttu-id="d4406-136">执行此代码行时，将从以下路径返回视图：</span><span class="sxs-lookup"><span data-stu-id="d4406-136">When this line of code is executed, a view is returned from the following path:</span></span>

<span data-ttu-id="d4406-137">\Views\Home\Fred.aspx</span><span class="sxs-lookup"><span data-stu-id="d4406-137">\Views\Home\Fred.aspx</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="d4406-138">如果计划为 ASP.NET MVC 应用程序创建单元测试，则最好是显式了解视图名称。</span><span class="sxs-lookup"><span data-stu-id="d4406-138">If you plan to create unit tests for your ASP.NET MVC application then it is a good idea to be explicit about view names.</span></span> <span data-ttu-id="d4406-139">这样，便可以创建单元测试来验证控制器操作是否返回了预期视图。</span><span class="sxs-lookup"><span data-stu-id="d4406-139">That way, you can create a unit test to verify that the expected view was returned by a controller action.</span></span>

## <a name="adding-content-to-a-view"></a><span data-ttu-id="d4406-140">向视图添加内容</span><span class="sxs-lookup"><span data-stu-id="d4406-140">Adding Content to a View</span></span>

<span data-ttu-id="d4406-141">视图是可以包含脚本的标准 (X) HTML 文档。</span><span class="sxs-lookup"><span data-stu-id="d4406-141">A view is a standard (X)HTML document that can contain scripts.</span></span> <span data-ttu-id="d4406-142">您可以使用脚本向视图中添加动态内容。</span><span class="sxs-lookup"><span data-stu-id="d4406-142">You use scripts to add dynamic content to a view.</span></span>

<span data-ttu-id="d4406-143">例如，"列表 2" 中的视图显示当前日期和时间。</span><span class="sxs-lookup"><span data-stu-id="d4406-143">For example, the view in Listing 2 displays the current date and time.</span></span>

<span data-ttu-id="d4406-144">**列表 2-\Views\Home\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="d4406-144">**Listing 2 - \Views\Home\Index.aspx**</span></span>

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample2.aspx)]

<span data-ttu-id="d4406-145">请注意，列表2中的 HTML 页面的正文包含以下脚本：</span><span class="sxs-lookup"><span data-stu-id="d4406-145">Notice that the body of the HTML page in Listing 2 contains the following script:</span></span>

<span data-ttu-id="d4406-146">&lt;% 响应。写入 (日期时间。现在) %&gt;</span><span class="sxs-lookup"><span data-stu-id="d4406-146">&lt;% Response.Write(DateTime.Now)%&gt;</span></span>

<span data-ttu-id="d4406-147">使用脚本分隔符 &lt; % 和% &gt; 来标记脚本的开头和结尾。</span><span class="sxs-lookup"><span data-stu-id="d4406-147">You use the script delimiters &lt;% and %&gt; to mark the beginning and end of a script.</span></span> <span data-ttu-id="d4406-148">此脚本是用 Visual basic 编写的。</span><span class="sxs-lookup"><span data-stu-id="d4406-148">This script is written in Visual basic.</span></span> <span data-ttu-id="d4406-149">它通过调用响应来显示当前日期和时间。写入 ( # A1 方法，以将内容呈现到浏览器。</span><span class="sxs-lookup"><span data-stu-id="d4406-149">It displays the current date and time by calling the Response.Write() method to render content to the browser.</span></span> <span data-ttu-id="d4406-150">脚本分隔符 &lt; % 和% &gt; 可用于执行一个或多个语句。</span><span class="sxs-lookup"><span data-stu-id="d4406-150">The script delimiters &lt;% and %&gt; can be used to execute one or more statements.</span></span>

<span data-ttu-id="d4406-151">由于你调用了响应。请经常编写 ( # A1，Microsoft 将为你提供调用响应的快捷方式。编写 ( # A3 方法。</span><span class="sxs-lookup"><span data-stu-id="d4406-151">Since you call Response.Write() so often, Microsoft provides you with a shortcut for calling the Response.Write() method.</span></span> <span data-ttu-id="d4406-152">列表3中的视图使用分隔符 &lt; % = 和% &gt; 作为调用响应的快捷方式。写入 ( # A1。</span><span class="sxs-lookup"><span data-stu-id="d4406-152">The view in Listing 3 uses the delimiters &lt;%= and %&gt; as a shortcut for calling Response.Write().</span></span>

<span data-ttu-id="d4406-153">**列表 3-Views\Home\Index2.aspx**</span><span class="sxs-lookup"><span data-stu-id="d4406-153">**Listing 3 - Views\Home\Index2.aspx**</span></span>

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample3.aspx)]

<span data-ttu-id="d4406-154">您可以使用任何 .NET 语言在视图中生成动态内容。</span><span class="sxs-lookup"><span data-stu-id="d4406-154">You can use any .NET language to generate dynamic content in a view.</span></span> <span data-ttu-id="d4406-155">通常，你将使用 Visual Basic .NET 或 c # 来编写控制器和视图。</span><span class="sxs-lookup"><span data-stu-id="d4406-155">Normally, you'll use either Visual Basic .NET or C# to write your controllers and views.</span></span>

## <a name="using-html-helpers-to-generate-view-content"></a><span data-ttu-id="d4406-156">使用 HTML 帮助器生成视图内容</span><span class="sxs-lookup"><span data-stu-id="d4406-156">Using HTML Helpers to Generate View Content</span></span>

<span data-ttu-id="d4406-157">为了更轻松地向视图添加内容，你可以利用称为 *HTML 帮助器*的内容。</span><span class="sxs-lookup"><span data-stu-id="d4406-157">To make it easier to add content to a view, you can take advantage of something called an *HTML Helper*.</span></span> <span data-ttu-id="d4406-158">通常，HTML 帮助器是生成字符串的方法。</span><span class="sxs-lookup"><span data-stu-id="d4406-158">An HTML Helper, typically, is a method that generates a string.</span></span> <span data-ttu-id="d4406-159">您可以使用 HTML 帮助器生成标准 HTML 元素，例如文本框、链接、下拉列表和列表框。</span><span class="sxs-lookup"><span data-stu-id="d4406-159">You can use HTML Helpers to generate standard HTML elements such as textboxes, links, dropdown lists, and list boxes.</span></span>

<span data-ttu-id="d4406-160">例如，列表4中的视图利用三个 HTML 帮助器--Html.beginform ( # A1，文本框 ( # A3 和 Password ( # A5 帮助程序--生成登录窗体 (参阅图 1) 。</span><span class="sxs-lookup"><span data-stu-id="d4406-160">For example, the view in Listing 4 takes advantage of three HTML Helpers -- the BeginForm(), the TextBox() and Password() helpers -- to generate a Login form (see Figure 1).</span></span>

<span data-ttu-id="d4406-161">**列表 4--\Views\Home\Login.aspx**</span><span class="sxs-lookup"><span data-stu-id="d4406-161">**Listing 4 -- \Views\Home\Login.aspx**</span></span>

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample4.aspx)]

<span data-ttu-id="d4406-162">[![“新建项目”对话框](asp-net-mvc-views-overview-vb/_static/image1.jpg)](asp-net-mvc-views-overview-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="d4406-162">[![The New Project dialog box](asp-net-mvc-views-overview-vb/_static/image1.jpg)](asp-net-mvc-views-overview-vb/_static/image1.png)</span></span>

<span data-ttu-id="d4406-163">**图 01**：标准登录表单 ([单击查看全尺寸图像](asp-net-mvc-views-overview-vb/_static/image2.png)) </span><span class="sxs-lookup"><span data-stu-id="d4406-163">**Figure 01**: A standard Login form ([Click to view full-size image](asp-net-mvc-views-overview-vb/_static/image2.png))</span></span>

<span data-ttu-id="d4406-164">所有 HTML 帮助器方法都是在视图的 Html 属性上调用的。</span><span class="sxs-lookup"><span data-stu-id="d4406-164">All of the HTML Helpers methods are called on the Html property of the view.</span></span> <span data-ttu-id="d4406-165">例如，通过调用 Html. TextBox ( # A1 方法呈现 TextBox。</span><span class="sxs-lookup"><span data-stu-id="d4406-165">For example, you render a TextBox by calling the Html.TextBox() method.</span></span>

<span data-ttu-id="d4406-166">请注意，在 &lt; 调用 Html. TextBox 时，使用脚本分隔符% = 和% &gt; ( # A1 和 html ( # A3 帮助程序。</span><span class="sxs-lookup"><span data-stu-id="d4406-166">Notice that you use the script delimiters &lt;%= and %&gt; when calling both the Html.TextBox() and Html.Password() helpers.</span></span> <span data-ttu-id="d4406-167">这些帮助程序只返回一个字符串。</span><span class="sxs-lookup"><span data-stu-id="d4406-167">These helpers simply return a string.</span></span> <span data-ttu-id="d4406-168">需要调用响应。写入 ( # A1，以便将字符串呈现到浏览器。</span><span class="sxs-lookup"><span data-stu-id="d4406-168">You need to call Response.Write() in order to render the string to the browser.</span></span>

<span data-ttu-id="d4406-169">使用 HTML 帮助器方法是可选的。</span><span class="sxs-lookup"><span data-stu-id="d4406-169">Using HTML Helper methods is optional.</span></span> <span data-ttu-id="d4406-170">通过减少需要编写的 HTML 和脚本数量，使你的生活变得更加轻松。</span><span class="sxs-lookup"><span data-stu-id="d4406-170">They make your life easier by reducing the amount of HTML and script that you need to write.</span></span> <span data-ttu-id="d4406-171">列表5中的视图在不使用 HTML 帮助器的情况下，将与列表4中的视图呈现完全相同的窗体。</span><span class="sxs-lookup"><span data-stu-id="d4406-171">The view in Listing 5 renders the exact same form as the view in Listing 4 without using HTML Helpers.</span></span>

<span data-ttu-id="d4406-172">**列表 5--\Views\Home\Login.aspx**</span><span class="sxs-lookup"><span data-stu-id="d4406-172">**Listing 5 -- \Views\Home\Login.aspx**</span></span>

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample5.aspx)]

<span data-ttu-id="d4406-173">你还可以选择创建你自己的 HTML 帮助器。</span><span class="sxs-lookup"><span data-stu-id="d4406-173">You also have the option of creating your own HTML Helpers.</span></span> <span data-ttu-id="d4406-174">例如，可以创建一个 GridView ( # A1 helper 方法，该方法在 HTML 表中自动显示一组数据库记录。</span><span class="sxs-lookup"><span data-stu-id="d4406-174">For example, you can create a GridView() helper method that displays a set of database records in an HTML table automatically.</span></span> <span data-ttu-id="d4406-175">本主题介绍了如何 **创建自定义 HTML 帮助**程序。</span><span class="sxs-lookup"><span data-stu-id="d4406-175">We explore this topic in the tutorial **Creating Custom HTML Helpers**.</span></span>

## <a name="using-view-data-to-pass-data-to-a-view"></a><span data-ttu-id="d4406-176">使用视图数据将数据传递给视图</span><span class="sxs-lookup"><span data-stu-id="d4406-176">Using View Data to Pass Data to a View</span></span>

<span data-ttu-id="d4406-177">您可以使用 "查看数据" 将数据从控制器传递到视图。</span><span class="sxs-lookup"><span data-stu-id="d4406-177">You use view data to pass data from a controller to a view.</span></span> <span data-ttu-id="d4406-178">请考虑视图数据，如通过邮件发送的包。</span><span class="sxs-lookup"><span data-stu-id="d4406-178">Think of view data like a package that you send through the mail.</span></span> <span data-ttu-id="d4406-179">必须使用此包发送从控制器传递到视图的所有数据。</span><span class="sxs-lookup"><span data-stu-id="d4406-179">All data passed from a controller to a view must be sent using this package.</span></span> <span data-ttu-id="d4406-180">例如，清单6中的控制器添加了用于查看数据的消息。</span><span class="sxs-lookup"><span data-stu-id="d4406-180">For example, the controller in Listing 6 adds a message to view data.</span></span>

<span data-ttu-id="d4406-181">**列表 6-ProductController**</span><span class="sxs-lookup"><span data-stu-id="d4406-181">**Listing 6 - ProductController.vb**</span></span>

[!code-vb[Main](asp-net-mvc-views-overview-vb/samples/sample6.vb)]

<span data-ttu-id="d4406-182">控制器 ViewData 属性表示名称和值对的集合。</span><span class="sxs-lookup"><span data-stu-id="d4406-182">The controller ViewData property represents a collection of name and value pairs.</span></span> <span data-ttu-id="d4406-183">在列表6中，索引 ( # A1 方法将项添加到名为 message 的视图数据集合中，值 Hello World！。</span><span class="sxs-lookup"><span data-stu-id="d4406-183">In Listing 6, the Index() method adds an item to the view data collection named message with the value Hello World!.</span></span> <span data-ttu-id="d4406-184">当索引 ( # A1 方法返回视图时，会自动将视图数据传递给视图。</span><span class="sxs-lookup"><span data-stu-id="d4406-184">When the view is returned by the Index() method, the view data is passed to the view automatically.</span></span>

<span data-ttu-id="d4406-185">列表7中的视图从查看数据中检索消息，并将消息呈现到浏览器。</span><span class="sxs-lookup"><span data-stu-id="d4406-185">The view in Listing 7 retrieves the message from the view data and renders the message to the browser.</span></span>

<span data-ttu-id="d4406-186">**列表 7--\Views\Product\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="d4406-186">**Listing 7 -- \Views\Product\Index.aspx**</span></span>

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample7.aspx)]

<span data-ttu-id="d4406-187">请注意，视图利用 Html. 在呈现消息时， ( # A1 HTML Helper 方法进行编码。</span><span class="sxs-lookup"><span data-stu-id="d4406-187">Notice that the view takes advantage of the Html.Encode() HTML Helper method when rendering the message.</span></span> <span data-ttu-id="d4406-188">Html 编码 ( # A1 HTML 帮助器将特殊字符（例如和）编码为可 &lt; &gt; 安全显示在网页中的字符。</span><span class="sxs-lookup"><span data-stu-id="d4406-188">The Html.Encode() HTML Helper encodes special characters such as &lt; and &gt; into characters that are safe to display in a web page.</span></span> <span data-ttu-id="d4406-189">每当你呈现用户提交到网站的内容时，你应该对内容进行编码，以防出现 JavaScript 注入攻击。</span><span class="sxs-lookup"><span data-stu-id="d4406-189">Whenever you render content that a user submits to a website, you should encode the content to prevent JavaScript injection attacks.</span></span>

<span data-ttu-id="d4406-190"> (因为我们在 ProductController 中创建了自己的消息，所以我们不需要对消息进行编码。</span><span class="sxs-lookup"><span data-stu-id="d4406-190">(Because we created the message ourselves in the ProductController, we don't really need to encode the message.</span></span> <span data-ttu-id="d4406-191">但是，在显示从视图中的视图数据检索到的内容时，始终调用 Html. 编码 ( # A1 方法是一种很好的习惯。 ) </span><span class="sxs-lookup"><span data-stu-id="d4406-191">However, it is a good habit to always call the Html.Encode() method when displaying content retrieved from view data within a view.)</span></span>

<span data-ttu-id="d4406-192">在列表7中，我们利用了视图数据将简单字符串消息从控制器传递到视图。</span><span class="sxs-lookup"><span data-stu-id="d4406-192">In Listing 7, we took advantage of view data to pass a simple string message from a controller to a view.</span></span> <span data-ttu-id="d4406-193">你还可以使用 "查看数据" 将其他类型的数据（如数据库记录集合）从控制器传递到视图。</span><span class="sxs-lookup"><span data-stu-id="d4406-193">You also can use view data to pass other types of data, such as a collection of database records, from a controller to a view.</span></span> <span data-ttu-id="d4406-194">例如，如果您想要在视图中显示 Products 数据库表的内容，则可以在视图数据中传递数据库记录的集合。</span><span class="sxs-lookup"><span data-stu-id="d4406-194">For example, if you want to display the contents of the Products database table in a view, then you would pass the collection of database records in view data.</span></span>

<span data-ttu-id="d4406-195">你还可以选择将强类型视图数据从控制器传递到视图。</span><span class="sxs-lookup"><span data-stu-id="d4406-195">You also have the option of passing strongly typed view data from a controller to a view.</span></span> <span data-ttu-id="d4406-196">本主题介绍了 **了解强类型视图数据和视图**的教程。</span><span class="sxs-lookup"><span data-stu-id="d4406-196">We explore this topic in the tutorial **Understanding Strongly Typed View Data and Views**.</span></span>

## <a name="summary"></a><span data-ttu-id="d4406-197">摘要</span><span class="sxs-lookup"><span data-stu-id="d4406-197">Summary</span></span>

<span data-ttu-id="d4406-198">本教程简要介绍了 ASP.NET MVC 视图、视图数据和 HTML 帮助器。</span><span class="sxs-lookup"><span data-stu-id="d4406-198">This tutorial provided a brief introduction to ASP.NET MVC views, view data, and HTML Helpers.</span></span> <span data-ttu-id="d4406-199">在第一部分中，您学习了如何向项目中添加新视图。</span><span class="sxs-lookup"><span data-stu-id="d4406-199">In the first section, you learned how to add new views to your project.</span></span> <span data-ttu-id="d4406-200">您已经了解到，您必须将视图添加到正确的文件夹中，以便从特定控制器调用它。</span><span class="sxs-lookup"><span data-stu-id="d4406-200">You learned that you must add a view to the right folder in order to call it from a particular controller.</span></span> <span data-ttu-id="d4406-201">接下来，我们讨论了 HTML 帮助器的主题。</span><span class="sxs-lookup"><span data-stu-id="d4406-201">Next, we discussed the topic of HTML Helpers.</span></span> <span data-ttu-id="d4406-202">您学习了 HTML 帮助程序如何使您能够轻松地生成标准 HTML 内容。</span><span class="sxs-lookup"><span data-stu-id="d4406-202">You learned how HTML Helpers enable you to easily generate standard HTML content.</span></span> <span data-ttu-id="d4406-203">最后，您学习了如何利用视图数据将数据从控制器传递到视图。</span><span class="sxs-lookup"><span data-stu-id="d4406-203">Finally, you learned how to take advantage of view data to pass data from a controller to a view.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="d4406-204">[上一页](passing-data-to-view-master-pages-cs.md)
> [下一页](creating-custom-html-helpers-vb.md)</span><span class="sxs-lookup"><span data-stu-id="d4406-204">[Previous](passing-data-to-view-master-pages-cs.md)
[Next](creating-custom-html-helpers-vb.md)</span></span>

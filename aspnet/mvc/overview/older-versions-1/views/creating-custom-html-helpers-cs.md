---
uid: mvc/overview/older-versions-1/views/creating-custom-html-helpers-cs
title: 创建自定义 HTML 帮助器 （C#） |微软文档
author: microsoft
description: 本教程的目标是演示如何创建自定义 HTML 帮助器，您可以在 MVC 视图中使用。 通过利用 HTML 帮助程序...
ms.author: riande
ms.date: 10/07/2008
ms.assetid: e454c67d-a86e-4119-a858-eb04bbec2dff
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-custom-html-helpers-cs
msc.type: authoredcontent
ms.openlocfilehash: 7a2e5a5b42aa5bf267a42fef2fcad7022001ce6f
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675331"
---
# <a name="creating-custom-html-helpers-c"></a><span data-ttu-id="2b464-104">创建自定义 HTML 帮助程序 (C#)</span><span class="sxs-lookup"><span data-stu-id="2b464-104">Creating Custom HTML Helpers (C#)</span></span>

<span data-ttu-id="2b464-105">由[微软](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="2b464-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="2b464-106">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="2b464-106">Download PDF</span></span>](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_9_CS.pdf)

> <span data-ttu-id="2b464-107">本教程的目标是演示如何创建自定义 HTML 帮助器，您可以在 MVC 视图中使用。</span><span class="sxs-lookup"><span data-stu-id="2b464-107">The goal of this tutorial is to demonstrate how you can create custom HTML Helpers that you can use within your MVC views.</span></span> <span data-ttu-id="2b464-108">通过使用 HTML 帮助器，可以减少创建标准 HTML 页必须执行的繁琐键入 HTML 标记的数量。</span><span class="sxs-lookup"><span data-stu-id="2b464-108">By taking advantage of HTML Helpers, you can reduce the amount of tedious typing of HTML tags that you must perform to create a standard HTML page.</span></span>

<span data-ttu-id="2b464-109">本教程的目标是演示如何创建自定义 HTML 帮助器，您可以在 MVC 视图中使用。</span><span class="sxs-lookup"><span data-stu-id="2b464-109">The goal of this tutorial is to demonstrate how you can create custom HTML Helpers that you can use within your MVC views.</span></span> <span data-ttu-id="2b464-110">通过使用 HTML 帮助器，可以减少创建标准 HTML 页必须执行的繁琐键入 HTML 标记的数量。</span><span class="sxs-lookup"><span data-stu-id="2b464-110">By taking advantage of HTML Helpers, you can reduce the amount of tedious typing of HTML tags that you must perform to create a standard HTML page.</span></span>

<span data-ttu-id="2b464-111">在本教程的第一部分中，我描述了 ASP.NET MVC 框架中包含的一些现有 HTML 帮助器。</span><span class="sxs-lookup"><span data-stu-id="2b464-111">In the first part of this tutorial, I describe some of the existing HTML Helpers included with the ASP.NET MVC framework.</span></span> <span data-ttu-id="2b464-112">接下来，我描述了创建自定义 HTML 帮助器的两种方法：我解释如何通过创建静态方法和创建扩展方法来创建自定义 HTML 帮助程序。</span><span class="sxs-lookup"><span data-stu-id="2b464-112">Next, I describe two methods of creating custom HTML Helpers: I explain how to create custom HTML Helpers by creating a static method and by creating an extension method.</span></span>

## <a name="understanding-html-helpers"></a><span data-ttu-id="2b464-113">了解 HTML 帮助器</span><span class="sxs-lookup"><span data-stu-id="2b464-113">Understanding HTML Helpers</span></span>

<span data-ttu-id="2b464-114">HTML 帮助程序只是返回字符串的方法。</span><span class="sxs-lookup"><span data-stu-id="2b464-114">An HTML Helper is just a method that returns a string.</span></span> <span data-ttu-id="2b464-115">字符串可以表示所需的任何类型的内容。</span><span class="sxs-lookup"><span data-stu-id="2b464-115">The string can represent any type of content that you want.</span></span> <span data-ttu-id="2b464-116">例如，可以使用 HTML 帮助器呈现标准 HTML 标记（如`<input>` `<img>` HTML 和标记）。</span><span class="sxs-lookup"><span data-stu-id="2b464-116">For example, you can use HTML Helpers to render standard HTML tags like HTML `<input>` and `<img>` tags.</span></span> <span data-ttu-id="2b464-117">您还可以使用 HTML 帮助器呈现更复杂的内容，如选项卡条或数据库数据的 HTML 表。</span><span class="sxs-lookup"><span data-stu-id="2b464-117">You also can use HTML Helpers to render more complex content such as a tab strip or an HTML table of database data.</span></span>

<span data-ttu-id="2b464-118">mVC 框架ASP.NET包括以下一组标准 HTML 帮助器（这不是完整的列表）：</span><span class="sxs-lookup"><span data-stu-id="2b464-118">The ASP.NET MVC framework includes the following set of standard HTML Helpers (this is not a complete list):</span></span>

- <span data-ttu-id="2b464-119">Html.操作链接（）</span><span class="sxs-lookup"><span data-stu-id="2b464-119">Html.ActionLink()</span></span>
- <span data-ttu-id="2b464-120">Html.开始形式（）</span><span class="sxs-lookup"><span data-stu-id="2b464-120">Html.BeginForm()</span></span>
- <span data-ttu-id="2b464-121">Html.复选框（）</span><span class="sxs-lookup"><span data-stu-id="2b464-121">Html.CheckBox()</span></span>
- <span data-ttu-id="2b464-122">Html.下拉列表（）</span><span class="sxs-lookup"><span data-stu-id="2b464-122">Html.DropDownList()</span></span>
- <span data-ttu-id="2b464-123">Html.结束形式（）</span><span class="sxs-lookup"><span data-stu-id="2b464-123">Html.EndForm()</span></span>
- <span data-ttu-id="2b464-124">Html.隐藏（）</span><span class="sxs-lookup"><span data-stu-id="2b464-124">Html.Hidden()</span></span>
- <span data-ttu-id="2b464-125">Html.列表框（）</span><span class="sxs-lookup"><span data-stu-id="2b464-125">Html.ListBox()</span></span>
- <span data-ttu-id="2b464-126">Html.密码（）</span><span class="sxs-lookup"><span data-stu-id="2b464-126">Html.Password()</span></span>
- <span data-ttu-id="2b464-127">Html.收音机按钮（）</span><span class="sxs-lookup"><span data-stu-id="2b464-127">Html.RadioButton()</span></span>
- <span data-ttu-id="2b464-128">Html.文本区域（）</span><span class="sxs-lookup"><span data-stu-id="2b464-128">Html.TextArea()</span></span>
- <span data-ttu-id="2b464-129">Html.TextBox（）</span><span class="sxs-lookup"><span data-stu-id="2b464-129">Html.TextBox()</span></span>

<span data-ttu-id="2b464-130">例如，请考虑清单 1 中的窗体。</span><span class="sxs-lookup"><span data-stu-id="2b464-130">For example, consider the form in Listing 1.</span></span> <span data-ttu-id="2b464-131">此表单是在两个标准 HTML 帮助器的帮助下呈现的（参见图 1）。</span><span class="sxs-lookup"><span data-stu-id="2b464-131">This form is rendered with the help of two of the standard HTML Helpers (see Figure 1).</span></span> <span data-ttu-id="2b464-132">此窗体使用`Html.BeginForm()`和`Html.TextBox()`帮助器方法呈现简单的 HTML 窗体。</span><span class="sxs-lookup"><span data-stu-id="2b464-132">This form uses the `Html.BeginForm()` and `Html.TextBox()` Helper methods to render a simple HTML form.</span></span>

<span data-ttu-id="2b464-133">[![使用 HTML 帮助器呈现的页面](creating-custom-html-helpers-cs/_static/image2.png)](creating-custom-html-helpers-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="2b464-133">[![Page rendered with HTML Helpers](creating-custom-html-helpers-cs/_static/image2.png)](creating-custom-html-helpers-cs/_static/image1.png)</span></span>

<span data-ttu-id="2b464-134">**图 01**： 使用 HTML 帮助器呈现的页面 （[单击以查看全尺寸图像](creating-custom-html-helpers-cs/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="2b464-134">**Figure 01**: Page rendered with HTML Helpers ([Click to view full-size image](creating-custom-html-helpers-cs/_static/image3.png))</span></span>

<span data-ttu-id="2b464-135">**清单1 |`Views\Home\Index.aspx`**</span><span class="sxs-lookup"><span data-stu-id="2b464-135">**Listing 1 – `Views\Home\Index.aspx`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample1.aspx)]

<span data-ttu-id="2b464-136">Html.BeginForm（） 帮助器方法用于创建打开和关闭 HTML`<form>`标记。</span><span class="sxs-lookup"><span data-stu-id="2b464-136">The Html.BeginForm() Helper method is used to create the opening and closing HTML `<form>` tags.</span></span> <span data-ttu-id="2b464-137">请注意，该方法`Html.BeginForm()`是在 using 语句中调用的。</span><span class="sxs-lookup"><span data-stu-id="2b464-137">Notice that the `Html.BeginForm()` method is called within a using statement.</span></span> <span data-ttu-id="2b464-138">using 语句可确保标记在`<form>`using 块的末尾关闭。</span><span class="sxs-lookup"><span data-stu-id="2b464-138">The using statement ensures that the `<form>` tag gets closed at the end of the using block.</span></span>

<span data-ttu-id="2b464-139">如果您愿意，可以调用 Html.EndForm（） 帮助器方法来关闭`<form>`标记，而不是创建 using 块。</span><span class="sxs-lookup"><span data-stu-id="2b464-139">If you prefer, instead of creating a using block, you can call the Html.EndForm() Helper method to close the `<form>` tag.</span></span> <span data-ttu-id="2b464-140">使用任何方法创建您最直观的开始和结束`<form>`标记。</span><span class="sxs-lookup"><span data-stu-id="2b464-140">Use whichever approach to creating an opening and closing `<form>` tag that seems most intuitive to you.</span></span>

<span data-ttu-id="2b464-141">在`Html.TextBox()`清单1中使用帮助器方法来呈现 HTML`<input>`标记。</span><span class="sxs-lookup"><span data-stu-id="2b464-141">The `Html.TextBox()` Helper methods are used in Listing 1 to render HTML `<input>` tags.</span></span> <span data-ttu-id="2b464-142">如果在浏览器中选择视图源，则会在清单 2 中看到 HTML 源。</span><span class="sxs-lookup"><span data-stu-id="2b464-142">If you select view source in your browser then you see the HTML source in Listing 2.</span></span> <span data-ttu-id="2b464-143">请注意，源包含标准 HTML 标记。</span><span class="sxs-lookup"><span data-stu-id="2b464-143">Notice that the source contains standard HTML tags.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2b464-144">请注意 -HTML`Html.TextBox()`帮助程序使用`<%= %>`标记而不是`<% %>`标记呈现。</span><span class="sxs-lookup"><span data-stu-id="2b464-144">notice that the `Html.TextBox()`-HTML Helper is rendered with `<%= %>` tags instead of `<% %>` tags.</span></span> <span data-ttu-id="2b464-145">如果未包含等号，则不会向浏览器呈现任何内容。</span><span class="sxs-lookup"><span data-stu-id="2b464-145">If you don't include the equal sign, then nothing gets rendered to the browser.</span></span>

<span data-ttu-id="2b464-146">mVC ASP.NET框架包含一小组帮助器。</span><span class="sxs-lookup"><span data-stu-id="2b464-146">The ASP.NET MVC framework contains a small set of helpers.</span></span> <span data-ttu-id="2b464-147">最有可能的是，您需要使用自定义 HTML 帮助程序扩展 MVC 框架。</span><span class="sxs-lookup"><span data-stu-id="2b464-147">Most likely, you will need to extend the MVC framework with custom HTML Helpers.</span></span> <span data-ttu-id="2b464-148">在本教程的其余部分中，您将学习创建自定义 HTML 帮助器的两种方法。</span><span class="sxs-lookup"><span data-stu-id="2b464-148">In the remainder of this tutorial, you learn two methods of creating custom HTML Helpers.</span></span>

<span data-ttu-id="2b464-149">**清单2 |`Index.aspx Source`**</span><span class="sxs-lookup"><span data-stu-id="2b464-149">**Listing 2 – `Index.aspx Source`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample2.aspx)]

### <a name="creating-html-helpers-with-static-methods"></a><span data-ttu-id="2b464-150">使用静态方法创建 HTML 帮助器</span><span class="sxs-lookup"><span data-stu-id="2b464-150">Creating HTML Helpers with Static Methods</span></span>

<span data-ttu-id="2b464-151">创建新 HTML 帮助器的最简单方法是创建返回字符串的静态方法。</span><span class="sxs-lookup"><span data-stu-id="2b464-151">The easiest way to create a new HTML Helper is to create a static method that returns a string.</span></span> <span data-ttu-id="2b464-152">例如，假设您决定创建一个呈现 HTML`<label>`标记的新 HTML 帮助程序。</span><span class="sxs-lookup"><span data-stu-id="2b464-152">Imagine, for example, that you decide to create a new HTML Helper that renders an HTML `<label>` tag.</span></span> <span data-ttu-id="2b464-153">可以使用清单 2 中的类来呈现 。 `<label>`</span><span class="sxs-lookup"><span data-stu-id="2b464-153">You can use the class in Listing 2 to render a `<label>` .</span></span>

<span data-ttu-id="2b464-154">**清单2 |`Helpers\LabelHelper.cs`**</span><span class="sxs-lookup"><span data-stu-id="2b464-154">**Listing 2 – `Helpers\LabelHelper.cs`**</span></span>

[!code-csharp[Main](creating-custom-html-helpers-cs/samples/sample3.cs)]

<span data-ttu-id="2b464-155">清单2中的类没有什么特别之处。</span><span class="sxs-lookup"><span data-stu-id="2b464-155">There is nothing special about the class in Listing 2.</span></span> <span data-ttu-id="2b464-156">该方法`Label()`只需返回一个字符串。</span><span class="sxs-lookup"><span data-stu-id="2b464-156">The `Label()` method simply returns a string.</span></span>

<span data-ttu-id="2b464-157">清单3中修改后的索引视图使用`LabelHelper`来呈现 HTML`<label>`标记。</span><span class="sxs-lookup"><span data-stu-id="2b464-157">The modified Index view in Listing 3 uses the `LabelHelper` to render HTML `<label>` tags.</span></span> <span data-ttu-id="2b464-158">请注意，视图包含导入命名`<%@ imports %>`空间的`Application1.Helpers`指令。</span><span class="sxs-lookup"><span data-stu-id="2b464-158">Notice that the view includes an `<%@ imports %>` directive that imports the `Application1.Helpers` namespace.</span></span>

<span data-ttu-id="2b464-159">**清单2 |`Views\Home\Index2.aspx`**</span><span class="sxs-lookup"><span data-stu-id="2b464-159">**Listing 2 – `Views\Home\Index2.aspx`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample4.aspx)]

### <a name="creating-html-helpers-with-extension-methods"></a><span data-ttu-id="2b464-160">使用扩展方法创建 HTML 帮助程序</span><span class="sxs-lookup"><span data-stu-id="2b464-160">Creating HTML Helpers with Extension Methods</span></span>

<span data-ttu-id="2b464-161">如果要创建与 ASP.NET mVC 框架中包含的标准 HTML 帮助程序相同的 HTML 帮助程序，则需要创建扩展方法。</span><span class="sxs-lookup"><span data-stu-id="2b464-161">If you want to create HTML Helpers that work just like the standard HTML Helpers included in the ASP.NET MVC framework then you need to create extension methods.</span></span> <span data-ttu-id="2b464-162">扩展方法使您能够向现有类添加新方法。</span><span class="sxs-lookup"><span data-stu-id="2b464-162">Extension methods enable you to add new methods to an existing class.</span></span> <span data-ttu-id="2b464-163">创建 HTML 帮助器方法时，向由视图的 Html 属性表示的 HtmlHelper 类添加新方法。</span><span class="sxs-lookup"><span data-stu-id="2b464-163">When creating an HTML Helper method, you add new methods to the HtmlHelper class represented by a view's Html property.</span></span>

<span data-ttu-id="2b464-164">清单3中的类向名为 的`HtmlHelper``Label()`类添加了扩展方法。</span><span class="sxs-lookup"><span data-stu-id="2b464-164">The class in Listing 3 adds an extension method to the `HtmlHelper` class named `Label()`.</span></span> <span data-ttu-id="2b464-165">关于这个类，你应该注意一些事情。</span><span class="sxs-lookup"><span data-stu-id="2b464-165">There are a couple of things that you should notice about this class.</span></span> <span data-ttu-id="2b464-166">首先，请注意类是静态类。</span><span class="sxs-lookup"><span data-stu-id="2b464-166">First, notice that the class is a static class.</span></span> <span data-ttu-id="2b464-167">必须使用静态类定义扩展方法。</span><span class="sxs-lookup"><span data-stu-id="2b464-167">You must define an extension method with a static class.</span></span>

<span data-ttu-id="2b464-168">其次，请注意，`Label()`方法的第一个参数前面是关键字`this`。</span><span class="sxs-lookup"><span data-stu-id="2b464-168">Second, notice that the first parameter of the `Label()` method is preceded by the keyword `this`.</span></span> <span data-ttu-id="2b464-169">扩展方法的第一个参数指示扩展方法扩展的类。</span><span class="sxs-lookup"><span data-stu-id="2b464-169">The first parameter of an extension method indicates the class that the extension method extends.</span></span>

<span data-ttu-id="2b464-170">**清单3 |`Helpers\LabelExtensions.cs`**</span><span class="sxs-lookup"><span data-stu-id="2b464-170">**Listing 3 – `Helpers\LabelExtensions.cs`**</span></span>

[!code-csharp[Main](creating-custom-html-helpers-cs/samples/sample5.cs)]

<span data-ttu-id="2b464-171">创建扩展方法并成功构建应用程序后，扩展方法与类的所有其他方法一样显示在 Visual Studio Intellisense 中（参见图 2）。</span><span class="sxs-lookup"><span data-stu-id="2b464-171">After you create an extension method, and build your application successfully, the extension method appears in Visual Studio Intellisense like all of the other methods of a class (see Figure 2).</span></span> <span data-ttu-id="2b464-172">唯一的区别是扩展方法旁边出现一个特殊符号（向下箭头的图标）。</span><span class="sxs-lookup"><span data-stu-id="2b464-172">The only difference is that extension methods appear with a special symbol next to them (an icon of a downward arrow).</span></span>

<span data-ttu-id="2b464-173">[![使用 Html.label（） 扩展方法](creating-custom-html-helpers-cs/_static/image5.png)](creating-custom-html-helpers-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="2b464-173">[![Using the Html.Label() extension method](creating-custom-html-helpers-cs/_static/image5.png)](creating-custom-html-helpers-cs/_static/image4.png)</span></span>

<span data-ttu-id="2b464-174">**图 02**： 使用 Html.label（） 扩展方法 （[单击以查看全尺寸图像](creating-custom-html-helpers-cs/_static/image6.png)）</span><span class="sxs-lookup"><span data-stu-id="2b464-174">**Figure 02**: Using the Html.Label() extension method  ([Click to view full-size image](creating-custom-html-helpers-cs/_static/image6.png))</span></span>

<span data-ttu-id="2b464-175">清单4中修改后的索引视图使用 Html.label（） 扩展方法呈现其所有`<label>`标记。</span><span class="sxs-lookup"><span data-stu-id="2b464-175">The modified Index view in Listing 4 uses the Html.Label() extension method to render all of its `<label>` tags.</span></span>

<span data-ttu-id="2b464-176">**清单4 |`Views\Home\Index3.aspx`**</span><span class="sxs-lookup"><span data-stu-id="2b464-176">**Listing 4 – `Views\Home\Index3.aspx`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample6.aspx)]

## <a name="summary"></a><span data-ttu-id="2b464-177">总结</span><span class="sxs-lookup"><span data-stu-id="2b464-177">Summary</span></span>

<span data-ttu-id="2b464-178">在本教程中，您学习了创建自定义 HTML 帮助器的两种方法。</span><span class="sxs-lookup"><span data-stu-id="2b464-178">In this tutorial, you learned two methods of creating custom HTML Helpers.</span></span> <span data-ttu-id="2b464-179">首先，您学习了如何通过创建返回字符串`Label()`的静态方法来创建自定义 HTML 帮助程序。</span><span class="sxs-lookup"><span data-stu-id="2b464-179">First, you learned how to create a custom `Label()` HTML Helper by creating a static method that returns a string.</span></span> <span data-ttu-id="2b464-180">接下来，您学习了如何通过在`Label()``HtmlHelper`类上创建扩展方法来创建自定义 HTML 帮助器方法。</span><span class="sxs-lookup"><span data-stu-id="2b464-180">Next, you learned how to create a custom `Label()` HTML Helper method by creating an extension method on the `HtmlHelper` class.</span></span>

<span data-ttu-id="2b464-181">在本教程中，我重点讨论了构建一个非常简单的 HTML 帮助器方法。</span><span class="sxs-lookup"><span data-stu-id="2b464-181">In this tutorial, I focused on building an extremely simple HTML Helper method.</span></span> <span data-ttu-id="2b464-182">意识到 HTML 帮助程序可能非常复杂。</span><span class="sxs-lookup"><span data-stu-id="2b464-182">Realize that an HTML Helper can be as complicated as you want.</span></span> <span data-ttu-id="2b464-183">可以生成 HTML 帮助程序，这些帮助程序呈现丰富的内容，如树视图、菜单或数据库数据表。</span><span class="sxs-lookup"><span data-stu-id="2b464-183">You can build HTML Helpers that render rich content such as tree views, menus, or tables of database data.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="2b464-184">[上一页](asp-net-mvc-views-overview-cs.md)
> [下一页](using-the-tagbuilder-class-to-build-html-helpers-cs.md)</span><span class="sxs-lookup"><span data-stu-id="2b464-184">[Previous](asp-net-mvc-views-overview-cs.md)
[Next](using-the-tagbuilder-class-to-build-html-helpers-cs.md)</span></span>

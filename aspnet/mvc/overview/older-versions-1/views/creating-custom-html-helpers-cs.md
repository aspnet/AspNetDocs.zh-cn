---
uid: aspnet/mvc/overview/older-versions-1/views/creating-custom-html-helpers-cs
title: 创建自定义 HTML 帮助程序 (C#) |Microsoft Docs
author: microsoft
description: 本教程的目的是演示如何创建自定义 HTML 帮助程序，你可以使用您的 MVC 视图中。 通过利用 HTML 帮助器...
ms.author: riande
ms.date: 10/07/2008
ms.assetid: e454c67d-a86e-4119-a858-eb04bbec2dff
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-custom-html-helpers-cs
msc.type: authoredcontent
ms.openlocfilehash: 23741d7974713102e6ccb46ced5d62ec202505e8
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/09/2019
ms.locfileid: "59400849"
---
# <a name="creating-custom-html-helpers-c"></a><span data-ttu-id="f81b8-104">创建自定义 HTML 帮助程序 (C#)</span><span class="sxs-lookup"><span data-stu-id="f81b8-104">Creating Custom HTML Helpers (C#)</span></span>

<span data-ttu-id="f81b8-105">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="f81b8-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="f81b8-106">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="f81b8-106">Download PDF</span></span>](http://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_9_CS.pdf)

> <span data-ttu-id="f81b8-107">本教程的目的是演示如何创建自定义 HTML 帮助程序，你可以使用您的 MVC 视图中。</span><span class="sxs-lookup"><span data-stu-id="f81b8-107">The goal of this tutorial is to demonstrate how you can create custom HTML Helpers that you can use within your MVC views.</span></span> <span data-ttu-id="f81b8-108">通过利用 HTML 帮助程序，可以减少量，你必须执行来创建标准的 HTML 页面的 HTML 标记的类型设置枯燥乏味。</span><span class="sxs-lookup"><span data-stu-id="f81b8-108">By taking advantage of HTML Helpers, you can reduce the amount of tedious typing of HTML tags that you must perform to create a standard HTML page.</span></span>


<span data-ttu-id="f81b8-109">本教程的目的是演示如何创建自定义 HTML 帮助程序，你可以使用您的 MVC 视图中。</span><span class="sxs-lookup"><span data-stu-id="f81b8-109">The goal of this tutorial is to demonstrate how you can create custom HTML Helpers that you can use within your MVC views.</span></span> <span data-ttu-id="f81b8-110">通过利用 HTML 帮助程序，可以减少量，你必须执行来创建标准的 HTML 页面的 HTML 标记的类型设置枯燥乏味。</span><span class="sxs-lookup"><span data-stu-id="f81b8-110">By taking advantage of HTML Helpers, you can reduce the amount of tedious typing of HTML tags that you must perform to create a standard HTML page.</span></span>

<span data-ttu-id="f81b8-111">在本教程的第一个部分中，我介绍了一些现有 ASP.NET MVC framework 附带的 HTML 帮助程序。</span><span class="sxs-lookup"><span data-stu-id="f81b8-111">In the first part of this tutorial, I describe some of the existing HTML Helpers included with the ASP.NET MVC framework.</span></span> <span data-ttu-id="f81b8-112">接下来，我将介绍创建自定义 HTML 帮助程序的两个方法：我将介绍如何创建自定义 HTML 帮助程序，通过创建一个静态方法，并创建扩展方法。</span><span class="sxs-lookup"><span data-stu-id="f81b8-112">Next, I describe two methods of creating custom HTML Helpers: I explain how to create custom HTML Helpers by creating a static method and by creating an extension method.</span></span>

## <a name="understanding-html-helpers"></a><span data-ttu-id="f81b8-113">了解 HTML 帮助程序</span><span class="sxs-lookup"><span data-stu-id="f81b8-113">Understanding HTML Helpers</span></span>

<span data-ttu-id="f81b8-114">HTML 帮助器就是返回一个字符串的方法。</span><span class="sxs-lookup"><span data-stu-id="f81b8-114">An HTML Helper is just a method that returns a string.</span></span> <span data-ttu-id="f81b8-115">该字符串可表示任何类型的所需的内容。</span><span class="sxs-lookup"><span data-stu-id="f81b8-115">The string can represent any type of content that you want.</span></span> <span data-ttu-id="f81b8-116">例如，使用 HTML 帮助器来呈现标准 HTML 标记与 HTML 一样`<input>`和`<img>`标记。</span><span class="sxs-lookup"><span data-stu-id="f81b8-116">For example, you can use HTML Helpers to render standard HTML tags like HTML `<input>` and `<img>` tags.</span></span> <span data-ttu-id="f81b8-117">此外可以使用 HTML 帮助器来呈现选项卡条带或 HTML 表的数据库数据等更复杂的内容。</span><span class="sxs-lookup"><span data-stu-id="f81b8-117">You also can use HTML Helpers to render more complex content such as a tab strip or an HTML table of database data.</span></span>

<span data-ttu-id="f81b8-118">ASP.NET MVC 框架包括以下一组标准的 HTML 帮助程序 （这不是完整的列表）：</span><span class="sxs-lookup"><span data-stu-id="f81b8-118">The ASP.NET MVC framework includes the following set of standard HTML Helpers (this is not a complete list):</span></span>

- <span data-ttu-id="f81b8-119">Html.ActionLink()</span><span class="sxs-lookup"><span data-stu-id="f81b8-119">Html.ActionLink()</span></span>
- <span data-ttu-id="f81b8-120">Html.BeginForm()</span><span class="sxs-lookup"><span data-stu-id="f81b8-120">Html.BeginForm()</span></span>
- <span data-ttu-id="f81b8-121">Html.CheckBox()</span><span class="sxs-lookup"><span data-stu-id="f81b8-121">Html.CheckBox()</span></span>
- <span data-ttu-id="f81b8-122">Html.DropDownList()</span><span class="sxs-lookup"><span data-stu-id="f81b8-122">Html.DropDownList()</span></span>
- <span data-ttu-id="f81b8-123">Html.EndForm()</span><span class="sxs-lookup"><span data-stu-id="f81b8-123">Html.EndForm()</span></span>
- <span data-ttu-id="f81b8-124">Html.Hidden()</span><span class="sxs-lookup"><span data-stu-id="f81b8-124">Html.Hidden()</span></span>
- <span data-ttu-id="f81b8-125">Html.ListBox()</span><span class="sxs-lookup"><span data-stu-id="f81b8-125">Html.ListBox()</span></span>
- <span data-ttu-id="f81b8-126">Html.Password()</span><span class="sxs-lookup"><span data-stu-id="f81b8-126">Html.Password()</span></span>
- <span data-ttu-id="f81b8-127">Html.RadioButton()</span><span class="sxs-lookup"><span data-stu-id="f81b8-127">Html.RadioButton()</span></span>
- <span data-ttu-id="f81b8-128">Html.TextArea()</span><span class="sxs-lookup"><span data-stu-id="f81b8-128">Html.TextArea()</span></span>
- <span data-ttu-id="f81b8-129">Html.TextBox()</span><span class="sxs-lookup"><span data-stu-id="f81b8-129">Html.TextBox()</span></span>

<span data-ttu-id="f81b8-130">例如，考虑列表 1 中的窗体。</span><span class="sxs-lookup"><span data-stu-id="f81b8-130">For example, consider the form in Listing 1.</span></span> <span data-ttu-id="f81b8-131">呈现此窗体所使用的两个标准 HTML 帮助程序 （请参阅图 1） 的帮助。</span><span class="sxs-lookup"><span data-stu-id="f81b8-131">This form is rendered with the help of two of the standard HTML Helpers (see Figure 1).</span></span> <span data-ttu-id="f81b8-132">使用此窗体`Html.BeginForm()`和`Html.TextBox()`帮助器方法来呈现一个简单的 HTML 窗体。</span><span class="sxs-lookup"><span data-stu-id="f81b8-132">This form uses the `Html.BeginForm()` and `Html.TextBox()` Helper methods to render a simple HTML form.</span></span>


[![P<span data-ttu-id="f81b8-133">使用 HTML 帮助器呈现的 age]</span><span class="sxs-lookup"><span data-stu-id="f81b8-133">age rendered with HTML Helpers]</span></span>(creating-custom-html-helpers-cs/_static/image2.png)](creating-custom-html-helpers-cs/_static/image1.png)

<span data-ttu-id="f81b8-134">**图 01**:与 HTML 帮助器呈现的页 ([单击此项可查看原尺寸图像](creating-custom-html-helpers-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="f81b8-134">**Figure 01**: Page rendered with HTML Helpers ([Click to view full-size image](creating-custom-html-helpers-cs/_static/image3.png))</span></span>


**<span data-ttu-id="f81b8-135">代码清单 1 –</span><span class="sxs-lookup"><span data-stu-id="f81b8-135">Listing 1 –</span></span> `Views\Home\Index.aspx`**

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample1.aspx)]

<span data-ttu-id="f81b8-136">Html.BeginForm() 帮助器方法用于创建开始和结束 HTML`<form>`标记。</span><span class="sxs-lookup"><span data-stu-id="f81b8-136">The Html.BeginForm() Helper method is used to create the opening and closing HTML `<form>` tags.</span></span> <span data-ttu-id="f81b8-137">请注意，`Html.BeginForm()`方法调用中的 using 语句。</span><span class="sxs-lookup"><span data-stu-id="f81b8-137">Notice that the `Html.BeginForm()` method is called within a using statement.</span></span> <span data-ttu-id="f81b8-138">使用语句将确保`<form>`标记获取使用的结尾处结束块。</span><span class="sxs-lookup"><span data-stu-id="f81b8-138">The using statement ensures that the `<form>` tag gets closed at the end of the using block.</span></span>

<span data-ttu-id="f81b8-139">如果您愿意，而不是创建一个 using 块中，您可以调用 Html.EndForm() 帮助器方法来关闭`<form>`标记。</span><span class="sxs-lookup"><span data-stu-id="f81b8-139">If you prefer, instead of creating a using block, you can call the Html.EndForm() Helper method to close the `<form>` tag.</span></span> <span data-ttu-id="f81b8-140">使用任何方法来创建一个打开和关闭`<form>`似乎是最直观的标记。</span><span class="sxs-lookup"><span data-stu-id="f81b8-140">Use whichever approach to creating an opening and closing `<form>` tag that seems most intuitive to you.</span></span>

<span data-ttu-id="f81b8-141">`Html.TextBox()`帮助器方法用于在列表 1 中呈现 HTML`<input>`标记。</span><span class="sxs-lookup"><span data-stu-id="f81b8-141">The `Html.TextBox()` Helper methods are used in Listing 1 to render HTML `<input>` tags.</span></span> <span data-ttu-id="f81b8-142">如果你看到代码清单 2 中的 HTML 源，然后在浏览器中选择查看源。</span><span class="sxs-lookup"><span data-stu-id="f81b8-142">If you select view source in your browser then you see the HTML source in Listing 2.</span></span> <span data-ttu-id="f81b8-143">请注意源包含标准的 HTML 标记。</span><span class="sxs-lookup"><span data-stu-id="f81b8-143">Notice that the source contains standard HTML tags.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f81b8-144">请注意，`Html.TextBox()`帮助器呈现 HTML`<%= %>`标记而不是`<% %>`标记。</span><span class="sxs-lookup"><span data-stu-id="f81b8-144">notice that the `Html.TextBox()`-HTML Helper is rendered with `<%= %>` tags instead of `<% %>` tags.</span></span> <span data-ttu-id="f81b8-145">如果不包含等号，然后执行任何操作获取浏览器中呈现。</span><span class="sxs-lookup"><span data-stu-id="f81b8-145">If you don't include the equal sign, then nothing gets rendered to the browser.</span></span>

<span data-ttu-id="f81b8-146">ASP.NET MVC 框架包含一小组帮助程序。</span><span class="sxs-lookup"><span data-stu-id="f81b8-146">The ASP.NET MVC framework contains a small set of helpers.</span></span> <span data-ttu-id="f81b8-147">很可能需要扩展 MVC 框架使用自定义 HTML 帮助程序。</span><span class="sxs-lookup"><span data-stu-id="f81b8-147">Most likely, you will need to extend the MVC framework with custom HTML Helpers.</span></span> <span data-ttu-id="f81b8-148">在本教程的其余部分，了解创建自定义 HTML 帮助程序的两个方法。</span><span class="sxs-lookup"><span data-stu-id="f81b8-148">In the remainder of this tutorial, you learn two methods of creating custom HTML Helpers.</span></span>

**<span data-ttu-id="f81b8-149">代码清单 2 –</span><span class="sxs-lookup"><span data-stu-id="f81b8-149">Listing 2 –</span></span> `Index.aspx Source`**

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample2.aspx)]

### <a name="creating-html-helpers-with-static-methods"></a><span data-ttu-id="f81b8-150">创建包含静态方法的 HTML 帮助程序</span><span class="sxs-lookup"><span data-stu-id="f81b8-150">Creating HTML Helpers with Static Methods</span></span>

<span data-ttu-id="f81b8-151">若要创建新的 HTML 帮助器的最简单方法是创建返回的字符串的静态方法。</span><span class="sxs-lookup"><span data-stu-id="f81b8-151">The easiest way to create a new HTML Helper is to create a static method that returns a string.</span></span> <span data-ttu-id="f81b8-152">例如，假设你决定创建新的 HTML 帮助程序呈现 HTML`<label>`标记。</span><span class="sxs-lookup"><span data-stu-id="f81b8-152">Imagine, for example, that you decide to create a new HTML Helper that renders an HTML `<label>` tag.</span></span> <span data-ttu-id="f81b8-153">可以使用在代码清单 2 中的类来呈现`<label>`。</span><span class="sxs-lookup"><span data-stu-id="f81b8-153">You can use the class in Listing 2 to render a `<label>` .</span></span>

**<span data-ttu-id="f81b8-154">代码清单 2 –</span><span class="sxs-lookup"><span data-stu-id="f81b8-154">Listing 2 –</span></span> `Helpers\LabelHelper.cs`**

[!code-csharp[Main](creating-custom-html-helpers-cs/samples/sample3.cs)]

<span data-ttu-id="f81b8-155">没有什么特别之处代码清单 2 中的类。</span><span class="sxs-lookup"><span data-stu-id="f81b8-155">There is nothing special about the class in Listing 2.</span></span> <span data-ttu-id="f81b8-156">`Label()`方法只返回一个字符串。</span><span class="sxs-lookup"><span data-stu-id="f81b8-156">The `Label()` method simply returns a string.</span></span>

<span data-ttu-id="f81b8-157">列表 3 中已修改的索引视图使用`LabelHelper`呈现 HTML`<label>`标记。</span><span class="sxs-lookup"><span data-stu-id="f81b8-157">The modified Index view in Listing 3 uses the `LabelHelper` to render HTML `<label>` tags.</span></span> <span data-ttu-id="f81b8-158">请注意，该视图包含`<%@ imports %>`导入指令`Application1.Helpers`命名空间。</span><span class="sxs-lookup"><span data-stu-id="f81b8-158">Notice that the view includes an `<%@ imports %>` directive that imports the `Application1.Helpers` namespace.</span></span>

**<span data-ttu-id="f81b8-159">代码清单 2 –</span><span class="sxs-lookup"><span data-stu-id="f81b8-159">Listing 2 –</span></span> `Views\Home\Index2.aspx`**

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample4.aspx)]

### <a name="creating-html-helpers-with-extension-methods"></a><span data-ttu-id="f81b8-160">使用扩展方法创建 HTML 帮助程序</span><span class="sxs-lookup"><span data-stu-id="f81b8-160">Creating HTML Helpers with Extension Methods</span></span>

<span data-ttu-id="f81b8-161">如果你想要创建的 HTML 帮助程序就类似于标准的 HTML 帮助程序，它们包含在 ASP.NET MVC framework，则需要创建扩展方法。</span><span class="sxs-lookup"><span data-stu-id="f81b8-161">If you want to create HTML Helpers that work just like the standard HTML Helpers included in the ASP.NET MVC framework then you need to create extension methods.</span></span> <span data-ttu-id="f81b8-162">扩展方法，可向现有类中添加新的方法。</span><span class="sxs-lookup"><span data-stu-id="f81b8-162">Extension methods enable you to add new methods to an existing class.</span></span> <span data-ttu-id="f81b8-163">时创建的 HTML 帮助器方法，您将新方法添加到视图的 Html 属性表示 HtmlHelper 类。</span><span class="sxs-lookup"><span data-stu-id="f81b8-163">When creating an HTML Helper method, you add new methods to the HtmlHelper class represented by a view's Html property.</span></span>

<span data-ttu-id="f81b8-164">列表 3 中的类添加到扩展方法`HtmlHelper`类名为`Label()`。</span><span class="sxs-lookup"><span data-stu-id="f81b8-164">The class in Listing 3 adds an extension method to the `HtmlHelper` class named `Label()`.</span></span> <span data-ttu-id="f81b8-165">有几个您应注意到有关此类的地方。</span><span class="sxs-lookup"><span data-stu-id="f81b8-165">There are a couple of things that you should notice about this class.</span></span> <span data-ttu-id="f81b8-166">首先，请注意此类是一个静态类。</span><span class="sxs-lookup"><span data-stu-id="f81b8-166">First, notice that the class is a static class.</span></span> <span data-ttu-id="f81b8-167">必须定义具有一个静态类的扩展方法。</span><span class="sxs-lookup"><span data-stu-id="f81b8-167">You must define an extension method with a static class.</span></span>

<span data-ttu-id="f81b8-168">其次，注意的第一个参数`Label()`方法前面由关键字`this`。</span><span class="sxs-lookup"><span data-stu-id="f81b8-168">Second, notice that the first parameter of the `Label()` method is preceded by the keyword `this`.</span></span> <span data-ttu-id="f81b8-169">扩展方法的第一个参数指示的扩展方法扩展的类。</span><span class="sxs-lookup"><span data-stu-id="f81b8-169">The first parameter of an extension method indicates the class that the extension method extends.</span></span>

**<span data-ttu-id="f81b8-170">代码清单 3 –</span><span class="sxs-lookup"><span data-stu-id="f81b8-170">Listing 3 –</span></span> `Helpers\LabelExtensions.cs`**

[!code-csharp[Main](creating-custom-html-helpers-cs/samples/sample5.cs)]

<span data-ttu-id="f81b8-171">创建一个扩展方法，并已成功生成应用程序后，扩展方法将出现在 Visual Studio Intellisense 等所有其他方法的类 （请参见图 2）。</span><span class="sxs-lookup"><span data-stu-id="f81b8-171">After you create an extension method, and build your application successfully, the extension method appears in Visual Studio Intellisense like all of the other methods of a class (see Figure 2).</span></span> <span data-ttu-id="f81b8-172">唯一的区别是该扩展方法显示一个特殊符号旁边 （向下箭头的图标）。</span><span class="sxs-lookup"><span data-stu-id="f81b8-172">The only difference is that extension methods appear with a special symbol next to them (an icon of a downward arrow).</span></span>


[![U<span data-ttu-id="f81b8-173">发挥最大功效 Html.Label() 扩展方法]</span><span class="sxs-lookup"><span data-stu-id="f81b8-173">sing the Html.Label() extension method]</span></span>(creating-custom-html-helpers-cs/_static/image5.png)](creating-custom-html-helpers-cs/_static/image4.png)

<span data-ttu-id="f81b8-174">**图 02**:使用 Html.Label() 扩展方法 ([单击此项可查看原尺寸图像](creating-custom-html-helpers-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="f81b8-174">**Figure 02**: Using the Html.Label() extension method  ([Click to view full-size image](creating-custom-html-helpers-cs/_static/image6.png))</span></span>


<span data-ttu-id="f81b8-175">列表 4 中经过修改的索引视图使用 Html.Label() 扩展方法呈现的所有其`<label>`标记。</span><span class="sxs-lookup"><span data-stu-id="f81b8-175">The modified Index view in Listing 4 uses the Html.Label() extension method to render all of its `<label>` tags.</span></span>

**<span data-ttu-id="f81b8-176">列表 4 –</span><span class="sxs-lookup"><span data-stu-id="f81b8-176">Listing 4 –</span></span> `Views\Home\Index3.aspx`**

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample6.aspx)]

## <a name="summary"></a><span data-ttu-id="f81b8-177">总结</span><span class="sxs-lookup"><span data-stu-id="f81b8-177">Summary</span></span>

<span data-ttu-id="f81b8-178">在本教程中，您学习了创建自定义 HTML 帮助程序的两个方法。</span><span class="sxs-lookup"><span data-stu-id="f81b8-178">In this tutorial, you learned two methods of creating custom HTML Helpers.</span></span> <span data-ttu-id="f81b8-179">首先，您学习了如何创建自定义`Label()`通过创建一个静态方法的 HTML 帮助器返回的字符串。</span><span class="sxs-lookup"><span data-stu-id="f81b8-179">First, you learned how to create a custom `Label()` HTML Helper by creating a static method that returns a string.</span></span> <span data-ttu-id="f81b8-180">接下来，您学习了如何创建自定义`Label()`上创建扩展方法的 HTML 帮助器方法`HtmlHelper`类。</span><span class="sxs-lookup"><span data-stu-id="f81b8-180">Next, you learned how to create a custom `Label()` HTML Helper method by creating an extension method on the `HtmlHelper` class.</span></span>

<span data-ttu-id="f81b8-181">在本教程中，我专注于构建一个非常简单的 HTML 帮助器方法。</span><span class="sxs-lookup"><span data-stu-id="f81b8-181">In this tutorial, I focused on building an extremely simple HTML Helper method.</span></span> <span data-ttu-id="f81b8-182">请注意，HTML 帮助器可以是你想的那么复杂。</span><span class="sxs-lookup"><span data-stu-id="f81b8-182">Realize that an HTML Helper can be as complicated as you want.</span></span> <span data-ttu-id="f81b8-183">您可以构建丰富的内容，如树视图、 菜单或表的数据库数据呈现的 HTML 帮助程序。</span><span class="sxs-lookup"><span data-stu-id="f81b8-183">You can build HTML Helpers that render rich content such as tree views, menus, or tables of database data.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="f81b8-184">[上一页](asp-net-mvc-views-overview-cs.md)
> [下一页](using-the-tagbuilder-class-to-build-html-helpers-cs.md)</span><span class="sxs-lookup"><span data-stu-id="f81b8-184">[Previous](asp-net-mvc-views-overview-cs.md)
[Next](using-the-tagbuilder-class-to-build-html-helpers-cs.md)</span></span>

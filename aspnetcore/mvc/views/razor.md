---
title: ASP.NET Core 的 Razor 语法参考
author: rick-anderson
description: 了解 Razor 标记语法，该语法用于将基于服务器的代码嵌入网页中。
ms.author: riande
ms.date: 10/26/2018
uid: mvc/views/razor
ms.openlocfilehash: 8e9ec3c5040e5a24cd5f773b1232897338741c0c
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57052494"
---
# <a name="razor-syntax-reference-for-aspnet-core"></a><span data-ttu-id="206d2-103">ASP.NET Core 的 Razor 语法参考</span><span class="sxs-lookup"><span data-stu-id="206d2-103">Razor syntax reference for ASP.NET Core</span></span>

<span data-ttu-id="206d2-104">作者：[Rick Anderson](https://twitter.com/RickAndMSFT)、[Luke Latham](https://github.com/guardrex)、[Taylor Mullen](https://twitter.com/ntaylormullen) 和 [Dan Vicarel](https://github.com/Rabadash8820)</span><span class="sxs-lookup"><span data-stu-id="206d2-104">By [Rick Anderson](https://twitter.com/RickAndMSFT), [Luke Latham](https://github.com/guardrex), [Taylor Mullen](https://twitter.com/ntaylormullen), and [Dan Vicarel](https://github.com/Rabadash8820)</span></span>

<span data-ttu-id="206d2-105">Razor 是一种标记语法，用于将基于服务器的代码嵌入网页中。</span><span class="sxs-lookup"><span data-stu-id="206d2-105">Razor is a markup syntax for embedding server-based code into webpages.</span></span> <span data-ttu-id="206d2-106">Razor 语法由 Razor 标记、C# 和 HTML 组成。</span><span class="sxs-lookup"><span data-stu-id="206d2-106">The Razor syntax consists of Razor markup, C#, and HTML.</span></span> <span data-ttu-id="206d2-107">包含 Razor 的文件通常具有 *.cshtml* 文件扩展名。</span><span class="sxs-lookup"><span data-stu-id="206d2-107">Files containing Razor generally have a *.cshtml* file extension.</span></span>

## <a name="rendering-html"></a><span data-ttu-id="206d2-108">呈现 HTML</span><span class="sxs-lookup"><span data-stu-id="206d2-108">Rendering HTML</span></span>

<span data-ttu-id="206d2-109">默认 Razor 语言为 HTML。</span><span class="sxs-lookup"><span data-stu-id="206d2-109">The default Razor language is HTML.</span></span> <span data-ttu-id="206d2-110">从 Razor 标记呈现 HTML 与从 HTML 文件呈现 HTML 并没有什么不同。</span><span class="sxs-lookup"><span data-stu-id="206d2-110">Rendering HTML from Razor markup is no different than rendering HTML from an HTML file.</span></span> <span data-ttu-id="206d2-111">服务器会按原样呈现 *.cshtml* Razor 文件中的 HTML 标记。</span><span class="sxs-lookup"><span data-stu-id="206d2-111">HTML markup in *.cshtml* Razor files is rendered by the server unchanged.</span></span>

## <a name="razor-syntax"></a><span data-ttu-id="206d2-112">Razor 语法</span><span class="sxs-lookup"><span data-stu-id="206d2-112">Razor syntax</span></span>

<span data-ttu-id="206d2-113">Razor 支持 C#，并使用 `@` 符号从 HTML 转换为 C#。</span><span class="sxs-lookup"><span data-stu-id="206d2-113">Razor supports C# and uses the `@` symbol to transition from HTML to C#.</span></span> <span data-ttu-id="206d2-114">Razor 计算 C# 表达式，并将它们呈现在 HTML 输出中。</span><span class="sxs-lookup"><span data-stu-id="206d2-114">Razor evaluates C# expressions and renders them in the HTML output.</span></span>

<span data-ttu-id="206d2-115">当 `@` 符号后跟 [Razor 保留关键字](#razor-reserved-keywords)时，它会转换为 Razor 特定标记。</span><span class="sxs-lookup"><span data-stu-id="206d2-115">When an `@` symbol is followed by a [Razor reserved keyword](#razor-reserved-keywords), it transitions into Razor-specific markup.</span></span> <span data-ttu-id="206d2-116">否则会转换为纯 C#。</span><span class="sxs-lookup"><span data-stu-id="206d2-116">Otherwise, it transitions into plain C#.</span></span>

<span data-ttu-id="206d2-117">若要对 Razor 标记中的 `@` 符号进行转义，请使用另一个 `@` 符号：</span><span class="sxs-lookup"><span data-stu-id="206d2-117">To escape an `@` symbol in Razor markup, use a second `@` symbol:</span></span>

```cshtml
<p>@@Username</p>
```

<span data-ttu-id="206d2-118">该代码在 HTML 中使用单个 `@` 符号呈现：</span><span class="sxs-lookup"><span data-stu-id="206d2-118">The code is rendered in HTML with a single `@` symbol:</span></span>

```html
<p>@Username</p>
```

<span data-ttu-id="206d2-119">包含电子邮件地址的 HTML 属性和内容不将 `@` 符号视为转换字符。</span><span class="sxs-lookup"><span data-stu-id="206d2-119">HTML attributes and content containing email addresses don't treat the `@` symbol as a transition character.</span></span> <span data-ttu-id="206d2-120">Razor 分析不会处理以下示例中的电子邮件地址：</span><span class="sxs-lookup"><span data-stu-id="206d2-120">The email addresses in the following example are untouched by Razor parsing:</span></span>

```cshtml
<a href="mailto:Support@contoso.com">Support@contoso.com</a>
```

## <a name="implicit-razor-expressions"></a><span data-ttu-id="206d2-121">隐式 Razor 表达式</span><span class="sxs-lookup"><span data-stu-id="206d2-121">Implicit Razor expressions</span></span>

<span data-ttu-id="206d2-122">隐式 Razor 表达式以 `@` 开头，后跟 C# 代码：</span><span class="sxs-lookup"><span data-stu-id="206d2-122">Implicit Razor expressions start with `@` followed by C# code:</span></span>

```cshtml
<p>@DateTime.Now</p>
<p>@DateTime.IsLeapYear(2016)</p>
```

<span data-ttu-id="206d2-123">隐式表达式不能包含空格，但 C# `await` 关键字除外。</span><span class="sxs-lookup"><span data-stu-id="206d2-123">With the exception of the C# `await` keyword, implicit expressions must not contain spaces.</span></span> <span data-ttu-id="206d2-124">如果该 C# 语句具有明确的结束标记，则可以混用空格：</span><span class="sxs-lookup"><span data-stu-id="206d2-124">If the C# statement has a clear ending, spaces can be intermingled:</span></span>

```cshtml
<p>@await DoSomething("hello", "world")</p>
```

<span data-ttu-id="206d2-125">隐式表达式**不能**包含 C# 泛型，因为括号 (`<>`) 内的字符会被解释为 HTML 标记。</span><span class="sxs-lookup"><span data-stu-id="206d2-125">Implicit expressions **cannot** contain C# generics, as the characters inside the brackets (`<>`) are interpreted as an HTML tag.</span></span> <span data-ttu-id="206d2-126">以下代码**无**效：</span><span class="sxs-lookup"><span data-stu-id="206d2-126">The following code is **not** valid:</span></span>

```cshtml
<p>@GenericMethod<int>()</p>
```

<span data-ttu-id="206d2-127">上述代码生成与以下错误之一类似的编译器错误：</span><span class="sxs-lookup"><span data-stu-id="206d2-127">The preceding code generates a compiler error similar to one of the following:</span></span>

 * <span data-ttu-id="206d2-128">"int" 元素未结束。</span><span class="sxs-lookup"><span data-stu-id="206d2-128">The "int" element wasn't closed.</span></span> <span data-ttu-id="206d2-129">所有元素都必须自结束或具有匹配的结束标记。</span><span class="sxs-lookup"><span data-stu-id="206d2-129">All elements must be either self-closing or have a matching end tag.</span></span>
 *  <span data-ttu-id="206d2-130">无法将方法组 "GenericMethod" 转换为非委托类型 "object"。</span><span class="sxs-lookup"><span data-stu-id="206d2-130">Cannot convert method group 'GenericMethod' to non-delegate type 'object'.</span></span> <span data-ttu-id="206d2-131">是否希望调用此方法?\`</span><span class="sxs-lookup"><span data-stu-id="206d2-131">Did you intend to invoke the method?\`</span></span> 
 
<span data-ttu-id="206d2-132">泛型方法调用必须包装在[显式 Razor 表达式](#explicit-razor-expressions)或 [Razor 代码块](#razor-code-blocks)中。</span><span class="sxs-lookup"><span data-stu-id="206d2-132">Generic method calls must be wrapped in an [explicit Razor expression](#explicit-razor-expressions) or a [Razor code block](#razor-code-blocks).</span></span>

## <a name="explicit-razor-expressions"></a><span data-ttu-id="206d2-133">显式 Razor 表达式</span><span class="sxs-lookup"><span data-stu-id="206d2-133">Explicit Razor expressions</span></span>

<span data-ttu-id="206d2-134">显式 Razor 表达式由 `@` 符号和平衡圆括号组成。</span><span class="sxs-lookup"><span data-stu-id="206d2-134">Explicit Razor expressions consist of an `@` symbol with balanced parenthesis.</span></span> <span data-ttu-id="206d2-135">若要呈现上一周的时间，可使用以下 Razor 标记：</span><span class="sxs-lookup"><span data-stu-id="206d2-135">To render last week's time, the following Razor markup is used:</span></span>

```cshtml
<p>Last week this time: @(DateTime.Now - TimeSpan.FromDays(7))</p>
```

<span data-ttu-id="206d2-136">将计算 `@()` 括号中的所有内容，并将其呈现到输出中。</span><span class="sxs-lookup"><span data-stu-id="206d2-136">Any content within the `@()` parenthesis is evaluated and rendered to the output.</span></span>

<span data-ttu-id="206d2-137">前面部分中所述的隐式表达式通常不能包含空格。</span><span class="sxs-lookup"><span data-stu-id="206d2-137">Implicit expressions, described in the previous section, generally can't contain spaces.</span></span> <span data-ttu-id="206d2-138">在下面的代码中，不会从当前时间减去一周：</span><span class="sxs-lookup"><span data-stu-id="206d2-138">In the following code, one week isn't subtracted from the current time:</span></span>

[!code-cshtml[](razor/sample/Views/Home/Contact.cshtml?range=17)]

<span data-ttu-id="206d2-139">该代码呈现以下 HTML：</span><span class="sxs-lookup"><span data-stu-id="206d2-139">The code renders the following HTML:</span></span>

```html
<p>Last week: 7/7/2016 4:39:52 PM - TimeSpan.FromDays(7)</p>
```

<span data-ttu-id="206d2-140">可以使用显式表达式将文本与表达式结果串联起来：</span><span class="sxs-lookup"><span data-stu-id="206d2-140">Explicit expressions can be used to concatenate text with an expression result:</span></span>

```cshtml
@{
    var joe = new Person("Joe", 33);
}

<p>Age@(joe.Age)</p>
```

<span data-ttu-id="206d2-141">如果不使用显式表达式，`<p>Age@joe.Age</p>` 会被视为电子邮件地址，因此会呈现 `<p>Age@joe.Age</p>`。</span><span class="sxs-lookup"><span data-stu-id="206d2-141">Without the explicit expression, `<p>Age@joe.Age</p>` is treated as an email address, and `<p>Age@joe.Age</p>` is rendered.</span></span> <span data-ttu-id="206d2-142">如果编写为显式表达式，则呈现 `<p>Age33</p>`。</span><span class="sxs-lookup"><span data-stu-id="206d2-142">When written as an explicit expression, `<p>Age33</p>` is rendered.</span></span>

<span data-ttu-id="206d2-143">显式表达式可用于从 *.cshtml* 文件中的泛型方法呈现输出。</span><span class="sxs-lookup"><span data-stu-id="206d2-143">Explicit expressions can be used to render output from generic methods in *.cshtml* files.</span></span> <span data-ttu-id="206d2-144">以下标记显示了如何更正之前出现的由 C# 泛型的括号引起的错误。</span><span class="sxs-lookup"><span data-stu-id="206d2-144">The following markup shows how to correct the error shown earlier caused by the brackets of a C# generic.</span></span> <span data-ttu-id="206d2-145">此代码以显式表达式的形式编写：</span><span class="sxs-lookup"><span data-stu-id="206d2-145">The code is written as an explicit expression:</span></span>

```cshtml
<p>@(GenericMethod<int>())</p>
```

## <a name="expression-encoding"></a><span data-ttu-id="206d2-146">表达式编码</span><span class="sxs-lookup"><span data-stu-id="206d2-146">Expression encoding</span></span>

<span data-ttu-id="206d2-147">计算结果为字符串的 C# 表达式采用 HTML 编码。</span><span class="sxs-lookup"><span data-stu-id="206d2-147">C# expressions that evaluate to a string are HTML encoded.</span></span> <span data-ttu-id="206d2-148">计算结果为 `IHtmlContent` 的 C# 表达式直接通过 `IHtmlContent.WriteTo` 呈现。</span><span class="sxs-lookup"><span data-stu-id="206d2-148">C# expressions that evaluate to `IHtmlContent` are rendered directly through `IHtmlContent.WriteTo`.</span></span> <span data-ttu-id="206d2-149">计算结果不为 `IHtmlContent` 的 C# 表达式通过 `ToString` 转换为字符串，并在呈现前进行编码。</span><span class="sxs-lookup"><span data-stu-id="206d2-149">C# expressions that don't evaluate to `IHtmlContent` are converted to a string by `ToString` and encoded before they're rendered.</span></span>

```cshtml
@("<span>Hello World</span>")
```

<span data-ttu-id="206d2-150">该代码呈现以下 HTML：</span><span class="sxs-lookup"><span data-stu-id="206d2-150">The code renders the following HTML:</span></span>

```html
&lt;span&gt;Hello World&lt;/span&gt;
```

<span data-ttu-id="206d2-151">该 HTML 在浏览器中显示为：</span><span class="sxs-lookup"><span data-stu-id="206d2-151">The HTML is shown in the browser as:</span></span>

```
<span>Hello World</span>
```

<span data-ttu-id="206d2-152">`HtmlHelper.Raw` 输出不进行编码，但呈现为 HTML 标记。</span><span class="sxs-lookup"><span data-stu-id="206d2-152">`HtmlHelper.Raw` output isn't encoded but rendered as HTML markup.</span></span>

> [!WARNING]
> <span data-ttu-id="206d2-153">对未经审查的用户输入使用 `HtmlHelper.Raw` 会带来安全风险。</span><span class="sxs-lookup"><span data-stu-id="206d2-153">Using `HtmlHelper.Raw` on unsanitized user input is a security risk.</span></span> <span data-ttu-id="206d2-154">用户输入可能包含恶意的 JavaScript 或其他攻击。</span><span class="sxs-lookup"><span data-stu-id="206d2-154">User input might contain malicious JavaScript or other exploits.</span></span> <span data-ttu-id="206d2-155">审查用户输入比较困难。</span><span class="sxs-lookup"><span data-stu-id="206d2-155">Sanitizing user input is difficult.</span></span> <span data-ttu-id="206d2-156">应避免对用户输入使用 `HtmlHelper.Raw`。</span><span class="sxs-lookup"><span data-stu-id="206d2-156">Avoid using `HtmlHelper.Raw` with user input.</span></span>

```cshtml
@Html.Raw("<span>Hello World</span>")
```

<span data-ttu-id="206d2-157">该代码呈现以下 HTML：</span><span class="sxs-lookup"><span data-stu-id="206d2-157">The code renders the following HTML:</span></span>

```html
<span>Hello World</span>
```

## <a name="razor-code-blocks"></a><span data-ttu-id="206d2-158">Razor 代码块</span><span class="sxs-lookup"><span data-stu-id="206d2-158">Razor code blocks</span></span>

<span data-ttu-id="206d2-159">Razor 代码块以 `@` 开头，并括在 `{}` 中。</span><span class="sxs-lookup"><span data-stu-id="206d2-159">Razor code blocks start with `@` and are enclosed by `{}`.</span></span> <span data-ttu-id="206d2-160">代码块内的 C# 代码不会呈现，这点与表达式不同。</span><span class="sxs-lookup"><span data-stu-id="206d2-160">Unlike expressions, C# code inside code blocks isn't rendered.</span></span> <span data-ttu-id="206d2-161">一个视图中的代码块和表达式共享相同的作用域并按顺序进行定义：</span><span class="sxs-lookup"><span data-stu-id="206d2-161">Code blocks and expressions in a view share the same scope and are defined in order:</span></span>

```cshtml
@{
    var quote = "The future depends on what you do today. - Mahatma Gandhi";
}

<p>@quote</p>

@{
    quote = "Hate cannot drive out hate, only love can do that. - Martin Luther King, Jr.";
}

<p>@quote</p>
```

<span data-ttu-id="206d2-162">该代码呈现以下 HTML：</span><span class="sxs-lookup"><span data-stu-id="206d2-162">The code renders the following HTML:</span></span>

```html
<p>The future depends on what you do today. - Mahatma Gandhi</p>
<p>Hate cannot drive out hate, only love can do that. - Martin Luther King, Jr.</p>
```

### <a name="implicit-transitions"></a><span data-ttu-id="206d2-163">隐式转换</span><span class="sxs-lookup"><span data-stu-id="206d2-163">Implicit transitions</span></span>

<span data-ttu-id="206d2-164">代码块中的默认语言为 C#，不过，Razor 页面可以转换回 HTML：</span><span class="sxs-lookup"><span data-stu-id="206d2-164">The default language in a code block is C#, but the Razor Page can transition back to HTML:</span></span>

```cshtml
@{
    var inCSharp = true;
    <p>Now in HTML, was in C# @inCSharp</p>
}
```

### <a name="explicit-delimited-transition"></a><span data-ttu-id="206d2-165">带分隔符的显式转换</span><span class="sxs-lookup"><span data-stu-id="206d2-165">Explicit delimited transition</span></span>

<span data-ttu-id="206d2-166">若要定义应呈现 HTML 的代码块子节，请使用 Razor **\<text>** 标记将要呈现的字符括起来：</span><span class="sxs-lookup"><span data-stu-id="206d2-166">To define a subsection of a code block that should render HTML, surround the characters for rendering with the Razor **\<text>** tag:</span></span>

```cshtml
@for (var i = 0; i < people.Length; i++)
{
    var person = people[i];
    <text>Name: @person.Name</text>
}
```

<span data-ttu-id="206d2-167">使用此方法可呈现未被 HTML 标记括起来的 HTML。</span><span class="sxs-lookup"><span data-stu-id="206d2-167">Use this approach to render HTML that isn't surrounded by an HTML tag.</span></span> <span data-ttu-id="206d2-168">如果没有 HTML 或 Razor 标记，会发生 Razor 运行时错误。</span><span class="sxs-lookup"><span data-stu-id="206d2-168">Without an HTML or Razor tag, a Razor runtime error occurs.</span></span>

<span data-ttu-id="206d2-169">**\<text>** 标记可用于在呈现内容时控制空格：</span><span class="sxs-lookup"><span data-stu-id="206d2-169">The **\<text>** tag is useful to control whitespace when rendering content:</span></span>

* <span data-ttu-id="206d2-170">仅呈现 **\<text>** 标记之间的内容。</span><span class="sxs-lookup"><span data-stu-id="206d2-170">Only the content between the **\<text>** tag is rendered.</span></span> 
* <span data-ttu-id="206d2-171">**\<text>** 标记之前或之后的空格不会显示在 HTML 输出中。</span><span class="sxs-lookup"><span data-stu-id="206d2-171">No whitespace before or after the **\<text>** tag appears in the HTML output.</span></span>

### <a name="explicit-line-transition-with-"></a><span data-ttu-id="206d2-172">使用 @ 的显式行转换：</span><span class="sxs-lookup"><span data-stu-id="206d2-172">Explicit Line Transition with @:</span></span>

<span data-ttu-id="206d2-173">若要在代码块内以 HTML 的形式呈现整个行的其余内容，请使用 `@:` 语法：</span><span class="sxs-lookup"><span data-stu-id="206d2-173">To render the rest of an entire line as HTML inside a code block, use the `@:` syntax:</span></span>

```cshtml
@for (var i = 0; i < people.Length; i++)
{
    var person = people[i];
    @:Name: @person.Name
}
```

<span data-ttu-id="206d2-174">如果代码中没有 `@:`，会生成 Razor 运行时错误。</span><span class="sxs-lookup"><span data-stu-id="206d2-174">Without the `@:` in the code, a Razor runtime error is generated.</span></span>

<span data-ttu-id="206d2-175">警告：Razor 文件中多余的 `@` 字符可能会导致代码块中后面的语句发生编译器错误。</span><span class="sxs-lookup"><span data-stu-id="206d2-175">Warning: Extra `@` characters in a Razor file can cause compiler errors at statements later in the block.</span></span> <span data-ttu-id="206d2-176">这些编译器错误可能难以理解，因为实际错误发生在报告的错误之前。</span><span class="sxs-lookup"><span data-stu-id="206d2-176">These compiler errors can be difficult to understand because the actual error occurs before the reported error.</span></span> <span data-ttu-id="206d2-177">将多个隐式/显式表达式合并到单个代码块以后，经常会发生此错误。</span><span class="sxs-lookup"><span data-stu-id="206d2-177">This error is common after combining multiple implicit/explicit expressions into a single code block.</span></span>

## <a name="control-structures"></a><span data-ttu-id="206d2-178">控制结构</span><span class="sxs-lookup"><span data-stu-id="206d2-178">Control structures</span></span>

<span data-ttu-id="206d2-179">控制结构是对代码块的扩展。</span><span class="sxs-lookup"><span data-stu-id="206d2-179">Control structures are an extension of code blocks.</span></span> <span data-ttu-id="206d2-180">代码块的各个方面（转换为标记、内联 C#）同样适用于以下结构：</span><span class="sxs-lookup"><span data-stu-id="206d2-180">All aspects of code blocks (transitioning to markup, inline C#) also apply to the following structures:</span></span>

### <a name="conditionals-if-else-if-else-and-switch"></a><span data-ttu-id="206d2-181">条件语句 @if、else if、else 和 @switch</span><span class="sxs-lookup"><span data-stu-id="206d2-181">Conditionals @if, else if, else, and @switch</span></span>

<span data-ttu-id="206d2-182">`@if` 控制何时运行代码：</span><span class="sxs-lookup"><span data-stu-id="206d2-182">`@if` controls when code runs:</span></span>

```cshtml
@if (value % 2 == 0)
{
    <p>The value was even.</p>
}
```

<span data-ttu-id="206d2-183">`else` 和 `else if` 不需要 `@` 符号：</span><span class="sxs-lookup"><span data-stu-id="206d2-183">`else` and `else if` don't require the `@` symbol:</span></span>

```cshtml
@if (value % 2 == 0)
{
    <p>The value was even.</p>
}
else if (value >= 1337)
{
    <p>The value is large.</p>
}
else
{
    <p>The value is odd and small.</p>
}
```

<span data-ttu-id="206d2-184">以下标记展示如何使用 switch 语句：</span><span class="sxs-lookup"><span data-stu-id="206d2-184">The following markup shows how to use a switch statement:</span></span>

```cshtml
@switch (value)
{
    case 1:
        <p>The value is 1!</p>
        break;
    case 1337:
        <p>Your number is 1337!</p>
        break;
    default:
        <p>Your number wasn't 1 or 1337.</p>
        break;
}
```

### <a name="looping-for-foreach-while-and-do-while"></a><span data-ttu-id="206d2-185">循环语句 @for、@foreach、@while 和 @do while</span><span class="sxs-lookup"><span data-stu-id="206d2-185">Looping @for, @foreach, @while, and @do while</span></span>

<span data-ttu-id="206d2-186">可以使用循环控制语句呈现模板化 HTML。</span><span class="sxs-lookup"><span data-stu-id="206d2-186">Templated HTML can be rendered with looping control statements.</span></span> <span data-ttu-id="206d2-187">若要呈现一组人员：</span><span class="sxs-lookup"><span data-stu-id="206d2-187">To render a list of people:</span></span>

```cshtml
@{
    var people = new Person[]
    {
          new Person("Weston", 33),
          new Person("Johnathon", 41),
          ...
    };
}
```

<span data-ttu-id="206d2-188">支持以下循环语句：</span><span class="sxs-lookup"><span data-stu-id="206d2-188">The following looping statements are supported:</span></span>

`@for`

```cshtml
@for (var i = 0; i < people.Length; i++)
{
    var person = people[i];
    <p>Name: @person.Name</p>
    <p>Age: @person.Age</p>
}
```

`@foreach`

```cshtml
@foreach (var person in people)
{
    <p>Name: @person.Name</p>
    <p>Age: @person.Age</p>
}
```

`@while`

```cshtml
@{ var i = 0; }
@while (i < people.Length)
{
    var person = people[i];
    <p>Name: @person.Name</p>
    <p>Age: @person.Age</p>

    i++;
}
```

`@do while`

```cshtml
@{ var i = 0; }
@do
{
    var person = people[i];
    <p>Name: @person.Name</p>
    <p>Age: @person.Age</p>

    i++;
} while (i < people.Length);
```

### <a name="compound-using"></a><span data-ttu-id="206d2-189">复合语句 @using</span><span class="sxs-lookup"><span data-stu-id="206d2-189">Compound @using</span></span>

<span data-ttu-id="206d2-190">在 C# 中，`using` 语句用于确保释放对象。</span><span class="sxs-lookup"><span data-stu-id="206d2-190">In C#, a `using` statement is used to ensure an object is disposed.</span></span> <span data-ttu-id="206d2-191">在 Razor 中，可使用相同的机制来创建包含附加内容的 HTML 帮助程序。</span><span class="sxs-lookup"><span data-stu-id="206d2-191">In Razor, the same mechanism is used to create HTML Helpers that contain additional content.</span></span> <span data-ttu-id="206d2-192">在下面的代码中，HTML 帮助程序使用 `@using` 语句呈现表单标记：</span><span class="sxs-lookup"><span data-stu-id="206d2-192">In the following code, HTML Helpers render a form tag with the `@using` statement:</span></span>


```cshtml
@using (Html.BeginForm())
{
    <div>
        email:
        <input type="email" id="Email" value="">
        <button>Register</button>
    </div>
}
```

<span data-ttu-id="206d2-193">可以使用[标记帮助程序](xref:mvc/views/tag-helpers/intro)执行作用域级别的操作。</span><span class="sxs-lookup"><span data-stu-id="206d2-193">Scope-level actions can be performed with [Tag Helpers](xref:mvc/views/tag-helpers/intro).</span></span>

### <a name="try-catch-finally"></a><span data-ttu-id="206d2-194">@try、catch、finally</span><span class="sxs-lookup"><span data-stu-id="206d2-194">@try, catch, finally</span></span>

<span data-ttu-id="206d2-195">异常处理与 C# 类似：</span><span class="sxs-lookup"><span data-stu-id="206d2-195">Exception handling is similar to C#:</span></span>

[!code-cshtml[](razor/sample/Views/Home/Contact7.cshtml)]

### <a name="lock"></a>@lock

<span data-ttu-id="206d2-196">Razor 可以使用 lock 语句来保护关键节：</span><span class="sxs-lookup"><span data-stu-id="206d2-196">Razor has the capability to protect critical sections with lock statements:</span></span>

```cshtml
@lock (SomeLock)
{
    // Do critical section work
}
```

### <a name="comments"></a><span data-ttu-id="206d2-197">注释</span><span class="sxs-lookup"><span data-stu-id="206d2-197">Comments</span></span>

<span data-ttu-id="206d2-198">Razor 支持 C# 和 HTML 注释：</span><span class="sxs-lookup"><span data-stu-id="206d2-198">Razor supports C# and HTML comments:</span></span>

```cshtml
@{
    /* C# comment */
    // Another C# comment
}
<!-- HTML comment -->
```

<span data-ttu-id="206d2-199">该代码呈现以下 HTML：</span><span class="sxs-lookup"><span data-stu-id="206d2-199">The code renders the following HTML:</span></span>

```html
<!-- HTML comment -->
```

<span data-ttu-id="206d2-200">在呈现网页之前，服务器会删除 Razor 注释。</span><span class="sxs-lookup"><span data-stu-id="206d2-200">Razor comments are removed by the server before the webpage is rendered.</span></span> <span data-ttu-id="206d2-201">Razor 使用 `@*  *@` 来分隔注释。</span><span class="sxs-lookup"><span data-stu-id="206d2-201">Razor uses `@*  *@` to delimit comments.</span></span> <span data-ttu-id="206d2-202">以下代码已被注释禁止，因此服务器不呈现任何标记：</span><span class="sxs-lookup"><span data-stu-id="206d2-202">The following code is commented out, so the server doesn't render any markup:</span></span>

```cshtml
@*
    @{
        /* C# comment */
        // Another C# comment
    }
    <!-- HTML comment -->
*@
```

## <a name="directives"></a><span data-ttu-id="206d2-203">指令</span><span class="sxs-lookup"><span data-stu-id="206d2-203">Directives</span></span>

<span data-ttu-id="206d2-204">Razor 指令由隐式表达式表示：`@` 符号后跟保留关键字。</span><span class="sxs-lookup"><span data-stu-id="206d2-204">Razor directives are represented by implicit expressions with reserved keywords following the `@` symbol.</span></span> <span data-ttu-id="206d2-205">指令通常用于更改视图分析方式或启用不同的功能。</span><span class="sxs-lookup"><span data-stu-id="206d2-205">A directive typically changes the way a view is parsed or enables different functionality.</span></span>

<span data-ttu-id="206d2-206">通过了解 Razor 如何为视图生成代码，更易理解指令的工作原理。</span><span class="sxs-lookup"><span data-stu-id="206d2-206">Understanding how Razor generates code for a view makes it easier to understand how directives work.</span></span>

[!code-cshtml[](razor/sample/Views/Home/Contact8.cshtml)]

<span data-ttu-id="206d2-207">该代码生成与下面类似的类：</span><span class="sxs-lookup"><span data-stu-id="206d2-207">The code generates a class similar to the following:</span></span>

```csharp
public class _Views_Something_cshtml : RazorPage<dynamic>
{
    public override async Task ExecuteAsync()
    {
        var output = "Getting old ain't for wimps! - Anonymous";

        WriteLiteral("/r/n<div>Quote of the Day: ");
        Write(output);
        WriteLiteral("</div>");
    }
}
```

<span data-ttu-id="206d2-208">本文后面的[检查为视图生成的 Razor C# 类](#inspect-the-razor-c-class-generated-for-a-view)部分说明了如何查看此生成的类。</span><span class="sxs-lookup"><span data-stu-id="206d2-208">Later in this article, the section [Inspect the Razor C# class generated for a view](#inspect-the-razor-c-class-generated-for-a-view) explains how to view this generated class.</span></span>

<a name="using"></a>
### <a name="using"></a>@using

<span data-ttu-id="206d2-209">`@using` 指令用于向生成的视图添加 C# `using` 指令：</span><span class="sxs-lookup"><span data-stu-id="206d2-209">The `@using` directive adds the C# `using` directive to the generated view:</span></span>

[!code-cshtml[](razor/sample/Views/Home/Contact9.cshtml)]

### <a name="model"></a>@model

<span data-ttu-id="206d2-210">`@model` 指令指定传递到视图的模型类型：</span><span class="sxs-lookup"><span data-stu-id="206d2-210">The `@model` directive specifies the type of the model passed to a view:</span></span>

```cshtml
@model TypeNameOfModel
```

<span data-ttu-id="206d2-211">在使用个人用户帐户创建的 ASP.NET Core MVC 应用中，*Views/Account/Login.cshtml* 视图包含以下模型声明：</span><span class="sxs-lookup"><span data-stu-id="206d2-211">In an ASP.NET Core MVC app created with individual user accounts, the *Views/Account/Login.cshtml* view contains the following model declaration:</span></span>

```cshtml
@model LoginViewModel
```

<span data-ttu-id="206d2-212">生成的类继承自 `RazorPage<dynamic>`：</span><span class="sxs-lookup"><span data-stu-id="206d2-212">The class generated inherits from `RazorPage<dynamic>`:</span></span>

```csharp
public class _Views_Account_Login_cshtml : RazorPage<LoginViewModel>
```

<span data-ttu-id="206d2-213">Razor 公开了 `Model` 属性，用于访问传递到视图的模型：</span><span class="sxs-lookup"><span data-stu-id="206d2-213">Razor exposes a `Model` property for accessing the model passed to the view:</span></span>

```cshtml
<div>The Login Email: @Model.Email</div>
```

<span data-ttu-id="206d2-214">`@model` 指令指定此属性的类型。</span><span class="sxs-lookup"><span data-stu-id="206d2-214">The `@model` directive specifies the type of this property.</span></span> <span data-ttu-id="206d2-215">该指令将 `RazorPage<T>` 中的 `T` 指定为生成的类，视图便派生自该类。</span><span class="sxs-lookup"><span data-stu-id="206d2-215">The directive specifies the `T` in `RazorPage<T>` that the generated class that the view derives from.</span></span> <span data-ttu-id="206d2-216">如果未指定 `@model` 指令，则 `Model` 属性的类型为 `dynamic`。</span><span class="sxs-lookup"><span data-stu-id="206d2-216">If the `@model` directive isn't specified, the `Model` property is of type `dynamic`.</span></span> <span data-ttu-id="206d2-217">模型的值会从控制器传递到视图。</span><span class="sxs-lookup"><span data-stu-id="206d2-217">The value of the model is passed from the controller to the view.</span></span> <span data-ttu-id="206d2-218">有关详细信息，请参阅[强类型模型和&commat;模型关键字](xref:tutorials/first-mvc-app/adding-model#strongly-typed-models-and-the--keyword)。</span><span class="sxs-lookup"><span data-stu-id="206d2-218">For more information, see [Strongly typed models and the &commat;model keyword](xref:tutorials/first-mvc-app/adding-model#strongly-typed-models-and-the--keyword).</span></span>

### <a name="inherits"></a>@inherits

<span data-ttu-id="206d2-219">`@inherits` 指令对视图继承的类提供完全控制：</span><span class="sxs-lookup"><span data-stu-id="206d2-219">The `@inherits` directive provides full control of the class the view inherits:</span></span>

```cshtml
@inherits TypeNameOfClassToInheritFrom
```

<span data-ttu-id="206d2-220">下面的代码是一种自定义 Razor 页面类型：</span><span class="sxs-lookup"><span data-stu-id="206d2-220">The following code is a custom Razor page type:</span></span>

[!code-csharp[](razor/sample/Classes/CustomRazorPage.cs)]

<span data-ttu-id="206d2-221">`CustomText` 显示在视图中：</span><span class="sxs-lookup"><span data-stu-id="206d2-221">The `CustomText` is displayed in a view:</span></span>

[!code-cshtml[](razor/sample/Views/Home/Contact10.cshtml)]

<span data-ttu-id="206d2-222">该代码呈现以下 HTML：</span><span class="sxs-lookup"><span data-stu-id="206d2-222">The code renders the following HTML:</span></span>

```html
<div>Custom text: Gardyloo! - A Scottish warning yelled from a window before dumping a slop bucket on the street below.</div>
```

 <span data-ttu-id="206d2-223">`@model` 和 `@inherits` 可在同一视图中使用。</span><span class="sxs-lookup"><span data-stu-id="206d2-223">`@model` and `@inherits` can be used in the same view.</span></span> <span data-ttu-id="206d2-224">`@inherits` 可位于视图导入的 *_ViewImports.cshtml* 文件中：</span><span class="sxs-lookup"><span data-stu-id="206d2-224">`@inherits` can be in a *_ViewImports.cshtml* file that the view imports:</span></span>

[!code-cshtml[](razor/sample/Views/_ViewImportsModel.cshtml)]

<span data-ttu-id="206d2-225">下面的代码是一种强类型视图：</span><span class="sxs-lookup"><span data-stu-id="206d2-225">The following code is an example of a strongly-typed view:</span></span>

[!code-cshtml[](razor/sample/Views/Home/Login1.cshtml)]

<span data-ttu-id="206d2-226">如果在模型中传递“rick@contoso.com”，视图将生成以下 HTML 标记：</span><span class="sxs-lookup"><span data-stu-id="206d2-226">If "rick@contoso.com" is passed in the model, the view generates the following HTML markup:</span></span>

```html
<div>The Login Email: rick@contoso.com</div>
<div>Custom text: Gardyloo! - A Scottish warning yelled from a window before dumping a slop bucket on the street below.</div>
```

### <a name="inject"></a>@inject

<span data-ttu-id="206d2-227">`@inject` 指令允许 Razor 页面将服务从[服务容器](xref:fundamentals/dependency-injection)注入到视图。</span><span class="sxs-lookup"><span data-stu-id="206d2-227">The `@inject` directive enables the Razor Page to inject a service from the [service container](xref:fundamentals/dependency-injection) into a view.</span></span> <span data-ttu-id="206d2-228">有关详细信息，请参阅[视图中的依赖关系注入](xref:mvc/views/dependency-injection)。</span><span class="sxs-lookup"><span data-stu-id="206d2-228">For more information, see [Dependency injection into views](xref:mvc/views/dependency-injection).</span></span>

### <a name="functions"></a>@functions

<span data-ttu-id="206d2-229">`@functions` 指令允许 Razor 页面将 C# 代码块添加到视图中：</span><span class="sxs-lookup"><span data-stu-id="206d2-229">The `@functions` directive enables a Razor Page to add a C# code block to a view:</span></span>

```cshtml
@functions { // C# Code }
```

<span data-ttu-id="206d2-230">例如:</span><span class="sxs-lookup"><span data-stu-id="206d2-230">For example:</span></span>

[!code-cshtml[](razor/sample/Views/Home/Contact6.cshtml)]

<span data-ttu-id="206d2-231">该代码生成以下 HTML 标记：</span><span class="sxs-lookup"><span data-stu-id="206d2-231">The code generates the following HTML markup:</span></span>

```html
<div>From method: Hello</div>
```

<span data-ttu-id="206d2-232">以下代码是生成的 Razor C# 类：</span><span class="sxs-lookup"><span data-stu-id="206d2-232">The following code is the generated Razor C# class:</span></span>

[!code-csharp[](razor/sample/Classes/Views_Home_Test_cshtml.cs?range=1-19)]

### <a name="section"></a>@section

<span data-ttu-id="206d2-233">`@section` 指令与[布局](xref:mvc/views/layout)结合使用，允许视图将内容呈现在 HTML 页面的不同部分。</span><span class="sxs-lookup"><span data-stu-id="206d2-233">The `@section` directive is used in conjunction with the [layout](xref:mvc/views/layout) to enable views to render content in different parts of the HTML page.</span></span> <span data-ttu-id="206d2-234">有关详细信息，请参阅[部分](xref:mvc/views/layout#layout-sections-label)。</span><span class="sxs-lookup"><span data-stu-id="206d2-234">For more information, see [Sections](xref:mvc/views/layout#layout-sections-label).</span></span>

## <a name="templated-razor-delegates"></a><span data-ttu-id="206d2-235">模板化 Razor 委托</span><span class="sxs-lookup"><span data-stu-id="206d2-235">Templated Razor delegates</span></span>

<span data-ttu-id="206d2-236">通过 Razor 模板，可使用以下格式定义 UI 代码片段：</span><span class="sxs-lookup"><span data-stu-id="206d2-236">Razor templates allow you to define a UI snippet with the following format:</span></span>

```cshtml
@<tag>...</tag>
```

<span data-ttu-id="206d2-237">下面的示例演示如何指定模板化 Razor 委托作为 <xref:System.Func`2>。</span><span class="sxs-lookup"><span data-stu-id="206d2-237">The following example illustrates how to specify a templated Razor delegate as a <xref:System.Func`2>.</span></span> <span data-ttu-id="206d2-238">为委托封装的方法的参数指定[动态类型](/dotnet/csharp/programming-guide/types/using-type-dynamic)。</span><span class="sxs-lookup"><span data-stu-id="206d2-238">The [dynamic type](/dotnet/csharp/programming-guide/types/using-type-dynamic) is specified for the parameter of the method that the delegate encapsulates.</span></span> <span data-ttu-id="206d2-239">将[对象类型](/dotnet/csharp/language-reference/keywords/object)指定为委托的返回值。</span><span class="sxs-lookup"><span data-stu-id="206d2-239">An [object type](/dotnet/csharp/language-reference/keywords/object) is specified as the return value of the delegate.</span></span> <span data-ttu-id="206d2-240">该模板与 `Pet`（具有 `Name` 属性）的 <xref:System.Collections.Generic.List`1> 一起使用。</span><span class="sxs-lookup"><span data-stu-id="206d2-240">The template is used with a <xref:System.Collections.Generic.List`1> of `Pet` that has a `Name` property.</span></span>

```csharp
public class Pet
{
    public string Name { get; set; }
}
```

```cshtml
@{
    Func<dynamic, object> petTemplate = @<p>You have a pet named <strong>@item.Name</strong>.</p>;

    var pets = new List<Pet>
    {
        new Pet { Name = "Rin Tin Tin" },
        new Pet { Name = "Mr. Bigglesworth" },
        new Pet { Name = "K-9" }
    };
}
```

<span data-ttu-id="206d2-241">使用 `foreach` 语句提供的 `pets` 呈现该模板：</span><span class="sxs-lookup"><span data-stu-id="206d2-241">The template is rendered with `pets` supplied by a `foreach` statement:</span></span>

```cshtml
@foreach (var pet in pets)
{
    @petTemplate(pet)
}
```

<span data-ttu-id="206d2-242">呈现的输出：</span><span class="sxs-lookup"><span data-stu-id="206d2-242">Rendered output:</span></span>

```html
<p>You have a pet named <strong>Rin Tin Tin</strong>.</p>
<p>You have a pet named <strong>Mr. Bigglesworth</strong>.</p>
<p>You have a pet named <strong>K-9</strong>.</p>
```

<span data-ttu-id="206d2-243">还可以提供内联 Razor 模板作为方法的参数。</span><span class="sxs-lookup"><span data-stu-id="206d2-243">You can also supply an inline Razor template as an argument to a method.</span></span> <span data-ttu-id="206d2-244">如下示例中，`Repeat` 方法收到一个 Razor 模板。</span><span class="sxs-lookup"><span data-stu-id="206d2-244">In the following example, the `Repeat` method receives a Razor template.</span></span> <span data-ttu-id="206d2-245">该方法使用模板生成 HTML 内容，其中包含列表中提供的重复项：</span><span class="sxs-lookup"><span data-stu-id="206d2-245">The method uses the template to produce HTML content with repeats of items supplied from a list:</span></span>

```cshtml
@using Microsoft.AspNetCore.Html

@functions {
    public static IHtmlContent Repeat(IEnumerable<dynamic> items, int times, 
        Func<dynamic, IHtmlContent> template)
    {
        var html = new HtmlContentBuilder();

        foreach (var item in items)
        {
            for (var i = 0; i < times; i++)
            {
                html.AppendHtml(template(item));
            }
        }

        return html;
    }
}
```

<span data-ttu-id="206d2-246">使用前面示例中的 pets 列表，调用 `Repeat` 方法以及：</span><span class="sxs-lookup"><span data-stu-id="206d2-246">Using the list of pets from the prior example, the `Repeat` method is called with:</span></span>

* <span data-ttu-id="206d2-247">`Pet` 的 <xref:System.Collections.Generic.List`1>。</span><span class="sxs-lookup"><span data-stu-id="206d2-247"><xref:System.Collections.Generic.List`1> of `Pet`.</span></span>
* <span data-ttu-id="206d2-248">每只宠物的重复次数。</span><span class="sxs-lookup"><span data-stu-id="206d2-248">Number of times to repeat each pet.</span></span>
* <span data-ttu-id="206d2-249">用于无序列表的列表项的内联模板。</span><span class="sxs-lookup"><span data-stu-id="206d2-249">Inline template to use for the list items of an unordered list.</span></span>

```cshtml
<ul>
    @Repeat(pets, 3, @<li>@item.Name</li>)
</ul>
```

<span data-ttu-id="206d2-250">呈现的输出：</span><span class="sxs-lookup"><span data-stu-id="206d2-250">Rendered output:</span></span>

```html
<ul>
    <li>Rin Tin Tin</li>
    <li>Rin Tin Tin</li>
    <li>Rin Tin Tin</li>
    <li>Mr. Bigglesworth</li>
    <li>Mr. Bigglesworth</li>
    <li>Mr. Bigglesworth</li>
    <li>K-9</li>
    <li>K-9</li>
    <li>K-9</li>
</ul>
```

## <a name="tag-helpers"></a><span data-ttu-id="206d2-251">标记帮助程序</span><span class="sxs-lookup"><span data-stu-id="206d2-251">Tag Helpers</span></span>

<span data-ttu-id="206d2-252">[标记帮助程序](xref:mvc/views/tag-helpers/intro)有三个相关指令。</span><span class="sxs-lookup"><span data-stu-id="206d2-252">There are three directives that pertain to [Tag Helpers](xref:mvc/views/tag-helpers/intro).</span></span>

| <span data-ttu-id="206d2-253">指令</span><span class="sxs-lookup"><span data-stu-id="206d2-253">Directive</span></span> | <span data-ttu-id="206d2-254">函数</span><span class="sxs-lookup"><span data-stu-id="206d2-254">Function</span></span> |
| --------- | -------- |
| [<span data-ttu-id="206d2-255">&commat;addTagHelper</span><span class="sxs-lookup"><span data-stu-id="206d2-255">&commat;addTagHelper</span></span>](xref:mvc/views/tag-helpers/intro#add-helper-label) | <span data-ttu-id="206d2-256">向视图提供标记帮助程序。</span><span class="sxs-lookup"><span data-stu-id="206d2-256">Makes Tag Helpers available to a view.</span></span> |
| [<span data-ttu-id="206d2-257">&commat;removeTagHelper</span><span class="sxs-lookup"><span data-stu-id="206d2-257">&commat;removeTagHelper</span></span>](xref:mvc/views/tag-helpers/intro#remove-razor-directives-label) | <span data-ttu-id="206d2-258">从视图中删除以前添加的标记帮助程序。</span><span class="sxs-lookup"><span data-stu-id="206d2-258">Removes Tag Helpers previously added from a view.</span></span> |
| [<span data-ttu-id="206d2-259">&commat;tagHelperPrefix</span><span class="sxs-lookup"><span data-stu-id="206d2-259">&commat;tagHelperPrefix</span></span>](xref:mvc/views/tag-helpers/intro#prefix-razor-directives-label) | <span data-ttu-id="206d2-260">指定标记前缀，以启用标记帮助程序支持并阐明标记帮助程序的用法。</span><span class="sxs-lookup"><span data-stu-id="206d2-260">Specifies a tag prefix to enable Tag Helper support and to make Tag Helper usage explicit.</span></span> |

## <a name="razor-reserved-keywords"></a><span data-ttu-id="206d2-261">Razor 保留关键字</span><span class="sxs-lookup"><span data-stu-id="206d2-261">Razor reserved keywords</span></span>

### <a name="razor-keywords"></a><span data-ttu-id="206d2-262">Razor 关键字</span><span class="sxs-lookup"><span data-stu-id="206d2-262">Razor keywords</span></span>

* <span data-ttu-id="206d2-263">page（需要 ASP.NET Core 2.0 及更高版本）</span><span class="sxs-lookup"><span data-stu-id="206d2-263">page (Requires ASP.NET Core 2.0 and later)</span></span>
* <span data-ttu-id="206d2-264">namespace</span><span class="sxs-lookup"><span data-stu-id="206d2-264">namespace</span></span>
* <span data-ttu-id="206d2-265">functions</span><span class="sxs-lookup"><span data-stu-id="206d2-265">functions</span></span>
* <span data-ttu-id="206d2-266">inherits</span><span class="sxs-lookup"><span data-stu-id="206d2-266">inherits</span></span>
* <span data-ttu-id="206d2-267">model</span><span class="sxs-lookup"><span data-stu-id="206d2-267">model</span></span>
* <span data-ttu-id="206d2-268">section</span><span class="sxs-lookup"><span data-stu-id="206d2-268">section</span></span>
* <span data-ttu-id="206d2-269">helper（ASP.NET Core 当前不支持）</span><span class="sxs-lookup"><span data-stu-id="206d2-269">helper (Not currently supported by ASP.NET Core)</span></span>

<span data-ttu-id="206d2-270">Razor 关键字使用 `@(Razor Keyword)` 进行转义（例如，`@(functions)`）。</span><span class="sxs-lookup"><span data-stu-id="206d2-270">Razor keywords are escaped with `@(Razor Keyword)` (for example, `@(functions)`).</span></span>

### <a name="c-razor-keywords"></a><span data-ttu-id="206d2-271">C# Razor 关键字</span><span class="sxs-lookup"><span data-stu-id="206d2-271">C# Razor keywords</span></span>

* <span data-ttu-id="206d2-272">case</span><span class="sxs-lookup"><span data-stu-id="206d2-272">case</span></span>
* <span data-ttu-id="206d2-273">do</span><span class="sxs-lookup"><span data-stu-id="206d2-273">do</span></span>
* <span data-ttu-id="206d2-274">default</span><span class="sxs-lookup"><span data-stu-id="206d2-274">default</span></span>
* <span data-ttu-id="206d2-275">for</span><span class="sxs-lookup"><span data-stu-id="206d2-275">for</span></span>
* <span data-ttu-id="206d2-276">foreach</span><span class="sxs-lookup"><span data-stu-id="206d2-276">foreach</span></span>
* <span data-ttu-id="206d2-277">if</span><span class="sxs-lookup"><span data-stu-id="206d2-277">if</span></span>
* <span data-ttu-id="206d2-278">else</span><span class="sxs-lookup"><span data-stu-id="206d2-278">else</span></span>
* <span data-ttu-id="206d2-279">lock</span><span class="sxs-lookup"><span data-stu-id="206d2-279">lock</span></span>
* <span data-ttu-id="206d2-280">switch</span><span class="sxs-lookup"><span data-stu-id="206d2-280">switch</span></span>
* <span data-ttu-id="206d2-281">try</span><span class="sxs-lookup"><span data-stu-id="206d2-281">try</span></span>
* <span data-ttu-id="206d2-282">catch</span><span class="sxs-lookup"><span data-stu-id="206d2-282">catch</span></span>
* <span data-ttu-id="206d2-283">finally</span><span class="sxs-lookup"><span data-stu-id="206d2-283">finally</span></span>
* <span data-ttu-id="206d2-284">using</span><span class="sxs-lookup"><span data-stu-id="206d2-284">using</span></span>
* <span data-ttu-id="206d2-285">while</span><span class="sxs-lookup"><span data-stu-id="206d2-285">while</span></span>

<span data-ttu-id="206d2-286">C# Razor 关键字必须使用 `@(@C# Razor Keyword)` 进行双转义（例如，`@(@case)`）。</span><span class="sxs-lookup"><span data-stu-id="206d2-286">C# Razor keywords must be double-escaped with `@(@C# Razor Keyword)` (for example, `@(@case)`).</span></span> <span data-ttu-id="206d2-287">第一个 `@` 对 Razor 分析器转义。</span><span class="sxs-lookup"><span data-stu-id="206d2-287">The first `@` escapes the Razor parser.</span></span> <span data-ttu-id="206d2-288">第二个 `@` 对 C# 分析器转义。</span><span class="sxs-lookup"><span data-stu-id="206d2-288">The second `@` escapes the C# parser.</span></span>

### <a name="reserved-keywords-not-used-by-razor"></a><span data-ttu-id="206d2-289">Razor 不使用的保留关键字</span><span class="sxs-lookup"><span data-stu-id="206d2-289">Reserved keywords not used by Razor</span></span>

* <span data-ttu-id="206d2-290">class</span><span class="sxs-lookup"><span data-stu-id="206d2-290">class</span></span>

## <a name="inspect-the-razor-c-class-generated-for-a-view"></a><span data-ttu-id="206d2-291">检查为视图生成的 Razor C# 类</span><span class="sxs-lookup"><span data-stu-id="206d2-291">Inspect the Razor C# class generated for a view</span></span>

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="206d2-292">在 .NET Core SDK 2.1 或更高版本中，[Razor SDK](xref:razor-pages/sdk) 负责编译 Razor 文件。</span><span class="sxs-lookup"><span data-stu-id="206d2-292">With .NET Core SDK 2.1 or later, the [Razor SDK](xref:razor-pages/sdk) handles compilation of Razor files.</span></span> <span data-ttu-id="206d2-293">生成项目时，Razor SDK 在项目根目录中生成 obj/<build_configuration>/<target_framework_moniker>/Razor 目录。</span><span class="sxs-lookup"><span data-stu-id="206d2-293">When building a project, the Razor SDK generates an *obj/<build_configuration>/<target_framework_moniker>/Razor* directory in the project root.</span></span> <span data-ttu-id="206d2-294">Razor 目录中的目录结构反映项目的目录结构。</span><span class="sxs-lookup"><span data-stu-id="206d2-294">The directory structure within the *Razor* directory mirrors the project's directory structure.</span></span>

<span data-ttu-id="206d2-295">在面向 .NET Core 2.1 的 ASP.NET Core 2.1 Razor Pages 项目中，请考虑以下目录结构：</span><span class="sxs-lookup"><span data-stu-id="206d2-295">Consider the following directory structure in an ASP.NET Core 2.1 Razor Pages project targeting .NET Core 2.1:</span></span>

* <span data-ttu-id="206d2-296">Areas/</span><span class="sxs-lookup"><span data-stu-id="206d2-296">**Areas/**</span></span>
  * <span data-ttu-id="206d2-297">Admin/</span><span class="sxs-lookup"><span data-stu-id="206d2-297">**Admin/**</span></span>
    * <span data-ttu-id="206d2-298">Pages/</span><span class="sxs-lookup"><span data-stu-id="206d2-298">**Pages/**</span></span>
      * <span data-ttu-id="206d2-299">Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="206d2-299">*Index.cshtml*</span></span>
      * <span data-ttu-id="206d2-300">Index.cshtml.cs</span><span class="sxs-lookup"><span data-stu-id="206d2-300">*Index.cshtml.cs*</span></span>
* <span data-ttu-id="206d2-301">Pages/</span><span class="sxs-lookup"><span data-stu-id="206d2-301">**Pages/**</span></span>
  * <span data-ttu-id="206d2-302">Shared/</span><span class="sxs-lookup"><span data-stu-id="206d2-302">**Shared/**</span></span>
    * <span data-ttu-id="206d2-303">_Layout.cshtml</span><span class="sxs-lookup"><span data-stu-id="206d2-303">*_Layout.cshtml*</span></span>
  * <span data-ttu-id="206d2-304">_ViewImports.cshtml</span><span class="sxs-lookup"><span data-stu-id="206d2-304">*_ViewImports.cshtml*</span></span>
  * <span data-ttu-id="206d2-305">*_ViewStart.cshtml*</span><span class="sxs-lookup"><span data-stu-id="206d2-305">*_ViewStart.cshtml*</span></span>
  * <span data-ttu-id="206d2-306">Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="206d2-306">*Index.cshtml*</span></span>
  * <span data-ttu-id="206d2-307">Index.cshtml.cs</span><span class="sxs-lookup"><span data-stu-id="206d2-307">*Index.cshtml.cs*</span></span>

<span data-ttu-id="206d2-308">在 Debug 配置下生成项目将生成以下 obj 目录：</span><span class="sxs-lookup"><span data-stu-id="206d2-308">Building the project in *Debug* configuration yields the following *obj* directory:</span></span>

* <span data-ttu-id="206d2-309">obj/</span><span class="sxs-lookup"><span data-stu-id="206d2-309">**obj/**</span></span>
  * <span data-ttu-id="206d2-310">Debug/</span><span class="sxs-lookup"><span data-stu-id="206d2-310">**Debug/**</span></span>
    * <span data-ttu-id="206d2-311">netcoreapp2.1/</span><span class="sxs-lookup"><span data-stu-id="206d2-311">**netcoreapp2.1/**</span></span>
      * <span data-ttu-id="206d2-312">Razor/</span><span class="sxs-lookup"><span data-stu-id="206d2-312">**Razor/**</span></span>
        * <span data-ttu-id="206d2-313">Areas/</span><span class="sxs-lookup"><span data-stu-id="206d2-313">**Areas/**</span></span>
          * <span data-ttu-id="206d2-314">Admin/</span><span class="sxs-lookup"><span data-stu-id="206d2-314">**Admin/**</span></span>
            * <span data-ttu-id="206d2-315">Pages/</span><span class="sxs-lookup"><span data-stu-id="206d2-315">**Pages/**</span></span>
              * <span data-ttu-id="206d2-316">Index.g.cshtml.cs</span><span class="sxs-lookup"><span data-stu-id="206d2-316">*Index.g.cshtml.cs*</span></span>
        * <span data-ttu-id="206d2-317">Pages/</span><span class="sxs-lookup"><span data-stu-id="206d2-317">**Pages/**</span></span>
          * <span data-ttu-id="206d2-318">Shared/</span><span class="sxs-lookup"><span data-stu-id="206d2-318">**Shared/**</span></span>
            * <span data-ttu-id="206d2-319">_Layout.g.cshtml.cs</span><span class="sxs-lookup"><span data-stu-id="206d2-319">*_Layout.g.cshtml.cs*</span></span>
          * <span data-ttu-id="206d2-320">_ViewImports.g.cshtml.cs</span><span class="sxs-lookup"><span data-stu-id="206d2-320">*_ViewImports.g.cshtml.cs*</span></span>
          * <span data-ttu-id="206d2-321">_ViewStart.g.cshtml.cs</span><span class="sxs-lookup"><span data-stu-id="206d2-321">*_ViewStart.g.cshtml.cs*</span></span>
          * <span data-ttu-id="206d2-322">Index.g.cshtml.cs</span><span class="sxs-lookup"><span data-stu-id="206d2-322">*Index.g.cshtml.cs*</span></span>

<span data-ttu-id="206d2-323">若要查看 Pages/Index.cshtml 的生成类，请打开 obj/Debug/netcoreapp2.1/Razor/Pages/Index.g.cshtml.cs。</span><span class="sxs-lookup"><span data-stu-id="206d2-323">To view the generated class for *Pages/Index.cshtml*, open *obj/Debug/netcoreapp2.1/Razor/Pages/Index.g.cshtml.cs*.</span></span>

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

<span data-ttu-id="206d2-324">将下面的类添加到 ASP.NET Core MVC 项目：</span><span class="sxs-lookup"><span data-stu-id="206d2-324">Add the following class to the ASP.NET Core MVC project:</span></span>

[!code-csharp[](razor/sample/Utilities/CustomTemplateEngine.cs)]

<span data-ttu-id="206d2-325">在 `Startup.ConfigureServices` 中，使用 `CustomTemplateEngine` 类替代 MVC 添加的 `RazorTemplateEngine`：</span><span class="sxs-lookup"><span data-stu-id="206d2-325">In `Startup.ConfigureServices`, override the `RazorTemplateEngine` added by MVC with the `CustomTemplateEngine` class:</span></span>

[!code-csharp[](razor/sample/Startup.cs?highlight=4&range=10-14)]

<span data-ttu-id="206d2-326">在 `CustomTemplateEngine` 的 `return csharpDocument;` 语句上设置断点。</span><span class="sxs-lookup"><span data-stu-id="206d2-326">Set a breakpoint on the `return csharpDocument;` statement of `CustomTemplateEngine`.</span></span> <span data-ttu-id="206d2-327">当程序执行在断点处停止时，查看 `generatedCode` 的值。</span><span class="sxs-lookup"><span data-stu-id="206d2-327">When program execution stops at the breakpoint, view the value of `generatedCode`.</span></span>

![generatedCode 的文本可视化工具视图](razor/_static/tvr.png)

::: moniker-end

## <a name="view-lookups-and-case-sensitivity"></a><span data-ttu-id="206d2-329">视图查找和区分大小写</span><span class="sxs-lookup"><span data-stu-id="206d2-329">View lookups and case sensitivity</span></span>

<span data-ttu-id="206d2-330">Razor 视图引擎为视图执行区分大小写的查找。</span><span class="sxs-lookup"><span data-stu-id="206d2-330">The Razor view engine performs case-sensitive lookups for views.</span></span> <span data-ttu-id="206d2-331">但是，实际查找取决于基础文件系统：</span><span class="sxs-lookup"><span data-stu-id="206d2-331">However, the actual lookup is determined by the underlying file system:</span></span>

* <span data-ttu-id="206d2-332">基于文件的源：</span><span class="sxs-lookup"><span data-stu-id="206d2-332">File based source:</span></span>
  * <span data-ttu-id="206d2-333">在使用不区分大小写的文件系统的操作系统（例如，Windows）上，物理文件提供程序查找不区分大小写。</span><span class="sxs-lookup"><span data-stu-id="206d2-333">On operating systems with case insensitive file systems (for example, Windows), physical file provider lookups are case insensitive.</span></span> <span data-ttu-id="206d2-334">例如，`return View("Test")` 可匹配 */Views/Home/Test.cshtml*、*/Views/home/test.cshtml* 以及任何其他大小写变体。</span><span class="sxs-lookup"><span data-stu-id="206d2-334">For example, `return View("Test")` results in matches for */Views/Home/Test.cshtml*, */Views/home/test.cshtml*, and any other casing variant.</span></span>
  * <span data-ttu-id="206d2-335">在区分大小写的文件系统（例如，Linux、OSX 以及使用 `EmbeddedFileProvider` 构建的文件系统）上，查找区分大小写。</span><span class="sxs-lookup"><span data-stu-id="206d2-335">On case-sensitive file systems (for example, Linux, OSX, and with `EmbeddedFileProvider`), lookups are case-sensitive.</span></span> <span data-ttu-id="206d2-336">例如，`return View("Test")` 专门匹配 */Views/Home/Test.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="206d2-336">For example, `return View("Test")` specifically matches */Views/Home/Test.cshtml*.</span></span>
* <span data-ttu-id="206d2-337">预编译视图：在 ASP.NET Core 2.0 及更高版本中，预编译视图查找在所有操作系统上均不区分大小写。</span><span class="sxs-lookup"><span data-stu-id="206d2-337">Precompiled views: With ASP.NET Core 2.0 and later, looking up precompiled views is case insensitive on all operating systems.</span></span> <span data-ttu-id="206d2-338">该行为与 Windows 上物理文件提供程序的行为相同。</span><span class="sxs-lookup"><span data-stu-id="206d2-338">The behavior is identical to physical file provider's behavior on Windows.</span></span> <span data-ttu-id="206d2-339">如果两个预编译视图仅大小写不同，则查找的结果具有不确定性。</span><span class="sxs-lookup"><span data-stu-id="206d2-339">If two precompiled views differ only in case, the result of lookup is non-deterministic.</span></span>

<span data-ttu-id="206d2-340">建议开发人员将文件和目录名称的大小写与以下项的大小写匹配：</span><span class="sxs-lookup"><span data-stu-id="206d2-340">Developers are encouraged to match the casing of file and directory names to the casing of:</span></span>

* <span data-ttu-id="206d2-341">区域、控制器和操作名称。</span><span class="sxs-lookup"><span data-stu-id="206d2-341">Area, controller, and action names.</span></span>
* <span data-ttu-id="206d2-342">Razor 页面。</span><span class="sxs-lookup"><span data-stu-id="206d2-342">Razor Pages.</span></span>

<span data-ttu-id="206d2-343">匹配大小写可确保无论使用哪种基础文件系统，部署都能找到其视图。</span><span class="sxs-lookup"><span data-stu-id="206d2-343">Matching case ensures the deployments find their views regardless of the underlying file system.</span></span>

---
uid: web-pages/overview/getting-started/introducing-razor-syntax-c
title: 使用 Razor 语法 (C#) 的 ASP.NET Web 编程简介 |Microsoft Docs
author: Rick-Anderson
description: 本章提供了您的编程概述与 ASP.NET Web Pages 使用 Razor 语法。 ASP.NET 是 Microsoft 的技术，用于运行动态 web pa...
ms.author: riande
ms.date: 02/07/2014
ms.assetid: aa67d304-583b-4bf8-a231-195656cfb587
msc.legacyurl: /web-pages/overview/getting-started/introducing-razor-syntax-c
msc.type: authoredcontent
ms.openlocfilehash: b5eb98dfdf3fc013920f45080d4a20e1fa507725
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57032664"
---
<a name="introduction-to-aspnet-web-programming-using-the-razor-syntax-c"></a><span data-ttu-id="faae6-104">使用 Razor 语法 (C#) 的 ASP.NET Web 编程简介</span><span class="sxs-lookup"><span data-stu-id="faae6-104">Introduction to ASP.NET Web Programming Using the Razor Syntax (C#)</span></span>
====================
<span data-ttu-id="faae6-105">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="faae6-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="faae6-106">本文提供了您的编程概述与 ASP.NET Web Pages 使用 Razor 语法。</span><span class="sxs-lookup"><span data-stu-id="faae6-106">This article gives you an overview of programming with ASP.NET Web Pages using the Razor syntax.</span></span> <span data-ttu-id="faae6-107">ASP.NET 是 Microsoft 的技术，用于在 web 服务器上运行动态网页。</span><span class="sxs-lookup"><span data-stu-id="faae6-107">ASP.NET is Microsoft's technology for running dynamic web pages on web servers.</span></span> <span data-ttu-id="faae6-108">此文章重点介绍使用 C# 编程语言。</span><span class="sxs-lookup"><span data-stu-id="faae6-108">This articles focuses on using the C# programming language.</span></span>
> 
> <span data-ttu-id="faae6-109">**你将了解**:</span><span class="sxs-lookup"><span data-stu-id="faae6-109">**What you'll learn**:</span></span>
> 
> - <span data-ttu-id="faae6-110">前 8 的编程的入门知识编程使用 Razor 语法的 ASP.NET Web Pages 的提示。</span><span class="sxs-lookup"><span data-stu-id="faae6-110">The top 8 programming tips for getting started with programming ASP.NET Web Pages using Razor syntax.</span></span>
> - <span data-ttu-id="faae6-111">你将需要的基本编程概念。</span><span class="sxs-lookup"><span data-stu-id="faae6-111">Basic programming concepts you'll need.</span></span>
> - <span data-ttu-id="faae6-112">ASP.NET 服务器代码和 Razor 语法是所有有关。</span><span class="sxs-lookup"><span data-stu-id="faae6-112">What ASP.NET server code and the Razor syntax is all about.</span></span>
>   
> 
> ## <a name="software-versions"></a><span data-ttu-id="faae6-113">软件版本</span><span class="sxs-lookup"><span data-stu-id="faae6-113">Software versions</span></span>
> 
> 
> - <span data-ttu-id="faae6-114">ASP.NET 网页 (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="faae6-114">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="faae6-115">本教程还适用于 ASP.NET Web Pages 2。</span><span class="sxs-lookup"><span data-stu-id="faae6-115">This tutorial also works with ASP.NET Web Pages 2.</span></span>


## <a name="the-top-8-programming-tips"></a><span data-ttu-id="faae6-116">最重要的 8 编程提示</span><span class="sxs-lookup"><span data-stu-id="faae6-116">The Top 8 Programming Tips</span></span>

<span data-ttu-id="faae6-117">本部分列出了绝对需要知道当你开始使用 Razor 语法的 ASP.NET 服务器代码编写的一些提示。</span><span class="sxs-lookup"><span data-stu-id="faae6-117">This section lists a few tips that you absolutely need to know as you start writing ASP.NET server code using the Razor syntax.</span></span>

> [!NOTE]
> <span data-ttu-id="faae6-118">Razor 语法基于 C# 编程语言，这也最常使用使用 ASP.NET Web Pages 的语言。</span><span class="sxs-lookup"><span data-stu-id="faae6-118">The Razor syntax is based on the C# programming language, and that's the language that's used most often with ASP.NET Web Pages.</span></span> <span data-ttu-id="faae6-119">但是，Razor 语法还支持 Visual Basic 语言以及你看到你还可以执行在 Visual Basic 中的所有内容。</span><span class="sxs-lookup"><span data-stu-id="faae6-119">However, the Razor syntax also supports the Visual Basic language, and everything you see you can also do in Visual Basic.</span></span> <span data-ttu-id="faae6-120">有关详细信息，请参阅附录[Visual Basic 语言和语法](https://go.microsoft.com/fwlink/?LinkId=202908)。</span><span class="sxs-lookup"><span data-stu-id="faae6-120">For details, see the appendix [Visual Basic Language and Syntax](https://go.microsoft.com/fwlink/?LinkId=202908).</span></span>


<span data-ttu-id="faae6-121">在本文的后面，可以找到有关这些编程技术的大多数的更多详细信息。</span><span class="sxs-lookup"><span data-stu-id="faae6-121">You can find more details about most of these programming techniques later in the article.</span></span>

### <a name="1-you-add-code-to-a-page-using-the--character"></a><span data-ttu-id="faae6-122">1.将代码添加到页使用 @ 字符</span><span class="sxs-lookup"><span data-stu-id="faae6-122">1. You add code to a page using the @ character</span></span>

<span data-ttu-id="faae6-123">`@`字符开始内联表达式、 单个语句块和多语句块：</span><span class="sxs-lookup"><span data-stu-id="faae6-123">The `@` character starts inline expressions, single statement blocks, and multi-statement blocks:</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample1.html)]

<span data-ttu-id="faae6-124">这是这些语句在浏览器中运行页面时的如下：</span><span class="sxs-lookup"><span data-stu-id="faae6-124">This is what these statements look like when the page runs in a browser:</span></span>

![Razor-Img1](introducing-razor-syntax-c/_static/image1.jpg)

> [!TIP] 
> 
> <span data-ttu-id="faae6-126">**HTML 编码**</span><span class="sxs-lookup"><span data-stu-id="faae6-126">**HTML Encoding**</span></span>
> 
> <span data-ttu-id="faae6-127">在页面中使用显示内容时`@`字符 ASP.NET HTML 编码输出，如前面的示例中所示。</span><span class="sxs-lookup"><span data-stu-id="faae6-127">When you display content in a page using the `@` character, as in the preceding examples, ASP.NET HTML-encodes the output.</span></span> <span data-ttu-id="faae6-128">它取代了 HTML 的保留的字符 (如`<`并`>`和`&`) 启用字符作为字符而不是解释为 HTML 标记或实体的网页中显示的代码。</span><span class="sxs-lookup"><span data-stu-id="faae6-128">This replaces reserved HTML characters (such as `<` and `>` and `&`) with codes that enable the characters to be displayed as characters in a web page instead of being interpreted as HTML tags or entities.</span></span> <span data-ttu-id="faae6-129">无需 HTML 编码，即可在服务器代码中的输出可能不会显示正确，并可能会暴露于安全风险的页面。</span><span class="sxs-lookup"><span data-stu-id="faae6-129">Without HTML encoding, the output from your server code might not display correctly, and could expose a page to security risks.</span></span>
> 
> <span data-ttu-id="faae6-130">如果你的目标是输出以标记形式呈现标记的 HTML 标记 (例如`<p></p>`段落或`<em></em>`来强调文本)，请参阅部分[组合文本、 标记和代码块中的代码](#BM_CombiningTextMarkupAndCode)这篇文章中更高版本。</span><span class="sxs-lookup"><span data-stu-id="faae6-130">If your goal is to output HTML markup that renders tags as markup (for example `<p></p>` for a paragraph or `<em></em>` to emphasize text), see the section [Combining Text, Markup, and Code in Code Blocks](#BM_CombiningTextMarkupAndCode) later in this article.</span></span>
> 
> <span data-ttu-id="faae6-131">你可以阅读更多有关中的 HTML 编码[使用窗体](https://go.microsoft.com/fwlink/?LinkId=202892)。</span><span class="sxs-lookup"><span data-stu-id="faae6-131">You can read more about HTML encoding in [Working with Forms](https://go.microsoft.com/fwlink/?LinkId=202892).</span></span>


### <a name="2-you-enclose-code-blocks-in-braces"></a><span data-ttu-id="faae6-132">2.将代码块括在大括号中</span><span class="sxs-lookup"><span data-stu-id="faae6-132">2. You enclose code blocks in braces</span></span>

<span data-ttu-id="faae6-133">一个*代码块*包括一个或多个代码语句并括在大括号。</span><span class="sxs-lookup"><span data-stu-id="faae6-133">A *code block* includes one or more code statements and is enclosed in braces.</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample2.html)]

<span data-ttu-id="faae6-134">在浏览器中显示的结果：</span><span class="sxs-lookup"><span data-stu-id="faae6-134">The result displayed in a browser:</span></span>

![Razor-Img2](introducing-razor-syntax-c/_static/image2.jpg)

### <a name="3-inside-a-block-you-end-each-code-statement-with-a-semicolon"></a><span data-ttu-id="faae6-136">3.在块中，您最终以分号结束每条代码语句</span><span class="sxs-lookup"><span data-stu-id="faae6-136">3. Inside a block, you end each code statement with a semicolon</span></span>

<span data-ttu-id="faae6-137">在代码块中，每个完整的代码语句必须以分号结尾。</span><span class="sxs-lookup"><span data-stu-id="faae6-137">Inside a code block, each complete code statement must end with a semicolon.</span></span> <span data-ttu-id="faae6-138">内联表达式不以分号结束。</span><span class="sxs-lookup"><span data-stu-id="faae6-138">Inline expressions don't end with a semicolon.</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample3.html)]

### <a name="4-you-use-variables-to-store-values"></a><span data-ttu-id="faae6-139">4.使用变量来存储值</span><span class="sxs-lookup"><span data-stu-id="faae6-139">4. You use variables to store values</span></span>

<span data-ttu-id="faae6-140">可以存储中的值*变量*，包括字符串、 数字和日期等。创建一个新的变量使用`var`关键字。</span><span class="sxs-lookup"><span data-stu-id="faae6-140">You can store values in a *variable*, including strings, numbers, and dates, etc. You create a new variable using the `var` keyword.</span></span> <span data-ttu-id="faae6-141">可以直接在页中使用插入变量值`@`。</span><span class="sxs-lookup"><span data-stu-id="faae6-141">You can insert variable values directly in a page using `@`.</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample4.html)]

<span data-ttu-id="faae6-142">在浏览器中显示的结果：</span><span class="sxs-lookup"><span data-stu-id="faae6-142">The result displayed in a browser:</span></span>

![Razor-Img3](introducing-razor-syntax-c/_static/image3.jpg)

<a id="ID_StringLiterals"></a>
### <a name="5-you-enclose-literal-string-values-in-double-quotation-marks"></a><span data-ttu-id="faae6-144">5.将文本字符串值括在双引号内</span><span class="sxs-lookup"><span data-stu-id="faae6-144">5. You enclose literal string values in double quotation marks</span></span>

<span data-ttu-id="faae6-145">一个*字符串*是被视为文本字符序列。</span><span class="sxs-lookup"><span data-stu-id="faae6-145">A *string* is a sequence of characters that are treated as text.</span></span> <span data-ttu-id="faae6-146">若要指定一个字符串，则将其括在双引号内：</span><span class="sxs-lookup"><span data-stu-id="faae6-146">To specify a string, you enclose it in double quotation marks:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample5.cshtml)]

<span data-ttu-id="faae6-147">如果你想要显示的字符串包含反斜杠字符 ( `\` ) 或双引号 ( `"` )，使用*原义字符串文本*前面带`@`运算符。</span><span class="sxs-lookup"><span data-stu-id="faae6-147">If the string that you want to display contains a backslash character ( `\` ) or double quotation marks ( `"` ), use a *verbatim string literal* that's prefixed with the `@` operator.</span></span> <span data-ttu-id="faae6-148">(在 C# 中，\ 字符具有特殊含义，除非使用原义字符串文本。)</span><span class="sxs-lookup"><span data-stu-id="faae6-148">(In C#, the \ character has special meaning unless you use a verbatim string literal.)</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample6.html)]

<span data-ttu-id="faae6-149">若要嵌入双引号引起来，使用逐字字符串文本，并重复引号引起来：</span><span class="sxs-lookup"><span data-stu-id="faae6-149">To embed double quotation marks, use a verbatim string literal and repeat the quotation marks:</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample7.html)]

<span data-ttu-id="faae6-150">下面是在一个页面中使用这两个示例的结果：</span><span class="sxs-lookup"><span data-stu-id="faae6-150">Here's the result of using both of these examples in a page:</span></span>

![Razor-Img4](introducing-razor-syntax-c/_static/image4.jpg)

> [!NOTE]
> <span data-ttu-id="faae6-152">请注意，`@`标记在 C# 中的逐字字符串文本和标记 ASP.NET 页面中的代码使用字符。</span><span class="sxs-lookup"><span data-stu-id="faae6-152">Notice that the `@` character is used both to mark verbatim string literals in C# and to mark code in ASP.NET pages.</span></span>


### <a name="6-code-is-case-sensitive"></a><span data-ttu-id="faae6-153">6.代码是区分大小写</span><span class="sxs-lookup"><span data-stu-id="faae6-153">6. Code is case sensitive</span></span>

<span data-ttu-id="faae6-154">在 C# 中，关键字 (如`var`， `true`，和`if`) 和变量名称区分大小写。</span><span class="sxs-lookup"><span data-stu-id="faae6-154">In C#, keywords (like `var`, `true`, and `if`) and variable names are case sensitive.</span></span> <span data-ttu-id="faae6-155">以下代码行创建两个不同的变量，`lastName`和 `LastName.`</span><span class="sxs-lookup"><span data-stu-id="faae6-155">The following lines of code create two different variables, `lastName` and `LastName.`</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample8.cshtml)]

<span data-ttu-id="faae6-156">如果声明一个变量，作为`var lastName = "Smith";`，如果试图引用该变量在页中作为`@LastName`，会发生错误，因为`LastName`将无法识别。</span><span class="sxs-lookup"><span data-stu-id="faae6-156">If you declare a variable as `var lastName = "Smith";` and if you try to reference that variable in your page as `@LastName`, an error results because `LastName` won't be recognized.</span></span>

> [!NOTE]
> <span data-ttu-id="faae6-157">在 Visual Basic 关键字和变量是*不*区分大小写。</span><span class="sxs-lookup"><span data-stu-id="faae6-157">In Visual Basic, keywords and variables are *not* case sensitive.</span></span>


### <a name="7-much-of-your-coding-involves-objects"></a><span data-ttu-id="faae6-158">7.大部分代码涉及到对象</span><span class="sxs-lookup"><span data-stu-id="faae6-158">7. Much of your coding involves objects</span></span>

<span data-ttu-id="faae6-159">*对象*表示的接口可以带有程序&#8212;页、 文本框、 文件、 图像、 web 请求、 电子邮件、 客户记录 （数据库行），等等。对象具有描述它们的特征的属性，并且你可以读取或更改&#8212;文本框对象具有`Text`（及其他） 的属性，请求对象具有`Url`属性，电子邮件具有`From`属性，和客户对象都具有`FirstName`属性。</span><span class="sxs-lookup"><span data-stu-id="faae6-159">An *object* represents a thing that you can program with &#8212; a page, a text box, a file, an image, a web request, an email message, a customer record (database row), etc. Objects have properties that describe their characteristics and that you can read or change &#8212; a text box object has a `Text` property (among others), a request object has a `Url` property, an email message has a `From` property, and a customer object has a `FirstName` property.</span></span> <span data-ttu-id="faae6-160">对象还具有方法&quot;谓词&quot;他们可以执行。</span><span class="sxs-lookup"><span data-stu-id="faae6-160">Objects also have methods that are the &quot;verbs&quot; they can perform.</span></span> <span data-ttu-id="faae6-161">示例包括文件对象的`Save`方法中，映像对象的`Rotate`方法，并电子邮件对象的`Send`方法。</span><span class="sxs-lookup"><span data-stu-id="faae6-161">Examples include a file object's `Save` method, an image object's `Rotate` method, and an email object's `Send` method.</span></span>

<span data-ttu-id="faae6-162">你经常要用`Request`对象，后者可提供信息，如值的文本框 （窗体字段） 在页面上，进行浏览器的哪种类型的请求的 URL 的页面、 用户标识，等等。下面的示例演示如何访问的属性`Request`对象以及如何调用`MapPath`方法的`Request`对象，这将使您在服务器上的页面的绝对路径：</span><span class="sxs-lookup"><span data-stu-id="faae6-162">You'll often work with the `Request` object, which gives you information like the values of text boxes (form fields) on the page, what type of browser made the request, the URL of the page, the user identity, etc. The following example shows how to access properties of the `Request` object and how to call the `MapPath` method of the `Request` object, which gives you the absolute path of the page on the server:</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample9.html)]

<span data-ttu-id="faae6-163">在浏览器中显示的结果：</span><span class="sxs-lookup"><span data-stu-id="faae6-163">The result displayed in a browser:</span></span>

![Razor-Img5](introducing-razor-syntax-c/_static/image5.jpg)

### <a name="8-you-can-write-code-that-makes-decisions"></a><span data-ttu-id="faae6-165">8。可以编写代码来做出决策</span><span class="sxs-lookup"><span data-stu-id="faae6-165">8. You can write code that makes decisions</span></span>

<span data-ttu-id="faae6-166">动态网页的一项主要功能是，您可以确定要执行的操作根据条件。</span><span class="sxs-lookup"><span data-stu-id="faae6-166">A key feature of dynamic web pages is that you can determine what to do based on conditions.</span></span> <span data-ttu-id="faae6-167">若要执行此操作的最常见方法是使用`if`语句 (和可选`else`语句)。</span><span class="sxs-lookup"><span data-stu-id="faae6-167">The most common way to do this is with the `if` statement (and optional `else` statement).</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample10.cshtml)]

<span data-ttu-id="faae6-168">该语句`if(IsPost)`是一种编写的速记方法`if(IsPost == true)`。</span><span class="sxs-lookup"><span data-stu-id="faae6-168">The statement `if(IsPost)` is a shorthand way of writing `if(IsPost == true)`.</span></span> <span data-ttu-id="faae6-169">连同`if`语句，有多种方法可以测试条件，重复的代码块，并且依此类推，这是本文后面所述。</span><span class="sxs-lookup"><span data-stu-id="faae6-169">Along with `if` statements, there are a variety of ways to test conditions, repeat blocks of code, and so on, which are described later in this article.</span></span>

<span data-ttu-id="faae6-170">在浏览器中显示的结果 (单击后**提交**):</span><span class="sxs-lookup"><span data-stu-id="faae6-170">The result displayed in a browser (after clicking **Submit**):</span></span>

![Razor-Img6](introducing-razor-syntax-c/_static/image6.jpg)

> [!TIP] 
> 
> <a id="SB_HttpGetPost"></a>
> ### <a name="http-get-and-post-methods-and-the-ispost-property"></a><span data-ttu-id="faae6-172">HTTP GET 和 POST 方法和 IsPost 属性</span><span class="sxs-lookup"><span data-stu-id="faae6-172">HTTP GET and POST Methods and the IsPost Property</span></span>
> 
> <span data-ttu-id="faae6-173">用于网页 (HTTP) 的协议支持的方法 （谓词） 用来向服务器发出请求的数量很少。</span><span class="sxs-lookup"><span data-stu-id="faae6-173">The protocol used for web pages (HTTP) supports a very limited number of methods (verbs) that are used to make requests to the server.</span></span> <span data-ttu-id="faae6-174">两个最常见的是 GET、 用于读取某页和用于将网页提交的文章。</span><span class="sxs-lookup"><span data-stu-id="faae6-174">The two most common ones are GET, which is used to read a page, and POST, which is used to submit a page.</span></span> <span data-ttu-id="faae6-175">一般情况下，用户请求页面时，第一次请求页面时使用 GET。</span><span class="sxs-lookup"><span data-stu-id="faae6-175">In general, the first time a user requests a page, the page is requested using GET.</span></span> <span data-ttu-id="faae6-176">如果用户在填写窗体，并单击提交按钮，浏览器向服务器发出的 POST 请求。</span><span class="sxs-lookup"><span data-stu-id="faae6-176">If the user fills in a form and then clicks a submit button, the browser makes a POST request to the server.</span></span>
> 
> <span data-ttu-id="faae6-177">在 web 编程中，它通常是有助于了解是否请求页面时正在作为 GET 或 POST，以便您知道如何处理页面。</span><span class="sxs-lookup"><span data-stu-id="faae6-177">In web programming, it's often useful to know whether a page is being requested as a GET or as a POST so that you know how to process the page.</span></span> <span data-ttu-id="faae6-178">ASP.NET Web Pages 中，可以使用`IsPost`属性以确定请求是否为 GET 或 POST。</span><span class="sxs-lookup"><span data-stu-id="faae6-178">In ASP.NET Web Pages, you can use the `IsPost` property to see whether a request is a GET or a POST.</span></span> <span data-ttu-id="faae6-179">如果请求为 POST，`IsPost`属性将返回 true，然后你可以执行诸如读取窗体上的文本框的值。</span><span class="sxs-lookup"><span data-stu-id="faae6-179">If the request is a POST, the `IsPost` property will return true, and you can do things like read the values of text boxes on a form.</span></span> <span data-ttu-id="faae6-180">你将看到许多示例演示如何处理以不同的方式具体取决于值页面`IsPost`。</span><span class="sxs-lookup"><span data-stu-id="faae6-180">Many examples you'll see show you how to process the page differently depending on the value of `IsPost`.</span></span>


## <a name="a-simple-code-example"></a><span data-ttu-id="faae6-181">简单的代码示例</span><span class="sxs-lookup"><span data-stu-id="faae6-181">A Simple Code Example</span></span>

<span data-ttu-id="faae6-182">此过程演示如何创建一个页面，说明了基本的编程技术。</span><span class="sxs-lookup"><span data-stu-id="faae6-182">This procedure shows you how to create a page that illustrates basic programming techniques.</span></span> <span data-ttu-id="faae6-183">在示例中，您可以创建允许用户输入两个数字，然后将它们添加并显示结果的页面。</span><span class="sxs-lookup"><span data-stu-id="faae6-183">In the example, you create a page that lets users enter two numbers, then it adds them and displays the result.</span></span>

1. <span data-ttu-id="faae6-184">在编辑器中，创建一个新文件并将其命名*AddNumbers.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="faae6-184">In your editor, create a new file and name it *AddNumbers.cshtml*.</span></span>
2. <span data-ttu-id="faae6-185">将以下代码和标记复制到页中，替换已在页中的任何内容。</span><span class="sxs-lookup"><span data-stu-id="faae6-185">Copy the following code and markup into the page, replacing anything already in the page.</span></span>  

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample11.cshtml)]

    <span data-ttu-id="faae6-186">下面是您需要注意一些事项：</span><span class="sxs-lookup"><span data-stu-id="faae6-186">Here are some things for you to note:</span></span>

    - <span data-ttu-id="faae6-187">`@`字符在页中，启动第一个代码块，它位于之前`totalMessage`嵌入在页面底部附近的变量。</span><span class="sxs-lookup"><span data-stu-id="faae6-187">The `@` character starts the first block of code in the page, and it precedes the `totalMessage` variable that's embedded near the bottom of the page.</span></span>
    - <span data-ttu-id="faae6-188">在页面顶部块括在大括号中。</span><span class="sxs-lookup"><span data-stu-id="faae6-188">The block at the top of the page is enclosed in braces.</span></span>
    - <span data-ttu-id="faae6-189">在顶部块中，所有行以分号都结束。</span><span class="sxs-lookup"><span data-stu-id="faae6-189">In the block at the top, all lines end with a semicolon.</span></span>
    - <span data-ttu-id="faae6-190">变量`total`， `num1`， `num2`，和`totalMessage`存储多个数字和字符串。</span><span class="sxs-lookup"><span data-stu-id="faae6-190">The variables `total`, `num1`, `num2`, and `totalMessage` store several numbers and a string.</span></span>
    - <span data-ttu-id="faae6-191">分配给的文字字符串值`totalMessage`变量是在双引号。</span><span class="sxs-lookup"><span data-stu-id="faae6-191">The literal string value assigned to the `totalMessage` variable is in double quotation marks.</span></span>
    - <span data-ttu-id="faae6-192">因为代码是区分大小写，当`totalMessage`变量使用页面底部附近，其名称必须完全匹配在顶部的变量。</span><span class="sxs-lookup"><span data-stu-id="faae6-192">Because the code is case-sensitive, when the `totalMessage` variable is used near the bottom of the page, its name must match the variable at the top exactly.</span></span>
    - <span data-ttu-id="faae6-193">表达式`num1.AsInt() + num2.AsInt()`演示如何使用对象和方法。</span><span class="sxs-lookup"><span data-stu-id="faae6-193">The expression `num1.AsInt() + num2.AsInt()` shows how to work with objects and methods.</span></span> <span data-ttu-id="faae6-194">`AsInt`上每个变量的方法将转换输入用户的数字 （整数），以便可以对其执行算术运算的字符串。</span><span class="sxs-lookup"><span data-stu-id="faae6-194">The `AsInt` method on each variable converts the string entered by a user to a number (an integer) so that you can perform arithmetic on it.</span></span>
    - <span data-ttu-id="faae6-195">`<form>`标记包含`method="post"`属性。</span><span class="sxs-lookup"><span data-stu-id="faae6-195">The `<form>` tag includes a `method="post"` attribute.</span></span> <span data-ttu-id="faae6-196">此步骤指定当用户单击**添加**，页面将发送到服务器使用 HTTP POST 方法。</span><span class="sxs-lookup"><span data-stu-id="faae6-196">This specifies that when the user clicks **Add**, the page will be sent to the server using the HTTP POST method.</span></span> <span data-ttu-id="faae6-197">提交页面后，`if(IsPost)`测试的计算结果为 true，条件性代码运行时，显示数字相加的结果。</span><span class="sxs-lookup"><span data-stu-id="faae6-197">When the page is submitted, the `if(IsPost)` test evaluates to true and the conditional code runs, displaying the result of adding the numbers.</span></span>
3. <span data-ttu-id="faae6-198">保存页面，并在浏览器中运行它。</span><span class="sxs-lookup"><span data-stu-id="faae6-198">Save the page and run it in a browser.</span></span> <span data-ttu-id="faae6-199">(请确保的页中选择**文件**工作区之前运行它。)输入两个整数，然后单击**添加**按钮。</span><span class="sxs-lookup"><span data-stu-id="faae6-199">(Make sure the page is selected in the **Files** workspace before you run it.) Enter two whole numbers and then click the **Add** button.</span></span> 

    ![Razor-Img7](introducing-razor-syntax-c/_static/image7.jpg)

## <a name="basic-programming-concepts"></a><span data-ttu-id="faae6-201">基本编程概念</span><span class="sxs-lookup"><span data-stu-id="faae6-201">Basic Programming Concepts</span></span>

<span data-ttu-id="faae6-202">本文为您提供了 ASP.NET web 编程的概述。</span><span class="sxs-lookup"><span data-stu-id="faae6-202">This article provides you with an overview of ASP.NET web programming.</span></span> <span data-ttu-id="faae6-203">它并不详尽检查，只需快速介绍一下将最常使用的编程概念。</span><span class="sxs-lookup"><span data-stu-id="faae6-203">It isn't an exhaustive examination, just a quick tour through the programming concepts you'll use most often.</span></span> <span data-ttu-id="faae6-204">即便如此，它涵盖了你将需要开始使用 ASP.NET Web Pages 几乎所有内容。</span><span class="sxs-lookup"><span data-stu-id="faae6-204">Even so, it covers almost everything you'll need to get started with ASP.NET Web Pages.</span></span>

<span data-ttu-id="faae6-205">但首先，一点的技术背景知识。</span><span class="sxs-lookup"><span data-stu-id="faae6-205">But first, a little technical background.</span></span>

### <a name="the-razor-syntax-server-code-and-aspnet"></a><span data-ttu-id="faae6-206">Razor 语法、 服务器代码和 ASP.NET</span><span class="sxs-lookup"><span data-stu-id="faae6-206">The Razor Syntax, Server Code, and ASP.NET</span></span>

<span data-ttu-id="faae6-207">Razor 语法是一种简单的编程语法，用于在网页中嵌入基于服务器的代码。</span><span class="sxs-lookup"><span data-stu-id="faae6-207">Razor syntax is a simple programming syntax for embedding server-based code in a web page.</span></span> <span data-ttu-id="faae6-208">在使用 Razor 语法的网页，有两种类型的内容： 客户端内容和服务器代码。</span><span class="sxs-lookup"><span data-stu-id="faae6-208">In a web page that uses the Razor syntax, there are two kinds of content: client content and server code.</span></span> <span data-ttu-id="faae6-209">客户端内容是你习惯于在 web pages 中的内容：HTML 标记 （元素），如 CSS，也许某些客户端脚本如 JavaScript 和纯文本的样式信息。</span><span class="sxs-lookup"><span data-stu-id="faae6-209">Client content is the stuff you're used to in web pages: HTML markup (elements), style information such as CSS, maybe some client script such as JavaScript, and plain text.</span></span>

<span data-ttu-id="faae6-210">Razor 语法，可以将服务器代码添加到此客户端内容。</span><span class="sxs-lookup"><span data-stu-id="faae6-210">Razor syntax lets you add server code to this client content.</span></span> <span data-ttu-id="faae6-211">是否存在服务器代码页中，服务器运行该代码首先，它将页发送到浏览器之前。</span><span class="sxs-lookup"><span data-stu-id="faae6-211">If there's server code in the page, the server runs that code first, before it sends the page to the browser.</span></span> <span data-ttu-id="faae6-212">通过在服务器上运行，代码可以执行任务，可以是更复杂，无法使用独立的如访问基于服务器的数据库的客户端内容执行操作。</span><span class="sxs-lookup"><span data-stu-id="faae6-212">By running on the server, the code can perform tasks that can be a lot more complex to do using client content alone, like accessing server-based databases.</span></span> <span data-ttu-id="faae6-213">最重要的是，服务器代码可以动态创建客户端内容&#8212;它可以生成 HTML 标记或其他动态内容并将其发送给浏览器以及页可能会包含任何静态 HTML。</span><span class="sxs-lookup"><span data-stu-id="faae6-213">Most importantly, server code can dynamically create client content &#8212; it can generate HTML markup or other content on the fly and then send it to the browser along with any static HTML that the page might contain.</span></span> <span data-ttu-id="faae6-214">从浏览器的角度来看，客户端在服务器代码生成的内容是与任何其他客户端内容没有什么不同。</span><span class="sxs-lookup"><span data-stu-id="faae6-214">From the browser's perspective, client content that's generated by your server code is no different than any other client content.</span></span> <span data-ttu-id="faae6-215">如您所见，所需的服务器代码是非常简单。</span><span class="sxs-lookup"><span data-stu-id="faae6-215">As you've already seen, the server code that's required is quite simple.</span></span>

<span data-ttu-id="faae6-216">包含 Razor 语法的 ASP.NET 网页具有特殊的文件扩展名 (*.cshtml*或 *.vbhtml*)。</span><span class="sxs-lookup"><span data-stu-id="faae6-216">ASP.NET web pages that include the Razor syntax have a special file extension (*.cshtml* or *.vbhtml*).</span></span> <span data-ttu-id="faae6-217">服务器可以识别这些扩展，运行的代码，使用 Razor 语法标记，然后将页发送到浏览器。</span><span class="sxs-lookup"><span data-stu-id="faae6-217">The server recognizes these extensions, runs the code that's marked with Razor syntax, and then sends the page to the browser.</span></span>

### <a name="where-does-aspnet-fit-in"></a><span data-ttu-id="faae6-218">ASP.NET 的适用？</span><span class="sxs-lookup"><span data-stu-id="faae6-218">Where does ASP.NET fit in?</span></span>

<span data-ttu-id="faae6-219">Razor 语法基于名为 ASP.NET，又基于 Microsoft.NET Framework 的 microsoft 技术。</span><span class="sxs-lookup"><span data-stu-id="faae6-219">Razor syntax is based on a technology from Microsoft called ASP.NET, which in turn is based on the Microsoft .NET Framework.</span></span> <span data-ttu-id="faae6-220">.Net Framework 是一个大的全面编程框架从 Microsoft 开发几乎任何类型的计算机应用程序。</span><span class="sxs-lookup"><span data-stu-id="faae6-220">The.NET Framework is a big, comprehensive programming framework from Microsoft for developing virtually any type of computer application.</span></span> <span data-ttu-id="faae6-221">ASP.NET 是专门设计用于创建 web 应用程序的.NET Framework 的一部分。</span><span class="sxs-lookup"><span data-stu-id="faae6-221">ASP.NET is the part of the .NET Framework that's specifically designed for creating web applications.</span></span> <span data-ttu-id="faae6-222">开发人员使用 ASP.NET 创建的最大和最高流量网站的许多世界中。</span><span class="sxs-lookup"><span data-stu-id="faae6-222">Developers have used ASP.NET to create many of the largest and highest-traffic websites in the world.</span></span> <span data-ttu-id="faae6-223">(只要您看到的文件扩展名 *.aspx*作为一个站点中的 URL 的一部分，您就会知道该站点使用 ASP.NET 进行编写。)</span><span class="sxs-lookup"><span data-stu-id="faae6-223">(Any time you see the file-name extension *.aspx* as part of the URL in a site, you'll know that the site was written using ASP.NET.)</span></span>

<span data-ttu-id="faae6-224">Razor 语法提供 ASP.NET，但使用的简化的语法来更轻松地了解你是否方面的专家，如果您是初学者，可将您提高工作效率的所有强大的功能。</span><span class="sxs-lookup"><span data-stu-id="faae6-224">The Razor syntax gives you all the power of ASP.NET, but using a simplified syntax that's easier to learn if you're a beginner and that makes you more productive if you're an expert.</span></span> <span data-ttu-id="faae6-225">尽管此语法易于使用，它与 ASP.NET 和.NET Framework 的系列关系意味着随着你的网站变得更复杂的还有可供你的更大框架的功能。</span><span class="sxs-lookup"><span data-stu-id="faae6-225">Even though this syntax is simple to use, its family relationship to ASP.NET and the .NET Framework means that as your websites become more sophisticated, you have the power of the larger frameworks available to you.</span></span>

![Razor-Img8](introducing-razor-syntax-c/_static/image8.jpg)

> [!TIP] 
> 
> <span data-ttu-id="faae6-227">**类和实例**</span><span class="sxs-lookup"><span data-stu-id="faae6-227">**Classes and Instances**</span></span>
> 
> <span data-ttu-id="faae6-228">ASP.NET 服务器代码使用对象，又基于类的概念。</span><span class="sxs-lookup"><span data-stu-id="faae6-228">ASP.NET server code uses objects, which are in turn built on the idea of classes.</span></span> <span data-ttu-id="faae6-229">此类是定义或模板的对象。</span><span class="sxs-lookup"><span data-stu-id="faae6-229">The class is the definition or template for an object.</span></span> <span data-ttu-id="faae6-230">例如，应用程序可能包含`Customer`类，该类定义的属性和任何客户对象所需的方法。</span><span class="sxs-lookup"><span data-stu-id="faae6-230">For example, an application might contain a `Customer` class that defines the properties and methods that any customer object needs.</span></span>
> 
> <span data-ttu-id="faae6-231">当应用程序需要使用实际的客户信息时，它创建的实例 (或*实例化*) 客户对象。</span><span class="sxs-lookup"><span data-stu-id="faae6-231">When the application needs to work with actual customer information, it creates an instance of (or *instantiates*) a customer object.</span></span> <span data-ttu-id="faae6-232">每个单独的客户是一个单独的实例`Customer`类。</span><span class="sxs-lookup"><span data-stu-id="faae6-232">Each individual customer is a separate instance of the `Customer` class.</span></span> <span data-ttu-id="faae6-233">每个实例支持的相同的属性和方法，但每个实例的属性值通常不同，因为每个客户对象都是唯一。</span><span class="sxs-lookup"><span data-stu-id="faae6-233">Every instance supports the same properties and methods, but the property values for each instance are typically different, because each customer object is unique.</span></span> <span data-ttu-id="faae6-234">一个客户对象中`LastName`属性可能是"Smith"; 在另一个客户对象，`LastName`属性可能会"Jones"。</span><span class="sxs-lookup"><span data-stu-id="faae6-234">In one customer object, the `LastName` property might be "Smith"; in another customer object, the `LastName` property might be "Jones."</span></span>
> 
> <span data-ttu-id="faae6-235">同样，在站点中任何单个 web 页是`Page`对象，它的实例`Page`类。</span><span class="sxs-lookup"><span data-stu-id="faae6-235">Similarly, any individual web page in your site is a `Page` object that's an instance of the `Page` class.</span></span> <span data-ttu-id="faae6-236">页面上的按钮是`Button`对象，它的实例`Button`类中，依次类推。</span><span class="sxs-lookup"><span data-stu-id="faae6-236">A button on the page is a `Button` object that is an instance of the `Button` class, and so on.</span></span> <span data-ttu-id="faae6-237">每个实例都有其自己的特征，但它们都基于对象的类定义中指定的内容。</span><span class="sxs-lookup"><span data-stu-id="faae6-237">Each instance has its own characteristics, but they all are based on what's specified in the object's class definition.</span></span>


## <a name="basic-syntax"></a><span data-ttu-id="faae6-238">基本语法</span><span class="sxs-lookup"><span data-stu-id="faae6-238">Basic Syntax</span></span>

<span data-ttu-id="faae6-239">前面您了解了如何创建 ASP.NET Web Pages 页，以及如何可以将服务器代码添加到 HTML 标记的一个基本示例。</span><span class="sxs-lookup"><span data-stu-id="faae6-239">Earlier you saw a basic example of how to create an ASP.NET Web Pages page, and how you can add server code to HTML markup.</span></span> <span data-ttu-id="faae6-240">本文介绍使用 Razor 语法的 ASP.NET 服务器代码的基础知识&#8212;，它是编程语言规则。</span><span class="sxs-lookup"><span data-stu-id="faae6-240">Here you'll learn the basics of writing ASP.NET server code using the Razor syntax &#8212; that is, the programming language rules.</span></span>

<span data-ttu-id="faae6-241">如果你是经验丰富的编程 （尤其是如果你使用过 C、 c + +、 C#、 Visual Basic 或 JavaScript），您现在阅读的许多并不陌生。</span><span class="sxs-lookup"><span data-stu-id="faae6-241">If you're experienced with programming (especially if you've used C, C++, C#, Visual Basic, or JavaScript), much of what you read here will be familiar.</span></span> <span data-ttu-id="faae6-242">您可能需要仅与如何将服务器代码添加到标记中了解了相关 *.cshtml*文件。</span><span class="sxs-lookup"><span data-stu-id="faae6-242">You'll probably need to familiarize yourself only with how server code is added to markup in *.cshtml* files.</span></span>

<a id="BM_CombiningTextMarkupAndCode"></a>
### <a name="combining-text-markup-and-code-in-code-blocks"></a><span data-ttu-id="faae6-243">组合文本、 标记和代码块中的代码</span><span class="sxs-lookup"><span data-stu-id="faae6-243">Combining Text, Markup, and Code in Code Blocks</span></span>

<span data-ttu-id="faae6-244">在服务器代码块内，通常要输出的文本或标记 （或两者） 到页面。</span><span class="sxs-lookup"><span data-stu-id="faae6-244">In server code blocks, you often want to output text or markup (or both) to the page.</span></span> <span data-ttu-id="faae6-245">如果服务器代码块包含的文本的不是代码和，而是应呈现是，ASP.NET 将需要能够将该文本与代码区分开来。</span><span class="sxs-lookup"><span data-stu-id="faae6-245">If a server code block contains text that's not code and that instead should be rendered as is, ASP.NET needs to be able to distinguish that text from code.</span></span> <span data-ttu-id="faae6-246">有若干方法可实现此操作。</span><span class="sxs-lookup"><span data-stu-id="faae6-246">There are several ways to do this.</span></span>

- <span data-ttu-id="faae6-247">将文本括在类似的 HTML 元素`<p></p>`或`<em></em>`:</span><span class="sxs-lookup"><span data-stu-id="faae6-247">Enclose the text in an HTML element like `<p></p>` or `<em></em>`:</span></span>   

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample12.cshtml)]

    <span data-ttu-id="faae6-248">HTML 元素可以包括文本、 其他 HTML 元素和服务器代码表达式。</span><span class="sxs-lookup"><span data-stu-id="faae6-248">The HTML element can include text, additional HTML elements, and server-code expressions.</span></span> <span data-ttu-id="faae6-249">当 ASP.NET 发现 HTML 开始标记 (例如， `<p>`)，它将呈现所有内容包括元素和作为其内容是浏览器中，按照其设想解决服务器代码表达式。</span><span class="sxs-lookup"><span data-stu-id="faae6-249">When ASP.NET sees the opening HTML tag (for example, `<p>`), it renders everything including the element and its content as is to the browser, resolving server-code expressions as it goes.</span></span>
- <span data-ttu-id="faae6-250">使用`@:`运算符或`<text>`元素。</span><span class="sxs-lookup"><span data-stu-id="faae6-250">Use the `@:` operator or the `<text>` element.</span></span> <span data-ttu-id="faae6-251">`@:`输出一行内容包含纯文本或 HTML 标记不匹配;`<text>`元素包含多行输出。</span><span class="sxs-lookup"><span data-stu-id="faae6-251">The `@:` outputs a single line of content containing plain text or unmatched HTML tags; the `<text>` element encloses multiple lines to output.</span></span> <span data-ttu-id="faae6-252">不想要作为输出的一部分呈现的 HTML 元素时，这些选项非常有用。</span><span class="sxs-lookup"><span data-stu-id="faae6-252">These options are useful when you don't want to render an HTML element as part of the output.</span></span>  

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample13.cshtml)]

    <span data-ttu-id="faae6-253">如果你想要输出多行文本或 HTML 标记不匹配，则可以在前面与每个行`@:`，或可以放置在行外侧`<text>`元素。</span><span class="sxs-lookup"><span data-stu-id="faae6-253">If you want to output multiple lines of text or unmatched HTML tags, you can precede each line with `@:`, or you can enclose the line in a `<text>` element.</span></span> <span data-ttu-id="faae6-254">像`@:`运算符，`<text>`标记 ASP.NET 用于识别文本的内容和页面输出中永远不会呈现。</span><span class="sxs-lookup"><span data-stu-id="faae6-254">Like the `@:` operator,`<text>` tags are used by ASP.NET to identify text content and are never rendered in the page output.</span></span>

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample14.cshtml)]

    <span data-ttu-id="faae6-255">第一个示例重复前面的示例，但会使用一对`<text>`标记括起要呈现的文本。</span><span class="sxs-lookup"><span data-stu-id="faae6-255">The first example repeats the previous example but uses a single pair of `<text>` tags to enclose the text to render.</span></span> <span data-ttu-id="faae6-256">在第二个示例中，`<text>`并`</text>`标记将三个行，都有一些非包含的文本和不匹配的 HTML 标记括起来 (`<br />`)，以及服务器代码和匹配的 HTML 标记。</span><span class="sxs-lookup"><span data-stu-id="faae6-256">In the second example, the `<text>` and `</text>` tags enclose three lines, all of which have some uncontained text and unmatched HTML tags (`<br />`), along with server code and matched HTML tags.</span></span> <span data-ttu-id="faae6-257">同样，还可以位于单独使用每个行`@:`运算符; 任一种方法的工作原理。</span><span class="sxs-lookup"><span data-stu-id="faae6-257">Again, you could also precede each line individually with the `@:` operator; either way works.</span></span>

    > [!NOTE]
    > <span data-ttu-id="faae6-258">当输出文本，如本部分中所示&#8212;使用 HTML 元素，`@:`运算符，或`<text>`元素&#8212;ASP.NET 不会进行 HTML 编码输出。</span><span class="sxs-lookup"><span data-stu-id="faae6-258">When you output text as shown in this section &#8212; using an HTML element, the `@:` operator, or the `<text>` element &#8212; ASP.NET doesn't HTML-encode the output.</span></span> <span data-ttu-id="faae6-259">(如前文所述，ASP.NET does 对服务器的代码表达式的前面使用的服务器代码块的输出进行编码`@`，本节中所述的特殊情况除外。)</span><span class="sxs-lookup"><span data-stu-id="faae6-259">(As noted earlier, ASP.NET does encode the output of server code expressions and server code blocks that are preceded by `@`, except in the special cases noted in this section.)</span></span>

### <a name="whitespace"></a><span data-ttu-id="faae6-260">Whitespace</span><span class="sxs-lookup"><span data-stu-id="faae6-260">Whitespace</span></span>

<span data-ttu-id="faae6-261">在语句中 （和字符串文字之外） 额外空间不会影响该语句：</span><span class="sxs-lookup"><span data-stu-id="faae6-261">Extra spaces in a statement (and outside of a string literal) don't affect the statement:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample15.cshtml)]

<span data-ttu-id="faae6-262">在语句中的一个分行符语句上的无效，且可换行以提高可读性的语句。</span><span class="sxs-lookup"><span data-stu-id="faae6-262">A line break in a statement has no effect on the statement, and you can wrap statements for readability.</span></span> <span data-ttu-id="faae6-263">以下语句是相同的：</span><span class="sxs-lookup"><span data-stu-id="faae6-263">The following statements are the same:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample16.cshtml)]

<span data-ttu-id="faae6-264">但是，您将无法打包中间字符串文本行。</span><span class="sxs-lookup"><span data-stu-id="faae6-264">However, you can't wrap a line in the middle of a string literal.</span></span> <span data-ttu-id="faae6-265">下面的示例不起作用：</span><span class="sxs-lookup"><span data-stu-id="faae6-265">The following example doesn't work:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample17.cshtml)]

<span data-ttu-id="faae6-266">若要组合的长字符串，如上面的代码中的多个行包装，有两个选项。</span><span class="sxs-lookup"><span data-stu-id="faae6-266">To combine a long string that wraps to multiple lines like the above code, there are two options.</span></span> <span data-ttu-id="faae6-267">可以使用串联运算符 (`+`)，您将会看到这篇文章中更高版本。</span><span class="sxs-lookup"><span data-stu-id="faae6-267">You can use the concatenation operator (`+`), which you'll see later in this article.</span></span> <span data-ttu-id="faae6-268">此外可以使用`@`创建原义字符串文本，如本文前面所看到的字符。</span><span class="sxs-lookup"><span data-stu-id="faae6-268">You can also use the `@` character to create a verbatim string literal, as you saw earlier in this article.</span></span> <span data-ttu-id="faae6-269">可以位于同一行中的原义字符串文本：</span><span class="sxs-lookup"><span data-stu-id="faae6-269">You can break verbatim string literals across lines:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample18.cshtml)]

### <a name="code-and-markup-comments"></a><span data-ttu-id="faae6-270">代码 （和标记） 的注释</span><span class="sxs-lookup"><span data-stu-id="faae6-270">Code (and Markup) Comments</span></span>

<span data-ttu-id="faae6-271">注释使您可以保留为自己或他人的说明。</span><span class="sxs-lookup"><span data-stu-id="faae6-271">Comments let you leave notes for yourself or others.</span></span> <span data-ttu-id="faae6-272">它们还允许您禁用 (*注释掉*) 代码或标记，您不想运行，但想要暂时在页中保留的部分。</span><span class="sxs-lookup"><span data-stu-id="faae6-272">They also allow you to disable (*comment out*) a section of code or markup that you don't want to run but want to keep in your page for the time being.</span></span>

<span data-ttu-id="faae6-273">没有其他注释语法 Razor 代码以及 HTML 标记。</span><span class="sxs-lookup"><span data-stu-id="faae6-273">There's different commenting syntax for Razor code and for HTML markup.</span></span> <span data-ttu-id="faae6-274">与所有 Razor 代码一样，Razor 注释处理 （，然后删除） 页发送到浏览器之前在服务器上。</span><span class="sxs-lookup"><span data-stu-id="faae6-274">As with all Razor code, Razor comments are processed (and then removed) on the server before the page is sent to the browser.</span></span> <span data-ttu-id="faae6-275">因此，Razor 注释语法允许您将编辑该文件，但用户看不到，即使在页源时，可以看到的注释的代码 （或甚至到标记）。</span><span class="sxs-lookup"><span data-stu-id="faae6-275">Therefore, the Razor commenting syntax lets you put comments into the code (or even into the markup) that you can see when you edit the file, but that users don't see, even in the page source.</span></span>

<span data-ttu-id="faae6-276">ASP.NET Razor 注释的开始与注释`@*`日期和结束其与`*@`。</span><span class="sxs-lookup"><span data-stu-id="faae6-276">For ASP.NET Razor comments, you start the comment with `@*` and end it with `*@`.</span></span> <span data-ttu-id="faae6-277">注释可以为一行或多个行上：</span><span class="sxs-lookup"><span data-stu-id="faae6-277">The comment can be on one line or multiple lines:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample19.cshtml)]

<span data-ttu-id="faae6-278">下面是一个代码块中的注释：</span><span class="sxs-lookup"><span data-stu-id="faae6-278">Here is a comment within a code block:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample20.cshtml)]

<span data-ttu-id="faae6-279">下面的代码行使用同一个块的代码，注释掉，以便它不会运行：</span><span class="sxs-lookup"><span data-stu-id="faae6-279">Here is the same block of code, with the line of code commented out so that it won't run:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample21.cshtml)]

<span data-ttu-id="faae6-280">在代码块中，作为一种方式使用 Razor 注释语法，您可以使用注释使用的，如 C# 的编程语言的语法：</span><span class="sxs-lookup"><span data-stu-id="faae6-280">Inside a code block, as an alternative to using Razor comment syntax, you can use the commenting syntax of the programming language you're using, such as C#:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample22.cshtml)]

<span data-ttu-id="faae6-281">在 C# 中的单行注释的前面有`//`字符和多行注释开头`/*`开头和结尾`*/`。</span><span class="sxs-lookup"><span data-stu-id="faae6-281">In C#, single-line comments are preceded by the `//` characters, and multi-line comments begin with `/*` and end with `*/`.</span></span> <span data-ttu-id="faae6-282">（使用 Razor 注释，如 C# 注释不会呈现到浏览器。）</span><span class="sxs-lookup"><span data-stu-id="faae6-282">(As with Razor comments, C# comments are not rendered to the browser.)</span></span>

<span data-ttu-id="faae6-283">标记中，您可能知道，可以创建 HTML 注释：</span><span class="sxs-lookup"><span data-stu-id="faae6-283">For markup, as you probably know, you can create an HTML comment:</span></span>

[!code-xml[Main](introducing-razor-syntax-c/samples/sample23.xml)]

<span data-ttu-id="faae6-284">HTML 注释开头`<!--`字符和结尾`-->`。</span><span class="sxs-lookup"><span data-stu-id="faae6-284">HTML comments start with `<!--` characters and end with `-->`.</span></span> <span data-ttu-id="faae6-285">您可以使用 HTML 注释来包围不仅文本，而且还可能想要保留的页中，但不想呈现任何 HTML 标记。</span><span class="sxs-lookup"><span data-stu-id="faae6-285">You can use HTML comments to surround not only text, but also any HTML markup that you may want to keep in the page but don't want to render.</span></span> <span data-ttu-id="faae6-286">此 HTML 注释将隐藏标记和它们所包含的文本的整个内容：</span><span class="sxs-lookup"><span data-stu-id="faae6-286">This HTML comment will hide the entire content of the tags and the text they contain:</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample24.html)]

<span data-ttu-id="faae6-287">与 Razor 注释，HTML 注释不同*是*呈现给页和用户可以通过查看页面源文件来查看它们。</span><span class="sxs-lookup"><span data-stu-id="faae6-287">Unlike Razor comments, HTML comments *are* rendered to the page and the user can see them by viewing the page source.</span></span>

<span data-ttu-id="faae6-288">Razor 在嵌套的块中的 C# 上存在限制。</span><span class="sxs-lookup"><span data-stu-id="faae6-288">Razor has limitations on nested blocks of C#.</span></span> <span data-ttu-id="faae6-289">有关详细信息请参阅[名为 C# 变量和嵌套的块生成中断代码](http://aspnetwebstack.codeplex.com/workitem/1914)</span><span class="sxs-lookup"><span data-stu-id="faae6-289">For more information see [Named C# Variables and Nested Blocks Generate Broken Code](http://aspnetwebstack.codeplex.com/workitem/1914)</span></span>

## <a name="variables"></a><span data-ttu-id="faae6-290">变量</span><span class="sxs-lookup"><span data-stu-id="faae6-290">Variables</span></span>

<span data-ttu-id="faae6-291">变量是命名的对象，用于存储数据。</span><span class="sxs-lookup"><span data-stu-id="faae6-291">A variable is a named object that you use to store data.</span></span> <span data-ttu-id="faae6-292">您可以命名变量任何内容，但该名称必须以字母字符开头，不能包含空格或保留的字符。</span><span class="sxs-lookup"><span data-stu-id="faae6-292">You can name variables anything, but the name must begin with an alphabetic character and it cannot contain whitespace or reserved characters.</span></span>

### <a name="variables-and-data-types"></a><span data-ttu-id="faae6-293">变量和数据类型</span><span class="sxs-lookup"><span data-stu-id="faae6-293">Variables and Data Types</span></span>

<span data-ttu-id="faae6-294">变量可以具有特定的数据类型，指示在变量中存储的数据的种类。</span><span class="sxs-lookup"><span data-stu-id="faae6-294">A variable can have a specific data type, which indicates what kind of data is stored in the variable.</span></span> <span data-ttu-id="faae6-295">你可以存储字符串值的字符串变量 (如&quot;Hello world&quot;)，存储 （如 3 或 79） 的整数值的整数变量和存储中以不同的格式 （如 2012 年 4 月 12 日或 2009 年 3 月的日期值的日期变量).</span><span class="sxs-lookup"><span data-stu-id="faae6-295">You can have string variables that store string values (like &quot;Hello world&quot;), integer variables that store whole-number values (like 3 or 79), and date variables that store date values in a variety of formats (like 4/12/2012 or March 2009).</span></span> <span data-ttu-id="faae6-296">还有许多可以使用其他数据类型。</span><span class="sxs-lookup"><span data-stu-id="faae6-296">And there are many other data types you can use.</span></span>

<span data-ttu-id="faae6-297">但是，你通常无需指定类型的变量。</span><span class="sxs-lookup"><span data-stu-id="faae6-297">However, you generally don't have to specify a type for a variable.</span></span> <span data-ttu-id="faae6-298">大多数情况下，ASP.NET 可找出基于变量中的数据的使用方式的类型。</span><span class="sxs-lookup"><span data-stu-id="faae6-298">Most of the time, ASP.NET can figure out the type based on how the data in the variable is being used.</span></span> <span data-ttu-id="faae6-299">（有时必须指定一个类型; 您将看到示例这为 true。）</span><span class="sxs-lookup"><span data-stu-id="faae6-299">(Occasionally you must specify a type; you'll see examples where this is true.)</span></span>

<span data-ttu-id="faae6-300">声明变量使用`var`关键字 （如果不想指定类型） 或使用的类型名称：</span><span class="sxs-lookup"><span data-stu-id="faae6-300">You declare a variable using the `var` keyword (if you don't want to specify a type) or by using the name of the type:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample25.cshtml)]

<span data-ttu-id="faae6-301">下面的示例演示在网页中的变量的一些典型用法：</span><span class="sxs-lookup"><span data-stu-id="faae6-301">The following example shows some typical uses of variables in a web page:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample26.cshtml)]

<span data-ttu-id="faae6-302">如果合并前面的示例页中，你会看到此浏览器中显示：</span><span class="sxs-lookup"><span data-stu-id="faae6-302">If you combine the previous examples in a page, you see this displayed in a browser:</span></span>

![Razor-Img9](introducing-razor-syntax-c/_static/image9.jpg)

### <a name="converting-and-testing-data-types"></a><span data-ttu-id="faae6-304">转换和测试数据类型</span><span class="sxs-lookup"><span data-stu-id="faae6-304">Converting and Testing Data Types</span></span>

<span data-ttu-id="faae6-305">尽管 ASP.NET 通常可以自动确定数据类型，但有时不能进行。</span><span class="sxs-lookup"><span data-stu-id="faae6-305">Although ASP.NET can usually determine a data type automatically, sometimes it can't.</span></span> <span data-ttu-id="faae6-306">因此，您可能需要通过执行显式转换来帮助解决问题的 ASP.NET。</span><span class="sxs-lookup"><span data-stu-id="faae6-306">Therefore, you might need to help ASP.NET out by performing an explicit conversion.</span></span> <span data-ttu-id="faae6-307">即使您没有将类型转换，有时很有帮助进行测试以查看哪些类型的数据，可能正在处理。</span><span class="sxs-lookup"><span data-stu-id="faae6-307">Even if you don't have to convert types, sometimes it's helpful to test to see what type of data you might be working with.</span></span>

<span data-ttu-id="faae6-308">最常见的情况是，您必须将字符串转换为另一种类型，如向整数或日期。</span><span class="sxs-lookup"><span data-stu-id="faae6-308">The most common case is that you have to convert a string to another type, such as to an integer or date.</span></span> <span data-ttu-id="faae6-309">下面的示例演示一个典型的例子，必须将字符串转换为数字。</span><span class="sxs-lookup"><span data-stu-id="faae6-309">The following example shows a typical case where you must convert a string to a number.</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample27.cshtml)]

<span data-ttu-id="faae6-310">通常，用户输入到你以字符串形式提供。</span><span class="sxs-lookup"><span data-stu-id="faae6-310">As a rule, user input comes to you as strings.</span></span> <span data-ttu-id="faae6-311">即使系统已提示用户输入一个数字，并且即使在提交用户输入以及代码中读取时所输入的一个数字，数据的格式字符串。</span><span class="sxs-lookup"><span data-stu-id="faae6-311">Even if you've prompted users to enter a number, and even if they've entered a digit, when user input is submitted and you read it in code, the data is in string format.</span></span> <span data-ttu-id="faae6-312">因此，必须将字符串转换为数字。</span><span class="sxs-lookup"><span data-stu-id="faae6-312">Therefore, you must convert the string to a number.</span></span> <span data-ttu-id="faae6-313">在示例中，如果你尝试值执行算术运算，而不转换它们，出现以下错误结果，因为 ASP.NET 不能添加两个字符串：</span><span class="sxs-lookup"><span data-stu-id="faae6-313">In the example, if you try to perform arithmetic on the values without converting them, the following error results, because ASP.NET cannot add two strings:</span></span>

<span data-ttu-id="faae6-314">*不能隐式转换为 int 的 string 类型。*</span><span class="sxs-lookup"><span data-stu-id="faae6-314">*Cannot implicitly convert type 'string' to 'int'.*</span></span>

<span data-ttu-id="faae6-315">若要将值转换为整数，则调用`AsInt`方法。</span><span class="sxs-lookup"><span data-stu-id="faae6-315">To convert the values to integers, you call the `AsInt` method.</span></span> <span data-ttu-id="faae6-316">如果转换成功，您可以将数字。</span><span class="sxs-lookup"><span data-stu-id="faae6-316">If the conversion is successful, you can then add the numbers.</span></span>

<span data-ttu-id="faae6-317">下表列出了一些常见的转换和测试方法的变量。</span><span class="sxs-lookup"><span data-stu-id="faae6-317">The following table lists some common conversion and test methods for variables.</span></span>

:::row:::
    :::column:::
    <span data-ttu-id="faae6-318"><strong>方法</strong></span><span class="sxs-lookup"><span data-stu-id="faae6-318"><strong>Method</strong></span></span>
    :::column-end:::
    :::column:::
    <span data-ttu-id="faae6-319"><strong>说明</strong></span><span class="sxs-lookup"><span data-stu-id="faae6-319"><strong>Description</strong></span></span>
    :::column-end:::
    :::column:::
    <span data-ttu-id="faae6-320"><strong>示例</strong></span><span class="sxs-lookup"><span data-stu-id="faae6-320"><strong>Example</strong></span></span>
    :::column-end:::
:::row-end:::
* * *
:::row:::
    :::column:::
        `AsInt(), IsInt()`
    :::column-end:::
    :::column:::
    <span data-ttu-id="faae6-321">将转换为整数表示 （如"593") 的整数的字符串。</span><span class="sxs-lookup"><span data-stu-id="faae6-321">Converts a string that represents a whole number (like "593") to an integer.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample28.cs)]
    :::column-end:::
:::row-end:::
* * *
:::row:::
    :::column:::
        `AsBool(), IsBool()`
    :::column-end:::
    :::column:::
    <span data-ttu-id="faae6-322">将转换字符串，如&quot;，则返回 true&quot;或&quot;false&quot;为 Boolean 类型。</span><span class="sxs-lookup"><span data-stu-id="faae6-322">Converts a string like &quot;true&quot; or &quot;false&quot; to a Boolean type.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample29.cs)]
    :::column-end:::
:::row-end:::
* * *
:::row:::
    :::column:::
        `AsFloat(), IsFloat()`
    :::column-end:::
    :::column:::
    <span data-ttu-id="faae6-323">将具有类似的十进制值的字符串转换&quot;1.3&quot;或&quot;7.439&quot;为浮点数。</span><span class="sxs-lookup"><span data-stu-id="faae6-323">Converts a string that has a decimal value like &quot;1.3&quot; or &quot;7.439&quot; to a floating-point number.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample30.cs)]
    :::column-end:::
:::row-end:::
* * *
:::row:::
    :::column:::
        `AsDecimal(), IsDecimal()`
    :::column-end:::
    :::column:::
    <span data-ttu-id="faae6-324">将具有类似的十进制值的字符串转换&quot;1.3&quot;或&quot;7.439&quot;为十进制数。</span><span class="sxs-lookup"><span data-stu-id="faae6-324">Converts a string that has a decimal value like &quot;1.3&quot; or &quot;7.439&quot; to a decimal number.</span></span> <span data-ttu-id="faae6-325">（在 ASP.NET 中，十进制数字是一个浮点数，更详细地说明。）</span><span class="sxs-lookup"><span data-stu-id="faae6-325">(In ASP.NET, a decimal number is more precise than a floating-point number.)</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample31.cs)]
    :::column-end:::
:::row-end:::
* * *
:::row:::
    :::column:::
        `AsDateTime(), IsDateTime()`
    :::column-end:::
    :::column:::
    <span data-ttu-id="faae6-326">将对 ASP.NET 表示的日期和时间值的字符串转换`DateTime`类型。</span><span class="sxs-lookup"><span data-stu-id="faae6-326">Converts a string that represents a date and time value to the ASP.NET `DateTime` type.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample32.cs)]
    :::column-end:::
:::row-end:::
* * *
:::row:::
    :::column:::
        `ToString()`
    :::column-end:::
    :::column:::
    <span data-ttu-id="faae6-327">将任何其他数据类型转换为字符串。</span><span class="sxs-lookup"><span data-stu-id="faae6-327">Converts any other data type to a string.</span></span>
    :::column-end:::
    :::column:::
        [!code-javascript[Main](introducing-razor-syntax-c/samples/sample33.js)]
    :::column-end:::
:::row-end:::

## <a name="operators"></a><span data-ttu-id="faae6-328">运算符</span><span class="sxs-lookup"><span data-stu-id="faae6-328">Operators</span></span>

<span data-ttu-id="faae6-329">运算符是命令的关键字或告诉 ASP.NET 什么样来执行在表达式中的字符。</span><span class="sxs-lookup"><span data-stu-id="faae6-329">An operator is a keyword or character that tells ASP.NET what kind of command to perform in an expression.</span></span> <span data-ttu-id="faae6-330">C# 语言 （及对其基于 Razor 语法） 支持很多运算符，但只需识别几个开始。</span><span class="sxs-lookup"><span data-stu-id="faae6-330">The C# language (and the Razor syntax that's based on it) supports many operators, but you only need to recognize a few to get started.</span></span> <span data-ttu-id="faae6-331">下表总结了最常见的运算符。</span><span class="sxs-lookup"><span data-stu-id="faae6-331">The following table summarizes the most common operators.</span></span>


:::row:::
    :::column:::
    <span data-ttu-id="faae6-332"><strong>Operator</strong></span><span class="sxs-lookup"><span data-stu-id="faae6-332"><strong>Operator</strong></span></span>
    :::column-end:::
    :::column:::
    <span data-ttu-id="faae6-333"><strong>说明</strong></span><span class="sxs-lookup"><span data-stu-id="faae6-333"><strong>Description</strong></span></span>
    :::column-end:::
    :::column:::
    <span data-ttu-id="faae6-334"><strong>示例</strong></span><span class="sxs-lookup"><span data-stu-id="faae6-334"><strong>Examples</strong></span></span>
    :::column-end:::
:::row-end:::
* * *
:::row:::
    :::column:::
        `+` `-` `*` `/`
    :::column-end:::
    :::column:::
    <span data-ttu-id="faae6-335">在数值表达式中使用的数学运算符。</span><span class="sxs-lookup"><span data-stu-id="faae6-335">Math operators used in numerical expressions.</span></span>
    :::column-end:::
    :::column:::
        [!code-css[Main](introducing-razor-syntax-c/samples/sample34.css)]
    :::column-end:::
:::row-end:::
* * *
:::row:::
    :::column:::
        `=`
    :::column-end:::
    :::column:::
    <span data-ttu-id="faae6-336">赋值。</span><span class="sxs-lookup"><span data-stu-id="faae6-336">Assignment.</span></span> <span data-ttu-id="faae6-337">将一条语句右侧的值分配给左侧和右侧的对象。</span><span class="sxs-lookup"><span data-stu-id="faae6-337">Assigns the value on the right side of a statement to the object on the left side.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample35.cs)]
    :::column-end:::
:::row-end:::
* * *
:::row:::
    :::column:::
        `==`
    :::column-end:::
    :::column:::
    <span data-ttu-id="faae6-338">相等。</span><span class="sxs-lookup"><span data-stu-id="faae6-338">Equality.</span></span> <span data-ttu-id="faae6-339">返回`true`值是否相等。</span><span class="sxs-lookup"><span data-stu-id="faae6-339">Returns `true` if the values are equal.</span></span> <span data-ttu-id="faae6-340">(请注意之间的区别`=`运算符和`==`运算符。)</span><span class="sxs-lookup"><span data-stu-id="faae6-340">(Notice the distinction between the `=` operator and the `==` operator.)</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample36.cs)]
    :::column-end:::
:::row-end:::
* * *
:::row:::
    :::column:::
        `!=`
    :::column-end:::
    :::column:::
    <span data-ttu-id="faae6-341">不相等。</span><span class="sxs-lookup"><span data-stu-id="faae6-341">Inequality.</span></span> <span data-ttu-id="faae6-342">返回`true`如果值不相等。</span><span class="sxs-lookup"><span data-stu-id="faae6-342">Returns `true` if the values are not equal.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample37.cs)]
    :::column-end:::
:::row-end:::
* * *
:::row:::
    :::column:::
        `< > <= >=`
    :::column-end:::
    :::column:::
    <span data-ttu-id="faae6-343">更少的相比，更高的比，小于-或者-等于，以及大于或等于。</span><span class="sxs-lookup"><span data-stu-id="faae6-343">Less-than, greater-than, less-than-or-equal, and greater-than-or-equal.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample38.cs)]
    :::column-end:::
:::row-end:::
* * *
:::row:::
    :::column:::
        `+`
    :::column-end:::
    :::column:::
    <span data-ttu-id="faae6-344">串联用于联接的字符串。</span><span class="sxs-lookup"><span data-stu-id="faae6-344">Concatenation, which is used to join strings.</span></span> <span data-ttu-id="faae6-345">ASP.NET 就会知道此运算符和加法运算符的表达式的数据类型之间的差异。</span><span class="sxs-lookup"><span data-stu-id="faae6-345">ASP.NET knows the difference between this operator and the addition operator based on the data type of the expression.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample39.cs)]
    :::column-end:::
:::row-end:::
* * *
:::row:::
    :::column:::
        `+=` `-=`
    :::column-end:::
    :::column:::
    <span data-ttu-id="faae6-346">递增和递减运算符，从而添加，并且从变量 （分别） 减 1。</span><span class="sxs-lookup"><span data-stu-id="faae6-346">The increment and decrement operators, which add and subtract 1 (respectively) from a variable.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample40.cs)]
    :::column-end:::
:::row-end:::
* * *
:::row:::
    :::column:::
        `.`
    :::column-end:::
    :::column:::
    <span data-ttu-id="faae6-347">圆点。</span><span class="sxs-lookup"><span data-stu-id="faae6-347">Dot.</span></span> <span data-ttu-id="faae6-348">用于区分对象及其属性和方法。</span><span class="sxs-lookup"><span data-stu-id="faae6-348">Used to distinguish objects and their properties and methods.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample41.cs)]
    :::column-end:::
:::row-end:::
* * *
:::row:::
    :::column:::
        `()`
    :::column-end:::
    :::column:::
    <span data-ttu-id="faae6-349">括号。</span><span class="sxs-lookup"><span data-stu-id="faae6-349">Parentheses.</span></span> <span data-ttu-id="faae6-350">使用组表达式，并将参数传递给方法。</span><span class="sxs-lookup"><span data-stu-id="faae6-350">Used to group expressions and to pass parameters to methods.</span></span>
    :::column-end:::
    :::column:::
        [!code-javascript[Main](introducing-razor-syntax-c/samples/sample42.js)]
    :::column-end:::
:::row-end:::
* * *
:::row:::
    :::column:::
        `[]`
    :::column-end:::
    :::column:::
    <span data-ttu-id="faae6-351">方括号。</span><span class="sxs-lookup"><span data-stu-id="faae6-351">Brackets.</span></span> <span data-ttu-id="faae6-352">用于访问数组或集合中的值。</span><span class="sxs-lookup"><span data-stu-id="faae6-352">Used for accessing values in arrays or collections.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample43.cs)]
    :::column-end:::
:::row-end:::
* * *
:::row:::
    :::column:::
        `!`
    :::column-end:::
    :::column:::
    <span data-ttu-id="faae6-353">不。</span><span class="sxs-lookup"><span data-stu-id="faae6-353">Not.</span></span> <span data-ttu-id="faae6-354">反转`true`值设为`false`，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="faae6-354">Reverses a `true` value to `false` and vice versa.</span></span> <span data-ttu-id="faae6-355">通常用作测试的速记方法`false`(即，对于不`true`)。</span><span class="sxs-lookup"><span data-stu-id="faae6-355">Typically used as a shorthand way to test for `false` (that is, for not `true`).</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample44.cs)]
    :::column-end:::
:::row-end:::
* * *
:::row:::
    :::column:::
        `&&` <code>&#124;&#124;</code>
    :::column-end:::
    :::column:::
    <span data-ttu-id="faae6-356">逻辑 AND 和 OR，用于链接在一起条件。</span><span class="sxs-lookup"><span data-stu-id="faae6-356">Logical AND and OR, which are used to link conditions together.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample45.cs)]
    :::column-end:::
:::row-end:::

<a id="ID_WorkingWithFileAndFolderPaths"></a>
## <a name="working-with-file-and-folder-paths-in-code"></a><span data-ttu-id="faae6-357">使用文件和代码中的文件夹路径</span><span class="sxs-lookup"><span data-stu-id="faae6-357">Working with File and Folder Paths in Code</span></span>

<span data-ttu-id="faae6-358">将在代码中经常处理的文件和文件夹的路径。</span><span class="sxs-lookup"><span data-stu-id="faae6-358">You'll often work with file and folder paths in your code.</span></span> <span data-ttu-id="faae6-359">下面是用于网站的物理文件夹结构的示例，它可能会显示在开发计算机上：</span><span class="sxs-lookup"><span data-stu-id="faae6-359">Here is an example of physical folder structure for a website as it might appear on your development computer:</span></span>

`C:\WebSites\MyWebSite default.cshtml datafile.txt \images Logo.jpg \styles Styles.css`

<span data-ttu-id="faae6-360">下面是一些有关 Url 和路径的重要详细信息：</span><span class="sxs-lookup"><span data-stu-id="faae6-360">Here are some essential details about URLs and paths:</span></span>

- <span data-ttu-id="faae6-361">开始使用的域名的 URL (`http://www.example.com`) 或服务器名称 (`http://localhost`， `http://mycomputer`)。</span><span class="sxs-lookup"><span data-stu-id="faae6-361">A URL begins with either a domain name (`http://www.example.com`) or a server name (`http://localhost`, `http://mycomputer`).</span></span>
- <span data-ttu-id="faae6-362">URL 对应于主机计算机上的物理路径。</span><span class="sxs-lookup"><span data-stu-id="faae6-362">A URL corresponds to a physical path on a host computer.</span></span> <span data-ttu-id="faae6-363">例如，`http://myserver`可能对应于文件夹*C:\websites\mywebsite*在服务器上。</span><span class="sxs-lookup"><span data-stu-id="faae6-363">For example, `http://myserver` might correspond to the folder *C:\websites\mywebsite* on the server.</span></span>
- <span data-ttu-id="faae6-364">虚拟路径是简写形式来表示在代码中的路径，而无需指定完整路径。</span><span class="sxs-lookup"><span data-stu-id="faae6-364">A virtual path is shorthand to represent paths in code without having to specify the full path.</span></span> <span data-ttu-id="faae6-365">它包括遵守域或服务器名称的 URL 的一部分。</span><span class="sxs-lookup"><span data-stu-id="faae6-365">It includes the portion of a URL that follows the domain or server name.</span></span> <span data-ttu-id="faae6-366">当你使用的虚拟路径时，可以而无需更新的路径，你的代码移动到不同的域或服务器。</span><span class="sxs-lookup"><span data-stu-id="faae6-366">When you use virtual paths, you can move your code to a different domain or server without having to update the paths.</span></span>

<span data-ttu-id="faae6-367">下面是一个示例，帮助您了解的差异：</span><span class="sxs-lookup"><span data-stu-id="faae6-367">Here's an example to help you understand the differences:</span></span>

| <span data-ttu-id="faae6-368">完整的 URL</span><span class="sxs-lookup"><span data-stu-id="faae6-368">Complete URL</span></span> | `http://mycompanyserver/humanresources/CompanyPolicy.htm` |
| --- | --- |
| <span data-ttu-id="faae6-369">服务器名称</span><span class="sxs-lookup"><span data-stu-id="faae6-369">Server name</span></span> | <span data-ttu-id="faae6-370">*mycompanyserver*</span><span class="sxs-lookup"><span data-stu-id="faae6-370">*mycompanyserver*</span></span> |
| <span data-ttu-id="faae6-371">虚拟路径</span><span class="sxs-lookup"><span data-stu-id="faae6-371">Virtual path</span></span> | <span data-ttu-id="faae6-372">*/humanresources/CompanyPolicy.htm*</span><span class="sxs-lookup"><span data-stu-id="faae6-372">*/humanresources/CompanyPolicy.htm*</span></span> |
| <span data-ttu-id="faae6-373">物理路径</span><span class="sxs-lookup"><span data-stu-id="faae6-373">Physical path</span></span> | <span data-ttu-id="faae6-374">*C:\mywebsites\humanresources\CompanyPolicy.htm*</span><span class="sxs-lookup"><span data-stu-id="faae6-374">*C:\mywebsites\humanresources\CompanyPolicy.htm*</span></span> |

<span data-ttu-id="faae6-375">虚拟根目录为 /，就像在 c： 驱动器是 \。</span><span class="sxs-lookup"><span data-stu-id="faae6-375">The virtual root is /, just like the root of your C: drive is \.</span></span> <span data-ttu-id="faae6-376">（虚拟文件夹路径始终使用正斜杠。）文件夹的虚拟路径不需要作为物理文件夹; 具有相同的名称它可以是一个别名。</span><span class="sxs-lookup"><span data-stu-id="faae6-376">(Virtual folder paths always use forward slashes.) The virtual path of a folder doesn't have to have the same name as the physical folder; it can be an alias.</span></span> <span data-ttu-id="faae6-377">（在生产服务器上的虚拟路径很少与匹配确切的物理路径。）</span><span class="sxs-lookup"><span data-stu-id="faae6-377">(On production servers, the virtual path rarely matches an exact physical path.)</span></span>

<span data-ttu-id="faae6-378">代码中的文件和文件夹时，有时您需要引用的物理路径，有时也是虚拟路径，具体取决于您正在使用哪些对象。</span><span class="sxs-lookup"><span data-stu-id="faae6-378">When you work with files and folders in code, sometimes you need to reference the physical path and sometimes a virtual path, depending on what objects you're working with.</span></span> <span data-ttu-id="faae6-379">ASP.NET 提供了这些工具用于在代码中的文件和文件夹路径：`Server.MapPath`方法，并`~`运算符和`Href`方法。</span><span class="sxs-lookup"><span data-stu-id="faae6-379">ASP.NET gives you these tools for working with file and folder paths in code: the `Server.MapPath` method, and the `~` operator and `Href` method.</span></span>

### <a name="converting-virtual-to-physical-paths-the-servermappath-method"></a><span data-ttu-id="faae6-380">转换虚拟与物理路径： Server.MapPath 方法</span><span class="sxs-lookup"><span data-stu-id="faae6-380">Converting virtual to physical paths: the Server.MapPath method</span></span>

<span data-ttu-id="faae6-381">`Server.MapPath`方法将为虚拟路径 (如 */default.cshtml*) 为绝对物理路径 (如*C:\WebSites\MyWebSiteFolder\default.cshtml*)。</span><span class="sxs-lookup"><span data-stu-id="faae6-381">The `Server.MapPath` method converts a virtual path (like */default.cshtml*) to an absolute physical path (like *C:\WebSites\MyWebSiteFolder\default.cshtml*).</span></span> <span data-ttu-id="faae6-382">每当您需要完整的物理路径使用此方法。</span><span class="sxs-lookup"><span data-stu-id="faae6-382">You use this method any time you need a complete physical path.</span></span> <span data-ttu-id="faae6-383">典型示例是要读取或写入文本文件或 web 服务器上的图像文件时。</span><span class="sxs-lookup"><span data-stu-id="faae6-383">A typical example is when you're reading or writing a text file or image file on the web server.</span></span>

<span data-ttu-id="faae6-384">通常不知道你的站点托管站点服务器上的绝对物理路径，因此此方法可以将路径转换您知道的虚拟路径 — 到您的服务器上的相应路径。</span><span class="sxs-lookup"><span data-stu-id="faae6-384">You typically don't know the absolute physical path of your site on a hosting site's server, so this method can convert the path you do know — the virtual path — to the corresponding path on the server for you.</span></span> <span data-ttu-id="faae6-385">将虚拟路径传递给文件或文件夹的方法，并返回的物理路径：</span><span class="sxs-lookup"><span data-stu-id="faae6-385">You pass the virtual path to a file or folder to the method, and it returns the physical path:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample46.cshtml)]

### <a name="referencing-the-virtual-root-the--operator-and-href-method"></a><span data-ttu-id="faae6-386">引用虚拟根： ~ 运算符和 Href 方法</span><span class="sxs-lookup"><span data-stu-id="faae6-386">Referencing the virtual root: the ~ operator and Href method</span></span>

<span data-ttu-id="faae6-387">在中 *.cshtml*或 *.vbhtml*文件中，您可以引用虚拟根路径使用`~`运算符。</span><span class="sxs-lookup"><span data-stu-id="faae6-387">In a *.cshtml* or *.vbhtml* file, you can reference the virtual root path using the `~` operator.</span></span> <span data-ttu-id="faae6-388">这是非常方便，因为您可以来回移动网页，在站点中，并且它们包含到其他页面的任何链接不会被破坏。</span><span class="sxs-lookup"><span data-stu-id="faae6-388">This is very handy because you can move pages around in a site, and any links they contain to other pages won't be broken.</span></span> <span data-ttu-id="faae6-389">如果曾经将你的网站移动到另一个位置还有非常方便。</span><span class="sxs-lookup"><span data-stu-id="faae6-389">It's also handy in case you ever move your website to a different location.</span></span> <span data-ttu-id="faae6-390">下面是一些可能的恶意活动：</span><span class="sxs-lookup"><span data-stu-id="faae6-390">Here are some examples:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample47.cshtml)]

<span data-ttu-id="faae6-391">如果网站`http://myserver/myapp`，下面是如何 ASP.NET 会将这些路径运行页面时：</span><span class="sxs-lookup"><span data-stu-id="faae6-391">If the website is `http://myserver/myapp`, here's how ASP.NET will treat these paths when the page runs:</span></span>

- <span data-ttu-id="faae6-392">`myImagesFolder`: `http://myserver/myapp/images`</span><span class="sxs-lookup"><span data-stu-id="faae6-392">`myImagesFolder`: `http://myserver/myapp/images`</span></span>
- <span data-ttu-id="faae6-393">`myStyleSheet` : `http://myserver/myapp/styles/Stylesheet.css`</span><span class="sxs-lookup"><span data-stu-id="faae6-393">`myStyleSheet` : `http://myserver/myapp/styles/Stylesheet.css`</span></span>

<span data-ttu-id="faae6-394">（您实际上不会看到这些路径作为该变量的值，但像这就是它们的是，ASP.NET 会将路径）。</span><span class="sxs-lookup"><span data-stu-id="faae6-394">(You won't actually see these paths as the values of the variable, but ASP.NET will treat the paths as if that's what they were.)</span></span>

<span data-ttu-id="faae6-395">可以使用`~`运算符 （如上所述） 的服务器代码中和在标记中，像这样：</span><span class="sxs-lookup"><span data-stu-id="faae6-395">You can use the `~` operator both in server code (as above) and in markup, like this:</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample48.html)]

<span data-ttu-id="faae6-396">在标记中，您使用`~`运算符来创建资源，如图像文件、 其他网页和 CSS 文件的路径。</span><span class="sxs-lookup"><span data-stu-id="faae6-396">In markup, you use the `~` operator to create paths to resources like image files, other web pages, and CSS files.</span></span> <span data-ttu-id="faae6-397">页运行时，ASP.NET 页面 （代码和标记） 中查找并解决所有`~`引用到适当的路径。</span><span class="sxs-lookup"><span data-stu-id="faae6-397">When the page runs, ASP.NET looks through the page (both code and markup) and resolves all the `~` references to the appropriate path.</span></span>

## <a name="conditional-logic-and-loops"></a><span data-ttu-id="faae6-398">条件逻辑和循环</span><span class="sxs-lookup"><span data-stu-id="faae6-398">Conditional Logic and Loops</span></span>

<span data-ttu-id="faae6-399">ASP.NET 服务器代码可以执行基于条件的任务，并编写特定次数的重复语句的代码 （即，运行一个循环的代码）。</span><span class="sxs-lookup"><span data-stu-id="faae6-399">ASP.NET server code lets you perform tasks based on conditions and write code that repeats statements a specific number of times (that is, code that runs a loop).</span></span>

### <a name="testing-conditions"></a><span data-ttu-id="faae6-400">测试条件</span><span class="sxs-lookup"><span data-stu-id="faae6-400">Testing Conditions</span></span>

<span data-ttu-id="faae6-401">若要测试使用一个简单条件`if`语句，返回 true 或 false 基于你指定的测试：</span><span class="sxs-lookup"><span data-stu-id="faae6-401">To test a simple condition you use the `if` statement, which returns true or false based on a test you specify:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample49.cshtml)]

<span data-ttu-id="faae6-402">`if`关键字开始块。</span><span class="sxs-lookup"><span data-stu-id="faae6-402">The `if` keyword starts a block.</span></span> <span data-ttu-id="faae6-403">实际的测试 （条件） 位于括号中，并返回 true 或 false。</span><span class="sxs-lookup"><span data-stu-id="faae6-403">The actual test (condition) is in parentheses and returns true or false.</span></span> <span data-ttu-id="faae6-404">运行测试为 true 的语句括在大括号中。</span><span class="sxs-lookup"><span data-stu-id="faae6-404">The statements that run if the test is true are enclosed in braces.</span></span> <span data-ttu-id="faae6-405">`if`语句中可以包含`else`指定如果条件为 false，则运行语句块：</span><span class="sxs-lookup"><span data-stu-id="faae6-405">An `if` statement can include an `else` block that specifies statements to run if the condition is false:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample50.cshtml)]

<span data-ttu-id="faae6-406">您可以添加多个条件使用`else if`块：</span><span class="sxs-lookup"><span data-stu-id="faae6-406">You can add multiple conditions using an `else if` block:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample51.cshtml)]

<span data-ttu-id="faae6-407">在此示例中，如果第一个条件中 if 块不为 true，`else if`条件进行检查。</span><span class="sxs-lookup"><span data-stu-id="faae6-407">In this example, if the first condition in the if block is not true, the `else if` condition is checked.</span></span> <span data-ttu-id="faae6-408">如果满足该条件，则在语句`else if`块执行。</span><span class="sxs-lookup"><span data-stu-id="faae6-408">If that condition is met, the statements in the `else if` block are executed.</span></span> <span data-ttu-id="faae6-409">如果没有条件为真中的语句`else`块执行。</span><span class="sxs-lookup"><span data-stu-id="faae6-409">If none of the conditions are met, the statements in the `else` block are executed.</span></span> <span data-ttu-id="faae6-410">可以添加任意数量的 else if 的阻止，并使用然后关闭`else`作为阻止&quot;其他所有内容&quot;条件。</span><span class="sxs-lookup"><span data-stu-id="faae6-410">You can add any number of else if blocks, and then close with an `else` block as the &quot;everything else&quot; condition.</span></span>

<span data-ttu-id="faae6-411">若要测试大量的条件，请使用`switch`块：</span><span class="sxs-lookup"><span data-stu-id="faae6-411">To test a large number of conditions, use a `switch` block:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample52.cshtml)]

<span data-ttu-id="faae6-412">要测试的值位于括号中 (在示例中，`weekday`变量)。</span><span class="sxs-lookup"><span data-stu-id="faae6-412">The value to test is in parentheses (in the example, the `weekday` variable).</span></span> <span data-ttu-id="faae6-413">每个单独测试使用`case`语句以冒号 （:） 结尾。</span><span class="sxs-lookup"><span data-stu-id="faae6-413">Each individual test uses a `case` statement that ends with a colon (:).</span></span> <span data-ttu-id="faae6-414">如果的值`case`语句进行匹配的测试值时，该事例块中的代码执行。</span><span class="sxs-lookup"><span data-stu-id="faae6-414">If the value of a `case` statement matches the test value, the code in that case block is executed.</span></span> <span data-ttu-id="faae6-415">关闭与每个 case 语句`break`语句。</span><span class="sxs-lookup"><span data-stu-id="faae6-415">You close each case statement with a `break` statement.</span></span> <span data-ttu-id="faae6-416">(如果你忘记了在每个包括中断`case`阻止，请从下一个代码`case`语句还将运行。)一个`switch`块通常具有`default`语句的最后一种情况作为&quot;其他所有内容&quot;如果不满足的其他情况下运行的选项。</span><span class="sxs-lookup"><span data-stu-id="faae6-416">(If you forget to include break in each `case` block, the code from the next `case` statement will run also.) A `switch` block often has a `default` statement as the last case for an &quot;everything else&quot; option that runs if none of the other cases are true.</span></span>

<span data-ttu-id="faae6-417">在浏览器中显示的最后两个条件块的结果：</span><span class="sxs-lookup"><span data-stu-id="faae6-417">The result of the last two conditional blocks displayed in a browser:</span></span>

![Razor-Img10](introducing-razor-syntax-c/_static/image10.jpg)

### <a name="looping-code"></a><span data-ttu-id="faae6-419">循环的代码</span><span class="sxs-lookup"><span data-stu-id="faae6-419">Looping Code</span></span>

<span data-ttu-id="faae6-420">通常需要反复运行相同的语句。</span><span class="sxs-lookup"><span data-stu-id="faae6-420">You often need to run the same statements repeatedly.</span></span> <span data-ttu-id="faae6-421">通过循环执行此操作。</span><span class="sxs-lookup"><span data-stu-id="faae6-421">You do this by looping.</span></span> <span data-ttu-id="faae6-422">例如，您通常运行同一个语句为每个项集合中的数据。</span><span class="sxs-lookup"><span data-stu-id="faae6-422">For example, you often run the same statements for each item in a collection of data.</span></span> <span data-ttu-id="faae6-423">如果你确切地知道多少次循环，则可以使用`for`循环。</span><span class="sxs-lookup"><span data-stu-id="faae6-423">If you know exactly how many times you want to loop, you can use a `for` loop.</span></span> <span data-ttu-id="faae6-424">此种类型的循环非常适合计算或向下计数：</span><span class="sxs-lookup"><span data-stu-id="faae6-424">This kind of loop is especially useful for counting up or counting down:</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample53.html)]

<span data-ttu-id="faae6-425">循环开头`for`关键字后, 跟三个语句在括号内，每个以分号结尾。</span><span class="sxs-lookup"><span data-stu-id="faae6-425">The loop begins with the `for` keyword, followed by three statements in parentheses, each terminated with a semicolon.</span></span>

- <span data-ttu-id="faae6-426">在括号内的第一个语句 (`var i=10;`) 创建一个计数器并将初始化为 10。</span><span class="sxs-lookup"><span data-stu-id="faae6-426">Inside the parentheses, the first statement (`var i=10;`) creates a counter and initializes it to 10.</span></span> <span data-ttu-id="faae6-427">无需命名计数器`i`&#8212;可以使用任何变量。</span><span class="sxs-lookup"><span data-stu-id="faae6-427">You don't have to name the counter `i` &#8212; you can use any variable.</span></span> <span data-ttu-id="faae6-428">当`for`循环运行时，会自动增加计数器的数值。</span><span class="sxs-lookup"><span data-stu-id="faae6-428">When the `for` loop runs, the counter is automatically incremented.</span></span>
- <span data-ttu-id="faae6-429">第二个语句 (`i < 21;`) 设置距离您要计数的条件。</span><span class="sxs-lookup"><span data-stu-id="faae6-429">The second statement (`i < 21;`) sets the condition for how far you want to count.</span></span> <span data-ttu-id="faae6-430">在这种情况下，想要转到最多 20 个 （即，继续时该计数器是小于 21）。</span><span class="sxs-lookup"><span data-stu-id="faae6-430">In this case, you want it to go to a maximum of 20 (that is, keep going while the counter is less than 21).</span></span>
- <span data-ttu-id="faae6-431">第三个语句 (`i++` ) 使用递增运算符，只需指定计数器应具有 1 添加到其每次循环运行的时。</span><span class="sxs-lookup"><span data-stu-id="faae6-431">The third statement (`i++` ) uses an increment operator, which simply specifies that the counter should have 1 added to it each time the loop runs.</span></span>

<span data-ttu-id="faae6-432">大括号内是循环的每次迭代就会运行的代码。</span><span class="sxs-lookup"><span data-stu-id="faae6-432">Inside the braces is the code that will run for each iteration of the loop.</span></span> <span data-ttu-id="faae6-433">标记将创建一个新段落 (`<p>`元素) 每个时间，并将行添加到输出，显示的值`i`（计数器）。</span><span class="sxs-lookup"><span data-stu-id="faae6-433">The markup creates a new paragraph (`<p>` element) each time and adds a line to the output, displaying the value of `i` (the counter).</span></span> <span data-ttu-id="faae6-434">在运行此页时，该示例将创建显示每个行，该值指示项编号中的文本的输出的 11 行。</span><span class="sxs-lookup"><span data-stu-id="faae6-434">When you run this page, the example creates 11 lines displaying the output, with the text in each line indicating the item number.</span></span>

![Razor-Img11](introducing-razor-syntax-c/_static/image11.jpg)

<span data-ttu-id="faae6-436">如果您正在使用集合或数组，通常使用`foreach`循环。</span><span class="sxs-lookup"><span data-stu-id="faae6-436">If you're working with a collection or array, you often use a `foreach` loop.</span></span> <span data-ttu-id="faae6-437">集合是一组类似对象和`foreach`循环可让你执行在集合中每一项任务。</span><span class="sxs-lookup"><span data-stu-id="faae6-437">A collection is a group of similar objects, and the `foreach` loop lets you carry out a task on each item in the collection.</span></span> <span data-ttu-id="faae6-438">此类型的循环非常方便的集合，因为与不同`for`循环中，您无需使计数器递增或设置的限制。</span><span class="sxs-lookup"><span data-stu-id="faae6-438">This type of loop is convenient for collections, because unlike a `for` loop, you don't have to increment the counter or set a limit.</span></span> <span data-ttu-id="faae6-439">相反，`foreach`循环代码只需继续遍历该集合直到完成。</span><span class="sxs-lookup"><span data-stu-id="faae6-439">Instead, the `foreach` loop code simply proceeds through the collection until it's finished.</span></span>

<span data-ttu-id="faae6-440">例如，以下代码将返回中的项`Request.ServerVariables`集合，这是一个对象，包含有关你的 web 服务器的信息。</span><span class="sxs-lookup"><span data-stu-id="faae6-440">For example, the following code returns the items in the `Request.ServerVariables` collection, which is an object that contains information about your web server.</span></span> <span data-ttu-id="faae6-441">它使用`foreac`h 循环，以显示每个项的名称，通过创建一个新`<li>`HTML 项目符号列表中的元素。</span><span class="sxs-lookup"><span data-stu-id="faae6-441">It uses a `foreac` h loop to display the name of each item by creating a new `<li>` element in an HTML bulleted list.</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample54.html)]

<span data-ttu-id="faae6-442">`foreach`关键字后跟括号，声明表示集合中的单个项的变量 (在示例中， `var item`) 后, 跟`in`关键字后, 跟想要循环访问的集合。</span><span class="sxs-lookup"><span data-stu-id="faae6-442">The `foreach` keyword is followed by parentheses where you declare a variable that represents a single item in the collection (in the example, `var item`), followed by the `in` keyword, followed by the collection you want to loop through.</span></span> <span data-ttu-id="faae6-443">正文中`foreach`循环中，您可以访问使用你之前声明的变量的当前项。</span><span class="sxs-lookup"><span data-stu-id="faae6-443">In the body of the `foreach` loop, you can access the current item using the variable that you declared earlier.</span></span>

![Razor-Img12](introducing-razor-syntax-c/_static/image12.jpg)

<span data-ttu-id="faae6-445">若要创建一个更通用的循环，请使用`while`语句：</span><span class="sxs-lookup"><span data-stu-id="faae6-445">To create a more general-purpose loop, use the `while` statement:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample55.cshtml)]

<span data-ttu-id="faae6-446">一个`while`循环开头`while`关键字后, 跟括号指定循环继续的时间长度 (这里，为只要`countNum`小于 50)，然后要重复的块。</span><span class="sxs-lookup"><span data-stu-id="faae6-446">A `while` loop begins with the `while` keyword, followed by parentheses where you specify how long the loop continues (here, for as long as `countNum` is less than 50), then the block to repeat.</span></span> <span data-ttu-id="faae6-447">循环通常递增 （将添加到） 或递减 （从减） 的变量或用于计数的对象。</span><span class="sxs-lookup"><span data-stu-id="faae6-447">Loops typically increment (add to) or decrement (subtract from) a variable or object used for counting.</span></span> <span data-ttu-id="faae6-448">在示例中，`+=`运算符将添加到 1`countNum`每次循环运行的时。</span><span class="sxs-lookup"><span data-stu-id="faae6-448">In the example, the `+=` operator adds 1 to `countNum` each time the loop runs.</span></span> <span data-ttu-id="faae6-449">(若要递减的向下计数的循环中的变量，将使用递减运算符`-=`)。</span><span class="sxs-lookup"><span data-stu-id="faae6-449">(To decrement a variable in a loop that counts down, you would use the decrement operator `-=`).</span></span>

## <a name="objects-and-collections"></a><span data-ttu-id="faae6-450">对象和集合</span><span class="sxs-lookup"><span data-stu-id="faae6-450">Objects and Collections</span></span>

<span data-ttu-id="faae6-451">在 ASP.NET 网站中几乎所有内容是一个对象，包括在 web 页面。</span><span class="sxs-lookup"><span data-stu-id="faae6-451">Nearly everything in an ASP.NET website is an object, including the web page itself.</span></span> <span data-ttu-id="faae6-452">本部分介绍一些重要的对象，您将使用频繁地在代码中。</span><span class="sxs-lookup"><span data-stu-id="faae6-452">This section discusses some important objects you'll work with frequently in your code.</span></span>

### <a name="page-objects"></a><span data-ttu-id="faae6-453">页对象</span><span class="sxs-lookup"><span data-stu-id="faae6-453">Page Objects</span></span>

<span data-ttu-id="faae6-454">在 ASP.NET 中的最基本对象是页。</span><span class="sxs-lookup"><span data-stu-id="faae6-454">The most basic object in ASP.NET is the page.</span></span> <span data-ttu-id="faae6-455">可以访问的不符合要求的任何对象而直接的 page 对象的属性。</span><span class="sxs-lookup"><span data-stu-id="faae6-455">You can access properties of the page object directly without any qualifying object.</span></span> <span data-ttu-id="faae6-456">以下代码获取页的文件路径，使用`Request`页的对象：</span><span class="sxs-lookup"><span data-stu-id="faae6-456">The following code gets the page's file path, using the `Request` object of the page:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample56.cshtml)]

<span data-ttu-id="faae6-457">若要使其明确的引用的当前的页对象上属性和方法，你可以选择使用关键字`this`来表示在代码中的页对象。</span><span class="sxs-lookup"><span data-stu-id="faae6-457">To make it clear that you're referencing properties and methods on the current page object, you can optionally use the keyword `this` to represent the page object in your code.</span></span> <span data-ttu-id="faae6-458">下面是前面的代码示例中，使用`this`添加来表示页面：</span><span class="sxs-lookup"><span data-stu-id="faae6-458">Here is the previous code example, with `this` added to represent the page:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample57.cshtml)]

<span data-ttu-id="faae6-459">可以使用的属性`Page`对象以获得大量的信息，例如：</span><span class="sxs-lookup"><span data-stu-id="faae6-459">You can use properties of the `Page` object to get a lot of information, such as:</span></span>

- <span data-ttu-id="faae6-460">`Request`。</span><span class="sxs-lookup"><span data-stu-id="faae6-460">`Request`.</span></span> <span data-ttu-id="faae6-461">如您所见，这是信息的一系列有关当前请求，包括哪种类型的浏览器发出了请求、 页面、 用户标识，等等的 URL。</span><span class="sxs-lookup"><span data-stu-id="faae6-461">As you've already seen, this is a collection of information about the current request, including what type of browser made the request, the URL of the page, the user identity, etc.</span></span>
- <span data-ttu-id="faae6-462">`Response`。</span><span class="sxs-lookup"><span data-stu-id="faae6-462">`Response`.</span></span> <span data-ttu-id="faae6-463">这是信息的有关在服务器代码完成运行时将发送到浏览器的响应 （页） 集合。</span><span class="sxs-lookup"><span data-stu-id="faae6-463">This is a collection of information about the response (page) that will be sent to the browser when the server code has finished running.</span></span> <span data-ttu-id="faae6-464">例如，此属性可用于将信息写入到响应。</span><span class="sxs-lookup"><span data-stu-id="faae6-464">For example, you can use this property to write information into the response.</span></span> 

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample58.cshtml)]

<a id="ID_CollectionsAndObjects"></a>
### <a name="collection-objects-arrays-and-dictionaries"></a><span data-ttu-id="faae6-465">集合对象 （数组和字典）</span><span class="sxs-lookup"><span data-stu-id="faae6-465">Collection Objects (Arrays and Dictionaries)</span></span>

<span data-ttu-id="faae6-466">一个*集合*是一组相同的类型，如集合的对象的`Customer`数据库中的对象。</span><span class="sxs-lookup"><span data-stu-id="faae6-466">A *collection* is a group of objects of the same type, such as a collection of `Customer` objects from a database.</span></span> <span data-ttu-id="faae6-467">ASP.NET 包含多个内置集合，例如`Request.Files`集合。</span><span class="sxs-lookup"><span data-stu-id="faae6-467">ASP.NET contains many built-in collections, like the `Request.Files` collection.</span></span>

<span data-ttu-id="faae6-468">通常将使用集合中的数据。</span><span class="sxs-lookup"><span data-stu-id="faae6-468">You'll often work with data in collections.</span></span> <span data-ttu-id="faae6-469">两个常见集合类型是*数组*并*字典*。</span><span class="sxs-lookup"><span data-stu-id="faae6-469">Two common collection types are the *array* and the *dictionary*.</span></span> <span data-ttu-id="faae6-470">如果你想要存储类似项的集合，但不想创建一个单独的变量来保存每个项，数组非常有用：</span><span class="sxs-lookup"><span data-stu-id="faae6-470">An array is useful when you want to store a collection of similar items but don't want to create a separate variable to hold each item:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample59.cshtml)]

<span data-ttu-id="faae6-471">对于数组，声明特定数据类型，如`string`， `int`，或`DateTime`。</span><span class="sxs-lookup"><span data-stu-id="faae6-471">With arrays, you declare a specific data type, such as `string`, `int`, or `DateTime`.</span></span> <span data-ttu-id="faae6-472">若要指示该变量可以包含的数组，向声明添加方括号 (如`string[]`或`int[]`)。</span><span class="sxs-lookup"><span data-stu-id="faae6-472">To indicate that the variable can contain an array, you add brackets to the declaration (such as `string[]` or `int[]`).</span></span> <span data-ttu-id="faae6-473">您可以访问项在数组中使用它们的位置 （索引） 或通过使用`foreach`语句。</span><span class="sxs-lookup"><span data-stu-id="faae6-473">You can access items in an array using their position (index) or by using the `foreach` statement.</span></span> <span data-ttu-id="faae6-474">从零开始的数组索引为&#8212;，它是第一项是在位置 0，第二项是在位置 1，依此类推。</span><span class="sxs-lookup"><span data-stu-id="faae6-474">Array indexes are zero-based &#8212; that is, the first item is at position 0, the second item is at position 1, and so on.</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample60.cshtml)]

<span data-ttu-id="faae6-475">可以通过获取确定数组中的项的数目及其`Length`属性。</span><span class="sxs-lookup"><span data-stu-id="faae6-475">You can determine the number of items in an array by getting its `Length` property.</span></span> <span data-ttu-id="faae6-476">若要获取特定项的数组 （若要搜索数组） 中的位置，请使用`Array.IndexOf`方法。</span><span class="sxs-lookup"><span data-stu-id="faae6-476">To get the position of a specific item in the array (to search the array), use the `Array.IndexOf` method.</span></span> <span data-ttu-id="faae6-477">此外可以执行诸如反向数组的内容 (`Array.Reverse`方法) 或对内容进行排序 (`Array.Sort`方法)。</span><span class="sxs-lookup"><span data-stu-id="faae6-477">You can also do things like reverse the contents of an array (the `Array.Reverse` method) or sort the contents (the `Array.Sort` method).</span></span>

<span data-ttu-id="faae6-478">在浏览器中显示的字符串数组代码的输出：</span><span class="sxs-lookup"><span data-stu-id="faae6-478">The output of the string array code displayed in a browser:</span></span>

![Razor-Img13](introducing-razor-syntax-c/_static/image13.jpg)

<span data-ttu-id="faae6-480">字典是键/值对的集合，其中提供密钥 （或名称） 设置或检索相应的值：</span><span class="sxs-lookup"><span data-stu-id="faae6-480">A dictionary is a collection of key/value pairs, where you provide the key (or name) to set or retrieve the corresponding value:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample61.cshtml)]

<span data-ttu-id="faae6-481">若要创建一个字典，请使用`new`关键字来指示您要创建新的字典对象。</span><span class="sxs-lookup"><span data-stu-id="faae6-481">To create a dictionary, you use the `new` keyword to indicate that you're creating a new dictionary object.</span></span> <span data-ttu-id="faae6-482">可以将字典分配给变量使用`var`关键字。</span><span class="sxs-lookup"><span data-stu-id="faae6-482">You can assign a dictionary to a variable using the `var` keyword.</span></span> <span data-ttu-id="faae6-483">指示使用尖括号字典中的项的数据类型 ( `< >` )。</span><span class="sxs-lookup"><span data-stu-id="faae6-483">You indicate the data types of the items in the dictionary using angle brackets ( `< >` ).</span></span> <span data-ttu-id="faae6-484">在声明的末尾，必须添加一对圆括号，因为这是实际创建一个新的字典的方法。</span><span class="sxs-lookup"><span data-stu-id="faae6-484">At the end of the declaration, you must add a pair of parentheses, because this is actually a method that creates a new dictionary.</span></span>

<span data-ttu-id="faae6-485">若要将项添加到字典中，可以调用`Add`字典变量或方法 (`myScores`这种情况下)，然后指定一个键和值。</span><span class="sxs-lookup"><span data-stu-id="faae6-485">To add items to the dictionary, you can call the `Add` method of the dictionary variable (`myScores` in this case), and then specify a key and a value.</span></span> <span data-ttu-id="faae6-486">或者，可以使用方括号以指示该密钥，并执行简单的赋值，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="faae6-486">Alternatively, you can use square brackets to indicate the key and do a simple assignment, as in the following example:</span></span>

[!code-csharp[Main](introducing-razor-syntax-c/samples/sample62.cs)]

<span data-ttu-id="faae6-487">若要从字典中获取一个值，请在方括号中指定密钥：</span><span class="sxs-lookup"><span data-stu-id="faae6-487">To get a value from the dictionary, you specify the key in brackets:</span></span>

[!code-csharp[Main](introducing-razor-syntax-c/samples/sample63.cs)]

## <a name="calling-methods-with-parameters"></a><span data-ttu-id="faae6-488">调用带参数的方法</span><span class="sxs-lookup"><span data-stu-id="faae6-488">Calling Methods with Parameters</span></span>

<span data-ttu-id="faae6-489">在阅读本文前面部分中，带有程序的对象可以具有方法。</span><span class="sxs-lookup"><span data-stu-id="faae6-489">As you read earlier in this article, the objects that you program with can have methods.</span></span> <span data-ttu-id="faae6-490">例如，`Database`对象可能具有`Database.Connect`方法。</span><span class="sxs-lookup"><span data-stu-id="faae6-490">For example, a `Database` object might have a `Database.Connect` method.</span></span> <span data-ttu-id="faae6-491">许多方法还具有一个或多个参数。</span><span class="sxs-lookup"><span data-stu-id="faae6-491">Many methods also have one or more parameters.</span></span> <span data-ttu-id="faae6-492">一个*参数*是向方法传递一个值以使该方法以完成其任务。</span><span class="sxs-lookup"><span data-stu-id="faae6-492">A *parameter* is a value that you pass to a method to enable the method to complete its task.</span></span> <span data-ttu-id="faae6-493">例如，查看有关声明`Request.MapPath`方法，它使用三个参数：</span><span class="sxs-lookup"><span data-stu-id="faae6-493">For example, look at a declaration for the `Request.MapPath` method, which takes three parameters:</span></span>

[!code-csharp[Main](introducing-razor-syntax-c/samples/sample64.cs)]

<span data-ttu-id="faae6-494">（已换行以使其更具可读性。</span><span class="sxs-lookup"><span data-stu-id="faae6-494">(The line has been wrapped to make it more readable.</span></span> <span data-ttu-id="faae6-495">请记住，可以将分行符几乎任何位置除了内部字符串用引号括起来。)</span><span class="sxs-lookup"><span data-stu-id="faae6-495">Remember that you can put line breaks almost any place except inside strings that are enclosed in quotation marks.)</span></span>

<span data-ttu-id="faae6-496">此方法相对应的服务器上的物理路径返回到指定的虚拟路径。</span><span class="sxs-lookup"><span data-stu-id="faae6-496">This method returns the physical path on the server that corresponds to a specified virtual path.</span></span> <span data-ttu-id="faae6-497">该方法的三个参数是`virtualPath`， `baseVirtualDir`，和`allowCrossAppMapping`。</span><span class="sxs-lookup"><span data-stu-id="faae6-497">The three parameters for the method are `virtualPath`, `baseVirtualDir`, and `allowCrossAppMapping`.</span></span> <span data-ttu-id="faae6-498">（请注意，在声明中，所列的参数将接受的数据的数据类型）。当调用此方法时，必须提供所有三个参数的值。</span><span class="sxs-lookup"><span data-stu-id="faae6-498">(Notice that in the declaration, the parameters are listed with the data types of the data that they'll accept.) When you call this method, you must supply values for all three parameters.</span></span>

<span data-ttu-id="faae6-499">Razor 语法可以用于将参数传递给方法的两个选项：*位置参数*并*命名参数*。</span><span class="sxs-lookup"><span data-stu-id="faae6-499">The Razor syntax gives you two options for passing parameters to a method: *positional parameters* and *named parameters*.</span></span> <span data-ttu-id="faae6-500">若要调用使用位置参数的方法，请按严格顺序方法声明中指定的传递参数。</span><span class="sxs-lookup"><span data-stu-id="faae6-500">To call a method using positional parameters, you pass the parameters in a strict order that's specified in the method declaration.</span></span> <span data-ttu-id="faae6-501">（您通常知道此顺序通过阅读文档的方法。）必须遵循的顺序，并且你不能跳过的任何参数&#8212;如果有必要，请传递了空字符串 (`""`) 或`null`不具有的值为位置参数。</span><span class="sxs-lookup"><span data-stu-id="faae6-501">(You would typically know this order by reading documentation for the method.) You must follow the order, and you can't skip any of the parameters &#8212; if necessary, you pass an empty string (`""`) or `null` for a positional parameter that you don't have a value for.</span></span>

<span data-ttu-id="faae6-502">下面的示例假定你有一个名为的文件夹*脚本*上你的网站。</span><span class="sxs-lookup"><span data-stu-id="faae6-502">The following example assumes you have a folder named *scripts* on your website.</span></span> <span data-ttu-id="faae6-503">该代码调用`Request.MapPath`方法，并传递正确的顺序中的三个参数的值。</span><span class="sxs-lookup"><span data-stu-id="faae6-503">The code calls the `Request.MapPath` method and passes values for the three parameters in the correct order.</span></span> <span data-ttu-id="faae6-504">然后，它显示生成映射的路径。</span><span class="sxs-lookup"><span data-stu-id="faae6-504">It then displays the resulting mapped path.</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample65.cshtml)]

<span data-ttu-id="faae6-505">当某个方法具有多个参数时，您可以保留你的代码更具可读性使用命名参数。</span><span class="sxs-lookup"><span data-stu-id="faae6-505">When a method has many parameters, you can keep your code more readable by using named parameters.</span></span> <span data-ttu-id="faae6-506">若要调用的方法使用命名的参数，您指定的参数名称后跟一个冒号 （:），然后选择值。</span><span class="sxs-lookup"><span data-stu-id="faae6-506">To call a method using named parameters, you specify the parameter name followed by a colon (:), and then the value.</span></span> <span data-ttu-id="faae6-507">命名参数的优点是，可以将它们传递所需的任何顺序。</span><span class="sxs-lookup"><span data-stu-id="faae6-507">The advantage of named parameters is that you can pass them in any order you want.</span></span> <span data-ttu-id="faae6-508">（一个缺点是方法调用不是精简。）</span><span class="sxs-lookup"><span data-stu-id="faae6-508">(A disadvantage is that the method call is not as compact.)</span></span>

<span data-ttu-id="faae6-509">下面的示例调用按上面所述的相同方法，但使用命名参数提供的值：</span><span class="sxs-lookup"><span data-stu-id="faae6-509">The following example calls the same method as above, but uses named parameters to supply the values:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample66.cshtml)]

<span data-ttu-id="faae6-510">正如您所看到的会以不同的顺序传递参数。</span><span class="sxs-lookup"><span data-stu-id="faae6-510">As you can see, the parameters are passed in a different order.</span></span> <span data-ttu-id="faae6-511">但是，如果在运行上面的例子和此示例中，它们将返回相同的值。</span><span class="sxs-lookup"><span data-stu-id="faae6-511">However, if you run the previous example and this example, they'll return the same value.</span></span>

<a id="ID_HandlingErrors"></a>
## <a name="handling-errors"></a><span data-ttu-id="faae6-512">处理错误</span><span class="sxs-lookup"><span data-stu-id="faae6-512">Handling Errors</span></span>

### <a name="try-catch-statements"></a><span data-ttu-id="faae6-513">Try Catch 语句</span><span class="sxs-lookup"><span data-stu-id="faae6-513">Try-Catch Statements</span></span>

<span data-ttu-id="faae6-514">通常必须在代码中可能会失败的原因有您的控制范围内的语句。</span><span class="sxs-lookup"><span data-stu-id="faae6-514">You'll often have statements in your code that might fail for reasons outside your control.</span></span> <span data-ttu-id="faae6-515">例如：</span><span class="sxs-lookup"><span data-stu-id="faae6-515">For example:</span></span>

- <span data-ttu-id="faae6-516">如果你的代码尝试创建或访问的文件时，可能会出现各种类型的错误。</span><span class="sxs-lookup"><span data-stu-id="faae6-516">If your code tries to create or access a file, all sorts of errors might occur.</span></span> <span data-ttu-id="faae6-517">所需的文件可能不存在，则可能锁定，代码可能不具有的权限，等等。</span><span class="sxs-lookup"><span data-stu-id="faae6-517">The file you want might not exist, it might be locked, the code might not have permissions, and so on.</span></span>
- <span data-ttu-id="faae6-518">同样，如果你的代码尝试更新数据库中的记录，可能出现权限问题、 与数据库的连接可能会断开，要保存的数据可能无效，依此类推。</span><span class="sxs-lookup"><span data-stu-id="faae6-518">Similarly, if your code tries to update records in a database, there can be permissions issues, the connection to the database might be dropped, the data to save might be invalid, and so on.</span></span>

<span data-ttu-id="faae6-519">在编程术语中，这些应用场景被称为*异常*。</span><span class="sxs-lookup"><span data-stu-id="faae6-519">In programming terms, these situations are called *exceptions*.</span></span> <span data-ttu-id="faae6-520">如果你的代码遇到的异常，它将生成 （的引发操作） 的错误消息的在最令人讨厌的用户：</span><span class="sxs-lookup"><span data-stu-id="faae6-520">If your code encounters an exception, it generates (throws) an error message that's, at best, annoying to users:</span></span>

![Razor-Img14](introducing-razor-syntax-c/_static/image14.jpg)

<span data-ttu-id="faae6-522">在其中您的代码可能会发生异常的情况下，为了避免这种类型的错误消息，可以使用`try/catch`语句。</span><span class="sxs-lookup"><span data-stu-id="faae6-522">In situations where your code might encounter exceptions, and in order to avoid error messages of this type, you can use `try/catch` statements.</span></span> <span data-ttu-id="faae6-523">在`try`语句中，您运行要检查的代码。</span><span class="sxs-lookup"><span data-stu-id="faae6-523">In the `try` statement, you run the code that you're checking.</span></span> <span data-ttu-id="faae6-524">一个或多个`catch`语句，则可以寻找特定于可能发生的错误 （特定类型的异常）。</span><span class="sxs-lookup"><span data-stu-id="faae6-524">In one or more `catch` statements, you can look for specific errors (specific types of exceptions) that might have occurred.</span></span> <span data-ttu-id="faae6-525">可以包括任意多个`catch`语句作为您需要查找你预期会发生的错误。</span><span class="sxs-lookup"><span data-stu-id="faae6-525">You can include as many `catch` statements as you need to look for errors that you are anticipating.</span></span>

> [!NOTE]
> <span data-ttu-id="faae6-526">我们建议您不要使用`Response.Redirect`中的方法`try/catch`语句，因为它可以在页面中导致异常。</span><span class="sxs-lookup"><span data-stu-id="faae6-526">We recommend that you avoid using the `Response.Redirect` method in `try/catch` statements, because it can cause an exception in your page.</span></span>


<span data-ttu-id="faae6-527">下面的示例显示了创建第一个请求上的文本文件，然后显示一个按钮，使用户可以打开文件的页面。</span><span class="sxs-lookup"><span data-stu-id="faae6-527">The following example shows a page that creates a text file on the first request and then displays a button that lets the user open the file.</span></span> <span data-ttu-id="faae6-528">该示例故意使用错误的文件名称，以便它将导致异常。</span><span class="sxs-lookup"><span data-stu-id="faae6-528">The example deliberately uses a bad file name so that it will cause an exception.</span></span> <span data-ttu-id="faae6-529">该代码包括`catch`两个可能的异常的语句： `FileNotFoundException`，就会出现此错误，文件名称是否和`DirectoryNotFoundException`，如果 ASP.NET 甚至找不到该文件夹将出现此情况。</span><span class="sxs-lookup"><span data-stu-id="faae6-529">The code includes `catch` statements for two possible exceptions: `FileNotFoundException`, which occurs if the file name is bad, and `DirectoryNotFoundException`, which occurs if ASP.NET can't even find the folder.</span></span> <span data-ttu-id="faae6-530">（您可以取消注释该示例中的语句才能看到它时一切运行正常的运行。）</span><span class="sxs-lookup"><span data-stu-id="faae6-530">(You can uncomment a statement in the example in order to see how it runs when everything works properly.)</span></span>

<span data-ttu-id="faae6-531">如果你的代码未处理异常，会看到一个错误页面，如前面的屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="faae6-531">If your code didn't handle the exception, you would see an error page like the previous screen shot.</span></span> <span data-ttu-id="faae6-532">但是，`try/catch`部分可帮助防止用户看到这些类型的错误。</span><span class="sxs-lookup"><span data-stu-id="faae6-532">However, the `try/catch` section helps prevent the user from seeing these types of errors.</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample67.cshtml)]

## <a name="additional-resources"></a><span data-ttu-id="faae6-533">其他资源</span><span class="sxs-lookup"><span data-stu-id="faae6-533">Additional Resources</span></span>

<span data-ttu-id="faae6-534">**使用 Visual Basic 进行编程**</span><span class="sxs-lookup"><span data-stu-id="faae6-534">**Programming with Visual Basic**</span></span>


[<span data-ttu-id="faae6-535">附录：Visual Basic 语言和语法</span><span class="sxs-lookup"><span data-stu-id="faae6-535">Appendix: Visual Basic Language and Syntax</span></span>](https://go.microsoft.com/fwlink/?LinkId=202908)


<span data-ttu-id="faae6-536">**参考文档**</span><span class="sxs-lookup"><span data-stu-id="faae6-536">**Reference Documentation**</span></span>


[<span data-ttu-id="faae6-537">ASP.NET 2.0</span><span class="sxs-lookup"><span data-stu-id="faae6-537">ASP.NET</span></span>](https://msdn.microsoft.com/library/ee532866.aspx)

[<span data-ttu-id="faae6-538">C# 语言</span><span class="sxs-lookup"><span data-stu-id="faae6-538">C# Language</span></span>](https://msdn.microsoft.com/library/kx37x362.aspx)

---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/form-basics
title: 介绍ASP.NET网页 - HTML表单基础知识 |微软文档
author: Rick-Anderson
description: 本教程介绍如何创建输入表单以及使用ASP.NET网页 （Razor） 时如何处理用户输入的基础知识。 现在你...
ms.author: riande
ms.date: 05/28/2015
ms.assetid: 81ed82bf-b940-44f1-b94a-555d0cb7cc98
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/form-basics
msc.type: authoredcontent
ms.openlocfilehash: f57661077ec3bb13f3d4ec41b130bda4d2fb9070
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675921"
---
# <a name="introducing-aspnet-web-pages---html-form-basics"></a><span data-ttu-id="2b5ad-104">介绍ASP.NET网页 - HTML表单基础知识</span><span class="sxs-lookup"><span data-stu-id="2b5ad-104">Introducing ASP.NET Web Pages - HTML Form Basics</span></span>

<span data-ttu-id="2b5ad-105"> 作者 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="2b5ad-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="2b5ad-106">本教程介绍如何创建输入表单以及使用ASP.NET网页 （Razor） 时如何处理用户输入的基础知识。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-106">This tutorial shows you the basics of how to create an input form and how to handle the user's input when you use ASP.NET Web Pages (Razor).</span></span> <span data-ttu-id="2b5ad-107">现在您已经有了一个数据库，您将使用表单技能让用户在数据库中查找特定影片。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-107">And now that you've got a database, you'll use your form skills to let users find specific movies in the database.</span></span> <span data-ttu-id="2b5ad-108">它假定您已经通过[介绍使用ASP.NET网页显示数据](/aspnet/web-pages/overview/getting-started/introducing-aspnet-web-pages-2/displaying-data)完成了该系列。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-108">It assumes you have completed the series through [Introduction to Displaying Data Using ASP.NET Web Pages](/aspnet/web-pages/overview/getting-started/introducing-aspnet-web-pages-2/displaying-data).</span></span>
> 
> <span data-ttu-id="2b5ad-109">学习内容：</span><span class="sxs-lookup"><span data-stu-id="2b5ad-109">What you'll learn:</span></span>
> 
> - <span data-ttu-id="2b5ad-110">如何使用标准 HTML 元素创建窗体。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-110">How to create a form by using standard HTML elements.</span></span>
> - <span data-ttu-id="2b5ad-111">如何读取表单中的用户输入。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-111">How to read the user's input in a form.</span></span>
> - <span data-ttu-id="2b5ad-112">如何创建 SQL 查询，该查询通过使用用户提供的搜索词选择性地获取数据。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-112">How to create a SQL query that selectively gets data by using a search term that the user supplies.</span></span>
> - <span data-ttu-id="2b5ad-113">如何在页面中"记住"用户输入的内容。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-113">How to have fields in the page "remember" what the user entered.</span></span>
>   
> 
> <span data-ttu-id="2b5ad-114">讨论的功能/技术：</span><span class="sxs-lookup"><span data-stu-id="2b5ad-114">Features/technologies discussed:</span></span>
> 
> - <span data-ttu-id="2b5ad-115">`Request` 对象。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-115">The `Request` object.</span></span>
> - <span data-ttu-id="2b5ad-116">SQL`Where`子句。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-116">The SQL `Where` clause.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="2b5ad-117">所需操作</span><span class="sxs-lookup"><span data-stu-id="2b5ad-117">What You'll Build</span></span>

<span data-ttu-id="2b5ad-118">在前面的教程中，您创建了一个数据库，向它添加了数据，然后使用`WebGrid`帮助器来显示数据。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-118">In the previous tutorial, you created a database, added data to it, and then used the `WebGrid` helper to display the data.</span></span> <span data-ttu-id="2b5ad-119">在本教程中，您将添加一个搜索框，允许您查找特定流派的电影或其标题包含您输入的任何单词。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-119">In this tutorial, you'll add a search box that lets you find movies of a specific genre or whose title contains whatever word you enter.</span></span> <span data-ttu-id="2b5ad-120">（例如，您可以查找所有类型为"行动"或标题包含"Harry"或"冒险"的电影。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-120">(For example, you'll be able to find all movies whose genre is "Action" or whose title contains "Harry" or "Adventure.")</span></span>

<span data-ttu-id="2b5ad-121">完成本教程后，您将有一个像这样的页面：</span><span class="sxs-lookup"><span data-stu-id="2b5ad-121">When you're done with this tutorial, you'll have a page like this one:</span></span>

![包含流派和标题搜索的电影页面](form-basics/_static/image1.png)

<span data-ttu-id="2b5ad-123">页面的列表部分与上一教程&mdash;中网格相同。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-123">The listing part of the page is the same as in the last tutorial &mdash; a grid.</span></span> <span data-ttu-id="2b5ad-124">区别在于网格将仅显示您搜索的电影。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-124">The difference will be that the grid will show only the movies that you searched for.</span></span>

## <a name="about-html-forms"></a><span data-ttu-id="2b5ad-125">关于 HTML 表单</span><span class="sxs-lookup"><span data-stu-id="2b5ad-125">About HTML Forms</span></span>

<span data-ttu-id="2b5ad-126">（如果您在创建 HTML 窗体方面拥有经验，并且具有 和`GET``POST`之间的差异，则可以跳过此部分。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-126">(If you've got experience with creating HTML forms and with the difference between `GET` and `POST`, you can skip this section.)</span></span>

<span data-ttu-id="2b5ad-127">窗体具有用户输入元素&mdash;文本框、按钮、单选按钮、复选框、下拉列表等。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-127">A form has user input elements &mdash; text boxes, buttons, radio buttons, check boxes, drop-down lists, and so on.</span></span> <span data-ttu-id="2b5ad-128">用户填写这些控件或进行选择，然后通过单击按钮提交表单。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-128">Users fill in these controls or make selections and then submit the form by clicking a button.</span></span>

<span data-ttu-id="2b5ad-129">以下示例说明了窗体的基本 HTML 语法：</span><span class="sxs-lookup"><span data-stu-id="2b5ad-129">The basic HTML syntax of a form is illustrated by this example:</span></span>

[!code-html[Main](form-basics/samples/sample1.html)]

<span data-ttu-id="2b5ad-130">当此标记在页面中运行时，它将创建一个类似于下图的简单窗体：</span><span class="sxs-lookup"><span data-stu-id="2b5ad-130">When this markup runs in a page, it creates a simple form that looks like this illustration:</span></span>

![在浏览器中呈现的基本 HTML 表单](form-basics/_static/image2.png)

<span data-ttu-id="2b5ad-132">该`<form>`元素包含要提交的 HTML 元素。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-132">The `<form>` element encloses HTML elements to be submitted.</span></span> <span data-ttu-id="2b5ad-133">（一个简单的错误是向页面添加元素，但随后忘记将它们放入`<form>`元素中。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-133">(An easy mistake to make is to add elements to the page but then forget to put them inside a `<form>` element.</span></span> <span data-ttu-id="2b5ad-134">在这种情况下，不会提交任何内容。该`method`属性告诉浏览器如何提交用户输入。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-134">In that case, nothing is submitted.) The `method` attribute tells the browser how to submit the user input.</span></span> <span data-ttu-id="2b5ad-135">`post`如果在服务器上执行更新，或者`get`只是从服务器获取数据，则可以将此设置为</span><span class="sxs-lookup"><span data-stu-id="2b5ad-135">You set this to `post` if you're performing an update on the server or to `get` if you're just fetching data from the server.</span></span>

<a id="GET,_POST,_and_HTTP_Verb_Safety"></a>

> [!TIP] 
> 
> <span data-ttu-id="2b5ad-136">**获取、POST 和 HTTP 动词安全**</span><span class="sxs-lookup"><span data-stu-id="2b5ad-136">**GET, POST, and HTTP Verb Safety**</span></span>
> 
> <span data-ttu-id="2b5ad-137">HTTP是浏览器和服务器用来交换信息的协议，其基本操作非常简单。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-137">HTTP, the protocol that browsers and servers use to exchange information, is remarkably simple in its basic operations.</span></span> <span data-ttu-id="2b5ad-138">浏览器仅使用几个谓词向服务器发出请求。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-138">Browsers use only a few verbs to make requests to servers.</span></span> <span data-ttu-id="2b5ad-139">为 Web 编写代码时，了解这些谓词以及浏览器和服务器如何使用这些谓词会很有帮助。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-139">When you write code for the web, it's helpful to understand these verbs and how the browser and server use them.</span></span> <span data-ttu-id="2b5ad-140">远外最常用的动词是：</span><span class="sxs-lookup"><span data-stu-id="2b5ad-140">Far and away the most commonly used verbs are these:</span></span>
> 
> - <span data-ttu-id="2b5ad-141">`GET`.</span><span class="sxs-lookup"><span data-stu-id="2b5ad-141">`GET`.</span></span> <span data-ttu-id="2b5ad-142">浏览器使用此谓词从服务器获取内容。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-142">The browser uses this verb to fetch something from the server.</span></span> <span data-ttu-id="2b5ad-143">例如，当您在浏览器中键入 URL 时，浏览器将执行操作`GET`以请求所需的页面。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-143">For example, when you type a URL into your browser, the browser performs a `GET` operation to request the page you want.</span></span> <span data-ttu-id="2b5ad-144">如果页面包含图形，浏览器将执行其他`GET`操作以获取图像。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-144">If the page includes graphics, the browser performs additional `GET` operations to get the images.</span></span> <span data-ttu-id="2b5ad-145">如果`GET`操作必须将信息传递到服务器，则信息将作为查询字符串中 URL 的一部分传递。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-145">If the `GET` operation has to pass information to the server, the information is passed as part of the URL in the query string.</span></span>
> - <span data-ttu-id="2b5ad-146">`POST`.</span><span class="sxs-lookup"><span data-stu-id="2b5ad-146">`POST`.</span></span> <span data-ttu-id="2b5ad-147">浏览器发送`POST`请求以提交要在服务器上添加或更改的数据。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-147">The browser sends a `POST` request in order to submit data to be added or changed on the server.</span></span> <span data-ttu-id="2b5ad-148">例如，谓`POST`词用于在数据库中创建记录或更改现有记录。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-148">For example, the `POST` verb is used to create records in a database or change existing ones.</span></span> <span data-ttu-id="2b5ad-149">大多数时候，当您填写表单并单击提交按钮时，浏览器将执行操作`POST`。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-149">Most of the time, when you fill in a form and click the submit button, the browser performs a `POST` operation.</span></span> <span data-ttu-id="2b5ad-150">在操作`POST`中，传递给服务器的数据位于页面正文中。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-150">In a `POST` operation, the data being passed to the server is in the body of the page.</span></span>
> 
> <span data-ttu-id="2b5ad-151">这些谓词之间的一个重要区别是，操作`GET`不应更改服务器上的任何内容，或者以稍微抽象的方式将其放在操作中，`GET`操作不会导致服务器上的状态更改。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-151">An important distinction between these verbs is that a `GET` operation is not supposed to change anything on the server — or to put it in a slightly more abstract way, a `GET` operation does not result in a change in state on the server.</span></span> <span data-ttu-id="2b5ad-152">您可以根据需要多次对`GET`同一资源执行操作，并且这些资源不会更改。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-152">You can perform a `GET` operation on the same resources as many times as you like, and those resources don't change.</span></span> <span data-ttu-id="2b5ad-153">（操作`GET`通常说是"安全的"，或者使用技术术语，是*幂*等的。当然，与此相反，每次执行`POST`操作时，请求都会更改服务器上的内容。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-153">(A `GET` operation is often said to be "safe," or to use a technical term, is *idempotent*.) In contrast, of course, a `POST` request changes something on the server each time you perform the operation.</span></span>
> 
> <span data-ttu-id="2b5ad-154">两个例子将有助于说明这一区别。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-154">Two examples will help illustrate this distinction.</span></span> <span data-ttu-id="2b5ad-155">当您使用必应或 Google 等引擎执行搜索时，您将填写包含一个文本框的表单，然后单击搜索按钮。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-155">When you perform a search using an engine like Bing or Google, you fill in a form that consists of one text box, and then you click the search button.</span></span> <span data-ttu-id="2b5ad-156">浏览器执行操作`GET`，输入到框中的值作为 URL 的一部分传递。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-156">The browser performs a `GET` operation, with the value you entered into the box passed as part of the URL.</span></span> <span data-ttu-id="2b5ad-157">对这种类型的`GET`窗体使用操作很好，因为搜索操作不会更改服务器上的任何资源，因此只需获取信息。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-157">Using a `GET` operation for this type of form is fine, because a search operation doesn't change any resources on the server, it just fetches information.</span></span>
> 
> <span data-ttu-id="2b5ad-158">现在考虑在线订购内容的过程。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-158">Now consider the process of ordering something online.</span></span> <span data-ttu-id="2b5ad-159">您填写订单详细信息，然后单击提交按钮。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-159">You fill in the order details and then click the submit button.</span></span> <span data-ttu-id="2b5ad-160">此操作将是一个`POST`请求，因为该操作将导致服务器上的更改，例如新订单记录、帐户信息的更改，以及许多其他更改。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-160">This operation will be a `POST` request, because the operation will result in changes on the server, such as a new order record, a change in your account information, and perhaps many other changes.</span></span> <span data-ttu-id="2b5ad-161">与`GET`操作不同，您不能重复请求`POST`- 如果重复请求，则每次重新提交请求时，都会在服务器上生成新订单。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-161">Unlike the `GET` operation, you cannot repeat your `POST` request — if you did, each time you resubmitted the request, you'd generate a new order on the server.</span></span> <span data-ttu-id="2b5ad-162">（在这种情况下，网站通常会警告您不要多次单击提交按钮，或者将禁用提交按钮，以便您不会意外重新提交表单。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-162">(In cases like this, websites will often warn you not to click a submit button more than once, or will disable the submit button so that you don't resubmit the form accidentally.)</span></span>
> 
> <span data-ttu-id="2b5ad-163">在本教程中，您将使用`GET`操作和`POST`操作来处理 HTML 窗体。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-163">In the course of this tutorial, you'll use both a `GET` operation and a `POST` operation to work with HTML forms.</span></span> <span data-ttu-id="2b5ad-164">我们将在每种情况下解释为什么您使用的动词是合适的。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-164">We'll explain in each case why the verb you use is the appropriate one.</span></span>
> 
> <span data-ttu-id="2b5ad-165">（要了解有关 HTTP 谓词的更多信息，请参阅 W3C 网站上的[方法定义](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html)文章。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-165">(To learn more about HTTP verbs, see the [Method Definitions](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html) article on the W3C site.)</span></span>

<span data-ttu-id="2b5ad-166">大多数用户输入元素是`<input>`HTML 元素。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-166">Most user input elements are HTML `<input>` elements.</span></span> <span data-ttu-id="2b5ad-167">它们看起来像`<input type="type" name="name">,`*类型*指示所需用户输入控件的类型。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-167">They look like `<input type="type" name="name">,` where *type* indicates the kind of user input control you want.</span></span> <span data-ttu-id="2b5ad-168">这些元素是常见的元素：</span><span class="sxs-lookup"><span data-stu-id="2b5ad-168">These elements are the common ones:</span></span>

- <span data-ttu-id="2b5ad-169">文本框：`<input type="text">`</span><span class="sxs-lookup"><span data-stu-id="2b5ad-169">Text box: `<input type="text">`</span></span>
- <span data-ttu-id="2b5ad-170">复选框：`<input type="check">`</span><span class="sxs-lookup"><span data-stu-id="2b5ad-170">Check box: `<input type="check">`</span></span>
- <span data-ttu-id="2b5ad-171">单选按钮：`<input type="radio">`</span><span class="sxs-lookup"><span data-stu-id="2b5ad-171">Radio button: `<input type="radio">`</span></span>
- <span data-ttu-id="2b5ad-172">按钮：`<input type="button">`</span><span class="sxs-lookup"><span data-stu-id="2b5ad-172">Button: `<input type="button">`</span></span>
- <span data-ttu-id="2b5ad-173">提交按钮：`<input type="submit">`</span><span class="sxs-lookup"><span data-stu-id="2b5ad-173">Submit button: `<input type="submit">`</span></span>

<span data-ttu-id="2b5ad-174">您还可以使用 元素`<textarea>`创建多行文本框和`<select>`元素以创建下拉列表或可滚动列表。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-174">You can also use the `<textarea>` element to create a multiline text box and the `<select>` element to create a drop-down list or scrollable list.</span></span> <span data-ttu-id="2b5ad-175">（有关 HTML 表单元素的更多内容，请参阅 W3Schools 网站上的[HTML 表单和输入](http://www.w3schools.com/html/html_forms.asp)。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-175">(For more about HTML form elements, see [HTML Forms and Input](http://www.w3schools.com/html/html_forms.asp) on the W3Schools site.)</span></span>

<span data-ttu-id="2b5ad-176">该`name`属性非常重要，因为名称是以后获取元素值的方式，稍后将看到。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-176">The `name` attribute is very important, because the name is how you'll get the value of the element later, as you'll see shortly.</span></span>

<span data-ttu-id="2b5ad-177">有趣的部分是您，页面开发人员，对用户输入所做的操作。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-177">The interesting part is what you, the page developer, do with the user's input.</span></span> <span data-ttu-id="2b5ad-178">没有与这些元素关联的内置行为。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-178">There's no built-in behavior associated with these elements.</span></span> <span data-ttu-id="2b5ad-179">相反，您必须获取用户已输入或选择的值，并对其进行操作。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-179">Instead, you have to get the values that the user has entered or selected and do something with them.</span></span> <span data-ttu-id="2b5ad-180">这是您将在本教程中学到的。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-180">That's what you'll learn in this tutorial.</span></span>

> [!TIP] 
> 
> <span data-ttu-id="2b5ad-181">**HTML5 和输入表单**</span><span class="sxs-lookup"><span data-stu-id="2b5ad-181">**HTML5 and Input Forms**</span></span>
> 
> <span data-ttu-id="2b5ad-182">您可能知道，HTML 处于过渡状态，最新版本 （HTML5） 包括支持用户输入信息的更直观方式。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-182">As you might know, HTML is in transition and the latest version (HTML5) includes support for more intuitive ways for users to enter information.</span></span> <span data-ttu-id="2b5ad-183">例如，在 HTML5 中，您可以告诉页面您希望用户输入日期。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-183">For example, in HTML5, you (the page developer) can tell the page that you want the user to enter a date.</span></span> <span data-ttu-id="2b5ad-184">然后，浏览器可以自动显示日历，而不是要求用户手动输入日期。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-184">The browser can then automatically display a calendar rather than requiring the user to enter a date manually.</span></span> <span data-ttu-id="2b5ad-185">但是，HTML5 是新的，并非所有浏览器都支持 HTML5。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-185">However, HTML5 is new and is not supported in all browsers yet.</span></span>
> 
> <span data-ttu-id="2b5ad-186">ASP.NET网页支持 HTML5 输入，只要用户的浏览器支持 HTML5 输入。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-186">ASP.NET Web Pages supports HTML5 input to the extent that the user's browser does.</span></span> <span data-ttu-id="2b5ad-187">有关 HTML5 中`<input>`元素的新属性的概念，请参阅 W3Schools 站点上的 HTML[&lt;输入&gt;类型属性](http://www.w3schools.com/html/html_form_input_types.asp)。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-187">For an idea of the new attributes for the `<input>` element in HTML5, see [HTML &lt;input&gt; type Attribute](http://www.w3schools.com/html/html_form_input_types.asp) on the W3Schools site.</span></span>

## <a name="creating-the-form"></a><span data-ttu-id="2b5ad-188">创建窗体</span><span class="sxs-lookup"><span data-stu-id="2b5ad-188">Creating the Form</span></span>

<span data-ttu-id="2b5ad-189">在 WebMatrix 中，在 **"文件**"工作区中，打开 *"电影.cshtml"* 页面。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-189">In WebMatrix, in the **Files** workspace, open the *Movies.cshtml* page.</span></span>

<span data-ttu-id="2b5ad-190">在结束`</h1>`标记之后和`<div>``grid.GetHtml`呼叫的开头标记之前，添加以下标记：</span><span class="sxs-lookup"><span data-stu-id="2b5ad-190">After the closing `</h1>` tag and before the opening `<div>` tag of the `grid.GetHtml` call, add the following markup:</span></span>

[!code-html[Main](form-basics/samples/sample2.html)]

<span data-ttu-id="2b5ad-191">此标记创建一个窗体，该窗体具有名为`searchGenre`文本框和提交按钮。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-191">This markup creates a form that has a text box named `searchGenre` and a submit button.</span></span> <span data-ttu-id="2b5ad-192">文本框和提交按钮包含在其`<form>``method`属性设置为`get`的元素中。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-192">The text box and submit button are enclosed in a `<form>` element whose `method` attribute is set to `get`.</span></span> <span data-ttu-id="2b5ad-193">（请记住，如果不将文本框和提交按钮放在`<form>`元素中，则单击该按钮时不会提交任何内容。您在此处使用`GET`谓词是因为您正在创建一个不会在服务器上进行任何更改的窗体 - 它只是导致搜索。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-193">(Remember that if you don't put the text box and submit button inside a `<form>` element, nothing will be submitted when you click the button.) You use the `GET` verb here because you're creating a form that does not make any changes on the server — it just results in a search.</span></span> <span data-ttu-id="2b5ad-194">（在前面的教程中，您使用了一`post`种方法，即向服务器提交更改的方式。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-194">(In the previous tutorial, you used a `post` method, which is how you submit changes to the server.</span></span> <span data-ttu-id="2b5ad-195">您将在下一教程中再次看到这一点。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-195">You'll see that in the next tutorial again.)</span></span>

<span data-ttu-id="2b5ad-196">运行页面。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-196">Run the page.</span></span> <span data-ttu-id="2b5ad-197">尽管尚未为窗体定义任何行为，但您可以看到它的外观：</span><span class="sxs-lookup"><span data-stu-id="2b5ad-197">Although you haven't defined any behavior for the form, you can see what it looks like:</span></span>

![带有"流派"搜索框的影片页面](form-basics/_static/image3.png)

<span data-ttu-id="2b5ad-199">在文本框中输入一个值，如"喜剧"。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-199">Enter a value into the text box, like "Comedy."</span></span> <span data-ttu-id="2b5ad-200">然后单击**搜索流派**。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-200">Then click **Search Genre**.</span></span>

<span data-ttu-id="2b5ad-201">记下页面的 URL。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-201">Take note of the URL of the page.</span></span> <span data-ttu-id="2b5ad-202">由于将`<form>`元素的属性`method`设置为`get`，因此您输入的值现在是 URL 中查询字符串的一部分，如下所示：</span><span class="sxs-lookup"><span data-stu-id="2b5ad-202">Because you set the `<form>` element's `method` attribute to `get`, the value you entered is now part of the query string in the URL, like this:</span></span>

`http://localhost:45661/Movies.cshtml?searchGenre=Comedy`

## <a name="reading-form-values"></a><span data-ttu-id="2b5ad-203">读取窗体值</span><span class="sxs-lookup"><span data-stu-id="2b5ad-203">Reading Form Values</span></span>

<span data-ttu-id="2b5ad-204">该页已包含一些代码，这些代码获取数据库数据并在网格中显示结果。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-204">The page already contains some code that gets database data and displays the results in a grid.</span></span> <span data-ttu-id="2b5ad-205">现在，您必须添加一些读取文本框值的代码，以便运行包含搜索词的 SQL 查询。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-205">Now you have to add some code that reads the value of the text box so you can run a SQL query that includes the search term.</span></span>

<span data-ttu-id="2b5ad-206">由于将窗体的方法设置为`get`，因此可以使用如下所示的代码读取输入到文本框中的值：</span><span class="sxs-lookup"><span data-stu-id="2b5ad-206">Because you set the form's method to `get`, you can read the value that was entered into the text box by using code like the following:</span></span>

`var searchTerm = Request.QueryString["searchGenre"];`

<span data-ttu-id="2b5ad-207">对象`Request.QueryString`（`QueryString``Request`对象的属性）包括作为`GET`操作的一部分提交的元素的值。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-207">The `Request.QueryString` object (the `QueryString` property of the `Request` object) includes the values of elements that were submitted as part of the `GET` operation.</span></span> <span data-ttu-id="2b5ad-208">属性`Request.QueryString`包含表单中提交的值*的集合*（列表）。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-208">The `Request.QueryString` property contains a *collection* (a list) of the values that are submitted in the form.</span></span> <span data-ttu-id="2b5ad-209">要获取任何单个值，请指定所需的元素的名称。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-209">To get any individual value, you specify the name of the element that you want.</span></span> <span data-ttu-id="2b5ad-210">这就是为什么您必须在创建文本框`name``<input>`的元素 （`searchTerm`） 上具有属性的原因。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-210">That's why you have to have a `name` attribute on the `<input>` element (`searchTerm`) that creates the text box.</span></span> <span data-ttu-id="2b5ad-211">（有关对象的更多，`Request`请参阅侧[边栏](#BKMK_TheRequestObject)。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-211">(For more about the `Request` object, see the [sidebar](#BKMK_TheRequestObject) later.)</span></span>

<span data-ttu-id="2b5ad-212">阅读文本框的值非常简单。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-212">It's simple enough to read the value of the text box.</span></span> <span data-ttu-id="2b5ad-213">但是，如果用户在文本框中根本不输入任何内容，但无论如何都单击 **"搜索"，** 则可以忽略该单击，因为没有什么可搜索的。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-213">But if the user didn't enter anything at all in the text box but clicked **Search** anyway, you can ignore that click, since there's nothing to search.</span></span>

<span data-ttu-id="2b5ad-214">以下代码是演示如何实现这些条件的示例。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-214">The following code is an example that shows how to implement these conditions.</span></span> <span data-ttu-id="2b5ad-215">（您不必添加此代码，您一会儿就将添加。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-215">(You don't have to add this code yet; you'll do that in a moment.)</span></span>

[!code-csharp[Main](form-basics/samples/sample3.cs)]

<span data-ttu-id="2b5ad-216">测试以这种方式分解：</span><span class="sxs-lookup"><span data-stu-id="2b5ad-216">The test breaks down in this way:</span></span>

- <span data-ttu-id="2b5ad-217">获取 的值`Request.QueryString["searchGenre"]`，即输入到名为`<input>``searchGenre`的元素中的值。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-217">Get the value of `Request.QueryString["searchGenre"]`, namely the value that was entered into the `<input>` element named `searchGenre`.</span></span>
- <span data-ttu-id="2b5ad-218">使用`IsEmpty`方法了解其是否为空。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-218">Find out if it's empty by using the `IsEmpty` method.</span></span> <span data-ttu-id="2b5ad-219">此方法是确定某些内容（例如窗体元素）是否包含值的标准方法。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-219">This method is the standard way to determine whether something (for example, a form element) contains a value.</span></span> <span data-ttu-id="2b5ad-220">但实际上，你只关心，如果它*不*是空的，因此...</span><span class="sxs-lookup"><span data-stu-id="2b5ad-220">But really, you care only if it's *not* empty, therefore ...</span></span>
- <span data-ttu-id="2b5ad-221">在`!``IsEmpty`测试前添加运算符。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-221">Add the `!` operator in front of the `IsEmpty` test.</span></span> <span data-ttu-id="2b5ad-222">（运算符`!`表示逻辑 NOT）。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-222">(The `!` operator means logical NOT).</span></span>

<span data-ttu-id="2b5ad-223">在纯英语中，整个`if`条件将转换为以下内容：*如果窗体的 searchGenre 元素不为空，则 ...*</span><span class="sxs-lookup"><span data-stu-id="2b5ad-223">In plain English, the entire `if` condition translates into the following: *If the form's searchGenre element is not empty, then ...*</span></span>

<span data-ttu-id="2b5ad-224">此块设置创建使用搜索词的查询的阶段。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-224">This block sets the stage for creating a query that uses the search term.</span></span> <span data-ttu-id="2b5ad-225">将在下一部分执行该操作。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-225">You'll do that in the next section.</span></span>

<a id="BKMK_TheRequestObject"></a>

> [!TIP] 
> 
> <span data-ttu-id="2b5ad-226">**请求对象**</span><span class="sxs-lookup"><span data-stu-id="2b5ad-226">**The Request Object**</span></span>
> 
> <span data-ttu-id="2b5ad-227">该`Request`对象包含浏览器在请求或提交页面时发送到应用程序的所有信息。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-227">The `Request` object contains all the information that the browser sends to your application when a page is requested or submitted.</span></span> <span data-ttu-id="2b5ad-228">此对象包括用户提供的任何信息，如文本框值或要上载的文件。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-228">This object includes any information that the user provides, like text box values or a file to upload.</span></span> <span data-ttu-id="2b5ad-229">它还包括各种附加信息，如 Cookie、URL 查询字符串中的值（如果有）、正在运行的页面的文件路径、用户使用的浏览器类型、在浏览器中设置的语言列表等等。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-229">It also includes all sorts of additional information, like cookies, values in the URL query string (if any), the file path of the page that is running, the type of browser that the user is using, the list of languages that are set in the browser, and much more.</span></span>
> 
> <span data-ttu-id="2b5ad-230">该`Request`对象是值*的集合*（列表）。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-230">The `Request` object is a *collection* (list) of values.</span></span> <span data-ttu-id="2b5ad-231">通过指定单个值的名称，从集合中获取单个值：</span><span class="sxs-lookup"><span data-stu-id="2b5ad-231">You get an individual value out of the collection by specifying its name:</span></span>
> 
> `var someValue = Request["name"];`
> 
> <span data-ttu-id="2b5ad-232">该`Request`对象实际上公开了几个子集。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-232">The `Request` object actually exposes several subsets.</span></span> <span data-ttu-id="2b5ad-233">例如：</span><span class="sxs-lookup"><span data-stu-id="2b5ad-233">For example:</span></span>
> 
> - <span data-ttu-id="2b5ad-234">`Request.Form`如果请求是`POST`请求，则从提交`<form>`元素中的元素提供值。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-234">`Request.Form` gives you values from elements inside the submitted `<form>` element if the request is a `POST` request.</span></span>
> - <span data-ttu-id="2b5ad-235">`Request.QueryString`仅为您提供 URL 查询字符串中的值。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-235">`Request.QueryString` gives you just the values in the URL's query string.</span></span> <span data-ttu-id="2b5ad-236">（在 URL`http://mysite/myapp/page?searchGenre=action&page=2`中，URL 的`?searchGenre=action&page=2`部分是查询字符串。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-236">(In a URL like `http://mysite/myapp/page?searchGenre=action&page=2`, the `?searchGenre=action&page=2` section of the URL is the query string.)</span></span>
> - <span data-ttu-id="2b5ad-237">`Request.Cookies`集合允许您访问浏览器发送的 Cookie。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-237">`Request.Cookies` collection gives you access to cookies that the browser has sent.</span></span>
> 
> <span data-ttu-id="2b5ad-238">要获取您知道在提交的窗体中的值，可以使用`Request["name"]`。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-238">To get a value that you know is in the submitted form, you can use `Request["name"]`.</span></span> <span data-ttu-id="2b5ad-239">或者，`Request.Form["name"]`您可以使用更具体的版本（用于`POST`请求）或`Request.QueryString["name"]`（用于`GET`请求）。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-239">Alternatively, you can use the more specific versions `Request.Form["name"]` (for `POST` requests) or `Request.QueryString["name"]` (for `GET` requests).</span></span> <span data-ttu-id="2b5ad-240">当然，*名称*是要获取的项的名称。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-240">Of course, *name* is the name of the item to get.</span></span>
> 
> <span data-ttu-id="2b5ad-241">要获取的项的名称必须在要使用的集合中是唯一的。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-241">The name of the item you want to get has to be unique within the collection you're using.</span></span> <span data-ttu-id="2b5ad-242">这就是为什么`Request`对象提供子集，如`Request.Form`和`Request.QueryString`。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-242">That's why the `Request` object provides the subsets like `Request.Form` and `Request.QueryString`.</span></span> <span data-ttu-id="2b5ad-243">假设您的页面包含名为 的`userName`窗体元素，*并且还*包含名为 的`userName`Cookie。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-243">Suppose that your page contains a form element named `userName` and *also* contains a cookie named `userName`.</span></span> <span data-ttu-id="2b5ad-244">如果得到`Request["userName"]`，则是模糊的是想要表单值还是 Cookie。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-244">If you get `Request["userName"]`, it's ambiguous whether you want the form value or the cookie.</span></span> <span data-ttu-id="2b5ad-245">但是，如果您得到`Request.Form["userName"]`或`Request.Cookie["userName"]`，则明确要获取的值。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-245">However, if you get `Request.Form["userName"]` or `Request.Cookie["userName"]`, you're being explicit about which value to get.</span></span>
> 
> <span data-ttu-id="2b5ad-246">最好是具体使用您感兴趣的子集`Request`，例如`Request.Form`或`Request.QueryString`。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-246">It's a good practice to be specific and use the subset of `Request` that you're interested in, like `Request.Form` or `Request.QueryString`.</span></span> <span data-ttu-id="2b5ad-247">对于您在本教程中创建的简单页面，它可能没有任何区别。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-247">For the simple pages that you're creating in this tutorial, it probably doesn't really make any difference.</span></span> <span data-ttu-id="2b5ad-248">但是，当您创建更复杂的页面时，使用显式版本`Request.Form`或`Request.QueryString`可以帮助您避免在页面包含窗体（或多个窗体）、Cookie、查询字符串值等时可能出现的问题。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-248">However, as you create more complex pages, using the explicit version `Request.Form` or `Request.QueryString` can help you avoid problems that can arise when the page contains a form (or multiple forms), cookies, query string values, and so on.</span></span>

## <a name="creating-a-query-by-using-a-search-term"></a><span data-ttu-id="2b5ad-249">使用搜索词创建查询</span><span class="sxs-lookup"><span data-stu-id="2b5ad-249">Creating a Query by Using a Search Term</span></span>

<span data-ttu-id="2b5ad-250">现在，您已经知道如何获取用户输入的搜索词，您可以创建使用它的查询。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-250">Now that you know how to get the search term that the user entered, you can create a query that uses it.</span></span> <span data-ttu-id="2b5ad-251">请记住，要将所有影片项从数据库中获取出来，您使用的是 SQL 查询，该查询如下所示：</span><span class="sxs-lookup"><span data-stu-id="2b5ad-251">Remember that to get all the movie items out of the database, you're using a SQL query that looks like this statement:</span></span>

`SELECT * FROM Movies`

<span data-ttu-id="2b5ad-252">要仅获取某些影片，必须使用包含子句的`Where`查询。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-252">To get only certain movies, you have to use a query that includes a `Where` clause.</span></span> <span data-ttu-id="2b5ad-253">此子句允许您设置查询返回行的条件。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-253">This clause lets you set a condition on which rows are returned by the query.</span></span> <span data-ttu-id="2b5ad-254">下面是一个示例：</span><span class="sxs-lookup"><span data-stu-id="2b5ad-254">Here's an example:</span></span>

`SELECT * FROM Movies WHERE Genre = 'Action'`

<span data-ttu-id="2b5ad-255">基本格式为`WHERE column = value`。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-255">The basic format is `WHERE column = value`.</span></span> <span data-ttu-id="2b5ad-256">除了（`=`大于`>`）、（小于）、（`<`不等于）、（`<>``<=`小于或等于）等之外，还可以使用不同的运算符，具体取决于您要查找的内容。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-256">You can use different operators besides just `=`, like `>` (greater than), `<` (less than), `<>` (not equal to), `<=` (less than or equal to), etc., depending on what you're looking for.</span></span>

<span data-ttu-id="2b5ad-257">如果您想知道，SQL 语句不是大小写敏感&mdash;`SELECT`与`Select`（或 甚至`select`） 相同。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-257">In case you're wondering, SQL statements are not case sensitive &mdash; `SELECT` is the same as `Select` (or even `select`).</span></span> <span data-ttu-id="2b5ad-258">但是，人们通常使用 SQL 语句中的关键字（`SELECT`如`WHERE`和）来使其更易于阅读。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-258">However, people often capitalize keywords in a SQL statement, like `SELECT` and `WHERE`, to make it easier to read.</span></span>

### <a name="passing-the-search-term-as-a-parameter"></a><span data-ttu-id="2b5ad-259">将搜索词作为参数传递</span><span class="sxs-lookup"><span data-stu-id="2b5ad-259">Passing the search term as a parameter</span></span>

<span data-ttu-id="2b5ad-260">搜索特定流派非常简单 （），`WHERE Genre = 'Action'`但您希望能够搜索用户输入的任何流派。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-260">Searching for a specific genre is easy enough (`WHERE Genre = 'Action'`), but you want to be able to search for any genre that the user enters.</span></span> <span data-ttu-id="2b5ad-261">为此，您可以创建为 SQL 查询，其中包含要搜索的值的占位符。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-261">To do that, you create as SQL query that includes a placeholder for the value to search.</span></span> <span data-ttu-id="2b5ad-262">它将看起来像此命令：</span><span class="sxs-lookup"><span data-stu-id="2b5ad-262">It will look like this command:</span></span>

`SELECT * FROM Movies WHERE Genre = @0`

<span data-ttu-id="2b5ad-263">占位符是字符`@`后跟零。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-263">The placeholder is the `@` character followed by zero.</span></span> <span data-ttu-id="2b5ad-264">正如您可能猜到的，查询可以包含多个占位符，并且它们将命名为`@0`、、、、、、、、、、、、、、`@1``@2`它们。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-264">As you might guess, a query can contain multiple placeholders, and they'd be named `@0`, `@1`, `@2`, etc.</span></span>

<span data-ttu-id="2b5ad-265">要设置查询并实际传递该值，请使用如下所示的代码：</span><span class="sxs-lookup"><span data-stu-id="2b5ad-265">To set up the query and actually pass it the value, you use the code like the following:</span></span>

[!code-sql[Main](form-basics/samples/sample4.sql)]

<span data-ttu-id="2b5ad-266">此代码类似于您为在网格中显示数据所做的。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-266">This code is similar to what you've already done to display data in the grid.</span></span> <span data-ttu-id="2b5ad-267">唯一的区别是：</span><span class="sxs-lookup"><span data-stu-id="2b5ad-267">The only differences are:</span></span>

- <span data-ttu-id="2b5ad-268">查询包含占位符 （`WHERE Genre = @0"`。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-268">The query contains a placeholder (`WHERE Genre = @0"`).</span></span>
- <span data-ttu-id="2b5ad-269">查询被放入变量 （`selectCommand`;之前，您将查询直接传递给 方法`db.Query`。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-269">The query is put into a variable (`selectCommand`); before, you passed the query directly to the `db.Query` method.</span></span>
- <span data-ttu-id="2b5ad-270">调用`db.Query`方法时，将传递查询和要用于占位符的值。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-270">When you call the `db.Query` method, you pass both the query and the value to use for the placeholder.</span></span> <span data-ttu-id="2b5ad-271">（如果查询有多个占位符，则将它们全部作为单独的值传递给方法。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-271">(If the query had multiple placeholders, you'd pass them all as separate values to the method.)</span></span>

<span data-ttu-id="2b5ad-272">如果将所有这些元素放在一起，您将获得以下代码：</span><span class="sxs-lookup"><span data-stu-id="2b5ad-272">If you put all these elements together, you get the following code:</span></span>

[!code-csharp[Main](form-basics/samples/sample5.cs)]

> [!NOTE] 
> 
> <span data-ttu-id="2b5ad-273">**重要！**</span><span class="sxs-lookup"><span data-stu-id="2b5ad-273">**Important!**</span></span> <span data-ttu-id="2b5ad-274">使用占位符`@0`（如 ） 将值传递给 SQL 命令对于安全性*至关重要*。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-274">Using placeholders (like `@0`) to pass values to a SQL command is *extremely important* for security.</span></span> <span data-ttu-id="2b5ad-275">此处查看的方式（使用变量数据的占位符）是构建 SQL 命令的唯一方法。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-275">The way you see it here, with placeholders for variable data, is the only way you should construct SQL commands.</span></span>
> 
> <span data-ttu-id="2b5ad-276">切勿通过将从用户获得的文本和值组合（串联）来构造 SQL 语句。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-276">Never construct a SQL statement by putting together (concatenating) literal text and values you get from the user.</span></span> <span data-ttu-id="2b5ad-277">将用户输入串联到 SQL 语句中会将您的网站置于*SQL 注入攻击*中，恶意用户向您的页面提交入侵数据库的值。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-277">Concatenating user input into a SQL statement opens your site to a *SQL injection attack* where a malicious user submits values to your page that hack your database.</span></span> <span data-ttu-id="2b5ad-278">（您可以在文章[SQL 注入](https://msdn.microsoft.com/library/ms161953.aspx)MSDN 网站中阅读更多内容。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-278">(You can read more in the article [SQL Injection](https://msdn.microsoft.com/library/ms161953.aspx) the MSDN website.)</span></span>

## <a name="updating-the-movies-page-with-search-code"></a><span data-ttu-id="2b5ad-279">使用搜索代码更新电影页面</span><span class="sxs-lookup"><span data-stu-id="2b5ad-279">Updating the Movies Page with Search Code</span></span>

<span data-ttu-id="2b5ad-280">现在，您可以更新 *"电影.cshtml"* 文件中的代码。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-280">Now you can update the code in the *Movies.cshtml* file.</span></span> <span data-ttu-id="2b5ad-281">首先，用以下代码替换页面顶部的代码块中的代码：</span><span class="sxs-lookup"><span data-stu-id="2b5ad-281">To begin, replace the code in the code block at the top of the page with this code:</span></span>

[!code-csharp[Main](form-basics/samples/sample6.cs)]

<span data-ttu-id="2b5ad-282">此处的区别是，您已将查询放入变量中`selectCommand`，稍后将传递给`db.Query`该变量。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-282">The difference here is that you've put the query into the `selectCommand` variable, which you'll pass to `db.Query` later.</span></span> <span data-ttu-id="2b5ad-283">将 SQL 语句放入变量中可以更改语句，这是执行搜索时执行的操作。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-283">Putting the SQL statement into a variable lets you change the statement, which is what you'll do to perform the search.</span></span>

<span data-ttu-id="2b5ad-284">您还删除了这两行，稍后将重新放入：</span><span class="sxs-lookup"><span data-stu-id="2b5ad-284">You've also removed these two lines, which you'll put back in later:</span></span>

[!code-csharp[Main](form-basics/samples/sample7.cs)]

<span data-ttu-id="2b5ad-285">您还不想运行查询（即调用`db.Query`），并且也不想初始化`WebGrid`帮助程序。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-285">You don't want to run the query yet (that is, call `db.Query`) and you don't want to initialize the `WebGrid` helper yet either.</span></span> <span data-ttu-id="2b5ad-286">在找出必须运行哪些 SQL 语句后，您将执行这些操作。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-286">You'll do those things after you've figured out which SQL statement has to run.</span></span>

<span data-ttu-id="2b5ad-287">重写此块后，可以添加新逻辑来处理搜索。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-287">After this rewritten block, you can add the new logic for handling the search.</span></span> <span data-ttu-id="2b5ad-288">已完成的代码如下所示。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-288">The completed code will look like the following.</span></span> <span data-ttu-id="2b5ad-289">更新页面中的代码，使其与此示例匹配：</span><span class="sxs-lookup"><span data-stu-id="2b5ad-289">Update the code in your page so it matches this example:</span></span>

[!code-cshtml[Main](form-basics/samples/sample8.cshtml)]

<span data-ttu-id="2b5ad-290">页面现在像这样工作。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-290">The page now works like this.</span></span> <span data-ttu-id="2b5ad-291">每次运行页面时，代码都会打开数据库，`selectCommand`变量将设置为 SQL 语句，该语句从`Movies`表中获取所有记录。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-291">Every time the page runs, the code opens the database and the `selectCommand` variable is set to the SQL statement that gets all the records from the `Movies` table.</span></span> <span data-ttu-id="2b5ad-292">代码还会初始化`searchTerm`变量。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-292">The code also initializes the `searchTerm` variable.</span></span>

<span data-ttu-id="2b5ad-293">但是，如果当前请求包含`searchGenre`元素的值，则代码将设置`selectCommand`为不同的查询，即包含用于搜索流派`Where`的子句。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-293">However, if the current request includes a value for the `searchGenre` element, the code sets `selectCommand` to a different query — namely, to one that includes the `Where` clause to search for a genre.</span></span> <span data-ttu-id="2b5ad-294">它还设置`searchTerm`到搜索框传递的一切（可能什么都不）。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-294">It also sets `searchTerm` to whatever was passed for the search box (which might be nothing).</span></span>

<span data-ttu-id="2b5ad-295">无论 SQL 语句在`selectCommand`中哪个，代码都会`db.Query`调用以运行查询，将其传递给`searchTerm`中的任何内容。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-295">Regardless of which SQL statement is in `selectCommand`, the code then calls `db.Query` to run the query, passing it whatever is in `searchTerm`.</span></span> <span data-ttu-id="2b5ad-296">如果 中`searchTerm`没有任何内容，则无关紧要，因为在这种情况下，没有参数可以无论如何将值传递给`selectCommand`。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-296">If there's nothing in `searchTerm`, it doesn't matter, because in that case there's no parameter to pass the value to `selectCommand` anyway.</span></span>

<span data-ttu-id="2b5ad-297">最后，代码使用查询结果初始化`WebGrid`帮助程序，就像以前一样。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-297">Finally, the code initializes the `WebGrid` helper by using the query results, just like before.</span></span>

<span data-ttu-id="2b5ad-298">您可以看到，通过将 SQL 语句和搜索词放入变量中，增加了代码的灵活性。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-298">You can see that by putting the SQL statement and the search term into variables, you've added flexibility to the code.</span></span> <span data-ttu-id="2b5ad-299">正如本教程稍后将看到的那样，您可以使用此基本框架，并继续为不同类型的搜索添加逻辑。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-299">As you'll see later in this tutorial, you can use this basic framework and keep adding logic for different types of searches.</span></span>

## <a name="testing-the-search-by-genre-feature"></a><span data-ttu-id="2b5ad-300">测试按类型搜索功能</span><span class="sxs-lookup"><span data-stu-id="2b5ad-300">Testing the Search-by-Genre Feature</span></span>

<span data-ttu-id="2b5ad-301">在 WebMatrix 中，运行 *"电影.cshtml"* 页。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-301">In WebMatrix, run the *Movies.cshtml* page.</span></span> <span data-ttu-id="2b5ad-302">您将看到带有流派文本框的页面。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-302">You see the page with the text box for genre.</span></span>

<span data-ttu-id="2b5ad-303">输入您为其中一个测试记录输入的流派，然后单击 **"搜索**"。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-303">Enter a genre that you've entered for one of your test records, then click **Search**.</span></span> <span data-ttu-id="2b5ad-304">这一次，你看到一个列表，只是电影匹配该流派：</span><span class="sxs-lookup"><span data-stu-id="2b5ad-304">This time you see a listing of just the movies that match that genre:</span></span>

![电影页面列表后搜索流派"喜剧"](form-basics/_static/image4.png)

<span data-ttu-id="2b5ad-306">输入其他流派并再次搜索。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-306">Enter a different genre and search again.</span></span> <span data-ttu-id="2b5ad-307">尝试使用所有小写或所有大写字母输入流派，以便您可以看到搜索不区分大小写。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-307">Try entering the genre by using all lowercase or all uppercase letters so that you can see that the search is not case sensitive.</span></span>

## <a name="remembering-what-the-user-entered"></a><span data-ttu-id="2b5ad-308">"记住"用户输入的内容</span><span class="sxs-lookup"><span data-stu-id="2b5ad-308">"Remembering" What the User Entered</span></span>

<span data-ttu-id="2b5ad-309">您可能已经注意到，在您输入一个流派并单击**搜索流派**后，您看到了该流派的列表。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-309">You might have noticed that after you entered a genre and clicked **Search Genre**, you saw a listing for that genre.</span></span> <span data-ttu-id="2b5ad-310">但是，搜索文本框换句话说是&mdash;空的，它不记得您输入的内容。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-310">However, the search text box was empty &mdash; in other words, it didn't remember what you'd entered.</span></span>

<span data-ttu-id="2b5ad-311">了解此行为发生的原因非常重要。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-311">It's important to understand why this behavior occurs.</span></span> <span data-ttu-id="2b5ad-312">提交页面时，浏览器会向 Web 服务器发送请求。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-312">When you submit a page, the browser sends a request to the web server.</span></span> <span data-ttu-id="2b5ad-313">当ASP.NET收到请求时，它会创建页面的全新实例，在其中运行代码，然后将页面再次呈现给浏览器。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-313">When ASP.NET gets the request, it creates a brand-new instance of the page, runs the code in it, and then renders the page to the browser again.</span></span> <span data-ttu-id="2b5ad-314">实际上，该页面不知道您只是使用自身的早期版本。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-314">In effect, though, the page doesn't know that you were just working with a previous version of itself.</span></span> <span data-ttu-id="2b5ad-315">它只知道，它得到了一个请求，其中有一些表单数据。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-315">All it knows is that it got a request that had some form data in it.</span></span>

<span data-ttu-id="2b5ad-316">每次请求页面时，无论是&mdash;首次请求还是提交页面&mdash;，您都会获得新页面。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-316">Every time you request a page &mdash; whether for the first time or by submitting it &mdash; you're getting a new page.</span></span> <span data-ttu-id="2b5ad-317">Web 服务器没有您上次请求的内存。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-317">The web server has no memory of your last request.</span></span> <span data-ttu-id="2b5ad-318">浏览器也不ASP.NET，浏览器也不ASP.NET。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-318">Neither does ASP.NET, and neither does the browser.</span></span> <span data-ttu-id="2b5ad-319">页面的这些单独实例之间的唯一连接是您在它们之间传输的任何数据。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-319">The only connection between these separate instances of the page is any data that you transmit between them.</span></span> <span data-ttu-id="2b5ad-320">例如，如果提交页面，则新页面实例可以获取前一个实例发送的表单数据。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-320">If you submit a page, for example, the new page instance can get the form data that was sent by the earlier instance.</span></span> <span data-ttu-id="2b5ad-321">（在页面之间传递数据的另一种方法是使用 Cookie。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-321">(Another way to pass data between pages is to use cookies.)</span></span>

<span data-ttu-id="2b5ad-322">描述这种情况的一个正式方法是说网页是*无状态的*。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-322">A formal way to describe this situation is to say that web pages are *stateless*.</span></span> <span data-ttu-id="2b5ad-323">Web 服务器和页面本身以及页面中的元素不保留有关页面以前状态的任何信息。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-323">Web servers and the pages themselves and the elements in the page do not maintain any information about the previous state of a page.</span></span> <span data-ttu-id="2b5ad-324">Web 之所以以这种方式设计，是因为维护单个请求的状态会迅速耗尽 Web 服务器的资源，而 Web 服务器通常每秒处理数千甚至数十万个请求。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-324">The web was designed this way because maintaining state for individual requests would quickly exhaust the resources of web servers, which often handle thousands, maybe even hundreds of thousands, of requests per second.</span></span>

<span data-ttu-id="2b5ad-325">因此，文本框为空的原因。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-325">So that's why the text box was empty.</span></span> <span data-ttu-id="2b5ad-326">提交页面后，ASP.NET创建了该页的新实例，并运行了代码和标记。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-326">After you submitted the page, ASP.NET created a new instance of the page and ran through the code and markup.</span></span> <span data-ttu-id="2b5ad-327">该代码中没有任何内容告诉ASP.NET在文本框中输入值。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-327">There was nothing in that code that told ASP.NET to put a value into the text box.</span></span> <span data-ttu-id="2b5ad-328">因此ASP.NET什么都没做，文本框呈现时没有值。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-328">So ASP.NET didn't do anything, and the text box was rendered without a value in it.</span></span>

<span data-ttu-id="2b5ad-329">实际上，有一个简单的方法来解决此问题。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-329">There's actually an easy way to get around this issue.</span></span> <span data-ttu-id="2b5ad-330">您在文本框中输入的流派*可在*文本框中的代码&mdash;中`Request.QueryString["searchGenre"]`使用。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-330">The genre that you entered into the text box *is* available to you in code &mdash; it's in `Request.QueryString["searchGenre"]`.</span></span>

<span data-ttu-id="2b5ad-331">更新文本框的标记，以便`value`属性从 获取`searchTerm`其值，如下所示：</span><span class="sxs-lookup"><span data-stu-id="2b5ad-331">Update the markup for the text box so that the `value` attribute gets its value from `searchTerm`, like this example:</span></span>

[!code-html[Main](form-basics/samples/sample9.html?highlight=1)]

<span data-ttu-id="2b5ad-332">在此页中`value`，还可以将属性设置为`searchTerm`变量，因为该变量还包含您输入的流派。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-332">In this page, you could have also set the `value` attribute to the `searchTerm` variable, since that variable also contains the genre you entered.</span></span> <span data-ttu-id="2b5ad-333">但是，`Request`使用 对象设置如下所示`value`的属性是完成此任务的标准方法。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-333">But using the `Request` object to set the `value` attribute as shown here is the standard way to accomplish this task.</span></span> <span data-ttu-id="2b5ad-334">（假设在某些情况下甚至想要执行此操作&mdash;，则可能需要呈现*没有*字段中值的页面。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-334">(Assuming you even want to do this &mdash; in some situations, you might want to render the page *without* values in the fields.</span></span> <span data-ttu-id="2b5ad-335">这完全取决于你的应用发生了什么。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-335">It all depends on what's going on with your app.)</span></span>

> [!NOTE]
> <span data-ttu-id="2b5ad-336">您无法"记住"用于密码的文本框的值。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-336">You can't "remember" the value of a text box that's used for passwords.</span></span> <span data-ttu-id="2b5ad-337">使用代码允许人们填写密码字段是一个安全漏洞。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-337">It would be a security hole to allow people to fill in a password field by using code.</span></span>

<span data-ttu-id="2b5ad-338">再次运行页面，输入流派，然后单击**搜索流派**。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-338">Run the page again, enter a genre, and click **Search Genre**.</span></span> <span data-ttu-id="2b5ad-339">这一次，您不仅看到搜索结果，而且文本框会记住您上次输入的内容：</span><span class="sxs-lookup"><span data-stu-id="2b5ad-339">This time not only do you see the results of the search, but the text box remembers what you entered last time:</span></span>

![显示文本框已"记住"上一个条目的页面](form-basics/_static/image5.png)

## <a name="searching-for-any-word-in-the-title"></a><span data-ttu-id="2b5ad-341">在标题中搜索任何单词</span><span class="sxs-lookup"><span data-stu-id="2b5ad-341">Searching for Any Word in the Title</span></span>

<span data-ttu-id="2b5ad-342">您现在可以搜索任何流派，但您可能还需要搜索标题。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-342">You can now search for any genre, but you might also want to search for a title.</span></span> <span data-ttu-id="2b5ad-343">搜索时很难完全正确获取标题，因此您可以搜索标题内任何位置的单词。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-343">It's hard to get a title exactly right when you search, so instead you can search for a word that appears anywhere inside a title.</span></span> <span data-ttu-id="2b5ad-344">要在 SQL 中执行此操作，`LIKE`请使用运算符和语法，如下所示：</span><span class="sxs-lookup"><span data-stu-id="2b5ad-344">To do that in SQL, you use the `LIKE` operator and syntax like the following:</span></span>

`SELECT * FROM Movies WHERE Title LIKE '%adventure%'`

<span data-ttu-id="2b5ad-345">此命令获取其标题包含"冒险"的所有影片。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-345">This command gets all the movies whose titles contain "adventure".</span></span> <span data-ttu-id="2b5ad-346">使用运算符时，`LIKE`将通配符`%`作为搜索词的一部分。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-346">When you use the `LIKE` operator, you include the wildcard character `%` as part of the search term.</span></span> <span data-ttu-id="2b5ad-347">搜索`LIKE 'adventure%'`意味着"从'冒险'开始"。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-347">The search `LIKE 'adventure%'` means "starting with 'adventure'".</span></span> <span data-ttu-id="2b5ad-348">（从技术上讲，它意味着"字符串'冒险'后跟任何东西。同样，搜索词`LIKE '%adventure'`的意思是"任何后面跟着字符串'冒险'"，这是另一种方式说"以'冒险'结束"。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-348">(Technically, it means "The string 'adventure' followed by anything.") Similarly, the search term `LIKE '%adventure'` means "anything followed by the string 'adventure'", which is another way to say "ending with 'adventure'".</span></span>

<span data-ttu-id="2b5ad-349">因此，搜索`LIKE '%adventure%'`词表示"与标题中的任何位置都具有'冒险性'"。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-349">The search term `LIKE '%adventure%'` therefore means "with 'adventure' anywhere in the title."</span></span> <span data-ttu-id="2b5ad-350">（从技术上讲，"标题中的任何内容，然后是'冒险'，然后是任何东西。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-350">(Technically, "anything in the title, followed by 'adventure', followed by anything.")</span></span>

<span data-ttu-id="2b5ad-351">在元素`<form>`中，在流派搜索的关闭`</div>`标记下方添加以下标记（就在结束`</form>`元素之前）：</span><span class="sxs-lookup"><span data-stu-id="2b5ad-351">Inside the `<form>` element, add the following markup right under the closing `</div>` tag for the genre search (just before the closing `</form>` element):</span></span>

[!code-html[Main](form-basics/samples/sample10.html)]

<span data-ttu-id="2b5ad-352">处理此搜索的代码与流派搜索的代码类似，只不过您必须组装`LIKE`搜索。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-352">The code to handle this search is similar to the code for the genre search, except that you have to assemble the `LIKE` search.</span></span> <span data-ttu-id="2b5ad-353">在页面顶部的代码块中，在流派搜索`if``if`的块之后添加此块：</span><span class="sxs-lookup"><span data-stu-id="2b5ad-353">Inside the code block at the top of the page, add this `if` block just after the `if` block for the genre search:</span></span>

[!code-csharp[Main](form-basics/samples/sample11.cs)]

<span data-ttu-id="2b5ad-354">此代码使用之前看到的相同逻辑，只不过搜索使用`LIKE`运算符，并且代码在搜索词之前和之后放置""。`%`</span><span class="sxs-lookup"><span data-stu-id="2b5ad-354">This code uses the same logic you saw earlier, except that the search uses a `LIKE` operator and the code puts "`%`" before and after the search term.</span></span>

<span data-ttu-id="2b5ad-355">请注意如何轻松地向页面添加另一个搜索。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-355">Notice how it was easy to add another search to the page.</span></span> <span data-ttu-id="2b5ad-356">你所要做的就是：</span><span class="sxs-lookup"><span data-stu-id="2b5ad-356">All you had to do was:</span></span>

- <span data-ttu-id="2b5ad-357">创建测试`if`的块以查看相关搜索框是否具有值。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-357">Create an `if` block that tested to see whether the relevant search box had a value.</span></span>
- <span data-ttu-id="2b5ad-358">将`selectCommand`变量设置为新的 SQL 语句。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-358">Set the `selectCommand` variable to a new SQL statement.</span></span>
- <span data-ttu-id="2b5ad-359">将`searchTerm`变量设置为要传递给查询的值。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-359">Set the `searchTerm` variable to the value to pass to the query.</span></span>

<span data-ttu-id="2b5ad-360">下面是完整的代码块，其中包含标题搜索的新逻辑：</span><span class="sxs-lookup"><span data-stu-id="2b5ad-360">Here's the complete code block, which contains the new logic for a title search:</span></span>

[!code-cshtml[Main](form-basics/samples/sample12.cshtml)]

<span data-ttu-id="2b5ad-361">下面总结了此代码的用途：</span><span class="sxs-lookup"><span data-stu-id="2b5ad-361">Here's a summary of what this code does:</span></span>

- <span data-ttu-id="2b5ad-362">变量`searchTerm`和`selectCommand`在顶部初始化。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-362">The variables `searchTerm` and `selectCommand` are initialized at the top.</span></span> <span data-ttu-id="2b5ad-363">您将根据用户在页面中所做的操作将这些变量设置为相应的搜索词（如果有）和相应的 SQL 命令。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-363">You're going to set these variables to the appropriate search term (if any) and appropriate SQL command based on what the user does in the page.</span></span> <span data-ttu-id="2b5ad-364">默认搜索是从数据库中获取所有影片的简单示例。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-364">The default search is the simple case of getting all the movies from the database.</span></span>
- <span data-ttu-id="2b5ad-365">在 和`searchGenre``searchTitle`的测试中，代码将`searchTerm`设置到要搜索的值。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-365">In the tests for `searchGenre` and `searchTitle`, the code sets `searchTerm` to the value you want to search for.</span></span> <span data-ttu-id="2b5ad-366">这些代码块还设置为`selectCommand`该搜索的相应 SQL 命令。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-366">Those code blocks also set `selectCommand` to an appropriate SQL command for that search.</span></span>
- <span data-ttu-id="2b5ad-367">该方法`db.Query`仅调用一次，使用 中`selectedCommand`的任何 SQL 命令和 中`searchTerm`的任何值。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-367">The `db.Query` method is invoked only once, using whatever SQL command is in `selectedCommand` and whatever value is in `searchTerm`.</span></span> <span data-ttu-id="2b5ad-368">如果没有搜索词（没有流派，没有标题词），则 值`searchTerm`为空字符串。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-368">If there is no search term (no genre and no title word), the value of `searchTerm` is an empty string.</span></span> <span data-ttu-id="2b5ad-369">但是，这并不重要，因为在这种情况下，查询不需要参数。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-369">However, that doesn't matter, because in that case the query doesn't require a parameter.</span></span>

## <a name="testing-the-title-search-feature"></a><span data-ttu-id="2b5ad-370">测试标题搜索功能</span><span class="sxs-lookup"><span data-stu-id="2b5ad-370">Testing the Title Search Feature</span></span>

<span data-ttu-id="2b5ad-371">现在，您可以测试已完成的搜索页面。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-371">Now you can test your completed search page.</span></span> <span data-ttu-id="2b5ad-372">运行*电影.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="2b5ad-372">Run *Movies.cshtml*.</span></span>

<span data-ttu-id="2b5ad-373">输入流派，然后单击**搜索流派**。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-373">Enter a genre and click **Search Genre**.</span></span> <span data-ttu-id="2b5ad-374">网格显示该流派的电影，就像以前一样。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-374">The grid displays movies of that genre, like before.</span></span>

<span data-ttu-id="2b5ad-375">输入标题字，然后单击 **"搜索标题**"。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-375">Enter a title word and click **Search Title**.</span></span> <span data-ttu-id="2b5ad-376">网格显示标题中具有该单词的电影。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-376">The grid displays movies that have that word in the title.</span></span>

![在标题中搜索"The"后的电影页面列表](form-basics/_static/image6.png)

<span data-ttu-id="2b5ad-378">将两个文本框留空，然后单击任一按钮。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-378">Leave both text boxes blank and click either button.</span></span> <span data-ttu-id="2b5ad-379">网格显示所有影片。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-379">The grid displays all the movies.</span></span>

## <a name="combining-the-queries"></a><span data-ttu-id="2b5ad-380">组合查询</span><span class="sxs-lookup"><span data-stu-id="2b5ad-380">Combining the Queries</span></span>

<span data-ttu-id="2b5ad-381">您可能会注意到，您可以执行的搜索是独占的。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-381">You might notice that the searches you can perform are exclusive.</span></span> <span data-ttu-id="2b5ad-382">不能同时搜索标题和流派，即使两个搜索框中都有值。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-382">You can't search the title and the genre at the same time, even if both search boxes have values in them.</span></span> <span data-ttu-id="2b5ad-383">例如，您无法搜索标题包含"冒险"的所有动作影片。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-383">For example, you can't search for all action movies whose title contains "Adventure".</span></span> <span data-ttu-id="2b5ad-384">（现在对页面进行编码时，如果同时输入流派和标题的值，则标题搜索将优先。要创建结合条件的搜索，必须创建具有如下语法的 SQL 查询：</span><span class="sxs-lookup"><span data-stu-id="2b5ad-384">(As the page is coded now, if you enter values for both genre and title, the title search gets precedence.) To create a search that combines the conditions, you would have to create a SQL query that has syntax like the following:</span></span>

`SELECT * FROM Movies WHERE Genre = @0 AND Title LIKE @1`

<span data-ttu-id="2b5ad-385">您必须使用如下语句来运行查询（大致而言）：</span><span class="sxs-lookup"><span data-stu-id="2b5ad-385">And you'd have to run the query by using a statement like the following (roughly speaking):</span></span>

`var selectedData = db.Query(selectCommand, searchGenre, searchTitle);`

<span data-ttu-id="2b5ad-386">如您所见，创建逻辑以允许搜索条件的许多排列，可能会涉及一些内容。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-386">Creating logic to allow many permutations of search criteria can get a bit involved, as you can see.</span></span> <span data-ttu-id="2b5ad-387">因此，我们将在这里停留。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-387">Therefore, we'll stop here.</span></span>

## <a name="coming-up-next"></a><span data-ttu-id="2b5ad-388">下一步</span><span class="sxs-lookup"><span data-stu-id="2b5ad-388">Coming Up Next</span></span>

<span data-ttu-id="2b5ad-389">在下一教程中，您将创建一个页面，该页面使用窗体允许用户向数据库添加影片。</span><span class="sxs-lookup"><span data-stu-id="2b5ad-389">In the next tutorial, you'll create a page that uses a form to let users add movies to the database.</span></span>

## <a name="complete-listing-for-movie-page-updated-with-search"></a><span data-ttu-id="2b5ad-390">影片页面的完整列表（通过搜索更新）</span><span class="sxs-lookup"><span data-stu-id="2b5ad-390">Complete Listing for Movie Page (Updated with Search)</span></span>

[!code-cshtml[Main](form-basics/samples/sample13.cshtml)]

## <a name="additional-resources"></a><span data-ttu-id="2b5ad-391">其他资源</span><span class="sxs-lookup"><span data-stu-id="2b5ad-391">Additional Resources</span></span>

- [<span data-ttu-id="2b5ad-392">使用 Razor 语法进行 ASP.NET Web 编程简介</span><span class="sxs-lookup"><span data-stu-id="2b5ad-392">Introduction to ASP.NET Web Programming Using the Razor Syntax</span></span>](https://go.microsoft.com/fwlink/?LinkID=202890)
- <span data-ttu-id="2b5ad-393">W3学校网站上的[SQL WHERE 条款](http://www.w3schools.com/sql/sql_where.asp)</span><span class="sxs-lookup"><span data-stu-id="2b5ad-393">[SQL WHERE Clause](http://www.w3schools.com/sql/sql_where.asp) on the W3Schools site</span></span>
- <span data-ttu-id="2b5ad-394">[方法定义](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html)W3C 站点上的文章</span><span class="sxs-lookup"><span data-stu-id="2b5ad-394">[Method Definitions](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html) article on the W3C site</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="2b5ad-395">[上一页](displaying-data.md)
> [下一页](entering-data.md)</span><span class="sxs-lookup"><span data-stu-id="2b5ad-395">[Previous](displaying-data.md)
[Next](entering-data.md)</span></span>

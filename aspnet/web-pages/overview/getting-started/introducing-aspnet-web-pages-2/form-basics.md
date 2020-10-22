---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/form-basics
title: 介绍 ASP.NET 网页-HTML 窗体基础知识 |Microsoft Docs
author: Rick-Anderson
description: 本教程介绍了如何创建输入窗体的基础知识，以及如何在使用 ASP.NET 网页 (Razor) 时处理用户的输入。 现在，你 .。。
ms.author: riande
ms.date: 05/28/2015
ms.assetid: 81ed82bf-b940-44f1-b94a-555d0cb7cc98
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/form-basics
msc.type: authoredcontent
ms.openlocfilehash: f57661077ec3bb13f3d4ec41b130bda4d2fb9070
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345455"
---
# <a name="introducing-aspnet-web-pages---html-form-basics"></a><span data-ttu-id="9801f-104">介绍 ASP.NET 网页-HTML 窗体基础知识</span><span class="sxs-lookup"><span data-stu-id="9801f-104">Introducing ASP.NET Web Pages - HTML Form Basics</span></span>

<span data-ttu-id="9801f-105"> 作者 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="9801f-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="9801f-106">本教程介绍了如何创建输入窗体的基础知识，以及如何在使用 ASP.NET 网页 (Razor) 时处理用户的输入。</span><span class="sxs-lookup"><span data-stu-id="9801f-106">This tutorial shows you the basics of how to create an input form and how to handle the user's input when you use ASP.NET Web Pages (Razor).</span></span> <span data-ttu-id="9801f-107">现在您已经有了一个数据库，您将使用您的表单技能让用户在数据库中找到特定的电影。</span><span class="sxs-lookup"><span data-stu-id="9801f-107">And now that you've got a database, you'll use your form skills to let users find specific movies in the database.</span></span> <span data-ttu-id="9801f-108">它假定您已完成了 [使用 ASP.NET 网页显示数据的简介](/aspnet/web-pages/overview/getting-started/introducing-aspnet-web-pages-2/displaying-data)。</span><span class="sxs-lookup"><span data-stu-id="9801f-108">It assumes you have completed the series through [Introduction to Displaying Data Using ASP.NET Web Pages](/aspnet/web-pages/overview/getting-started/introducing-aspnet-web-pages-2/displaying-data).</span></span>
> 
> <span data-ttu-id="9801f-109">学习内容：</span><span class="sxs-lookup"><span data-stu-id="9801f-109">What you'll learn:</span></span>
> 
> - <span data-ttu-id="9801f-110">如何使用标准 HTML 元素创建窗体。</span><span class="sxs-lookup"><span data-stu-id="9801f-110">How to create a form by using standard HTML elements.</span></span>
> - <span data-ttu-id="9801f-111">如何读取窗体中的用户输入。</span><span class="sxs-lookup"><span data-stu-id="9801f-111">How to read the user's input in a form.</span></span>
> - <span data-ttu-id="9801f-112">如何创建可通过使用用户提供的搜索词来有选择地获取数据的 SQL 查询。</span><span class="sxs-lookup"><span data-stu-id="9801f-112">How to create a SQL query that selectively gets data by using a search term that the user supplies.</span></span>
> - <span data-ttu-id="9801f-113">如何在页中包含用户输入的内容。</span><span class="sxs-lookup"><span data-stu-id="9801f-113">How to have fields in the page "remember" what the user entered.</span></span>
>   
> 
> <span data-ttu-id="9801f-114">介绍的功能/技术：</span><span class="sxs-lookup"><span data-stu-id="9801f-114">Features/technologies discussed:</span></span>
> 
> - <span data-ttu-id="9801f-115">`Request` 对象。</span><span class="sxs-lookup"><span data-stu-id="9801f-115">The `Request` object.</span></span>
> - <span data-ttu-id="9801f-116">SQL `Where` 子句。</span><span class="sxs-lookup"><span data-stu-id="9801f-116">The SQL `Where` clause.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="9801f-117">所需操作</span><span class="sxs-lookup"><span data-stu-id="9801f-117">What You'll Build</span></span>

<span data-ttu-id="9801f-118">在上一教程中，您创建了一个数据库，向其中添加了数据，然后使用该 `WebGrid` 帮助器来显示数据。</span><span class="sxs-lookup"><span data-stu-id="9801f-118">In the previous tutorial, you created a database, added data to it, and then used the `WebGrid` helper to display the data.</span></span> <span data-ttu-id="9801f-119">在本教程中，您将添加一个搜索框，您可以在其中查找特定流派的电影或标题包含您输入的任何单词的电影。</span><span class="sxs-lookup"><span data-stu-id="9801f-119">In this tutorial, you'll add a search box that lets you find movies of a specific genre or whose title contains whatever word you enter.</span></span> <span data-ttu-id="9801f-120"> (例如，你可以查找流派为 "Action" 或标题包含 "Harry" 或 "艾德" 的所有电影。) </span><span class="sxs-lookup"><span data-stu-id="9801f-120">(For example, you'll be able to find all movies whose genre is "Action" or whose title contains "Harry" or "Adventure.")</span></span>

<span data-ttu-id="9801f-121">完成本教程后，会看到如下所示的页面：</span><span class="sxs-lookup"><span data-stu-id="9801f-121">When you're done with this tutorial, you'll have a page like this one:</span></span>

![具有流派和标题搜索的电影页面](form-basics/_static/image1.png)

<span data-ttu-id="9801f-123">页面的列表部分与上一教程网格中的部分相同 &mdash; 。</span><span class="sxs-lookup"><span data-stu-id="9801f-123">The listing part of the page is the same as in the last tutorial &mdash; a grid.</span></span> <span data-ttu-id="9801f-124">不同之处在于网格只显示您搜索的影片。</span><span class="sxs-lookup"><span data-stu-id="9801f-124">The difference will be that the grid will show only the movies that you searched for.</span></span>

## <a name="about-html-forms"></a><span data-ttu-id="9801f-125">关于 HTML 窗体</span><span class="sxs-lookup"><span data-stu-id="9801f-125">About HTML Forms</span></span>

<span data-ttu-id="9801f-126"> (如果你获得了创建 HTML 表单以及与之间的差异的经验 `GET` `POST` ，则可以跳过此部分。 ) </span><span class="sxs-lookup"><span data-stu-id="9801f-126">(If you've got experience with creating HTML forms and with the difference between `GET` and `POST`, you can skip this section.)</span></span>

<span data-ttu-id="9801f-127">窗体具有用户输入元素 &mdash; 文本框、按钮、单选按钮、复选框、下拉列表等。</span><span class="sxs-lookup"><span data-stu-id="9801f-127">A form has user input elements &mdash; text boxes, buttons, radio buttons, check boxes, drop-down lists, and so on.</span></span> <span data-ttu-id="9801f-128">用户填写这些控件或进行选择，然后通过单击按钮提交窗体。</span><span class="sxs-lookup"><span data-stu-id="9801f-128">Users fill in these controls or make selections and then submit the form by clicking a button.</span></span>

<span data-ttu-id="9801f-129">下面的示例演示了窗体的基本 HTML 语法：</span><span class="sxs-lookup"><span data-stu-id="9801f-129">The basic HTML syntax of a form is illustrated by this example:</span></span>

[!code-html[Main](form-basics/samples/sample1.html)]

<span data-ttu-id="9801f-130">当此标记在页中运行时，它将创建一个简单的窗体，如下图所示：</span><span class="sxs-lookup"><span data-stu-id="9801f-130">When this markup runs in a page, it creates a simple form that looks like this illustration:</span></span>

![在浏览器中呈现的基本 HTML 窗体](form-basics/_static/image2.png)

<span data-ttu-id="9801f-132">`<form>`元素包含要提交的 HTML 元素。</span><span class="sxs-lookup"><span data-stu-id="9801f-132">The `<form>` element encloses HTML elements to be submitted.</span></span> <span data-ttu-id="9801f-133"> (一种简单的错误，就是将元素添加到页面，然后忘记将它们放在 `<form>` 元素中。</span><span class="sxs-lookup"><span data-stu-id="9801f-133">(An easy mistake to make is to add elements to the page but then forget to put them inside a `<form>` element.</span></span> <span data-ttu-id="9801f-134">在这种情况下，不会提交任何内容。 ) `method` 特性会告诉浏览器如何提交用户输入。</span><span class="sxs-lookup"><span data-stu-id="9801f-134">In that case, nothing is submitted.) The `method` attribute tells the browser how to submit the user input.</span></span> <span data-ttu-id="9801f-135">`post`如果要在服务器上执行更新，或者 `get` 只是从服务器中提取数据，请将此设置为。</span><span class="sxs-lookup"><span data-stu-id="9801f-135">You set this to `post` if you're performing an update on the server or to `get` if you're just fetching data from the server.</span></span>

<a id="GET,_POST,_and_HTTP_Verb_Safety"></a>

> [!TIP] 
> 
> <span data-ttu-id="9801f-136">**GET、POST 和 HTTP Verb 安全**</span><span class="sxs-lookup"><span data-stu-id="9801f-136">**GET, POST, and HTTP Verb Safety**</span></span>
> 
> <span data-ttu-id="9801f-137">HTTP （浏览器和服务器用于交换信息的协议）在基本操作中非常简单。</span><span class="sxs-lookup"><span data-stu-id="9801f-137">HTTP, the protocol that browsers and servers use to exchange information, is remarkably simple in its basic operations.</span></span> <span data-ttu-id="9801f-138">浏览器仅使用几个谓词来向服务器发出请求。</span><span class="sxs-lookup"><span data-stu-id="9801f-138">Browsers use only a few verbs to make requests to servers.</span></span> <span data-ttu-id="9801f-139">编写 web 代码时，了解这些谓词以及浏览器和服务器如何使用它们都很有帮助。</span><span class="sxs-lookup"><span data-stu-id="9801f-139">When you write code for the web, it's helpful to understand these verbs and how the browser and server use them.</span></span> <span data-ttu-id="9801f-140">到目前为止，最常用的动词如下：</span><span class="sxs-lookup"><span data-stu-id="9801f-140">Far and away the most commonly used verbs are these:</span></span>
> 
> - <span data-ttu-id="9801f-141">`GET`.</span><span class="sxs-lookup"><span data-stu-id="9801f-141">`GET`.</span></span> <span data-ttu-id="9801f-142">浏览器使用此谓词从服务器提取内容。</span><span class="sxs-lookup"><span data-stu-id="9801f-142">The browser uses this verb to fetch something from the server.</span></span> <span data-ttu-id="9801f-143">例如，当你在浏览器中键入 URL 时，浏览器将执行 `GET` 操作来请求所需的页面。</span><span class="sxs-lookup"><span data-stu-id="9801f-143">For example, when you type a URL into your browser, the browser performs a `GET` operation to request the page you want.</span></span> <span data-ttu-id="9801f-144">如果页面包含图形，浏览器会执行其他 `GET` 操作来获取图像。</span><span class="sxs-lookup"><span data-stu-id="9801f-144">If the page includes graphics, the browser performs additional `GET` operations to get the images.</span></span> <span data-ttu-id="9801f-145">如果 `GET` 操作必须将信息传递给服务器，则会将信息作为 URL 的一部分传递到查询字符串中。</span><span class="sxs-lookup"><span data-stu-id="9801f-145">If the `GET` operation has to pass information to the server, the information is passed as part of the URL in the query string.</span></span>
> - <span data-ttu-id="9801f-146">`POST`.</span><span class="sxs-lookup"><span data-stu-id="9801f-146">`POST`.</span></span> <span data-ttu-id="9801f-147">浏览器发送请求，以便 `POST` 提交要在服务器上添加或更改的数据。</span><span class="sxs-lookup"><span data-stu-id="9801f-147">The browser sends a `POST` request in order to submit data to be added or changed on the server.</span></span> <span data-ttu-id="9801f-148">例如， `POST` 谓词用于在数据库中创建记录或更改现有记录。</span><span class="sxs-lookup"><span data-stu-id="9801f-148">For example, the `POST` verb is used to create records in a database or change existing ones.</span></span> <span data-ttu-id="9801f-149">大多数情况下，当你填写表单并单击 "提交" 按钮时，浏览器将执行 `POST` 操作。</span><span class="sxs-lookup"><span data-stu-id="9801f-149">Most of the time, when you fill in a form and click the submit button, the browser performs a `POST` operation.</span></span> <span data-ttu-id="9801f-150">在 `POST` 操作中，传递给服务器的数据在页面的正文中。</span><span class="sxs-lookup"><span data-stu-id="9801f-150">In a `POST` operation, the data being passed to the server is in the body of the page.</span></span>
> 
> <span data-ttu-id="9801f-151">这些谓词之间的一个重要区别在于， `GET` 操作不应更改服务器上的任何内容，或者将其放在更抽象的方法中，操作不 `GET` 会导致服务器上的状态发生更改。</span><span class="sxs-lookup"><span data-stu-id="9801f-151">An important distinction between these verbs is that a `GET` operation is not supposed to change anything on the server — or to put it in a slightly more abstract way, a `GET` operation does not result in a change in state on the server.</span></span> <span data-ttu-id="9801f-152">您可以根据 `GET` 自己的需要多次对相同的资源执行操作，这些资源不会更改。</span><span class="sxs-lookup"><span data-stu-id="9801f-152">You can perform a `GET` operation on the same resources as many times as you like, and those resources don't change.</span></span> <span data-ttu-id="9801f-153"> (`GET` 操作通常被称为 "安全"，或者使用技术术语，则是 *幂等*的 ) 。相反，在 `POST` 每次执行操作时，请求都会在服务器上更改某些内容。</span><span class="sxs-lookup"><span data-stu-id="9801f-153">(A `GET` operation is often said to be "safe," or to use a technical term, is *idempotent*.) In contrast, of course, a `POST` request changes something on the server each time you perform the operation.</span></span>
> 
> <span data-ttu-id="9801f-154">下面两个示例将帮助说明这种区别。</span><span class="sxs-lookup"><span data-stu-id="9801f-154">Two examples will help illustrate this distinction.</span></span> <span data-ttu-id="9801f-155">使用必应或 Google 等引擎执行搜索时，需要填写包含一个文本框的窗体，然后单击 "搜索" 按钮。</span><span class="sxs-lookup"><span data-stu-id="9801f-155">When you perform a search using an engine like Bing or Google, you fill in a form that consists of one text box, and then you click the search button.</span></span> <span data-ttu-id="9801f-156">浏览器执行一个 `GET` 操作，其值输入到作为 URL 的一部分传递的框中。</span><span class="sxs-lookup"><span data-stu-id="9801f-156">The browser performs a `GET` operation, with the value you entered into the box passed as part of the URL.</span></span> <span data-ttu-id="9801f-157">`GET`对此类型的窗体使用操作非常好，因为搜索操作不会更改服务器上的任何资源，而只会提取信息。</span><span class="sxs-lookup"><span data-stu-id="9801f-157">Using a `GET` operation for this type of form is fine, because a search operation doesn't change any resources on the server, it just fetches information.</span></span>
> 
> <span data-ttu-id="9801f-158">现在，请考虑订购联机内容的过程。</span><span class="sxs-lookup"><span data-stu-id="9801f-158">Now consider the process of ordering something online.</span></span> <span data-ttu-id="9801f-159">填写订单详细信息，然后单击 "提交" 按钮。</span><span class="sxs-lookup"><span data-stu-id="9801f-159">You fill in the order details and then click the submit button.</span></span> <span data-ttu-id="9801f-160">此操作将是一个 `POST` 请求，因为该操作将导致服务器上发生更改，如新订单记录、帐户信息更改以及可能有许多其他更改。</span><span class="sxs-lookup"><span data-stu-id="9801f-160">This operation will be a `POST` request, because the operation will result in changes on the server, such as a new order record, a change in your account information, and perhaps many other changes.</span></span> <span data-ttu-id="9801f-161">与操作不同的是 `GET` ，您不能重复您的 `POST` 请求。如果您这样做，每次重新提交请求时，都将在服务器上生成新的订单。</span><span class="sxs-lookup"><span data-stu-id="9801f-161">Unlike the `GET` operation, you cannot repeat your `POST` request — if you did, each time you resubmitted the request, you'd generate a new order on the server.</span></span> <span data-ttu-id="9801f-162"> (，在这种情况下，网站通常会警告您不要多次单击 "提交" 按钮，否则将禁用 "提交" 按钮，以便不会意外地重新提交窗体。 ) </span><span class="sxs-lookup"><span data-stu-id="9801f-162">(In cases like this, websites will often warn you not to click a submit button more than once, or will disable the submit button so that you don't resubmit the form accidentally.)</span></span>
> 
> <span data-ttu-id="9801f-163">在本教程的过程中，您将使用 `GET` 操作和 `POST` 操作来处理 HTML 窗体。</span><span class="sxs-lookup"><span data-stu-id="9801f-163">In the course of this tutorial, you'll use both a `GET` operation and a `POST` operation to work with HTML forms.</span></span> <span data-ttu-id="9801f-164">在每种情况下，我们都将介绍你使用的动词是合适的。</span><span class="sxs-lookup"><span data-stu-id="9801f-164">We'll explain in each case why the verb you use is the appropriate one.</span></span>
> 
> <span data-ttu-id="9801f-165"> (若要详细了解 HTTP 谓词，请参阅 W3C 网站上的 [方法定义](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html) 一文。 ) </span><span class="sxs-lookup"><span data-stu-id="9801f-165">(To learn more about HTTP verbs, see the [Method Definitions](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html) article on the W3C site.)</span></span>

<span data-ttu-id="9801f-166">大多数用户输入元素都是 HTML `<input>` 元素。</span><span class="sxs-lookup"><span data-stu-id="9801f-166">Most user input elements are HTML `<input>` elements.</span></span> <span data-ttu-id="9801f-167">它们看起来就像， `<input type="type" name="name">,` 其中 *类型* 指示所需的用户输入控件的类型。</span><span class="sxs-lookup"><span data-stu-id="9801f-167">They look like `<input type="type" name="name">,` where *type* indicates the kind of user input control you want.</span></span> <span data-ttu-id="9801f-168">这些元素是通用元素：</span><span class="sxs-lookup"><span data-stu-id="9801f-168">These elements are the common ones:</span></span>

- <span data-ttu-id="9801f-169">文本框： `<input type="text">`</span><span class="sxs-lookup"><span data-stu-id="9801f-169">Text box: `<input type="text">`</span></span>
- <span data-ttu-id="9801f-170">复选框： `<input type="check">`</span><span class="sxs-lookup"><span data-stu-id="9801f-170">Check box: `<input type="check">`</span></span>
- <span data-ttu-id="9801f-171">单选按钮： `<input type="radio">`</span><span class="sxs-lookup"><span data-stu-id="9801f-171">Radio button: `<input type="radio">`</span></span>
- <span data-ttu-id="9801f-172">鼠标 `<input type="button">`</span><span class="sxs-lookup"><span data-stu-id="9801f-172">Button: `<input type="button">`</span></span>
- <span data-ttu-id="9801f-173">提交按钮： `<input type="submit">`</span><span class="sxs-lookup"><span data-stu-id="9801f-173">Submit button: `<input type="submit">`</span></span>

<span data-ttu-id="9801f-174">你还可以使用 `<textarea>` 元素来创建多行文本框和 `<select>` 元素，以创建下拉列表或可滚动列表。</span><span class="sxs-lookup"><span data-stu-id="9801f-174">You can also use the `<textarea>` element to create a multiline text box and the `<select>` element to create a drop-down list or scrollable list.</span></span> <span data-ttu-id="9801f-175"> (有关 HTML 窗体元素的详细信息，请参阅 W3Schools 站点上的 [Html 窗体和输入](http://www.w3schools.com/html/html_forms.asp) ) </span><span class="sxs-lookup"><span data-stu-id="9801f-175">(For more about HTML form elements, see [HTML Forms and Input](http://www.w3schools.com/html/html_forms.asp) on the W3Schools site.)</span></span>

<span data-ttu-id="9801f-176">`name`特性非常重要，因为该名称是稍后会获得元素值的方式，正如你将很快看到的一样。</span><span class="sxs-lookup"><span data-stu-id="9801f-176">The `name` attribute is very important, because the name is how you'll get the value of the element later, as you'll see shortly.</span></span>

<span data-ttu-id="9801f-177">有趣的部分是页面开发人员处理用户输入的内容。</span><span class="sxs-lookup"><span data-stu-id="9801f-177">The interesting part is what you, the page developer, do with the user's input.</span></span> <span data-ttu-id="9801f-178">没有与这些元素关联的内置行为。</span><span class="sxs-lookup"><span data-stu-id="9801f-178">There's no built-in behavior associated with these elements.</span></span> <span data-ttu-id="9801f-179">相反，您必须获取用户输入或选择的值，并对其执行一些操作。</span><span class="sxs-lookup"><span data-stu-id="9801f-179">Instead, you have to get the values that the user has entered or selected and do something with them.</span></span> <span data-ttu-id="9801f-180">这就是你在本教程中学习的内容。</span><span class="sxs-lookup"><span data-stu-id="9801f-180">That's what you'll learn in this tutorial.</span></span>

> [!TIP] 
> 
> <span data-ttu-id="9801f-181">**HTML5 和输入窗体**</span><span class="sxs-lookup"><span data-stu-id="9801f-181">**HTML5 and Input Forms**</span></span>
> 
> <span data-ttu-id="9801f-182">如您所知，HTML 正在转换，最新版本 (HTML5) 包括对用户输入信息的更直观方式的支持。</span><span class="sxs-lookup"><span data-stu-id="9801f-182">As you might know, HTML is in transition and the latest version (HTML5) includes support for more intuitive ways for users to enter information.</span></span> <span data-ttu-id="9801f-183">例如，在 HTML5 中，您 (页面开发人员) 可以告诉页面您希望用户输入日期。</span><span class="sxs-lookup"><span data-stu-id="9801f-183">For example, in HTML5, you (the page developer) can tell the page that you want the user to enter a date.</span></span> <span data-ttu-id="9801f-184">然后，浏览器可以自动显示日历，而不需要用户手动输入日期。</span><span class="sxs-lookup"><span data-stu-id="9801f-184">The browser can then automatically display a calendar rather than requiring the user to enter a date manually.</span></span> <span data-ttu-id="9801f-185">不过，HTML5 是新的，但并非所有浏览器都支持此项。</span><span class="sxs-lookup"><span data-stu-id="9801f-185">However, HTML5 is new and is not supported in all browsers yet.</span></span>
> 
> <span data-ttu-id="9801f-186">ASP.NET 网页支持 HTML5 输入用户浏览器的范围。</span><span class="sxs-lookup"><span data-stu-id="9801f-186">ASP.NET Web Pages supports HTML5 input to the extent that the user's browser does.</span></span> <span data-ttu-id="9801f-187">若要了解 HTML5 中元素的新属性 `<input>` ，请参阅 W3Schools 站点上的 [HTML &lt; 输入 &gt; 类型属性](http://www.w3schools.com/html/html_form_input_types.asp) 。</span><span class="sxs-lookup"><span data-stu-id="9801f-187">For an idea of the new attributes for the `<input>` element in HTML5, see [HTML &lt;input&gt; type Attribute](http://www.w3schools.com/html/html_form_input_types.asp) on the W3Schools site.</span></span>

## <a name="creating-the-form"></a><span data-ttu-id="9801f-188">创建窗体</span><span class="sxs-lookup"><span data-stu-id="9801f-188">Creating the Form</span></span>

<span data-ttu-id="9801f-189">在 WebMatrix 的 " **文件** " 工作区中，打开 " *电影. cshtml* " 页。</span><span class="sxs-lookup"><span data-stu-id="9801f-189">In WebMatrix, in the **Files** workspace, open the *Movies.cshtml* page.</span></span>

<span data-ttu-id="9801f-190">在调用的结束标记后 `</h1>` 和开始 `<div>` 标记之前 `grid.GetHtml` ，添加以下标记：</span><span class="sxs-lookup"><span data-stu-id="9801f-190">After the closing `</h1>` tag and before the opening `<div>` tag of the `grid.GetHtml` call, add the following markup:</span></span>

[!code-html[Main](form-basics/samples/sample2.html)]

<span data-ttu-id="9801f-191">此标记创建一个窗体，该窗体具有名为的文本框 `searchGenre` 和一个提交按钮。</span><span class="sxs-lookup"><span data-stu-id="9801f-191">This markup creates a form that has a text box named `searchGenre` and a submit button.</span></span> <span data-ttu-id="9801f-192">文本框和提交按钮包含在 `<form>` 其 `method` 特性设置为的元素中 `get` 。</span><span class="sxs-lookup"><span data-stu-id="9801f-192">The text box and submit button are enclosed in a `<form>` element whose `method` attribute is set to `get`.</span></span> <span data-ttu-id="9801f-193"> (请记住，如果不将文本框和提交按钮放入 `<form>` 元素，则在单击该按钮时，不会提交任何内容。 ) 你在 `GET` 此处使用谓词，因为你要创建的窗体不会在服务器上进行任何更改，而只是导致搜索。</span><span class="sxs-lookup"><span data-stu-id="9801f-193">(Remember that if you don't put the text box and submit button inside a `<form>` element, nothing will be submitted when you click the button.) You use the `GET` verb here because you're creating a form that does not make any changes on the server — it just results in a search.</span></span> <span data-ttu-id="9801f-194"> (上一教程中，你使用了一种 `post` 方法，即如何向服务器提交更改。</span><span class="sxs-lookup"><span data-stu-id="9801f-194">(In the previous tutorial, you used a `post` method, which is how you submit changes to the server.</span></span> <span data-ttu-id="9801f-195">你将在下一教程中看到该。 ) </span><span class="sxs-lookup"><span data-stu-id="9801f-195">You'll see that in the next tutorial again.)</span></span>

<span data-ttu-id="9801f-196">运行页面。</span><span class="sxs-lookup"><span data-stu-id="9801f-196">Run the page.</span></span> <span data-ttu-id="9801f-197">虽然您没有为窗体定义任何行为，但您可以看到它的外观：</span><span class="sxs-lookup"><span data-stu-id="9801f-197">Although you haven't defined any behavior for the form, you can see what it looks like:</span></span>

![用于流派的搜索框的电影页面](form-basics/_static/image3.png)

<span data-ttu-id="9801f-199">在文本框中输入一个值，如 "喜剧"。</span><span class="sxs-lookup"><span data-stu-id="9801f-199">Enter a value into the text box, like "Comedy."</span></span> <span data-ttu-id="9801f-200">然后单击 " **搜索流派**"。</span><span class="sxs-lookup"><span data-stu-id="9801f-200">Then click **Search Genre**.</span></span>

<span data-ttu-id="9801f-201">记下页面的 URL。</span><span class="sxs-lookup"><span data-stu-id="9801f-201">Take note of the URL of the page.</span></span> <span data-ttu-id="9801f-202">由于您将 `<form>` 元素的 `method` 属性设置为 `get` ，因此您输入的值现在是 URL 中的查询字符串的一部分，如下所示：</span><span class="sxs-lookup"><span data-stu-id="9801f-202">Because you set the `<form>` element's `method` attribute to `get`, the value you entered is now part of the query string in the URL, like this:</span></span>

`http://localhost:45661/Movies.cshtml?searchGenre=Comedy`

## <a name="reading-form-values"></a><span data-ttu-id="9801f-203">读取窗体值</span><span class="sxs-lookup"><span data-stu-id="9801f-203">Reading Form Values</span></span>

<span data-ttu-id="9801f-204">该页已经包含一些可获取数据库数据的代码，并在网格中显示结果。</span><span class="sxs-lookup"><span data-stu-id="9801f-204">The page already contains some code that gets database data and displays the results in a grid.</span></span> <span data-ttu-id="9801f-205">现在，你必须添加一些代码来读取文本框的值，以便可以运行包含搜索词的 SQL 查询。</span><span class="sxs-lookup"><span data-stu-id="9801f-205">Now you have to add some code that reads the value of the text box so you can run a SQL query that includes the search term.</span></span>

<span data-ttu-id="9801f-206">由于您将窗体的方法设置为 `get` ，因此您可以使用如下代码来读取在文本框中输入的值：</span><span class="sxs-lookup"><span data-stu-id="9801f-206">Because you set the form's method to `get`, you can read the value that was entered into the text box by using code like the following:</span></span>

`var searchTerm = Request.QueryString["searchGenre"];`

<span data-ttu-id="9801f-207">对象 `Request.QueryString` (对象的 `QueryString` 属性 `Request`) 包含作为操作的一部分提交的元素的值 `GET` 。</span><span class="sxs-lookup"><span data-stu-id="9801f-207">The `Request.QueryString` object (the `QueryString` property of the `Request` object) includes the values of elements that were submitted as part of the `GET` operation.</span></span> <span data-ttu-id="9801f-208">`Request.QueryString`属性包含在表单中提交的值 (列表) 的*集合*。</span><span class="sxs-lookup"><span data-stu-id="9801f-208">The `Request.QueryString` property contains a *collection* (a list) of the values that are submitted in the form.</span></span> <span data-ttu-id="9801f-209">若要获取任何单个值，请指定所需的元素的名称。</span><span class="sxs-lookup"><span data-stu-id="9801f-209">To get any individual value, you specify the name of the element that you want.</span></span> <span data-ttu-id="9801f-210">这就是为什么必须 `name` 在 `<input>` 元素 (`searchTerm`) 创建文本框的属性。</span><span class="sxs-lookup"><span data-stu-id="9801f-210">That's why you have to have a `name` attribute on the `<input>` element (`searchTerm`) that creates the text box.</span></span> <span data-ttu-id="9801f-211"> (有关对象的详细信息 `Request` ，请参阅后面的 [边栏](#BKMK_TheRequestObject) 。 ) </span><span class="sxs-lookup"><span data-stu-id="9801f-211">(For more about the `Request` object, see the [sidebar](#BKMK_TheRequestObject) later.)</span></span>

<span data-ttu-id="9801f-212">很简单，足以读取文本框的值。</span><span class="sxs-lookup"><span data-stu-id="9801f-212">It's simple enough to read the value of the text box.</span></span> <span data-ttu-id="9801f-213">但是，如果用户没有在文本框中输入任何内容，但仍单击 " **搜索** "，则可以忽略这一单击，因为没有要搜索的内容。</span><span class="sxs-lookup"><span data-stu-id="9801f-213">But if the user didn't enter anything at all in the text box but clicked **Search** anyway, you can ignore that click, since there's nothing to search.</span></span>

<span data-ttu-id="9801f-214">下面的代码示例演示如何实现这些条件。</span><span class="sxs-lookup"><span data-stu-id="9801f-214">The following code is an example that shows how to implement these conditions.</span></span> <span data-ttu-id="9801f-215"> (你还不必添加此代码;稍后你将执行此操作。 ) </span><span class="sxs-lookup"><span data-stu-id="9801f-215">(You don't have to add this code yet; you'll do that in a moment.)</span></span>

[!code-csharp[Main](form-basics/samples/sample3.cs)]

<span data-ttu-id="9801f-216">测试将以这种方式断开：</span><span class="sxs-lookup"><span data-stu-id="9801f-216">The test breaks down in this way:</span></span>

- <span data-ttu-id="9801f-217">获取的值 `Request.QueryString["searchGenre"]` ，即输入到名为的元素中的值 `<input>` `searchGenre` 。</span><span class="sxs-lookup"><span data-stu-id="9801f-217">Get the value of `Request.QueryString["searchGenre"]`, namely the value that was entered into the `<input>` element named `searchGenre`.</span></span>
- <span data-ttu-id="9801f-218">使用方法查明其是否为空 `IsEmpty` 。</span><span class="sxs-lookup"><span data-stu-id="9801f-218">Find out if it's empty by using the `IsEmpty` method.</span></span> <span data-ttu-id="9801f-219">此方法是一种标准方法，用于确定是否 (例如，) 包含值的窗体元素。</span><span class="sxs-lookup"><span data-stu-id="9801f-219">This method is the standard way to determine whether something (for example, a form element) contains a value.</span></span> <span data-ttu-id="9801f-220">但实际上，您只关心它 *是否不* 为空，因此 .。。</span><span class="sxs-lookup"><span data-stu-id="9801f-220">But really, you care only if it's *not* empty, therefore ...</span></span>
- <span data-ttu-id="9801f-221">`!`在测试的前面添加运算符 `IsEmpty` 。</span><span class="sxs-lookup"><span data-stu-id="9801f-221">Add the `!` operator in front of the `IsEmpty` test.</span></span> <span data-ttu-id="9801f-222"> (`!` 运算符意味着逻辑 NOT) 。</span><span class="sxs-lookup"><span data-stu-id="9801f-222">(The `!` operator means logical NOT).</span></span>

<span data-ttu-id="9801f-223">在纯英文版中，整个 `if` 条件转换为以下 *形式：如果窗体的 searchGenre 元素不为空，则 ...*</span><span class="sxs-lookup"><span data-stu-id="9801f-223">In plain English, the entire `if` condition translates into the following: *If the form's searchGenre element is not empty, then ...*</span></span>

<span data-ttu-id="9801f-224">此块设置用于创建使用搜索词的查询的阶段。</span><span class="sxs-lookup"><span data-stu-id="9801f-224">This block sets the stage for creating a query that uses the search term.</span></span> <span data-ttu-id="9801f-225">将在下一部分执行该操作。</span><span class="sxs-lookup"><span data-stu-id="9801f-225">You'll do that in the next section.</span></span>

<a id="BKMK_TheRequestObject"></a>

> [!TIP] 
> 
> <span data-ttu-id="9801f-226">**Request 对象**</span><span class="sxs-lookup"><span data-stu-id="9801f-226">**The Request Object**</span></span>
> 
> <span data-ttu-id="9801f-227">`Request`对象包含浏览器在请求或提交页面时发送给应用程序的所有信息。</span><span class="sxs-lookup"><span data-stu-id="9801f-227">The `Request` object contains all the information that the browser sends to your application when a page is requested or submitted.</span></span> <span data-ttu-id="9801f-228">此对象包括用户提供的所有信息，如要上传的文本框值或文件。</span><span class="sxs-lookup"><span data-stu-id="9801f-228">This object includes any information that the user provides, like text box values or a file to upload.</span></span> <span data-ttu-id="9801f-229">它还包括所有种类的附加信息，如 cookie、URL 查询字符串中的值 (如有任何) 、正在运行的页面的文件路径、用户使用的浏览器的类型、在浏览器中设置的语言的列表，等等。</span><span class="sxs-lookup"><span data-stu-id="9801f-229">It also includes all sorts of additional information, like cookies, values in the URL query string (if any), the file path of the page that is running, the type of browser that the user is using, the list of languages that are set in the browser, and much more.</span></span>
> 
> <span data-ttu-id="9801f-230">`Request`对象是值 (列表) 的*集合*。</span><span class="sxs-lookup"><span data-stu-id="9801f-230">The `Request` object is a *collection* (list) of values.</span></span> <span data-ttu-id="9801f-231">通过指定集合的名称，可以获取集合中的单个值：</span><span class="sxs-lookup"><span data-stu-id="9801f-231">You get an individual value out of the collection by specifying its name:</span></span>
> 
> `var someValue = Request["name"];`
> 
> <span data-ttu-id="9801f-232">`Request`对象实际上公开了多个子集。</span><span class="sxs-lookup"><span data-stu-id="9801f-232">The `Request` object actually exposes several subsets.</span></span> <span data-ttu-id="9801f-233">例如：</span><span class="sxs-lookup"><span data-stu-id="9801f-233">For example:</span></span>
> 
> - <span data-ttu-id="9801f-234">`Request.Form``<form>`如果请求是请求，则从已提交元素内的元素中提供值 `POST` 。</span><span class="sxs-lookup"><span data-stu-id="9801f-234">`Request.Form` gives you values from elements inside the submitted `<form>` element if the request is a `POST` request.</span></span>
> - <span data-ttu-id="9801f-235">`Request.QueryString` 只提供 URL 的查询字符串中的值。</span><span class="sxs-lookup"><span data-stu-id="9801f-235">`Request.QueryString` gives you just the values in the URL's query string.</span></span> <span data-ttu-id="9801f-236"> (在 URL （如 `http://mysite/myapp/page?searchGenre=action&page=2` ）中， `?searchGenre=action&page=2` url 的部分是查询字符串。 ) </span><span class="sxs-lookup"><span data-stu-id="9801f-236">(In a URL like `http://mysite/myapp/page?searchGenre=action&page=2`, the `?searchGenre=action&page=2` section of the URL is the query string.)</span></span>
> - <span data-ttu-id="9801f-237">`Request.Cookies` 集合使你可以访问浏览器已发送的 cookie。</span><span class="sxs-lookup"><span data-stu-id="9801f-237">`Request.Cookies` collection gives you access to cookies that the browser has sent.</span></span>
> 
> <span data-ttu-id="9801f-238">若要获取你知道的值在提交的窗体中，你可以使用 `Request["name"]` 。</span><span class="sxs-lookup"><span data-stu-id="9801f-238">To get a value that you know is in the submitted form, you can use `Request["name"]`.</span></span> <span data-ttu-id="9801f-239">或者，你可以使用更具体的版本 `Request.Form["name"]` (`POST` 请求) 或 `Request.QueryString["name"]` (`GET`) 请求。</span><span class="sxs-lookup"><span data-stu-id="9801f-239">Alternatively, you can use the more specific versions `Request.Form["name"]` (for `POST` requests) or `Request.QueryString["name"]` (for `GET` requests).</span></span> <span data-ttu-id="9801f-240">当然， *name* 是要获取的项的名称。</span><span class="sxs-lookup"><span data-stu-id="9801f-240">Of course, *name* is the name of the item to get.</span></span>
> 
> <span data-ttu-id="9801f-241">要获取的项的名称必须在所使用的集合中是唯一的。</span><span class="sxs-lookup"><span data-stu-id="9801f-241">The name of the item you want to get has to be unique within the collection you're using.</span></span> <span data-ttu-id="9801f-242">这就是 `Request` 对象提供类似于和的子集的原因 `Request.Form` `Request.QueryString` 。</span><span class="sxs-lookup"><span data-stu-id="9801f-242">That's why the `Request` object provides the subsets like `Request.Form` and `Request.QueryString`.</span></span> <span data-ttu-id="9801f-243">假设页面包含一个名为的窗体元素 `userName` ， *还* 包含一个名为的 cookie `userName` 。</span><span class="sxs-lookup"><span data-stu-id="9801f-243">Suppose that your page contains a form element named `userName` and *also* contains a cookie named `userName`.</span></span> <span data-ttu-id="9801f-244">如果获得 `Request["userName"]` 了，是否需要窗体值或 cookie。</span><span class="sxs-lookup"><span data-stu-id="9801f-244">If you get `Request["userName"]`, it's ambiguous whether you want the form value or the cookie.</span></span> <span data-ttu-id="9801f-245">但是，如果你获取 `Request.Form["userName"]` `Request.Cookie["userName"]` 了或，则会明确了解要获取的值。</span><span class="sxs-lookup"><span data-stu-id="9801f-245">However, if you get `Request.Form["userName"]` or `Request.Cookie["userName"]`, you're being explicit about which value to get.</span></span>
> 
> <span data-ttu-id="9801f-246">这是一种很好的做法， `Request` 只需使用您感兴趣的子集，如 `Request.Form` 或 `Request.QueryString` 。</span><span class="sxs-lookup"><span data-stu-id="9801f-246">It's a good practice to be specific and use the subset of `Request` that you're interested in, like `Request.Form` or `Request.QueryString`.</span></span> <span data-ttu-id="9801f-247">对于您在本教程中创建的简单页面，它可能不会真正产生任何差别。</span><span class="sxs-lookup"><span data-stu-id="9801f-247">For the simple pages that you're creating in this tutorial, it probably doesn't really make any difference.</span></span> <span data-ttu-id="9801f-248">但是，当你创建更复杂的页面时，使用显式版本 `Request.Form` 或 `Request.QueryString` 可以帮助你避免在页面包含窗体时可能出现的问题 (或多个窗体) 、cookie、查询字符串值等。</span><span class="sxs-lookup"><span data-stu-id="9801f-248">However, as you create more complex pages, using the explicit version `Request.Form` or `Request.QueryString` can help you avoid problems that can arise when the page contains a form (or multiple forms), cookies, query string values, and so on.</span></span>

## <a name="creating-a-query-by-using-a-search-term"></a><span data-ttu-id="9801f-249">使用搜索词创建查询</span><span class="sxs-lookup"><span data-stu-id="9801f-249">Creating a Query by Using a Search Term</span></span>

<span data-ttu-id="9801f-250">现在，您已经知道了如何获取用户输入的搜索词，接下来可以创建一个使用它的查询。</span><span class="sxs-lookup"><span data-stu-id="9801f-250">Now that you know how to get the search term that the user entered, you can create a query that uses it.</span></span> <span data-ttu-id="9801f-251">请记住，若要从数据库中获取所有电影项，请使用类似于以下语句的 SQL 查询：</span><span class="sxs-lookup"><span data-stu-id="9801f-251">Remember that to get all the movie items out of the database, you're using a SQL query that looks like this statement:</span></span>

`SELECT * FROM Movies`

<span data-ttu-id="9801f-252">若要仅获取特定电影，必须使用包含子句的查询 `Where` 。</span><span class="sxs-lookup"><span data-stu-id="9801f-252">To get only certain movies, you have to use a query that includes a `Where` clause.</span></span> <span data-ttu-id="9801f-253">此子句可用于设置查询返回的行的条件。</span><span class="sxs-lookup"><span data-stu-id="9801f-253">This clause lets you set a condition on which rows are returned by the query.</span></span> <span data-ttu-id="9801f-254">下面的示例说明：</span><span class="sxs-lookup"><span data-stu-id="9801f-254">Here's an example:</span></span>

`SELECT * FROM Movies WHERE Genre = 'Action'`

<span data-ttu-id="9801f-255">基本格式是 `WHERE column = value` 。</span><span class="sxs-lookup"><span data-stu-id="9801f-255">The basic format is `WHERE column = value`.</span></span> <span data-ttu-id="9801f-256">除了 (大于) 以外，你还可以使用不同的运算符， `=` `>` `<` (小于) ， `<>` (不等于) ， `<=` (小于或等于) 等，具体取决于你要查找的内容。</span><span class="sxs-lookup"><span data-stu-id="9801f-256">You can use different operators besides just `=`, like `>` (greater than), `<` (less than), `<>` (not equal to), `<=` (less than or equal to), etc., depending on what you're looking for.</span></span>

<span data-ttu-id="9801f-257">如果您想知道，SQL 语句不区分大小写， &mdash; `SELECT` `Select` (甚至 `select`) 。</span><span class="sxs-lookup"><span data-stu-id="9801f-257">In case you're wondering, SQL statements are not case sensitive &mdash; `SELECT` is the same as `Select` (or even `select`).</span></span> <span data-ttu-id="9801f-258">但是，用户通常在 SQL 语句（如和）中将关键字大写， `SELECT` `WHERE` 使其更易于阅读。</span><span class="sxs-lookup"><span data-stu-id="9801f-258">However, people often capitalize keywords in a SQL statement, like `SELECT` and `WHERE`, to make it easier to read.</span></span>

### <a name="passing-the-search-term-as-a-parameter"></a><span data-ttu-id="9801f-259">作为参数传递搜索词</span><span class="sxs-lookup"><span data-stu-id="9801f-259">Passing the search term as a parameter</span></span>

<span data-ttu-id="9801f-260">搜索特定的流派非常容易 `WHERE Genre = 'Action'`)  (，但您希望能够搜索用户输入的任何流派。</span><span class="sxs-lookup"><span data-stu-id="9801f-260">Searching for a specific genre is easy enough (`WHERE Genre = 'Action'`), but you want to be able to search for any genre that the user enters.</span></span> <span data-ttu-id="9801f-261">为此，你将创建为包含要搜索的值的占位符的 SQL 查询。</span><span class="sxs-lookup"><span data-stu-id="9801f-261">To do that, you create as SQL query that includes a placeholder for the value to search.</span></span> <span data-ttu-id="9801f-262">它将类似于以下命令：</span><span class="sxs-lookup"><span data-stu-id="9801f-262">It will look like this command:</span></span>

`SELECT * FROM Movies WHERE Genre = @0`

<span data-ttu-id="9801f-263">占位符是 `@` 后跟零的字符。</span><span class="sxs-lookup"><span data-stu-id="9801f-263">The placeholder is the `@` character followed by zero.</span></span> <span data-ttu-id="9801f-264">您可能猜到，查询可以包含多个占位符，它们被命名为 `@0` 、 `@1` 、等 `@2` 。</span><span class="sxs-lookup"><span data-stu-id="9801f-264">As you might guess, a query can contain multiple placeholders, and they'd be named `@0`, `@1`, `@2`, etc.</span></span>

<span data-ttu-id="9801f-265">若要设置查询并为其实际传递值，请使用如下所示的代码：</span><span class="sxs-lookup"><span data-stu-id="9801f-265">To set up the query and actually pass it the value, you use the code like the following:</span></span>

[!code-sql[Main](form-basics/samples/sample4.sql)]

<span data-ttu-id="9801f-266">此代码类似于在网格中显示数据所执行的操作。</span><span class="sxs-lookup"><span data-stu-id="9801f-266">This code is similar to what you've already done to display data in the grid.</span></span> <span data-ttu-id="9801f-267">唯一的区别是：</span><span class="sxs-lookup"><span data-stu-id="9801f-267">The only differences are:</span></span>

- <span data-ttu-id="9801f-268">查询包含占位符 (`WHERE Genre = @0"`) 。</span><span class="sxs-lookup"><span data-stu-id="9801f-268">The query contains a placeholder (`WHERE Genre = @0"`).</span></span>
- <span data-ttu-id="9801f-269">查询将被放入变量 (`selectCommand`) ; 之前，你将查询直接传递到 `db.Query` 方法。</span><span class="sxs-lookup"><span data-stu-id="9801f-269">The query is put into a variable (`selectCommand`); before, you passed the query directly to the `db.Query` method.</span></span>
- <span data-ttu-id="9801f-270">当调用方法时 `db.Query` ，将同时传递查询和用于占位符的值。</span><span class="sxs-lookup"><span data-stu-id="9801f-270">When you call the `db.Query` method, you pass both the query and the value to use for the placeholder.</span></span> <span data-ttu-id="9801f-271"> (如果查询具有多个占位符，则可以将它们全部作为不同的值传递给方法。 ) </span><span class="sxs-lookup"><span data-stu-id="9801f-271">(If the query had multiple placeholders, you'd pass them all as separate values to the method.)</span></span>

<span data-ttu-id="9801f-272">如果将所有这些元素放在一起，则会获得以下代码：</span><span class="sxs-lookup"><span data-stu-id="9801f-272">If you put all these elements together, you get the following code:</span></span>

[!code-csharp[Main](form-basics/samples/sample5.cs)]

> [!NOTE] 
> 
> <span data-ttu-id="9801f-273">**重要说明：**</span><span class="sxs-lookup"><span data-stu-id="9801f-273">**Important!**</span></span> <span data-ttu-id="9801f-274">使用占位符 (如 `@0`) 将值传递给 SQL 命令对于安全性 *极其重要* 。</span><span class="sxs-lookup"><span data-stu-id="9801f-274">Using placeholders (like `@0`) to pass values to a SQL command is *extremely important* for security.</span></span> <span data-ttu-id="9801f-275">在此处看到的是变量数据的占位符，是构造 SQL 命令的唯一方法。</span><span class="sxs-lookup"><span data-stu-id="9801f-275">The way you see it here, with placeholders for variable data, is the only way you should construct SQL commands.</span></span>
> 
> <span data-ttu-id="9801f-276">永远不会通过组合 (将从用户那里) 文本和值连接在一起来构造 SQL 语句。</span><span class="sxs-lookup"><span data-stu-id="9801f-276">Never construct a SQL statement by putting together (concatenating) literal text and values you get from the user.</span></span> <span data-ttu-id="9801f-277">将用户输入连接到 SQL 语句将打开站点到 *sql 注入攻击* ，恶意用户会将值提交到攻击数据库的页面。</span><span class="sxs-lookup"><span data-stu-id="9801f-277">Concatenating user input into a SQL statement opens your site to a *SQL injection attack* where a malicious user submits values to your page that hack your database.</span></span> <span data-ttu-id="9801f-278"> (可以在 MSDN 网站的 [SQL 注入](https://msdn.microsoft.com/library/ms161953.aspx) 一文中阅读更多详细信息。 ) </span><span class="sxs-lookup"><span data-stu-id="9801f-278">(You can read more in the article [SQL Injection](https://msdn.microsoft.com/library/ms161953.aspx) the MSDN website.)</span></span>

## <a name="updating-the-movies-page-with-search-code"></a><span data-ttu-id="9801f-279">更新包含搜索代码的电影页面</span><span class="sxs-lookup"><span data-stu-id="9801f-279">Updating the Movies Page with Search Code</span></span>

<span data-ttu-id="9801f-280">现在，您可以更新 " *电影* " 文件中的代码。</span><span class="sxs-lookup"><span data-stu-id="9801f-280">Now you can update the code in the *Movies.cshtml* file.</span></span> <span data-ttu-id="9801f-281">首先，将页面顶部代码块中的代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="9801f-281">To begin, replace the code in the code block at the top of the page with this code:</span></span>

[!code-csharp[Main](form-basics/samples/sample6.cs)]

<span data-ttu-id="9801f-282">此处的差别在于，你已将查询放入 `selectCommand` 变量中，稍后会将该变量传递给 `db.Query` 。</span><span class="sxs-lookup"><span data-stu-id="9801f-282">The difference here is that you've put the query into the `selectCommand` variable, which you'll pass to `db.Query` later.</span></span> <span data-ttu-id="9801f-283">如果将 SQL 语句放入变量中，则可以更改语句，这是执行搜索的操作。</span><span class="sxs-lookup"><span data-stu-id="9801f-283">Putting the SQL statement into a variable lets you change the statement, which is what you'll do to perform the search.</span></span>

<span data-ttu-id="9801f-284">你还删除了这两行，稍后会将其放回：</span><span class="sxs-lookup"><span data-stu-id="9801f-284">You've also removed these two lines, which you'll put back in later:</span></span>

[!code-csharp[Main](form-basics/samples/sample7.cs)]

<span data-ttu-id="9801f-285">您不想运行查询 (也就是说，调用 `db.Query`) 并且您还不想初始化 `WebGrid` 帮助程序。</span><span class="sxs-lookup"><span data-stu-id="9801f-285">You don't want to run the query yet (that is, call `db.Query`) and you don't want to initialize the `WebGrid` helper yet either.</span></span> <span data-ttu-id="9801f-286">确定要运行的 SQL 语句后，您将执行这些操作。</span><span class="sxs-lookup"><span data-stu-id="9801f-286">You'll do those things after you've figured out which SQL statement has to run.</span></span>

<span data-ttu-id="9801f-287">在此重写块后，可以添加用于处理搜索的新逻辑。</span><span class="sxs-lookup"><span data-stu-id="9801f-287">After this rewritten block, you can add the new logic for handling the search.</span></span> <span data-ttu-id="9801f-288">已完成的代码将如下所示。</span><span class="sxs-lookup"><span data-stu-id="9801f-288">The completed code will look like the following.</span></span> <span data-ttu-id="9801f-289">更新页面中的代码，使其与以下示例匹配：</span><span class="sxs-lookup"><span data-stu-id="9801f-289">Update the code in your page so it matches this example:</span></span>

[!code-cshtml[Main](form-basics/samples/sample8.cshtml)]

<span data-ttu-id="9801f-290">该页的工作方式如下所示。</span><span class="sxs-lookup"><span data-stu-id="9801f-290">The page now works like this.</span></span> <span data-ttu-id="9801f-291">每次运行该页面时，代码都会打开数据库，并将 `selectCommand` 变量设置为从表中获取所有记录的 SQL 语句 `Movies` 。</span><span class="sxs-lookup"><span data-stu-id="9801f-291">Every time the page runs, the code opens the database and the `selectCommand` variable is set to the SQL statement that gets all the records from the `Movies` table.</span></span> <span data-ttu-id="9801f-292">此代码还初始化 `searchTerm` 变量。</span><span class="sxs-lookup"><span data-stu-id="9801f-292">The code also initializes the `searchTerm` variable.</span></span>

<span data-ttu-id="9801f-293">但是，如果当前请求包含一个元素的值 `searchGenre` ，则代码会将 `selectCommand` 另一个查询（即）设置为一个包含子句的其他查询， `Where` 以搜索流派。</span><span class="sxs-lookup"><span data-stu-id="9801f-293">However, if the current request includes a value for the `searchGenre` element, the code sets `selectCommand` to a different query — namely, to one that includes the `Where` clause to search for a genre.</span></span> <span data-ttu-id="9801f-294">它还将设置 `searchTerm` 为搜索框中传递的任何内容 (这可能不是) 。</span><span class="sxs-lookup"><span data-stu-id="9801f-294">It also sets `searchTerm` to whatever was passed for the search box (which might be nothing).</span></span>

<span data-ttu-id="9801f-295">无论在哪个 SQL 语句中 `selectCommand` ，代码都会调用 `db.Query` 来运行查询，同时传递其中的任何内容 `searchTerm` 。</span><span class="sxs-lookup"><span data-stu-id="9801f-295">Regardless of which SQL statement is in `selectCommand`, the code then calls `db.Query` to run the query, passing it whatever is in `searchTerm`.</span></span> <span data-ttu-id="9801f-296">如果中没有任何内容 `searchTerm` ，则不重要，因为在这种情况下，没有参数可将值传递给 `selectCommand` 无论如何。</span><span class="sxs-lookup"><span data-stu-id="9801f-296">If there's nothing in `searchTerm`, it doesn't matter, because in that case there's no parameter to pass the value to `selectCommand` anyway.</span></span>

<span data-ttu-id="9801f-297">最后，代码 `WebGrid` 使用查询结果来初始化帮助程序，就像以前一样。</span><span class="sxs-lookup"><span data-stu-id="9801f-297">Finally, the code initializes the `WebGrid` helper by using the query results, just like before.</span></span>

<span data-ttu-id="9801f-298">你可以看到，通过将 SQL 语句和搜索词放入变量中，你已增加了代码的灵活性。</span><span class="sxs-lookup"><span data-stu-id="9801f-298">You can see that by putting the SQL statement and the search term into variables, you've added flexibility to the code.</span></span> <span data-ttu-id="9801f-299">你将在本教程的后面部分中看到，你可以使用此基本框架，并为不同类型的搜索继续添加逻辑。</span><span class="sxs-lookup"><span data-stu-id="9801f-299">As you'll see later in this tutorial, you can use this basic framework and keep adding logic for different types of searches.</span></span>

## <a name="testing-the-search-by-genre-feature"></a><span data-ttu-id="9801f-300">测试流派搜索功能</span><span class="sxs-lookup"><span data-stu-id="9801f-300">Testing the Search-by-Genre Feature</span></span>

<span data-ttu-id="9801f-301">在 WebMatrix 中，运行 " *电影* " 页。</span><span class="sxs-lookup"><span data-stu-id="9801f-301">In WebMatrix, run the *Movies.cshtml* page.</span></span> <span data-ttu-id="9801f-302">你会看到带有流派文本框的页面。</span><span class="sxs-lookup"><span data-stu-id="9801f-302">You see the page with the text box for genre.</span></span>

<span data-ttu-id="9801f-303">输入你为某个测试记录输入的流派，然后单击 " **搜索**"。</span><span class="sxs-lookup"><span data-stu-id="9801f-303">Enter a genre that you've entered for one of your test records, then click **Search**.</span></span> <span data-ttu-id="9801f-304">此时会看到一个列表，其中列出了与该流派匹配的影片：</span><span class="sxs-lookup"><span data-stu-id="9801f-304">This time you see a listing of just the movies that match that genre:</span></span>

![搜索 "Comedies" 流派后的电影页面列表](form-basics/_static/image4.png)

<span data-ttu-id="9801f-306">请输入不同的流派并重新搜索。</span><span class="sxs-lookup"><span data-stu-id="9801f-306">Enter a different genre and search again.</span></span> <span data-ttu-id="9801f-307">尝试使用全部小写字母或所有大写字母输入流派，以便可以看到搜索不区分大小写。</span><span class="sxs-lookup"><span data-stu-id="9801f-307">Try entering the genre by using all lowercase or all uppercase letters so that you can see that the search is not case sensitive.</span></span>

## <a name="remembering-what-the-user-entered"></a><span data-ttu-id="9801f-308">"记住" 用户输入的内容</span><span class="sxs-lookup"><span data-stu-id="9801f-308">"Remembering" What the User Entered</span></span>

<span data-ttu-id="9801f-309">您可能已注意到，在输入流派并单击 **搜索流派**后，会看到该流派的列表。</span><span class="sxs-lookup"><span data-stu-id="9801f-309">You might have noticed that after you entered a genre and clicked **Search Genre**, you saw a listing for that genre.</span></span> <span data-ttu-id="9801f-310">不过，"搜索" 文本框是空的 &mdash; ，也就是说，它不记得您输入的内容。</span><span class="sxs-lookup"><span data-stu-id="9801f-310">However, the search text box was empty &mdash; in other words, it didn't remember what you'd entered.</span></span>

<span data-ttu-id="9801f-311">务必了解为何会出现此行为。</span><span class="sxs-lookup"><span data-stu-id="9801f-311">It's important to understand why this behavior occurs.</span></span> <span data-ttu-id="9801f-312">提交页面后，浏览器会向 web 服务器发送请求。</span><span class="sxs-lookup"><span data-stu-id="9801f-312">When you submit a page, the browser sends a request to the web server.</span></span> <span data-ttu-id="9801f-313">当 ASP.NET 获取请求时，它会创建页面的全新实例，运行其中的代码，然后再次将页面呈现到浏览器。</span><span class="sxs-lookup"><span data-stu-id="9801f-313">When ASP.NET gets the request, it creates a brand-new instance of the page, runs the code in it, and then renders the page to the browser again.</span></span> <span data-ttu-id="9801f-314">但实际上，页面并不知道自己使用的是其自身的以前版本。</span><span class="sxs-lookup"><span data-stu-id="9801f-314">In effect, though, the page doesn't know that you were just working with a previous version of itself.</span></span> <span data-ttu-id="9801f-315">它的所有人都知道，请求中包含某些表单数据。</span><span class="sxs-lookup"><span data-stu-id="9801f-315">All it knows is that it got a request that had some form data in it.</span></span>

<span data-ttu-id="9801f-316">每次请求页面时， &mdash; 无论是首次请求还是提交，都 &mdash; 要获取一个新页面。</span><span class="sxs-lookup"><span data-stu-id="9801f-316">Every time you request a page &mdash; whether for the first time or by submitting it &mdash; you're getting a new page.</span></span> <span data-ttu-id="9801f-317">Web 服务器没有最近的请求的内存。</span><span class="sxs-lookup"><span data-stu-id="9801f-317">The web server has no memory of your last request.</span></span> <span data-ttu-id="9801f-318">既不 ASP.NET，也不执行浏览器。</span><span class="sxs-lookup"><span data-stu-id="9801f-318">Neither does ASP.NET, and neither does the browser.</span></span> <span data-ttu-id="9801f-319">页面的这些单独实例之间唯一的连接是在它们之间传输的任何数据。</span><span class="sxs-lookup"><span data-stu-id="9801f-319">The only connection between these separate instances of the page is any data that you transmit between them.</span></span> <span data-ttu-id="9801f-320">例如，如果您提交一个页面，则新页面实例可以获取之前实例发送的表单数据。</span><span class="sxs-lookup"><span data-stu-id="9801f-320">If you submit a page, for example, the new page instance can get the form data that was sent by the earlier instance.</span></span> <span data-ttu-id="9801f-321"> (在页面间传递数据的另一种方法是使用 cookie。 ) </span><span class="sxs-lookup"><span data-stu-id="9801f-321">(Another way to pass data between pages is to use cookies.)</span></span>

<span data-ttu-id="9801f-322">描述这种情况的一种正式方法是说，网页是 *无状态*的。</span><span class="sxs-lookup"><span data-stu-id="9801f-322">A formal way to describe this situation is to say that web pages are *stateless*.</span></span> <span data-ttu-id="9801f-323">Web 服务器以及页面本身和页面中的元素不会维护有关页面以前状态的任何信息。</span><span class="sxs-lookup"><span data-stu-id="9801f-323">Web servers and the pages themselves and the elements in the page do not maintain any information about the previous state of a page.</span></span> <span data-ttu-id="9801f-324">Web 是以这种方式设计的，因为维护单个请求的状态会迅速耗尽 web 服务器的资源，这通常会处理数千个，甚至可能每秒处理成千上万个请求。</span><span class="sxs-lookup"><span data-stu-id="9801f-324">The web was designed this way because maintaining state for individual requests would quickly exhaust the resources of web servers, which often handle thousands, maybe even hundreds of thousands, of requests per second.</span></span>

<span data-ttu-id="9801f-325">这就是文本框为空的原因。</span><span class="sxs-lookup"><span data-stu-id="9801f-325">So that's why the text box was empty.</span></span> <span data-ttu-id="9801f-326">提交页面后，ASP.NET 创建了页面的新实例，并通过代码和标记进行了运行。</span><span class="sxs-lookup"><span data-stu-id="9801f-326">After you submitted the page, ASP.NET created a new instance of the page and ran through the code and markup.</span></span> <span data-ttu-id="9801f-327">此代码中没有告诉 ASP.NET 将值放入文本框的内容。</span><span class="sxs-lookup"><span data-stu-id="9801f-327">There was nothing in that code that told ASP.NET to put a value into the text box.</span></span> <span data-ttu-id="9801f-328">因此，ASP.NET 不会执行任何操作，并且文本框中的值不包含任何值。</span><span class="sxs-lookup"><span data-stu-id="9801f-328">So ASP.NET didn't do anything, and the text box was rendered without a value in it.</span></span>

<span data-ttu-id="9801f-329">实际上有一种简单的方法可解决此问题。</span><span class="sxs-lookup"><span data-stu-id="9801f-329">There's actually an easy way to get around this issue.</span></span> <span data-ttu-id="9801f-330">您 *在文本框* 中输入的流派可供您在中的代码中使用 &mdash; `Request.QueryString["searchGenre"]` 。</span><span class="sxs-lookup"><span data-stu-id="9801f-330">The genre that you entered into the text box *is* available to you in code &mdash; it's in `Request.QueryString["searchGenre"]`.</span></span>

<span data-ttu-id="9801f-331">更新文本框的标记 `value` ，以便属性从获取其值 `searchTerm` ，如下例所示：</span><span class="sxs-lookup"><span data-stu-id="9801f-331">Update the markup for the text box so that the `value` attribute gets its value from `searchTerm`, like this example:</span></span>

[!code-html[Main](form-basics/samples/sample9.html?highlight=1)]

<span data-ttu-id="9801f-332">在此页中，还可以将属性设置 `value` 为 `searchTerm` 变量，因为该变量还包含您输入的流派。</span><span class="sxs-lookup"><span data-stu-id="9801f-332">In this page, you could have also set the `value` attribute to the `searchTerm` variable, since that variable also contains the genre you entered.</span></span> <span data-ttu-id="9801f-333">但使用 `Request` 对象来设置 `value` 属性（如下所示）是完成此任务的标准方法。</span><span class="sxs-lookup"><span data-stu-id="9801f-333">But using the `Request` object to set the `value` attribute as shown here is the standard way to accomplish this task.</span></span> <span data-ttu-id="9801f-334"> (假设您甚至要在某些情况下执行此操作 &mdash; ，则您可能希望在字段中呈现 *没有* 值的页面。</span><span class="sxs-lookup"><span data-stu-id="9801f-334">(Assuming you even want to do this &mdash; in some situations, you might want to render the page *without* values in the fields.</span></span> <span data-ttu-id="9801f-335">这一切都取决于应用的进展情况。 ) </span><span class="sxs-lookup"><span data-stu-id="9801f-335">It all depends on what's going on with your app.)</span></span>

> [!NOTE]
> <span data-ttu-id="9801f-336">不能 "记住" 用于密码的文本框的值。</span><span class="sxs-lookup"><span data-stu-id="9801f-336">You can't "remember" the value of a text box that's used for passwords.</span></span> <span data-ttu-id="9801f-337">这会成为允许用户使用代码填写密码字段的安全漏洞。</span><span class="sxs-lookup"><span data-stu-id="9801f-337">It would be a security hole to allow people to fill in a password field by using code.</span></span>

<span data-ttu-id="9801f-338">再次运行该页面，输入流派，然后单击 " **搜索流派**"。</span><span class="sxs-lookup"><span data-stu-id="9801f-338">Run the page again, enter a genre, and click **Search Genre**.</span></span> <span data-ttu-id="9801f-339">这一次不仅能看到搜索结果，而且文本框记住了上次输入的内容：</span><span class="sxs-lookup"><span data-stu-id="9801f-339">This time not only do you see the results of the search, but the text box remembers what you entered last time:</span></span>

![显示前一项已 "记住" 文本框的页面](form-basics/_static/image5.png)

## <a name="searching-for-any-word-in-the-title"></a><span data-ttu-id="9801f-341">搜索标题中的任何词</span><span class="sxs-lookup"><span data-stu-id="9801f-341">Searching for Any Word in the Title</span></span>

<span data-ttu-id="9801f-342">你现在可以搜索任何流派，但你可能还希望搜索标题。</span><span class="sxs-lookup"><span data-stu-id="9801f-342">You can now search for any genre, but you might also want to search for a title.</span></span> <span data-ttu-id="9801f-343">搜索时很难准确地获取标题，因此，您可以搜索出现在标题内任意位置的单词。</span><span class="sxs-lookup"><span data-stu-id="9801f-343">It's hard to get a title exactly right when you search, so instead you can search for a word that appears anywhere inside a title.</span></span> <span data-ttu-id="9801f-344">为此，请使用 `LIKE` 运算符和语法，如下所示：</span><span class="sxs-lookup"><span data-stu-id="9801f-344">To do that in SQL, you use the `LIKE` operator and syntax like the following:</span></span>

`SELECT * FROM Movies WHERE Title LIKE '%adventure%'`

<span data-ttu-id="9801f-345">此命令将获取其标题包含 "艾德" 的所有电影。</span><span class="sxs-lookup"><span data-stu-id="9801f-345">This command gets all the movies whose titles contain "adventure".</span></span> <span data-ttu-id="9801f-346">使用 `LIKE` 运算符时，请在搜索词中包含通配符 `%` 。</span><span class="sxs-lookup"><span data-stu-id="9801f-346">When you use the `LIKE` operator, you include the wildcard character `%` as part of the search term.</span></span> <span data-ttu-id="9801f-347">搜索 `LIKE 'adventure%'` 表示 "以 ' 艾德 ' 开头"。</span><span class="sxs-lookup"><span data-stu-id="9801f-347">The search `LIKE 'adventure%'` means "starting with 'adventure'".</span></span> <span data-ttu-id="9801f-348">从技术上说，这意味着 "字符串 ' 艾德" 后跟任何内容。 " (类似地 ) ，搜索词 `LIKE '%adventure'` 表示 "任何内容后跟字符串 ' 艾德 '"，这是另一种说 "以 ' 艾德 ' 结尾" 的方法。</span><span class="sxs-lookup"><span data-stu-id="9801f-348">(Technically, it means "The string 'adventure' followed by anything.") Similarly, the search term `LIKE '%adventure'` means "anything followed by the string 'adventure'", which is another way to say "ending with 'adventure'".</span></span>

<span data-ttu-id="9801f-349">因此，搜索词 `LIKE '%adventure%'` 表示在标题中的任意位置具有 "艾德"。</span><span class="sxs-lookup"><span data-stu-id="9801f-349">The search term `LIKE '%adventure%'` therefore means "with 'adventure' anywhere in the title."</span></span> <span data-ttu-id="9801f-350">从技术上说，"标题中的任何内容，后面跟有" 艾德公司 "，然后再执行任何操作。" () </span><span class="sxs-lookup"><span data-stu-id="9801f-350">(Technically, "anything in the title, followed by 'adventure', followed by anything.")</span></span>

<span data-ttu-id="9801f-351">在 `<form>` 元素中，将以下标记添加到 "流派搜索" 的结束 `</div>` 标记下 (紧靠在结束 `</form>` 元素) 之前：</span><span class="sxs-lookup"><span data-stu-id="9801f-351">Inside the `<form>` element, add the following markup right under the closing `</div>` tag for the genre search (just before the closing `</form>` element):</span></span>

[!code-html[Main](form-basics/samples/sample10.html)]

<span data-ttu-id="9801f-352">用于处理此搜索的代码与用于流派搜索的代码相似，不同之处在于您必须对搜索进行组合 `LIKE` 。</span><span class="sxs-lookup"><span data-stu-id="9801f-352">The code to handle this search is similar to the code for the genre search, except that you have to assemble the `LIKE` search.</span></span> <span data-ttu-id="9801f-353">在页面顶部的代码块中，将此块添加到 `if` `if` 流派搜索块的紧后面：</span><span class="sxs-lookup"><span data-stu-id="9801f-353">Inside the code block at the top of the page, add this `if` block just after the `if` block for the genre search:</span></span>

[!code-csharp[Main](form-basics/samples/sample11.cs)]

<span data-ttu-id="9801f-354">此代码使用前面看到的相同逻辑，不同之处在于，搜索使用 `LIKE` 运算符，并且代码在搜索词前后放置 " `%` "。</span><span class="sxs-lookup"><span data-stu-id="9801f-354">This code uses the same logic you saw earlier, except that the search uses a `LIKE` operator and the code puts "`%`" before and after the search term.</span></span>

<span data-ttu-id="9801f-355">请注意如何轻松地向页面中添加另一个搜索。</span><span class="sxs-lookup"><span data-stu-id="9801f-355">Notice how it was easy to add another search to the page.</span></span> <span data-ttu-id="9801f-356">你需要做的只是：</span><span class="sxs-lookup"><span data-stu-id="9801f-356">All you had to do was:</span></span>

- <span data-ttu-id="9801f-357">创建 `if` 测试的块以查看相关搜索框是否具有值。</span><span class="sxs-lookup"><span data-stu-id="9801f-357">Create an `if` block that tested to see whether the relevant search box had a value.</span></span>
- <span data-ttu-id="9801f-358">将 `selectCommand` 变量设置为新的 SQL 语句。</span><span class="sxs-lookup"><span data-stu-id="9801f-358">Set the `selectCommand` variable to a new SQL statement.</span></span>
- <span data-ttu-id="9801f-359">将 `searchTerm` 变量设置为要传递给查询的值。</span><span class="sxs-lookup"><span data-stu-id="9801f-359">Set the `searchTerm` variable to the value to pass to the query.</span></span>

<span data-ttu-id="9801f-360">下面是完整的代码块，其中包含用于标题搜索的新逻辑：</span><span class="sxs-lookup"><span data-stu-id="9801f-360">Here's the complete code block, which contains the new logic for a title search:</span></span>

[!code-cshtml[Main](form-basics/samples/sample12.cshtml)]

<span data-ttu-id="9801f-361">下面总结了此代码的用途：</span><span class="sxs-lookup"><span data-stu-id="9801f-361">Here's a summary of what this code does:</span></span>

- <span data-ttu-id="9801f-362">变量 `searchTerm` 和在 `selectCommand` 顶部进行了初始化。</span><span class="sxs-lookup"><span data-stu-id="9801f-362">The variables `searchTerm` and `selectCommand` are initialized at the top.</span></span> <span data-ttu-id="9801f-363">) 如果根据用户在页面中执行的操作，将这些变量设置为相应的搜索词 (。</span><span class="sxs-lookup"><span data-stu-id="9801f-363">You're going to set these variables to the appropriate search term (if any) and appropriate SQL command based on what the user does in the page.</span></span> <span data-ttu-id="9801f-364">默认搜索是从数据库中获取所有电影的简单情况。</span><span class="sxs-lookup"><span data-stu-id="9801f-364">The default search is the simple case of getting all the movies from the database.</span></span>
- <span data-ttu-id="9801f-365">在和的测试 `searchGenre` 中 `searchTitle` ，代码设置 `searchTerm` 为要搜索的值。</span><span class="sxs-lookup"><span data-stu-id="9801f-365">In the tests for `searchGenre` and `searchTitle`, the code sets `searchTerm` to the value you want to search for.</span></span> <span data-ttu-id="9801f-366">对于该搜索，这些代码块也设置 `selectCommand` 为相应的 SQL 命令。</span><span class="sxs-lookup"><span data-stu-id="9801f-366">Those code blocks also set `selectCommand` to an appropriate SQL command for that search.</span></span>
- <span data-ttu-id="9801f-367">`db.Query`方法只调用一次，并使用任何 SQL 命令，并使用中的 `selectedCommand` 任何值 `searchTerm` 。</span><span class="sxs-lookup"><span data-stu-id="9801f-367">The `db.Query` method is invoked only once, using whatever SQL command is in `selectedCommand` and whatever value is in `searchTerm`.</span></span> <span data-ttu-id="9801f-368">如果没有搜索词 (没有流派，并且没有) 的标题字，则的值 `searchTerm` 是空字符串。</span><span class="sxs-lookup"><span data-stu-id="9801f-368">If there is no search term (no genre and no title word), the value of `searchTerm` is an empty string.</span></span> <span data-ttu-id="9801f-369">但这并不重要，因为在这种情况下，查询不需要参数。</span><span class="sxs-lookup"><span data-stu-id="9801f-369">However, that doesn't matter, because in that case the query doesn't require a parameter.</span></span>

## <a name="testing-the-title-search-feature"></a><span data-ttu-id="9801f-370">测试标题搜索功能</span><span class="sxs-lookup"><span data-stu-id="9801f-370">Testing the Title Search Feature</span></span>

<span data-ttu-id="9801f-371">现在可以测试已完成的搜索页面。</span><span class="sxs-lookup"><span data-stu-id="9801f-371">Now you can test your completed search page.</span></span> <span data-ttu-id="9801f-372">运行*Movies.cshtml*</span><span class="sxs-lookup"><span data-stu-id="9801f-372">Run *Movies.cshtml*.</span></span>

<span data-ttu-id="9801f-373">输入一个流派，然后单击 " **搜索流派**"。</span><span class="sxs-lookup"><span data-stu-id="9801f-373">Enter a genre and click **Search Genre**.</span></span> <span data-ttu-id="9801f-374">网格显示该流派的电影，就像之前一样。</span><span class="sxs-lookup"><span data-stu-id="9801f-374">The grid displays movies of that genre, like before.</span></span>

<span data-ttu-id="9801f-375">输入标题字，并单击 " **搜索标题**"。</span><span class="sxs-lookup"><span data-stu-id="9801f-375">Enter a title word and click **Search Title**.</span></span> <span data-ttu-id="9801f-376">网格显示在标题中包含该单词的影片。</span><span class="sxs-lookup"><span data-stu-id="9801f-376">The grid displays movies that have that word in the title.</span></span>

![搜索标题中的 "the" 后的电影页面列表](form-basics/_static/image6.png)

<span data-ttu-id="9801f-378">将这两个文本框留空，然后单击其中一个按钮。</span><span class="sxs-lookup"><span data-stu-id="9801f-378">Leave both text boxes blank and click either button.</span></span> <span data-ttu-id="9801f-379">网格显示所有电影。</span><span class="sxs-lookup"><span data-stu-id="9801f-379">The grid displays all the movies.</span></span>

## <a name="combining-the-queries"></a><span data-ttu-id="9801f-380">合并查询</span><span class="sxs-lookup"><span data-stu-id="9801f-380">Combining the Queries</span></span>

<span data-ttu-id="9801f-381">你可能会注意到，你可以执行的搜索是独占的。</span><span class="sxs-lookup"><span data-stu-id="9801f-381">You might notice that the searches you can perform are exclusive.</span></span> <span data-ttu-id="9801f-382">不能同时搜索标题和流派，即使两个搜索框中都有值。</span><span class="sxs-lookup"><span data-stu-id="9801f-382">You can't search the title and the genre at the same time, even if both search boxes have values in them.</span></span> <span data-ttu-id="9801f-383">例如，不能搜索标题包含 "艾德" 的所有操作电影。</span><span class="sxs-lookup"><span data-stu-id="9801f-383">For example, you can't search for all action movies whose title contains "Adventure".</span></span> <span data-ttu-id="9801f-384"> (在该页上进行编码时，如果为 "流派" 和 "标题" 输入值，则将优先搜索标题。 ) 若要创建组合条件的搜索，则必须创建包含如下语法的 SQL 查询：</span><span class="sxs-lookup"><span data-stu-id="9801f-384">(As the page is coded now, if you enter values for both genre and title, the title search gets precedence.) To create a search that combines the conditions, you would have to create a SQL query that has syntax like the following:</span></span>

`SELECT * FROM Movies WHERE Genre = @0 AND Title LIKE @1`

<span data-ttu-id="9801f-385">而且，您必须使用如下所示的语句来运行查询 (大致) ：</span><span class="sxs-lookup"><span data-stu-id="9801f-385">And you'd have to run the query by using a statement like the following (roughly speaking):</span></span>

`var selectedData = db.Query(selectCommand, searchGenre, searchTitle);`

<span data-ttu-id="9801f-386">正如您所看到的，创建逻辑以允许搜索条件的多个排列可能会很多。</span><span class="sxs-lookup"><span data-stu-id="9801f-386">Creating logic to allow many permutations of search criteria can get a bit involved, as you can see.</span></span> <span data-ttu-id="9801f-387">因此，我们将在此处停止。</span><span class="sxs-lookup"><span data-stu-id="9801f-387">Therefore, we'll stop here.</span></span>

## <a name="coming-up-next"></a><span data-ttu-id="9801f-388">下一步</span><span class="sxs-lookup"><span data-stu-id="9801f-388">Coming Up Next</span></span>

<span data-ttu-id="9801f-389">在下一教程中，您将创建一个使用窗体的页面，使用户能够将电影添加到数据库中。</span><span class="sxs-lookup"><span data-stu-id="9801f-389">In the next tutorial, you'll create a page that uses a form to let users add movies to the database.</span></span>

## <a name="complete-listing-for-movie-page-updated-with-search"></a><span data-ttu-id="9801f-390">通过搜索) 更新了电影页面 (的完整列表</span><span class="sxs-lookup"><span data-stu-id="9801f-390">Complete Listing for Movie Page (Updated with Search)</span></span>

[!code-cshtml[Main](form-basics/samples/sample13.cshtml)]

## <a name="additional-resources"></a><span data-ttu-id="9801f-391">其他资源</span><span class="sxs-lookup"><span data-stu-id="9801f-391">Additional Resources</span></span>

- [<span data-ttu-id="9801f-392">使用 Razor 语法进行 ASP.NET Web 编程简介</span><span class="sxs-lookup"><span data-stu-id="9801f-392">Introduction to ASP.NET Web Programming Using the Razor Syntax</span></span>](https://go.microsoft.com/fwlink/?LinkID=202890)
- <span data-ttu-id="9801f-393">W3Schools 站点上的[SQL WHERE 子句](http://www.w3schools.com/sql/sql_where.asp)</span><span class="sxs-lookup"><span data-stu-id="9801f-393">[SQL WHERE Clause](http://www.w3schools.com/sql/sql_where.asp) on the W3Schools site</span></span>
- <span data-ttu-id="9801f-394">W3C 网站上的[方法定义](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html)一文</span><span class="sxs-lookup"><span data-stu-id="9801f-394">[Method Definitions](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html) article on the W3C site</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="9801f-395">[上一页](displaying-data.md)
> [下一页](entering-data.md)</span><span class="sxs-lookup"><span data-stu-id="9801f-395">[Previous](displaying-data.md)
[Next](entering-data.md)</span></span>

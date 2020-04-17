---
uid: mvc/overview/older-versions-1/nerddinner/use-ajax-to-deliver-dynamic-updates
title: 使用 AJAX 提供动态更新 |微软文档
author: rick-anderson
description: 步骤 10 支持登录用户 RSVP，他们有兴趣参加晚宴，使用基于 Ajax 的方法集成在晚餐详细信息中...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 18700815-8e6c-4489-91af-7ea9dab6529e
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-ajax-to-deliver-dynamic-updates
msc.type: authoredcontent
ms.openlocfilehash: 13680b91edc665852fd4af56e4fc79551e6de15e
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541242"
---
# <a name="use-ajax-to-deliver-dynamic-updates"></a><span data-ttu-id="ff7a8-103">使用 AJAX 提供动态更新</span><span class="sxs-lookup"><span data-stu-id="ff7a8-103">Use AJAX to Deliver Dynamic Updates</span></span>

<span data-ttu-id="ff7a8-104">由[微软](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="ff7a8-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="ff7a8-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="ff7a8-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="ff7a8-106">这是一个免费的["NerdDinner"应用程序教程](introducing-the-nerddinner-tutorial.md)的第10步，该教程演示如何使用 ASP.NETmVC 1构建小型但完整的Web应用程序。</span><span class="sxs-lookup"><span data-stu-id="ff7a8-106">This is step 10 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="ff7a8-107">步骤 10 使用在晚餐详细信息页中集成的基于 Ajax 的方法，实现对登录用户的支持，以便 RSVP 让他们对参加晚宴感兴趣。</span><span class="sxs-lookup"><span data-stu-id="ff7a8-107">Step 10 implements support for logged-in users to RSVP their interest in attending a dinner, using an Ajax-based approach integrated within the dinner details page.</span></span>
> 
> <span data-ttu-id="ff7a8-108">如果您使用的是ASP.NET MVC 3，我们建议您按照[MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC 音乐商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程进行操作。</span><span class="sxs-lookup"><span data-stu-id="ff7a8-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-10-ajax-enabling-rsvps-accepts"></a><span data-ttu-id="ff7a8-109">神经晚餐步骤 10： AJAX 启用 RSV 接受</span><span class="sxs-lookup"><span data-stu-id="ff7a8-109">NerdDinner Step 10: AJAX Enabling RSVPs Accepts</span></span>

<span data-ttu-id="ff7a8-110">现在，让我们对登录用户实施支持，以便 RSVP 对参加晚宴感兴趣。</span><span class="sxs-lookup"><span data-stu-id="ff7a8-110">Let's now implement support for logged-in users to RSVP their interest in attending a dinner.</span></span> <span data-ttu-id="ff7a8-111">我们将使用在晚餐详细信息页中集成的基于 AJAX 的方法启用此功能。</span><span class="sxs-lookup"><span data-stu-id="ff7a8-111">We'll enable this using an AJAX-based approach integrated within the dinner details page.</span></span>

### <a name="indicating-whether-the-user-is-rsvpd"></a><span data-ttu-id="ff7a8-112">指示用户是否为 RSVP'd</span><span class="sxs-lookup"><span data-stu-id="ff7a8-112">Indicating whether the user is RSVP'd</span></span>

<span data-ttu-id="ff7a8-113">用户可以访问 */Dinners/详细信息/[id]* URL 以查看有关特定晚餐的详细信息：</span><span class="sxs-lookup"><span data-stu-id="ff7a8-113">Users can visit the */Dinners/Details/[id*] URL to see details about a particular dinner:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image1.png)

<span data-ttu-id="ff7a8-114">详细信息（）操作方法的实现方式是这样的：</span><span class="sxs-lookup"><span data-stu-id="ff7a8-114">The Details() action method is implemented like so:</span></span>

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample1.cs)]

<span data-ttu-id="ff7a8-115">实现 RSVP 支持的第一步是向我们的 Dinner 对象（在之前构建的Dinner.cs部分类中）添加"IsUser 注册（用户名）"帮助器方法。</span><span class="sxs-lookup"><span data-stu-id="ff7a8-115">Our first step to implement RSVP support will be to add an "IsUserRegistered(username)" helper method to our Dinner object (within the Dinner.cs partial class we built earlier).</span></span> <span data-ttu-id="ff7a8-116">此帮助程序方法返回 true 或 false，具体取决于用户当前是晚餐的 RSVP d：</span><span class="sxs-lookup"><span data-stu-id="ff7a8-116">This helper method returns true or false depending on whether the user is currently RSVP'd for the Dinner:</span></span>

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample2.cs)]

<span data-ttu-id="ff7a8-117">然后，我们可以向 Details.aspx 视图模板添加以下代码，以显示指示用户是否已注册的事件的适当消息：</span><span class="sxs-lookup"><span data-stu-id="ff7a8-117">We can then add the following code to our Details.aspx view template to display an appropriate message indicating whether the user is registered or not for the event:</span></span>

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample3.html)]

<span data-ttu-id="ff7a8-118">现在，当用户访问他们注册的晚餐时，他们会看到此消息：</span><span class="sxs-lookup"><span data-stu-id="ff7a8-118">And now when a user visits a Dinner they are registered for they'll see this message:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image2.png)

<span data-ttu-id="ff7a8-119">当他们访问晚餐时，他们没有注册，他们会看到以下消息：</span><span class="sxs-lookup"><span data-stu-id="ff7a8-119">And when they visit a Dinner they are not registered for they'll see the below message:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image3.png)

### <a name="implementing-the-register-action-method"></a><span data-ttu-id="ff7a8-120">实现寄存器操作方法</span><span class="sxs-lookup"><span data-stu-id="ff7a8-120">Implementing the Register Action Method</span></span>

<span data-ttu-id="ff7a8-121">现在，让我们添加必要的功能，使用户能够从详细信息页面到 RSVP 共进晚餐。</span><span class="sxs-lookup"><span data-stu-id="ff7a8-121">Let's now add the functionality necessary to enable users to RSVP for a dinner from the details page.</span></span>

<span data-ttu-id="ff7a8-122">为了实现这一点，我们将通过右键单击 \控制器目录并选择"添加控制器&gt;"菜单命令创建新的"RSVPController"类。</span><span class="sxs-lookup"><span data-stu-id="ff7a8-122">To implement this, we'll create a new "RSVPController" class by right-clicking on the \Controllers directory and choosing the Add-&gt;Controller menu command.</span></span>

<span data-ttu-id="ff7a8-123">我们将在新的 RSVPController 类中实现"注册"操作方法，该方法以 Dinner 的 ID 作为参数，检索相应的 Dinner 对象，检查登录用户当前是否位于已注册的用户列表中，如果没有为其添加 RSVP 对象：</span><span class="sxs-lookup"><span data-stu-id="ff7a8-123">We'll implement a "Register" action method within the new RSVPController class that takes an id for a Dinner as an argument, retrieves the appropriate Dinner object, checks to see if the logged-in user is currently in the list of users who have registered for it, and if not adds an RSVP object for them:</span></span>

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample4.cs)]

<span data-ttu-id="ff7a8-124">请注意，我们如何返回一个简单的字符串作为操作方法的输出。</span><span class="sxs-lookup"><span data-stu-id="ff7a8-124">Notice above how we are returning a simple string as the output of the action method.</span></span> <span data-ttu-id="ff7a8-125">我们本可以将此消息嵌入到视图模板中 ，但由于它非常小，我们只需在控制器基类上使用 Content（） 帮助器方法，并返回如下所示的字符串消息。</span><span class="sxs-lookup"><span data-stu-id="ff7a8-125">We could have embedded this message within a view template – but since it is so small we'll just use the Content() helper method on the controller base class and return a string message like above.</span></span>

### <a name="calling-the-rsvpforevent-action-method-using-ajax"></a><span data-ttu-id="ff7a8-126">使用 AJAX 调用 RSVPForEvent 操作方法</span><span class="sxs-lookup"><span data-stu-id="ff7a8-126">Calling the RSVPForEvent Action Method using AJAX</span></span>

<span data-ttu-id="ff7a8-127">我们将使用 AJAX 从"详细信息"视图中调用注册操作方法。</span><span class="sxs-lookup"><span data-stu-id="ff7a8-127">We'll use AJAX to invoke the Register action method from our Details view.</span></span> <span data-ttu-id="ff7a8-128">实现这一点非常简单。</span><span class="sxs-lookup"><span data-stu-id="ff7a8-128">Implementing this is pretty easy.</span></span> <span data-ttu-id="ff7a8-129">首先，我们将添加两个脚本库引用：</span><span class="sxs-lookup"><span data-stu-id="ff7a8-129">First we'll add two script library references:</span></span>

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample5.html)]

<span data-ttu-id="ff7a8-130">第一个库引用 ASP.NET AJAX 客户端脚本库的核心。</span><span class="sxs-lookup"><span data-stu-id="ff7a8-130">The first library references the core ASP.NET AJAX client-side script library.</span></span> <span data-ttu-id="ff7a8-131">此文件的大小约为 24k（压缩），包含核心客户端 AJAX 功能。</span><span class="sxs-lookup"><span data-stu-id="ff7a8-131">This file is approximately 24k in size (compressed) and contains core client-side AJAX functionality.</span></span> <span data-ttu-id="ff7a8-132">第二个库包含与ASP.NET MVC 的内置 AJAX 帮助器方法集成的实用程序函数（我们稍后会使用）。</span><span class="sxs-lookup"><span data-stu-id="ff7a8-132">The second library contains utility functions that integrate with ASP.NET MVC's built-in AJAX helper methods (which we'll use shortly).</span></span>

<span data-ttu-id="ff7a8-133">然后，我们可以更新我们之前添加的视图模板代码，以便我们不是提供"您未注册此事件"消息，而是呈现一个链接，当推送时执行 AJAX 调用时，该链接会调用我们的 RSVPForEvent 操作方法，并在用户中调用 RSVP：</span><span class="sxs-lookup"><span data-stu-id="ff7a8-133">We can then update the view template code we added earlier so that instead of outputting a "You are not registered for this event" message, we instead render a link that when pushed performs an AJAX call that invokes our RSVPForEvent action method on our RSVP controller and RSVPs the user:</span></span>

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample6.aspx)]

<span data-ttu-id="ff7a8-134">上面使用的Ajax.ActionLink（） 帮助器方法内置于mVCASP.NET，与 Html.ActionLink（） 帮助器方法类似，只不过，在单击链接时，它不是执行标准导航，而是对操作方法发出 AJAX 调用。</span><span class="sxs-lookup"><span data-stu-id="ff7a8-134">The Ajax.ActionLink() helper method used above is built-into ASP.NET MVC and is similar to the Html.ActionLink() helper method except that instead of performing a standard navigation it makes an AJAX call to the action method when the link is clicked.</span></span> <span data-ttu-id="ff7a8-135">上面我们调用"RSVP"控制器上的"注册"操作方法，并将 DinnerID 作为"id"参数传递给它。</span><span class="sxs-lookup"><span data-stu-id="ff7a8-135">Above we are calling the "Register" action method on the "RSVP" controller and passing the DinnerID as the "id" parameter to it.</span></span> <span data-ttu-id="ff7a8-136">我们传递的最终 AjaxOptions 参数表示，我们希望获取从操作方法返回的内容，并更新 ID 为"rsvpmsg"的页面上的 HTML &lt;div&gt;元素。</span><span class="sxs-lookup"><span data-stu-id="ff7a8-136">The final AjaxOptions parameter we are passing indicates that we want to take the content returned from the action method and update the HTML &lt;div&gt; element on the page whose id is "rsvpmsg".</span></span>

<span data-ttu-id="ff7a8-137">现在，当用户浏览到尚未注册的晚餐时，他们会看到指向 RSVP 的链接：</span><span class="sxs-lookup"><span data-stu-id="ff7a8-137">And now when a user browses to a dinner they aren't registered for yet they'll see a link to RSVP for it:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image4.png)

<span data-ttu-id="ff7a8-138">如果他们单击"此事件的 RSVP"链接，他们将对 RSVP 控制器上的注册操作方法进行 AJAX 调用，并且当它完成后，他们将看到如下更新的消息：</span><span class="sxs-lookup"><span data-stu-id="ff7a8-138">If they click the "RSVP for this event" link they'll make an AJAX call to the Register action method on the RSVP controller, and when it completes they'll see an updated message like below:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image5.png)

<span data-ttu-id="ff7a8-139">进行此 AJAX 调用时所涉及的网络带宽和流量非常轻量。</span><span class="sxs-lookup"><span data-stu-id="ff7a8-139">The network bandwidth and traffic involved when making this AJAX call is really lightweight.</span></span> <span data-ttu-id="ff7a8-140">当用户单击"此事件的 RSVP"链接时，将针对在线路上如下所示的 */Dinners/Register/1* URL 发出小型 HTTP POST 网络请求：</span><span class="sxs-lookup"><span data-stu-id="ff7a8-140">When the user clicks on the "RSVP for this event" link, a small HTTP POST network request is made to the */Dinners/Register/1* URL that looks like below on the wire:</span></span>

[!code-console[Main](use-ajax-to-deliver-dynamic-updates/samples/sample7.cmd)]

<span data-ttu-id="ff7a8-141">我们的注册操作方法的响应很简单：</span><span class="sxs-lookup"><span data-stu-id="ff7a8-141">And the response from our Register action method is simply:</span></span>

[!code-console[Main](use-ajax-to-deliver-dynamic-updates/samples/sample8.cmd)]

<span data-ttu-id="ff7a8-142">此轻量级呼叫速度很快，即使在速度较慢的网络上也能正常工作。</span><span class="sxs-lookup"><span data-stu-id="ff7a8-142">This lightweight call is fast and will work even over a slow network.</span></span>

### <a name="adding-a-jquery-animation"></a><span data-ttu-id="ff7a8-143">添加 jQuery 动画</span><span class="sxs-lookup"><span data-stu-id="ff7a8-143">Adding a jQuery Animation</span></span>

<span data-ttu-id="ff7a8-144">我们实现的AJAX功能工作良好，速度快。</span><span class="sxs-lookup"><span data-stu-id="ff7a8-144">The AJAX functionality we implemented works well and fast.</span></span> <span data-ttu-id="ff7a8-145">但是，有时发生得如此之快，以至于用户可能没有注意到 RSVP 链接已被新文本替换。</span><span class="sxs-lookup"><span data-stu-id="ff7a8-145">Sometimes it can happen so fast, though, that a user might not notice that the RSVP link has been replaced with new text.</span></span> <span data-ttu-id="ff7a8-146">为了使结果更加明显一点，我们可以添加一个简单的动画来吸引对更新消息的注意。</span><span class="sxs-lookup"><span data-stu-id="ff7a8-146">To make the outcome a little more obvious we can add a simple animation to draw attention to the update message.</span></span>

<span data-ttu-id="ff7a8-147">默认ASP.NET MVC 项目模板包括 jQuery - 一个出色的（非常受欢迎的）开源 JavaScript 库，也受 Microsoft 支持。</span><span class="sxs-lookup"><span data-stu-id="ff7a8-147">The default ASP.NET MVC project template includes jQuery – an excellent (and very popular) open source JavaScript library that is also supported by Microsoft.</span></span> <span data-ttu-id="ff7a8-148">jQuery 提供了许多功能，包括不错的 HTML DOM 选择和效果库。</span><span class="sxs-lookup"><span data-stu-id="ff7a8-148">jQuery provides a number of features, including a nice HTML DOM selection and effects library.</span></span>

<span data-ttu-id="ff7a8-149">要使用 jQuery，我们将首先向其添加脚本引用。</span><span class="sxs-lookup"><span data-stu-id="ff7a8-149">To use jQuery we'll first add a script reference to it.</span></span> <span data-ttu-id="ff7a8-150">由于我们将在网站内的各种位置使用 jQuery，因此我们将在 Site.master 页面文件中添加脚本引用，以便所有页面都可以使用它。</span><span class="sxs-lookup"><span data-stu-id="ff7a8-150">Because we are going to be using jQuery within a variety of places within our site, we'll add the script reference within our Site.master master page file so that all pages can use it.</span></span>

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample9.html)]

<span data-ttu-id="ff7a8-151">*提示：请确保您已为 VS 2008 SP1 安装了 JavaScript 智能感知修补程序，从而能够对 JavaScript 文件（包括 jQuery）提供更丰富的对讲义支持。您可以通过以下位置下载：http://tinyurl.com/vs2008javascripthotfix*</span><span class="sxs-lookup"><span data-stu-id="ff7a8-151">*Tip: make sure you have installed the JavaScript intellisense hotfix for VS 2008 SP1 that enables richer intellisense support for JavaScript files (including jQuery). You can download it from: http://tinyurl.com/vs2008javascripthotfix*</span></span>

<span data-ttu-id="ff7a8-152">使用 JQuery 编写的代码通常使用全局"$（）"JavaScript 方法，该方法使用 CSS 选择器检索一个或多个 HTML 元素。</span><span class="sxs-lookup"><span data-stu-id="ff7a8-152">Code written using JQuery often uses a global "$()" JavaScript method that retrieves one or more HTML elements using a CSS selector.</span></span> <span data-ttu-id="ff7a8-153">例如 *，$（"#rsvpmsg"）* 选择任何具有 rsvpmsg ID 的 HTML 元素，而 *$（".某事"）* 将选择具有"某物"CSS 类名称的所有元素。</span><span class="sxs-lookup"><span data-stu-id="ff7a8-153">For example, *$("#rsvpmsg")* selects any HTML element with the id of rsvpmsg, while *$(".something")* would select all elements with the "something" CSS class name.</span></span> <span data-ttu-id="ff7a8-154">您还可以使用选择器查询编写更高级的查询，如"返回所有已检查的单选按钮"，例如 *：$（"输入="@type收音机\*\*）"。@checked*</span><span class="sxs-lookup"><span data-stu-id="ff7a8-154">You can also write more advanced queries like "return all of the checked radio buttons" using a selector query like: *$("input[@type=radio][@checked]")*.</span></span>

<span data-ttu-id="ff7a8-155">选择元素后，可以调用方法对它们执行操作，例如隐藏它们 *：$（"#rsvpmsg"）。"隐藏";*</span><span class="sxs-lookup"><span data-stu-id="ff7a8-155">Once you've selected elements, you can call methods on them to take action, like hiding them: *$("#rsvpmsg").hide();*</span></span>

<span data-ttu-id="ff7a8-156">对于我们的 RSVP 方案，我们将定义一个名为"AnimateRSVPMessage"的简单 JavaScript 函数，该函数选择"rsvpmsg"div&lt;&gt;并为其文本内容的大小设置动画。</span><span class="sxs-lookup"><span data-stu-id="ff7a8-156">For our RSVP scenario, we'll define a simple JavaScript function named "AnimateRSVPMessage" that selects the "rsvpmsg" &lt;div&gt; and animates the size of its text content.</span></span> <span data-ttu-id="ff7a8-157">下面的代码将文本启动较小，然后使其在 400 毫秒的时间内增加：</span><span class="sxs-lookup"><span data-stu-id="ff7a8-157">The below code starts the text small and then causes it to increase over a 400 milliseconds timeframe:</span></span>

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample10.html)]

<span data-ttu-id="ff7a8-158">然后，我们可以通过将其名称传递给我们的Ajax.ActionLink（） 帮助器方法（通过AjaxOptions"OnSuccess"事件属性）来连接此 JavaScript 函数，以在 AJAX 调用成功完成后调用它：</span><span class="sxs-lookup"><span data-stu-id="ff7a8-158">We can then wire-up this JavaScript function to be called after our AJAX call successfully completes by passing its name to our Ajax.ActionLink() helper method (via the AjaxOptions "OnSuccess" event property):</span></span>

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample11.aspx)]

<span data-ttu-id="ff7a8-159">现在，当单击"此事件的 RSVP"链接并成功完成我们的 AJAX 呼叫时，发回的内容消息将设置动画并变大：</span><span class="sxs-lookup"><span data-stu-id="ff7a8-159">And now when the "RSVP for this event" link is clicked and our AJAX call completes successfully, the content message sent back will animate and grow large:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image6.png)

<span data-ttu-id="ff7a8-160">除了提供"On成功"事件外，AjaxOptions 对象还公开了您可以处理的 OnBegin、OnOn 失败和 OnComplete 事件（以及各种其他属性和有用的选项）。</span><span class="sxs-lookup"><span data-stu-id="ff7a8-160">In addition to providing an "OnSuccess" event, the AjaxOptions object exposes OnBegin, OnFailure, and OnComplete events that you can handle (along with a variety of other properties and useful options).</span></span>

### <a name="cleanup---refactor-out-a-rsvp-partial-view"></a><span data-ttu-id="ff7a8-161">清理 - 重构 RSVP 部分视图</span><span class="sxs-lookup"><span data-stu-id="ff7a8-161">Cleanup - Refactor out a RSVP Partial View</span></span>

<span data-ttu-id="ff7a8-162">我们的详细信息视图模板开始变得有点长，加班会使它很难理解。</span><span class="sxs-lookup"><span data-stu-id="ff7a8-162">Our details view template is starting to get a little long, which overtime will make it a little harder to understand.</span></span> <span data-ttu-id="ff7a8-163">为了帮助提高代码的可读性，让我们通过创建一个部分视图 （ RSVPStatus.ascx） 来完成，该视图封装了我们详细信息页的所有 RSVP 视图代码。</span><span class="sxs-lookup"><span data-stu-id="ff7a8-163">To help improve the code readability, let's finish up by creating a partial view – RSVPStatus.ascx – that encapsulate all of the RSVP view code for our Details page.</span></span>

<span data-ttu-id="ff7a8-164">我们可以通过右键单击 [Views_Dinners] 文件夹，然后选择"添加-&gt;视图"菜单命令来执行此操作。</span><span class="sxs-lookup"><span data-stu-id="ff7a8-164">We can do this by right-clicking on the \Views\Dinners folder and then choosing the Add-&gt;View menu command.</span></span> <span data-ttu-id="ff7a8-165">我们将它采用晚餐对象作为其强类型视图模型。</span><span class="sxs-lookup"><span data-stu-id="ff7a8-165">We'll have it take a Dinner object as its strongly-typed ViewModel.</span></span> <span data-ttu-id="ff7a8-166">然后，我们可以复制/粘贴从我们的细节.aspx 视图的 RSVP 内容到它。</span><span class="sxs-lookup"><span data-stu-id="ff7a8-166">We can then copy/paste the RSVP content from our Details.aspx view into it.</span></span>

<span data-ttu-id="ff7a8-167">完成此操作后，我们还要创建另一个部分视图 - EditAndDeleteLinks.ascx - 封装我们的"编辑"和"删除"链接视图代码。</span><span class="sxs-lookup"><span data-stu-id="ff7a8-167">Once we've done that, let's also create another partial view – EditAndDeleteLinks.ascx - that encapsulates our Edit and Delete link view code.</span></span> <span data-ttu-id="ff7a8-168">我们还将它将一个 Dinner 对象作为其强类型视图模型，并将"编辑"和"删除"逻辑从"详细信息.aspx"视图中复制/粘贴到该对象中。</span><span class="sxs-lookup"><span data-stu-id="ff7a8-168">We'll also have it take a Dinner object as its strongly-typed ViewModel, and copy/paste the Edit and Delete logic from our Details.aspx view into it.</span></span>

<span data-ttu-id="ff7a8-169">然后，我们的详细信息视图模板可以只包括底部的两个 Html.Render 部分（） 方法调用：</span><span class="sxs-lookup"><span data-stu-id="ff7a8-169">Our details view template can then just include two Html.RenderPartial() method calls at the bottom:</span></span>

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample12.aspx)]

<span data-ttu-id="ff7a8-170">这使得代码的读取和维护更简洁。</span><span class="sxs-lookup"><span data-stu-id="ff7a8-170">This makes the code cleaner to read and maintain.</span></span>

### <a name="next-step"></a><span data-ttu-id="ff7a8-171">下一步</span><span class="sxs-lookup"><span data-stu-id="ff7a8-171">Next Step</span></span>

<span data-ttu-id="ff7a8-172">现在，让我们来看看如何进一步使用AJAX，并将交互式映射支持添加到我们的应用程序。</span><span class="sxs-lookup"><span data-stu-id="ff7a8-172">Let's now look at how we can use AJAX even further and add interactive mapping support to our application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="ff7a8-173">[上一页](secure-applications-using-authentication-and-authorization.md)
> [下一页](use-ajax-to-implement-mapping-scenarios.md)</span><span class="sxs-lookup"><span data-stu-id="ff7a8-173">[Previous](secure-applications-using-authentication-and-authorization.md)
[Next](use-ajax-to-implement-mapping-scenarios.md)</span></span>

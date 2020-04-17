---
uid: mvc/overview/older-versions-1/nerddinner/re-use-ui-using-master-pages-and-partials
title: 使用母版页和部分重用 UI |微软文档
author: rick-anderson
description: 步骤 7 探讨了在视图模板中应用"DRY 原则"的方法，以便使用部分视图模板和母版页来消除代码重复。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: d4243a4a-e91c-4116-9ae0-5c08e5285677
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/re-use-ui-using-master-pages-and-partials
msc.type: authoredcontent
ms.openlocfilehash: f381c4424a9fa0718cd234beeb01ce41bc4ca61e
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542594"
---
# <a name="re-use-ui-using-master-pages-and-partials"></a><span data-ttu-id="b6ba0-103">使用母版页和部分重用 UI</span><span class="sxs-lookup"><span data-stu-id="b6ba0-103">Re-use UI Using Master Pages and Partials</span></span>

<span data-ttu-id="b6ba0-104">由[微软](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="b6ba0-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="b6ba0-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="b6ba0-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="b6ba0-106">这是一个免费的["NerdDinner"应用程序教程](introducing-the-nerddinner-tutorial.md)的第7步，该教程演示如何使用ASP.NET MVC 1 构建小型但完整的 Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="b6ba0-106">This is step 7 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="b6ba0-107">步骤 7 探讨了在视图模板中应用"DRY 原则"的方法，以便使用部分视图模板和母版页来消除代码重复。</span><span class="sxs-lookup"><span data-stu-id="b6ba0-107">Step 7 looks at ways we can apply the "DRY Principle" within our view templates to eliminate code duplication, using partial view templates and master pages.</span></span>
> 
> <span data-ttu-id="b6ba0-108">如果您使用的是ASP.NET MVC 3，我们建议您按照[MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC 音乐商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程进行操作。</span><span class="sxs-lookup"><span data-stu-id="b6ba0-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-7-partials-and-master-pages"></a><span data-ttu-id="b6ba0-109">神经晚餐步骤 7：部分和母版页</span><span class="sxs-lookup"><span data-stu-id="b6ba0-109">NerdDinner Step 7: Partials and Master Pages</span></span>

<span data-ttu-id="b6ba0-110">MVC 拥抱ASP.NET的设计理念之一是"不要重复自己"原则（通常称为"DRY"）。</span><span class="sxs-lookup"><span data-stu-id="b6ba0-110">One of the design philosophies ASP.NET MVC embraces is the "Do Not Repeat Yourself" principle (commonly referred to as "DRY").</span></span> <span data-ttu-id="b6ba0-111">DRY 设计有助于消除代码和逻辑的重复，最终使应用程序构建速度更快，更易于维护。</span><span class="sxs-lookup"><span data-stu-id="b6ba0-111">A DRY design helps eliminate the duplication of code and logic, which ultimately makes applications faster to build and easier to maintain.</span></span>

<span data-ttu-id="b6ba0-112">我们已经看到 DRY 原则应用于我们的一些 NerdDinner 方案。</span><span class="sxs-lookup"><span data-stu-id="b6ba0-112">We've already seen the DRY principle applied in several of our NerdDinner scenarios.</span></span> <span data-ttu-id="b6ba0-113">举几个例子：我们的验证逻辑在我们的模型层中实现，这使得它可以在控制器中编辑和创建方案之间强制执行;我们正在跨"编辑"、"详细信息"和"删除"操作方法重用"未找到"视图模板;我们使用具有视图模板的约定命名模式，这样无需在调用 View（） 帮助器方法时显式指定名称;我们正在重新使用 DinnerFormViewModel 类进行编辑和创建操作方案。</span><span class="sxs-lookup"><span data-stu-id="b6ba0-113">A few examples: our validation logic is implemented within our model layer, which enables it to be enforced across both edit and create scenarios in our controller; we are re-using the "NotFound" view template across the Edit, Details and Delete action methods; we are using a convention- naming pattern with our view templates, which eliminates the need to explicitly specify the name when we call the View() helper method; and we are re-using the DinnerFormViewModel class for both Edit and Create action scenarios.</span></span>

<span data-ttu-id="b6ba0-114">现在，让我们来看看如何在我们的视图模板中应用"DRY 原则"，以消除代码重复。</span><span class="sxs-lookup"><span data-stu-id="b6ba0-114">Let's now look at ways we can apply the "DRY Principle" within our view templates to eliminate code duplication there as well.</span></span>

### <a name="re-visiting-our-edit-and-create-view-templates"></a><span data-ttu-id="b6ba0-115">重新访问我们的编辑和创建视图模板</span><span class="sxs-lookup"><span data-stu-id="b6ba0-115">Re-visiting our Edit and Create View Templates</span></span>

<span data-ttu-id="b6ba0-116">目前，我们使用两个不同的视图模板 - "Edit.aspx"和"Create.aspx" - 以显示我们的晚餐表单 UI。</span><span class="sxs-lookup"><span data-stu-id="b6ba0-116">Currently we are using two different view templates – "Edit.aspx" and "Create.aspx" – to display our Dinner form UI.</span></span> <span data-ttu-id="b6ba0-117">快速直观地比较它们，突出显示它们有多相似。</span><span class="sxs-lookup"><span data-stu-id="b6ba0-117">A quick visual comparison of them highlights how similar they are.</span></span> <span data-ttu-id="b6ba0-118">下面是创建窗体的外观：</span><span class="sxs-lookup"><span data-stu-id="b6ba0-118">Below is what the create form looks like:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image1.png)

<span data-ttu-id="b6ba0-119">下面是我们的"编辑"窗体的外观：</span><span class="sxs-lookup"><span data-stu-id="b6ba0-119">And here is what our "Edit" form looks like:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image2.png)

<span data-ttu-id="b6ba0-120">没有什么区别吗？</span><span class="sxs-lookup"><span data-stu-id="b6ba0-120">Not much of a difference is there?</span></span> <span data-ttu-id="b6ba0-121">除了标题和标题文本之外，窗体布局和输入控件是相同的。</span><span class="sxs-lookup"><span data-stu-id="b6ba0-121">Other than the title and header text, the form layout and input controls are identical.</span></span>

<span data-ttu-id="b6ba0-122">如果我们打开"Edit.aspx"和"Create.aspx"视图模板，我们会发现它们包含相同的表单布局和输入控制代码。</span><span class="sxs-lookup"><span data-stu-id="b6ba0-122">If we open up the "Edit.aspx" and "Create.aspx" view templates we'll find that they contain identical form layout and input control code.</span></span> <span data-ttu-id="b6ba0-123">这种重复意味着我们最终必须作出两次更改，每当我们介绍或改变一个新的晚餐属性 - 这是不好的。</span><span class="sxs-lookup"><span data-stu-id="b6ba0-123">This duplication means we end up having to make changes twice anytime we introduce or change a new Dinner property - which is not good.</span></span>

### <a name="using-partial-view-templates"></a><span data-ttu-id="b6ba0-124">使用部分视图模板</span><span class="sxs-lookup"><span data-stu-id="b6ba0-124">Using Partial View Templates</span></span>

<span data-ttu-id="b6ba0-125">mVC ASP.NET支持定义可用于封装页面子部分的视图呈现逻辑的"部分视图"模板的能力。</span><span class="sxs-lookup"><span data-stu-id="b6ba0-125">ASP.NET MVC supports the ability to define "partial view" templates that can be used to encapsulate view rendering logic for a sub-portion of a page.</span></span> <span data-ttu-id="b6ba0-126">"部分"提供了一种有用的方法来定义一次视图呈现逻辑，然后在应用程序之间的多个位置重用它。</span><span class="sxs-lookup"><span data-stu-id="b6ba0-126">"Partials" provide a useful way to define view rendering logic once, and then re-use it in multiple places across an application.</span></span>

<span data-ttu-id="b6ba0-127">为了帮助"DRYup"我们的 Edit.aspx 和 Create.aspx 视图模板复制，我们可以创建名为"DinnerForm.ascx"的部分视图模板，该模板封装了两者共有的窗体布局和输入元素。</span><span class="sxs-lookup"><span data-stu-id="b6ba0-127">To help "DRY-up" our Edit.aspx and Create.aspx view template duplication, we can create a partial view template named "DinnerForm.ascx" that encapsulates the form layout and input elements common to both.</span></span> <span data-ttu-id="b6ba0-128">我们将通过右键单击 /Views/Dinners 目录并选择"添加-&gt;视图"菜单命令来执行此操作：</span><span class="sxs-lookup"><span data-stu-id="b6ba0-128">We'll do this by right-clicking on our /Views/Dinners directory and choosing the "Add-&gt;View" menu command:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image3.png)

<span data-ttu-id="b6ba0-129">这将显示"添加视图"对话框。</span><span class="sxs-lookup"><span data-stu-id="b6ba0-129">This will display the "Add View" dialog.</span></span> <span data-ttu-id="b6ba0-130">我们将命名要创建"DinnerForm"的新视图，在对话框中选择"创建部分视图"复选框，并指示我们将传递一个 DinnerFormViewModel 类：</span><span class="sxs-lookup"><span data-stu-id="b6ba0-130">We'll name the new view we want to create "DinnerForm", select the "Create a partial view" checkbox within the dialog, and indicate that we will pass it a DinnerFormViewModel class:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image4.png)

<span data-ttu-id="b6ba0-131">当我们单击"添加"按钮时，Visual Studio 将在"@Views_Dinners"目录中为我们创建新的"DinnerForm.ascx"视图模板。</span><span class="sxs-lookup"><span data-stu-id="b6ba0-131">When we click the "Add" button, Visual Studio will create a new "DinnerForm.ascx" view template for us within the "\Views\Dinners" directory.</span></span>

<span data-ttu-id="b6ba0-132">然后，我们可以将重复的表单布局/输入控制代码从我们的 Edit.aspx/ Create.aspx 视图模板复制/粘贴到新的"DinnerForm.ascx"部分视图模板中：</span><span class="sxs-lookup"><span data-stu-id="b6ba0-132">We can then copy/paste the duplicate form layout / input control code from our Edit.aspx/ Create.aspx view templates into our new "DinnerForm.ascx" partial view template:</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample1.aspx)]

<span data-ttu-id="b6ba0-133">然后，我们可以更新我们的"编辑"和"创建"视图模板，以调用 DinnerForm 部分模板并消除表单复制。</span><span class="sxs-lookup"><span data-stu-id="b6ba0-133">We can then update our Edit and Create view templates to call the DinnerForm partial template and eliminate the form duplication.</span></span> <span data-ttu-id="b6ba0-134">我们可以在视图模板中调用 Html.Render 部分（"DinnerForm"）来执行此操作：</span><span class="sxs-lookup"><span data-stu-id="b6ba0-134">We can do this by calling Html.RenderPartial("DinnerForm") within our view templates:</span></span>

##### <a name="createaspx"></a><span data-ttu-id="b6ba0-135">创建.aspx</span><span class="sxs-lookup"><span data-stu-id="b6ba0-135">Create.aspx</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample2.aspx)]

##### <a name="editaspx"></a><span data-ttu-id="b6ba0-136">编辑.aspx</span><span class="sxs-lookup"><span data-stu-id="b6ba0-136">Edit.aspx</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample3.aspx)]

<span data-ttu-id="b6ba0-137">在调用 Html.Render 部分（例如：\*视图/Dinners/DinnerForm.ascx）时，您可以显式限定所需的部分模板的路径。</span><span class="sxs-lookup"><span data-stu-id="b6ba0-137">You can explicitly qualify the path of the partial template you want when calling Html.RenderPartial (for example: ~Views/Dinners/DinnerForm.ascx").</span></span> <span data-ttu-id="b6ba0-138">但是，在上面的代码中，我们利用了 mVC ASP.NET中基于约定的命名模式，并将"DinnerForm"指定为要呈现的部分名称。</span><span class="sxs-lookup"><span data-stu-id="b6ba0-138">In our code above, though, we are taking advantage of the convention-based naming pattern within ASP.NET MVC, and just specifying "DinnerForm" as the name of the partial to render.</span></span> <span data-ttu-id="b6ba0-139">当我们这样做时ASP.NET MVC 将首先查看基于约定的视图目录（对于 DinnerSController，这将是 /视图/晚餐）。</span><span class="sxs-lookup"><span data-stu-id="b6ba0-139">When we do this ASP.NET MVC will look first in the convention-based views directory (for DinnersController this would be /Views/Dinners).</span></span> <span data-ttu-id="b6ba0-140">如果找不到部分模板，它将在 /Views/共享目录中查找它。</span><span class="sxs-lookup"><span data-stu-id="b6ba0-140">If it doesn't find the partial template there it will then look for it in the /Views/Shared directory.</span></span>

<span data-ttu-id="b6ba0-141">当仅使用部分视图的名称调用 Html.Render 部分（）时，ASP.NET MVC 将传递给调用视图模板使用的相同模型和 ViewData 字典对象。</span><span class="sxs-lookup"><span data-stu-id="b6ba0-141">When Html.RenderPartial() is called with just the name of the partial view, ASP.NET MVC will pass to the partial view the same Model and ViewData dictionary objects used by the calling view template.</span></span> <span data-ttu-id="b6ba0-142">或者，有重载版本的 Html.Render偏（）使您能够传递备用模型对象和/或 ViewData 字典供部分视图使用。</span><span class="sxs-lookup"><span data-stu-id="b6ba0-142">Alternatively, there are overloaded versions of Html.RenderPartial() that enable you to pass an alternate Model object and/or ViewData dictionary for the partial view to use.</span></span> <span data-ttu-id="b6ba0-143">这对于只想传递完整模型/视图模型子集的方案非常有用。</span><span class="sxs-lookup"><span data-stu-id="b6ba0-143">This is useful for scenarios where you only want to pass a subset of the full Model/ViewModel.</span></span>

| <span data-ttu-id="b6ba0-144">**侧主题：为什么&lt;%&gt;而不是&lt;%=&gt;% ？**</span><span class="sxs-lookup"><span data-stu-id="b6ba0-144">**Side Topic: Why &lt;% %&gt; instead of &lt;%= %&gt;?**</span></span> |
| --- |
| <span data-ttu-id="b6ba0-145">使用上述代码您可能注意到的一个微妙事情是，在调用 Html.Render.Render&lt;部分（） 时，&lt;我们使用的是&gt;% 块&gt;而不是 %% 块。</span><span class="sxs-lookup"><span data-stu-id="b6ba0-145">One of the subtle things you might have noticed with the code above is that we are using a &lt;% %&gt; block instead of a &lt;%= %&gt; block when calling Html.RenderPartial().</span></span> <span data-ttu-id="b6ba0-146">&lt;%=&gt; %ASP.NET 块表示开发人员想要呈现指定值（例如：%= &lt;"你好"百分比&gt;将呈现"你好"）。</span><span class="sxs-lookup"><span data-stu-id="b6ba0-146">&lt;%= %&gt; blocks in ASP.NET indicate that a developer wants to render a specified value (for example: &lt;%= "Hello" %&gt; would render "Hello").</span></span> <span data-ttu-id="b6ba0-147">&lt;%&gt; % 块相反表示开发人员想要执行代码，并且其中的任何呈现输出都必须显式完成（例如：&lt;百分比响应.Write（"你好"）%&gt;。</span><span class="sxs-lookup"><span data-stu-id="b6ba0-147">&lt;% %&gt; blocks instead indicate that the developer wants to execute code, and that any rendered output within them must be done explicitly (for example: &lt;% Response.Write("Hello") %&gt;.</span></span> <span data-ttu-id="b6ba0-148">我们使用&lt;上述 Html.Render 部分&gt;代码的 % 块的原因是 Html.Render 部分（） 方法不返回字符串，而是将内容直接输出到调用视图模板的输出流。</span><span class="sxs-lookup"><span data-stu-id="b6ba0-148">The reason we are using a &lt;% %&gt; block with our Html.RenderPartial code above is because the Html.RenderPartial() method doesn't return a string, and instead outputs the content directly to the calling view template's output stream.</span></span> <span data-ttu-id="b6ba0-149">这样做是出于性能效率的原因，并且这样做可以避免创建（可能非常大的）临时字符串对象。</span><span class="sxs-lookup"><span data-stu-id="b6ba0-149">It does this for performance efficiency reasons, and by doing so it avoids the need to create a (potentially very large) temporary string object.</span></span> <span data-ttu-id="b6ba0-150">这减少了内存使用量，并提高了应用程序的总体吞吐量。</span><span class="sxs-lookup"><span data-stu-id="b6ba0-150">This reduces memory usage and improves overall application throughput.</span></span> <span data-ttu-id="b6ba0-151">使用 Html.Render 部分（）时，一个常见的错误是忘记在呼叫结束时添加分号，而该分号在&lt;% 块&gt;内。</span><span class="sxs-lookup"><span data-stu-id="b6ba0-151">One common mistake when using Html.RenderPartial() is to forget to add a semi-colon at the end of the call when it is within a &lt;% %&gt; block.</span></span> <span data-ttu-id="b6ba0-152">例如，此代码将导致编译器错误：% &lt;Html.Render 部分（"DinnerForm"）您&gt;需要编写： &lt;% html.render部分（"DinnerForm"）;%&gt;这是因为&lt;%&gt; % 块是自包含的代码语句，并且使用 C# 代码语句时需要用分号终止。</span><span class="sxs-lookup"><span data-stu-id="b6ba0-152">For example, this code will cause a compiler error: &lt;% Html.RenderPartial("DinnerForm") %&gt; You instead need to write: &lt;% Html.RenderPartial("DinnerForm"); %&gt; This is because &lt;% %&gt; blocks are self-contained code statements, and when using C# code statements need to be terminated with a semi-colon.</span></span> |

### <a name="using-partial-view-templates-to-clarify-code"></a><span data-ttu-id="b6ba0-153">使用部分视图模板来澄清代码</span><span class="sxs-lookup"><span data-stu-id="b6ba0-153">Using Partial View Templates to Clarify Code</span></span>

<span data-ttu-id="b6ba0-154">我们创建了"DinnerForm"部分视图模板，以避免在多个位置复制视图呈现逻辑。</span><span class="sxs-lookup"><span data-stu-id="b6ba0-154">We created the "DinnerForm" partial view template to avoid duplicating view rendering logic in multiple places.</span></span> <span data-ttu-id="b6ba0-155">这是创建部分视图模板的最常见原因。</span><span class="sxs-lookup"><span data-stu-id="b6ba0-155">This is the most common reason to create partial view templates.</span></span>

<span data-ttu-id="b6ba0-156">有时，即使只在单个位置调用部分视图，创建部分视图仍然有意义。</span><span class="sxs-lookup"><span data-stu-id="b6ba0-156">Sometimes it still makes sense to create partial views even when they are only being called in a single place.</span></span> <span data-ttu-id="b6ba0-157">非常复杂的视图模板在提取视图呈现逻辑并将其分区为一个或多个命名良好的部分模板时，通常更容易阅读。</span><span class="sxs-lookup"><span data-stu-id="b6ba0-157">Very complicated view templates can often become much easier to read when their view rendering logic is extracted and partitioned into one or more well named partial templates.</span></span>

<span data-ttu-id="b6ba0-158">例如，在我们的项目中考虑 Site.master 文件中的以下代码段（我们稍后将查看）。</span><span class="sxs-lookup"><span data-stu-id="b6ba0-158">For example, consider the below code-snippet from the Site.master file in our project (which we will be looking at shortly).</span></span> <span data-ttu-id="b6ba0-159">代码相对直接读取 - 部分是因为在屏幕右上角显示登录/注销链接的逻辑封装在"LogOnUserControl"部分：</span><span class="sxs-lookup"><span data-stu-id="b6ba0-159">The code is relatively straight-forward to read – partly because the logic to display a login/logout link at the top right of the screen is encapsulated within the "LogOnUserControl" partial:</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample4.aspx)]

<span data-ttu-id="b6ba0-160">每当您发现自己试图了解视图模板中的 html/代码标记时感到困惑，请考虑如果提取某些标记并将其重构为命名良好的部分视图，是否不清楚。</span><span class="sxs-lookup"><span data-stu-id="b6ba0-160">Whenever you find yourself getting confused trying to understand the html/code markup within a view-template, consider whether it wouldn't be clearer if some of it was extracted and refactored into well-named partial views.</span></span>

### <a name="master-pages"></a><span data-ttu-id="b6ba0-161">母版页</span><span class="sxs-lookup"><span data-stu-id="b6ba0-161">Master Pages</span></span>

<span data-ttu-id="b6ba0-162">除了支持部分视图外，ASP.NET MVC 还支持创建可用于定义网站通用布局和顶级 html 的"母版页"模板的功能。</span><span class="sxs-lookup"><span data-stu-id="b6ba0-162">In addition to supporting partial views, ASP.NET MVC also supports the ability to create "master page" templates that can be used to define the common layout and top-level html of a site.</span></span> <span data-ttu-id="b6ba0-163">然后，可以将内容占位符控件添加到母版页，以标识视图可以覆盖或"填充"的可替换区域。</span><span class="sxs-lookup"><span data-stu-id="b6ba0-163">Content placeholder controls can then be added to the master page to identify replaceable regions that can be overridden or "filled in" by views.</span></span> <span data-ttu-id="b6ba0-164">这提供了一种非常有效（和 DRY）的方法，用于跨应用程序应用通用布局。</span><span class="sxs-lookup"><span data-stu-id="b6ba0-164">This provides a very effective (and DRY) way to apply a common layout across an application.</span></span>

<span data-ttu-id="b6ba0-165">默认情况下，新的ASP.NET MVC 项目会自动向其添加母版页模板。</span><span class="sxs-lookup"><span data-stu-id="b6ba0-165">By default, new ASP.NET MVC projects have a master page template automatically added to them.</span></span> <span data-ttu-id="b6ba0-166">此母版页名为"Site.master"，位于 [视图] 共享] 文件夹中：</span><span class="sxs-lookup"><span data-stu-id="b6ba0-166">This master page is named "Site.master" and lives within the \Views\Shared\ folder:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image5.png)

<span data-ttu-id="b6ba0-167">默认的 Site.master 文件如下所示。</span><span class="sxs-lookup"><span data-stu-id="b6ba0-167">The default Site.master file looks like below.</span></span> <span data-ttu-id="b6ba0-168">它定义网站的外层 html，以及顶部导航菜单。</span><span class="sxs-lookup"><span data-stu-id="b6ba0-168">It defines the outer html of the site, along with a menu for navigation at the top.</span></span> <span data-ttu-id="b6ba0-169">它包含两个可替换的内容占位符控件 - 一个用于标题，另一个用于应替换页面的主要内容的位置：</span><span class="sxs-lookup"><span data-stu-id="b6ba0-169">It contains two replaceable content placeholder controls – one for the title, and the other for where the primary content of a page should be replaced:</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample5.aspx)]

<span data-ttu-id="b6ba0-170">我们为 NerdDinner 应用程序创建的所有视图模板（"列表"、"详细信息"、"编辑"、"创建"、"未找到"等）都基于此 Site.master 模板。</span><span class="sxs-lookup"><span data-stu-id="b6ba0-170">All of the view templates we've created for our NerdDinner application ("List", "Details", "Edit", "Create", "NotFound", etc) have been based on this Site.master template.</span></span> <span data-ttu-id="b6ba0-171">当我们使用"添加视图"对话框创建视图时，默认情况下添加到顶部&lt;% = 页面 %&gt;指令的"MasterPageFile"属性指示此指示：</span><span class="sxs-lookup"><span data-stu-id="b6ba0-171">This is indicated via the "MasterPageFile" attribute that was added by default to the top &lt;% @ Page %&gt; directive when we created our views using the "Add View" dialog:</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample6.aspx)]

<span data-ttu-id="b6ba0-172">这意味着我们可以更改 Site.master 内容，并在呈现任何视图模板时自动应用和使用更改。</span><span class="sxs-lookup"><span data-stu-id="b6ba0-172">What this means is that we can change the Site.master content, and have the changes automatically be applied and used when we render any of our view templates.</span></span>

<span data-ttu-id="b6ba0-173">让我们更新我们的网站.master 的标头部分，以便我们的应用程序的标头是"NerdDinner"而不是"我的 MVC 应用程序"。</span><span class="sxs-lookup"><span data-stu-id="b6ba0-173">Let's update our Site.master's header section so that the header of our application is "NerdDinner" instead of "My MVC Application".</span></span> <span data-ttu-id="b6ba0-174">让我们还更新我们的导航菜单，以便第一个选项卡是"查找晚餐"（由 HomeController 的 Index（） 操作方法处理），并且让我们添加一个名为"主持晚餐"的新选项卡（由 DinnersController 的 Create（） 操作方法处理）：</span><span class="sxs-lookup"><span data-stu-id="b6ba0-174">Let's also update our navigation menu so that the first tab is "Find a Dinner" (handled by the HomeController's Index() action method), and let's add a new tab called "Host a Dinner" (handled by the DinnersController's Create() action method):</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample7.aspx)]

<span data-ttu-id="b6ba0-175">当我们保存 Site.master 文件并刷新浏览器时，我们将看到我们的标头更改显示在应用程序中的所有视图中。</span><span class="sxs-lookup"><span data-stu-id="b6ba0-175">When we save the Site.master file and refresh our browser we'll see our header changes show up across all views within our application.</span></span> <span data-ttu-id="b6ba0-176">例如：</span><span class="sxs-lookup"><span data-stu-id="b6ba0-176">For example:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image6.png)

<span data-ttu-id="b6ba0-177">使用 */Dinners/编辑/[id]* URL：</span><span class="sxs-lookup"><span data-stu-id="b6ba0-177">And with the */Dinners/Edit/[id]* URL:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image7.png)

### <a name="next-step"></a><span data-ttu-id="b6ba0-178">下一步</span><span class="sxs-lookup"><span data-stu-id="b6ba0-178">Next Step</span></span>

<span data-ttu-id="b6ba0-179">部分页和母版页提供了非常灵活的选项，使您能够干净地组织视图。</span><span class="sxs-lookup"><span data-stu-id="b6ba0-179">Partials and master pages provide very flexible options that enable you to cleanly organize views.</span></span> <span data-ttu-id="b6ba0-180">您会发现，它们可帮助您避免复制视图内容/代码，并使视图模板更易于阅读和维护。</span><span class="sxs-lookup"><span data-stu-id="b6ba0-180">You'll find that they help you avoid duplicating view content/ code, and make your view templates easier to read and maintain.</span></span>

<span data-ttu-id="b6ba0-181">现在，让我们重新访问我们之前构建的列表方案，并启用可扩展的分页支持。</span><span class="sxs-lookup"><span data-stu-id="b6ba0-181">Let's now revisit the listing scenario we built earlier and enable scalable paging support.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="b6ba0-182">[上一页](use-viewdata-and-implement-viewmodel-classes.md)
> [下一页](implement-efficient-data-paging.md)</span><span class="sxs-lookup"><span data-stu-id="b6ba0-182">[Previous](use-viewdata-and-implement-viewmodel-classes.md)
[Next](implement-efficient-data-paging.md)</span></span>

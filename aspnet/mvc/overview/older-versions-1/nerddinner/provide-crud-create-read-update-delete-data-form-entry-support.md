---
uid: mvc/overview/older-versions-1/nerddinner/provide-crud-create-read-update-delete-data-form-entry-support
title: 提供 CRUD（创建、读取、更新、删除）数据表单输入支持 |微软文档
author: rick-anderson
description: 步骤 5 演示如何通过支持编辑、创建和删除晚餐来进一步增加我们的 DinnersController 课程。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: bbb976e5-6150-4283-a374-c22fbafe29f5
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/provide-crud-create-read-update-delete-data-form-entry-support
msc.type: authoredcontent
ms.openlocfilehash: 2b75a7eda8bce4baa25d92626639f4d904eb363a
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542620"
---
# <a name="provide-crud-create-read-update-delete-data-form-entry-support"></a><span data-ttu-id="563e2-103">提供 CRUD（创建、读取、更新和删除）数据窗体输入支持</span><span class="sxs-lookup"><span data-stu-id="563e2-103">Provide CRUD (Create, Read, Update, Delete) Data Form Entry Support</span></span>

<span data-ttu-id="563e2-104">由[微软](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="563e2-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="563e2-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="563e2-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="563e2-106">这是一个免费的["NerdDinner"应用程序教程](introducing-the-nerddinner-tutorial.md)的第5步，它介绍了如何使用 ASP.NETmVC1构建小型但完整的Web应用程序。</span><span class="sxs-lookup"><span data-stu-id="563e2-106">This is step 5 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="563e2-107">步骤 5 演示如何通过支持编辑、创建和删除晚餐来进一步增加我们的 DinnersController 课程。</span><span class="sxs-lookup"><span data-stu-id="563e2-107">Step 5 shows how to take our DinnersController class further by enable support for editing, creating and deleting Dinners with it as well.</span></span>
> 
> <span data-ttu-id="563e2-108">如果您使用的是ASP.NET MVC 3，我们建议您按照[MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC 音乐商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程进行操作。</span><span class="sxs-lookup"><span data-stu-id="563e2-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-5-create-update-delete-form-scenarios"></a><span data-ttu-id="563e2-109">神经晚餐步骤 5：创建、更新、删除表单方案</span><span class="sxs-lookup"><span data-stu-id="563e2-109">NerdDinner Step 5: Create, Update, Delete Form Scenarios</span></span>

<span data-ttu-id="563e2-110">我们介绍了控制器和视图，并介绍了如何使用它们在现场为 Dinner 实现列表/详细信息体验。</span><span class="sxs-lookup"><span data-stu-id="563e2-110">We've introduced controllers and views, and covered how to use them to implement a listing/details experience for Dinners on site.</span></span> <span data-ttu-id="563e2-111">我们的下一步是进一步提高我们的 DinnersController 课程，并支持编辑、创建和删除晚餐。</span><span class="sxs-lookup"><span data-stu-id="563e2-111">Our next step will be to take our DinnersController class further and enable support for editing, creating and deleting Dinners with it as well.</span></span>

### <a name="urls-handled-by-dinnerscontroller"></a><span data-ttu-id="563e2-112">由晚餐控制器处理的 URL</span><span class="sxs-lookup"><span data-stu-id="563e2-112">URLs handled by DinnersController</span></span>

<span data-ttu-id="563e2-113">我们之前向 DinnersController 添加了操作方法，这些方法对两个 URL 进行了支持 *：/晚餐*和 */晚餐/详细信息/[id]。*</span><span class="sxs-lookup"><span data-stu-id="563e2-113">We previously added action methods to DinnersController that implemented support for two URLs: */Dinners* and */Dinners/Details/[id]*.</span></span>

| <span data-ttu-id="563e2-114">**URL**</span><span class="sxs-lookup"><span data-stu-id="563e2-114">**URL**</span></span> | <span data-ttu-id="563e2-115">**动词**</span><span class="sxs-lookup"><span data-stu-id="563e2-115">**VERB**</span></span> | <span data-ttu-id="563e2-116">**目标**</span><span class="sxs-lookup"><span data-stu-id="563e2-116">**Purpose**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="563e2-117">*/晚餐/*</span><span class="sxs-lookup"><span data-stu-id="563e2-117">*/Dinners/*</span></span> | <span data-ttu-id="563e2-118">GET</span><span class="sxs-lookup"><span data-stu-id="563e2-118">GET</span></span> | <span data-ttu-id="563e2-119">显示即将来临的晚宴的 HTML 列表。</span><span class="sxs-lookup"><span data-stu-id="563e2-119">Display an HTML list of upcoming dinners.</span></span> |
| <span data-ttu-id="563e2-120">*/晚餐/详情/[id]*</span><span class="sxs-lookup"><span data-stu-id="563e2-120">*/Dinners/Details/[id]*</span></span> | <span data-ttu-id="563e2-121">GET</span><span class="sxs-lookup"><span data-stu-id="563e2-121">GET</span></span> | <span data-ttu-id="563e2-122">显示有关特定晚餐的详细信息。</span><span class="sxs-lookup"><span data-stu-id="563e2-122">Display details about a specific dinner.</span></span> |

<span data-ttu-id="563e2-123">现在，我们将添加操作方法来实现三个附加*URL：/晚餐/编辑/[id]、/\*\*晚餐/创建*和 */晚餐/删除/[id]。*</span><span class="sxs-lookup"><span data-stu-id="563e2-123">We will now add action methods to implement three additional URLs: */Dinners/Edit/[id]*, */Dinners/Create*, and */Dinners/Delete/[id]*.</span></span> <span data-ttu-id="563e2-124">这些 URL 将支持编辑现有晚餐、创建新晚餐和删除晚餐。</span><span class="sxs-lookup"><span data-stu-id="563e2-124">These URLs will enable support for editing existing Dinners, creating new Dinners, and deleting Dinners.</span></span>

<span data-ttu-id="563e2-125">我们将支持 HTTP GET 和 HTTP POST 谓词与这些新 URL 的交互。</span><span class="sxs-lookup"><span data-stu-id="563e2-125">We will support both HTTP GET and HTTP POST verb interactions with these new URLs.</span></span> <span data-ttu-id="563e2-126">对这些 URL 的 HTTP GET 请求将显示数据的初始 HTML 视图（在"编辑"的情况下填充了 Dinner 数据的窗体，在"创建"的情况下填充了空白表单，在"删除"的情况下显示删除确认屏幕）。</span><span class="sxs-lookup"><span data-stu-id="563e2-126">HTTP GET requests to these URLs will display the initial HTML view of the data (a form populated with the Dinner data in the case of "edit", a blank form in the case of "create", and a delete confirmation screen in the case of "delete").</span></span> <span data-ttu-id="563e2-127">对这些 URL 的 HTTP POST 请求将保存/更新/删除我们的晚餐存储库中的晚餐数据（并从那里保存到数据库）。</span><span class="sxs-lookup"><span data-stu-id="563e2-127">HTTP POST requests to these URLs will save/update/delete the Dinner data in our DinnerRepository (and from there to the database).</span></span>

| <span data-ttu-id="563e2-128">**URL**</span><span class="sxs-lookup"><span data-stu-id="563e2-128">**URL**</span></span> | <span data-ttu-id="563e2-129">**动词**</span><span class="sxs-lookup"><span data-stu-id="563e2-129">**VERB**</span></span> | <span data-ttu-id="563e2-130">**目标**</span><span class="sxs-lookup"><span data-stu-id="563e2-130">**Purpose**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="563e2-131">*/晚餐/编辑/[id]*</span><span class="sxs-lookup"><span data-stu-id="563e2-131">*/Dinners/Edit/[id]*</span></span> | <span data-ttu-id="563e2-132">GET</span><span class="sxs-lookup"><span data-stu-id="563e2-132">GET</span></span> | <span data-ttu-id="563e2-133">显示填充晚餐数据的可编辑 HTML 表单。</span><span class="sxs-lookup"><span data-stu-id="563e2-133">Display an editable HTML form populated with Dinner data.</span></span> |
| <span data-ttu-id="563e2-134">POST</span><span class="sxs-lookup"><span data-stu-id="563e2-134">POST</span></span> | <span data-ttu-id="563e2-135">将特定 Dinner 的窗体更改保存到数据库。</span><span class="sxs-lookup"><span data-stu-id="563e2-135">Save the form changes for a particular Dinner to the database.</span></span> |
| <span data-ttu-id="563e2-136">*/晚餐/创建*</span><span class="sxs-lookup"><span data-stu-id="563e2-136">*/Dinners/Create*</span></span> | <span data-ttu-id="563e2-137">GET</span><span class="sxs-lookup"><span data-stu-id="563e2-137">GET</span></span> | <span data-ttu-id="563e2-138">显示一个空的 HTML 表单，允许用户定义新的晚餐。</span><span class="sxs-lookup"><span data-stu-id="563e2-138">Display an empty HTML form that allows users to define new Dinners.</span></span> |
| <span data-ttu-id="563e2-139">POST</span><span class="sxs-lookup"><span data-stu-id="563e2-139">POST</span></span> | <span data-ttu-id="563e2-140">创建新的晚餐并将其保存在数据库中。</span><span class="sxs-lookup"><span data-stu-id="563e2-140">Create a new Dinner and save it in the database.</span></span> |
| <span data-ttu-id="563e2-141">*/晚餐/删除/[id]*</span><span class="sxs-lookup"><span data-stu-id="563e2-141">*/Dinners/Delete/[id]*</span></span> | <span data-ttu-id="563e2-142">GET</span><span class="sxs-lookup"><span data-stu-id="563e2-142">GET</span></span> | <span data-ttu-id="563e2-143">显示删除确认屏幕。</span><span class="sxs-lookup"><span data-stu-id="563e2-143">Display delete confirmation screen.</span></span> |
| <span data-ttu-id="563e2-144">POST</span><span class="sxs-lookup"><span data-stu-id="563e2-144">POST</span></span> | <span data-ttu-id="563e2-145">从数据库中删除指定的晚餐。</span><span class="sxs-lookup"><span data-stu-id="563e2-145">Deletes the specified dinner from the database.</span></span> |

### <a name="edit-support"></a><span data-ttu-id="563e2-146">编辑支持</span><span class="sxs-lookup"><span data-stu-id="563e2-146">Edit Support</span></span>

<span data-ttu-id="563e2-147">让我们从实现"编辑"方案开始。</span><span class="sxs-lookup"><span data-stu-id="563e2-147">Let's begin by implementing the "edit" scenario.</span></span>

#### <a name="the-http-get-edit-action-method"></a><span data-ttu-id="563e2-148">HTTP-GET 编辑操作方法</span><span class="sxs-lookup"><span data-stu-id="563e2-148">The HTTP-GET Edit Action Method</span></span>

<span data-ttu-id="563e2-149">我们将首先实现编辑操作方法的 HTTP"GET"行为。</span><span class="sxs-lookup"><span data-stu-id="563e2-149">We'll start by implementing the HTTP "GET" behavior of our edit action method.</span></span> <span data-ttu-id="563e2-150">当请求 */Dinners/Edit/[id]* URL 时，将调用此方法。</span><span class="sxs-lookup"><span data-stu-id="563e2-150">This method will be invoked when the */Dinners/Edit/[id]* URL is requested.</span></span> <span data-ttu-id="563e2-151">我们的实现将如下所示：</span><span class="sxs-lookup"><span data-stu-id="563e2-151">Our implementation will look like:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample1.cs)]

<span data-ttu-id="563e2-152">上述代码使用 Dinner 存储库检索 Dinner 对象。</span><span class="sxs-lookup"><span data-stu-id="563e2-152">The code above uses the DinnerRepository to retrieve a Dinner object.</span></span> <span data-ttu-id="563e2-153">然后，它使用"晚餐"对象呈现视图模板。</span><span class="sxs-lookup"><span data-stu-id="563e2-153">It then renders a View template using the Dinner object.</span></span> <span data-ttu-id="563e2-154">由于我们尚未将模板名称显式传递给*View（）* 帮助器方法，它将使用基于约定的默认路径来解决视图模板：/视图/Dinners/Edit.aspx。</span><span class="sxs-lookup"><span data-stu-id="563e2-154">Because we haven't explicitly passed a template name to the *View()* helper method, it will use the convention based default path to resolve the view template: /Views/Dinners/Edit.aspx.</span></span>

<span data-ttu-id="563e2-155">现在，让我们创建此视图模板。</span><span class="sxs-lookup"><span data-stu-id="563e2-155">Let's now create this view template.</span></span> <span data-ttu-id="563e2-156">我们将在"编辑"方法中右键单击并选择"添加视图"上下文菜单命令来执行此操作：</span><span class="sxs-lookup"><span data-stu-id="563e2-156">We will do this by right-clicking within the Edit method and selecting the "Add View" context menu command:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image1.png)

<span data-ttu-id="563e2-157">在"添加视图"对话框中，我们将指示我们将将 Dinner 对象传递给视图模板作为其模型，并选择自动基脚模式"编辑"模板：</span><span class="sxs-lookup"><span data-stu-id="563e2-157">Within the "Add View" dialog we'll indicate that we are passing a Dinner object to our view template as its model, and choose to auto-scaffold an "Edit" template:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image2.png)

<span data-ttu-id="563e2-158">当我们单击"添加"按钮时，Visual Studio 将在"@Views_Dinners"目录中为我们添加新的"Edit.aspx"视图模板文件。</span><span class="sxs-lookup"><span data-stu-id="563e2-158">When we click the "Add" button, Visual Studio will add a new "Edit.aspx" view template file for us within the "\Views\Dinners" directory.</span></span> <span data-ttu-id="563e2-159">它还将在代码编辑器中打开新的"Edit.aspx"视图模板 ， 填充了初始的"编辑"基架实现，如下所示：</span><span class="sxs-lookup"><span data-stu-id="563e2-159">It will also open up the new "Edit.aspx" view template within the code-editor – populated with an initial "Edit" scaffold implementation like below:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image3.png)

<span data-ttu-id="563e2-160">让我们对生成的默认"编辑"基架进行一些更改，并更新编辑视图模板以包含以下内容（这将删除一些我们不想公开的属性）：</span><span class="sxs-lookup"><span data-stu-id="563e2-160">Let's make a few changes to the default "edit" scaffold generated, and update the edit view template to have the content below (which removes a few of the properties we don't want to expose):</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample2.aspx)]

<span data-ttu-id="563e2-161">当我们运行应用程序并请求 *"/晚餐/编辑/1"URL*时，我们将看到以下页面：</span><span class="sxs-lookup"><span data-stu-id="563e2-161">When we run the application and request the *"/Dinners/Edit/1"* URL we will see the following page:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image4.png)

<span data-ttu-id="563e2-162">我们的视图生成的 HTML 标记如下所示。</span><span class="sxs-lookup"><span data-stu-id="563e2-162">The HTML markup generated by our view looks like below.</span></span> <span data-ttu-id="563e2-163">它是标准 HTML –&lt;当&gt;按下"保存"&lt;输入类型="提交"/&gt;按钮时，具有对 */Dinners/Edit/1* URL 执行 HTTP POST 的表单元素。</span><span class="sxs-lookup"><span data-stu-id="563e2-163">It is standard HTML – with a &lt;form&gt; element that performs an HTTP POST to the */Dinners/Edit/1* URL when the "Save" &lt;input type="submit"/&gt; button is pushed.</span></span> <span data-ttu-id="563e2-164">已为每个&lt;可编辑属性输出 HTML&gt;输入类型="文本"/元素：</span><span class="sxs-lookup"><span data-stu-id="563e2-164">A HTML &lt;input type="text"/&gt; element has been output for each editable property:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image5.png)

#### <a name="htmlbeginform-and-htmltextbox-html-helper-methods"></a><span data-ttu-id="563e2-165">Html.BeginForm（） 和 html.TextBox（） html 帮助器方法</span><span class="sxs-lookup"><span data-stu-id="563e2-165">Html.BeginForm() and Html.TextBox() Html Helper Methods</span></span>

<span data-ttu-id="563e2-166">我们的"Edit.aspx"视图模板使用多个"Html 帮助程序"方法：Html.验证摘要（）、Html.BeginForm（）、Html.TextBox（）和 Html.验证消息（）。</span><span class="sxs-lookup"><span data-stu-id="563e2-166">Our "Edit.aspx" view template is using several "Html Helper" methods: Html.ValidationSummary(), Html.BeginForm(), Html.TextBox(), and Html.ValidationMessage().</span></span> <span data-ttu-id="563e2-167">除了为我们生成 HTML 标记外，这些帮助程序方法还提供内置的错误处理和验证支持。</span><span class="sxs-lookup"><span data-stu-id="563e2-167">In addition to generating HTML markup for us, these helper methods provide built-in error handling and validation support.</span></span>

##### <a name="htmlbeginform-helper-method"></a><span data-ttu-id="563e2-168">Html.BeginForm（） 帮助器方法</span><span class="sxs-lookup"><span data-stu-id="563e2-168">Html.BeginForm() helper method</span></span>

<span data-ttu-id="563e2-169">Html.BeginForm（） 帮助器方法是在我们的标记中输出&lt;HTML&gt;表单元素的内容。</span><span class="sxs-lookup"><span data-stu-id="563e2-169">The Html.BeginForm() helper method is what output the HTML &lt;form&gt; element in our markup.</span></span> <span data-ttu-id="563e2-170">在我们的 Edit.aspx 视图模板中，您会注意到，在使用此方法时，我们正在应用 C#"使用"语句。</span><span class="sxs-lookup"><span data-stu-id="563e2-170">In our Edit.aspx view template you'll notice that we are applying a C# "using" statement when using this method.</span></span> <span data-ttu-id="563e2-171">打开的大&lt;括号表示窗体&gt;内容的开始，而关闭的大括号表示&lt;/form&gt;元素的结束：</span><span class="sxs-lookup"><span data-stu-id="563e2-171">The open curly brace indicates the beginning of the &lt;form&gt; content, and the closing curly brace is what indicates the end of the &lt;/form&gt; element:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample3.cs)]

<span data-ttu-id="563e2-172">或者，如果您发现"使用"语句方法对于这样的方案不自然，则可以使用 Html.BeginForm（） 和 Html.EndForm（） 组合（执行相同的功能）：</span><span class="sxs-lookup"><span data-stu-id="563e2-172">Alternatively, if you find the "using" statement approach unnatural for a scenario like this, you can use a Html.BeginForm() and Html.EndForm() combination (which does the same thing):</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample4.aspx)]

<span data-ttu-id="563e2-173">调用 Html.BeginForm（） 没有任何参数将导致它输出对当前请求的 URL 执行 HTTP-POST 的窗体元素。</span><span class="sxs-lookup"><span data-stu-id="563e2-173">Calling Html.BeginForm() without any parameters will cause it to output a form element that does an HTTP-POST to the current request's URL.</span></span> <span data-ttu-id="563e2-174">这就是为什么我们的"编辑"视图生成*&lt;表单操作\"/晚餐/编辑/1"方法="后"&gt;* 元素。</span><span class="sxs-lookup"><span data-stu-id="563e2-174">That is why our Edit view generates a *&lt;form action="/Dinners/Edit/1" method="post"&gt;* element.</span></span> <span data-ttu-id="563e2-175">如果我们想要发布到其他 URL，我们也可以将显式参数传递给 Html.BeginForm（）。</span><span class="sxs-lookup"><span data-stu-id="563e2-175">We could have alternatively passed explicit parameters to Html.BeginForm() if we wanted to post to a different URL.</span></span>

##### <a name="htmltextbox-helper-method"></a><span data-ttu-id="563e2-176">Html.TextBox（） 帮助器方法</span><span class="sxs-lookup"><span data-stu-id="563e2-176">Html.TextBox() helper method</span></span>

<span data-ttu-id="563e2-177">我们的 Edit.aspx 视图使用 Html.TextBox（） 帮助器&lt;方法输出输入类型="文本&gt;"/元素：</span><span class="sxs-lookup"><span data-stu-id="563e2-177">Our Edit.aspx view uses the Html.TextBox() helper method to output &lt;input type="text"/&gt; elements:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample5.aspx)]

<span data-ttu-id="563e2-178">上面的 Html.TextBox（） 方法采用单个参数 ， 用于指定&lt;要输出的输入类型的 id/name 属性= "text"/&gt;元素，以及用于填充文本框值的模型属性。</span><span class="sxs-lookup"><span data-stu-id="563e2-178">The Html.TextBox() method above takes a single parameter – which is being used to specify both the id/name attributes of the &lt;input type="text"/&gt; element to output, as well as the model property to populate the textbox value from.</span></span> <span data-ttu-id="563e2-179">例如，我们传递给"编辑"视图的 Dinner 对象具有".NET 期货"的"标题"属性值，因此我们的 Html.TextBox（"标题"）方法调用输出：*&lt;输入 id="标题"名称="标题"类型="文本"值=".NET&gt;期货"/。*</span><span class="sxs-lookup"><span data-stu-id="563e2-179">For example, the Dinner object we passed to the Edit view had a "Title" property value of ".NET Futures", and so our Html.TextBox("Title") method call output: *&lt;input id="Title" name="Title" type="text" value=".NET Futures" /&gt;*.</span></span>

<span data-ttu-id="563e2-180">或者，我们可以使用第一个 Html.TextBox（） 参数来指定元素的 ID/名称，然后显式传递值以用作第二个参数：</span><span class="sxs-lookup"><span data-stu-id="563e2-180">Alternatively, we can use the first Html.TextBox() parameter to specify the id/name of the element, and then explicitly pass in the value to use as a second parameter:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample6.aspx)]

<span data-ttu-id="563e2-181">通常，我们希望对输出的值执行自定义格式设置。</span><span class="sxs-lookup"><span data-stu-id="563e2-181">Often we'll want to perform custom formatting on the value that is output.</span></span> <span data-ttu-id="563e2-182">内置于 .NET 的 String.Format（） 静态方法对于这些方案很有用。</span><span class="sxs-lookup"><span data-stu-id="563e2-182">The String.Format() static method built-into .NET is useful for these scenarios.</span></span> <span data-ttu-id="563e2-183">我们的 Edit.aspx 视图模板正在使用此设置事件日期值（类型为 DateTime）的格式，以便它不显示时间上的秒数：</span><span class="sxs-lookup"><span data-stu-id="563e2-183">Our Edit.aspx view template is using this to format the EventDate value (which is of type DateTime) so that it doesn't show seconds for the time:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample7.aspx)]

<span data-ttu-id="563e2-184">可以选择使用 Html.TextBox（） 的第三个参数来输出其他 HTML 属性。</span><span class="sxs-lookup"><span data-stu-id="563e2-184">A third parameter to Html.TextBox() can optionally be used to output additional HTML attributes.</span></span> <span data-ttu-id="563e2-185">下面的代码段演示如何在&lt;输入类型="text"/&gt;元素上呈现额外的大小="30"属性和类="mycssclass"属性。</span><span class="sxs-lookup"><span data-stu-id="563e2-185">The code-snippet below demonstrates how to render an additional size="30" attribute and a class="mycssclass" attribute on the &lt;input type="text"/&gt; element.</span></span> <span data-ttu-id="563e2-186">请注意，如何使用"类"@" character because "从类属性的名称中转义是 C# 中的保留关键字：</span><span class="sxs-lookup"><span data-stu-id="563e2-186">Note how we are escaping the name of the class attribute using a "@" character because "class" is a reserved keyword in C#:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample8.aspx)]

#### <a name="implementing-the-http-post-edit-action-method"></a><span data-ttu-id="563e2-187">实现 HTTP-POST 编辑操作方法</span><span class="sxs-lookup"><span data-stu-id="563e2-187">Implementing the HTTP-POST Edit Action Method</span></span>

<span data-ttu-id="563e2-188">现在，我们实现了"编辑"操作方法的 HTTP-GET 版本。</span><span class="sxs-lookup"><span data-stu-id="563e2-188">We now have the HTTP-GET version of our Edit action method implemented.</span></span> <span data-ttu-id="563e2-189">当用户请求 */Dinners/Edit/1* URL 时，他们收到一个 HTML 页面，如下所示：</span><span class="sxs-lookup"><span data-stu-id="563e2-189">When a user requests the */Dinners/Edit/1* URL they receive an HTML page like the following:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image6.png)

<span data-ttu-id="563e2-190">按下"保存"按钮会导致表单发布到 */Dinners/Edit/1* URL，并使用 HTTP POST 谓&lt;词&gt;提交 HTML 输入表单值。</span><span class="sxs-lookup"><span data-stu-id="563e2-190">Pressing the "Save" button causes a form post to the */Dinners/Edit/1* URL, and submits the HTML &lt;input&gt; form values using the HTTP POST verb.</span></span> <span data-ttu-id="563e2-191">现在，让我们实现编辑操作方法的 HTTP POST 行为 ， 这将处理保存晚餐。</span><span class="sxs-lookup"><span data-stu-id="563e2-191">Let's now implement the HTTP POST behavior of our edit action method – which will handle saving the Dinner.</span></span>

<span data-ttu-id="563e2-192">我们将首先向 DinnersController 添加一个重载的"编辑"操作方法，该控制器上具有"AcceptVerbs"属性，指示它处理 HTTP POST 方案：</span><span class="sxs-lookup"><span data-stu-id="563e2-192">We'll begin by adding an overloaded "Edit" action method to our DinnersController that has an "AcceptVerbs" attribute on it that indicates it handles HTTP POST scenarios:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample9.cs)]

<span data-ttu-id="563e2-193">当 [AcceptVerbs] 属性应用于重载操作方法时，ASP.NET MVC 根据传入的 HTTP 谓词自动处理向相应操作方法发送请求。</span><span class="sxs-lookup"><span data-stu-id="563e2-193">When the [AcceptVerbs] attribute is applied to overloaded action methods, ASP.NET MVC automatically handles dispatching requests to the appropriate action method depending on the incoming HTTP verb.</span></span> <span data-ttu-id="563e2-194">HTTP POST 对 */Dinners/Edit/[id]* URL 的请求将转到上述编辑方法，而所有其他 HTTP 谓词请求 */Dinners/Edit/[id]* URL 将转到我们实现的第一个编辑方法（`[AcceptVerbs]`该方法没有属性）。</span><span class="sxs-lookup"><span data-stu-id="563e2-194">HTTP POST requests to */Dinners/Edit/[id]* URLs will go to the above Edit method, while all other HTTP verb requests to */Dinners/Edit/[id]* URLs will go to the first Edit method we implemented (which did not have an `[AcceptVerbs]` attribute).</span></span>

| <span data-ttu-id="563e2-195">**侧主题：为什么通过 HTTP 谓词进行区分？**</span><span class="sxs-lookup"><span data-stu-id="563e2-195">**Side Topic: Why differentiate via HTTP verbs?**</span></span> |
| --- |
| <span data-ttu-id="563e2-196">您可能会问 – 为什么我们使用单个 URL 并通过 HTTP 谓词区分其行为？</span><span class="sxs-lookup"><span data-stu-id="563e2-196">You might ask – why are we using a single URL and differentiating its behavior via the HTTP verb?</span></span> <span data-ttu-id="563e2-197">为什么不只有两个单独的 URL 来处理加载和保存编辑更改？</span><span class="sxs-lookup"><span data-stu-id="563e2-197">Why not just have two separate URLs to handle loading and saving edit changes?</span></span> <span data-ttu-id="563e2-198">例如：/Dinners/Edit/[id]以显示初始窗体和/Dinners/保存/[id]来处理表单帖子以保存它？</span><span class="sxs-lookup"><span data-stu-id="563e2-198">For example: /Dinners/Edit/[id] to display the initial form and /Dinners/Save/[id] to handle the form post to save it?</span></span> <span data-ttu-id="563e2-199">发布两个单独的 URL 的缺点是，如果我们发布到 /Dinners/Save/2，然后由于输入错误而需要重新显示 HTML 表单，最终用户最终将在其浏览器的地址栏中具有 /Dinners/Save/2 URL（因为这是表单发布到的 URL）。</span><span class="sxs-lookup"><span data-stu-id="563e2-199">The downside with publishing two separate URLs is that in cases where we post to /Dinners/Save/2, and then need to redisplay the HTML form because of an input error, the end-user will end up having the /Dinners/Save/2 URL in their browser's address bar (since that was the URL the form posted to).</span></span> <span data-ttu-id="563e2-200">如果最终用户将此重新显示的页面标记为其浏览器收藏夹列表，或将 URL 复制/粘贴并通过电子邮件发送给朋友，则他们最终将保存将来无法工作的 URL（因为该 URL 取决于帖子值）。</span><span class="sxs-lookup"><span data-stu-id="563e2-200">If the end-user bookmarks this redisplayed page to their browser favorites list, or copy/pastes the URL and emails it to a friend, they will end up saving a URL that won't work in the future (since that URL depends on post values).</span></span> <span data-ttu-id="563e2-201">通过公开单个 URL（如：/Dinners/Edit/[id]）并通过 HTTP 谓词区分其处理，最终用户可以安全地为编辑页面添加书签和/或将 URL 发送给其他人。</span><span class="sxs-lookup"><span data-stu-id="563e2-201">By exposing a single URL (like: /Dinners/Edit/[id]) and differentiating the processing of it by HTTP verb, it is safe for end-users to bookmark the edit page and/or send the URL to others.</span></span> |

#### <a name="retrieving-form-post-values"></a><span data-ttu-id="563e2-202">检索表单过帐值</span><span class="sxs-lookup"><span data-stu-id="563e2-202">Retrieving Form Post Values</span></span>

<span data-ttu-id="563e2-203">我们可以通过多种方式访问 HTTP POST"编辑"方法中的已发布的表单参数。</span><span class="sxs-lookup"><span data-stu-id="563e2-203">There are a variety of ways we can access posted form parameters within our HTTP POST "Edit" method.</span></span> <span data-ttu-id="563e2-204">一个简单的方法是只使用 Controller 基类上的 Request 属性来访问窗体集合并直接检索已过帐的值：</span><span class="sxs-lookup"><span data-stu-id="563e2-204">One simple approach is to just use the Request property on the Controller base class to access the form collection and retrieve the posted values directly:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample10.cs)]

<span data-ttu-id="563e2-205">不过，上述方法有点冗长，尤其是在添加错误处理逻辑后。</span><span class="sxs-lookup"><span data-stu-id="563e2-205">The above approach is a little verbose, though, especially once we add error handling logic.</span></span>

<span data-ttu-id="563e2-206">此方案的更好方法是在控制器基类上利用内置*的 UpdateModel（）* 帮助器方法。</span><span class="sxs-lookup"><span data-stu-id="563e2-206">A better approach for this scenario is to leverage the built-in *UpdateModel()* helper method on the Controller base class.</span></span> <span data-ttu-id="563e2-207">它支持更新使用传入窗体参数传递的对象的属性。</span><span class="sxs-lookup"><span data-stu-id="563e2-207">It supports updating the properties of an object we pass it using the incoming form parameters.</span></span> <span data-ttu-id="563e2-208">它使用反射来确定对象上的属性名称，然后根据客户端提交的输入值自动转换和分配值。</span><span class="sxs-lookup"><span data-stu-id="563e2-208">It uses reflection to determine the property names on the object, and then automatically converts and assigns values to them based on the input values submitted by the client.</span></span>

<span data-ttu-id="563e2-209">我们可以使用 UpdateModel（） 方法使用此代码简化我们的 HTTP-POST 编辑操作：</span><span class="sxs-lookup"><span data-stu-id="563e2-209">We could use the UpdateModel() method to simplify our HTTP-POST Edit Action using this code:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample11.cs)]

<span data-ttu-id="563e2-210">我们现在可以访问 */Dinners/Edit/1* URL，并更改我们的晚餐标题：</span><span class="sxs-lookup"><span data-stu-id="563e2-210">We can now visit the */Dinners/Edit/1* URL, and change the title of our Dinner:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image7.png)

<span data-ttu-id="563e2-211">单击"保存"按钮时，我们将执行"编辑"操作的表单帖子，更新的值将保留在数据库中。</span><span class="sxs-lookup"><span data-stu-id="563e2-211">When we click the "Save" button, we'll perform a form post to our Edit action, and the updated values will be persisted in the database.</span></span> <span data-ttu-id="563e2-212">然后，我们将重定向到晚餐的详细信息 URL（将显示新保存的值）：</span><span class="sxs-lookup"><span data-stu-id="563e2-212">We will then be redirected to the Details URL for the Dinner (which will display the newly saved values):</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image8.png)

#### <a name="handling-edit-errors"></a><span data-ttu-id="563e2-213">处理编辑错误</span><span class="sxs-lookup"><span data-stu-id="563e2-213">Handling Edit Errors</span></span>

<span data-ttu-id="563e2-214">我们当前的 HTTP-POST 实现工作正常，除非出现错误。</span><span class="sxs-lookup"><span data-stu-id="563e2-214">Our current HTTP-POST implementation works fine – except when there are errors.</span></span>

<span data-ttu-id="563e2-215">当用户在编辑表单时出错时，我们需要确保表单重新显示一条信息性错误消息，以指导他们修复表单。</span><span class="sxs-lookup"><span data-stu-id="563e2-215">When a user makes a mistake editing a form, we need to make sure that the form is redisplayed with an informative error message that guides them to fix it.</span></span> <span data-ttu-id="563e2-216">这包括最终用户发布不正确的输入（例如：格式不正确的日期字符串）的情况，以及输入格式有效但存在业务规则冲突的情况。</span><span class="sxs-lookup"><span data-stu-id="563e2-216">This includes cases where an end-user posts incorrect input (for example: a malformed date string), as well as cases where the input format is valid but there is a business rule violation.</span></span> <span data-ttu-id="563e2-217">发生错误时，窗体应保留用户最初输入的输入数据，以便不必手动重新填充其更改。</span><span class="sxs-lookup"><span data-stu-id="563e2-217">When errors occur the form should preserve the input data the user originally entered so that they don't have to refill their changes manually.</span></span> <span data-ttu-id="563e2-218">此过程应根据需要重复多次，直到表单成功完成。</span><span class="sxs-lookup"><span data-stu-id="563e2-218">This process should repeat as many times as necessary until the form successfully completes.</span></span>

<span data-ttu-id="563e2-219">ASP.NET MVC 包含一些不错的内置功能，使错误处理和表单重新显示变得简单。</span><span class="sxs-lookup"><span data-stu-id="563e2-219">ASP.NET MVC includes some nice built-in features that make error handling and form redisplay easy.</span></span> <span data-ttu-id="563e2-220">要查看这些功能，让我们使用以下代码更新我们的 Edit 操作方法：</span><span class="sxs-lookup"><span data-stu-id="563e2-220">To see these features in action let's update our Edit action method with the following code:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample12.cs)]

<span data-ttu-id="563e2-221">上述代码与之前的实现类似，只是我们现在正在将 try/catch 错误处理块包装在工作周围。</span><span class="sxs-lookup"><span data-stu-id="563e2-221">The above code is similar to our previous implementation – except that we are now wrapping a try/catch error handling block around our work.</span></span> <span data-ttu-id="563e2-222">如果在调用 UpdateModel（） 时或尝试保存 DinnerRepository 时出现异常（如果我们试图保存的 Dinner 对象由于模型中的规则冲突而无效，则将引发异常），则将执行 catch 错误处理块。</span><span class="sxs-lookup"><span data-stu-id="563e2-222">If an exception occurs either when calling UpdateModel(), or when we try and save the DinnerRepository (which will raise an exception if the Dinner object we are trying to save is invalid because of a rule violation within our model), our catch error handling block will execute.</span></span> <span data-ttu-id="563e2-223">在其中，我们循环对"晚餐"对象中存在的任何规则冲突，并将其添加到 ModelState 对象（我们稍后将讨论）。</span><span class="sxs-lookup"><span data-stu-id="563e2-223">Within it we loop over any rule violations that exist in the Dinner object and add them to a ModelState object (which we'll discuss shortly).</span></span> <span data-ttu-id="563e2-224">然后，我们重新显示视图。</span><span class="sxs-lookup"><span data-stu-id="563e2-224">We then redisplay the view.</span></span>

<span data-ttu-id="563e2-225">要看到这个工作，让我们重新运行应用程序，编辑晚餐，并更改它有一个空的标题，事件日期的"BOGUS"，并使用一个英国电话号码与国家国家值的美国。</span><span class="sxs-lookup"><span data-stu-id="563e2-225">To see this working let's re-run the application, edit a Dinner, and change it to have an empty Title, an EventDate of "BOGUS", and use a UK phone number with a country value of USA.</span></span> <span data-ttu-id="563e2-226">当我们按下"保存"按钮时，我们的 HTTP POST 编辑方法将无法保存晚餐（因为存在错误），并将重新显示该窗体：</span><span class="sxs-lookup"><span data-stu-id="563e2-226">When we press the "Save" button our HTTP POST Edit method will not be able to save the Dinner (because there are errors) and will redisplay the form:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image9.png)

<span data-ttu-id="563e2-227">我们的应用程序有一个体面的错误经验。</span><span class="sxs-lookup"><span data-stu-id="563e2-227">Our application has a decent error experience.</span></span> <span data-ttu-id="563e2-228">具有无效输入的文本元素以红色突出显示，验证错误消息向最终用户显示。</span><span class="sxs-lookup"><span data-stu-id="563e2-228">The text elements with the invalid input are highlighted in red, and validation error messages are displayed to the end user about them.</span></span> <span data-ttu-id="563e2-229">该窗体还保留用户最初输入的输入数据，以便他们不必重新填充任何内容。</span><span class="sxs-lookup"><span data-stu-id="563e2-229">The form is also preserving the input data the user originally entered – so that they don't have to refill anything.</span></span>

<span data-ttu-id="563e2-230">你可能会问，这是怎么发生的？</span><span class="sxs-lookup"><span data-stu-id="563e2-230">How, you might ask, did this occur?</span></span> <span data-ttu-id="563e2-231">标题、事件日期和 ContactPhone 文本框如何以红色突出显示自己，并知道要输出最初输入的用户值？</span><span class="sxs-lookup"><span data-stu-id="563e2-231">How did the Title, EventDate, and ContactPhone textboxes highlight themselves in red and know to output the originally entered user values?</span></span> <span data-ttu-id="563e2-232">错误消息是如何显示在顶部列表中的？</span><span class="sxs-lookup"><span data-stu-id="563e2-232">And how did error messages get displayed in the list at the top?</span></span> <span data-ttu-id="563e2-233">好消息是，这不是魔术造成的，而是因为我们使用了一些内置ASP.NET MVC 功能，使输入验证和错误处理方案变得容易。</span><span class="sxs-lookup"><span data-stu-id="563e2-233">The good news is that this didn't occur by magic - rather it was because we used some of the built-in ASP.NET MVC features that make input validation and error handling scenarios easy.</span></span>

#### <a name="understanding-modelstate-and-the-validation-html-helper-methods"></a><span data-ttu-id="563e2-234">了解模型状态和验证 HTML 帮助器方法</span><span class="sxs-lookup"><span data-stu-id="563e2-234">Understanding ModelState and the Validation HTML Helper Methods</span></span>

<span data-ttu-id="563e2-235">控制器类具有"ModelState"属性集合，它提供了一种指示模型对象传递给 View 存在错误的方法。</span><span class="sxs-lookup"><span data-stu-id="563e2-235">Controller classes have a "ModelState" property collection which provides a way to indicate that errors exist with a model object being passed to a View.</span></span> <span data-ttu-id="563e2-236">ModelState 集合中的错误条目标识具有问题的模型属性的名称（例如："标题"、"事件日期"或"ContactPhone"），并允许指定人性化的错误消息（例如："需要标题"）。</span><span class="sxs-lookup"><span data-stu-id="563e2-236">Error entries within the ModelState collection identify the name of the model property with the issue (for example: "Title", "EventDate", or "ContactPhone"), and allow a human-friendly error message to be specified (for example: "Title is required").</span></span>

<span data-ttu-id="563e2-237">*UpdateModel（）* 帮助器方法在尝试将窗体值分配给模型对象的属性时遇到错误时自动填充模型状态集合。</span><span class="sxs-lookup"><span data-stu-id="563e2-237">The *UpdateModel()* helper method automatically populates the ModelState collection when it encounters errors while trying to assign form values to properties on the model object.</span></span> <span data-ttu-id="563e2-238">例如，我们的 Dinner 对象的 EventDate 属性为"日期时间"类型。</span><span class="sxs-lookup"><span data-stu-id="563e2-238">For example, our Dinner object's EventDate property is of type DateTime.</span></span> <span data-ttu-id="563e2-239">当 UpdateModel（） 方法无法在上述方案中为其分配字符串值"BOGUS"时，UpdateModel（） 方法向 ModelState 集合添加了一个条目，指示该属性发生了赋值错误。</span><span class="sxs-lookup"><span data-stu-id="563e2-239">When the UpdateModel() method was unable to assign the string value "BOGUS" to it in the scenario above, the UpdateModel() method added an entry to the ModelState collection indicating an assignment error had occurred with that property.</span></span>

<span data-ttu-id="563e2-240">开发人员还可以编写代码，将错误条目显式添加到 ModelState 集合中，就像我们在下面的"catch"错误处理块中所做的一样，该块基于"晚餐"对象中的活动规则冲突填充了 ModelState 集合：</span><span class="sxs-lookup"><span data-stu-id="563e2-240">Developers can also write code to explicitly add error entries into the ModelState collection like we are doing below within our "catch" error handling block, which is populating the ModelState collection with entries based on the active Rule Violations in the Dinner object:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample13.cs)]

#### <a name="html-helper-integration-with-modelstate"></a><span data-ttu-id="563e2-241">Html 帮助器与模型状态集成</span><span class="sxs-lookup"><span data-stu-id="563e2-241">Html Helper Integration with ModelState</span></span>

<span data-ttu-id="563e2-242">HTML 帮助器方法（如 Html.TextBox（） ） - 在呈现输出时选中 ModelState 集合。</span><span class="sxs-lookup"><span data-stu-id="563e2-242">HTML helper methods - like Html.TextBox() - check the ModelState collection when rendering output.</span></span> <span data-ttu-id="563e2-243">如果项存在错误，则呈现用户输入的值和 CSS 错误类。</span><span class="sxs-lookup"><span data-stu-id="563e2-243">If an error for the item exists, they render the user-entered value and a CSS error class.</span></span>

<span data-ttu-id="563e2-244">例如，在我们的"编辑"视图中，我们使用 Html.TextBox（） 帮助器方法来呈现晚餐对象的事件日期：</span><span class="sxs-lookup"><span data-stu-id="563e2-244">For example, in our "Edit" view we are using the Html.TextBox() helper method to render the EventDate of our Dinner object:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample14.aspx)]

<span data-ttu-id="563e2-245">在错误方案中呈现视图时，Html.TextBox（） 方法检查了 ModelState 集合，以查看是否存在与 Dinner 对象的"EventDate"属性关联的任何错误。</span><span class="sxs-lookup"><span data-stu-id="563e2-245">When the view was rendered in the error scenario, the Html.TextBox() method checked the ModelState collection to see if there were any errors associated with the "EventDate" property of our Dinner object.</span></span> <span data-ttu-id="563e2-246">当它确定存在错误时，它呈现提交的用户输入（"BOGUS"）作为值，并将 css 错误类添加到&lt;它生成的输入类型="textbox"/&gt;标记：</span><span class="sxs-lookup"><span data-stu-id="563e2-246">When it determined that there was an error it rendered the submitted user input ("BOGUS") as the value, and added a css error class to the &lt;input type="textbox"/&gt; markup it generated:</span></span>

[!code-html[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample15.html)]

<span data-ttu-id="563e2-247">您可以自定义 css 错误类的外观，以按所需时间查看。</span><span class="sxs-lookup"><span data-stu-id="563e2-247">You can customize the appearance of the css error class to look however you want.</span></span> <span data-ttu-id="563e2-248">默认 CSS 错误类 （ "输入验证-错误" ） 在 *_content_site.css*样式表中定义，如下所示：</span><span class="sxs-lookup"><span data-stu-id="563e2-248">The default CSS error class – "input-validation-error" – is defined in the *\content\site.css* stylesheet and looks like below:</span></span>

[!code-css[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample16.css)]

<span data-ttu-id="563e2-249">此 CSS 规则导致无效输入元素突出显示的原因如下：</span><span class="sxs-lookup"><span data-stu-id="563e2-249">This CSS rule is what caused our invalid input elements to be highlighted like below:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image10.png)

##### <a name="htmlvalidationmessage-helper-method"></a><span data-ttu-id="563e2-250">Html.验证消息（） 帮助器方法</span><span class="sxs-lookup"><span data-stu-id="563e2-250">Html.ValidationMessage() Helper Method</span></span>

<span data-ttu-id="563e2-251">Html.验证消息（） 帮助器方法可用于输出与特定模型属性关联的 ModelState 错误消息：</span><span class="sxs-lookup"><span data-stu-id="563e2-251">The Html.ValidationMessage() helper method can be used to output the ModelState error message associated with a particular model property:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample17.aspx)]

<span data-ttu-id="563e2-252">上述代码输出：*&lt;跨类="字段验证错误"&gt;值"BOGUS"无效&lt;/跨&gt;*</span><span class="sxs-lookup"><span data-stu-id="563e2-252">The above code outputs: *&lt;span class="field-validation-error"&gt; The value ‘BOGUS' is invalid&lt;/span&gt;*</span></span>

<span data-ttu-id="563e2-253">Html.验证消息（） 帮助器方法还支持第二个参数，该参数允许开发人员重写显示的错误文本消息：</span><span class="sxs-lookup"><span data-stu-id="563e2-253">The Html.ValidationMessage() helper method also supports a second parameter that allows developers to override the error text message that is displayed:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample18.aspx)]

<span data-ttu-id="563e2-254">上述代码输出：*&lt;跨类="字段验证-错误"/span，&gt;\*&lt;&gt;* 而不是当 EventDate 属性存在错误时，而不是默认错误文本。</span><span class="sxs-lookup"><span data-stu-id="563e2-254">The above code outputs: *&lt;span class="field-validation-error"&gt;\*&lt;/span&gt;* instead of the default error text when an error is present for the EventDate property.</span></span>

##### <a name="htmlvalidationsummary-helper-method"></a><span data-ttu-id="563e2-255">Html.验证摘要（） 帮助器方法</span><span class="sxs-lookup"><span data-stu-id="563e2-255">Html.ValidationSummary() Helper Method</span></span>

<span data-ttu-id="563e2-256">Html.验证摘要（） 帮助程序方法可用于呈现摘要错误消息，并附带 ModelState 集合中&lt;所有&gt;&lt;详细错误消息&gt;&lt;的&gt;ul li//ul 列表：</span><span class="sxs-lookup"><span data-stu-id="563e2-256">The Html.ValidationSummary() helper method can be used to render a summary error message, accompanied by a &lt;ul&gt;&lt;li/&gt;&lt;/ul&gt; list of all detailed error messages in the ModelState collection:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image11.png)

<span data-ttu-id="563e2-257">Html.验证摘要（） 帮助程序方法采用可选字符串参数 ， 它定义一个摘要错误消息，以显示在详细错误列表的上方：</span><span class="sxs-lookup"><span data-stu-id="563e2-257">The Html.ValidationSummary() helper method takes an optional string parameter – which defines a summary error message to display above the list of detailed errors:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample19.aspx)]

<span data-ttu-id="563e2-258">您可以选择使用 CSS 来覆盖错误列表的外观。</span><span class="sxs-lookup"><span data-stu-id="563e2-258">You can optionally use CSS to override what the error list looks like.</span></span>

#### <a name="using-a-addruleviolations-helper-method"></a><span data-ttu-id="563e2-259">使用添加规则冲突帮助器方法</span><span class="sxs-lookup"><span data-stu-id="563e2-259">Using a AddRuleViolations Helper Method</span></span>

<span data-ttu-id="563e2-260">我们的初始 HTTP-POST 编辑实现使用 catch 块中的 foreach 语句来循环访问 Dinner 对象的"规则冲突"，并将它们添加到控制器的 ModelState 集合中：</span><span class="sxs-lookup"><span data-stu-id="563e2-260">Our initial HTTP-POST Edit implementation used a foreach statement within its catch block to loop over the Dinner object's Rule Violations and add them to the controller's ModelState collection:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample20.cs)]

<span data-ttu-id="563e2-261">通过将"控制器帮助器"类添加到 NerdDinner 项目中，并在其中实现"AddRuleRule冲突"扩展方法，将帮助器方法添加到ASP.NET MVC ModelState字典类，我们可以使此代码更简洁一些。</span><span class="sxs-lookup"><span data-stu-id="563e2-261">We can make this code a little cleaner by adding a "ControllerHelpers" class to the NerdDinner project, and implement an "AddRuleViolations" extension method within it that adds a helper method to the ASP.NET MVC ModelStateDictionary class.</span></span> <span data-ttu-id="563e2-262">此扩展方法可以使用规则冲突错误列表封装填充 ModelState字典所需的逻辑：</span><span class="sxs-lookup"><span data-stu-id="563e2-262">This extension method can encapsulate the logic necessary to populate the ModelStateDictionary with a list of RuleViolation errors:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample21.cs)]

<span data-ttu-id="563e2-263">然后，我们可以更新我们的 HTTP-POST 编辑操作方法，以使用此扩展方法使用我们的晚餐规则冲突填充 ModelState 集合。</span><span class="sxs-lookup"><span data-stu-id="563e2-263">We can then update our HTTP-POST Edit action method to use this extension method to populate the ModelState collection with our Dinner Rule Violations.</span></span>

#### <a name="complete-edit-action-method-implementations"></a><span data-ttu-id="563e2-264">完整的编辑操作方法实现</span><span class="sxs-lookup"><span data-stu-id="563e2-264">Complete Edit Action Method Implementations</span></span>

<span data-ttu-id="563e2-265">以下代码实现了编辑方案所需的所有控制器逻辑：</span><span class="sxs-lookup"><span data-stu-id="563e2-265">The code below implements all of the controller logic necessary for our Edit scenario:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample22.cs)]

<span data-ttu-id="563e2-266">我们的 Edit 实现好处是，我们的 Controller 类和 View 模板都不需要了解我们的 Dinner 模型正在强制执行的特定验证或业务规则。</span><span class="sxs-lookup"><span data-stu-id="563e2-266">The nice thing about our Edit implementation is that neither our Controller class nor our View template has to know anything about the specific validation or business rules being enforced by our Dinner model.</span></span> <span data-ttu-id="563e2-267">将来，我们可以向模型添加其他规则，并且不必对我们的控制器或视图进行任何代码更改，以便支持这些规则。</span><span class="sxs-lookup"><span data-stu-id="563e2-267">We can add additional rules to our model in the future and do not have to make any code changes to our controller or view in order for them to be supported.</span></span> <span data-ttu-id="563e2-268">这为我们提供了灵活性，以便在未来以最少的代码更改轻松发展我们的应用程序需求。</span><span class="sxs-lookup"><span data-stu-id="563e2-268">This provides us with the flexibility to easily evolve our application requirements in the future with a minimum of code changes.</span></span>

### <a name="create-support"></a><span data-ttu-id="563e2-269">创建支持</span><span class="sxs-lookup"><span data-stu-id="563e2-269">Create Support</span></span>

<span data-ttu-id="563e2-270">我们已经完成了晚餐控制器类的"编辑"行为。</span><span class="sxs-lookup"><span data-stu-id="563e2-270">We've finished implementing the "Edit" behavior of our DinnersController class.</span></span> <span data-ttu-id="563e2-271">现在，让我们继续实现其上的"创建"支持 - 这将使用户能够添加新的晚餐。</span><span class="sxs-lookup"><span data-stu-id="563e2-271">Let's now move on to implement the "Create" support on it – which will enable users to add new Dinners.</span></span>

#### <a name="the-http-get-create-action-method"></a><span data-ttu-id="563e2-272">HTTP-GET 创建操作方法</span><span class="sxs-lookup"><span data-stu-id="563e2-272">The HTTP-GET Create Action Method</span></span>

<span data-ttu-id="563e2-273">我们将首先实现创建操作方法的 HTTP"GET"行为。</span><span class="sxs-lookup"><span data-stu-id="563e2-273">We'll begin by implementing the HTTP "GET" behavior of our create action method.</span></span> <span data-ttu-id="563e2-274">当有人访问 */Dinners/创建*URL 时，将调用此方法。</span><span class="sxs-lookup"><span data-stu-id="563e2-274">This method will be called when someone visits the */Dinners/Create* URL.</span></span> <span data-ttu-id="563e2-275">我们的实现如下所示：</span><span class="sxs-lookup"><span data-stu-id="563e2-275">Our implementation looks like:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample23.cs)]

<span data-ttu-id="563e2-276">上面的代码将创建一个新的 Dinner 对象，并将其事件日期属性分配为将来一周。</span><span class="sxs-lookup"><span data-stu-id="563e2-276">The code above creates a new Dinner object, and assigns its EventDate property to be one week in the future.</span></span> <span data-ttu-id="563e2-277">然后，它呈现基于新"晚餐"对象的视图。</span><span class="sxs-lookup"><span data-stu-id="563e2-277">It then renders a View that is based on the new Dinner object.</span></span> <span data-ttu-id="563e2-278">由于我们尚未显式将名称传递给*View（）* 帮助器方法，它将使用基于约定的默认路径来解决视图模板：/视图/Dinners/Create.aspx。</span><span class="sxs-lookup"><span data-stu-id="563e2-278">Because we haven't explicitly passed a name to the *View()* helper method, it will use the convention based default path to resolve the view template: /Views/Dinners/Create.aspx.</span></span>

<span data-ttu-id="563e2-279">现在，让我们创建此视图模板。</span><span class="sxs-lookup"><span data-stu-id="563e2-279">Let's now create this view template.</span></span> <span data-ttu-id="563e2-280">我们可以在"创建操作"方法中右键单击并选择"添加视图"上下文菜单命令来执行此操作。</span><span class="sxs-lookup"><span data-stu-id="563e2-280">We can do this by right-clicking within the Create action method and selecting the "Add View" context menu command.</span></span> <span data-ttu-id="563e2-281">在"添加视图"对话框中，我们将指示我们将将 Dinner 对象传递到视图模板，并选择自动基脚手架"创建"模板：</span><span class="sxs-lookup"><span data-stu-id="563e2-281">Within the "Add View" dialog we'll indicate that we are passing a Dinner object to the view template, and choose to auto-scaffold a "Create" template:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image12.png)

<span data-ttu-id="563e2-282">单击"添加"按钮时，Visual Studio 会将基于脚手架的新"Create.aspx"视图保存到"_Views_Dinners"目录，并在 IDE 中将其打开：</span><span class="sxs-lookup"><span data-stu-id="563e2-282">When we click the "Add" button, Visual Studio will save a new scaffold-based "Create.aspx" view to the "\Views\Dinners" directory, and open it up within the IDE:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image13.png)

<span data-ttu-id="563e2-283">让我们对为我们生成的默认"创建"基架文件进行一些更改，并将其修改为如下所示：</span><span class="sxs-lookup"><span data-stu-id="563e2-283">Let's make a few changes to the default "create" scaffold file that was generated for us, and modify it up to look like below:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample24.aspx)]

<span data-ttu-id="563e2-284">现在，当我们运行应用程序并访问浏览器中的 *"/Dinner/Create"URL*时，它将从我们的"创建操作"实现中呈现如下 UI：</span><span class="sxs-lookup"><span data-stu-id="563e2-284">And now when we run our application and access the *"/Dinners/Create"* URL within the browser it will render UI like below from our Create action implementation:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image14.png)

#### <a name="implementing-the-http-post-create-action-method"></a><span data-ttu-id="563e2-285">实现 HTTP-POST 创建操作方法</span><span class="sxs-lookup"><span data-stu-id="563e2-285">Implementing the HTTP-POST Create Action Method</span></span>

<span data-ttu-id="563e2-286">我们实现了"创建操作方法"的 HTTP-GET 版本。</span><span class="sxs-lookup"><span data-stu-id="563e2-286">We have the HTTP-GET version of our Create action method implemented.</span></span> <span data-ttu-id="563e2-287">当用户单击"保存"按钮时，它会执行表单发布到 */Dinners/Create* URL，并使用 HTTP POST 谓词&lt;提交&gt;HTML 输入表单值。</span><span class="sxs-lookup"><span data-stu-id="563e2-287">When a user clicks the "Save" button it performs a form post to the */Dinners/Create* URL, and submits the HTML &lt;input&gt; form values using the HTTP POST verb.</span></span>

<span data-ttu-id="563e2-288">现在，让我们实现创建操作方法的 HTTP POST 行为。</span><span class="sxs-lookup"><span data-stu-id="563e2-288">Let's now implement the HTTP POST behavior of our create action method.</span></span> <span data-ttu-id="563e2-289">我们将首先向 DinnersController 添加一个重载的"创建"操作方法，该控制器上具有"AcceptVerbs"属性，指示它处理 HTTP POST 方案：</span><span class="sxs-lookup"><span data-stu-id="563e2-289">We'll begin by adding an overloaded "Create" action method to our DinnersController that has an "AcceptVerbs" attribute on it that indicates it handles HTTP POST scenarios:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample25.cs)]

<span data-ttu-id="563e2-290">我们可以通过多种方式访问启用 HTTP-POST 的"创建"方法中的已过帐表单参数。</span><span class="sxs-lookup"><span data-stu-id="563e2-290">There are a variety of ways we can access the posted form parameters within our HTTP-POST enabled "Create" method.</span></span>

<span data-ttu-id="563e2-291">一种方法是创建新的 Dinner 对象，然后使用*UpdateModel（）* 帮助器方法（就像我们使用"编辑"操作所做的那样）使用张贴的表单值填充它。</span><span class="sxs-lookup"><span data-stu-id="563e2-291">One approach is to create a new Dinner object and then use the *UpdateModel()* helper method (like we did with the Edit action) to populate it with the posted form values.</span></span> <span data-ttu-id="563e2-292">然后，我们可以将其添加到 DinnerRepository 中，将其保存到数据库中，并将用户重定向到"详细信息"操作，以便使用以下代码显示新创建的 Dinner：</span><span class="sxs-lookup"><span data-stu-id="563e2-292">We can then add it to our DinnerRepository, persist it to the database, and redirect the user to our Details action to show the newly created Dinner using the code below:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample26.cs)]

<span data-ttu-id="563e2-293">或者，我们可以使用一种方法，其中我们的 Create（） 操作方法将 Dinner 对象作为方法参数。</span><span class="sxs-lookup"><span data-stu-id="563e2-293">Alternatively, we can use an approach where we have our Create() action method take a Dinner object as a method parameter.</span></span> <span data-ttu-id="563e2-294">然后ASP.NET MVC 将自动为我们实例化新的 Dinner 对象，使用表单输入填充其属性，并将其传递给我们的操作方法：</span><span class="sxs-lookup"><span data-stu-id="563e2-294">ASP.NET MVC will then automatically instantiate a new Dinner object for us, populate its properties using the form inputs, and pass it to our action method:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample27.cs)]

<span data-ttu-id="563e2-295">上述操作方法通过检查 ModelState.IsValid 属性，验证 Dinner 对象已成功填充表单后值。</span><span class="sxs-lookup"><span data-stu-id="563e2-295">Our action method above verifies that the Dinner object has been successfully populated with the form post values by checking the ModelState.IsValid property.</span></span> <span data-ttu-id="563e2-296">如果存在输入转换问题（例如：EventDate 属性的"BOGUS"字符串），并且有任何问题，我们的操作方法将重新显示窗体，则返回 false。</span><span class="sxs-lookup"><span data-stu-id="563e2-296">This will return false if there are input conversion issues (for example: a string of "BOGUS" for the EventDate property), and if there are any issues our action method redisplays the form.</span></span>

<span data-ttu-id="563e2-297">如果输入值有效，则操作方法将尝试将新 Dinner 添加到 DinnerRepository 中。</span><span class="sxs-lookup"><span data-stu-id="563e2-297">If the input values are valid, then the action method attempts to add and save the new Dinner to the DinnerRepository.</span></span> <span data-ttu-id="563e2-298">它将这项工作包装在 try/catch 块中，如果有任何违反业务规则的行为（这将导致晚餐存储库.Save（） 方法引发异常，则重新显示表单。</span><span class="sxs-lookup"><span data-stu-id="563e2-298">It wraps this work within a try/catch block and redisplays the form if there are any business rule violations (which would cause the dinnerRepository.Save() method to raise an exception).</span></span>

<span data-ttu-id="563e2-299">要查看此错误处理行为是否在起作用，我们可以请求 */Dinners/Create* URL 并填写有关新晚餐的详细信息。</span><span class="sxs-lookup"><span data-stu-id="563e2-299">To see this error handling behavior in action, we can request the */Dinners/Create* URL and fill out details about a new Dinner.</span></span> <span data-ttu-id="563e2-300">输入或值不正确将导致重新显示创建窗体，并突出显示错误如下：</span><span class="sxs-lookup"><span data-stu-id="563e2-300">Incorrect input or values will cause the create form to be redisplayed with the errors highlighted like below:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image15.png)

<span data-ttu-id="563e2-301">请注意，我们的"创建"窗体如何遵守与"编辑"窗体完全相同的验证和业务规则。</span><span class="sxs-lookup"><span data-stu-id="563e2-301">Notice how our Create form is honoring the exact same validation and business rules as our Edit form.</span></span> <span data-ttu-id="563e2-302">这是因为我们的验证和业务规则是在模型中定义的，并且未嵌入到应用程序的 UI 或控制器中。</span><span class="sxs-lookup"><span data-stu-id="563e2-302">This is because our validation and business rules were defined in the model, and were not embedded within the UI or controller of the application.</span></span> <span data-ttu-id="563e2-303">这意味着我们以后可以在一个位置更改/发展我们的验证或业务规则，并在整个应用程序中应用这些规则。</span><span class="sxs-lookup"><span data-stu-id="563e2-303">This means we can later change/evolve our validation or business rules in a single place and have them apply throughout our application.</span></span> <span data-ttu-id="563e2-304">我们不必更改"编辑"或"创建操作方法"中的任何代码，即可自动遵守任何新规则或对现有规则的修改。</span><span class="sxs-lookup"><span data-stu-id="563e2-304">We will not have to change any code within either our Edit or Create action methods to automatically honor any new rules or modifications to existing ones.</span></span>

<span data-ttu-id="563e2-305">当我们修复输入值并再次单击"保存"按钮时，我们添加到 DinnerRepository 将成功，并且将添加新的 Dinner 添加到数据库中。</span><span class="sxs-lookup"><span data-stu-id="563e2-305">When we fix the input values and click the "Save" button again, our addition to the DinnerRepository will succeed, and a new Dinner will be added to the database.</span></span> <span data-ttu-id="563e2-306">然后，我们将重定向到 */Dinners/详细信息/[id]* URL - 我们将向这里介绍有关新创建的晚餐的详细信息：</span><span class="sxs-lookup"><span data-stu-id="563e2-306">We will then be redirected to the */Dinners/Details/[id]* URL – where we will be presented with details about the newly created Dinner:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image16.png)

### <a name="delete-support"></a><span data-ttu-id="563e2-307">删除支持</span><span class="sxs-lookup"><span data-stu-id="563e2-307">Delete Support</span></span>

<span data-ttu-id="563e2-308">现在，让我们向"删除"支持添加到我们的晚餐控制器。</span><span class="sxs-lookup"><span data-stu-id="563e2-308">Let's now add "Delete" support to our DinnersController.</span></span>

#### <a name="the-http-get-delete-action-method"></a><span data-ttu-id="563e2-309">HTTP-GET 删除操作方法</span><span class="sxs-lookup"><span data-stu-id="563e2-309">The HTTP-GET Delete Action Method</span></span>

<span data-ttu-id="563e2-310">我们将首先实现删除操作方法的 HTTP GET 行为。</span><span class="sxs-lookup"><span data-stu-id="563e2-310">We'll begin by implementing the HTTP GET behavior of our delete action method.</span></span> <span data-ttu-id="563e2-311">当有人访问 */Dinners/Delete/[id]* URL 时，将调用此方法。</span><span class="sxs-lookup"><span data-stu-id="563e2-311">This method will get called when someone visits the */Dinners/Delete/[id]* URL.</span></span> <span data-ttu-id="563e2-312">以下是实现：</span><span class="sxs-lookup"><span data-stu-id="563e2-312">Below is the implementation:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample28.cs)]

<span data-ttu-id="563e2-313">操作方法尝试检索要删除的"晚餐"。</span><span class="sxs-lookup"><span data-stu-id="563e2-313">The action method attempts to retrieve the Dinner to be deleted.</span></span> <span data-ttu-id="563e2-314">如果"晚餐"存在，则根据"晚餐"对象呈现视图。</span><span class="sxs-lookup"><span data-stu-id="563e2-314">If the Dinner exists it renders a View based on the Dinner object.</span></span> <span data-ttu-id="563e2-315">如果对象不存在（或已被删除），它将返回一个视图，该视图呈现了我们之前为"详细信息"操作方法创建的"NotFound"视图模板。</span><span class="sxs-lookup"><span data-stu-id="563e2-315">If the object doesn't exist (or has already been deleted) it returns a View that renders the "NotFound" view template we created earlier for our "Details" action method.</span></span>

<span data-ttu-id="563e2-316">我们可以在"删除操作"方法中右键单击并选择"添加视图"上下文菜单命令来创建"删除"视图模板。</span><span class="sxs-lookup"><span data-stu-id="563e2-316">We can create the "Delete" view template by right-clicking within the Delete action method and selecting the "Add View" context menu command.</span></span> <span data-ttu-id="563e2-317">在"添加视图"对话框中，我们将指示我们将将 Dinner 对象作为模型传递给视图模板，并选择创建空模板：</span><span class="sxs-lookup"><span data-stu-id="563e2-317">Within the "Add View" dialog we'll indicate that we are passing a Dinner object to our view template as its model, and choose to create an empty template:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image17.png)

<span data-ttu-id="563e2-318">当我们单击"添加"按钮时，Visual Studio 将在"@Views_Dinners"目录中为我们添加新的"Delete.aspx"视图模板文件。</span><span class="sxs-lookup"><span data-stu-id="563e2-318">When we click the "Add" button, Visual Studio will add a new "Delete.aspx" view template file for us within our "\Views\Dinners" directory.</span></span> <span data-ttu-id="563e2-319">我们将向模板添加一些 HTML 和代码，以实现如下删除确认屏幕：</span><span class="sxs-lookup"><span data-stu-id="563e2-319">We'll add some HTML and code to the template to implement a delete confirmation screen like below:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample29.aspx)]

<span data-ttu-id="563e2-320">上面的代码显示要删除的 Dinner 的标题，并在最终用户单击其中的"删除&lt;"&gt;按钮时输出对 /Dinners/Delete/[id] URL 执行 POST 的表单元素。</span><span class="sxs-lookup"><span data-stu-id="563e2-320">The code above displays the title of the Dinner to be deleted, and outputs a &lt;form&gt; element that does a POST to the /Dinners/Delete/[id] URL if the end-user clicks the "Delete" button within it.</span></span>

<span data-ttu-id="563e2-321">当我们运行应用程序并访问有效 Dinner 对象的 *"/晚餐/删除/[id]"URL*时，它将呈现如下 UI：</span><span class="sxs-lookup"><span data-stu-id="563e2-321">When we run our application and access the *"/Dinners/Delete/[id]"* URL for a valid Dinner object it renders UI like below:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image18.png)

| <span data-ttu-id="563e2-322">**侧主题：我们为什么要进行 POST？**</span><span class="sxs-lookup"><span data-stu-id="563e2-322">**Side Topic: Why are we doing a POST?**</span></span> |
| --- |
| <span data-ttu-id="563e2-323">您可能会问 – 我们为什么要在"删除"确认屏幕中&lt;创建&gt;表单？</span><span class="sxs-lookup"><span data-stu-id="563e2-323">You might ask – why did we go through the effort of creating a &lt;form&gt; within our Delete confirmation screen?</span></span> <span data-ttu-id="563e2-324">为什么不只使用标准超链接链接到执行实际删除操作的操作方法？</span><span class="sxs-lookup"><span data-stu-id="563e2-324">Why not just use a standard hyperlink to link to an action method that does the actual delete operation?</span></span> <span data-ttu-id="563e2-325">原因是，我们希望小心防范 Web 爬网者和搜索引擎发现我们的 URL，并在跟踪链接时无意中导致数据被删除。</span><span class="sxs-lookup"><span data-stu-id="563e2-325">The reason is because we want to be careful to guard against web-crawlers and search engines discovering our URLs and inadvertently causing data to be deleted when they follow the links.</span></span> <span data-ttu-id="563e2-326">基于 HTTP-GET 的 URL 被视为"安全"的 URL，它们可以访问/爬网，并且它们不应遵循 HTTP-POST URL。</span><span class="sxs-lookup"><span data-stu-id="563e2-326">HTTP-GET based URLs are considered "safe" for them to access/crawl, and they are supposed to not follow HTTP-POST ones.</span></span> <span data-ttu-id="563e2-327">一个好的规则是确保您始终将破坏性或数据修改操作放在 HTTP-POST 请求后面。</span><span class="sxs-lookup"><span data-stu-id="563e2-327">A good rule is to make sure you always put destructive or data modifying operations behind HTTP-POST requests.</span></span> |

#### <a name="implementing-the-http-post-delete-action-method"></a><span data-ttu-id="563e2-328">实现 HTTP-POST 删除操作方法</span><span class="sxs-lookup"><span data-stu-id="563e2-328">Implementing the HTTP-POST Delete Action Method</span></span>

<span data-ttu-id="563e2-329">现在，我们实现了 HTTP-GET 版本的删除操作方法，显示删除确认屏幕。</span><span class="sxs-lookup"><span data-stu-id="563e2-329">We now have the HTTP-GET version of our Delete action method implemented which displays a delete confirmation screen.</span></span> <span data-ttu-id="563e2-330">当最终用户单击"删除"按钮时，它将执行表单发布到 */Dinners/Dinner/[id]* URL。</span><span class="sxs-lookup"><span data-stu-id="563e2-330">When an end user clicks the "Delete" button it will perform a form post to the */Dinners/Dinner/[id]* URL.</span></span>

<span data-ttu-id="563e2-331">现在，让我们使用以下代码实现删除操作方法的 HTTP"POST"行为：</span><span class="sxs-lookup"><span data-stu-id="563e2-331">Let's now implement the HTTP "POST" behavior of the delete action method using the code below:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample30.cs)]

<span data-ttu-id="563e2-332">HTTP-POST 版本的"删除"操作方法尝试检索要删除的晚餐对象。</span><span class="sxs-lookup"><span data-stu-id="563e2-332">The HTTP-POST version of our Delete action method attempts to retrieve the dinner object to delete.</span></span> <span data-ttu-id="563e2-333">如果找不到它（因为它已被删除），它将呈现我们的"未找到"模板。</span><span class="sxs-lookup"><span data-stu-id="563e2-333">If it can't find it (because it has already been deleted) it renders our "NotFound" template.</span></span> <span data-ttu-id="563e2-334">如果它找到晚餐，它会从晚餐存储库中删除它。</span><span class="sxs-lookup"><span data-stu-id="563e2-334">If it finds the Dinner, it deletes it from the DinnerRepository.</span></span> <span data-ttu-id="563e2-335">然后，它呈现一个"已删除"模板。</span><span class="sxs-lookup"><span data-stu-id="563e2-335">It then renders a "Deleted" template.</span></span>

<span data-ttu-id="563e2-336">要实现"已删除"模板，我们将在操作方法中右键单击并选择"添加视图"上下文菜单。</span><span class="sxs-lookup"><span data-stu-id="563e2-336">To implement the "Deleted" template we'll right-click in the action method and choose the "Add View" context menu.</span></span> <span data-ttu-id="563e2-337">我们将视图命名为"已删除"，并将其命名为空模板（而不是采用强类型模型对象）。</span><span class="sxs-lookup"><span data-stu-id="563e2-337">We'll name our view "Deleted" and have it be an empty template (and not take a strongly-typed model object).</span></span> <span data-ttu-id="563e2-338">然后，我们将向其中添加一些 HTML 内容：</span><span class="sxs-lookup"><span data-stu-id="563e2-338">We'll then add some HTML content to it:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample31.aspx)]

<span data-ttu-id="563e2-339">现在，当我们运行我们的应用程序，并访问有效的晚餐对象的 *"/晚餐/删除/[id]"URL*时，它将呈现我们的晚餐删除确认屏幕，如下所示：</span><span class="sxs-lookup"><span data-stu-id="563e2-339">And now when we run our application and access the *"/Dinners/Delete/[id]"* URL for a valid Dinner object it will render our Dinner delete confirmation screen like below:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image19.png)

<span data-ttu-id="563e2-340">当我们单击"删除"按钮时，它将对 */Dinners/Delete/[id]* URL 执行 HTTP-POST，这将从我们的数据库中删除晚餐，并显示我们的"已删除"视图模板：</span><span class="sxs-lookup"><span data-stu-id="563e2-340">When we click the "Delete" button it will perform an HTTP-POST to the */Dinners/Delete/[id]* URL, which will delete the Dinner from our database, and display our "Deleted" view template:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image20.png)

### <a name="model-binding-security"></a><span data-ttu-id="563e2-341">模型绑定安全性</span><span class="sxs-lookup"><span data-stu-id="563e2-341">Model Binding Security</span></span>

<span data-ttu-id="563e2-342">我们讨论了使用ASP.NET MVC 的内置模型绑定功能的两种不同的方法。</span><span class="sxs-lookup"><span data-stu-id="563e2-342">We've discussed two different ways to use the built-in model-binding features of ASP.NET MVC.</span></span> <span data-ttu-id="563e2-343">第一个使用 UpdateModel（） 方法更新现有模型对象的属性，第二个使用 ASP.NET mVC 支持将模型对象作为操作方法参数传递。</span><span class="sxs-lookup"><span data-stu-id="563e2-343">The first using the UpdateModel() method to update properties on an existing model object, and the second using ASP.NET MVC's support for passing model objects in as action method parameters.</span></span> <span data-ttu-id="563e2-344">这两种技术都非常强大，非常有用。</span><span class="sxs-lookup"><span data-stu-id="563e2-344">Both of these techniques are very powerful and extremely useful.</span></span>

<span data-ttu-id="563e2-345">这种力量也带来了责任。</span><span class="sxs-lookup"><span data-stu-id="563e2-345">This power also brings with it responsibility.</span></span> <span data-ttu-id="563e2-346">在接受任何用户输入时，始终对安全性持偏执状态很重要，在绑定对象以形成输入时也是如此。</span><span class="sxs-lookup"><span data-stu-id="563e2-346">It is important to always be paranoid about security when accepting any user input, and this is also true when binding objects to form input.</span></span> <span data-ttu-id="563e2-347">您应该始终小心 HTML 编码任何用户输入的值，以避免 HTML 和 JavaScript 注入攻击，并小心 SQL 注入攻击（请注意：我们使用 LINQ 到 SQL 作为应用程序，它会自动对参数进行编码，以防止这些类型的攻击）。</span><span class="sxs-lookup"><span data-stu-id="563e2-347">You should be careful to always HTML encode any user-entered values to avoid HTML and JavaScript injection attacks, and be careful of SQL injection attacks (note: we are using LINQ to SQL for our application, which automatically encodes parameters to prevent these types of attacks).</span></span> <span data-ttu-id="563e2-348">您绝不应仅依赖客户端验证，并且始终使用服务器端验证来防止黑客试图向您发送虚假值。</span><span class="sxs-lookup"><span data-stu-id="563e2-348">You should never rely on client-side validation alone, and always employ server-side validation to guard against hackers attempting to send you bogus values.</span></span>

<span data-ttu-id="563e2-349">使用 ASP.NET MVC 的绑定功能时，要确保考虑的另一个安全项是绑定对象的范围。</span><span class="sxs-lookup"><span data-stu-id="563e2-349">One additional security item to make sure you think about when using the binding features of ASP.NET MVC is the scope of the objects you are binding.</span></span> <span data-ttu-id="563e2-350">具体来说，您希望确保您了解允许绑定的属性的安全含义，并确保仅允许最终用户更新真正应该更新的属性。</span><span class="sxs-lookup"><span data-stu-id="563e2-350">Specifically, you want to make sure you understand the security implications of the properties you are allowing to be bound, and make sure you only allow those properties that really should be updatable by an end-user to be updated.</span></span>

<span data-ttu-id="563e2-351">默认情况下，UpdateModel（） 方法将尝试更新模型对象上与传入窗体参数值匹配的所有属性。</span><span class="sxs-lookup"><span data-stu-id="563e2-351">By default, the UpdateModel() method will attempt to update all properties on the model object that match incoming form parameter values.</span></span> <span data-ttu-id="563e2-352">同样，默认情况下作为操作方法参数传递的对象可以通过窗体参数设置其所有属性。</span><span class="sxs-lookup"><span data-stu-id="563e2-352">Likewise, objects passed as action method parameters also by default can have all of their properties set via form parameters.</span></span>

#### <a name="locking-down-binding-on-a-per-usage-basis"></a><span data-ttu-id="563e2-353">按使用情况锁定绑定</span><span class="sxs-lookup"><span data-stu-id="563e2-353">Locking down binding on a per-usage basis</span></span>

<span data-ttu-id="563e2-354">通过提供可更新的属性的显式"包含列表"，可以按使用情况锁定绑定策略。</span><span class="sxs-lookup"><span data-stu-id="563e2-354">You can lock down the binding policy on a per-usage basis by providing an explicit "include list" of properties that can be updated.</span></span> <span data-ttu-id="563e2-355">这可以通过将额外的字符串数组参数传递给 UpdateModel（） 方法来实现，如下所示：</span><span class="sxs-lookup"><span data-stu-id="563e2-355">This can be done by passing an extra string array parameter to the UpdateModel() method like below:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample32.cs)]

<span data-ttu-id="563e2-356">作为操作方法参数传递的对象还支持 [Bind] 属性，该属性允许如下指定允许属性的"包含列表"：</span><span class="sxs-lookup"><span data-stu-id="563e2-356">Objects passed as action method parameters also support a [Bind] attribute that enables an "include list" of allowed properties to be specified like below:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample33.cs)]

#### <a name="locking-down-binding-on-a-type-basis"></a><span data-ttu-id="563e2-357">在类型上锁定绑定</span><span class="sxs-lookup"><span data-stu-id="563e2-357">Locking down binding on a type basis</span></span>

<span data-ttu-id="563e2-358">您还可以按类型锁定绑定规则。</span><span class="sxs-lookup"><span data-stu-id="563e2-358">You can also lock down the binding rules on a per-type basis.</span></span> <span data-ttu-id="563e2-359">这允许您指定绑定规则一次，然后将它们应用于所有控制器和操作方法的所有方案（包括 UpdateModel 和操作方法参数方案）。</span><span class="sxs-lookup"><span data-stu-id="563e2-359">This allows you to specify the binding rules once, and then have them apply in all scenarios (including both UpdateModel and action method parameter scenarios) across all controllers and action methods.</span></span>

<span data-ttu-id="563e2-360">您可以通过将 [Bind] 属性添加到类型上，或通过在应用程序的 Global.asax 文件中注册来自定义每种类型的绑定规则（对于您不拥有该类型的方案非常有用）。</span><span class="sxs-lookup"><span data-stu-id="563e2-360">You can customize the per-type binding rules by adding a [Bind] attribute onto a type, or by registering it within the Global.asax file of the application (useful for scenarios where you don't own the type).</span></span> <span data-ttu-id="563e2-361">然后，可以使用 Bind 属性的"包含"和"排除"属性来控制特定类或接口可绑定哪些属性。</span><span class="sxs-lookup"><span data-stu-id="563e2-361">You can then use the Bind attribute's Include and Exclude properties to control which properties are bindable for the particular class or interface.</span></span>

<span data-ttu-id="563e2-362">我们将在 NerdDinner 应用程序中对 Dinner 类使用此技术，并为其添加 [Bind] 属性，将可绑定属性列表限制为以下内容：</span><span class="sxs-lookup"><span data-stu-id="563e2-362">We'll use this technique for the Dinner class in our NerdDinner application, and add a [Bind] attribute to it that restricts the list of bindable properties to the following:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample34.cs)]

<span data-ttu-id="563e2-363">请注意，我们不允许通过绑定操作 RSSP 集合，也不允许通过绑定设置 DinnerID 或托管比属性。</span><span class="sxs-lookup"><span data-stu-id="563e2-363">Notice we are not allowing the RSVPs collection to be manipulated via binding, nor are we allowing the DinnerID or HostedBy properties to be set via binding.</span></span> <span data-ttu-id="563e2-364">出于安全原因，我们将只使用操作方法中的显式代码来操作这些特定属性。</span><span class="sxs-lookup"><span data-stu-id="563e2-364">For security reasons we'll instead only manipulate these particular properties using explicit code within our action methods.</span></span>

### <a name="crud-wrap-up"></a><span data-ttu-id="563e2-365">CRUD 总结</span><span class="sxs-lookup"><span data-stu-id="563e2-365">CRUD Wrap-Up</span></span>

<span data-ttu-id="563e2-366">ASP.NET MVC 包含许多内置功能，可帮助实现表单发布方案。</span><span class="sxs-lookup"><span data-stu-id="563e2-366">ASP.NET MVC includes a number of built-in features that help with implementing form posting scenarios.</span></span> <span data-ttu-id="563e2-367">我们使用多种功能在晚餐存储库上提供 CRUD UI 支持。</span><span class="sxs-lookup"><span data-stu-id="563e2-367">We used a variety of these features to provide CRUD UI support on top of our DinnerRepository.</span></span>

<span data-ttu-id="563e2-368">我们使用以模型为中心的方法来实现我们的应用程序。</span><span class="sxs-lookup"><span data-stu-id="563e2-368">We are using a model-focused approach to implement our application.</span></span> <span data-ttu-id="563e2-369">这意味着我们所有的验证和业务规则逻辑都在我们的模型层中定义，而不是在我们的控制器或视图中定义。</span><span class="sxs-lookup"><span data-stu-id="563e2-369">This means that all our validation and business rule logic is defined within our model layer – and not within our controllers or views.</span></span> <span data-ttu-id="563e2-370">我们的 Controller 类和 View 模板都不知道我们的 Dinner 模型类正在强制执行的特定业务规则。</span><span class="sxs-lookup"><span data-stu-id="563e2-370">Neither our Controller class nor our View templates know anything about the specific business rules being enforced by our Dinner model class.</span></span>

<span data-ttu-id="563e2-371">这将保持我们的应用程序体系结构清洁，并使其更易于测试。</span><span class="sxs-lookup"><span data-stu-id="563e2-371">This will keep our application architecture clean and make it easier to test.</span></span> <span data-ttu-id="563e2-372">将来，我们可以向模型层添加其他业务规则，而不必对我们的控制器或视图*进行任何代码更改*，以便支持这些规则。</span><span class="sxs-lookup"><span data-stu-id="563e2-372">We can add additional business rules to our model layer in the future and *not have to make any code changes* to our Controller or View in order for them to be supported.</span></span> <span data-ttu-id="563e2-373">这将为我们提供极大的敏捷性，以便我们在未来发展和改变我们的应用程序。</span><span class="sxs-lookup"><span data-stu-id="563e2-373">This is going to provide us with a great deal of agility to evolve and change our application in the future.</span></span>

<span data-ttu-id="563e2-374">我们的晚餐控制器现在启用晚餐列表/详细信息，以及创建、编辑和删除支持。</span><span class="sxs-lookup"><span data-stu-id="563e2-374">Our DinnersController now enables Dinner listings/details, as well as create, edit and delete support.</span></span> <span data-ttu-id="563e2-375">类的完整代码如下所示：</span><span class="sxs-lookup"><span data-stu-id="563e2-375">The complete code for the class can be found below:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample35.cs)]

### <a name="next-step"></a><span data-ttu-id="563e2-376">下一步</span><span class="sxs-lookup"><span data-stu-id="563e2-376">Next Step</span></span>

<span data-ttu-id="563e2-377">现在，我们的 DinnersController 类中实现了基本的 CRUD（创建、读取、更新和删除）支持。</span><span class="sxs-lookup"><span data-stu-id="563e2-377">We now have basic CRUD (Create, Read, Update and Delete) support implement within our DinnersController class.</span></span>

<span data-ttu-id="563e2-378">现在，让我们来看看如何使用 ViewData 和 ViewModel 类在我们的窗体上启用更丰富的 UI。</span><span class="sxs-lookup"><span data-stu-id="563e2-378">Let's now look at how we can use ViewData and ViewModel classes to enable even richer UI on our forms.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="563e2-379">[上一页](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
> [下一页](use-viewdata-and-implement-viewmodel-classes.md)</span><span class="sxs-lookup"><span data-stu-id="563e2-379">[Previous](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
[Next](use-viewdata-and-implement-viewmodel-classes.md)</span></span>

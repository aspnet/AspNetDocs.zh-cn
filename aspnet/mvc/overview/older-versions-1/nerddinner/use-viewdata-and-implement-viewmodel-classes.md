---
uid: mvc/overview/older-versions-1/nerddinner/use-viewdata-and-implement-viewmodel-classes
title: 使用视图数据并实现视图模型类 |微软文档
author: rick-anderson
description: 步骤 6 显示了如何支持更丰富的表单编辑方案，并讨论了两种方法，可用于将数据从控制器传递到视图：...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 5755ec4c-60f1-4057-9ec0-3a5de3a20e23
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-viewdata-and-implement-viewmodel-classes
msc.type: authoredcontent
ms.openlocfilehash: 7fa2af2a55d12bbe11b29dff594823a1e5ea0152
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541099"
---
# <a name="use-viewdata-and-implement-viewmodel-classes"></a><span data-ttu-id="b1dec-103">使用 ViewData 和实现 ViewModel 类</span><span class="sxs-lookup"><span data-stu-id="b1dec-103">Use ViewData and Implement ViewModel Classes</span></span>

<span data-ttu-id="b1dec-104">由[微软](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="b1dec-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="b1dec-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="b1dec-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="b1dec-106">这是一个免费的["NerdDinner"应用程序教程](introducing-the-nerddinner-tutorial.md)的第6步，该教程演示如何使用ASP.NET MVC 1 构建小型但完整的 Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="b1dec-106">This is step 6 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="b1dec-107">步骤 6 显示了如何支持更丰富的表单编辑方案，并讨论了可用于将数据从控制器传递到视图的两种方法：ViewData 和 ViewModel。</span><span class="sxs-lookup"><span data-stu-id="b1dec-107">Step 6 shows how enable support for richer form editing scenarios, and also discusses two approaches that can be used to pass data from controllers to views: ViewData and ViewModel.</span></span>
> 
> <span data-ttu-id="b1dec-108">如果您使用的是ASP.NET MVC 3，我们建议您按照[MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC 音乐商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程进行操作。</span><span class="sxs-lookup"><span data-stu-id="b1dec-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-6-viewdata-and-viewmodel"></a><span data-ttu-id="b1dec-109">神经晚餐步骤 6：查看数据和视图模型</span><span class="sxs-lookup"><span data-stu-id="b1dec-109">NerdDinner Step 6: ViewData and ViewModel</span></span>

<span data-ttu-id="b1dec-110">我们介绍了一些表单发布方案，并讨论了如何实现创建、更新和删除 （CRUD） 支持。</span><span class="sxs-lookup"><span data-stu-id="b1dec-110">We've covered a number of form post scenarios, and discussed how to implement create, update and delete (CRUD) support.</span></span> <span data-ttu-id="b1dec-111">现在，我们将进一步实施 DinnersController，并支持更丰富的表单编辑方案。</span><span class="sxs-lookup"><span data-stu-id="b1dec-111">We'll now take our DinnersController implementation further and enable support for richer form editing scenarios.</span></span> <span data-ttu-id="b1dec-112">在此过程中，我们将讨论两种可用于将数据从控制器传递到视图的方法：ViewData 和 ViewModel。</span><span class="sxs-lookup"><span data-stu-id="b1dec-112">While doing this we'll discuss two approaches that can be used to pass data from controllers to views: ViewData and ViewModel.</span></span>

### <a name="passing-data-from-controllers-to-view-templates"></a><span data-ttu-id="b1dec-113">将数据从控制器传递到视图模板</span><span class="sxs-lookup"><span data-stu-id="b1dec-113">Passing Data from Controllers to View-Templates</span></span>

<span data-ttu-id="b1dec-114">MVC 模式的一个定义特征是严格"关注点分离"，它有助于在应用程序的不同组件之间强制执行。</span><span class="sxs-lookup"><span data-stu-id="b1dec-114">One of the defining characteristics of the MVC pattern is the strict "separation of concerns" it helps enforce between the different components of an application.</span></span> <span data-ttu-id="b1dec-115">模型、控制器和视图都有定义明确的角色和职责，它们之间以定义明确的方式相互通信。</span><span class="sxs-lookup"><span data-stu-id="b1dec-115">Models, Controllers and Views each have well defined roles and responsibilities, and they communicate amongst each other in well defined ways.</span></span> <span data-ttu-id="b1dec-116">这有助于提高可测试性和代码重用性。</span><span class="sxs-lookup"><span data-stu-id="b1dec-116">This helps promote testability and code reuse.</span></span>

<span data-ttu-id="b1dec-117">当 Controller 类决定将 HTML 响应呈现回客户端时，它负责显式将呈现响应所需的所有数据传递给视图模板。</span><span class="sxs-lookup"><span data-stu-id="b1dec-117">When a Controller class decides to render an HTML response back to a client, it is responsible for explicitly passing to the view template all of the data needed to render the response.</span></span> <span data-ttu-id="b1dec-118">视图模板绝不应执行任何数据检索或应用程序逻辑，而应限制自己仅具有由控制器从模型/数据中驱动的呈现代码。</span><span class="sxs-lookup"><span data-stu-id="b1dec-118">View templates should never perform any data retrieval or application logic – and should instead limit themselves to only have rendering code that is driven off of the model/data passed to it by the controller.</span></span>

<span data-ttu-id="b1dec-119">现在，我们的 DinnersController 类传递给视图模板的模型数据简单而直接 — 在 Index（）的情况下，是晚餐对象的列表，如果是详细信息（、Edit（）、Create（） 和删除（）的情况下，只有一个晚餐对象。</span><span class="sxs-lookup"><span data-stu-id="b1dec-119">Right now the model data being passed by our DinnersController class to our view templates is simple and straight-forward – a list of Dinner objects in the case of Index(), and a single Dinner object in the case of Details(), Edit(), Create() and Delete().</span></span> <span data-ttu-id="b1dec-120">当我们向应用程序添加更多 UI 功能时，我们通常需要传递的不仅仅是这些数据，才能在视图模板中呈现 HTML 响应。</span><span class="sxs-lookup"><span data-stu-id="b1dec-120">As we add more UI capabilities to our application, we are often going to need to pass more than just this data to render HTML responses within our view templates.</span></span> <span data-ttu-id="b1dec-121">例如，我们可能希望将"编辑"和"创建视图"中的"国家/地区"字段从 HTML 文本框更改为下拉列表。</span><span class="sxs-lookup"><span data-stu-id="b1dec-121">For example, we might want to change the "Country" field within our Edit and Create views from being an HTML textbox to a dropdownlist.</span></span> <span data-ttu-id="b1dec-122">我们不是在视图模板中硬编码国家名称的下拉列表，而是希望从我们动态填充的支持国家/地区列表中生成它。</span><span class="sxs-lookup"><span data-stu-id="b1dec-122">Rather than hard-code the dropdown list of country names in the view template, we might want to generate it from a list of supported countries that we populate dynamically.</span></span> <span data-ttu-id="b1dec-123">我们需要一种方法，将 Dinner 对象*和支持*的国家/地区列表从控制器传递到视图模板。</span><span class="sxs-lookup"><span data-stu-id="b1dec-123">We will need a way to pass both the Dinner object *and* the list of supported countries from our controller to our view templates.</span></span>

<span data-ttu-id="b1dec-124">让我们来看看两种实现此目的的方法。</span><span class="sxs-lookup"><span data-stu-id="b1dec-124">Let's look at two ways we can accomplish this.</span></span>

### <a name="using-the-viewdata-dictionary"></a><span data-ttu-id="b1dec-125">使用视图数据字典</span><span class="sxs-lookup"><span data-stu-id="b1dec-125">Using the ViewData Dictionary</span></span>

<span data-ttu-id="b1dec-126">控制器基类公开一个"ViewData"字典属性，该属性可用于将其他数据项从控制器传递到视图。</span><span class="sxs-lookup"><span data-stu-id="b1dec-126">The Controller base class exposes a "ViewData" dictionary property that can be used to pass additional data items from Controllers to Views.</span></span>

<span data-ttu-id="b1dec-127">例如，为了支持我们希望将"编辑"视图中的"国家/地区"文本框从 HTML 文本框更改为下拉列表的方案，我们可以更新我们的 Edit（） 操作方法，以传递（除了晚餐对象之外）可用作国家/地区下拉列表的模型的 SelectList 对象。</span><span class="sxs-lookup"><span data-stu-id="b1dec-127">For example, to support the scenario where we want to change the "Country" textbox within our Edit view from being an HTML textbox to a dropdownlist, we can update our Edit() action method to pass (in addition to a Dinner object) a SelectList object that can be used as the model of a countries dropdownlist.</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample1.cs)]

<span data-ttu-id="b1dec-128">上面 SelectList 的构造函数正在接受要使用下拉列表以及当前选择的值填充下拉列表的县列表。</span><span class="sxs-lookup"><span data-stu-id="b1dec-128">The constructor of the SelectList above is accepting a list of counties to populate the drop-downlist with, as well as the currently selected value.</span></span>

<span data-ttu-id="b1dec-129">然后，我们可以更新我们的 Edit.aspx 视图模板，以使用 Html.DropDownList（） 帮助程序方法，而不是我们以前使用的 Html.TextBox（） 帮助器方法：</span><span class="sxs-lookup"><span data-stu-id="b1dec-129">We can then update our Edit.aspx view template to use the Html.DropDownList() helper method instead of the Html.TextBox() helper method we used previously:</span></span>

[!code-aspx[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample2.aspx)]

<span data-ttu-id="b1dec-130">上面的 Html.DropDownList（） 帮助器方法采用两个参数。</span><span class="sxs-lookup"><span data-stu-id="b1dec-130">The Html.DropDownList() helper method above takes two parameters.</span></span> <span data-ttu-id="b1dec-131">第一个是要输出的 HTML 窗体元素的名称。</span><span class="sxs-lookup"><span data-stu-id="b1dec-131">The first is the name of the HTML form element to output.</span></span> <span data-ttu-id="b1dec-132">第二个是我们通过 ViewData 字典传递的"选择列表"模型。</span><span class="sxs-lookup"><span data-stu-id="b1dec-132">The second is the "SelectList" model we passed via the ViewData dictionary.</span></span> <span data-ttu-id="b1dec-133">我们使用 C#"as"关键字将字典中的类型转换为 SelectList。</span><span class="sxs-lookup"><span data-stu-id="b1dec-133">We are using the C# "as" keyword to cast the type within the dictionary as a SelectList.</span></span>

<span data-ttu-id="b1dec-134">现在，当我们运行应用程序并访问浏览器中的 */Dinners/Edit/1* URL 时，我们将看到我们的编辑 UI 已更新以显示国家/地区列表而不是文本框：</span><span class="sxs-lookup"><span data-stu-id="b1dec-134">And now when we run our application and access the */Dinners/Edit/1* URL within our browser we'll see that our edit UI has been updated to display a dropdownlist of countries instead of a textbox:</span></span>

![](use-viewdata-and-implement-viewmodel-classes/_static/image1.png)

<span data-ttu-id="b1dec-135">由于我们还从 HTTP-POST Edit 方法呈现 Edit 视图模板（在发生错误时），我们希望确保在错误方案中呈现视图模板时，还要更新此方法以将 SelectList 添加到 ViewData：</span><span class="sxs-lookup"><span data-stu-id="b1dec-135">Because we also render the Edit view template from the HTTP-POST Edit method (in scenarios when errors occur), we'll want to make sure that we also update this method to add the SelectList to ViewData when the view template is rendered in error scenarios:</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample3.cs)]

<span data-ttu-id="b1dec-136">现在，我们的晚餐控制器编辑方案支持下拉列表。</span><span class="sxs-lookup"><span data-stu-id="b1dec-136">And now our DinnersController edit scenario supports a DropDownList.</span></span>

### <a name="using-a-viewmodel-pattern"></a><span data-ttu-id="b1dec-137">使用视图模型模式</span><span class="sxs-lookup"><span data-stu-id="b1dec-137">Using a ViewModel Pattern</span></span>

<span data-ttu-id="b1dec-138">ViewData 字典方法具有相当快速且易于实现的好处。</span><span class="sxs-lookup"><span data-stu-id="b1dec-138">The ViewData dictionary approach has the benefit of being fairly fast and easy to implement.</span></span> <span data-ttu-id="b1dec-139">但是，有些开发人员不喜欢使用基于字符串的字典，因为拼写错误可能导致在编译时不会捕获的错误。</span><span class="sxs-lookup"><span data-stu-id="b1dec-139">Some developers don't like using string-based dictionaries, though, since typos can lead to errors that will not be caught at compile-time.</span></span> <span data-ttu-id="b1dec-140">未键入的 ViewData 字典还要求在视图模板中使用强类型语言（如 C#）时使用"as"运算符或强制转换。</span><span class="sxs-lookup"><span data-stu-id="b1dec-140">The un-typed ViewData dictionary also requires using the "as" operator or casting when using a strongly-typed language like C# in a view template.</span></span>

<span data-ttu-id="b1dec-141">我们可以使用的另一种方法是通常称为"视图模型"模式的方法。</span><span class="sxs-lookup"><span data-stu-id="b1dec-141">An alternative approach that we could use is one often referred to as the "ViewModel" pattern.</span></span> <span data-ttu-id="b1dec-142">使用此模式时，我们创建针对特定视图方案优化的强类型类，并公开视图模板所需的动态值/内容的属性。</span><span class="sxs-lookup"><span data-stu-id="b1dec-142">When using this pattern we create strongly-typed classes that are optimized for our specific view scenarios, and which expose properties for the dynamic values/content needed by our view templates.</span></span> <span data-ttu-id="b1dec-143">然后，我们的控制器类可以填充这些视图优化的类并将其传递给我们的视图模板使用。</span><span class="sxs-lookup"><span data-stu-id="b1dec-143">Our controller classes can then populate and pass these view-optimized classes to our view template to use.</span></span> <span data-ttu-id="b1dec-144">这支持视图模板中的类型安全、编译时间检查和编辑器对讲。</span><span class="sxs-lookup"><span data-stu-id="b1dec-144">This enables type-safety, compile-time checking, and editor intellisense within view templates.</span></span>

<span data-ttu-id="b1dec-145">例如，为了启用晚餐表单编辑方案，我们可以创建一个"DinnerFormViewModel"类，如下所示，该类公开了两个强类型属性：一个"晚餐"对象，以及填充国家/地区下拉列表所需的 SelectList 模型：</span><span class="sxs-lookup"><span data-stu-id="b1dec-145">For example, to enable dinner form editing scenarios we can create a "DinnerFormViewModel" class like below that exposes two strongly-typed properties: a Dinner object, and the SelectList model needed to populate the countries dropdownlist:</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample4.cs)]

<span data-ttu-id="b1dec-146">然后，我们可以更新我们的 Edit（） 操作方法，使用从存储库检索的 Dinner 对象创建 DinnerFormViewModel，然后将其传递到视图模板：</span><span class="sxs-lookup"><span data-stu-id="b1dec-146">We can then update our Edit() action method to create the DinnerFormViewModel using the Dinner object we retrieve from our repository, and then pass it to our view template:</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample5.cs)]

<span data-ttu-id="b1dec-147">然后，我们将更新视图模板，以便它期望有一个"DinnerFormViewModel"而不是"Dinner"对象，例如，更改 edit.aspx 页面顶部的"继承"属性：</span><span class="sxs-lookup"><span data-stu-id="b1dec-147">We'll then update our view template so that it expects a "DinnerFormViewModel" instead of a "Dinner" object by changing the "inherits" attribute at the top of the edit.aspx page like so:</span></span>

[!code-cshtml[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample6.cshtml)]

<span data-ttu-id="b1dec-148">一旦我们这样做，视图模板中"模型"属性的对讲义将更新，以反映我们传递的 DinnerFormViewModel 类型的对象模型：</span><span class="sxs-lookup"><span data-stu-id="b1dec-148">Once we do this, the intellisense of the "Model" property within our view template will be updated to reflect the object model of the DinnerFormViewModel type we are passing it:</span></span>

![](use-viewdata-and-implement-viewmodel-classes/_static/image2.png)

![](use-viewdata-and-implement-viewmodel-classes/_static/image3.png)

<span data-ttu-id="b1dec-149">然后，我们可以更新视图代码以摆脱它。</span><span class="sxs-lookup"><span data-stu-id="b1dec-149">We can then update our view code to work off of it.</span></span> <span data-ttu-id="b1dec-150">请注意，下面我们如何不更改要创建的输入元素的名称（表单元素仍将命名为"标题"、"国家/地区"），但我们正在更新 HTML 帮助器方法，以便使用 DinnerFormViewModel 类检索值：</span><span class="sxs-lookup"><span data-stu-id="b1dec-150">Notice below how we are not changing the names of the input elements we are creating (the form elements will still be named "Title", "Country") – but we are updating the HTML Helper methods to retrieve the values using the DinnerFormViewModel class:</span></span>

[!code-aspx[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample7.aspx)]

<span data-ttu-id="b1dec-151">在呈现错误时，我们还将更新编辑帖子方法以使用 DinnerFormViewModel 类：</span><span class="sxs-lookup"><span data-stu-id="b1dec-151">We'll also update our Edit post method to use the DinnerFormViewModel class when rendering errors:</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample8.cs)]

<span data-ttu-id="b1dec-152">我们还可以更新我们的 Create（） 操作方法，以重复使用完全相同的*DinnerFormViewModel*类，使这些国家/地区也能够删除列表。</span><span class="sxs-lookup"><span data-stu-id="b1dec-152">We can also update our Create() action methods to re-use the exact same *DinnerFormViewModel* class to enable the countries DropDownList within those as well.</span></span> <span data-ttu-id="b1dec-153">下面是 HTTP-GET 实现：</span><span class="sxs-lookup"><span data-stu-id="b1dec-153">Below is the HTTP-GET implementation:</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample9.cs)]

<span data-ttu-id="b1dec-154">下面是 HTTP-POST 创建方法的实现：</span><span class="sxs-lookup"><span data-stu-id="b1dec-154">Below is the implementation of the HTTP-POST Create method:</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample10.cs)]

<span data-ttu-id="b1dec-155">现在，我们的"编辑"和"创建"屏幕都支持选择国家/地区的下拉列表。</span><span class="sxs-lookup"><span data-stu-id="b1dec-155">And now both our Edit and Create screens support drop-downlists for picking the country.</span></span>

### <a name="custom-shaped-viewmodel-classes"></a><span data-ttu-id="b1dec-156">自定义形状的视图模型类</span><span class="sxs-lookup"><span data-stu-id="b1dec-156">Custom-shaped ViewModel classes</span></span>

<span data-ttu-id="b1dec-157">在上面的场景中，我们的 DinnerFormViewModel 类直接将 Dinner 模型对象公开为属性，以及支持 SelectList 模型属性。</span><span class="sxs-lookup"><span data-stu-id="b1dec-157">In the scenario above, our DinnerFormViewModel class directly exposes the Dinner model object as a property, along with a supporting SelectList model property.</span></span> <span data-ttu-id="b1dec-158">此方法适用于要在视图模板中创建的 HTML UI 与域模型对象相对接近的情况。</span><span class="sxs-lookup"><span data-stu-id="b1dec-158">This approach works fine for scenarios where the HTML UI we want to create within our view template corresponds relatively closely to our domain model objects.</span></span>

<span data-ttu-id="b1dec-159">对于情况并非如此的情况，可以使用的一个选项是创建一个自定义形状的 ViewModel 类，其对象模型更优化以供视图使用，并且可能与基础域模型对象的外观完全不同。</span><span class="sxs-lookup"><span data-stu-id="b1dec-159">For scenarios where this isn't the case, one option that you can use is to create a custom-shaped ViewModel class whose object model is more optimized for consumption by the view – and which might look completely different from the underlying domain model object.</span></span> <span data-ttu-id="b1dec-160">例如，它可能会公开从多个模型对象收集的不同属性名称和/或聚合属性。</span><span class="sxs-lookup"><span data-stu-id="b1dec-160">For example, it could potentially expose different property names and/or aggregate properties collected from multiple model objects.</span></span>

<span data-ttu-id="b1dec-161">自定义形状的 ViewModel 类既可用于将数据从控制器传递到要渲染的视图，也可用于帮助处理发回控制器操作方法的表单数据。</span><span class="sxs-lookup"><span data-stu-id="b1dec-161">Custom-shaped ViewModel classes can be used both to pass data from controllers to views to render, as well as to help handle form data posted back to a controller's action method.</span></span> <span data-ttu-id="b1dec-162">对于此后续方案，您可能让操作方法使用发布表单的数据更新 ViewModel 对象，然后使用 ViewModel 实例映射或检索实际域模型对象。</span><span class="sxs-lookup"><span data-stu-id="b1dec-162">For this later scenario, you might have the action method update a ViewModel object with the form-posted data, and then use the ViewModel instance to map or retrieve an actual domain model object.</span></span>

<span data-ttu-id="b1dec-163">自定义形状的 ViewModel 类可以提供很大的灵活性，并且每当在视图模板中查找呈现代码或操作方法中的表单发布代码开始变得过于复杂时，都是要调查的内容。</span><span class="sxs-lookup"><span data-stu-id="b1dec-163">Custom-shaped ViewModel classes can provide a great deal of flexibility, and are something to investigate any time you find the rendering code within your view templates or the form-posting code inside your action methods starting to get too complicated.</span></span> <span data-ttu-id="b1dec-164">这通常表明域模型与您生成的 UI 不干净对应，并且中间自定义形状的 ViewModel 类可以提供帮助。</span><span class="sxs-lookup"><span data-stu-id="b1dec-164">This is often a sign that your domain models don't cleanly correspond to the UI you are generating, and that an intermediate custom-shaped ViewModel class can help.</span></span>

### <a name="next-step"></a><span data-ttu-id="b1dec-165">下一步</span><span class="sxs-lookup"><span data-stu-id="b1dec-165">Next Step</span></span>

<span data-ttu-id="b1dec-166">现在，让我们来了解一下如何使用部分页和母版页来重用和共享整个应用程序中的 UI。</span><span class="sxs-lookup"><span data-stu-id="b1dec-166">Let's now look at how we can use partials and master-pages to re-use and share UI across our application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="b1dec-167">[上一页](provide-crud-create-read-update-delete-data-form-entry-support.md)
> [下一页](re-use-ui-using-master-pages-and-partials.md)</span><span class="sxs-lookup"><span data-stu-id="b1dec-167">[Previous](provide-crud-create-read-update-delete-data-form-entry-support.md)
[Next](re-use-ui-using-master-pages-and-partials.md)</span></span>

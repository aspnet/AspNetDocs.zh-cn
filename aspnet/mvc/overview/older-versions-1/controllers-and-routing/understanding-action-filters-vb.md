---
uid: mvc/overview/older-versions-1/controllers-and-routing/understanding-action-filters-vb
title: 了解操作筛选器 （VB） |微软文档
author: rick-anderson
description: 本教程的目的是解释操作筛选器。 操作筛选器是一个属性，您可以应用于控制器操作或整个控制器...
ms.author: riande
ms.date: 10/16/2008
ms.assetid: e83812f2-c53e-4a43-a7c1-d64c59ecf694
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/understanding-action-filters-vb
msc.type: authoredcontent
ms.openlocfilehash: 70ab564bc1217f67874090d2ae6899d9bcd743a1
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542100"
---
# <a name="understanding-action-filters-vb"></a><span data-ttu-id="e1974-104">了解操作筛选器 (VB)</span><span class="sxs-lookup"><span data-stu-id="e1974-104">Understanding Action Filters (VB)</span></span>

<span data-ttu-id="e1974-105">由[微软](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="e1974-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="e1974-106">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="e1974-106">Download PDF</span></span>](https://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_14_VB.pdf)

> <span data-ttu-id="e1974-107">本教程的目的是解释操作筛选器。</span><span class="sxs-lookup"><span data-stu-id="e1974-107">The goal of this tutorial is to explain action filters.</span></span> <span data-ttu-id="e1974-108">操作筛选器是一个属性，您可以应用于控制器操作（或整个控制器），该属性修改操作的执行方式。</span><span class="sxs-lookup"><span data-stu-id="e1974-108">An action filter is an attribute that you can apply to a controller action -- or an entire controller -- that modifies the way in which the action is executed.</span></span>

## <a name="understanding-action-filters"></a><span data-ttu-id="e1974-109">了解操作筛选器</span><span class="sxs-lookup"><span data-stu-id="e1974-109">Understanding Action Filters</span></span>

<span data-ttu-id="e1974-110">本教程的目的是解释操作筛选器。</span><span class="sxs-lookup"><span data-stu-id="e1974-110">The goal of this tutorial is to explain action filters.</span></span> <span data-ttu-id="e1974-111">操作筛选器是一个属性，您可以应用于控制器操作（或整个控制器），该属性修改操作的执行方式。</span><span class="sxs-lookup"><span data-stu-id="e1974-111">An action filter is an attribute that you can apply to a controller action -- or an entire controller -- that modifies the way in which the action is executed.</span></span> <span data-ttu-id="e1974-112">ASP.NET MVC 框架包括多个操作筛选器：</span><span class="sxs-lookup"><span data-stu-id="e1974-112">The ASP.NET MVC framework includes several action filters:</span></span>

- <span data-ttu-id="e1974-113">输出缓存 - 此操作筛选器缓存控制器操作的输出，以指定的时间进行。</span><span class="sxs-lookup"><span data-stu-id="e1974-113">OutputCache – This action filter caches the output of a controller action for a specified amount of time.</span></span>
- <span data-ttu-id="e1974-114">句柄错误 - 此操作筛选器处理执行控制器操作时引发的错误。</span><span class="sxs-lookup"><span data-stu-id="e1974-114">HandleError – This action filter handles errors raised when a controller action executes.</span></span>
- <span data-ttu-id="e1974-115">授权 – 此操作筛选器使您能够限制对特定用户或角色的访问。</span><span class="sxs-lookup"><span data-stu-id="e1974-115">Authorize – This action filter enables you to restrict access to a particular user or role.</span></span>

<span data-ttu-id="e1974-116">您还可以创建自己的自定义操作筛选器。</span><span class="sxs-lookup"><span data-stu-id="e1974-116">You also can create your own custom action filters.</span></span> <span data-ttu-id="e1974-117">例如，您可能希望创建自定义操作筛选器以实现自定义身份验证系统。</span><span class="sxs-lookup"><span data-stu-id="e1974-117">For example, you might want to create a custom action filter in order to implement a custom authentication system.</span></span> <span data-ttu-id="e1974-118">或者，您可能希望创建一个操作筛选器，用于修改控制器操作返回的视图数据。</span><span class="sxs-lookup"><span data-stu-id="e1974-118">Or, you might want to create an action filter that modifies the view data returned by a controller action.</span></span>

<span data-ttu-id="e1974-119">在本教程中，您将了解如何从开始构建操作筛选器。</span><span class="sxs-lookup"><span data-stu-id="e1974-119">In this tutorial, you learn how to build an action filter from the ground up.</span></span> <span data-ttu-id="e1974-120">我们创建一个 Log 操作筛选器，将操作处理的不同阶段记录到可视化工作室输出窗口。</span><span class="sxs-lookup"><span data-stu-id="e1974-120">We create a Log action filter that logs different stages of the processing of an action to the Visual Studio Output window.</span></span>

### <a name="using-an-action-filter"></a><span data-ttu-id="e1974-121">使用操作筛选器</span><span class="sxs-lookup"><span data-stu-id="e1974-121">Using an Action Filter</span></span>

<span data-ttu-id="e1974-122">操作筛选器是属性。</span><span class="sxs-lookup"><span data-stu-id="e1974-122">An action filter is an attribute.</span></span> <span data-ttu-id="e1974-123">您可以将大多数操作筛选器应用于单个控制器操作或整个控制器。</span><span class="sxs-lookup"><span data-stu-id="e1974-123">You can apply most action filters to either an individual controller action or an entire controller.</span></span>

<span data-ttu-id="e1974-124">例如，清单 1 中的数据控制器公开名为`Index()`返回当前时间的操作。</span><span class="sxs-lookup"><span data-stu-id="e1974-124">For example, the Data controller in Listing 1 exposes an action named `Index()` that returns the current time.</span></span> <span data-ttu-id="e1974-125">此操作使用`OutputCache`操作筛选器进行修饰。</span><span class="sxs-lookup"><span data-stu-id="e1974-125">This action is decorated with the `OutputCache` action filter.</span></span> <span data-ttu-id="e1974-126">此筛选器会导致将操作返回的值缓存 10 秒。</span><span class="sxs-lookup"><span data-stu-id="e1974-126">This filter causes the value returned by the action to be cached for 10 seconds.</span></span>

<span data-ttu-id="e1974-127">**清单1 |`Controllers\DataController.vb`**</span><span class="sxs-lookup"><span data-stu-id="e1974-127">**Listing 1 – `Controllers\DataController.vb`**</span></span>

[!code-vb[Main](understanding-action-filters-vb/samples/sample1.vb)]

<span data-ttu-id="e1974-128">如果通过将 URL/`Index()`数据/索引输入浏览器的地址栏并多次点击"刷新"按钮来重复调用该操作，则您将在 10 秒内看到相同的时间。</span><span class="sxs-lookup"><span data-stu-id="e1974-128">If you repeatedly invoke the `Index()` action by entering the URL /Data/Index into the address bar of your browser and hitting the Refresh button multiple times, then you will see the same time for 10 seconds.</span></span> <span data-ttu-id="e1974-129">操作的`Index()`输出缓存 10 秒（参见图 1）。</span><span class="sxs-lookup"><span data-stu-id="e1974-129">The output of the `Index()` action is cached for 10 seconds (see Figure 1).</span></span>

<span data-ttu-id="e1974-130">[![缓存时间](understanding-action-filters-vb/_static/image2.png)](understanding-action-filters-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="e1974-130">[![Cached time](understanding-action-filters-vb/_static/image2.png)](understanding-action-filters-vb/_static/image1.png)</span></span>

<span data-ttu-id="e1974-131">**图 01**： 缓存时间 （[单击以查看全尺寸图像](understanding-action-filters-vb/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="e1974-131">**Figure 01**: Cached time ([Click to view full-size image](understanding-action-filters-vb/_static/image3.png))</span></span>

<span data-ttu-id="e1974-132">在清单 1 中，单个操作筛选器`OutputCache`（操作筛选器）应用于`Index()`该方法。</span><span class="sxs-lookup"><span data-stu-id="e1974-132">In Listing 1, a single action filter – the `OutputCache` action filter – is applied to the `Index()` method.</span></span> <span data-ttu-id="e1974-133">如果需要，可以将多个操作筛选器应用于同一操作。</span><span class="sxs-lookup"><span data-stu-id="e1974-133">If you need, you can apply multiple action filters to the same action.</span></span> <span data-ttu-id="e1974-134">例如，您可能希望将 和`OutputCache``HandleError`操作筛选器应用于同一操作。</span><span class="sxs-lookup"><span data-stu-id="e1974-134">For example, you might want to apply both the `OutputCache` and `HandleError` action filters to the same action.</span></span>

<span data-ttu-id="e1974-135">在清单 1`OutputCache`中，操作筛选器应用于操作`Index()`。</span><span class="sxs-lookup"><span data-stu-id="e1974-135">In Listing 1, the `OutputCache` action filter is applied to the `Index()` action.</span></span> <span data-ttu-id="e1974-136">您还可以将此属性应用于`DataController`类本身。</span><span class="sxs-lookup"><span data-stu-id="e1974-136">You also could apply this attribute to the `DataController` class itself.</span></span> <span data-ttu-id="e1974-137">在这种情况下，控制器公开的任何操作返回的结果将被缓存 10 秒。</span><span class="sxs-lookup"><span data-stu-id="e1974-137">In that case, the result returned by any action exposed by the controller would be cached for 10 seconds.</span></span>

### <a name="the-different-types-of-filters"></a><span data-ttu-id="e1974-138">不同类型的过滤器</span><span class="sxs-lookup"><span data-stu-id="e1974-138">The Different Types of Filters</span></span>

<span data-ttu-id="e1974-139">ASP.NET MVC 框架支持四种不同类型的筛选器：</span><span class="sxs-lookup"><span data-stu-id="e1974-139">The ASP.NET MVC framework supports four different types of filters:</span></span>

1. <span data-ttu-id="e1974-140">授权筛选器 = 实现`IAuthorizationFilter`属性。</span><span class="sxs-lookup"><span data-stu-id="e1974-140">Authorization filters – Implements the `IAuthorizationFilter` attribute.</span></span>
2. <span data-ttu-id="e1974-141">操作筛选器 = 实现`IActionFilter`属性。</span><span class="sxs-lookup"><span data-stu-id="e1974-141">Action filters – Implements the `IActionFilter` attribute.</span></span>
3. <span data-ttu-id="e1974-142">结果筛选器 = 实现`IResultFilter`属性。</span><span class="sxs-lookup"><span data-stu-id="e1974-142">Result filters – Implements the `IResultFilter` attribute.</span></span>
4. <span data-ttu-id="e1974-143">异常筛选器 = 实现`IExceptionFilter`属性。</span><span class="sxs-lookup"><span data-stu-id="e1974-143">Exception filters – Implements the `IExceptionFilter` attribute.</span></span>

<span data-ttu-id="e1974-144">筛选器按上面列出的顺序执行。</span><span class="sxs-lookup"><span data-stu-id="e1974-144">Filters are executed in the order listed above.</span></span> <span data-ttu-id="e1974-145">例如，授权筛选器始终在操作筛选器和异常筛选器始终在每一种其他类型的筛选器之后执行。</span><span class="sxs-lookup"><span data-stu-id="e1974-145">For example, authorization filters are always executed before action filters and exception filters are always executed after every other type of filter.</span></span>

<span data-ttu-id="e1974-146">授权筛选器用于实现控制器操作的身份验证和授权。</span><span class="sxs-lookup"><span data-stu-id="e1974-146">Authorization filters are used to implement authentication and authorization for controller actions.</span></span> <span data-ttu-id="e1974-147">例如，"授权"筛选器是授权筛选器的示例。</span><span class="sxs-lookup"><span data-stu-id="e1974-147">For example, the Authorize filter is an example of an Authorization filter.</span></span>

<span data-ttu-id="e1974-148">操作筛选器包含在控制器操作执行之前和之后执行的逻辑。</span><span class="sxs-lookup"><span data-stu-id="e1974-148">Action filters contain logic that is executed before and after a controller action executes.</span></span> <span data-ttu-id="e1974-149">例如，可以使用操作筛选器修改控制器操作返回的视图数据。</span><span class="sxs-lookup"><span data-stu-id="e1974-149">You can use an action filter, for instance, to modify the view data that a controller action returns.</span></span>

<span data-ttu-id="e1974-150">结果筛选器包含在执行视图结果之前和之后执行的逻辑。</span><span class="sxs-lookup"><span data-stu-id="e1974-150">Result filters contain logic that is executed before and after a view result is executed.</span></span> <span data-ttu-id="e1974-151">例如，您可能希望在视图呈现给浏览器之前修改视图结果。</span><span class="sxs-lookup"><span data-stu-id="e1974-151">For example, you might want to modify a view result right before the view is rendered to the browser.</span></span>

<span data-ttu-id="e1974-152">异常筛选器是要运行的最后一种筛选器类型。</span><span class="sxs-lookup"><span data-stu-id="e1974-152">Exception filters are the last type of filter to run.</span></span> <span data-ttu-id="e1974-153">可以使用异常筛选器来处理控制器操作或控制器操作结果引发的错误。</span><span class="sxs-lookup"><span data-stu-id="e1974-153">You can use an exception filter to handle errors raised by either your controller actions or controller action results.</span></span> <span data-ttu-id="e1974-154">您还可以使用异常筛选器来记录错误。</span><span class="sxs-lookup"><span data-stu-id="e1974-154">You also can use exception filters to log errors.</span></span>

<span data-ttu-id="e1974-155">每种不同类型的筛选器都按特定顺序执行。</span><span class="sxs-lookup"><span data-stu-id="e1974-155">Each different type of filter is executed in a particular order.</span></span> <span data-ttu-id="e1974-156">如果要控制执行相同类型的筛选器的顺序，则可以设置筛选器的 Order 属性。</span><span class="sxs-lookup"><span data-stu-id="e1974-156">If you want to control the order in which filters of the same type are executed then you can set a filter's Order property.</span></span>

<span data-ttu-id="e1974-157">所有操作筛选器的基类是类`System.Web.Mvc.FilterAttribute`。</span><span class="sxs-lookup"><span data-stu-id="e1974-157">The base class for all action filters is the `System.Web.Mvc.FilterAttribute` class.</span></span> <span data-ttu-id="e1974-158">如果要实现特定类型的筛选器，则需要创建从基本筛选器类继承的类，并实现一个或多个 I授权筛选器、IActionFilter、IResultFilter 或例外筛选器接口。</span><span class="sxs-lookup"><span data-stu-id="e1974-158">If you want to implement a particular type of filter, then you need to create a class that inherits from the base Filter class and implements one or more of the IAuthorizationFilter, IActionFilter, IResultFilter, or ExceptionFilter interfaces.</span></span>

### <a name="the-base-actionfilterattribute-class"></a><span data-ttu-id="e1974-159">基本操作筛选器属性类</span><span class="sxs-lookup"><span data-stu-id="e1974-159">The Base ActionFilterAttribute Class</span></span>

<span data-ttu-id="e1974-160">为了更轻松地实现自定义操作筛选器，ASP.NET MVC 框架包括一`ActionFilterAttribute`个基本类。</span><span class="sxs-lookup"><span data-stu-id="e1974-160">In order to make it easier for you to implement a custom action filter, the ASP.NET MVC framework includes a base `ActionFilterAttribute` class.</span></span> <span data-ttu-id="e1974-161">此类实现 和`IActionFilter``IResultFilter`接口并从`Filter`类继承。</span><span class="sxs-lookup"><span data-stu-id="e1974-161">This class implements both the `IActionFilter` and `IResultFilter` interfaces and inherits from the `Filter` class.</span></span>

<span data-ttu-id="e1974-162">此处的术语并不完全一致。</span><span class="sxs-lookup"><span data-stu-id="e1974-162">The terminology here is not entirely consistent.</span></span> <span data-ttu-id="e1974-163">从技术上讲，从 ActionFilterAttribute 类继承的类既是操作筛选器，也是结果筛选器。</span><span class="sxs-lookup"><span data-stu-id="e1974-163">Technically, a class that inherits from the ActionFilterAttribute class is both an action filter and a result filter.</span></span> <span data-ttu-id="e1974-164">但是，在松散的意义上，单词操作筛选器用于引用 mVC 框架中的任何类型的筛选器ASP.NET。</span><span class="sxs-lookup"><span data-stu-id="e1974-164">However, in the loose sense, the word action filter is used to refer to any type of filter in the ASP.NET MVC framework.</span></span>

<span data-ttu-id="e1974-165">基本操作筛选器属性类具有您可以重写的以下方法：</span><span class="sxs-lookup"><span data-stu-id="e1974-165">The base ActionFilterAttribute class has the following methods that you can override:</span></span>

- <span data-ttu-id="e1974-166">OnAction 执行 – 在执行控制器操作之前调用此方法。</span><span class="sxs-lookup"><span data-stu-id="e1974-166">OnActionExecuting – This method is called before a controller action is executed.</span></span>
- <span data-ttu-id="e1974-167">执行执行时 - 在执行控制器操作后调用此方法。</span><span class="sxs-lookup"><span data-stu-id="e1974-167">OnActionExecuted – This method is called after a controller action is executed.</span></span>
- <span data-ttu-id="e1974-168">OnResult 执行 – 在执行控制器操作结果之前调用此方法。</span><span class="sxs-lookup"><span data-stu-id="e1974-168">OnResultExecuting – This method is called before a controller action result is executed.</span></span>
- <span data-ttu-id="e1974-169">OnResult 执行 - 在执行控制器操作结果后调用此方法。</span><span class="sxs-lookup"><span data-stu-id="e1974-169">OnResultExecuted – This method is called after a controller action result is executed.</span></span>

<span data-ttu-id="e1974-170">在下一节中，我们将了解如何实现每种不同方法。</span><span class="sxs-lookup"><span data-stu-id="e1974-170">In the next section, we'll see how you can implement each of these different methods.</span></span>

### <a name="creating-a-log-action-filter"></a><span data-ttu-id="e1974-171">创建日志操作筛选器</span><span class="sxs-lookup"><span data-stu-id="e1974-171">Creating a Log Action Filter</span></span>

<span data-ttu-id="e1974-172">为了说明如何构建自定义操作筛选器，我们将创建一个自定义操作筛选器，将处理控制器操作的各个阶段记录到 Visual Studio 输出窗口。</span><span class="sxs-lookup"><span data-stu-id="e1974-172">In order to illustrate how you can build a custom action filter, we'll create a custom action filter that logs the stages of processing a controller action to the Visual Studio Output window.</span></span> <span data-ttu-id="e1974-173">我们的`LogActionFilter`包含在清单2中。</span><span class="sxs-lookup"><span data-stu-id="e1974-173">Our `LogActionFilter` is contained in Listing 2.</span></span>

<span data-ttu-id="e1974-174">**清单2 |`ActionFilters\LogActionFilter.vb`**</span><span class="sxs-lookup"><span data-stu-id="e1974-174">**Listing 2 – `ActionFilters\LogActionFilter.vb`**</span></span>

[!code-vb[Main](understanding-action-filters-vb/samples/sample2.vb)]

<span data-ttu-id="e1974-175">在清单 2`OnActionExecuting()`中`OnActionExecuted()``OnResultExecuting()`，、、`OnResultExecuted()`和 方法都`Log()`调用 方法。</span><span class="sxs-lookup"><span data-stu-id="e1974-175">In Listing 2, the `OnActionExecuting()`, `OnActionExecuted()`, `OnResultExecuting()`, and `OnResultExecuted()` methods all call the `Log()` method.</span></span> <span data-ttu-id="e1974-176">方法的名称和当前路由数据将传递给 方法`Log()`。</span><span class="sxs-lookup"><span data-stu-id="e1974-176">The name of the method and the current route data is passed to the `Log()` method.</span></span> <span data-ttu-id="e1974-177">该方法`Log()`将消息写入可视化工作室输出窗口（参见图 2）。</span><span class="sxs-lookup"><span data-stu-id="e1974-177">The `Log()` method writes a message to the Visual Studio Output window (see Figure 2).</span></span>

<span data-ttu-id="e1974-178">[![写入可视化工作室输出窗口](understanding-action-filters-vb/_static/image5.png)](understanding-action-filters-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="e1974-178">[![Writing to the Visual Studio Output window](understanding-action-filters-vb/_static/image5.png)](understanding-action-filters-vb/_static/image4.png)</span></span>

<span data-ttu-id="e1974-179">**图 02**： 写入可视化工作室输出窗口 （[单击以查看全尺寸图像](understanding-action-filters-vb/_static/image6.png)）</span><span class="sxs-lookup"><span data-stu-id="e1974-179">**Figure 02**: Writing to the Visual Studio Output window ([Click to view full-size image](understanding-action-filters-vb/_static/image6.png))</span></span>

<span data-ttu-id="e1974-180">清单3中的主控制器说明了如何将 Log 操作筛选器应用于整个控制器类。</span><span class="sxs-lookup"><span data-stu-id="e1974-180">The Home controller in Listing 3 illustrates how you can apply the Log action filter to an entire controller class.</span></span> <span data-ttu-id="e1974-181">每当调用主控制器公开的任何操作（`Index()`方法或`About()`方法），处理操作的各个阶段都会记录到 Visual Studio 输出窗口。</span><span class="sxs-lookup"><span data-stu-id="e1974-181">Whenever any of the actions exposed by the Home controller are invoked – either the `Index()` method or the `About()` method – the stages of processing the action are logged to the Visual Studio Output window.</span></span>

<span data-ttu-id="e1974-182">**清单3 |`Controllers\HomeController.vb`**</span><span class="sxs-lookup"><span data-stu-id="e1974-182">**Listing 3 – `Controllers\HomeController.vb`**</span></span>

[!code-vb[Main](understanding-action-filters-vb/samples/sample3.vb)]

### <a name="summary"></a><span data-ttu-id="e1974-183">总结</span><span class="sxs-lookup"><span data-stu-id="e1974-183">Summary</span></span>

<span data-ttu-id="e1974-184">在本教程中，您将被介绍到ASP.NET MVC 操作筛选器。</span><span class="sxs-lookup"><span data-stu-id="e1974-184">In this tutorial, you were introduced to ASP.NET MVC action filters.</span></span> <span data-ttu-id="e1974-185">您了解了四种不同类型的筛选器：授权筛选器、操作筛选器、结果筛选器和异常筛选器。</span><span class="sxs-lookup"><span data-stu-id="e1974-185">You learned about the four different types of filters: authorization filters, action filters, result filters, and exception filters.</span></span> <span data-ttu-id="e1974-186">您还了解了基`ActionFilterAttribute`类。</span><span class="sxs-lookup"><span data-stu-id="e1974-186">You also learned about the base `ActionFilterAttribute` class.</span></span>

<span data-ttu-id="e1974-187">最后，您学习了如何实现简单的操作筛选器。</span><span class="sxs-lookup"><span data-stu-id="e1974-187">Finally, you learned how to implement a simple action filter.</span></span> <span data-ttu-id="e1974-188">我们创建了一个 Log 操作筛选器，将处理控制器操作的各个阶段记录到可视化工作室输出窗口。</span><span class="sxs-lookup"><span data-stu-id="e1974-188">We created a Log action filter that logs the stages of processing a controller action to the Visual Studio Output window.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="e1974-189">[上一页](asp-net-mvc-routing-overview-vb.md)
> [下一页](improving-performance-with-output-caching-vb.md)</span><span class="sxs-lookup"><span data-stu-id="e1974-189">[Previous](asp-net-mvc-routing-overview-vb.md)
[Next](improving-performance-with-output-caching-vb.md)</span></span>

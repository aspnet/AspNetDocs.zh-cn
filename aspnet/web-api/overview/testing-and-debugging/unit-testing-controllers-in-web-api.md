---
uid: web-api/overview/testing-and-debugging/unit-testing-controllers-in-web-api
title: ASP.NET Web API 2 中的单元测试控制器 |Microsoft Docs
author: MikeWasson
description: 本主题介绍了 Web API 2 中的单元测试控制器的一些特定技术。 阅读本主题之前，您可能需要阅读教程单元 .。。
ms.author: riande
ms.date: 06/11/2014
ms.assetid: 43a6cce7-a3ef-42aa-ad06-90d36d49f098
msc.legacyurl: /web-api/overview/testing-and-debugging/unit-testing-controllers-in-web-api
msc.type: authoredcontent
ms.openlocfilehash: 3b89009a375e766f1c5b439dfe3fffd43b4963b3
ms.sourcegitcommit: a4c3c7e04e5f53cf8cd334f036d324976b78d154
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2020
ms.locfileid: "84172921"
---
# <a name="unit-testing-controllers-in-aspnet-web-api-2"></a><span data-ttu-id="0ea45-104">ASP.NET Web API 2 中的单元测试控制器</span><span class="sxs-lookup"><span data-stu-id="0ea45-104">Unit Testing Controllers in ASP.NET Web API 2</span></span>

<span data-ttu-id="0ea45-105">作者： [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="0ea45-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="0ea45-106">本主题介绍了 Web API 2 中的单元测试控制器的一些特定技术。</span><span class="sxs-lookup"><span data-stu-id="0ea45-106">This topic describes some specific techniques for unit testing controllers in Web API 2.</span></span> <span data-ttu-id="0ea45-107">阅读本主题之前，您可能需要阅读教程[单元测试 ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md)，其中演示了如何将单元测试项目添加到您的解决方案中。</span><span class="sxs-lookup"><span data-stu-id="0ea45-107">Before reading this topic, you might want to read the tutorial [Unit Testing ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md), which shows how to add a unit-test project to your solution.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="0ea45-108">本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="0ea45-108">Software versions used in the tutorial</span></span>
>
> - [<span data-ttu-id="0ea45-109">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="0ea45-109">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
> - <span data-ttu-id="0ea45-110">Web API 2</span><span class="sxs-lookup"><span data-stu-id="0ea45-110">Web API 2</span></span>
> - <span data-ttu-id="0ea45-111">[Moq](https://github.com/Moq) 4.5.30</span><span class="sxs-lookup"><span data-stu-id="0ea45-111">[Moq](https://github.com/Moq) 4.5.30</span></span>

> [!NOTE]
> <span data-ttu-id="0ea45-112">我使用的是 Moq，但也适用于任何模拟框架。</span><span class="sxs-lookup"><span data-stu-id="0ea45-112">I used Moq, but the same idea applies to any mocking framework.</span></span> <span data-ttu-id="0ea45-113">Moq 4.5.30 （及更高版本）支持 Visual Studio 2017、Roslyn 和 .NET 4.5 及更高版本。</span><span class="sxs-lookup"><span data-stu-id="0ea45-113">Moq 4.5.30 (and later) supports Visual Studio 2017, Roslyn and .NET 4.5 and later versions.</span></span>

<span data-ttu-id="0ea45-114">单元测试中的一种常见模式是 "按操作 &quot; 断言" &quot; ：</span><span class="sxs-lookup"><span data-stu-id="0ea45-114">A common pattern in unit tests is &quot;arrange-act-assert&quot;:</span></span>

- <span data-ttu-id="0ea45-115">排列：为要运行的测试设置任何先决条件。</span><span class="sxs-lookup"><span data-stu-id="0ea45-115">Arrange: Set up any prerequisites for the test to run.</span></span>
- <span data-ttu-id="0ea45-116">Act：执行测试。</span><span class="sxs-lookup"><span data-stu-id="0ea45-116">Act: Perform the test.</span></span>
- <span data-ttu-id="0ea45-117">断言：验证测试是否成功。</span><span class="sxs-lookup"><span data-stu-id="0ea45-117">Assert: Verify that the test succeeded.</span></span>

<span data-ttu-id="0ea45-118">在 "排列" 步骤中，您将经常使用 mock 或存根对象。</span><span class="sxs-lookup"><span data-stu-id="0ea45-118">In the arrange step, you will often use mock or stub objects.</span></span> <span data-ttu-id="0ea45-119">这可最大程度地减少依赖项的数量，因此，测试重点在于测试一项内容。</span><span class="sxs-lookup"><span data-stu-id="0ea45-119">That minimizes the number of dependencies, so the test is focused on testing one thing.</span></span>

<span data-ttu-id="0ea45-120">下面是一些应在 Web API 控制器中进行单元测试的事项：</span><span class="sxs-lookup"><span data-stu-id="0ea45-120">Here are some things that you should unit test in your Web API controllers:</span></span>

- <span data-ttu-id="0ea45-121">操作返回正确类型的响应。</span><span class="sxs-lookup"><span data-stu-id="0ea45-121">The action returns the correct type of response.</span></span>
- <span data-ttu-id="0ea45-122">无效参数返回正确的错误响应。</span><span class="sxs-lookup"><span data-stu-id="0ea45-122">Invalid parameters return the correct error response.</span></span>
- <span data-ttu-id="0ea45-123">操作对存储库或服务层调用正确的方法。</span><span class="sxs-lookup"><span data-stu-id="0ea45-123">The action calls the correct method on the repository or service layer.</span></span>
- <span data-ttu-id="0ea45-124">如果响应包含域模型，请验证模型类型。</span><span class="sxs-lookup"><span data-stu-id="0ea45-124">If the response includes a domain model, verify the model type.</span></span>

<span data-ttu-id="0ea45-125">下面是一些要测试的一般内容，具体取决于控制器实现情况。</span><span class="sxs-lookup"><span data-stu-id="0ea45-125">These are some of the general things to test, but the specifics depend on your controller implementation.</span></span> <span data-ttu-id="0ea45-126">具体来说，无论控制器操作返回**HttpResponseMessage**还是**IHttpActionResult**，它都有很大的区别。</span><span class="sxs-lookup"><span data-stu-id="0ea45-126">In particular, it makes a big difference whether your controller actions return **HttpResponseMessage** or **IHttpActionResult**.</span></span> <span data-ttu-id="0ea45-127">有关这些结果类型的详细信息，请参阅[Web Api 2 中的操作结果](../getting-started-with-aspnet-web-api/action-results.md)。</span><span class="sxs-lookup"><span data-stu-id="0ea45-127">For more information about these result types, see [Action Results in Web Api 2](../getting-started-with-aspnet-web-api/action-results.md).</span></span>

## <a name="testing-actions-that-return-httpresponsemessage"></a><span data-ttu-id="0ea45-128">返回 HttpResponseMessage 的测试操作</span><span class="sxs-lookup"><span data-stu-id="0ea45-128">Testing Actions that Return HttpResponseMessage</span></span>

<span data-ttu-id="0ea45-129">下面是其操作返回**HttpResponseMessage**的控制器的示例。</span><span class="sxs-lookup"><span data-stu-id="0ea45-129">Here is an example of a controller whose actions return **HttpResponseMessage**.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample1.cs)]

<span data-ttu-id="0ea45-130">请注意，控制器使用依赖关系注入来注入 `IProductRepository` 。</span><span class="sxs-lookup"><span data-stu-id="0ea45-130">Notice the controller uses dependency injection to inject an `IProductRepository`.</span></span> <span data-ttu-id="0ea45-131">这会使控制器更具可测试性，因为你可以注入 mock 存储库。</span><span class="sxs-lookup"><span data-stu-id="0ea45-131">That makes the controller more testable, because you can inject a mock repository.</span></span> <span data-ttu-id="0ea45-132">下面的单元测试将验证方法是否将 `Get` 写入 `Product` 响应正文。</span><span class="sxs-lookup"><span data-stu-id="0ea45-132">The following unit test verifies that the `Get` method writes a `Product` to the response body.</span></span> <span data-ttu-id="0ea45-133">假设 `repository` 是模拟 `IProductRepository` 。</span><span class="sxs-lookup"><span data-stu-id="0ea45-133">Assume that `repository` is a mock `IProductRepository`.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample2.cs)]

<span data-ttu-id="0ea45-134">必须在控制器上设置**请求**和**配置**。</span><span class="sxs-lookup"><span data-stu-id="0ea45-134">It's important to set **Request** and **Configuration** on the controller.</span></span> <span data-ttu-id="0ea45-135">否则，测试将失败，并出现**system.argumentnullexception**或**InvalidOperationException**。</span><span class="sxs-lookup"><span data-stu-id="0ea45-135">Otherwise, the test will fail with an **ArgumentNullException** or **InvalidOperationException**.</span></span>

## <a name="testing-link-generation"></a><span data-ttu-id="0ea45-136">测试链接生成</span><span class="sxs-lookup"><span data-stu-id="0ea45-136">Testing Link Generation</span></span>

<span data-ttu-id="0ea45-137">`Post`方法调用**UrlHelper**以在响应中创建链接。</span><span class="sxs-lookup"><span data-stu-id="0ea45-137">The `Post` method calls **UrlHelper.Link** to create links in the response.</span></span> <span data-ttu-id="0ea45-138">这需要在单元测试中进行更多的设置：</span><span class="sxs-lookup"><span data-stu-id="0ea45-138">This requires a little more setup in the unit test:</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample3.cs)]

<span data-ttu-id="0ea45-139">**UrlHelper**类需要请求 URL 和路由数据，因此测试必须为这些值设置值。</span><span class="sxs-lookup"><span data-stu-id="0ea45-139">The **UrlHelper** class needs the request URL and route data, so the test has to set values for these.</span></span> <span data-ttu-id="0ea45-140">另一种方法是 mock 或存根**UrlHelper**。</span><span class="sxs-lookup"><span data-stu-id="0ea45-140">Another option is mock or stub **UrlHelper**.</span></span> <span data-ttu-id="0ea45-141">使用此方法时，请将[ApiController](https://msdn.microsoft.com/library/system.web.http.apicontroller.url.aspx)的默认值替换为返回固定值的 mock 或存根版本。</span><span class="sxs-lookup"><span data-stu-id="0ea45-141">With this approach, you replace the default value of [ApiController.Url](https://msdn.microsoft.com/library/system.web.http.apicontroller.url.aspx) with a mock or stub version that returns a fixed value.</span></span>

<span data-ttu-id="0ea45-142">让我们使用[Moq](https://github.com/Moq)框架重写测试。</span><span class="sxs-lookup"><span data-stu-id="0ea45-142">Let's rewrite the test using the [Moq](https://github.com/Moq) framework.</span></span> <span data-ttu-id="0ea45-143">`Moq`在测试项目中安装 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="0ea45-143">Install the `Moq` NuGet package in the test project.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample4.cs)]

<span data-ttu-id="0ea45-144">在此版本中，无需设置任何路由数据，因为模拟**UrlHelper**返回常量字符串。</span><span class="sxs-lookup"><span data-stu-id="0ea45-144">In this version, you don't need to set up any route data, because the mock **UrlHelper** returns a constant string.</span></span>

## <a name="testing-actions-that-return-ihttpactionresult"></a><span data-ttu-id="0ea45-145">返回 IHttpActionResult 的测试操作</span><span class="sxs-lookup"><span data-stu-id="0ea45-145">Testing Actions that Return IHttpActionResult</span></span>

<span data-ttu-id="0ea45-146">在 Web API 2 中，控制器操作可以返回**IHttpActionResult**，这类似于 ASP.NET MVC 中的**ActionResult** 。</span><span class="sxs-lookup"><span data-stu-id="0ea45-146">In Web API 2, a controller action can return **IHttpActionResult**, which is analogous to **ActionResult** in ASP.NET MVC.</span></span> <span data-ttu-id="0ea45-147">**IHttpActionResult**接口定义用于创建 HTTP 响应的命令模式。</span><span class="sxs-lookup"><span data-stu-id="0ea45-147">The **IHttpActionResult** interface defines a command pattern for creating HTTP responses.</span></span> <span data-ttu-id="0ea45-148">控制器返回**IHttpActionResult**，而不是直接创建响应。</span><span class="sxs-lookup"><span data-stu-id="0ea45-148">Instead of creating the response directly, the controller returns an **IHttpActionResult**.</span></span> <span data-ttu-id="0ea45-149">稍后，管道将调用**IHttpActionResult**来创建响应。</span><span class="sxs-lookup"><span data-stu-id="0ea45-149">Later, the pipeline invokes the **IHttpActionResult** to create the response.</span></span> <span data-ttu-id="0ea45-150">这种方法可以更轻松地编写单元测试，因为可以跳过**HttpResponseMessage**所需的大量设置。</span><span class="sxs-lookup"><span data-stu-id="0ea45-150">This approach makes it easier to write unit tests, because you can skip a lot of the setup that is needed for **HttpResponseMessage**.</span></span>

<span data-ttu-id="0ea45-151">下面是一个示例控制器，其操作返回**IHttpActionResult**。</span><span class="sxs-lookup"><span data-stu-id="0ea45-151">Here is an example controller whose actions return **IHttpActionResult**.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample5.cs)]

<span data-ttu-id="0ea45-152">此示例显示了使用**IHttpActionResult**的一些常用模式。</span><span class="sxs-lookup"><span data-stu-id="0ea45-152">This example shows some common patterns using **IHttpActionResult**.</span></span> <span data-ttu-id="0ea45-153">让我们看看如何对它们进行单元测试。</span><span class="sxs-lookup"><span data-stu-id="0ea45-153">Let's see how to unit test them.</span></span>

### <a name="action-returns-200-ok-with-a-response-body"></a><span data-ttu-id="0ea45-154">操作返回200（正常），其中包含响应正文</span><span class="sxs-lookup"><span data-stu-id="0ea45-154">Action returns 200 (OK) with a response body</span></span>

<span data-ttu-id="0ea45-155">`Get`如果找到该产品，则方法将调用 `Ok(product)` 。</span><span class="sxs-lookup"><span data-stu-id="0ea45-155">The `Get` method calls `Ok(product)` if the product is found.</span></span> <span data-ttu-id="0ea45-156">在单元测试中，确保返回类型为**OkNegotiatedContentResult** ，并且返回的产品具有正确的 ID。</span><span class="sxs-lookup"><span data-stu-id="0ea45-156">In the unit test, make sure the return type is **OkNegotiatedContentResult** and the returned product has the right ID.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample6.cs)]

<span data-ttu-id="0ea45-157">请注意，单元测试不执行操作结果。</span><span class="sxs-lookup"><span data-stu-id="0ea45-157">Notice that the unit test doesn't execute the action result.</span></span> <span data-ttu-id="0ea45-158">可以假设操作结果正确地创建 HTTP 响应。</span><span class="sxs-lookup"><span data-stu-id="0ea45-158">You can assume the action result creates the HTTP response correctly.</span></span> <span data-ttu-id="0ea45-159">（这就是 Web API 框架有自己的单元测试的原因！）</span><span class="sxs-lookup"><span data-stu-id="0ea45-159">(That's why the Web API framework has its own unit tests!)</span></span>

### <a name="action-returns-404-not-found"></a><span data-ttu-id="0ea45-160">操作返回404（未找到）</span><span class="sxs-lookup"><span data-stu-id="0ea45-160">Action returns 404 (Not Found)</span></span>

<span data-ttu-id="0ea45-161">`Get`如果找不到该产品，则方法将调用 `NotFound()` 。</span><span class="sxs-lookup"><span data-stu-id="0ea45-161">The `Get` method calls `NotFound()` if the product is not found.</span></span> <span data-ttu-id="0ea45-162">在这种情况下，单元测试仅检查返回类型是否为**NotFoundResult**。</span><span class="sxs-lookup"><span data-stu-id="0ea45-162">For this case, the unit test just checks if the return type is **NotFoundResult**.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample7.cs)]

### <a name="action-returns-200-ok-with-no-response-body"></a><span data-ttu-id="0ea45-163">操作返回200（正常），没有响应正文</span><span class="sxs-lookup"><span data-stu-id="0ea45-163">Action returns 200 (OK) with no response body</span></span>

<span data-ttu-id="0ea45-164">`Delete`方法调用 `Ok()` 来返回空的 HTTP 200 响应。</span><span class="sxs-lookup"><span data-stu-id="0ea45-164">The `Delete` method calls `Ok()` to return an empty HTTP 200 response.</span></span> <span data-ttu-id="0ea45-165">与前面的示例一样，单元测试检查返回类型，在本例中为**OkResult**。</span><span class="sxs-lookup"><span data-stu-id="0ea45-165">Like the previous example, the unit test checks the return type, in this case **OkResult**.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample8.cs)]

### <a name="action-returns-201-created-with-a-location-header"></a><span data-ttu-id="0ea45-166">操作返回带有 Location 标头的201（已创建）</span><span class="sxs-lookup"><span data-stu-id="0ea45-166">Action returns 201 (Created) with a Location header</span></span>

<span data-ttu-id="0ea45-167">`Post`方法调用 `CreatedAtRoute` 以返回带有 Location 标头中的 URI 的 HTTP 201 响应。</span><span class="sxs-lookup"><span data-stu-id="0ea45-167">The `Post` method calls `CreatedAtRoute` to return an HTTP 201 response with a URI in the Location header.</span></span> <span data-ttu-id="0ea45-168">在单元测试中，验证操作是否设置了正确的路由值。</span><span class="sxs-lookup"><span data-stu-id="0ea45-168">In the unit test, verify that the action sets the correct routing values.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample9.cs)]

### <a name="action-returns-another-2xx-with-a-response-body"></a><span data-ttu-id="0ea45-169">操作返回包含响应正文的另一个2xx</span><span class="sxs-lookup"><span data-stu-id="0ea45-169">Action returns another 2xx with a response body</span></span>

<span data-ttu-id="0ea45-170">`Put`方法调用 `Content` 以返回带有响应正文的 HTTP 202 （可接受）响应。</span><span class="sxs-lookup"><span data-stu-id="0ea45-170">The `Put` method calls `Content` to return an HTTP 202 (Accepted) response with a response body.</span></span> <span data-ttu-id="0ea45-171">这种情况类似于返回200（正常），但单元测试还应检查状态代码。</span><span class="sxs-lookup"><span data-stu-id="0ea45-171">This case is similar to returning 200 (OK), but the unit test should also check the status code.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample10.cs)]

## <a name="additional-resources"></a><span data-ttu-id="0ea45-172">其他资源</span><span class="sxs-lookup"><span data-stu-id="0ea45-172">Additional Resources</span></span>

- [<span data-ttu-id="0ea45-173">单元测试 ASP.NET Web API 2 时的模拟实体框架</span><span class="sxs-lookup"><span data-stu-id="0ea45-173">Mocking Entity Framework when Unit Testing ASP.NET Web API 2</span></span>](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md)
- <span data-ttu-id="0ea45-174">[为 ASP.NET Web API 服务编写测试](https://docs.microsoft.com/en-gb/archive/blogs/youssefm/writing-tests-for-an-asp-net-web-api-service)（Youssef Moussaoui 的博客文章）。</span><span class="sxs-lookup"><span data-stu-id="0ea45-174">[Writing tests for an ASP.NET Web API service](https://docs.microsoft.com/en-gb/archive/blogs/youssefm/writing-tests-for-an-asp-net-web-api-service) (blog post by Youssef Moussaoui).</span></span>
- [<span data-ttu-id="0ea45-175">Debugging ASP.NET Web API with Route Debugger（使用路由调试器调试 ASP.NET Web API）</span><span class="sxs-lookup"><span data-stu-id="0ea45-175">Debugging ASP.NET Web API with Route Debugger</span></span>](https://blogs.msdn.com/b/webdev/archive/2013/04/04/debugging-asp-net-web-api-with-route-debugger.aspx)

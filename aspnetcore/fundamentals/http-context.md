---
title: 在 ASP.NET Core 中访问 HttpContext
author: coderandhiker
description: 了解如何在 ASP.NET Core 中访问 HttpContext。
ms.author: riande
ms.custom: mvc
ms.date: 07/27/2018
uid: fundamentals/httpcontext
ms.openlocfilehash: 446882297524af3cbaed3ba7f941935debf5e7f4
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57026424"
---
# <a name="access-httpcontext-in-aspnet-core"></a><span data-ttu-id="770b3-103">在 ASP.NET Core 中访问 HttpContext</span><span class="sxs-lookup"><span data-stu-id="770b3-103">Access HttpContext in ASP.NET Core</span></span>

<span data-ttu-id="770b3-104">ASP.NET Core 应用通过 [IHttpContextAccessor](/dotnet/api/microsoft.aspnetcore.http.ihttpcontextaccessor) 接口及其默认实现 [HttpContextAccessor](/dotnet/api/microsoft.aspnetcore.http.httpcontextaccessor) 来访问 `HttpContext`。</span><span class="sxs-lookup"><span data-stu-id="770b3-104">ASP.NET Core apps access the `HttpContext` through the [IHttpContextAccessor](/dotnet/api/microsoft.aspnetcore.http.ihttpcontextaccessor) interface and its default implementation [HttpContextAccessor](/dotnet/api/microsoft.aspnetcore.http.httpcontextaccessor).</span></span> <span data-ttu-id="770b3-105">只有在需要访问服务内的 `HttpContext` 时，才有必要使用 `IHttpContextAccessor`。</span><span class="sxs-lookup"><span data-stu-id="770b3-105">It's only necessary to use `IHttpContextAccessor` when you need access to the `HttpContext` inside a service.</span></span>

::: moniker range=">= aspnetcore-2.0"

## <a name="use-httpcontext-from-razor-pages"></a><span data-ttu-id="770b3-106">通过 Razor Pages 使用 HttpContext</span><span class="sxs-lookup"><span data-stu-id="770b3-106">Use HttpContext from Razor Pages</span></span>

<span data-ttu-id="770b3-107">Razor Pages [PageModel](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.pagemodel) 公开 [HttpContext](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.pagemodel.httpcontext) 属性：</span><span class="sxs-lookup"><span data-stu-id="770b3-107">The Razor Pages [PageModel](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.pagemodel) exposes the [HttpContext](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.pagemodel.httpcontext) property:</span></span>

```csharp
public class AboutModel : PageModel
{
    public string Message { get; set; }

    public void OnGet()
    {
        Message = HttpContext.Request.PathBase;
    }
}
```

::: moniker-end

## <a name="use-httpcontext-from-a-razor-view"></a><span data-ttu-id="770b3-108">通过 Razor 视图使用 HttpContext</span><span class="sxs-lookup"><span data-stu-id="770b3-108">Use HttpContext from a Razor view</span></span>

<span data-ttu-id="770b3-109">Razor 视图通过视图上的 [RazorPage.Context](/dotnet/api/microsoft.aspnetcore.mvc.razor.razorpage.context#Microsoft_AspNetCore_Mvc_Razor_RazorPage_Context) 属性直接公开 `HttpContext`。</span><span class="sxs-lookup"><span data-stu-id="770b3-109">Razor views expose the `HttpContext` directly via a [RazorPage.Context](/dotnet/api/microsoft.aspnetcore.mvc.razor.razorpage.context#Microsoft_AspNetCore_Mvc_Razor_RazorPage_Context) property on the view.</span></span> <span data-ttu-id="770b3-110">下面的示例使用 Windows 身份验证检索 Intranet 应用中的当前用户名：</span><span class="sxs-lookup"><span data-stu-id="770b3-110">The following example retrieves the current username in an Intranet app using Windows Authentication:</span></span>

```cshtml
@{
    var username = Context.User.Identity.Name;
}
```

## <a name="use-httpcontext-from-a-controller"></a><span data-ttu-id="770b3-111">通过控制器使用 HttpContext</span><span class="sxs-lookup"><span data-stu-id="770b3-111">Use HttpContext from a controller</span></span>

<span data-ttu-id="770b3-112">控制器公开 [ControllerBase.HttpContext](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.httpcontext) 属性：</span><span class="sxs-lookup"><span data-stu-id="770b3-112">Controllers expose the [ControllerBase.HttpContext](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.httpcontext) property:</span></span>

```csharp
public class HomeController : Controller
{
    public IActionResult About()
    {
        var pathBase = HttpContext.Request.PathBase;
        // Do something with the PathBase.

        return View();
    }
}
```

## <a name="use-httpcontext-from-middleware"></a><span data-ttu-id="770b3-113">通过中间件使用 HttpContext</span><span class="sxs-lookup"><span data-stu-id="770b3-113">Use HttpContext from middleware</span></span>

<span data-ttu-id="770b3-114">使用自定义中间件组件时，`HttpContext` 传递到 `Invoke` 或 `InvokeAsync` 方法，在中间件配置后可供访问：</span><span class="sxs-lookup"><span data-stu-id="770b3-114">When working with custom middleware components, `HttpContext` is passed into the `Invoke` or `InvokeAsync` method and can be accessed when the middleware is configured:</span></span>

```csharp
public class MyCustomMiddleware
{
    public Task InvokeAsync(HttpContext context)
    {
        // Middleware initialization optionally using HttpContext
    }
}
```

## <a name="use-httpcontext-from-custom-components"></a><span data-ttu-id="770b3-115">通过自定义组件使用 HttpContext</span><span class="sxs-lookup"><span data-stu-id="770b3-115">Use HttpContext from custom components</span></span>

<span data-ttu-id="770b3-116">对于需要访问 `HttpContext` 的其他框架和自定义组件，建议使用内置的[依赖项注入](xref:fundamentals/dependency-injection)容器来注册依赖项。</span><span class="sxs-lookup"><span data-stu-id="770b3-116">For other framework and custom components that require access to `HttpContext`, the recommended approach is to register a dependency using the built-in [dependency injection](xref:fundamentals/dependency-injection) container.</span></span> <span data-ttu-id="770b3-117">依赖项注入容器向任意类提供 `IHttpContextAccessor`，以供类在自己的构造函数中将它声明为依赖项。</span><span class="sxs-lookup"><span data-stu-id="770b3-117">The dependency injection container supplies the `IHttpContextAccessor` to any classes that declare it as a dependency in their constructors.</span></span>

::: moniker range=">= aspnetcore-2.1"

```csharp
public void ConfigureServices(IServiceCollection services)
{
     services.AddMvc()
         .SetCompatibilityVersion(CompatibilityVersion.Version_2_1);
     services.AddHttpContextAccessor();
     services.AddTransient<IUserRepository, UserRepository>();
}
```

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

```csharp
public void ConfigureServices(IServiceCollection services)
{
     services.AddMvc();
     services.AddSingleton<IHttpContextAccessor, HttpContextAccessor>();
     services.AddTransient<IUserRepository, UserRepository>();
}
```

::: moniker-end

<span data-ttu-id="770b3-118">如下示例中：</span><span class="sxs-lookup"><span data-stu-id="770b3-118">In the following example:</span></span>

* <span data-ttu-id="770b3-119">`UserRepository` 声明自己对 `IHttpContextAccessor` 的依赖。</span><span class="sxs-lookup"><span data-stu-id="770b3-119">`UserRepository` declares its dependency on `IHttpContextAccessor`.</span></span>
* <span data-ttu-id="770b3-120">当依赖项注入容器解析依赖链并创建 `UserRepository` 实例时，就会注入依赖项。</span><span class="sxs-lookup"><span data-stu-id="770b3-120">The dependency is supplied when dependency injection resolves the dependency chain and creates an instance of `UserRepository`.</span></span>

```csharp
public class UserRepository : IUserRepository
{
    private readonly IHttpContextAccessor _httpContextAccessor;

    public UserRepository(IHttpContextAccessor httpContextAccessor)
    {
        _httpContextAccessor = httpContextAccessor;
    }

    public void LogCurrentUser()
    {
        var username = _httpContextAccessor.HttpContext.User.Identity.Name;
        service.LogAccessRequest(username);
    }
}
```

## <a name="httpcontext-access-from-a-background-thread"></a><span data-ttu-id="770b3-121">从后台线程访问 HttpContext</span><span class="sxs-lookup"><span data-stu-id="770b3-121">HttpContext access from a background thread</span></span>

<span data-ttu-id="770b3-122">`HttpContext` 不是线程安全。</span><span class="sxs-lookup"><span data-stu-id="770b3-122">`HttpContext` is not thread-safe.</span></span> <span data-ttu-id="770b3-123">在处理请求之外读取或写入 `HttpContext` 的属性可能会导致 `NullReferenceException`。</span><span class="sxs-lookup"><span data-stu-id="770b3-123">Reading or writing properties of the `HttpContext` outside of processing a request can result in a `NullReferenceException`.</span></span>

> [!NOTE]
> <span data-ttu-id="770b3-124">在处理请求之外使用 `HttpContext` 通常会导致 `NullReferenceException`。</span><span class="sxs-lookup"><span data-stu-id="770b3-124">Using `HttpContext` outside of processing a request often results in a `NullReferenceException`.</span></span> <span data-ttu-id="770b3-125">如果应用生成偶发的 `NullReferenceException`，请评审启动后台处理的部分代码，或者在请求完成后继续处理的部分代码。</span><span class="sxs-lookup"><span data-stu-id="770b3-125">If your app generates sporadic `NullReferenceException`s , review parts of the code that start background processing, or that continue processing after a request completes.</span></span> <span data-ttu-id="770b3-126">查找将控制器方法定义为 `async void` 的错误。</span><span class="sxs-lookup"><span data-stu-id="770b3-126">Look for a mistakes like defining a controller method as `async void`.</span></span>

<span data-ttu-id="770b3-127">要使用 `HttpContext` 数据安全地执行后台工作，请执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="770b3-127">To safely perform background work with `HttpContext` data:</span></span>

* <span data-ttu-id="770b3-128">在请求处理过程中复制所需的数据。</span><span class="sxs-lookup"><span data-stu-id="770b3-128">Copy the required data during request processing.</span></span>
* <span data-ttu-id="770b3-129">将复制的数据传递给后台任务。</span><span class="sxs-lookup"><span data-stu-id="770b3-129">Pass the copied data to a background task.</span></span>

<span data-ttu-id="770b3-130">要避免不安全代码，请勿将 `HttpContext` 传递给执行后台工作的方法，而是传递所需要的数据。</span><span class="sxs-lookup"><span data-stu-id="770b3-130">To avoid unsafe code, never pass the `HttpContext` into a method that does background work - pass the data you need instead.</span></span>

```csharp
public class EmailController
{
    public ActionResult SendEmail(string email)
    {
        var correlationId = HttpContext.Request.Headers["x-correlation-id"].ToString();

        // Starts sending an email, but doesn't wait for it to complete
        _ = SendEmailCore(correlationId);
        return View();
    }

    private async Task SendEmailCore(string correlationId)
    {
        // send the email
    }
}


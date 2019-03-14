---
title: 迁移 ClaimsPrincipal.Current
author: mjrousos
description: 了解如何摆脱 ClaimsPrincipal.Current 检索当前经过身份验证的用户的标识和 ASP.NET Core 中的声明。
ms.author: scaddie
ms.custom: mvc
ms.date: 05/04/2018
uid: migration/claimsprincipal-current
ms.openlocfilehash: 35c3389798041e141c45bf0a76fa9d7285212768
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57039274"
---
# <a name="migrate-from-claimsprincipalcurrent"></a><span data-ttu-id="cfa0a-103">迁移 ClaimsPrincipal.Current</span><span class="sxs-lookup"><span data-stu-id="cfa0a-103">Migrate from ClaimsPrincipal.Current</span></span>

<span data-ttu-id="cfa0a-104">在 ASP.NET 4.x 项目中，常见的做法是使用[ClaimsPrincipal.Current](/dotnet/api/system.security.claims.claimsprincipal.current)来检索当前身份验证的用户的标识和声明。</span><span class="sxs-lookup"><span data-stu-id="cfa0a-104">In ASP.NET 4.x projects, it was common to use [ClaimsPrincipal.Current](/dotnet/api/system.security.claims.claimsprincipal.current) to retrieve the current authenticated user's identity and claims.</span></span> <span data-ttu-id="cfa0a-105">在 ASP.NET Core 中，不能再设置此属性。</span><span class="sxs-lookup"><span data-stu-id="cfa0a-105">In ASP.NET Core, this property is no longer set.</span></span> <span data-ttu-id="cfa0a-106">取决于它的代码需要更新，以通过不同方式获取当前经过身份验证的用户的标识。</span><span class="sxs-lookup"><span data-stu-id="cfa0a-106">Code that was depending on it needs to be updated to get the current authenticated user's identity through a different means.</span></span>

## <a name="context-specific-data-instead-of-static-data"></a><span data-ttu-id="cfa0a-107">特定于上下文的数据，而不是静态数据</span><span class="sxs-lookup"><span data-stu-id="cfa0a-107">Context-specific data instead of static data</span></span>

<span data-ttu-id="cfa0a-108">使用 ASP.NET Core，这两者的值时`ClaimsPrincipal.Current`和`Thread.CurrentPrincipal`未设置。</span><span class="sxs-lookup"><span data-stu-id="cfa0a-108">When using ASP.NET Core, the values of both `ClaimsPrincipal.Current` and `Thread.CurrentPrincipal` aren't set.</span></span> <span data-ttu-id="cfa0a-109">这些属性都表示静态状态，通常避免 ASP.NET Core。</span><span class="sxs-lookup"><span data-stu-id="cfa0a-109">These properties both represent static state, which ASP.NET Core generally avoids.</span></span> <span data-ttu-id="cfa0a-110">相反，ASP.NET Core 体系结构是检索特定于上下文的服务集合 （如当前用户的标识） 的依赖关系 (使用其[依赖关系注入](xref:fundamentals/dependency-injection)(DI) 模型)。</span><span class="sxs-lookup"><span data-stu-id="cfa0a-110">Instead, ASP.NET Core's architecture is to retrieve dependencies (like the current user's identity) from context-specific service collections (using its [dependency injection](xref:fundamentals/dependency-injection) (DI) model).</span></span> <span data-ttu-id="cfa0a-111">此外，`Thread.CurrentPrincipal`是线程静态的因此它可能不会持续某些异步方案中的更改 (并`ClaimsPrincipal.Current`只需调用`Thread.CurrentPrincipal`默认情况下)。</span><span class="sxs-lookup"><span data-stu-id="cfa0a-111">What's more, `Thread.CurrentPrincipal` is thread static, so it may not persist changes in some asynchronous scenarios (and `ClaimsPrincipal.Current` just calls `Thread.CurrentPrincipal` by default).</span></span>

<span data-ttu-id="cfa0a-112">若要了解的问题线程类型的静态成员可能会导致在异步方案中，请考虑下面的代码段：</span><span class="sxs-lookup"><span data-stu-id="cfa0a-112">To understand the sorts of problems thread static members can lead to in asynchronous scenarios, consider the following code snippet:</span></span>

```csharp
// Create a ClaimsPrincipal and set Thread.CurrentPrincipal
var identity = new ClaimsIdentity();
identity.AddClaim(new Claim(ClaimTypes.Name, "User1"));
Thread.CurrentPrincipal = new ClaimsPrincipal(identity);

// Check the current user
Console.WriteLine($"Current user: {Thread.CurrentPrincipal?.Identity.Name}");

// For the method to complete asynchronously
await Task.Yield();

// Check the current user after
Console.WriteLine($"Current user: {Thread.CurrentPrincipal?.Identity.Name}");
```

<span data-ttu-id="cfa0a-113">前面的示例代码集`Thread.CurrentPrincipal`，并检查其值之前和之后等待的异步调用。</span><span class="sxs-lookup"><span data-stu-id="cfa0a-113">The preceding sample code sets `Thread.CurrentPrincipal` and checks its value before and after awaiting an asynchronous call.</span></span> <span data-ttu-id="cfa0a-114">`Thread.CurrentPrincipal` 特定于*线程*在其上设置，而且方法是可能会继续在另一个线程在等待后的执行。</span><span class="sxs-lookup"><span data-stu-id="cfa0a-114">`Thread.CurrentPrincipal` is specific to the *thread* on which it's set, and the method is likely to resume execution on a different thread after the await.</span></span> <span data-ttu-id="cfa0a-115">因此，`Thread.CurrentPrincipal`存在时将首先检查，但在调用后为 null `await Task.Yield()`。</span><span class="sxs-lookup"><span data-stu-id="cfa0a-115">Consequently, `Thread.CurrentPrincipal` is present when it's first checked but is null after the call to `await Task.Yield()`.</span></span>

<span data-ttu-id="cfa0a-116">从应用程序的 DI 服务集合获取当前用户的标识太多可测试性，因为可以轻松地注入测试的标识。</span><span class="sxs-lookup"><span data-stu-id="cfa0a-116">Getting the current user's identity from the app's DI service collection is more testable, too, since test identities can be easily injected.</span></span>

## <a name="retrieve-the-current-user-in-an-aspnet-core-app"></a><span data-ttu-id="cfa0a-117">检索当前用户在 ASP.NET Core 应用程序</span><span class="sxs-lookup"><span data-stu-id="cfa0a-117">Retrieve the current user in an ASP.NET Core app</span></span>

<span data-ttu-id="cfa0a-118">有几个选项用于检索当前经过身份验证的用户的`ClaimsPrincipal`中代替了 ASP.NET Core `ClaimsPrincipal.Current`:</span><span class="sxs-lookup"><span data-stu-id="cfa0a-118">There are several options for retrieving the current authenticated user's `ClaimsPrincipal` in ASP.NET Core in place of `ClaimsPrincipal.Current`:</span></span>

* <span data-ttu-id="cfa0a-119">**ControllerBase.User**。</span><span class="sxs-lookup"><span data-stu-id="cfa0a-119">**ControllerBase.User**.</span></span> <span data-ttu-id="cfa0a-120">MVC 控制器可以访问当前经过身份验证的用户使用其[用户](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.user)属性。</span><span class="sxs-lookup"><span data-stu-id="cfa0a-120">MVC controllers can access the current authenticated user with their [User](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.user) property.</span></span>
* <span data-ttu-id="cfa0a-121">**HttpContext.User**。</span><span class="sxs-lookup"><span data-stu-id="cfa0a-121">**HttpContext.User**.</span></span> <span data-ttu-id="cfa0a-122">有权访问当前组件`HttpContext`（中间件） 可以获取当前用户的`ClaimsPrincipal`从[HttpContext.User](/dotnet/api/microsoft.aspnetcore.http.httpcontext.user)。</span><span class="sxs-lookup"><span data-stu-id="cfa0a-122">Components with access to the current `HttpContext` (middleware, for example) can get the current user's `ClaimsPrincipal` from [HttpContext.User](/dotnet/api/microsoft.aspnetcore.http.httpcontext.user).</span></span>
* <span data-ttu-id="cfa0a-123">**从调用方传入**。</span><span class="sxs-lookup"><span data-stu-id="cfa0a-123">**Passed in from caller**.</span></span> <span data-ttu-id="cfa0a-124">而无需访问当前库`HttpContext`通常称为从控制器或中间件组件，并且能与当前用户的标识作为参数传递。</span><span class="sxs-lookup"><span data-stu-id="cfa0a-124">Libraries without access to the current `HttpContext` are often called from controllers or middleware components and can have the current user's identity passed as an argument.</span></span>
* <span data-ttu-id="cfa0a-125">**IHttpContextAccessor**。</span><span class="sxs-lookup"><span data-stu-id="cfa0a-125">**IHttpContextAccessor**.</span></span> <span data-ttu-id="cfa0a-126">正在迁移到 ASP.NET Core 项目可能太大，无法轻松地将当前用户的标识传递到所有必要的位置。</span><span class="sxs-lookup"><span data-stu-id="cfa0a-126">The project being migrated to ASP.NET Core may be too large to easily pass the current user's identity to all necessary locations.</span></span> <span data-ttu-id="cfa0a-127">在这种情况下， [IHttpContextAccessor](/dotnet/api/microsoft.aspnetcore.http.ihttpcontextaccessor)可用作一种解决方法。</span><span class="sxs-lookup"><span data-stu-id="cfa0a-127">In such cases, [IHttpContextAccessor](/dotnet/api/microsoft.aspnetcore.http.ihttpcontextaccessor) can be used as a workaround.</span></span> <span data-ttu-id="cfa0a-128">`IHttpContextAccessor` 能够访问当前`HttpContext`（如果存在）。</span><span class="sxs-lookup"><span data-stu-id="cfa0a-128">`IHttpContextAccessor` is able to access the current `HttpContext` (if one exists).</span></span> <span data-ttu-id="cfa0a-129">将获取尚未尚未更新可以使用 ASP.NET Core DI 驱动体系结构的代码中的当前用户的标识的短期解决方案：</span><span class="sxs-lookup"><span data-stu-id="cfa0a-129">A short-term solution to getting the current user's identity in code that hasn't yet been updated to work with ASP.NET Core's DI-driven architecture would be:</span></span>

  * <span data-ttu-id="cfa0a-130">请`IHttpContextAccessor`DI 容器通过调用中提供[AddHttpContextAccessor](https://github.com/aspnet/Hosting/issues/793)中`Startup.ConfigureServices`。</span><span class="sxs-lookup"><span data-stu-id="cfa0a-130">Make `IHttpContextAccessor` available in the DI container by calling [AddHttpContextAccessor](https://github.com/aspnet/Hosting/issues/793) in `Startup.ConfigureServices`.</span></span>
  * <span data-ttu-id="cfa0a-131">获取的实例`IHttpContextAccessor`在启动过程并将其存储在静态变量中。</span><span class="sxs-lookup"><span data-stu-id="cfa0a-131">Get an instance of `IHttpContextAccessor` during startup and store it in a static variable.</span></span> <span data-ttu-id="cfa0a-132">实例将提供对以前已从静态属性检索当前用户的代码。</span><span class="sxs-lookup"><span data-stu-id="cfa0a-132">The instance is made available to code that was previously retrieving the current user from a static property.</span></span>
  * <span data-ttu-id="cfa0a-133">检索当前用户的`ClaimsPrincipal`使用`HttpContextAccessor.HttpContext?.User`。</span><span class="sxs-lookup"><span data-stu-id="cfa0a-133">Retrieve the current user's `ClaimsPrincipal` using `HttpContextAccessor.HttpContext?.User`.</span></span> <span data-ttu-id="cfa0a-134">如果此代码使用的 HTTP 请求上下文之外`HttpContext`为 null。</span><span class="sxs-lookup"><span data-stu-id="cfa0a-134">If this code is used outside of the context of an HTTP request, the `HttpContext` is null.</span></span>

<span data-ttu-id="cfa0a-135">最后一个选项，请使用`IHttpContextAccessor`，行为是违背 ASP.NET Core 原则 （首选静态依赖项的插入依赖关系）。</span><span class="sxs-lookup"><span data-stu-id="cfa0a-135">The final option, using `IHttpContextAccessor`, is contrary to ASP.NET Core principles (preferring injected dependencies to static dependencies).</span></span> <span data-ttu-id="cfa0a-136">计划将最终删除依赖于静态`IHttpContextAccessor`帮助器。</span><span class="sxs-lookup"><span data-stu-id="cfa0a-136">Plan to eventually remove the dependency on the static `IHttpContextAccessor` helper.</span></span> <span data-ttu-id="cfa0a-137">不过，可以迁移之前使用的大型现有 ASP.NET 应用时它是一个有用的桥， `ClaimsPrincipal.Current`。</span><span class="sxs-lookup"><span data-stu-id="cfa0a-137">It can be a useful bridge, though, when migrating large existing ASP.NET apps that were previously using `ClaimsPrincipal.Current`.</span></span>

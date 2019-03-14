---
title: ASP.NET Core 中的应用启动
author: tdykstra
description: 了解 ASP.NET Core 中的 Startup 类如何配置服务和应用的请求管道。
monikerRange: '>= aspnetcore-2.1'
ms.author: tdykstra
ms.custom: mvc
ms.date: 01/17/2019
uid: fundamentals/startup
ms.openlocfilehash: cfd0a57d5d0b60862b017a170b6d5cbddf56f15a
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57025354"
---
# <a name="app-startup-in-aspnet-core"></a><span data-ttu-id="49e92-103">ASP.NET Core 中的应用启动</span><span class="sxs-lookup"><span data-stu-id="49e92-103">App startup in ASP.NET Core</span></span>

<span data-ttu-id="49e92-104">作者：[Tom Dykstra](https://github.com/tdykstra)、[Luke Latham](https://github.com/guardrex) 和 [Steve Smith](https://ardalis.com)</span><span class="sxs-lookup"><span data-stu-id="49e92-104">By [Tom Dykstra](https://github.com/tdykstra), [Luke Latham](https://github.com/guardrex), and [Steve Smith](https://ardalis.com)</span></span>

<span data-ttu-id="49e92-105">`Startup` 类配置服务和应用的请求管道。</span><span class="sxs-lookup"><span data-stu-id="49e92-105">The `Startup` class configures services and the app's request pipeline.</span></span>

## <a name="the-startup-class"></a><span data-ttu-id="49e92-106">Startup 类</span><span class="sxs-lookup"><span data-stu-id="49e92-106">The Startup class</span></span>

<span data-ttu-id="49e92-107">ASP.NET Core 应用使用 `Startup` 类，按照约定命名为 `Startup`。</span><span class="sxs-lookup"><span data-stu-id="49e92-107">ASP.NET Core apps use a `Startup` class, which is named `Startup` by convention.</span></span> <span data-ttu-id="49e92-108">`Startup` 类：</span><span class="sxs-lookup"><span data-stu-id="49e92-108">The `Startup` class:</span></span>

* <span data-ttu-id="49e92-109">可选择性地包括 <xref:Microsoft.AspNetCore.Hosting.StartupBase.ConfigureServices*> 方法以配置应用的服务。</span><span class="sxs-lookup"><span data-stu-id="49e92-109">Optionally includes a <xref:Microsoft.AspNetCore.Hosting.StartupBase.ConfigureServices*> method to configure the app's *services*.</span></span> <span data-ttu-id="49e92-110">服务是一个提供应用功能的可重用组件。</span><span class="sxs-lookup"><span data-stu-id="49e92-110">A service is a reusable component that provides app functionality.</span></span> <span data-ttu-id="49e92-111">在 `ConfigureServices` 中配置配置（也称为“注册”）并通过[依存关系注入 (DI)](xref:fundamentals/dependency-injection) 或 <xref:Microsoft.AspNetCore.Builder.IApplicationBuilder.ApplicationServices*> 在整个应用中使用。</span><span class="sxs-lookup"><span data-stu-id="49e92-111">Services are configured&mdash;also described as *registered*&mdash;in `ConfigureServices` and consumed across the app via [dependency injection (DI)](xref:fundamentals/dependency-injection) or <xref:Microsoft.AspNetCore.Builder.IApplicationBuilder.ApplicationServices*>.</span></span>
* <span data-ttu-id="49e92-112">包括 <xref:Microsoft.AspNetCore.Hosting.StartupBase.Configure*> 方法以创建应用的请求处理管道。</span><span class="sxs-lookup"><span data-stu-id="49e92-112">Includes a <xref:Microsoft.AspNetCore.Hosting.StartupBase.Configure*> method to create the app's request processing pipeline.</span></span>

<span data-ttu-id="49e92-113">当应用启动时，运行时调用 `ConfigureServices` 和 `Configure`：</span><span class="sxs-lookup"><span data-stu-id="49e92-113">`ConfigureServices` and `Configure` are called by the runtime when the app starts:</span></span>

[!code-csharp[](startup/sample_snapshot/Startup1.cs?highlight=4,10)]

<span data-ttu-id="49e92-114">在构建应用的[主机](xref:fundamentals/index#host)时，系统为应用指定 `Startup` 类。</span><span class="sxs-lookup"><span data-stu-id="49e92-114">The `Startup` class is specified to the app when the app's [host](xref:fundamentals/index#host) is built.</span></span> <span data-ttu-id="49e92-115">在 `Program` 类的主机生成器上调用 `Build` 时，将生成应用的主机。</span><span class="sxs-lookup"><span data-stu-id="49e92-115">The app's host is built when `Build` is called on the host builder in the `Program` class.</span></span> <span data-ttu-id="49e92-116">通常通过在主机生成器上调用 [WebHostBuilderExtensions.UseStartup\<TStartup>](xref:Microsoft.AspNetCore.Hosting.WebHostBuilderExtensions.UseStartup*) 方法来指定 `Startup` 类：</span><span class="sxs-lookup"><span data-stu-id="49e92-116">The `Startup` class is usually specified by calling the [WebHostBuilderExtensions.UseStartup\<TStartup>](xref:Microsoft.AspNetCore.Hosting.WebHostBuilderExtensions.UseStartup*) method on the host builder:</span></span>

[!code-csharp[](startup/sample_snapshot/Program3.cs?name=snippet_Program&highlight=10)]

<span data-ttu-id="49e92-117">主机提供 `Startup` 类构造函数可用的某些服务。</span><span class="sxs-lookup"><span data-stu-id="49e92-117">The host provides services that are available to the `Startup` class constructor.</span></span> <span data-ttu-id="49e92-118">应用通过 `ConfigureServices` 添加其他服务。</span><span class="sxs-lookup"><span data-stu-id="49e92-118">The app adds additional services via `ConfigureServices`.</span></span> <span data-ttu-id="49e92-119">然后，主机和应用服务都可以在 `Configure` 和整个应用中使用。</span><span class="sxs-lookup"><span data-stu-id="49e92-119">Both the host and app services are then available in `Configure` and throughout the app.</span></span>

<span data-ttu-id="49e92-120">在 `Startup` 类中[注入依赖关系](xref:fundamentals/dependency-injection)的常见用途为注入：</span><span class="sxs-lookup"><span data-stu-id="49e92-120">A common use of [dependency injection](xref:fundamentals/dependency-injection) into the `Startup` class is to inject:</span></span>

* <span data-ttu-id="49e92-121"><xref:Microsoft.AspNetCore.Hosting.IHostingEnvironment> 按环境配置服务。</span><span class="sxs-lookup"><span data-stu-id="49e92-121"><xref:Microsoft.AspNetCore.Hosting.IHostingEnvironment> to configure services by environment.</span></span>
* <span data-ttu-id="49e92-122"><xref:Microsoft.Extensions.Configuration.IConfigurationBuilder> 读取配置。</span><span class="sxs-lookup"><span data-stu-id="49e92-122"><xref:Microsoft.Extensions.Configuration.IConfigurationBuilder> to read configuration.</span></span>
* <span data-ttu-id="49e92-123"><xref:Microsoft.Extensions.Logging.ILoggerFactory> 在记录器中创建 `Startup.ConfigureServices`。</span><span class="sxs-lookup"><span data-stu-id="49e92-123"><xref:Microsoft.Extensions.Logging.ILoggerFactory> to create a logger in `Startup.ConfigureServices`.</span></span>

[!code-csharp[](startup/sample_snapshot/Startup2.cs?highlight=7-8)]

<span data-ttu-id="49e92-124">注入 `IHostingEnvironment` 的替代方法是使用基于约定的方法。</span><span class="sxs-lookup"><span data-stu-id="49e92-124">An alternative to injecting `IHostingEnvironment` is to use a conventions-based approach.</span></span> <span data-ttu-id="49e92-125">应用为不同的环境（例如，`StartupDevelopment`）单独定义 `Startup` 类时，相应的 `Startup` 类会在运行时被选中。</span><span class="sxs-lookup"><span data-stu-id="49e92-125">When the app defines separate `Startup` classes for different environments (for example, `StartupDevelopment`), the appropriate `Startup` class is selected at runtime.</span></span> <span data-ttu-id="49e92-126">优先考虑名称后缀与当前环境相匹配的类。</span><span class="sxs-lookup"><span data-stu-id="49e92-126">The class whose name suffix matches the current environment is prioritized.</span></span> <span data-ttu-id="49e92-127">如果应用在开发环境中运行并包含 `Startup` 类和 `StartupDevelopment` 类，则使用 `StartupDevelopment` 类。</span><span class="sxs-lookup"><span data-stu-id="49e92-127">If the app is run in the Development environment and includes both a `Startup` class and a `StartupDevelopment` class, the `StartupDevelopment` class is used.</span></span> <span data-ttu-id="49e92-128">有关详细信息，请参阅[使用多个环境](xref:fundamentals/environments#environment-based-startup-class-and-methods)。</span><span class="sxs-lookup"><span data-stu-id="49e92-128">For more information, see [Use multiple environments](xref:fundamentals/environments#environment-based-startup-class-and-methods).</span></span>

<span data-ttu-id="49e92-129">要详细了解有关主机的详细信息，请参阅[主机](xref:fundamentals/index#host)。</span><span class="sxs-lookup"><span data-stu-id="49e92-129">To learn more about the host, see [The host](xref:fundamentals/index#host).</span></span> <span data-ttu-id="49e92-130">有关在启动过程中处理错误的信息，请参阅[启动异常处理](xref:fundamentals/error-handling#startup-exception-handling)。</span><span class="sxs-lookup"><span data-stu-id="49e92-130">For information on handling errors during startup, see [Startup exception handling](xref:fundamentals/error-handling#startup-exception-handling).</span></span>

## <a name="the-configureservices-method"></a><span data-ttu-id="49e92-131">ConfigureServices 方法</span><span class="sxs-lookup"><span data-stu-id="49e92-131">The ConfigureServices method</span></span>

<span data-ttu-id="49e92-132"><xref:Microsoft.AspNetCore.Hosting.StartupBase.ConfigureServices*> 方法：</span><span class="sxs-lookup"><span data-stu-id="49e92-132">The <xref:Microsoft.AspNetCore.Hosting.StartupBase.ConfigureServices*> method is:</span></span>

* <span data-ttu-id="49e92-133">可选。</span><span class="sxs-lookup"><span data-stu-id="49e92-133">Optional.</span></span>
* <span data-ttu-id="49e92-134">在 `Configure` 方法配置应用服务之前，由主机调用。</span><span class="sxs-lookup"><span data-stu-id="49e92-134">Called by the host before the `Configure` method to configure the app's services.</span></span>
* <span data-ttu-id="49e92-135">其中按常规设置[配置选项](xref:fundamentals/configuration/index)。</span><span class="sxs-lookup"><span data-stu-id="49e92-135">Where [configuration options](xref:fundamentals/configuration/index) are set by convention.</span></span>

<span data-ttu-id="49e92-136">典型模式是调用所有 `Add{Service}` 方法，然后调用所有 `services.Configure{Service}` 方法。</span><span class="sxs-lookup"><span data-stu-id="49e92-136">The typical pattern is to call all the `Add{Service}` methods and then call all of the `services.Configure{Service}` methods.</span></span> <span data-ttu-id="49e92-137">有关示例，请参阅[配置标识服务](xref:security/authentication/identity#pw)。</span><span class="sxs-lookup"><span data-stu-id="49e92-137">For example, see [Configure Identity services](xref:security/authentication/identity#pw).</span></span>

<span data-ttu-id="49e92-138">主机可能会在调用 `Startup` 方法之前配置某些服务。</span><span class="sxs-lookup"><span data-stu-id="49e92-138">The host may configure some services before `Startup` methods are called.</span></span> <span data-ttu-id="49e92-139">有关详细信息，请参阅[主机](xref:fundamentals/index#host)。</span><span class="sxs-lookup"><span data-stu-id="49e92-139">For more information, see [The host](xref:fundamentals/index#host).</span></span>

<span data-ttu-id="49e92-140">对于需要大量设置的功能，<xref:Microsoft.Extensions.DependencyInjection.IServiceCollection> 上有 `Add{Service}` 扩展方法。</span><span class="sxs-lookup"><span data-stu-id="49e92-140">For features that require substantial setup, there are `Add{Service}` extension methods on <xref:Microsoft.Extensions.DependencyInjection.IServiceCollection>.</span></span> <span data-ttu-id="49e92-141">典型 ASP.NET Core 应用将为实体框架、标识和 MVC 注册服务：</span><span class="sxs-lookup"><span data-stu-id="49e92-141">A typical ASP.NET Core app registers services for Entity Framework, Identity, and MVC:</span></span>

[!code-csharp[](startup/sample_snapshot/Startup3.cs?highlight=4,7,11)]

<span data-ttu-id="49e92-142">将服务添加到服务容器，使其在应用和 `Configure` 方法中可用。</span><span class="sxs-lookup"><span data-stu-id="49e92-142">Adding services to the service container makes them available within the app and in the `Configure` method.</span></span> <span data-ttu-id="49e92-143">服务通过[依赖关系注入](xref:fundamentals/dependency-injection)或 <xref:Microsoft.AspNetCore.Builder.IApplicationBuilder.ApplicationServices*> 进行解析。</span><span class="sxs-lookup"><span data-stu-id="49e92-143">The services are resolved via [dependency injection](xref:fundamentals/dependency-injection) or from <xref:Microsoft.AspNetCore.Builder.IApplicationBuilder.ApplicationServices*>.</span></span>

## <a name="the-configure-method"></a><span data-ttu-id="49e92-144">Configure 方法</span><span class="sxs-lookup"><span data-stu-id="49e92-144">The Configure method</span></span>

<span data-ttu-id="49e92-145"><xref:Microsoft.AspNetCore.Hosting.StartupBase.Configure*> 方法用于指定应用响应 HTTP 请求的方式。</span><span class="sxs-lookup"><span data-stu-id="49e92-145">The <xref:Microsoft.AspNetCore.Hosting.StartupBase.Configure*> method is used to specify how the app responds to HTTP requests.</span></span> <span data-ttu-id="49e92-146">可通过将[中间件](xref:fundamentals/middleware/index)组件添加到 <xref:Microsoft.AspNetCore.Builder.IApplicationBuilder> 实例来配置请求管道。</span><span class="sxs-lookup"><span data-stu-id="49e92-146">The request pipeline is configured by adding [middleware](xref:fundamentals/middleware/index) components to an <xref:Microsoft.AspNetCore.Builder.IApplicationBuilder> instance.</span></span> <span data-ttu-id="49e92-147">`Configure` 方法可使用 `IApplicationBuilder`，但未在服务容器中注册。</span><span class="sxs-lookup"><span data-stu-id="49e92-147">`IApplicationBuilder` is available to the `Configure` method, but it isn't registered in the service container.</span></span> <span data-ttu-id="49e92-148">托管创建 `IApplicationBuilder` 并将其直接传递到 `Configure`。</span><span class="sxs-lookup"><span data-stu-id="49e92-148">Hosting creates an `IApplicationBuilder` and passes it directly to `Configure`.</span></span>

<span data-ttu-id="49e92-149">[ASP.NET Core 模板](/dotnet/core/tools/dotnet-new)配置的管道支持：</span><span class="sxs-lookup"><span data-stu-id="49e92-149">The [ASP.NET Core templates](/dotnet/core/tools/dotnet-new) configure the pipeline with support for:</span></span>

* [<span data-ttu-id="49e92-150">开发人员异常页</span><span class="sxs-lookup"><span data-stu-id="49e92-150">Developer exception page</span></span>](xref:fundamentals/error-handling#the-developer-exception-page)
* [<span data-ttu-id="49e92-151">异常处理程序</span><span class="sxs-lookup"><span data-stu-id="49e92-151">Exception handler</span></span>](xref:fundamentals/error-handling#configure-a-custom-exception-handling-page)
* [<span data-ttu-id="49e92-152">HTTP 严格传输安全性 (HSTS)</span><span class="sxs-lookup"><span data-stu-id="49e92-152">HTTP Strict Transport Security (HSTS)</span></span>](xref:security/enforcing-ssl#http-strict-transport-security-protocol-hsts)
* [<span data-ttu-id="49e92-153">HTTPS 重定向</span><span class="sxs-lookup"><span data-stu-id="49e92-153">HTTPS redirection</span></span>](xref:security/enforcing-ssl)
* [<span data-ttu-id="49e92-154">静态文件</span><span class="sxs-lookup"><span data-stu-id="49e92-154">Static files</span></span>](xref:fundamentals/static-files)
* [<span data-ttu-id="49e92-155">一般数据保护条例 (GDPR)</span><span class="sxs-lookup"><span data-stu-id="49e92-155">General Data Protection Regulation (GDPR)</span></span>](xref:security/gdpr)
* <span data-ttu-id="49e92-156">ASP.NET Core [MVC](xref:mvc/overview) 和 [Razor Pages](xref:razor-pages/index)</span><span class="sxs-lookup"><span data-stu-id="49e92-156">ASP.NET Core [MVC](xref:mvc/overview) and [Razor Pages](xref:razor-pages/index)</span></span>

[!code-csharp[](startup/sample_snapshot/Startup4.cs)]

<span data-ttu-id="49e92-157">每个 `Use` 扩展方法将一个或多个中间件组件添加到请求管道。</span><span class="sxs-lookup"><span data-stu-id="49e92-157">Each `Use` extension method adds one or more middleware components to the request pipeline.</span></span> <span data-ttu-id="49e92-158">例如，`UseMvc` 扩展方法将[路由中间件](xref:fundamentals/routing)添加到请求管道，并将 [MVC](xref:mvc/overview) 配置为默认处理程序。</span><span class="sxs-lookup"><span data-stu-id="49e92-158">For instance, the `UseMvc` extension method adds [Routing Middleware](xref:fundamentals/routing) to the request pipeline and configures [MVC](xref:mvc/overview) as the default handler.</span></span>

<span data-ttu-id="49e92-159">请求管道中的每个中间件组件负责调用管道中的下一个组件，或在适当情况下使链发生短路。</span><span class="sxs-lookup"><span data-stu-id="49e92-159">Each middleware component in the request pipeline is responsible for invoking the next component in the pipeline or short-circuiting the chain, if appropriate.</span></span> <span data-ttu-id="49e92-160">如果中间件链中未发生短路，则每个中间件都有第二次机会在将请求发送到客户端前处理该请求。</span><span class="sxs-lookup"><span data-stu-id="49e92-160">If short-circuiting doesn't occur along the middleware chain, each middleware has a second chance to process the request before it's sent to the client.</span></span>

<span data-ttu-id="49e92-161">其他服务（如 `IHostingEnvironment` 和 `ILoggerFactory`），也可以在 `Configure` 方法签名中指定。</span><span class="sxs-lookup"><span data-stu-id="49e92-161">Additional services, such as `IHostingEnvironment` and `ILoggerFactory`, may also be specified in the `Configure` method signature.</span></span> <span data-ttu-id="49e92-162">如果指定，其他服务如果可用，将被注入。</span><span class="sxs-lookup"><span data-stu-id="49e92-162">When specified, additional services are injected if they're available.</span></span>

<span data-ttu-id="49e92-163">有关如何使用 `IApplicationBuilder` 和中间件处理顺序的详细信息，请参阅 <xref:fundamentals/middleware/index>。</span><span class="sxs-lookup"><span data-stu-id="49e92-163">For more information on how to use `IApplicationBuilder` and the order of middleware processing, see <xref:fundamentals/middleware/index>.</span></span>

## <a name="convenience-methods"></a><span data-ttu-id="49e92-164">便利方法</span><span class="sxs-lookup"><span data-stu-id="49e92-164">Convenience methods</span></span>

<span data-ttu-id="49e92-165">若要配置服务和请求处理管道，而不使用 `Startup` 类，请在主机生成器上调用 `ConfigureServices` 和 `Configure` 便捷方法。</span><span class="sxs-lookup"><span data-stu-id="49e92-165">To configure services and the request processing pipeline without using a `Startup` class, call `ConfigureServices` and `Configure` convenience methods on the host builder.</span></span> <span data-ttu-id="49e92-166">多次调用 `ConfigureServices` 将追加到另一个。</span><span class="sxs-lookup"><span data-stu-id="49e92-166">Multiple calls to `ConfigureServices` append to one another.</span></span> <span data-ttu-id="49e92-167">如果存在多个 `Configure` 方法调用，则使用最后一个 `Configure` 调用。</span><span class="sxs-lookup"><span data-stu-id="49e92-167">If multiple `Configure` method calls exist, the last `Configure` call is used.</span></span>

[!code-csharp[](startup/sample_snapshot/Program1.cs?highlight=18,22)]

## <a name="extend-startup-with-startup-filters"></a><span data-ttu-id="49e92-168">使用 Startup 筛选器扩展 Startup</span><span class="sxs-lookup"><span data-stu-id="49e92-168">Extend Startup with startup filters</span></span>

<span data-ttu-id="49e92-169">在应用的 [Configure](#the-configure-method) 中间件管道的开头或末尾使用 <xref:Microsoft.AspNetCore.Hosting.IStartupFilter> 来配置中间件。</span><span class="sxs-lookup"><span data-stu-id="49e92-169">Use <xref:Microsoft.AspNetCore.Hosting.IStartupFilter> to configure middleware at the beginning or end of an app's [Configure](#the-configure-method) middleware pipeline.</span></span> <span data-ttu-id="49e92-170">`IStartupFilter` 有助于确保中间件在应用请求处理管道的开始或结束时由库添加的中间件之前或之后运行。</span><span class="sxs-lookup"><span data-stu-id="49e92-170">`IStartupFilter` is useful to ensure that a middleware runs before or after middleware added by libraries at the start or end of the app's request processing pipeline.</span></span>

<span data-ttu-id="49e92-171">`IStartupFilter` 实现单个方法（即 <xref:Microsoft.AspNetCore.Hosting.StartupBase.Configure*>），该方法接收并返回 `Action<IApplicationBuilder>`。</span><span class="sxs-lookup"><span data-stu-id="49e92-171">`IStartupFilter` implements a single method, <xref:Microsoft.AspNetCore.Hosting.StartupBase.Configure*>, which receives and returns an `Action<IApplicationBuilder>`.</span></span> <span data-ttu-id="49e92-172"><xref:Microsoft.AspNetCore.Builder.IApplicationBuilder> 定义用于配置应用请求管道的类。</span><span class="sxs-lookup"><span data-stu-id="49e92-172">An <xref:Microsoft.AspNetCore.Builder.IApplicationBuilder> defines a class to configure an app's request pipeline.</span></span> <span data-ttu-id="49e92-173">有关详细信息，请参阅[使用 IApplicationBuilder 创建中间件管道](xref:fundamentals/middleware/index#create-a-middleware-pipeline-with-iapplicationbuilder)。</span><span class="sxs-lookup"><span data-stu-id="49e92-173">For more information, see [Create a middleware pipeline with IApplicationBuilder](xref:fundamentals/middleware/index#create-a-middleware-pipeline-with-iapplicationbuilder).</span></span>

<span data-ttu-id="49e92-174">在请求管道中，每个 `IStartupFilter` 实现一个或多个中间件。</span><span class="sxs-lookup"><span data-stu-id="49e92-174">Each `IStartupFilter` implements one or more middlewares in the request pipeline.</span></span> <span data-ttu-id="49e92-175">筛选器按照添加到服务容器的顺序调用。</span><span class="sxs-lookup"><span data-stu-id="49e92-175">The filters are invoked in the order they were added to the service container.</span></span> <span data-ttu-id="49e92-176">筛选器可在将控件传递给下一个筛选器之前或之后添加中间件，从而附加到应用管道的开头或末尾。</span><span class="sxs-lookup"><span data-stu-id="49e92-176">Filters may add middleware before or after passing control to the next filter, thus they append to the beginning or end of the app pipeline.</span></span>

<span data-ttu-id="49e92-177">下面的示例演示如何使用 `IStartupFilter` 注册中间件。</span><span class="sxs-lookup"><span data-stu-id="49e92-177">The following example demonstrates how to register a middleware with `IStartupFilter`.</span></span>

<span data-ttu-id="49e92-178">`RequestSetOptionsMiddleware` 中间件从查询字符串参数中设置选项值：</span><span class="sxs-lookup"><span data-stu-id="49e92-178">The `RequestSetOptionsMiddleware` middleware sets an options value from a query string parameter:</span></span>

[!code-csharp[](startup/sample_snapshot/RequestSetOptionsMiddleware.cs?name=snippet1&highlight=21)]

<span data-ttu-id="49e92-179">在 `RequestSetOptionsStartupFilter` 类中配置 `RequestSetOptionsMiddleware`：</span><span class="sxs-lookup"><span data-stu-id="49e92-179">The `RequestSetOptionsMiddleware` is configured in the `RequestSetOptionsStartupFilter` class:</span></span>

[!code-csharp[](startup/sample_snapshot/RequestSetOptionsStartupFilter.cs?name=snippet1&highlight=7)]

<span data-ttu-id="49e92-180">`IStartupFilter` 在 <xref:Microsoft.AspNetCore.Hosting.StartupBase.ConfigureServices*> 的服务容器中注册，参数 `Startup` 从 `Startup` 类外部注册：</span><span class="sxs-lookup"><span data-stu-id="49e92-180">The `IStartupFilter` is registered in the service container in <xref:Microsoft.AspNetCore.Hosting.StartupBase.ConfigureServices*> and augments `Startup` from outside of the `Startup` class:</span></span>

[!code-csharp[](startup/sample_snapshot/Program2.cs?name=snippet1&highlight=4-5)]

<span data-ttu-id="49e92-181">当提供 `option` 的查询字符串参数时，中间件在 MVC 中间件呈现响应之前处理分配值：</span><span class="sxs-lookup"><span data-stu-id="49e92-181">When a query string parameter for `option` is provided, the middleware processes the value assignment before the MVC middleware renders the response:</span></span>

![浏览器窗口显示已呈现的索引页。](startup/_static/index.png)

<span data-ttu-id="49e92-184">中间件执行顺序由 `IStartupFilter` 注册顺序设置：</span><span class="sxs-lookup"><span data-stu-id="49e92-184">Middleware execution order is set by the order of `IStartupFilter` registrations:</span></span>

* <span data-ttu-id="49e92-185">多个 `IStartupFilter` 实现可能与相同的对象进行交互。</span><span class="sxs-lookup"><span data-stu-id="49e92-185">Multiple `IStartupFilter` implementations may interact with the same objects.</span></span> <span data-ttu-id="49e92-186">如果顺序很重要，请将它们的 `IStartupFilter` 服务注册进行排序，以匹配其中间件应有的运行顺序。</span><span class="sxs-lookup"><span data-stu-id="49e92-186">If ordering is important, order their `IStartupFilter` service registrations to match the order that their middlewares should run.</span></span>
* <span data-ttu-id="49e92-187">库可能添加包含一个或多个 `IStartupFilter` 实现的中间件，这些实现在向 `IStartupFilter` 注册的其他应用中间件之前或之后运行。</span><span class="sxs-lookup"><span data-stu-id="49e92-187">Libraries may add middleware with one or more `IStartupFilter` implementations that run before or after other app middleware registered with `IStartupFilter`.</span></span> <span data-ttu-id="49e92-188">若要在库的 `IStartupFilter` 添加中间件之前调用 `IStartupFilter` 中间件，请在将库添加到服务容器之前定位服务注册。</span><span class="sxs-lookup"><span data-stu-id="49e92-188">To invoke an `IStartupFilter` middleware before a middleware added by a library's `IStartupFilter`, position the service registration before the library is added to the service container.</span></span> <span data-ttu-id="49e92-189">若要在此后调用，请在添加库之后定位服务注册。</span><span class="sxs-lookup"><span data-stu-id="49e92-189">To invoke it afterward, position the service registration after the library is added.</span></span>

## <a name="add-configuration-at-startup-from-an-external-assembly"></a><span data-ttu-id="49e92-190">在启动时从外部程序集添加配置</span><span class="sxs-lookup"><span data-stu-id="49e92-190">Add configuration at startup from an external assembly</span></span>

<span data-ttu-id="49e92-191">通过 <xref:Microsoft.AspNetCore.Hosting.IHostingStartup> 实现，可在启动时从应用 `Startup` 类之外的外部程序集向应用添加增强功能。</span><span class="sxs-lookup"><span data-stu-id="49e92-191">An <xref:Microsoft.AspNetCore.Hosting.IHostingStartup> implementation allows adding enhancements to an app at startup from an external assembly outside of the app's `Startup` class.</span></span> <span data-ttu-id="49e92-192">有关详细信息，请参阅 <xref:fundamentals/configuration/platform-specific-configuration>。</span><span class="sxs-lookup"><span data-stu-id="49e92-192">For more information, see <xref:fundamentals/configuration/platform-specific-configuration>.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="49e92-193">其他资源</span><span class="sxs-lookup"><span data-stu-id="49e92-193">Additional resources</span></span>

* [<span data-ttu-id="49e92-194">主机</span><span class="sxs-lookup"><span data-stu-id="49e92-194">The host</span></span>](xref:fundamentals/index#host)
* <xref:fundamentals/environments>
* <xref:fundamentals/middleware/index>
* <xref:fundamentals/logging/index>
* <xref:fundamentals/configuration/index>

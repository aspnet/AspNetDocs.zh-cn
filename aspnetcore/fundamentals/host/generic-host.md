---
title: .NET 通用主机
author: guardrex
description: 了解有关 ASP.NET Core 泛型主机，该主机负责应用启动和生存期管理。
monikerRange: '>= aspnetcore-2.1'
ms.author: riande
ms.custom: mvc
ms.date: 11/28/2018
uid: fundamentals/host/generic-host
ms.openlocfilehash: a128b7c19d544d1dd28ab16f7a208ceef680ce81
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57048564"
---
# <a name="net-generic-host"></a><span data-ttu-id="b102b-103">.NET 通用主机</span><span class="sxs-lookup"><span data-stu-id="b102b-103">.NET Generic Host</span></span>

<span data-ttu-id="b102b-104">作者：[Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="b102b-104">By [Luke Latham](https://github.com/guardrex)</span></span>

::: moniker range="<= aspnetcore-2.2"

<span data-ttu-id="b102b-105">ASP.NET Core 应用配置和启动主机。</span><span class="sxs-lookup"><span data-stu-id="b102b-105">ASP.NET Core apps configure and launch a host.</span></span> <span data-ttu-id="b102b-106">主机负责应用程序启动和生存期管理。</span><span class="sxs-lookup"><span data-stu-id="b102b-106">The host is responsible for app startup and lifetime management.</span></span>

<span data-ttu-id="b102b-107">本文介绍 ASP.NET Core 泛型主机 (<xref:Microsoft.Extensions.Hosting.HostBuilder>)，该主机用于无法处理 HTTP 请求的应用。</span><span class="sxs-lookup"><span data-stu-id="b102b-107">This article covers the ASP.NET Core Generic Host (<xref:Microsoft.Extensions.Hosting.HostBuilder>), which is used for apps that don't process HTTP requests.</span></span>

<span data-ttu-id="b102b-108">泛型主机的用途是将 HTTP 管道从 Web 主机 API 中分离出来，从而启用更多的主机方案。</span><span class="sxs-lookup"><span data-stu-id="b102b-108">The purpose of Generic Host is to decouple the HTTP pipeline from the Web Host API to enable a wider array of host scenarios.</span></span> <span data-ttu-id="b102b-109">基于泛型主机的消息、后台任务和其他非 HTTP 工作负载可从横切功能（如配置、依赖关系注入 [DI] 和日志记录）中受益。</span><span class="sxs-lookup"><span data-stu-id="b102b-109">Messaging, background tasks, and other non-HTTP workloads based on Generic Host benefit from cross-cutting capabilities, such as configuration, dependency injection (DI), and logging.</span></span>

<span data-ttu-id="b102b-110">泛型主机是 ASP.NET Core 2.1 中的新增功能，不适用于 Web 承载方案。</span><span class="sxs-lookup"><span data-stu-id="b102b-110">Generic Host is new in ASP.NET Core 2.1 and isn't suitable for web hosting scenarios.</span></span> <span data-ttu-id="b102b-111">对于 Web 承载方案，请使用 [Web 主机](xref:fundamentals/host/web-host)。</span><span class="sxs-lookup"><span data-stu-id="b102b-111">For web hosting scenarios, use the [Web Host](xref:fundamentals/host/web-host).</span></span> <span data-ttu-id="b102b-112">泛型主机将在未来版本中替换 Web 主机，并在 HTTP 和非 HTTP 方案中充当主要的主机 API。</span><span class="sxs-lookup"><span data-stu-id="b102b-112">Generic Host will replace Web Host in a future release and act as the primary host API in both HTTP and non-HTTP scenarios.</span></span>

::: moniker-end

::: moniker range="> aspnetcore-2.2"

<span data-ttu-id="b102b-113">ASP.NET Core 应用配置和启动主机。</span><span class="sxs-lookup"><span data-stu-id="b102b-113">ASP.NET Core apps configure and launch a host.</span></span> <span data-ttu-id="b102b-114">主机负责应用程序启动和生存期管理。</span><span class="sxs-lookup"><span data-stu-id="b102b-114">The host is responsible for app startup and lifetime management.</span></span>

<span data-ttu-id="b102b-115">本文介绍 .NET Core 泛型主机 (<xref:Microsoft.Extensions.Hosting.HostBuilder>)。</span><span class="sxs-lookup"><span data-stu-id="b102b-115">This article covers the .NET Core Generic Host (<xref:Microsoft.Extensions.Hosting.HostBuilder>).</span></span>

<span data-ttu-id="b102b-116">泛型主机与 Web 主机的不同之处在于它将 HTTP 管道与 Web 主机 API 分离，以启用更广泛的主机方案。</span><span class="sxs-lookup"><span data-stu-id="b102b-116">Generic Host differs from Web Host in that it decouples the HTTP pipeline from the Web Host API to enable a wider array of host scenarios.</span></span> <span data-ttu-id="b102b-117">消息、后台任务和其他非 HTTP 工作负载可以使用泛型主机并从横切功能（如配置、依赖关系注入 [DI] 和日志记录）中受益。</span><span class="sxs-lookup"><span data-stu-id="b102b-117">Messaging, background tasks, and other non-HTTP workloads can use Generic Host and benefit from cross-cutting capabilities, such as configuration, dependency injection (DI), and logging.</span></span>

<span data-ttu-id="b102b-118">自 ASP.NET Core 3.0 起，建议为 HTTP 和非 HTTP 工作负载使用泛型主机。</span><span class="sxs-lookup"><span data-stu-id="b102b-118">Starting in ASP.NET Core 3.0, Generic Host is recommended for both HTTP and non-HTTP workloads.</span></span> <span data-ttu-id="b102b-119">HTTP 服务器实现（如果包括）作为 <xref:Microsoft.Extensions.Hosting.IHostedService> 的实现运行。</span><span class="sxs-lookup"><span data-stu-id="b102b-119">An HTTP server implementation, if included, runs as an implementation of <xref:Microsoft.Extensions.Hosting.IHostedService>.</span></span> <span data-ttu-id="b102b-120">`IHostedService` 是可用于其他工作负载的接口。</span><span class="sxs-lookup"><span data-stu-id="b102b-120">`IHostedService` is an interface that can be used for other workloads as well.</span></span>

<span data-ttu-id="b102b-121">对于 Web 应用，不再建议使用 Web 主机，但该主机仍可用于后向兼容性。</span><span class="sxs-lookup"><span data-stu-id="b102b-121">Web Host is no longer recommended for web apps but remains available for backward compatibility.</span></span>

> [!NOTE]
> <span data-ttu-id="b102b-122">本文的其余部分尚未针对 3.0 进行更新。</span><span class="sxs-lookup"><span data-stu-id="b102b-122">This remainder of this article has not yet been updated for 3.0.</span></span>

::: moniker-end

<span data-ttu-id="b102b-123">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/host/generic-host/samples/)（[如何下载](xref:index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="b102b-123">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/host/generic-host/samples/) ([how to download](xref:index#how-to-download-a-sample))</span></span>

<span data-ttu-id="b102b-124">在 [Visual Studio Code](https://code.visualstudio.com/) 中运行示例应用时，请使用外部或集成终端。</span><span class="sxs-lookup"><span data-stu-id="b102b-124">When running the sample app in [Visual Studio Code](https://code.visualstudio.com/), use an *external or integrated terminal*.</span></span> <span data-ttu-id="b102b-125">请勿在 `internalConsole` 中运行示例。</span><span class="sxs-lookup"><span data-stu-id="b102b-125">Don't run the sample in an `internalConsole`.</span></span>

<span data-ttu-id="b102b-126">在 Visual Studio Code 中设置控制台：</span><span class="sxs-lookup"><span data-stu-id="b102b-126">To set the console in Visual Studio Code:</span></span>

1. <span data-ttu-id="b102b-127">打开 .vscode/launch.json 文件。</span><span class="sxs-lookup"><span data-stu-id="b102b-127">Open the *.vscode/launch.json* file.</span></span>
1. <span data-ttu-id="b102b-128">在 .NET Core 启动（控制台）配置中，找到控制台条目。</span><span class="sxs-lookup"><span data-stu-id="b102b-128">In the **.NET Core Launch (console)** configuration, locate the **console** entry.</span></span> <span data-ttu-id="b102b-129">将值设置为 `externalTerminal` 或 `integratedTerminal`。</span><span class="sxs-lookup"><span data-stu-id="b102b-129">Set the value to either `externalTerminal` or `integratedTerminal`.</span></span>

## <a name="introduction"></a><span data-ttu-id="b102b-130">介绍</span><span class="sxs-lookup"><span data-stu-id="b102b-130">Introduction</span></span>

<span data-ttu-id="b102b-131">通用主机库位于 <xref:Microsoft.Extensions.Hosting> 命名空间中，由 [Microsoft.Extensions.Hosting](https://www.nuget.org/packages/Microsoft.Extensions.Hosting/) 包提供。</span><span class="sxs-lookup"><span data-stu-id="b102b-131">The Generic Host library is available in the <xref:Microsoft.Extensions.Hosting> namespace and provided by the [Microsoft.Extensions.Hosting](https://www.nuget.org/packages/Microsoft.Extensions.Hosting/) package.</span></span> <span data-ttu-id="b102b-132">[Microsoft.AspNetCore.App 元包](xref:fundamentals/metapackage-app)（ASP.NET Core 2.1 或更高版本）中包括 `Microsoft.Extensions.Hosting` 包。</span><span class="sxs-lookup"><span data-stu-id="b102b-132">The `Microsoft.Extensions.Hosting` package is included in the [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app) (ASP.NET Core 2.1 or later).</span></span>

<span data-ttu-id="b102b-133"><xref:Microsoft.Extensions.Hosting.IHostedService> 是执行代码的入口点。</span><span class="sxs-lookup"><span data-stu-id="b102b-133"><xref:Microsoft.Extensions.Hosting.IHostedService> is the entry point to code execution.</span></span> <span data-ttu-id="b102b-134">每个 `IHostedService` 实现都按照 [ConfigureServices 中服务注册](#configureservices)的顺序执行。</span><span class="sxs-lookup"><span data-stu-id="b102b-134">Each `IHostedService` implementation is executed in the order of [service registration in ConfigureServices](#configureservices).</span></span> <span data-ttu-id="b102b-135">主机启动时，每个 `IHostedService` 上都会调用 <xref:Microsoft.Extensions.Hosting.IHostedService.StartAsync*>，主机正常关闭时，以反向注册顺序调用 <xref:Microsoft.Extensions.Hosting.IHostedService.StopAsync*>。</span><span class="sxs-lookup"><span data-stu-id="b102b-135"><xref:Microsoft.Extensions.Hosting.IHostedService.StartAsync*> is called on each `IHostedService` when the host starts, and <xref:Microsoft.Extensions.Hosting.IHostedService.StopAsync*> is called in reverse registration order when the host shuts down gracefully.</span></span>

## <a name="set-up-a-host"></a><span data-ttu-id="b102b-136">设置主机</span><span class="sxs-lookup"><span data-stu-id="b102b-136">Set up a host</span></span>

<span data-ttu-id="b102b-137"><xref:Microsoft.Extensions.Hosting.IHostBuilder> 是供库和应用初始化、生成和运行主机的主要组件：</span><span class="sxs-lookup"><span data-stu-id="b102b-137"><xref:Microsoft.Extensions.Hosting.IHostBuilder> is the main component that libraries and apps use to initialize, build, and run the host:</span></span>

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/Program.cs?name=snippet_HostBuilder)]

## <a name="options"></a><span data-ttu-id="b102b-138">选项</span><span class="sxs-lookup"><span data-stu-id="b102b-138">Options</span></span>

<span data-ttu-id="b102b-139"><xref:Microsoft.Extensions.Hosting.HostOptions> 配置 <xref:Microsoft.Extensions.Hosting.IHost> 的选项。</span><span class="sxs-lookup"><span data-stu-id="b102b-139"><xref:Microsoft.Extensions.Hosting.HostOptions> configure options for the <xref:Microsoft.Extensions.Hosting.IHost>.</span></span>

### <a name="shutdown-timeout"></a><span data-ttu-id="b102b-140">关闭超时值</span><span class="sxs-lookup"><span data-stu-id="b102b-140">Shutdown timeout</span></span>

<span data-ttu-id="b102b-141"><xref:Microsoft.Extensions.Hosting.HostOptions.ShutdownTimeout*> 设置 <xref:Microsoft.Extensions.Hosting.IHost.StopAsync*> 的超时值。</span><span class="sxs-lookup"><span data-stu-id="b102b-141"><xref:Microsoft.Extensions.Hosting.HostOptions.ShutdownTimeout*> sets the timeout for <xref:Microsoft.Extensions.Hosting.IHost.StopAsync*>.</span></span> <span data-ttu-id="b102b-142">默认值为 5 秒。</span><span class="sxs-lookup"><span data-stu-id="b102b-142">The default value is five seconds.</span></span>

<span data-ttu-id="b102b-143">`Program.Main` 中的以下选项配置将默认值为 5 秒的关闭超时值增加至 20 秒：</span><span class="sxs-lookup"><span data-stu-id="b102b-143">The following option configuration in `Program.Main` increases the default five second shutdown timeout to 20 seconds:</span></span>

```csharp
var host = new HostBuilder()
    .ConfigureServices((hostContext, services) =>
    {
        services.Configure<HostOptions>(option =>
        {
            option.ShutdownTimeout = System.TimeSpan.FromSeconds(20);
        });
    })
    .Build();
```

## <a name="default-services"></a><span data-ttu-id="b102b-144">默认服务</span><span class="sxs-lookup"><span data-stu-id="b102b-144">Default services</span></span>

<span data-ttu-id="b102b-145">在主机初始化期间注册以下服务：</span><span class="sxs-lookup"><span data-stu-id="b102b-145">The following services are registered during host initialization:</span></span>

* <span data-ttu-id="b102b-146">[环境](xref:fundamentals/environments) (<xref:Microsoft.Extensions.Hosting.IHostingEnvironment>)</span><span class="sxs-lookup"><span data-stu-id="b102b-146">[Environment](xref:fundamentals/environments) (<xref:Microsoft.Extensions.Hosting.IHostingEnvironment>)</span></span>
* <xref:Microsoft.Extensions.Hosting.HostBuilderContext>
* <span data-ttu-id="b102b-147">[配置](xref:fundamentals/configuration/index) (<xref:Microsoft.Extensions.Configuration.IConfiguration>)</span><span class="sxs-lookup"><span data-stu-id="b102b-147">[Configuration](xref:fundamentals/configuration/index) (<xref:Microsoft.Extensions.Configuration.IConfiguration>)</span></span>
* <span data-ttu-id="b102b-148"><xref:Microsoft.Extensions.Hosting.IApplicationLifetime> (<xref:Microsoft.Extensions.Hosting.Internal.ApplicationLifetime>)</span><span class="sxs-lookup"><span data-stu-id="b102b-148"><xref:Microsoft.Extensions.Hosting.IApplicationLifetime> (<xref:Microsoft.Extensions.Hosting.Internal.ApplicationLifetime>)</span></span>
* <span data-ttu-id="b102b-149"><xref:Microsoft.Extensions.Hosting.IHostLifetime> (<xref:Microsoft.Extensions.Hosting.Internal.ConsoleLifetime>)</span><span class="sxs-lookup"><span data-stu-id="b102b-149"><xref:Microsoft.Extensions.Hosting.IHostLifetime> (<xref:Microsoft.Extensions.Hosting.Internal.ConsoleLifetime>)</span></span>
* <xref:Microsoft.Extensions.Hosting.IHost>
* <span data-ttu-id="b102b-150">[选项](xref:fundamentals/configuration/options) (<xref:Microsoft.Extensions.DependencyInjection.OptionsServiceCollectionExtensions.AddOptions*>)</span><span class="sxs-lookup"><span data-stu-id="b102b-150">[Options](xref:fundamentals/configuration/options) (<xref:Microsoft.Extensions.DependencyInjection.OptionsServiceCollectionExtensions.AddOptions*>)</span></span>
* <span data-ttu-id="b102b-151">[日志记录](xref:fundamentals/logging/index) (<xref:Microsoft.Extensions.DependencyInjection.LoggingServiceCollectionExtensions.AddLogging*>)</span><span class="sxs-lookup"><span data-stu-id="b102b-151">[Logging](xref:fundamentals/logging/index) (<xref:Microsoft.Extensions.DependencyInjection.LoggingServiceCollectionExtensions.AddLogging*>)</span></span>

## <a name="host-configuration"></a><span data-ttu-id="b102b-152">主机配置</span><span class="sxs-lookup"><span data-stu-id="b102b-152">Host configuration</span></span>

<span data-ttu-id="b102b-153">主机配置的创建方式如下：</span><span class="sxs-lookup"><span data-stu-id="b102b-153">Host configuration is created by:</span></span>

* <span data-ttu-id="b102b-154">调用 <xref:Microsoft.Extensions.Hosting.IHostBuilder> 上的扩展方法以设置[“内容根”](#content-root)和[“环境”](#environment)。</span><span class="sxs-lookup"><span data-stu-id="b102b-154">Calling extension methods on <xref:Microsoft.Extensions.Hosting.IHostBuilder> to set the [content root](#content-root) and [environment](#environment).</span></span>
* <span data-ttu-id="b102b-155">从 <xref:Microsoft.Extensions.Hosting.HostBuilder.ConfigureHostConfiguration*> 中的配置提供程序读取配置。</span><span class="sxs-lookup"><span data-stu-id="b102b-155">Reading configuration from configuration providers in <xref:Microsoft.Extensions.Hosting.HostBuilder.ConfigureHostConfiguration*>.</span></span>

### <a name="extension-methods"></a><span data-ttu-id="b102b-156">扩展方法</span><span class="sxs-lookup"><span data-stu-id="b102b-156">Extension methods</span></span>

### <a name="application-key-name"></a><span data-ttu-id="b102b-157">应用程序键（名称）</span><span class="sxs-lookup"><span data-stu-id="b102b-157">Application key (name)</span></span>

<span data-ttu-id="b102b-158">[IHostingEnvironment.ApplicationName](xref:Microsoft.Extensions.Hosting.IHostingEnvironment.ApplicationName*) 属性是在主机构造期间通过主机配置设定的。</span><span class="sxs-lookup"><span data-stu-id="b102b-158">The [IHostingEnvironment.ApplicationName](xref:Microsoft.Extensions.Hosting.IHostingEnvironment.ApplicationName*) property is set from host configuration during host construction.</span></span> <span data-ttu-id="b102b-159">要显式设置值，请使用 [HostDefaults.ApplicationKey](xref:Microsoft.Extensions.Hosting.HostDefaults.ApplicationKey)：</span><span class="sxs-lookup"><span data-stu-id="b102b-159">To set the value explicitly, use the [HostDefaults.ApplicationKey](xref:Microsoft.Extensions.Hosting.HostDefaults.ApplicationKey):</span></span>

<span data-ttu-id="b102b-160">**密钥**：applicationName</span><span class="sxs-lookup"><span data-stu-id="b102b-160">**Key**: applicationName</span></span>  
<span data-ttu-id="b102b-161">**类型**：string</span><span class="sxs-lookup"><span data-stu-id="b102b-161">**Type**: *string*</span></span>  
<span data-ttu-id="b102b-162">**默认值**：包含应用入口点的程序集的名称。</span><span class="sxs-lookup"><span data-stu-id="b102b-162">**Default**: The name of the assembly containing the app's entry point.</span></span>  
<span data-ttu-id="b102b-163">**设置使用**：`HostBuilderContext.HostingEnvironment.ApplicationName`</span><span class="sxs-lookup"><span data-stu-id="b102b-163">**Set using**: `HostBuilderContext.HostingEnvironment.ApplicationName`</span></span>  
<span data-ttu-id="b102b-164">**环境变量**：`<PREFIX_>APPLICATIONNAME`（`<PREFIX_>` 是[用户定义的可选前缀](#configurehostconfiguration)）</span><span class="sxs-lookup"><span data-stu-id="b102b-164">**Environment variable**: `<PREFIX_>APPLICATIONNAME` (`<PREFIX_>` is [optional and user-defined](#configurehostconfiguration))</span></span>

### <a name="content-root"></a><span data-ttu-id="b102b-165">内容根</span><span class="sxs-lookup"><span data-stu-id="b102b-165">Content root</span></span>

<span data-ttu-id="b102b-166">此设置确定主机从哪里开始搜索内容文件。</span><span class="sxs-lookup"><span data-stu-id="b102b-166">This setting determines where the host begins searching for content files.</span></span>

<span data-ttu-id="b102b-167">**键**：contentRoot</span><span class="sxs-lookup"><span data-stu-id="b102b-167">**Key**: contentRoot</span></span>  
<span data-ttu-id="b102b-168">**类型**：string</span><span class="sxs-lookup"><span data-stu-id="b102b-168">**Type**: *string*</span></span>  
<span data-ttu-id="b102b-169">**默认值**：默认为应用程序集所在的文件夹。</span><span class="sxs-lookup"><span data-stu-id="b102b-169">**Default**: Defaults to the folder where the app assembly resides.</span></span>  
<span data-ttu-id="b102b-170">**设置使用**：`UseContentRoot`</span><span class="sxs-lookup"><span data-stu-id="b102b-170">**Set using**: `UseContentRoot`</span></span>  
<span data-ttu-id="b102b-171">**环境变量**：`<PREFIX_>CONTENTROOT`（`<PREFIX_>` 是[用户定义的可选前缀](#configurehostconfiguration)）</span><span class="sxs-lookup"><span data-stu-id="b102b-171">**Environment variable**: `<PREFIX_>CONTENTROOT` (`<PREFIX_>` is [optional and user-defined](#configurehostconfiguration))</span></span>

<span data-ttu-id="b102b-172">如果路径不存在，主机将无法启动。</span><span class="sxs-lookup"><span data-stu-id="b102b-172">If the path doesn't exist, the host fails to start.</span></span>

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/Program.cs?name=snippet_UseContentRoot)]

### <a name="environment"></a><span data-ttu-id="b102b-173">环境</span><span class="sxs-lookup"><span data-stu-id="b102b-173">Environment</span></span>

<span data-ttu-id="b102b-174">设置应用的[环境](xref:fundamentals/environments)。</span><span class="sxs-lookup"><span data-stu-id="b102b-174">Sets the app's [environment](xref:fundamentals/environments).</span></span>

<span data-ttu-id="b102b-175">**键**：环境</span><span class="sxs-lookup"><span data-stu-id="b102b-175">**Key**: environment</span></span>  
<span data-ttu-id="b102b-176">**类型**：string</span><span class="sxs-lookup"><span data-stu-id="b102b-176">**Type**: *string*</span></span>  
<span data-ttu-id="b102b-177">**默认值**：生产</span><span class="sxs-lookup"><span data-stu-id="b102b-177">**Default**: Production</span></span>  
<span data-ttu-id="b102b-178">**设置使用**：`UseEnvironment`</span><span class="sxs-lookup"><span data-stu-id="b102b-178">**Set using**: `UseEnvironment`</span></span>  
<span data-ttu-id="b102b-179">**环境变量**：`<PREFIX_>ENVIRONMENT`（`<PREFIX_>` 是[用户定义的可选前缀](#configurehostconfiguration)）</span><span class="sxs-lookup"><span data-stu-id="b102b-179">**Environment variable**: `<PREFIX_>ENVIRONMENT` (`<PREFIX_>` is [optional and user-defined](#configurehostconfiguration))</span></span>

<span data-ttu-id="b102b-180">环境可以设置为任何值。</span><span class="sxs-lookup"><span data-stu-id="b102b-180">The environment can be set to any value.</span></span> <span data-ttu-id="b102b-181">框架定义的值包括 `Development``Staging` 和 `Production`。</span><span class="sxs-lookup"><span data-stu-id="b102b-181">Framework-defined values include `Development`, `Staging`, and `Production`.</span></span> <span data-ttu-id="b102b-182">值不区分大小写。</span><span class="sxs-lookup"><span data-stu-id="b102b-182">Values aren't case sensitive.</span></span>

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/Program.cs?name=snippet_UseEnvironment)]

### <a name="configurehostconfiguration"></a><span data-ttu-id="b102b-183">ConfigureHostConfiguration</span><span class="sxs-lookup"><span data-stu-id="b102b-183">ConfigureHostConfiguration</span></span>

<span data-ttu-id="b102b-184">`ConfigureHostConfiguration` 使用 <xref:Microsoft.Extensions.Configuration.IConfigurationBuilder> 来为主机创建 <xref:Microsoft.Extensions.Configuration.IConfiguration>。</span><span class="sxs-lookup"><span data-stu-id="b102b-184">`ConfigureHostConfiguration` uses an <xref:Microsoft.Extensions.Configuration.IConfigurationBuilder> to create an <xref:Microsoft.Extensions.Configuration.IConfiguration> for the host.</span></span> <span data-ttu-id="b102b-185">主机配置用于初始化 <xref:Microsoft.Extensions.Hosting.IHostingEnvironment>，以供在应用的构建过程中使用。</span><span class="sxs-lookup"><span data-stu-id="b102b-185">The host configuration is used to initialize the <xref:Microsoft.Extensions.Hosting.IHostingEnvironment> for use in the app's build process.</span></span>

<span data-ttu-id="b102b-186">可多次调用 `ConfigureHostConfiguration`，并得到累计结果。</span><span class="sxs-lookup"><span data-stu-id="b102b-186">`ConfigureHostConfiguration` can be called multiple times with additive results.</span></span> <span data-ttu-id="b102b-187">主机使用上一次在一个给定键上设置值的选项。</span><span class="sxs-lookup"><span data-stu-id="b102b-187">The host uses whichever option sets a value last on a given key.</span></span>

<span data-ttu-id="b102b-188">主机配置自动流向应用配置（[ConfigureAppConfiguration](#configureappconfiguration) 和应用的其余部分）。</span><span class="sxs-lookup"><span data-stu-id="b102b-188">Host configuration automatically flows to app configuration ([ConfigureAppConfiguration](#configureappconfiguration) and the rest of the app).</span></span>

<span data-ttu-id="b102b-189">默认情况下不包括提供程序。</span><span class="sxs-lookup"><span data-stu-id="b102b-189">No providers are included by default.</span></span> <span data-ttu-id="b102b-190">必须在 `ConfigureHostConfiguration` 中显式指定应用所需的任何配置提供程序，包括：</span><span class="sxs-lookup"><span data-stu-id="b102b-190">You must explicitly specify whatever configuration providers the app requires in `ConfigureHostConfiguration`, including:</span></span>

* <span data-ttu-id="b102b-191">文件配置（例如，来自 hostsettings.json 文件）。</span><span class="sxs-lookup"><span data-stu-id="b102b-191">File configuration (for example, from a *hostsettings.json* file).</span></span>
* <span data-ttu-id="b102b-192">环境变量配置。</span><span class="sxs-lookup"><span data-stu-id="b102b-192">Environment variable configuration.</span></span>
* <span data-ttu-id="b102b-193">命令行参数配置。</span><span class="sxs-lookup"><span data-stu-id="b102b-193">Command-line argument configuration.</span></span>
* <span data-ttu-id="b102b-194">任何其他所需的配置提供程序。</span><span class="sxs-lookup"><span data-stu-id="b102b-194">Any other required configuration providers.</span></span>

<span data-ttu-id="b102b-195">通过使用 `SetBasePath` 指定应用的基本路径，然后调用其中一个[文件配置提供程序](xref:fundamentals/configuration/index#file-configuration-provider)，可以启用主机的文件配置。</span><span class="sxs-lookup"><span data-stu-id="b102b-195">File configuration of the host is enabled by specifying the app's base path with `SetBasePath` followed by a call to one of the [file configuration providers](xref:fundamentals/configuration/index#file-configuration-provider).</span></span> <span data-ttu-id="b102b-196">示例应用使用 JSON 文件 hostsettings.json，并调用 <xref:Microsoft.Extensions.Configuration.JsonConfigurationExtensions.AddJsonFile*> 来使用文件的主机配置设置。</span><span class="sxs-lookup"><span data-stu-id="b102b-196">The sample app uses a JSON file, *hostsettings.json*, and calls <xref:Microsoft.Extensions.Configuration.JsonConfigurationExtensions.AddJsonFile*> to consume the file's host configuration settings.</span></span>

<span data-ttu-id="b102b-197">要添加主机的[环境变量配置](xref:fundamentals/configuration/index#environment-variables-configuration-provider)，请在主机生成器上调用 <xref:Microsoft.Extensions.Configuration.EnvironmentVariablesExtensions.AddEnvironmentVariables*>。</span><span class="sxs-lookup"><span data-stu-id="b102b-197">To add [environment variable configuration](xref:fundamentals/configuration/index#environment-variables-configuration-provider) of the host, call <xref:Microsoft.Extensions.Configuration.EnvironmentVariablesExtensions.AddEnvironmentVariables*> on the host builder.</span></span> <span data-ttu-id="b102b-198">`AddEnvironmentVariables` 接受用户定义的前缀（可选）。</span><span class="sxs-lookup"><span data-stu-id="b102b-198">`AddEnvironmentVariables` accepts an optional user-defined prefix.</span></span> <span data-ttu-id="b102b-199">示例应用使用前缀 `PREFIX_`。</span><span class="sxs-lookup"><span data-stu-id="b102b-199">The sample app uses a prefix of `PREFIX_`.</span></span> <span data-ttu-id="b102b-200">当系统读取环境变量时，便会删除前缀。</span><span class="sxs-lookup"><span data-stu-id="b102b-200">The prefix is removed when the environment variables are read.</span></span> <span data-ttu-id="b102b-201">配置示例应用的主机后，`PREFIX_ENVIRONMENT` 的环境变量值就变成 `environment` 密钥的主机配置值。</span><span class="sxs-lookup"><span data-stu-id="b102b-201">When the sample app's host is configured, the environment variable value for `PREFIX_ENVIRONMENT` becomes the host configuration value for the `environment` key.</span></span>

<span data-ttu-id="b102b-202">在开发过程中，如果使用 [Visual Studio](https://www.visualstudio.com/) 或通过 `dotnet run` 运行应用，可能会在 Properties/launchSettings.json 文件中设置环境变量。</span><span class="sxs-lookup"><span data-stu-id="b102b-202">During development when using [Visual Studio](https://www.visualstudio.com/) or running an app with `dotnet run`, environment variables may be set in the *Properties/launchSettings.json* file.</span></span> <span data-ttu-id="b102b-203">若在开发过程中使用 [Visual Studio Code](https://code.visualstudio.com/)，可能会在 .vscode/launch.json 文件中设置环境变量。</span><span class="sxs-lookup"><span data-stu-id="b102b-203">In [Visual Studio Code](https://code.visualstudio.com/), environment variables may be set in the *.vscode/launch.json* file during development.</span></span> <span data-ttu-id="b102b-204">有关详细信息，请参阅 <xref:fundamentals/environments>。</span><span class="sxs-lookup"><span data-stu-id="b102b-204">For more information, see <xref:fundamentals/environments>.</span></span>

<span data-ttu-id="b102b-205">通过调用 <xref:Microsoft.Extensions.Configuration.CommandLineConfigurationExtensions.AddCommandLine*> 可添加[命令行配置](xref:fundamentals/configuration/index#command-line-configuration-provider)。</span><span class="sxs-lookup"><span data-stu-id="b102b-205">[Command-line configuration](xref:fundamentals/configuration/index#command-line-configuration-provider) is added by calling <xref:Microsoft.Extensions.Configuration.CommandLineConfigurationExtensions.AddCommandLine*>.</span></span> <span data-ttu-id="b102b-206">最后添加命令行配置以允许命令行参数替代之前配置提供程序提供的配置。</span><span class="sxs-lookup"><span data-stu-id="b102b-206">Command-line configuration is added last to permit command-line arguments to override configuration provided by the earlier configuration providers.</span></span>

<span data-ttu-id="b102b-207">hostsettings.json：</span><span class="sxs-lookup"><span data-stu-id="b102b-207">*hostsettings.json*:</span></span>

[!code-csharp[](generic-host/samples/2.x/GenericHostSample/hostsettings.json)]

<span data-ttu-id="b102b-208">可以通过 [applicationName](#application-key-name) 和 [contentRoot](#content-root) 键提供其他配置。</span><span class="sxs-lookup"><span data-stu-id="b102b-208">Additional configuration can be provided with the [applicationName](#application-key-name) and [contentRoot](#content-root) keys.</span></span>

<span data-ttu-id="b102b-209">示例 `HostBuilder` 配置使用 `ConfigureHostConfiguration`：</span><span class="sxs-lookup"><span data-stu-id="b102b-209">Example `HostBuilder` configuration using `ConfigureHostConfiguration`:</span></span>

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/Program.cs?name=snippet_ConfigureHostConfiguration)]

## <a name="configureappconfiguration"></a><span data-ttu-id="b102b-210">ConfigureAppConfiguration</span><span class="sxs-lookup"><span data-stu-id="b102b-210">ConfigureAppConfiguration</span></span>

<span data-ttu-id="b102b-211">通过在 <xref:Microsoft.Extensions.Hosting.IHostBuilder> 实现上调用 <xref:Microsoft.Extensions.Hosting.HostBuilder.ConfigureAppConfiguration*> 创建应用配置。</span><span class="sxs-lookup"><span data-stu-id="b102b-211">App configuration is created by calling <xref:Microsoft.Extensions.Hosting.HostBuilder.ConfigureAppConfiguration*> on the <xref:Microsoft.Extensions.Hosting.IHostBuilder> implementation.</span></span> <span data-ttu-id="b102b-212">`ConfigureAppConfiguration` 使用 <xref:Microsoft.Extensions.Configuration.IConfigurationBuilder> 来为应用创建 <xref:Microsoft.Extensions.Configuration.IConfiguration>。</span><span class="sxs-lookup"><span data-stu-id="b102b-212">`ConfigureAppConfiguration` uses an <xref:Microsoft.Extensions.Configuration.IConfigurationBuilder> to create an <xref:Microsoft.Extensions.Configuration.IConfiguration> for the app.</span></span> <span data-ttu-id="b102b-213">可多次调用 `ConfigureAppConfiguration`，并得到累计结果。</span><span class="sxs-lookup"><span data-stu-id="b102b-213">`ConfigureAppConfiguration` can be called multiple times with additive results.</span></span> <span data-ttu-id="b102b-214">应用使用上一次在一个给定键上设置值的选项。</span><span class="sxs-lookup"><span data-stu-id="b102b-214">The app uses whichever option sets a value last on a given key.</span></span> <span data-ttu-id="b102b-215">[HostBuilderContext.Configuration](xref:Microsoft.Extensions.Hosting.HostBuilderContext.Configuration*) 中提供 `ConfigureAppConfiguration` 创建的配置，以供进行后续操作和在 <xref:Microsoft.Extensions.Hosting.IHost.Services*> 中使用。</span><span class="sxs-lookup"><span data-stu-id="b102b-215">The configuration created by `ConfigureAppConfiguration` is available at [HostBuilderContext.Configuration](xref:Microsoft.Extensions.Hosting.HostBuilderContext.Configuration*) for subsequent operations and in <xref:Microsoft.Extensions.Hosting.IHost.Services*>.</span></span>

<span data-ttu-id="b102b-216">应用配置会自动接收 [ConfigureHostConfiguration](#configurehostconfiguration) 提供的主机配置。</span><span class="sxs-lookup"><span data-stu-id="b102b-216">App configuration automatically receives host configuration provided by [ConfigureHostConfiguration](#configurehostconfiguration).</span></span>

<span data-ttu-id="b102b-217">示例应用配置使用 `ConfigureAppConfiguration`：</span><span class="sxs-lookup"><span data-stu-id="b102b-217">Example app configuration using `ConfigureAppConfiguration`:</span></span>

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/Program.cs?name=snippet_ConfigureAppConfiguration)]

<span data-ttu-id="b102b-218">appsettings.json：</span><span class="sxs-lookup"><span data-stu-id="b102b-218">*appsettings.json*:</span></span>

[!code-csharp[](generic-host/samples/2.x/GenericHostSample/appsettings.json)]

<span data-ttu-id="b102b-219">appsettings.Development.json：</span><span class="sxs-lookup"><span data-stu-id="b102b-219">*appsettings.Development.json*:</span></span>

[!code-csharp[](generic-host/samples/2.x/GenericHostSample/appsettings.Development.json)]

<span data-ttu-id="b102b-220">appsettings.Production.json：</span><span class="sxs-lookup"><span data-stu-id="b102b-220">*appsettings.Production.json*:</span></span>

[!code-csharp[](generic-host/samples/2.x/GenericHostSample/appsettings.Production.json)]

<span data-ttu-id="b102b-221">要将设置文件移动到输出目录，请在项目文件中将设置文件指定为 [MSBuild 项目项](/visualstudio/msbuild/common-msbuild-project-items)。</span><span class="sxs-lookup"><span data-stu-id="b102b-221">To move settings files to the output directory, specify the settings files as [MSBuild project items](/visualstudio/msbuild/common-msbuild-project-items) in the project file.</span></span> <span data-ttu-id="b102b-222">示例应用移动具有以下 `<Content>` 项的 JSON 应用设置文件和 hostsettings.json：</span><span class="sxs-lookup"><span data-stu-id="b102b-222">The sample app moves its JSON app settings files and *hostsettings.json* with the following `<Content>` item:</span></span>

```xml
<ItemGroup>
  <Content Include="**\*.json" Exclude="bin\**\*;obj\**\*" CopyToOutputDirectory="PreserveNewest" />
</ItemGroup>
```

## <a name="configureservices"></a><span data-ttu-id="b102b-223">ConfigureServices</span><span class="sxs-lookup"><span data-stu-id="b102b-223">ConfigureServices</span></span>

<span data-ttu-id="b102b-224"><xref:Microsoft.Extensions.Hosting.HostingHostBuilderExtensions.ConfigureServices*> 将服务添加到应用的[依赖关系](xref:fundamentals/dependency-injection)注入容器。</span><span class="sxs-lookup"><span data-stu-id="b102b-224"><xref:Microsoft.Extensions.Hosting.HostingHostBuilderExtensions.ConfigureServices*> adds services to the app's [dependency injection](xref:fundamentals/dependency-injection) container.</span></span> <span data-ttu-id="b102b-225">可多次调用 `ConfigureServices`，并得到累计结果。</span><span class="sxs-lookup"><span data-stu-id="b102b-225">`ConfigureServices` can be called multiple times with additive results.</span></span>

<span data-ttu-id="b102b-226">托管服务是一个类，具有实现 <xref:Microsoft.Extensions.Hosting.IHostedService> 接口的后台任务逻辑。</span><span class="sxs-lookup"><span data-stu-id="b102b-226">A hosted service is a class with background task logic that implements the <xref:Microsoft.Extensions.Hosting.IHostedService> interface.</span></span> <span data-ttu-id="b102b-227">有关详细信息，请参阅 <xref:fundamentals/host/hosted-services>。</span><span class="sxs-lookup"><span data-stu-id="b102b-227">For more information, see <xref:fundamentals/host/hosted-services>.</span></span>

<span data-ttu-id="b102b-228">[示例应用](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/host/generic-host/samples/)使用 `AddHostedService` 扩展方法向应用添加生存期事件 `LifetimeEventsHostedService` 和定时后台任务 `TimedHostedService` 服务：</span><span class="sxs-lookup"><span data-stu-id="b102b-228">The [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/host/generic-host/samples/) uses the `AddHostedService` extension method to add a service for lifetime events, `LifetimeEventsHostedService`, and a timed background task, `TimedHostedService`, to the app:</span></span>

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/Program.cs?name=snippet_ConfigureServices)]

## <a name="configurelogging"></a><span data-ttu-id="b102b-229">ConfigureLogging</span><span class="sxs-lookup"><span data-stu-id="b102b-229">ConfigureLogging</span></span>

<span data-ttu-id="b102b-230"><xref:Microsoft.Extensions.Hosting.HostingHostBuilderExtensions.ConfigureLogging*> 添加了一个委托来配置提供的 <xref:Microsoft.Extensions.Logging.ILoggingBuilder>。</span><span class="sxs-lookup"><span data-stu-id="b102b-230"><xref:Microsoft.Extensions.Hosting.HostingHostBuilderExtensions.ConfigureLogging*> adds a delegate for configuring the provided <xref:Microsoft.Extensions.Logging.ILoggingBuilder>.</span></span> <span data-ttu-id="b102b-231">可以利用相加结果多次调用 `ConfigureLogging`。</span><span class="sxs-lookup"><span data-stu-id="b102b-231">`ConfigureLogging` may be called multiple times with additive results.</span></span>

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/Program.cs?name=snippet_ConfigureLogging)]

### <a name="useconsolelifetime"></a><span data-ttu-id="b102b-232">UseConsoleLifetime</span><span class="sxs-lookup"><span data-stu-id="b102b-232">UseConsoleLifetime</span></span>

<span data-ttu-id="b102b-233"><xref:Microsoft.Extensions.Hosting.HostingHostBuilderExtensions.UseConsoleLifetime*> 侦听 `Ctrl+C`/SIGINT 或 SIGTERM 并调用 <xref:Microsoft.Extensions.Hosting.IApplicationLifetime.StopApplication*> 来启动关闭进程。</span><span class="sxs-lookup"><span data-stu-id="b102b-233"><xref:Microsoft.Extensions.Hosting.HostingHostBuilderExtensions.UseConsoleLifetime*> listens for `Ctrl+C`/SIGINT or SIGTERM and calls <xref:Microsoft.Extensions.Hosting.IApplicationLifetime.StopApplication*> to start the shutdown process.</span></span> <span data-ttu-id="b102b-234">`UseConsoleLifetime` 解除阻止 [ RunAsync](#runasync) 和 [WaitForShutdownAsync](#waitforshutdownasync) 等扩展。</span><span class="sxs-lookup"><span data-stu-id="b102b-234">`UseConsoleLifetime` unblocks extensions such as [RunAsync](#runasync) and [WaitForShutdownAsync](#waitforshutdownasync).</span></span> <span data-ttu-id="b102b-235"><xref:Microsoft.Extensions.Hosting.Internal.ConsoleLifetime> 预注册为默认生存期实现。</span><span class="sxs-lookup"><span data-stu-id="b102b-235"><xref:Microsoft.Extensions.Hosting.Internal.ConsoleLifetime> is pre-registered as the default lifetime implementation.</span></span> <span data-ttu-id="b102b-236">使用注册的最后一个生存期。</span><span class="sxs-lookup"><span data-stu-id="b102b-236">The last lifetime registered is used.</span></span>

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/Program.cs?name=snippet_UseConsoleLifetime)]

## <a name="container-configuration"></a><span data-ttu-id="b102b-237">容器配置</span><span class="sxs-lookup"><span data-stu-id="b102b-237">Container configuration</span></span>

<span data-ttu-id="b102b-238">为支持插入其他容器中，主机可以接受 <xref:Microsoft.Extensions.DependencyInjection.IServiceProviderFactory`1>。</span><span class="sxs-lookup"><span data-stu-id="b102b-238">To support plugging in other containers, the host can accept an <xref:Microsoft.Extensions.DependencyInjection.IServiceProviderFactory`1>.</span></span> <span data-ttu-id="b102b-239">提供工厂不属于 DI 容器注册，而是用于创建具体 DI 容器的主机内部函数。</span><span class="sxs-lookup"><span data-stu-id="b102b-239">Providing a factory isn't part of the DI container registration but is instead a host intrinsic used to create the concrete DI container.</span></span> <span data-ttu-id="b102b-240">[UseServiceProviderFactory(IServiceProviderFactory&lt;TContainerBuilder&gt;)](xref:Microsoft.Extensions.Hosting.HostBuilder.UseServiceProviderFactory*) 重写用于创建应用的服务提供程序的默认工厂。</span><span class="sxs-lookup"><span data-stu-id="b102b-240">[UseServiceProviderFactory(IServiceProviderFactory&lt;TContainerBuilder&gt;)](xref:Microsoft.Extensions.Hosting.HostBuilder.UseServiceProviderFactory*) overrides the default factory used to create the app's service provider.</span></span>

<span data-ttu-id="b102b-241"><xref:Microsoft.Extensions.Hosting.HostBuilder.ConfigureContainer*> 方法托管自定义容器配置。</span><span class="sxs-lookup"><span data-stu-id="b102b-241">Custom container configuration is managed by the <xref:Microsoft.Extensions.Hosting.HostBuilder.ConfigureContainer*> method.</span></span> <span data-ttu-id="b102b-242">`ConfigureContainer` 提供在基础主机 API 的基础之上配置容器的强类型体验。</span><span class="sxs-lookup"><span data-stu-id="b102b-242">`ConfigureContainer` provides a strongly-typed experience for configuring the container on top of the underlying host API.</span></span> <span data-ttu-id="b102b-243">可以利用相加结果多次调用 `ConfigureContainer`。</span><span class="sxs-lookup"><span data-stu-id="b102b-243">`ConfigureContainer` can be called multiple times with additive results.</span></span>

<span data-ttu-id="b102b-244">为应用创建服务容器：</span><span class="sxs-lookup"><span data-stu-id="b102b-244">Create a service container for the app:</span></span>

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/ServiceContainer.cs)]

<span data-ttu-id="b102b-245">提供服务容器工厂：</span><span class="sxs-lookup"><span data-stu-id="b102b-245">Provide a service container factory:</span></span>

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/ServiceContainerFactory.cs)]

<span data-ttu-id="b102b-246">使用该工厂并为应用配置自定义服务容器：</span><span class="sxs-lookup"><span data-stu-id="b102b-246">Use the factory and configure the custom service container for the app:</span></span>

[!code-csharp[](generic-host/samples-snapshot/2.x/GenericHostSample/Program.cs?name=snippet_ContainerConfiguration)]

## <a name="extensibility"></a><span data-ttu-id="b102b-247">扩展性</span><span class="sxs-lookup"><span data-stu-id="b102b-247">Extensibility</span></span>

<span data-ttu-id="b102b-248">在 `IHostBuilder` 上使用扩展方法实现主机扩展性。</span><span class="sxs-lookup"><span data-stu-id="b102b-248">Host extensibility is performed with extension methods on `IHostBuilder`.</span></span> <span data-ttu-id="b102b-249">以下示例介绍扩展方法如何使用 <xref:fundamentals/host/hosted-services> 中所示的 [TimedHostedService](xref:fundamentals/host/hosted-services#timed-background-tasks) 示例来扩展 `IHostBuilder` 实现。</span><span class="sxs-lookup"><span data-stu-id="b102b-249">The following example shows how an extension method extends an `IHostBuilder` implementation with the [TimedHostedService](xref:fundamentals/host/hosted-services#timed-background-tasks) example demonstrated in <xref:fundamentals/host/hosted-services>.</span></span>

```csharp
var host = new HostBuilder()
    .UseHostedService<TimedHostedService>()
    .Build();

await host.StartAsync();
```

<span data-ttu-id="b102b-250">应用建立 `UseHostedService` 扩展方法，以注册在 `T` 中传递的托管服务：</span><span class="sxs-lookup"><span data-stu-id="b102b-250">An app establishes the `UseHostedService` extension method to register the hosted service passed in `T`:</span></span>

```csharp
using System;
using Microsoft.Extensions.DependencyInjection;
using Microsoft.Extensions.Hosting;

public static class Extensions
{
    public static IHostBuilder UseHostedService<T>(this IHostBuilder hostBuilder)
        where T : class, IHostedService, IDisposable
    {
        return hostBuilder.ConfigureServices(services =>
            services.AddHostedService<T>());
    }
}
```

## <a name="manage-the-host"></a><span data-ttu-id="b102b-251">管理主机</span><span class="sxs-lookup"><span data-stu-id="b102b-251">Manage the host</span></span>

<span data-ttu-id="b102b-252"><xref:Microsoft.Extensions.Hosting.IHost> 实现负责启动和停止服务容器中注册的 `IHostedService` 实现。</span><span class="sxs-lookup"><span data-stu-id="b102b-252">The <xref:Microsoft.Extensions.Hosting.IHost> implementation is responsible for starting and stopping the `IHostedService` implementations that are registered in the service container.</span></span>

### <a name="run"></a><span data-ttu-id="b102b-253">运行</span><span class="sxs-lookup"><span data-stu-id="b102b-253">Run</span></span>

<span data-ttu-id="b102b-254"><xref:Microsoft.Extensions.Hosting.HostingAbstractionsHostExtensions.Run*> 运行应用并阻止调用线程，直到关闭主机：</span><span class="sxs-lookup"><span data-stu-id="b102b-254"><xref:Microsoft.Extensions.Hosting.HostingAbstractionsHostExtensions.Run*> runs the app and blocks the calling thread until the host is shut down:</span></span>

```csharp
public class Program
{
    public void Main(string[] args)
    {
        var host = new HostBuilder()
            .Build();

        host.Run();
    }
}
```

### <a name="runasync"></a><span data-ttu-id="b102b-255">RunAsync</span><span class="sxs-lookup"><span data-stu-id="b102b-255">RunAsync</span></span>

<span data-ttu-id="b102b-256"><xref:Microsoft.Extensions.Hosting.HostingAbstractionsHostExtensions.RunAsync*> 运行应用并返回在触发取消令牌或关闭时完成的 `Task`：</span><span class="sxs-lookup"><span data-stu-id="b102b-256"><xref:Microsoft.Extensions.Hosting.HostingAbstractionsHostExtensions.RunAsync*> runs the app and returns a `Task` that completes when the cancellation token or shutdown is triggered:</span></span>

```csharp
public class Program
{
    public static async Task Main(string[] args)
    {
        var host = new HostBuilder()
            .Build();

        await host.RunAsync();
    }
}
```

### <a name="runconsoleasync"></a><span data-ttu-id="b102b-257">RunConsoleAsync</span><span class="sxs-lookup"><span data-stu-id="b102b-257">RunConsoleAsync</span></span>

<span data-ttu-id="b102b-258"><xref:Microsoft.Extensions.Hosting.HostingHostBuilderExtensions.RunConsoleAsync*> 启用控制台支持、生成和启动主机，以及等待 `Ctrl+C`/SIGINT 或 SIGTERM 关闭。</span><span class="sxs-lookup"><span data-stu-id="b102b-258"><xref:Microsoft.Extensions.Hosting.HostingHostBuilderExtensions.RunConsoleAsync*> enables console support, builds and starts the host, and waits for `Ctrl+C`/SIGINT or SIGTERM to shut down.</span></span>

```csharp
public class Program
{
    public static async Task Main(string[] args)
    {
        var hostBuilder = new HostBuilder();

        await hostBuilder.RunConsoleAsync();
    }
}
```

### <a name="start-and-stopasync"></a><span data-ttu-id="b102b-259">Start 和 StopAsync</span><span class="sxs-lookup"><span data-stu-id="b102b-259">Start and StopAsync</span></span>

<span data-ttu-id="b102b-260"><xref:Microsoft.Extensions.Hosting.HostingAbstractionsHostExtensions.Start*> 同步启动主机。</span><span class="sxs-lookup"><span data-stu-id="b102b-260"><xref:Microsoft.Extensions.Hosting.HostingAbstractionsHostExtensions.Start*> starts the host synchronously.</span></span>

<span data-ttu-id="b102b-261"><xref:Microsoft.Extensions.Hosting.HostingAbstractionsHostExtensions.StopAsync*> 尝试在提供的超时时间内停止主机。</span><span class="sxs-lookup"><span data-stu-id="b102b-261"><xref:Microsoft.Extensions.Hosting.HostingAbstractionsHostExtensions.StopAsync*> attempts to stop the host within the provided timeout.</span></span>

```csharp
public class Program
{
    public static async Task Main(string[] args)
    {
        var host = new HostBuilder()
            .Build();

        using (host)
        {
            host.Start();

            await host.StopAsync(TimeSpan.FromSeconds(5));
        }
    }
}
```

### <a name="startasync-and-stopasync"></a><span data-ttu-id="b102b-262">StartAsync 和 StopAsync</span><span class="sxs-lookup"><span data-stu-id="b102b-262">StartAsync and StopAsync</span></span>

<span data-ttu-id="b102b-263"><xref:Microsoft.Extensions.Hosting.IHost.StartAsync*> 启动应用。</span><span class="sxs-lookup"><span data-stu-id="b102b-263"><xref:Microsoft.Extensions.Hosting.IHost.StartAsync*> starts the app.</span></span>

<span data-ttu-id="b102b-264"><xref:Microsoft.Extensions.Hosting.IHost.StopAsync*> 停止应用。</span><span class="sxs-lookup"><span data-stu-id="b102b-264"><xref:Microsoft.Extensions.Hosting.IHost.StopAsync*> stops the app.</span></span>

```csharp
public class Program
{
    public static async Task Main(string[] args)
    {
        var host = new HostBuilder()
            .Build();

        using (host)
        {
            await host.StartAsync();

            await host.StopAsync();
        }
    }
}
```

### <a name="waitforshutdown"></a><span data-ttu-id="b102b-265">WaitForShutdown</span><span class="sxs-lookup"><span data-stu-id="b102b-265">WaitForShutdown</span></span>

<span data-ttu-id="b102b-266"><xref:Microsoft.Extensions.Hosting.HostingAbstractionsHostExtensions.WaitForShutdown*> 通过 <xref:Microsoft.Extensions.Hosting.IHostLifetime> 触发，例如 <xref:Microsoft.Extensions.Hosting.Internal.ConsoleLifetime>（侦听 `Ctrl+C`/SIGINT 或 SIGTERM）。</span><span class="sxs-lookup"><span data-stu-id="b102b-266"><xref:Microsoft.Extensions.Hosting.HostingAbstractionsHostExtensions.WaitForShutdown*> is triggered via the <xref:Microsoft.Extensions.Hosting.IHostLifetime>, such as <xref:Microsoft.Extensions.Hosting.Internal.ConsoleLifetime> (listens for `Ctrl+C`/SIGINT or SIGTERM).</span></span> <span data-ttu-id="b102b-267">`WaitForShutdown` 调用 <xref:Microsoft.Extensions.Hosting.IHost.StopAsync*>。</span><span class="sxs-lookup"><span data-stu-id="b102b-267">`WaitForShutdown` calls <xref:Microsoft.Extensions.Hosting.IHost.StopAsync*>.</span></span>

```csharp
public class Program
{
    public void Main(string[] args)
    {
        var host = new HostBuilder()
            .Build();

        using (host)
        {
            host.Start();

            host.WaitForShutdown();
        }
    }
}
```

### <a name="waitforshutdownasync"></a><span data-ttu-id="b102b-268">WaitForShutdownAsync</span><span class="sxs-lookup"><span data-stu-id="b102b-268">WaitForShutdownAsync</span></span>

<span data-ttu-id="b102b-269"><xref:Microsoft.Extensions.Hosting.HostingAbstractionsHostExtensions.WaitForShutdownAsync*> 返回在通过给定的令牌和调用 <xref:Microsoft.Extensions.Hosting.IHost.StopAsync*> 来触发关闭时完成的 `Task`。</span><span class="sxs-lookup"><span data-stu-id="b102b-269"><xref:Microsoft.Extensions.Hosting.HostingAbstractionsHostExtensions.WaitForShutdownAsync*> returns a `Task` that completes when shutdown is triggered via the given token and calls <xref:Microsoft.Extensions.Hosting.IHost.StopAsync*>.</span></span>

```csharp
public class Program
{
    public static async Task Main(string[] args)
    {
        var host = new HostBuilder()
            .Build();

        using (host)
        {
            await host.StartAsync();

            await host.WaitForShutdownAsync();
        }

    }
}
```

### <a name="external-control"></a><span data-ttu-id="b102b-270">外部控件</span><span class="sxs-lookup"><span data-stu-id="b102b-270">External control</span></span>

<span data-ttu-id="b102b-271">使用可从外部调用的方法，能够实现主机的外部控件：</span><span class="sxs-lookup"><span data-stu-id="b102b-271">External control of the host can be achieved using methods that can be called externally:</span></span>

```csharp
public class Program
{
    private IHost _host;

    public Program()
    {
        _host = new HostBuilder()
            .Build();
    }

    public async Task StartAsync()
    {
        _host.StartAsync();
    }

    public async Task StopAsync()
    {
        using (_host)
        {
            await _host.StopAsync(TimeSpan.FromSeconds(5));
        }
    }
}
```

<span data-ttu-id="b102b-272">在 <xref:Microsoft.Extensions.Hosting.IHost.StartAsync*> 开始时调用 <xref:Microsoft.Extensions.Hosting.IHostLifetime.WaitForStartAsync*>，在继续之前，会一直等待该操作完成。</span><span class="sxs-lookup"><span data-stu-id="b102b-272"><xref:Microsoft.Extensions.Hosting.IHostLifetime.WaitForStartAsync*> is called at the start of <xref:Microsoft.Extensions.Hosting.IHost.StartAsync*>, which waits until it's complete before continuing.</span></span> <span data-ttu-id="b102b-273">它可用于延迟启动，直到外部事件发出信号。</span><span class="sxs-lookup"><span data-stu-id="b102b-273">This can be used to delay startup until signaled by an external event.</span></span>

## <a name="ihostingenvironment-interface"></a><span data-ttu-id="b102b-274">IHostingEnvironment 接口</span><span class="sxs-lookup"><span data-stu-id="b102b-274">IHostingEnvironment interface</span></span>

<span data-ttu-id="b102b-275"><xref:Microsoft.Extensions.Hosting.IHostingEnvironment> 提供有关应用托管环境的信息。</span><span class="sxs-lookup"><span data-stu-id="b102b-275"><xref:Microsoft.Extensions.Hosting.IHostingEnvironment> provides information about the app's hosting environment.</span></span> <span data-ttu-id="b102b-276">使用[构造函数注入](xref:fundamentals/dependency-injection)获取 `IHostingEnvironment` 以使用其属性和扩展方法：</span><span class="sxs-lookup"><span data-stu-id="b102b-276">Use [constructor injection](xref:fundamentals/dependency-injection) to obtain the `IHostingEnvironment` in order to use its properties and extension methods:</span></span>

```csharp
public class MyClass
{
    private readonly IHostingEnvironment _env;

    public MyClass(IHostingEnvironment env)
    {
        _env = env;
    }

    public void DoSomething()
    {
        var environmentName = _env.EnvironmentName;
    }
}
```

<span data-ttu-id="b102b-277">有关详细信息，请参阅 <xref:fundamentals/environments>。</span><span class="sxs-lookup"><span data-stu-id="b102b-277">For more information, see <xref:fundamentals/environments>.</span></span>

## <a name="iapplicationlifetime-interface"></a><span data-ttu-id="b102b-278">IApplicationLifetime 接口</span><span class="sxs-lookup"><span data-stu-id="b102b-278">IApplicationLifetime interface</span></span>

<span data-ttu-id="b102b-279"><xref:Microsoft.Extensions.Hosting.IApplicationLifetime> 允许启动后和关闭活动，包括正常关闭请求。</span><span class="sxs-lookup"><span data-stu-id="b102b-279"><xref:Microsoft.Extensions.Hosting.IApplicationLifetime> allows for post-startup and shutdown activities, including graceful shutdown requests.</span></span> <span data-ttu-id="b102b-280">接口上的三个属性是用于注册 `Action` 方法（用于定义启动和关闭事件）的取消标记。</span><span class="sxs-lookup"><span data-stu-id="b102b-280">Three properties on the interface are cancellation tokens used to register `Action` methods that define startup and shutdown events.</span></span>

| <span data-ttu-id="b102b-281">取消标记</span><span class="sxs-lookup"><span data-stu-id="b102b-281">Cancellation Token</span></span> | <span data-ttu-id="b102b-282">触发条件</span><span class="sxs-lookup"><span data-stu-id="b102b-282">Triggered when&#8230;</span></span> |
| ------------------ | --------------------- |
| <xref:Microsoft.Extensions.Hosting.IApplicationLifetime.ApplicationStarted*> | <span data-ttu-id="b102b-283">主机已完全启动。</span><span class="sxs-lookup"><span data-stu-id="b102b-283">The host has fully started.</span></span> |
| <xref:Microsoft.Extensions.Hosting.IApplicationLifetime.ApplicationStopped*> | <span data-ttu-id="b102b-284">主机正在完成正常关闭。</span><span class="sxs-lookup"><span data-stu-id="b102b-284">The host is completing a graceful shutdown.</span></span> <span data-ttu-id="b102b-285">应处理所有请求。</span><span class="sxs-lookup"><span data-stu-id="b102b-285">All requests should be processed.</span></span> <span data-ttu-id="b102b-286">关闭受到阻止，直到完成此事件。</span><span class="sxs-lookup"><span data-stu-id="b102b-286">Shutdown blocks until this event completes.</span></span> |
| <xref:Microsoft.Extensions.Hosting.IApplicationLifetime.ApplicationStopping*> | <span data-ttu-id="b102b-287">主机正在执行正常关闭。</span><span class="sxs-lookup"><span data-stu-id="b102b-287">The host is performing a graceful shutdown.</span></span> <span data-ttu-id="b102b-288">仍在处理请求。</span><span class="sxs-lookup"><span data-stu-id="b102b-288">Requests may still be processing.</span></span> <span data-ttu-id="b102b-289">关闭受到阻止，直到完成此事件。</span><span class="sxs-lookup"><span data-stu-id="b102b-289">Shutdown blocks until this event completes.</span></span> |

<span data-ttu-id="b102b-290">构造函数将 `IApplicationLifetime` 服务注入到任何类中。</span><span class="sxs-lookup"><span data-stu-id="b102b-290">Constructor-inject the `IApplicationLifetime` service into any class.</span></span> <span data-ttu-id="b102b-291">[示例应用](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/host/generic-host/samples/)将构造函数注入到 `LifetimeEventsHostedService` 类（一个 `IHostedService` 实现）中，用于注册事件。</span><span class="sxs-lookup"><span data-stu-id="b102b-291">The [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/host/generic-host/samples/) uses constructor injection into a `LifetimeEventsHostedService` class (an `IHostedService` implementation) to register the events.</span></span>

<span data-ttu-id="b102b-292">LifetimeEventsHostedService.cs：</span><span class="sxs-lookup"><span data-stu-id="b102b-292">*LifetimeEventsHostedService.cs*:</span></span>

[!code-csharp[](generic-host/samples/2.x/GenericHostSample/LifetimeEventsHostedService.cs?name=snippet1)]

<span data-ttu-id="b102b-293"><xref:Microsoft.Extensions.Hosting.IApplicationLifetime.StopApplication*> 请求终止应用。</span><span class="sxs-lookup"><span data-stu-id="b102b-293"><xref:Microsoft.Extensions.Hosting.IApplicationLifetime.StopApplication*> requests termination of the app.</span></span> <span data-ttu-id="b102b-294">以下类在调用类的 `Shutdown` 方法时使用 `StopApplication` 正常关闭应用：</span><span class="sxs-lookup"><span data-stu-id="b102b-294">The following class uses `StopApplication` to gracefully shut down an app when the class's `Shutdown` method is called:</span></span>

```csharp
public class MyClass
{
    private readonly IApplicationLifetime _appLifetime;

    public MyClass(IApplicationLifetime appLifetime)
    {
        _appLifetime = appLifetime;
    }

    public void Shutdown()
    {
        _appLifetime.StopApplication();
    }
}
```

## <a name="additional-resources"></a><span data-ttu-id="b102b-295">其他资源</span><span class="sxs-lookup"><span data-stu-id="b102b-295">Additional resources</span></span>

* <xref:fundamentals/host/hosted-services>
* [<span data-ttu-id="b102b-296">GitHub 上托管的存储库示例</span><span class="sxs-lookup"><span data-stu-id="b102b-296">Hosting repo samples on GitHub</span></span>](https://github.com/aspnet/Hosting/tree/release/2.1/samples)

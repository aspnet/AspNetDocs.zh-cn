---
title: 在 ASP.NET Core 中使用承载启动程序集
author: guardrex
description: 了解如何使用 IHostingStartup 从外部程序集增强 ASP.NET Core 应用。
monikerRange: '>= aspnetcore-2.0'
ms.author: riande
ms.custom: mvc, seodec18
ms.date: 02/14/2019
uid: fundamentals/configuration/platform-specific-configuration
ms.openlocfilehash: cffad201c84414ee4788877d80d3619a9013ae99
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57028734"
---
# <a name="use-hosting-startup-assemblies-in-aspnet-core"></a><span data-ttu-id="ddc13-103">在 ASP.NET Core 中使用承载启动程序集</span><span class="sxs-lookup"><span data-stu-id="ddc13-103">Use hosting startup assemblies in ASP.NET Core</span></span>

<span data-ttu-id="ddc13-104">作者：[Luke Latham](https://github.com/guardrex) 和 [Pavel Krymets](https://github.com/pakrym)</span><span class="sxs-lookup"><span data-stu-id="ddc13-104">By [Luke Latham](https://github.com/guardrex) and [Pavel Krymets](https://github.com/pakrym)</span></span>

<span data-ttu-id="ddc13-105">通过 [IHostingStartup](/dotnet/api/microsoft.aspnetcore.hosting.ihostingstartup)（承载启动）实现，在启动时从外部程序集向应用添加增强功能。</span><span class="sxs-lookup"><span data-stu-id="ddc13-105">An [IHostingStartup](/dotnet/api/microsoft.aspnetcore.hosting.ihostingstartup) (hosting startup) implementation adds enhancements to an app at startup from an external assembly.</span></span> <span data-ttu-id="ddc13-106">例如，外部库可使用承载启动实现为应用提供其他配置提供程序或服务。</span><span class="sxs-lookup"><span data-stu-id="ddc13-106">For example, an external library can use a hosting startup implementation to provide additional configuration providers or services to an app.</span></span> <span data-ttu-id="ddc13-107">ASP.NET Core 2.0 或更高版本中提供了 `IHostingStartup`。</span><span class="sxs-lookup"><span data-stu-id="ddc13-107">`IHostingStartup` *is available in ASP.NET Core 2.0 or later.*</span></span>

<span data-ttu-id="ddc13-108">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/host/platform-specific-configuration/samples/)（[如何下载](xref:index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="ddc13-108">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/host/platform-specific-configuration/samples/) ([how to download](xref:index#how-to-download-a-sample))</span></span>

## <a name="hostingstartup-attribute"></a><span data-ttu-id="ddc13-109">HostingStartup 属性</span><span class="sxs-lookup"><span data-stu-id="ddc13-109">HostingStartup attribute</span></span>

<span data-ttu-id="ddc13-110">[HostingStartup](/dotnet/api/microsoft.aspnetcore.hosting.hostingstartupattribute) 属性表示存在要在运行时激活的承载启动程序集。</span><span class="sxs-lookup"><span data-stu-id="ddc13-110">A [HostingStartup](/dotnet/api/microsoft.aspnetcore.hosting.hostingstartupattribute) attribute indicates the presence of a hosting startup assembly to activate at runtime.</span></span>

<span data-ttu-id="ddc13-111">将自动扫描输入程序集或包含 `Startup` 类的程序集以查找 `HostingStartup` 属性。</span><span class="sxs-lookup"><span data-stu-id="ddc13-111">The entry assembly or the assembly containing the `Startup` class is automatically scanned for the `HostingStartup` attribute.</span></span> <span data-ttu-id="ddc13-112">用于搜索 `HostingStartup` 属性的程序集列表在运行时从 [WebHostDefaults.HostingStartupAssembliesKey](/dotnet/api/microsoft.aspnetcore.hosting.webhostdefaults.hostingstartupassemblieskey) 中的配置加载。</span><span class="sxs-lookup"><span data-stu-id="ddc13-112">The list of assemblies to search for `HostingStartup` attributes is loaded at runtime from configuration in the [WebHostDefaults.HostingStartupAssembliesKey](/dotnet/api/microsoft.aspnetcore.hosting.webhostdefaults.hostingstartupassemblieskey).</span></span> <span data-ttu-id="ddc13-113">要从发现中排除的程序集列表从 [WebHostDefaults.HostingStartupExcludeAssembliesKey](/dotnet/api/microsoft.aspnetcore.hosting.webhostdefaults.hostingstartupexcludeassemblieskey) 加载。</span><span class="sxs-lookup"><span data-stu-id="ddc13-113">The list of assemblies to exclude from discovery is loaded from the [WebHostDefaults.HostingStartupExcludeAssembliesKey](/dotnet/api/microsoft.aspnetcore.hosting.webhostdefaults.hostingstartupexcludeassemblieskey).</span></span> <span data-ttu-id="ddc13-114">有关详细信息，请参阅 [Web 主机：承载启动程序集](xref:fundamentals/host/web-host#hosting-startup-assemblies)和 [Web 主机：承载启动排除程序集](xref:fundamentals/host/web-host#hosting-startup-exclude-assemblies)。</span><span class="sxs-lookup"><span data-stu-id="ddc13-114">For more information, see [Web Host: Hosting Startup Assemblies](xref:fundamentals/host/web-host#hosting-startup-assemblies) and [Web Host: Hosting Startup Exclude Assemblies](xref:fundamentals/host/web-host#hosting-startup-exclude-assemblies).</span></span>

<span data-ttu-id="ddc13-115">在以下示例中，承载启动程序集的命名空间为 `StartupEnhancement`。</span><span class="sxs-lookup"><span data-stu-id="ddc13-115">In the following example, the namespace of the hosting startup assembly is `StartupEnhancement`.</span></span> <span data-ttu-id="ddc13-116">包含承载启动代码的类是 `StartupEnhancementHostingStartup`：</span><span class="sxs-lookup"><span data-stu-id="ddc13-116">The class containing the hosting startup code is `StartupEnhancementHostingStartup`:</span></span>

[!code-csharp[](platform-specific-configuration/samples-snapshot/2.x/StartupEnhancement.cs?name=snippet1)]

<span data-ttu-id="ddc13-117">`HostingStartup` 属性通常位于承载启动程序集的 `IHostingStartup` 实现类文件中。</span><span class="sxs-lookup"><span data-stu-id="ddc13-117">The `HostingStartup` attribute is typically located in the hosting startup assembly's `IHostingStartup` implementation class file.</span></span>

## <a name="discover-loaded-hosting-startup-assemblies"></a><span data-ttu-id="ddc13-118">发现加载的承载启动程序集</span><span class="sxs-lookup"><span data-stu-id="ddc13-118">Discover loaded hosting startup assemblies</span></span>

<span data-ttu-id="ddc13-119">要发现加载的承载启动程序集，请启用日志记录并检查应用的日志。</span><span class="sxs-lookup"><span data-stu-id="ddc13-119">To discover loaded hosting startup assemblies, enable logging and check the app's logs.</span></span> <span data-ttu-id="ddc13-120">记录加载程序集时发生的错误。</span><span class="sxs-lookup"><span data-stu-id="ddc13-120">Errors that occur when loading assemblies are logged.</span></span> <span data-ttu-id="ddc13-121">会在调试级别记录加载的承载启动程序集，并记录所有错误。</span><span class="sxs-lookup"><span data-stu-id="ddc13-121">Loaded hosting startup assemblies are logged at the Debug level, and all errors are logged.</span></span>

## <a name="disable-automatic-loading-of-hosting-startup-assemblies"></a><span data-ttu-id="ddc13-122">禁用承载启动程序集的自动加载</span><span class="sxs-lookup"><span data-stu-id="ddc13-122">Disable automatic loading of hosting startup assemblies</span></span>

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="ddc13-123">要禁用承载启动程序集的自动加载，请使用以下方法之一：</span><span class="sxs-lookup"><span data-stu-id="ddc13-123">To disable automatic loading of hosting startup assemblies, use one of the following approaches:</span></span>

* <span data-ttu-id="ddc13-124">要阻止加载所有承载启动程序集，请将以下内容之一设置为 `true` 或 `1`：</span><span class="sxs-lookup"><span data-stu-id="ddc13-124">To prevent all hosting startup assemblies from loading, set one of the following to `true` or `1`:</span></span>
  * <span data-ttu-id="ddc13-125">[阻止承载启动](xref:fundamentals/host/web-host#prevent-hosting-startup)主机配置设置。</span><span class="sxs-lookup"><span data-stu-id="ddc13-125">[Prevent Hosting Startup](xref:fundamentals/host/web-host#prevent-hosting-startup) host configuration setting.</span></span>
  * <span data-ttu-id="ddc13-126">`ASPNETCORE_PREVENTHOSTINGSTARTUP` 环境变量。</span><span class="sxs-lookup"><span data-stu-id="ddc13-126">`ASPNETCORE_PREVENTHOSTINGSTARTUP` environment variable.</span></span>
* <span data-ttu-id="ddc13-127">要阻止加载特定的承载启动程序集，请将以下之一设置为以分号分隔的承载启动程序集字符串，以便在启动时排除：</span><span class="sxs-lookup"><span data-stu-id="ddc13-127">To prevent specific hosting startup assemblies from loading, set one of the following to a semicolon-delimited string of hosting startup assemblies to exclude at startup:</span></span>
  * <span data-ttu-id="ddc13-128">[承载启动排除程序集](xref:fundamentals/host/web-host#hosting-startup-exclude-assemblies)承载配置设置。</span><span class="sxs-lookup"><span data-stu-id="ddc13-128">[Hosting Startup Exclude Assemblies](xref:fundamentals/host/web-host#hosting-startup-exclude-assemblies) host configuration setting.</span></span>
  * <span data-ttu-id="ddc13-129">`ASPNETCORE_HOSTINGSTARTUPEXCLUDEASSEMBLIES` 环境变量。</span><span class="sxs-lookup"><span data-stu-id="ddc13-129">`ASPNETCORE_HOSTINGSTARTUPEXCLUDEASSEMBLIES` environment variable.</span></span>

::: moniker-end

::: moniker range="= aspnetcore-2.0"

<span data-ttu-id="ddc13-130">要禁用承载启动程序集的自动加载，请将以下之一设置为 `true` 或 `1`：</span><span class="sxs-lookup"><span data-stu-id="ddc13-130">To disable automatic loading of hosting startup assemblies, set one of the following to `true` or `1`:</span></span>

* <span data-ttu-id="ddc13-131">[阻止承载启动](xref:fundamentals/host/web-host#prevent-hosting-startup)主机配置设置。</span><span class="sxs-lookup"><span data-stu-id="ddc13-131">[Prevent Hosting Startup](xref:fundamentals/host/web-host#prevent-hosting-startup) host configuration setting.</span></span>
* <span data-ttu-id="ddc13-132">`ASPNETCORE_PREVENTHOSTINGSTARTUP` 环境变量。</span><span class="sxs-lookup"><span data-stu-id="ddc13-132">`ASPNETCORE_PREVENTHOSTINGSTARTUP` environment variable.</span></span>

::: moniker-end

<span data-ttu-id="ddc13-133">如果同时设置了主机配置设置和环境变量，则主机设置将控制行为。</span><span class="sxs-lookup"><span data-stu-id="ddc13-133">If both the host configuration setting and the environment variable are set, the host setting controls the behavior.</span></span>

<span data-ttu-id="ddc13-134">如果使用主机设置或环境变量来禁用承载启动程序集，将全局禁用程序集，并可能会禁用应用的多个特征。</span><span class="sxs-lookup"><span data-stu-id="ddc13-134">Disabling hosting startup assemblies using the host setting or environment variable disables the assembly globally and may disable several characteristics of an app.</span></span>

## <a name="project"></a><span data-ttu-id="ddc13-135">项目</span><span class="sxs-lookup"><span data-stu-id="ddc13-135">Project</span></span>

<span data-ttu-id="ddc13-136">使用以下任一项目类型创建承载启动：</span><span class="sxs-lookup"><span data-stu-id="ddc13-136">Create a hosting startup with either of the following project types:</span></span>

* [<span data-ttu-id="ddc13-137">类库</span><span class="sxs-lookup"><span data-stu-id="ddc13-137">Class library</span></span>](#class-library)
* [<span data-ttu-id="ddc13-138">无入口点的控制台应用</span><span class="sxs-lookup"><span data-stu-id="ddc13-138">Console app without an entry point</span></span>](#console-app-without-an-entry-point)

### <a name="class-library"></a><span data-ttu-id="ddc13-139">类库</span><span class="sxs-lookup"><span data-stu-id="ddc13-139">Class library</span></span>

<span data-ttu-id="ddc13-140">可在类库中提供承载启动增强。</span><span class="sxs-lookup"><span data-stu-id="ddc13-140">A hosting startup enhancement can be provided in a class library.</span></span> <span data-ttu-id="ddc13-141">库包含 `HostingStartup` 属性。</span><span class="sxs-lookup"><span data-stu-id="ddc13-141">The library contains a `HostingStartup` attribute.</span></span>

<span data-ttu-id="ddc13-142">[示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/host/platform-specific-configuration/samples/)包括 Razor Pages 应用、HostingStartupApp 和类库 HostingStartupLibrary。</span><span class="sxs-lookup"><span data-stu-id="ddc13-142">The [sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/host/platform-specific-configuration/samples/) includes a Razor Pages app, *HostingStartupApp*, and a class library, *HostingStartupLibrary*.</span></span> <span data-ttu-id="ddc13-143">类库：</span><span class="sxs-lookup"><span data-stu-id="ddc13-143">The class library:</span></span>

* <span data-ttu-id="ddc13-144">包含承载启动类 `ServiceKeyInjection`，用于实现 `IHostingStartup`。</span><span class="sxs-lookup"><span data-stu-id="ddc13-144">Contains a hosting startup class, `ServiceKeyInjection`, which implements `IHostingStartup`.</span></span> <span data-ttu-id="ddc13-145">`ServiceKeyInjection` 使用内存中配置提供程序 ([AddInMemoryCollection](/dotnet/api/microsoft.extensions.configuration.memoryconfigurationbuilderextensions.addinmemorycollection)) 将一对服务字符串添加到应用的配置中。</span><span class="sxs-lookup"><span data-stu-id="ddc13-145">`ServiceKeyInjection` adds a pair of service strings to the app's configuration using the in-memory configuration provider ([AddInMemoryCollection](/dotnet/api/microsoft.extensions.configuration.memoryconfigurationbuilderextensions.addinmemorycollection)).</span></span>
* <span data-ttu-id="ddc13-146">包含 `HostingStartup` 属性，用于标识承载启动的命名空间和类。</span><span class="sxs-lookup"><span data-stu-id="ddc13-146">Includes a `HostingStartup` attribute that identifies the hosting startup's namespace and class.</span></span>

<span data-ttu-id="ddc13-147">`ServiceKeyInjection` 类的 [Configure](/dotnet/api/microsoft.aspnetcore.hosting.ihostingstartup.configure) 方法使用 [IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder) 将增强功能添加到应用。</span><span class="sxs-lookup"><span data-stu-id="ddc13-147">The `ServiceKeyInjection` class's [Configure](/dotnet/api/microsoft.aspnetcore.hosting.ihostingstartup.configure) method uses an [IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder) to add enhancements to an app.</span></span>

<span data-ttu-id="ddc13-148">HostingStartupLibrary/ServiceKeyInjection.cs：</span><span class="sxs-lookup"><span data-stu-id="ddc13-148">*HostingStartupLibrary/ServiceKeyInjection.cs*:</span></span>

[!code-csharp[](platform-specific-configuration/samples/2.x/HostingStartupLibrary/ServiceKeyInjection.cs?name=snippet1)]

<span data-ttu-id="ddc13-149">应用的索引页读取并呈现类库承载启动程序集设置的两个键的配置值：</span><span class="sxs-lookup"><span data-stu-id="ddc13-149">The app's Index page reads and renders the configuration values for the two keys set by the class library's hosting startup assembly:</span></span>

<span data-ttu-id="ddc13-150">HostingStartupApp/Pages/Index.cshtml.cs：</span><span class="sxs-lookup"><span data-stu-id="ddc13-150">*HostingStartupApp/Pages/Index.cshtml.cs*:</span></span>

[!code-csharp[](platform-specific-configuration/samples/2.x/HostingStartupApp/Pages/Index.cshtml.cs?name=snippet1&highlight=5-6,11-12)]

<span data-ttu-id="ddc13-151">[示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/host/platform-specific-configuration/samples/)还包括一个 NuGet 包项目，该项目提供单独的承载启动 HostingStartupPackage。</span><span class="sxs-lookup"><span data-stu-id="ddc13-151">The [sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/host/platform-specific-configuration/samples/) also includes a NuGet package project that provides a separate hosting startup, *HostingStartupPackage*.</span></span> <span data-ttu-id="ddc13-152">该包具有与前述类库相同的特征。</span><span class="sxs-lookup"><span data-stu-id="ddc13-152">The package has the same characteristics of the class library described earlier.</span></span> <span data-ttu-id="ddc13-153">包：</span><span class="sxs-lookup"><span data-stu-id="ddc13-153">The package:</span></span>

* <span data-ttu-id="ddc13-154">包含承载启动类 `ServiceKeyInjection`，用于实现 `IHostingStartup`。</span><span class="sxs-lookup"><span data-stu-id="ddc13-154">Contains a hosting startup class, `ServiceKeyInjection`, which implements `IHostingStartup`.</span></span> <span data-ttu-id="ddc13-155">`ServiceKeyInjection` 将一对服务字符串添加到应用的配置中。</span><span class="sxs-lookup"><span data-stu-id="ddc13-155">`ServiceKeyInjection` adds a pair of service strings to the app's configuration.</span></span>
* <span data-ttu-id="ddc13-156">包含 `HostingStartup` 属性。</span><span class="sxs-lookup"><span data-stu-id="ddc13-156">Includes a `HostingStartup` attribute.</span></span>

<span data-ttu-id="ddc13-157">HostingStartupPackage/ServiceKeyInjection.cs：</span><span class="sxs-lookup"><span data-stu-id="ddc13-157">*HostingStartupPackage/ServiceKeyInjection.cs*:</span></span>

[!code-csharp[](platform-specific-configuration/samples/2.x/HostingStartupPackage/ServiceKeyInjection.cs?name=snippet1)]

<span data-ttu-id="ddc13-158">应用的索引页读取并呈现包承载启动程序集设置的两个键的配置值：</span><span class="sxs-lookup"><span data-stu-id="ddc13-158">The app's Index page reads and renders the configuration values for the two keys set by the package's hosting startup assembly:</span></span>

<span data-ttu-id="ddc13-159">HostingStartupApp/Pages/Index.cshtml.cs：</span><span class="sxs-lookup"><span data-stu-id="ddc13-159">*HostingStartupApp/Pages/Index.cshtml.cs*:</span></span>

[!code-csharp[](platform-specific-configuration/samples/2.x/HostingStartupApp/Pages/Index.cshtml.cs?name=snippet1&highlight=7-8,13-14)]

### <a name="console-app-without-an-entry-point"></a><span data-ttu-id="ddc13-160">无入口点的控制台应用</span><span class="sxs-lookup"><span data-stu-id="ddc13-160">Console app without an entry point</span></span>

<span data-ttu-id="ddc13-161">此方法仅适用于 .NET Core 应用，不适用于 .NET Framework。</span><span class="sxs-lookup"><span data-stu-id="ddc13-161">*This approach is only available for .NET Core apps, not .NET Framework.*</span></span>

<span data-ttu-id="ddc13-162">可在包含 `HostingStartup` 属性的无入口点的控制台应用中提供动态承载启动增强功能，该功能无需编译时引用进行激活。</span><span class="sxs-lookup"><span data-stu-id="ddc13-162">A dynamic hosting startup enhancement that doesn't require a compile-time reference for activation can be provided in a console app without an entry point that contains a `HostingStartup` attribute.</span></span> <span data-ttu-id="ddc13-163">发布控制台应用会生成可从运行时存储中使用的承载启动程序集。</span><span class="sxs-lookup"><span data-stu-id="ddc13-163">Publishing the console app produces a hosting startup assembly that can be consumed from the runtime store.</span></span>

<span data-ttu-id="ddc13-164">此过程中使用没有入口点的控制台应用，因为：</span><span class="sxs-lookup"><span data-stu-id="ddc13-164">A console app without an entry point is used in this process because:</span></span>

* <span data-ttu-id="ddc13-165">需要依赖项文件来使用承载启动程序集中的承载启动。</span><span class="sxs-lookup"><span data-stu-id="ddc13-165">A dependencies file is required to consume the hosting startup in the hosting startup assembly.</span></span> <span data-ttu-id="ddc13-166">依赖项文件是一种可运行的应用资产，它通过发布应用而不是库来生成。</span><span class="sxs-lookup"><span data-stu-id="ddc13-166">A dependencies file is a runnable app asset that's produced by publishing an app, not a library.</span></span>
* <span data-ttu-id="ddc13-167">无法直接将库添加到[运行时包存储](/dotnet/core/deploying/runtime-store)，该过程需要一个以已共享运行时为目标的可运行项目。</span><span class="sxs-lookup"><span data-stu-id="ddc13-167">A library can't be added directly to the [runtime package store](/dotnet/core/deploying/runtime-store), which requires a runnable project that targets the shared runtime.</span></span>

<span data-ttu-id="ddc13-168">创建动态承载启动过程中：</span><span class="sxs-lookup"><span data-stu-id="ddc13-168">In the creation of a dynamic hosting startup:</span></span>

* <span data-ttu-id="ddc13-169">从控制台应用创建承载启动程序集，无需以下入口点：</span><span class="sxs-lookup"><span data-stu-id="ddc13-169">A hosting startup assembly is created from the console app without an entry point that:</span></span>
  * <span data-ttu-id="ddc13-170">包含 `IHostingStartup` 实现的类。</span><span class="sxs-lookup"><span data-stu-id="ddc13-170">Includes a class that contains the `IHostingStartup` implementation.</span></span>
  * <span data-ttu-id="ddc13-171">包含用于识别 `IHostingStartup` 实现类的 [HostingStartup](/dotnet/api/microsoft.aspnetcore.hosting.hostingstartupattribute) 属性。</span><span class="sxs-lookup"><span data-stu-id="ddc13-171">Includes a [HostingStartup](/dotnet/api/microsoft.aspnetcore.hosting.hostingstartupattribute) attribute to identify the `IHostingStartup` implementation class.</span></span>
* <span data-ttu-id="ddc13-172">发布控制台应用，获取承载启动的依赖项。</span><span class="sxs-lookup"><span data-stu-id="ddc13-172">The console app is published to obtain the hosting startup's dependencies.</span></span> <span data-ttu-id="ddc13-173">发布控制台应用的结果是从依赖项文件中删除了未使用的依赖项。</span><span class="sxs-lookup"><span data-stu-id="ddc13-173">A consequence of publishing the console app is that unused dependencies are trimmed from the dependencies file.</span></span>
* <span data-ttu-id="ddc13-174">修改依赖项文件以设置承载启动程序集的运行时位置。</span><span class="sxs-lookup"><span data-stu-id="ddc13-174">The dependencies file is modified to set the runtime location of the hosting startup assembly.</span></span>
* <span data-ttu-id="ddc13-175">承载启动程序集及其依赖项文件位于运行时包存储中。</span><span class="sxs-lookup"><span data-stu-id="ddc13-175">The hosting startup assembly and its dependencies file is placed into the runtime package store.</span></span> <span data-ttu-id="ddc13-176">要发现承载启动程序集及其依赖项文件，它们将在一对环境变量中列出。</span><span class="sxs-lookup"><span data-stu-id="ddc13-176">To discover the hosting startup assembly and its dependencies file, they're listed in a pair of environment variables.</span></span>

<span data-ttu-id="ddc13-177">控制台应用引用 [Microsoft.AspNetCore.Hosting.Abstractions](https://www.nuget.org/packages/Microsoft.AspNetCore.Hosting.Abstractions/) 包：</span><span class="sxs-lookup"><span data-stu-id="ddc13-177">The console app references the [Microsoft.AspNetCore.Hosting.Abstractions](https://www.nuget.org/packages/Microsoft.AspNetCore.Hosting.Abstractions/) package:</span></span>

[!code-xml[](platform-specific-configuration/samples-snapshot/2.x/StartupEnhancement.csproj)]

<span data-ttu-id="ddc13-178">生成 [IWebHost](/dotnet/api/microsoft.aspnetcore.hosting.iwebhost) 时，[HostingStartup](/dotnet/api/microsoft.aspnetcore.hosting.hostingstartupattribute) 属性将类标识为 `IHostingStartup` 的实现，用于加载和执行。</span><span class="sxs-lookup"><span data-stu-id="ddc13-178">A [HostingStartup](/dotnet/api/microsoft.aspnetcore.hosting.hostingstartupattribute) attribute identifies a class as an implementation of `IHostingStartup` for loading and execution when building the [IWebHost](/dotnet/api/microsoft.aspnetcore.hosting.iwebhost).</span></span> <span data-ttu-id="ddc13-179">在下面的示例中，命名空间为 `StartupEnhancement`，类为 `StartupEnhancementHostingStartup`：</span><span class="sxs-lookup"><span data-stu-id="ddc13-179">In the following example, the namespace is `StartupEnhancement`, and the class is `StartupEnhancementHostingStartup`:</span></span>

[!code-csharp[](platform-specific-configuration/samples-snapshot/2.x/StartupEnhancement.cs?name=snippet1)]

<span data-ttu-id="ddc13-180">类实现 `IHostingStartup`。</span><span class="sxs-lookup"><span data-stu-id="ddc13-180">A class implements `IHostingStartup`.</span></span> <span data-ttu-id="ddc13-181">类的 [Configure](/dotnet/api/microsoft.aspnetcore.hosting.ihostingstartup.configure) 方法使用 [IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder) 将增强功能添加到应用。</span><span class="sxs-lookup"><span data-stu-id="ddc13-181">The class's [Configure](/dotnet/api/microsoft.aspnetcore.hosting.ihostingstartup.configure) method uses an [IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder) to add enhancements to an app.</span></span> <span data-ttu-id="ddc13-182">用户代码中 `Startup.Configure` 之前的运行时调用托管启动程序集中的 `IHostingStartup.Configure`，允许用户代码覆盖托管启动程序集提供的任何配置。</span><span class="sxs-lookup"><span data-stu-id="ddc13-182">`IHostingStartup.Configure` in the hosting startup assembly is called by the runtime before `Startup.Configure` in user code, which allows user code to overwrite any configuration provided by the hosting startup assembly.</span></span>

[!code-csharp[](platform-specific-configuration/samples-snapshot/2.x/StartupEnhancement.cs?name=snippet2&highlight=3,5)]

<span data-ttu-id="ddc13-183">生成 `IHostingStartup` 项目时，依赖项文件 (\*.deps.json) 将程序集的 `runtime` 位置设为 bin 文件夹：</span><span class="sxs-lookup"><span data-stu-id="ddc13-183">When building an `IHostingStartup` project, the dependencies file (*\*.deps.json*) sets the `runtime` location of the assembly to the *bin* folder:</span></span>

[!code-json[](platform-specific-configuration/samples-snapshot/2.x/StartupEnhancement1.deps.json?range=2-13&highlight=8)]

<span data-ttu-id="ddc13-184">仅显示部分文件。</span><span class="sxs-lookup"><span data-stu-id="ddc13-184">Only part of the file is shown.</span></span> <span data-ttu-id="ddc13-185">示例中程序集的名称是 `StartupEnhancement`。</span><span class="sxs-lookup"><span data-stu-id="ddc13-185">The assembly name in the example is `StartupEnhancement`.</span></span>

## <a name="configuration-provided-by-the-hosting-startup"></a><span data-ttu-id="ddc13-186">托管启动提供的配置</span><span class="sxs-lookup"><span data-stu-id="ddc13-186">Configuration provided by the hosting startup</span></span>

<span data-ttu-id="ddc13-187">处理配置有两种方法，具体取决于是希望托管启动的配置优先还是应用的配置优先：</span><span class="sxs-lookup"><span data-stu-id="ddc13-187">There are two approaches to handling configuration depending on whether you want the hosting startup's configuration to take precedence or the app's configuration to take precedence:</span></span>

1. <span data-ttu-id="ddc13-188">使用 <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder.ConfigureAppConfiguration*> 为应用提供配置，在应用的 <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder.ConfigureAppConfiguration*> 委托执行后加载配置。</span><span class="sxs-lookup"><span data-stu-id="ddc13-188">Provide configuration to the app using <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder.ConfigureAppConfiguration*> to load the configuration after the app's <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder.ConfigureAppConfiguration*> delegates execute.</span></span> <span data-ttu-id="ddc13-189">使用此方法，托管启动配置优先于应用的配置。</span><span class="sxs-lookup"><span data-stu-id="ddc13-189">Hosting startup configuration takes priority over the app's configuration using this approach.</span></span>
1. <span data-ttu-id="ddc13-190">使用 <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*> 为应用提供配置，在应用的 <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder.ConfigureAppConfiguration*> 委托执行之前加载配置。</span><span class="sxs-lookup"><span data-stu-id="ddc13-190">Provide configuration to the app using <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*> to load the configuration before the app's <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder.ConfigureAppConfiguration*> delegates execute.</span></span> <span data-ttu-id="ddc13-191">使用此方法，应用的配置值优先于托管启动程序提供的值。</span><span class="sxs-lookup"><span data-stu-id="ddc13-191">The app's configuration values take priority over those provided by the hosting startup using this approach.</span></span>

```csharp
public class ConfigurationInjection : IHostingStartup
{
    public void Configure(IWebHostBuilder builder)
    {
        Dictionary<string, string> dict;

        builder.ConfigureAppConfiguration(config =>
        {
            dict = new Dictionary<string, string>
            {
                {"ConfigurationKey1", 
                    "From IHostingStartup: Higher priority than the app's configuration."},
            };

            config.AddInMemoryCollection(dict);
        });

        dict = new Dictionary<string, string>
        {
            {"ConfigurationKey2", 
                "From IHostingStartup: Lower priority than the app's configuration."},
        };

        var builtConfig = new ConfigurationBuilder()
            .AddInMemoryCollection(dict)
            .Build();

        builder.UseConfiguration(builtConfig);
    }
}
```

## <a name="specify-the-hosting-startup-assembly"></a><span data-ttu-id="ddc13-192">指定承载启动程序集</span><span class="sxs-lookup"><span data-stu-id="ddc13-192">Specify the hosting startup assembly</span></span>

<span data-ttu-id="ddc13-193">对于类库或控制台应用提供的承载启动，请在 `ASPNETCORE_HOSTINGSTARTUPASSEMBLIES` 环境变量中指定承载启动程序集的名称。</span><span class="sxs-lookup"><span data-stu-id="ddc13-193">For either a class library- or console app-supplied hosting startup, specify the hosting startup assembly's name in the `ASPNETCORE_HOSTINGSTARTUPASSEMBLIES` environment variable.</span></span> <span data-ttu-id="ddc13-194">环境变量是以分号分隔的程序集列表。</span><span class="sxs-lookup"><span data-stu-id="ddc13-194">The environment variable is a semicolon-delimited list of assemblies.</span></span>

<span data-ttu-id="ddc13-195">仅扫描承载启动程序集以查找 `HostingStartup` 属性。</span><span class="sxs-lookup"><span data-stu-id="ddc13-195">Only hosting startup assemblies are scanned for the `HostingStartup` attribute.</span></span> <span data-ttu-id="ddc13-196">对于示例应用 HostingStartupApp，要发现前述的承载启动，请将环境变量设置为以下值：</span><span class="sxs-lookup"><span data-stu-id="ddc13-196">For the sample app, *HostingStartupApp*, to discover the hosting startups described earlier, the environment variable is set to the following value:</span></span>

```
HostingStartupLibrary;HostingStartupPackage;StartupDiagnostics
```

<span data-ttu-id="ddc13-197">还可使用[承载启动程序集](xref:fundamentals/host/web-host#hosting-startup-assemblies)主机配置设置来设置此承载启动程序集。</span><span class="sxs-lookup"><span data-stu-id="ddc13-197">A hosting startup assembly can also be set using the [Hosting Startup Assemblies](xref:fundamentals/host/web-host#hosting-startup-assemblies) host configuration setting.</span></span>

<span data-ttu-id="ddc13-198">存在多个托管启动程序集时，将按列出程序集的顺序执行 [Configure](/dotnet/api/microsoft.aspnetcore.hosting.ihostingstartup.configure) 方法。</span><span class="sxs-lookup"><span data-stu-id="ddc13-198">When multiple hosting startup assembles are present, their [Configure](/dotnet/api/microsoft.aspnetcore.hosting.ihostingstartup.configure) methods are executed in the order that the assemblies are listed.</span></span>

## <a name="activation"></a><span data-ttu-id="ddc13-199">激活</span><span class="sxs-lookup"><span data-stu-id="ddc13-199">Activation</span></span>

<span data-ttu-id="ddc13-200">承载启动激活的选项包括：</span><span class="sxs-lookup"><span data-stu-id="ddc13-200">Options for hosting startup activation are:</span></span>

* <span data-ttu-id="ddc13-201">[运行时存储](#runtime-store) &ndash; 激活无需用于激活的编译时引用。</span><span class="sxs-lookup"><span data-stu-id="ddc13-201">[Runtime store](#runtime-store) &ndash; Activation doesn't require a compile-time reference for activation.</span></span> <span data-ttu-id="ddc13-202">示例应用将承载启动程序集和依赖项文件放入文件夹“deployment”，以便在多计算机环境中部署承载启动。</span><span class="sxs-lookup"><span data-stu-id="ddc13-202">The sample app places the hosting startup assembly and dependencies files into a folder, *deployment*, to facilitate deployment of the hosting startup in a multimachine environment.</span></span> <span data-ttu-id="ddc13-203">“deployment”文件夹还包括 PowerShell 脚本，该脚本可在部署系统上创建或修改环境变量以启用承载启动。</span><span class="sxs-lookup"><span data-stu-id="ddc13-203">The *deployment* folder also includes a PowerShell script that creates or modifies environment variables on the deployment system to enable the hosting startup.</span></span>
* <span data-ttu-id="ddc13-204">激活所需的编译时引用</span><span class="sxs-lookup"><span data-stu-id="ddc13-204">Compile-time reference required for activation</span></span>
  * [<span data-ttu-id="ddc13-205">NuGet 包</span><span class="sxs-lookup"><span data-stu-id="ddc13-205">NuGet package</span></span>](#nuget-package)
  * [<span data-ttu-id="ddc13-206">项目 bin 文件夹</span><span class="sxs-lookup"><span data-stu-id="ddc13-206">Project bin folder</span></span>](#project-bin-folder)

### <a name="runtime-store"></a><span data-ttu-id="ddc13-207">运行时存储</span><span class="sxs-lookup"><span data-stu-id="ddc13-207">Runtime store</span></span>

<span data-ttu-id="ddc13-208">承载启动实现位于[运行时存储](/dotnet/core/deploying/runtime-store)中。</span><span class="sxs-lookup"><span data-stu-id="ddc13-208">The hosting startup implementation is placed in the [runtime store](/dotnet/core/deploying/runtime-store).</span></span> <span data-ttu-id="ddc13-209">增强型应用无需对程序集进行编译时引用。</span><span class="sxs-lookup"><span data-stu-id="ddc13-209">A compile-time reference to the assembly isn't required by the enhanced app.</span></span>

<span data-ttu-id="ddc13-210">构建承载启动后，使用清单项目文件和 [dotnet store](/dotnet/core/tools/dotnet-store) 命令生成运行时存储。</span><span class="sxs-lookup"><span data-stu-id="ddc13-210">After the hosting startup is built, a runtime store is generated using the manifest project file and the [dotnet store](/dotnet/core/tools/dotnet-store) command.</span></span>

```console
dotnet store --manifest {MANIFEST FILE} --runtime {RUNTIME IDENTIFIER} --output {OUTPUT LOCATION} --skip-optimization
```

<span data-ttu-id="ddc13-211">在示例应用（*RuntimeStore* 项目）中，使用以下命令：</span><span class="sxs-lookup"><span data-stu-id="ddc13-211">In the sample app (*RuntimeStore* project) the following command is used:</span></span>

``` console
dotnet store --manifest store.manifest.csproj --runtime win7-x64 --output ./deployment/store --skip-optimization
```

<span data-ttu-id="ddc13-212">对于发现运行时存储的运行时，运行时存储的位置将添加到 `DOTNET_SHARED_STORE` 环境变量中。</span><span class="sxs-lookup"><span data-stu-id="ddc13-212">For the runtime to discover the runtime store, the runtime store's location is added to the `DOTNET_SHARED_STORE` environment variable.</span></span>

<span data-ttu-id="ddc13-213">**修改并放置承载启动的依赖项文件**</span><span class="sxs-lookup"><span data-stu-id="ddc13-213">**Modify and place the hosting startup's dependencies file**</span></span>

<span data-ttu-id="ddc13-214">要在未包引用增强功能的情况下激活增强功能，请使用 `additionalDeps` 为运行时指定附加依赖项。</span><span class="sxs-lookup"><span data-stu-id="ddc13-214">To activate the enhancement without a package reference to the enhancement, specify additional dependencies to the runtime with `additionalDeps`.</span></span> <span data-ttu-id="ddc13-215">使用 `additionalDeps`，你可以：</span><span class="sxs-lookup"><span data-stu-id="ddc13-215">`additionalDeps` allows you to:</span></span>

* <span data-ttu-id="ddc13-216">通过提供一组附加的 *\*.deps.json* 文件来扩展应用的库图，以便在启动时与应用自身的 *\*.deps.json* 文件合并。</span><span class="sxs-lookup"><span data-stu-id="ddc13-216">Extend the app's library graph by providing a set of additional *\*.deps.json* files to merge with the app's own *\*.deps.json* file on startup.</span></span>
* <span data-ttu-id="ddc13-217">使承载启动程序集可被发现并可加载。</span><span class="sxs-lookup"><span data-stu-id="ddc13-217">Make the hosting startup assembly discoverable and loadable.</span></span>

<span data-ttu-id="ddc13-218">生成附加依赖项文件的推荐方法是：</span><span class="sxs-lookup"><span data-stu-id="ddc13-218">The recommended approach for generating the additional dependencies file is to:</span></span>

 1. <span data-ttu-id="ddc13-219">对上一节中引用的运行时存储清单文件执行 `dotnet publish`。</span><span class="sxs-lookup"><span data-stu-id="ddc13-219">Execute `dotnet publish` on the runtime store manifest file referenced in the previous section.</span></span>
 1. <span data-ttu-id="ddc13-220">从库中删除清单引用，以及生成的 *\*deps.json* 文件的 `runtime` 部分。</span><span class="sxs-lookup"><span data-stu-id="ddc13-220">Remove the manifest reference from libraries and the `runtime` section of the resulting *\*deps.json* file.</span></span>

<span data-ttu-id="ddc13-221">在示例项目中，`store.manifest/1.0.0` 属性已从 `targets` 和 `libraries` 部分中删除：</span><span class="sxs-lookup"><span data-stu-id="ddc13-221">In the example project, the `store.manifest/1.0.0` property is removed from the `targets` and `libraries` section:</span></span>

```json
{
  "runtimeTarget": {
    "name": ".NETCoreApp,Version=v2.1",
    "signature": "4ea77c7b75ad1895ae1ea65e6ba2399010514f99"
  },
  "compilationOptions": {},
  "targets": {
    ".NETCoreApp,Version=v2.1": {
      "store.manifest/1.0.0": {
        "dependencies": {
          "StartupDiagnostics": "1.0.0"
        },
        "runtime": {
          "store.manifest.dll": {}
        }
      },
      "StartupDiagnostics/1.0.0": {
        "runtime": {
          "lib/netcoreapp2.1/StartupDiagnostics.dll": {
            "assemblyVersion": "1.0.0.0",
            "fileVersion": "1.0.0.0"
          }
        }
      }
    }
  },
  "libraries": {
    "store.manifest/1.0.0": {
      "type": "project",
      "serviceable": false,
      "sha512": ""
    },
    "StartupDiagnostics/1.0.0": {
      "type": "package",
      "serviceable": true,
      "sha512": "sha512-oiQr60vBQW7+nBTmgKLSldj06WNLRTdhOZpAdEbCuapoZ+M2DJH2uQbRLvFT8EGAAv4TAKzNtcztpx5YOgBXQQ==",
      "path": "startupdiagnostics/1.0.0",
      "hashPath": "startupdiagnostics.1.0.0.nupkg.sha512"
    }
  }
}
```

<span data-ttu-id="ddc13-222">将 *\*.deps.json* 文件放入以下位置：</span><span class="sxs-lookup"><span data-stu-id="ddc13-222">Place the *\*.deps.json* file into the following location:</span></span>

```
{ADDITIONAL DEPENDENCIES PATH}/shared/{SHARED FRAMEWORK NAME}/{SHARED FRAMEWORK VERSION}/{ENHANCEMENT ASSEMBLY NAME}.deps.json
```

* <span data-ttu-id="ddc13-223">`{ADDITIONAL DEPENDENCIES PATH}` &ndash; 添加到 `DOTNET_ADDITIONAL_DEPS` 环境变量中的位置。</span><span class="sxs-lookup"><span data-stu-id="ddc13-223">`{ADDITIONAL DEPENDENCIES PATH}` &ndash; Location added to the `DOTNET_ADDITIONAL_DEPS` environment variable.</span></span>
* <span data-ttu-id="ddc13-224">`{SHARED FRAMEWORK NAME}` &ndash; 此附加依赖项文件所需的共享框架。</span><span class="sxs-lookup"><span data-stu-id="ddc13-224">`{SHARED FRAMEWORK NAME}` &ndash; Shared framework required for this additional dependencies file.</span></span>
* <span data-ttu-id="ddc13-225">`{SHARED FRAMEWORK VERSION}` &ndash; 最小共享框架版本。</span><span class="sxs-lookup"><span data-stu-id="ddc13-225">`{SHARED FRAMEWORK VERSION}` &ndash; Minimum shared framework version.</span></span>
* <span data-ttu-id="ddc13-226">`{ENHANCEMENT ASSEMBLY NAME}` &ndash; 增强功能的程序集名称。</span><span class="sxs-lookup"><span data-stu-id="ddc13-226">`{ENHANCEMENT ASSEMBLY NAME}` &ndash; The enhancement's assembly name.</span></span>

<span data-ttu-id="ddc13-227">在示例应用（*RuntimeStore*  项目）中，附加依赖项文件放于以下位置：</span><span class="sxs-lookup"><span data-stu-id="ddc13-227">In the sample app (*RuntimeStore* project), the additional dependencies file is placed into the following location:</span></span>

```
additionalDeps/shared/Microsoft.AspNetCore.App/2.1.0/StartupDiagnostics.deps.json
```

<span data-ttu-id="ddc13-228">对于发现运行时存储位置的运行时，附加依赖项文件位置将添加到 `DOTNET_ADDITIONAL_DEPS` 环境变量中。</span><span class="sxs-lookup"><span data-stu-id="ddc13-228">For runtime to discover the runtime store location, the additional dependencies file location is added to the `DOTNET_ADDITIONAL_DEPS` environment variable.</span></span>

<span data-ttu-id="ddc13-229">在示例应用（*RuntimeStore* 项目）中，使用 [PowerShell](/powershell/scripting/powershell-scripting) 脚本完成构建运行时存储并生成附加依赖项文件。</span><span class="sxs-lookup"><span data-stu-id="ddc13-229">In the sample app (*RuntimeStore* project), building the runtime store and generating the additional dependencies file is accomplished using a [PowerShell](/powershell/scripting/powershell-scripting) script.</span></span>

<span data-ttu-id="ddc13-230">有关如何设置各种操作系统的环境变量的示例，请参阅[使用多个环境](xref:fundamentals/environments)。</span><span class="sxs-lookup"><span data-stu-id="ddc13-230">For examples of how to set environment variables for various operating systems, see [Use multiple environments](xref:fundamentals/environments).</span></span>

<span data-ttu-id="ddc13-231">**部署**</span><span class="sxs-lookup"><span data-stu-id="ddc13-231">**Deployment**</span></span>

<span data-ttu-id="ddc13-232">为了便于在多计算机环境中部署托承载启动，示例应用在已发布的输出中创建一个“deployment”文件夹，其中包含：</span><span class="sxs-lookup"><span data-stu-id="ddc13-232">To facilitate the deployment of a hosting startup in a multimachine environment, the sample app creates a *deployment* folder in published output that contains:</span></span>

* <span data-ttu-id="ddc13-233">承载启动运行时存储。</span><span class="sxs-lookup"><span data-stu-id="ddc13-233">The hosting startup runtime store.</span></span>
* <span data-ttu-id="ddc13-234">承载启动依赖项文件。</span><span class="sxs-lookup"><span data-stu-id="ddc13-234">The hosting startup dependencies file.</span></span>
* <span data-ttu-id="ddc13-235">PowerShell 脚本，用于创建或修改 `ASPNETCORE_HOSTINGSTARTUPASSEMBLIES`、`DOTNET_SHARED_STORE` 和 `DOTNET_ADDITIONAL_DEPS` 以支持激活承载启动。</span><span class="sxs-lookup"><span data-stu-id="ddc13-235">A PowerShell script that creates or modifies the `ASPNETCORE_HOSTINGSTARTUPASSEMBLIES`, `DOTNET_SHARED_STORE`, and `DOTNET_ADDITIONAL_DEPS` to support the activation of the hosting startup.</span></span> <span data-ttu-id="ddc13-236">从部署系统上的管理 PowerShell 命令提示符运行脚本。</span><span class="sxs-lookup"><span data-stu-id="ddc13-236">Run the script from an administrative PowerShell command prompt on the deployment system.</span></span>

### <a name="nuget-package"></a><span data-ttu-id="ddc13-237">NuGet 程序包</span><span class="sxs-lookup"><span data-stu-id="ddc13-237">NuGet package</span></span>

<span data-ttu-id="ddc13-238">可在 NuGet 包中提供承载启动增强。</span><span class="sxs-lookup"><span data-stu-id="ddc13-238">A hosting startup enhancement can be provided in a NuGet package.</span></span> <span data-ttu-id="ddc13-239">该包含有 `HostingStartup` 属性。</span><span class="sxs-lookup"><span data-stu-id="ddc13-239">The package has a `HostingStartup` attribute.</span></span> <span data-ttu-id="ddc13-240">包提供的承载启动类型使用以下任一方法提供给应用：</span><span class="sxs-lookup"><span data-stu-id="ddc13-240">The hosting startup types provided by the package are made available to the app using either of the following approaches:</span></span>

* <span data-ttu-id="ddc13-241">增强型应用的项目文件在应用的项目文件（编译时引用）中为承载启动提供了包引用。</span><span class="sxs-lookup"><span data-stu-id="ddc13-241">The enhanced app's project file makes a package reference for the hosting startup in the app's project file (a compile-time reference).</span></span> <span data-ttu-id="ddc13-242">有了编译时引用，承载启动程序集及其所有依赖项都会合并到应用的依赖项文件 (\*.deps.json) 中。</span><span class="sxs-lookup"><span data-stu-id="ddc13-242">With the compile-time reference in place, the hosting startup assembly and all of its dependencies are incorporated into the app's dependency file (*\*.deps.json*).</span></span> <span data-ttu-id="ddc13-243">此方法适用于已发布到 [nuget.org](https://www.nuget.org/) 的承载启动程序集包。</span><span class="sxs-lookup"><span data-stu-id="ddc13-243">This approach applies to a hosting startup assembly package published to [nuget.org](https://www.nuget.org/).</span></span>
* <span data-ttu-id="ddc13-244">承载启动的依赖项文件可用于增强型应用，如[运行时存储](#runtime-store)部分所述（无编译时引用）。</span><span class="sxs-lookup"><span data-stu-id="ddc13-244">The hosting startup's dependencies file is made available to the enhanced app as described in the [Runtime store](#runtime-store) section (without a compile-time reference).</span></span>

<span data-ttu-id="ddc13-245">有关 NuGet 包和运行时存储的详细信息，请参阅以下主题：</span><span class="sxs-lookup"><span data-stu-id="ddc13-245">For more information on NuGet packages and the runtime store, see the following topics:</span></span>

* [<span data-ttu-id="ddc13-246">如何使用跨平台工具创建 NuGet 包</span><span class="sxs-lookup"><span data-stu-id="ddc13-246">How to Create a NuGet Package with Cross Platform Tools</span></span>](/dotnet/core/deploying/creating-nuget-packages)
* [<span data-ttu-id="ddc13-247">发布包</span><span class="sxs-lookup"><span data-stu-id="ddc13-247">Publishing packages</span></span>](/nuget/create-packages/publish-a-package)
* [<span data-ttu-id="ddc13-248">运行时包存储</span><span class="sxs-lookup"><span data-stu-id="ddc13-248">Runtime package store</span></span>](/dotnet/core/deploying/runtime-store)

### <a name="project-bin-folder"></a><span data-ttu-id="ddc13-249">项目 bin 文件夹</span><span class="sxs-lookup"><span data-stu-id="ddc13-249">Project bin folder</span></span>

<span data-ttu-id="ddc13-250">承载启动增强功能可通过增强型应用中的 bin -deployed 程序集提供。</span><span class="sxs-lookup"><span data-stu-id="ddc13-250">A hosting startup enhancement can be provided by a *bin*-deployed assembly in the enhanced app.</span></span> <span data-ttu-id="ddc13-251">程序集提供的承载启动类型使用以下任一方法提供给应用：</span><span class="sxs-lookup"><span data-stu-id="ddc13-251">The hosting startup types provided by the assembly are made available to the app using either of the following approaches:</span></span>

* <span data-ttu-id="ddc13-252">增强型应用的项目文件对承载启动进行了程序集引用（编译时引用）。</span><span class="sxs-lookup"><span data-stu-id="ddc13-252">The enhanced app's project file makes an assembly reference to the hosting startup (a compile-time reference).</span></span> <span data-ttu-id="ddc13-253">有了编译时引用，承载启动程序集及其所有依赖项都会合并到应用的依赖项文件 (\*.deps.json) 中。</span><span class="sxs-lookup"><span data-stu-id="ddc13-253">With the compile-time reference in place, the hosting startup assembly and all of its dependencies are incorporated into the app's dependency file (*\*.deps.json*).</span></span> <span data-ttu-id="ddc13-254">如果部署方案要求将已编译承载启动库的程序集（DLL 文件）移动到使用项目中或使用项目可访问的位置，并且对承载启动程序集进行编译时引用，此方法适用。</span><span class="sxs-lookup"><span data-stu-id="ddc13-254">This approach applies when the deployment scenario calls for moving the compiled hosting startup library's assembly (DLL file) to the consuming project or to a location accessible by the consuming project and a compile-time reference is made to the hosting startup's assembly.</span></span>
* <span data-ttu-id="ddc13-255">承载启动的依赖项文件可用于增强型应用，如[运行时存储](#runtime-store)部分所述（无编译时引用）。</span><span class="sxs-lookup"><span data-stu-id="ddc13-255">The hosting startup's dependencies file is made available to the enhanced app as described in the [Runtime store](#runtime-store) section (without a compile-time reference).</span></span>

## <a name="sample-code"></a><span data-ttu-id="ddc13-256">示例代码</span><span class="sxs-lookup"><span data-stu-id="ddc13-256">Sample code</span></span>

<span data-ttu-id="ddc13-257">[示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/host/platform-specific-configuration/samples/)（[如何下载](xref:index#how-to-download-a-sample)）演示了承载启动实现方案：</span><span class="sxs-lookup"><span data-stu-id="ddc13-257">The [sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/host/platform-specific-configuration/samples/) ([how to download](xref:index#how-to-download-a-sample)) demonstrates hosting startup implementation scenarios:</span></span>

* <span data-ttu-id="ddc13-258">两个承载启动程序集（类库）分别设置一对内存中配置键值对：</span><span class="sxs-lookup"><span data-stu-id="ddc13-258">Two hosting startup assemblies (class libraries) set a pair of in-memory configuration key-value pairs each:</span></span>
  * <span data-ttu-id="ddc13-259">NuGet 包 (HostingStartupPackage)</span><span class="sxs-lookup"><span data-stu-id="ddc13-259">NuGet package (*HostingStartupPackage*)</span></span>
  * <span data-ttu-id="ddc13-260">类库 (HostingStartupLibrary)</span><span class="sxs-lookup"><span data-stu-id="ddc13-260">Class library (*HostingStartupLibrary*)</span></span>
* <span data-ttu-id="ddc13-261">从运行时存储部署的程序集 (StartupDiagnostics) 激活承载启动。</span><span class="sxs-lookup"><span data-stu-id="ddc13-261">A hosting startup is activated from a runtime store-deployed assembly (*StartupDiagnostics*).</span></span> <span data-ttu-id="ddc13-262">该程序集在启动时将两个中间件添加到应用，用于提供以下内容的诊断信息：</span><span class="sxs-lookup"><span data-stu-id="ddc13-262">The assembly adds two middlewares to the app at startup that provide diagnostic information on:</span></span>
  * <span data-ttu-id="ddc13-263">已注册服务</span><span class="sxs-lookup"><span data-stu-id="ddc13-263">Registered services</span></span>
  * <span data-ttu-id="ddc13-264">地址（方案、主机、基路径、路径、查询字符串）</span><span class="sxs-lookup"><span data-stu-id="ddc13-264">Address (scheme, host, path base, path, query string)</span></span>
  * <span data-ttu-id="ddc13-265">连接（远程 IP、远程端口、本地 IP、本地端口、客户端证书）</span><span class="sxs-lookup"><span data-stu-id="ddc13-265">Connection (remote IP, remote port, local IP, local port, client certificate)</span></span>
  * <span data-ttu-id="ddc13-266">请求标头</span><span class="sxs-lookup"><span data-stu-id="ddc13-266">Request headers</span></span>
  * <span data-ttu-id="ddc13-267">环境变量</span><span class="sxs-lookup"><span data-stu-id="ddc13-267">Environment variables</span></span>

<span data-ttu-id="ddc13-268">运行示例：</span><span class="sxs-lookup"><span data-stu-id="ddc13-268">To run the sample:</span></span>

<span data-ttu-id="ddc13-269">**从 NuGet 包激活**</span><span class="sxs-lookup"><span data-stu-id="ddc13-269">**Activation from a NuGet package**</span></span>

1. <span data-ttu-id="ddc13-270">使用 [dotnet pack](/dotnet/core/tools/dotnet-pack) 命令编译 HostingStartupPackage 包。</span><span class="sxs-lookup"><span data-stu-id="ddc13-270">Compile the *HostingStartupPackage* package with the [dotnet pack](/dotnet/core/tools/dotnet-pack) command.</span></span>
1. <span data-ttu-id="ddc13-271">将包的程序集名称 HostingStartupPackage 添加到 `ASPNETCORE_HOSTINGSTARTUPASSEMBLIES` 环境变量中。</span><span class="sxs-lookup"><span data-stu-id="ddc13-271">Add the package's assembly name of the *HostingStartupPackage* to the `ASPNETCORE_HOSTINGSTARTUPASSEMBLIES` environment variable.</span></span>
1. <span data-ttu-id="ddc13-272">编译并运行应用。</span><span class="sxs-lookup"><span data-stu-id="ddc13-272">Compile and run the app.</span></span> <span data-ttu-id="ddc13-273">增强型应用中存在包引用（编译时引用）。</span><span class="sxs-lookup"><span data-stu-id="ddc13-273">A package reference is present in the enhanced app (a compile-time reference).</span></span> <span data-ttu-id="ddc13-274">应用项目文件中的 `<PropertyGroup>` 指定包项目的输出 (../HostingStartupPackage/bin/Debug) 作为包源。</span><span class="sxs-lookup"><span data-stu-id="ddc13-274">A `<PropertyGroup>` in the app's project file specifies the package project's output (*../HostingStartupPackage/bin/Debug*) as a package source.</span></span> <span data-ttu-id="ddc13-275">这允许应用使用该包而无需将包上传到 [nuget.org](https://www.nuget.org/)。有关详细信息，请参阅 HostingStartupApp 项目文件中的说明。</span><span class="sxs-lookup"><span data-stu-id="ddc13-275">This allows the app to use the package without uploading the package to [nuget.org](https://www.nuget.org/). For more information, see the notes in the HostingStartupApp's project file.</span></span>

   ```xml
   <PropertyGroup>
     <RestoreSources>$(RestoreSources);https://api.nuget.org/v3/index.json;../HostingStartupPackage/bin/Debug</RestoreSources>
   </PropertyGroup>
   ```
1. <span data-ttu-id="ddc13-276">观察到索引页呈现的服务配置键值与包的 `ServiceKeyInjection.Configure` 方法设置的值匹配。</span><span class="sxs-lookup"><span data-stu-id="ddc13-276">Observe that the service configuration key values rendered by the Index page match the values set by the package's `ServiceKeyInjection.Configure` method.</span></span>

<span data-ttu-id="ddc13-277">如果更改并重新编译 HostingStartupPackage 项目，请清除本地 NuGet 包缓存，确保 HostingStartupApp 从本地缓存中收到更新后的包而不是旧包。</span><span class="sxs-lookup"><span data-stu-id="ddc13-277">If you make changes to the *HostingStartupPackage* project and recompile it, clear the local NuGet package caches to ensure that the *HostingStartupApp* receives the updated package and not a stale package from the local cache.</span></span> <span data-ttu-id="ddc13-278">要清除本地 NuGet 缓存，请执行以下 [dotnet nuget locals](/dotnet/core/tools/dotnet-nuget-locals) 命令：</span><span class="sxs-lookup"><span data-stu-id="ddc13-278">To clear the local NuGet caches, execute the following [dotnet nuget locals](/dotnet/core/tools/dotnet-nuget-locals) command:</span></span>

```console
dotnet nuget locals all --clear
```

<span data-ttu-id="ddc13-279">**从类库激活**</span><span class="sxs-lookup"><span data-stu-id="ddc13-279">**Activation from a class library**</span></span>

1. <span data-ttu-id="ddc13-280">使用 [dotnet build](/dotnet/core/tools/dotnet-build) 命令编译 HostingStartupLibrary 类库。</span><span class="sxs-lookup"><span data-stu-id="ddc13-280">Compile the *HostingStartupLibrary* class library with the [dotnet build](/dotnet/core/tools/dotnet-build) command.</span></span>
1. <span data-ttu-id="ddc13-281">将类库的程序集名称 HostingStartupLibrary 添加到 `ASPNETCORE_HOSTINGSTARTUPASSEMBLIES` 环境变量中。</span><span class="sxs-lookup"><span data-stu-id="ddc13-281">Add the class library's assembly name of *HostingStartupLibrary* to the `ASPNETCORE_HOSTINGSTARTUPASSEMBLIES` environment variable.</span></span>
1. <span data-ttu-id="ddc13-282">bin - 通过将类库编译输出中的 HostingStartupLibrary.dll 文件复制到应用的 bin/Debug 文件夹，将类库程序集部署到应用。</span><span class="sxs-lookup"><span data-stu-id="ddc13-282">*bin*-deploy the class library's assembly to the app by copying the *HostingStartupLibrary.dll* file from the class library's compiled output to the app's *bin/Debug* folder.</span></span>
1. <span data-ttu-id="ddc13-283">编译并运行应用。</span><span class="sxs-lookup"><span data-stu-id="ddc13-283">Compile and run the app.</span></span> <span data-ttu-id="ddc13-284">应用项目文件中的 `<ItemGroup>` 引用类库的程序集 (.\bin\Debug\netcoreapp2.1\HostingStartupLibrary.dll)（编译时引用）。</span><span class="sxs-lookup"><span data-stu-id="ddc13-284">An `<ItemGroup>` in the app's project file references the class library's assembly (*.\bin\Debug\netcoreapp2.1\HostingStartupLibrary.dll*) (a compile-time reference).</span></span> <span data-ttu-id="ddc13-285">有关详细信息，请参阅 HostingStartupApp 项目文件中的说明。</span><span class="sxs-lookup"><span data-stu-id="ddc13-285">For more information, see the notes in the HostingStartupApp's project file.</span></span>

   ```xml
   <ItemGroup>
     <Reference Include=".\bin\Debug\netcoreapp2.1\HostingStartupLibrary.dll">
       <HintPath>.\bin\Debug\netcoreapp2.1\HostingStartupLibrary.dll</HintPath>
       <SpecificVersion>False</SpecificVersion>
     </Reference>
   </ItemGroup>
   ```
1. <span data-ttu-id="ddc13-286">观察到索引页呈现的服务配置键值与类库的 `ServiceKeyInjection.Configure` 方法设置的值匹配。</span><span class="sxs-lookup"><span data-stu-id="ddc13-286">Observe that the service configuration key values rendered by the Index page match the values set by the class library's `ServiceKeyInjection.Configure` method.</span></span>

<span data-ttu-id="ddc13-287">**从运行时存储部署的程序集激活**</span><span class="sxs-lookup"><span data-stu-id="ddc13-287">**Activation from a runtime store-deployed assembly**</span></span>

1. <span data-ttu-id="ddc13-288">StartupDiagnostics 项目使用 [PowerShell](/powershell/scripting/powershell-scripting) 修改其 StartupDiagnostics.deps.json 文件。</span><span class="sxs-lookup"><span data-stu-id="ddc13-288">The *StartupDiagnostics* project uses [PowerShell](/powershell/scripting/powershell-scripting) to modify its *StartupDiagnostics.deps.json* file.</span></span> <span data-ttu-id="ddc13-289">默认情况下，Windows 7 SP1 和 Windows Server 2008 R2 SP1 及以后版本的 Windows 上安装有 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="ddc13-289">PowerShell is installed by default on Windows starting with Windows 7 SP1 and Windows Server 2008 R2 SP1.</span></span> <span data-ttu-id="ddc13-290">若要在其他平台上获取 PowerShell，请参阅[安装 Windows PowerShell](/powershell/scripting/setup/installing-powershell#powershell-core)。</span><span class="sxs-lookup"><span data-stu-id="ddc13-290">To obtain PowerShell on other platforms, see [Installing Windows PowerShell](/powershell/scripting/setup/installing-powershell#powershell-core).</span></span>
1. <span data-ttu-id="ddc13-291">构建 StartupDiagnostics 项目。</span><span class="sxs-lookup"><span data-stu-id="ddc13-291">Build the *StartupDiagnostics* project.</span></span> <span data-ttu-id="ddc13-292">构建项目后，会自动生成项目文件中的构建目标：</span><span class="sxs-lookup"><span data-stu-id="ddc13-292">After the project is built, a build target in the project file automatically:</span></span>
   * <span data-ttu-id="ddc13-293">触发 PowerShell 脚本以修改 StartupDiagnostics.deps.json 文件。</span><span class="sxs-lookup"><span data-stu-id="ddc13-293">Triggers the PowerShell script to modify the *StartupDiagnostics.deps.json* file.</span></span>
   * <span data-ttu-id="ddc13-294">将 StartupDiagnostics.deps.json 文件移动到用户配置文件的 additionalDeps 文件夹。</span><span class="sxs-lookup"><span data-stu-id="ddc13-294">Moves the *StartupDiagnostics.deps.json* file to the user profile's *additionalDeps* folder.</span></span>
1. <span data-ttu-id="ddc13-295">在承载启动目录的命令提示符处执行 `dotnet store` 命令，将程序集及其依赖项存储在用户配置文件的运行时存储中：</span><span class="sxs-lookup"><span data-stu-id="ddc13-295">Execute the `dotnet store` command at a command prompt in the hosting startup's directory to store the assembly and its dependencies in the user profile's runtime store:</span></span>

   ```console
   dotnet store --manifest StartupDiagnostics.csproj --runtime <RID>
   ```
   <span data-ttu-id="ddc13-296">对于 Windows，该命令使用 `win7-x64` [运行时标识符 (RID)](/dotnet/core/rid-catalog)。</span><span class="sxs-lookup"><span data-stu-id="ddc13-296">For Windows, the command uses the `win7-x64` [runtime identifier (RID)](/dotnet/core/rid-catalog).</span></span> <span data-ttu-id="ddc13-297">为其他运行时提供承载启动时，请替换为正确的 RID。</span><span class="sxs-lookup"><span data-stu-id="ddc13-297">When providing the hosting startup for a different runtime, substitute the correct RID.</span></span>
1. <span data-ttu-id="ddc13-298">设置环境变量：</span><span class="sxs-lookup"><span data-stu-id="ddc13-298">Set the environment variables:</span></span>
   * <span data-ttu-id="ddc13-299">将程序集名称 StartupDiagnostics 的添加到 `ASPNETCORE_HOSTINGSTARTUPASSEMBLIES` 环境变量中。</span><span class="sxs-lookup"><span data-stu-id="ddc13-299">Add the assembly name of *StartupDiagnostics* to the `ASPNETCORE_HOSTINGSTARTUPASSEMBLIES` environment variable.</span></span>
   * <span data-ttu-id="ddc13-300">在 Windows 上，将 `DOTNET_ADDITIONAL_DEPS` 环境变量设置为 `%UserProfile%\.dotnet\x64\additionalDeps\StartupDiagnostics\`。</span><span class="sxs-lookup"><span data-stu-id="ddc13-300">On Windows, set the `DOTNET_ADDITIONAL_DEPS` environment variable to `%UserProfile%\.dotnet\x64\additionalDeps\StartupDiagnostics\`.</span></span> <span data-ttu-id="ddc13-301">在 macOS/Linux 上，将 `DOTNET_ADDITIONAL_DEPS` 环境变量设置为 `/Users/<USER>/.dotnet/x64/additionalDeps/StartupDiagnostics/`，其中 `<USER>` 是包含承载启动的用户配置文件。</span><span class="sxs-lookup"><span data-stu-id="ddc13-301">On macOS/Linux, set the `DOTNET_ADDITIONAL_DEPS` environment variable to `/Users/<USER>/.dotnet/x64/additionalDeps/StartupDiagnostics/`, where `<USER>` is the user profile that contains the hosting startup.</span></span>
1. <span data-ttu-id="ddc13-302">运行示例应用。</span><span class="sxs-lookup"><span data-stu-id="ddc13-302">Run the sample app.</span></span>
1. <span data-ttu-id="ddc13-303">请求 `/services` 终结点以查看应用的注册服务。</span><span class="sxs-lookup"><span data-stu-id="ddc13-303">Request the `/services` endpoint to see the app's registered services.</span></span> <span data-ttu-id="ddc13-304">请求 `/diag` 终结点以查看诊断信息。</span><span class="sxs-lookup"><span data-stu-id="ddc13-304">Request the `/diag` endpoint to see the diagnostic information.</span></span>

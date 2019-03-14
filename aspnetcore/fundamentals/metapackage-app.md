---
title: ASP.NET Core 2.1 及更高版本的 Microsoft.AspNetCore.App 元包
author: Rick-Anderson
description: Microsoft.AspNetCore.App 元包包含所有受支持的 ASP.NET Core 和 Entity Framework Core 包。
monikerRange: '>= aspnetcore-2.1'
ms.author: riande
ms.date: 09/20/2017
uid: fundamentals/metapackage-app
ms.openlocfilehash: 68b5aca60273a8c6ef03c0a29842e6a5305adeb3
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57034434"
---
# <a name="microsoftaspnetcoreapp-metapackage-for-aspnet-core-21"></a><span data-ttu-id="5b0c2-103">ASP.NET Core 2.1 的 Microsoft.AspNetCore.App 元包</span><span class="sxs-lookup"><span data-stu-id="5b0c2-103">Microsoft.AspNetCore.App metapackage for ASP.NET Core 2.1</span></span>

<span data-ttu-id="5b0c2-104">此功能需要面向 .NET Core 2.1 及更高版本的 ASP.NET Core 2.1。</span><span class="sxs-lookup"><span data-stu-id="5b0c2-104">This feature requires ASP.NET Core 2.1 and later targeting .NET Core 2.1 and later.</span></span>

<span data-ttu-id="5b0c2-105">ASP.NET Core 的 [Microsoft.AspNetCore.App](https://www.nuget.org/packages/Microsoft.AspNetCore.App) [元包](/dotnet/core/packages#metapackages)：</span><span class="sxs-lookup"><span data-stu-id="5b0c2-105">The [Microsoft.AspNetCore.App](https://www.nuget.org/packages/Microsoft.AspNetCore.App) [metapackage](/dotnet/core/packages#metapackages) for ASP.NET Core:</span></span>

* <span data-ttu-id="5b0c2-106">不包括第三方依赖项，[Json.NET](https://www.nuget.org/packages/Newtonsoft.Json/)、[Remotion.Linq](https://www.nuget.org/packages/Remotion.Linq/) 和 [IX-Async](https://www.nuget.org/packages/System.Interactive.Async/) 除外。</span><span class="sxs-lookup"><span data-stu-id="5b0c2-106">Does not include third-party dependencies except for [Json.NET](https://www.nuget.org/packages/Newtonsoft.Json/), [Remotion.Linq](https://www.nuget.org/packages/Remotion.Linq/), and [IX-Async](https://www.nuget.org/packages/System.Interactive.Async/).</span></span> <span data-ttu-id="5b0c2-107">为确保正常使用主要框架功能，这些第三方依赖项均为必要条件。</span><span class="sxs-lookup"><span data-stu-id="5b0c2-107">These 3rd-party dependencies are deemed necessary to ensure the major frameworks features function.</span></span>
* <span data-ttu-id="5b0c2-108">包括 ASP.NET Core 团队支持的所有软件包，包含第三方依赖项的软件包（不包括上文所述）除外。</span><span class="sxs-lookup"><span data-stu-id="5b0c2-108">Includes all supported packages by the ASP.NET Core team except those that contain third-party dependencies (other than those previously mentioned).</span></span>
* <span data-ttu-id="5b0c2-109">包括 Entity Framework Core 团队支持的所有软件包，包含第三方依赖项的软件包（不包括上文所述）除外。</span><span class="sxs-lookup"><span data-stu-id="5b0c2-109">Includes all supported packages by the Entity Framework Core team except those that contain third-party dependencies (other than those previously mentioned).</span></span>

<span data-ttu-id="5b0c2-110">`Microsoft.AspNetCore.App` 包中包含了 ASP.NET Core 2.1 及更高版本和 Entity Framework Core 2.1 及更高版本的所有功能。</span><span class="sxs-lookup"><span data-stu-id="5b0c2-110">All the features of ASP.NET Core 2.1 and later and Entity Framework Core 2.1 and later are included in the `Microsoft.AspNetCore.App` package.</span></span> <span data-ttu-id="5b0c2-111">面向 ASP.NET Core 2.1 及更高版本的默认项目模板使用此包。</span><span class="sxs-lookup"><span data-stu-id="5b0c2-111">The default project templates targeting ASP.NET Core 2.1 and later use this package.</span></span> <span data-ttu-id="5b0c2-112">建议面向 ASP.NET Core 2.1 及更高版本和 Entity Framework Core 2.1 及更高版本的应用程序使用 `Microsoft.AspNetCore.App` 包。</span><span class="sxs-lookup"><span data-stu-id="5b0c2-112">We recommend applications targeting ASP.NET Core 2.1 and later and Entity Framework Core 2.1 and later use the `Microsoft.AspNetCore.App` package.</span></span>

<span data-ttu-id="5b0c2-113">`Microsoft.AspNetCore.App` 元包的版本号表示 ASP.NET Core 版本和 Entity Framework Core 版本。</span><span class="sxs-lookup"><span data-stu-id="5b0c2-113">The version number of the `Microsoft.AspNetCore.App` metapackage represents the ASP.NET Core version and Entity Framework Core version.</span></span>

<span data-ttu-id="5b0c2-114">使用 `Microsoft.AspNetCore.App` 元包可提供用于保护应用的版本限制：</span><span class="sxs-lookup"><span data-stu-id="5b0c2-114">Using the `Microsoft.AspNetCore.App` metapackage provides version restrictions that protect your app:</span></span>

* <span data-ttu-id="5b0c2-115">如果包含的包对 `Microsoft.AspNetCore.App` 中的包具有可传递的（非直接）依赖项，且这些版本号不同，则 NuGet 将生成错误。</span><span class="sxs-lookup"><span data-stu-id="5b0c2-115">If a package is included that has a transitive (not direct) dependency on a package in `Microsoft.AspNetCore.App`, and those version numbers differ, NuGet will generate an error.</span></span>
* <span data-ttu-id="5b0c2-116">添加到应用的其他包无法更改 `Microsoft.AspNetCore.App` 中包含的包版本。</span><span class="sxs-lookup"><span data-stu-id="5b0c2-116">Other packages added to your app cannot change the version of packages included in `Microsoft.AspNetCore.App`.</span></span>
* <span data-ttu-id="5b0c2-117">版本一致性能确保可靠的体验。</span><span class="sxs-lookup"><span data-stu-id="5b0c2-117">Version consistency ensures a reliable experience.</span></span> <span data-ttu-id="5b0c2-118">`Microsoft.AspNetCore.App` 旨在防止在同一应用中结合使用未经测试的相关位版本组合。</span><span class="sxs-lookup"><span data-stu-id="5b0c2-118">`Microsoft.AspNetCore.App` was designed to prevent untested version combinations of related bits being used together in the same app.</span></span>

<span data-ttu-id="5b0c2-119">使用 `Microsoft.AspNetCore.App` 元包的应用程序会自动使用 ASP.NET Core 共享框架。</span><span class="sxs-lookup"><span data-stu-id="5b0c2-119">Applications that use the `Microsoft.AspNetCore.App` metapackage automatically take advantage of the ASP.NET Core shared framework.</span></span> <span data-ttu-id="5b0c2-120">使用 `Microsoft.AspNetCore.App` 元包时，应用程序不部署所引用的 ASP.NET Core NuGet 包中的任何资产 &mdash; .NET Core 共享框架包含这些资产。</span><span class="sxs-lookup"><span data-stu-id="5b0c2-120">When you use the `Microsoft.AspNetCore.App` metapackage, **no** assets from the referenced ASP.NET Core NuGet packages are deployed with the application&mdash;the ASP.NET Core shared framework contains these assets.</span></span> <span data-ttu-id="5b0c2-121">共享框架中的资产已经过预编译，以便缩短应用程序启动时间。</span><span class="sxs-lookup"><span data-stu-id="5b0c2-121">The assets in the shared framework are precompiled to improve application startup time.</span></span> <span data-ttu-id="5b0c2-122">有关详细信息，请参阅 [.NET Core 分发打包](/dotnet/core/build/distribution-packaging)中的“共享框架”。</span><span class="sxs-lookup"><span data-stu-id="5b0c2-122">For more information, see "shared framework" in [.NET Core distribution packaging](/dotnet/core/build/distribution-packaging).</span></span>

<span data-ttu-id="5b0c2-123">以下项目文件为 ASP.NET Core 引用 `Microsoft.AspNetCore.App` 元包，该文件是一种典型的 ASP.NET Core 2.1 模板：</span><span class="sxs-lookup"><span data-stu-id="5b0c2-123">The following project file references the `Microsoft.AspNetCore.App` metapackage for ASP.NET Core and represents a typical ASP.NET Core 2.1 template:</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk.Web">

  <PropertyGroup>
    <TargetFramework>netcoreapp2.1</TargetFramework>
  </PropertyGroup>

  <ItemGroup>
    <PackageReference Include="Microsoft.AspNetCore.App" />
  </ItemGroup>

</Project>
```

<span data-ttu-id="5b0c2-124">前面的标记表示典型的 ASP.NET Core 2.1 及更高版本模板。</span><span class="sxs-lookup"><span data-stu-id="5b0c2-124">The preceding markup represents a typical ASP.NET Core 2.1 and later template.</span></span> <span data-ttu-id="5b0c2-125">它不会为 `Microsoft.AspNetCore.App` 包引用指定版本号。</span><span class="sxs-lookup"><span data-stu-id="5b0c2-125">It doesn't specify a version number for the `Microsoft.AspNetCore.App` package reference.</span></span> <span data-ttu-id="5b0c2-126">如果未指定版本，SDK 会指定[隐式](https://github.com/dotnet/core/blob/master/release-notes/1.0/sdk/1.0-rc3-implicit-package-refs.md)版本，即 `Microsoft.NET.Sdk.Web`。</span><span class="sxs-lookup"><span data-stu-id="5b0c2-126">When the version is not specified, an [implicit](https://github.com/dotnet/core/blob/master/release-notes/1.0/sdk/1.0-rc3-implicit-package-refs.md) version is specified by the SDK, that is, `Microsoft.NET.Sdk.Web`.</span></span> <span data-ttu-id="5b0c2-127">建议使用 SDK 指定的隐式版本，而不是在包引用上显式设置版本号。</span><span class="sxs-lookup"><span data-stu-id="5b0c2-127">We recommend relying on the implicit version specified by the SDK and not explicitly setting the version number on the package reference.</span></span> <span data-ttu-id="5b0c2-128">如果对这种方法有任何疑问，可以在 [Microsoft.AspNetCore.App 隐式版本讨论](https://github.com/aspnet/Docs/issues/6430)上发表 GitHub 评论。</span><span class="sxs-lookup"><span data-stu-id="5b0c2-128">If you have questions on this approach, leave a GitHub comment at the [Discussion for the Microsoft.AspNetCore.App implicit version](https://github.com/aspnet/Docs/issues/6430).</span></span>

<span data-ttu-id="5b0c2-129">对于便携式应用，隐式版本设置为 `major.minor.0`。</span><span class="sxs-lookup"><span data-stu-id="5b0c2-129">The implicit version is set to `major.minor.0` for portable apps.</span></span> <span data-ttu-id="5b0c2-130">共享框架前滚机制将在安装的共享框架的最新兼容版本上运行应用。</span><span class="sxs-lookup"><span data-stu-id="5b0c2-130">The shared framework roll-forward mechanism will run the app on the latest compatible version among the installed shared frameworks.</span></span> <span data-ttu-id="5b0c2-131">为确保在开发、测试和生产中使用相同的版本，请确保在所有环境中都安装相同版本的共享框架。</span><span class="sxs-lookup"><span data-stu-id="5b0c2-131">To guarantee the same version is used in development, test, and production, ensure the same version of the shared framework is installed in all environments.</span></span> <span data-ttu-id="5b0c2-132">对于独立应用，将隐式版本号设置为在已安装的 SDK 中捆绑的共享框架的 `major.minor.patch`。</span><span class="sxs-lookup"><span data-stu-id="5b0c2-132">For self contained apps, the implicit version number is set to the `major.minor.patch` of the shared framework bundled in the installed SDK.</span></span>

<span data-ttu-id="5b0c2-133">在 `Microsoft.AspNetCore.App` 引用上指定版本号，不能保证将选择该共享框架版本。</span><span class="sxs-lookup"><span data-stu-id="5b0c2-133">Specifying a version number on the `Microsoft.AspNetCore.App` reference does **not** guarantee that version of the shared framework will be chosen.</span></span> <span data-ttu-id="5b0c2-134">例如，假设指定的版本是“2.1.1”，但安装的是“2.1.3”。</span><span class="sxs-lookup"><span data-stu-id="5b0c2-134">For example, suppose version "2.1.1" is specified, but "2.1.3" is installed.</span></span> <span data-ttu-id="5b0c2-135">这种情况下，应用将使用"2.1.3"。</span><span class="sxs-lookup"><span data-stu-id="5b0c2-135">In that case, the app will use "2.1.3".</span></span> <span data-ttu-id="5b0c2-136">不过不建议这样做，你可以禁用前滚（修补程序和/或次要版本）。</span><span class="sxs-lookup"><span data-stu-id="5b0c2-136">Although not recommended, you can disable roll forward (patch and/or minor).</span></span> <span data-ttu-id="5b0c2-137">有关 dotnet 主机前滚以及如何配置其行为的详细信息，请参阅 [dotnet 主机前滚](https://github.com/dotnet/core-setup/blob/master/Documentation/design-docs/roll-forward-on-no-candidate-fx.md)。</span><span class="sxs-lookup"><span data-stu-id="5b0c2-137">For more information regarding dotnet host roll-forward and how to configure its behavior, see [dotnet host roll forward](https://github.com/dotnet/core-setup/blob/master/Documentation/design-docs/roll-forward-on-no-candidate-fx.md).</span></span>

<span data-ttu-id="5b0c2-138">`<Project Sdk` 必须设置为 `Microsoft.NET.Sdk.Web` 以使用隐式版本 `Microsoft.AspNetCore.App`。</span><span class="sxs-lookup"><span data-stu-id="5b0c2-138">`<Project Sdk` must be set to `Microsoft.NET.Sdk.Web` to use the implicit version `Microsoft.AspNetCore.App`.</span></span>  <span data-ttu-id="5b0c2-139">使用 `<Project Sdk="Microsoft.NET.Sdk">`（不带尾随 `.Web`）时：</span><span class="sxs-lookup"><span data-stu-id="5b0c2-139">When `<Project Sdk="Microsoft.NET.Sdk">` (without the trailing `.Web`) is used:</span></span>

* <span data-ttu-id="5b0c2-140">生成以下警告：</span><span class="sxs-lookup"><span data-stu-id="5b0c2-140">The following warning is generated:</span></span>

     <span data-ttu-id="5b0c2-141">*警告 NU1604:项目依赖项 Microsoft.AspNetCore.App 不包含包含下限。* 请在依赖项版本中包括下限，以确保一致的还原结果。</span><span class="sxs-lookup"><span data-stu-id="5b0c2-141">*Warning NU1604: Project dependency Microsoft.AspNetCore.App does not contain an inclusive lower bound. Include a lower bound in the dependency version to ensure consistent restore results.*</span></span>
* <span data-ttu-id="5b0c2-142">这是 .NET Core 2.1 SDK 的一个已知问题，将在 .NET Core 2.2 SDK 中修复。</span><span class="sxs-lookup"><span data-stu-id="5b0c2-142">This is a known issue with the .NET Core 2.1 SDK and will be fixed in the .NET Core 2.2 SDK.</span></span>

<a name="update"></a>

## <a name="update-aspnet-core"></a><span data-ttu-id="5b0c2-143">更新 ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="5b0c2-143">Update ASP.NET Core</span></span>

<span data-ttu-id="5b0c2-144">`Microsoft.AspNetCore.App` [元包](/dotnet/core/packages#metapackages)不是从 NuGet 更新的传统包。</span><span class="sxs-lookup"><span data-stu-id="5b0c2-144">The `Microsoft.AspNetCore.App` [metapackage](/dotnet/core/packages#metapackages) isn't a traditional package that's updated from NuGet.</span></span> <span data-ttu-id="5b0c2-145">类似于 `Microsoft.NETCore.App`，`Microsoft.AspNetCore.App` 表示共享运行时，它具有在 NuGet 之外处理的特殊版本控制语义。</span><span class="sxs-lookup"><span data-stu-id="5b0c2-145">Similar to `Microsoft.NETCore.App`, `Microsoft.AspNetCore.App` represents a shared runtime, which has special versioning semantics handled outside of NuGet.</span></span> <span data-ttu-id="5b0c2-146">有关详细信息，请参阅[包、元包和框架](/dotnet/core/packages)。</span><span class="sxs-lookup"><span data-stu-id="5b0c2-146">For more information, see [Packages, metapackages and frameworks](/dotnet/core/packages).</span></span>

<span data-ttu-id="5b0c2-147">更新 ASP.NET Core：</span><span class="sxs-lookup"><span data-stu-id="5b0c2-147">To update ASP.NET Core:</span></span>

* <span data-ttu-id="5b0c2-148">在开发计算机和生成服务器：下载并安装[.NET Core SDK](https://www.microsoft.com/net/download)。</span><span class="sxs-lookup"><span data-stu-id="5b0c2-148">On development machines and build servers: Download and install the [.NET Core SDK](https://www.microsoft.com/net/download).</span></span>
* <span data-ttu-id="5b0c2-149">在部署服务器：下载并安装[.NET Core 运行时](https://www.microsoft.com/net/download)。</span><span class="sxs-lookup"><span data-stu-id="5b0c2-149">On deployment servers: Download and install the [.NET Core runtime](https://www.microsoft.com/net/download).</span></span>

 <span data-ttu-id="5b0c2-150">在应用程序重启时，应用程序将前滚到最新安装的版本。</span><span class="sxs-lookup"><span data-stu-id="5b0c2-150">Applications will roll forward to the latest installed version on application restart.</span></span> <span data-ttu-id="5b0c2-151">无需更新项目文件中的 `Microsoft.AspNetCore.App` 版本号。</span><span class="sxs-lookup"><span data-stu-id="5b0c2-151">It's not necessary to update the `Microsoft.AspNetCore.App` version number in the project file.</span></span> <span data-ttu-id="5b0c2-152">有关详细信息，请参阅[依赖于框架的应用会前滚](/dotnet/core/versions/selection#framework-dependent-apps-roll-forward)。</span><span class="sxs-lookup"><span data-stu-id="5b0c2-152">For more information, see [Framework-dependent apps roll forward](/dotnet/core/versions/selection#framework-dependent-apps-roll-forward).</span></span>

<span data-ttu-id="5b0c2-153">如果应用程序之前使用 `Microsoft.AspNetCore.All`，请参阅[从 Microsoft.AspNetCore.All 迁移到 Microsoft.AspNetCore.App](xref:fundamentals/metapackage#migrate)。</span><span class="sxs-lookup"><span data-stu-id="5b0c2-153">If your application previously used `Microsoft.AspNetCore.All`, see [Migrating from Microsoft.AspNetCore.All to Microsoft.AspNetCore.App](xref:fundamentals/metapackage#migrate).</span></span>

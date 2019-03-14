---
title: ASP.NET Core 中的 Razor 文件编译
author: rick-anderson
description: 了解 Razor 文件编译在 ASP.NET Core 应用中的发生方式。
monikerRange: '>= aspnetcore-1.1'
ms.author: riande
ms.custom: mvc
ms.date: 02/13/2019
uid: mvc/views/view-compilation
ms.openlocfilehash: 0b6173a7860f5f1d9d11219fbf3f57f76d703031
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57036794"
---
# <a name="razor-file-compilation-in-aspnet-core"></a>ASP.NET Core 中的 Razor 文件编译

作者：[Rick Anderson](https://twitter.com/RickAndMSFT)

::: moniker range="= aspnetcore-1.1"

调用相关的 MVC 视图时，Razor 文件在运行时进行编译。 不支持在生成时发布 Razor 文件。 可以使用预编译工具，在发布时选择编译 Razor 文件并将其与应用一起部署。

::: moniker-end

::: moniker range="= aspnetcore-2.0"

调用相关的 Razor 页和 MVC 视图时，Razor 文件在运行时进行编译。 不支持在生成时发布 Razor 文件。 可以使用预编译工具，在发布时选择编译 Razor 文件并将其与应用一起部署。

::: moniker-end

::: moniker range=">= aspnetcore-2.1 <= aspnetcore-2.2"

调用相关的 Razor 页和 MVC 视图时，Razor 文件在运行时进行编译。 在生成时和发布时使用 [Razor SDK](xref:razor-pages/sdk) 编译 Razor 文件。

::: moniker-end

::: moniker range=">= aspnetcore-3.0"

在生成时和发布时使用 [Razor SDK](xref:razor-pages/sdk) 编译 Razor 文件。 通过配置应用程序，可以选择启用运行时编译

::: moniker-end

## <a name="razor-compilation"></a>Razor 编译

::: moniker range=">= aspnetcore-3.0"
Razor SDK 默认启用 Razor 文件的生成时和发布时编译。 启用后，运行时编译将补充生成时编译，允许更新 Razor 文件（如果对其进行编辑）。

::: moniker-end

::: moniker range=">= aspnetcore-2.1 <= aspnetcore-2.2"

Razor SDK 默认启用 Razor 文件的生成时和发布时编译。 Razor 文件更新后，支持在生成时编辑这些文件。 默认情况下，只有编译 Razor 文件所需的编译的 Views.dll（而非 .cshtml）文件或引用程序集随应用一起部署。

> [!IMPORTANT]
> 已弃用预编译工具，并且将在 ASP.NET Core 3.0 中删除该工具。 建议迁移到 [Razor Sdk](xref:razor-pages/sdk)。
>
> 仅当项目文件中未设置特定于预编译的属性时，Razor SDK 才有效。 例如，通过将 .csproj 文件的 `MvcRazorCompileOnPublish` 属性设置为 `true` 来禁用 Razor SDK。

::: moniker-end

::: moniker range="= aspnetcore-2.0"

如果项目面向 .NET Framework，请安装 [Microsoft.AspNetCore.Mvc.Razor.ViewCompilation](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.Razor.ViewCompilation/) NuGet 包：

[!code-xml[](view-compilation/sample/DotNetFrameworkProject.csproj?name=snippet_ViewCompilationPackage)]

如果项目面向 .NET Core，则无需进行任何更改。

默认情况下，ASP.NET Core 2.x 项目模板将 `MvcRazorCompileOnPublish` 属性隐式设置为 `true`。 因此，可以从 .csproj 文件中安全地删除此元素。

> [!IMPORTANT]
> 已弃用预编译工具，并且将在 ASP.NET Core 3.0 中删除该工具。 建议迁移到 [Razor Sdk](xref:razor-pages/sdk)。
>
> 在 ASP.NET Core 2.0 中执行[独立部署 (SCD)](/dotnet/core/deploying/#self-contained-deployments-scd) 时，无法使用 Razor 文件预编译。

::: moniker-end

::: moniker range="= aspnetcore-1.1"

将 `MvcRazorCompileOnPublish` 属性设置为 `true`，然后安装 [Microsoft.AspNetCore.Mvc.Razor.ViewCompilation](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.Razor.ViewCompilation/) NuGet 包。 以下 .csproj 示例突出显示了这些设置：

[!code-xml[](view-compilation/sample/MvcRazorCompileOnPublish.csproj?highlight=4,10)]

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

使用 [.NET Core CLI 发布命令](/dotnet/core/tools/dotnet-publish)，让应用做好[框架依赖型部署](/dotnet/core/deploying/#framework-dependent-deployments-fdd)的准备。 例如，在项目根目录中执行以下命令：

```console
dotnet publish -c Release
```

预编译成功后，将生成包含已编译 Razor 文件的 <project_name>.PrecompiledViews.dll 文件。 例如，以下屏幕截图描述了 WebApplication1.PrecompiledViews.dll 中 Index.cshtml 的内容：

![DLL 中的 Razor 视图](view-compilation/_static/razor-views-in-dll.png)

::: moniker-end

## <a name="runtime-compilation"></a>运行时编译

::: moniker range="= aspnetcore-2.1"

通过 Razor 文件的运行时编译补充生成时编译。 当 .cshtml 文件的内容发生更改时，ASP.NET Core MVC 将重新编译 Razor 文件。

::: moniker-end

::: moniker range="= aspnetcore-2.2"

通过 Razor 文件的运行时编译补充生成时编译。 <xref:Microsoft.AspNetCore.Mvc.Razor.RazorViewEngineOptions> <xref:Microsoft.AspNetCore.Mvc.Razor.RazorViewEngineOptions.AllowRecompilingViewsOnFileChange> 获取或设置一个值，该值确定当磁盘上的文件发生更改时是否重新编译和更新 Razor 文件（Razor 视图和 Razor Pages）。

对于以下项，默认值为 `true`：

* 将应用的兼容性版本设置为 <xref:Microsoft.AspNetCore.Mvc.CompatibilityVersion.Version_2_1> 或更早版本
* 将应用的兼容性版本设置为 <xref:Microsoft.AspNetCore.Mvc.CompatibilityVersion.Version_2_2> 或更高版本，并且应用已在开发环境 <xref:Microsoft.AspNetCore.Hosting.HostingEnvironmentExtensions.IsDevelopment*> 中。 换句话说，除非明确设置 <xref:Microsoft.AspNetCore.Mvc.Razor.RazorViewEngineOptions.AllowRecompilingViewsOnFileChange>，否则 Razor 文件不会在非开发环境中重新编译。

有关设置应用的兼容性版本的指导和示例，请参阅 <xref:mvc/compatibility-version>。

::: moniker-end

::: moniker range=">= aspnetcore-3.0"

使用 `Microsoft.AspNetCore.Mvc.Razor.RuntimeCompilation` 包启用运行时编译。 要启用运行时编译，应用必须

* 安装 [Microsoft.AspNetCore.Mvc.Razor.RuntimeCompilation](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.Razor.RuntimeCompilation/) NuGet 包。
* 更新应用程序的 `ConfigureServices` 以包含对 `AddMvcRazorRuntimeCompilation` 的调用：

```csharp
services
    .AddMvc()
    .AddMvcRazorRuntimeCompilation()
```

要使运行时编译在部署时起作用，应用必须另外修改其项目文件以将 `PreserveCompilationReferences` 设置为 `true`。
[!code-xml[](view-compilation/sample/RuntimeCompilation.csproj?highlight=3)]

::: moniker-end

## <a name="additional-resources"></a>其他资源

::: moniker range="= aspnetcore-1.1"

* <xref:mvc/views/overview>

::: moniker-end

::: moniker range="= aspnetcore-2.0"

* <xref:razor-pages/index>
* <xref:mvc/views/overview>

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

* <xref:razor-pages/index>
* <xref:mvc/views/overview>
* <xref:razor-pages/sdk>

::: moniker-end

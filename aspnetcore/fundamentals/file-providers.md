---
title: ASP.NET Core 中的文件提供程序
author: guardrex
description: 了解 ASP.NET Core 如何通过文件提供程序来抽象化文件系统访问。
ms.author: riande
ms.custom: mvc
ms.date: 08/01/2018
uid: fundamentals/file-providers
ms.openlocfilehash: 5d0d46ba82cd84e48e5a9b23d6d330d8888beb41
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57042714"
---
# <a name="file-providers-in-aspnet-core"></a><span data-ttu-id="9a1bf-103">ASP.NET Core 中的文件提供程序</span><span class="sxs-lookup"><span data-stu-id="9a1bf-103">File Providers in ASP.NET Core</span></span>

<span data-ttu-id="9a1bf-104">作者：[Steve Smith](https://ardalis.com/) 和 [Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="9a1bf-104">By [Steve Smith](https://ardalis.com/) and [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="9a1bf-105">ASP.NET Core 通过文件提供程序来抽象化文件系统访问。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-105">ASP.NET Core abstracts file system access through the use of File Providers.</span></span> <span data-ttu-id="9a1bf-106">在 ASP.NET Core 框架中使用文件提供程序：</span><span class="sxs-lookup"><span data-stu-id="9a1bf-106">File Providers are used throughout the ASP.NET Core framework:</span></span>

* <span data-ttu-id="9a1bf-107">[IHostingEnvironment](/dotnet/api/microsoft.extensions.hosting.ihostingenvironment) 将应用的内容根和 Web 根作为 `IFileProvider` 类型公开。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-107">[IHostingEnvironment](/dotnet/api/microsoft.extensions.hosting.ihostingenvironment) exposes the app's content root and web root as `IFileProvider` types.</span></span>
* <span data-ttu-id="9a1bf-108">[静态文件中间件](xref:fundamentals/static-files)使用文件提供程序来查找静态文件。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-108">[Static File Middleware](xref:fundamentals/static-files) uses File Providers to locate static files.</span></span>
* <span data-ttu-id="9a1bf-109">[Razor](xref:mvc/views/razor) 使用文件提供程序来查找页面和视图。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-109">[Razor](xref:mvc/views/razor) uses File Providers to locate pages and views.</span></span>
* <span data-ttu-id="9a1bf-110">.NET Core 工具使用文件提供程序和 glob 模式来指定应该发布哪些文件。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-110">.NET Core tooling uses File Providers and glob patterns to specify which files should be published.</span></span>

<span data-ttu-id="9a1bf-111">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/file-providers/samples)（[如何下载](xref:index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="9a1bf-111">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/file-providers/samples) ([how to download](xref:index#how-to-download-a-sample))</span></span>

## <a name="file-provider-interfaces"></a><span data-ttu-id="9a1bf-112">文件提供程序接口</span><span class="sxs-lookup"><span data-stu-id="9a1bf-112">File Provider interfaces</span></span>

<span data-ttu-id="9a1bf-113">主接口为 [IFileProvider](/dotnet/api/microsoft.extensions.fileproviders.ifileprovider)。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-113">The primary interface is [IFileProvider](/dotnet/api/microsoft.extensions.fileproviders.ifileprovider).</span></span> <span data-ttu-id="9a1bf-114">`IFileProvider` 公开方法以实现以下目的：</span><span class="sxs-lookup"><span data-stu-id="9a1bf-114">`IFileProvider` exposes methods to:</span></span>

* <span data-ttu-id="9a1bf-115">获取文件信息 ([IFileInfo](/dotnet/api/microsoft.extensions.fileproviders.ifileinfo))。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-115">Obtain file information ([IFileInfo](/dotnet/api/microsoft.extensions.fileproviders.ifileinfo)).</span></span>
* <span data-ttu-id="9a1bf-116">获取目录信息 ([IDirectoryContents](/dotnet/api/microsoft.extensions.fileproviders.idirectorycontents))。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-116">Obtain directory information ([IDirectoryContents](/dotnet/api/microsoft.extensions.fileproviders.idirectorycontents)).</span></span>
* <span data-ttu-id="9a1bf-117">设置更改通知（使用 [IChangeToken](/dotnet/api/microsoft.extensions.primitives.ichangetoken)）。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-117">Set up change notifications (using an [IChangeToken](/dotnet/api/microsoft.extensions.primitives.ichangetoken)).</span></span>

<span data-ttu-id="9a1bf-118">`IFileInfo` 提供用于处理文件的方法和属性：</span><span class="sxs-lookup"><span data-stu-id="9a1bf-118">`IFileInfo` provides methods and properties for working with files:</span></span>

* [<span data-ttu-id="9a1bf-119">Exists</span><span class="sxs-lookup"><span data-stu-id="9a1bf-119">Exists</span></span>](/dotnet/api/microsoft.extensions.fileproviders.ifileinfo.exists)
* [<span data-ttu-id="9a1bf-120">IsDirectory</span><span class="sxs-lookup"><span data-stu-id="9a1bf-120">IsDirectory</span></span>](/dotnet/api/microsoft.extensions.fileproviders.ifileinfo.isdirectory)
* [<span data-ttu-id="9a1bf-121">名称</span><span class="sxs-lookup"><span data-stu-id="9a1bf-121">Name</span></span>](/dotnet/api/microsoft.extensions.fileproviders.ifileinfo.name)
* <span data-ttu-id="9a1bf-122">[Length](/dotnet/api/microsoft.extensions.fileproviders.ifileinfo.length)（以字节为单位）</span><span class="sxs-lookup"><span data-stu-id="9a1bf-122">[Length](/dotnet/api/microsoft.extensions.fileproviders.ifileinfo.length) (in bytes)</span></span>
* <span data-ttu-id="9a1bf-123">[LastModified](/dotnet/api/microsoft.extensions.fileproviders.ifileinfo.lastmodified) 日期</span><span class="sxs-lookup"><span data-stu-id="9a1bf-123">[LastModified](/dotnet/api/microsoft.extensions.fileproviders.ifileinfo.lastmodified) date</span></span>

<span data-ttu-id="9a1bf-124">可以使用 [IFileInfo.CreateReadStream](/dotnet/api/microsoft.extensions.fileproviders.ifileinfo.createreadstream) 方法从文件读取内容。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-124">You can read from the file using the [IFileInfo.CreateReadStream](/dotnet/api/microsoft.extensions.fileproviders.ifileinfo.createreadstream) method.</span></span>

<span data-ttu-id="9a1bf-125">示例应用演示了如何在 `Startup.ConfigureServices` 中配置文件提供程序，以便通过[依赖关系注入](xref:fundamentals/dependency-injection)在应用中使用。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-125">The sample app demonstrates how to configure a File Provider in `Startup.ConfigureServices` for use throughout the app via [dependency injection](xref:fundamentals/dependency-injection).</span></span>

## <a name="file-provider-implementations"></a><span data-ttu-id="9a1bf-126">文件提供程序实现</span><span class="sxs-lookup"><span data-stu-id="9a1bf-126">File Provider implementations</span></span>

<span data-ttu-id="9a1bf-127">`IFileProvider` 有三种实现。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-127">Three implementations of `IFileProvider` are available.</span></span>

::: moniker range=">= aspnetcore-2.0"

| <span data-ttu-id="9a1bf-128">实现</span><span class="sxs-lookup"><span data-stu-id="9a1bf-128">Implementation</span></span> | <span data-ttu-id="9a1bf-129">描述</span><span class="sxs-lookup"><span data-stu-id="9a1bf-129">Description</span></span> |
| -------------- | ----------- |
| [<span data-ttu-id="9a1bf-130">PhysicalFileProvider</span><span class="sxs-lookup"><span data-stu-id="9a1bf-130">PhysicalFileProvider</span></span>](#physicalfileprovider) | <span data-ttu-id="9a1bf-131">物理提供程序用于访问系统的物理文件。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-131">The physical provider is used to access the system's physical files.</span></span> |
| [<span data-ttu-id="9a1bf-132">ManifestEmbeddedFileProvider</span><span class="sxs-lookup"><span data-stu-id="9a1bf-132">ManifestEmbeddedFileProvider</span></span>](#manifestembeddedfileprovider) | <span data-ttu-id="9a1bf-133">清单嵌入式提供程序用于访问程序集中嵌入的文件。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-133">The manifest embedded provider is used to access files embedded in assemblies.</span></span> |
| [<span data-ttu-id="9a1bf-134">CompositeFileProvider</span><span class="sxs-lookup"><span data-stu-id="9a1bf-134">CompositeFileProvider</span></span>](#compositefileprovider) | <span data-ttu-id="9a1bf-135">复合式提供程序提供对一个或多个其他提供程序中的文件和目录的合并访问。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-135">The composite provider is used to provide combined access to files and directories from one or more other providers.</span></span> |

::: moniker-end

::: moniker range="< aspnetcore-2.0"

| <span data-ttu-id="9a1bf-136">实现</span><span class="sxs-lookup"><span data-stu-id="9a1bf-136">Implementation</span></span> | <span data-ttu-id="9a1bf-137">描述</span><span class="sxs-lookup"><span data-stu-id="9a1bf-137">Description</span></span> |
| -------------- | ----------- |
| [<span data-ttu-id="9a1bf-138">PhysicalFileProvider</span><span class="sxs-lookup"><span data-stu-id="9a1bf-138">PhysicalFileProvider</span></span>](#physicalfileprovider) | <span data-ttu-id="9a1bf-139">物理提供程序用于访问系统的物理文件。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-139">The physical provider is used to access the system's physical files.</span></span> |
| [<span data-ttu-id="9a1bf-140">EmbeddedFileProvider</span><span class="sxs-lookup"><span data-stu-id="9a1bf-140">EmbeddedFileProvider</span></span>](#embeddedfileprovider) | <span data-ttu-id="9a1bf-141">嵌入式提供程序用于访问嵌入在程序集中的文件。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-141">The embedded provider is used to access files embedded in assemblies.</span></span> |
| [<span data-ttu-id="9a1bf-142">CompositeFileProvider</span><span class="sxs-lookup"><span data-stu-id="9a1bf-142">CompositeFileProvider</span></span>](#compositefileprovider) | <span data-ttu-id="9a1bf-143">复合式提供程序提供对一个或多个其他提供程序中的文件和目录的合并访问。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-143">The composite provider is used to provide combined access to files and directories from one or more other providers.</span></span> |

::: moniker-end

### <a name="physicalfileprovider"></a><span data-ttu-id="9a1bf-144">PhysicalFileProvider</span><span class="sxs-lookup"><span data-stu-id="9a1bf-144">PhysicalFileProvider</span></span>

<span data-ttu-id="9a1bf-145">[PhysicalFileProvider](/dotnet/api/microsoft.extensions.fileproviders.physicalfileprovider) 提供对物理文件系统的访问。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-145">The [PhysicalFileProvider](/dotnet/api/microsoft.extensions.fileproviders.physicalfileprovider) provides access to the physical file system.</span></span> <span data-ttu-id="9a1bf-146">`PhysicalFileProvider` 使用（物理提供程序的）[System.IO.File](/dotnet/api/system.io.file) 类型并将所有路径范围限制到目录及其子目录。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-146">`PhysicalFileProvider` uses the [System.IO.File](/dotnet/api/system.io.file) type (for the physical provider) and scopes all paths to a directory and its children.</span></span> <span data-ttu-id="9a1bf-147">此范围界定可防止访问指定目录和子目录之外的文件系统。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-147">This scoping prevents access to the file system outside of the specified directory and its children.</span></span> <span data-ttu-id="9a1bf-148">实例化此提供程序时，必须提供目录路径并将其作为使用提供程序发出的所有请求的基路径。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-148">When instantiating this provider, a directory path is required and serves as the base path for all requests made using the provider.</span></span> <span data-ttu-id="9a1bf-149">可以直接实例化 `PhysicalFileProvider` 提供程序，也可以通过[依赖关系注入](xref:fundamentals/dependency-injection)请求构造函数中的 `IFileProvider`。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-149">You can instantiate a `PhysicalFileProvider` provider directly, or you can request an `IFileProvider` in a constructor through [dependency injection](xref:fundamentals/dependency-injection).</span></span>

<span data-ttu-id="9a1bf-150">**静态类型**</span><span class="sxs-lookup"><span data-stu-id="9a1bf-150">**Static types**</span></span>

<span data-ttu-id="9a1bf-151">下面的代码演示如何创建 `PhysicalFileProvider` 并用它来获取目录内容和文件信息：</span><span class="sxs-lookup"><span data-stu-id="9a1bf-151">The following code shows how to create a `PhysicalFileProvider` and use it to obtain directory contents and file information:</span></span>

```csharp
var provider = new PhysicalFileProvider(applicationRoot);
var contents = provider.GetDirectoryContents(string.Empty);
var fileInfo = provider.GetFileInfo("wwwroot/js/site.js");
```

<span data-ttu-id="9a1bf-152">前面的示例中的类型：</span><span class="sxs-lookup"><span data-stu-id="9a1bf-152">Types in the preceding example:</span></span>

* <span data-ttu-id="9a1bf-153">`provider` 是 `IFileProvider`。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-153">`provider` is an `IFileProvider`.</span></span>
* <span data-ttu-id="9a1bf-154">`contents` 是 `IDirectoryContents`。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-154">`contents` is an `IDirectoryContents`.</span></span>
* <span data-ttu-id="9a1bf-155">`fileInfo` 是 `IFileInfo`。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-155">`fileInfo` is an `IFileInfo`.</span></span>

<span data-ttu-id="9a1bf-156">文件提供程序可用于循环访问 `applicationRoot` 指定的目录或调用 `GetFileInfo` 来获取文件信息。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-156">The File Provider can be used to iterate through the directory specified by `applicationRoot` or call `GetFileInfo` to obtain a file's information.</span></span> <span data-ttu-id="9a1bf-157">该文件提供程序无法访问 `applicationRoot` 目录外部的任何内容。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-157">The File Provider has no access outside of the `applicationRoot` directory.</span></span>

<span data-ttu-id="9a1bf-158">示例应用使用 [IHostingEnvironment.ContentRootFileProvider](/dotnet/api/microsoft.extensions.hosting.ihostingenvironment.contentrootfileprovider) 在应用的 `Startup.ConfigureServices` 类中创建提供程序：</span><span class="sxs-lookup"><span data-stu-id="9a1bf-158">The sample app creates the provider in the app's `Startup.ConfigureServices` class using [IHostingEnvironment.ContentRootFileProvider](/dotnet/api/microsoft.extensions.hosting.ihostingenvironment.contentrootfileprovider):</span></span>

```csharp
var physicalProvider = _env.ContentRootFileProvider;
```

<span data-ttu-id="9a1bf-159">**使用依赖关系注入获取文件提供程序类型**</span><span class="sxs-lookup"><span data-stu-id="9a1bf-159">**Obtain File Provider types with dependency injection**</span></span>

<span data-ttu-id="9a1bf-160">将提供程序注入任何类构造函数，并将其分配给本地字段。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-160">Inject the provider into any class constructor and assign it to a local field.</span></span> <span data-ttu-id="9a1bf-161">在整个类的方法中使用该字段来访问文件。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-161">Use the field throughout the class's methods to access files.</span></span>

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="9a1bf-162">在示例应用中，`IndexModel` 类接收 `IFileProvider` 实例，获取应用的基路径的目录内容。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-162">In the sample app, the `IndexModel` class receives an `IFileProvider` instance to obtain directory contents for the app's base path.</span></span>

<span data-ttu-id="9a1bf-163">Pages/Index.cshtml.cs：</span><span class="sxs-lookup"><span data-stu-id="9a1bf-163">*Pages/Index.cshtml.cs*:</span></span>

[!code-csharp[](file-providers/samples/2.x/FileProviderSample/Pages/Index.cshtml.cs?name=snippet1)]

<span data-ttu-id="9a1bf-164">在页中循环访问 `IDirectoryContents`。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-164">The `IDirectoryContents` are iterated in the page.</span></span>

<span data-ttu-id="9a1bf-165">Pages/Index.cshtml：</span><span class="sxs-lookup"><span data-stu-id="9a1bf-165">*Pages/Index.cshtml*:</span></span>

[!code-cshtml[](file-providers/samples/2.x/FileProviderSample/Pages/Index.cshtml?name=snippet1)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="9a1bf-166">在示例应用中，`HomeController` 类接收 `IFileProvider` 实例，获取应用的基路径的目录内容。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-166">In the sample app, the `HomeController` class receives an `IFileProvider` instance to obtain directory contents for the app's base path.</span></span>

<span data-ttu-id="9a1bf-167">Controllers/HomeController.cs：</span><span class="sxs-lookup"><span data-stu-id="9a1bf-167">*Controllers/HomeController.cs*:</span></span>

[!code-csharp[](file-providers/samples/1.x/FileProviderSample/Controllers/HomeController.cs?name=snippet1)]

<span data-ttu-id="9a1bf-168">在视图中循环访问 `IDirectoryContents`。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-168">The `IDirectoryContents` are iterated in the view.</span></span>

<span data-ttu-id="9a1bf-169">Views/Home/Index.cshtml：</span><span class="sxs-lookup"><span data-stu-id="9a1bf-169">*Views/Home/Index.cshtml*:</span></span>

[!code-cshtml[](file-providers/samples/1.x/FileProviderSample/Views/Home/Index.cshtml?name=snippet1)]

::: moniker-end

::: moniker range=">= aspnetcore-2.0"

### <a name="manifestembeddedfileprovider"></a><span data-ttu-id="9a1bf-170">ManifestEmbeddedFileProvider</span><span class="sxs-lookup"><span data-stu-id="9a1bf-170">ManifestEmbeddedFileProvider</span></span>

<span data-ttu-id="9a1bf-171">[ManifestEmbeddedFileProvider](/dotnet/api/microsoft.extensions.fileproviders.manifestembeddedfileprovider) 用于访问程序集内嵌入的文件。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-171">The [ManifestEmbeddedFileProvider](/dotnet/api/microsoft.extensions.fileproviders.manifestembeddedfileprovider) is used to access files embedded within assemblies.</span></span> <span data-ttu-id="9a1bf-172">`ManifestEmbeddedFileProvider` 使用编译到程序集中的某个清单来重建嵌入的文件的原始路径。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-172">The `ManifestEmbeddedFileProvider` uses a manifest compiled into the assembly to reconstruct the original paths of the embedded files.</span></span>

> [!NOTE]
> <span data-ttu-id="9a1bf-173">ASP.NET Core 2.1 或更高版本中提供了 `ManifestEmbeddedFileProvider`。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-173">The `ManifestEmbeddedFileProvider` is available in ASP.NET Core 2.1 or later.</span></span> <span data-ttu-id="9a1bf-174">若要访问在 ASP.NET Core 2.0 或更早版本 的程序集中嵌入的文件，请参阅[本主题的 ASP.NET Core 1.x 版本](/aspnet/core/fundamentals/file-providers?view=aspnetcore-1.1)。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-174">To access files embedded in assemblies in ASP.NET Core 2.0 or earlier, see the [ASP.NET Core 1.x version of this topic](/aspnet/core/fundamentals/file-providers?view=aspnetcore-1.1).</span></span>

<span data-ttu-id="9a1bf-175">若要生成嵌入的文件清单，请将 `<GenerateEmbeddedFilesManifest>` 属性设置为 `true`。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-175">To generate a manifest of the embedded files, set the `<GenerateEmbeddedFilesManifest>` property to `true`.</span></span> <span data-ttu-id="9a1bf-176">指定要使用 [&lt;EmbeddedResource&gt;](/dotnet/core/tools/csproj#default-compilation-includes-in-net-core-projects) 嵌入的文件：</span><span class="sxs-lookup"><span data-stu-id="9a1bf-176">Specify the files to embed with [&lt;EmbeddedResource&gt;](/dotnet/core/tools/csproj#default-compilation-includes-in-net-core-projects):</span></span>

[!code-csharp[](file-providers/samples/2.x/FileProviderSample/FileProviderSample.csproj?highlight=5,13)]

<span data-ttu-id="9a1bf-177">使用 [glob 模式](#glob-patterns)指定要嵌入到程序集中的一个或多个文件。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-177">Use [glob patterns](#glob-patterns) to specify one or more files to embed into the assembly.</span></span>

<span data-ttu-id="9a1bf-178">示例应用创建 `ManifestEmbeddedFileProvider` 并将当前正在执行的程序集传递给其构造函数。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-178">The sample app creates an `ManifestEmbeddedFileProvider` and passes the currently executing assembly to its constructor.</span></span>

<span data-ttu-id="9a1bf-179">*Startup.cs*：</span><span class="sxs-lookup"><span data-stu-id="9a1bf-179">*Startup.cs*:</span></span>

```csharp
var manifestEmbeddedProvider = 
    new ManifestEmbeddedFileProvider(Assembly.GetEntryAssembly());
```

<span data-ttu-id="9a1bf-180">其他重载使你能够：</span><span class="sxs-lookup"><span data-stu-id="9a1bf-180">Additional overloads allow you to:</span></span>

* <span data-ttu-id="9a1bf-181">指定相对文件路径。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-181">Specify a relative file path.</span></span>
* <span data-ttu-id="9a1bf-182">将文件范围限制到上次修改日期。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-182">Scope files to a last modified date.</span></span>
* <span data-ttu-id="9a1bf-183">为包含嵌入文件清单的嵌入资源命名。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-183">Name the embedded resource containing the embedded file manifest.</span></span>

| <span data-ttu-id="9a1bf-184">重载</span><span class="sxs-lookup"><span data-stu-id="9a1bf-184">Overload</span></span> | <span data-ttu-id="9a1bf-185">描述</span><span class="sxs-lookup"><span data-stu-id="9a1bf-185">Description</span></span> |
| -------- | ----------- |
| [<span data-ttu-id="9a1bf-186">ManifestEmbeddedFileProvider(Assembly, String)</span><span class="sxs-lookup"><span data-stu-id="9a1bf-186">ManifestEmbeddedFileProvider(Assembly, String)</span></span>](/dotnet/api/microsoft.extensions.fileproviders.manifestembeddedfileprovider.-ctor#Microsoft_Extensions_FileProviders_ManifestEmbeddedFileProvider__ctor_System_Reflection_Assembly_System_String_) | <span data-ttu-id="9a1bf-187">接受一个可选的 `root` 相对路径参数。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-187">Accepts an optional `root` relative path parameter.</span></span> <span data-ttu-id="9a1bf-188">指定 `root` 将对 [GetDirectoryContents](/dotnet/api/microsoft.extensions.fileproviders.ifileprovider.getdirectorycontents) 的调用范围限制为提供的路径下的那些资源。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-188">Specify the `root` to scope calls to [GetDirectoryContents](/dotnet/api/microsoft.extensions.fileproviders.ifileprovider.getdirectorycontents) to those resources under the provided path.</span></span> |
| [<span data-ttu-id="9a1bf-189">ManifestEmbeddedFileProvider(Assembly, String, DateTimeOffset)</span><span class="sxs-lookup"><span data-stu-id="9a1bf-189">ManifestEmbeddedFileProvider(Assembly, String, DateTimeOffset)</span></span>](/dotnet/api/microsoft.extensions.fileproviders.manifestembeddedfileprovider.-ctor#Microsoft_Extensions_FileProviders_ManifestEmbeddedFileProvider__ctor_System_Reflection_Assembly_System_String_System_DateTimeOffset_) | <span data-ttu-id="9a1bf-190">接受一个可选的 `root` 相对路径参数和一个 `lastModified` 日期 ([DateTimeOffset](/dotnet/api/system.datetimeoffset)) 参数。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-190">Accepts an optional `root` relative path parameter and a `lastModified` date ([DateTimeOffset](/dotnet/api/system.datetimeoffset)) parameter.</span></span> <span data-ttu-id="9a1bf-191">`lastModified` 日期限制 [IFileProvider](/dotnet/api/microsoft.extensions.fileproviders.ifileprovider) 返回的 [IFileInfo](/dotnet/api/microsoft.extensions.fileproviders.ifileinfo) 实例的上次修改日期范围。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-191">The `lastModified` date scopes the last modification date for the [IFileInfo](/dotnet/api/microsoft.extensions.fileproviders.ifileinfo) instances returned by the [IFileProvider](/dotnet/api/microsoft.extensions.fileproviders.ifileprovider).</span></span> |
| [<span data-ttu-id="9a1bf-192">ManifestEmbeddedFileProvider(Assembly, String, String, DateTimeOffset)</span><span class="sxs-lookup"><span data-stu-id="9a1bf-192">ManifestEmbeddedFileProvider(Assembly, String, String, DateTimeOffset)</span></span>](/dotnet/api/microsoft.extensions.fileproviders.manifestembeddedfileprovider.-ctor#Microsoft_Extensions_FileProviders_ManifestEmbeddedFileProvider__ctor_System_Reflection_Assembly_System_String_System_String_System_DateTimeOffset_) | <span data-ttu-id="9a1bf-193">接受一个可选的 `root` 相对路径、`lastModified` 日期和 `manifestName` 参数。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-193">Accepts an optional `root` relative path, `lastModified` date, and `manifestName` parameters.</span></span> <span data-ttu-id="9a1bf-194">`manifestName` 表示包含清单的嵌入资源的名称。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-194">The `manifestName` represents the name of the embedded resource containing the manifest.</span></span> |

::: moniker-end

::: moniker range="< aspnetcore-2.0"

### <a name="embeddedfileprovider"></a><span data-ttu-id="9a1bf-195">EmbeddedFileProvider</span><span class="sxs-lookup"><span data-stu-id="9a1bf-195">EmbeddedFileProvider</span></span>

<span data-ttu-id="9a1bf-196">[EmbeddedFileProvider](/dotnet/api/microsoft.extensions.fileproviders.embeddedfileprovider)用于访问程序集内嵌入的文件。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-196">The [EmbeddedFileProvider](/dotnet/api/microsoft.extensions.fileproviders.embeddedfileprovider) is used to access files embedded within assemblies.</span></span> <span data-ttu-id="9a1bf-197">指定要使用项目文件中的 [&lt;EmbeddedResource&gt;](/dotnet/core/tools/csproj#default-compilation-includes-in-net-core-projects) 属性嵌入的文件：</span><span class="sxs-lookup"><span data-stu-id="9a1bf-197">Specify the files to embed with the [&lt;EmbeddedResource&gt;](/dotnet/core/tools/csproj#default-compilation-includes-in-net-core-projects) property in the project file:</span></span>

```xml
<ItemGroup>
  <EmbeddedResource Include="Resource.txt" />
</ItemGroup>
```

<span data-ttu-id="9a1bf-198">使用 [glob 模式](#glob-patterns)指定要嵌入到程序集中的一个或多个文件。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-198">Use [glob patterns](#glob-patterns) to specify one or more files to embed into the assembly.</span></span>

<span data-ttu-id="9a1bf-199">示例应用创建 `EmbeddedFileProvider` 并将当前正在执行的程序集传递给其构造函数。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-199">The sample app creates an `EmbeddedFileProvider` and passes the currently executing assembly to its constructor.</span></span>

<span data-ttu-id="9a1bf-200">*Startup.cs*：</span><span class="sxs-lookup"><span data-stu-id="9a1bf-200">*Startup.cs*:</span></span>

```csharp
var embeddedProvider = new EmbeddedFileProvider(Assembly.GetEntryAssembly());
```

<span data-ttu-id="9a1bf-201">嵌入的资源不会公开目录。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-201">Embedded resources don't expose directories.</span></span> <span data-ttu-id="9a1bf-202">而是使用 `.` 分隔符将指向资源的路径（通过其命名空间）嵌入其文件名中。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-202">Rather, the path to the resource (via its namespace) is embedded in its filename using `.` separators.</span></span> <span data-ttu-id="9a1bf-203">在示例应用中，`baseNamespace` 是 `FileProviderSample.`。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-203">In the sample app, the `baseNamespace` is `FileProviderSample.`.</span></span>

<span data-ttu-id="9a1bf-204">[EmbeddedFileProvider(Assembly, String)](/dotnet/api/microsoft.extensions.fileproviders.embeddedfileprovider.-ctor#Microsoft_Extensions_FileProviders_EmbeddedFileProvider__ctor_System_Reflection_Assembly_) 构造函数接受一个可选的 `baseNamespace` 参数。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-204">The [EmbeddedFileProvider(Assembly, String)](/dotnet/api/microsoft.extensions.fileproviders.embeddedfileprovider.-ctor#Microsoft_Extensions_FileProviders_EmbeddedFileProvider__ctor_System_Reflection_Assembly_) constructor accepts an optional `baseNamespace` parameter.</span></span> <span data-ttu-id="9a1bf-205">指定基命名空间，将对 [GetDirectoryContents](/dotnet/api/microsoft.extensions.fileproviders.ifileprovider.getdirectorycontents) 的调用范围限制为提供的命名空间下的那些资源。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-205">Specify the base namespace to scope calls to [GetDirectoryContents](/dotnet/api/microsoft.extensions.fileproviders.ifileprovider.getdirectorycontents) to those resources under the provided namespace.</span></span>

::: moniker-end

### <a name="compositefileprovider"></a><span data-ttu-id="9a1bf-206">CompositeFileProvider</span><span class="sxs-lookup"><span data-stu-id="9a1bf-206">CompositeFileProvider</span></span>

<span data-ttu-id="9a1bf-207">[CompositeFileProvider](/dotnet/api/microsoft.extensions.fileproviders.compositefileprovider) 结合了 `IFileProvider` 实例，以便公开一个接口来处理来自多个提供程序的文件。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-207">The [CompositeFileProvider](/dotnet/api/microsoft.extensions.fileproviders.compositefileprovider) combines `IFileProvider` instances, exposing a single interface for working with files from multiple providers.</span></span> <span data-ttu-id="9a1bf-208">创建 `CompositeFileProvider` 时，将一个或多个 `IFileProvider` 实例传递给其构造函数。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-208">When creating the `CompositeFileProvider`, pass one or more `IFileProvider` instances to its constructor.</span></span>

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="9a1bf-209">在示例应用中，`PhysicalFileProvider` 和 `ManifestEmbeddedFileProvider` 向在应用的服务容器中注册的 `CompositeFileProvider` 提供文件：</span><span class="sxs-lookup"><span data-stu-id="9a1bf-209">In the sample app, a `PhysicalFileProvider` and a `ManifestEmbeddedFileProvider` provide files to a `CompositeFileProvider` registered in the app's service container:</span></span>

[!code-csharp[](file-providers/samples/2.x/FileProviderSample/Startup.cs?name=snippet1)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="9a1bf-210">在示例应用中，`PhysicalFileProvider` 和 `EmbeddedFileProvider` 向在应用的服务容器中注册的 `CompositeFileProvider` 提供文件：</span><span class="sxs-lookup"><span data-stu-id="9a1bf-210">In the sample app, a `PhysicalFileProvider` and an `EmbeddedFileProvider` provide files to a `CompositeFileProvider` registered in the app's service container:</span></span>

[!code-csharp[](file-providers/samples/1.x/FileProviderSample/Startup.cs?name=snippet1)]

::: moniker-end

## <a name="watch-for-changes"></a><span data-ttu-id="9a1bf-211">监视更改</span><span class="sxs-lookup"><span data-stu-id="9a1bf-211">Watch for changes</span></span>

<span data-ttu-id="9a1bf-212">[IFileProvider.Watch](/dotnet/api/microsoft.extensions.fileproviders.ifileprovider.watch) 方法提供了一个方案来监视一个或多个文件或目录是否发生更改。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-212">The [IFileProvider.Watch](/dotnet/api/microsoft.extensions.fileproviders.ifileprovider.watch) method provides a scenario to watch one or more files or directories for changes.</span></span> <span data-ttu-id="9a1bf-213">`Watch` 接受路径字符串，它可以使用 [glob 模式](#glob-patterns)指定多个文件。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-213">`Watch` accepts a path string, which can use [glob patterns](#glob-patterns) to specify multiple files.</span></span> <span data-ttu-id="9a1bf-214">`Watch` 返回 [IChangeToken](/dotnet/api/microsoft.extensions.primitives.ichangetoken)。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-214">`Watch` returns an [IChangeToken](/dotnet/api/microsoft.extensions.primitives.ichangetoken).</span></span> <span data-ttu-id="9a1bf-215">更改令牌会公开以下内容：</span><span class="sxs-lookup"><span data-stu-id="9a1bf-215">The change token exposes:</span></span>

* <span data-ttu-id="9a1bf-216">[HasChanged](/dotnet/api/microsoft.extensions.primitives.ichangetoken.haschanged):一个属性，可以对其进行检查，以确定已发生更改。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-216">[HasChanged](/dotnet/api/microsoft.extensions.primitives.ichangetoken.haschanged): A property that can be inspected to determine if a change has occurred.</span></span>
* <span data-ttu-id="9a1bf-217">[RegisterChangeCallback](/dotnet/api/microsoft.extensions.primitives.ichangetoken.registerchangecallback):当检测到指定的路径字符串的变化时调用。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-217">[RegisterChangeCallback](/dotnet/api/microsoft.extensions.primitives.ichangetoken.registerchangecallback): Called when changes are detected to the specified path string.</span></span> <span data-ttu-id="9a1bf-218">每个更改令牌仅调用其关联的回调来响应单个更改。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-218">Each change token only calls its associated callback in response to a single change.</span></span> <span data-ttu-id="9a1bf-219">若要启用持续监视，请使用 [TaskCompletionSource](/dotnet/api/system.threading.tasks.taskcompletionsource-1)（如下所示）或重新创建 `IChangeToken` 实例以响应更改。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-219">To enable constant monitoring, use a [TaskCompletionSource](/dotnet/api/system.threading.tasks.taskcompletionsource-1) (shown below) or recreate `IChangeToken` instances in response to changes.</span></span>

<span data-ttu-id="9a1bf-220">在示例应用中，WatchConsole 控制台应用配置为每次修改了文本文件时显示一条消息：</span><span class="sxs-lookup"><span data-stu-id="9a1bf-220">In the sample app, the *WatchConsole* console app is configured to display a message whenever a text file is modified:</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](file-providers/samples/2.x/WatchConsole/Program.cs?name=snippet1&highlight=1-2,16,19-20)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](file-providers/samples/1.x/WatchConsole/Program.cs?name=snippet1&highlight=1-2,16,19-20)]

::: moniker-end

<span data-ttu-id="9a1bf-221">某些文件系统（例如 Docker 容器和网络共享）可能无法可靠地发送更改通知。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-221">Some file systems, such as Docker containers and network shares, may not reliably send change notifications.</span></span> <span data-ttu-id="9a1bf-222">将 `DOTNET_USE_POLLING_FILE_WATCHER` 环境变量设置为 `1` 或 `true` 以每隔四秒轮询一次文件系统，确认是否发生更改（不可配置）。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-222">Set the `DOTNET_USE_POLLING_FILE_WATCHER` environment variable to `1` or `true` to poll the file system for changes every four seconds (not configurable).</span></span>

## <a name="glob-patterns"></a><span data-ttu-id="9a1bf-223">glob 模式</span><span class="sxs-lookup"><span data-stu-id="9a1bf-223">Glob patterns</span></span>

<span data-ttu-id="9a1bf-224">文件系统路径使用名为 glob（或通配）模式的通配符模式。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-224">File system paths use wildcard patterns called *glob (or globbing) patterns*.</span></span> <span data-ttu-id="9a1bf-225">使用这些模式指定文件的组。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-225">Specify groups of files with these patterns.</span></span> <span data-ttu-id="9a1bf-226">两个通配符分别是 `*` 和 `**`：</span><span class="sxs-lookup"><span data-stu-id="9a1bf-226">The two wildcard characters are `*` and `**`:</span></span>

**`*`**  
<span data-ttu-id="9a1bf-227">匹配当前文件夹级别的任何内容、任何文件名或任何文件扩展名。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-227">Matches anything at the current folder level, any filename, or any file extension.</span></span> <span data-ttu-id="9a1bf-228">匹配由文件路径中的 `/` 和 `.` 字符终止。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-228">Matches are terminated by `/` and `.` characters in the file path.</span></span>

**`**`**  
<span data-ttu-id="9a1bf-229">匹配多个目录级别的任何内容。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-229">Matches anything across multiple directory levels.</span></span> <span data-ttu-id="9a1bf-230">可用于以递归方式匹配目录层次结构中的许多文件。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-230">Can be used to recursively match many files within a directory hierarchy.</span></span>

<span data-ttu-id="9a1bf-231">**glob 模式示例**</span><span class="sxs-lookup"><span data-stu-id="9a1bf-231">**Glob pattern examples**</span></span>

**`directory/file.txt`**  
<span data-ttu-id="9a1bf-232">匹配特定目录中的特定文件。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-232">Matches a specific file in a specific directory.</span></span>

**`directory/*.txt`**  
<span data-ttu-id="9a1bf-233">匹配特定目录中带 .txt 扩展名的所有文件。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-233">Matches all files with *.txt* extension in a specific directory.</span></span>

**`directory/*/appsettings.json`**  
<span data-ttu-id="9a1bf-234">匹配正好位于“目录”文件夹中下一级目录中的所有 `appsettings.json` 文件。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-234">Matches all `appsettings.json` files in directories exactly one level below the *directory* folder.</span></span>

**`directory/**/*.txt`**  
<span data-ttu-id="9a1bf-235">匹配在“目录”文件夹下任何位置找到的带 .txt 扩展名的所有文件。</span><span class="sxs-lookup"><span data-stu-id="9a1bf-235">Matches all files with *.txt* extension found anywhere under the *directory* folder.</span></span>

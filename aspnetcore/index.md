---
title: ASP.NET Core 简介
author: rick-anderson
description: 获取 ASP.NET Core 的简介，它是一个跨平台的高性能开源框架，用于生成基于云且连接 Internet 的新式应用程序。
ms.author: riande
ms.custom: mvc
ms.date: 02/14/2019
uid: index
---
# <a name="introduction-to-aspnet-core"></a><span data-ttu-id="2ae3c-103">ASP.NET Core 简介</span><span class="sxs-lookup"><span data-stu-id="2ae3c-103">Introduction to ASP.NET Core</span></span>

<span data-ttu-id="2ae3c-104">作者：[Daniel Roth](https://github.com/danroth27)[Rick Anderson](https://twitter.com/RickAndMSFT) 和 [Shaun Luttin](https://twitter.com/dicshaunary)</span><span class="sxs-lookup"><span data-stu-id="2ae3c-104">By [Daniel Roth](https://github.com/danroth27), [Rick Anderson](https://twitter.com/RickAndMSFT), and [Shaun Luttin](https://twitter.com/dicshaunary)</span></span>

<span data-ttu-id="2ae3c-105">ASP.NET Core 是一个跨平台的高性能[开源](https://github.com/aspnet/home)框架，用于生成基于云且连接 Internet 的新式应用程序。</span><span class="sxs-lookup"><span data-stu-id="2ae3c-105">ASP.NET Core is a cross-platform, high-performance, [open-source](https://github.com/aspnet/home) framework for building modern, cloud-based, Internet-connected applications.</span></span> <span data-ttu-id="2ae3c-106">使用 ASP.NET Core，您可以：</span><span class="sxs-lookup"><span data-stu-id="2ae3c-106">With ASP.NET Core, you can:</span></span>

* <span data-ttu-id="2ae3c-107">创建 Web 应用程序和服务、[IoT](https://www.microsoft.com/internet-of-things/) 应用和移动后端。</span><span class="sxs-lookup"><span data-stu-id="2ae3c-107">Build web apps and services, [IoT](https://www.microsoft.com/internet-of-things/) apps, and mobile backends.</span></span>
* <span data-ttu-id="2ae3c-108">在 Windows、macOS 和 Linux 上使用喜爱的开发工具。</span><span class="sxs-lookup"><span data-stu-id="2ae3c-108">Use your favorite development tools on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="2ae3c-109">部署到云或本地。</span><span class="sxs-lookup"><span data-stu-id="2ae3c-109">Deploy to the cloud or on-premises.</span></span>
* <span data-ttu-id="2ae3c-110">在 [.NET Core 或 .NET Framework](/dotnet/articles/standard/choosing-core-framework-server) 上运行。</span><span class="sxs-lookup"><span data-stu-id="2ae3c-110">Run on [.NET Core or .NET Framework](/dotnet/articles/standard/choosing-core-framework-server).</span></span>

## <a name="why-use-aspnet-core"></a><span data-ttu-id="2ae3c-111">为何使用 ASP.NET Core？</span><span class="sxs-lookup"><span data-stu-id="2ae3c-111">Why use ASP.NET Core?</span></span>

<span data-ttu-id="2ae3c-112">数百万开发人员使用过（并将继续使用）[ASP.NET 4.x](/aspnet/overview) 创建 Web 应用。</span><span class="sxs-lookup"><span data-stu-id="2ae3c-112">Millions of developers have used (and continue to use) [ASP.NET 4.x](/aspnet/overview) to create web apps.</span></span> <span data-ttu-id="2ae3c-113">ASP.NET Core 是重新设计的 ASP.NET 4.x，更改了体系结构，形成了更精简的模块化框架。</span><span class="sxs-lookup"><span data-stu-id="2ae3c-113">ASP.NET Core is a redesign of ASP.NET 4.x, with architectural changes that result in a leaner, more modular framework.</span></span>

[!INCLUDE[](~/includes/benefits.md)]

## <a name="build-web-apis-and-web-ui-using-aspnet-core-mvc"></a><span data-ttu-id="2ae3c-114">使用 ASP.NET Core MVC 生成 Web API 和 Web UI</span><span class="sxs-lookup"><span data-stu-id="2ae3c-114">Build web APIs and web UI using ASP.NET Core MVC</span></span>

<span data-ttu-id="2ae3c-115">ASP.NET Core MVC 提供生成 [Web API](xref:tutorials/first-web-api) 和 [Web 应用](xref:tutorials/razor-pages/index)所需的功能：</span><span class="sxs-lookup"><span data-stu-id="2ae3c-115">ASP.NET Core MVC provides features to build [web APIs](xref:tutorials/first-web-api) and [web apps](xref:tutorials/razor-pages/index):</span></span>

* <span data-ttu-id="2ae3c-116">[Model-View-Controller (MVC) 模式](xref:mvc/overview) 使 Web API 和 Web 应用可测试。</span><span class="sxs-lookup"><span data-stu-id="2ae3c-116">The [Model-View-Controller (MVC) pattern](xref:mvc/overview) helps make your web APIs and web apps testable.</span></span>
* <span data-ttu-id="2ae3c-117">[Razor Pages](xref:razor-pages/index) 是基于页面的编程模型，它让 Web UI 的生成更加简单高效。</span><span class="sxs-lookup"><span data-stu-id="2ae3c-117">[Razor Pages](xref:razor-pages/index) is a page-based programming model that makes building web UI easier and more productive.</span></span>
* <span data-ttu-id="2ae3c-118">[Razor 标记](xref:mvc/views/razor)提供了适用于 [Razor 页面](xref:razor-pages/index)和 [MVC 视图](xref:mvc/views/overview)的高效语法。</span><span class="sxs-lookup"><span data-stu-id="2ae3c-118">[Razor markup](xref:mvc/views/razor) provides a productive syntax for [Razor Pages](xref:razor-pages/index) and [MVC views](xref:mvc/views/overview).</span></span>
* <span data-ttu-id="2ae3c-119">[标记帮助程序](xref:mvc/views/tag-helpers/intro)使服务器端代码可以在 Razor 文件中参与创建和呈现 HTML 元素。</span><span class="sxs-lookup"><span data-stu-id="2ae3c-119">[Tag Helpers](xref:mvc/views/tag-helpers/intro) enable server-side code to participate in creating and rendering HTML elements in Razor files.</span></span>
* <span data-ttu-id="2ae3c-120">内置的[多数据格式和内容协商](xref:web-api/advanced/formatting)支持使 Web API 可访问多种客户端，包括浏览器和移动设备。</span><span class="sxs-lookup"><span data-stu-id="2ae3c-120">Built-in support for [multiple data formats and content negotiation](xref:web-api/advanced/formatting) lets your web APIs reach a broad range of clients, including browsers and mobile devices.</span></span>
* <span data-ttu-id="2ae3c-121">[模型绑定](xref:mvc/models/model-binding)自动将 HTTP 请求中的数据映射到操作方法参数。</span><span class="sxs-lookup"><span data-stu-id="2ae3c-121">[Model binding](xref:mvc/models/model-binding) automatically maps data from HTTP requests to action method parameters.</span></span>
* <span data-ttu-id="2ae3c-122">[模型验证](xref:mvc/models/validation)自动执行客户端和服务器端验证。</span><span class="sxs-lookup"><span data-stu-id="2ae3c-122">[Model validation](xref:mvc/models/validation) automatically performs client-side and server-side validation.</span></span>

## <a name="client-side-development"></a><span data-ttu-id="2ae3c-123">客户端开发</span><span class="sxs-lookup"><span data-stu-id="2ae3c-123">Client-side development</span></span>

<span data-ttu-id="2ae3c-124">ASP.NET Core 与常用客户端框架和库（包括 [Razor Components](xref:razor-components/index)、[Angular](xref:spa/angular)、[React](xref:spa/react) 和 [Bootstrap](https://getbootstrap.com/)）无缝集成。</span><span class="sxs-lookup"><span data-stu-id="2ae3c-124">ASP.NET Core integrates seamlessly with popular client-side frameworks and libraries, including [Razor Components](xref:razor-components/index), [Angular](xref:spa/angular), [React](xref:spa/react), and [Bootstrap](https://getbootstrap.com/).</span></span> <span data-ttu-id="2ae3c-125">有关详细信息，请参阅 [Razor Components](xref:razor-components/index) 和“客户端开发”下的相关主题。</span><span class="sxs-lookup"><span data-stu-id="2ae3c-125">For more information, see [Razor Components](xref:razor-components/index) and related topics under *Client-side development*.</span></span>

<a name="target-framework"></a>

## <a name="aspnet-core-targeting-net-framework"></a><span data-ttu-id="2ae3c-126">面向 .NET Framework 的 ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="2ae3c-126">ASP.NET Core targeting .NET Framework</span></span>

<span data-ttu-id="2ae3c-127">ASP.NET Core 2.x 可以面向 .NET Core 或 .NET Framework。</span><span class="sxs-lookup"><span data-stu-id="2ae3c-127">ASP.NET Core 2.x can target .NET Core or .NET Framework.</span></span> <span data-ttu-id="2ae3c-128">面向 .NET Framework 的 ASP.NET Core 应用无法跨平台，它们仅在 Windows 上运行。</span><span class="sxs-lookup"><span data-stu-id="2ae3c-128">ASP.NET Core apps targeting .NET Framework aren't cross-platform&mdash;they run on Windows only.</span></span> <span data-ttu-id="2ae3c-129">通常，ASP.NET Core 2.x 由 [.NET Standard](/dotnet/standard/net-standard) 库组成。</span><span class="sxs-lookup"><span data-stu-id="2ae3c-129">Generally, ASP.NET Core 2.x is made up of [.NET Standard](/dotnet/standard/net-standard) libraries.</span></span> <span data-ttu-id="2ae3c-130">使用 .NET Standard 2.0 编写的应用可在 NET Standard 2.0 支持的任何位置运行。</span><span class="sxs-lookup"><span data-stu-id="2ae3c-130">Apps written with .NET Standard 2.0 run anywhere that .NET Standard 2.0 is supported.</span></span>

<span data-ttu-id="2ae3c-131">与 .NET Standard 2.0 兼容的 .NET Framework 版本支持 ASP.NET Core 2.x：</span><span class="sxs-lookup"><span data-stu-id="2ae3c-131">ASP.NET Core 2.x is supported on .NET Framework versions compatible with .NET Standard 2.0:</span></span>

* <span data-ttu-id="2ae3c-132">强烈建议使用 .NET Framework 4.7.1 及更高版本。</span><span class="sxs-lookup"><span data-stu-id="2ae3c-132">.NET Framework 4.7.1 and later is strongly recommended.</span></span>
* <span data-ttu-id="2ae3c-133">.NET Framework 4.6.1 及更高版本。</span><span class="sxs-lookup"><span data-stu-id="2ae3c-133">.NET Framework 4.6.1 and later.</span></span>

<span data-ttu-id="2ae3c-134">ASP.NET Core 3.0 以及更高版本只能在 .NET Core 中运行。</span><span class="sxs-lookup"><span data-stu-id="2ae3c-134">ASP.NET Core 3.0 and later will only run on .NET Core.</span></span> <span data-ttu-id="2ae3c-135">有关此更改的详细信息，请参阅 [A first look at changes coming in ASP.NET Core 3.0](https://blogs.msdn.microsoft.com/webdev/2018/10/29/a-first-look-at-changes-coming-in-asp-net-core-3-0/)（抢先了解 ASP.NET Core 3.0 即将推出的更改）。</span><span class="sxs-lookup"><span data-stu-id="2ae3c-135">For more details regarding this change, see [A first look at changes coming in ASP.NET Core 3.0](https://blogs.msdn.microsoft.com/webdev/2018/10/29/a-first-look-at-changes-coming-in-asp-net-core-3-0/).</span></span>

<span data-ttu-id="2ae3c-136">面向 .NET Core 有以下几个优势，并且这些优势会随着每次发布增加。</span><span class="sxs-lookup"><span data-stu-id="2ae3c-136">There are several advantages to targeting .NET Core, and these advantages increase with each release.</span></span> <span data-ttu-id="2ae3c-137">与 .NET Framework 相比，.NET Core 的部分优势包括：</span><span class="sxs-lookup"><span data-stu-id="2ae3c-137">Some advantages of .NET Core over .NET Framework include:</span></span>

* <span data-ttu-id="2ae3c-138">跨平台。</span><span class="sxs-lookup"><span data-stu-id="2ae3c-138">Cross-platform.</span></span> <span data-ttu-id="2ae3c-139">在 macOS、Linux 和 Windows 上运行。</span><span class="sxs-lookup"><span data-stu-id="2ae3c-139">Runs on macOS, Linux, and Windows.</span></span>
* <span data-ttu-id="2ae3c-140">增强的性能</span><span class="sxs-lookup"><span data-stu-id="2ae3c-140">Improved performance</span></span>
* <span data-ttu-id="2ae3c-141">并行版本控制</span><span class="sxs-lookup"><span data-stu-id="2ae3c-141">Side-by-side versioning</span></span>
* <span data-ttu-id="2ae3c-142">新 API</span><span class="sxs-lookup"><span data-stu-id="2ae3c-142">New APIs</span></span>
* <span data-ttu-id="2ae3c-143">开源</span><span class="sxs-lookup"><span data-stu-id="2ae3c-143">Open source</span></span>

<span data-ttu-id="2ae3c-144">我们正努力缩小 .NET Framework 与 .NET Core 的 API 差距。</span><span class="sxs-lookup"><span data-stu-id="2ae3c-144">We're working hard to close the API gap from .NET Framework to .NET Core.</span></span> <span data-ttu-id="2ae3c-145">[Windows 兼容性包](/dotnet/core/porting/windows-compat-pack)使数千个仅可在Windows运行的API 可在 .NET Core 中使用。</span><span class="sxs-lookup"><span data-stu-id="2ae3c-145">The [Windows Compatibility Pack](/dotnet/core/porting/windows-compat-pack) made thousands of Windows-only APIs available in .NET Core.</span></span> <span data-ttu-id="2ae3c-146">这些 API 在 .NET Core 1.x 中不可用。</span><span class="sxs-lookup"><span data-stu-id="2ae3c-146">These APIs weren't available in .NET Core 1.x.</span></span>

## <a name="recommended-learning-path"></a><span data-ttu-id="2ae3c-147">推荐的学习路径</span><span class="sxs-lookup"><span data-stu-id="2ae3c-147">Recommended learning path</span></span>

<span data-ttu-id="2ae3c-148">建议使用以下一系列教程和文章来介绍如何开发 ASP.NET Core 应用程序：</span><span class="sxs-lookup"><span data-stu-id="2ae3c-148">We recommend the following sequence of tutorials and articles for an introduction to developing ASP.NET Core apps:</span></span>

1. <span data-ttu-id="2ae3c-149">请按照适用于要开发或维护的应用类型的教程操作：</span><span class="sxs-lookup"><span data-stu-id="2ae3c-149">Follow a tutorial for the type of app you want to develop or maintain:</span></span>

   |<span data-ttu-id="2ae3c-150">应用类型</span><span class="sxs-lookup"><span data-stu-id="2ae3c-150">App type</span></span>  |<span data-ttu-id="2ae3c-151">方案</span><span class="sxs-lookup"><span data-stu-id="2ae3c-151">Scenario</span></span>  |<span data-ttu-id="2ae3c-152">教程</span><span class="sxs-lookup"><span data-stu-id="2ae3c-152">Tutorial</span></span>  |
   |----------|----------|----------|
   |<span data-ttu-id="2ae3c-153">Web 应用</span><span class="sxs-lookup"><span data-stu-id="2ae3c-153">Web app</span></span>       | <span data-ttu-id="2ae3c-154">用于新的开发</span><span class="sxs-lookup"><span data-stu-id="2ae3c-154">For new development</span></span>        |[<span data-ttu-id="2ae3c-155">Razor 页面入门</span><span class="sxs-lookup"><span data-stu-id="2ae3c-155">Get started with Razor Pages</span></span>](xref:tutorials/razor-pages/razor-pages-start) |
   |<span data-ttu-id="2ae3c-156">Web 应用</span><span class="sxs-lookup"><span data-stu-id="2ae3c-156">Web app</span></span>       | <span data-ttu-id="2ae3c-157">用于维护 MVC 应用</span><span class="sxs-lookup"><span data-stu-id="2ae3c-157">For maintaining an MVC app</span></span> |[<span data-ttu-id="2ae3c-158">MVC 入门</span><span class="sxs-lookup"><span data-stu-id="2ae3c-158">Get started with MVC</span></span>](xref:tutorials/first-mvc-app/start-mvc)|
   |<span data-ttu-id="2ae3c-159">Web API</span><span class="sxs-lookup"><span data-stu-id="2ae3c-159">Web API</span></span>       |                            |<span data-ttu-id="2ae3c-160">[创建 Web API](xref:tutorials/first-web-api)\*</span><span class="sxs-lookup"><span data-stu-id="2ae3c-160">[Create a web API](xref:tutorials/first-web-api)\*</span></span>  |
   |<span data-ttu-id="2ae3c-161">实时应用</span><span class="sxs-lookup"><span data-stu-id="2ae3c-161">Real-time app</span></span> |                            |[<span data-ttu-id="2ae3c-162">SignalR 入门</span><span class="sxs-lookup"><span data-stu-id="2ae3c-162">Get started with SignalR</span></span>](xref:tutorials/signalr) |

1. <span data-ttu-id="2ae3c-163">请按照介绍如何进行基本数据访问的教程操作：</span><span class="sxs-lookup"><span data-stu-id="2ae3c-163">Follow a tutorial that shows how to do basic data access:</span></span>

   |<span data-ttu-id="2ae3c-164">方案</span><span class="sxs-lookup"><span data-stu-id="2ae3c-164">Scenario</span></span>  |<span data-ttu-id="2ae3c-165">教程</span><span class="sxs-lookup"><span data-stu-id="2ae3c-165">Tutorial</span></span>  |
   |----------|----------|
   | <span data-ttu-id="2ae3c-166">用于新的开发</span><span class="sxs-lookup"><span data-stu-id="2ae3c-166">For new development</span></span>        |[<span data-ttu-id="2ae3c-167">结合使用 Razor Pages 和 Entity Framework Core</span><span class="sxs-lookup"><span data-stu-id="2ae3c-167">Razor Pages with Entity Framework Core</span></span>](xref:data/ef-rp/intro) |
   | <span data-ttu-id="2ae3c-168">用于维护 MVC 应用</span><span class="sxs-lookup"><span data-stu-id="2ae3c-168">For maintaining an MVC app</span></span> |[<span data-ttu-id="2ae3c-169">结合使用 MVC 和 Entity Framework Core</span><span class="sxs-lookup"><span data-stu-id="2ae3c-169">MVC with Entity Framework Core</span></span>](xref:data/ef-mvc/intro)

1. <span data-ttu-id="2ae3c-170">参阅适用于所有应用类型的 ASP.NET Core 功能的概述：</span><span class="sxs-lookup"><span data-stu-id="2ae3c-170">Read an overview of ASP.NET Core features that apply to all app types:</span></span>

   * [<span data-ttu-id="2ae3c-171">基础知识</span><span class="sxs-lookup"><span data-stu-id="2ae3c-171">Fundamentals</span></span>](xref:fundamentals/index)

1. <span data-ttu-id="2ae3c-172">浏览目录以了解其他感兴趣的主题。</span><span class="sxs-lookup"><span data-stu-id="2ae3c-172">Browse the Table of Contents for other topics of interest.</span></span>

<span data-ttu-id="2ae3c-173">\* 新增了[在浏览器中完全遵循的 Web API 教程](https://docs.microsoft.com/learn/modules/build-web-api-net-core)，无需安装本地 IDE。</span><span class="sxs-lookup"><span data-stu-id="2ae3c-173">\* There is a new [web API tutorial that you follow entirely in the browser](https://docs.microsoft.com/learn/modules/build-web-api-net-core), no local IDE installation required.</span></span>  <span data-ttu-id="2ae3c-174">代码在 [Azure Cloud Shell](https://azure.microsoft.com/features/cloud-shell/) 中运行，并且 [curl](https://curl.haxx.se/) 用于测试。</span><span class="sxs-lookup"><span data-stu-id="2ae3c-174">The code runs in an [Azure Cloud Shell](https://azure.microsoft.com/features/cloud-shell/), and [curl](https://curl.haxx.se/) is used for testing.</span></span>

## <a name="how-to-download-a-sample"></a><span data-ttu-id="2ae3c-175">如何下载示例</span><span class="sxs-lookup"><span data-stu-id="2ae3c-175">How to download a sample</span></span>

<span data-ttu-id="2ae3c-176">很多文章和教程中都包含有示例代码链接。</span><span class="sxs-lookup"><span data-stu-id="2ae3c-176">Many of the articles and tutorials include links to sample code.</span></span>

1. <span data-ttu-id="2ae3c-177">[下载 ASP.NET 存储库 zip 文件](https://codeload.github.com/aspnet/Docs/zip/master)。</span><span class="sxs-lookup"><span data-stu-id="2ae3c-177">[Download the ASP.NET repository zip file](https://codeload.github.com/aspnet/Docs/zip/master).</span></span>
1. <span data-ttu-id="2ae3c-178">解压缩 Docs-master.zip 文件。</span><span class="sxs-lookup"><span data-stu-id="2ae3c-178">Unzip the *Docs-master.zip* file.</span></span>
1. <span data-ttu-id="2ae3c-179">使用示例链接中的 URL 帮助你导航到示例目录。</span><span class="sxs-lookup"><span data-stu-id="2ae3c-179">Use the URL in the sample link to help you navigate to the sample directory.</span></span>

### <a name="preprocessor-directives-in-sample-code"></a><span data-ttu-id="2ae3c-180">示例代码中的预处理器指令</span><span class="sxs-lookup"><span data-stu-id="2ae3c-180">Preprocessor directives in sample code</span></span>

<span data-ttu-id="2ae3c-181">为了演示多个方案，示例应用将使用 `#define` 和 `#if-#else/#elif-#endif` C# 语句选择性地编译和运行不同的示例代码段。</span><span class="sxs-lookup"><span data-stu-id="2ae3c-181">To demonstrate multiple scenarios, sample apps use the `#define` and `#if-#else/#elif-#endif` C# statements to selectively compile and run different sections of sample code.</span></span> <span data-ttu-id="2ae3c-182">对于那些利用此方法的示例，请将 C# 文件顶部的 `#define` 语句设置为与你想要运行的方案相关联的符号。</span><span class="sxs-lookup"><span data-stu-id="2ae3c-182">For those samples that make use of this approach, set the `#define` statement at the top of the C# files to the symbol associated with the scenario that you want to run.</span></span> <span data-ttu-id="2ae3c-183">一些示例要求在多个文件的顶部设置符号才能运行方案。</span><span class="sxs-lookup"><span data-stu-id="2ae3c-183">Some samples require setting the symbol at the top of multiple files in order to run a scenario.</span></span>

<span data-ttu-id="2ae3c-184">例如，以下 `#define` 符号列表指示四个方案可用（每个符号一个方案）。</span><span class="sxs-lookup"><span data-stu-id="2ae3c-184">For example, the following `#define` symbol list indicates that four scenarios are available (one scenario per symbol).</span></span> <span data-ttu-id="2ae3c-185">当前示例配置运行 `TemplateCode` 方案：</span><span class="sxs-lookup"><span data-stu-id="2ae3c-185">The current sample configuration runs the `TemplateCode` scenario:</span></span>

```csharp
#define TemplateCode // or LogFromMain or ExpandDefault or FilterInCode
```

<span data-ttu-id="2ae3c-186">若要更改示例以运行 `ExpandDefault` 方案，请定义 `ExpandDefault` 符号并保留剩余的符号处于被注释掉的状态：</span><span class="sxs-lookup"><span data-stu-id="2ae3c-186">To change the sample to run the `ExpandDefault` scenario, define the `ExpandDefault` symbol and leave the remaining symbols commented-out:</span></span>

```csharp
#define ExpandDefault // TemplateCode or LogFromMain or FilterInCode
```

<span data-ttu-id="2ae3c-187">若要详细了解如何使用 [C# 预处理器指令](/dotnet/csharp/language-reference/preprocessor-directives/)选择性地编译代码段，请参阅 [#define（C# 参考）](/dotnet/csharp/language-reference/preprocessor-directives/preprocessor-define)和 [#if（C# 参考）](/dotnet/csharp/language-reference/preprocessor-directives/preprocessor-if)。</span><span class="sxs-lookup"><span data-stu-id="2ae3c-187">For more information on using [C# preprocessor directives](/dotnet/csharp/language-reference/preprocessor-directives/) to selectively compile sections of code, see [#define (C# Reference)](/dotnet/csharp/language-reference/preprocessor-directives/preprocessor-define) and [#if (C# Reference)](/dotnet/csharp/language-reference/preprocessor-directives/preprocessor-if).</span></span>

### <a name="regions-in-sample-code"></a><span data-ttu-id="2ae3c-188">示例代码中的区域</span><span class="sxs-lookup"><span data-stu-id="2ae3c-188">Regions in sample code</span></span>

<span data-ttu-id="2ae3c-189">一些示例应用包含由 [#region](/dotnet/csharp/language-reference/preprocessor-directives/preprocessor-region) 和 [#endregion](/dotnet/csharp/language-reference/preprocessor-directives/preprocessor-endregion) C# 语句包围的代码片段。</span><span class="sxs-lookup"><span data-stu-id="2ae3c-189">Some sample apps contain sections of code surrounded by [#region](/dotnet/csharp/language-reference/preprocessor-directives/preprocessor-region) and [#endregion](/dotnet/csharp/language-reference/preprocessor-directives/preprocessor-endregion) C# statements.</span></span> <span data-ttu-id="2ae3c-190">文档生成系统会将这些区域注入到所呈现的文档主题中。</span><span class="sxs-lookup"><span data-stu-id="2ae3c-190">The documentation build system injects these regions into the rendered documentation topics.</span></span>  

<span data-ttu-id="2ae3c-191">区域名称通常包含“代码段”一词。</span><span class="sxs-lookup"><span data-stu-id="2ae3c-191">Region names usually contain the word "snippet."</span></span> <span data-ttu-id="2ae3c-192">下面的示例显示了一个名为 `snippet_FilterInCode` 的区域：</span><span class="sxs-lookup"><span data-stu-id="2ae3c-192">The following example shows a region named `snippet_FilterInCode`:</span></span>

```csharp
#region snippet_FilterInCode
WebHost.CreateDefaultBuilder(args)
    .UseStartup<Startup>()
    .ConfigureLogging(logging =>
        logging.AddFilter("System", LogLevel.Debug)
            .AddFilter<DebugLoggerProvider>("Microsoft", LogLevel.Trace))
            .Build();
#endregion
```

<span data-ttu-id="2ae3c-193">主题的 markdown 文件在以下行中应用了前面的 C# 代码段：</span><span class="sxs-lookup"><span data-stu-id="2ae3c-193">The preceding C# code snippet is referenced in the topic's markdown file with the following line:</span></span>

```
[!code-csharp[](sample/SampleApp/Program.cs?name=snippet_FilterInCode)]
```

<span data-ttu-id="2ae3c-194">你可放心忽略（或删除）代码两侧的 `#region` 和 `#endregion` 语句。</span><span class="sxs-lookup"><span data-stu-id="2ae3c-194">You may safely ignore (or remove) the `#region` and `#endregion` statements that surround the code.</span></span> <span data-ttu-id="2ae3c-195">如果计划运行主题中所述的示例方案，请不要更改这些语句中的代码。</span><span class="sxs-lookup"><span data-stu-id="2ae3c-195">Don't alter the code within these statements if you plan to run the sample scenarios described in the topic.</span></span> <span data-ttu-id="2ae3c-196">试用其他方案时，可随时更改代码。</span><span class="sxs-lookup"><span data-stu-id="2ae3c-196">Feel free to alter the code when experimenting with other scenarios.</span></span>

<span data-ttu-id="2ae3c-197">有关详细信息，请参阅[参与 ASP.NET 文档：代码片段](https://github.com/aspnet/Docs/blob/master/CONTRIBUTING.md#code-snippets)。</span><span class="sxs-lookup"><span data-stu-id="2ae3c-197">For more information, see [Contribute to the ASP.NET documentation: Code snippets](https://github.com/aspnet/Docs/blob/master/CONTRIBUTING.md#code-snippets).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2ae3c-198">后续步骤</span><span class="sxs-lookup"><span data-stu-id="2ae3c-198">Next steps</span></span>

<span data-ttu-id="2ae3c-199">有关更多信息，请参见以下资源：</span><span class="sxs-lookup"><span data-stu-id="2ae3c-199">For more information, see the following resources:</span></span>

* <xref:getting-started>
* <xref:tutorials/publish-to-azure-webapp-using-vs>
* [<span data-ttu-id="2ae3c-200">ASP.NET Core 基础知识</span><span class="sxs-lookup"><span data-stu-id="2ae3c-200">ASP.NET Core fundamentals</span></span>](xref:fundamentals/index)
* <span data-ttu-id="2ae3c-201">[每周 ASP.NET Community Standup](https://live.asp.net/) 介绍了团队的工作进度和计划。</span><span class="sxs-lookup"><span data-stu-id="2ae3c-201">[The weekly ASP.NET community standup](https://live.asp.net/) covers the team's progress and plans.</span></span> <span data-ttu-id="2ae3c-202">它以新博客和第三方软件为重点。</span><span class="sxs-lookup"><span data-stu-id="2ae3c-202">It features new blogs and third-party software.</span></span>

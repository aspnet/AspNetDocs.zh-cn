---
uid: whitepapers/whats-new-in-aspnet-45-and-visual-studio-2012
title: ASP.NET 4.5 和 Visual Studio 2012 的新增功能 |Microsoft Docs
author: rick-anderson
description: 本文档介绍了 ASP.NET 4.5 中引入的新功能和增强功能。 还介绍了对 web 开发的改进 .。。
ms.author: riande
ms.date: 02/29/2012
ms.assetid: ba1fabb4-31a3-4ebf-8327-41a6bbba6eaf
msc.legacyurl: /whitepapers/whats-new-in-aspnet-45-and-visual-studio-2012
msc.type: content
ms.openlocfilehash: 32fbf7c25b00f3f0796c4c3fdd38ca2a86c89199
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345405"
---
# <a name="whats-new-in-aspnet-45-and-visual-studio-2012"></a><span data-ttu-id="13a34-104">ASP.NET 4.5 和 Visual Studio 2012 的新增功能</span><span class="sxs-lookup"><span data-stu-id="13a34-104">What's New in ASP.NET 4.5 and Visual Studio 2012</span></span>

> <span data-ttu-id="13a34-105">本文档介绍了 ASP.NET 4.5 中引入的新功能和增强功能。</span><span class="sxs-lookup"><span data-stu-id="13a34-105">This document describes new features and enhancements that are being introduced in ASP.NET 4.5.</span></span> <span data-ttu-id="13a34-106">还介绍了在 Visual Studio 2012 中对 web 开发所做的改进。</span><span class="sxs-lookup"><span data-stu-id="13a34-106">It also describes improvements being made for web development in Visual Studio 2012.</span></span> <span data-ttu-id="13a34-107">此文档最初发布于2012年2月29日。</span><span class="sxs-lookup"><span data-stu-id="13a34-107">This document was originally published on February 29, 2012.</span></span>

- [<span data-ttu-id="13a34-108">ASP.NET Core 运行时和框架</span><span class="sxs-lookup"><span data-stu-id="13a34-108">ASP.NET Core Runtime and Framework</span></span>](#_Toc318097372)

    - [<span data-ttu-id="13a34-109">异步读取和写入 HTTP 请求和响应</span><span class="sxs-lookup"><span data-stu-id="13a34-109">Asynchronously Reading and Writing HTTP Requests and Responses</span></span>](#_Toc318097373)
    - [<span data-ttu-id="13a34-110">对 HttpRequest 处理的改进</span><span class="sxs-lookup"><span data-stu-id="13a34-110">Improvements to HttpRequest handling</span></span>](#_Toc318097374)
    - [<span data-ttu-id="13a34-111">异步刷新响应</span><span class="sxs-lookup"><span data-stu-id="13a34-111">Asynchronously flushing a response</span></span>](#_Toc318097375)
    - [<span data-ttu-id="13a34-112">对 *await* 和基于 *任务*的异步模块和处理程序的支持</span><span class="sxs-lookup"><span data-stu-id="13a34-112">Support for *await* and *Task*-Based Asynchronous Modules and Handlers</span></span>](#_Toc318097376)
    - [<span data-ttu-id="13a34-113">异步 HTTP 模块</span><span class="sxs-lookup"><span data-stu-id="13a34-113">Asynchronous HTTP modules</span></span>](#_Toc318097377)
    - [<span data-ttu-id="13a34-114">异步 HTTP 处理程序</span><span class="sxs-lookup"><span data-stu-id="13a34-114">Asynchronous HTTP handlers</span></span>](#_Toc318097378)
    - [<span data-ttu-id="13a34-115">新 ASP.NET 请求验证功能</span><span class="sxs-lookup"><span data-stu-id="13a34-115">New ASP.NET Request Validation Features</span></span>](#_Toc318097379)
    - [<span data-ttu-id="13a34-116">延迟 ( "延迟" ) 请求验证</span><span class="sxs-lookup"><span data-stu-id="13a34-116">Deferred ("lazy") request validation</span></span>](#_Toc318097380)
    - [<span data-ttu-id="13a34-117">支持未经验证请求</span><span class="sxs-lookup"><span data-stu-id="13a34-117">Support for unvalidated requests</span></span>](#_Toc318097381)
    - [<span data-ttu-id="13a34-118">AntiXSS 库</span><span class="sxs-lookup"><span data-stu-id="13a34-118">AntiXSS Library</span></span>](#_Toc318097382)
    - [<span data-ttu-id="13a34-119">Websocket 协议支持</span><span class="sxs-lookup"><span data-stu-id="13a34-119">Support for WebSockets Protocol</span></span>](#_Toc318097383)
    - [<span data-ttu-id="13a34-120">捆绑和缩小</span><span class="sxs-lookup"><span data-stu-id="13a34-120">Bundling and Minification</span></span>](#_Toc318097384)
    - [<span data-ttu-id="13a34-121">Web 托管的性能改进</span><span class="sxs-lookup"><span data-stu-id="13a34-121">Performance Improvements for Web Hosting</span></span>](#_Toc_perf)

        - [<span data-ttu-id="13a34-122">关键绩效因素</span><span class="sxs-lookup"><span data-stu-id="13a34-122">Key Performance Factors</span></span>](#_Toc_perf_1)
        - [<span data-ttu-id="13a34-123">新性能功能的要求</span><span class="sxs-lookup"><span data-stu-id="13a34-123">Requirements for New Performance Features</span></span>](#_Toc_perf_2)
        - [<span data-ttu-id="13a34-124">共享公用程序集</span><span class="sxs-lookup"><span data-stu-id="13a34-124">Sharing Common Assemblies</span></span>](#_Toc_perf_3)
        - [<span data-ttu-id="13a34-125">使用多核心 JIT 编译加快启动速度</span><span class="sxs-lookup"><span data-stu-id="13a34-125">Using multi-Core JIT compilation for faster startup</span></span>](#_Toc_perf_4)
        - [<span data-ttu-id="13a34-126">优化垃圾回收以优化内存</span><span class="sxs-lookup"><span data-stu-id="13a34-126">Tuning garbage collection to optimize for memory</span></span>](#_Toc_perf_5)
        - [<span data-ttu-id="13a34-127">对 web 应用程序的预提取</span><span class="sxs-lookup"><span data-stu-id="13a34-127">Prefetching for web applications</span></span>](#_Toc_perf_6)
- [<span data-ttu-id="13a34-128">ASP.NET Web 窗体</span><span class="sxs-lookup"><span data-stu-id="13a34-128">ASP.NET Web Forms</span></span>](#_Toc318097385)

    - [<span data-ttu-id="13a34-129">强类型化数据控件</span><span class="sxs-lookup"><span data-stu-id="13a34-129">Strongly Typed Data Controls</span></span>](#_Toc318097386)
    - [<span data-ttu-id="13a34-130">模型绑定</span><span class="sxs-lookup"><span data-stu-id="13a34-130">Model Binding</span></span>](#_Toc318097387)

        - [<span data-ttu-id="13a34-131">选择数据</span><span class="sxs-lookup"><span data-stu-id="13a34-131">Selecting data</span></span>](#_Toc318097388)
        - [<span data-ttu-id="13a34-132">值提供程序</span><span class="sxs-lookup"><span data-stu-id="13a34-132">Value providers</span></span>](#_Toc318097389)
        - [<span data-ttu-id="13a34-133">按控件中的值进行筛选</span><span class="sxs-lookup"><span data-stu-id="13a34-133">Filtering by values from a control</span></span>](#_Toc318097390)
    - [<span data-ttu-id="13a34-134">HTML 编码 Data-Binding 表达式</span><span class="sxs-lookup"><span data-stu-id="13a34-134">HTML Encoded Data-Binding Expressions</span></span>](#_Toc318097391)
    - [<span data-ttu-id="13a34-135">非引人注目验证</span><span class="sxs-lookup"><span data-stu-id="13a34-135">Unobtrusive Validation</span></span>](#_Toc318097392)
    - [<span data-ttu-id="13a34-136">HTML5 更新</span><span class="sxs-lookup"><span data-stu-id="13a34-136">HTML5 Updates</span></span>](#_Toc318097393)
- [<span data-ttu-id="13a34-137">ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="13a34-137">ASP.NET MVC 4</span></span>](#_Toc318097394)
- [<span data-ttu-id="13a34-138">ASP.NET 网页 2</span><span class="sxs-lookup"><span data-stu-id="13a34-138">ASP.NET Web Pages 2</span></span>](#_Toc318097395)
- [<span data-ttu-id="13a34-139">Visual Studio 2012 候选发布版本</span><span class="sxs-lookup"><span data-stu-id="13a34-139">Visual Studio 2012 Release Candidate</span></span>](#_Toc318097396)

    - [<span data-ttu-id="13a34-140">Visual Studio 2010 和 Visual Studio 2012 候选发布版本之间的项目共享 (项目兼容性) </span><span class="sxs-lookup"><span data-stu-id="13a34-140">Project Sharing Between Visual Studio 2010 and Visual Studio 2012 Release Candidate (Project Compatibility)</span></span>](#project-compatibility)
    - [<span data-ttu-id="13a34-141">ASP.NET 4.5 网站模板中的配置更改</span><span class="sxs-lookup"><span data-stu-id="13a34-141">Configuration Changes in ASP.NET 4.5 Website Templates</span></span>](#Configuration_Changes_In_ASPNET45_Website_Templates)
    - [<span data-ttu-id="13a34-142">IIS 7 中用于 ASP.NET 路由的本机支持</span><span class="sxs-lookup"><span data-stu-id="13a34-142">Native Support in IIS 7 for ASP.NET Routing</span></span>](#Native_Support_In_IIS7_For_ASPNET_Routine)
    - [<span data-ttu-id="13a34-143">HTML 编辑器</span><span class="sxs-lookup"><span data-stu-id="13a34-143">HTML Editor</span></span>](#_Toc318097397)

        - [<span data-ttu-id="13a34-144">智能任务</span><span class="sxs-lookup"><span data-stu-id="13a34-144">Smart Tasks</span></span>](#_Toc318097398)
        - [<span data-ttu-id="13a34-145">WAI-ARIA 支持</span><span class="sxs-lookup"><span data-stu-id="13a34-145">WAI-ARIA support</span></span>](#_Toc318097399)
        - [<span data-ttu-id="13a34-146">新 HTML5 代码段</span><span class="sxs-lookup"><span data-stu-id="13a34-146">New HTML5 snippets</span></span>](#_Toc318097400)
        - [<span data-ttu-id="13a34-147">提取到用户控件</span><span class="sxs-lookup"><span data-stu-id="13a34-147">Extract to user control</span></span>](#_Toc318097401)
        - [<span data-ttu-id="13a34-148">特性中代码片段的 IntelliSense</span><span class="sxs-lookup"><span data-stu-id="13a34-148">IntelliSense for code nuggets in attributes</span></span>](#_Toc318097402)
        - [<span data-ttu-id="13a34-149">重命名开始或结束标记时自动重命名匹配标记</span><span class="sxs-lookup"><span data-stu-id="13a34-149">Automatic renaming of matching tag when you rename an opening or closing tag</span></span>](#_Toc318097403)
        - [<span data-ttu-id="13a34-150">生成事件处理程序</span><span class="sxs-lookup"><span data-stu-id="13a34-150">Event handler generation</span></span>](#_Toc318097404)
        - [<span data-ttu-id="13a34-151">智能缩进</span><span class="sxs-lookup"><span data-stu-id="13a34-151">Smart indent</span></span>](#_Toc318097405)
        - [<span data-ttu-id="13a34-152">自动减少语句完成</span><span class="sxs-lookup"><span data-stu-id="13a34-152">Auto-reduce statement completion</span></span>](#_Toc318097406)
    - [<span data-ttu-id="13a34-153">JavaScript 编辑器</span><span class="sxs-lookup"><span data-stu-id="13a34-153">JavaScript Editor</span></span>](#_Toc318097407)

        - [<span data-ttu-id="13a34-154">代码大纲显示</span><span class="sxs-lookup"><span data-stu-id="13a34-154">Code outlining</span></span>](#_Toc318097408)
        - [<span data-ttu-id="13a34-155">大括号匹配</span><span class="sxs-lookup"><span data-stu-id="13a34-155">Brace matching</span></span>](#_Toc318097409)
        - [<span data-ttu-id="13a34-156">转到定义</span><span class="sxs-lookup"><span data-stu-id="13a34-156">Go to Definition</span></span>](#_Toc318097410)
        - [<span data-ttu-id="13a34-157">ECMAScript5 支持</span><span class="sxs-lookup"><span data-stu-id="13a34-157">ECMAScript5 support</span></span>](#_Toc318097411)
        - [<span data-ttu-id="13a34-158">DOM IntelliSense</span><span class="sxs-lookup"><span data-stu-id="13a34-158">DOM IntelliSense</span></span>](#_Toc318097412)
        - [<span data-ttu-id="13a34-159">VSDOC 签名重载</span><span class="sxs-lookup"><span data-stu-id="13a34-159">VSDOC signature overloads</span></span>](#_Toc318097413)
        - [<span data-ttu-id="13a34-160">隐式引用</span><span class="sxs-lookup"><span data-stu-id="13a34-160">Implicit references</span></span>](#_Toc318097414)
    - [<span data-ttu-id="13a34-161">CSS 编辑器</span><span class="sxs-lookup"><span data-stu-id="13a34-161">CSS Editor</span></span>](#_Toc318097415)

        - [<span data-ttu-id="13a34-162">自动减少语句完成</span><span class="sxs-lookup"><span data-stu-id="13a34-162">Auto-reduce statement completion</span></span>](#_Toc318097416)
        - [<span data-ttu-id="13a34-163">分层缩进。</span><span class="sxs-lookup"><span data-stu-id="13a34-163">Hierarchical indentation.</span></span>](#_Toc318097417)
        - [<span data-ttu-id="13a34-164">CSS 黑客支持</span><span class="sxs-lookup"><span data-stu-id="13a34-164">CSS hacks support</span></span>](#_Toc318097418)
        - [<span data-ttu-id="13a34-165">特定于供应商的架构 (-moz-,-webkit) </span><span class="sxs-lookup"><span data-stu-id="13a34-165">Vendor specific schemas (-moz-,-webkit)</span></span>](#_Toc318097419)
        - [<span data-ttu-id="13a34-166">注释和取消注释支持</span><span class="sxs-lookup"><span data-stu-id="13a34-166">Commenting and uncommenting support</span></span>](#_Toc318097420)
        - [<span data-ttu-id="13a34-167">颜色选取器</span><span class="sxs-lookup"><span data-stu-id="13a34-167">Color picker</span></span>](#_Toc318097421)
        - [<span data-ttu-id="13a34-168">片段</span><span class="sxs-lookup"><span data-stu-id="13a34-168">Snippets</span></span>](#_Toc318097422)
        - [<span data-ttu-id="13a34-169">自定义区域</span><span class="sxs-lookup"><span data-stu-id="13a34-169">Custom regions</span></span>](#_Toc318097423)
    - [<span data-ttu-id="13a34-170">Page Inspector</span><span class="sxs-lookup"><span data-stu-id="13a34-170">Page Inspector</span></span>](#_Toc318097424)
    - [<span data-ttu-id="13a34-171">发布</span><span class="sxs-lookup"><span data-stu-id="13a34-171">Publishing</span></span>](#_Toc318097425)

        - <span data-ttu-id="13a34-172">发布配置文件 </span><span class="sxs-lookup"><span data-stu-id="13a34-172">[Publish profiles](#_Toc318097426)</span></span>
        - [<span data-ttu-id="13a34-173">ASP.NET 预编译和合并</span><span class="sxs-lookup"><span data-stu-id="13a34-173">ASP.NET precompilation and merge</span></span>](#_Toc318097427)
- [<span data-ttu-id="13a34-174">IIS Express</span><span class="sxs-lookup"><span data-stu-id="13a34-174">IIS Express</span></span>](#_Toc318097428)
- [<span data-ttu-id="13a34-175">免责声明</span><span class="sxs-lookup"><span data-stu-id="13a34-175">Disclaimer</span></span>](#_Toc318097429)

<a id="_Toc318097372"></a>
## <a name="aspnet-core-runtime-and-framework"></a><span data-ttu-id="13a34-176">ASP.NET Core 运行时和框架</span><span class="sxs-lookup"><span data-stu-id="13a34-176">ASP.NET Core Runtime and Framework</span></span>

<a id="_Toc318097373"></a>
### <a name="asynchronously-reading-and-writing-http-requests-and-responses"></a><span data-ttu-id="13a34-177">异步读取和写入 HTTP 请求和响应</span><span class="sxs-lookup"><span data-stu-id="13a34-177">Asynchronously Reading and Writing HTTP Requests and Responses</span></span>

<span data-ttu-id="13a34-178">ASP.NET 4 引入了使用 *HttpRequest. GetBufferlessInputStream* 方法将 HTTP 请求实体作为流进行读取的功能。</span><span class="sxs-lookup"><span data-stu-id="13a34-178">ASP.NET 4 introduced the ability to read an HTTP request entity as a stream using the *HttpRequest.GetBufferlessInputStream* method.</span></span> <span data-ttu-id="13a34-179">此方法提供对请求实体的流式访问。</span><span class="sxs-lookup"><span data-stu-id="13a34-179">This method provided streaming access to the request entity.</span></span> <span data-ttu-id="13a34-180">但是，它会同步执行，这会在请求的持续时间内将线程关联起来。</span><span class="sxs-lookup"><span data-stu-id="13a34-180">However, it executed synchronously, which tied up a thread for the duration of a request.</span></span>

<span data-ttu-id="13a34-181">ASP.NET 4.5 支持能够以异步方式在 HTTP 请求实体上读取流，并且能够以异步方式刷新。</span><span class="sxs-lookup"><span data-stu-id="13a34-181">ASP.NET 4.5 supports the ability to read streams asynchronously on an HTTP request entity, and the ability to flush asynchronously.</span></span> <span data-ttu-id="13a34-182">使用 ASP.NET 4.5，你还可以将 HTTP 请求实体加倍，这使得与下游 HTTP 处理程序（如 .aspx 页面处理程序和 ASP.NET MVC 控制器）的集成更加简单。</span><span class="sxs-lookup"><span data-stu-id="13a34-182">ASP.NET 4.5 also gives you the ability to double-buffer an HTTP request entity, which provides easier integration with downstream HTTP handlers such as .aspx page handlers and ASP.NET MVC controllers.</span></span>

<a id="_Toc318097374"></a>
#### <a name="improvements-to-httprequest-handling"></a><span data-ttu-id="13a34-183">对 HttpRequest 处理的改进</span><span class="sxs-lookup"><span data-stu-id="13a34-183">Improvements to HttpRequest handling</span></span>

<span data-ttu-id="13a34-184">ASP.NET 4.5 从 *HttpRequest* 返回的流引用支持同步和异步读取方法。</span><span class="sxs-lookup"><span data-stu-id="13a34-184">The Stream reference returned by ASP.NET 4.5 from *HttpRequest.GetBufferlessInputStream* supports both synchronous and asynchronous read methods.</span></span> <span data-ttu-id="13a34-185">从*GetBufferlessInputStream*返回的*流*对象现在同时实现 BeginRead 和 EndRead 方法。</span><span class="sxs-lookup"><span data-stu-id="13a34-185">The *Stream* object returned from *GetBufferlessInputStream* now implements both the BeginRead and EndRead methods.</span></span> <span data-ttu-id="13a34-186">使用异步 *流* 方法，你可以在块中异步读取请求实体，而 ASP.NET 将在异步读取循环的每次迭代之间释放当前线程。</span><span class="sxs-lookup"><span data-stu-id="13a34-186">The asynchronous *Stream* methods let you asynchronously read the request entity in chunks, while ASP.NET releases the current thread between each iteration of an asynchronous read loop.</span></span>

<span data-ttu-id="13a34-187">ASP.NET 4.5 还添加了一种以缓冲方式读取请求实体的伴随方法： *HttpRequest. GetBufferedInputStream*。</span><span class="sxs-lookup"><span data-stu-id="13a34-187">ASP.NET 4.5 has also added a companion method for reading the request entity in a buffered way: *HttpRequest.GetBufferedInputStream*.</span></span> <span data-ttu-id="13a34-188">此新重载的工作方式类似于 *GetBufferlessInputStream*，同时支持同步和异步读取。</span><span class="sxs-lookup"><span data-stu-id="13a34-188">This new overload works like *GetBufferlessInputStream*, supporting both synchronous and asynchronous reads.</span></span> <span data-ttu-id="13a34-189">但在读取时， *GetBufferedInputStream* 还会将实体字节复制到 ASP.NET 内部缓冲区，以便下游模块和处理程序仍可以访问请求实体。</span><span class="sxs-lookup"><span data-stu-id="13a34-189">However, as it reads, *GetBufferedInputStream* also copies the entity bytes into ASP.NET internal buffers so that downstream modules and handlers can still access the request entity.</span></span> <span data-ttu-id="13a34-190">例如，如果管道中的某些上游代码已使用 *GetBufferedInputStream*读取请求实体，则仍可使用 *HttpRequest* 或 *HttpRequest*。</span><span class="sxs-lookup"><span data-stu-id="13a34-190">For example, if some upstream code in the pipeline has already read the request entity using *GetBufferedInputStream*, you can still use *HttpRequest.Form* or *HttpRequest.Files*.</span></span> <span data-ttu-id="13a34-191">这使你可以对请求执行异步处理 (例如，将大型文件上传到数据库) ，但此后仍运行 .aspx 页面和 MVC ASP.NET 控制器。</span><span class="sxs-lookup"><span data-stu-id="13a34-191">This lets you perform asynchronous processing on a request (for example, streaming a large file upload to a database), but still run .aspx pages and MVC ASP.NET controllers afterward.</span></span>

<a id="_Toc318097375"></a>
#### <a name="asynchronously-flushing-a-response"></a><span data-ttu-id="13a34-192">异步刷新响应</span><span class="sxs-lookup"><span data-stu-id="13a34-192">Asynchronously flushing a response</span></span>

<span data-ttu-id="13a34-193">向 HTTP 客户端发送响应可能需要相当长的时间，因为客户端可能会太远，或者具有低带宽连接。</span><span class="sxs-lookup"><span data-stu-id="13a34-193">Sending responses to an HTTP client can take considerable time when the client is far away or has a low-bandwidth connection.</span></span> <span data-ttu-id="13a34-194">通常，在应用程序创建响应字节时，ASP.NET 会将其缓冲。</span><span class="sxs-lookup"><span data-stu-id="13a34-194">Normally ASP.NET buffers the response bytes as they are created by an application.</span></span> <span data-ttu-id="13a34-195">然后，ASP.NET 会在请求处理结束时执行累计缓冲区的单个发送操作。</span><span class="sxs-lookup"><span data-stu-id="13a34-195">ASP.NET then performs a single send operation of the accrued buffers at the very end of request processing.</span></span>

<span data-ttu-id="13a34-196">如果缓冲响应很大 (例如，将大型文件流式传输到客户端) ，则必须定期调用 *httpresponse.cache* ，以将缓冲的输出发送到客户端，并使内存使用保持控制。</span><span class="sxs-lookup"><span data-stu-id="13a34-196">If the buffered response is large (for example, streaming a large file to a client), you must periodically call *HttpResponse.Flush* to send buffered output to the client and keep memory usage under control.</span></span> <span data-ttu-id="13a34-197">不过，由于 *刷新* 是同步调用，因此，在可能长时间运行的请求的持续时间内，反复调用 *刷新* 仍会消耗线程。</span><span class="sxs-lookup"><span data-stu-id="13a34-197">However, because *Flush* is a synchronous call, iteratively calling *Flush* still consumes a thread for the duration of potentially long-running requests.</span></span>

<span data-ttu-id="13a34-198">ASP.NET 4.5 添加了对使用*httpresponse.cache*类的*BeginFlush*和*EndFlush*方法异步执行刷新的支持。</span><span class="sxs-lookup"><span data-stu-id="13a34-198">ASP.NET 4.5 adds support for performing flushes asynchronously using the *BeginFlush* and *EndFlush* methods of the *HttpResponse* class.</span></span> <span data-ttu-id="13a34-199">使用这些方法，你可以创建异步模块和异步处理程序，以将数据增量发送到客户端，而无需占用操作系统线程。</span><span class="sxs-lookup"><span data-stu-id="13a34-199">Using these methods, you can create asynchronous modules and asynchronous handlers that incrementally send data to a client without tying up operating-system threads.</span></span> <span data-ttu-id="13a34-200">在 *BeginFlush* 和 *EndFlush* 调用之间，ASP.NET 释放当前线程。</span><span class="sxs-lookup"><span data-stu-id="13a34-200">In between *BeginFlush* and *EndFlush* calls, ASP.NET releases the current thread.</span></span> <span data-ttu-id="13a34-201">这大大减少了支持长时间运行的 HTTP 下载所需的活动线程的总数。</span><span class="sxs-lookup"><span data-stu-id="13a34-201">This substantially reduces the total number of active threads that are needed in order to support long-running HTTP downloads.</span></span>

<a id="_Toc318097376"></a>
### <a name="support-for-await-and-task---based-asynchronous-modules-and-handlers"></a><span data-ttu-id="13a34-202">对 *await* 和基于 *任务* 的异步模块和处理程序的支持</span><span class="sxs-lookup"><span data-stu-id="13a34-202">Support for *await* and *Task* - Based Asynchronous Modules and Handlers</span></span>

<span data-ttu-id="13a34-203">.NET Framework 4 引入了一个称为 *任务*的异步编程概念。</span><span class="sxs-lookup"><span data-stu-id="13a34-203">The .NET Framework 4 introduced an asynchronous programming concept referred to as a *task*.</span></span> <span data-ttu-id="13a34-204">任务由*tasks 命名空间中的\*\*任务*类型和相关类型来表示。</span><span class="sxs-lookup"><span data-stu-id="13a34-204">Tasks are represented by the *Task* type and related types in the *System.Threading.Tasks* namespace.</span></span> <span data-ttu-id="13a34-205">.NET Framework 4.5 通过编译器增强功能生成，使 *任务* 对象的使用更加简单。</span><span class="sxs-lookup"><span data-stu-id="13a34-205">The .NET Framework 4.5 builds on this with compiler enhancements that make working with *Task* objects simple.</span></span> <span data-ttu-id="13a34-206">在 .NET Framework 4.5 中，编译器支持两个新的关键字： *await* 和 *async*。</span><span class="sxs-lookup"><span data-stu-id="13a34-206">In the .NET Framework 4.5, the compilers support two new keywords: *await* and *async*.</span></span> <span data-ttu-id="13a34-207">*Await*关键字是语法简写，指示代码段应以异步方式等待某个代码的其他部分。</span><span class="sxs-lookup"><span data-stu-id="13a34-207">The *await* keyword is syntactical shorthand for indicating that a piece of code should asynchronously wait on some other piece of code.</span></span> <span data-ttu-id="13a34-208">*Async*关键字表示一个提示，可用于将方法标记为基于任务的异步方法。</span><span class="sxs-lookup"><span data-stu-id="13a34-208">The *async* keyword represents a hint that you can use to mark methods as task-based asynchronous methods.</span></span>

<span data-ttu-id="13a34-209">*Await*、 *async*和*Task*对象的组合使你可以更轻松地在 .net 4.5 中编写异步代码。</span><span class="sxs-lookup"><span data-stu-id="13a34-209">The combination of *await*, *async*, and the *Task* object makes it much easier for you to write asynchronous code in .NET 4.5.</span></span> <span data-ttu-id="13a34-210">ASP.NET 4.5 通过新的 Api 支持这些简化，使你能够使用新的编译器增强功能编写异步 HTTP 模块和异步 HTTP 处理程序。</span><span class="sxs-lookup"><span data-stu-id="13a34-210">ASP.NET 4.5 supports these simplifications with new APIs that let you write asynchronous HTTP modules and asynchronous HTTP handlers using the new compiler enhancements.</span></span>

<a id="_Toc318097377"></a>
#### <a name="asynchronous-http-modules"></a><span data-ttu-id="13a34-211">异步 HTTP 模块</span><span class="sxs-lookup"><span data-stu-id="13a34-211">Asynchronous HTTP modules</span></span>

<span data-ttu-id="13a34-212">假设要在返回 *Task* 对象的方法中执行异步工作。</span><span class="sxs-lookup"><span data-stu-id="13a34-212">Suppose that you want to perform asynchronous work within a method that returns a *Task* object.</span></span> <span data-ttu-id="13a34-213">下面的代码示例定义了一个异步方法，该方法可执行异步调用以下载 Microsoft 主页。</span><span class="sxs-lookup"><span data-stu-id="13a34-213">The following code example defines an asynchronous method that makes an asynchronous call to download the Microsoft home page.</span></span> <span data-ttu-id="13a34-214">请注意，在方法签名中使用 *async* 关键字，并在 *等待* 调用 *DownloadStringTaskAsync*。</span><span class="sxs-lookup"><span data-stu-id="13a34-214">Notice the use of the *async* keyword in the method signature and the *await* call to *DownloadStringTaskAsync*.</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample1.cs)]

<span data-ttu-id="13a34-215">这就是您必须编写的所有内容，.NET Framework 将在等待下载完成时自动处理展开调用堆栈，并在下载完成后自动还原调用堆栈。</span><span class="sxs-lookup"><span data-stu-id="13a34-215">That's all you have to write — the .NET Framework will automatically handle unwinding the call stack while waiting for the download to complete, as well as automatically restoring the call stack after the download is done.</span></span>

<span data-ttu-id="13a34-216">现在假设要在异步 ASP.NET HTTP 模块中使用此异步方法。</span><span class="sxs-lookup"><span data-stu-id="13a34-216">Now suppose that you want to use this asynchronous method in an asynchronous ASP.NET HTTP module.</span></span> <span data-ttu-id="13a34-217">ASP.NET 4.5 包含一个帮助器方法 (*EventHandlerTaskAsyncHelper*) 和一个新的委托类型 (*TaskEventHandler*) ，可用于将基于任务的异步方法与 ASP.NET HTTP 管道公开的旧异步编程模型集成。</span><span class="sxs-lookup"><span data-stu-id="13a34-217">ASP.NET 4.5 includes a helper method (*EventHandlerTaskAsyncHelper*) and a new delegate type (*TaskEventHandler*) that you can use to integrate task-based asynchronous methods with the older asynchronous programming model exposed by the ASP.NET HTTP pipeline.</span></span> <span data-ttu-id="13a34-218">此示例演示如何执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="13a34-218">This example shows how:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample2.cs)]

<a id="_Toc318097378"></a>
#### <a name="asynchronous-http-handlers"></a><span data-ttu-id="13a34-219">异步 HTTP 处理程序</span><span class="sxs-lookup"><span data-stu-id="13a34-219">Asynchronous HTTP handlers</span></span>

<span data-ttu-id="13a34-220">在 ASP.NET 中编写异步处理程序的传统方法是实现 *IHttpAsyncHandler* 接口。</span><span class="sxs-lookup"><span data-stu-id="13a34-220">The traditional approach to writing asynchronous handlers in ASP.NET is to implement the *IHttpAsyncHandler* interface.</span></span> <span data-ttu-id="13a34-221">ASP.NET 4.5 引入了可从派生的 *HttpTaskAsyncHandler* 异步基类型，这使得编写异步处理程序变得更加容易。</span><span class="sxs-lookup"><span data-stu-id="13a34-221">ASP.NET 4.5 introduces the *HttpTaskAsyncHandler* asynchronous base type that you can derive from, which makes it much easier to write asynchronous handlers.</span></span>

<span data-ttu-id="13a34-222">*HttpTaskAsyncHandler*类型是抽象的，需要重写*ProcessRequestAsync*方法。</span><span class="sxs-lookup"><span data-stu-id="13a34-222">The *HttpTaskAsyncHandler* type is abstract and requires you to override the *ProcessRequestAsync* method.</span></span> <span data-ttu-id="13a34-223">内部 ASP.NET 负责将 (*Task* 对象) *ProcessRequestAsync* 的返回签名与 ASP.NET 管道使用的旧异步编程模型相集成。</span><span class="sxs-lookup"><span data-stu-id="13a34-223">Internally ASP.NET takes care of integrating the return signature (a *Task* object) of *ProcessRequestAsync* with the older asynchronous programming model used by the ASP.NET pipeline.</span></span>

<span data-ttu-id="13a34-224">下面的示例演示如何使用 *Task* 和 *AWAIT* 作为异步 HTTP 处理程序实现的一部分：</span><span class="sxs-lookup"><span data-stu-id="13a34-224">The following example shows how you can use *Task* and *await* as part of the implementation of an asynchronous HTTP handler:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample3.cs)]

<a id="_Toc318097379"></a>
### <a name="new-aspnet-request-validation-features"></a><span data-ttu-id="13a34-225">新 ASP.NET 请求验证功能</span><span class="sxs-lookup"><span data-stu-id="13a34-225">New ASP.NET Request Validation Features</span></span>

<span data-ttu-id="13a34-226">默认情况下，ASP.NET 执行请求验证，即检查请求以查找字段、标头、cookie 等中的标记或脚本。</span><span class="sxs-lookup"><span data-stu-id="13a34-226">By default, ASP.NET performs request validation — it examines requests to look for markup or script in fields, headers, cookies, and so on.</span></span> <span data-ttu-id="13a34-227">如果检测到任何，ASP.NET 将引发异常。</span><span class="sxs-lookup"><span data-stu-id="13a34-227">If any is detected, ASP.NET throws an exception.</span></span> <span data-ttu-id="13a34-228">这作为防御潜在跨站点脚本攻击的第一道防线。</span><span class="sxs-lookup"><span data-stu-id="13a34-228">This acts as a first line of defense against potential cross-site scripting attacks.</span></span>

<span data-ttu-id="13a34-229">ASP.NET 4.5 使你可以轻松地选择读取未经验证请求数据。</span><span class="sxs-lookup"><span data-stu-id="13a34-229">ASP.NET 4.5 makes it easy to selectively read unvalidated request data.</span></span> <span data-ttu-id="13a34-230">ASP.NET 4.5 还集成了常用的 AntiXSS 库，这是以前的外部库。</span><span class="sxs-lookup"><span data-stu-id="13a34-230">ASP.NET 4.5 also integrates the popular AntiXSS library, which was formerly an external library.</span></span>

<span data-ttu-id="13a34-231">开发人员经常需要为其应用程序选择关闭请求验证的能力。</span><span class="sxs-lookup"><span data-stu-id="13a34-231">Developers have frequently asked for the ability to selectively turn off request validation for their applications.</span></span> <span data-ttu-id="13a34-232">例如，如果你的应用程序是论坛软件，则你可能希望允许用户提交 HTML 格式的论坛帖子和评论，但仍要确保请求验证检查其他所有内容。</span><span class="sxs-lookup"><span data-stu-id="13a34-232">For example, if your application is forum software, you might want to allow users to submit HTML-formatted forum posts and comments, but still make sure that request validation is checking everything else.</span></span>

<span data-ttu-id="13a34-233">ASP.NET 4.5 引入了两个功能，使你可以轻松地使用未经验证输入：延迟 ( "延迟" ) 请求验证和访问未经验证请求数据。</span><span class="sxs-lookup"><span data-stu-id="13a34-233">ASP.NET 4.5 introduces two features that make it easy for you to selectively work with unvalidated input: deferred ("lazy") request validation and access to unvalidated request data.</span></span>

<a id="_Toc318097380"></a>
#### <a name="deferred-lazy-request-validation"></a><span data-ttu-id="13a34-234">延迟 ( "延迟" ) 请求验证</span><span class="sxs-lookup"><span data-stu-id="13a34-234">Deferred ("lazy") request validation</span></span>

<span data-ttu-id="13a34-235">在 ASP.NET 4.5 中，默认情况下，所有请求数据都服从请求验证。</span><span class="sxs-lookup"><span data-stu-id="13a34-235">In ASP.NET 4.5, by default all request data is subject to request validation.</span></span> <span data-ttu-id="13a34-236">但是，你可以将应用程序配置为延迟请求验证，直到实际访问请求数据为止。</span><span class="sxs-lookup"><span data-stu-id="13a34-236">However, you can configure the application to defer request validation until you actually access request data.</span></span> <span data-ttu-id="13a34-237"> (这有时被称为延迟请求验证，这是基于某些数据方案的延迟加载等术语。 ) 可以通过将*httpRUntime*元素中的*requestValidationMode*属性设置为4.5，将应用程序配置为在 Web.config 文件中使用延迟的验证，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="13a34-237">(This is sometimes referred to as lazy request validation, based on terms like lazy loading for certain data scenarios.) You can configure the application to use deferred validation in the Web.config file by setting the *requestValidationMode* attribute to 4.5 in the *httpRUntime* element, as in the following example:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample4.xml)]

<span data-ttu-id="13a34-238">当请求验证模式设置为4.5 时，仅当代码访问该值时才会触发请求验证。</span><span class="sxs-lookup"><span data-stu-id="13a34-238">When request validation mode is set to 4.5, request validation is triggered only for a specific request value and only when your code accesses that value.</span></span> <span data-ttu-id="13a34-239">例如，如果你的代码获取 "请求" 的值。表单 ["论坛 \_ 帖子"]，只为窗体集合中的该元素调用请求验证。</span><span class="sxs-lookup"><span data-stu-id="13a34-239">For example, if your code gets the value of Request.Form["forum\_post"], request validation is invoked only for that element in the form collection.</span></span> <span data-ttu-id="13a34-240">未验证 *窗体* 集合中的其他元素。</span><span class="sxs-lookup"><span data-stu-id="13a34-240">None of the other elements in the *Form* collection are validated.</span></span> <span data-ttu-id="13a34-241">在以前版本的 ASP.NET 中，当访问集合中的任何元素时，将触发整个请求集合的请求验证。</span><span class="sxs-lookup"><span data-stu-id="13a34-241">In previous versions of ASP.NET, request validation was triggered for the entire request collection when any element in the collection was accessed.</span></span> <span data-ttu-id="13a34-242">新行为使不同的应用程序组件可以更轻松地查看不同的请求数据块，而不会在其他部分触发请求验证。</span><span class="sxs-lookup"><span data-stu-id="13a34-242">The new behavior makes it easier for different application components to look at different pieces of request data without triggering request validation on other pieces.</span></span>

<a id="_Toc318097381"></a>
#### <a name="support-for-unvalidated-requests"></a><span data-ttu-id="13a34-243">支持未经验证请求</span><span class="sxs-lookup"><span data-stu-id="13a34-243">Support for unvalidated requests</span></span>

<span data-ttu-id="13a34-244">仅限延迟的请求验证不能解决有选择性地绕过请求验证的问题。</span><span class="sxs-lookup"><span data-stu-id="13a34-244">Deferred request validation alone doesn't solve the problem of selectively bypassing request validation.</span></span> <span data-ttu-id="13a34-245">对请求的调用。窗体 ["论坛 \_ 帖子"] 仍将触发对该特定请求值的请求验证。</span><span class="sxs-lookup"><span data-stu-id="13a34-245">The call to Request.Form["forum\_post"] still triggers request validation for that specific request value.</span></span> <span data-ttu-id="13a34-246">但是，你可能想要访问此字段而不触发验证，因为你希望在该字段中允许标记。</span><span class="sxs-lookup"><span data-stu-id="13a34-246">However, you might want to access this field without triggering validation because you want to allow markup in that field.</span></span>

<span data-ttu-id="13a34-247">为此，ASP.NET 4.5 现在支持对请求数据进行未经验证访问。</span><span class="sxs-lookup"><span data-stu-id="13a34-247">To allow this, ASP.NET 4.5 now supports unvalidated access to request data.</span></span> <span data-ttu-id="13a34-248">ASP.NET 4.5 在*HttpRequest*类中包含新的*未经验证*集合属性。</span><span class="sxs-lookup"><span data-stu-id="13a34-248">ASP.NET 4.5 includes a new *Unvalidated* collection property in the *HttpRequest* class.</span></span> <span data-ttu-id="13a34-249">此集合提供对请求数据的所有公共值的访问，如 *窗体*、 *查询字符串*、 *cookie*和 *Url*。</span><span class="sxs-lookup"><span data-stu-id="13a34-249">This collection provides access to all of the common values of request data, like *Form*, *QueryString*, *Cookies*, and *Url*.</span></span>

<span data-ttu-id="13a34-250">使用论坛示例，若要读取未经验证请求数据，首先需要将应用程序配置为使用新的请求验证模式：</span><span class="sxs-lookup"><span data-stu-id="13a34-250">Using the forum example, to be able to read unvalidated request data, you first need to configure the application to use the new request validation mode:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample5.xml)]

<span data-ttu-id="13a34-251">然后，可以使用未经验证属性来读取未经验证窗体值 *HttpRequest* ：</span><span class="sxs-lookup"><span data-stu-id="13a34-251">You can then use the *HttpRequest.Unvalidated* property to read the unvalidated form value:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample6.cs)]

> [!WARNING]
> <span data-ttu-id="13a34-252">安全性- *使用未经验证请求数据！*</span><span class="sxs-lookup"><span data-stu-id="13a34-252">Security - *Use unvalidated request data with care!*</span></span> <span data-ttu-id="13a34-253">ASP.NET 4.5 添加了未经验证请求属性和集合，使你能够更轻松地访问非常特定的未经验证请求数据。</span><span class="sxs-lookup"><span data-stu-id="13a34-253">ASP.NET 4.5 added the unvalidated request properties and collections to make it easier for you to access very specific unvalidated request data.</span></span> <span data-ttu-id="13a34-254">但是，仍必须对原始请求数据执行自定义验证，以确保不会向用户呈现危险文本。</span><span class="sxs-lookup"><span data-stu-id="13a34-254">However, you must still perform custom validation on the raw request data to ensure that dangerous text is not rendered to users.</span></span>

<a id="_Toc318097382"></a>
### <a name="antixss-library"></a><span data-ttu-id="13a34-255">AntiXSS 库</span><span class="sxs-lookup"><span data-stu-id="13a34-255">AntiXSS Library</span></span>

<span data-ttu-id="13a34-256">由于 Microsoft AntiXSS 库的普及，ASP.NET 4.5 现在合并了该库版本4.0 中的核心编码例程。</span><span class="sxs-lookup"><span data-stu-id="13a34-256">Due to the popularity of the Microsoft AntiXSS Library, ASP.NET 4.5 now incorporates core encoding routines from version 4.0 of that library.</span></span>

<span data-ttu-id="13a34-257">编码例程由 *AntiXssEncoder* 类型在新的 *AntiXss* 命名空间中实现。</span><span class="sxs-lookup"><span data-stu-id="13a34-257">The encoding routines are implemented by the *AntiXssEncoder* type in the new *System.Web.Security.AntiXss* namespace.</span></span> <span data-ttu-id="13a34-258">可以通过调用在类型中实现的任何静态编码方法，直接使用 *AntiXssEncoder* 类型。</span><span class="sxs-lookup"><span data-stu-id="13a34-258">You can use the *AntiXssEncoder* type directly by calling any of the static encoding methods that are implemented in the type.</span></span> <span data-ttu-id="13a34-259">然而，最简单的方法是使用新的防 XSS 例程，将 ASP.NET 应用程序配置为在默认情况下使用 *AntiXssEncoder* 类。</span><span class="sxs-lookup"><span data-stu-id="13a34-259">However, the easiest approach for using the new anti-XSS routines is to configure an ASP.NET application to use the *AntiXssEncoder* class by default.</span></span> <span data-ttu-id="13a34-260">为此，请将以下属性添加到 Web.config 文件：</span><span class="sxs-lookup"><span data-stu-id="13a34-260">To do this, add the following attribute to the Web.config file:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample7.xml)]

<span data-ttu-id="13a34-261">当 *encoderType* 属性设置为使用 *AntiXssEncoder* 类型时，ASP.NET 中的所有输出编码会自动使用新的编码例程。</span><span class="sxs-lookup"><span data-stu-id="13a34-261">When the *encoderType* attribute is set to use the *AntiXssEncoder* type, all output encoding in ASP.NET automatically uses the new encoding routines.</span></span>

<span data-ttu-id="13a34-262">以下是外部 AntiXSS 库中已合并到 ASP.NET 4.5 的部分：</span><span class="sxs-lookup"><span data-stu-id="13a34-262">These are the portions of the external AntiXSS library that have been incorporated into ASP.NET 4.5:</span></span>

- <span data-ttu-id="13a34-263">*Server.htmlencode*、 *HtmlFormUrlEncode*和 *HtmlAttributeEncode*</span><span class="sxs-lookup"><span data-stu-id="13a34-263">*HtmlEncode*, *HtmlFormUrlEncode*, and *HtmlAttributeEncode*</span></span>
- <span data-ttu-id="13a34-264">*XmlAttributeEncode* 和 *XmlEncode*</span><span class="sxs-lookup"><span data-stu-id="13a34-264">*XmlAttributeEncode* and *XmlEncode*</span></span>
- <span data-ttu-id="13a34-265">*UrlEncode* 和 *UrlPathEncode* (new) </span><span class="sxs-lookup"><span data-stu-id="13a34-265">*UrlEncode* and *UrlPathEncode* (new)</span></span>
- <span data-ttu-id="13a34-266">*CssEncode*</span><span class="sxs-lookup"><span data-stu-id="13a34-266">*CssEncode*</span></span>

<a id="_Toc318097383"></a>
### <a name="support-for-websockets-protocol"></a><span data-ttu-id="13a34-267">Websocket 协议支持</span><span class="sxs-lookup"><span data-stu-id="13a34-267">Support for WebSockets Protocol</span></span>

<span data-ttu-id="13a34-268">Websocket 协议是一种基于标准的网络协议，用于定义如何通过 HTTP 建立客户端与服务器之间的安全实时双向通信。</span><span class="sxs-lookup"><span data-stu-id="13a34-268">WebSockets protocol is a standards-based network protocol that defines how to establish secure, real-time bidirectional communications between a client and a server over HTTP.</span></span> <span data-ttu-id="13a34-269">Microsoft 同时结合了 IETF 和 W3C 标准，有助于定义协议。</span><span class="sxs-lookup"><span data-stu-id="13a34-269">Microsoft has worked with both the IETF and W3C standards bodies to help define the protocol.</span></span> <span data-ttu-id="13a34-270">不只是浏览器) 的任何客户 (端都支持 Websocket 协议，Microsoft 在客户端和移动操作系统上对支持 Websocket 协议的大量资源进行投资。</span><span class="sxs-lookup"><span data-stu-id="13a34-270">The WebSockets protocol is supported by any client (not just browsers), with Microsoft investing substantial resources supporting WebSockets protocol on both client and mobile operating systems.</span></span>

<span data-ttu-id="13a34-271">Websocket 协议使在客户端和服务器之间创建长时间运行的数据传输变得更加容易。</span><span class="sxs-lookup"><span data-stu-id="13a34-271">WebSockets protocol makes it much easier to create long-running data transfers between a client and a server.</span></span> <span data-ttu-id="13a34-272">例如，编写聊天应用程序要容易得多，因为你可以在客户端与服务器之间建立真正长时间运行的连接。</span><span class="sxs-lookup"><span data-stu-id="13a34-272">For example, writing a chat application is much easier because you can establish a true long-running connection between a client and a server.</span></span> <span data-ttu-id="13a34-273">不必使用定期轮询或 HTTP 长轮询等解决方法来模拟套接字的行为。</span><span class="sxs-lookup"><span data-stu-id="13a34-273">You do not have to resort to workarounds like periodic polling or HTTP long-polling to simulate the behavior of a socket.</span></span>

<span data-ttu-id="13a34-274">ASP.NET 4.5 和 IIS 8 包含低级别 Websocket 支持，使 ASP.NET 开发人员可以使用托管 Api 在 Websocket 对象上异步读取和写入字符串和二进制数据。</span><span class="sxs-lookup"><span data-stu-id="13a34-274">ASP.NET 4.5 and IIS 8 include low-level WebSockets support, enabling ASP.NET developers to use managed APIs for asynchronously reading and writing both string and binary data on a WebSockets object.</span></span> <span data-ttu-id="13a34-275">对于 ASP.NET 4.5，有 *一个新的* system.servicemodel 命名空间，其中包含用于 websocket 协议的类型。</span><span class="sxs-lookup"><span data-stu-id="13a34-275">For ASP.NET 4.5, there is a new *System.Web.WebSockets* namespace that contains types for working with WebSockets protocol.</span></span>

<span data-ttu-id="13a34-276">浏览器客户端通过创建指向 ASP.NET 应用程序中的 URL 的 DOM *WebSocket* 对象建立 websocket 连接，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="13a34-276">A browser client establishes a WebSockets connection by creating a DOM *WebSocket* object that points to a URL in an ASP.NET application, as in the following example:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample8.cs)]

<span data-ttu-id="13a34-277">可以使用任何类型的模块或处理程序在 ASP.NET 中创建 Websocket 终结点。</span><span class="sxs-lookup"><span data-stu-id="13a34-277">You can create WebSockets endpoints in ASP.NET using any kind of module or handler.</span></span> <span data-ttu-id="13a34-278">在上面的示例中，使用了一个 foo.ashx 文件，因为 foo.ashx 文件是创建处理程序的快速方法。</span><span class="sxs-lookup"><span data-stu-id="13a34-278">In the previous example, an .ashx file was used, because .ashx files are a quick way to create a handler.</span></span>

<span data-ttu-id="13a34-279">根据 Websocket 协议，ASP.NET 应用程序可通过指明请求应从 HTTP GET 请求升级到 Websocket 请求来接受客户端的 Websocket 请求。</span><span class="sxs-lookup"><span data-stu-id="13a34-279">According to the WebSockets protocol, an ASP.NET application accepts a client's WebSockets request by indicating that the request should be upgraded from an HTTP GET request to a WebSockets request.</span></span> <span data-ttu-id="13a34-280">下面的示例说明：</span><span class="sxs-lookup"><span data-stu-id="13a34-280">Here's an example:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample9.cs)]

<span data-ttu-id="13a34-281">*AcceptWebSocketRequest*方法接受函数委托，因为 ASP.NET 将展开当前 HTTP 请求，然后将控制转移到函数委托。</span><span class="sxs-lookup"><span data-stu-id="13a34-281">The *AcceptWebSocketRequest* method accepts a function delegate because ASP.NET unwinds the current HTTP request and then transfers control to the function delegate.</span></span> <span data-ttu-id="13a34-282">从概念上讲，这种方法类似于你使用的方法，在此方法中， *你将在*其中定义执行后台工作的线程启动委托。</span><span class="sxs-lookup"><span data-stu-id="13a34-282">Conceptually this approach is similar to how you use *System.Threading.Thread*, where you define a thread-start delegate in which background work is performed.</span></span>

<span data-ttu-id="13a34-283">在 ASP.NET 和客户端成功完成 Websocket 握手后，ASP.NET 将调用你的委托，并且 Websocket 应用程序开始运行。</span><span class="sxs-lookup"><span data-stu-id="13a34-283">After ASP.NET and the client have successfully completed a WebSockets handshake, ASP.NET calls your delegate and the WebSockets application starts running.</span></span> <span data-ttu-id="13a34-284">下面的代码示例演示了一个简单的回显应用程序，它使用 ASP.NET 中的内置 Websocket 支持：</span><span class="sxs-lookup"><span data-stu-id="13a34-284">The following code example shows a simple echo application that uses the built-in WebSockets support in ASP.NET:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample10.cs)]

<span data-ttu-id="13a34-285">对于 *await* 关键字和基于任务的异步操作，.net 4.5 中的支持是编写 websocket 应用程序的自然。</span><span class="sxs-lookup"><span data-stu-id="13a34-285">The support in .NET 4.5 for the *await* keyword and asynchronous task-based operations is a natural fit for writing WebSockets applications.</span></span> <span data-ttu-id="13a34-286">此代码示例显示 Websocket 请求在 ASP.NET 内完全以异步方式运行。</span><span class="sxs-lookup"><span data-stu-id="13a34-286">The code example shows that a WebSockets request runs completely asynchronously inside ASP.NET.</span></span> <span data-ttu-id="13a34-287">应用程序通过调用 await 套接字异步等待客户端发送消息 *。ReceiveAsync*。</span><span class="sxs-lookup"><span data-stu-id="13a34-287">The application waits asynchronously for a message to be sent from a client by calling *await socket.ReceiveAsync*.</span></span> <span data-ttu-id="13a34-288">同样，可以通过调用 await socket 将异步消息发送到客户端 *。SendAsync*。</span><span class="sxs-lookup"><span data-stu-id="13a34-288">Similarly, you can send an asynchronous message to a client by calling *await socket.SendAsync*.</span></span>

<span data-ttu-id="13a34-289">在浏览器中，应用程序通过 *onmessage* 函数接收 websocket 消息。</span><span class="sxs-lookup"><span data-stu-id="13a34-289">In the browser, an application receives WebSockets messages through an *onmessage* function.</span></span> <span data-ttu-id="13a34-290">若要从浏览器发送消息，请调用*WebSocket* DOM 类型的*send*方法，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="13a34-290">To send a message from a browser, you call the *send* method of the *WebSocket* DOM type, as shown in this example:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample11.cs)]

<span data-ttu-id="13a34-291">将来，我们可能会发布对此功能的更新，这些更新将抽象掉此版本中的 Websocket 应用程序所需的一些低级别编码。</span><span class="sxs-lookup"><span data-stu-id="13a34-291">In the future, we might release updates to this functionality that abstract away some of the low-level coding that is required in this release for WebSockets applications.</span></span>

<a id="_Toc318097384"></a>
### <a name="bundling-and-minification"></a><span data-ttu-id="13a34-292">捆绑和缩小</span><span class="sxs-lookup"><span data-stu-id="13a34-292">Bundling and Minification</span></span>

<span data-ttu-id="13a34-293">绑定使你可以将单个 JavaScript 和 CSS 文件合并成一个可以视为单个文件的捆绑包。</span><span class="sxs-lookup"><span data-stu-id="13a34-293">Bundling lets you combine individual JavaScript and CSS files into a bundle that can be treated like a single file.</span></span> <span data-ttu-id="13a34-294">缩减通过删除不需要的空格和其他字符来会将 JavaScript 和 CSS 文件。</span><span class="sxs-lookup"><span data-stu-id="13a34-294">Minification condenses JavaScript and CSS files by removing whitespace and other characters that are not required.</span></span> <span data-ttu-id="13a34-295">这些功能适用于 Web 窗体、ASP.NET MVC 和网页。</span><span class="sxs-lookup"><span data-stu-id="13a34-295">These features work with Web Forms, ASP.NET MVC, and Web Pages.</span></span>

<span data-ttu-id="13a34-296">使用捆绑类或其子类之一（ScriptBundle 和 StyleBundle）创建捆绑包。</span><span class="sxs-lookup"><span data-stu-id="13a34-296">Bundles are created using the Bundle class or one of its child classes, ScriptBundle and StyleBundle.</span></span> <span data-ttu-id="13a34-297">在配置捆绑的实例后，只需将该绑定添加到全局 BundleCollection 实例，即可将其提供给传入的请求。</span><span class="sxs-lookup"><span data-stu-id="13a34-297">After configuring an instance of a bundle, the bundle is made available to incoming requests by simply adding it to a global BundleCollection instance.</span></span> <span data-ttu-id="13a34-298">在默认模板中，捆绑配置是在 BundleConfig 文件中执行的。</span><span class="sxs-lookup"><span data-stu-id="13a34-298">In the default templates, bundle configuration is performed in a BundleConfig file.</span></span> <span data-ttu-id="13a34-299">此默认配置将为模板使用的所有核心脚本和 css 文件创建捆绑包。</span><span class="sxs-lookup"><span data-stu-id="13a34-299">This default configuration creates bundles for all of the core scripts and css files used by the templates.</span></span>

<span data-ttu-id="13a34-300">使用几种可能的帮助程序方法之一在视图中引用绑定。</span><span class="sxs-lookup"><span data-stu-id="13a34-300">Bundles are referenced from within views by using one of a couple possible helper methods.</span></span> <span data-ttu-id="13a34-301">为了支持在调试和发布模式下为捆绑包呈现不同的标记，ScriptBundle 和 StyleBundle 类具有 helper 方法，即 Render。</span><span class="sxs-lookup"><span data-stu-id="13a34-301">In order to support rendering different markup for a bundle when in debug vs. release mode, the ScriptBundle and StyleBundle classes have the helper method, Render.</span></span> <span data-ttu-id="13a34-302">处于调试模式时，Render 将为捆绑包中的每个资源生成标记。</span><span class="sxs-lookup"><span data-stu-id="13a34-302">When in debug mode, Render will generate markup for each resource in the bundle.</span></span> <span data-ttu-id="13a34-303">在发布模式下，Render 将为整个绑定生成一个标记元素。</span><span class="sxs-lookup"><span data-stu-id="13a34-303">When in release mode, Render will generate a single markup element for the entire bundle.</span></span> <span data-ttu-id="13a34-304">可以通过在 web.config 中修改编译元素的 debug 特性来完成调试和发布模式间的切换，如下所示：</span><span class="sxs-lookup"><span data-stu-id="13a34-304">Toggling between debug and release mode can be accomplished by modifying the debug attribute of the compilation element in web.config as shown below:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample12.xml)]

<span data-ttu-id="13a34-305">此外，还可以通过 Bundletable.enableoptimization. EnableOptimizations 属性直接设置启用或禁用优化。</span><span class="sxs-lookup"><span data-stu-id="13a34-305">Additionally, enabling or disabling optimization can be set directly via the BundleTable.EnableOptimizations property.</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample13.cs)]

<span data-ttu-id="13a34-306">当捆绑文件时，将首先按字母顺序对文件进行排序， (它们在 **解决方案资源管理器**) 中的显示方式。</span><span class="sxs-lookup"><span data-stu-id="13a34-306">When files are bundled, they are first sorted alphabetically (the way they are displayed in **Solution Explorer**).</span></span> <span data-ttu-id="13a34-307">然后对它们进行组织，以便先加载 (的已知库及其自定义扩展插件，例如 jQuery、MooTools 和 Dojo) 。</span><span class="sxs-lookup"><span data-stu-id="13a34-307">They are then organized so that known libraries and their custom extensions (such as jQuery, MooTools, and Dojo) are loaded first.</span></span> <span data-ttu-id="13a34-308">例如，如上所示的 "脚本" 文件夹的绑定最终顺序如下：</span><span class="sxs-lookup"><span data-stu-id="13a34-308">For example, the final order for the bundling of the Scripts folder as shown above will be:</span></span>

1. <span data-ttu-id="13a34-309">jquery-1.6.2.js</span><span class="sxs-lookup"><span data-stu-id="13a34-309">jquery-1.6.2.js</span></span>
2. <span data-ttu-id="13a34-310">jquery-ui.js</span><span class="sxs-lookup"><span data-stu-id="13a34-310">jquery-ui.js</span></span>
3. <span data-ttu-id="13a34-311">jquery.tools.js</span><span class="sxs-lookup"><span data-stu-id="13a34-311">jquery.tools.js</span></span>
4. <span data-ttu-id="13a34-312">a.js</span><span class="sxs-lookup"><span data-stu-id="13a34-312">a.js</span></span>

<span data-ttu-id="13a34-313">CSS 文件也按字母顺序进行排序，然后再进行重新组织，以便在任何其他文件之前进行重置。</span><span class="sxs-lookup"><span data-stu-id="13a34-313">CSS files are also sorted alphabetically and then reorganized so that reset.css and normalize.css come before any other file.</span></span> <span data-ttu-id="13a34-314">上面所示的样式文件夹的绑定的最终排序如下：</span><span class="sxs-lookup"><span data-stu-id="13a34-314">The final sorting of the bundling of the Styles folder shown above will be this:</span></span>

1. <span data-ttu-id="13a34-315">重置 .css</span><span class="sxs-lookup"><span data-stu-id="13a34-315">reset.css</span></span>
2. <span data-ttu-id="13a34-316">内容 .css</span><span class="sxs-lookup"><span data-stu-id="13a34-316">content.css</span></span>
3. <span data-ttu-id="13a34-317">forms .css</span><span class="sxs-lookup"><span data-stu-id="13a34-317">forms.css</span></span>
4. <span data-ttu-id="13a34-318">globals</span><span class="sxs-lookup"><span data-stu-id="13a34-318">globals.css</span></span>
5. <span data-ttu-id="13a34-319">menu .css</span><span class="sxs-lookup"><span data-stu-id="13a34-319">menu.css</span></span>
6. <span data-ttu-id="13a34-320">样式 .css</span><span class="sxs-lookup"><span data-stu-id="13a34-320">styles.css</span></span>

<a id="_Toc_perf"></a>
### <a name="performance-improvements-for-web-hosting"></a><span data-ttu-id="13a34-321">Web 托管的性能改进</span><span class="sxs-lookup"><span data-stu-id="13a34-321">Performance Improvements for Web Hosting</span></span>

<span data-ttu-id="13a34-322">.NET Framework 4.5 和 Windows 8 中引入了一些功能，可帮助你为 web 服务器工作负荷实现显著的性能提升。</span><span class="sxs-lookup"><span data-stu-id="13a34-322">The .NET Framework 4.5 and Windows 8 introduce features that can help you achieve a significant performance boost for web-server workloads.</span></span> <span data-ttu-id="13a34-323">这包括在启动时间和使用 ASP.NET 的 web 托管站点的内存占用量中，最多可降低 35% ) 的 (。</span><span class="sxs-lookup"><span data-stu-id="13a34-323">This includes a reduction (up to 35%) in both startup time and in the memory footprint of web hosting sites that use ASP.NET.</span></span>

<a id="_Toc_perf_1"></a>
#### <a name="key-performance-factors"></a><span data-ttu-id="13a34-324">关键绩效因素</span><span class="sxs-lookup"><span data-stu-id="13a34-324">Key performance factors</span></span>

<span data-ttu-id="13a34-325">理想情况下，所有网站都应该处于活动状态，并且在内存中，以便在每次请求时都能快速响应下一个请求。</span><span class="sxs-lookup"><span data-stu-id="13a34-325">Ideally, all websites should be active and in memory to assure quick response to the next request, whenever it comes.</span></span> <span data-ttu-id="13a34-326">影响站点响应能力的因素包括：</span><span class="sxs-lookup"><span data-stu-id="13a34-326">Factors that can affect site responsiveness include:</span></span>

- <span data-ttu-id="13a34-327">在应用程序池回收后重新启动站点所用的时间。</span><span class="sxs-lookup"><span data-stu-id="13a34-327">The time it takes for a site to restart after an app pool recycles.</span></span> <span data-ttu-id="13a34-328">这是在站点程序集不再处于内存中时，为站点启动 web 服务器进程所用的时间。</span><span class="sxs-lookup"><span data-stu-id="13a34-328">This is the time it takes to launch a web server process for the site when the site assemblies are no longer in memory.</span></span> <span data-ttu-id="13a34-329"> (平台程序集仍在内存中，因为它们被其他站点使用。 ) 这种情况称为 "冷站点、热框架启动" 或简称为 "冷站点启动"。</span><span class="sxs-lookup"><span data-stu-id="13a34-329">(The platform assemblies are still in memory, since they are used by other sites.) This situation is referred to as "cold site, warm framework startup" or just "cold site startup."</span></span>
- <span data-ttu-id="13a34-330">站点占用的内存量。</span><span class="sxs-lookup"><span data-stu-id="13a34-330">How much memory the site occupies.</span></span> <span data-ttu-id="13a34-331">这是 "每个站点的内存占用量" 或 "非共享工作集"。</span><span class="sxs-lookup"><span data-stu-id="13a34-331">Terms for this are "per-site memory consumption" or "unshared working set."</span></span>

<span data-ttu-id="13a34-332">新性能改进重点介绍了这两个因素。</span><span class="sxs-lookup"><span data-stu-id="13a34-332">The new performance improvements focus on both of these factors.</span></span>

<a id="_Toc_perf_2"></a>
#### <a name="requirements-for-new-performance-features"></a><span data-ttu-id="13a34-333">新性能功能的要求</span><span class="sxs-lookup"><span data-stu-id="13a34-333">Requirements for New Performance Features</span></span>

<span data-ttu-id="13a34-334">新功能的要求可划分为以下类别：</span><span class="sxs-lookup"><span data-stu-id="13a34-334">The requirements for the new features can be broken down into these categories:</span></span>

- <span data-ttu-id="13a34-335">.NET Framework 4 上运行的改进。</span><span class="sxs-lookup"><span data-stu-id="13a34-335">Improvements that run on the .NET Framework 4.</span></span>
- <span data-ttu-id="13a34-336">需要 .NET Framework 4.5 的改进，但可以在任何 Windows 版本上运行。</span><span class="sxs-lookup"><span data-stu-id="13a34-336">Improvements that require the .NET Framework 4.5 but can run on any version of Windows.</span></span>
- <span data-ttu-id="13a34-337">仅适用于在 Windows 8 上运行的 .NET Framework 4.5 的改进。</span><span class="sxs-lookup"><span data-stu-id="13a34-337">Improvements that are available only with .NET Framework 4.5 running on Windows 8.</span></span>

<span data-ttu-id="13a34-338">性能会随你能够启用的每个改进级别而增加。</span><span class="sxs-lookup"><span data-stu-id="13a34-338">Performance increases with each level of improvement that you are able to enable.</span></span>

<span data-ttu-id="13a34-339">.NET Framework 的部分4.5 改进利用适用于其他方案的更广泛的性能功能。</span><span class="sxs-lookup"><span data-stu-id="13a34-339">Some of the .NET Framework 4.5 improvements take advantage of broader performance features that apply to other scenarios as well.</span></span>

<a id="_Toc_perf_3"></a>
#### <a name="sharing-common-assemblies"></a><span data-ttu-id="13a34-340">共享公用程序集</span><span class="sxs-lookup"><span data-stu-id="13a34-340">Sharing Common Assemblies</span></span>

<span data-ttu-id="13a34-341">**要求**： .NET Framework 4 和 Visual Studio 11 开发人员预览版 SDK</span><span class="sxs-lookup"><span data-stu-id="13a34-341">**Requirement**: .NET Framework 4 and Visual Studio 11 Developer Preview SDK</span></span>

<span data-ttu-id="13a34-342">服务器上的不同站点通常使用相同的帮助程序集 (例如，初学者工具包或示例应用程序) 中的程序集。</span><span class="sxs-lookup"><span data-stu-id="13a34-342">Different sites on a server often use the same helper assemblies (for example, assemblies from a starter kit or sample application).</span></span> <span data-ttu-id="13a34-343">每个站点在其 Bin 目录中都有其自己的这些程序集副本。</span><span class="sxs-lookup"><span data-stu-id="13a34-343">Each site has its own copy of these assemblies in its Bin directory.</span></span> <span data-ttu-id="13a34-344">即使程序集的对象代码是相同的，它们也是物理上独立的程序集，因此，每个程序集都必须在冷站点启动期间单独读取，并在内存中单独保存。</span><span class="sxs-lookup"><span data-stu-id="13a34-344">Even though the object code for the assemblies is identical, they're physically separate assemblies, so each assembly has to be read separately during cold site startup and kept separately in memory.</span></span>

<span data-ttu-id="13a34-345">新的暂存功能可解决这一低效，同时降低 RAM 要求和加载时间。</span><span class="sxs-lookup"><span data-stu-id="13a34-345">The new interning functionality solves this inefficiency and reduces both RAM requirements and load time.</span></span> <span data-ttu-id="13a34-346">通过使用留用功能，Windows 可以在文件系统中保留每个程序集的单个副本，并将网站 Bin 文件夹中的各个程序集替换为指向单个副本的符号链接。</span><span class="sxs-lookup"><span data-stu-id="13a34-346">Interning lets Windows keep a single copy of each assembly in the file system, and individual assemblies in the site Bin folders are replaced with symbolic links to the single copy.</span></span> <span data-ttu-id="13a34-347">如果单个站点需要不同版本的程序集，则符号链接将替换为该程序集的新版本，并且仅影响该站点。</span><span class="sxs-lookup"><span data-stu-id="13a34-347">If an individual site needs a distinct version of the assembly, the symbolic link is replaced by the new version of the assembly, and only that site is affected.</span></span>

<span data-ttu-id="13a34-348">使用符号链接共享程序集需要一个名为 aspnetintern.exe 的新工具 \_ ，它使您可以创建和管理暂存的程序集的存储区。</span><span class="sxs-lookup"><span data-stu-id="13a34-348">Sharing assemblies using symbolic links requires a new tool named aspnet\_intern.exe, which lets you create and manage the store of interned assemblies.</span></span> <span data-ttu-id="13a34-349">它作为 Visual Studio 11 开发人员预览版 SDK 的一部分提供。</span><span class="sxs-lookup"><span data-stu-id="13a34-349">It is provided as a part of the Visual Studio 11 Developer Preview SDK.</span></span> <span data-ttu-id="13a34-350">但 (，它将在仅安装了 .NET Framework 4 的系统上运行，前提是已安装了最新的 [更新](https://support.microsoft.com/kb/2468871)。 ) </span><span class="sxs-lookup"><span data-stu-id="13a34-350">(However, it will work on a system that has only the .NET Framework 4 installed, assuming you have installed the latest [update](https://support.microsoft.com/kb/2468871).)</span></span>

<span data-ttu-id="13a34-351">为了确保所有符合条件的程序集都已留用，你可以定期运行 aspnet \_intern.exe (例如，一周作为计划的任务) 。</span><span class="sxs-lookup"><span data-stu-id="13a34-351">To make sure all eligible assemblies have been interned, you run aspnet\_intern.exe periodically (for example, once a week as a scheduled task).</span></span> <span data-ttu-id="13a34-352">典型用法如下所示：</span><span class="sxs-lookup"><span data-stu-id="13a34-352">A typical use is as follows:</span></span>

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample14.cmd)]

<span data-ttu-id="13a34-353">若要查看所有选项，请不带参数运行该工具。</span><span class="sxs-lookup"><span data-stu-id="13a34-353">To see all options, run the tool with no arguments.</span></span>

<a id="_Toc_perf_4"></a>
#### <a name="using-multi-core-jit-compilation-for-faster-startup"></a><span data-ttu-id="13a34-354">使用多核心 JIT 编译加快启动速度</span><span class="sxs-lookup"><span data-stu-id="13a34-354">Using multi-Core JIT compilation for faster startup</span></span>

<span data-ttu-id="13a34-355">**要求**： .NET Framework 4。5</span><span class="sxs-lookup"><span data-stu-id="13a34-355">**Requirement**: .NET Framework 4.5</span></span>

<span data-ttu-id="13a34-356">对于冷站点启动，不仅必须从磁盘读取程序集，而且必须对站点进行 JIT 编译。</span><span class="sxs-lookup"><span data-stu-id="13a34-356">For a cold site startup, not only do assemblies have to be read from disk, but the site must be JIT-compiled.</span></span> <span data-ttu-id="13a34-357">对于复杂站点，这可能会增加很多延迟。</span><span class="sxs-lookup"><span data-stu-id="13a34-357">For a complex site, this can add significant delays.</span></span> <span data-ttu-id="13a34-358">.NET Framework 4.5 中的一种新的通用技术可通过跨可用处理器核心传播 JIT 编译来减少这些延迟。</span><span class="sxs-lookup"><span data-stu-id="13a34-358">A new general-purpose technique in the .NET Framework 4.5 reduces these delays by spreading JIT-compilation across available processor cores.</span></span> <span data-ttu-id="13a34-359">它通过使用在上一次启动站点时收集的信息，尽快实现此功能。</span><span class="sxs-lookup"><span data-stu-id="13a34-359">It does this as much and as early as possible by using information gathered during previous launches of the site.</span></span> <span data-ttu-id="13a34-360">此功能由 [ProfileOptimization. StartProfile](https://msdn.microsoft.com/library/system.runtime.profileoptimization.startprofile(VS.110).aspx) 方法实现。</span><span class="sxs-lookup"><span data-stu-id="13a34-360">This functionality implemented by the [System.Runtime.ProfileOptimization.StartProfile](https://msdn.microsoft.com/library/system.runtime.profileoptimization.startprofile(VS.110).aspx) method.</span></span>

<span data-ttu-id="13a34-361">默认情况下，在 ASP.NET 中启用了使用多个核心的 JIT 编译，因此您无需执行任何操作即可利用此功能。</span><span class="sxs-lookup"><span data-stu-id="13a34-361">JIT-compiling using multiple cores is enabled by default in ASP.NET, so you do not need to do anything to take advantage of this feature.</span></span> <span data-ttu-id="13a34-362">如果要禁用此功能，请在 Web.config 文件中设置以下设置：</span><span class="sxs-lookup"><span data-stu-id="13a34-362">If you want to disable this feature, make the following setting in the Web.config file:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample15.xml)]

<a id="_Toc_perf_5"></a>
#### <a name="tuning-garbage-collection-to-optimize-for-memory"></a><span data-ttu-id="13a34-363">优化垃圾回收以优化内存</span><span class="sxs-lookup"><span data-stu-id="13a34-363">Tuning garbage collection to optimize for memory</span></span>

<span data-ttu-id="13a34-364">**要求**： .NET Framework 4。5</span><span class="sxs-lookup"><span data-stu-id="13a34-364">**Requirement**: .NET Framework 4.5</span></span>

<span data-ttu-id="13a34-365">站点运行后，使用垃圾回收器 (GC) 堆会成为其内存消耗的重要因素。</span><span class="sxs-lookup"><span data-stu-id="13a34-365">Once a site is running, its use of the garbage-collector (GC) heap can be a significant factor in its memory consumption.</span></span> <span data-ttu-id="13a34-366">与任何垃圾回收器一样，.NET Framework GC 在 CPU 时间 (频率和集合的重要性之间进行权衡) 和内存占用 (额外空间，) 使用新的、释放或自由的对象。</span><span class="sxs-lookup"><span data-stu-id="13a34-366">Like any garbage collector, the .NET Framework GC makes tradeoffs between CPU time (frequency and significance of collections) and memory consumption (extra space that is used for new, freed, or free-able objects).</span></span> <span data-ttu-id="13a34-367">对于以前的版本，我们提供了有关如何配置 GC 以实现适当平衡 (例如，请参阅 [ASP.NET 2.0/3.5 共享的托管配置](https://www.iis.net/learn/web-hosting/web-server-for-shared-hosting/aspnet-20-35-shared-hosting-configuration)) 。</span><span class="sxs-lookup"><span data-stu-id="13a34-367">For previous releases, we have provided guidance on how to configure the GC to achieve the right balance (for example, see [ASP.NET 2.0/3.5 Shared Hosting Configuration](https://www.iis.net/learn/web-hosting/web-server-for-shared-hosting/aspnet-20-35-shared-hosting-configuration)).</span></span>

<span data-ttu-id="13a34-368">对于 .NET Framework 4.5，而不是使用多个独立的设置，提供了工作负荷定义的配置设置，这些设置可启用所有先前推荐的 GC 设置以及新的优化功能，从而为每个站点的工作集提供附加性能。</span><span class="sxs-lookup"><span data-stu-id="13a34-368">For the .NET Framework 4.5, instead of multiple standalone settings, a workload-defined configuration setting is available that enables all of the previously recommended GC settings as well as new tuning that delivers additional performance for the per-site working set.</span></span>

<span data-ttu-id="13a34-369">若要启用 GC 内存优化，请将以下设置添加到 Windows\Microsoft.NET\Framework\v4.0.30319\aspnet.config 文件：</span><span class="sxs-lookup"><span data-stu-id="13a34-369">To enable GC memory tuning, add the following setting to the Windows\Microsoft.NET\Framework\v4.0.30319\aspnet.config file:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample16.xml)]

<span data-ttu-id="13a34-370"> (如果你熟悉以前的 aspnet.config 更改指南，请注意，此设置将替换旧设置，例如，无需设置 r、t 等。无需删除旧设置。 ) </span><span class="sxs-lookup"><span data-stu-id="13a34-370">(If you're familiar with the previous guidance for changes to aspnet.config, note that this setting replaces the old settings — for example, there is no need to set gcServer, gcConcurrent, etc. You do not have to remove the old settings.)</span></span>

<a id="_Toc_perf_6"></a>
#### <a name="prefetching-for-web-applications"></a><span data-ttu-id="13a34-371">对 web 应用程序的预提取</span><span class="sxs-lookup"><span data-stu-id="13a34-371">Prefetching for web applications</span></span>

<span data-ttu-id="13a34-372">**要求**：在 Windows 8 上运行 .NET Framework 4。5</span><span class="sxs-lookup"><span data-stu-id="13a34-372">**Requirement**: .NET Framework 4.5 running on Windows 8</span></span>

<span data-ttu-id="13a34-373">对于多个版本，Windows 包含了称为 [prefetcher](http://en.wikipedia.org/wiki/Prefetcher) 的技术，可减少应用程序启动时的磁盘读取成本。</span><span class="sxs-lookup"><span data-stu-id="13a34-373">For several releases, Windows has included a technology known as the [prefetcher](http://en.wikipedia.org/wiki/Prefetcher) that reduces the disk-read cost of application startup.</span></span> <span data-ttu-id="13a34-374">由于冷启动是客户端应用程序的主要问题，因此此技术尚未包含在 Windows Server 中，后者仅包含对服务器非常重要的组件。</span><span class="sxs-lookup"><span data-stu-id="13a34-374">Because cold startup is a problem predominantly for client applications, this technology has not been included in Windows Server, which includes only components that are essential to a server.</span></span> <span data-ttu-id="13a34-375">预提取功能现已在最新版本的 Windows Server 中提供，可在其中优化各个网站的启动。</span><span class="sxs-lookup"><span data-stu-id="13a34-375">Prefetching is now available in the latest version of Windows Server, where it can optimize the launch of individual websites.</span></span>

<span data-ttu-id="13a34-376">对于 Windows Server，默认情况下不启用 prefetcher。</span><span class="sxs-lookup"><span data-stu-id="13a34-376">For Windows Server, the prefetcher is not enabled by default.</span></span> <span data-ttu-id="13a34-377">若要为高密度 web 宿主启用和配置 prefetcher，请在命令行中运行以下命令集：</span><span class="sxs-lookup"><span data-stu-id="13a34-377">To enable and configure the prefetcher for high-density web hosting, run the following set of commands at the command line:</span></span>

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample17.cmd)]

<span data-ttu-id="13a34-378">然后，若要将 prefetcher 与 ASP.NET 应用程序集成，请将以下内容添加到 Web.config 文件：</span><span class="sxs-lookup"><span data-stu-id="13a34-378">Then, to integrate the prefetcher with ASP.NET applications, add the following to the Web.config file:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample18.xml)]

<a id="_Toc318097385"></a>
## <a name="aspnet-web-forms"></a><span data-ttu-id="13a34-379">ASP.NET Web 窗体</span><span class="sxs-lookup"><span data-stu-id="13a34-379">ASP.NET Web Forms</span></span>

<a id="_Toc318097386"></a>
### <a name="strongly-typed-data-controls"></a><span data-ttu-id="13a34-380">强类型化数据控件</span><span class="sxs-lookup"><span data-stu-id="13a34-380">Strongly Typed Data Controls</span></span>

<span data-ttu-id="13a34-381">在 ASP.NET 4.5 中，Web 窗体包含一些用于处理数据的改进。</span><span class="sxs-lookup"><span data-stu-id="13a34-381">In ASP.NET 4.5, Web Forms includes some improvements for working with data.</span></span> <span data-ttu-id="13a34-382">第一次改进是强类型化的数据控件。</span><span class="sxs-lookup"><span data-stu-id="13a34-382">The first improvement is strongly typed data controls.</span></span> <span data-ttu-id="13a34-383">对于以前版本的 ASP.NET 中的 Web 窗体控件，使用 *Eval* 和数据绑定表达式显示数据绑定值：</span><span class="sxs-lookup"><span data-stu-id="13a34-383">For Web Forms controls in previous versions of ASP.NET, you display a data-bound value using *Eval* and a data-binding expression:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample19.aspx)]

<span data-ttu-id="13a34-384">对于双向数据绑定，可使用 *Bind*：</span><span class="sxs-lookup"><span data-stu-id="13a34-384">For two-way data binding, you use *Bind*:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample20.aspx)]

<span data-ttu-id="13a34-385">在运行时，这些调用使用反射来读取指定成员的值，然后在标记中显示结果。</span><span class="sxs-lookup"><span data-stu-id="13a34-385">At run time, these calls use reflection to read the value of the specified member and then display the result in the markup.</span></span> <span data-ttu-id="13a34-386">利用这种方法，可以轻松地将数据绑定到任意 unshaped 数据。</span><span class="sxs-lookup"><span data-stu-id="13a34-386">This approach makes it easy to data bind against arbitrary, unshaped data.</span></span>

<span data-ttu-id="13a34-387">但是，这种类似于这样的数据绑定表达式并不支持用于成员名称、导航 (（如中转到定义) 或对这些名称进行编译时检查）等功能。</span><span class="sxs-lookup"><span data-stu-id="13a34-387">However, data-binding expressions like this don't support features like IntelliSense for member names, navigation (like Go To Definition), or compile-time checking for these names.</span></span>

<span data-ttu-id="13a34-388">为了解决此问题，ASP.NET 4.5 添加了声明控件绑定到的数据的数据类型的功能。</span><span class="sxs-lookup"><span data-stu-id="13a34-388">To address this issue, ASP.NET 4.5 adds the ability to declare the data type of the data that a control is bound to.</span></span> <span data-ttu-id="13a34-389">使用新的 *ItemType* 属性来执行此操作。</span><span class="sxs-lookup"><span data-stu-id="13a34-389">You do this using the new *ItemType* property.</span></span> <span data-ttu-id="13a34-390">设置此属性时，数据绑定表达式的作用域中提供两个新的类型化变量： *Item* 和 *BindItem*。</span><span class="sxs-lookup"><span data-stu-id="13a34-390">When you set this property, two new typed variables are available in the scope of data-binding expressions: *Item* and *BindItem*.</span></span> <span data-ttu-id="13a34-391">由于变量是强类型的，因此你可以获得 Visual Studio 开发体验的全部好处。</span><span class="sxs-lookup"><span data-stu-id="13a34-391">Because the variables are strongly typed, you get the full benefits of the Visual Studio development experience.</span></span>

<span data-ttu-id="13a34-392">对于双向数据绑定表达式，请使用 *BindItem* 变量：</span><span class="sxs-lookup"><span data-stu-id="13a34-392">For two-way data-binding expressions, use the *BindItem* variable:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample21.aspx)]

<span data-ttu-id="13a34-393">ASP.NET Web 窗体框架中支持数据绑定的大多数控件已更新，以支持 *ItemType* 属性。</span><span class="sxs-lookup"><span data-stu-id="13a34-393">Most controls in the ASP.NET Web Forms framework that support data binding have been updated to support the *ItemType* property.</span></span>

<a id="_Toc318097387"></a>
### <a name="model-binding"></a><span data-ttu-id="13a34-394">模型绑定</span><span class="sxs-lookup"><span data-stu-id="13a34-394">Model Binding</span></span>

<span data-ttu-id="13a34-395">模型绑定将 ASP.NET Web 窗体控件中的数据绑定扩展到使用以代码为中心的数据访问中。</span><span class="sxs-lookup"><span data-stu-id="13a34-395">Model binding extends data binding in ASP.NET Web Forms controls to work with code-focused data access.</span></span> <span data-ttu-id="13a34-396">它结合了 *ObjectDataSource* 控件中的概念和 ASP.NET MVC 中的模型绑定。</span><span class="sxs-lookup"><span data-stu-id="13a34-396">It incorporates concepts from the *ObjectDataSource* control and from model binding in ASP.NET MVC.</span></span>

<a id="_Toc318097388"></a>
#### <a name="selecting-data"></a><span data-ttu-id="13a34-397">选择数据</span><span class="sxs-lookup"><span data-stu-id="13a34-397">Selecting data</span></span>

<span data-ttu-id="13a34-398">若要将数据控件配置为使用模型绑定来选择数据，请将控件的 *SelectMethod* 属性设置为该页的代码中的方法的名称。</span><span class="sxs-lookup"><span data-stu-id="13a34-398">To configure a data control to use model binding to select data, you set the control's *SelectMethod* property to the name of a method in the page's code.</span></span> <span data-ttu-id="13a34-399">数据控件在页面生命周期中的适当时间调用方法，并自动绑定返回的数据。</span><span class="sxs-lookup"><span data-stu-id="13a34-399">The data control calls the method at the appropriate time in the page life cycle and automatically binds the returned data.</span></span> <span data-ttu-id="13a34-400">无需显式调用 *DataBind* 方法。</span><span class="sxs-lookup"><span data-stu-id="13a34-400">There's no need to explicitly call the *DataBind* method.</span></span>

<span data-ttu-id="13a34-401">在下面的示例中， *GridView* 控件配置为使用名为 *GetCategories*的方法：</span><span class="sxs-lookup"><span data-stu-id="13a34-401">In the following example, the *GridView* control is configured to use a method named *GetCategories*:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample22.aspx)]

<span data-ttu-id="13a34-402">在该页的代码中创建 *GetCategories* 方法。</span><span class="sxs-lookup"><span data-stu-id="13a34-402">You create the *GetCategories* method in the page's code.</span></span> <span data-ttu-id="13a34-403">对于简单的选择操作，方法不需要任何参数，并且应返回 *IEnumerable* 或 *IQueryable* 对象。</span><span class="sxs-lookup"><span data-stu-id="13a34-403">For a simple select operation, the method needs no parameters and should return an *IEnumerable* or *IQueryable* object.</span></span> <span data-ttu-id="13a34-404">如果将新*的 ItemType*属性设置 (使强类型的数据绑定表达式（如之前) 的[强类型数据控件](#_Toc318097386)所述），则应返回这些接口的泛型版本， \* &lt; &gt; 即 IEnumerable\* t 或*IQueryable &lt; t &gt; *，其中*t*参数与*ItemType*属性的类型匹配 (例如， \*IQueryable &lt; 类别 &gt; \*) 。</span><span class="sxs-lookup"><span data-stu-id="13a34-404">If the new *ItemType* property is set (which enables strongly typed data-binding expressions, as explained under [Strongly Typed Data Controls](#_Toc318097386) earlier), the generic versions of these interfaces should be returned — *IEnumerable&lt;T&gt;* or *IQueryable&lt;T&gt;*, with the *T* parameter matching the type of the *ItemType* property (for example, *IQueryable&lt;Category&gt;*).</span></span>

<span data-ttu-id="13a34-405">下面的示例演示了 *GetCategories* 方法的代码。</span><span class="sxs-lookup"><span data-stu-id="13a34-405">The following example shows the code for a *GetCategories* method.</span></span> <span data-ttu-id="13a34-406">此示例将实体框架 Code First 模型与 Northwind 示例数据库一起使用。</span><span class="sxs-lookup"><span data-stu-id="13a34-406">This example uses the Entity Framework Code First model with the Northwind sample database.</span></span> <span data-ttu-id="13a34-407">此代码可确保查询通过 *Include* 方法返回每个类别的相关产品的详细信息。</span><span class="sxs-lookup"><span data-stu-id="13a34-407">The code makes sure that the query returns details of the related products for each category by way of the *Include* method.</span></span> <span data-ttu-id="13a34-408"> (这可确保标记中的 *TemplateField* 元素显示每个类别中的产品计数，无需 [选择 "n + 1](http://stackoverflow.com/questions/97197/what-is-the-n1-selects-problem)"。 ) </span><span class="sxs-lookup"><span data-stu-id="13a34-408">(This ensures that the *TemplateField* element in the markup displays the count of products in each category without requiring an [n+1 select](http://stackoverflow.com/questions/97197/what-is-the-n1-selects-problem).)</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample23.cs)]

<span data-ttu-id="13a34-409">当页面运行时， *GridView* 控件会自动调用 *GetCategories* 方法，并使用配置的字段呈现返回的数据：</span><span class="sxs-lookup"><span data-stu-id="13a34-409">When the page runs, the *GridView* control calls the *GetCategories* method automatically and renders the returned data using the configured fields:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image2.png)

<span data-ttu-id="13a34-410">因为 select 方法返回 *IQueryable* 对象，所以在执行该查询之前， *GridView* 控件可以进一步对其进行操作。</span><span class="sxs-lookup"><span data-stu-id="13a34-410">Because the select method returns an *IQueryable* object, the *GridView* control can further manipulate the query before executing it.</span></span> <span data-ttu-id="13a34-411">例如，在执行所返回的*IQueryable*对象之前， *GridView*控件可以添加查询表达式进行排序和分页，以便这些操作由基础 LINQ 提供程序执行。</span><span class="sxs-lookup"><span data-stu-id="13a34-411">For example, the *GridView* control can add query expressions for sorting and paging to the returned *IQueryable* object before it is executed, so that those operations are performed by the underlying LINQ provider.</span></span> <span data-ttu-id="13a34-412">在这种情况下，实体框架将确保在数据库中执行这些操作。</span><span class="sxs-lookup"><span data-stu-id="13a34-412">In this case, Entity Framework will ensure those operations are performed in the database.</span></span>

<span data-ttu-id="13a34-413">下面的示例演示了修改为允许排序和分页的 *GridView* 控件：</span><span class="sxs-lookup"><span data-stu-id="13a34-413">The following example shows the *GridView* control modified to allow sorting and paging:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample24.aspx)]

<span data-ttu-id="13a34-414">现在，当页面运行时，控件可以确保只显示当前数据页，并按选定列排序：</span><span class="sxs-lookup"><span data-stu-id="13a34-414">Now when the page runs, the control can make sure that only the current page of data is displayed and that it's ordered by the selected column:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image3.png)

<span data-ttu-id="13a34-415">若要筛选返回的数据，必须将参数添加到 select 方法。</span><span class="sxs-lookup"><span data-stu-id="13a34-415">To filter the returned data, parameters have to be added to the select method.</span></span> <span data-ttu-id="13a34-416">在运行时，模型绑定将填充这些参数，您可以使用它们在返回数据之前更改查询。</span><span class="sxs-lookup"><span data-stu-id="13a34-416">These parameters will be populated by the model binding at run time, and you can use them to alter the query before returning the data.</span></span>

<span data-ttu-id="13a34-417">例如，假设您希望允许用户通过在查询字符串中输入关键字来筛选产品。</span><span class="sxs-lookup"><span data-stu-id="13a34-417">For example, assume that you want to let users filter products by entering a keyword in the query string.</span></span> <span data-ttu-id="13a34-418">您可以将参数添加到方法，并更新代码以使用参数值：</span><span class="sxs-lookup"><span data-stu-id="13a34-418">You can add a parameter to the method and update the code to use the parameter value:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample25.cs)]

<span data-ttu-id="13a34-419">如果为*关键字*提供了值，则此代码包含*Where*表达式，然后返回查询结果。</span><span class="sxs-lookup"><span data-stu-id="13a34-419">This code includes a *Where* expression if a value is provided for *keyword* and then returns the query results.</span></span>

<a id="_Toc318097389"></a>
#### <a name="value-providers"></a><span data-ttu-id="13a34-420">值提供程序</span><span class="sxs-lookup"><span data-stu-id="13a34-420">Value providers</span></span>

<span data-ttu-id="13a34-421">前面的示例并不特定于 *关键字* 参数的值来自何处。</span><span class="sxs-lookup"><span data-stu-id="13a34-421">The previous example was not specific about where the value for the *keyword* parameter was coming from.</span></span> <span data-ttu-id="13a34-422">若要指示此信息，可以使用参数特性。</span><span class="sxs-lookup"><span data-stu-id="13a34-422">To indicate this information, you can use a parameter attribute.</span></span> <span data-ttu-id="13a34-423">在此示例中，可以使用*ModelBinding*命名空间中的*QueryStringAttribute*类：</span><span class="sxs-lookup"><span data-stu-id="13a34-423">For this example, you can use the *QueryStringAttribute* class that's in the *System.Web.ModelBinding* namespace:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample26.cs)]

<span data-ttu-id="13a34-424">这将指示模型绑定在运行时尝试将值从查询字符串绑定到 *关键字* 参数。</span><span class="sxs-lookup"><span data-stu-id="13a34-424">This instructs model binding to try to bind a value from the query string to the *keyword* parameter at run time.</span></span> <span data-ttu-id="13a34-425"> (这可能会涉及到执行类型转换，但在这种情况下不会出现这种情况。 ) 如果无法提供值并且类型不可为 null，则会引发异常。</span><span class="sxs-lookup"><span data-stu-id="13a34-425">(This might involve performing type conversion, although it doesn't in this case.) If a value cannot be provided and the type is non-nullable, an exception is thrown.</span></span>

<span data-ttu-id="13a34-426">这些方法的值的源称为值提供程序，参数属性指示要使用的值提供程序称为值提供程序特性。</span><span class="sxs-lookup"><span data-stu-id="13a34-426">The sources of values for these methods are referred to as value providers, and the parameter attributes that indicate which value provider to use are referred to as value provider attributes.</span></span> <span data-ttu-id="13a34-427">Web 窗体将包含 Web 窗体应用程序中的所有典型用户输入源的值提供程序和相应属性，例如查询字符串、cookie、窗体值、控件、视图状态、会话状态和配置文件属性。</span><span class="sxs-lookup"><span data-stu-id="13a34-427">Web Forms will include value providers and corresponding attributes for all of the typical sources of user input in a Web Forms application, such as the query string, cookies, form values, controls, view state, session state, and profile properties.</span></span> <span data-ttu-id="13a34-428">你还可以编写自定义值提供程序。</span><span class="sxs-lookup"><span data-stu-id="13a34-428">You can also write custom value providers.</span></span>

<span data-ttu-id="13a34-429">默认情况下，参数名称用作查找值提供程序集合中的值的键。</span><span class="sxs-lookup"><span data-stu-id="13a34-429">By default, the parameter name is used as the key to find a value in the value provider collection.</span></span> <span data-ttu-id="13a34-430">在此示例中，代码将查找名为关键字的查询字符串值 (例如，~/default.aspx？关键字 = chef) 。</span><span class="sxs-lookup"><span data-stu-id="13a34-430">In the example, the code will look for a query-string value named keyword (for example, ~/default.aspx?keyword=chef).</span></span> <span data-ttu-id="13a34-431">可以通过将自定义键作为参数传递给 parameter 特性来指定它。</span><span class="sxs-lookup"><span data-stu-id="13a34-431">You can specify a custom key by passing it as an argument to the parameter attribute.</span></span> <span data-ttu-id="13a34-432">例如，若要使用名为 q 的查询字符串变量的值，您可以执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="13a34-432">For example, to use the value of the query-string variable named q, you could do this:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample27.cs)]

<span data-ttu-id="13a34-433">如果此方法在页面的代码中，则用户可以通过使用查询字符串传递关键字来筛选结果：</span><span class="sxs-lookup"><span data-stu-id="13a34-433">If this method is in the page's code, users can filter the results by passing a keyword using the query string:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image4.png)

<span data-ttu-id="13a34-434">模型绑定完成了多个手动编码的任务：读取值、检查 null 值，尝试将其转换为适当的类型，检查转换是否成功，最后使用查询中的值。</span><span class="sxs-lookup"><span data-stu-id="13a34-434">Model binding accomplishes many tasks that you would otherwise have to code by hand: reading the value, checking for a null value, attempting to convert it to the appropriate type, checking whether the conversion was successful, and finally, using the value in the query.</span></span> <span data-ttu-id="13a34-435">模型绑定产生的代码更少，并且能够在整个应用程序中重复使用该功能。</span><span class="sxs-lookup"><span data-stu-id="13a34-435">Model binding results in far less code and in the ability to reuse the functionality throughout your application.</span></span>

<a id="_Toc318097390"></a>
#### <a name="filtering-by-values-from-a-control"></a><span data-ttu-id="13a34-436">按控件中的值进行筛选</span><span class="sxs-lookup"><span data-stu-id="13a34-436">Filtering by values from a control</span></span>

<span data-ttu-id="13a34-437">假设要扩展该示例，使用户可以从下拉列表中选择筛选器值。</span><span class="sxs-lookup"><span data-stu-id="13a34-437">Suppose you want to extend the example to let the user choose a filter value from a drop-down list.</span></span> <span data-ttu-id="13a34-438">向标记添加以下下拉列表，并将其配置为使用 *SelectMethod* 属性从另一个方法获取其数据：</span><span class="sxs-lookup"><span data-stu-id="13a34-438">Add the following drop-down list to the markup and configure it to get its data from another method using the *SelectMethod* property:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample28.aspx)]

<span data-ttu-id="13a34-439">通常，还会将 *EmptyDataTemplate* 元素添加到 *GridView* 控件，以便在未找到匹配的产品时，控件将显示一条消息：</span><span class="sxs-lookup"><span data-stu-id="13a34-439">Typically you would also add an *EmptyDataTemplate* element to the *GridView* control so that the control will display a message if no matching products are found:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample29.aspx)]

<span data-ttu-id="13a34-440">在页代码中，为下拉列表添加新的选择方法：</span><span class="sxs-lookup"><span data-stu-id="13a34-440">In the page code, add the new select method for the drop-down list:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample30.cs)]

<span data-ttu-id="13a34-441">最后，更新 *GetProducts* select 方法以从下拉列表中获取一个包含所选类别 ID 的新参数：</span><span class="sxs-lookup"><span data-stu-id="13a34-441">Finally, update the *GetProducts* select method to take a new parameter that contains the ID of the selected category from the drop-down list:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample31.cs)]

<span data-ttu-id="13a34-442">现在，当页面运行时，用户可以从下拉列表中选择一个类别，然后自动重新绑定 *GridView* 控件以显示筛选后的数据。</span><span class="sxs-lookup"><span data-stu-id="13a34-442">Now when the page runs, users can select a category from the drop-down list, and the *GridView* control is automatically re-bound to show the filtered data.</span></span> <span data-ttu-id="13a34-443">这是可能的，因为模型绑定跟踪 select 方法的参数值，并检测回发后是否有任何参数值发生了更改。</span><span class="sxs-lookup"><span data-stu-id="13a34-443">This is possible because model binding tracks the values of parameters for select methods and detects whether any parameter value has changed after a postback.</span></span> <span data-ttu-id="13a34-444">如果是这样，则模型绑定强制关联的数据控件重新绑定到数据。</span><span class="sxs-lookup"><span data-stu-id="13a34-444">If so, model binding forces the associated data control to re-bind to the data.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image5.png)

<a id="_Toc318097391"></a>
### <a name="html-encoded-data-binding-expressions"></a><span data-ttu-id="13a34-445">HTML 编码 Data-Binding 表达式</span><span class="sxs-lookup"><span data-stu-id="13a34-445">HTML Encoded Data-Binding Expressions</span></span>

<span data-ttu-id="13a34-446">现在可以对数据绑定表达式的结果进行 HTML 编码。</span><span class="sxs-lookup"><span data-stu-id="13a34-446">You can now HTML-encode the result of data-binding expressions.</span></span> <span data-ttu-id="13a34-447">将冒号 (： ) 添加到用于 &lt; 标记数据绑定表达式的% # 前缀的末尾：</span><span class="sxs-lookup"><span data-stu-id="13a34-447">Add a colon (:) to the end of the &lt;%# prefix that marks the data-binding expression:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample32.aspx)]

<a id="_Toc318097392"></a>
### <a name="unobtrusive-validation"></a><span data-ttu-id="13a34-448">非引人注目验证</span><span class="sxs-lookup"><span data-stu-id="13a34-448">Unobtrusive Validation</span></span>

<span data-ttu-id="13a34-449">你现在可以配置内置验证程序控件，以对客户端验证逻辑使用不引人注目的 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="13a34-449">You can now configure the built-in validator controls to use unobtrusive JavaScript for client-side validation logic.</span></span> <span data-ttu-id="13a34-450">这可以显著减少在页面标记中以内联方式呈现的 JavaScript 数量，并减少总体页面大小。</span><span class="sxs-lookup"><span data-stu-id="13a34-450">This significantly reduces the amount of JavaScript rendered inline in the page markup and reduces the overall page size.</span></span> <span data-ttu-id="13a34-451">可以通过以下任一方式为验证程序控件配置不引人注目的 JavaScript：</span><span class="sxs-lookup"><span data-stu-id="13a34-451">You can configure unobtrusive JavaScript for validator controls in any of these ways:</span></span>

- <span data-ttu-id="13a34-452">通过将以下设置添加到 Web.config 文件中的\* &lt; appSettings &gt; \*元素全局：</span><span class="sxs-lookup"><span data-stu-id="13a34-452">Globally by adding the following setting to the *&lt;appSettings&gt;* element in the Web.config file:</span></span> 

    [!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample33.xml)]
- <span data-ttu-id="13a34-453">通过将静态 *ValidationSettings* 属性设置为 *UnobtrusiveValidationMode* ，将 UnobtrusiveValidationMode 属性设置为全局性 (通常在 Global.asax 文件中的 *应用程序 \_ 启动* 方法) 。</span><span class="sxs-lookup"><span data-stu-id="13a34-453">Globally by setting the static *System.Web.UI.ValidationSettings.UnobtrusiveValidationMode* property to *UnobtrusiveValidationMode.WebForms* (typically in the *Application\_Start* method in the Global.asax file).</span></span>
- <span data-ttu-id="13a34-454">通过将*page*类的新 " *UnobtrusiveValidationMode* " 属性设置为 "UnobtrusiveValidationMode"，单独用于页面 *。*</span><span class="sxs-lookup"><span data-stu-id="13a34-454">Individually for a page by setting the new *UnobtrusiveValidationMode* property of the *Page* class to *UnobtrusiveValidationMode.WebForms*.</span></span>

<a id="_Toc318097393"></a>
### <a name="html5-updates"></a><span data-ttu-id="13a34-455">HTML5 更新</span><span class="sxs-lookup"><span data-stu-id="13a34-455">HTML5 Updates</span></span>

<span data-ttu-id="13a34-456">对 Web 窗体服务器控件进行了一些改进，以利用 HTML5 的新功能：</span><span class="sxs-lookup"><span data-stu-id="13a34-456">Some improvements have been made to Web Forms server controls to take advantage of new features of HTML5:</span></span>

- <span data-ttu-id="13a34-457">已更新*TextBox*控件的*TextMode*属性，以支持新的 HTML5 输入类型（如*电子邮件*、*日期时间*等）。</span><span class="sxs-lookup"><span data-stu-id="13a34-457">The *TextMode* property of the *TextBox* control has been updated to support the new HTML5 input types like *email*, *datetime*, and so on.</span></span>
- <span data-ttu-id="13a34-458">*FileUpload*控件现在支持支持此 HTML5 功能的浏览器中的多个文件上传。</span><span class="sxs-lookup"><span data-stu-id="13a34-458">The *FileUpload* control now supports multiple file uploads from browsers that support this HTML5 feature.</span></span>
- <span data-ttu-id="13a34-459">验证程序控件现在支持验证 HTML5 输入元素。</span><span class="sxs-lookup"><span data-stu-id="13a34-459">Validator controls now support validating HTML5 input elements.</span></span>
- <span data-ttu-id="13a34-460">具有表示 URL 的特性的新 HTML5 元素现在支持 runat = "server"。</span><span class="sxs-lookup"><span data-stu-id="13a34-460">New HTML5 elements that have attributes that represent a URL now support runat="server".</span></span> <span data-ttu-id="13a34-461">因此，可以在 URL 路径中使用 ASP.NET 约定，如 ~ 运算符来表示应用程序根 (例如， &lt; 视频 runat = "server" src = "~/myVideo.wmv"/ &gt;) 。</span><span class="sxs-lookup"><span data-stu-id="13a34-461">As a result, you can use ASP.NET conventions in URL paths, like the ~ operator to represent the application root (for example, &lt;video runat="server" src="~/myVideo.wmv" /&gt;).</span></span>
- <span data-ttu-id="13a34-462">已修复 *UpdatePanel* 控件以支持发布 HTML5 输入字段。</span><span class="sxs-lookup"><span data-stu-id="13a34-462">The *UpdatePanel* control has been fixed to support posting HTML5 input fields.</span></span>

<a id="_Toc318097394"></a>
## <a name="aspnet-mvc-4"></a><span data-ttu-id="13a34-463">ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="13a34-463">ASP.NET MVC 4</span></span>

<span data-ttu-id="13a34-464">ASP.NET MVC 4 Beta 现在随附在 Visual Studio 11 Beta 版中。</span><span class="sxs-lookup"><span data-stu-id="13a34-464">ASP.NET MVC 4 Beta is now included with Visual Studio 11 Beta.</span></span> <span data-ttu-id="13a34-465">ASP.NET MVC 是一个框架，用于通过利用模型-视图-控制器 (MVC) 模式来开发高度可测试性和可维护的 Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="13a34-465">ASP.NET MVC is a framework for developing highly testable and maintainable Web applications by leveraging the Model-View-Controller (MVC) pattern.</span></span> <span data-ttu-id="13a34-466">ASP.NET MVC 4 使你可以轻松地生成适用于移动网络的应用程序并包括 ASP.NET Web API，这有助于构建可访问任何设备的 HTTP 服务。</span><span class="sxs-lookup"><span data-stu-id="13a34-466">ASP.NET MVC 4 makes it easy to build applications for the mobile Web and includes ASP.NET Web API, which helps you build HTTP services that can reach any device.</span></span> <span data-ttu-id="13a34-467">有关详细信息，请参阅 [ASP.NET MVC 4 发行说明](mvc4-release-notes.md)。</span><span class="sxs-lookup"><span data-stu-id="13a34-467">For more information, see the [ASP.NET MVC 4 Release Notes](mvc4-release-notes.md).</span></span>

<a id="_Toc318097395"></a>
## <a name="aspnet-web-pages-2"></a><span data-ttu-id="13a34-468">ASP.NET 网页 2</span><span class="sxs-lookup"><span data-stu-id="13a34-468">ASP.NET Web Pages 2</span></span>

<span data-ttu-id="13a34-469">新增功能包括：</span><span class="sxs-lookup"><span data-stu-id="13a34-469">New features include the following:</span></span>

- <span data-ttu-id="13a34-470">新的和更新的站点模板。</span><span class="sxs-lookup"><span data-stu-id="13a34-470">New and updated site templates.</span></span>
- <span data-ttu-id="13a34-471">使用 *验证* 帮助器添加服务器端和客户端验证。</span><span class="sxs-lookup"><span data-stu-id="13a34-471">Adding server-side and client-side validation using the *Validation* helper.</span></span>
- <span data-ttu-id="13a34-472">使用资产管理器注册脚本的能力。</span><span class="sxs-lookup"><span data-stu-id="13a34-472">The ability to register scripts using an assets manager.</span></span>
- <span data-ttu-id="13a34-473">使用 OAuth 和 OpenID 启用 Facebook 和其他站点的登录。</span><span class="sxs-lookup"><span data-stu-id="13a34-473">Enabling logins from Facebook and other sites using OAuth and OpenID.</span></span>
- <span data-ttu-id="13a34-474">使用 *map* helper 添加映射。</span><span class="sxs-lookup"><span data-stu-id="13a34-474">Adding maps using the *Maps* helper.</span></span>
- <span data-ttu-id="13a34-475">并行运行 Web Pages 应用程序。</span><span class="sxs-lookup"><span data-stu-id="13a34-475">Running Web Pages applications side-by-side.</span></span>
- <span data-ttu-id="13a34-476">移动设备的呈现页。</span><span class="sxs-lookup"><span data-stu-id="13a34-476">Rendering pages for mobile devices.</span></span>

<span data-ttu-id="13a34-477">有关这些功能和整页代码示例的详细信息，请参阅 [Web Pages 2 Beta 版中的主要功能](https://go.microsoft.com/fwlink/?LinkID=227824)。</span><span class="sxs-lookup"><span data-stu-id="13a34-477">For more information about these features and full-page code examples, see [The Top Features in Web Pages 2 Beta](https://go.microsoft.com/fwlink/?LinkID=227824).</span></span>

<a id="_Toc318097396"></a>
## <a name="visual-web-developer-11-beta"></a><span data-ttu-id="13a34-478">Visual Web Developer 11 Beta</span><span class="sxs-lookup"><span data-stu-id="13a34-478">Visual Web Developer 11 Beta</span></span>

<span data-ttu-id="13a34-479">本部分提供有关在 Visual Web Developer 11 Beta 和 Visual Studio 2012 候选发布版中对 web 开发的改进的信息。</span><span class="sxs-lookup"><span data-stu-id="13a34-479">This section provides information about improvements for web development in Visual Web Developer 11 Beta and Visual Studio 2012 Release Candidate.</span></span>

<a id="project-compatibility"></a>
### <a name="project-sharing-between-visual-studio-2010-and-visual-studio-2012-release-candidate-project-compatibility"></a><span data-ttu-id="13a34-480">Visual Studio 2010 和 Visual Studio 2012 候选发布版本之间的项目共享 (项目兼容性) </span><span class="sxs-lookup"><span data-stu-id="13a34-480">Project Sharing Between Visual Studio 2010 and Visual Studio 2012 Release Candidate (Project Compatibility)</span></span>

<span data-ttu-id="13a34-481">在 Visual Studio 2012 候选发布版本之前，在较新版本的 Visual Studio 中打开现有项目会启动转换向导。</span><span class="sxs-lookup"><span data-stu-id="13a34-481">Until Visual Studio 2012 Release Candidate, opening an existing project in a newer version of Visual Studio launched the Conversion Wizard.</span></span> <span data-ttu-id="13a34-482">这会强制将项目的 (资产) 的内容升级到不向后兼容的新格式。</span><span class="sxs-lookup"><span data-stu-id="13a34-482">This forced an upgrade of the content (assets) of a project and solution to new formats that were not backward compatible.</span></span> <span data-ttu-id="13a34-483">因此，在转换后，无法在较旧版本的 Visual Studio 中打开该项目。</span><span class="sxs-lookup"><span data-stu-id="13a34-483">Therefore, after the conversion you could not open the project in the older version of Visual Studio.</span></span>

<span data-ttu-id="13a34-484">许多客户告诉我们，这并不是正确的方法。</span><span class="sxs-lookup"><span data-stu-id="13a34-484">Many customers have told us that this was not the right approach.</span></span> <span data-ttu-id="13a34-485">在 Visual Studio 11 测试版中，我们现在支持通过 Visual Studio 2010 SP1 共享项目和解决方案。</span><span class="sxs-lookup"><span data-stu-id="13a34-485">In Visual Studio 11 Beta, we now support sharing projects and solutions with Visual Studio 2010 SP1.</span></span> <span data-ttu-id="13a34-486">这意味着，如果你在 Visual Studio 2012 候选发布版本中打开2010项目，你仍可以在 Visual Studio 2010 SP1 中打开该项目。</span><span class="sxs-lookup"><span data-stu-id="13a34-486">This means that if you open a 2010 project in Visual Studio 2012 Release Candidate, you will still be able to open the project in Visual Studio 2010 SP1.</span></span>

> [!NOTE]
> <span data-ttu-id="13a34-487">几种类型的项目不能在 Visual Studio 2010 SP1 和 Visual Studio 2012 候选发布版本之间共享。</span><span class="sxs-lookup"><span data-stu-id="13a34-487">A few types of projects cannot be shared between Visual Studio 2010 SP1 and Visual Studio 2012 Release Candidate.</span></span> <span data-ttu-id="13a34-488">其中包括一些较旧的项目 (如用于特殊目的的 ASP.NET MVC 2 项目) 或项目 (如安装项目) 。</span><span class="sxs-lookup"><span data-stu-id="13a34-488">These include some older projects (such as ASP.NET MVC 2 projects) or projects for special purposes (such as Setup projects).</span></span>

<span data-ttu-id="13a34-489">在 Visual Studio 11 Beta 中首次打开 Visual Studio 2010 SP1 Web 项目时，会将以下属性添加到项目文件中：</span><span class="sxs-lookup"><span data-stu-id="13a34-489">When you open a Visual Studio 2010 SP1 Web project for the first time in Visual Studio 11 Beta, the following properties are added to the project file:</span></span>

- <span data-ttu-id="13a34-490">FileUpgradeFlags</span><span class="sxs-lookup"><span data-stu-id="13a34-490">FileUpgradeFlags</span></span>
- <span data-ttu-id="13a34-491">UpgradeBackupLocation</span><span class="sxs-lookup"><span data-stu-id="13a34-491">UpgradeBackupLocation</span></span>
- <span data-ttu-id="13a34-492">OldToolsVersion</span><span class="sxs-lookup"><span data-stu-id="13a34-492">OldToolsVersion</span></span>
- <span data-ttu-id="13a34-493">VisualStudioVersion</span><span class="sxs-lookup"><span data-stu-id="13a34-493">VisualStudioVersion</span></span>
- <span data-ttu-id="13a34-494">VSToolsPath</span><span class="sxs-lookup"><span data-stu-id="13a34-494">VSToolsPath</span></span>

<span data-ttu-id="13a34-495">FileUpgradeFlags、UpgradeBackupLocation 和 OldToolsVersion 由升级项目文件的进程使用。</span><span class="sxs-lookup"><span data-stu-id="13a34-495">FileUpgradeFlags, UpgradeBackupLocation, and OldToolsVersion are used by the process that upgrades the project file.</span></span> <span data-ttu-id="13a34-496">它们不会影响在 Visual Studio 2010 中使用项目。</span><span class="sxs-lookup"><span data-stu-id="13a34-496">They have no impact on working with the project in Visual Studio 2010.</span></span>

<span data-ttu-id="13a34-497">VisualStudioVersion 是 MSBuild 4.5 使用的新属性，用于指示当前项目的 Visual Studio 版本。</span><span class="sxs-lookup"><span data-stu-id="13a34-497">VisualStudioVersion is a new property used by MSBuild 4.5 that indicates the version of Visual Studio for the current project.</span></span> <span data-ttu-id="13a34-498">由于 MSBuild 4.0 中不存在此属性 (Visual Studio 2010 SP1 使用) 的 MSBuild 版本，因此我们会在项目文件中注入默认值。</span><span class="sxs-lookup"><span data-stu-id="13a34-498">Because this property didn't exist in MSBuild 4.0 (the version of MSBuild that Visual Studio 2010 SP1 uses), we inject a default value into the project file.</span></span>

<span data-ttu-id="13a34-499">VSToolsPath 属性用于确定要从 MSBuildExtensionsPath32 设置表示的路径导入的正确 .targets 文件。</span><span class="sxs-lookup"><span data-stu-id="13a34-499">The VSToolsPath property is used to determine the correct .targets file to import from the path represented by the MSBuildExtensionsPath32 setting.</span></span>

<span data-ttu-id="13a34-500">此外，还有一些与 Import 元素相关的更改。</span><span class="sxs-lookup"><span data-stu-id="13a34-500">There are also some changes related to Import elements.</span></span> <span data-ttu-id="13a34-501">需要进行这些更改，以支持两个版本的 Visual Studio 之间的兼容性。</span><span class="sxs-lookup"><span data-stu-id="13a34-501">These changes are required in order to support compatibility between both versions of Visual Studio.</span></span>

> [!NOTE]
> <span data-ttu-id="13a34-502">如果在两台不同的计算机上的 Visual Studio 2010 SP1 和 Visual Studio 11 Beta 之间共享项目，并且项目在应用数据文件夹中包含本地数据库 \_ ，则必须确保两台计算机上都安装了数据库使用的 SQL Server 版本。</span><span class="sxs-lookup"><span data-stu-id="13a34-502">If a project is being shared between Visual Studio 2010 SP1 and Visual Studio 11 Beta on two different computers, and if the project includes a local database in the App\_Data folder, you must make sure that the version of SQL Server used by the database is installed on both computers.</span></span>

<a id="Configuration_Changes_In_ASPNET45_Website_Templates"></a>
### <a name="configuration-changes-in-aspnet-45-website-templates"></a><span data-ttu-id="13a34-503">ASP.NET 4.5 网站模板中的配置更改</span><span class="sxs-lookup"><span data-stu-id="13a34-503">Configuration Changes in ASP.NET 4.5 Website Templates</span></span>

<span data-ttu-id="13a34-504">已对使用 Visual Studio 2012 候选发布版中的网站模板创建的站点的默认 *Web.config* 文件进行了以下更改：</span><span class="sxs-lookup"><span data-stu-id="13a34-504">The following changes have been made to the default *Web.config* file for site that are created using website templates in Visual Studio 2012 Release Candidate:</span></span>

- <span data-ttu-id="13a34-505">在 `<httpRuntime>` 元素中， `encoderType` 现在默认设置属性，以使用已添加到 ASP.NET 的 AntiXSS 类型。</span><span class="sxs-lookup"><span data-stu-id="13a34-505">In the `<httpRuntime>` element, the `encoderType` attribute is now set by default to use the AntiXSS types that were added to ASP.NET.</span></span> <span data-ttu-id="13a34-506">有关详细信息，请参阅 [AntiXSS Library](#_Toc318097382)。</span><span class="sxs-lookup"><span data-stu-id="13a34-506">For details, see [AntiXSS Library](#_Toc318097382).</span></span>
- <span data-ttu-id="13a34-507">同样，在 `<httpRuntime>` 元素中， `requestValidationMode` 特性设置为 "4.5"。</span><span class="sxs-lookup"><span data-stu-id="13a34-507">Also in the `<httpRuntime>` element, the `requestValidationMode` attribute is set to "4.5".</span></span> <span data-ttu-id="13a34-508">这意味着，默认情况下，请求验证配置为使用延迟 ( "延迟" ) 验证。</span><span class="sxs-lookup"><span data-stu-id="13a34-508">This means that by default, request validation is configured to use deferred ("lazy") validation.</span></span> <span data-ttu-id="13a34-509">有关详细信息，请参阅 [New ASP.NET Request 验证功能](#_Toc318097379)。</span><span class="sxs-lookup"><span data-stu-id="13a34-509">For details, see [New ASP.NET Request Validation Features](#_Toc318097379).</span></span>
- <span data-ttu-id="13a34-510">`<modules>`部分的元素 `<system.webServer>` 不包含 `runAllManagedModulesForAllRequests` 特性。</span><span class="sxs-lookup"><span data-stu-id="13a34-510">The `<modules>` element of the `<system.webServer>` section does not contain a `runAllManagedModulesForAllRequests` attribute.</span></span> <span data-ttu-id="13a34-511"> (其默认值为 false。 ) 这意味着，如果你使用的是尚未更新到 SP1 的 IIS 7 版本，则在新站点中进行路由时可能会遇到问题。</span><span class="sxs-lookup"><span data-stu-id="13a34-511">(Its default value is false.) This means that if you are using a version of IIS 7 that has not been updated to SP1, you might have issues with routing in a new site.</span></span> <span data-ttu-id="13a34-512">有关详细信息，请参阅 [IIS 7 for ASP.NET 路由中的本机支持](#Native_Support_In_IIS7_For_ASPNET_Routine)。</span><span class="sxs-lookup"><span data-stu-id="13a34-512">For more information, see [Native Support in IIS 7 for ASP.NET Routing](#Native_Support_In_IIS7_For_ASPNET_Routine).</span></span>

<span data-ttu-id="13a34-513">这些更改不会影响现有应用程序。</span><span class="sxs-lookup"><span data-stu-id="13a34-513">These changes do not affect existing applications.</span></span> <span data-ttu-id="13a34-514">但是，它们可能代表现有网站与你使用新模板为 ASP.NET 4.5 创建的新网站之间的行为差异。</span><span class="sxs-lookup"><span data-stu-id="13a34-514">However, they might represent a difference in behavior between existing websites and new websites that you create for ASP.NET 4.5 using the new templates.</span></span>

<a id="Native_Support_In_IIS7_For_ASPNET_Routine"></a>
### <a name="native-support-in-iis-7-for-aspnet-routing"></a><span data-ttu-id="13a34-515">IIS 7 中用于 ASP.NET 路由的本机支持</span><span class="sxs-lookup"><span data-stu-id="13a34-515">Native Support in IIS 7 for ASP.NET Routing</span></span>

<span data-ttu-id="13a34-516">这并不是 ASP.NET 的更改，但对于新网站项目的模板进行了更改，如果你正在使用的 IIS 7 版本未应用 SP1 更新，则可能会影响你。</span><span class="sxs-lookup"><span data-stu-id="13a34-516">This is not a change to ASP.NET as such, but a change in templates for new website projects that can affect you if you are working a version of IIS 7 that has not had the SP1 update applied.</span></span>

<span data-ttu-id="13a34-517">在 ASP.NET 中，可以将以下配置设置添加到应用程序，以便支持路由：</span><span class="sxs-lookup"><span data-stu-id="13a34-517">In ASP.NET, you can add the following configuration setting to applications in order to support routing:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample34.xml?highlight=3)]

<span data-ttu-id="13a34-518">当 **runAllManagedModulesForAllRequests** 为 true 时，url （如）将 `http://mysite/myapp/home` 转到 ASP.NET，即使 url 上没有 *.aspx*、 *mvc*或类似扩展名也是如此。</span><span class="sxs-lookup"><span data-stu-id="13a34-518">When **runAllManagedModulesForAllRequests** is true, a URL like `http://mysite/myapp/home` goes to ASP.NET, even though there is no *.aspx*, *.mvc*, or similar extension on the URL.</span></span>

<span data-ttu-id="13a34-519">对 IIS 7 进行的更新使得 **runAllManagedModulesForAllRequests** 设置不必要，并支持本机 ASP.NET 路由。</span><span class="sxs-lookup"><span data-stu-id="13a34-519">An update that was made to IIS 7 makes the **runAllManagedModulesForAllRequests** setting unnecessary and supports ASP.NET routing natively.</span></span> <span data-ttu-id="13a34-520"> (有关更新的信息，请参阅 Microsoft 支持部门文章 [提供了可使某些 IIS 7.0 或 iis 7.5 处理程序处理其 url 不以句点结尾的请求的更新](https://support.microsoft.com/kb/980368)。 ) </span><span class="sxs-lookup"><span data-stu-id="13a34-520">(For information about the update, see the Microsoft Support article [An update is available that enables certain IIS 7.0 or IIS 7.5 handlers to handle requests whose URLs do not end with a period](https://support.microsoft.com/kb/980368).)</span></span>

<span data-ttu-id="13a34-521">如果你的网站在 IIS 7 上运行，并且如果 IIS 已更新，则不需要将 **runAllManagedModulesForAllRequests** 设置为 true。</span><span class="sxs-lookup"><span data-stu-id="13a34-521">If your website is running on IIS 7 and if IIS has been updated, you do not need to set **runAllManagedModulesForAllRequests** to true.</span></span> <span data-ttu-id="13a34-522">事实上，不建议将其设置为 true，因为这样做会增加不必要的处理开销来请求。</span><span class="sxs-lookup"><span data-stu-id="13a34-522">In fact, setting it to true is not recommended, because it adds unnecessary processing overhead to request.</span></span> <span data-ttu-id="13a34-523">如果此设置为 true，则所有请求（包括 *.htm*、 *.jpg*和其他静态文件的请求）也会经历 ASP.NET 请求管道。</span><span class="sxs-lookup"><span data-stu-id="13a34-523">When this setting is true, all requests, including those for *.htm*, *.jpg*, and other static files, also go through the ASP.NET request pipeline.</span></span>

<span data-ttu-id="13a34-524">如果使用 Visual Studio 2012 RC 中提供的模板创建新的 ASP.NET 4.5 网站，则网站的配置不包括 **runAllManagedModulesForAllRequests** 设置。</span><span class="sxs-lookup"><span data-stu-id="13a34-524">If you create a new ASP.NET 4.5 website using the templates that are provided in Visual Studio 2012 RC, the configuration for the website does not include the **runAllManagedModulesForAllRequests** setting.</span></span> <span data-ttu-id="13a34-525">这意味着，默认情况下，设置为 false。</span><span class="sxs-lookup"><span data-stu-id="13a34-525">This means that by default the setting is false.</span></span>

<span data-ttu-id="13a34-526">如果你随后在未安装 SP1 的 Windows 7 上运行该网站，则 IIS 7 将不包括所需的更新。</span><span class="sxs-lookup"><span data-stu-id="13a34-526">If you then run the website on Windows 7 without SP1 installed, IIS 7 will not include the required update.</span></span> <span data-ttu-id="13a34-527">因此，路由将不起作用，并且你将看到错误。</span><span class="sxs-lookup"><span data-stu-id="13a34-527">As a consequence, routing will not work and you will see errors.</span></span> <span data-ttu-id="13a34-528">如果出现无法使用路由的问题，则可以执行以下任一操作：</span><span class="sxs-lookup"><span data-stu-id="13a34-528">If you have a problem where routing does not work, you can do either the following:</span></span>

- <span data-ttu-id="13a34-529">将 Windows 7 更新为 SP1，这会将更新添加到 IIS 7。</span><span class="sxs-lookup"><span data-stu-id="13a34-529">Update Windows 7 to SP1, which will add the update to IIS 7.</span></span>
- <span data-ttu-id="13a34-530">安装前面列出的 Microsoft 支持部门文章中描述的更新。</span><span class="sxs-lookup"><span data-stu-id="13a34-530">Install the update that's described in the Microsoft Support article listed previously.</span></span>
- <span data-ttu-id="13a34-531">在该网站的 Web.config 文件中，将 **runAllManagedModulesForAllRequests** 设置为 true。</span><span class="sxs-lookup"><span data-stu-id="13a34-531">Set **runAllManagedModulesForAllRequests** to true in that website's Web.config file.</span></span> <span data-ttu-id="13a34-532">请注意，这将为请求增加一些开销。</span><span class="sxs-lookup"><span data-stu-id="13a34-532">Note that this will add some overhead to requests.</span></span>

<a id="_Toc318097397"></a>
### <a name="html-editor"></a><span data-ttu-id="13a34-533">HTML 编辑器</span><span class="sxs-lookup"><span data-stu-id="13a34-533">HTML Editor</span></span>

<a id="_Toc318097398"></a>
#### <a name="smart-tasks"></a><span data-ttu-id="13a34-534">智能任务</span><span class="sxs-lookup"><span data-stu-id="13a34-534">Smart Tasks</span></span>

<span data-ttu-id="13a34-535">在设计视图中，服务器控件的复杂属性通常具有相关联的对话框和向导，以使其易于设置。</span><span class="sxs-lookup"><span data-stu-id="13a34-535">In Design view, complex properties of server controls often have associated dialog boxes and wizards to make it easy to set them.</span></span> <span data-ttu-id="13a34-536">例如，您可以使用一个特殊的对话框向 *Repeater* 控件添加数据源，或将列添加到 *GridView* 控件。</span><span class="sxs-lookup"><span data-stu-id="13a34-536">For example, you can use a special dialog box to add a data source to a *Repeater* control or add columns to a *GridView* control.</span></span>

<span data-ttu-id="13a34-537">但对于复杂属性，这种类型的 UI 帮助在源视图中不可用。</span><span class="sxs-lookup"><span data-stu-id="13a34-537">However, this type of UI help for complex properties has not been available in Source view.</span></span> <span data-ttu-id="13a34-538">因此，Visual Studio 11 为源视图引入了智能任务。</span><span class="sxs-lookup"><span data-stu-id="13a34-538">Therefore, Visual Studio 11 introduces Smart Tasks for Source view.</span></span> <span data-ttu-id="13a34-539">智能任务是适用于 c # 和 Visual Basic 编辑器中的常用功能的上下文感知快捷方式。</span><span class="sxs-lookup"><span data-stu-id="13a34-539">Smart Tasks are context-aware shortcuts for commonly used features in the C# and Visual Basic editors.</span></span>

<span data-ttu-id="13a34-540">对于 ASP.NET Web 窗体控件，当插入点位于元素内时，智能任务会作为小标志符号出现在服务器标记中：</span><span class="sxs-lookup"><span data-stu-id="13a34-540">For ASP.NET Web Forms controls, Smart Tasks appear on server tags as a small glyph when the insertion point is inside the element:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image6.png)

<span data-ttu-id="13a34-541">当单击标志符号或按 CTRL + 时，智能任务将展开。</span><span class="sxs-lookup"><span data-stu-id="13a34-541">The Smart Task expands when you click the glyph or press CTRL+.</span></span> <span data-ttu-id="13a34-542"> (点) ，就像在代码编辑器中一样。</span><span class="sxs-lookup"><span data-stu-id="13a34-542">(dot), just as in the code editors.</span></span> <span data-ttu-id="13a34-543">然后，它会显示与设计视图中的智能任务类似的快捷方式。</span><span class="sxs-lookup"><span data-stu-id="13a34-543">It then displays shortcuts that are similar to the Smart Tasks in Design view.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image7.png)

<span data-ttu-id="13a34-544">例如，上图中的智能任务显示 GridView 任务选项。</span><span class="sxs-lookup"><span data-stu-id="13a34-544">For example, the Smart Task in the previous illustration shows the GridView Tasks options.</span></span> <span data-ttu-id="13a34-545">如果选择 "编辑列"，将显示以下对话框：</span><span class="sxs-lookup"><span data-stu-id="13a34-545">If you choose Edit Columns, the following dialog box is displayed:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image8.png)

<span data-ttu-id="13a34-546">填写此对话框将设置可以在设计视图中设置的相同属性。</span><span class="sxs-lookup"><span data-stu-id="13a34-546">Filling in the dialog box sets the same properties you can set in Design view.</span></span> <span data-ttu-id="13a34-547">单击 "确定" 后，将用新设置更新控件的标记：</span><span class="sxs-lookup"><span data-stu-id="13a34-547">When you click OK, the markup for the control is updated with the new settings:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image9.png)

<a id="_Toc318097399"></a>
#### <a name="wai-aria-support"></a><span data-ttu-id="13a34-548">WAI-ARIA 支持</span><span class="sxs-lookup"><span data-stu-id="13a34-548">WAI-ARIA support</span></span>

<span data-ttu-id="13a34-549">编写可访问的网站越来越重要。</span><span class="sxs-lookup"><span data-stu-id="13a34-549">Writing accessible websites is becoming increasingly important.</span></span> <span data-ttu-id="13a34-550">[WAI-ARIA 辅助功能标准](http://www.w3.org/WAI/intro/aria)定义开发人员应如何编写可访问的网站。</span><span class="sxs-lookup"><span data-stu-id="13a34-550">The [WAI-ARIA accessibility standard](http://www.w3.org/WAI/intro/aria) defines how developers should write accessible websites.</span></span> <span data-ttu-id="13a34-551">Visual Studio 现在完全支持此标准。</span><span class="sxs-lookup"><span data-stu-id="13a34-551">This standard is now fully supported in Visual Studio.</span></span>

<span data-ttu-id="13a34-552">例如， *role* 属性现在具有完整的 IntelliSense：</span><span class="sxs-lookup"><span data-stu-id="13a34-552">For example, the *role* attribute now has full IntelliSense:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image10.png)

<span data-ttu-id="13a34-553">WAI 标准还引入了用 *ARIA* 作为前缀的属性，使你可以向 HTML5 文档添加语义。</span><span class="sxs-lookup"><span data-stu-id="13a34-553">The WAI-ARIA standard also introduces attributes that are prefixed with *aria-* that let you add semantics to an HTML5 document.</span></span> <span data-ttu-id="13a34-554">Visual Studio 还完全支持以下 *aria* 特性：</span><span class="sxs-lookup"><span data-stu-id="13a34-554">Visual Studio also fully supports these *aria-* attributes:</span></span>

<span data-ttu-id="13a34-555">![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image11.png) ![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image12.png)</span><span class="sxs-lookup"><span data-stu-id="13a34-555">![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image11.png) ![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image12.png)</span></span>

<a id="_Toc318097400"></a>
#### <a name="new-html5-snippets"></a><span data-ttu-id="13a34-556">新 HTML5 代码段</span><span class="sxs-lookup"><span data-stu-id="13a34-556">New HTML5 snippets</span></span>

<span data-ttu-id="13a34-557">为了更快、更轻松地编写常用 HTML5 标记，Visual Studio 提供了很多代码段。</span><span class="sxs-lookup"><span data-stu-id="13a34-557">To make it faster and easier to write commonly used HTML5 markup, Visual Studio includes a number of snippets.</span></span> <span data-ttu-id="13a34-558">视频片段是一个示例：</span><span class="sxs-lookup"><span data-stu-id="13a34-558">An example is the video snippet:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image13.png)

<span data-ttu-id="13a34-559">若要调用代码段，请在 IntelliSense 中选择元素时，按 Tab 两次：</span><span class="sxs-lookup"><span data-stu-id="13a34-559">To invoke the snippet, press Tab twice when the element is selected in IntelliSense:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image14.png)

<span data-ttu-id="13a34-560">这会生成一个可自定义的代码段。</span><span class="sxs-lookup"><span data-stu-id="13a34-560">This produces a snippet that you can customize.</span></span>

<a id="_Toc318097401"></a>
#### <a name="extract-to-user-control"></a><span data-ttu-id="13a34-561">提取到用户控件</span><span class="sxs-lookup"><span data-stu-id="13a34-561">Extract to user control</span></span>

<span data-ttu-id="13a34-562">在较大的网页中，最好将各个部分移到用户控件中。</span><span class="sxs-lookup"><span data-stu-id="13a34-562">In large web pages, it can be a good idea to move individual pieces into user controls.</span></span> <span data-ttu-id="13a34-563">这种形式的重构有助于提高页面的可读性，并可以简化页面结构。</span><span class="sxs-lookup"><span data-stu-id="13a34-563">This form of refactoring can help increase the readability of the page and can simplify the page structure.</span></span>

<span data-ttu-id="13a34-564">若要简化此操作，在 "源" 视图中编辑 Web 窗体页时，现在可以在页中选择文本，右键单击它，然后选择 "提取到用户控件"：</span><span class="sxs-lookup"><span data-stu-id="13a34-564">To make this easier, when you edit Web Forms pages in Source view, you can now select text in a page, right-click it, and then choose Extract to User Control:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image2.jpg)

<a id="_Toc318097402"></a>
#### <a name="intellisense-for-code-nuggets-in-attributes"></a><span data-ttu-id="13a34-565">特性中代码片段的 IntelliSense</span><span class="sxs-lookup"><span data-stu-id="13a34-565">IntelliSense for code nuggets in attributes</span></span>

<span data-ttu-id="13a34-566">Visual Studio 始终为任何页面或控件中的服务器端代码片段提供 IntelliSense。</span><span class="sxs-lookup"><span data-stu-id="13a34-566">Visual Studio has always provided IntelliSense for server-side code nuggets in any page or control.</span></span> <span data-ttu-id="13a34-567">现在，Visual Studio 还包括 HTML 特性中代码片段的 IntelliSense。</span><span class="sxs-lookup"><span data-stu-id="13a34-567">Now Visual Studio includes IntelliSense for code nuggets in HTML attributes as well.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image15.png)

<span data-ttu-id="13a34-568">这样可以更轻松地创建数据绑定表达式：</span><span class="sxs-lookup"><span data-stu-id="13a34-568">This makes it easier to create data-binding expressions:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image16.png)

<a id="_Toc318097403"></a>
#### <a name="automatic-renaming-of-matching-tag-when-you-rename-an-opening-or-closing-tag"></a><span data-ttu-id="13a34-569">重命名开始或结束标记时自动重命名匹配标记</span><span class="sxs-lookup"><span data-stu-id="13a34-569">Automatic renaming of matching tag when you rename an opening or closing tag</span></span>

<span data-ttu-id="13a34-570">如果重命名 HTML 元素 (例如，将 *div* 标记更改为) *标头* 标记，则对应的开始标记或结束标记也会实时更改。</span><span class="sxs-lookup"><span data-stu-id="13a34-570">If you rename an HTML element (for example, you change a *div* tag to be a *header* tag), the corresponding opening or closing tag also changes in real time.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image17.png)

<span data-ttu-id="13a34-571">这有助于避免在您忘记更改结束标记或更改错误时出现的错误。</span><span class="sxs-lookup"><span data-stu-id="13a34-571">This helps avoid the error where you forget to change a closing tag or change the wrong one.</span></span>

<a id="_Toc318097404"></a>
#### <a name="event-handler-generation"></a><span data-ttu-id="13a34-572">生成事件处理程序</span><span class="sxs-lookup"><span data-stu-id="13a34-572">Event handler generation</span></span>

<span data-ttu-id="13a34-573">Visual Studio 现在包含源视图中的功能，可帮助你编写和手动绑定事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="13a34-573">Visual Studio now includes features in Source view to help you write event handlers and bind them manually.</span></span> <span data-ttu-id="13a34-574">如果在 "源" 视图中编辑事件名称，IntelliSense &lt; 将显示 "创建新事件 &gt; "，该事件将在页面的代码中创建一个具有正确签名的事件处理程序：</span><span class="sxs-lookup"><span data-stu-id="13a34-574">If you are editing an event name in Source view, IntelliSense displays &lt;Create New Event&gt;, which will create an event handler in the page's code that has the right signature:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image3.jpg)

<span data-ttu-id="13a34-575">默认情况下，事件处理程序将使用控件的 ID 作为事件处理方法的名称：</span><span class="sxs-lookup"><span data-stu-id="13a34-575">By default, the event handler will use the control's ID for the name of the event-handling method:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image4.jpg)

<span data-ttu-id="13a34-576">在这种情况下，生成的事件处理程序将类似于以下 (在 c # 中 ) ：</span><span class="sxs-lookup"><span data-stu-id="13a34-576">The resulting event handler will look like this (in this case, in C#):</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image18.png)

<a id="_Toc318097405"></a>
#### <a name="smart-indent"></a><span data-ttu-id="13a34-577">智能缩进</span><span class="sxs-lookup"><span data-stu-id="13a34-577">Smart indent</span></span>

<span data-ttu-id="13a34-578">当在空 HTML 元素内按 Enter 时，编辑器会将插入点放在正确的位置：</span><span class="sxs-lookup"><span data-stu-id="13a34-578">When you press Enter while inside an empty HTML element, the editor will put the insertion point in the right place:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image19.png)

<span data-ttu-id="13a34-579">如果在此位置按 Enter，则结束标记将向下移动并缩进，以匹配开始标记。</span><span class="sxs-lookup"><span data-stu-id="13a34-579">If you press Enter in this location, the closing tag is moved down and indented to match the opening tag.</span></span> <span data-ttu-id="13a34-580">插入点还缩进：</span><span class="sxs-lookup"><span data-stu-id="13a34-580">The insertion point is also indented:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image20.png)

<a id="_Toc318097406"></a>
#### <a name="auto-reduce-statement-completion"></a><span data-ttu-id="13a34-581">自动减少语句完成</span><span class="sxs-lookup"><span data-stu-id="13a34-581">Auto-reduce statement completion</span></span>

<span data-ttu-id="13a34-582">Visual Studio 中的 IntelliSense 列表现在基于你键入的内容进行筛选，以便仅显示相关选项：</span><span class="sxs-lookup"><span data-stu-id="13a34-582">The IntelliSense list in Visual Studio now filters based on what you type so that it displays only relevant options:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image21.png)

<span data-ttu-id="13a34-583">IntelliSense 还基于 IntelliSense 列表中各个单词的标题用例进行筛选。</span><span class="sxs-lookup"><span data-stu-id="13a34-583">IntelliSense also filters based on the title case of the individual words in the IntelliSense list.</span></span> <span data-ttu-id="13a34-584">例如，如果键入 "dl"，则会显示 dl 和 asp： DataList：</span><span class="sxs-lookup"><span data-stu-id="13a34-584">For example, if you type "dl", both dl and asp:DataList are displayed:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image22.png)

<span data-ttu-id="13a34-585">此功能可以更快地获取已知元素的语句完成。</span><span class="sxs-lookup"><span data-stu-id="13a34-585">This feature makes it faster to get statement completion for known elements.</span></span>

<a id="_Toc318097407"></a>
### <a name="javascript-editor"></a><span data-ttu-id="13a34-586">JavaScript 编辑器</span><span class="sxs-lookup"><span data-stu-id="13a34-586">JavaScript Editor</span></span>

<span data-ttu-id="13a34-587">Visual Studio 2012 候选发布版中的 JavaScript 编辑器是全新的，它大大提高了在 Visual Studio 中使用 JavaScript 的体验。</span><span class="sxs-lookup"><span data-stu-id="13a34-587">The JavaScript editor in Visual Studio 2012 Release Candidate is completely new and it greatly improves the experience of working with JavaScript in Visual Studio.</span></span>

<a id="_Toc318097408"></a>
#### <a name="code-outlining"></a><span data-ttu-id="13a34-588">代码大纲显示</span><span class="sxs-lookup"><span data-stu-id="13a34-588">Code outlining</span></span>

<span data-ttu-id="13a34-589">现在会自动为所有函数创建大纲显示区域，从而使您可以折叠部分文件中与当前焦点无关的部分。</span><span class="sxs-lookup"><span data-stu-id="13a34-589">Outlining regions are now automatically created for all functions, allowing you to collapse parts of the file that aren't pertinent to your current focus.</span></span>

<a id="_Toc318097409"></a>
#### <a name="brace-matching"></a><span data-ttu-id="13a34-590">大括号匹配</span><span class="sxs-lookup"><span data-stu-id="13a34-590">Brace matching</span></span>

<span data-ttu-id="13a34-591">当您将插入点放在左大括号或右大括号上时，该编辑器将突出显示匹配项。</span><span class="sxs-lookup"><span data-stu-id="13a34-591">When you put the insertion point on an opening or closing brace, the editor highlights the matching one.</span></span>

<a id="_Toc318097410"></a>
#### <a name="go-to-definition"></a><span data-ttu-id="13a34-592">转到定义</span><span class="sxs-lookup"><span data-stu-id="13a34-592">Go to Definition</span></span>

<span data-ttu-id="13a34-593">"转到定义" 命令可用于跳转到函数或变量的源。</span><span class="sxs-lookup"><span data-stu-id="13a34-593">The Go to Definition command lets you jump to the source for a function or variable.</span></span>

<a id="_Toc318097411"></a>
#### <a name="ecmascript5-support"></a><span data-ttu-id="13a34-594">ECMAScript5 支持</span><span class="sxs-lookup"><span data-stu-id="13a34-594">ECMAScript5 support</span></span>

<span data-ttu-id="13a34-595">编辑器支持 ECMAScript5 中的新语法和 Api，这是描述 JavaScript 语言的最新标准版本。</span><span class="sxs-lookup"><span data-stu-id="13a34-595">The editor supports the new syntax and APIs in ECMAScript5, the latest version of the standard that describes the JavaScript language.</span></span>

<a id="_Toc318097412"></a>
#### <a name="dom-intellisense"></a><span data-ttu-id="13a34-596">DOM IntelliSense</span><span class="sxs-lookup"><span data-stu-id="13a34-596">DOM IntelliSense</span></span>

<span data-ttu-id="13a34-597">已改进了 DOM Api 的 IntelliSense，并支持许多新的 HTML5 Api，包括 *querySelector*、DOM 存储、跨文档消息和 *画布*。</span><span class="sxs-lookup"><span data-stu-id="13a34-597">IntelliSense for DOM APIs has been improved, with support for many new HTML5 APIs including *querySelector*, DOM Storage, cross-document messaging, and *canvas*.</span></span> <span data-ttu-id="13a34-598">DOM IntelliSense 现在由单个简单的 JavaScript 文件驱动，而不是由本机类型库定义驱动。</span><span class="sxs-lookup"><span data-stu-id="13a34-598">DOM IntelliSense is now driven by a single simple JavaScript file, rather than by a native type library definition.</span></span> <span data-ttu-id="13a34-599">这样就可以轻松地扩展或替换。</span><span class="sxs-lookup"><span data-stu-id="13a34-599">This makes it easy to extend or replace.</span></span>

<a id="_Toc318097413"></a>
#### <a name="vsdoc-signature-overloads"></a><span data-ttu-id="13a34-600">VSDOC 签名重载</span><span class="sxs-lookup"><span data-stu-id="13a34-600">VSDOC signature overloads</span></span>

<span data-ttu-id="13a34-601">现在，可以使用新的\* &lt; 签名 &gt; \*元素为 JavaScript 函数的单独重载声明详细的 IntelliSense 注释，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="13a34-601">Detailed IntelliSense comments can now be declared for separate overloads of JavaScript functions by using the new *&lt;signature&gt;* element, as shown in this example:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample35.cs)]

<a id="_Toc318097414"></a>
#### <a name="implicit-references"></a><span data-ttu-id="13a34-602">隐式引用</span><span class="sxs-lookup"><span data-stu-id="13a34-602">Implicit references</span></span>

<span data-ttu-id="13a34-603">你现在可以将 JavaScript 文件添加到一个中央列表，该列表将隐式包含在任何给定 JavaScript 文件或块引用的文件列表中，这意味着你将获得其内容的 IntelliSense。</span><span class="sxs-lookup"><span data-stu-id="13a34-603">You can now add JavaScript files to a central list that will be implicitly included in the list of files that any given JavaScript file or block references, meaning you'll get IntelliSense for its contents.</span></span> <span data-ttu-id="13a34-604">例如，可以将 jQuery 文件添加到文件的中央列表，并在文件的任何 JavaScript 块中获取 jQuery 函数的 IntelliSense，无论是否已使用/// &lt; reference/) 显式引用 (&gt; 。</span><span class="sxs-lookup"><span data-stu-id="13a34-604">For example, you can add jQuery files to the central list of files, and you'll get IntelliSense for jQuery functions in any JavaScript block of file, whether you've referenced it explicitly (using /// &lt;reference /&gt;) or not.</span></span>

<a id="_Toc318097415"></a>
### <a name="css-editor"></a><span data-ttu-id="13a34-605">CSS 编辑器</span><span class="sxs-lookup"><span data-stu-id="13a34-605">CSS Editor</span></span>

<a id="_Toc318097416"></a>
#### <a name="auto-reduce-statement-completion"></a><span data-ttu-id="13a34-606">自动减少语句完成</span><span class="sxs-lookup"><span data-stu-id="13a34-606">Auto-reduce statement completion</span></span>

<span data-ttu-id="13a34-607">现在，CSS 的 IntelliSense 列表基于所选架构支持的 CSS 属性和值进行筛选。</span><span class="sxs-lookup"><span data-stu-id="13a34-607">The IntelliSense list for CSS now filters based on the CSS properties and values supported by the selected schema.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image23.png)

<span data-ttu-id="13a34-608">IntelliSense 还支持标题 case 搜索：</span><span class="sxs-lookup"><span data-stu-id="13a34-608">IntelliSense also supports title case searches:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image24.png)

<a id="_Toc318097417"></a>
#### <a name="hierarchical-indentation"></a><span data-ttu-id="13a34-609">分层缩进</span><span class="sxs-lookup"><span data-stu-id="13a34-609">Hierarchical indentation</span></span>

<span data-ttu-id="13a34-610">CSS 编辑器使用缩进来显示分层规则，这为您提供了对级联规则进行逻辑组织的概述。</span><span class="sxs-lookup"><span data-stu-id="13a34-610">The CSS editor uses indentation to display hierarchical rules, which gives you an overview of how the cascading rules are logically organized.</span></span> <span data-ttu-id="13a34-611">在下面的示例中，#list 选择器是列表的一个级联子级，因此缩进。</span><span class="sxs-lookup"><span data-stu-id="13a34-611">In the following example, the #list a selector is a cascading child of list and is therefore indented.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image25.png)

<span data-ttu-id="13a34-612">下面的示例演示了更复杂的继承：</span><span class="sxs-lookup"><span data-stu-id="13a34-612">The following example shows more complex inheritance:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image26.png)

<span data-ttu-id="13a34-613">规则的缩进由其父规则确定。</span><span class="sxs-lookup"><span data-stu-id="13a34-613">The indentation of a rule is determined by its parent rules.</span></span> <span data-ttu-id="13a34-614">默认情况下启用分层缩进，但你可以在 "选项" 对话框 (工具 "、菜单栏中的选项) ：</span><span class="sxs-lookup"><span data-stu-id="13a34-614">Hierarchical indentation is enabled by default, but you can disable it the Options dialog box (Tools, Options from the menu bar):</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image27.png)

<a id="_Toc318097418"></a>
#### <a name="css-hacks-support"></a><span data-ttu-id="13a34-615">CSS 黑客支持</span><span class="sxs-lookup"><span data-stu-id="13a34-615">CSS hacks support</span></span>

<span data-ttu-id="13a34-616">分析数百个真实的 CSS 文件表明，CSS 攻击非常常见，而 Visual Studio 现在支持最广泛使用的文件。</span><span class="sxs-lookup"><span data-stu-id="13a34-616">Analysis of hundreds of real-world CSS files shows that CSS hacks are very common, and now Visual Studio supports the most widely used ones.</span></span> <span data-ttu-id="13a34-617">此支持包括智能感知和对星形 (\*) 和下划线 (\_) 属性黑客的验证：</span><span class="sxs-lookup"><span data-stu-id="13a34-617">This support includes IntelliSense and validation of the star (\*) and underscore (\_) property hacks:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image28.png)

<span data-ttu-id="13a34-618">还支持典型的选择器黑客，以便即使在应用分层缩进时也能进行维护。</span><span class="sxs-lookup"><span data-stu-id="13a34-618">Typical selector hacks are also supported so that hierarchical indentation is maintained even when they are applied.</span></span> <span data-ttu-id="13a34-619">用于面向 Internet Explorer 7 的典型选择器黑客是在选择器前面预置\* \* ： first-child + html\*。</span><span class="sxs-lookup"><span data-stu-id="13a34-619">A typical selector hack used to target Internet Explorer 7 is to prepend a selector with *\*:first-child + html*.</span></span> <span data-ttu-id="13a34-620">使用该规则将维护分层缩进：</span><span class="sxs-lookup"><span data-stu-id="13a34-620">Using that rule will maintain the hierarchical indentation:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image29.png)

<a id="_Toc318097419"></a>
#### <a name="vendor-specific-schemas--moz---webkit"></a><span data-ttu-id="13a34-621">特定于供应商的架构 (-moz-,-webkit) </span><span class="sxs-lookup"><span data-stu-id="13a34-621">Vendor specific schemas (-moz-, -webkit)</span></span>

<span data-ttu-id="13a34-622">CSS3 引入了许多在不同时间由不同的浏览器实现的属性。</span><span class="sxs-lookup"><span data-stu-id="13a34-622">CSS3 introduces many properties that have been implemented by different browsers at different times.</span></span> <span data-ttu-id="13a34-623">之前，此方法迫使开发人员使用特定于供应商的语法为特定浏览器编写代码。</span><span class="sxs-lookup"><span data-stu-id="13a34-623">This previously forced developers to code for specific browsers by using vendor-specific syntax.</span></span> <span data-ttu-id="13a34-624">这些特定于浏览器的属性现已包含在 IntelliSense 中。</span><span class="sxs-lookup"><span data-stu-id="13a34-624">These browser-specific properties are now included in IntelliSense.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image30.png)

<a id="_Toc318097420"></a>
#### <a name="commenting-and-uncommenting-support"></a><span data-ttu-id="13a34-625">注释和取消注释支持</span><span class="sxs-lookup"><span data-stu-id="13a34-625">Commenting and uncommenting support</span></span>

<span data-ttu-id="13a34-626">你现在可以使用在代码编辑器中使用的相同快捷键来注释和取消注释 CSS 规则 (Ctrl + K、C to 注释和 Ctrl + K，用于取消注释) 。</span><span class="sxs-lookup"><span data-stu-id="13a34-626">You can now comment and uncomment CSS rules using the same shortcuts that you use in the code editor (Ctrl+K,C to comment and Ctrl+K,U to uncomment).</span></span>

<a id="_Toc318097421"></a>
#### <a name="color-picker"></a><span data-ttu-id="13a34-627">颜色选取器</span><span class="sxs-lookup"><span data-stu-id="13a34-627">Color picker</span></span>

<span data-ttu-id="13a34-628">在 Visual Studio 的早期版本中，与颜色相关的属性的 IntelliSense 由命名颜色值的下拉列表组成。</span><span class="sxs-lookup"><span data-stu-id="13a34-628">In previous versions of Visual Studio, IntelliSense for color-related attributes consisted of a drop-down list of named color values.</span></span> <span data-ttu-id="13a34-629">该列表已替换为功能完备的颜色选取器。</span><span class="sxs-lookup"><span data-stu-id="13a34-629">That list has been replaced by a full-featured color picker.</span></span>

<span data-ttu-id="13a34-630">输入颜色值时，颜色选取器会自动显示，并显示以前使用的颜色的列表，后跟默认调色板。</span><span class="sxs-lookup"><span data-stu-id="13a34-630">When you enter a color value, the color picker is displayed automatically and presents a list of previously used colors followed by a default color palette.</span></span> <span data-ttu-id="13a34-631">您可以使用鼠标或键盘选择颜色。</span><span class="sxs-lookup"><span data-stu-id="13a34-631">You can select a color using the mouse or the keyboard.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image31.png)

<span data-ttu-id="13a34-632">该列表可以扩展为完整的颜色选取器。</span><span class="sxs-lookup"><span data-stu-id="13a34-632">The list can be expanded into a complete color picker.</span></span> <span data-ttu-id="13a34-633">使用选取器可以在移动不透明度滑块时，通过自动将任何颜色转换为 RGBA 来控制 alpha 通道：</span><span class="sxs-lookup"><span data-stu-id="13a34-633">The picker lets you control the alpha channel by automatically converting any color into RGBA when you move the opacity slider:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image32.png)

<a id="_Toc318097422"></a>
#### <a name="snippets"></a><span data-ttu-id="13a34-634">代码片段</span><span class="sxs-lookup"><span data-stu-id="13a34-634">Snippets</span></span>

<span data-ttu-id="13a34-635">CSS 编辑器中的代码片段使创建跨浏览器样式更加简单快捷。</span><span class="sxs-lookup"><span data-stu-id="13a34-635">Snippets in the CSS editor make it easier and faster to create cross-browser styles.</span></span> <span data-ttu-id="13a34-636">许多需要浏览器特定设置的 CSS3 属性现在已滚动到代码段中。</span><span class="sxs-lookup"><span data-stu-id="13a34-636">Many CSS3 properties that require browser-specific settings have now been rolled into snippets.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image33.png)

<span data-ttu-id="13a34-637">CSS 代码段支持 (如 CSS3 媒体查询) 的高级方案， ( @ ) 键入符号，其中显示 IntelliSense 列表。</span><span class="sxs-lookup"><span data-stu-id="13a34-637">CSS snippets support advanced scenarios (like CSS3 media queries) by typing the at-symbol (@), which shows the IntelliSense list.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image34.png)

<span data-ttu-id="13a34-638">当你选择 " @media 值" 并按 tab 键时，CSS 编辑器将插入以下代码片段：</span><span class="sxs-lookup"><span data-stu-id="13a34-638">When you select @media value and press Tab, the CSS editor inserts the following snippet:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image5.jpg)

<span data-ttu-id="13a34-639">与代码的代码段一样，你可以创建自己的 CSS 代码段。</span><span class="sxs-lookup"><span data-stu-id="13a34-639">As with snippets for code, you can create your own CSS snippets.</span></span>

<a id="_Toc318097423"></a>
#### <a name="custom-regions"></a><span data-ttu-id="13a34-640">自定义区域</span><span class="sxs-lookup"><span data-stu-id="13a34-640">Custom regions</span></span>

<span data-ttu-id="13a34-641">已在代码编辑器中使用的命名代码区域现在可用于 CSS 编辑。</span><span class="sxs-lookup"><span data-stu-id="13a34-641">Named code regions, which are already available in the code editor, are now available for CSS editing.</span></span> <span data-ttu-id="13a34-642">这使您可以轻松地对相关样式块进行分组。</span><span class="sxs-lookup"><span data-stu-id="13a34-642">This lets you easily group related style blocks.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image35.png)

<span data-ttu-id="13a34-643">当区域处于折叠状态时，它将显示区域的名称：</span><span class="sxs-lookup"><span data-stu-id="13a34-643">When a region is collapsed it displays the name of the region:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image36.png)

<a id="_Toc318097424"></a>
### <a name="page-inspector"></a><span data-ttu-id="13a34-644">Page Inspector</span><span class="sxs-lookup"><span data-stu-id="13a34-644">Page Inspector</span></span>

<span data-ttu-id="13a34-645">Page Inspector 是一种工具，用于在 Visual Studio IDE 中 (HTML、Web 窗体、ASP.NET MVC 或 Web Pages) 呈现网页，并使你可以查看源代码和生成的输出。</span><span class="sxs-lookup"><span data-stu-id="13a34-645">Page Inspector is a tool that renders a web page (HTML, Web Forms, ASP.NET MVC, or Web Pages) in the Visual Studio IDE and lets you examine both the source code and the resulting output.</span></span> <span data-ttu-id="13a34-646">对于 ASP.NET 页，Page Inspector 允许你确定哪些服务器端代码生成了呈现到浏览器中的 HTML 标记。</span><span class="sxs-lookup"><span data-stu-id="13a34-646">For ASP.NET pages, Page Inspector lets you determine which server-side code has produced the HTML markup that is rendered to the browser.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image37.png)

<span data-ttu-id="13a34-647">有关 Page Inspector 的详细信息，请参阅以下教程：</span><span class="sxs-lookup"><span data-stu-id="13a34-647">For more information about Page Inspector, please see the following tutorials:</span></span>

- <span data-ttu-id="13a34-648">在[ASP.NET MVC](../mvc/overview/views/using-page-inspector-in-aspnet-mvc.md)中使用 Page Inspector</span><span class="sxs-lookup"><span data-stu-id="13a34-648">Using Page Inspector in [ASP.NET MVC](../mvc/overview/views/using-page-inspector-in-aspnet-mvc.md)</span></span>
- <span data-ttu-id="13a34-649">在[ASP.NET Web 窗体](../web-forms/overview/getting-started/using-page-inspector-in-a-visual-studio-11-beta-web-forms-project.md)中使用 Page Inspector</span><span class="sxs-lookup"><span data-stu-id="13a34-649">Using Page Inspector in [ASP.NET Web Forms](../web-forms/overview/getting-started/using-page-inspector-in-a-visual-studio-11-beta-web-forms-project.md)</span></span>

<a id="_Toc318097425"></a>
### <a name="publishing"></a><span data-ttu-id="13a34-650">发布</span><span class="sxs-lookup"><span data-stu-id="13a34-650">Publishing</span></span>

<a id="_Toc318097426"></a>
#### <a name="publish-profiles"></a><span data-ttu-id="13a34-651">发布配置文件</span><span class="sxs-lookup"><span data-stu-id="13a34-651">Publish profiles</span></span>

<span data-ttu-id="13a34-652">在 Visual Studio 2010 中，Web 应用程序项目的发布信息不会存储在版本控制中，也不会与他人共享。</span><span class="sxs-lookup"><span data-stu-id="13a34-652">In Visual Studio 2010, publishing information for Web application projects is not stored in version control and is not designed for sharing with others.</span></span> <span data-ttu-id="13a34-653">在 Visual Studio 2012 候选发布版中，发布配置文件的格式已更改。</span><span class="sxs-lookup"><span data-stu-id="13a34-653">In Visual Studio 2012 Release Candidate, the format of the publish profile has been changed.</span></span> <span data-ttu-id="13a34-654">它已成为一个团队项目，现在可以轻松地利用基于 MSBuild 的生成。</span><span class="sxs-lookup"><span data-stu-id="13a34-654">It has been made a team artifact, and it is now easy to leverage from builds based on MSBuild.</span></span> <span data-ttu-id="13a34-655">"发布" 对话框中的生成配置信息可在发布之前轻松地切换生成配置。</span><span class="sxs-lookup"><span data-stu-id="13a34-655">Build configuration information is in the Publish dialog box so that you can easily switch build configurations before publishing.</span></span>

<span data-ttu-id="13a34-656">发布配置文件存储在 PublishProfiles 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="13a34-656">Publish profiles are stored in the PublishProfiles folder.</span></span> <span data-ttu-id="13a34-657">文件夹位置取决于所使用的编程语言：</span><span class="sxs-lookup"><span data-stu-id="13a34-657">The location of the folder depends on what programming language you are using:</span></span>

- <span data-ttu-id="13a34-658">C #： Properties\PublishProfiles</span><span class="sxs-lookup"><span data-stu-id="13a34-658">C#: Properties\PublishProfiles</span></span>
- <span data-ttu-id="13a34-659">Visual Basic：我的 Project\PublishProfiles</span><span class="sxs-lookup"><span data-stu-id="13a34-659">Visual Basic: My Project\PublishProfiles</span></span>

<span data-ttu-id="13a34-660">每个配置文件都是一个 MSBuild 文件。</span><span class="sxs-lookup"><span data-stu-id="13a34-660">Each profile is an MSBuild file.</span></span> <span data-ttu-id="13a34-661">在发布过程中，此文件将导入项目的 MSBuild 文件。</span><span class="sxs-lookup"><span data-stu-id="13a34-661">During publishing, this file is imported into the project's MSBuild file.</span></span> <span data-ttu-id="13a34-662">在 Visual Studio 2010 中，如果要对发布或包过程进行更改，则必须将自定义项放在名为 **项目名称**的文件中。</span><span class="sxs-lookup"><span data-stu-id="13a34-662">In Visual Studio 2010, if you want to make changes to the publish or package process, you have to put your customizations in a file named **ProjectName**.wpp.targets.</span></span> <span data-ttu-id="13a34-663">这仍受支持，但你现在可以将你的自定义项放在发布配置文件中。</span><span class="sxs-lookup"><span data-stu-id="13a34-663">This is still supported, but you can now put your customizations in the publish profile itself.</span></span> <span data-ttu-id="13a34-664">这样，自定义将仅用于该配置文件。</span><span class="sxs-lookup"><span data-stu-id="13a34-664">That way, the customizations will be used only for that profile.</span></span>

<span data-ttu-id="13a34-665">你现在还可以利用 MSBuild 中的发布配置文件。</span><span class="sxs-lookup"><span data-stu-id="13a34-665">You can now also leverage publish profiles from MSBuild.</span></span> <span data-ttu-id="13a34-666">为此，请在生成项目时使用以下命令：</span><span class="sxs-lookup"><span data-stu-id="13a34-666">To do so, use the following command when you build the project:</span></span>

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample36.cmd)]

<span data-ttu-id="13a34-667">项目 .csproj 值是项目的路径，ProfileName 是要发布的配置文件的名称。</span><span class="sxs-lookup"><span data-stu-id="13a34-667">The project.csproj value is the path of the project, and ProfileName is the name of the profile to publish.</span></span> <span data-ttu-id="13a34-668">或者，你可以将完整路径传递到发布配置文件，而不是传递 *PublishProfile* 属性的配置文件名称。</span><span class="sxs-lookup"><span data-stu-id="13a34-668">Alternatively, instead of passing the profile name for the *PublishProfile* property, you can pass in the full path to the publish profile.</span></span>

<a id="_Toc318097427"></a>
#### <a name="aspnet-precompilation-and-merge"></a><span data-ttu-id="13a34-669">ASP.NET 预编译和合并</span><span class="sxs-lookup"><span data-stu-id="13a34-669">ASP.NET precompilation and merge</span></span>

<span data-ttu-id="13a34-670">对于 Web 应用程序项目，Visual Studio 2012 候选发布版将在 "打包/发布 Web 属性" 页上添加一个选项，通过该选项，您可以在发布或打包项目时预编译和合并网站的内容。</span><span class="sxs-lookup"><span data-stu-id="13a34-670">For Web application projects, Visual Studio 2012 Release Candidate adds an option on the Package/Publish Web properties page that lets you precompile and merge your site's content when you publish or package the project.</span></span> <span data-ttu-id="13a34-671">若要查看这些选项，请在解决方案资源管理器中右键单击项目，选择 "属性"，然后选择 "打包/发布 Web" 属性页。</span><span class="sxs-lookup"><span data-stu-id="13a34-671">To see these options, right-click the project in Solution Explorer, choose Properties, and then choose the Package/Publish Web property page.</span></span> <span data-ttu-id="13a34-672">下图显示了 "发布之前预编译此应用程序" 选项。</span><span class="sxs-lookup"><span data-stu-id="13a34-672">The following illustration shows the Precompile this application before publishing option.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image6.jpg)

<span data-ttu-id="13a34-673">如果选择此选项，则每当您发布或打包 web 应用程序时，Visual Studio 都会预编译应用程序。</span><span class="sxs-lookup"><span data-stu-id="13a34-673">When this option is selected, Visual Studio precompiles the application whenever you publish or package the web application.</span></span> <span data-ttu-id="13a34-674">如果要控制如何预编译站点或如何合并程序集，请单击 "高级" 按钮以配置这些选项。</span><span class="sxs-lookup"><span data-stu-id="13a34-674">If you want to control how the site is precompiled or how assemblies are merged, click the Advanced button to configure those options.</span></span>

<a id="_Toc318097428"></a>
### <a name="iis-express"></a><span data-ttu-id="13a34-675">IIS Express</span><span class="sxs-lookup"><span data-stu-id="13a34-675">IIS Express</span></span>

<span data-ttu-id="13a34-676">现在 IIS Express 用于测试 Visual Studio 中 web 项目的默认 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="13a34-676">The default web server for testing web projects in Visual Studio is now IIS Express.</span></span> <span data-ttu-id="13a34-677">开发期间本地 web 服务器仍有 Visual Studio 开发服务器，但现在建议使用 IIS Express 服务器。</span><span class="sxs-lookup"><span data-stu-id="13a34-677">The Visual Studio Development Server is still an option for local web server during development, but IIS Express is now the recommended server.</span></span> <span data-ttu-id="13a34-678">在 Visual Studio 11 Beta 中使用 IIS Express 的体验非常类似于在 Visual Studio 2010 SP1 中使用它。</span><span class="sxs-lookup"><span data-stu-id="13a34-678">The experience of using IIS Express in Visual Studio 11 Beta is very similar to using it in Visual Studio 2010 SP1.</span></span>

<a id="_Toc318097429"></a>
## <a name="disclaimer"></a><span data-ttu-id="13a34-679">免责声明</span><span class="sxs-lookup"><span data-stu-id="13a34-679">Disclaimer</span></span>

<span data-ttu-id="13a34-680">这是一份初稿，并可能在本文所述软件最终商业发布之前进行大幅更改。</span><span class="sxs-lookup"><span data-stu-id="13a34-680">This is a preliminary document and may be changed substantially prior to final commercial release of the software described herein.</span></span>

<span data-ttu-id="13a34-681">本文档中包含的信息代表 Microsoft Corporation 在发布之日对所讨论问题的当前观点。</span><span class="sxs-lookup"><span data-stu-id="13a34-681">The information contained in this document represents the current view of Microsoft Corporation on the issues discussed as of the date of publication.</span></span> <span data-ttu-id="13a34-682">由于 Microsoft 必须响应不断变化的市场条件，因此不应将其解释为 Microsoft 作出的承诺，并且 Microsoft 无法保证在发布日期之后提供的任何信息的准确性。</span><span class="sxs-lookup"><span data-stu-id="13a34-682">Because Microsoft must respond to changing market conditions, it should not be interpreted to be a commitment on the part of Microsoft, and Microsoft cannot guarantee the accuracy of any information presented after the date of publication.</span></span>

<span data-ttu-id="13a34-683">本白皮书仅用于提供信息。</span><span class="sxs-lookup"><span data-stu-id="13a34-683">This White Paper is for informational purposes only.</span></span> <span data-ttu-id="13a34-684">MICROSOFT 对本文档中的信息不做任何明示、暗示或法定的担保。</span><span class="sxs-lookup"><span data-stu-id="13a34-684">MICROSOFT MAKES NO WARRANTIES, EXPRESS, IMPLIED OR STATUTORY, AS TO THE INFORMATION IN THIS DOCUMENT.</span></span>

<span data-ttu-id="13a34-685">用户有责任遵守所有适用的版权法/著作权法。</span><span class="sxs-lookup"><span data-stu-id="13a34-685">Complying with all applicable copyright laws is the responsibility of the user.</span></span> <span data-ttu-id="13a34-686">在不限制版权所辖权利的前提下，未经 Microsoft Corporation 的明确书面许可，本文档的任何部分不得被复制、存储或引进检索系统，或者以任何形式、任何方式（电子、机械、影印、录音等）或为任何目的进行传播。</span><span class="sxs-lookup"><span data-stu-id="13a34-686">Without limiting the rights under copyright, no part of this document may be reproduced, stored in or introduced into a retrieval system, or transmitted in any form or by any means (electronic, mechanical, photocopying, recording, or otherwise), or for any purpose, without the express written permission of Microsoft Corporation.</span></span>

<span data-ttu-id="13a34-687">Microsoft 可能拥有本文档所涵盖主题的专利、专利申请、商标、版权或其他知识产权。</span><span class="sxs-lookup"><span data-stu-id="13a34-687">Microsoft may have patents, patent applications, trademarks, copyrights, or other intellectual property rights covering subject matter in this document.</span></span> <span data-ttu-id="13a34-688">除非 Microsoft 提供了明确的书面许可协议，否则提供本文档并不意味着赋予您这些专利、商标、版权或其他知识产权的任何许可。</span><span class="sxs-lookup"><span data-stu-id="13a34-688">Except as expressly provided in any written license agreement from Microsoft, the furnishing of this document does not give you any license to these patents, trademarks, copyrights, or other intellectual property.</span></span>

<span data-ttu-id="13a34-689">除非另有说明，否则，本文档中提及的示例公司、组织、产品、域名、电子邮件地址、徽标、人员、地点和事件均属虚构，与任何真实的公司、组织、产品、域名、电子邮件地址、徽标、人物、地点或事件没有任何关联。</span><span class="sxs-lookup"><span data-stu-id="13a34-689">Unless otherwise noted, the example companies, organizations, products, domain names, email addresses, logos, people, places and events depicted herein are fictitious, and no association with any real company, organization, product, domain name, email address, logo, person, place or event is intended or should be inferred.</span></span>

<span data-ttu-id="13a34-690">(C) 2012 Microsoft Corporation。</span><span class="sxs-lookup"><span data-stu-id="13a34-690">© 2012 Microsoft Corporation.</span></span> <span data-ttu-id="13a34-691">保留所有权利。</span><span class="sxs-lookup"><span data-stu-id="13a34-691">All rights reserved.</span></span>

<span data-ttu-id="13a34-692">Microsoft 和 Windows 是 Microsoft Corporation 在美国和/或其他国家/地区的注册商标或商标。</span><span class="sxs-lookup"><span data-stu-id="13a34-692">Microsoft and Windows are either registered trademarks or trademarks of Microsoft Corporation in the United States and/or other countries.</span></span>

<span data-ttu-id="13a34-693">此处提到的真实公司和产品的名称可能是其各自所有者的商标。</span><span class="sxs-lookup"><span data-stu-id="13a34-693">The names of actual companies and products mentioned herein may be the trademarks of their respective owners.</span></span>

---
uid: whitepapers/whats-new-in-aspnet-45-and-visual-studio-2012
title: ASP.NET 4.5 和视觉工作室 2012 中的新增功能 |微软文档
author: rick-anderson
description: 本文档介绍 ASP.NET 4.5 中引入的新功能和增强功能。 它还描述了为 Web 开发所做的改进...
ms.author: riande
ms.date: 02/29/2012
ms.assetid: ba1fabb4-31a3-4ebf-8327-41a6bbba6eaf
msc.legacyurl: /whitepapers/whats-new-in-aspnet-45-and-visual-studio-2012
msc.type: content
ms.openlocfilehash: 32fbf7c25b00f3f0796c4c3fdd38ca2a86c89199
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675885"
---
# <a name="whats-new-in-aspnet-45-and-visual-studio-2012"></a><span data-ttu-id="83b60-104">ASP.NET 4.5 和 Visual Studio 2012 的新增功能</span><span class="sxs-lookup"><span data-stu-id="83b60-104">What's New in ASP.NET 4.5 and Visual Studio 2012</span></span>

> <span data-ttu-id="83b60-105">本文档介绍 ASP.NET 4.5 中引入的新功能和增强功能。</span><span class="sxs-lookup"><span data-stu-id="83b60-105">This document describes new features and enhancements that are being introduced in ASP.NET 4.5.</span></span> <span data-ttu-id="83b60-106">它还描述了在 Visual Studio 2012 中为 Web 开发所做的改进。</span><span class="sxs-lookup"><span data-stu-id="83b60-106">It also describes improvements being made for web development in Visual Studio 2012.</span></span> <span data-ttu-id="83b60-107">本文档最初发布于 2012 年 2 月 29 日。</span><span class="sxs-lookup"><span data-stu-id="83b60-107">This document was originally published on February 29, 2012.</span></span>

- [<span data-ttu-id="83b60-108">ASP.NET核心运行时和框架</span><span class="sxs-lookup"><span data-stu-id="83b60-108">ASP.NET Core Runtime and Framework</span></span>](#_Toc318097372)

    - [<span data-ttu-id="83b60-109">异步读取和写入 HTTP 请求和响应</span><span class="sxs-lookup"><span data-stu-id="83b60-109">Asynchronously Reading and Writing HTTP Requests and Responses</span></span>](#_Toc318097373)
    - [<span data-ttu-id="83b60-110">HttpRequest 处理的改进</span><span class="sxs-lookup"><span data-stu-id="83b60-110">Improvements to HttpRequest handling</span></span>](#_Toc318097374)
    - [<span data-ttu-id="83b60-111">异步刷新响应</span><span class="sxs-lookup"><span data-stu-id="83b60-111">Asynchronously flushing a response</span></span>](#_Toc318097375)
    - [<span data-ttu-id="83b60-112">支持*等待*和基于*任务的*异步模块和处理程序</span><span class="sxs-lookup"><span data-stu-id="83b60-112">Support for *await* and *Task*-Based Asynchronous Modules and Handlers</span></span>](#_Toc318097376)
    - [<span data-ttu-id="83b60-113">异步 HTTP 模块</span><span class="sxs-lookup"><span data-stu-id="83b60-113">Asynchronous HTTP modules</span></span>](#_Toc318097377)
    - [<span data-ttu-id="83b60-114">异步 HTTP 处理程序</span><span class="sxs-lookup"><span data-stu-id="83b60-114">Asynchronous HTTP handlers</span></span>](#_Toc318097378)
    - [<span data-ttu-id="83b60-115">新的ASP.NET请求验证功能</span><span class="sxs-lookup"><span data-stu-id="83b60-115">New ASP.NET Request Validation Features</span></span>](#_Toc318097379)
    - [<span data-ttu-id="83b60-116">延迟（"延迟"）请求验证</span><span class="sxs-lookup"><span data-stu-id="83b60-116">Deferred ("lazy") request validation</span></span>](#_Toc318097380)
    - [<span data-ttu-id="83b60-117">支持未经验证的请求</span><span class="sxs-lookup"><span data-stu-id="83b60-117">Support for unvalidated requests</span></span>](#_Toc318097381)
    - [<span data-ttu-id="83b60-118">AntiXSS 库</span><span class="sxs-lookup"><span data-stu-id="83b60-118">AntiXSS Library</span></span>](#_Toc318097382)
    - [<span data-ttu-id="83b60-119">支持 WebSocket 协议</span><span class="sxs-lookup"><span data-stu-id="83b60-119">Support for WebSockets Protocol</span></span>](#_Toc318097383)
    - [<span data-ttu-id="83b60-120">捆绑和最小化</span><span class="sxs-lookup"><span data-stu-id="83b60-120">Bundling and Minification</span></span>](#_Toc318097384)
    - [<span data-ttu-id="83b60-121">Web 托管的性能改进</span><span class="sxs-lookup"><span data-stu-id="83b60-121">Performance Improvements for Web Hosting</span></span>](#_Toc_perf)

        - [<span data-ttu-id="83b60-122">关键性能因素</span><span class="sxs-lookup"><span data-stu-id="83b60-122">Key Performance Factors</span></span>](#_Toc_perf_1)
        - [<span data-ttu-id="83b60-123">对新性能功能的要求</span><span class="sxs-lookup"><span data-stu-id="83b60-123">Requirements for New Performance Features</span></span>](#_Toc_perf_2)
        - [<span data-ttu-id="83b60-124">共享公共程序集</span><span class="sxs-lookup"><span data-stu-id="83b60-124">Sharing Common Assemblies</span></span>](#_Toc_perf_3)
        - [<span data-ttu-id="83b60-125">使用多核 JIT 编译，加快启动速度</span><span class="sxs-lookup"><span data-stu-id="83b60-125">Using multi-Core JIT compilation for faster startup</span></span>](#_Toc_perf_4)
        - [<span data-ttu-id="83b60-126">调整垃圾回收以优化内存</span><span class="sxs-lookup"><span data-stu-id="83b60-126">Tuning garbage collection to optimize for memory</span></span>](#_Toc_perf_5)
        - [<span data-ttu-id="83b60-127">为 Web 应用程序预取</span><span class="sxs-lookup"><span data-stu-id="83b60-127">Prefetching for web applications</span></span>](#_Toc_perf_6)
- [<span data-ttu-id="83b60-128">ASP.NET Web 表单</span><span class="sxs-lookup"><span data-stu-id="83b60-128">ASP.NET Web Forms</span></span>](#_Toc318097385)

    - [<span data-ttu-id="83b60-129">强类型化数据控件</span><span class="sxs-lookup"><span data-stu-id="83b60-129">Strongly Typed Data Controls</span></span>](#_Toc318097386)
    - [<span data-ttu-id="83b60-130">模型绑定</span><span class="sxs-lookup"><span data-stu-id="83b60-130">Model Binding</span></span>](#_Toc318097387)

        - [<span data-ttu-id="83b60-131">选择数据</span><span class="sxs-lookup"><span data-stu-id="83b60-131">Selecting data</span></span>](#_Toc318097388)
        - [<span data-ttu-id="83b60-132">价值提供者</span><span class="sxs-lookup"><span data-stu-id="83b60-132">Value providers</span></span>](#_Toc318097389)
        - [<span data-ttu-id="83b60-133">按控件的值筛选</span><span class="sxs-lookup"><span data-stu-id="83b60-133">Filtering by values from a control</span></span>](#_Toc318097390)
    - [<span data-ttu-id="83b60-134">HTML 编码数据绑定表达式</span><span class="sxs-lookup"><span data-stu-id="83b60-134">HTML Encoded Data-Binding Expressions</span></span>](#_Toc318097391)
    - [<span data-ttu-id="83b60-135">不显眼的验证</span><span class="sxs-lookup"><span data-stu-id="83b60-135">Unobtrusive Validation</span></span>](#_Toc318097392)
    - [<span data-ttu-id="83b60-136">HTML5 更新</span><span class="sxs-lookup"><span data-stu-id="83b60-136">HTML5 Updates</span></span>](#_Toc318097393)
- [<span data-ttu-id="83b60-137">ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="83b60-137">ASP.NET MVC 4</span></span>](#_Toc318097394)
- [<span data-ttu-id="83b60-138">ASP.NET 网页 2</span><span class="sxs-lookup"><span data-stu-id="83b60-138">ASP.NET Web Pages 2</span></span>](#_Toc318097395)
- [<span data-ttu-id="83b60-139">Visual Studio 2012 候选发布版本</span><span class="sxs-lookup"><span data-stu-id="83b60-139">Visual Studio 2012 Release Candidate</span></span>](#_Toc318097396)

    - [<span data-ttu-id="83b60-140">Visual Studio 2010 和 Visual Studio 2012 版本候选版本之间的项目共享（项目兼容性）</span><span class="sxs-lookup"><span data-stu-id="83b60-140">Project Sharing Between Visual Studio 2010 and Visual Studio 2012 Release Candidate (Project Compatibility)</span></span>](#project-compatibility)
    - [<span data-ttu-id="83b60-141">ASP.NET 4.5 网站模板中的配置更改</span><span class="sxs-lookup"><span data-stu-id="83b60-141">Configuration Changes in ASP.NET 4.5 Website Templates</span></span>](#Configuration_Changes_In_ASPNET45_Website_Templates)
    - [<span data-ttu-id="83b60-142">IIS 7 中用于ASP.NET路由的本机支持</span><span class="sxs-lookup"><span data-stu-id="83b60-142">Native Support in IIS 7 for ASP.NET Routing</span></span>](#Native_Support_In_IIS7_For_ASPNET_Routine)
    - [<span data-ttu-id="83b60-143">HTML 编辑器</span><span class="sxs-lookup"><span data-stu-id="83b60-143">HTML Editor</span></span>](#_Toc318097397)

        - [<span data-ttu-id="83b60-144">智能任务</span><span class="sxs-lookup"><span data-stu-id="83b60-144">Smart Tasks</span></span>](#_Toc318097398)
        - [<span data-ttu-id="83b60-145">WAI-ARIA 支持</span><span class="sxs-lookup"><span data-stu-id="83b60-145">WAI-ARIA support</span></span>](#_Toc318097399)
        - [<span data-ttu-id="83b60-146">新的 HTML5 代码段</span><span class="sxs-lookup"><span data-stu-id="83b60-146">New HTML5 snippets</span></span>](#_Toc318097400)
        - [<span data-ttu-id="83b60-147">提取到用户控件</span><span class="sxs-lookup"><span data-stu-id="83b60-147">Extract to user control</span></span>](#_Toc318097401)
        - [<span data-ttu-id="83b60-148">属性中代码块的 IntelliSense</span><span class="sxs-lookup"><span data-stu-id="83b60-148">IntelliSense for code nuggets in attributes</span></span>](#_Toc318097402)
        - [<span data-ttu-id="83b60-149">重命名打开或关闭标记时自动重命名匹配标记</span><span class="sxs-lookup"><span data-stu-id="83b60-149">Automatic renaming of matching tag when you rename an opening or closing tag</span></span>](#_Toc318097403)
        - [<span data-ttu-id="83b60-150">事件处理程序生成</span><span class="sxs-lookup"><span data-stu-id="83b60-150">Event handler generation</span></span>](#_Toc318097404)
        - [<span data-ttu-id="83b60-151">智能缩进</span><span class="sxs-lookup"><span data-stu-id="83b60-151">Smart indent</span></span>](#_Toc318097405)
        - [<span data-ttu-id="83b60-152">自动减少语句完成</span><span class="sxs-lookup"><span data-stu-id="83b60-152">Auto-reduce statement completion</span></span>](#_Toc318097406)
    - [<span data-ttu-id="83b60-153">JavaScript 编辑器</span><span class="sxs-lookup"><span data-stu-id="83b60-153">JavaScript Editor</span></span>](#_Toc318097407)

        - [<span data-ttu-id="83b60-154">代码概述</span><span class="sxs-lookup"><span data-stu-id="83b60-154">Code outlining</span></span>](#_Toc318097408)
        - [<span data-ttu-id="83b60-155">大括号匹配</span><span class="sxs-lookup"><span data-stu-id="83b60-155">Brace matching</span></span>](#_Toc318097409)
        - [<span data-ttu-id="83b60-156">转到定义</span><span class="sxs-lookup"><span data-stu-id="83b60-156">Go to Definition</span></span>](#_Toc318097410)
        - [<span data-ttu-id="83b60-157">ECMAScript5 支持</span><span class="sxs-lookup"><span data-stu-id="83b60-157">ECMAScript5 support</span></span>](#_Toc318097411)
        - [<span data-ttu-id="83b60-158">DOM 感知</span><span class="sxs-lookup"><span data-stu-id="83b60-158">DOM IntelliSense</span></span>](#_Toc318097412)
        - [<span data-ttu-id="83b60-159">VSDOC 签名重载</span><span class="sxs-lookup"><span data-stu-id="83b60-159">VSDOC signature overloads</span></span>](#_Toc318097413)
        - [<span data-ttu-id="83b60-160">隐式引用</span><span class="sxs-lookup"><span data-stu-id="83b60-160">Implicit references</span></span>](#_Toc318097414)
    - [<span data-ttu-id="83b60-161">CSS 编辑器</span><span class="sxs-lookup"><span data-stu-id="83b60-161">CSS Editor</span></span>](#_Toc318097415)

        - [<span data-ttu-id="83b60-162">自动减少语句完成</span><span class="sxs-lookup"><span data-stu-id="83b60-162">Auto-reduce statement completion</span></span>](#_Toc318097416)
        - [<span data-ttu-id="83b60-163">分层缩进。</span><span class="sxs-lookup"><span data-stu-id="83b60-163">Hierarchical indentation.</span></span>](#_Toc318097417)
        - [<span data-ttu-id="83b60-164">CSS 黑客支持</span><span class="sxs-lookup"><span data-stu-id="83b60-164">CSS hacks support</span></span>](#_Toc318097418)
        - [<span data-ttu-id="83b60-165">供应商特定的架构（-moz-,-webkit）</span><span class="sxs-lookup"><span data-stu-id="83b60-165">Vendor specific schemas (-moz-,-webkit)</span></span>](#_Toc318097419)
        - [<span data-ttu-id="83b60-166">评论和非评论支持</span><span class="sxs-lookup"><span data-stu-id="83b60-166">Commenting and uncommenting support</span></span>](#_Toc318097420)
        - [<span data-ttu-id="83b60-167">颜色选取器</span><span class="sxs-lookup"><span data-stu-id="83b60-167">Color picker</span></span>](#_Toc318097421)
        - [<span data-ttu-id="83b60-168">片段</span><span class="sxs-lookup"><span data-stu-id="83b60-168">Snippets</span></span>](#_Toc318097422)
        - [<span data-ttu-id="83b60-169">自定义区域</span><span class="sxs-lookup"><span data-stu-id="83b60-169">Custom regions</span></span>](#_Toc318097423)
    - [<span data-ttu-id="83b60-170">Page Inspector</span><span class="sxs-lookup"><span data-stu-id="83b60-170">Page Inspector</span></span>](#_Toc318097424)
    - [<span data-ttu-id="83b60-171">发布</span><span class="sxs-lookup"><span data-stu-id="83b60-171">Publishing</span></span>](#_Toc318097425)

        - [<span data-ttu-id="83b60-172">发布配置文件</span><span class="sxs-lookup"><span data-stu-id="83b60-172">Publish profiles</span></span>](#_Toc318097426)
        - [<span data-ttu-id="83b60-173">ASP.NET预编译和合并</span><span class="sxs-lookup"><span data-stu-id="83b60-173">ASP.NET precompilation and merge</span></span>](#_Toc318097427)
- [<span data-ttu-id="83b60-174">IIS Express</span><span class="sxs-lookup"><span data-stu-id="83b60-174">IIS Express</span></span>](#_Toc318097428)
- [<span data-ttu-id="83b60-175">免责声明</span><span class="sxs-lookup"><span data-stu-id="83b60-175">Disclaimer</span></span>](#_Toc318097429)

<a id="_Toc318097372"></a>
## <a name="aspnet-core-runtime-and-framework"></a><span data-ttu-id="83b60-176">ASP.NET核心运行时和框架</span><span class="sxs-lookup"><span data-stu-id="83b60-176">ASP.NET Core Runtime and Framework</span></span>

<a id="_Toc318097373"></a>
### <a name="asynchronously-reading-and-writing-http-requests-and-responses"></a><span data-ttu-id="83b60-177">异步读取和写入 HTTP 请求和响应</span><span class="sxs-lookup"><span data-stu-id="83b60-177">Asynchronously Reading and Writing HTTP Requests and Responses</span></span>

<span data-ttu-id="83b60-178">ASP.NET 4 引入了使用*httpRequest.Get 无缓冲区输入流*方法将 HTTP 请求实体作为流读取的功能。</span><span class="sxs-lookup"><span data-stu-id="83b60-178">ASP.NET 4 introduced the ability to read an HTTP request entity as a stream using the *HttpRequest.GetBufferlessInputStream* method.</span></span> <span data-ttu-id="83b60-179">此方法提供了对请求实体的流式访问。</span><span class="sxs-lookup"><span data-stu-id="83b60-179">This method provided streaming access to the request entity.</span></span> <span data-ttu-id="83b60-180">但是，它同步执行，在请求的持续时间内将线程捆绑在一起。</span><span class="sxs-lookup"><span data-stu-id="83b60-180">However, it executed synchronously, which tied up a thread for the duration of a request.</span></span>

<span data-ttu-id="83b60-181">ASP.NET 4.5 支持在 HTTP 请求实体上异步读取流的功能，以及异步刷新的能力。</span><span class="sxs-lookup"><span data-stu-id="83b60-181">ASP.NET 4.5 supports the ability to read streams asynchronously on an HTTP request entity, and the ability to flush asynchronously.</span></span> <span data-ttu-id="83b60-182">ASP.NET 4.5 还使您能够对 HTTP 请求实体进行双缓冲，从而更轻松地与下游 HTTP 处理程序（如 .aspx 页处理程序和 ASP.NET MVC 控制器）集成。</span><span class="sxs-lookup"><span data-stu-id="83b60-182">ASP.NET 4.5 also gives you the ability to double-buffer an HTTP request entity, which provides easier integration with downstream HTTP handlers such as .aspx page handlers and ASP.NET MVC controllers.</span></span>

<a id="_Toc318097374"></a>
#### <a name="improvements-to-httprequest-handling"></a><span data-ttu-id="83b60-183">HttpRequest 处理的改进</span><span class="sxs-lookup"><span data-stu-id="83b60-183">Improvements to HttpRequest handling</span></span>

<span data-ttu-id="83b60-184">ASP.NET 4.5 从 HttpRequest 返回的流引用 *.Get无缓冲区输入流*支持同步和异步读取方法。</span><span class="sxs-lookup"><span data-stu-id="83b60-184">The Stream reference returned by ASP.NET 4.5 from *HttpRequest.GetBufferlessInputStream* supports both synchronous and asynchronous read methods.</span></span> <span data-ttu-id="83b60-185">从*Get 无缓冲区输入流*返回的*流*对象现在实现了 BeginRead 和 EndRead 方法。</span><span class="sxs-lookup"><span data-stu-id="83b60-185">The *Stream* object returned from *GetBufferlessInputStream* now implements both the BeginRead and EndRead methods.</span></span> <span data-ttu-id="83b60-186">异步*流*方法允许您以块异步读取请求实体，而ASP.NET在异步读取循环的每个迭代之间释放当前线程。</span><span class="sxs-lookup"><span data-stu-id="83b60-186">The asynchronous *Stream* methods let you asynchronously read the request entity in chunks, while ASP.NET releases the current thread between each iteration of an asynchronous read loop.</span></span>

<span data-ttu-id="83b60-187">ASP.NET 4.5 还添加了一种以缓冲方式读取请求实体的配套方法 *：httpRequest.GetBufferedInputStream*。</span><span class="sxs-lookup"><span data-stu-id="83b60-187">ASP.NET 4.5 has also added a companion method for reading the request entity in a buffered way: *HttpRequest.GetBufferedInputStream*.</span></span> <span data-ttu-id="83b60-188">这种新的重载工作类似于*Get 无缓冲区输入流*，支持同步读取和异步读取。</span><span class="sxs-lookup"><span data-stu-id="83b60-188">This new overload works like *GetBufferlessInputStream*, supporting both synchronous and asynchronous reads.</span></span> <span data-ttu-id="83b60-189">但是，在读取时 *，GetBufferedInputStream*还会将实体字节复制到ASP.NET内部缓冲区中，以便下游模块和处理程序仍可以访问请求实体。</span><span class="sxs-lookup"><span data-stu-id="83b60-189">However, as it reads, *GetBufferedInputStream* also copies the entity bytes into ASP.NET internal buffers so that downstream modules and handlers can still access the request entity.</span></span> <span data-ttu-id="83b60-190">例如，如果管道中的一些上游代码已经使用*GetBufferedInputStream*读取了请求实体，您仍可以使用*HttpRequest.Form*或*httpRequest.Files*。</span><span class="sxs-lookup"><span data-stu-id="83b60-190">For example, if some upstream code in the pipeline has already read the request entity using *GetBufferedInputStream*, you can still use *HttpRequest.Form* or *HttpRequest.Files*.</span></span> <span data-ttu-id="83b60-191">这允许您对请求执行异步处理（例如，将大型文件上载流式传输到数据库），但之后仍运行 .aspx 页和 MVC ASP.NET控制器。</span><span class="sxs-lookup"><span data-stu-id="83b60-191">This lets you perform asynchronous processing on a request (for example, streaming a large file upload to a database), but still run .aspx pages and MVC ASP.NET controllers afterward.</span></span>

<a id="_Toc318097375"></a>
#### <a name="asynchronously-flushing-a-response"></a><span data-ttu-id="83b60-192">异步刷新响应</span><span class="sxs-lookup"><span data-stu-id="83b60-192">Asynchronously flushing a response</span></span>

<span data-ttu-id="83b60-193">当客户端距离遥远或具有低带宽连接时，向 HTTP 客户端发送响应可能需要相当长的时间。</span><span class="sxs-lookup"><span data-stu-id="83b60-193">Sending responses to an HTTP client can take considerable time when the client is far away or has a low-bandwidth connection.</span></span> <span data-ttu-id="83b60-194">通常ASP.NET缓冲响应字节，因为它们是由应用程序创建的。</span><span class="sxs-lookup"><span data-stu-id="83b60-194">Normally ASP.NET buffers the response bytes as they are created by an application.</span></span> <span data-ttu-id="83b60-195">然后ASP.NET然后在请求处理的末尾执行累积缓冲区的单个发送操作。</span><span class="sxs-lookup"><span data-stu-id="83b60-195">ASP.NET then performs a single send operation of the accrued buffers at the very end of request processing.</span></span>

<span data-ttu-id="83b60-196">如果缓冲响应很大（例如，将大型文件流式传输到客户端），则必须定期调用*HttpResponse.Flush，* 以便向客户端发送缓冲输出并保持内存使用情况控制。</span><span class="sxs-lookup"><span data-stu-id="83b60-196">If the buffered response is large (for example, streaming a large file to a client), you must periodically call *HttpResponse.Flush* to send buffered output to the client and keep memory usage under control.</span></span> <span data-ttu-id="83b60-197">但是，由于*Flush*是同步调用，因此迭代调用*Flush*仍会在可能长时间运行的请求的持续时间内使用线程。</span><span class="sxs-lookup"><span data-stu-id="83b60-197">However, because *Flush* is a synchronous call, iteratively calling *Flush* still consumes a thread for the duration of potentially long-running requests.</span></span>

<span data-ttu-id="83b60-198">ASP.NET 4.5 添加了使用*HttpResponse*类的*BeginFlush*和*endFlush*方法异步执行刷新的支持。</span><span class="sxs-lookup"><span data-stu-id="83b60-198">ASP.NET 4.5 adds support for performing flushes asynchronously using the *BeginFlush* and *EndFlush* methods of the *HttpResponse* class.</span></span> <span data-ttu-id="83b60-199">使用这些方法，您可以创建异步模块和异步处理程序，这些模块和异步处理程序在不捆绑操作系统线程的情况下将数据增量发送到客户端。</span><span class="sxs-lookup"><span data-stu-id="83b60-199">Using these methods, you can create asynchronous modules and asynchronous handlers that incrementally send data to a client without tying up operating-system threads.</span></span> <span data-ttu-id="83b60-200">在*BeginFlush*和*结束刷新*调用之间，ASP.NET释放当前线程。</span><span class="sxs-lookup"><span data-stu-id="83b60-200">In between *BeginFlush* and *EndFlush* calls, ASP.NET releases the current thread.</span></span> <span data-ttu-id="83b60-201">这大大减少了支持长时间运行的 HTTP 下载所需的活动线程总数。</span><span class="sxs-lookup"><span data-stu-id="83b60-201">This substantially reduces the total number of active threads that are needed in order to support long-running HTTP downloads.</span></span>

<a id="_Toc318097376"></a>
### <a name="support-for-await-and-task---based-asynchronous-modules-and-handlers"></a><span data-ttu-id="83b60-202">支持*等待*和*任务*- 基于异步模块和处理程序</span><span class="sxs-lookup"><span data-stu-id="83b60-202">Support for *await* and *Task* - Based Asynchronous Modules and Handlers</span></span>

<span data-ttu-id="83b60-203">.NET 框架 4 引入了一个异步编程概念，称为*任务*。</span><span class="sxs-lookup"><span data-stu-id="83b60-203">The .NET Framework 4 introduced an asynchronous programming concept referred to as a *task*.</span></span> <span data-ttu-id="83b60-204">任务由系统中的*任务*类型和相关类型表示 *。*</span><span class="sxs-lookup"><span data-stu-id="83b60-204">Tasks are represented by the *Task* type and related types in the *System.Threading.Tasks* namespace.</span></span> <span data-ttu-id="83b60-205">.NET Framework 4.5 基于此功能，具有编译器增强功能，使使用*Task*对象变得简单。</span><span class="sxs-lookup"><span data-stu-id="83b60-205">The .NET Framework 4.5 builds on this with compiler enhancements that make working with *Task* objects simple.</span></span> <span data-ttu-id="83b60-206">在 .NET 框架 4.5 中，编译器支持两个新关键字：*等待*和*异步*。</span><span class="sxs-lookup"><span data-stu-id="83b60-206">In the .NET Framework 4.5, the compilers support two new keywords: *await* and *async*.</span></span> <span data-ttu-id="83b60-207">*await*关键字是语法速记，用于指示代码段应异步等待其他代码段。</span><span class="sxs-lookup"><span data-stu-id="83b60-207">The *await* keyword is syntactical shorthand for indicating that a piece of code should asynchronously wait on some other piece of code.</span></span> <span data-ttu-id="83b60-208">*异步*关键字表示可用于将方法标记为基于任务的异步方法的提示。</span><span class="sxs-lookup"><span data-stu-id="83b60-208">The *async* keyword represents a hint that you can use to mark methods as task-based asynchronous methods.</span></span>

<span data-ttu-id="83b60-209">*await、\*\*异步*和*任务*对象的组合使您在 .NET 4.5 中编写异步代码变得更加容易。</span><span class="sxs-lookup"><span data-stu-id="83b60-209">The combination of *await*, *async*, and the *Task* object makes it much easier for you to write asynchronous code in .NET 4.5.</span></span> <span data-ttu-id="83b60-210">ASP.NET 4.5 支持这些简化与新的 API，允许您编写异步 HTTP 模块和异步 HTTP 处理程序使用新的编译器增强功能。</span><span class="sxs-lookup"><span data-stu-id="83b60-210">ASP.NET 4.5 supports these simplifications with new APIs that let you write asynchronous HTTP modules and asynchronous HTTP handlers using the new compiler enhancements.</span></span>

<a id="_Toc318097377"></a>
#### <a name="asynchronous-http-modules"></a><span data-ttu-id="83b60-211">异步 HTTP 模块</span><span class="sxs-lookup"><span data-stu-id="83b60-211">Asynchronous HTTP modules</span></span>

<span data-ttu-id="83b60-212">假设您要在返回*任务*对象的方法内执行异步工作。</span><span class="sxs-lookup"><span data-stu-id="83b60-212">Suppose that you want to perform asynchronous work within a method that returns a *Task* object.</span></span> <span data-ttu-id="83b60-213">以下代码示例定义了一个异步方法，该方法进行异步调用以下载 Microsoft 主页。</span><span class="sxs-lookup"><span data-stu-id="83b60-213">The following code example defines an asynchronous method that makes an asynchronous call to download the Microsoft home page.</span></span> <span data-ttu-id="83b60-214">请注意在方法签名中使用*异步*关键字，并注意对*下载StringTaskAsync*的*等待*调用。</span><span class="sxs-lookup"><span data-stu-id="83b60-214">Notice the use of the *async* keyword in the method signature and the *await* call to *DownloadStringTaskAsync*.</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample1.cs)]

<span data-ttu-id="83b60-215">这就是您需要编写的 - .NET Framework 将自动处理在等待下载完成时展开调用堆栈，以及在下载完成后自动还原调用堆栈。</span><span class="sxs-lookup"><span data-stu-id="83b60-215">That's all you have to write — the .NET Framework will automatically handle unwinding the call stack while waiting for the download to complete, as well as automatically restoring the call stack after the download is done.</span></span>

<span data-ttu-id="83b60-216">现在假设您要在异步ASP.NET HTTP 模块中使用此异步方法。</span><span class="sxs-lookup"><span data-stu-id="83b60-216">Now suppose that you want to use this asynchronous method in an asynchronous ASP.NET HTTP module.</span></span> <span data-ttu-id="83b60-217">ASP.NET 4.5 包括帮助器方法 *（EventHandlerTaskAsyncHelper*） 和新的委托类型 *（TaskEventHandler），* 可用于将基于任务的异步方法与 ASP.NET HTTP 管道公开的较旧的异步编程模型集成。</span><span class="sxs-lookup"><span data-stu-id="83b60-217">ASP.NET 4.5 includes a helper method (*EventHandlerTaskAsyncHelper*) and a new delegate type (*TaskEventHandler*) that you can use to integrate task-based asynchronous methods with the older asynchronous programming model exposed by the ASP.NET HTTP pipeline.</span></span> <span data-ttu-id="83b60-218">此示例演示如何：</span><span class="sxs-lookup"><span data-stu-id="83b60-218">This example shows how:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample2.cs)]

<a id="_Toc318097378"></a>
#### <a name="asynchronous-http-handlers"></a><span data-ttu-id="83b60-219">异步 HTTP 处理程序</span><span class="sxs-lookup"><span data-stu-id="83b60-219">Asynchronous HTTP handlers</span></span>

<span data-ttu-id="83b60-220">在ASP.NET中编写异步处理程序的传统方法是实现*IHttpAsyncHandler*接口。</span><span class="sxs-lookup"><span data-stu-id="83b60-220">The traditional approach to writing asynchronous handlers in ASP.NET is to implement the *IHttpAsyncHandler* interface.</span></span> <span data-ttu-id="83b60-221">ASP.NET 4.5 引入了可以从派生的*HttpTaskSyncHandler*异步基类型，这使得编写异步处理程序变得更加容易。</span><span class="sxs-lookup"><span data-stu-id="83b60-221">ASP.NET 4.5 introduces the *HttpTaskAsyncHandler* asynchronous base type that you can derive from, which makes it much easier to write asynchronous handlers.</span></span>

<span data-ttu-id="83b60-222">*HttpTaskAsyncHandler*类型是抽象的，需要您重写*ProcessRequestAsync*方法。</span><span class="sxs-lookup"><span data-stu-id="83b60-222">The *HttpTaskAsyncHandler* type is abstract and requires you to override the *ProcessRequestAsync* method.</span></span> <span data-ttu-id="83b60-223">内部ASP.NET负责将*ProcessRequestAsync*的返回签名（*任务*对象）与ASP.NET管道使用的旧异步编程模型集成。</span><span class="sxs-lookup"><span data-stu-id="83b60-223">Internally ASP.NET takes care of integrating the return signature (a *Task* object) of *ProcessRequestAsync* with the older asynchronous programming model used by the ASP.NET pipeline.</span></span>

<span data-ttu-id="83b60-224">下面的示例演示如何使用*Task*和*等待*作为异步 HTTP 处理程序实现的一部分：</span><span class="sxs-lookup"><span data-stu-id="83b60-224">The following example shows how you can use *Task* and *await* as part of the implementation of an asynchronous HTTP handler:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample3.cs)]

<a id="_Toc318097379"></a>
### <a name="new-aspnet-request-validation-features"></a><span data-ttu-id="83b60-225">新的ASP.NET请求验证功能</span><span class="sxs-lookup"><span data-stu-id="83b60-225">New ASP.NET Request Validation Features</span></span>

<span data-ttu-id="83b60-226">默认情况下，ASP.NET执行请求验证 - 它会检查在字段、标头、Cookie 等中查找标记或脚本的请求。</span><span class="sxs-lookup"><span data-stu-id="83b60-226">By default, ASP.NET performs request validation — it examines requests to look for markup or script in fields, headers, cookies, and so on.</span></span> <span data-ttu-id="83b60-227">如果检测到任何异常，ASP.NET将引发异常。</span><span class="sxs-lookup"><span data-stu-id="83b60-227">If any is detected, ASP.NET throws an exception.</span></span> <span data-ttu-id="83b60-228">这是抵御潜在跨站点脚本攻击的第一道防线。</span><span class="sxs-lookup"><span data-stu-id="83b60-228">This acts as a first line of defense against potential cross-site scripting attacks.</span></span>

<span data-ttu-id="83b60-229">ASP.NET 4.5 使选择性读取未经验证的请求数据变得容易。</span><span class="sxs-lookup"><span data-stu-id="83b60-229">ASP.NET 4.5 makes it easy to selectively read unvalidated request data.</span></span> <span data-ttu-id="83b60-230">ASP.NET 4.5 还集成了流行的 AntiXSS 库，该库以前是外部库。</span><span class="sxs-lookup"><span data-stu-id="83b60-230">ASP.NET 4.5 also integrates the popular AntiXSS library, which was formerly an external library.</span></span>

<span data-ttu-id="83b60-231">开发人员经常要求能够有选择地关闭其应用程序的请求验证。</span><span class="sxs-lookup"><span data-stu-id="83b60-231">Developers have frequently asked for the ability to selectively turn off request validation for their applications.</span></span> <span data-ttu-id="83b60-232">例如，如果您的应用程序是论坛软件，您可能希望允许用户提交 HTML 格式的论坛帖子和评论，但仍要确保请求验证检查所有其他内容。</span><span class="sxs-lookup"><span data-stu-id="83b60-232">For example, if your application is forum software, you might want to allow users to submit HTML-formatted forum posts and comments, but still make sure that request validation is checking everything else.</span></span>

<span data-ttu-id="83b60-233">ASP.NET 4.5 引入了两个功能，使您能够轻松有选择地处理未验证的输入：延迟（"延迟"）请求验证和对未验证请求数据的访问。</span><span class="sxs-lookup"><span data-stu-id="83b60-233">ASP.NET 4.5 introduces two features that make it easy for you to selectively work with unvalidated input: deferred ("lazy") request validation and access to unvalidated request data.</span></span>

<a id="_Toc318097380"></a>
#### <a name="deferred-lazy-request-validation"></a><span data-ttu-id="83b60-234">延迟（"延迟"）请求验证</span><span class="sxs-lookup"><span data-stu-id="83b60-234">Deferred ("lazy") request validation</span></span>

<span data-ttu-id="83b60-235">在 ASP.NET 4.5 中，默认情况下，所有请求数据都需接受请求验证。</span><span class="sxs-lookup"><span data-stu-id="83b60-235">In ASP.NET 4.5, by default all request data is subject to request validation.</span></span> <span data-ttu-id="83b60-236">但是，您可以将应用程序配置为延迟请求验证，直到实际访问请求数据。</span><span class="sxs-lookup"><span data-stu-id="83b60-236">However, you can configure the application to defer request validation until you actually access request data.</span></span> <span data-ttu-id="83b60-237">（这有时称为延迟请求验证，具体取决于某些数据方案的延迟加载等术语。通过将*请求验证模式*属性设置为*httpRUntime*元素中的 4.5，可以将应用程序配置为在 Web.config 文件中使用延迟验证，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="83b60-237">(This is sometimes referred to as lazy request validation, based on terms like lazy loading for certain data scenarios.) You can configure the application to use deferred validation in the Web.config file by setting the *requestValidationMode* attribute to 4.5 in the *httpRUntime* element, as in the following example:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample4.xml)]

<span data-ttu-id="83b60-238">当请求验证模式设置为 4.5 时，请求验证仅针对特定请求值触发，并且仅在代码访问该值时触发。</span><span class="sxs-lookup"><span data-stu-id="83b60-238">When request validation mode is set to 4.5, request validation is triggered only for a specific request value and only when your code accesses that value.</span></span> <span data-ttu-id="83b60-239">例如，如果代码获取了"Request.Form_"论坛\_帖子"的值，则仅针对窗体集合中该元素调用请求验证。</span><span class="sxs-lookup"><span data-stu-id="83b60-239">For example, if your code gets the value of Request.Form["forum\_post"], request validation is invoked only for that element in the form collection.</span></span> <span data-ttu-id="83b60-240">*窗体*集合中的其他元素均未经过验证。</span><span class="sxs-lookup"><span data-stu-id="83b60-240">None of the other elements in the *Form* collection are validated.</span></span> <span data-ttu-id="83b60-241">在ASP.NET的早期版本中，当访问集合中的任何元素时，将触发整个请求集合的请求验证。</span><span class="sxs-lookup"><span data-stu-id="83b60-241">In previous versions of ASP.NET, request validation was triggered for the entire request collection when any element in the collection was accessed.</span></span> <span data-ttu-id="83b60-242">新的行为使不同的应用程序组件能够更轻松地查看不同的请求数据，而不会触发其他部分的请求验证。</span><span class="sxs-lookup"><span data-stu-id="83b60-242">The new behavior makes it easier for different application components to look at different pieces of request data without triggering request validation on other pieces.</span></span>

<a id="_Toc318097381"></a>
#### <a name="support-for-unvalidated-requests"></a><span data-ttu-id="83b60-243">支持未经验证的请求</span><span class="sxs-lookup"><span data-stu-id="83b60-243">Support for unvalidated requests</span></span>

<span data-ttu-id="83b60-244">仅延迟请求验证并不能解决选择性绕过请求验证的问题。</span><span class="sxs-lookup"><span data-stu-id="83b60-244">Deferred request validation alone doesn't solve the problem of selectively bypassing request validation.</span></span> <span data-ttu-id="83b60-245">对"请求.Form_"论坛\_帖子"的调用仍触发该特定请求值的请求验证。</span><span class="sxs-lookup"><span data-stu-id="83b60-245">The call to Request.Form["forum\_post"] still triggers request validation for that specific request value.</span></span> <span data-ttu-id="83b60-246">但是，您可能希望在不触发验证的情况下访问此字段，因为您希望允许该字段中的标记。</span><span class="sxs-lookup"><span data-stu-id="83b60-246">However, you might want to access this field without triggering validation because you want to allow markup in that field.</span></span>

<span data-ttu-id="83b60-247">为此，ASP.NET 4.5 现在支持对请求数据的未经验证的访问。</span><span class="sxs-lookup"><span data-stu-id="83b60-247">To allow this, ASP.NET 4.5 now supports unvalidated access to request data.</span></span> <span data-ttu-id="83b60-248">ASP.NET 4.5 在*HttpRequest*类中包括一个新的*未验证*集合属性。</span><span class="sxs-lookup"><span data-stu-id="83b60-248">ASP.NET 4.5 includes a new *Unvalidated* collection property in the *HttpRequest* class.</span></span> <span data-ttu-id="83b60-249">此集合提供对请求数据的所有常见值（如*窗体*、*查询字符串\*\*、Cookie*和*Url）* 的访问。</span><span class="sxs-lookup"><span data-stu-id="83b60-249">This collection provides access to all of the common values of request data, like *Form*, *QueryString*, *Cookies*, and *Url*.</span></span>

<span data-ttu-id="83b60-250">使用论坛示例，为了能够读取未经验证的请求数据，首先需要将应用程序配置为使用新的请求验证模式：</span><span class="sxs-lookup"><span data-stu-id="83b60-250">Using the forum example, to be able to read unvalidated request data, you first need to configure the application to use the new request validation mode:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample5.xml)]

<span data-ttu-id="83b60-251">然后，您可以使用*HttpRequest.未验证*的属性读取未验证的窗体值：</span><span class="sxs-lookup"><span data-stu-id="83b60-251">You can then use the *HttpRequest.Unvalidated* property to read the unvalidated form value:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample6.cs)]

> [!WARNING]
> <span data-ttu-id="83b60-252">安全性 -*小心使用未经验证的请求数据！*</span><span class="sxs-lookup"><span data-stu-id="83b60-252">Security - *Use unvalidated request data with care!*</span></span> <span data-ttu-id="83b60-253">ASP.NET 4.5 添加了未经验证的请求属性和集合，以便您更轻松地访问非常具体的未验证请求数据。</span><span class="sxs-lookup"><span data-stu-id="83b60-253">ASP.NET 4.5 added the unvalidated request properties and collections to make it easier for you to access very specific unvalidated request data.</span></span> <span data-ttu-id="83b60-254">但是，您仍必须对原始请求数据执行自定义验证，以确保不会向用户呈现危险文本。</span><span class="sxs-lookup"><span data-stu-id="83b60-254">However, you must still perform custom validation on the raw request data to ensure that dangerous text is not rendered to users.</span></span>

<a id="_Toc318097382"></a>
### <a name="antixss-library"></a><span data-ttu-id="83b60-255">AntiXSS 库</span><span class="sxs-lookup"><span data-stu-id="83b60-255">AntiXSS Library</span></span>

<span data-ttu-id="83b60-256">由于 Microsoft AntiXSS 库的普及，ASP.NET 4.5 现在包含该库版本 4.0 的核心编码例程。</span><span class="sxs-lookup"><span data-stu-id="83b60-256">Due to the popularity of the Microsoft AntiXSS Library, ASP.NET 4.5 now incorporates core encoding routines from version 4.0 of that library.</span></span>

<span data-ttu-id="83b60-257">编码例程由新*系统.Web.Security.AntiXs*命名空间中的*AntiXsEncoder*类型实现。</span><span class="sxs-lookup"><span data-stu-id="83b60-257">The encoding routines are implemented by the *AntiXssEncoder* type in the new *System.Web.Security.AntiXss* namespace.</span></span> <span data-ttu-id="83b60-258">您可以通过调用类型中实现的任何静态编码方法直接使用*AntiXsEncoder*类型。</span><span class="sxs-lookup"><span data-stu-id="83b60-258">You can use the *AntiXssEncoder* type directly by calling any of the static encoding methods that are implemented in the type.</span></span> <span data-ttu-id="83b60-259">但是，使用新的反 XSS 例程的最简单方法是将ASP.NET应用程序配置为默认使用*AntiXsEncoder*类。</span><span class="sxs-lookup"><span data-stu-id="83b60-259">However, the easiest approach for using the new anti-XSS routines is to configure an ASP.NET application to use the *AntiXssEncoder* class by default.</span></span> <span data-ttu-id="83b60-260">为此，向 Web.config 文件添加以下属性：</span><span class="sxs-lookup"><span data-stu-id="83b60-260">To do this, add the following attribute to the Web.config file:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample7.xml)]

<span data-ttu-id="83b60-261">当*编码器类型*属性设置为使用*AntiXsEncoder*类型时，ASP.NET中的所有输出编码将自动使用新的编码例程。</span><span class="sxs-lookup"><span data-stu-id="83b60-261">When the *encoderType* attribute is set to use the *AntiXssEncoder* type, all output encoding in ASP.NET automatically uses the new encoding routines.</span></span>

<span data-ttu-id="83b60-262">这些是外部 AntiXSS 库中已集成到 ASP.NET 4.5 中的部分：</span><span class="sxs-lookup"><span data-stu-id="83b60-262">These are the portions of the external AntiXSS library that have been incorporated into ASP.NET 4.5:</span></span>

- <span data-ttu-id="83b60-263">*Html编码* *，HtmlFormUrl 编码*， 和*html 属性编码*</span><span class="sxs-lookup"><span data-stu-id="83b60-263">*HtmlEncode*, *HtmlFormUrlEncode*, and *HtmlAttributeEncode*</span></span>
- <span data-ttu-id="83b60-264">*XmlAttributeEncode*和*XmlEncode*</span><span class="sxs-lookup"><span data-stu-id="83b60-264">*XmlAttributeEncode* and *XmlEncode*</span></span>
- <span data-ttu-id="83b60-265">*UrlEncode*和*UrlPath 编码*（新）</span><span class="sxs-lookup"><span data-stu-id="83b60-265">*UrlEncode* and *UrlPathEncode* (new)</span></span>
- <span data-ttu-id="83b60-266">*CsEncode*</span><span class="sxs-lookup"><span data-stu-id="83b60-266">*CssEncode*</span></span>

<a id="_Toc318097383"></a>
### <a name="support-for-websockets-protocol"></a><span data-ttu-id="83b60-267">支持 WebSocket 协议</span><span class="sxs-lookup"><span data-stu-id="83b60-267">Support for WebSockets Protocol</span></span>

<span data-ttu-id="83b60-268">WebSockets 协议是基于标准的网络协议，它定义了如何通过 HTTP 在客户端和服务器之间建立安全的实时双向通信。</span><span class="sxs-lookup"><span data-stu-id="83b60-268">WebSockets protocol is a standards-based network protocol that defines how to establish secure, real-time bidirectional communications between a client and a server over HTTP.</span></span> <span data-ttu-id="83b60-269">Microsoft 与 IETF 和 W3C 标准机构合作，帮助定义该协议。</span><span class="sxs-lookup"><span data-stu-id="83b60-269">Microsoft has worked with both the IETF and W3C standards bodies to help define the protocol.</span></span> <span data-ttu-id="83b60-270">WebSockets 协议由任何客户端（而不仅仅是浏览器）支持，Microsoft 在客户端和移动操作系统上投入大量资源支持 WebSocket 协议。</span><span class="sxs-lookup"><span data-stu-id="83b60-270">The WebSockets protocol is supported by any client (not just browsers), with Microsoft investing substantial resources supporting WebSockets protocol on both client and mobile operating systems.</span></span>

<span data-ttu-id="83b60-271">WebSockets 协议使在客户端和服务器之间创建长时间运行的数据传输变得更加容易。</span><span class="sxs-lookup"><span data-stu-id="83b60-271">WebSockets protocol makes it much easier to create long-running data transfers between a client and a server.</span></span> <span data-ttu-id="83b60-272">例如，编写聊天应用程序要容易得多，因为您可以在客户端和服务器之间建立真正的长时间运行的连接。</span><span class="sxs-lookup"><span data-stu-id="83b60-272">For example, writing a chat application is much easier because you can establish a true long-running connection between a client and a server.</span></span> <span data-ttu-id="83b60-273">您不必使用定期轮询或 HTTP 长轮询等解决方法来模拟套接字的行为。</span><span class="sxs-lookup"><span data-stu-id="83b60-273">You do not have to resort to workarounds like periodic polling or HTTP long-polling to simulate the behavior of a socket.</span></span>

<span data-ttu-id="83b60-274">ASP.NET 4.5 和 IIS 8 都支持低级 WebSocket，使ASP.NET开发人员能够使用托管 API 在 WebSocket 对象上异步读取和写入字符串和二进制数据。</span><span class="sxs-lookup"><span data-stu-id="83b60-274">ASP.NET 4.5 and IIS 8 include low-level WebSockets support, enabling ASP.NET developers to use managed APIs for asynchronously reading and writing both string and binary data on a WebSockets object.</span></span> <span data-ttu-id="83b60-275">对于ASP.NET 4.5，有一个新的*System.Web.WebSockets*命名空间，其中包含用于使用 WebSockets 协议的类型。</span><span class="sxs-lookup"><span data-stu-id="83b60-275">For ASP.NET 4.5, there is a new *System.Web.WebSockets* namespace that contains types for working with WebSockets protocol.</span></span>

<span data-ttu-id="83b60-276">浏览器客户端通过创建 DOM WebSocket 对象来建立*WebSocket*连接，该对象指向ASP.NET应用程序中的 URL，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="83b60-276">A browser client establishes a WebSockets connection by creating a DOM *WebSocket* object that points to a URL in an ASP.NET application, as in the following example:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample8.cs)]

<span data-ttu-id="83b60-277">您可以使用任何类型的模块或处理程序在ASP.NET创建 WebSockets 终结点。</span><span class="sxs-lookup"><span data-stu-id="83b60-277">You can create WebSockets endpoints in ASP.NET using any kind of module or handler.</span></span> <span data-ttu-id="83b60-278">在前面的示例中，使用了 .ashx 文件，因为 .ashx 文件是创建处理程序的快速方法。</span><span class="sxs-lookup"><span data-stu-id="83b60-278">In the previous example, an .ashx file was used, because .ashx files are a quick way to create a handler.</span></span>

<span data-ttu-id="83b60-279">根据 WebSocket 协议，ASP.NET应用程序通过指示请求应从 HTTP GET 请求升级到 WebSockets 请求来接受客户端的 WebSockets 请求。</span><span class="sxs-lookup"><span data-stu-id="83b60-279">According to the WebSockets protocol, an ASP.NET application accepts a client's WebSockets request by indicating that the request should be upgraded from an HTTP GET request to a WebSockets request.</span></span> <span data-ttu-id="83b60-280">下面是一个示例：</span><span class="sxs-lookup"><span data-stu-id="83b60-280">Here's an example:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample9.cs)]

<span data-ttu-id="83b60-281">*AcceptWebSocketRequest 方法*接受函数委托，因为ASP.NET解除当前 HTTP 请求，然后将控制权传输到函数委托。</span><span class="sxs-lookup"><span data-stu-id="83b60-281">The *AcceptWebSocketRequest* method accepts a function delegate because ASP.NET unwinds the current HTTP request and then transfers control to the function delegate.</span></span> <span data-ttu-id="83b60-282">从概念上讲，这种方法类似于您使用*System.Threading.Thread*的方式，在其中定义执行后台工作的线程启动委托。</span><span class="sxs-lookup"><span data-stu-id="83b60-282">Conceptually this approach is similar to how you use *System.Threading.Thread*, where you define a thread-start delegate in which background work is performed.</span></span>

<span data-ttu-id="83b60-283">ASP.NET和客户端成功完成 WebSocket 握手后，ASP.NET调用您的委托，WebSockets 应用程序开始运行。</span><span class="sxs-lookup"><span data-stu-id="83b60-283">After ASP.NET and the client have successfully completed a WebSockets handshake, ASP.NET calls your delegate and the WebSockets application starts running.</span></span> <span data-ttu-id="83b60-284">以下代码示例显示了一个简单的回声应用程序，该应用程序在ASP.NET中使用内置 WebSocket 支持：</span><span class="sxs-lookup"><span data-stu-id="83b60-284">The following code example shows a simple echo application that uses the built-in WebSockets support in ASP.NET:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample10.cs)]

<span data-ttu-id="83b60-285">.NET 4.5 中支持*await*关键字和基于异步任务的操作自然适合编写 WebSockets 应用程序。</span><span class="sxs-lookup"><span data-stu-id="83b60-285">The support in .NET 4.5 for the *await* keyword and asynchronous task-based operations is a natural fit for writing WebSockets applications.</span></span> <span data-ttu-id="83b60-286">代码示例显示 WebSockets 请求完全异步地在ASP.NET内部运行。</span><span class="sxs-lookup"><span data-stu-id="83b60-286">The code example shows that a WebSockets request runs completely asynchronously inside ASP.NET.</span></span> <span data-ttu-id="83b60-287">应用程序通过调用*await 套接字以异步等待从客户端发送消息。接收Async*。</span><span class="sxs-lookup"><span data-stu-id="83b60-287">The application waits asynchronously for a message to be sent from a client by calling *await socket.ReceiveAsync*.</span></span> <span data-ttu-id="83b60-288">同样，您可以通过调用*await 套接字向客户端发送异步消息。森步同步*。</span><span class="sxs-lookup"><span data-stu-id="83b60-288">Similarly, you can send an asynchronous message to a client by calling *await socket.SendAsync*.</span></span>

<span data-ttu-id="83b60-289">在浏览器中，应用程序通过*onmessage*功能接收 WebSocket 消息。</span><span class="sxs-lookup"><span data-stu-id="83b60-289">In the browser, an application receives WebSockets messages through an *onmessage* function.</span></span> <span data-ttu-id="83b60-290">要从浏览器发送消息，请调用*WebSocket* DOM 类型的*发送*方法，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="83b60-290">To send a message from a browser, you call the *send* method of the *WebSocket* DOM type, as shown in this example:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample11.cs)]

<span data-ttu-id="83b60-291">将来，我们可能会发布此功能的更新，以抽象掉 WebSocket 应用程序在此版本中所需的一些低级编码。</span><span class="sxs-lookup"><span data-stu-id="83b60-291">In the future, we might release updates to this functionality that abstract away some of the low-level coding that is required in this release for WebSockets applications.</span></span>

<a id="_Toc318097384"></a>
### <a name="bundling-and-minification"></a><span data-ttu-id="83b60-292">捆绑和缩小</span><span class="sxs-lookup"><span data-stu-id="83b60-292">Bundling and Minification</span></span>

<span data-ttu-id="83b60-293">捆绑允许您将单个 JavaScript 和 CSS 文件合并到可以视为单个文件的捆绑包中。</span><span class="sxs-lookup"><span data-stu-id="83b60-293">Bundling lets you combine individual JavaScript and CSS files into a bundle that can be treated like a single file.</span></span> <span data-ttu-id="83b60-294">Min化通过删除空白和其他不需要的字符来压缩 JavaScript 和 CSS 文件。</span><span class="sxs-lookup"><span data-stu-id="83b60-294">Minification condenses JavaScript and CSS files by removing whitespace and other characters that are not required.</span></span> <span data-ttu-id="83b60-295">这些功能与 Web 窗体、ASP.NET MVC 和网页配合使用。</span><span class="sxs-lookup"><span data-stu-id="83b60-295">These features work with Web Forms, ASP.NET MVC, and Web Pages.</span></span>

<span data-ttu-id="83b60-296">捆绑包是使用捆绑类或其子类之一的脚本捆绑包和样式捆绑包创建的。</span><span class="sxs-lookup"><span data-stu-id="83b60-296">Bundles are created using the Bundle class or one of its child classes, ScriptBundle and StyleBundle.</span></span> <span data-ttu-id="83b60-297">配置捆绑包的实例后，只需将其添加到全局捆绑收集实例，即可向传入请求提供该捆绑包。</span><span class="sxs-lookup"><span data-stu-id="83b60-297">After configuring an instance of a bundle, the bundle is made available to incoming requests by simply adding it to a global BundleCollection instance.</span></span> <span data-ttu-id="83b60-298">在默认模板中，捆绑配置在 Bundle Config 文件中执行。</span><span class="sxs-lookup"><span data-stu-id="83b60-298">In the default templates, bundle configuration is performed in a BundleConfig file.</span></span> <span data-ttu-id="83b60-299">此默认配置为模板使用的所有核心脚本和 css 文件创建捆绑包。</span><span class="sxs-lookup"><span data-stu-id="83b60-299">This default configuration creates bundles for all of the core scripts and css files used by the templates.</span></span>

<span data-ttu-id="83b60-300">通过使用几个可能的帮助方法之一，从视图中引用捆绑包。</span><span class="sxs-lookup"><span data-stu-id="83b60-300">Bundles are referenced from within views by using one of a couple possible helper methods.</span></span> <span data-ttu-id="83b60-301">为了支持在调试与发布模式下呈现捆绑包的不同标记，ScriptBundle 和 StyleBundle 类具有帮助器方法 Render。</span><span class="sxs-lookup"><span data-stu-id="83b60-301">In order to support rendering different markup for a bundle when in debug vs. release mode, the ScriptBundle and StyleBundle classes have the helper method, Render.</span></span> <span data-ttu-id="83b60-302">在调试模式下，渲染将为捆绑包中的每个资源生成标记。</span><span class="sxs-lookup"><span data-stu-id="83b60-302">When in debug mode, Render will generate markup for each resource in the bundle.</span></span> <span data-ttu-id="83b60-303">在发布模式下，渲染将为整个捆绑包生成单个标记元素。</span><span class="sxs-lookup"><span data-stu-id="83b60-303">When in release mode, Render will generate a single markup element for the entire bundle.</span></span> <span data-ttu-id="83b60-304">通过修改 Web.config 中编译元素的调试属性，可以在调试和发布模式之间切换，如下所示：</span><span class="sxs-lookup"><span data-stu-id="83b60-304">Toggling between debug and release mode can be accomplished by modifying the debug attribute of the compilation element in web.config as shown below:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample12.xml)]

<span data-ttu-id="83b60-305">此外，可以直接通过 BundleTable 设置启用或禁用优化。</span><span class="sxs-lookup"><span data-stu-id="83b60-305">Additionally, enabling or disabling optimization can be set directly via the BundleTable.EnableOptimizations property.</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample13.cs)]

<span data-ttu-id="83b60-306">当文件捆绑时，它们首先按字母顺序排序（它们在**解决方案资源管理器**中显示的方式）。</span><span class="sxs-lookup"><span data-stu-id="83b60-306">When files are bundled, they are first sorted alphabetically (the way they are displayed in **Solution Explorer**).</span></span> <span data-ttu-id="83b60-307">然后组织它们，以便首先加载已知的库及其自定义扩展（如 jQuery、MooTools 和 Dojo）。</span><span class="sxs-lookup"><span data-stu-id="83b60-307">They are then organized so that known libraries and their custom extensions (such as jQuery, MooTools, and Dojo) are loaded first.</span></span> <span data-ttu-id="83b60-308">例如，如上所述，捆绑脚本文件夹的最终顺序为：</span><span class="sxs-lookup"><span data-stu-id="83b60-308">For example, the final order for the bundling of the Scripts folder as shown above will be:</span></span>

1. <span data-ttu-id="83b60-309">jquery-1.6.2.js</span><span class="sxs-lookup"><span data-stu-id="83b60-309">jquery-1.6.2.js</span></span>
2. <span data-ttu-id="83b60-310">jquery-ui.js</span><span class="sxs-lookup"><span data-stu-id="83b60-310">jquery-ui.js</span></span>
3. <span data-ttu-id="83b60-311">jquery.tools.js</span><span class="sxs-lookup"><span data-stu-id="83b60-311">jquery.tools.js</span></span>
4. <span data-ttu-id="83b60-312">a.js</span><span class="sxs-lookup"><span data-stu-id="83b60-312">a.js</span></span>

<span data-ttu-id="83b60-313">CSS 文件也按字母顺序排序，然后重新组织，以便重置.css 和规范化.css 在任何其他文件之前出现。</span><span class="sxs-lookup"><span data-stu-id="83b60-313">CSS files are also sorted alphabetically and then reorganized so that reset.css and normalize.css come before any other file.</span></span> <span data-ttu-id="83b60-314">上面显示的样式文件夹捆绑的最终排序是：</span><span class="sxs-lookup"><span data-stu-id="83b60-314">The final sorting of the bundling of the Styles folder shown above will be this:</span></span>

1. <span data-ttu-id="83b60-315">重置.css</span><span class="sxs-lookup"><span data-stu-id="83b60-315">reset.css</span></span>
2. <span data-ttu-id="83b60-316">内容.css</span><span class="sxs-lookup"><span data-stu-id="83b60-316">content.css</span></span>
3. <span data-ttu-id="83b60-317">窗体.css</span><span class="sxs-lookup"><span data-stu-id="83b60-317">forms.css</span></span>
4. <span data-ttu-id="83b60-318">globals.css</span><span class="sxs-lookup"><span data-stu-id="83b60-318">globals.css</span></span>
5. <span data-ttu-id="83b60-319">菜单.css</span><span class="sxs-lookup"><span data-stu-id="83b60-319">menu.css</span></span>
6. <span data-ttu-id="83b60-320">样式.css</span><span class="sxs-lookup"><span data-stu-id="83b60-320">styles.css</span></span>

<a id="_Toc_perf"></a>
### <a name="performance-improvements-for-web-hosting"></a><span data-ttu-id="83b60-321">Web 托管的性能改进</span><span class="sxs-lookup"><span data-stu-id="83b60-321">Performance Improvements for Web Hosting</span></span>

<span data-ttu-id="83b60-322">.NET 框架 4.5 和 Windows 8 引入了可帮助您为 Web 服务器工作负载实现显著性能提升的功能。</span><span class="sxs-lookup"><span data-stu-id="83b60-322">The .NET Framework 4.5 and Windows 8 introduce features that can help you achieve a significant performance boost for web-server workloads.</span></span> <span data-ttu-id="83b60-323">这包括减少（高达 35%）在启动时间和使用ASP.NET的网站托管站点的内存占用量中。</span><span class="sxs-lookup"><span data-stu-id="83b60-323">This includes a reduction (up to 35%) in both startup time and in the memory footprint of web hosting sites that use ASP.NET.</span></span>

<a id="_Toc_perf_1"></a>
#### <a name="key-performance-factors"></a><span data-ttu-id="83b60-324">关键性能因素</span><span class="sxs-lookup"><span data-stu-id="83b60-324">Key performance factors</span></span>

<span data-ttu-id="83b60-325">理想情况下，所有网站都应处于活动状态且处于内存中，以确保随时对下一个请求做出快速响应。</span><span class="sxs-lookup"><span data-stu-id="83b60-325">Ideally, all websites should be active and in memory to assure quick response to the next request, whenever it comes.</span></span> <span data-ttu-id="83b60-326">可能影响站点响应能力的因素包括：</span><span class="sxs-lookup"><span data-stu-id="83b60-326">Factors that can affect site responsiveness include:</span></span>

- <span data-ttu-id="83b60-327">应用池回收后站点重新启动所需的时间。</span><span class="sxs-lookup"><span data-stu-id="83b60-327">The time it takes for a site to restart after an app pool recycles.</span></span> <span data-ttu-id="83b60-328">当站点程序集不再在内存中时，此时需要启动站点的 Web 服务器进程。</span><span class="sxs-lookup"><span data-stu-id="83b60-328">This is the time it takes to launch a web server process for the site when the site assemblies are no longer in memory.</span></span> <span data-ttu-id="83b60-329">（平台程序集仍在内存中，因为它们被其他站点使用。这种情况称为"冷站点，暖框架启动"或只是"冷站点启动"。</span><span class="sxs-lookup"><span data-stu-id="83b60-329">(The platform assemblies are still in memory, since they are used by other sites.) This situation is referred to as "cold site, warm framework startup" or just "cold site startup."</span></span>
- <span data-ttu-id="83b60-330">站点占用的内存量。</span><span class="sxs-lookup"><span data-stu-id="83b60-330">How much memory the site occupies.</span></span> <span data-ttu-id="83b60-331">其术语是"每个站点内存消耗"或"非共享工作集"。</span><span class="sxs-lookup"><span data-stu-id="83b60-331">Terms for this are "per-site memory consumption" or "unshared working set."</span></span>

<span data-ttu-id="83b60-332">新的性能改进侧重于这两个因素。</span><span class="sxs-lookup"><span data-stu-id="83b60-332">The new performance improvements focus on both of these factors.</span></span>

<a id="_Toc_perf_2"></a>
#### <a name="requirements-for-new-performance-features"></a><span data-ttu-id="83b60-333">对新性能功能的要求</span><span class="sxs-lookup"><span data-stu-id="83b60-333">Requirements for New Performance Features</span></span>

<span data-ttu-id="83b60-334">新功能的要求可以分为以下几类：</span><span class="sxs-lookup"><span data-stu-id="83b60-334">The requirements for the new features can be broken down into these categories:</span></span>

- <span data-ttu-id="83b60-335">在 .NET 框架 4 上运行的改进。</span><span class="sxs-lookup"><span data-stu-id="83b60-335">Improvements that run on the .NET Framework 4.</span></span>
- <span data-ttu-id="83b60-336">需要 .NET 框架 4.5 但可在任何版本的 Windows 上运行的改进。</span><span class="sxs-lookup"><span data-stu-id="83b60-336">Improvements that require the .NET Framework 4.5 but can run on any version of Windows.</span></span>
- <span data-ttu-id="83b60-337">仅在 Windows 8 上运行 .NET 框架 4.5 时可用的改进。</span><span class="sxs-lookup"><span data-stu-id="83b60-337">Improvements that are available only with .NET Framework 4.5 running on Windows 8.</span></span>

<span data-ttu-id="83b60-338">性能随您能够启用的每个改进级别而提高。</span><span class="sxs-lookup"><span data-stu-id="83b60-338">Performance increases with each level of improvement that you are able to enable.</span></span>

<span data-ttu-id="83b60-339">一些 .NET Framework 4.5 改进还利用了适用于其他方案的更广泛的性能功能。</span><span class="sxs-lookup"><span data-stu-id="83b60-339">Some of the .NET Framework 4.5 improvements take advantage of broader performance features that apply to other scenarios as well.</span></span>

<a id="_Toc_perf_3"></a>
#### <a name="sharing-common-assemblies"></a><span data-ttu-id="83b60-340">共享公共程序集</span><span class="sxs-lookup"><span data-stu-id="83b60-340">Sharing Common Assemblies</span></span>

<span data-ttu-id="83b60-341">**要求**： .NET 框架 4 和可视化工作室 11 开发人员预览 SDK</span><span class="sxs-lookup"><span data-stu-id="83b60-341">**Requirement**: .NET Framework 4 and Visual Studio 11 Developer Preview SDK</span></span>

<span data-ttu-id="83b60-342">服务器上的不同站点通常使用相同的帮助器程序集（例如，来自初学者工具包或示例应用程序的程序集）。</span><span class="sxs-lookup"><span data-stu-id="83b60-342">Different sites on a server often use the same helper assemblies (for example, assemblies from a starter kit or sample application).</span></span> <span data-ttu-id="83b60-343">每个站点在其 Bin 目录中都有自己的程序集副本。</span><span class="sxs-lookup"><span data-stu-id="83b60-343">Each site has its own copy of these assemblies in its Bin directory.</span></span> <span data-ttu-id="83b60-344">即使程序集的对象代码相同，但它们是物理上独立的程序集，因此在冷站点启动期间必须单独读取每个程序集，并单独保存在内存中。</span><span class="sxs-lookup"><span data-stu-id="83b60-344">Even though the object code for the assemblies is identical, they're physically separate assemblies, so each assembly has to be read separately during cold site startup and kept separately in memory.</span></span>

<span data-ttu-id="83b60-345">新的实习功能解决了这种低效率，减少了 RAM 要求和加载时间。</span><span class="sxs-lookup"><span data-stu-id="83b60-345">The new interning functionality solves this inefficiency and reduces both RAM requirements and load time.</span></span> <span data-ttu-id="83b60-346">使用允许 Windows 在文件系统中保留每个程序集的单个副本，站点 Bin 文件夹中的各个程序集将替换为指向单个副本的符号链接。</span><span class="sxs-lookup"><span data-stu-id="83b60-346">Interning lets Windows keep a single copy of each assembly in the file system, and individual assemblies in the site Bin folders are replaced with symbolic links to the single copy.</span></span> <span data-ttu-id="83b60-347">如果单个站点需要程序集的不同版本，则符号链接将被程序集的新版本替换，并且只有该站点受到影响。</span><span class="sxs-lookup"><span data-stu-id="83b60-347">If an individual site needs a distinct version of the assembly, the symbolic link is replaced by the new version of the assembly, and only that site is affected.</span></span>

<span data-ttu-id="83b60-348">使用符号链接共享程序集需要一个名为 aspnet\_intern.exe 的新工具，该工具允许您创建和管理已处理程序集的存储。</span><span class="sxs-lookup"><span data-stu-id="83b60-348">Sharing assemblies using symbolic links requires a new tool named aspnet\_intern.exe, which lets you create and manage the store of interned assemblies.</span></span> <span data-ttu-id="83b60-349">它是作为可视化工作室 11 开发人员预览 SDK 的一部分提供的。</span><span class="sxs-lookup"><span data-stu-id="83b60-349">It is provided as a part of the Visual Studio 11 Developer Preview SDK.</span></span> <span data-ttu-id="83b60-350">（但是，假定已安装最新的[更新](https://support.microsoft.com/kb/2468871)，它将在仅安装 .NET 框架 4 的系统上工作。</span><span class="sxs-lookup"><span data-stu-id="83b60-350">(However, it will work on a system that has only the .NET Framework 4 installed, assuming you have installed the latest [update](https://support.microsoft.com/kb/2468871).)</span></span>

<span data-ttu-id="83b60-351">为了确保所有符合条件的程序集都已暂留，您定期运行 aspnet\_intern.exe（例如，每周一次作为计划任务）。</span><span class="sxs-lookup"><span data-stu-id="83b60-351">To make sure all eligible assemblies have been interned, you run aspnet\_intern.exe periodically (for example, once a week as a scheduled task).</span></span> <span data-ttu-id="83b60-352">典型用途如下：</span><span class="sxs-lookup"><span data-stu-id="83b60-352">A typical use is as follows:</span></span>

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample14.cmd)]

<span data-ttu-id="83b60-353">要查看所有选项，运行没有参数的工具。</span><span class="sxs-lookup"><span data-stu-id="83b60-353">To see all options, run the tool with no arguments.</span></span>

<a id="_Toc_perf_4"></a>
#### <a name="using-multi-core-jit-compilation-for-faster-startup"></a><span data-ttu-id="83b60-354">使用多核 JIT 编译，加快启动速度</span><span class="sxs-lookup"><span data-stu-id="83b60-354">Using multi-Core JIT compilation for faster startup</span></span>

<span data-ttu-id="83b60-355">**要求**： .NET 框架 4.5</span><span class="sxs-lookup"><span data-stu-id="83b60-355">**Requirement**: .NET Framework 4.5</span></span>

<span data-ttu-id="83b60-356">对于冷站点启动，不仅必须从磁盘读取程序集，而且必须编译站点。</span><span class="sxs-lookup"><span data-stu-id="83b60-356">For a cold site startup, not only do assemblies have to be read from disk, but the site must be JIT-compiled.</span></span> <span data-ttu-id="83b60-357">对于复杂的站点，这可能会增加明显的延迟。</span><span class="sxs-lookup"><span data-stu-id="83b60-357">For a complex site, this can add significant delays.</span></span> <span data-ttu-id="83b60-358">.NET Framework 4.5 中的一种新的通用技术通过在可用的处理器内核中扩展 JIT 编译来减少这些延迟。</span><span class="sxs-lookup"><span data-stu-id="83b60-358">A new general-purpose technique in the .NET Framework 4.5 reduces these delays by spreading JIT-compilation across available processor cores.</span></span> <span data-ttu-id="83b60-359">它通过使用在以前发布网站期间收集的信息，尽可能早地这样做。</span><span class="sxs-lookup"><span data-stu-id="83b60-359">It does this as much and as early as possible by using information gathered during previous launches of the site.</span></span> <span data-ttu-id="83b60-360">此功能由[系统.运行时.配置文件优化.启动配置文件](https://msdn.microsoft.com/library/system.runtime.profileoptimization.startprofile(VS.110).aspx)方法实现。</span><span class="sxs-lookup"><span data-stu-id="83b60-360">This functionality implemented by the [System.Runtime.ProfileOptimization.StartProfile](https://msdn.microsoft.com/library/system.runtime.profileoptimization.startprofile(VS.110).aspx) method.</span></span>

<span data-ttu-id="83b60-361">默认情况下，使用多个内核进行 JIT 编译ASP.NET，因此您无需执行任何操作来利用此功能。</span><span class="sxs-lookup"><span data-stu-id="83b60-361">JIT-compiling using multiple cores is enabled by default in ASP.NET, so you do not need to do anything to take advantage of this feature.</span></span> <span data-ttu-id="83b60-362">如果要禁用此功能，请在 Web.config 文件中进行以下设置：</span><span class="sxs-lookup"><span data-stu-id="83b60-362">If you want to disable this feature, make the following setting in the Web.config file:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample15.xml)]

<a id="_Toc_perf_5"></a>
#### <a name="tuning-garbage-collection-to-optimize-for-memory"></a><span data-ttu-id="83b60-363">调整垃圾回收以优化内存</span><span class="sxs-lookup"><span data-stu-id="83b60-363">Tuning garbage collection to optimize for memory</span></span>

<span data-ttu-id="83b60-364">**要求**： .NET 框架 4.5</span><span class="sxs-lookup"><span data-stu-id="83b60-364">**Requirement**: .NET Framework 4.5</span></span>

<span data-ttu-id="83b60-365">站点运行后，其使用垃圾回收器 （GC） 堆可能是其内存消耗的重要因素。</span><span class="sxs-lookup"><span data-stu-id="83b60-365">Once a site is running, its use of the garbage-collector (GC) heap can be a significant factor in its memory consumption.</span></span> <span data-ttu-id="83b60-366">与任何垃圾回收器一样，.NET 框架 GC 在 CPU 时间（集合的频率和重要性）和内存消耗（用于新、释放或自由的对象的额外空间）之间进行权衡。</span><span class="sxs-lookup"><span data-stu-id="83b60-366">Like any garbage collector, the .NET Framework GC makes tradeoffs between CPU time (frequency and significance of collections) and memory consumption (extra space that is used for new, freed, or free-able objects).</span></span> <span data-ttu-id="83b60-367">对于以前的版本，我们提供了有关如何配置 GC 以实现适当平衡的指导（例如，请参阅[ASP.NET 2.0/3.5 共享主机配置](https://www.iis.net/learn/web-hosting/web-server-for-shared-hosting/aspnet-20-35-shared-hosting-configuration)）。</span><span class="sxs-lookup"><span data-stu-id="83b60-367">For previous releases, we have provided guidance on how to configure the GC to achieve the right balance (for example, see [ASP.NET 2.0/3.5 Shared Hosting Configuration](https://www.iis.net/learn/web-hosting/web-server-for-shared-hosting/aspnet-20-35-shared-hosting-configuration)).</span></span>

<span data-ttu-id="83b60-368">对于 .NET Framework 4.5，提供工作负载定义的配置设置，该设置支持以前建议的所有 GC 设置以及为每个站点工作集提供额外性能的新调优。</span><span class="sxs-lookup"><span data-stu-id="83b60-368">For the .NET Framework 4.5, instead of multiple standalone settings, a workload-defined configuration setting is available that enables all of the previously recommended GC settings as well as new tuning that delivers additional performance for the per-site working set.</span></span>

<span data-ttu-id="83b60-369">要启用 GC 内存调优，请向 Windows_Microsoft.NET_Framework_v4.0.30319_aspnet.config 文件添加以下设置：</span><span class="sxs-lookup"><span data-stu-id="83b60-369">To enable GC memory tuning, add the following setting to the Windows\Microsoft.NET\Framework\v4.0.30319\aspnet.config file:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample16.xml)]

<span data-ttu-id="83b60-370">（如果您熟悉之前对 aspnet.config 的更改指南，请注意此设置将替换旧设置，例如，无需设置 gcServer、gc并发等。您不必删除旧设置。</span><span class="sxs-lookup"><span data-stu-id="83b60-370">(If you're familiar with the previous guidance for changes to aspnet.config, note that this setting replaces the old settings — for example, there is no need to set gcServer, gcConcurrent, etc. You do not have to remove the old settings.)</span></span>

<a id="_Toc_perf_6"></a>
#### <a name="prefetching-for-web-applications"></a><span data-ttu-id="83b60-371">为 Web 应用程序预取</span><span class="sxs-lookup"><span data-stu-id="83b60-371">Prefetching for web applications</span></span>

<span data-ttu-id="83b60-372">**要求**： .NET 框架 4.5 在 Windows 8 上运行</span><span class="sxs-lookup"><span data-stu-id="83b60-372">**Requirement**: .NET Framework 4.5 running on Windows 8</span></span>

<span data-ttu-id="83b60-373">对于多个版本，Windows 包含一种称为[预取器](http://en.wikipedia.org/wiki/Prefetcher)的技术，可降低应用程序启动的磁盘读取成本。</span><span class="sxs-lookup"><span data-stu-id="83b60-373">For several releases, Windows has included a technology known as the [prefetcher](http://en.wikipedia.org/wiki/Prefetcher) that reduces the disk-read cost of application startup.</span></span> <span data-ttu-id="83b60-374">由于冷启动主要针对客户端应用程序，因此此技术未包含在 Windows Server 中，该服务器仅包含对服务器至关重要的组件。</span><span class="sxs-lookup"><span data-stu-id="83b60-374">Because cold startup is a problem predominantly for client applications, this technology has not been included in Windows Server, which includes only components that are essential to a server.</span></span> <span data-ttu-id="83b60-375">预取现已在最新版本的 Windows Server 中提供，它可以优化单个网站的启动。</span><span class="sxs-lookup"><span data-stu-id="83b60-375">Prefetching is now available in the latest version of Windows Server, where it can optimize the launch of individual websites.</span></span>

<span data-ttu-id="83b60-376">对于 Windows 服务器，默认情况下未启用预取器。</span><span class="sxs-lookup"><span data-stu-id="83b60-376">For Windows Server, the prefetcher is not enabled by default.</span></span> <span data-ttu-id="83b60-377">要启用和配置高密度 Web 托管的预取器，请在命令行上运行以下命令集：</span><span class="sxs-lookup"><span data-stu-id="83b60-377">To enable and configure the prefetcher for high-density web hosting, run the following set of commands at the command line:</span></span>

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample17.cmd)]

<span data-ttu-id="83b60-378">然后，要将预取器与ASP.NET应用程序集成，请向 Web.config 文件添加以下内容：</span><span class="sxs-lookup"><span data-stu-id="83b60-378">Then, to integrate the prefetcher with ASP.NET applications, add the following to the Web.config file:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample18.xml)]

<a id="_Toc318097385"></a>
## <a name="aspnet-web-forms"></a><span data-ttu-id="83b60-379">ASP.NET Web 窗体</span><span class="sxs-lookup"><span data-stu-id="83b60-379">ASP.NET Web Forms</span></span>

<a id="_Toc318097386"></a>
### <a name="strongly-typed-data-controls"></a><span data-ttu-id="83b60-380">强类型化数据控件</span><span class="sxs-lookup"><span data-stu-id="83b60-380">Strongly Typed Data Controls</span></span>

<span data-ttu-id="83b60-381">在 ASP.NET 4.5 中，Web 窗体包括一些用于处理数据的改进。</span><span class="sxs-lookup"><span data-stu-id="83b60-381">In ASP.NET 4.5, Web Forms includes some improvements for working with data.</span></span> <span data-ttu-id="83b60-382">第一个改进是强类型数据控制。</span><span class="sxs-lookup"><span data-stu-id="83b60-382">The first improvement is strongly typed data controls.</span></span> <span data-ttu-id="83b60-383">对于早期版本的 ASP.NET 中的 Web 窗体控件，使用*Eval*和数据绑定表达式显示数据绑定值：</span><span class="sxs-lookup"><span data-stu-id="83b60-383">For Web Forms controls in previous versions of ASP.NET, you display a data-bound value using *Eval* and a data-binding expression:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample19.aspx)]

<span data-ttu-id="83b60-384">对于双向数据绑定，请使用*绑定*：</span><span class="sxs-lookup"><span data-stu-id="83b60-384">For two-way data binding, you use *Bind*:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample20.aspx)]

<span data-ttu-id="83b60-385">在运行时，这些调用使用反射读取指定成员的值，然后在标记中显示结果。</span><span class="sxs-lookup"><span data-stu-id="83b60-385">At run time, these calls use reflection to read the value of the specified member and then display the result in the markup.</span></span> <span data-ttu-id="83b60-386">此方法使数据与任意、未成形的数据绑定变得容易。</span><span class="sxs-lookup"><span data-stu-id="83b60-386">This approach makes it easy to data bind against arbitrary, unshaped data.</span></span>

<span data-ttu-id="83b60-387">但是，像这样的数据绑定表达式不支持诸如成员名称的 IntelliSense、导航（如转到定义）或对这些名称的编译时间检查等功能。</span><span class="sxs-lookup"><span data-stu-id="83b60-387">However, data-binding expressions like this don't support features like IntelliSense for member names, navigation (like Go To Definition), or compile-time checking for these names.</span></span>

<span data-ttu-id="83b60-388">为了解决此问题，ASP.NET 4.5 添加了声明控件绑定到的数据的数据类型的能力。</span><span class="sxs-lookup"><span data-stu-id="83b60-388">To address this issue, ASP.NET 4.5 adds the ability to declare the data type of the data that a control is bound to.</span></span> <span data-ttu-id="83b60-389">使用新的*ItemType*属性执行此操作。</span><span class="sxs-lookup"><span data-stu-id="83b60-389">You do this using the new *ItemType* property.</span></span> <span data-ttu-id="83b60-390">设置此属性时，数据绑定表达式的作用域中有两个新的类型变量 *：Item*和*BindItem*。</span><span class="sxs-lookup"><span data-stu-id="83b60-390">When you set this property, two new typed variables are available in the scope of data-binding expressions: *Item* and *BindItem*.</span></span> <span data-ttu-id="83b60-391">由于变量是强类型，因此您可以获得 Visual Studio 开发体验的全部优势。</span><span class="sxs-lookup"><span data-stu-id="83b60-391">Because the variables are strongly typed, you get the full benefits of the Visual Studio development experience.</span></span>

<span data-ttu-id="83b60-392">对于双向数据绑定表达式，请使用*BindItem*变量：</span><span class="sxs-lookup"><span data-stu-id="83b60-392">For two-way data-binding expressions, use the *BindItem* variable:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample21.aspx)]

<span data-ttu-id="83b60-393">ASP.NET Web 窗体框架中支持数据绑定的大多数控件都已更新以支持*ItemType*属性。</span><span class="sxs-lookup"><span data-stu-id="83b60-393">Most controls in the ASP.NET Web Forms framework that support data binding have been updated to support the *ItemType* property.</span></span>

<a id="_Toc318097387"></a>
### <a name="model-binding"></a><span data-ttu-id="83b60-394">模型绑定</span><span class="sxs-lookup"><span data-stu-id="83b60-394">Model Binding</span></span>

<span data-ttu-id="83b60-395">模型绑定扩展了ASP.NET Web 窗体控件中的数据绑定，以便使用以代码为中心的数据访问。</span><span class="sxs-lookup"><span data-stu-id="83b60-395">Model binding extends data binding in ASP.NET Web Forms controls to work with code-focused data access.</span></span> <span data-ttu-id="83b60-396">它包含*了 ObjectDataSource*控件和模型绑定中的概念ASP.NET MVC。</span><span class="sxs-lookup"><span data-stu-id="83b60-396">It incorporates concepts from the *ObjectDataSource* control and from model binding in ASP.NET MVC.</span></span>

<a id="_Toc318097388"></a>
#### <a name="selecting-data"></a><span data-ttu-id="83b60-397">选择数据</span><span class="sxs-lookup"><span data-stu-id="83b60-397">Selecting data</span></span>

<span data-ttu-id="83b60-398">要将数据控件配置为使用模型绑定来选择数据，请将控件的*SelectMethod*属性设置为页面代码中的方法的名称。</span><span class="sxs-lookup"><span data-stu-id="83b60-398">To configure a data control to use model binding to select data, you set the control's *SelectMethod* property to the name of a method in the page's code.</span></span> <span data-ttu-id="83b60-399">数据控件在页面生命周期中的适当时间调用该方法，并自动绑定返回的数据。</span><span class="sxs-lookup"><span data-stu-id="83b60-399">The data control calls the method at the appropriate time in the page life cycle and automatically binds the returned data.</span></span> <span data-ttu-id="83b60-400">无需显式调用*DataBind*方法。</span><span class="sxs-lookup"><span data-stu-id="83b60-400">There's no need to explicitly call the *DataBind* method.</span></span>

<span data-ttu-id="83b60-401">在下面的示例中 *，GridView*控件配置为使用名为*GetCategories*的方法 ：</span><span class="sxs-lookup"><span data-stu-id="83b60-401">In the following example, the *GridView* control is configured to use a method named *GetCategories*:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample22.aspx)]

<span data-ttu-id="83b60-402">在页面的代码中创建*GetCategories*方法。</span><span class="sxs-lookup"><span data-stu-id="83b60-402">You create the *GetCategories* method in the page's code.</span></span> <span data-ttu-id="83b60-403">对于简单的选择操作，该方法不需要任何参数，并且应返回*IE50 或* *IQuery 对象*。</span><span class="sxs-lookup"><span data-stu-id="83b60-403">For a simple select operation, the method needs no parameters and should return an *IEnumerable* or *IQueryable* object.</span></span> <span data-ttu-id="83b60-404">如果设置了新的*ItemType*属性（启用强类型数据绑定表达式，如前面在[强类型数据控件](#_Toc318097386)中所述），则应返回这些接口的泛型版本 - *IE5500t&lt;&gt;* 或*IQuery&lt;&gt;T，T\*\*参数匹配* *ItemType*属性的类型（例如 *，IQuery&lt;类别&gt;*）。</span><span class="sxs-lookup"><span data-stu-id="83b60-404">If the new *ItemType* property is set (which enables strongly typed data-binding expressions, as explained under [Strongly Typed Data Controls](#_Toc318097386) earlier), the generic versions of these interfaces should be returned — *IEnumerable&lt;T&gt;* or *IQueryable&lt;T&gt;*, with the *T* parameter matching the type of the *ItemType* property (for example, *IQueryable&lt;Category&gt;*).</span></span>

<span data-ttu-id="83b60-405">下面的示例显示了*GetCategories*方法的代码。</span><span class="sxs-lookup"><span data-stu-id="83b60-405">The following example shows the code for a *GetCategories* method.</span></span> <span data-ttu-id="83b60-406">本示例使用实体框架代码第一模型与北风示例数据库。</span><span class="sxs-lookup"><span data-stu-id="83b60-406">This example uses the Entity Framework Code First model with the Northwind sample database.</span></span> <span data-ttu-id="83b60-407">代码确保查询通过 *"包括"* 方法返回每个类别的相关产品的详细信息。</span><span class="sxs-lookup"><span data-stu-id="83b60-407">The code makes sure that the query returns details of the related products for each category by way of the *Include* method.</span></span> <span data-ttu-id="83b60-408">（这可确保标记中的*模板字段*元素显示每个类别中的产品计数，而无需[n+1 选择](http://stackoverflow.com/questions/97197/what-is-the-n1-selects-problem).）</span><span class="sxs-lookup"><span data-stu-id="83b60-408">(This ensures that the *TemplateField* element in the markup displays the count of products in each category without requiring an [n+1 select](http://stackoverflow.com/questions/97197/what-is-the-n1-selects-problem).)</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample23.cs)]

<span data-ttu-id="83b60-409">当页面运行时 *，GridView*控件会自动调用*GetCategories*方法，并使用配置的字段呈现返回的数据：</span><span class="sxs-lookup"><span data-stu-id="83b60-409">When the page runs, the *GridView* control calls the *GetCategories* method automatically and renders the returned data using the configured fields:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image2.png)

<span data-ttu-id="83b60-410">由于选择方法返回*IQuery 对象*，因此*GridView*控件可以在执行查询之前进一步操作查询。</span><span class="sxs-lookup"><span data-stu-id="83b60-410">Because the select method returns an *IQueryable* object, the *GridView* control can further manipulate the query before executing it.</span></span> <span data-ttu-id="83b60-411">例如 *，GridView*控件可以在执行返回*的 IQuery 对象*之前将用于排序和分页的查询表达式添加到返回的 IQuery 对象，以便这些操作由基础 LINQ 提供程序执行。</span><span class="sxs-lookup"><span data-stu-id="83b60-411">For example, the *GridView* control can add query expressions for sorting and paging to the returned *IQueryable* object before it is executed, so that those operations are performed by the underlying LINQ provider.</span></span> <span data-ttu-id="83b60-412">在这种情况下，实体框架将确保在数据库中执行这些操作。</span><span class="sxs-lookup"><span data-stu-id="83b60-412">In this case, Entity Framework will ensure those operations are performed in the database.</span></span>

<span data-ttu-id="83b60-413">下面的示例显示已修改的*GridView*控件以允许排序和分页：</span><span class="sxs-lookup"><span data-stu-id="83b60-413">The following example shows the *GridView* control modified to allow sorting and paging:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample24.aspx)]

<span data-ttu-id="83b60-414">现在，当页面运行时，控件可以确保只显示当前数据页，并且数据按所选列排序：</span><span class="sxs-lookup"><span data-stu-id="83b60-414">Now when the page runs, the control can make sure that only the current page of data is displayed and that it's ordered by the selected column:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image3.png)

<span data-ttu-id="83b60-415">要筛选返回的数据，必须将参数添加到选择方法。</span><span class="sxs-lookup"><span data-stu-id="83b60-415">To filter the returned data, parameters have to be added to the select method.</span></span> <span data-ttu-id="83b60-416">这些参数将在运行时由模型绑定填充，您可以在返回数据之前使用它们来更改查询。</span><span class="sxs-lookup"><span data-stu-id="83b60-416">These parameters will be populated by the model binding at run time, and you can use them to alter the query before returning the data.</span></span>

<span data-ttu-id="83b60-417">例如，假设您要通过在查询字符串中输入关键字来允许用户筛选产品。</span><span class="sxs-lookup"><span data-stu-id="83b60-417">For example, assume that you want to let users filter products by entering a keyword in the query string.</span></span> <span data-ttu-id="83b60-418">您可以将参数添加到 方法并更新代码以使用参数值：</span><span class="sxs-lookup"><span data-stu-id="83b60-418">You can add a parameter to the method and update the code to use the parameter value:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample25.cs)]

<span data-ttu-id="83b60-419">如果为*关键字*提供了值，然后返回查询结果，则此代码包括*Where*表达式。</span><span class="sxs-lookup"><span data-stu-id="83b60-419">This code includes a *Where* expression if a value is provided for *keyword* and then returns the query results.</span></span>

<a id="_Toc318097389"></a>
#### <a name="value-providers"></a><span data-ttu-id="83b60-420">价值提供者</span><span class="sxs-lookup"><span data-stu-id="83b60-420">Value providers</span></span>

<span data-ttu-id="83b60-421">前面的示例没有具体说明*关键字*参数的值来自何处。</span><span class="sxs-lookup"><span data-stu-id="83b60-421">The previous example was not specific about where the value for the *keyword* parameter was coming from.</span></span> <span data-ttu-id="83b60-422">要指示此信息，可以使用参数属性。</span><span class="sxs-lookup"><span data-stu-id="83b60-422">To indicate this information, you can use a parameter attribute.</span></span> <span data-ttu-id="83b60-423">在此示例中，可以使用*System.Web.Model 绑定*命名空间中的*QueryStringattribute*类：</span><span class="sxs-lookup"><span data-stu-id="83b60-423">For this example, you can use the *QueryStringAttribute* class that's in the *System.Web.ModelBinding* namespace:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample26.cs)]

<span data-ttu-id="83b60-424">这指示模型绑定尝试在运行时将值从查询字符串绑定到*关键字*参数。</span><span class="sxs-lookup"><span data-stu-id="83b60-424">This instructs model binding to try to bind a value from the query string to the *keyword* parameter at run time.</span></span> <span data-ttu-id="83b60-425">（这可能涉及执行类型转换，尽管在这种情况下不执行。如果无法提供值且类型不可为空，则引发异常。</span><span class="sxs-lookup"><span data-stu-id="83b60-425">(This might involve performing type conversion, although it doesn't in this case.) If a value cannot be provided and the type is non-nullable, an exception is thrown.</span></span>

<span data-ttu-id="83b60-426">这些方法的值源称为值提供程序，指示要使用的值提供程序的参数属性称为值提供程序属性。</span><span class="sxs-lookup"><span data-stu-id="83b60-426">The sources of values for these methods are referred to as value providers, and the parameter attributes that indicate which value provider to use are referred to as value provider attributes.</span></span> <span data-ttu-id="83b60-427">Web 窗体将包括 Web 窗体应用程序中所有典型用户输入源的值提供程序和相应属性，例如查询字符串、Cookie、窗体值、控件、视图状态、会话状态和配置文件属性。</span><span class="sxs-lookup"><span data-stu-id="83b60-427">Web Forms will include value providers and corresponding attributes for all of the typical sources of user input in a Web Forms application, such as the query string, cookies, form values, controls, view state, session state, and profile properties.</span></span> <span data-ttu-id="83b60-428">您还可以编写自定义值提供程序。</span><span class="sxs-lookup"><span data-stu-id="83b60-428">You can also write custom value providers.</span></span>

<span data-ttu-id="83b60-429">默认情况下，参数名称用作在值提供程序集合中查找值的键。</span><span class="sxs-lookup"><span data-stu-id="83b60-429">By default, the parameter name is used as the key to find a value in the value provider collection.</span></span> <span data-ttu-id="83b60-430">在此示例中，代码将查找名为关键字的查询字符串值（例如，\*/default.aspx？关键字_chef）。</span><span class="sxs-lookup"><span data-stu-id="83b60-430">In the example, the code will look for a query-string value named keyword (for example, ~/default.aspx?keyword=chef).</span></span> <span data-ttu-id="83b60-431">可以通过将自定义键作为参数传递给参数属性来指定它。</span><span class="sxs-lookup"><span data-stu-id="83b60-431">You can specify a custom key by passing it as an argument to the parameter attribute.</span></span> <span data-ttu-id="83b60-432">例如，要使用名为 q 的查询字符串变量的值，可以执行此操作：</span><span class="sxs-lookup"><span data-stu-id="83b60-432">For example, to use the value of the query-string variable named q, you could do this:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample27.cs)]

<span data-ttu-id="83b60-433">如果此方法位于页面的代码中，用户可以通过使用查询字符串传递关键字来筛选结果：</span><span class="sxs-lookup"><span data-stu-id="83b60-433">If this method is in the page's code, users can filter the results by passing a keyword using the query string:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image4.png)

<span data-ttu-id="83b60-434">模型绑定完成许多任务，否则您必须手动编写代码：读取值、检查空值、尝试将其转换为适当的类型、检查转换是否成功，最后使用查询中的值。</span><span class="sxs-lookup"><span data-stu-id="83b60-434">Model binding accomplishes many tasks that you would otherwise have to code by hand: reading the value, checking for a null value, attempting to convert it to the appropriate type, checking whether the conversion was successful, and finally, using the value in the query.</span></span> <span data-ttu-id="83b60-435">模型绑定导致的代码少得多，并且能够在整个应用程序中重用该功能。</span><span class="sxs-lookup"><span data-stu-id="83b60-435">Model binding results in far less code and in the ability to reuse the functionality throughout your application.</span></span>

<a id="_Toc318097390"></a>
#### <a name="filtering-by-values-from-a-control"></a><span data-ttu-id="83b60-436">按控件的值筛选</span><span class="sxs-lookup"><span data-stu-id="83b60-436">Filtering by values from a control</span></span>

<span data-ttu-id="83b60-437">假设您要扩展示例，以便用户从下拉列表中选择筛选器值。</span><span class="sxs-lookup"><span data-stu-id="83b60-437">Suppose you want to extend the example to let the user choose a filter value from a drop-down list.</span></span> <span data-ttu-id="83b60-438">将以下下拉列表添加到标记中，并将其配置为使用*SelectMethod*属性从其他方法获取其数据：</span><span class="sxs-lookup"><span data-stu-id="83b60-438">Add the following drop-down list to the markup and configure it to get its data from another method using the *SelectMethod* property:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample28.aspx)]

<span data-ttu-id="83b60-439">通常，您还会向*GridView*控件添加*EmptyDataTemplate*元素，以便在找不到匹配的产品时，控件将显示一条消息：</span><span class="sxs-lookup"><span data-stu-id="83b60-439">Typically you would also add an *EmptyDataTemplate* element to the *GridView* control so that the control will display a message if no matching products are found:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample29.aspx)]

<span data-ttu-id="83b60-440">在页面代码中，为下拉列表添加新的 select 方法：</span><span class="sxs-lookup"><span data-stu-id="83b60-440">In the page code, add the new select method for the drop-down list:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample30.cs)]

<span data-ttu-id="83b60-441">最后，更新*GetProducts*选择方法，从下拉列表中获取包含所选类别 ID 的新参数：</span><span class="sxs-lookup"><span data-stu-id="83b60-441">Finally, update the *GetProducts* select method to take a new parameter that contains the ID of the selected category from the drop-down list:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample31.cs)]

<span data-ttu-id="83b60-442">现在，当页面运行时，用户可以从下拉列表中选择一个类别，并且*GridView*控件将自动重新绑定以显示筛选的数据。</span><span class="sxs-lookup"><span data-stu-id="83b60-442">Now when the page runs, users can select a category from the drop-down list, and the *GridView* control is automatically re-bound to show the filtered data.</span></span> <span data-ttu-id="83b60-443">这是可能的，因为模型绑定跟踪选定方法的参数值，并检测任何参数值在回退后是否已更改。</span><span class="sxs-lookup"><span data-stu-id="83b60-443">This is possible because model binding tracks the values of parameters for select methods and detects whether any parameter value has changed after a postback.</span></span> <span data-ttu-id="83b60-444">如果是这样，模型绑定强制关联的数据控件重新绑定到数据。</span><span class="sxs-lookup"><span data-stu-id="83b60-444">If so, model binding forces the associated data control to re-bind to the data.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image5.png)

<a id="_Toc318097391"></a>
### <a name="html-encoded-data-binding-expressions"></a><span data-ttu-id="83b60-445">HTML 编码数据绑定表达式</span><span class="sxs-lookup"><span data-stu-id="83b60-445">HTML Encoded Data-Binding Expressions</span></span>

<span data-ttu-id="83b60-446">现在，您可以对数据绑定表达式的结果进行 HTML 编码。</span><span class="sxs-lookup"><span data-stu-id="83b60-446">You can now HTML-encode the result of data-binding expressions.</span></span> <span data-ttu-id="83b60-447">添加冒号（:)标记数据绑定表达式的&lt;%# 前缀的末尾：</span><span class="sxs-lookup"><span data-stu-id="83b60-447">Add a colon (:) to the end of the &lt;%# prefix that marks the data-binding expression:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample32.aspx)]

<a id="_Toc318097392"></a>
### <a name="unobtrusive-validation"></a><span data-ttu-id="83b60-448">不显眼的验证</span><span class="sxs-lookup"><span data-stu-id="83b60-448">Unobtrusive Validation</span></span>

<span data-ttu-id="83b60-449">现在，您可以将内置验证器控件配置为对客户端验证逻辑使用不显眼的 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="83b60-449">You can now configure the built-in validator controls to use unobtrusive JavaScript for client-side validation logic.</span></span> <span data-ttu-id="83b60-450">这大大减少了页面标记中内联呈现的 JavaScript 量，并减小了整个页面大小。</span><span class="sxs-lookup"><span data-stu-id="83b60-450">This significantly reduces the amount of JavaScript rendered inline in the page markup and reduces the overall page size.</span></span> <span data-ttu-id="83b60-451">您可以通过以下任何方式为验证器控件配置不显眼的 JavaScript：</span><span class="sxs-lookup"><span data-stu-id="83b60-451">You can configure unobtrusive JavaScript for validator controls in any of these ways:</span></span>

- <span data-ttu-id="83b60-452">通过向 Web.config 文件中*&lt;的应用&gt;设置*元素添加以下设置，从而全局：</span><span class="sxs-lookup"><span data-stu-id="83b60-452">Globally by adding the following setting to the *&lt;appSettings&gt;* element in the Web.config file:</span></span> 

    [!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample33.xml)]
- <span data-ttu-id="83b60-453">通过将静态*System.Web.UI.验证设置.无显眼验证模式*属性设置为 *"无显眼验证模式.WebForms"（* 通常在 Global.asax 文件中*的应用程序\_启动*方法中），在全球范围内。</span><span class="sxs-lookup"><span data-stu-id="83b60-453">Globally by setting the static *System.Web.UI.ValidationSettings.UnobtrusiveValidationMode* property to *UnobtrusiveValidationMode.WebForms* (typically in the *Application\_Start* method in the Global.asax file).</span></span>
- <span data-ttu-id="83b60-454">通过将页面类的新 *"不显眼验证模式"* 属性设置为 *"不显眼验证模式.WebForms"，* 单独为*页面*。</span><span class="sxs-lookup"><span data-stu-id="83b60-454">Individually for a page by setting the new *UnobtrusiveValidationMode* property of the *Page* class to *UnobtrusiveValidationMode.WebForms*.</span></span>

<a id="_Toc318097393"></a>
### <a name="html5-updates"></a><span data-ttu-id="83b60-455">HTML5 更新</span><span class="sxs-lookup"><span data-stu-id="83b60-455">HTML5 Updates</span></span>

<span data-ttu-id="83b60-456">为了利用 HTML5 的新功能，对 Web 窗体服务器控件进行了一些改进：</span><span class="sxs-lookup"><span data-stu-id="83b60-456">Some improvements have been made to Web Forms server controls to take advantage of new features of HTML5:</span></span>

- <span data-ttu-id="83b60-457">*TextBox*控件的*TextMode*属性已更新以支持新的 HTML5 输入类型，如*电子邮件*、*日期时间*等。</span><span class="sxs-lookup"><span data-stu-id="83b60-457">The *TextMode* property of the *TextBox* control has been updated to support the new HTML5 input types like *email*, *datetime*, and so on.</span></span>
- <span data-ttu-id="83b60-458">*FileUpload*控件现在支持从支持此 HTML5 功能的浏览器上载多个文件。</span><span class="sxs-lookup"><span data-stu-id="83b60-458">The *FileUpload* control now supports multiple file uploads from browsers that support this HTML5 feature.</span></span>
- <span data-ttu-id="83b60-459">验证器控件现在支持验证 HTML5 输入元素。</span><span class="sxs-lookup"><span data-stu-id="83b60-459">Validator controls now support validating HTML5 input elements.</span></span>
- <span data-ttu-id="83b60-460">具有表示 URL 属性的新 HTML5 元素现在支持 runat_"server"。</span><span class="sxs-lookup"><span data-stu-id="83b60-460">New HTML5 elements that have attributes that represent a URL now support runat="server".</span></span> <span data-ttu-id="83b60-461">因此，您可以在 URL 路径中使用ASP.NET约定，例如 \* 运算符来表示应用程序根（例如，&lt;视频 runat_"服务器"src_"/myVideo.wmv"/&gt;）。</span><span class="sxs-lookup"><span data-stu-id="83b60-461">As a result, you can use ASP.NET conventions in URL paths, like the ~ operator to represent the application root (for example, &lt;video runat="server" src="~/myVideo.wmv" /&gt;).</span></span>
- <span data-ttu-id="83b60-462">*UpdatePanel*控件已修复，以支持过帐 HTML5 输入字段。</span><span class="sxs-lookup"><span data-stu-id="83b60-462">The *UpdatePanel* control has been fixed to support posting HTML5 input fields.</span></span>

<a id="_Toc318097394"></a>
## <a name="aspnet-mvc-4"></a><span data-ttu-id="83b60-463">ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="83b60-463">ASP.NET MVC 4</span></span>

<span data-ttu-id="83b60-464">ASP.NET MVC 4 测试版现在包含在 Visual Studio 11 测试版中。</span><span class="sxs-lookup"><span data-stu-id="83b60-464">ASP.NET MVC 4 Beta is now included with Visual Studio 11 Beta.</span></span> <span data-ttu-id="83b60-465">ASP.NET MVC 是利用模型视图控制器 （MVC） 模式开发高度可测试和可维护的 Web 应用程序的框架。</span><span class="sxs-lookup"><span data-stu-id="83b60-465">ASP.NET MVC is a framework for developing highly testable and maintainable Web applications by leveraging the Model-View-Controller (MVC) pattern.</span></span> <span data-ttu-id="83b60-466">ASP.NET MVC 4 使构建移动 Web 应用程序变得容易，并且包括ASP.NET Web API，这有助于构建可覆盖任何设备的 HTTP 服务。</span><span class="sxs-lookup"><span data-stu-id="83b60-466">ASP.NET MVC 4 makes it easy to build applications for the mobile Web and includes ASP.NET Web API, which helps you build HTTP services that can reach any device.</span></span> <span data-ttu-id="83b60-467">有关详细信息，请参阅 ASP.NET [MVC 4 发行说明](mvc4-release-notes.md)。</span><span class="sxs-lookup"><span data-stu-id="83b60-467">For more information, see the [ASP.NET MVC 4 Release Notes](mvc4-release-notes.md).</span></span>

<a id="_Toc318097395"></a>
## <a name="aspnet-web-pages-2"></a><span data-ttu-id="83b60-468">ASP.NET 网页 2</span><span class="sxs-lookup"><span data-stu-id="83b60-468">ASP.NET Web Pages 2</span></span>

<span data-ttu-id="83b60-469">新功能包括以下内容：</span><span class="sxs-lookup"><span data-stu-id="83b60-469">New features include the following:</span></span>

- <span data-ttu-id="83b60-470">新建和更新的网站模板。</span><span class="sxs-lookup"><span data-stu-id="83b60-470">New and updated site templates.</span></span>
- <span data-ttu-id="83b60-471">使用*验证*帮助程序添加服务器端和客户端验证。</span><span class="sxs-lookup"><span data-stu-id="83b60-471">Adding server-side and client-side validation using the *Validation* helper.</span></span>
- <span data-ttu-id="83b60-472">使用资产管理注册脚本的功能。</span><span class="sxs-lookup"><span data-stu-id="83b60-472">The ability to register scripts using an assets manager.</span></span>
- <span data-ttu-id="83b60-473">使用 OAuth 和 OpenID 启用来自 Facebook 和其他网站的登录。</span><span class="sxs-lookup"><span data-stu-id="83b60-473">Enabling logins from Facebook and other sites using OAuth and OpenID.</span></span>
- <span data-ttu-id="83b60-474">使用地图帮助器添加*地图*。</span><span class="sxs-lookup"><span data-stu-id="83b60-474">Adding maps using the *Maps* helper.</span></span>
- <span data-ttu-id="83b60-475">并排运行网页应用程序。</span><span class="sxs-lookup"><span data-stu-id="83b60-475">Running Web Pages applications side-by-side.</span></span>
- <span data-ttu-id="83b60-476">移动设备的呈现页面。</span><span class="sxs-lookup"><span data-stu-id="83b60-476">Rendering pages for mobile devices.</span></span>

<span data-ttu-id="83b60-477">有关这些功能和整页代码示例的详细信息，请参阅[网页 2 Beta 中的顶部功能](https://go.microsoft.com/fwlink/?LinkID=227824)。</span><span class="sxs-lookup"><span data-stu-id="83b60-477">For more information about these features and full-page code examples, see [The Top Features in Web Pages 2 Beta](https://go.microsoft.com/fwlink/?LinkID=227824).</span></span>

<a id="_Toc318097396"></a>
## <a name="visual-web-developer-11-beta"></a><span data-ttu-id="83b60-478">可视化 Web 开发人员 11 测试版</span><span class="sxs-lookup"><span data-stu-id="83b60-478">Visual Web Developer 11 Beta</span></span>

<span data-ttu-id="83b60-479">本节提供有关可视化 Web 开发人员 11 Beta 和可视化工作室 2012 版本候选版中 Web 开发改进的信息。</span><span class="sxs-lookup"><span data-stu-id="83b60-479">This section provides information about improvements for web development in Visual Web Developer 11 Beta and Visual Studio 2012 Release Candidate.</span></span>

<a id="project-compatibility"></a>
### <a name="project-sharing-between-visual-studio-2010-and-visual-studio-2012-release-candidate-project-compatibility"></a><span data-ttu-id="83b60-480">Visual Studio 2010 和 Visual Studio 2012 版本候选版本之间的项目共享（项目兼容性）</span><span class="sxs-lookup"><span data-stu-id="83b60-480">Project Sharing Between Visual Studio 2010 and Visual Studio 2012 Release Candidate (Project Compatibility)</span></span>

<span data-ttu-id="83b60-481">在 Visual Studio 2012 发布候选版之前，在较新版本的 Visual Studio 中打开现有项目启动了转换向导。</span><span class="sxs-lookup"><span data-stu-id="83b60-481">Until Visual Studio 2012 Release Candidate, opening an existing project in a newer version of Visual Studio launched the Conversion Wizard.</span></span> <span data-ttu-id="83b60-482">这迫使项目的内容（资产）和解决方案升级到不向后兼容的新格式。</span><span class="sxs-lookup"><span data-stu-id="83b60-482">This forced an upgrade of the content (assets) of a project and solution to new formats that were not backward compatible.</span></span> <span data-ttu-id="83b60-483">因此，转换后，您无法在旧版本的 Visual Studio 中打开项目。</span><span class="sxs-lookup"><span data-stu-id="83b60-483">Therefore, after the conversion you could not open the project in the older version of Visual Studio.</span></span>

<span data-ttu-id="83b60-484">许多客户告诉我们，这不是正确的方法。</span><span class="sxs-lookup"><span data-stu-id="83b60-484">Many customers have told us that this was not the right approach.</span></span> <span data-ttu-id="83b60-485">在 Visual Studio 11 Beta 中，我们现在支持与 Visual Studio 2010 SP1 共享项目和解决方案。</span><span class="sxs-lookup"><span data-stu-id="83b60-485">In Visual Studio 11 Beta, we now support sharing projects and solutions with Visual Studio 2010 SP1.</span></span> <span data-ttu-id="83b60-486">这意味着，如果您在 Visual Studio 2012 版本候选版中打开 2010 年项目，您仍然可以在 Visual Studio 2010 SP1 中打开该项目。</span><span class="sxs-lookup"><span data-stu-id="83b60-486">This means that if you open a 2010 project in Visual Studio 2012 Release Candidate, you will still be able to open the project in Visual Studio 2010 SP1.</span></span>

> [!NOTE]
> <span data-ttu-id="83b60-487">几种类型的项目不能在 Visual Studio 2010 SP1 和 Visual Studio 2012 版本候选版之间共享。</span><span class="sxs-lookup"><span data-stu-id="83b60-487">A few types of projects cannot be shared between Visual Studio 2010 SP1 and Visual Studio 2012 Release Candidate.</span></span> <span data-ttu-id="83b60-488">其中包括一些较旧的项目（如ASP.NET MVC 2 项目）或用于特殊目的的项目（如安装程序项目）。</span><span class="sxs-lookup"><span data-stu-id="83b60-488">These include some older projects (such as ASP.NET MVC 2 projects) or projects for special purposes (such as Setup projects).</span></span>

<span data-ttu-id="83b60-489">首次在 Visual Studio 11 Beta 中打开 Visual Studio 2010 SP1 Web 项目时，以下属性将添加到项目文件中：</span><span class="sxs-lookup"><span data-stu-id="83b60-489">When you open a Visual Studio 2010 SP1 Web project for the first time in Visual Studio 11 Beta, the following properties are added to the project file:</span></span>

- <span data-ttu-id="83b60-490">文件升级标志</span><span class="sxs-lookup"><span data-stu-id="83b60-490">FileUpgradeFlags</span></span>
- <span data-ttu-id="83b60-491">升级备份位置</span><span class="sxs-lookup"><span data-stu-id="83b60-491">UpgradeBackupLocation</span></span>
- <span data-ttu-id="83b60-492">旧工具版本</span><span class="sxs-lookup"><span data-stu-id="83b60-492">OldToolsVersion</span></span>
- <span data-ttu-id="83b60-493">VisualStudioVersion</span><span class="sxs-lookup"><span data-stu-id="83b60-493">VisualStudioVersion</span></span>
- <span data-ttu-id="83b60-494">VSToolsPath</span><span class="sxs-lookup"><span data-stu-id="83b60-494">VSToolsPath</span></span>

<span data-ttu-id="83b60-495">文件升级标志、升级备份位置和旧工具版本由升级项目文件的过程使用。</span><span class="sxs-lookup"><span data-stu-id="83b60-495">FileUpgradeFlags, UpgradeBackupLocation, and OldToolsVersion are used by the process that upgrades the project file.</span></span> <span data-ttu-id="83b60-496">它们对在 Visual Studio 2010 中使用该项目没有任何影响。</span><span class="sxs-lookup"><span data-stu-id="83b60-496">They have no impact on working with the project in Visual Studio 2010.</span></span>

<span data-ttu-id="83b60-497">VisualStudioVersion 是 MSBuild 4.5 使用的新属性，用于指示当前项目的 Visual Studio 版本。</span><span class="sxs-lookup"><span data-stu-id="83b60-497">VisualStudioVersion is a new property used by MSBuild 4.5 that indicates the version of Visual Studio for the current project.</span></span> <span data-ttu-id="83b60-498">由于此属性在 MSBuild 4.0 中不存在（Visual Studio 2010 SP1 使用的 MSBuild 版本），因此我们将默认值注入到项目文件中。</span><span class="sxs-lookup"><span data-stu-id="83b60-498">Because this property didn't exist in MSBuild 4.0 (the version of MSBuild that Visual Studio 2010 SP1 uses), we inject a default value into the project file.</span></span>

<span data-ttu-id="83b60-499">VSToolsPath 属性用于确定要从 MSBuild 扩展器Path32 设置表示的路径导入的正确 .target 文件。</span><span class="sxs-lookup"><span data-stu-id="83b60-499">The VSToolsPath property is used to determine the correct .targets file to import from the path represented by the MSBuildExtensionsPath32 setting.</span></span>

<span data-ttu-id="83b60-500">还有一些与导入元素相关的更改。</span><span class="sxs-lookup"><span data-stu-id="83b60-500">There are also some changes related to Import elements.</span></span> <span data-ttu-id="83b60-501">为了支持两个版本的 Visual Studio 之间的兼容性，需要进行这些更改。</span><span class="sxs-lookup"><span data-stu-id="83b60-501">These changes are required in order to support compatibility between both versions of Visual Studio.</span></span>

> [!NOTE]
> <span data-ttu-id="83b60-502">如果 Visual Studio 2010 SP1 和 Visual Studio 11 Beta 在两台不同计算机上共享项目，并且该项目在应用\_数据文件夹中包含本地数据库，则必须确保数据库使用的 SQL Server 版本安装在两台计算机上。</span><span class="sxs-lookup"><span data-stu-id="83b60-502">If a project is being shared between Visual Studio 2010 SP1 and Visual Studio 11 Beta on two different computers, and if the project includes a local database in the App\_Data folder, you must make sure that the version of SQL Server used by the database is installed on both computers.</span></span>

<a id="Configuration_Changes_In_ASPNET45_Website_Templates"></a>
### <a name="configuration-changes-in-aspnet-45-website-templates"></a><span data-ttu-id="83b60-503">ASP.NET 4.5 网站模板中的配置更改</span><span class="sxs-lookup"><span data-stu-id="83b60-503">Configuration Changes in ASP.NET 4.5 Website Templates</span></span>

<span data-ttu-id="83b60-504">对使用 Visual Studio 2012 版本候选版中的网站模板创建的网站的默认*Web.config*文件进行了以下更改：</span><span class="sxs-lookup"><span data-stu-id="83b60-504">The following changes have been made to the default *Web.config* file for site that are created using website templates in Visual Studio 2012 Release Candidate:</span></span>

- <span data-ttu-id="83b60-505">在元素`<httpRuntime>`中，`encoderType`属性现在默认设置为使用添加到ASP.NET的 AntiXSS 类型。</span><span class="sxs-lookup"><span data-stu-id="83b60-505">In the `<httpRuntime>` element, the `encoderType` attribute is now set by default to use the AntiXSS types that were added to ASP.NET.</span></span> <span data-ttu-id="83b60-506">有关详细信息，请参阅[AntiXSS 库](#_Toc318097382)。</span><span class="sxs-lookup"><span data-stu-id="83b60-506">For details, see [AntiXSS Library](#_Toc318097382).</span></span>
- <span data-ttu-id="83b60-507">此外，在`<httpRuntime>`元素中，`requestValidationMode`属性设置为"4.5"。</span><span class="sxs-lookup"><span data-stu-id="83b60-507">Also in the `<httpRuntime>` element, the `requestValidationMode` attribute is set to "4.5".</span></span> <span data-ttu-id="83b60-508">这意味着默认情况下，请求验证配置为使用延迟（"延迟"）验证。</span><span class="sxs-lookup"><span data-stu-id="83b60-508">This means that by default, request validation is configured to use deferred ("lazy") validation.</span></span> <span data-ttu-id="83b60-509">有关详细信息，请参阅[新ASP.NET请求验证功能](#_Toc318097379)。</span><span class="sxs-lookup"><span data-stu-id="83b60-509">For details, see [New ASP.NET Request Validation Features](#_Toc318097379).</span></span>
- <span data-ttu-id="83b60-510">节`<modules>`的元素`<system.webServer>`不包含属性`runAllManagedModulesForAllRequests`。</span><span class="sxs-lookup"><span data-stu-id="83b60-510">The `<modules>` element of the `<system.webServer>` section does not contain a `runAllManagedModulesForAllRequests` attribute.</span></span> <span data-ttu-id="83b60-511">（其默认值为 false。这意味着，如果您使用的 IIS 7 版本尚未更新到 SP1，则新站点中的路由可能有问题。</span><span class="sxs-lookup"><span data-stu-id="83b60-511">(Its default value is false.) This means that if you are using a version of IIS 7 that has not been updated to SP1, you might have issues with routing in a new site.</span></span> <span data-ttu-id="83b60-512">有关详细信息，请参阅[IIS 7 中的本机支持，了解ASP.NET路由](#Native_Support_In_IIS7_For_ASPNET_Routine)。</span><span class="sxs-lookup"><span data-stu-id="83b60-512">For more information, see [Native Support in IIS 7 for ASP.NET Routing](#Native_Support_In_IIS7_For_ASPNET_Routine).</span></span>

<span data-ttu-id="83b60-513">这些更改不会影响现有应用程序。</span><span class="sxs-lookup"><span data-stu-id="83b60-513">These changes do not affect existing applications.</span></span> <span data-ttu-id="83b60-514">但是，它们可能表示现有网站与您使用新模板为 ASP.NET 4.5 创建的新网站的行为差异。</span><span class="sxs-lookup"><span data-stu-id="83b60-514">However, they might represent a difference in behavior between existing websites and new websites that you create for ASP.NET 4.5 using the new templates.</span></span>

<a id="Native_Support_In_IIS7_For_ASPNET_Routine"></a>
### <a name="native-support-in-iis-7-for-aspnet-routing"></a><span data-ttu-id="83b60-515">IIS 7 中用于ASP.NET路由的本机支持</span><span class="sxs-lookup"><span data-stu-id="83b60-515">Native Support in IIS 7 for ASP.NET Routing</span></span>

<span data-ttu-id="83b60-516">这不是对ASP.NET的更改，而是新网站项目的模板更改，如果您正在使用未应用 SP1 更新的 IIS 7 版本，可能会影响您。</span><span class="sxs-lookup"><span data-stu-id="83b60-516">This is not a change to ASP.NET as such, but a change in templates for new website projects that can affect you if you are working a version of IIS 7 that has not had the SP1 update applied.</span></span>

<span data-ttu-id="83b60-517">在ASP.NET中，您可以将以下配置设置添加到应用程序中，以支持路由：</span><span class="sxs-lookup"><span data-stu-id="83b60-517">In ASP.NET, you can add the following configuration setting to applications in order to support routing:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample34.xml?highlight=3)]

<span data-ttu-id="83b60-518">当**RunAll管理ModuleAll请求**为 true 时，`http://mysite/myapp/home`即使 URL 上没有 *.aspx、.mvc*或类似扩展，也可以将类似 URL 转到ASP.NET。 *.mvc*</span><span class="sxs-lookup"><span data-stu-id="83b60-518">When **runAllManagedModulesForAllRequests** is true, a URL like `http://mysite/myapp/home` goes to ASP.NET, even though there is no *.aspx*, *.mvc*, or similar extension on the URL.</span></span>

<span data-ttu-id="83b60-519">对 IIS 7 所做的更新使**runAll管理模块所有请求**设置变得不必要，并支持本机路由ASP.NET路由。</span><span class="sxs-lookup"><span data-stu-id="83b60-519">An update that was made to IIS 7 makes the **runAllManagedModulesForAllRequests** setting unnecessary and supports ASP.NET routing natively.</span></span> <span data-ttu-id="83b60-520">（有关更新的信息，请参阅 Microsoft 支持文章[一个可用更新，使某些 IIS 7.0 或 IIS 7.5 处理程序能够处理 URL 未以句点结尾的请求](https://support.microsoft.com/kb/980368)。</span><span class="sxs-lookup"><span data-stu-id="83b60-520">(For information about the update, see the Microsoft Support article [An update is available that enables certain IIS 7.0 or IIS 7.5 handlers to handle requests whose URLs do not end with a period](https://support.microsoft.com/kb/980368).)</span></span>

<span data-ttu-id="83b60-521">如果您的网站在 IIS 7 上运行，并且 IIS 已更新，则无需将**运行All管理模块全部请求**设置为 true。</span><span class="sxs-lookup"><span data-stu-id="83b60-521">If your website is running on IIS 7 and if IIS has been updated, you do not need to set **runAllManagedModulesForAllRequests** to true.</span></span> <span data-ttu-id="83b60-522">事实上，不建议将其设置为 true，因为它会增加不必要的处理开销。</span><span class="sxs-lookup"><span data-stu-id="83b60-522">In fact, setting it to true is not recommended, because it adds unnecessary processing overhead to request.</span></span> <span data-ttu-id="83b60-523">当此设置为 true 时，所有请求（包括 *.htm、.jpg*和其他静态文件的请求）也会通过请求管道ASP.NET。 *.jpg*</span><span class="sxs-lookup"><span data-stu-id="83b60-523">When this setting is true, all requests, including those for *.htm*, *.jpg*, and other static files, also go through the ASP.NET request pipeline.</span></span>

<span data-ttu-id="83b60-524">如果使用 Visual Studio 2012 RC 中提供的模板创建新ASP.NET 4.5 网站，则网站的配置不包括**RunAll管理模块全部请求**设置。</span><span class="sxs-lookup"><span data-stu-id="83b60-524">If you create a new ASP.NET 4.5 website using the templates that are provided in Visual Studio 2012 RC, the configuration for the website does not include the **runAllManagedModulesForAllRequests** setting.</span></span> <span data-ttu-id="83b60-525">这意味着默认情况下，该设置为 false。</span><span class="sxs-lookup"><span data-stu-id="83b60-525">This means that by default the setting is false.</span></span>

<span data-ttu-id="83b60-526">如果随后在 Windows 7 上运行网站而不安装 SP1，则 IIS 7 将不包含所需的更新。</span><span class="sxs-lookup"><span data-stu-id="83b60-526">If you then run the website on Windows 7 without SP1 installed, IIS 7 will not include the required update.</span></span> <span data-ttu-id="83b60-527">因此，路由将不起作用，您将看到错误。</span><span class="sxs-lookup"><span data-stu-id="83b60-527">As a consequence, routing will not work and you will see errors.</span></span> <span data-ttu-id="83b60-528">如果路由不起作用，可以执行以下任一操作：</span><span class="sxs-lookup"><span data-stu-id="83b60-528">If you have a problem where routing does not work, you can do either the following:</span></span>

- <span data-ttu-id="83b60-529">将 Windows 7 更新为 SP1，这将将更新添加到 IIS 7。</span><span class="sxs-lookup"><span data-stu-id="83b60-529">Update Windows 7 to SP1, which will add the update to IIS 7.</span></span>
- <span data-ttu-id="83b60-530">安装前面列出的 Microsoft 支持文章中所述的更新。</span><span class="sxs-lookup"><span data-stu-id="83b60-530">Install the update that's described in the Microsoft Support article listed previously.</span></span>
- <span data-ttu-id="83b60-531">将**运行All管理模块所有请求**设置为 true，在该网站的 Web.config 文件中。</span><span class="sxs-lookup"><span data-stu-id="83b60-531">Set **runAllManagedModulesForAllRequests** to true in that website's Web.config file.</span></span> <span data-ttu-id="83b60-532">请注意，这将为请求增加一些开销。</span><span class="sxs-lookup"><span data-stu-id="83b60-532">Note that this will add some overhead to requests.</span></span>

<a id="_Toc318097397"></a>
### <a name="html-editor"></a><span data-ttu-id="83b60-533">HTML 编辑器</span><span class="sxs-lookup"><span data-stu-id="83b60-533">HTML Editor</span></span>

<a id="_Toc318097398"></a>
#### <a name="smart-tasks"></a><span data-ttu-id="83b60-534">智能任务</span><span class="sxs-lookup"><span data-stu-id="83b60-534">Smart Tasks</span></span>

<span data-ttu-id="83b60-535">在"设计"视图中，服务器控件的复杂属性通常具有关联的对话框和向导，以便轻松设置它们。</span><span class="sxs-lookup"><span data-stu-id="83b60-535">In Design view, complex properties of server controls often have associated dialog boxes and wizards to make it easy to set them.</span></span> <span data-ttu-id="83b60-536">例如，可以使用特殊的对话框向*中继器*控件添加数据源或向*GridView*控件添加列。</span><span class="sxs-lookup"><span data-stu-id="83b60-536">For example, you can use a special dialog box to add a data source to a *Repeater* control or add columns to a *GridView* control.</span></span>

<span data-ttu-id="83b60-537">但是，针对复杂属性的这种类型的 UI 帮助在源视图中不可用。</span><span class="sxs-lookup"><span data-stu-id="83b60-537">However, this type of UI help for complex properties has not been available in Source view.</span></span> <span data-ttu-id="83b60-538">因此，Visual Studio 11 引入了源视图的智能任务。</span><span class="sxs-lookup"><span data-stu-id="83b60-538">Therefore, Visual Studio 11 introduces Smart Tasks for Source view.</span></span> <span data-ttu-id="83b60-539">智能任务是 C# 和 Visual Basic 编辑器中常用功能的上下文感知快捷方式。</span><span class="sxs-lookup"><span data-stu-id="83b60-539">Smart Tasks are context-aware shortcuts for commonly used features in the C# and Visual Basic editors.</span></span>

<span data-ttu-id="83b60-540">对于ASP.NET Web 窗体控件，当插入点位于元素内部时，智能任务在服务器标记上显示为一个小字形：</span><span class="sxs-lookup"><span data-stu-id="83b60-540">For ASP.NET Web Forms controls, Smart Tasks appear on server tags as a small glyph when the insertion point is inside the element:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image6.png)

<span data-ttu-id="83b60-541">单击字形或按 CTRL+时，智能任务将展开。</span><span class="sxs-lookup"><span data-stu-id="83b60-541">The Smart Task expands when you click the glyph or press CTRL+.</span></span> <span data-ttu-id="83b60-542">（点），就像代码编辑器一样。</span><span class="sxs-lookup"><span data-stu-id="83b60-542">(dot), just as in the code editors.</span></span> <span data-ttu-id="83b60-543">然后，它显示类似于"设计"视图中的智能任务的快捷方式。</span><span class="sxs-lookup"><span data-stu-id="83b60-543">It then displays shortcuts that are similar to the Smart Tasks in Design view.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image7.png)

<span data-ttu-id="83b60-544">例如，上图中的智能任务显示了 GridView 任务选项。</span><span class="sxs-lookup"><span data-stu-id="83b60-544">For example, the Smart Task in the previous illustration shows the GridView Tasks options.</span></span> <span data-ttu-id="83b60-545">如果选择"编辑列"，将显示以下对话框：</span><span class="sxs-lookup"><span data-stu-id="83b60-545">If you choose Edit Columns, the following dialog box is displayed:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image8.png)

<span data-ttu-id="83b60-546">填写对话框将设置可在"设计"视图中设置的相同属性。</span><span class="sxs-lookup"><span data-stu-id="83b60-546">Filling in the dialog box sets the same properties you can set in Design view.</span></span> <span data-ttu-id="83b60-547">单击"确定"时，控件的标记将使用新设置更新：</span><span class="sxs-lookup"><span data-stu-id="83b60-547">When you click OK, the markup for the control is updated with the new settings:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image9.png)

<a id="_Toc318097399"></a>
#### <a name="wai-aria-support"></a><span data-ttu-id="83b60-548">WAI-ARIA 支持</span><span class="sxs-lookup"><span data-stu-id="83b60-548">WAI-ARIA support</span></span>

<span data-ttu-id="83b60-549">编写可访问的网站变得越来越重要。</span><span class="sxs-lookup"><span data-stu-id="83b60-549">Writing accessible websites is becoming increasingly important.</span></span> <span data-ttu-id="83b60-550">[WAI-ARIA 辅助功能标准](http://www.w3.org/WAI/intro/aria)定义了开发人员应如何编写可访问的网站。</span><span class="sxs-lookup"><span data-stu-id="83b60-550">The [WAI-ARIA accessibility standard](http://www.w3.org/WAI/intro/aria) defines how developers should write accessible websites.</span></span> <span data-ttu-id="83b60-551">此标准现在完全支持在视觉工作室。</span><span class="sxs-lookup"><span data-stu-id="83b60-551">This standard is now fully supported in Visual Studio.</span></span>

<span data-ttu-id="83b60-552">例如，*角色*属性现在具有完整的 IntelliSense：</span><span class="sxs-lookup"><span data-stu-id="83b60-552">For example, the *role* attribute now has full IntelliSense:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image10.png)

<span data-ttu-id="83b60-553">WAI-ARIA 标准还引入了以*aria-* 预缀的属性，这些属性允许您向 HTML5 文档添加语义。</span><span class="sxs-lookup"><span data-stu-id="83b60-553">The WAI-ARIA standard also introduces attributes that are prefixed with *aria-* that let you add semantics to an HTML5 document.</span></span> <span data-ttu-id="83b60-554">Visual Studio 还完全支持这些*aria 属性*：</span><span class="sxs-lookup"><span data-stu-id="83b60-554">Visual Studio also fully supports these *aria-* attributes:</span></span>

<span data-ttu-id="83b60-555">![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image11.png) ![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image12.png)</span><span class="sxs-lookup"><span data-stu-id="83b60-555">![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image11.png) ![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image12.png)</span></span>

<a id="_Toc318097400"></a>
#### <a name="new-html5-snippets"></a><span data-ttu-id="83b60-556">新的 HTML5 代码段</span><span class="sxs-lookup"><span data-stu-id="83b60-556">New HTML5 snippets</span></span>

<span data-ttu-id="83b60-557">为了使编写常用的 HTML5 标记更快、更容易，Visual Studio 包含许多代码段。</span><span class="sxs-lookup"><span data-stu-id="83b60-557">To make it faster and easier to write commonly used HTML5 markup, Visual Studio includes a number of snippets.</span></span> <span data-ttu-id="83b60-558">例如视频片段：</span><span class="sxs-lookup"><span data-stu-id="83b60-558">An example is the video snippet:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image13.png)

<span data-ttu-id="83b60-559">要调用代码段，请在 IntelliSense 中选择元素时按 Tab 两次：</span><span class="sxs-lookup"><span data-stu-id="83b60-559">To invoke the snippet, press Tab twice when the element is selected in IntelliSense:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image14.png)

<span data-ttu-id="83b60-560">这将生成可以自定义的代码段。</span><span class="sxs-lookup"><span data-stu-id="83b60-560">This produces a snippet that you can customize.</span></span>

<a id="_Toc318097401"></a>
#### <a name="extract-to-user-control"></a><span data-ttu-id="83b60-561">提取到用户控件</span><span class="sxs-lookup"><span data-stu-id="83b60-561">Extract to user control</span></span>

<span data-ttu-id="83b60-562">在大型网页中，最好将单个片段移动到用户控件中。</span><span class="sxs-lookup"><span data-stu-id="83b60-562">In large web pages, it can be a good idea to move individual pieces into user controls.</span></span> <span data-ttu-id="83b60-563">这种重构形式有助于提高页面的可读性，并可以简化页面结构。</span><span class="sxs-lookup"><span data-stu-id="83b60-563">This form of refactoring can help increase the readability of the page and can simplify the page structure.</span></span>

<span data-ttu-id="83b60-564">为了简化此功能，当您在"源"视图中编辑"Web 窗体"页时，您现在可以选择页面中的文本，右键单击它，然后选择"提取到用户控制"：</span><span class="sxs-lookup"><span data-stu-id="83b60-564">To make this easier, when you edit Web Forms pages in Source view, you can now select text in a page, right-click it, and then choose Extract to User Control:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image2.jpg)

<a id="_Toc318097402"></a>
#### <a name="intellisense-for-code-nuggets-in-attributes"></a><span data-ttu-id="83b60-565">属性中代码块的 IntelliSense</span><span class="sxs-lookup"><span data-stu-id="83b60-565">IntelliSense for code nuggets in attributes</span></span>

<span data-ttu-id="83b60-566">Visual Studio 始终为任何页面或控件中的服务器端代码块提供 IntelliSense。</span><span class="sxs-lookup"><span data-stu-id="83b60-566">Visual Studio has always provided IntelliSense for server-side code nuggets in any page or control.</span></span> <span data-ttu-id="83b60-567">现在，Visual Studio 还包括用于 HTML 属性中的代码块的 IntelliSense。</span><span class="sxs-lookup"><span data-stu-id="83b60-567">Now Visual Studio includes IntelliSense for code nuggets in HTML attributes as well.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image15.png)

<span data-ttu-id="83b60-568">这样可以更轻松地创建数据绑定表达式：</span><span class="sxs-lookup"><span data-stu-id="83b60-568">This makes it easier to create data-binding expressions:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image16.png)

<a id="_Toc318097403"></a>
#### <a name="automatic-renaming-of-matching-tag-when-you-rename-an-opening-or-closing-tag"></a><span data-ttu-id="83b60-569">重命名打开或关闭标记时自动重命名匹配标记</span><span class="sxs-lookup"><span data-stu-id="83b60-569">Automatic renaming of matching tag when you rename an opening or closing tag</span></span>

<span data-ttu-id="83b60-570">如果重命名 HTML 元素（例如，将*div*标记更改为*标头*标记），相应的打开或关闭标记也会实时更改。</span><span class="sxs-lookup"><span data-stu-id="83b60-570">If you rename an HTML element (for example, you change a *div* tag to be a *header* tag), the corresponding opening or closing tag also changes in real time.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image17.png)

<span data-ttu-id="83b60-571">这有助于避免忘记更改结束标记或更改错误标记的错误。</span><span class="sxs-lookup"><span data-stu-id="83b60-571">This helps avoid the error where you forget to change a closing tag or change the wrong one.</span></span>

<a id="_Toc318097404"></a>
#### <a name="event-handler-generation"></a><span data-ttu-id="83b60-572">事件处理程序生成</span><span class="sxs-lookup"><span data-stu-id="83b60-572">Event handler generation</span></span>

<span data-ttu-id="83b60-573">Visual Studio 现在包括在"源"视图中的功能，以帮助您编写事件处理程序并手动绑定它们。</span><span class="sxs-lookup"><span data-stu-id="83b60-573">Visual Studio now includes features in Source view to help you write event handlers and bind them manually.</span></span> <span data-ttu-id="83b60-574">如果要在源视图中编辑事件名称，IntelliSense 将显示&lt;"创建新事件&gt;"，这将在具有正确签名的页面代码中创建事件处理程序：</span><span class="sxs-lookup"><span data-stu-id="83b60-574">If you are editing an event name in Source view, IntelliSense displays &lt;Create New Event&gt;, which will create an event handler in the page's code that has the right signature:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image3.jpg)

<span data-ttu-id="83b60-575">默认情况下，事件处理程序将使用控件的 ID 来表示事件处理方法的名称：</span><span class="sxs-lookup"><span data-stu-id="83b60-575">By default, the event handler will use the control's ID for the name of the event-handling method:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image4.jpg)

<span data-ttu-id="83b60-576">生成的事件处理程序将如下所示（在本例中，在 C#中）：</span><span class="sxs-lookup"><span data-stu-id="83b60-576">The resulting event handler will look like this (in this case, in C#):</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image18.png)

<a id="_Toc318097405"></a>
#### <a name="smart-indent"></a><span data-ttu-id="83b60-577">智能缩进</span><span class="sxs-lookup"><span data-stu-id="83b60-577">Smart indent</span></span>

<span data-ttu-id="83b60-578">当您在空的 HTML 元素内按 Enter 时，编辑器将插入点放在正确的位置：</span><span class="sxs-lookup"><span data-stu-id="83b60-578">When you press Enter while inside an empty HTML element, the editor will put the insertion point in the right place:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image19.png)

<span data-ttu-id="83b60-579">如果在此位置按 Enter，则关闭标记将向下移动并缩进以匹配打开标记。</span><span class="sxs-lookup"><span data-stu-id="83b60-579">If you press Enter in this location, the closing tag is moved down and indented to match the opening tag.</span></span> <span data-ttu-id="83b60-580">插入点也缩进：</span><span class="sxs-lookup"><span data-stu-id="83b60-580">The insertion point is also indented:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image20.png)

<a id="_Toc318097406"></a>
#### <a name="auto-reduce-statement-completion"></a><span data-ttu-id="83b60-581">自动减少语句完成</span><span class="sxs-lookup"><span data-stu-id="83b60-581">Auto-reduce statement completion</span></span>

<span data-ttu-id="83b60-582">Visual Studio 中的 IntelliSense 列表现在根据您键入的内容进行筛选，以便仅显示相关选项：</span><span class="sxs-lookup"><span data-stu-id="83b60-582">The IntelliSense list in Visual Studio now filters based on what you type so that it displays only relevant options:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image21.png)

<span data-ttu-id="83b60-583">IntelliSense 还会根据 IntelliSense 列表中单个单词的标题大小写进行筛选。</span><span class="sxs-lookup"><span data-stu-id="83b60-583">IntelliSense also filters based on the title case of the individual words in the IntelliSense list.</span></span> <span data-ttu-id="83b60-584">例如，如果您键入"dl"，则将显示 dl 和 asp：DataList：</span><span class="sxs-lookup"><span data-stu-id="83b60-584">For example, if you type "dl", both dl and asp:DataList are displayed:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image22.png)

<span data-ttu-id="83b60-585">此功能使获取已知元素的语句完成速度更快。</span><span class="sxs-lookup"><span data-stu-id="83b60-585">This feature makes it faster to get statement completion for known elements.</span></span>

<a id="_Toc318097407"></a>
### <a name="javascript-editor"></a><span data-ttu-id="83b60-586">JavaScript 编辑器</span><span class="sxs-lookup"><span data-stu-id="83b60-586">JavaScript Editor</span></span>

<span data-ttu-id="83b60-587">Visual Studio 2012 版本候选版中的 JavaScript 编辑器是全新的，它极大地改善了在可视化工作室中使用 JavaScript 的体验。</span><span class="sxs-lookup"><span data-stu-id="83b60-587">The JavaScript editor in Visual Studio 2012 Release Candidate is completely new and it greatly improves the experience of working with JavaScript in Visual Studio.</span></span>

<a id="_Toc318097408"></a>
#### <a name="code-outlining"></a><span data-ttu-id="83b60-588">代码大纲显示</span><span class="sxs-lookup"><span data-stu-id="83b60-588">Code outlining</span></span>

<span data-ttu-id="83b60-589">现在会自动为所有函数创建大纲区域，从而可以折叠与当前焦点无关的文件部分。</span><span class="sxs-lookup"><span data-stu-id="83b60-589">Outlining regions are now automatically created for all functions, allowing you to collapse parts of the file that aren't pertinent to your current focus.</span></span>

<a id="_Toc318097409"></a>
#### <a name="brace-matching"></a><span data-ttu-id="83b60-590">大括号匹配</span><span class="sxs-lookup"><span data-stu-id="83b60-590">Brace matching</span></span>

<span data-ttu-id="83b60-591">将插入点放在开括号或关闭大括号上时，编辑器将突出显示匹配的支撑。</span><span class="sxs-lookup"><span data-stu-id="83b60-591">When you put the insertion point on an opening or closing brace, the editor highlights the matching one.</span></span>

<a id="_Toc318097410"></a>
#### <a name="go-to-definition"></a><span data-ttu-id="83b60-592">转到定义</span><span class="sxs-lookup"><span data-stu-id="83b60-592">Go to Definition</span></span>

<span data-ttu-id="83b60-593">"转到定义"命令允许您跳转到函数或变量的源。</span><span class="sxs-lookup"><span data-stu-id="83b60-593">The Go to Definition command lets you jump to the source for a function or variable.</span></span>

<a id="_Toc318097411"></a>
#### <a name="ecmascript5-support"></a><span data-ttu-id="83b60-594">ECMAScript5 支持</span><span class="sxs-lookup"><span data-stu-id="83b60-594">ECMAScript5 support</span></span>

<span data-ttu-id="83b60-595">编辑器支持 ECMAScript5 中的新语法和 API，ECMAScript5 是描述 JavaScript 语言的标准的最新版本。</span><span class="sxs-lookup"><span data-stu-id="83b60-595">The editor supports the new syntax and APIs in ECMAScript5, the latest version of the standard that describes the JavaScript language.</span></span>

<a id="_Toc318097412"></a>
#### <a name="dom-intellisense"></a><span data-ttu-id="83b60-596">DOM 感知</span><span class="sxs-lookup"><span data-stu-id="83b60-596">DOM IntelliSense</span></span>

<span data-ttu-id="83b60-597">DOM API 的智能感知得到了改进，支持许多新的 HTML5 API，包括*查询选择器*、DOM 存储、跨文档消息传递和*画布*。</span><span class="sxs-lookup"><span data-stu-id="83b60-597">IntelliSense for DOM APIs has been improved, with support for many new HTML5 APIs including *querySelector*, DOM Storage, cross-document messaging, and *canvas*.</span></span> <span data-ttu-id="83b60-598">DOM IntelliSense 现在由单个简单的 JavaScript 文件驱动，而不是由本机类型库定义驱动。</span><span class="sxs-lookup"><span data-stu-id="83b60-598">DOM IntelliSense is now driven by a single simple JavaScript file, rather than by a native type library definition.</span></span> <span data-ttu-id="83b60-599">这使得扩展或更换变得容易。</span><span class="sxs-lookup"><span data-stu-id="83b60-599">This makes it easy to extend or replace.</span></span>

<a id="_Toc318097413"></a>
#### <a name="vsdoc-signature-overloads"></a><span data-ttu-id="83b60-600">VSDOC 签名重载</span><span class="sxs-lookup"><span data-stu-id="83b60-600">VSDOC signature overloads</span></span>

<span data-ttu-id="83b60-601">现在可以使用新的*&lt;签名&gt;* 元素声明详细的 IntelliSense 注释，以便单独重载 JavaScript 函数，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="83b60-601">Detailed IntelliSense comments can now be declared for separate overloads of JavaScript functions by using the new *&lt;signature&gt;* element, as shown in this example:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample35.cs)]

<a id="_Toc318097414"></a>
#### <a name="implicit-references"></a><span data-ttu-id="83b60-602">隐式引用</span><span class="sxs-lookup"><span data-stu-id="83b60-602">Implicit references</span></span>

<span data-ttu-id="83b60-603">现在，您可以将 JavaScript 文件添加到一个中心列表中，该列表将隐式包含在任何给定的 JavaScript 文件或阻止引用的文件列表中，这意味着您将获得 IntelliSense 的内容。</span><span class="sxs-lookup"><span data-stu-id="83b60-603">You can now add JavaScript files to a central list that will be implicitly included in the list of files that any given JavaScript file or block references, meaning you'll get IntelliSense for its contents.</span></span> <span data-ttu-id="83b60-604">例如，您可以将 jQuery 文件添加到文件的中心列表中，并且无论是否已显式引用它（使用 // /&lt;引用 /），&gt;您都将在任何 JavaScript 文件块中获取 jQuery 函数的 IntelliSense。</span><span class="sxs-lookup"><span data-stu-id="83b60-604">For example, you can add jQuery files to the central list of files, and you'll get IntelliSense for jQuery functions in any JavaScript block of file, whether you've referenced it explicitly (using /// &lt;reference /&gt;) or not.</span></span>

<a id="_Toc318097415"></a>
### <a name="css-editor"></a><span data-ttu-id="83b60-605">CSS 编辑器</span><span class="sxs-lookup"><span data-stu-id="83b60-605">CSS Editor</span></span>

<a id="_Toc318097416"></a>
#### <a name="auto-reduce-statement-completion"></a><span data-ttu-id="83b60-606">自动减少语句完成</span><span class="sxs-lookup"><span data-stu-id="83b60-606">Auto-reduce statement completion</span></span>

<span data-ttu-id="83b60-607">CSS 的 IntelliSense 列表现在根据所选架构支持的 CSS 属性和值进行筛选。</span><span class="sxs-lookup"><span data-stu-id="83b60-607">The IntelliSense list for CSS now filters based on the CSS properties and values supported by the selected schema.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image23.png)

<span data-ttu-id="83b60-608">IntelliSense 还支持标题案例搜索：</span><span class="sxs-lookup"><span data-stu-id="83b60-608">IntelliSense also supports title case searches:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image24.png)

<a id="_Toc318097417"></a>
#### <a name="hierarchical-indentation"></a><span data-ttu-id="83b60-609">分层缩进</span><span class="sxs-lookup"><span data-stu-id="83b60-609">Hierarchical indentation</span></span>

<span data-ttu-id="83b60-610">CSS 编辑器使用缩进来显示分层规则，这为您提供了级联规则逻辑组织方式的概述。</span><span class="sxs-lookup"><span data-stu-id="83b60-610">The CSS editor uses indentation to display hierarchical rules, which gives you an overview of how the cascading rules are logically organized.</span></span> <span data-ttu-id="83b60-611">在下面的示例中，选择器#list是列表的级联子级，因此缩进。</span><span class="sxs-lookup"><span data-stu-id="83b60-611">In the following example, the #list a selector is a cascading child of list and is therefore indented.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image25.png)

<span data-ttu-id="83b60-612">下面的示例显示了更复杂的继承：</span><span class="sxs-lookup"><span data-stu-id="83b60-612">The following example shows more complex inheritance:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image26.png)

<span data-ttu-id="83b60-613">规则的缩进由其父规则决定。</span><span class="sxs-lookup"><span data-stu-id="83b60-613">The indentation of a rule is determined by its parent rules.</span></span> <span data-ttu-id="83b60-614">默认情况下启用分层缩进，但您可以禁用"选项"对话框（菜单栏中的工具、选项）：</span><span class="sxs-lookup"><span data-stu-id="83b60-614">Hierarchical indentation is enabled by default, but you can disable it the Options dialog box (Tools, Options from the menu bar):</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image27.png)

<a id="_Toc318097418"></a>
#### <a name="css-hacks-support"></a><span data-ttu-id="83b60-615">CSS 黑客支持</span><span class="sxs-lookup"><span data-stu-id="83b60-615">CSS hacks support</span></span>

<span data-ttu-id="83b60-616">对数百个真实 CSS 文件的分析表明，CSS 黑客非常常见，现在 Visual Studio 支持使用最广泛的黑客。</span><span class="sxs-lookup"><span data-stu-id="83b60-616">Analysis of hundreds of real-world CSS files shows that CSS hacks are very common, and now Visual Studio supports the most widely used ones.</span></span> <span data-ttu-id="83b60-617">这种支持包括IntelliSense和验证的明星 （\*） 和下\_划线 （ ） 属性黑客：</span><span class="sxs-lookup"><span data-stu-id="83b60-617">This support includes IntelliSense and validation of the star (\*) and underscore (\_) property hacks:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image28.png)

<span data-ttu-id="83b60-618">还支持典型的选择器黑客，以便即使应用分层缩进，也能保持分层缩进。</span><span class="sxs-lookup"><span data-stu-id="83b60-618">Typical selector hacks are also supported so that hierarchical indentation is maintained even when they are applied.</span></span> <span data-ttu-id="83b60-619">一个典型的选择器黑客用于目标互联网浏览器7是准备一个选择器与*\*：第一个孩子 + html*。</span><span class="sxs-lookup"><span data-stu-id="83b60-619">A typical selector hack used to target Internet Explorer 7 is to prepend a selector with *\*:first-child + html*.</span></span> <span data-ttu-id="83b60-620">使用该规则将保持分层缩进：</span><span class="sxs-lookup"><span data-stu-id="83b60-620">Using that rule will maintain the hierarchical indentation:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image29.png)

<a id="_Toc318097419"></a>
#### <a name="vendor-specific-schemas--moz---webkit"></a><span data-ttu-id="83b60-621">供应商特定的架构（-moz-, -webkit）</span><span class="sxs-lookup"><span data-stu-id="83b60-621">Vendor specific schemas (-moz-, -webkit)</span></span>

<span data-ttu-id="83b60-622">CSS3 引入了许多由不同浏览器在不同时间实现的属性。</span><span class="sxs-lookup"><span data-stu-id="83b60-622">CSS3 introduces many properties that have been implemented by different browsers at different times.</span></span> <span data-ttu-id="83b60-623">这以前迫使开发人员使用特定于供应商的语法为特定浏览器编写代码。</span><span class="sxs-lookup"><span data-stu-id="83b60-623">This previously forced developers to code for specific browsers by using vendor-specific syntax.</span></span> <span data-ttu-id="83b60-624">这些特定于浏览器的属性现在包含在 IntelliSense 中。</span><span class="sxs-lookup"><span data-stu-id="83b60-624">These browser-specific properties are now included in IntelliSense.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image30.png)

<a id="_Toc318097420"></a>
#### <a name="commenting-and-uncommenting-support"></a><span data-ttu-id="83b60-625">评论和非评论支持</span><span class="sxs-lookup"><span data-stu-id="83b60-625">Commenting and uncommenting support</span></span>

<span data-ttu-id="83b60-626">现在，您可以使用代码编辑器中使用的快捷方式（Ctrl_K、C 注释和 Ctrl_K，您取消注释）对 CSS 规则进行注释和取消注释。</span><span class="sxs-lookup"><span data-stu-id="83b60-626">You can now comment and uncomment CSS rules using the same shortcuts that you use in the code editor (Ctrl+K,C to comment and Ctrl+K,U to uncomment).</span></span>

<a id="_Toc318097421"></a>
#### <a name="color-picker"></a><span data-ttu-id="83b60-627">颜色选取器</span><span class="sxs-lookup"><span data-stu-id="83b60-627">Color picker</span></span>

<span data-ttu-id="83b60-628">在早期版本的 Visual Studio 中，与颜色相关的属性的 IntelliSense 由命名颜色值的下拉列表组成。</span><span class="sxs-lookup"><span data-stu-id="83b60-628">In previous versions of Visual Studio, IntelliSense for color-related attributes consisted of a drop-down list of named color values.</span></span> <span data-ttu-id="83b60-629">该列表已被全功能颜色选取器替换。</span><span class="sxs-lookup"><span data-stu-id="83b60-629">That list has been replaced by a full-featured color picker.</span></span>

<span data-ttu-id="83b60-630">输入颜色值时，颜色选取器将自动显示，并显示以前使用的颜色列表，后跟默认调色板。</span><span class="sxs-lookup"><span data-stu-id="83b60-630">When you enter a color value, the color picker is displayed automatically and presents a list of previously used colors followed by a default color palette.</span></span> <span data-ttu-id="83b60-631">您可以使用鼠标或键盘选择颜色。</span><span class="sxs-lookup"><span data-stu-id="83b60-631">You can select a color using the mouse or the keyboard.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image31.png)

<span data-ttu-id="83b60-632">该列表可以展开为完整的颜色选取器。</span><span class="sxs-lookup"><span data-stu-id="83b60-632">The list can be expanded into a complete color picker.</span></span> <span data-ttu-id="83b60-633">选取器允许您在移动不协调性滑块时自动将任何颜色转换为 RGBA 来控制 Alpha 通道：</span><span class="sxs-lookup"><span data-stu-id="83b60-633">The picker lets you control the alpha channel by automatically converting any color into RGBA when you move the opacity slider:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image32.png)

<a id="_Toc318097422"></a>
#### <a name="snippets"></a><span data-ttu-id="83b60-634">代码片段</span><span class="sxs-lookup"><span data-stu-id="83b60-634">Snippets</span></span>

<span data-ttu-id="83b60-635">CSS 编辑器中的代码段使创建跨浏览器样式变得更加简单和快速。</span><span class="sxs-lookup"><span data-stu-id="83b60-635">Snippets in the CSS editor make it easier and faster to create cross-browser styles.</span></span> <span data-ttu-id="83b60-636">许多需要特定于浏览器设置的 CSS3 属性现已滚入代码段。</span><span class="sxs-lookup"><span data-stu-id="83b60-636">Many CSS3 properties that require browser-specific settings have now been rolled into snippets.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image33.png)

<span data-ttu-id="83b60-637">CSS 代码段通过键入在符号 （#） 中显示 IntelliSense 列表来支持高级方案（如 CSS3 媒体查询）。</span><span class="sxs-lookup"><span data-stu-id="83b60-637">CSS snippets support advanced scenarios (like CSS3 media queries) by typing the at-symbol (@), which shows the IntelliSense list.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image34.png)

<span data-ttu-id="83b60-638">当您选择@media值并按选项卡时，CSS 编辑器将插入以下代码段：</span><span class="sxs-lookup"><span data-stu-id="83b60-638">When you select @media value and press Tab, the CSS editor inserts the following snippet:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image5.jpg)

<span data-ttu-id="83b60-639">与代码代码段一样，您可以创建自己的 CSS 代码段。</span><span class="sxs-lookup"><span data-stu-id="83b60-639">As with snippets for code, you can create your own CSS snippets.</span></span>

<a id="_Toc318097423"></a>
#### <a name="custom-regions"></a><span data-ttu-id="83b60-640">自定义区域</span><span class="sxs-lookup"><span data-stu-id="83b60-640">Custom regions</span></span>

<span data-ttu-id="83b60-641">命名代码区域（已在代码编辑器中提供）现在可用于 CSS 编辑。</span><span class="sxs-lookup"><span data-stu-id="83b60-641">Named code regions, which are already available in the code editor, are now available for CSS editing.</span></span> <span data-ttu-id="83b60-642">这使您可以轻松对相关的样式块进行分组。</span><span class="sxs-lookup"><span data-stu-id="83b60-642">This lets you easily group related style blocks.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image35.png)

<span data-ttu-id="83b60-643">当区域折叠时，将显示区域的名称：</span><span class="sxs-lookup"><span data-stu-id="83b60-643">When a region is collapsed it displays the name of the region:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image36.png)

<a id="_Toc318097424"></a>
### <a name="page-inspector"></a><span data-ttu-id="83b60-644">Page Inspector</span><span class="sxs-lookup"><span data-stu-id="83b60-644">Page Inspector</span></span>

<span data-ttu-id="83b60-645">页面检查器是一种工具，用于在 Visual Studio IDE 中呈现网页（HTML、Web 窗体、ASP.NET MVC 或网页），并允许您检查源代码和生成的输出。</span><span class="sxs-lookup"><span data-stu-id="83b60-645">Page Inspector is a tool that renders a web page (HTML, Web Forms, ASP.NET MVC, or Web Pages) in the Visual Studio IDE and lets you examine both the source code and the resulting output.</span></span> <span data-ttu-id="83b60-646">对于ASP.NET页，页面检查器允许您确定哪些服务器端代码已生成呈现到浏览器的 HTML 标记。</span><span class="sxs-lookup"><span data-stu-id="83b60-646">For ASP.NET pages, Page Inspector lets you determine which server-side code has produced the HTML markup that is rendered to the browser.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image37.png)

<span data-ttu-id="83b60-647">有关页面检查器的详细信息，请参阅以下教程：</span><span class="sxs-lookup"><span data-stu-id="83b60-647">For more information about Page Inspector, please see the following tutorials:</span></span>

- <span data-ttu-id="83b60-648">在[mVC 中使用ASP.NET](../mvc/overview/views/using-page-inspector-in-aspnet-mvc.md)页检查器</span><span class="sxs-lookup"><span data-stu-id="83b60-648">Using Page Inspector in [ASP.NET MVC](../mvc/overview/views/using-page-inspector-in-aspnet-mvc.md)</span></span>
- <span data-ttu-id="83b60-649">在[ASP.NET Web 窗体](../web-forms/overview/getting-started/using-page-inspector-in-a-visual-studio-11-beta-web-forms-project.md)中使用页面检查器</span><span class="sxs-lookup"><span data-stu-id="83b60-649">Using Page Inspector in [ASP.NET Web Forms](../web-forms/overview/getting-started/using-page-inspector-in-a-visual-studio-11-beta-web-forms-project.md)</span></span>

<a id="_Toc318097425"></a>
### <a name="publishing"></a><span data-ttu-id="83b60-650">发布</span><span class="sxs-lookup"><span data-stu-id="83b60-650">Publishing</span></span>

<a id="_Toc318097426"></a>
#### <a name="publish-profiles"></a><span data-ttu-id="83b60-651">发布配置文件</span><span class="sxs-lookup"><span data-stu-id="83b60-651">Publish profiles</span></span>

<span data-ttu-id="83b60-652">在 Visual Studio 2010 中，Web 应用程序项目的发布信息不存储在版本控制中，并且不设计为与他人共享。</span><span class="sxs-lookup"><span data-stu-id="83b60-652">In Visual Studio 2010, publishing information for Web application projects is not stored in version control and is not designed for sharing with others.</span></span> <span data-ttu-id="83b60-653">在 Visual Studio 2012 版本候选版中，发布配置文件的格式已更改。</span><span class="sxs-lookup"><span data-stu-id="83b60-653">In Visual Studio 2012 Release Candidate, the format of the publish profile has been changed.</span></span> <span data-ttu-id="83b60-654">它已成为团队工件，现在很容易从基于 MSBuild 的生成中利用。</span><span class="sxs-lookup"><span data-stu-id="83b60-654">It has been made a team artifact, and it is now easy to leverage from builds based on MSBuild.</span></span> <span data-ttu-id="83b60-655">生成配置信息位于"发布"对话框中，以便在发布之前轻松切换生成配置。</span><span class="sxs-lookup"><span data-stu-id="83b60-655">Build configuration information is in the Publish dialog box so that you can easily switch build configurations before publishing.</span></span>

<span data-ttu-id="83b60-656">发布配置文件存储在"发布配置文件"文件夹中。</span><span class="sxs-lookup"><span data-stu-id="83b60-656">Publish profiles are stored in the PublishProfiles folder.</span></span> <span data-ttu-id="83b60-657">文件夹的位置取决于您使用的编程语言：</span><span class="sxs-lookup"><span data-stu-id="83b60-657">The location of the folder depends on what programming language you are using:</span></span>

- <span data-ttu-id="83b60-658">C#：属性\发布配置文件</span><span class="sxs-lookup"><span data-stu-id="83b60-658">C#: Properties\PublishProfiles</span></span>
- <span data-ttu-id="83b60-659">可视化基础知识：我的项目\发布配置文件</span><span class="sxs-lookup"><span data-stu-id="83b60-659">Visual Basic: My Project\PublishProfiles</span></span>

<span data-ttu-id="83b60-660">每个配置文件都是一个 MSBuild 文件。</span><span class="sxs-lookup"><span data-stu-id="83b60-660">Each profile is an MSBuild file.</span></span> <span data-ttu-id="83b60-661">在发布期间，此文件将导入到项目的 MSBuild 文件中。</span><span class="sxs-lookup"><span data-stu-id="83b60-661">During publishing, this file is imported into the project's MSBuild file.</span></span> <span data-ttu-id="83b60-662">在 Visual Studio 2010 中，如果要对发布或包过程进行更改，则必须将自定义项放在名为**ProjectName**.wpp.target 的文件中。</span><span class="sxs-lookup"><span data-stu-id="83b60-662">In Visual Studio 2010, if you want to make changes to the publish or package process, you have to put your customizations in a file named **ProjectName**.wpp.targets.</span></span> <span data-ttu-id="83b60-663">这仍然受支持，但现在可以将自定义项放在发布配置文件本身中。</span><span class="sxs-lookup"><span data-stu-id="83b60-663">This is still supported, but you can now put your customizations in the publish profile itself.</span></span> <span data-ttu-id="83b60-664">这样，自定义将仅用于该配置文件。</span><span class="sxs-lookup"><span data-stu-id="83b60-664">That way, the customizations will be used only for that profile.</span></span>

<span data-ttu-id="83b60-665">您现在还可以利用 MSBuild 的发布配置文件。</span><span class="sxs-lookup"><span data-stu-id="83b60-665">You can now also leverage publish profiles from MSBuild.</span></span> <span data-ttu-id="83b60-666">为此，在生成项目时使用以下命令：</span><span class="sxs-lookup"><span data-stu-id="83b60-666">To do so, use the following command when you build the project:</span></span>

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample36.cmd)]

<span data-ttu-id="83b60-667">project.csproj 值是项目的路径，而配置文件名称是要发布的配置文件的名称。</span><span class="sxs-lookup"><span data-stu-id="83b60-667">The project.csproj value is the path of the project, and ProfileName is the name of the profile to publish.</span></span> <span data-ttu-id="83b60-668">或者，您可以传入发布配置文件的完整路径，而不是传递*PublishProfile*属性的配置文件名称。</span><span class="sxs-lookup"><span data-stu-id="83b60-668">Alternatively, instead of passing the profile name for the *PublishProfile* property, you can pass in the full path to the publish profile.</span></span>

<a id="_Toc318097427"></a>
#### <a name="aspnet-precompilation-and-merge"></a><span data-ttu-id="83b60-669">ASP.NET预编译和合并</span><span class="sxs-lookup"><span data-stu-id="83b60-669">ASP.NET precompilation and merge</span></span>

<span data-ttu-id="83b60-670">对于 Web 应用程序项目，Visual Studio 2012 发布候选版在"包/发布 Web 属性"页上添加了一个选项，允许您在发布或打包项目时预编译和合并网站的内容。</span><span class="sxs-lookup"><span data-stu-id="83b60-670">For Web application projects, Visual Studio 2012 Release Candidate adds an option on the Package/Publish Web properties page that lets you precompile and merge your site's content when you publish or package the project.</span></span> <span data-ttu-id="83b60-671">要查看这些选项，请右键单击解决方案资源管理器中的项目，选择"属性"，然后选择"包/发布 Web 属性页"。</span><span class="sxs-lookup"><span data-stu-id="83b60-671">To see these options, right-click the project in Solution Explorer, choose Properties, and then choose the Package/Publish Web property page.</span></span> <span data-ttu-id="83b60-672">下图显示了发布选项之前预编译此应用程序。</span><span class="sxs-lookup"><span data-stu-id="83b60-672">The following illustration shows the Precompile this application before publishing option.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image6.jpg)

<span data-ttu-id="83b60-673">选择此选项后，每当发布或打包 Web 应用程序时，Visual Studio 都会预编译应用程序。</span><span class="sxs-lookup"><span data-stu-id="83b60-673">When this option is selected, Visual Studio precompiles the application whenever you publish or package the web application.</span></span> <span data-ttu-id="83b60-674">如果要控制站点的预编译方式或程序集的合并方式，请单击"高级"按钮以配置这些选项。</span><span class="sxs-lookup"><span data-stu-id="83b60-674">If you want to control how the site is precompiled or how assemblies are merged, click the Advanced button to configure those options.</span></span>

<a id="_Toc318097428"></a>
### <a name="iis-express"></a><span data-ttu-id="83b60-675">IIS Express</span><span class="sxs-lookup"><span data-stu-id="83b60-675">IIS Express</span></span>

<span data-ttu-id="83b60-676">用于在 Visual Studio 中测试 Web 项目的默认 Web 服务器现在是 IIS Express。</span><span class="sxs-lookup"><span data-stu-id="83b60-676">The default web server for testing web projects in Visual Studio is now IIS Express.</span></span> <span data-ttu-id="83b60-677">可视化工作室开发服务器仍然是开发过程中本地 Web 服务器的选项，但 IIS Express 现在是推荐的服务器。</span><span class="sxs-lookup"><span data-stu-id="83b60-677">The Visual Studio Development Server is still an option for local web server during development, but IIS Express is now the recommended server.</span></span> <span data-ttu-id="83b60-678">在 Visual Studio 11 Beta 中使用 IIS Express 的经验与在 Visual Studio 2010 SP1 中使用它非常相似。</span><span class="sxs-lookup"><span data-stu-id="83b60-678">The experience of using IIS Express in Visual Studio 11 Beta is very similar to using it in Visual Studio 2010 SP1.</span></span>

<a id="_Toc318097429"></a>
## <a name="disclaimer"></a><span data-ttu-id="83b60-679">免责声明</span><span class="sxs-lookup"><span data-stu-id="83b60-679">Disclaimer</span></span>

<span data-ttu-id="83b60-680">这是一份初稿，并可能在本文所述软件最终商业发布之前进行大幅更改。</span><span class="sxs-lookup"><span data-stu-id="83b60-680">This is a preliminary document and may be changed substantially prior to final commercial release of the software described herein.</span></span>

<span data-ttu-id="83b60-681">本文档中包含的信息代表 Microsoft Corporation 在发布之日对所讨论问题的当前观点。</span><span class="sxs-lookup"><span data-stu-id="83b60-681">The information contained in this document represents the current view of Microsoft Corporation on the issues discussed as of the date of publication.</span></span> <span data-ttu-id="83b60-682">由于 Microsoft 必须响应不断变化的市场条件，因此不应将其解释为 Microsoft 作出的承诺，并且 Microsoft 无法保证在发布日期之后提供的任何信息的准确性。</span><span class="sxs-lookup"><span data-stu-id="83b60-682">Because Microsoft must respond to changing market conditions, it should not be interpreted to be a commitment on the part of Microsoft, and Microsoft cannot guarantee the accuracy of any information presented after the date of publication.</span></span>

<span data-ttu-id="83b60-683">本白皮书仅用于提供信息。</span><span class="sxs-lookup"><span data-stu-id="83b60-683">This White Paper is for informational purposes only.</span></span> <span data-ttu-id="83b60-684">MICROSOFT 对本文档中的信息不做任何明示、暗示或法定的担保。</span><span class="sxs-lookup"><span data-stu-id="83b60-684">MICROSOFT MAKES NO WARRANTIES, EXPRESS, IMPLIED OR STATUTORY, AS TO THE INFORMATION IN THIS DOCUMENT.</span></span>

<span data-ttu-id="83b60-685">用户有责任遵守所有适用的版权法/著作权法。</span><span class="sxs-lookup"><span data-stu-id="83b60-685">Complying with all applicable copyright laws is the responsibility of the user.</span></span> <span data-ttu-id="83b60-686">在不限制版权所辖权利的前提下，未经 Microsoft Corporation 的明确书面许可，本文档的任何部分不得被复制、存储或引进检索系统，或者以任何形式、任何方式（电子、机械、影印、录音等）或为任何目的进行传播。</span><span class="sxs-lookup"><span data-stu-id="83b60-686">Without limiting the rights under copyright, no part of this document may be reproduced, stored in or introduced into a retrieval system, or transmitted in any form or by any means (electronic, mechanical, photocopying, recording, or otherwise), or for any purpose, without the express written permission of Microsoft Corporation.</span></span>

<span data-ttu-id="83b60-687">Microsoft 可能拥有本文档所涵盖主题的专利、专利申请、商标、版权或其他知识产权。</span><span class="sxs-lookup"><span data-stu-id="83b60-687">Microsoft may have patents, patent applications, trademarks, copyrights, or other intellectual property rights covering subject matter in this document.</span></span> <span data-ttu-id="83b60-688">除非 Microsoft 提供了明确的书面许可协议，否则提供本文档并不意味着赋予您这些专利、商标、版权或其他知识产权的任何许可。</span><span class="sxs-lookup"><span data-stu-id="83b60-688">Except as expressly provided in any written license agreement from Microsoft, the furnishing of this document does not give you any license to these patents, trademarks, copyrights, or other intellectual property.</span></span>

<span data-ttu-id="83b60-689">除非另有说明，否则此处描述的示例公司、组织、产品、域名、电子邮件地址、徽标、人员、地点和事件均属虚构，且无意或不应推断与任何真实的公司、组织、产品、域名、电子邮件地址、徽标、人员、地点或事件有任何关联。</span><span class="sxs-lookup"><span data-stu-id="83b60-689">Unless otherwise noted, the example companies, organizations, products, domain names, email addresses, logos, people, places and events depicted herein are fictitious, and no association with any real company, organization, product, domain name, email address, logo, person, place or event is intended or should be inferred.</span></span>

<span data-ttu-id="83b60-690">(C) 2012 Microsoft Corporation。</span><span class="sxs-lookup"><span data-stu-id="83b60-690">© 2012 Microsoft Corporation.</span></span> <span data-ttu-id="83b60-691">保留所有权利。</span><span class="sxs-lookup"><span data-stu-id="83b60-691">All rights reserved.</span></span>

<span data-ttu-id="83b60-692">Microsoft 和 Windows 是 Microsoft Corporation 在美国和/或其他国家/地区的注册商标或商标。</span><span class="sxs-lookup"><span data-stu-id="83b60-692">Microsoft and Windows are either registered trademarks or trademarks of Microsoft Corporation in the United States and/or other countries.</span></span>

<span data-ttu-id="83b60-693">此处提到的真实公司和产品的名称可能是其各自所有者的商标。</span><span class="sxs-lookup"><span data-stu-id="83b60-693">The names of actual companies and products mentioned herein may be the trademarks of their respective owners.</span></span>

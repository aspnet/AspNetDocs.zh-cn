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
# <a name="whats-new-in-aspnet-45-and-visual-studio-2012"></a>ASP.NET 4.5 和 Visual Studio 2012 的新增功能

> 本文档介绍了 ASP.NET 4.5 中引入的新功能和增强功能。 还介绍了在 Visual Studio 2012 中对 web 开发所做的改进。 此文档最初发布于2012年2月29日。

- [ASP.NET Core 运行时和框架](#_Toc318097372)

    - [异步读取和写入 HTTP 请求和响应](#_Toc318097373)
    - [对 HttpRequest 处理的改进](#_Toc318097374)
    - [异步刷新响应](#_Toc318097375)
    - [对 *await* 和基于 *任务*的异步模块和处理程序的支持](#_Toc318097376)
    - [异步 HTTP 模块](#_Toc318097377)
    - [异步 HTTP 处理程序](#_Toc318097378)
    - [新 ASP.NET 请求验证功能](#_Toc318097379)
    - [延迟 ( "延迟" ) 请求验证](#_Toc318097380)
    - [支持未经验证请求](#_Toc318097381)
    - [AntiXSS 库](#_Toc318097382)
    - [Websocket 协议支持](#_Toc318097383)
    - [捆绑和缩小](#_Toc318097384)
    - [Web 托管的性能改进](#_Toc_perf)

        - [关键绩效因素](#_Toc_perf_1)
        - [新性能功能的要求](#_Toc_perf_2)
        - [共享公用程序集](#_Toc_perf_3)
        - [使用多核心 JIT 编译加快启动速度](#_Toc_perf_4)
        - [优化垃圾回收以优化内存](#_Toc_perf_5)
        - [对 web 应用程序的预提取](#_Toc_perf_6)
- [ASP.NET Web 窗体](#_Toc318097385)

    - [强类型化数据控件](#_Toc318097386)
    - [模型绑定](#_Toc318097387)

        - [选择数据](#_Toc318097388)
        - [值提供程序](#_Toc318097389)
        - [按控件中的值进行筛选](#_Toc318097390)
    - [HTML 编码 Data-Binding 表达式](#_Toc318097391)
    - [非引人注目验证](#_Toc318097392)
    - [HTML5 更新](#_Toc318097393)
- [ASP.NET MVC 4](#_Toc318097394)
- [ASP.NET 网页 2](#_Toc318097395)
- [Visual Studio 2012 候选发布版本](#_Toc318097396)

    - [Visual Studio 2010 和 Visual Studio 2012 候选发布版本之间的项目共享 (项目兼容性) ](#project-compatibility)
    - [ASP.NET 4.5 网站模板中的配置更改](#Configuration_Changes_In_ASPNET45_Website_Templates)
    - [IIS 7 中用于 ASP.NET 路由的本机支持](#Native_Support_In_IIS7_For_ASPNET_Routine)
    - [HTML 编辑器](#_Toc318097397)

        - [智能任务](#_Toc318097398)
        - [WAI-ARIA 支持](#_Toc318097399)
        - [新 HTML5 代码段](#_Toc318097400)
        - [提取到用户控件](#_Toc318097401)
        - [特性中代码片段的 IntelliSense](#_Toc318097402)
        - [重命名开始或结束标记时自动重命名匹配标记](#_Toc318097403)
        - [生成事件处理程序](#_Toc318097404)
        - [智能缩进](#_Toc318097405)
        - [自动减少语句完成](#_Toc318097406)
    - [JavaScript 编辑器](#_Toc318097407)

        - [代码大纲显示](#_Toc318097408)
        - [大括号匹配](#_Toc318097409)
        - [转到定义](#_Toc318097410)
        - [ECMAScript5 支持](#_Toc318097411)
        - [DOM IntelliSense](#_Toc318097412)
        - [VSDOC 签名重载](#_Toc318097413)
        - [隐式引用](#_Toc318097414)
    - [CSS 编辑器](#_Toc318097415)

        - [自动减少语句完成](#_Toc318097416)
        - [分层缩进。](#_Toc318097417)
        - [CSS 黑客支持](#_Toc318097418)
        - [特定于供应商的架构 (-moz-,-webkit) ](#_Toc318097419)
        - [注释和取消注释支持](#_Toc318097420)
        - [颜色选取器](#_Toc318097421)
        - [片段](#_Toc318097422)
        - [自定义区域](#_Toc318097423)
    - [Page Inspector](#_Toc318097424)
    - [发布](#_Toc318097425)

        - 发布配置文件 
        - [ASP.NET 预编译和合并](#_Toc318097427)
- [IIS Express](#_Toc318097428)
- [免责声明](#_Toc318097429)

<a id="_Toc318097372"></a>
## <a name="aspnet-core-runtime-and-framework"></a>ASP.NET Core 运行时和框架

<a id="_Toc318097373"></a>
### <a name="asynchronously-reading-and-writing-http-requests-and-responses"></a>异步读取和写入 HTTP 请求和响应

ASP.NET 4 引入了使用 *HttpRequest. GetBufferlessInputStream* 方法将 HTTP 请求实体作为流进行读取的功能。 此方法提供对请求实体的流式访问。 但是，它会同步执行，这会在请求的持续时间内将线程关联起来。

ASP.NET 4.5 支持能够以异步方式在 HTTP 请求实体上读取流，并且能够以异步方式刷新。 使用 ASP.NET 4.5，你还可以将 HTTP 请求实体加倍，这使得与下游 HTTP 处理程序（如 .aspx 页面处理程序和 ASP.NET MVC 控制器）的集成更加简单。

<a id="_Toc318097374"></a>
#### <a name="improvements-to-httprequest-handling"></a>对 HttpRequest 处理的改进

ASP.NET 4.5 从 *HttpRequest* 返回的流引用支持同步和异步读取方法。 从*GetBufferlessInputStream*返回的*流*对象现在同时实现 BeginRead 和 EndRead 方法。 使用异步 *流* 方法，你可以在块中异步读取请求实体，而 ASP.NET 将在异步读取循环的每次迭代之间释放当前线程。

ASP.NET 4.5 还添加了一种以缓冲方式读取请求实体的伴随方法： *HttpRequest. GetBufferedInputStream*。 此新重载的工作方式类似于 *GetBufferlessInputStream*，同时支持同步和异步读取。 但在读取时， *GetBufferedInputStream* 还会将实体字节复制到 ASP.NET 内部缓冲区，以便下游模块和处理程序仍可以访问请求实体。 例如，如果管道中的某些上游代码已使用 *GetBufferedInputStream*读取请求实体，则仍可使用 *HttpRequest* 或 *HttpRequest*。 这使你可以对请求执行异步处理 (例如，将大型文件上传到数据库) ，但此后仍运行 .aspx 页面和 MVC ASP.NET 控制器。

<a id="_Toc318097375"></a>
#### <a name="asynchronously-flushing-a-response"></a>异步刷新响应

向 HTTP 客户端发送响应可能需要相当长的时间，因为客户端可能会太远，或者具有低带宽连接。 通常，在应用程序创建响应字节时，ASP.NET 会将其缓冲。 然后，ASP.NET 会在请求处理结束时执行累计缓冲区的单个发送操作。

如果缓冲响应很大 (例如，将大型文件流式传输到客户端) ，则必须定期调用 *httpresponse.cache* ，以将缓冲的输出发送到客户端，并使内存使用保持控制。 不过，由于 *刷新* 是同步调用，因此，在可能长时间运行的请求的持续时间内，反复调用 *刷新* 仍会消耗线程。

ASP.NET 4.5 添加了对使用*httpresponse.cache*类的*BeginFlush*和*EndFlush*方法异步执行刷新的支持。 使用这些方法，你可以创建异步模块和异步处理程序，以将数据增量发送到客户端，而无需占用操作系统线程。 在 *BeginFlush* 和 *EndFlush* 调用之间，ASP.NET 释放当前线程。 这大大减少了支持长时间运行的 HTTP 下载所需的活动线程的总数。

<a id="_Toc318097376"></a>
### <a name="support-for-await-and-task---based-asynchronous-modules-and-handlers"></a>对 *await* 和基于 *任务* 的异步模块和处理程序的支持

.NET Framework 4 引入了一个称为 *任务*的异步编程概念。 任务由*tasks 命名空间中的**任务*类型和相关类型来表示。 .NET Framework 4.5 通过编译器增强功能生成，使 *任务* 对象的使用更加简单。 在 .NET Framework 4.5 中，编译器支持两个新的关键字： *await* 和 *async*。 *Await*关键字是语法简写，指示代码段应以异步方式等待某个代码的其他部分。 *Async*关键字表示一个提示，可用于将方法标记为基于任务的异步方法。

*Await*、 *async*和*Task*对象的组合使你可以更轻松地在 .net 4.5 中编写异步代码。 ASP.NET 4.5 通过新的 Api 支持这些简化，使你能够使用新的编译器增强功能编写异步 HTTP 模块和异步 HTTP 处理程序。

<a id="_Toc318097377"></a>
#### <a name="asynchronous-http-modules"></a>异步 HTTP 模块

假设要在返回 *Task* 对象的方法中执行异步工作。 下面的代码示例定义了一个异步方法，该方法可执行异步调用以下载 Microsoft 主页。 请注意，在方法签名中使用 *async* 关键字，并在 *等待* 调用 *DownloadStringTaskAsync*。

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample1.cs)]

这就是您必须编写的所有内容，.NET Framework 将在等待下载完成时自动处理展开调用堆栈，并在下载完成后自动还原调用堆栈。

现在假设要在异步 ASP.NET HTTP 模块中使用此异步方法。 ASP.NET 4.5 包含一个帮助器方法 (*EventHandlerTaskAsyncHelper*) 和一个新的委托类型 (*TaskEventHandler*) ，可用于将基于任务的异步方法与 ASP.NET HTTP 管道公开的旧异步编程模型集成。 此示例演示如何执行以下操作：

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample2.cs)]

<a id="_Toc318097378"></a>
#### <a name="asynchronous-http-handlers"></a>异步 HTTP 处理程序

在 ASP.NET 中编写异步处理程序的传统方法是实现 *IHttpAsyncHandler* 接口。 ASP.NET 4.5 引入了可从派生的 *HttpTaskAsyncHandler* 异步基类型，这使得编写异步处理程序变得更加容易。

*HttpTaskAsyncHandler*类型是抽象的，需要重写*ProcessRequestAsync*方法。 内部 ASP.NET 负责将 (*Task* 对象) *ProcessRequestAsync* 的返回签名与 ASP.NET 管道使用的旧异步编程模型相集成。

下面的示例演示如何使用 *Task* 和 *AWAIT* 作为异步 HTTP 处理程序实现的一部分：

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample3.cs)]

<a id="_Toc318097379"></a>
### <a name="new-aspnet-request-validation-features"></a>新 ASP.NET 请求验证功能

默认情况下，ASP.NET 执行请求验证，即检查请求以查找字段、标头、cookie 等中的标记或脚本。 如果检测到任何，ASP.NET 将引发异常。 这作为防御潜在跨站点脚本攻击的第一道防线。

ASP.NET 4.5 使你可以轻松地选择读取未经验证请求数据。 ASP.NET 4.5 还集成了常用的 AntiXSS 库，这是以前的外部库。

开发人员经常需要为其应用程序选择关闭请求验证的能力。 例如，如果你的应用程序是论坛软件，则你可能希望允许用户提交 HTML 格式的论坛帖子和评论，但仍要确保请求验证检查其他所有内容。

ASP.NET 4.5 引入了两个功能，使你可以轻松地使用未经验证输入：延迟 ( "延迟" ) 请求验证和访问未经验证请求数据。

<a id="_Toc318097380"></a>
#### <a name="deferred-lazy-request-validation"></a>延迟 ( "延迟" ) 请求验证

在 ASP.NET 4.5 中，默认情况下，所有请求数据都服从请求验证。 但是，你可以将应用程序配置为延迟请求验证，直到实际访问请求数据为止。  (这有时被称为延迟请求验证，这是基于某些数据方案的延迟加载等术语。 ) 可以通过将*httpRUntime*元素中的*requestValidationMode*属性设置为4.5，将应用程序配置为在 Web.config 文件中使用延迟的验证，如以下示例中所示：

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample4.xml)]

当请求验证模式设置为4.5 时，仅当代码访问该值时才会触发请求验证。 例如，如果你的代码获取 "请求" 的值。表单 ["论坛 \_ 帖子"]，只为窗体集合中的该元素调用请求验证。 未验证 *窗体* 集合中的其他元素。 在以前版本的 ASP.NET 中，当访问集合中的任何元素时，将触发整个请求集合的请求验证。 新行为使不同的应用程序组件可以更轻松地查看不同的请求数据块，而不会在其他部分触发请求验证。

<a id="_Toc318097381"></a>
#### <a name="support-for-unvalidated-requests"></a>支持未经验证请求

仅限延迟的请求验证不能解决有选择性地绕过请求验证的问题。 对请求的调用。窗体 ["论坛 \_ 帖子"] 仍将触发对该特定请求值的请求验证。 但是，你可能想要访问此字段而不触发验证，因为你希望在该字段中允许标记。

为此，ASP.NET 4.5 现在支持对请求数据进行未经验证访问。 ASP.NET 4.5 在*HttpRequest*类中包含新的*未经验证*集合属性。 此集合提供对请求数据的所有公共值的访问，如 *窗体*、 *查询字符串*、 *cookie*和 *Url*。

使用论坛示例，若要读取未经验证请求数据，首先需要将应用程序配置为使用新的请求验证模式：

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample5.xml)]

然后，可以使用未经验证属性来读取未经验证窗体值 *HttpRequest* ：

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample6.cs)]

> [!WARNING]
> 安全性- *使用未经验证请求数据！* ASP.NET 4.5 添加了未经验证请求属性和集合，使你能够更轻松地访问非常特定的未经验证请求数据。 但是，仍必须对原始请求数据执行自定义验证，以确保不会向用户呈现危险文本。

<a id="_Toc318097382"></a>
### <a name="antixss-library"></a>AntiXSS 库

由于 Microsoft AntiXSS 库的普及，ASP.NET 4.5 现在合并了该库版本4.0 中的核心编码例程。

编码例程由 *AntiXssEncoder* 类型在新的 *AntiXss* 命名空间中实现。 可以通过调用在类型中实现的任何静态编码方法，直接使用 *AntiXssEncoder* 类型。 然而，最简单的方法是使用新的防 XSS 例程，将 ASP.NET 应用程序配置为在默认情况下使用 *AntiXssEncoder* 类。 为此，请将以下属性添加到 Web.config 文件：

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample7.xml)]

当 *encoderType* 属性设置为使用 *AntiXssEncoder* 类型时，ASP.NET 中的所有输出编码会自动使用新的编码例程。

以下是外部 AntiXSS 库中已合并到 ASP.NET 4.5 的部分：

- *Server.htmlencode*、 *HtmlFormUrlEncode*和 *HtmlAttributeEncode*
- *XmlAttributeEncode* 和 *XmlEncode*
- *UrlEncode* 和 *UrlPathEncode* (new) 
- *CssEncode*

<a id="_Toc318097383"></a>
### <a name="support-for-websockets-protocol"></a>Websocket 协议支持

Websocket 协议是一种基于标准的网络协议，用于定义如何通过 HTTP 建立客户端与服务器之间的安全实时双向通信。 Microsoft 同时结合了 IETF 和 W3C 标准，有助于定义协议。 不只是浏览器) 的任何客户 (端都支持 Websocket 协议，Microsoft 在客户端和移动操作系统上对支持 Websocket 协议的大量资源进行投资。

Websocket 协议使在客户端和服务器之间创建长时间运行的数据传输变得更加容易。 例如，编写聊天应用程序要容易得多，因为你可以在客户端与服务器之间建立真正长时间运行的连接。 不必使用定期轮询或 HTTP 长轮询等解决方法来模拟套接字的行为。

ASP.NET 4.5 和 IIS 8 包含低级别 Websocket 支持，使 ASP.NET 开发人员可以使用托管 Api 在 Websocket 对象上异步读取和写入字符串和二进制数据。 对于 ASP.NET 4.5，有 *一个新的* system.servicemodel 命名空间，其中包含用于 websocket 协议的类型。

浏览器客户端通过创建指向 ASP.NET 应用程序中的 URL 的 DOM *WebSocket* 对象建立 websocket 连接，如以下示例中所示：

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample8.cs)]

可以使用任何类型的模块或处理程序在 ASP.NET 中创建 Websocket 终结点。 在上面的示例中，使用了一个 foo.ashx 文件，因为 foo.ashx 文件是创建处理程序的快速方法。

根据 Websocket 协议，ASP.NET 应用程序可通过指明请求应从 HTTP GET 请求升级到 Websocket 请求来接受客户端的 Websocket 请求。 下面的示例说明：

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample9.cs)]

*AcceptWebSocketRequest*方法接受函数委托，因为 ASP.NET 将展开当前 HTTP 请求，然后将控制转移到函数委托。 从概念上讲，这种方法类似于你使用的方法，在此方法中， *你将在*其中定义执行后台工作的线程启动委托。

在 ASP.NET 和客户端成功完成 Websocket 握手后，ASP.NET 将调用你的委托，并且 Websocket 应用程序开始运行。 下面的代码示例演示了一个简单的回显应用程序，它使用 ASP.NET 中的内置 Websocket 支持：

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample10.cs)]

对于 *await* 关键字和基于任务的异步操作，.net 4.5 中的支持是编写 websocket 应用程序的自然。 此代码示例显示 Websocket 请求在 ASP.NET 内完全以异步方式运行。 应用程序通过调用 await 套接字异步等待客户端发送消息 *。ReceiveAsync*。 同样，可以通过调用 await socket 将异步消息发送到客户端 *。SendAsync*。

在浏览器中，应用程序通过 *onmessage* 函数接收 websocket 消息。 若要从浏览器发送消息，请调用*WebSocket* DOM 类型的*send*方法，如以下示例中所示：

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample11.cs)]

将来，我们可能会发布对此功能的更新，这些更新将抽象掉此版本中的 Websocket 应用程序所需的一些低级别编码。

<a id="_Toc318097384"></a>
### <a name="bundling-and-minification"></a>捆绑和缩小

绑定使你可以将单个 JavaScript 和 CSS 文件合并成一个可以视为单个文件的捆绑包。 缩减通过删除不需要的空格和其他字符来会将 JavaScript 和 CSS 文件。 这些功能适用于 Web 窗体、ASP.NET MVC 和网页。

使用捆绑类或其子类之一（ScriptBundle 和 StyleBundle）创建捆绑包。 在配置捆绑的实例后，只需将该绑定添加到全局 BundleCollection 实例，即可将其提供给传入的请求。 在默认模板中，捆绑配置是在 BundleConfig 文件中执行的。 此默认配置将为模板使用的所有核心脚本和 css 文件创建捆绑包。

使用几种可能的帮助程序方法之一在视图中引用绑定。 为了支持在调试和发布模式下为捆绑包呈现不同的标记，ScriptBundle 和 StyleBundle 类具有 helper 方法，即 Render。 处于调试模式时，Render 将为捆绑包中的每个资源生成标记。 在发布模式下，Render 将为整个绑定生成一个标记元素。 可以通过在 web.config 中修改编译元素的 debug 特性来完成调试和发布模式间的切换，如下所示：

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample12.xml)]

此外，还可以通过 Bundletable.enableoptimization. EnableOptimizations 属性直接设置启用或禁用优化。

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample13.cs)]

当捆绑文件时，将首先按字母顺序对文件进行排序， (它们在 **解决方案资源管理器**) 中的显示方式。 然后对它们进行组织，以便先加载 (的已知库及其自定义扩展插件，例如 jQuery、MooTools 和 Dojo) 。 例如，如上所示的 "脚本" 文件夹的绑定最终顺序如下：

1. jquery-1.6.2.js
2. jquery-ui.js
3. jquery.tools.js
4. a.js

CSS 文件也按字母顺序进行排序，然后再进行重新组织，以便在任何其他文件之前进行重置。 上面所示的样式文件夹的绑定的最终排序如下：

1. 重置 .css
2. 内容 .css
3. forms .css
4. globals
5. menu .css
6. 样式 .css

<a id="_Toc_perf"></a>
### <a name="performance-improvements-for-web-hosting"></a>Web 托管的性能改进

.NET Framework 4.5 和 Windows 8 中引入了一些功能，可帮助你为 web 服务器工作负荷实现显著的性能提升。 这包括在启动时间和使用 ASP.NET 的 web 托管站点的内存占用量中，最多可降低 35% ) 的 (。

<a id="_Toc_perf_1"></a>
#### <a name="key-performance-factors"></a>关键绩效因素

理想情况下，所有网站都应该处于活动状态，并且在内存中，以便在每次请求时都能快速响应下一个请求。 影响站点响应能力的因素包括：

- 在应用程序池回收后重新启动站点所用的时间。 这是在站点程序集不再处于内存中时，为站点启动 web 服务器进程所用的时间。  (平台程序集仍在内存中，因为它们被其他站点使用。 ) 这种情况称为 "冷站点、热框架启动" 或简称为 "冷站点启动"。
- 站点占用的内存量。 这是 "每个站点的内存占用量" 或 "非共享工作集"。

新性能改进重点介绍了这两个因素。

<a id="_Toc_perf_2"></a>
#### <a name="requirements-for-new-performance-features"></a>新性能功能的要求

新功能的要求可划分为以下类别：

- .NET Framework 4 上运行的改进。
- 需要 .NET Framework 4.5 的改进，但可以在任何 Windows 版本上运行。
- 仅适用于在 Windows 8 上运行的 .NET Framework 4.5 的改进。

性能会随你能够启用的每个改进级别而增加。

.NET Framework 的部分4.5 改进利用适用于其他方案的更广泛的性能功能。

<a id="_Toc_perf_3"></a>
#### <a name="sharing-common-assemblies"></a>共享公用程序集

**要求**： .NET Framework 4 和 Visual Studio 11 开发人员预览版 SDK

服务器上的不同站点通常使用相同的帮助程序集 (例如，初学者工具包或示例应用程序) 中的程序集。 每个站点在其 Bin 目录中都有其自己的这些程序集副本。 即使程序集的对象代码是相同的，它们也是物理上独立的程序集，因此，每个程序集都必须在冷站点启动期间单独读取，并在内存中单独保存。

新的暂存功能可解决这一低效，同时降低 RAM 要求和加载时间。 通过使用留用功能，Windows 可以在文件系统中保留每个程序集的单个副本，并将网站 Bin 文件夹中的各个程序集替换为指向单个副本的符号链接。 如果单个站点需要不同版本的程序集，则符号链接将替换为该程序集的新版本，并且仅影响该站点。

使用符号链接共享程序集需要一个名为 aspnetintern.exe 的新工具 \_ ，它使您可以创建和管理暂存的程序集的存储区。 它作为 Visual Studio 11 开发人员预览版 SDK 的一部分提供。 但 (，它将在仅安装了 .NET Framework 4 的系统上运行，前提是已安装了最新的 [更新](https://support.microsoft.com/kb/2468871)。 ) 

为了确保所有符合条件的程序集都已留用，你可以定期运行 aspnet \_intern.exe (例如，一周作为计划的任务) 。 典型用法如下所示：

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample14.cmd)]

若要查看所有选项，请不带参数运行该工具。

<a id="_Toc_perf_4"></a>
#### <a name="using-multi-core-jit-compilation-for-faster-startup"></a>使用多核心 JIT 编译加快启动速度

**要求**： .NET Framework 4。5

对于冷站点启动，不仅必须从磁盘读取程序集，而且必须对站点进行 JIT 编译。 对于复杂站点，这可能会增加很多延迟。 .NET Framework 4.5 中的一种新的通用技术可通过跨可用处理器核心传播 JIT 编译来减少这些延迟。 它通过使用在上一次启动站点时收集的信息，尽快实现此功能。 此功能由 [ProfileOptimization. StartProfile](https://msdn.microsoft.com/library/system.runtime.profileoptimization.startprofile(VS.110).aspx) 方法实现。

默认情况下，在 ASP.NET 中启用了使用多个核心的 JIT 编译，因此您无需执行任何操作即可利用此功能。 如果要禁用此功能，请在 Web.config 文件中设置以下设置：

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample15.xml)]

<a id="_Toc_perf_5"></a>
#### <a name="tuning-garbage-collection-to-optimize-for-memory"></a>优化垃圾回收以优化内存

**要求**： .NET Framework 4。5

站点运行后，使用垃圾回收器 (GC) 堆会成为其内存消耗的重要因素。 与任何垃圾回收器一样，.NET Framework GC 在 CPU 时间 (频率和集合的重要性之间进行权衡) 和内存占用 (额外空间，) 使用新的、释放或自由的对象。 对于以前的版本，我们提供了有关如何配置 GC 以实现适当平衡 (例如，请参阅 [ASP.NET 2.0/3.5 共享的托管配置](https://www.iis.net/learn/web-hosting/web-server-for-shared-hosting/aspnet-20-35-shared-hosting-configuration)) 。

对于 .NET Framework 4.5，而不是使用多个独立的设置，提供了工作负荷定义的配置设置，这些设置可启用所有先前推荐的 GC 设置以及新的优化功能，从而为每个站点的工作集提供附加性能。

若要启用 GC 内存优化，请将以下设置添加到 Windows\Microsoft.NET\Framework\v4.0.30319\aspnet.config 文件：

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample16.xml)]

 (如果你熟悉以前的 aspnet.config 更改指南，请注意，此设置将替换旧设置，例如，无需设置 r、t 等。无需删除旧设置。 ) 

<a id="_Toc_perf_6"></a>
#### <a name="prefetching-for-web-applications"></a>对 web 应用程序的预提取

**要求**：在 Windows 8 上运行 .NET Framework 4。5

对于多个版本，Windows 包含了称为 [prefetcher](http://en.wikipedia.org/wiki/Prefetcher) 的技术，可减少应用程序启动时的磁盘读取成本。 由于冷启动是客户端应用程序的主要问题，因此此技术尚未包含在 Windows Server 中，后者仅包含对服务器非常重要的组件。 预提取功能现已在最新版本的 Windows Server 中提供，可在其中优化各个网站的启动。

对于 Windows Server，默认情况下不启用 prefetcher。 若要为高密度 web 宿主启用和配置 prefetcher，请在命令行中运行以下命令集：

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample17.cmd)]

然后，若要将 prefetcher 与 ASP.NET 应用程序集成，请将以下内容添加到 Web.config 文件：

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample18.xml)]

<a id="_Toc318097385"></a>
## <a name="aspnet-web-forms"></a>ASP.NET Web 窗体

<a id="_Toc318097386"></a>
### <a name="strongly-typed-data-controls"></a>强类型化数据控件

在 ASP.NET 4.5 中，Web 窗体包含一些用于处理数据的改进。 第一次改进是强类型化的数据控件。 对于以前版本的 ASP.NET 中的 Web 窗体控件，使用 *Eval* 和数据绑定表达式显示数据绑定值：

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample19.aspx)]

对于双向数据绑定，可使用 *Bind*：

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample20.aspx)]

在运行时，这些调用使用反射来读取指定成员的值，然后在标记中显示结果。 利用这种方法，可以轻松地将数据绑定到任意 unshaped 数据。

但是，这种类似于这样的数据绑定表达式并不支持用于成员名称、导航 (（如中转到定义) 或对这些名称进行编译时检查）等功能。

为了解决此问题，ASP.NET 4.5 添加了声明控件绑定到的数据的数据类型的功能。 使用新的 *ItemType* 属性来执行此操作。 设置此属性时，数据绑定表达式的作用域中提供两个新的类型化变量： *Item* 和 *BindItem*。 由于变量是强类型的，因此你可以获得 Visual Studio 开发体验的全部好处。

对于双向数据绑定表达式，请使用 *BindItem* 变量：

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample21.aspx)]

ASP.NET Web 窗体框架中支持数据绑定的大多数控件已更新，以支持 *ItemType* 属性。

<a id="_Toc318097387"></a>
### <a name="model-binding"></a>模型绑定

模型绑定将 ASP.NET Web 窗体控件中的数据绑定扩展到使用以代码为中心的数据访问中。 它结合了 *ObjectDataSource* 控件中的概念和 ASP.NET MVC 中的模型绑定。

<a id="_Toc318097388"></a>
#### <a name="selecting-data"></a>选择数据

若要将数据控件配置为使用模型绑定来选择数据，请将控件的 *SelectMethod* 属性设置为该页的代码中的方法的名称。 数据控件在页面生命周期中的适当时间调用方法，并自动绑定返回的数据。 无需显式调用 *DataBind* 方法。

在下面的示例中， *GridView* 控件配置为使用名为 *GetCategories*的方法：

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample22.aspx)]

在该页的代码中创建 *GetCategories* 方法。 对于简单的选择操作，方法不需要任何参数，并且应返回 *IEnumerable* 或 *IQueryable* 对象。 如果将新*的 ItemType*属性设置 (使强类型的数据绑定表达式（如之前) 的[强类型数据控件](#_Toc318097386)所述），则应返回这些接口的泛型版本， * &lt; &gt; 即 IEnumerable* t 或*IQueryable &lt; t &gt; *，其中*t*参数与*ItemType*属性的类型匹配 (例如， *IQueryable &lt; 类别 &gt; *) 。

下面的示例演示了 *GetCategories* 方法的代码。 此示例将实体框架 Code First 模型与 Northwind 示例数据库一起使用。 此代码可确保查询通过 *Include* 方法返回每个类别的相关产品的详细信息。  (这可确保标记中的 *TemplateField* 元素显示每个类别中的产品计数，无需 [选择 "n + 1](http://stackoverflow.com/questions/97197/what-is-the-n1-selects-problem)"。 ) 

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample23.cs)]

当页面运行时， *GridView* 控件会自动调用 *GetCategories* 方法，并使用配置的字段呈现返回的数据：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image2.png)

因为 select 方法返回 *IQueryable* 对象，所以在执行该查询之前， *GridView* 控件可以进一步对其进行操作。 例如，在执行所返回的*IQueryable*对象之前， *GridView*控件可以添加查询表达式进行排序和分页，以便这些操作由基础 LINQ 提供程序执行。 在这种情况下，实体框架将确保在数据库中执行这些操作。

下面的示例演示了修改为允许排序和分页的 *GridView* 控件：

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample24.aspx)]

现在，当页面运行时，控件可以确保只显示当前数据页，并按选定列排序：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image3.png)

若要筛选返回的数据，必须将参数添加到 select 方法。 在运行时，模型绑定将填充这些参数，您可以使用它们在返回数据之前更改查询。

例如，假设您希望允许用户通过在查询字符串中输入关键字来筛选产品。 您可以将参数添加到方法，并更新代码以使用参数值：

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample25.cs)]

如果为*关键字*提供了值，则此代码包含*Where*表达式，然后返回查询结果。

<a id="_Toc318097389"></a>
#### <a name="value-providers"></a>值提供程序

前面的示例并不特定于 *关键字* 参数的值来自何处。 若要指示此信息，可以使用参数特性。 在此示例中，可以使用*ModelBinding*命名空间中的*QueryStringAttribute*类：

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample26.cs)]

这将指示模型绑定在运行时尝试将值从查询字符串绑定到 *关键字* 参数。  (这可能会涉及到执行类型转换，但在这种情况下不会出现这种情况。 ) 如果无法提供值并且类型不可为 null，则会引发异常。

这些方法的值的源称为值提供程序，参数属性指示要使用的值提供程序称为值提供程序特性。 Web 窗体将包含 Web 窗体应用程序中的所有典型用户输入源的值提供程序和相应属性，例如查询字符串、cookie、窗体值、控件、视图状态、会话状态和配置文件属性。 你还可以编写自定义值提供程序。

默认情况下，参数名称用作查找值提供程序集合中的值的键。 在此示例中，代码将查找名为关键字的查询字符串值 (例如，~/default.aspx？关键字 = chef) 。 可以通过将自定义键作为参数传递给 parameter 特性来指定它。 例如，若要使用名为 q 的查询字符串变量的值，您可以执行以下操作：

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample27.cs)]

如果此方法在页面的代码中，则用户可以通过使用查询字符串传递关键字来筛选结果：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image4.png)

模型绑定完成了多个手动编码的任务：读取值、检查 null 值，尝试将其转换为适当的类型，检查转换是否成功，最后使用查询中的值。 模型绑定产生的代码更少，并且能够在整个应用程序中重复使用该功能。

<a id="_Toc318097390"></a>
#### <a name="filtering-by-values-from-a-control"></a>按控件中的值进行筛选

假设要扩展该示例，使用户可以从下拉列表中选择筛选器值。 向标记添加以下下拉列表，并将其配置为使用 *SelectMethod* 属性从另一个方法获取其数据：

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample28.aspx)]

通常，还会将 *EmptyDataTemplate* 元素添加到 *GridView* 控件，以便在未找到匹配的产品时，控件将显示一条消息：

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample29.aspx)]

在页代码中，为下拉列表添加新的选择方法：

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample30.cs)]

最后，更新 *GetProducts* select 方法以从下拉列表中获取一个包含所选类别 ID 的新参数：

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample31.cs)]

现在，当页面运行时，用户可以从下拉列表中选择一个类别，然后自动重新绑定 *GridView* 控件以显示筛选后的数据。 这是可能的，因为模型绑定跟踪 select 方法的参数值，并检测回发后是否有任何参数值发生了更改。 如果是这样，则模型绑定强制关联的数据控件重新绑定到数据。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image5.png)

<a id="_Toc318097391"></a>
### <a name="html-encoded-data-binding-expressions"></a>HTML 编码 Data-Binding 表达式

现在可以对数据绑定表达式的结果进行 HTML 编码。 将冒号 (： ) 添加到用于 &lt; 标记数据绑定表达式的% # 前缀的末尾：

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample32.aspx)]

<a id="_Toc318097392"></a>
### <a name="unobtrusive-validation"></a>非引人注目验证

你现在可以配置内置验证程序控件，以对客户端验证逻辑使用不引人注目的 JavaScript。 这可以显著减少在页面标记中以内联方式呈现的 JavaScript 数量，并减少总体页面大小。 可以通过以下任一方式为验证程序控件配置不引人注目的 JavaScript：

- 通过将以下设置添加到 Web.config 文件中的* &lt; appSettings &gt; *元素全局： 

    [!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample33.xml)]
- 通过将静态 *ValidationSettings* 属性设置为 *UnobtrusiveValidationMode* ，将 UnobtrusiveValidationMode 属性设置为全局性 (通常在 Global.asax 文件中的 *应用程序 \_ 启动* 方法) 。
- 通过将*page*类的新 " *UnobtrusiveValidationMode* " 属性设置为 "UnobtrusiveValidationMode"，单独用于页面 *。*

<a id="_Toc318097393"></a>
### <a name="html5-updates"></a>HTML5 更新

对 Web 窗体服务器控件进行了一些改进，以利用 HTML5 的新功能：

- 已更新*TextBox*控件的*TextMode*属性，以支持新的 HTML5 输入类型（如*电子邮件*、*日期时间*等）。
- *FileUpload*控件现在支持支持此 HTML5 功能的浏览器中的多个文件上传。
- 验证程序控件现在支持验证 HTML5 输入元素。
- 具有表示 URL 的特性的新 HTML5 元素现在支持 runat = "server"。 因此，可以在 URL 路径中使用 ASP.NET 约定，如 ~ 运算符来表示应用程序根 (例如， &lt; 视频 runat = "server" src = "~/myVideo.wmv"/ &gt;) 。
- 已修复 *UpdatePanel* 控件以支持发布 HTML5 输入字段。

<a id="_Toc318097394"></a>
## <a name="aspnet-mvc-4"></a>ASP.NET MVC 4

ASP.NET MVC 4 Beta 现在随附在 Visual Studio 11 Beta 版中。 ASP.NET MVC 是一个框架，用于通过利用模型-视图-控制器 (MVC) 模式来开发高度可测试性和可维护的 Web 应用程序。 ASP.NET MVC 4 使你可以轻松地生成适用于移动网络的应用程序并包括 ASP.NET Web API，这有助于构建可访问任何设备的 HTTP 服务。 有关详细信息，请参阅 [ASP.NET MVC 4 发行说明](mvc4-release-notes.md)。

<a id="_Toc318097395"></a>
## <a name="aspnet-web-pages-2"></a>ASP.NET 网页 2

新增功能包括：

- 新的和更新的站点模板。
- 使用 *验证* 帮助器添加服务器端和客户端验证。
- 使用资产管理器注册脚本的能力。
- 使用 OAuth 和 OpenID 启用 Facebook 和其他站点的登录。
- 使用 *map* helper 添加映射。
- 并行运行 Web Pages 应用程序。
- 移动设备的呈现页。

有关这些功能和整页代码示例的详细信息，请参阅 [Web Pages 2 Beta 版中的主要功能](https://go.microsoft.com/fwlink/?LinkID=227824)。

<a id="_Toc318097396"></a>
## <a name="visual-web-developer-11-beta"></a>Visual Web Developer 11 Beta

本部分提供有关在 Visual Web Developer 11 Beta 和 Visual Studio 2012 候选发布版中对 web 开发的改进的信息。

<a id="project-compatibility"></a>
### <a name="project-sharing-between-visual-studio-2010-and-visual-studio-2012-release-candidate-project-compatibility"></a>Visual Studio 2010 和 Visual Studio 2012 候选发布版本之间的项目共享 (项目兼容性) 

在 Visual Studio 2012 候选发布版本之前，在较新版本的 Visual Studio 中打开现有项目会启动转换向导。 这会强制将项目的 (资产) 的内容升级到不向后兼容的新格式。 因此，在转换后，无法在较旧版本的 Visual Studio 中打开该项目。

许多客户告诉我们，这并不是正确的方法。 在 Visual Studio 11 测试版中，我们现在支持通过 Visual Studio 2010 SP1 共享项目和解决方案。 这意味着，如果你在 Visual Studio 2012 候选发布版本中打开2010项目，你仍可以在 Visual Studio 2010 SP1 中打开该项目。

> [!NOTE]
> 几种类型的项目不能在 Visual Studio 2010 SP1 和 Visual Studio 2012 候选发布版本之间共享。 其中包括一些较旧的项目 (如用于特殊目的的 ASP.NET MVC 2 项目) 或项目 (如安装项目) 。

在 Visual Studio 11 Beta 中首次打开 Visual Studio 2010 SP1 Web 项目时，会将以下属性添加到项目文件中：

- FileUpgradeFlags
- UpgradeBackupLocation
- OldToolsVersion
- VisualStudioVersion
- VSToolsPath

FileUpgradeFlags、UpgradeBackupLocation 和 OldToolsVersion 由升级项目文件的进程使用。 它们不会影响在 Visual Studio 2010 中使用项目。

VisualStudioVersion 是 MSBuild 4.5 使用的新属性，用于指示当前项目的 Visual Studio 版本。 由于 MSBuild 4.0 中不存在此属性 (Visual Studio 2010 SP1 使用) 的 MSBuild 版本，因此我们会在项目文件中注入默认值。

VSToolsPath 属性用于确定要从 MSBuildExtensionsPath32 设置表示的路径导入的正确 .targets 文件。

此外，还有一些与 Import 元素相关的更改。 需要进行这些更改，以支持两个版本的 Visual Studio 之间的兼容性。

> [!NOTE]
> 如果在两台不同的计算机上的 Visual Studio 2010 SP1 和 Visual Studio 11 Beta 之间共享项目，并且项目在应用数据文件夹中包含本地数据库 \_ ，则必须确保两台计算机上都安装了数据库使用的 SQL Server 版本。

<a id="Configuration_Changes_In_ASPNET45_Website_Templates"></a>
### <a name="configuration-changes-in-aspnet-45-website-templates"></a>ASP.NET 4.5 网站模板中的配置更改

已对使用 Visual Studio 2012 候选发布版中的网站模板创建的站点的默认 *Web.config* 文件进行了以下更改：

- 在 `<httpRuntime>` 元素中， `encoderType` 现在默认设置属性，以使用已添加到 ASP.NET 的 AntiXSS 类型。 有关详细信息，请参阅 [AntiXSS Library](#_Toc318097382)。
- 同样，在 `<httpRuntime>` 元素中， `requestValidationMode` 特性设置为 "4.5"。 这意味着，默认情况下，请求验证配置为使用延迟 ( "延迟" ) 验证。 有关详细信息，请参阅 [New ASP.NET Request 验证功能](#_Toc318097379)。
- `<modules>`部分的元素 `<system.webServer>` 不包含 `runAllManagedModulesForAllRequests` 特性。  (其默认值为 false。 ) 这意味着，如果你使用的是尚未更新到 SP1 的 IIS 7 版本，则在新站点中进行路由时可能会遇到问题。 有关详细信息，请参阅 [IIS 7 for ASP.NET 路由中的本机支持](#Native_Support_In_IIS7_For_ASPNET_Routine)。

这些更改不会影响现有应用程序。 但是，它们可能代表现有网站与你使用新模板为 ASP.NET 4.5 创建的新网站之间的行为差异。

<a id="Native_Support_In_IIS7_For_ASPNET_Routine"></a>
### <a name="native-support-in-iis-7-for-aspnet-routing"></a>IIS 7 中用于 ASP.NET 路由的本机支持

这并不是 ASP.NET 的更改，但对于新网站项目的模板进行了更改，如果你正在使用的 IIS 7 版本未应用 SP1 更新，则可能会影响你。

在 ASP.NET 中，可以将以下配置设置添加到应用程序，以便支持路由：

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample34.xml?highlight=3)]

当 **runAllManagedModulesForAllRequests** 为 true 时，url （如）将 `http://mysite/myapp/home` 转到 ASP.NET，即使 url 上没有 *.aspx*、 *mvc*或类似扩展名也是如此。

对 IIS 7 进行的更新使得 **runAllManagedModulesForAllRequests** 设置不必要，并支持本机 ASP.NET 路由。  (有关更新的信息，请参阅 Microsoft 支持部门文章 [提供了可使某些 IIS 7.0 或 iis 7.5 处理程序处理其 url 不以句点结尾的请求的更新](https://support.microsoft.com/kb/980368)。 ) 

如果你的网站在 IIS 7 上运行，并且如果 IIS 已更新，则不需要将 **runAllManagedModulesForAllRequests** 设置为 true。 事实上，不建议将其设置为 true，因为这样做会增加不必要的处理开销来请求。 如果此设置为 true，则所有请求（包括 *.htm*、 *.jpg*和其他静态文件的请求）也会经历 ASP.NET 请求管道。

如果使用 Visual Studio 2012 RC 中提供的模板创建新的 ASP.NET 4.5 网站，则网站的配置不包括 **runAllManagedModulesForAllRequests** 设置。 这意味着，默认情况下，设置为 false。

如果你随后在未安装 SP1 的 Windows 7 上运行该网站，则 IIS 7 将不包括所需的更新。 因此，路由将不起作用，并且你将看到错误。 如果出现无法使用路由的问题，则可以执行以下任一操作：

- 将 Windows 7 更新为 SP1，这会将更新添加到 IIS 7。
- 安装前面列出的 Microsoft 支持部门文章中描述的更新。
- 在该网站的 Web.config 文件中，将 **runAllManagedModulesForAllRequests** 设置为 true。 请注意，这将为请求增加一些开销。

<a id="_Toc318097397"></a>
### <a name="html-editor"></a>HTML 编辑器

<a id="_Toc318097398"></a>
#### <a name="smart-tasks"></a>智能任务

在设计视图中，服务器控件的复杂属性通常具有相关联的对话框和向导，以使其易于设置。 例如，您可以使用一个特殊的对话框向 *Repeater* 控件添加数据源，或将列添加到 *GridView* 控件。

但对于复杂属性，这种类型的 UI 帮助在源视图中不可用。 因此，Visual Studio 11 为源视图引入了智能任务。 智能任务是适用于 c # 和 Visual Basic 编辑器中的常用功能的上下文感知快捷方式。

对于 ASP.NET Web 窗体控件，当插入点位于元素内时，智能任务会作为小标志符号出现在服务器标记中：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image6.png)

当单击标志符号或按 CTRL + 时，智能任务将展开。  (点) ，就像在代码编辑器中一样。 然后，它会显示与设计视图中的智能任务类似的快捷方式。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image7.png)

例如，上图中的智能任务显示 GridView 任务选项。 如果选择 "编辑列"，将显示以下对话框：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image8.png)

填写此对话框将设置可以在设计视图中设置的相同属性。 单击 "确定" 后，将用新设置更新控件的标记：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image9.png)

<a id="_Toc318097399"></a>
#### <a name="wai-aria-support"></a>WAI-ARIA 支持

编写可访问的网站越来越重要。 [WAI-ARIA 辅助功能标准](http://www.w3.org/WAI/intro/aria)定义开发人员应如何编写可访问的网站。 Visual Studio 现在完全支持此标准。

例如， *role* 属性现在具有完整的 IntelliSense：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image10.png)

WAI 标准还引入了用 *ARIA* 作为前缀的属性，使你可以向 HTML5 文档添加语义。 Visual Studio 还完全支持以下 *aria* 特性：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image11.png) ![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image12.png)

<a id="_Toc318097400"></a>
#### <a name="new-html5-snippets"></a>新 HTML5 代码段

为了更快、更轻松地编写常用 HTML5 标记，Visual Studio 提供了很多代码段。 视频片段是一个示例：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image13.png)

若要调用代码段，请在 IntelliSense 中选择元素时，按 Tab 两次：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image14.png)

这会生成一个可自定义的代码段。

<a id="_Toc318097401"></a>
#### <a name="extract-to-user-control"></a>提取到用户控件

在较大的网页中，最好将各个部分移到用户控件中。 这种形式的重构有助于提高页面的可读性，并可以简化页面结构。

若要简化此操作，在 "源" 视图中编辑 Web 窗体页时，现在可以在页中选择文本，右键单击它，然后选择 "提取到用户控件"：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image2.jpg)

<a id="_Toc318097402"></a>
#### <a name="intellisense-for-code-nuggets-in-attributes"></a>特性中代码片段的 IntelliSense

Visual Studio 始终为任何页面或控件中的服务器端代码片段提供 IntelliSense。 现在，Visual Studio 还包括 HTML 特性中代码片段的 IntelliSense。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image15.png)

这样可以更轻松地创建数据绑定表达式：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image16.png)

<a id="_Toc318097403"></a>
#### <a name="automatic-renaming-of-matching-tag-when-you-rename-an-opening-or-closing-tag"></a>重命名开始或结束标记时自动重命名匹配标记

如果重命名 HTML 元素 (例如，将 *div* 标记更改为) *标头* 标记，则对应的开始标记或结束标记也会实时更改。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image17.png)

这有助于避免在您忘记更改结束标记或更改错误时出现的错误。

<a id="_Toc318097404"></a>
#### <a name="event-handler-generation"></a>生成事件处理程序

Visual Studio 现在包含源视图中的功能，可帮助你编写和手动绑定事件处理程序。 如果在 "源" 视图中编辑事件名称，IntelliSense &lt; 将显示 "创建新事件 &gt; "，该事件将在页面的代码中创建一个具有正确签名的事件处理程序：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image3.jpg)

默认情况下，事件处理程序将使用控件的 ID 作为事件处理方法的名称：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image4.jpg)

在这种情况下，生成的事件处理程序将类似于以下 (在 c # 中 ) ：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image18.png)

<a id="_Toc318097405"></a>
#### <a name="smart-indent"></a>智能缩进

当在空 HTML 元素内按 Enter 时，编辑器会将插入点放在正确的位置：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image19.png)

如果在此位置按 Enter，则结束标记将向下移动并缩进，以匹配开始标记。 插入点还缩进：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image20.png)

<a id="_Toc318097406"></a>
#### <a name="auto-reduce-statement-completion"></a>自动减少语句完成

Visual Studio 中的 IntelliSense 列表现在基于你键入的内容进行筛选，以便仅显示相关选项：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image21.png)

IntelliSense 还基于 IntelliSense 列表中各个单词的标题用例进行筛选。 例如，如果键入 "dl"，则会显示 dl 和 asp： DataList：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image22.png)

此功能可以更快地获取已知元素的语句完成。

<a id="_Toc318097407"></a>
### <a name="javascript-editor"></a>JavaScript 编辑器

Visual Studio 2012 候选发布版中的 JavaScript 编辑器是全新的，它大大提高了在 Visual Studio 中使用 JavaScript 的体验。

<a id="_Toc318097408"></a>
#### <a name="code-outlining"></a>代码大纲显示

现在会自动为所有函数创建大纲显示区域，从而使您可以折叠部分文件中与当前焦点无关的部分。

<a id="_Toc318097409"></a>
#### <a name="brace-matching"></a>大括号匹配

当您将插入点放在左大括号或右大括号上时，该编辑器将突出显示匹配项。

<a id="_Toc318097410"></a>
#### <a name="go-to-definition"></a>转到定义

"转到定义" 命令可用于跳转到函数或变量的源。

<a id="_Toc318097411"></a>
#### <a name="ecmascript5-support"></a>ECMAScript5 支持

编辑器支持 ECMAScript5 中的新语法和 Api，这是描述 JavaScript 语言的最新标准版本。

<a id="_Toc318097412"></a>
#### <a name="dom-intellisense"></a>DOM IntelliSense

已改进了 DOM Api 的 IntelliSense，并支持许多新的 HTML5 Api，包括 *querySelector*、DOM 存储、跨文档消息和 *画布*。 DOM IntelliSense 现在由单个简单的 JavaScript 文件驱动，而不是由本机类型库定义驱动。 这样就可以轻松地扩展或替换。

<a id="_Toc318097413"></a>
#### <a name="vsdoc-signature-overloads"></a>VSDOC 签名重载

现在，可以使用新的* &lt; 签名 &gt; *元素为 JavaScript 函数的单独重载声明详细的 IntelliSense 注释，如以下示例中所示：

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample35.cs)]

<a id="_Toc318097414"></a>
#### <a name="implicit-references"></a>隐式引用

你现在可以将 JavaScript 文件添加到一个中央列表，该列表将隐式包含在任何给定 JavaScript 文件或块引用的文件列表中，这意味着你将获得其内容的 IntelliSense。 例如，可以将 jQuery 文件添加到文件的中央列表，并在文件的任何 JavaScript 块中获取 jQuery 函数的 IntelliSense，无论是否已使用/// &lt; reference/) 显式引用 (&gt; 。

<a id="_Toc318097415"></a>
### <a name="css-editor"></a>CSS 编辑器

<a id="_Toc318097416"></a>
#### <a name="auto-reduce-statement-completion"></a>自动减少语句完成

现在，CSS 的 IntelliSense 列表基于所选架构支持的 CSS 属性和值进行筛选。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image23.png)

IntelliSense 还支持标题 case 搜索：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image24.png)

<a id="_Toc318097417"></a>
#### <a name="hierarchical-indentation"></a>分层缩进

CSS 编辑器使用缩进来显示分层规则，这为您提供了对级联规则进行逻辑组织的概述。 在下面的示例中，#list 选择器是列表的一个级联子级，因此缩进。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image25.png)

下面的示例演示了更复杂的继承：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image26.png)

规则的缩进由其父规则确定。 默认情况下启用分层缩进，但你可以在 "选项" 对话框 (工具 "、菜单栏中的选项) ：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image27.png)

<a id="_Toc318097418"></a>
#### <a name="css-hacks-support"></a>CSS 黑客支持

分析数百个真实的 CSS 文件表明，CSS 攻击非常常见，而 Visual Studio 现在支持最广泛使用的文件。 此支持包括智能感知和对星形 (\*) 和下划线 (\_) 属性黑客的验证：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image28.png)

还支持典型的选择器黑客，以便即使在应用分层缩进时也能进行维护。 用于面向 Internet Explorer 7 的典型选择器黑客是在选择器前面预置* \* ： first-child + html*。 使用该规则将维护分层缩进：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image29.png)

<a id="_Toc318097419"></a>
#### <a name="vendor-specific-schemas--moz---webkit"></a>特定于供应商的架构 (-moz-,-webkit) 

CSS3 引入了许多在不同时间由不同的浏览器实现的属性。 之前，此方法迫使开发人员使用特定于供应商的语法为特定浏览器编写代码。 这些特定于浏览器的属性现已包含在 IntelliSense 中。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image30.png)

<a id="_Toc318097420"></a>
#### <a name="commenting-and-uncommenting-support"></a>注释和取消注释支持

你现在可以使用在代码编辑器中使用的相同快捷键来注释和取消注释 CSS 规则 (Ctrl + K、C to 注释和 Ctrl + K，用于取消注释) 。

<a id="_Toc318097421"></a>
#### <a name="color-picker"></a>颜色选取器

在 Visual Studio 的早期版本中，与颜色相关的属性的 IntelliSense 由命名颜色值的下拉列表组成。 该列表已替换为功能完备的颜色选取器。

输入颜色值时，颜色选取器会自动显示，并显示以前使用的颜色的列表，后跟默认调色板。 您可以使用鼠标或键盘选择颜色。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image31.png)

该列表可以扩展为完整的颜色选取器。 使用选取器可以在移动不透明度滑块时，通过自动将任何颜色转换为 RGBA 来控制 alpha 通道：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image32.png)

<a id="_Toc318097422"></a>
#### <a name="snippets"></a>代码片段

CSS 编辑器中的代码片段使创建跨浏览器样式更加简单快捷。 许多需要浏览器特定设置的 CSS3 属性现在已滚动到代码段中。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image33.png)

CSS 代码段支持 (如 CSS3 媒体查询) 的高级方案， ( @ ) 键入符号，其中显示 IntelliSense 列表。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image34.png)

当你选择 " @media 值" 并按 tab 键时，CSS 编辑器将插入以下代码片段：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image5.jpg)

与代码的代码段一样，你可以创建自己的 CSS 代码段。

<a id="_Toc318097423"></a>
#### <a name="custom-regions"></a>自定义区域

已在代码编辑器中使用的命名代码区域现在可用于 CSS 编辑。 这使您可以轻松地对相关样式块进行分组。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image35.png)

当区域处于折叠状态时，它将显示区域的名称：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image36.png)

<a id="_Toc318097424"></a>
### <a name="page-inspector"></a>Page Inspector

Page Inspector 是一种工具，用于在 Visual Studio IDE 中 (HTML、Web 窗体、ASP.NET MVC 或 Web Pages) 呈现网页，并使你可以查看源代码和生成的输出。 对于 ASP.NET 页，Page Inspector 允许你确定哪些服务器端代码生成了呈现到浏览器中的 HTML 标记。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image37.png)

有关 Page Inspector 的详细信息，请参阅以下教程：

- 在[ASP.NET MVC](../mvc/overview/views/using-page-inspector-in-aspnet-mvc.md)中使用 Page Inspector
- 在[ASP.NET Web 窗体](../web-forms/overview/getting-started/using-page-inspector-in-a-visual-studio-11-beta-web-forms-project.md)中使用 Page Inspector

<a id="_Toc318097425"></a>
### <a name="publishing"></a>发布

<a id="_Toc318097426"></a>
#### <a name="publish-profiles"></a>发布配置文件

在 Visual Studio 2010 中，Web 应用程序项目的发布信息不会存储在版本控制中，也不会与他人共享。 在 Visual Studio 2012 候选发布版中，发布配置文件的格式已更改。 它已成为一个团队项目，现在可以轻松地利用基于 MSBuild 的生成。 "发布" 对话框中的生成配置信息可在发布之前轻松地切换生成配置。

发布配置文件存储在 PublishProfiles 文件夹中。 文件夹位置取决于所使用的编程语言：

- C #： Properties\PublishProfiles
- Visual Basic：我的 Project\PublishProfiles

每个配置文件都是一个 MSBuild 文件。 在发布过程中，此文件将导入项目的 MSBuild 文件。 在 Visual Studio 2010 中，如果要对发布或包过程进行更改，则必须将自定义项放在名为 **项目名称**的文件中。 这仍受支持，但你现在可以将你的自定义项放在发布配置文件中。 这样，自定义将仅用于该配置文件。

你现在还可以利用 MSBuild 中的发布配置文件。 为此，请在生成项目时使用以下命令：

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample36.cmd)]

项目 .csproj 值是项目的路径，ProfileName 是要发布的配置文件的名称。 或者，你可以将完整路径传递到发布配置文件，而不是传递 *PublishProfile* 属性的配置文件名称。

<a id="_Toc318097427"></a>
#### <a name="aspnet-precompilation-and-merge"></a>ASP.NET 预编译和合并

对于 Web 应用程序项目，Visual Studio 2012 候选发布版将在 "打包/发布 Web 属性" 页上添加一个选项，通过该选项，您可以在发布或打包项目时预编译和合并网站的内容。 若要查看这些选项，请在解决方案资源管理器中右键单击项目，选择 "属性"，然后选择 "打包/发布 Web" 属性页。 下图显示了 "发布之前预编译此应用程序" 选项。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image6.jpg)

如果选择此选项，则每当您发布或打包 web 应用程序时，Visual Studio 都会预编译应用程序。 如果要控制如何预编译站点或如何合并程序集，请单击 "高级" 按钮以配置这些选项。

<a id="_Toc318097428"></a>
### <a name="iis-express"></a>IIS Express

现在 IIS Express 用于测试 Visual Studio 中 web 项目的默认 web 服务器。 开发期间本地 web 服务器仍有 Visual Studio 开发服务器，但现在建议使用 IIS Express 服务器。 在 Visual Studio 11 Beta 中使用 IIS Express 的体验非常类似于在 Visual Studio 2010 SP1 中使用它。

<a id="_Toc318097429"></a>
## <a name="disclaimer"></a>免责声明

这是一份初稿，并可能在本文所述软件最终商业发布之前进行大幅更改。

本文档中包含的信息代表 Microsoft Corporation 在发布之日对所讨论问题的当前观点。 由于 Microsoft 必须响应不断变化的市场条件，因此不应将其解释为 Microsoft 作出的承诺，并且 Microsoft 无法保证在发布日期之后提供的任何信息的准确性。

本白皮书仅用于提供信息。 MICROSOFT 对本文档中的信息不做任何明示、暗示或法定的担保。

用户有责任遵守所有适用的版权法/著作权法。 在不限制版权所辖权利的前提下，未经 Microsoft Corporation 的明确书面许可，本文档的任何部分不得被复制、存储或引进检索系统，或者以任何形式、任何方式（电子、机械、影印、录音等）或为任何目的进行传播。

Microsoft 可能拥有本文档所涵盖主题的专利、专利申请、商标、版权或其他知识产权。 除非 Microsoft 提供了明确的书面许可协议，否则提供本文档并不意味着赋予您这些专利、商标、版权或其他知识产权的任何许可。

除非另有说明，否则，本文档中提及的示例公司、组织、产品、域名、电子邮件地址、徽标、人员、地点和事件均属虚构，与任何真实的公司、组织、产品、域名、电子邮件地址、徽标、人物、地点或事件没有任何关联。

(C) 2012 Microsoft Corporation。 保留所有权利。

Microsoft 和 Windows 是 Microsoft Corporation 在美国和/或其他国家/地区的注册商标或商标。

此处提到的真实公司和产品的名称可能是其各自所有者的商标。

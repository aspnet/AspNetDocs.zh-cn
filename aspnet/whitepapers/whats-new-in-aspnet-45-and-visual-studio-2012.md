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
# <a name="whats-new-in-aspnet-45-and-visual-studio-2012"></a>ASP.NET 4.5 和 Visual Studio 2012 的新增功能

> 本文档介绍 ASP.NET 4.5 中引入的新功能和增强功能。 它还描述了在 Visual Studio 2012 中为 Web 开发所做的改进。 本文档最初发布于 2012 年 2 月 29 日。

- [ASP.NET核心运行时和框架](#_Toc318097372)

    - [异步读取和写入 HTTP 请求和响应](#_Toc318097373)
    - [HttpRequest 处理的改进](#_Toc318097374)
    - [异步刷新响应](#_Toc318097375)
    - [支持*等待*和基于*任务的*异步模块和处理程序](#_Toc318097376)
    - [异步 HTTP 模块](#_Toc318097377)
    - [异步 HTTP 处理程序](#_Toc318097378)
    - [新的ASP.NET请求验证功能](#_Toc318097379)
    - [延迟（"延迟"）请求验证](#_Toc318097380)
    - [支持未经验证的请求](#_Toc318097381)
    - [AntiXSS 库](#_Toc318097382)
    - [支持 WebSocket 协议](#_Toc318097383)
    - [捆绑和最小化](#_Toc318097384)
    - [Web 托管的性能改进](#_Toc_perf)

        - [关键性能因素](#_Toc_perf_1)
        - [对新性能功能的要求](#_Toc_perf_2)
        - [共享公共程序集](#_Toc_perf_3)
        - [使用多核 JIT 编译，加快启动速度](#_Toc_perf_4)
        - [调整垃圾回收以优化内存](#_Toc_perf_5)
        - [为 Web 应用程序预取](#_Toc_perf_6)
- [ASP.NET Web 表单](#_Toc318097385)

    - [强类型化数据控件](#_Toc318097386)
    - [模型绑定](#_Toc318097387)

        - [选择数据](#_Toc318097388)
        - [价值提供者](#_Toc318097389)
        - [按控件的值筛选](#_Toc318097390)
    - [HTML 编码数据绑定表达式](#_Toc318097391)
    - [不显眼的验证](#_Toc318097392)
    - [HTML5 更新](#_Toc318097393)
- [ASP.NET MVC 4](#_Toc318097394)
- [ASP.NET 网页 2](#_Toc318097395)
- [Visual Studio 2012 候选发布版本](#_Toc318097396)

    - [Visual Studio 2010 和 Visual Studio 2012 版本候选版本之间的项目共享（项目兼容性）](#project-compatibility)
    - [ASP.NET 4.5 网站模板中的配置更改](#Configuration_Changes_In_ASPNET45_Website_Templates)
    - [IIS 7 中用于ASP.NET路由的本机支持](#Native_Support_In_IIS7_For_ASPNET_Routine)
    - [HTML 编辑器](#_Toc318097397)

        - [智能任务](#_Toc318097398)
        - [WAI-ARIA 支持](#_Toc318097399)
        - [新的 HTML5 代码段](#_Toc318097400)
        - [提取到用户控件](#_Toc318097401)
        - [属性中代码块的 IntelliSense](#_Toc318097402)
        - [重命名打开或关闭标记时自动重命名匹配标记](#_Toc318097403)
        - [事件处理程序生成](#_Toc318097404)
        - [智能缩进](#_Toc318097405)
        - [自动减少语句完成](#_Toc318097406)
    - [JavaScript 编辑器](#_Toc318097407)

        - [代码概述](#_Toc318097408)
        - [大括号匹配](#_Toc318097409)
        - [转到定义](#_Toc318097410)
        - [ECMAScript5 支持](#_Toc318097411)
        - [DOM 感知](#_Toc318097412)
        - [VSDOC 签名重载](#_Toc318097413)
        - [隐式引用](#_Toc318097414)
    - [CSS 编辑器](#_Toc318097415)

        - [自动减少语句完成](#_Toc318097416)
        - [分层缩进。](#_Toc318097417)
        - [CSS 黑客支持](#_Toc318097418)
        - [供应商特定的架构（-moz-,-webkit）](#_Toc318097419)
        - [评论和非评论支持](#_Toc318097420)
        - [颜色选取器](#_Toc318097421)
        - [片段](#_Toc318097422)
        - [自定义区域](#_Toc318097423)
    - [Page Inspector](#_Toc318097424)
    - [发布](#_Toc318097425)

        - [发布配置文件](#_Toc318097426)
        - [ASP.NET预编译和合并](#_Toc318097427)
- [IIS Express](#_Toc318097428)
- [免责声明](#_Toc318097429)

<a id="_Toc318097372"></a>
## <a name="aspnet-core-runtime-and-framework"></a>ASP.NET核心运行时和框架

<a id="_Toc318097373"></a>
### <a name="asynchronously-reading-and-writing-http-requests-and-responses"></a>异步读取和写入 HTTP 请求和响应

ASP.NET 4 引入了使用*httpRequest.Get 无缓冲区输入流*方法将 HTTP 请求实体作为流读取的功能。 此方法提供了对请求实体的流式访问。 但是，它同步执行，在请求的持续时间内将线程捆绑在一起。

ASP.NET 4.5 支持在 HTTP 请求实体上异步读取流的功能，以及异步刷新的能力。 ASP.NET 4.5 还使您能够对 HTTP 请求实体进行双缓冲，从而更轻松地与下游 HTTP 处理程序（如 .aspx 页处理程序和 ASP.NET MVC 控制器）集成。

<a id="_Toc318097374"></a>
#### <a name="improvements-to-httprequest-handling"></a>HttpRequest 处理的改进

ASP.NET 4.5 从 HttpRequest 返回的流引用 *.Get无缓冲区输入流*支持同步和异步读取方法。 从*Get 无缓冲区输入流*返回的*流*对象现在实现了 BeginRead 和 EndRead 方法。 异步*流*方法允许您以块异步读取请求实体，而ASP.NET在异步读取循环的每个迭代之间释放当前线程。

ASP.NET 4.5 还添加了一种以缓冲方式读取请求实体的配套方法 *：httpRequest.GetBufferedInputStream*。 这种新的重载工作类似于*Get 无缓冲区输入流*，支持同步读取和异步读取。 但是，在读取时 *，GetBufferedInputStream*还会将实体字节复制到ASP.NET内部缓冲区中，以便下游模块和处理程序仍可以访问请求实体。 例如，如果管道中的一些上游代码已经使用*GetBufferedInputStream*读取了请求实体，您仍可以使用*HttpRequest.Form*或*httpRequest.Files*。 这允许您对请求执行异步处理（例如，将大型文件上载流式传输到数据库），但之后仍运行 .aspx 页和 MVC ASP.NET控制器。

<a id="_Toc318097375"></a>
#### <a name="asynchronously-flushing-a-response"></a>异步刷新响应

当客户端距离遥远或具有低带宽连接时，向 HTTP 客户端发送响应可能需要相当长的时间。 通常ASP.NET缓冲响应字节，因为它们是由应用程序创建的。 然后ASP.NET然后在请求处理的末尾执行累积缓冲区的单个发送操作。

如果缓冲响应很大（例如，将大型文件流式传输到客户端），则必须定期调用*HttpResponse.Flush，* 以便向客户端发送缓冲输出并保持内存使用情况控制。 但是，由于*Flush*是同步调用，因此迭代调用*Flush*仍会在可能长时间运行的请求的持续时间内使用线程。

ASP.NET 4.5 添加了使用*HttpResponse*类的*BeginFlush*和*endFlush*方法异步执行刷新的支持。 使用这些方法，您可以创建异步模块和异步处理程序，这些模块和异步处理程序在不捆绑操作系统线程的情况下将数据增量发送到客户端。 在*BeginFlush*和*结束刷新*调用之间，ASP.NET释放当前线程。 这大大减少了支持长时间运行的 HTTP 下载所需的活动线程总数。

<a id="_Toc318097376"></a>
### <a name="support-for-await-and-task---based-asynchronous-modules-and-handlers"></a>支持*等待*和*任务*- 基于异步模块和处理程序

.NET 框架 4 引入了一个异步编程概念，称为*任务*。 任务由系统中的*任务*类型和相关类型表示 *。* .NET Framework 4.5 基于此功能，具有编译器增强功能，使使用*Task*对象变得简单。 在 .NET 框架 4.5 中，编译器支持两个新关键字：*等待*和*异步*。 *await*关键字是语法速记，用于指示代码段应异步等待其他代码段。 *异步*关键字表示可用于将方法标记为基于任务的异步方法的提示。

*await、**异步*和*任务*对象的组合使您在 .NET 4.5 中编写异步代码变得更加容易。 ASP.NET 4.5 支持这些简化与新的 API，允许您编写异步 HTTP 模块和异步 HTTP 处理程序使用新的编译器增强功能。

<a id="_Toc318097377"></a>
#### <a name="asynchronous-http-modules"></a>异步 HTTP 模块

假设您要在返回*任务*对象的方法内执行异步工作。 以下代码示例定义了一个异步方法，该方法进行异步调用以下载 Microsoft 主页。 请注意在方法签名中使用*异步*关键字，并注意对*下载StringTaskAsync*的*等待*调用。

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample1.cs)]

这就是您需要编写的 - .NET Framework 将自动处理在等待下载完成时展开调用堆栈，以及在下载完成后自动还原调用堆栈。

现在假设您要在异步ASP.NET HTTP 模块中使用此异步方法。 ASP.NET 4.5 包括帮助器方法 *（EventHandlerTaskAsyncHelper*） 和新的委托类型 *（TaskEventHandler），* 可用于将基于任务的异步方法与 ASP.NET HTTP 管道公开的较旧的异步编程模型集成。 此示例演示如何：

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample2.cs)]

<a id="_Toc318097378"></a>
#### <a name="asynchronous-http-handlers"></a>异步 HTTP 处理程序

在ASP.NET中编写异步处理程序的传统方法是实现*IHttpAsyncHandler*接口。 ASP.NET 4.5 引入了可以从派生的*HttpTaskSyncHandler*异步基类型，这使得编写异步处理程序变得更加容易。

*HttpTaskAsyncHandler*类型是抽象的，需要您重写*ProcessRequestAsync*方法。 内部ASP.NET负责将*ProcessRequestAsync*的返回签名（*任务*对象）与ASP.NET管道使用的旧异步编程模型集成。

下面的示例演示如何使用*Task*和*等待*作为异步 HTTP 处理程序实现的一部分：

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample3.cs)]

<a id="_Toc318097379"></a>
### <a name="new-aspnet-request-validation-features"></a>新的ASP.NET请求验证功能

默认情况下，ASP.NET执行请求验证 - 它会检查在字段、标头、Cookie 等中查找标记或脚本的请求。 如果检测到任何异常，ASP.NET将引发异常。 这是抵御潜在跨站点脚本攻击的第一道防线。

ASP.NET 4.5 使选择性读取未经验证的请求数据变得容易。 ASP.NET 4.5 还集成了流行的 AntiXSS 库，该库以前是外部库。

开发人员经常要求能够有选择地关闭其应用程序的请求验证。 例如，如果您的应用程序是论坛软件，您可能希望允许用户提交 HTML 格式的论坛帖子和评论，但仍要确保请求验证检查所有其他内容。

ASP.NET 4.5 引入了两个功能，使您能够轻松有选择地处理未验证的输入：延迟（"延迟"）请求验证和对未验证请求数据的访问。

<a id="_Toc318097380"></a>
#### <a name="deferred-lazy-request-validation"></a>延迟（"延迟"）请求验证

在 ASP.NET 4.5 中，默认情况下，所有请求数据都需接受请求验证。 但是，您可以将应用程序配置为延迟请求验证，直到实际访问请求数据。 （这有时称为延迟请求验证，具体取决于某些数据方案的延迟加载等术语。通过将*请求验证模式*属性设置为*httpRUntime*元素中的 4.5，可以将应用程序配置为在 Web.config 文件中使用延迟验证，如以下示例所示：

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample4.xml)]

当请求验证模式设置为 4.5 时，请求验证仅针对特定请求值触发，并且仅在代码访问该值时触发。 例如，如果代码获取了"Request.Form_"论坛\_帖子"的值，则仅针对窗体集合中该元素调用请求验证。 *窗体*集合中的其他元素均未经过验证。 在ASP.NET的早期版本中，当访问集合中的任何元素时，将触发整个请求集合的请求验证。 新的行为使不同的应用程序组件能够更轻松地查看不同的请求数据，而不会触发其他部分的请求验证。

<a id="_Toc318097381"></a>
#### <a name="support-for-unvalidated-requests"></a>支持未经验证的请求

仅延迟请求验证并不能解决选择性绕过请求验证的问题。 对"请求.Form_"论坛\_帖子"的调用仍触发该特定请求值的请求验证。 但是，您可能希望在不触发验证的情况下访问此字段，因为您希望允许该字段中的标记。

为此，ASP.NET 4.5 现在支持对请求数据的未经验证的访问。 ASP.NET 4.5 在*HttpRequest*类中包括一个新的*未验证*集合属性。 此集合提供对请求数据的所有常见值（如*窗体*、*查询字符串**、Cookie*和*Url）* 的访问。

使用论坛示例，为了能够读取未经验证的请求数据，首先需要将应用程序配置为使用新的请求验证模式：

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample5.xml)]

然后，您可以使用*HttpRequest.未验证*的属性读取未验证的窗体值：

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample6.cs)]

> [!WARNING]
> 安全性 -*小心使用未经验证的请求数据！* ASP.NET 4.5 添加了未经验证的请求属性和集合，以便您更轻松地访问非常具体的未验证请求数据。 但是，您仍必须对原始请求数据执行自定义验证，以确保不会向用户呈现危险文本。

<a id="_Toc318097382"></a>
### <a name="antixss-library"></a>AntiXSS 库

由于 Microsoft AntiXSS 库的普及，ASP.NET 4.5 现在包含该库版本 4.0 的核心编码例程。

编码例程由新*系统.Web.Security.AntiXs*命名空间中的*AntiXsEncoder*类型实现。 您可以通过调用类型中实现的任何静态编码方法直接使用*AntiXsEncoder*类型。 但是，使用新的反 XSS 例程的最简单方法是将ASP.NET应用程序配置为默认使用*AntiXsEncoder*类。 为此，向 Web.config 文件添加以下属性：

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample7.xml)]

当*编码器类型*属性设置为使用*AntiXsEncoder*类型时，ASP.NET中的所有输出编码将自动使用新的编码例程。

这些是外部 AntiXSS 库中已集成到 ASP.NET 4.5 中的部分：

- *Html编码* *，HtmlFormUrl 编码*， 和*html 属性编码*
- *XmlAttributeEncode*和*XmlEncode*
- *UrlEncode*和*UrlPath 编码*（新）
- *CsEncode*

<a id="_Toc318097383"></a>
### <a name="support-for-websockets-protocol"></a>支持 WebSocket 协议

WebSockets 协议是基于标准的网络协议，它定义了如何通过 HTTP 在客户端和服务器之间建立安全的实时双向通信。 Microsoft 与 IETF 和 W3C 标准机构合作，帮助定义该协议。 WebSockets 协议由任何客户端（而不仅仅是浏览器）支持，Microsoft 在客户端和移动操作系统上投入大量资源支持 WebSocket 协议。

WebSockets 协议使在客户端和服务器之间创建长时间运行的数据传输变得更加容易。 例如，编写聊天应用程序要容易得多，因为您可以在客户端和服务器之间建立真正的长时间运行的连接。 您不必使用定期轮询或 HTTP 长轮询等解决方法来模拟套接字的行为。

ASP.NET 4.5 和 IIS 8 都支持低级 WebSocket，使ASP.NET开发人员能够使用托管 API 在 WebSocket 对象上异步读取和写入字符串和二进制数据。 对于ASP.NET 4.5，有一个新的*System.Web.WebSockets*命名空间，其中包含用于使用 WebSockets 协议的类型。

浏览器客户端通过创建 DOM WebSocket 对象来建立*WebSocket*连接，该对象指向ASP.NET应用程序中的 URL，如以下示例所示：

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample8.cs)]

您可以使用任何类型的模块或处理程序在ASP.NET创建 WebSockets 终结点。 在前面的示例中，使用了 .ashx 文件，因为 .ashx 文件是创建处理程序的快速方法。

根据 WebSocket 协议，ASP.NET应用程序通过指示请求应从 HTTP GET 请求升级到 WebSockets 请求来接受客户端的 WebSockets 请求。 下面是一个示例：

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample9.cs)]

*AcceptWebSocketRequest 方法*接受函数委托，因为ASP.NET解除当前 HTTP 请求，然后将控制权传输到函数委托。 从概念上讲，这种方法类似于您使用*System.Threading.Thread*的方式，在其中定义执行后台工作的线程启动委托。

ASP.NET和客户端成功完成 WebSocket 握手后，ASP.NET调用您的委托，WebSockets 应用程序开始运行。 以下代码示例显示了一个简单的回声应用程序，该应用程序在ASP.NET中使用内置 WebSocket 支持：

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample10.cs)]

.NET 4.5 中支持*await*关键字和基于异步任务的操作自然适合编写 WebSockets 应用程序。 代码示例显示 WebSockets 请求完全异步地在ASP.NET内部运行。 应用程序通过调用*await 套接字以异步等待从客户端发送消息。接收Async*。 同样，您可以通过调用*await 套接字向客户端发送异步消息。森步同步*。

在浏览器中，应用程序通过*onmessage*功能接收 WebSocket 消息。 要从浏览器发送消息，请调用*WebSocket* DOM 类型的*发送*方法，如以下示例所示：

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample11.cs)]

将来，我们可能会发布此功能的更新，以抽象掉 WebSocket 应用程序在此版本中所需的一些低级编码。

<a id="_Toc318097384"></a>
### <a name="bundling-and-minification"></a>捆绑和缩小

捆绑允许您将单个 JavaScript 和 CSS 文件合并到可以视为单个文件的捆绑包中。 Min化通过删除空白和其他不需要的字符来压缩 JavaScript 和 CSS 文件。 这些功能与 Web 窗体、ASP.NET MVC 和网页配合使用。

捆绑包是使用捆绑类或其子类之一的脚本捆绑包和样式捆绑包创建的。 配置捆绑包的实例后，只需将其添加到全局捆绑收集实例，即可向传入请求提供该捆绑包。 在默认模板中，捆绑配置在 Bundle Config 文件中执行。 此默认配置为模板使用的所有核心脚本和 css 文件创建捆绑包。

通过使用几个可能的帮助方法之一，从视图中引用捆绑包。 为了支持在调试与发布模式下呈现捆绑包的不同标记，ScriptBundle 和 StyleBundle 类具有帮助器方法 Render。 在调试模式下，渲染将为捆绑包中的每个资源生成标记。 在发布模式下，渲染将为整个捆绑包生成单个标记元素。 通过修改 Web.config 中编译元素的调试属性，可以在调试和发布模式之间切换，如下所示：

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample12.xml)]

此外，可以直接通过 BundleTable 设置启用或禁用优化。

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample13.cs)]

当文件捆绑时，它们首先按字母顺序排序（它们在**解决方案资源管理器**中显示的方式）。 然后组织它们，以便首先加载已知的库及其自定义扩展（如 jQuery、MooTools 和 Dojo）。 例如，如上所述，捆绑脚本文件夹的最终顺序为：

1. jquery-1.6.2.js
2. jquery-ui.js
3. jquery.tools.js
4. a.js

CSS 文件也按字母顺序排序，然后重新组织，以便重置.css 和规范化.css 在任何其他文件之前出现。 上面显示的样式文件夹捆绑的最终排序是：

1. 重置.css
2. 内容.css
3. 窗体.css
4. globals.css
5. 菜单.css
6. 样式.css

<a id="_Toc_perf"></a>
### <a name="performance-improvements-for-web-hosting"></a>Web 托管的性能改进

.NET 框架 4.5 和 Windows 8 引入了可帮助您为 Web 服务器工作负载实现显著性能提升的功能。 这包括减少（高达 35%）在启动时间和使用ASP.NET的网站托管站点的内存占用量中。

<a id="_Toc_perf_1"></a>
#### <a name="key-performance-factors"></a>关键性能因素

理想情况下，所有网站都应处于活动状态且处于内存中，以确保随时对下一个请求做出快速响应。 可能影响站点响应能力的因素包括：

- 应用池回收后站点重新启动所需的时间。 当站点程序集不再在内存中时，此时需要启动站点的 Web 服务器进程。 （平台程序集仍在内存中，因为它们被其他站点使用。这种情况称为"冷站点，暖框架启动"或只是"冷站点启动"。
- 站点占用的内存量。 其术语是"每个站点内存消耗"或"非共享工作集"。

新的性能改进侧重于这两个因素。

<a id="_Toc_perf_2"></a>
#### <a name="requirements-for-new-performance-features"></a>对新性能功能的要求

新功能的要求可以分为以下几类：

- 在 .NET 框架 4 上运行的改进。
- 需要 .NET 框架 4.5 但可在任何版本的 Windows 上运行的改进。
- 仅在 Windows 8 上运行 .NET 框架 4.5 时可用的改进。

性能随您能够启用的每个改进级别而提高。

一些 .NET Framework 4.5 改进还利用了适用于其他方案的更广泛的性能功能。

<a id="_Toc_perf_3"></a>
#### <a name="sharing-common-assemblies"></a>共享公共程序集

**要求**： .NET 框架 4 和可视化工作室 11 开发人员预览 SDK

服务器上的不同站点通常使用相同的帮助器程序集（例如，来自初学者工具包或示例应用程序的程序集）。 每个站点在其 Bin 目录中都有自己的程序集副本。 即使程序集的对象代码相同，但它们是物理上独立的程序集，因此在冷站点启动期间必须单独读取每个程序集，并单独保存在内存中。

新的实习功能解决了这种低效率，减少了 RAM 要求和加载时间。 使用允许 Windows 在文件系统中保留每个程序集的单个副本，站点 Bin 文件夹中的各个程序集将替换为指向单个副本的符号链接。 如果单个站点需要程序集的不同版本，则符号链接将被程序集的新版本替换，并且只有该站点受到影响。

使用符号链接共享程序集需要一个名为 aspnet\_intern.exe 的新工具，该工具允许您创建和管理已处理程序集的存储。 它是作为可视化工作室 11 开发人员预览 SDK 的一部分提供的。 （但是，假定已安装最新的[更新](https://support.microsoft.com/kb/2468871)，它将在仅安装 .NET 框架 4 的系统上工作。

为了确保所有符合条件的程序集都已暂留，您定期运行 aspnet\_intern.exe（例如，每周一次作为计划任务）。 典型用途如下：

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample14.cmd)]

要查看所有选项，运行没有参数的工具。

<a id="_Toc_perf_4"></a>
#### <a name="using-multi-core-jit-compilation-for-faster-startup"></a>使用多核 JIT 编译，加快启动速度

**要求**： .NET 框架 4.5

对于冷站点启动，不仅必须从磁盘读取程序集，而且必须编译站点。 对于复杂的站点，这可能会增加明显的延迟。 .NET Framework 4.5 中的一种新的通用技术通过在可用的处理器内核中扩展 JIT 编译来减少这些延迟。 它通过使用在以前发布网站期间收集的信息，尽可能早地这样做。 此功能由[系统.运行时.配置文件优化.启动配置文件](https://msdn.microsoft.com/library/system.runtime.profileoptimization.startprofile(VS.110).aspx)方法实现。

默认情况下，使用多个内核进行 JIT 编译ASP.NET，因此您无需执行任何操作来利用此功能。 如果要禁用此功能，请在 Web.config 文件中进行以下设置：

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample15.xml)]

<a id="_Toc_perf_5"></a>
#### <a name="tuning-garbage-collection-to-optimize-for-memory"></a>调整垃圾回收以优化内存

**要求**： .NET 框架 4.5

站点运行后，其使用垃圾回收器 （GC） 堆可能是其内存消耗的重要因素。 与任何垃圾回收器一样，.NET 框架 GC 在 CPU 时间（集合的频率和重要性）和内存消耗（用于新、释放或自由的对象的额外空间）之间进行权衡。 对于以前的版本，我们提供了有关如何配置 GC 以实现适当平衡的指导（例如，请参阅[ASP.NET 2.0/3.5 共享主机配置](https://www.iis.net/learn/web-hosting/web-server-for-shared-hosting/aspnet-20-35-shared-hosting-configuration)）。

对于 .NET Framework 4.5，提供工作负载定义的配置设置，该设置支持以前建议的所有 GC 设置以及为每个站点工作集提供额外性能的新调优。

要启用 GC 内存调优，请向 Windows_Microsoft.NET_Framework_v4.0.30319_aspnet.config 文件添加以下设置：

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample16.xml)]

（如果您熟悉之前对 aspnet.config 的更改指南，请注意此设置将替换旧设置，例如，无需设置 gcServer、gc并发等。您不必删除旧设置。

<a id="_Toc_perf_6"></a>
#### <a name="prefetching-for-web-applications"></a>为 Web 应用程序预取

**要求**： .NET 框架 4.5 在 Windows 8 上运行

对于多个版本，Windows 包含一种称为[预取器](http://en.wikipedia.org/wiki/Prefetcher)的技术，可降低应用程序启动的磁盘读取成本。 由于冷启动主要针对客户端应用程序，因此此技术未包含在 Windows Server 中，该服务器仅包含对服务器至关重要的组件。 预取现已在最新版本的 Windows Server 中提供，它可以优化单个网站的启动。

对于 Windows 服务器，默认情况下未启用预取器。 要启用和配置高密度 Web 托管的预取器，请在命令行上运行以下命令集：

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample17.cmd)]

然后，要将预取器与ASP.NET应用程序集成，请向 Web.config 文件添加以下内容：

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample18.xml)]

<a id="_Toc318097385"></a>
## <a name="aspnet-web-forms"></a>ASP.NET Web 窗体

<a id="_Toc318097386"></a>
### <a name="strongly-typed-data-controls"></a>强类型化数据控件

在 ASP.NET 4.5 中，Web 窗体包括一些用于处理数据的改进。 第一个改进是强类型数据控制。 对于早期版本的 ASP.NET 中的 Web 窗体控件，使用*Eval*和数据绑定表达式显示数据绑定值：

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample19.aspx)]

对于双向数据绑定，请使用*绑定*：

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample20.aspx)]

在运行时，这些调用使用反射读取指定成员的值，然后在标记中显示结果。 此方法使数据与任意、未成形的数据绑定变得容易。

但是，像这样的数据绑定表达式不支持诸如成员名称的 IntelliSense、导航（如转到定义）或对这些名称的编译时间检查等功能。

为了解决此问题，ASP.NET 4.5 添加了声明控件绑定到的数据的数据类型的能力。 使用新的*ItemType*属性执行此操作。 设置此属性时，数据绑定表达式的作用域中有两个新的类型变量 *：Item*和*BindItem*。 由于变量是强类型，因此您可以获得 Visual Studio 开发体验的全部优势。

对于双向数据绑定表达式，请使用*BindItem*变量：

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample21.aspx)]

ASP.NET Web 窗体框架中支持数据绑定的大多数控件都已更新以支持*ItemType*属性。

<a id="_Toc318097387"></a>
### <a name="model-binding"></a>模型绑定

模型绑定扩展了ASP.NET Web 窗体控件中的数据绑定，以便使用以代码为中心的数据访问。 它包含*了 ObjectDataSource*控件和模型绑定中的概念ASP.NET MVC。

<a id="_Toc318097388"></a>
#### <a name="selecting-data"></a>选择数据

要将数据控件配置为使用模型绑定来选择数据，请将控件的*SelectMethod*属性设置为页面代码中的方法的名称。 数据控件在页面生命周期中的适当时间调用该方法，并自动绑定返回的数据。 无需显式调用*DataBind*方法。

在下面的示例中 *，GridView*控件配置为使用名为*GetCategories*的方法 ：

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample22.aspx)]

在页面的代码中创建*GetCategories*方法。 对于简单的选择操作，该方法不需要任何参数，并且应返回*IE50 或* *IQuery 对象*。 如果设置了新的*ItemType*属性（启用强类型数据绑定表达式，如前面在[强类型数据控件](#_Toc318097386)中所述），则应返回这些接口的泛型版本 - *IE5500t&lt;&gt;* 或*IQuery&lt;&gt;T，T**参数匹配* *ItemType*属性的类型（例如 *，IQuery&lt;类别&gt;*）。

下面的示例显示了*GetCategories*方法的代码。 本示例使用实体框架代码第一模型与北风示例数据库。 代码确保查询通过 *"包括"* 方法返回每个类别的相关产品的详细信息。 （这可确保标记中的*模板字段*元素显示每个类别中的产品计数，而无需[n+1 选择](http://stackoverflow.com/questions/97197/what-is-the-n1-selects-problem).）

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample23.cs)]

当页面运行时 *，GridView*控件会自动调用*GetCategories*方法，并使用配置的字段呈现返回的数据：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image2.png)

由于选择方法返回*IQuery 对象*，因此*GridView*控件可以在执行查询之前进一步操作查询。 例如 *，GridView*控件可以在执行返回*的 IQuery 对象*之前将用于排序和分页的查询表达式添加到返回的 IQuery 对象，以便这些操作由基础 LINQ 提供程序执行。 在这种情况下，实体框架将确保在数据库中执行这些操作。

下面的示例显示已修改的*GridView*控件以允许排序和分页：

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample24.aspx)]

现在，当页面运行时，控件可以确保只显示当前数据页，并且数据按所选列排序：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image3.png)

要筛选返回的数据，必须将参数添加到选择方法。 这些参数将在运行时由模型绑定填充，您可以在返回数据之前使用它们来更改查询。

例如，假设您要通过在查询字符串中输入关键字来允许用户筛选产品。 您可以将参数添加到 方法并更新代码以使用参数值：

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample25.cs)]

如果为*关键字*提供了值，然后返回查询结果，则此代码包括*Where*表达式。

<a id="_Toc318097389"></a>
#### <a name="value-providers"></a>价值提供者

前面的示例没有具体说明*关键字*参数的值来自何处。 要指示此信息，可以使用参数属性。 在此示例中，可以使用*System.Web.Model 绑定*命名空间中的*QueryStringattribute*类：

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample26.cs)]

这指示模型绑定尝试在运行时将值从查询字符串绑定到*关键字*参数。 （这可能涉及执行类型转换，尽管在这种情况下不执行。如果无法提供值且类型不可为空，则引发异常。

这些方法的值源称为值提供程序，指示要使用的值提供程序的参数属性称为值提供程序属性。 Web 窗体将包括 Web 窗体应用程序中所有典型用户输入源的值提供程序和相应属性，例如查询字符串、Cookie、窗体值、控件、视图状态、会话状态和配置文件属性。 您还可以编写自定义值提供程序。

默认情况下，参数名称用作在值提供程序集合中查找值的键。 在此示例中，代码将查找名为关键字的查询字符串值（例如，*/default.aspx？关键字_chef）。 可以通过将自定义键作为参数传递给参数属性来指定它。 例如，要使用名为 q 的查询字符串变量的值，可以执行此操作：

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample27.cs)]

如果此方法位于页面的代码中，用户可以通过使用查询字符串传递关键字来筛选结果：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image4.png)

模型绑定完成许多任务，否则您必须手动编写代码：读取值、检查空值、尝试将其转换为适当的类型、检查转换是否成功，最后使用查询中的值。 模型绑定导致的代码少得多，并且能够在整个应用程序中重用该功能。

<a id="_Toc318097390"></a>
#### <a name="filtering-by-values-from-a-control"></a>按控件的值筛选

假设您要扩展示例，以便用户从下拉列表中选择筛选器值。 将以下下拉列表添加到标记中，并将其配置为使用*SelectMethod*属性从其他方法获取其数据：

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample28.aspx)]

通常，您还会向*GridView*控件添加*EmptyDataTemplate*元素，以便在找不到匹配的产品时，控件将显示一条消息：

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample29.aspx)]

在页面代码中，为下拉列表添加新的 select 方法：

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample30.cs)]

最后，更新*GetProducts*选择方法，从下拉列表中获取包含所选类别 ID 的新参数：

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample31.cs)]

现在，当页面运行时，用户可以从下拉列表中选择一个类别，并且*GridView*控件将自动重新绑定以显示筛选的数据。 这是可能的，因为模型绑定跟踪选定方法的参数值，并检测任何参数值在回退后是否已更改。 如果是这样，模型绑定强制关联的数据控件重新绑定到数据。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image5.png)

<a id="_Toc318097391"></a>
### <a name="html-encoded-data-binding-expressions"></a>HTML 编码数据绑定表达式

现在，您可以对数据绑定表达式的结果进行 HTML 编码。 添加冒号（:)标记数据绑定表达式的&lt;%# 前缀的末尾：

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample32.aspx)]

<a id="_Toc318097392"></a>
### <a name="unobtrusive-validation"></a>不显眼的验证

现在，您可以将内置验证器控件配置为对客户端验证逻辑使用不显眼的 JavaScript。 这大大减少了页面标记中内联呈现的 JavaScript 量，并减小了整个页面大小。 您可以通过以下任何方式为验证器控件配置不显眼的 JavaScript：

- 通过向 Web.config 文件中*&lt;的应用&gt;设置*元素添加以下设置，从而全局： 

    [!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample33.xml)]
- 通过将静态*System.Web.UI.验证设置.无显眼验证模式*属性设置为 *"无显眼验证模式.WebForms"（* 通常在 Global.asax 文件中*的应用程序\_启动*方法中），在全球范围内。
- 通过将页面类的新 *"不显眼验证模式"* 属性设置为 *"不显眼验证模式.WebForms"，* 单独为*页面*。

<a id="_Toc318097393"></a>
### <a name="html5-updates"></a>HTML5 更新

为了利用 HTML5 的新功能，对 Web 窗体服务器控件进行了一些改进：

- *TextBox*控件的*TextMode*属性已更新以支持新的 HTML5 输入类型，如*电子邮件*、*日期时间*等。
- *FileUpload*控件现在支持从支持此 HTML5 功能的浏览器上载多个文件。
- 验证器控件现在支持验证 HTML5 输入元素。
- 具有表示 URL 属性的新 HTML5 元素现在支持 runat_"server"。 因此，您可以在 URL 路径中使用ASP.NET约定，例如 * 运算符来表示应用程序根（例如，&lt;视频 runat_"服务器"src_"/myVideo.wmv"/&gt;）。
- *UpdatePanel*控件已修复，以支持过帐 HTML5 输入字段。

<a id="_Toc318097394"></a>
## <a name="aspnet-mvc-4"></a>ASP.NET MVC 4

ASP.NET MVC 4 测试版现在包含在 Visual Studio 11 测试版中。 ASP.NET MVC 是利用模型视图控制器 （MVC） 模式开发高度可测试和可维护的 Web 应用程序的框架。 ASP.NET MVC 4 使构建移动 Web 应用程序变得容易，并且包括ASP.NET Web API，这有助于构建可覆盖任何设备的 HTTP 服务。 有关详细信息，请参阅 ASP.NET [MVC 4 发行说明](mvc4-release-notes.md)。

<a id="_Toc318097395"></a>
## <a name="aspnet-web-pages-2"></a>ASP.NET 网页 2

新功能包括以下内容：

- 新建和更新的网站模板。
- 使用*验证*帮助程序添加服务器端和客户端验证。
- 使用资产管理注册脚本的功能。
- 使用 OAuth 和 OpenID 启用来自 Facebook 和其他网站的登录。
- 使用地图帮助器添加*地图*。
- 并排运行网页应用程序。
- 移动设备的呈现页面。

有关这些功能和整页代码示例的详细信息，请参阅[网页 2 Beta 中的顶部功能](https://go.microsoft.com/fwlink/?LinkID=227824)。

<a id="_Toc318097396"></a>
## <a name="visual-web-developer-11-beta"></a>可视化 Web 开发人员 11 测试版

本节提供有关可视化 Web 开发人员 11 Beta 和可视化工作室 2012 版本候选版中 Web 开发改进的信息。

<a id="project-compatibility"></a>
### <a name="project-sharing-between-visual-studio-2010-and-visual-studio-2012-release-candidate-project-compatibility"></a>Visual Studio 2010 和 Visual Studio 2012 版本候选版本之间的项目共享（项目兼容性）

在 Visual Studio 2012 发布候选版之前，在较新版本的 Visual Studio 中打开现有项目启动了转换向导。 这迫使项目的内容（资产）和解决方案升级到不向后兼容的新格式。 因此，转换后，您无法在旧版本的 Visual Studio 中打开项目。

许多客户告诉我们，这不是正确的方法。 在 Visual Studio 11 Beta 中，我们现在支持与 Visual Studio 2010 SP1 共享项目和解决方案。 这意味着，如果您在 Visual Studio 2012 版本候选版中打开 2010 年项目，您仍然可以在 Visual Studio 2010 SP1 中打开该项目。

> [!NOTE]
> 几种类型的项目不能在 Visual Studio 2010 SP1 和 Visual Studio 2012 版本候选版之间共享。 其中包括一些较旧的项目（如ASP.NET MVC 2 项目）或用于特殊目的的项目（如安装程序项目）。

首次在 Visual Studio 11 Beta 中打开 Visual Studio 2010 SP1 Web 项目时，以下属性将添加到项目文件中：

- 文件升级标志
- 升级备份位置
- 旧工具版本
- VisualStudioVersion
- VSToolsPath

文件升级标志、升级备份位置和旧工具版本由升级项目文件的过程使用。 它们对在 Visual Studio 2010 中使用该项目没有任何影响。

VisualStudioVersion 是 MSBuild 4.5 使用的新属性，用于指示当前项目的 Visual Studio 版本。 由于此属性在 MSBuild 4.0 中不存在（Visual Studio 2010 SP1 使用的 MSBuild 版本），因此我们将默认值注入到项目文件中。

VSToolsPath 属性用于确定要从 MSBuild 扩展器Path32 设置表示的路径导入的正确 .target 文件。

还有一些与导入元素相关的更改。 为了支持两个版本的 Visual Studio 之间的兼容性，需要进行这些更改。

> [!NOTE]
> 如果 Visual Studio 2010 SP1 和 Visual Studio 11 Beta 在两台不同计算机上共享项目，并且该项目在应用\_数据文件夹中包含本地数据库，则必须确保数据库使用的 SQL Server 版本安装在两台计算机上。

<a id="Configuration_Changes_In_ASPNET45_Website_Templates"></a>
### <a name="configuration-changes-in-aspnet-45-website-templates"></a>ASP.NET 4.5 网站模板中的配置更改

对使用 Visual Studio 2012 版本候选版中的网站模板创建的网站的默认*Web.config*文件进行了以下更改：

- 在元素`<httpRuntime>`中，`encoderType`属性现在默认设置为使用添加到ASP.NET的 AntiXSS 类型。 有关详细信息，请参阅[AntiXSS 库](#_Toc318097382)。
- 此外，在`<httpRuntime>`元素中，`requestValidationMode`属性设置为"4.5"。 这意味着默认情况下，请求验证配置为使用延迟（"延迟"）验证。 有关详细信息，请参阅[新ASP.NET请求验证功能](#_Toc318097379)。
- 节`<modules>`的元素`<system.webServer>`不包含属性`runAllManagedModulesForAllRequests`。 （其默认值为 false。这意味着，如果您使用的 IIS 7 版本尚未更新到 SP1，则新站点中的路由可能有问题。 有关详细信息，请参阅[IIS 7 中的本机支持，了解ASP.NET路由](#Native_Support_In_IIS7_For_ASPNET_Routine)。

这些更改不会影响现有应用程序。 但是，它们可能表示现有网站与您使用新模板为 ASP.NET 4.5 创建的新网站的行为差异。

<a id="Native_Support_In_IIS7_For_ASPNET_Routine"></a>
### <a name="native-support-in-iis-7-for-aspnet-routing"></a>IIS 7 中用于ASP.NET路由的本机支持

这不是对ASP.NET的更改，而是新网站项目的模板更改，如果您正在使用未应用 SP1 更新的 IIS 7 版本，可能会影响您。

在ASP.NET中，您可以将以下配置设置添加到应用程序中，以支持路由：

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample34.xml?highlight=3)]

当**RunAll管理ModuleAll请求**为 true 时，`http://mysite/myapp/home`即使 URL 上没有 *.aspx、.mvc*或类似扩展，也可以将类似 URL 转到ASP.NET。 *.mvc*

对 IIS 7 所做的更新使**runAll管理模块所有请求**设置变得不必要，并支持本机路由ASP.NET路由。 （有关更新的信息，请参阅 Microsoft 支持文章[一个可用更新，使某些 IIS 7.0 或 IIS 7.5 处理程序能够处理 URL 未以句点结尾的请求](https://support.microsoft.com/kb/980368)。

如果您的网站在 IIS 7 上运行，并且 IIS 已更新，则无需将**运行All管理模块全部请求**设置为 true。 事实上，不建议将其设置为 true，因为它会增加不必要的处理开销。 当此设置为 true 时，所有请求（包括 *.htm、.jpg*和其他静态文件的请求）也会通过请求管道ASP.NET。 *.jpg*

如果使用 Visual Studio 2012 RC 中提供的模板创建新ASP.NET 4.5 网站，则网站的配置不包括**RunAll管理模块全部请求**设置。 这意味着默认情况下，该设置为 false。

如果随后在 Windows 7 上运行网站而不安装 SP1，则 IIS 7 将不包含所需的更新。 因此，路由将不起作用，您将看到错误。 如果路由不起作用，可以执行以下任一操作：

- 将 Windows 7 更新为 SP1，这将将更新添加到 IIS 7。
- 安装前面列出的 Microsoft 支持文章中所述的更新。
- 将**运行All管理模块所有请求**设置为 true，在该网站的 Web.config 文件中。 请注意，这将为请求增加一些开销。

<a id="_Toc318097397"></a>
### <a name="html-editor"></a>HTML 编辑器

<a id="_Toc318097398"></a>
#### <a name="smart-tasks"></a>智能任务

在"设计"视图中，服务器控件的复杂属性通常具有关联的对话框和向导，以便轻松设置它们。 例如，可以使用特殊的对话框向*中继器*控件添加数据源或向*GridView*控件添加列。

但是，针对复杂属性的这种类型的 UI 帮助在源视图中不可用。 因此，Visual Studio 11 引入了源视图的智能任务。 智能任务是 C# 和 Visual Basic 编辑器中常用功能的上下文感知快捷方式。

对于ASP.NET Web 窗体控件，当插入点位于元素内部时，智能任务在服务器标记上显示为一个小字形：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image6.png)

单击字形或按 CTRL+时，智能任务将展开。 （点），就像代码编辑器一样。 然后，它显示类似于"设计"视图中的智能任务的快捷方式。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image7.png)

例如，上图中的智能任务显示了 GridView 任务选项。 如果选择"编辑列"，将显示以下对话框：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image8.png)

填写对话框将设置可在"设计"视图中设置的相同属性。 单击"确定"时，控件的标记将使用新设置更新：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image9.png)

<a id="_Toc318097399"></a>
#### <a name="wai-aria-support"></a>WAI-ARIA 支持

编写可访问的网站变得越来越重要。 [WAI-ARIA 辅助功能标准](http://www.w3.org/WAI/intro/aria)定义了开发人员应如何编写可访问的网站。 此标准现在完全支持在视觉工作室。

例如，*角色*属性现在具有完整的 IntelliSense：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image10.png)

WAI-ARIA 标准还引入了以*aria-* 预缀的属性，这些属性允许您向 HTML5 文档添加语义。 Visual Studio 还完全支持这些*aria 属性*：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image11.png) ![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image12.png)

<a id="_Toc318097400"></a>
#### <a name="new-html5-snippets"></a>新的 HTML5 代码段

为了使编写常用的 HTML5 标记更快、更容易，Visual Studio 包含许多代码段。 例如视频片段：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image13.png)

要调用代码段，请在 IntelliSense 中选择元素时按 Tab 两次：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image14.png)

这将生成可以自定义的代码段。

<a id="_Toc318097401"></a>
#### <a name="extract-to-user-control"></a>提取到用户控件

在大型网页中，最好将单个片段移动到用户控件中。 这种重构形式有助于提高页面的可读性，并可以简化页面结构。

为了简化此功能，当您在"源"视图中编辑"Web 窗体"页时，您现在可以选择页面中的文本，右键单击它，然后选择"提取到用户控制"：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image2.jpg)

<a id="_Toc318097402"></a>
#### <a name="intellisense-for-code-nuggets-in-attributes"></a>属性中代码块的 IntelliSense

Visual Studio 始终为任何页面或控件中的服务器端代码块提供 IntelliSense。 现在，Visual Studio 还包括用于 HTML 属性中的代码块的 IntelliSense。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image15.png)

这样可以更轻松地创建数据绑定表达式：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image16.png)

<a id="_Toc318097403"></a>
#### <a name="automatic-renaming-of-matching-tag-when-you-rename-an-opening-or-closing-tag"></a>重命名打开或关闭标记时自动重命名匹配标记

如果重命名 HTML 元素（例如，将*div*标记更改为*标头*标记），相应的打开或关闭标记也会实时更改。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image17.png)

这有助于避免忘记更改结束标记或更改错误标记的错误。

<a id="_Toc318097404"></a>
#### <a name="event-handler-generation"></a>事件处理程序生成

Visual Studio 现在包括在"源"视图中的功能，以帮助您编写事件处理程序并手动绑定它们。 如果要在源视图中编辑事件名称，IntelliSense 将显示&lt;"创建新事件&gt;"，这将在具有正确签名的页面代码中创建事件处理程序：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image3.jpg)

默认情况下，事件处理程序将使用控件的 ID 来表示事件处理方法的名称：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image4.jpg)

生成的事件处理程序将如下所示（在本例中，在 C#中）：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image18.png)

<a id="_Toc318097405"></a>
#### <a name="smart-indent"></a>智能缩进

当您在空的 HTML 元素内按 Enter 时，编辑器将插入点放在正确的位置：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image19.png)

如果在此位置按 Enter，则关闭标记将向下移动并缩进以匹配打开标记。 插入点也缩进：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image20.png)

<a id="_Toc318097406"></a>
#### <a name="auto-reduce-statement-completion"></a>自动减少语句完成

Visual Studio 中的 IntelliSense 列表现在根据您键入的内容进行筛选，以便仅显示相关选项：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image21.png)

IntelliSense 还会根据 IntelliSense 列表中单个单词的标题大小写进行筛选。 例如，如果您键入"dl"，则将显示 dl 和 asp：DataList：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image22.png)

此功能使获取已知元素的语句完成速度更快。

<a id="_Toc318097407"></a>
### <a name="javascript-editor"></a>JavaScript 编辑器

Visual Studio 2012 版本候选版中的 JavaScript 编辑器是全新的，它极大地改善了在可视化工作室中使用 JavaScript 的体验。

<a id="_Toc318097408"></a>
#### <a name="code-outlining"></a>代码大纲显示

现在会自动为所有函数创建大纲区域，从而可以折叠与当前焦点无关的文件部分。

<a id="_Toc318097409"></a>
#### <a name="brace-matching"></a>大括号匹配

将插入点放在开括号或关闭大括号上时，编辑器将突出显示匹配的支撑。

<a id="_Toc318097410"></a>
#### <a name="go-to-definition"></a>转到定义

"转到定义"命令允许您跳转到函数或变量的源。

<a id="_Toc318097411"></a>
#### <a name="ecmascript5-support"></a>ECMAScript5 支持

编辑器支持 ECMAScript5 中的新语法和 API，ECMAScript5 是描述 JavaScript 语言的标准的最新版本。

<a id="_Toc318097412"></a>
#### <a name="dom-intellisense"></a>DOM 感知

DOM API 的智能感知得到了改进，支持许多新的 HTML5 API，包括*查询选择器*、DOM 存储、跨文档消息传递和*画布*。 DOM IntelliSense 现在由单个简单的 JavaScript 文件驱动，而不是由本机类型库定义驱动。 这使得扩展或更换变得容易。

<a id="_Toc318097413"></a>
#### <a name="vsdoc-signature-overloads"></a>VSDOC 签名重载

现在可以使用新的*&lt;签名&gt;* 元素声明详细的 IntelliSense 注释，以便单独重载 JavaScript 函数，如以下示例所示：

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample35.cs)]

<a id="_Toc318097414"></a>
#### <a name="implicit-references"></a>隐式引用

现在，您可以将 JavaScript 文件添加到一个中心列表中，该列表将隐式包含在任何给定的 JavaScript 文件或阻止引用的文件列表中，这意味着您将获得 IntelliSense 的内容。 例如，您可以将 jQuery 文件添加到文件的中心列表中，并且无论是否已显式引用它（使用 // /&lt;引用 /），&gt;您都将在任何 JavaScript 文件块中获取 jQuery 函数的 IntelliSense。

<a id="_Toc318097415"></a>
### <a name="css-editor"></a>CSS 编辑器

<a id="_Toc318097416"></a>
#### <a name="auto-reduce-statement-completion"></a>自动减少语句完成

CSS 的 IntelliSense 列表现在根据所选架构支持的 CSS 属性和值进行筛选。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image23.png)

IntelliSense 还支持标题案例搜索：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image24.png)

<a id="_Toc318097417"></a>
#### <a name="hierarchical-indentation"></a>分层缩进

CSS 编辑器使用缩进来显示分层规则，这为您提供了级联规则逻辑组织方式的概述。 在下面的示例中，选择器#list是列表的级联子级，因此缩进。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image25.png)

下面的示例显示了更复杂的继承：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image26.png)

规则的缩进由其父规则决定。 默认情况下启用分层缩进，但您可以禁用"选项"对话框（菜单栏中的工具、选项）：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image27.png)

<a id="_Toc318097418"></a>
#### <a name="css-hacks-support"></a>CSS 黑客支持

对数百个真实 CSS 文件的分析表明，CSS 黑客非常常见，现在 Visual Studio 支持使用最广泛的黑客。 这种支持包括IntelliSense和验证的明星 （\*） 和下\_划线 （ ） 属性黑客：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image28.png)

还支持典型的选择器黑客，以便即使应用分层缩进，也能保持分层缩进。 一个典型的选择器黑客用于目标互联网浏览器7是准备一个选择器与*\*：第一个孩子 + html*。 使用该规则将保持分层缩进：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image29.png)

<a id="_Toc318097419"></a>
#### <a name="vendor-specific-schemas--moz---webkit"></a>供应商特定的架构（-moz-, -webkit）

CSS3 引入了许多由不同浏览器在不同时间实现的属性。 这以前迫使开发人员使用特定于供应商的语法为特定浏览器编写代码。 这些特定于浏览器的属性现在包含在 IntelliSense 中。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image30.png)

<a id="_Toc318097420"></a>
#### <a name="commenting-and-uncommenting-support"></a>评论和非评论支持

现在，您可以使用代码编辑器中使用的快捷方式（Ctrl_K、C 注释和 Ctrl_K，您取消注释）对 CSS 规则进行注释和取消注释。

<a id="_Toc318097421"></a>
#### <a name="color-picker"></a>颜色选取器

在早期版本的 Visual Studio 中，与颜色相关的属性的 IntelliSense 由命名颜色值的下拉列表组成。 该列表已被全功能颜色选取器替换。

输入颜色值时，颜色选取器将自动显示，并显示以前使用的颜色列表，后跟默认调色板。 您可以使用鼠标或键盘选择颜色。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image31.png)

该列表可以展开为完整的颜色选取器。 选取器允许您在移动不协调性滑块时自动将任何颜色转换为 RGBA 来控制 Alpha 通道：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image32.png)

<a id="_Toc318097422"></a>
#### <a name="snippets"></a>代码片段

CSS 编辑器中的代码段使创建跨浏览器样式变得更加简单和快速。 许多需要特定于浏览器设置的 CSS3 属性现已滚入代码段。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image33.png)

CSS 代码段通过键入在符号 （#） 中显示 IntelliSense 列表来支持高级方案（如 CSS3 媒体查询）。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image34.png)

当您选择@media值并按选项卡时，CSS 编辑器将插入以下代码段：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image5.jpg)

与代码代码段一样，您可以创建自己的 CSS 代码段。

<a id="_Toc318097423"></a>
#### <a name="custom-regions"></a>自定义区域

命名代码区域（已在代码编辑器中提供）现在可用于 CSS 编辑。 这使您可以轻松对相关的样式块进行分组。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image35.png)

当区域折叠时，将显示区域的名称：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image36.png)

<a id="_Toc318097424"></a>
### <a name="page-inspector"></a>Page Inspector

页面检查器是一种工具，用于在 Visual Studio IDE 中呈现网页（HTML、Web 窗体、ASP.NET MVC 或网页），并允许您检查源代码和生成的输出。 对于ASP.NET页，页面检查器允许您确定哪些服务器端代码已生成呈现到浏览器的 HTML 标记。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image37.png)

有关页面检查器的详细信息，请参阅以下教程：

- 在[mVC 中使用ASP.NET](../mvc/overview/views/using-page-inspector-in-aspnet-mvc.md)页检查器
- 在[ASP.NET Web 窗体](../web-forms/overview/getting-started/using-page-inspector-in-a-visual-studio-11-beta-web-forms-project.md)中使用页面检查器

<a id="_Toc318097425"></a>
### <a name="publishing"></a>发布

<a id="_Toc318097426"></a>
#### <a name="publish-profiles"></a>发布配置文件

在 Visual Studio 2010 中，Web 应用程序项目的发布信息不存储在版本控制中，并且不设计为与他人共享。 在 Visual Studio 2012 版本候选版中，发布配置文件的格式已更改。 它已成为团队工件，现在很容易从基于 MSBuild 的生成中利用。 生成配置信息位于"发布"对话框中，以便在发布之前轻松切换生成配置。

发布配置文件存储在"发布配置文件"文件夹中。 文件夹的位置取决于您使用的编程语言：

- C#：属性\发布配置文件
- 可视化基础知识：我的项目\发布配置文件

每个配置文件都是一个 MSBuild 文件。 在发布期间，此文件将导入到项目的 MSBuild 文件中。 在 Visual Studio 2010 中，如果要对发布或包过程进行更改，则必须将自定义项放在名为**ProjectName**.wpp.target 的文件中。 这仍然受支持，但现在可以将自定义项放在发布配置文件本身中。 这样，自定义将仅用于该配置文件。

您现在还可以利用 MSBuild 的发布配置文件。 为此，在生成项目时使用以下命令：

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample36.cmd)]

project.csproj 值是项目的路径，而配置文件名称是要发布的配置文件的名称。 或者，您可以传入发布配置文件的完整路径，而不是传递*PublishProfile*属性的配置文件名称。

<a id="_Toc318097427"></a>
#### <a name="aspnet-precompilation-and-merge"></a>ASP.NET预编译和合并

对于 Web 应用程序项目，Visual Studio 2012 发布候选版在"包/发布 Web 属性"页上添加了一个选项，允许您在发布或打包项目时预编译和合并网站的内容。 要查看这些选项，请右键单击解决方案资源管理器中的项目，选择"属性"，然后选择"包/发布 Web 属性页"。 下图显示了发布选项之前预编译此应用程序。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image6.jpg)

选择此选项后，每当发布或打包 Web 应用程序时，Visual Studio 都会预编译应用程序。 如果要控制站点的预编译方式或程序集的合并方式，请单击"高级"按钮以配置这些选项。

<a id="_Toc318097428"></a>
### <a name="iis-express"></a>IIS Express

用于在 Visual Studio 中测试 Web 项目的默认 Web 服务器现在是 IIS Express。 可视化工作室开发服务器仍然是开发过程中本地 Web 服务器的选项，但 IIS Express 现在是推荐的服务器。 在 Visual Studio 11 Beta 中使用 IIS Express 的经验与在 Visual Studio 2010 SP1 中使用它非常相似。

<a id="_Toc318097429"></a>
## <a name="disclaimer"></a>免责声明

这是一份初稿，并可能在本文所述软件最终商业发布之前进行大幅更改。

本文档中包含的信息代表 Microsoft Corporation 在发布之日对所讨论问题的当前观点。 由于 Microsoft 必须响应不断变化的市场条件，因此不应将其解释为 Microsoft 作出的承诺，并且 Microsoft 无法保证在发布日期之后提供的任何信息的准确性。

本白皮书仅用于提供信息。 MICROSOFT 对本文档中的信息不做任何明示、暗示或法定的担保。

用户有责任遵守所有适用的版权法/著作权法。 在不限制版权所辖权利的前提下，未经 Microsoft Corporation 的明确书面许可，本文档的任何部分不得被复制、存储或引进检索系统，或者以任何形式、任何方式（电子、机械、影印、录音等）或为任何目的进行传播。

Microsoft 可能拥有本文档所涵盖主题的专利、专利申请、商标、版权或其他知识产权。 除非 Microsoft 提供了明确的书面许可协议，否则提供本文档并不意味着赋予您这些专利、商标、版权或其他知识产权的任何许可。

除非另有说明，否则此处描述的示例公司、组织、产品、域名、电子邮件地址、徽标、人员、地点和事件均属虚构，且无意或不应推断与任何真实的公司、组织、产品、域名、电子邮件地址、徽标、人员、地点或事件有任何关联。

(C) 2012 Microsoft Corporation。 保留所有权利。

Microsoft 和 Windows 是 Microsoft Corporation 在美国和/或其他国家/地区的注册商标或商标。

此处提到的真实公司和产品的名称可能是其各自所有者的商标。

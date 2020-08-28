---
uid: web-forms/overview/performance-and-caching/using-asynchronous-methods-in-aspnet-45
title: 在 ASP.NET 4.5 中使用异步方法 |Microsoft Docs
author: Rick-Anderson
description: 本教程将教你使用 Visual Studio Express 2012 for Web 构建异步 ASP.NET Web 窗体应用程序的基础知识，这是一个免费的 .。。
ms.author: riande
ms.date: 01/02/2019
ms.assetid: a585c9a2-7c8e-478b-9706-90f3739c50d1
msc.legacyurl: /web-forms/overview/performance-and-caching/using-asynchronous-methods-in-aspnet-45
msc.type: authoredcontent
ms.openlocfilehash: a0aed792c5a2e790eed10c1aecf84fe5e535cea4
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045151"
---
# <a name="using-asynchronous-methods-in-aspnet-45"></a>在 ASP.NET 4.5 中使用异步方法

作者： [Rick Anderson](https://twitter.com/RickAndMSFT)

> 本教程将教你使用 [Visual Studio Express 2012 For Web](https://www.microsoft.com/visualstudio/11)构建异步 ASP.NET Web 窗体应用程序的基础知识，该应用程序是 Microsoft Visual Studio 的免费版本。 你还可以使用 [Visual Studio 2012](https://www.microsoft.com/visualstudio/11)。 本教程包含以下部分。
> 
> - [线程池处理请求的方式](#HowRequestsProcessedByTP)
> - [选择同步或异步方法](#ChoosingSyncVasync)
> - [示例应用程序](#SampleApp)
> - [Gizmos 同步页](#GizmosSynch)
> - [创建异步 Gizmos 页](#CreatingAsynchGizmos)
> - [并行执行多个操作](#Parallel)
> - [使用取消标记](#CancelToken)
> - [高并发/高延迟 Web 服务调用的服务器配置](#ServerConfig)
> 
> 本教程提供了一个完整的示例，网址为：  
> [https://github.com/RickAndMSFT/Async-ASP.NET/](https://github.com/RickAndMSFT/Async-ASP.NET/) 在 [GitHub](https://github.com/) 站点上。

[.Net 4.5](https://msdn.microsoft.com/library/w0x726c2(VS.110).aspx)中的 ASP.NET 4.5 网页使你能够注册返回类型为[Task](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx)的对象的异步方法。 .NET Framework 4 引入了一个称为 [任务](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) 的异步编程概念，ASP.NET 4.5 支持 [任务](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx)。 任务由[tasks 命名空间中的](https://msdn.microsoft.com/library/system.threading.tasks.aspx)**任务**类型和相关类型来表示。 .NET Framework 4.5 使用 [await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) 和 [async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) 关键字构建这一异步支持，这些关键字使得处理 [任务](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) 对象比以前的异步方法更复杂。 [Await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx)关键字是语法简写，指示代码段应以异步方式等待某个代码的其他部分。 [Async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx)关键字表示一个提示，可用于将方法标记为基于任务的异步方法。 **Await**、 **async**和**Task**对象的组合使你可以更轻松地在 .net 4.5 中编写异步代码。 异步方法的新模型称为 *基于任务的异步模式* (**点击**) 。 本教程假定你熟悉使用 [await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) 和 [Async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) 关键字以及 [任务](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) 命名空间的异步编程。

有关使用 [await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) 和 [Async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) 关键字以及 [任务](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) 命名空间的详细信息，请参阅以下参考。

- [白皮书： .NET 中的异步](https://go.microsoft.com/fwlink/?LinkId=204844)
- [Async/Await 常见问题](https://blogs.msdn.com/b/pfxteam/archive/2012/04/12/10293335.aspx)
- [Visual Studio 异步编程](https://msdn.microsoft.com/vstudio/gg316360)

## <a name="how-requests-are-processed-by-the-thread-pool"></a><a id="HowRequestsProcessedByTP"></a>  线程池如何处理请求

在 web 服务器上，.NET Framework 维护用于处理 ASP.NET 请求的线程池。 当请求到达时，将调度池中的线程以处理该请求。 如果以同步方式处理请求，则处理请求的线程将在处理请求时处于繁忙状态，并且该线程无法处理其他请求。   
  
这可能不是问题，因为线程池的大小足以容纳多个繁忙线程。 但是，线程池中的线程数受到限制 (.NET 4.5 的默认最大值为 5000) 。 在具有长时间运行的请求的高并发性的大型应用程序中，所有可用线程可能都处于繁忙状态。 这种情况称为“线程不足”。 达到此条件时，web 服务器会将请求排队。 如果请求队列已满，则 web 服务器将拒绝 HTTP 503 状态 (服务器太忙) 的请求。 CLR 线程池在新线程注入上具有限制。 如果并发是突发的 (也就是说，你的网站可能会突然获得大量请求) 并且所有可用请求线程都处于繁忙状态，因为后端调用的延迟较高，所以有限的线程注入率会使你的应用程序的响应速度非常差。 此外，添加到线程池的每个新线程都具有开销 (例如 1 MB 的堆栈内存) 。 使用同步方法对高延迟调用进行服务的 web 应用程序，其中线程池增长到 .NET 4.5 默认的最大值5，000线程会消耗大约 5 GB 的内存，而不是应用程序能够使用异步方法和仅50线程处理相同的请求。 执行异步工作时，不一定要使用线程。 例如，当你发出异步 web 服务请求时，ASP.NET 将不会在 **异步** 方法调用与 **await**之间使用任何线程。 使用线程池来处理具有较高延迟的请求可能会导致内存占用量较大，并且服务器硬件利用率不佳。

## <a name="processing-asynchronous-requests"></a>处理异步请求

在启动时可看到大量并发请求的 web 应用程序中，或具有突发负载 (（其中并发增长突然) ）时，使 web 服务调用异步会提高应用程序的响应能力。 异步请求与同步请求所需的处理时间相同。 例如，如果某个请求发出的 web 服务调用需要两秒钟才能完成，则该请求将需要两秒钟，无论是同步执行还是异步执行。 但是，在异步调用期间，线程在等待第一个请求完成时不会被阻止响应其他请求。 因此，当有多个并发请求调用长时间运行的操作时，异步请求会阻止请求队列和线程池的增长。

## <a name="choosing-synchronous-or-asynchronous-methods"></a><a id="ChoosingSyncVasync"></a>  选择同步或异步方法

本部分列出了使用同步或异步方法的相关准则。 这些只是指导原则;分别检查每个应用程序，以确定异步方法是否有助于提高性能。

通常，在下列情况下使用同步方法：

- 操作很简单或运行时间很短。
- 简单性比效率更重要。
- 此操作主要是 CPU 操作而不是包含大量的磁盘或网络开销的操作。 在占用 CPU 的操作上使用异步方法不会带来任何好处，并会导致更高的开销。

通常，在下列情况下使用异步方法：

- 正在调用可通过异步方法使用的服务，并且使用的是 .NET 4.5 或更高版本。
- 操作是网络绑定的或 I/O 绑定的而不是 CPU 绑定的。
- 并行性比代码的简单性更重要。
- 您希望提供一种可让用户取消长时间运行的请求的机制。
- 切换线程的优点超出了上下文切换的成本。 通常，如果同步方法在不执行任何操作的情况下阻止 ASP.NET 请求线程，则应使方法成为异步方法。 通过将调用设为异步，ASP.NET 请求线程在等待 web 服务请求完成时不会被阻止。
- 测试表明阻塞操作是站点性能瓶颈，而 IIS 可以通过对这些阻止调用使用异步方法来提供更多请求。

  可下载的示例演示如何有效地使用异步方法。 提供的示例旨在提供 ASP.NET 4.5 中异步编程的简单演示。 该示例不是 ASP.NET 中异步编程的参考体系结构。 该示例程序调用 [ASP.NET Web API](../../../web-api/index.md) 方法，这些方法进而调用 [任务。延迟](https://msdn.microsoft.com/library/hh139096(VS.110).aspx) 以模拟长时间运行的 Web 服务调用。 大多数生产应用程序将不会显示此类明显的使用异步方法的好处。   
  
一些应用程序要求所有方法都是异步的。 通常，将一些同步方法转换为异步方法可为所需工作量提高效率。

## <a name="the-sample-application"></a><a id="SampleApp"></a>  示例应用程序

你可以从 [https://github.com/RickAndMSFT/Async-ASP.NET](https://github.com/RickAndMSFT/Async-ASP.NET) [GitHub](https://github.com/) 站点上下载示例应用程序。 存储库由三个项目组成：

- *WebAppAsync*：使用 Web API **WebAPIpwg** 服务的 ASP.NET Web 窗体项目。 本教程的大部分代码都来自此项目。
- *WebAPIpgw*：用于实现控制器的 ASP.NET MVC 4 Web API 项目 `Products, Gizmos and Widgets` 。 它为 *WebAppAsync* 项目和 *Mvc4Async* 项目提供数据。
- *Mvc4Async*： ASP.NET MVC 4 项目，其中包含其他教程中使用的代码。 它使 Web API 调用 **WebAPIpwg** 服务。

## <a name="the-gizmos-synchronous-page"></a><a id="GizmosSynch"></a>  Gizmos 同步页

 下面的代码演示了 `Page_Load` 用于显示 gizmos 列表的同步方法。  (本文，别出心裁是虚构的机械设备。 )  

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample1.cs)]

以下代码显示了 `GetGizmos` 别出心裁服务的方法。

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample2.cs)]

`GizmoService GetGizmos`方法将 URI 传递给 ASP.NET WEB API HTTP 服务，该服务返回 gizmos 数据的列表。 *WebAPIpgw*项目包含 Web API `gizmos, widget` 和控制器的实现 `product` 。  
下图显示了示例项目中的 gizmos 页。

![Gizmos](using-asynchronous-methods-in-aspnet-45/_static/image1.png)

## <a name="creating-an-asynchronous-gizmos-page"></a><a id="CreatingAsynchGizmos"></a>  创建异步 Gizmos 页

该示例使用 .NET 4.5 和 Visual Studio 2012) 中的新的 [async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) 和 [await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) 关键字 (，让编译器负责维护异步编程所需的复杂转换。 编译器使你可以使用 c # 的同步控制流构造编写代码，并且编译器会自动应用使用回调所需的转换，以避免阻止线程。

ASP.NET 异步页必须包含[Page](https://msdn.microsoft.com/library/ydy4x04a.aspx) `Async` 属性设置为 "True" 的 Page 指令。 下面的代码显示[Page](https://msdn.microsoft.com/library/ydy4x04a.aspx) `Async` *GizmosAsync*页的特性设置为 "true" 的页指令。

[!code-aspx[Main](using-asynchronous-methods-in-aspnet-45/samples/sample3.aspx?highlight=1)]

以下代码显示了 `Gizmos` 同步 `Page_Load` 方法和 `GizmosAsync` 异步页面。 如果浏览器支持 [HTML 5 &lt; mark &gt; 元素](http://www.w3.org/wiki/HTML/Elements/mark)，则会看到 `GizmosAsync` 黄色突出显示中的更改。

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample4.cs)]

异步版本：

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample5.cs?highlight=3,6-7,9,11)]

 应用了以下更改，以允许 `GizmosAsync` 页面是异步的。

- [Page](https://msdn.microsoft.com/library/ydy4x04a.aspx)指令的 `Async` 特性必须设置为 "true"。
- `RegisterAsyncTask`方法用于注册包含异步运行的代码的异步任务。
- 新 `GetGizmosSvcAsync` 方法标记有 [async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) 关键字，该关键字告诉编译器为部分主体生成回调并自动创建 `Task` 返回的。
- &quot;&quot;异步方法名称后追加了 Async。 不需要追加 "Async"，但这是编写异步方法时的约定。
- 新方法的返回类型 `GetGizmosSvcAsync` 是 `Task` 。 的返回类型 `Task` 表示正在进行的工作，并为方法的调用方提供一个句柄，用于等待异步操作完成。
- [Await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx)关键字已应用于 web 服务调用。
- )  (调用了异步 web 服务 API `GetGizmosAsync` 。

在 `GetGizmosSvcAsync` 方法体内部，调用另一个异步方法 `GetGizmosAsync` 。 `GetGizmosAsync` 立即返回 `Task<List<Gizmo>>` 将在数据可用时最终完成的。 由于你不需要执行任何其他操作，直到有别出心裁数据，代码使用 **await** 关键字) 来等待任务 (。 只能在使用**async**关键字批注的方法中使用**await**关键字。

**等待**关键字不会阻止线程，直到任务完成。 它将方法的其余部分注册为任务的回调，并立即返回。 当等待的任务最终完成时，它将调用该回调，并因此在其中断时继续执行方法。 有关使用 [await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) 和 [Async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) 关键字以及 [任务](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) 命名空间的详细信息，请参阅 [async 引用](https://docs.microsoft.com/dotnet/csharp/language-reference/keywords/async)。

以下代码显示了 `GetGizmos` 和 `GetGizmosAsync` 方法。

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample6.cs)]

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample7.cs?highlight=1,4-8)]

 异步更改与上述 **GizmosAsync** 的更改类似。 

- 方法签名通过 [async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) 关键字进行批注，返回类型已更改为 `Task<List<Gizmo>>` ，而 *async* 追加到方法名称。
- 使用异步 [HttpClient](https://msdn.microsoft.com/library/system.net.http.httpclient(VS.110).aspx) 类，而不是同步 [WebClient](https://msdn.microsoft.com/library/system.net.webclient.aspx) 类。
- [Await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx)关键字已应用于[HttpClient](https://msdn.microsoft.com/library/system.net.http.httpclient(VS.110).aspx)[GetAsync](https://msdn.microsoft.com/library/hh158944(VS.110).aspx)异步方法。

下图显示了异步别出心裁视图。

![async](using-asynchronous-methods-in-aspnet-45/_static/image2.png)

Gizmos 数据的浏览器表示形式与同步调用创建的视图相同。 唯一的区别是，在负载较重的情况下，异步版本的性能可能更高。

## <a name="registerasynctask-notes"></a>Onendselect 说明

与挂钩的方法 `RegisterAsyncTask` 会立即运行。 [PreRender](https://msdn.microsoft.com/library/ms178472.aspx)

如果直接使用 async void page 事件，如以下代码所示：

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample8.cs)]

当事件执行时，您不再拥有完全控制权。 例如，如果 .aspx 和都是。Master 定义 `Page_Load` 事件，其中一个或两个都是异步的，不能保证执行顺序。 事件处理程序的不确定顺序 (如 `async void Button_Click` ) 适用。

## <a name="performing-multiple-operations-in-parallel"></a><a id="Parallel"></a>  并行执行多个操作

当操作必须执行多个独立的操作时，异步方法与同步方法相比具有明显的优势。 在提供的示例中，"产品"、"小组件" 和 ") Gizmos" 的 "同步" 页 *PWG* (显示了三个 web 服务调用的结果，以获取产品、小组件和 Gizmos 的列表。 提供这些服务的 [ASP.NET Web API](../../../web-api/index.md) 项目使用 [任务延迟](https://msdn.microsoft.com/library/hh139096(VS.110).aspx) 来模拟延迟或慢速网络调用。 当延迟设置为500毫秒时，异步 *PWGasync* 页将需要一小段500以上的时间才能完成，而同步版本则 `PWG` 需要超过1500毫秒。 下面的代码演示了同步 *PWG* 页。

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample9.cs)]

`PWGasync`下面显示了异步代码隐藏。

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample10.cs?highlight=5,11,21)]

下图显示了从异步 *PWGasync* 页返回的视图。

![](using-asynchronous-methods-in-aspnet-45/_static/image3.png)

## <a name="using-a-cancellation-token"></a><a id="CancelToken"></a>  使用取消标记

返回的异步方法 `Task` 可取消，即当使用 Page 指令的特性提供一个参数时，它们将采用[CancellationToken](https://msdn.microsoft.com/library/system.threading.cancellationtoken(VS.110).aspx)参数 `AsyncTimeout` 。 [Page](https://msdn.microsoft.com/library/ydy4x04a.aspx) 下面的代码演示 *GizmosCancelAsync* 页，其超时值为秒。

[!code-aspx[Main](using-asynchronous-methods-in-aspnet-45/samples/sample11.aspx?highlight=1)]

下面的代码显示了 *GizmosCancelAsync.aspx.cs* 文件。

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample12.cs?highlight=6,9)]

在提供的示例应用程序中，选择 *GizmosCancelAsync* 链接将调用 *GizmosCancelAsync* 页，并通过超时异步调用的) 来演示取消 (。 由于延迟时间在随机范围内，你可能需要多次刷新页面以获取超时错误消息。

## <a name="server-configuration-for-high-concurrencyhigh-latency-web-service-calls"></a><a id="ServerConfig"></a>  高并发/高延迟 Web 服务调用的服务器配置

若要实现异步 web 应用程序的优势，可能需要对默认服务器配置进行一些更改。 配置和压力测试异步 web 应用程序时，请记住以下几点。

- Windows 7、Windows Vista、windows 8 和所有 Windows 客户端操作系统最多可以有10个并发请求。 你将需要 Windows Server 操作系统，以查看高负载下的异步方法的优点。
- 使用以下命令，从提升的命令提示符向 IIS 注册 .NET 4.5：  
  %windir%\Microsoft.NET\Framework64 \v4.0.30319\aspnet \_ regiis-i  
  请参阅    [ASP.NET IIS 注册工具 (Aspnet \_regiis.exe) ](https://msdn.microsoft.com/library/k6h9cz8h.aspx)
- 可能需要将 [HTTP.sys](https://www.iis.net/learn/get-started/introduction-to-iis/introduction-to-iis-architecture) 队列限制从默认值1000提高到5000。 如果设置过低，则可能会看到 [HTTP.sys](https://www.iis.net/learn/get-started/introduction-to-iis/introduction-to-iis-architecture) 使用 HTTP 503 状态的拒绝请求。 更改 HTTP.sys 队列限制：

    - 打开 IIS 管理器并导航到 "应用程序池" 窗格。
    - 右键单击目标应用程序池，然后选择 " **高级设置**"。  
        ![高](using-asynchronous-methods-in-aspnet-45/_static/image4.png)
    - 在 " **高级设置** " 对话框中，将 *队列长度* 从1000更改为5000。  
        ![队列长度](using-asynchronous-methods-in-aspnet-45/_static/image5.png)  
  
  请注意，在上面的图像中，.NET framework 作为 "v 4.0" 列出，即使应用程序池使用的是 .NET 4.5 也是如此。 要了解这种差异，请参阅以下内容：

- [.NET 版本控制和多目标 .NET 4.5 是 .NET 4.0 的就地升级](http://www.hanselman.com/blog/NETVersioningAndMultiTargetingNET45IsAnInplaceUpgradeToNET40.aspx)
- [如何将 IIS 应用程序或 AppPool 设置为使用 ASP.NET 3.5，而不是2。0](http://www.hanselman.com/blog/HowToSetAnIISApplicationOrAppPoolToUseASPNET35RatherThan20.aspx)
- [.NET Framework 版本和依赖关系](https://msdn.microsoft.com/library/bb822049(VS.110).aspx)

- 如果你的应用程序使用 web 服务或 System.NET 通过 HTTP 与后端通信，则你可能需要增加 [connectionManagement/maxconnection](https://msdn.microsoft.com/library/fb6y0fyc(VS.110).aspx) 元素。 对于 ASP.NET 应用程序，这被自动配置功能限制为 Cpu 数量的12倍。 这意味着，在四个处理器上，最多可以有 12 \* 个 4 = 48 并发连接到 IP 终结点。 由于这与自动[配置](https://msdn.microsoft.com/library/7w2sway1(VS.110).aspx)相关联，因此，在 ASP.NET 应用程序中增加的最简单方法 `maxconnection` 是在 global.asax 文件的 from 方法中以编程方式设置[ServicePointManager。](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit(VS.110).aspx) `Application_Start` *global.asax* 有关示例，请参阅示例下载。
- 在 .NET 4.5 中， [MaxConcurrentRequestsPerCPU](https://blogs.msdn.com/tmarq/archive/2007/07/21/asp-net-thread-usage-on-iis-7-0-and-6-0.aspx) 的默认值为5000。

## <a name="contributors"></a>作者

- [Levi Broderick](http://stackoverflow.com/users/59641/levi)
- [Tom Dykstra](http://www.bing.com/search?q=site%3Aasp.net+%22Tom+Dykstra%22+-forums.asp.net&amp;qs=n&amp;form=QBRE&amp;pq=site%3Aasp.net+%22tom+dykstra%22+-forums.asp.net&amp;sc=8-42&amp;sp=-1&amp;sk=)
- [Brad Wilson](http://bradwilson.typepad.com/)
- [HongMei Ge](https://blogs.msdn.com/b/hongmeig/)

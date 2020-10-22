---
uid: signalr/overview/performance/signalr-performance
title: SignalR 性能 |Microsoft Docs
author: bradygaster
description: SignalR 性能
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 3751f5e7-59db-4be0-a290-50abc24e5c84
msc.legacyurl: /signalr/overview/performance/signalr-performance
msc.type: authoredcontent
ms.openlocfilehash: b8a44f4c924c94cdfff1ce7630539b45fe269bbf
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345269"
---
# <a name="signalr-performance"></a>SignalR 性能

作者： [Fletcher](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 本主题介绍如何在 SignalR 应用程序中设计、度量和提高性能。
>
> ## <a name="software-versions-used-in-this-topic"></a>本主题中使用的软件版本
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - .NET 4.5
> - SignalR 版本2
>
>
>
> ## <a name="previous-versions-of-this-topic"></a>本主题的早期版本
>
> 有关早期版本的 SignalR 的信息，请参阅 [SignalR 旧版本](../older-versions/index.md)。
>
> ## <a name="questions-and-comments"></a>问题和注释
>
> 请提供有关你喜欢本教程的方式的反馈，并在页面底部的评论中留下反馈。 如果你有与本教程不直接相关的问题，则可以将其发布到 [ASP.NET SignalR 论坛](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 或 [StackOverflow.com](http://stackoverflow.com/)。

有关 SignalR 性能和缩放的最新演示，请参阅 [使用 ASP.NET SignalR 缩放实时 Web](https://channel9.msdn.com/Events/Build/2013/3-502)。

本主题包含以下各节：

- [设计注意事项](#design)
- [优化 SignalR 服务器的性能](#tuning)
- [性能问题疑难解答](#troubleshooting)
- [使用 SignalR 性能计数器](#perfcounters)
- [使用其他性能计数器](#othercounters)
- [其他资源](#otherresources)

<a id="design"></a>

## <a name="design-considerations"></a>设计注意事项

本部分介绍在设计 SignalR 应用程序的过程中可以实现的模式，以确保不会通过生成不必要的网络流量来影响性能。

### <a name="throttling-message-frequency"></a>限制消息频率

即使在以高频率发送消息 (如实时游戏应用程序) 的应用程序中，大多数应用程序也不需要发送多条消息。 若要减少每个客户端生成的流量，可以实现消息循环，使队列和发送消息的频率不高于固定速率 (也就是说，如果在该时间间隔内发送的消息) ，则每秒发送的消息数将为每秒发送的消息数。 有关将消息限制为从客户端和服务器)  (的示例应用程序，请参阅 [使用 SignalR 的高频率实时](../getting-started/tutorial-high-frequency-realtime-with-signalr.md)。

### <a name="reducing-message-size"></a>减小消息大小

可以通过减小序列化对象的大小来减小 SignalR 消息的大小。 在服务器代码中，如果要发送的对象包含不需要传输的属性，则通过使用属性防止这些属性进行序列化 `JsonIgnore` 。 属性的名称也存储在消息中;使用特性可以缩短属性的名称 `JsonProperty` 。 下面的代码示例演示如何排除将某个属性发送到客户端，以及如何缩短属性名称：

**.NET 服务器代码，该代码演示了用于排除发送到客户端的数据的 JsonIgnore 特性，以及用于减小消息大小的 JsonProperty 特性**

[!code-csharp[Main](signalr-performance/samples/sample1.cs?highlight=5,7,10)]

若要在客户端代码中保留可读性/可维护性，在收到消息后，可将缩略属性名称重新映射到友好名称。 下面的代码示例演示了一种可能的方法：将缩短的名称重新映射到较长的名称，方法是：定义消息协定 (映射) ，并使用 `reMap` 函数将协定应用到优化的消息类：

**将简化的属性名称重新映射到用户可读名称的客户端 JavaScript 代码**

[!code-javascript[Main](signalr-performance/samples/sample2.js)]

使用相同的方法，还可以将客户端的消息中的名称缩写给服务器。

减少内存占用量 (也就是说，消息对象的消息) 所使用的内存量也会提高性能。 例如，如果不需要的完整范围 `int` ， `short` `byte` 可以改为使用或。

由于消息存储在服务器内存中的消息总线上，因此减少消息大小也可能解决服务器内存问题。

<a id="tuning"></a>

### <a name="tuning-your-signalr-server-for-performance"></a>优化 SignalR 服务器的性能

以下配置设置可用于优化服务器，以在 SignalR 应用程序中获得更好的性能。 有关如何在 ASP.NET 应用程序中提高性能的常规信息，请参阅 [改善 ASP.NET 性能](https://msdn.microsoft.com/library/ff647787.aspx)。

**SignalR 配置设置**

- **DefaultMessageBufferSize**：默认情况下，SignalR 每次连接时在内存中保留1000消息。 如果正在使用大消息，这可能会产生内存问题，可以通过减少该值来缓解此问题。 此设置可在 `Application_Start` ASP.NET 应用程序中的事件处理程序中设置，或在 `Configuration` 自承载应用程序中的 OWIN startup 类的方法中设置。 下面的示例演示如何减小此值以便减少应用程序的内存占用量，以减少使用的服务器内存量：

    **Startup.cs 中用于减小默认消息缓冲区大小的 .NET server 代码**

    [!code-csharp[Main](signalr-performance/samples/sample3.cs)]

**IIS 配置设置**

- **每个应用程序的最大并发请求**数：增加并发 IIS 请求数将增加可用于为请求提供服务的服务器资源。 默认值为 5000;若要增加此设置，请在提升的命令提示符下执行以下命令：

    [!code-console[Main](signalr-performance/samples/sample4.cmd)]
- **ApplicationPool QueueLength**：这是为应用程序池 Http.sys 队列的最大请求数。 如果队列已满，则新请求将收到 503 "服务不可用" 响应。 默认值为 1000。

    缩短承载应用程序的应用程序池中的工作进程的队列长度将节省内存资源。 有关详细信息，请参阅 [管理、优化和配置应用程序池](https://technet.microsoft.com/library/cc745955.aspx)。

**ASP.NET 配置设置**

本部分包括可以在文件中设置的配置设置 `aspnet.config` 。 此文件位于以下两个位置之一，具体取决于平台：

- `%windir%\Microsoft.NET\Framework\v4.0.30319\aspnet.config`
- `%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet.config`

可提高 SignalR 性能的 ASP.NET 设置包括：

- **每 CPU 的最大并发请求**数：增加此设置可以缓解性能瓶颈。 若要增加此设置，请将以下配置设置添加到 `aspnet.config` 文件中：

    [!code-xml[Main](signalr-performance/samples/sample5.xml?highlight=4)]
- **请求队列限制**：当连接总数超过设置值时 `maxConcurrentRequestsPerCPU` ，ASP.NET 将使用队列开始限制请求。 若要增加队列的大小，可以增加 `requestQueueLimit` 设置。 为此，请将以下配置设置添加到 `processModel` (中的节点， `config/machine.config` 而不是 `aspnet.config`) ：

    [!code-xml[Main](signalr-performance/samples/sample6.xml)]

<a id="troubleshooting"></a>

## <a name="troubleshooting-performance-issues"></a>性能问题故障排除

本部分介绍在应用程序中查找性能瓶颈的方法。

### <a name="verifying-that-websocket-is-being-used"></a>验证是否正在使用 WebSocket

尽管 SignalR 可以使用各种传输来实现客户端与服务器之间的通信，但 WebSocket 提供了显著的性能优势，如果客户端和服务器支持，则应使用这些传输。 若要确定客户端和服务器是否满足 WebSocket 的要求，请参阅 [传输和回退](../getting-started/introduction-to-signalr.md#transports)。 若要确定应用程序中使用的传输，可以使用浏览器开发人员工具，并检查日志以查看连接所使用的传输。 有关在 Internet Explorer 和 Chrome 中使用浏览器开发工具的信息，请参阅 [传输和回退](../getting-started/introduction-to-signalr.md#transports)。

<a id="perfcounters"></a>

## <a name="using-signalr-performance-counters"></a>使用 SignalR 性能计数器

本部分介绍如何启用和使用在包中找到的 SignalR 性能计数器 `Microsoft.AspNet.SignalR.Utils` 。

### <a name="installing-signalrexe"></a>安装 signalr.exe

可以使用名为 SignalR.exe 的实用程序将性能计数器添加到服务器。 若要安装此实用程序，请执行以下步骤：

1. 在 Visual Studio 中，选择 "**工具**" "  >  **nuget 包管理器**" "  >  **管理解决方案的 NuGet 包**"
2. 搜索 **signalr. utils**，并选择 "安装"。

    ![](signalr-performance/_static/image1.png)
3. 接受许可协议以安装包。
4. SignalR.exe 将安装到 `<project folder>/packages/Microsoft.AspNet.SignalR.Utils.<version>/tools` 。

### <a name="installing-performance-counters-with-signalrexe"></a>SignalR.exe 安装性能计数器

若要安装 SignalR 性能计数器，请使用以下参数在提升的命令提示符下运行 SignalR.exe：

[!code-console[Main](signalr-performance/samples/sample7.cmd)]

若要删除 SignalR 性能计数器，请使用以下参数在提升的命令提示符下运行 SignalR.exe：

[!code-console[Main](signalr-performance/samples/sample8.cmd)]

### <a name="signalr-performance-counters"></a>SignalR 性能计数器

实用工具包将安装下列性能计数器。 "Total" 计数器测量自上次应用程序池或服务器重新启动后发生的事件数。

**连接指标**

以下度量值测量发生的连接生存期事件。 有关详细信息，请参阅 [了解和处理连接生存期事件](../guide-to-the-api/handling-connection-lifetime-events.md)。

- **连接已连接**
- **连接已重新连接**
- **断开连接**
- **当前连接数**

**消息指标**

以下度量值测量由 SignalR 生成的消息流量。

- **接收的连接消息总数**
- **已发送的连接消息总数**
- **每秒接收的连接消息数**
- **发送的连接消息/秒**

**消息总线指标**

以下度量值度量通过内部 SignalR 消息总线的流量，其中放置了所有传入和传出 SignalR 消息的队列。 发送或广播消息时，会将其 **发布** 。 在此上下文中， **订阅服务器** 是对消息总线的订阅;这应该等于客户端数量加上服务器本身。 已 **分配的工作线程** 是将数据发送到活动连接的组件; **繁忙辅助角色** 是指主动发送消息的辅助角色。

- **消息总线接收消息总数**
- **每秒接收的消息总线消息数**
- **消息总线消息已发布总计**
- **发布的消息总线消息数/秒**
- **消息总线订阅服务器当前**
- **消息总线订阅服务器总数**
- **消息总线订阅者数/秒**
- **消息总线分配的工作线程**
- **消息总线繁忙辅助角色**
- **消息总线主题当前**

**错误度量值**

以下度量值度量 SignalR 消息流量生成的错误。 集线器**解析**错误发生在无法解析集线器或集线器方法时。 **中心调用** 错误是调用集线器方法时引发的异常。 **传输** 错误是 HTTP 请求或响应期间引发的连接错误。

- **错误：全部总计**
- **错误：全部/秒**
- **错误：集线器解析总数**
- **错误：集线器分辨率/秒**
- **错误：集线器调用总数**
- **错误：集线器调用数/秒**
- **错误：传输总数**
- **错误：传输数/秒**

<a id="scaleout_metrics"></a>

**扩展指标**

以下度量值度量扩展提供程序生成的流量和错误。 此上下文中的 **流** 是扩展提供程序使用的缩放单位;如果使用 SQL Server，则这是一个表; 如果使用了服务总线，则为一个主题，如果使用了 Redis，则为一个订阅。 每个流都确保按顺序进行读写操作;单个流是潜在的缩放瓶颈，因此可以增加流数量以帮助减少瓶颈。 如果使用多个流，则 SignalR 会自动在这些流上分发 (分片) 消息，从而确保按顺序发送从任何给定连接发送的消息。

[MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx)设置控制 SignalR 维护的扩展发送队列的长度。 如果将其设置为大于0的值，则会将发送队列中的所有消息一次发送到配置的消息传送底板。 如果队列的大小超过配置的长度，则后续的发送调用将立即失败并返回 [InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception(v=vs.118).aspx) ，直到队列中的消息数小于设置。 默认情况下，队列处于禁用状态，因为实现的底板通常具有自己的队列或流控制。 在 SQL Server 情况下，连接池会有效地限制每次发送的发送的次数。

默认情况下，只有一个流用于 SQL Server 和 Redis，5个流用于服务总线，而队列被禁用，但这些设置可以通过 SQL Server 和服务总线上的配置进行更改：

**用于配置 SQL Server 底板的表计数和队列长度的 .NET Server 代码**

[!code-csharp[Main](signalr-performance/samples/sample9.cs)]

**用于配置服务总线背板的主题计数和队列长度的 .NET Server 代码**

[!code-csharp[Main](signalr-performance/samples/sample10.cs)]

**缓冲**流是进入出错状态的流;当流处于出错状态时，发送到底板的所有消息都将立即失败，直到流不再出错。 **发送队列长度**是已发布但尚未发送的消息数。

- **扩展消息总线消息数/秒**
- **扩展流总数**
- **扩展流打开**
- **扩展流缓冲**
- **扩展错误总数**
- **扩展错误数/秒**
- **扩展发送队列长度**

有关这些计数器度量的详细信息，请参阅 [SignalR 扩展 With Azure Service Bus](scaleout-with-windows-azure-service-bus.md)。

<a id="othercounters"></a>

## <a name="using-other-performance-counters"></a>使用其他性能计数器

以下性能计数器对于监视应用程序的性能可能也很有用。

**内存**

- \\W3wp.exe) 的所有堆中的 .NET CLR 内存 # 字节 (

**ASP.NET**

- ASP. NET\Requests Current
- NET\Queued
- NET\Rejected

**CPU**

- 处理器 Information\Processor 时间

**TCP/IP**

- 已建立 TCPv6/连接
- 已建立 TCPv4/连接

**Web 服务**

- Web Service\current connections 连接
- Web Service\Maximum 连接

**线程处理**

- .NET CLR 锁和线程 \\ # 个当前逻辑线程
- .NET CLR 锁和线程 \\ # 个当前物理线程

<a id="otherresources"></a>

## <a name="other-resources"></a>其他资源

有关 ASP.NET 性能监视和优化的详细信息，请参阅以下主题：

- [ASP.NET 性能概述](https://msdn.microsoft.com/library/cc668225(v=vs.100).aspx)
- [IIS 7.5、IIS 7.0 和 IIS 6.0 上的 ASP.NET 线程使用情况](https://blogs.msdn.com/b/tmarq/archive/2007/07/21/asp-net-thread-usage-on-iis-7-0-and-6-0.aspx)
- [&lt;&gt; (Web 设置的 applicationPool 元素) ](https://msdn.microsoft.com/library/dd560842.aspx)

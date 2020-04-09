---
uid: signalr/overview/performance/signalr-performance
title: 信号器性能 |微软文档
author: bradygaster
description: SignalR 性能
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 3751f5e7-59db-4be0-a290-50abc24e5c84
msc.legacyurl: /signalr/overview/performance/signalr-performance
msc.type: authoredcontent
ms.openlocfilehash: b8a44f4c924c94cdfff1ce7630539b45fe269bbf
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675717"
---
# <a name="signalr-performance"></a>SignalR 性能

由[帕特里克·弗莱彻](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 本主题介绍如何为 SignalR 应用程序中的设计、测量和改进性能。
>
> ## <a name="software-versions-used-in-this-topic"></a>本主题中使用的软件版本
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - .NET 4.5
> - 信号R版本 2
>
>
>
> ## <a name="previous-versions-of-this-topic"></a>本主题的早期版本
>
> 有关早期版本的 SignalR 的信息，请参阅[SignalR 旧版本](../older-versions/index.md)。
>
> ## <a name="questions-and-comments"></a>问题和评论
>
> 请留下反馈，关于你喜欢本教程的方式，以及我们可以在页面底部的评论中改进什么。 如果您有与本教程没有直接关系的问题，您可以将它们发布到[ASP.NET SignalR 论坛](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com/)。

有关 SignalR 性能和缩放的最新演示文稿，请参阅[使用ASP.NET信号R 缩放实时 Web。](https://channel9.msdn.com/Events/Build/2013/3-502)

本主题包含以下各节：

- [设计注意事项](#design)
- [调整 SignalR 服务器的性能](#tuning)
- [性能问题故障排除](#troubleshooting)
- [使用信号R性能计数器](#perfcounters)
- [使用其他性能计数器](#othercounters)
- [其他资源](#otherresources)

<a id="design"></a>

## <a name="design-considerations"></a>设计注意事项

本节介绍在设计 SignalR 应用程序期间可以实现的模式，以确保不会因生成不必要的网络流量而妨碍性能。

### <a name="throttling-message-frequency"></a>限制消息频率

即使在以高频率发送消息的应用程序（如实时游戏应用程序）中，大多数应用程序也不需要每秒发送多条消息。 为了减少每个客户端生成的流量，可以实现一个消息循环，该队列和发送消息的频率不会超过固定速率（也就是说，如果该时间间隔内有要发送的消息，每秒最多发送一定数量的消息）。 有关将消息限制到特定速率（来自客户端和服务器）的示例应用程序，请参阅[使用 SignalR 的高频实时](../getting-started/tutorial-high-frequency-realtime-with-signalr.md)。

### <a name="reducing-message-size"></a>减小消息大小

您可以通过减小序列化对象的大小来减小 SignalR 消息的大小。 在服务器代码中，如果发送的对象包含不需要传输的属性，则防止使用 属性`JsonIgnore`序列化这些属性。 属性的名称也存储在消息中;可以使用 属性缩短`JsonProperty`属性的名称。 以下代码示例演示如何排除属性发送到客户端，以及如何缩短属性名称：

**.NET 服务器代码，用于演示 JsonIgnore 属性，以排除发送到客户端的数据，以及用于减小消息大小的 JsonProperty 属性**

[!code-csharp[Main](signalr-performance/samples/sample1.cs?highlight=5,7,10)]

为了在客户端代码中保持可读性/可维护性，在收到消息后，可以将缩写属性名称重新映射到人友好名称。 以下代码示例演示了一种通过将缩短的名称重新映射到较长的名称的方法，方法是定义消息协定（映射），并使用 函数`reMap`将协定应用于优化的消息类：

**客户端 JavaScript 代码将缩短的属性名称重新映射到人可读名称**

[!code-javascript[Main](signalr-performance/samples/sample2.js)]

名称也可以使用相同的方法在从客户端到服务器的电子邮件中缩短。

减少消息对象的内存占用空间（即用于消息的内存量）也可以提高性能。 例如，如果不需要全部范围的 ，`int`则可以改用 或`short``byte`。

由于邮件存储在服务器内存中的消息总线中，因此减小消息大小还可以解决服务器内存问题。

<a id="tuning"></a>

### <a name="tuning-your-signalr-server-for-performance"></a>调整 SignalR 服务器的性能

以下配置设置可用于调整服务器，以便在 SignalR 应用程序中获得更好的性能。 有关如何提高ASP.NET应用程序中性能的一般信息，请参阅[改进ASP.NET性能](https://msdn.microsoft.com/library/ff647787.aspx)。

**信号R配置设置**

- **默认消息缓冲区大小**：默认情况下，SignalR 每个连接的内存中保留 1000 条消息。 如果使用大型消息，则可能会产生内存问题，通过减小此值来缓解这些问题。 此设置可以在ASP.NET应用程序中`Application_Start`的事件处理程序中设置，也可以在自托管应用程序中的 OWIN 启动类`Configuration`方法中设置。 以下示例演示如何减小此值以减少应用程序的内存占用量，以减少使用的服务器内存量：

    **Startup.cs 中的 .NET 服务器代码，用于减小默认邮件缓冲区大小**

    [!code-csharp[Main](signalr-performance/samples/sample3.cs)]

**IIS 配置设置**

- **每个应用程序的最多并发请求**：增加并发 IIS 请求的数量将增加可用于服务请求的服务器资源。 默认值为 5000;要增加此设置，请在提升的命令提示符中执行以下命令：

    [!code-console[Main](signalr-performance/samples/sample4.cmd)]
- **应用程序池队列长度**：这是 Http.sys 为应用程序池排队的最大请求数。 队列已满时，新请求将收到 503"服务不可用"响应。 默认值为 1000。

    缩短应用程序托管的应用程序池中工作进程的队列长度将节省内存资源。 有关详细信息，请参阅[管理、调整和配置应用程序池](https://technet.microsoft.com/library/cc745955.aspx)。

**ASP.NET配置设置**

本节包括可在文件中设置的`aspnet.config`配置设置。 此文件位于两个位置之一，具体取决于平台：

- `%windir%\Microsoft.NET\Framework\v4.0.30319\aspnet.config`
- `%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet.config`

可能提高 SignalR 性能ASP.NET设置包括：

- **每个 CPU 的最大并发请求**：增加此设置可能会缓解性能瓶颈。 要增加此设置，向`aspnet.config`文件添加以下配置设置：

    [!code-xml[Main](signalr-performance/samples/sample5.xml?highlight=4)]
- **请求队列限制**：当连接总数超过`maxConcurrentRequestsPerCPU`设置时，ASP.NET将使用队列开始限制请求。 要增加队列的大小，可以增加`requestQueueLimit`设置。 为此，向 中的`processModel``config/machine.config`节点添加以下配置设置（而不是`aspnet.config`）：

    [!code-xml[Main](signalr-performance/samples/sample6.xml)]

<a id="troubleshooting"></a>

## <a name="troubleshooting-performance-issues"></a>性能问题故障排除

本节介绍查找应用程序中的性能瓶颈的方法。

### <a name="verifying-that-websocket-is-being-used"></a>验证是否正在使用 WebSocket

虽然 SignalR 可以使用各种传输在客户端和服务器之间通信，但 WebSocket 具有显著的性能优势，如果客户端和服务器支持它，则应使用它。 要确定客户端和服务器是否满足 WebSocket 的要求，请参阅[传输和回退](../getting-started/introduction-to-signalr.md#transports)。 要确定应用程序中正在使用哪些传输，可以使用浏览器开发人员工具，并检查日志以查看用于连接的传输。 有关在 Internet 资源管理器和 Chrome 中使用浏览器开发工具的信息，请参阅[传输和回退](../getting-started/introduction-to-signalr.md#transports)。

<a id="perfcounters"></a>

## <a name="using-signalr-performance-counters"></a>使用信号R性能计数器

本节介绍如何在`Microsoft.AspNet.SignalR.Utils`封装中找到的启用和使用 SignalR 性能计数器。

### <a name="installing-signalrexe"></a>安装信号器.exe

可以使用称为 SignalR.exe 的实用程序将性能计数器添加到服务器。 要安装此实用程序，请按照以下步骤操作：

1. 在可视化工作室中，选择**工具** > **NuGet 包管理器** > **管理 NuGet 包以进行解决方案**
2. 搜索**信号器.utils，** 然后选择"安装"。

    ![](signalr-performance/_static/image1.png)
3. 接受安装包的许可协议。
4. SignalR.exe 将安装到`<project folder>/packages/Microsoft.AspNet.SignalR.Utils.<version>/tools`。

### <a name="installing-performance-counters-with-signalrexe"></a>使用 SignalR.exe 安装性能计数器

要安装 SignalR 性能计数器，请使用以下参数在提升的命令提示符中运行 SignalR.exe：

[!code-console[Main](signalr-performance/samples/sample7.cmd)]

要删除 SignalR 性能计数器，请使用以下参数在提升的命令提示符中运行 SignalR.exe：

[!code-console[Main](signalr-performance/samples/sample8.cmd)]

### <a name="signalr-performance-counters"></a>信号R性能计数器

实用程序包安装以下性能计数器。 "总计"计数器测量自上次应用程序池或服务器重新启动以来的事件数。

**连接指标**

以下指标衡量发生的连接生存期事件。 有关详细信息，请参阅[了解和处理连接生存期事件](../guide-to-the-api/handling-connection-lifetime-events.md)。

- **连接已连接**
- **连接重新连接**
- **连接已断开连接**
- **连接电流**

**消息指标**

以下指标测量 SignalR 生成的消息流量。

- **接收的连接消息总数**
- **连接消息发送总数**
- **已接收/秒的连接消息**
- **已发送/秒的连接消息**

**消息总线指标**

以下指标测量通过内部 SignalR 消息总线（放置所有传入和传出 SignalR 消息的队列）的流量。 消息在发送或广播时**已发布**。 此上下文中的**订阅服务器**是消息总线上的订阅;这应该等于客户端数加上服务器本身。 **已分配的工作线程**是将数据发送到活动连接的组件;**忙工作人员**是主动发送消息的工作人员。

- **收到的消息总线消息总计**
- **收到/秒的消息总线消息**
- **消息总线消息已发布总计**
- **已发布/秒的消息总线消息**
- **消息总线订阅服务器当前**
- **消息总线订阅者总计**
- **消息总线订阅者/秒**
- **消息总线分配工作**
- **消息总线忙工作人员**
- **邮件总线主题当前**

**错误指标**

以下指标测量由 SignalR 消息流量生成的错误。 当无法解析中心或中心方法时，就会发生**中心解析**错误。 **中心调用**错误是在调用集线器方法时引发的异常。 **传输**错误是在 HTTP 请求或响应期间引发的连接错误。

- **错误：全部总计**
- **错误：全部/秒**
- **错误：中心分辨率总计**
- **错误：集线器分辨率/秒**
- **错误：集线器调用总计**
- **错误：集线器调用/秒**
- **错误：传输总计**
- **错误：传输/秒**

<a id="scaleout_metrics"></a>

**横向扩展指标**

以下指标衡量横向扩展提供程序生成的流量和错误。 此上下文中的**流**是横向扩展提供程序使用的缩放单位;如果使用 SQL Server，则这是表;使用服务总线时的主题;如果使用 Redis，则为订阅。 每个流确保有序的读取和写入操作;单个流是潜在的规模瓶颈，因此可以增加流的数量，以帮助减少该瓶颈。 如果使用多个流，SignalR 将自动在这些流中分发（分片）消息，以确保从任何给定连接发送的消息按顺序排列。

["最大队列长度](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx)"设置控制 SignalR 维护的横向扩展发送队列的长度。 将其设置为大于 0 的值将使发送队列中的所有消息一次发送到配置的消息背板。 如果队列的大小高于配置的长度，则后续发送的呼叫将立即失败，使用[InvalidTheAa，](https://msdn.microsoft.com/library/system.invalidoperationexception(v=vs.118).aspx)直到队列中的消息数再次小于设置。 默认情况下禁用排队，因为实现的背板通常有自己的队列或流控制。 对于 SQL Server，连接池有效地限制了任何一次进行发送的次数。

默认情况下，只有一个流用于 SQL Server 和 Redis，五个流用于服务总线，并且禁用排队，但这些设置可以通过 SQL Server 和服务总线上的配置更改：

**.NET 服务器代码，用于配置 SQL Server 背板的表计数和队列长度**

[!code-csharp[Main](signalr-performance/samples/sample9.cs)]

**.NET 服务器代码，用于配置服务总线背板的主题计数和队列长度**

[!code-csharp[Main](signalr-performance/samples/sample10.cs)]

**缓冲**流是已进入错误状态的流流;当流处于故障状态时，发送到背板的所有消息将立即失败，直到流不再出现故障。 **发送队列长度**是已过帐但尚未发送的邮件数。

- **已接收/秒的横向扩展消息总线消息**
- **横向扩展流总计**
- **展开扩展流**
- **横向扩展流缓冲**
- **横向扩展错误总计**
- **横向扩展错误/秒**
- **横向扩展发送队列长度**

有关这些计数器正在测量的内容的详细信息，请参阅[使用 Azure 服务总线 进行信号R横向扩展](scaleout-with-windows-azure-service-bus.md)。

<a id="othercounters"></a>

## <a name="using-other-performance-counters"></a>使用其他性能计数器

以下性能计数器在监视应用程序的性能时可能也很有用。

**内存**

- .NET CLR\\内存 = 所有堆中的字节（对于 w3wp）

**ASP.NET**

- ASP.NET_请求当前
- ASP.NET_已排队
- ASP.NET_已拒绝

CPU****

- 处理器信息+处理器时间

**TCP/IP**

- TCPv6/已建立连接
- TCPv4/已建立连接

**网络服务**

- Web 服务\当前连接
- Web 服务= 最大连接

**线程**

- .NET CLR 锁\\和线程 # 当前逻辑线程
- .NET CLR 锁\\和线程 # 当前物理线程

<a id="otherresources"></a>

## <a name="other-resources"></a>其他资源

有关ASP.NET性能监视和调优的详细信息，请参阅以下主题：

- [ASP.NET 性能概述](https://msdn.microsoft.com/library/cc668225(v=vs.100).aspx)
- [iIS 7.5、IIS 7.0 和 IIS 6.0 上的ASP.NET线程使用情况](https://blogs.msdn.com/b/tmarq/archive/2007/07/21/asp-net-thread-usage-on-iis-7-0-and-6-0.aspx)
- [&lt;应用程序池&gt;元素（Web 设置）](https://msdn.microsoft.com/library/dd560842.aspx)

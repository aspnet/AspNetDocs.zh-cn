---
uid: signalr/overview/guide-to-the-api/handling-connection-lifetime-events
title: 理解和处理信号R中的连接寿命事件 |微软文档
author: bradygaster
description: 本文介绍如何使用中心 API 公开的事件。
ms.author: bradyg
ms.date: 01/15/2019
ms.assetid: 03960de2-8d95-4444-9169-4426dcc64913
msc.legacyurl: /signalr/overview/guide-to-the-api/handling-connection-lifetime-events
msc.type: authoredcontent
ms.openlocfilehash: 5bdf20549fccab5d644e35fdf4ce351540c8620d
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675825"
---
# <a name="understanding-and-handling-connection-lifetime-events-in-signalr"></a>了解和处理 SignalR 中的连接生存期事件

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 本文概述了可以处理的 SignalR 连接、重新连接和断开连接事件，以及可以配置的超时和保持活动设置。
>
> 本文假定您已经对 SignalR 和连接生存期事件有所了解。 有关信号R 的介绍，请参阅[信号R 简介](../getting-started/introduction-to-signalr.md)。 有关连接生存期事件的列表，请参阅以下资源：
>
> - [如何处理集线器类中的连接生存期事件](hubs-api-guide-server.md#connectionlifetime)
> - [如何处理 JavaScript 客户端中的连接生存期事件](hubs-api-guide-javascript-client.md#connectionlifetime)
> - [如何处理 .NET 客户端中的连接生存期事件](hubs-api-guide-net-client.md#connectionlifetime)
>
> ## <a name="software-versions-used-in-this-topic"></a>本主题中使用的软件版本
>
>
> - [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/)
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

## <a name="overview"></a>概述

本文包含以下各节：

- [连接生存期术语和方案](#terminology)

    - [信号R连接、传输连接和物理连接](#signalrvstransport)
    - [传输断开连接方案](#transportdisconnect)
    - [客户端断开连接方案](#clientdisconnect)
    - [服务器断开连接方案](#serverdisconnect)
- [超时和保持活动设置](#timeoutkeepalive)

    - [ConnectionTimeout](#connectiontimeout)
    - [断开连接超时](#disconnecttimeout)
    - [KeepAlive](#keepalive)
    - [如何更改超时并保持活动设置](#changetimeout)
- [如何通知用户断开连接](#notifydisconnect)
- [如何持续重新连接](#continuousreconnect)
- [如何在服务器代码中断开客户端](#disconnectclientfromserver)
- [检测断开连接的原因](#detectingreasonfordisconnection)

指向 API 参考主题的链接指向 API 的 .NET 4.5 版本。 如果使用 .NET 4，请参阅[API 主题的 .NET 4 版本](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx)。

<a id="terminology"></a>

## <a name="connection-lifetime-terminology-and-scenarios"></a>连接生存期术语和方案

SignalR Hub 中`OnReconnected`的事件处理程序可以直接在给定客户端`OnConnected`之后执行，`OnDisconnected`但不能在之后执行。 在没有断开连接的情况下进行重新连接的原因是，在 SignalR 中使用"连接"一词有多种方式。

<a id="signalrvstransport"></a>

### <a name="signalr-connections-transport-connections-and-physical-connections"></a>信号R连接、传输连接和物理连接

本文将区分*SignalR 连接*、*传输连接*和*物理连接*：

- **SignalR 连接**是指客户端和服务器 URL 之间的逻辑关系，由 SignalR API 维护，并由连接 ID 唯一标识。 有关此关系的数据由 SignalR 维护，用于建立传输连接。 当客户端调用`Stop`方法或达到超时限制时，当 SignalR 尝试重新建立丢失的传输连接时，关系结束，SignalR 会释放数据。
- **传输连接**是指客户端和服务器之间的逻辑关系，由四个传输 API 之一维护：WebSockets、服务器发送的事件、永久帧或长轮询。 SignalR 使用传输 API 创建传输连接，传输 API 取决于物理网络连接的存在来创建传输连接。 当 SignalR 终止传输连接或传输 API 检测到物理连接断开时，传输连接将结束。
- **物理连接**是指促进客户端计算机与服务器计算机之间通信的物理网络链路（电线、无线信号、路由器等）。 物理连接必须存在才能建立传输连接，并且必须建立传输连接才能建立 SignalR 连接。 但是，中断物理连接并不总是会立即结束传输连接或 SignalR 连接，本主题稍后将对此进行说明。

在下图中，SignalR 连接由集线器 API 和持久连接 API SignalR 层表示，传输连接由传输层表示，物理连接由服务器和客户端之间的线表示。

![信号R架构图](handling-connection-lifetime-events/_static/image1.png)

在 SignalR`Start`客户端中调用 该方法时，您提供 SignalR 客户端代码，并提供它所需的所有信息，以便建立与服务器的物理连接。 SignalR 客户端代码使用此信息发出 HTTP 请求，并建立使用四种传输方法之一的物理连接。 如果传输连接失败或服务器发生故障，SignalR 连接不会立即消失，因为客户端仍然拥有自动重新建立到同一 SignalR URL 的新传输连接所需的信息。 在这种情况下，不涉及来自用户应用程序的干预，当 SignalR 客户端代码建立新的传输连接时，它不会启动新的 SignalR 连接。 SignalR 连接的连续性反映在这样一个事实中：在调用`Start`方法时创建的连接 ID 不会更改。

当`OnReconnected`传输连接在丢失后自动重新建立时，中心上的事件处理程序将执行。 事件`OnDisconnected`处理程序在 SignalR 连接的末尾执行。 SignalR 连接可以以以下任何方式结束：

- 如果客户端调用 方法`Stop`，将停止消息将发送到服务器，并且客户端和服务器都会立即终止 SignalR 连接。
- 客户端和服务器之间的连接丢失后，客户端将尝试重新连接，并且服务器等待客户端重新连接。 如果重新连接的尝试不成功，并且断开连接超时期结束，则客户端和服务器都终止 SignalR 连接。 客户端停止尝试重新连接，服务器将释放其 SignalR 连接的表示形式。
- 如果客户端停止运行而没有机会调用`Stop`该方法，服务器将等待客户端重新连接，然后在断开连接超时期后结束 SignalR 连接。
- 如果服务器停止运行，客户端将尝试重新连接（重新创建传输连接），然后在断开连接超时期间后结束 SignalR 连接。

当没有连接问题时，并且用户应用程序通过调用`Stop`该方法结束 SignalR 连接时，SignalR 连接和传输连接大约在同一时间开始和结束。 以下各节将更详细地介绍其他方案。

<a id="transportdisconnect"></a>

### <a name="transport-disconnection-scenarios"></a>传输断开连接方案

物理连接可能很慢，或者连接可能有中断。 根据中断长度等因素，可能会断开传输连接。 然后，SignalR 尝试重新建立传输连接。 有时传输连接 API 检测到中断并丢弃传输连接，SignalR 会立即发现连接丢失。 在其他情况下，传输连接 API 和 SignalR 都不会立即意识到连接已丢失。 对于除长轮询之外的所有传输，SignalR 客户端使用名为 *"保持活动"* 的函数来检查传输 API 无法检测到的连接损失。 有关长轮询连接的信息，请参阅本主题后面的[超时和保持活动设置](#timeoutkeepalive)。

当连接处于非活动状态时，服务器会定期向客户端发送保持活动数据包。 截至撰写本文之日，默认频率为每 10 秒一次。 通过侦听这些数据包，客户端可以判断是否有连接问题。 如果预期时未收到保持活动数据包，则在短时间内客户端假定存在连接问题，如速度缓慢或中断。 如果长时间后仍未收到保持活动，则客户端假定连接已断开，并开始尝试重新连接。

下图说明了在典型方案中在传输 API 无法立即识别的物理连接出现问题时引发的客户端和服务器事件。 该图适用于以下情况：

- 传输是 WebSocket、永久帧或服务器发送的事件。
- 物理网络连接中断的时间各不相同。
- 传输 API 不会意识到中断，因此 SignalR 依赖于保持状态功能来检测中断。

![传输断开](handling-connection-lifetime-events/_static/image2.png)

如果客户端进入重新连接模式，但无法在断开连接超时限制内建立传输连接，服务器将终止 SignalR 连接。 发生这种情况时，服务器将执行 Hub`OnDisconnected`的方法，并排队将断开连接消息发送到客户端，以防客户端以后设法连接。 如果客户端随后重新连接，它将接收断开连接命令并调用`Stop`方法。 在这种情况下，`OnReconnected`在客户端重新连接时不执行，并且`OnDisconnected`在客户端调用`Stop`时不执行。 下图说明了此方案。

![传输中断 - 服务器超时](handling-connection-lifetime-events/_static/image3.png)

可能在客户端上引发的 SignalR 连接生存期事件如下：

- `ConnectionSlow`客户端事件。

    自收到最后一条消息或保持活 ping 以来，保持活动超时的预设比例已过时引发。 默认保持活动超时警告周期为保持活动超时的 2/3。 保持活动超时为 20 秒，因此警告在大约 13 秒时发生。

    默认情况下，服务器每 10 秒发送一次保持活动 ping，客户端大约每 2 秒检查一次保持活动 ping（保持活动超时值和保持活动超时警告值之间的三分之一差异）。

    如果传输 API 意识到断开连接，则在保持活动超时警告期之前，可能会通知 SignalR 断开连接。 在这种情况下，`ConnectionSlow`将不会引发该事件，SignalR 将直接转到该`Reconnecting`事件。
- `Reconnecting`客户端事件。

    当 （a） 传输 API 检测到连接丢失，或 （b） 自上次收到消息或保持活动 ping 以来，保持活动超时期已过。 SignalR 客户端代码开始尝试重新连接。 如果您希望应用程序在传输连接丢失时执行某些操作，则可以处理此事件。 默认保持活动超时期限当前为 20 秒。

    如果客户端代码尝试在 SignalR 处于重新连接模式时调用 Hub 方法，SignalR 将尝试发送命令。 大多数时候，这种尝试会失败，但在某些情况下，它们可能会成功。 对于服务器发送的事件、永久帧和长轮询传输，SignalR 使用两个通信通道，一个通信通道是客户端用于发送消息的，另一个用于接收消息。 用于接收的通道是永久打开的通道，在物理连接中断时，该通道将关闭。 用于发送的通道仍然可用，因此，如果恢复物理连接，则在重新建立接收通道之前，客户端到服务器的方法调用可能成功。 在 SignalR 重新打开用于接收的通道之前，不会接收返回值。
- `Reconnected`客户端事件。

    重新建立传输连接时引发。 中心`OnReconnected`中的事件处理程序执行。
- `Closed`客户端事件（JavaScript`disconnected`中的事件）。

    当断开连接超时期到期时，当 SignalR 客户端代码在丢失传输连接后尝试重新连接时引发。 默认断开连接超时为 30 秒。 （当连接结束时，也会引发此事件，`Stop`因为调用该方法。

传输 API 未检测到的传输连接中断，并且不会延迟服务器中保持活动 ping 的接收时间超过保持活动超时警告期的时间，则可能导致引发任何连接生存期事件。

某些网络环境有意关闭空闲连接，保持状态数据包的另一个功能是通过让这些网络知道 SignalR 连接正在使用来帮助防止这种情况。 在极端情况下，保持活值的默认频率可能不足以阻止关闭连接。 在这种情况下，您可以将保持活动 ping 配置为更频繁地发送。 有关详细信息，请参阅本主题后面的[超时和保持活动设置](#timeoutkeepalive)。

> [!NOTE]
>
> **重要提示**：此处描述的事件序列不保证。 根据此方案，SignalR 会尝试以可预测的方式引发连接生存期事件，但网络事件有许多变化，以及传输 API 等基础通信框架处理这些事件的许多方式。 例如，客户端重新`Reconnected`连接时可能不会引发该事件，或者当尝试建立连接失败`OnConnected`时，服务器上的处理程序可能会运行。 本主题仅描述通常由某些典型情况产生的影响。

<a id="clientdisconnect"></a>

### <a name="client-disconnection-scenarios"></a>客户端断开连接方案

在浏览器客户端中，维护 SignalR 连接的 SignalR 客户端代码在网页的 JavaScript 上下文中运行。 这就是为什么当您从一个页面导航到另一个页面时，SignalR 连接必须结束，这就是为什么如果您从多个浏览器窗口或选项卡连接时，您有多个连接与多个连接指示。 当用户关闭浏览器窗口或选项卡，或导航到新页面或刷新页面时，SignalR 连接将立即结束，因为 SignalR 客户端代码会为您处理该浏览器事件并调用`Stop`该方法。 在这些情况下，或者在应用程序`Stop`调用方法时的任何客户端平台中，`OnDisconnected`事件处理程序会立即在服务器上执行，并且客户端引发`Closed`事件（事件在 JavaScript 中命名）。 `disconnected`

如果客户端应用程序或运行在崩溃时运行的计算机崩溃或进入睡眠状态（例如，当用户关闭便携式计算机时），服务器不会被告知发生了什么。 据服务器所知，客户端丢失可能是由于连接中断，客户端可能尝试重新连接。 因此，在这些情况下，服务器等待给客户端重新连接的机会，并且`OnDisconnected`在断开连接超时期到期之前不会执行（默认情况下约为 30 秒）。 下图说明了此方案。

![客户端计算机故障](handling-connection-lifetime-events/_static/image4.png)

<a id="serverdisconnect"></a>

### <a name="server-disconnection-scenarios"></a>服务器断开连接方案

当服务器脱机时 （它重新启动、 失败、 应用域回收等 ） 结果可能类似于丢失的连接，或者传输 API 和 SignalR 可能立即知道服务器已消失，SignalR 可能开始尝试重新连接而不引发`ConnectionSlow`事件。 如果客户端进入重新连接模式，并且服务器恢复或重新启动，或者新服务器在断开连接超时期到期之前联机，则客户端将重新连接到已还原或新服务器。 在这种情况下，SignalR 连接将继续在客户端上，`Reconnected`并引发事件。 在第一台服务器上，`OnDisconnected`从不执行，在新服务器上执行，`OnReconnected`尽管`OnConnected`以前从未为该服务器上的客户端执行过。 （如果客户端在重新启动或应用域回收后重新连接到同一服务器，则效果相同，因为当服务器重新启动时，它没有以前连接活动的内存。下图假定传输 API 会立即意识到丢失的连接，因此不会引发`ConnectionSlow`事件。

![服务器故障和重新连接](handling-connection-lifetime-events/_static/image5.png)

如果服务器在断开连接超时期间不可用，SignalR 连接将结束。 在这种情况下，事件`Closed`（`disconnected`在 JavaScript 客户端中）在客户端上引发，但从未`OnDisconnected`在服务器上调用。 下图假定传输 API 不会意识到丢失的连接，因此 SignalR 保持活动功能检测到该`ConnectionSlow`事件并引发事件。

![服务器故障和超时](handling-connection-lifetime-events/_static/image6.png)

<a id="timeoutkeepalive"></a>

## <a name="timeout-and-keepalive-settings"></a>超时和保持活动设置

默认`ConnectionTimeout`的`DisconnectTimeout`和`KeepAlive`值适用于大多数方案，但如果环境有特殊需要，则可以更改。 例如，如果网络环境关闭空闲 5 秒的连接，则可能必须减小保持活动值。

<a id="connectiontimeout"></a>

### <a name="connectiontimeout"></a>ConnectionTimeout

此设置表示在关闭传输连接和打开新连接之前保持传输连接打开并等待响应的时间量。 默认值为 110 秒。

此设置仅在禁用保持活动功能时适用，这通常仅适用于长轮询传输。 下图说明了此设置对长轮询传输连接的影响。

![长轮询传输连接](handling-connection-lifetime-events/_static/image7.png)

<a id="disconnecttimeout"></a>

### <a name="disconnecttimeout"></a>断开连接超时

此设置表示引发`Disconnected`事件之前传输连接丢失后等待的时间量。 默认值为 30 秒。 设置 时`DisconnectTimeout`，`KeepAlive`将自动设置为值的`DisconnectTimeout`1/3。

<a id="keepalive"></a>

### <a name="keepalive"></a>KeepAlive

此设置表示在通过空闲连接发送保持活动数据包之前等待的时间量。 默认值为 10 秒。 此值不能超过该值的`DisconnectTimeout`1/3。

`DisconnectTimeout`如果要同时设置 和`KeepAlive`，则`KeepAlive`设置为`DisconnectTimeout`。 否则，`KeepAlive`当自动设置为`KeepAlive`超时值的`DisconnectTimeout`1/3 时，您的设置将被覆盖。

如果要禁用保持活动功能，请设置为`KeepAlive`null。 对于长轮询传输，将自动禁用保持活动功能。

<a id="changetimeout"></a>

### <a name="how-to-change-timeout-and-keepalive-settings"></a>如何更改超时并保持活动设置

要更改这些设置的默认值，请将其设置在`Application_Start` *Global.asax*文件中，如以下示例所示。 示例代码中显示的值与默认值相同。

[!code-csharp[Main](handling-connection-lifetime-events/samples/sample1.cs)]

<a id="notifydisconnect"></a>

## <a name="how-to-notify-the-user-about-disconnections"></a>如何通知用户断开连接

在某些应用程序中，您可能希望在存在连接问题时向用户显示消息。 对于如何以及何时执行此操作，您有多种选择。 以下代码示例适用于使用生成的代理的 JavaScript 客户端。

- 在`connectionSlow`SignalR 意识到连接问题后，在事件进入重新连接模式时，立即处理该事件以显示消息。

    [!code-javascript[Main](handling-connection-lifetime-events/samples/sample2.js)]
- 当`reconnecting`SignalR 意识到断开并进入重新连接模式时，处理事件以显示消息。

    [!code-javascript[Main](handling-connection-lifetime-events/samples/sample3.js)]
- 当尝试`disconnected`重新连接超时时，处理事件以显示消息。在这种情况下，再次与服务器重新建立连接的唯一方法是通过调用`Start`方法重新启动 SignalR 连接，这将创建新的连接 ID。 以下代码示例使用标志来确保仅在重新连接超时后发出通知，而不是在调用`Stop`方法导致的 SignalR 连接的正常结束之后发出通知。

    [!code-javascript[Main](handling-connection-lifetime-events/samples/sample4.js)]

<a id="continuousreconnect"></a>

## <a name="how-to-continuously-reconnect"></a>如何持续重新连接

在某些应用程序中，您可能希望在连接丢失且重新连接尝试超时后自动重新建立连接。为此，可以从`Start``Closed`事件处理程序（JavaScript`disconnected`客户端上的事件处理程序）调用 方法。 您可能需要在调用`Start`之前等待一段时间，以避免在服务器或物理连接不可用时过于频繁地执行此操作。 以下代码示例适用于使用生成的代理的 JavaScript 客户端。

[!code-javascript[Main](handling-connection-lifetime-events/samples/sample5.js)]

在移动客户端中需要注意的一个潜在问题是，当服务器或物理连接不可用时，连续重新连接尝试可能会导致不必要的电池耗尽。

<a id="disconnectclientfromserver"></a>

## <a name="how-to-disconnect-a-client-in-server-code"></a>如何在服务器代码中断开客户端

SignalR 版本 2 没有用于断开客户端的内置服务器 API。 有[计划在未来添加此功能](https://github.com/SignalR/SignalR/issues/2101)。 在当前 SignalR 版本中，将客户端与服务器断开连接的最简单方法是在客户端上实现断开连接方法，并从服务器调用该方法。 以下代码示例显示了使用生成的代理的 JavaScript 客户端的断开连接方法。

[!code-javascript[Main](handling-connection-lifetime-events/samples/sample6.js)]

> [!WARNING]
> 安全性 - 此连接客户端的方法和建议的内置 API 都不会解决运行恶意代码的受黑客攻击的客户端的情况，因为客户端可以重新连接，或者被黑客攻击的代码可能会删除`stopClient`该方法或更改它的作用。 实现有状态拒绝服务 （DOS） 保护的适当位置不在框架或服务器层中，而是在前端基础结构中。

<a id="detectingreasonfordisconnection"></a>
## <a name="detecting-the-reason-for-a-disconnection"></a>检测断开连接的原因

SignalR 2.1 向服务器`OnDisconnect`事件添加重载，指示客户端是否有意断开连接，而不是超时。如果`StopCalled`客户端显式关闭连接，则参数为 true。 在 JavaScript 中，如果服务器错误导致客户端断开连接，则错误信息将作为 传递给客户端`$.connection.hub.lastError`。

**C# 服务器代码`stopCalled`：参数**

[!code-csharp[Main](handling-connection-lifetime-events/samples/sample7.cs?highlight=1,3)]

**JavaScript 客户端代码：在`lastError``disconnect`事件中访问。**

[!code-javascript[Main](handling-connection-lifetime-events/samples/sample8.js?highlight=2-3)]

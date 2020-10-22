---
uid: signalr/overview/guide-to-the-api/handling-connection-lifetime-events
title: 了解并处理 SignalR 中的连接生存期事件 |Microsoft Docs
author: bradygaster
description: 本文介绍如何使用由中心 API 公开的事件。
ms.author: bradyg
ms.date: 01/15/2019
ms.assetid: 03960de2-8d95-4444-9169-4426dcc64913
msc.legacyurl: /signalr/overview/guide-to-the-api/handling-connection-lifetime-events
msc.type: authoredcontent
ms.openlocfilehash: 5bdf20549fccab5d644e35fdf4ce351540c8620d
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345223"
---
# <a name="understanding-and-handling-connection-lifetime-events-in-signalr"></a>了解和处理 SignalR 中的连接生存期事件

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 本文概述了你可以处理的 SignalR 连接、重新连接和断开连接事件，以及你可以配置的超时和 keepalive 设置。
>
> 本文假设你已了解 SignalR 和连接生存期事件。 有关 SignalR 的简介，请参阅 [SignalR 简介](../getting-started/introduction-to-signalr.md)。 有关连接生存期事件的列表，请参阅以下资源：
>
> - [如何处理中心类中的连接生存期事件](hubs-api-guide-server.md#connectionlifetime)
> - [如何处理 JavaScript 客户端中的连接生存期事件](hubs-api-guide-javascript-client.md#connectionlifetime)
> - [如何处理 .NET 客户端中的连接生存期事件](hubs-api-guide-net-client.md#connectionlifetime)
>
> ## <a name="software-versions-used-in-this-topic"></a>本主题中使用的软件版本
>
>
> - [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/)
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

## <a name="overview"></a>概述

本文包含以下各节：

- [连接生存期术语和方案](#terminology)

    - [SignalR 连接、传输连接和物理连接](#signalrvstransport)
    - [传输断开连接方案](#transportdisconnect)
    - [客户端断开连接方案](#clientdisconnect)
    - [服务器断开连接方案](#serverdisconnect)
- [超时和 keepalive 设置](#timeoutkeepalive)

    - [ConnectionTimeout](#connectiontimeout)
    - [DisconnectTimeout](#disconnecttimeout)
    - [KeepAlive](#keepalive)
    - [如何更改超时和 keepalive 设置](#changetimeout)
- [如何通知用户断开](#notifydisconnect)
- [如何持续重新连接](#continuousreconnect)
- [如何在服务器代码中断开客户端连接](#disconnectclientfromserver)
- [检测断开连接的原因](#detectingreasonfordisconnection)

API 参考主题的链接适用于 .NET 4.5 版本的 API。 如果使用的是 .NET 4，请参阅 [.net 4 版本的 API 主题](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx)。

<a id="terminology"></a>

## <a name="connection-lifetime-terminology-and-scenarios"></a>连接生存期术语和方案

`OnReconnected`SignalR 中心内的事件处理程序可以在 `OnConnected` 给定客户端之后直接执行，但不能在之后执行 `OnDisconnected` 。 在没有断开连接的情况下，无需断开连接的原因是在 SignalR 中使用 "连接" 一词。

<a id="signalrvstransport"></a>

### <a name="signalr-connections-transport-connections-and-physical-connections"></a>SignalR 连接、传输连接和物理连接

本文将区分 *SignalR 连接*、 *传输连接*和 *物理连接*：

- **SignalR 连接** 是指由 SignalR API 维护的客户端和服务器 URL 之间的逻辑关系，由连接 ID 唯一标识。 有关此关系的数据由 SignalR 维护，并用于建立传输连接。 当客户端调用方法时， `Stop` 或者当 SignalR 尝试重新建立丢失的传输连接时达到超时限制时，关系将结束并 SignalR 释放数据。
- **传输连接** 指的是客户端与服务器之间的逻辑关系，由四个传输 api 之一： websocket、服务器发送事件、永久帧或长轮询来维护。 SignalR 使用传输 API 创建传输连接，而传输 API 依赖于是否存在物理网络连接来创建传输连接。 当 SignalR 终止传输连接时，或当传输 API 检测到物理连接中断时，传输连接将结束。
- **物理连接** 指的是使客户端计算机和服务器计算机之间的通信更加便利的物理网络链接（线路、无线信号、路由器等）。 若要建立传输连接，必须建立物理连接，若要建立 SignalR 连接，必须建立传输连接。 但是，中断物理连接并不总是立即终止传输连接或 SignalR 连接，这将在本主题的后面部分进行说明。

在下图中，SignalR 连接由集线器 API 和 PersistentConnection API SignalR 层表示，传输连接由传输层表示，物理连接由服务器和客户端之间的线路表示。

![SignalR 体系结构图](handling-connection-lifetime-events/_static/image1.png)

在 `Start` SignalR 客户端中调用方法时，会向 SignalR 客户端代码提供所需的所有信息，以便与服务器建立物理连接。 SignalR 客户端代码使用此信息发出 HTTP 请求，并建立使用四种传输方法之一的物理连接。 如果传输连接失败或服务器发生故障，则 SignalR 连接不会立即消失，因为客户端仍然具有自动重新建立到相同 SignalR URL 的新传输连接所需的信息。 在这种情况下，不涉及用户应用程序的任何干预，并且当 SignalR 客户端代码建立新的传输连接时，它不会启动新的 SignalR 连接。 如果连接 ID 是在调用方法时创建的，则不会更改 SignalR 连接的连续性 `Start` 。

`OnReconnected`集线器上的事件处理程序在丢失后自动重新建立传输连接时执行。 `OnDisconnected`事件处理程序在 SignalR 连接结束时执行。 SignalR 连接可以通过以下任一方式结束：

- 如果客户端调用 `Stop` 方法，则会将停止消息发送到服务器，客户端和服务器会立即结束 SignalR 连接。
- 客户端与服务器之间的连接断开后，客户端会尝试重新连接，并且服务器会等待客户端重新连接。 如果尝试重新连接失败并且断开连接超时期限结束，则客户端和服务器都将结束 SignalR 连接。 客户端将停止尝试重新连接，并且服务器会释放其 SignalR 连接的表示形式。
- 如果客户端在没有机会调用方法的情况下停止运行 `Stop` ，则服务器将等待客户端重新连接，然后在断开连接超时期限后结束 SignalR 连接。
- 如果服务器停止运行，则客户端会尝试重新连接 (重新创建传输连接) ，然后在断开连接超时期限后结束 SignalR 连接。

如果没有连接问题，并且用户应用程序通过调用方法来结束 SignalR 连接 `Stop` ，则 SignalR 连接和传输连接将开始和结束。 以下部分更详细地介绍了其他方案。

<a id="transportdisconnect"></a>

### <a name="transport-disconnection-scenarios"></a>传输断开连接方案

物理连接可能较慢，或者连接可能中断。 根据各种因素（如中断长度），传输连接可能会断开。 SignalR 然后尝试重新建立传输连接。 有时，传输连接 API 会检测中断并断开传输连接，SignalR 会立即发现连接丢失。 在其他情况下，传输连接 API 和 SignalR 都不会立即意识到连接已丢失。 对于除了长时间轮询之外的所有传输，SignalR 客户端使用名为 *keepalive* 的函数检查传输 API 无法检测到的连接是否丢失。 有关长轮询连接的详细信息，请参阅本主题后面的 [超时和 keepalive 设置](#timeoutkeepalive) 。

当某个连接处于非活动状态时，服务器会定期将 keepalive 数据包发送到客户端。 截止本文撰写之日起，默认频率为每10秒。 通过侦听这些数据包，客户端可以判断是否存在连接问题。 如果在需要时未收到 keepalive 数据包，则在经过一段时间后，客户端会假定存在连接问题（如缓慢或中断）。 如果在较长时间后仍未收到 keepalive，则客户端会假定连接已断开，并开始尝试重新连接。

下图说明了在传输 API 无法立即识别的物理连接问题时，在典型方案中引发的客户端和服务器事件。 此关系图适用于以下情况：

- 传输为 Websocket、永久帧或服务器发送事件。
- 物理网络连接中存在不同的中断段。
- 传输 API 不会发现中断，因此 SignalR 依赖于 keepalive 功能来检测它们。

![传输断开](handling-connection-lifetime-events/_static/image2.png)

如果客户端进入重新连接模式，但无法在断开连接超时限制内建立传输连接，则服务器将终止 SignalR 连接。 发生这种情况时，服务器会执行中心的 `OnDisconnected` 方法，并将断开连接消息排队以发送到客户端，以防客户端管理稍后连接。 如果客户端重新连接，则它将接收 disconnect 命令并调用 `Stop` 方法。 在这种情况下， `OnReconnected` 当客户端重新连接时，不会执行，并且不会在 `OnDisconnected` 客户端调用时执行 `Stop` 。 下图说明了这种情况。

![传输中断-服务器超时](handling-connection-lifetime-events/_static/image3.png)

可能会在客户端上引发的 SignalR 连接生存期事件如下所示：

- `ConnectionSlow` 客户端事件。

    自上次收到消息或 keepalive ping 后，当 keepalive 超时期限的预设比例已过去时引发。 默认的 keepalive 超时警告期为2/3。 Keepalive 超时为20秒，因此警告大约会在13秒后发生。

    默认情况下，服务器每隔10秒发送一次 keepalive ping，而客户端会检查每隔2秒的 keepalive ping， (keepalive 超时值和 keepalive 超时警告值) 之间的三分之一。

    如果传输 API 能识别断开连接，则在 keepalive 超时警告期通过之前，可能会通知 SignalR 断开连接。 在这种情况下，将 `ConnectionSlow` 不会引发事件，并且 SignalR 将直接跳到 `Reconnecting` 事件。
- `Reconnecting` 客户端事件。

    当 (传输 API) 检测到连接丢失，或在收到上一个消息或 keepalive ping 后， (b) keepalive 超时期限后引发。 SignalR 客户端代码开始尝试重新连接。 如果希望应用程序在传输连接丢失时执行某些操作，则可以处理此事件。 默认的 keepalive 超时期限当前为20秒。

    如果客户端代码在 SignalR 处于重新连接模式时尝试调用集线器方法，SignalR 将尝试发送命令。 大多数情况下，此类尝试将会失败，但在某些情况下，它们可能会成功。 对于服务器发送的事件、永久帧和长轮询传输，SignalR 将使用两个信道，其中一个信道用于发送消息，另一个用于接收消息。 用于接收的通道是永久打开的通道，并且是物理连接中断时关闭的通道。 用于发送的通道仍可用，因此，如果恢复物理连接，则在重新建立接收通道之前，从客户端到服务器的方法调用可能会成功。 在 SignalR 重新打开用于接收的通道之前，将不会收到返回值。
- `Reconnected` 客户端事件。

    重新建立传输连接时引发。 `OnReconnected`中心中的事件处理程序执行。
- `Closed` JavaScript 中的客户端事件 (`disconnected` 事件) 。

    当断开连接超时期限过期时，SignalR 客户端代码在丢失传输连接后尝试重新连接时引发。 默认断开超时为30秒。  (，当由于调用方法而结束连接时也将引发此事件 `Stop` 。 ) 

传输 API 未检测到的传输连接中断，并且不会延迟从服务器接收的 keepalive ping 超过 keepalive 超时警告期限，这可能不会导致任何连接生存期事件引发。

某些网络环境特意关闭空闲连接，而 keepalive 数据包的另一个功能是通过让这些网络知道 SignalR 连接正在使用来帮助防止这种情况。 在极端情况下，keepalive ping 的默认频率可能不足以防止关闭连接。 在这种情况下，你可以将 keepalive ping 配置为更频繁地发送。 有关详细信息，请参阅本主题后面的 [超时和 keepalive 设置](#timeoutkeepalive) 。

> [!NOTE]
>
> **重要提示**：此处所述的事件序列不能得到保证。 SignalR 使每次尝试按照此方案以可预测的方式引发连接生存期事件，但有很多不同的网络事件，例如传输 Api 等基础通信框架处理它们。 例如，当 `Reconnected` 客户端重新连接时，可能不会引发事件，或者 `OnConnected` 当尝试建立连接时，服务器上的处理程序可能会运行失败。 本主题仅介绍某些典型情况下通常会产生的影响。

<a id="clientdisconnect"></a>

### <a name="client-disconnection-scenarios"></a>客户端断开连接方案

在浏览器客户端中，维护 SignalR 连接的 SignalR 客户端代码在网页的 JavaScript 上下文中运行。 这就是当您从一个页面导航到另一个页面时，SignalR 连接必须结束的原因，这就是当您从多个浏览器窗口或选项卡进行连接时，为什么您具有多个连接 Id 的连接。 当用户关闭浏览器窗口或选项卡，或者导航到新页面或刷新页面时，SignalR 连接将立即结束，因为 SignalR 客户端代码会为你处理该浏览器事件并调用 `Stop` 方法。 在这些情况下，或在应用程序调用方法时的任何客户端平台中 `Stop` ， `OnDisconnected` 事件处理程序会立即在服务器上执行，并且客户端将引发 `Closed` 事件 (在 `disconnected` JavaScript) 中对该事件命名。

例如，如果客户端应用程序或运行的计算机出现故障或进入睡眠状态 (例如，当用户关闭便携式计算机) 时，不会通知服务器发生了什么情况。 服务器知道，客户端的丢失可能是由于连接中断，并且客户端可能会尝试重新连接。 因此，在这些情况下，服务器会等待，使客户端有机会重新连接，并且在 `OnDisconnected` "断开连接超时期限" 过期之前不会执行 () 默认为30秒。 下图说明了这种情况。

![客户端计算机故障](handling-connection-lifetime-events/_static/image4.png)

<a id="serverdisconnect"></a>

### <a name="server-disconnection-scenarios"></a>服务器断开连接方案

当服务器进入脱机状态时，它将重新启动、失败、应用程序域回收等。--结果可能类似于丢失的连接，或者传输 API 和 SignalR 可能会立即知道服务器已丢失，并且 SignalR 可能开始尝试重新连接而不引发 `ConnectionSlow` 事件。 如果客户端进入重新连接模式，并且在断开连接超时期限过期之前，服务器恢复或重新启动，或者新服务器处于联机状态，则客户端将重新连接到已还原的或新的服务器。 在这种情况下，SignalR 连接在客户端上继续，并 `Reconnected` 引发事件。 在第一台服务器上， `OnDisconnected` 将永远不会执行，并且在新服务器上 `OnReconnected` 执行，但之前从未对该 `OnConnected` 服务器上的客户端执行此操作。 如果在重新启动或应用域回收之后客户端重新连接到同一台服务器， (效果是相同的，因为当服务器重启时，它没有以前的连接活动的内存。 ) 下图假设传输 API 立即意识到丢失的连接，因此 `ConnectionSlow` 不会引发事件。

![服务器故障和重新连接](handling-connection-lifetime-events/_static/image5.png)

如果在断开连接超时期限内服务器不能使用，SignalR 连接将结束。 在此方案中， `Closed` `disconnected` JavaScript 客户端) 中 (事件在客户端上引发，但 `OnDisconnected` 从不在服务器上调用。 以下关系图假定传输 API 不会意识到丢失的连接，因此 SignalR keepalive 功能检测到它，并 `ConnectionSlow` 引发事件。

![服务器故障和超时](handling-connection-lifetime-events/_static/image6.png)

<a id="timeoutkeepalive"></a>

## <a name="timeout-and-keepalive-settings"></a>超时和 keepalive 设置

默认 `ConnectionTimeout` 值、 `DisconnectTimeout` 和 `KeepAlive` 值适用于大多数方案，但如果你的环境有特殊需求，则可以更改这些值。 例如，如果你的网络环境关闭闲置时间为5秒的连接，则可能需要减少 keepalive 值。

<a id="connectiontimeout"></a>

### <a name="connectiontimeout"></a>ConnectionTimeout

此设置表示在关闭传输连接并打开新连接之前，该连接保持打开并等待响应的时间量。 默认值为110秒。

此设置仅适用于禁用 keepalive 功能的情况，该功能通常仅适用于长轮询传输。 下图说明了此设置对长轮询传输连接的影响。

![长轮询传输连接](handling-connection-lifetime-events/_static/image7.png)

<a id="disconnecttimeout"></a>

### <a name="disconnecttimeout"></a>DisconnectTimeout

此设置表示在引发事件之前等待传输连接丢失的时间量 `Disconnected` 。 默认值为 30 秒。 设置时 `DisconnectTimeout` ，会 `KeepAlive` 自动将值设置为 1/3 `DisconnectTimeout` 。

<a id="keepalive"></a>

### <a name="keepalive"></a>KeepAlive

此设置表示在通过空闲连接发送 keepalive 数据包之前要等待的时间量。 默认值为 10 秒。 此值不能大于 1/3 `DisconnectTimeout` 。

如果要设置 `DisconnectTimeout` 和 `KeepAlive` ，请 `KeepAlive` 在后面设置 `DisconnectTimeout` 。 否则 `KeepAlive` ，将在 `DisconnectTimeout` 自动将 `KeepAlive` 超时值设置为1/3 时覆盖你的设置。

如果要禁用 keepalive 功能，则将设置 `KeepAlive` 为 null。 自动为长轮询传输禁用 Keepalive 功能。

<a id="changetimeout"></a>

### <a name="how-to-change-timeout-and-keepalive-settings"></a>如何更改超时和 keepalive 设置

若要更改这些设置的默认值，请在 `Application_Start` *global.asax* 文件中将其设置为，如下面的示例中所示。 示例代码中显示的值与默认值相同。

[!code-csharp[Main](handling-connection-lifetime-events/samples/sample1.cs)]

<a id="notifydisconnect"></a>

## <a name="how-to-notify-the-user-about-disconnections"></a>如何通知用户断开

在某些应用程序中，当出现连接问题时，您可能希望向用户显示一条消息。 您有几个选项可用于执行此操作的方式和时间。 下面的代码示例适用于使用生成的代理的 JavaScript 客户端。

- 处理 `connectionSlow` 事件，以便在 SignalR 了解连接问题之后，在进入重新连接模式之前立即显示消息。

    [!code-javascript[Main](handling-connection-lifetime-events/samples/sample2.js)]
- 处理 `reconnecting` 事件，以便在 SignalR 知道断开连接并且进入重新连接模式时显示一条消息。

    [!code-javascript[Main](handling-connection-lifetime-events/samples/sample3.js)]
- 处理 `disconnected` 事件，以便在尝试重新连接时显示一条消息。在此方案中，重新建立与服务器的连接的唯一方法是通过调用方法来重新启动 SignalR 连接 `Start` ，这将创建一个新的连接 ID。 下面的代码示例使用标志，以确保仅在重新连接超时后（而不是在通过调用方法导致的 SignalR 连接结束后）发出通知 `Stop` 。

    [!code-javascript[Main](handling-connection-lifetime-events/samples/sample4.js)]

<a id="continuousreconnect"></a>

## <a name="how-to-continuously-reconnect"></a>如何持续重新连接

在某些应用程序中，你可能希望在连接丢失后自动重新建立连接，并且尝试重新连接已超时。为此，可以 `Start` 从事件处理程序调用该方法， `Closed` (`disconnected` JavaScript 客户端) 上的事件处理程序。 在调用之前，您可能需要等待一段时间 `Start` ，以避免在服务器或物理连接不可用时过于频繁地执行此操作。 下面的代码示例适用于使用生成的代理的 JavaScript 客户端。

[!code-javascript[Main](handling-connection-lifetime-events/samples/sample5.js)]

在移动客户端中需要注意的一个潜在问题是：当服务器或物理连接不可用时，连续重新连接尝试可能会导致不必要的电池消耗。

<a id="disconnectclientfromserver"></a>

## <a name="how-to-disconnect-a-client-in-server-code"></a>如何在服务器代码中断开客户端连接

SignalR 版本2没有用于断开客户端的内置服务器 API。 将来有一些 [用于添加此功能的计划](https://github.com/SignalR/SignalR/issues/2101)。 在当前的 SignalR 版本中，将客户端与服务器断开连接的最简单方法是在客户端上实现断开连接方法，并从服务器调用该方法。 下面的代码示例演示如何使用生成的代理为 JavaScript 客户端提供断开连接方法。

[!code-javascript[Main](handling-connection-lifetime-events/samples/sample6.js)]

> [!WARNING]
> 安全性-用于断开客户端的这种方法和建议的内置 API 将解决正在运行恶意代码的被攻击的客户端的情况，因为客户端可以重新连接或被攻击的代码可能会删除 `stopClient` 方法或更改其功能。 用于实现有状态拒绝服务 (DOS 的适当位置) 保护不在框架或服务器层中，而是在前端基础结构中。

<a id="detectingreasonfordisconnection"></a>
## <a name="detecting-the-reason-for-a-disconnection"></a>检测断开连接的原因

SignalR 2.1 将重载添加到服务器 `OnDisconnect` 事件，该事件指示客户端是否特意断开连接，而不是超时。 `StopCalled` 如果客户端显式关闭连接，则参数为 true。 在 JavaScript 中，如果服务器错误导致客户端断开连接，则错误信息将作为发送到客户端 `$.connection.hub.lastError` 。

**C # 服务器代码： `stopCalled` 参数**

[!code-csharp[Main](handling-connection-lifetime-events/samples/sample7.cs?highlight=1,3)]

**JavaScript 客户端代码： `lastError` 在事件中访问 `disconnect` 。**

[!code-javascript[Main](handling-connection-lifetime-events/samples/sample8.js?highlight=2-3)]

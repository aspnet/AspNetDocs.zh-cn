---
uid: signalr/overview/older-versions/signalr-1x-hubs-api-guide-net-client
title: ASP.NET SignalR 中心 API 指南-.NET 客户端（SignalR 1.x） |Microsoft Docs
author: bradygaster
description: 本文档介绍了如何在 .NET 客户端中使用 SignalR 版本2的中心 API，例如 Windows 应用商店（WinRT）、WPF、Silverlight 和缺点 。
ms.author: bradyg
ms.date: 04/17/2013
ms.assetid: c334adc3-d6dc-44f3-9f06-f7634475aad3
msc.legacyurl: /signalr/overview/older-versions/signalr-1x-hubs-api-guide-net-client
msc.type: authoredcontent
ms.openlocfilehash: 2b22b53c405a865f91b04e677f60b82dd46dbf9b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78505970"
---
# <a name="aspnet-signalr-hubs-api-guide---net-client-signalr-1x"></a>ASP.NET SignalR 中心 API 指南-.NET 客户端（SignalR 1.x）

作者： [Fletcher](https://github.com/pfletcher)， [Tom Dykstra](https://github.com/tdykstra)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 本文档介绍了如何在 .NET 客户端中使用 SignalR 版本2的中心 API，例如 Windows 应用商店（WinRT）、WPF、Silverlight 和控制台应用程序。
> 
> 利用 SignalR 中心 API，你可以将服务器中的远程过程调用（Rpc）连接到已连接的客户端和客户端。 在服务器代码中，你将定义可由客户端调用的方法，并调用在客户端上运行的方法。 在客户端代码中，定义可从服务器调用的方法，并调用在服务器上运行的方法。 SignalR 负责处理所有的客户端到服务器的操作。
> 
> SignalR 还提供名为持久性连接的较低级别 API。 有关 SignalR、集线器和持久性连接的简介，或有关演示如何生成完整 SignalR 应用程序的教程，请参阅[SignalR-入门](../getting-started/index.md)。

## <a name="overview"></a>概述

本文档包含以下各节：

- [客户端设置](#clientsetup)
- [如何建立连接](#establishconnection)

    - [来自 Silverlight 客户端的跨域连接](#slcrossdomain)
- [如何配置连接](#configureconnection)

    - [如何设置 WPF 客户端中的最大并发连接数](#maxconnections)
    - [如何指定查询字符串参数](#querystring)
    - [如何指定传输方法](#transport)
    - [如何指定 HTTP 标头](#httpheaders)
    - [如何指定客户端证书](#clientcertificate)
- [如何创建中心代理](#proxy)
- [如何在客户端上定义服务器可以调用的方法](#callclient)

    - [不带参数的方法](#clientmethodswithoutparms)
    - [带参数的方法，指定参数类型](#clientmethodswithparmtypes)
    - [带参数的方法，指定参数的动态对象](#clientmethodswithdynamparms)
    - [如何删除处理程序](#removehandler)
- [如何从客户端调用服务器方法](#callserver)
- [如何处理连接生存期事件](#connectionlifetime)
- [如何处理错误](#handleerrors)
- [如何启用客户端日志记录](#logging)
- [服务器可以调用的客户端方法的 WPF、Silverlight 和控制台应用程序代码示例](#wpfsl)

对于 .NET 客户端项目示例，请参阅以下资源：

- [gustavo-GitHub.com 上的 armenta/SignalR](https://github.com/gustavo-armenta/SignalR-Samples) （WinRT，Silverlight，控制台应用程序示例）。
- [DamianEdwards/SignalR-MoveShapeDemo/MoveShape](https://github.com/DamianEdwards/SignalR-MoveShapeDemo/tree/master/MoveShape/MoveShape.Desktop) on GITHUB.COM （WPF 示例）。
- GitHub.com 上的[SignalR/SignalR](https://github.com/SignalR/SignalR/tree/master/samples/Microsoft.AspNet.SignalR.Client.Samples) （控制台应用示例）。

有关如何对服务器或 JavaScript 客户端进行编程的文档，请参阅以下资源：

- [SignalR 中心 API 指南-服务器](../guide-to-the-api/hubs-api-guide-server.md)
- [SignalR 中心 API 指南-JavaScript 客户端](../guide-to-the-api/hubs-api-guide-javascript-client.md)

API 参考主题的链接适用于 .NET 4.5 版本的 API。 如果使用的是 .NET 4，请参阅[.net 4 版本的 API 主题](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx)。

<a id="clientsetup"></a>

## <a name="client-setup"></a>客户端设置

安装[SignalR](http://nuget.org/packages/Microsoft.AspNet.SignalR.Client) NuGet 包（而不是[SignalR](http://nuget.org/packages/microsoft.aspnet.signalr)包）（& e）。 对于 .NET 4 和 .NET 4.5，此包支持 WinRT、Silverlight、WPF、控制台应用程序和 Windows Phone 客户端。

如果客户端上的 SignalR 版本与服务器上的版本不同，则 SignalR 通常能够适应不同之处。 例如，当发布 SignalR 版本2.0，并在服务器上安装该版本时，服务器将支持安装了 1.1. x 的客户端以及安装有2.0 的客户端。 如果服务器上的版本与客户端上的版本之间的差异太大，则当客户端尝试建立连接时，SignalR 将引发 `InvalidOperationException` 异常。 错误消息为 "`You are using a version of the client that isn't compatible with the server. Client version X.X, server version X.X`"。

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a>如何建立连接

建立连接之前，必须先创建一个 `HubConnection` 对象并创建一个代理。 若要建立连接，请对 `HubConnection` 对象调用 `Start` 方法。

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample1.cs?highlight=1,4)]

> [!NOTE]
> 对于 JavaScript 客户端，你必须注册至少一个事件处理程序，然后才能调用 `Start` 方法来建立连接。 这不是 .NET 客户端所必需的。 对于 JavaScript 客户端，生成的代理代码会自动为服务器上存在的所有中心创建代理，并注册处理程序，以指示客户端打算使用哪些集线器。 但对于 .NET 客户端，你可以手动创建中心代理，因此 SignalR 假定你将使用为创建代理的任何集线器。

示例代码使用默认的 "/signalr" URL 连接到 SignalR 服务。 有关如何指定其他基 URL 的信息，请参阅[ASP.NET SignalR HUB API 指南-Server-/SIGNALR URL](../guide-to-the-api/hubs-api-guide-server.md#signalrurl)。

`Start` 方法以异步方式执行。 若要确保后续代码行在建立连接之前不会执行，请使用 ASP.NET 4.5 异步方法中的 `await` 或在同步方法中 `.Wait()`。 请勿在 WinRT 客户端中使用 `.Wait()`。

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample2.cs?highlight=1)]

[!code-css[Main](signalr-1x-hubs-api-guide-net-client/samples/sample3.css?highlight=1)]

`HubConnection` 类是线程安全的。

<a id="slcrossdomain"></a>

### <a name="cross-domain-connections-from-silverlight-clients"></a>来自 Silverlight 客户端的跨域连接

有关如何从 Silverlight 客户端启用跨域连接的信息，请参阅[使服务跨域边界可用](https://msdn.microsoft.com/library/cc197955(v=vs.95).aspx)。

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a>如何配置连接

在建立连接之前，您可以指定以下任一选项：

- 并发连接限制。
- 查询字符串参数。
- 传输方法。
- HTTP 标头。
- 客户端证书。

<a id="maxconnections"></a>

### <a name="how-to-set-the-maximum-number-of-concurrent-connections-in-wpf-clients"></a>如何设置 WPF 客户端中的最大并发连接数

在 WPF 客户端中，你可能必须将最大并发连接数从其默认值2增加到最大值。 建议值为10。

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample4.cs?highlight=4)]

有关详细信息，请参阅[ServicePointManager. servicepointmanager.defaultconnectionlimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx)。

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a>如何指定查询字符串参数

如果要在客户端连接时将数据发送到服务器，则可以将查询字符串参数添加到连接对象。 下面的示例演示如何在客户端代码中设置查询字符串参数。

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample5.cs)]

下面的示例演示如何读取服务器代码中的查询字符串参数。

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample6.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a>如何指定传输方法

作为连接过程的一部分，SignalR 客户端通常与服务器协商以确定服务器和客户端支持的最佳传输。 如果已知道要使用的传输，可以绕过此协商过程。 若要指定传输方法，请将传输对象传入到 Start 方法。 下面的示例演示如何在客户端代码中指定传输方法。

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample7.cs?highlight=4)]

[SignalR](https://msdn.microsoft.com/library/jj918090(v=vs.111).aspx)命名空间包含可用于指定传输的以下类。 "的命名空间可用于指定传输。

- [LongPollingTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.longpollingtransport(v=vs.111).aspx)
- [ServerSentEventsTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.serversenteventstransport(v=vs.111).aspx)
- [WebSocketTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.websockettransport(v=vs.111).aspx) （仅在服务器和客户端都使用 .net 4.5 时可用。）
- [AutoTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.autotransport(v=vs.111).aspx) （自动选择客户端和服务器支持的最佳传输。 这是默认传输。 将此传入到 `Start` 方法与不传入任何内容相同。）

此列表中不包含 ForeverFrame 传输，因为它仅由浏览器使用。

有关如何在服务器代码中检查传输方法的信息，请参阅[ASP.NET SignalR HUB API 指南-服务器-如何从上下文属性获取有关客户端的信息](../guide-to-the-api/hubs-api-guide-server.md#contextproperty)。 有关传输和回退的详细信息，请参阅[SignalR-传输和回退简介](../getting-started/introduction-to-signalr.md#transports)。

<a id="httpheaders"></a>

### <a name="how-to-specify-http-headers"></a>如何指定 HTTP 标头

若要设置 HTTP 标头，请使用连接对象的 `Headers` 属性。 下面的示例演示如何添加 HTTP 标头。

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample8.cs?highlight=2)]

<a id="clientcertificate"></a>

### <a name="how-to-specify-client-certificates"></a>如何指定客户端证书

若要添加客户端证书，请对连接对象使用 `AddClientCertificate` 方法。

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample9.cs?highlight=2)]

<a id="proxy"></a>

## <a name="how-to-create-the-hub-proxy"></a>如何创建中心代理

若要在客户端上定义集线器可以从服务器调用的方法，并在服务器上调用集线器上的方法，请通过对连接对象调用 `CreateHubProxy` 来为集线器创建代理。 传递给 `CreateHubProxy` 的字符串是中心类的名称，或 `HubName` 属性指定的名称（如果服务器上使用了一个名称）。 名称匹配不区分大小写。

**服务器上的中心类**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample10.cs?highlight=1)]

**创建中心类的客户端代理**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample11.cs?highlight=2)]

如果使用 `HubName` 特性修饰中心类，请使用该名称。

**服务器上的中心类**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample12.cs)]

**创建中心类的客户端代理**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample13.cs?highlight=2)]

代理对象是线程安全的。 事实上，如果用相同的 `hubName`多次调用 `HubConnection.CreateHubProxy`，则会获得相同的缓存 `IHubProxy` 对象。

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a>如何在客户端上定义服务器可以调用的方法

若要定义服务器可以调用的方法，请使用代理的 `On` 方法来注册事件处理程序。

方法名称匹配不区分大小写。 例如，服务器上的 `Clients.All.UpdateStockPrice` 会在客户端上执行 `updateStockPrice`、`updatestockprice`或 `UpdateStockPrice`。

不同的客户端平台对于你编写方法代码以更新 UI 的方式有不同的要求。 显示的示例适用于 WinRT （Windows 应用商店 .NET）客户端。 WPF、Silverlight 和控制台应用程序示例在[本主题后面的单独章节](#wpfsl)中提供。

<a id="clientmethodswithoutparms"></a>

### <a name="methods-without-parameters"></a>不带参数的方法

如果正在处理的方法没有参数，请使用 `On` 方法的非泛型重载：

**调用不带参数的客户端方法的服务器代码**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample14.cs?highlight=5)]

**从没有参数的服务器中调用的方法的 WinRT 客户端代码（[请参阅本主题后面的 WPF 和 Silverlight 示例](#wpfsl)）**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample15.cs)]

<a id="clientmethodswithparmtypes"></a>

### <a name="methods-with-parameters-specifying-the-parameter-types"></a>带参数的方法，指定参数类型

如果正在处理的方法具有参数，请将参数的类型指定为 `On` 方法的泛型类型。 `On` 方法的泛型重载可用于指定多达8个参数（4在 Windows Phone 7 上）。 在下面的示例中，将一个参数发送到 `UpdateStockPrice` 方法。

**使用参数调用客户端方法的服务器代码**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample16.cs?highlight=3)]

**用于参数的 Stock 类**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample17.cs)]

**从具有参数的服务器中调用的方法的 WinRT 客户端代码（[请参阅本主题后面的 WPF 和 Silverlight 示例](#wpfsl)）**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample18.cs?highlight=1,5)]

<a id="clientmethodswithdynamparms"></a>

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a>带参数的方法，指定参数的动态对象

作为将参数指定为 `On` 方法的泛型类型的替代方法，可以将参数指定为动态对象：

**使用参数调用客户端方法的服务器代码**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample19.cs?highlight=3)]

**用于参数的 Stock 类**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample20.cs)]

**从具有参数的服务器中调用的方法的 WinRT 客户端代码，对参数使用动态对象（[请参阅本主题后面的 WPF 和 Silverlight 示例](#wpfsl)）**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample21.cs?highlight=1,5)]

<a id="removehandler"></a>

### <a name="how-to-remove-a-handler"></a>如何删除处理程序

若要删除处理程序，请调用其 `Dispose` 方法。

**从服务器调用的方法的客户端代码**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample22.cs?highlight=1)]

**用于删除处理程序的客户端代码**

[!code-css[Main](signalr-1x-hubs-api-guide-net-client/samples/sample23.css?highlight=1)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a>如何从客户端调用服务器方法

若要在服务器上调用方法，请在中心代理上使用 `Invoke` 方法。

如果服务器方法没有返回值，请使用 `Invoke` 方法的非泛型重载。

**没有返回值的方法的服务器代码**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample24.cs?highlight=3)]

**调用没有返回值的方法的客户端代码**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample25.cs?highlight=1)]

如果服务器方法具有返回值，则将返回类型指定为 `Invoke` 方法的泛型类型。

**具有返回值并采用复杂类型参数的方法的服务器代码**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample26.cs?highlight=1)]

**用于参数和返回值的 Stock 类**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample27.cs)]

**在 ASP.NET 4.5 异步方法中调用具有返回值并采用复杂类型参数的方法的客户端代码**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample28.cs?highlight=1-2)]

**在同步方法中调用具有返回值并采用复杂类型参数的方法的客户端代码**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample29.cs?highlight=1-2)]

`Invoke` 方法异步执行并返回一个 `Task` 对象。 如果未指定 `await` 或 `.Wait()`，则在调用的方法完成执行之前，将执行下一行代码。

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a>如何处理连接生存期事件

SignalR 提供以下连接生存期事件，你可以处理这些事件：

- `Received`：在连接上接收到任何数据时引发。 提供接收的数据。
- `ConnectionSlow`：当客户端检测到连接缓慢或频繁断开时引发。
- `Reconnecting`：基础传输开始重新连接时引发。
- `Reconnected`：在基础传输重新连接后引发。
- `StateChanged`：在连接状态发生更改时引发。 提供旧状态和新状态。 有关连接状态值的信息，请参阅[ConnectionState 枚举](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connectionstate(v=vs.111).aspx)。
- `Closed`：连接断开连接时引发。

例如，如果想要显示不是致命错误的警告消息，但会导致间歇连接问题（如缓慢或频繁断开连接），则应对 `ConnectionSlow` 事件。

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample30.cs)]

有关详细信息，请参阅[了解和处理 SignalR 中的连接生存期事件](../guide-to-the-api/handling-connection-lifetime-events.md)。

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a>如何处理错误

如果未在服务器上显式启用详细的错误消息，则在出现错误后 SignalR 返回的异常对象包含有关错误的最小信息。 例如，如果对 `newContosoChatMessage` 的调用失败，则出于安全原因，不建议将错误对象中的错误消息包含 "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" 向生产中的客户端发送详细的错误消息，但如果想要启用详细的错误消息以进行故障排除，请在服务器上使用以下代码。

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample31.cs?highlight=2)]

<a id="handleerrors"></a>

若要处理 SignalR 引发的错误，可以在连接对象上为 `Error` 事件添加处理程序。

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample32.cs)]

若要处理方法调用中的错误，请将代码包装在 try-catch 块中。

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample33.cs)]

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a>如何启用客户端日志记录

若要启用客户端日志记录，请设置连接对象的 "`TraceLevel`" 和 "`TraceWriter`" 属性。

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample34.cs?highlight=2-3)]

<a id="wpfsl"></a>

## <a name="wpf-silverlight-and-console-application-code-samples-for-client-methods-that-the-server-can-call"></a>服务器可以调用的客户端方法的 WPF、Silverlight 和控制台应用程序代码示例

前面所示的代码示例用于定义服务器可以调用的客户端方法。 以下示例显示了适用于 WPF、Silverlight 和控制台应用程序客户端的等效代码。

### <a name="methods-without-parameters"></a>不带参数的方法

**从没有参数的服务器中调用的方法的 WPF 客户端代码**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample35.cs?highlight=1)]

**从没有参数的服务器中调用的方法的 Silverlight 客户端代码**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample36.cs?highlight=1)]

**不带参数的服务器中调用的方法的控制台应用程序客户端代码**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample37.cs?highlight=1)]

### <a name="methods-with-parameters-specifying-the-parameter-types"></a>带参数的方法，指定参数类型

**从具有参数的服务器中调用的方法的 WPF 客户端代码**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample38.cs?highlight=1,4)]

**从具有参数的服务器中调用的方法的 Silverlight 客户端代码**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample39.cs?highlight=1,5)]

**从具有参数的服务器中调用的方法的控制台应用程序客户端代码**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample40.cs?highlight=1-2)]

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a>带参数的方法，指定参数的动态对象

**从具有参数的服务器中调用的方法的 WPF 客户端代码，对参数使用动态对象**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample41.cs?highlight=1,4)]

**从具有参数的服务器中调用的方法的 Silverlight 客户端代码，对参数使用动态对象**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample42.cs?highlight=1,5)]

**从具有参数的服务器中调用的方法的控制台应用程序客户端代码，对参数使用动态对象**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample43.cs?highlight=1-2)]

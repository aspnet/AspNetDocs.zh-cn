---
uid: signalr/overview/guide-to-the-api/hubs-api-guide-net-client
title: ASP.NET信号器集线器 API 指南 - .NET 客户端 （C#） |微软文档
author: bradygaster
description: 本文档介绍了在 .NET 客户端（如 Windows 应用商店 （WinRT）、WPF、Silverlight 和 cons...
ms.author: bradyg
ms.date: 01/15/2019
ms.assetid: 6d02d9f7-94e5-4140-9f51-5a6040f274f6
msc.legacyurl: /signalr/overview/guide-to-the-api/hubs-api-guide-net-client
msc.type: authoredcontent
ms.openlocfilehash: d3536f1c15cd7dad7cd660becf0577e5c131f707
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675927"
---
# <a name="aspnet-signalr-hubs-api-guide---net-client-c"></a>ASP.NET信号器集线器 API 指南 - .NET 客户端 （C#）

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 本文档介绍了在 .NET 客户端（如 Windows 应用商店 （WinRT）、WPF、Silverlight 和控制台应用程序）中为 SignalR 版本 2 使用集线器 API 的简介。
>
> SignalR 集线器 API 使您能够从服务器对连接的客户端以及从客户端到服务器进行远程过程调用 （RPC）。 在服务器代码中，定义客户端可以调用的方法，并调用在客户端上运行的方法。 在客户端代码中，定义可以从服务器调用的方法，并调用在服务器上运行的方法。 SignalR 为您处理所有客户端到服务器管道。
>
> SignalR 还提供称为持久连接的较低级别的 API。 有关 SignalR、集线器和持久连接的介绍，或者有关如何构建完整的 SignalR 应用程序的教程，请参阅[SignalR - 入门](../getting-started/index.md)。
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

本文档包含以下各节：

- [客户端设置](#clientsetup)
- [如何建立连接](#establishconnection)

    - [来自银光客户端的跨域连接](#slcrossdomain)
- [如何配置连接](#configureconnection)

    - [如何设置 WPF 客户端中的最大并发连接数](#maxconnections)
    - [如何指定查询字符串参数](#querystring)
    - [如何指定传输方法](#transport)
    - [如何指定 HTTP 标头](#httpheaders)
    - [如何指定客户端证书](#clientcertificate)
- [如何创建中心代理](#proxy)
- [如何在客户端上定义服务器可以调用的方法](#callclient)

    - [没有参数的方法](#clientmethodswithoutparms)
    - [具有参数的方法，指定参数类型](#clientmethodswithparmtypes)
    - [具有参数的方法，为参数指定动态对象](#clientmethodswithdynamparms)
    - [如何删除处理程序](#removehandler)
- [如何从客户端调用服务器方法](#callserver)
- [如何处理连接生存期事件](#connectionlifetime)
- [如何处理错误](#handleerrors)
- [如何启用客户端日志记录](#logging)
- [WPF、Silverlight 和控制台应用程序代码示例，用于服务器可以调用的客户端方法](#wpfsl)

有关示例 .NET 客户端项目，请参阅以下资源：

- [古斯塔沃-阿尔门塔 / 信号R-样本](https://github.com/gustavo-armenta/SignalR-Samples)GitHub.com（WinRT，银光，控制台应用程序示例）。
- [达米安爱德华兹 / 信号R-移动形状演示 / 移动形状.桌面](https://github.com/DamianEdwards/SignalR-MoveShapeDemo/tree/master/MoveShape/MoveShape.Desktop)GitHub.com （WPF 示例）。
- [信号R / 微软.AspNet.SignalR.客户端.GitHub.com上的样本](https://github.com/SignalR/SignalR/tree/master/samples/Microsoft.AspNet.SignalR.Client.Samples)（控制台应用示例）。

有关如何对服务器或 JavaScript 客户端进行编程的文档，请参阅以下资源：

- [信号器集线器 API 指南 - 服务器](hubs-api-guide-server.md)
- [信号器中心 API 指南 - JavaScript 客户端](hubs-api-guide-javascript-client.md)

指向 API 参考主题的链接指向 API 的 .NET 4.5 版本。 如果使用 .NET 4，请参阅[API 主题的 .NET 4 版本](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx)。

<a id="clientsetup"></a>

## <a name="client-setup"></a>客户端设置

安装[微软.AspNet.SignalR.客户端](http://nuget.org/packages/Microsoft.AspNet.SignalR.Client)NuGet 包（不是[微软.AspNet.SignalR](http://nuget.org/packages/microsoft.aspnet.signalr)包）。 此包支持 WinRT、Silverlight、WPF、控制台应用程序和 Windows Phone 客户端，适用于 .NET 4 和 .NET 4.5。

如果客户端上的 SignalR 版本与服务器上的版本不同，则 SignalR 通常能够适应差异。 例如，运行 SignalR 版本 2 的服务器将支持安装了 1.1.x 的客户端以及安装了版本 2 的客户端。 如果服务器上的版本和客户端上的版本之间的差异太大，或者如果客户端比服务器新，则在客户端尝试建立连接时，SignalR 会引发`InvalidOperationException`异常。 错误消息为""。`You are using a version of the client that isn't compatible with the server. Client version X.X, server version X.X`

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a>如何建立连接

在建立连接之前，必须创建对象`HubConnection`并创建代理。 要建立连接，请`Start`调用`HubConnection`对象上的方法。

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample1.cs?highlight=1,5)]

> [!NOTE]
> 对于 JavaScript 客户端，在调用方法建立连接之前，`Start`您必须至少注册一个事件处理程序。 对于 .NET 客户端，这不需要。 对于 JavaScript 客户端，生成的代理代码会自动为服务器上存在的所有中心创建代理，注册处理程序是指示客户端打算使用哪个集线器的方式。 但对于 .NET 客户端，您可以手动创建集线器代理，因此 SignalR 假定您将使用为其创建代理的任何集线器。

示例代码使用默认的"/信号器"URL 连接到您的 SignalR 服务。 有关如何指定其他基本 URL 的信息，请参阅[ASP.NET信号R中心 API 指南 - 服务器 - /signalr URL](hubs-api-guide-server.md#signalrurl)。

该方法`Start`以异步方式执行。 为了确保后续代码行在建立连接之前不会执行，请使用`await`ASP.NET 4.5 异步方法或`.Wait()`同步方法。 不要在 WinRT`.Wait()`客户端中使用。

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample2.cs?highlight=1)]

[!code-css[Main](hubs-api-guide-net-client/samples/sample3.css?highlight=1)]

<a id="slcrossdomain"></a>

### <a name="cross-domain-connections-from-silverlight-clients"></a>来自银光客户端的跨域连接

有关如何启用来自 Silverlight 客户端的跨域连接的信息，请参阅[使服务跨域边界可用](https://msdn.microsoft.com/library/cc197955(v=vs.95).aspx)。

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a>如何配置连接

在建立连接之前，可以指定以下任一选项：

- 并发连接限制。
- 查询字符串参数。
- 传输方法。
- HTTP 标头。
- 客户端证书。

<a id="maxconnections"></a>

### <a name="how-to-set-the-maximum-number-of-concurrent-connections-in-wpf-clients"></a>如何设置 WPF 客户端中的最大并发连接数

在 WPF 客户端中，您可能需要从默认值 2 增加并发连接的最大数量。 建议的值为 10。

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample4.cs?highlight=5)]

有关详细信息，请参阅[服务点管理器.默认连接限制](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx)。

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a>如何指定查询字符串参数

如果要在客户端连接时将数据发送到服务器，则可以向连接对象添加查询字符串参数。 下面的示例演示如何在客户端代码中设置查询字符串参数。

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample5.cs)]

下面的示例演示如何读取服务器代码中的查询字符串参数。

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample6.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a>如何指定传输方法

作为连接过程的一部分，SignalR 客户端通常与服务器协商以确定服务器和客户端支持的最佳传输。 如果您已经知道要使用的传输，可以绕过此协商过程。 要指定传输方法，请将传输对象传递给 Start 方法。 下面的示例演示如何在客户端代码中指定传输方法。

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample7.cs?highlight=5)]

[Microsoft.AspNet.SignalR.Client.传输](https://msdn.microsoft.com/library/jj918090(v=vs.111).aspx)命名空间包括以下类，可用于指定传输。

- [长轮询传输](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.longpollingtransport(v=vs.111).aspx)
- [服务器发送事件传输](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.serversenteventstransport(v=vs.111).aspx)
- [WebSocket 传输](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.websockettransport(v=vs.111).aspx)（仅在服务器和客户端使用 .NET 4.5 时可用。
- [自动传输](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.autotransport(v=vs.111).aspx)（自动选择客户端和服务器支持的最佳传输。 这是默认传输。 将此传递给`Start`方法的效果与不传入任何内容的效果相同。

ForeverFrame 传输不包括在此列表中，因为它仅由浏览器使用。

有关如何在服务器代码中检查传输方法的信息，请参阅[ASP.NET SignalR 集线器 API 指南 - 服务器 - 如何从 Context 属性获取有关客户端的信息](hubs-api-guide-server.md#contextproperty)。 有关传输和回退的详细信息，请参阅[信号R - 传输和回退简介](../getting-started/introduction-to-signalr.md#transports)。

<a id="httpheaders"></a>

### <a name="how-to-specify-http-headers"></a>如何指定 HTTP 标头

要设置 HTTP 标头，`Headers`请使用连接对象上的属性。 下面的示例演示如何添加 HTTP 标头。

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample8.cs?highlight=2)]

<a id="clientcertificate"></a>

### <a name="how-to-specify-client-certificates"></a>如何指定客户端证书

要添加客户端证书，`AddClientCertificate`请使用连接对象上的方法。

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample9.cs?highlight=2)]

<a id="proxy"></a>

## <a name="how-to-create-the-hub-proxy"></a>如何创建中心代理

为了在客户端上定义集线器可以从服务器调用的方法，并在服务器上的集线器上调用方法，请通过调用`CreateHubProxy`连接对象为集线器创建代理。 传递给的字符串`CreateHubProxy`是 Hub 类的名称，或者`HubName`属性指定的名称（如果在服务器上使用）。 名称匹配不区分大小写。

**服务器上的集线器类**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample10.cs?highlight=1)]

**为中心类创建客户端代理**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample11.cs?highlight=3)]

如果使用`HubName`属性修饰 Hub 类，请使用该名称。

**服务器上的集线器类**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample12.cs)]

**为中心类创建客户端代理**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample13.cs?highlight=3)]

如果使用相同的`HubConnection.CreateHubProxy``hubName`调用多次 ，则会获取相同的缓存`IHubProxy`对象。

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a>如何在客户端上定义服务器可以调用的方法

要定义服务器可以调用的方法，请使用代理`On`的方法注册事件处理程序。

方法名称匹配不区分大小写。 例如，`Clients.All.UpdateStockPrice`在服务器上将执行`updateStockPrice`、`updatestockprice`或`UpdateStockPrice`在客户端上。

不同的客户端平台对如何编写方法来更新 UI 有不同的要求。 显示的示例适用于 WinRT （Windows 应用商店 .NET） 客户端。 WPF、Silverlight 和控制台应用程序示例在本[主题后面的单独部分](#wpfsl)提供。

<a id="clientmethodswithoutparms"></a>

### <a name="methods-without-parameters"></a>没有参数的方法

如果正在处理的方法没有参数，请使用`On`方法的非泛型重载：

**服务器代码调用没有参数的客户端方法**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample14.cs?highlight=5)]

**WinRT 客户端代码用于从服务器调用没有参数的方法（[请参阅本主题后面的 WPF 和 Silverlight 示例](#wpfsl)）**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample15.cs)]

<a id="clientmethodswithparmtypes"></a>

### <a name="methods-with-parameters-specifying-the-parameter-types"></a>具有参数的方法，指定参数类型

如果要处理的方法具有参数，请指定参数的类型作为`On`方法的泛型类型。 `On`该方法有泛型重载，使您能够指定最多 8 个参数（Windows Phone 7 上的 4 个参数）。 在下面的示例中，一个参数发送到`UpdateStockPrice`方法。

**使用参数调用客户端方法的服务器代码**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample16.cs?highlight=3)]

**用于参数的 Stock 类**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample17.cs)]

**WinRT 客户端代码用于从具有参数的服务器调用的方法（[请参阅本主题后面的 WPF 和 Silverlight 示例](#wpfsl)）**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample18.cs?highlight=1,5)]

<a id="clientmethodswithdynamparms"></a>

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a>具有参数的方法，为参数指定动态对象

作为将参数指定为`On`方法的泛型类型的替代方法，可以将参数指定为动态对象：

**使用参数调用客户端方法的服务器代码**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample19.cs?highlight=3)]

**用于参数的 Stock 类**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample20.cs)]

**WinRT 客户端代码用于使用参数从服务器调用的方法，使用参数的动态对象（[请参阅本主题后面的 WPF 和 Silverlight 示例](#wpfsl)）**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample21.cs?highlight=1,5)]

<a id="removehandler"></a>

### <a name="how-to-remove-a-handler"></a>如何删除处理程序

要删除处理程序，请调用其`Dispose`方法。

**从服务器调用的方法的客户端代码**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample22.cs?highlight=1)]

**客户端代码以删除处理程序**

[!code-css[Main](hubs-api-guide-net-client/samples/sample23.css?highlight=1)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a>如何从客户端调用服务器方法

要在服务器上调用方法，`Invoke`请使用集线器代理上的方法。

如果服务器方法没有返回值，请使用`Invoke`方法的非泛型重载。

**没有返回值的方法的服务器代码**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample24.cs?highlight=3)]

**调用没有返回值的方法的客户端代码**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample25.cs?highlight=1)]

如果服务器方法具有返回值，请指定返回类型作为`Invoke`方法的泛型类型。

**具有返回值并采用复杂类型参数的方法的服务器代码**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample26.cs?highlight=1)]

**用于参数和返回值的 Stock 类**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample27.cs)]

**客户端代码调用具有返回值并采用复杂类型参数的方法，在 ASP.NET 4.5 异步方法中调用**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample28.cs?highlight=1-2)]

**客户端代码调用具有返回值并采用复杂类型参数的方法（在同步方法中）**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample29.cs?highlight=1-2)]

该方法`Invoke`异步执行并返回对象`Task`。 如果不指定`await`或`.Wait()`，则下一行代码将在调用的方法完成执行之前执行。

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a>如何处理连接生存期事件

SignalR 提供您可以处理的以下连接生存期事件：

- `Received`：在连接上收到任何数据时引发。 提供接收的数据。
- `ConnectionSlow`：当客户端检测到连接缓慢或频繁断开时引发。
- `Reconnecting`：当基础传输开始重新连接时引发。
- `Reconnected`：在基础传输重新连接时引发。
- `StateChanged`：当连接状态更改时引发。 提供旧状态和新状态。 有关连接状态值的信息，请参阅[连接状态枚举](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connectionstate(v=vs.111).aspx)。
- `Closed`：连接断开连接时引发。

例如，如果要显示未致命但会导致间歇性连接问题（如连接速度慢或频繁断开）的错误的警告消息，则处理该`ConnectionSlow`事件。

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample30.cs)]

有关详细信息，请参阅在[SignalR 中了解和处理连接生存期事件](handling-connection-lifetime-events.md)。

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a>如何处理错误

如果未在服务器上显式启用详细的错误消息，则 SignalR 在错误后返回的异常对象包含有关该错误的最少信息。 例如，如果调用`newContosoChatMessage`失败，错误对象中的错误消息包含"`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`出于安全原因不建议向生产中的客户端发送详细的错误消息，但如果要启用详细的错误消息以进行故障排除，请使用服务器上的以下代码。

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample31.cs?highlight=2)]

<a id="handleerrors"></a>

要处理 SignalR 引发的错误，可以在连接对象上为`Error`事件添加处理程序。

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample32.cs)]

要处理方法调用中的错误，请将代码包装在 try-catch 块中。

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample33.cs)]

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a>如何启用客户端日志记录

要启用客户端日志记录，在连接对象上`TraceLevel`设置`TraceWriter`和 属性。

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample34.cs?highlight=3-4)]

<a id="wpfsl"></a>

## <a name="wpf-silverlight-and-console-application-code-samples-for-client-methods-that-the-server-can-call"></a>WPF、Silverlight 和控制台应用程序代码示例，用于服务器可以调用的客户端方法

前面显示的代码示例用于定义服务器可以调用的客户端方法，应用于 WinRT 客户端。 以下示例显示了 WPF、Silverlight 和控制台应用程序客户端的等效代码。

### <a name="methods-without-parameters"></a>没有参数的方法

**WPF 客户端代码，用于从服务器调用无参数的方法**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample35.cs?highlight=1)]

**银光客户端代码，用于从服务器调用无参数的方法**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample36.cs?highlight=1)]

**控制台应用程序客户端代码，用于从服务器调用无参数的方法**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample37.cs?highlight=1)]

### <a name="methods-with-parameters-specifying-the-parameter-types"></a>具有参数的方法，指定参数类型

**WPF 客户端代码，用于从具有参数的服务器调用的方法**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample38.cs?highlight=1,4)]

**使用参数从服务器调用的方法的 Silverlight 客户端代码**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample39.cs?highlight=1,5)]

**控制台应用程序客户端代码，用于从具有参数的服务器调用的方法**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample40.cs?highlight=1-2)]

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a>具有参数的方法，为参数指定动态对象

**使用参数的动态对象从服务器调用的方法的 WPF 客户端代码**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample41.cs?highlight=1,4)]

**使用参数的动态对象从服务器调用的方法的 Silverlight 客户端代码**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample42.cs?highlight=1,5)]

**使用参数的动态对象从服务器调用的方法的控制台应用程序客户端代码**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample43.cs?highlight=1-2)]

---
uid: signalr/overview/older-versions/troubleshooting
title: 信号R故障排除（信号R 1.x） |微软文档
author: bradygaster
description: 本文介绍了开发SignalR应用的常见问题。
ms.author: bradyg
ms.date: 06/05/2013
ms.assetid: 347210ba-c452-4feb-886f-b51d89f58971
msc.legacyurl: /signalr/overview/older-versions/troubleshooting
msc.type: authoredcontent
ms.openlocfilehash: e65ce086d28cff2a36c609f47a05af632081be63
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543088"
---
# <a name="signalr-troubleshooting-signalr-1x"></a>SignalR 疑难解答 (SignalR 1.x)

由[帕特里克·弗莱彻](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 本文档介绍 SignalR 的常见故障排除问题。

本文档包含以下部分。

- [客户端和服务器之间的调用方法以静默方式失败](#connection)
- [其他连接问题](#other)
- [编译和服务器端错误](#server)
- [视觉工作室问题](#vs)
- [互联网信息服务问题](#iis)
- [Azure 问题](#azure)

<a id="connection"></a>

## <a name="calling-methods-between-the-client-and-server-silently-fails"></a>客户端和服务器之间的调用方法以静默方式失败

本节介绍客户端和服务器之间的方法调用失败而不出现有意义的错误消息的可能原因。 在 SignalR 应用程序中，服务器没有关于客户端实现的方法的信息;因此，服务器没有实现的方法。当服务器调用客户端方法时，方法名称和参数数据将发送到客户端，并且仅当该方法以服务器指定的格式存在时才执行该方法。 如果在客户端上找不到匹配方法，则不发生任何操作，并且服务器上不引发错误消息。

要进一步调查未被调用的客户端方法，可以在调用集线器上的 start 方法之前打开日志记录，以查看来自服务器的调用。 要在 JavaScript 应用程序中启用日志记录，请参阅[如何启用客户端日志记录（JavaScript 客户端版本）。](../guide-to-the-api/hubs-api-guide-javascript-client.md#logging) 要在 .NET 客户端应用程序中启用日志记录，请参阅[如何启用客户端日志记录 （.NET 客户端版本）。](../guide-to-the-api/hubs-api-guide-net-client.md#logging)

### <a name="misspelled-method-incorrect-method-signature-or-incorrect-hub-name"></a>拼写错误的方法、不正确的方法签名或不正确的中心名称

如果被调用方法的名称或签名与客户端上的适当方法不完全匹配，则调用将失败。 验证服务器调用的方法名称是否与客户端上的方法的名称匹配。 此外，SignalR 使用骆驼大小写方法创建集线器代理，这在 JavaScript 中是合适的`SendMessage`，因此在客户端代理中`sendMessage`调用服务器上调用的方法。 如果在服务器端代码`HubName`中使用该属性，请验证所使用的名称是否与在客户端上创建中心的名称匹配。 如果不使用 该`HubName`属性，请验证 JavaScript 客户端中中心的名称是否为骆驼大小写，例如聊天Hub而不是 ChatHub。

### <a name="duplicate-method-name-on-client"></a>客户端上的重复方法名称

验证客户端上没有仅因大小写而异的重复方法。 如果客户端应用程序具有称为`sendMessage`的方法，请验证是否也没有调用`SendMessage`的方法。

### <a name="missing-json-parser-on-the-client"></a>客户端上缺少 JSON 解析器

SignalR 需要 JSON 解析器存在以序列化服务器和客户端之间的呼叫。 如果客户端没有内置的 JSON 解析器（如 Internet Explorer 7），则需要在应用程序中包含一个。 你可以[在这里](http://nuget.org/packages/json2)下载JSON解析器。

### <a name="mixing-hub-and-persistentconnection-syntax"></a>混合集线器和持久连接语法

SignalR 使用两种通信模型：集线器和持久连接。 调用这两种通信模型的语法在客户端代码中是不同的。 如果在服务器代码中添加了中心，请验证所有客户端代码是否使用正确的中心语法。

**在 JavaScript 客户端中创建持久连接的 JavaScript 客户端代码**

[!code-javascript[Main](troubleshooting/samples/sample1.js)]

**在 Javascript 客户端中创建中心代理的 JavaScript 客户端代码**

[!code-javascript[Main](troubleshooting/samples/sample2.js)]

**将路由映射到持久连接的 C# 服务器代码**

[!code-csharp[Main](troubleshooting/samples/sample3.cs)]

**C# 服务器代码，用于将路由映射到集线器，或者如果您有多个应用程序，则映射到多个集线器**

[!code-csharp[Main](troubleshooting/samples/sample4.cs)]

### <a name="connection-started-before-subscriptions-are-added"></a>添加订阅之前启动的连接

如果在将可以从服务器调用的方法添加到代理之前启动中心连接，将不会接收消息。 以下 JavaScript 代码将无法正确启动中心：

**不正确的 JavaScript 客户端代码，不允许接收中心消息**

[!code-javascript[Main](troubleshooting/samples/sample5.js)]

而是在调用"开始"之前添加方法订阅：

**正确将订阅添加到中心的 JavaScript 客户端代码**

[!code-javascript[Main](troubleshooting/samples/sample6.js)]

### <a name="missing-method-name-on-the-hub-proxy"></a>中心代理上缺少方法名称

验证在服务器上定义的方法是否订阅在客户端上。 即使服务器定义了该方法，仍必须将其添加到客户端代理中。 方法可以通过以下方式添加到客户端代理（请注意，该方法已添加到中心`client`成员，而不是直接添加到中心）：

**将方法添加到中心代理的 JavaScript 客户端代码**

[!code-javascript[Main](troubleshooting/samples/sample7.js)]

### <a name="hub-or-hub-methods-not-declared-as-public"></a>未声明为公共的集线器或中心方法

要在客户端上可见，必须将中心实现和方法声明为`public`。

### <a name="accessing-hub-from-a-different-application"></a>从其他应用程序访问集线器

信号R中心只能通过实现SignalR客户端的应用程序进行访问。 SignalR 不能与其他通信库（如 SOAP 或 WCF Web 服务）互操作。如果目标平台没有可用的 SignalR 客户端，则无法直接访问服务器的终结点。

### <a name="manually-serializing-data"></a>手动序列化数据

SignalR 将自动使用 JSON 来序列化方法参数 - 无需自行执行。

### <a name="remote-hub-method-not-executed-on-client-in-ondisconnected-function"></a>在 OnDisconnected 函数中的客户端上未执行远程中心方法

这是设计的行为。 调用`OnDisconnected`时，中心已进入状态`Disconnected`，不允许调用其他集线器方法。

**C# 服务器代码，在"不断开"事件中正确执行代码**

[!code-csharp[Main](troubleshooting/samples/sample8.cs)]

### <a name="connection-limit-reached"></a>达到连接限制

在 Windows 7 等客户端操作系统上使用完整版本的 IIS 时，将强制实施 10 个连接限制。 使用客户端操作系统时，请使用 IIS Express 来避免此限制。

### <a name="cross-domain-connection-not-set-up-properly"></a>跨域连接设置不正确

如果跨域连接（SignalR URL 与托管页不在同一域中的连接）设置不正确，则连接可能会失败，而不会出现错误消息。 有关如何启用跨域通信的信息，请参阅[如何建立跨域连接](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)。

### <a name="connection-using-ntlm-active-directory-not-working-in-net-client"></a>使用 NTLM（活动目录）在 .NET 客户端中不起作用的连接

如果连接配置不正确，则使用域安全的 .NET 客户端应用程序中的连接可能会失败。 要在域环境中使用 SignalR，请使用如下方式设置所需的连接属性：

**实现连接凭据的 C# 客户端代码**

[!code-csharp[Main](troubleshooting/samples/sample9.cs)]

<a id="other"></a>

## <a name="other-connection-issues"></a>其他连接问题

本节介绍连接过程中发生的特定症状或错误消息的原因和解决方案。

### <a name="start-must-be-called-before-data-can-be-sent-error"></a>"必须先调用开始才能发送数据"错误

如果代码在连接启动之前引用 SignalR 对象，则通常可以看到此错误。 必须在连接完成后添加处理程序的布线等调用服务器上定义的调用方法。 请注意，调用`Start`是异步的，因此在调用完成之前可以执行调用后的代码。 在连接完全启动后添加处理程序的最佳方法是将它们放入回调函数中，该函数作为参数传递给 start 方法：

**正确添加引用 SignalR 对象的事件处理程序的 JavaScript 客户端代码**

[!code-javascript[Main](troubleshooting/samples/sample10.js?highlight=1)]

如果连接在仍在引用 SignalR 对象时停止，也会看到此错误。

### <a name="301-moved-permanently-or-302-moved-temporarily-error"></a>"301 永久移动"或"302 临时移动"错误

如果项目包含名为 SignalR 的文件夹，则可能会看到此错误，这将干扰自动创建的代理。 为了避免此错误，请勿使用应用程序中调用`SignalR`的文件夹，或关闭自动代理生成。 有关详细信息[，请参阅生成的代理及其为您做什么](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy)。

### <a name="403-forbidden-error-in-net-or-silverlight-client"></a>.NET 或银光客户端中的"403 禁止"错误

此错误可能发生在跨域环境中，其中跨域通信未正确启用。 有关如何启用跨域通信的信息，请参阅[如何建立跨域连接](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)。 要在 Silverlight 客户端中建立跨域连接，请参阅[来自 Silverlight 客户端的跨域连接](../guide-to-the-api/hubs-api-guide-net-client.md#slcrossdomain)。

### <a name="404-not-found-error"></a>"404 未找到"错误

此问题有多种原因。 验证以下所有情况：

- **中心代理地址引用格式不正确：** 如果对生成的中心代理地址的引用格式不正确，则通常可以看到此错误。 验证对中心地址的引用是否正确。 有关详细信息[，请参阅如何引用动态生成的代理](../guide-to-the-api/hubs-api-guide-javascript-client.md#dynamicproxy)。
- **在添加中心路由之前向应用程序添加路由：** 如果应用程序使用其他路由，请验证添加的第一个路由是否调用`MapHubs`。

### <a name="500-internal-server-error"></a>"500 内部服务器错误"

这是一个非常通用的错误，可能有各种各样的原因。 错误的详细信息应出现在服务器的事件日志中，或者可以通过调试服务器找到。 通过在服务器上打开详细的错误，可以获得更详细的错误信息。 有关详细信息，请参阅如何处理[Hub 类中的错误](../guide-to-the-api/hubs-api-guide-server.md#handleErrors)。

### <a name="typeerror-lthubtypegt-is-undefined-error"></a>"类型错误：&lt;中心类型&gt;未定义"错误

如果调用`MapHubs`不正确，将导致此错误。 有关详细信息[，请参阅如何注册 SignalR 路由和配置 SignalR 选项](../guide-to-the-api/hubs-api-guide-server.md#route)。

### <a name="jsonserializationexception-was-unhandled-by-user-code"></a>用户代码未处理 Json 序列化异常

验证发送到方法的参数是否不包括不可序列化的类型（如文件句柄或数据库连接）。 如果需要在不希望发送到客户端的服务器端对象上使用成员（出于安全性或序列化原因），请使用 该`JSONIgnore`属性。

### <a name="protocol-error-unknown-transport-error"></a>"协议错误：未知传输"错误

如果客户端不支持 SignalR 使用的传输，则可能发生此错误。 有关哪些浏览器可与 SignalR 一起使用的信息，请参阅[传输和回退](../getting-started/introduction-to-signalr.md#transports)。

### <a name="javascript-hub-proxy-generation-has-been-disabled"></a>"JavaScript 中心代理生成已被禁用。

如果`DisableJavaScriptProxies`设置时将发生此错误，同时还包括对 动态生成的代理的`signalr/hubs`引用。 有关手动创建代理的详细信息，请参阅[生成的代理及其为您做什么](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy)。

### <a name="the-connection-id-is-in-the-incorrect-format-or-the-user-identity-cannot-change-during-an-active-signalr-connection-error"></a>"连接 ID 格式不正确"或"用户身份在活动 SignalR 连接期间无法更改"错误

如果正在使用身份验证，并且客户端在停止连接之前注销，则可能会看到此错误。 解决方案是在注销客户端之前停止 SignalR 连接。

### <a name="uncaught-error-signalr-jquery-not-found-please-ensure-jquery-is-referenced-before-the-signalrjs-file-error"></a>"未捕获错误：信号R：找不到 jQuery。 请确保在 SignalR.js 文件"错误之前引用 jQuery

SignalR JavaScript 客户端需要 jQuery 才能运行。 验证对 jQuery 的引用是否正确，使用的路径是否有效，以及对 jQuery 的引用是否位于对 SignalR 的引用之前。

### <a name="uncaught-typeerror-cannot-read-property-ltpropertygt-of-undefined-error"></a>"未捕获的类型错误：无法读取属性'&lt;属性&gt;'未定义"错误

此错误导致没有正确引用 jQuery 或中心代理。 验证对 jQuery 和集线器代理的引用是否正确，使用的路径是否有效，以及对 jQuery 的引用是否位于对集线器代理的引用之前。 对集线器代理的默认引用应如下所示：

**正确引用中心代理的 HTML 客户端代码**

[!code-html[Main](troubleshooting/samples/sample11.html)]

### <a name="runtimebinderexception-was-unhandled-by-user-code-error"></a>"运行时Binder异常未由用户代码处理"错误

当使用不正确的重载`Hub.On`时，可能会出现此错误。 如果方法具有返回值，则必须将返回类型指定为泛型类型参数：

**在客户端上定义的方法（没有生成的代理）**

[!code-html[Main](troubleshooting/samples/sample12.html?highlight=1)]

### <a name="connection-id-is-inconsistent-or-connection-breaks-between-page-loads"></a>连接 ID 不一致或页面加载之间的连接中断

这是设计的行为。 由于中心对象托管在页面对象中，因此在页面刷新时将销毁中心。 多页应用程序需要维护用户和连接指示之间的关联，以便它们在页面加载之间保持一致。 连接指示可以存储在`ConcurrentDictionary`对象或数据库中的服务器上。

### <a name="value-cannot-be-null-error"></a>"值不能为空"错误

当前不支持具有可选参数的服务器端方法;如果省略可选参数，该方法将失败。 有关详细信息，请参阅[可选参数](https://github.com/SignalR/SignalR/issues/324)。

### <a name="firefox-cant-establish-a-connection-to-the-server-at-ltaddressgt-error-in-firebug"></a>"Firefox 无法在&lt;地址&gt;建立与服务器的连接"Firebug 中的错误

如果 WebSocket 传输协商失败，并且使用另一个传输，可以在 Firebug 中看到此错误消息。 这是设计的行为。

### <a name="the-remote-certificate-is-invalid-according-to-the-validation-procedure-error-in-net-client-application"></a>.NET 客户端应用程序中的"远程证书根据验证过程无效"错误

如果服务器需要自定义客户端证书，则可以在发出请求之前向连接添加 x509 证书。 使用 将证书添加到连接中`Connection.AddClientCertificate`。

### <a name="connection-drops-after-authentication-times-out"></a>身份验证超时后连接断开

这是设计的行为。 当连接处于活动状态时，无法修改身份验证凭据;要刷新凭据，必须停止并重新启动连接。

### <a name="onconnected-gets-called-twice-when-using-jquery-mobile"></a>使用 jQuery 移动时，OnConnected 被调用两次

jQuery Mobile`initializePage`的功能强制重新执行每个页面中的脚本，从而创建第二个连接。 此问题的解决方案包括：

- 在 JavaScript 文件之前包括对 jQuery 移动的引用。
- 通过设置`initializePage``$.mobile.autoInitializePage = false`禁用 函数。
- 在开始连接之前，等待页面完成初始化。

### <a name="messages-are-delayed-in-silverlight-applications-using-server-sent-events"></a>使用服务器发送事件在 Silverlight 应用程序中延迟消息

在 Silverlight 上使用服务器发送的事件时，消息会延迟。 要强制使用长轮询，在启动连接时使用以下内容：

[!code-css[Main](troubleshooting/samples/sample13.css)]

### <a name="permission-denied-using-forever-frame-protocol"></a>使用永久帧协议"拒绝权限"

这是一个已知的问题，[此处](https://github.com/SignalR/SignalR/issues/1963)描述。 可以使用最新的 JQuery 库看到此症状;解决方法是将应用程序降级为 JQuery 1.8.2。

<a id="server"></a>

## <a name="compilation-and-server-side-errors"></a>编译和服务器端错误

 以下部分包含编译器和服务器端运行时错误的可能解决方案。 

### <a name="reference-to-hub-instance-is-null"></a>对中心实例的引用为空

由于为每个连接创建了一个中心实例，因此无法自己在代码中创建集线器的实例。 要从中心外部调用方法，请参阅[如何调用客户端方法并从中心类外部管理组](../guide-to-the-api/hubs-api-guide-server.md#callfromoutsidehub)，了解如何获取对中心上下文的引用。

### <a name="httpcontextcurrentsession-is-null"></a>HTTPContext.当前.会话为空

这是设计的行为。 SignalR 不支持ASP.NET会话状态，因为启用会话状态将中断双工消息。

### <a name="no-suitable-method-to-override"></a>没有合适的方法可以重写

如果您使用的是来自旧文档或博客的代码，则可能会看到此错误。 验证您没有引用已更改或弃用的方法的名称（如`OnConnectedAsync`）。

### <a name="hostcontextextensionswebsocketserverurl-is-null"></a>主机上下文扩展.WebSocket服务器Url为空

这是设计的行为。 此成员已弃用，不应使用。

### <a name="a-route-named-signalrhubs-is-already-in-the-route-collection-error"></a>"名为"Signalr.hubs"的路由已在路由集合中"错误

如果`MapHubs`应用程序调用了两次，则将看到此错误。 一些示例应用程序`MapHubs`直接调用全局应用程序文件中;其他人在包装类中进行调用。 确保应用程序不同时执行这两种操作。

<a id="vs"></a>

## <a name="visual-studio-issues"></a>视觉工作室问题

本节介绍视觉工作室中遇到的问题。

### <a name="script-documents-node-does-not-appear-in-solution-explorer"></a>脚本文档节点未显示在解决方案资源管理器中

我们的一些教程将引导您到解决方案资源管理器中的"脚本文档"节点进行调试。 此节点由 JavaScript 调试器生成，仅在 Internet 资源管理器中调试浏览器客户端时出现;如果使用 Chrome 或 Firefox，将不会显示该节点。 如果运行了另一个客户端调试器（如 Silverlight 调试器），JavaScript 调试器也不会运行。

### <a name="signalr-does-not-work-on-visual-studio-2008-or-earlier"></a>信号R在视觉工作室 2008 或更早版本上不起作用

这是设计的行为。 信号R需要 .NET 框架 4 或更高版本;这要求在 Visual Studio 2010 或更高版本中开发 SignalR 应用程序。

<a id="iis"></a>

## <a name="iis-issues"></a>IIS 问题

本节包含互联网信息服务的问题。

### <a name="web-site-crashes-after-maphubs-call"></a>地图中心调用后网站崩溃

此问题已在最新版本的 SignalR 中修复。 使用 NuGet 更新安装，验证您使用的是最新版本的 SignalR。

<a id="azure"></a>

## <a name="azure-issues"></a>Azure 问题

本节包含 Microsoft Azure 的问题。

### <a name="messages-are-not-received-through-the-azure-backplane-after-altering-topic-names"></a>更改主题名称后，不会通过 Azure 背板接收消息

Azure 背板使用的主题不用于用户配置。

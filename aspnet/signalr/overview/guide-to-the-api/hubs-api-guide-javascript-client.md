---
uid: signalr/overview/guide-to-the-api/hubs-api-guide-javascript-client
title: ASP.NET SignalR 中心 API 指南-JavaScript 客户端 |Microsoft Docs
author: bradygaster
description: 本文档介绍了如何使用 JavaScript 客户端（如浏览器和 Windows 应用商店 (WinJS) applicat .。。
ms.author: bradyg
ms.date: 01/15/2019
ms.assetid: a9fd4dc0-1b96-4443-82ca-932a5b4a8ea4
msc.legacyurl: /signalr/overview/guide-to-the-api/hubs-api-guide-javascript-client
msc.type: authoredcontent
ms.openlocfilehash: 8befe133c3627dac1f7d011959c68e2054d345da
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345434"
---
# <a name="aspnet-signalr-hubs-api-guide---javascript-client"></a>ASP.NET SignalR 中心 API 指南-JavaScript 客户端

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 本文档介绍了如何在 JavaScript 客户端（如浏览器和 Windows 应用商店 (WinJS) 应用程序）中使用适用于 SignalR 版本2的中心 API。
>
> 通过 SignalR 中心 API，你可以 (Rpc) 从服务器连接到连接的客户端和从客户端到服务器的远程过程调用。 在服务器代码中，你将定义可由客户端调用的方法，并调用在客户端上运行的方法。 在客户端代码中，定义可从服务器调用的方法，并调用在服务器上运行的方法。 SignalR 负责处理所有的客户端到服务器的操作。
>
> SignalR 还提供名为持久性连接的较低级别 API。 有关 SignalR、集线器和持续连接的简介，请参阅 [SignalR 简介](../getting-started/introduction-to-signalr.md)。
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

本文档包含以下各节：

- [生成的代理以及它为你执行的操作](#genproxy)

    - [何时使用生成的代理](#cantusegenproxy)
- [客户端设置](#clientsetup)

    - [如何引用动态生成的代理](#dynamicproxy)
    - [如何为 SignalR 生成的代理创建物理文件](#manualproxy)
- [如何建立连接](#establishconnection)

    - [$. 连接中心是与 hubConnection ( # A1 创建的对象相同的对象。](#connequivalence)
    - [开始方法的异步执行](#asyncstart)
- [如何建立跨域连接](#crossdomain)
- [如何配置连接](#configureconnection)

    - [如何指定查询字符串参数](#querystring)
    - [如何指定传输方法](#transport)
- [如何获取集线器类的代理](#getproxy)
- [如何在客户端上定义服务器可以调用的方法](#callclient)
- [如何从客户端调用服务器方法](#callserver)
- [如何处理连接生存期事件](#connectionlifetime)
- [如何处理错误](#handleerrors)
- [如何启用客户端日志记录](#logging)

有关如何对服务器或 .NET 客户端进行编程的文档，请参阅以下资源：

- [SignalR 中心 API 指南-服务器](hubs-api-guide-server.md)
- [SignalR 中心 API 指南-.NET 客户端](hubs-api-guide-net-client.md)

SignalR 2 服务器组件仅适用于 .NET 4.5 (但 .net 4.0) 上有一个用于 SignalR 2 的 .NET 客户端。

<a id="genproxy"></a>

## <a name="the-generated-proxy-and-what-it-does-for-you"></a>生成的代理以及它为你执行的操作

你可以对 JavaScript 客户端进行编程，以便使用或不使用 SignalR 生成的代理来与 SignalR 服务进行通信。 代理的作用是简化用于连接的代码的语法，编写服务器调用的方法，并在服务器上调用方法。

当你编写代码来调用服务器方法时，生成的代理使你能够使用类似于你执行本地函数的语法：你可以编写 `serverMethod(arg1, arg2)` 而不是 `invoke('serverMethod', arg1, arg2)` 。 如果错误键入服务器方法名称，生成的代理语法还会启用立即和可识别的客户端错误。 如果手动创建定义代理的文件，还可以获取对编写调用服务器方法的代码的 IntelliSense 支持。

例如，假设您在服务器上具有以下中心类：

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample1.cs?highlight=1,3,5)]

下面的代码示例演示了 `NewContosoChatMessage` 在服务器上调用方法以及从服务器接收方法调用时，JavaScript 代码的外观 `addContosoChatMessageToPage` 。

**与生成的代理**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample2.js?highlight=1-2,8)]

**没有生成的代理**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample3.js?highlight=2-3,9)]

<a id="cantusegenproxy"></a>

### <a name="when-to-use-the-generated-proxy"></a>何时使用生成的代理

如果要为服务器调用的客户端方法注册多个事件处理程序，则不能使用生成的代理。 否则，你可以选择使用生成的代理，而不是基于编码首选项。 如果选择不使用此方法，则无需在 `script` 客户端代码中引用元素中的 "signalr/hub" URL。

<a id="clientsetup"></a>

## <a name="client-setup"></a>客户端设置

JavaScript 客户端需要引用 jQuery 和 SignalR core JavaScript 文件。 JQuery 版本必须是1.6.4 或主要版本，如1.7.2、1.8.2 或1.9.1。 如果决定使用生成的代理，则还需要引用 SignalR 生成的代理 JavaScript 文件。 下面的示例演示在使用生成的代理的 HTML 页中，引用可能如下所示。

[!code-html[Main](hubs-api-guide-javascript-client/samples/sample4.html)]

这些引用必须按以下顺序包含： jQuery first、SignalR core 之后，以及 SignalR 代理 last。

<a id="dynamicproxy"></a>

### <a name="how-to-reference-the-dynamically-generated-proxy"></a>如何引用动态生成的代理

在前面的示例中，对 SignalR 生成的代理的引用是动态生成的 JavaScript 代码，而不是物理文件。 SignalR 会动态地为代理创建 JavaScript 代码，并将其提供给客户端，以响应 "/signalr/hubs" URL。 如果你在方法中为服务器上的 SignalR 连接指定了不同的基 URL `MapSignalR` ，则动态生成的代理文件的 url 是自定义 url，后面追加了 "/hubs"。

> [!NOTE]
> 对于 Windows 8 (Windows 应用商店) JavaScript 客户端，请使用物理代理文件而不是动态生成的文件。 有关详细信息，请参阅本主题后面的 [如何为 SignalR 生成的代理创建物理文件](#manualproxy) 。

在 ASP.NET MVC 4 或 5 Razor 视图中，使用波形符在代理文件引用中引用应用程序根目录：

[!code-html[Main](hubs-api-guide-javascript-client/samples/sample5.html)]

有关在 MVC 5 中使用 SignalR 的详细信息，请参阅 [使用 SignalR 和 MVC 5 入门](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)。

在 ASP.NET MVC 3 Razor 视图中，将用作 `Url.Content` 代理文件参考：

[!code-cshtml[Main](hubs-api-guide-javascript-client/samples/sample6.cshtml)]

在 ASP.NET Web 窗体应用程序中， `ResolveClientUrl` 为代理文件引用使用，或使用应用根相对路径通过 ScriptManager 注册它， (以颚化) 开头：

[!code-aspx[Main](hubs-api-guide-javascript-client/samples/sample7.aspx)]

作为一般规则，请使用与指定用于 CSS 或 JavaScript 文件的 "/signalr/hubs" URL 相同的方法。 如果在不使用波形符的情况下指定 URL，则在 Visual Studio 中使用 IIS Express 进行测试时，应用程序将正常工作，但在部署到完整 IIS 时将失败并出现404错误。 有关详细信息，请参阅 MSDN 网站上的在[Visual Studio for ASP.NET Web 项目的 Web 服务器中](https://msdn.microsoft.com/library/58wxa9w5.aspx)**解析对 Root-Level 资源的引用**。

在调试模式下运行 Visual Studio 2017 中的 web 项目时，如果使用 Internet Explorer 作为浏览器，则可以在 "**脚本**" 下的**解决方案资源管理器**中查看该代理文件。

若要查看文件的内容，请双击 " **中心**"。 如果使用的不是 Visual Studio 2012 或2013和 Internet Explorer，或者不处于调试模式，还可以通过浏览到 "/signalR/hubs" URL 来获取文件的内容。 例如，如果你的站点运行于 `http://localhost:56699` ，请 `http://localhost:56699/SignalR/hubs` 在浏览器中转到。

<a id="manualproxy"></a>

### <a name="how-to-create-a-physical-file-for-the-signalr-generated-proxy"></a>如何为 SignalR 生成的代理创建物理文件

作为动态生成的代理的替代方法，可以创建包含代理代码的物理文件，并引用该文件。 您可能想要执行此操作以控制缓存或绑定行为，或者在编码对服务器方法的调用时获取 IntelliSense。

若要创建代理文件，请执行以下步骤：

1. 安装 [SignalR. Utils](https://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/) NuGet 包。
2. 打开命令提示符，浏览到包含 SignalR.exe 文件的 " *工具* " 文件夹。 "工具" 文件夹位于以下位置：

    `[your solution folder]\packages\Microsoft.AspNet.SignalR.Utils.2.1.0\tools`
3. 输入以下命令：

    `signalr ghp /path:[path to the .dll that contains your Hub class]`

    *.Dll*的路径通常为项目文件夹中的*bin*文件夹。

    此命令在*signalr.exe*所在的文件夹中创建一个名为*server.js*的文件。
4. 将 *server.js* 文件放在项目中的适当文件夹中，将其重命名为适用于你的应用程序的，并在 "signalr/hub" 引用的位置添加对该文件的引用。

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a>如何建立连接

建立连接之前，必须先创建连接对象、创建代理，并为可从服务器调用的方法注册事件处理程序。 如果设置了代理和事件处理程序，则通过调用方法来建立连接 `start` 。

如果使用生成的代理，则无需在自己的代码中创建连接对象，因为生成的代理代码会为你执行该连接。

<a id="nogenconnection"></a>

**使用生成的代理建立连接 () **

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample8.js?highlight=5)]

**建立连接 (没有生成的代理) **

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample9.js?highlight=1,6)]

示例代码使用默认的 "/signalr" URL 连接到 SignalR 服务。 有关如何指定其他基 URL 的信息，请参阅 [ASP.NET SignalR HUB API 指南-Server-/SIGNALR URL](hubs-api-guide-server.md#signalrurl)。

默认情况下，中心位置是当前服务器;如果要连接到其他服务器，请在调用方法之前指定 URL `start` ，如以下示例中所示：

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample10.js)]

> [!NOTE]
> 通常，在调用方法之前注册事件处理程序 `start` 以建立连接。 如果要在建立连接后注册某些事件处理程序，则可以这样做，但必须在调用方法之前注册至少一个 () 事件处理程序 `start` 。 导致这种情况的原因之一是，应用程序中可以有很多的中心，但 `OnConnected` 如果只打算使用其中一种，则不希望在每个中心触发事件。 建立连接后，在集线器代理上存在客户端方法会告诉 SignalR 触发 `OnConnected` 事件。 如果在调用方法之前未注册任何事件处理程序 `start` ，则可以在中心调用方法，但不会调用中心的方法，也 `OnConnected` 不会从服务器中调用任何客户端方法。

<a id="connequivalence"></a>

### <a name="connectionhub-is-the-same-object-that-hubconnection-creates"></a>$. 连接中心是与 hubConnection ( # A1 创建的对象相同的对象。

如示例中所示，当你使用生成的代理时， `$.connection.hub` 引用连接对象。 这是你在 `$.hubConnection()` 不使用生成的代理时调用的相同对象。 生成的代理代码通过执行以下语句来创建连接：

![在生成的代理文件中创建连接](hubs-api-guide-javascript-client/_static/image3.png)

当你使用生成的代理时，你可以对使用连接对象执行的任何操作进行操作， `$.connection.hub` 而不是使用生成的代理。

<a id="asyncstart"></a>

### <a name="asynchronous-execution-of-the-start-method"></a>开始方法的异步执行

`start`方法以异步方式执行。 它返回 [JQuery 延迟的对象](http://api.jquery.com/category/deferred-object/)，这意味着你可以通过调用、和等方法添加回调函数 `pipe` `done` `fail` 。 如果你有想要在建立连接后执行的代码（例如，对服务器方法的调用），请将该代码放入回调函数或从回调函数调用它。 在 `.done` 建立连接后，以及在 `OnConnected` 服务器上的事件处理程序方法中的任何代码执行完毕后，将执行该回调方法。

如果将前面的示例中的 "现在连接的" 语句作为方法调用之后的下一行代码 `start` (不在 `.done` 回调) 中，则在 `console.log` 建立连接之前，将执行该行，如以下示例中所示：

![编写在建立连接后运行的代码的错误方法](hubs-api-guide-javascript-client/_static/image5.png)

<a id="crossdomain"></a>

## <a name="how-to-establish-a-cross-domain-connection"></a>如何建立跨域连接

通常，当浏览器从加载页面时 `http://contoso.com` ，SignalR 连接位于同一域中 `http://contoso.com/signalr` 。 如果中的页 `http://contoso.com` 建立了到的连接 `http://fabrikam.com/signalr` ，则这是一个跨域连接。 出于安全原因，在默认情况下将禁用跨域连接。

在 SignalR 1.x 中，跨域请求由单个 EnableCrossDomain 标志控制。 此标志控制 JSONP 和 CORS 请求。 为了获得更大的灵活性，已从 SignalR 的服务器组件中删除了所有 CORS 支持 (JavaScript 客户端在检测到浏览器支持它) 时仍使用 CORS，并提供新的 OWIN 中间件以支持这些方案。

如果客户端 (需要 JSONP 以支持较早浏览器) 中的跨域请求，则需要通过将对象上的设置为来显式启用此功能 `EnableJSONP` `HubConfiguration` `true` ，如下所示。 默认情况下，JSONP 处于禁用状态，因为它的安全性低于 CORS。

**将 Owin 添加到你的项目：** 若要安装此库，请在包管理器控制台中运行以下命令：

`Install-Package Microsoft.Owin.Cors`

此命令会将2.1.0 版本的包添加到你的项目。

### <a name="calling-usecors"></a>调用 UseCors

 下面的代码段演示如何在 SignalR 2 中实现跨域连接。

**在 SignalR 2 中实现跨域请求**

下面的代码演示如何在 SignalR 2 项目中启用 CORS 或 JSONP。 此代码示例使用 `Map` 和 `RunSignalR` 而不是 `MapSignalR` ，因此，CORS 中间件仅针对需要 CORS 支持 (而不是对中指定的路径中的所有流量运行的 SignalR 请求运行 `MapSignalR` 。 ) 映射还可用于需要针对特定 URL 前缀运行的任何其他中间件，而不是针对整个应用程序。

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample11.cs)]

> [!NOTE]
>
> - 不要 `jQuery.support.cors` 在代码中将设置为 true。
>
>     ![请勿将 jQuery. 支持 cors 设置为 true](hubs-api-guide-javascript-client/_static/image7.png)
>
>     SignalR 处理 CORS 的使用。 如果将设置 `jQuery.support.cors` 为 true，则将禁用 JSONP，因为它会导致 SignalR 假定浏览器支持 CORS。
> - 当你连接到 localhost URL 时，Internet Explorer 10 不会将其视为跨域连接，因此，即使你未在服务器上启用跨域连接，应用程序也会在本地使用 IE 10。
> - 有关使用 Internet Explorer 9 的跨域连接的信息，请参阅 [此 StackOverflow 线程](http://stackoverflow.com/questions/13573397/siganlr-ie9-cross-domain-request-dont-work)。
> - 有关将跨域连接与 Chrome 一起使用的信息，请参阅 [此 StackOverflow 线程](http://stackoverflow.com/questions/15467373/signalr-1-0-1-cross-domain-request-cors-with-chrome)。
> - 示例代码使用默认的 "/signalr" URL 连接到 SignalR 服务。 有关如何指定其他基 URL 的信息，请参阅 [ASP.NET SignalR HUB API 指南-Server-/SIGNALR URL](hubs-api-guide-server.md#signalrurl)。

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a>如何配置连接

在建立连接之前，您可以指定查询字符串参数或指定传输方法。

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a>如何指定查询字符串参数

如果要在客户端连接时将数据发送到服务器，则可以将查询字符串参数添加到连接对象。 下面的示例演示如何在客户端代码中设置查询字符串参数。

**在调用 start 方法 (与生成的代理) 之前设置查询字符串值 **

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample12.js?highlight=1)]

**在调用 start 方法之前设置查询字符串值，不 (生成的代理) **

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample13.js?highlight=2)]

下面的示例演示如何读取服务器代码中的查询字符串参数。

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample14.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a>如何指定传输方法

作为连接过程的一部分，SignalR 客户端通常与服务器协商以确定服务器和客户端支持的最佳传输。 如果已知道要使用的传输，则可以在调用方法时指定传输方法，绕过此协商过程 `start` 。

**指定传输方法与生成的代理 (的客户端代码) **

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample15.js?highlight=1)]

**指定传输方法的客户端代码 (没有生成的代理) **

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample16.js?highlight=2)]

作为替代方法，你可以按你希望 SignalR 尝试的顺序指定多个传输方法：

**指定自定义传输回退方案 (与生成的代理) 的客户端代码 **

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample17.js?highlight=1)]

**指定自定义传输回退方案 (的客户端代码，不包含生成的代理) **

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample18.js?highlight=2)]

您可以使用以下值来指定传输方法：

- Websocket
- "foreverFrame"
- "serverSentEvents"
- "longPolling"

下面的示例演示如何查明某个连接正在使用哪种传输方法。

**显示连接所使用的传输方法的客户端代码 (与生成的代理) **

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample19.js?highlight=2)]

**显示连接 (使用的传输方法的客户端代码，不包含生成的代理) **

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample20.js?highlight=3)]

有关如何在服务器代码中检查传输方法的信息，请参阅 [ASP.NET SignalR HUB API 指南-服务器-如何从上下文属性获取有关客户端的信息](hubs-api-guide-server.md#contextproperty)。 有关传输和回退的详细信息，请参阅 [SignalR-传输和回退简介](../getting-started/introduction-to-signalr.md#transports)。

<a id="getproxy"></a>

## <a name="how-to-get-a-proxy-for-a-hub-class"></a>如何获取集线器类的代理

你创建的每个连接对象将封装有关与包含一个或多个中心类的 SignalR 服务的连接的信息。 若要与 Hub 类通信，可以使用自己创建的代理对象 (如果你未使用生成的代理) 或为你生成。

在客户端上，代理名称为集线器类名的 camel 大小写形式。 SignalR 会自动进行此更改，以便 JavaScript 代码可以符合 JavaScript 约定。

**服务器上的中心类**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample21.cs?highlight=1)]

**获取对中心生成的客户端代理的引用**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample22.js?highlight=1)]

**为集线器类 (创建客户端代理，但不生成代理) **

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample23.cs?highlight=1)]

如果使用属性修饰中心类 `HubName` ，请使用完全相同的名称，但不更改大小写。

**服务器上具有 HubName 属性的中心类**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample24.cs?highlight=1)]

**获取对中心生成的客户端代理的引用**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample25.js?highlight=1)]

**为集线器类 (创建客户端代理，但不生成代理) **

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample26.cs?highlight=1)]

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a>如何在客户端上定义服务器可以调用的方法

若要定义服务器可从集线器调用的方法，请使用生成的代理的属性向中心代理添加事件处理程序 `client` ， `on` 如果不使用生成的代理，则调用方法。 参数可以是复杂对象。

在调用方法之前添加事件处理程序 `start` 以建立连接。  (如果要在调用方法后添加事件处理程序 `start` ，请参阅本文档前面 [如何建立连接](#establishconnection) 中的说明，并使用所示的语法来定义方法，而不使用生成的代理。 ) 

方法名称匹配不区分大小写。 例如， `Clients.All.addContosoChatMessageToPage` 在服务器上，将在 `AddContosoChatMessageToPage` 客户端上执行、 `addContosoChatMessageToPage` 或 `addcontosochatmessagetopage` 。

**用生成的代理定义客户端 (的方法) **

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample27.js?highlight=2)]

**用生成的代理定义客户端 (方法的替代方法) **

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample28.js?highlight=1-2)]

**在没有生成的代理的客户端 (上定义方法，或在调用 start 方法后添加) **

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample29.js?highlight=3)]

**调用客户端方法的服务器代码**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample30.cs?highlight=5)]

下面的示例包含一个作为方法参数的复杂对象。

**在客户端上定义 (使用生成的代理的复杂对象的方法) **

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample31.js?highlight=2-3)]

**在不使用生成的代理的情况下使用 (复杂对象的客户端上的定义方法) **

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample32.js?highlight=3-4)]

**定义复杂对象的服务器代码**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample33.cs?highlight=1)]

**使用复杂对象调用客户端方法的服务器代码**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample34.cs?highlight=3)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a>如何从客户端调用服务器方法

若要从客户端调用服务器方法，请在 `server` 不使用生成的代理的情况下，使用生成的代理或 `invoke` 中心代理上的方法的属性。 返回值可以是复杂对象。

在集线器上传入方法名称的 camel 大小写形式。 SignalR 会自动进行此更改，以便 JavaScript 代码可以符合 JavaScript 约定。

下面的示例演示如何调用没有返回值的服务器方法，以及如何调用具有返回值的服务器方法。

**不带 HubMethodName 属性的服务器方法**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample35.cs?highlight=3)]

**定义在参数中传递的复杂对象的服务器代码**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample36.cs)]

**调用服务器方法的客户端代码与生成的代理 () **

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample37.js?highlight=1)]

**在没有生成的代理) 的情况下调用服务器方法 (的客户端代码 **

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample38.js?highlight=1)]

如果使用属性修饰了 Hub 方法 `HubMethodName` ，请在不更改大小写的情况下使用该名称。

具有 HubMethodName 属性的**服务器方法**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample39.cs?highlight=3)]

**调用服务器方法的客户端代码与生成的代理 () **

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample40.js?highlight=1)]

**在没有生成的代理) 的情况下调用服务器方法 (的客户端代码 **

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample41.js?highlight=1)]

前面的示例演示如何调用没有返回值的服务器方法。 下面的示例演示如何调用具有返回值的服务器方法。

**具有返回值的方法的服务器代码**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample42.cs?highlight=3)]

用于返回值的**Stock 类**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample43.cs?highlight=1)]

**调用服务器方法的客户端代码与生成的代理 () **

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample44.js?highlight=2,4-5)]

**在没有生成的代理) 的情况下调用服务器方法 (的客户端代码 **

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample45.js?highlight=2,4-5)]

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a>如何处理连接生存期事件

SignalR 提供以下连接生存期事件，你可以处理这些事件：

- `starting`：在通过连接发送任何数据之前引发。
- `received`：在连接上接收到任何数据时引发。 提供接收的数据。
- `connectionSlow`：当客户端检测到连接缓慢或频繁断开时引发。
- `reconnecting`：基础传输开始重新连接时引发。
- `reconnected`：当基础传输重新连接时引发。
- `stateChanged`：连接状态更改时引发。 提供旧状态和新状态， (连接、连接、重新连接或断开连接) 。
- `disconnected`：连接断开连接时引发。

例如，如果要在存在可能导致明显延迟的连接问题时显示警告消息，请处理 `connectionSlow` 事件。

**处理 connectionSlow 事件 (与生成的代理) **

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample46.js?highlight=1)]

**在没有生成的代理) 的情况下处理 connectionSlow 事件 (**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample47.js?highlight=2)]

有关详细信息，请参阅 [了解和处理 SignalR 中的连接生存期事件](handling-connection-lifetime-events.md)。

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a>如何处理错误

SignalR JavaScript 客户端提供 `error` 可为其添加处理程序的事件。 还可以使用 fail 方法为服务器方法调用导致的错误添加处理程序。

如果未在服务器上显式启用详细的错误消息，则在出现错误后 SignalR 返回的异常对象包含有关错误的最小信息。 例如，如果对的调用 `newContosoChatMessage` 失败，则出于安全原因，不建议将错误对象中的错误消息包含 " `There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.` " 向生产中的客户端发送详细的错误消息，但如果你想要启用详细的错误消息以进行故障排除，请在服务器上使用以下代码。

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample48.cs?highlight=2)]

下面的示例演示如何为错误事件添加处理程序。

**添加一个错误处理程序 (与生成的代理) **

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample49.js?highlight=1)]

**添加一个错误处理程序， (没有生成的代理) **

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample50.js?highlight=2)]

下面的示例演示如何处理方法调用中的错误。

**使用生成的代理从方法调用 (处理错误) **

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample51.js?highlight=2)]

**处理方法调用中的错误， (没有生成的代理) **

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample52.js?highlight=2)]

如果方法调用失败，则 `error` 还会引发事件，因此将 `error` 执行方法处理程序和方法回调中的代码 `.fail` 。

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a>如何启用客户端日志记录

若要对连接启用客户端日志记录，请在 `logging` 调用方法之前设置连接对象的属性， `start` 以建立连接。

**使用生成的代理启用日志记录 () **

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample53.js?highlight=1)]

**启用没有生成的代理)  (日志记录 **

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample54.js?highlight=2)]

若要查看日志，请打开浏览器的开发人员工具，并切换到 "控制台" 选项卡。有关显示如何执行此操作的分步说明和屏幕截图的教程，请参阅 [使用 ASP.NET Signalr 进行服务器广播-启用日志记录](../getting-started/tutorial-server-broadcast-with-signalr.md#enable-logging)。

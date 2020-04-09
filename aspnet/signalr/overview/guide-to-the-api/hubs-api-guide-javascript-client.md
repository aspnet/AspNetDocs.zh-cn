---
uid: signalr/overview/guide-to-the-api/hubs-api-guide-javascript-client
title: ASP.NET信号器中心 API 指南 - JavaScript 客户端 |微软文档
author: bradygaster
description: 本文档介绍了在 JavaScript 客户端（如浏览器和 Windows 应用商店 （WinJS） 应用中，将集线器 API 用于 SignalR 版本 2。
ms.author: bradyg
ms.date: 01/15/2019
ms.assetid: a9fd4dc0-1b96-4443-82ca-932a5b4a8ea4
msc.legacyurl: /signalr/overview/guide-to-the-api/hubs-api-guide-javascript-client
msc.type: authoredcontent
ms.openlocfilehash: 8befe133c3627dac1f7d011959c68e2054d345da
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675711"
---
# <a name="aspnet-signalr-hubs-api-guide---javascript-client"></a>ASP.NET信号器中心 API 指南 - JavaScript 客户端

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 本文档介绍了在 JavaScript 客户端（如浏览器和 Windows 应用商店 （WinJS） 应用程序中，将集线器 API 用于 SignalR 版本 2。
>
> SignalR 集线器 API 使您能够从服务器对连接的客户端以及从客户端到服务器进行远程过程调用 （RPC）。 在服务器代码中，定义客户端可以调用的方法，并调用在客户端上运行的方法。 在客户端代码中，定义可以从服务器调用的方法，并调用在服务器上运行的方法。 SignalR 为您处理所有客户端到服务器管道。
>
> SignalR 还提供称为持久连接的较低级别的 API。 有关信号R、集线器和持久连接的介绍，请参阅[信号R 简介](../getting-started/introduction-to-signalr.md)。
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

- [生成的代理及其为您做什么](#genproxy)

    - [何时使用生成的代理](#cantusegenproxy)
- [客户端设置](#clientsetup)

    - [如何引用动态生成的代理](#dynamicproxy)
    - [如何为 SignalR 生成的代理创建物理文件](#manualproxy)
- [如何建立连接](#establishconnection)

    - [$.connect.hub 是 $.hubConnection（） 创建的对象](#connequivalence)
    - [启动方法的异步执行](#asyncstart)
- [如何建立跨域连接](#crossdomain)
- [如何配置连接](#configureconnection)

    - [如何指定查询字符串参数](#querystring)
    - [如何指定传输方法](#transport)
- [如何获取中心类的代理](#getproxy)
- [如何在客户端上定义服务器可以调用的方法](#callclient)
- [如何从客户端调用服务器方法](#callserver)
- [如何处理连接生存期事件](#connectionlifetime)
- [如何处理错误](#handleerrors)
- [如何启用客户端日志记录](#logging)

有关如何对服务器或 .NET 客户端进行编程的文档，请参阅以下资源：

- [信号器集线器 API 指南 - 服务器](hubs-api-guide-server.md)
- [信号器集线器 API 指南 - .NET 客户端](hubs-api-guide-net-client.md)

SignalR 2 服务器组件仅在 .NET 4.5 上可用（尽管在 .NET 4.0 上有一个用于 SignalR 2 的 .NET 客户端）。

<a id="genproxy"></a>

## <a name="the-generated-proxy-and-what-it-does-for-you"></a>生成的代理及其为您做什么

您可以对 JavaScript 客户端进行编程，以便与 SignalR 服务进行通信，无论是否没有 SignalR 为您生成的代理。 代理的作用是简化用于连接的代码的语法、编写服务器调用的方法以及调用服务器上的方法。

编写代码以调用服务器方法时，生成的代理使您能够使用看起来好像在执行本地函数的语法：可以编写`serverMethod(arg1, arg2)`而不是`invoke('serverMethod', arg1, arg2)`。 如果键入服务器方法名称错误，生成的代理语法还允许立即且可理解的客户端错误。 如果手动创建定义代理的文件，还可以获得 IntelliSense 支持编写调用服务器方法的代码。

例如，假设您在服务器上具有以下中心类：

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample1.cs?highlight=1,3,5)]

以下代码示例显示了 JavaScript 代码在服务器上调用`NewContosoChatMessage`该方法和从服务器接收`addContosoChatMessageToPage`方法调用的外观。

**使用生成的代理**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample2.js?highlight=1-2,8)]

**没有生成的代理**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample3.js?highlight=2-3,9)]

<a id="cantusegenproxy"></a>

### <a name="when-to-use-the-generated-proxy"></a>何时使用生成的代理

如果要为服务器调用的客户端方法注册多个事件处理程序，则不能使用生成的代理。 否则，您可以选择使用生成的代理，或者不使用基于编码首选项。 如果选择不使用它，则不必在客户端代码`script`中的元素中引用"信号器/集线器"URL。

<a id="clientsetup"></a>

## <a name="client-setup"></a>客户端设置

JavaScript 客户端需要引用 jQuery 和 SignalR 核心 JavaScript 文件。 jQuery 版本必须为 1.6.4 或主要更高版本，例如 1.7.2、1.8.2 或 1.9.1。 如果您决定使用生成的代理，还需要引用 SignalR 生成的代理 JavaScript 文件。 下面的示例显示了使用生成的代理的 HTML 页中引用的外观。

[!code-html[Main](hubs-api-guide-javascript-client/samples/sample4.html)]

这些引用必须包含在此顺序中：jQuery 优先，之后为 SignalR 内核，最后显示 SignalR 代理。

<a id="dynamicproxy"></a>

### <a name="how-to-reference-the-dynamically-generated-proxy"></a>如何引用动态生成的代理

在前面的示例中，对 SignalR 生成的代理的引用是动态生成的 JavaScript 代码，而不是物理文件。 SignalR 动态为代理创建 JavaScript 代码，并将其用于客户端以响应"/信号器/集线器"URL。 如果在方法`MapSignalR`中为服务器上的 SignalR 连接指定了不同的基本 URL，则动态生成的代理文件的 URL 是自定义 URL，并附加了"/集线器"。

> [!NOTE]
> 对于 Windows 8（Windows 应用商店）JavaScript 客户端，请使用物理代理文件而不是动态生成的文件。 有关详细信息，请参阅本主题后面的["如何为 SignalR 生成的代理创建物理文件](#manualproxy)"。

在ASP.NET MVC 4 或 5 Razor 视图中，使用波浪线引用代理文件引用中的应用程序根：

[!code-html[Main](hubs-api-guide-javascript-client/samples/sample5.html)]

有关在 MVC 5 中使用信号R 的详细信息，请参阅[使用信号R 和 MVC 5 入门](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)。

在ASP.NET MVC 3 Razor`Url.Content`视图中，用于代理文件引用：

[!code-cshtml[Main](hubs-api-guide-javascript-client/samples/sample6.cshtml)]

在ASP.NET Web 窗体应用程序中，`ResolveClientUrl`使用代理文件引用或使用应用根相对路径（以波浪线开头）通过脚本管理器注册它：

[!code-aspx[Main](hubs-api-guide-javascript-client/samples/sample7.aspx)]

通常，使用相同的方法来指定用于 CSS 或 JavaScript 文件的"/信号器/集线器"URL。 如果在不使用波浪线的情况下指定 URL，则在某些情况下，当您使用 IIS Express 在 Visual Studio 中测试时，应用程序将正常工作，但在部署到完整 IIS 时，应用程序将失败，出现 404 错误。 有关详细信息，请参阅在 Visual Studio 中解析对 Web 服务器中的**根级资源的引用**[，以便ASP.NET](https://msdn.microsoft.com/library/58wxa9w5.aspx) MSDN 站点上的 Web 项目。

当您在 Visual Studio 2017 中调试模式下运行 Web 项目时，如果您使用 Internet Explorer 作为浏览器，则可以在**脚本**下**的解决方案资源管理器**中看到代理文件。

要查看文件的内容，请双击**集线器**。 如果您没有使用 Visual Studio 2012 或 2013 和 Internet Explorer，或者如果您未处于调试模式，还可以通过浏览"/signalR/集线器"URL来获取文件内容。 例如，如果您的网站在`http://localhost:56699`中运行，请转到`http://localhost:56699/SignalR/hubs`浏览器中。

<a id="manualproxy"></a>

### <a name="how-to-create-a-physical-file-for-the-signalr-generated-proxy"></a>如何为 SignalR 生成的代理创建物理文件

作为动态生成的代理的替代方法，您可以创建具有代理代码并引用该文件的物理文件。 您可能希望执行此操作以控制缓存或捆绑行为，或者在对服务器方法的调用进行编码时获取 IntelliSense。

要创建代理文件，请执行以下步骤：

1. 安装[Microsoft.AspNet.SignalR.Utils](https://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/) NuGet 软件包。
2. 打开命令提示符并浏览到包含 SignalR.exe 文件*的工具*文件夹。 工具文件夹位于以下位置：

    `[your solution folder]\packages\Microsoft.AspNet.SignalR.Utils.2.1.0\tools`
3. 输入以下命令：

    `signalr ghp /path:[path to the .dll that contains your Hub class]`

    *.dll*的路径通常是项目文件夹中的*bin*文件夹。

    此命令创建一个名为*server.js*的文件，该文件与*signalr.exe*在同一文件夹中。
4. 将*server.js*文件放在项目中的相应文件夹中，将其重命名为适合您的应用程序，并添加对该文件的引用，以代替"信号器/集线器"引用。

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a>如何建立连接

在建立连接之前，必须创建连接对象、创建代理和注册事件处理程序，以便从服务器调用的方法。 设置代理和事件处理程序时，通过调用`start`方法建立连接。

如果使用生成的代理，则不必在自己的代码中创建连接对象，因为生成的代理代码会为您创建连接对象。

<a id="nogenconnection"></a>

**建立连接（使用生成的代理）**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample8.js?highlight=5)]

**建立连接（没有生成的代理）**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample9.js?highlight=1,6)]

示例代码使用默认的"/信号器"URL 连接到您的 SignalR 服务。 有关如何指定其他基本 URL 的信息，请参阅[ASP.NET信号R中心 API 指南 - 服务器 - /signalr URL](hubs-api-guide-server.md#signalrurl)。

默认情况下，中心位置是当前服务器;如果要连接到其他服务器，请在调用`start`该方法之前指定 URL，如以下示例所示：

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample10.js)]

> [!NOTE]
> 通常，在调用 方法以建立连接之前`start`注册事件处理程序。 如果要在建立连接后注册一些事件处理程序，可以执行此操作，但在调用`start`该方法之前，必须至少注册一个事件处理程序。 原因之一是应用程序中可能有许多中心，但如果您只要使用其中一个集线器，则不希望在每个集`OnConnected`线器上触发事件。 建立连接后，在 Hub 的代理上存在客户端方法是指示 SignalR 触发`OnConnected`事件的原因。 如果在调用`start`方法之前未注册任何事件处理程序，则可以在 Hub 上调用方法，但不会调用 Hub`OnConnected`的方法，也不会从服务器调用任何客户端方法。

<a id="connequivalence"></a>

### <a name="connectionhub-is-the-same-object-that-hubconnection-creates"></a>$.connect.hub 是 $.hubConnection（） 创建的对象

正如您从示例中所看到的，当您使用生成的代理时，`$.connection.hub`引用连接对象。 这与不使用生成的代理时通过调用`$.hubConnection()`获得的对象相同。 生成的代理代码通过执行以下语句为您创建连接：

![在生成的代理文件中创建连接](hubs-api-guide-javascript-client/_static/image3.png)

使用生成的代理时，可以使用任何不使用生成的代理时对连接对象`$.connection.hub`执行的任何操作。

<a id="asyncstart"></a>

### <a name="asynchronous-execution-of-the-start-method"></a>启动方法的异步执行

该方法`start`以异步方式执行。 它返回[jQuery 延迟对象](http://api.jquery.com/category/deferred-object/)，这意味着您可以通过调用方法（如`pipe`、`done`和`fail`） 添加回调函数。 如果已建立连接后需要执行的代码（如调用服务器方法），请将该代码放入回调函数中，或从回调函数调用它。 回调`.done`方法在建立连接后执行，并在服务器上`OnConnected`的事件处理程序方法中的任何代码完成执行之后。

如果将上述示例中的"现在连接"语句作为`start`方法调用后的下一`.done`行代码（不在回调中），则`console.log`该行将在建立连接之前执行，如以下示例所示：

![编写建立连接后运行的代码的错误方法](hubs-api-guide-javascript-client/_static/image5.png)

<a id="crossdomain"></a>

## <a name="how-to-establish-a-cross-domain-connection"></a>如何建立跨域连接

通常，如果浏览器从`http://contoso.com`加载页面，则 SignalR 连接位于同一域中`http://contoso.com/signalr`，在 。 如果 中的`http://contoso.com`页面与`http://fabrikam.com/signalr`断开连接，则为跨域连接。 出于安全原因，默认情况下禁用跨域连接。

在 SignalR 1.x 中，跨域请求由单个启用CrossDomain 标志控制。 此标志同时控制 JSONP 和 CORS 请求。 为了更灵活，所有 CORS 支持都从 SignalR 的服务器组件中删除（如果检测到浏览器支持它，JavaScript 客户端仍通常使用 CORS），并且新的 OWIN 中间件已可用于支持这些方案。

如果客户端上需要 JSONP（以支持旧浏览器中的跨域请求），则需要通过在`EnableJSONP``HubConfiguration`对象`true`上设置为 （如下所示）显式启用它。 默认情况下禁用 JSONP，因为它的安全性低于 CORS。

**将 Microsoft.Owin.Cors 添加到您的项目中：** 要安装此库，请在包管理器控制台中运行以下命令：

`Install-Package Microsoft.Owin.Cors`

此命令会将包的 2.1.0 版本添加到项目中。

### <a name="calling-usecors"></a>调用使用参数

 以下代码段演示如何在 SignalR 2 中实现跨域连接。

**在 SignalR 2 中实现跨域请求**

以下代码演示如何在 SignalR 2 项目中启用 CORS 或 JSONP。 此代码示例使用`Map``RunSignalR`而不是`MapSignalR`，以便 CORS 中间件仅运行需要 CORS 支持的 SignalR 请求（而不是针对 中`MapSignalR`指定的路径上的所有流量）。映射还可用于需要为特定 URL 前缀运行的任何其他中间件，而不是整个应用程序。

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample11.cs)]

> [!NOTE]
>
> - 不要在代码中设置为`jQuery.support.cors`true。
>
>     ![不要将 jQuery.support.cors 设置为 true](hubs-api-guide-javascript-client/_static/image7.png)
>
>     信号R处理CORS的使用。 设置为`jQuery.support.cors`true 禁用 JSONP，因为它会导致 SignalR 假定浏览器支持 CORS。
> - 当您连接到本地主机 URL 时，Internet Explorer 10 不会将其视为跨域连接，因此应用程序将在本地使用 IE 10，即使您未在服务器上启用跨域连接也是如此。
> - 有关将跨域连接与 Internet Explorer 9 一起使用的信息，请参阅[此堆栈溢出线程](http://stackoverflow.com/questions/13573397/siganlr-ie9-cross-domain-request-dont-work)。
> - 有关使用 Chrome 跨域连接的信息，请参阅[此堆栈溢出线程](http://stackoverflow.com/questions/15467373/signalr-1-0-1-cross-domain-request-cors-with-chrome)。
> - 示例代码使用默认的"/信号器"URL 连接到您的 SignalR 服务。 有关如何指定其他基本 URL 的信息，请参阅[ASP.NET信号R中心 API 指南 - 服务器 - /signalr URL](hubs-api-guide-server.md#signalrurl)。

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a>如何配置连接

在建立连接之前，可以指定查询字符串参数或指定传输方法。

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a>如何指定查询字符串参数

如果要在客户端连接时将数据发送到服务器，则可以向连接对象添加查询字符串参数。 以下示例演示如何在客户端代码中设置查询字符串参数。

**在调用 start 方法之前设置查询字符串值（使用生成的代理）**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample12.js?highlight=1)]

**在调用 start 方法之前设置查询字符串值（没有生成的代理）**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample13.js?highlight=2)]

下面的示例演示如何读取服务器代码中的查询字符串参数。

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample14.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a>如何指定传输方法

作为连接过程的一部分，SignalR 客户端通常与服务器协商以确定服务器和客户端支持的最佳传输。 如果您已经知道要使用的传输，则可以在调用 方法时指定传输方法来`start`绕过此协商过程。

**指定传输方法的客户端代码（使用生成的代理）**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample15.js?highlight=1)]

**指定传输方法的客户端代码（没有生成的代理）**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample16.js?highlight=2)]

作为替代方法，您可以按希望 SignalR 尝试它们的顺序指定多个传输方法：

**指定自定义传输回退方案（使用生成的代理）的客户端代码**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample17.js?highlight=1)]

**指定自定义传输回退方案的客户端代码（没有生成的代理）**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample18.js?highlight=2)]

可以使用以下值指定传输方法：

- "网络套接字"
- "永久框架"
- "服务器发送事件"
- "长轮询"

以下示例演示如何找出连接正在使用哪种传输方法。

**显示连接使用的传输方法的客户端代码（使用生成的代理）**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample19.js?highlight=2)]

**显示连接使用的传输方法的客户端代码（没有生成的代理）**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample20.js?highlight=3)]

有关如何在服务器代码中检查传输方法的信息，请参阅[ASP.NET SignalR 集线器 API 指南 - 服务器 - 如何从 Context 属性获取有关客户端的信息](hubs-api-guide-server.md#contextproperty)。 有关传输和回退的详细信息，请参阅[信号R - 传输和回退简介](../getting-started/introduction-to-signalr.md#transports)。

<a id="getproxy"></a>

## <a name="how-to-get-a-proxy-for-a-hub-class"></a>如何获取中心类的代理

您创建的每个连接对象都封装了有关连接到包含一个或多个集线器类的 SignalR 服务的信息。 要与 Hub 类通信，请使用自己创建的代理对象（如果您不使用生成的代理）或为您生成的代理。

在客户端上，代理名称是集线器类名称的骆驼大小写版本。 SignalR 会自动进行此更改，以便 JavaScript 代码可以符合 JavaScript 约定。

**服务器上的集线器类**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample21.cs?highlight=1)]

**获取对中心生成的客户端代理的引用**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample22.js?highlight=1)]

**为中心类创建客户端代理（没有生成的代理）**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample23.cs?highlight=1)]

如果使用`HubName`属性装饰 Hub 类，请使用确切名称而不更改大小写。

**服务器上具有 HubName 属性的集线器类**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample24.cs?highlight=1)]

**获取对中心生成的客户端代理的引用**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample25.js?highlight=1)]

**为中心类创建客户端代理（没有生成的代理）**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample26.cs?highlight=1)]

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a>如何在客户端上定义服务器可以调用的方法

要定义服务器可以从集线器调用的方法，请使用生成的代理`client`的属性向中心代理添加事件处理程序，或者如果您不使用生成的代理，`on`则调用 方法。 参数可以是复杂对象。

在调用 方法以建立连接之前添加`start`事件处理程序。 （如果要在调用`start`方法后添加事件处理程序，请参阅本文档前面[如何建立连接](#establishconnection)的说明，并使用显示的语法来定义方法而不使用生成的代理。

方法名称匹配不区分大小写。 例如，`Clients.All.addContosoChatMessageToPage`在服务器上将执行`AddContosoChatMessageToPage`、`addContosoChatMessageToPage`或`addcontosochatmessagetopage`在客户端上。

**在客户端上定义方法（使用生成的代理）**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample27.js?highlight=2)]

**在客户端上定义方法的替代方法（使用生成的代理）**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample28.js?highlight=1-2)]

**在客户端上定义方法（没有生成的代理，或在调用 start 方法后添加时）**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample29.js?highlight=3)]

**调用客户端方法的服务器代码**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample30.cs?highlight=5)]

以下示例包括作为方法参数的复杂对象。

**在客户端上定义采用复杂对象的方法（使用生成的代理）**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample31.js?highlight=2-3)]

**在客户端上定义采用复杂对象的方法（没有生成的代理）**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample32.js?highlight=3-4)]

**定义复杂对象的服务器代码**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample33.cs?highlight=1)]

**使用复杂对象调用客户端方法的服务器代码**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample34.cs?highlight=3)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a>如何从客户端调用服务器方法

要从客户端调用服务器方法，请使用生成的代理`server`的属性或 Hub 代理上`invoke`的方法（如果您不使用生成的代理）。 返回值或参数可以是复杂对象。

在集线器上传递方法名称的骆驼大小写版本。 SignalR 会自动进行此更改，以便 JavaScript 代码可以符合 JavaScript 约定。

以下示例演示如何调用没有返回值的服务器方法以及如何调用具有返回值的服务器方法。

**没有 HubMethodName 属性的服务器方法**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample35.cs?highlight=3)]

**定义参数中传递的复杂对象的服务器代码**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample36.cs)]

**调用服务器方法的客户端代码（使用生成的代理）**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample37.js?highlight=1)]

**调用服务器方法的客户端代码（没有生成的代理）**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample38.js?highlight=1)]

如果使用`HubMethodName`属性修饰 Hub 方法，请使用该名称而不更改大小写。

具有 HubMethodName 属性的**服务器方法**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample39.cs?highlight=3)]

**调用服务器方法的客户端代码（使用生成的代理）**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample40.js?highlight=1)]

**调用服务器方法的客户端代码（没有生成的代理）**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample41.js?highlight=1)]

前面的示例演示如何调用没有返回值的服务器方法。 以下示例演示如何调用具有返回值的服务器方法。

**具有返回值的方法的服务器代码**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample42.cs?highlight=3)]

**用于**回报值的 Stock 类

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample43.cs?highlight=1)]

**调用服务器方法的客户端代码（使用生成的代理）**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample44.js?highlight=2,4-5)]

**调用服务器方法的客户端代码（没有生成的代理）**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample45.js?highlight=2,4-5)]

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a>如何处理连接生存期事件

SignalR 提供您可以处理的以下连接生存期事件：

- `starting`：在通过连接发送任何数据之前引发。
- `received`：在连接上收到任何数据时引发。 提供接收的数据。
- `connectionSlow`：当客户端检测到连接缓慢或频繁断开时引发。
- `reconnecting`：当基础传输开始重新连接时引发。
- `reconnected`：在基础传输重新连接时引发。
- `stateChanged`：当连接状态更改时引发。 提供旧状态和新状态（连接、连接、重新连接或断开连接）。
- `disconnected`：连接断开连接时引发。

例如，如果要在连接问题可能导致明显延迟时显示警告消息，则处理该`connectionSlow`事件。

**处理连接速度事件（使用生成的代理）**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample46.js?highlight=1)]

**处理连接速度慢事件（没有生成的代理）**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample47.js?highlight=2)]

有关详细信息，请参阅在[SignalR 中了解和处理连接生存期事件](handling-connection-lifetime-events.md)。

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a>如何处理错误

SignalR JavaScript 客户端提供`error`一个事件，您可以为其添加处理程序。 您还可以使用 fail 方法为服务器方法调用导致的错误添加处理程序。

如果未在服务器上显式启用详细的错误消息，则 SignalR 在错误后返回的异常对象包含有关该错误的最少信息。 例如，如果调用`newContosoChatMessage`失败，错误对象中的错误消息包含"`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`出于安全原因不建议向生产中的客户端发送详细的错误消息，但如果要启用详细的错误消息以进行故障排除，请使用服务器上的以下代码。

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample48.cs?highlight=2)]

下面的示例演示如何为错误事件添加处理程序。

**添加错误处理程序（使用生成的代理）**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample49.js?highlight=1)]

**添加错误处理程序（没有生成的代理）**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample50.js?highlight=2)]

下面的示例演示如何处理方法调用中的错误。

**处理方法调用中的错误（使用生成的代理）**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample51.js?highlight=2)]

**处理方法调用中的错误（没有生成的代理）**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample52.js?highlight=2)]

如果方法调用失败，也会引发`error`该事件，因此`error`方法处理程序中的代码`.fail`和方法回调中的代码将执行。

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a>如何启用客户端日志记录

要在连接上启用客户端日志记录，在调用`logging``start`方法建立连接之前，在连接对象上设置属性。

**启用日志记录（使用生成的代理）**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample53.js?highlight=1)]

**启用日志记录（没有生成的代理）**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample54.js?highlight=2)]

要查看日志，请打开浏览器的开发人员工具，然后转到"控制台"选项卡。有关显示分步说明和显示如何执行此操作的屏幕截图的教程，请参阅[使用ASP.NET信号器的服务器广播 - 启用日志记录](../getting-started/tutorial-server-broadcast-with-signalr.md#enable-logging)。

---
uid: signalr/overview/security/introduction-to-security
title: 信号R安全简介 |微软文档
author: bradygaster
description: 描述在开发 SignalR 应用程序时必须考虑的安全问题。
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: ed562717-8591-4936-8e10-c7e63dcb570a
msc.legacyurl: /signalr/overview/security/introduction-to-security
msc.type: authoredcontent
ms.openlocfilehash: 24ce20b45543468de28ad017ba62d2f6e5a00f3b
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675807"
---
# <a name="introduction-to-signalr-security"></a>SignalR 安全性简介

由[帕特里克·弗莱彻](https://github.com/pfletcher)，[汤姆·菲茨麦克肯](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 本文介绍了在开发 SignalR 应用程序时必须考虑的安全问题。
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

## <a name="overview"></a>概述

本文档包含以下各节：

- [信号R安全概念](#concepts)

    - [身份验证和授权](#authentication)
    - [连接令牌](#connectiontoken)
    - [重新连接时重新加入组](#rejoingroup)
- [信号器如何防止跨站点请求伪造](#csrf)
- [信号R安全建议](#recommendations)

    - [安全套接字层 （SSL） 协议](#ssl)
    - [不要将组用作安全机制](#groupsecurity)
    - [安全地处理来自客户端的输入](#input)
    - [协调用户状态更改与活动连接](#reconcile)
    - [自动生成的 JavaScript 代理文件](#autogen)
    - [异常](#exceptions)

<a id="concepts"></a>

## <a name="signalr-security-concepts"></a>信号R安全概念

<a id="authentication"></a>

### <a name="authentication-and-authorization"></a>身份验证和授权

SignalR 不提供任何用于验证用户的功能。 相反，您将 SignalR 功能集成到应用程序的现有身份验证结构中。 您可以像在应用程序中通常一样对用户进行身份验证，并处理 SignalR 代码中的身份验证结果。 例如，您可以使用ASP.NET窗体身份验证对用户进行身份验证，然后在中心中强制授权哪些用户或角色调用方法。 在集线器中，还可以将身份验证信息（如用户名或用户是否属于角色）传递给客户端。

SignalR 提供[授权](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx)属性来指定哪些用户有权访问集线器或方法。 将"授权"属性应用于中心或中心中的特定方法。 如果没有"授权"属性，则连接到集线器的客户端可以使用集线器上的所有公共方法。 有关集线器的详细信息，请参阅[SignalR 集线器的身份验证和授权](hub-authorization.md)。

将`Authorize`属性应用于中心，但不应用于持久连接。 在使用 时强制实施授权规则`PersistentConnection`，必须重写`AuthorizeRequest`方法。 有关持久连接的详细信息，请参阅[SignalR 持久连接的身份验证和授权](persistent-connection-authorization.md)。

<a id="connectiontoken"></a>

### <a name="connection-token"></a>连接令牌

SignalR 通过验证发件人的身份来降低执行恶意命令的风险。 对于每个请求，客户端和服务器传递一个连接令牌，其中包含经过身份验证的用户的连接 ID 和用户名。 连接 ID 唯一标识每个连接的客户端。 服务器在创建新连接时随机生成连接 ID，并在连接期间保留该 ID。 Web 应用程序的身份验证机制提供用户名。 SignalR 使用加密和数字签名来保护连接令牌。

![](introduction-to-security/_static/image2.png)

对于每个请求，服务器验证令牌的内容，以确保请求来自指定用户。 用户名必须对应于连接 ID。通过验证连接 ID 和用户名，SignalR 可防止恶意用户轻松模拟其他用户。 如果服务器无法验证连接令牌，则请求失败。

![](introduction-to-security/_static/image4.png)

由于连接 ID 是验证过程的一部分，因此不应向其他用户显示一个用户的连接 ID 或将该值存储在客户端上（如 Cookie 中）。

#### <a name="connection-tokens-vs-other-token-types"></a>连接令牌与其他令牌类型

连接令牌偶尔会被安全工具标记，因为它们看起来像是会话令牌或身份验证令牌，如果暴露，就会造成风险。

SignalR 的连接令牌不是身份验证令牌。 它用于确认发出此请求的用户与创建连接的用户相同。 连接令牌是必需的，因为ASP.NET SignalR 允许连接在服务器之间移动。 令牌将连接与特定用户关联，但不断言发出请求的用户的身份。 要对 SignalR 请求进行正确身份验证，它必须具有一些其他维护用户身份的令牌，例如 Cookie 或承载令牌。 但是，连接令牌本身不声明请求是由该用户发出，只是声明令牌中包含的连接 ID 与该用户相关联。

由于连接令牌不提供自己的身份验证声明，因此它不被视为"会话"或"身份验证"令牌。 获取给定用户的连接令牌并在作为其他用户（或未身份验证的请求）身份验证的请求中重播该令牌将失败，因为请求的用户标识和存储在令牌中的标识不匹配。

<a id="rejoingroup"></a>

### <a name="rejoining-groups-when-reconnecting"></a>重新连接时重新加入组

默认情况下，SignalR 应用程序在从临时中断重新连接时（例如连接在连接超时之前断开和重新建立连接时）时，将自动将用户重新分配给相应的组。重新连接时，客户端传递一个组令牌，其中包含连接 ID 和分配的组。 组令牌经过数字签名和加密。 客户端在重新连接后保留相同的连接 ID;因此，从重新连接的客户端传递的连接 ID 必须与客户端使用以前的连接 ID 匹配。 此验证可防止恶意用户在重新连接时传递加入未授权组的请求。

但是，请务必注意，组令牌不会过期。 如果用户过去属于一个组，但被禁止从该组，该用户可能能够模拟包含禁止组的组令牌。 如果需要安全地管理哪些用户属于哪些组，则需要将数据存储在服务器上，例如数据库中。 然后，向应用程序添加逻辑，以验证服务器上的用户是否属于组。 有关验证组成员身份的示例，请参阅[使用组](../guide-to-the-api/working-with-groups.md)。

仅当连接在临时中断后重新连接时，自动重新加入组才适用。 如果用户通过导航离开应用程序而断开连接，或者应用程序重新启动，则应用程序必须处理如何将该用户添加到正确的组。 有关详细信息，请参阅[使用组](../guide-to-the-api/working-with-groups.md)。

<a id="csrf"></a>

## <a name="how-signalr-prevents-cross-site-request-forgery"></a>信号器如何防止跨站点请求伪造

跨站点请求伪造 （CSRF） 是恶意站点向用户当前登录的易受攻击站点发送请求的攻击。 SignalR 通过使恶意站点极不可能为 SignalR 应用程序创建有效请求来防止 CSRF。

### <a name="description-of-csrf-attack"></a>CSRF 攻击的描述

下面是 CSRF 攻击的示例：

1. 用户使用窗体身份验证登录到www.example.com。
2. 服务器对用户进行身份验证。 来自服务器的响应包括身份验证 Cookie。
3. 无需注销，用户将访问恶意网站。 此恶意网站包含以下 HTML 表单：

    [!code-html[Main](introduction-to-security/samples/sample1.html)]

   请注意，表单操作发布到易受攻击的网站，而不是恶意站点。 这是CSRF的"跨站点"部分。
4. 用户单击提交按钮。 浏览器包含带有请求的身份验证 Cookie。
5. 请求在具有用户身份验证上下文的example.com服务器上运行，并可以执行允许经过身份验证的用户执行的任何操作。

尽管此示例要求用户单击窗体按钮，但恶意页面同样可以轻松地运行向 SignalR 应用程序发送 AJAX 请求的脚本。 此外，使用 SSL 不会阻止 CSRF 攻击，因为恶意站点可以发送"https://"请求。

通常，CSRF 攻击可能会针对使用 Cookie 进行身份验证的网站，因为浏览器会将所有相关 Cookie 发送到目标网站。 但是，CSRF 的攻击并不仅限于利用 Cookie。 例如，基本身份验证和摘要身份验证也容易受到攻击。 用户使用"基本"或"摘要"身份验证登录后，浏览器会自动发送凭据，直到会话结束。

### <a name="csrf-mitigations-taken-by-signalr"></a>SignalR 采取的 CSRF 缓解措施

SignalR 采取以下步骤防止恶意站点向应用程序创建有效请求。 默认情况下，SignalR 执行这些步骤，无需在代码中执行任何操作。

- **禁用跨域请求**SignalR 禁用跨域请求，以防止用户从外部域调用 SignalR 终结点。 SignalR 认为来自外部域的任何请求都无效，并阻止请求。 我们建议您保留此默认行为;但是，我们建议您保留此默认行为。否则，恶意网站可能会诱使用户向您的网站发送命令。 如果需要使用跨域请求，请参阅[如何建立跨域连接](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)。
- **在查询字符串中传递连接令牌，而不是 Cookie**SignalR 将连接令牌作为查询字符串值传递，而不是作为 Cookie 传递。 将连接令牌存储在 Cookie 中不安全，因为当遇到恶意代码时，浏览器可能会无意中转发连接令牌。 此外，在查询字符串中传递连接令牌可防止连接令牌保留在当前连接之外。 因此，恶意用户不能根据其他用户的身份验证凭据发出请求。
- **验证连接令牌**如[连接令牌](#connectiontoken)部分所述，服务器知道哪个连接 ID 与每个经过身份验证的用户相关联。 服务器不处理来自连接 ID 与用户名不匹配的任何请求。 恶意用户不太可能猜到有效请求，因为恶意用户必须知道用户名和当前随机生成的连接 ID。连接 ID 一旦结束，该连接 ID 将变为无效。 匿名用户不应访问任何敏感信息。

<a id="recommendations"></a>

## <a name="signalr-security-recommendations"></a>信号R安全建议

<a id="ssl"></a>

### <a name="secure-socket-layers-ssl-protocol"></a>安全套接字层 （SSL） 协议

SSL 协议使用加密来保护客户端和服务器之间的数据传输。 如果您的 SignalR 应用程序在客户端和服务器之间传输敏感信息，请使用 SSL 进行传输。 有关设置 SSL 的详细信息，请参阅[如何在 IIS 7 上设置 SSL。](https://www.iis.net/learn/manage/configuring-security/how-to-set-up-ssl-on-iis)

<a id="groupsecurity"></a>

### <a name="do-not-use-groups-as-a-security-mechanism"></a>不要将组用作安全机制

组是收集相关用户的便捷方式，但它们不是限制对敏感信息访问的安全机制。 当用户可以在重新连接期间自动重新加入组时，尤其如此。 相反，请考虑将特权用户添加到角色，并将对中心方法的访问限制为该角色的成员。 有关基于角色限制访问的示例，请参阅[SignalR 中心的身份验证和授权](hub-authorization.md)。 有关在重新连接时检查用户访问组的示例，请参阅[使用组](../guide-to-the-api/working-with-groups.md)。

<a id="input"></a>

### <a name="safely-handling-input-from-clients"></a>安全地处理来自客户端的输入

为了确保恶意用户不会向其他用户发送脚本，您必须对客户端用于广播到其他客户端的所有输入进行编码。 您应该对接收客户端而不是服务器上的消息进行编码，因为 SignalR 应用程序可能具有许多不同类型的客户端。 因此，HTML 编码适用于 Web 客户端，但对于其他类型的客户端则不有效。 例如，显示聊天消息的 Web 客户端方法可以通过调用`html()`函数安全地处理用户名和消息。

[!code-html[Main](introduction-to-security/samples/sample2.html?highlight=3-4)]

<a id="reconcile"></a>

### <a name="reconciling-a-change-in-user-status-with-an-active-connection"></a>协调用户状态更改与活动连接

如果用户的身份验证状态在存在活动连接时发生更改，则用户将收到一个错误，指出"用户标识在活动 SignalR 连接期间无法更改"。 在这种情况下，应用程序应重新连接到服务器，以确保连接 ID 和用户名得到协调。 例如，如果应用程序允许用户在存在活动连接时注销，则连接的用户名将不再与为下一个请求传入的名称匹配。 您需要在用户注销之前停止连接，然后重新启动它。

但是，请务必注意，大多数应用程序不需要手动停止并启动连接。 如果应用程序在注销后将用户重定向到单独的页面（例如 Web 窗体应用程序或 MVC 应用程序中的默认行为，或在注销后刷新当前页面，则活动连接将自动断开连接，不需要任何其他操作。

下面的示例演示如何在用户状态更改时停止和启动连接。

[!code-html[Main](introduction-to-security/samples/sample3.html)]

或者，如果您的网站使用表单身份验证的滑动过期，并且没有活动保持身份验证 Cookie 的有效性，则用户的身份验证状态可能会更改。 在这种情况下，用户将被注销，用户名将不再与连接令牌中的用户名匹配。 您可以通过添加一些脚本来解决此问题，这些脚本定期请求 Web 服务器上的资源以保持身份验证 Cookie 的有效性。 下面的示例演示如何每 30 分钟请求一次资源。

[!code-javascript[Main](introduction-to-security/samples/sample4.js)]

<a id="autogen"></a>

### <a name="automatically-generated-javascript-proxy-files"></a>自动生成的 JavaScript 代理文件

如果不想在每个用户的 JavaScript 代理文件中包含所有中心和方法，则可以禁用该文件的自动生成。 如果有多个集线器和方法，但不希望每个用户都了解所有方法，则可以选择此选项。 通过将**启用JavaScriptProxie设置为** **false，** 可以禁用自动生成。

[!code-csharp[Main](introduction-to-security/samples/sample5.cs)]

有关 JavaScript 代理文件的详细信息，请参阅[生成的代理及其为您做什么](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy)。 <a id="exceptions"></a>

### <a name="exceptions"></a>例外

应避免将异常对象传递给客户端，因为对象可能会向客户端公开敏感信息。 相反，在显示相关错误消息的客户端上调用方法。

[!code-csharp[Main](introduction-to-security/samples/sample6.cs)]

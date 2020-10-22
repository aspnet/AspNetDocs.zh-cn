---
uid: signalr/overview/security/introduction-to-security
title: SignalR Security 简介 |Microsoft Docs
author: bradygaster
description: 描述在开发 SignalR 应用程序时必须考虑的安全问题。
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: ed562717-8591-4936-8e10-c7e63dcb570a
msc.legacyurl: /signalr/overview/security/introduction-to-security
msc.type: authoredcontent
ms.openlocfilehash: 24ce20b45543468de28ad017ba62d2f6e5a00f3b
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345441"
---
# <a name="introduction-to-signalr-security"></a>SignalR 安全性简介

作者： [Fletcher](https://github.com/pfletcher)， [Tom FitzMacken](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 本文介绍了在开发 SignalR 应用程序时必须考虑的安全问题。
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

## <a name="overview"></a>概述

本文档包含以下各节：

- [SignalR 安全概念](#concepts)

    - [身份验证和授权](#authentication)
    - [连接令牌](#connectiontoken)
    - [重新连接时的重新加入组](#rejoingroup)
- [SignalR 如何阻止跨站点请求伪造](#csrf)
- [SignalR 安全建议](#recommendations)

    - [ (SSL) 协议的安全套接字层](#ssl)
    - [不要将组用作安全机制](#groupsecurity)
    - [安全处理来自客户端的输入](#input)
    - [协调用户状态更改与活动连接](#reconcile)
    - [自动生成的 JavaScript 代理文件](#autogen)
    - [异常](#exceptions)

<a id="concepts"></a>

## <a name="signalr-security-concepts"></a>SignalR 安全概念

<a id="authentication"></a>

### <a name="authentication-and-authorization"></a>身份验证和授权

SignalR 不提供任何用于对用户进行身份验证的功能。 相反，将 SignalR 功能集成到应用程序的现有身份验证结构中。 在应用程序中按通常的方式对用户进行身份验证，并在 SignalR 代码中处理身份验证的结果。 例如，你可以使用 ASP.NET forms 身份验证对用户进行身份验证，然后在你的中心内强制实施有权调用方法的用户或角色。 你还可以在中心将身份验证信息（如用户名或用户是否属于角色）传递给客户端。

SignalR 提供 [授权](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx) 属性以指定哪些用户有权访问集线器或方法。 将授权属性应用于中心中的集线器或特定方法。 如果没有授权属性，则中心上的所有公共方法都可用于连接到中心的客户端。 有关中心的详细信息，请参阅 [SignalR hub 的身份验证和授权](hub-authorization.md)。

将该属性应用于 `Authorize` 中心，但不应用于持久性连接。 若要在使用时强制执行授权规则 `PersistentConnection` ，必须重写 `AuthorizeRequest` 方法。 有关永久性连接的详细信息，请参阅 [SignalR 永久性连接的身份验证和授权](persistent-connection-authorization.md)。

<a id="connectiontoken"></a>

### <a name="connection-token"></a>连接令牌

SignalR 通过验证发件人的身份，降低执行恶意命令的风险。 对于每个请求，客户端和服务器传递一个连接令牌，其中包含经过身份验证的用户的连接 id 和用户名。 连接 id 唯一标识每个连接的客户端。 在创建新连接时，服务器会随机生成连接 id，并在连接持续时间内保留该 id。 Web 应用程序的身份验证机制提供用户名。 SignalR 使用加密和数字签名来保护连接令牌。

![](introduction-to-security/_static/image2.png)

对于每个请求，服务器会验证令牌的内容，以确保请求来自指定的用户。 用户名必须与连接 id 相对应。通过验证连接 id 和用户名，SignalR 可防止恶意用户轻松地模拟其他用户。 如果服务器无法验证连接令牌，请求会失败。

![](introduction-to-security/_static/image4.png)

由于连接 id 是验证过程的一部分，因此不应将一个用户的连接 id 泄露给其他用户，或将该值存储在客户端上，例如在 cookie 中。

#### <a name="connection-tokens-vs-other-token-types"></a>连接令牌与其他令牌类型

安全工具有时会标记连接令牌，因为它们看起来像是会话令牌或身份验证令牌，如果公开，则会带来风险。

SignalR 的连接令牌不是身份验证令牌。 它用于确认发出此请求的用户与创建连接的用户相同。 连接令牌是必需的，因为 ASP.NET SignalR 允许在服务器之间移动连接。 该令牌将连接与特定用户关联，但不会声明发出请求的用户的标识。 若要对 SignalR 请求进行正确的身份验证，它必须具有另一个断言用户身份的标记，如 cookie 或持有者令牌。 不过，连接令牌本身不会声明该用户发出请求，只有令牌中包含的连接 ID 与该用户相关联。

由于连接令牌不提供自身的身份验证声明，因此不会将其视为 "会话" 或 "身份验证" 令牌。 获取给定用户的连接令牌并将其重播到作为不同用户 (身份验证的请求中，否则) 不经过身份验证的请求将失败，因为请求的用户标识和令牌中存储的标识不匹配。

<a id="rejoingroup"></a>

### <a name="rejoining-groups-when-reconnecting"></a>重新连接时的重新加入组

默认情况下，当从暂时中断重新连接时，SignalR 应用程序会自动将用户重新分配给相应的组，例如在连接断开之前断开并重新建立连接。重新连接时，客户端会传递包含连接 id 和分配组的组令牌。 组令牌已进行数字签名和加密。 重新连接后，客户端将保留相同的连接 id;因此，从重新连接的客户端传递的连接 id 必须与客户端使用的以前的连接 id 匹配。 此验证可防止恶意用户在重新连接时将请求传递给加入未经授权的组。

但是，请务必注意，组令牌不会过期。 如果用户属于过去的某个组，但从该组中被禁止，则该用户可能能够模拟包含禁止组的组令牌。 如果你需要安全地管理属于哪些组的用户，则需要将该数据存储在服务器上，例如在数据库中。 然后，将逻辑添加到应用程序，以便在服务器上验证用户是否属于组。 有关验证组成员身份的示例，请参阅 [使用组](../guide-to-the-api/working-with-groups.md)。

仅当在暂时中断后重新连接连接时，自动重新加入组才适用。 如果用户通过离开应用程序或重新启动应用程序而断开连接，则应用程序必须处理如何将该用户添加到正确的组。 有关详细信息，请参阅使用 [组](../guide-to-the-api/working-with-groups.md)。

<a id="csrf"></a>

## <a name="how-signalr-prevents-cross-site-request-forgery"></a>SignalR 如何阻止跨站点请求伪造

跨站点请求伪造 (CSRF) 是一种攻击，其中恶意站点将请求发送到用户当前登录到的有漏洞站点。 SignalR 通过使恶意网站极不可能为 SignalR 应用程序创建有效请求来防止 CSRF。

### <a name="description-of-csrf-attack"></a>CSRF 攻击说明

下面是 CSRF 攻击的示例：

1. 用户使用窗体身份验证登录到 www.example.com。
2. 服务器对用户进行身份验证。 来自服务器的响应包含一个身份验证 cookie。
3. 如果不注销，用户将访问恶意网站。 此恶意网站包含以下 HTML 格式：

    [!code-html[Main](introduction-to-security/samples/sample1.html)]

   请注意，窗体操作会发布到易受攻击的站点，而不是恶意站点。 这是 CSRF 的 "跨站点" 部分。
4. 用户单击 "提交" 按钮。 浏览器包含请求中的身份验证 cookie。
5. 请求使用用户的身份验证上下文在 example.com 服务器上运行，并可执行允许经过身份验证的用户执行的任何操作。

尽管此示例要求用户单击 "窗体" 按钮，但恶意页面可以轻松地运行一个将 AJAX 请求发送到 SignalR 应用程序的脚本。 而且，使用 SSL 不会阻止 CSRF 攻击，因为恶意站点可以发送 "https://" 请求。

通常，可以对使用 cookie 进行身份验证的网站执行 CSRF 攻击，因为浏览器会将所有相关 cookie 发送到目标网站。 但是，CSRF 攻击并不局限于利用 cookie。 例如，基本身份验证和摘要式身份验证也容易受到攻击。 用户使用基本或摘要式身份验证登录后，浏览器会自动发送凭据，直到会话结束。

### <a name="csrf-mitigations-taken-by-signalr"></a>SignalR 执行的 CSRF 缓解措施

SignalR 执行以下步骤，以防止恶意网站创建对应用程序的有效请求。 默认情况下，SignalR 会执行这些步骤，无需在代码中执行任何操作。

- **禁用跨域请求** SignalR 禁用跨域请求，以防止用户从外部域调用 SignalR 终结点。 SignalR 将来自外部域的任何请求都视为无效，并阻止请求。 建议保留此默认行为;否则，恶意站点可能会诱使用户将命令发送到您的站点。 如果需要使用跨域请求，请参阅     [如何建立跨域连接](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain) 。
- **在查询字符串中传递连接标记，而不是 cookie** SignalR 将连接令牌作为查询字符串值（而不是 cookie）传递。 将连接令牌存储在 cookie 中是不安全的，因为浏览器在遇到恶意代码时可能会无意中转发连接令牌。 此外，在查询字符串中传递连接令牌可防止连接令牌在当前连接之外保留。 因此，恶意用户无法使用其他用户的身份验证凭据发出请求。
- **验证连接令牌** 如 "     [连接令牌](#connectiontoken) " 部分中所述，服务器知道哪个连接 id 与每个经过身份验证的用户相关联。 服务器不处理来自连接 id 的任何不匹配用户名的请求。 恶意用户可能猜不到有效的请求，因为恶意用户必须知道用户名和当前随机生成的连接 id。连接结束后，该连接 id 就会变得无效。 匿名用户无权访问任何敏感信息。

<a id="recommendations"></a>

## <a name="signalr-security-recommendations"></a>SignalR 安全建议

<a id="ssl"></a>

### <a name="secure-socket-layers-ssl-protocol"></a> (SSL) 协议的安全套接字层

SSL 协议使用加密来保护客户端和服务器之间的数据传输。 如果 SignalR 应用程序在客户端和服务器之间传输敏感信息，请使用 SSL 进行传输。 有关设置 SSL 的详细信息，请参阅 [如何在 IIS 7 上设置 ssl](https://www.iis.net/learn/manage/configuring-security/how-to-set-up-ssl-on-iis)。

<a id="groupsecurity"></a>

### <a name="do-not-use-groups-as-a-security-mechanism"></a>不要将组用作安全机制

组是一种收集相关用户的便捷方法，但它们并不是一种安全机制，用于限制对敏感信息的访问。 当用户可以在重新连接期间自动重新加入组时，尤其如此。 请考虑将特权用户添加到角色，并将对集线器方法的访问仅限制为该角色的成员。 有关基于角色限制访问的示例，请参阅 [SignalR hub 的身份验证和授权](hub-authorization.md)。 有关在重新连接时检查用户对组的访问的示例，请参阅使用 [组](../guide-to-the-api/working-with-groups.md)。

<a id="input"></a>

### <a name="safely-handling-input-from-clients"></a>安全处理来自客户端的输入

若要确保恶意用户不向其他用户发送脚本，你必须对要广播到其他客户端的客户端的所有输入进行编码。 你应对接收客户端而不是服务器上的消息进行编码，因为你的 SignalR 应用程序可能有许多不同类型的客户端。 因此，HTML 编码适用于 web 客户端，但不适用于其他类型的客户端。 例如，用于显示聊天消息的 web 客户端方法可以通过调用函数安全地处理用户名和消息 `html()` 。

[!code-html[Main](introduction-to-security/samples/sample2.html?highlight=3-4)]

<a id="reconcile"></a>

### <a name="reconciling-a-change-in-user-status-with-an-active-connection"></a>协调用户状态更改与活动连接

如果用户的身份验证状态在存在活动连接时发生更改，则用户将收到一条错误消息，指出 "在 active SignalR 连接期间，用户标识无法更改"。 在这种情况下，应用程序应该重新连接到服务器，确保连接 id 和用户名是协调的。 例如，如果你的应用程序允许用户在有活动连接的情况下注销，则连接的用户名将不再与为下一个请求传入的名称匹配。 你需要在用户注销之前停止连接，然后重新启动。

但是，请务必注意，大多数应用程序不需要手动停止并启动连接。 如果你的应用程序在注销后将用户重定向到单独的页（例如 Web 窗体应用程序或 MVC 应用程序中的默认行为），或在注销后刷新当前页，则活动连接将自动断开连接，并且无需任何其他操作。

下面的示例演示如何在用户状态发生更改时停止和启动连接。

[!code-html[Main](introduction-to-security/samples/sample3.html)]

或者，如果你的站点使用窗体身份验证的可调过期，并且没有任何活动来使身份验证 cookie 有效，则用户的身份验证状态可能会发生更改。 在这种情况下，用户将被注销，用户名将不再与连接令牌中的用户名匹配。 通过添加一些定期请求 web 服务器上的资源以使身份验证 cookie 有效的脚本，可以解决此问题。 下面的示例演示如何每隔30分钟请求一次资源。

[!code-javascript[Main](introduction-to-security/samples/sample4.js)]

<a id="autogen"></a>

### <a name="automatically-generated-javascript-proxy-files"></a>自动生成的 JavaScript 代理文件

如果你不想在每个用户的 JavaScript 代理文件中包含所有的中心和方法，则可以禁用文件的自动生成。 如果有多个中心和方法，但不希望每个用户都知道所有方法，则可以选择此选项。 可以通过将 **EnableJavaScriptProxies** 设置为 **false**来禁用自动生成。

[!code-csharp[Main](introduction-to-security/samples/sample5.cs)]

有关 JavaScript 代理文件的详细信息，请参阅 [生成的代理及其功能](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy)。 <a id="exceptions"></a>

### <a name="exceptions"></a>例外

应避免向客户端传递异常对象，因为这些对象可能会向客户端公开敏感信息。 请改为在客户端上调用显示相关错误消息的方法。

[!code-csharp[Main](introduction-to-security/samples/sample6.cs)]

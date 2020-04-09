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
# <a name="introduction-to-signalr-security"></a><span data-ttu-id="28e00-103">SignalR 安全性简介</span><span class="sxs-lookup"><span data-stu-id="28e00-103">Introduction to SignalR Security</span></span>

<span data-ttu-id="28e00-104">由[帕特里克·弗莱彻](https://github.com/pfletcher)，[汤姆·菲茨麦克肯](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="28e00-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="28e00-105">本文介绍了在开发 SignalR 应用程序时必须考虑的安全问题。</span><span class="sxs-lookup"><span data-stu-id="28e00-105">This article describes the security issues you must consider when developing a SignalR application.</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="28e00-106">本主题中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="28e00-106">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="28e00-107">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="28e00-107">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="28e00-108">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="28e00-108">.NET 4.5</span></span>
> - <span data-ttu-id="28e00-109">信号R版本 2</span><span class="sxs-lookup"><span data-stu-id="28e00-109">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="28e00-110">本主题的早期版本</span><span class="sxs-lookup"><span data-stu-id="28e00-110">Previous versions of this topic</span></span>
>
> <span data-ttu-id="28e00-111">有关早期版本的 SignalR 的信息，请参阅[SignalR 旧版本](../older-versions/index.md)。</span><span class="sxs-lookup"><span data-stu-id="28e00-111">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="28e00-112">问题和评论</span><span class="sxs-lookup"><span data-stu-id="28e00-112">Questions and comments</span></span>
>
> <span data-ttu-id="28e00-113">请留下反馈，关于你喜欢本教程的方式，以及我们可以在页面底部的评论中改进什么。</span><span class="sxs-lookup"><span data-stu-id="28e00-113">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="28e00-114">如果您有与本教程没有直接关系的问题，您可以将它们发布到[ASP.NET SignalR 论坛](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com/)。</span><span class="sxs-lookup"><span data-stu-id="28e00-114">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="overview"></a><span data-ttu-id="28e00-115">概述</span><span class="sxs-lookup"><span data-stu-id="28e00-115">Overview</span></span>

<span data-ttu-id="28e00-116">本文档包含以下各节：</span><span class="sxs-lookup"><span data-stu-id="28e00-116">This document contains the following sections:</span></span>

- [<span data-ttu-id="28e00-117">信号R安全概念</span><span class="sxs-lookup"><span data-stu-id="28e00-117">SignalR Security Concepts</span></span>](#concepts)

    - [<span data-ttu-id="28e00-118">身份验证和授权</span><span class="sxs-lookup"><span data-stu-id="28e00-118">Authentication and authorization</span></span>](#authentication)
    - [<span data-ttu-id="28e00-119">连接令牌</span><span class="sxs-lookup"><span data-stu-id="28e00-119">Connection token</span></span>](#connectiontoken)
    - [<span data-ttu-id="28e00-120">重新连接时重新加入组</span><span class="sxs-lookup"><span data-stu-id="28e00-120">Rejoining groups when reconnecting</span></span>](#rejoingroup)
- [<span data-ttu-id="28e00-121">信号器如何防止跨站点请求伪造</span><span class="sxs-lookup"><span data-stu-id="28e00-121">How SignalR prevents Cross-Site Request Forgery</span></span>](#csrf)
- [<span data-ttu-id="28e00-122">信号R安全建议</span><span class="sxs-lookup"><span data-stu-id="28e00-122">SignalR Security Recommendations</span></span>](#recommendations)

    - [<span data-ttu-id="28e00-123">安全套接字层 （SSL） 协议</span><span class="sxs-lookup"><span data-stu-id="28e00-123">Secure Socket Layers (SSL) protocol</span></span>](#ssl)
    - [<span data-ttu-id="28e00-124">不要将组用作安全机制</span><span class="sxs-lookup"><span data-stu-id="28e00-124">Do not use groups as a security mechanism</span></span>](#groupsecurity)
    - [<span data-ttu-id="28e00-125">安全地处理来自客户端的输入</span><span class="sxs-lookup"><span data-stu-id="28e00-125">Safely handling input from clients</span></span>](#input)
    - [<span data-ttu-id="28e00-126">协调用户状态更改与活动连接</span><span class="sxs-lookup"><span data-stu-id="28e00-126">Reconciling a change in user status with an active connection</span></span>](#reconcile)
    - [<span data-ttu-id="28e00-127">自动生成的 JavaScript 代理文件</span><span class="sxs-lookup"><span data-stu-id="28e00-127">Automatically generated JavaScript proxy files</span></span>](#autogen)
    - [<span data-ttu-id="28e00-128">异常</span><span class="sxs-lookup"><span data-stu-id="28e00-128">Exceptions</span></span>](#exceptions)

<a id="concepts"></a>

## <a name="signalr-security-concepts"></a><span data-ttu-id="28e00-129">信号R安全概念</span><span class="sxs-lookup"><span data-stu-id="28e00-129">SignalR Security Concepts</span></span>

<a id="authentication"></a>

### <a name="authentication-and-authorization"></a><span data-ttu-id="28e00-130">身份验证和授权</span><span class="sxs-lookup"><span data-stu-id="28e00-130">Authentication and authorization</span></span>

<span data-ttu-id="28e00-131">SignalR 不提供任何用于验证用户的功能。</span><span class="sxs-lookup"><span data-stu-id="28e00-131">SignalR does not provide any features for authenticating users.</span></span> <span data-ttu-id="28e00-132">相反，您将 SignalR 功能集成到应用程序的现有身份验证结构中。</span><span class="sxs-lookup"><span data-stu-id="28e00-132">Instead, you integrate the SignalR features into the existing authentication structure for an application.</span></span> <span data-ttu-id="28e00-133">您可以像在应用程序中通常一样对用户进行身份验证，并处理 SignalR 代码中的身份验证结果。</span><span class="sxs-lookup"><span data-stu-id="28e00-133">You authenticate users as you would normally in your application, and work with the results of the authentication in your SignalR code.</span></span> <span data-ttu-id="28e00-134">例如，您可以使用ASP.NET窗体身份验证对用户进行身份验证，然后在中心中强制授权哪些用户或角色调用方法。</span><span class="sxs-lookup"><span data-stu-id="28e00-134">For example, you might authenticate your users with ASP.NET forms authentication, and then in your hub, enforce which users or roles are authorized to call a method.</span></span> <span data-ttu-id="28e00-135">在集线器中，还可以将身份验证信息（如用户名或用户是否属于角色）传递给客户端。</span><span class="sxs-lookup"><span data-stu-id="28e00-135">In your hub, you can also pass authentication information, such as user name or whether a user belongs to a role, to the client.</span></span>

<span data-ttu-id="28e00-136">SignalR 提供[授权](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx)属性来指定哪些用户有权访问集线器或方法。</span><span class="sxs-lookup"><span data-stu-id="28e00-136">SignalR provides the [Authorize](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx) attribute to specify which users have access to a hub or method.</span></span> <span data-ttu-id="28e00-137">将"授权"属性应用于中心或中心中的特定方法。</span><span class="sxs-lookup"><span data-stu-id="28e00-137">You apply the Authorize attribute to either a hub or particular methods in a hub.</span></span> <span data-ttu-id="28e00-138">如果没有"授权"属性，则连接到集线器的客户端可以使用集线器上的所有公共方法。</span><span class="sxs-lookup"><span data-stu-id="28e00-138">Without the Authorize attribute, all public methods on the hub are available to a client that is connected to the hub.</span></span> <span data-ttu-id="28e00-139">有关集线器的详细信息，请参阅[SignalR 集线器的身份验证和授权](hub-authorization.md)。</span><span class="sxs-lookup"><span data-stu-id="28e00-139">For more information about hubs, see [Authentication and Authorization for SignalR Hubs](hub-authorization.md).</span></span>

<span data-ttu-id="28e00-140">将`Authorize`属性应用于中心，但不应用于持久连接。</span><span class="sxs-lookup"><span data-stu-id="28e00-140">You apply the `Authorize` attribute to hubs, but not persistent connections.</span></span> <span data-ttu-id="28e00-141">在使用 时强制实施授权规则`PersistentConnection`，必须重写`AuthorizeRequest`方法。</span><span class="sxs-lookup"><span data-stu-id="28e00-141">To enforce authorization rules when using a `PersistentConnection` you must override the `AuthorizeRequest` method.</span></span> <span data-ttu-id="28e00-142">有关持久连接的详细信息，请参阅[SignalR 持久连接的身份验证和授权](persistent-connection-authorization.md)。</span><span class="sxs-lookup"><span data-stu-id="28e00-142">For more information about persistent connections, see [Authentication and Authorization for SignalR Persistent Connections](persistent-connection-authorization.md).</span></span>

<a id="connectiontoken"></a>

### <a name="connection-token"></a><span data-ttu-id="28e00-143">连接令牌</span><span class="sxs-lookup"><span data-stu-id="28e00-143">Connection token</span></span>

<span data-ttu-id="28e00-144">SignalR 通过验证发件人的身份来降低执行恶意命令的风险。</span><span class="sxs-lookup"><span data-stu-id="28e00-144">SignalR mitigates the risk of executing malicious commands by validating the identity of the sender.</span></span> <span data-ttu-id="28e00-145">对于每个请求，客户端和服务器传递一个连接令牌，其中包含经过身份验证的用户的连接 ID 和用户名。</span><span class="sxs-lookup"><span data-stu-id="28e00-145">For each request, the client and server pass a connection token which contains the connection id and username for authenticated users.</span></span> <span data-ttu-id="28e00-146">连接 ID 唯一标识每个连接的客户端。</span><span class="sxs-lookup"><span data-stu-id="28e00-146">The connection id uniquely identifies each connected client.</span></span> <span data-ttu-id="28e00-147">服务器在创建新连接时随机生成连接 ID，并在连接期间保留该 ID。</span><span class="sxs-lookup"><span data-stu-id="28e00-147">The server randomly generates the connection id when a new connection is created, and persists that id for the duration of the connection.</span></span> <span data-ttu-id="28e00-148">Web 应用程序的身份验证机制提供用户名。</span><span class="sxs-lookup"><span data-stu-id="28e00-148">The authentication mechanism for the web application provides the username.</span></span> <span data-ttu-id="28e00-149">SignalR 使用加密和数字签名来保护连接令牌。</span><span class="sxs-lookup"><span data-stu-id="28e00-149">SignalR uses encryption and a digital signature to protect the connection token.</span></span>

![](introduction-to-security/_static/image2.png)

<span data-ttu-id="28e00-150">对于每个请求，服务器验证令牌的内容，以确保请求来自指定用户。</span><span class="sxs-lookup"><span data-stu-id="28e00-150">For each request, the server validates the contents of the token to ensure that the request is coming from the specified user.</span></span> <span data-ttu-id="28e00-151">用户名必须对应于连接 ID。通过验证连接 ID 和用户名，SignalR 可防止恶意用户轻松模拟其他用户。</span><span class="sxs-lookup"><span data-stu-id="28e00-151">The username must correspond to the connection id. By validating both the connection id and the username, SignalR prevents a malicious user from easily impersonating another user.</span></span> <span data-ttu-id="28e00-152">如果服务器无法验证连接令牌，则请求失败。</span><span class="sxs-lookup"><span data-stu-id="28e00-152">If the server cannot validate the connection token, the request fails.</span></span>

![](introduction-to-security/_static/image4.png)

<span data-ttu-id="28e00-153">由于连接 ID 是验证过程的一部分，因此不应向其他用户显示一个用户的连接 ID 或将该值存储在客户端上（如 Cookie 中）。</span><span class="sxs-lookup"><span data-stu-id="28e00-153">Because the connection id is part of the verification process, you should not reveal one user's connection id to other users or store the value on the client, such as in a cookie.</span></span>

#### <a name="connection-tokens-vs-other-token-types"></a><span data-ttu-id="28e00-154">连接令牌与其他令牌类型</span><span class="sxs-lookup"><span data-stu-id="28e00-154">Connection tokens vs. other token types</span></span>

<span data-ttu-id="28e00-155">连接令牌偶尔会被安全工具标记，因为它们看起来像是会话令牌或身份验证令牌，如果暴露，就会造成风险。</span><span class="sxs-lookup"><span data-stu-id="28e00-155">Connection tokens are occasionally flagged by security tools because they appear to be session tokens or authentication tokens, which poses a risk if exposed.</span></span>

<span data-ttu-id="28e00-156">SignalR 的连接令牌不是身份验证令牌。</span><span class="sxs-lookup"><span data-stu-id="28e00-156">SignalR's connection token isn't an authentication token.</span></span> <span data-ttu-id="28e00-157">它用于确认发出此请求的用户与创建连接的用户相同。</span><span class="sxs-lookup"><span data-stu-id="28e00-157">It is used to confirm that the user making this request is the same one that created the connection.</span></span> <span data-ttu-id="28e00-158">连接令牌是必需的，因为ASP.NET SignalR 允许连接在服务器之间移动。</span><span class="sxs-lookup"><span data-stu-id="28e00-158">The connection token is necessary because ASP.NET SignalR allows connections to move between servers.</span></span> <span data-ttu-id="28e00-159">令牌将连接与特定用户关联，但不断言发出请求的用户的身份。</span><span class="sxs-lookup"><span data-stu-id="28e00-159">The token associates the connection with a particular user but doesn't assert the identity of the user making the request.</span></span> <span data-ttu-id="28e00-160">要对 SignalR 请求进行正确身份验证，它必须具有一些其他维护用户身份的令牌，例如 Cookie 或承载令牌。</span><span class="sxs-lookup"><span data-stu-id="28e00-160">For a SignalR request to be properly authenticated, it must have some other token that asserts the identity of the user, such as a cookie or bearer token.</span></span> <span data-ttu-id="28e00-161">但是，连接令牌本身不声明请求是由该用户发出，只是声明令牌中包含的连接 ID 与该用户相关联。</span><span class="sxs-lookup"><span data-stu-id="28e00-161">However, the connection token itself makes no claim that the request was made by that user, only that the connection ID contained within the token is associated with that user.</span></span>

<span data-ttu-id="28e00-162">由于连接令牌不提供自己的身份验证声明，因此它不被视为"会话"或"身份验证"令牌。</span><span class="sxs-lookup"><span data-stu-id="28e00-162">Since the connection token provides no authentication claim of its own, it isn't considered a "session" or "authentication" token.</span></span> <span data-ttu-id="28e00-163">获取给定用户的连接令牌并在作为其他用户（或未身份验证的请求）身份验证的请求中重播该令牌将失败，因为请求的用户标识和存储在令牌中的标识不匹配。</span><span class="sxs-lookup"><span data-stu-id="28e00-163">Taking a given user's connection token and replaying it in a request authenticated as a different user (or an unauthenticated request) will fail, because the user identity of the request and the identity stored in the token won't match.</span></span>

<a id="rejoingroup"></a>

### <a name="rejoining-groups-when-reconnecting"></a><span data-ttu-id="28e00-164">重新连接时重新加入组</span><span class="sxs-lookup"><span data-stu-id="28e00-164">Rejoining groups when reconnecting</span></span>

<span data-ttu-id="28e00-165">默认情况下，SignalR 应用程序在从临时中断重新连接时（例如连接在连接超时之前断开和重新建立连接时）时，将自动将用户重新分配给相应的组。重新连接时，客户端传递一个组令牌，其中包含连接 ID 和分配的组。</span><span class="sxs-lookup"><span data-stu-id="28e00-165">By default, the SignalR application will automatically re-assign a user to the appropriate groups when reconnecting from a temporary disruption, such as when a connection is dropped and re-established before the connection times out. When reconnecting, the client passes a group token that includes the connection id and the assigned groups.</span></span> <span data-ttu-id="28e00-166">组令牌经过数字签名和加密。</span><span class="sxs-lookup"><span data-stu-id="28e00-166">The group token is digitally signed and encrypted.</span></span> <span data-ttu-id="28e00-167">客户端在重新连接后保留相同的连接 ID;因此，从重新连接的客户端传递的连接 ID 必须与客户端使用以前的连接 ID 匹配。</span><span class="sxs-lookup"><span data-stu-id="28e00-167">The client retains the same connection id after a reconnection; therefore, the connection id passed from the reconnected client must match the previous connection id used by the client.</span></span> <span data-ttu-id="28e00-168">此验证可防止恶意用户在重新连接时传递加入未授权组的请求。</span><span class="sxs-lookup"><span data-stu-id="28e00-168">This verification prevents a malicious user from passing requests to join unauthorized groups when reconnecting.</span></span>

<span data-ttu-id="28e00-169">但是，请务必注意，组令牌不会过期。</span><span class="sxs-lookup"><span data-stu-id="28e00-169">However, it's important to note, that the group token does not expire.</span></span> <span data-ttu-id="28e00-170">如果用户过去属于一个组，但被禁止从该组，该用户可能能够模拟包含禁止组的组令牌。</span><span class="sxs-lookup"><span data-stu-id="28e00-170">If a user belonged to a group in the past, but was banned from that group, that user may be able to mimic a group token that includes the prohibited group.</span></span> <span data-ttu-id="28e00-171">如果需要安全地管理哪些用户属于哪些组，则需要将数据存储在服务器上，例如数据库中。</span><span class="sxs-lookup"><span data-stu-id="28e00-171">If you need to securely manage which users belong to which groups, you need to store that data on the server, such as in a database.</span></span> <span data-ttu-id="28e00-172">然后，向应用程序添加逻辑，以验证服务器上的用户是否属于组。</span><span class="sxs-lookup"><span data-stu-id="28e00-172">Then, add logic to your application that verifies on the server whether a user belongs to a group.</span></span> <span data-ttu-id="28e00-173">有关验证组成员身份的示例，请参阅[使用组](../guide-to-the-api/working-with-groups.md)。</span><span class="sxs-lookup"><span data-stu-id="28e00-173">For an example of verifying group membership, see [Working with groups](../guide-to-the-api/working-with-groups.md).</span></span>

<span data-ttu-id="28e00-174">仅当连接在临时中断后重新连接时，自动重新加入组才适用。</span><span class="sxs-lookup"><span data-stu-id="28e00-174">Automatically rejoining groups only applies when a connection is reconnected after a temporary disruption.</span></span> <span data-ttu-id="28e00-175">如果用户通过导航离开应用程序而断开连接，或者应用程序重新启动，则应用程序必须处理如何将该用户添加到正确的组。</span><span class="sxs-lookup"><span data-stu-id="28e00-175">If a user disconnects by navigating away from the application or the application restarts, your application must handle how to add that user to the correct groups.</span></span> <span data-ttu-id="28e00-176">有关详细信息，请参阅[使用组](../guide-to-the-api/working-with-groups.md)。</span><span class="sxs-lookup"><span data-stu-id="28e00-176">For more information, see [Working with groups](../guide-to-the-api/working-with-groups.md).</span></span>

<a id="csrf"></a>

## <a name="how-signalr-prevents-cross-site-request-forgery"></a><span data-ttu-id="28e00-177">信号器如何防止跨站点请求伪造</span><span class="sxs-lookup"><span data-stu-id="28e00-177">How SignalR prevents Cross-Site Request Forgery</span></span>

<span data-ttu-id="28e00-178">跨站点请求伪造 （CSRF） 是恶意站点向用户当前登录的易受攻击站点发送请求的攻击。</span><span class="sxs-lookup"><span data-stu-id="28e00-178">Cross-Site Request Forgery (CSRF) is an attack where a malicious site sends a request to a vulnerable site where the user is currently logged in.</span></span> <span data-ttu-id="28e00-179">SignalR 通过使恶意站点极不可能为 SignalR 应用程序创建有效请求来防止 CSRF。</span><span class="sxs-lookup"><span data-stu-id="28e00-179">SignalR prevents CSRF by making it extremely unlikely for a malicious site to create a valid request for your SignalR application.</span></span>

### <a name="description-of-csrf-attack"></a><span data-ttu-id="28e00-180">CSRF 攻击的描述</span><span class="sxs-lookup"><span data-stu-id="28e00-180">Description of CSRF attack</span></span>

<span data-ttu-id="28e00-181">下面是 CSRF 攻击的示例：</span><span class="sxs-lookup"><span data-stu-id="28e00-181">Here is an example of a CSRF attack:</span></span>

1. <span data-ttu-id="28e00-182">用户使用窗体身份验证登录到www.example.com。</span><span class="sxs-lookup"><span data-stu-id="28e00-182">A user logs into www.example.com, using forms authentication.</span></span>
2. <span data-ttu-id="28e00-183">服务器对用户进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="28e00-183">The server authenticates the user.</span></span> <span data-ttu-id="28e00-184">来自服务器的响应包括身份验证 Cookie。</span><span class="sxs-lookup"><span data-stu-id="28e00-184">The response from the server includes an authentication cookie.</span></span>
3. <span data-ttu-id="28e00-185">无需注销，用户将访问恶意网站。</span><span class="sxs-lookup"><span data-stu-id="28e00-185">Without logging out, the user visits a malicious web site.</span></span> <span data-ttu-id="28e00-186">此恶意网站包含以下 HTML 表单：</span><span class="sxs-lookup"><span data-stu-id="28e00-186">This malicious site contains the following HTML form:</span></span>

    [!code-html[Main](introduction-to-security/samples/sample1.html)]

   <span data-ttu-id="28e00-187">请注意，表单操作发布到易受攻击的网站，而不是恶意站点。</span><span class="sxs-lookup"><span data-stu-id="28e00-187">Notice that the form action posts to the vulnerable site, not to the malicious site.</span></span> <span data-ttu-id="28e00-188">这是CSRF的"跨站点"部分。</span><span class="sxs-lookup"><span data-stu-id="28e00-188">This is the "cross-site" part of CSRF.</span></span>
4. <span data-ttu-id="28e00-189">用户单击提交按钮。</span><span class="sxs-lookup"><span data-stu-id="28e00-189">The user clicks the submit button.</span></span> <span data-ttu-id="28e00-190">浏览器包含带有请求的身份验证 Cookie。</span><span class="sxs-lookup"><span data-stu-id="28e00-190">The browser includes the authentication cookie with the request.</span></span>
5. <span data-ttu-id="28e00-191">请求在具有用户身份验证上下文的example.com服务器上运行，并可以执行允许经过身份验证的用户执行的任何操作。</span><span class="sxs-lookup"><span data-stu-id="28e00-191">The request runs on the example.com server with the user's authentication context, and can do anything that an authenticated user is allowed to do.</span></span>

<span data-ttu-id="28e00-192">尽管此示例要求用户单击窗体按钮，但恶意页面同样可以轻松地运行向 SignalR 应用程序发送 AJAX 请求的脚本。</span><span class="sxs-lookup"><span data-stu-id="28e00-192">Although this example requires the user to click the form button, the malicious page could just as easily run a script that sends an AJAX request to your SignalR application.</span></span> <span data-ttu-id="28e00-193">此外，使用 SSL 不会阻止 CSRF 攻击，因为恶意站点可以发送"https://"请求。</span><span class="sxs-lookup"><span data-stu-id="28e00-193">Moreover, using SSL does not prevent a CSRF attack, because the malicious site can send an "https://" request.</span></span>

<span data-ttu-id="28e00-194">通常，CSRF 攻击可能会针对使用 Cookie 进行身份验证的网站，因为浏览器会将所有相关 Cookie 发送到目标网站。</span><span class="sxs-lookup"><span data-stu-id="28e00-194">Typically, CSRF attacks are possible against web sites that use cookies for authentication, because browsers send all relevant cookies to the destination web site.</span></span> <span data-ttu-id="28e00-195">但是，CSRF 的攻击并不仅限于利用 Cookie。</span><span class="sxs-lookup"><span data-stu-id="28e00-195">However, CSRF attacks are not limited to exploiting cookies.</span></span> <span data-ttu-id="28e00-196">例如，基本身份验证和摘要身份验证也容易受到攻击。</span><span class="sxs-lookup"><span data-stu-id="28e00-196">For example, Basic and Digest authentication are also vulnerable.</span></span> <span data-ttu-id="28e00-197">用户使用"基本"或"摘要"身份验证登录后，浏览器会自动发送凭据，直到会话结束。</span><span class="sxs-lookup"><span data-stu-id="28e00-197">After a user logs in with Basic or Digest authentication, the browser automatically sends the credentials until the session ends.</span></span>

### <a name="csrf-mitigations-taken-by-signalr"></a><span data-ttu-id="28e00-198">SignalR 采取的 CSRF 缓解措施</span><span class="sxs-lookup"><span data-stu-id="28e00-198">CSRF mitigations taken by SignalR</span></span>

<span data-ttu-id="28e00-199">SignalR 采取以下步骤防止恶意站点向应用程序创建有效请求。</span><span class="sxs-lookup"><span data-stu-id="28e00-199">SignalR takes the following steps to prevent a malicious site from creating valid requests to your application.</span></span> <span data-ttu-id="28e00-200">默认情况下，SignalR 执行这些步骤，无需在代码中执行任何操作。</span><span class="sxs-lookup"><span data-stu-id="28e00-200">SignalR takes these steps by default, you do not need to take any action in your code.</span></span>

- <span data-ttu-id="28e00-201">**禁用跨域请求**SignalR 禁用跨域请求，以防止用户从外部域调用 SignalR 终结点。</span><span class="sxs-lookup"><span data-stu-id="28e00-201">**Disable cross domain requests** SignalR disables cross domain requests to prevent users from calling a SignalR endpoint from an external domain.</span></span> <span data-ttu-id="28e00-202">SignalR 认为来自外部域的任何请求都无效，并阻止请求。</span><span class="sxs-lookup"><span data-stu-id="28e00-202">SignalR considers any request from an external domain to be invalid and blocks the request.</span></span> <span data-ttu-id="28e00-203">我们建议您保留此默认行为;但是，我们建议您保留此默认行为。否则，恶意网站可能会诱使用户向您的网站发送命令。</span><span class="sxs-lookup"><span data-stu-id="28e00-203">We recommend that you keep this default behavior; otherwise, a malicious site could trick users into sending commands to your site.</span></span> <span data-ttu-id="28e00-204">如果需要使用跨域请求，请参阅[如何建立跨域连接](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)。</span><span class="sxs-lookup"><span data-stu-id="28e00-204">If you need to use cross domain requests, see     [How to establish a cross-domain connection](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain) .</span></span>
- <span data-ttu-id="28e00-205">**在查询字符串中传递连接令牌，而不是 Cookie**SignalR 将连接令牌作为查询字符串值传递，而不是作为 Cookie 传递。</span><span class="sxs-lookup"><span data-stu-id="28e00-205">**Pass connection token in query string, not cookie** SignalR passes the connection token as a query string value, instead of as a cookie.</span></span> <span data-ttu-id="28e00-206">将连接令牌存储在 Cookie 中不安全，因为当遇到恶意代码时，浏览器可能会无意中转发连接令牌。</span><span class="sxs-lookup"><span data-stu-id="28e00-206">Storing the connection token in a cookie is unsafe because the browser can inadvertently forward the connection token when malicious code is encountered.</span></span> <span data-ttu-id="28e00-207">此外，在查询字符串中传递连接令牌可防止连接令牌保留在当前连接之外。</span><span class="sxs-lookup"><span data-stu-id="28e00-207">Also, passing the connection token in the query string prevents the connection token from persisting beyond the current connection.</span></span> <span data-ttu-id="28e00-208">因此，恶意用户不能根据其他用户的身份验证凭据发出请求。</span><span class="sxs-lookup"><span data-stu-id="28e00-208">Therefore, a malicious user cannot make a request under another user's authentication credentials.</span></span>
- <span data-ttu-id="28e00-209">**验证连接令牌**如[连接令牌](#connectiontoken)部分所述，服务器知道哪个连接 ID 与每个经过身份验证的用户相关联。</span><span class="sxs-lookup"><span data-stu-id="28e00-209">**Verify connection token** As described in the     [Connection token](#connectiontoken) section, the server knows which connection id is associated with each authenticated user.</span></span> <span data-ttu-id="28e00-210">服务器不处理来自连接 ID 与用户名不匹配的任何请求。</span><span class="sxs-lookup"><span data-stu-id="28e00-210">The server does not process any request from a connection id that does not match the user name.</span></span> <span data-ttu-id="28e00-211">恶意用户不太可能猜到有效请求，因为恶意用户必须知道用户名和当前随机生成的连接 ID。连接 ID 一旦结束，该连接 ID 将变为无效。</span><span class="sxs-lookup"><span data-stu-id="28e00-211">It is unlikely a malicious user could guess a valid request because the malicious user would have to know the user name and the current randomly-generated connection id. That connection id becomes invalid as soon as the connection is ended.</span></span> <span data-ttu-id="28e00-212">匿名用户不应访问任何敏感信息。</span><span class="sxs-lookup"><span data-stu-id="28e00-212">Anonymous users should not have access to any sensitive information.</span></span>

<a id="recommendations"></a>

## <a name="signalr-security-recommendations"></a><span data-ttu-id="28e00-213">信号R安全建议</span><span class="sxs-lookup"><span data-stu-id="28e00-213">SignalR Security Recommendations</span></span>

<a id="ssl"></a>

### <a name="secure-socket-layers-ssl-protocol"></a><span data-ttu-id="28e00-214">安全套接字层 （SSL） 协议</span><span class="sxs-lookup"><span data-stu-id="28e00-214">Secure Socket Layers (SSL) protocol</span></span>

<span data-ttu-id="28e00-215">SSL 协议使用加密来保护客户端和服务器之间的数据传输。</span><span class="sxs-lookup"><span data-stu-id="28e00-215">The SSL protocol uses encryption to secure the transport of data between a client and server.</span></span> <span data-ttu-id="28e00-216">如果您的 SignalR 应用程序在客户端和服务器之间传输敏感信息，请使用 SSL 进行传输。</span><span class="sxs-lookup"><span data-stu-id="28e00-216">If your SignalR application transmits sensitive information between the client and server, use SSL for the transport.</span></span> <span data-ttu-id="28e00-217">有关设置 SSL 的详细信息，请参阅[如何在 IIS 7 上设置 SSL。](https://www.iis.net/learn/manage/configuring-security/how-to-set-up-ssl-on-iis)</span><span class="sxs-lookup"><span data-stu-id="28e00-217">For more information about setting up SSL, see [How to set up SSL on IIS 7](https://www.iis.net/learn/manage/configuring-security/how-to-set-up-ssl-on-iis).</span></span>

<a id="groupsecurity"></a>

### <a name="do-not-use-groups-as-a-security-mechanism"></a><span data-ttu-id="28e00-218">不要将组用作安全机制</span><span class="sxs-lookup"><span data-stu-id="28e00-218">Do not use groups as a security mechanism</span></span>

<span data-ttu-id="28e00-219">组是收集相关用户的便捷方式，但它们不是限制对敏感信息访问的安全机制。</span><span class="sxs-lookup"><span data-stu-id="28e00-219">Groups are a convenient way of collecting related users, but they are not a secure mechanism for limiting access to sensitive information.</span></span> <span data-ttu-id="28e00-220">当用户可以在重新连接期间自动重新加入组时，尤其如此。</span><span class="sxs-lookup"><span data-stu-id="28e00-220">This is especially true when users can automatically rejoin groups during a reconnect.</span></span> <span data-ttu-id="28e00-221">相反，请考虑将特权用户添加到角色，并将对中心方法的访问限制为该角色的成员。</span><span class="sxs-lookup"><span data-stu-id="28e00-221">Instead, consider adding privileged users to a role and limiting access to a hub method to only members of that role.</span></span> <span data-ttu-id="28e00-222">有关基于角色限制访问的示例，请参阅[SignalR 中心的身份验证和授权](hub-authorization.md)。</span><span class="sxs-lookup"><span data-stu-id="28e00-222">For an example of restricting access based on a role, see [Authentication and Authorization for SignalR Hubs](hub-authorization.md).</span></span> <span data-ttu-id="28e00-223">有关在重新连接时检查用户访问组的示例，请参阅[使用组](../guide-to-the-api/working-with-groups.md)。</span><span class="sxs-lookup"><span data-stu-id="28e00-223">For an example of checking user access to groups when reconnecting, see [Working with groups](../guide-to-the-api/working-with-groups.md).</span></span>

<a id="input"></a>

### <a name="safely-handling-input-from-clients"></a><span data-ttu-id="28e00-224">安全地处理来自客户端的输入</span><span class="sxs-lookup"><span data-stu-id="28e00-224">Safely handling input from clients</span></span>

<span data-ttu-id="28e00-225">为了确保恶意用户不会向其他用户发送脚本，您必须对客户端用于广播到其他客户端的所有输入进行编码。</span><span class="sxs-lookup"><span data-stu-id="28e00-225">To ensure that a malicious user does not send script to other users, you must encode all input from clients that is intended for broadcast to other clients.</span></span> <span data-ttu-id="28e00-226">您应该对接收客户端而不是服务器上的消息进行编码，因为 SignalR 应用程序可能具有许多不同类型的客户端。</span><span class="sxs-lookup"><span data-stu-id="28e00-226">You should encode messages on the receiving clients rather than the server, because your SignalR application may have many different types of clients.</span></span> <span data-ttu-id="28e00-227">因此，HTML 编码适用于 Web 客户端，但对于其他类型的客户端则不有效。</span><span class="sxs-lookup"><span data-stu-id="28e00-227">Therefore, HTML-encoding works for a web client, but not for other types of clients.</span></span> <span data-ttu-id="28e00-228">例如，显示聊天消息的 Web 客户端方法可以通过调用`html()`函数安全地处理用户名和消息。</span><span class="sxs-lookup"><span data-stu-id="28e00-228">For example, a web client method to display a chat message would safely handle the user name and message by calling the `html()` function.</span></span>

[!code-html[Main](introduction-to-security/samples/sample2.html?highlight=3-4)]

<a id="reconcile"></a>

### <a name="reconciling-a-change-in-user-status-with-an-active-connection"></a><span data-ttu-id="28e00-229">协调用户状态更改与活动连接</span><span class="sxs-lookup"><span data-stu-id="28e00-229">Reconciling a change in user status with an active connection</span></span>

<span data-ttu-id="28e00-230">如果用户的身份验证状态在存在活动连接时发生更改，则用户将收到一个错误，指出"用户标识在活动 SignalR 连接期间无法更改"。</span><span class="sxs-lookup"><span data-stu-id="28e00-230">If a user's authentication status changes while an active connection exists, the user will receive an error that states, "The user identity cannot change during an active SignalR connection."</span></span> <span data-ttu-id="28e00-231">在这种情况下，应用程序应重新连接到服务器，以确保连接 ID 和用户名得到协调。</span><span class="sxs-lookup"><span data-stu-id="28e00-231">In that case, your application should re-connect to the server to make sure the connection id and username are coordinated.</span></span> <span data-ttu-id="28e00-232">例如，如果应用程序允许用户在存在活动连接时注销，则连接的用户名将不再与为下一个请求传入的名称匹配。</span><span class="sxs-lookup"><span data-stu-id="28e00-232">For example, if your application allows the user to log out while an active connection exists, the username for the connection will no longer match the name that is passed in for the next request.</span></span> <span data-ttu-id="28e00-233">您需要在用户注销之前停止连接，然后重新启动它。</span><span class="sxs-lookup"><span data-stu-id="28e00-233">You will want to stop the connection before the user logs out, and then restart it.</span></span>

<span data-ttu-id="28e00-234">但是，请务必注意，大多数应用程序不需要手动停止并启动连接。</span><span class="sxs-lookup"><span data-stu-id="28e00-234">However, it is important to note that most applications will not need to manually stop and start the connection.</span></span> <span data-ttu-id="28e00-235">如果应用程序在注销后将用户重定向到单独的页面（例如 Web 窗体应用程序或 MVC 应用程序中的默认行为，或在注销后刷新当前页面，则活动连接将自动断开连接，不需要任何其他操作。</span><span class="sxs-lookup"><span data-stu-id="28e00-235">If your application redirects users to a separate page after logging out, such as the default behavior in a Web Forms application or MVC application, or refreshes the current page after logging out, the active connection is automatically disconnected and does not require any additional action.</span></span>

<span data-ttu-id="28e00-236">下面的示例演示如何在用户状态更改时停止和启动连接。</span><span class="sxs-lookup"><span data-stu-id="28e00-236">The following example shows how to stop and start a connection when the user status has changed.</span></span>

[!code-html[Main](introduction-to-security/samples/sample3.html)]

<span data-ttu-id="28e00-237">或者，如果您的网站使用表单身份验证的滑动过期，并且没有活动保持身份验证 Cookie 的有效性，则用户的身份验证状态可能会更改。</span><span class="sxs-lookup"><span data-stu-id="28e00-237">Or, the user's authentication status may change if your site uses sliding expiration with Forms Authentication, and there is no activity to keep the authentication cookie valid.</span></span> <span data-ttu-id="28e00-238">在这种情况下，用户将被注销，用户名将不再与连接令牌中的用户名匹配。</span><span class="sxs-lookup"><span data-stu-id="28e00-238">In that case, the user will be logged out and the user name will no longer match the user name in the connection token.</span></span> <span data-ttu-id="28e00-239">您可以通过添加一些脚本来解决此问题，这些脚本定期请求 Web 服务器上的资源以保持身份验证 Cookie 的有效性。</span><span class="sxs-lookup"><span data-stu-id="28e00-239">You can fix this problem by adding some script that periodically requests a resource on the web server to keep the authentication cookie valid.</span></span> <span data-ttu-id="28e00-240">下面的示例演示如何每 30 分钟请求一次资源。</span><span class="sxs-lookup"><span data-stu-id="28e00-240">The following example shows how to request a resource every 30 minutes.</span></span>

[!code-javascript[Main](introduction-to-security/samples/sample4.js)]

<a id="autogen"></a>

### <a name="automatically-generated-javascript-proxy-files"></a><span data-ttu-id="28e00-241">自动生成的 JavaScript 代理文件</span><span class="sxs-lookup"><span data-stu-id="28e00-241">Automatically generated JavaScript proxy files</span></span>

<span data-ttu-id="28e00-242">如果不想在每个用户的 JavaScript 代理文件中包含所有中心和方法，则可以禁用该文件的自动生成。</span><span class="sxs-lookup"><span data-stu-id="28e00-242">If you do not want to include all of the hubs and methods in the JavaScript proxy file for each user, you can disable the automatic generation of the file.</span></span> <span data-ttu-id="28e00-243">如果有多个集线器和方法，但不希望每个用户都了解所有方法，则可以选择此选项。</span><span class="sxs-lookup"><span data-stu-id="28e00-243">You might choose this option if you have multiple hubs and methods, but do not want every user to be aware of all of the methods.</span></span> <span data-ttu-id="28e00-244">通过将**启用JavaScriptProxie设置为** **false，** 可以禁用自动生成。</span><span class="sxs-lookup"><span data-stu-id="28e00-244">You disable automatic generation by setting **EnableJavaScriptProxies** to **false**.</span></span>

[!code-csharp[Main](introduction-to-security/samples/sample5.cs)]

<span data-ttu-id="28e00-245">有关 JavaScript 代理文件的详细信息，请参阅[生成的代理及其为您做什么](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy)。</span><span class="sxs-lookup"><span data-stu-id="28e00-245">For more information about the JavaScript proxy files, see [The generated proxy and what it does for you](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy).</span></span> <a id="exceptions"></a>

### <a name="exceptions"></a><span data-ttu-id="28e00-246">例外</span><span class="sxs-lookup"><span data-stu-id="28e00-246">Exceptions</span></span>

<span data-ttu-id="28e00-247">应避免将异常对象传递给客户端，因为对象可能会向客户端公开敏感信息。</span><span class="sxs-lookup"><span data-stu-id="28e00-247">You should avoid passing exception objects to clients because the objects may expose sensitive information to the clients.</span></span> <span data-ttu-id="28e00-248">相反，在显示相关错误消息的客户端上调用方法。</span><span class="sxs-lookup"><span data-stu-id="28e00-248">Instead, call a method on the client that displays the relevant error message.</span></span>

[!code-csharp[Main](introduction-to-security/samples/sample6.cs)]

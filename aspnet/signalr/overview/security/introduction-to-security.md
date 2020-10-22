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
# <a name="introduction-to-signalr-security"></a><span data-ttu-id="3a548-103">SignalR 安全性简介</span><span class="sxs-lookup"><span data-stu-id="3a548-103">Introduction to SignalR Security</span></span>

<span data-ttu-id="3a548-104">作者： [Fletcher](https://github.com/pfletcher)， [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="3a548-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="3a548-105">本文介绍了在开发 SignalR 应用程序时必须考虑的安全问题。</span><span class="sxs-lookup"><span data-stu-id="3a548-105">This article describes the security issues you must consider when developing a SignalR application.</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="3a548-106">本主题中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="3a548-106">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="3a548-107">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="3a548-107">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="3a548-108">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="3a548-108">.NET 4.5</span></span>
> - <span data-ttu-id="3a548-109">SignalR 版本2</span><span class="sxs-lookup"><span data-stu-id="3a548-109">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="3a548-110">本主题的早期版本</span><span class="sxs-lookup"><span data-stu-id="3a548-110">Previous versions of this topic</span></span>
>
> <span data-ttu-id="3a548-111">有关早期版本的 SignalR 的信息，请参阅 [SignalR 旧版本](../older-versions/index.md)。</span><span class="sxs-lookup"><span data-stu-id="3a548-111">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="3a548-112">问题和注释</span><span class="sxs-lookup"><span data-stu-id="3a548-112">Questions and comments</span></span>
>
> <span data-ttu-id="3a548-113">请提供有关你喜欢本教程的方式的反馈，并在页面底部的评论中留下反馈。</span><span class="sxs-lookup"><span data-stu-id="3a548-113">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="3a548-114">如果你有与本教程不直接相关的问题，则可以将其发布到 [ASP.NET SignalR 论坛](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 或 [StackOverflow.com](http://stackoverflow.com/)。</span><span class="sxs-lookup"><span data-stu-id="3a548-114">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="overview"></a><span data-ttu-id="3a548-115">概述</span><span class="sxs-lookup"><span data-stu-id="3a548-115">Overview</span></span>

<span data-ttu-id="3a548-116">本文档包含以下各节：</span><span class="sxs-lookup"><span data-stu-id="3a548-116">This document contains the following sections:</span></span>

- [<span data-ttu-id="3a548-117">SignalR 安全概念</span><span class="sxs-lookup"><span data-stu-id="3a548-117">SignalR Security Concepts</span></span>](#concepts)

    - [<span data-ttu-id="3a548-118">身份验证和授权</span><span class="sxs-lookup"><span data-stu-id="3a548-118">Authentication and authorization</span></span>](#authentication)
    - [<span data-ttu-id="3a548-119">连接令牌</span><span class="sxs-lookup"><span data-stu-id="3a548-119">Connection token</span></span>](#connectiontoken)
    - [<span data-ttu-id="3a548-120">重新连接时的重新加入组</span><span class="sxs-lookup"><span data-stu-id="3a548-120">Rejoining groups when reconnecting</span></span>](#rejoingroup)
- [<span data-ttu-id="3a548-121">SignalR 如何阻止跨站点请求伪造</span><span class="sxs-lookup"><span data-stu-id="3a548-121">How SignalR prevents Cross-Site Request Forgery</span></span>](#csrf)
- [<span data-ttu-id="3a548-122">SignalR 安全建议</span><span class="sxs-lookup"><span data-stu-id="3a548-122">SignalR Security Recommendations</span></span>](#recommendations)

    - [<span data-ttu-id="3a548-123"> (SSL) 协议的安全套接字层</span><span class="sxs-lookup"><span data-stu-id="3a548-123">Secure Socket Layers (SSL) protocol</span></span>](#ssl)
    - [<span data-ttu-id="3a548-124">不要将组用作安全机制</span><span class="sxs-lookup"><span data-stu-id="3a548-124">Do not use groups as a security mechanism</span></span>](#groupsecurity)
    - [<span data-ttu-id="3a548-125">安全处理来自客户端的输入</span><span class="sxs-lookup"><span data-stu-id="3a548-125">Safely handling input from clients</span></span>](#input)
    - [<span data-ttu-id="3a548-126">协调用户状态更改与活动连接</span><span class="sxs-lookup"><span data-stu-id="3a548-126">Reconciling a change in user status with an active connection</span></span>](#reconcile)
    - [<span data-ttu-id="3a548-127">自动生成的 JavaScript 代理文件</span><span class="sxs-lookup"><span data-stu-id="3a548-127">Automatically generated JavaScript proxy files</span></span>](#autogen)
    - [<span data-ttu-id="3a548-128">异常</span><span class="sxs-lookup"><span data-stu-id="3a548-128">Exceptions</span></span>](#exceptions)

<a id="concepts"></a>

## <a name="signalr-security-concepts"></a><span data-ttu-id="3a548-129">SignalR 安全概念</span><span class="sxs-lookup"><span data-stu-id="3a548-129">SignalR Security Concepts</span></span>

<a id="authentication"></a>

### <a name="authentication-and-authorization"></a><span data-ttu-id="3a548-130">身份验证和授权</span><span class="sxs-lookup"><span data-stu-id="3a548-130">Authentication and authorization</span></span>

<span data-ttu-id="3a548-131">SignalR 不提供任何用于对用户进行身份验证的功能。</span><span class="sxs-lookup"><span data-stu-id="3a548-131">SignalR does not provide any features for authenticating users.</span></span> <span data-ttu-id="3a548-132">相反，将 SignalR 功能集成到应用程序的现有身份验证结构中。</span><span class="sxs-lookup"><span data-stu-id="3a548-132">Instead, you integrate the SignalR features into the existing authentication structure for an application.</span></span> <span data-ttu-id="3a548-133">在应用程序中按通常的方式对用户进行身份验证，并在 SignalR 代码中处理身份验证的结果。</span><span class="sxs-lookup"><span data-stu-id="3a548-133">You authenticate users as you would normally in your application, and work with the results of the authentication in your SignalR code.</span></span> <span data-ttu-id="3a548-134">例如，你可以使用 ASP.NET forms 身份验证对用户进行身份验证，然后在你的中心内强制实施有权调用方法的用户或角色。</span><span class="sxs-lookup"><span data-stu-id="3a548-134">For example, you might authenticate your users with ASP.NET forms authentication, and then in your hub, enforce which users or roles are authorized to call a method.</span></span> <span data-ttu-id="3a548-135">你还可以在中心将身份验证信息（如用户名或用户是否属于角色）传递给客户端。</span><span class="sxs-lookup"><span data-stu-id="3a548-135">In your hub, you can also pass authentication information, such as user name or whether a user belongs to a role, to the client.</span></span>

<span data-ttu-id="3a548-136">SignalR 提供 [授权](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx) 属性以指定哪些用户有权访问集线器或方法。</span><span class="sxs-lookup"><span data-stu-id="3a548-136">SignalR provides the [Authorize](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx) attribute to specify which users have access to a hub or method.</span></span> <span data-ttu-id="3a548-137">将授权属性应用于中心中的集线器或特定方法。</span><span class="sxs-lookup"><span data-stu-id="3a548-137">You apply the Authorize attribute to either a hub or particular methods in a hub.</span></span> <span data-ttu-id="3a548-138">如果没有授权属性，则中心上的所有公共方法都可用于连接到中心的客户端。</span><span class="sxs-lookup"><span data-stu-id="3a548-138">Without the Authorize attribute, all public methods on the hub are available to a client that is connected to the hub.</span></span> <span data-ttu-id="3a548-139">有关中心的详细信息，请参阅 [SignalR hub 的身份验证和授权](hub-authorization.md)。</span><span class="sxs-lookup"><span data-stu-id="3a548-139">For more information about hubs, see [Authentication and Authorization for SignalR Hubs](hub-authorization.md).</span></span>

<span data-ttu-id="3a548-140">将该属性应用于 `Authorize` 中心，但不应用于持久性连接。</span><span class="sxs-lookup"><span data-stu-id="3a548-140">You apply the `Authorize` attribute to hubs, but not persistent connections.</span></span> <span data-ttu-id="3a548-141">若要在使用时强制执行授权规则 `PersistentConnection` ，必须重写 `AuthorizeRequest` 方法。</span><span class="sxs-lookup"><span data-stu-id="3a548-141">To enforce authorization rules when using a `PersistentConnection` you must override the `AuthorizeRequest` method.</span></span> <span data-ttu-id="3a548-142">有关永久性连接的详细信息，请参阅 [SignalR 永久性连接的身份验证和授权](persistent-connection-authorization.md)。</span><span class="sxs-lookup"><span data-stu-id="3a548-142">For more information about persistent connections, see [Authentication and Authorization for SignalR Persistent Connections](persistent-connection-authorization.md).</span></span>

<a id="connectiontoken"></a>

### <a name="connection-token"></a><span data-ttu-id="3a548-143">连接令牌</span><span class="sxs-lookup"><span data-stu-id="3a548-143">Connection token</span></span>

<span data-ttu-id="3a548-144">SignalR 通过验证发件人的身份，降低执行恶意命令的风险。</span><span class="sxs-lookup"><span data-stu-id="3a548-144">SignalR mitigates the risk of executing malicious commands by validating the identity of the sender.</span></span> <span data-ttu-id="3a548-145">对于每个请求，客户端和服务器传递一个连接令牌，其中包含经过身份验证的用户的连接 id 和用户名。</span><span class="sxs-lookup"><span data-stu-id="3a548-145">For each request, the client and server pass a connection token which contains the connection id and username for authenticated users.</span></span> <span data-ttu-id="3a548-146">连接 id 唯一标识每个连接的客户端。</span><span class="sxs-lookup"><span data-stu-id="3a548-146">The connection id uniquely identifies each connected client.</span></span> <span data-ttu-id="3a548-147">在创建新连接时，服务器会随机生成连接 id，并在连接持续时间内保留该 id。</span><span class="sxs-lookup"><span data-stu-id="3a548-147">The server randomly generates the connection id when a new connection is created, and persists that id for the duration of the connection.</span></span> <span data-ttu-id="3a548-148">Web 应用程序的身份验证机制提供用户名。</span><span class="sxs-lookup"><span data-stu-id="3a548-148">The authentication mechanism for the web application provides the username.</span></span> <span data-ttu-id="3a548-149">SignalR 使用加密和数字签名来保护连接令牌。</span><span class="sxs-lookup"><span data-stu-id="3a548-149">SignalR uses encryption and a digital signature to protect the connection token.</span></span>

![](introduction-to-security/_static/image2.png)

<span data-ttu-id="3a548-150">对于每个请求，服务器会验证令牌的内容，以确保请求来自指定的用户。</span><span class="sxs-lookup"><span data-stu-id="3a548-150">For each request, the server validates the contents of the token to ensure that the request is coming from the specified user.</span></span> <span data-ttu-id="3a548-151">用户名必须与连接 id 相对应。通过验证连接 id 和用户名，SignalR 可防止恶意用户轻松地模拟其他用户。</span><span class="sxs-lookup"><span data-stu-id="3a548-151">The username must correspond to the connection id. By validating both the connection id and the username, SignalR prevents a malicious user from easily impersonating another user.</span></span> <span data-ttu-id="3a548-152">如果服务器无法验证连接令牌，请求会失败。</span><span class="sxs-lookup"><span data-stu-id="3a548-152">If the server cannot validate the connection token, the request fails.</span></span>

![](introduction-to-security/_static/image4.png)

<span data-ttu-id="3a548-153">由于连接 id 是验证过程的一部分，因此不应将一个用户的连接 id 泄露给其他用户，或将该值存储在客户端上，例如在 cookie 中。</span><span class="sxs-lookup"><span data-stu-id="3a548-153">Because the connection id is part of the verification process, you should not reveal one user's connection id to other users or store the value on the client, such as in a cookie.</span></span>

#### <a name="connection-tokens-vs-other-token-types"></a><span data-ttu-id="3a548-154">连接令牌与其他令牌类型</span><span class="sxs-lookup"><span data-stu-id="3a548-154">Connection tokens vs. other token types</span></span>

<span data-ttu-id="3a548-155">安全工具有时会标记连接令牌，因为它们看起来像是会话令牌或身份验证令牌，如果公开，则会带来风险。</span><span class="sxs-lookup"><span data-stu-id="3a548-155">Connection tokens are occasionally flagged by security tools because they appear to be session tokens or authentication tokens, which poses a risk if exposed.</span></span>

<span data-ttu-id="3a548-156">SignalR 的连接令牌不是身份验证令牌。</span><span class="sxs-lookup"><span data-stu-id="3a548-156">SignalR's connection token isn't an authentication token.</span></span> <span data-ttu-id="3a548-157">它用于确认发出此请求的用户与创建连接的用户相同。</span><span class="sxs-lookup"><span data-stu-id="3a548-157">It is used to confirm that the user making this request is the same one that created the connection.</span></span> <span data-ttu-id="3a548-158">连接令牌是必需的，因为 ASP.NET SignalR 允许在服务器之间移动连接。</span><span class="sxs-lookup"><span data-stu-id="3a548-158">The connection token is necessary because ASP.NET SignalR allows connections to move between servers.</span></span> <span data-ttu-id="3a548-159">该令牌将连接与特定用户关联，但不会声明发出请求的用户的标识。</span><span class="sxs-lookup"><span data-stu-id="3a548-159">The token associates the connection with a particular user but doesn't assert the identity of the user making the request.</span></span> <span data-ttu-id="3a548-160">若要对 SignalR 请求进行正确的身份验证，它必须具有另一个断言用户身份的标记，如 cookie 或持有者令牌。</span><span class="sxs-lookup"><span data-stu-id="3a548-160">For a SignalR request to be properly authenticated, it must have some other token that asserts the identity of the user, such as a cookie or bearer token.</span></span> <span data-ttu-id="3a548-161">不过，连接令牌本身不会声明该用户发出请求，只有令牌中包含的连接 ID 与该用户相关联。</span><span class="sxs-lookup"><span data-stu-id="3a548-161">However, the connection token itself makes no claim that the request was made by that user, only that the connection ID contained within the token is associated with that user.</span></span>

<span data-ttu-id="3a548-162">由于连接令牌不提供自身的身份验证声明，因此不会将其视为 "会话" 或 "身份验证" 令牌。</span><span class="sxs-lookup"><span data-stu-id="3a548-162">Since the connection token provides no authentication claim of its own, it isn't considered a "session" or "authentication" token.</span></span> <span data-ttu-id="3a548-163">获取给定用户的连接令牌并将其重播到作为不同用户 (身份验证的请求中，否则) 不经过身份验证的请求将失败，因为请求的用户标识和令牌中存储的标识不匹配。</span><span class="sxs-lookup"><span data-stu-id="3a548-163">Taking a given user's connection token and replaying it in a request authenticated as a different user (or an unauthenticated request) will fail, because the user identity of the request and the identity stored in the token won't match.</span></span>

<a id="rejoingroup"></a>

### <a name="rejoining-groups-when-reconnecting"></a><span data-ttu-id="3a548-164">重新连接时的重新加入组</span><span class="sxs-lookup"><span data-stu-id="3a548-164">Rejoining groups when reconnecting</span></span>

<span data-ttu-id="3a548-165">默认情况下，当从暂时中断重新连接时，SignalR 应用程序会自动将用户重新分配给相应的组，例如在连接断开之前断开并重新建立连接。重新连接时，客户端会传递包含连接 id 和分配组的组令牌。</span><span class="sxs-lookup"><span data-stu-id="3a548-165">By default, the SignalR application will automatically re-assign a user to the appropriate groups when reconnecting from a temporary disruption, such as when a connection is dropped and re-established before the connection times out. When reconnecting, the client passes a group token that includes the connection id and the assigned groups.</span></span> <span data-ttu-id="3a548-166">组令牌已进行数字签名和加密。</span><span class="sxs-lookup"><span data-stu-id="3a548-166">The group token is digitally signed and encrypted.</span></span> <span data-ttu-id="3a548-167">重新连接后，客户端将保留相同的连接 id;因此，从重新连接的客户端传递的连接 id 必须与客户端使用的以前的连接 id 匹配。</span><span class="sxs-lookup"><span data-stu-id="3a548-167">The client retains the same connection id after a reconnection; therefore, the connection id passed from the reconnected client must match the previous connection id used by the client.</span></span> <span data-ttu-id="3a548-168">此验证可防止恶意用户在重新连接时将请求传递给加入未经授权的组。</span><span class="sxs-lookup"><span data-stu-id="3a548-168">This verification prevents a malicious user from passing requests to join unauthorized groups when reconnecting.</span></span>

<span data-ttu-id="3a548-169">但是，请务必注意，组令牌不会过期。</span><span class="sxs-lookup"><span data-stu-id="3a548-169">However, it's important to note, that the group token does not expire.</span></span> <span data-ttu-id="3a548-170">如果用户属于过去的某个组，但从该组中被禁止，则该用户可能能够模拟包含禁止组的组令牌。</span><span class="sxs-lookup"><span data-stu-id="3a548-170">If a user belonged to a group in the past, but was banned from that group, that user may be able to mimic a group token that includes the prohibited group.</span></span> <span data-ttu-id="3a548-171">如果你需要安全地管理属于哪些组的用户，则需要将该数据存储在服务器上，例如在数据库中。</span><span class="sxs-lookup"><span data-stu-id="3a548-171">If you need to securely manage which users belong to which groups, you need to store that data on the server, such as in a database.</span></span> <span data-ttu-id="3a548-172">然后，将逻辑添加到应用程序，以便在服务器上验证用户是否属于组。</span><span class="sxs-lookup"><span data-stu-id="3a548-172">Then, add logic to your application that verifies on the server whether a user belongs to a group.</span></span> <span data-ttu-id="3a548-173">有关验证组成员身份的示例，请参阅 [使用组](../guide-to-the-api/working-with-groups.md)。</span><span class="sxs-lookup"><span data-stu-id="3a548-173">For an example of verifying group membership, see [Working with groups](../guide-to-the-api/working-with-groups.md).</span></span>

<span data-ttu-id="3a548-174">仅当在暂时中断后重新连接连接时，自动重新加入组才适用。</span><span class="sxs-lookup"><span data-stu-id="3a548-174">Automatically rejoining groups only applies when a connection is reconnected after a temporary disruption.</span></span> <span data-ttu-id="3a548-175">如果用户通过离开应用程序或重新启动应用程序而断开连接，则应用程序必须处理如何将该用户添加到正确的组。</span><span class="sxs-lookup"><span data-stu-id="3a548-175">If a user disconnects by navigating away from the application or the application restarts, your application must handle how to add that user to the correct groups.</span></span> <span data-ttu-id="3a548-176">有关详细信息，请参阅使用 [组](../guide-to-the-api/working-with-groups.md)。</span><span class="sxs-lookup"><span data-stu-id="3a548-176">For more information, see [Working with groups](../guide-to-the-api/working-with-groups.md).</span></span>

<a id="csrf"></a>

## <a name="how-signalr-prevents-cross-site-request-forgery"></a><span data-ttu-id="3a548-177">SignalR 如何阻止跨站点请求伪造</span><span class="sxs-lookup"><span data-stu-id="3a548-177">How SignalR prevents Cross-Site Request Forgery</span></span>

<span data-ttu-id="3a548-178">跨站点请求伪造 (CSRF) 是一种攻击，其中恶意站点将请求发送到用户当前登录到的有漏洞站点。</span><span class="sxs-lookup"><span data-stu-id="3a548-178">Cross-Site Request Forgery (CSRF) is an attack where a malicious site sends a request to a vulnerable site where the user is currently logged in.</span></span> <span data-ttu-id="3a548-179">SignalR 通过使恶意网站极不可能为 SignalR 应用程序创建有效请求来防止 CSRF。</span><span class="sxs-lookup"><span data-stu-id="3a548-179">SignalR prevents CSRF by making it extremely unlikely for a malicious site to create a valid request for your SignalR application.</span></span>

### <a name="description-of-csrf-attack"></a><span data-ttu-id="3a548-180">CSRF 攻击说明</span><span class="sxs-lookup"><span data-stu-id="3a548-180">Description of CSRF attack</span></span>

<span data-ttu-id="3a548-181">下面是 CSRF 攻击的示例：</span><span class="sxs-lookup"><span data-stu-id="3a548-181">Here is an example of a CSRF attack:</span></span>

1. <span data-ttu-id="3a548-182">用户使用窗体身份验证登录到 www.example.com。</span><span class="sxs-lookup"><span data-stu-id="3a548-182">A user logs into www.example.com, using forms authentication.</span></span>
2. <span data-ttu-id="3a548-183">服务器对用户进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="3a548-183">The server authenticates the user.</span></span> <span data-ttu-id="3a548-184">来自服务器的响应包含一个身份验证 cookie。</span><span class="sxs-lookup"><span data-stu-id="3a548-184">The response from the server includes an authentication cookie.</span></span>
3. <span data-ttu-id="3a548-185">如果不注销，用户将访问恶意网站。</span><span class="sxs-lookup"><span data-stu-id="3a548-185">Without logging out, the user visits a malicious web site.</span></span> <span data-ttu-id="3a548-186">此恶意网站包含以下 HTML 格式：</span><span class="sxs-lookup"><span data-stu-id="3a548-186">This malicious site contains the following HTML form:</span></span>

    [!code-html[Main](introduction-to-security/samples/sample1.html)]

   <span data-ttu-id="3a548-187">请注意，窗体操作会发布到易受攻击的站点，而不是恶意站点。</span><span class="sxs-lookup"><span data-stu-id="3a548-187">Notice that the form action posts to the vulnerable site, not to the malicious site.</span></span> <span data-ttu-id="3a548-188">这是 CSRF 的 "跨站点" 部分。</span><span class="sxs-lookup"><span data-stu-id="3a548-188">This is the "cross-site" part of CSRF.</span></span>
4. <span data-ttu-id="3a548-189">用户单击 "提交" 按钮。</span><span class="sxs-lookup"><span data-stu-id="3a548-189">The user clicks the submit button.</span></span> <span data-ttu-id="3a548-190">浏览器包含请求中的身份验证 cookie。</span><span class="sxs-lookup"><span data-stu-id="3a548-190">The browser includes the authentication cookie with the request.</span></span>
5. <span data-ttu-id="3a548-191">请求使用用户的身份验证上下文在 example.com 服务器上运行，并可执行允许经过身份验证的用户执行的任何操作。</span><span class="sxs-lookup"><span data-stu-id="3a548-191">The request runs on the example.com server with the user's authentication context, and can do anything that an authenticated user is allowed to do.</span></span>

<span data-ttu-id="3a548-192">尽管此示例要求用户单击 "窗体" 按钮，但恶意页面可以轻松地运行一个将 AJAX 请求发送到 SignalR 应用程序的脚本。</span><span class="sxs-lookup"><span data-stu-id="3a548-192">Although this example requires the user to click the form button, the malicious page could just as easily run a script that sends an AJAX request to your SignalR application.</span></span> <span data-ttu-id="3a548-193">而且，使用 SSL 不会阻止 CSRF 攻击，因为恶意站点可以发送 "https://" 请求。</span><span class="sxs-lookup"><span data-stu-id="3a548-193">Moreover, using SSL does not prevent a CSRF attack, because the malicious site can send an "https://" request.</span></span>

<span data-ttu-id="3a548-194">通常，可以对使用 cookie 进行身份验证的网站执行 CSRF 攻击，因为浏览器会将所有相关 cookie 发送到目标网站。</span><span class="sxs-lookup"><span data-stu-id="3a548-194">Typically, CSRF attacks are possible against web sites that use cookies for authentication, because browsers send all relevant cookies to the destination web site.</span></span> <span data-ttu-id="3a548-195">但是，CSRF 攻击并不局限于利用 cookie。</span><span class="sxs-lookup"><span data-stu-id="3a548-195">However, CSRF attacks are not limited to exploiting cookies.</span></span> <span data-ttu-id="3a548-196">例如，基本身份验证和摘要式身份验证也容易受到攻击。</span><span class="sxs-lookup"><span data-stu-id="3a548-196">For example, Basic and Digest authentication are also vulnerable.</span></span> <span data-ttu-id="3a548-197">用户使用基本或摘要式身份验证登录后，浏览器会自动发送凭据，直到会话结束。</span><span class="sxs-lookup"><span data-stu-id="3a548-197">After a user logs in with Basic or Digest authentication, the browser automatically sends the credentials until the session ends.</span></span>

### <a name="csrf-mitigations-taken-by-signalr"></a><span data-ttu-id="3a548-198">SignalR 执行的 CSRF 缓解措施</span><span class="sxs-lookup"><span data-stu-id="3a548-198">CSRF mitigations taken by SignalR</span></span>

<span data-ttu-id="3a548-199">SignalR 执行以下步骤，以防止恶意网站创建对应用程序的有效请求。</span><span class="sxs-lookup"><span data-stu-id="3a548-199">SignalR takes the following steps to prevent a malicious site from creating valid requests to your application.</span></span> <span data-ttu-id="3a548-200">默认情况下，SignalR 会执行这些步骤，无需在代码中执行任何操作。</span><span class="sxs-lookup"><span data-stu-id="3a548-200">SignalR takes these steps by default, you do not need to take any action in your code.</span></span>

- <span data-ttu-id="3a548-201">**禁用跨域请求** SignalR 禁用跨域请求，以防止用户从外部域调用 SignalR 终结点。</span><span class="sxs-lookup"><span data-stu-id="3a548-201">**Disable cross domain requests** SignalR disables cross domain requests to prevent users from calling a SignalR endpoint from an external domain.</span></span> <span data-ttu-id="3a548-202">SignalR 将来自外部域的任何请求都视为无效，并阻止请求。</span><span class="sxs-lookup"><span data-stu-id="3a548-202">SignalR considers any request from an external domain to be invalid and blocks the request.</span></span> <span data-ttu-id="3a548-203">建议保留此默认行为;否则，恶意站点可能会诱使用户将命令发送到您的站点。</span><span class="sxs-lookup"><span data-stu-id="3a548-203">We recommend that you keep this default behavior; otherwise, a malicious site could trick users into sending commands to your site.</span></span> <span data-ttu-id="3a548-204">如果需要使用跨域请求，请参阅     [如何建立跨域连接](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain) 。</span><span class="sxs-lookup"><span data-stu-id="3a548-204">If you need to use cross domain requests, see     [How to establish a cross-domain connection](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain) .</span></span>
- <span data-ttu-id="3a548-205">**在查询字符串中传递连接标记，而不是 cookie** SignalR 将连接令牌作为查询字符串值（而不是 cookie）传递。</span><span class="sxs-lookup"><span data-stu-id="3a548-205">**Pass connection token in query string, not cookie** SignalR passes the connection token as a query string value, instead of as a cookie.</span></span> <span data-ttu-id="3a548-206">将连接令牌存储在 cookie 中是不安全的，因为浏览器在遇到恶意代码时可能会无意中转发连接令牌。</span><span class="sxs-lookup"><span data-stu-id="3a548-206">Storing the connection token in a cookie is unsafe because the browser can inadvertently forward the connection token when malicious code is encountered.</span></span> <span data-ttu-id="3a548-207">此外，在查询字符串中传递连接令牌可防止连接令牌在当前连接之外保留。</span><span class="sxs-lookup"><span data-stu-id="3a548-207">Also, passing the connection token in the query string prevents the connection token from persisting beyond the current connection.</span></span> <span data-ttu-id="3a548-208">因此，恶意用户无法使用其他用户的身份验证凭据发出请求。</span><span class="sxs-lookup"><span data-stu-id="3a548-208">Therefore, a malicious user cannot make a request under another user's authentication credentials.</span></span>
- <span data-ttu-id="3a548-209">**验证连接令牌** 如 "     [连接令牌](#connectiontoken) " 部分中所述，服务器知道哪个连接 id 与每个经过身份验证的用户相关联。</span><span class="sxs-lookup"><span data-stu-id="3a548-209">**Verify connection token** As described in the     [Connection token](#connectiontoken) section, the server knows which connection id is associated with each authenticated user.</span></span> <span data-ttu-id="3a548-210">服务器不处理来自连接 id 的任何不匹配用户名的请求。</span><span class="sxs-lookup"><span data-stu-id="3a548-210">The server does not process any request from a connection id that does not match the user name.</span></span> <span data-ttu-id="3a548-211">恶意用户可能猜不到有效的请求，因为恶意用户必须知道用户名和当前随机生成的连接 id。连接结束后，该连接 id 就会变得无效。</span><span class="sxs-lookup"><span data-stu-id="3a548-211">It is unlikely a malicious user could guess a valid request because the malicious user would have to know the user name and the current randomly-generated connection id. That connection id becomes invalid as soon as the connection is ended.</span></span> <span data-ttu-id="3a548-212">匿名用户无权访问任何敏感信息。</span><span class="sxs-lookup"><span data-stu-id="3a548-212">Anonymous users should not have access to any sensitive information.</span></span>

<a id="recommendations"></a>

## <a name="signalr-security-recommendations"></a><span data-ttu-id="3a548-213">SignalR 安全建议</span><span class="sxs-lookup"><span data-stu-id="3a548-213">SignalR Security Recommendations</span></span>

<a id="ssl"></a>

### <a name="secure-socket-layers-ssl-protocol"></a><span data-ttu-id="3a548-214"> (SSL) 协议的安全套接字层</span><span class="sxs-lookup"><span data-stu-id="3a548-214">Secure Socket Layers (SSL) protocol</span></span>

<span data-ttu-id="3a548-215">SSL 协议使用加密来保护客户端和服务器之间的数据传输。</span><span class="sxs-lookup"><span data-stu-id="3a548-215">The SSL protocol uses encryption to secure the transport of data between a client and server.</span></span> <span data-ttu-id="3a548-216">如果 SignalR 应用程序在客户端和服务器之间传输敏感信息，请使用 SSL 进行传输。</span><span class="sxs-lookup"><span data-stu-id="3a548-216">If your SignalR application transmits sensitive information between the client and server, use SSL for the transport.</span></span> <span data-ttu-id="3a548-217">有关设置 SSL 的详细信息，请参阅 [如何在 IIS 7 上设置 ssl](https://www.iis.net/learn/manage/configuring-security/how-to-set-up-ssl-on-iis)。</span><span class="sxs-lookup"><span data-stu-id="3a548-217">For more information about setting up SSL, see [How to set up SSL on IIS 7](https://www.iis.net/learn/manage/configuring-security/how-to-set-up-ssl-on-iis).</span></span>

<a id="groupsecurity"></a>

### <a name="do-not-use-groups-as-a-security-mechanism"></a><span data-ttu-id="3a548-218">不要将组用作安全机制</span><span class="sxs-lookup"><span data-stu-id="3a548-218">Do not use groups as a security mechanism</span></span>

<span data-ttu-id="3a548-219">组是一种收集相关用户的便捷方法，但它们并不是一种安全机制，用于限制对敏感信息的访问。</span><span class="sxs-lookup"><span data-stu-id="3a548-219">Groups are a convenient way of collecting related users, but they are not a secure mechanism for limiting access to sensitive information.</span></span> <span data-ttu-id="3a548-220">当用户可以在重新连接期间自动重新加入组时，尤其如此。</span><span class="sxs-lookup"><span data-stu-id="3a548-220">This is especially true when users can automatically rejoin groups during a reconnect.</span></span> <span data-ttu-id="3a548-221">请考虑将特权用户添加到角色，并将对集线器方法的访问仅限制为该角色的成员。</span><span class="sxs-lookup"><span data-stu-id="3a548-221">Instead, consider adding privileged users to a role and limiting access to a hub method to only members of that role.</span></span> <span data-ttu-id="3a548-222">有关基于角色限制访问的示例，请参阅 [SignalR hub 的身份验证和授权](hub-authorization.md)。</span><span class="sxs-lookup"><span data-stu-id="3a548-222">For an example of restricting access based on a role, see [Authentication and Authorization for SignalR Hubs](hub-authorization.md).</span></span> <span data-ttu-id="3a548-223">有关在重新连接时检查用户对组的访问的示例，请参阅使用 [组](../guide-to-the-api/working-with-groups.md)。</span><span class="sxs-lookup"><span data-stu-id="3a548-223">For an example of checking user access to groups when reconnecting, see [Working with groups](../guide-to-the-api/working-with-groups.md).</span></span>

<a id="input"></a>

### <a name="safely-handling-input-from-clients"></a><span data-ttu-id="3a548-224">安全处理来自客户端的输入</span><span class="sxs-lookup"><span data-stu-id="3a548-224">Safely handling input from clients</span></span>

<span data-ttu-id="3a548-225">若要确保恶意用户不向其他用户发送脚本，你必须对要广播到其他客户端的客户端的所有输入进行编码。</span><span class="sxs-lookup"><span data-stu-id="3a548-225">To ensure that a malicious user does not send script to other users, you must encode all input from clients that is intended for broadcast to other clients.</span></span> <span data-ttu-id="3a548-226">你应对接收客户端而不是服务器上的消息进行编码，因为你的 SignalR 应用程序可能有许多不同类型的客户端。</span><span class="sxs-lookup"><span data-stu-id="3a548-226">You should encode messages on the receiving clients rather than the server, because your SignalR application may have many different types of clients.</span></span> <span data-ttu-id="3a548-227">因此，HTML 编码适用于 web 客户端，但不适用于其他类型的客户端。</span><span class="sxs-lookup"><span data-stu-id="3a548-227">Therefore, HTML-encoding works for a web client, but not for other types of clients.</span></span> <span data-ttu-id="3a548-228">例如，用于显示聊天消息的 web 客户端方法可以通过调用函数安全地处理用户名和消息 `html()` 。</span><span class="sxs-lookup"><span data-stu-id="3a548-228">For example, a web client method to display a chat message would safely handle the user name and message by calling the `html()` function.</span></span>

[!code-html[Main](introduction-to-security/samples/sample2.html?highlight=3-4)]

<a id="reconcile"></a>

### <a name="reconciling-a-change-in-user-status-with-an-active-connection"></a><span data-ttu-id="3a548-229">协调用户状态更改与活动连接</span><span class="sxs-lookup"><span data-stu-id="3a548-229">Reconciling a change in user status with an active connection</span></span>

<span data-ttu-id="3a548-230">如果用户的身份验证状态在存在活动连接时发生更改，则用户将收到一条错误消息，指出 "在 active SignalR 连接期间，用户标识无法更改"。</span><span class="sxs-lookup"><span data-stu-id="3a548-230">If a user's authentication status changes while an active connection exists, the user will receive an error that states, "The user identity cannot change during an active SignalR connection."</span></span> <span data-ttu-id="3a548-231">在这种情况下，应用程序应该重新连接到服务器，确保连接 id 和用户名是协调的。</span><span class="sxs-lookup"><span data-stu-id="3a548-231">In that case, your application should re-connect to the server to make sure the connection id and username are coordinated.</span></span> <span data-ttu-id="3a548-232">例如，如果你的应用程序允许用户在有活动连接的情况下注销，则连接的用户名将不再与为下一个请求传入的名称匹配。</span><span class="sxs-lookup"><span data-stu-id="3a548-232">For example, if your application allows the user to log out while an active connection exists, the username for the connection will no longer match the name that is passed in for the next request.</span></span> <span data-ttu-id="3a548-233">你需要在用户注销之前停止连接，然后重新启动。</span><span class="sxs-lookup"><span data-stu-id="3a548-233">You will want to stop the connection before the user logs out, and then restart it.</span></span>

<span data-ttu-id="3a548-234">但是，请务必注意，大多数应用程序不需要手动停止并启动连接。</span><span class="sxs-lookup"><span data-stu-id="3a548-234">However, it is important to note that most applications will not need to manually stop and start the connection.</span></span> <span data-ttu-id="3a548-235">如果你的应用程序在注销后将用户重定向到单独的页（例如 Web 窗体应用程序或 MVC 应用程序中的默认行为），或在注销后刷新当前页，则活动连接将自动断开连接，并且无需任何其他操作。</span><span class="sxs-lookup"><span data-stu-id="3a548-235">If your application redirects users to a separate page after logging out, such as the default behavior in a Web Forms application or MVC application, or refreshes the current page after logging out, the active connection is automatically disconnected and does not require any additional action.</span></span>

<span data-ttu-id="3a548-236">下面的示例演示如何在用户状态发生更改时停止和启动连接。</span><span class="sxs-lookup"><span data-stu-id="3a548-236">The following example shows how to stop and start a connection when the user status has changed.</span></span>

[!code-html[Main](introduction-to-security/samples/sample3.html)]

<span data-ttu-id="3a548-237">或者，如果你的站点使用窗体身份验证的可调过期，并且没有任何活动来使身份验证 cookie 有效，则用户的身份验证状态可能会发生更改。</span><span class="sxs-lookup"><span data-stu-id="3a548-237">Or, the user's authentication status may change if your site uses sliding expiration with Forms Authentication, and there is no activity to keep the authentication cookie valid.</span></span> <span data-ttu-id="3a548-238">在这种情况下，用户将被注销，用户名将不再与连接令牌中的用户名匹配。</span><span class="sxs-lookup"><span data-stu-id="3a548-238">In that case, the user will be logged out and the user name will no longer match the user name in the connection token.</span></span> <span data-ttu-id="3a548-239">通过添加一些定期请求 web 服务器上的资源以使身份验证 cookie 有效的脚本，可以解决此问题。</span><span class="sxs-lookup"><span data-stu-id="3a548-239">You can fix this problem by adding some script that periodically requests a resource on the web server to keep the authentication cookie valid.</span></span> <span data-ttu-id="3a548-240">下面的示例演示如何每隔30分钟请求一次资源。</span><span class="sxs-lookup"><span data-stu-id="3a548-240">The following example shows how to request a resource every 30 minutes.</span></span>

[!code-javascript[Main](introduction-to-security/samples/sample4.js)]

<a id="autogen"></a>

### <a name="automatically-generated-javascript-proxy-files"></a><span data-ttu-id="3a548-241">自动生成的 JavaScript 代理文件</span><span class="sxs-lookup"><span data-stu-id="3a548-241">Automatically generated JavaScript proxy files</span></span>

<span data-ttu-id="3a548-242">如果你不想在每个用户的 JavaScript 代理文件中包含所有的中心和方法，则可以禁用文件的自动生成。</span><span class="sxs-lookup"><span data-stu-id="3a548-242">If you do not want to include all of the hubs and methods in the JavaScript proxy file for each user, you can disable the automatic generation of the file.</span></span> <span data-ttu-id="3a548-243">如果有多个中心和方法，但不希望每个用户都知道所有方法，则可以选择此选项。</span><span class="sxs-lookup"><span data-stu-id="3a548-243">You might choose this option if you have multiple hubs and methods, but do not want every user to be aware of all of the methods.</span></span> <span data-ttu-id="3a548-244">可以通过将 **EnableJavaScriptProxies** 设置为 **false**来禁用自动生成。</span><span class="sxs-lookup"><span data-stu-id="3a548-244">You disable automatic generation by setting **EnableJavaScriptProxies** to **false**.</span></span>

[!code-csharp[Main](introduction-to-security/samples/sample5.cs)]

<span data-ttu-id="3a548-245">有关 JavaScript 代理文件的详细信息，请参阅 [生成的代理及其功能](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy)。</span><span class="sxs-lookup"><span data-stu-id="3a548-245">For more information about the JavaScript proxy files, see [The generated proxy and what it does for you](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy).</span></span> <a id="exceptions"></a>

### <a name="exceptions"></a><span data-ttu-id="3a548-246">例外</span><span class="sxs-lookup"><span data-stu-id="3a548-246">Exceptions</span></span>

<span data-ttu-id="3a548-247">应避免向客户端传递异常对象，因为这些对象可能会向客户端公开敏感信息。</span><span class="sxs-lookup"><span data-stu-id="3a548-247">You should avoid passing exception objects to clients because the objects may expose sensitive information to the clients.</span></span> <span data-ttu-id="3a548-248">请改为在客户端上调用显示相关错误消息的方法。</span><span class="sxs-lookup"><span data-stu-id="3a548-248">Instead, call a method on the client that displays the relevant error message.</span></span>

[!code-csharp[Main](introduction-to-security/samples/sample6.cs)]

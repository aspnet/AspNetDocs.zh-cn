---
uid: web-api/overview/security/individual-accounts-in-web-api
title: 使用个人帐户和本地登录名保护 Web API ASP.NET Web API 2.2 |Microsoft Docs
author: MikeWasson
description: 本主题演示如何使用 OAuth2 对成员资格数据库进行身份验证的 web API 的安全。 教程中使用的软件版本 Visual Studio 201 。
ms.author: riande
ms.date: 10/15/2014
ms.assetid: 92c84846-f0ea-4b5e-94b6-5004874eb060
msc.legacyurl: /web-api/overview/security/individual-accounts-in-web-api
msc.type: authoredcontent
ms.openlocfilehash: 7492c4aa4c2a0a8aeed64c3462bda8fc51f35a6b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78447176"
---
# <a name="secure-a-web-api-with-individual-accounts-and-local-login-in-aspnet-web-api-22"></a><span data-ttu-id="fcc5f-104">在 ASP.NET Web API 2.2 中使用个人帐户和本地登录保护 Web API</span><span class="sxs-lookup"><span data-stu-id="fcc5f-104">Secure a Web API with Individual Accounts and Local Login in ASP.NET Web API 2.2</span></span>

<span data-ttu-id="fcc5f-105">作者： [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="fcc5f-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="fcc5f-106">下载示例应用</span><span class="sxs-lookup"><span data-stu-id="fcc5f-106">Download Sample App</span></span>](https://github.com/MikeWasson/LocalAccountsApp)

> <span data-ttu-id="fcc5f-107">本主题演示如何使用 OAuth2 对成员资格数据库进行身份验证的 web API 的安全。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-107">This topic shows how to secure a web API using OAuth2 to authenticate against a membership database.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="fcc5f-108">本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="fcc5f-108">Software versions used in the tutorial</span></span>
> 
> 
> - [<span data-ttu-id="fcc5f-109">Visual Studio 2013 Update 3</span><span class="sxs-lookup"><span data-stu-id="fcc5f-109">Visual Studio 2013 Update 3</span></span>](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - [<span data-ttu-id="fcc5f-110">Web API 2。2</span><span class="sxs-lookup"><span data-stu-id="fcc5f-110">Web API 2.2</span></span>](../releases/whats-new-in-aspnet-web-api-22.md)
> - [<span data-ttu-id="fcc5f-111">ASP.NET Identity 2。1</span><span class="sxs-lookup"><span data-stu-id="fcc5f-111">ASP.NET Identity 2.1</span></span>](../../../identity/index.md)

<span data-ttu-id="fcc5f-112">在 Visual Studio 2013 中，Web API 项目模板提供了三个身份验证选项：</span><span class="sxs-lookup"><span data-stu-id="fcc5f-112">In Visual Studio 2013, the Web API project template gives you three options for authentication:</span></span>

- <span data-ttu-id="fcc5f-113">**个人帐户。**</span><span class="sxs-lookup"><span data-stu-id="fcc5f-113">**Individual accounts.**</span></span> <span data-ttu-id="fcc5f-114">应用使用成员资格数据库。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-114">The app uses a membership database.</span></span>
- <span data-ttu-id="fcc5f-115">**组织帐户。**</span><span class="sxs-lookup"><span data-stu-id="fcc5f-115">**Organizational accounts.**</span></span> <span data-ttu-id="fcc5f-116">用户通过其 Azure Active Directory、Office 365 或本地 Active Directory 凭据进行登录。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-116">Users sign in with their Azure Active Directory, Office 365, or on-premise Active Directory credentials.</span></span>
- <span data-ttu-id="fcc5f-117">**Windows 身份验证。**</span><span class="sxs-lookup"><span data-stu-id="fcc5f-117">**Windows authentication.**</span></span> <span data-ttu-id="fcc5f-118">此选项适用于 Intranet 应用程序，并使用 Windows 身份验证 IIS 模块。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-118">This option is intended for Intranet applications, and uses the Windows Authentication IIS module.</span></span>

<span data-ttu-id="fcc5f-119">有关这些选项的更多详细信息，请参阅[在 Visual Studio 2013 中创建 ASP.NET Web 项目](../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#auth)。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-119">For more details about these options, see [Creating ASP.NET Web Projects in Visual Studio 2013](../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#auth).</span></span>

<span data-ttu-id="fcc5f-120">单个帐户为用户提供了两种登录方式：</span><span class="sxs-lookup"><span data-stu-id="fcc5f-120">Individual accounts provide two ways for a user to log in:</span></span>

- <span data-ttu-id="fcc5f-121">**本地登录名**。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-121">**Local login**.</span></span> <span data-ttu-id="fcc5f-122">用户在站点上注册，并输入用户名和密码。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-122">The user registers at the site, entering a username and password.</span></span> <span data-ttu-id="fcc5f-123">此应用将密码哈希存储在成员资格数据库中。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-123">The app stores the password hash in the membership database.</span></span> <span data-ttu-id="fcc5f-124">当用户登录时，ASP.NET Identity 系统会验证密码。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-124">When the user logs in, the ASP.NET Identity system verifies the password.</span></span>
- <span data-ttu-id="fcc5f-125">**社交登录**。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-125">**Social login**.</span></span> <span data-ttu-id="fcc5f-126">用户使用外部服务（如 Facebook、Microsoft 或 Google）登录。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-126">The user signs in with an external service, such as Facebook, Microsoft, or Google.</span></span> <span data-ttu-id="fcc5f-127">应用仍会在成员资格数据库中为用户创建一个条目，但不会存储任何凭据。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-127">The app still creates an entry for the user in the membership database, but does not store any credentials.</span></span> <span data-ttu-id="fcc5f-128">用户通过登录到外部服务进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-128">The user authenticates by signing into the external service.</span></span>

<span data-ttu-id="fcc5f-129">本文介绍本地登录方案。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-129">This article looks at the local login scenario.</span></span> <span data-ttu-id="fcc5f-130">对于本地和社交登录，Web API 都使用 OAuth2 来对请求进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-130">For both local and social login, Web API uses OAuth2 to authenticate requests.</span></span> <span data-ttu-id="fcc5f-131">但对于本地和社交登录，凭据流是不同的。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-131">However, the credential flows are different for local and social login.</span></span>

<span data-ttu-id="fcc5f-132">在本文中，我将演示一个简单的应用程序，该应用程序允许用户登录并将经过身份验证的 AJAX 调用发送到 web API。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-132">In this article, I'll demonstrate a simple app that lets the user log in and send authenticated AJAX calls to a web API.</span></span> <span data-ttu-id="fcc5f-133">你可以在[此处](https://github.com/MikeWasson/LocalAccountsApp)下载代码示例。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-133">You can download the sample code [here](https://github.com/MikeWasson/LocalAccountsApp).</span></span> <span data-ttu-id="fcc5f-134">该自述文件介绍了如何在 Visual Studio 中从头开始创建示例。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-134">The readme describes how to create the sample from scratch in Visual Studio.</span></span>

[![](individual-accounts-in-web-api/_static/image2.png)](individual-accounts-in-web-api/_static/image1.png)

<span data-ttu-id="fcc5f-135">示例应用使用挖空的数据绑定和 jQuery 来发送 AJAX 请求。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-135">The sample app uses Knockout.js for data-binding and jQuery for sending AJAX requests.</span></span> <span data-ttu-id="fcc5f-136">我将重点介绍 AJAX 调用，因此，您不需要了解本文的挖空。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-136">I'll be focusing on the AJAX calls, so you don't need to know Knockout.js for this article.</span></span>

<span data-ttu-id="fcc5f-137">在此过程中，我将介绍：</span><span class="sxs-lookup"><span data-stu-id="fcc5f-137">Along the way, I'll describe:</span></span>

- <span data-ttu-id="fcc5f-138">应用在客户端执行的操作。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-138">What the app is doing on the client side.</span></span>
- <span data-ttu-id="fcc5f-139">服务器上发生了什么情况。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-139">What's happening on the server.</span></span>
- <span data-ttu-id="fcc5f-140">中间的 HTTP 流量。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-140">The HTTP traffic in the middle.</span></span>

<span data-ttu-id="fcc5f-141">首先，我们需要定义一些 OAuth2 术语。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-141">First, we need to define some OAuth2 terminology.</span></span>

- <span data-ttu-id="fcc5f-142">*资源*。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-142">*Resource*.</span></span> <span data-ttu-id="fcc5f-143">可以保护的某些数据片段。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-143">Some piece of data that can be protected.</span></span>
- <span data-ttu-id="fcc5f-144">*资源服务器*。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-144">*Resource server*.</span></span> <span data-ttu-id="fcc5f-145">承载资源的服务器。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-145">The server that hosts the resource.</span></span>
- <span data-ttu-id="fcc5f-146">*资源所有者*。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-146">*Resource owner*.</span></span> <span data-ttu-id="fcc5f-147">可授予对资源的访问权限的实体。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-147">The entity that can grant permission to access a resource.</span></span> <span data-ttu-id="fcc5f-148">（通常为用户。）</span><span class="sxs-lookup"><span data-stu-id="fcc5f-148">(Typically the user.)</span></span>
- <span data-ttu-id="fcc5f-149">*Client*：要访问资源的应用。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-149">*Client*: The app that wants access to the resource.</span></span> <span data-ttu-id="fcc5f-150">在本文中，客户端是一个 web 浏览器。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-150">In this article, the client is a web browser.</span></span>
- <span data-ttu-id="fcc5f-151">*访问令牌*。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-151">*Access token*.</span></span> <span data-ttu-id="fcc5f-152">用于授予对资源的访问权限的令牌。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-152">A token that grants access to a resource.</span></span>
- <span data-ttu-id="fcc5f-153">*持有者令牌*。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-153">*Bearer token*.</span></span> <span data-ttu-id="fcc5f-154">特定类型的访问令牌，其中包含任何人都可以使用令牌的属性。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-154">A particular type of access token, with the property that anyone can use the token.</span></span> <span data-ttu-id="fcc5f-155">换句话说，客户端不需要加密密钥或其他机密即可使用持有者令牌。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-155">In other words, a client doesn't need a cryptographic key or other secret to use a bearer token.</span></span> <span data-ttu-id="fcc5f-156">出于此原因，持有者令牌只应在 HTTPS 上使用，并且应具有相对较短的过期时间。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-156">For that reason, bearer tokens should only be used over a HTTPS, and should have relatively short expiration times.</span></span>
- <span data-ttu-id="fcc5f-157">*授权服务器*。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-157">*Authorization server*.</span></span> <span data-ttu-id="fcc5f-158">提供访问令牌的服务器。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-158">A server that gives out access tokens.</span></span>

<span data-ttu-id="fcc5f-159">应用程序可以同时充当授权服务器和资源服务器。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-159">An application can act as both authorization server and resource server.</span></span> <span data-ttu-id="fcc5f-160">Web API 项目模板遵循此模式。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-160">The Web API project template follows this pattern.</span></span>

## <a name="local-login-credential-flow"></a><span data-ttu-id="fcc5f-161">本地登录凭据流</span><span class="sxs-lookup"><span data-stu-id="fcc5f-161">Local Login Credential Flow</span></span>

<span data-ttu-id="fcc5f-162">对于本地登录，Web API 使用 OAuth2 中定义的[资源所有者密码流](http://oauthlib.readthedocs.org/en/latest/oauth2/grants/password.html)。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-162">For local login, Web API uses the [resource owner password flow](http://oauthlib.readthedocs.org/en/latest/oauth2/grants/password.html) defined in OAuth2.</span></span>

1. <span data-ttu-id="fcc5f-163">用户在客户端中输入名称和密码。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-163">The user enters a name and password into the client.</span></span>
2. <span data-ttu-id="fcc5f-164">客户端会将这些凭据发送到授权服务器。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-164">The client sends these credentials to the authorization server.</span></span>
3. <span data-ttu-id="fcc5f-165">授权服务器对凭据进行身份验证并返回一个访问令牌。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-165">The authorization server authenticates the credentials and returns an access token.</span></span>
4. <span data-ttu-id="fcc5f-166">若要访问受保护的资源，客户端在 HTTP 请求的授权标头中包含访问令牌。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-166">To access a protected resource, the client includes the access token in the Authorization header of the HTTP request.</span></span>

![](individual-accounts-in-web-api/_static/image3.png)

<span data-ttu-id="fcc5f-167">当你在 Web API 项目模板中选择**单个帐户**时，该项目将包括验证用户凭据和颁发令牌的授权服务器。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-167">When you select **Individual accounts** in the Web API project template, the project includes an authorization server that validates user credentials and issues tokens.</span></span> <span data-ttu-id="fcc5f-168">下图显示了 Web API 组件方面的相同凭据流。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-168">The following diagram shows the same credential flow in terms of Web API components.</span></span>

![](individual-accounts-in-web-api/_static/image4.png)

<span data-ttu-id="fcc5f-169">在这种情况下，Web API 控制器充当资源服务器。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-169">In this scenario, Web API controllers act as resource servers.</span></span> <span data-ttu-id="fcc5f-170">身份验证筛选器验证访问令牌，而 **[授权]** 属性用于保护资源。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-170">An authentication filter validates access tokens, and the **[Authorize]** attribute is used to protect a resource.</span></span> <span data-ttu-id="fcc5f-171">当控制器或操作具有 " **[授权]** " 属性时，对该控制器或操作的所有请求都必须经过身份验证。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-171">When a controller or action has the **[Authorize]** attribute, all requests to that controller or action must be authenticated.</span></span> <span data-ttu-id="fcc5f-172">否则，将拒绝授权，并且 Web API 将返回401（未授权）错误。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-172">Otherwise, authorization is denied, and Web API returns a 401 (Unauthorized) error.</span></span>

<span data-ttu-id="fcc5f-173">授权服务器和身份验证筛选器都调用[OWIN 中间件](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)组件来处理 OAuth2 的详细信息。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-173">The authorization server and the authentication filter both call into an [OWIN middleware](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) component that handles the details of OAuth2.</span></span> <span data-ttu-id="fcc5f-174">在本教程的后面部分，我将更详细地介绍设计。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-174">I'll describe the design in more detail later in this tutorial.</span></span>

## <a name="sending-an-unauthorized-request"></a><span data-ttu-id="fcc5f-175">发送未经授权的请求</span><span class="sxs-lookup"><span data-stu-id="fcc5f-175">Sending an Unauthorized Request</span></span>

<span data-ttu-id="fcc5f-176">若要开始，请运行应用，并单击 "**调用 API** " 按钮。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-176">To get started, run the app and click the **Call API** button.</span></span> <span data-ttu-id="fcc5f-177">请求完成后，"**结果**" 框中会显示一条错误消息。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-177">When the request completes, you should see an error message in the **Result** box.</span></span> <span data-ttu-id="fcc5f-178">这是因为请求不包含访问令牌，因此请求未经授权。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-178">That's because the request does not contain an access token, so the request is unauthorized.</span></span>

[![](individual-accounts-in-web-api/_static/image6.png)](individual-accounts-in-web-api/_static/image5.png)

<span data-ttu-id="fcc5f-179">"**调用 API** " 按钮将 AJAX 请求发送到 ~/api/values，后者调用 Web API 控制器操作。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-179">The **Call API** button sends an AJAX request to ~/api/values, which invokes a Web API controller action.</span></span> <span data-ttu-id="fcc5f-180">下面是发送 AJAX 请求的 JavaScript 代码部分。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-180">Here is the section of JavaScript code that sends the AJAX request.</span></span> <span data-ttu-id="fcc5f-181">在示例应用中，所有 JavaScript 应用代码位于 Scripts\app.js 文件中。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-181">In the sample app, all of the JavaScript app code is located in the Scripts\app.js file.</span></span>

[!code-javascript[Main](individual-accounts-in-web-api/samples/sample1.js)]

<span data-ttu-id="fcc5f-182">在用户登录之前，没有持有者令牌，因此请求中没有任何授权标头。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-182">Until the user logs in, there is no bearer token, and therefore no Authorization header in the request.</span></span> <span data-ttu-id="fcc5f-183">这将导致请求返回401错误。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-183">This causes the request to return a 401 error.</span></span>

<span data-ttu-id="fcc5f-184">下面是 HTTP 请求。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-184">Here is the HTTP request.</span></span> <span data-ttu-id="fcc5f-185">（我使用[Fiddler](http://www.telerik.com/fiddler)捕获 HTTP 流量。）</span><span class="sxs-lookup"><span data-stu-id="fcc5f-185">(I used [Fiddler](http://www.telerik.com/fiddler) to capture the HTTP traffic.)</span></span>

[!code-console[Main](individual-accounts-in-web-api/samples/sample2.cmd)]

<span data-ttu-id="fcc5f-186">HTTP 响应：</span><span class="sxs-lookup"><span data-stu-id="fcc5f-186">HTTP response:</span></span>

[!code-console[Main](individual-accounts-in-web-api/samples/sample3.cmd?highlight=1,4)]

<span data-ttu-id="fcc5f-187">请注意，响应包含一个 Www 验证标头，其质询设置为 "持有者"。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-187">Notice that the response includes a Www-Authenticate header with the challenge set to Bearer.</span></span> <span data-ttu-id="fcc5f-188">指示服务器需要持有者令牌的。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-188">That indicates the server expects a bearer token.</span></span>

## <a name="register-a-user"></a><span data-ttu-id="fcc5f-189">注册用户</span><span class="sxs-lookup"><span data-stu-id="fcc5f-189">Register a User</span></span>

<span data-ttu-id="fcc5f-190">在应用的 "**注册**" 部分中，输入电子邮件和密码，然后单击 "**注册**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-190">In the **Register** section of the app, enter an email and password, and click the **Register** button.</span></span>

<span data-ttu-id="fcc5f-191">对于本示例，无需使用有效的电子邮件地址，但真正的应用会确认该地址。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-191">You don't need to use a valid email address for this sample, but a real app would confirm the address.</span></span> <span data-ttu-id="fcc5f-192">（请参阅[创建具有登录、电子邮件确认和密码重置的安全 ASP.NET MVC 5 web 应用](../../../mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md)。）对于密码，请使用类似于 "Password1！" 的内容，其中包含大写字母、小写字母、数字和非字母数字字符。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-192">(See [Create a secure ASP.NET MVC 5 web app with log in, email confirmation and password reset](../../../mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md).) For the password, use something like "Password1!", with an upper case letter, lower case letter, number, and non-alpha-numeric character.</span></span> <span data-ttu-id="fcc5f-193">为了使应用程序保持简单，我省略了客户端验证，因此，如果密码格式有问题，会收到400（错误请求）错误。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-193">To keep the app simple, I left out client-side validation, so if there is a problem with the password format, you'll get a 400 (Bad Request) error.</span></span>

[![](individual-accounts-in-web-api/_static/image8.png)](individual-accounts-in-web-api/_static/image7.png)

<span data-ttu-id="fcc5f-194">"**注册**" 按钮将 POST 请求发送到 ~/api/Account/Register/。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-194">The **Register** button sends a POST request to ~/api/Account/Register/.</span></span> <span data-ttu-id="fcc5f-195">请求正文是一个包含用户名和密码的 JSON 对象。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-195">The request body is a JSON object that holds the name and password.</span></span> <span data-ttu-id="fcc5f-196">下面是发送请求的 JavaScript 代码：</span><span class="sxs-lookup"><span data-stu-id="fcc5f-196">Here is the JavaScript code that sends the request:</span></span>

[!code-javascript[Main](individual-accounts-in-web-api/samples/sample4.js)]

<span data-ttu-id="fcc5f-197">HTTP 请求：</span><span class="sxs-lookup"><span data-stu-id="fcc5f-197">HTTP request:</span></span>

[!code-console[Main](individual-accounts-in-web-api/samples/sample5.cmd?highlight=5,10)]

<span data-ttu-id="fcc5f-198">HTTP 响应：</span><span class="sxs-lookup"><span data-stu-id="fcc5f-198">HTTP response:</span></span>

[!code-console[Main](individual-accounts-in-web-api/samples/sample6.cmd)]

<span data-ttu-id="fcc5f-199">此请求由 `AccountController` 类处理。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-199">This request is handled by the `AccountController` class.</span></span> <span data-ttu-id="fcc5f-200">在内部，`AccountController` 使用 ASP.NET Identity 来管理成员资格数据库。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-200">Internally, `AccountController` uses ASP.NET Identity to manage the membership database.</span></span>

<span data-ttu-id="fcc5f-201">如果从 Visual Studio 本地运行应用，用户帐户将存储在 LocalDB 中的 AspNetUsers 表中。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-201">If you run the app locally from Visual Studio, user accounts are stored in LocalDB, in the AspNetUsers table.</span></span> <span data-ttu-id="fcc5f-202">若要在 Visual Studio 中查看表，请单击 "**视图**" 菜单，选择 "**服务器资源管理器**"，然后展开 "**数据连接**"。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-202">To view the tables in Visual Studio, click the **View** menu, select **Server Explorer**, then expand **Data Connections**.</span></span>

![](individual-accounts-in-web-api/_static/image9.png)

## <a name="get-an-access-token"></a><span data-ttu-id="fcc5f-203">获取访问令牌</span><span class="sxs-lookup"><span data-stu-id="fcc5f-203">Get an Access Token</span></span>

<span data-ttu-id="fcc5f-204">到目前为止，我们尚未执行任何 OAuth，但现在我们会在请求访问令牌时，在操作中看到 OAuth 授权服务器。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-204">So far we have not done any OAuth, but now we'll see the OAuth authorization server in action, when we request an access token.</span></span> <span data-ttu-id="fcc5f-205">在示例应用程序的 "**登录**" 区域中，输入电子邮件和密码，并单击 "**登录**"。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-205">In the **Log In** area of the sample app, enter the email and password and click **Log In**.</span></span>

[![](individual-accounts-in-web-api/_static/image11.png)](individual-accounts-in-web-api/_static/image10.png)

<span data-ttu-id="fcc5f-206">"**登录**" 按钮向令牌终结点发送请求。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-206">The **Log In** button sends a request to the token endpoint.</span></span> <span data-ttu-id="fcc5f-207">请求正文包含以下形式的 url 编码数据：</span><span class="sxs-lookup"><span data-stu-id="fcc5f-207">The body of the request contains the following form-url-encoded data:</span></span>

- <span data-ttu-id="fcc5f-208">授予\_类型： "密码"</span><span class="sxs-lookup"><span data-stu-id="fcc5f-208">grant\_type: "password"</span></span>
- <span data-ttu-id="fcc5f-209">username： &lt;用户的电子邮件&gt;</span><span class="sxs-lookup"><span data-stu-id="fcc5f-209">username: &lt;the user's email&gt;</span></span>
- <span data-ttu-id="fcc5f-210">密码： &lt;密码&gt;</span><span class="sxs-lookup"><span data-stu-id="fcc5f-210">password: &lt;password&gt;</span></span>

<span data-ttu-id="fcc5f-211">下面是发送 AJAX 请求的 JavaScript 代码：</span><span class="sxs-lookup"><span data-stu-id="fcc5f-211">Here is the JavaScript code that sends the AJAX request:</span></span>

[!code-javascript[Main](individual-accounts-in-web-api/samples/sample7.js?highlight=14)]

<span data-ttu-id="fcc5f-212">如果请求成功，授权服务器将在响应正文中返回一个访问令牌。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-212">If the request succeeds, the authorization server returns an access token in the response body.</span></span> <span data-ttu-id="fcc5f-213">请注意，我们将标记存储在会话存储中，以便在稍后将请求发送到 API 时使用。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-213">Notice that we store the token in session storage, to use later when sending requests to the API.</span></span> <span data-ttu-id="fcc5f-214">与某些形式的身份验证不同（例如基于 cookie 的身份验证），浏览器不会自动在后续请求中包含访问令牌。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-214">Unlike some forms of authentication (such as cookie-based authentication), the browser will not automatically include the access token in subsequent requests.</span></span> <span data-ttu-id="fcc5f-215">应用程序必须显式执行此操作。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-215">The application must do so explicitly.</span></span> <span data-ttu-id="fcc5f-216">这是一件好事，因为它限制了[CSRF 漏洞](preventing-cross-site-request-forgery-csrf-attacks.md)。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-216">That's a good thing, because it limits [CSRF vulnerabilities](preventing-cross-site-request-forgery-csrf-attacks.md).</span></span>

<span data-ttu-id="fcc5f-217">HTTP 请求：</span><span class="sxs-lookup"><span data-stu-id="fcc5f-217">HTTP request:</span></span>

[!code-console[Main](individual-accounts-in-web-api/samples/sample8.cmd?highlight=5,10)]

<span data-ttu-id="fcc5f-218">你可以看到该请求包含用户的凭据。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-218">You can see that the request contains the user's credentials.</span></span> <span data-ttu-id="fcc5f-219">*必须*使用 HTTPS 来提供传输层安全性。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-219">You *must* use HTTPS to provide transport layer security.</span></span>

<span data-ttu-id="fcc5f-220">HTTP 响应：</span><span class="sxs-lookup"><span data-stu-id="fcc5f-220">HTTP response:</span></span>

[!code-console[Main](individual-accounts-in-web-api/samples/sample9.cmd?highlight=8)]

<span data-ttu-id="fcc5f-221">为方便起见，我缩进了 JSON 并截断了访问令牌，这是一个很长的时间。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-221">For readability, I indented the JSON and truncated the access token, which is a quite long.</span></span>

<span data-ttu-id="fcc5f-222">`access_token`、`token_type`和 `expires_in` 属性由 OAuth2 规范定义。其他属性（`userName`、`.issued`和 `.expires`）只用于提供信息。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-222">The `access_token`, `token_type`, and `expires_in` properties are defined by the OAuth2 spec. The other properties (`userName`, `.issued`, and `.expires`) are just for informational purposes.</span></span> <span data-ttu-id="fcc5f-223">您可以在/Providers/ApplicationOAuthProvider.cs 文件的 `TokenEndpoint` 方法中找到添加这些附加属性的代码。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-223">You can find the code that adds those additional properties in the `TokenEndpoint` method, in the /Providers/ApplicationOAuthProvider.cs file.</span></span>

## <a name="send-an-authenticated-request"></a><span data-ttu-id="fcc5f-224">发送经过身份验证的请求</span><span class="sxs-lookup"><span data-stu-id="fcc5f-224">Send an Authenticated Request</span></span>

<span data-ttu-id="fcc5f-225">现在我们有了持有者令牌，接下来我们可以向 API 发出经过身份验证的请求。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-225">Now that we have a bearer token, we can make an authenticated request to the API.</span></span> <span data-ttu-id="fcc5f-226">这是通过设置请求中的 Authorization 标头来完成的。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-226">This is done by setting the Authorization header in the request.</span></span> <span data-ttu-id="fcc5f-227">再次单击 "**调用 API** " 按钮以查看此。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-227">Click the **Call API** button again to see this.</span></span>

[![](individual-accounts-in-web-api/_static/image13.png)](individual-accounts-in-web-api/_static/image12.png)

<span data-ttu-id="fcc5f-228">HTTP 请求：</span><span class="sxs-lookup"><span data-stu-id="fcc5f-228">HTTP request:</span></span>

[!code-console[Main](individual-accounts-in-web-api/samples/sample10.cmd?highlight=5)]

<span data-ttu-id="fcc5f-229">HTTP 响应：</span><span class="sxs-lookup"><span data-stu-id="fcc5f-229">HTTP response:</span></span>

[!code-console[Main](individual-accounts-in-web-api/samples/sample11.cmd)]

## <a name="log-out"></a><span data-ttu-id="fcc5f-230">注销</span><span class="sxs-lookup"><span data-stu-id="fcc5f-230">Log Out</span></span>

<span data-ttu-id="fcc5f-231">由于浏览器不缓存凭据或访问令牌，因此注销只需从会话存储中删除令牌即可 "忘记密码"：</span><span class="sxs-lookup"><span data-stu-id="fcc5f-231">Because the browser does not cache the credentials or the access token, logging out is simply a matter of "forgetting" the token, by removing it from session storage:</span></span>

[!code-javascript[Main](individual-accounts-in-web-api/samples/sample12.js)]

## <a name="understanding-the-individual-accounts-project-template"></a><span data-ttu-id="fcc5f-232">了解各个帐户的项目模板</span><span class="sxs-lookup"><span data-stu-id="fcc5f-232">Understanding the Individual Accounts Project Template</span></span>

<span data-ttu-id="fcc5f-233">当你在 "ASP.NET Web 应用程序" 项目模板中选择**单个帐户**时，该项目包括：</span><span class="sxs-lookup"><span data-stu-id="fcc5f-233">When you select **Individual Accounts** in the ASP.NET Web Application project template, the project includes:</span></span>

- <span data-ttu-id="fcc5f-234">OAuth2 授权服务器。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-234">An OAuth2 authorization server.</span></span>
- <span data-ttu-id="fcc5f-235">用于管理用户帐户的 Web API 终结点</span><span class="sxs-lookup"><span data-stu-id="fcc5f-235">A Web API endpoint for managing user accounts</span></span>
- <span data-ttu-id="fcc5f-236">用于存储用户帐户的 EF 模型。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-236">An EF model for storing user accounts.</span></span>

<span data-ttu-id="fcc5f-237">下面是实现这些功能的主要应用程序类：</span><span class="sxs-lookup"><span data-stu-id="fcc5f-237">Here are the main application classes that implement these features:</span></span>

- <span data-ttu-id="fcc5f-238">`AccountController`。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-238">`AccountController`.</span></span> <span data-ttu-id="fcc5f-239">提供用于管理用户帐户的 Web API 终结点。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-239">Provides a Web API endpoint for managing user accounts.</span></span> <span data-ttu-id="fcc5f-240">`Register` 操作是本教程中使用的唯一操作。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-240">The `Register` action is the only one that we used in this tutorial.</span></span> <span data-ttu-id="fcc5f-241">类上的其他方法支持重置密码、社交登录和其他功能。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-241">Other methods on the class support password reset, social logins, and other functionality.</span></span>
- <span data-ttu-id="fcc5f-242">`ApplicationUser`，在/Models/IdentityModels.cs. 中定义</span><span class="sxs-lookup"><span data-stu-id="fcc5f-242">`ApplicationUser`, defined in /Models/IdentityModels.cs.</span></span> <span data-ttu-id="fcc5f-243">此类是成员资格数据库中用户帐户的 EF 模型。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-243">This class is the EF model for user accounts in the membership database.</span></span>
- <span data-ttu-id="fcc5f-244">`ApplicationUserManager`，在/App\_Start/IdentityConfig 中定义。 cs 此类派生自[UserManager](https://msdn.microsoft.com/library/dn613290.aspx) ，对用户帐户执行操作，例如创建新用户、验证密码等，并自动保存对数据库所做的更改。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-244">`ApplicationUserManager`, defined in /App\_Start/IdentityConfig.cs This class derives from [UserManager](https://msdn.microsoft.com/library/dn613290.aspx) and performs operations on user accounts, such as creating a new user, verifying passwords, and so forth, and automatically persists changes to the database.</span></span>
- <span data-ttu-id="fcc5f-245">`ApplicationOAuthProvider`。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-245">`ApplicationOAuthProvider`.</span></span> <span data-ttu-id="fcc5f-246">此对象将插入到 OWIN 中间件，并处理中间件所引发的事件。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-246">This object plugs into the OWIN middleware, and processes events raised by the middleware.</span></span> <span data-ttu-id="fcc5f-247">它派生自[OAuthAuthorizationServerProvider](https://msdn.microsoft.com/library/microsoft.owin.security.oauth.oauthauthorizationserverprovider.aspx)。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-247">It derives from [OAuthAuthorizationServerProvider](https://msdn.microsoft.com/library/microsoft.owin.security.oauth.oauthauthorizationserverprovider.aspx).</span></span>

![](individual-accounts-in-web-api/_static/image14.png)

### <a name="configuring-the-authorization-server"></a><span data-ttu-id="fcc5f-248">配置授权服务器</span><span class="sxs-lookup"><span data-stu-id="fcc5f-248">Configuring the Authorization Server</span></span>

<span data-ttu-id="fcc5f-249">在 StartupAuth.cs 中，以下代码将配置 OAuth2 授权服务器。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-249">In StartupAuth.cs, the following code configures the OAuth2 authorization server.</span></span>

[!code-csharp[Main](individual-accounts-in-web-api/samples/sample13.cs)]

<span data-ttu-id="fcc5f-250">`TokenEndpointPath` 属性是授权服务器终结点的 URL 路径。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-250">The `TokenEndpointPath` property is the URL path to the authorization server endpoint.</span></span> <span data-ttu-id="fcc5f-251">这是应用用于获取持有者令牌的 URL。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-251">That's the URL that app uses to get the bearer tokens.</span></span>

<span data-ttu-id="fcc5f-252">`Provider` 属性指定插入到 OWIN 中间件的提供程序，并处理中间件所引发的事件。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-252">The `Provider` property specifies a provider that plugs into the OWIN middleware, and processes events raised by the middleware.</span></span>

<span data-ttu-id="fcc5f-253">下面是应用想要获取令牌时的基本流程：</span><span class="sxs-lookup"><span data-stu-id="fcc5f-253">Here is the basic flow when the app wants to get a token:</span></span>

1. <span data-ttu-id="fcc5f-254">若要获取访问令牌，应用会将请求发送到 ~/Token。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-254">To get an access token, the app sends a request to ~/Token.</span></span>
2. <span data-ttu-id="fcc5f-255">OAuth 中间件调用提供程序 `GrantResourceOwnerCredentials`。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-255">The OAuth middleware calls `GrantResourceOwnerCredentials` on the provider.</span></span>
3. <span data-ttu-id="fcc5f-256">提供程序调用 `ApplicationUserManager` 来验证凭据并创建声明标识。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-256">The provider calls the `ApplicationUserManager` to validate the credentials and create a claims identity.</span></span>
4. <span data-ttu-id="fcc5f-257">如果成功，则提供程序将创建用于生成令牌的身份验证票证。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-257">If that succeeds, the provider creates an authentication ticket, which is used to generate the token.</span></span>

[![](individual-accounts-in-web-api/_static/image16.png)](individual-accounts-in-web-api/_static/image15.png)

<span data-ttu-id="fcc5f-258">OAuth 中间件不知道有关用户帐户的任何信息。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-258">The OAuth middleware doesn't know anything about the user accounts.</span></span> <span data-ttu-id="fcc5f-259">提供程序在中间件和 ASP.NET Identity 之间进行通信。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-259">The provider communicates between the middleware and ASP.NET Identity.</span></span> <span data-ttu-id="fcc5f-260">有关实施授权服务器的详细信息，请参阅[OWIN OAuth 2.0 Authorization server](../../../aspnet/overview/owin-and-katana/owin-oauth-20-authorization-server.md)。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-260">For more information about implementing the authorization server, see [OWIN OAuth 2.0 Authorization Server](../../../aspnet/overview/owin-and-katana/owin-oauth-20-authorization-server.md).</span></span>

### <a name="configuring-web-api-to-use-bearer-tokens"></a><span data-ttu-id="fcc5f-261">将 Web API 配置为使用持有者令牌</span><span class="sxs-lookup"><span data-stu-id="fcc5f-261">Configuring Web API to use Bearer Tokens</span></span>

<span data-ttu-id="fcc5f-262">在 `WebApiConfig.Register` 方法中，以下代码将设置 Web API 管道的身份验证：</span><span class="sxs-lookup"><span data-stu-id="fcc5f-262">In the `WebApiConfig.Register` method, the following code sets up authentication for the Web API pipeline:</span></span>

[!code-csharp[Main](individual-accounts-in-web-api/samples/sample14.cs)]

<span data-ttu-id="fcc5f-263">**HostAuthenticationFilter**类启用使用持有者令牌进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-263">The **HostAuthenticationFilter** class enables authentication using bearer tokens.</span></span>

<span data-ttu-id="fcc5f-264">**Config.suppressdefaulthostauthentication**方法告诉 Web API 忽略任何在请求之前通过 IIS 或 OWIN 中间件进行的身份验证。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-264">The **SuppressDefaultHostAuthentication** method tells Web API to ignore any authentication that happens before the request reaches the Web API pipeline, either by IIS or by OWIN middleware.</span></span> <span data-ttu-id="fcc5f-265">如此，便可以限制 Web API 仅使用持有者令牌进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-265">That way, we can restrict Web API to authenticate only using bearer tokens.</span></span>

> [!NOTE]
> <span data-ttu-id="fcc5f-266">特别是，你的应用程序的 MVC 部分可能使用 forms 身份验证，该身份验证将凭据存储在一个 cookie 中。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-266">In particular, the MVC portion of your app might use forms authentication, which stores credentials in a cookie.</span></span> <span data-ttu-id="fcc5f-267">基于 Cookie 的身份验证需要使用防伪令牌来防止 CSRF 攻击。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-267">Cookie-based authentication requires the use of anti-forgery tokens, to prevent CSRF attacks.</span></span> <span data-ttu-id="fcc5f-268">这对于 web Api 是一个问题，因为 web API 无法方便地将防伪标记发送到客户端。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-268">That's a problem for web APIs, because there is no convenient way for the web API to send the anti-forgery token to the client.</span></span> <span data-ttu-id="fcc5f-269">（有关此问题的更多背景信息，请参阅[在 WEB API 中阻止 CSRF 攻击](preventing-cross-site-request-forgery-csrf-attacks.md)。）调用**config.suppressdefaulthostauthentication**可确保 Web API 容易受到 cookie 中存储的凭据的 CSRF 攻击。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-269">(For more background on this issue, see [Preventing CSRF Attacks in Web API](preventing-cross-site-request-forgery-csrf-attacks.md).) Calling **SuppressDefaultHostAuthentication** ensures that Web API is not vulnerable to CSRF attacks from credentials stored in cookies.</span></span>

<span data-ttu-id="fcc5f-270">当客户端请求受保护的资源时，以下是 Web API 管道中发生的情况：</span><span class="sxs-lookup"><span data-stu-id="fcc5f-270">When the client requests a protected resource, here is what happens in the Web API pipeline:</span></span>

1. <span data-ttu-id="fcc5f-271">**HostAuthentication**筛选器调用 OAuth 中间件来验证令牌。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-271">The **HostAuthentication** filter calls the OAuth middleware to validate the token.</span></span>
2. <span data-ttu-id="fcc5f-272">中间件将令牌转换为声明标识。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-272">The middleware converts the token into a claims identity.</span></span>
3. <span data-ttu-id="fcc5f-273">此时，请求已*通过身份验证*，但未*获得授权*。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-273">At this point, the request is *authenticated* but not *authorized*.</span></span>
4. <span data-ttu-id="fcc5f-274">授权筛选器检查声明标识。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-274">The authorization filter examines the claims identity.</span></span> <span data-ttu-id="fcc5f-275">如果声明向用户授权该资源，则请求已获得授权。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-275">If the claims authorize the user for that resource, the request is authorized.</span></span> <span data-ttu-id="fcc5f-276">默认情况下， **[授权]** 属性将对任何经过身份验证的请求进行授权。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-276">By default, the **[Authorize]** attribute will authorize any request that is authenticated.</span></span> <span data-ttu-id="fcc5f-277">但是，你可以按角色或其他声明授权。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-277">However, you can authorize by role or by other claims.</span></span> <span data-ttu-id="fcc5f-278">有关详细信息，请参阅[WEB API 中的身份验证和授权](authentication-and-authorization-in-aspnet-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-278">For more information, see [Authentication and Authorization in Web API](authentication-and-authorization-in-aspnet-web-api.md).</span></span>
5. <span data-ttu-id="fcc5f-279">如果前面的步骤成功，控制器将返回受保护的资源。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-279">If the previous steps are successful, the controller returns the protected resource.</span></span> <span data-ttu-id="fcc5f-280">否则，客户端将收到401（未授权）错误。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-280">Otherwise, the client receives a 401 (Unauthorized) error.</span></span>

[![](individual-accounts-in-web-api/_static/image18.png)](individual-accounts-in-web-api/_static/image17.png)

## <a name="additional-resources"></a><span data-ttu-id="fcc5f-281">其他资源</span><span class="sxs-lookup"><span data-stu-id="fcc5f-281">Additional Resources</span></span>

- [<span data-ttu-id="fcc5f-282">ASP.NET Identity</span><span class="sxs-lookup"><span data-stu-id="fcc5f-282">ASP.NET Identity</span></span>](../../../identity/index.md)
- <span data-ttu-id="fcc5f-283">[了解适用于 VS2013 RC 的 SPA 模板中的安全功能](https://blogs.msdn.com/b/webdev/archive/2013/09/20/understanding-security-features-in-spa-template.aspx)。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-283">[Understanding Security Features in the SPA Template for VS2013 RC](https://blogs.msdn.com/b/webdev/archive/2013/09/20/understanding-security-features-in-spa-template.aspx).</span></span> <span data-ttu-id="fcc5f-284">Hongye Sun 的 MSDN 博客文章。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-284">MSDN blog post by Hongye Sun.</span></span>
- <span data-ttu-id="fcc5f-285">[二级 WEB API 个人帐户模板–第2部分：本地帐户](http://leastprivilege.com/2013/11/26/dissecting-the-web-api-individual-accounts-templatepart-2-local-accounts/)。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-285">[Dissecting the Web API Individual Accounts Template–Part 2: Local Accounts](http://leastprivilege.com/2013/11/26/dissecting-the-web-api-individual-accounts-templatepart-2-local-accounts/).</span></span> <span data-ttu-id="fcc5f-286">Dominick Baier 的博客文章。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-286">Blog post by Dominick Baier.</span></span>
- <span data-ttu-id="fcc5f-287">[主机身份验证和具有 OWIN 的 WEB API](http://brockallen.com/2013/10/27/host-authentication-and-web-api-with-owin-and-active-vs-passive-authentication-middleware/)。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-287">[Host authentication and Web API with OWIN](http://brockallen.com/2013/10/27/host-authentication-and-web-api-with-owin-and-active-vs-passive-authentication-middleware/).</span></span> <span data-ttu-id="fcc5f-288">Brock Allen 的 `SuppressDefaultHostAuthentication` 和 `HostAuthenticationFilter` 的很好的说明。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-288">A good explanation of `SuppressDefaultHostAuthentication` and `HostAuthenticationFilter` by Brock Allen.</span></span>
- <span data-ttu-id="fcc5f-289">[自定义 VS 2013 模板 ASP.NET Identity 中的配置文件信息](https://blogs.msdn.com/b/webdev/archive/2013/10/16/customizing-profile-information-in-asp-net-identity-in-vs-2013-templates.aspx)。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-289">[Customizing profile information in ASP.NET Identity in VS 2013 templates](https://blogs.msdn.com/b/webdev/archive/2013/10/16/customizing-profile-information-in-asp-net-identity-in-vs-2013-templates.aspx).</span></span> <span data-ttu-id="fcc5f-290">MSDN 博客文章 Pranav Rastogi 撰写。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-290">MSDN blog post by Pranav Rastogi.</span></span>
- <span data-ttu-id="fcc5f-291">[ASP.NET Identity 中的 UserManager 类的按请求生存期管理](https://blogs.msdn.com/b/webdev/archive/2014/02/12/per-request-lifetime-management-for-usermanager-class-in-asp-net-identity.aspx)。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-291">[Per request lifetime management for UserManager class in ASP.NET Identity](https://blogs.msdn.com/b/webdev/archive/2014/02/12/per-request-lifetime-management-for-usermanager-class-in-asp-net-identity.aspx).</span></span> <span data-ttu-id="fcc5f-292">MSDN 博客文章 Suhas Joshi，具有对 `UserManager` 类的良好说明。</span><span class="sxs-lookup"><span data-stu-id="fcc5f-292">MSDN blog post by Suhas Joshi, with a good explanation of the `UserManager` class.</span></span>

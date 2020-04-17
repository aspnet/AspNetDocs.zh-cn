---
uid: aspnet/overview/owin-and-katana/owin-oauth-20-authorization-server
title: OWIN OAuth 2.0 授权服务器 |微软文档
author: hongyes
description: 本教程将指导您如何使用 OWIN OAuth 中间件实现 OAuth 2.0 授权服务器。 这是一个高级教程，只有出...
ms.author: riande
ms.date: 03/20/2014
ms.assetid: 20acee16-c70c-41e9-b38f-92bfcf9a4c1c
msc.legacyurl: /aspnet/overview/owin-and-katana/owin-oauth-20-authorization-server
msc.type: authoredcontent
ms.openlocfilehash: d758fa2639d10e1b7be8d87c5d1f7adb7e292ac7
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81540379"
---
<a name="owin-oauth-20-authorization-server"></a><span data-ttu-id="65742-104">OWIN OAuth 2.0 授权服务器</span><span class="sxs-lookup"><span data-stu-id="65742-104">OWIN OAuth 2.0 Authorization Server</span></span>
====================
<span data-ttu-id="65742-105">由[孙洪业](https://github.com/hongyes)和[普拉布拉杰·蒂加拉詹](https://github.com/Praburaj)</span><span class="sxs-lookup"><span data-stu-id="65742-105">by [Hongye Sun](https://github.com/hongyes) and [Praburaj Thiagarajan](https://github.com/Praburaj)</span></span>

> <span data-ttu-id="65742-106">本教程将指导您如何使用 OWIN OAuth 中间件实现 OAuth 2.0 授权服务器。</span><span class="sxs-lookup"><span data-stu-id="65742-106">This tutorial will guide you on how to implement an OAuth 2.0 Authorization Server using OWIN OAuth middleware.</span></span> <span data-ttu-id="65742-107">这是一个高级教程，仅概述创建 OWIN OAuth 2.0 授权服务器的步骤。</span><span class="sxs-lookup"><span data-stu-id="65742-107">This is an advanced tutorial that only outlines the steps to create an OWIN OAuth 2.0 Authorization Server.</span></span> <span data-ttu-id="65742-108">这不是一步一步的教程。</span><span class="sxs-lookup"><span data-stu-id="65742-108">This is not a step by step tutorial.</span></span> <span data-ttu-id="65742-109">[下载示例代码](https://code.msdn.microsoft.com/OWIN-OAuth-20-Authorization-ba2b8783/file/114932/1/AuthorizationServer.zip)。</span><span class="sxs-lookup"><span data-stu-id="65742-109">[Download the sample code](https://code.msdn.microsoft.com/OWIN-OAuth-20-Authorization-ba2b8783/file/114932/1/AuthorizationServer.zip).</span></span>
>
> > [!NOTE]
> > <span data-ttu-id="65742-110">此大纲不应用于创建安全生产应用。</span><span class="sxs-lookup"><span data-stu-id="65742-110">This outline should not be intended to be used for creating a secure production app.</span></span> <span data-ttu-id="65742-111">本教程旨在仅提供如何使用 OWIN OAuth 中间件实现 OAuth 2.0 授权服务器的大纲。</span><span class="sxs-lookup"><span data-stu-id="65742-111">This tutorial is intended to provide only an outline on how to implement an OAuth 2.0 Authorization Server using OWIN OAuth middleware.</span></span>
>
>
> ## <a name="software-versions"></a><span data-ttu-id="65742-112">软件版本</span><span class="sxs-lookup"><span data-stu-id="65742-112">Software versions</span></span>
>
> | <span data-ttu-id="65742-113">**在教程中显示**</span><span class="sxs-lookup"><span data-stu-id="65742-113">**Shown in the tutorial**</span></span> | <span data-ttu-id="65742-114">**也适用于**</span><span class="sxs-lookup"><span data-stu-id="65742-114">**Also works with**</span></span> |
> | --- | --- |
> | <span data-ttu-id="65742-115">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="65742-115">Windows 8.1</span></span> | <span data-ttu-id="65742-116">视窗 8， 视窗 7</span><span class="sxs-lookup"><span data-stu-id="65742-116">Windows 8, Windows 7</span></span> |
> | [<span data-ttu-id="65742-117">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="65742-117">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013) | <span data-ttu-id="65742-118">[视觉工作室 2013 快递为桌面](https://my.visualstudio.com/Downloads?q=visual%20studio%202013#d-2013-express).</span><span class="sxs-lookup"><span data-stu-id="65742-118">[Visual Studio 2013 Express for Desktop](https://my.visualstudio.com/Downloads?q=visual%20studio%202013#d-2013-express).</span></span> <span data-ttu-id="65742-119">带有最新更新的 Visual Studio 2012 应该可以正常工作，但本教程尚未使用它进行测试，并且某些菜单选择和对话框是不同的。</span><span class="sxs-lookup"><span data-stu-id="65742-119">Visual Studio 2012 with the latest update should work, but the tutorial has not been tested with it, and some menu selections and dialog boxes are different.</span></span> |
> | <span data-ttu-id="65742-120">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="65742-120">.NET 4.5</span></span> |  |
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="65742-121">问题和评论</span><span class="sxs-lookup"><span data-stu-id="65742-121">Questions and Comments</span></span>
>
> <span data-ttu-id="65742-122">如果您有与本教程没有直接关系的问题，您可以在[GitHub 上的 Katana 项目](https://github.com/aspnet/AspNetKatana/)上发布这些问题。</span><span class="sxs-lookup"><span data-stu-id="65742-122">If you have questions that are not directly related to the tutorial, you can post them at [Katana Project on GitHub](https://github.com/aspnet/AspNetKatana/).</span></span> <span data-ttu-id="65742-123">有关教程本身的问题和注释，请参阅页面底部的注释部分。</span><span class="sxs-lookup"><span data-stu-id="65742-123">For questions and comments regarding the tutorial itself, see the comments section at the bottom of the page.</span></span>


<span data-ttu-id="65742-124">[OAuth 2.0 框架](http://tools.ietf.org/html/rfc6749)使第三方应用能够获得对 HTTP 服务的有限访问权限。</span><span class="sxs-lookup"><span data-stu-id="65742-124">The [OAuth 2.0 framework](http://tools.ietf.org/html/rfc6749) enables a third-party app to obtain limited access to an HTTP service.</span></span> <span data-ttu-id="65742-125">客户端不需要使用资源所有者的凭据来访问受保护的资源，而是获取访问令牌（这是表示特定作用域、生存期和其他访问属性的字符串）。</span><span class="sxs-lookup"><span data-stu-id="65742-125">Instead of using the resource owner's credentials to access a protected resource, the client obtains an access token (which is a string denoting a specific scope, lifetime, and other access attributes).</span></span> <span data-ttu-id="65742-126">访问令牌由授权服务器在资源所有者批准下颁发给第三方客户端。</span><span class="sxs-lookup"><span data-stu-id="65742-126">Access tokens are issued to third-party clients by an authorization server with the approval of the resource owner.</span></span>

<span data-ttu-id="65742-127">本教程将介绍：</span><span class="sxs-lookup"><span data-stu-id="65742-127">This tutorial will cover:</span></span>

- <span data-ttu-id="65742-128">如何创建授权服务器以支持四种授权授予类型和刷新令牌：</span><span class="sxs-lookup"><span data-stu-id="65742-128">How to create an authorization server to support four authorization grant types and refresh tokens:</span></span>
    - <span data-ttu-id="65742-129">授权代码授予</span><span class="sxs-lookup"><span data-stu-id="65742-129">Authorization code grant</span></span>
    - <span data-ttu-id="65742-130">隐式授予</span><span class="sxs-lookup"><span data-stu-id="65742-130">Implicit Grant</span></span>
    - <span data-ttu-id="65742-131">资源所有者密码凭据授予</span><span class="sxs-lookup"><span data-stu-id="65742-131">Resource Owner Password Credentials Grant</span></span>
    - <span data-ttu-id="65742-132">客户端凭据授予</span><span class="sxs-lookup"><span data-stu-id="65742-132">Client Credentials Grant</span></span>
- <span data-ttu-id="65742-133">创建受访问令牌保护的资源服务器。</span><span class="sxs-lookup"><span data-stu-id="65742-133">Creating a resource server which is protected by an access token.</span></span>
- <span data-ttu-id="65742-134">创建 OAuth 2.0 客户端。</span><span class="sxs-lookup"><span data-stu-id="65742-134">Creating OAuth 2.0 clients.</span></span>

<a id="prerequisites"></a>
## <a name="prerequisites"></a><span data-ttu-id="65742-135">先决条件</span><span class="sxs-lookup"><span data-stu-id="65742-135">Prerequisites</span></span>

- <span data-ttu-id="65742-136">[Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/downloads#d-2013-editions)或免费[的 Visual Studio Express 2013，](https://www.microsoft.com/visualstudio/eng/downloads#d-2013-express)如页面顶部**的软件版本**所示。</span><span class="sxs-lookup"><span data-stu-id="65742-136">[Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/downloads#d-2013-editions) or the free [Visual Studio Express 2013](https://www.microsoft.com/visualstudio/eng/downloads#d-2013-express), as indicated in **Software Versions** at the top of the page.</span></span>
- <span data-ttu-id="65742-137">熟悉 OWIN。</span><span class="sxs-lookup"><span data-stu-id="65742-137">Familiarity with OWIN.</span></span> <span data-ttu-id="65742-138">请参阅[开始与卡塔纳项目和](https://msdn.microsoft.com/magazine/dn451439.aspx)[什么在OWIN和卡塔纳的新增功能](index.md)。</span><span class="sxs-lookup"><span data-stu-id="65742-138">See [Getting Started with the Katana Project](https://msdn.microsoft.com/magazine/dn451439.aspx) and [What's new in OWIN and Katana](index.md).</span></span>
- <span data-ttu-id="65742-139">熟悉[OAuth](http://tools.ietf.org/html/rfc6749)术语，包括[角色](http://tools.ietf.org/html/rfc6749#section-1.1)、[协议流程](http://tools.ietf.org/html/rfc6749#section-1.2)和[授权授予](http://tools.ietf.org/html/rfc6749#section-1.3)。</span><span class="sxs-lookup"><span data-stu-id="65742-139">Familiarity with [OAuth](http://tools.ietf.org/html/rfc6749) terminology, including [Roles](http://tools.ietf.org/html/rfc6749#section-1.1), [Protocol Flow](http://tools.ietf.org/html/rfc6749#section-1.2), and [Authorization Grant](http://tools.ietf.org/html/rfc6749#section-1.3).</span></span> <span data-ttu-id="65742-140">[OAuth 2.0 介绍](http://tools.ietf.org/html/rfc6749#section-1)提供了很好的介绍。</span><span class="sxs-lookup"><span data-stu-id="65742-140">[OAuth 2.0 introduction](http://tools.ietf.org/html/rfc6749#section-1) provides a good introduction.</span></span>

## <a name="create-an-authorization-server"></a><span data-ttu-id="65742-141">创建授权服务器</span><span class="sxs-lookup"><span data-stu-id="65742-141">Create an Authorization Server</span></span>

<span data-ttu-id="65742-142">在本教程中，我们将大致勾勒出如何使用[OWIN](https://msdn.microsoft.com/magazine/dn451439.aspx)和 ASP.NET MVC 创建授权服务器。</span><span class="sxs-lookup"><span data-stu-id="65742-142">In this tutorial, we will roughly sketch out how to use [OWIN](https://msdn.microsoft.com/magazine/dn451439.aspx) and ASP.NET MVC to create an authorization server.</span></span> <span data-ttu-id="65742-143">我们希望很快为已完成的示例提供下载，因为本教程不包括每个步骤。</span><span class="sxs-lookup"><span data-stu-id="65742-143">We hope to soon provide a download for the completed sample, as this tutorial does not include each step.</span></span> <span data-ttu-id="65742-144">首先，创建名为 *"授权服务器"* 的空 Web 应用并安装以下程序包：</span><span class="sxs-lookup"><span data-stu-id="65742-144">First, create an empty web app named *AuthorizationServer* and install the following packages:</span></span>

- <span data-ttu-id="65742-145">微软.阿斯普内.Mvc</span><span class="sxs-lookup"><span data-stu-id="65742-145">Microsoft.AspNet.Mvc</span></span>
- <span data-ttu-id="65742-146">Microsoft.Owin.Host.SystemWeb</span><span class="sxs-lookup"><span data-stu-id="65742-146">Microsoft.Owin.Host.SystemWeb</span></span>
- <span data-ttu-id="65742-147">Microsoft.Owin.Security.OAuth</span><span class="sxs-lookup"><span data-stu-id="65742-147">Microsoft.Owin.Security.OAuth</span></span>
- <span data-ttu-id="65742-148">Microsoft.Owin.Security.Cookies</span><span class="sxs-lookup"><span data-stu-id="65742-148">Microsoft.Owin.Security.Cookies</span></span>
- <span data-ttu-id="65742-149">微软.Owin.Security.Google（或任何其他社交登录包，如微软.Owin.Security.Facebook）</span><span class="sxs-lookup"><span data-stu-id="65742-149">Microsoft.Owin.Security.Google (Or any other social login package such as Microsoft.Owin.Security.Facebook)</span></span>

<span data-ttu-id="65742-150">在名为 *"启动"* 的项目根文件夹下添加[OWIN 启动类](owin-startup-class-detection.md)。</span><span class="sxs-lookup"><span data-stu-id="65742-150">Add an [OWIN Startup class](owin-startup-class-detection.md) under the project root folder named *Startup*.</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample1.cs?highlight=8)]

<span data-ttu-id="65742-151">创建 *"应用\_开始"* 文件夹。</span><span class="sxs-lookup"><span data-stu-id="65742-151">Create an *App\_Start* folder.</span></span> <span data-ttu-id="65742-152">选择 *"应用\_启动"* 文件夹并使用 Shift_Alt_A 添加 *"授权服务器"[应用\_启动]启动.Auth.cs*文件的下载版本。</span><span class="sxs-lookup"><span data-stu-id="65742-152">Select the *App\_Start* folder and use Shift+Alt+A to add the downloaded version of the *AuthorizationServer\App\_Start\Startup.Auth.cs* file.</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample2.cs)]

<span data-ttu-id="65742-153">上述代码支持应用程序/外部登录 Cookie 和 Google 身份验证，授权服务器本身使用它们来管理帐户。</span><span class="sxs-lookup"><span data-stu-id="65742-153">The code above enables application/external sign in cookies and Google authentication, which are used by authorization server itself to manage accounts.</span></span>

<span data-ttu-id="65742-154">扩展`UseOAuthAuthorizationServer`方法是设置授权服务器。</span><span class="sxs-lookup"><span data-stu-id="65742-154">The `UseOAuthAuthorizationServer` extension method is to setup the authorization server.</span></span> <span data-ttu-id="65742-155">设置选项包括：</span><span class="sxs-lookup"><span data-stu-id="65742-155">The setup options are:</span></span>

- <span data-ttu-id="65742-156">`AuthorizeEndpointPath`：客户端应用程序将重定向用户代理以获得用户同意发出令牌或代码的请求路径。</span><span class="sxs-lookup"><span data-stu-id="65742-156">`AuthorizeEndpointPath`: The request path where client applications will redirect the user-agent in order to obtain the users consent to issue a token or code.</span></span> <span data-ttu-id="65742-157">它必须以前导斜杠开头，例如，""。`/Authorize`</span><span class="sxs-lookup"><span data-stu-id="65742-157">It must begin with a leading slash, for example, "`/Authorize`".</span></span>
- <span data-ttu-id="65742-158">`TokenEndpointPath`：请求路径客户端应用程序直接通信以获取访问令牌。</span><span class="sxs-lookup"><span data-stu-id="65742-158">`TokenEndpointPath`: The request path client applications directly communicate to obtain the access token.</span></span> <span data-ttu-id="65742-159">它必须以前导斜杠开头，如"/令牌"。</span><span class="sxs-lookup"><span data-stu-id="65742-159">It must begin with a leading slash, like "/Token".</span></span> <span data-ttu-id="65742-160">如果客户端被颁发[客户端\_密钥](http://tools.ietf.org/html/rfc6749#appendix-A.2)，则必须将其提供给此终结点。</span><span class="sxs-lookup"><span data-stu-id="65742-160">If the client is issued a [client\_secret](http://tools.ietf.org/html/rfc6749#appendix-A.2), it must be provided to this endpoint.</span></span>
- <span data-ttu-id="65742-161">`ApplicationCanDisplayErrors`：设置为`true`如果 Web 应用程序想要为终结点上的`/Authorize`客户端验证错误生成自定义错误页。</span><span class="sxs-lookup"><span data-stu-id="65742-161">`ApplicationCanDisplayErrors`: Set to `true` if the web application wants to generate a custom error page for the client validation errors on `/Authorize` endpoint.</span></span> <span data-ttu-id="65742-162">仅当浏览器未重定向回客户端应用程序（例如，`client_id`当 或`redirect_uri`不正确时），才需要这样做。</span><span class="sxs-lookup"><span data-stu-id="65742-162">This is only needed for cases where the browser is not redirected back to the client application, for example, when the `client_id` or `redirect_uri` are incorrect.</span></span> <span data-ttu-id="65742-163">终结点`/Authorize`应期望看到"auth"。错误"，"哦。错误描述"和"错误描述"。ErrorUri"属性将添加到 OWIN 环境中。</span><span class="sxs-lookup"><span data-stu-id="65742-163">The `/Authorize` endpoint should expect to see the "oauth.Error", "oauth.ErrorDescription", and "oauth.ErrorUri" properties are added to the OWIN environment.</span></span>

    > [!NOTE]
    > <span data-ttu-id="65742-164">如果为 true，授权服务器将返回包含错误详细信息的默认错误页。</span><span class="sxs-lookup"><span data-stu-id="65742-164">If not true, the authorization server will return a default error page with the error details.</span></span>
- <span data-ttu-id="65742-165">`AllowInsecureHttp`：如果为 True，允许授权和令牌请求到达 HTTP URI 地址，并允许`redirect_uri`传入授权请求参数具有 HTTP URI 地址。</span><span class="sxs-lookup"><span data-stu-id="65742-165">`AllowInsecureHttp`: True to allow authorize and token requests to arrive on HTTP URI addresses, and to allow incoming `redirect_uri` authorize request parameters to have HTTP URI addresses.</span></span>

    > [!WARNING]
    > <span data-ttu-id="65742-166">安全性 - 这仅用于开发。</span><span class="sxs-lookup"><span data-stu-id="65742-166">Security - This is for development only.</span></span>
- <span data-ttu-id="65742-167">`Provider`：应用程序为处理授权服务器中间件引发的事件而提供的对象。</span><span class="sxs-lookup"><span data-stu-id="65742-167">`Provider`: The object provided by the application to process events raised by the Authorization Server middleware.</span></span> <span data-ttu-id="65742-168">应用程序可以完全实现接口，也可以创建此服务器支持的 OAuth`OAuthAuthorizationServerProvider`流所需的实例和分配委托。</span><span class="sxs-lookup"><span data-stu-id="65742-168">The application may implement the interface fully, or it may create an instance of `OAuthAuthorizationServerProvider` and assign delegates necessary for the OAuth flows this server supports.</span></span>
- <span data-ttu-id="65742-169">`AuthorizationCodeProvider`：生成一次性授权代码以返回到客户端应用程序。</span><span class="sxs-lookup"><span data-stu-id="65742-169">`AuthorizationCodeProvider`: Produces a single-use authorization code to return to the client application.</span></span> <span data-ttu-id="65742-170">为了保护 OAuth 服务器的安全，应用程序**必须**提供一个实例`AuthorizationCodeProvider`，其中`OnCreate/OnCreateAsync`事件生成的令牌仅对 一次调用 有效`OnReceive/OnReceiveAsync`。</span><span class="sxs-lookup"><span data-stu-id="65742-170">For the OAuth server to be secure the application **MUST** provide an instance for `AuthorizationCodeProvider` where the token produced by the `OnCreate/OnCreateAsync` event is considered valid for only one call to `OnReceive/OnReceiveAsync`.</span></span>
- <span data-ttu-id="65742-171">`RefreshTokenProvider`：生成刷新令牌，可在需要时用于生成新的访问令牌。</span><span class="sxs-lookup"><span data-stu-id="65742-171">`RefreshTokenProvider`: Produces a refresh token which may be used to produce a new access token when needed.</span></span> <span data-ttu-id="65742-172">如果未提供授权服务器将不会从`/Token`终结点返回刷新令牌。</span><span class="sxs-lookup"><span data-stu-id="65742-172">If not provided the authorization server will not return refresh tokens from the `/Token` endpoint.</span></span>

## <a name="account-management"></a><span data-ttu-id="65742-173">帐户管理</span><span class="sxs-lookup"><span data-stu-id="65742-173">Account Management</span></span>

<span data-ttu-id="65742-174">OAuth 不关心您管理用户帐户信息的位置或方式。</span><span class="sxs-lookup"><span data-stu-id="65742-174">OAuth doesn't care where or how you manage your user account information.</span></span> <span data-ttu-id="65742-175">负责它的[ASP.NET身份](../../../identity/index.md)。</span><span class="sxs-lookup"><span data-stu-id="65742-175">It's [ASP.NET Identity](../../../identity/index.md) which is responsible for it.</span></span> <span data-ttu-id="65742-176">在本教程中，我们将简化帐户管理代码，并确保用户可以使用 OWIN Cookie 中间件登录。</span><span class="sxs-lookup"><span data-stu-id="65742-176">In this tutorial, we will simplify the account management code and just make sure that user can login using OWIN cookie middleware.</span></span> <span data-ttu-id="65742-177">下面是 ： 的`AccountController`简化示例代码：</span><span class="sxs-lookup"><span data-stu-id="65742-177">Here is the simplified sample code for the `AccountController`:</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample3.cs)]

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample4.cs?highlight=1)]

<span data-ttu-id="65742-178">`ValidateClientRedirectUri`用于验证客户端及其注册的重定向 URL。</span><span class="sxs-lookup"><span data-stu-id="65742-178">`ValidateClientRedirectUri` is used to validate the client with its registered redirect URL.</span></span> <span data-ttu-id="65742-179">`ValidateClientAuthentication`检查基本方案标头和窗体正文以获取客户端的凭据。</span><span class="sxs-lookup"><span data-stu-id="65742-179">`ValidateClientAuthentication` checks the basic scheme header and form body to get the client's credentials.</span></span>

<span data-ttu-id="65742-180">登录页面如下所示：</span><span class="sxs-lookup"><span data-stu-id="65742-180">The login page is shown below:</span></span>

![](owin-oauth-20-authorization-server/_static/image1.png)

<span data-ttu-id="65742-181">立即查看 IETF 的 OAuth 2[授权代码授予](http://tools.ietf.org/html/rfc6749#section-4.1)部分。</span><span class="sxs-lookup"><span data-stu-id="65742-181">Review the IETF's OAuth 2 [Authorization Code Grant](http://tools.ietf.org/html/rfc6749#section-4.1) section now.</span></span>

<span data-ttu-id="65742-182">**提供程序**（下表中）是[OAuth 授权服务器选项](https://msdn.microsoft.com/library/microsoft.owin.security.oauth.oauthauthorizationserveroptions(v=vs.111).aspx)。提供程序，其类型 为`OAuthAuthorizationServerProvider`，它包含所有 OAuth 服务器事件。</span><span class="sxs-lookup"><span data-stu-id="65742-182">**Provider** (in the table below) is [OAuthAuthorizationServerOptions](https://msdn.microsoft.com/library/microsoft.owin.security.oauth.oauthauthorizationserveroptions(v=vs.111).aspx).Provider, which is of type `OAuthAuthorizationServerProvider`, which contains all OAuth server events.</span></span>

| <span data-ttu-id="65742-183">授权代码授予部分的流步骤</span><span class="sxs-lookup"><span data-stu-id="65742-183">Flow steps from Authorization Code Grant section</span></span> | <span data-ttu-id="65742-184">示例下载执行以下步骤：</span><span class="sxs-lookup"><span data-stu-id="65742-184">Sample download performs these steps with:</span></span> |
| --- | --- |
|  |  |
| <span data-ttu-id="65742-185">（A） 客户端通过将资源所有者的用户代理定向到授权终结点来启动流。</span><span class="sxs-lookup"><span data-stu-id="65742-185">(A) The client initiates the flow by directing the resource owner's user-agent to the authorization endpoint.</span></span> <span data-ttu-id="65742-186">客户端包括其客户端标识符、请求的范围、本地状态和重定向 URI，授权服务器将在授予（或拒绝）访问权限后将用户代理发送回该 URI。</span><span class="sxs-lookup"><span data-stu-id="65742-186">The client includes its client identifier, requested scope, local state, and a redirection URI to which the authorization server will send the user-agent back once access is granted (or denied).</span></span> | <span data-ttu-id="65742-187">提供程序.匹配终结点提供程序.验证客户端重定向提供程序.验证授权请求提供程序.授权终结点</span><span class="sxs-lookup"><span data-stu-id="65742-187">Provider.MatchEndpoint Provider.ValidateClientRedirectUri Provider.ValidateAuthorizeRequest Provider.AuthorizeEndpoint</span></span> |
|  |  |
| <span data-ttu-id="65742-188">（B） 授权服务器对资源所有者进行身份验证（通过用户代理），并确定资源所有者是授予还是拒绝客户端的访问请求。</span><span class="sxs-lookup"><span data-stu-id="65742-188">(B) The authorization server authenticates the resource owner (via the user-agent) and establishes whether the resource owner grants or denies the client's access request.</span></span> | <span data-ttu-id="65742-189">**如果用户授予访问权限&gt;&lt;** 提供程序.匹配终结点提供程序.验证客户端重定向提供程序.验证授权请求提供程序.授权终结点授权码提供程序.创建Async</span><span class="sxs-lookup"><span data-stu-id="65742-189">**&lt;If user grants access&gt;** Provider.MatchEndpoint Provider.ValidateClientRedirectUri Provider.ValidateAuthorizeRequest Provider.AuthorizeEndpoint AuthorizationCodeProvider.CreateAsync</span></span> |
|  |  |
| <span data-ttu-id="65742-190">（C） 假设资源所有者授予访问权限，授权服务器使用前面提供的重定向 URI（在请求中或客户端注册期间）将用户代理重定向回客户端。</span><span class="sxs-lookup"><span data-stu-id="65742-190">(C) Assuming the resource owner grants access, the authorization server redirects the user-agent back to the client using the redirection URI provided earlier (in the request or during client registration).</span></span> <span data-ttu-id="65742-191">...</span><span class="sxs-lookup"><span data-stu-id="65742-191">...</span></span> |  |
|  |  |
| <span data-ttu-id="65742-192">（D） 客户端通过包含上一步骤中收到的授权代码，从授权服务器的令牌终结点请求访问令牌。</span><span class="sxs-lookup"><span data-stu-id="65742-192">(D) The client requests an access token from the authorization server's token endpoint by including the authorization code received in the previous step.</span></span> <span data-ttu-id="65742-193">发出请求时，客户端会使用授权服务器进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="65742-193">When making the request, the client authenticates with the authorization server.</span></span> <span data-ttu-id="65742-194">客户端包括用于获取验证授权码的重定向 URI。</span><span class="sxs-lookup"><span data-stu-id="65742-194">The client includes the redirection URI used to obtain the authorization code for verification.</span></span> | <span data-ttu-id="65742-195">提供程序.匹配终结点提供程序.验证客户端身份验证授权代码提供程序.接收 Async 提供程序.验证令牌请求提供程序.授予授权代码提供程序.令牌终结点访问令牌提供程序.创建 async 刷新令牌提供程序.创建async</span><span class="sxs-lookup"><span data-stu-id="65742-195">Provider.MatchEndpoint Provider.ValidateClientAuthentication AuthorizationCodeProvider.ReceiveAsync Provider.ValidateTokenRequest Provider.GrantAuthorizationCode Provider.TokenEndpoint AccessTokenProvider.CreateAsync RefreshTokenProvider.CreateAsync</span></span> |

<span data-ttu-id="65742-196">下面显示了 用于`AuthorizationCodeProvider.CreateAsync``ReceiveAsync`和控制授权代码的创建和验证的示例实现。</span><span class="sxs-lookup"><span data-stu-id="65742-196">A sample implementation for `AuthorizationCodeProvider.CreateAsync` and `ReceiveAsync` to control the creation and validation of authorization code is shown below.</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample5.cs)]

<span data-ttu-id="65742-197">上述代码使用内存中并发字典来存储代码和标识票证，并在收到代码后还原标识。</span><span class="sxs-lookup"><span data-stu-id="65742-197">The code above uses an in-memory concurrent dictionary to store the code and identity ticket and restore the identity after receiving the code.</span></span> <span data-ttu-id="65742-198">在实际应用程序中，它将被持久性数据存储替换。</span><span class="sxs-lookup"><span data-stu-id="65742-198">In a real application, it would be replaced by a persistent data store.</span></span> <span data-ttu-id="65742-199">授权终结点供资源所有者授予对客户端的访问权限。</span><span class="sxs-lookup"><span data-stu-id="65742-199">The authorization endpoint is for the resource owner to grant access to the client.</span></span> <span data-ttu-id="65742-200">通常，它需要一个用户界面来允许用户单击按钮并确认授予。</span><span class="sxs-lookup"><span data-stu-id="65742-200">Usually, it needs a user interface to allow the user to click a button and confirm the grant.</span></span> <span data-ttu-id="65742-201">OWIN OAuth 中间件允许应用程序代码处理授权终结点。</span><span class="sxs-lookup"><span data-stu-id="65742-201">OWIN OAuth middleware allows application code to handle the authorization endpoint.</span></span> <span data-ttu-id="65742-202">在我们的示例应用中，我们使用调用`OAuthController`的 MVC 控制器来处理它。</span><span class="sxs-lookup"><span data-stu-id="65742-202">In our sample app, we use an MVC controller called `OAuthController` to handle it.</span></span> <span data-ttu-id="65742-203">下面是实现的示例：</span><span class="sxs-lookup"><span data-stu-id="65742-203">Here is the sample implementation:</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample6.cs?highlight=15)]

<span data-ttu-id="65742-204">此操作`Authorize`将首先检查用户是否登录到授权服务器。</span><span class="sxs-lookup"><span data-stu-id="65742-204">The `Authorize` action will first check if the user has logged in to the authorization server.</span></span> <span data-ttu-id="65742-205">如果没有，身份验证中间件会向调用方提出使用"应用程序"Cookie 进行身份验证的挑战，并重定向到登录页。</span><span class="sxs-lookup"><span data-stu-id="65742-205">If not, the authentication middleware challenges the caller to authenticate using the "Application" cookie and redirects to the login page.</span></span> <span data-ttu-id="65742-206">（请参阅上面突出显示的代码。如果用户已登录，它将呈现"授权"视图，如下所示：</span><span class="sxs-lookup"><span data-stu-id="65742-206">(See highlighted code above.) If user has logged in, it will render the Authorize view, as shown below:</span></span>

![](owin-oauth-20-authorization-server/_static/image2.png)

<span data-ttu-id="65742-207">如果选择了 **"授予**"按钮，`Authorize`该操作将创建新的"持有者"标识并登录。</span><span class="sxs-lookup"><span data-stu-id="65742-207">If the **Grant** button is selected, the `Authorize` action will create a new "Bearer" identity and sign in with it.</span></span> <span data-ttu-id="65742-208">它将触发授权服务器以生成无记名令牌，并将其发送回具有 JSON 负载的客户端。</span><span class="sxs-lookup"><span data-stu-id="65742-208">It will trigger the authorization server to generate a bearer token and send it back to the client with JSON payload.</span></span>

### <a name="implicit-grant"></a><span data-ttu-id="65742-209">隐式授予</span><span class="sxs-lookup"><span data-stu-id="65742-209">Implicit Grant</span></span>

<span data-ttu-id="65742-210">立即请参阅 IETF 的 OAuth 2[隐式授予](http://tools.ietf.org/html/rfc6749#section-4.2)部分。</span><span class="sxs-lookup"><span data-stu-id="65742-210">Refer to the IETF's OAuth 2 [Implicit Grant](http://tools.ietf.org/html/rfc6749#section-4.2) section now.</span></span>

 <span data-ttu-id="65742-211">图 4 所示[的隐式授予](http://tools.ietf.org/html/rfc6749#section-4.2)流是 OWIN OAuth 中间件后面的流和映射。</span><span class="sxs-lookup"><span data-stu-id="65742-211">The [Implicit Grant](http://tools.ietf.org/html/rfc6749#section-4.2) flow shown in Figure 4 is the flow and mapping which the OWIN OAuth middleware follows.</span></span>

| <span data-ttu-id="65742-212">来自隐式授予部分的流步骤</span><span class="sxs-lookup"><span data-stu-id="65742-212">Flow steps from Implicit Grant section</span></span> | <span data-ttu-id="65742-213">示例下载执行以下步骤：</span><span class="sxs-lookup"><span data-stu-id="65742-213">Sample download performs these steps with:</span></span> |
| --- | --- |
|  |  |
| <span data-ttu-id="65742-214">（A） 客户端通过将资源所有者的用户代理定向到授权终结点来启动流。</span><span class="sxs-lookup"><span data-stu-id="65742-214">(A) The client initiates the flow by directing the resource owner's user-agent to the authorization endpoint.</span></span> <span data-ttu-id="65742-215">客户端包括其客户端标识符、请求的范围、本地状态和重定向 URI，授权服务器将在授予（或拒绝）访问权限后将用户代理发送回该 URI。</span><span class="sxs-lookup"><span data-stu-id="65742-215">The client includes its client identifier, requested scope, local state, and a redirection URI to which the authorization server will send the user-agent back once access is granted (or denied).</span></span> | <span data-ttu-id="65742-216">提供程序.匹配终结点提供程序.验证客户端重定向提供程序.验证授权请求提供程序.授权终结点</span><span class="sxs-lookup"><span data-stu-id="65742-216">Provider.MatchEndpoint Provider.ValidateClientRedirectUri Provider.ValidateAuthorizeRequest Provider.AuthorizeEndpoint</span></span> |
|  |  |
| <span data-ttu-id="65742-217">（B） 授权服务器对资源所有者进行身份验证（通过用户代理），并确定资源所有者是授予还是拒绝客户端的访问请求。</span><span class="sxs-lookup"><span data-stu-id="65742-217">(B) The authorization server authenticates the resource owner (via the user-agent) and establishes whether the resource owner grants or denies the client's access request.</span></span> | <span data-ttu-id="65742-218">**如果用户授予访问权限&gt;&lt;** 提供程序.匹配终结点提供程序.验证客户端重定向提供程序.验证授权请求提供程序.授权终结点授权码提供程序.创建Async</span><span class="sxs-lookup"><span data-stu-id="65742-218">**&lt;If user grants access&gt;** Provider.MatchEndpoint Provider.ValidateClientRedirectUri Provider.ValidateAuthorizeRequest Provider.AuthorizeEndpoint AuthorizationCodeProvider.CreateAsync</span></span> |
|  |  |
| <span data-ttu-id="65742-219">（C） 假设资源所有者授予访问权限，授权服务器使用前面提供的重定向 URI（在请求中或客户端注册期间）将用户代理重定向回客户端。</span><span class="sxs-lookup"><span data-stu-id="65742-219">(C) Assuming the resource owner grants access, the authorization server redirects the user-agent back to the client using the redirection URI provided earlier (in the request or during client registration).</span></span> <span data-ttu-id="65742-220">...</span><span class="sxs-lookup"><span data-stu-id="65742-220">...</span></span> |  |
|  |  |
| <span data-ttu-id="65742-221">（D） 客户端通过包含上一步骤中收到的授权代码，从授权服务器的令牌终结点请求访问令牌。</span><span class="sxs-lookup"><span data-stu-id="65742-221">(D) The client requests an access token from the authorization server's token endpoint by including the authorization code received in the previous step.</span></span> <span data-ttu-id="65742-222">发出请求时，客户端会使用授权服务器进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="65742-222">When making the request, the client authenticates with the authorization server.</span></span> <span data-ttu-id="65742-223">客户端包括用于获取验证授权码的重定向 URI。</span><span class="sxs-lookup"><span data-stu-id="65742-223">The client includes the redirection URI used to obtain the authorization code for verification.</span></span> |  |

<span data-ttu-id="65742-224">由于我们已经实现了授权代码授予的授权终结点`OAuthController.Authorize`（操作），因此它会自动启用隐式流。</span><span class="sxs-lookup"><span data-stu-id="65742-224">Since we already implemented the authorization endpoint (`OAuthController.Authorize` action) for authorization code grant, it automatically enables implicit flow as well.</span></span> <span data-ttu-id="65742-225">注意：`Provider.ValidateClientRedirectUri`用于验证客户端 ID 及其重定向 URL，它保护隐式授予流从发送访问令牌到恶意客户端（[中间人攻击](https://www.owasp.org/index.php/Man-in-the-middle_attack)）。</span><span class="sxs-lookup"><span data-stu-id="65742-225">Note: `Provider.ValidateClientRedirectUri` is used to validate the client ID with its redirection URL, which protects the implicit grant flow from sending the access token to malicious clients ([Man-in-the-middle attack](https://www.owasp.org/index.php/Man-in-the-middle_attack)).</span></span>

### <a name="resource-owner-password-credentials-grant"></a><span data-ttu-id="65742-226">资源所有者密码凭据授予</span><span class="sxs-lookup"><span data-stu-id="65742-226">Resource Owner Password Credentials Grant</span></span>

<span data-ttu-id="65742-227">立即请参阅 IETF 的 OAuth 2[资源所有者密码凭据授予](http://tools.ietf.org/html/rfc6749#section-4.3)部分。</span><span class="sxs-lookup"><span data-stu-id="65742-227">Refer to the IETF's OAuth 2 [Resource Owner Password Credentials Grant](http://tools.ietf.org/html/rfc6749#section-4.3) section now.</span></span>

 <span data-ttu-id="65742-228">图 5 所示[的资源所有者密码凭据授予](http://tools.ietf.org/html/rfc6749#section-4.3)流是 OWIN OAuth 中间件后面的流和映射。</span><span class="sxs-lookup"><span data-stu-id="65742-228">The [Resource Owner Password Credentials Grant](http://tools.ietf.org/html/rfc6749#section-4.3) flow shown in Figure 5 is the flow and mapping which the OWIN OAuth middleware follows.</span></span>

| <span data-ttu-id="65742-229">来自资源所有者密码凭据授予部分的流步骤</span><span class="sxs-lookup"><span data-stu-id="65742-229">Flow steps from Resource Owner Password Credentials Grant section</span></span> | <span data-ttu-id="65742-230">示例下载执行以下步骤：</span><span class="sxs-lookup"><span data-stu-id="65742-230">Sample download performs these steps with:</span></span> |
| --- | --- |
|  |  |
| <span data-ttu-id="65742-231">（A） 资源所有者向客户端提供其用户名和密码。</span><span class="sxs-lookup"><span data-stu-id="65742-231">(A) The resource owner provides the client with its username and password.</span></span> |  |
|  |  |
| <span data-ttu-id="65742-232">（B） 客户端通过包含从资源所有者收到的凭据来请求来自授权服务器令牌终结点的访问令牌。</span><span class="sxs-lookup"><span data-stu-id="65742-232">(B) The client requests an access token from the authorization server's token endpoint by including the credentials received from the resource owner.</span></span> <span data-ttu-id="65742-233">发出请求时，客户端会使用授权服务器进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="65742-233">When making the request, the client authenticates with the authorization server.</span></span> | <span data-ttu-id="65742-234">提供程序.匹配终结点提供程序.验证客户端身份验证提供程序.验证令牌请求提供程序.授予资源所有者凭据提供程序.令牌终结点访问令牌提供程序.创建同步刷新令牌提供程序.创建async</span><span class="sxs-lookup"><span data-stu-id="65742-234">Provider.MatchEndpoint Provider.ValidateClientAuthentication Provider.ValidateTokenRequest Provider.GrantResourceOwnerCredentials Provider.TokenEndpoint AccessToken Provider.CreateAsync RefreshTokenProvider.CreateAsync</span></span> |
|  |  |
| <span data-ttu-id="65742-235">（C） 授权服务器对客户端进行身份验证并验证资源所有者凭据，如果有效，则颁发访问令牌。</span><span class="sxs-lookup"><span data-stu-id="65742-235">(C) The authorization server authenticates the client and validates the resource owner credentials, and if valid, issues an access token.</span></span> |  |

<span data-ttu-id="65742-236">下面是`Provider.GrantResourceOwnerCredentials`以下示例实现：</span><span class="sxs-lookup"><span data-stu-id="65742-236">Here is the sample implementation for `Provider.GrantResourceOwnerCredentials`:</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample7.cs)]

> [!NOTE]
> <span data-ttu-id="65742-237">上面的代码旨在解释本教程的这一部分，不应在安全或生产应用中使用。</span><span class="sxs-lookup"><span data-stu-id="65742-237">The code above is intended to explain this section of the tutorial and should not be used in secure or production apps.</span></span> <span data-ttu-id="65742-238">它不检查资源所有者凭据。</span><span class="sxs-lookup"><span data-stu-id="65742-238">It does not check the resource owners credentials.</span></span> <span data-ttu-id="65742-239">它假定每个凭据都有效，并为其创建新标识。</span><span class="sxs-lookup"><span data-stu-id="65742-239">It assumes every credential is valid and creates a new identity for it.</span></span> <span data-ttu-id="65742-240">新标识将用于生成访问令牌和刷新令牌。</span><span class="sxs-lookup"><span data-stu-id="65742-240">The new identity will be used to generate the access token and refresh token.</span></span> <span data-ttu-id="65742-241">请将代码替换为您自己的安全帐户管理代码。</span><span class="sxs-lookup"><span data-stu-id="65742-241">Please replace the code with your own secure account management code.</span></span>


### <a name="client-credentials-grant"></a><span data-ttu-id="65742-242">客户端凭据授予</span><span class="sxs-lookup"><span data-stu-id="65742-242">Client Credentials Grant</span></span>

<span data-ttu-id="65742-243">立即请参阅 IETF 的 OAuth 2[客户端凭据授予](http://tools.ietf.org/html/rfc6749#section-4.4)部分。</span><span class="sxs-lookup"><span data-stu-id="65742-243">Refer to the IETF's OAuth 2 [Client Credentials Grant](http://tools.ietf.org/html/rfc6749#section-4.4) section now.</span></span>

 <span data-ttu-id="65742-244">图 6 所示[的客户端凭据授予](http://tools.ietf.org/html/rfc6749#section-4.4)流是 OWIN OAuth 中间件后面的流和映射。</span><span class="sxs-lookup"><span data-stu-id="65742-244">The [Client Credentials Grant](http://tools.ietf.org/html/rfc6749#section-4.4) flow shown in Figure 6 is the flow and mapping which the OWIN OAuth middleware follows.</span></span>

| <span data-ttu-id="65742-245">来自客户端凭据授予部分的流步骤</span><span class="sxs-lookup"><span data-stu-id="65742-245">Flow steps from Client Credentials Grant section</span></span> | <span data-ttu-id="65742-246">示例下载执行以下步骤：</span><span class="sxs-lookup"><span data-stu-id="65742-246">Sample download performs these steps with:</span></span> |
| --- | --- |
|  |  |
| <span data-ttu-id="65742-247">（A） 客户端使用授权服务器进行身份验证，并从令牌终结点请求访问令牌。</span><span class="sxs-lookup"><span data-stu-id="65742-247">(A) The client authenticates with the authorization server and requests an access token from the token endpoint.</span></span> | <span data-ttu-id="65742-248">提供程序.匹配终结点提供程序.验证客户端身份验证提供程序.验证令牌请求提供程序.授予客户端凭据提供程序.令牌终结点访问令牌提供程序.创建同步刷新令牌提供程序.创建async</span><span class="sxs-lookup"><span data-stu-id="65742-248">Provider.MatchEndpoint Provider.ValidateClientAuthentication Provider.ValidateTokenRequest Provider.GrantClientCredentials Provider.TokenEndpoint AccessTokenProvider.CreateAsync RefreshTokenProvider.CreateAsync</span></span> |
|  |  |
| <span data-ttu-id="65742-249">（B） 授权服务器对客户端进行身份验证，如果有效，则颁发访问令牌。</span><span class="sxs-lookup"><span data-stu-id="65742-249">(B) The authorization server authenticates the client, and if valid, issues an access token.</span></span> |  |

<span data-ttu-id="65742-250">下面是`Provider.GrantClientCredentials`以下示例实现：</span><span class="sxs-lookup"><span data-stu-id="65742-250">Here is the sample implementation for `Provider.GrantClientCredentials`:</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample8.cs)]

> [!NOTE]
> <span data-ttu-id="65742-251">上面的代码旨在解释本教程的这一部分，不应在安全或生产应用中使用。</span><span class="sxs-lookup"><span data-stu-id="65742-251">The code above is intended to explain this section of the tutorial and should not be used in secure or production apps.</span></span> <span data-ttu-id="65742-252">请将代码替换为您自己的安全客户端管理代码。</span><span class="sxs-lookup"><span data-stu-id="65742-252">Please replace the code with your own secure client management code.</span></span>


### <a name="refresh-token"></a><span data-ttu-id="65742-253">刷新令牌</span><span class="sxs-lookup"><span data-stu-id="65742-253">Refresh Token</span></span>

<span data-ttu-id="65742-254">立即请参阅 IETF 的 OAuth 2[刷新令牌](http://tools.ietf.org/html/rfc6749#section-1.5)部分。</span><span class="sxs-lookup"><span data-stu-id="65742-254">Refer to the IETF's OAuth 2 [Refresh Token](http://tools.ietf.org/html/rfc6749#section-1.5) section now.</span></span>

 <span data-ttu-id="65742-255">图 2 所示的[刷新令牌](http://tools.ietf.org/html/rfc6749#section-1.5)流是 OWIN OAuth 中间件后面的流和映射。</span><span class="sxs-lookup"><span data-stu-id="65742-255">The [Refresh Token](http://tools.ietf.org/html/rfc6749#section-1.5) flow shown in Figure 2 is the flow and mapping which the OWIN OAuth middleware follows.</span></span>

| <span data-ttu-id="65742-256">来自客户端凭据授予部分的流步骤</span><span class="sxs-lookup"><span data-stu-id="65742-256">Flow steps from Client Credentials Grant section</span></span> | <span data-ttu-id="65742-257">示例下载执行以下步骤：</span><span class="sxs-lookup"><span data-stu-id="65742-257">Sample download performs these steps with:</span></span> |
| --- | --- |
|  |  |
| <span data-ttu-id="65742-258">（G） 客户端通过使用授权服务器进行身份验证并呈现刷新令牌来请求新的访问令牌。</span><span class="sxs-lookup"><span data-stu-id="65742-258">(G) The client requests a new access token by authenticating with the authorization server and presenting the refresh token.</span></span> <span data-ttu-id="65742-259">客户端身份验证要求基于客户端类型和授权服务器策略。</span><span class="sxs-lookup"><span data-stu-id="65742-259">The client authentication requirements are based on the client type and on the authorization server policies.</span></span> | <span data-ttu-id="65742-260">提供程序.匹配终结点提供程序.验证客户端身份验证刷新令牌提供程序.接收async提供程序.验证令牌请求提供程序.授予refreshtoken提供程序.令牌终结点访问令牌提供程序.创建async刷新令牌提供程序.创建Async</span><span class="sxs-lookup"><span data-stu-id="65742-260">Provider.MatchEndpoint Provider.ValidateClientAuthentication RefreshTokenProvider.ReceiveAsync Provider.ValidateTokenRequest Provider.GrantRefreshToken Provider.TokenEndpoint AccessTokenProvider.CreateAsync RefreshTokenProvider.CreateAsync</span></span> |
|  |  |
| <span data-ttu-id="65742-261">（H） 授权服务器对客户端进行身份验证并验证刷新令牌，如果有效，则颁发新的访问令牌（以及可选为新刷新令牌）。</span><span class="sxs-lookup"><span data-stu-id="65742-261">(H) The authorization server authenticates the client and validates the refresh token, and if valid, issues a new access token (and, optionally, a new refresh token).</span></span> |  |

<span data-ttu-id="65742-262">下面是`Provider.GrantRefreshToken`以下示例实现：</span><span class="sxs-lookup"><span data-stu-id="65742-262">Here is the sample implementation for `Provider.GrantRefreshToken`:</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample9.cs)]

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample10.cs)]

## <a name="create-a-resource-server-which-is-protected-by-access-token"></a><span data-ttu-id="65742-263">创建受访问令牌保护的资源服务器</span><span class="sxs-lookup"><span data-stu-id="65742-263">Create a Resource Server which is protected by Access Token</span></span>

<span data-ttu-id="65742-264">创建空 Web 应用项目并在项目中安装以下包：</span><span class="sxs-lookup"><span data-stu-id="65742-264">Create an empty web app project and install following packages in the project:</span></span>

- <span data-ttu-id="65742-265">微软.AspNet.WebApi.Owin</span><span class="sxs-lookup"><span data-stu-id="65742-265">Microsoft.AspNet.WebApi.Owin</span></span>
- <span data-ttu-id="65742-266">Microsoft.Owin.Host.SystemWeb</span><span class="sxs-lookup"><span data-stu-id="65742-266">Microsoft.Owin.Host.SystemWeb</span></span>
- <span data-ttu-id="65742-267">Microsoft.Owin.Security.OAuth</span><span class="sxs-lookup"><span data-stu-id="65742-267">Microsoft.Owin.Security.OAuth</span></span>

<span data-ttu-id="65742-268">创建启动类并配置身份验证和 Web API。</span><span class="sxs-lookup"><span data-stu-id="65742-268">Create a startup class and configure authentication and Web API.</span></span> <span data-ttu-id="65742-269">请参阅*示例下载中的授权服务器\资源服务器\启动.cs。*</span><span class="sxs-lookup"><span data-stu-id="65742-269">See *AuthorizationServer\ResourceServer\Startup.cs* in the sample download.</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample11.cs)]

<span data-ttu-id="65742-270">请参阅*示例下载中的授权服务器\资源\_服务器\应用启动\启动.Auth.cs。*</span><span class="sxs-lookup"><span data-stu-id="65742-270">See *AuthorizationServer\ResourceServer\App\_Start\Startup.Auth.cs* in the sample download.</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample12.cs)]

<span data-ttu-id="65742-271">请参阅*示例下载中的授权服务器\资源\_服务器\应用启动\启动.WebApi.cs。*</span><span class="sxs-lookup"><span data-stu-id="65742-271">See *AuthorizationServer\ResourceServer\App\_Start\Startup.WebApi.cs* in the sample download.</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample13.cs)]

- <span data-ttu-id="65742-272">`UseCors`方法允许所有域的 CORS。</span><span class="sxs-lookup"><span data-stu-id="65742-272">`UseCors` method allows CORS for all domains.</span></span>
- <span data-ttu-id="65742-273">`UseOAuthBearerAuthentication`方法启用 OAuth 承载令牌身份验证中间件，它将从请求中的授权标头接收和验证无记名令牌。</span><span class="sxs-lookup"><span data-stu-id="65742-273">`UseOAuthBearerAuthentication` method enables OAuth bearer token authentication middleware which will receive and validate bearer token from authorization header in the request.</span></span>
- <span data-ttu-id="65742-274">`Config.SuppressDefaultHostAuthenticaiton`禁止从应用中默认主机经过身份验证的主体，因此在此调用后所有请求都将是匿名的。</span><span class="sxs-lookup"><span data-stu-id="65742-274">`Config.SuppressDefaultHostAuthenticaiton` suppresses default host authenticated principal from the app, therefore all requests will be anonymous after this call.</span></span>
- <span data-ttu-id="65742-275">`HostAuthenticationFilter`仅针对指定的身份验证类型启用身份验证。</span><span class="sxs-lookup"><span data-stu-id="65742-275">`HostAuthenticationFilter` enables authentication just for the specified authentication type.</span></span> <span data-ttu-id="65742-276">在这种情况下，它是承载身份验证类型。</span><span class="sxs-lookup"><span data-stu-id="65742-276">In this case, it's bearer authentication type.</span></span>

<span data-ttu-id="65742-277">为了演示经过身份验证的身份，我们创建了一个 ApiController 来输出当前用户的声明。</span><span class="sxs-lookup"><span data-stu-id="65742-277">In order to demonstrate the authenticated identity, we create an ApiController to output current user's claims.</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample14.cs)]

<span data-ttu-id="65742-278">如果授权服务器和资源服务器不在同一台计算机上，OAuth 中间件将使用不同的计算机密钥来加密和解密承载访问令牌。</span><span class="sxs-lookup"><span data-stu-id="65742-278">If the authorization server and the resource server are not on the same computer, the OAuth middleware will use the different machine keys to encrypt and decrypt bearer access token.</span></span> <span data-ttu-id="65742-279">为了在两个项目之间共享相同的私钥，我们在两个`machinekey`*Web.config*文件中添加相同的设置。</span><span class="sxs-lookup"><span data-stu-id="65742-279">In order to share the same private key between both projects, we add the same `machinekey` setting in both *web.config* files.</span></span>

[!code-xml[Main](owin-oauth-20-authorization-server/samples/sample15.xml?highlight=8-10)]

## <a name="create-oauth-20-clients"></a><span data-ttu-id="65742-280">创建 OAuth 2.0 客户端</span><span class="sxs-lookup"><span data-stu-id="65742-280">Create OAuth 2.0 Clients</span></span>

 <span data-ttu-id="65742-281">我们使用[DotNetOpenAuth.OAuth2.客户端](http://www.nuget.org/packages/DotNetOpenAuth.OAuth2.Client)NuGet 包来简化客户端代码。</span><span class="sxs-lookup"><span data-stu-id="65742-281">We use the [DotNetOpenAuth.OAuth2.Client](http://www.nuget.org/packages/DotNetOpenAuth.OAuth2.Client) NuGet package to simplify the client code.</span></span>

### <a name="authorization-code-grant-client"></a><span data-ttu-id="65742-282">授权代码授予客户端</span><span class="sxs-lookup"><span data-stu-id="65742-282">Authorization Code Grant Client</span></span>

 <span data-ttu-id="65742-283">此客户端是 MVC 应用程序。</span><span class="sxs-lookup"><span data-stu-id="65742-283">This client is an MVC application.</span></span> <span data-ttu-id="65742-284">它将触发授权代码授予流，以便从后端获取访问令牌。</span><span class="sxs-lookup"><span data-stu-id="65742-284">It will trigger an authorization code grant flow to get the access token from backend.</span></span> <span data-ttu-id="65742-285">它有一个页面，如下所示：</span><span class="sxs-lookup"><span data-stu-id="65742-285">It has a single page as shown below:</span></span>

![](owin-oauth-20-authorization-server/_static/image3.png)

- <span data-ttu-id="65742-286">"**授权"** 按钮将浏览器重定向到授权服务器，以通知资源所有者授予对此客户端的访问权限。</span><span class="sxs-lookup"><span data-stu-id="65742-286">The **Authorize** button will redirect browser to the authorization server to notify the resource owner to grant access to this client.</span></span>
- <span data-ttu-id="65742-287">"**刷新**"按钮将使用当前刷新令牌获取新的访问令牌和刷新令牌。</span><span class="sxs-lookup"><span data-stu-id="65742-287">The **Refresh** button will get a new access token and refresh token using the current refresh token.</span></span>
- <span data-ttu-id="65742-288">**"访问受保护资源 API"** 按钮将调用资源服务器获取当前用户的声明数据并在页面上显示这些数据。</span><span class="sxs-lookup"><span data-stu-id="65742-288">The **Access Protected Resource API** button will call the resource server to get current user's claims data and show them on the page.</span></span>

<span data-ttu-id="65742-289">下面是客户端`HomeController`的示例代码。</span><span class="sxs-lookup"><span data-stu-id="65742-289">Here is the sample code of the `HomeController` of the client.</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample16.cs)]

<span data-ttu-id="65742-290">`DotNetOpenAuth`默认情况下需要 SSL。</span><span class="sxs-lookup"><span data-stu-id="65742-290">`DotNetOpenAuth` requires SSL by default.</span></span> <span data-ttu-id="65742-291">由于我们的演示使用 HTTP，您需要在配置文件中添加以下设置：</span><span class="sxs-lookup"><span data-stu-id="65742-291">Since our demo is using HTTP, you need to add following setting in the config file:</span></span>

[!code-xml[Main](owin-oauth-20-authorization-server/samples/sample17.xml?highlight=4-6)]

> [!WARNING]
> <span data-ttu-id="65742-292">安全性 - 切勿在生产应用中禁用 SSL。</span><span class="sxs-lookup"><span data-stu-id="65742-292">Security - Never disable SSL in a production app.</span></span> <span data-ttu-id="65742-293">您的登录凭据现在以明文形式通过网络发送。</span><span class="sxs-lookup"><span data-stu-id="65742-293">Your login credentials are now being sent in clear-text across the wire.</span></span> <span data-ttu-id="65742-294">上面的代码仅用于本地示例调试和探索。</span><span class="sxs-lookup"><span data-stu-id="65742-294">The code above is just for local sample debugging and exploration.</span></span>


### <a name="implicit-grant-client"></a><span data-ttu-id="65742-295">隐式授予客户端</span><span class="sxs-lookup"><span data-stu-id="65742-295">Implicit Grant Client</span></span>

<span data-ttu-id="65742-296">此客户端使用 JavaScript 来：</span><span class="sxs-lookup"><span data-stu-id="65742-296">This client is using JavaScript to:</span></span>

1. <span data-ttu-id="65742-297">打开新窗口并重定向到授权服务器的授权终结点。</span><span class="sxs-lookup"><span data-stu-id="65742-297">Open a new window and redirect to the authorize endpoint of the Authorization Server.</span></span>
2. <span data-ttu-id="65742-298">当 URL 片段重定向回时，从它获取访问令牌。</span><span class="sxs-lookup"><span data-stu-id="65742-298">Get the access token from URL fragments when it redirects back.</span></span>

<span data-ttu-id="65742-299">下图显示了此过程：</span><span class="sxs-lookup"><span data-stu-id="65742-299">The following image shows this process:</span></span>

![](owin-oauth-20-authorization-server/_static/image4.png)

<span data-ttu-id="65742-300">客户端应该有两个页面：一个用于主页，另一个用于回调。下面是*在 Index.cshtml*文件中找到的示例 JavaScript 代码：</span><span class="sxs-lookup"><span data-stu-id="65742-300">The client should have two pages: one for home page and the other for callback.Here is the sample JavaScript code found in the *Index.cshtml* file:</span></span>

[!code-cshtml[Main](owin-oauth-20-authorization-server/samples/sample18.cshtml)]

<span data-ttu-id="65742-301">下面是*SignIn.cshtml*文件中的回调处理代码：</span><span class="sxs-lookup"><span data-stu-id="65742-301">Here is the callback handling code in *SignIn.cshtml* file:</span></span>

[!code-cshtml[Main](owin-oauth-20-authorization-server/samples/sample19.cshtml)]

> [!NOTE]
> <span data-ttu-id="65742-302">最佳做法是将 JavaScript 移动到外部文件，而不是将其嵌入 Razor 标记中。</span><span class="sxs-lookup"><span data-stu-id="65742-302">A best practice is to move the JavaScript to an external file and not embed it with the Razor markup.</span></span> <span data-ttu-id="65742-303">为了保持此示例的简单性，它们已被合并。</span><span class="sxs-lookup"><span data-stu-id="65742-303">To keep this sample simple, they have been combined.</span></span>


### <a name="resource-owner-password-credentials-grant-client"></a><span data-ttu-id="65742-304">资源所有者密码凭据授予客户端</span><span class="sxs-lookup"><span data-stu-id="65742-304">Resource Owner Password Credentials Grant Client</span></span>

<span data-ttu-id="65742-305">我们使用控制台应用程序来演示此客户端。</span><span class="sxs-lookup"><span data-stu-id="65742-305">We uses a console app to demo this client.</span></span> <span data-ttu-id="65742-306">代码如下：</span><span class="sxs-lookup"><span data-stu-id="65742-306">Here is the code:</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample20.cs)]

### <a name="client-credentials-grant-client"></a><span data-ttu-id="65742-307">客户端凭据授予客户端</span><span class="sxs-lookup"><span data-stu-id="65742-307">Client Credentials Grant Client</span></span>

<span data-ttu-id="65742-308">与资源所有者密码凭据授予类似，下面是控制台应用代码：</span><span class="sxs-lookup"><span data-stu-id="65742-308">Similar to the Resource Owner Password Credentials Grant, here is console app code:</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample21.cs)]

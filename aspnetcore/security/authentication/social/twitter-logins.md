---
title: Twitter 外部登录名与 ASP.NET Core 的安装程序
author: rick-anderson
description: 本教程演示的集成到现有的 ASP.NET Core 应用的 Twitter 帐户用户身份验证。
ms.author: riande
ms.custom: mvc
ms.date: 11/11/2018
uid: security/authentication/twitter-logins
ms.openlocfilehash: 49db8b921fde169380ca284f46e535786b2b8a30
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57055944"
---
# <a name="twitter-external-login-setup-with-aspnet-core"></a><span data-ttu-id="f4267-103">Twitter 外部登录名与 ASP.NET Core 的安装程序</span><span class="sxs-lookup"><span data-stu-id="f4267-103">Twitter external login setup with ASP.NET Core</span></span>

<span data-ttu-id="f4267-104">作者：[Valeriy Novytskyy](https://github.com/01binary) 和 [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="f4267-104">By [Valeriy Novytskyy](https://github.com/01binary) and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="f4267-105">本教程演示如何启用到你的用户[使用 Twitter 帐户登录](https://dev.twitter.com/web/sign-in/desktop-browser)上使用示例 ASP.NET Core 2.0 项目创建[上一页](xref:security/authentication/social/index)。</span><span class="sxs-lookup"><span data-stu-id="f4267-105">This tutorial shows you how to enable your users to [sign in with their Twitter account](https://dev.twitter.com/web/sign-in/desktop-browser) using a sample ASP.NET Core 2.0 project created on the [previous page](xref:security/authentication/social/index).</span></span>

## <a name="create-the-app-in-twitter"></a><span data-ttu-id="f4267-106">在 Twitter 中创建应用程序</span><span class="sxs-lookup"><span data-stu-id="f4267-106">Create the app in Twitter</span></span>

* <span data-ttu-id="f4267-107">导航到[ https://apps.twitter.com/ ](https://apps.twitter.com/)并登录。</span><span class="sxs-lookup"><span data-stu-id="f4267-107">Navigate to [https://apps.twitter.com/](https://apps.twitter.com/) and sign in.</span></span> <span data-ttu-id="f4267-108">如果还没有 Twitter 帐户，使用 **[立即注册](https://twitter.com/signup)** 链接创建一个链接。</span><span class="sxs-lookup"><span data-stu-id="f4267-108">If you don't already have a Twitter account, use the **[Sign up now](https://twitter.com/signup)** link to create one.</span></span> <span data-ttu-id="f4267-109">登录后，**应用程序管理**页所示：</span><span class="sxs-lookup"><span data-stu-id="f4267-109">After signing in, the **Application Management** page is shown:</span></span>

  ![在 Microsoft Edge 中打开 twitter 应用程序管理](index/_static/TwitterAppManage.png)

* <span data-ttu-id="f4267-111">点击**创建新的应用程序**，应用程序中填写**名称**，**说明**和公共**网站**URI （可以是临时直到注册的域名）：</span><span class="sxs-lookup"><span data-stu-id="f4267-111">Tap **Create New App** and fill out the application **Name**, **Description** and public **Website** URI (this can be temporary until you register the domain name):</span></span>

  ![创建应用程序页](index/_static/TwitterCreate.png)

* <span data-ttu-id="f4267-113">输入你的开发 URI 与`/signin-twitter`追加到**有效的 OAuth 重定向 Uri**字段 (例如： `https://localhost:44320/signin-twitter`)。</span><span class="sxs-lookup"><span data-stu-id="f4267-113">Enter your development URI with `/signin-twitter` appended into the **Valid OAuth Redirect URIs** field (for example: `https://localhost:44320/signin-twitter`).</span></span> <span data-ttu-id="f4267-114">本教程中稍后配置 Twitter 身份验证方案将自动处理在请求`/signin-twitter`路由实现 OAuth 流。</span><span class="sxs-lookup"><span data-stu-id="f4267-114">The Twitter authentication scheme configured later in this tutorial will automatically handle requests at `/signin-twitter` route to implement the OAuth flow.</span></span>

  > [!NOTE]
  > <span data-ttu-id="f4267-115">URI 段`/signin-twitter`设置为 Twitter 身份验证提供程序的默认回调。</span><span class="sxs-lookup"><span data-stu-id="f4267-115">The URI segment `/signin-twitter` is set as the default callback of the Twitter authentication provider.</span></span> <span data-ttu-id="f4267-116">配置 Twitter 身份验证中间件通过继承时，可以更改默认的回调 URI [RemoteAuthenticationOptions.CallbackPath](/dotnet/api/microsoft.aspnetcore.authentication.remoteauthenticationoptions.callbackpath)的属性[TwitterOptions](/dotnet/api/microsoft.aspnetcore.authentication.twitter.twitteroptions)类。</span><span class="sxs-lookup"><span data-stu-id="f4267-116">You can change the default callback URI while configuring the Twitter authentication middleware via the inherited [RemoteAuthenticationOptions.CallbackPath](/dotnet/api/microsoft.aspnetcore.authentication.remoteauthenticationoptions.callbackpath) property of the [TwitterOptions](/dotnet/api/microsoft.aspnetcore.authentication.twitter.twitteroptions) class.</span></span>

* <span data-ttu-id="f4267-117">填写窗体的其余部分，然后点击**创建 Twitter 应用程序**。</span><span class="sxs-lookup"><span data-stu-id="f4267-117">Fill out the rest of the form and tap **Create your Twitter application**.</span></span> <span data-ttu-id="f4267-118">显示新的应用程序详细信息：</span><span class="sxs-lookup"><span data-stu-id="f4267-118">New application details are displayed:</span></span>

  ![应用程序页上的详细信息选项卡](index/_static/TwitterAppDetails.png)

* <span data-ttu-id="f4267-120">部署站点时将需要重新访问**应用程序管理**页上，并注册一个新的公共 URI。</span><span class="sxs-lookup"><span data-stu-id="f4267-120">When deploying the site you'll need to revisit the **Application Management** page and register a new public URI.</span></span>

## <a name="storing-twitter-consumerkey-and-consumersecret"></a><span data-ttu-id="f4267-121">存储 Twitter ConsumerKey 和 ConsumerSecret</span><span class="sxs-lookup"><span data-stu-id="f4267-121">Storing Twitter ConsumerKey and ConsumerSecret</span></span>

<span data-ttu-id="f4267-122">链接敏感设置，例如 Twitter`Consumer Key`并`Consumer Secret`到应用程序的配置使用[机密管理器](xref:security/app-secrets)。</span><span class="sxs-lookup"><span data-stu-id="f4267-122">Link sensitive settings like Twitter `Consumer Key` and `Consumer Secret` to your application configuration using the [Secret Manager](xref:security/app-secrets).</span></span> <span data-ttu-id="f4267-123">对于本教程的目的，命名为令牌`Authentication:Twitter:ConsumerKey`和`Authentication:Twitter:ConsumerSecret`。</span><span class="sxs-lookup"><span data-stu-id="f4267-123">For the purposes of this tutorial, name the tokens `Authentication:Twitter:ConsumerKey` and `Authentication:Twitter:ConsumerSecret`.</span></span>

<span data-ttu-id="f4267-124">这些令牌可在**密钥和访问令牌**选项卡后创建新的 Twitter 应用程序：</span><span class="sxs-lookup"><span data-stu-id="f4267-124">These tokens can be found on the **Keys and Access Tokens** tab after creating your new Twitter application:</span></span>

![密钥和访问令牌的选项卡](index/_static/TwitterKeys.png)

## <a name="configure-twitter-authentication"></a><span data-ttu-id="f4267-126">配置 Twitter 身份验证</span><span class="sxs-lookup"><span data-stu-id="f4267-126">Configure Twitter Authentication</span></span>

<span data-ttu-id="f4267-127">在本教程中使用的项目模板可确保[Microsoft.AspNetCore.Authentication.Twitter](https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.Twitter)包已安装。</span><span class="sxs-lookup"><span data-stu-id="f4267-127">The project template used in this tutorial ensures that [Microsoft.AspNetCore.Authentication.Twitter](https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.Twitter) package is already installed.</span></span>

* <span data-ttu-id="f4267-128">若要使用 Visual Studio 2017 中安装此包，请右键单击项目并选择**管理 NuGet 包**。</span><span class="sxs-lookup"><span data-stu-id="f4267-128">To install this package with Visual Studio 2017, right-click on the project and select **Manage NuGet Packages**.</span></span>
* <span data-ttu-id="f4267-129">若要使用.NET Core CLI 安装，请在项目目录中执行以下命令：</span><span class="sxs-lookup"><span data-stu-id="f4267-129">To install with .NET Core CLI, execute the following in your project directory:</span></span>

  `dotnet add package Microsoft.AspNetCore.Authentication.Twitter`

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="f4267-130">将 Twitter 服务中的添加`ConfigureServices`中的方法*Startup.cs*文件：</span><span class="sxs-lookup"><span data-stu-id="f4267-130">Add the Twitter service in the `ConfigureServices` method in *Startup.cs* file:</span></span>

```csharp
services.AddDefaultIdentity<IdentityUser>()
        .AddDefaultUI(UIFramework.Bootstrap4)
        .AddEntityFrameworkStores<ApplicationDbContext>();

services.AddAuthentication().AddTwitter(twitterOptions =>
{
    twitterOptions.ConsumerKey = Configuration["Authentication:Twitter:ConsumerKey"];
    twitterOptions.ConsumerSecret = Configuration["Authentication:Twitter:ConsumerSecret"];
});
```

[!INCLUDE [default settings configuration](includes/default-settings.md)]

[!INCLUDE[](includes/chain-auth-providers.md)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="f4267-131">添加中的 Twitter 中间件`Configure`中的方法*Startup.cs*文件：</span><span class="sxs-lookup"><span data-stu-id="f4267-131">Add the Twitter middleware in the `Configure` method in *Startup.cs* file:</span></span>

```csharp
app.UseTwitterAuthentication(new TwitterOptions()
{
    ConsumerKey = Configuration["Authentication:Twitter:ConsumerKey"],
    ConsumerSecret = Configuration["Authentication:Twitter:ConsumerSecret"]
});
```

::: moniker-end

<span data-ttu-id="f4267-132">请参阅[TwitterOptions](/dotnet/api/microsoft.aspnetcore.builder.twitteroptions) Twitter 身份验证支持的配置选项的详细信息的 API 参考。</span><span class="sxs-lookup"><span data-stu-id="f4267-132">See the [TwitterOptions](/dotnet/api/microsoft.aspnetcore.builder.twitteroptions) API reference for more information on configuration options supported by Twitter authentication.</span></span> <span data-ttu-id="f4267-133">这可以用于请求有关用户的不同信息。</span><span class="sxs-lookup"><span data-stu-id="f4267-133">This can be used to request different information about the user.</span></span>

## <a name="sign-in-with-twitter"></a><span data-ttu-id="f4267-134">使用 Twitter 登录</span><span class="sxs-lookup"><span data-stu-id="f4267-134">Sign in with Twitter</span></span>

<span data-ttu-id="f4267-135">运行你的应用程序，然后单击**登录**。</span><span class="sxs-lookup"><span data-stu-id="f4267-135">Run your application and click **Log in**.</span></span> <span data-ttu-id="f4267-136">通过 Twitter 进行登录的选项将显示：</span><span class="sxs-lookup"><span data-stu-id="f4267-136">An option to sign in with Twitter appears:</span></span>

![Web 应用程序：用户未经过身份验证](index/_static/DoneTwitter.png)

<span data-ttu-id="f4267-138">单击**Twitter**将重定向到 Twitter 进行身份验证：</span><span class="sxs-lookup"><span data-stu-id="f4267-138">Clicking on **Twitter** redirects to Twitter for authentication:</span></span>

![Twitter 身份验证页面](index/_static/TwitterLogin.png)

<span data-ttu-id="f4267-140">输入你的 Twitter 凭据后，你将重定向回 web 站点，你可以设置你的电子邮件。</span><span class="sxs-lookup"><span data-stu-id="f4267-140">After entering your Twitter credentials, you are redirected back to the web site where you can set your email.</span></span>

<span data-ttu-id="f4267-141">现在已在使用你的 Twitter 凭据进行登录：</span><span class="sxs-lookup"><span data-stu-id="f4267-141">You are now logged in using your Twitter credentials:</span></span>

![Web 应用程序：用户通过身份验证](index/_static/Done.png)

[!INCLUDE[Forward request information when behind a proxy or load balancer section](includes/forwarded-headers-middleware.md)]

## <a name="troubleshooting"></a><span data-ttu-id="f4267-143">疑难解答</span><span class="sxs-lookup"><span data-stu-id="f4267-143">Troubleshooting</span></span>

* <span data-ttu-id="f4267-144">**ASP.NET Core 仅限 2.x:** 如果不通过调用配置标识`services.AddIdentity`中`ConfigureServices`，尝试进行身份验证将导致*ArgumentException:必须提供 SignInScheme 选项*。</span><span class="sxs-lookup"><span data-stu-id="f4267-144">**ASP.NET Core 2.x only:** If Identity isn't configured by calling `services.AddIdentity` in `ConfigureServices`, attempting to authenticate will result in *ArgumentException: The 'SignInScheme' option must be provided*.</span></span> <span data-ttu-id="f4267-145">在本教程中使用的项目模板可确保，此操作。</span><span class="sxs-lookup"><span data-stu-id="f4267-145">The project template used in this tutorial ensures that this is done.</span></span>
* <span data-ttu-id="f4267-146">如果尚未通过应用初始迁移创建站点数据库，则会收到*处理请求时，数据库操作失败*错误。</span><span class="sxs-lookup"><span data-stu-id="f4267-146">If the site database has not been created by applying the initial migration, you will get *A database operation failed while processing the request* error.</span></span> <span data-ttu-id="f4267-147">点击**应用迁移**创建数据库，并刷新以忽略错误继续。</span><span class="sxs-lookup"><span data-stu-id="f4267-147">Tap **Apply Migrations** to create the database and refresh to continue past the error.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f4267-148">后续步骤</span><span class="sxs-lookup"><span data-stu-id="f4267-148">Next steps</span></span>

* <span data-ttu-id="f4267-149">本文介绍了您如何可以使用 Twitter 进行验证。</span><span class="sxs-lookup"><span data-stu-id="f4267-149">This article showed how you can authenticate with Twitter.</span></span> <span data-ttu-id="f4267-150">可以遵循类似的方法来使用上列出其他提供程序进行身份验证[上一页](xref:security/authentication/social/index)。</span><span class="sxs-lookup"><span data-stu-id="f4267-150">You can follow a similar approach to authenticate with other providers listed on the [previous page](xref:security/authentication/social/index).</span></span>

* <span data-ttu-id="f4267-151">一旦您将您的网站发布到 Azure web 应用时，应重置`ConsumerSecret`Twitter 开发人员门户中。</span><span class="sxs-lookup"><span data-stu-id="f4267-151">Once you publish your web site to Azure web app, you should reset the `ConsumerSecret` in the Twitter developer portal.</span></span>

* <span data-ttu-id="f4267-152">设置`Authentication:Twitter:ConsumerKey`和`Authentication:Twitter:ConsumerSecret`作为在 Azure 门户中的应用程序设置。</span><span class="sxs-lookup"><span data-stu-id="f4267-152">Set the `Authentication:Twitter:ConsumerKey` and `Authentication:Twitter:ConsumerSecret` as application settings in the Azure portal.</span></span> <span data-ttu-id="f4267-153">配置系统设置以从环境变量读取密钥。</span><span class="sxs-lookup"><span data-stu-id="f4267-153">The configuration system is set up to read keys from environment variables.</span></span>

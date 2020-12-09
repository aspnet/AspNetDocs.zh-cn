---
uid: identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity
title: '帐户确认 & 密码恢复-ASP.NET Identity (c # ) -ASP.NET 4。x'
author: HaoK
description: 在学习本教程之前，应先完成创建具有登录、电子邮件确认和密码重置的安全 ASP.NET MVC 5 web 应用。 本教程 .。。
ms.author: riande
ms.date: 01/23/2019
ms.assetid: 8d54180d-f826-4df7-b503-7debf5ed9fb3
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity
msc.type: authoredcontent
ms.openlocfilehash: e27d9180bf8da3572b48cb342be4e703f093d45a
ms.sourcegitcommit: 6727454a30f11ac2365e1cc8a37ef0005f5d15b3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/09/2020
ms.locfileid: "96934105"
---
# <a name="account-confirmation-and-password-recovery-with-aspnet-identity-c"></a> (c # 的 ASP.NET Identity 帐户确认和密码恢复 ) 

> 在学习本教程之前，应先完成 [创建具有登录、电子邮件确认和密码重置的安全 ASP.NET MVC 5 web 应用](../../../mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md)。 本教程包含更多详细信息，并演示如何设置电子邮件以进行本地帐户确认，并使用户能够在 ASP.NET Identity 中重置其忘记的密码。

本地用户帐户要求用户为该帐户创建密码，并且该密码 (在 web 应用中安全) 存储。 ASP.NET Identity 还支持社交帐户，这不需要用户为应用创建密码。 [社交帐户](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) 使用第三方 (（如 Google、Twitter、Facebook 或 Microsoft) ）对用户进行身份验证。 本主题涵盖以下内容：

- [创建 ASP.NET MVC 应用](#createMvc) 并浏览 ASP.NET Identity 功能。
- [构建标识示例](#build)
- [设置电子邮件确认](#email)

新用户注册其电子邮件别名，这会创建一个本地帐户。

![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image1.png)

选择 "注册" 按钮会向电子邮件地址发送一封包含验证令牌的确认电子邮件。

![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image2.png)

向用户发送一封电子邮件，其中包含其帐户的确认令牌。

![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image3.png)

选择该链接即可确认帐户。

![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image4.png)

<a id="passwordReset"></a>

## <a name="password-recoveryreset"></a>密码恢复/重置

忘记密码的本地用户可以将安全令牌发送到其电子邮件帐户，从而使他们能够重置其密码。  
  
![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image5.png)  
  
用户很快会收到一封电子邮件，其中包含允许用户重置其密码的链接。  
  
![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image6.png)  
选择该链接会将其转到重置页面。  
  
![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image7.png)  
  
选择 " **重置** " 按钮将确认密码已重置。  
  
![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image8.png)

<a id="createMvc"></a>

## <a name="create-an-aspnet-web-app"></a>创建 ASP.NET Web 应用

首先，安装并运行 [Visual Studio 2017](https://visualstudio.microsoft.com/)。

1. 创建新的 ASP.NET Web 项目，并选择 MVC 模板。 Web 窗体还支持 ASP.NET Identity，因此你可以按照 web 窗体应用程序中的类似步骤进行操作。
2. 更改 **单独用户帐户** 的身份验证。
3. 运行应用，选择 " **注册** " 链接并注册用户。 此时，电子邮件的唯一验证是带有 [[EmailAddress]](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.emailaddressattribute(v=vs.110).aspx) 属性。
4. 在服务器资源管理器中，导航到 " **数据 Connections\DefaultConnection\Tables\AspNetUsers**"，右键单击并选择 " **打开表定义**"。

    下图显示了该 `AspNetUsers` 架构：

    ![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image9.png)
5. 右键单击 **AspNetUsers** 表，然后选择 " **显示表数据**"。  
  
    ![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image10.png)  
  
   此时，尚未确认电子邮件。

ASP.NET Identity 的默认数据存储实体框架，但你可以将其配置为使用其他数据存储并添加其他字段。 请参阅本教程末尾的 [其他资源](#addRes) 部分。

当应用程序启动时，将调用 [OWIN startup 类](../../../aspnet/overview/owin-and-katana/owin-startup-class-detection.md) ( *Startup.cs* ) ，并调用 `ConfigureAuth` *app \_ Start\Startup.Auth.cs* 中的方法，该方法配置 OWIN 管道并初始化 ASP.NET Identity。 检查 `ConfigureAuth` 方法。 每个 `CreatePerOwinContext` 调用都注册一个回调 (保存在 `OwinContext`) 中，每次请求将调用该回调来创建指定类型的实例。 您可以在每个类型的构造函数和方法中设置一个断点 `Create` (`ApplicationDbContext, ApplicationUserManager`) 并验证每个请求的调用。 和的实例 `ApplicationDbContext` `ApplicationUserManager` 存储在 OWIN 上下文中，该上下文可在整个应用程序中访问。 通过 cookie 中间件 ASP.NET Identity 挂钩到 OWIN 管道。 有关详细信息，请参阅 [ASP.NET Identity 中的针对 UserManager 类的每个请求生存期管理](https://blogs.msdn.com/b/webdev/archive/2014/02/12/per-request-lifetime-management-for-usermanager-class-in-asp-net-identity.aspx)。

更改安全配置文件时，会生成新的安全戳，并将其存储在 `SecurityStamp` *AspNetUsers* 表的字段中。 请注意，该 `SecurityStamp` 字段不同于安全 cookie。 安全 cookie 不会存储在表中 `AspNetUsers` (或标识 DB) 中的任何其他位置。 安全 cookie 令牌使用 [DPAPI](https://msdn.microsoft.com/library/system.security.cryptography.protecteddata.aspx) 自签名，并使用 `UserId, SecurityStamp` 和过期时间信息进行创建。

Cookie 中间件检查每个请求的 cookie。 `SecurityStampValidator`类中的方法会 `Startup` 按指定的顺序命中数据库并定期检查安全标记 `validateInterval` 。 这只会在示例) 中每30分钟发生一次 (除非更改了安全配置文件。 选择了30分钟间隔，以最大程度地减少对数据库的行程。 有关更多详细信息，请参阅我的 [双因素身份验证教程](index.md) 。

根据代码中的注释，此 `UseCookieAuthentication` 方法支持 cookie 身份验证。 此 `SecurityStamp` 字段和关联代码为应用程序提供了额外的安全层，当你更改密码时，你将从使用登录的浏览器中注销。 此 `SecurityStampValidator.OnValidateIdentity` 方法使应用程序能够在用户登录时验证安全令牌，当你更改密码或使用外部登录时，将使用该令牌。 这是为了确保通过旧密码 (cookie) 生成的任何令牌失效。 在示例项目中，如果更改用户密码，则会为用户生成一个新的令牌，任何以前的令牌都会失效，并 `SecurityStamp` 更新字段。

标识系统允许配置应用，以便在用户的安全配置文件发生更改时 (例如，当用户更改其密码或更改关联登录名 (例如 Facebook、Google、) Microsoft 帐户等）时，用户将从所有浏览器实例中注销。 例如，下面的图像显示了 [单个 signout 示例](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/SingleSignOutSample) 应用程序，该应用程序允许用户通过选择一个按钮，从) 的所有浏览器实例中注销 (。 此外，该示例还允许您仅注销特定的浏览器实例。

![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image11.png)

[单个 signout 示例](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/SingleSignOutSample)应用程序演示了 ASP.NET Identity 如何允许您重新生成安全令牌。 这是为了确保通过旧密码 (cookie) 生成的任何令牌失效。 此功能为应用程序提供了额外的安全层;当你更改密码时，你将被注销，你已登录到此应用程序。

*App \_ Start\IdentityConfig.cs* 文件包含 `ApplicationUserManager` 、 `EmailService` 和 `SmsService` 类。 `EmailService`和 `SmsService` 类分别实现 `IIdentityMessageService` 接口，因此，每个类中都有一些用于配置电子邮件和短信的常用方法。 虽然本教程仅介绍了如何通过 [SendGrid](http://sendgrid.com/)添加电子邮件通知，但你可以使用 SMTP 和其他机制发送电子邮件。

此 `Startup` 类还包含样板板式 (Facebook、twitter 等 ) 上添加社会登录名、有关详细信息，请参阅我 [的教程5应用，并提供 Facebook、Twitter、LinkedIn 和 Google OAuth2 登录](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) 。

检查 `ApplicationUserManager` 类，该类包含用户标识信息并配置以下功能：

- 密码强度要求。
- 用户锁定 (尝试和时间) 。
- 双因素身份验证 (2FA) 。 我将在另一个教程中介绍2FA 和 SMS。
- 挂接电子邮件和 SMS 服务。  (我将在另一个教程) 中介绍短信。

`ApplicationUserManager`类派生自泛型 `UserManager<ApplicationUser>` 类。 `ApplicationUser` 派生自 [IdentityUser](https://msdn.microsoft.com/library/microsoft.aspnet.identity.entityframework.identityuser.aspx)。 `IdentityUser` 派生自泛型 `IdentityUser` 类：

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample1.cs)]

上面所示的属性与表中的属性一致 `AspNetUsers` 。

上的泛型参数 `IUser` 使你能够使用不同的主键类型来派生类。 请参阅 [ChangePK](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/ChangePK) 示例，该示例演示如何将主密钥从 string 更改为 INT 或 GUID。

### <a name="applicationuser"></a>ApplicationUser

`ApplicationUser` (`public class ApplicationUserManager : UserManager<ApplicationUser>`) 在 *Models\IdentityModels.cs* 中定义为：

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample2.cs?highlight=8-9)]

上面突出显示的代码生成 [ClaimsIdentity](https://msdn.microsoft.com/library/system.security.claims.claimsidentity.aspx)。 ASP.NET Identity 和 OWIN Cookie 身份验证是基于声明的，因此框架要求应用为 `ClaimsIdentity` 用户生成。 `ClaimsIdentity` 包含有关用户的所有声明的信息，如用户的姓名、年龄和用户所属的角色。 你还可以在此阶段为用户添加更多声明。

OWIN `AuthenticationManager.SignIn` 方法传入 `ClaimsIdentity` 用户的和签名：

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample3.cs?highlight=4-6)]

[带有 Facebook、Twitter、LinkedIn 和 Google OAuth2 登录的 MVC 5 应用](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) 显示了如何将其他属性添加到 `ApplicationUser` 类。

## <a name="email-confirmation"></a>电子邮件确认

最好确认电子邮件中新用户注册的电子邮件，以验证他们是否未模拟其他人 (也就是说，他们并未注册其他人的电子邮件) 。 假设你有一个论坛，你可能想要阻止 `"bob@example.com"` 注册为 `"joe@contoso.com"` 。 如果未确认电子邮件， `"joe@contoso.com"` 可能会从你的应用收到不需要的电子邮件。 假设 Bob 偶然注册为 `"bib@example.com"` ，未注意到，他无法使用密码恢复，因为该应用没有正确的电子邮件。 电子邮件确认仅提供对 bot 的有限保护，不提供对已确定垃圾邮件发送者的保护，它们具有可用于注册的许多工作电子邮件别名。在下面的示例中，用户将无法更改其密码，除非他们选择了在其注册的电子邮件帐户上收到的确认链接 (。 ) 你可以将此工作流应用于其他方案，例如发送链接以确认并重置管理员创建的新帐户的密码，并在用户更改其配置文件后向用户发送电子邮件。 通常，在通过电子邮件、短信或其他机制确认新用户之前，要阻止新用户将任何数据发布到您的网站。 <a id="build"></a>

## <a name="build-a-more-complete-sample"></a>生成更完整的示例

在本部分中，你将使用 NuGet 下载我们将使用的更完整的示例。

1. 创建新的 ***empty** _ ASP.NET Web 项目。
2. 在 "程序包管理器控制台" 中，输入以下命令： 

    [!code-console[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample4.cmd)]

   在本教程中，我们将使用 [SendGrid](http://sendgrid.com/) 发送电子邮件。 `Identity.Samples`包将安装要使用的代码。
3. 将 [项目设置为使用 SSL](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)。
4. 通过运行应用程序，选择 _ *注册** 链接并发布注册窗体，来测试本地帐户创建。
5. 选择 "演示电子邮件" 链接，该链接模拟电子邮件确认。
6. 从示例 (`ViewBag.Link` 帐户控制器中的代码中删除演示电子邮件链接确认代码。 请参阅 `DisplayEmail` 和 `ForgotPasswordConfirmation` 操作方法和 razor 视图 ) 。

> [!WARNING]
> 如果更改此示例中的任何安全设置，则生产应用将需要进行安全审核，以显式调用所做的更改。

## <a name="examine-the-code-in-app_startidentityconfigcs"></a>检查应用 Start\IdentityConfig.cs 中的代码 \_

此示例演示如何创建帐户并将其添加到 *管理员* 角色。 应该将示例中的电子邮件替换为要用于管理员帐户的电子邮件。 在方法中以编程方式创建管理员帐户的最简单方法 `Seed` 。 我们希望在将来使用一种工具来创建和管理用户和角色。 示例代码允许您创建和管理用户和角色，但您必须首先使用管理员帐户来运行角色和用户管理页面。 在此示例中，在对数据库进行种子设定时，将创建管理员帐户。

更改密码，并将名称更改为可接收电子邮件通知的帐户。

> [!WARNING]
> 安全性-永远不要将敏感数据存储在源代码中。

如前所述， `app.CreatePerOwinContext` startup 类中的调用会将回调添加到 `Create` 应用数据库内容、用户管理器和角色管理器类的方法。 OWIN 管道对 `Create` 每个请求的这些类调用方法，并存储每个类的上下文。 帐户控制器通过 HTTP 上下文公开用户管理器 (其中包含 OWIN 上下文) ：

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample5.cs)]

当用户注册本地帐户时，将 `HTTP Post Register` 调用方法：

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample6.cs)]

上面的代码使用模型数据，通过输入的电子邮件和密码来创建新的用户帐户。 如果电子邮件别名在数据存储中，则帐户创建将失败，并再次显示表单。 `GenerateEmailConfirmationTokenAsync`方法创建一个安全确认令牌并将其存储在 ASP.NET Identity 的数据存储中。 [Url。 Action](https://msdn.microsoft.com/library/dd505232(v=vs.118).aspx)方法创建包含 `UserId` 和确认令牌的链接。 然后，可以通过电子邮件向用户发送此链接，用户可以在其电子邮件应用的链接上选择，以确认其帐户。

<a id="email"></a>

## <a name="set-up-email-confirmation"></a>设置电子邮件确认

请参阅 SendGrid 注册页面并注册免费帐户。 添加类似于下面的代码以配置 SendGrid：

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample7.cs?highlight=5)]

> [!NOTE]
> 电子邮件客户端通常只接受 (没有 HTML) 的短信。 应提供文本和 HTML 格式的消息。 在上面的 SendGrid 示例中，此操作是通过 `myMessage.Text` 上面显示的和代码完成的 `myMessage.Html` 。

下面的代码演示如何使用 [send-mailmessage](https://msdn.microsoft.com/library/system.net.mail.mailmessage.aspx) 类发送电子邮件，其中 `message.Body` 仅返回链接。

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample8.cs)]

> [!WARNING]
> 安全性-永远不要将敏感数据存储在源代码中。 帐户和凭据存储在 appSetting 中。 在 Azure 上，可以将这些值安全地存储在 Azure 门户中的 " **[配置](https://blogs.msdn.com/b/webdev/archive/2014/06/04/queuebackgroundworkitem-to-reliably-schedule-and-run-long-background-process-in-asp-net.aspx)** " 选项卡上。 请参阅 [将密码和其他敏感数据部署到 ASP.NET 和 Azure 的最佳做法](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)。

输入你的 SendGrid 凭据，运行应用，使用电子邮件别名进行注册可以选择电子邮件中的 "确认" 链接。 若要查看如何通过 [Outlook.com](http://outlook.com) 电子邮件帐户执行此操作，请参阅 John Atten 的 [c # smtp CONFIGURATION For Outlook.Com SMTP Host](http://typecastexception.com/post/2013/12/20/C-SMTP-Configuration-for-OutlookCom-SMTP-Host.aspx) 和他的[ASP.NET Identity 2.0：设置帐户验证和 Two-Factor 授权](http://typecastexception.com/post/2014/04/20/ASPNET-Identity-20-Setting-Up-Account-Validation-and-Two-Factor-Authorization.aspx) 文章。

用户选择 " **注册** " 按钮后，将会向电子邮件地址发送一封包含验证令牌的确认电子邮件。

![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image12.png)

向用户发送一封电子邮件，其中包含其帐户的确认令牌。

![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image13.png)

## <a name="examine-the-code"></a>检查代码

以下代码演示了 `POST ForgotPassword` 方法。

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample9.cs)]

如果未确认用户电子邮件，则该方法将以无提示方式失败。 如果针对无效电子邮件地址发布了错误，恶意用户可以使用该信息来查找有效的 userId (电子邮件别名) 攻击。

下面的代码显示 `ConfirmEmail` 帐户控制器中的方法，当用户在发送给他们的电子邮件中选择确认链接时，将调用该方法：

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample10.cs)]

使用忘记的密码令牌后，它会失效。 `Create` (*应用 \_ Start\IdentityConfig.cs* 文件中的方法中的以下代码更改) 将令牌设置为3小时后过期。

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample11.cs?highlight=6-8)]

在上面的代码中，忘记的密码和电子邮件确认令牌将在3小时后过期。 默认值 `TokenLifespan` 为一天。

以下代码显示电子邮件确认方法：

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample12.cs)]

 为了使应用更安全，ASP.NET Identity 支持 Two-Factor 身份验证 (2FA) 。 请参阅 [ASP.NET Identity 2.0：设置帐户验证和 Two-Factor](http://typecastexception.com/post/2014/04/20/ASPNET-Identity-20-Setting-Up-Account-Validation-and-Two-Factor-Authorization.aspx) John Atten 授权。 虽然你可以在登录密码尝试失败时设置帐户锁定，但该方法会使你的登录容易受到 [DOS](http://en.wikipedia.org/wiki/Denial-of-service_attack) 锁定。 建议仅将帐户锁定用于2FA。  
<a id="addRes"></a>

## <a name="additional-resources"></a>其他资源

- [ASP.NET Identity 的自定义存储提供程序概述](../extensibility/overview-of-custom-storage-providers-for-aspnet-identity.md)
- [带有 Facebook、Twitter、LinkedIn 和 Google OAuth2 登录的 MVC 5 应用程序](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) 还演示如何将配置文件信息添加到用户表中。
- [ASP.NET MVC 和 Identity 2.0：了解 John Atten 的基础知识](http://typecastexception.com/post/2014/04/20/ASPNET-MVC-and-Identity-20-Understanding-the-Basics.aspx) 。
- [ASP.NET Identity 简介](../getting-started/introduction-to-aspnet-identity.md)
- [公告 ASP.NET Identity 2.0.0](https://blogs.msdn.com/b/webdev/archive/2014/03/20/test-announcing-rtm-of-asp-net-identity-2-0-0.aspx) By Pranav RASTOGI 撰写的 RTM。

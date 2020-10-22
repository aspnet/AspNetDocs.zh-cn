---
uid: mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on
title: '通过 Facebook、Twitter、LinkedIn 和 Google OAuth2 登录 (c # ) 创建 MVC 5 应用程序 |Microsoft Docs'
author: Rick-Anderson
description: 本教程演示如何生成一个 ASP.NET MVC 5 web 应用程序，该应用程序使用户能够使用带有外部身份的凭据的 OAuth 2.0 登录 .。。
ms.author: riande
ms.date: 04/03/2015
ms.assetid: 81ee500f-fc37-40d6-8722-f1b64720fbb6
msc.legacyurl: /mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on
msc.type: authoredcontent
ms.openlocfilehash: dd2e55d68ceb5a90134e394c00f3a3a231cb27d6
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345645"
---
# <a name="create-an-aspnet-mvc-5-app-with-facebook-twitter-linkedin-and-google-oauth2-sign-on-c"></a>创建 ASP.NET MVC 5 应用，实现 Facebook、Twitter、LinkedIn 和 Google OAuth2 登录 (C#)

作者： [Rick Anderson](https://twitter.com/RickAndMSFT)

> 本教程演示如何生成一个 ASP.NET MVC 5 web 应用程序，该应用程序允许用户 [2.0](http://oauth.net/2/) 使用来自外部身份验证提供程序（如 Facebook、Twitter、LinkedIn、Microsoft 或 Google）的凭据登录。 为简单起见，本教程重点介绍如何使用 Facebook 和 Google 的凭据。
> 
> 如果在您的网站中启用这些凭据，则会带来明显的优势，因为数百万用户已经拥有了具有这些外部提供商的帐户。 如果用户无需创建和记住一组新凭据，则可能更倾向于注册你的站点。
> 
> 另请参阅 [ASP.NET MVC 5 应用以及 SMS 和电子邮件 Two-Factor 身份验证](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md)。
> 
> 本教程还演示如何为用户添加配置文件数据，以及如何使用成员资格 API 添加角色。 本教程由 [Rick Anderson](https://blogs.msdn.com/rickAndy) 编写 ( 请在 Twitter 上关注： [@RickAndMSFT](https://twitter.com/RickAndMSFT) ) 。

<a id="start"></a>
## <a name="getting-started"></a>入门

首先，安装并运行[适用于 Web 或 Visual Studio 2013 的 Visual Studio Express 2013](https://go.microsoft.com/fwlink/?LinkId=299058) 。 [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566) 安装 Visual Studio [2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390521) 或更高版本。 有关 Dropbox、GitHub、Linkedin、Instagram、Buffer、Salesforce、流、堆栈交换、Tripit、Twitch、Twitter、Yahoo！等的帮助，请参阅此 [示例项目](https://github.com/matthewdunsdon/oauthforaspnet)。

> [!NOTE]
> 必须安装 Visual Studio [2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390521) 或更高版本才能使用 Google OAuth 2 并在本地调试，而不会出现 SSL 警告。

在**起始**页上单击 "**新建项目**"，或者可以使用菜单并依次选择 "**文件**" 和 "**新建项目**"。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image1.png)  

<a id="1st"></a>
## <a name="creating-your-first-application"></a>创建第一个应用程序

单击 " **新建项目**"，然后选择左侧的 " **Visual c #** "，然后选择 " **web** "，然后选择 " **ASP.NET Web 应用程序**"。 将项目命名为 "MvcAuth"，然后单击 **"确定**"。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image2.png)

在 " **新建 ASP.NET 项目** " 对话框中，单击 " **MVC**"。 如果身份验证不是 **单个用户帐户**，请单击 " **更改身份验证** " 按钮，然后选择 " **个人用户帐户**"。 通过检查 **云中的主机**，应用将非常易于在 Azure 中托管。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image3.png)

如果选择 **了 "在云中托管**"，请完成 "配置" 对话框。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image4.png)

### <a name="use-nuget-to-update-to-the-latest-owin-middleware"></a>使用 NuGet 更新到最新的 OWIN 中间件

使用 NuGet 包管理器更新 [OWIN 中间件](../../../aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana.md)。 在左侧菜单中选择 " **更新** "。 您可以单击 " **全部更新** " 按钮，也可以仅搜索 OWIN 包 (下一个图像) ：

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image5.png)

在下图中，只显示了 OWIN 包：

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image6.png)

从包管理器控制台 (PMC) ，可以输入 `Update-Package` 命令，该命令将更新所有包。

按 **F5** 或 **Ctrl + F5** 运行该应用程序。 在下图中，端口号为1234。 运行应用程序时，将看到不同的端口号。

根据浏览器窗口的大小，可能需要单击导航图标才能看到 " **主页**"、" **关于**"、" **联系人**"、" **注册** " 和 " **登录** " 链接。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image7.png)  
![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image8.png) 

<a id="ssl"></a>
## <a name="setting-up-ssl-in-the-project"></a>在项目中设置 SSL

若要连接到身份验证提供程序（如 Google 和 Facebook），需要将 IIS-Express 设置为使用 SSL。 务必要在登录后继续使用 SSL，而不是回发到 HTTP，登录 cookie 就像用户名和密码一样机密，而不使用 SSL，则会在网络上以明文形式发送密码。 除此之外，你已经花了些时间来执行握手并保护通道 (，这是在 MVC 管道运行之前，HTTPS 慢于 HTTP) 的内容，因此，在你登录后重定向回 HTTP 不会使当前请求或未来请求速度快得多。

1. 在 **解决方案资源管理器**中，单击 **MvcAuth** 项目。
2. 按 F4 键显示项目属性。 或者，您可以从 " **视图** " 菜单中选择 " **属性窗口**"。
3. 将 " **已启用 SSL** " 更改为 True。  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image9.png)
4. 将 (的 SSL URL 复制到该 URL， `https://localhost:44300/` 除非已) 创建其他 SSL 项目。
5. 在 **解决方案资源管理器**中，右键单击 **MvcAuth** 项目，然后选择 " **属性**"。
6. 选择 " **Web** " 选项卡，然后将 SSL URL 粘贴到 " **项目 URL** " 框中。 将该文件保存 (Ctl + S) 。 你将需要此 URL 来配置 Facebook 和 Google 身份验证应用。  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image10.png)
7. 将 [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) 特性添加到 `Home` 控制器，以要求所有请求都必须使用 HTTPS。 更安全的方法是将 [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) 筛选器添加到应用程序。 请参阅 &quot; 本教程中的使用 SSL 保护应用程序和授权属性部分 &quot; 教程 [使用身份验证和 SQL 数据库创建 ASP.NET MVC 应用并将其部署到 Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)。 主控制器的一部分如下所示。

    [!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample1.cs?highlight=1)]
8. 按 Ctrl+F5 运行应用程序。 如果以前安装过证书，则可以跳过本部分的其余部分，跳转到为 [OAuth 2 创建 Google 应用并将应用连接到该项目](#goog)，否则，请按照说明信任 IIS Express 生成的自签名证书。  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image11.png)
9. 阅读 " **安全警告** " 对话框，如果要安装代表 localhost 的证书，请单击 **"是"** 。  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image12.png)
10. IE 会显示“主页”** 页面，而且不会出现 SSL 警告。  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image13.png)
11. Google Chrome 也会接受证书，并且不出现警告便显示 HTTPS 内容。 Firefox 会使用自己的证书存储区，因此会显示警告。 对于我们的应用程序，你可以安全地单击 **"我了解风险"**。   
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image14.png)

<a id="goog"></a>
## <a name="creating-a-google-app-for-oauth-2-and-connecting-the-app-to-the-project"></a>为 OAuth 2 创建 Google 应用并将应用连接到项目

> [!WARNING]
> 有关当前 Google OAuth 说明，请参阅 [在 ASP.NET Core 中配置 Google authentication](/aspnet/core/security/authentication/social/google-logins)。

1. 导航到 [Google 开发人员控制台](https://console.developers.google.com/)。
2. 如果之前尚未创建项目，请在左侧选项卡中选择 " **凭据** "，然后选择 " **创建**"。
3. 在左侧选项卡中，单击 " **凭据**"。
4. 单击 " **创建凭据** "，然后单击 " **OAUTH 客户端 ID**"。 

    1. 在 " **创建客户端 ID** " 对话框中，保留应用程序类型的默认 **Web 应用程序** 。
    2. **Authorized JavaScript** `https://localhost:44300/` 除非你已创建其他 ssl 项目，否则请将授权的 JavaScript 源设置为你前面 (的 ssl URL) 
    3. 将 **授权的重定向 URI** 设置为：  
         `https://localhost:44300/signin-google`
5. 单击 "OAuth 许可屏幕" 菜单项，然后设置你的电子邮件地址和产品名称。 完成此窗体后，单击 " **保存**"。
6. 单击 "库" 菜单项，搜索 " **Google + API**"，单击它，然后按 "启用"。
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image15.png)  
  
   下图显示了已启用的 Api。  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image16.png)
7. 在 Google Api API 管理器中，访问 " **凭据** " 选项卡以获取 **客户端 ID**。 下载以使用应用程序机密保存 JSON 文件。 将**ClientId**和**ClientSecret**复制并粘贴到 `UseGoogleAuthentication` *App_Start*文件夹中的*Startup.Auth.cs*文件中的方法。 下面显示的 **ClientId** 和 **ClientSecret** 值为示例，不起作用。

    [!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample2.cs?highlight=37-39)]

    > [!WARNING]
    > 安全性-永远不要将敏感数据存储在源代码中。 帐户和凭据将添加到上面的代码中，以使示例简单。 请参阅 [将密码和其他敏感数据部署到 ASP.NET 和 Azure App Service 的最佳实践](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)。
8. 按 **CTRL + F5** 生成并运行应用程序。 单击 " **登录** " 链接。  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image17.png)
9. 在 " **使用其他服务进行登录**" 下，单击 " **Google**"。  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image18.png)

    > [!NOTE]
    > 如果错过上述任何步骤，会收到 HTTP 401 错误。 重新检查以上步骤。 如果错过了所需的设置 (例如 **产品名称**) ，请添加缺少的项并保存;身份验证可能需要几分钟的时间才能生效。
10. 你将被重定向到 Google 站点，你将在其中输入你的凭据。   
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image19.png)
11. 输入你的凭据后，你将会提示你刚创建的 Web 应用程序对其授予权限：
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image20.png)
12. 单击“接受”。 你现在将重定向回 MvcAuth 应用程序的 " **注册** " 页，你可以在该应用程序中注册 Google 帐户。 你可以选择更改 Gmail 帐户使用的本地电子邮件注册名称，但是，你通常会保留默认电子邮件别名（即，用于身份验证的名称）。 单击“注册”。  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image21.png)

<a id="fb"></a>
## <a name="creating-the-app-in-facebook-and-connecting-the-app-to-the-project"></a>在 Facebook 中创建应用并将应用连接到项目

> [!WARNING]
> 有关当前 Facebook OAuth2 authentication 说明，请参阅 [配置 Facebook 身份验证](/aspnet/core/security/authentication/social/facebook-logins)

<a id="mdb"></a>
## <a name="examine-the-membership-data"></a>检查成员身份数据

在 " **视图** " 菜单上，单击 **服务器资源管理器**。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image32.png)

展开 **DefaultConnection (MvcAuth) **，展开 " **表**"，右键单击 **AspNetUsers** ，然后单击 " **显示表数据**"。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image33.png)

![aspnetusers 表数据](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image34.png)

<a id="ap"></a>
## <a name="adding-profile-data-to-the-user-class"></a>将配置文件数据添加到用户类

在本部分中，将在注册期间将出生日期和住宅区添加到用户数据中，如下图所示。

![家庭城镇和 Bday 注册](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image35.png)

打开 *Models\IdentityModels.cs* 文件并添加出生日期和住宅城镇属性：

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample4.cs?highlight=3-4)]

打开 *Models\AccountViewModels.cs* 文件，并在中打开 "设置出生日期" 和 "住宅城镇" 属性 `ExternalLoginConfirmationViewModel` 。

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample5.cs?highlight=8-9)]

打开 *Controllers\AccountController.cs* 文件，并在操作方法中添加 "出生日期" 和 "住宅" 的代码，如下 `ExternalLoginConfirmation` 所示：

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample6.cs?highlight=21-23)]

将出生日期和家庭城镇添加到 *Views\Account\ExternalLoginConfirmation.cshtml* 文件：

[!code-cshtml[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample7.cshtml?highlight=27-40)]

删除成员资格数据库，以便可以再次将 Facebook 帐户注册到你的应用程序，并验证你是否可以添加新的出生日期和家庭城镇个人资料信息。

在 **解决方案资源管理器**中，单击 " **显示所有文件** " 图标，然后右键单击 " *添加 \_ Data\aspnet-MvcAuth- &lt; 日期戳 &gt; * "，然后单击 " **删除**"。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image36.png)

从 " **工具** " 菜单中，单击 " **NuGet 包管理**器"，然后单击 " **程序包管理器控制台** (PMC) "。 在 PMC 中输入以下命令。

1. Enable-Migrations
2. Add-Migration Init
3. Update-Database

运行应用程序，并使用 FaceBook 和 Google 登录并注册某些用户。

## <a name="examine-the-membership-data"></a>检查成员身份数据

在 " **视图** " 菜单上，单击 **服务器资源管理器**。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image37.png)

右键单击 **AspNetUsers** ，然后单击 " **显示表数据**"。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image38.png)

`HomeTown`和 `BirthDate` 字段如下所示。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image39.png)

<a id="off"></a>
## <a name="logging-off-your-app-and-logging-in-with-another-account"></a>注销应用并登录到其他帐户

如果你使用 Facebook 登录到你的应用，然后注销并尝试使用其他 Facebook 帐户重新登录 (使用同一浏览器) ，你将立即登录到你使用的以前的 Facebook 帐户。 要使用其他帐户，你需要导航到 Facebook 并注销 Facebook。 同样的规则也适用于任何其他第三方身份验证提供程序。 或者，您可以使用其他浏览器通过其他帐户登录。

## <a name="next-steps"></a>后续步骤

有关 Yahoo 和 LinkedIn 说明，请参阅为 OWIN by Jerrie Pelser [介绍 yahoo 和 Linkedin OAuth security providers](http://www.jerriepelser.com/blog/introducing-the-yahoo-linkedin-oauth-security-providers-for-owin/) 。 请参阅 Jerrie 的 "ASP.NET MVC 5 的社交登录" 按钮，获取 "启用社交登录" 按钮。

按照我 [的教程创建具有身份验证和 SQL 数据库的 ASP.NET MVC 应用并将其部署到 Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)，这将继续本教程，并显示以下内容：

1. 如何将应用部署到 Azure。
2. 如何通过角色保护应用。
3. 如何通过 [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute(v=vs.108).aspx) 和 [授权](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.100).aspx) 筛选器保护你的应用程序。
4. 如何使用成员资格 API 添加用户和角色。

请提供有关你喜欢此教程的方式以及我们可以改进的内容的反馈。 你还可以在 [显示如何处理代码](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code)中请求新主题。 甚至可以询问并投票要添加到 ASP.NET 的新功能。 例如，你可以投票工具来 [创建和管理用户和角色。](http://aspnet.uservoice.com/forums/41199-general-asp-net/suggestions/5646857-asp-net-identity-membership-db-tool-to-mangage-use)

有关 ASP.NET 外部身份验证服务工作原理的详细说明，请参阅 Robert Mcmurray 有关的 [外部身份验证服务](https://asp.net/web-api/overview/security/external-authentication-services)。 Robert 的文章还详细介绍了如何启用 Microsoft 和 Twitter 身份验证。 Tom Dykstra 的绝佳 [EF/MVC 教程](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) 介绍了如何使用实体框架。

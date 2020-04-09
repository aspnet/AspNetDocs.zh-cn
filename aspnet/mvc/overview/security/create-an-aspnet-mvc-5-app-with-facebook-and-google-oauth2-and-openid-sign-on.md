---
uid: mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on
title: 使用 Facebook、Twitter、LinkedIn 和 Google OAuth2 登录 （C#） 创建 MVC 5 应用程序 |微软文档
author: Rick-Anderson
description: 本教程介绍如何构建ASP.NET MVC 5 Web 应用程序，使用户能够使用 OAuth 2.0 使用外部 authenti 的凭据登录...
ms.author: riande
ms.date: 04/03/2015
ms.assetid: 81ee500f-fc37-40d6-8722-f1b64720fbb6
msc.legacyurl: /mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on
msc.type: authoredcontent
ms.openlocfilehash: dd2e55d68ceb5a90134e394c00f3a3a231cb27d6
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675915"
---
# <a name="create-an-aspnet-mvc-5-app-with-facebook-twitter-linkedin-and-google-oauth2-sign-on-c"></a>创建 ASP.NET MVC 5 应用，实现 Facebook、Twitter、LinkedIn 和 Google OAuth2 登录 (C#)

由[里克·安德森](https://twitter.com/RickAndMSFT)

> 本教程介绍如何构建ASP.NET MVC 5 Web 应用程序，使用户能够使用[OAuth 2.0](http://oauth.net/2/)使用外部身份验证提供商（如 Facebook、Twitter、LinkedIn、微软或 Google）的凭据登录。 为简单起见，本教程重点介绍使用来自 Facebook 和 Google 的凭据。
> 
> 在您的网站中启用这些凭据提供了显著优势，因为数百万用户已经拥有了这些外部提供商的帐户。 如果用户不必创建并记住一组新的凭据，他们可能更倾向于注册您的网站。
> 
> 另请参阅[ASP.NET MVC 5 应用程序与短信和电子邮件双重身份验证](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md)。
> 
> 本教程还演示如何为用户添加配置文件数据，以及如何使用成员资格 API 添加角色。 本教程是由[里克安德森](https://blogs.msdn.com/rickAndy)（请关注我在推特上： [@RickAndMSFT](https://twitter.com/RickAndMSFT) ）.

<a id="start"></a>
## <a name="getting-started"></a>入门

首先安装和运行[Visual Studio Express 2013 用于 Web](https://go.microsoft.com/fwlink/?LinkId=299058)或[可视化工作室 2013](https://go.microsoft.com/fwlink/?LinkId=306566)。 安装可视化工作室[2013 更新 3](https://go.microsoft.com/fwlink/?LinkId=390521)或更高版本。 有关 Dropbox、GitHub、LinkedIn、Instagram、缓冲、销售力量、STEAM、堆栈交换、三联、Twitch、Twitter、Yahoo！等的帮助，请参阅此示例[项目](https://github.com/matthewdunsdon/oauthforaspnet)。

> [!NOTE]
> 您必须安装 Visual Studio [2013 更新 3](https://go.microsoft.com/fwlink/?LinkId=390521)或更高版本才能使用 Google OAuth 2 并在本地调试，而无需出现 SSL 警告。

单击 **"开始"** 页中的 **"新项目**"，也可以使用菜单并选择 **"文件**"，然后选择 **"新项目**"。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image1.png)  

<a id="1st"></a>
## <a name="creating-your-first-application"></a>创建第一个应用程序

单击 **"新项目**"，然后选择左侧的**可视化 C#，** 然后选择**Web，** 然后选择**ASP.NET Web 应用程序**。 将项目命名为"MvcAuth"，然后单击"**确定**"。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image2.png)

在 **"新ASP.NET项目"** 对话框中，单击**MVC**。 如果身份验证不是**单个用户帐户**，请单击 **"更改身份验证**"按钮并选择**单个用户帐户**。 通过检查**云中的主机**，应用程序将很容易在 Azure 中托管。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image3.png)

如果在**云中选择"主机**"，请完成配置对话框。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image4.png)

### <a name="use-nuget-to-update-to-the-latest-owin-middleware"></a>使用 NuGet 更新到最新的 OWIN 中间件

使用 NuGet 软件包管理器更新[OWIN 中间件](../../../aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana.md)。 选择左侧菜单中的 **"更新**"。 您可以单击"**全部更新"** 按钮，也可以仅搜索 OWIN 包（下一张图片所示）：

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image5.png)

在下图中，仅显示 OWIN 包：

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image6.png)

从包管理器控制台 （PMC） 中，您可以`Update-Package`输入该命令，该命令将更新所有包。

按**F5**或**Ctrl+F5**以运行应用程序。 在下图中，端口号为 1234。 运行应用程序时，您将看到不同的端口号。

根据浏览器窗口的大小，您可能需要单击导航图标才能查看 **"主页**、**关于**"、**联系**、**注册**和**登录**链接。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image7.png)  
![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image8.png) 

<a id="ssl"></a>
## <a name="setting-up-ssl-in-the-project"></a>在项目中设置 SSL

要连接到 Google 和 Facebook 等身份验证提供商，您需要设置 IIS-Express 才能使用 SSL。 登录后继续使用 SSL 而不回退到 HTTP 非常重要，您的登录 Cookie 与用户名和密码一样具有机密性，无需使用 SSL，则通过线发送清晰文本。 此外，在运行 MVC 管道之前，您已经花时间执行握手并保护通道（这是使 HTTPS 比 HTTP 慢的大部分），因此在登录后重定向回 HTTP 不会使当前请求或将来的请求更快。

1. 在**解决方案资源管理器中**，单击**MvcAuth**项目。
2. 点击 F4 键以显示项目属性。 或者，从 **"视图"** 菜单中选择 **"属性窗口**"。
3. 将**启用的 SSL**更改为 true。  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image9.png)
4. 复制 SSL URL（除非您创建了`https://localhost:44300/`其他 SSL 项目，否则这将是 SSL URL）。
5. 在**解决方案资源管理器**中，右键单击**MvcAuth**项目并选择**属性**。
6. 选择 **"Web"** 选项卡，然后将 SSL URL 粘贴到 **"项目 Url"** 框中。 保存文件 （Ctl_S）。 您需要此网址来配置 Facebook 和 Google 身份验证应用。  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image10.png)
7. 将["要求Https"](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx)属性添加到`Home`控制器，以要求所有请求都必须使用 HTTPS。 更安全的方法是向应用程序添加["需要Https"](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx)筛选器。 请参阅我的教程&quot;中的"使用 SSL 和授权属性&quot;保护应用程序"一节[，创建一个带有身份验证和 SQL DB 的ASP.NET MVC 应用并部署到 Azure 应用服务](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)。 主控制器的一部分如下所示。

    [!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample1.cs?highlight=1)]
8. 按 Ctrl+F5 运行应用程序。 如果您过去安装了证书，则可以跳过本节的其余部分，跳转到[为 OAuth 2 创建 Google 应用并将应用连接到项目](#goog)，否则，请按照说明信任 IIS Express 生成的自签名证书。  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image11.png)
9. 阅读**安全警告**对话框，然后单击"**是**"，如果要安装表示本地主机的证书。  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image12.png)
10. IE 会显示“主页”** 页面，而且不会出现 SSL 警告。  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image13.png)
11. Google Chrome 也会接受证书，并且不出现警告便显示 HTTPS 内容。 Firefox 会使用自己的证书存储区，因此会显示警告。 对于我们的应用程序，您可以安全地点击 **"我了解风险**"。   
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image14.png)

<a id="goog"></a>
## <a name="creating-a-google-app-for-oauth-2-and-connecting-the-app-to-the-project"></a>为 OAuth 2 创建 Google 应用并将应用连接到项目

> [!WARNING]
> 有关当前 Google OAuth 说明，请参阅[在 ASP.NET 核心 中配置 Google 身份验证](/aspnet/core/security/authentication/social/google-logins)。

1. 导航到[谷歌开发者控制台](https://console.developers.google.com/)。
2. 如果以前未创建项目，请在左侧选项卡中选择 **"凭据"，** 然后选择"**创建**"。
3. 在左侧选项卡中，单击 **"凭据**"。
4. 单击 **"创建凭据**"，然后单击**OAuth 客户端 ID**。 

    1. 在 **"创建客户端 ID"** 对话框中，保留应用程序类型的默认**Web 应用程序**。
    2. 将**授权 JavaScript**源设置为上述使用的 SSL URL（`https://localhost:44300/`除非您创建了其他 SSL 项目）
    3. 将**授权重定向 URI**设置为：  
         `https://localhost:44300/signin-google`
5. 单击"OAuth 同意"屏幕菜单项，然后设置您的电子邮件地址和产品名称。 填写完表格后，单击"**保存**"。
6. 点击库菜单项目，搜索**谷歌+API，** 点击它，然后按启用。
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image15.png)  
  
   下图显示了启用的 API。  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image16.png)
7. 从 Google API API API 管理器，访问**凭据**选项卡以获取**客户端 ID**。 下载以保存包含应用程序机密的 JSON 文件。 将**客户端 Id**和**客户端机密**复制并粘贴`UseGoogleAuthentication`到*App_Start*文件夹中*Startup.Auth.cs*文件中找到的方法。 下面显示的**客户端 Id**和**客户端机密**值是示例，不起作用。

    [!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample2.cs?highlight=37-39)]

    > [!WARNING]
    > 安全性 - 切勿将敏感数据存储在源代码中。 帐户和凭据将添加到上面的代码中，以保持示例简单。 请参阅[将密码和其他敏感数据部署到ASP.NET和 Azure 应用服务的最佳做法](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)。
8. 按**CTRL+F5**生成并运行应用程序。 单击**登录**链接。  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image17.png)
9. 在 **"使用其他服务登录**"下，单击**Google**。  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image18.png)

    > [!NOTE]
    > 如果您错过了上述任何步骤，您将获得 HTTP 401 错误。 重新检查上面的步骤。 如果错过了所需的设置（例如**产品名称**），则添加缺少的项目并保存;身份验证可能需要几分钟才能工作。
10. 您将被重定向到 Google 网站，您将在其中输入您的凭据。   
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image19.png)
11. 输入你的凭据后，你将会提示你刚创建的 Web 应用程序对其授予权限：
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image20.png)
12. 单击“接受”****。 现在，您将被重定向回 MvcAuth 应用程序的**注册**页面，您可以在其中注册您的 Google 帐户。 你可以选择更改 Gmail 帐户使用的本地电子邮件注册名称，但是，你通常会保留默认电子邮件别名（即，用于身份验证的名称）。 单击“注册”  。  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image21.png)

<a id="fb"></a>
## <a name="creating-the-app-in-facebook-and-connecting-the-app-to-the-project"></a>在 Facebook 中创建应用并将应用连接到项目

> [!WARNING]
> 有关当前 Facebook OAuth2 身份验证说明，请参阅[配置 Facebook 身份验证](/aspnet/core/security/authentication/social/facebook-logins)

<a id="mdb"></a>
## <a name="examine-the-membership-data"></a>检查成员资格数据

在 **"查看"** 菜单中，单击 **"服务器资源管理器**"。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image32.png)

展开**默认连接 （MvcAuth），** 展开**表**， 右键单击**AspNetUsers**并单击**显示表数据**。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image33.png)

![aspnetuser 表数据](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image34.png)

<a id="ap"></a>
## <a name="adding-profile-data-to-the-user-class"></a>将配置文件数据添加到用户类

在本节中，您将在注册期间将出生日期和家乡添加到用户数据中，如下图所示。

![与家乡和布莱德](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image35.png)

打开*模型_身份模型.cs*文件并添加出生日期和家乡属性：

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample4.cs?highlight=3-4)]

打开*模型_AccountViewModels.cs*文件以及 中的`ExternalLoginConfirmationViewModel`设定出生日期和家乡属性。

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample5.cs?highlight=8-9)]

打开*控制器\AccountController.cs*文件，并在`ExternalLoginConfirmation`操作方法中添加出生日期和家乡的代码，如图所示：

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample6.cs?highlight=21-23)]

将出生日期和家乡添加到*视图\帐户\外部登录确认.cshtml*文件：

[!code-cshtml[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample7.cshtml?highlight=27-40)]

删除会员数据库，以便您可以再次将您的 Facebook 帐户注册到您的应用程序，并验证您可以添加新的出生日期和家乡个人资料信息。

从**解决方案资源管理器**中，单击 **"显示所有文件**"图标，然后单击 *"\_添加&lt;数据\aspnet-MvcAuth-dateStamp.mdf"，&gt;* 然后单击"**删除**"。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image36.png)

在 **"工具"** 菜单中，单击**NuGet 包管理器，** 然后单击**包管理器控制台**（PMC）。 在 PMC 中输入以下命令。

1. 启用迁移
2. 添加迁移 Init
3. Update-Database

运行该应用程序并使用 FaceBook 和 Google 登录并注册一些用户。

## <a name="examine-the-membership-data"></a>检查成员资格数据

在 **"查看"** 菜单中，单击 **"服务器资源管理器**"。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image37.png)

右键单击**AspNetUsers**并单击"**显示表数据**"。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image38.png)

和`HomeTown``BirthDate`字段如下所示。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image39.png)

<a id="off"></a>
## <a name="logging-off-your-app-and-logging-in-with-another-account"></a>注销应用并与其他帐户登录

如果您使用 Facebook 登录你的应用，然后注销并尝试使用其他 Facebook 帐户（使用相同的浏览器）再次登录，您将立即登录到您使用的以前的 Facebook 帐户。 要使用其他帐户，您需要导航到 Facebook 并在 Facebook 注销。 相同的规则适用于任何其他第三方身份验证提供程序。 或者，您可以使用其他浏览器使用其他帐户登录。

## <a name="next-steps"></a>后续步骤

请参阅介绍[雅虎和LinkedInOAuth安全提供商为OWIN](http://www.jerriepelser.com/blog/introducing-the-yahoo-linkedin-oauth-security-providers-for-owin/)由杰里佩尔瑟雅虎和LinkedIn说明。 请参阅 Jerrie 的"漂亮的社交登录按钮"ASP.NET MVC 5，以获得启用社交登录按钮。

按照我的教程[创建一个带有 auth 和 SQL DB 的 ASP.NET MVC 应用并部署到 Azure 应用服务](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)，该教程将继续本教程并显示以下内容：

1. 如何将应用部署到 Azure。
2. 如何使用角色保护应用。
3. 如何使用["需要 Http"](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute(v=vs.108).aspx)和["授权](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.100).aspx)"筛选器保护应用。
4. 如何使用成员资格 API 添加用户和角色。

请留下反馈，关于你喜欢本教程的方式，以及我们可以改进什么。 您也可以在["向我展示代码如何](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code)"上请求新主题。 您甚至可以要求并投票表决要添加到ASP.NET的新功能。 例如，您可以投票选择[创建和管理用户和角色的工具。](http://aspnet.uservoice.com/forums/41199-general-asp-net/suggestions/5646857-asp-net-identity-membership-db-tool-to-mangage-use)

有关外部身份验证服务ASP.NET工作方式的良好说明，请参阅罗伯特·麦克默里的外部[身份验证服务](https://asp.net/web-api/overview/security/external-authentication-services)。 罗伯特的文章还详细介绍了微软和Twitter的认证。 Tom Dykstra 出色的[EF/MVC 教程](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)展示了如何使用实体框架。

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
# <a name="create-an-aspnet-mvc-5-app-with-facebook-twitter-linkedin-and-google-oauth2-sign-on-c"></a><span data-ttu-id="ae393-103">创建 ASP.NET MVC 5 应用，实现 Facebook、Twitter、LinkedIn 和 Google OAuth2 登录 (C#)</span><span class="sxs-lookup"><span data-stu-id="ae393-103">Create an ASP.NET MVC 5 App with Facebook, Twitter, LinkedIn and Google OAuth2 Sign-on (C#)</span></span>

<span data-ttu-id="ae393-104">由[里克·安德森](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="ae393-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> <span data-ttu-id="ae393-105">本教程介绍如何构建ASP.NET MVC 5 Web 应用程序，使用户能够使用[OAuth 2.0](http://oauth.net/2/)使用外部身份验证提供商（如 Facebook、Twitter、LinkedIn、微软或 Google）的凭据登录。</span><span class="sxs-lookup"><span data-stu-id="ae393-105">This tutorial shows you how to build an ASP.NET MVC 5 web application that enables users to log in using [OAuth 2.0](http://oauth.net/2/) with credentials from an external authentication provider, such as Facebook, Twitter, LinkedIn, Microsoft, or Google.</span></span> <span data-ttu-id="ae393-106">为简单起见，本教程重点介绍使用来自 Facebook 和 Google 的凭据。</span><span class="sxs-lookup"><span data-stu-id="ae393-106">For simplicity, this tutorial focuses on working with credentials from Facebook and Google.</span></span>
> 
> <span data-ttu-id="ae393-107">在您的网站中启用这些凭据提供了显著优势，因为数百万用户已经拥有了这些外部提供商的帐户。</span><span class="sxs-lookup"><span data-stu-id="ae393-107">Enabling these credentials in your web sites provides a significant advantage because millions of users already have accounts with these external providers.</span></span> <span data-ttu-id="ae393-108">如果用户不必创建并记住一组新的凭据，他们可能更倾向于注册您的网站。</span><span class="sxs-lookup"><span data-stu-id="ae393-108">These users may be more inclined to sign up for your site if they do not have to create and remember a new set of credentials.</span></span>
> 
> <span data-ttu-id="ae393-109">另请参阅[ASP.NET MVC 5 应用程序与短信和电子邮件双重身份验证](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="ae393-109">See also [ASP.NET MVC 5 app with SMS and email Two-Factor Authentication](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md).</span></span>
> 
> <span data-ttu-id="ae393-110">本教程还演示如何为用户添加配置文件数据，以及如何使用成员资格 API 添加角色。</span><span class="sxs-lookup"><span data-stu-id="ae393-110">The tutorial also shows how to add profile data for the user, and how to use the Membership API to add roles.</span></span> <span data-ttu-id="ae393-111">本教程是由[里克安德森](https://blogs.msdn.com/rickAndy)（请关注我在推特上： [@RickAndMSFT](https://twitter.com/RickAndMSFT) ）.</span><span class="sxs-lookup"><span data-stu-id="ae393-111">This tutorial was written by [Rick Anderson](https://blogs.msdn.com/rickAndy) ( Please follow me on Twitter: [@RickAndMSFT](https://twitter.com/RickAndMSFT) ).</span></span>

<a id="start"></a>
## <a name="getting-started"></a><span data-ttu-id="ae393-112">入门</span><span class="sxs-lookup"><span data-stu-id="ae393-112">Getting Started</span></span>

<span data-ttu-id="ae393-113">首先安装和运行[Visual Studio Express 2013 用于 Web](https://go.microsoft.com/fwlink/?LinkId=299058)或[可视化工作室 2013](https://go.microsoft.com/fwlink/?LinkId=306566)。</span><span class="sxs-lookup"><span data-stu-id="ae393-113">Start by installing and running [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) or [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566).</span></span> <span data-ttu-id="ae393-114">安装可视化工作室[2013 更新 3](https://go.microsoft.com/fwlink/?LinkId=390521)或更高版本。</span><span class="sxs-lookup"><span data-stu-id="ae393-114">Install Visual Studio [2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390521) or higher.</span></span> <span data-ttu-id="ae393-115">有关 Dropbox、GitHub、LinkedIn、Instagram、缓冲、销售力量、STEAM、堆栈交换、三联、Twitch、Twitter、Yahoo！等的帮助，请参阅此示例[项目](https://github.com/matthewdunsdon/oauthforaspnet)。</span><span class="sxs-lookup"><span data-stu-id="ae393-115">For help with Dropbox, GitHub, Linkedin, Instagram, Buffer, Salesforce, STEAM, Stack Exchange, Tripit, Twitch, Twitter, Yahoo!, and more, see this [sample project](https://github.com/matthewdunsdon/oauthforaspnet).</span></span>

> [!NOTE]
> <span data-ttu-id="ae393-116">您必须安装 Visual Studio [2013 更新 3](https://go.microsoft.com/fwlink/?LinkId=390521)或更高版本才能使用 Google OAuth 2 并在本地调试，而无需出现 SSL 警告。</span><span class="sxs-lookup"><span data-stu-id="ae393-116">You must install Visual Studio [2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390521) or higher to use Google OAuth 2 and to debug locally without SSL warnings.</span></span>

<span data-ttu-id="ae393-117">单击 **"开始"** 页中的 **"新项目**"，也可以使用菜单并选择 **"文件**"，然后选择 **"新项目**"。</span><span class="sxs-lookup"><span data-stu-id="ae393-117">Click **New Project** from the **Start** page, or you can use the menu and select **File**, and then **New Project**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image1.png)  

<a id="1st"></a>
## <a name="creating-your-first-application"></a><span data-ttu-id="ae393-118">创建第一个应用程序</span><span class="sxs-lookup"><span data-stu-id="ae393-118">Creating Your First Application</span></span>

<span data-ttu-id="ae393-119">单击 **"新项目**"，然后选择左侧的**可视化 C#，** 然后选择**Web，** 然后选择**ASP.NET Web 应用程序**。</span><span class="sxs-lookup"><span data-stu-id="ae393-119">Click **New Project**, then select **Visual C#** on the left, then **Web** and then select **ASP.NET Web Application**.</span></span> <span data-ttu-id="ae393-120">将项目命名为"MvcAuth"，然后单击"**确定**"。</span><span class="sxs-lookup"><span data-stu-id="ae393-120">Name your project "MvcAuth" and then click **OK**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image2.png)

<span data-ttu-id="ae393-121">在 **"新ASP.NET项目"** 对话框中，单击**MVC**。</span><span class="sxs-lookup"><span data-stu-id="ae393-121">In the **New ASP.NET Project** dialog, click **MVC**.</span></span> <span data-ttu-id="ae393-122">如果身份验证不是**单个用户帐户**，请单击 **"更改身份验证**"按钮并选择**单个用户帐户**。</span><span class="sxs-lookup"><span data-stu-id="ae393-122">If the Authentication is not **Individual User Accounts**, click the **Change Authentication** button and select **Individual User Accounts**.</span></span> <span data-ttu-id="ae393-123">通过检查**云中的主机**，应用程序将很容易在 Azure 中托管。</span><span class="sxs-lookup"><span data-stu-id="ae393-123">By checking **Host in the cloud**, the app will be very easy to host in Azure.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image3.png)

<span data-ttu-id="ae393-124">如果在**云中选择"主机**"，请完成配置对话框。</span><span class="sxs-lookup"><span data-stu-id="ae393-124">If you selected **Host in the cloud**, complete the configure dialog.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image4.png)

### <a name="use-nuget-to-update-to-the-latest-owin-middleware"></a><span data-ttu-id="ae393-125">使用 NuGet 更新到最新的 OWIN 中间件</span><span class="sxs-lookup"><span data-stu-id="ae393-125">Use NuGet to update to the latest OWIN middleware</span></span>

<span data-ttu-id="ae393-126">使用 NuGet 软件包管理器更新[OWIN 中间件](../../../aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana.md)。</span><span class="sxs-lookup"><span data-stu-id="ae393-126">Use the NuGet package manager to update the [OWIN middleware](../../../aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana.md).</span></span> <span data-ttu-id="ae393-127">选择左侧菜单中的 **"更新**"。</span><span class="sxs-lookup"><span data-stu-id="ae393-127">Select **Updates** in the left menu.</span></span> <span data-ttu-id="ae393-128">您可以单击"**全部更新"** 按钮，也可以仅搜索 OWIN 包（下一张图片所示）：</span><span class="sxs-lookup"><span data-stu-id="ae393-128">You can click on the **Update All** button or you can search for only OWIN packages (shown in the next image):</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image5.png)

<span data-ttu-id="ae393-129">在下图中，仅显示 OWIN 包：</span><span class="sxs-lookup"><span data-stu-id="ae393-129">In the image below, only OWIN packages are shown:</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image6.png)

<span data-ttu-id="ae393-130">从包管理器控制台 （PMC） 中，您可以`Update-Package`输入该命令，该命令将更新所有包。</span><span class="sxs-lookup"><span data-stu-id="ae393-130">From the Package Manager Console (PMC), you can enter the `Update-Package` command, which will update all packages.</span></span>

<span data-ttu-id="ae393-131">按**F5**或**Ctrl+F5**以运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="ae393-131">Press **F5** or **Ctrl+F5** to run the application.</span></span> <span data-ttu-id="ae393-132">在下图中，端口号为 1234。</span><span class="sxs-lookup"><span data-stu-id="ae393-132">In the image below, the port number is 1234.</span></span> <span data-ttu-id="ae393-133">运行应用程序时，您将看到不同的端口号。</span><span class="sxs-lookup"><span data-stu-id="ae393-133">When you run the application, you'll see a different port number.</span></span>

<span data-ttu-id="ae393-134">根据浏览器窗口的大小，您可能需要单击导航图标才能查看 **"主页**、**关于**"、**联系**、**注册**和**登录**链接。</span><span class="sxs-lookup"><span data-stu-id="ae393-134">Depending on the size of your browser window, you might need to click the navigation icon to see the **Home**, **About**, **Contact**, **Register** and **Log in** links.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image7.png)  
![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image8.png) 

<a id="ssl"></a>
## <a name="setting-up-ssl-in-the-project"></a><span data-ttu-id="ae393-135">在项目中设置 SSL</span><span class="sxs-lookup"><span data-stu-id="ae393-135">Setting up SSL in the Project</span></span>

<span data-ttu-id="ae393-136">要连接到 Google 和 Facebook 等身份验证提供商，您需要设置 IIS-Express 才能使用 SSL。</span><span class="sxs-lookup"><span data-stu-id="ae393-136">To connect to authentication providers like Google and Facebook, you will need to set up IIS-Express to use SSL.</span></span> <span data-ttu-id="ae393-137">登录后继续使用 SSL 而不回退到 HTTP 非常重要，您的登录 Cookie 与用户名和密码一样具有机密性，无需使用 SSL，则通过线发送清晰文本。</span><span class="sxs-lookup"><span data-stu-id="ae393-137">It's important to keep using SSL after login and not drop back to HTTP, your login cookie is just as secret as your username and password, and without using SSL you're sending it in clear-text across the wire.</span></span> <span data-ttu-id="ae393-138">此外，在运行 MVC 管道之前，您已经花时间执行握手并保护通道（这是使 HTTPS 比 HTTP 慢的大部分），因此在登录后重定向回 HTTP 不会使当前请求或将来的请求更快。</span><span class="sxs-lookup"><span data-stu-id="ae393-138">Besides, you've already taken the time to perform the handshake and secure the channel (which is the bulk of what makes HTTPS slower than HTTP) before the MVC pipeline is run, so redirecting back to HTTP after you're logged in won't make the current request or future requests much faster.</span></span>

1. <span data-ttu-id="ae393-139">在**解决方案资源管理器中**，单击**MvcAuth**项目。</span><span class="sxs-lookup"><span data-stu-id="ae393-139">In **Solution Explorer**, click the **MvcAuth** project.</span></span>
2. <span data-ttu-id="ae393-140">点击 F4 键以显示项目属性。</span><span class="sxs-lookup"><span data-stu-id="ae393-140">Hit the F4 key to show the project properties.</span></span> <span data-ttu-id="ae393-141">或者，从 **"视图"** 菜单中选择 **"属性窗口**"。</span><span class="sxs-lookup"><span data-stu-id="ae393-141">Alternatively, from the **View** menu you can select **Properties Window**.</span></span>
3. <span data-ttu-id="ae393-142">将**启用的 SSL**更改为 true。</span><span class="sxs-lookup"><span data-stu-id="ae393-142">Change **SSL Enabled** to True.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image9.png)
4. <span data-ttu-id="ae393-143">复制 SSL URL（除非您创建了`https://localhost:44300/`其他 SSL 项目，否则这将是 SSL URL）。</span><span class="sxs-lookup"><span data-stu-id="ae393-143">Copy the SSL URL (which will be `https://localhost:44300/` unless you've created other SSL projects).</span></span>
5. <span data-ttu-id="ae393-144">在**解决方案资源管理器**中，右键单击**MvcAuth**项目并选择**属性**。</span><span class="sxs-lookup"><span data-stu-id="ae393-144">In **Solution Explorer**, right click the **MvcAuth** project and select **Properties**.</span></span>
6. <span data-ttu-id="ae393-145">选择 **"Web"** 选项卡，然后将 SSL URL 粘贴到 **"项目 Url"** 框中。</span><span class="sxs-lookup"><span data-stu-id="ae393-145">Select the **Web** tab, and then paste the SSL URL into the **Project Url** box.</span></span> <span data-ttu-id="ae393-146">保存文件 （Ctl_S）。</span><span class="sxs-lookup"><span data-stu-id="ae393-146">Save the file (Ctl+S).</span></span> <span data-ttu-id="ae393-147">您需要此网址来配置 Facebook 和 Google 身份验证应用。</span><span class="sxs-lookup"><span data-stu-id="ae393-147">You will need this URL to configure Facebook and Google authentication apps.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image10.png)
7. <span data-ttu-id="ae393-148">将["要求Https"](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx)属性添加到`Home`控制器，以要求所有请求都必须使用 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="ae393-148">Add the [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) attribute to the `Home` controller to require all requests must use HTTPS.</span></span> <span data-ttu-id="ae393-149">更安全的方法是向应用程序添加["需要Https"](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx)筛选器。</span><span class="sxs-lookup"><span data-stu-id="ae393-149">A more secure approach is to add the [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) filter to the application.</span></span> <span data-ttu-id="ae393-150">请参阅我的教程&quot;中的"使用 SSL 和授权属性&quot;保护应用程序"一节[，创建一个带有身份验证和 SQL DB 的ASP.NET MVC 应用并部署到 Azure 应用服务](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)。</span><span class="sxs-lookup"><span data-stu-id="ae393-150">See the section &quot;Protect the Application with SSL and the Authorize Attribute&quot; in my tutorial [Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span></span> <span data-ttu-id="ae393-151">主控制器的一部分如下所示。</span><span class="sxs-lookup"><span data-stu-id="ae393-151">A portion of the Home controller is shown below.</span></span>

    [!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample1.cs?highlight=1)]
8. <span data-ttu-id="ae393-152">按 Ctrl+F5 运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="ae393-152">Press CTRL+F5 to run the application.</span></span> <span data-ttu-id="ae393-153">如果您过去安装了证书，则可以跳过本节的其余部分，跳转到[为 OAuth 2 创建 Google 应用并将应用连接到项目](#goog)，否则，请按照说明信任 IIS Express 生成的自签名证书。</span><span class="sxs-lookup"><span data-stu-id="ae393-153">If you've installed the certificate in the past, you can skip the rest of this section and jump to [Creating a Google app for OAuth 2 and connecting the app to the project](#goog), otherwise, follow the instructions to trust the self-signed certificate that IIS Express has generated.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image11.png)
9. <span data-ttu-id="ae393-154">阅读**安全警告**对话框，然后单击"**是**"，如果要安装表示本地主机的证书。</span><span class="sxs-lookup"><span data-stu-id="ae393-154">Read the **Security Warning** dialog and then click **Yes** if you want to install the certificate representing localhost.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image12.png)
10. <span data-ttu-id="ae393-155">IE 会显示“主页”\*\* 页面，而且不会出现 SSL 警告。</span><span class="sxs-lookup"><span data-stu-id="ae393-155">IE shows the *Home* page and there are no SSL warnings.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image13.png)
11. <span data-ttu-id="ae393-156">Google Chrome 也会接受证书，并且不出现警告便显示 HTTPS 内容。</span><span class="sxs-lookup"><span data-stu-id="ae393-156">Google Chrome also accepts the certificate and will show HTTPS content without a warning.</span></span> <span data-ttu-id="ae393-157">Firefox 会使用自己的证书存储区，因此会显示警告。</span><span class="sxs-lookup"><span data-stu-id="ae393-157">Firefox uses its own certificate store, so it will display a warning.</span></span> <span data-ttu-id="ae393-158">对于我们的应用程序，您可以安全地点击 **"我了解风险**"。</span><span class="sxs-lookup"><span data-stu-id="ae393-158">For our application you can safely click **I Understand the Risks**.</span></span>   
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image14.png)

<a id="goog"></a>
## <a name="creating-a-google-app-for-oauth-2-and-connecting-the-app-to-the-project"></a><span data-ttu-id="ae393-159">为 OAuth 2 创建 Google 应用并将应用连接到项目</span><span class="sxs-lookup"><span data-stu-id="ae393-159">Creating a Google app for OAuth 2 and connecting the app to the project</span></span>

> [!WARNING]
> <span data-ttu-id="ae393-160">有关当前 Google OAuth 说明，请参阅[在 ASP.NET 核心 中配置 Google 身份验证](/aspnet/core/security/authentication/social/google-logins)。</span><span class="sxs-lookup"><span data-stu-id="ae393-160">For current Google OAuth instructions, see [Configuring Google authentication in ASP.NET Core](/aspnet/core/security/authentication/social/google-logins).</span></span>

1. <span data-ttu-id="ae393-161">导航到[谷歌开发者控制台](https://console.developers.google.com/)。</span><span class="sxs-lookup"><span data-stu-id="ae393-161">Navigate to the [Google Developers Console](https://console.developers.google.com/).</span></span>
2. <span data-ttu-id="ae393-162">如果以前未创建项目，请在左侧选项卡中选择 **"凭据"，** 然后选择"**创建**"。</span><span class="sxs-lookup"><span data-stu-id="ae393-162">If you haven't created a project before, select **Credentials** in the left tab, and then select **Create**.</span></span>
3. <span data-ttu-id="ae393-163">在左侧选项卡中，单击 **"凭据**"。</span><span class="sxs-lookup"><span data-stu-id="ae393-163">In the left tab, click **Credentials**.</span></span>
4. <span data-ttu-id="ae393-164">单击 **"创建凭据**"，然后单击**OAuth 客户端 ID**。</span><span class="sxs-lookup"><span data-stu-id="ae393-164">Click **Create credentials** then **OAuth client ID**.</span></span> 

    1. <span data-ttu-id="ae393-165">在 **"创建客户端 ID"** 对话框中，保留应用程序类型的默认**Web 应用程序**。</span><span class="sxs-lookup"><span data-stu-id="ae393-165">In the **Create Client ID** dialog, keep the default **Web application** for the application type.</span></span>
    2. <span data-ttu-id="ae393-166">将**授权 JavaScript**源设置为上述使用的 SSL URL（`https://localhost:44300/`除非您创建了其他 SSL 项目）</span><span class="sxs-lookup"><span data-stu-id="ae393-166">Set the **Authorized JavaScript** origins to the SSL URL you used above (`https://localhost:44300/` unless you've created other SSL projects)</span></span>
    3. <span data-ttu-id="ae393-167">将**授权重定向 URI**设置为：</span><span class="sxs-lookup"><span data-stu-id="ae393-167">Set the **Authorized redirect URI** to:</span></span>  
         `https://localhost:44300/signin-google`
5. <span data-ttu-id="ae393-168">单击"OAuth 同意"屏幕菜单项，然后设置您的电子邮件地址和产品名称。</span><span class="sxs-lookup"><span data-stu-id="ae393-168">Click the OAuth Consent screen menu item, then set your email address and product name.</span></span> <span data-ttu-id="ae393-169">填写完表格后，单击"**保存**"。</span><span class="sxs-lookup"><span data-stu-id="ae393-169">When you have completed the form click **Save**.</span></span>
6. <span data-ttu-id="ae393-170">点击库菜单项目，搜索**谷歌+API，** 点击它，然后按启用。</span><span class="sxs-lookup"><span data-stu-id="ae393-170">Click the Library menu item, search **Google+ API**, click on it then press Enable.</span></span>
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image15.png)  
  
   <span data-ttu-id="ae393-171">下图显示了启用的 API。</span><span class="sxs-lookup"><span data-stu-id="ae393-171">The image below shows the enabled APIs.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image16.png)
7. <span data-ttu-id="ae393-172">从 Google API API API 管理器，访问**凭据**选项卡以获取**客户端 ID**。</span><span class="sxs-lookup"><span data-stu-id="ae393-172">From the Google APIs API Manager, visit the **Credentials** tab to obtain the **Client ID**.</span></span> <span data-ttu-id="ae393-173">下载以保存包含应用程序机密的 JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="ae393-173">Download to save a JSON file with application secrets.</span></span> <span data-ttu-id="ae393-174">将**客户端 Id**和**客户端机密**复制并粘贴`UseGoogleAuthentication`到*App_Start*文件夹中*Startup.Auth.cs*文件中找到的方法。</span><span class="sxs-lookup"><span data-stu-id="ae393-174">Copy and paste the **ClientId** and **ClientSecret** into the `UseGoogleAuthentication` method found in the *Startup.Auth.cs* file in the *App_Start* folder.</span></span> <span data-ttu-id="ae393-175">下面显示的**客户端 Id**和**客户端机密**值是示例，不起作用。</span><span class="sxs-lookup"><span data-stu-id="ae393-175">The **ClientId** and **ClientSecret** values shown below are samples and don't work.</span></span>

    [!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample2.cs?highlight=37-39)]

    > [!WARNING]
    > <span data-ttu-id="ae393-176">安全性 - 切勿将敏感数据存储在源代码中。</span><span class="sxs-lookup"><span data-stu-id="ae393-176">Security - Never store sensitive data in your source code.</span></span> <span data-ttu-id="ae393-177">帐户和凭据将添加到上面的代码中，以保持示例简单。</span><span class="sxs-lookup"><span data-stu-id="ae393-177">The account and credentials are added to the code above to keep the sample simple.</span></span> <span data-ttu-id="ae393-178">请参阅[将密码和其他敏感数据部署到ASP.NET和 Azure 应用服务的最佳做法](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)。</span><span class="sxs-lookup"><span data-stu-id="ae393-178">See [Best practices for deploying passwords and other sensitive data to ASP.NET and Azure App Service](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md).</span></span>
8. <span data-ttu-id="ae393-179">按**CTRL+F5**生成并运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="ae393-179">Press **CTRL+F5** to build and run the application.</span></span> <span data-ttu-id="ae393-180">单击**登录**链接。</span><span class="sxs-lookup"><span data-stu-id="ae393-180">Click the **Log in** link.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image17.png)
9. <span data-ttu-id="ae393-181">在 **"使用其他服务登录**"下，单击**Google**。</span><span class="sxs-lookup"><span data-stu-id="ae393-181">Under **Use another service to log in**, click **Google**.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image18.png)

    > [!NOTE]
    > <span data-ttu-id="ae393-182">如果您错过了上述任何步骤，您将获得 HTTP 401 错误。</span><span class="sxs-lookup"><span data-stu-id="ae393-182">If you miss any of the steps above you will get a HTTP 401 error.</span></span> <span data-ttu-id="ae393-183">重新检查上面的步骤。</span><span class="sxs-lookup"><span data-stu-id="ae393-183">Recheck your steps above.</span></span> <span data-ttu-id="ae393-184">如果错过了所需的设置（例如**产品名称**），则添加缺少的项目并保存;身份验证可能需要几分钟才能工作。</span><span class="sxs-lookup"><span data-stu-id="ae393-184">If you miss a required setting (for example **product name**), add the missing item and save; it can take a few minutes for authentication to work.</span></span>
10. <span data-ttu-id="ae393-185">您将被重定向到 Google 网站，您将在其中输入您的凭据。</span><span class="sxs-lookup"><span data-stu-id="ae393-185">You will be redirected to the Google site where you will enter your credentials.</span></span>   
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image19.png)
11. <span data-ttu-id="ae393-186">输入你的凭据后，你将会提示你刚创建的 Web 应用程序对其授予权限：</span><span class="sxs-lookup"><span data-stu-id="ae393-186">After you enter your credentials, you will be prompted to give permissions to the web application you just created:</span></span>
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image20.png)
12. <span data-ttu-id="ae393-187">单击“接受”\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="ae393-187">Click **Accept**.</span></span> <span data-ttu-id="ae393-188">现在，您将被重定向回 MvcAuth 应用程序的**注册**页面，您可以在其中注册您的 Google 帐户。</span><span class="sxs-lookup"><span data-stu-id="ae393-188">You will now be redirected back to the **Register** page of the MvcAuth application where you can register your Google account.</span></span> <span data-ttu-id="ae393-189">你可以选择更改 Gmail 帐户使用的本地电子邮件注册名称，但是，你通常会保留默认电子邮件别名（即，用于身份验证的名称）。</span><span class="sxs-lookup"><span data-stu-id="ae393-189">You have the option of changing the local email registration name used for your Gmail account, but you generally want to keep the default email alias (that is, the one you used for authentication).</span></span> <span data-ttu-id="ae393-190">单击“注册”  。</span><span class="sxs-lookup"><span data-stu-id="ae393-190">Click **Register**.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image21.png)

<a id="fb"></a>
## <a name="creating-the-app-in-facebook-and-connecting-the-app-to-the-project"></a><span data-ttu-id="ae393-191">在 Facebook 中创建应用并将应用连接到项目</span><span class="sxs-lookup"><span data-stu-id="ae393-191">Creating the app in Facebook and connecting the app to the project</span></span>

> [!WARNING]
> <span data-ttu-id="ae393-192">有关当前 Facebook OAuth2 身份验证说明，请参阅[配置 Facebook 身份验证](/aspnet/core/security/authentication/social/facebook-logins)</span><span class="sxs-lookup"><span data-stu-id="ae393-192">For current Facebook OAuth2 authentication instructions, see [Configuring Facebook authentication](/aspnet/core/security/authentication/social/facebook-logins)</span></span>

<a id="mdb"></a>
## <a name="examine-the-membership-data"></a><span data-ttu-id="ae393-193">检查成员资格数据</span><span class="sxs-lookup"><span data-stu-id="ae393-193">Examine the Membership Data</span></span>

<span data-ttu-id="ae393-194">在 **"查看"** 菜单中，单击 **"服务器资源管理器**"。</span><span class="sxs-lookup"><span data-stu-id="ae393-194">In the **View** menu, click **Server Explorer**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image32.png)

<span data-ttu-id="ae393-195">展开**默认连接 （MvcAuth），** 展开**表**， 右键单击**AspNetUsers**并单击**显示表数据**。</span><span class="sxs-lookup"><span data-stu-id="ae393-195">Expand **DefaultConnection (MvcAuth)**, expand **Tables**, right click **AspNetUsers** and click **Show Table Data**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image33.png)

![aspnetuser 表数据](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image34.png)

<a id="ap"></a>
## <a name="adding-profile-data-to-the-user-class"></a><span data-ttu-id="ae393-197">将配置文件数据添加到用户类</span><span class="sxs-lookup"><span data-stu-id="ae393-197">Adding Profile Data to the User Class</span></span>

<span data-ttu-id="ae393-198">在本节中，您将在注册期间将出生日期和家乡添加到用户数据中，如下图所示。</span><span class="sxs-lookup"><span data-stu-id="ae393-198">In this section you'll add birth date and home town to the user data during registration, as shown in the following image.</span></span>

![与家乡和布莱德](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image35.png)

<span data-ttu-id="ae393-200">打开*模型_身份模型.cs*文件并添加出生日期和家乡属性：</span><span class="sxs-lookup"><span data-stu-id="ae393-200">Open the *Models\IdentityModels.cs* file and add birth date and home town properties:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample4.cs?highlight=3-4)]

<span data-ttu-id="ae393-201">打开*模型_AccountViewModels.cs*文件以及 中的`ExternalLoginConfirmationViewModel`设定出生日期和家乡属性。</span><span class="sxs-lookup"><span data-stu-id="ae393-201">Open the *Models\AccountViewModels.cs* file and the set birth date and home town properties in `ExternalLoginConfirmationViewModel`.</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample5.cs?highlight=8-9)]

<span data-ttu-id="ae393-202">打开*控制器\AccountController.cs*文件，并在`ExternalLoginConfirmation`操作方法中添加出生日期和家乡的代码，如图所示：</span><span class="sxs-lookup"><span data-stu-id="ae393-202">Open the *Controllers\AccountController.cs* file and add code for birth date and home town in the `ExternalLoginConfirmation` action method as shown:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample6.cs?highlight=21-23)]

<span data-ttu-id="ae393-203">将出生日期和家乡添加到*视图\帐户\外部登录确认.cshtml*文件：</span><span class="sxs-lookup"><span data-stu-id="ae393-203">Add birth date and home town to the *Views\Account\ExternalLoginConfirmation.cshtml* file:</span></span>

[!code-cshtml[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample7.cshtml?highlight=27-40)]

<span data-ttu-id="ae393-204">删除会员数据库，以便您可以再次将您的 Facebook 帐户注册到您的应用程序，并验证您可以添加新的出生日期和家乡个人资料信息。</span><span class="sxs-lookup"><span data-stu-id="ae393-204">Delete the membership database so you can again register your Facebook account with your application and verify you can add the new birth date and home town profile information.</span></span>

<span data-ttu-id="ae393-205">从**解决方案资源管理器**中，单击 **"显示所有文件**"图标，然后单击 *"\_添加&lt;数据\aspnet-MvcAuth-dateStamp.mdf"，&gt;* 然后单击"**删除**"。</span><span class="sxs-lookup"><span data-stu-id="ae393-205">From **Solution Explorer**, click the **Show All Files** icon, then right click *Add\_Data\aspnet-MvcAuth-&lt;dateStamp&gt;.mdf* and click **Delete**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image36.png)

<span data-ttu-id="ae393-206">在 **"工具"** 菜单中，单击**NuGet 包管理器，** 然后单击**包管理器控制台**（PMC）。</span><span class="sxs-lookup"><span data-stu-id="ae393-206">From the **Tools** menu, click **NuGet Package Manger**, then click **Package Manager Console** (PMC).</span></span> <span data-ttu-id="ae393-207">在 PMC 中输入以下命令。</span><span class="sxs-lookup"><span data-stu-id="ae393-207">Enter the following commands in the PMC.</span></span>

1. <span data-ttu-id="ae393-208">启用迁移</span><span class="sxs-lookup"><span data-stu-id="ae393-208">Enable-Migrations</span></span>
2. <span data-ttu-id="ae393-209">添加迁移 Init</span><span class="sxs-lookup"><span data-stu-id="ae393-209">Add-Migration Init</span></span>
3. <span data-ttu-id="ae393-210">Update-Database</span><span class="sxs-lookup"><span data-stu-id="ae393-210">Update-Database</span></span>

<span data-ttu-id="ae393-211">运行该应用程序并使用 FaceBook 和 Google 登录并注册一些用户。</span><span class="sxs-lookup"><span data-stu-id="ae393-211">Run the application and use FaceBook and Google to log in and register some users.</span></span>

## <a name="examine-the-membership-data"></a><span data-ttu-id="ae393-212">检查成员资格数据</span><span class="sxs-lookup"><span data-stu-id="ae393-212">Examine the Membership Data</span></span>

<span data-ttu-id="ae393-213">在 **"查看"** 菜单中，单击 **"服务器资源管理器**"。</span><span class="sxs-lookup"><span data-stu-id="ae393-213">In the **View** menu, click **Server Explorer**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image37.png)

<span data-ttu-id="ae393-214">右键单击**AspNetUsers**并单击"**显示表数据**"。</span><span class="sxs-lookup"><span data-stu-id="ae393-214">Right click **AspNetUsers** and click **Show Table Data**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image38.png)

<span data-ttu-id="ae393-215">和`HomeTown``BirthDate`字段如下所示。</span><span class="sxs-lookup"><span data-stu-id="ae393-215">The `HomeTown` and `BirthDate` fields are shown below.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image39.png)

<a id="off"></a>
## <a name="logging-off-your-app-and-logging-in-with-another-account"></a><span data-ttu-id="ae393-216">注销应用并与其他帐户登录</span><span class="sxs-lookup"><span data-stu-id="ae393-216">Logging off your App and Logging in With Another Account</span></span>

<span data-ttu-id="ae393-217">如果您使用 Facebook 登录你的应用，然后注销并尝试使用其他 Facebook 帐户（使用相同的浏览器）再次登录，您将立即登录到您使用的以前的 Facebook 帐户。</span><span class="sxs-lookup"><span data-stu-id="ae393-217">If you log on to your app with Facebook,, and then log out and try to log in again with a different Facebook account (using the same browser), you will be immediately logged in to the previous Facebook account you used.</span></span> <span data-ttu-id="ae393-218">要使用其他帐户，您需要导航到 Facebook 并在 Facebook 注销。</span><span class="sxs-lookup"><span data-stu-id="ae393-218">In order to use another account, you need to navigate to Facebook and log out at Facebook.</span></span> <span data-ttu-id="ae393-219">相同的规则适用于任何其他第三方身份验证提供程序。</span><span class="sxs-lookup"><span data-stu-id="ae393-219">The same rule applies to any other 3rd party authentication provider.</span></span> <span data-ttu-id="ae393-220">或者，您可以使用其他浏览器使用其他帐户登录。</span><span class="sxs-lookup"><span data-stu-id="ae393-220">Alternatively, you can log in with another account by using a different browser.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ae393-221">后续步骤</span><span class="sxs-lookup"><span data-stu-id="ae393-221">Next Steps</span></span>

<span data-ttu-id="ae393-222">请参阅介绍[雅虎和LinkedInOAuth安全提供商为OWIN](http://www.jerriepelser.com/blog/introducing-the-yahoo-linkedin-oauth-security-providers-for-owin/)由杰里佩尔瑟雅虎和LinkedIn说明。</span><span class="sxs-lookup"><span data-stu-id="ae393-222">See [Introducing the Yahoo and LinkedIn OAuth security providers for OWIN](http://www.jerriepelser.com/blog/introducing-the-yahoo-linkedin-oauth-security-providers-for-owin/) by Jerrie Pelser for Yahoo and LinkedIn instructions.</span></span> <span data-ttu-id="ae393-223">请参阅 Jerrie 的"漂亮的社交登录按钮"ASP.NET MVC 5，以获得启用社交登录按钮。</span><span class="sxs-lookup"><span data-stu-id="ae393-223">See Jerrie's Pretty social login buttons for ASP.NET MVC 5 to get enable social login buttons.</span></span>

<span data-ttu-id="ae393-224">按照我的教程[创建一个带有 auth 和 SQL DB 的 ASP.NET MVC 应用并部署到 Azure 应用服务](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)，该教程将继续本教程并显示以下内容：</span><span class="sxs-lookup"><span data-stu-id="ae393-224">Follow my tutorial [Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data), which continues this tutorial and shows the following:</span></span>

1. <span data-ttu-id="ae393-225">如何将应用部署到 Azure。</span><span class="sxs-lookup"><span data-stu-id="ae393-225">How to deploy your app to Azure.</span></span>
2. <span data-ttu-id="ae393-226">如何使用角色保护应用。</span><span class="sxs-lookup"><span data-stu-id="ae393-226">How to secure you app with roles.</span></span>
3. <span data-ttu-id="ae393-227">如何使用["需要 Http"](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute(v=vs.108).aspx)和["授权](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.100).aspx)"筛选器保护应用。</span><span class="sxs-lookup"><span data-stu-id="ae393-227">How to secure your app with the [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute(v=vs.108).aspx) and [Authorize](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.100).aspx) filters.</span></span>
4. <span data-ttu-id="ae393-228">如何使用成员资格 API 添加用户和角色。</span><span class="sxs-lookup"><span data-stu-id="ae393-228">How to use the membership API to add users and roles.</span></span>

<span data-ttu-id="ae393-229">请留下反馈，关于你喜欢本教程的方式，以及我们可以改进什么。</span><span class="sxs-lookup"><span data-stu-id="ae393-229">Please leave feedback on how you liked this tutorial and what we could improve.</span></span> <span data-ttu-id="ae393-230">您也可以在["向我展示代码如何](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code)"上请求新主题。</span><span class="sxs-lookup"><span data-stu-id="ae393-230">You can also request new topics at [Show Me How With Code](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code).</span></span> <span data-ttu-id="ae393-231">您甚至可以要求并投票表决要添加到ASP.NET的新功能。</span><span class="sxs-lookup"><span data-stu-id="ae393-231">You can even ask for and vote on new features to be added to ASP.NET.</span></span> <span data-ttu-id="ae393-232">例如，您可以投票选择[创建和管理用户和角色的工具。](http://aspnet.uservoice.com/forums/41199-general-asp-net/suggestions/5646857-asp-net-identity-membership-db-tool-to-mangage-use)</span><span class="sxs-lookup"><span data-stu-id="ae393-232">For example, you can vote for a tool to [create and manage users and roles.](http://aspnet.uservoice.com/forums/41199-general-asp-net/suggestions/5646857-asp-net-identity-membership-db-tool-to-mangage-use)</span></span>

<span data-ttu-id="ae393-233">有关外部身份验证服务ASP.NET工作方式的良好说明，请参阅罗伯特·麦克默里的外部[身份验证服务](https://asp.net/web-api/overview/security/external-authentication-services)。</span><span class="sxs-lookup"><span data-stu-id="ae393-233">For an good explanation of how ASP.NET External Authentication Services work, see Robert McMurray's [External Authentication Services](https://asp.net/web-api/overview/security/external-authentication-services).</span></span> <span data-ttu-id="ae393-234">罗伯特的文章还详细介绍了微软和Twitter的认证。</span><span class="sxs-lookup"><span data-stu-id="ae393-234">Robert's article also goes into detail in enabling Microsoft and Twitter authentication.</span></span> <span data-ttu-id="ae393-235">Tom Dykstra 出色的[EF/MVC 教程](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)展示了如何使用实体框架。</span><span class="sxs-lookup"><span data-stu-id="ae393-235">Tom Dykstra's excellent [EF/MVC tutorial](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) shows how to work with the Entity Framework.</span></span>

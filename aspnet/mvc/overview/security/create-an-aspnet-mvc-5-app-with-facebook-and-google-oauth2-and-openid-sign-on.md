---
uid: mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on
title: 创建 MVC 5 应用程序与 Facebook、 Twitter、 LinkedIn 和 Google OAuth2 登录 (C#) |Microsoft Docs
author: Rick-Anderson
description: 本教程演示如何构建 ASP.NET MVC 5 web 应用程序，使用户能够使用 OAuth 2.0 和外部身份验证的凭据...
ms.author: riande
ms.date: 04/03/2015
ms.assetid: 81ee500f-fc37-40d6-8722-f1b64720fbb6
msc.legacyurl: /mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on
msc.type: authoredcontent
ms.openlocfilehash: 132560c0280a2e4096ea4e9a715c32bc880a8b82
ms.sourcegitcommit: 289e051cc8a90e8f7127e239fda73047bde4de12
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2019
ms.locfileid: "58421422"
---
<a name="create-an-aspnet-mvc-5-app-with-facebook-twitter-linkedin-and-google-oauth2-sign-on-c"></a><span data-ttu-id="26220-103">创建 ASP.NET MVC 5 应用，实现 Facebook、Twitter、LinkedIn 和 Google OAuth2 登录 (C#)</span><span class="sxs-lookup"><span data-stu-id="26220-103">Create an ASP.NET MVC 5 App with Facebook, Twitter, LinkedIn and Google OAuth2 Sign-on (C#)</span></span>
====================
<span data-ttu-id="26220-104">通过[Rick Anderson]((https://twitter.com/RickAndMSFT))</span><span class="sxs-lookup"><span data-stu-id="26220-104">by [Rick Anderson]((https://twitter.com/RickAndMSFT))</span></span>

> <span data-ttu-id="26220-105">本教程演示如何生成使用 ASP.NET MVC 5 web 应用程序，使用户能够登录[OAuth 2.0](http://oauth.net/2/)使用 Facebook、 Twitter、 LinkedIn、 Microsoft 或 Google 之类的外部身份验证提供程序的凭据。</span><span class="sxs-lookup"><span data-stu-id="26220-105">This tutorial shows you how to build an ASP.NET MVC 5 web application that enables users to log in using [OAuth 2.0](http://oauth.net/2/) with credentials from an external authentication provider, such as Facebook, Twitter, LinkedIn, Microsoft, or Google.</span></span> <span data-ttu-id="26220-106">为简单起见，本教程重点介绍使用 Facebook 和 Google 凭据。</span><span class="sxs-lookup"><span data-stu-id="26220-106">For simplicity, this tutorial focuses on working with credentials from Facebook and Google.</span></span>
> 
> <span data-ttu-id="26220-107">启用这些凭据在您的网站中提供一个明显的优势，因为数以百万计的用户已获得与这些外部提供商的帐户。</span><span class="sxs-lookup"><span data-stu-id="26220-107">Enabling these credentials in your web sites provides a significant advantage because millions of users already have accounts with these external providers.</span></span> <span data-ttu-id="26220-108">这些用户可能更倾向于注册为您的网站，如果它们不需要创建和记住一组新的凭据。</span><span class="sxs-lookup"><span data-stu-id="26220-108">These users may be more inclined to sign up for your site if they do not have to create and remember a new set of credentials.</span></span>
> 
> <span data-ttu-id="26220-109">另请参阅[使用 SMS 和电子邮件双因素身份验证的 ASP.NET MVC 5 应用](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="26220-109">See also [ASP.NET MVC 5 app with SMS and email Two-Factor Authentication](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md).</span></span>
> 
> <span data-ttu-id="26220-110">本教程还介绍如何添加配置文件数据的用户，以及如何使用成员资格 API 添加角色。</span><span class="sxs-lookup"><span data-stu-id="26220-110">The tutorial also shows how to add profile data for the user, and how to use the Membership API to add roles.</span></span> <span data-ttu-id="26220-111">本教程由编写[Rick Anderson](https://blogs.msdn.com/rickAndy) (请在 Twitter 上关注我： [ @RickAndMSFT ](https://twitter.com/RickAndMSFT) )。</span><span class="sxs-lookup"><span data-stu-id="26220-111">This tutorial was written by [Rick Anderson](https://blogs.msdn.com/rickAndy) ( Please follow me on Twitter: [@RickAndMSFT](https://twitter.com/RickAndMSFT) ).</span></span>


<a id="start"></a>
## <a name="getting-started"></a><span data-ttu-id="26220-112">入门</span><span class="sxs-lookup"><span data-stu-id="26220-112">Getting Started</span></span>

<span data-ttu-id="26220-113">首先，安装并运行[Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058)或[Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566)。</span><span class="sxs-lookup"><span data-stu-id="26220-113">Start by installing and running [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) or [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566).</span></span> <span data-ttu-id="26220-114">安装 Visual Studio [2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390521)或更高版本。</span><span class="sxs-lookup"><span data-stu-id="26220-114">Install Visual Studio [2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390521) or higher.</span></span> <span data-ttu-id="26220-115">有关 Dropbox、 GitHub、 Linkedin、 Instagram、 缓冲区、 Salesforce、 流、 Stack Exchange、 Tripit、 Twitch、 Twitter、 yahoo ！ 和的详细信息的帮助，请参阅此[示例项目](https://github.com/matthewdunsdon/oauthforaspnet)。</span><span class="sxs-lookup"><span data-stu-id="26220-115">For help with Dropbox, GitHub, Linkedin, Instagram, Buffer, Salesforce, STEAM, Stack Exchange, Tripit, Twitch, Twitter, Yahoo!, and more, see this [sample project](https://github.com/matthewdunsdon/oauthforaspnet).</span></span>

> [!NOTE]
> <span data-ttu-id="26220-116">必须安装 Visual Studio [2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390521)或更高版本使用 Google OAuth 2 和本地调试而无需 SSL 警告。</span><span class="sxs-lookup"><span data-stu-id="26220-116">You must install Visual Studio [2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390521) or higher to use Google OAuth 2 and to debug locally without SSL warnings.</span></span>


<span data-ttu-id="26220-117">单击**新的项目**从**启动**页上，或者可以使用菜单并选择**文件**，然后**新项目**。</span><span class="sxs-lookup"><span data-stu-id="26220-117">Click **New Project** from the **Start** page, or you can use the menu and select **File**, and then **New Project**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image1.png)  
 

<a id="1st"></a>
## <a name="creating-your-first-application"></a><span data-ttu-id="26220-118">创建第一个应用程序</span><span class="sxs-lookup"><span data-stu-id="26220-118">Creating Your First Application</span></span>

<span data-ttu-id="26220-119">单击**新的项目**，然后选择**Visual C#** 在左侧，然后**Web** ，然后选择**ASP.NET Web 应用程序**。</span><span class="sxs-lookup"><span data-stu-id="26220-119">Click **New Project**, then select **Visual C#** on the left, then **Web** and then select **ASP.NET Web Application**.</span></span> <span data-ttu-id="26220-120">"MvcAuth"将项目命名，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="26220-120">Name your project "MvcAuth" and then click **OK**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image2.png)

<span data-ttu-id="26220-121">在中**新建 ASP.NET 项目**对话框中，单击**MVC**。</span><span class="sxs-lookup"><span data-stu-id="26220-121">In the **New ASP.NET Project** dialog, click **MVC**.</span></span> <span data-ttu-id="26220-122">如果身份验证不是**单个用户帐户**，单击**更改身份验证**按钮，然后选择**单个用户帐户**。</span><span class="sxs-lookup"><span data-stu-id="26220-122">If the Authentication is not **Individual User Accounts**, click the **Change Authentication** button and select **Individual User Accounts**.</span></span> <span data-ttu-id="26220-123">通过检查**在云中托管**，应用将为非常轻松地在 Azure 中托管。</span><span class="sxs-lookup"><span data-stu-id="26220-123">By checking **Host in the cloud**, the app will be very easy to host in Azure.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image3.png)

<span data-ttu-id="26220-124">如果所选**在云中托管**，完成配置对话框中。</span><span class="sxs-lookup"><span data-stu-id="26220-124">If you selected **Host in the cloud**, complete the configure dialog.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image4.png)


### <a name="use-nuget-to-update-to-the-latest-owin-middleware"></a><span data-ttu-id="26220-125">使用 NuGet 更新到最新的 OWIN 中间件</span><span class="sxs-lookup"><span data-stu-id="26220-125">Use NuGet to update to the latest OWIN middleware</span></span>

<span data-ttu-id="26220-126">使用 NuGet 包管理器更新[OWIN 中间件](../../../aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana.md)。</span><span class="sxs-lookup"><span data-stu-id="26220-126">Use the NuGet package manager to update the [OWIN middleware](../../../aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana.md).</span></span> <span data-ttu-id="26220-127">选择**更新**在左侧菜单中。</span><span class="sxs-lookup"><span data-stu-id="26220-127">Select **Updates** in the left menu.</span></span> <span data-ttu-id="26220-128">你可以单击**全部更新**按钮也可以搜索仅 OWIN 包 （下一步图中所示）：</span><span class="sxs-lookup"><span data-stu-id="26220-128">You can click on the **Update All** button or you can search for only OWIN packages (shown in the next image):</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image5.png)

<span data-ttu-id="26220-129">在下图显示仅 OWIN 包：</span><span class="sxs-lookup"><span data-stu-id="26220-129">In the image below, only OWIN packages are shown:</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image6.png)

<span data-ttu-id="26220-130">从包管理器控制台 (PMC) 中，您可以输入`Update-Package`命令，将更新所有包。</span><span class="sxs-lookup"><span data-stu-id="26220-130">From the Package Manager Console (PMC), you can enter the `Update-Package` command, which will update all packages.</span></span>

<span data-ttu-id="26220-131">按**F5**或**Ctrl + F5**运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="26220-131">Press **F5** or **Ctrl+F5** to run the application.</span></span> <span data-ttu-id="26220-132">下图中的端口号是 1234年。</span><span class="sxs-lookup"><span data-stu-id="26220-132">In the image below, the port number is 1234.</span></span> <span data-ttu-id="26220-133">当您运行该应用程序时，您将看到不同的端口号。</span><span class="sxs-lookup"><span data-stu-id="26220-133">When you run the application, you'll see a different port number.</span></span>

<span data-ttu-id="26220-134">具体取决于浏览器窗口的大小，可能需要单击导航图标以查看**主页**，**有关**，**联系人**，**注册**并**登录**链接。</span><span class="sxs-lookup"><span data-stu-id="26220-134">Depending on the size of your browser window, you might need to click the navigation icon to see the **Home**, **About**, **Contact**, **Register** and **Log in** links.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image7.png)  
![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image8.png) 

<a id="ssl"></a>
## <a name="setting-up-ssl-in-the-project"></a><span data-ttu-id="26220-135">设置项目中的 SSL</span><span class="sxs-lookup"><span data-stu-id="26220-135">Setting up SSL in the Project</span></span>

<span data-ttu-id="26220-136">若要连接到 Google 和 Facebook 身份验证提供程序，您需要设置为使用 SSL 的 IIS Express。</span><span class="sxs-lookup"><span data-stu-id="26220-136">To connect to authentication providers like Google and Facebook, you will need to set up IIS-Express to use SSL.</span></span> <span data-ttu-id="26220-137">务必要在登录后使用 SSL 来保留和未退回到 HTTP，登录 cookie 是只需为机密作为用户名和密码，也无需使用的 SSL 要通过网络以明文发送它。</span><span class="sxs-lookup"><span data-stu-id="26220-137">It's important to keep using SSL after login and not drop back to HTTP, your login cookie is just as secret as your username and password, and without using SSL you're sending it in clear-text across the wire.</span></span> <span data-ttu-id="26220-138">此外，您已经完成了执行握手和安全通道 （这是使 HTTPS 慢于 HTTP 的大容量） 的时间运行 MVC 管道之前，因此重定向回 HTTP 在登录后不会带来的当前请求或未来请求要快得多。</span><span class="sxs-lookup"><span data-stu-id="26220-138">Besides, you've already taken the time to perform the handshake and secure the channel (which is the bulk of what makes HTTPS slower than HTTP) before the MVC pipeline is run, so redirecting back to HTTP after you're logged in won't make the current request or future requests much faster.</span></span>

1. <span data-ttu-id="26220-139">在中**解决方案资源管理器**，单击**MvcAuth**项目。</span><span class="sxs-lookup"><span data-stu-id="26220-139">In **Solution Explorer**, click the **MvcAuth** project.</span></span>
2. <span data-ttu-id="26220-140">按 F4 键显示项目属性。</span><span class="sxs-lookup"><span data-stu-id="26220-140">Hit the F4 key to show the project properties.</span></span> <span data-ttu-id="26220-141">或者，从**视图**可以选择的菜单**属性窗口**。</span><span class="sxs-lookup"><span data-stu-id="26220-141">Alternatively, from the **View** menu you can select **Properties Window**.</span></span>
3. <span data-ttu-id="26220-142">更改**已启用 SSL**为 True。</span><span class="sxs-lookup"><span data-stu-id="26220-142">Change **SSL Enabled** to True.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image9.png)
4. <span data-ttu-id="26220-143">复制 SSL URL (这将是`https://localhost:44300/`除非你已创建其他 SSL 项目)。</span><span class="sxs-lookup"><span data-stu-id="26220-143">Copy the SSL URL (which will be `https://localhost:44300/` unless you've created other SSL projects).</span></span>
5. <span data-ttu-id="26220-144">在中**解决方案资源管理器**，右键单击**MvcAuth**项目，然后选择**属性**。</span><span class="sxs-lookup"><span data-stu-id="26220-144">In **Solution Explorer**, right click the **MvcAuth** project and select **Properties**.</span></span>
6. <span data-ttu-id="26220-145">选择**Web**选项卡，然后粘贴到 SSL URL**项目 Url**框。</span><span class="sxs-lookup"><span data-stu-id="26220-145">Select the **Web** tab, and then paste the SSL URL into the **Project Url** box.</span></span> <span data-ttu-id="26220-146">保存文件 (Ctl + S)。</span><span class="sxs-lookup"><span data-stu-id="26220-146">Save the file (Ctl+S).</span></span> <span data-ttu-id="26220-147">将需要此 URL 来配置 Facebook 和 Google 身份验证应用。</span><span class="sxs-lookup"><span data-stu-id="26220-147">You will need this URL to configure Facebook and Google authentication apps.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image10.png)
7. <span data-ttu-id="26220-148">添加[RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx)属性为`Home`控制器需要的所有请求必须使用 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="26220-148">Add the [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) attribute to the `Home` controller to require all requests must use HTTPS.</span></span> <span data-ttu-id="26220-149">更安全的方法是将添加[RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx)筛选器添加到应用程序。</span><span class="sxs-lookup"><span data-stu-id="26220-149">A more secure approach is to add the [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) filter to the application.</span></span> <span data-ttu-id="26220-150">请参阅的部分&quot;保护应用程序使用 SSL 和 Authorize 属性&quot;在我的教程[使用身份验证和 SQL 数据库创建 ASP.NET MVC 应用并将其部署到 Azure 应用服务](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)。</span><span class="sxs-lookup"><span data-stu-id="26220-150">See the section &quot;Protect the Application with SSL and the Authorize Attribute&quot; in my tutorial [Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span></span> <span data-ttu-id="26220-151">下面显示了主控制器的一部分。</span><span class="sxs-lookup"><span data-stu-id="26220-151">A portion of the Home controller is shown below.</span></span>

    [!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample1.cs?highlight=1)]
8. <span data-ttu-id="26220-152">按 Ctrl+F5 运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="26220-152">Press CTRL+F5 to run the application.</span></span> <span data-ttu-id="26220-153">如果在过去，在已安装了证书，可以跳过本部分的其余部分并跳转到[OAuth 2 中创建的 Google 应用程序和应用连接到该项目](#goog)，否则，请按照说明信任自签名IIS Express 已生成的证书。</span><span class="sxs-lookup"><span data-stu-id="26220-153">If you've installed the certificate in the past, you can skip the rest of this section and jump to [Creating a Google app for OAuth 2 and connecting the app to the project](#goog), otherwise, follow the instructions to trust the self-signed certificate that IIS Express has generated.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image11.png)
9. <span data-ttu-id="26220-154">读取**安全警告**对话框，然后再单击**是**如果你想要安装表示本地主机的证书。</span><span class="sxs-lookup"><span data-stu-id="26220-154">Read the **Security Warning** dialog and then click **Yes** if you want to install the certificate representing localhost.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image12.png)
10. <span data-ttu-id="26220-155">IE 会显示*主页*页上并不会出现 SSL 警告。</span><span class="sxs-lookup"><span data-stu-id="26220-155">IE shows the *Home* page and there are no SSL warnings.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image13.png)
11. <span data-ttu-id="26220-156">Google Chrome 也接受证书并将显示 HTTPS 内容而不发出警告。</span><span class="sxs-lookup"><span data-stu-id="26220-156">Google Chrome also accepts the certificate and will show HTTPS content without a warning.</span></span> <span data-ttu-id="26220-157">Firefox 会使用其自己的证书存储，因此它将显示一条警告。</span><span class="sxs-lookup"><span data-stu-id="26220-157">Firefox uses its own certificate store, so it will display a warning.</span></span> <span data-ttu-id="26220-158">对于我们的应用程序，你可以安全地单击**我了解风险**。</span><span class="sxs-lookup"><span data-stu-id="26220-158">For our application you can safely click **I Understand the Risks**.</span></span>   
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image14.png)

<a id="goog"></a>
## <a name="creating-a-google-app-for-oauth-2-and-connecting-the-app-to-the-project"></a><span data-ttu-id="26220-159">为 OAuth 2 中创建的 Google 应用程序和应用程序连接到项目</span><span class="sxs-lookup"><span data-stu-id="26220-159">Creating a Google app for OAuth 2 and connecting the app to the project</span></span>

> [!WARNING]
> <span data-ttu-id="26220-160">当前的 Google OAuth 说明，请参阅[ASP.NET Core 中的配置 Google 身份验证](/aspnet/core/security/authentication/social/google-logins)。</span><span class="sxs-lookup"><span data-stu-id="26220-160">For current Google OAuth instructions, see [Configuring Google authentication in ASP.NET Core](/aspnet/core/security/authentication/social/google-logins).</span></span>

1. <span data-ttu-id="26220-161">导航到[Google 开发人员控制台](https://console.developers.google.com/)。</span><span class="sxs-lookup"><span data-stu-id="26220-161">Navigate to the [Google Developers Console](https://console.developers.google.com/).</span></span>
2. <span data-ttu-id="26220-162">如果尚未创建的项目之前，请选择**凭据**在左侧选项卡，然后选择**创建**。</span><span class="sxs-lookup"><span data-stu-id="26220-162">If you haven't created a project before, select **Credentials** in the left tab, and then select **Create**.</span></span>
3. <span data-ttu-id="26220-163">在左侧选项卡中，单击**凭据**。</span><span class="sxs-lookup"><span data-stu-id="26220-163">In the left tab, click **Credentials**.</span></span>
4. <span data-ttu-id="26220-164">单击**创建凭据**然后**OAuth 客户端 ID**。</span><span class="sxs-lookup"><span data-stu-id="26220-164">Click **Create credentials** then **OAuth client ID**.</span></span> 

    1. <span data-ttu-id="26220-165">在中**创建客户端 ID**对话框中，保留默认**Web 应用程序**为应用程序类型。</span><span class="sxs-lookup"><span data-stu-id="26220-165">In the **Create Client ID** dialog, keep the default **Web application** for the application type.</span></span>
    2. <span data-ttu-id="26220-166">设置**授权的 JavaScript**上面使用的 SSL url 的来源 (`https://localhost:44300/`除非你已创建其他 SSL 项目)</span><span class="sxs-lookup"><span data-stu-id="26220-166">Set the **Authorized JavaScript** origins to the SSL URL you used above (`https://localhost:44300/` unless you've created other SSL projects)</span></span>
    3. <span data-ttu-id="26220-167">设置**已授权重定向 URI**到：</span><span class="sxs-lookup"><span data-stu-id="26220-167">Set the **Authorized redirect URI** to:</span></span>  
         `https://localhost:44300/signin-google`
5. <span data-ttu-id="26220-168">单击 OAuth 许可屏幕菜单项，然后设置你的电子邮件地址和产品名称。</span><span class="sxs-lookup"><span data-stu-id="26220-168">Click the OAuth Consent screen menu item, then set your email address and product name.</span></span> <span data-ttu-id="26220-169">当您完成窗体中单击**保存**。</span><span class="sxs-lookup"><span data-stu-id="26220-169">When you have completed the form click **Save**.</span></span>
6. <span data-ttu-id="26220-170">单击库菜单项，搜索**Google + API**，单击它，然后按启用。</span><span class="sxs-lookup"><span data-stu-id="26220-170">Click the Library menu item, search **Google+ API**, click on it then press Enable.</span></span>
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image15.png)  
  
   <span data-ttu-id="26220-171">下图显示了已启用的 Api。</span><span class="sxs-lookup"><span data-stu-id="26220-171">The image below shows the enabled APIs.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image16.png)
7. <span data-ttu-id="26220-172">从 Google Api API 管理器中，请访问**凭据**选项卡来获取**客户端 ID**。</span><span class="sxs-lookup"><span data-stu-id="26220-172">From the Google APIs API Manager, visit the **Credentials** tab to obtain the **Client ID**.</span></span> <span data-ttu-id="26220-173">若要使用应用程序机密保存 JSON 文件的下载。</span><span class="sxs-lookup"><span data-stu-id="26220-173">Download to save a JSON file with application secrets.</span></span> <span data-ttu-id="26220-174">复制并粘贴**ClientId**并**ClientSecret**到`UseGoogleAuthentication`方法中找到*Startup.Auth.cs*文件*App_Start*文件夹。</span><span class="sxs-lookup"><span data-stu-id="26220-174">Copy and paste the **ClientId** and **ClientSecret** into the `UseGoogleAuthentication` method found in the *Startup.Auth.cs* file in the *App_Start* folder.</span></span> <span data-ttu-id="26220-175">**ClientId**并**ClientSecret**如下所示的值是示例，它们不起作用。</span><span class="sxs-lookup"><span data-stu-id="26220-175">The **ClientId** and **ClientSecret** values shown below are samples and don't work.</span></span>

    [!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample2.cs?highlight=37-39)]

    > [!WARNING]
    > <span data-ttu-id="26220-176">安全性-永远不会存储在源代码中敏感数据。</span><span class="sxs-lookup"><span data-stu-id="26220-176">Security - Never store sensitive data in your source code.</span></span> <span data-ttu-id="26220-177">帐户和凭据添加到上面的代码以使示例保持简单。</span><span class="sxs-lookup"><span data-stu-id="26220-177">The account and credentials are added to the code above to keep the sample simple.</span></span> <span data-ttu-id="26220-178">请参阅[的密码和其他敏感数据部署到 ASP.NET 和 Azure 应用服务最佳做法](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)。</span><span class="sxs-lookup"><span data-stu-id="26220-178">See [Best practices for deploying passwords and other sensitive data to ASP.NET and Azure App Service](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md).</span></span>
8. <span data-ttu-id="26220-179">按**CTRL + F5**生成并运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="26220-179">Press **CTRL+F5** to build and run the application.</span></span> <span data-ttu-id="26220-180">单击**登录**链接。</span><span class="sxs-lookup"><span data-stu-id="26220-180">Click the **Log in** link.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image17.png)
9. <span data-ttu-id="26220-181">下**使用其他服务进行登录**，单击**Google**。</span><span class="sxs-lookup"><span data-stu-id="26220-181">Under **Use another service to log in**, click **Google**.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image18.png)

    > [!NOTE]
    > <span data-ttu-id="26220-182">如果您错过任何上述步骤将获取 HTTP 401 错误。</span><span class="sxs-lookup"><span data-stu-id="26220-182">If you miss any of the steps above you will get a HTTP 401 error.</span></span> <span data-ttu-id="26220-183">重新检查上述步骤。</span><span class="sxs-lookup"><span data-stu-id="26220-183">Recheck your steps above.</span></span> <span data-ttu-id="26220-184">如果你缺少所需的设置 (例如**产品名称**)、 添加缺少的项，并保存; 可能需要几分钟时间验证才能工作。</span><span class="sxs-lookup"><span data-stu-id="26220-184">If you miss a required setting (for example **product name**), add the missing item and save; it can take a few minutes for authentication to work.</span></span>
10. <span data-ttu-id="26220-185">你将重定向到 Google 站点将在其中输入你的凭据。</span><span class="sxs-lookup"><span data-stu-id="26220-185">You will be redirected to the Google site where you will enter your credentials.</span></span>   
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image19.png)
11. <span data-ttu-id="26220-186">输入你的凭据后，您将会提示您刚创建的 web 应用程序对其授予权限：</span><span class="sxs-lookup"><span data-stu-id="26220-186">After you enter your credentials, you will be prompted to give permissions to the web application you just created:</span></span>
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image20.png)
12. <span data-ttu-id="26220-187">单击**接受**。</span><span class="sxs-lookup"><span data-stu-id="26220-187">Click **Accept**.</span></span> <span data-ttu-id="26220-188">你将立即重定向回**注册**MvcAuth 应用程序可以在其中注册你的 Google 帐户页。</span><span class="sxs-lookup"><span data-stu-id="26220-188">You will now be redirected back to the **Register** page of the MvcAuth application where you can register your Google account.</span></span> <span data-ttu-id="26220-189">可以选择更改 Gmail 帐户使用的本地电子邮件注册名称，但你通常想要保留的默认电子邮件别名 （即，一个用于身份验证）。</span><span class="sxs-lookup"><span data-stu-id="26220-189">You have the option of changing the local email registration name used for your Gmail account, but you generally want to keep the default email alias (that is, the one you used for authentication).</span></span> <span data-ttu-id="26220-190">单击“注册”。</span><span class="sxs-lookup"><span data-stu-id="26220-190">Click **Register**.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image21.png)

<a id="fb"></a>
## <a name="creating-the-app-in-facebook-and-connecting-the-app-to-the-project"></a><span data-ttu-id="26220-191">在 Facebook 中创建应用并将应用程序连接到项目</span><span class="sxs-lookup"><span data-stu-id="26220-191">Creating the app in Facebook and connecting the app to the project</span></span>

> [!WARNING]
> <span data-ttu-id="26220-192">当前 Facebook OAuth2 身份验证说明，请参阅[配置 Facebook 身份验证](/aspnet/core/security/authentication/social/facebook-logins)</span><span class="sxs-lookup"><span data-stu-id="26220-192">For current Facebook OAuth2 authentication instructions, see [Configuring Facebook authentication](/aspnet/core/security/authentication/social/facebook-logins)</span></span>


<a id="mdb"></a>
## <a name="examine-the-membership-data"></a><span data-ttu-id="26220-193">检查成员身份数据</span><span class="sxs-lookup"><span data-stu-id="26220-193">Examine the Membership Data</span></span>

<span data-ttu-id="26220-194">在中**视图**菜单上，单击**服务器资源管理器**。</span><span class="sxs-lookup"><span data-stu-id="26220-194">In the **View** menu, click **Server Explorer**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image32.png)

<span data-ttu-id="26220-195">展开**DefaultConnection (MvcAuth)**，展开**表**，右键单击**AspNetUsers**然后单击**显示表数据**。</span><span class="sxs-lookup"><span data-stu-id="26220-195">Expand **DefaultConnection (MvcAuth)**, expand **Tables**, right click **AspNetUsers** and click **Show Table Data**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image33.png)

![aspnetusers 表数据](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image34.png)

<a id="ap"></a>
## <a name="adding-profile-data-to-the-user-class"></a><span data-ttu-id="26220-197">将配置文件数据添加到用户类</span><span class="sxs-lookup"><span data-stu-id="26220-197">Adding Profile Data to the User Class</span></span>

<span data-ttu-id="26220-198">在本部分中您将添加出生日期和家庭城镇对用户数据在注册期间，在下图中所示。</span><span class="sxs-lookup"><span data-stu-id="26220-198">In this section you'll add birth date and home town to the user data during registration, as shown in the following image.</span></span>

![使用家庭城镇和 Bday reg](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image35.png)

<span data-ttu-id="26220-200">打开*Models\IdentityModels.cs*文件，并添加出生日期和主页城镇属性：</span><span class="sxs-lookup"><span data-stu-id="26220-200">Open the *Models\IdentityModels.cs* file and add birth date and home town properties:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample4.cs?highlight=3-4)]

<span data-ttu-id="26220-201">打开*Models\AccountViewModels.cs*文件和组出生日期和主页中的城镇属性`ExternalLoginConfirmationViewModel`。</span><span class="sxs-lookup"><span data-stu-id="26220-201">Open the *Models\AccountViewModels.cs* file and the set birth date and home town properties in `ExternalLoginConfirmationViewModel`.</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample5.cs?highlight=8-9)]

<span data-ttu-id="26220-202">打开*Controllers\AccountController.cs*文件，并添加代码中的出生日期和主页城镇`ExternalLoginConfirmation`操作方法所示：</span><span class="sxs-lookup"><span data-stu-id="26220-202">Open the *Controllers\AccountController.cs* file and add code for birth date and home town in the `ExternalLoginConfirmation` action method as shown:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample6.cs?highlight=21-23)]

<span data-ttu-id="26220-203">添加出生日期和到主城镇*Views\Account\ExternalLoginConfirmation.cshtml*文件：</span><span class="sxs-lookup"><span data-stu-id="26220-203">Add birth date and home town to the *Views\Account\ExternalLoginConfirmation.cshtml* file:</span></span>

[!code-cshtml[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample7.cshtml?highlight=27-40)]

<span data-ttu-id="26220-204">删除成员资格数据库，使您可以再次使用你的应用程序注册你的 Facebook 帐户并验证可以添加新的出生日期和家庭城镇配置文件信息。</span><span class="sxs-lookup"><span data-stu-id="26220-204">Delete the membership database so you can again register your Facebook account with your application and verify you can add the new birth date and home town profile information.</span></span>

<span data-ttu-id="26220-205">从**解决方案资源管理器**，单击**显示所有文件**图标，然后右键单击*添加\_Data\aspnet-MvcAuth-&lt;日期戳&gt;.mdf*然后单击**删除**。</span><span class="sxs-lookup"><span data-stu-id="26220-205">From **Solution Explorer**, click the **Show All Files** icon, then right click *Add\_Data\aspnet-MvcAuth-&lt;dateStamp&gt;.mdf* and click **Delete**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image36.png)

<span data-ttu-id="26220-206">从**工具**菜单上，单击**NuGet 包管理器**，然后单击**程序包管理器控制台**(PMC)。</span><span class="sxs-lookup"><span data-stu-id="26220-206">From the **Tools** menu, click **NuGet Package Manger**, then click **Package Manager Console** (PMC).</span></span> <span data-ttu-id="26220-207">在 PMC 中输入以下命令。</span><span class="sxs-lookup"><span data-stu-id="26220-207">Enter the following commands in the PMC.</span></span>

1. <span data-ttu-id="26220-208">启用迁移</span><span class="sxs-lookup"><span data-stu-id="26220-208">Enable-Migrations</span></span>
2. <span data-ttu-id="26220-209">添加迁移 Init</span><span class="sxs-lookup"><span data-stu-id="26220-209">Add-Migration Init</span></span>
3. <span data-ttu-id="26220-210">Update-Database</span><span class="sxs-lookup"><span data-stu-id="26220-210">Update-Database</span></span>

<span data-ttu-id="26220-211">运行应用程序并使用 FaceBook 和 Google 登录并注册某些用户。</span><span class="sxs-lookup"><span data-stu-id="26220-211">Run the application and use FaceBook and Google to log in and register some users.</span></span>

## <a name="examine-the-membership-data"></a><span data-ttu-id="26220-212">检查成员身份数据</span><span class="sxs-lookup"><span data-stu-id="26220-212">Examine the Membership Data</span></span>

<span data-ttu-id="26220-213">在中**视图**菜单上，单击**服务器资源管理器**。</span><span class="sxs-lookup"><span data-stu-id="26220-213">In the **View** menu, click **Server Explorer**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image37.png)

<span data-ttu-id="26220-214">右键单击**AspNetUsers**然后单击**显示表数据**。</span><span class="sxs-lookup"><span data-stu-id="26220-214">Right click **AspNetUsers** and click **Show Table Data**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image38.png)

<span data-ttu-id="26220-215">`HomeTown`和`BirthDate`字段如下所示。</span><span class="sxs-lookup"><span data-stu-id="26220-215">The `HomeTown` and `BirthDate` fields are shown below.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image39.png)

<a id="off"></a>
## <a name="logging-off-your-app-and-logging-in-with-another-account"></a><span data-ttu-id="26220-216">您的应用程序中注销并使用另一个帐户中的日志记录</span><span class="sxs-lookup"><span data-stu-id="26220-216">Logging off your App and Logging in With Another Account</span></span>

<span data-ttu-id="26220-217">如果使用 Facebook、 向应用登录，然后注销并尝试登录再次使用其他 Facebook 帐户 （使用的同一浏览器），你将立即登录到您使用的上一个 Facebook 帐户。</span><span class="sxs-lookup"><span data-stu-id="26220-217">If you log on to your app with Facebook,, and then log out and try to log in again with a different Facebook account (using the same browser), you will be immediately logged in to the previous Facebook account you used.</span></span> <span data-ttu-id="26220-218">若要使用另一个帐户，需要导航到 Facebook，然后在 Facebook 上注销。</span><span class="sxs-lookup"><span data-stu-id="26220-218">In order to use another account, you need to navigate to Facebook and log out at Facebook.</span></span> <span data-ttu-id="26220-219">同一规则适用于任何其他第三方身份验证提供程序。</span><span class="sxs-lookup"><span data-stu-id="26220-219">The same rule applies to any other 3rd party authentication provider.</span></span> <span data-ttu-id="26220-220">或者，您可以将另一个帐户登录使用不同的浏览器。</span><span class="sxs-lookup"><span data-stu-id="26220-220">Alternatively, you can log in with another account by using a different browser.</span></span>

## <a name="next-steps"></a><span data-ttu-id="26220-221">后续步骤</span><span class="sxs-lookup"><span data-stu-id="26220-221">Next Steps</span></span>

<span data-ttu-id="26220-222">请参阅[引入 owin Yahoo 和 LinkedIn OAuth 安全提供程序](http://www.jerriepelser.com/blog/introducing-the-yahoo-linkedin-oauth-security-providers-for-owin/)通过 Jerrie Pelser 有关 Yahoo 和 LinkedIn 的说明。</span><span class="sxs-lookup"><span data-stu-id="26220-222">See [Introducing the Yahoo and LinkedIn OAuth security providers for OWIN](http://www.jerriepelser.com/blog/introducing-the-yahoo-linkedin-oauth-security-providers-for-owin/) by Jerrie Pelser for Yahoo and LinkedIn instructions.</span></span> <span data-ttu-id="26220-223">请参阅 Jerrie 的美观社交登录按钮的 ASP.NET MVC 5，获取启用社交登录按钮。</span><span class="sxs-lookup"><span data-stu-id="26220-223">See Jerrie's Pretty social login buttons for ASP.NET MVC 5 to get enable social login buttons.</span></span>

<span data-ttu-id="26220-224">请遵循我的教程[使用身份验证和 SQL 数据库创建 ASP.NET MVC 应用并将其部署到 Azure 应用服务](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)，它将继续本教程并显示以下：</span><span class="sxs-lookup"><span data-stu-id="26220-224">Follow my tutorial [Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data), which continues this tutorial and shows the following:</span></span>

1. <span data-ttu-id="26220-225">如何将应用部署到 Azure。</span><span class="sxs-lookup"><span data-stu-id="26220-225">How to deploy your app to Azure.</span></span>
2. <span data-ttu-id="26220-226">如何保护应用程序与角色。</span><span class="sxs-lookup"><span data-stu-id="26220-226">How to secure you app with roles.</span></span>
3. <span data-ttu-id="26220-227">如何保护应用程序与[RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute(v=vs.108).aspx)并[Authorize](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.100).aspx)筛选器。</span><span class="sxs-lookup"><span data-stu-id="26220-227">How to secure your app with the [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute(v=vs.108).aspx) and [Authorize](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.100).aspx) filters.</span></span>
4. <span data-ttu-id="26220-228">如何使用成员资格 API 来添加用户和角色。</span><span class="sxs-lookup"><span data-stu-id="26220-228">How to use the membership API to add users and roles.</span></span>

<span data-ttu-id="26220-229">请在你喜欢本教程的内容，我们可以提高上留下反馈。</span><span class="sxs-lookup"><span data-stu-id="26220-229">Please leave feedback on how you liked this tutorial and what we could improve.</span></span> <span data-ttu-id="26220-230">此外可以请求新主题[教我代码](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code)。</span><span class="sxs-lookup"><span data-stu-id="26220-230">You can also request new topics at [Show Me How With Code](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code).</span></span> <span data-ttu-id="26220-231">甚至可以请求并对要添加到 ASP.NET 的新功能进行投票。</span><span class="sxs-lookup"><span data-stu-id="26220-231">You can even ask for and vote on new features to be added to ASP.NET.</span></span> <span data-ttu-id="26220-232">例如，可以投票到工具[创建和管理用户和角色。](http://aspnet.uservoice.com/forums/41199-general-asp-net/suggestions/5646857-asp-net-identity-membership-db-tool-to-mangage-use)</span><span class="sxs-lookup"><span data-stu-id="26220-232">For example, you can vote for a tool to [create and manage users and roles.](http://aspnet.uservoice.com/forums/41199-general-asp-net/suggestions/5646857-asp-net-identity-membership-db-tool-to-mangage-use)</span></span>

<span data-ttu-id="26220-233">有关 ASP.NET 外部身份验证服务的工作方式的很好的说明，请参阅 Robert McMurray[外部身份验证服务](https://asp.net/web-api/overview/security/external-authentication-services)。</span><span class="sxs-lookup"><span data-stu-id="26220-233">For an good explanation of how ASP.NET External Authentication Services work, see Robert McMurray's [External Authentication Services](https://asp.net/web-api/overview/security/external-authentication-services).</span></span> <span data-ttu-id="26220-234">Robert 的文章还介绍在启用 Microsoft 和 Twitter 身份验证的详细信息。</span><span class="sxs-lookup"><span data-stu-id="26220-234">Robert's article also goes into detail in enabling Microsoft and Twitter authentication.</span></span> <span data-ttu-id="26220-235">Tom Dykstra 的绝佳[EF/MVC 教程](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)演示如何使用实体框架。</span><span class="sxs-lookup"><span data-stu-id="26220-235">Tom Dykstra's excellent [EF/MVC tutorial](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) shows how to work with the Entity Framework.</span></span>

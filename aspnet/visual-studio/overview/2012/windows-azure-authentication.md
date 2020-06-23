---
uid: visual-studio/overview/2012/windows-azure-authentication
title: Windows Azure 身份验证 |Microsoft Docs
author: Rick-Anderson
description: 适用于 Windows Azure Active Directory 的 Microsoft ASP.NET 工具使为在 Microsoft Azure 网站上托管的 web 应用程序启用身份验证变得简单 ...。
ms.author: riande
ms.date: 02/20/2013
ms.assetid: a3cef801-a54b-4ebd-93c3-55764e2e14b1
msc.legacyurl: /visual-studio/overview/2012/windows-azure-authentication
msc.type: authoredcontent
ms.openlocfilehash: ab75218cbe3817c14a064e9816388aebc7e431f7
ms.sourcegitcommit: 0cf7d06071a8ff986e6c028ac9daf0c0e7490412
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/23/2020
ms.locfileid: "85240557"
---
# <a name="windows-azure-authentication"></a><span data-ttu-id="0f8a9-103">Microsoft Azure 身份验证</span><span class="sxs-lookup"><span data-stu-id="0f8a9-103">Windows Azure Authentication</span></span>

<span data-ttu-id="0f8a9-104">作者： [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="0f8a9-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> <span data-ttu-id="0f8a9-105">适用于 Windows Azure Active Directory Microsoft ASP.NET 工具使为[Microsoft Azure 网站](https://www.windowsazure.com/home/features/web-sites/)上托管的 web 应用程序启用身份验证变得简单。</span><span class="sxs-lookup"><span data-stu-id="0f8a9-105">Microsoft ASP.NET tools for Windows Azure Active Directory makes it simple to enable authentication for web applications hosted on [Windows Azure Web Sites](https://www.windowsazure.com/home/features/web-sites/).</span></span> <span data-ttu-id="0f8a9-106">您可以使用 Microsoft Azure 身份验证对您的组织中的 Office 365 用户进行身份验证、从您的本地 Active Directory 或用户在自己的自定义 Windows Azure Active Directory 域中创建的用户进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="0f8a9-106">You can use Windows Azure Authentication to authenticate Office 365 users from your organization, corporate accounts synced from your on-premise Active Directory or users created in your own custom Windows Azure Active Directory domain.</span></span> <span data-ttu-id="0f8a9-107">启用 Windows Azure 身份验证可以将应用程序配置为使用单个[Windows Azure Active Directory](https://docs.microsoft.com/azure/active-directory/)租户对用户进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="0f8a9-107">Enabling Windows Azure Authentication configures your application to authenticate users using a single [Windows Azure Active Directory](https://docs.microsoft.com/azure/active-directory/) tenant.</span></span>
>
> <span data-ttu-id="0f8a9-108">云服务中的 web 角色不支持 ASP.NET Windows Azure 身份验证工具，但我们计划在未来的版本中执行此操作。</span><span class="sxs-lookup"><span data-stu-id="0f8a9-108">The ASP.NET Windows Azure Authentication tool is not supported for web roles in a cloud service but we plan to do so in a future release.</span></span> <span data-ttu-id="0f8a9-109">Windows Azure web 角色支持[Windows Identity Foundation](https://msdn.microsoft.com/library/hh291066(v=VS.110).aspx) （WIF）。</span><span class="sxs-lookup"><span data-stu-id="0f8a9-109">[Windows Identity Foundation](https://msdn.microsoft.com/library/hh291066(v=VS.110).aspx) (WIF) is supported in Windows Azure web roles.</span></span>
>
> <span data-ttu-id="0f8a9-110">有关如何在本地 Active Directory 和 Windows Azure Active Directory 租户之间设置同步的详细信息，请参阅[使用 AD FS 2.0 实现和管理单一登录](https://technet.microsoft.com/library/jj205462.aspx)。</span><span class="sxs-lookup"><span data-stu-id="0f8a9-110">For details on how to setup synchronization between your on-premise Active Directory and your Windows Azure Active Directory tenant please see [Use AD FS 2.0 to implement and manage single sign-on](https://technet.microsoft.com/library/jj205462.aspx).</span></span>
>
> <span data-ttu-id="0f8a9-111">Windows Azure Active Directory 当前以[免费预览版服务](https://azure.microsoft.com/free/dotnet/)的形式提供。</span><span class="sxs-lookup"><span data-stu-id="0f8a9-111">Windows Azure Active Directory is currently available as a [free preview service](https://azure.microsoft.com/free/dotnet/).</span></span>

## <a name="requirements"></a><span data-ttu-id="0f8a9-112">要求：</span><span class="sxs-lookup"><span data-stu-id="0f8a9-112">Requirements:</span></span>

- <span data-ttu-id="0f8a9-113">Visual Studio 2012 或[Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express)</span><span class="sxs-lookup"><span data-stu-id="0f8a9-113">Visual Studio 2012 or [Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express)</span></span>
- <span data-ttu-id="0f8a9-114">用于 Visual Studio Express 2012 的 Visual Studio 2012 或[Web Tools 扩展](https://go.microsoft.com/fwlink/?LinkID=282231&amp;clcid=0x409)[的 web 工具扩展](https://go.microsoft.com/fwlink/?LinkID=282228&amp;clcid=0x409)</span><span class="sxs-lookup"><span data-stu-id="0f8a9-114">[Web Tools Extensions for Visual Studio 2012](https://go.microsoft.com/fwlink/?LinkID=282228&amp;clcid=0x409) or [Web Tools Extensions for Visual Studio Express 2012](https://go.microsoft.com/fwlink/?LinkID=282231&amp;clcid=0x409)</span></span>
- <span data-ttu-id="0f8a9-115">[适用于 windows Azure Active Directory 的 Microsoft ASP.NET 工具– Visual Studio 2012](https://go.microsoft.com/fwlink/?LinkID=282306)或[适用于 Windows 的 Microsoft ASP.NET 工具 Azure Active Directory – Visual Studio Express 2012 for Web](https://go.microsoft.com/fwlink/?LinkId=282652)</span><span class="sxs-lookup"><span data-stu-id="0f8a9-115">[Microsoft ASP.NET Tools for Windows Azure Active Directory – Visual Studio 2012](https://go.microsoft.com/fwlink/?LinkID=282306) or [Microsoft ASP.NET Tools for Windows Azure Active Directory – Visual Studio Express 2012 for Web](https://go.microsoft.com/fwlink/?LinkId=282652)</span></span>

## <a name="create-an-aspnet-web-application-with-visual-studio-2012"></a><span data-ttu-id="0f8a9-116">使用 Visual Studio 2012 创建 ASP.NET Web 应用程序</span><span class="sxs-lookup"><span data-stu-id="0f8a9-116">Create an ASP.NET Web Application with Visual Studio 2012</span></span>

<span data-ttu-id="0f8a9-117">您可以使用 Visual Studio 2012 创建任何 Web 应用程序，本教程使用 ASP.NET MVC intranet 模板。</span><span class="sxs-lookup"><span data-stu-id="0f8a9-117">You can create any Web Application with Visual Studio 2012, this tutorial uses the ASP.NET MVC intranet template.</span></span>

1. <span data-ttu-id="0f8a9-118">创建新的 ASP.NET MVC 4 Intranet 应用程序并接受所有默认值。</span><span class="sxs-lookup"><span data-stu-id="0f8a9-118">Create a new ASP.NET MVC 4 Intranet Application and accept all the defaults.</span></span> <span data-ttu-id="0f8a9-119">（它必须是**tra** net 中的，而不是**t** net 项目中）。</span><span class="sxs-lookup"><span data-stu-id="0f8a9-119">(It must be an In **tra** net and not In **ter** net project).</span></span>
     ![](windows-azure-authentication/_static/image1.png)

## <a name="enable-window-azure-authentication-when-you-are-a-global-administrator-of-the-tenet"></a><span data-ttu-id="0f8a9-120">启用 Window Azure 身份验证（如果是原则的全局管理员）</span><span class="sxs-lookup"><span data-stu-id="0f8a9-120">Enable Window Azure Authentication (When you are a Global Administrator of the Tenet)</span></span>

<span data-ttu-id="0f8a9-121">如果你没有现有的 Windows Azure Active Directory 租户（例如，通过现有的 Office 365 帐户），则可以通过注册[新的 windows Azure Active Directory 帐户](https://g.microsoftonline.com/0AX00en/5)来创建新租户。</span><span class="sxs-lookup"><span data-stu-id="0f8a9-121">If you do not have an existing Windows Azure Active Directory tenant (For example, through an existing Office 365 account) you can create a new tenant by signing up for a [new Windows Azure Active Directory account](https://g.microsoftonline.com/0AX00en/5).</span></span>

1. <span data-ttu-id="0f8a9-122">从 "项目" 菜单中选择 "**启用 Microsoft Azure 身份验证**"：</span><span class="sxs-lookup"><span data-stu-id="0f8a9-122">From the Project menu select **Enable Windows Azure Authentication**:</span></span>

   ![](windows-azure-authentication/_static/image2.png)

2. <span data-ttu-id="0f8a9-123">输入 Windows Azure Active Directory 租户的域（例如 contoso.onmicrosoft.com），然后单击 "**启用**"：</span><span class="sxs-lookup"><span data-stu-id="0f8a9-123">Enter the domain for your Windows Azure Active Directory tenant (for example, contoso.onmicrosoft.com) and click **Enable**:</span></span>

![](windows-azure-authentication/_static/image3.png)

3. <span data-ttu-id="0f8a9-124">在 Web 身份验证对话框中，以管理员身份登录 Windows Azure Active Directory 租户：</span><span class="sxs-lookup"><span data-stu-id="0f8a9-124">In the Web Authentication dialog sign in as an administrator for your Windows Azure Active Directory tenant:</span></span>

   ![](windows-azure-authentication/_static/image4.png)

![](windows-azure-authentication/_static/image5.png)

## <a name="enable-window-azure-by-a-non-administrator-of-the-tenet"></a><span data-ttu-id="0f8a9-125">通过原则的非管理员启用 Window Azure</span><span class="sxs-lookup"><span data-stu-id="0f8a9-125">Enable Window Azure by a non-administrator of the Tenet</span></span>

<span data-ttu-id="0f8a9-126">如果你没有 Windows Azure Active Directory 租户的全局管理员权限，则可以取消选中用于预配应用程序的复选框。</span><span class="sxs-lookup"><span data-stu-id="0f8a9-126">If you do not have Global Administrator privilege for your Windows Azure Active Directory tenant, you can uncheck the checkbox for provisioning the application.</span></span>

![](windows-azure-authentication/_static/image6.png)

<span data-ttu-id="0f8a9-127">此对话框将显示使用 Azure Active Directory 原则预配应用程序所需的 "**域**"、"**应用程序主体 Id** " 和 "**答复 URL** "。</span><span class="sxs-lookup"><span data-stu-id="0f8a9-127">The dialog will display the **Domain**, **Application Principal Id** and **Reply URL** which are required for provisioning the application with an Azure Active Directory tenet.</span></span> <span data-ttu-id="0f8a9-128">需要将此信息提供给有足够权限来预配应用程序的人员。</span><span class="sxs-lookup"><span data-stu-id="0f8a9-128">You need to give this information to someone who has sufficient privilege to provision the application.</span></span> <span data-ttu-id="0f8a9-129">有关如何使用 cmdlet 来手动创建服务主体的详细信息，请参阅[如何使用 Windows Azure Active Directory ASP.NET 应用程序实现单一登录](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect)。</span><span class="sxs-lookup"><span data-stu-id="0f8a9-129">See[How to implement single sign-on with Windows Azure Active Directory - ASP.NET Application](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) for details on how to use cmdlet to create the service principal manually.</span></span>
<span data-ttu-id="0f8a9-130">成功预配应用程序后，可以单击 "继续"**以更新具有所选设置的 web.config**。</span><span class="sxs-lookup"><span data-stu-id="0f8a9-130">Once the application has been successfully provisioned, you can click on **Continue to update web.config with the selected settings**.</span></span> <span data-ttu-id="0f8a9-131">如果要在等待预配发生的同时继续开发应用程序，则可以单击 "**关闭" 以记住项目文件中的设置**。</span><span class="sxs-lookup"><span data-stu-id="0f8a9-131">If you want to continue developing the application while waiting for provisioning to happen, you can click **Close to remember the settings in project file**.</span></span> <span data-ttu-id="0f8a9-132">下次调用 "启用 Windows Azure 身份验证" 并取消选中 "设置" 复选框时，将看到相同的设置，你可以单击 "**继续**"，然后单击 " **web.config中的" 应用这些设置**"。</span><span class="sxs-lookup"><span data-stu-id="0f8a9-132">The next time you invoke Enable Windows Azure Authentication and uncheck the provisioning checkbox, you will see the same settings and you can click **Continue**, then click, **Apply these settings in web.config**.</span></span>

1. <span data-ttu-id="0f8a9-133">等待你的应用程序配置为进行 Windows Azure 身份验证，并已设置为 Windows Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="0f8a9-133">Wait while your application is configured for Windows Azure Authentication and provisioned with Windows Azure Active Directory.</span></span>
2. <span data-ttu-id="0f8a9-134">为应用程序启用 Windows Azure 身份验证后，单击 "**关闭"：**</span><span class="sxs-lookup"><span data-stu-id="0f8a9-134">Once Windows Azure Authentication has been enabled for your application, click **Close:**</span></span>

    ![](windows-azure-authentication/_static/image7.png)
3. <span data-ttu-id="0f8a9-135">按 F5 运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="0f8a9-135">Hit F5 to run your application.</span></span> <span data-ttu-id="0f8a9-136">应该会自动重定向到登录页。</span><span class="sxs-lookup"><span data-stu-id="0f8a9-136">You should automatically get redirected to login page.</span></span> <span data-ttu-id="0f8a9-137">使用目录原则用户凭据登录到应用程序。</span><span class="sxs-lookup"><span data-stu-id="0f8a9-137">Use the directory tenet user credentials to login to the application..</span></span>

    ![](windows-azure-authentication/_static/image1.jpg)
4. <span data-ttu-id="0f8a9-138">由于你的应用程序当前正在使用自签名测试证书，你会收到来自浏览器的一条警告，指出证书不是由受信任的证书颁发机构颁发的。</span><span class="sxs-lookup"><span data-stu-id="0f8a9-138">Because your application is currently using a self-signed test certificate you will receive a warning from the browser that the certificate was not issued by a trusted certificate authority.</span></span>

    <span data-ttu-id="0f8a9-139">在本地开发期间，单击 "**继续浏览此网站**" 可安全地忽略此警告：</span><span class="sxs-lookup"><span data-stu-id="0f8a9-139">This warning can be safely ignored during local development by clicking **Continue to this website:**</span></span>

    ![](windows-azure-authentication/_static/image8.png)
5. <span data-ttu-id="0f8a9-140">现已成功使用 Windows Azure 身份验证登录到应用程序！</span><span class="sxs-lookup"><span data-stu-id="0f8a9-140">You have now successfully logged in to your application using Windows Azure Authentication!</span></span>

    ![](windows-azure-authentication/_static/image2.jpg)

<span data-ttu-id="0f8a9-141">启用 Windows Azure 身份验证会对应用程序进行以下更改：</span><span class="sxs-lookup"><span data-stu-id="0f8a9-141">Enabling Windows Azure authentication makes the following changes to your application:</span></span>

- <span data-ttu-id="0f8a9-142">反跨站点请求伪造（[CSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF))）类（*应用 \_ Start\AntiXsrfConfig.cs* ）已添加到你的项目中。</span><span class="sxs-lookup"><span data-stu-id="0f8a9-142">An Anti-Cross-Site Request Forgery ([CSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF))) class ( *App\_Start\AntiXsrfConfig.cs* ) is added to your project.</span></span>
- <span data-ttu-id="0f8a9-143">NuGet 包 `System.IdentityModel.Tokens.ValidatingIssuerNameRegistry` 将添加到你的项目中。</span><span class="sxs-lookup"><span data-stu-id="0f8a9-143">The NuGet packages `System.IdentityModel.Tokens.ValidatingIssuerNameRegistry` is added to your project.</span></span>
- <span data-ttu-id="0f8a9-144">应用程序中的 Windows Identity Foundation 设置将配置为接受来自 Windows Azure Active Directory 租户的安全令牌。</span><span class="sxs-lookup"><span data-stu-id="0f8a9-144">Windows Identity Foundation settings in your application will be configured to accept security tokens from your Windows Azure Active Directory tenant.</span></span> <span data-ttu-id="0f8a9-145">单击下面的图像可查看对*Web.config*文件所做更改的扩展视图。</span><span class="sxs-lookup"><span data-stu-id="0f8a9-145">Click on the image below to see an expanded view of the changes made to the *Web.config* file.</span></span>

     ![](windows-azure-authentication/_static/image9.png)
- <span data-ttu-id="0f8a9-146">将在 Windows Azure Active Directory 租户中设置应用程序的服务主体。</span><span class="sxs-lookup"><span data-stu-id="0f8a9-146">A service principal for your application in your Windows Azure Active Directory tenant will be provisioned.</span></span>
- <span data-ttu-id="0f8a9-147">HTTPS 已启用。</span><span class="sxs-lookup"><span data-stu-id="0f8a9-147">HTTPS is enabled.</span></span>

## <a name="deploy-the-application-to-windows-azure"></a><span data-ttu-id="0f8a9-148">将应用程序部署到 Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="0f8a9-148">Deploy the application to Windows Azure</span></span>

<span data-ttu-id="0f8a9-149">有关完整说明，请参阅将[ASP.NET Web 应用程序部署到 Microsoft Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet)网站。</span><span class="sxs-lookup"><span data-stu-id="0f8a9-149">For complete instructions, see [Deploying an ASP.NET Web Application to a Windows Azure Web Site](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet).</span></span>

<span data-ttu-id="0f8a9-150">若要将使用 Windows Azure 身份验证的应用程序发布到 Azure 网站：</span><span class="sxs-lookup"><span data-stu-id="0f8a9-150">To publish an application using Windows Azure Authentication to an Azure Web Site:</span></span>

1. <span data-ttu-id="0f8a9-151">右键单击应用程序，然后选择 "**发布"：**</span><span class="sxs-lookup"><span data-stu-id="0f8a9-151">Right click on your application and select **Publish:**</span></span>

    ![](windows-azure-authentication/_static/image3.jpg)
2. <span data-ttu-id="0f8a9-152">从 "发布 Web" 对话框中，下载并导入 Azure 网站的发布配置文件。</span><span class="sxs-lookup"><span data-stu-id="0f8a9-152">From the Publish Web dialog download and import a publishing profile for your Azure Web Site.</span></span>

    ![](windows-azure-authentication/_static/image4.jpg)
3. <span data-ttu-id="0f8a9-153">"**连接**" 选项卡显示**目标 url** （应用程序的面向公众的 url）。</span><span class="sxs-lookup"><span data-stu-id="0f8a9-153">The **Connection** tab shows the **Destination URL** (the public facing URL for your application).</span></span> <span data-ttu-id="0f8a9-154">单击 "**验证连接**" 以测试连接：</span><span class="sxs-lookup"><span data-stu-id="0f8a9-154">Click **Validate Connection** to test your connection:</span></span>

    ![](windows-azure-authentication/_static/image5.jpg)
4. <span data-ttu-id="0f8a9-155">如果之前已发布到此 Azure 网站，请考虑选中 "**删除目标上的其他文件**" 设置，以确保应用程序能够干净地发布。</span><span class="sxs-lookup"><span data-stu-id="0f8a9-155">If you have published to this Azure Web Site previously consider checking the **Remove additional files at destination** setting to ensure your application publishes cleanly.</span></span> <span data-ttu-id="0f8a9-156">请注意，"**启用 Windows Azure 身份验证**" 复选框处于选中状态。</span><span class="sxs-lookup"><span data-stu-id="0f8a9-156">Notice the **Enable Windows Azure Authentication** check box is selected.</span></span>

    ![](windows-azure-authentication/_static/image10.png)
5. <span data-ttu-id="0f8a9-157">可选：在 "**预览**" 选项卡上，单击 "**开始预览**" 以查看所部署的文件。</span><span class="sxs-lookup"><span data-stu-id="0f8a9-157">Optional: On the **Preview** tab click **Start Preview** to see the files deployed.</span></span>

    ![](windows-azure-authentication/_static/image6.jpg)
6. <span data-ttu-id="0f8a9-158">单击 "**发布"。**</span><span class="sxs-lookup"><span data-stu-id="0f8a9-158">Click **Publish.**</span></span>

    <span data-ttu-id="0f8a9-159">系统将提示你为目标主机启用 Windows Azure 身份验证。</span><span class="sxs-lookup"><span data-stu-id="0f8a9-159">You will be prompted to enable Windows Azure Authentication for the target host.</span></span> <span data-ttu-id="0f8a9-160">单击 "**启用**" 以继续：</span><span class="sxs-lookup"><span data-stu-id="0f8a9-160">Click **Enable** to continue:</span></span>

    ![](windows-azure-authentication/_static/image11.png)
7. <span data-ttu-id="0f8a9-161">输入 Windows Azure Active Directory 租户的管理员凭据：</span><span class="sxs-lookup"><span data-stu-id="0f8a9-161">Enter your administrator credentials for your Windows Azure Active Directory tenant:</span></span>

    ![](windows-azure-authentication/_static/image7.jpg)
8. <span data-ttu-id="0f8a9-162">成功发布应用程序后，浏览器将打开到已发布的网站。</span><span class="sxs-lookup"><span data-stu-id="0f8a9-162">Once your application has been successfully published, a browser will open to the published web site.</span></span>

    > [!NOTE]
    > <span data-ttu-id="0f8a9-163">对于目标主机启用 Windows Azure 身份验证后，你的应用程序将使用 Windows Azure Active Directory 完全预配，最长可能需要5分钟。</span><span class="sxs-lookup"><span data-stu-id="0f8a9-163">It may take up to five minutes (typically must less) for your application to be fully provisioned with Windows Azure Active Directory after enabling Windows Azure Authentication for the target host.</span></span> <span data-ttu-id="0f8a9-164">当你收到错误 ACS50001 时首次运行应用程序时，找不到名为 "[领域]" 的信赖方，请等待几分钟，然后尝试再次运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="0f8a9-164">When you first run your application if you receive error ACS50001: Relying party with name ‘[realm]' was not found, then wait a few minutes and try running the application again.</span></span>
9. <span data-ttu-id="0f8a9-165">出现提示时，以用户身份登录到目录：</span><span class="sxs-lookup"><span data-stu-id="0f8a9-165">When prompted, log in as a user in your directory:</span></span>

    ![](windows-azure-authentication/_static/image8.jpg)
10. <span data-ttu-id="0f8a9-166">现已成功使用 Windows Azure 身份验证登录到 Azure 托管的应用程序。</span><span class="sxs-lookup"><span data-stu-id="0f8a9-166">You have now successfully logged into your Azure hosted application using Windows Azure Authentication.</span></span>

     ![](windows-azure-authentication/_static/image9.jpg)

## <a name="known-issues"></a><span data-ttu-id="0f8a9-167">已知问题</span><span class="sxs-lookup"><span data-stu-id="0f8a9-167">Known Issues</span></span>

#### <a name="role-based-authorization-fails-when-using-windows-azure-authentication"></a><span data-ttu-id="0f8a9-168">使用 Windows Azure 身份验证时，基于角色的授权失败</span><span class="sxs-lookup"><span data-stu-id="0f8a9-168">Role-based authorization fails when using Windows Azure Authentication</span></span>

<span data-ttu-id="0f8a9-169">Windows Azure 身份验证当前不提供必要的角色声明，因此可以执行基于角色的授权。</span><span class="sxs-lookup"><span data-stu-id="0f8a9-169">Windows Azure Authentication does not currently provide the necessary role claim so that role-based authorization can be performed.</span></span> <span data-ttu-id="0f8a9-170">必须从 Windows Azure Active Directory 中手动检索经过身份验证的用户的角色。</span><span class="sxs-lookup"><span data-stu-id="0f8a9-170">The role of the authenticated user must be manually retrieved from Windows Azure Active Directory.</span></span>

#### <a name="browsing-to-an-application-with-windows-azure-authentication-results-in-the-error-acs20016-the-domain-of-the-logged-in-user-livecom-does-not-match-any-allowed-domain-of-this-sts"></a><span data-ttu-id="0f8a9-171">使用 Windows Azure 身份验证浏览到应用程序会导致错误 "ACS20016 已登录用户的域（live.com）与此 STS 的任何允许域都不匹配"</span><span class="sxs-lookup"><span data-stu-id="0f8a9-171">Browsing to an application with Windows Azure Authentication results in the error "ACS20016 The domain of the logged in user (live.com) does not match any allowed domain of this STS"</span></span>

<span data-ttu-id="0f8a9-172">如果你已登录到 Microsoft 帐户（例如 hotmail.com、live.com、outlook.com），并且尝试访问已启用 Windows Azure 身份验证的应用程序，你可能会收到400错误响应，因为 Windows Azure Active Directory 无法识别你的 Microsoft 帐户的域。</span><span class="sxs-lookup"><span data-stu-id="0f8a9-172">If you are already logged in to a Microsoft Account (for example hotmail.com, live.com, outlook.com) and you attempt to access an application that has enabled Windows Azure Authentication you may get a 400 error response because the domain of your Microsoft Account is not recognized by Windows Azure Active Directory.</span></span> <span data-ttu-id="0f8a9-173">若要登录到应用程序，请先从你的 Microsoft 帐户注销。</span><span class="sxs-lookup"><span data-stu-id="0f8a9-173">To log into the application, log out from your Microsoft Account first.</span></span>

#### <a name="logging-into-an-application-with-windows-azure-authentication-enabled-and-a-x509certificatevalidationmode-other-than-none-results-in-certificate-validation-errors-for-the-accountsaccesscontrolwindowsnet-certificate"></a><span data-ttu-id="0f8a9-174">登录到启用了 Windows Azure 身份验证的应用程序，如果 X509certificatevalidationmode.custom 不为 "无"，则会导致 accounts.accesscontrol.windows.net 证书的证书验证错误</span><span class="sxs-lookup"><span data-stu-id="0f8a9-174">Logging into an application with Windows Azure Authentication enabled and a X509CertificateValidationMode other than None results in certificate validation errors for the accounts.accesscontrol.windows.net certificate</span></span>

<span data-ttu-id="0f8a9-175">证书验证不是必需的，应保持禁用状态。</span><span class="sxs-lookup"><span data-stu-id="0f8a9-175">Certificate validation is not required and should be left disabled.</span></span> <span data-ttu-id="0f8a9-176">此颁发者证书的指纹由 WSFederationAuthenticationModule 验证。</span><span class="sxs-lookup"><span data-stu-id="0f8a9-176">The thumbprint of the issuer certificate is validated by the WSFederationAuthenticationModule.</span></span>

#### <a name="when-attempting-to-enable-windows-azure-authentication-the-web-authentication-dialog-shows-the-error-acs20016-the-domain-of-the-logged-in-user-contosoonmicrosoftcom-does-not-match-any-allowed-domain-of-this-sts"></a><span data-ttu-id="0f8a9-177">尝试启用 Windows Azure 身份验证时，Web 身份验证对话框显示错误 "ACS20016：登录用户的域（contoso.onmicrosoft.com）与此 STS 的任何允许的域都不匹配"。</span><span class="sxs-lookup"><span data-stu-id="0f8a9-177">When attempting to enable Windows Azure Authentication the Web Authentication dialog shows the error "ACS20016: The domain of the logged in user (contoso.onmicrosoft.com) does not match any allowed domain of this STS."</span></span>

<span data-ttu-id="0f8a9-178">如果以前已使用不同的 Windows Azure Active Directory 帐户从同一 Visual Studio 过程中成功登录，则可能会看到此错误。</span><span class="sxs-lookup"><span data-stu-id="0f8a9-178">You may see this error when you have previously successfully logged in using a different Windows Azure Active Directory account from within the same Visual Studio process.</span></span> <span data-ttu-id="0f8a9-179">请从指定帐户注销或重启 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="0f8a9-179">Log out from the specified account or restart Visual Studio.</span></span> <span data-ttu-id="0f8a9-180">如果以前登录并选择了 "使我保持登录状态" 选项，则可能需要清除浏览器 cookie。</span><span class="sxs-lookup"><span data-stu-id="0f8a9-180">If you previously logged in and selected the option to "Keep me signed in" then you may need to clear your browser cookies.</span></span>

## <a name="acs20012-the-request-is-not-a-valid-ws-federation-protocol-message"></a><span data-ttu-id="0f8a9-181">ACS20012：该请求不是有效的 WS 联合身份验证协议消息</span><span class="sxs-lookup"><span data-stu-id="0f8a9-181">ACS20012: The request is not a valid WS-Federation protocol message</span></span>

<span data-ttu-id="0f8a9-182">如果你已登录到某个 Azure 服务，则可能会发生这种情况。</span><span class="sxs-lookup"><span data-stu-id="0f8a9-182">This can happen if you are already logged in with some other Microsoft ID to one of the Azure services.</span></span> <span data-ttu-id="0f8a9-183">在 IE 中使用 InPrivate 或 Incognito 中的 InPrivate 浏览器窗口，或者清除所有 cookie。</span><span class="sxs-lookup"><span data-stu-id="0f8a9-183">Use Private browser window like InPrivate in IE or Incognito in Chrome or clear all the cookies.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0f8a9-184">其他资源</span><span class="sxs-lookup"><span data-stu-id="0f8a9-184">Additional Resources</span></span>

- <span data-ttu-id="0f8a9-185">[适用于 Windows Azure Active Directory Microsoft ASP.NET 工具– Visual Studio 2012](https://blogs.msdn.com/b/vbertocci/archive/2013/02/18/microsoft-asp-net-tools-for-windows-azure-active-directory-visual-studio-2012.aspx) – Vittorio Bertocci</span><span class="sxs-lookup"><span data-stu-id="0f8a9-185">[Microsoft ASP.NET Tools for Windows Azure Active Directory – Visual Studio 2012](https://blogs.msdn.com/b/vbertocci/archive/2013/02/18/microsoft-asp-net-tools-for-windows-azure-active-directory-visual-studio-2012.aspx) – Vittorio Bertocci</span></span>
- [<span data-ttu-id="0f8a9-186">Windows Azure 功能：标识</span><span class="sxs-lookup"><span data-stu-id="0f8a9-186">Windows Azure Features: Identity</span></span>](https://docs.microsoft.com/azure/active-directory/)
- [<span data-ttu-id="0f8a9-187">TechNet： Windows Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0f8a9-187">TechNet: Windows Azure Active Directory</span></span>](https://technet.microsoft.com/library/hh967619.aspx)
- [<span data-ttu-id="0f8a9-188">Windows Azure Active Directory：开发适用于你的组织的应用</span><span class="sxs-lookup"><span data-stu-id="0f8a9-188">Windows Azure Active Directory: Develop Apps for your organization</span></span>](https://activedirectory.windowsazure.com/Develop/Single-Tenant.aspx)
- [<span data-ttu-id="0f8a9-189">Windows Azure Active Directory：为多个组织开发应用程序</span><span class="sxs-lookup"><span data-stu-id="0f8a9-189">Windows Azure Active Directory: Develop Apps for multiple organizations</span></span>](https://activedirectory.windowsazure.com/Develop/Multi-Tenant.aspx)
- [<span data-ttu-id="0f8a9-190">如何实现 Windows Azure Active Directory 的单一登录</span><span class="sxs-lookup"><span data-stu-id="0f8a9-190">How to implement single sign-on with Windows Azure Active Directory</span></span>](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect)
- <span data-ttu-id="0f8a9-191">[Windows Azure Active Directory 的单一登录：深入探讨](https://blogs.msdn.com/b/vbertocci/archive/2012/07/05/single-sign-on-with-windows-azure-active-directory-a-deep-dive.aspx)– Vittorio Bertocci</span><span class="sxs-lookup"><span data-stu-id="0f8a9-191">[Single Sign-On with Windows Azure Active Directory: a Deep Dive](https://blogs.msdn.com/b/vbertocci/archive/2012/07/05/single-sign-on-with-windows-azure-active-directory-a-deep-dive.aspx) – Vittorio Bertocci</span></span>
- [<span data-ttu-id="0f8a9-192">使用 AD FS 2.0 实现和管理单一登录</span><span class="sxs-lookup"><span data-stu-id="0f8a9-192">Use AD FS 2.0 to implement and manage single sign-on</span></span>](https://technet.microsoft.com/library/jj205462.aspx)

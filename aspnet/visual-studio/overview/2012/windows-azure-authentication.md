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
# <a name="windows-azure-authentication"></a>Microsoft Azure 身份验证

作者： [Rick Anderson](https://twitter.com/RickAndMSFT)

> 适用于 Windows Azure Active Directory Microsoft ASP.NET 工具使为[Microsoft Azure 网站](https://www.windowsazure.com/home/features/web-sites/)上托管的 web 应用程序启用身份验证变得简单。 您可以使用 Microsoft Azure 身份验证对您的组织中的 Office 365 用户进行身份验证、从您的本地 Active Directory 或用户在自己的自定义 Windows Azure Active Directory 域中创建的用户进行身份验证。 启用 Windows Azure 身份验证可以将应用程序配置为使用单个[Windows Azure Active Directory](https://docs.microsoft.com/azure/active-directory/)租户对用户进行身份验证。
>
> 云服务中的 web 角色不支持 ASP.NET Windows Azure 身份验证工具，但我们计划在未来的版本中执行此操作。 Windows Azure web 角色支持[Windows Identity Foundation](https://msdn.microsoft.com/library/hh291066(v=VS.110).aspx) （WIF）。
>
> 有关如何在本地 Active Directory 和 Windows Azure Active Directory 租户之间设置同步的详细信息，请参阅[使用 AD FS 2.0 实现和管理单一登录](https://technet.microsoft.com/library/jj205462.aspx)。
>
> Windows Azure Active Directory 当前以[免费预览版服务](https://azure.microsoft.com/free/dotnet/)的形式提供。

## <a name="requirements"></a>要求：

- Visual Studio 2012 或[Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express)
- 用于 Visual Studio Express 2012 的 Visual Studio 2012 或[Web Tools 扩展](https://go.microsoft.com/fwlink/?LinkID=282231&amp;clcid=0x409)[的 web 工具扩展](https://go.microsoft.com/fwlink/?LinkID=282228&amp;clcid=0x409)
- [适用于 windows Azure Active Directory 的 Microsoft ASP.NET 工具– Visual Studio 2012](https://go.microsoft.com/fwlink/?LinkID=282306)或[适用于 Windows 的 Microsoft ASP.NET 工具 Azure Active Directory – Visual Studio Express 2012 for Web](https://go.microsoft.com/fwlink/?LinkId=282652)

## <a name="create-an-aspnet-web-application-with-visual-studio-2012"></a>使用 Visual Studio 2012 创建 ASP.NET Web 应用程序

您可以使用 Visual Studio 2012 创建任何 Web 应用程序，本教程使用 ASP.NET MVC intranet 模板。

1. 创建新的 ASP.NET MVC 4 Intranet 应用程序并接受所有默认值。 （它必须是**tra** net 中的，而不是**t** net 项目中）。
     ![](windows-azure-authentication/_static/image1.png)

## <a name="enable-window-azure-authentication-when-you-are-a-global-administrator-of-the-tenet"></a>启用 Window Azure 身份验证（如果是原则的全局管理员）

如果你没有现有的 Windows Azure Active Directory 租户（例如，通过现有的 Office 365 帐户），则可以通过注册[新的 windows Azure Active Directory 帐户](https://g.microsoftonline.com/0AX00en/5)来创建新租户。

1. 从 "项目" 菜单中选择 "**启用 Microsoft Azure 身份验证**"：

   ![](windows-azure-authentication/_static/image2.png)

2. 输入 Windows Azure Active Directory 租户的域（例如 contoso.onmicrosoft.com），然后单击 "**启用**"：

![](windows-azure-authentication/_static/image3.png)

3. 在 Web 身份验证对话框中，以管理员身份登录 Windows Azure Active Directory 租户：

   ![](windows-azure-authentication/_static/image4.png)

![](windows-azure-authentication/_static/image5.png)

## <a name="enable-window-azure-by-a-non-administrator-of-the-tenet"></a>通过原则的非管理员启用 Window Azure

如果你没有 Windows Azure Active Directory 租户的全局管理员权限，则可以取消选中用于预配应用程序的复选框。

![](windows-azure-authentication/_static/image6.png)

此对话框将显示使用 Azure Active Directory 原则预配应用程序所需的 "**域**"、"**应用程序主体 Id** " 和 "**答复 URL** "。 需要将此信息提供给有足够权限来预配应用程序的人员。 有关如何使用 cmdlet 来手动创建服务主体的详细信息，请参阅[如何使用 Windows Azure Active Directory ASP.NET 应用程序实现单一登录](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect)。
成功预配应用程序后，可以单击 "继续"**以更新具有所选设置的 web.config**。 如果要在等待预配发生的同时继续开发应用程序，则可以单击 "**关闭" 以记住项目文件中的设置**。 下次调用 "启用 Windows Azure 身份验证" 并取消选中 "设置" 复选框时，将看到相同的设置，你可以单击 "**继续**"，然后单击 " **web.config中的" 应用这些设置**"。

1. 等待你的应用程序配置为进行 Windows Azure 身份验证，并已设置为 Windows Azure Active Directory。
2. 为应用程序启用 Windows Azure 身份验证后，单击 "**关闭"：**

    ![](windows-azure-authentication/_static/image7.png)
3. 按 F5 运行应用程序。 应该会自动重定向到登录页。 使用目录原则用户凭据登录到应用程序。

    ![](windows-azure-authentication/_static/image1.jpg)
4. 由于你的应用程序当前正在使用自签名测试证书，你会收到来自浏览器的一条警告，指出证书不是由受信任的证书颁发机构颁发的。

    在本地开发期间，单击 "**继续浏览此网站**" 可安全地忽略此警告：

    ![](windows-azure-authentication/_static/image8.png)
5. 现已成功使用 Windows Azure 身份验证登录到应用程序！

    ![](windows-azure-authentication/_static/image2.jpg)

启用 Windows Azure 身份验证会对应用程序进行以下更改：

- 反跨站点请求伪造（[CSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF))）类（*应用 \_ Start\AntiXsrfConfig.cs* ）已添加到你的项目中。
- NuGet 包 `System.IdentityModel.Tokens.ValidatingIssuerNameRegistry` 将添加到你的项目中。
- 应用程序中的 Windows Identity Foundation 设置将配置为接受来自 Windows Azure Active Directory 租户的安全令牌。 单击下面的图像可查看对*Web.config*文件所做更改的扩展视图。

     ![](windows-azure-authentication/_static/image9.png)
- 将在 Windows Azure Active Directory 租户中设置应用程序的服务主体。
- HTTPS 已启用。

## <a name="deploy-the-application-to-windows-azure"></a>将应用程序部署到 Microsoft Azure

有关完整说明，请参阅将[ASP.NET Web 应用程序部署到 Microsoft Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet)网站。

若要将使用 Windows Azure 身份验证的应用程序发布到 Azure 网站：

1. 右键单击应用程序，然后选择 "**发布"：**

    ![](windows-azure-authentication/_static/image3.jpg)
2. 从 "发布 Web" 对话框中，下载并导入 Azure 网站的发布配置文件。

    ![](windows-azure-authentication/_static/image4.jpg)
3. "**连接**" 选项卡显示**目标 url** （应用程序的面向公众的 url）。 单击 "**验证连接**" 以测试连接：

    ![](windows-azure-authentication/_static/image5.jpg)
4. 如果之前已发布到此 Azure 网站，请考虑选中 "**删除目标上的其他文件**" 设置，以确保应用程序能够干净地发布。 请注意，"**启用 Windows Azure 身份验证**" 复选框处于选中状态。

    ![](windows-azure-authentication/_static/image10.png)
5. 可选：在 "**预览**" 选项卡上，单击 "**开始预览**" 以查看所部署的文件。

    ![](windows-azure-authentication/_static/image6.jpg)
6. 单击 "**发布"。**

    系统将提示你为目标主机启用 Windows Azure 身份验证。 单击 "**启用**" 以继续：

    ![](windows-azure-authentication/_static/image11.png)
7. 输入 Windows Azure Active Directory 租户的管理员凭据：

    ![](windows-azure-authentication/_static/image7.jpg)
8. 成功发布应用程序后，浏览器将打开到已发布的网站。

    > [!NOTE]
    > 对于目标主机启用 Windows Azure 身份验证后，你的应用程序将使用 Windows Azure Active Directory 完全预配，最长可能需要5分钟。 当你收到错误 ACS50001 时首次运行应用程序时，找不到名为 "[领域]" 的信赖方，请等待几分钟，然后尝试再次运行该应用程序。
9. 出现提示时，以用户身份登录到目录：

    ![](windows-azure-authentication/_static/image8.jpg)
10. 现已成功使用 Windows Azure 身份验证登录到 Azure 托管的应用程序。

     ![](windows-azure-authentication/_static/image9.jpg)

## <a name="known-issues"></a>已知问题

#### <a name="role-based-authorization-fails-when-using-windows-azure-authentication"></a>使用 Windows Azure 身份验证时，基于角色的授权失败

Windows Azure 身份验证当前不提供必要的角色声明，因此可以执行基于角色的授权。 必须从 Windows Azure Active Directory 中手动检索经过身份验证的用户的角色。

#### <a name="browsing-to-an-application-with-windows-azure-authentication-results-in-the-error-acs20016-the-domain-of-the-logged-in-user-livecom-does-not-match-any-allowed-domain-of-this-sts"></a>使用 Windows Azure 身份验证浏览到应用程序会导致错误 "ACS20016 已登录用户的域（live.com）与此 STS 的任何允许域都不匹配"

如果你已登录到 Microsoft 帐户（例如 hotmail.com、live.com、outlook.com），并且尝试访问已启用 Windows Azure 身份验证的应用程序，你可能会收到400错误响应，因为 Windows Azure Active Directory 无法识别你的 Microsoft 帐户的域。 若要登录到应用程序，请先从你的 Microsoft 帐户注销。

#### <a name="logging-into-an-application-with-windows-azure-authentication-enabled-and-a-x509certificatevalidationmode-other-than-none-results-in-certificate-validation-errors-for-the-accountsaccesscontrolwindowsnet-certificate"></a>登录到启用了 Windows Azure 身份验证的应用程序，如果 X509certificatevalidationmode.custom 不为 "无"，则会导致 accounts.accesscontrol.windows.net 证书的证书验证错误

证书验证不是必需的，应保持禁用状态。 此颁发者证书的指纹由 WSFederationAuthenticationModule 验证。

#### <a name="when-attempting-to-enable-windows-azure-authentication-the-web-authentication-dialog-shows-the-error-acs20016-the-domain-of-the-logged-in-user-contosoonmicrosoftcom-does-not-match-any-allowed-domain-of-this-sts"></a>尝试启用 Windows Azure 身份验证时，Web 身份验证对话框显示错误 "ACS20016：登录用户的域（contoso.onmicrosoft.com）与此 STS 的任何允许的域都不匹配"。

如果以前已使用不同的 Windows Azure Active Directory 帐户从同一 Visual Studio 过程中成功登录，则可能会看到此错误。 请从指定帐户注销或重启 Visual Studio。 如果以前登录并选择了 "使我保持登录状态" 选项，则可能需要清除浏览器 cookie。

## <a name="acs20012-the-request-is-not-a-valid-ws-federation-protocol-message"></a>ACS20012：该请求不是有效的 WS 联合身份验证协议消息

如果你已登录到某个 Azure 服务，则可能会发生这种情况。 在 IE 中使用 InPrivate 或 Incognito 中的 InPrivate 浏览器窗口，或者清除所有 cookie。

## <a name="additional-resources"></a>其他资源

- [适用于 Windows Azure Active Directory Microsoft ASP.NET 工具– Visual Studio 2012](https://blogs.msdn.com/b/vbertocci/archive/2013/02/18/microsoft-asp-net-tools-for-windows-azure-active-directory-visual-studio-2012.aspx) – Vittorio Bertocci
- [Windows Azure 功能：标识](https://docs.microsoft.com/azure/active-directory/)
- [TechNet： Windows Azure Active Directory](https://technet.microsoft.com/library/hh967619.aspx)
- [Windows Azure Active Directory：开发适用于你的组织的应用](https://activedirectory.windowsazure.com/Develop/Single-Tenant.aspx)
- [Windows Azure Active Directory：为多个组织开发应用程序](https://activedirectory.windowsazure.com/Develop/Multi-Tenant.aspx)
- [如何实现 Windows Azure Active Directory 的单一登录](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect)
- [Windows Azure Active Directory 的单一登录：深入探讨](https://blogs.msdn.com/b/vbertocci/archive/2012/07/05/single-sign-on-with-windows-azure-active-directory-a-deep-dive.aspx)– Vittorio Bertocci
- [使用 AD FS 2.0 实现和管理单一登录](https://technet.microsoft.com/library/jj205462.aspx)

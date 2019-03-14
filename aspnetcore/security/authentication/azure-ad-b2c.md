---
title: Azure Active Directory B2C ASP.NET Core 中使用云身份验证
author: camsoper
description: 了解如何设置与 ASP.NET Core的 Azure Active Directory B2C 身份验证。
ms.date: 01/25/2018
ms.custom: mvc
uid: security/authentication/azure-ad-b2c
ms.openlocfilehash: 2c544475ccd3eb76f2737fec1cf269ac86add372
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57040624"
---
# <a name="cloud-authentication-with-azure-active-directory-b2c-in-aspnet-core"></a><span data-ttu-id="1d986-103">Azure Active Directory B2C ASP.NET Core 中使用云身份验证</span><span class="sxs-lookup"><span data-stu-id="1d986-103">Cloud authentication with Azure Active Directory B2C in ASP.NET Core</span></span>

<span data-ttu-id="1d986-104">作者：[Cam Soper](https://twitter.com/camsoper)</span><span class="sxs-lookup"><span data-stu-id="1d986-104">By [Cam Soper](https://twitter.com/camsoper)</span></span>

<span data-ttu-id="1d986-105">[Azure Active Directory B2C](/azure/active-directory-b2c/active-directory-b2c-overview) (Azure AD B2C) 是云标识管理解决方案，适用于 web 和移动应用。</span><span class="sxs-lookup"><span data-stu-id="1d986-105">[Azure Active Directory B2C](/azure/active-directory-b2c/active-directory-b2c-overview) (Azure AD B2C) is a cloud identity management solution for web and mobile apps.</span></span> <span data-ttu-id="1d986-106">该服务提供用于在云中和本地托管的应用的身份验证。</span><span class="sxs-lookup"><span data-stu-id="1d986-106">The service provides authentication for apps hosted in the cloud and on-premises.</span></span> <span data-ttu-id="1d986-107">身份验证类型包括个人帐户，社交网络帐户和联合企业帐户。</span><span class="sxs-lookup"><span data-stu-id="1d986-107">Authentication types include individual accounts, social network accounts, and federated enterprise accounts.</span></span> <span data-ttu-id="1d986-108">此外，Azure AD B2C 可以提供最小配置多重身份验证。</span><span class="sxs-lookup"><span data-stu-id="1d986-108">Additionally, Azure AD B2C can provide multi-factor authentication with minimal configuration.</span></span>

> [!TIP]
> <span data-ttu-id="1d986-109">Azure Active Directory (Azure AD) 和 Azure AD B2C 是单独的产品产品/服务。</span><span class="sxs-lookup"><span data-stu-id="1d986-109">Azure Active Directory (Azure AD) and Azure AD B2C are separate product offerings.</span></span> <span data-ttu-id="1d986-110">Azure AD 租户表示组织，而 Azure AD B2C 租户表示与信赖方应用程序将使用的集合。</span><span class="sxs-lookup"><span data-stu-id="1d986-110">An Azure AD tenant represents an organization, while an Azure AD B2C tenant represents a collection of identities to be used with relying party applications.</span></span> <span data-ttu-id="1d986-111">若要了解详细信息，请参阅[Azure AD B2C:常见问题 (FAQ)](/azure/active-directory-b2c/active-directory-b2c-faqs)。</span><span class="sxs-lookup"><span data-stu-id="1d986-111">To learn more, see [Azure AD B2C: Frequently asked questions (FAQ)](/azure/active-directory-b2c/active-directory-b2c-faqs).</span></span>

<span data-ttu-id="1d986-112">在本教程中，学习如何：</span><span class="sxs-lookup"><span data-stu-id="1d986-112">In this tutorial, learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1d986-113">创建 Azure Active Directory B2C 租户</span><span class="sxs-lookup"><span data-stu-id="1d986-113">Create an Azure Active Directory B2C tenant</span></span>
> * <span data-ttu-id="1d986-114">在 Azure AD B2C 中注册应用</span><span class="sxs-lookup"><span data-stu-id="1d986-114">Register an app in Azure AD B2C</span></span>
> * <span data-ttu-id="1d986-115">使用 Visual Studio 创建 ASP.NET Core web 应用配置为使用 Azure AD B2C 租户进行身份验证</span><span class="sxs-lookup"><span data-stu-id="1d986-115">Use Visual Studio to create an ASP.NET Core web app configured to use the Azure AD B2C tenant for authentication</span></span>
> * <span data-ttu-id="1d986-116">配置控制的 Azure AD B2C 租户行为的策略</span><span class="sxs-lookup"><span data-stu-id="1d986-116">Configure policies controlling the behavior of the Azure AD B2C tenant</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1d986-117">系统必备</span><span class="sxs-lookup"><span data-stu-id="1d986-117">Prerequisites</span></span>

<span data-ttu-id="1d986-118">本演练需要以下项：</span><span class="sxs-lookup"><span data-stu-id="1d986-118">The following are required for this walkthrough:</span></span>

* [<span data-ttu-id="1d986-119">Microsoft Azure 订阅</span><span class="sxs-lookup"><span data-stu-id="1d986-119">Microsoft Azure subscription</span></span>](https://azure.microsoft.com/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio)
* <span data-ttu-id="1d986-120">[Visual Studio 2017](https://aka.ms/vsdownload?utm_source=mscom&utm_campaign=msdocs) （任何版本）</span><span class="sxs-lookup"><span data-stu-id="1d986-120">[Visual Studio 2017](https://aka.ms/vsdownload?utm_source=mscom&utm_campaign=msdocs) (any edition)</span></span>

## <a name="create-the-azure-active-directory-b2c-tenant"></a><span data-ttu-id="1d986-121">创建 Azure Active Directory B2C 租户</span><span class="sxs-lookup"><span data-stu-id="1d986-121">Create the Azure Active Directory B2C tenant</span></span>

<span data-ttu-id="1d986-122">创建 Azure Active Directory B2C 租户[文档中所述](/azure/active-directory-b2c/active-directory-b2c-get-started)。</span><span class="sxs-lookup"><span data-stu-id="1d986-122">Create an Azure Active Directory B2C tenant [as described in the documentation](/azure/active-directory-b2c/active-directory-b2c-get-started).</span></span> <span data-ttu-id="1d986-123">出现提示时，将租户与 Azure 订阅相关联是可选的用于本教程。</span><span class="sxs-lookup"><span data-stu-id="1d986-123">When prompted, associating the tenant with an Azure subscription is optional for this tutorial.</span></span>

## <a name="register-the-app-in-azure-ad-b2c"></a><span data-ttu-id="1d986-124">在 Azure AD B2C 中注册应用</span><span class="sxs-lookup"><span data-stu-id="1d986-124">Register the app in Azure AD B2C</span></span>

<span data-ttu-id="1d986-125">在新创建的 Azure AD B2C 租户中注册应用程序使用[文档中的步骤](/azure/active-directory-b2c/active-directory-b2c-app-registration#register-a-web-app)下**注册 web 应用**部分。</span><span class="sxs-lookup"><span data-stu-id="1d986-125">In the newly created Azure AD B2C tenant, register your app using [the steps in the documentation](/azure/active-directory-b2c/active-directory-b2c-app-registration#register-a-web-app) under the **Register a web app** section.</span></span> <span data-ttu-id="1d986-126">在停止**创建 web 应用客户端机密**部分。</span><span class="sxs-lookup"><span data-stu-id="1d986-126">Stop at the **Create a web app client secret** section.</span></span> <span data-ttu-id="1d986-127">本教程不需要客户端机密。</span><span class="sxs-lookup"><span data-stu-id="1d986-127">A client secret isn't required for this tutorial.</span></span> 

<span data-ttu-id="1d986-128">使用以下值：</span><span class="sxs-lookup"><span data-stu-id="1d986-128">Use the following values:</span></span>

| <span data-ttu-id="1d986-129">设置</span><span class="sxs-lookup"><span data-stu-id="1d986-129">Setting</span></span>                       | <span data-ttu-id="1d986-130">值</span><span class="sxs-lookup"><span data-stu-id="1d986-130">Value</span></span>                     | <span data-ttu-id="1d986-131">说明</span><span class="sxs-lookup"><span data-stu-id="1d986-131">Notes</span></span>                                                                                                                                                                                              |
|-------------------------------|---------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="1d986-132">**名称**</span><span class="sxs-lookup"><span data-stu-id="1d986-132">**Name**</span></span>                      | <span data-ttu-id="1d986-133">*&lt;应用名称&gt;*</span><span class="sxs-lookup"><span data-stu-id="1d986-133">*&lt;app name&gt;*</span></span>        | <span data-ttu-id="1d986-134">输入**名称**描述你的应用向使用者的应用。</span><span class="sxs-lookup"><span data-stu-id="1d986-134">Enter a **Name** for the app that describes your app to consumers.</span></span>                                                                                                                                 |
| <span data-ttu-id="1d986-135">**包括 web 应用 /web API**</span><span class="sxs-lookup"><span data-stu-id="1d986-135">**Include web app / web API**</span></span> | <span data-ttu-id="1d986-136">是</span><span class="sxs-lookup"><span data-stu-id="1d986-136">Yes</span></span>                       |                                                                                                                                                                                                    |
| <span data-ttu-id="1d986-137">**允许隐式流**</span><span class="sxs-lookup"><span data-stu-id="1d986-137">**Allow implicit flow**</span></span>       | <span data-ttu-id="1d986-138">是</span><span class="sxs-lookup"><span data-stu-id="1d986-138">Yes</span></span>                       |                                                                                                                                                                                                    |
| <span data-ttu-id="1d986-139">**回复 URL**</span><span class="sxs-lookup"><span data-stu-id="1d986-139">**Reply URL**</span></span>                 | `https://localhost:44300/signin-oidc` | <span data-ttu-id="1d986-140">回复 Url 属于终结点，Azure AD B2C 在其中返回应用请求的任何令牌。</span><span class="sxs-lookup"><span data-stu-id="1d986-140">Reply URLs are endpoints where Azure AD B2C returns any tokens that your app requests.</span></span> <span data-ttu-id="1d986-141">Visual Studio 提供了要使用的回复 URL。</span><span class="sxs-lookup"><span data-stu-id="1d986-141">Visual Studio provides the Reply URL to use.</span></span> <span data-ttu-id="1d986-142">现在，输入`https://localhost:44300/signin-oidc`填写表单。</span><span class="sxs-lookup"><span data-stu-id="1d986-142">For now, enter `https://localhost:44300/signin-oidc` to complete the form.</span></span> |
| <span data-ttu-id="1d986-143">**应用程序 ID URI**</span><span class="sxs-lookup"><span data-stu-id="1d986-143">**App ID URI**</span></span>                | <span data-ttu-id="1d986-144">将保留为空</span><span class="sxs-lookup"><span data-stu-id="1d986-144">Leave blank</span></span>               | <span data-ttu-id="1d986-145">对于本教程不被必需。</span><span class="sxs-lookup"><span data-stu-id="1d986-145">Not required for this tutorial.</span></span>                                                                                                                                                                    |
| <span data-ttu-id="1d986-146">**包含本机客户端**</span><span class="sxs-lookup"><span data-stu-id="1d986-146">**Include native client**</span></span>     | <span data-ttu-id="1d986-147">否</span><span class="sxs-lookup"><span data-stu-id="1d986-147">No</span></span>                        |                                                                                                                                                                                                    |

> [!WARNING]
> <span data-ttu-id="1d986-148">如果设置了非 localhost 答复 URL，请注意[回复 URL 列表中允许的内容的约束](/azure/active-directory-b2c/active-directory-b2c-app-registration#choosing-a-web-app-or-api-reply-url)。</span><span class="sxs-lookup"><span data-stu-id="1d986-148">If setting up a non-localhost Reply URL, be aware of the [constraints on what is allowed in the Reply URL list](/azure/active-directory-b2c/active-directory-b2c-app-registration#choosing-a-web-app-or-api-reply-url).</span></span> 

<span data-ttu-id="1d986-149">注册应用后，将显示租户中的应用列表。</span><span class="sxs-lookup"><span data-stu-id="1d986-149">After the app is registered, the list of apps in the tenant is displayed.</span></span> <span data-ttu-id="1d986-150">选择刚注册的应用。</span><span class="sxs-lookup"><span data-stu-id="1d986-150">Select the app that was just registered.</span></span> <span data-ttu-id="1d986-151">选择**副本**右侧的图标**应用程序 ID**字段以将其复制到剪贴板。</span><span class="sxs-lookup"><span data-stu-id="1d986-151">Select the **Copy** icon to the right of the **Application ID** field to copy it to the clipboard.</span></span>

<span data-ttu-id="1d986-152">执行任何操作的详细信息在此期间，可以在 Azure AD B2C 租户中配置，但使浏览器窗口保持打开状态。</span><span class="sxs-lookup"><span data-stu-id="1d986-152">Nothing more can be configured in the Azure AD B2C tenant at this time, but leave the browser window open.</span></span> <span data-ttu-id="1d986-153">创建 ASP.NET Core 应用后，没有更多的配置。</span><span class="sxs-lookup"><span data-stu-id="1d986-153">There is more configuration after the ASP.NET Core app is created.</span></span>

## <a name="create-an-aspnet-core-app-in-visual-studio-2017"></a><span data-ttu-id="1d986-154">在 Visual Studio 2017 年 1 中创建 ASP.NET Core 应用</span><span class="sxs-lookup"><span data-stu-id="1d986-154">Create an ASP.NET Core app in Visual Studio 2017</span></span>

<span data-ttu-id="1d986-155">Visual Studio Web 应用程序模板可以配置为使用 Azure AD B2C 租户进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="1d986-155">The Visual Studio Web Application template can be configured to use the Azure AD B2C tenant for authentication.</span></span>

<span data-ttu-id="1d986-156">在 Visual Studio 中：</span><span class="sxs-lookup"><span data-stu-id="1d986-156">In Visual Studio:</span></span>

1. <span data-ttu-id="1d986-157">创建新的 ASP.NET Core Web 应用呈现。</span><span class="sxs-lookup"><span data-stu-id="1d986-157">Create a new ASP.NET Core Web Application.</span></span> 
2. <span data-ttu-id="1d986-158">选择**Web 应用程序**从模板列表。</span><span class="sxs-lookup"><span data-stu-id="1d986-158">Select **Web Application** from the list of templates.</span></span>
3. <span data-ttu-id="1d986-159">选择**更改身份验证**按钮。</span><span class="sxs-lookup"><span data-stu-id="1d986-159">Select the **Change Authentication** button.</span></span>
    
    ![更改身份验证按钮](./azure-ad-b2c/_static/changeauth.png)

4. <span data-ttu-id="1d986-161">在中**更改身份验证**对话框中，选择**单个用户帐户**，然后选择**连接到现有用户存储在云中**下拉列表中。</span><span class="sxs-lookup"><span data-stu-id="1d986-161">In the **Change Authentication** dialog, select **Individual User Accounts**, and then select **Connect to an existing user store in the cloud** in the dropdown.</span></span> 
    
    ![更改身份验证对话框](./azure-ad-b2c/_static/changeauthdialog.png)

5. <span data-ttu-id="1d986-163">完成窗体具有以下值：</span><span class="sxs-lookup"><span data-stu-id="1d986-163">Complete the form with the following values:</span></span>
    
    | <span data-ttu-id="1d986-164">设置</span><span class="sxs-lookup"><span data-stu-id="1d986-164">Setting</span></span>                       | <span data-ttu-id="1d986-165">值</span><span class="sxs-lookup"><span data-stu-id="1d986-165">Value</span></span>                                                 |
    |-------------------------------|-------------------------------------------------------|
    | <span data-ttu-id="1d986-166">**域名**</span><span class="sxs-lookup"><span data-stu-id="1d986-166">**Domain Name**</span></span>               | <span data-ttu-id="1d986-167">*&lt;在 B2C 租户的域名&gt;*</span><span class="sxs-lookup"><span data-stu-id="1d986-167">*&lt;the domain name of your B2C tenant&gt;*</span></span>          |
    | <span data-ttu-id="1d986-168">**应用程序 ID**</span><span class="sxs-lookup"><span data-stu-id="1d986-168">**Application ID**</span></span>            | <span data-ttu-id="1d986-169">*&lt;粘贴剪贴板中的应用程序 ID&gt;*</span><span class="sxs-lookup"><span data-stu-id="1d986-169">*&lt;paste the Application ID from the clipboard&gt;*</span></span> |
    | <span data-ttu-id="1d986-170">**回调路径**</span><span class="sxs-lookup"><span data-stu-id="1d986-170">**Callback Path**</span></span>             | <span data-ttu-id="1d986-171">*&lt;使用默认值&gt;*</span><span class="sxs-lookup"><span data-stu-id="1d986-171">*&lt;use the default value&gt;*</span></span>                       |
    | <span data-ttu-id="1d986-172">**注册或登录策略**</span><span class="sxs-lookup"><span data-stu-id="1d986-172">**Sign-up or sign-in policy**</span></span> | `B2C_1_SiUpIn`                                        |
    | <span data-ttu-id="1d986-173">**重置密码策略**</span><span class="sxs-lookup"><span data-stu-id="1d986-173">**Reset password policy**</span></span>     | `B2C_1_SSPR`                                          |
    | <span data-ttu-id="1d986-174">**编辑配置文件策略**</span><span class="sxs-lookup"><span data-stu-id="1d986-174">**Edit profile policy**</span></span>       | <span data-ttu-id="1d986-175">*&lt;将保留为空&gt;*</span><span class="sxs-lookup"><span data-stu-id="1d986-175">*&lt;leave blank&gt;*</span></span>                                 |
    
    <span data-ttu-id="1d986-176">选择**副本**链接旁边**回复 URI**将回复 URI 复制到剪贴板。</span><span class="sxs-lookup"><span data-stu-id="1d986-176">Select the **Copy** link next to **Reply URI** to copy the Reply URI to the clipboard.</span></span> <span data-ttu-id="1d986-177">选择**确定**以关闭**更改身份验证**对话框。</span><span class="sxs-lookup"><span data-stu-id="1d986-177">Select **OK** to close the **Change Authentication** dialog.</span></span> <span data-ttu-id="1d986-178">选择**确定**创建 web 应用。</span><span class="sxs-lookup"><span data-stu-id="1d986-178">Select **OK** to create the web app.</span></span>

## <a name="finish-the-b2c-app-registration"></a><span data-ttu-id="1d986-179">完成 B2C 应用程序注册</span><span class="sxs-lookup"><span data-stu-id="1d986-179">Finish the B2C app registration</span></span>

<span data-ttu-id="1d986-180">返回到 B2C 应用程序属性仍然打开的浏览器窗口。</span><span class="sxs-lookup"><span data-stu-id="1d986-180">Return to the browser window with the B2C app properties still open.</span></span> <span data-ttu-id="1d986-181">更改临时**回复 URL**从 Visual Studio 指定更早的值复制。</span><span class="sxs-lookup"><span data-stu-id="1d986-181">Change the temporary **Reply URL** specified earlier to the value copied from Visual Studio.</span></span> <span data-ttu-id="1d986-182">选择**保存**在窗口的顶部。</span><span class="sxs-lookup"><span data-stu-id="1d986-182">Select **Save** at the top of the window.</span></span>

> [!TIP]
> <span data-ttu-id="1d986-183">如果未复制回复 URL，在 web 项目属性中，使用调试选项卡中的 HTTPS 地址并追加**CallbackPath**值从*appsettings.json*。</span><span class="sxs-lookup"><span data-stu-id="1d986-183">If you didn't copy the Reply URL, use the HTTPS address from the Debug tab in the web project properties, and append the **CallbackPath** value from *appsettings.json*.</span></span>

## <a name="configure-policies"></a><span data-ttu-id="1d986-184">配置策略</span><span class="sxs-lookup"><span data-stu-id="1d986-184">Configure policies</span></span>

<span data-ttu-id="1d986-185">使用到的 Azure AD B2C 文档中的步骤[创建注册或登录策略](/azure/active-directory-b2c/active-directory-b2c-reference-policies#create-a-sign-up-or-sign-in-policy)，然后[创建密码重置策略](/azure/active-directory-b2c/active-directory-b2c-reference-policies#create-a-password-reset-policy)。</span><span class="sxs-lookup"><span data-stu-id="1d986-185">Use the steps in the Azure AD B2C documentation to [create a sign-up or sign-in policy](/azure/active-directory-b2c/active-directory-b2c-reference-policies#create-a-sign-up-or-sign-in-policy), and then [create a password reset policy](/azure/active-directory-b2c/active-directory-b2c-reference-policies#create-a-password-reset-policy).</span></span> <span data-ttu-id="1d986-186">使用提供的文档中的示例值**标识提供者**，**注册属性**，并**应用程序声明**。</span><span class="sxs-lookup"><span data-stu-id="1d986-186">Use the example values provided in the documentation for **Identity providers**, **Sign-up attributes**, and **Application claims**.</span></span> <span data-ttu-id="1d986-187">使用**立即运行**是可选的按钮以测试这些策略，如文档中所述。</span><span class="sxs-lookup"><span data-stu-id="1d986-187">Using the **Run now** button to test the policies as described in the documentation is optional.</span></span>

> [!WARNING]
> <span data-ttu-id="1d986-188">确保策略名称完全按照说明在文档中，并与这些策略中使用**更改身份验证**Visual Studio 中的对话框。</span><span class="sxs-lookup"><span data-stu-id="1d986-188">Ensure the policy names are exactly as described in the documentation, as those policies were used in the **Change Authentication** dialog in Visual Studio.</span></span> <span data-ttu-id="1d986-189">可以在中验证的策略名称*appsettings.json*。</span><span class="sxs-lookup"><span data-stu-id="1d986-189">The policy names can be verified in *appsettings.json*.</span></span>

## <a name="run-the-app"></a><span data-ttu-id="1d986-190">运行应用</span><span class="sxs-lookup"><span data-stu-id="1d986-190">Run the app</span></span>

<span data-ttu-id="1d986-191">在 Visual Studio 中，按**F5**生成并运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="1d986-191">In Visual Studio, press **F5** to build and run the app.</span></span> <span data-ttu-id="1d986-192">Web 应用启动后，选择**Accept**以接受使用 cookie （如果提示），然后选择**登录**。</span><span class="sxs-lookup"><span data-stu-id="1d986-192">After the web app launches, select **Accept** to accept the use of cookies (if prompted), and then select **Sign in**.</span></span>

![登录到应用](./azure-ad-b2c/_static/signin.png)

<span data-ttu-id="1d986-194">在浏览器将重定向到 Azure AD B2C 租户。</span><span class="sxs-lookup"><span data-stu-id="1d986-194">The browser redirects to the Azure AD B2C tenant.</span></span> <span data-ttu-id="1d986-195">（如果已经创建了一个测试策略） 的现有帐户登录，或选择**立即注册**若要创建新帐户。</span><span class="sxs-lookup"><span data-stu-id="1d986-195">Sign in with an existing account (if one was created testing the policies) or select **Sign up now** to create a new account.</span></span> <span data-ttu-id="1d986-196">**忘记了密码？** 链接用于重置忘记的密码。</span><span class="sxs-lookup"><span data-stu-id="1d986-196">The **Forgot your password?** link is used to reset a forgotten password.</span></span>

![Azure AD B2C 登录](./azure-ad-b2c/_static/b2csts.png)

<span data-ttu-id="1d986-198">已成功登录后，浏览器将重定向到 web 应用。</span><span class="sxs-lookup"><span data-stu-id="1d986-198">After successfully signing in, the browser redirects to the web app.</span></span>

![成功](./azure-ad-b2c/_static/success.png)

## <a name="next-steps"></a><span data-ttu-id="1d986-200">后续步骤</span><span class="sxs-lookup"><span data-stu-id="1d986-200">Next steps</span></span>

<span data-ttu-id="1d986-201">在本教程中，你将了解：</span><span class="sxs-lookup"><span data-stu-id="1d986-201">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1d986-202">创建 Azure Active Directory B2C 租户</span><span class="sxs-lookup"><span data-stu-id="1d986-202">Create an Azure Active Directory B2C tenant</span></span>
> * <span data-ttu-id="1d986-203">在 Azure AD B2C 中注册应用</span><span class="sxs-lookup"><span data-stu-id="1d986-203">Register an app in Azure AD B2C</span></span>
> * <span data-ttu-id="1d986-204">使用 Visual Studio 创建 ASP.NET Core Web 应用程序配置为使用 Azure AD B2C 租户进行身份验证</span><span class="sxs-lookup"><span data-stu-id="1d986-204">Use Visual Studio to create an ASP.NET Core Web Application configured to use the Azure AD B2C tenant for authentication</span></span>
> * <span data-ttu-id="1d986-205">配置控制的 Azure AD B2C 租户行为的策略</span><span class="sxs-lookup"><span data-stu-id="1d986-205">Configure policies controlling the behavior of the Azure AD B2C tenant</span></span>

<span data-ttu-id="1d986-206">现在，ASP.NET Core 应用程序配置为使用 Azure AD B2C 进行身份验证， [Authorize 属性](xref:security/authorization/simple)可用来保护你的应用。</span><span class="sxs-lookup"><span data-stu-id="1d986-206">Now that the ASP.NET Core app is configured to use Azure AD B2C for authentication, the [Authorize attribute](xref:security/authorization/simple) can be used to secure your app.</span></span> <span data-ttu-id="1d986-207">在继续开发您的应用程序通过学习：</span><span class="sxs-lookup"><span data-stu-id="1d986-207">Continue developing your app by learning to:</span></span>

* <span data-ttu-id="1d986-208">[自定义 Azure AD B2C 用户界面](/azure/active-directory-b2c/active-directory-b2c-reference-ui-customization)。</span><span class="sxs-lookup"><span data-stu-id="1d986-208">[Customize the Azure AD B2C user interface](/azure/active-directory-b2c/active-directory-b2c-reference-ui-customization).</span></span>
* <span data-ttu-id="1d986-209">[配置密码复杂性要求](/azure/active-directory-b2c/active-directory-b2c-reference-password-complexity)。</span><span class="sxs-lookup"><span data-stu-id="1d986-209">[Configure password complexity requirements](/azure/active-directory-b2c/active-directory-b2c-reference-password-complexity).</span></span>
* <span data-ttu-id="1d986-210">[启用多重身份验证](/azure/active-directory-b2c/active-directory-b2c-reference-mfa)。</span><span class="sxs-lookup"><span data-stu-id="1d986-210">[Enable multi-factor authentication](/azure/active-directory-b2c/active-directory-b2c-reference-mfa).</span></span>
* <span data-ttu-id="1d986-211">配置其他标识提供者，例如[Microsoft](/azure/active-directory-b2c/active-directory-b2c-setup-msa-app)， [Facebook](/azure/active-directory-b2c/active-directory-b2c-setup-fb-app)， [Google](/azure/active-directory-b2c/active-directory-b2c-setup-goog-app)， [Amazon](/azure/active-directory-b2c/active-directory-b2c-setup-amzn-app)， [Twitter](/azure/active-directory-b2c/active-directory-b2c-setup-twitter-app)，等等。</span><span class="sxs-lookup"><span data-stu-id="1d986-211">Configure additional identity providers, such as [Microsoft](/azure/active-directory-b2c/active-directory-b2c-setup-msa-app), [Facebook](/azure/active-directory-b2c/active-directory-b2c-setup-fb-app), [Google](/azure/active-directory-b2c/active-directory-b2c-setup-goog-app), [Amazon](/azure/active-directory-b2c/active-directory-b2c-setup-amzn-app), [Twitter](/azure/active-directory-b2c/active-directory-b2c-setup-twitter-app), and others.</span></span>
* <span data-ttu-id="1d986-212">[使用 Azure AD Graph API](/azure/active-directory-b2c/active-directory-b2c-devquickstarts-graph-dotnet)从 Azure AD B2C 租户中检索其他用户信息，例如组成员身份。</span><span class="sxs-lookup"><span data-stu-id="1d986-212">[Use the Azure AD Graph API](/azure/active-directory-b2c/active-directory-b2c-devquickstarts-graph-dotnet) to retrieve additional user information, such as group membership, from the Azure AD B2C tenant.</span></span>
* <span data-ttu-id="1d986-213">[保护 web API 使用 Azure AD B2C 的 ASP.NET Core](xref:security/authentication/azure-ad-b2c-webapi)。</span><span class="sxs-lookup"><span data-stu-id="1d986-213">[Secure an ASP.NET Core web API using Azure AD B2C](xref:security/authentication/azure-ad-b2c-webapi).</span></span>
* <span data-ttu-id="1d986-214">[从.NET web 应用中使用 Azure AD B2C 调用.NET web API](/azure/active-directory-b2c/active-directory-b2c-devquickstarts-web-api-dotnet)。</span><span class="sxs-lookup"><span data-stu-id="1d986-214">[Call a .NET web API from a .NET web app using Azure AD B2C](/azure/active-directory-b2c/active-directory-b2c-devquickstarts-web-api-dotnet).</span></span>

---
uid: mvc/overview/older-versions-1/security/authenticating-users-with-windows-authentication-cs
title: 使用 Windows 身份验证 （C#） 对用户进行身份验证 |微软文档
author: rick-anderson
description: 了解如何在 MVC 应用程序的上下文中使用 Windows 身份验证。 您将了解如何在应用程序的 Web 身份验证中启用 Windows 身份验证...
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 418bb07e-f369-4119-b4b0-08f890f7abb2
msc.legacyurl: /mvc/overview/older-versions-1/security/authenticating-users-with-windows-authentication-cs
msc.type: authoredcontent
ms.openlocfilehash: fb6ba3d52d7c70d61c6aa16b4ada67cc6bdd4f96
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81540735"
---
# <a name="authenticating-users-with-windows-authentication-c"></a><span data-ttu-id="254ff-104">使用 Windows 身份验证对用户进行身份验证 (C#)</span><span class="sxs-lookup"><span data-stu-id="254ff-104">Authenticating Users with Windows Authentication (C#)</span></span>

<span data-ttu-id="254ff-105">由[微软](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="254ff-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="254ff-106">了解如何在 MVC 应用程序的上下文中使用 Windows 身份验证。</span><span class="sxs-lookup"><span data-stu-id="254ff-106">Learn how to use Windows authentication in the context of an MVC application.</span></span> <span data-ttu-id="254ff-107">您将了解如何在应用程序的 Web 配置文件中启用 Windows 身份验证，以及如何使用 IIS 配置身份验证。</span><span class="sxs-lookup"><span data-stu-id="254ff-107">You learn how to enable Windows authentication within your application's web configuration file and how to configure authentication with IIS.</span></span> <span data-ttu-id="254ff-108">最后，您将了解如何使用 [授权] 属性将控制器操作的访问限制为特定的 Windows 用户或组。</span><span class="sxs-lookup"><span data-stu-id="254ff-108">Finally, you learn how to use the [Authorize] attribute to restrict access to controller actions to particular Windows users or groups.</span></span>

<span data-ttu-id="254ff-109">本教程的目的是说明如何利用 Internet 信息服务中内置的安全功能来密码保护 MVC 应用程序中的视图。</span><span class="sxs-lookup"><span data-stu-id="254ff-109">The goal of this tutorial is to explain how you can take advantage of the security features built into Internet Information Services to password protect the views in your MVC applications.</span></span> <span data-ttu-id="254ff-110">您将了解如何仅允许特定 Windows 用户或属于特定 Windows 组的成员的用户调用控制器操作。</span><span class="sxs-lookup"><span data-stu-id="254ff-110">You learn how to allow controller actions to be invoked only by particular Windows users or users who are members of particular Windows groups.</span></span>

<span data-ttu-id="254ff-111">当您构建内部公司网站（Intranet 网站）并希望用户在访问网站时能够使用其标准 Windows 用户名和密码时，使用 Windows 身份验证是有意义的。</span><span class="sxs-lookup"><span data-stu-id="254ff-111">Using Windows authentication makes sense when you are building an internal company website (an intranet site) and you want your users to be able to use their standard Windows user names and passwords when accessing the website.</span></span> <span data-ttu-id="254ff-112">如果您正在构建面向外的网站（Internet 网站），请考虑改用表单身份验证。</span><span class="sxs-lookup"><span data-stu-id="254ff-112">If you are building an outwards facing website (an Internet website) consider using Forms authentication instead.</span></span>

#### <a name="enabling-windows-authentication"></a><span data-ttu-id="254ff-113">启用 Windows 身份验证</span><span class="sxs-lookup"><span data-stu-id="254ff-113">Enabling Windows Authentication</span></span>

<span data-ttu-id="254ff-114">创建新ASP.NET MVC 应用程序时，默认情况下不会启用 Windows 身份验证。</span><span class="sxs-lookup"><span data-stu-id="254ff-114">When you create a new ASP.NET MVC application, Windows authentication is not enabled by default.</span></span> <span data-ttu-id="254ff-115">窗体身份验证是为 MVC 应用程序启用的默认身份验证类型。</span><span class="sxs-lookup"><span data-stu-id="254ff-115">Forms authentication is the default authentication type enabled for MVC applications.</span></span> <span data-ttu-id="254ff-116">必须通过修改 MVC 应用程序的 Web 配置 （Web.config） 文件来启用 Windows 身份验证。</span><span class="sxs-lookup"><span data-stu-id="254ff-116">You must enable Windows authentication by modifying your MVC application's web configuration (web.config) file.</span></span> <span data-ttu-id="254ff-117">查找&lt;身份验证&gt;部分并对其进行修改以使用 Windows 而不是窗体身份验证，如下所示：</span><span class="sxs-lookup"><span data-stu-id="254ff-117">Find the &lt;authentication&gt; section and modify it to use Windows instead of Forms authentication like this:</span></span>

[!code-xml[Main](authenticating-users-with-windows-authentication-cs/samples/sample1.xml)]

<span data-ttu-id="254ff-118">启用 Windows 身份验证后，Web 服务器将负责对用户进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="254ff-118">When you enable Windows authentication, your web server becomes responsible for authenticating users.</span></span> <span data-ttu-id="254ff-119">通常，在创建和部署ASP.NET MVC 应用程序时，可以使用两种不同类型的 Web 服务器。</span><span class="sxs-lookup"><span data-stu-id="254ff-119">Typically, there are two different types of web servers that you use when creating and deploying an ASP.NET MVC application.</span></span>

<span data-ttu-id="254ff-120">首先，在开发 MVC 应用程序时，您可以使用 Visual Studio 附带的ASP.NET开发 Web 服务器。</span><span class="sxs-lookup"><span data-stu-id="254ff-120">First, while developing an MVC application, you use the ASP.NET Development Web Server included with Visual Studio.</span></span> <span data-ttu-id="254ff-121">默认情况下，ASP.NET开发 Web 服务器在当前 Windows 帐户（用于登录到 Windows 的任何帐户）的上下文中执行所有页面。</span><span class="sxs-lookup"><span data-stu-id="254ff-121">By default, the ASP.NET Development Web Server executes all pages in the context of the current Windows account (whatever account you used to log into Windows).</span></span>

<span data-ttu-id="254ff-122">ASP.NET开发 Web 服务器还支持 NTLM 身份验证。</span><span class="sxs-lookup"><span data-stu-id="254ff-122">The ASP.NET Development Web Server also supports NTLM authentication.</span></span> <span data-ttu-id="254ff-123">您可以通过在解决方案资源管理器窗口中右键单击项目名称并选择"属性"来启用 NTLM 身份验证。</span><span class="sxs-lookup"><span data-stu-id="254ff-123">You can enable NTLM authentication by right-clicking the name of your project in the Solution Explorer window and selecting Properties.</span></span> <span data-ttu-id="254ff-124">接下来，选择 Web 选项卡并选中 NTLM 复选框（参见图 1）。</span><span class="sxs-lookup"><span data-stu-id="254ff-124">Next, select the Web tab and check the NTLM checkbox (see Figure 1).</span></span>

<span data-ttu-id="254ff-125">**图 1 = 为ASP.NET开发 Web 服务器启用 NTLM 身份验证**</span><span class="sxs-lookup"><span data-stu-id="254ff-125">**Figure 1 – Enabling NTLM authentication for the ASP.NET Development Web Server**</span></span>

![clip_image002](authenticating-users-with-windows-authentication-cs/_static/image1.jpg)

<span data-ttu-id="254ff-127">对于生产 Web 应用程序，使用 IIS 作为 Web 服务器。</span><span class="sxs-lookup"><span data-stu-id="254ff-127">For a production web application, on the hand, you use IIS as your web server.</span></span> <span data-ttu-id="254ff-128">IIS 支持多种类型的身份验证，包括：</span><span class="sxs-lookup"><span data-stu-id="254ff-128">IIS supports several types of authentication including:</span></span>

- <span data-ttu-id="254ff-129">基本身份验证 – 定义为 HTTP 1.0 协议的一部分。</span><span class="sxs-lookup"><span data-stu-id="254ff-129">Basic Authentication – Defined as part of the HTTP 1.0 protocol.</span></span> <span data-ttu-id="254ff-130">在 Internet 上以明文（Base64 编码）发送用户名和密码。</span><span class="sxs-lookup"><span data-stu-id="254ff-130">Sends user names and passwords in clear text (Base64 encoded) across the Internet.</span></span> <span data-ttu-id="254ff-131">- 摘要身份验证 – 通过互联网发送密码的哈希值，而不是密码本身。</span><span class="sxs-lookup"><span data-stu-id="254ff-131">- Digest Authentication – Sends a hash of a password, instead of the password itself, across the internet.</span></span> <span data-ttu-id="254ff-132">- 集成 Windows （NTLM） 身份验证 – 使用窗口在 Intranet 环境中使用的最佳身份验证类型。</span><span class="sxs-lookup"><span data-stu-id="254ff-132">- Integrated Windows (NTLM) Authentication – The best type of authentication to use in intranet environments using windows.</span></span> <span data-ttu-id="254ff-133">- 证书身份验证 – 使用客户端证书启用身份验证。</span><span class="sxs-lookup"><span data-stu-id="254ff-133">- Certificate Authentication – Enables authentication using a client-side certificate.</span></span> <span data-ttu-id="254ff-134">证书映射到 Windows 用户帐户。</span><span class="sxs-lookup"><span data-stu-id="254ff-134">The certificate maps to a Windows user account.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="254ff-135">有关这些不同类型的身份验证的更详细概述，请参阅[https://msdn.microsoft.com/library/aa292114(VS.71).aspx](https://msdn.microsoft.com/library/aa292114(VS.71).aspx)。</span><span class="sxs-lookup"><span data-stu-id="254ff-135">For a more detailed overview of these different types of authentication, see [https://msdn.microsoft.com/library/aa292114(VS.71).aspx](https://msdn.microsoft.com/library/aa292114(VS.71).aspx).</span></span>

<span data-ttu-id="254ff-136">您可以使用 Internet 信息服务管理器启用特定类型的身份验证。</span><span class="sxs-lookup"><span data-stu-id="254ff-136">You can use Internet Information Services Manager to enable a particular type of authentication.</span></span> <span data-ttu-id="254ff-137">请注意，对于每个操作系统，所有类型的身份验证都不可用。</span><span class="sxs-lookup"><span data-stu-id="254ff-137">Be aware that all types of authentication are not available in the case of every operating system.</span></span> <span data-ttu-id="254ff-138">此外，如果您将 IIS 7.0 与 Windows Vista 一起使用，则需要在 Internet 信息服务管理器中显示不同类型的 Windows 身份验证之前启用这些身份验证。</span><span class="sxs-lookup"><span data-stu-id="254ff-138">Furthermore, if you are using IIS 7.0 with Windows Vista, you will need to enable the different types of Windows authentication before they appear in the Internet Information Services Manager.</span></span> <span data-ttu-id="254ff-139">打开**控制面板、程序、程序和功能，打开或关闭 Windows 功能**，并展开 Internet 信息服务节点（参见图 2）。</span><span class="sxs-lookup"><span data-stu-id="254ff-139">Open **Control Panel, Programs, Programs and Features, Turn Windows features on or off**, and expand the Internet Information Services node (see Figure 2).</span></span>

<span data-ttu-id="254ff-140">**图 2 = 启用 Windows IIS 功能**</span><span class="sxs-lookup"><span data-stu-id="254ff-140">**Figure 2 – Enabling Windows IIS features**</span></span>

![clip_image004](authenticating-users-with-windows-authentication-cs/_static/image2.jpg)

<span data-ttu-id="254ff-142">使用 Internet 信息服务，您可以启用或禁用不同类型的身份验证。</span><span class="sxs-lookup"><span data-stu-id="254ff-142">Using Internet Information Services, you can enable or disable different types of authentication.</span></span> <span data-ttu-id="254ff-143">例如，图 3 演示了在使用 IIS 7.0 时禁用匿名身份验证和启用集成 Windows （NTLM） 身份验证。</span><span class="sxs-lookup"><span data-stu-id="254ff-143">For example, Figure 3 illustrates disabling anonymous authentication and enabling Integrated Windows (NTLM) authentication when using IIS 7.0.</span></span>

<span data-ttu-id="254ff-144">**图 3 = 启用集成 Windows 身份验证**</span><span class="sxs-lookup"><span data-stu-id="254ff-144">**Figure 3 – Enabling Integrated Windows Authentication**</span></span>

![clip_image006](authenticating-users-with-windows-authentication-cs/_static/image3.jpg)

#### <a name="authorizing-windows-users-and-groups"></a><span data-ttu-id="254ff-146">授权 Windows 用户和组</span><span class="sxs-lookup"><span data-stu-id="254ff-146">Authorizing Windows Users and Groups</span></span>

<span data-ttu-id="254ff-147">启用 Windows 身份验证后，可以使用 [授权] 属性来控制对控制器或控制器操作的访问。</span><span class="sxs-lookup"><span data-stu-id="254ff-147">After you enable Windows authentication, you can use the [Authorize] attribute to control access to controllers or controller actions.</span></span> <span data-ttu-id="254ff-148">此属性可以应用于整个 MVC 控制器或特定控制器操作。</span><span class="sxs-lookup"><span data-stu-id="254ff-148">This attribute can be applied to an entire MVC controller or a particular controller action.</span></span>

<span data-ttu-id="254ff-149">例如，清单 1 中的主页控制器公开了名为 Index（）、公司机密（）和 StephenSecrets（） 的三个操作。</span><span class="sxs-lookup"><span data-stu-id="254ff-149">For example, the Home controller in Listing 1 exposes three actions named Index(), CompanySecrets(), and StephenSecrets().</span></span> <span data-ttu-id="254ff-150">任何人都可以调用 Index（） 操作。</span><span class="sxs-lookup"><span data-stu-id="254ff-150">Anyone can invoke the Index() action.</span></span> <span data-ttu-id="254ff-151">但是，只有 Windows 本地经理组的成员才能调用公司机密（）操作。</span><span class="sxs-lookup"><span data-stu-id="254ff-151">However, only members of the Windows local Managers group can invoke the CompanySecrets() action.</span></span> <span data-ttu-id="254ff-152">最后，只有名为 Stephen 的 Windows 域用户（在雷德蒙德域中）才能调用 StephenSecrets（） 操作。</span><span class="sxs-lookup"><span data-stu-id="254ff-152">Finally, only the Windows domain user named Stephen (in the Redmond domain) can invoke the StephenSecrets() action.</span></span>

<span data-ttu-id="254ff-153">**清单1 = 控制器\主控制器.cs**</span><span class="sxs-lookup"><span data-stu-id="254ff-153">**Listing 1 – Controllers\HomeController.cs**</span></span>

[!code-csharp[Main](authenticating-users-with-windows-authentication-cs/samples/sample2.cs)]

> [!NOTE] 
> 
> <span data-ttu-id="254ff-154">由于 Windows 用户帐户控制 （UAC），使用 Windows Vista 或 Windows 服务器 2008 时，本地管理员组的行为将不同于其他组。</span><span class="sxs-lookup"><span data-stu-id="254ff-154">Because of Windows User Account Control (UAC), when working with Windows Vista or Windows Server 2008, the local Administrators group will behave differently than other groups.</span></span> <span data-ttu-id="254ff-155">除非修改计算机的 UAC 设置，否则 [授权] 属性将无法正确识别本地管理员组的成员。</span><span class="sxs-lookup"><span data-stu-id="254ff-155">The [Authorize] attribute won't correctly recognize a member of the local Administrators group unless you modify your computer's UAC settings.</span></span>

<span data-ttu-id="254ff-156">当您尝试调用控制器操作而不具有正确的权限时，具体会发生什么情况取决于启用的身份验证类型。</span><span class="sxs-lookup"><span data-stu-id="254ff-156">Exactly what happens when you attempt to invoke a controller action without being the right permissions depends on the type of authentication enabled.</span></span> <span data-ttu-id="254ff-157">默认情况下，当使用ASP.NET开发服务器时，只需获得一个空白页。</span><span class="sxs-lookup"><span data-stu-id="254ff-157">By default, when using the ASP.NET Development Server, you simply get a blank page.</span></span> <span data-ttu-id="254ff-158">该页面提供**401 未授权**HTTP 响应状态。</span><span class="sxs-lookup"><span data-stu-id="254ff-158">The page is served with a **401 Not Authorized** HTTP Response Status.</span></span>

<span data-ttu-id="254ff-159">另一方面，如果您使用的 IIS 禁用了匿名身份验证并启用了基本身份验证，则每次请求受保护页面时，您都会不断收到登录对话框提示（参见图 4）。</span><span class="sxs-lookup"><span data-stu-id="254ff-159">If, on the other hand, you are using IIS with Anonymous authentication disabled and Basic authentication enabled, then you keep getting a login dialog prompt each time you request the protected page (see Figure 4).</span></span>

<span data-ttu-id="254ff-160">**图 4 = 基本身份验证登录对话框**</span><span class="sxs-lookup"><span data-stu-id="254ff-160">**Figure 4 – Basic authentication login dialog**</span></span>

![clip_image008](authenticating-users-with-windows-authentication-cs/_static/image4.jpg)

#### <a name="summary"></a><span data-ttu-id="254ff-162">总结</span><span class="sxs-lookup"><span data-stu-id="254ff-162">Summary</span></span>

<span data-ttu-id="254ff-163">本教程介绍了如何在ASP.NET MVC 应用程序的上下文中使用 Windows 身份验证。</span><span class="sxs-lookup"><span data-stu-id="254ff-163">This tutorial explained how you can use Windows authentication in the context of an ASP.NET MVC application.</span></span> <span data-ttu-id="254ff-164">您学习了如何在应用程序的 Web 配置文件中启用 Windows 身份验证，以及如何使用 IIS 配置身份验证。</span><span class="sxs-lookup"><span data-stu-id="254ff-164">You learned how to enable Windows authentication within your application's web configuration file and how to configure authentication with IIS.</span></span> <span data-ttu-id="254ff-165">最后，您学习了如何使用 [授权] 属性将控制器操作的访问限制为特定的 Windows 用户或组。</span><span class="sxs-lookup"><span data-stu-id="254ff-165">Finally, you learned how to use the [Authorize] attribute to restrict access to controller actions to particular Windows users or groups.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="254ff-166">[上一页](authenticating-users-with-forms-authentication-cs.md)
> [下一页](preventing-javascript-injection-attacks-cs.md)</span><span class="sxs-lookup"><span data-stu-id="254ff-166">[Previous](authenticating-users-with-forms-authentication-cs.md)
[Next](preventing-javascript-injection-attacks-cs.md)</span></span>

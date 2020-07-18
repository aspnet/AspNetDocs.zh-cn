---
uid: web-api/overview/security/integrated-windows-authentication
title: 集成的 Windows 身份验证 |Microsoft Docs
author: MikeWasson
description: 介绍如何在 ASP.NET Web API 中使用集成的 Windows 身份验证。
ms.author: riande
ms.date: 12/18/2012
ms.assetid: 71ee4c78-c500-4d1c-b761-b4e161a291b5
msc.legacyurl: /web-api/overview/security/integrated-windows-authentication
msc.type: authoredcontent
ms.openlocfilehash: c5fe57c4a20e28fa434659a75484e3a4c37195f8
ms.sourcegitcommit: 000cbcd1de66fe8a766f203ef2d6f009e4435f53
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/16/2020
ms.locfileid: "86424782"
---
# <a name="integrated-windows-authentication"></a><span data-ttu-id="7f385-103">Windows 集成身份验证</span><span class="sxs-lookup"><span data-stu-id="7f385-103">Integrated Windows Authentication</span></span>

<span data-ttu-id="7f385-104">作者： [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="7f385-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="7f385-105">使用集成的 Windows 身份验证，用户可以使用 Kerberos 或 NTLM 通过其 Windows 凭据进行登录。</span><span class="sxs-lookup"><span data-stu-id="7f385-105">Integrated Windows authentication enables users to log in with their Windows credentials, using Kerberos or NTLM.</span></span> <span data-ttu-id="7f385-106">客户端在授权标头中发送凭据。</span><span class="sxs-lookup"><span data-stu-id="7f385-106">The client sends credentials in the Authorization header.</span></span> <span data-ttu-id="7f385-107">Windows 身份验证最适合 Intranet 环境。</span><span class="sxs-lookup"><span data-stu-id="7f385-107">Windows authentication is best suited for an intranet environment.</span></span> <span data-ttu-id="7f385-108">有关详细信息，请参阅 [Windows 身份验证](https://www.iis.net/configreference/system.webserver/security/authentication/windowsauthentication)。</span><span class="sxs-lookup"><span data-stu-id="7f385-108">For more information, see [Windows Authentication](https://www.iis.net/configreference/system.webserver/security/authentication/windowsauthentication).</span></span>

| <span data-ttu-id="7f385-109">优点</span><span class="sxs-lookup"><span data-stu-id="7f385-109">Advantages</span></span> | <span data-ttu-id="7f385-110">缺点</span><span class="sxs-lookup"><span data-stu-id="7f385-110">Disadvantages</span></span> |
| --- | --- |
| <span data-ttu-id="7f385-111">内置到 IIS 中。</span><span class="sxs-lookup"><span data-stu-id="7f385-111">Built into IIS.</span></span> | <span data-ttu-id="7f385-112">不建议用于 Internet 应用程序。</span><span class="sxs-lookup"><span data-stu-id="7f385-112">Not recommended for Internet applications.</span></span> | 
| <span data-ttu-id="7f385-113">不会发送请求中的用户凭据。</span><span class="sxs-lookup"><span data-stu-id="7f385-113">Does not send the user credentials in the request.</span></span> | <span data-ttu-id="7f385-114">要求在客户端中提供 Kerberos 或 NTLM 支持。</span><span class="sxs-lookup"><span data-stu-id="7f385-114">Requires Kerberos or NTLM support in the client.</span></span> |
| <span data-ttu-id="7f385-115">如果客户端计算机属于域（例如 intranet 应用程序），则用户无需输入凭据。</span><span class="sxs-lookup"><span data-stu-id="7f385-115">If the client computer belongs to the domain (for example, intranet application), the user does not need to enter credentials.</span></span> | <span data-ttu-id="7f385-116">客户端必须在 Active Directory 域中。</span><span class="sxs-lookup"><span data-stu-id="7f385-116">Client must be in the Active Directory domain.</span></span> |

> [!NOTE]
> <span data-ttu-id="7f385-117">如果你的应用程序托管在 Azure 上，并且你有本地 Active Directory 域，请考虑将你的本地 AD 与 Azure Active Directory 进行联合。</span><span class="sxs-lookup"><span data-stu-id="7f385-117">If your application is hosted on Azure and you have an on-premise Active Directory domain, consider federating your on-premise AD with Azure Active Directory.</span></span> <span data-ttu-id="7f385-118">这样，用户便可以使用其本地凭据登录，但 Azure AD 会执行身份验证。</span><span class="sxs-lookup"><span data-stu-id="7f385-118">That way, users can log in with their on-premise credentials, but the authentication is performed by Azure AD.</span></span> <span data-ttu-id="7f385-119">有关详细信息，请参阅[Azure 身份验证](../../../visual-studio/overview/2012/windows-azure-authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="7f385-119">For more information, see [Azure Authentication](../../../visual-studio/overview/2012/windows-azure-authentication.md).</span></span>

<span data-ttu-id="7f385-120">若要创建使用集成 Windows 身份验证的应用程序，请在 MVC 4 项目向导中选择 "Intranet 应用程序" 模板。</span><span class="sxs-lookup"><span data-stu-id="7f385-120">To create an application that uses Integrated Windows authentication, select the "Intranet Application" template in the MVC 4 project wizard.</span></span> <span data-ttu-id="7f385-121">此项目模板将以下设置置于 Web.config 文件中：</span><span class="sxs-lookup"><span data-stu-id="7f385-121">This project template puts the following setting in the Web.config file:</span></span>

[!code-xml[Main](integrated-windows-authentication/samples/sample1.xml)]

<span data-ttu-id="7f385-122">在客户端，集成的 Windows 身份验证与支持[协商](http://www.ietf.org/rfc/rfc4559.txt)身份验证方案的任何浏览器（包括最主要的浏览器）一起工作。</span><span class="sxs-lookup"><span data-stu-id="7f385-122">On the client side, Integrated Windows authentication works with any browser that supports the [Negotiate](http://www.ietf.org/rfc/rfc4559.txt) authentication scheme, which includes most major browsers.</span></span> <span data-ttu-id="7f385-123">对于 .NET 客户端应用程序， **HttpClient**类支持 Windows 身份验证：</span><span class="sxs-lookup"><span data-stu-id="7f385-123">For .NET client applications, the **HttpClient** class supports Windows authentication:</span></span>

[!code-csharp[Main](integrated-windows-authentication/samples/sample2.cs)]

<span data-ttu-id="7f385-124">Windows 身份验证容易受到跨站点请求伪造（CSRF）攻击。</span><span class="sxs-lookup"><span data-stu-id="7f385-124">Windows authentication is vulnerable to cross-site request forgery (CSRF) attacks.</span></span> <span data-ttu-id="7f385-125">请参阅[防止跨站点请求伪造（CSRF）攻击](preventing-cross-site-request-forgery-csrf-attacks.md)。</span><span class="sxs-lookup"><span data-stu-id="7f385-125">See [Preventing Cross-Site Request Forgery (CSRF) Attacks](preventing-cross-site-request-forgery-csrf-attacks.md).</span></span>

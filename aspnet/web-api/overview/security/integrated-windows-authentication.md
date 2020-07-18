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
# <a name="integrated-windows-authentication"></a>Windows 集成身份验证

作者： [Mike Wasson](https://github.com/MikeWasson)

使用集成的 Windows 身份验证，用户可以使用 Kerberos 或 NTLM 通过其 Windows 凭据进行登录。 客户端在授权标头中发送凭据。 Windows 身份验证最适合 Intranet 环境。 有关详细信息，请参阅 [Windows 身份验证](https://www.iis.net/configreference/system.webserver/security/authentication/windowsauthentication)。

| 优点 | 缺点 |
| --- | --- |
| 内置到 IIS 中。 | 不建议用于 Internet 应用程序。 | 
| 不会发送请求中的用户凭据。 | 要求在客户端中提供 Kerberos 或 NTLM 支持。 |
| 如果客户端计算机属于域（例如 intranet 应用程序），则用户无需输入凭据。 | 客户端必须在 Active Directory 域中。 |

> [!NOTE]
> 如果你的应用程序托管在 Azure 上，并且你有本地 Active Directory 域，请考虑将你的本地 AD 与 Azure Active Directory 进行联合。 这样，用户便可以使用其本地凭据登录，但 Azure AD 会执行身份验证。 有关详细信息，请参阅[Azure 身份验证](../../../visual-studio/overview/2012/windows-azure-authentication.md)。

若要创建使用集成 Windows 身份验证的应用程序，请在 MVC 4 项目向导中选择 "Intranet 应用程序" 模板。 此项目模板将以下设置置于 Web.config 文件中：

[!code-xml[Main](integrated-windows-authentication/samples/sample1.xml)]

在客户端，集成的 Windows 身份验证与支持[协商](http://www.ietf.org/rfc/rfc4559.txt)身份验证方案的任何浏览器（包括最主要的浏览器）一起工作。 对于 .NET 客户端应用程序， **HttpClient**类支持 Windows 身份验证：

[!code-csharp[Main](integrated-windows-authentication/samples/sample2.cs)]

Windows 身份验证容易受到跨站点请求伪造（CSRF）攻击。 请参阅[防止跨站点请求伪造（CSRF）攻击](preventing-cross-site-request-forgery-csrf-attacks.md)。

---
uid: mvc/overview/older-versions-1/security/authenticating-users-with-windows-authentication-vb
title: 使用 Windows 身份验证 （VB） 对用户进行身份验证 |微软文档
author: rick-anderson
description: 了解如何在 MVC 应用程序的上下文中使用 Windows 身份验证。 您将了解如何在应用程序的 Web 身份验证中启用 Windows 身份验证...
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 532fa051-7d5c-4d6d-87f6-339ce4b84c44
msc.legacyurl: /mvc/overview/older-versions-1/security/authenticating-users-with-windows-authentication-vb
msc.type: authoredcontent
ms.openlocfilehash: 446dcc338f61e1f76478c1085773e7ad089c73f4
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81540592"
---
# <a name="authenticating-users-with-windows-authentication-vb"></a>使用 Windows 身份验证对用户进行身份验证 (VB)

由[微软](https://github.com/microsoft)

> 了解如何在 MVC 应用程序的上下文中使用 Windows 身份验证。 您将了解如何在应用程序的 Web 配置文件中启用 Windows 身份验证，以及如何使用 IIS 配置身份验证。 最后，您将了解如何使用 [授权] 属性将控制器操作的访问限制为特定的 Windows 用户或组。

本教程的目的是说明如何利用 Internet 信息服务中内置的安全功能来密码保护 MVC 应用程序中的视图。 您将了解如何仅允许特定 Windows 用户或属于特定 Windows 组的成员的用户调用控制器操作。

当您构建内部公司网站（Intranet 网站）并希望用户在访问网站时能够使用其标准 Windows 用户名和密码时，使用 Windows 身份验证是有意义的。 如果您正在构建面向外的网站（Internet 网站），请考虑改用表单身份验证。

#### <a name="enabling-windows-authentication"></a>启用 Windows 身份验证

创建新ASP.NET MVC 应用程序时，默认情况下不会启用 Windows 身份验证。 窗体身份验证是为 MVC 应用程序启用的默认身份验证类型。 必须通过修改 MVC 应用程序的 Web 配置 （Web.config） 文件来启用 Windows 身份验证。 查找&lt;身份验证&gt;部分并对其进行修改以使用 Windows 而不是窗体身份验证，如下所示：

[!code-xml[Main](authenticating-users-with-windows-authentication-vb/samples/sample1.xml)]

启用 Windows 身份验证后，Web 服务器将负责对用户进行身份验证。 通常，在创建和部署ASP.NET MVC 应用程序时，可以使用两种不同类型的 Web 服务器。

首先，在开发 MVC 应用程序时，您可以使用 Visual Studio 附带的ASP.NET开发 Web 服务器。 默认情况下，ASP.NET开发 Web 服务器在当前 Windows 帐户（用于登录到 Windows 的任何帐户）的上下文中执行所有页面。

ASP.NET开发 Web 服务器还支持 NTLM 身份验证。 您可以通过在解决方案资源管理器窗口中右键单击项目名称并选择"属性"来启用 NTLM 身份验证。 接下来，选择 Web 选项卡并选中 NTLM 复选框（参见图 1）。

**图 1 = 为ASP.NET开发 Web 服务器启用 NTLM 身份验证**

![clip_image002](authenticating-users-with-windows-authentication-vb/_static/image1.jpg)

对于生产 Web 应用程序，使用 IIS 作为 Web 服务器。 IIS 支持多种类型的身份验证，包括：

- 基本身份验证 – 定义为 HTTP 1.0 协议的一部分。 在 Internet 上以明文（Base64 编码）发送用户名和密码。 - 摘要身份验证 – 通过互联网发送密码的哈希值，而不是密码本身。 - 集成 Windows （NTLM） 身份验证 – 使用窗口在 Intranet 环境中使用的最佳身份验证类型。 - 证书身份验证 – 使用客户端证书启用身份验证。 证书映射到 Windows 用户帐户。

> [!NOTE] 
> 
> 有关这些不同类型的身份验证的更详细概述，请参阅[https://msdn.microsoft.com/library/aa292114(VS.71).aspx](https://msdn.microsoft.com/library/aa292114(VS.71).aspx)。

您可以使用 Internet 信息服务管理器启用特定类型的身份验证。 请注意，对于每个操作系统，所有类型的身份验证都不可用。 此外，如果您将 IIS 7.0 与 Windows Vista 一起使用，则需要在 Internet 信息服务管理器中显示不同类型的 Windows 身份验证之前启用这些身份验证。 打开**控制面板、程序、程序和功能，打开或关闭 Windows 功能**，并展开 Internet 信息服务节点（参见图 2）。

**图 2 = 启用 Windows IIS 功能**

![clip_image004](authenticating-users-with-windows-authentication-vb/_static/image2.jpg)

使用 Internet 信息服务，您可以启用或禁用不同类型的身份验证。 例如，图 3 演示了在使用 IIS 7.0 时禁用匿名身份验证和启用集成 Windows （NTLM） 身份验证。

**图 3 = 启用集成 Windows 身份验证**

![clip_image006](authenticating-users-with-windows-authentication-vb/_static/image3.jpg)

#### <a name="authorizing-windows-users-and-groups"></a>授权 Windows 用户和组

启用 Windows 身份验证后，可以使用&lt;"授权"&gt;属性来控制对控制器或控制器操作的访问。 此属性可以应用于整个 MVC 控制器或特定控制器操作。

例如，清单 1 中的主页控制器公开了名为 Index（）、公司机密（）和 StephenSecrets（） 的三个操作。 任何人都可以调用 Index（） 操作。 但是，只有 Windows 本地经理组的成员才能调用公司机密（）操作。 最后，只有名为 Stephen 的 Windows 域用户（在雷德蒙德域中）才能调用 StephenSecrets（） 操作。

**清单1 = 控制器\主控制器.vb**

[!code-vb[Main](authenticating-users-with-windows-authentication-vb/samples/sample2.vb)]

> [!NOTE]
> 由于 Windows 用户帐户控制 （UAC），使用 Windows Vista 或 Windows 服务器 2008 时，本地管理员组的行为将不同于其他组。 除非您&lt;修改&gt;计算机的 UAC 设置，否则"授权"属性将无法正确识别本地管理员组的成员。

当您尝试调用控制器操作而不具有正确的权限时，具体会发生什么情况取决于启用的身份验证类型。 默认情况下，当使用ASP.NET开发服务器时，只需获得一个空白页。 该页面提供**401 未授权**HTTP 响应状态。

另一方面，如果您使用的 IIS 禁用了匿名身份验证并启用了基本身份验证，则每次请求受保护页面时，您都会不断收到登录对话框提示（参见图 4）。

**图 4 = 基本身份验证登录对话框**

![clip_image008](authenticating-users-with-windows-authentication-vb/_static/image4.jpg)

#### <a name="summary"></a>总结

本教程介绍了如何在ASP.NET MVC 应用程序的上下文中使用 Windows 身份验证。 您学习了如何在应用程序的 Web 配置文件中启用 Windows 身份验证，以及如何使用 IIS 配置身份验证。 最后，您学习了如何使用&lt;"授权"&gt;属性将控制器操作的访问限制为特定的 Windows 用户或组。

> [!div class="step-by-step"]
> [上一页](authenticating-users-with-forms-authentication-vb.md)
> [下一页](preventing-javascript-injection-attacks-vb.md)

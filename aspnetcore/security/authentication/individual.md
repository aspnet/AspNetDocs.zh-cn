---
title: 基于 ASP.NET Core 项目使用单个用户帐户创建项目
author: rick-anderson
description: 发现基于 ASP.NET Core 项目使用单个用户帐户创建的文章。
ms.author: riande
ms.date: 11/30/2017
uid: security/authentication/individual
ms.openlocfilehash: c73365eafaf2c38ef02c3c83ccf5ced4264f7dc0
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57033834"
---
# <a name="articles-based-on-aspnet-core-projects-created-with-individual-user-accounts"></a>基于 ASP.NET Core 项目使用单个用户帐户创建项目

ASP.NET Core 标识包含在 Visual Studio 中使用"单个用户帐户"选项的项目模板中。

中使用的.NET Core CLI 中可用的身份验证模板`-au Individual`:

::: moniker range=">= aspnetcore-2.1"

```console
dotnet new mvc -au Individual
dotnet new webapp -au Individual
```

::: moniker-end

::: moniker range="= aspnetcore-2.0"

```console
dotnet new mvc -au Individual
dotnet new razor -au Individual
```

::: moniker-end

请参阅[此 GitHub 问题](https://github.com/aspnet/AspNetCore/issues/5833)web API 身份验证。

<a name="no"></a>
## <a name="no-authentication"></a>无身份验证

在.NET Core CLI 与指定身份验证`-au`选项。 在 Visual Studio 中，**更改身份验证**对话框是适用于新 web 应用程序。 默认值为 Visual Studio 中的新 web 应用**无身份验证**。

使用无身份验证创建的项目：

* 不包含 web 页面和 UI 中登录和注销。
* 不包含身份验证代码。

<a name="win"></a>
## <a name="windows-authentication"></a>Windows 身份验证

Windows 身份验证指定为新 web 应用程序中使用.NET Core CLI`-au Windows`选项。 在 Visual Studio 中，**更改身份验证**对话框提供了**Windows 身份验证**选项。

如果选择 Windows 身份验证，则该应用程序配置为使用[Windows 身份验证 IIS 模块](xref:host-and-deploy/iis/modules)。 Windows 身份验证适用于 Intranet web 站点。

## <a name="additional-resources"></a>其他资源

以下文章演示了如何使用 ASP.NET Core 使用单个用户帐户的模板中生成的代码：

* [使用 SMS 设置双因素身份验证](xref:security/authentication/2fa)
* [ASP.NET Core 中的帐户确认和密码恢复](xref:security/authentication/accconfirm)
* [使用受授权的用户数据创建 ASP.NET Core 应用](xref:security/authorization/secure-data)

---
uid: webhooks/source
title: ASP.NET WebHooks 源代码和 NuGet 包 |微软文档
author: rick-anderson
description: 指向ASP.NET WebHooks 源代码和 NuGet 包的链接
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 91a62bfa-ea3a-41f9-a2e1-e90d2c8fc8ca
ms.openlocfilehash: ad368125878871c0e38f35152c86fe4eea143924
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675324"
---
# <a name="aspnet-webhooks-source-code-and-nuget-packages"></a>ASP.NET WebHooks 源代码和 NuGet 包

微软ASP.NETWebHooks是微软ASP.NET模块系列的一部分，并作为[开放源码项目在GitHub上](https://github.com/aspnet/WebHooks)托管。 这意味着我们接受捐款，但在提交拉取请求之前，请查看["贡献指南](https://github.com/aspnet/Home/blob/master/CONTRIBUTING.md)"。

您现在阅读的此联机文档也托管[在 GitHub 上作为开源](http://docs.asp.net/en/latest/contribute/style-guide.html#style-guide)，并接受贡献。

## <a name="nuget-packages"></a>NuGet 包

[NuGet 包](https://nuget.org/packages?q=Microsoft.AspNet.WebHooks)分为三个部分：

* [常见](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Common)：在发送方和接收方之间共享的通用包。

* [发件人](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Custom)：一组包，支持向他人发送您自己的 WebHook。 发送 WebHook 的功能在[发送 WebHook](sending/senders.md)中进行了更详细的描述。

* [接收者](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers)：一组支持接收他人 WebHook 的包。 接收 WebHook 的功能在[接收 WebHook](receiving/index.md)中进行了更详细的描述。

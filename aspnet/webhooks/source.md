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
# <a name="aspnet-webhooks-source-code-and-nuget-packages"></a><span data-ttu-id="8728b-103">ASP.NET WebHooks 源代码和 NuGet 包</span><span class="sxs-lookup"><span data-stu-id="8728b-103">ASP.NET WebHooks source code and NuGet packages</span></span>

<span data-ttu-id="8728b-104">微软ASP.NETWebHooks是微软ASP.NET模块系列的一部分，并作为[开放源码项目在GitHub上](https://github.com/aspnet/WebHooks)托管。</span><span class="sxs-lookup"><span data-stu-id="8728b-104">Microsoft ASP.NET WebHooks is part of the Microsoft ASP.NET family of modules and is hosted as an [Open Source Project on GitHub](https://github.com/aspnet/WebHooks).</span></span> <span data-ttu-id="8728b-105">这意味着我们接受捐款，但在提交拉取请求之前，请查看["贡献指南](https://github.com/aspnet/Home/blob/master/CONTRIBUTING.md)"。</span><span class="sxs-lookup"><span data-stu-id="8728b-105">This means that we accept contributions, but please look at the [Contribution Guidelines](https://github.com/aspnet/Home/blob/master/CONTRIBUTING.md) before submitting a pull request.</span></span>

<span data-ttu-id="8728b-106">您现在阅读的此联机文档也托管[在 GitHub 上作为开源](http://docs.asp.net/en/latest/contribute/style-guide.html#style-guide)，并接受贡献。</span><span class="sxs-lookup"><span data-stu-id="8728b-106">This online documentation which you are reading now is also hosted as [Open Source on GitHub](http://docs.asp.net/en/latest/contribute/style-guide.html#style-guide) and also accepts contributions.</span></span>

## <a name="nuget-packages"></a><span data-ttu-id="8728b-107">NuGet 包</span><span class="sxs-lookup"><span data-stu-id="8728b-107">NuGet packages</span></span>

<span data-ttu-id="8728b-108">[NuGet 包](https://nuget.org/packages?q=Microsoft.AspNet.WebHooks)分为三个部分：</span><span class="sxs-lookup"><span data-stu-id="8728b-108">The [NuGet packages](https://nuget.org/packages?q=Microsoft.AspNet.WebHooks) are divided into three parts:</span></span>

* <span data-ttu-id="8728b-109">[常见](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Common)：在发送方和接收方之间共享的通用包。</span><span class="sxs-lookup"><span data-stu-id="8728b-109">[Common](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Common): A common package that is shared between senders and receivers.</span></span>

* <span data-ttu-id="8728b-110">[发件人](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Custom)：一组包，支持向他人发送您自己的 WebHook。</span><span class="sxs-lookup"><span data-stu-id="8728b-110">[Sender](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Custom): A set of packages supporting sending your own WebHooks to others.</span></span> <span data-ttu-id="8728b-111">发送 WebHook 的功能在[发送 WebHook](sending/senders.md)中进行了更详细的描述。</span><span class="sxs-lookup"><span data-stu-id="8728b-111">The functionality for sending WebHooks is described in more detail in [Sending WebHooks](sending/senders.md).</span></span>

* <span data-ttu-id="8728b-112">[接收者](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers)：一组支持接收他人 WebHook 的包。</span><span class="sxs-lookup"><span data-stu-id="8728b-112">[Receivers](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers): A set of packages supporting receiving WebHooks from others.</span></span> <span data-ttu-id="8728b-113">接收 WebHook 的功能在[接收 WebHook](receiving/index.md)中进行了更详细的描述。</span><span class="sxs-lookup"><span data-stu-id="8728b-113">The functionality for receiving WebHooks is described in more detail in [Receiving WebHooks](receiving/index.md).</span></span>

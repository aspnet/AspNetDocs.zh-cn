---
uid: webhooks/receiving/dependencies
title: ASP.NET WebHooks 接收器依赖项 |微软文档
author: rick-anderson
description: ASP.NET WebHook 中的接收器依赖项和依赖项注入。
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 5125e483-c2bb-435b-8cd1-21d3499bfaaf
ms.openlocfilehash: b50442b3d95512bc0db7583b93de3bbef2d4bb4a
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675197"
---
# <a name="aspnet-webhooks-receiver-dependencies"></a>ASP.NET WebHooks 接收器依赖项

微软ASP.NETWebHooks的设计考虑到了依赖注入。 使用依赖项注入引擎可以将系统中的大多数依赖项替换为替代实现。

有关接收器依赖项列表，请参阅[依赖项范围扩展](https://github.com/aspnet/aspnetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Extensions/DependencyScopeExtensions.cs)。 如果未注册依赖项，则使用默认实现。 有关默认实现的列表，请参阅[Receiver 服务](https://github.com/aspnet/aspnetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Services/ReceiverServices.cs)。

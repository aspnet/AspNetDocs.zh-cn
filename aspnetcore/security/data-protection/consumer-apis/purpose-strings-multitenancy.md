---
title: 目的层次结构和 ASP.NET Core 中的多租户
author: rick-anderson
description: 了解目的字符串层次结构和多租户因为它与 ASP.NET Core 数据保护 Api。
ms.author: riande
ms.date: 10/14/2016
uid: security/data-protection/consumer-apis/purpose-strings-multitenancy
ms.openlocfilehash: 1133d40e7b325d58b3f70e7387494dae36ff8ac9
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57047004"
---
# <a name="purpose-hierarchy-and-multi-tenancy-in-aspnet-core"></a>目的层次结构和 ASP.NET Core 中的多租户

由于`IDataProtector`也是隐式`IDataProtectionProvider`，目的可以链接在一起。 在这种情况下，`provider.CreateProtector([ "purpose1", "purpose2" ])`等效于`provider.CreateProtector("purpose1").CreateProtector("purpose2")`。

这允许通过数据保护系统的一些有趣的层次结构关系。 在上例中的[Contoso.Messaging.SecureMessage](xref:security/data-protection/consumer-apis/purpose-strings#data-protection-contoso-purpose)，可以调用 SecureMessage 组件`provider.CreateProtector("Contoso.Messaging.SecureMessage")`一次前期和到专用缓存的结果`_myProvider`字段。 然后可以通过调用创建将来的保护程序`_myProvider.CreateProtector("User: username")`，并且这些保护程序将用于保护单个消息。

这也可以被翻转。 哪些主机可以使用其自己的身份验证和状态管理系统配置 （一个 CMS 似乎是合理） 的多个租户，以及每个租户，请考虑单个逻辑应用程序。 总括性应用程序具有单一的主提供程序，并且它将调用`provider.CreateProtector("Tenant 1")`和`provider.CreateProtector("Tenant 2")`为每个租户提供其自己的数据保护系统的独立的切片。 租户然后可以派生他们自己单独的保护程序，基于其自身的需求，但不管如何努力尝试不能创建其发生冲突的保护程序与其他任何租户系统中。 以图形方式，这表示如下所示。

![多租户目的](purpose-strings-multitenancy/_static/purposes-multi-tenancy.png)

>[!WARNING]
> 此操作假定涵盖性应用程序控制哪些 Api 可供各个租户和租户不能在服务器上执行任意代码。 如果租户可以执行任意代码，它们可以执行专用的反射来中断隔离保证，或它们只是无法直接读取主密钥密钥材料和派生任何子项力度。

数据保护系统实际上使用其默认的箱配置中的多租户的排序。 默认情况下工作进程帐户的用户配置文件文件夹 （或用于 IIS 应用程序池标识注册表） 中存储主密钥的密钥材料。 但它实际上相当通常使用单个帐户来运行多个应用程序，并因此所有这些应用程序将最终共享主密钥材料。 若要解决此问题，数据保护系统将自动作为整体的用途链中的第一个元素插入唯一对每个应用程序标识符。 此隐式提供给[将单个应用程序隔离](xref:security/data-protection/configuration/overview#per-application-isolation)从另一个方法是有效地将每个应用程序，如系统和保护程序的创建过程中唯一租户看起来与上面的图像相同。

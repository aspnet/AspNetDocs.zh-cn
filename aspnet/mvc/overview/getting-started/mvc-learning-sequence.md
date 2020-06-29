---
uid: mvc/overview/getting-started/mvc-learning-sequence
title: MVC 推荐的教程和文章 |Microsoft Docs
author: Rick-Anderson
description: 此页面包含指向 ASP.NET MVC 教程的链接，以及用于关注这些教程的建议顺序。
ms.author: riande
ms.date: 05/22/2015
ms.assetid: 8513a57a-2d45-4d6b-881c-15a01c5cbb1c
msc.legacyurl: /mvc/overview/getting-started/mvc-learning-sequence
msc.type: authoredcontent
ms.openlocfilehash: 7dc81cf09309194df4471fedfc74d4051f0fdb78
ms.sourcegitcommit: 8d34fb54e790cfba2d64097afc8276da5b22283e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2020
ms.locfileid: "85484212"
---
# <a name="mvc-recommended-tutorials-and-articles"></a>MVC 建议的教程和文章

作者： [Rick Anderson](https://twitter.com/RickAndMSFT)

<a id="pwd"></a>
## <a name="getting-started"></a>入门

- [与 ASP.NET MVC 5 入门](introduction/getting-started.md)此11部分系列是一个不错的开端。
- [Pluralsight ASP.NET MVC 5 基础知识](https://pluralsight.com/training/Player?author=scott-allen&amp;name=aspdotnet-mvc5-fundamentals-m1-introduction&amp;mode=live&amp;clip=0&amp;course=aspdotnet-mvc5-fundamentals)（视频课程）
- 吴建 Galloway 和 Christopher Harrison 的[ASP.NET MVC 简介](https://channel9.msdn.com/Series/Introduction-to-ASP-NET-MVC)
- [ASP.NET MVC 5 应用程序的生命周期](lifecycle-of-an-aspnet-mvc-5-application.md)ASP.NET MVC 5 应用程序的生命周期的 PDF 文档。

<a id="con"></a>
## <a name="working-with-data"></a>使用数据

- [使用 MVC 5 Code First 入门](getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)Tom Dykstra 备受好评的系列深入深入到 EF。

<a id="wj"></a>
## <a name="security"></a>安全性

- [使用身份验证和 SQL 数据库创建 ASP.NET MVC 应用并将其部署到 Azure](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/)此热门教程介绍了如何创建简单的应用程序，以及如何添加成员身份和角色。
- [使用 Facebook、Twitter、LinkedIn 和 Google OAuth2 登录创建 ASP.NET MVC 5 应用程序](../security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)本教程演示如何生成一个 ASP.NET MVC 5 web 应用程序，该应用程序允许用户2.0 使用来自外部身份验证提供程序（如 Facebook、Twitter、LinkedIn、Microsoft 或 Google）的凭据登录。
- [创建具有登录、电子邮件确认和密码重置的安全 ASP.NET MVC 5 web 应用](../security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md)第一系列有关标识的，其中包括用于[重新发送确认链接](../security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md#rsend)的代码。
- [ASP.NET MVC 5 应用（带有 SMS 和电子邮件双因素身份验证）](../security/aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md)标识序列上的第二个。
- [向 ASP.NET 和 Azure 应用服务部署密码和其他敏感数据的最佳做法](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)
- [使用 SMS 和电子邮件的双因素身份验证 ASP.NET Identity](../../../identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity.md) `isPersistent`安全 cookie 的代码要求用户在登录之前获得验证的电子邮件帐户、提供如何检查2FA 要求等。
- [帐户确认和密码恢复与 ASP.NET Identity](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)提供有关在[使用登录创建安全 ASP.NET MVC 5 web 应用中找不到的标识的详细信息、电子邮件确认和密码重置，](../security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md)如如何允许用户重置其忘记的密码。

<a id="da"></a>
## <a name="azure"></a>Azure

- [在 Azure 中创建 ASP.NET web 应用](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/)部署到 Azure 的简短教程。
- [使用身份验证和 SQL 数据库创建 ASP.NET MVC 应用并将其部署到 Azure](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/)

<a id="perf"></a>
## <a name="performance-and-debugging"></a>性能和调试

- [使用 Glimpse 分析和调试 ASP.NET MVC 应用](../performance/profile-and-debug-your-aspnet-mvc-app-with-glimpse.md)

## <a name="aspnet-mvc-dropdownlistfor-with-selectlistitem"></a>ASP.NET MVC DropDownListFor with SelectListItem

当使用 <xref:System.Web.Mvc.Html.SelectExtensions.DropDownListFor%2A> helper 并向其传递从中填充它的的集合时 `SelectListItem` ，将 `DropdownListFor` 修改调用后传递的集合。 `DropdownListFor`将 `SelectListItems` 所选属性更改为下拉列表选择的任何属性。 这会导致意外的行为。

<xref:System.Web.Mvc.Html.SelectExtensions.DropDownListFor%2A>、、 <xref:System.Web.Mvc.Html.SelectExtensions.DropDownList%2A> 、 <xref:System.Web.Mvc.Html.SelectExtensions.EnumDropDownListFor%2A> <xref:System.Web.Mvc.Html.SelectExtensions.ListBox%2A> 和更新了 <xref:System.Web.Mvc.Html.SelectExtensions.ListBoxFor%2A> `IEnumerable<SelectListItem>` ViewData 中传递的或找到的任何属性。

解决方法是为 `SelectListItem` 模型中的每个属性创建单独的枚举，其中包含不同的实例。

有关详细信息，请参阅

* [DropdownListFor 修改传递给它的 SelectListItem 集合](http://web.archive.org/web/20140902031437/http://aspnetwebstack.codeplex.com/workitem/1913)
* [GetSelectListWithDefaultValue 修改 IEnumerable <SelectListItem> selectList](https://github.com/aspnet/AspNetWebStack/issues/271)
---
uid: web-api/overview/security/authentication-and-authorization-in-aspnet-web-api
title: ASP.NET Web API 中的身份验证和授权 |Microsoft Docs
author: MikeWasson
description: 提供 ASP.NET Web API 中身份验证和授权的一般概述。
ms.author: riande
ms.date: 11/27/2012
ms.assetid: 6dfb51ea-9f4d-4e70-916c-8ef8344a88d6
msc.legacyurl: /web-api/overview/security/authentication-and-authorization-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 368d2b9456d12b2bb4063a23333e5c8837faa3b8
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345631"
---
# <a name="authentication-and-authorization-in-aspnet-web-api"></a>Authentication and Authorization in ASP.NET Web API（ASP.NET Web API 中的身份验证和授权）

作者： [Mike Wasson](https://github.com/MikeWasson)

你已经创建了一个 web API，但现在想要控制对它的访问。 在这一系列的文章中，我们将介绍一些用于保护 web API 不受未经授权的用户使用的选项。 此系列涵盖身份验证和授权。

- *身份验证* 知道用户的身份。 例如，Alice 使用用户名和密码登录，并且服务器使用密码对 Alice 进行身份验证。
- *授权* 是指是否允许用户执行某个操作。 例如，Alice 有权获取资源，但不能创建资源。

本系列文章中的第一篇文章概括介绍了 ASP.NET Web API 中的身份验证和授权。 其他主题介绍了 Web API 的常见身份验证方案。

> [!NOTE]
> 感谢人们审阅此系列并提供有价值的反馈： Rick Anderson、Levi Broderick、Barry Dorrans、Tom Dykstra、Hongmei Ge、David Matson、Daniel Roth、Tim Teebken。

## <a name="authentication"></a>身份验证

Web API 假定在主机中发生身份验证。 对于 web 承载，主机为 IIS，后者使用 HTTP 模块进行身份验证。 你可以将项目配置为使用在 IIS 或 ASP.NET 中内置的任何身份验证模块，或编写你自己的 HTTP 模块来执行自定义身份验证。

当主机对用户进行身份验证时，它将创建一个[IPrincipal](https://msdn.microsoft.com/library/System.Security.Principal.IPrincipal.aspx) *对象，该*对象表示运行代码的安全上下文。 宿主通过设置 **thread.currentprincipal**将主体附加到当前线程。 主体包含关联的 **标识** 对象，其中包含有关用户的信息。 如果对用户进行了身份验证，则 **IsAuthenticated** 属性返回 **true**。 对于匿名请求， **IsAuthenticated** 返回 **false**。 有关主体的详细信息，请参阅 [基于角色的安全性](https://msdn.microsoft.com/library/shz8h065.aspx)。

### <a name="http-message-handlers-for-authentication"></a>用于身份验证的 HTTP 消息处理程序

可以将身份验证逻辑放入 [HTTP 消息处理程序](../advanced/http-message-handlers.md)中，而不是使用主机进行身份验证。 在这种情况下，消息处理程序将检查 HTTP 请求并设置主体。

何时应使用消息处理程序进行身份验证？ 下面是一些折衷方案：

- HTTP 模块会查看所有经过 ASP.NET 管道的请求。 消息处理程序仅查看路由到 Web API 的请求。
- 你可以设置按路由消息处理程序，这使你可以将身份验证方案应用于特定路由。
- HTTP 模块是特定于 IIS 的。 消息处理程序是不可知的，因此它们可用于 web 托管和自承载。
- HTTP 模块参与 IIS 日志记录、审核等。
- HTTP 模块先前在管道中运行。 如果在消息处理程序中处理身份验证，则在处理程序运行之前，主体不会被设置。 此外，当响应离开消息处理程序时，主体恢复到以前的主体。

通常，如果不需要支持自承载，则 HTTP 模块是一个更好的选择。 如果需要支持自承载，请考虑使用消息处理程序。

### <a name="setting-the-principal"></a>设置主体

如果你的应用程序执行任何自定义身份验证逻辑，则必须在以下两个位置设置主体：

- **Thread.currentprincipal**。 此属性是在 .NET 中设置线程的主体的标准方法。
- **Httpcontext.current**。 此属性特定于 ASP.NET。

下面的代码演示如何设置主体：

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample1.cs)]

对于 web 承载，必须在这两个位置设置主体;否则，安全上下文可能会变得不一致。 但对于自承载， **HttpContext** 为 null。 因此，若要确保代码不可知，请在分配到 **HttpContext**之前检查 null，如下所示。

## <a name="authorization"></a>授权

稍后在管道中进行授权，越接近控制器。 这样，你可以在授予对资源的访问权限时进行更详细的选择。

- 在控制器操作之前运行*授权筛选器*。 如果请求未获授权，筛选器将返回错误响应，并且不会调用该操作。
- 在控制器操作中，可以从 **ApiController** 属性获取当前主体。 例如，你可以根据用户名筛选资源列表，仅返回属于该用户的资源。

![](authentication-and-authorization-in-aspnet-web-api/_static/image1.png)

<a id="auth3"></a>
### <a name="using-the-authorize-attribute"></a>使用 [授权] 特性

Web API 提供内置的授权筛选器 [AuthorizeAttribute](https://msdn.microsoft.com/library/system.web.http.authorizeattribute.aspx)。 此筛选器将检查是否对用户进行了身份验证。 否则，它将返回 HTTP 状态代码 401 (未经授权的) ，而不调用操作。

您可以在全局、控制器级别或单个操作级别应用筛选器。

**全局**：若要限制每个 Web API 控制器的访问，请将 **AuthorizeAttribute** 筛选器添加到全局筛选器列表中：

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample2.cs)]

**控制器**：若要限制对特定控制器的访问，请将筛选器作为属性添加到控制器：

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample3.cs)]

**操作**：若要限制对特定操作的访问，请将特性添加到操作方法中：

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample4.cs)]

或者，你可以使用属性来限制控制器，然后允许对特定操作进行匿名访问 `[AllowAnonymous]` 。 在下面的示例中， `Post` 方法是受限的，但 `Get` 方法允许匿名访问。

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample5.cs)]

在前面的示例中，筛选器允许任何经过身份验证的用户访问受限制的方法;仅匿名用户会被保留。你还可以将访问权限限制为特定用户或特定角色的用户：

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample6.cs)]

> [!NOTE]
> Web API 控制器的 **AuthorizeAttribute** 筛选器位于 **system.web** 命名空间中。 **System.web**命名空间中的 MVC 控制器的筛选器与 web API 控制器不兼容。

### <a name="custom-authorization-filters"></a>自定义授权筛选器

若要编写自定义授权筛选器，请从以下类型之一派生：

- **AuthorizeAttribute**。 扩展此类以根据当前用户和用户的角色执行授权逻辑。
- **AuthorizationFilterAttribute**。 扩展此类以执行不一定基于当前用户或角色的同步授权逻辑。
- **IAuthorizationFilter**。 实现此接口可执行异步授权逻辑;例如，如果授权逻辑发出异步 i/o 或网络调用。  (如果授权逻辑是 CPU 绑定的，则从 **AuthorizationFilterAttribute**派生更简单，因为这样就不需要编写异步方法。 ) 

下图显示了 **AuthorizeAttribute** 类的类层次结构。

![](authentication-and-authorization-in-aspnet-web-api/_static/image2.png)

### <a name="authorization-inside-a-controller-action"></a>控制器操作内的授权

在某些情况下，你可能会允许请求继续，但会根据主体更改行为。 例如，你返回的信息可能会根据用户的角色而发生更改。 在控制器方法中，可以从 **ApiController** 属性获取当前主体。

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample7.cs)]

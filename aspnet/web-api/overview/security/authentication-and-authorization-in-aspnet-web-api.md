---
uid: web-api/overview/security/authentication-and-authorization-in-aspnet-web-api
title: ASP.NET Web API 中的身份验证和授权 |微软文档
author: MikeWasson
description: 提供了ASP.NET Web API 中的身份验证和授权的概述。
ms.author: riande
ms.date: 11/27/2012
ms.assetid: 6dfb51ea-9f4d-4e70-916c-8ef8344a88d6
msc.legacyurl: /web-api/overview/security/authentication-and-authorization-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 368d2b9456d12b2bb4063a23333e5c8837faa3b8
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675861"
---
# <a name="authentication-and-authorization-in-aspnet-web-api"></a>Authentication and Authorization in ASP.NET Web API（ASP.NET Web API 中的身份验证和授权）

由[迈克·瓦森](https://github.com/MikeWasson)

您已经创建了 Web API，但现在要控制对它的访问。 在本系列文章中，我们将介绍一些保护 Web API 免受未经授权的用户访问的选项。 本系列将涵盖身份验证和授权。

- *身份验证*是知道用户的身份。 例如，Alice 使用用户名和密码登录，服务器使用密码对 Alice 进行身份验证。
- *授权*是决定是否允许用户执行操作。 例如，Alice 有权获取资源，但不能创建资源。

本系列的第一篇文章概述了ASP.NET Web API 中的身份验证和授权。 其他主题描述 Web API 的常见身份验证方案。

> [!NOTE]
> 感谢那些回顾这个系列并提供宝贵反馈的人：里克·安德森、利维·布罗德里克、巴里·多兰斯、汤姆·戴克斯特拉、葛红梅、大卫·马特森、丹尼尔·罗斯、蒂姆·蒂肯。

## <a name="authentication"></a>身份验证

Web API 假定身份验证发生在主机中。 对于 Web 托管，主机是 IIS，它使用 HTTP 模块进行身份验证。 您可以将项目配置为使用 IIS 或ASP.NET内置的任何身份验证模块，或者编写自己的 HTTP 模块以执行自定义身份验证。

当主机对用户进行身份验证时，它会创建一个*主体*，它是一个[IThe 对象](https://msdn.microsoft.com/library/System.Security.Principal.IPrincipal.aspx)，表示代码运行的安全上下文。 主机通过设置**Thread.Currentthe 将**主体附加到当前线程。 主体包含一个关联的**标识**对象，该对象包含有关用户的信息。 如果用户已过身份验证，**标识.Is 验证**属性将返回**true**。 对于匿名请求 **，已身份验证**返回**false**。 有关主体的详细信息，请参阅[基于角色的安全性](https://msdn.microsoft.com/library/shz8h065.aspx)。

### <a name="http-message-handlers-for-authentication"></a>用于身份验证的 HTTP 消息处理程序

您可以将身份验证逻辑放入[HTTP 消息处理程序](../advanced/http-message-handlers.md)中，而不是使用主机进行身份验证。 在这种情况下，消息处理程序检查 HTTP 请求并设置主体。

何时应该使用消息处理程序进行身份验证？ 以下是一些权衡：

- HTTP 模块看到通过ASP.NET管道的所有请求。 消息处理程序只看到路由到 Web API 的请求。
- 您可以设置每个路由的消息处理程序，这允许您将身份验证方案应用于特定路由。
- HTTP 模块特定于 IIS。 消息处理程序与主机无关，因此可以同时用于 Web 托管和自托管。
- HTTP 模块参与 IIS 日志记录、审核等。
- HTTP 模块在管道中运行较早。 如果在消息处理程序中处理身份验证，则在处理程序运行之前不会设置主体。 此外，当响应离开消息处理程序时，主体将还原到上一个主体。

通常，如果您不需要支持自托管，HTTP 模块是一个更好的选择。 如果需要支持自托管，请考虑消息处理程序。

### <a name="setting-the-principal"></a>设置主体

如果应用程序执行任何自定义身份验证逻辑，则必须在以下两个位置设置主体：

- **线程.电流主体**。 此属性是在 .NET 中设置线程主体的标准方法。
- **httpContext.当前.用户**。 此属性特定于ASP.NET。

以下代码演示如何设置主体：

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample1.cs)]

对于 Web 托管，必须在两个位置设置主体;否则，安全上下文可能会变得不一致。 但是，对于自托管 **，httpContext.current**为 null。 因此，为了确保代码与主机无关，请在分配给**HttpContext.Current**之前检查空。

## <a name="authorization"></a>授权

授权在管道中稍后发生，更接近控制器。 这样，在授予对资源的权限时，可以做出更精细的选择。

- *授权筛选器在*控制器操作之前运行。 如果请求未获授权，筛选器将返回错误响应，并且不会调用该操作。
- 在控制器操作中，可以从**ApiController.User**属性获取当前主体。 例如，您可以根据用户名筛选资源列表，仅返回属于该用户的资源。

![](authentication-and-authorization-in-aspnet-web-api/_static/image1.png)

<a id="auth3"></a>
### <a name="using-the-authorize-attribute"></a>使用 [授权] 属性

Web API 提供一个内置的授权筛选器，[授权属性](https://msdn.microsoft.com/library/system.web.http.authorizeattribute.aspx)。 此筛选器检查用户是否经过身份验证。 如果没有，它将返回 HTTP 状态代码 401（未授权），而不调用该操作。

您可以全局、控制器级别或单个操作级别应用筛选器。

**全局**：要限制每个 Web API 控制器的访问，将**授权属性**筛选器添加到全局筛选器列表中：

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample2.cs)]

**控制器**：要限制特定控制器的访问，将筛选器作为属性添加到控制器：

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample3.cs)]

**操作**：要限制特定操作的访问，将属性添加到操作方法：

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample4.cs)]

或者，您可以限制控制器，然后允许使用 属性`[AllowAnonymous]`匿名访问特定操作。 在下面的示例中，`Post`该方法受到限制，`Get`但该方法允许匿名访问。

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample5.cs)]

在前面的示例中，筛选器允许任何经过身份验证的用户访问受限制的方法;只有匿名用户被挡在外。您还可以限制对特定用户或特定角色的用户的访问：

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample6.cs)]

> [!NOTE]
> Web API 控制器的授权**属性**筛选器位于**System.Web.http**命名空间中。 **系统.Web.Mvc**命名空间中有 MVC 控制器的类似筛选器，该筛选器与 Web API 控制器不兼容。

### <a name="custom-authorization-filters"></a>自定义授权筛选器

要编写自定义授权筛选器，请派生自以下类型之一：

- **授权属性**. 扩展此类以基于当前用户和用户的角色执行授权逻辑。
- **授权筛选器属性**. 扩展此类以执行不一定基于当前用户或角色的同步授权逻辑。
- **I 授权筛选器**。 实现此接口以执行异步授权逻辑;例如，如果授权逻辑进行异步 I/O 或网络调用。 （如果授权逻辑是 CPU 绑定的，则从**授权筛选器属性**派生会更简单，因为则不需要编写异步方法。

下图显示了**授权属性**类的类层次结构。

![](authentication-and-authorization-in-aspnet-web-api/_static/image2.png)

### <a name="authorization-inside-a-controller-action"></a>控制器操作中的授权

在某些情况下，您可以允许请求继续，但基于主体更改行为。 例如，返回的信息可能会根据用户的角色而变化。 在控制器方法中，可以从**ApiController.User**属性获取当前主体。

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample7.cs)]

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
# <a name="authentication-and-authorization-in-aspnet-web-api"></a><span data-ttu-id="0b746-103">Authentication and Authorization in ASP.NET Web API（ASP.NET Web API 中的身份验证和授权）</span><span class="sxs-lookup"><span data-stu-id="0b746-103">Authentication and Authorization in ASP.NET Web API</span></span>

<span data-ttu-id="0b746-104">由[迈克·瓦森](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="0b746-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="0b746-105">您已经创建了 Web API，但现在要控制对它的访问。</span><span class="sxs-lookup"><span data-stu-id="0b746-105">You've created a web API, but now you want to control access to it.</span></span> <span data-ttu-id="0b746-106">在本系列文章中，我们将介绍一些保护 Web API 免受未经授权的用户访问的选项。</span><span class="sxs-lookup"><span data-stu-id="0b746-106">In this series of articles, we'll look at some options for securing a web API from unauthorized users.</span></span> <span data-ttu-id="0b746-107">本系列将涵盖身份验证和授权。</span><span class="sxs-lookup"><span data-stu-id="0b746-107">This series will cover both authentication and authorization.</span></span>

- <span data-ttu-id="0b746-108">*身份验证*是知道用户的身份。</span><span class="sxs-lookup"><span data-stu-id="0b746-108">*Authentication* is knowing the identity of the user.</span></span> <span data-ttu-id="0b746-109">例如，Alice 使用用户名和密码登录，服务器使用密码对 Alice 进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="0b746-109">For example, Alice logs in with her username and password, and the server uses the password to authenticate Alice.</span></span>
- <span data-ttu-id="0b746-110">*授权*是决定是否允许用户执行操作。</span><span class="sxs-lookup"><span data-stu-id="0b746-110">*Authorization* is deciding whether a user is allowed to perform an action.</span></span> <span data-ttu-id="0b746-111">例如，Alice 有权获取资源，但不能创建资源。</span><span class="sxs-lookup"><span data-stu-id="0b746-111">For example, Alice has permission to get a resource but not create a resource.</span></span>

<span data-ttu-id="0b746-112">本系列的第一篇文章概述了ASP.NET Web API 中的身份验证和授权。</span><span class="sxs-lookup"><span data-stu-id="0b746-112">The first article in the series gives a general overview of authentication and authorization in ASP.NET Web API.</span></span> <span data-ttu-id="0b746-113">其他主题描述 Web API 的常见身份验证方案。</span><span class="sxs-lookup"><span data-stu-id="0b746-113">Other topics describe common authentication scenarios for Web API.</span></span>

> [!NOTE]
> <span data-ttu-id="0b746-114">感谢那些回顾这个系列并提供宝贵反馈的人：里克·安德森、利维·布罗德里克、巴里·多兰斯、汤姆·戴克斯特拉、葛红梅、大卫·马特森、丹尼尔·罗斯、蒂姆·蒂肯。</span><span class="sxs-lookup"><span data-stu-id="0b746-114">Thanks to the people who reviewed this series and provided valuable feedback: Rick Anderson, Levi Broderick, Barry Dorrans, Tom Dykstra, Hongmei Ge, David Matson, Daniel Roth, Tim Teebken.</span></span>

## <a name="authentication"></a><span data-ttu-id="0b746-115">身份验证</span><span class="sxs-lookup"><span data-stu-id="0b746-115">Authentication</span></span>

<span data-ttu-id="0b746-116">Web API 假定身份验证发生在主机中。</span><span class="sxs-lookup"><span data-stu-id="0b746-116">Web API assumes that authentication happens in the host.</span></span> <span data-ttu-id="0b746-117">对于 Web 托管，主机是 IIS，它使用 HTTP 模块进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="0b746-117">For web-hosting, the host is IIS, which uses HTTP modules for authentication.</span></span> <span data-ttu-id="0b746-118">您可以将项目配置为使用 IIS 或ASP.NET内置的任何身份验证模块，或者编写自己的 HTTP 模块以执行自定义身份验证。</span><span class="sxs-lookup"><span data-stu-id="0b746-118">You can configure your project to use any of the authentication modules built in to IIS or ASP.NET, or write your own HTTP module to perform custom authentication.</span></span>

<span data-ttu-id="0b746-119">当主机对用户进行身份验证时，它会创建一个*主体*，它是一个[IThe 对象](https://msdn.microsoft.com/library/System.Security.Principal.IPrincipal.aspx)，表示代码运行的安全上下文。</span><span class="sxs-lookup"><span data-stu-id="0b746-119">When the host authenticates the user, it creates a *principal*, which is an [IPrincipal](https://msdn.microsoft.com/library/System.Security.Principal.IPrincipal.aspx) object that represents the security context under which code is running.</span></span> <span data-ttu-id="0b746-120">主机通过设置**Thread.Currentthe 将**主体附加到当前线程。</span><span class="sxs-lookup"><span data-stu-id="0b746-120">The host attaches the principal to the current thread by setting **Thread.CurrentPrincipal**.</span></span> <span data-ttu-id="0b746-121">主体包含一个关联的**标识**对象，该对象包含有关用户的信息。</span><span class="sxs-lookup"><span data-stu-id="0b746-121">The principal contains an associated **Identity** object that contains information about the user.</span></span> <span data-ttu-id="0b746-122">如果用户已过身份验证，**标识.Is 验证**属性将返回**true**。</span><span class="sxs-lookup"><span data-stu-id="0b746-122">If the user is authenticated, the **Identity.IsAuthenticated** property returns **true**.</span></span> <span data-ttu-id="0b746-123">对于匿名请求 **，已身份验证**返回**false**。</span><span class="sxs-lookup"><span data-stu-id="0b746-123">For anonymous requests, **IsAuthenticated** returns **false**.</span></span> <span data-ttu-id="0b746-124">有关主体的详细信息，请参阅[基于角色的安全性](https://msdn.microsoft.com/library/shz8h065.aspx)。</span><span class="sxs-lookup"><span data-stu-id="0b746-124">For more information about principals, see [Role-Based Security](https://msdn.microsoft.com/library/shz8h065.aspx).</span></span>

### <a name="http-message-handlers-for-authentication"></a><span data-ttu-id="0b746-125">用于身份验证的 HTTP 消息处理程序</span><span class="sxs-lookup"><span data-stu-id="0b746-125">HTTP Message Handlers for Authentication</span></span>

<span data-ttu-id="0b746-126">您可以将身份验证逻辑放入[HTTP 消息处理程序](../advanced/http-message-handlers.md)中，而不是使用主机进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="0b746-126">Instead of using the host for authentication, you can put authentication logic into an [HTTP message handler](../advanced/http-message-handlers.md).</span></span> <span data-ttu-id="0b746-127">在这种情况下，消息处理程序检查 HTTP 请求并设置主体。</span><span class="sxs-lookup"><span data-stu-id="0b746-127">In that case, the message handler examines the HTTP request and sets the principal.</span></span>

<span data-ttu-id="0b746-128">何时应该使用消息处理程序进行身份验证？</span><span class="sxs-lookup"><span data-stu-id="0b746-128">When should you use message handlers for authentication?</span></span> <span data-ttu-id="0b746-129">以下是一些权衡：</span><span class="sxs-lookup"><span data-stu-id="0b746-129">Here are some tradeoffs:</span></span>

- <span data-ttu-id="0b746-130">HTTP 模块看到通过ASP.NET管道的所有请求。</span><span class="sxs-lookup"><span data-stu-id="0b746-130">An HTTP module sees all requests that go through the ASP.NET pipeline.</span></span> <span data-ttu-id="0b746-131">消息处理程序只看到路由到 Web API 的请求。</span><span class="sxs-lookup"><span data-stu-id="0b746-131">A message handler only sees requests that are routed to Web API.</span></span>
- <span data-ttu-id="0b746-132">您可以设置每个路由的消息处理程序，这允许您将身份验证方案应用于特定路由。</span><span class="sxs-lookup"><span data-stu-id="0b746-132">You can set per-route message handlers, which lets you apply an authentication scheme to a specific route.</span></span>
- <span data-ttu-id="0b746-133">HTTP 模块特定于 IIS。</span><span class="sxs-lookup"><span data-stu-id="0b746-133">HTTP modules are specific to IIS.</span></span> <span data-ttu-id="0b746-134">消息处理程序与主机无关，因此可以同时用于 Web 托管和自托管。</span><span class="sxs-lookup"><span data-stu-id="0b746-134">Message handlers are host-agnostic, so they can be used with both web-hosting and self-hosting.</span></span>
- <span data-ttu-id="0b746-135">HTTP 模块参与 IIS 日志记录、审核等。</span><span class="sxs-lookup"><span data-stu-id="0b746-135">HTTP modules participate in IIS logging, auditing, and so on.</span></span>
- <span data-ttu-id="0b746-136">HTTP 模块在管道中运行较早。</span><span class="sxs-lookup"><span data-stu-id="0b746-136">HTTP modules run earlier in the pipeline.</span></span> <span data-ttu-id="0b746-137">如果在消息处理程序中处理身份验证，则在处理程序运行之前不会设置主体。</span><span class="sxs-lookup"><span data-stu-id="0b746-137">If you handle authentication in a message handler, the principal does not get set until the handler runs.</span></span> <span data-ttu-id="0b746-138">此外，当响应离开消息处理程序时，主体将还原到上一个主体。</span><span class="sxs-lookup"><span data-stu-id="0b746-138">Moreover, the principal reverts back to the previous principal when the response leaves the message handler.</span></span>

<span data-ttu-id="0b746-139">通常，如果您不需要支持自托管，HTTP 模块是一个更好的选择。</span><span class="sxs-lookup"><span data-stu-id="0b746-139">Generally, if you don't need to support self-hosting, an HTTP module is a better option.</span></span> <span data-ttu-id="0b746-140">如果需要支持自托管，请考虑消息处理程序。</span><span class="sxs-lookup"><span data-stu-id="0b746-140">If you need to support self-hosting, consider a message handler.</span></span>

### <a name="setting-the-principal"></a><span data-ttu-id="0b746-141">设置主体</span><span class="sxs-lookup"><span data-stu-id="0b746-141">Setting the Principal</span></span>

<span data-ttu-id="0b746-142">如果应用程序执行任何自定义身份验证逻辑，则必须在以下两个位置设置主体：</span><span class="sxs-lookup"><span data-stu-id="0b746-142">If your application performs any custom authentication logic, you must set the principal on two places:</span></span>

- <span data-ttu-id="0b746-143">**线程.电流主体**。</span><span class="sxs-lookup"><span data-stu-id="0b746-143">**Thread.CurrentPrincipal**.</span></span> <span data-ttu-id="0b746-144">此属性是在 .NET 中设置线程主体的标准方法。</span><span class="sxs-lookup"><span data-stu-id="0b746-144">This property is the standard way to set the thread's principal in .NET.</span></span>
- <span data-ttu-id="0b746-145">**httpContext.当前.用户**。</span><span class="sxs-lookup"><span data-stu-id="0b746-145">**HttpContext.Current.User**.</span></span> <span data-ttu-id="0b746-146">此属性特定于ASP.NET。</span><span class="sxs-lookup"><span data-stu-id="0b746-146">This property is specific to ASP.NET.</span></span>

<span data-ttu-id="0b746-147">以下代码演示如何设置主体：</span><span class="sxs-lookup"><span data-stu-id="0b746-147">The following code shows how to set the principal:</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample1.cs)]

<span data-ttu-id="0b746-148">对于 Web 托管，必须在两个位置设置主体;否则，安全上下文可能会变得不一致。</span><span class="sxs-lookup"><span data-stu-id="0b746-148">For web-hosting, you must set the principal in both places; otherwise the security context may become inconsistent.</span></span> <span data-ttu-id="0b746-149">但是，对于自托管 **，httpContext.current**为 null。</span><span class="sxs-lookup"><span data-stu-id="0b746-149">For self-hosting, however, **HttpContext.Current** is null.</span></span> <span data-ttu-id="0b746-150">因此，为了确保代码与主机无关，请在分配给**HttpContext.Current**之前检查空。</span><span class="sxs-lookup"><span data-stu-id="0b746-150">To ensure your code is host-agnostic, therefore, check for null before assigning to **HttpContext.Current**, as shown.</span></span>

## <a name="authorization"></a><span data-ttu-id="0b746-151">授权</span><span class="sxs-lookup"><span data-stu-id="0b746-151">Authorization</span></span>

<span data-ttu-id="0b746-152">授权在管道中稍后发生，更接近控制器。</span><span class="sxs-lookup"><span data-stu-id="0b746-152">Authorization happens later in the pipeline, closer to the controller.</span></span> <span data-ttu-id="0b746-153">这样，在授予对资源的权限时，可以做出更精细的选择。</span><span class="sxs-lookup"><span data-stu-id="0b746-153">That lets you make more granular choices when you grant access to resources.</span></span>

- <span data-ttu-id="0b746-154">*授权筛选器在*控制器操作之前运行。</span><span class="sxs-lookup"><span data-stu-id="0b746-154">*Authorization filters* run before the controller action.</span></span> <span data-ttu-id="0b746-155">如果请求未获授权，筛选器将返回错误响应，并且不会调用该操作。</span><span class="sxs-lookup"><span data-stu-id="0b746-155">If the request is not authorized, the filter returns an error response, and the action is not invoked.</span></span>
- <span data-ttu-id="0b746-156">在控制器操作中，可以从**ApiController.User**属性获取当前主体。</span><span class="sxs-lookup"><span data-stu-id="0b746-156">Within a controller action, you can get the current principal from the **ApiController.User** property.</span></span> <span data-ttu-id="0b746-157">例如，您可以根据用户名筛选资源列表，仅返回属于该用户的资源。</span><span class="sxs-lookup"><span data-stu-id="0b746-157">For example, you might filter a list of resources based on the user name, returning only those resources that belong to that user.</span></span>

![](authentication-and-authorization-in-aspnet-web-api/_static/image1.png)

<a id="auth3"></a>
### <a name="using-the-authorize-attribute"></a><span data-ttu-id="0b746-158">使用 [授权] 属性</span><span class="sxs-lookup"><span data-stu-id="0b746-158">Using the [Authorize] Attribute</span></span>

<span data-ttu-id="0b746-159">Web API 提供一个内置的授权筛选器，[授权属性](https://msdn.microsoft.com/library/system.web.http.authorizeattribute.aspx)。</span><span class="sxs-lookup"><span data-stu-id="0b746-159">Web API provides a built-in authorization filter, [AuthorizeAttribute](https://msdn.microsoft.com/library/system.web.http.authorizeattribute.aspx).</span></span> <span data-ttu-id="0b746-160">此筛选器检查用户是否经过身份验证。</span><span class="sxs-lookup"><span data-stu-id="0b746-160">This filter checks whether the user is authenticated.</span></span> <span data-ttu-id="0b746-161">如果没有，它将返回 HTTP 状态代码 401（未授权），而不调用该操作。</span><span class="sxs-lookup"><span data-stu-id="0b746-161">If not, it returns HTTP status code 401 (Unauthorized), without invoking the action.</span></span>

<span data-ttu-id="0b746-162">您可以全局、控制器级别或单个操作级别应用筛选器。</span><span class="sxs-lookup"><span data-stu-id="0b746-162">You can apply the filter globally, at the controller level, or at the level of individual actions.</span></span>

<span data-ttu-id="0b746-163">**全局**：要限制每个 Web API 控制器的访问，将**授权属性**筛选器添加到全局筛选器列表中：</span><span class="sxs-lookup"><span data-stu-id="0b746-163">**Globally**: To restrict access for every Web API controller, add the **AuthorizeAttribute** filter to the global filter list:</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample2.cs)]

<span data-ttu-id="0b746-164">**控制器**：要限制特定控制器的访问，将筛选器作为属性添加到控制器：</span><span class="sxs-lookup"><span data-stu-id="0b746-164">**Controller**: To restrict access for a specific controller, add the filter as an attribute to the controller:</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample3.cs)]

<span data-ttu-id="0b746-165">**操作**：要限制特定操作的访问，将属性添加到操作方法：</span><span class="sxs-lookup"><span data-stu-id="0b746-165">**Action**: To restrict access for specific actions, add the attribute to the action method:</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample4.cs)]

<span data-ttu-id="0b746-166">或者，您可以限制控制器，然后允许使用 属性`[AllowAnonymous]`匿名访问特定操作。</span><span class="sxs-lookup"><span data-stu-id="0b746-166">Alternatively, you can restrict the controller and then allow anonymous access to specific actions, by using the `[AllowAnonymous]` attribute.</span></span> <span data-ttu-id="0b746-167">在下面的示例中，`Post`该方法受到限制，`Get`但该方法允许匿名访问。</span><span class="sxs-lookup"><span data-stu-id="0b746-167">In the following example, the `Post` method is restricted, but the `Get` method allows anonymous access.</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample5.cs)]

<span data-ttu-id="0b746-168">在前面的示例中，筛选器允许任何经过身份验证的用户访问受限制的方法;只有匿名用户被挡在外。您还可以限制对特定用户或特定角色的用户的访问：</span><span class="sxs-lookup"><span data-stu-id="0b746-168">In the previous examples, the filter allows any authenticated user to access the restricted methods; only anonymous users are kept out. You can also limit access to specific users or to users in specific roles:</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample6.cs)]

> [!NOTE]
> <span data-ttu-id="0b746-169">Web API 控制器的授权**属性**筛选器位于**System.Web.http**命名空间中。</span><span class="sxs-lookup"><span data-stu-id="0b746-169">The **AuthorizeAttribute** filter for Web API controllers is located in the **System.Web.Http** namespace.</span></span> <span data-ttu-id="0b746-170">**系统.Web.Mvc**命名空间中有 MVC 控制器的类似筛选器，该筛选器与 Web API 控制器不兼容。</span><span class="sxs-lookup"><span data-stu-id="0b746-170">There is a similar filter for MVC controllers in the **System.Web.Mvc** namespace, which is not compatible with Web API controllers.</span></span>

### <a name="custom-authorization-filters"></a><span data-ttu-id="0b746-171">自定义授权筛选器</span><span class="sxs-lookup"><span data-stu-id="0b746-171">Custom Authorization Filters</span></span>

<span data-ttu-id="0b746-172">要编写自定义授权筛选器，请派生自以下类型之一：</span><span class="sxs-lookup"><span data-stu-id="0b746-172">To write a custom authorization filter, derive from one of these types:</span></span>

- <span data-ttu-id="0b746-173">**授权属性**.</span><span class="sxs-lookup"><span data-stu-id="0b746-173">**AuthorizeAttribute**.</span></span> <span data-ttu-id="0b746-174">扩展此类以基于当前用户和用户的角色执行授权逻辑。</span><span class="sxs-lookup"><span data-stu-id="0b746-174">Extend this class to perform authorization logic based on the current user and the user's roles.</span></span>
- <span data-ttu-id="0b746-175">**授权筛选器属性**.</span><span class="sxs-lookup"><span data-stu-id="0b746-175">**AuthorizationFilterAttribute**.</span></span> <span data-ttu-id="0b746-176">扩展此类以执行不一定基于当前用户或角色的同步授权逻辑。</span><span class="sxs-lookup"><span data-stu-id="0b746-176">Extend this class to perform synchronous authorization logic that is not necessarily based on the current user or role.</span></span>
- <span data-ttu-id="0b746-177">**I 授权筛选器**。</span><span class="sxs-lookup"><span data-stu-id="0b746-177">**IAuthorizationFilter**.</span></span> <span data-ttu-id="0b746-178">实现此接口以执行异步授权逻辑;例如，如果授权逻辑进行异步 I/O 或网络调用。</span><span class="sxs-lookup"><span data-stu-id="0b746-178">Implement this interface to perform asynchronous authorization logic; for example, if your authorization logic makes asynchronous I/O or network calls.</span></span> <span data-ttu-id="0b746-179">（如果授权逻辑是 CPU 绑定的，则从**授权筛选器属性**派生会更简单，因为则不需要编写异步方法。</span><span class="sxs-lookup"><span data-stu-id="0b746-179">(If your authorization logic is CPU-bound, it is simpler to derive from **AuthorizationFilterAttribute**, because then you don't need to write an asynchronous method.)</span></span>

<span data-ttu-id="0b746-180">下图显示了**授权属性**类的类层次结构。</span><span class="sxs-lookup"><span data-stu-id="0b746-180">The following diagram shows the class hierarchy for the **AuthorizeAttribute** class.</span></span>

![](authentication-and-authorization-in-aspnet-web-api/_static/image2.png)

### <a name="authorization-inside-a-controller-action"></a><span data-ttu-id="0b746-181">控制器操作中的授权</span><span class="sxs-lookup"><span data-stu-id="0b746-181">Authorization Inside a Controller Action</span></span>

<span data-ttu-id="0b746-182">在某些情况下，您可以允许请求继续，但基于主体更改行为。</span><span class="sxs-lookup"><span data-stu-id="0b746-182">In some cases, you might allow a request to proceed, but change the behavior based on the principal.</span></span> <span data-ttu-id="0b746-183">例如，返回的信息可能会根据用户的角色而变化。</span><span class="sxs-lookup"><span data-stu-id="0b746-183">For example, the information that you return might change depending on the user's role.</span></span> <span data-ttu-id="0b746-184">在控制器方法中，可以从**ApiController.User**属性获取当前主体。</span><span class="sxs-lookup"><span data-stu-id="0b746-184">Within a controller method, you can get the current principal from the **ApiController.User** property.</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample7.cs)]

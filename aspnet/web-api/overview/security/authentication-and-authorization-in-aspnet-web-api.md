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
# <a name="authentication-and-authorization-in-aspnet-web-api"></a><span data-ttu-id="e63ea-103">Authentication and Authorization in ASP.NET Web API（ASP.NET Web API 中的身份验证和授权）</span><span class="sxs-lookup"><span data-stu-id="e63ea-103">Authentication and Authorization in ASP.NET Web API</span></span>

<span data-ttu-id="e63ea-104">作者： [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="e63ea-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="e63ea-105">你已经创建了一个 web API，但现在想要控制对它的访问。</span><span class="sxs-lookup"><span data-stu-id="e63ea-105">You've created a web API, but now you want to control access to it.</span></span> <span data-ttu-id="e63ea-106">在这一系列的文章中，我们将介绍一些用于保护 web API 不受未经授权的用户使用的选项。</span><span class="sxs-lookup"><span data-stu-id="e63ea-106">In this series of articles, we'll look at some options for securing a web API from unauthorized users.</span></span> <span data-ttu-id="e63ea-107">此系列涵盖身份验证和授权。</span><span class="sxs-lookup"><span data-stu-id="e63ea-107">This series will cover both authentication and authorization.</span></span>

- <span data-ttu-id="e63ea-108">*身份验证* 知道用户的身份。</span><span class="sxs-lookup"><span data-stu-id="e63ea-108">*Authentication* is knowing the identity of the user.</span></span> <span data-ttu-id="e63ea-109">例如，Alice 使用用户名和密码登录，并且服务器使用密码对 Alice 进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="e63ea-109">For example, Alice logs in with her username and password, and the server uses the password to authenticate Alice.</span></span>
- <span data-ttu-id="e63ea-110">*授权* 是指是否允许用户执行某个操作。</span><span class="sxs-lookup"><span data-stu-id="e63ea-110">*Authorization* is deciding whether a user is allowed to perform an action.</span></span> <span data-ttu-id="e63ea-111">例如，Alice 有权获取资源，但不能创建资源。</span><span class="sxs-lookup"><span data-stu-id="e63ea-111">For example, Alice has permission to get a resource but not create a resource.</span></span>

<span data-ttu-id="e63ea-112">本系列文章中的第一篇文章概括介绍了 ASP.NET Web API 中的身份验证和授权。</span><span class="sxs-lookup"><span data-stu-id="e63ea-112">The first article in the series gives a general overview of authentication and authorization in ASP.NET Web API.</span></span> <span data-ttu-id="e63ea-113">其他主题介绍了 Web API 的常见身份验证方案。</span><span class="sxs-lookup"><span data-stu-id="e63ea-113">Other topics describe common authentication scenarios for Web API.</span></span>

> [!NOTE]
> <span data-ttu-id="e63ea-114">感谢人们审阅此系列并提供有价值的反馈： Rick Anderson、Levi Broderick、Barry Dorrans、Tom Dykstra、Hongmei Ge、David Matson、Daniel Roth、Tim Teebken。</span><span class="sxs-lookup"><span data-stu-id="e63ea-114">Thanks to the people who reviewed this series and provided valuable feedback: Rick Anderson, Levi Broderick, Barry Dorrans, Tom Dykstra, Hongmei Ge, David Matson, Daniel Roth, Tim Teebken.</span></span>

## <a name="authentication"></a><span data-ttu-id="e63ea-115">身份验证</span><span class="sxs-lookup"><span data-stu-id="e63ea-115">Authentication</span></span>

<span data-ttu-id="e63ea-116">Web API 假定在主机中发生身份验证。</span><span class="sxs-lookup"><span data-stu-id="e63ea-116">Web API assumes that authentication happens in the host.</span></span> <span data-ttu-id="e63ea-117">对于 web 承载，主机为 IIS，后者使用 HTTP 模块进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="e63ea-117">For web-hosting, the host is IIS, which uses HTTP modules for authentication.</span></span> <span data-ttu-id="e63ea-118">你可以将项目配置为使用在 IIS 或 ASP.NET 中内置的任何身份验证模块，或编写你自己的 HTTP 模块来执行自定义身份验证。</span><span class="sxs-lookup"><span data-stu-id="e63ea-118">You can configure your project to use any of the authentication modules built in to IIS or ASP.NET, or write your own HTTP module to perform custom authentication.</span></span>

<span data-ttu-id="e63ea-119">当主机对用户进行身份验证时，它将创建一个[IPrincipal](https://msdn.microsoft.com/library/System.Security.Principal.IPrincipal.aspx) *对象，该*对象表示运行代码的安全上下文。</span><span class="sxs-lookup"><span data-stu-id="e63ea-119">When the host authenticates the user, it creates a *principal*, which is an [IPrincipal](https://msdn.microsoft.com/library/System.Security.Principal.IPrincipal.aspx) object that represents the security context under which code is running.</span></span> <span data-ttu-id="e63ea-120">宿主通过设置 **thread.currentprincipal**将主体附加到当前线程。</span><span class="sxs-lookup"><span data-stu-id="e63ea-120">The host attaches the principal to the current thread by setting **Thread.CurrentPrincipal**.</span></span> <span data-ttu-id="e63ea-121">主体包含关联的 **标识** 对象，其中包含有关用户的信息。</span><span class="sxs-lookup"><span data-stu-id="e63ea-121">The principal contains an associated **Identity** object that contains information about the user.</span></span> <span data-ttu-id="e63ea-122">如果对用户进行了身份验证，则 **IsAuthenticated** 属性返回 **true**。</span><span class="sxs-lookup"><span data-stu-id="e63ea-122">If the user is authenticated, the **Identity.IsAuthenticated** property returns **true**.</span></span> <span data-ttu-id="e63ea-123">对于匿名请求， **IsAuthenticated** 返回 **false**。</span><span class="sxs-lookup"><span data-stu-id="e63ea-123">For anonymous requests, **IsAuthenticated** returns **false**.</span></span> <span data-ttu-id="e63ea-124">有关主体的详细信息，请参阅 [基于角色的安全性](https://msdn.microsoft.com/library/shz8h065.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e63ea-124">For more information about principals, see [Role-Based Security](https://msdn.microsoft.com/library/shz8h065.aspx).</span></span>

### <a name="http-message-handlers-for-authentication"></a><span data-ttu-id="e63ea-125">用于身份验证的 HTTP 消息处理程序</span><span class="sxs-lookup"><span data-stu-id="e63ea-125">HTTP Message Handlers for Authentication</span></span>

<span data-ttu-id="e63ea-126">可以将身份验证逻辑放入 [HTTP 消息处理程序](../advanced/http-message-handlers.md)中，而不是使用主机进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="e63ea-126">Instead of using the host for authentication, you can put authentication logic into an [HTTP message handler](../advanced/http-message-handlers.md).</span></span> <span data-ttu-id="e63ea-127">在这种情况下，消息处理程序将检查 HTTP 请求并设置主体。</span><span class="sxs-lookup"><span data-stu-id="e63ea-127">In that case, the message handler examines the HTTP request and sets the principal.</span></span>

<span data-ttu-id="e63ea-128">何时应使用消息处理程序进行身份验证？</span><span class="sxs-lookup"><span data-stu-id="e63ea-128">When should you use message handlers for authentication?</span></span> <span data-ttu-id="e63ea-129">下面是一些折衷方案：</span><span class="sxs-lookup"><span data-stu-id="e63ea-129">Here are some tradeoffs:</span></span>

- <span data-ttu-id="e63ea-130">HTTP 模块会查看所有经过 ASP.NET 管道的请求。</span><span class="sxs-lookup"><span data-stu-id="e63ea-130">An HTTP module sees all requests that go through the ASP.NET pipeline.</span></span> <span data-ttu-id="e63ea-131">消息处理程序仅查看路由到 Web API 的请求。</span><span class="sxs-lookup"><span data-stu-id="e63ea-131">A message handler only sees requests that are routed to Web API.</span></span>
- <span data-ttu-id="e63ea-132">你可以设置按路由消息处理程序，这使你可以将身份验证方案应用于特定路由。</span><span class="sxs-lookup"><span data-stu-id="e63ea-132">You can set per-route message handlers, which lets you apply an authentication scheme to a specific route.</span></span>
- <span data-ttu-id="e63ea-133">HTTP 模块是特定于 IIS 的。</span><span class="sxs-lookup"><span data-stu-id="e63ea-133">HTTP modules are specific to IIS.</span></span> <span data-ttu-id="e63ea-134">消息处理程序是不可知的，因此它们可用于 web 托管和自承载。</span><span class="sxs-lookup"><span data-stu-id="e63ea-134">Message handlers are host-agnostic, so they can be used with both web-hosting and self-hosting.</span></span>
- <span data-ttu-id="e63ea-135">HTTP 模块参与 IIS 日志记录、审核等。</span><span class="sxs-lookup"><span data-stu-id="e63ea-135">HTTP modules participate in IIS logging, auditing, and so on.</span></span>
- <span data-ttu-id="e63ea-136">HTTP 模块先前在管道中运行。</span><span class="sxs-lookup"><span data-stu-id="e63ea-136">HTTP modules run earlier in the pipeline.</span></span> <span data-ttu-id="e63ea-137">如果在消息处理程序中处理身份验证，则在处理程序运行之前，主体不会被设置。</span><span class="sxs-lookup"><span data-stu-id="e63ea-137">If you handle authentication in a message handler, the principal does not get set until the handler runs.</span></span> <span data-ttu-id="e63ea-138">此外，当响应离开消息处理程序时，主体恢复到以前的主体。</span><span class="sxs-lookup"><span data-stu-id="e63ea-138">Moreover, the principal reverts back to the previous principal when the response leaves the message handler.</span></span>

<span data-ttu-id="e63ea-139">通常，如果不需要支持自承载，则 HTTP 模块是一个更好的选择。</span><span class="sxs-lookup"><span data-stu-id="e63ea-139">Generally, if you don't need to support self-hosting, an HTTP module is a better option.</span></span> <span data-ttu-id="e63ea-140">如果需要支持自承载，请考虑使用消息处理程序。</span><span class="sxs-lookup"><span data-stu-id="e63ea-140">If you need to support self-hosting, consider a message handler.</span></span>

### <a name="setting-the-principal"></a><span data-ttu-id="e63ea-141">设置主体</span><span class="sxs-lookup"><span data-stu-id="e63ea-141">Setting the Principal</span></span>

<span data-ttu-id="e63ea-142">如果你的应用程序执行任何自定义身份验证逻辑，则必须在以下两个位置设置主体：</span><span class="sxs-lookup"><span data-stu-id="e63ea-142">If your application performs any custom authentication logic, you must set the principal on two places:</span></span>

- <span data-ttu-id="e63ea-143">**Thread.currentprincipal**。</span><span class="sxs-lookup"><span data-stu-id="e63ea-143">**Thread.CurrentPrincipal**.</span></span> <span data-ttu-id="e63ea-144">此属性是在 .NET 中设置线程的主体的标准方法。</span><span class="sxs-lookup"><span data-stu-id="e63ea-144">This property is the standard way to set the thread's principal in .NET.</span></span>
- <span data-ttu-id="e63ea-145">**Httpcontext.current**。</span><span class="sxs-lookup"><span data-stu-id="e63ea-145">**HttpContext.Current.User**.</span></span> <span data-ttu-id="e63ea-146">此属性特定于 ASP.NET。</span><span class="sxs-lookup"><span data-stu-id="e63ea-146">This property is specific to ASP.NET.</span></span>

<span data-ttu-id="e63ea-147">下面的代码演示如何设置主体：</span><span class="sxs-lookup"><span data-stu-id="e63ea-147">The following code shows how to set the principal:</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample1.cs)]

<span data-ttu-id="e63ea-148">对于 web 承载，必须在这两个位置设置主体;否则，安全上下文可能会变得不一致。</span><span class="sxs-lookup"><span data-stu-id="e63ea-148">For web-hosting, you must set the principal in both places; otherwise the security context may become inconsistent.</span></span> <span data-ttu-id="e63ea-149">但对于自承载， **HttpContext** 为 null。</span><span class="sxs-lookup"><span data-stu-id="e63ea-149">For self-hosting, however, **HttpContext.Current** is null.</span></span> <span data-ttu-id="e63ea-150">因此，若要确保代码不可知，请在分配到 **HttpContext**之前检查 null，如下所示。</span><span class="sxs-lookup"><span data-stu-id="e63ea-150">To ensure your code is host-agnostic, therefore, check for null before assigning to **HttpContext.Current**, as shown.</span></span>

## <a name="authorization"></a><span data-ttu-id="e63ea-151">授权</span><span class="sxs-lookup"><span data-stu-id="e63ea-151">Authorization</span></span>

<span data-ttu-id="e63ea-152">稍后在管道中进行授权，越接近控制器。</span><span class="sxs-lookup"><span data-stu-id="e63ea-152">Authorization happens later in the pipeline, closer to the controller.</span></span> <span data-ttu-id="e63ea-153">这样，你可以在授予对资源的访问权限时进行更详细的选择。</span><span class="sxs-lookup"><span data-stu-id="e63ea-153">That lets you make more granular choices when you grant access to resources.</span></span>

- <span data-ttu-id="e63ea-154">在控制器操作之前运行*授权筛选器*。</span><span class="sxs-lookup"><span data-stu-id="e63ea-154">*Authorization filters* run before the controller action.</span></span> <span data-ttu-id="e63ea-155">如果请求未获授权，筛选器将返回错误响应，并且不会调用该操作。</span><span class="sxs-lookup"><span data-stu-id="e63ea-155">If the request is not authorized, the filter returns an error response, and the action is not invoked.</span></span>
- <span data-ttu-id="e63ea-156">在控制器操作中，可以从 **ApiController** 属性获取当前主体。</span><span class="sxs-lookup"><span data-stu-id="e63ea-156">Within a controller action, you can get the current principal from the **ApiController.User** property.</span></span> <span data-ttu-id="e63ea-157">例如，你可以根据用户名筛选资源列表，仅返回属于该用户的资源。</span><span class="sxs-lookup"><span data-stu-id="e63ea-157">For example, you might filter a list of resources based on the user name, returning only those resources that belong to that user.</span></span>

![](authentication-and-authorization-in-aspnet-web-api/_static/image1.png)

<a id="auth3"></a>
### <a name="using-the-authorize-attribute"></a><span data-ttu-id="e63ea-158">使用 [授权] 特性</span><span class="sxs-lookup"><span data-stu-id="e63ea-158">Using the [Authorize] Attribute</span></span>

<span data-ttu-id="e63ea-159">Web API 提供内置的授权筛选器 [AuthorizeAttribute](https://msdn.microsoft.com/library/system.web.http.authorizeattribute.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e63ea-159">Web API provides a built-in authorization filter, [AuthorizeAttribute](https://msdn.microsoft.com/library/system.web.http.authorizeattribute.aspx).</span></span> <span data-ttu-id="e63ea-160">此筛选器将检查是否对用户进行了身份验证。</span><span class="sxs-lookup"><span data-stu-id="e63ea-160">This filter checks whether the user is authenticated.</span></span> <span data-ttu-id="e63ea-161">否则，它将返回 HTTP 状态代码 401 (未经授权的) ，而不调用操作。</span><span class="sxs-lookup"><span data-stu-id="e63ea-161">If not, it returns HTTP status code 401 (Unauthorized), without invoking the action.</span></span>

<span data-ttu-id="e63ea-162">您可以在全局、控制器级别或单个操作级别应用筛选器。</span><span class="sxs-lookup"><span data-stu-id="e63ea-162">You can apply the filter globally, at the controller level, or at the level of individual actions.</span></span>

<span data-ttu-id="e63ea-163">**全局**：若要限制每个 Web API 控制器的访问，请将 **AuthorizeAttribute** 筛选器添加到全局筛选器列表中：</span><span class="sxs-lookup"><span data-stu-id="e63ea-163">**Globally**: To restrict access for every Web API controller, add the **AuthorizeAttribute** filter to the global filter list:</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample2.cs)]

<span data-ttu-id="e63ea-164">**控制器**：若要限制对特定控制器的访问，请将筛选器作为属性添加到控制器：</span><span class="sxs-lookup"><span data-stu-id="e63ea-164">**Controller**: To restrict access for a specific controller, add the filter as an attribute to the controller:</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample3.cs)]

<span data-ttu-id="e63ea-165">**操作**：若要限制对特定操作的访问，请将特性添加到操作方法中：</span><span class="sxs-lookup"><span data-stu-id="e63ea-165">**Action**: To restrict access for specific actions, add the attribute to the action method:</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample4.cs)]

<span data-ttu-id="e63ea-166">或者，你可以使用属性来限制控制器，然后允许对特定操作进行匿名访问 `[AllowAnonymous]` 。</span><span class="sxs-lookup"><span data-stu-id="e63ea-166">Alternatively, you can restrict the controller and then allow anonymous access to specific actions, by using the `[AllowAnonymous]` attribute.</span></span> <span data-ttu-id="e63ea-167">在下面的示例中， `Post` 方法是受限的，但 `Get` 方法允许匿名访问。</span><span class="sxs-lookup"><span data-stu-id="e63ea-167">In the following example, the `Post` method is restricted, but the `Get` method allows anonymous access.</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample5.cs)]

<span data-ttu-id="e63ea-168">在前面的示例中，筛选器允许任何经过身份验证的用户访问受限制的方法;仅匿名用户会被保留。你还可以将访问权限限制为特定用户或特定角色的用户：</span><span class="sxs-lookup"><span data-stu-id="e63ea-168">In the previous examples, the filter allows any authenticated user to access the restricted methods; only anonymous users are kept out. You can also limit access to specific users or to users in specific roles:</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample6.cs)]

> [!NOTE]
> <span data-ttu-id="e63ea-169">Web API 控制器的 **AuthorizeAttribute** 筛选器位于 **system.web** 命名空间中。</span><span class="sxs-lookup"><span data-stu-id="e63ea-169">The **AuthorizeAttribute** filter for Web API controllers is located in the **System.Web.Http** namespace.</span></span> <span data-ttu-id="e63ea-170">**System.web**命名空间中的 MVC 控制器的筛选器与 web API 控制器不兼容。</span><span class="sxs-lookup"><span data-stu-id="e63ea-170">There is a similar filter for MVC controllers in the **System.Web.Mvc** namespace, which is not compatible with Web API controllers.</span></span>

### <a name="custom-authorization-filters"></a><span data-ttu-id="e63ea-171">自定义授权筛选器</span><span class="sxs-lookup"><span data-stu-id="e63ea-171">Custom Authorization Filters</span></span>

<span data-ttu-id="e63ea-172">若要编写自定义授权筛选器，请从以下类型之一派生：</span><span class="sxs-lookup"><span data-stu-id="e63ea-172">To write a custom authorization filter, derive from one of these types:</span></span>

- <span data-ttu-id="e63ea-173">**AuthorizeAttribute**。</span><span class="sxs-lookup"><span data-stu-id="e63ea-173">**AuthorizeAttribute**.</span></span> <span data-ttu-id="e63ea-174">扩展此类以根据当前用户和用户的角色执行授权逻辑。</span><span class="sxs-lookup"><span data-stu-id="e63ea-174">Extend this class to perform authorization logic based on the current user and the user's roles.</span></span>
- <span data-ttu-id="e63ea-175">**AuthorizationFilterAttribute**。</span><span class="sxs-lookup"><span data-stu-id="e63ea-175">**AuthorizationFilterAttribute**.</span></span> <span data-ttu-id="e63ea-176">扩展此类以执行不一定基于当前用户或角色的同步授权逻辑。</span><span class="sxs-lookup"><span data-stu-id="e63ea-176">Extend this class to perform synchronous authorization logic that is not necessarily based on the current user or role.</span></span>
- <span data-ttu-id="e63ea-177">**IAuthorizationFilter**。</span><span class="sxs-lookup"><span data-stu-id="e63ea-177">**IAuthorizationFilter**.</span></span> <span data-ttu-id="e63ea-178">实现此接口可执行异步授权逻辑;例如，如果授权逻辑发出异步 i/o 或网络调用。</span><span class="sxs-lookup"><span data-stu-id="e63ea-178">Implement this interface to perform asynchronous authorization logic; for example, if your authorization logic makes asynchronous I/O or network calls.</span></span> <span data-ttu-id="e63ea-179"> (如果授权逻辑是 CPU 绑定的，则从 **AuthorizationFilterAttribute**派生更简单，因为这样就不需要编写异步方法。 ) </span><span class="sxs-lookup"><span data-stu-id="e63ea-179">(If your authorization logic is CPU-bound, it is simpler to derive from **AuthorizationFilterAttribute**, because then you don't need to write an asynchronous method.)</span></span>

<span data-ttu-id="e63ea-180">下图显示了 **AuthorizeAttribute** 类的类层次结构。</span><span class="sxs-lookup"><span data-stu-id="e63ea-180">The following diagram shows the class hierarchy for the **AuthorizeAttribute** class.</span></span>

![](authentication-and-authorization-in-aspnet-web-api/_static/image2.png)

### <a name="authorization-inside-a-controller-action"></a><span data-ttu-id="e63ea-181">控制器操作内的授权</span><span class="sxs-lookup"><span data-stu-id="e63ea-181">Authorization Inside a Controller Action</span></span>

<span data-ttu-id="e63ea-182">在某些情况下，你可能会允许请求继续，但会根据主体更改行为。</span><span class="sxs-lookup"><span data-stu-id="e63ea-182">In some cases, you might allow a request to proceed, but change the behavior based on the principal.</span></span> <span data-ttu-id="e63ea-183">例如，你返回的信息可能会根据用户的角色而发生更改。</span><span class="sxs-lookup"><span data-stu-id="e63ea-183">For example, the information that you return might change depending on the user's role.</span></span> <span data-ttu-id="e63ea-184">在控制器方法中，可以从 **ApiController** 属性获取当前主体。</span><span class="sxs-lookup"><span data-stu-id="e63ea-184">Within a controller method, you can get the current principal from the **ApiController.User** property.</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample7.cs)]

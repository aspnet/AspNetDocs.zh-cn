---
uid: web-api/overview/security/authentication-filters
title: ASP.NET Web API 2 中的身份验证筛选器 |Microsoft Docs
author: MikeWasson
description: 身份验证筛选器是 HTTP 请求进行身份验证的组件。 Web API 2 和 MVC 5 都支持身份验证筛选器，但它们略有不同...
ms.author: riande
ms.date: 09/25/2014
ms.assetid: b9882e53-b3ca-4def-89b0-322846973ccb
msc.legacyurl: /web-api/overview/security/authentication-filters
msc.type: authoredcontent
ms.openlocfilehash: 22178890e8a5d481a80e5efdd37d3e43f1a30955
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/09/2019
ms.locfileid: "59406036"
---
# <a name="authentication-filters-in-aspnet-web-api-2"></a><span data-ttu-id="ec74f-104">ASP.NET Web API 2 中的身份验证筛选器</span><span class="sxs-lookup"><span data-stu-id="ec74f-104">Authentication Filters in ASP.NET Web API 2</span></span>

<span data-ttu-id="ec74f-105">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="ec74f-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="ec74f-106">身份验证筛选器是 HTTP 请求进行身份验证的组件。</span><span class="sxs-lookup"><span data-stu-id="ec74f-106">An authentication filter is a component that authenticates an HTTP request.</span></span> <span data-ttu-id="ec74f-107">Web API 2 和 MVC 5 都支持身份验证筛选器，但它们略有不同，主要是在筛选器接口的命名约定。</span><span class="sxs-lookup"><span data-stu-id="ec74f-107">Web API 2 and MVC 5 both support authentication filters, but they differ slightly, mostly in the naming conventions for the filter interface.</span></span> <span data-ttu-id="ec74f-108">本主题介绍 Web API 身份验证筛选器。</span><span class="sxs-lookup"><span data-stu-id="ec74f-108">This topic describes Web API authentication filters.</span></span>


<span data-ttu-id="ec74f-109">身份验证筛选器，可以为各个控制器或操作设置身份验证方案。</span><span class="sxs-lookup"><span data-stu-id="ec74f-109">Authentication filters let you set an authentication scheme for individual controllers or actions.</span></span> <span data-ttu-id="ec74f-110">这样一来，您的应用程序可以支持为不同的 HTTP 资源不同的身份验证机制。</span><span class="sxs-lookup"><span data-stu-id="ec74f-110">That way, your app can support different authentication mechanisms for different HTTP resources.</span></span>

<span data-ttu-id="ec74f-111">在本文中，我将介绍中的代码[基本身份验证](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/BasicAuthentication/ReadMe.txt)上的示例[ http://aspnet.codeplex.com ](http://aspnet.codeplex.com)。</span><span class="sxs-lookup"><span data-stu-id="ec74f-111">In this article, I'll show code from the [Basic Authentication](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/BasicAuthentication/ReadMe.txt) sample on [http://aspnet.codeplex.com](http://aspnet.codeplex.com).</span></span> <span data-ttu-id="ec74f-112">此示例演示实现 HTTP 基本访问身份验证方案 (RFC 2617) 的身份验证筛选器。</span><span class="sxs-lookup"><span data-stu-id="ec74f-112">The sample shows an authentication filter that implements the HTTP Basic Access Authentication scheme (RFC 2617).</span></span> <span data-ttu-id="ec74f-113">在名为的类中实现筛选器`IdentityBasicAuthenticationAttribute`。</span><span class="sxs-lookup"><span data-stu-id="ec74f-113">The filter is implemented in a class named `IdentityBasicAuthenticationAttribute`.</span></span> <span data-ttu-id="ec74f-114">我不会显示所有的示例代码只是说明了如何编写身份验证筛选器的部件。</span><span class="sxs-lookup"><span data-stu-id="ec74f-114">I won't show all of the code from the sample, just the parts that illustrate how to write an authentication filter.</span></span>

## <a name="setting-an-authentication-filter"></a><span data-ttu-id="ec74f-115">将身份验证筛选器设置</span><span class="sxs-lookup"><span data-stu-id="ec74f-115">Setting an Authentication Filter</span></span>

<span data-ttu-id="ec74f-116">类似于其他筛选器，身份验证筛选器可以是应用的每个控制器，每个操作或全局范围内为所有 Web API 控制器。</span><span class="sxs-lookup"><span data-stu-id="ec74f-116">Like other filters, authentication filters can be applied per-controller, per-action, or globally to all Web API controllers.</span></span>

<span data-ttu-id="ec74f-117">若要应用到控制器的身份验证筛选器，修饰具有筛选器特性的控制器类。</span><span class="sxs-lookup"><span data-stu-id="ec74f-117">To apply an authentication filter to a controller, decorate the controller class with the filter attribute.</span></span> <span data-ttu-id="ec74f-118">下面的代码设置`[IdentityBasicAuthentication]`上了控制器类，从而使所有控制器的操作的基本身份验证筛选器。</span><span class="sxs-lookup"><span data-stu-id="ec74f-118">The following code sets the `[IdentityBasicAuthentication]` filter on a controller class, which enables Basic Authentication for all of the controller's actions.</span></span>

[!code-csharp[Main](authentication-filters/samples/sample1.cs)]

<span data-ttu-id="ec74f-119">要应用到一个操作筛选器，请使用筛选器修饰操作。</span><span class="sxs-lookup"><span data-stu-id="ec74f-119">To apply the filter to one action, decorate the action with the filter.</span></span> <span data-ttu-id="ec74f-120">下面的代码设置`[IdentityBasicAuthentication]`在控制器上的筛选器`Post`方法。</span><span class="sxs-lookup"><span data-stu-id="ec74f-120">The following code sets the `[IdentityBasicAuthentication]` filter on the controller's `Post` method.</span></span>

[!code-csharp[Main](authentication-filters/samples/sample2.cs)]

<span data-ttu-id="ec74f-121">若要将筛选器应用于所有的 Web API 控制器，将其添加到**GlobalConfiguration.Filters**。</span><span class="sxs-lookup"><span data-stu-id="ec74f-121">To apply the filter to all Web API controllers, add it to **GlobalConfiguration.Filters**.</span></span>

[!code-csharp[Main](authentication-filters/samples/sample3.cs)]

## <a name="implementing-a-web-api-authentication-filter"></a><span data-ttu-id="ec74f-122">实现 Web API 身份验证筛选器</span><span class="sxs-lookup"><span data-stu-id="ec74f-122">Implementing a Web API Authentication Filter</span></span>

<span data-ttu-id="ec74f-123">在 Web API 中，身份验证筛选器实现[System.Web.Http.Filters.IAuthenticationFilter](https://msdn.microsoft.com/library/system.web.http.filters.iauthenticationfilter.aspx)接口。</span><span class="sxs-lookup"><span data-stu-id="ec74f-123">In Web API, authentication filters implement the [System.Web.Http.Filters.IAuthenticationFilter](https://msdn.microsoft.com/library/system.web.http.filters.iauthenticationfilter.aspx) interface.</span></span> <span data-ttu-id="ec74f-124">它们还应继承自**System.Attribute**，以便作为属性应用。</span><span class="sxs-lookup"><span data-stu-id="ec74f-124">They should also inherit from **System.Attribute**, in order to be applied as attributes.</span></span>

<span data-ttu-id="ec74f-125">**IAuthenticationFilter**接口有两个方法：</span><span class="sxs-lookup"><span data-stu-id="ec74f-125">The **IAuthenticationFilter** interface has two methods:</span></span>

- <span data-ttu-id="ec74f-126">**AuthenticateAsync**请求进行身份验证通过验证凭据在请求中，如果存在。</span><span class="sxs-lookup"><span data-stu-id="ec74f-126">**AuthenticateAsync** authenticates the request by validating credentials in the request, if present.</span></span>
- <span data-ttu-id="ec74f-127">**ChallengeAsync**必要到 HTTP 响应中，添加身份验证质询。</span><span class="sxs-lookup"><span data-stu-id="ec74f-127">**ChallengeAsync** adds an authentication challenge to the HTTP response, if needed.</span></span>

<span data-ttu-id="ec74f-128">这些方法对应于定义中的身份验证流[RFC 2612](http://tools.ietf.org/html/rfc2616)并[RFC 2617](http://tools.ietf.org/html/rfc2617):</span><span class="sxs-lookup"><span data-stu-id="ec74f-128">These methods correspond to the authentication flow defined in [RFC 2612](http://tools.ietf.org/html/rfc2616) and [RFC 2617](http://tools.ietf.org/html/rfc2617):</span></span>

1. <span data-ttu-id="ec74f-129">客户端将 Authorization 标头中发送凭据。</span><span class="sxs-lookup"><span data-stu-id="ec74f-129">The client sends credentials in the Authorization header.</span></span> <span data-ttu-id="ec74f-130">这通常发生在客户端从服务器收到 401 （未经授权） 响应之后。</span><span class="sxs-lookup"><span data-stu-id="ec74f-130">This typically happens after the client receives a 401 (Unauthorized) response from the server.</span></span> <span data-ttu-id="ec74f-131">但是，客户端可以收到 401 后处理不只是发送的任何请求的凭据。</span><span class="sxs-lookup"><span data-stu-id="ec74f-131">However, a client can send credentials with any request, not just after getting a 401.</span></span>
2. <span data-ttu-id="ec74f-132">如果服务器不接受凭据，则返回 401 （未经授权） 响应。</span><span class="sxs-lookup"><span data-stu-id="ec74f-132">If the server does not accept the credentials, it returns a 401 (Unauthorized) response.</span></span> <span data-ttu-id="ec74f-133">响应包括 Www-authenticate 标头，其中包含一个或多个挑战。</span><span class="sxs-lookup"><span data-stu-id="ec74f-133">The response includes a Www-Authenticate header that contains one or more challenges.</span></span> <span data-ttu-id="ec74f-134">每个质询指定服务器识别的身份验证方案。</span><span class="sxs-lookup"><span data-stu-id="ec74f-134">Each challenge specifies an authentication scheme recognized by the server.</span></span>

<span data-ttu-id="ec74f-135">服务器还可以通过匿名请求返回 401。</span><span class="sxs-lookup"><span data-stu-id="ec74f-135">The server can also return 401 from an anonymous request.</span></span> <span data-ttu-id="ec74f-136">实际上，这通常是在发起身份验证过程的方式：</span><span class="sxs-lookup"><span data-stu-id="ec74f-136">In fact, that's typically how the authentication process is initiated:</span></span>

1. <span data-ttu-id="ec74f-137">客户端发送的匿名请求。</span><span class="sxs-lookup"><span data-stu-id="ec74f-137">The client sends an anonymous request.</span></span>
2. <span data-ttu-id="ec74f-138">服务器将返回 401。</span><span class="sxs-lookup"><span data-stu-id="ec74f-138">The server returns 401.</span></span>
3. <span data-ttu-id="ec74f-139">客户端重新发送请求使用的凭据。</span><span class="sxs-lookup"><span data-stu-id="ec74f-139">The clients resends the request with credentials.</span></span>

<span data-ttu-id="ec74f-140">此流包括这两个*身份验证*并*授权*步骤。</span><span class="sxs-lookup"><span data-stu-id="ec74f-140">This flow includes both *authentication* and *authorization* steps.</span></span>

- <span data-ttu-id="ec74f-141">身份验证可证明客户端的标识。</span><span class="sxs-lookup"><span data-stu-id="ec74f-141">Authentication proves the identity of the client.</span></span>
- <span data-ttu-id="ec74f-142">授权将确定客户端是否可以访问特定资源。</span><span class="sxs-lookup"><span data-stu-id="ec74f-142">Authorization determines whether the client can access a particular resource.</span></span>

<span data-ttu-id="ec74f-143">在 Web API 中，身份验证筛选器处理身份验证，但未授权。</span><span class="sxs-lookup"><span data-stu-id="ec74f-143">In Web API, authentication filters handle authentication, but not authorization.</span></span> <span data-ttu-id="ec74f-144">通过授权筛选器或在控制器操作中，则应完成授权。</span><span class="sxs-lookup"><span data-stu-id="ec74f-144">Authorization should be done by an authorization filter or inside the controller action.</span></span>

<span data-ttu-id="ec74f-145">下面是流中的 Web API 2 管道：</span><span class="sxs-lookup"><span data-stu-id="ec74f-145">Here is the flow in the Web API 2 pipeline:</span></span>

1. <span data-ttu-id="ec74f-146">在调用之前操作，Web API 创建该操作的身份验证筛选器的列表。</span><span class="sxs-lookup"><span data-stu-id="ec74f-146">Before invoking an action, Web API creates a list of the authentication filters for that action.</span></span> <span data-ttu-id="ec74f-147">这包括具有操作作用域、 控制器范围和全局范围的筛选器。</span><span class="sxs-lookup"><span data-stu-id="ec74f-147">This includes filters with action scope, controller scope, and global scope.</span></span>
2. <span data-ttu-id="ec74f-148">Web API 调用**AuthenticateAsync**上列表中每个筛选器。</span><span class="sxs-lookup"><span data-stu-id="ec74f-148">Web API calls **AuthenticateAsync** on every filter in the list.</span></span> <span data-ttu-id="ec74f-149">每个筛选器来验证请求中的凭据。</span><span class="sxs-lookup"><span data-stu-id="ec74f-149">Each filter can validate credentials in the request.</span></span> <span data-ttu-id="ec74f-150">如果任何筛选器已成功验证凭据，该筛选器将创建**IPrincipal**并将其附加到请求。</span><span class="sxs-lookup"><span data-stu-id="ec74f-150">If any filter successfully validates credentials, the filter creates an **IPrincipal** and attaches it to the request.</span></span> <span data-ttu-id="ec74f-151">筛选器还可以在此时触发错误。</span><span class="sxs-lookup"><span data-stu-id="ec74f-151">A filter can also trigger an error at this point.</span></span> <span data-ttu-id="ec74f-152">如果是这样，则不运行管道的其余部分。</span><span class="sxs-lookup"><span data-stu-id="ec74f-152">If so, the rest of the pipeline does not run.</span></span>
3. <span data-ttu-id="ec74f-153">假设没有错误，该请求流通过管道的其余部分。</span><span class="sxs-lookup"><span data-stu-id="ec74f-153">Assuming there is no error, the request flows through the rest of the pipeline.</span></span>
4. <span data-ttu-id="ec74f-154">最后，Web API 调用每个身份验证筛选器**ChallengeAsync**方法。</span><span class="sxs-lookup"><span data-stu-id="ec74f-154">Finally, Web API calls every authentication filter's **ChallengeAsync** method.</span></span> <span data-ttu-id="ec74f-155">筛选器使用此方法将一项挑战添加到响应中，如果需要。</span><span class="sxs-lookup"><span data-stu-id="ec74f-155">Filters use this method to add a challenge to the response, if needed.</span></span> <span data-ttu-id="ec74f-156">通常 （但并非总是如此），会发生 401 错误响应。</span><span class="sxs-lookup"><span data-stu-id="ec74f-156">Typically (but not always) that would happen in response to a 401 error.</span></span>

<span data-ttu-id="ec74f-157">下图显示两个可能的情况。</span><span class="sxs-lookup"><span data-stu-id="ec74f-157">The following diagrams show two possible cases.</span></span> <span data-ttu-id="ec74f-158">在第一个，身份验证筛选器已成功请求进行身份验证、 授权筛选器对请求，授权和控制器操作返回 200 （正常）。</span><span class="sxs-lookup"><span data-stu-id="ec74f-158">In the first, the authentication filter successfully authenticates the request, an authorization filter authorizes the request, and the controller action returns 200 (OK).</span></span>

![](authentication-filters/_static/image1.png)

<span data-ttu-id="ec74f-159">在第二个示例中，身份验证筛选器进行身份验证请求，但授权筛选器将返回 401 （未经授权）。</span><span class="sxs-lookup"><span data-stu-id="ec74f-159">In the second example, the authentication filter authenticates the request, but the authorization filter returns 401 (Unauthorized).</span></span> <span data-ttu-id="ec74f-160">在这种情况下，不会调用控制器操作。</span><span class="sxs-lookup"><span data-stu-id="ec74f-160">In this case, the controller action is not invoked.</span></span> <span data-ttu-id="ec74f-161">身份验证筛选器将 Www-authenticate 标头添加到响应。</span><span class="sxs-lookup"><span data-stu-id="ec74f-161">The authentication filter adds a Www-Authenticate header to the response.</span></span>

![](authentication-filters/_static/image2.png)

<span data-ttu-id="ec74f-162">其他组合都有可能&mdash;例如，如果控制器操作允许匿名请求，则可能必须身份验证筛选器，但没有授权。</span><span class="sxs-lookup"><span data-stu-id="ec74f-162">Other combinations are possible&mdash;for example, if the controller action allows anonymous requests, you might have an authentication filter but no authorization.</span></span>

## <a name="implementing-the-authenticateasync-method"></a><span data-ttu-id="ec74f-163">实现 AuthenticateAsync 方法</span><span class="sxs-lookup"><span data-stu-id="ec74f-163">Implementing the AuthenticateAsync Method</span></span>

<span data-ttu-id="ec74f-164">**AuthenticateAsync**方法尝试进行身份验证请求。</span><span class="sxs-lookup"><span data-stu-id="ec74f-164">The **AuthenticateAsync** method tries to authenticate the request.</span></span> <span data-ttu-id="ec74f-165">以下是方法签名：</span><span class="sxs-lookup"><span data-stu-id="ec74f-165">Here is the method signature:</span></span>

[!code-csharp[Main](authentication-filters/samples/sample4.cs)]

<span data-ttu-id="ec74f-166">**AuthenticateAsync**方法必须执行下列操作之一：</span><span class="sxs-lookup"><span data-stu-id="ec74f-166">The **AuthenticateAsync** method must do one of the following:</span></span>

1. <span data-ttu-id="ec74f-167">执行任何操作 （无操作）。</span><span class="sxs-lookup"><span data-stu-id="ec74f-167">Nothing (no-op).</span></span>
2. <span data-ttu-id="ec74f-168">创建**IPrincipal**并将其设置在请求上。</span><span class="sxs-lookup"><span data-stu-id="ec74f-168">Create an **IPrincipal** and set it on the request.</span></span>
3. <span data-ttu-id="ec74f-169">设置错误结果。</span><span class="sxs-lookup"><span data-stu-id="ec74f-169">Set an error result.</span></span>

<span data-ttu-id="ec74f-170">选项 (1) 表示该请求没有筛选器能够理解的任何凭据。</span><span class="sxs-lookup"><span data-stu-id="ec74f-170">Option (1) means the request did not have any credentials that the filter understands.</span></span> <span data-ttu-id="ec74f-171">选项 (2) 表示筛选器已成功通过身份验证请求。</span><span class="sxs-lookup"><span data-stu-id="ec74f-171">Option (2) means the filter successfully authenticated the request.</span></span> <span data-ttu-id="ec74f-172">选项 (3) 表示该请求具有无效凭据 （如错误的密码），这将触发错误响应。</span><span class="sxs-lookup"><span data-stu-id="ec74f-172">Option (3) means the request had invalid credentials (like the wrong password), which triggers an error response.</span></span>

<span data-ttu-id="ec74f-173">下面是用于实现常规大纲**AuthenticateAsync**。</span><span class="sxs-lookup"><span data-stu-id="ec74f-173">Here is a general outline for implementing **AuthenticateAsync**.</span></span>

1. <span data-ttu-id="ec74f-174">查找在请求中的凭据。</span><span class="sxs-lookup"><span data-stu-id="ec74f-174">Look for credentials in the request.</span></span>
2. <span data-ttu-id="ec74f-175">如果没有凭据，则不执行任何操作并返回 （无操作）。</span><span class="sxs-lookup"><span data-stu-id="ec74f-175">If there are no credentials, do nothing and return (no-op).</span></span>
3. <span data-ttu-id="ec74f-176">如果没有凭据，但筛选器不能识别的身份验证方案，不执行任何操作并返回 （无操作）。</span><span class="sxs-lookup"><span data-stu-id="ec74f-176">If there are credentials but the filter does not recognize the authentication scheme, do nothing and return (no-op).</span></span> <span data-ttu-id="ec74f-177">在管道中的另一个筛选器可能会理解此方案。</span><span class="sxs-lookup"><span data-stu-id="ec74f-177">Another filter in the pipeline might understand the scheme.</span></span>
4. <span data-ttu-id="ec74f-178">如果没有筛选器识别的凭据，请尝试对其进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="ec74f-178">If there are credentials that the filter understands, try to authenticate them.</span></span>
5. <span data-ttu-id="ec74f-179">如果凭据不正确，通过设置返回 401 `context.ErrorResult`。</span><span class="sxs-lookup"><span data-stu-id="ec74f-179">If the credentials are bad, return 401 by setting `context.ErrorResult`.</span></span>
6. <span data-ttu-id="ec74f-180">如果凭据有效，创建**IPrincipal**并设置`context.Principal`。</span><span class="sxs-lookup"><span data-stu-id="ec74f-180">If the credentials are valid, create an **IPrincipal** and set `context.Principal`.</span></span>

<span data-ttu-id="ec74f-181">以下代码所示**AuthenticateAsync**方法从[基本身份验证](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/BasicAuthentication/ReadMe.txt)示例。</span><span class="sxs-lookup"><span data-stu-id="ec74f-181">The follow code shows the **AuthenticateAsync** method from the [Basic Authentication](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/BasicAuthentication/ReadMe.txt) sample.</span></span> <span data-ttu-id="ec74f-182">注释中描述的每个步骤。</span><span class="sxs-lookup"><span data-stu-id="ec74f-182">The comments indicate each step.</span></span> <span data-ttu-id="ec74f-183">代码显示了几种类型的错误：使用任何凭据、 格式不正确的凭据和用户名/密码错误 Authorization 标头。</span><span class="sxs-lookup"><span data-stu-id="ec74f-183">The code shows several types of error: An Authorization header with no credentials, malformed credentials, and bad username/password.</span></span>

[!code-csharp[Main](authentication-filters/samples/sample5.cs)]

## <a name="setting-an-error-result"></a><span data-ttu-id="ec74f-184">设置错误结果</span><span class="sxs-lookup"><span data-stu-id="ec74f-184">Setting an Error Result</span></span>

<span data-ttu-id="ec74f-185">如果凭据无效，则必须设置的筛选器`context.ErrorResult`到**IHttpActionResult**创建错误响应。</span><span class="sxs-lookup"><span data-stu-id="ec74f-185">If the credentials are invalid, the filter must set `context.ErrorResult` to an **IHttpActionResult** that creates an error response.</span></span> <span data-ttu-id="ec74f-186">有关详细信息**IHttpActionResult**，请参阅[Web API 2 中的操作结果](../getting-started-with-aspnet-web-api/action-results.md)。</span><span class="sxs-lookup"><span data-stu-id="ec74f-186">For more information about **IHttpActionResult**, see [Action Results in Web API 2](../getting-started-with-aspnet-web-api/action-results.md).</span></span>

<span data-ttu-id="ec74f-187">基本身份验证示例包括`AuthenticationFailureResult`适用于此目的的类。</span><span class="sxs-lookup"><span data-stu-id="ec74f-187">The Basic Authentication sample includes an `AuthenticationFailureResult` class that is suitable for this purpose.</span></span>

[!code-csharp[Main](authentication-filters/samples/sample6.cs)]

## <a name="implementing-challengeasync"></a><span data-ttu-id="ec74f-188">实现 ChallengeAsync</span><span class="sxs-lookup"><span data-stu-id="ec74f-188">Implementing ChallengeAsync</span></span>

<span data-ttu-id="ec74f-189">目的**ChallengeAsync**方法是将身份验证质询添加到响应中，如果需要。</span><span class="sxs-lookup"><span data-stu-id="ec74f-189">The purpose of the **ChallengeAsync** method is to add authentication challenges to the response, if needed.</span></span> <span data-ttu-id="ec74f-190">以下是方法签名：</span><span class="sxs-lookup"><span data-stu-id="ec74f-190">Here is the method signature:</span></span>

[!code-csharp[Main](authentication-filters/samples/sample7.cs)]

<span data-ttu-id="ec74f-191">在请求管道中每个身份验证筛选器上调用方法。</span><span class="sxs-lookup"><span data-stu-id="ec74f-191">The method is called on every authentication filter in the request pipeline.</span></span>

<span data-ttu-id="ec74f-192">务必要理解这**ChallengeAsync**称为*之前*HTTP 响应已创建，并甚至可能之前的控制器操作运行。</span><span class="sxs-lookup"><span data-stu-id="ec74f-192">It's important to understand that **ChallengeAsync** is called *before* the HTTP response is created, and possibly even before the controller action runs.</span></span> <span data-ttu-id="ec74f-193">当**ChallengeAsync**调用时，`context.Result`包含**IHttpActionResult**，用于更高版本创建的 HTTP 响应。</span><span class="sxs-lookup"><span data-stu-id="ec74f-193">When **ChallengeAsync** is called, `context.Result` contains an **IHttpActionResult**, which is used later to create the HTTP response.</span></span> <span data-ttu-id="ec74f-194">因此，在**ChallengeAsync**是调用，你还没有了解有关 HTTP 响应的任何信息。</span><span class="sxs-lookup"><span data-stu-id="ec74f-194">So when **ChallengeAsync** is called, you don't know anything about the HTTP response yet.</span></span> <span data-ttu-id="ec74f-195">**ChallengeAsync**方法应替换的原始值`context.Result`用新**IHttpActionResult**。</span><span class="sxs-lookup"><span data-stu-id="ec74f-195">The **ChallengeAsync** method should replace the original value of `context.Result` with a new **IHttpActionResult**.</span></span> <span data-ttu-id="ec74f-196">这**IHttpActionResult**必须包装原始`context.Result`。</span><span class="sxs-lookup"><span data-stu-id="ec74f-196">This **IHttpActionResult** must wrap the original `context.Result`.</span></span>

![](authentication-filters/_static/image3.png)

<span data-ttu-id="ec74f-197">我将调用原始**IHttpActionResult** *内部结果*，并且新**IHttpActionResult** *外部结果*。</span><span class="sxs-lookup"><span data-stu-id="ec74f-197">I'll call the original **IHttpActionResult** the *inner result*, and the new **IHttpActionResult** the *outer result*.</span></span> <span data-ttu-id="ec74f-198">外部结果必须执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="ec74f-198">The outer result must do the following:</span></span>

1. <span data-ttu-id="ec74f-199">调用内部的结果创建 HTTP 响应。</span><span class="sxs-lookup"><span data-stu-id="ec74f-199">Invoke the inner result to create the HTTP response.</span></span>
2. <span data-ttu-id="ec74f-200">检查该响应。</span><span class="sxs-lookup"><span data-stu-id="ec74f-200">Examine the response.</span></span>
3. <span data-ttu-id="ec74f-201">如果需要为响应，添加身份验证质询。</span><span class="sxs-lookup"><span data-stu-id="ec74f-201">Add an authentication challenge to the response, if needed.</span></span>

<span data-ttu-id="ec74f-202">下面的示例来自基本身份验证示例。</span><span class="sxs-lookup"><span data-stu-id="ec74f-202">The following example is taken from the Basic Authentication sample.</span></span> <span data-ttu-id="ec74f-203">它定义**IHttpActionResult**外部的结果。</span><span class="sxs-lookup"><span data-stu-id="ec74f-203">It defines an **IHttpActionResult** for the outer result.</span></span>

[!code-csharp[Main](authentication-filters/samples/sample8.cs)]

<span data-ttu-id="ec74f-204">`InnerResult`属性包含内部**IHttpActionResult**。</span><span class="sxs-lookup"><span data-stu-id="ec74f-204">The `InnerResult` property holds the inner **IHttpActionResult**.</span></span> <span data-ttu-id="ec74f-205">`Challenge`属性表示 Www 身份验证标头。</span><span class="sxs-lookup"><span data-stu-id="ec74f-205">The `Challenge` property represents a Www-Authentication header.</span></span> <span data-ttu-id="ec74f-206">请注意， **ExecuteAsync**首先调用`InnerResult.ExecuteAsync`创建 HTTP 响应，然后根据需要添加面临的挑战。</span><span class="sxs-lookup"><span data-stu-id="ec74f-206">Notice that **ExecuteAsync** first calls `InnerResult.ExecuteAsync` to create the HTTP response, and then adds the challenge if needed.</span></span>

<span data-ttu-id="ec74f-207">添加这一难题之前检查响应代码。</span><span class="sxs-lookup"><span data-stu-id="ec74f-207">Check the response code before adding the challenge.</span></span> <span data-ttu-id="ec74f-208">大多数身份验证方案只能添加一项挑战如果响应，则 401，如下所示。</span><span class="sxs-lookup"><span data-stu-id="ec74f-208">Most authentication schemes only add a challenge if the response is 401, as shown here.</span></span> <span data-ttu-id="ec74f-209">但是，某些身份验证方案执行操作的成功响应向添加一项挑战。</span><span class="sxs-lookup"><span data-stu-id="ec74f-209">However, some authentication schemes do add a challenge to a success response.</span></span> <span data-ttu-id="ec74f-210">有关示例，请参阅[Negotiate](http://tools.ietf.org/html/rfc4559#section-5) (RFC 4559)。</span><span class="sxs-lookup"><span data-stu-id="ec74f-210">For example, see [Negotiate](http://tools.ietf.org/html/rfc4559#section-5) (RFC 4559).</span></span>

<span data-ttu-id="ec74f-211">给定`AddChallengeOnUnauthorizedResult`类中的实际代码**ChallengeAsync**很简单。</span><span class="sxs-lookup"><span data-stu-id="ec74f-211">Given the `AddChallengeOnUnauthorizedResult` class, the actual code in **ChallengeAsync** is simple.</span></span> <span data-ttu-id="ec74f-212">您只需创建的结果并将其附加到`context.Result`。</span><span class="sxs-lookup"><span data-stu-id="ec74f-212">You just create the result and attach it to `context.Result`.</span></span>

[!code-csharp[Main](authentication-filters/samples/sample9.cs)]

<span data-ttu-id="ec74f-213">注意:基本身份验证示例提取此逻辑一点，将其放在扩展方法。</span><span class="sxs-lookup"><span data-stu-id="ec74f-213">Note: The Basic Authentication sample abstracts this logic a bit, by placing it in an extension method.</span></span>

## <a name="combining-authentication-filters-with-host-level-authentication"></a><span data-ttu-id="ec74f-214">结合使用主机级别的身份验证的身份验证筛选器</span><span class="sxs-lookup"><span data-stu-id="ec74f-214">Combining Authentication Filters with Host-Level Authentication</span></span>

<span data-ttu-id="ec74f-215">"主机级别的身份验证"是之前的请求到达 Web API 框架执行的主机 （如 IIS) 中，身份验证。</span><span class="sxs-lookup"><span data-stu-id="ec74f-215">"Host-level authentication" is authentication performed by the host (such as IIS), before the request reaches the Web API framework.</span></span>

<span data-ttu-id="ec74f-216">通常情况下，你可能想要启用应用程序的其余部分的主机级身份验证，但禁用的 Web API 控制器。</span><span class="sxs-lookup"><span data-stu-id="ec74f-216">Often, you may want to enable host-level authentication for the rest of your application, but disable it for your Web API controllers.</span></span> <span data-ttu-id="ec74f-217">例如，典型的方案是启用表单身份验证在主机级别，但对 Web API 使用基于令牌的身份验证。</span><span class="sxs-lookup"><span data-stu-id="ec74f-217">For example, a typical scenario is to enable Forms Authentication at the host level, but use token-based authentication for Web API.</span></span>

<span data-ttu-id="ec74f-218">若要禁用 Web API 管道中的主机级身份验证，请调用`config.SuppressHostPrincipal()`在配置中。</span><span class="sxs-lookup"><span data-stu-id="ec74f-218">To disable host-level authentication inside the Web API pipeline, call `config.SuppressHostPrincipal()` in your configuration.</span></span> <span data-ttu-id="ec74f-219">这会导致 Web API 删除**IPrincipal**从输入 Web API 管道的任何请求。</span><span class="sxs-lookup"><span data-stu-id="ec74f-219">This causes Web API to remove the **IPrincipal** from any request that enters the Web API pipeline.</span></span> <span data-ttu-id="ec74f-220">实际上，它&quot;取消-进行身份验证&quot;请求。</span><span class="sxs-lookup"><span data-stu-id="ec74f-220">Effectively, it &quot;un-authenticates&quot; the request.</span></span>

[!code-csharp[Main](authentication-filters/samples/sample10.cs)]

## <a name="additional-resources"></a><span data-ttu-id="ec74f-221">其他资源</span><span class="sxs-lookup"><span data-stu-id="ec74f-221">Additional Resources</span></span>

<span data-ttu-id="ec74f-222">[ASP.NET Web API 安全筛选器](https://msdn.microsoft.com/magazine/dn781361.aspx)（MSDN 杂志）</span><span class="sxs-lookup"><span data-stu-id="ec74f-222">[ASP.NET Web API Security Filters](https://msdn.microsoft.com/magazine/dn781361.aspx) (MSDN Magazine)</span></span>

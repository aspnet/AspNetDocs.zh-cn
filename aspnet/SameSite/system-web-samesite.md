---
title: 在 ASP.NET 中使用 SameSite cookie
author: rick-anderson
description: 了解如何使用在 ASP.NET 中 SameSite cookie
ms.author: riande
ms.date: 2/15/2019
uid: samesite/system-web-samesite
ms.openlocfilehash: d50f157c6d92cb56cb6c59381af9139d1d3d1d3d
ms.sourcegitcommit: a309ca7af61e59195beb745b501a1a9f06fcd493
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/16/2020
ms.locfileid: "92119358"
---
# <a name="work-with-samesite-cookies-in-aspnet"></a><span data-ttu-id="a80a8-103">在 ASP.NET 中使用 SameSite cookie</span><span class="sxs-lookup"><span data-stu-id="a80a8-103">Work with SameSite cookies in ASP.NET</span></span>

<span data-ttu-id="a80a8-104">作者：[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="a80a8-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="a80a8-105">SameSite 是一种 [IETF](https://ietf.org/about/) 草案标准，旨在针对跨站点请求伪造 (CSRF) 攻击提供一些保护。</span><span class="sxs-lookup"><span data-stu-id="a80a8-105">SameSite is an [IETF](https://ietf.org/about/) draft standard designed to provide some protection against cross-site request forgery (CSRF) attacks.</span></span> <span data-ttu-id="a80a8-106">最初在 [2016](https://tools.ietf.org/html/draft-west-first-party-cookies-07)中起草草案标准版已在 [2019](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00)中更新。</span><span class="sxs-lookup"><span data-stu-id="a80a8-106">Originally drafted in [2016](https://tools.ietf.org/html/draft-west-first-party-cookies-07), the draft standard was updated in [2019](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00).</span></span> <span data-ttu-id="a80a8-107">更新的标准与以前的标准不是向后兼容，以下是最明显的区别：</span><span class="sxs-lookup"><span data-stu-id="a80a8-107">The updated standard is not backward compatible with the previous standard, with the following being the most noticeable differences:</span></span>

* <span data-ttu-id="a80a8-108">默认情况下，不带 SameSite 标头的 cookie 被视为 `SameSite=Lax` 。</span><span class="sxs-lookup"><span data-stu-id="a80a8-108">Cookies without SameSite header are treated as `SameSite=Lax` by default.</span></span>
* <span data-ttu-id="a80a8-109">`SameSite=None` 必须使用以允许跨站点 cookie。</span><span class="sxs-lookup"><span data-stu-id="a80a8-109">`SameSite=None` must be used to allow cross-site cookie use.</span></span>
* <span data-ttu-id="a80a8-110">断言 `SameSite=None` 还必须标记为的 cookie `Secure` 。</span><span class="sxs-lookup"><span data-stu-id="a80a8-110">Cookies that assert `SameSite=None` must also be marked as `Secure`.</span></span>
* <span data-ttu-id="a80a8-111">使用的应用程序 [`<iframe>`](https://developer.mozilla.org/docs/Web/HTML/Element/iframe) 可能会遇到 `sameSite=Lax` 或 cookie 的问题， `sameSite=Strict` 因为 `<iframe>` 被视为跨站点方案。</span><span class="sxs-lookup"><span data-stu-id="a80a8-111">Applications that use [`<iframe>`](https://developer.mozilla.org/docs/Web/HTML/Element/iframe) may experience issues with `sameSite=Lax` or `sameSite=Strict` cookies because `<iframe>` is treated as cross-site scenarios.</span></span>
* <span data-ttu-id="a80a8-112">`SameSite=None` [2016 标准](https://tools.ietf.org/html/draft-west-first-party-cookies-07)不允许该值，并导致某些实现将此类 cookie 视为 `SameSite=Strict` 。</span><span class="sxs-lookup"><span data-stu-id="a80a8-112">The value `SameSite=None` is not allowed by the [2016 standard](https://tools.ietf.org/html/draft-west-first-party-cookies-07) and causes some implementations to treat such cookies as `SameSite=Strict`.</span></span> <span data-ttu-id="a80a8-113">请参阅本文档中的 [支持旧版浏览器](#sob) 。</span><span class="sxs-lookup"><span data-stu-id="a80a8-113">See [Supporting older browsers](#sob) in this document.</span></span>

<span data-ttu-id="a80a8-114">此 `SameSite=Lax` 设置适用于大多数应用程序 cookie。</span><span class="sxs-lookup"><span data-stu-id="a80a8-114">The `SameSite=Lax` setting works for most application cookies.</span></span> <span data-ttu-id="a80a8-115">某些形式的身份验证，例如 [OpenID connect](https://openid.net/connect/) (OIDC) ，并且 [WS 联合](https://auth0.com/docs/protocols/ws-fed) 身份验证默认为基于 POST 的重定向。</span><span class="sxs-lookup"><span data-stu-id="a80a8-115">Some forms of authentication like [OpenID Connect](https://openid.net/connect/) (OIDC) and [WS-Federation](https://auth0.com/docs/protocols/ws-fed) default to POST based redirects.</span></span> <span data-ttu-id="a80a8-116">基于后期的重定向会触发 SameSite 浏览器保护，因此，对这些组件禁用了 SameSite。</span><span class="sxs-lookup"><span data-stu-id="a80a8-116">The POST based redirects trigger the SameSite browser protections, so SameSite is disabled for these components.</span></span> <span data-ttu-id="a80a8-117">由于请求的流动方式不同，大多数 [OAuth](https://oauth.net/) 登录名不受影响。</span><span class="sxs-lookup"><span data-stu-id="a80a8-117">Most [OAuth](https://oauth.net/) logins are not affected due to differences in how the request flows.</span></span>

<span data-ttu-id="a80a8-118">发出 cookie 的每个 ASP.NET 组件都需要确定 SameSite 是否适用。</span><span class="sxs-lookup"><span data-stu-id="a80a8-118">Each ASP.NET component that emits cookies needs to decide if SameSite is appropriate.</span></span>

<span data-ttu-id="a80a8-119">在安装 2019 .Net SameSite 更新后，请参阅应用程序问题的 [已知问题](#known) 。</span><span class="sxs-lookup"><span data-stu-id="a80a8-119">See [Known Issues](#known) for problems with applications after installing the 2019 .Net SameSite updates.</span></span>

## <a name="using-samesite-in-aspnet-472-and-48"></a><span data-ttu-id="a80a8-120">在 ASP.NET 4.7.2 和4.8 中使用 SameSite</span><span class="sxs-lookup"><span data-stu-id="a80a8-120">Using SameSite in ASP.NET 4.7.2 and 4.8</span></span>

<span data-ttu-id="a80a8-121">.Net 4.7.2 和4.8 支持 SameSite 的 [2019 草案标准](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00) ，因为年12月2019更新发布。</span><span class="sxs-lookup"><span data-stu-id="a80a8-121">.Net 4.7.2 and 4.8 supports the [2019 draft standard](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00) for SameSite since the release of updates in December 2019.</span></span> <span data-ttu-id="a80a8-122">开发人员可以使用 [HttpCookie 属性](/dotnet/api/system.web.httpcookie.samesite#System_Web_HttpCookie_SameSite)以编程方式控制 SameSite 标头的值。</span><span class="sxs-lookup"><span data-stu-id="a80a8-122">Developers are able to programmatically control the value of the SameSite header using the [HttpCookie.SameSite property](/dotnet/api/system.web.httpcookie.samesite#System_Web_HttpCookie_SameSite).</span></span> <span data-ttu-id="a80a8-123">将 `SameSite` 属性设置为 `Strict` 、 `Lax` 或会 `None` 导致这些值用 cookie 写入网络。</span><span class="sxs-lookup"><span data-stu-id="a80a8-123">Setting the `SameSite` property to `Strict`, `Lax`, or `None` results in those values being written on the network with the cookie.</span></span> <span data-ttu-id="a80a8-124">如果将其设置为 "等于"，则 `(SameSiteMode)(-1)` 表示网络上不应包含带有 cookie 的 SameSite 标头。</span><span class="sxs-lookup"><span data-stu-id="a80a8-124">Setting it equal to `(SameSiteMode)(-1)` indicates that no SameSite header should be included on the network with the cookie.</span></span> <span data-ttu-id="a80a8-125">[HttpCookie 属性](/dotnet/api/system.web.httpcookie.secure)（或配置文件中的 "requireSSL"）可用于将 cookie 标记为 `Secure` 。</span><span class="sxs-lookup"><span data-stu-id="a80a8-125">The [HttpCookie.Secure Property](/dotnet/api/system.web.httpcookie.secure), or 'requireSSL' in config files, can be used to mark the cookie as `Secure` or not.</span></span>

<span data-ttu-id="a80a8-126">新 `HttpCookie` 实例将默认为 `SameSite=(SameSiteMode)(-1)` 和 `Secure=false` 。</span><span class="sxs-lookup"><span data-stu-id="a80a8-126">New `HttpCookie` instances will default to `SameSite=(SameSiteMode)(-1)` and `Secure=false`.</span></span> <span data-ttu-id="a80a8-127">可以在配置节中重写这些默认值 `system.web/httpCookies` ，其中字符串 `"Unspecified"` 是适用于的友好仅配置语法 `(SameSiteMode)(-1)` ：</span><span class="sxs-lookup"><span data-stu-id="a80a8-127">These defaults can be overridden in the `system.web/httpCookies` configuration section, where the string `"Unspecified"` is a friendly configuration-only syntax for `(SameSiteMode)(-1)`:</span></span>

```xml
<configuration>
 <system.web>
  <httpCookies sameSite="[Strict|Lax|None|Unspecified]" requireSSL="[true|false]" />
 <system.web>
<configuration>
```

<span data-ttu-id="a80a8-128">ASP.Net 还为这些功能颁发了自己的四个特定 cookie：匿名身份验证、Forms 身份验证、会话状态和角色管理。</span><span class="sxs-lookup"><span data-stu-id="a80a8-128">ASP.Net also issues four specific cookies of its own for these features: Anonymous Authentication, Forms Authentication, Session State, and Role Management.</span></span> <span data-ttu-id="a80a8-129">可以使用和属性来操作在运行时中获得的这些 cookie 的实例 `SameSite` ， `Secure` 就像任何其他 HttpCookie 实例一样。</span><span class="sxs-lookup"><span data-stu-id="a80a8-129">Instances of these cookies obtained in runtime can be manipulated using the `SameSite` and `Secure` properties just like any other HttpCookie instance.</span></span> <span data-ttu-id="a80a8-130">然而，由于 SameSite 标准的大杂烩出现，这四个功能 cookie 的配置选项不一致。</span><span class="sxs-lookup"><span data-stu-id="a80a8-130">However, due to the patchwork emergence of the SameSite standard, configuration options for these four features cookies is inconsistent.</span></span> <span data-ttu-id="a80a8-131">相关配置节和属性的默认值如下所示。</span><span class="sxs-lookup"><span data-stu-id="a80a8-131">The relevant configuration sections and attributes, with defaults, are shown below.</span></span> <span data-ttu-id="a80a8-132">如果 `SameSite` 某个功能没有或 `Secure` 相关的属性，则该功能将回退前面讨论的部分中配置的默认值 `system.web/httpCookies` 。</span><span class="sxs-lookup"><span data-stu-id="a80a8-132">If there is no `SameSite` or `Secure` related attribute for a feature, then the feature will fall back on the defaults configured in the `system.web/httpCookies` section discussed above.</span></span>

```xml
<configuration>
 <system.web>
  <anonymousIdentification cookieRequireSSL="false" /> <!-- No config attribute for SameSite -->
  <authentication>
   <forms cookieSameSite="Lax" requireSSL="false" />
  </authentication>
  <sessionState cookieSameSite="Lax" /> <!-- No config attribute for Secure -->
  <roleManager cookieRequireSSL="false" /> <!-- No config attribute for SameSite -->
 <system.web>
<configuration>
```  

<span data-ttu-id="a80a8-133">**注意**：目前仅可使用 "未指定" `system.web/httpCookies@sameSite` 。</span><span class="sxs-lookup"><span data-stu-id="a80a8-133">**Note**: 'Unspecified' is only available to `system.web/httpCookies@sameSite` at the moment.</span></span> <span data-ttu-id="a80a8-134">我们希望在以后的更新中，将类似语法添加到前面所示的 cookieSameSite 属性。</span><span class="sxs-lookup"><span data-stu-id="a80a8-134">We hope to add similar syntax to the previously shown cookieSameSite attributes in future updates.</span></span> <span data-ttu-id="a80a8-135">`(SameSiteMode)(-1)`代码中的设置仍适用于这些 cookie 的实例。 \*</span><span class="sxs-lookup"><span data-stu-id="a80a8-135">Setting `(SameSiteMode)(-1)` in code still works on instances of these cookies.\*</span></span>

[!INCLUDE[](~/includes/MTcomments.md)]

<a name="retargeting"></a>

### <a name="retarget-net-apps"></a><span data-ttu-id="a80a8-136">重定目标 .NET 应用</span><span class="sxs-lookup"><span data-stu-id="a80a8-136">Retarget .NET apps</span></span>

<span data-ttu-id="a80a8-137">面向 .NET 4.7.2 或更高版本：</span><span class="sxs-lookup"><span data-stu-id="a80a8-137">To target .NET 4.7.2 or later:</span></span>

* <span data-ttu-id="a80a8-138">确保 *web.config* 包含以下各项：</span><span class="sxs-lookup"><span data-stu-id="a80a8-138">Ensure *web.config* contains the following:</span></span>  <!-- review, I removed `debug="true"` -->

  ```xml
  <system.web>
    <compilation targetFramework="4.7.2"/>
    <httpRuntime targetFramework="4.7.2"/>
  </system.web>

* Verify the project file contains the correct [TargetFrameworkVersion](/visualstudio/msbuild/msbuild-target-framework-and-target-platform?view=vs-2019):

  ```xml
  <TargetFrameworkVersion>v4.7.2</TargetFrameworkVersion>
  ```

  <span data-ttu-id="a80a8-139">[.Net 迁移指南](/dotnet/framework/migration-guide/)提供了更多详细信息。</span><span class="sxs-lookup"><span data-stu-id="a80a8-139">The [.NET Migration Guide](/dotnet/framework/migration-guide/) has more details.</span></span>

* <span data-ttu-id="a80a8-140">验证项目中的 NuGet 包的版本是否正确。</span><span class="sxs-lookup"><span data-stu-id="a80a8-140">Verify NuGet packages in the project are targeted at the correct framework version.</span></span> <span data-ttu-id="a80a8-141">可以通过检查 *packages.config* 文件来验证正确的框架版本，例如：</span><span class="sxs-lookup"><span data-stu-id="a80a8-141">You can verify the correct framework version by examining the *packages.config* file, for example:</span></span>

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <packages>
    <package id="Microsoft.AspNet.Mvc" version="5.2.7" targetFramework="net472" />
    <package id="Microsoft.ApplicationInsights" version="2.4.0" targetFramework="net451" />
  </packages>
  ```

  <span data-ttu-id="a80a8-142">在上述 *packages.config* 文件中， `Microsoft.ApplicationInsights` 包：</span><span class="sxs-lookup"><span data-stu-id="a80a8-142">In the preceding *packages.config* file, the `Microsoft.ApplicationInsights` package:</span></span>
    * <span data-ttu-id="a80a8-143">面向 .NET 4.5.1。</span><span class="sxs-lookup"><span data-stu-id="a80a8-143">Is  targeted against .NET 4.5.1.</span></span>
    * <span data-ttu-id="a80a8-144">应将其 `targetFramework` 属性更新为， `net472` 前提是目标为框架目标的更新包已存在。</span><span class="sxs-lookup"><span data-stu-id="a80a8-144">Should have its `targetFramework` attribute updated to `net472` if an updated package targeting your framework target exists.</span></span>

<a name="nope"></a>

### <a name="net-versions-earlier-than-472"></a><span data-ttu-id="a80a8-145">早于4.7.2 的 .NET 版本</span><span class="sxs-lookup"><span data-stu-id="a80a8-145">.NET versions earlier than 4.7.2</span></span>

<span data-ttu-id="a80a8-146">Microsoft 不支持将4.7.2 用于写入同一站点 cookie 属性的 .NET 版本。</span><span class="sxs-lookup"><span data-stu-id="a80a8-146">Microsoft does not support .NET versions lower that 4.7.2 for writing the same-site cookie attribute.</span></span> <span data-ttu-id="a80a8-147">我们找不到一种可靠的方法来执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="a80a8-147">We have not found a reliable way to:</span></span>

* <span data-ttu-id="a80a8-148">确保根据浏览器版本正确写入特性。</span><span class="sxs-lookup"><span data-stu-id="a80a8-148">Ensure the attribute is written correctly based on browser version.</span></span>
* <span data-ttu-id="a80a8-149">在旧版本的 framework 上拦截并调整身份验证和会话 cookie。</span><span class="sxs-lookup"><span data-stu-id="a80a8-149">Intercept and adjust authentication and session cookies on older framework versions.</span></span>

### <a name="december-patch-behavior-changes"></a><span data-ttu-id="a80a8-150">12月修补程序行为更改</span><span class="sxs-lookup"><span data-stu-id="a80a8-150">December patch behavior changes</span></span>

<span data-ttu-id="a80a8-151">.NET Framework 的特定行为更改是 `SameSite` 属性如何解释 `None` 值：</span><span class="sxs-lookup"><span data-stu-id="a80a8-151">The specific behavior change for .NET Framework is how the `SameSite` property interprets the `None` value:</span></span>

* <span data-ttu-id="a80a8-152">在修补程序的值为之前 `None` ：</span><span class="sxs-lookup"><span data-stu-id="a80a8-152">Before the patch a value of `None` meant:</span></span>
  * <span data-ttu-id="a80a8-153">根本不发出属性。</span><span class="sxs-lookup"><span data-stu-id="a80a8-153">Do not emit the attribute at all.</span></span>
* <span data-ttu-id="a80a8-154">修补后：</span><span class="sxs-lookup"><span data-stu-id="a80a8-154">After the patch:</span></span>
  * <span data-ttu-id="a80a8-155">值为 `None` 表示 "发出属性，其值为 `None` "。</span><span class="sxs-lookup"><span data-stu-id="a80a8-155">A value of `None` means "Emit the attribute with a value of `None`".</span></span>
  * <span data-ttu-id="a80a8-156">`SameSite`值为将 `(SameSiteMode)(-1)` 导致不发出属性。</span><span class="sxs-lookup"><span data-stu-id="a80a8-156">A `SameSite` value of `(SameSiteMode)(-1)` causes the attribute not to be emitted.</span></span>

<span data-ttu-id="a80a8-157">Forms 身份验证和会话状态 cookie 的默认 SameSite 值从更改 `None` 为 `Lax` 。</span><span class="sxs-lookup"><span data-stu-id="a80a8-157">The default SameSite value for forms authentication and session state cookies was changed from `None` to `Lax`.</span></span>

### <a name="summary-of-change-impact-on-browsers"></a><span data-ttu-id="a80a8-158">更改对浏览器的影响</span><span class="sxs-lookup"><span data-stu-id="a80a8-158">Summary of change impact on browsers</span></span>

<span data-ttu-id="a80a8-159">如果安装修补程序并使用发出 cookie，则 `SameSite.None` 将发生以下两种情况之一：</span><span class="sxs-lookup"><span data-stu-id="a80a8-159">If you install the patch and issue a cookie with `SameSite.None`, one of two things will happen:</span></span>
* <span data-ttu-id="a80a8-160">Chrome v80 将根据新的实现来处理此 cookie，而不会对 cookie 强制实施相同的站点限制。</span><span class="sxs-lookup"><span data-stu-id="a80a8-160">Chrome v80 will treat this cookie according to the new implementation, and not enforce same site restrictions on the cookie.</span></span>
* <span data-ttu-id="a80a8-161">尚未更新以支持新实现的任何浏览器都将遵循旧实现。</span><span class="sxs-lookup"><span data-stu-id="a80a8-161">Any browser that has not been updated to support the new implementation will follow the old implementation.</span></span> <span data-ttu-id="a80a8-162">旧实现显示：</span><span class="sxs-lookup"><span data-stu-id="a80a8-162">The old implementation says:</span></span>
  * <span data-ttu-id="a80a8-163">如果你看到不了解的值，请将其忽略，并切换到严格相同的站点限制。</span><span class="sxs-lookup"><span data-stu-id="a80a8-163">If you see a value you don't understand, ignore it and switch to strict same site restrictions.</span></span>

<span data-ttu-id="a80a8-164">这样，应用程序就可以在 Chrome 中中断，也可以在很多其他地方中断。</span><span class="sxs-lookup"><span data-stu-id="a80a8-164">So either the app breaks in Chrome, or you break in numerous other places.</span></span>

## <a name="history-and-changes"></a><span data-ttu-id="a80a8-165">历史记录和更改</span><span class="sxs-lookup"><span data-stu-id="a80a8-165">History and changes</span></span>

<span data-ttu-id="a80a8-166">SameSite 支持是在使用 [2016 草案标准](https://tools.ietf.org/html/draft-west-first-party-cookies-07#section-4.1)的 .net 4.7.2 中首次实现的。</span><span class="sxs-lookup"><span data-stu-id="a80a8-166">SameSite support was first implemented in .NET 4.7.2 using the [2016 draft standard](https://tools.ietf.org/html/draft-west-first-party-cookies-07#section-4.1).</span></span>

<span data-ttu-id="a80a8-167">2019年11月19日更新了 Windows 更新后的 .NET 4.7.2 + 2016 标准版和2019标准版。</span><span class="sxs-lookup"><span data-stu-id="a80a8-167">The November 19, 2019 updates for Windows updated .NET 4.7.2+ from the 2016 standard to the 2019 standard.</span></span> <span data-ttu-id="a80a8-168">其他版本的 Windows 即将推出其他更新。</span><span class="sxs-lookup"><span data-stu-id="a80a8-168">Additional updates are forthcoming for other versions of Windows.</span></span> <span data-ttu-id="a80a8-169">有关详细信息，请参阅 <xref:samesite/kbs-samesite>。</span><span class="sxs-lookup"><span data-stu-id="a80a8-169">For more information, see <xref:samesite/kbs-samesite>.</span></span>

 <span data-ttu-id="a80a8-170">SameSite 规范的2019草案：</span><span class="sxs-lookup"><span data-stu-id="a80a8-170">The 2019 draft of the SameSite specification:</span></span>

* <span data-ttu-id="a80a8-171">**不**向后兼容2016草案。</span><span class="sxs-lookup"><span data-stu-id="a80a8-171">Is **not** backwards compatible with the 2016 draft.</span></span> <span data-ttu-id="a80a8-172">有关详细信息，请参阅本文档中的 [支持旧版浏览器](#sob) 。</span><span class="sxs-lookup"><span data-stu-id="a80a8-172">For more information, see [Supporting older browsers](#sob) in this document.</span></span>
* <span data-ttu-id="a80a8-173">指定 `SameSite=Lax` 按默认值处理 cookie。</span><span class="sxs-lookup"><span data-stu-id="a80a8-173">Specifies cookies are treated as `SameSite=Lax` by default.</span></span>
* <span data-ttu-id="a80a8-174">指定显式断言以便 `SameSite=None` 启用跨站点传递的 cookie 也应该标记为 `Secure` 。</span><span class="sxs-lookup"><span data-stu-id="a80a8-174">Specifies cookies that explicitly assert `SameSite=None` in order to enable cross-site delivery should also be marked as `Secure`.</span></span>
* <span data-ttu-id="a80a8-175">按照上面列出的 KB 中所述，发布的修补程序支持。</span><span class="sxs-lookup"><span data-stu-id="a80a8-175">Is supported by patches issued as described in the KB's listed above.</span></span>
* <span data-ttu-id="a80a8-176">默认 [情况下，计划](https://chromestatus.com/feature/5088147346030592) 在 [2020 年2月](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)启用。</span><span class="sxs-lookup"><span data-stu-id="a80a8-176">Is scheduled to be enabled by [Chrome](https://chromestatus.com/feature/5088147346030592) by default in [Feb 2020](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html).</span></span> <span data-ttu-id="a80a8-177">浏览器已开始在2019中移动到此标准。</span><span class="sxs-lookup"><span data-stu-id="a80a8-177">Browsers started moving to this standard in 2019.</span></span>

<a name="known"></a>

## <a name="known-issues"></a><span data-ttu-id="a80a8-178">已知问题</span><span class="sxs-lookup"><span data-stu-id="a80a8-178">Known Issues</span></span>

<span data-ttu-id="a80a8-179">因为2016和2019草案规范不兼容，所以，11月 2019 .Net Framework 更新引入了一些可能会中断的更改。</span><span class="sxs-lookup"><span data-stu-id="a80a8-179">Because the 2016 and 2019 draft specifications are not compatible, the November 2019 .Net Framework update introduces some changes that may be breaking.</span></span>

* <span data-ttu-id="a80a8-180">会话状态和窗体身份验证 cookie 现在会写入网络， `Lax` 而不是未指定。</span><span class="sxs-lookup"><span data-stu-id="a80a8-180">Session State and Forms Authentication cookies are now written to the network as `Lax` instead of unspecified.</span></span>
  * <span data-ttu-id="a80a8-181">大多数应用程序使用 `SameSite=Lax` cookie 时，通过在使用的站点或应用程序中发布的应用程序 `iframe` 可能会发现其会话状态或窗体授权 cookie 没有按预期方式使用。</span><span class="sxs-lookup"><span data-stu-id="a80a8-181">While most apps work with `SameSite=Lax` cookies, apps that POST across sites or applications that make use of `iframe` may find that their session state or forms authorization cookies aren't being used as expected.</span></span> <span data-ttu-id="a80a8-182">若要解决此情况，请 `cookieSameSite` 在前面所述的相应配置节中更改值。</span><span class="sxs-lookup"><span data-stu-id="a80a8-182">To remedy this, change the `cookieSameSite` value in the appropriate configuration section as discussed previously.</span></span>
* <span data-ttu-id="a80a8-183">`SameSite=None`在代码或配置中显式设置的 HttpCookies 现在将使用 cookie 写入该值，而以前省略了该值。</span><span class="sxs-lookup"><span data-stu-id="a80a8-183">HttpCookies that explicitly set `SameSite=None` in code or configuration now have that value written with the cookie, whereas it was previously omitted.</span></span> <span data-ttu-id="a80a8-184">这可能会导致旧版浏览器出现一些仅支持2016草案标准的问题。</span><span class="sxs-lookup"><span data-stu-id="a80a8-184">This may cause issues with older browsers that only support the 2016 draft standard.</span></span>
  * <span data-ttu-id="a80a8-185">如果面向的浏览器支持2019草案 standard with `SameSite=None` cookie，请记住也要将其标记为 `Secure` 或无法识别。</span><span class="sxs-lookup"><span data-stu-id="a80a8-185">When targeting browsers supporting the 2019 draft standard with `SameSite=None` cookies, remember to also mark them `Secure` or they may not be recognized.</span></span>
  * <span data-ttu-id="a80a8-186">若要恢复为2016的不写入行为 `SameSite=None` ，请使用应用设置 `aspnet:SupressSameSiteNone=true` 。</span><span class="sxs-lookup"><span data-stu-id="a80a8-186">To revert to the 2016 behavior of not writing `SameSite=None`, use the app setting `aspnet:SupressSameSiteNone=true`.</span></span> <span data-ttu-id="a80a8-187">请注意，这将适用于应用中的所有 HttpCookies。</span><span class="sxs-lookup"><span data-stu-id="a80a8-187">Note that this will apply to all HttpCookies in the app.</span></span>

### <a name="azure-app-servicesamesite-cookie-handling"></a><span data-ttu-id="a80a8-188">Azure App Service — SameSite cookie 处理</span><span class="sxs-lookup"><span data-stu-id="a80a8-188">Azure App Service—SameSite cookie handling</span></span>

<span data-ttu-id="a80a8-189">请参阅 [Azure App Service-SameSite cookie 处理和 .NET Framework 4.7.2 修补程序](https://azure.microsoft.com/updates/app-service-samesite-cookie-update/) ，以获取有关 Azure App Service 如何在 .net 4.7.2 apps 中配置 SameSite 行为的信息。</span><span class="sxs-lookup"><span data-stu-id="a80a8-189">See [Azure App Service—SameSite cookie handling and .NET Framework 4.7.2 patch](https://azure.microsoft.com/updates/app-service-samesite-cookie-update/) for information about how Azure App Service is configuring SameSite behaviors in .Net 4.7.2 apps.</span></span>

<a name="sob"></a>

## <a name="supporting-older-browsers"></a><span data-ttu-id="a80a8-190">支持旧版浏览器</span><span class="sxs-lookup"><span data-stu-id="a80a8-190">Supporting older browsers</span></span>

<span data-ttu-id="a80a8-191">2016 SameSite 标准规定，未知值必须被视为 `SameSite=Strict` 值。</span><span class="sxs-lookup"><span data-stu-id="a80a8-191">The 2016 SameSite standard mandated that unknown values must be treated as `SameSite=Strict` values.</span></span> <span data-ttu-id="a80a8-192">从支持 2016 SameSite 标准的旧版浏览器访问的应用在收到值为的 SameSite 属性时可能会中断 `None` 。</span><span class="sxs-lookup"><span data-stu-id="a80a8-192">Apps accessed from older browsers which support the 2016 SameSite standard may break when they get a SameSite property with a value of `None`.</span></span> <span data-ttu-id="a80a8-193">如果 Web 应用要支持较旧的浏览器，则必须实现浏览器检测。</span><span class="sxs-lookup"><span data-stu-id="a80a8-193">Web apps must implement browser detection if they intend to support older browsers.</span></span> <span data-ttu-id="a80a8-194">ASP.NET 不会实现浏览器检测，因为 User-Agents 的值非常不稳定，会频繁更改。</span><span class="sxs-lookup"><span data-stu-id="a80a8-194">ASP.NET doesn't implement browser detection because User-Agents values are highly volatile and change frequently.</span></span>

<span data-ttu-id="a80a8-195">Microsoft 解决该问题的方法是帮助您实现浏览器检测组件，以便在 `sameSite=None` 浏览器不支持时从 cookie 中去除属性。</span><span class="sxs-lookup"><span data-stu-id="a80a8-195">Microsoft's approach to fixing the problem is to help you implement browser detection components to strip the `sameSite=None` attribute from cookies if a browser is known to not support it.</span></span> <span data-ttu-id="a80a8-196">Google 建议颁发双重 cookie，一个具有新属性，另一个不包含属性。</span><span class="sxs-lookup"><span data-stu-id="a80a8-196">Google's advice was to issue double cookies, one with the new attribute, and one without the attribute at all.</span></span> <span data-ttu-id="a80a8-197">但我们认为 Google 的建议有限。</span><span class="sxs-lookup"><span data-stu-id="a80a8-197">However we consider Google's advice limited.</span></span> <span data-ttu-id="a80a8-198">某些浏览器，尤其是移动浏览器对站点的 cookie 数的限制非常小，或者域名可以发送。</span><span class="sxs-lookup"><span data-stu-id="a80a8-198">Some browsers, especially mobile browsers have very small limits on the number of cookies a site, or a domain name can send.</span></span> <span data-ttu-id="a80a8-199">发送多个 cookie，尤其是大型 cookie （例如身份验证 cookie）会很快达到移动浏览器限制，从而导致难以诊断和修复的应用失败。</span><span class="sxs-lookup"><span data-stu-id="a80a8-199">Sending multiple cookies, especially large cookies like authentication cookies can reach the mobile browser limit very quickly, causing app failures that are hard to diagnose and fix.</span></span> <span data-ttu-id="a80a8-200">此外，作为一个框架，有一大一小部分第三方代码和组件可能未更新为使用 double cookie 方法。</span><span class="sxs-lookup"><span data-stu-id="a80a8-200">Furthermore as a framework there is a large ecosystem of third party code and components that may not be updated to use a double cookie approach.</span></span>

<span data-ttu-id="a80a8-201">[此 GitHub 存储库]()中的示例项目中使用的浏览器检测代码包含在两个文件中</span><span class="sxs-lookup"><span data-stu-id="a80a8-201">The browser detection code used in the sample projects in [this GitHub repository]() is contained in two files</span></span>

* [<span data-ttu-id="a80a8-202">C # SameSiteSupport.cs</span><span class="sxs-lookup"><span data-stu-id="a80a8-202">C# SameSiteSupport.cs</span></span>](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/SameSiteSupport.cs)
* [<span data-ttu-id="a80a8-203">VB SameSiteSupport</span><span class="sxs-lookup"><span data-stu-id="a80a8-203">VB SameSiteSupport.vb</span></span>](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/SameSiteSupport.vb)

<span data-ttu-id="a80a8-204">这些检测是我们所见到的最常见的浏览器代理，它支持2016标准，并且需要完全删除该属性。</span><span class="sxs-lookup"><span data-stu-id="a80a8-204">These detections are the most common browser agents we have seen that support the 2016 standard and for which the attribute needs to be completely removed.</span></span> <span data-ttu-id="a80a8-205">这并不是一种完整的实现方式：</span><span class="sxs-lookup"><span data-stu-id="a80a8-205">It isn't meant as a complete implementation:</span></span>

* <span data-ttu-id="a80a8-206">您的应用程序可能会看到我们的测试网站不提供的浏览器。</span><span class="sxs-lookup"><span data-stu-id="a80a8-206">Your app may see browsers that our test sites do not.</span></span>
* <span data-ttu-id="a80a8-207">应准备好根据环境需要添加检测。</span><span class="sxs-lookup"><span data-stu-id="a80a8-207">You should be prepared to add detections as necessary for your environment.</span></span>

<span data-ttu-id="a80a8-208">根据所使用的 .NET 版本和 web 框架的不同，检测检测的方式会有所不同。</span><span class="sxs-lookup"><span data-stu-id="a80a8-208">How you wire up the detection varies according the version of .NET and the web framework that you are using.</span></span> <span data-ttu-id="a80a8-209">可在 [HttpCookie](/dotnet/api/system.web.httpcookie) 调用站点调用以下代码：</span><span class="sxs-lookup"><span data-stu-id="a80a8-209">The following code can be called at the [HttpCookie](/dotnet/api/system.web.httpcookie) call site:</span></span>

[!code-csharp[](sample/SameSiteCheck.cs?name=snippet)]

<span data-ttu-id="a80a8-210">请参阅以下 ASP.NET 4.7.2 SameSite cookie 主题：</span><span class="sxs-lookup"><span data-stu-id="a80a8-210">See the following ASP.NET 4.7.2 SameSite cookie topics:</span></span>

* [<span data-ttu-id="a80a8-211">C# MVC</span><span class="sxs-lookup"><span data-stu-id="a80a8-211">C# MVC</span></span>](xref:samesite/csMVC)
* [<span data-ttu-id="a80a8-212">C# WebForms</span><span class="sxs-lookup"><span data-stu-id="a80a8-212">C# WebForms</span></span>](xref:samesite/CSharpWebForms)
* [<span data-ttu-id="a80a8-213">VB WebForms</span><span class="sxs-lookup"><span data-stu-id="a80a8-213">VB WebForms</span></span>](xref:samesite/vbWF)
* [<span data-ttu-id="a80a8-214">VB MVC</span><span class="sxs-lookup"><span data-stu-id="a80a8-214">VB MVC</span></span>](xref:samesite/vbMVC)
<!--
* <xref:samesite/csMVC>
* <xref:samesite/CSharpWebForms>
* <xref:samesite/vbWF>
* <xref:samesite/vbMVC>
-->

### <a name="ensuring-your-site-redirects-to-https"></a><span data-ttu-id="a80a8-215">确保你的网站重定向到 HTTPS</span><span class="sxs-lookup"><span data-stu-id="a80a8-215">Ensuring your site redirects to HTTPS</span></span>

<span data-ttu-id="a80a8-216">对于 ASP.NET 4.x、WebForms 和 MVC，可以使用 [IIS 的 URL 重写](/iis/extensions/url-rewrite-module/creating-rewrite-rules-for-the-url-rewrite-module) 功能将所有请求重定向到 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="a80a8-216">For ASP.NET 4.x, WebForms and MVC, [IIS's URL Rewrite](/iis/extensions/url-rewrite-module/creating-rewrite-rules-for-the-url-rewrite-module) feature can be used to redirect all requests to HTTPS.</span></span> <span data-ttu-id="a80a8-217">以下 XML 显示了一个示例规则：</span><span class="sxs-lookup"><span data-stu-id="a80a8-217">The following XML shows a sample rule:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
  <system.webServer>
    <rewrite>
      <rules>
        <rule name="Redirect to https" stopProcessing="true">
          <match url="(.*)"/>
          <conditions>
            <add input="{HTTPS}" pattern="Off"/>
            <add input="{REQUEST_METHOD}" pattern="^get$|^head$" />
          </conditions>
          <action type="Redirect" url="https://{HTTP_HOST}/{R:1}" redirectType="Permanent"/>
        </rule>
      </rules>
    </rewrite>
  </system.webServer>
</configuration>
```

<span data-ttu-id="a80a8-218">[IIS URL 重写](https://www.iis.net/downloads/microsoft/url-rewrite)的本地安装是一项可选功能，可能需要安装。</span><span class="sxs-lookup"><span data-stu-id="a80a8-218">In on-premises installations of [IIS URL Rewrite](https://www.iis.net/downloads/microsoft/url-rewrite) is an optional feature that may need installing.</span></span>

## <a name="test-apps-for-samesite-problems"></a><span data-ttu-id="a80a8-219">测试应用的 SameSite 问题</span><span class="sxs-lookup"><span data-stu-id="a80a8-219">Test apps for SameSite problems</span></span>

<span data-ttu-id="a80a8-220">必须使用支持的浏览器测试应用程序，并完成涉及 cookie 的方案。</span><span class="sxs-lookup"><span data-stu-id="a80a8-220">You must test your app with the browsers you support and go through your scenarios that involve cookies.</span></span> <span data-ttu-id="a80a8-221">Cookie 方案通常涉及</span><span class="sxs-lookup"><span data-stu-id="a80a8-221">Cookie scenarios typically involve</span></span>

* <span data-ttu-id="a80a8-222">登录窗体</span><span class="sxs-lookup"><span data-stu-id="a80a8-222">Login forms</span></span>
* <span data-ttu-id="a80a8-223">外部登录机制，如 Facebook、Azure AD、OAuth 和 OIDC</span><span class="sxs-lookup"><span data-stu-id="a80a8-223">External login mechanisms such as Facebook, Azure AD, OAuth and OIDC</span></span>
* <span data-ttu-id="a80a8-224">接受来自其他站点的请求的页面</span><span class="sxs-lookup"><span data-stu-id="a80a8-224">Pages that accept requests from other sites</span></span>
* <span data-ttu-id="a80a8-225">应用中旨在嵌入 iframe 的页面</span><span class="sxs-lookup"><span data-stu-id="a80a8-225">Pages in your app designed to be embedded in iframes</span></span>

<span data-ttu-id="a80a8-226">你应检查是否在应用中正确创建、保存并删除了 cookie。</span><span class="sxs-lookup"><span data-stu-id="a80a8-226">You should check that cookies are created, persisted and deleted correctly in your app.</span></span>

<span data-ttu-id="a80a8-227">与远程站点（如通过第三方登录）交互的应用需要：</span><span class="sxs-lookup"><span data-stu-id="a80a8-227">Apps that interact with remote sites such as through third-party login need to:</span></span>

* <span data-ttu-id="a80a8-228">测试多个浏览器上的交互。</span><span class="sxs-lookup"><span data-stu-id="a80a8-228">Test the interaction on multiple browsers.</span></span>
* <span data-ttu-id="a80a8-229">应用本文档中讨论的 [浏览器检测和缓解措施](#sob) 。</span><span class="sxs-lookup"><span data-stu-id="a80a8-229">Apply the [browser detection and mitigation](#sob) discussed in this document.</span></span>

<span data-ttu-id="a80a8-230">使用可选择新的 SameSite 行为的客户端版本测试 web 应用。</span><span class="sxs-lookup"><span data-stu-id="a80a8-230">Test web apps using a client version that can opt-in to the new SameSite behavior.</span></span> <span data-ttu-id="a80a8-231">Chrome、Firefox 和 Chromium Edge 都具有可用于测试的新的可选功能标志。</span><span class="sxs-lookup"><span data-stu-id="a80a8-231">Chrome, Firefox, and Chromium Edge all have new opt-in feature flags that can be used for testing.</span></span> <span data-ttu-id="a80a8-232">应用应用 SameSite 修补程序后，请对其进行测试，使其与早期版本的客户端版本（尤其是 Safari）</span><span class="sxs-lookup"><span data-stu-id="a80a8-232">After your app applies the SameSite patches, test it with older client versions, especially Safari.</span></span> <span data-ttu-id="a80a8-233">有关详细信息，请参阅本文档中的 [支持旧版浏览器](#sob) 。</span><span class="sxs-lookup"><span data-stu-id="a80a8-233">For more information, see [Supporting older browsers](#sob) in this document.</span></span>

### <a name="test-with-chrome"></a><span data-ttu-id="a80a8-234">用 Chrome 测试</span><span class="sxs-lookup"><span data-stu-id="a80a8-234">Test with Chrome</span></span>

<span data-ttu-id="a80a8-235">Chrome 78 + 提供了令人误解的结果，因为它具有临时的缓解措施。</span><span class="sxs-lookup"><span data-stu-id="a80a8-235">Chrome 78+ gives misleading results because it has a temporary mitigation in place.</span></span> <span data-ttu-id="a80a8-236">Chrome 78 + 暂时缓解功能允许 cookie 不到两分钟。</span><span class="sxs-lookup"><span data-stu-id="a80a8-236">The Chrome 78+ temporary mitigation allows cookies less than two minutes old.</span></span> <span data-ttu-id="a80a8-237">已启用适当测试标志的 Chrome 76 或77提供更准确的结果。</span><span class="sxs-lookup"><span data-stu-id="a80a8-237">Chrome 76 or 77 with the appropriate test flags enabled provides more accurate results.</span></span> <span data-ttu-id="a80a8-238">若要测试新的 SameSite 行为切换 `chrome://flags/#same-site-by-default-cookies` 为 **启用状态**。</span><span class="sxs-lookup"><span data-stu-id="a80a8-238">To test the new SameSite behavior toggle `chrome://flags/#same-site-by-default-cookies` to **Enabled**.</span></span> <span data-ttu-id="a80a8-239">旧版本的 Chrome (75 及更) 低版本将报告为失败，并出现新 `None` 设置。</span><span class="sxs-lookup"><span data-stu-id="a80a8-239">Older versions of Chrome (75 and below) are reported to fail with the new `None` setting.</span></span> <span data-ttu-id="a80a8-240">请参阅本文档中的 [支持旧版浏览器](#sob) 。</span><span class="sxs-lookup"><span data-stu-id="a80a8-240">See [Supporting older browsers](#sob) in this document.</span></span>

<span data-ttu-id="a80a8-241">Google 不会使旧版 chrome 版本可用。</span><span class="sxs-lookup"><span data-stu-id="a80a8-241">Google does not make older chrome versions available.</span></span> <span data-ttu-id="a80a8-242">遵循 [下载 Chromium](https://www.chromium.org/getting-involved/download-chromium) 中的说明来测试旧版 Chrome。</span><span class="sxs-lookup"><span data-stu-id="a80a8-242">Follow the instructions at [Download Chromium](https://www.chromium.org/getting-involved/download-chromium) to test older versions of Chrome.</span></span> <span data-ttu-id="a80a8-243">不要从通过搜索旧版 chrome 提供的 **链接下载 chrome** 。</span><span class="sxs-lookup"><span data-stu-id="a80a8-243">Do **not** download Chrome from links provided by searching for older versions of chrome.</span></span>

* [<span data-ttu-id="a80a8-244">Chromium 76 Win64</span><span class="sxs-lookup"><span data-stu-id="a80a8-244">Chromium 76 Win64</span></span>](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/664998/)
* [<span data-ttu-id="a80a8-245">Chromium 74 Win64</span><span class="sxs-lookup"><span data-stu-id="a80a8-245">Chromium 74 Win64</span></span>](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/638880/)
* <span data-ttu-id="a80a8-246">如果你不使用64位版本的 Windows，则可以使用 [OmahaProxy 查看器](https://omahaproxy.appspot.com/) 来查找与 Chrome 74 (v 74.0.3729.108) 对应的 Chromium 分支，并使用 [Chromium 提供的说明](https://www.chromium.org/getting-involved/download-chromium)。</span><span class="sxs-lookup"><span data-stu-id="a80a8-246">If you're not using a 64bit version of Windows you can use the [OmahaProxy viewer](https://omahaproxy.appspot.com/) to look up which Chromium branch corresponds to Chrome 74 (v74.0.3729.108) using the [instructions provided by Chromium](https://www.chromium.org/getting-involved/download-chromium).</span></span>

<span data-ttu-id="a80a8-247">从 "未完成" 的版本开始 `80.0.3975.0` ，可以使用新标志来禁用宽松的 + 后续暂时缓解，以 `--enable-features=SameSiteDefaultChecksMethodRigorously` 允许在删除缓解功能的最终状态下测试站点和服务。</span><span class="sxs-lookup"><span data-stu-id="a80a8-247">Starting in Canary version `80.0.3975.0`, the Lax+POST temporary mitigation can be disabled for testing purposes using the new flag `--enable-features=SameSiteDefaultChecksMethodRigorously` to allow testing of sites and services in the eventual end state of the feature where the mitigation has been removed.</span></span> <span data-ttu-id="a80a8-248">有关详细信息，请参阅 Chromium 项目 [SameSite Updates](https://www.chromium.org/updates/same-site)</span><span class="sxs-lookup"><span data-stu-id="a80a8-248">For more information, see The Chromium Projects [SameSite Updates](https://www.chromium.org/updates/same-site)</span></span>

#### <a name="test-with-chrome-80"></a><span data-ttu-id="a80a8-249">用 Chrome 80 + 测试</span><span class="sxs-lookup"><span data-stu-id="a80a8-249">Test with Chrome 80+</span></span>

<span data-ttu-id="a80a8-250">[下载](https://www.google.com/chrome/) 支持新属性的 Chrome 版本。</span><span class="sxs-lookup"><span data-stu-id="a80a8-250">[Download](https://www.google.com/chrome/) a version of Chrome that supports their new attribute.</span></span> <span data-ttu-id="a80a8-251">编写时，当前版本为 Chrome 80。</span><span class="sxs-lookup"><span data-stu-id="a80a8-251">At the time of writing, the current version is Chrome 80.</span></span> <span data-ttu-id="a80a8-252">Chrome 80 需要启用标志 `chrome://flags/#same-site-by-default-cookies` 才能使用新行为。</span><span class="sxs-lookup"><span data-stu-id="a80a8-252">Chrome 80 needs the flag `chrome://flags/#same-site-by-default-cookies` enabled to use the new behavior.</span></span> <span data-ttu-id="a80a8-253">还应启用 (`chrome://flags/#cookies-without-same-site-must-be-secure`) 来测试不启用 sameSite 属性的 cookie 的即将到来的行为。</span><span class="sxs-lookup"><span data-stu-id="a80a8-253">You should also enable (`chrome://flags/#cookies-without-same-site-must-be-secure`) to test the upcoming behavior for cookies which have no sameSite attribute enabled.</span></span> <span data-ttu-id="a80a8-254">Chrome 80 在目标上，使交换机不使用属性将 cookie 视为不是 `SameSite=Lax` ，但对于某些请求，会有一个超时宽限期。</span><span class="sxs-lookup"><span data-stu-id="a80a8-254">Chrome 80 is on target to make the switch to treat cookies without the attribute as `SameSite=Lax`, albeit with a timed grace period for certain requests.</span></span> <span data-ttu-id="a80a8-255">若要禁用定时宽限期，可以通过以下命令行参数启动 Chrome 80：</span><span class="sxs-lookup"><span data-stu-id="a80a8-255">To disable the timed grace period Chrome 80 can be launched with the following command line argument:</span></span>

`--enable-features=SameSiteDefaultChecksMethodRigorously`

<span data-ttu-id="a80a8-256">Chrome 80 在浏览器控制台中包含缺少 sameSite 属性的警告消息。</span><span class="sxs-lookup"><span data-stu-id="a80a8-256">Chrome 80 has warning messages in the browser console about missing sameSite attributes.</span></span> <span data-ttu-id="a80a8-257">使用 F12 打开浏览器控制台。</span><span class="sxs-lookup"><span data-stu-id="a80a8-257">Use F12 to open the browser console.</span></span>

### <a name="test-with-safari"></a><span data-ttu-id="a80a8-258">用 Safari 测试</span><span class="sxs-lookup"><span data-stu-id="a80a8-258">Test with Safari</span></span>

<span data-ttu-id="a80a8-259">Safari 12 严格实现了之前的草稿，在新 `None` 值在 cookie 中时失败。</span><span class="sxs-lookup"><span data-stu-id="a80a8-259">Safari 12 strictly implemented the prior draft and fails when the new `None` value is in a cookie.</span></span> <span data-ttu-id="a80a8-260">`None` 通过本文档中 [支持旧版浏览](#sob) 器的浏览器检测代码，避免了这种情况。</span><span class="sxs-lookup"><span data-stu-id="a80a8-260">`None` is avoided via the browser detection code [Supporting older browsers](#sob) in this document.</span></span> <span data-ttu-id="a80a8-261">使用 MSAL、ADAL 或所使用的任何库，测试 Safari 12、Safari 13 和基于 WebKit 的 OS 样式登录。</span><span class="sxs-lookup"><span data-stu-id="a80a8-261">Test Safari 12, Safari 13, and WebKit based OS style logins using MSAL, ADAL or whatever library you are using.</span></span> <span data-ttu-id="a80a8-262">问题取决于基础 OS 版本。</span><span class="sxs-lookup"><span data-stu-id="a80a8-262">The problem is dependent on the underlying OS version.</span></span> <span data-ttu-id="a80a8-263">已知 OSX Mojave (10.14) 和 iOS 12 与新的 SameSite 行为存在兼容性问题。</span><span class="sxs-lookup"><span data-stu-id="a80a8-263">OSX Mojave (10.14) and iOS 12 are known to have compatibility problems with the new SameSite behavior.</span></span> <span data-ttu-id="a80a8-264">将 OS 升级到 OSX Catalina (10.15) 或 iOS 13 修复了此问题。</span><span class="sxs-lookup"><span data-stu-id="a80a8-264">Upgrading the OS to OSX Catalina (10.15) or iOS 13 fixes the problem.</span></span> <span data-ttu-id="a80a8-265">Safari 当前没有用于测试新规范行为的选择标记。</span><span class="sxs-lookup"><span data-stu-id="a80a8-265">Safari does not currently have an opt-in flag for testing the new spec behavior.</span></span>

### <a name="test-with-firefox"></a><span data-ttu-id="a80a8-266">用 Firefox 测试</span><span class="sxs-lookup"><span data-stu-id="a80a8-266">Test with Firefox</span></span>

<span data-ttu-id="a80a8-267">可以在版本 68 + 上测试对新标准的 Firefox 支持，方法是在页面上选择 `about:config` 功能标志 `network.cookie.sameSite.laxByDefault` 。</span><span class="sxs-lookup"><span data-stu-id="a80a8-267">Firefox support for the new standard can be tested on version 68+ by opting in on the `about:config` page with the feature flag `network.cookie.sameSite.laxByDefault`.</span></span> <span data-ttu-id="a80a8-268">以前版本的 Firefox 没有出现兼容性问题的报告。</span><span class="sxs-lookup"><span data-stu-id="a80a8-268">There haven't been reports of compatibility issues with older versions of Firefox.</span></span>

### <a name="test-with-edge-legacy-browser"></a><span data-ttu-id="a80a8-269"> (旧) 浏览器进行测试</span><span class="sxs-lookup"><span data-stu-id="a80a8-269">Test with Edge (Legacy) browser</span></span>

<span data-ttu-id="a80a8-270">Edge 支持旧的 SameSite 标准。</span><span class="sxs-lookup"><span data-stu-id="a80a8-270">Edge supports the old SameSite standard.</span></span> <span data-ttu-id="a80a8-271">边缘版本 44 + 与新的标准没有任何已知的兼容性问题。</span><span class="sxs-lookup"><span data-stu-id="a80a8-271">Edge version 44+ doesn't have any known compatibility problems with the new standard.</span></span>

### <a name="test-with-edge-chromium"></a><span data-ttu-id="a80a8-272"> (Chromium 的边缘测试) </span><span class="sxs-lookup"><span data-stu-id="a80a8-272">Test with Edge (Chromium)</span></span>

<span data-ttu-id="a80a8-273">页面上设置了 SameSite 标志 `edge://flags/#same-site-by-default-cookies` 。</span><span class="sxs-lookup"><span data-stu-id="a80a8-273">SameSite flags are set on the `edge://flags/#same-site-by-default-cookies` page.</span></span> <span data-ttu-id="a80a8-274">未发现边缘 Chromium 的兼容性问题。</span><span class="sxs-lookup"><span data-stu-id="a80a8-274">No compatibility issues were discovered with Edge Chromium.</span></span>

### <a name="test-with-electron"></a><span data-ttu-id="a80a8-275">用 Electron 进行测试</span><span class="sxs-lookup"><span data-stu-id="a80a8-275">Test with Electron</span></span>

<span data-ttu-id="a80a8-276">Electron 的版本包括较早版本的 Chromium。</span><span class="sxs-lookup"><span data-stu-id="a80a8-276">Versions of Electron include older versions of Chromium.</span></span> <span data-ttu-id="a80a8-277">例如，团队使用的 Electron 版本为 Chromium 66，该版本展示了较旧的行为。</span><span class="sxs-lookup"><span data-stu-id="a80a8-277">For example, the version of Electron used by Teams is Chromium 66, which exhibits the older behavior.</span></span> <span data-ttu-id="a80a8-278">你必须使用你的产品使用的 Electron 版本执行你自己的兼容性测试。</span><span class="sxs-lookup"><span data-stu-id="a80a8-278">You must perform your own compatibility testing with the version of Electron your product uses.</span></span> <span data-ttu-id="a80a8-279">请参阅 [支持旧版浏览器](#sob)。</span><span class="sxs-lookup"><span data-stu-id="a80a8-279">See [Supporting older browsers](#sob).</span></span>

## <a name="reverting-samesite-patches"></a><span data-ttu-id="a80a8-280">恢复 SameSite 修补程序</span><span class="sxs-lookup"><span data-stu-id="a80a8-280">Reverting SameSite patches</span></span>

<span data-ttu-id="a80a8-281">您可以将 .NET Framework 应用程序中更新的 sameSite 行为还原为以前的行为，其中不会发出的值的 sameSite 属性 `None` ，而是将身份验证和会话 cookie 恢复为不发出该值。</span><span class="sxs-lookup"><span data-stu-id="a80a8-281">You can revert the updated sameSite behavior in .NET Framework apps to its previous behavior where the sameSite attribute is not emitted for a value of `None`, and revert the authentication and session cookies to not emit the value.</span></span> <span data-ttu-id="a80a8-282">这应作为一种 *极临时的修补程序*进行查看，因为 Chrome 更改会对使用支持标准更改的浏览器的用户中断任何外部 POST 请求或身份验证。</span><span class="sxs-lookup"><span data-stu-id="a80a8-282">This should be viewed as an *extremely temporary fix*, as the Chrome changes will break any external POST requests or authentication for users using browsers which support the changes to the standard.</span></span>

### <a name="reverting-net-472-behavior"></a><span data-ttu-id="a80a8-283">恢复 .NET 4.7.2 行为</span><span class="sxs-lookup"><span data-stu-id="a80a8-283">Reverting .NET 4.7.2 behavior</span></span>

<span data-ttu-id="a80a8-284">更新 *web.config* 以包含以下配置设置：</span><span class="sxs-lookup"><span data-stu-id="a80a8-284">Update *web.config* to include the following configuration settings:</span></span>

```xml
<configuration> 
  <appSettings>
    <add key="aspnet:SuppressSameSiteNone" value="true" />
  </appSettings>
 
  <system.web> 
    <authentication> 
      <forms cookieSameSite="None" /> 
    </authentication> 
    <sessionState cookieSameSite="None" /> 
  </system.web> 
</configuration>
```

## <a name="additional-resources"></a><span data-ttu-id="a80a8-285">其他资源</span><span class="sxs-lookup"><span data-stu-id="a80a8-285">Additional resources</span></span>

* [<span data-ttu-id="a80a8-286">即将推出 SameSite Cookie 更改 ASP.NET 和 ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="a80a8-286">Upcoming SameSite Cookie Changes in ASP.NET and ASP.NET Core</span></span>](https://devblogs.microsoft.com/aspnet/upcoming-samesite-cookie-changes-in-asp-net-and-asp-net-core/)
* [<span data-ttu-id="a80a8-287">SameSite 和 "SameSite = None" 测试和调试的提示安全 "cookie</span><span class="sxs-lookup"><span data-stu-id="a80a8-287">Tips for testing and debugging SameSite-by-default and “SameSite=None; Secure” cookies</span></span>](https://www.chromium.org/updates/same-site/test-debug)
* [<span data-ttu-id="a80a8-288">Chromium 博客：开发人员：准备好新 SameSite = 无;安全 Cookie 设置</span><span class="sxs-lookup"><span data-stu-id="a80a8-288">Chromium Blog:Developers: Get Ready for New SameSite=None; Secure Cookie Settings</span></span>](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)
* [<span data-ttu-id="a80a8-289">SameSite cookie 说明</span><span class="sxs-lookup"><span data-stu-id="a80a8-289">SameSite cookies explained</span></span>](https://web.dev/samesite-cookies-explained/)
* [<span data-ttu-id="a80a8-290">Chrome 更新</span><span class="sxs-lookup"><span data-stu-id="a80a8-290">Chrome Updates</span></span>](https://www.chromium.org/updates/same-site)
* [<span data-ttu-id="a80a8-291">.NET SameSite 修补程序</span><span class="sxs-lookup"><span data-stu-id="a80a8-291">.NET SameSite Patches</span></span>](/aspnet/samesite/kbs-samesite)
* [<span data-ttu-id="a80a8-292">Azure Web 应用程序相同站点信息</span><span class="sxs-lookup"><span data-stu-id="a80a8-292">Azure Web Applications Same Site Information</span></span>](https://azure.microsoft.com/updates/app-service-samesite-cookie-update/)
* [<span data-ttu-id="a80a8-293">Azure ActiveDirectory 相同站点信息</span><span class="sxs-lookup"><span data-stu-id="a80a8-293">Azure ActiveDirectory Same Site Information</span></span>](/azure/active-directory/develop/howto-handle-samesite-cookie-changes-chrome-browser)

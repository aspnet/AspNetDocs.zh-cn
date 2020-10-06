---
title: 在 ASP.NET 中使用 SameSite cookie
author: rick-anderson
description: 了解如何使用在 ASP.NET 中 SameSite cookie
ms.author: riande
ms.date: 2/15/2019
uid: samesite/system-web-samesite
ms.openlocfilehash: 2a39663dcbfa97ae441edd9a9768172cafbaab03
ms.sourcegitcommit: 09a34635ed0e74d6c2625f6a485c78f201c689ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/06/2020
ms.locfileid: "91763466"
---
# <a name="work-with-samesite-cookies-in-aspnet"></a>在 ASP.NET 中使用 SameSite cookie

作者：[Rick Anderson](https://twitter.com/RickAndMSFT)

SameSite 是一种 [IETF](https://ietf.org/about/) 草案标准，旨在针对跨站点请求伪造 (CSRF) 攻击提供一些保护。 最初在 [2016](https://tools.ietf.org/html/draft-west-first-party-cookies-07)中起草草案标准版已在 [2019](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00)中更新。 更新的标准与以前的标准不是向后兼容，以下是最明显的区别：

* 默认情况下，不带 SameSite 标头的 cookie 被视为 `SameSite=Lax` 。
* `SameSite=None` 必须使用以允许跨站点 cookie。
* 断言 `SameSite=None` 还必须标记为的 cookie `Secure` 。
* 使用的应用程序 [`<iframe>`](https://developer.mozilla.org/docs/Web/HTML/Element/iframe) 可能会遇到 `sameSite=Lax` 或 cookie 的问题， `sameSite=Strict` 因为 `<iframe>` 被视为跨站点方案。
* `SameSite=None` [2016 标准](https://tools.ietf.org/html/draft-west-first-party-cookies-07)不允许该值，并导致某些实现将此类 cookie 视为 `SameSite=Strict` 。 请参阅本文档中的 [支持旧版浏览器](#sob) 。

此 `SameSite=Lax` 设置适用于大多数应用程序 cookie。 某些形式的身份验证，例如 [OpenID connect](https://openid.net/connect/) (OIDC) ，并且 [WS 联合](https://auth0.com/docs/protocols/ws-fed) 身份验证默认为基于 POST 的重定向。 基于后期的重定向会触发 SameSite 浏览器保护，因此，对这些组件禁用了 SameSite。 由于请求的流动方式不同，大多数 [OAuth](https://oauth.net/) 登录名不受影响。

发出 cookie 的每个 ASP.NET 组件都需要确定 SameSite 是否适用。

在安装 2019 .Net SameSite 更新后，请参阅应用程序问题的 [已知问题](#known) 。

## <a name="using-samesite-in-aspnet-472-and-48"></a>在 ASP.NET 4.7.2 和4.8 中使用 SameSite

.Net 4.7.2 和4.8 支持 SameSite 的 [2019 草案标准](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00) ，因为年12月2019更新发布。 开发人员可以使用 [HttpCookie 属性](/dotnet/api/system.web.httpcookie.samesite#System_Web_HttpCookie_SameSite)以编程方式控制 SameSite 标头的值。 将 `SameSite` 属性设置为 `Strict` 、 `Lax` 或会 `None` 导致这些值用 cookie 写入网络。 如果将其设置为 "等于"，则 `(SameSiteMode)(-1)` 表示网络上不应包含带有 cookie 的 SameSite 标头。 [HttpCookie 属性](/dotnet/api/system.web.httpcookie.secure)（或配置文件中的 "requireSSL"）可用于将 cookie 标记为 `Secure` 。

新 `HttpCookie` 实例将默认为 `SameSite=(SameSiteMode)(-1)` 和 `Secure=false` 。 可以在配置节中重写这些默认值 `system.web/httpCookies` ，其中字符串 `"Unspecified"` 是适用于的友好仅配置语法 `(SameSiteMode)(-1)` ：

```xml
<configuration>
 <system.web>
  <httpCookies sameSite="[Strict|Lax|None|Unspecified]" requireSSL="[true|false]" />
 <system.web>
<configuration>
```

ASP.Net 还为这些功能颁发了自己的四个特定 cookie：匿名身份验证、Forms 身份验证、会话状态和角色管理。 可以使用和属性来操作在运行时中获得的这些 cookie 的实例 `SameSite` ， `Secure` 就像任何其他 HttpCookie 实例一样。 然而，由于 SameSite 标准的大杂烩出现，这四个功能 cookie 的配置选项不一致。 相关配置节和属性的默认值如下所示。 如果 `SameSite` 某个功能没有或 `Secure` 相关的属性，则该功能将回退前面讨论的部分中配置的默认值 `system.web/httpCookies` 。

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

**注意**：目前仅可使用 "未指定" `system.web/httpCookies@sameSite` 。 我们希望在以后的更新中，将类似语法添加到前面所示的 cookieSameSite 属性。 `(SameSiteMode)(-1)`代码中的设置仍适用于这些 cookie 的实例。 *

[!INCLUDE[](~/includes/MTcomments.md)]

<a name="retargeting"></a>

### <a name="retarget-net-apps"></a>重定目标 .NET 应用

面向 .NET 4.7.2 或更高版本：

* 确保 *web.config* 包含以下各项：  <!-- review, I removed `debug="true"` -->

  ```xml
  <system.web>
    <compilation targetFramework="4.7.2"/>
    <httpRuntime targetFramework="4.7.2"/>
  </system.web>

* Verify the project file contains the correct [TargetFrameworkVersion](/visualstudio/msbuild/msbuild-target-framework-and-target-platform?view=vs-2019):

  ```xml
  <TargetFrameworkVersion>v4.7.2</TargetFrameworkVersion>
  ```

  [.Net 迁移指南](/dotnet/framework/migration-guide/)提供了更多详细信息。

* 验证项目中的 NuGet 包的版本是否正确。 可以通过检查 *packages.config* 文件来验证正确的框架版本，例如：

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <packages>
    <package id="Microsoft.AspNet.Mvc" version="5.2.7" targetFramework="net472" />
    <package id="Microsoft.ApplicationInsights" version="2.4.0" targetFramework="net451" />
  </packages>
  ```

  在上述 *packages.config* 文件中， `Microsoft.ApplicationInsights` 包：
    * 面向 .NET 4.5.1。
    * 应将其 `targetFramework` 属性更新为， `net472` 前提是目标为框架目标的更新包已存在。

<a name="nope"></a>

### <a name="net-versions-earlier-than-472"></a>早于4.7.2 的 .NET 版本

Microsoft 不支持将4.7.2 用于写入同一站点 cookie 属性的 .NET 版本。 我们找不到一种可靠的方法来执行以下操作：

* 确保根据浏览器版本正确写入特性。
* 在旧版本的 framework 上拦截并调整身份验证和会话 cookie。

### <a name="december-patch-behavior-changes"></a>12月修补程序行为更改

.NET Framework 的特定行为更改是 `SameSite` 属性如何解释 `None` 值：

* 在修补程序的值为之前 `None` ：
  * 根本不发出属性。
* 修补后：
  * 如果值为， `None` 则表示 "发出属性，其值为 `None` "。
  * `SameSite`值为将 `(SameSiteMode)(-1)` 导致不发出属性。

Forms 身份验证和会话状态 cookie 的默认 SameSite 值从更改 `None` 为 `Lax` 。

### <a name="summary-of-change-impact-on-browsers"></a>更改对浏览器的影响

如果安装修补程序并使用发出 cookie，则 `SameSite.None` 将发生以下两种情况之一：
* Chrome v80 将根据新的实现来处理此 cookie，而不会对 cookie 强制实施相同的站点限制。
* 尚未更新以支持新实现的任何浏览器都将遵循旧实现。 旧实现显示：
  * 如果你看到不了解的值，请将其忽略，并切换到严格相同的站点限制。

这样，应用程序就可以在 Chrome 中中断，也可以在很多其他地方中断。

## <a name="history-and-changes"></a>历史记录和更改

SameSite 支持是在使用 [2016 草案标准](https://tools.ietf.org/html/draft-west-first-party-cookies-07#section-4.1)的 .net 4.7.2 中首次实现的。

2019年11月19日更新了 Windows 更新后的 .NET 4.7.2 + 2016 标准版和2019标准版。 其他版本的 Windows 即将推出其他更新。 有关详细信息，请参阅 <xref:samesite/kbs-samesite>。

 SameSite 规范的2019草案：

* **不**向后兼容2016草案。 有关详细信息，请参阅本文档中的 [支持旧版浏览器](#sob) 。
* 指定 `SameSite=Lax` 按默认值处理 cookie。
* 指定显式断言以便 `SameSite=None` 启用跨站点传递的 cookie 也应该标记为 `Secure` 。
* 按照上面列出的 KB 中所述，发布的修补程序支持。
* 默认 [情况下，计划](https://chromestatus.com/feature/5088147346030592) 在 [2020 年2月](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)启用。 浏览器已开始在2019中移动到此标准。

<a name="known"></a>

## <a name="known-issues"></a>已知问题

因为2016和2019草案规范不兼容，所以，11月 2019 .Net Framework 更新引入了一些可能会中断的更改。

* 会话状态和窗体身份验证 cookie 现在会写入网络， `Lax` 而不是未指定。
  * 大多数应用程序使用 `SameSite=Lax` cookie 时，通过在使用的站点或应用程序中发布的应用程序 `iframe` 可能会发现其会话状态或窗体授权 cookie 没有按预期方式使用。 若要解决此情况，请 `cookieSameSite` 在前面所述的相应配置节中更改值。
* `SameSite=None`在代码或配置中显式设置的 HttpCookies 现在将使用 cookie 写入该值，而以前省略了该值。 这可能会导致旧版浏览器出现一些仅支持2016草案标准的问题。
  * 如果面向的浏览器支持2019草案 standard with `SameSite=None` cookie，请记住也要将其标记为 `Secure` 或无法识别。
  * 若要恢复为2016的不写入行为 `SameSite=None` ，请使用应用设置 `aspnet:SupressSameSiteNone=true` 。 请注意，这将适用于应用中的所有 HttpCookies。

### <a name="azure-app-servicesamesite-cookie-handling"></a>Azure App Service — SameSite cookie 处理

请参阅 [Azure App Service-SameSite cookie 处理和 .NET Framework 4.7.2 修补程序](https://azure.microsoft.com/updates/app-service-samesite-cookie-update/) ，以获取有关 Azure App Service 如何在 .net 4.7.2 apps 中配置 SameSite 行为的信息。

<a name="sob"></a>

## <a name="supporting-older-browsers"></a>支持旧版浏览器

2016 SameSite 标准规定，未知值必须被视为 `SameSite=Strict` 值。 从支持 2016 SameSite 标准的旧版浏览器访问的应用在收到值为的 SameSite 属性时可能会中断 `None` 。 如果 Web 应用要支持较旧的浏览器，则必须实现浏览器检测。 ASP.NET 不实现浏览器检测，因为用户代理值非常不稳定，并且经常更改。

Microsoft 解决该问题的方法是帮助您实现浏览器检测组件，以便在 `sameSite=None` 浏览器不支持时从 cookie 中去除属性。 Google 建议颁发双重 cookie，一个具有新属性，另一个不包含属性。 但我们认为 Google 的建议有限。 某些浏览器，尤其是移动浏览器对站点的 cookie 数的限制非常小，或者域名可以发送。 发送多个 cookie，尤其是大型 cookie （例如身份验证 cookie）会很快达到移动浏览器限制，从而导致难以诊断和修复的应用失败。 此外，作为一个框架，有一大一小部分第三方代码和组件可能未更新为使用 double cookie 方法。

[此 GitHub 存储库]()中的示例项目中使用的浏览器检测代码包含在两个文件中

* [C # SameSiteSupport.cs](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/SameSiteSupport.cs)
* [VB SameSiteSupport](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/SameSiteSupport.vb)

这些检测是我们所见到的最常见的浏览器代理，它支持2016标准，并且需要完全删除该属性。 这并不是一种完整的实现方式：

* 您的应用程序可能会看到我们的测试网站不提供的浏览器。
* 应准备好根据环境需要添加检测。

根据所使用的 .NET 版本和 web 框架的不同，检测检测的方式会有所不同。 可在 [HttpCookie](/dotnet/api/system.web.httpcookie) 调用站点调用以下代码：

[!code-csharp[](sample/SameSiteCheck.cs?name=snippet)]

请参阅以下 ASP.NET 4.7.2 SameSite cookie 主题：

* [C# MVC](xref:samesite/csMVC)
* [C# WebForms](xref:samesite/CSharpWebForms)
* [VB WebForms](xref:samesite/vbWF)
* [VB MVC](xref:samesite/vbMVC)
<!--
* <xref:samesite/csMVC>
* <xref:samesite/CSharpWebForms>
* <xref:samesite/vbWF>
* <xref:samesite/vbMVC>
-->

### <a name="ensuring-your-site-redirects-to-https"></a>确保你的网站重定向到 HTTPS

对于 ASP.NET 4.x、WebForms 和 MVC，可以使用 [IIS 的 URL 重写](/iis/extensions/url-rewrite-module/creating-rewrite-rules-for-the-url-rewrite-module) 功能将所有请求重定向到 HTTPS。 以下 XML 显示了一个示例规则：

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

[IIS URL 重写](https://www.iis.net/downloads/microsoft/url-rewrite)的本地安装是一项可选功能，可能需要安装。

## <a name="test-apps-for-samesite-problems"></a>测试应用的 SameSite 问题

必须使用支持的浏览器测试应用程序，并完成涉及 cookie 的方案。 Cookie 方案通常涉及

* 登录窗体
* 外部登录机制，如 Facebook、Azure AD、OAuth 和 OIDC
* 接受来自其他站点的请求的页面
* 应用中旨在嵌入 iframe 的页面

你应检查是否在应用中正确创建、保存并删除了 cookie。

与远程站点（如通过第三方登录）交互的应用需要：

* 测试多个浏览器上的交互。
* 应用本文档中讨论的 [浏览器检测和缓解措施](#sob) 。

使用可选择新的 SameSite 行为的客户端版本测试 web 应用。 Chrome、Firefox 和 Chromium Edge 都具有可用于测试的新的可选功能标志。 应用应用 SameSite 修补程序后，请对其进行测试，使其与早期版本的客户端版本（尤其是 Safari） 有关详细信息，请参阅本文档中的 [支持旧版浏览器](#sob) 。

### <a name="test-with-chrome"></a>用 Chrome 测试

Chrome 78 + 提供了令人误解的结果，因为它具有临时的缓解措施。 Chrome 78 + 暂时缓解功能允许 cookie 不到两分钟。 已启用适当测试标志的 Chrome 76 或77提供更准确的结果。 若要测试新的 SameSite 行为切换 `chrome://flags/#same-site-by-default-cookies` 为 **启用状态**。 旧版本的 Chrome (75 及更) 低版本将报告为失败，并出现新 `None` 设置。 请参阅本文档中的 [支持旧版浏览器](#sob) 。

Google 不会使旧版 chrome 版本可用。 遵循 [下载 Chromium](https://www.chromium.org/getting-involved/download-chromium) 中的说明来测试旧版 Chrome。 不要从通过搜索旧版 chrome 提供的 **链接下载 chrome** 。

* [Chromium 76 Win64](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/664998/)
* [Chromium 74 Win64](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/638880/)
* 如果你不使用64位版本的 Windows，则可以使用 [OmahaProxy 查看器](https://omahaproxy.appspot.com/) 来查找与 Chrome 74 (v 74.0.3729.108) 对应的 Chromium 分支，并使用 [Chromium 提供的说明](https://www.chromium.org/getting-involved/download-chromium)。

从 "未完成" 的版本开始 `80.0.3975.0` ，可以使用新标志来禁用宽松的 + 后续暂时缓解，以 `--enable-features=SameSiteDefaultChecksMethodRigorously` 允许在删除缓解功能的最终状态下测试站点和服务。 有关详细信息，请参阅 Chromium 项目 [SameSite Updates](https://www.chromium.org/updates/same-site)

#### <a name="test-with-chrome-80"></a>用 Chrome 80 + 测试

[下载](https://www.google.com/chrome/) 支持新属性的 Chrome 版本。 编写时，当前版本为 Chrome 80。 Chrome 80 需要启用标志 `chrome://flags/#same-site-by-default-cookies` 才能使用新行为。 还应启用 (`chrome://flags/#cookies-without-same-site-must-be-secure`) 来测试不启用 sameSite 属性的 cookie 的即将到来的行为。 Chrome 80 在目标上，使交换机不使用属性将 cookie 视为不是 `SameSite=Lax` ，但对于某些请求，会有一个超时宽限期。 若要禁用定时宽限期，可以通过以下命令行参数启动 Chrome 80：

`--enable-features=SameSiteDefaultChecksMethodRigorously`

Chrome 80 在浏览器控制台中包含缺少 sameSite 属性的警告消息。 使用 F12 打开浏览器控制台。

### <a name="test-with-safari"></a>用 Safari 测试

Safari 12 严格实现了之前的草稿，在新 `None` 值在 cookie 中时失败。 `None` 通过本文档中 [支持旧版浏览](#sob) 器的浏览器检测代码，避免了这种情况。 使用 MSAL、ADAL 或所使用的任何库，测试 Safari 12、Safari 13 和基于 WebKit 的 OS 样式登录。 问题取决于基础 OS 版本。 已知 OSX Mojave (10.14) 和 iOS 12 与新的 SameSite 行为存在兼容性问题。 将 OS 升级到 OSX Catalina (10.15) 或 iOS 13 修复了此问题。 Safari 当前没有用于测试新规范行为的选择标记。

### <a name="test-with-firefox"></a>用 Firefox 测试

可以在版本 68 + 上测试对新标准的 Firefox 支持，方法是在页面上选择 `about:config` 功能标志 `network.cookie.sameSite.laxByDefault` 。 以前版本的 Firefox 没有出现兼容性问题的报告。

### <a name="test-with-edge-legacy-browser"></a> (旧) 浏览器进行测试

Edge 支持旧的 SameSite 标准。 边缘版本 44 + 与新的标准没有任何已知的兼容性问题。

### <a name="test-with-edge-chromium"></a> (Chromium 的边缘测试) 

页面上设置了 SameSite 标志 `edge://flags/#same-site-by-default-cookies` 。 未发现边缘 Chromium 的兼容性问题。

### <a name="test-with-electron"></a>用 Electron 进行测试

Electron 的版本包括较早版本的 Chromium。 例如，团队使用的 Electron 版本为 Chromium 66，该版本展示了较旧的行为。 你必须使用你的产品使用的 Electron 版本执行你自己的兼容性测试。 请参阅 [支持旧版浏览器](#sob)。

## <a name="reverting-samesite-patches"></a>恢复 SameSite 修补程序

您可以将 .NET Framework 应用程序中更新的 sameSite 行为还原为以前的行为，其中不会发出的值的 sameSite 属性 `None` ，而是将身份验证和会话 cookie 恢复为不发出该值。 这应作为一种 *极临时的修补程序*进行查看，因为 Chrome 更改会对使用支持标准更改的浏览器的用户中断任何外部 POST 请求或身份验证。

### <a name="reverting-net-472-behavior"></a>恢复 .NET 4.7.2 行为

更新 *web.config* 以包含以下配置设置：

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

## <a name="additional-resources"></a>其他资源

* [即将推出 SameSite Cookie 更改 ASP.NET 和 ASP.NET Core](https://devblogs.microsoft.com/aspnet/upcoming-samesite-cookie-changes-in-asp-net-and-asp-net-core/)
* [SameSite 和 "SameSite = None" 测试和调试的提示安全 "cookie](https://www.chromium.org/updates/same-site/test-debug)
* [Chromium 博客：开发人员：准备好新 SameSite = 无;安全 Cookie 设置](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)
* [SameSite cookie 说明](https://web.dev/samesite-cookies-explained/)
* [Chrome 更新](https://www.chromium.org/updates/same-site)
* [.NET SameSite 修补程序](/aspnet/samesite/kbs-samesite)
* [Azure Web 应用程序相同站点信息](https://azure.microsoft.com/updates/app-service-samesite-cookie-update/)
* [Azure ActiveDirectory 相同站点信息](/azure/active-directory/develop/howto-handle-samesite-cookie-changes-chrome-browser)

---
uid: mvc/overview/security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages
title: ASP.NET MVC 和网页中的 XSRF/CSRF 防护 |Microsoft Docs
author: Rick-Anderson
description: 跨站点请求伪造 (也称为 XSRF 或 CSRF) 对 web 托管的应用程序的攻击，恶意网站可能会影响 interacti .。。
ms.author: riande
ms.date: 03/14/2013
ms.assetid: aadc5fa4-8215-4fc7-afd5-bcd2ef879728
msc.legacyurl: /mvc/overview/security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages
msc.type: authoredcontent
ms.openlocfilehash: 7c45e342bc55ece3a6b41dcc42a0f33cd3eceffd
ms.sourcegitcommit: 4b78855427f1397df0a7be3559e04ec94a78c308
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/25/2020
ms.locfileid: "96151872"
---
# <a name="xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages"></a>ASP.NET MVC 和网页中的 XSRF/CSRF 防护

作者： [Rick Anderson](https://twitter.com/RickAndMSFT)

> 跨站点请求伪造（也称为 XSRF 或 CSRF）是一种针对 Web 托管型应用程序的攻击，恶意网站凭此可以影响客户端浏览器与受该浏览器信任的网站之间的交互。 这些攻击出现的原因可能是 Web 浏览器针对每一个对网站的请求自动发送身份验证令牌。 典型示例是身份验证 cookie，如 ASP.NET 的表单身份验证票证。 然而，使用任何持久身份验证（如 Windows Authentication、Basic 等）的网站也可能成为受攻击目标。
> 
> XSRF 攻击不同于网络钓鱼攻击。 网络钓鱼攻击需要与受害者进行交互。 在网络钓鱼攻击中，恶意网站将仿冒目标网站，受到欺骗的受害者会向攻击者提供敏感信息。 在 XSRF 攻击中，通常不必与受害者进行交互。 相反，浏览器自动向目标网站发送所有相关 cookie 为攻击者提供了可乘之机。
> 
> 有关详细信息，请参阅 [打开 Web 应用程序安全项目](https://www.owasp.org/index.php/Main_Page) (OWASP) [XSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF))。

## <a name="anatomy-of-an-attack"></a>攻击剖析

若要演练 XSRF 攻击，请考虑要执行一些在线银行交易的用户。 此用户先访问 WoodgroveBank.com 并登录，此时响应标头将包含她的身份验证 cookie：

[!code-console[Main](xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages/samples/sample1.cmd)]

因为身份验证 cookie 是会话 cookie，浏览器在浏览器进程退出时会自动将其清除。 但在此之前，浏览器将自动在每个请求中包括 cookie 和 WoodgroveBank.com。 用户现在想要将 $1000 传输到另一个帐户，因此她在银行站点上填写表单，浏览器向服务器发出此请求：

[!code-console[Main](xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages/samples/sample2.cmd)]

由于此操作在启动货币交易)  (有副作用，因此银行站点已选择要求 HTTP POST 以便启动此操作。 服务器从请求中读取身份验证令牌，查找当前用户的帐号，验证是否存在足够的资金，然后启动该事务进入目标帐户。

她的在线银行完成后，用户离开银行网站并访问 web 上的其他位置。 其中一个站点– fabrikam.com –在某个已嵌入到 iframe 中的页面上包含以下标记 &lt; &gt; ：

[!code-html[Main](xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages/samples/sample3.html)]

然后，它将导致浏览器发出此请求：

[!code-console[Main](xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages/samples/sample4.cmd)]

攻击者利用这一事实，用户可能仍具有适用于目标网站的有效身份验证令牌，而她使用 Javascript 的小片段来使浏览器自动向目标站点发出 HTTP POST。 如果身份验证令牌仍然有效，银行站点将启动 $250 到攻击者选择的帐户的传输。

### <a name="ineffective-mitigations"></a>低效缓解

请注意，在上面的方案中，WoodgroveBank.com 是通过 SSL 访问的，并且只有仅限 SSL 的身份验证 cookie，才能阻止攻击。 攻击者可以在她的 form 元素中指定 [URI 方案](http://en.wikipedia.org/wiki/URI_scheme) (https &lt;) &gt; ，浏览器将继续将未过期的 cookie 发送到目标站点，前提是这些 cookie 与目标站点的 uri 方案一致。

用户可能会认为，用户只应不访问不受信任的站点，因为仅访问可信网站有助于保持联机安全。 这一点很有意义，但遗憾的是，这一建议并不总是可行。 用户可能会 "信任" 本地新闻站点 ConsolidatedMessenger.com 并转而改为访问该站点，但该站点会提供 XSS 漏洞，使攻击者可以注入在 fabrikam.com 上运行的相同代码片段。

可以验证传入请求是否具有引用域的 [Referer 标头](http://www.w3.org/Protocols/HTTP/HTRQ_Headers.html#z14) 。 这将停止从第三方域中无意提交的请求。 但有些人出于隐私原因禁用了其浏览器的 Referer 标头，如果受害者安装了某些不安全的软件，攻击者有时会欺骗该标头。 验证 [Referer 标头](http://www.w3.org/Protocols/HTTP/HTRQ_Headers.html#z14) 不会被视为阻止 XSRF 攻击的安全方法。

## <a name="web-stack-runtime-xsrf-mitigations"></a>Web Stack 运行时 XSRF 缓解

ASP.NET Web Stack 运行时使用 [同步器令牌模式](https://cheatsheetseries.owasp.org/cheatsheets/Cross-Site_Request_Forgery_Prevention_Cheat_Sheet.html#synchronizer-token-pattern) 的变体来防御 XSRF 攻击。 同步令牌模式的一般形式是将两个 XSRF 令牌提交给服务器，其中每个 HTTP POST (除了身份验证令牌) ：一个令牌作为 cookie，另一个作为窗体值。 ASP.NET 运行时生成的令牌值不是由攻击者确定的，也不是可预测的。 提交令牌后，服务器将仅在两个令牌通过比较检查时才允许请求继续。

XSRF 请求验证 *会话令牌* 存储为 HTTP cookie，当前在其负载中包含以下信息：

- 安全令牌，由随机的128位标识符组成。   
 下图显示了使用 Internet Explorer F12 开发人员工具显示的 XSRF 请求验证会话令牌： (注意这是当前的实现，甚至可能会发生更改。 ) 

![](xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages/_static/image1.png)

*字段标记* 存储为 `<input type="hidden" />` ，在其有效负载中包含以下信息：

- 已登录用户的用户名 (如果经过身份验证) 。
- [IAntiForgeryAdditionalDataProvider](https://msdn.microsoft.com/library/system.web.helpers.iantiforgeryadditionaldataprovider(v=vs.111).aspx)提供的任何其他数据。

防 XSRF 令牌的负载经过加密和签名，因此使用工具检查令牌时，无法查看用户名。 如果 web 应用程序面向 ASP.NET 4.0，则 [MachineKey](https://msdn.microsoft.com/library/system.web.security.machinekey.encode.aspx) 例程会提供加密服务。 当 web 应用程序面向 ASP.NET 4.5 或更高版本时，会通过 [MachineKey](https://msdn.microsoft.com/library/system.web.security.machinekey.protect(v=vs.110)) 例程提供加密服务，从而提供更好的性能、扩展性和安全性。 有关更多详细信息，请参阅以下博客文章：

- [ASP.NET 4.5，pt 中的加密改进](https://blogs.msdn.com/b/webdev/archive/2012/10/22/cryptographic-improvements-in-asp-net-4-5-pt-1.aspx)
- [ASP.NET 4.5，pt 中的加密改进](https://blogs.msdn.com/b/webdev/archive/2012/10/23/cryptographic-improvements-in-asp-net-4-5-pt-2.aspx)
- [ASP.NET 4.5，pt 中的加密改进](https://blogs.msdn.com/b/webdev/archive/2012/10/24/cryptographic-improvements-in-asp-net-4-5-pt-3.aspx)

## <a name="generating-the-tokens"></a>生成令牌

若要生成 XSRF 标记，请 [@Html.AntiForgeryToken](https://msdn.microsoft.com/library/dd470175.aspx) 从 MVC 视图调用方法，或 @AntiForgery.GetHtml 从 Razor 页面中 ( # A1。 运行时将执行以下步骤：

1. 如果当前 HTTP 请求已经包含 XSRF 会话令牌 (XSRF cookie \_ \_ RequestVerificationToken) ，则将从该令牌中提取安全令牌。 如果 HTTP 请求不包含 XSRF 会话令牌，或如果提取安全令牌失败，将生成一个新的随机反 XSRF 令牌。
2. 将使用上述步骤 (1) 中的安全令牌和当前已登录用户的标识生成反 XSRF 字段令牌。  (有关确定用户标识的详细信息，请参阅下面的 " **[使用特殊支持的方案](#_Scenarios_with_special)** " 部分 ) 。此外，如果配置了 [IAntiForgeryAdditionalDataProvider](https://msdn.microsoft.com/library/jj158328(v=vs.111).aspx) ，则运行时将调用其 [GetAdditionalData](https://msdn.microsoft.com/library/system.web.helpers.iantiforgeryadditionaldataprovider.getadditionaldata(v=vs.111).aspx) 方法，并将返回的字符串包含在字段标记中。 有关详细信息，请参阅 **[配置和扩展性](#_Configuration_and_extensibility)** 部分 () 
3. 如果在步骤 (1) 中生成了新的 XSRF 令牌，则将创建一个新的会话令牌来包含该令牌，并将其添加到出站 HTTP cookie 集合中。 步骤 (2) 中的字段标记将被包装在 `<input type="hidden" />` 元素中，此 HTML 标记将为或的返回值 `Html.AntiForgeryToken()` `AntiForgery.GetHtml()` 。

## <a name="validating-the-tokens"></a>验证令牌

若要验证传入的 XSRF 令牌，开发人员需要在其 MVC 操作或控制器上包含 [ValidateAntiForgeryToken](https://msdn.microsoft.com/library/system.web.mvc.validateantiforgerytokenattribute(VS.108).aspx) 属性，或 `@AntiForgery.Validate()` 从她的 Razor 页面调用。 运行时将执行以下步骤：

1. 读取传入会话令牌和字段令牌，并从每个会话中提取 XSRF 标记。 XSRF 令牌必须与生成例程中的每个步骤 (2) 相同。
2. 如果对当前用户进行身份验证，则会将她的用户名与存储在字段令牌中的用户名进行比较。 用户名必须匹配。
3. 如果配置了 [IAntiForgeryAdditionalDataProvider](https://msdn.microsoft.com/library/system.web.helpers.iantiforgeryadditionaldataprovider(v=vs.111).aspx) ，则运行时将调用其 *ValidateAdditionalData* 方法。 方法必须返回布尔值 *true*。

如果验证成功，则允许请求继续。 如果验证失败，框架将引发 *HttpAntiForgeryException*。

## <a name="failure-conditions"></a>失败条件

从 ASP.NET Web Stack 运行时 v2 开始，验证期间引发的任何 *HttpAntiForgeryException* 都将包含有关错误的详细信息。 当前定义的故障条件如下：

- 请求中不存在会话令牌或窗体令牌。
- 无法读取会话令牌或窗体令牌。 最可能的原因是运行了不匹配的 ASP.NET Web Stack 运行时版本或场，其中 &lt; &gt; Web.config 计算机之间的 machineKey 元素不同。 可以使用 Fiddler 之类的工具通过篡改反 XSRF 标记来强制此异常。
- 已交换会话令牌和字段令牌。
- 会话令牌和字段令牌包含不匹配的安全令牌。
- 嵌入在字段令牌中的用户名与当前已登录用户的用户名不匹配。
- *[IAntiForgeryAdditionalDataProvider. ValidateAdditionalData](https://msdn.microsoft.com/library/system.web.helpers.iantiforgeryadditionaldataprovider.validateadditionaldata(v=vs.111).aspx)* 方法返回 *false*。

XSRF 设施还可以在令牌生成或验证过程中执行额外检查，这些检查过程中的故障可能会导致引发异常。 有关详细信息，请参阅 [WIF/ACS/基于声明的身份验证](#_WIF_ACS) 和 **[配置和扩展性](#_Configuration_and_extensibility)** 部分。

<a id="_Scenarios_with_special"></a>

## <a name="scenarios-with-special-support"></a>具有特殊支持的方案

### <a name="anonymous-authentication"></a>匿名身份验证

反 XSRF 系统包含对匿名用户的特殊支持，其中 "anonymous" 被定义为用户，其中 *IIdentity. IsAuthenticated* 属性返回 *false*。 方案包括在对用户进行身份验证之前 (向登录页提供 XSRF 保护) 和自定义身份验证方案，其中应用程序使用 *IIdentity* 以外的机制来标识用户。

若要支持这些方案，请记住，通过安全令牌（即，128位随机生成的不透明标识符）来联接会话和字段令牌。 此安全令牌用于在用户导航站点时跟踪单个用户的会话，因此它有效地充当了匿名标识符的用途。 空字符串用于替代上述生成和验证例程的用户名。

<a id="_WIF_ACS"></a>

### <a name="wif--acs--claims-based-authentication"></a>WIF/ACS/基于声明的身份验证

通常，内置于 .NET Framework 中的 *IIdentity* 类具有 *IIdentity.Name* 足够的属性，用于唯一标识特定应用程序内的特定用户。 例如， *FormsIdentity.Name* 返回存储在成员资格数据库中的用户名 (这对于所有应用程序都是唯一的，具体取决于该数据库) ， *WindowsIdentity.Name* 返回用户的域限定标识，依此类推。 这些系统不仅提供身份验证;它们还会将用户 *标识* 到应用程序。

另一方面，基于声明的身份验证不一定需要标识特定用户。 相反， *ClaimsPrincipal* 和 *ClaimsIdentity* 类型与 *声明* 实例集相关联，其中单个声明可能为 "为 18 + 岁以上，或对任何其他内容是管理员"。 由于用户不必进行标识，因此运行时无法将 *ClaimsIdentity.Name* 属性用作此特定用户的唯一标识符。 此团队已经了解了真实的示例，其中 *ClaimsIdentity.Name* 返回 *null*、返回友好 (显示) 名称，或者返回一个不适合用作用户的唯一标识符的字符串。

使用基于声明的身份验证的许多部署都 (ACS) 使用 [Azure 访问控制服务](https://msdn.microsoft.com/library/windowsazure/gg429786.aspx) 。 ACS 允许开发人员配置单个 *标识提供者* (例如 ADFS、Microsoft 帐户提供程序、OpenID 提供程序（例如 yahoo！）等 ) ，标识提供程序将返回 *名称标识符*。 这些名称标识符可能包含 (PII) 的个人身份信息（如电子邮件地址），也可能匿名，如专用个人标识符 (PPID) 。 无论如何，元组 (标识提供者、名称标识符) 在用户浏览站点时都可以作为特定用户的相应跟踪令牌，因此，ASP.NET Web Stack 运行时可以使用元组来代替用户名，同时生成和验证反 XSRF 字段标记。 标识提供程序和名称标识符的特定 Uri 为：

- `https://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider`
- `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier`

有关详细信息，请 (参阅此 [ACS 文档页](https://msdn.microsoft.com/library/windowsazure/gg185971.aspx) 。 ) 

生成或验证令牌时，ASP.NET Web Stack 运行时将在运行时尝试绑定到类型：

- `Microsoft.IdentityModel.Claims.IClaimsIdentity, Microsoft.IdentityModel, Version=3.5.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35` WIF SDK (。 ) 
- `System.Security.Claims.ClaimsIdentity` 适用于 .NET 4.5) 的 (。

如果这些类型存在，并且如果当前用户的 *IIIIdentity* 实现或子类其中一种类型，则在生成和验证令牌时，反 XSRF 设施将使用 (标识提供者、名称标识符) 元组代替用户名。 如果不存在这样的元组，则该请求将失败，并显示一条错误，指出开发人员如何配置反 XSRF 系统以了解所使用的特定于声明的特定身份验证机制。 有关详细信息，请参阅 **[配置和扩展性](#_Configuration_and_extensibility)** 部分。

### <a name="oauth--openid-authentication"></a>OAuth/OpenID 身份验证

最后，XSRF 工具对使用 OAuth 或 OpenID 身份验证的应用程序有特殊支持。 此支持基于试探法：如果当前 *IIdentity.Name* 以 http://或 https://开头，则将使用序号比较器而不是默认的 stringcomparison.ordinalignorecase 比较器来完成用户名比较。

<a id="_Configuration_and_extensibility"></a>

## <a name="configuration-and-extensibility"></a>配置和扩展性

有时，开发人员可能希望更严格地控制反 XSRF 生成和验证行为。 例如，可能不需要 MVC 和 Web Pages 助手的默认行为自动将 HTTP cookie 添加到响应中，开发人员可能希望将令牌保存在其他位置。 有两个 Api 可帮助解决此操作：

`AntiForgery.GetTokens(string oldCookieToken, out string newCookieToken, out string formToken);`  
`AntiForgery.Validate(string cookieToken, string formToken);`

*GetTokens* 方法将现有的 XSRF 请求验证会话令牌作为输入 (，这可能为 null) ，并生成一个新的 XSRF 请求验证会话令牌和字段令牌作为输出。 标记只是不透明的字符串，无修饰;实例的 *formToken* 值将不会包装在 &lt; 输入标记中 &gt; 。 *NewCookieToken* 值可以为 null;如果出现这种情况，则 *oldCookieToken* 值仍然有效，无需设置新的响应 cookie。 *GetTokens* 的调用方负责持久保存任何必需的响应 cookie 或生成任何所需的标记;*GetTokens* 方法本身不会将响应更改为副作用。 *Validate* 方法获取传入会话和字段令牌，并对其运行上述验证逻辑。

### <a name="antiforgeryconfig"></a>AntiForgeryConfig

开发人员可从应用程序启动配置 XSRF 系统 \_ 。 配置是以编程方式进行的。 下面描述了静态 *AntiForgeryConfig* 类型的属性。 大多数使用声明的用户都要设置 UniqueClaimTypeIdentifier 属性。

| **属性** | **说明** |
| --- | --- |
| **AdditionalDataProvider** | 在令牌生成过程中提供附加数据并在令牌验证期间使用其他数据的 [IAntiForgeryAdditionalDataProvider](https://msdn.microsoft.com/library/system.web.helpers.iantiforgeryadditionaldataprovider(v=vs.111).aspx) 。 默认值为 *null*。 有关详细信息，请参阅 [IAntiForgeryAdditionalDataProvider](https://msdn.microsoft.com/library/system.web.helpers.iantiforgeryadditionaldataprovider(v=vs.111).aspx) 部分。 |
| **CookieName** | 一个字符串，它提供用于存储 XSRF 会话令牌的 HTTP cookie 的名称。 如果未设置此值，将根据应用程序的已部署虚拟路径自动生成名称。 默认值为 *null*。 |
| **RequireSsl** | 一个布尔值，指示是否需要在受 SSL 保护的通道上提交 XSRF 令牌。 如果此值为 *true*，则自动生成的任何 cookie 都将设置 "安全" 标志，并在从未通过 SSL 提交的请求内调用时，将引发 XSRF api。 默认值是 *false* 秒。 |
| **SuppressIdentityHeuristicChecks** | 一个布尔值，指示 XSRF 系统是否应停用其对基于声明的标识的支持。 如果此值为 *true*，则系统将假设 *IIdentity.Name* 适用于用作唯一的每用户标识符，并且不会尝试按 [WIF/ACS/基于声明的身份验证](#_WIF_ACS)部分所述尝试使用特殊的 *IClaimsIdentity* 或 *ClClaimsIdentity* 。 默认值为 `false`。 |
| **UniqueClaimTypeIdentifier** | 一个字符串，指示哪种声明类型适用于每个用户的唯一标识符。 如果设置了此值并且当前 *IIdentity* 是基于声明的，则系统将尝试提取 *UniqueClaimTypeIdentifier* 指定的类型的声明，并在生成字段标记时使用相应的值来代替用户的用户名。 如果找不到声明类型，则系统将无法请求。 默认值为 *null*，指示系统应使用 (标识提供者、名称标识符) 元组，如前面所述的替代用户的用户名。 |

<a id="_IAntiForgeryAdditionalDataProvider"></a>

### <a name="iantiforgeryadditionaldataprovider"></a>IAntiForgeryAdditionalDataProvider

*[IAntiForgeryAdditionalDataProvider](https://msdn.microsoft.com/library/system.web.helpers.iantiforgeryadditionaldataprovider(v=vs.111).aspx)* 类型允许开发人员通过往返每个标记中的其他数据来扩展反 XSRF 系统的行为。 每次生成字段标记时都会调用 *GetAdditionalData* 方法，并且返回值嵌入到生成的标记中。 实施者可能会从该方法返回一个时间戳、nonce 或其他任何值。

同样，每次验证字段令牌时，都会调用 *ValidateAdditionalData* 方法，并且在令牌中嵌入的 "附加数据" 字符串将传递给方法。 验证例程可以通过检查当前时间与创建令牌时所存储的时间) 、nonce 检查例程或任何其他所需的逻辑，来实现超时 (。

## <a name="design-decisions-and-security-considerations"></a>设计决策和安全注意事项

在技术上，仅在尝试防止匿名/未经身份验证的用户防御 XSRF 攻击时，才需要在技术上链接会话和字段令牌。 对用户进行身份验证时，身份验证令牌本身 (以 cookie 的形式提交的) 可以用作同步器令牌对的一半。 但是，可以使用有效的方案来保护通过未经身份验证的用户访问的登录页，并通过始终生成和验证安全令牌（即使对于经过身份验证的用户）使 XSRF 逻辑更简单。 如果某个字段令牌被攻击者泄露，还会提供一些额外的保护措施，因为设置或猜测会话令牌会成为攻击者面临的另一个障碍。

在单个域中托管多个应用程序时，开发人员应小心。 例如，尽管 *example1.cloudapp.net* 和 *example2.cloudapp.net* 是不同的主机，但 *\* cloudapp.net* 域下的所有主机之间存在隐式信任关系。 这种隐式信任关系 [允许潜在的不受信任的主机影响彼此的 cookie](http://stackoverflow.com/questions/9636857/how-can-asp-net-or-asp-net-mvc-be-protected-from-related-domain-cookie-attacks) (控制 AJAX 请求的相同源策略不一定适用于 HTTP cookie) 。 ASP.NET Web Stack 运行时提供一些缓解措施，因为用户名嵌入到字段令牌中，因此即使恶意子域能够覆盖会话令牌，也不能为用户生成有效的字段令牌。 但是，如果在此类环境中托管，则内置的 XSRF 例程仍无法防御会话劫持或登录 XSRF。

XSRF 例程当前不防御 [点击劫持](https://www.owasp.org/index.php/Clickjacking)。 希望针对点击劫持进行保护的应用程序可以通过发送 X 框架选项： SAMEORIGIN 标头和每个响应来轻松实现此目的。 所有最新的浏览器都支持此标头。 有关详细信息，请参阅 [IE 博客](https://blogs.msdn.com/b/ieinternals/archive/2010/03/30/combating-clickjacking-with-x-frame-options.aspx)、 [SDL 博客](https://blogs.msdn.com/b/sdl/archive/2009/02/05/clickjacking-defense-in-ie8.aspx)和 [OWASP](https://www.owasp.org/index.php/Clickjacking)。 ASP.NET Web Stack 运行时可能会在将来的版本中使 MVC 和 Web Pages XSRF 帮助器自动设置此标头，以便自动保护应用程序免受这种攻击。

Web 开发人员应继续确保其网站不会受到 XSS 攻击。 XSS 攻击非常强大，成功利用漏洞还会破坏 ASP.NET Web Stack 运行时防御 XSRF 攻击。

## <a name="acknowledgment"></a>确认

[@LeviBroderick](https://twitter.com/LeviBroderick)，其中大部分 ASP.NET 安全代码都是此信息的大部分内容。

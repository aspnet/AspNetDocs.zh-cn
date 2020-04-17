---
uid: aspnet/overview/owin-and-katana/owin-oauth-20-authorization-server
title: OWIN OAuth 2.0 授权服务器 |微软文档
author: hongyes
description: 本教程将指导您如何使用 OWIN OAuth 中间件实现 OAuth 2.0 授权服务器。 这是一个高级教程，只有出...
ms.author: riande
ms.date: 03/20/2014
ms.assetid: 20acee16-c70c-41e9-b38f-92bfcf9a4c1c
msc.legacyurl: /aspnet/overview/owin-and-katana/owin-oauth-20-authorization-server
msc.type: authoredcontent
ms.openlocfilehash: d758fa2639d10e1b7be8d87c5d1f7adb7e292ac7
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81540379"
---
<a name="owin-oauth-20-authorization-server"></a>OWIN OAuth 2.0 授权服务器
====================
由[孙洪业](https://github.com/hongyes)和[普拉布拉杰·蒂加拉詹](https://github.com/Praburaj)

> 本教程将指导您如何使用 OWIN OAuth 中间件实现 OAuth 2.0 授权服务器。 这是一个高级教程，仅概述创建 OWIN OAuth 2.0 授权服务器的步骤。 这不是一步一步的教程。 [下载示例代码](https://code.msdn.microsoft.com/OWIN-OAuth-20-Authorization-ba2b8783/file/114932/1/AuthorizationServer.zip)。
>
> > [!NOTE]
> > 此大纲不应用于创建安全生产应用。 本教程旨在仅提供如何使用 OWIN OAuth 中间件实现 OAuth 2.0 授权服务器的大纲。
>
>
> ## <a name="software-versions"></a>软件版本
>
> | **在教程中显示** | **也适用于** |
> | --- | --- |
> | Windows 8.1 | 视窗 8， 视窗 7 |
> | [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013) | [视觉工作室 2013 快递为桌面](https://my.visualstudio.com/Downloads?q=visual%20studio%202013#d-2013-express). 带有最新更新的 Visual Studio 2012 应该可以正常工作，但本教程尚未使用它进行测试，并且某些菜单选择和对话框是不同的。 |
> | .NET 4.5 |  |
>
> ## <a name="questions-and-comments"></a>问题和评论
>
> 如果您有与本教程没有直接关系的问题，您可以在[GitHub 上的 Katana 项目](https://github.com/aspnet/AspNetKatana/)上发布这些问题。 有关教程本身的问题和注释，请参阅页面底部的注释部分。


[OAuth 2.0 框架](http://tools.ietf.org/html/rfc6749)使第三方应用能够获得对 HTTP 服务的有限访问权限。 客户端不需要使用资源所有者的凭据来访问受保护的资源，而是获取访问令牌（这是表示特定作用域、生存期和其他访问属性的字符串）。 访问令牌由授权服务器在资源所有者批准下颁发给第三方客户端。

本教程将介绍：

- 如何创建授权服务器以支持四种授权授予类型和刷新令牌：
    - 授权代码授予
    - 隐式授予
    - 资源所有者密码凭据授予
    - 客户端凭据授予
- 创建受访问令牌保护的资源服务器。
- 创建 OAuth 2.0 客户端。

<a id="prerequisites"></a>
## <a name="prerequisites"></a>先决条件

- [Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/downloads#d-2013-editions)或免费[的 Visual Studio Express 2013，](https://www.microsoft.com/visualstudio/eng/downloads#d-2013-express)如页面顶部**的软件版本**所示。
- 熟悉 OWIN。 请参阅[开始与卡塔纳项目和](https://msdn.microsoft.com/magazine/dn451439.aspx)[什么在OWIN和卡塔纳的新增功能](index.md)。
- 熟悉[OAuth](http://tools.ietf.org/html/rfc6749)术语，包括[角色](http://tools.ietf.org/html/rfc6749#section-1.1)、[协议流程](http://tools.ietf.org/html/rfc6749#section-1.2)和[授权授予](http://tools.ietf.org/html/rfc6749#section-1.3)。 [OAuth 2.0 介绍](http://tools.ietf.org/html/rfc6749#section-1)提供了很好的介绍。

## <a name="create-an-authorization-server"></a>创建授权服务器

在本教程中，我们将大致勾勒出如何使用[OWIN](https://msdn.microsoft.com/magazine/dn451439.aspx)和 ASP.NET MVC 创建授权服务器。 我们希望很快为已完成的示例提供下载，因为本教程不包括每个步骤。 首先，创建名为 *"授权服务器"* 的空 Web 应用并安装以下程序包：

- 微软.阿斯普内.Mvc
- Microsoft.Owin.Host.SystemWeb
- Microsoft.Owin.Security.OAuth
- Microsoft.Owin.Security.Cookies
- 微软.Owin.Security.Google（或任何其他社交登录包，如微软.Owin.Security.Facebook）

在名为 *"启动"* 的项目根文件夹下添加[OWIN 启动类](owin-startup-class-detection.md)。

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample1.cs?highlight=8)]

创建 *"应用\_开始"* 文件夹。 选择 *"应用\_启动"* 文件夹并使用 Shift_Alt_A 添加 *"授权服务器"[应用\_启动]启动.Auth.cs*文件的下载版本。

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample2.cs)]

上述代码支持应用程序/外部登录 Cookie 和 Google 身份验证，授权服务器本身使用它们来管理帐户。

扩展`UseOAuthAuthorizationServer`方法是设置授权服务器。 设置选项包括：

- `AuthorizeEndpointPath`：客户端应用程序将重定向用户代理以获得用户同意发出令牌或代码的请求路径。 它必须以前导斜杠开头，例如，""。`/Authorize`
- `TokenEndpointPath`：请求路径客户端应用程序直接通信以获取访问令牌。 它必须以前导斜杠开头，如"/令牌"。 如果客户端被颁发[客户端\_密钥](http://tools.ietf.org/html/rfc6749#appendix-A.2)，则必须将其提供给此终结点。
- `ApplicationCanDisplayErrors`：设置为`true`如果 Web 应用程序想要为终结点上的`/Authorize`客户端验证错误生成自定义错误页。 仅当浏览器未重定向回客户端应用程序（例如，`client_id`当 或`redirect_uri`不正确时），才需要这样做。 终结点`/Authorize`应期望看到"auth"。错误"，"哦。错误描述"和"错误描述"。ErrorUri"属性将添加到 OWIN 环境中。

    > [!NOTE]
    > 如果为 true，授权服务器将返回包含错误详细信息的默认错误页。
- `AllowInsecureHttp`：如果为 True，允许授权和令牌请求到达 HTTP URI 地址，并允许`redirect_uri`传入授权请求参数具有 HTTP URI 地址。

    > [!WARNING]
    > 安全性 - 这仅用于开发。
- `Provider`：应用程序为处理授权服务器中间件引发的事件而提供的对象。 应用程序可以完全实现接口，也可以创建此服务器支持的 OAuth`OAuthAuthorizationServerProvider`流所需的实例和分配委托。
- `AuthorizationCodeProvider`：生成一次性授权代码以返回到客户端应用程序。 为了保护 OAuth 服务器的安全，应用程序**必须**提供一个实例`AuthorizationCodeProvider`，其中`OnCreate/OnCreateAsync`事件生成的令牌仅对 一次调用 有效`OnReceive/OnReceiveAsync`。
- `RefreshTokenProvider`：生成刷新令牌，可在需要时用于生成新的访问令牌。 如果未提供授权服务器将不会从`/Token`终结点返回刷新令牌。

## <a name="account-management"></a>帐户管理

OAuth 不关心您管理用户帐户信息的位置或方式。 负责它的[ASP.NET身份](../../../identity/index.md)。 在本教程中，我们将简化帐户管理代码，并确保用户可以使用 OWIN Cookie 中间件登录。 下面是 ： 的`AccountController`简化示例代码：

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample3.cs)]

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample4.cs?highlight=1)]

`ValidateClientRedirectUri`用于验证客户端及其注册的重定向 URL。 `ValidateClientAuthentication`检查基本方案标头和窗体正文以获取客户端的凭据。

登录页面如下所示：

![](owin-oauth-20-authorization-server/_static/image1.png)

立即查看 IETF 的 OAuth 2[授权代码授予](http://tools.ietf.org/html/rfc6749#section-4.1)部分。

**提供程序**（下表中）是[OAuth 授权服务器选项](https://msdn.microsoft.com/library/microsoft.owin.security.oauth.oauthauthorizationserveroptions(v=vs.111).aspx)。提供程序，其类型 为`OAuthAuthorizationServerProvider`，它包含所有 OAuth 服务器事件。

| 授权代码授予部分的流步骤 | 示例下载执行以下步骤： |
| --- | --- |
|  |  |
| （A） 客户端通过将资源所有者的用户代理定向到授权终结点来启动流。 客户端包括其客户端标识符、请求的范围、本地状态和重定向 URI，授权服务器将在授予（或拒绝）访问权限后将用户代理发送回该 URI。 | 提供程序.匹配终结点提供程序.验证客户端重定向提供程序.验证授权请求提供程序.授权终结点 |
|  |  |
| （B） 授权服务器对资源所有者进行身份验证（通过用户代理），并确定资源所有者是授予还是拒绝客户端的访问请求。 | **如果用户授予访问权限&gt;&lt;** 提供程序.匹配终结点提供程序.验证客户端重定向提供程序.验证授权请求提供程序.授权终结点授权码提供程序.创建Async |
|  |  |
| （C） 假设资源所有者授予访问权限，授权服务器使用前面提供的重定向 URI（在请求中或客户端注册期间）将用户代理重定向回客户端。 ... |  |
|  |  |
| （D） 客户端通过包含上一步骤中收到的授权代码，从授权服务器的令牌终结点请求访问令牌。 发出请求时，客户端会使用授权服务器进行身份验证。 客户端包括用于获取验证授权码的重定向 URI。 | 提供程序.匹配终结点提供程序.验证客户端身份验证授权代码提供程序.接收 Async 提供程序.验证令牌请求提供程序.授予授权代码提供程序.令牌终结点访问令牌提供程序.创建 async 刷新令牌提供程序.创建async |

下面显示了 用于`AuthorizationCodeProvider.CreateAsync``ReceiveAsync`和控制授权代码的创建和验证的示例实现。

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample5.cs)]

上述代码使用内存中并发字典来存储代码和标识票证，并在收到代码后还原标识。 在实际应用程序中，它将被持久性数据存储替换。 授权终结点供资源所有者授予对客户端的访问权限。 通常，它需要一个用户界面来允许用户单击按钮并确认授予。 OWIN OAuth 中间件允许应用程序代码处理授权终结点。 在我们的示例应用中，我们使用调用`OAuthController`的 MVC 控制器来处理它。 下面是实现的示例：

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample6.cs?highlight=15)]

此操作`Authorize`将首先检查用户是否登录到授权服务器。 如果没有，身份验证中间件会向调用方提出使用"应用程序"Cookie 进行身份验证的挑战，并重定向到登录页。 （请参阅上面突出显示的代码。如果用户已登录，它将呈现"授权"视图，如下所示：

![](owin-oauth-20-authorization-server/_static/image2.png)

如果选择了 **"授予**"按钮，`Authorize`该操作将创建新的"持有者"标识并登录。 它将触发授权服务器以生成无记名令牌，并将其发送回具有 JSON 负载的客户端。

### <a name="implicit-grant"></a>隐式授予

立即请参阅 IETF 的 OAuth 2[隐式授予](http://tools.ietf.org/html/rfc6749#section-4.2)部分。

 图 4 所示[的隐式授予](http://tools.ietf.org/html/rfc6749#section-4.2)流是 OWIN OAuth 中间件后面的流和映射。

| 来自隐式授予部分的流步骤 | 示例下载执行以下步骤： |
| --- | --- |
|  |  |
| （A） 客户端通过将资源所有者的用户代理定向到授权终结点来启动流。 客户端包括其客户端标识符、请求的范围、本地状态和重定向 URI，授权服务器将在授予（或拒绝）访问权限后将用户代理发送回该 URI。 | 提供程序.匹配终结点提供程序.验证客户端重定向提供程序.验证授权请求提供程序.授权终结点 |
|  |  |
| （B） 授权服务器对资源所有者进行身份验证（通过用户代理），并确定资源所有者是授予还是拒绝客户端的访问请求。 | **如果用户授予访问权限&gt;&lt;** 提供程序.匹配终结点提供程序.验证客户端重定向提供程序.验证授权请求提供程序.授权终结点授权码提供程序.创建Async |
|  |  |
| （C） 假设资源所有者授予访问权限，授权服务器使用前面提供的重定向 URI（在请求中或客户端注册期间）将用户代理重定向回客户端。 ... |  |
|  |  |
| （D） 客户端通过包含上一步骤中收到的授权代码，从授权服务器的令牌终结点请求访问令牌。 发出请求时，客户端会使用授权服务器进行身份验证。 客户端包括用于获取验证授权码的重定向 URI。 |  |

由于我们已经实现了授权代码授予的授权终结点`OAuthController.Authorize`（操作），因此它会自动启用隐式流。 注意：`Provider.ValidateClientRedirectUri`用于验证客户端 ID 及其重定向 URL，它保护隐式授予流从发送访问令牌到恶意客户端（[中间人攻击](https://www.owasp.org/index.php/Man-in-the-middle_attack)）。

### <a name="resource-owner-password-credentials-grant"></a>资源所有者密码凭据授予

立即请参阅 IETF 的 OAuth 2[资源所有者密码凭据授予](http://tools.ietf.org/html/rfc6749#section-4.3)部分。

 图 5 所示[的资源所有者密码凭据授予](http://tools.ietf.org/html/rfc6749#section-4.3)流是 OWIN OAuth 中间件后面的流和映射。

| 来自资源所有者密码凭据授予部分的流步骤 | 示例下载执行以下步骤： |
| --- | --- |
|  |  |
| （A） 资源所有者向客户端提供其用户名和密码。 |  |
|  |  |
| （B） 客户端通过包含从资源所有者收到的凭据来请求来自授权服务器令牌终结点的访问令牌。 发出请求时，客户端会使用授权服务器进行身份验证。 | 提供程序.匹配终结点提供程序.验证客户端身份验证提供程序.验证令牌请求提供程序.授予资源所有者凭据提供程序.令牌终结点访问令牌提供程序.创建同步刷新令牌提供程序.创建async |
|  |  |
| （C） 授权服务器对客户端进行身份验证并验证资源所有者凭据，如果有效，则颁发访问令牌。 |  |

下面是`Provider.GrantResourceOwnerCredentials`以下示例实现：

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample7.cs)]

> [!NOTE]
> 上面的代码旨在解释本教程的这一部分，不应在安全或生产应用中使用。 它不检查资源所有者凭据。 它假定每个凭据都有效，并为其创建新标识。 新标识将用于生成访问令牌和刷新令牌。 请将代码替换为您自己的安全帐户管理代码。


### <a name="client-credentials-grant"></a>客户端凭据授予

立即请参阅 IETF 的 OAuth 2[客户端凭据授予](http://tools.ietf.org/html/rfc6749#section-4.4)部分。

 图 6 所示[的客户端凭据授予](http://tools.ietf.org/html/rfc6749#section-4.4)流是 OWIN OAuth 中间件后面的流和映射。

| 来自客户端凭据授予部分的流步骤 | 示例下载执行以下步骤： |
| --- | --- |
|  |  |
| （A） 客户端使用授权服务器进行身份验证，并从令牌终结点请求访问令牌。 | 提供程序.匹配终结点提供程序.验证客户端身份验证提供程序.验证令牌请求提供程序.授予客户端凭据提供程序.令牌终结点访问令牌提供程序.创建同步刷新令牌提供程序.创建async |
|  |  |
| （B） 授权服务器对客户端进行身份验证，如果有效，则颁发访问令牌。 |  |

下面是`Provider.GrantClientCredentials`以下示例实现：

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample8.cs)]

> [!NOTE]
> 上面的代码旨在解释本教程的这一部分，不应在安全或生产应用中使用。 请将代码替换为您自己的安全客户端管理代码。


### <a name="refresh-token"></a>刷新令牌

立即请参阅 IETF 的 OAuth 2[刷新令牌](http://tools.ietf.org/html/rfc6749#section-1.5)部分。

 图 2 所示的[刷新令牌](http://tools.ietf.org/html/rfc6749#section-1.5)流是 OWIN OAuth 中间件后面的流和映射。

| 来自客户端凭据授予部分的流步骤 | 示例下载执行以下步骤： |
| --- | --- |
|  |  |
| （G） 客户端通过使用授权服务器进行身份验证并呈现刷新令牌来请求新的访问令牌。 客户端身份验证要求基于客户端类型和授权服务器策略。 | 提供程序.匹配终结点提供程序.验证客户端身份验证刷新令牌提供程序.接收async提供程序.验证令牌请求提供程序.授予refreshtoken提供程序.令牌终结点访问令牌提供程序.创建async刷新令牌提供程序.创建Async |
|  |  |
| （H） 授权服务器对客户端进行身份验证并验证刷新令牌，如果有效，则颁发新的访问令牌（以及可选为新刷新令牌）。 |  |

下面是`Provider.GrantRefreshToken`以下示例实现：

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample9.cs)]

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample10.cs)]

## <a name="create-a-resource-server-which-is-protected-by-access-token"></a>创建受访问令牌保护的资源服务器

创建空 Web 应用项目并在项目中安装以下包：

- 微软.AspNet.WebApi.Owin
- Microsoft.Owin.Host.SystemWeb
- Microsoft.Owin.Security.OAuth

创建启动类并配置身份验证和 Web API。 请参阅*示例下载中的授权服务器\资源服务器\启动.cs。*

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample11.cs)]

请参阅*示例下载中的授权服务器\资源\_服务器\应用启动\启动.Auth.cs。*

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample12.cs)]

请参阅*示例下载中的授权服务器\资源\_服务器\应用启动\启动.WebApi.cs。*

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample13.cs)]

- `UseCors`方法允许所有域的 CORS。
- `UseOAuthBearerAuthentication`方法启用 OAuth 承载令牌身份验证中间件，它将从请求中的授权标头接收和验证无记名令牌。
- `Config.SuppressDefaultHostAuthenticaiton`禁止从应用中默认主机经过身份验证的主体，因此在此调用后所有请求都将是匿名的。
- `HostAuthenticationFilter`仅针对指定的身份验证类型启用身份验证。 在这种情况下，它是承载身份验证类型。

为了演示经过身份验证的身份，我们创建了一个 ApiController 来输出当前用户的声明。

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample14.cs)]

如果授权服务器和资源服务器不在同一台计算机上，OAuth 中间件将使用不同的计算机密钥来加密和解密承载访问令牌。 为了在两个项目之间共享相同的私钥，我们在两个`machinekey`*Web.config*文件中添加相同的设置。

[!code-xml[Main](owin-oauth-20-authorization-server/samples/sample15.xml?highlight=8-10)]

## <a name="create-oauth-20-clients"></a>创建 OAuth 2.0 客户端

 我们使用[DotNetOpenAuth.OAuth2.客户端](http://www.nuget.org/packages/DotNetOpenAuth.OAuth2.Client)NuGet 包来简化客户端代码。

### <a name="authorization-code-grant-client"></a>授权代码授予客户端

 此客户端是 MVC 应用程序。 它将触发授权代码授予流，以便从后端获取访问令牌。 它有一个页面，如下所示：

![](owin-oauth-20-authorization-server/_static/image3.png)

- "**授权"** 按钮将浏览器重定向到授权服务器，以通知资源所有者授予对此客户端的访问权限。
- "**刷新**"按钮将使用当前刷新令牌获取新的访问令牌和刷新令牌。
- **"访问受保护资源 API"** 按钮将调用资源服务器获取当前用户的声明数据并在页面上显示这些数据。

下面是客户端`HomeController`的示例代码。

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample16.cs)]

`DotNetOpenAuth`默认情况下需要 SSL。 由于我们的演示使用 HTTP，您需要在配置文件中添加以下设置：

[!code-xml[Main](owin-oauth-20-authorization-server/samples/sample17.xml?highlight=4-6)]

> [!WARNING]
> 安全性 - 切勿在生产应用中禁用 SSL。 您的登录凭据现在以明文形式通过网络发送。 上面的代码仅用于本地示例调试和探索。


### <a name="implicit-grant-client"></a>隐式授予客户端

此客户端使用 JavaScript 来：

1. 打开新窗口并重定向到授权服务器的授权终结点。
2. 当 URL 片段重定向回时，从它获取访问令牌。

下图显示了此过程：

![](owin-oauth-20-authorization-server/_static/image4.png)

客户端应该有两个页面：一个用于主页，另一个用于回调。下面是*在 Index.cshtml*文件中找到的示例 JavaScript 代码：

[!code-cshtml[Main](owin-oauth-20-authorization-server/samples/sample18.cshtml)]

下面是*SignIn.cshtml*文件中的回调处理代码：

[!code-cshtml[Main](owin-oauth-20-authorization-server/samples/sample19.cshtml)]

> [!NOTE]
> 最佳做法是将 JavaScript 移动到外部文件，而不是将其嵌入 Razor 标记中。 为了保持此示例的简单性，它们已被合并。


### <a name="resource-owner-password-credentials-grant-client"></a>资源所有者密码凭据授予客户端

我们使用控制台应用程序来演示此客户端。 代码如下：

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample20.cs)]

### <a name="client-credentials-grant-client"></a>客户端凭据授予客户端

与资源所有者密码凭据授予类似，下面是控制台应用代码：

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample21.cs)]

---
uid: webhooks/receiving/receivers
title: ASP.NET WebHook 接收器 |微软文档
author: rick-anderson
description: ASP.NET WebHook 接收器
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 6cdea089-15b2-4732-8c68-921ca561a8f1
ms.openlocfilehash: 60f46141b59fc3888a6480d8201160420469d1a7
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675170"
---
# <a name="aspnet-webhooks-receivers"></a>ASP.NET WebHook 接收器

接收 WebHook 取决于发件人是谁。 有时，还有其他步骤注册 WebHook，验证订阅者是否真正在侦听。 某些 WebHook 提供推送到拉取模型，其中 HTTP POST 请求仅包含对事件信息的引用，然后由该引用独立检索。 通常，安全模型差异很大。

Microsoft ASP.NET WebHooks 的目的是使连接 API 更简单、更一致，而无需花费大量时间来了解如何处理 WebHook 的任何特定变体。

WebHook 接收器负责接受和验证来自特定发件人的 WebHook。 WebHook 接收器可以支持任意数量的 WebHook，每个 WebHook 都有自己的配置。 例如，GitHub WebHook 接收器可以接受来自任意数量的 GitHub 存储库的 WebHook。

## <a name="webhook-receiver-uris"></a>WebHook 接收器 URI

通过安装 Microsoft ASP.NET WebHooks，您可以获得一个常规 WebHook 控制器，该控制器接受来自开源服务数量的 WebHook 请求。 请求到达时，它会选择已安装的用于处理特定 WebHook 发送方的相应接收器。

此控制器的 URI 是您向服务注册的 WebHook URI，其形式为：

```
https://<host>/api/webhooks/incoming/<receiver>/{id}
```

出于安全原因，许多 WebHook 接收器要求 URI 是*https* URI，在某些情况下，它还必须包含一个额外的查询参数，用于强制只有目标方才能将 WebHook 发送到上述 URI。

组件`<receiver>`是接收器的名称，例如`github`或`slack`。

*{id}* 是一个可选标识符，可用于标识特定的 WebHook 接收器配置。 这可用于向特定接收器注册 N WebHook。 例如，以下三个 URI 可用于注册三个独立的 WebHook：

```
https://<host>/api/webhooks/incoming/github
https://<host>/api/webhooks/incoming/github/12345
https://<host>/api/webhooks/incoming/github/54321
```

## <a name="installing-a-webhook-receiver"></a>安装 WebHook 接收器

要使用 Microsoft ASP.NET WebHook 接收 WebHook，请首先为要接收 WebHook 的 WebHook 提供商或提供商安装 Nuget 包。 Nuget 包名为[Microsoft.AspNet.WebHooks.Receivers.*，](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers)其中最后一部分表示支持的服务。 例如：

[微软.AspNet.WebHooks.Receivers.GitHub](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.GitHub)支持接收来自GitHub和[微软的WebHook.AspNet.WebHooks.Receivers.Customs.Customs](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.Custom)为接收由ASP.NETWebHooks生成的WebHook提供支持。

开箱即用，您可以找到对 Dropbox、GitHub、MailChimp、PayPal、Pusher、Salesforce、Slack、Stripe、Trello 和 WordPress 的支持，但可以支持任意数量的其他提供商。

## <a name="configuring-a-webhook-receiver"></a>配置 WebHook 接收器

WebHook 接收器通过[IWebHookReceiverConfig 整](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/IWebHookReceiverConfig.cs)面进行配置，该接口的特定实现可以使用任何依赖项注入模型进行注册。 默认实现使用应用程序设置，可以在 Web.config 文件中设置，或者，如果使用 Azure Web 应用，可以通过[Azure 门户](https://portal.azure.com/)进行设置。

![Azure 应用设置](_static/AzureAppSettings.png)

应用程序设置键的格式如下：

```
MS_WebHookReceiverSecret_<receiver>
```

该值是与已注册 WebHook 的 *[id]* 值匹配的逗号分隔的值列表，例如：

```
MS_WebHookReceiverSecret_GitHub = <secret1>, 12345=<secret2>, 54321=<secret3>
```

## <a name="initializing-a-webhook-receiver"></a>初始化 WebHook 接收器

WebHook 接收器通过注册来初始化，通常在*WebApiConfig*静态类中，例如：

```csharp
namespace WebHookReceivers
{
    public static class WebApiConfig
    {
        public static void Register(HttpConfiguration config)
        {
            // Web API configuration and services

            // Web API routes
            config.MapHttpAttributeRoutes();

            config.Routes.MapHttpRoute(
                name: "DefaultApi",
                routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional }
            );

            // Load receivers
            config.InitializeReceiveGitHubWebHooks();
        }
    }
}
```

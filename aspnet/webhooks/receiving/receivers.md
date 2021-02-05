---
uid: webhooks/receiving/receivers
title: ASP.NET Webhook 接收方 |Microsoft Docs
author: rick-anderson
description: ASP.NET Webhook 接收者
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 6cdea089-15b2-4732-8c68-921ca561a8f1
ms.openlocfilehash: b2ff82777b396949ee089f4275cb6c318a45570c
ms.sourcegitcommit: e890232aa69193044409a0d4f968e5fec9ac4eb5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/05/2021
ms.locfileid: "99572069"
---
# <a name="aspnet-webhooks-receivers"></a>ASP.NET Webhook 接收者

接收 Webhook 取决于发件人是谁。 有时，注册 WebHook 的附加步骤是验证订阅服务器是否确实正在侦听。 有些 Webhook 提供了推送到请求模型，其中的 HTTP POST 请求仅包含对事件信息的引用，然后将对这些信息进行单独检索。 安全模型通常会变化很多。

Microsoft ASP.NET Webhook 的目的是为了使 API 更简单、更一致，无需花费大量时间来了解如何处理 Webhook 的任何特定变体。

WebHook 接收方负责接受和验证来自特定发件人的 Webhook。 WebHook 接收方可以支持任意数量的 Webhook，每个都有其自己的配置。 例如，GitHub WebHook 接收方可以接受任意数量 GitHub 存储库中的 Webhook。

## <a name="webhook-receiver-uris"></a>WebHook 接收方 Uri

通过安装 Microsoft ASP.NET Webhook，你将获得一个常规 WebHook 控制器，该控制器接受来自开放式服务数量的 WebHook 请求。 请求到达时，会选取为处理特定 WebHook 发送程序而安装的适当接收方。

此控制器的 URI 是向服务注册的 WebHook URI，其格式为：

```
https://<host>/api/webhooks/incoming/<receiver>/{id}
```

出于安全原因，许多 WebHook 接收方都要求 URI 是 *https* uri，并且在某些情况下，它还必须包含一个附加查询参数，该参数用于强制只有目标参与方可以将 webhook 发送到上述 URI。

`<receiver>`组件是接收方的名称，例如 `github` 或 `slack` 。

*{Id}* 是可选标识符，可用于标识特定 WebHook 接收器配置。 这可用于向特定接收方注册 N Webhook。 例如，以下三个 Uri 可用于注册三个独立的 Webhook：

```
https://<host>/api/webhooks/incoming/github
https://<host>/api/webhooks/incoming/github/12345
https://<host>/api/webhooks/incoming/github/54321
```

## <a name="installing-a-webhook-receiver"></a>安装 WebHook 接收器

若要使用 Microsoft ASP.NET Webhook 接收 Webhook，请首先为要从中接收 Webhook 的 WebHook 提供程序或提供程序安装 Nuget 包。 Nuget 包名为 [webhook. *](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers) ，其中最后一个部分指示支持的服务。 例如

[Webhook](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.GitHub)为从 GitHub 和 Webhook 接收 webhook 提供支持。 [](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.Custom)提供了对接收 webhook ASP.NET webhook 生成的的支持。

在此框中，你可以找到对 Dropbox、GitHub、MailChimp、PayPal、Pusher、Salesforce、时差、磁条、Trello 和 WordPress 的支持，但也可以支持任意数量的其他提供商。

## <a name="configuring-a-webhook-receiver"></a>配置 WebHook 接收方

通过 [IWebHookReceiverConfig](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/IWebHookReceiverConfig.cs) 接口配置 WebHook 接收方，并且可以使用任何依赖关系注入模型注册该接口的特定实现。 默认实现使用可以在 Web.config 文件中设置的应用程序设置，如果使用 Azure Web 应用，则可以通过 [Azure 门户](https://portal.azure.com/)进行设置。

![Azure 应用设置](_static/AzureAppSettings.png)

应用程序设置键的格式如下所示：

```
MS_WebHookReceiverSecret_<receiver>
```

该值是一个以逗号分隔的值列表，其中包含已注册 Webhook 的 *{id}* 值，例如：

```
MS_WebHookReceiverSecret_GitHub = <secret1>, 12345=<secret2>, 54321=<secret3>
```

## <a name="initializing-a-webhook-receiver"></a>初始化 WebHook 接收方

通过注册 WebHook 接收器，通常在 *webapiconfig.cs* 静态类中进行初始化，例如：

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

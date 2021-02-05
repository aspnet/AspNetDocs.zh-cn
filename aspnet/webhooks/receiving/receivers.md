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
# <a name="aspnet-webhooks-receivers"></a><span data-ttu-id="2cdda-103">ASP.NET Webhook 接收者</span><span class="sxs-lookup"><span data-stu-id="2cdda-103">ASP.NET WebHooks receivers</span></span>

<span data-ttu-id="2cdda-104">接收 Webhook 取决于发件人是谁。</span><span class="sxs-lookup"><span data-stu-id="2cdda-104">Receiving WebHooks depends on who the sender is.</span></span> <span data-ttu-id="2cdda-105">有时，注册 WebHook 的附加步骤是验证订阅服务器是否确实正在侦听。</span><span class="sxs-lookup"><span data-stu-id="2cdda-105">Sometimes there are additional steps registering a WebHook verifying that the subscriber is really listening.</span></span> <span data-ttu-id="2cdda-106">有些 Webhook 提供了推送到请求模型，其中的 HTTP POST 请求仅包含对事件信息的引用，然后将对这些信息进行单独检索。</span><span class="sxs-lookup"><span data-stu-id="2cdda-106">Some WebHooks provide a push-to-pull model where the HTTP POST request only contains a reference to the event information which is then to be retrieved independently.</span></span> <span data-ttu-id="2cdda-107">安全模型通常会变化很多。</span><span class="sxs-lookup"><span data-stu-id="2cdda-107">Often the security model varies quite a bit.</span></span>

<span data-ttu-id="2cdda-108">Microsoft ASP.NET Webhook 的目的是为了使 API 更简单、更一致，无需花费大量时间来了解如何处理 Webhook 的任何特定变体。</span><span class="sxs-lookup"><span data-stu-id="2cdda-108">The purpose of Microsoft ASP.NET WebHooks is to make it both simpler and more consistent to wire up your API without spending a lot of time figuring out how to handle any particular variant of WebHooks.</span></span>

<span data-ttu-id="2cdda-109">WebHook 接收方负责接受和验证来自特定发件人的 Webhook。</span><span class="sxs-lookup"><span data-stu-id="2cdda-109">A WebHook receiver is responsible for accepting and verifying WebHooks from a particular sender.</span></span> <span data-ttu-id="2cdda-110">WebHook 接收方可以支持任意数量的 Webhook，每个都有其自己的配置。</span><span class="sxs-lookup"><span data-stu-id="2cdda-110">A WebHook receiver can support any number of WebHooks, each with their own configuration.</span></span> <span data-ttu-id="2cdda-111">例如，GitHub WebHook 接收方可以接受任意数量 GitHub 存储库中的 Webhook。</span><span class="sxs-lookup"><span data-stu-id="2cdda-111">For example, the GitHub WebHook receiver can accept WebHooks from any number of GitHub repositories.</span></span>

## <a name="webhook-receiver-uris"></a><span data-ttu-id="2cdda-112">WebHook 接收方 Uri</span><span class="sxs-lookup"><span data-stu-id="2cdda-112">WebHook Receiver URIs</span></span>

<span data-ttu-id="2cdda-113">通过安装 Microsoft ASP.NET Webhook，你将获得一个常规 WebHook 控制器，该控制器接受来自开放式服务数量的 WebHook 请求。</span><span class="sxs-lookup"><span data-stu-id="2cdda-113">By installing Microsoft ASP.NET WebHooks you get a general WebHook controller which accepts WebHook requests from an open-ended number of services.</span></span> <span data-ttu-id="2cdda-114">请求到达时，会选取为处理特定 WebHook 发送程序而安装的适当接收方。</span><span class="sxs-lookup"><span data-stu-id="2cdda-114">When a request arrives, it picks the appropriate receiver that you have installed for handling a particular WebHook sender.</span></span>

<span data-ttu-id="2cdda-115">此控制器的 URI 是向服务注册的 WebHook URI，其格式为：</span><span class="sxs-lookup"><span data-stu-id="2cdda-115">The URI of this controller is the WebHook URI that you register with the service and is of the form:</span></span>

```
https://<host>/api/webhooks/incoming/<receiver>/{id}
```

<span data-ttu-id="2cdda-116">出于安全原因，许多 WebHook 接收方都要求 URI 是 *https* uri，并且在某些情况下，它还必须包含一个附加查询参数，该参数用于强制只有目标参与方可以将 webhook 发送到上述 URI。</span><span class="sxs-lookup"><span data-stu-id="2cdda-116">For security reasons, many WebHook receivers require that the URI is an *https* URI and in some cases it must also contain an additional query parameter which is used to enforce that only the intended party can send WebHooks to the URI above.</span></span>

<span data-ttu-id="2cdda-117">`<receiver>`组件是接收方的名称，例如 `github` 或 `slack` 。</span><span class="sxs-lookup"><span data-stu-id="2cdda-117">The `<receiver>` component is the name of the receiver, for example `github` or `slack`.</span></span>

<span data-ttu-id="2cdda-118">*{Id}* 是可选标识符，可用于标识特定 WebHook 接收器配置。</span><span class="sxs-lookup"><span data-stu-id="2cdda-118">The *{id}* is an optional identifier which can be used to identify a particular WebHook receiver configuration.</span></span> <span data-ttu-id="2cdda-119">这可用于向特定接收方注册 N Webhook。</span><span class="sxs-lookup"><span data-stu-id="2cdda-119">This can be used to register N WebHooks with a particular receiver.</span></span> <span data-ttu-id="2cdda-120">例如，以下三个 Uri 可用于注册三个独立的 Webhook：</span><span class="sxs-lookup"><span data-stu-id="2cdda-120">For example, the following three URIs can be used to register for three independent WebHooks:</span></span>

```
https://<host>/api/webhooks/incoming/github
https://<host>/api/webhooks/incoming/github/12345
https://<host>/api/webhooks/incoming/github/54321
```

## <a name="installing-a-webhook-receiver"></a><span data-ttu-id="2cdda-121">安装 WebHook 接收器</span><span class="sxs-lookup"><span data-stu-id="2cdda-121">Installing a WebHook Receiver</span></span>

<span data-ttu-id="2cdda-122">若要使用 Microsoft ASP.NET Webhook 接收 Webhook，请首先为要从中接收 Webhook 的 WebHook 提供程序或提供程序安装 Nuget 包。</span><span class="sxs-lookup"><span data-stu-id="2cdda-122">To receive WebHooks using Microsoft ASP.NET WebHooks, you first install the Nuget package for the WebHook provider or providers you want to receive WebHooks from.</span></span> <span data-ttu-id="2cdda-123">Nuget 包名为 [webhook. \*](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers) ，其中最后一个部分指示支持的服务。</span><span class="sxs-lookup"><span data-stu-id="2cdda-123">The Nuget packages are named [Microsoft.AspNet.WebHooks.Receivers.\*](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers) where the last part indicates the service supported.</span></span> <span data-ttu-id="2cdda-124">例如</span><span class="sxs-lookup"><span data-stu-id="2cdda-124">For example</span></span>

<span data-ttu-id="2cdda-125">[Webhook](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.GitHub)为从 GitHub 和 Webhook 接收 webhook 提供支持。 [](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.Custom)提供了对接收 webhook ASP.NET webhook 生成的的支持。</span><span class="sxs-lookup"><span data-stu-id="2cdda-125">[Microsoft.AspNet.WebHooks.Receivers.GitHub](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.GitHub) provides support for receiving WebHooks from GitHub and [Microsoft.AspNet.WebHooks.Receivers.Custom](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.Custom) provides support for receiving WebHooks generated by ASP.NET WebHooks.</span></span>

<span data-ttu-id="2cdda-126">在此框中，你可以找到对 Dropbox、GitHub、MailChimp、PayPal、Pusher、Salesforce、时差、磁条、Trello 和 WordPress 的支持，但也可以支持任意数量的其他提供商。</span><span class="sxs-lookup"><span data-stu-id="2cdda-126">Out of the box you can find support for Dropbox, GitHub, MailChimp, PayPal, Pusher, Salesforce, Slack, Stripe, Trello, and WordPress but it is possible to support any number of other providers.</span></span>

## <a name="configuring-a-webhook-receiver"></a><span data-ttu-id="2cdda-127">配置 WebHook 接收方</span><span class="sxs-lookup"><span data-stu-id="2cdda-127">Configuring a WebHook Receiver</span></span>

<span data-ttu-id="2cdda-128">通过 [IWebHookReceiverConfig](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/IWebHookReceiverConfig.cs) 接口配置 WebHook 接收方，并且可以使用任何依赖关系注入模型注册该接口的特定实现。</span><span class="sxs-lookup"><span data-stu-id="2cdda-128">WebHook Receivers are configured through the [IWebHookReceiverConfig](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/IWebHookReceiverConfig.cs) interface and particular implementations of that interface can be registered using any dependency injection model.</span></span> <span data-ttu-id="2cdda-129">默认实现使用可以在 Web.config 文件中设置的应用程序设置，如果使用 Azure Web 应用，则可以通过 [Azure 门户](https://portal.azure.com/)进行设置。</span><span class="sxs-lookup"><span data-stu-id="2cdda-129">The default implementation uses Application Settings which can either be set in the Web.config file, or, if using Azure Web Apps, can be set through the [Azure Portal](https://portal.azure.com/).</span></span>

![Azure 应用设置](_static/AzureAppSettings.png)

<span data-ttu-id="2cdda-131">应用程序设置键的格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="2cdda-131">The format for Application Setting keys is as follows:</span></span>

```
MS_WebHookReceiverSecret_<receiver>
```

<span data-ttu-id="2cdda-132">该值是一个以逗号分隔的值列表，其中包含已注册 Webhook 的 *{id}* 值，例如：</span><span class="sxs-lookup"><span data-stu-id="2cdda-132">The value is a comma-separated list of values matching the *{id}* values for which WebHooks have been registered, for example:</span></span>

```
MS_WebHookReceiverSecret_GitHub = <secret1>, 12345=<secret2>, 54321=<secret3>
```

## <a name="initializing-a-webhook-receiver"></a><span data-ttu-id="2cdda-133">初始化 WebHook 接收方</span><span class="sxs-lookup"><span data-stu-id="2cdda-133">Initializing a WebHook Receiver</span></span>

<span data-ttu-id="2cdda-134">通过注册 WebHook 接收器，通常在 *webapiconfig.cs* 静态类中进行初始化，例如：</span><span class="sxs-lookup"><span data-stu-id="2cdda-134">WebHook Receivers are initialized by registering them, typically in the *WebApiConfig* static class, for example:</span></span>

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

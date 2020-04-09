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
# <a name="aspnet-webhooks-receivers"></a><span data-ttu-id="8b757-103">ASP.NET WebHook 接收器</span><span class="sxs-lookup"><span data-stu-id="8b757-103">ASP.NET WebHooks receivers</span></span>

<span data-ttu-id="8b757-104">接收 WebHook 取决于发件人是谁。</span><span class="sxs-lookup"><span data-stu-id="8b757-104">Receiving WebHooks depends on who the sender is.</span></span> <span data-ttu-id="8b757-105">有时，还有其他步骤注册 WebHook，验证订阅者是否真正在侦听。</span><span class="sxs-lookup"><span data-stu-id="8b757-105">Sometimes there are additional steps registering a WebHook verifying that the subscriber is really listening.</span></span> <span data-ttu-id="8b757-106">某些 WebHook 提供推送到拉取模型，其中 HTTP POST 请求仅包含对事件信息的引用，然后由该引用独立检索。</span><span class="sxs-lookup"><span data-stu-id="8b757-106">Some WebHooks provide a push-to-pull model where the HTTP POST request only contains a reference to the event information which is then to be retrieved independently.</span></span> <span data-ttu-id="8b757-107">通常，安全模型差异很大。</span><span class="sxs-lookup"><span data-stu-id="8b757-107">Often the security model varies quite a bit.</span></span>

<span data-ttu-id="8b757-108">Microsoft ASP.NET WebHooks 的目的是使连接 API 更简单、更一致，而无需花费大量时间来了解如何处理 WebHook 的任何特定变体。</span><span class="sxs-lookup"><span data-stu-id="8b757-108">The purpose of Microsoft ASP.NET WebHooks is to make it both simpler and more consistent to wire up your API without spending a lot of time figuring out how to handle any particular variant of WebHooks.</span></span>

<span data-ttu-id="8b757-109">WebHook 接收器负责接受和验证来自特定发件人的 WebHook。</span><span class="sxs-lookup"><span data-stu-id="8b757-109">A WebHook receiver is responsible for accepting and verifying WebHooks from a particular sender.</span></span> <span data-ttu-id="8b757-110">WebHook 接收器可以支持任意数量的 WebHook，每个 WebHook 都有自己的配置。</span><span class="sxs-lookup"><span data-stu-id="8b757-110">A WebHook receiver can support any number of WebHooks, each with their own configuration.</span></span> <span data-ttu-id="8b757-111">例如，GitHub WebHook 接收器可以接受来自任意数量的 GitHub 存储库的 WebHook。</span><span class="sxs-lookup"><span data-stu-id="8b757-111">For example, the GitHub WebHook receiver can accept WebHooks from any number of GitHub repositories.</span></span>

## <a name="webhook-receiver-uris"></a><span data-ttu-id="8b757-112">WebHook 接收器 URI</span><span class="sxs-lookup"><span data-stu-id="8b757-112">WebHook Receiver URIs</span></span>

<span data-ttu-id="8b757-113">通过安装 Microsoft ASP.NET WebHooks，您可以获得一个常规 WebHook 控制器，该控制器接受来自开源服务数量的 WebHook 请求。</span><span class="sxs-lookup"><span data-stu-id="8b757-113">By installing Microsoft ASP.NET WebHooks you get a general WebHook controller which accepts WebHook requests from an open-ended number of services.</span></span> <span data-ttu-id="8b757-114">请求到达时，它会选择已安装的用于处理特定 WebHook 发送方的相应接收器。</span><span class="sxs-lookup"><span data-stu-id="8b757-114">When a request arrives, it picks the appropriate receiver that you have installed for handling a particular WebHook sender.</span></span>

<span data-ttu-id="8b757-115">此控制器的 URI 是您向服务注册的 WebHook URI，其形式为：</span><span class="sxs-lookup"><span data-stu-id="8b757-115">The URI of this controller is the WebHook URI that you register with the service and is of the form:</span></span>

```
https://<host>/api/webhooks/incoming/<receiver>/{id}
```

<span data-ttu-id="8b757-116">出于安全原因，许多 WebHook 接收器要求 URI 是*https* URI，在某些情况下，它还必须包含一个额外的查询参数，用于强制只有目标方才能将 WebHook 发送到上述 URI。</span><span class="sxs-lookup"><span data-stu-id="8b757-116">For security reasons, many WebHook receivers require that the URI is an *https* URI and in some cases it must also contain an additional query parameter which is used to enforce that only the intended party can send WebHooks to the URI above.</span></span>

<span data-ttu-id="8b757-117">组件`<receiver>`是接收器的名称，例如`github`或`slack`。</span><span class="sxs-lookup"><span data-stu-id="8b757-117">The `<receiver>` component is the name of the receiver, for example `github` or `slack`.</span></span>

<span data-ttu-id="8b757-118">*{id}* 是一个可选标识符，可用于标识特定的 WebHook 接收器配置。</span><span class="sxs-lookup"><span data-stu-id="8b757-118">The *{id}* is an optional identifier which can be used to identify a particular WebHook receiver configuration.</span></span> <span data-ttu-id="8b757-119">这可用于向特定接收器注册 N WebHook。</span><span class="sxs-lookup"><span data-stu-id="8b757-119">This can be used to register N WebHooks with a particular receiver.</span></span> <span data-ttu-id="8b757-120">例如，以下三个 URI 可用于注册三个独立的 WebHook：</span><span class="sxs-lookup"><span data-stu-id="8b757-120">For example, the following three URIs can be used to register for three independent WebHooks:</span></span>

```
https://<host>/api/webhooks/incoming/github
https://<host>/api/webhooks/incoming/github/12345
https://<host>/api/webhooks/incoming/github/54321
```

## <a name="installing-a-webhook-receiver"></a><span data-ttu-id="8b757-121">安装 WebHook 接收器</span><span class="sxs-lookup"><span data-stu-id="8b757-121">Installing a WebHook Receiver</span></span>

<span data-ttu-id="8b757-122">要使用 Microsoft ASP.NET WebHook 接收 WebHook，请首先为要接收 WebHook 的 WebHook 提供商或提供商安装 Nuget 包。</span><span class="sxs-lookup"><span data-stu-id="8b757-122">To receive WebHooks using Microsoft ASP.NET WebHooks, you first install the Nuget package for the WebHook provider or providers you want to receive WebHooks from.</span></span> <span data-ttu-id="8b757-123">Nuget 包名为[Microsoft.AspNet.WebHooks.Receivers.\*，](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers)其中最后一部分表示支持的服务。</span><span class="sxs-lookup"><span data-stu-id="8b757-123">The Nuget packages are named [Microsoft.AspNet.WebHooks.Receivers.\*](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers) where the last part indicates the service supported.</span></span> <span data-ttu-id="8b757-124">例如：</span><span class="sxs-lookup"><span data-stu-id="8b757-124">For example</span></span>

<span data-ttu-id="8b757-125">[微软.AspNet.WebHooks.Receivers.GitHub](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.GitHub)支持接收来自GitHub和[微软的WebHook.AspNet.WebHooks.Receivers.Customs.Customs](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.Custom)为接收由ASP.NETWebHooks生成的WebHook提供支持。</span><span class="sxs-lookup"><span data-stu-id="8b757-125">[Microsoft.AspNet.WebHooks.Receivers.GitHub](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.GitHub) provides support for receiving WebHooks from GitHub and [Microsoft.AspNet.WebHooks.Receivers.Custom](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.Custom) provides support for receiving WebHooks generated by ASP.NET WebHooks.</span></span>

<span data-ttu-id="8b757-126">开箱即用，您可以找到对 Dropbox、GitHub、MailChimp、PayPal、Pusher、Salesforce、Slack、Stripe、Trello 和 WordPress 的支持，但可以支持任意数量的其他提供商。</span><span class="sxs-lookup"><span data-stu-id="8b757-126">Out of the box you can find support for Dropbox, GitHub, MailChimp, PayPal, Pusher, Salesforce, Slack, Stripe, Trello, and WordPress but it is possible to support any number of other providers.</span></span>

## <a name="configuring-a-webhook-receiver"></a><span data-ttu-id="8b757-127">配置 WebHook 接收器</span><span class="sxs-lookup"><span data-stu-id="8b757-127">Configuring a WebHook Receiver</span></span>

<span data-ttu-id="8b757-128">WebHook 接收器通过[IWebHookReceiverConfig 整](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/IWebHookReceiverConfig.cs)面进行配置，该接口的特定实现可以使用任何依赖项注入模型进行注册。</span><span class="sxs-lookup"><span data-stu-id="8b757-128">WebHook Receivers are configured through the [IWebHookReceiverConfig](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/IWebHookReceiverConfig.cs) inteface and particular implementations of that interface can be registered using any dependency injection model.</span></span> <span data-ttu-id="8b757-129">默认实现使用应用程序设置，可以在 Web.config 文件中设置，或者，如果使用 Azure Web 应用，可以通过[Azure 门户](https://portal.azure.com/)进行设置。</span><span class="sxs-lookup"><span data-stu-id="8b757-129">The default implementation uses Application Settings which can either be set in the Web.config file, or, if using Azure Web Apps, can be set through the [Azure Portal](https://portal.azure.com/).</span></span>

![Azure 应用设置](_static/AzureAppSettings.png)

<span data-ttu-id="8b757-131">应用程序设置键的格式如下：</span><span class="sxs-lookup"><span data-stu-id="8b757-131">The format for Application Setting keys is as follows:</span></span>

```
MS_WebHookReceiverSecret_<receiver>
```

<span data-ttu-id="8b757-132">该值是与已注册 WebHook 的 *[id]* 值匹配的逗号分隔的值列表，例如：</span><span class="sxs-lookup"><span data-stu-id="8b757-132">The value is a comma-separated list of values matching the *{id}* values for which WebHooks have been registered, for example:</span></span>

```
MS_WebHookReceiverSecret_GitHub = <secret1>, 12345=<secret2>, 54321=<secret3>
```

## <a name="initializing-a-webhook-receiver"></a><span data-ttu-id="8b757-133">初始化 WebHook 接收器</span><span class="sxs-lookup"><span data-stu-id="8b757-133">Initializing a WebHook Receiver</span></span>

<span data-ttu-id="8b757-134">WebHook 接收器通过注册来初始化，通常在*WebApiConfig*静态类中，例如：</span><span class="sxs-lookup"><span data-stu-id="8b757-134">WebHook Receivers are initialized by registering them, typically in the *WebApiConfig* static class, for example:</span></span>

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

---
uid: webhooks/index
title: ASP.NET网页概述 |微软文档
author: rick-anderson
description: ASP.NET网络钩子的简介。
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 5e2843f0-f499-448f-a712-33d4e9858321
ms.openlocfilehash: aa5fa190386ec803a6801de2d815c948677fe1f5
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675432"
---
# <a name="aspnet-webhooks-overview"></a><span data-ttu-id="86c74-103">ASP.NET WebHooks 概述</span><span class="sxs-lookup"><span data-stu-id="86c74-103">ASP.NET WebHooks overview</span></span>

<span data-ttu-id="86c74-104">WebHooks 是一种轻量级的 HTTP 模式，提供简单的 pub/子模型，用于将 Web API 和 SaaS 服务连接在一起。</span><span class="sxs-lookup"><span data-stu-id="86c74-104">WebHooks is a lightweight HTTP pattern providing a simple pub/sub model for wiring together Web APIs and SaaS services.</span></span> <span data-ttu-id="86c74-105">当服务中发生事件时，通知以 HTTP POST 请求的形式发送给注册订阅者。</span><span class="sxs-lookup"><span data-stu-id="86c74-105">When an event happens in a service, a notification is sent in the form of an HTTP POST request to registered subscribers.</span></span> <span data-ttu-id="86c74-106">POST 请求包含有关事件的信息，使接收方能够采取相应行动。</span><span class="sxs-lookup"><span data-stu-id="86c74-106">The POST request contains information about the event which makes it possible for the receiver to act accordingly.</span></span>

<span data-ttu-id="86c74-107">由于其简单性，WebHook已经暴露出大量的服务，包括[Dropbox，GitHub，](http://dropbox.com/)[比特巴克](https://bitbucket.org/)[GitHub](https://www.github.com/)[，MailChimp，PayPal，](http://www.mailchimp.com/)[松弛](http://www.slack.com)，[PayPal](http://www.paypal.com/)[条纹](http://www.stripe.com)，[特雷洛](http://www.trello.com/)，以及更多。</span><span class="sxs-lookup"><span data-stu-id="86c74-107">Because of their simplicity, WebHooks are already exposed by a large number of services including [Dropbox](http://dropbox.com/), [GitHub](https://www.github.com/), [Bitbucket](https://bitbucket.org/), [MailChimp](http://www.mailchimp.com/), [PayPal](http://www.paypal.com/), [Slack](http://www.slack.com), [Stripe](http://www.stripe.com), [Trello](http://www.trello.com/), and many more.</span></span> <span data-ttu-id="86c74-108">例如，WebHook 可以指示[Dropbox](http://dropbox.com/)中的文件已更改，或者已在 GitHub 中提交代码更改，或者已在[PayPal](http://www.paypal.com/)中启动付款，或者已在[Trello](http://www.trello.com/)中创建了一张卡。</span><span class="sxs-lookup"><span data-stu-id="86c74-108">For example, a WebHook can indicate that a file has changed in [Dropbox](http://dropbox.com/), or a code change has been committed in GitHub, or a payment has been initiated in [PayPal](http://www.paypal.com/), or a card has been created in [Trello](http://www.trello.com/).</span></span> <span data-ttu-id="86c74-109">可能性是无穷无尽的！</span><span class="sxs-lookup"><span data-stu-id="86c74-109">The possibilities are endless!</span></span>

<span data-ttu-id="86c74-110">Microsoft ASP.NET WebHooks 使发送和接收 WebHook 变得更容易，作为ASP.NET应用程序的一部分：</span><span class="sxs-lookup"><span data-stu-id="86c74-110">Microsoft ASP.NET WebHooks makes it easier to both send and receive WebHooks as part of your ASP.NET application:</span></span>

* <span data-ttu-id="86c74-111">在接收端，它提供了一个用于接收和处理来自任意数量的 WebHook 提供商的 WebHook 的通用模型。</span><span class="sxs-lookup"><span data-stu-id="86c74-111">On the receiving side, it provides a common model for receiving and processing WebHooks from any number of WebHook providers.</span></span> <span data-ttu-id="86c74-112">它出来的盒子与[支持Dropbox，GitHub，](http://dropbox.com/)[比特巴克](https://bitbucket.org/)[，MailChimp，](http://www.mailchimp.com/)[贝宝](http://www.paypal.com/)，[推手](http://www.pusher.com)，[销售部队](http://www.salesforce.com)，[松弛](http://www.slack.com)，[条纹](http://www.stripe.com)，[特雷洛](http://www.trello.com/)[，WordPress](http://www.wordpress.com)和[Zendesk，](https://www.zendesk.com/)但它是很容易添加支持更多。 [GitHub](https://www.github.com/)</span><span class="sxs-lookup"><span data-stu-id="86c74-112">It comes out of the box with support for [Dropbox](http://dropbox.com/), [GitHub](https://www.github.com/), [Bitbucket](https://bitbucket.org/), [MailChimp](http://www.mailchimp.com/), [PayPal](http://www.paypal.com/), [Pusher](http://www.pusher.com), [Salesforce](http://www.salesforce.com), [Slack](http://www.slack.com), [Stripe](http://www.stripe.com), [Trello](http://www.trello.com/),[WordPress](http://www.wordpress.com) and [Zendesk](https://www.zendesk.com/) but it is easy to add support for more.</span></span>

* <span data-ttu-id="86c74-113">在发送端，它支持管理和存储订阅以及向正确的订阅者集发送事件通知。</span><span class="sxs-lookup"><span data-stu-id="86c74-113">On the sending side it provides support for managing and storing subscriptions as well as for sending event notifications to the right set of subscribers.</span></span> <span data-ttu-id="86c74-114">这允许您定义您自己的事件集，订阅者可以订阅这些事件，并在事件发生时通知它们。</span><span class="sxs-lookup"><span data-stu-id="86c74-114">This allows you to define your own set of events that subscribers can subscribe to and notify them when things happens.</span></span>

<span data-ttu-id="86c74-115">这两个部分可以一起使用，也可以分开使用，具体取决于您的方案。</span><span class="sxs-lookup"><span data-stu-id="86c74-115">The two parts can be used together or apart depending on your scenario.</span></span> <span data-ttu-id="86c74-116">如果您只需要从其他服务接收 WebHook，则只需使用接收方部件;如果你只想公开WebHook供他人使用，那么你可以这样做。</span><span class="sxs-lookup"><span data-stu-id="86c74-116">If you only need to receive WebHooks from other services then you can use just the receiver part; if you only want to expose WebHooks for others to consume, then you can do just that.</span></span>

<span data-ttu-id="86c74-117">代码以web API 2ASP.NET，ASP.NET MVC 5，在[GitHub 上作为 OSS](https://github.com/aspnet/WebHooks)提供。</span><span class="sxs-lookup"><span data-stu-id="86c74-117">The code targets ASP.NET Web API 2 and ASP.NET MVC 5 and is available as [OSS on GitHub](https://github.com/aspnet/WebHooks).</span></span>

## <a name="webhooks-overview"></a><span data-ttu-id="86c74-118">网页概述</span><span class="sxs-lookup"><span data-stu-id="86c74-118">WebHooks Overview</span></span>

<span data-ttu-id="86c74-119">WebHooks 是一种模式，这意味着它因服务而异，但基本思想是相同的。</span><span class="sxs-lookup"><span data-stu-id="86c74-119">WebHooks is a pattern which means that it varies how it is used from service to service but the basic idea is the same.</span></span> <span data-ttu-id="86c74-120">您可以将 WebHooks 视为一个简单的 pub/子模型，用户可以订阅在其他地方发生的事件。</span><span class="sxs-lookup"><span data-stu-id="86c74-120">You can think of WebHooks as a simple pub/sub model where a user can subscribe to events happening elsewhere.</span></span> <span data-ttu-id="86c74-121">事件通知作为 HTTP POST 请求传播，其中包含有关事件本身的信息。</span><span class="sxs-lookup"><span data-stu-id="86c74-121">The event notifications are propagated as HTTP POST requests containing information about the event itself.</span></span>

<span data-ttu-id="86c74-122">通常，HTTP POST 请求包含由 WebHook 发送方确定的 JSON 对象或 HTML 表单数据，包括有关导致 WebHook 触发的事件的信息。</span><span class="sxs-lookup"><span data-stu-id="86c74-122">Typically the HTTP POST request contains a JSON object or HTML form data determined by the WebHook sender including information about the event causing the WebHook to trigger.</span></span> <span data-ttu-id="86c74-123">例如，由于在特定存储库中打开新问题[，GitHub](https://www.github.com/)的 WebHook POST 请求正文如下所示：</span><span class="sxs-lookup"><span data-stu-id="86c74-123">For example, a WebHook POST request body from [GitHub](https://www.github.com/) looks like this as a result of a new issue being opened in a particular repository:</span></span>

```json
{
  "action": "opened",
  "issue": {
      "url": "https://api.github.com/repos/octocat/Hello-World/issues/1347",
      "number": 1347,
      ...
  },
  "repository": {
      "id": 1296269,
      "full_name": "octocat/Hello-World",
      "owner": {
          "login": "octocat",
          "id": 1
          ...
      },
      ...
  },
  "sender": {
      "login": "octocat",
      "id": 1,
      ...
  }
}
```

<span data-ttu-id="86c74-124">为了确保 WebHook 确实来自预期的发送方，POST 请求以某种方式受到保护，然后由接收方进行验证。</span><span class="sxs-lookup"><span data-stu-id="86c74-124">To ensure that the WebHook is indeed from the intended sender, the POST request is secured in some way and then verified by the receiver.</span></span> <span data-ttu-id="86c74-125">例如[，GitHub WebHooks](https://developer.github.com/webhooks/)包括一个*X-Hub 签名*HTTP 标头，其中包含请求正文的哈希，由接收方实现进行检查，因此您不必担心。</span><span class="sxs-lookup"><span data-stu-id="86c74-125">For example, [GitHub WebHooks](https://developer.github.com/webhooks/) includes an *X-Hub-Signature* HTTP header with a hash of the request body which is checked by the receiver implementation so you don't have to worry about it.</span></span>

<span data-ttu-id="86c74-126">WebHook 流通常如下所示：</span><span class="sxs-lookup"><span data-stu-id="86c74-126">The WebHook flow generally goes something like this:</span></span>

* <span data-ttu-id="86c74-127">WebHook 发送方公开客户端可以订阅的事件。</span><span class="sxs-lookup"><span data-stu-id="86c74-127">The WebHook sender exposes events that a client can subscribe to.</span></span> <span data-ttu-id="86c74-128">这些事件描述对系统的可观察更改，例如插入了新的数据项、进程已完成或其他内容。</span><span class="sxs-lookup"><span data-stu-id="86c74-128">The events describe observable changes to the system, for example that a new data item has been inserted, that a process has completed, or something else.</span></span>

* <span data-ttu-id="86c74-129">WebHook 接收器通过注册包含四个内容的 WebHook 进行订阅：</span><span class="sxs-lookup"><span data-stu-id="86c74-129">The WebHook receiver subscribes by registering a WebHook consisting of four things:</span></span>

     1. <span data-ttu-id="86c74-130">以 HTTP POST 请求的形式发布事件通知的 URI;</span><span class="sxs-lookup"><span data-stu-id="86c74-130">A URI for where the event notification should be posted in the form of an HTTP POST request;</span></span>

     2. <span data-ttu-id="86c74-131">一组筛选器，描述应为其触发 WebHook 的特定事件;</span><span class="sxs-lookup"><span data-stu-id="86c74-131">A set of filters describing the particular events for which the WebHook should be fired;</span></span>

     3. <span data-ttu-id="86c74-132">用于对 HTTP POST 请求进行签名的密钥;</span><span class="sxs-lookup"><span data-stu-id="86c74-132">A secret key which is used to sign the HTTP POST request;</span></span>

     4. <span data-ttu-id="86c74-133">要包含在 HTTP POST 请求中的其他数据。</span><span class="sxs-lookup"><span data-stu-id="86c74-133">Additional data which is to be included in the HTTP POST request.</span></span> <span data-ttu-id="86c74-134">例如，这可以是 HTTP POST 请求正文中包含的其他 HTTP 标头字段或属性。</span><span class="sxs-lookup"><span data-stu-id="86c74-134">This can for example be additional HTTP header fields or properties included in the HTTP POST request body.</span></span>

* <span data-ttu-id="86c74-135">事件发生后，将找到匹配的 WebHook 注册，并提交 HTTP POST 请求。</span><span class="sxs-lookup"><span data-stu-id="86c74-135">Once an event happens, the matching WebHook registrations are found and HTTP POST requests are submitted.</span></span> <span data-ttu-id="86c74-136">通常，如果收件人由于某种原因未响应或 HTTP POST 请求导致错误响应，则多次重试 HTTP POST 请求的生成。</span><span class="sxs-lookup"><span data-stu-id="86c74-136">Typically, the generation of the HTTP POST requests are retried several times if for some reason the recipient is not responding or the HTTP POST request results in an error response.</span></span>

## <a name="webhooks-processing-pipeline"></a><span data-ttu-id="86c74-137">WebHooks 处理管道</span><span class="sxs-lookup"><span data-stu-id="86c74-137">WebHooks Processing Pipeline</span></span>

<span data-ttu-id="86c74-138">Microsoft ASP.NET WebHooks 处理管道以访问传入 WebHook 如下所示：</span><span class="sxs-lookup"><span data-stu-id="86c74-138">The Microsoft ASP.NET WebHooks processing pipeline for incoming WebHooks looks like this:</span></span>

![ASP.NET WebHooks 处理管道](_static/WebHookReceivers.png)

<span data-ttu-id="86c74-140">这里的两个关键概念是*接收器*和*处理程序*：</span><span class="sxs-lookup"><span data-stu-id="86c74-140">The two key concepts here are *Receivers* and *Handlers*:</span></span>

* <span data-ttu-id="86c74-141">*接收方*负责处理来自给定发件人的 WebHook 的特定风格，并强制进行安全检查，以确保 WebHook 请求确实来自预期的发件人。</span><span class="sxs-lookup"><span data-stu-id="86c74-141">*Receivers* are responsible for handling the particular flavor of WebHook from a given sender and for enforcing security checks to ensure that the WebHook request indeed is from the intended sender.</span></span>

* <span data-ttu-id="86c74-142">*处理程序*通常是用户代码运行处理特定 WebHook 的位置。</span><span class="sxs-lookup"><span data-stu-id="86c74-142">*Handlers* are typically where user code runs processing the particular WebHook.</span></span>

<span data-ttu-id="86c74-143">在以下节点中，这些概念将更详细地描述。</span><span class="sxs-lookup"><span data-stu-id="86c74-143">In the following nodes these concepts are described in more details.</span></span>

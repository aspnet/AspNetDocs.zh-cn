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
# <a name="aspnet-webhooks-overview"></a>ASP.NET WebHooks 概述

WebHooks 是一种轻量级的 HTTP 模式，提供简单的 pub/子模型，用于将 Web API 和 SaaS 服务连接在一起。 当服务中发生事件时，通知以 HTTP POST 请求的形式发送给注册订阅者。 POST 请求包含有关事件的信息，使接收方能够采取相应行动。

由于其简单性，WebHook已经暴露出大量的服务，包括[Dropbox，GitHub，](http://dropbox.com/)[比特巴克](https://bitbucket.org/)[GitHub](https://www.github.com/)[，MailChimp，PayPal，](http://www.mailchimp.com/)[松弛](http://www.slack.com)，[PayPal](http://www.paypal.com/)[条纹](http://www.stripe.com)，[特雷洛](http://www.trello.com/)，以及更多。 例如，WebHook 可以指示[Dropbox](http://dropbox.com/)中的文件已更改，或者已在 GitHub 中提交代码更改，或者已在[PayPal](http://www.paypal.com/)中启动付款，或者已在[Trello](http://www.trello.com/)中创建了一张卡。 可能性是无穷无尽的！

Microsoft ASP.NET WebHooks 使发送和接收 WebHook 变得更容易，作为ASP.NET应用程序的一部分：

* 在接收端，它提供了一个用于接收和处理来自任意数量的 WebHook 提供商的 WebHook 的通用模型。 它出来的盒子与[支持Dropbox，GitHub，](http://dropbox.com/)[比特巴克](https://bitbucket.org/)[，MailChimp，](http://www.mailchimp.com/)[贝宝](http://www.paypal.com/)，[推手](http://www.pusher.com)，[销售部队](http://www.salesforce.com)，[松弛](http://www.slack.com)，[条纹](http://www.stripe.com)，[特雷洛](http://www.trello.com/)[，WordPress](http://www.wordpress.com)和[Zendesk，](https://www.zendesk.com/)但它是很容易添加支持更多。 [GitHub](https://www.github.com/)

* 在发送端，它支持管理和存储订阅以及向正确的订阅者集发送事件通知。 这允许您定义您自己的事件集，订阅者可以订阅这些事件，并在事件发生时通知它们。

这两个部分可以一起使用，也可以分开使用，具体取决于您的方案。 如果您只需要从其他服务接收 WebHook，则只需使用接收方部件;如果你只想公开WebHook供他人使用，那么你可以这样做。

代码以web API 2ASP.NET，ASP.NET MVC 5，在[GitHub 上作为 OSS](https://github.com/aspnet/WebHooks)提供。

## <a name="webhooks-overview"></a>网页概述

WebHooks 是一种模式，这意味着它因服务而异，但基本思想是相同的。 您可以将 WebHooks 视为一个简单的 pub/子模型，用户可以订阅在其他地方发生的事件。 事件通知作为 HTTP POST 请求传播，其中包含有关事件本身的信息。

通常，HTTP POST 请求包含由 WebHook 发送方确定的 JSON 对象或 HTML 表单数据，包括有关导致 WebHook 触发的事件的信息。 例如，由于在特定存储库中打开新问题[，GitHub](https://www.github.com/)的 WebHook POST 请求正文如下所示：

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

为了确保 WebHook 确实来自预期的发送方，POST 请求以某种方式受到保护，然后由接收方进行验证。 例如[，GitHub WebHooks](https://developer.github.com/webhooks/)包括一个*X-Hub 签名*HTTP 标头，其中包含请求正文的哈希，由接收方实现进行检查，因此您不必担心。

WebHook 流通常如下所示：

* WebHook 发送方公开客户端可以订阅的事件。 这些事件描述对系统的可观察更改，例如插入了新的数据项、进程已完成或其他内容。

* WebHook 接收器通过注册包含四个内容的 WebHook 进行订阅：

     1. 以 HTTP POST 请求的形式发布事件通知的 URI;

     2. 一组筛选器，描述应为其触发 WebHook 的特定事件;

     3. 用于对 HTTP POST 请求进行签名的密钥;

     4. 要包含在 HTTP POST 请求中的其他数据。 例如，这可以是 HTTP POST 请求正文中包含的其他 HTTP 标头字段或属性。

* 事件发生后，将找到匹配的 WebHook 注册，并提交 HTTP POST 请求。 通常，如果收件人由于某种原因未响应或 HTTP POST 请求导致错误响应，则多次重试 HTTP POST 请求的生成。

## <a name="webhooks-processing-pipeline"></a>WebHooks 处理管道

Microsoft ASP.NET WebHooks 处理管道以访问传入 WebHook 如下所示：

![ASP.NET WebHooks 处理管道](_static/WebHookReceivers.png)

这里的两个关键概念是*接收器*和*处理程序*：

* *接收方*负责处理来自给定发件人的 WebHook 的特定风格，并强制进行安全检查，以确保 WebHook 请求确实来自预期的发件人。

* *处理程序*通常是用户代码运行处理特定 WebHook 的位置。

在以下节点中，这些概念将更详细地描述。

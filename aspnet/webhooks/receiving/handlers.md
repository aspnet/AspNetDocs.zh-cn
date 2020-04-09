---
uid: webhooks/receiving/handlers
title: ASP.NET WebHook 处理程序 |微软文档
author: rick-anderson
description: 如何处理ASP.NET WebHook 中的请求。
ms.author: riande
ms.date: 01/17/2012
ms.assetid: a55b0d20-9c90-4bd3-a471-20da6f569f0c
ms.openlocfilehash: ff12dd8df167eca17ecbd9f03a71807d44af2b30
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675215"
---
# <a name="aspnet-webhooks-handlers"></a>ASP.NET WebHook 处理程序

WebHooks 请求由 WebHook 接收器验证后，即可由用户代码处理。 这是*处理程序*的来向。 处理程序派生自[IWebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs)接口，但通常使用[WebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs)类，而不是直接从该接口派生。

WebHook 请求可以由一个或多个处理程序处理。 处理程序根据各自的*Order*属性从最低到最高的顺序调用，其中 Order 是一个简单的整数（建议介于 1 和 100 之间）：

![WebHook 处理程序顺序属性图](_static/Handlers.png)

处理程序可以选择在 WebHookHandlerContext 上设置*响应*属性，这将导致处理停止，并将响应作为对 WebHook 的 HTTP 响应发送回来。 在上面的案例中，不会调用处理程序 C，因为它的顺序高于 B，B 设置响应。

设置响应通常只与 WebHook 相关，响应可以将信息回源 API。 例如，Slack WebHooks 的响应被发回 WebHook 的通道。 如果处理程序只想从该特定接收器接收 WebHook，则可以设置 Receiver 属性。 如果他们不设置接收器，他们被要求所有这些。

响应的另一个常见用途是使用*410 Gone*响应来指示 WebHook 不再处于活动状态，并且不应提交进一步的请求。

默认情况下，所有 WebHook 接收器都将调用处理程序。 但是，如果*Receiver*属性设置为处理程序的名称，则该处理程序将仅接收来自该接收方的 WebHook 请求。

## <a name="processing-a-webhook"></a>处理 WebHook

调用处理程序时，它会获取包含有关 WebHook 请求的信息的[WebHook处理程序。](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandlerContext.cs) 数据（通常是 HTTP 请求正文）可从*Data*属性获得。

数据类型通常是 JSON 或 HTML 表单数据，但如果需要，可以强制转换为更具体的类型。 例如，ASP.NET WebHooks 生成的自定义 WebHook 可以转换为["自定义通知"](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers.Custom/WebHooks/CustomNotifications.cs)类型，如下所示：

```csharp
public class MyWebHookHandler : WebHookHandler
{
    public MyWebHookHandler()
    {
        this.Receiver = "custom";
    }

    public override Task ExecuteAsync(string generator, WebHookHandlerContext context)
    {
        CustomNotifications notifications = context.GetDataOrDefault<CustomNotifications>();
        foreach (var notification in notifications.Notifications)
        {
            ...
        }
        return Task.FromResult(true);
    }
}
```

  ## <a name="queued-processing"></a>排队处理

如果在几秒钟内未生成响应，大多数 WebHook 发送方将重新发送 WebHook。 这意味着处理程序必须在该时间范围内完成处理，以便不要再次调用它。

如果处理时间较长，或者最好单独处理，则[WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs)可用于将 WebHook 请求提交到队列，例如 Azure[存储队列](https://msdn.microsoft.com/library/azure/dd179353.aspx)。

此处提供了[WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs)实现的概要：

```csharp
public class QueueHandler : WebHookQueueHandler
{
    public override Task EnqueueAsync(WebHookQueueContext context)
    {

        // Enqueue WebHookQueueContext to your queuing system of choice

        return Task.FromResult(true);
    }
}
```

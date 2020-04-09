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
# <a name="aspnet-webhooks-handlers"></a><span data-ttu-id="cf770-103">ASP.NET WebHook 处理程序</span><span class="sxs-lookup"><span data-stu-id="cf770-103">ASP.NET WebHooks handlers</span></span>

<span data-ttu-id="cf770-104">WebHooks 请求由 WebHook 接收器验证后，即可由用户代码处理。</span><span class="sxs-lookup"><span data-stu-id="cf770-104">Once WebHooks requests has been validated by a WebHook receiver, it is ready to be processed by user code.</span></span> <span data-ttu-id="cf770-105">这是*处理程序*的来向。</span><span class="sxs-lookup"><span data-stu-id="cf770-105">This is where *handlers* come in.</span></span> <span data-ttu-id="cf770-106">处理程序派生自[IWebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs)接口，但通常使用[WebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs)类，而不是直接从该接口派生。</span><span class="sxs-lookup"><span data-stu-id="cf770-106">Handlers derive from the [IWebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) interface but typically uses the [WebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) class instead of deriving directly from the interface.</span></span>

<span data-ttu-id="cf770-107">WebHook 请求可以由一个或多个处理程序处理。</span><span class="sxs-lookup"><span data-stu-id="cf770-107">A WebHook request can be processed by one or more handlers.</span></span> <span data-ttu-id="cf770-108">处理程序根据各自的*Order*属性从最低到最高的顺序调用，其中 Order 是一个简单的整数（建议介于 1 和 100 之间）：</span><span class="sxs-lookup"><span data-stu-id="cf770-108">Handlers are called in order based on their respective *Order* property going from lowest to highest where Order is a simple integer (suggested to be between 1 and 100):</span></span>

![WebHook 处理程序顺序属性图](_static/Handlers.png)

<span data-ttu-id="cf770-110">处理程序可以选择在 WebHookHandlerContext 上设置*响应*属性，这将导致处理停止，并将响应作为对 WebHook 的 HTTP 响应发送回来。</span><span class="sxs-lookup"><span data-stu-id="cf770-110">A handler can optionally set the *Response* property on the WebHookHandlerContext which will lead the processing to stop and the response to be sent back as the HTTP response to the WebHook.</span></span> <span data-ttu-id="cf770-111">在上面的案例中，不会调用处理程序 C，因为它的顺序高于 B，B 设置响应。</span><span class="sxs-lookup"><span data-stu-id="cf770-111">In the case above, Handler C won't get called because it has a higher order than B and B sets the response.</span></span>

<span data-ttu-id="cf770-112">设置响应通常只与 WebHook 相关，响应可以将信息回源 API。</span><span class="sxs-lookup"><span data-stu-id="cf770-112">Setting the response is typically only relevant for WebHooks where the response can carry information back to the originating API.</span></span> <span data-ttu-id="cf770-113">例如，Slack WebHooks 的响应被发回 WebHook 的通道。</span><span class="sxs-lookup"><span data-stu-id="cf770-113">This is for example the case with Slack WebHooks where the response is posted back to the channel where the WebHook came from.</span></span> <span data-ttu-id="cf770-114">如果处理程序只想从该特定接收器接收 WebHook，则可以设置 Receiver 属性。</span><span class="sxs-lookup"><span data-stu-id="cf770-114">Handlers can set the Receiver property if they only want to receive WebHooks from that particular receiver.</span></span> <span data-ttu-id="cf770-115">如果他们不设置接收器，他们被要求所有这些。</span><span class="sxs-lookup"><span data-stu-id="cf770-115">If they don't set the receiver they are called for all of them.</span></span>

<span data-ttu-id="cf770-116">响应的另一个常见用途是使用*410 Gone*响应来指示 WebHook 不再处于活动状态，并且不应提交进一步的请求。</span><span class="sxs-lookup"><span data-stu-id="cf770-116">One other common use of a response is to use a *410 Gone* response to indicate that the WebHook no longer is active and no further requests should be submitted.</span></span>

<span data-ttu-id="cf770-117">默认情况下，所有 WebHook 接收器都将调用处理程序。</span><span class="sxs-lookup"><span data-stu-id="cf770-117">By default a handler will be called by all WebHook receivers.</span></span> <span data-ttu-id="cf770-118">但是，如果*Receiver*属性设置为处理程序的名称，则该处理程序将仅接收来自该接收方的 WebHook 请求。</span><span class="sxs-lookup"><span data-stu-id="cf770-118">However, if the *Receiver* property is set to the name of a handler then that handler will only receive WebHook requests from that receiver.</span></span>

## <a name="processing-a-webhook"></a><span data-ttu-id="cf770-119">处理 WebHook</span><span class="sxs-lookup"><span data-stu-id="cf770-119">Processing a WebHook</span></span>

<span data-ttu-id="cf770-120">调用处理程序时，它会获取包含有关 WebHook 请求的信息的[WebHook处理程序。](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandlerContext.cs)</span><span class="sxs-lookup"><span data-stu-id="cf770-120">When a handler is called, it gets a [WebHookHandlerContext](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandlerContext.cs) containing information about the WebHook request.</span></span> <span data-ttu-id="cf770-121">数据（通常是 HTTP 请求正文）可从*Data*属性获得。</span><span class="sxs-lookup"><span data-stu-id="cf770-121">The data, typically the HTTP request body, is available from the *Data* property.</span></span>

<span data-ttu-id="cf770-122">数据类型通常是 JSON 或 HTML 表单数据，但如果需要，可以强制转换为更具体的类型。</span><span class="sxs-lookup"><span data-stu-id="cf770-122">The type of the data is typically JSON or HTML form data, but it is possible to cast to a more specific type if desired.</span></span> <span data-ttu-id="cf770-123">例如，ASP.NET WebHooks 生成的自定义 WebHook 可以转换为["自定义通知"](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers.Custom/WebHooks/CustomNotifications.cs)类型，如下所示：</span><span class="sxs-lookup"><span data-stu-id="cf770-123">For example, the custom WebHooks generated by ASP.NET WebHooks can be cast to the type [CustomNotifications](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers.Custom/WebHooks/CustomNotifications.cs) as follows:</span></span>

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

  ## <a name="queued-processing"></a><span data-ttu-id="cf770-124">排队处理</span><span class="sxs-lookup"><span data-stu-id="cf770-124">Queued Processing</span></span>

<span data-ttu-id="cf770-125">如果在几秒钟内未生成响应，大多数 WebHook 发送方将重新发送 WebHook。</span><span class="sxs-lookup"><span data-stu-id="cf770-125">Most WebHook senders will resend a WebHook if a response is not generated within a handful of seconds.</span></span> <span data-ttu-id="cf770-126">这意味着处理程序必须在该时间范围内完成处理，以便不要再次调用它。</span><span class="sxs-lookup"><span data-stu-id="cf770-126">This means that your handler must complete the processing within that time frame in order not for it to be called again.</span></span>

<span data-ttu-id="cf770-127">如果处理时间较长，或者最好单独处理，则[WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs)可用于将 WebHook 请求提交到队列，例如 Azure[存储队列](https://msdn.microsoft.com/library/azure/dd179353.aspx)。</span><span class="sxs-lookup"><span data-stu-id="cf770-127">If the processing takes longer, or is better handled separately then the [WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) can be used to submit the WebHook request to a queue, for example [Azure Storage Queue](https://msdn.microsoft.com/library/azure/dd179353.aspx).</span></span>

<span data-ttu-id="cf770-128">此处提供了[WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs)实现的概要：</span><span class="sxs-lookup"><span data-stu-id="cf770-128">An outline of a [WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) implementation is provided here:</span></span>

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

---
uid: aspnet/overview/owin-and-katana/katana-samples
title: 卡塔纳样品 |微软文档
author: rick-anderson
description: ''
ms.author: riande
ms.date: 01/17/2014
ms.assetid: bec04f5d-2638-4417-b288-97c58c8d6379
msc.legacyurl: /aspnet/overview/owin-and-katana/katana-samples
msc.type: authoredcontent
ms.openlocfilehash: 15cc1084b16db2619f2295ee21dec4f49eb2e354
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81540436"
---
# <a name="katana-samples"></a><span data-ttu-id="a0249-102">Katana 示例</span><span class="sxs-lookup"><span data-stu-id="a0249-102">Katana Samples</span></span>

<span data-ttu-id="a0249-103">由[微软](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="a0249-103">by [Microsoft](https://github.com/microsoft)</span></span>

## <a name="katana-samples"></a><span data-ttu-id="a0249-104">Katana 示例</span><span class="sxs-lookup"><span data-stu-id="a0249-104">Katana Samples</span></span>

<span data-ttu-id="a0249-105">**ASP.NET路由示例** | [源代码](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/AspNetRoutes)</span><span class="sxs-lookup"><span data-stu-id="a0249-105">**ASP.NET Routes Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/AspNetRoutes)</span></span>  
<span data-ttu-id="a0249-106">在某些应用程序中，您需要将Asp.Net路由表中的 OWIN 组件与非 OWIN 组件并排连接。</span><span class="sxs-lookup"><span data-stu-id="a0249-106">In some applications you will want to hook up OWIN components in the Asp.Net route table side by side with non-OWIN components.</span></span> <span data-ttu-id="a0249-107">此示例演示如何使用 Microsoft.Owin.Host.SystemWeb 提供的路由收集扩展方法 MapOwinPath 和 MapOwinRoute。</span><span class="sxs-lookup"><span data-stu-id="a0249-107">This sample shows how to use the RouteCollection extension methods MapOwinPath and MapOwinRoute provided by Microsoft.Owin.Host.SystemWeb.</span></span>

<span data-ttu-id="a0249-108">**分支管道示例** | [源代码](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/BranchingPipelines)</span><span class="sxs-lookup"><span data-stu-id="a0249-108">**Branching Pipelines Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/BranchingPipelines)</span></span>  
<span data-ttu-id="a0249-109">OWIN 请求处理管道不需要线性处理，它们可以通过不同的方式分支处理请求。</span><span class="sxs-lookup"><span data-stu-id="a0249-109">OWIN request processing pipelines do not need to be linear, they can be branched to process requests in different ways.</span></span> <span data-ttu-id="a0249-110">此示例演示如何基于请求路径或其他请求数据（如标头）构造分支管道。</span><span class="sxs-lookup"><span data-stu-id="a0249-110">This sample shows how to construct a branching pipeline based on request paths or other request data such as headers.</span></span> <span data-ttu-id="a0249-111">这些组件在 Microsoft.Owin.映射 nuget 包中可用。</span><span class="sxs-lookup"><span data-stu-id="a0249-111">These components are available in the Microsoft.Owin.Mapping nuget package.</span></span>

<span data-ttu-id="a0249-112">**自定义服务器示例** | [源代码](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/CustomServer) </span><span class="sxs-lookup"><span data-stu-id="a0249-112">**Custom Server Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/CustomServer) </span></span>  
<span data-ttu-id="a0249-113">演示如何在自托管 OWIN 时使用自定义 OWIN 服务器。</span><span class="sxs-lookup"><span data-stu-id="a0249-113">Shows how to use a custom OWIN server when self-hosting OWIN.</span></span>

<span data-ttu-id="a0249-114">**嵌入式示例** | [源代码](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/Embedded)</span><span class="sxs-lookup"><span data-stu-id="a0249-114">**Embedded Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/Embedded)</span></span>  
<span data-ttu-id="a0249-115">某些 OWIN 服务器可以在您自己的进程（&quot;自托管&quot;）内运行。</span><span class="sxs-lookup"><span data-stu-id="a0249-115">Some OWIN servers can be run inside of your own process (&quot;self-hosted&quot;).</span></span> <span data-ttu-id="a0249-116">此示例演示如何使用 Microsoft.Owin.Hosting nuget 包提供的工具启动 OWIN 应用程序。</span><span class="sxs-lookup"><span data-stu-id="a0249-116">This sample shows how to start an OWIN application using the tools provided by the Microsoft.Owin.Hosting nuget package.</span></span>

<span data-ttu-id="a0249-117">**HelloWorld 示例** | [源代码](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorld)</span><span class="sxs-lookup"><span data-stu-id="a0249-117">**HelloWorld Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorld)</span></span>  
<span data-ttu-id="a0249-118">OWIN 是一个 HTTP 服务器 API 抽象，可在各种服务器上实现应用程序可移植性。</span><span class="sxs-lookup"><span data-stu-id="a0249-118">OWIN is a HTTP server API abstraction that enables application portability across various servers.</span></span> <span data-ttu-id="a0249-119">此示例演示如何使用原始 OWIN 抽象周围的一些**简单包装器**编写 Hello World 应用程序，并在 web 服务器上运行它，如 ASP.NET。</span><span class="sxs-lookup"><span data-stu-id="a0249-119">This sample demonstrates how to write a Hello World application using some **simple wrappers** around the raw OWIN abstraction and run it on a web server like ASP.NET.</span></span>

<span data-ttu-id="a0249-120">**你好世界原始OWIN样品** | [源代码](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorldRawOwin)</span><span class="sxs-lookup"><span data-stu-id="a0249-120">**Hello World Raw OWIN Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorldRawOwin)</span></span>  
<span data-ttu-id="a0249-121">此示例演示如何使用**原始**OWIN 抽象编写 Hello World 应用程序，并在 web 服务器上运行它，如 Asp.Net。</span><span class="sxs-lookup"><span data-stu-id="a0249-121">This sample demonstrates how to write a Hello World application using the **raw** OWIN abstraction and run it on a web server like Asp.Net.</span></span>

<span data-ttu-id="a0249-122">**信号器样本** | [源代码](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/SignalR)</span><span class="sxs-lookup"><span data-stu-id="a0249-122">**SignalR Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/SignalR)</span></span>  
<span data-ttu-id="a0249-123">演示如何使用 OWIN / Katana 自承载 SignalR。</span><span class="sxs-lookup"><span data-stu-id="a0249-123">Shows how to self-host SignalR using OWIN / Katana.</span></span> <span data-ttu-id="a0249-124">有关自托管信号R 的详细信息，请参阅[教程：SignalR 自主机](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)。</span><span class="sxs-lookup"><span data-stu-id="a0249-124">For more info about self-hosting SignalR, see [Tutorial: SignalR Self-Host](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).</span></span>

<span data-ttu-id="a0249-125">**静态文件示例** | [源代码](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/StaticFilesSample) </span><span class="sxs-lookup"><span data-stu-id="a0249-125">**Static Files Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/StaticFilesSample) </span></span>  
<span data-ttu-id="a0249-126">演示如何使用 OWIN / Katana 支持静态文件的 HTTP 请求。</span><span class="sxs-lookup"><span data-stu-id="a0249-126">Shows how to support HTTP requests for static files using OWIN / Katana.</span></span>

<span data-ttu-id="a0249-127">**Web API** | [源代码](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebApi) </span><span class="sxs-lookup"><span data-stu-id="a0249-127">**Web API** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebApi) </span></span>  
<span data-ttu-id="a0249-128">此示例演示如何在 IIS 中托管 OWIN 并将 Web API 添加到 OWIN 管道。</span><span class="sxs-lookup"><span data-stu-id="a0249-128">This sample shows how to host OWIN in IIS and add Web API to the OWIN pipeline.</span></span>

<span data-ttu-id="a0249-129">**Web 套接字示例** | [源代码](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebSocketSample) </span><span class="sxs-lookup"><span data-stu-id="a0249-129">**Web Socket Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebSocketSample) </span></span>  
<span data-ttu-id="a0249-130">演示如何使用[System.Net.WebSockets.WebSocket](https://msdn.microsoft.com/library/system.net.websockets.websocket(v=vs.110).aspx)类支持 OWIN 中的 Web 套接字。</span><span class="sxs-lookup"><span data-stu-id="a0249-130">Shows how to support Web Sockets in OWIN by using the [System.Net.WebSockets.WebSocket](https://msdn.microsoft.com/library/system.net.websockets.websocket(v=vs.110).aspx) class.</span></span>

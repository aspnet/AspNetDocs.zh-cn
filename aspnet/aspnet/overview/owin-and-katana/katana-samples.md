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
# <a name="katana-samples"></a>Katana 示例

由[微软](https://github.com/microsoft)

## <a name="katana-samples"></a>Katana 示例

**ASP.NET路由示例** | [源代码](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/AspNetRoutes)  
在某些应用程序中，您需要将Asp.Net路由表中的 OWIN 组件与非 OWIN 组件并排连接。 此示例演示如何使用 Microsoft.Owin.Host.SystemWeb 提供的路由收集扩展方法 MapOwinPath 和 MapOwinRoute。

**分支管道示例** | [源代码](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/BranchingPipelines)  
OWIN 请求处理管道不需要线性处理，它们可以通过不同的方式分支处理请求。 此示例演示如何基于请求路径或其他请求数据（如标头）构造分支管道。 这些组件在 Microsoft.Owin.映射 nuget 包中可用。

**自定义服务器示例** | [源代码](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/CustomServer)   
演示如何在自托管 OWIN 时使用自定义 OWIN 服务器。

**嵌入式示例** | [源代码](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/Embedded)  
某些 OWIN 服务器可以在您自己的进程（&quot;自托管&quot;）内运行。 此示例演示如何使用 Microsoft.Owin.Hosting nuget 包提供的工具启动 OWIN 应用程序。

**HelloWorld 示例** | [源代码](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorld)  
OWIN 是一个 HTTP 服务器 API 抽象，可在各种服务器上实现应用程序可移植性。 此示例演示如何使用原始 OWIN 抽象周围的一些**简单包装器**编写 Hello World 应用程序，并在 web 服务器上运行它，如 ASP.NET。

**你好世界原始OWIN样品** | [源代码](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorldRawOwin)  
此示例演示如何使用**原始**OWIN 抽象编写 Hello World 应用程序，并在 web 服务器上运行它，如 Asp.Net。

**信号器样本** | [源代码](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/SignalR)  
演示如何使用 OWIN / Katana 自承载 SignalR。 有关自托管信号R 的详细信息，请参阅[教程：SignalR 自主机](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)。

**静态文件示例** | [源代码](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/StaticFilesSample)   
演示如何使用 OWIN / Katana 支持静态文件的 HTTP 请求。

**Web API** | [源代码](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebApi)   
此示例演示如何在 IIS 中托管 OWIN 并将 Web API 添加到 OWIN 管道。

**Web 套接字示例** | [源代码](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebSocketSample)   
演示如何使用[System.Net.WebSockets.WebSocket](https://msdn.microsoft.com/library/system.net.websockets.websocket(v=vs.110).aspx)类支持 OWIN 中的 Web 套接字。

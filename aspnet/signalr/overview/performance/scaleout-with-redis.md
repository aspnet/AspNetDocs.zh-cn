---
uid: signalr/overview/performance/scaleout-with-redis
title: 使用 Redis 的 SignalR 横向扩展 |Microsoft Docs
author: bradygaster
description: Visual Studio 2013.NET 4.5 SignalR 本主题中使用软件版本信息有关早期版本的版本 2 的本主题的早期版本...
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 6ecd08c1-e364-4cd7-ad4c-806521911585
msc.legacyurl: /signalr/overview/performance/scaleout-with-redis
msc.type: authoredcontent
ms.openlocfilehash: c20341a7fa0f5c5382ce7f2f6d459c4a6bec509f
ms.sourcegitcommit: 289e051cc8a90e8f7127e239fda73047bde4de12
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2019
ms.locfileid: "58424087"
---
<a name="signalr-scaleout-with-redis"></a>使用 Redis 的 SignalR 横向扩展
====================
通过[Mike Wasson](https://github.com/MikeWasson)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> ## <a name="software-versions-used-in-this-topic"></a>本主题中使用的软件版本
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - .NET 4.5
> - SignalR 版本 2.4
>
>
>
> ## <a name="previous-versions-of-this-topic"></a>本主题的早期版本
>
> 有关 SignalR 的早期版本的信息，请参阅[SignalR 较早版本](../older-versions/index.md)。
>
> ## <a name="questions-and-comments"></a>问题和提出的意见
>
> 请在你喜欢本教程的内容以及我们可以改进的页的底部的评论中留下反馈。 如果你有与本教程不直接相关的问题，你可以发布到[ASP.NET SignalR 论坛](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com/)。


在本教程中，您将使用[Redis](http://redis.io/)若要部署在两个单独的 IIS 实例的 SignalR 应用程序间分发消息。

Redis 是内存中键 / 值存储。 它还支持发布/订阅模型的消息传送系统。 Redis 的 SignalR 基架使用发布/订阅功能以将消息转发到其他服务器。

![](scaleout-with-redis/_static/image1.png)

对于本教程中，将使用三个服务器：

- 两台运行 Windows，将使用的 SignalR 应用程序部署的服务器。
- 一台运行 Linux，你将用于运行 Redis 服务器。 在本教程中的屏幕截图，我使用 Ubuntu 12.04 TLS。

如果没有要使用的三个物理服务器，您可以在 HYPER-V 上创建 Vm。 另一个选项是在 Azure 上创建 Vm。

虽然本教程使用官方 Redis 实现，此外，还有[Windows 端口的 Redis](https://github.com/MSOpenTech/redis)从 MSOpenTech。 安装和配置不相同，但否则步骤是相同的。

> [!NOTE]
>
> 使用 Redis 的 SignalR 横向扩展不支持 Redis 群集。


## <a name="overview"></a>概述

我们进入详细教程之前，下面是将执行哪些操作的快速概述。

1. 安装 Redis 并启动 Redis 服务器。
2. 将以下 NuGet 包添加到你的应用程序：

    - [Microsoft.AspNet.SignalR](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [Microsoft.AspNet.SignalR.StackExchangeRedis](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.StackExchangeRedis)
    
3. 创建 SignalR 应用程序。
4. 将以下代码添加到 Startup.cs 配置基架：

    [!code-csharp[Main](scaleout-with-redis/samples/sample1.cs)]

## <a name="ubuntu-on-hyper-v"></a>Ubuntu 上的 HYPER-V

使用 Windows 的 HYPER-V，您可以轻松创建 Ubuntu VM 在 Windows Server 上。

下载从 Ubuntu ISO [ http://www.ubuntu.com ](http://www.ubuntu.com/)。

在 HYPER-V 中添加新的 VM。 在中**连接虚拟硬盘**步骤中，选择**创建虚拟硬盘**。

![](scaleout-with-redis/_static/image2.png)

在中**安装选项**步骤中，选择**映像文件 (.iso)**，单击**浏览**，并浏览到 Ubuntu 安装 ISO。

![](scaleout-with-redis/_static/image3.png)

## <a name="install-redis"></a>安装 Redis

遵循的步骤[ http://redis.io/download ](http://redis.io/download)以下载和生成 Redis。

[!code-console[Main](scaleout-with-redis/samples/sample2.cmd)]

这会生成 Redis 二进制文件`src`目录。

默认情况下，Redis 不需要密码。 若要设置密码，请编辑`redis.conf`文件的源代码的根目录中。 （请文件的备份副本之前对其进行编辑 ！）添加以下指令为`redis.conf`:

[!code-powershell[Main](scaleout-with-redis/samples/sample3.ps1)]

现在，启动 Redis 服务器：

[!code-css[Main](scaleout-with-redis/samples/sample4.css)]

![](scaleout-with-redis/_static/image4.png)

打开端口 6379，这是 Redis 的默认端口上侦听。 （可以更改配置文件中的端口号。）

## <a name="create-the-signalr-application"></a>创建 SignalR 应用程序

创建 SignalR 应用程序按照以下教程之一：

- [SignalR 2.0 入门](../getting-started/tutorial-getting-started-with-signalr.md)
- [SignalR 2.0 和 MVC 5 入门](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)

接下来，我们将修改聊天应用程序，以支持采用 Redis 的扩展。 首先，添加`Microsoft.AspNet.SignalR.StackExchangeRedis`到你的项目的 NuGet 包。 在 Visual Studio 中，从**工具**菜单中，选择**NuGet 包管理器**，然后选择**程序包管理器控制台**。 在包管理器控制台窗口中，输入以下命令：

[!code-powershell[Main](scaleout-with-redis/samples/sample5.ps1)]

接下来，打开 Startup.cs 文件。 将以下代码添加到**配置**方法：

[!code-csharp[Main](scaleout-with-redis/samples/sample6.cs)]

- "服务器"是运行 Redis 服务器的名称。
- *端口*是端口号
- "密码"是 redis.conf 文件中定义的密码。
- "AppName"是任何字符串。 SignalR 具有此名称创建的 Redis 发布/订阅通道。

例如：

[!code-csharp[Main](scaleout-with-redis/samples/sample7.cs)]

## <a name="deploy-and-run-the-application"></a>部署和运行应用程序

准备 Windows Server 实例将 SignalR 应用程序部署。

添加 IIS 角色。 包含"应用程序开发"功能，包括 WebSocket 协议。

![](scaleout-with-redis/_static/image5.png)

此外包括管理服务 （在"管理工具"列出）。

![](scaleout-with-redis/_static/image6.png)

**安装 Web 部署 3.0。** 当你运行 IIS 管理器，它将提示你安装 Microsoft Web 平台，或者可以[下载安装程序](https://go.microsoft.com/fwlink/?LinkId=255386)。 在平台安装程序中，搜索 Web 部署并安装 Web Deploy 3.0

![](scaleout-with-redis/_static/image7.png)

检查 Web 管理服务正在运行。 如果没有，请启动服务。 （如果在 Windows 服务列表中，看不到 Web 管理服务，请确保添加 IIS 角色时安装管理服务。）

默认情况下，Web 管理服务侦听 TCP 端口 8172。 在 Windows 防火墙中创建一个新的入站的规则以允许端口 8172 上的 TCP 流量。 有关详细信息，请参阅[配置防火墙规则](https://technet.microsoft.com/library/dd448559(WS.10).aspx)。 （如果托管在 Azure 上的 Vm，你可以直接在 Azure 门户中。 请参阅[如何设置虚拟机的终结点](https://azure.microsoft.com/documentation/articles/virtual-machines-set-up-endpoints/)。)

现在已准备好部署到服务器从开发计算机的 Visual Studio 项目。 在解决方案资源管理器，右键单击解决方案，然后单击**发布**。

有关更详细的有关 web 部署的文档，请参阅[用于 Visual Studio 和 ASP.NET 的 Web 部署内容映射](../../../whitepapers/aspnet-web-deployment-content-map.md)。

如果部署到两个服务器应用程序，可以在一个单独的浏览器窗口中打开每个实例，并查看它们每个接收来自其他 SignalR 消息。 （当然，在生产环境中，两个服务器将位于负载均衡器后面。）

![](scaleout-with-redis/_static/image8.png)

如果您感兴趣，查看将发送到 Redis，可以使用的消息**redis cli**安装使用 Redis 的客户端。

[!code-xml[Main](scaleout-with-redis/samples/sample8.xml)]

![](scaleout-with-redis/_static/image9.png)

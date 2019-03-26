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
<a name="signalr-scaleout-with-redis"></a><span data-ttu-id="30a54-103">使用 Redis 的 SignalR 横向扩展</span><span class="sxs-lookup"><span data-stu-id="30a54-103">SignalR Scaleout with Redis</span></span>
====================
<span data-ttu-id="30a54-104">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="30a54-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="30a54-105">本主题中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="30a54-105">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="30a54-106">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="30a54-106">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="30a54-107">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="30a54-107">.NET 4.5</span></span>
> - <span data-ttu-id="30a54-108">SignalR 版本 2.4</span><span class="sxs-lookup"><span data-stu-id="30a54-108">SignalR version 2.4</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="30a54-109">本主题的早期版本</span><span class="sxs-lookup"><span data-stu-id="30a54-109">Previous versions of this topic</span></span>
>
> <span data-ttu-id="30a54-110">有关 SignalR 的早期版本的信息，请参阅[SignalR 较早版本](../older-versions/index.md)。</span><span class="sxs-lookup"><span data-stu-id="30a54-110">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="30a54-111">问题和提出的意见</span><span class="sxs-lookup"><span data-stu-id="30a54-111">Questions and comments</span></span>
>
> <span data-ttu-id="30a54-112">请在你喜欢本教程的内容以及我们可以改进的页的底部的评论中留下反馈。</span><span class="sxs-lookup"><span data-stu-id="30a54-112">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="30a54-113">如果你有与本教程不直接相关的问题，你可以发布到[ASP.NET SignalR 论坛](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com/)。</span><span class="sxs-lookup"><span data-stu-id="30a54-113">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>


<span data-ttu-id="30a54-114">在本教程中，您将使用[Redis](http://redis.io/)若要部署在两个单独的 IIS 实例的 SignalR 应用程序间分发消息。</span><span class="sxs-lookup"><span data-stu-id="30a54-114">In this tutorial, you will use [Redis](http://redis.io/) to distribute messages across a SignalR application that is deployed on two separate IIS instances.</span></span>

<span data-ttu-id="30a54-115">Redis 是内存中键 / 值存储。</span><span class="sxs-lookup"><span data-stu-id="30a54-115">Redis is an in-memory key-value store.</span></span> <span data-ttu-id="30a54-116">它还支持发布/订阅模型的消息传送系统。</span><span class="sxs-lookup"><span data-stu-id="30a54-116">It also supports a messaging system with a publish/subscribe model.</span></span> <span data-ttu-id="30a54-117">Redis 的 SignalR 基架使用发布/订阅功能以将消息转发到其他服务器。</span><span class="sxs-lookup"><span data-stu-id="30a54-117">The SignalR Redis backplane uses the pub/sub feature to forward messages to other servers.</span></span>

![](scaleout-with-redis/_static/image1.png)

<span data-ttu-id="30a54-118">对于本教程中，将使用三个服务器：</span><span class="sxs-lookup"><span data-stu-id="30a54-118">For this tutorial, you will use three servers:</span></span>

- <span data-ttu-id="30a54-119">两台运行 Windows，将使用的 SignalR 应用程序部署的服务器。</span><span class="sxs-lookup"><span data-stu-id="30a54-119">Two servers running Windows, which you will use to deploy a SignalR application.</span></span>
- <span data-ttu-id="30a54-120">一台运行 Linux，你将用于运行 Redis 服务器。</span><span class="sxs-lookup"><span data-stu-id="30a54-120">One server running Linux, which you will use to run Redis.</span></span> <span data-ttu-id="30a54-121">在本教程中的屏幕截图，我使用 Ubuntu 12.04 TLS。</span><span class="sxs-lookup"><span data-stu-id="30a54-121">For the screenshots in this tutorial, I used Ubuntu 12.04 TLS.</span></span>

<span data-ttu-id="30a54-122">如果没有要使用的三个物理服务器，您可以在 HYPER-V 上创建 Vm。</span><span class="sxs-lookup"><span data-stu-id="30a54-122">If you don't have three physical servers to use, you can create VMs on Hyper-V.</span></span> <span data-ttu-id="30a54-123">另一个选项是在 Azure 上创建 Vm。</span><span class="sxs-lookup"><span data-stu-id="30a54-123">Another option is to create VMs on Azure.</span></span>

<span data-ttu-id="30a54-124">虽然本教程使用官方 Redis 实现，此外，还有[Windows 端口的 Redis](https://github.com/MSOpenTech/redis)从 MSOpenTech。</span><span class="sxs-lookup"><span data-stu-id="30a54-124">Although this tutorial uses the official Redis implementation, there is also a [Windows port of Redis](https://github.com/MSOpenTech/redis) from MSOpenTech.</span></span> <span data-ttu-id="30a54-125">安装和配置不相同，但否则步骤是相同的。</span><span class="sxs-lookup"><span data-stu-id="30a54-125">Setup and configuration are different, but otherwise the steps are the same.</span></span>

> [!NOTE]
>
> <span data-ttu-id="30a54-126">使用 Redis 的 SignalR 横向扩展不支持 Redis 群集。</span><span class="sxs-lookup"><span data-stu-id="30a54-126">SignalR scaleout with Redis does not support Redis clusters.</span></span>


## <a name="overview"></a><span data-ttu-id="30a54-127">概述</span><span class="sxs-lookup"><span data-stu-id="30a54-127">Overview</span></span>

<span data-ttu-id="30a54-128">我们进入详细教程之前，下面是将执行哪些操作的快速概述。</span><span class="sxs-lookup"><span data-stu-id="30a54-128">Before we get to the detailed tutorial, here is a quick overview of what you will do.</span></span>

1. <span data-ttu-id="30a54-129">安装 Redis 并启动 Redis 服务器。</span><span class="sxs-lookup"><span data-stu-id="30a54-129">Install Redis and start the Redis server.</span></span>
2. <span data-ttu-id="30a54-130">将以下 NuGet 包添加到你的应用程序：</span><span class="sxs-lookup"><span data-stu-id="30a54-130">Add these NuGet packages to your application:</span></span>

    - [<span data-ttu-id="30a54-131">Microsoft.AspNet.SignalR</span><span class="sxs-lookup"><span data-stu-id="30a54-131">Microsoft.AspNet.SignalR</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [<span data-ttu-id="30a54-132">Microsoft.AspNet.SignalR.StackExchangeRedis</span><span class="sxs-lookup"><span data-stu-id="30a54-132">Microsoft.AspNet.SignalR.StackExchangeRedis</span></span>](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.StackExchangeRedis)
    
3. <span data-ttu-id="30a54-133">创建 SignalR 应用程序。</span><span class="sxs-lookup"><span data-stu-id="30a54-133">Create a SignalR application.</span></span>
4. <span data-ttu-id="30a54-134">将以下代码添加到 Startup.cs 配置基架：</span><span class="sxs-lookup"><span data-stu-id="30a54-134">Add the following code to Startup.cs to configure the backplane:</span></span>

    [!code-csharp[Main](scaleout-with-redis/samples/sample1.cs)]

## <a name="ubuntu-on-hyper-v"></a><span data-ttu-id="30a54-135">Ubuntu 上的 HYPER-V</span><span class="sxs-lookup"><span data-stu-id="30a54-135">Ubuntu on Hyper-V</span></span>

<span data-ttu-id="30a54-136">使用 Windows 的 HYPER-V，您可以轻松创建 Ubuntu VM 在 Windows Server 上。</span><span class="sxs-lookup"><span data-stu-id="30a54-136">Using Windows Hyper-V, you can easily create an Ubuntu VM on Windows Server.</span></span>

<span data-ttu-id="30a54-137">下载从 Ubuntu ISO [ http://www.ubuntu.com ](http://www.ubuntu.com/)。</span><span class="sxs-lookup"><span data-stu-id="30a54-137">Download the Ubuntu ISO from [http://www.ubuntu.com](http://www.ubuntu.com/).</span></span>

<span data-ttu-id="30a54-138">在 HYPER-V 中添加新的 VM。</span><span class="sxs-lookup"><span data-stu-id="30a54-138">In Hyper-V, add a new VM.</span></span> <span data-ttu-id="30a54-139">在中**连接虚拟硬盘**步骤中，选择**创建虚拟硬盘**。</span><span class="sxs-lookup"><span data-stu-id="30a54-139">In the **Connect Virtual Hard Disk** step, select **Create a virtual hard disk**.</span></span>

![](scaleout-with-redis/_static/image2.png)

<span data-ttu-id="30a54-140">在中**安装选项**步骤中，选择**映像文件 (.iso)**，单击**浏览**，并浏览到 Ubuntu 安装 ISO。</span><span class="sxs-lookup"><span data-stu-id="30a54-140">In the **Installation Options** step, select **Image file (.iso)**, click **Browse**, and browse to the Ubuntu installation ISO.</span></span>

![](scaleout-with-redis/_static/image3.png)

## <a name="install-redis"></a><span data-ttu-id="30a54-141">安装 Redis</span><span class="sxs-lookup"><span data-stu-id="30a54-141">Install Redis</span></span>

<span data-ttu-id="30a54-142">遵循的步骤[ http://redis.io/download ](http://redis.io/download)以下载和生成 Redis。</span><span class="sxs-lookup"><span data-stu-id="30a54-142">Follow the steps at [http://redis.io/download](http://redis.io/download) to download and build Redis.</span></span>

[!code-console[Main](scaleout-with-redis/samples/sample2.cmd)]

<span data-ttu-id="30a54-143">这会生成 Redis 二进制文件`src`目录。</span><span class="sxs-lookup"><span data-stu-id="30a54-143">This builds the Redis binaries in the `src` directory.</span></span>

<span data-ttu-id="30a54-144">默认情况下，Redis 不需要密码。</span><span class="sxs-lookup"><span data-stu-id="30a54-144">By default, Redis does not require a password.</span></span> <span data-ttu-id="30a54-145">若要设置密码，请编辑`redis.conf`文件的源代码的根目录中。</span><span class="sxs-lookup"><span data-stu-id="30a54-145">To set a password, edit the `redis.conf` file, which is located in the root directory of the source code.</span></span> <span data-ttu-id="30a54-146">（请文件的备份副本之前对其进行编辑 ！）添加以下指令为`redis.conf`:</span><span class="sxs-lookup"><span data-stu-id="30a54-146">(Make a backup copy of the file before you edit it!) Add the following directive to `redis.conf`:</span></span>

[!code-powershell[Main](scaleout-with-redis/samples/sample3.ps1)]

<span data-ttu-id="30a54-147">现在，启动 Redis 服务器：</span><span class="sxs-lookup"><span data-stu-id="30a54-147">Now start the Redis server:</span></span>

[!code-css[Main](scaleout-with-redis/samples/sample4.css)]

![](scaleout-with-redis/_static/image4.png)

<span data-ttu-id="30a54-148">打开端口 6379，这是 Redis 的默认端口上侦听。</span><span class="sxs-lookup"><span data-stu-id="30a54-148">Open port 6379, which is the default port that Redis listens on.</span></span> <span data-ttu-id="30a54-149">（可以更改配置文件中的端口号。）</span><span class="sxs-lookup"><span data-stu-id="30a54-149">(You can change the port number in the configuration file.)</span></span>

## <a name="create-the-signalr-application"></a><span data-ttu-id="30a54-150">创建 SignalR 应用程序</span><span class="sxs-lookup"><span data-stu-id="30a54-150">Create the SignalR Application</span></span>

<span data-ttu-id="30a54-151">创建 SignalR 应用程序按照以下教程之一：</span><span class="sxs-lookup"><span data-stu-id="30a54-151">Create a SignalR application by following either of these tutorials:</span></span>

- [<span data-ttu-id="30a54-152">SignalR 2.0 入门</span><span class="sxs-lookup"><span data-stu-id="30a54-152">Getting Started with SignalR 2.0</span></span>](../getting-started/tutorial-getting-started-with-signalr.md)
- [<span data-ttu-id="30a54-153">SignalR 2.0 和 MVC 5 入门</span><span class="sxs-lookup"><span data-stu-id="30a54-153">Getting Started with SignalR 2.0 and MVC 5</span></span>](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)

<span data-ttu-id="30a54-154">接下来，我们将修改聊天应用程序，以支持采用 Redis 的扩展。</span><span class="sxs-lookup"><span data-stu-id="30a54-154">Next, we'll modify the chat application to support scaleout with Redis.</span></span> <span data-ttu-id="30a54-155">首先，添加`Microsoft.AspNet.SignalR.StackExchangeRedis`到你的项目的 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="30a54-155">First, add the `Microsoft.AspNet.SignalR.StackExchangeRedis` NuGet package to your project.</span></span> <span data-ttu-id="30a54-156">在 Visual Studio 中，从**工具**菜单中，选择**NuGet 包管理器**，然后选择**程序包管理器控制台**。</span><span class="sxs-lookup"><span data-stu-id="30a54-156">In Visual Studio, from the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="30a54-157">在包管理器控制台窗口中，输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="30a54-157">In the Package Manager Console window, enter the following command:</span></span>

[!code-powershell[Main](scaleout-with-redis/samples/sample5.ps1)]

<span data-ttu-id="30a54-158">接下来，打开 Startup.cs 文件。</span><span class="sxs-lookup"><span data-stu-id="30a54-158">Next, open the Startup.cs file.</span></span> <span data-ttu-id="30a54-159">将以下代码添加到**配置**方法：</span><span class="sxs-lookup"><span data-stu-id="30a54-159">Add the following code to the **Configuration** method:</span></span>

[!code-csharp[Main](scaleout-with-redis/samples/sample6.cs)]

- <span data-ttu-id="30a54-160">"服务器"是运行 Redis 服务器的名称。</span><span class="sxs-lookup"><span data-stu-id="30a54-160">"server" is the name of the server that is running Redis.</span></span>
- <span data-ttu-id="30a54-161">*端口*是端口号</span><span class="sxs-lookup"><span data-stu-id="30a54-161">*port* is the port number</span></span>
- <span data-ttu-id="30a54-162">"密码"是 redis.conf 文件中定义的密码。</span><span class="sxs-lookup"><span data-stu-id="30a54-162">"password" is the password that you defined in the redis.conf file.</span></span>
- <span data-ttu-id="30a54-163">"AppName"是任何字符串。</span><span class="sxs-lookup"><span data-stu-id="30a54-163">"AppName" is any string.</span></span> <span data-ttu-id="30a54-164">SignalR 具有此名称创建的 Redis 发布/订阅通道。</span><span class="sxs-lookup"><span data-stu-id="30a54-164">SignalR creates a Redis pub/sub channel with this name.</span></span>

<span data-ttu-id="30a54-165">例如：</span><span class="sxs-lookup"><span data-stu-id="30a54-165">For example:</span></span>

[!code-csharp[Main](scaleout-with-redis/samples/sample7.cs)]

## <a name="deploy-and-run-the-application"></a><span data-ttu-id="30a54-166">部署和运行应用程序</span><span class="sxs-lookup"><span data-stu-id="30a54-166">Deploy and Run the Application</span></span>

<span data-ttu-id="30a54-167">准备 Windows Server 实例将 SignalR 应用程序部署。</span><span class="sxs-lookup"><span data-stu-id="30a54-167">Prepare your Windows Server instances to deploy the SignalR application.</span></span>

<span data-ttu-id="30a54-168">添加 IIS 角色。</span><span class="sxs-lookup"><span data-stu-id="30a54-168">Add the IIS role.</span></span> <span data-ttu-id="30a54-169">包含"应用程序开发"功能，包括 WebSocket 协议。</span><span class="sxs-lookup"><span data-stu-id="30a54-169">Include "Application Development" features, including the WebSocket Protocol.</span></span>

![](scaleout-with-redis/_static/image5.png)

<span data-ttu-id="30a54-170">此外包括管理服务 （在"管理工具"列出）。</span><span class="sxs-lookup"><span data-stu-id="30a54-170">Also include the Management Service (listed under "Management Tools").</span></span>

![](scaleout-with-redis/_static/image6.png)

<span data-ttu-id="30a54-171">**安装 Web 部署 3.0。**</span><span class="sxs-lookup"><span data-stu-id="30a54-171">**Install Web Deploy 3.0.**</span></span> <span data-ttu-id="30a54-172">当你运行 IIS 管理器，它将提示你安装 Microsoft Web 平台，或者可以[下载安装程序](https://go.microsoft.com/fwlink/?LinkId=255386)。</span><span class="sxs-lookup"><span data-stu-id="30a54-172">When you run IIS Manager, it will prompt you to install Microsoft Web Platform, or you can [download the installer](https://go.microsoft.com/fwlink/?LinkId=255386).</span></span> <span data-ttu-id="30a54-173">在平台安装程序中，搜索 Web 部署并安装 Web Deploy 3.0</span><span class="sxs-lookup"><span data-stu-id="30a54-173">In the Platform Installer, search for Web Deploy and install Web Deploy 3.0</span></span>

![](scaleout-with-redis/_static/image7.png)

<span data-ttu-id="30a54-174">检查 Web 管理服务正在运行。</span><span class="sxs-lookup"><span data-stu-id="30a54-174">Check that the Web Management Service is running.</span></span> <span data-ttu-id="30a54-175">如果没有，请启动服务。</span><span class="sxs-lookup"><span data-stu-id="30a54-175">If not, start the service.</span></span> <span data-ttu-id="30a54-176">（如果在 Windows 服务列表中，看不到 Web 管理服务，请确保添加 IIS 角色时安装管理服务。）</span><span class="sxs-lookup"><span data-stu-id="30a54-176">(If you don't see Web Management Service in the list of Windows services, make sure that you installed the Management Service when you added the IIS role.)</span></span>

<span data-ttu-id="30a54-177">默认情况下，Web 管理服务侦听 TCP 端口 8172。</span><span class="sxs-lookup"><span data-stu-id="30a54-177">By default, the Web Management Service listens on TCP port 8172.</span></span> <span data-ttu-id="30a54-178">在 Windows 防火墙中创建一个新的入站的规则以允许端口 8172 上的 TCP 流量。</span><span class="sxs-lookup"><span data-stu-id="30a54-178">In Windows Firewall, create a new inbound rule to allow TCP traffic on port 8172.</span></span> <span data-ttu-id="30a54-179">有关详细信息，请参阅[配置防火墙规则](https://technet.microsoft.com/library/dd448559(WS.10).aspx)。</span><span class="sxs-lookup"><span data-stu-id="30a54-179">For more information, see [Configuring Firewall Rules](https://technet.microsoft.com/library/dd448559(WS.10).aspx).</span></span> <span data-ttu-id="30a54-180">（如果托管在 Azure 上的 Vm，你可以直接在 Azure 门户中。</span><span class="sxs-lookup"><span data-stu-id="30a54-180">(If you are hosting the VMs on Azure, you can do this directly in the Azure portal.</span></span> <span data-ttu-id="30a54-181">请参阅[如何设置虚拟机的终结点](https://azure.microsoft.com/documentation/articles/virtual-machines-set-up-endpoints/)。)</span><span class="sxs-lookup"><span data-stu-id="30a54-181">See [How to Set Up Endpoints to a Virtual Machine](https://azure.microsoft.com/documentation/articles/virtual-machines-set-up-endpoints/).)</span></span>

<span data-ttu-id="30a54-182">现在已准备好部署到服务器从开发计算机的 Visual Studio 项目。</span><span class="sxs-lookup"><span data-stu-id="30a54-182">Now you are ready to deploy the Visual Studio project from your development machine to the server.</span></span> <span data-ttu-id="30a54-183">在解决方案资源管理器，右键单击解决方案，然后单击**发布**。</span><span class="sxs-lookup"><span data-stu-id="30a54-183">In Solution Explorer, right-click the solution and click **Publish**.</span></span>

<span data-ttu-id="30a54-184">有关更详细的有关 web 部署的文档，请参阅[用于 Visual Studio 和 ASP.NET 的 Web 部署内容映射](../../../whitepapers/aspnet-web-deployment-content-map.md)。</span><span class="sxs-lookup"><span data-stu-id="30a54-184">For more detailed documentation about web deployment, see [Web Deployment Content Map for Visual Studio and ASP.NET](../../../whitepapers/aspnet-web-deployment-content-map.md).</span></span>

<span data-ttu-id="30a54-185">如果部署到两个服务器应用程序，可以在一个单独的浏览器窗口中打开每个实例，并查看它们每个接收来自其他 SignalR 消息。</span><span class="sxs-lookup"><span data-stu-id="30a54-185">If you deploy the application to two servers, you can open each instance in a separate browser window and see that they each receive SignalR messages from the other.</span></span> <span data-ttu-id="30a54-186">（当然，在生产环境中，两个服务器将位于负载均衡器后面。）</span><span class="sxs-lookup"><span data-stu-id="30a54-186">(Of course, in a production environment, the two servers would sit behind a load balancer.)</span></span>

![](scaleout-with-redis/_static/image8.png)

<span data-ttu-id="30a54-187">如果您感兴趣，查看将发送到 Redis，可以使用的消息**redis cli**安装使用 Redis 的客户端。</span><span class="sxs-lookup"><span data-stu-id="30a54-187">If you're curious to see the messages that are sent to Redis, you can use the **redis-cli** client, which installs with Redis.</span></span>

[!code-xml[Main](scaleout-with-redis/samples/sample8.xml)]

![](scaleout-with-redis/_static/image9.png)

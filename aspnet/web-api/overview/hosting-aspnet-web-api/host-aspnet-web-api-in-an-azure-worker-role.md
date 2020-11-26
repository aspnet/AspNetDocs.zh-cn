---
uid: web-api/overview/hosting-aspnet-web-api/host-aspnet-web-api-in-an-azure-worker-role
title: Azure 辅助角色中的主机 ASP.NET Web API 2-ASP.NET 4。x
author: MikeWasson
description: 教程：在 Azure 辅助角色中托管 ASP.NET Web API，使用 OWIN 自承载 Web API 框架。
ms.author: riande
ms.date: 04/02/2014
ms.custom: seoapril2019
ms.assetid: 6980ee2e-d6b0-4a08-8fb6-ab96362dd0e3
msc.legacyurl: /web-api/overview/hosting-aspnet-web-api/host-aspnet-web-api-in-an-azure-worker-role
msc.type: authoredcontent
ms.openlocfilehash: 06bd33a7d30ab38d851d929d72ae8c539e16873c
ms.sourcegitcommit: 4b78855427f1397df0a7be3559e04ec94a78c308
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/25/2020
ms.locfileid: "96151901"
---
# <a name="host-aspnet-web-api-2-in-an-azure-worker-role"></a><span data-ttu-id="766de-103">Azure 辅助角色中的主机 ASP.NET Web API 2</span><span class="sxs-lookup"><span data-stu-id="766de-103">Host ASP.NET Web API 2 in an Azure Worker Role</span></span>

<span data-ttu-id="766de-104">作者： [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="766de-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="766de-105">本教程介绍了如何使用 OWIN 在 Azure 辅助角色中托管 ASP.NET Web API 来自承载 Web API 框架。</span><span class="sxs-lookup"><span data-stu-id="766de-105">This tutorial shows how to host ASP.NET Web API in an Azure Worker Role, using OWIN to self-host the Web API framework.</span></span>
>
> <span data-ttu-id="766de-106">[开放式 Web Interface for .net](http://owin.org/) (OWIN) 定义 .net Web 服务器和 Web 应用程序之间的抽象。</span><span class="sxs-lookup"><span data-stu-id="766de-106">[Open Web Interface for .NET](http://owin.org/) (OWIN) defines an abstraction between .NET web servers and web applications.</span></span> <span data-ttu-id="766de-107">OWIN 将 web 应用程序与服务器分离，这使得 OWIN 非常适合用于在你自己的进程（例如，在 Azure 辅助角色中）自承载 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="766de-107">OWIN decouples the web application from the server, which makes OWIN ideal for self-hosting a web application in your own process, outside of IIS–for example, inside an Azure worker role.</span></span>
>
> <span data-ttu-id="766de-108">在本教程中，你将使用 Owin 包，它提供了一个用于自承载 OWIN 应用程序的 HTTP 服务器。</span><span class="sxs-lookup"><span data-stu-id="766de-108">In this tutorial, you'll use the Microsoft.Owin.Host.HttpListener package, which provides an HTTP server that be used to self-host OWIN applications.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="766de-109">本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="766de-109">Software versions used in the tutorial</span></span>
>
>
> - [<span data-ttu-id="766de-110">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="766de-110">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="766de-111">Web API 2</span><span class="sxs-lookup"><span data-stu-id="766de-111">Web API 2</span></span>
> - [<span data-ttu-id="766de-112">用于 .NET 2.3 的 Azure SDK</span><span class="sxs-lookup"><span data-stu-id="766de-112">Azure SDK for .NET 2.3</span></span>](https://azure.microsoft.com/downloads/)

## <a name="create-a-microsoft-azure-project"></a><span data-ttu-id="766de-113">创建 Microsoft Azure 项目</span><span class="sxs-lookup"><span data-stu-id="766de-113">Create a Microsoft Azure Project</span></span>

<span data-ttu-id="766de-114">以管理员权限启动 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="766de-114">Start Visual Studio with administrator privileges.</span></span> <span data-ttu-id="766de-115">需要管理员权限才能使用 Azure 计算仿真程序在本地调试应用程序。</span><span class="sxs-lookup"><span data-stu-id="766de-115">Administrator privileges are needed to debug the application locally, using the Azure Compute Emulator.</span></span>

<span data-ttu-id="766de-116">在 " **文件** " 菜单上，单击 " **新建**"，然后单击 " **项目**"。</span><span class="sxs-lookup"><span data-stu-id="766de-116">On the **File** menu, click **New**, then click **Project**.</span></span> <span data-ttu-id="766de-117">从 "**已安装的模板**" 的 "Visual c #" 下，单击 "**云**"，然后单击 " **microsoft Azure 云服务**</span><span class="sxs-lookup"><span data-stu-id="766de-117">From **Installed Templates**, under Visual C#, click **Cloud** and then click **Windows Azure Cloud Service**.</span></span> <span data-ttu-id="766de-118">将项目命名为 "AzureApp"，然后单击 **"确定**"。</span><span class="sxs-lookup"><span data-stu-id="766de-118">Name the project "AzureApp" and click **OK**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image2.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image1.png)

<span data-ttu-id="766de-119">在 " **新建 Microsoft Azure 云服务** " 对话框中，双击 " **辅助角色**"。</span><span class="sxs-lookup"><span data-stu-id="766de-119">In the **New Windows Azure Cloud Service** dialog, double-click **Worker Role**.</span></span> <span data-ttu-id="766de-120">保留默认名称 ( "WorkerRole1" ) 。</span><span class="sxs-lookup"><span data-stu-id="766de-120">Leave the default name ("WorkerRole1").</span></span> <span data-ttu-id="766de-121">此步骤将辅助角色添加到解决方案。</span><span class="sxs-lookup"><span data-stu-id="766de-121">This step adds a worker role to the solution.</span></span> <span data-ttu-id="766de-122">单击" **确定**"。</span><span class="sxs-lookup"><span data-stu-id="766de-122">Click **OK**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image4.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image3.png)

<span data-ttu-id="766de-123">创建的 Visual Studio 解决方案包含两个项目：</span><span class="sxs-lookup"><span data-stu-id="766de-123">The Visual Studio solution that is created contains two projects:</span></span>

- <span data-ttu-id="766de-124">&quot;AzureApp &quot; 定义 Azure 应用程序的角色和配置。</span><span class="sxs-lookup"><span data-stu-id="766de-124">&quot;AzureApp&quot; defines the roles and configuration for the Azure application.</span></span>
- <span data-ttu-id="766de-125">&quot;WorkerRole1 &quot; 包含辅助角色的代码。</span><span class="sxs-lookup"><span data-stu-id="766de-125">&quot;WorkerRole1&quot; contains the code for the worker role.</span></span>

<span data-ttu-id="766de-126">通常，Azure 应用程序可以包含多个角色，但本教程使用单个角色。</span><span class="sxs-lookup"><span data-stu-id="766de-126">In general, an Azure application can contain multiple roles, although this tutorial uses a single role.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image5.png)

## <a name="add-the-web-api-and-owin-packages"></a><span data-ttu-id="766de-127">添加 Web API 和 OWIN 包</span><span class="sxs-lookup"><span data-stu-id="766de-127">Add the Web API and OWIN Packages</span></span>

<span data-ttu-id="766de-128">从 " **工具** " 菜单中，单击 " **NuGet 包管理器**"，然后单击 " **程序包管理器控制台**"。</span><span class="sxs-lookup"><span data-stu-id="766de-128">From the **Tools** menu, click **NuGet Package Manager**, then click **Package Manager Console**.</span></span>

<span data-ttu-id="766de-129">在“Package Manager Console”窗口中，输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="766de-129">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample1.cmd)]

## <a name="add-an-http-endpoint"></a><span data-ttu-id="766de-130">添加 HTTP 终结点</span><span class="sxs-lookup"><span data-stu-id="766de-130">Add an HTTP Endpoint</span></span>

<span data-ttu-id="766de-131">在解决方案资源管理器中，展开 AzureApp 项目。</span><span class="sxs-lookup"><span data-stu-id="766de-131">In Solution Explorer, expand the AzureApp project.</span></span> <span data-ttu-id="766de-132">展开 "角色" 节点，右键单击 WorkerRole1，然后选择 " **属性**"。</span><span class="sxs-lookup"><span data-stu-id="766de-132">Expand the Roles node, right-click WorkerRole1, and select **Properties**.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image6.png)

<span data-ttu-id="766de-133">单击“终结点”，然后单击“添加终结点”。</span><span class="sxs-lookup"><span data-stu-id="766de-133">Click **Endpoints**, and then click **Add Endpoint**.</span></span>

<span data-ttu-id="766de-134">在 " **协议** " 下拉列表中，选择 "http"。</span><span class="sxs-lookup"><span data-stu-id="766de-134">In the **Protocol** dropdown list, select "http".</span></span> <span data-ttu-id="766de-135">在 " **公用端口** " 和 " **专用端口**" 中，键入80。</span><span class="sxs-lookup"><span data-stu-id="766de-135">In **Public Port** and **Private Port**, type 80.</span></span> <span data-ttu-id="766de-136">这些端口号可以不同。</span><span class="sxs-lookup"><span data-stu-id="766de-136">These port numbers can be different.</span></span> <span data-ttu-id="766de-137">公用端口是客户端向角色发送请求时使用的端口。</span><span class="sxs-lookup"><span data-stu-id="766de-137">The public port is what clients use when they send a request to the role.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image8.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image7.png)

## <a name="configure-web-api-for-self-host"></a><span data-ttu-id="766de-138">为 Self-Host 配置 Web API</span><span class="sxs-lookup"><span data-stu-id="766de-138">Configure Web API for Self-Host</span></span>

<span data-ttu-id="766de-139">在解决方案资源管理器中，右键单击 WorkerRole1 项目，然后选择 "**添加**  /  **类**" 添加新类。</span><span class="sxs-lookup"><span data-stu-id="766de-139">In Solution Explorer, right click the WorkerRole1 project and select **Add** / **Class** to add a new class.</span></span> <span data-ttu-id="766de-140">命名类 `Startup`。</span><span class="sxs-lookup"><span data-stu-id="766de-140">Name the class `Startup`.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image9.png)

<span data-ttu-id="766de-141">将此文件中的所有样本代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="766de-141">Replace all of the boilerplate code in this file with the following:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample2.cs)]

## <a name="add-a-web-api-controller"></a><span data-ttu-id="766de-142">添加 Web API 控制器</span><span class="sxs-lookup"><span data-stu-id="766de-142">Add a Web API Controller</span></span>

<span data-ttu-id="766de-143">接下来，添加 Web API 控制器类。</span><span class="sxs-lookup"><span data-stu-id="766de-143">Next, add a Web API controller class.</span></span> <span data-ttu-id="766de-144">右键单击 "WorkerRole1" 项目，然后选择 "**添加**  /  **类**"。</span><span class="sxs-lookup"><span data-stu-id="766de-144">Right-click the WorkerRole1 project and select **Add** / **Class**.</span></span> <span data-ttu-id="766de-145">将类命名为 TestController。</span><span class="sxs-lookup"><span data-stu-id="766de-145">Name the class TestController.</span></span> <span data-ttu-id="766de-146">将此文件中的所有样本代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="766de-146">Replace all of the boilerplate code in this file with the following:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample3.cs)]

<span data-ttu-id="766de-147">为简单起见，此控制器只定义了两个返回纯文本的 GET 方法。</span><span class="sxs-lookup"><span data-stu-id="766de-147">For simplicity, this controller just defines two GET methods that return plain text.</span></span>

## <a name="start-the-owin-host"></a><span data-ttu-id="766de-148">启动 OWIN 主机</span><span class="sxs-lookup"><span data-stu-id="766de-148">Start the OWIN Host</span></span>

<span data-ttu-id="766de-149">打开 WorkerRole.cs 文件。</span><span class="sxs-lookup"><span data-stu-id="766de-149">Open the WorkerRole.cs file.</span></span> <span data-ttu-id="766de-150">此类定义在启动和停止辅助角色时运行的代码。</span><span class="sxs-lookup"><span data-stu-id="766de-150">This class defines the code that runs when the worker role is started and stopped.</span></span>

<span data-ttu-id="766de-151">添加以下 using 语句：</span><span class="sxs-lookup"><span data-stu-id="766de-151">Add the following using statement:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample4.cs)]

<span data-ttu-id="766de-152">将 **IDisposable** 成员添加到 `WorkerRole` 类：</span><span class="sxs-lookup"><span data-stu-id="766de-152">Add an **IDisposable** member to the `WorkerRole` class:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample5.cs)]

<span data-ttu-id="766de-153">在 `OnStart` 方法中，添加以下代码以启动主机：</span><span class="sxs-lookup"><span data-stu-id="766de-153">In the `OnStart` method, add the following code to start the host:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample6.cs?highlight=5)]

<span data-ttu-id="766de-154">**WebApp** 方法启动 OWIN 主机。</span><span class="sxs-lookup"><span data-stu-id="766de-154">The **WebApp.Start** method starts the OWIN host.</span></span> <span data-ttu-id="766de-155">类的名称 `Startup` 是方法的类型参数。</span><span class="sxs-lookup"><span data-stu-id="766de-155">The name of the `Startup` class is a type parameter to the method.</span></span> <span data-ttu-id="766de-156">按照约定，主机将调用 `Configure` 此类的方法。</span><span class="sxs-lookup"><span data-stu-id="766de-156">By convention, the host will call the `Configure` method of this class.</span></span>

<span data-ttu-id="766de-157">重写 `OnStop` 以释放 *\_ 应用程序* 实例：</span><span class="sxs-lookup"><span data-stu-id="766de-157">Override the `OnStop` to dispose of the *\_app* instance:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample7.cs)]

<span data-ttu-id="766de-158">下面是 WorkerRole.cs 的完整代码：</span><span class="sxs-lookup"><span data-stu-id="766de-158">Here is the complete code for WorkerRole.cs:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample8.cs)]

<span data-ttu-id="766de-159">生成解决方案，然后按 F5 在 Azure 计算模拟器中本地运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="766de-159">Build the solution, and press F5 to run the application locally in the Azure Compute Emulator.</span></span> <span data-ttu-id="766de-160">根据防火墙设置，你可能需要通过防火墙允许模拟器。</span><span class="sxs-lookup"><span data-stu-id="766de-160">Depending on your firewall settings, you might need to allow the emulator through your firewall.</span></span>

> [!NOTE]
> <span data-ttu-id="766de-161">如果收到如下所示的异常，请参阅 [此博客文章](https://blogs.msdn.com/b/praburaj/archive/2013/11/20/fileloadexception-on-microsoft-owin-when-running-on-worker-role.aspx) 了解解决方法。</span><span class="sxs-lookup"><span data-stu-id="766de-161">If you get an exception like the following, please see [this blog post](https://blogs.msdn.com/b/praburaj/archive/2013/11/20/fileloadexception-on-microsoft-owin-when-running-on-worker-role.aspx) for a workaround.</span></span> <span data-ttu-id="766de-162">"无法加载文件或程序集" Owin，Version = 2.0.2.0，Culture = 中立，PublicKeyToken = 31bf3856ad364e35 "或其依赖项之一。</span><span class="sxs-lookup"><span data-stu-id="766de-162">"Could not load file or assembly 'Microsoft.Owin, Version=2.0.2.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' or one of its dependencies.</span></span> <span data-ttu-id="766de-163">找到的程序集清单定义与程序集引用不匹配。</span><span class="sxs-lookup"><span data-stu-id="766de-163">The located assembly's manifest definition does not match the assembly reference.</span></span> <span data-ttu-id="766de-164"> (HRESULT 中的异常： 0x80131040) "</span><span class="sxs-lookup"><span data-stu-id="766de-164">(Exception from HRESULT: 0x80131040)"</span></span>

<span data-ttu-id="766de-165">计算模拟器将本地 IP 地址分配到终结点。</span><span class="sxs-lookup"><span data-stu-id="766de-165">The compute emulator assigns a local IP address to the endpoint.</span></span> <span data-ttu-id="766de-166">可以通过查看计算模拟器 UI 来查找 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="766de-166">You can find the IP address by viewing the Compute Emulator UI.</span></span> <span data-ttu-id="766de-167">右键单击任务栏通知区域中的模拟器图标，然后选择 " **显示计算模拟器 UI**"。</span><span class="sxs-lookup"><span data-stu-id="766de-167">Right-click the emulator icon in the task bar notification area, and select **Show Compute Emulator UI**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image11.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image10.png)

<span data-ttu-id="766de-168">查找服务部署、部署 [id] 和服务详细信息下的 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="766de-168">Find the IP address under Service Deployments, deployment [id], Service Details.</span></span> <span data-ttu-id="766de-169">打开 web 浏览器并导航到 http://<em>address</em>/test/1，其中 <em>address</em> 是计算模拟器分配的 IP 地址;例如， `http://127.0.0.1:80/test/1` 。</span><span class="sxs-lookup"><span data-stu-id="766de-169">Open a web browser and navigate to http://<em>address</em>/test/1, where <em>address</em> is the IP address assigned by the compute emulator; for example, `http://127.0.0.1:80/test/1`.</span></span> <span data-ttu-id="766de-170">应会看到来自 Web API 控制器的响应：</span><span class="sxs-lookup"><span data-stu-id="766de-170">You should see the response from the Web API controller:</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image12.png)

## <a name="deploy-to-azure"></a><span data-ttu-id="766de-171">部署到 Azure</span><span class="sxs-lookup"><span data-stu-id="766de-171">Deploy to Azure</span></span>

<span data-ttu-id="766de-172">对于此步骤，你必须有一个 Azure 帐户。</span><span class="sxs-lookup"><span data-stu-id="766de-172">For this step, you must have an Azure account.</span></span> <span data-ttu-id="766de-173">如果还没有，只需花费几分钟就能创建一个免费试用帐户。</span><span class="sxs-lookup"><span data-stu-id="766de-173">If you don't already have one, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="766de-174">有关详细信息，请参阅 [Microsoft Azure 免费试用版](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)。</span><span class="sxs-lookup"><span data-stu-id="766de-174">For details, see [Microsoft Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>

<span data-ttu-id="766de-175">在解决方案资源管理器中，右键单击 AzureApp 项目。</span><span class="sxs-lookup"><span data-stu-id="766de-175">In Solution Explorer, right-click the AzureApp project.</span></span> <span data-ttu-id="766de-176">选择“发布”。</span><span class="sxs-lookup"><span data-stu-id="766de-176">Select **Publish**.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image13.png)

<span data-ttu-id="766de-177">如果尚未登录到 Azure 帐户，请单击 " **登录**"。</span><span class="sxs-lookup"><span data-stu-id="766de-177">If you are not signed in to your Azure account, click **Sign In**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image15.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image14.png)

<span data-ttu-id="766de-178">登录后，选择一个订阅，然后单击 " **下一步**"。</span><span class="sxs-lookup"><span data-stu-id="766de-178">After you are signed in, choose a subscription and click **Next**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image17.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image16.png)

<span data-ttu-id="766de-179">输入云服务的名称，并选择区域。</span><span class="sxs-lookup"><span data-stu-id="766de-179">Enter a name for the cloud service and choose a region.</span></span> <span data-ttu-id="766de-180">单击“创建”。</span><span class="sxs-lookup"><span data-stu-id="766de-180">Click **Create**.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image18.png)

<span data-ttu-id="766de-181">单击“发布”。 </span><span class="sxs-lookup"><span data-stu-id="766de-181">Click **Publish**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image20.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image19.png)

<span data-ttu-id="766de-182">"Azure 活动日志" 窗口显示部署的进度。</span><span class="sxs-lookup"><span data-stu-id="766de-182">The Azure Activity Log window shows the progress of the deployment.</span></span> <span data-ttu-id="766de-183">部署应用后，请浏览到 http://appname.cloudapp.net/test/1 。</span><span class="sxs-lookup"><span data-stu-id="766de-183">When the app is deployed, browse to http://appname.cloudapp.net/test/1.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image21.png)

## <a name="additional-resources"></a><span data-ttu-id="766de-184">其他资源</span><span class="sxs-lookup"><span data-stu-id="766de-184">Additional Resources</span></span>

- [<span data-ttu-id="766de-185">项目 Katana 概述</span><span class="sxs-lookup"><span data-stu-id="766de-185">An Overview of Project Katana</span></span>](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)
- [<span data-ttu-id="766de-186">GitHub 上的 Katana 项目</span><span class="sxs-lookup"><span data-stu-id="766de-186">Katana Project on GitHub</span></span>](https://github.com/aspnet/AspNetKatana)

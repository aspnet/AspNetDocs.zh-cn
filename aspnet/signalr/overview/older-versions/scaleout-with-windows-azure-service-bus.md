---
uid: signalr/overview/older-versions/scaleout-with-windows-azure-service-bus
title: SignalR 扩展与 Azure 服务总线（SignalR 1.x） |Microsoft Docs
author: bradygaster
description: ''
ms.author: bradyg
ms.date: 05/01/2013
ms.assetid: 501db899-e68c-49ff-81b2-1dc561bfe908
msc.legacyurl: /signalr/overview/older-versions/scaleout-with-windows-azure-service-bus
msc.type: authoredcontent
ms.openlocfilehash: e64f84db00b571c01ea52f48d1ac1af46698d391
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449936"
---
# <a name="signalr-scaleout-with-azure-service-bus-signalr-1x"></a><span data-ttu-id="f4e12-102">使用 Azure 服务总线的 SignalR 横向扩展 (SignalR 1.x)</span><span class="sxs-lookup"><span data-stu-id="f4e12-102">SignalR Scaleout with Azure Service Bus (SignalR 1.x)</span></span>

<span data-ttu-id="f4e12-103">作者： [Mike Wasson](https://github.com/MikeWasson)， [Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="f4e12-103">by [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

<span data-ttu-id="f4e12-104">在本教程中，将 SignalR 应用程序部署到 Microsoft Azure Web 角色，使用服务总线底板将消息分发给每个角色实例。</span><span class="sxs-lookup"><span data-stu-id="f4e12-104">In this tutorial, you will deploy a SignalR application to a Windows Azure Web Role, using the Service Bus backplane to distribute messages to each role instance.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image1.png)

<span data-ttu-id="f4e12-105">先决条件：</span><span class="sxs-lookup"><span data-stu-id="f4e12-105">Prerequisites:</span></span>

- <span data-ttu-id="f4e12-106">一个 Microsoft Azure 帐户。</span><span class="sxs-lookup"><span data-stu-id="f4e12-106">A Windows Azure account.</span></span>
- <span data-ttu-id="f4e12-107">[Windows AZURE SDK](https://go.microsoft.com/fwlink/?linkid=254364&amp;clcid=0x409)。</span><span class="sxs-lookup"><span data-stu-id="f4e12-107">The [Windows Azure SDK](https://go.microsoft.com/fwlink/?linkid=254364&amp;clcid=0x409).</span></span>
- <span data-ttu-id="f4e12-108">Visual Studio 2012。</span><span class="sxs-lookup"><span data-stu-id="f4e12-108">Visual Studio 2012.</span></span>

<span data-ttu-id="f4e12-109">Service bus 底板还与[适用于 Windows Server 的服务总线](https://msdn.microsoft.com/library/windowsazure/dn282144.aspx)版本1.1 兼容。</span><span class="sxs-lookup"><span data-stu-id="f4e12-109">The service bus backplane is also compatible with [Service Bus for Windows Server](https://msdn.microsoft.com/library/windowsazure/dn282144.aspx), version 1.1.</span></span> <span data-ttu-id="f4e12-110">但是，它与适用于 Windows Server 的服务总线1.0 版不兼容。</span><span class="sxs-lookup"><span data-stu-id="f4e12-110">However, it is not compatible with version 1.0 of Service Bus for Windows Server.</span></span>

## <a name="pricing"></a><span data-ttu-id="f4e12-111">定价</span><span class="sxs-lookup"><span data-stu-id="f4e12-111">Pricing</span></span>

<span data-ttu-id="f4e12-112">Service Bus 底板使用主题发送消息。</span><span class="sxs-lookup"><span data-stu-id="f4e12-112">The Service Bus backplane uses topics to send messages.</span></span> <span data-ttu-id="f4e12-113">有关最新定价信息，请参阅[服务总线](https://azure.microsoft.com/pricing/details/service-bus/)。</span><span class="sxs-lookup"><span data-stu-id="f4e12-113">For the latest pricing information, see [Service Bus](https://azure.microsoft.com/pricing/details/service-bus/).</span></span> <span data-ttu-id="f4e12-114">撰写本文时，可以每月发送1000000条消息，小于 $1。</span><span class="sxs-lookup"><span data-stu-id="f4e12-114">At the time of this writing, you can send 1,000,000 messages per month for less than $1.</span></span> <span data-ttu-id="f4e12-115">该底板为 SignalR 集线器方法的每个调用发送服务总线消息。</span><span class="sxs-lookup"><span data-stu-id="f4e12-115">The backplane sends a service bus message for each invocation of a SignalR hub method.</span></span> <span data-ttu-id="f4e12-116">还有一些用于连接、断开连接、加入或离开组等的控制消息。</span><span class="sxs-lookup"><span data-stu-id="f4e12-116">There are also some control messages for connections, disconnections, joining or leaving groups, and so forth.</span></span> <span data-ttu-id="f4e12-117">在大多数应用程序中，大多数消息流量均为集线器方法调用。</span><span class="sxs-lookup"><span data-stu-id="f4e12-117">In most applications, the majority of the message traffic will be hub method invocations.</span></span>

## <a name="overview"></a><span data-ttu-id="f4e12-118">概述</span><span class="sxs-lookup"><span data-stu-id="f4e12-118">Overview</span></span>

<span data-ttu-id="f4e12-119">在学习详细教程之前，下面简要概述了你将执行的操作。</span><span class="sxs-lookup"><span data-stu-id="f4e12-119">Before we get to the detailed tutorial, here is a quick overview of what you will do.</span></span>

1. <span data-ttu-id="f4e12-120">使用 Windows Azure 门户创建新的 Service Bus 命名空间。</span><span class="sxs-lookup"><span data-stu-id="f4e12-120">Use the Windows Azure portal to create a new Service Bus namespace.</span></span>
2. <span data-ttu-id="f4e12-121">将以下 NuGet 包添加到应用程序：</span><span class="sxs-lookup"><span data-stu-id="f4e12-121">Add these NuGet packages to your application:</span></span> 

    - [<span data-ttu-id="f4e12-122">SignalR</span><span class="sxs-lookup"><span data-stu-id="f4e12-122">Microsoft.AspNet.SignalR</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [<span data-ttu-id="f4e12-123">SignalR。</span><span class="sxs-lookup"><span data-stu-id="f4e12-123">Microsoft.AspNet.SignalR.ServiceBus</span></span>](http://www.nuget.org/packages/SignalR.WindowsAzureServiceBus)
3. <span data-ttu-id="f4e12-124">创建 SignalR 应用程序。</span><span class="sxs-lookup"><span data-stu-id="f4e12-124">Create a SignalR application.</span></span>
4. <span data-ttu-id="f4e12-125">将以下代码添加到 global.asax 以配置底板：</span><span class="sxs-lookup"><span data-stu-id="f4e12-125">Add the following code to Global.asax to configure the backplane:</span></span> 

    [!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample1.cs)]

<span data-ttu-id="f4e12-126">对于每个应用程序，请为 "YourAppName" 选择不同的值。</span><span class="sxs-lookup"><span data-stu-id="f4e12-126">For each application, pick a different value for "YourAppName".</span></span> <span data-ttu-id="f4e12-127">不要跨多个应用程序使用相同的值。</span><span class="sxs-lookup"><span data-stu-id="f4e12-127">Do not use the same value across multiple applications.</span></span>

## <a name="create-the-azure-services"></a><span data-ttu-id="f4e12-128">创建 Azure 服务</span><span class="sxs-lookup"><span data-stu-id="f4e12-128">Create the Azure Services</span></span>

<span data-ttu-id="f4e12-129">按照[如何创建和部署云服务](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy)中的说明创建云服务。</span><span class="sxs-lookup"><span data-stu-id="f4e12-129">Create a Cloud Service, as described in [How to Create and Deploy a Cloud Service](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy).</span></span> <span data-ttu-id="f4e12-130">按照 "如何：使用快速创建创建云服务" 一节中的步骤进行操作。</span><span class="sxs-lookup"><span data-stu-id="f4e12-130">Follow the steps in the section "How to: Create a cloud service using Quick Create".</span></span> <span data-ttu-id="f4e12-131">对于本教程，无需上载证书。</span><span class="sxs-lookup"><span data-stu-id="f4e12-131">For this tutorial, you do not need to upload a certificate.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image2.png)

<span data-ttu-id="f4e12-132">按照[如何使用服务总线主题/订阅](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions)中的说明创建新的服务总线命名空间。</span><span class="sxs-lookup"><span data-stu-id="f4e12-132">Create a new Service Bus namespace, as described in [How to Use Service Bus Topics/Subscriptions](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions).</span></span> <span data-ttu-id="f4e12-133">按照 "创建服务命名空间" 一节中的步骤进行操作。</span><span class="sxs-lookup"><span data-stu-id="f4e12-133">Follow the steps in the section "Create a Service Namespace".</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image3.png)

> [!NOTE]
> <span data-ttu-id="f4e12-134">请确保为云服务和服务总线命名空间选择相同的区域。</span><span class="sxs-lookup"><span data-stu-id="f4e12-134">Make sure to select the same region for the cloud service and the Service Bus namespace.</span></span>

## <a name="create-the-visual-studio-project"></a><span data-ttu-id="f4e12-135">创建 Visual Studio 项目</span><span class="sxs-lookup"><span data-stu-id="f4e12-135">Create the Visual Studio Project</span></span>

<span data-ttu-id="f4e12-136">启动 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="f4e12-136">Start Visual Studio.</span></span> <span data-ttu-id="f4e12-137">在“文件”菜单上，单击“新建项目”</span><span class="sxs-lookup"><span data-stu-id="f4e12-137">From the **File** menu, click **New Project**.</span></span>

<span data-ttu-id="f4e12-138">在 "**新建项目**" 对话框中，展开 "**视觉对象C#** "。</span><span class="sxs-lookup"><span data-stu-id="f4e12-138">In the **New Project** dialog box, expand **Visual C#**.</span></span> <span data-ttu-id="f4e12-139">在 "**已安装模板**" 下，选择 "**云**"，然后选择 " **microsoft Azure 云服务**"。</span><span class="sxs-lookup"><span data-stu-id="f4e12-139">Under **Installed Templates**, select **Cloud** and then select **Windows Azure Cloud Service**.</span></span> <span data-ttu-id="f4e12-140">保持默认值 .NET Framework 4.5。</span><span class="sxs-lookup"><span data-stu-id="f4e12-140">Keep the default .NET Framework 4.5.</span></span> <span data-ttu-id="f4e12-141">将应用程序命名为 ChatService，然后单击 **"确定"** 。</span><span class="sxs-lookup"><span data-stu-id="f4e12-141">Name the application ChatService and click **OK**.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image4.png)

<span data-ttu-id="f4e12-142">在 "**新建 Microsoft Azure 云服务**" 对话框中，选择 "ASP.NET MVC 4 Web 角色"。</span><span class="sxs-lookup"><span data-stu-id="f4e12-142">In the **New Windows Azure Cloud Service** dialog, select ASP.NET MVC 4 Web Role.</span></span> <span data-ttu-id="f4e12-143">单击右箭头按钮（ **&gt;** ）可将该角色添加到解决方案中。</span><span class="sxs-lookup"><span data-stu-id="f4e12-143">Click the right-arrow button (**&gt;**) to add the role to your solution.</span></span>

<span data-ttu-id="f4e12-144">将鼠标悬停在新角色上，使铅笔图标可见。</span><span class="sxs-lookup"><span data-stu-id="f4e12-144">Hover the mouse over the new role, so the pencil icon visible.</span></span> <span data-ttu-id="f4e12-145">单击此图标可重命名角色。</span><span class="sxs-lookup"><span data-stu-id="f4e12-145">Click this icon to rename the role.</span></span> <span data-ttu-id="f4e12-146">将角色命名为 "SignalRChat"，然后单击 **"确定**"。</span><span class="sxs-lookup"><span data-stu-id="f4e12-146">Name the role "SignalRChat" and click **OK**.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image5.png)

<span data-ttu-id="f4e12-147">在**New ASP.NET MVC 4 项目**向导中，选择 " **Internet 应用程序**"。</span><span class="sxs-lookup"><span data-stu-id="f4e12-147">In the **New ASP.NET MVC 4 Project** wizard, select **Internet Application**.</span></span> <span data-ttu-id="f4e12-148">单击“确定”。</span><span class="sxs-lookup"><span data-stu-id="f4e12-148">Click **OK**.</span></span> <span data-ttu-id="f4e12-149">项目向导将创建两个项目：</span><span class="sxs-lookup"><span data-stu-id="f4e12-149">The project wizard creates two projects:</span></span>

- <span data-ttu-id="f4e12-150">ChatService：此项目是 Microsoft Azure 应用程序。</span><span class="sxs-lookup"><span data-stu-id="f4e12-150">ChatService: This project is the Windows Azure application.</span></span> <span data-ttu-id="f4e12-151">它定义了 Azure 角色和其他配置选项。</span><span class="sxs-lookup"><span data-stu-id="f4e12-151">It defines the Azure roles and other configuration options.</span></span>
- <span data-ttu-id="f4e12-152">SignalRChat：此项目是 ASP.NET MVC 4 项目。</span><span class="sxs-lookup"><span data-stu-id="f4e12-152">SignalRChat: This project is your ASP.NET MVC 4 project.</span></span>

## <a name="create-the-signalr-chat-application"></a><span data-ttu-id="f4e12-153">创建 SignalR Chat 应用程序</span><span class="sxs-lookup"><span data-stu-id="f4e12-153">Create the SignalR Chat Application</span></span>

<span data-ttu-id="f4e12-154">若要创建聊天应用程序，请按照教程[入门 With SignalR AND MVC 4](tutorial-getting-started-with-signalr-and-mvc-4.md)"中的步骤进行操作。</span><span class="sxs-lookup"><span data-stu-id="f4e12-154">To create the chat application, follow the steps in the tutorial [Getting Started with SignalR and MVC 4](tutorial-getting-started-with-signalr-and-mvc-4.md).</span></span>

<span data-ttu-id="f4e12-155">使用 NuGet 安装所需的库。</span><span class="sxs-lookup"><span data-stu-id="f4e12-155">Use NuGet to install the required libraries.</span></span> <span data-ttu-id="f4e12-156">从 "**工具**" 菜单中，选择 " **NuGet 包管理器**"，然后选择 "**程序包管理器控制台**"。</span><span class="sxs-lookup"><span data-stu-id="f4e12-156">From the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="f4e12-157">在 "**程序包管理器控制台**" 窗口中，输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="f4e12-157">In the **Package Manager Console** window, enter the following commands:</span></span>

[!code-powershell[Main](scaleout-with-windows-azure-service-bus/samples/sample2.ps1)]

<span data-ttu-id="f4e12-158">使用 `-ProjectName` 选项将包安装到 ASP.NET MVC 项目，而不是 Windows Azure 项目。</span><span class="sxs-lookup"><span data-stu-id="f4e12-158">Use the `-ProjectName` option to install the packages to the ASP.NET MVC project, rather than the Windows Azure project.</span></span>

## <a name="configure-the-backplane"></a><span data-ttu-id="f4e12-159">配置底板</span><span class="sxs-lookup"><span data-stu-id="f4e12-159">Configure the Backplane</span></span>

<span data-ttu-id="f4e12-160">在应用程序的 global.asax 文件中，添加以下代码：</span><span class="sxs-lookup"><span data-stu-id="f4e12-160">In your application's Global.asax file, add the following code:</span></span>

[!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample3.cs)]

<span data-ttu-id="f4e12-161">现在，需要获取服务总线连接字符串。</span><span class="sxs-lookup"><span data-stu-id="f4e12-161">Now you need to get your service bus connection string.</span></span> <span data-ttu-id="f4e12-162">在 Azure 门户中，选择你创建的服务总线命名空间，然后单击 "访问密钥" 图标。</span><span class="sxs-lookup"><span data-stu-id="f4e12-162">In the Azure portal, select the service bus namespace that you created and click the Access Key icon.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image6.png)

<span data-ttu-id="f4e12-163">将连接字符串复制到剪贴板，然后将其粘贴到*connectionString*变量中。</span><span class="sxs-lookup"><span data-stu-id="f4e12-163">Copy the connection string to the clipboard, then paste it into the *connectionString* variable.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image7.png)

[!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample4.cs)]

## <a name="deploy-to-azure"></a><span data-ttu-id="f4e12-164">部署到 Azure</span><span class="sxs-lookup"><span data-stu-id="f4e12-164">Deploy to Azure</span></span>

<span data-ttu-id="f4e12-165">在解决方案资源管理器中，展开 "ChatService" 项目中的 "**角色**" 文件夹。</span><span class="sxs-lookup"><span data-stu-id="f4e12-165">In Solution Explorer, expand the **Roles** folder inside the ChatService project.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image8.png)

<span data-ttu-id="f4e12-166">右键单击 "SignalRChat" 角色，然后选择 "**属性**"。</span><span class="sxs-lookup"><span data-stu-id="f4e12-166">Right-click the SignalRChat role and select **Properties**.</span></span> <span data-ttu-id="f4e12-167">选择 "**配置**" 选项卡。在 "**实例**" 下选择2。</span><span class="sxs-lookup"><span data-stu-id="f4e12-167">Select the **Configuration** tab. Under **Instances** select 2.</span></span> <span data-ttu-id="f4e12-168">你还可以将 VM 大小设置为 "**特小**"。</span><span class="sxs-lookup"><span data-stu-id="f4e12-168">You can also set the VM size to **Extra Small**.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image9.png)

<span data-ttu-id="f4e12-169">保存更改。</span><span class="sxs-lookup"><span data-stu-id="f4e12-169">Save the changes.</span></span>

<span data-ttu-id="f4e12-170">在解决方案资源管理器中，右键单击 ChatService 项目。</span><span class="sxs-lookup"><span data-stu-id="f4e12-170">In Solution Explorer, right-click the ChatService project.</span></span> <span data-ttu-id="f4e12-171">选择“发布”。</span><span class="sxs-lookup"><span data-stu-id="f4e12-171">Select **Publish**.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image10.png)

<span data-ttu-id="f4e12-172">如果这是您首次发布到 Windows Azure，则必须下载您的凭据。</span><span class="sxs-lookup"><span data-stu-id="f4e12-172">If this is your first time publishing to Windows Azure, you must download your credentials.</span></span> <span data-ttu-id="f4e12-173">在**发布**向导中，单击 "登录以下载凭据"。</span><span class="sxs-lookup"><span data-stu-id="f4e12-173">In the **Publish** wizard, click "Sign in to download credentials".</span></span> <span data-ttu-id="f4e12-174">这会提示你登录到 Windows Azure 门户并下载发布设置文件。</span><span class="sxs-lookup"><span data-stu-id="f4e12-174">This will prompt you to sign into the Windows Azure portal and download a publish settings file.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image11.png)

<span data-ttu-id="f4e12-175">单击 "**导入**" 并选择已下载的发布设置文件。</span><span class="sxs-lookup"><span data-stu-id="f4e12-175">Click **Import** and select the publish settings file that you downloaded.</span></span>

<span data-ttu-id="f4e12-176">单击 **“下一步”** 。</span><span class="sxs-lookup"><span data-stu-id="f4e12-176">Click **Next**.</span></span> <span data-ttu-id="f4e12-177">在 "**发布设置**" 对话框中的 "**云服务**" 下，选择之前创建的云服务。</span><span class="sxs-lookup"><span data-stu-id="f4e12-177">In the **Publish Settings** dialog, under **Cloud Service**, select the cloud service that you created earlier.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image12.png)

<span data-ttu-id="f4e12-178">单击“发布”。</span><span class="sxs-lookup"><span data-stu-id="f4e12-178">Click **Publish**.</span></span> <span data-ttu-id="f4e12-179">部署应用程序并启动 Vm 可能需要几分钟时间。</span><span class="sxs-lookup"><span data-stu-id="f4e12-179">It can take a few minutes to deploy the application and start the VMs.</span></span>

<span data-ttu-id="f4e12-180">现在，在运行聊天应用程序时，角色实例将使用服务总线主题通过 Azure 服务总线进行通信。</span><span class="sxs-lookup"><span data-stu-id="f4e12-180">Now when you run the chat application, the role instances communicate through Azure Service Bus, using a Service Bus topic.</span></span> <span data-ttu-id="f4e12-181">主题是允许多个订阅服务器的消息队列。</span><span class="sxs-lookup"><span data-stu-id="f4e12-181">A topic is a message queue that allows multiple subscribers.</span></span>

<span data-ttu-id="f4e12-182">该底板会自动创建主题和订阅。</span><span class="sxs-lookup"><span data-stu-id="f4e12-182">The backplane automatically creates the topic and the subscriptions.</span></span> <span data-ttu-id="f4e12-183">若要查看订阅和消息活动，请打开 Azure 门户，选择服务总线命名空间，然后单击 "主题"。</span><span class="sxs-lookup"><span data-stu-id="f4e12-183">To see the subscriptions and message activity, open the Azure portal, select the Service Bus namespace, and click on "Topics".</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image13.png)

<span data-ttu-id="f4e12-184">需要几分钟时间，消息活动才会显示在仪表板中。</span><span class="sxs-lookup"><span data-stu-id="f4e12-184">It make take a few minutes for the message activity to show up in the dashboard.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image14.png)

<span data-ttu-id="f4e12-185">SignalR 管理主题生存期。</span><span class="sxs-lookup"><span data-stu-id="f4e12-185">SignalR manages the topic lifetime.</span></span> <span data-ttu-id="f4e12-186">只要部署了你的应用程序，就不要尝试手动删除主题或更改主题的设置。</span><span class="sxs-lookup"><span data-stu-id="f4e12-186">As long as your application is deployed, don't try to manually delete topics or change settings on the topic.</span></span>

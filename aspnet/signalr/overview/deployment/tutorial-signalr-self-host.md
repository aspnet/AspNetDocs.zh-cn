---
uid: signalr/overview/deployment/tutorial-signalr-self-host
title: 教程： SignalR 自承载 |Microsoft Docs
author: bradygaster
description: 本教程演示如何创建自承载的 SignalR 2 服务器，以及如何使用 JavaScript 客户端连接到该服务器。 教程 V 中使用的软件版本 .。。
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 400db427-27af-4f2f-abf0-5486d5e024b5
msc.legacyurl: /signalr/overview/deployment/tutorial-signalr-self-host
msc.type: authoredcontent
ms.openlocfilehash: 7470e0d6b68772ccfd979c834b7db81fbba3ca78
ms.sourcegitcommit: 0cf7d06071a8ff986e6c028ac9daf0c0e7490412
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/23/2020
ms.locfileid: "85240618"
---
# <a name="tutorial-signalr-self-host"></a><span data-ttu-id="3e2bf-104">教程：自承载 SignalR</span><span class="sxs-lookup"><span data-stu-id="3e2bf-104">Tutorial: SignalR Self-Host</span></span>

<span data-ttu-id="3e2bf-105">作者： [Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="3e2bf-105">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="3e2bf-106">本教程演示如何创建自承载的 SignalR 2 服务器，以及如何使用 JavaScript 客户端连接到该服务器。</span><span class="sxs-lookup"><span data-stu-id="3e2bf-106">This tutorial shows how to create a self-hosted SignalR 2 server, and how to connect to it with a JavaScript client.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="3e2bf-107">本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="3e2bf-107">Software versions used in the tutorial</span></span>
>
>
> - [<span data-ttu-id="3e2bf-108">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="3e2bf-108">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="3e2bf-109">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="3e2bf-109">.NET 4.5</span></span>
> - <span data-ttu-id="3e2bf-110">SignalR 版本2</span><span class="sxs-lookup"><span data-stu-id="3e2bf-110">SignalR version 2</span></span>
>
>
>
> ## <a name="using-visual-studio-2012-with-this-tutorial"></a><span data-ttu-id="3e2bf-111">在本教程中使用 Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="3e2bf-111">Using Visual Studio 2012 with this tutorial</span></span>
>
>
> <span data-ttu-id="3e2bf-112">若要在本教程中使用 Visual Studio 2012，请执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="3e2bf-112">To use Visual Studio 2012 with this tutorial, do the following:</span></span>
>
> - <span data-ttu-id="3e2bf-113">将[包管理器](http://docs.nuget.org/docs/start-here/installing-nuget)更新到最新版本。</span><span class="sxs-lookup"><span data-stu-id="3e2bf-113">Update your [Package Manager](http://docs.nuget.org/docs/start-here/installing-nuget) to the latest version.</span></span>
> - <span data-ttu-id="3e2bf-114">安装[Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)。</span><span class="sxs-lookup"><span data-stu-id="3e2bf-114">Install the [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx).</span></span>
> - <span data-ttu-id="3e2bf-115">在 Web 平台安装程序中，搜索并安装适用**于 Visual Studio 2012 的 ASP.NET 和 Web 工具 2013.1**。</span><span class="sxs-lookup"><span data-stu-id="3e2bf-115">In the Web Platform Installer, search for and install **ASP.NET and Web Tools 2013.1 for Visual Studio 2012**.</span></span> <span data-ttu-id="3e2bf-116">这会为 SignalR 类（例如**中心**）安装 Visual Studio 模板。</span><span class="sxs-lookup"><span data-stu-id="3e2bf-116">This will install Visual Studio templates for SignalR classes such as **Hub**.</span></span>
> - <span data-ttu-id="3e2bf-117">某些模板（如**OWIN Startup 类**）将不可用;对于这些情况，请改用类文件。</span><span class="sxs-lookup"><span data-stu-id="3e2bf-117">Some templates (such as **OWIN Startup Class**) will not be available; for these, use a Class file instead.</span></span>
>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="3e2bf-118">问题和注释</span><span class="sxs-lookup"><span data-stu-id="3e2bf-118">Questions and comments</span></span>
>
> <span data-ttu-id="3e2bf-119">请提供有关你喜欢本教程的方式的反馈，并在页面底部的评论中留下反馈。</span><span class="sxs-lookup"><span data-stu-id="3e2bf-119">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="3e2bf-120">如果你有与本教程不直接相关的问题，则可以将其发布到[ASP.NET SignalR 论坛](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com/)。</span><span class="sxs-lookup"><span data-stu-id="3e2bf-120">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="overview"></a><span data-ttu-id="3e2bf-121">概述</span><span class="sxs-lookup"><span data-stu-id="3e2bf-121">Overview</span></span>

<span data-ttu-id="3e2bf-122">SignalR 服务器通常托管在 IIS 的 ASP.NET 应用程序中，但也可以使用自承载库自承载（如控制台应用程序或 Windows 服务）。</span><span class="sxs-lookup"><span data-stu-id="3e2bf-122">A SignalR server is usually hosted in an ASP.NET application in IIS, but it can also be self-hosted (such as in a console application or Windows service) using the self-host library.</span></span> <span data-ttu-id="3e2bf-123">此库与所有 SignalR 2 一样，都是在 OWIN （[.net 的开放 Web 接口](http://owin.org)）上构建的。</span><span class="sxs-lookup"><span data-stu-id="3e2bf-123">This library, like all of SignalR 2, is built on OWIN ([Open Web Interface for .NET](http://owin.org)).</span></span> <span data-ttu-id="3e2bf-124">OWIN 定义 .NET web 服务器和 web 应用程序之间的抽象。</span><span class="sxs-lookup"><span data-stu-id="3e2bf-124">OWIN defines an abstraction between .NET web servers and web applications.</span></span> <span data-ttu-id="3e2bf-125">OWIN 将 web 应用程序与服务器分离，这使得 OWIN 非常适合用于在你自己的进程（IIS 以外）中自承载 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="3e2bf-125">OWIN decouples the web application from the server, which makes OWIN ideal for self-hosting a web application in your own process, outside of IIS.</span></span>

<span data-ttu-id="3e2bf-126">不在 IIS 中托管的原因包括：</span><span class="sxs-lookup"><span data-stu-id="3e2bf-126">Reasons for not hosting in IIS include:</span></span>

- <span data-ttu-id="3e2bf-127">IIS 不可用或不需要的环境，如没有 IIS 的现有服务器场。</span><span class="sxs-lookup"><span data-stu-id="3e2bf-127">Environments where IIS is not available or desirable, such as an existing server farm without IIS.</span></span>
- <span data-ttu-id="3e2bf-128">需要避免 IIS 的性能开销。</span><span class="sxs-lookup"><span data-stu-id="3e2bf-128">The performance overhead of IIS needs to be avoided.</span></span>
- <span data-ttu-id="3e2bf-129">SignalR 功能将添加到在 Windows 服务、Azure 辅助角色或其他进程中运行的现有应用程序。</span><span class="sxs-lookup"><span data-stu-id="3e2bf-129">SignalR functionality is to be added to an existing application that runs in a Windows Service, Azure worker role, or other process.</span></span>

<span data-ttu-id="3e2bf-130">如果出于性能方面的原因，将解决方案作为自宿主进行开发，则建议也测试在 IIS 中托管的应用程序，以确定性能优势。</span><span class="sxs-lookup"><span data-stu-id="3e2bf-130">If a solution is being developed as self-host for performance reasons, it's recommended to also test the application hosted in IIS to determine the performance benefit.</span></span>

<span data-ttu-id="3e2bf-131">本教程包含以下部分：</span><span class="sxs-lookup"><span data-stu-id="3e2bf-131">This tutorial contains the following sections:</span></span>

- [<span data-ttu-id="3e2bf-132">创建服务器</span><span class="sxs-lookup"><span data-stu-id="3e2bf-132">Creating the server</span></span>](#server)
- [<span data-ttu-id="3e2bf-133">使用 JavaScript 客户端访问服务器</span><span class="sxs-lookup"><span data-stu-id="3e2bf-133">Accessing the server with a JavaScript client</span></span>](#js)

<a id="server"></a>

## <a name="creating-the-server"></a><span data-ttu-id="3e2bf-134">创建服务器</span><span class="sxs-lookup"><span data-stu-id="3e2bf-134">Creating the server</span></span>

<span data-ttu-id="3e2bf-135">在本教程中，你将创建一个托管在控制台应用程序中的服务器，但该服务器可以托管在任何类型的进程中，如 Windows 服务或 Azure 辅助角色。</span><span class="sxs-lookup"><span data-stu-id="3e2bf-135">In this tutorial, you'll create a server that's hosted in a console application, but the server can be hosted in any sort of process, such as a Windows service or Azure worker role.</span></span> <span data-ttu-id="3e2bf-136">有关在 Windows 服务中承载 SignalR 服务器的示例代码，请参阅[Windows 服务中的自承载 SignalR](https://code.msdn.microsoft.com/SignalR-self-hosted-in-6ff7e6c3)。</span><span class="sxs-lookup"><span data-stu-id="3e2bf-136">For sample code for hosting a SignalR server in a Windows Service, see [Self-Hosting SignalR in a Windows Service](https://code.msdn.microsoft.com/SignalR-self-hosted-in-6ff7e6c3).</span></span>

1. <span data-ttu-id="3e2bf-137">以管理员权限打开 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="3e2bf-137">Open Visual Studio 2013 with administrator privileges.</span></span> <span data-ttu-id="3e2bf-138">选择 "**文件**"、"**新建项目**"。</span><span class="sxs-lookup"><span data-stu-id="3e2bf-138">Select **File**, **New Project**.</span></span> <span data-ttu-id="3e2bf-139">在 "**模板**" 窗格中的 " **Visual c #** " 节点下选择 " **Windows** "，然后选择 "**控制台应用程序**" 模板。</span><span class="sxs-lookup"><span data-stu-id="3e2bf-139">Select **Windows** under the **Visual C#** node in the **Templates** pane, and select the **Console Application** template.</span></span> <span data-ttu-id="3e2bf-140">将新项目命名为 "SignalRSelfHost"，然后单击 **"确定**"。</span><span class="sxs-lookup"><span data-stu-id="3e2bf-140">Name the new project "SignalRSelfHost" and click **OK**.</span></span>

    ![](tutorial-signalr-self-host/_static/image1.png)
2. <span data-ttu-id="3e2bf-141">通过选择 "**工具**" "  >  **nuget 包管理**器" "  >  **包管理器控制台**"，打开 NuGet 包管理器控制台。</span><span class="sxs-lookup"><span data-stu-id="3e2bf-141">Open the NuGet package manager console by selecting **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>
3. <span data-ttu-id="3e2bf-142">在 "程序包管理器控制台" 中，输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="3e2bf-142">In the package manager console, enter the following command:</span></span>

    [!code-powershell[Main](tutorial-signalr-self-host/samples/sample1.ps1)]

    <span data-ttu-id="3e2bf-143">此命令将 SignalR 2 自承载库添加到项目。</span><span class="sxs-lookup"><span data-stu-id="3e2bf-143">This command adds the SignalR 2 Self-Host libraries to the project.</span></span>
4. <span data-ttu-id="3e2bf-144">在 "程序包管理器控制台" 中，输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="3e2bf-144">In the package manager console, enter the following command:</span></span>

    [!code-powershell[Main](tutorial-signalr-self-host/samples/sample2.ps1)]

    <span data-ttu-id="3e2bf-145">此命令将 Owin 库添加到项目。</span><span class="sxs-lookup"><span data-stu-id="3e2bf-145">This command adds the Microsoft.Owin.Cors library to the project.</span></span> <span data-ttu-id="3e2bf-146">此库将用于跨域支持，此支持是在不同域中承载 SignalR 和网页客户端的应用程序所必需的。</span><span class="sxs-lookup"><span data-stu-id="3e2bf-146">This library will be used for cross-domain support, which is required for applications that host SignalR and a web page client in different domains.</span></span> <span data-ttu-id="3e2bf-147">由于你将在不同的端口上托管 SignalR 服务器和 web 客户端，因此这意味着必须启用跨域，以便在这些组件之间进行通信。</span><span class="sxs-lookup"><span data-stu-id="3e2bf-147">Since you'll be hosting the SignalR server and the web client on different ports, this means that cross-domain must be enabled for communication between these components.</span></span>
5. <span data-ttu-id="3e2bf-148">将 Program.cs 的内容替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="3e2bf-148">Replace the contents of Program.cs with the following code.</span></span>

    [!code-csharp[Main](tutorial-signalr-self-host/samples/sample3.cs)]

    <span data-ttu-id="3e2bf-149">上面的代码包括三个类：</span><span class="sxs-lookup"><span data-stu-id="3e2bf-149">The above code includes three classes:</span></span>

    - <span data-ttu-id="3e2bf-150">**程序**，包括定义主执行路径的**Main**方法。</span><span class="sxs-lookup"><span data-stu-id="3e2bf-150">**Program**, including the **Main** method defining the primary path of execution.</span></span> <span data-ttu-id="3e2bf-151">在此方法中，**启动类型为**的 web 应用程序是在指定的 URL （）启动的 `http://localhost:8080` 。</span><span class="sxs-lookup"><span data-stu-id="3e2bf-151">In this method, a web application of type **Startup** is started at the specified URL (`http://localhost:8080`).</span></span> <span data-ttu-id="3e2bf-152">如果终结点上需要安全性，则可以实现 SSL。</span><span class="sxs-lookup"><span data-stu-id="3e2bf-152">If security is required on the endpoint, SSL can be implemented.</span></span> <span data-ttu-id="3e2bf-153">有关详细信息，请参阅[如何：使用 SSL 证书配置端口](https://msdn.microsoft.com/library/ms733791.aspx)。</span><span class="sxs-lookup"><span data-stu-id="3e2bf-153">See [How to: Configure a Port with an SSL Certificate](https://msdn.microsoft.com/library/ms733791.aspx) for more information.</span></span>
    - <span data-ttu-id="3e2bf-154">**启动**时，包含 SignalR 服务器的配置的类（本教程使用的唯一配置是对的调用 `UseCors` ）以及对的调用 `MapSignalR` ，后者为项目中的任何中心对象创建路由。</span><span class="sxs-lookup"><span data-stu-id="3e2bf-154">**Startup**, the class containing the configuration for the SignalR server (the only configuration this tutorial uses is the call to `UseCors`), and the call to `MapSignalR`, which creates routes for any Hub objects in the project.</span></span>
    - <span data-ttu-id="3e2bf-155">**MyHub**，应用程序将提供给客户端的 SignalR Hub 类。</span><span class="sxs-lookup"><span data-stu-id="3e2bf-155">**MyHub**, the SignalR Hub class that the application will provide to clients.</span></span> <span data-ttu-id="3e2bf-156">此类有一个方法 "**发送**"，客户端将调用以将消息广播到所有其他已连接的客户端。</span><span class="sxs-lookup"><span data-stu-id="3e2bf-156">This class has a single method, **Send**, that clients will call to broadcast a message to all other connected clients.</span></span>
6. <span data-ttu-id="3e2bf-157">编译并运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="3e2bf-157">Compile and run the application.</span></span> <span data-ttu-id="3e2bf-158">运行服务器的地址应显示在控制台窗口中。</span><span class="sxs-lookup"><span data-stu-id="3e2bf-158">The address that the server is running should show in a console window.</span></span>

    ![](tutorial-signalr-self-host/_static/image2.png)
7. <span data-ttu-id="3e2bf-159">如果执行失败并出现异常 `System.Reflection.TargetInvocationException was unhandled` ，你将需要重新启动具有管理员权限的 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="3e2bf-159">If execution fails with the exception `System.Reflection.TargetInvocationException was unhandled`, you will need to restart Visual Studio with administrator privileges.</span></span>
8. <span data-ttu-id="3e2bf-160">停止应用程序，然后继续下一部分。</span><span class="sxs-lookup"><span data-stu-id="3e2bf-160">Stop the application before proceeding to the next section.</span></span>

<a id="js"></a>

## <a name="accessing-the-server-with-a-javascript-client"></a><span data-ttu-id="3e2bf-161">使用 JavaScript 客户端访问服务器</span><span class="sxs-lookup"><span data-stu-id="3e2bf-161">Accessing the server with a JavaScript client</span></span>

<span data-ttu-id="3e2bf-162">在本部分中，你将使用[入门教程](../getting-started/tutorial-getting-started-with-signalr.md)中的相同 JavaScript 客户端。</span><span class="sxs-lookup"><span data-stu-id="3e2bf-162">In this section, you'll use the same JavaScript client from the [Getting Started tutorial](../getting-started/tutorial-getting-started-with-signalr.md).</span></span> <span data-ttu-id="3e2bf-163">我们只会对客户端进行一项修改，即显式定义中心 URL。</span><span class="sxs-lookup"><span data-stu-id="3e2bf-163">We'll only make one modification to the client, which is to explicitly define the hub URL.</span></span> <span data-ttu-id="3e2bf-164">对于自承载的应用程序，服务器可能不一定与连接 URL 位于同一地址（因为反向代理和负载均衡器），因此需要显式定义 URL。</span><span class="sxs-lookup"><span data-stu-id="3e2bf-164">With a self-hosted application, the server may not necessarily be at the same address as the connection URL (due to reverse proxies and load balancers), so the URL needs to be defined explicitly.</span></span>

1. <span data-ttu-id="3e2bf-165">在**解决方案资源管理器**中，右键单击解决方案并选择 "**添加**"、"**新建项目**"。</span><span class="sxs-lookup"><span data-stu-id="3e2bf-165">In **Solution Explorer**, right-click on the solution and select **Add**, **New Project**.</span></span> <span data-ttu-id="3e2bf-166">选择 " **web** " 节点，然后选择 " **ASP.NET Web 应用程序**" 模板。</span><span class="sxs-lookup"><span data-stu-id="3e2bf-166">Select the **Web** node, and select the **ASP.NET Web Application** template.</span></span> <span data-ttu-id="3e2bf-167">将项目命名为 "JavascriptClient"，然后单击 **"确定**"。</span><span class="sxs-lookup"><span data-stu-id="3e2bf-167">Name the project "JavascriptClient" and click **OK**.</span></span>

    ![](tutorial-signalr-self-host/_static/image3.png)
2. <span data-ttu-id="3e2bf-168">选择**空**模板，并保留未选定的其余选项。</span><span class="sxs-lookup"><span data-stu-id="3e2bf-168">Select the **Empty** template, and leave the remaining options unselected.</span></span> <span data-ttu-id="3e2bf-169">选择 "**创建项目**"。</span><span class="sxs-lookup"><span data-stu-id="3e2bf-169">Select **Create Project**.</span></span>

    ![](tutorial-signalr-self-host/_static/image4.png)
3. <span data-ttu-id="3e2bf-170">在 "程序包管理器控制台" 中，选择 "**默认项目**" 下拉下的 "JavascriptClient" 项目，然后执行以下命令：</span><span class="sxs-lookup"><span data-stu-id="3e2bf-170">In the package manager console, select the "JavascriptClient" project in the **Default project** drop-down, and execute the following command:</span></span>

    [!code-powershell[Main](tutorial-signalr-self-host/samples/sample4.ps1)]

    <span data-ttu-id="3e2bf-171">此命令安装客户端中所需的 SignalR 和 JQuery 库。</span><span class="sxs-lookup"><span data-stu-id="3e2bf-171">This command installs the SignalR and JQuery libraries that you'll need in the client.</span></span>
4. <span data-ttu-id="3e2bf-172">右键单击项目，然后选择 "**添加**"、"**新建项**"。</span><span class="sxs-lookup"><span data-stu-id="3e2bf-172">Right-click on your project and select **Add**, **New Item**.</span></span> <span data-ttu-id="3e2bf-173">选择 " **Web** " 节点，然后选择 "HTML 页"。</span><span class="sxs-lookup"><span data-stu-id="3e2bf-173">Select the **Web** node, and select HTML Page.</span></span> <span data-ttu-id="3e2bf-174">将页面命名**Default.html**。</span><span class="sxs-lookup"><span data-stu-id="3e2bf-174">Name the page **Default.html**.</span></span>

    ![](tutorial-signalr-self-host/_static/image5.png)
5. <span data-ttu-id="3e2bf-175">将新 HTML 页面的内容替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="3e2bf-175">Replace the contents of the new HTML page with the following code.</span></span> <span data-ttu-id="3e2bf-176">验证此处的脚本引用是否与项目的 Scripts 文件夹中的脚本匹配。</span><span class="sxs-lookup"><span data-stu-id="3e2bf-176">Verify that the script references here match the scripts in the Scripts folder of the project.</span></span>

    [!code-html[Main](tutorial-signalr-self-host/samples/sample5.html?highlight=31-32)]

    <span data-ttu-id="3e2bf-177">下面的代码（上面的代码示例中突出显示的代码）是你在获取入门教程中所使用的客户端的补充（除了将代码升级到 SignalR 版本 2 beta 版本之外）。</span><span class="sxs-lookup"><span data-stu-id="3e2bf-177">The following code (highlighted in the code sample above) is the addition that you've made to the client used in the Getting Stared tutorial (in addition to upgrading the code to SignalR version 2 beta).</span></span> <span data-ttu-id="3e2bf-178">此代码行显式设置服务器上的 SignalR 的基连接 URL。</span><span class="sxs-lookup"><span data-stu-id="3e2bf-178">This line of code explicitly sets the base connection URL for SignalR on the server.</span></span>

    [!code-javascript[Main](tutorial-signalr-self-host/samples/sample6.js)]
6. <span data-ttu-id="3e2bf-179">右键单击该解决方案，然后选择 "**设置启动项目 ...**"。选择 "**多启动项目**" 单选按钮，并将两个项目的 "**操作**" 设置为 "**启动**"。</span><span class="sxs-lookup"><span data-stu-id="3e2bf-179">Right-click on the solution, and select **Set Startup Projects...**. Select the **Multiple startup projects** radio button, and set both projects' **Action** to **Start**.</span></span>

    ![](tutorial-signalr-self-host/_static/image6.png)
7. <span data-ttu-id="3e2bf-180">右键单击 "Default.html" 并选择 "**设为起始页**"。</span><span class="sxs-lookup"><span data-stu-id="3e2bf-180">Right-click on "Default.html" and select **Set As Start Page**.</span></span>
8. <span data-ttu-id="3e2bf-181">运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="3e2bf-181">Run the application.</span></span> <span data-ttu-id="3e2bf-182">服务器和页面将启动。</span><span class="sxs-lookup"><span data-stu-id="3e2bf-182">The server and page will launch.</span></span> <span data-ttu-id="3e2bf-183">如果在启动服务器之前加载页面，则可能需要重新加载网页（或选择 "在调试器中**继续**"）。</span><span class="sxs-lookup"><span data-stu-id="3e2bf-183">You may need to reload the web page (or select **Continue** in the debugger) if the page loads before the server is started.</span></span>
9. <span data-ttu-id="3e2bf-184">在浏览器中，在出现提示时提供用户名。</span><span class="sxs-lookup"><span data-stu-id="3e2bf-184">In the browser, provide a username when prompted.</span></span> <span data-ttu-id="3e2bf-185">将页面的 URL 复制到其他浏览器选项卡或窗口中，并提供不同的用户名。</span><span class="sxs-lookup"><span data-stu-id="3e2bf-185">Copy the page's URL into another browser tab or window and provide a different username.</span></span> <span data-ttu-id="3e2bf-186">你将能够将消息从一个浏览器窗格发送到另一个浏览器窗格，如入门教程中所示。</span><span class="sxs-lookup"><span data-stu-id="3e2bf-186">You will be able to send messages from one browser pane to the other, as in the Getting Started tutorial.</span></span>

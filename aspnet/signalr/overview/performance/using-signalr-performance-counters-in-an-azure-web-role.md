---
uid: signalr/overview/performance/using-signalr-performance-counters-in-an-azure-web-role
title: 在 Azure Web 角色中使用 SignalR 性能计数器 |Microsoft Docs
author: guardrex
description: 如何在 Azure Web 角色中安装和使用 SignalR 性能计数器。
keywords: .ASP、signalr、性能计数器、azure web 角色
ms.author: bradyg
ms.date: 10/03/2018
ms.assetid: 2a127d3b-21ed-4cc9-bec0-cdab4e742a25
msc.legacyurl: /signalr/overview/performance/using-signalr-performance-counters-in-an-azure-web-role
msc.type: authoredcontent
ms.openlocfilehash: 3de42435887113f93c6b8c36145793952af4d735
ms.sourcegitcommit: 0cf7d06071a8ff986e6c028ac9daf0c0e7490412
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/23/2020
ms.locfileid: "85240637"
---
# <a name="using-signalr-performance-counters-in-an-azure-web-role"></a><span data-ttu-id="24ea0-104">在 Azure Web 角色中使用 SignalR 性能计数器</span><span class="sxs-lookup"><span data-stu-id="24ea0-104">Using SignalR performance counters in an Azure Web Role</span></span>

<span data-ttu-id="24ea0-105">作者：[Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="24ea0-105">By [Luke Latham](https://github.com/guardrex)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

<span data-ttu-id="24ea0-106">SignalR 性能计数器用于监视 Azure Web 角色中的应用性能。</span><span class="sxs-lookup"><span data-stu-id="24ea0-106">SignalR performance counters are used to monitor your app's performance in an Azure Web Role.</span></span> <span data-ttu-id="24ea0-107">Microsoft Azure 诊断捕获计数器。</span><span class="sxs-lookup"><span data-stu-id="24ea0-107">The counters are captured by Microsoft Azure Diagnostics.</span></span> <span data-ttu-id="24ea0-108">使用*signalr.exe*在 Azure 上安装 SignalR 性能计数器，该工具用于独立应用或本地应用。</span><span class="sxs-lookup"><span data-stu-id="24ea0-108">You install SignalR performance counters on Azure with *signalr.exe*, the same tool used for standalone or on-premises apps.</span></span> <span data-ttu-id="24ea0-109">由于 Azure 角色是暂时性的，因此，你可以将应用配置为在启动时安装和注册 SignalR 性能计数器。</span><span class="sxs-lookup"><span data-stu-id="24ea0-109">Since Azure roles are transient, you configure an app to install and register SignalR performance counters upon startup.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="24ea0-110">先决条件</span><span class="sxs-lookup"><span data-stu-id="24ea0-110">Prerequisites</span></span>

* <span data-ttu-id="24ea0-111">Visual Studio 2015 或[2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)</span><span class="sxs-lookup"><span data-stu-id="24ea0-111">Visual Studio 2015 or [2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)</span></span>
* <span data-ttu-id="24ea0-112">[MICROSOFT AZURE sdk For Visual Studio](https://azure.microsoft.com/downloads/) **说明：安装 Sdk 后重新启动计算机。**</span><span class="sxs-lookup"><span data-stu-id="24ea0-112">[Microsoft Azure SDK for Visual Studio](https://azure.microsoft.com/downloads/) **Note: Restart your machine after installing the SDK.**</span></span>
* <span data-ttu-id="24ea0-113">Microsoft Azure 订阅：若要注册免费的 Azure 试用帐户，请参阅[Azure 免费试用](https://azure.microsoft.com/free/dotnet/)。</span><span class="sxs-lookup"><span data-stu-id="24ea0-113">Microsoft Azure subscription: To sign up for a free Azure trial account, see [Azure Free Trial](https://azure.microsoft.com/free/dotnet/).</span></span>

## <a name="creating-an-azure-web-role-application-that-exposes-signalr-performance-counters"></a><span data-ttu-id="24ea0-114">创建公开 SignalR 性能计数器的 Azure Web 角色应用程序</span><span class="sxs-lookup"><span data-stu-id="24ea0-114">Creating an Azure Web Role application that exposes SignalR performance counters</span></span>

1. <span data-ttu-id="24ea0-115">打开 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="24ea0-115">Open Visual Studio.</span></span>

2. <span data-ttu-id="24ea0-116">在 Visual Studio 中，选择“文件” > “新建” > “项目”。</span><span class="sxs-lookup"><span data-stu-id="24ea0-116">In Visual Studio, select **File** > **New** > **Project**.</span></span>

3. <span data-ttu-id="24ea0-117">在 "**新建项目**" 对话框中，选择左侧的 " **Visual c #**  >  **云**" 类别，然后选择 " **Azure 云服务**" 模板。</span><span class="sxs-lookup"><span data-stu-id="24ea0-117">In the **New Project** dialog box, select the **Visual C#** > **Cloud** category on the left, and then select the **Azure Cloud Service** template.</span></span> <span data-ttu-id="24ea0-118">将应用命名为**SignalRPerfCounters** ，然后选择 **"确定"**。</span><span class="sxs-lookup"><span data-stu-id="24ea0-118">Name the app **SignalRPerfCounters** and select **OK**.</span></span>

   ![新的云应用程序](using-signalr-performance-counters-in-an-azure-web-role/_static/image1.png)

   > [!NOTE]
   > <span data-ttu-id="24ea0-120">如果看不到**云**模板类别或**azure 云服务**模板，则需要安装适用于 Visual Studio 2017 的**Azure 开发**工作负荷。</span><span class="sxs-lookup"><span data-stu-id="24ea0-120">If you don't see the **Cloud** template category or the **Azure Cloud Service** template, you need to install the **Azure development** workload for Visual Studio 2017.</span></span> <span data-ttu-id="24ea0-121">选择 "**新建项目**" 对话框左下角的 "**打开 Visual Studio 安装程序**" 链接，打开 Visual Studio 安装程序。</span><span class="sxs-lookup"><span data-stu-id="24ea0-121">Choose the **Open Visual Studio Installer** link on the bottom-left side of the **New Project** dialog to open Visual Studio Installer.</span></span> <span data-ttu-id="24ea0-122">选择 " **Azure 开发**" 工作负载，然后选择 "**修改**" 开始安装工作负荷。</span><span class="sxs-lookup"><span data-stu-id="24ea0-122">Select the **Azure development** workload, and then choose **Modify** to start installing the workload.</span></span>
   >
   > ![Visual Studio 安装程序中的 Azure 开发工作负荷](using-signalr-performance-counters-in-an-azure-web-role/_static/azure-development-workload.png)

4. <span data-ttu-id="24ea0-124">在 "**新建 Microsoft Azure 云服务**" 对话框中，选择 " **ASP.NET Web 角色**"，然后选择 ">" 按钮，将角色添加到项目。</span><span class="sxs-lookup"><span data-stu-id="24ea0-124">In the **New Microsoft Azure Cloud Service** dialog, select **ASP.NET Web Role** and select the > button to add the role to the project.</span></span> <span data-ttu-id="24ea0-125">选择“确定”。</span><span class="sxs-lookup"><span data-stu-id="24ea0-125">Select **OK**.</span></span>

   ![添加 ASP.NET Web 角色](using-signalr-performance-counters-in-an-azure-web-role/_static/image2.png)

5. <span data-ttu-id="24ea0-127">在 "**新建 ASP.NET Web 应用程序-WebRole1** " 对话框中，选择 " **MVC** " 模板，然后选择 **"确定"**。</span><span class="sxs-lookup"><span data-stu-id="24ea0-127">In the **New ASP.NET Web Application - WebRole1** dialog, select the **MVC** template, and then select **OK**.</span></span>

   ![添加 MVC 和 Web API](using-signalr-performance-counters-in-an-azure-web-role/_static/image3.png)

6. <span data-ttu-id="24ea0-129">在**解决方案资源管理器**中，打开**WebRole1**下的*diagnostics.wadcfgx*文件。</span><span class="sxs-lookup"><span data-stu-id="24ea0-129">In **Solution Explorer**, open the *diagnostics.wadcfgx* file under **WebRole1**.</span></span>

   ![解决方案资源管理器 diagnostics.wadcfgx](using-signalr-performance-counters-in-an-azure-web-role/_static/image4.png)

7. <span data-ttu-id="24ea0-131">将该文件的内容替换为以下配置，并保存该文件：</span><span class="sxs-lookup"><span data-stu-id="24ea0-131">Replace the contents of the file with the following configuration and save the file:</span></span>

   [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample1.xml)]

8. <span data-ttu-id="24ea0-132">从 "**工具**" "NuGet 包管理器" 中打开**包管理器控制台**  >  **NuGet Package Manager**。</span><span class="sxs-lookup"><span data-stu-id="24ea0-132">Open the **Package Manager Console** from **Tools** > **NuGet Package Manager**.</span></span> <span data-ttu-id="24ea0-133">输入以下命令以安装最新版本的 SignalR 和 SignalR 实用工具包：</span><span class="sxs-lookup"><span data-stu-id="24ea0-133">Enter the following commands to install the latest version of SignalR and the SignalR utilities package:</span></span>

   [!code-powershell[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample2.ps1)]

9. <span data-ttu-id="24ea0-134">配置应用，以便在启动或回收角色实例时将 SignalR 性能计数器安装到该实例中。</span><span class="sxs-lookup"><span data-stu-id="24ea0-134">Configure the app to install the SignalR performance counters into the role instance when it starts up or recycles.</span></span> <span data-ttu-id="24ea0-135">在**解决方案资源管理器**中，右键单击**WebRole1**项目，然后选择 "**添加**  >  **新文件夹**"。</span><span class="sxs-lookup"><span data-stu-id="24ea0-135">In **Solution Explorer**, right-click on the **WebRole1** project and select **Add** > **New Folder**.</span></span> <span data-ttu-id="24ea0-136">将新文件夹命名为 "*启动*"。</span><span class="sxs-lookup"><span data-stu-id="24ea0-136">Name the new folder *Startup*.</span></span>

   ![添加启动文件夹](using-signalr-performance-counters-in-an-azure-web-role/_static/image5.png)

10. <span data-ttu-id="24ea0-138">从**Microsoft.AspNet.SignalR.Utils** /SignalRPerfCounters/packages/Microsoft.AspNet.SignalR.Utils. *signalr.exe* \<project folder> 复制 \<version>signalr.exe文件（通过 Utils 包添加）/tools 在上一步中创建的*启动*文件夹。</span><span class="sxs-lookup"><span data-stu-id="24ea0-138">Copy the *signalr.exe* file (added with the **Microsoft.AspNet.SignalR.Utils** package) from \<project folder>/SignalRPerfCounters/packages/Microsoft.AspNet.SignalR.Utils.\<version>/tools to the *Startup* folder you created in the previous step.</span></span>

11. <span data-ttu-id="24ea0-139">在**解决方案资源管理器**中，右键单击 "*启动*" 文件夹，然后选择 "**添加**  >  **现有项**"。</span><span class="sxs-lookup"><span data-stu-id="24ea0-139">In **Solution Explorer**, right-click the *Startup* folder and select **Add** > **Existing Item**.</span></span> <span data-ttu-id="24ea0-140">在出现的对话框中，选择 " *signalr.exe* "，然后选择 "**添加**"。</span><span class="sxs-lookup"><span data-stu-id="24ea0-140">In the dialog that appears, select *signalr.exe* and select **Add**.</span></span>

    ![将 signalr.exe 添加到项目](using-signalr-performance-counters-in-an-azure-web-role/_static/image6.png)

12. <span data-ttu-id="24ea0-142">右键单击您创建的*启动*文件夹。</span><span class="sxs-lookup"><span data-stu-id="24ea0-142">Right-click on the *Startup* folder you created.</span></span> <span data-ttu-id="24ea0-143">选择 "**添加**  >  **新项**"。</span><span class="sxs-lookup"><span data-stu-id="24ea0-143">Select **Add** > **New Item**.</span></span> <span data-ttu-id="24ea0-144">选择 "**常规**" 节点，选择 "**文本文件**"，并将新项目命名为 " *SignalRPerfCounterInstall*"。</span><span class="sxs-lookup"><span data-stu-id="24ea0-144">Select the **General** node, select **Text File**, and name the new item *SignalRPerfCounterInstall.cmd*.</span></span> <span data-ttu-id="24ea0-145">此命令文件将 SignalR 性能计数器安装到 web 角色中。</span><span class="sxs-lookup"><span data-stu-id="24ea0-145">This command file will install the SignalR performance counters into the web role.</span></span>

    ![Create SignalR 性能计数器安装批处理文件](using-signalr-performance-counters-in-an-azure-web-role/_static/image7.png)

13. <span data-ttu-id="24ea0-147">当 Visual Studio 创建*SignalRPerfCounterInstall*文件时，它将在主窗口中自动打开。</span><span class="sxs-lookup"><span data-stu-id="24ea0-147">When Visual Studio creates the *SignalRPerfCounterInstall.cmd* file, it will automatically open in the main window.</span></span> <span data-ttu-id="24ea0-148">将该文件的内容替换为下面的脚本，然后保存并关闭该文件。</span><span class="sxs-lookup"><span data-stu-id="24ea0-148">Replace the contents of the file with the following script, then save and close the file.</span></span> <span data-ttu-id="24ea0-149">此脚本执行*signalr.exe*，这会将 SignalR 性能计数器添加到角色实例。</span><span class="sxs-lookup"><span data-stu-id="24ea0-149">This script executes *signalr.exe*, which adds the SignalR performance counters to the role instance.</span></span>

    [!code-console[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample3.cmd)]

14. <span data-ttu-id="24ea0-150">选择**解决方案资源管理器**中的*signalr.exe*文件。</span><span class="sxs-lookup"><span data-stu-id="24ea0-150">Select the *signalr.exe* file in **Solution Explorer**.</span></span> <span data-ttu-id="24ea0-151">在文件的**属性**中，将 "**复制到输出目录**" 设置为 "**始终复制**"。</span><span class="sxs-lookup"><span data-stu-id="24ea0-151">In the file's **Properties**, set **Copy to Output Directory** to **Copy Always**.</span></span>

    ![将 "复制到输出目录" 设置为 "始终复制"](using-signalr-performance-counters-in-an-azure-web-role/_static/image8.png)

15. <span data-ttu-id="24ea0-153">对于*SignalRPerfCounterInstall*文件，请重复上一步。</span><span class="sxs-lookup"><span data-stu-id="24ea0-153">Repeat the previous step for the *SignalRPerfCounterInstall.cmd* file.</span></span>

16. <span data-ttu-id="24ea0-154">右键单击 " *SignalRPerfCounterInstall* " 文件，然后选择 "**打开方式**"。</span><span class="sxs-lookup"><span data-stu-id="24ea0-154">Right-click on the *SignalRPerfCounterInstall.cmd* file and select **Open With**.</span></span> <span data-ttu-id="24ea0-155">在出现的对话框中，选择 "**二进制编辑器**"，然后选择 **"确定"**。</span><span class="sxs-lookup"><span data-stu-id="24ea0-155">In the dialog that appears, select **Binary Editor** and select **OK**.</span></span>

    ![用二进制编辑器打开](using-signalr-performance-counters-in-an-azure-web-role/_static/image9.png)

17. <span data-ttu-id="24ea0-157">在二进制编辑器中，选择文件中的所有前导字节，并将其删除。</span><span class="sxs-lookup"><span data-stu-id="24ea0-157">In the binary editor, select any leading bytes in the file and delete them.</span></span> <span data-ttu-id="24ea0-158">保存并关闭该文件。</span><span class="sxs-lookup"><span data-stu-id="24ea0-158">Save and close the file.</span></span>

    ![删除前导字节](using-signalr-performance-counters-in-an-azure-web-role/_static/image10.png)

18. <span data-ttu-id="24ea0-160">打开*servicedefinition.csdef* ，并在服务启动时添加执行*SignalrPerfCounterInstall*文件的启动任务：</span><span class="sxs-lookup"><span data-stu-id="24ea0-160">Open *ServiceDefinition.csdef* and add a startup task that executes the *SignalrPerfCounterInstall.cmd* file when the service starts up:</span></span>

    [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample4.xml?highlight=4-7)]

19. <span data-ttu-id="24ea0-161">打开 `Views/Shared/_Layout.cshtml` 并删除文件末尾的 jQuery 捆绑脚本。</span><span class="sxs-lookup"><span data-stu-id="24ea0-161">Open `Views/Shared/_Layout.cshtml` and remove the jQuery bundle script from the end of the file.</span></span>

    [!code-cshtml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample5.cshtml)]

20. <span data-ttu-id="24ea0-162">添加在服务器上持续调用方法的 JavaScript 客户端 `increment` 。</span><span class="sxs-lookup"><span data-stu-id="24ea0-162">Add a JavaScript client that continuously calls the `increment` method on the server.</span></span> <span data-ttu-id="24ea0-163">打开 `Views/Home/Index.cshtml` 并将内容替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="24ea0-163">Open `Views/Home/Index.cshtml` and replace the contents with the following code:</span></span>

    [!code-cshtml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample6.cshtml)]

21. <span data-ttu-id="24ea0-164">在名为*hub*的**WebRole1**项目中创建一个新文件夹。</span><span class="sxs-lookup"><span data-stu-id="24ea0-164">Create a new folder in the **WebRole1** project named *Hubs*.</span></span> <span data-ttu-id="24ea0-165">右键单击**解决方案资源管理器**中的 "*中心*" 文件夹，然后选择 "**添加**  >  **新项**"。</span><span class="sxs-lookup"><span data-stu-id="24ea0-165">Right-click the *Hubs* folder in **Solution Explorer** and select **Add** > **New Item**.</span></span> <span data-ttu-id="24ea0-166">在 "**添加新项**" 对话框中，选择 " **Web**  >  **SignalR** " 类别，然后选择 " **SignalR" 集线器类（v2）** 项模板。</span><span class="sxs-lookup"><span data-stu-id="24ea0-166">In the **Add New Item** dialog box, select the **Web** > **SignalR** category, and then select the **SignalR Hub Class (v2)** item template.</span></span> <span data-ttu-id="24ea0-167">将新的中心命名为*MyHub.cs* ，然后选择 "**添加**"。</span><span class="sxs-lookup"><span data-stu-id="24ea0-167">Name the new hub *MyHub.cs* and select **Add**.</span></span>

    ![将 SignalR Hub 类添加到 "添加新项" 对话框中的 "中心" 文件夹](using-signalr-performance-counters-in-an-azure-web-role/_static/image13.png)

22. <span data-ttu-id="24ea0-169">*MyHub.cs*将在主窗口中自动打开。</span><span class="sxs-lookup"><span data-stu-id="24ea0-169">*MyHub.cs* will automatically open in the main window.</span></span> <span data-ttu-id="24ea0-170">将内容替换为以下代码，然后保存并关闭该文件：</span><span class="sxs-lookup"><span data-stu-id="24ea0-170">Replace the contents with the following code, then save and close the file:</span></span>

    [!code-csharp[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample7.cs)]

23. <span data-ttu-id="24ea0-171">*[Crank.exe](signalr-connection-density-testing-with-crank.md)* 是随 SignalR 基本代码提供的连接密度测试工具。</span><span class="sxs-lookup"><span data-stu-id="24ea0-171">*[Crank.exe](signalr-connection-density-testing-with-crank.md)* is a connection density testing tool provided with the SignalR codebase.</span></span> <span data-ttu-id="24ea0-172">由于曲柄需要持久性连接，因此你可以将其添加到你的站点，以便在测试时使用。</span><span class="sxs-lookup"><span data-stu-id="24ea0-172">Since Crank requires a persistent connection, you add one to your site for use when testing.</span></span> <span data-ttu-id="24ea0-173">将一个新文件夹添加到名为*PersistentConnections*的**WebRole1**项目。</span><span class="sxs-lookup"><span data-stu-id="24ea0-173">Add a new folder to the **WebRole1** project called *PersistentConnections*.</span></span> <span data-ttu-id="24ea0-174">右键单击此文件夹，然后选择 "**添加**  >  **类**"。</span><span class="sxs-lookup"><span data-stu-id="24ea0-174">Right-click this folder and select **Add** > **Class**.</span></span> <span data-ttu-id="24ea0-175">将新的类文件命名为*MyPersistentConnections.cs* ，然后选择 "**添加**"。</span><span class="sxs-lookup"><span data-stu-id="24ea0-175">Name the new class file *MyPersistentConnections.cs* and select **Add**.</span></span>

24. <span data-ttu-id="24ea0-176">Visual Studio 将在主窗口中打开*MyPersistentConnections.cs*文件。</span><span class="sxs-lookup"><span data-stu-id="24ea0-176">Visual Studio will open the *MyPersistentConnections.cs* file in the main window.</span></span> <span data-ttu-id="24ea0-177">将内容替换为以下代码，然后保存并关闭该文件：</span><span class="sxs-lookup"><span data-stu-id="24ea0-177">Replace the contents with the following code, then save and close the file:</span></span>

    [!code-csharp[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample8.cs)]

25. <span data-ttu-id="24ea0-178">使用 `Startup` 类，SignalR 对象在 OWIN 启动时启动。</span><span class="sxs-lookup"><span data-stu-id="24ea0-178">Using the `Startup` class, the SignalR objects start when OWIN starts up.</span></span> <span data-ttu-id="24ea0-179">打开或创建*Startup.cs* ，并将内容替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="24ea0-179">Open or create *Startup.cs* and replace the contents with the following code:</span></span>

    [!code-csharp[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample9.cs)]

    <span data-ttu-id="24ea0-180">在上面的代码中， `OwinStartup` 属性标记此类以启动 OWIN。</span><span class="sxs-lookup"><span data-stu-id="24ea0-180">In the code above, the `OwinStartup` attribute marks this class to start OWIN.</span></span> <span data-ttu-id="24ea0-181">`Configuration`方法启动 SignalR。</span><span class="sxs-lookup"><span data-stu-id="24ea0-181">The `Configuration` method starts SignalR.</span></span>

26. <span data-ttu-id="24ea0-182">按**F5**在 Microsoft Azure 模拟器中测试应用程序。</span><span class="sxs-lookup"><span data-stu-id="24ea0-182">Test your application in the Microsoft Azure Emulator by pressing **F5**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="24ea0-183">如果在**MapSignalR**上遇到**FileLoadException** ，请将*web.config*中的绑定重定向更改为以下内容：</span><span class="sxs-lookup"><span data-stu-id="24ea0-183">If you encounter a **FileLoadException** at **MapSignalR**, change the binding redirects in *web.config* to the following:</span></span>

    [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample12.xml?highlight=3,7)]

27. <span data-ttu-id="24ea0-184">等待大约一分钟。</span><span class="sxs-lookup"><span data-stu-id="24ea0-184">Wait about one minute.</span></span> <span data-ttu-id="24ea0-185">在 Visual Studio 中打开 "Cloud Explorer 工具" 窗口（"**查看**  >  **Cloud Explorer**"）并展开该路径 `(Local)/Storage Accounts/(Development)/Tables` 。</span><span class="sxs-lookup"><span data-stu-id="24ea0-185">Open the Cloud Explorer tool window in Visual Studio (**View** > **Cloud Explorer**) and expand the path `(Local)/Storage Accounts/(Development)/Tables`.</span></span> <span data-ttu-id="24ea0-186">双击 " **WADPerformanceCountersTable**"。</span><span class="sxs-lookup"><span data-stu-id="24ea0-186">Double-click **WADPerformanceCountersTable**.</span></span> <span data-ttu-id="24ea0-187">你应在表数据中看到 SignalR 计数器。</span><span class="sxs-lookup"><span data-stu-id="24ea0-187">You should see SignalR counters in the table data.</span></span> <span data-ttu-id="24ea0-188">如果看不到此表，可能需要重新输入 Azure 存储凭据。</span><span class="sxs-lookup"><span data-stu-id="24ea0-188">If you don't see the table, you may need to re-enter your Azure Storage credentials.</span></span> <span data-ttu-id="24ea0-189">您可能需要选择 "**刷新**" 按钮以查看**Cloud Explorer**中的表，或在 "打开表" 窗口中选择 "**刷新**" 按钮以查看表中的数据。</span><span class="sxs-lookup"><span data-stu-id="24ea0-189">You may need to select the **Refresh** button to see the table in **Cloud Explorer** or select the **Refresh** button in the open table window to see data in the table.</span></span>

    ![在 Visual Studio 中选择 "WAD 性能计数器" 表 Cloud Explorer](using-signalr-performance-counters-in-an-azure-web-role/_static/image11.png)

    ![显示 WAD 性能计数器表中收集的计数器](using-signalr-performance-counters-in-an-azure-web-role/_static/image12.png)

28. <span data-ttu-id="24ea0-192">若要在云中测试应用程序，请更新**serviceconfiguration.cscfg**文件，并将设置 `Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString` 为有效的 Azure 存储帐户连接字符串。</span><span class="sxs-lookup"><span data-stu-id="24ea0-192">To test your application in the cloud, update the **ServiceConfiguration.Cloud.cscfg** file and set the `Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString` to a valid Azure Storage account connection string.</span></span>

    [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample10.xml)]

29. <span data-ttu-id="24ea0-193">将应用程序部署到你的 Azure 订阅。</span><span class="sxs-lookup"><span data-stu-id="24ea0-193">Deploy the application to your Azure subscription.</span></span> <span data-ttu-id="24ea0-194">有关如何将应用程序部署到 Azure 的详细信息，请参阅[如何创建和部署云服务](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy)。</span><span class="sxs-lookup"><span data-stu-id="24ea0-194">For details on how to deploy an application to Azure, see [How to Create and Deploy a Cloud Service](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy).</span></span>

30. <span data-ttu-id="24ea0-195">稍等几分钟。</span><span class="sxs-lookup"><span data-stu-id="24ea0-195">Wait a few minutes.</span></span> <span data-ttu-id="24ea0-196">在**Cloud Explorer**中，找到前面配置的存储帐户，并 `WADPerformanceCountersTable` 在其中找到该表。</span><span class="sxs-lookup"><span data-stu-id="24ea0-196">In **Cloud Explorer**, locate the storage account you configured above and find the `WADPerformanceCountersTable` table in it.</span></span> <span data-ttu-id="24ea0-197">你应在表数据中看到 SignalR 计数器。</span><span class="sxs-lookup"><span data-stu-id="24ea0-197">You should see SignalR counters in the table data.</span></span> <span data-ttu-id="24ea0-198">如果看不到此表，可能需要重新输入 Azure 存储凭据。</span><span class="sxs-lookup"><span data-stu-id="24ea0-198">If you don't see the table, you may need to re-enter your Azure Storage credentials.</span></span> <span data-ttu-id="24ea0-199">您可能需要选择 "**刷新**" 按钮以查看**Cloud Explorer**中的表，或在 "打开表" 窗口中选择 "**刷新**" 按钮以查看表中的数据。</span><span class="sxs-lookup"><span data-stu-id="24ea0-199">You may need to select the **Refresh** button to see the table in **Cloud Explorer** or select the **Refresh** button in the open table window to see data in the table.</span></span>

<span data-ttu-id="24ea0-200">特别感谢在本教程中使用的原始内容的[Richard](https://social.msdn.microsoft.com/profile/Martin+Richard) 。</span><span class="sxs-lookup"><span data-stu-id="24ea0-200">Special thanks to [Martin Richard](https://social.msdn.microsoft.com/profile/Martin+Richard) for the original content used in this tutorial.</span></span>

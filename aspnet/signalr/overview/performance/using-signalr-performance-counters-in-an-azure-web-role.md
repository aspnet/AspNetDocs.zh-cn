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
# <a name="using-signalr-performance-counters-in-an-azure-web-role"></a>在 Azure Web 角色中使用 SignalR 性能计数器

作者：[Luke Latham](https://github.com/guardrex)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

SignalR 性能计数器用于监视 Azure Web 角色中的应用性能。 Microsoft Azure 诊断捕获计数器。 使用*signalr.exe*在 Azure 上安装 SignalR 性能计数器，该工具用于独立应用或本地应用。 由于 Azure 角色是暂时性的，因此，你可以将应用配置为在启动时安装和注册 SignalR 性能计数器。

## <a name="prerequisites"></a>先决条件

* Visual Studio 2015 或[2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
* [MICROSOFT AZURE sdk For Visual Studio](https://azure.microsoft.com/downloads/) **说明：安装 Sdk 后重新启动计算机。**
* Microsoft Azure 订阅：若要注册免费的 Azure 试用帐户，请参阅[Azure 免费试用](https://azure.microsoft.com/free/dotnet/)。

## <a name="creating-an-azure-web-role-application-that-exposes-signalr-performance-counters"></a>创建公开 SignalR 性能计数器的 Azure Web 角色应用程序

1. 打开 Visual Studio。

2. 在 Visual Studio 中，选择“文件” > “新建” > “项目”。

3. 在 "**新建项目**" 对话框中，选择左侧的 " **Visual c #**  >  **云**" 类别，然后选择 " **Azure 云服务**" 模板。 将应用命名为**SignalRPerfCounters** ，然后选择 **"确定"**。

   ![新的云应用程序](using-signalr-performance-counters-in-an-azure-web-role/_static/image1.png)

   > [!NOTE]
   > 如果看不到**云**模板类别或**azure 云服务**模板，则需要安装适用于 Visual Studio 2017 的**Azure 开发**工作负荷。 选择 "**新建项目**" 对话框左下角的 "**打开 Visual Studio 安装程序**" 链接，打开 Visual Studio 安装程序。 选择 " **Azure 开发**" 工作负载，然后选择 "**修改**" 开始安装工作负荷。
   >
   > ![Visual Studio 安装程序中的 Azure 开发工作负荷](using-signalr-performance-counters-in-an-azure-web-role/_static/azure-development-workload.png)

4. 在 "**新建 Microsoft Azure 云服务**" 对话框中，选择 " **ASP.NET Web 角色**"，然后选择 ">" 按钮，将角色添加到项目。 选择“确定”。

   ![添加 ASP.NET Web 角色](using-signalr-performance-counters-in-an-azure-web-role/_static/image2.png)

5. 在 "**新建 ASP.NET Web 应用程序-WebRole1** " 对话框中，选择 " **MVC** " 模板，然后选择 **"确定"**。

   ![添加 MVC 和 Web API](using-signalr-performance-counters-in-an-azure-web-role/_static/image3.png)

6. 在**解决方案资源管理器**中，打开**WebRole1**下的*diagnostics.wadcfgx*文件。

   ![解决方案资源管理器 diagnostics.wadcfgx](using-signalr-performance-counters-in-an-azure-web-role/_static/image4.png)

7. 将该文件的内容替换为以下配置，并保存该文件：

   [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample1.xml)]

8. 从 "**工具**" "NuGet 包管理器" 中打开**包管理器控制台**  >  **NuGet Package Manager**。 输入以下命令以安装最新版本的 SignalR 和 SignalR 实用工具包：

   [!code-powershell[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample2.ps1)]

9. 配置应用，以便在启动或回收角色实例时将 SignalR 性能计数器安装到该实例中。 在**解决方案资源管理器**中，右键单击**WebRole1**项目，然后选择 "**添加**  >  **新文件夹**"。 将新文件夹命名为 "*启动*"。

   ![添加启动文件夹](using-signalr-performance-counters-in-an-azure-web-role/_static/image5.png)

10. 从**Microsoft.AspNet.SignalR.Utils** /SignalRPerfCounters/packages/Microsoft.AspNet.SignalR.Utils. *signalr.exe* \<project folder> 复制 \<version>signalr.exe文件（通过 Utils 包添加）/tools 在上一步中创建的*启动*文件夹。

11. 在**解决方案资源管理器**中，右键单击 "*启动*" 文件夹，然后选择 "**添加**  >  **现有项**"。 在出现的对话框中，选择 " *signalr.exe* "，然后选择 "**添加**"。

    ![将 signalr.exe 添加到项目](using-signalr-performance-counters-in-an-azure-web-role/_static/image6.png)

12. 右键单击您创建的*启动*文件夹。 选择 "**添加**  >  **新项**"。 选择 "**常规**" 节点，选择 "**文本文件**"，并将新项目命名为 " *SignalRPerfCounterInstall*"。 此命令文件将 SignalR 性能计数器安装到 web 角色中。

    ![Create SignalR 性能计数器安装批处理文件](using-signalr-performance-counters-in-an-azure-web-role/_static/image7.png)

13. 当 Visual Studio 创建*SignalRPerfCounterInstall*文件时，它将在主窗口中自动打开。 将该文件的内容替换为下面的脚本，然后保存并关闭该文件。 此脚本执行*signalr.exe*，这会将 SignalR 性能计数器添加到角色实例。

    [!code-console[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample3.cmd)]

14. 选择**解决方案资源管理器**中的*signalr.exe*文件。 在文件的**属性**中，将 "**复制到输出目录**" 设置为 "**始终复制**"。

    ![将 "复制到输出目录" 设置为 "始终复制"](using-signalr-performance-counters-in-an-azure-web-role/_static/image8.png)

15. 对于*SignalRPerfCounterInstall*文件，请重复上一步。

16. 右键单击 " *SignalRPerfCounterInstall* " 文件，然后选择 "**打开方式**"。 在出现的对话框中，选择 "**二进制编辑器**"，然后选择 **"确定"**。

    ![用二进制编辑器打开](using-signalr-performance-counters-in-an-azure-web-role/_static/image9.png)

17. 在二进制编辑器中，选择文件中的所有前导字节，并将其删除。 保存并关闭该文件。

    ![删除前导字节](using-signalr-performance-counters-in-an-azure-web-role/_static/image10.png)

18. 打开*servicedefinition.csdef* ，并在服务启动时添加执行*SignalrPerfCounterInstall*文件的启动任务：

    [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample4.xml?highlight=4-7)]

19. 打开 `Views/Shared/_Layout.cshtml` 并删除文件末尾的 jQuery 捆绑脚本。

    [!code-cshtml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample5.cshtml)]

20. 添加在服务器上持续调用方法的 JavaScript 客户端 `increment` 。 打开 `Views/Home/Index.cshtml` 并将内容替换为以下代码：

    [!code-cshtml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample6.cshtml)]

21. 在名为*hub*的**WebRole1**项目中创建一个新文件夹。 右键单击**解决方案资源管理器**中的 "*中心*" 文件夹，然后选择 "**添加**  >  **新项**"。 在 "**添加新项**" 对话框中，选择 " **Web**  >  **SignalR** " 类别，然后选择 " **SignalR" 集线器类（v2）** 项模板。 将新的中心命名为*MyHub.cs* ，然后选择 "**添加**"。

    ![将 SignalR Hub 类添加到 "添加新项" 对话框中的 "中心" 文件夹](using-signalr-performance-counters-in-an-azure-web-role/_static/image13.png)

22. *MyHub.cs*将在主窗口中自动打开。 将内容替换为以下代码，然后保存并关闭该文件：

    [!code-csharp[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample7.cs)]

23. *[Crank.exe](signalr-connection-density-testing-with-crank.md)* 是随 SignalR 基本代码提供的连接密度测试工具。 由于曲柄需要持久性连接，因此你可以将其添加到你的站点，以便在测试时使用。 将一个新文件夹添加到名为*PersistentConnections*的**WebRole1**项目。 右键单击此文件夹，然后选择 "**添加**  >  **类**"。 将新的类文件命名为*MyPersistentConnections.cs* ，然后选择 "**添加**"。

24. Visual Studio 将在主窗口中打开*MyPersistentConnections.cs*文件。 将内容替换为以下代码，然后保存并关闭该文件：

    [!code-csharp[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample8.cs)]

25. 使用 `Startup` 类，SignalR 对象在 OWIN 启动时启动。 打开或创建*Startup.cs* ，并将内容替换为以下代码：

    [!code-csharp[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample9.cs)]

    在上面的代码中， `OwinStartup` 属性标记此类以启动 OWIN。 `Configuration`方法启动 SignalR。

26. 按**F5**在 Microsoft Azure 模拟器中测试应用程序。

    > [!NOTE]
    > 如果在**MapSignalR**上遇到**FileLoadException** ，请将*web.config*中的绑定重定向更改为以下内容：

    [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample12.xml?highlight=3,7)]

27. 等待大约一分钟。 在 Visual Studio 中打开 "Cloud Explorer 工具" 窗口（"**查看**  >  **Cloud Explorer**"）并展开该路径 `(Local)/Storage Accounts/(Development)/Tables` 。 双击 " **WADPerformanceCountersTable**"。 你应在表数据中看到 SignalR 计数器。 如果看不到此表，可能需要重新输入 Azure 存储凭据。 您可能需要选择 "**刷新**" 按钮以查看**Cloud Explorer**中的表，或在 "打开表" 窗口中选择 "**刷新**" 按钮以查看表中的数据。

    ![在 Visual Studio 中选择 "WAD 性能计数器" 表 Cloud Explorer](using-signalr-performance-counters-in-an-azure-web-role/_static/image11.png)

    ![显示 WAD 性能计数器表中收集的计数器](using-signalr-performance-counters-in-an-azure-web-role/_static/image12.png)

28. 若要在云中测试应用程序，请更新**serviceconfiguration.cscfg**文件，并将设置 `Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString` 为有效的 Azure 存储帐户连接字符串。

    [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample10.xml)]

29. 将应用程序部署到你的 Azure 订阅。 有关如何将应用程序部署到 Azure 的详细信息，请参阅[如何创建和部署云服务](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy)。

30. 稍等几分钟。 在**Cloud Explorer**中，找到前面配置的存储帐户，并 `WADPerformanceCountersTable` 在其中找到该表。 你应在表数据中看到 SignalR 计数器。 如果看不到此表，可能需要重新输入 Azure 存储凭据。 您可能需要选择 "**刷新**" 按钮以查看**Cloud Explorer**中的表，或在 "打开表" 窗口中选择 "**刷新**" 按钮以查看表中的数据。

特别感谢在本教程中使用的原始内容的[Richard](https://social.msdn.microsoft.com/profile/Martin+Richard) 。

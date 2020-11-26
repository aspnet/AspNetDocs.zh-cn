---
uid: aspnet/overview/owin-and-katana/host-owin-in-an-azure-worker-role
title: 在 Azure 辅助角色中托管 OWIN |Microsoft Docs
author: MikeWasson
description: 本教程介绍如何在 Microsoft Azure 辅助角色中自行托管 OWIN。 开放式 Web Interface for .NET (OWIN) 定义 .NET Web 服务器之间的抽象 .。。
ms.author: riande
ms.date: 04/11/2014
ms.assetid: 07aa855a-92ee-4d43-ba66-5bfd7de20ee6
msc.legacyurl: /aspnet/overview/owin-and-katana/host-owin-in-an-azure-worker-role
msc.type: authoredcontent
ms.openlocfilehash: f4faeda4cc8428c54b761f30833f9a31edfd2ddb
ms.sourcegitcommit: 4b78855427f1397df0a7be3559e04ec94a78c308
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/25/2020
ms.locfileid: "96151888"
---
# <a name="host-owin-in-an-azure-worker-role"></a>在 Azure 辅助角色中承载 OWIN

作者： [Mike Wasson](https://github.com/MikeWasson)

> 本教程介绍如何在 Microsoft Azure 辅助角色中自行托管 OWIN。
>
> [开放式 Web Interface for .net](http://owin.org/) (OWIN) 定义 .net Web 服务器和 Web 应用程序之间的抽象。 OWIN 将 web 应用程序与服务器分离，这使得 OWIN 非常适合用于在你自己的进程（例如，在 Azure 辅助角色中）自承载 web 应用程序。
>
> 在本教程中，你将了解如何在 Microsoft Azure 辅助角色内自行托管 OWIN 的应用程序。 若要了解有关辅助角色的详细信息，请参阅 [Azure 执行模型](https://azure.microsoft.com/documentation/articles/fundamentals-application-models/#CloudServices)。
>
> ## <a name="software-versions-used-in-the-tutorial"></a>本教程中使用的软件版本
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - [用于 .NET 2.3 的 Azure SDK](https://azure.microsoft.com/downloads/)
> - [Owin. Selfhost 2.1。0](http://www.nuget.org/packages/Microsoft.Owin.SelfHost/2.1.0)

## <a name="create-a-microsoft-azure-project"></a>创建 Microsoft Azure 项目

以管理员权限启动 Visual Studio。 需要管理员权限才能使用 Azure 计算仿真程序在本地调试应用程序。

在 " **文件** " 菜单上，单击 " **新建**"，然后单击 " **项目**"。 从 "**已安装的模板**" 的 "Visual c #" 下，单击 "**云**"，然后单击 " **microsoft Azure 云服务** 将项目命名为 "AzureApp"，然后单击 **"确定**"。

[![](host-owin-in-an-azure-worker-role/_static/image2.png)](host-owin-in-an-azure-worker-role/_static/image1.png)

在 " **新建 Microsoft Azure 云服务** " 对话框中，双击 " **辅助角色**"。 保留默认名称 ( "WorkerRole1" ) 。 此步骤将辅助角色添加到解决方案。 单击" **确定**"。

[![](host-owin-in-an-azure-worker-role/_static/image4.png)](host-owin-in-an-azure-worker-role/_static/image3.png)

创建的 Visual Studio 解决方案包含两个项目：

- &quot;AzureApp &quot; 定义 Azure 应用程序的角色和配置。
- &quot;WorkerRole1 &quot; 包含辅助角色的代码。

通常，Azure 应用程序可以包含多个角色，但本教程使用单个角色。

![](host-owin-in-an-azure-worker-role/_static/image5.png)

## <a name="add-the-owin-self-host-packages"></a>添加 OWIN Self-Host 包

从 " **工具** " 菜单中，单击 " **NuGet 包管理器**"，然后单击 " **程序包管理器控制台**"。

在“Package Manager Console”窗口中，输入以下命令：

[!code-console[Main](host-owin-in-an-azure-worker-role/samples/sample1.cmd)]

## <a name="add-an-http-endpoint"></a>添加 HTTP 终结点

在解决方案资源管理器中，展开 AzureApp 项目。 展开 "角色" 节点，右键单击 WorkerRole1，然后选择 " **属性**"。

![](host-owin-in-an-azure-worker-role/_static/image6.png)

单击“终结点”，然后单击“添加终结点”。

在 " **协议** " 下拉列表中，选择 "http"。 在 " **公用端口** " 和 " **专用端口**" 中，键入80。 这些端口号可以不同。 公用端口是客户端向角色发送请求时使用的端口。

[![](host-owin-in-an-azure-worker-role/_static/image8.png)](host-owin-in-an-azure-worker-role/_static/image7.png)

## <a name="create-the-owin-startup-class"></a>创建 OWIN Startup 类

在解决方案资源管理器中，右键单击 WorkerRole1 项目，然后选择 "**添加**  /  **类**" 添加新类。 命名类 `Startup`。

将所有样本代码替换为以下代码：

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample2.cs)]

`UseWelcomePage`扩展方法可向应用程序添加一个简单的 HTML 页，以验证该站点是否正常工作。

## <a name="start-the-owin-host"></a>启动 OWIN 主机

打开 WorkerRole.cs 文件。 此类定义在启动和停止辅助角色时运行的代码。

添加以下 using 语句：

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample3.cs)]

将 **IDisposable** 成员添加到 `WorkerRole` 类：

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample4.cs)]

在 `OnStart` 方法中，添加以下代码以启动主机：

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample5.cs?highlight=5)]

**WebApp** 方法启动 OWIN 主机。 类的名称 `Startup` 是方法的类型参数。 按照约定，主机将调用 `Configure` 此类的方法。

重写 `OnStop` 以释放 *\_ 应用程序* 实例：

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample6.cs)]

下面是 WorkerRole.cs 的完整代码：

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample7.cs)]

生成解决方案，然后按 F5 在 Azure 计算模拟器中本地运行应用程序。 根据防火墙设置，你可能需要通过防火墙允许模拟器。

计算模拟器将本地 IP 地址分配到终结点。 可以通过查看计算模拟器 UI 来查找 IP 地址。 右键单击任务栏通知区域中的模拟器图标，然后选择 " **显示计算模拟器 UI**"。

[![](host-owin-in-an-azure-worker-role/_static/image10.png)](host-owin-in-an-azure-worker-role/_static/image9.png)

查找服务部署、部署 [id] 和服务详细信息下的 IP 地址。 打开 web 浏览器并导航到 http： \/ \/ *address*，其中 *address* 是计算模拟器分配的 IP 地址; 例如， `http://127.0.0.1:80` 。 应会看到 "OWIN 欢迎" 页：

![](host-owin-in-an-azure-worker-role/_static/image11.png)

## <a name="deploy-to-azure"></a>部署到 Azure

对于此步骤，你必须有一个 Azure 帐户。 如果还没有，只需花费几分钟就能创建一个免费试用帐户。 有关详细信息，请参阅 [Microsoft Azure 免费试用版](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)。

在解决方案资源管理器中，右键单击 AzureApp 项目。 选择“发布”。

![](host-owin-in-an-azure-worker-role/_static/image12.png)

如果尚未登录到 Azure 帐户，请单击 " **登录**"。

[![](host-owin-in-an-azure-worker-role/_static/image14.png)](host-owin-in-an-azure-worker-role/_static/image13.png)

登录后，选择一个订阅，然后单击 " **下一步**"。

[![](host-owin-in-an-azure-worker-role/_static/image16.png)](host-owin-in-an-azure-worker-role/_static/image15.png)

输入云服务的名称，并选择区域。 单击“创建”。

![](host-owin-in-an-azure-worker-role/_static/image17.png)

单击“发布”。 

[![](host-owin-in-an-azure-worker-role/_static/image19.png)](host-owin-in-an-azure-worker-role/_static/image18.png)

"Azure 活动日志" 窗口显示部署的进度。 部署应用后，浏览到 `http://appname.cloudapp.net/` ，其中 *appname* 是你的云服务的名称。

## <a name="additional-resources"></a>其他资源

- [项目 Katana 概述](an-overview-of-project-katana.md)
- [GitHub 上的 Katana 项目](https://github.com/aspnet/AspNetKatana/)

---
uid: aspnet/overview/owin-and-katana/host-owin-in-an-azure-worker-role
title: 托管在 Azure 辅助角色中的 OWIN |Microsoft Docs
author: MikeWasson
description: 本教程演示如何在自托管 OWIN 在 Microsoft Azure 辅助角色中。 Open Web Interface for.NET (OWIN) 定义.NET web 服务器之间的抽象...
ms.author: riande
ms.date: 04/11/2014
ms.assetid: 07aa855a-92ee-4d43-ba66-5bfd7de20ee6
msc.legacyurl: /aspnet/overview/owin-and-katana/host-owin-in-an-azure-worker-role
msc.type: authoredcontent
ms.openlocfilehash: dbf0964695dd2592d063b05c0778923edffe8e2e
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57058034"
---
<a name="host-owin-in-an-azure-worker-role"></a>在 Azure 辅助角色中承载 OWIN
====================
通过[Mike Wasson](https://github.com/MikeWasson)

> 本教程演示如何在自托管 OWIN 在 Microsoft Azure 辅助角色中。
>
> [用于.NET 开放 Web 接口](http://owin.org/)(OWIN) 定义.NET web 服务器和 web 应用程序之间的抽象。 OWIN 将分离 web 应用程序从服务器中，这使 OWIN 适合于自承载在 IIS 外部自己进程中的 web 应用程序 – 例如，在 Azure 辅助角色。
>
> 在本教程中，将学习如何在自托管在 Microsoft Azure 辅助角色的 OWIN 应用程序。 若要了解有关辅助角色的详细信息，请参阅[Azure 执行模型](https://azure.microsoft.com/documentation/articles/fundamentals-application-models/#CloudServices)。
>
> ## <a name="software-versions-used-in-the-tutorial"></a>在本教程中使用的软件版本
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - [Azure SDK for .NET 2.3](https://azure.microsoft.com/downloads/)
> - [Microsoft.Owin.Selfhost 2.1.0](http://www.nuget.org/packages/Microsoft.Owin.SelfHost/2.1.0)


## <a name="create-a-microsoft-azure-project"></a>创建 Microsoft Azure 项目

使用管理员权限启动 Visual Studio。 本地调试应用程序，使用 Azure 计算仿真程序时需要管理员权限。

上**文件**菜单上，单击**新建**，然后单击**项目**。 从**已安装的模板**，在 Visual C# 中，单击**云**，然后单击**Windows Azure 云服务**。 命名项目"AzureApp"，然后单击**确定**。

[![](host-owin-in-an-azure-worker-role/_static/image2.png)](host-owin-in-an-azure-worker-role/_static/image1.png)

在中**新的 Windows Azure 云服务**对话框中，双击**辅助角色**。 保留默认名称 ("WorkerRole1")。 此步骤将辅助角色添加到解决方案。 单击 **“确定”**。

[![](host-owin-in-an-azure-worker-role/_static/image4.png)](host-owin-in-an-azure-worker-role/_static/image3.png)

创建 Visual Studio 解决方案包含两个项目：

- &quot;AzureApp&quot;定义的角色和配置 Azure 应用程序。
- &quot;WorkerRole1&quot;包含辅助角色的代码。

一般情况下，Azure 应用程序可以包含多个角色，但本教程使用单个角色。

![](host-owin-in-an-azure-worker-role/_static/image5.png)

## <a name="add-the-owin-self-host-packages"></a>添加 OWIN 自承载包

从**工具**菜单上，单击**NuGet 包管理器**，然后单击**程序包管理器控制台**。

在包管理器控制台窗口中，输入以下命令：

[!code-console[Main](host-owin-in-an-azure-worker-role/samples/sample1.cmd)]

## <a name="add-an-http-endpoint"></a>添加 HTTP 终结点

在解决方案资源管理器，展开 AzureApp 项目。 展开角色节点，右键单击 WorkerRole1，然后选择**属性**。

![](host-owin-in-an-azure-worker-role/_static/image6.png)

单击**终结点**，然后单击**添加终结点**。

在中**协议**下拉列表中，选择"http"。 在中**公用端口**并**专用端口**，键入 80。 这些端口编号可以不同。 公用端口是客户端使用时将请求发送到的角色。

[![](host-owin-in-an-azure-worker-role/_static/image8.png)](host-owin-in-an-azure-worker-role/_static/image7.png)

## <a name="create-the-owin-startup-class"></a>创建 OWIN 启动类

在解决方案资源管理器，右键单击 WorkerRole1 项目并选择**外** / **类**以添加一个新类。 将此类命名为 `Startup`。

使用以下内容替换所有样板代码：

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample2.cs)]

`UseWelcomePage`扩展方法将一个简单的 HTML 页面添加到应用程序，以验证站点是否正常工作。

## <a name="start-the-owin-host"></a>启动 OWIN 主机

打开 WorkerRole.cs 文件。 此类定义运行时辅助角色启动和停止的代码。

添加以下 using 语句：

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample3.cs)]

添加**IDisposable**成员添加到`WorkerRole`类：

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample4.cs)]

在`OnStart`方法中，添加以下代码以启动主机：

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample5.cs?highlight=5)]

**WebApp.Start**方法启动的 OWIN 主机。 名称`Startup`类是方法的类型参数。 按照约定，宿主将调用`Configure`此类的方法。

重写`OnStop`释放*\_应用*实例：

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample6.cs)]

下面是 WorkerRole.cs 的完整代码：

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample7.cs)]

生成解决方案，然后按 F5 以在 Azure 计算模拟器中本地运行应用程序。 根据防火墙设置，可能需要允许通过防火墙的仿真程序。

在计算仿真程序将本地 IP 地址分配到的终结点。 可以通过查看计算仿真程序用户界面中找到的 IP 地址。 右键单击任务栏通知区域中的模拟器图标并选择**显示计算模拟器 UI**。

[![](host-owin-in-an-azure-worker-role/_static/image10.png)](host-owin-in-an-azure-worker-role/_static/image9.png)

找到服务部署，部署 [id] 服务详细信息下的 IP 地址。 打开 web 浏览器并浏览至 http://<em>地址</em>，其中<em>地址</em>是由计算模拟器; 分配的 IP 地址，如`http://127.0.0.1:80`。 应会看到 OWIN 欢迎页：

![](host-owin-in-an-azure-worker-role/_static/image11.png)

## <a name="deploy-to-azure"></a>部署到 Azure

对于此步骤，必须具有 Azure 帐户。 如果你还没有一个，可以在几分钟即可完成创建一个免费试用帐户。 有关详细信息，请参阅[Microsoft Azure 免费试用版](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)。

在解决方案资源管理器，右键单击 AzureApp 项目。 选择“发布”。

![](host-owin-in-an-azure-worker-role/_static/image12.png)

如果您未登录到你的 Azure 帐户，请单击**Sign In**。

[![](host-owin-in-an-azure-worker-role/_static/image14.png)](host-owin-in-an-azure-worker-role/_static/image13.png)

登录后，选择订阅，然后单击**下一步**。

[![](host-owin-in-an-azure-worker-role/_static/image16.png)](host-owin-in-an-azure-worker-role/_static/image15.png)

输入云服务的名称并选择区域。 单击 **“创建”**。

![](host-owin-in-an-azure-worker-role/_static/image17.png)

单击“发布” 。

[![](host-owin-in-an-azure-worker-role/_static/image19.png)](host-owin-in-an-azure-worker-role/_static/image18.png)

Azure 活动日志窗口显示部署进度。 部署应用程序时，浏览到`http://appname.cloudapp.net/`，其中*appname*是你的云服务的名称。

## <a name="additional-resources"></a>其他资源

- [项目 Katana 概述](an-overview-of-project-katana.md)
- [GitHub 上的 Katana 项目](https://github.com/aspnet/AspNetKatana/)

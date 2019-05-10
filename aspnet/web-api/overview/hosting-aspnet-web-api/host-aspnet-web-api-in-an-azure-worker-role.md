---
uid: web-api/overview/hosting-aspnet-web-api/host-aspnet-web-api-in-an-azure-worker-role
title: 承载 ASP.NET Web API 2 中的 Azure 辅助角色-ASP.NET 4.x
author: MikeWasson
description: 教程：托管在 Azure 辅助角色中，使用 OWIN 自托管 Web API 框架的 ASP.NET Web API。
ms.author: riande
ms.date: 04/02/2014
ms.custom: seoapril2019
ms.assetid: 6980ee2e-d6b0-4a08-8fb6-ab96362dd0e3
msc.legacyurl: /web-api/overview/hosting-aspnet-web-api/host-aspnet-web-api-in-an-azure-worker-role
msc.type: authoredcontent
ms.openlocfilehash: ec9904e0bff090be0f504036ae73977cfca0cb31
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/06/2019
ms.locfileid: "65130837"
---
# <a name="host-aspnet-web-api-2-in-an-azure-worker-role"></a>承载 ASP.NET Web API 2 中的 Azure 辅助角色

通过[Mike Wasson](https://github.com/MikeWasson)

> 本教程演示如何在托管在 Azure 辅助角色中，ASP.NET Web API 使用 OWIN 自托管 Web API 框架。
>
> [用于.NET 开放 Web 接口](http://owin.org/)(OWIN) 定义.NET web 服务器和 web 应用程序之间的抽象。 OWIN 将分离 web 应用程序从服务器中，这使 OWIN 适合于自承载在 IIS 外部自己进程中的 web 应用程序 – 例如，在 Azure 辅助角色。
>
> 在本教程中，您将使用 Microsoft.Owin.Host.HttpListener 包，其中提供的 HTTP 服务器，用于自托管 OWIN 应用程序。
>
> ## <a name="software-versions-used-in-the-tutorial"></a>在本教程中使用的软件版本
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - Web API 2
> - [Azure SDK for .NET 2.3](https://azure.microsoft.com/downloads/)

## <a name="create-a-microsoft-azure-project"></a>创建 Microsoft Azure 项目

使用管理员权限启动 Visual Studio。 本地调试应用程序，使用 Azure 计算仿真程序时需要管理员权限。

上**文件**菜单上，单击**新建**，然后单击**项目**。 从**已安装的模板**，在 Visual C# 中，单击**云**，然后单击**Windows Azure 云服务**。 命名项目"AzureApp"，然后单击**确定**。

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image2.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image1.png)

在中**新的 Windows Azure 云服务**对话框中，双击**辅助角色**。 保留默认名称 ("WorkerRole1")。 此步骤将辅助角色添加到解决方案。 单击 **“确定”**。

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image4.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image3.png)

创建 Visual Studio 解决方案包含两个项目：

- &quot;AzureApp&quot;定义的角色和配置 Azure 应用程序。
- &quot;WorkerRole1&quot;包含辅助角色的代码。

一般情况下，Azure 应用程序可以包含多个角色，但本教程使用单个角色。

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image5.png)

## <a name="add-the-web-api-and-owin-packages"></a>添加 Web API 和 OWIN 包

从**工具**菜单上，单击**NuGet 包管理器**，然后单击**程序包管理器控制台**。

在包管理器控制台窗口中，输入以下命令：

[!code-console[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample1.cmd)]

## <a name="add-an-http-endpoint"></a>添加 HTTP 终结点

在解决方案资源管理器，展开 AzureApp 项目。 展开角色节点，右键单击 WorkerRole1，然后选择**属性**。

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image6.png)

单击**终结点**，然后单击**添加终结点**。

在中**协议**下拉列表中，选择"http"。 在中**公用端口**并**专用端口**，键入 80。 这些端口编号可以不同。 公用端口是客户端使用时将请求发送到的角色。

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image8.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image7.png)

## <a name="configure-web-api-for-self-host"></a>配置 Web API 的自托管

在解决方案资源管理器，右键单击 WorkerRole1 项目并选择**外** / **类**以添加一个新类。 将此类命名为 `Startup`。

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image9.png)

使用以下内容替换所有样板代码，此文件中：

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample2.cs)]

## <a name="add-a-web-api-controller"></a>添加 Web API 控制器

接下来，添加 Web API 控制器类。 右键单击 WorkerRole1 项目并选择**外** / **类**。 类 TestController 命名。 使用以下内容替换所有样板代码，此文件中：

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample3.cs)]

为简单起见，此控制器只是定义返回纯文本的两个 GET 方法。

## <a name="start-the-owin-host"></a>启动 OWIN 主机

打开 WorkerRole.cs 文件。 此类定义运行时辅助角色启动和停止的代码。

添加以下 using 语句：

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample4.cs)]

添加**IDisposable**成员添加到`WorkerRole`类：

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample5.cs)]

在`OnStart`方法中，添加以下代码以启动主机：

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample6.cs?highlight=5)]

**WebApp.Start**方法启动的 OWIN 主机。 名称`Startup`类是方法的类型参数。 按照约定，宿主将调用`Configure`此类的方法。

重写`OnStop`释放*\_应用*实例：

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample7.cs)]

下面是 WorkerRole.cs 的完整代码：

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample8.cs)]

生成解决方案，然后按 F5 以在 Azure 计算模拟器中本地运行应用程序。 根据防火墙设置，可能需要允许通过防火墙的仿真程序。

> [!NOTE]
> 如果您收到类似于以下异常，请参阅[这篇博客文章](https://blogs.msdn.com/b/praburaj/archive/2013/11/20/fileloadexception-on-microsoft-owin-when-running-on-worker-role.aspx)的一种解决方法。 "无法加载文件或程序集 Microsoft.Owin，版本 = 2.0.2.0，区域性 = 中性，PublicKeyToken = 31bf3856ad364e35 或其某个依赖项。 找到的程序集清单定义与程序集引用不匹配。 （HRESULT 异常：0x80131040)"

在计算仿真程序将本地 IP 地址分配到的终结点。 可以通过查看计算仿真程序用户界面中找到的 IP 地址。 右键单击任务栏通知区域中的模拟器图标并选择**显示计算模拟器 UI**。

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image11.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image10.png)

找到服务部署，部署 [id] 服务详细信息下的 IP 地址。 打开 web 浏览器并浏览至 http://<em>地址</em>/测试/1，其中<em>地址</em>是由计算模拟器; 分配的 IP 地址，如 `http://127.0.0.1:80/test/1` 。 应会看到来自 Web API 控制器的响应：

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image12.png)

## <a name="deploy-to-azure"></a>部署到 Azure

对于此步骤，必须具有 Azure 帐户。 如果你还没有一个，可以在几分钟即可完成创建一个免费试用帐户。 有关详细信息，请参阅[Microsoft Azure 免费试用版](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)。

在解决方案资源管理器，右键单击 AzureApp 项目。 选择“发布”。

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image13.png)

如果您未登录到你的 Azure 帐户，请单击**Sign In**。

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image15.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image14.png)

登录后，选择订阅，然后单击**下一步**。

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image17.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image16.png)

输入云服务的名称并选择区域。 单击 **“创建”**。

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image18.png)

单击“发布” 。

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image20.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image19.png)

Azure 活动日志窗口显示部署进度。 部署应用程序时，浏览到 http://appname.cloudapp.net/test/1 。

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image21.png)

## <a name="additional-resources"></a>其他资源

- [项目 Katana 概述](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)
- [GitHub 上的 Katana 项目](https://github.com/aspnet/AspNetKatana)

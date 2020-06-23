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
# <a name="tutorial-signalr-self-host"></a>教程：自承载 SignalR

作者： [Fletcher](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 本教程演示如何创建自承载的 SignalR 2 服务器，以及如何使用 JavaScript 客户端连接到该服务器。
>
> ## <a name="software-versions-used-in-the-tutorial"></a>本教程中使用的软件版本
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - .NET 4.5
> - SignalR 版本2
>
>
>
> ## <a name="using-visual-studio-2012-with-this-tutorial"></a>在本教程中使用 Visual Studio 2012
>
>
> 若要在本教程中使用 Visual Studio 2012，请执行以下操作：
>
> - 将[包管理器](http://docs.nuget.org/docs/start-here/installing-nuget)更新到最新版本。
> - 安装[Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)。
> - 在 Web 平台安装程序中，搜索并安装适用**于 Visual Studio 2012 的 ASP.NET 和 Web 工具 2013.1**。 这会为 SignalR 类（例如**中心**）安装 Visual Studio 模板。
> - 某些模板（如**OWIN Startup 类**）将不可用;对于这些情况，请改用类文件。
>
>
> ## <a name="questions-and-comments"></a>问题和注释
>
> 请提供有关你喜欢本教程的方式的反馈，并在页面底部的评论中留下反馈。 如果你有与本教程不直接相关的问题，则可以将其发布到[ASP.NET SignalR 论坛](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com/)。

## <a name="overview"></a>概述

SignalR 服务器通常托管在 IIS 的 ASP.NET 应用程序中，但也可以使用自承载库自承载（如控制台应用程序或 Windows 服务）。 此库与所有 SignalR 2 一样，都是在 OWIN （[.net 的开放 Web 接口](http://owin.org)）上构建的。 OWIN 定义 .NET web 服务器和 web 应用程序之间的抽象。 OWIN 将 web 应用程序与服务器分离，这使得 OWIN 非常适合用于在你自己的进程（IIS 以外）中自承载 web 应用程序。

不在 IIS 中托管的原因包括：

- IIS 不可用或不需要的环境，如没有 IIS 的现有服务器场。
- 需要避免 IIS 的性能开销。
- SignalR 功能将添加到在 Windows 服务、Azure 辅助角色或其他进程中运行的现有应用程序。

如果出于性能方面的原因，将解决方案作为自宿主进行开发，则建议也测试在 IIS 中托管的应用程序，以确定性能优势。

本教程包含以下部分：

- [创建服务器](#server)
- [使用 JavaScript 客户端访问服务器](#js)

<a id="server"></a>

## <a name="creating-the-server"></a>创建服务器

在本教程中，你将创建一个托管在控制台应用程序中的服务器，但该服务器可以托管在任何类型的进程中，如 Windows 服务或 Azure 辅助角色。 有关在 Windows 服务中承载 SignalR 服务器的示例代码，请参阅[Windows 服务中的自承载 SignalR](https://code.msdn.microsoft.com/SignalR-self-hosted-in-6ff7e6c3)。

1. 以管理员权限打开 Visual Studio 2013。 选择 "**文件**"、"**新建项目**"。 在 "**模板**" 窗格中的 " **Visual c #** " 节点下选择 " **Windows** "，然后选择 "**控制台应用程序**" 模板。 将新项目命名为 "SignalRSelfHost"，然后单击 **"确定**"。

    ![](tutorial-signalr-self-host/_static/image1.png)
2. 通过选择 "**工具**" "  >  **nuget 包管理**器" "  >  **包管理器控制台**"，打开 NuGet 包管理器控制台。
3. 在 "程序包管理器控制台" 中，输入以下命令：

    [!code-powershell[Main](tutorial-signalr-self-host/samples/sample1.ps1)]

    此命令将 SignalR 2 自承载库添加到项目。
4. 在 "程序包管理器控制台" 中，输入以下命令：

    [!code-powershell[Main](tutorial-signalr-self-host/samples/sample2.ps1)]

    此命令将 Owin 库添加到项目。 此库将用于跨域支持，此支持是在不同域中承载 SignalR 和网页客户端的应用程序所必需的。 由于你将在不同的端口上托管 SignalR 服务器和 web 客户端，因此这意味着必须启用跨域，以便在这些组件之间进行通信。
5. 将 Program.cs 的内容替换为以下代码。

    [!code-csharp[Main](tutorial-signalr-self-host/samples/sample3.cs)]

    上面的代码包括三个类：

    - **程序**，包括定义主执行路径的**Main**方法。 在此方法中，**启动类型为**的 web 应用程序是在指定的 URL （）启动的 `http://localhost:8080` 。 如果终结点上需要安全性，则可以实现 SSL。 有关详细信息，请参阅[如何：使用 SSL 证书配置端口](https://msdn.microsoft.com/library/ms733791.aspx)。
    - **启动**时，包含 SignalR 服务器的配置的类（本教程使用的唯一配置是对的调用 `UseCors` ）以及对的调用 `MapSignalR` ，后者为项目中的任何中心对象创建路由。
    - **MyHub**，应用程序将提供给客户端的 SignalR Hub 类。 此类有一个方法 "**发送**"，客户端将调用以将消息广播到所有其他已连接的客户端。
6. 编译并运行该应用程序。 运行服务器的地址应显示在控制台窗口中。

    ![](tutorial-signalr-self-host/_static/image2.png)
7. 如果执行失败并出现异常 `System.Reflection.TargetInvocationException was unhandled` ，你将需要重新启动具有管理员权限的 Visual Studio。
8. 停止应用程序，然后继续下一部分。

<a id="js"></a>

## <a name="accessing-the-server-with-a-javascript-client"></a>使用 JavaScript 客户端访问服务器

在本部分中，你将使用[入门教程](../getting-started/tutorial-getting-started-with-signalr.md)中的相同 JavaScript 客户端。 我们只会对客户端进行一项修改，即显式定义中心 URL。 对于自承载的应用程序，服务器可能不一定与连接 URL 位于同一地址（因为反向代理和负载均衡器），因此需要显式定义 URL。

1. 在**解决方案资源管理器**中，右键单击解决方案并选择 "**添加**"、"**新建项目**"。 选择 " **web** " 节点，然后选择 " **ASP.NET Web 应用程序**" 模板。 将项目命名为 "JavascriptClient"，然后单击 **"确定**"。

    ![](tutorial-signalr-self-host/_static/image3.png)
2. 选择**空**模板，并保留未选定的其余选项。 选择 "**创建项目**"。

    ![](tutorial-signalr-self-host/_static/image4.png)
3. 在 "程序包管理器控制台" 中，选择 "**默认项目**" 下拉下的 "JavascriptClient" 项目，然后执行以下命令：

    [!code-powershell[Main](tutorial-signalr-self-host/samples/sample4.ps1)]

    此命令安装客户端中所需的 SignalR 和 JQuery 库。
4. 右键单击项目，然后选择 "**添加**"、"**新建项**"。 选择 " **Web** " 节点，然后选择 "HTML 页"。 将页面命名**Default.html**。

    ![](tutorial-signalr-self-host/_static/image5.png)
5. 将新 HTML 页面的内容替换为以下代码。 验证此处的脚本引用是否与项目的 Scripts 文件夹中的脚本匹配。

    [!code-html[Main](tutorial-signalr-self-host/samples/sample5.html?highlight=31-32)]

    下面的代码（上面的代码示例中突出显示的代码）是你在获取入门教程中所使用的客户端的补充（除了将代码升级到 SignalR 版本 2 beta 版本之外）。 此代码行显式设置服务器上的 SignalR 的基连接 URL。

    [!code-javascript[Main](tutorial-signalr-self-host/samples/sample6.js)]
6. 右键单击该解决方案，然后选择 "**设置启动项目 ...**"。选择 "**多启动项目**" 单选按钮，并将两个项目的 "**操作**" 设置为 "**启动**"。

    ![](tutorial-signalr-self-host/_static/image6.png)
7. 右键单击 "Default.html" 并选择 "**设为起始页**"。
8. 运行应用程序。 服务器和页面将启动。 如果在启动服务器之前加载页面，则可能需要重新加载网页（或选择 "在调试器中**继续**"）。
9. 在浏览器中，在出现提示时提供用户名。 将页面的 URL 复制到其他浏览器选项卡或窗口中，并提供不同的用户名。 你将能够将消息从一个浏览器窗格发送到另一个浏览器窗格，如入门教程中所示。

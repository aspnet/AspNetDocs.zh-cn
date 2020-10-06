---
uid: mvc/overview/deployment/docker-aspnetmvc
title: 将 ASP.NET MVC 应用程序迁移到 Windows 容器
description: 了解如何利用现有 ASP.NET MVC 应用程序并在 Windows Docker 容器中运行它
keywords: Windows 容器，Docker，ASP .NET MVC
author: BillWagner
ms.author: wiwagn
ms.date: 12/14/2018
ms.assetid: c9f1d52c-b4bd-4b5d-b7f9-8f9ceaf778c4
ms.openlocfilehash: 1c5e6af79c87123891ddd4d30c60e3a427910e9d
ms.sourcegitcommit: 09a34635ed0e74d6c2625f6a485c78f201c689ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/06/2020
ms.locfileid: "91763485"
---
# <a name="migrating-aspnet-mvc-applications-to-windows-containers"></a>将 ASP.NET MVC 应用程序迁移到 Windows 容器

在 Windows 容器中运行现有的 .NET Framework 应用程序不需要对应用程序进行任何更改。 若要在 Windows 容器中运行应用程序，请创建包含应用程序的 Docker 映像，然后启动容器。 本主题介绍了如何获取现有的 [ASP.NET MVC 应用程序](http://www.asp.net/mvc)，并在 Windows 容器中进行部署。

从现有的 ASP.NET MVC 应用程序入手，然后使用 Visual Studio 生成已发布的资产。 使用 Docker 创建包含并运行应用程序的映像。 转到在 Windows 容器中运行的网站，验证应用程序是否正常运行。

本文假定读者对 Docker 有一个基本的了解。 阅读 [Docker Overview](https://docs.docker.com/engine/understanding-docker/)（Docker 概述）即可了解 Docker。

在容器中运行的应用程序是一个随机回答问题的简单网站。 此应用程序是一款不具备身份验证或数据库存储的基本 MVC 应用程序，让你可以专心处理将 Web 层移到容器中。 后续主题将演示如何在容器化应用程序中移动和管理永久性存储。

移动应用程序涉及以下步骤：

1. [创建发布任务以生成映像资产。](#publish-script)
1. [生成将运行应用程序的 Docker 映像。](#build-the-image)
1. [启动用于运行映像的 Docker 容器。](#start-a-container)
1. [使用浏览器验证应用程序。](#verify-in-the-browser)

[完成的应用程序](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/mvc/overview/deployment/docker-aspnetmvc/samples/MVCRandomAnswerGenerator)位于 GitHub 上。

## <a name="prerequisites"></a>必备知识

开发计算机必须具有以下软件：

- [Windows 10 周年更新](https://www.microsoft.com/software-download/windows10/) (或更高版本) 或 [windows Server 2016](https://www.microsoft.com/cloud-platform/windows-server) (或更高版本) 
- [用于 Windows 的 Docker](https://docs.docker.com/docker-for-windows/) - 稳定版 1.13.0 或 1.12 beta 版本 26（或更高版本）
- [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)

> [!IMPORTANT]
> 如果使用的是 Windows Server 2016，请按[容器主机部署 - Windows Server](https://msdn.microsoft.com/virtualization/windowscontainers/deployment/deployment) 中的说明操作。

安装并启动 Docker 以后，右键单击任务栏图标，并选择“切换到 Windows 容器”。 这是运行基于 Windows 的 Docker 映像所必需的。 此命令需要几秒钟执行：

![Windows 容器][windows-container]

## <a name="publish-script"></a>发布脚本

在一个位置收集需加载到 Docker 映像中的所有资产。 可以使用 Visual Studio 的“**发布**”命令来创建应用程序的发布配置文件。 此配置文件会将所有资产汇集到同一目录树中，本教程的后面部分将介绍如何将此目录树复制到目标映像。

**发布步骤**

1. 在 Visual Studio 中右键单击 Web 项目，然后选择“发布”****。
1. 单击“**自定义配置文件**”按钮，然后选择“**文件系统**”作为方法。
1. 选择该目录。 按照约定，已下载示例将使用 `bin\Release\PublishOutput`。

![发布连接][publish-connection]

打开 "**设置**" 选项卡的 "**文件发布选项**" 部分。选择 "**在发布期间预编译**"。 这种优化意味着，在复制预编译视图的同时，在 Docker 容器中编译视图。

![发布设置][publish-settings]

单击“发布”****，Visual Studio 会将所有所需资产复制到目标文件夹。

## <a name="build-the-image"></a>生成映像

创建名为 *Dockerfile* 的新文件来定义 Docker 映像。 *Dockerfile* 包含用于构建最终映像的说明，并包括所有基本映像名称、必需组件、要运行的应用程序和其他配置映像。 *Dockerfile* 是 `docker build` 命令的输入，该命令用于创建映像。

对于本练习，你将基于 `microsoft/aspnet` 位于 [Docker 中心](https://hub.docker.com/r/microsoft/aspnet/)的映像生成映像。
基本映像 `microsoft/aspnet` 为 Windows Server 映像。 它包含 Windows Server Core、IIS 和 ASP.NET 4.7.2。 在容器中运行此映像时，它会自动启动 IIS 和已安装的网站。

创建映像的 Dockerfile 如下所示：

```console
# The `FROM` instruction specifies the base image. You are
# extending the `microsoft/aspnet` image.

FROM microsoft/aspnet

# The final instruction copies the site you published earlier into the container.
COPY ./bin/Release/PublishOutput/ /inetpub/wwwroot
```

此 Dockerfile 中没有 `ENTRYPOINT` 命令。 不需要该命令。 在运行带有 IIS 的 Windows Server 时，IIS 进程是入口点，配置为在 aspnet 基本映像中启动。

运行 Docker 生成命令，创建运行 ASP.NET 应用程序的映像。 为此，请在项目的目录中打开 PowerShell 窗口，然后在解决方案目录中键入以下命令：

```console
docker build -t mvcrandomanswers .
```

此命令将使用 Dockerfile 中的说明生成新映像，并将映像) 命名 ( 标记为 mvcrandomanswers。 这样做可能还会从 [Docker 中心](http://hub.docker.com)拉取基本映像，然后将应用程序添加到基本映像中。

命令完成后，便可以运行 `docker images` 命令，查看有关新映像的信息：

```console
REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
mvcrandomanswers              latest              86838648aab6        2 minutes ago       10.1 GB
```

计算机上的 IMAGE ID 会所不同。 现在，让我们来运行应用程序。

## <a name="start-a-container"></a>启动容器

通过执行以下 `docker run` 命令来启动容器：

```console
docker run -d --name randomanswers mvcrandomanswers
```

`-d` 参数告知 Docker 在分离模式下启动映像。 这意味着 Docker 映像会以断开连接当前 shell 的状态运行。

在许多 docker 示例中，你可能会看到-p 映射容器和主机端口。 默认的 aspnet 映像已将容器配置为侦听端口80并公开它。

`--name randomanswers` 为运行中容器命名。 可在大多数命令中使用此名称，而不是容器 ID。

`mvcrandomanswers` 是要启动的映像名称。

## <a name="verify-in-the-browser"></a>在浏览器中验证

容器启动后， `http://localhost` 在显示的示例中使用连接到正在运行的容器。 在浏览器中键入该 URL，应该可看到正在运行的站点。

> [!NOTE]
> 某 VPN 或代理软件可能会阻止你导航到站点。
> 可以暂时禁用它，确保容器正常工作。

GitHub 上的示例目录包含为你执行这些命令的 [PowerShell 脚本](https://github.com/dotnet/samples/blob/master/framework/docker/MVCRandomAnswerGenerator/run.ps1)。 打开 PowerShell 窗口，将目录更改为解决方案目录，然后键入：

```console
./run.ps1
```

上述命令将生成映像，显示计算机上的映像列表，并启动容器。

若要停止容器，请发出 `docker stop` 命令：

```console
docker stop randomanswers
```

若要删除该容器，可发出 `docker rm` 命令：

```console
docker rm randomanswers
```

[windows-container]: media/aspnetmvc/SwitchContainer.png "切换到 Windows 容器"
[publish-connection]: media/aspnetmvc/PublishConnection.png "发布到文件系统"
[publish-settings]: media/aspnetmvc/PublishSettings.png "发布设置"

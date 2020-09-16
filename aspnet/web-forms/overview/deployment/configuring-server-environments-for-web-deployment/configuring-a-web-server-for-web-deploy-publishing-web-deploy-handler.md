---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler
title: 配置用于 Web 部署发布的 Web 服务器（Web 部署处理程序）
author: jrjlee
description: 本主题介绍如何配置 Internet Information Services (IIS) web 服务器，以支持使用 IIS Web 部署汉语 .。。
ms.author: riande
ms.date: 01/29/2017
ms.assetid: 90ebf911-1c46-4470-b876-1335bd0f590f
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler
msc.type: authoredcontent
ms.openlocfilehash: af46b5a74309fbae4b5db072363e71d965445f9a
ms.sourcegitcommit: 4ed0b65ae32d9f35e42ee6296b877747e063df4d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/16/2020
ms.locfileid: "90609683"
---
# <a name="configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler"></a>配置用于 Web 部署发布的 Web 服务器（Web 部署处理程序）

[PDF 下载](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主题介绍如何使用 IIS Web 部署处理程序将 Internet Information Services (IIS) web 服务器配置为支持 web 发布和部署。
> 
> 使用 Web 部署2.0 或更高版本时，有三种主要方法可用于将应用程序或站点获取到 Web 服务器。 你可以：
> 
> - 使用 *Web 部署远程代理服务*。 此方法需要较少的 web 服务器配置，但你需要提供本地服务器管理员的凭据才能将任何内容部署到服务器。
> - 使用 *Web 部署处理程序*。 这种方法更复杂，需要进行更多初始工作才能设置 web 服务器。 但是，在使用此方法时，可以将 IIS 配置为允许非管理员用户执行部署。 Web 部署处理程序仅在 IIS 版本7或更高版本中可用。
> - 使用 *脱机部署*。 此方法需要最少的 web 服务器配置，但服务器管理员必须手动将 web 包复制到服务器上，并通过 IIS 管理器将其导入。
> 
> 有关这些方法的主要功能、优点和缺点的详细信息，请参阅 [选择正确的 Web 部署方法](choosing-the-right-approach-to-web-deployment.md)。

是，如果你希望允许非管理员用户将内容部署到特定的 IIS 网站。 此方法在以下类型的方案中通常是必需的：

- 过渡环境或生产环境，其中触发远程部署的人员或服务帐户不可能有权访问服务器管理员的凭据。
- 托管环境：你希望使远程用户能够更新其网站，而无需为他们提供对 web 服务器的完全控制权限， (或访问其他用户的网站) 。

在开发或测试方案中，或在小型组织中，使用服务器管理员凭据部署内容通常不会争用资源。 在这些情况下，将 web 服务器配置为支持使用 [Web 部署远程代理服务](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md) 进行部署，提供了更简单的方法。

## <a name="task-overview"></a>任务概述

若要将 web 服务器配置为使用 Web 部署处理程序方法从远程计算机接受和部署 web 包，需执行以下操作：

- 创建或选择一个域用户帐户 (要用于执行部署的凭据的 "非管理员用户" ) 。
- 安装 IIS 7.5，包括 Web 管理服务和基本身份验证模块。
- 安装 Web 部署2.1 或更高版本。
- 将 Web 管理服务配置为允许远程连接，并启动服务。
- 创建一个 IIS 网站来托管已部署的内容。
- 在 IIS 管理器中为你的网站授予非管理员用户权限。
- 确保 Web 管理服务委派规则允许服务使用您的非管理员用户帐户添加和更改网站内容。
- 配置任何防火墙以允许端口8172上的传入连接。

若要专门托管 ContactManager 示例解决方案，还需要：

- 安装 .NET Framework 4.0。
- 安装 ASP.NET MVC 3。

本主题将演示如何执行上述每个过程。 本主题中的任务和演练假设你开始使用运行 Windows Server 2016 的干净服务器版本。 继续之前，请确保：

- Windows Server 2016
- 服务器已加入域。
- 服务器具有静态 IP 地址。

> [!NOTE]
> 有关将计算机加入域的详细信息，请参阅将 [计算机加入到域并登录](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx)。 有关配置静态 IP 地址的详细信息，请参阅 [配置静态 Ip 地址](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx)。

## <a name="install-products-and-components"></a>安装产品和组件

本部分将指导你完成在 web 服务器上安装所需的产品和组件。 在开始之前，好的做法是运行 Windows 更新以确保服务器完全处于最新状态。

在这种情况下，需要安装以下内容：

- **IIS 7 建议的配置**。 这会使 **Web 服务器 (** web 服务器上的 iis) 角色，并安装承载 ASP.NET 应用程序所需的一组 iis 模块和组件。
- **IIS：管理服务**。 这会在 IIS 中安装 (WMSvc) 的 Web 管理服务。 此服务启用 IIS 网站的远程管理，并向客户端公开 Web 部署处理程序终结点。
- **IIS：基本身份验证**。 这会安装 IIS 基本身份验证模块。 这使 Web 管理服务 (WMSvc) 验证你提供的凭据。
- **Web 部署工具2.1 或更高版本**。 这会在服务器上安装 Web 部署 (及其基础可执行文件 MSDeploy.exe) 。 作为此过程的一部分，它将安装 Web 部署处理程序，并将其与 Web 管理服务集成。
- **.NET Framework 4.0**。 这是运行在此版本的 .NET Framework 上构建的应用程序所必需的。
- **ASP.NET MVC 3**。 这将安装运行 MVC 3 应用程序所需的程序集。

> [!NOTE]
> 本演练介绍了如何使用 Web 平台安装程序来安装和配置各种组件。 尽管无需使用 Web 平台安装程序，但它可以通过自动检测依赖项并确保始终获取最新的产品版本来简化安装过程。 有关详细信息，请参阅 [Microsoft Web 平台安装程序](https://go.microsoft.com/?linkid=9805118)。

**安装所需的产品和组件**

1. 下载并安装 [Web 平台安装程序](https://go.microsoft.com/?linkid=9805118)。
2. 安装完成后，Web 平台安装程序将自动启动。

    > [!NOTE]
    > 你现在可以从 " **开始** " 菜单启动 Web 平台安装程序。 为此，请在 " **开始** " 菜单上，单击 " **所有程序**"，然后单击 " **Microsoft Web 平台安装程序**"。
3. 在“Web 平台安装程序”**** 窗口的顶部，单击“产品”****。
4. 在窗口左侧的导航窗格中，单击 " **框架**"。
5. 在 **Microsoft .NET Framework 4** "行中，如果尚未安装 .NET Framework，请单击" **添加**"。

    > [!NOTE]
    > 可能已通过 Windows 更新安装 .NET Framework 4.0。 如果产品或组件已安装，Web 平台安装程序将通过将 " **添加** " 按钮替换为 **安装**的文本来指示这一点。

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image1.png)
6. 在 **ASP.NET MVC 3 (Visual Studio 2010) ** 行中，单击 " **添加**"。
7. 在导航窗格中，单击 " **服务器**"。
8. 在 " **IIS 7 推荐的配置** " 行中，单击 " **添加**"。
9. 在 **Web 部署工具 2.1** 行中，单击 " **添加**"。
10. 在 " **IIS：基本身份验证** " 行中，单击 " **添加**"。
11. 在 " **IIS：管理服务** " 行中，单击 " **添加**"。
12. 单击“安装” 。 Web 平台安装程序将向你显示一个产品列表，其中包含要安装的任何关联依赖项&#x2014;&#x2014;，并将提示你接受许可条款。

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image2.png)
13. 查看许可条款，如果同意条款，请单击 " **我接受**"。
14. 安装完成后，单击 " **完成**"，然后关闭 " **Web 平台安装程序** " 窗口。

如果在安装 IIS 之前安装了 .NET Framework 4.0，则需要运行 [ASP.NET Iis 注册工具](https://msdn.microsoft.com/library/k6h9cz8h(v=VS.100).aspx) (aspnet \_regiis.exe) 向 IIS 注册 ASP.NET 的最新版本。 如果不这样做，你会发现，IIS 将 (的静态内容提供) HTML 文件，但不会有任何问题，但在你尝试浏览到 ASP.NET 内容时，它将返回 **HTTP 错误404.0 –找不** 到。 您可以使用下一个过程来确保 ASP.NET 4.0 已注册。

**向 IIS 注册 ASP.NET 4。0**

1. 单击 " **开始**"，然后键入 **命令提示符**。
2. 在搜索结果中，右键单击 " **命令提示符**"，然后单击 " **以管理员身份运行**"。
3. 在命令提示符窗口中，导航到 " **%windir%\microsoft.net\framework\v4.0.30319 (对于** " 目录。
4. 键入以下命令，然后按 Enter：

    [!code-console[Main](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/samples/sample1.cmd)]
5. 如果你打算随时托管64位 web 应用程序，则还应将 ASP.NET 的64位版本注册到 IIS。 为此，请在命令提示符窗口中导航到 **%windir%\microsoft.net\framework64\v4.0.30319 (对于** 目录。
6. 键入以下命令，然后按 Enter：

    [!code-console[Main](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/samples/sample2.cmd)]

作为一种很好的做法，请再次使用 Windows 更新，下载并安装适用于已安装的新产品和组件的任何可用更新。

## <a name="configure-the-web-management-service"></a>配置 Web 管理服务

现在，你已安装了所需的一切，接下来的步骤是在 IIS 中配置 Web 管理服务。 在高级别上，需要完成以下任务：

- 在服务器级别启用基本身份验证。
- 将 Web 管理服务配置为接受远程连接。
- 启动 Web 管理服务。
- 检查所需的 Web 管理服务委派规则是否已就位。

**配置 Web 管理服务**

1. 在 " **开始** " 菜单上，指向 " **管理工具**"，然后单击 " **Internet Information Services (IIS) 管理器**"。
2. 在 IIS 管理器的 " **连接** " 窗格中，单击 "服务器" 节点 (例如 **STAGEWEB1**) 。

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image3.png)
3. 在中心窗格中的 " **IIS**" 下，双击 " **身份验证**"。

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image20.png)
4. 右键单击 " **基本身份验证**"，然后单击 " **启用**"。

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image5.png)
5. 在 " **连接** " 窗格中，再次单击服务器节点以返回到顶级设置。
6. 在中心窗格中的 " **管理**" 下，双击 " **管理服务**"。

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image6.png)
7. 在中心窗格中，选择 " **启用远程连接**"。

    > [!NOTE]
    > 如果 Web 管理服务已经在运行，则需要先将其停止。
8. 在 " **操作** " 窗格中，单击 " **启动** " 以启动 Web 管理服务。

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image7.png)
9. 如果系统提示你保存设置，请单击 **"是"**。

    > [!NOTE]
    > 你可能还想要将服务配置为自动启动。 为此，请打开 "服务" 控制台，右键单击 " **Web 管理服务**"，然后单击 " **属性**"。 在 " **启动类型** " 下拉列表中，选择 " **自动**"，然后单击 **"确定"**。
10. 在 " **连接** " 窗格中，再次单击服务器节点以返回到顶级设置。
11. 在中心窗格中的 " **管理**" 下，双击 " **管理服务委托**"。

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image8.png)
12. 验证中心窗格是否包含一组规则。

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image9.png)

    这些规则允许授权 Web 管理服务用户使用各种 Web 部署提供程序。 例如，若要通过 Web 部署处理程序将 web 应用程序和内容部署到 IIS，则必须有一个委派规则，该规则允许所有经过身份**验证的 Web**管理**iisApp**服务用户 (可在屏幕快照) 中看到的最后一个规则。

    如果按照本主题中所述的顺序安装了产品和组件，最新版本的 Web 部署应自动向 Web 管理服务添加所有必需的委派规则。 如果 "管理服务委派" 页没有显示任何规则，则需要自行创建。 有关如何执行此操作的说明，请参阅 [配置 Web 部署处理程序](https://go.microsoft.com/?linkid=9805124)。
13. 在 " **连接** " 窗格中，再次单击服务器节点以返回到顶级设置。

## <a name="create-and-configure-an-iis-website"></a>创建和配置 IIS 网站

你需要创建并配置一个 IIS 网站来托管内容，然后才能将 web 内容部署到你的服务器。 Web 部署只能将 web 包部署到现有 IIS 网站;它无法为你创建网站。 还需要执行一些额外的配置，以允许非管理员帐户远程部署内容。 在高级别上，需要完成以下任务：

- 在文件系统上创建一个文件夹以托管你的内容。
- 创建一个 IIS 网站来提供内容，并将其与本地文件夹关联。
- 向本地文件夹上的应用程序池标识授予读取权限。
- 向将部署你的 web 应用程序的域帐户授予必要的 IIS 权限。

尽管不会阻止你将内容部署到 IIS 中的默认网站，但对于除测试或演示方案之外的任何内容，不建议使用此方法。 若要模拟生产环境，应该创建一个新的 IIS 网站，其中包含特定于应用程序要求的设置。

**创建 IIS 网站**

1. 在本地文件系统上，创建一个文件夹以存储内容 (例如 **C:\DemoSite**) 。
2. 在 " **开始** " 菜单上，指向 " **管理工具**"，然后单击 " **Internet Information Services (IIS) 管理器**"。
3. 在 IIS 管理器的 " **连接** " 窗格中，展开 "服务器" 节点 (例如 **STAGEWEB1**) 。

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image10.png)
4. 右键单击 " **站点** " 节点，然后单击 " **添加网站**"。
5. 在 " **站点名称** " 框中，键入 IIS 网站的名称 (例如， **DemoSite**) 。
6. 在 " **物理路径** " 框中，键入 (或浏览) 本地文件夹 (路径，例如 **C:\DemoSite**) 。
7. 在 " **端口** " 框中，键入要在其上托管网站 (的端口号，例如 **85**) 。

    > [!NOTE]
    > 对于 HTTP，标准端口号为80，对于 HTTPS 则为443。 但是，如果你在端口80上托管此网站，你将需要停止默认网站，然后才能访问你的站点。
8. 将 " **主机名** " 框留空，除非要为网站配置域名系统 (DNS) 记录，然后单击 **"确定"**。

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image11.png)

    > [!NOTE]
    > 在生产环境中，你可能想要在端口80上托管你的网站，并配置主机标头和匹配的 DNS 记录。 有关在 IIS 7 中配置主机标头的详细信息，请参阅 [配置网站的主机标头 (IIS 7) ](https://technet.microsoft.com/library/cc753195(WS.10).aspx)。 有关 Windows Server 中的 DNS 服务器角色的详细信息，请参阅 [Dns 服务器概述](https://technet.microsoft.com/library/cc770392.aspx) 和 [dns 服务器](https://technet.microsoft.com/windowsserver/dd448607)。
9. 在“操作” **** 窗格中的“编辑站点” **** 之下，单击“绑定” ****。
10. 在“网站绑定”**** 对话框中，单击“添加”****。

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image12.png)
11. 在 " **添加站点绑定** " 对话框中，将 " **IP 地址** " 和 " **端口** " 设置为与现有站点配置匹配。
12. 在 " **主机名** " 框中，键入 web 服务器的名称 (例如 **STAGEWEB1**) ，然后单击 **"确定"**。

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image13.png)

    > [!NOTE]
    > 第一个站点绑定允许使用 IP 地址和端口或在本地访问站点 `http://localhost:85` 。 第二个站点绑定允许使用计算机名称从域中的其他计算机访问站点 (例如， http://stageweb1:85) 。
13. 在 **“网站绑定”** 对话框中，单击 **“关闭”**。
14. 在“连接”**** 窗格中，单击“应用程序池”****。
15. 在 " **应用程序池** " 窗格中，右键单击应用程序池的名称，然后单击 " **基本设置**"。 默认情况下，应用程序池的名称将与网站的名称相匹配 (例如 **DemoSite**) 。
16. 在 " **.NET clr 版本** " 列表中，选择 " **.net clr 4.0.30319**"，然后单击 **"确定"**。

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image21.png)

    > [!NOTE]
    > 示例解决方案需要 .NET Framework 4.0。 这并不是对 Web 部署一般的要求。

为了使你的网站提供内容，应用程序池标识必须对存储内容的本地文件夹具有读取权限。 在 IIS 7.5 中，应用程序池默认情况下使用唯一的应用程序池标识运行，与以前版本的 IIS 不同 (，应用程序池通常使用网络服务帐户) 运行。 应用程序池标识不是真实的用户帐户，并且不会显示在&#x2014;的任何用户或组列表中，而是在启动应用程序池时动态创建。 每个应用程序池标识都作为隐藏项添加到本地 **IIS \_ iis-iusrs** 安全组。

若要授予对文件或文件夹上的应用程序池标识的权限，可以使用两个选项：

- 通过使用 **Iis AppPool \( 应用程序池名称格式) ** (例如 **iis AppPool\DemoSite**) ，来直接将权限分配给应用程序池标识。
- 将权限分配给 **IIS \_ iis-iusrs** 组。

最常见的方法是将权限分配给本地 **IIS \_ iis-iusrs** 组，因为此方法允许你在不重新配置文件系统权限的情况下更改应用程序池。 下一过程使用此基于组的方法。

> [!NOTE]
> 有关 IIS 7.5 中的应用程序池标识的详细信息，请参阅 [应用程序池标识](https://go.microsoft.com/?linkid=9805123)。

**配置 IIS 网站的文件夹权限**

1. 在 Windows 资源管理器中，浏览到本地文件夹的位置。
2. 右键单击该文件夹，然后单击 **“属性”**。
3. 在“**Security**”选项卡上，依次单击“**Edit**”、“**Add**”。
4. 单击“位置”。 在 " **位置** " 对话框中，选择本地服务器，然后单击 **"确定"**。

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image15.png)
5. 在 " **选择用户或组** " 对话框中，键入 **IIS \_ Iis-iusrs**，单击 " **检查名称**"，然后单击 **"确定"**。
6. 在 " ** (文件夹名称) 的权限 ** " 对话框中，请注意，默认情况下已为新组分配了 " **读取 &amp; 执行**"、" **列出文件夹内容**" 和 " **读取** " 权限。 保持不变，并单击 **"确定"**。
7. 单击 **"确定"** 以关闭 "属性" 对话框 ** (文件夹) 名称** 。

作为最终任务，您必须向非管理员用户授予适当的权限，该用户的凭据将用于部署内容。 此用户需要权限以远程方式将内容部署到你的网站。

**为非管理员域用户配置 IIS 网站权限**

1. 在 IIS 管理器的 " **连接** " 窗格中，右键单击你的网站节点 (例如， **DemoSite**) "，指向" **部署**"，然后单击" **配置 "Web 部署发布**。

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image16.png)
2. 在 " **配置 Web 部署发布** " 对话框中，在 " **选择要向其授予发布权限的用户** " 列表右侧，单击省略号按钮。

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image17.png)
3. 在 " **允许用户** " 对话框中，键入要用于部署内容的帐户的域和用户名，然后单击 **"确定"**。

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image18.png)
4. 在 " **配置 Web 部署发布** " 对话框中，单击 " **设置**"。

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image19.png)

    > [!NOTE]
    > 此操作在一个步骤中执行两项关键功能。 首先，它授予用户通过 Web 管理服务远程修改网站的权限，具体取决于你在上一部分中检查的委派规则。 其次，它向用户授予网站的源文件夹的完全控制权限，这允许用户对网站内容添加、修改和设置权限。
5. 在 " **配置 Web 部署发布** " 对话框中，单击 " **关闭**"。

## <a name="configure-firewall-exceptions"></a>配置防火墙例外

默认情况下，IIS Web 管理服务在 TCP 端口8172上进行侦听。 如果在 web 服务器上启用了 Windows 防火墙，则需要创建新的入站规则，以允许端口8172上的 TCP 流量 (默认情况下，Windows 防火墙) 中允许所有出站流量。 如果使用第三方防火墙，则需要创建允许流量的规则。

| 方向 | 从端口 | 到端口 | 端口类型 |
| --- | --- | --- | --- |
| 入站 | 任意 | 8172 | TCP |
| 出站 | 8172 | 任意 | TCP |

有关在 Windows 防火墙中配置规则的详细信息，请参阅 [配置防火墙规则](https://technet.microsoft.com/library/dd448559(WS.10).aspx)。 对于第三方防火墙，请查阅你的产品文档。

## <a name="conclusion"></a>结论

你的 web 服务器现在应该已准备好通过 Web 管理服务接受到 Web 部署处理程序的远程部署。 尝试将 web 应用程序部署到服务器之前，可能需要检查以下要点：

- 是否在 IIS 中的服务器级别启用了基本身份验证？
- 是否启用了到 Web 管理服务的远程连接？
- 是否已启动 Web 管理服务？
- 是否有管理服务委派规则？
- 应用程序池标识是否具有对你的网站的源文件夹的 "读取" 访问权限？
- 非管理员用户帐户在 IIS 中是否有站点级权限？
- 防火墙是否允许在 TCP 端口8172上传入连接到服务器？

## <a name="further-reading"></a>深入阅读

有关如何配置自定义 Microsoft 生成引擎 (MSBuild) 项目文件以将 web 包部署到 Web 部署处理程序的指南，请参阅 [配置目标环境的部署属性](configuring-deployment-properties-for-a-target-environment.md)。

> [!div class="step-by-step"]
> [上一页](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)
> [下一页](configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)

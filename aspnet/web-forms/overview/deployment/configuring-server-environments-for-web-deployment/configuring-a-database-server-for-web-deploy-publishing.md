---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-database-server-for-web-deploy-publishing
title: 为 Web 部署发布配置数据库服务器 |Microsoft Docs
author: jrjlee
description: 本主题介绍如何配置 SQL Server 2008 R2 数据库服务器，以支持 web 部署和发布。 本主题中所述的任务是合作者 。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: e7c447f9-eddf-4bbe-9f18-3326d965d093
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-database-server-for-web-deploy-publishing
msc.type: authoredcontent
ms.openlocfilehash: ade3c1ba1c470092f512436f39b8831458408c2c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78515240"
---
# <a name="configuring-a-database-server-for-web-deploy-publishing"></a>配置用于 Web 部署发布的数据库服务器

作者： [Jason](https://github.com/jrjlee)

[下载 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主题介绍如何配置 SQL Server 2008 R2 数据库服务器，以支持 web 部署和发布。
> 
> 本主题中所述的任务适用于每种部署&#x2014;方案，无论你的 web 服务器是配置为使用 IIS Web 部署工具（Web 部署）远程代理服务、Web 部署处理程序还是脱机部署，或者你的应用程序在单个 web 服务器或服务器场中运行，这并不重要。 部署数据库的方式可能会根据安全要求和其他注意事项发生变化。 例如，你可以部署包含或不包含示例数据的数据库，你可以部署用户角色映射，或在部署后手动配置它们。 但是，配置数据库服务器的方式保持不变。

您无需安装任何其他产品或工具来配置数据库服务器以支持 web 部署。 假设您的数据库服务器和 web 服务器运行在不同的计算机上，只需执行以下操作：

- 允许 SQL Server 使用 TCP/IP 进行通信。
- 允许通过任何防火墙 SQL Server 流量。
- 为 web 服务器计算机帐户 SQL Server 登录名。
- 将计算机帐户登录映射到任何所需的数据库角色。
- 为将运行部署 SQL Server 登录名和数据库创建者权限授予帐户。
- 若要支持重复部署，请将部署帐户登录名映射到**db\_所有者**数据库角色。

本主题将演示如何执行上述每个过程。 本主题中的任务和演练假设你开始使用在 Windows Server 2008 R2 上运行 SQL Server 2008 R2 的默认实例。 继续之前，请确保：

- Windows Server 2008 R2 Service Pack 1 和所有可用更新均已安装。
- 服务器已加入域。
- 服务器具有静态 IP 地址。
- SQL Server 2008 R2 Service Pack 1 和所有可用更新均已安装。

SQL Server 实例只需要包括**数据库引擎服务**角色，此角色会自动包含在任何 SQL Server 安装中。 但是，为了便于配置和维护，我们建议你包括**管理工具-基本**和**管理工具–完整**的服务器角色。

> [!NOTE]
> 有关将计算机加入域的详细信息，请参阅将[计算机加入到域并登录](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx)。 有关配置静态 IP 地址的详细信息，请参阅[配置静态 Ip 地址](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx)。 有关安装 SQL Server 的详细信息，请参阅[安装 SQL Server 2008 R2](https://technet.microsoft.com/library/bb500395.aspx)。

## <a name="enable-remote-access-to-sql-server"></a>启用 SQL Server 的远程访问

SQL Server 使用 TCP/IP 与远程计算机进行通信。 如果数据库服务器和 web 服务器位于不同的计算机上，则需要：

- 配置 SQL Server 网络设置，以允许通过 TCP/IP 进行通信。
- 配置任何硬件或软件防火墙以允许 TCP 流量（在某些情况下，用户数据报协议（UDP）流量）在 SQL Server 实例使用的端口上。

若要启用 SQL Server 通过 TCP/IP 进行通信，请使用 SQL Server 配置管理器更改 SQL Server 实例的网络配置。

**启用 SQL Server 以使用 TCP/IP 进行通信**

1. 在 "**开始**" 菜单上，指向 "**所有程序**"，依次单击**Microsoft SQL Server 2008 R2**"、"**配置工具**"和" **SQL Server 配置管理器**"。
2. 在 "树视图" 窗格中，展开 " **SQL Server 网络配置**"，然后单击 " **MSSQLSERVER 的协议**"。

   > [!NOTE]
   > 如果已安装 SQL Server 的多个实例，则会看到每个实例的<em>[instance name]</em>项的<strong>协议</strong>。 你需要按实例配置网络设置。
3. 在详细信息窗格中，右键单击 " **tcp/ip** " 行，然后单击 "**启用**"。

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image1.png)
4. 在**警告**对话框中，单击 **"确定"** 。

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image2.png)
5. 需要重启 MSSQLSERVER 服务，新的网络配置才能生效。 你可以在命令提示符处、从服务控制台或 SQL Server Management Studio 执行此操作。 在此过程中，您将使用 SQL Server Management Studio。
6. 关闭“SQL Server 配置管理器”。
7. 在 "**开始**" 菜单上，指向 "**所有程序**"，单击**Microsoft SQL Server 2008 R2**"，然后单击" **SQL Server Management Studio**"。
8. 在 "**连接到服务器**" 对话框的 "**服务器名称**" 框中，键入数据库服务器的名称，然后单击 "**连接**"。

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image3.png)
9. 在**对象资源管理器**窗格中，右键单击父服务器节点（例如**TESTDB1**），然后单击 "**重新启动**"。

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image4.png)
10. 在 " **Microsoft SQL Server Management Studio** " 对话框中，单击 **"是"** 。

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image5.png)
11. 重新启动服务后，关闭 SQL Server Management Studio。

若要允许通过防火墙 SQL Server 流量，首先需要知道 SQL Server 实例使用的端口。 这将取决于创建和配置 SQL Server 实例的方式：

- SQL Server 的*默认实例*侦听 TCP 端口1433上的请求（并对其做出响应）。
- 的*命名实例*SQL Server 侦听动态分配的 TCP 端口上的请求（并对其做出响应）。
- 如果启用了 SQL Server Browser 服务，则客户端可以查询 UDP 端口1434上的服务，以找出要用于特定 SQL Server 实例的 TCP 端口。 但出于安全原因，通常会禁用此服务。

假设你要使用 SQL Server 的默认实例，则需要将防火墙配置为允许流量。

| 方向 | 从端口 | 到端口 | 端口类型 |
| --- | --- | --- | --- |
| 入站 | 任意 | 1433 | TCP |
| 出站 | 1433 | 任意 | TCP |

> [!NOTE]
> 从技术上讲，客户端计算机将使用介于1024和5000之间的随机分配 TCP 端口来与 SQL Server 通信，并且可以相应地限制防火墙规则。 有关 SQL Server 端口和防火墙的详细信息，请参阅[通过防火墙与 SQL 通信所需的 tcp/ip 端口号](https://go.microsoft.com/?linkid=9805125)，以及[如何将服务器配置为侦听特定的 TCP 端口（SQL Server 配置管理器）](https://msdn.microsoft.com/library/ms177440.aspx)。

在大多数 Windows Server 环境中，你可能必须在数据库服务器上配置 Windows 防火墙。 默认情况下，除非规则明确禁止，否则 Windows 防火墙将允许所有出站流量。 若要使 web 服务器可以访问数据库，需要配置一个入站规则，该规则允许 SQL Server 实例使用的端口号上的 TCP 流量。 如果使用 SQL Server 的默认实例，则可以使用下一个过程来配置此规则。

**将 Windows 防火墙配置为允许与默认 SQL Server 实例进行通信**

1. 在数据库服务器上的 "**开始**" 菜单中，指向 "**管理工具**"，然后单击 "**具有高级安全性的 Windows 防火墙**"。
2. 在树视图窗格中单击 "**入站规则**"。

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image6.png)
3. 在 "**操作**" 窗格中的 "**入站规则**" 下，单击 "**新建规则**"。
4. 在 "新建入站规则向导" 的 "**规则类型**" 页上，选择 "**端口**"，然后单击 "**下一步**"。

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image7.png)
5. 在 "**协议和端口**" 页上，确保已选中 " **TCP** "，并在 "**特定本地端口**" 框中键入**1433**，然后单击 "**下一步**"。

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image8.png)
6. 在 "**操作**" 页上，保留 **"允许选定连接"** ，然后单击 "**下一步**"。
7. 在 "**配置文件**" 页上，选中 "**域**"，清除 "**专用**" 和 "**公用**" 复选框，然后单击 "**下一步**"。

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image9.png)
8. 在 "**名称**" 页上，为规则指定一个适当的描述性名称（例如**SQL Server 默认实例–网络访问**），然后单击 "**完成**"。

有关为 SQL Server 配置 Windows 防火墙的详细信息，尤其是在需要通过非标准或动态端口与 SQL Server 通信时，请参阅[如何：为数据库引擎访问配置 Windows 防火墙](https://technet.microsoft.com/library/ms175043.aspx)。

## <a name="configure-logins-and-database-permissions"></a>配置登录名和数据库权限

将 web 应用程序部署到 Internet Information Services （IIS）时，应用程序将使用应用程序池的标识运行。 在域环境中，应用程序池标识使用运行它们的服务器的计算机帐户来访问网络资源。 计算机帐户采用<em>[域名]</em>格式<strong>\</strong ><em>[计算机名称]</em> <strong>$</strong> &#x2014;例如， <strong>FABRIKAM\TESTWEB1 $</strong>。 若要允许 web 应用程序通过网络访问数据库，需要执行以下操作：

- 向 SQL Server 实例添加 web 服务器计算机帐户的登录名。
- 将计算机帐户登录映射到任何所需的数据库角色（通常**db\_datareader**和**db\_datawriter**）。

如果你的 web 应用程序是在服务器场中运行，而不是在单个服务器上运行，则需要对服务器场中的每个 web 服务器重复这些步骤。

> [!NOTE]
> 有关应用程序池标识和访问网络资源的详细信息，请参阅[应用程序池标识](https://go.microsoft.com/?linkid=9805123)。

可以通过多种方式来实现这些任务。 若要创建登录名，可以执行以下任一操作：

- 使用 Transact-sql 或 SQL Server Management Studio，在数据库服务器上手动创建登录名。
- 使用 Visual Studio 中的 SQL Server 2008 服务器项目创建并部署登录名。

SQL Server 登录名是服务器级对象，而不是数据库级别的对象，因此不依赖于要部署的数据库。 因此，你可以随时创建登录名，并且最简单的方法是在开始部署数据库之前，在数据库服务器上手动创建登录名。 您可以使用下一个过程在 SQL Server Management Studio 中创建登录名。

**为 web 服务器计算机帐户创建 SQL Server 登录名**

1. 在数据库服务器上的 "**开始**" 菜单上，指向 "**所有程序**"，单击**Microsoft SQL Server 2008 R2**"，然后单击" **SQL Server Management Studio**"。
2. 在 "**连接到服务器**" 对话框的 "**服务器名称**" 框中，键入数据库服务器的名称，然后单击 "**连接**"。

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image10.png)
3. 在**对象资源管理器**窗格中，右键单击 "**安全**"，指向 "**新建**"，然后单击 "**登录名**"。
4. 在 "**登录名-新建**" 对话框的 "**登录名**" 框中，键入 web 服务器计算机帐户的名称（例如， **FABRIKAM\TESTWEB1 $** ）。

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image11.png)
5. 单击“确定”。

此时，数据库服务器已准备好进行 Web 部署发布。 但是，在将计算机帐户登录名映射到所需的数据库角色之前，你部署的任何解决方案都将不起作用。 将登录名映射到数据库角色需要更多的想法，因为在部署数据库之前无法映射角色。 若要将计算机帐户登录名映射到所需的数据库角色，可以执行以下任一操作：

- 首次部署数据库后，手动将数据库角色分配给登录名。
- 使用后期部署脚本将数据库角色分配给登录名。

有关自动创建登录名和数据库角色映射的详细信息，请参阅[将数据库角色成员身份部署到测试环境](../advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments.md)。 或者，您可以使用下一个过程将计算机帐户登录名手动映射到所需的数据库角色。 请记住，在部署数据库*之后*，才能执行此过程。

**将数据库角色映射到 web 服务器计算机帐户登录名**

1. 像以前一样打开 SQL Server Management Studio。
2. 在**对象资源管理器**窗格中，展开 "**安全**" 节点，展开 "**登录名**" 节点，然后双击计算机帐户登录（例如**FABRIKAM\TESTWEB1 $** ）。

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image12.png)
3. 在 "**登录属性**" 对话框中，单击 "**用户映射**"。
4. 在 "**映射到此登录名的用户**" 表中，选择数据库的名称（例如， **ContactManager**）。
5. 在 "**数据库角色成员身份：** *[数据库名称]* " 列表中，选择所需权限。 对于 "联系人管理器" 示例解决方案，您必须选择**db\_datareader**和**db\_datawriter**角色。

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image13.png)
6. 单击“确定”。

尽管手动映射数据库角色通常更适合测试环境，但对于过渡环境或生产环境的自动或一键式部署而言，这种做法并不理想。 你可以在[将数据库角色成员身份部署到测试环境](../advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments.md)中，了解有关使用后期部署脚本自动执行此类任务的详细信息。

> [!NOTE]
> 有关服务器项目和数据库项目的详细信息，请参阅[Visual Studio 2010 SQL Server 数据库项目](https://msdn.microsoft.com/library/ff678491.aspx)。

## <a name="configure-permissions-for-the-deployment-account"></a>配置部署帐户的权限

如果用于运行部署的帐户不是 SQL Server 管理员，则还需要为此帐户创建一个登录名。 若要创建数据库，该帐户必须是**dbcreator**服务器角色的成员或具有同等权限。

> [!NOTE]
> 使用 Web 部署或 VSDBCMD 部署数据库时，可以使用 Windows 凭据或 SQL Server 凭据（如果 SQL Server 实例配置为支持混合模式身份验证）。 下一个过程假定您要使用 Windows 凭据，但在配置部署时，不会阻止您在连接字符串中指定 SQL Server 用户名和密码。

**设置部署帐户的权限**

1. 像以前一样打开 SQL Server Management Studio。
2. 在**对象资源管理器**窗格中，右键单击 "**安全**"，指向 "**新建**"，然后单击 "**登录名**"。
3. 在 "**登录名-新建**" 对话框的 "**登录名**" 框中，键入部署帐户的名称（例如， **FABRIKAM\matt**）。
4. 在 "**选择页**" 窗格中，单击 "**服务器角色**"。
5. 选择 " **dbcreator**"，然后单击 **"确定"** 。

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image14.png)

若要支持后续部署，还需要在第一次部署后将部署帐户添加到数据库上的**db\_所有者**角色。 这是因为，在后续部署中，你要修改现有数据库的架构，而不是创建新数据库。 如前一部分中所述，在创建数据库之前，您无法将用户添加到数据库角色，原因很明显。

**将部署帐户登录名映射到 db\_所有者数据库角色**

1. 像以前一样打开 SQL Server Management Studio。
2. 在 "**对象资源管理器**" 窗口中，展开 "**安全**" 节点，展开 "**登录名**" 节点，然后双击计算机帐户登录（例如**FABRIKAM\matt**）。
3. 在 "**登录属性**" 对话框中，单击 "**用户映射**"。
4. 在 "**映射到此登录名的用户**" 表中，选择数据库的名称（例如， **ContactManager**）。
5. 在 "**数据库角色成员身份：** *[数据库名称]* " 列表中，选择 " **db\_所有者**" 角色。

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image15.png)
6. 单击“确定”。

## <a name="conclusion"></a>结束语

你的数据库服务器现在应已准备好接受远程数据库部署，并允许远程 IIS web 服务器访问你的数据库。 在尝试部署和使用数据库之前，您可能需要检查以下要点：

- 是否已将 SQL Server 配置为接受远程 TCP/IP 连接？
- 是否已将任何防火墙配置为允许 SQL Server 流量？
- 是否为将访问 SQL Server 的每个 web 服务器都创建了计算机帐户登录名？
- 您的数据库部署是否包含用于创建用户角色映射的脚本，或者您是否需要在第一次部署数据库后手动创建这些映射？
- 是否创建了部署帐户的登录名并将其添加到了**dbcreator**服务器角色？

## <a name="further-reading"></a>其他阅读材料

有关部署数据库项目的指南，请参阅[部署数据库项目](../web-deployment-in-the-enterprise/deploying-database-projects.md)。 有关通过运行后期部署脚本创建数据库角色成员身份的指南，请参阅[将数据库角色成员身份部署到测试环境](../advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments.md)。 有关如何满足成员资格数据库所带来的独特部署挑战的指导，请参阅[将成员资格数据库部署到企业环境](../advanced-enterprise-web-deployment/deploying-membership-databases-to-enterprise-environments.md)。

> [!div class="step-by-step"]
> [上一页](configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)
> [下一页](creating-a-server-farm-with-the-web-farm-framework.md)

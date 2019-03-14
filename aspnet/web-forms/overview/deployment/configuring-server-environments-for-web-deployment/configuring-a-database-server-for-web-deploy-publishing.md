---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-database-server-for-web-deploy-publishing
title: 配置数据库服务器的 Web 部署发布 |Microsoft Docs
author: jrjlee
description: 本主题介绍如何配置 SQL Server 2008 R2 数据库服务器以支持 web 部署和发布。 本主题中所述的任务是共同...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: e7c447f9-eddf-4bbe-9f18-3326d965d093
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-database-server-for-web-deploy-publishing
msc.type: authoredcontent
ms.openlocfilehash: 0f8639efcfcd02c9fdb65ce3ed25272965be8aa8
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57031694"
---
<a name="configuring-a-database-server-for-web-deploy-publishing"></a>配置用于 Web 部署发布的数据库服务器
====================
通过[Jason Lee](https://github.com/jrjlee)

[下载 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主题介绍如何配置 SQL Server 2008 R2 数据库服务器以支持 web 部署和发布。
> 
> 本主题中所述的任务是普遍适用于每个部署方案&#x2014;是否在 web 服务器配置为使用 IIS Web 部署工具 （Web 部署） 的远程代理服务、 Web 部署处理程序或离线部署并不重要或你的应用程序在单个 web 服务器或服务器场上运行。 部署数据库的方式根据安全要求和其他注意事项可能会更改。 例如，可能会部署数据库有或没有示例数据，并可能会部署用户角色映射或部署后手动配置它们。 但是，配置数据库服务器的方式保持不变。


您无需安装任何其他产品或工具到配置数据库服务器以支持 web 部署。 假设你的数据库服务器和 web 服务器在不同计算机上运行，您只需要：

- 允许 SQL Server 使用 TCP/IP 进行通信。
- 允许通过任何防火墙的 SQL Server 通信。
- 为 web 服务器计算机帐户提供的 SQL Server 登录名。
- 将计算机帐户登录名映射到任何所需的数据库角色。
- 提供将运行部署 SQL Server 登录名和数据库创建者权限的帐户。
- 若要支持重复部署，部署帐户的登录名映射到**db\_所有者**数据库角色。

本主题将演示如何执行每个这些过程。 任务和本主题中的演练假定您正在使用 Windows Server 2008 R2 上运行的 SQL Server 2008 R2 的默认实例。 在继续之前，请确保：

- 安装 Windows Server 2008 R2 Service Pack 1 和所有可用的更新。
- 服务器已加入域。
- 在服务器具有静态 IP 地址。
- 安装 SQL Server 2008 R2 Service Pack 1 和所有可用的更新。

SQL Server 实例只需要包括**数据库引擎服务**角色，它会自动包含在任何 SQL Server 安装。 但是，为了方便配置和维护，我们建议您包括**管理工具-Basic**并**管理工具-完整**服务器角色。

> [!NOTE]
> 有关将计算机加入到域的详细信息，请参阅[将计算机加入到域并登录](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx)。 有关配置静态 IP 地址的详细信息，请参阅[配置静态 IP 地址](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx)。 有关安装 SQL Server 的详细信息，请参阅[安装 SQL Server 2008 R2](https://technet.microsoft.com/library/bb500395.aspx)。


## <a name="enable-remote-access-to-sql-server"></a>启用对 SQL Server 的远程访问

SQL Server 使用 TCP/IP 与远程计算机进行通信。 如果你的数据库服务器和 web 服务器位于不同的计算机上，你需要：

- 配置 SQL Server 网络设置，以允许 TCP/IP 上的通信。
- 配置任何硬件或软件的防火墙允许 TCP 流量 （并在某些情况下用户数据报协议 (UDP) 流量） 上的 SQL Server 实例使用的端口。

若要启用 SQL Server 通过 TCP/IP 进行通信，请使用 SQL Server 配置管理器来更改您的 SQL Server 实例的网络配置。

**若要启用 SQL Server 通信使用 TCP/IP**

1. 上**启动**菜单，依次指向**所有程序**，单击**Microsoft SQL Server 2008 R2**，单击**配置工具**，然后单击**SQL Server 配置管理器**。
2. 在树视图窗格中，展开**SQL Server 网络配置**，然后单击**MSSQLSERVER 的协议**。

   > [!NOTE]
   > 如果已安装 SQL Server 的多个实例，则会看到<strong>协议</strong><em>[实例名称]</em>每个实例的项。 您需要配置网络设置基于实例的实例。
3. 在细节窗格中，右键单击**TCP/IP**行，然后依次**启用**。

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image1.png)
4. 在中**警告**对话框中，单击**确定**。

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image2.png)
5. 您需要重新启动 MSSQLSERVER 服务，新的网络配置才能生效。 您可以实现在命令提示符下，从服务控制台中，或从 SQL Server Management Studio。 在此过程中，将使用 SQL Server Management Studio。
6. 关闭 SQL Server 配置管理器。
7. 上**启动**菜单，依次指向**所有程序**，单击**Microsoft SQL Server 2008 R2**，然后单击**SQL Server Management Studio**。
8. 在中**连接到服务器**对话框中**服务器名称**框中，键入数据库服务器的名称，然后单击**Connect**。

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image3.png)
9. 在中**对象资源管理器**窗格中，右键单击父服务器节点 (例如， **TESTDB1**)，然后单击**重启**。

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image4.png)
10. 在中**Microsoft SQL Server Management Studio**对话框中，单击**是**。

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image5.png)
11. 已重新启动该服务，关闭 SQL Server Management Studio。

若要允许 SQL Server 通信通过防火墙，首先需要知道您的 SQL Server 实例所使用的端口。 这将取决于如何创建和配置 SQL Server 实例是：

- 一个*默认实例*的 SQL Server 侦听的 （和响应） TCP 端口 1433年上的请求。
- 一个*命名实例*的 SQL Server 侦听的 （和响应） 动态分配的 TCP 端口上的请求。
- 如果启用了 SQL Server Browser 服务，客户端可以查询查找要用于特定的 SQL Server 实例的 TCP 端口 1434 号 UDP 端口上的服务。 但是，此服务通常会出于安全原因被禁用。

假设您正在使用的 SQL Server 默认实例，需要将防火墙配置为允许流量。

| 方向 | 从端口 | 到端口 | 端口类型 |
| --- | --- | --- | --- |
| 入站 | 任意 | 1433 | TCP |
| 出站 | 1433 | 任意 | TCP |
  

> [!NOTE]
> 从技术上讲，客户端计算机将使用 1024年和 5000 之间随机分配的 TCP 端口与 SQL Server 进行通信，你可以相应地限制防火墙规则。 SQL Server 端口和防火墙的详细信息，请参阅[通过防火墙向 SQL 通信所需的 TCP/IP 端口号](https://go.microsoft.com/?linkid=9805125)和[如何：配置服务器以侦听特定 TCP 端口 （SQL Server 配置管理器）](https://msdn.microsoft.com/library/ms177440.aspx)。


在大多数 Windows Server 环境中，您可能需要在数据库服务器上配置 Windows 防火墙。 默认情况下，Windows 防火墙允许所有出站流量，除非规则专门禁止它。 若要启用 web 服务器，以访问您的数据库，您需要配置 SQL Server 实例使用的端口号允许 TCP 流量的入站的规则。 如果您使用 SQL Server 的默认实例，可以使用下一个过程来配置此规则。

**若要配置 Windows 防火墙以允许使用的默认 SQL Server 实例的通信**

1. 在数据库服务器上，在**启动**菜单，依次指向**管理工具**，然后单击**高级安全 Windows 防火墙**。
2. 在树视图窗格中，单击**入站规则**。

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image6.png)
3. 在中**操作**窗格下**入站规则**，单击**新规则**。
4. 在新入站规则向导中，在**规则类型**页上，选择**端口**，然后单击**下一步**。

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image7.png)
5. 上**协议和端口**页上，确保**TCP**已选中，然后在**特定本地端口**框中，键入**1433年**，然后单击**下一步**。

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image8.png)
6. 上**操作**页上，保留**允许连接**选中然后单击**下一步**。
7. 上**配置文件**页上，保留**域**选择，清除**专用**并**公共**复选框，然后依次**下一步**。

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image9.png)
8. 上**名称**页上，为规则指定适当的描述性名称 (例如， **SQL Server 默认实例 – 网络访问权限**)，然后单击**完成**。

有关详细信息为 SQL Server，配置 Windows 防火墙，尤其是如果你需要与 SQL Server 通信通过非标准的或动态端口，请参阅[如何：为数据库引擎访问配置 Windows 防火墙](https://technet.microsoft.com/library/ms175043.aspx)。

## <a name="configure-logins-and-database-permissions"></a>配置登录名和数据库权限

在部署 web 应用程序到 Internet 信息服务 (IIS) 时，应用程序使用的应用程序池标识运行。 在域环境中，应用程序池标识使用来访问网络资源在其的运行的服务器的计算机帐户。 计算机帐户需要在窗体<em>[域名]</em><strong>\</ s ><em>[machine name]</em><strong>$</strong>&#x2014;等<strong>FABRIKAM\TESTWEB1$</strong>。 若要允许 web 应用程序通过网络访问数据库，需要：

- 将 web 服务器计算机帐户的登录名添加到 SQL Server 实例。
- 将计算机帐户登录名映射到任何所需的数据库角色 (通常**db\_datareader**并**db\_datawriter**)。

如果服务器场中，而不是一台服务器上运行 web 应用程序，您需要在服务器场中每个 web 服务器重复这些步骤。

> [!NOTE]
> 应用程序池标识和访问网络资源的详细信息，请参阅[应用程序池标识](https://go.microsoft.com/?linkid=9805123)。


可以用来处理这些任务以各种方式。 若要创建登录名，您可以：

- 使用 TRANSACT-SQL 或 SQL Server Management Studio 在数据库服务器上手动创建登录名。
- 使用 SQL Server 2008 Server 项目在 Visual Studio 中创建和部署该登录名。

SQL Server 登录名是服务器级对象，而不是数据库级别对象，因此不依赖于你想要部署的数据库。 在这种情况下，可以在任何时候，创建登录名和最简单的方法通常是登录名之前手动创建数据库服务器上开始部署数据库。 下一步过程可用于在 SQL Server Management Studio 中创建一个登录名。

**创建 web 服务器计算机帐户的 SQL Server 登录名**

1. 在数据库服务器上，在**启动**菜单，依次指向**所有程序**，单击**Microsoft SQL Server 2008 R2**，然后单击**SQL Server Management Studio**.
2. 在中**连接到服务器**对话框中**服务器名称**框中，键入数据库服务器的名称，然后单击**Connect**。

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image10.png)
3. 在中**对象资源管理器**窗格中，右键单击**安全**，指向**新建**，然后单击**登录**。
4. 在中**登录名-新建**对话框中**登录名**框中，键入您的 web 服务器计算机帐户的名称 (例如， **FABRIKAM\TESTWEB1$**)。

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image11.png)
5. 单击 **“确定”**。

此时，你的数据库服务器是可供 Web 部署发布。 但是，在部署任何解决方案不起作用之前将计算机帐户登录名映射到所需的数据库角色。 将登录名映射到数据库角色需要更加认为很多，作为您不能映射到后已部署角色数据库。 若要将计算机帐户登录名映射到所需的数据库角色，您可以：

- 数据库角色对该登录名手动分配后首次部署该数据库。
- 后期部署脚本用于将数据库角色分配给该登录名。

自动创建登录名和数据库角色映射的详细信息，请参阅[到测试环境中部署数据库角色成员](../advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments.md)。 或者，可以使用下一个过程来手动将计算机帐户登录名映射到所需的数据库角色。 请记住，无法执行此过程直至*后*已部署数据库。

**将数据库角色映射到 web 服务器计算机帐户登录名**

1. 像以前一样打开 SQL Server Management Studio。
2. 在中**对象资源管理器**窗格中，展开**安全**节点，展开**登录名**节点，然后双击计算机帐户登录名 (例如， **FABRIKAM\TESTWEB1$**)。

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image12.png)
3. 在中**登录名属性**对话框中，单击**用户映射**。
4. 在中**映射到此登录名的用户**表中，选择你的数据库的名称 (例如， **ContactManager**)。
5. 在**数据库角色成员身份：** *[数据库名称]* 列表中，选择所需的权限。 在联系人管理器示例解决方案中，您必须选择**db\_datareader**并**db\_datawriter**角色。

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image13.png)
6. 单击 **“确定”**。

虽然手动映射数据库角色通常是多个适合测试环境，它不太可取为自动或一键式部署到过渡或生产环境。 你可以找到自动进行这种类型的使用中的后期部署脚本的任务的详细信息[到测试环境中部署数据库角色成员](../advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments.md)。

> [!NOTE]
> 服务器项目和数据库项目的详细信息，请参阅[Visual Studio 2010 SQL Server 数据库项目](https://msdn.microsoft.com/library/ff678491.aspx)。


## <a name="configure-permissions-for-the-deployment-account"></a>配置部署帐户的权限

如果将用于运行部署的帐户不是 SQL Server 管理员，还需要创建此帐户的登录名。 若要创建数据库，帐户必须隶属**dbcreator**服务器角色或具有同等权限。

> [!NOTE]
> 当您使用 Web 部署或 VSDBCMD 将数据库部署时，你可以使用 Windows 凭据或 SQL Server 凭据，（如果您的 SQL Server 实例配置为支持混合的模式身份验证）。 下一步的过程假设你想要使用 Windows 凭据，但没有什么措施可以阻止您从时将部署配置为在连接字符串中指定的 SQL Server 用户名和密码。


**若要设置部署帐户的访问权限**

1. 像以前一样打开 SQL Server Management Studio。
2. 在中**对象资源管理器**窗格中，右键单击**安全**，指向**新建**，然后单击**登录**。
3. 在中**登录名-新建**对话框中**登录名**框中，键入部署帐户的名称 (例如， **FABRIKAM\matt**)。
4. 在中**选择页**窗格中，单击**服务器角色**。
5. 选择**dbcreator**，然后单击**确定**。

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image14.png)

若要支持后续部署，您还需要部署将帐户添加到**db\_所有者**上第一次部署后的数据库角色。 这是因为在后续部署上您正在修改的现有数据库架构而不是创建新的数据库。 如前一部分中所述，无法将用户添加到数据库角色，直到已创建数据库，出于显而易见的原因。

**若要部署帐户登录名映射到 db\_所有者数据库角色**

1. 像以前一样打开 SQL Server Management Studio。
2. 在中**对象资源管理器**窗口中，展开**安全**节点，展开**登录名**节点，然后双击计算机帐户登录名 (例如， **FABRIKAM\matt**)。
3. 在中**登录名属性**对话框中，单击**用户映射**。
4. 在中**映射到此登录名的用户**表中，选择你的数据库的名称 (例如， **ContactManager**)。
5. 在**数据库角色成员身份：** *[数据库名称]* 列表中，选择**db\_所有者**角色。

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image15.png)
6. 单击 **“确定”**。

## <a name="conclusion"></a>结束语

你的数据库服务器现在应该准备好接受远程数据库部署并允许远程 IIS web 服务器以访问您的数据库。 在尝试部署和使用数据库之前，你可能想要检查这些关键点：

- 已配置为接受远程 TCP/IP 连接的 SQL Server 吗？
- 已配置任何防火墙以允许 SQL Server 流量吗？
- 您是否已将访问 SQL Server 的每个 web 服务器的计算机帐户登录？
- 您的数据库部署是否包括一个脚本来创建用户角色映射，或您需要在首次部署数据库后手动创建这些？
- 你已创建部署帐户的登录名并添加到**dbcreator**服务器角色？

## <a name="further-reading"></a>其他阅读材料

有关部署数据库项目的指导，请参阅[部署数据库项目](../web-deployment-in-the-enterprise/deploying-database-projects.md)。 通过运行后期部署脚本创建数据库角色成员身份的指导，请参阅[到测试环境中部署数据库角色成员](../advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments.md)。 有关如何满足成员资格数据库造成的唯一的部署困难的指导，请参阅[的成员资格数据库部署到企业环境](../advanced-enterprise-web-deployment/deploying-membership-databases-to-enterprise-environments.md)。

> [!div class="step-by-step"]
> [上一页](configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)
> [下一页](creating-a-server-farm-with-the-web-farm-framework.md)

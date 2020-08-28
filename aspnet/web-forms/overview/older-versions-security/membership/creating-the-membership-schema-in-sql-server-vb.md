---
uid: web-forms/overview/older-versions-security/membership/creating-the-membership-schema-in-sql-server-vb
title: 在 SQL Server (VB) 创建成员身份架构 |Microsoft Docs
author: rick-anderson
description: 本教程首先检查将必要的架构添加到数据库的方法，以便使用 SqlMembershipProvider。 接下来，我们将
ms.author: riande
ms.date: 01/18/2008
ms.assetid: 112a674d-716f-41a6-99b8-4074d65a54c0
msc.legacyurl: /web-forms/overview/older-versions-security/membership/creating-the-membership-schema-in-sql-server-vb
msc.type: authoredcontent
ms.openlocfilehash: 3596e85f6f1e36e046011212479128229be24201
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045073"
---
# <a name="creating-the-membership-schema-in-sql-server-vb"></a>在 SQL Server 中创建成员身份架构 (VB)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/ASPNET_Security_Tutorial_04_VB.zip) 或 [下载 PDF](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/aspnet_tutorial04_MembershipSetup_vb.pdf)

> 本教程首先检查将必要的架构添加到数据库的方法，以便使用 SqlMembershipProvider。 接下来，我们将检查架构中的关键表并讨论其用途和重要性。 本教程将介绍如何判断成员身份框架应使用的 ASP.NET 应用程序。

## <a name="introduction"></a>简介

前面的两个教程使用窗体身份验证来识别网站访问者。 利用 forms 身份验证框架，开发人员可以轻松地将用户登录到网站，并通过使用身份验证票证在页面访问中记住他们。 `FormsAuthentication`类包含用于生成票证并将其添加到访问者 cookie 的方法。 会 `FormsAuthenticationModule` 检查所有传入请求，对于具有有效身份验证票证的请求，将创建一个对象并将其 `GenericPrincipal` `FormsIdentity` 与当前请求相关联。 Forms 身份验证只是一种机制，用于在登录时向访问者授予身份验证票证，并在后续请求中对该票证进行分析，以确定用户的身份。 对于支持用户帐户的 web 应用程序，我们仍需要实现一个用户存储并添加功能来验证凭据、注册新用户以及其他许多与用户帐户相关的任务。

在 ASP.NET 2.0 之前，开发人员处于挂钩上，用于实现所有与用户帐户相关的任务。 幸运的是，ASP.NET 团队认识到了这种缺点，并引入了 ASP.NET 2.0 的成员身份框架。 成员身份框架是 .NET Framework 中的一组类，这些类提供用于完成与核心用户帐户相关的任务的编程接口。 此框架是在 [提供程序模型](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx)的顶层构建的，使开发人员能够将自定义的实现插入到标准化的 API 中。

如 <a id="Tutorial1"></a> [*安全基础和 ASP.NET 支持*](../introduction/security-basics-and-asp-net-support-vb.md)教程中所述，.NET Framework 附带了两个内置成员资格提供程序： [`ActiveDirectoryMembershipProvider`](https://msdn.microsoft.com/library/system.web.security.activedirectorymembershipprovider.aspx) 和 [`SqlMembershipProvider`](https://msdn.microsoft.com/library/system.web.security.sqlmembershipprovider.aspx) 。 顾名思义， `SqlMembershipProvider` 使用 Microsoft SQL Server 数据库作为用户存储区。 为了在应用程序中使用此提供程序，我们需要告知提供程序要用作存储的数据库。 如您所料， `SqlMembershipProvider` 要求用户存储数据库包含某些数据库表、视图和存储过程。 需要将此预期的架构添加到所选数据库。

本教程首先检查将必要的架构添加到数据库的方法，以便使用 `SqlMembershipProvider` 。 接下来，我们将检查架构中的关键表并讨论其用途和重要性。 本教程将介绍如何判断成员身份框架应使用的 ASP.NET 应用程序。

让我们开始吧！

## <a name="step-1-deciding-where-to-place-the-user-store"></a>步骤1：确定将用户存储放置在何处

ASP.NET 应用程序的数据通常存储在数据库的多个表中。 实现 `SqlMembershipProvider` 数据库架构时，必须决定是将成员身份架构放在与应用程序数据相同的数据库中，还是放置在备用数据库中。

建议在与应用程序数据相同的数据库中查找成员身份架构，原因如下：

- 可**维护性**：其中的数据封装在一个数据库中的应用程序比具有两个独立数据库的应用程序更易于理解、维护和部署。
- **关系完整性**  ：通过在与应用程序表相同的数据库中查找与成员相关的表，可以在与成员相关的表和相关的应用程序表中的主键之间建立 [外键约束](http://en.wikipedia.org/wiki/Foreign_key) 。

如果你有多个应用程序，而每个应用程序都使用不同的数据库，但需要共享一个公共用户存储，那么仅当你有多个应用程序时，将用户存储和应用程序数据分离

### <a name="creating-a-database"></a>创建数据库

在第二个教程中，我们已生成的应用程序尚未需要数据库。 但是，我们现在需要为用户存储提供一个。 让我们创建一个架构，然后向其添加提供程序所需的架构 `SqlMembershipProvider` (参见步骤 2) 。

> [!NOTE]
> 在本系列教程中，我们将使用 [Microsoft SQL Server 2005 Express Edition](https://msdn.microsoft.com/sql/Aa336346.aspx) 数据库来存储应用程序表和 `SqlMembershipProvider` 架构。 由于以下两个原因导致了此决定：第一种情况是因为其成本免费-Express Edition 是 SQL Server 2005 的最 readably 的可访问版本;其次，SQL Server 2005 Express Edition 数据库可以直接放置在 web 应用程序的 `App_Data` 文件夹中，因此 cinch 将数据库和 web 应用程序打包到一个 ZIP 文件中，并在不使用任何特殊设置说明或配置选项的情况下重新部署它。 如果希望继续使用 SQL Server 的非速成版版本，请随时免费。 步骤几乎完全相同。 此 `SqlMembershipProvider` 架构将适用于任何版本的 Microsoft SQL Server 2000 和更高版本。

在解决方案资源管理器中，右键单击该 `App_Data` 文件夹并选择 "添加新项"。  (如果未在项目中看到 `App_Data` 文件夹，请在解决方案资源管理器中右键单击该项目，选择 "添加 ASP.NET 文件夹"， `App_Data` ) 然后从 "添加新项" 对话框中选择添加一个名为的新 SQL 数据库 `SecurityTutorials.mdf` 。 在本教程中，我们将向 `SqlMembershipProvider` 此数据库添加架构; 在后续教程中，我们将创建其他表来捕获应用程序数据。

[![将名为 SecurityTutorials 的新 SQL 数据库添加到 App_Data 文件夹](creating-the-membership-schema-in-sql-server-vb/_static/image2.png)](creating-the-membership-schema-in-sql-server-vb/_static/image1.png)

**图 1**：向文件夹添加新的 SQL 数据库命名 `SecurityTutorials.mdf` 数据库 `App_Data` ([单击查看全尺寸图像](creating-the-membership-schema-in-sql-server-vb/_static/image3.png)) 

将数据库添加到该 `App_Data` 文件夹会将其自动包含在数据库资源管理器视图中。 在 Visual Studio 的非 Express 版本中 (，数据库资源管理器称为 "服务器资源管理器"。 ) 中转到数据库资源管理器并展开 "仅添加 `SecurityTutorials` 数据库"。 如果在屏幕上看不到 "数据库资源管理器"，请单击 "查看" 菜单，然后选择 "数据库资源管理器" 或按 Ctrl + Alt + S。 如图2所示， `SecurityTutorials` 数据库为空-它不包含任何表、视图和存储过程。

[![SecurityTutorials 数据库当前为空](creating-the-membership-schema-in-sql-server-vb/_static/image5.png)](creating-the-membership-schema-in-sql-server-vb/_static/image4.png)

**图 2**： `SecurityTutorials` 数据库当前为空 ([单击查看全尺寸图像](creating-the-membership-schema-in-sql-server-vb/_static/image6.png)) 

## <a name="step-2-adding-thesqlmembershipproviderschema-to-the-database"></a>步骤2：向 `SqlMembershipProvider` 数据库添加架构

`SqlMembershipProvider`需要在用户存储数据库中安装一组特定的表、视图和存储过程。 可以使用[ `aspnet_regsql.exe` 工具](https://msdn.microsoft.com/library/ms229862.aspx)添加这些必需的数据库对象。 此文件位于 `%WINDIR%\Microsoft.Net\Framework\v2.0.50727\` 文件夹中。

> [!NOTE]
> 该 `aspnet_regsql.exe` 工具提供了命令行功能和图形用户界面。 图形界面更易于用户理解，在本教程中我们将对此进行介绍。 如果添加架构需要自动执行，则命令行接口非常有用 `SqlMembershipProvider` ，例如在生成脚本或自动测试方案中。

该 `aspnet_regsql.exe` 工具用于在指定的 SQL Server 数据库中添加或删除 *ASP.NET 应用程序服务* 。 ASP.NET 应用程序服务包含和的架构 `SqlMembershipProvider` ，以及 `SqlRoleProvider` 适用于其他 ASP.NET 2.0 框架的基于 SQL 的提供程序的架构。 我们需要为该工具提供两位信息 `aspnet_regsql.exe` ：

- 是要添加还是删除应用程序服务，以及
- 要从中添加或删除应用程序服务架构的数据库

在提示数据库使用的情况下，该 `aspnet_regsql.exe` 工具将要求我们提供数据库所在的服务器的名称、用于连接到数据库的安全凭据以及数据库名称。 如果你使用的是非 Express 版本的 SQL Server，则应该已经知道此信息，因为它是你在通过 ASP.NET 网页使用数据库时必须通过连接字符串提供的相同信息。 但是，在使用文件夹中的 SQL Server 2005 Express Edition 数据库时，确定服务器和数据库名称 `App_Data` 更多。

以下部分介绍了在文件夹中指定 SQL Server 2005 Express Edition 数据库的服务器名称和数据库名称的一种简单方法 `App_Data` 。 如果使用的不是 SQL Server 2005 Express Edition 请随意跳到安装应用程序服务部分。

### <a name="determining-the-server-and-database-name-for-a-sql-server-2005-express-edition-database-in-theapp_datafolder"></a>确定文件夹中 SQL Server 2005 Express Edition 数据库的服务器和数据库名称 `App_Data`

为了使用该工具， `aspnet_regsql.exe` 我们需要知道服务器和数据库的名称。 服务器名称为 `localhost\InstanceName` 。 最可能的 *实例* 名称为 `SQLExpress` 。 但是，如果手动安装了 SQL Server 2005 Express Edition (即，安装 Visual Studio) 时未自动安装它，则可能是你选择了不同的实例名称。

确定数据库名称有点棘手。 文件夹中的数据库 `App_Data` 通常具有数据库名称，其中包含 [全局唯一标识符](http://en.wikipedia.org/wiki/Globally_Unique_Identifier) 以及数据库文件的路径。 为了通过添加应用程序服务架构，我们需要确定此数据库名称 `aspnet_regsql.exe` 。

确定数据库名称的最简单方法是通过 SQL Server Management Studio 来检查数据库名称。 SQL Server Management Studio 提供了一个图形界面用于管理 SQL Server 2005 数据库，但它不附带 SQL Server 2005 的 Express 版本。 好消息是， [你可以下载](https://www.microsoft.com/downloads/details.aspx?FamilyId=C243A5AE-4BD1-4E3D-94B8-5A0F62BF7796&amp;displaylang=en) SQL Server Management Studio 的免费 Express 版。

> [!NOTE]
> 如果你的桌面上还安装了非 Express Edition 版本的 SQL Server 2005，则可能会安装 Management Studio 的完整版本。 您可以使用完整版本来确定数据库名称，遵循的步骤与学习版中所述的步骤相同。

首先关闭 Visual Studio，以确保已关闭 Visual Studio 在数据库文件上施加的任何锁。 接下来，启动 SQL Server Management Studio 并连接到用于 `localhost\InstanceName` SQL Server 2005 Express Edition 的数据库。 如前文所述，实例名称可能是 `SQLExpress` 。 对于 "身份验证" 选项，请选择 "Windows 身份验证"。

[![连接到 SQL Server 2005 Express Edition 实例](creating-the-membership-schema-in-sql-server-vb/_static/image8.png)](creating-the-membership-schema-in-sql-server-vb/_static/image7.png)

**图 3**：连接到 SQL Server 2005 Express Edition 实例 ([单击查看完全大小的图像](creating-the-membership-schema-in-sql-server-vb/_static/image9.png)) 

连接到 SQL Server 2005 Express Edition 实例后，Management Studio 显示数据库、安全设置、服务器对象等文件夹。 如果你展开 "数据库" 选项卡，你将看到 `SecurityTutorials.mdf` 数据库 *未* 在数据库实例中注册-我们需要首先附加数据库。

右键单击 "数据库" 文件夹，然后从上下文菜单中选择 "附加"。 这将显示 "附加数据库" 对话框。 在此处单击 "添加" 按钮，浏览到该 `SecurityTutorials.mdf` 数据库，然后单击 "确定"。 图4显示了在选择数据库后 "附加数据库" 对话框 `SecurityTutorials.mdf` 。 图5显示了成功附加数据库后 Management Studio 对象资源管理器。

[![附加 SecurityTutorials 数据库](creating-the-membership-schema-in-sql-server-vb/_static/image11.png)](creating-the-membership-schema-in-sql-server-vb/_static/image10.png)

**图 4**：附加 `SecurityTutorials.mdf` 数据库 ([单击查看完全大小的图像](creating-the-membership-schema-in-sql-server-vb/_static/image12.png)) 

[![SecurityTutorials 数据库显示在 "数据库" 文件夹中](creating-the-membership-schema-in-sql-server-vb/_static/image14.png)](creating-the-membership-schema-in-sql-server-vb/_static/image13.png)

**图 5**： `SecurityTutorials.mdf` 数据库显示在 "数据库" 文件夹中 ([单击查看全尺寸图像](creating-the-membership-schema-in-sql-server-vb/_static/image15.png)) 

如图5所示， `SecurityTutorials.mdf` 数据库有一个 abstruse 的名称。 让我们将其更改为更容易记忆的 (并且更易于键入) 名称。 右键单击该数据库，从上下文菜单中选择 "重命名"，然后将其重命名 `SecurityTutorialsDatabase` 。 这不会更改文件名，而只会更改数据库用来标识自身 SQL Server 的名称。

[![将数据库重命名为 SecurityTutorialsDatabase](creating-the-membership-schema-in-sql-server-vb/_static/image17.png)](creating-the-membership-schema-in-sql-server-vb/_static/image16.png)

**图 6**：将数据库重命名为 `SecurityTutorialsDatabase` ([单击查看全尺寸图像](creating-the-membership-schema-in-sql-server-vb/_static/image18.png)) 

此时，我们知道数据库文件的服务器和数据库名称 `SecurityTutorials.mdf` ： `localhost\InstanceName` 和 `SecurityTutorialsDatabase` 。 现在，我们可以通过工具安装应用程序服务了 `aspnet_regsql.exe` 。

### <a name="installing-the-application-services"></a>安装应用程序服务

若要启动该 `aspnet_regsql.exe` 工具，请在 "开始" 菜单中选择 "运行"。 `%WINDIR%\Microsoft.Net\Framework\v2.0.50727\aspnet_regsql.exe`在文本框中输入，然后单击 "确定"。 或者，您可以使用 Windows 资源管理器向下钻取到相应的文件夹，然后双击该 `aspnet_regsql.exe` 文件。 这两种方法都将产生相同的结果。

在 `aspnet_regsql.exe` 没有任何命令行参数的情况下运行此工具将启动 ASP.NET SQL Server 安装向导图形用户界面。 使用该向导，可以轻松地在指定的数据库上添加或删除 ASP.NET 应用程序服务。 向导的第一个屏幕（如图7所示）描述了该工具的用途。

[![使用 ASP.NET SQL Server 安装向导来添加成员身份架构](creating-the-membership-schema-in-sql-server-vb/_static/image20.png)](creating-the-membership-schema-in-sql-server-vb/_static/image19.png)

**图 7**：使用 ASP.NET SQL Server 安装向导来添加成员身份架构 ([单击查看完全大小的映像](creating-the-membership-schema-in-sql-server-vb/_static/image21.png)) 

向导中的第二个步骤询问我们是否要添加应用程序服务或删除它们。 由于我们要添加所需的表、视图和存储过程 `SqlMembershipProvider` ，请选择 "为应用程序服务配置 SQL Server" 选项。 稍后，如果要从数据库中删除此架构，请重新运行此向导，而不是选择 "从现有数据库中删除应用程序服务信息" 选项。

[![选择 "为应用程序服务配置 SQL Server" 选项](creating-the-membership-schema-in-sql-server-vb/_static/image23.png)](creating-the-membership-schema-in-sql-server-vb/_static/image22.png)

**图 8**：选择 "为应用程序服务配置 SQL Server" 选项 ([单击以查看完全大小的图像](creating-the-membership-schema-in-sql-server-vb/_static/image24.png)) 

第三步提示输入数据库信息：服务器名称、身份验证信息和数据库名称。 如果已与本教程一起使用，并将数据库添加到， `SecurityTutorials.mdf` `App_Data` 并将 `localhost\InstanceName` 其重命名为， `SecurityTutorialsDatabase` 则使用以下值：

- 服务器：`localhost\InstanceName`
- Windows 身份验证
- 数据 `SecurityTutorialsDatabase`

[![输入数据库信息](creating-the-membership-schema-in-sql-server-vb/_static/image26.png)](creating-the-membership-schema-in-sql-server-vb/_static/image25.png)

**图 9**：输入数据库信息 ([单击查看全尺寸图像](creating-the-membership-schema-in-sql-server-vb/_static/image27.png)) 

输入数据库信息后，单击 "下一步"。 最后一个步骤汇总了将要执行的步骤。 单击 "下一步" 以安装应用程序服务，然后单击 "完成" 完成向导。

> [!NOTE]
> 如果使用 Management Studio 附加数据库并重命名数据库文件，请确保分离数据库并关闭 Management Studio，然后再重新打开 Visual Studio。 若要分离 `SecurityTutorialsDatabase` 数据库，请右键单击数据库名称，然后在 "任务" 菜单中选择 "分离"。

完成向导后，返回到 Visual Studio 并导航到数据库资源管理器。 展开“表”文件夹。 应该会看到一系列名称以前缀开头的表 `aspnet_` 。 同样，可以在 "视图" 和 "存储过程" 文件夹下找到各种视图和存储过程。 这些数据库对象构成应用程序服务架构。 我们将在步骤3中检查成员身份和特定于角色的数据库对象。

[![已将各种表、视图和存储过程添加到数据库中](creating-the-membership-schema-in-sql-server-vb/_static/image29.png)](creating-the-membership-schema-in-sql-server-vb/_static/image28.png)

**图 10**：已将各种表、视图和存储过程添加到数据库 ([单击查看全尺寸图像](creating-the-membership-schema-in-sql-server-vb/_static/image30.png)) 

> [!NOTE]
> 该 `aspnet_regsql.exe` 工具的图形用户界面将安装整个应用程序服务架构。 但 `aspnet_regsql.exe` 从命令行执行时，可以指定要安装哪些特定的应用程序服务组件 (或删除) 。 因此，如果只想要添加和提供程序所需的表、视图和存储过程 `SqlMembershipProvider` `SqlRoleProvider` ，请 `aspnet_regsql.exe` 从命令行运行。 或者，你可以手动运行使用的 T-sql 创建脚本的适当子集 `aspnet_regsql.exe` 。 这些脚本位于 `WINDIR%\Microsoft.Net\Framework\v2.0.50727\` 文件夹中，名称如 `InstallCommon.sql` 、 `InstallMembership.sql` 、 `InstallRoles.sql` 、、等 `InstallProfile.sql` `InstallSqlState.sql` 。

此时，我们已创建了所需的数据库对象 `SqlMembershipProvider` 。 但是，我们仍需要指示成员身份框架应使用 `SqlMembershipProvider` (与 `ActiveDirectoryMembershipProvider`) ，并且 `SqlMembershipProvider` 应使用 `SecurityTutorials` 数据库。 我们将介绍如何指定要使用的提供程序，以及如何在步骤4中自定义所选提供程序的设置。 但首先，让我们深入了解刚创建的数据库对象。

## <a name="step-3-a-look-at-the-schemas-core-tables"></a>步骤3：查看架构的核心表

在 ASP.NET 应用程序中使用成员身份和角色框架时，提供程序会封装实现细节。 在将来的教程中，我们将通过 .NET Framework 的和类与这些框架进行交互 `Membership` `Roles` 。 当使用这些高级 Api 时，我们不需要自己了解低级别的详细信息，例如执行了哪些查询或由和修改了哪些表 `SqlMembershipProvider` `SqlRoleProvider` 。

为此，我们可以放心地使用成员身份和角色框架，而无需探索在步骤2中创建的数据库架构。 但是，在创建用于存储应用程序数据的表时，可能需要创建与用户或角色相关的实体。 在 `SqlMembershipProvider` `SqlRoleProvider` 应用程序数据表和步骤2中创建的表之间建立外键约束时，这有助于熟悉和架构。 此外，在某些极少数情况下，可能需要在数据库级别 (而不是通过 `Membership` 或类) 与用户和角色存储直接交互 `Roles` 。

### <a name="partitioning-the-user-store-into-applications"></a>将用户存储分区到应用程序中

成员资格和角色框架的设计使单个用户和角色存储可以在许多不同的应用程序之间共享。 使用成员身份或角色框架的 ASP.NET 应用程序必须指定要使用的应用程序分区。 简而言之，多个 web 应用程序可以使用相同的用户和角色存储。 图11描述了分区为三个应用程序的用户和角色存储： HRSite、CustomerSite 和 SalesSite。 这三个 web 应用程序都有自己唯一的用户和角色，但它们在物理上将其用户帐户和角色信息存储在相同的数据库表中。

[![可以跨多个应用程序对用户帐户进行分区](creating-the-membership-schema-in-sql-server-vb/_static/image32.png)](creating-the-membership-schema-in-sql-server-vb/_static/image31.png)

**图 11**：可以跨多个应用程序对用户帐户进行分区 ([单击查看完全大小的图像](creating-the-membership-schema-in-sql-server-vb/_static/image33.png)) 

`aspnet_Applications`该表定义了这些分区。 使用数据库存储用户帐户信息的每个应用程序都用此表中的一行表示。 `aspnet_Applications`该表具有四列： `ApplicationId` 、 `ApplicationName` 、 `LoweredApplicationName` 和 `Description` 。`ApplicationId` 的类型为 [`uniqueidentifier`](https://msdn.microsoft.com/library/ms187942.aspx) ，并且为表的主键，为 `ApplicationName` 每个应用程序提供唯一的友好名称。

其他与角色相关的成员关系表链接回 `ApplicationId` 中的字段 `aspnet_Applications` 。 例如， `aspnet_Users` 表（其中包含每个用户帐户的记录）具有 `ApplicationId` 外键字段; 表的 ditto `aspnet_Roles` 。 `ApplicationId`这些表中的字段指定用户帐户或角色所属的应用程序分区。

### <a name="storing-user-account-information"></a>存储用户帐户信息

用户帐户信息保存在两个表中： `aspnet_Users` 和 `aspnet_Membership` 。 `aspnet_Users`该表包含的字段包含重要的用户帐户信息。 最相关的三个列是：

- `UserId`
- `UserName`
- `ApplicationId`

`UserId` 为主键 (类型 `uniqueidentifier`) 。 `UserName` 的类型为， `nvarchar(256)` 并且与密码一起构成用户的凭据。  (用户的密码存储在 `aspnet_Membership` 表中。 ) 将 `ApplicationId` 用户帐户链接到中的特定应用程序 `aspnet_Applications` 。 和列上有一个组合[ `UNIQUE` 约束](https://msdn.microsoft.com/library/ms191166.aspx) `UserName` `ApplicationId` 。 这可确保在给定的应用程序中，每个用户名都是唯一的，但它允许 `UserName` 在不同的应用程序中使用相同的。

`aspnet_Membership`该表包含附加的用户帐户信息，如用户的密码、电子邮件地址、上次登录日期和时间等。 和表中的记录之间存在一对一的对应关系 `aspnet_Users` `aspnet_Membership` 。 此关系由 `UserId` 中的字段确保，该字段 `aspnet_Membership` 用作表的主键。 与 `aspnet_Users` 表类似， `aspnet_Membership` 包括将 `ApplicationId` 此信息与特定应用程序分区联系的字段。

### <a name="securing-passwords"></a>保护密码

密码信息存储在表中 `aspnet_Membership` 。 `SqlMembershipProvider`允许使用以下三种方法之一在数据库中存储密码：

- **清除** -密码以纯文本形式存储在数据库中。 我强烈反对使用此选项。 如果数据库遭到入侵，黑客会发现后门或有不满的雇员拥有数据库访问权限，这是每个用户的凭据，
- **哈** 希-使用单向哈希算法和随机生成的 salt 值对密码进行哈希处理。 此哈希值与 salt)  (一起存储在数据库中。
- 已**加密**-密码的加密版本存储在数据库中。

使用的密码存储方法取决于 `SqlMembershipProvider` 中指定的设置 `Web.config` 。 我们将在步骤4中介绍如何自定义 `SqlMembershipProvider` 设置。 默认行为是存储密码的哈希。

负责存储密码的列是 `Password` 、 `PasswordFormat` 和 `PasswordSalt` 。 `PasswordFormat` 类型的字段， `int` 其值指示用于存储密码的方法：0表示清除; 1 表示哈希; 2 表示已加密。 `PasswordSalt` 无论使用何种密码存储技术，都将分配一个随机生成的字符串。 `PasswordSalt` 仅在计算密码的哈希时使用的值。 最后， `Password` 列包含实际的密码数据、纯文本密码、密码哈希或加密密码。

表1说明了在存储密码 MySecret 时，这三列可能会显示在各种存储技术中的情况！ .

| **存储技术 &lt; \_ o3a \_ p/&gt;** | **Password &lt; \_ o3a \_ p/&gt;** | **PasswordFormat &lt; \_ o3a \_ p/&gt;** | **PasswordSalt &lt; \_ o3a \_ p/&gt;** |
| --- | --- | --- | --- |
| Clear | MySecret! | 0 | tTnkPlesqissc2y2SMEygA = = |
| 计算 | 2oXm6sZHWbTHFgjgkGQsc2Ec9ZM = | 1 | wFgjUfhdUFOCKQiI61vtiQ = = |
| 已加密 | 62RZgDvhxykkqsMchZ0Yly7HS6onhpaoCYaRxV8g0F4CW56OXUU3e7Inza9j9BKp | 2 | LSRzhGS/aa/oqAXGLHJNBw = = |

**表 1**：存储密码 MySecret 时与密码相关的字段的示例值！

> [!NOTE]
> 使用的特定加密或哈希算法由 `SqlMembershipProvider` 元素中的设置确定 `<machineKey>` 。 我们在 <a id="Tutorial3"></a> [*Forms 身份验证配置和高级主题*](../introduction/forms-authentication-configuration-and-advanced-topics-vb.md)教程的步骤3中讨论了此配置元素。

### <a name="storing-roles-and-role-associations"></a>存储角色和角色关联

角色框架允许开发人员定义一组角色并指定哪些用户属于哪些角色。 此信息通过两个表在数据库中捕获： `aspnet_Roles` 和 `aspnet_UsersInRoles` 。 表中的每条记录 `aspnet_Roles` 表示特定应用程序的角色。 与表非常类似 `aspnet_Users` ， `aspnet_Roles` 表中有三列与我们的讨论相关：

- `RoleId`
- `RoleName`
- `ApplicationId`

`RoleId` 为主键 (类型 `uniqueidentifier`) 。 `RoleName` 的类型为 `nvarchar(256)`。 并 `ApplicationId` 将用户帐户链接到中的特定应用程序 `aspnet_Applications` 。 `UNIQUE`和列上有一个复合约束 `RoleName` `ApplicationId` ，可确保在给定的应用程序中，每个角色名称都是唯一的。

`aspnet_UsersInRoles`该表用作用户和角色之间的映射。 只有两个列 `UserId` ， `RoleId` 它们共同构成了一个组合主键。

## <a name="step-4-specifying-the-provider-and-customizing-its-settings"></a>步骤4：指定提供程序并自定义其设置

支持该提供程序模型的所有框架（例如成员身份和角色框架）本身缺乏实现细节，而是将该责任委托给提供程序类。 对于成员身份框架， `Membership` 类定义用于管理用户帐户的 API，但它不与任何用户存储直接交互。 相反， `Membership` 类的方法会将请求移交给已配置的提供程序-我们将使用 `SqlMembershipProvider` 。 当我们调用类中的方法之一时 `Membership` ，成员身份框架如何知道如何委托对的调用 `SqlMembershipProvider` ？

`Membership`类具有一个[ `Providers` 属性](https://msdn.microsoft.com/library/system.web.security.membership.providers.aspx)，该属性包含对成员身份框架可使用的所有已注册提供程序类的引用。 每个注册的提供程序都有关联的名称和类型。 该名称提供在集合中引用特定提供程序的友好方法 `Providers` ，而类型标识提供程序类。 而且，每个注册的提供程序都可以包括配置设置。 成员身份框架的配置设置包括 `PasswordFormat` 和 `requiresUniqueEmail` 。 有关使用的配置设置的完整列表，请参阅表 2 `SqlMembershipProvider` 。

`Providers`通过 web 应用程序的配置设置来指定属性的内容。 默认情况下，所有 web 应用程序都有一个名为 `AspNetSqlMembershipProvider` 的类型为的提供程序 `SqlMembershipProvider` 。 此默认成员资格提供程序在 `machine.config` 位于)  (上注册 `%WINDIR%\Microsoft.Net\Framework\v2.0.50727\CONFIG` ：

[!code-xml[Main](creating-the-membership-schema-in-sql-server-vb/samples/sample1.xml)]

正如上面的标记所示， [ `<membership>` 元素](https://msdn.microsoft.com/library/1b9hw62f.aspx)定义成员身份框架的配置设置，而[ `<providers>` 子元素](https://msdn.microsoft.com/library/6d4936ht.aspx)指定已注册的提供程序。 可以使用或元素添加或删除提供 [`<add>`](https://msdn.microsoft.com/library/whae3t94.aspx) 程序 [`<remove>`](https://msdn.microsoft.com/library/aykw9a6d.aspx) ; 使用 [`<clear>`](https://msdn.microsoft.com/library/t062y6yc.aspx) 元素删除所有当前已注册的提供程序。 如以上标记所示， `machine.config` 添加了一个类型为的提供程序 `AspNetSqlMembershipProvider` `SqlMembershipProvider` 。

除了 `name` 和 `type` 特性之外，元素还 `<add>` 包含一些属性，这些属性用于定义各种配置设置的值。 表2列出了可用 `SqlMembershipProvider` 的特定配置设置，以及每个设置的说明。

> [!NOTE]
> 表2中记下的任何默认值都是指在类中定义的默认值 `SqlMembershipProvider` 。 请注意，并非中的所有配置设置都 `AspNetSqlMembershipProvider` 对应于类的默认值 `SqlMembershipProvider` 。 例如，如果未在成员资格提供程序中指定，则 `requiresUniqueEmail` 设置默认为 true。 但是， `AspNetSqlMembershipProvider` 通过显式指定的值覆盖此默认值 `false` 。

| **设置 &lt; \_ o3a \_ p/&gt;** | **Description &lt; \_ o3a \_ p/&gt;** |
| --- | --- |
| `ApplicationName` | 请记住，成员身份框架允许跨多个应用程序对单个用户存储进行分区。 此设置指示成员资格提供程序所使用的应用程序分区的名称。 如果未显式指定此值，则在运行时将其设置为应用程序的虚拟根路径的值。 |
| `commandTimeout` | 指定 SQL 命令超时值 (，以秒为单位) 。 默认值为 30。 |
| `connectionStringName` | 元素中用于 `<connectionStrings>` 连接到用户存储数据库的连接字符串的名称。 此值是必需的。 |
| `description` | 提供已注册提供程序的友好说明。 |
| `enablePasswordRetrieval` | 指定用户是否可以检索其忘记的密码。 默认值为 `false`。 |
| `enablePasswordReset` | 指示是否允许用户重置其密码。 默认为 `true`。 |
| `maxInvalidPasswordAttempts` | 用户被锁定之前指定用户在指定的最大失败登录尝试次数 `passwordAttemptWindow` 。默认值为5。 |
| `minRequiredNonalphanumericCharacters` | 必须出现在用户密码中的非字母数字字符的最小数目。 此值必须介于0到128之间;默认值为1。 |
| `minRequiredPasswordLength` | 密码中所需的最小字符数。 此值必须介于0到128之间;默认值为7。 |
| `name` | 已注册的提供程序的名称。 此值是必需的。 |
| `passwordAttemptWindow` | 跟踪失败的登录尝试的分钟数。 如果用户在指定的时段内提供了无效的登录凭据 `maxInvalidPasswordAttempts` ，则会被锁定。默认值为10。 |
| `PasswordFormat` | 密码存储格式： `Clear` 、 `Hashed` 或 `Encrypted` 。 默认值为 `Hashed`。 |
| `passwordStrengthRegularExpression` | 如果提供了此正则表达式，则在创建新帐户或更改其密码时，将使用此正则表达式来评估用户所选密码的强度。 默认值为空字符串。 |
| `requiresQuestionAndAnswer` | 指定在检索或重置其密码时，用户是否必须回答其安全问题。 默认值为 `true`。 |
| `requiresUniqueEmail` | 指示给定应用程序分区中的所有用户帐户是否都必须具有唯一的电子邮件地址。 默认值为 `true`。 |
| `type` | 指定提供程序的类型。 此值是必需的。 |

**表 2**：成员身份和 `SqlMembershipProvider` 配置设置

除了 `AspNetSqlMembershipProvider` 之外，还可以通过将类似标记添加到文件，在应用程序的基础上注册其他成员资格提供程序 `Web.config` 。

> [!NOTE]
> 角色框架的工作方式大致相同：中有一个默认的注册角色提供程序 `machine.config` ，在中，可以在应用程序的基础上自定义注册的提供程序 `Web.config` 。 在将来的教程中，我们将详细介绍角色框架及其配置标记。

### <a name="customizing-thesqlmembershipprovidersettings"></a>自定义 `SqlMembershipProvider` 设置

默认 `SqlMembershipProvider` (`AspNetSqlMembershipProvider`) `connectionStringName` 将其特性设置为 `LocalSqlServer` 。 与 `AspNetSqlMembershipProvider` 提供程序一样，连接字符串名称 `LocalSqlServer` 是在中定义的 `machine.config` 。

[!code-xml[Main](creating-the-membership-schema-in-sql-server-vb/samples/sample2.xml)]

如您所见，此连接字符串定义2005了位于 |DataDirectory | aspnetdb.mdf。 字符串 |DataDirectory |在运行时将转换为指向 `~/App_Data/` 目录，因此，数据库路径 |DataDirectory | aspnetdb.mdf 转换为 `~/App_Data` / `aspnet.mdf` 。

如果我们未在应用程序文件中指定任何成员身份提供程序信息 `Web.config` ，则应用程序将使用默认的已注册成员资格提供程序 `AspNetSqlMembershipProvider` 。 如果 `~/App_Data/aspnet.mdf` 数据库不存在，ASP.NET 运行时将自动创建它并添加应用程序服务架构。 但是，我们不想使用数据库， `aspnet.mdf` 而是想要使用 `SecurityTutorials.mdf` 我们在步骤2中创建的数据库。 可以通过以下两种方式之一完成此修改：

- <strong>指定</strong> <strong>`LocalSqlServer`</strong><strong>连接字符串名称</strong> <strong>`Web.config`</strong><strong>.</strong> 通过覆盖中的 " `LocalSqlServer` 连接字符串名称" 值 `Web.config` ，可以 () 使用默认注册的成员资格提供程序， `AspNetSqlMembershipProvider` 并将其与数据库一起正确使用 `SecurityTutorials.mdf` 。 如果你是具有指定的配置设置的内容，则此方法很合适 `AspNetSqlMembershipProvider` 。 有关此技术的详细信息，请参阅 [Scott Guthrie](https://weblogs.asp.net/scottgu/)的博客文章将 [ASP.NET 2.0 应用程序服务配置为使用 SQL Server 2000 或 SQL Server 2005](https://weblogs.asp.net/scottgu/archive/2005/08/25/423703.aspx)。
- <strong>添加类型</strong> <strong>`SqlMembershipProvider`</strong> 为的新注册的提供程序<strong>并配置其</strong> <strong>`connectionStringName`</strong><strong>设置为指向</strong> <strong>`SecurityTutorials.mdf`</strong><strong>数据库。</strong> 如果要自定义数据库连接字符串以外的其他配置属性，则此方法非常有用。 在我自己的项目中，我始终使用这种方法，因为它具有灵活性和可读性。

在我们可以添加引用数据库的新注册的提供程序之前 `SecurityTutorials.mdf` ，首先需要在的部分中添加适当的连接字符串值 `<connectionStrings>` `Web.config` 。 下面的标记将添加一个名为的新连接字符串 `SecurityTutorialsConnectionString` ，该字符串引用 `SecurityTutorials.mdf` 文件夹中的 SQL Server 2005 Express Edition 数据库 `App_Data` 。

[!code-xml[Main](creating-the-membership-schema-in-sql-server-vb/samples/sample3.xml)]

> [!NOTE]
> 如果使用的是备用数据库文件，请根据需要更新连接字符串。 有关形成正确连接字符串的详细信息，请参阅 [ConnectionStrings.com](http://www.connectionstrings.com/)。

接下来，向该文件添加以下成员身份配置标记 `Web.config` 。 此标记将注册一个名为的新提供程序 `SecurityTutorialsSqlMembershipProvider` 。

[!code-xml[Main](creating-the-membership-schema-in-sql-server-vb/samples/sample4.xml)]

除注册 `SecurityTutorialsSqlMembershipProvider` 提供程序外，上述标记还 `SecurityTutorialsSqlMembershipProvider` 通过 `defaultProvider` 元素) 中的特性将定义为默认提供程序 (`<membership>` 。 请记住，成员身份框架可以有多个已注册的提供程序。 由于 `AspNetSqlMembershipProvider` 注册为中的第一个提供程序 `machine.config` ，因此它将用作默认提供程序，除非我们指示。

目前，我们的应用程序有两个注册的提供程序： `AspNetSqlMembershipProvider` 和 `SecurityTutorialsSqlMembershipProvider` 。 但是，在注册 `SecurityTutorialsSqlMembershipProvider` 提供程序之前，可以通过在元素前面添加[ `<clear />` 元素](https://msdn.microsoft.com/library/t062y6yc.aspx)来清除所有以前注册的提供程序 `<add>` 。 这将 `AspNetSqlMembershipProvider` 从已注册的提供程序列表中清除，这意味着将 `SecurityTutorialsSqlMembershipProvider` 是唯一注册的成员资格提供程序。 如果使用此方法，则不需要将 `SecurityTutorialsSqlMembershipProvider` 作为默认提供程序标记，因为它是唯一注册的成员资格提供程序。 有关使用的详细信息 `<clear />` ，请 [参阅 `<clear />` 添加提供程序时的使用](https://weblogs.asp.net/scottgu/archive/2006/11/20/common-gotcha-don-t-forget-to-clear-when-adding-providers.aspx)。

请注意， `SecurityTutorialsSqlMembershipProvider` 的 `connectionStringName` 设置引用刚刚添加的 `SecurityTutorialsConnectionString` 连接字符串名称，并且其设置已 `applicationName` 设置为 SecurityTutorials 值。 此外， `requiresUniqueEmail` 设置已设置为 `true` 。 所有其他配置选项都与中的值相同 `AspNetSqlMembershipProvider` 。 如果需要，可以在此处随意进行任何配置修改。 例如，你可以通过要求使用两个非字母数字的字符而不是一个，或者将密码长度增加到八个字符而不是七个字符来提高密码强度。

> [!NOTE]
> 请记住，成员身份框架允许跨多个应用程序对单个用户存储进行分区。 成员资格提供程序的 `applicationName` 设置指示当使用用户存储区时提供程序所使用的应用程序。 明确设置配置设置的值非常重要， `applicationName` 因为如果 `applicationName` 未显式设置，则会在运行时将其分配给 web 应用程序的虚拟根路径。 只要应用程序的虚拟根路径不改变，此操作就会正常运行，但如果将应用程序移到不同的路径，该 `applicationName` 设置也会更改。 发生这种情况时，成员资格提供程序将开始处理与以前使用的应用程序分区不同的应用程序分区。 在移动之前创建的用户帐户将驻留在不同的应用程序分区中，这些用户将无法再登录到该站点。 有关此问题的更深入讨论，请参阅 [ `applicationName` 配置 ASP.NET 2.0 成员身份和其他提供程序时始终设置属性](https://weblogs.asp.net/scottgu/443634)。

## <a name="summary"></a>摘要

此时，我们有了一个具有配置的应用程序服务 (的数据库 `SecurityTutorials.mdf`) 并配置了 web 应用程序，以便成员身份框架使用 `SecurityTutorialsSqlMembershipProvider` 刚才注册的提供程序。 此注册的提供程序的类型为 `SqlMembershipProvider` ，并 `connectionStringName` 将其设置为合适的连接字符串 (`SecurityTutorialsConnectionString`) 并 `applicationName` 显式设置其值。

现在，我们已准备好从应用程序使用成员身份框架。 在下一教程中，我们将介绍如何创建新的用户帐户。 接下来，我们将探索对用户进行身份验证，执行基于用户的授权，并在数据库中存储其他用户相关信息。

很高兴编程！

### <a name="further-reading"></a>深入阅读

有关本教程中讨论的主题的详细信息，请参阅以下资源：

- [`applicationName`配置 ASP.NET 2.0 成员身份和其他提供程序时始终设置属性](https://weblogs.asp.net/scottgu/443634)
- [配置 ASP.NET 2.0 应用程序服务以使用 SQL Server 2000 或 SQL Server 2005](https://weblogs.asp.net/scottgu/archive/2005/08/25/423703.aspx)
- [下载 SQL Server Management Studio Express Edition](https://www.microsoft.com/downloads/details.aspx?FamilyId=C243A5AE-4BD1-4E3D-94B8-5A0F62BF7796&amp;displaylang=en)
- [检查 ASP.NET 2.0 s 成员资格、角色和配置文件](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)
- [用于 `<add>` 成员身份的提供程序的元素](https://msdn.microsoft.com/library/whae3t94.aspx)
- [`<membership>`元素](https://msdn.microsoft.com/library/1b9hw62f.aspx)
- [`<providers>`成员资格的元素](https://msdn.microsoft.com/library/6d4936ht.aspx)
- [`<clear />`添加提供程序时使用](https://weblogs.asp.net/scottgu/archive/2006/11/20/common-gotcha-don-t-forget-to-clear-when-adding-providers.aspx)
- [直接使用 `SqlMembershipProvider`](http://aspnet.4guysfromrolla.com/articles/091207-1.aspx)

### <a name="video-training-on-topics-contained-in-this-tutorial"></a>本教程中包含的主题的视频培训

- [了解 ASP.NET 成员身份](../../../videos/authentication/understanding-aspnet-memberships.md)
- [配置 SQL 以使用成员身份架构](../../../videos/authentication/configuring-sql-to-work-with-membership-schemas.md)
- [更改默认成员身份架构中的成员身份设置](../../../videos/authentication/changing-membership-settings-in-the-default-membership-schema.md)

### <a name="about-the-author"></a>关于作者

Scott Mitchell，创始人的多个 ASP/ASP 和4GuysFromRolla.com 的作者已使用 Microsoft Web 技术，1998。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是， *[在24小时内，sam ASP.NET 2.0](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)*。 可以在上 [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com) 或通过他的博客访问 Scott [http://ScottOnWriting.NET](http://scottonwriting.net/) 。

### <a name="special-thanks-to"></a>特别感谢

此教程系列由许多有用的审阅者查看。 本教程的主管审查人员是 Alicja Maziarz。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在中放置一行 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com) 。

> [!div class="step-by-step"]
> [上一页](storing-additional-user-information-cs.md)
> [下一页](creating-user-accounts-vb.md)

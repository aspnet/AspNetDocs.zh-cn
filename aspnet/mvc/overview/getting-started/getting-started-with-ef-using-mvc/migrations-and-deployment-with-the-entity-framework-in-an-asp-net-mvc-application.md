---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application
title: 教程：在 ASP.NET MVC 应用中使用 EF 迁移并将其部署到 Azure
author: tdykstra
description: 在本教程中，你将启用 Code First 迁移，并将应用程序部署到 Azure 中的云。
ms.author: riande
ms.date: 01/16/2019
ms.topic: tutorial
ms.assetid: d4dfc435-bda6-4621-9762-9ba270f8de4e
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 2f3a6d57a7963eb7aafde62e344ae6b970af87e2
ms.sourcegitcommit: 8d34fb54e790cfba2d64097afc8276da5b22283e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2020
ms.locfileid: "85484225"
---
# <a name="tutorial-use-ef-migrations-in-an-aspnet-mvc-app-and-deploy-to-azure"></a>教程：在 ASP.NET MVC 应用中使用 EF 迁移并将其部署到 Azure

到目前为止，Contoso 大学示例 web 应用程序已在您的开发计算机上 IIS Express 本地运行。 要使真实应用程序可供其他人通过 Internet 使用，你必须将其部署到 web 托管提供商。 在本教程中，你将启用 Code First 迁移，并将应用程序部署到 Azure 中的云：

- 启用 Code First 迁移。 使用迁移功能，您可以更改数据模型并将更改部署到生产，方法是更新数据库架构，而无需删除并重新创建数据库。
- 部署到 Azure。 此步骤是可选的;你可以继续学习其余教程，而不会部署该项目。

建议你将持续集成过程与源代码管理配合使用来进行部署，但本教程并不介绍这些主题。 有关详细信息，请参阅在[Azure 中构建实际云应用程序](xref:aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction)的[源代码管理](xref:aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control)和[持续集成](xref:aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery)章节。

在本教程中，你将了解：

> [!div class="checklist"]
> * 启用 Code First 迁移
> * 在 Azure 中部署应用（可选）

## <a name="prerequisites"></a>先决条件

- [连接复原和命令截获](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="enable-code-first-migrations"></a>启用 Code First 迁移

开发新应用程序时，数据模型会频繁更改。每当模型更改时，模型都无法与数据库保持同步。 您已将实体框架配置为每次更改数据模型时，自动删除并重新创建数据库。 添加、删除或更改实体类或更改 `DbContext` 类时，下一次运行应用程序时，它会自动删除您的现有数据库，创建与模型匹配的新数据库，并使用测试数据为其设定种子。

这种使数据库与数据模型保持同步的方法适用于多种情况，但将应用程序部署到生产环境的情况除外。 当应用程序在生产环境中运行时，它通常存储您要保留的数据，并且您不希望每次进行更改（例如添加新列）时都丢失任何数据。 [Code First 迁移](https://msdn.microsoft.com/data/jj591621)功能通过启用 Code First 更新数据库架构（而不是删除并重新创建数据库）来解决此问题。 在本教程中，你将部署应用程序，并准备好要启用迁移。

1. 通过注释掉或删除 `contexts` 已添加到应用程序 Web.config 文件中的元素，禁用先前设置的初始值设定项。

    [!code-xml[Main](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.xml?highlight=2,6)]
2. 同样，在应用程序*Web.config*文件中，将连接字符串中的数据库名称更改为 ContosoUniversity2。

    [!code-xml[Main](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.xml?highlight=2)]

    此更改将设置项目，以便第一个迁移创建新数据库。 这并不是必需的，但稍后您将看到它是一个很好的想法。
3. 在“工具”菜单中，选择“NuGet 包管理器” > “包管理器控制台”。  

1. 在 `PM>` 提示符下输入以下命令：

    ```text
    enable-migrations
    add-migration InitialCreate
    ```

    `enable-migrations`命令将在 ContosoUniversity 项目中创建一个*迁移*文件夹，并*将该*文件夹置于该文件夹中，你可以编辑该文件以配置迁移。

    （如果你错过了上述步骤来更改数据库名称，则迁移将查找现有数据库并自动执行此 `add-migration` 命令。 没关系，这只意味着在部署数据库之前不会运行迁移代码测试。 稍后运行命令时， `update-database` 不会执行任何操作，因为数据库已存在。）

    打开*ContosoUniversity\Migrations\Configuration.cs*文件。 与前面看到的初始值设定项类一样， `Configuration` 类包含 `Seed` 方法。

    [!code-csharp[Main](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs)]

    [Seed](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx)方法的用途是使你能够在 Code First 创建或更新数据库后插入或更新测试数据。 创建数据库时，将调用方法，并在数据模型更改后每次更新数据库架构时调用此方法。

### <a name="set-up-the-seed-method"></a>设置种子方法

为每个数据模型更改删除并重新创建数据库时，可使用初始值设定项类的 `Seed` 方法插入测试数据，因为在每个模型更改后，数据库都会被删除，并且所有测试数据都将丢失。 在 Code First 迁移的情况下，在数据库更改后会保留测试数据，因此通常不需要在[Seed](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx)方法中包括测试数据。 事实上， `Seed` 如果您将使用迁移将数据库部署到生产环境，则不希望该方法插入测试数据，因为该 `Seed` 方法将在生产环境中运行。 在这种情况下，你希望 `Seed` 方法仅在生产中插入数据库中所需的数据。 例如， `Department` 当应用程序在生产中可用时，您可能希望数据库包括表中的实际部门名称。

对于本教程，你将使用迁移进行部署，但你的 `Seed` 方法将插入测试数据，以便更轻松地了解应用程序功能的工作方式，而无需手动插入大量数据。

1. 将*Configuration.cs*文件的内容替换为以下代码，该代码可将测试数据加载到新数据库中。

    [!code-csharp[Main](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

    [Seed](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx)方法采用数据库上下文对象作为输入参数，方法中的代码使用该对象将新实体添加到数据库中。 对于每个实体类型，代码将创建新实体的集合，将其添加到相应的[DbSet](https://msdn.microsoft.com/library/system.data.entity.dbset(v=vs.103).aspx)属性，然后将更改保存到数据库。 不需要在每个实体组后调用[SaveChanges](https://msdn.microsoft.com/library/system.data.entity.dbcontext.savechanges(v=VS.103).aspx)方法，这一点在此完成，但这样做可帮助您找到问题的根源（如果代码写入数据库时出现异常）。

    插入数据的某些语句使用[AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx)方法执行 "upsert" 操作。 由于在每 `Seed` 次执行命令时（通常在每次迁移之后）都将运行该方法，因此 `update-database` 您不能只插入数据，因为在第一个创建数据库的迁移之后，您尝试添加的行将已存在。 如果尝试插入已存在的行，"upsert" 操作将会阻止发生的错误，但会***覆盖***在测试应用程序时对数据所做的任何更改。 对于某些表中的测试数据，您可能不希望发生这种情况：在某些情况下，当您在测试时更改数据时，您希望在数据库更新后更改保持不变。 在这种情况下，需要执行条件插入操作：仅在不存在行时插入行。 Seed 方法使用这两种方法。

    传递给[AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx)方法的第一个参数指定要用于检查行是否已存在的属性。 对于所提供的测试学生数据， `LastName` 属性可用于此目的，因为列表中的每个姓氏都是唯一的：

    [!code-csharp[Main](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs)]

    此代码假定姓氏是唯一的。 如果你手动添加具有重复姓氏的学生，你将在下一次执行迁移时收到以下例外：

    **序列包含多个元素**

    有关如何处理冗余数据（如名为 "Alexander Carson" 的两名学生）的信息，请参阅 Rick Anderson 博客上的[播种和调试实体框架（EF）](https://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx)数据库。 有关方法的详细信息 `AddOrUpdate` ，请参阅 Julie Lerman 的博客上的[EF 4.3 AddOrUpdate 方法](http://thedatafarm.com/blog/data-access/take-care-with-ef-4-3-addorupdate-method/)。

    创建实体的代码 `Enrollment` 假设你在集合的 `ID` 实体中具有值 `students` ，但你未在创建该集合的代码中设置该属性。

    [!code-csharp[Main](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs?highlight=2)]

    你可以在 `ID` 此处使用属性，因为在 `ID` 为集合调用时设置值 `SaveChanges` `students` 。 在将实体插入到数据库中时，EF 会自动获取主键值，并更新 `ID` 内存中实体的属性。

    将每个实体添加 `Enrollment` 到 `Enrollments` 实体集的代码不使用 `AddOrUpdate` 方法。 它将检查实体是否已存在，如果实体不存在，则插入该实体。 此方法将保留你使用应用程序 UI 对注册级别所做的更改。 代码遍历列表中的每个成员 `Enrollment` [List](https://msdn.microsoft.com/library/6sh2ey19.aspx) ，如果未在数据库中找到注册，则会将注册添加到数据库中。 第一次更新数据库时，该数据库将为空，因此将添加每个注册。

    [!code-csharp[Main](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

2. 生成项目。

### <a name="execute-the-first-migration"></a>执行第一次迁移

执行 `add-migration` 命令时，迁移过程生成了从头开始创建数据库的代码。 此代码也位于名为* &lt; timestamp &gt; \_ InitialCreate.cs*的文件中的 "*迁移*" 文件夹中。 `Up`类的方法 `InitialCreate` 创建与数据模型实体集相对应的数据库表，方法将 `Down` 删除这些表。

[!code-csharp[Main](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

迁移调用 `Up` 方法为迁移实现数据模型更改。 输入用于回退更新的命令时，迁移调用 `Down` 方法。

这是在输入命令时创建的初始迁移 `add-migration InitialCreate` 。 参数（ `InitialCreate` 在本示例中为）用于文件名，可以是任何所需的内容; 通常，可以选择一个词或短语，用于汇总迁移中所执行的操作。 例如，你可以命名以后的迁移 &quot; AddDepartmentTable &quot; 。

如果创建初始迁移时已存在数据库，则会生成数据库创建代码，但此代码不必运行，因为数据库已与数据库模型相匹配。 将应用部署到其中尚不存在数据库的其他环境时，此代码将运行以创建数据库，因此最好提前进行测试。 这就是你在前面的连接字符串中更改数据库名称的原因， &mdash; 以便迁移可以从头开始创建一个新数据库。

1. 在“程序包管理器控制台”窗口中，输入以下命令：****

    `update-database`

    该 `update-database` 命令运行 `Up` 方法来创建数据库，然后运行 `Seed` 方法来填充数据库。 部署应用程序后，会在生产中自动运行相同的过程，如以下部分所示。
2. 使用**服务器资源管理器**来检查数据库，就像您在第一个教程中所做的那样，然后运行该应用程序以验证所有内容是否仍然像以前一样工作。

## <a name="deploy-to-azure"></a>部署到 Azure

到目前为止，应用程序已在本地 IIS Express 开发计算机上运行。 要使其可供其他人通过 Internet 使用，你必须将其部署到 web 托管提供商。 在本教程的此部分中，将其部署到 Azure。 本部分是可选的;你可以跳过此操作并继续学习以下教程，或者可以根据你选择的其他托管提供商改编此部分中的说明。

### <a name="use-code-first-migrations-to-deploy-the-database"></a>使用 Code First 迁移部署数据库

若要部署该数据库，你将使用 Code First 迁移。 当你创建用于配置从 Visual Studio 进行部署的设置时所用的发布配置文件时，你将选中标记为 "**更新数据库**" 的复选框。 此设置会导致部署过程在目标服务器上自动配置应用程序*Web.config*文件，使 Code First 使用 `MigrateDatabaseToLatestVersion` 初始值设定项类。

在部署过程中，Visual Studio 不会对数据库执行任何操作，而是将项目复制到目标服务器。 运行已部署的应用程序并在部署后首次访问数据库时，Code First 会检查数据库是否与数据模型相匹配。 如果存在不匹配的情况，Code First 会自动创建数据库（如果它尚不存在）或将数据库架构更新到最新版本（如果数据库存在但与模型不匹配）。 如果应用程序实现了迁移 `Seed` 方法，则该方法将在创建数据库或更新架构之后运行。

迁移 `Seed` 方法插入测试数据。 如果要部署到生产环境，则必须更改 `Seed` 方法，使其只插入要插入到生产数据库中的数据。 例如，在您的当前数据模型中，您可能希望在开发数据库中有真实的课程，但实际的学生。 你可以编写一个 `Seed` 方法，用于在开发中加载，然后在部署到生产环境之前注释掉虚构的学生。 或者，您可以编写一个 `Seed` 方法以仅加载课程，并使用应用程序的 UI 手动输入测试数据库中的虚构学生。

### <a name="get-an-azure-account"></a>获取 Azure 帐户

你将需要一个 Azure 帐户。 如果你还没有 Visual Studio 订阅，则可以[激活订阅权益](https://azure.microsoft.com/pricing/member-offers/credit-for-visual-studio-subscribers/
)。 否则，只需花费几分钟就能创建一个免费试用帐户。 有关详细信息，请参阅 [Azure 免费试用](https://azure.microsoft.com/free/dotnet/)。

### <a name="create-a-web-site-and-a-sql-database-in-azure"></a>在 Azure 中创建网站和 SQL 数据库

Azure 中的 web 应用将在共享宿主环境中运行，这意味着它将在与其他 Azure 客户端共享的虚拟机（Vm）上运行。 共享宿主环境是一种在云中开始工作的低成本方式。 稍后，如果你的 Web 流量增加，则应用程序可进行扩展，通过在专用 VM 上运行来满足需要。 若要详细了解 Azure App Service 的定价选项，请参阅[应用服务定价](https://azure.microsoft.com/pricing/details/app-service/)。

将数据库部署到 Azure SQL 数据库。 SQL 数据库是一种基于云的关系数据库服务，是基于 SQL Server 技术构建的。 与 SQL Server 一起使用的工具和应用程序也可用于 SQL 数据库。

1. 在[Azure 管理门户](https://portal.azure.com)中，在左侧选项卡中选择 "**创建资源**"，然后在**新**窗格（或*边栏*选项卡）上选择 "**查看全部**" 以查看所有可用资源。 在 "**所有内容**" 边栏选项卡的 " **web** " 部分中选择 " **web 应用 + SQL** "。 最后，选择 "**创建**"。

    ![在 Azure 门户中创建资源](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/_static/create-azure-resource.png)

   此时将打开用于创建新的**Web 应用 + SQL**资源的窗体。

2. 在 "**应用名称**" 框中输入一个字符串，将其用作应用程序的唯一 URL。 完整的 URL 由你在此处输入的内容和 Azure 应用 Services 的默认域（azurewebsites.net）组成。 如果**应用程序名称**已被使用，则向导将向你发出红色： *"应用程序名称不可用"* 消息。 如果**应用程序名称**可用，将看到绿色的复选标记。

3. 在 "**订阅**" 框中，选择要在其中驻留**应用服务**的 Azure 订阅。

4. 在 "**资源组**" 文本框中，选择一个资源组，或创建一个新的资源组。 此设置指定您的网站将在哪个数据中心运行。 有关资源组的详细信息，请参阅[资源组](/azure/azure-resource-manager/resource-group-overview#resource-groups)。

5. 单击 "*应用服务" 部分*、"**新建**"，并填写 "应用服务**计划**" （可以与应用服务相同的名称）、"**位置**" 和 "**定价层**"，创建新的**应用服务计划**（有免费选项）。

6. 单击 " **SQL 数据库**"，然后选择 "**创建新数据库**" 或 "选择现有数据库"。

7. 在 "**名称**" 框中，输入数据库的名称。
8. 单击 "**目标服务器**" 框，然后选择 "**创建新服务器**"。 或者，如果你以前创建了一个服务器，则可以从可用服务器列表中选择该服务器。
9. 选择 "**定价层**" 部分，选择 "*免费*"。 如果需要其他资源，可以随时对数据库进行扩展。 若要了解有关 Azure SQL 定价的详细信息，请参阅[AZURE Sql 数据库定价](https://azure.microsoft.com/pricing/details/sql-database/managed/)。
10. 根据需要修改[排序规则](/sql/relational-databases/collations/collation-and-unicode-support)。
11. 输入管理员**Sql 管理员用户名**和**sql 管理员密码**。

    - 如果选择了 "**新建 SQL 数据库服务器**"，请定义稍后在访问数据库时将使用的新名称和密码。
    - 如果选择了之前创建的服务器，请输入该服务器的凭据。

12. 可以使用 Application Insights 为应用服务启用遥测收集。 几乎没有配置，Application Insights 收集重要事件、异常、依赖项、请求和跟踪信息。 若要详细了解 Application Insights，请参阅[Azure Monitor](https://azure.microsoft.com/services/monitor/)。
13. 单击底部的 "**创建**" 以指示你已完成操作。

    管理门户将返回到 "仪表板" 页，页面顶部的 "**通知**" 区域会显示正在创建站点。 经过一段时间（通常不到一分钟），会出现部署成功的通知。 左侧导航栏中的 "**应用服务**" 部分会显示新的应用服务，新的 sql 数据库将显示在 " **SQL 数据库**" 部分中。

### <a name="deploy-the-app-to-azure"></a>将应用部署到 Azure

1. 在 Visual Studio 中，在“解决方案资源管理器”中右键单击项目，并从上下文菜单中选择“发布”。********

2. 在 "**选取发布目标**" 页上，选择 "**应用服务**"，然后**选择 "现有**"，然后选择 "**发布**"。

    ![选择发布目标页](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/_static/select-existing-app-service.png)

3. 如果之前未在 Visual Studio 中添加 Azure 订阅，请在屏幕上执行这些步骤。 这些步骤使 Visual Studio 能够连接到你的 Azure 订阅，以使**应用服务**列表包含你的网站。

4. 在 "**应用服务**" 页上，选择你向其中添加了应用服务的**订阅**。 在 "**视图**" 下，选择 "**资源组**"。 展开向其中添加了应用服务的资源组，然后选择 "应用服务"。 选择 **"确定"** 以发布应用。

5. “输出”窗口会显示已执行的部署操作并报告部署的成功完成。****

6. 成功完成部署后，默认浏览器会自动打开并指向已部署网站的 URL。

    ![Students_index_page_with_paging](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/_static/cloud-app-browser.png)

    应用现在正在云中运行。

此时，已在 Azure SQL 数据库中创建*SchoolContext*数据库，因为你选择了 **"执行 Code First 迁移（在应用启动时运行）**。 已部署网站中的*Web.config*文件已更改，以便在代码第一次读取或写入数据库中的数据时（在你选择 "**学生**" 选项卡时发生此情况） [MigrateDatabaseToLatestVersion](https://msdn.microsoft.com/library/hh829476(v=vs.103).aspx)初始值设定项：

![Web.config 文件摘录](https://asp.net/media/4367421/mig.png)

部署过程还为 Code First 迁移创建了一个新的连接字符串 *（SchoolContext \_ DatabasePublish*），以用于更新数据库架构和播种数据库。

![Web.config 文件中的连接字符串](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image26.png)

可以在*ContosoUniversity\obj\Release\Package\PackageTmp\Web.config*的计算机上查找 Web.config 文件的已部署版本。你可以通过使用 FTP 访问已部署的*Web.config*文件本身。 有关说明，请参阅[使用 Visual Studio 进行 ASP.NET Web 部署：部署代码更新](xref:web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update)。 按照以 "使用 FTP 工具" 开头的说明操作，需要以下三项内容： FTP URL、用户名和密码。 "

> [!NOTE]
> Web 应用不会实现安全性，因此查找 URL 的任何人都可以更改数据。 有关如何保护网站的说明，请参阅[将包含成员资格、OAuth 和 SQL 数据库的 secure ASP.NET MVC 应用程序部署到 Azure](/aspnet/core/security/authorization/secure-data)。 可以通过在 Visual Studio 中使用 Azure 管理门户或**服务器资源管理器**停止服务来阻止其他人使用该站点。

![停止应用服务菜单项](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/_static/server-explorer-stop-app-service.png)

## <a name="advanced-migrations-scenarios"></a>高级迁移方案

如果你通过按本教程中的说明自动运行迁移来部署数据库，并且你要部署到在多台服务器上运行的网站，则可能会收到多个服务器尝试同时运行迁移。 迁移是原子的，因此，如果两个服务器尝试运行相同的迁移，则将会成功，另一个服务器将失败（假定操作无法完成两次）。 在这种情况下，如果想要避免这些问题，可以手动调用迁移，并设置自己的代码，使其只发生一次。 有关详细信息，请参阅 Rowan 莎莎博客和[Migrate.exe](/ef/ef6/modeling/code-first/migrations/migrate-exe)上的[代码中的运行和脚本迁移](http://romiller.com/2012/02/09/running-scripting-migrations-from-code/)（用于从命令行执行迁移）。

有关其他迁移方案的信息，请参阅[迁移 Screencast 系列](https://blogs.msdn.com/b/adonet/archive/2014/03/12/migrations-screencast-series.aspx)。

## <a name="update-specific-migration"></a>更新特定迁移

`update-database -target MigrationName`

`update-database -target MigrationName`命令运行目标迁移。

## <a name="ignore-migration-changes-to-database"></a>忽略数据库的迁移更改

`Add-migration MigrationName -ignoreChanges`

`ignoreChanges`使用当前模型作为快照创建空迁移。

## <a name="code-first-initializers"></a>Code First 初始值设定项

在 "部署" 部分中，你看到了正在使用的[MigrateDatabaseToLatestVersion](https://msdn.microsoft.com/library/hh829476(v=vs.103).aspx)初始值设定项。 Code First 还提供其他初始值设定项，包括[CreateDatabaseIfNotExists](https://msdn.microsoft.com/library/gg679221(v=vs.103).aspx) （默认值）、 [DropCreateDatabaseIfModelChanges](https://msdn.microsoft.com/library/gg679604(v=VS.103).aspx) （以前使用过）和[DropCreateDatabaseAlways](https://msdn.microsoft.com/library/gg679506(v=VS.103).aspx)。 `DropCreateAlways`初始值设定项可用于设置单元测试的条件。 您还可以编写自己的初始值设定项，如果您不想等到应用程序从数据库中读取或写入数据，则可以显式调用初始值设定项。

有关初始值设定项的详细信息，请参阅[实体框架 Code First 中的数据库初始值设定项](http://www.codeguru.com/csharp/article.php/c19999/Understanding-Database-Initializers-in-Entity-Framework-Code-First.htm)和本书编程的第6章[实体框架：](http://shop.oreilly.com/product/0636920022220.do)通过 Julie Lerman 和 Rowan 莎莎 Code First。

## <a name="get-the-code"></a>获取代码

[下载完成的项目](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a>其他资源

可在[ASP.NET 数据访问-推荐的资源](xref:whitepapers/aspnet-data-access-content-map)中找到指向其他实体框架资源的链接。

## <a name="next-steps"></a>后续步骤

在本教程中，你将了解：

> [!div class="checklist"]
> * 已启用 Code First 迁移
> * 在 Azure 中部署应用（可选）

转到下一篇文章，了解如何为 ASP.NET MVC 应用程序创建更复杂的数据模型。
> [!div class="nextstepaction"]
> [创建更复杂的数据模型](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md)

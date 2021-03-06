---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/strategies-for-database-development-and-deployment-cs
title: 数据库开发和部署策略（C#） |Microsoft Docs
author: rick-anderson
description: 首次部署数据驱动的应用程序时，可以在开发环境中盲目地将数据库复制到生产环境中。 B. 。
ms.author: riande
ms.date: 04/23/2009
ms.assetid: 3e8b0627-3eb7-488e-807e-067cba7cec05
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/strategies-for-database-development-and-deployment-cs
msc.type: authoredcontent
ms.openlocfilehash: 4d9dbaf41926b43af171619ee34f58da84b5dab1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78509384"
---
# <a name="strategies-for-database-development-and-deployment-c"></a>数据库开发和部署策略 (C#)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载 PDF](https://download.microsoft.com/download/C/3/9/C391A649-B357-4A7B-BAA4-48C96871FEA6/aspnet_tutorial10_DBDevel_cs.pdf)

> 首次部署数据驱动的应用程序时，可以在开发环境中盲目地将数据库复制到生产环境中。 但在后续部署中执行一个直接复制将覆盖输入到生产数据库中的所有数据。 相反，部署数据库需要应用自上一次部署到生产数据库后对开发数据库所做的更改。 本教程将探讨这些挑战，并提供各种策略来帮助 chronicling 和应用自上次部署以来对数据库所做的更改。

## <a name="introduction"></a>简介

如前面的教程中所述，部署 ASP.NET 应用程序需要将相关内容从开发环境复制到生产环境。 部署不是一次性的事件，而是在每次发布软件的新版本时或发现并解决了 bug 或安全问题时出现的情况。 将 ASP.NET 页面、图像、JavaScript 文件和其他此类文件复制到生产环境时，无需考虑到自上次部署后这些文件如何发生更改。 你可以盲目地将文件复制到生产，并覆盖现有内容。 遗憾的是，这种简易性并不会扩展到部署数据库。

首次部署数据驱动的应用程序时，可以在开发环境中盲目地将数据库复制到生产环境中。 但在后续部署中执行一个直接复制将覆盖输入到生产数据库中的所有数据。 相反，部署数据库需要应用自上一次部署到生产数据库后对开发数据库所做的*更改*。 本教程将探讨这些挑战，并提供各种策略来帮助 chronicling 和应用自上次部署以来对数据库所做的更改。

## <a name="the-challenges-of-deploying-a-database"></a>部署数据库的挑战

在第一次部署数据驱动的应用程序之前，只需要一个数据库（即开发环境中的数据库），这就是在第一次部署数据驱动的应用程序时，在将数据库复制到开发环境部署到生产环境。 但在部署应用程序后，有两个数据库副本：一个在开发中，另一个在生产中。

在部署之间，开发和生产数据库可能会变得不同步。尽管生产数据库架构保持不变，但在添加新功能时，开发数据库的架构可能会更改。 您可以添加或删除列、表、视图或存储过程。 还可能会将重要数据添加到开发数据库。 许多数据驱动的应用程序包括用硬编码的、特定于应用程序的数据（不是用户可编辑的）填充的查找表。 例如，拍卖网站可能有一个下拉列表，其中包含用于描述要 auctioned 的项的条件的选项： "新"、"好" 和 "公平"。 通常最好将这些选项置于数据库表中，而不是直接在下拉列表中对这些选项进行硬编码。 如果在开发过程中将名为 "差" 的新条件添加到表中，则在部署应用程序时，需要将此同一记录添加到生产数据库中的查找表。

理想情况下，部署数据库需要将数据库从开发环境复制到生产环境中。 但请记住，在部署应用程序并恢复开发后，将使用真实用户的实际数据填充生产数据库。 因此，如果只是在下一次部署时将数据库从开发环境复制到生产环境中，则会覆盖生产数据库，并丢失现有数据。 最终的结果是，部署数据库，以应用自上次部署以来对开发数据库所做的更改。

由于部署数据库涉及应用架构中的更改（可能是自上次部署以来的数据），因此必须维护更改的历史记录（或在部署时确定），以便可以在生产环境中应用这些更改。 有多种方法可用于管理和应用数据模型更改。

### <a name="defining-the-baseline"></a>定义基线

若要维护对应用程序数据库所做的更改，需要有一些开始状态，即要将更改应用到的基线。 一种极端情况下，启动状态可以是没有表、视图或存储过程的空数据库。 此类基线将导致大更改日志，因为它必须包括创建所有数据库表、视图和存储过程，以及在初始部署之后所做的任何更改。 在该色谱的另一端，你可以将基线设置为最初部署到生产环境的数据库的版本。 此选择将导致更小的更改日志，因为它仅包含在首次部署后对数据库所做的更改。 这是我喜欢的方法。 当然，您可以选择一种更多的道路方法，将基线定义为在最初创建数据库与首次部署数据库之间的某个时间点。

选择基线后，可考虑生成可执行的 SQL 脚本来重新创建基线版本。 利用此类脚本，可以快速重新创建数据库的基准版本。 此功能在大型项目中特别有用，其中可能有多个开发人员在使用项目或其他环境（如测试或过渡），每个开发人员都需要自己的数据库副本。

有多种工具可用于生成基线版本的 SQL 脚本。 从 SQL Server Management Studio （SSMS）中，可以右键单击数据库，然后单击 "任务" 子菜单，然后选择 "生成脚本" 选项。 这将启动脚本向导，您可以通过该向导来生成包含用于创建数据库对象的 SQL 命令的文件。 另一种方法是数据库发布向导，它可以生成 SQL 命令，不仅可以创建数据库架构，还可以生成数据库表中的数据。 "数据库发布向导" 已详细介绍了 "*部署数据库*" 教程。 不管使用哪种工具，最终都应该有一个可用于重新创建数据库基准版本的脚本文件（如果需要）。

## <a name="documenting-the-database-changes-in-prose"></a>记录 Prose 中的数据库更改

在开发阶段维护数据模型更改日志的最简单方法是在 prose 中记录更改。 例如，如果在开发已部署的应用程序的过程中，将一个新列添加到 `Employees` 表中，从 `Orders` 表中删除一列，然后添加一个新表（`ProductCategories`），则需要维护包含以下历史记录的文本文件或 Microsoft Word 文档：

<a id="0.4_table01"></a>

| **更改日期** | **更改详细信息** |
| --- | --- |
| 2009-02-03: | 向 `Employees` 表中添加了列 `DepartmentID` （`int`，而非 NULL）。 向 `Employees.DepartmentID`添加了 `Departments.DepartmentID` 的外键约束。 |
| 2009-02-05: | 从 `Orders` 表中删除了列 `TotalWeight`。 已在关联的 `OrderDetails` 记录中捕获的数据。 |
| 2009-02-12: | 已创建 `ProductCategories` 表。 有三列： `ProductCategoryID` （`int`、`IDENTITY`、`NOT NULL`）、`CategoryName` （`nvarchar(50)`、`NOT NULL`）和 `Active` （`bit`、`NOT NULL`）。 已将 primary key 约束添加到 `ProductCategoryID`，将默认值1添加到 `Active`。 |

此方法有许多缺点。 对于初学者来说，无希望自动化。 无论何时需要将这些更改应用到数据库（例如，在部署应用程序时），开发人员都必须手动实现每个更改（一次一个）。 此外，如果您需要使用更改日志重构基线中的特定版本的数据库，则执行此操作将需要更多的时间，因为日志大小会增长。 此方法的另一个缺点是，每个更改日志条目的清晰度和详细程度会留给记录更改的人员。 在具有多个开发人员的团队中，某些开发人员可能会提供比其他开发人员更详细、更具可读性或更精确的条目。 此外，还可能会出现打字错误和其他与人工相关的数据输入错误。

在 prose 中记录数据库更改的主要好处是简单。 你不需要熟悉用于创建和更改数据库对象的 SQL 语法。 相反，可以在 prose 中记录更改，并通过 SQL Server Management Studio s 图形用户界面实现这些更改。

在 prose 中维护您的更改日志是不可否认的，不是非常复杂的，也不能很好地用于某些项目，例如很大范围内的项目、经常更改数据模型，或者涉及多个开发人员。 但我已经了解，这种方法在仅对数据模型进行了偶尔更改的小型单 man 项目中非常有效，而在 SQL 语法中，在创建和更改数据库对象的情况下，有条件的开发人员没有更好的背景。

> [!NOTE]
> 尽管更改日志中的信息在技术上是在部署时才需要，但建议保留更改的历史记录。 不过，请考虑为每个数据库版本提供不同的更改日志文件，而不是保留一个不断增长的更改日志文件。 通常，每次部署数据库时，您都需要对数据库进行版本。 通过维护更改日志的日志，你可以从基线开始，通过执行从版本1开始的更改日志脚本来重新创建任何数据库版本，并继续，直到你到达需要重新创建的版本为止。

## <a name="recording-the-sql-change-statements"></a>记录 SQL Change 语句

在 prose 中维护更改日志的主要缺点是缺乏自动化。 理想情况下，在部署时实施对生产数据库的数据库更改很简单，只需单击一个按钮即可执行脚本，而无需手动执行指令列表。 通过维护包含用于更改数据模型的 SQL 命令的更改日志，可以实现这种自动化。

SQL 语法包含多个用于创建和修改各种数据库对象的语句。 例如，执行时[*CREATE TABLE 语句*](https://msdn.microsoft.com/library/ms174979.aspx)将创建具有指定列和约束的新表。 [*ALTER TABLE 语句*](https://msdn.microsoft.com/library/ms190273.aspx)修改现有的表，添加、删除或修改其列或约束。 还提供了用于创建、修改和删除索引、视图、用户定义函数、存储过程、触发器和其他数据库对象的语句。

返回到我们之前的示例，在开发已部署的应用程序的过程中，会将一个新列添加到 `Employees` 表中，从 `Orders` 表中删除一列，然后添加一个新表（`ProductCategories`）。 此类操作会导致更改日志文件包含以下 SQL 命令：

[!code-sql[Main](strategies-for-database-development-and-deployment-cs/samples/sample1.sql)]

在部署时将这些更改推送到生产数据库的操作是单击操作：打开 SQL Server Management Studio，连接到生产数据库，打开新的查询窗口，粘贴更改日志的内容，然后单击 "执行" 以运行脚本。

## <a name="using-a-comparison-tool-to-synchronize-the-data-models"></a>使用比较工具同步数据模型

在 prose 中记录数据库更改很简单，但实施更改需要开发人员每次对生产数据库进行一次更改;记录更改 SQL 命令，就像单击按钮一样简单快捷地在生产数据库上实现这些更改，但需要学习和掌握用于创建和更改数据库对象的 SQL 语句和语法。 数据库比较工具最适用于这两种方法，并放弃最差。

数据库比较工具比较两个数据库的架构或数据，并显示摘要报告，其中显示了数据库的不同之处。 然后，单击按钮即可生成用于同步一个或多个数据库对象的 SQL 命令。 简而言之，可以在部署时使用数据库比较工具比较开发数据库和生产数据库，生成包含 SQL 命令的文件，该文件在执行时将应用对生产数据库 s 架构的更改，使其镜像开发数据库架构。

许多不同的供应商提供了各种第三方数据库比较工具。 其中一个例子就是[*SQL 比较*](http://www.red-gate.com/products/SQL_Compare/)（[*红色入口软件*](http://www.red-gate.com/)）。 让我们逐步完成使用 SQL 比较来比较和同步开发和生产数据库架构的过程。

> [!NOTE]
> 撰写本文时，SQL 比较的当前版本是版本7.1，标准版的成本为 $395。 可以通过下载为期14天的免费试用版进行跟踪。

当 SQL 比较开始时，将打开 "比较项目" 对话框，其中显示了已保存的 SQL 比较项目。 创建新项目。 这会启动项目配置向导，该向导会提示输入要比较的数据库的有关信息（请参阅图1）。 输入用于开发和生产环境数据库的信息。

[![比较开发和生产数据库](strategies-for-database-development-and-deployment-cs/_static/image2.jpg)](strategies-for-database-development-and-deployment-cs/_static/image1.jpg)

**图 1**：比较开发和生产数据库（[单击以查看完全大小的图像](strategies-for-database-development-and-deployment-cs/_static/image3.jpg)）

> [!NOTE]
> 如果你的开发环境数据库是网站的 `App_Data` 文件夹中的 SQL Express Edition 数据库文件，则需要在 SQL Server Express 数据库服务器中注册数据库，以便从图1所示的对话框中选择该数据库。 实现此目的的最简单方法是打开 SQL Server Management Studio （SSMS），连接到 SQL Server Express 数据库服务器，然后附加数据库。 如果你的计算机上未安装 SSMS，则可以下载并安装免费[*SQL Server 2008 Management Studio Basic 版本*](https://www.microsoft.com/downloads/details.aspx?FamilyId=7522A683-4CB2-454E-B908-E805E9BD4E28&amp;displaylang=en)。

除了选择要比较的数据库之外，还可以在 "选项" 选项卡中指定各种比较设置。你可能想要启用的一个选项是 "忽略约束和索引名称"。 请记住，在前面的教程中，我们将应用程序服务数据库对象添加到了开发和生产数据库中。 如果使用 `aspnet_regsql.exe` 工具在生产数据库上创建这些对象，则会发现在开发数据库和生产数据库之间，主键和唯一约束名称有所不同。 因此，SQL 比较会将所有应用程序服务表标记为不同。 您可以取消选中 "忽略约束和索引名称" 并同步约束名称，或指示 SQL 比较忽略这些差异。

选择要比较的数据库（并查看比较选项）后，单击 "立即比较" 按钮开始比较。 在接下来的几秒内，SQL 比较会检查两个数据库的架构，并生成有关它们之间的差异的报告。 我有意对开发数据库进行了一些修改，以显示 SQL 比较接口中如何注明此类差异。 如图2所示，我将 `BirthDate` 列添加到 `Authors` 表中，从 `Books` 表中删除了 `ISBN` 列，并添加了一个新的表 `Ratings`，这旨在让用户访问站点速率审阅的书籍。

> [!NOTE]
> 本教程中所做的数据模型更改已完成，可以使用数据库比较工具进行说明。 以后的教程中将不会在数据库中发现这些更改。

[![SQL 比较列出了开发数据库和生产数据库之间的差异](strategies-for-database-development-and-deployment-cs/_static/image5.jpg)](strategies-for-database-development-and-deployment-cs/_static/image4.jpg)

**图 2**： SQL 比较列出了开发数据库和生产数据库之间的差异（[单击查看完全大小的映像](strategies-for-database-development-and-deployment-cs/_static/image6.jpg)）

SQL 比较将数据库对象分解为多个组，快速显示两个数据库中存在的对象，但它们不同，其中的对象存在于一个数据库中，而不存在于另一个数据库中，哪些对象是相同的。 正如您所看到的，两个数据库中都存在两个对象，但两者不同：添加了列的 `Authors` 表和已删除一个列的 `Books` 表。 只有开发数据库存在一个对象，即新创建的 `Ratings` 表。 这两个数据库中的对象都是相同的。117

选择数据库对象将显示 "SQL 差异" 窗口，其中显示了这些对象的不同之处。 "SQL 差异" 窗口（如图2所示）突出显示了开发数据库中的 `Authors` 表具有 `BirthDate` 列，该列在生产数据库的 `Authors` 表中找不到。

查看差异并选择想要同步的对象后，下一步是生成更新生产数据库架构以匹配开发数据库所需的 SQL 命令。 这是通过同步向导实现的。 同步向导可确认要同步的对象并概述操作计划（请参阅图3）。 可以立即同步数据库，也可以生成包含可随时运行的 SQL 命令的脚本。

[![使用同步向导同步数据库架构](strategies-for-database-development-and-deployment-cs/_static/image8.jpg)](strategies-for-database-development-and-deployment-cs/_static/image7.jpg)

**图 3**：使用同步向导同步数据库架构（[单击查看完全大小的映像](strategies-for-database-development-and-deployment-cs/_static/image9.jpg)）

数据库比较工具（如红色入口软件的 SQL 比较）会将对开发数据库架构所做的更改应用到生产数据库，就像点击一样简单。

> [!NOTE]
> SQL 比较比较并同步两个数据库*架构*。 遗憾的是，它不比较和同步两个数据库表中的数据。 红色入口软件提供了一种名为[*Sql 数据比较*](http://www.red-gate.com/products/SQL_Data_Compare/)的产品，它在两个数据库之间比较并同步数据，但它是不同于 SQL 比较的一种产品，另一种是 $395。

## <a name="taking-the-application-offline-during-deployment"></a>在部署过程中使应用程序脱机

正如我们在这些教程中所见到的，部署是涉及多个步骤的过程：将 ASP.NET 页面、母版页、CSS 文件、JavaScript 文件、图像和其他必要的内容从开发环境复制到生产环境环境如果需要，复制特定于生产环境的配置信息;并将更改应用到自上一次部署以来的数据模型。 根据文件的数量和数据库的复杂性，可能需要几秒钟到几分钟的时间才能完成这些步骤。 在此窗口中，web 应用程序位于 flux 中，访问站点的用户可能会遇到错误或意外行为。

部署网站时，最好是在部署完成之前使 web 应用程序 "脱机"。 使应用程序脱机（并在部署过程完成后进行备份）非常简单，只需上传文件，然后将其删除即可。 从 ASP.NET 2.0 开始，应用程序根目录中的一个名为 `app_offline.htm` 的文件在整个网站中 "脱机"。 对该站点上的 ASP.NET 页面的任何请求都将自动使用 `app_offline.htm` 文件的内容进行响应。 删除该文件后，应用程序将重新联机。

在部署过程中使应用程序脱机，就像在开始部署过程之前将 `app_offline.htm` 文件上传到生产环境的根目录一样简单，然后在部署完成后将其删除（或将其重命名为其他内容）。 有关此技术的详细信息，请参阅 John Peterson 一文，使[*ASP.NET 应用程序脱机*](http://www.15seconds.com/issue/061207.htm)。

## <a name="summary"></a>摘要

在部署数据库时部署数据驱动的应用程序中心的主要挑战。 因为有两个版本的数据库-一个在开发环境中，另一个在生产环境中，因此在开发中添加新功能后，这两个数据库架构可能会变得不同步。 更多是，因为生产数据库是用真实用户的实际数据填充的，所以你不能用修改后的开发数据库覆盖生产数据库，就像部署构成应用程序的文件（ASP.NET 页）时，图像文件等。 相反，部署数据库需要实现自上次部署以来对生产数据库中的开发数据库所做的一系列更改。

本教程介绍了用于维护和应用数据库更改日志的三种方法。 最简单的方法是在 prose 中记录更改。 虽然这种策略使得在生产数据库上实现这些更改是一个手动过程，但它不需要了解用于创建和更改数据库对象的 SQL 命令。 更复杂的方法，以及在具有多个开发人员的大型项目或项目中更愉快的方法，是将更改记录为一系列 SQL 命令。 这极大地 hastens 将这些更改部署到目标数据库。 这两种方法的最佳方法都可以通过使用数据库比较工具来实现，例如，Red 关口 Software SQL 比较。

本教程将重点介绍如何部署数据驱动的应用程序。 下一组教程介绍了如何在生产环境中响应错误。 我们将介绍如何显示友好错误页面，而不显示死亡的黄屏。 我们将了解如何记录错误的详细信息以及如何在发生此类错误时发出警报。

很高兴编程！

> [!div class="step-by-step"]
> [上一页](configuring-a-website-that-uses-application-services-cs.md)
> [下一页](displaying-a-custom-error-page-cs.md)

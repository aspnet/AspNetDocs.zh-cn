---
uid: web-forms/overview/data-access/caching-data/using-sql-cache-dependencies-vb
title: 使用 SQL 缓存依赖项（VB） |Microsoft Docs
author: rick-anderson
description: 最简单的缓存策略是允许缓存数据在指定的时间段后过期。 但这种简单的方法意味着缓存的数据 maintai
ms.author: riande
ms.date: 05/30/2007
ms.assetid: bd347d93-4251-4532-801c-a36f2dfa7f96
msc.legacyurl: /web-forms/overview/data-access/caching-data/using-sql-cache-dependencies-vb
msc.type: authoredcontent
ms.openlocfilehash: 7d095538bd92d50675e5fce44f5ca68e8ee6c0e8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78442904"
---
# <a name="using-sql-cache-dependencies-vb"></a>使用 SQL 缓存依赖项 (VB)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_61_VB.zip)或[下载 PDF](using-sql-cache-dependencies-vb/_static/datatutorial61vb1.pdf)

> 最简单的缓存策略是允许缓存数据在指定的时间段后过期。 但这种简单的方法意味着缓存的数据与其基础数据源不保持关联，导致陈旧的数据过长或当前过期的数据太快过期。 更好的方法是使用 SqlCacheDependency 类，以便在 SQL 数据库中修改数据之前，数据将一直保持缓存状态。 本教程将向您介绍如何操作。

## <a name="introduction"></a>简介

使用 "体系结构" 教程中的 ObjectDataSource 和[缓存数据](caching-data-in-the-architecture-vb.md)在[缓存数据](caching-data-with-the-objectdatasource-vb.md)中检查的缓存方法使用基于时间的过期，在指定的时间段后从缓存中逐出数据。 这种方法是在缓存性能提高与数据过期情况之间取得平衡的最简单方法。 通过选择时间为*x*秒的时间，页面开发人员只需为*x*秒的缓存提供性能优势，但 concedes 的数据将永远不会超过最长*x*秒的时间。 当然，对于静态数据， *x*可以扩展到 web 应用程序的生存期，如在[应用程序启动时缓存数据](caching-data-at-application-startup-vb.md)教程中所述。

在缓存数据库数据时，通常会选择基于时间的过期，以方便使用，但这通常是一种不充分的解决方案。 理想情况下，数据库数据将保持缓存状态，直到在数据库中修改了基础数据时;只有这样才会逐出缓存。 此方法可最大程度地提高缓存性能，并最大程度地减少过时数据的持续时间。 但是，为了享受这些权益，必须有一些系统知道何时修改了基础数据库数据，并从缓存中逐出了相应的项。 在 ASP.NET 2.0 之前，页面开发人员负责实现此系统。

ASP.NET 2.0 提供[`SqlCacheDependency` 类](https://msdn.microsoft.com/library/system.web.caching.sqlcachedependency.aspx)和必要的基础结构，以确定数据库中发生更改的时间，以便可以逐出相应的缓存项。 可通过两种方法来确定基础数据更改的时间：通知和轮询。 讨论了通知与轮询之间的差异后，我们将创建支持轮询所需的基础结构，并探索如何在声明性和编程方案中使用 `SqlCacheDependency` 类。

## <a name="understanding-notification-and-polling"></a>了解通知和轮询

可以使用两种方法来确定何时修改数据库中的数据：通知和轮询。 使用通知时，数据库将在上次执行查询后更改了特定查询的结果时，自动对 ASP.NET 运行时发出警报，此时将逐出与查询关联的缓存项。 使用轮询，数据库服务器将保留有关特定表上次更新时间的信息。 ASP.NET 运行时定期轮询数据库，以检查自将哪些表输入缓存后，哪些表发生了更改。 已修改其数据的那些表的关联缓存项被逐出。

通知选项所需的安装比轮询少，并且更精细，因为它在查询级别（而不是表级别）跟踪更改。 遗憾的是，通知仅在 Microsoft SQL Server 2005 （即非 Express 版本）的完整版中提供。 但是，轮询选项可用于从7.0 到 2005 Microsoft SQL Server 的所有版本。 由于这些教程使用 Express edition SQL Server 2005，因此我们将重点介绍如何设置和使用 "轮询" 选项。 有关 SQL Server 2005 s 通知功能的详细资源，请参阅本教程末尾的进一步阅读部分。

使用轮询时，必须将数据库配置为包含一个名为 `AspNet_SqlCacheTablesForChangeNotification` 的表，该表包含三列 `tableName`、`notificationCreated`和 `changeId`。 对于包含可能需要在 web 应用程序的 SQL 缓存依赖项中使用的数据的每个表，此表都包含一行。 `tableName` 列指定表的名称，`notificationCreated` 指示该行添加到表中的日期和时间。 `changeId` 列的类型为 `int`，其初始值为0。 每次对表进行修改时，其值都是递增的。

除了 `AspNet_SqlCacheTablesForChangeNotification` 表，数据库还需要在可能出现在 SQL 缓存依赖关系中的每个表中包含触发器。 在插入、更新或删除行时，将执行这些触发器，并递增 `AspNet_SqlCacheTablesForChangeNotification`中的表 `changeId` 值。

使用 `SqlCacheDependency` 对象缓存数据时，ASP.NET 运行时将跟踪表的当前 `changeId`。 定期检查该数据库，并逐出 `changeId` 不同于数据库中的值的任何 `SqlCacheDependency` 对象，因为不同的 `changeId` 值表明自缓存数据以来对该表进行了更改。

## <a name="step-1-exploring-theaspnet_regsqlexecommand-line-program"></a>步骤1：浏览`aspnet_regsql.exe`命令行程序

使用轮询方法时，必须将数据库设置为包含上述基础结构：预定义的表（`AspNet_SqlCacheTablesForChangeNotification`）、少量的存储过程，以及在 web 应用程序中的 SQL 缓存依赖项中可能使用的每个表的触发器。 可以通过命令行程序 `aspnet_regsql.exe`创建这些表、存储过程和触发器，该程序位于 `$WINDOWS$\Microsoft.NET\Framework\version` 文件夹中。 若要创建 `AspNet_SqlCacheTablesForChangeNotification` 表和关联的存储过程，请从命令行运行以下命令：

[!code-console[Main](using-sql-cache-dependencies-vb/samples/sample1.cmd)]

> [!NOTE]
> 若要执行这些命令，指定的数据库登录名必须在[`db_securityadmin`](https://msdn.microsoft.com/library/ms188685.aspx)和[`db_ddladmin`](https://msdn.microsoft.com/library/ms190667.aspx)角色中。 若要检查 `aspnet_regsql.exe` 命令行程序发送到数据库的 T-sql，请参阅[此博客文章](http://scottonwriting.net/sowblog/posts/10709.aspx)。

例如，若要使用 Windows 身份验证将用于轮询的基础结构添加到名为 `ScottsServer` 的数据库服务器上名为 `pubs` 的 Microsoft SQL Server 数据库，请导航到相应的目录，然后在命令行中输入以下命令：

[!code-console[Main](using-sql-cache-dependencies-vb/samples/sample2.cmd)]

添加数据库级基础结构后，需要将触发器添加到将在 SQL 缓存依赖项中使用的那些表。 再次使用 `aspnet_regsql.exe` 命令行程序，但使用 `-t` 开关指定表名称，而不是使用 `-ed` 开关来使用 `-et`，如下所示：

[!code-html[Main](using-sql-cache-dependencies-vb/samples/sample3.html)]

若要将触发器添加到 `ScottsServer`上 `pubs` 数据库的 `authors` 和 `titles` 表中，请使用：

[!code-console[Main](using-sql-cache-dependencies-vb/samples/sample4.cmd)]

对于本教程，请将触发器添加到 `Products`、`Categories`和 `Suppliers` 表中。 我们将在步骤3中介绍特定的命令行语法。

## <a name="step-2-referencing-a-microsoft-sql-server-2005-express-edition-database-inapp_data"></a>步骤2：在`App_Data` 中引用 Microsoft SQL Server 2005 Express Edition 数据库

`aspnet_regsql.exe` 命令行程序需要数据库和服务器名称才能添加必要的轮询基础结构。 但 `App_Data` 文件夹中 Microsoft SQL Server 2005 Express 数据库的数据库和服务器名称是什么？ 我发现，最简单的方法是将数据库附加到 `localhost\SQLExpress` 的数据库实例，并使用[SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx)重命名数据，而不必了解数据库和服务器的名称。 如果计算机上安装了 SQL Server 2005 的完整版本之一，则计算机上可能已安装了 SQL Server Management Studio。 如果只有 Express edition，则可以下载免费的[Microsoft SQL Server Management Studio Express edition](https://www.microsoft.com/downloads/details.aspx?displaylang=en&amp;FamilyID=C243A5AE-4BD1-4E3D-94B8-5A0F62BF7796)。

首先关闭 Visual Studio。 接下来，打开 SQL Server Management Studio 并选择使用 Windows 身份验证连接到 `localhost\SQLExpress` 服务器。

![附加到 localhost\SQLExpress 服务器](using-sql-cache-dependencies-vb/_static/image1.gif)

**图 1**：附加到 `localhost\SQLExpress` 服务器

连接到服务器后，Management Studio 将显示服务器，并为数据库和安全性等提供子文件夹。 右键单击 "数据库" 文件夹，然后选择 "附加" 选项。 此时将显示 "附加数据库" 对话框（请参阅图2）。 单击 "添加" 按钮，然后选择 web 应用程序 `App_Data` 文件夹中的 `NORTHWND.MDF` 数据库文件夹。

[![附加 NORTHWND.MDF。App_Data 文件夹中的 MDF 数据库](using-sql-cache-dependencies-vb/_static/image2.gif)](using-sql-cache-dependencies-vb/_static/image1.png)

**图 2**：从 `App_Data` 文件夹附加 `NORTHWND.MDF` 数据库（[单击查看完全大小的映像](using-sql-cache-dependencies-vb/_static/image2.png)）

这会将数据库添加到 "数据库" 文件夹。 数据库名称可能是数据库文件的完整路径，或者是[GUID](http://en.wikipedia.org/wiki/Globally_Unique_Identifier)前面预置的完整路径。 若要避免在使用 aspnet\_regsql 命令行工具时必须键入此冗长的数据库名称，请右键单击 "刚附加的数据库"，然后选择 "重命名"，将数据库重命名为更友好的名称。 我已将数据库重命名为 DataTutorials。

![将附加的数据库重命名为更友好的名称](using-sql-cache-dependencies-vb/_static/image3.gif)

**图 3**：将附加的数据库重命名为更友好的名称

## <a name="step-3-adding-the-polling-infrastructure-to-the-northwind-database"></a>步骤3：将轮询基础结构添加到 Northwind 数据库

现在，我们已将 `NORTHWND.MDF` 数据库附加到 `App_Data` 文件夹中，接下来可以添加轮询基础结构。 假设你已将数据库重命名为 DataTutorials，请运行以下四个命令：

[!code-console[Main](using-sql-cache-dependencies-vb/samples/sample5.cmd)]

运行这四个命令后，在 Management Studio 中右键单击数据库名称，然后单击 "任务" 子菜单，然后选择 "分离"。 然后关闭 Management Studio 再重新打开 Visual Studio。

重新打开 Visual Studio 后，通过服务器资源管理器钻取到数据库。 注意新表（`AspNet_SqlCacheTablesForChangeNotification`）、新存储过程和 `Products`、`Categories`和 `Suppliers` 表的触发器。

![数据库现在包括必要的轮询基础结构](using-sql-cache-dependencies-vb/_static/image4.gif)

**图 4**：数据库现在包括必要的轮询基础结构

## <a name="step-4-configuring-the-polling-service"></a>步骤4：配置轮询服务

在数据库中创建所需的表、触发器和存储过程后，最后一步是配置轮询服务，该服务是通过 `Web.config` 指定要使用的数据库和以毫秒为单位的轮询频率来完成的。 以下标记每秒轮询一次 Northwind 数据库。

[!code-xml[Main](using-sql-cache-dependencies-vb/samples/sample6.xml)]

`<add>` 元素（NorthwindDB）中的 `name` 值将可读名称与特定数据库相关联。 使用 SQL 缓存依赖项时，需要引用此处定义的数据库名称以及缓存数据所基于的表。 我们将了解如何使用 `SqlCacheDependency` 类以编程方式将 SQL 缓存依赖项与步骤6中的缓存数据相关联。

建立 SQL 缓存依赖关系后，轮询系统将每隔 `pollTime` 毫秒连接到 `<databases>` 元素中定义的数据库，并执行 `AspNet_SqlCachePollingStoredProcedure` 存储过程。 使用 `aspnet_regsql.exe` 命令行工具在第3步中添加了此存储过程-返回 `AspNet_SqlCacheTablesForChangeNotification`中每条记录的 `tableName` 和 `changeId` 值。 过时的 SQL 缓存依赖关系从缓存中逐出。

`pollTime` 设置在性能和数据过期之间引入了折衷。 小型 `pollTime` 值将增加对数据库的请求数，但会更快地逐出缓存中的陈旧数据。 较大的 `pollTime` 值可以减少数据库请求的数量，但会增加后端数据发生变化和逐出相关缓存项之间的延迟时间。 幸运的是，数据库请求正在执行一个简单的存储过程，该存储过程只返回简单的轻型表中的几个行。 但请使用不同的 `pollTime` 值进行试验，以便在应用程序的数据库访问和数据过期情况之间获得理想的平衡。 允许的最小 `pollTime` 值为500。

> [!NOTE]
> 上面的示例在 `<sqlCacheDependency>` 元素中提供了单个 `pollTime` 值，但你可以选择在 `<add>` 元素中指定 `pollTime` 值。 如果已指定多个数据库，并且想要自定义每个数据库的轮询频率，此方法非常有用。

## <a name="step-5-declaratively-working-with-sql-cache-dependencies"></a>步骤5：以声明方式使用 SQL 缓存依赖项

在步骤1到步骤4中，我们介绍了如何设置所需的数据库基础结构并配置轮询系统。 使用此基础结构后，现在可以使用编程方式或声明性技术，将项添加到数据缓存，其中包含关联的 SQL 缓存依赖项。 在此步骤中，我们将检查如何以声明方式使用 SQL 缓存依赖项。 在步骤6中，我们将介绍编程方法。

[利用 objectdatasource 教程缓存数据](caching-data-with-the-objectdatasource-vb.md)探讨了 objectdatasource 的声明性缓存功能。 只需将 `EnableCaching` 属性设置为 `True` 并将 `CacheDuration` 属性设置为某个时间间隔，ObjectDataSource 就会根据指定的时间间隔自动缓存从其基础对象返回的数据。 ObjectDataSource 还可以使用一个或多个 SQL 缓存依赖项。

若要以声明方式使用 SQL 缓存依赖项，请打开 `Caching` 文件夹中的 "`SqlCacheDependencies.aspx`" 页，并将 GridView 从工具箱拖到设计器上。 将 GridView `ID` 设置为 `ProductsDeclarative`，并从其智能标记中，选择将其绑定到名为 `ProductsDataSourceDeclarative`的新 ObjectDataSource。

[![创建一个名为 ProductsDataSourceDeclarative 的新 ObjectDataSource](using-sql-cache-dependencies-vb/_static/image5.gif)](using-sql-cache-dependencies-vb/_static/image3.png)

**图 5**：创建名为 `ProductsDataSourceDeclarative` 的新 ObjectDataSource （[单击以查看完全大小的映像](using-sql-cache-dependencies-vb/_static/image4.png)）

将 ObjectDataSource 配置为使用 `ProductsBLL` 类，并在 "选择" 选项卡中设置下拉列表以 `GetProducts()`。 在 "更新" 选项卡中，选择具有三个输入参数的 `UpdateProduct` 重载-`productName`、`unitPrice`和 `productID`。 在 "插入" 和 "删除" 选项卡中将下拉列表设置为 "（无）"。

[![将 UpdateProduct 重载用于三个输入参数](using-sql-cache-dependencies-vb/_static/image6.gif)](using-sql-cache-dependencies-vb/_static/image5.png)

**图 6**：将 UpdateProduct 重载用于三个输入参数（[单击以查看完全大小的图像](using-sql-cache-dependencies-vb/_static/image6.png)）

[![将 "插入" 和 "删除" 选项卡的下拉列表设置为 "（无）"](using-sql-cache-dependencies-vb/_static/image7.gif)](using-sql-cache-dependencies-vb/_static/image7.png)

**图 7**：将 "插入" 和 "删除" 选项卡的下拉列表设置为 "（无）" （[单击查看完全大小的图像](using-sql-cache-dependencies-vb/_static/image8.png)）

完成 "配置数据源" 向导后，Visual Studio 将为每个数据字段在 GridView 中创建 BoundFields 和 CheckBoxFields。 删除所有字段但 `ProductName`、`CategoryName`和 `UnitPrice`，并根据需要设置这些字段的格式。 从 GridView s 智能标记中，选中 "启用分页"、"启用排序" 和 "启用编辑" 复选框。 Visual Studio 会将 ObjectDataSource `OldValuesParameterFormatString` 属性设置为 `original_{0}`。 为了使 GridView s 编辑功能正常工作，请从声明性语法中完全删除此属性，或将其设置回默认值 `{0}`。

最后，在 GridView 上方添加标签 Web 控件，并将其 `ID` 属性设置为 `ODSEvents`，并将其 `EnableViewState` 属性设置为 "`False`"。 进行这些更改后，页的声明性标记应如下所示。 请注意，我对 GridView 字段进行了一些美观的自定义，这些字段对演示 SQL 缓存依赖项功能并不是必需的。

[!code-aspx[Main](using-sql-cache-dependencies-vb/samples/sample7.aspx)]

接下来，为 ObjectDataSource `Selecting` 事件创建事件处理程序，并在其中添加以下代码：

[!code-vb[Main](using-sql-cache-dependencies-vb/samples/sample8.vb)]

请记住，仅当从其基础对象检索数据时才会触发 ObjectDataSource `Selecting` 事件。 如果 ObjectDataSource 访问自己的缓存中的数据，则不会触发此事件。

现在，请通过浏览器访问此页。 由于我们尚未实现任何缓存，每次页面、排序或编辑网格时，该页应显示文本，选择 "触发事件"，如图8所示。

[![每次对 GridView 进行分页、编辑或排序时激发的选择事件](using-sql-cache-dependencies-vb/_static/image8.gif)](using-sql-cache-dependencies-vb/_static/image9.png)

**图 8**：每次对 GridView 进行分页、编辑或排序时都会触发 `Selecting` 事件（[单击以查看完全大小的图像](using-sql-cache-dependencies-vb/_static/image10.png)）

正如我们在[使用 ObjectDataSource 缓存数据](caching-data-with-the-objectdatasource-vb.md)中看到的那样，将 `EnableCaching` 属性设置为 `True` 会导致 ObjectDataSource 在其 `CacheDuration` 属性指定的持续时间内缓存其数据。 ObjectDataSource 还具有一个[`SqlCacheDependency` 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.sqlcachedependency.aspx)，该属性使用模式将一个或多个 SQL 缓存依赖项添加到缓存的数据中：

[!code-css[Main](using-sql-cache-dependencies-vb/samples/sample9.css)]

其中*databaseName*是 `Web.config`中 `<add>` 元素的 `name` 属性中指定的数据库名称， *tableName*是数据库表的名称。 例如，若要创建一个 ObjectDataSource，使其基于与 Northwind `Products` 表的 SQL 缓存依赖项无限缓存数据，请将 ObjectDataSource 的 `EnableCaching` 属性设置为 `True`，并将其 `SqlCacheDependency` 属性设置为 "NorthwindDB： Products"。

> [!NOTE]
> 您可以使用 SQL 缓存依赖关系*和*基于时间的过期，方法是将 `EnableCaching` 设置为 `True`，`CacheDuration` 时间间隔，并 `SqlCacheDependency` 数据库和表名称。 此 ObjectDataSource 将在达到基于时间的过期时间或轮询系统注意到基础数据库数据已更改（以先发生者为准）时逐出其数据。

`SqlCacheDependencies.aspx` 中的 GridView 显示两个表中的数据-`Products` 和 `Categories` （通过 `JOIN` 上的 `Categories`检索 product s `CategoryName` 字段）。 因此，我们希望指定两个 SQL 缓存依赖关系： NorthwindDB： Products;NorthwindDB：类别。

[![通过对产品和类别使用 SQL 缓存依赖项配置 ObjectDataSource 来支持缓存](using-sql-cache-dependencies-vb/_static/image9.gif)](using-sql-cache-dependencies-vb/_static/image11.png)

**图 9**：使用 `Products` 和 `Categories` 上的 SQL 缓存依赖项配置 ObjectDataSource 以支持缓存（[单击查看完全大小的映像](using-sql-cache-dependencies-vb/_static/image12.png)）

配置 ObjectDataSource 以支持缓存后，请通过浏览器重新访问该页面。 同样，在第一次访问时应显示选中 "激发的事件" 的文本，但分页、排序或单击 "编辑" 或 "取消" 按钮时应消失。 这是因为在将数据加载到 ObjectDataSource s 缓存中后，它将保留在那里，直到修改了 `Products` 或 `Categories` 表，或者通过 GridView 更新数据为止。

通过网格分页并注意到缺少选中 "引发的事件" 文本后，打开新的浏览器窗口，并导航到编辑、插入和删除部分（`~/EditInsertDelete/Basics.aspx`）中的基础教程。 更新产品的名称或价格。 然后，从到第一个浏览器窗口，查看不同的数据页，对网格排序，或者单击行的 "编辑" 按钮。 此时，激发的选择事件应该重新出现，因为基础数据库数据已修改（请参阅图10）。 如果未显示该文本，请稍等片刻，然后重试。 请记住，轮询服务每隔 `pollTime` 毫秒检查对 `Products` 表所做的更改，因此在更新基础数据和逐出缓存数据之间存在延迟。

[![修改产品表逐出缓存的产品数据](using-sql-cache-dependencies-vb/_static/image10.gif)](using-sql-cache-dependencies-vb/_static/image13.png)

**图 10**：修改 Products 表逐出缓存的产品数据（[单击查看完全大小的图像](using-sql-cache-dependencies-vb/_static/image14.png)）

## <a name="step-6-programmatically-working-with-thesqlcachedependencyclass"></a>步骤6：以编程方式使用`SqlCacheDependency`类

[体系结构教程中的缓存数据](caching-data-in-the-architecture-vb.md)查看了在体系结构中使用单独的缓存层的好处，而不是将缓存与 ObjectDataSource 紧密耦合起来。 在本教程中，我们创建了一个 `ProductsCL` 类，以编程方式使用数据缓存。 若要在缓存层中使用 SQL 缓存依赖项，请使用 `SqlCacheDependency` 类。

使用轮询系统时，`SqlCacheDependency` 对象必须与特定的数据库和表对相关联。 例如，下面的代码创建一个基于 Northwind 数据库 `Products` 表的 `SqlCacheDependency` 对象：

[!code-vb[Main](using-sql-cache-dependencies-vb/samples/sample10.vb)]

`SqlCacheDependency` 构造函数的两个输入参数分别为数据库名称和表名称。 与 ObjectDataSource `SqlCacheDependency` 属性一样，使用的数据库名称与 `Web.config`中 `<add>` 元素的 `name` 属性中指定的值相同。 表名是数据库表的实际名称。

若要将 `SqlCacheDependency` 与添加到数据缓存中的项相关联，请使用接受依赖项的 `Insert` 方法重载之一。 下面的代码会无限期地将*值*添加到数据缓存，但会将其与 `Products` 表中的 `SqlCacheDependency` 关联。 简而言之，*值*将保留在缓存中，直到由于内存限制被逐出或轮询系统检测到 `Products` 表自从缓存后已更改。

[!code-vb[Main](using-sql-cache-dependencies-vb/samples/sample11.vb)]

缓存层 s `ProductsCL` 类当前使用60秒的基于时间的过期时间从 `Products` 表中缓存数据。 让我们更新此类，以使其使用 SQL 缓存依赖项。 `ProductsCL` 类 s `AddCacheItem` 方法（负责将数据添加到缓存）当前包含以下代码：

[!code-vb[Main](using-sql-cache-dependencies-vb/samples/sample12.vb)]

更新此代码以使用 `SqlCacheDependency` 对象，而不使用 `MasterCacheKeyArray` 缓存依赖关系：

[!code-vb[Main](using-sql-cache-dependencies-vb/samples/sample13.vb)]

若要测试此功能，请将 GridView 添加到现有 `ProductsDeclarative` GridView 下的页面。 将这个新 GridView `ID` 设置为 `ProductsProgrammatic`，并通过其智能标记将其绑定到名为 `ProductsDataSourceProgrammatic`的新 ObjectDataSource。 将 ObjectDataSource 配置为使用 `ProductsCL` 类，将 "选择" 和 "更新" 选项卡中的下拉列表分别设置为 `GetProducts` 和 `UpdateProduct`。

[![将 ObjectDataSource 配置为使用 ProductsCL 类](using-sql-cache-dependencies-vb/_static/image11.gif)](using-sql-cache-dependencies-vb/_static/image15.png)

**图 11**：将 ObjectDataSource 配置为使用 `ProductsCL` 类（[单击以查看完全大小的映像](using-sql-cache-dependencies-vb/_static/image16.png)）

[![从 "选择选项卡 s" 下拉列表中选择 GetProducts 方法](using-sql-cache-dependencies-vb/_static/image12.gif)](using-sql-cache-dependencies-vb/_static/image17.png)

**图 12**：从 "选择选项卡 s" 下拉列表中选择 `GetProducts` 方法（[单击以查看完全大小的图像](using-sql-cache-dependencies-vb/_static/image18.png)）

[![从 "更新" 选项卡的下拉列表中选择 "UpdateProduct" 方法](using-sql-cache-dependencies-vb/_static/image13.gif)](using-sql-cache-dependencies-vb/_static/image19.png)

**图 13**：从 "更新" 选项卡的下拉列表中选择 "UpdateProduct" 方法（[单击以查看完全大小的图像](using-sql-cache-dependencies-vb/_static/image20.png)）

完成 "配置数据源" 向导后，Visual Studio 将为每个数据字段在 GridView 中创建 BoundFields 和 CheckBoxFields。 与添加到此页的第一个 GridView 类似，删除所有字段但 `ProductName`、`CategoryName`和 `UnitPrice`，并根据需要设置这些字段的格式。 从 GridView s 智能标记中，选中 "启用分页"、"启用排序" 和 "启用编辑" 复选框。 与 `ProductsDataSourceDeclarative` ObjectDataSource 一样，Visual Studio 会将 `ProductsDataSourceProgrammatic` ObjectDataSource s `OldValuesParameterFormatString` 属性设置为 `original_{0}`。 为了使 GridView s 编辑功能正常工作，请将此属性设置回 `{0}` （或从声明性语法中删除属性赋值）。

完成这些任务后，生成的 GridView 和 ObjectDataSource 声明性标记应如下所示：

[!code-aspx[Main](using-sql-cache-dependencies-vb/samples/sample14.aspx)]

若要测试缓存层中的 SQL 缓存依赖关系，请在 `ProductCL` 类 s `AddCacheItem` 方法中设置断点，然后开始调试。 首次访问 `SqlCacheDependencies.aspx`时，应在第一次请求数据并将其放入缓存时命中断点。 接下来，在 GridView 中移动到另一页或对其中一列进行排序。 这会导致 GridView 重新查询其数据，但应在缓存中找到数据，因为未修改 `Products` 数据库表。 如果在缓存中未找到数据，请确保计算机上有足够的可用内存，然后重试。

通过 GridView 的几个页面进行分页后，打开第二个浏览器窗口，并导航到编辑、插入和删除部分（`~/EditInsertDelete/Basics.aspx`）中的基础教程。 更新 Products 表中的记录，然后在第一个浏览器窗口中查看新页或单击某个排序标头。

在这种情况下，你将看到以下两个内容之一：将命中断点，这表示由于数据库中的更改，已逐出缓存的数据;否则，将不会命中断点，这意味着 `SqlCacheDependencies.aspx` 现在显示过时数据。 如果未命中断点，则很可能是因为数据更改后轮询服务尚未触发。 请记住，轮询服务每隔 `pollTime` 毫秒检查对 `Products` 表所做的更改，因此在更新基础数据和逐出缓存数据之间存在延迟。

> [!NOTE]
> 在 `SqlCacheDependencies.aspx`中通过 GridView 编辑某个产品时，更有可能出现这种延迟。 在[体系结构中的缓存数据](caching-data-in-the-architecture-vb.md)教程中，我们添加了 `MasterCacheKeyArray` 缓存依赖关系，以确保通过 `ProductsCL` 类 `UpdateProduct` 方法编辑的数据已从缓存中逐出。 但是，在此步骤中修改 `AddCacheItem` 方法时，我们将替换此缓存依赖关系，因此 `ProductsCL` 类将继续显示缓存的数据，直到轮询系统记录对 `Products` 表的更改。 本文将介绍如何在步骤7中重新引入 `MasterCacheKeyArray` 缓存依赖关系。

## <a name="step-7-associating-multiple-dependencies-with-a-cached-item"></a>步骤7：将多个依赖项与缓存项关联

请记住，在更新与产品相关的任何数据时，将使用 `MasterCacheKeyArray` 缓存依赖关系来确保从缓存中逐出与产品相关的*所有*数据。 例如，`GetProductsByCategoryID(categoryID)` 方法为每个唯一的*类别 id*值缓存 `ProductsDataTables` 实例。 如果其中一个对象被逐出，则 `MasterCacheKeyArray` 缓存依赖项可确保其他对象也被删除。 如果没有此缓存依赖项，则在修改缓存的数据时，可能存在其他缓存的产品数据可能已过期。 因此，在使用 SQL 缓存依赖项时，必须维护 `MasterCacheKeyArray` 缓存依赖项。 但是，数据缓存 `Insert` 方法仅允许单个依赖项对象。

此外，在使用 SQL 缓存依赖项时，可能需要将多个数据库表关联为依赖项。 例如，在 `ProductsCL` 类中缓存的 `ProductsDataTable` 包含每个产品的类别和供应商名称，但是 `AddCacheItem` 方法只使用对 `Products`的依赖项。 在这种情况下，如果用户更新类别或供应商的名称，则缓存的产品数据将保留在缓存中，并将过期。 因此，我们想要使缓存的产品数据不仅依赖于 `Products` 表，还取决于 `Categories` 和 `Suppliers` 表。

[`AggregateCacheDependency` 类](https://msdn.microsoft.com/library/system.web.caching.aggregatecachedependency.aspx)提供一种将多个依赖项与缓存项相关联的方法。 首先创建 `AggregateCacheDependency` 实例。 接下来，使用 `AggregateCacheDependency` s `Add` 方法添加依赖项集。 以后在数据缓存中插入项时，将传入 `AggregateCacheDependency` 实例。 如果*任何*`AggregateCacheDependency` 实例的依赖项发生更改，则将逐出缓存的项。

下面显示了 `ProductsCL` 类 `AddCacheItem` 方法的更新代码。 方法将创建 `MasterCacheKeyArray` 缓存依赖项以及 `Products`、`Categories`和 `Suppliers` 表的 `SqlCacheDependency` 对象。 这全部合并为一个名为 `aggregateDependencies`的 `AggregateCacheDependency` 对象，然后将该对象传递到 `Insert` 方法。

[!code-vb[Main](using-sql-cache-dependencies-vb/samples/sample15.vb)]

请测试此新代码。现在，对 `Products`、`Categories`或 `Suppliers` 表的更改会导致缓存的数据被逐出。 此外，`ProductsCL` 类 `UpdateProduct` 方法（在通过 GridView 编辑产品时调用）可逐出 `MasterCacheKeyArray` 缓存依赖关系，这会使缓存的 `ProductsDataTable` 逐出，并在下一个请求中重新检索数据。

> [!NOTE]
> SQL 缓存依赖项还可与[输出缓存](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/caching/output.aspx)一起使用。 有关此功能的演示，请参阅：将[ASP.NET Output 缓存与 SQL Server 配合使用](https://msdn.microsoft.com/library/e3w8402y(VS.80).aspx)。

## <a name="summary"></a>摘要

缓存数据库数据时，数据在数据库中被修改之前，理想情况下将保留在缓存中。 使用 ASP.NET 2.0，可以在声明性和编程方案中创建和使用 SQL 缓存依赖项。 此方法的一大挑战是在数据被修改时发现。 Microsoft SQL Server 2005 的完整版本提供了通知功能，可以在查询结果发生更改时向应用程序发出警报。 对于 SQL Server 2005 和早期版本 SQL Server 的 Express 版本，必须改用轮询系统。 幸运的是，设置必要的轮询基础结构相当简单。

很高兴编程！

## <a name="further-reading"></a>其他阅读材料

有关本教程中讨论的主题的详细信息，请参阅以下资源：

- [在 Microsoft SQL Server 2005 中使用查询通知](https://msdn.microsoft.com/library/ms175110.aspx)
- [创建查询通知](https://msdn.microsoft.com/library/ms188669.aspx)
- [用 `SqlCacheDependency` 类在 ASP.NET 中进行缓存](https://msdn.microsoft.com/library/ms178604(VS.80).aspx)
- [ASP.NET SQL Server 注册工具（`aspnet_regsql.exe`）](https://msdn.microsoft.com/library/ms229862(vs.80).aspx)
- [`SqlCacheDependency` 概述](http://www.aspnetresources.com/blog/sql_cache_depedency_overview.aspx)

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)，已在使用 Microsoft Web 技术，自1998开始。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以[mitchell@4GuysFromRolla.com访问。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特别感谢

此教程系列由许多有用的审阅者查看。 本教程的主管评审者是 Marko Rangel、Teresa Murphy 和 Hilton Giesenow。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在mitchell@4GuysFromRolla.com放置一行[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](caching-data-at-application-startup-vb.md)

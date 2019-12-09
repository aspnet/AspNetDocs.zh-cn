---
uid: web-forms/overview/data-access/paging-and-sorting/efficiently-paging-through-large-amounts-of-data-cs
title: 通过大量数据有效分页（C#） |Microsoft Docs
author: rick-anderson
description: 在处理大量数据时，数据呈现控件的默认分页选项不合适，因为它的基础数据源控件 retriev 。
ms.author: riande
ms.date: 08/15/2006
ms.assetid: 59c01998-9326-4ecb-9392-cb9615962140
msc.legacyurl: /web-forms/overview/data-access/paging-and-sorting/efficiently-paging-through-large-amounts-of-data-cs
msc.type: authoredcontent
ms.openlocfilehash: a3e9562035cb24987b01fcdff5fbfb5fa8a1f894
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74629747"
---
# <a name="efficiently-paging-through-large-amounts-of-data-c"></a>通过大量数据有效分页 (C#)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_25_CS.exe)或[下载 PDF](efficiently-paging-through-large-amounts-of-data-cs/_static/datatutorial25cs1.pdf)

> 当处理大量数据时，数据呈现控件的默认分页选项不合适，因为即使只显示数据的子集，其基础数据源控件也会检索所有记录。 在这种情况下，必须启用自定义分页。

## <a name="introduction"></a>简介

如前面的教程中所述，可以通过以下两种方式之一实现分页：

- 只需在数据 Web 控件的智能标记中选中 "启用分页" 选项即可实现**默认分页**;但是，无论何时查看数据页，ObjectDataSource 都将检索*所有*记录，即使该页只显示其中的一个子集。
- **自定义分页**通过只从数据库中检索那些需要为用户请求的特定数据页显示的记录，从而提高了默认分页的性能;但是，自定义分页的实现工作比默认分页要多得多，

由于实现的方便性，只需选中一个复选框即可完成！ 默认分页是一个极具吸引力的选项。 不过，在检索所有记录时，它的 na 方法会使其成为可能的选择，当通过足够大的数据量或包含多个并发用户的站点进行分页时。 在这种情况下，必须启用自定义分页，才能提供响应式系统。

自定义分页的难题是，可以编写一个查询，该查询返回特定数据页所需的精确记录集。 幸运的是，Microsoft SQL Server 2005 为排名结果提供了一个新的关键字，这使我们可以编写一个查询，以便有效地检索正确的记录子集。 在本教程中，我们将了解如何使用此新的 SQL Server 2005 关键字在 GridView 控件中实现自定义分页。 尽管自定义分页的用户界面与默认分页的用户界面完全相同，但使用自定义分页从一个页面单步执行到下一个页面的速度要快于默认分页。

> [!NOTE]
> 自定义分页所表现出的确切性能提升取决于正在分页的记录总数以及要放置在数据库服务器上的负载。 在本教程结束时，我们将介绍一些大致的指标，其中展示了通过自定义分页获得的性能优势。

## <a name="step-1-understanding-the-custom-paging-process"></a>步骤1：了解自定义分页过程

在对数据进行分页时，页面中显示的准确记录取决于所请求的数据页和每页显示的记录数。 例如，假设我们想要翻阅81产品，每页显示10种产品。 查看第一页时，d 需要产品1到 10;查看第二页时，我们对产品11至20感兴趣，依此类推。

有三个变量用于决定需要检索的记录以及应如何呈现分页接口：

- **起始行索引**要显示的数据页中第一行的索引;可以通过将页索引与每页显示的记录相乘，然后再添加，来计算此索引。 例如，在每次对记录10进行分页时，对于第一页（其页索引为0），起始行索引为 0 \* 10 + 1 或 1;对于第二页（其页索引为1），起始行索引为 1 \* 10 + 1 或11。
- **最大行**数每页显示的最大记录数。 在最后一页中，此变量称为最大行数，返回的记录可能少于页面大小。 例如，在每页的 81 products 10 个记录分页时，第九页和最后一页将只有一条记录。 不过，如果没有页面，将显示超出最大行值的记录。
- **总记录**数：要分页到的记录总数。 尽管此变量不需要确定要为给定页面检索的记录，但它确实规定了分页接口。 例如，如果要将81的产品寻呼到其中，则分页接口知道在分页 UI 中显示九个页码。

通过默认分页，开始行索引计算为页索引的积和页面大小加一，而最大行只是页面大小。 由于在呈现任何数据页时，默认分页将从数据库中检索所有记录，因此，每行的索引都是已知的，从而使移动到起始行索引行成为一项重要任务。 而且，总记录计数随时可用，因为它只是 DataTable 中的记录数（或用来保存数据库结果的任何对象）。

给定起始行索引和最大行变量，自定义分页实现只能返回从起始行索引开始到最大行数后的记录的精确子集。 自定义分页提供两个难题：

- 我们必须能够有效地将行索引与要分页的整个数据中的每一行关联起来，以便我们可以开始在指定的起始行索引处返回记录
- 我们需要提供分页的记录总数

在接下来的两个步骤中，我们将检查需要对这两个挑战作出响应的 SQL 脚本。 除了 SQL 脚本之外，我们还需要在 DAL 和 BLL 中实现方法。

## <a name="step-2-returning-the-total-number-of-records-being-paged-through"></a>步骤2：返回分页的记录总数

在我们检查如何检索所显示页面的准确记录子集之前，让我们先来看看如何返回分页的记录总数。 此信息是正确配置寻呼用户界面所必需的。 可以使用[`COUNT` 聚合函数](https://msdn.microsoft.com/library/ms175997.aspx)获取特定 SQL 查询返回的记录总数。 例如，若要确定 `Products` 表中的记录总数，可以使用以下查询：

[!code-sql[Main](efficiently-paging-through-large-amounts-of-data-cs/samples/sample1.sql)]

让我们向 DAL 添加一个返回此信息的方法。 具体而言，我们将创建一个名为 `TotalNumberOfProducts()` 的 DAL 方法，该方法执行上面所示的 `SELECT` 语句。

首先打开 `App_Code/DAL` 文件夹中 `Northwind.xsd` 类型化的数据集文件。 接下来，右键单击设计器中的 `ProductsTableAdapter`，然后选择 "添加查询"。 如前面的教程中所示，这将使我们能够将新方法添加到 DAL，在调用该方法时，将执行特定的 SQL 语句或存储过程。 与前面教程中的 TableAdapter 方法一样，对于这种方法，选择使用即席 SQL 语句。

![使用即席 SQL 语句](efficiently-paging-through-large-amounts-of-data-cs/_static/image1.png)

**图 1**：使用即席 SQL 语句

在下一个屏幕上，可以指定要创建的查询类型。 由于此查询将返回单个标量值 `Products` 表中的记录总数，请选择返回单个值选项的 `SELECT`。

![将查询配置为使用返回单个值的 SELECT 语句](efficiently-paging-through-large-amounts-of-data-cs/_static/image2.png)

**图 2**：将查询配置为使用返回单个值的 SELECT 语句

在指示要使用的查询类型后，接下来必须指定查询。

![使用 SELECT COUNT （*） FROM Products 查询](efficiently-paging-through-large-amounts-of-data-cs/_static/image3.png)

**图 3**：使用 PRODUCTS 查询中的 SELECT COUNT （\*）

最后，指定方法的名称。 如前所述，让 `TotalNumberOfProducts`使用。

![将 DAL 方法命名为 TotalNumberOfProducts](efficiently-paging-through-large-amounts-of-data-cs/_static/image4.png)

**图 4**：命名 DAL 方法 TotalNumberOfProducts

单击 "完成" 后，向导会将 `TotalNumberOfProducts` 方法添加到 DAL。 如果 SQL 查询的结果是 `NULL`的，则 DAL 中返回的标量返回可为 null 的类型。 但 `COUNT` 查询将始终返回非`NULL` 值;不管，DAL 方法返回一个可以为 null 的整数。

除了 DAL 方法之外，我们还需要使用 BLL 中的方法。 打开 `ProductsBLL` 类文件，并添加 `TotalNumberOfProducts` 方法，只需向下调用 DAL s `TotalNumberOfProducts` 方法：

[!code-csharp[Main](efficiently-paging-through-large-amounts-of-data-cs/samples/sample2.cs)]

DAL s `TotalNumberOfProducts` 方法返回一个可以为 null 的整数;但是，我们已经创建了 `ProductsBLL` 类的 `TotalNumberOfProducts` 方法，使其返回标准整数。 因此，我们需要让 `ProductsBLL` 类 `TotalNumberOfProducts` 方法返回由 DAL s `TotalNumberOfProducts` 方法返回的可以为 null 的整数的值部分。 对 `GetValueOrDefault()` 的调用将返回可为 null 的整数值（如果存在）; 否则为。如果 `null`可以为 null 的整数，则返回默认整数值0。

## <a name="step-3-returning-the-precise-subset-of-records"></a>步骤3：返回记录的精确子集

接下来的任务是在 DAL 和 BLL 中创建接受前面讨论的 "起始行索引" 和 "最大行数" 变量的方法，并返回相应的记录。 在执行此操作之前，先查看所需的 SQL 脚本。 我们所面临的挑战是，我们必须能够有效地将索引分配给要分页到的整个结果中的每一行，以便我们可以只返回从起始行索引（和最大记录数到最大记录数）开始的这些记录。

如果数据库表中已有作为行索引的列，这不是一项挑战。 乍一看，我们可能认为 `Products` 表的 `ProductID` 字段足以满足要求，因为第一个产品的 `ProductID` 为1，第二个为2，依此类推。 但是，删除产品会使序列中存在间隔，使以前此方法。

有两种用于有效地将行索引与数据关联以便逐页处理的常规方法，从而允许检索准确的记录子集：

- **使用 SQL Server 2005 s `ROW_NUMBER()` 关键字**new SQL Server 2005，`ROW_NUMBER()` 关键字根据某些排序将排名与每个返回的记录相关联。 此排名可用作每行的行索引。
- **使用表变量和 `SET ROWCOUNT`** SQL Server s [`SET ROWCOUNT` 语句](https://msdn.microsoft.com/library/ms188774.aspx)可用于指定查询在终止之前应处理的总记录数;[表变量](http://www.sqlteam.com/item.asp?ItemID=9454)是可容纳表格数据的本地 t-sql 变量，类似于[临时表](http://www.sqlteam.com/item.asp?ItemID=2029)。 此方法同样适用于 Microsoft SQL Server 2005 和 SQL Server 2000 （而 `ROW_NUMBER()` 方法仅适用于 SQL Server 2005）。  
  
  这里的思路是创建一个表变量，其中包含一个 `IDENTITY` 列和一个列，其中包含要对其数据进行分页的表的主键。 接下来，要将其数据分页到的表的内容转储到表变量中，从而为表中的每条记录关联顺序行索引（通过 `IDENTITY` 列）。 填充表变量后，可以执行表变量上与基础表联接的 `SELECT` 语句来提取特定记录。 `SET ROWCOUNT` 语句用于智能地限制需要转储到表变量中的记录数。  
  
  此方法的效率取决于所请求的页码，因为 `SET ROWCOUNT` 的值被赋予 "起始行索引" 和 "最大行" 的值。 当通过低编号页面（如前几页的数据）进行分页时，此方法非常有效。 但是，在检索到结尾附近的页时，它会表现出默认的分页性能。

本教程使用 `ROW_NUMBER()` 关键字实现自定义分页。 有关使用表变量和 `SET ROWCOUNT` 方法的详细信息，请参阅[通过大型结果集进行分页的更高效方法](http://www.4guysfromrolla.com/webtech/042606-1.shtml)。

使用以下语法将 `ROW_NUMBER()` 关键字与按特定顺序返回的每条记录关联的排名：

[!code-sql[Main](efficiently-paging-through-large-amounts-of-data-cs/samples/sample3.sql)]

`ROW_NUMBER()` 返回一个数值，该数值指定与指定排序相关的每条记录的等级。 例如，若要查看每种产品的排名，按从最昂贵到最高的顺序排序，可以使用以下查询：

[!code-sql[Main](efficiently-paging-through-large-amounts-of-data-cs/samples/sample4.sql)]

图5显示了通过 Visual Studio 中的查询窗口运行时的这一查询结果。 请注意，产品按价格排序，并按每行的价格排名排序。

![为每个返回的记录包含价格排名](efficiently-paging-through-large-amounts-of-data-cs/_static/image5.png)

**图 5**：为每个返回的记录包含价格排名

> [!NOTE]
> `ROW_NUMBER()` 只是 SQL Server 2005 中提供的众多新排名函数之一。 若要深入了解 `ROW_NUMBER()`以及其他排名函数，请参阅[使用 Microsoft SQL Server 2005 返回排名结果](http://www.4guysfromrolla.com/webtech/010406-1.shtml)。

在按 `OVER` 子句中指定 `ORDER BY` 列对结果进行排序（`UnitPrice`，在上面的示例中），SQL Server 必须对结果进行排序。 如果对通过列对结果进行排序所依据的列存在聚集索引，则这是一个快速操作，如果有覆盖索引，则这是一个快速操作，否则可能更昂贵。 若要帮助提高足够大的查询性能，请考虑为排序所依据的列添加非聚集索引。 有关性能注意事项的详细信息，请参阅[SQL Server 2005 中的排名函数和性能](http://www.sql-server-performance.com/ak_ranking_functions.asp)。

`ROW_NUMBER()` 返回的排名信息不能直接在 `WHERE` 子句中使用。 但是，可以使用派生表来返回 `ROW_NUMBER()` 结果，该结果随后可以出现在 `WHERE` 子句中。 例如，下面的查询使用派生表返回 "产品名称" 和 "单价" 列，并使用 `ROW_NUMBER()` 结果，然后使用 `WHERE` 子句只返回价格级别介于11和20之间的产品：

[!code-sql[Main](efficiently-paging-through-large-amounts-of-data-cs/samples/sample5.sql)]

进一步扩展此概念，可以利用这种方法，根据所需的起始行索引和最大行值检索特定的数据页：

[!code-html[Main](efficiently-paging-through-large-amounts-of-data-cs/samples/sample6.html)]

> [!NOTE]
> 稍后将在本教程中看到，ObjectDataSource 提供的 *`StartRowIndex`* 从零开始编制索引，而 SQL Server 2005 返回的 `ROW_NUMBER()` 值从1开始索引。 因此，`WHERE` 子句返回的记录的 `PriceRank` 严格大于 *`StartRowIndex`* ，小于或等于 *`StartRowIndex`*  +  *`MaximumRows`* 。

现在，我们已经讨论了如何使用 `ROW_NUMBER()` 来检索特定的数据页（给定起始行索引和最大行值），接下来我们需要将此逻辑作为 DAL 和 BLL 中的方法实现。

创建此查询时，必须确定结果的排序依据：让我们按字母顺序对产品进行排序。 这意味着，在本教程中，通过自定义分页实现，我们将无法创建自定义分页报表，也不能对其进行排序。 但在下一教程中，我们将了解如何提供此类功能。

在上一部分中，我们将 DAL 方法创建为即席 SQL 语句。 遗憾的是，由 TableAdapter 向导使用的 Visual Studio 中的 T-sql 分析器不像 `ROW_NUMBER()` 函数使用的 `OVER` 语法。 因此，我们必须将此 DAL 方法创建为存储过程。 从 "视图" 菜单中选择 "服务器资源管理器" （或按 Ctrl + Alt + S），然后展开 "`NORTHWND.MDF`" 节点。 若要添加新的存储过程，请右键单击 "存储过程" 节点，然后选择 "添加新存储过程" （见图6）。

![添加用于对产品进行分页的新存储过程](efficiently-paging-through-large-amounts-of-data-cs/_static/image6.png)

**图 6**：添加新的存储过程以通过产品进行分页

此存储过程应接受两个整数输入参数-`@startRowIndex` 和 `@maximumRows` 并使用 `ProductName` 字段排序的 `ROW_NUMBER()` 函数，仅返回大于指定 `@startRowIndex` 的行并小于或等于 `@startRowIndex` + `@maximumRow`。 将以下脚本输入新的存储过程，然后单击 "保存" 图标，将该存储过程添加到数据库中。

[!code-sql[Main](efficiently-paging-through-large-amounts-of-data-cs/samples/sample7.sql)]

创建存储过程后，请花点时间进行测试。右键单击服务器资源管理器中的 `GetProductsPaged` 存储过程名称，然后选择 "执行" 选项。 然后，Visual Studio 会提示输入参数，`@startRowIndex` 和 `@maximumRow` （参见图7）。 尝试不同的值并检查结果。

![输入 @startRowIndex 和 @maximumRows 参数的值](efficiently-paging-through-large-amounts-of-data-cs/_static/image7.png)

<strong>图 7</strong>：输入 @startRowIndex 和 @maximumRows 参数的值

选择这些输入参数值后，"输出" 窗口会显示结果。 图8显示了为 `@startRowIndex` 和 `@maximumRows` 参数传递10时的结果。

[![返回将在第二页数据中显示的记录](efficiently-paging-through-large-amounts-of-data-cs/_static/image9.png)](efficiently-paging-through-large-amounts-of-data-cs/_static/image8.png)

**图 8**：返回将在第二页数据中显示的记录（[单击以查看完全大小的图像](efficiently-paging-through-large-amounts-of-data-cs/_static/image10.png)）

创建此存储过程后，就可以创建 `ProductsTableAdapter` 方法了。 打开 `Northwind.xsd` 类型化数据集，右键单击 `ProductsTableAdapter`，然后选择 "添加查询" 选项。 不要使用即席 SQL 语句创建查询，而是使用现有的存储过程创建它。

![使用现有存储过程创建 DAL 方法](efficiently-paging-through-large-amounts-of-data-cs/_static/image11.png)

**图 9**：使用现有存储过程创建 DAL 方法

接下来，系统会提示选择要调用的存储过程。 从下拉列表中选择 `GetProductsPaged` 存储过程。

![从下拉列表中选择 "GetProductsPaged" 存储过程](efficiently-paging-through-large-amounts-of-data-cs/_static/image12.png)

**图 10**：从下拉列表中选择 "GetProductsPaged" 存储过程

接下来的屏幕会询问存储过程返回的数据类型：表格数据、单个值或无值。 由于 `GetProductsPaged` 存储过程可以返回多个记录，因此表示返回表格数据。

![指示存储过程返回表格数据](efficiently-paging-through-large-amounts-of-data-cs/_static/image13.png)

**图 11**：指示存储过程返回表格数据

最后，指示要创建的方法的名称。 与前面的教程一样，请继续使用 "填充 DataTable" 和 "返回 DataTable" 创建方法。 将第一个方法命名 `FillPaged` 第二个 `GetProductsPaged`。

![将方法命名为 FillPaged 和 GetProductsPaged](efficiently-paging-through-large-amounts-of-data-cs/_static/image14.png)

**图 12**：将方法命名为 FillPaged 和 GetProductsPaged

除了创建用于返回特定产品页的 DAL 方法之外，我们还需要在 BLL 中提供此类功能。 与 DAL 方法一样，BLL s GetProductsPaged 方法必须接受两个整数输入来指定起始行索引和最大行数，并且必须只返回那些在指定范围内的记录。 在 ProductsBLL 类中创建这样一种 BLL 方法，只需向下调用 DAL s GetProductsPaged 方法，如下所示：

[!code-csharp[Main](efficiently-paging-through-large-amounts-of-data-cs/samples/sample8.cs)]

可以为 BLL 方法的输入参数使用任何名称，但正如我们稍后将看到的，在配置 ObjectDataSource 以使用此方法时，选择使用 `startRowIndex` 和 `maximumRows` 可节省额外的工作量。

## <a name="step-4-configuring-the-objectdatasource-to-use-custom-paging"></a>步骤4：将 ObjectDataSource 配置为使用自定义分页

使用 BLL 和 DAL 方法来访问特定记录子集完成后，我们便可以创建一个 GridView 控件，该控件使用自定义分页来浏览其基础记录。 首先打开 `PagingAndSorting` 文件夹中的 "`EfficientPaging.aspx`" 页，向页面添加一个 GridView，然后将其配置为使用新的 ObjectDataSource 控件。 在过去的教程中，我们通常将 ObjectDataSource 配置为使用 `ProductsBLL` 类 `GetProducts` 方法。 但这一次，我们要改为使用 `GetProductsPaged` 方法，因为 `GetProducts` 方法返回数据库中的*所有*产品，而 `GetProductsPaged` 只返回特定的记录子集。

![将 ObjectDataSource 配置为使用 ProductsBLL 类 s GetProductsPaged 方法](efficiently-paging-through-large-amounts-of-data-cs/_static/image15.png)

**图 13**：将 ObjectDataSource 配置为使用 ProductsBLL 类 s GetProductsPaged 方法

由于我们要创建只读 GridView，请花点时间将 "插入"、"更新" 和 "删除" 选项卡中的 "方法" 下拉列表设置为 "（无）"。

接下来，ObjectDataSource 向导会提示我们输入 `GetProductsPaged` 方法的源 `startRowIndex` 和 `maximumRows` 输入参数值。 这些输入参数实际上由 GridView 自动设置，因此只需将源设置为 "无"，然后单击 "完成" 即可。

![将输入参数源保留为 "无"](efficiently-paging-through-large-amounts-of-data-cs/_static/image16.png)

**图 14**：将输入参数源保留为 "无"

完成 ObjectDataSource 向导后，GridView 将包含每个产品数据字段的 BoundField 或 CheckBoxField。 您可以根据自己的情况自由地定制 GridView 的外观。 我选择仅显示 `ProductName`、`CategoryName`、`SupplierName`、`QuantityPerUnit`和 `UnitPrice` BoundFields。 此外，通过选中其智能标记中的 "启用分页" 复选框，将 GridView 配置为支持分页。 进行这些更改后，GridView 和 ObjectDataSource 声明性标记应如下所示：

[!code-aspx[Main](efficiently-paging-through-large-amounts-of-data-cs/samples/sample9.aspx)]

但是，如果您通过浏览器访问该页面，则不会在此处找到 GridView。

![不显示 GridView](efficiently-paging-through-large-amounts-of-data-cs/_static/image17.png)

**图 15**：不显示 GridView

缺少 GridView，因为 ObjectDataSource 目前使用0作为 `GetProductsPaged` `startRowIndex` 和 `maximumRows` 输入参数的值。 因此，生成的 SQL 查询未返回任何记录，因此不会显示 GridView。

若要解决此情况，需要将 ObjectDataSource 配置为使用自定义分页。 可以在以下步骤中完成此操作：

1. **将 objectdatasource `EnablePaging` 属性设置为 `true`** 这向 ObjectDataSource 指示它必须传递到 `SelectMethod` 两个附加参数：一个用于指定起始行索引（[`StartRowIndexParameterName`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.startrowindexparametername.aspx)），另一个用于指定最大行数（[`MaximumRowsParameterName`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.maximumrowsparametername.aspx)）。
2. **设置 ObjectDataSource s `StartRowIndexParameterName` 并相应地 `MaximumRowsParameterName` 属性**，`StartRowIndexParameterName` 和 `MaximumRowsParameterName` 属性指示为自定义分页目的传入 `SelectMethod` 的输入参数的名称。 默认情况下，这些参数名称是 `startIndexRow` 和 `maximumRows`，这就是为什么在 BLL 中创建 `GetProductsPaged` 方法时，我将这些值用于输入参数。 例如，如果选择使用不同的参数名称进行 `GetProductsPaged` 方法，例如 `startIndex` 和 `maxRows`，则需要相应地设置 ObjectDataSource 的 `StartRowIndexParameterName` 和 `MaximumRowsParameterName` 属性（例如，用于 `StartRowIndexParameterName` 的 startIndex 以及 `MaximumRowsParameterName`的 maxRows）。
3. **将 ObjectDataSource s [`SelectCountMethod` 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.selectcountmethod(VS.80).aspx)设置为方法的名称，该方法返回分页的记录总数（`TotalNumberOfProducts`）** ，这意味着 `ProductsBLL` 类的 `TotalNumberOfProducts` 方法返回使用执行 `SELECT COUNT(*) FROM Products` 查询的 DAL 方法进行分页的记录总数。 ObjectDataSource 需要此信息才能正确呈现分页接口。
4. **从 objectdatasource 的声明性标记中删除 `startRowIndex` 和 `maximumRows` `<asp:Parameter>` 元素**，在通过该向导配置 objectdatasource 时，Visual Studio 会自动添加两个 `GetProductsPaged` 方法 s 输入参数的 `<asp:Parameter>` 元素。 通过将 `EnablePaging` 设置为 `true`，将自动传递这些参数;如果它们也出现在声明性语法中，则 ObjectDataSource 会尝试将*四个*参数传递给 `GetProductsPaged` 方法，将两个参数传递给 `TotalNumberOfProducts` 方法。 如果忘记删除这些 `<asp:Parameter>` 元素，则在通过浏览器访问页面时，你将收到类似于以下的错误消息： *ObjectDataSource "ObjectDataSource1" 找不到具有参数的非泛型方法 "TotalNumberOfProducts"： startRowIndex，maximumRows*。

进行这些更改后，ObjectDataSource 的声明性语法应如下所示：

[!code-aspx[Main](efficiently-paging-through-large-amounts-of-data-cs/samples/sample10.aspx)]

请注意，已设置 "`EnablePaging`" 和 "`SelectCountMethod`" 属性，并且已删除 `<asp:Parameter>` 元素。 图16显示了这些更改之后属性窗口的屏幕截图。

![若要使用自定义分页，请配置 ObjectDataSource 控件](efficiently-paging-through-large-amounts-of-data-cs/_static/image18.png)

**图 16**：若要使用自定义分页，请配置 ObjectDataSource 控件

进行这些更改后，请通过浏览器访问此页。 应会看到列出了10个产品，按字母顺序排序。 请花点时间逐行查看数据。 虽然在默认分页与自定义分页之间没有与最终用户之间的视觉差别，但自定义分页可通过大量数据更有效地分页，因为它只检索需要为给定页面显示的记录。

[使用自定义分页 ![按产品名称排序的数据](efficiently-paging-through-large-amounts-of-data-cs/_static/image20.png)](efficiently-paging-through-large-amounts-of-data-cs/_static/image19.png)

**图 17**：按产品名称排序的数据已使用自定义分页进行分页（[单击以查看完全大小的图像](efficiently-paging-through-large-amounts-of-data-cs/_static/image21.png)）

> [!NOTE]
> 使用自定义分页时，ObjectDataSource s `SelectCountMethod` 返回的页计数值存储在 GridView 的视图状态中。 "`PageIndex`"、"`EditIndex`"、"`SelectedIndex`"、"`DataKeys` 集合" 等其他 GridView 变量存储在*控件状态*中，无论 GridView 的 "`EnableViewState`" 属性的值如何，都会保持该状态。 由于使用视图状态将 `PageCount` 值保留在回发之间，因此当使用包含链接的分页界面将您转到最后一页时，必须启用 GridView 的视图状态。 （如果分页接口不包含指向最后一页的直接链接，则可以禁用视图状态。）

单击 "最后一页" 链接将导致回发，并指示 GridView 更新其 `PageIndex` 属性。 如果单击最后一个页面链接，则 GridView 会将其 `PageIndex` 属性分配给小于其 `PageCount` 属性的值。 禁用视图状态时，将会在回发之间丢失 `PageCount` 值，并改为向 `PageIndex` 分配最大整数值。 接下来，GridView 尝试通过将 `PageSize` 和 `PageCount` 属性相乘来确定起始行索引。 这会导致 `OverflowException`，因为产品超出了允许的最大整数大小。

## <a name="implement-custom-paging-and-sorting"></a>实现自定义分页和排序

当前的自定义分页实现要求在创建 `GetProductsPaged` 存储过程时，通过静态方式指定数据分页的顺序。 不过，您可能已注意到，除了启用分页选项外，GridView s 智能标记还包含 "启用排序" 复选框。 遗憾的是，将排序支持添加到具有当前自定义分页实现的 GridView，只会对当前查看的数据页上的记录进行排序。 例如，如果您将 GridView 配置为还支持分页，然后在查看数据的第一页时按产品名称降序排序，则它会反转第1页上产品的顺序。 如图18所示，如按反向字母顺序进行排序时，Carnarvon 稀有作为第一个产品，这会忽略 Carnarvon 稀有之后出现的71其他产品，按字母顺序排列;只有第一页上的记录才会被视为排序。

[仅 ![当前页面上显示的数据进行排序](efficiently-paging-through-large-amounts-of-data-cs/_static/image23.png)](efficiently-paging-through-large-amounts-of-data-cs/_static/image22.png)

**图 18**：仅对当前页上显示的数据进行排序（[单击以查看完全大小的图像](efficiently-paging-through-large-amounts-of-data-cs/_static/image24.png)）

排序仅适用于当前数据页，因为在从 BLL s `GetProductsPaged` 方法检索到数据之后，此方法仅返回特定页的记录。 若要正确实现排序，需要将排序表达式传递到 `GetProductsPaged` 方法，以便在返回数据的特定页面之前，对数据进行适当排名。 我们将在下一教程中了解如何实现此目的。

## <a name="implementing-custom-paging-and-deleting"></a>实现自定义分页和删除

如果你在使用自定义分页技术对其数据进行分页的 GridView 中启用删除功能，你会发现，在删除最后一页中的最后一条记录时，GridView 会消失，而不会正确地递减 GridView 的 `PageIndex`。 若要重现此错误，请为刚创建的教程启用删除。 请访问最后一页（第9页），其中你应该会看到单个产品，因为我们将在81产品和10个产品中一次分页。 删除此产品。

删除最后一种产品后 *，GridView 会*自动进入第8页，此类功能将表现为默认分页。 但是，对于自定义分页，在删除最后一页上的最后一个产品后，GridView 完全从屏幕上消失。 导致这种情况的*确切原因是*在本教程的范围之外，有关此问题的根源，请参阅[从具有自定义分页的 GridView 中删除最后一页上的最后一条记录](http://scottonwriting.net/sowblog/posts/7326.aspx)。 概括而言，由于在单击 "删除" 按钮时，GridView 执行的步骤顺序如下：

1. 删除记录
2. 获取要为指定的 `PageIndex` 和 `PageSize` 显示的相应记录
3. 检查以确保 `PageIndex` 不超过数据源中的数据页数;如果是这样，将自动减小 GridView `PageIndex` 属性
4. 使用在步骤2中获取的记录将适当的数据页绑定到 GridView

此问题源自于第2步：在提取要显示的记录时使用的 `PageIndex` 仍是刚删除其唯一记录的最后一页的 `PageIndex`。 因此，在步骤2中，*不*会返回任何记录，因为该数据的最后一页不再包含任何记录。 然后，在步骤3中，GridView 认识到其 `PageIndex` 属性大于数据源中的总页数（因为我们已删除最后一页中的最后一条记录），因此将其 `PageIndex` 属性减少。 在步骤4中，GridView 尝试将自身绑定到步骤2中检索到的数据;但在步骤2中未返回任何记录，因此导致了一个空的 GridView。 对于默认分页，此问题不会出现，因为在第2步中，将从数据源检索*所有*记录。

若要解决此问题，我们有两个选择。 第一种方法是创建 GridView `RowDeleted` 事件处理程序的事件处理程序，该事件处理程序确定刚刚删除的页面中显示的记录数。 如果只有一条记录，则刚删除的记录必须是最后一个记录，并且我们需要减小 GridView `PageIndex`。 当然，如果删除操作确实成功，我们只想更新 `PageIndex`，这可以通过确保 `e.Exception` 属性 `null`来确定。

此方法有效，因为它将更新步骤1之后但在步骤2之前的 `PageIndex`。 因此，在步骤2中，返回相应的记录集。 若要实现此目的，请使用如下所示的代码：

[!code-csharp[Main](efficiently-paging-through-large-amounts-of-data-cs/samples/sample11.cs)]

另一种解决方法是为 ObjectDataSource `RowDeleted` 事件创建事件处理程序，并将 `AffectedRows` 属性设置为值1。 删除步骤1中的记录后（但在步骤2中重新检索数据之前），如果一个或多个行受操作影响，则 GridView 将更新其 `PageIndex` 属性。 但是，ObjectDataSource 并不设置 `AffectedRows` 属性，因此将省略此步骤。 执行此步骤的一种方法是，如果删除操作成功完成，则手动设置 `AffectedRows` 属性。 这可以通过使用如下代码来实现：

[!code-csharp[Main](efficiently-paging-through-large-amounts-of-data-cs/samples/sample12.cs)]

这两个事件处理程序的代码都可在 `EfficientPaging.aspx` 示例的代码隐藏类中找到。

## <a name="comparing-the-performance-of-default-and-custom-paging"></a>比较默认和自定义分页的性能

自定义分页仅检索所需记录，而默认分页将返回所查看的每个页面的*所有*记录，因此，这显然，自定义分页比默认分页更有效。 但自定义分页的效率要高得多？ 通过从默认分页转为自定义分页，可以查看哪种性能提升？

遗憾的是，这里没有任何一个合适的答案。 性能提升取决于许多因素，最重要的两个因素是要分页到的记录数，以及放置在数据库服务器和 web 服务器与数据库服务器之间的通信通道上的负载。 对于只有少量记录的小型表，性能差异可能会忽略不计。 对于包含数千到数百行的大型表，性能差异很大。

使用[SQL Server 2005 的 ASP.NET 2.0 中](http://aspnet.4guysfromrolla.com/articles/031506-1.aspx)的 "地雷" 自定义分页一文包含一些运行的性能测试，这些测试在分页通过包含50000记录的数据库表时，会表现出这两种分页技术之间的性能差异。 在这些测试中，我使用[ASP.NET 跟踪功能](https://msdn.microsoft.com/library/y13fw6we.aspx)在 SQL Server 级别（使用[SQL 事件探查器](https://msdn.microsoft.com/library/ms173757.aspx)）和 ASP.NET 页上都检查了执行查询的时间。 请记住，这些测试是在具有单个活动用户的开发框上运行的，因此是 unscientific 的，不会模拟典型的网站负载模式。 无论如何，结果都说明了在使用大量数据时，默认和自定义分页的执行时间的相对差异。

|  | **平均持续时间（秒）** | **读取次数** |
| --- | --- | --- |
| **默认分页 SQL 事件探查器** | 1.411 | 383 |
| **自定义分页 SQL 事件探查器** | 0.002 | 29 |
| **默认分页 ASP.NET 跟踪** | 2.379 | *不适用* |
| **自定义分页 ASP.NET 跟踪** | 0.029 | *不适用* |

正如您所看到的，检索特定的数据页需要354的平均读取量，而一小部分时间完成。 在 ASP.NET 页上，自定义页面在使用默认分页时，可以在<sup>接近1/100 的</sup>时间进行呈现。 请参阅[我的文章](http://aspnet.4guysfromrolla.com/articles/031506-1.aspx)，以了解有关这些结果的详细信息以及代码和数据库，你可以下载这些内容以在你自己的环境中重现这些测试。

## <a name="summary"></a>总结

默认分页是一个 cinch，只需检查数据 Web 控件的 "智能标记" 中的 "启用分页" 复选框，就会产生性能的代价。 使用默认分页时，当用户请求任何数据页时，将返回*所有*记录，即使只显示一小部分记录。 为了应对这种性能开销，ObjectDataSource 提供了一个可选的分页选项自定义分页。

尽管自定义分页通过仅检索那些需要显示的记录来改善默认分页性能问题，但它更多是实现自定义分页。 首先，必须正确（并且有效地）写入查询所请求的特定记录子集。 这可以通过多种方式完成：本教程中所述的是使用 SQL Server 2005 s new `ROW_NUMBER()` 函数对结果进行排序，然后只返回排名落在指定范围内的结果。 此外，我们还需要添加一个方法来确定要分页到的记录总数。 创建这些 DAL 和 BLL 方法后，我们还需要配置 ObjectDataSource，使其能够确定要分页到多少个记录，并可以将起始行索引和最大行值正确地传递给 BLL。

虽然实现自定义分页需要执行一些步骤，但并不像默认分页那样简单，但在通过足够大量的数据进行分页时，自定义分页是必需的。 如所述，自定义分页可能会在 ASP.NET 页面呈现时间之外舍弃秒，并可以通过一个或多个数量级使数据库服务器上的负载变亮。

很高兴编程！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)，已在使用 Microsoft Web 技术，自1998开始。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以[mitchell@4GuysFromRolla.com访问。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

> [!div class="step-by-step"]
> [上一页](paging-and-sorting-report-data-cs.md)
> [下一页](sorting-custom-paged-data-cs.md)

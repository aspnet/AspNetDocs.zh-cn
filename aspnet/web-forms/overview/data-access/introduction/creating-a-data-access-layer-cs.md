---
uid: web-forms/overview/data-access/introduction/creating-a-data-access-layer-cs
title: 创建数据访问层 (C#) |Microsoft Docs
author: rick-anderson
description: 在本教程中我们将开始从一开始，并创建数据访问层 (DAL)，使用类型化数据集，访问数据库中的信息。
ms.author: riande
ms.date: 04/05/2010
ms.assetid: cfe2a6a0-1e56-4dc8-9537-c8ec76ba96a4
msc.legacyurl: /web-forms/overview/data-access/introduction/creating-a-data-access-layer-cs
msc.type: authoredcontent
ms.openlocfilehash: 4a6942df142ef40b92a8461afbc5f61fdfbde4ba
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57037844"
---
<a name="creating-a-data-access-layer-c"></a>创建数据访问层 (C#)
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载 PDF](creating-a-data-access-layer-cs/_static/datatutorial01cs1.pdf)

> 在本教程中我们将开始从一开始，并创建数据访问层 (DAL)，使用类型化数据集，访问数据库中的信息。


## <a name="introduction"></a>介绍

作为 web 开发人员，我们的生活都围绕使用的数据。 我们将创建数据库来存储数据，用于检索和修改它，以及 web 页以收集和汇总其代码。 这是将了解如何在 ASP.NET 2.0 中实现这些常见的模式的方法的耗时较长序列中的第一个教程。 我们将开始创建[软件体系结构](http://en.wikipedia.org/wiki/Software_architecture)组合使用类型化数据集，业务逻辑层 (BLL) 数据访问层 (DAL)，它强制自定义业务规则和表示层组成 ASP.NET 的页共享一个通用的页面布局。 一旦该后端基础内容已排列，我们将继续介绍报告，显示如何显示，汇总、 收集和验证的 web 应用程序数据。 这些教程旨在是简洁并提供引导你完成该过程以可视方式很大的屏幕截图的分步说明。 每个教程是在 C# 和 Visual Basic 版本中可用，包括使用的完整代码下载。 （本教程中第一个是非常长，但其余部分显示更多的理解的多个块区中。）

这些教程中我们将使用 Microsoft SQL Server 2005 Express Edition 版本的 Northwind 数据库中放置**应用程序\_数据**目录。 数据库文件中，除了**应用程序\_数据**文件夹还包含用于创建数据库的 SQL 脚本，以防你想要使用不同的数据库版本。 这些脚本可能还会[直接从 Microsoft 下载](https://www.microsoft.com/downloads/details.aspx?FamilyID=06616212-0356-46a0-8da2-eebc53a68034&amp;DisplayLang=en)，如果您希望使用。 如果使用不同的 SQL Server 版本的 Northwind 数据库，您需要更新**NORTHWNDConnectionString**在应用程序的设置**Web.config**文件。 Web 应用程序已为文件系统基于 Web 站点项目使用 Visual Studio 2005 Professional Edition 构建。 但是，所有这些教程将会使用免费版本的 Visual Studio 2005 中，也同样[Visual Web Developer](https://msdn.microsoft.com/vstudio/express/vwd/)。  
  
在本教程中我们将开始从一开始，并创建数据访问层 (DAL) 后, 跟在第二个教程中，创建业务逻辑层 (BLL) 和页面布局和第三个中的导航。 在前三个中的布局的基础之上的第三个将生成后的教程。 我们有很多介绍此第一个教程中，因此启动 Visual Studio 并让我们开始吧 ！

## <a name="step-1-creating-a-web-project-and-connecting-to-the-database"></a>步骤 1：创建 Web 项目并连接到数据库

我们可以创建我们的数据访问层 (DAL) 之前，我们首先需要创建一个网站并设置我们的数据库。 首先，创建新文件系统基于 ASP.NET web 站点。 若要完成此操作，请转到文件菜单并选择新网站，显示新建网站对话框。 选择 ASP.NET 网站模板、 将位置下拉列表设置为文件系统、 选择一个文件夹以将该 web 站点，并将语言设置为 C#。


[![创建新的文件基于系统的 Web 站点](creating-a-data-access-layer-cs/_static/image2.png)](creating-a-data-access-layer-cs/_static/image1.png)

**图 1**:创建 New File System-Based 网站 ([单击此项可查看原尺寸图像](creating-a-data-access-layer-cs/_static/image3.png))


这将创建与新的 web 站点**Default.aspx** ASP.NET 页面和一个**应用\_数据**文件夹。

使用创建的网站下, 一步是在 Visual Studio 服务器资源管理器中添加对数据库的引用。 通过将数据库添加到服务器资源管理器可以添加表、 存储的过程、 视图和因此，在所有这些操作在 Visual Studio 中。 此外可以查看表数据或查询生成器通过手动或以图形方式创建自己的查询。 此外，我们为 DAL 生成类型化数据集时，我们需要对数据库可从其构造类型化数据集的 Visual studio。 虽然我们可以提供此连接信息在该点的时间，Visual Studio 将自动填充已在服务器资源管理器中注册的数据库的下拉列表。

将 Northwind 数据库添加到服务器资源管理器的步骤取决于是否想要使用 SQL Server 2005 Express Edition 数据库中的**应用程序\_数据**文件夹或者如果您使用 Microsoft SQL Server 2000 或 2005年你想要改为使用的数据库服务器设置。

## <a name="using-a-database-in-theappdatafolder"></a>在应用程序中使用数据库\_DataFolder

如果您不具有 SQL Server 2000 或 2005年数据库服务器连接到，或只是想要避免必须将数据库添加到数据库服务器，则可以使用位于下载网站的 Northwind 数据库的 SQL Server 2005 Express Edition 版本e's**应用程序\_数据**文件夹 (**northwnd 不。MDF**)。

将数据库置于**应用程序\_数据**文件夹自动添加到服务器资源管理器。 假设你有 SQL Server 2005 Express Edition 在计算机上安装您应该看到一个名为 northwnd 不节点。MDF 在服务器资源管理器，你可以展开和浏览其表、 视图、 存储的过程等 （请参见图 2）。

**应用程序\_数据**文件夹还可以包含 Microsoft Access **.mdb**文件，如 SQL Server 其对应项，会自动添加到服务器资源管理器。 如果不想要使用的任何 SQL Server 选项，则可以始终[下载 Northwind 数据库文件的 Microsoft Access 版本](https://www.microsoft.com/downloads/details.aspx?FamilyID=C6661372-8DBE-422B-8676-C632D66C529C&amp;displaylang=EN)放到**应用\_数据**目录。 请注意，但是，作为不访问数据库的 SQL Server 作为功能丰富并不设计为在 web 站点方案中使用。 此外，几个 35 + 教程将使用不受访问某些数据库级功能。

## <a name="connecting-to-the-database-in-a-microsoft-sql-server-2000-or-2005-database-server"></a>连接到 Microsoft SQL Server 2000 或 2005年数据库服务器中数据库

或者，你可能会连接到数据库服务器上安装的 Northwind 数据库。 如果数据库服务器还没有安装的 Northwind 数据库，您首先必须将其添加到数据库服务器通过运行安装脚本包含本教程中的下载中或通过[下载 Northwind SQL Server 2000 版本安装脚本和](https://www.microsoft.com/downloads/details.aspx?FamilyID=06616212-0356-46a0-8da2-eebc53a68034&amp;DisplayLang=en)直接从 Microsoft 网站上找到。

安装了数据库后，请转到 Visual Studio 的服务器资源管理器，右键单击数据连接节点，然后选择添加连接。 如果看不到服务器资源管理器转到视图 / 服务器资源管理器或命中的 Ctrl + Alt + S。 这将显示添加连接对话框，您可以在其中指定要连接到的服务器，身份验证信息和数据库名称。 一旦你已成功配置的数据库连接信息并单击确定按钮，数据库将添加为数据连接节点下的一个节点。 您可以展开数据库节点以探索其表、 视图、 存储的过程等。


![添加到数据库服务器的 Northwind 数据库的连接](creating-a-data-access-layer-cs/_static/image4.png)

**图 2**:添加到数据库服务器的 Northwind 数据库的连接


## <a name="step-2-creating-the-data-access-layer"></a>步骤 2：创建数据访问层

使用时数据的一种选择是特定于数据的逻辑将直接嵌入到表示层 （在 web 应用程序，ASP.NET 页面一起构成表示层）。 这可能需要在 ASP.NET 页面的代码部分中编写 ADO.NET 代码或使用的标记部分从 SqlDataSource 控件的窗体。 在任一情况下，这种方法紧密耦合数据访问逻辑与表示层。 但是，建议的方法是分开的表示层的数据访问逻辑。 此单独的层称为数据访问层，简称为 DAL，通常实现为一个单独的类库项目。 此分层式体系结构的优点也有文档记录 （在本教程，了解这些优点的信息的末尾看到"进一步读数"部分） 是本系列中，我们将采取的方法。

所有代码都是特定于基础数据源创建连接到数据库，例如颁发**选择**，**插入**，**更新**，和**删除**命令中，依次类推应位于 DAL。 表示层不应包含对这些数据访问代码的任何引用，但应改为对进行调用的所有数据请求 DAL。 数据访问层通常包含用于访问基础数据库数据的方法。 Northwind 数据库中，例如，具有**产品**并**类别**记录用于销售和到其所属的类别的产品的表。 DAL 中我们将具有类似的方法：

- **GetCategories()，** 这将返回有关所有类别信息
- **GetProducts()**，这将返回有关的所有产品的信息
- **GetProductsByCategoryID (*categoryID*)**，这将返回属于指定类别的所有产品
- **GetProductByProductID (*productID*)**，这将返回有关特定产品的信息

这些方法调用时，将连接到数据库、 发出相应的查询，并返回结果。 我们如何返回这些结果很重要。 这些方法可能只需返回数据集或 DataReader 填充的数据库查询，但理想情况下这些结果应返回使用*强类型对象*。 强类型化的对象是一个在编译时，严格定义其架构而相反，松散类型化的对象，是一个运行时之前不知道其架构。

例如，DataReader 和 （默认） 数据集是松散类型化对象，因为其架构定义由用来填充这些数据库查询返回的列。 若要访问的特定列对松散类型化 DataTable 中我们需要使用类似的语法：<strong><em>DataTable</em>.Rows[<em>index</em>]["<em>columnName</em>"]</strong>. DataTable 的松散类型化在此示例中表现出这一事实，我们需要访问使用字符串或序号索引的列名称。 强类型化 DataTable，但是，将具有的每个实现为属性，其列导致如下所示的代码：<strong><em>DataTable</em>.Rows[<em>index</em>].*columnName</strong>*.

若要返回强类型对象，开发人员可以创建他们自己的自定义业务对象或使用类型化数据集。 由开发人员实现业务对象，因为其属性通常反映基础数据库表的业务对象的列的类表示。 类型化数据集是由基于数据库架构和其成员都是强类型根据此架构的 Visual Studio 为您生成的类。 类型化数据集本身由扩展 ADO.NET DataSet、 DataTable 和 DataRow 类的类组成。 除了强类型化 Datatable，类型化数据集现在还包含 Tableadapter，是与用于填充数据集的数据表和传播回数据库内 DataTables 的修改方法的类。

> [!NOTE]
> 有关使用与自定义业务对象的类型化数据集的优缺点的详细信息，请参阅[设计数据层组件和层间传递数据](https://msdn.microsoft.com/library/ms978496.aspx)。


我们将使用这些教程的体系结构的强类型化数据集。 图 3 说明了使用类型化数据集的应用程序的不同层之间的工作流。


[![所有数据访问代码都交付给 DAL](creating-a-data-access-layer-cs/_static/image6.png)](creating-a-data-access-layer-cs/_static/image5.png)

**图 3**:所有数据访问代码都交付给 DAL ([单击此项可查看原尺寸图像](creating-a-data-access-layer-cs/_static/image7.png))


## <a name="creating-a-typed-dataset-and-table-adapter"></a>创建类型化数据集和表适配器

若要开始创建 DAL，我们先将类型化数据集添加到我们的项目。 若要完成此操作，右键单击解决方案资源管理器中的项目节点并选择新项添加。 从模板列表中选择数据集选项并将其命名**Northwind.xsd**。


[![选择将新的数据集添加到你的项目](creating-a-data-access-layer-cs/_static/image9.png)](creating-a-data-access-layer-cs/_static/image8.png)

**图 4**:选择将新的数据集添加到您的项目 ([单击此项可查看原尺寸图像](creating-a-data-access-layer-cs/_static/image10.png))


单击添加，当系统提示你添加到数据集后**应用程序\_代码**文件夹中，选择是。 将显示为类型化数据集设计器，并将启动 TableAdapter 配置向导，您可以将第一个 TableAdapter 添加到类型化数据集。

类型化数据集作为强类型集合的数据;它被构成的强类型化 DataTable 实例，其中每个由反过来的强类型化 DataRow 实例组成。 我们将为每个基础数据库表，我们需要使用本教程系列中创建强类型化 DataTable。 让我们开始创建的数据表**产品**表。

请记住，强类型化 Datatable 不包括有关如何访问其基础数据库表中的数据的任何信息。 若要检索的数据来填充 DataTable，我们使用 TableAdapter 类，用作我们的数据访问层。 对于我们**产品**数据表，TableAdapter 将包含方法**GetProducts()**， **GetProductByCategoryID (*categoryID*)**，依次类推，我们将调用从表示层。 DataTable 的作用是充当用于各层之间传递数据的强类型化对象。

TableAdapter 配置向导会首先提示您选择要使用的数据库。 下拉列表显示了在服务器资源管理器中的这些数据库。 如果您没有到服务器资源管理器添加 Northwind 数据库，可以在此时间为此，单击新建连接按钮。


[![从下拉列表中选择 Northwind 数据库](creating-a-data-access-layer-cs/_static/image12.png)](creating-a-data-access-layer-cs/_static/image11.png)

**图 5**:从下拉列表中选择 Northwind 数据库 ([单击此项可查看原尺寸图像](creating-a-data-access-layer-cs/_static/image13.png))


选择数据库并单击下一步之后, 您将要求你想要保存连接字符串中的**Web.config**文件。 通过将保存的连接字符串将避免必须硬编码在 TableAdapter 类中，这样可以简化操作，如果连接字符串信息在将来发生更改。 如果选择将连接字符串保存在配置文件中将被放置在 **&lt;connectionStrings&gt;** 部分中，可以是[（可选） 加密](http://aspnet.4guysfromrolla.com/articles/021506-1.aspx)以改进安全或更高版本通过新的 ASP.NET 2.0 属性页内 IIS GUI 管理工具的说明进行操作，这是更适合管理员已修改。


[![将连接字符串保存到 Web.config](creating-a-data-access-layer-cs/_static/image15.png)](creating-a-data-access-layer-cs/_static/image14.png)

**图 6**:保存到的连接字符串**Web.config** ([单击以查看实际尺寸的图像](creating-a-data-access-layer-cs/_static/image16.png))


接下来，我们需要定义为第一个强类型化 DataTable 的架构，并提供我们 TableAdapter 填充强类型化数据集时要使用的第一个方法。 这两个步骤都是同时完成通过创建查询，我们希望在我们 DataTable 中反映从表返回的列。 在向导末尾我们将对此查询提供的方法名称。 一旦已完成此操作，可以从我们的表示层调用此方法。 该方法将执行定义的查询，并填充强类型化 DataTable。

若要开始定义我们首先必须指示我们想要发出查询的 TableAdapter 的 SQL 查询。 我们可以使用临时 SQL 语句，创建新的存储的过程，或使用现有的存储的过程。 对于这些教程中，我们将使用的临时 SQL 语句。 请参阅[Brian Noyes](http://briannoyes.net/)的文章[与 Visual Studio 2005 数据集设计器将数据访问层构建](http://www.theserverside.net/articles/showarticle.tss?id=DataSetDesigner)有关使用存储的过程的示例。


[![查询使用的临时 SQL 语句的数据](creating-a-data-access-layer-cs/_static/image18.png)](creating-a-data-access-layer-cs/_static/image17.png)

**图 7**:查询使用的临时 SQL 语句的数据 ([单击此项可查看原尺寸图像](creating-a-data-access-layer-cs/_static/image19.png))


现在我们可以在 SQL 查询中手动键入。 当在 TableAdapter 中创建第一种方法通常想要让查询返回这些列需要在相应的 DataTable 中表达的。 我们可以通过创建返回所有列和中的所有行的查询来实现此目的**产品**表：


[![在文本框中输入 SQL 查询](creating-a-data-access-layer-cs/_static/image21.png)](creating-a-data-access-layer-cs/_static/image20.png)

**图 8**:输入 SQL 查询到文本框 ([单击此项可查看原尺寸图像](creating-a-data-access-layer-cs/_static/image22.png))


或者，使用查询生成器，并以图形方式构造查询，如图 9 中所示。


[![通过查询编辑器中以图形方式创建查询](creating-a-data-access-layer-cs/_static/image24.png)](creating-a-data-access-layer-cs/_static/image23.png)

**图 9**:创建查询以图形方式，通过查询编辑器中 ([单击此项可查看原尺寸图像](creating-a-data-access-layer-cs/_static/image25.png))


在创建查询，然后再移到下一个屏幕上，单击高级选项按钮。 在网站项目中，"生成 Insert、 Update 和 Delete 语句"是唯一一种高级选项选择默认设置。如果从类库或 Windows 项目运行此向导还将选择"使用开放式并发"选项。 现在将"使用开放式并发"选项保留未选中状态。 在将来的教程中，我们将介绍乐观并发。


[![选择仅生成 Insert、 Update 和 Delete 语句选项](creating-a-data-access-layer-cs/_static/image27.png)](creating-a-data-access-layer-cs/_static/image26.png)

**图 10**:选择仅生成 Insert、 Update 和 Delete 语句选项 ([单击此项可查看原尺寸图像](creating-a-data-access-layer-cs/_static/image28.png))


在验证的高级的选项后，单击下一步转到最后一个屏幕。 此处我们会要求选择要添加到 TableAdapter 的方法。 有两种模式来填充数据：

- **填充 DataTable**这种方法创建一个方法接受一个参数作为 DataTable 并填充它基于查询的结果。 ADO.NET DataAdapter 类，例如，实现此模式与其 **Fill()** 方法。
- **返回 DataTable**使用此方法时此方法将创建和填充 DataTable 的并将其返回作为方法返回值。

您可以实现一个或这两种模式的 TableAdapter。 您还可以重命名此处提供的方法。 尽管我们只会使用这些教程在后一种模式，我们将保留选中状态，这两个复选框。 此外，让我们重命名而不是泛型**GetData**方法**GetProducts**。

最后一个复选框，"GenerateDBDirectMethods，"如果选中，创建**insert （)**， **update （)**，并**delete （)** TableAdapter 的方法。 如果选中此选项，所有更新将都需要通过 TableAdapter 的唯一 **update （)** 方法，后者采用在类型化数据集、 数据表、 单个数据行或返回数据行的数组。 (如果已在图 9 中的高级属性中此复选框未选中"生成 Insert、 Update 和 Delete 语句"选项设置不起作用。)我们将保留选中此复选框。


[![GetData 方法名称更改为 GetProducts](creating-a-data-access-layer-cs/_static/image30.png)](creating-a-data-access-layer-cs/_static/image29.png)

**图 11**:将方法名称由**GetData**到**GetProducts** ([单击以查看实际尺寸的图像](creating-a-data-access-layer-cs/_static/image31.png))


单击完成完成向导。 在向导关闭后我们将返回到数据集设计器，其中显示我们刚刚创建的 DataTable。 可以看到列表中的列**产品**DataTable (**ProductID**， **ProductName**，等等)，以及的方法**ProductsTableAdapter** (**Fill()** 并**GetProducts()**)。


[![产品数据表和 ProductsTableAdapter 已添加到类型化数据集](creating-a-data-access-layer-cs/_static/image33.png)](creating-a-data-access-layer-cs/_static/image32.png)

**图 12**:**产品**DataTable 并**ProductsTableAdapter**已添加到类型化数据集 ([单击以查看实际尺寸的图像](creating-a-data-access-layer-cs/_static/image34.png))


我们现在有单个数据表的数据集类型 (**Northwind.Products**) 和一个强类型 DataAdapter 类 (**NorthwindTableAdapters.ProductsTableAdapter**) 与 **GetProducts()** 方法。 这些对象可以用于从类似的代码访问的所有产品的列表：

[!code-html[Main](creating-a-data-access-layer-cs/samples/sample1.html)]

此代码不需要我们编写数据访问特定于代码的一位。 我们不需要实例化任何 ADO.NET 类，我们不需要任何连接字符串，SQL 查询，请参阅或存储过程。 相反，TableAdapter 为我们提供低级别的数据访问代码。

此示例中使用每个对象也是强类型，以便 Visual Studio 提供 IntelliSense 和编译时类型检查。 并且返回的 TableAdapter 的所有 DataTables 的可以绑定到 ASP.NET 数据 Web 控件，如 GridView、 DetailsView、 DropDownList、 CheckBoxList 和其他几种。 下面的示例演示绑定返回的 DataTable **GetProducts()** 方法只需扫描的三个行中的代码中 gridview**页面\_负载**事件处理程序。

AllProducts.aspx

[!code-aspx[Main](creating-a-data-access-layer-cs/samples/sample2.aspx)]

AllProducts.aspx.cs

[!code-csharp[Main](creating-a-data-access-layer-cs/samples/sample3.cs)]


[![在 GridView 中显示的产品列表](creating-a-data-access-layer-cs/_static/image36.png)](creating-a-data-access-layer-cs/_static/image35.png)

**图 13**:在 GridView 中显示的产品列表 ([单击此项可查看原尺寸图像](creating-a-data-access-layer-cs/_static/image37.png))


尽管此示例要求这样做，我们编写三行代码在我们的 ASP.NET 页面**页上\_负载**事件处理程序中，在将来我们将介绍如何使用 ObjectDataSource 来以声明方式检索数据的教程DAL。 使用 ObjectDataSource 我们将不需要编写任何代码，并将分页和排序查询支持，并支持 ！

## <a name="step-3-adding-parameterized-methods-to-the-data-access-layer"></a>步骤 3：添加参数化的方法添加到数据访问层

此时我们**ProductsTableAdapter**类具有一种方法，但**GetProducts()**，它返回数据库中的所有产品。 在能够使用所有的产品是确实有用，在我们将的想要检索有关特定产品或属于特定类别的所有产品的信息。 若要将此类功能添加到我们的数据访问层，我们可以向 TableAdapter 添加参数化的方法。

让我们添加**GetProductsByCategoryID (*categoryID*)** 方法。 若要将新方法添加到 DAL，返回到数据集设计器中，右键单击**ProductsTableAdapter**部分，然后选择添加查询。


![右键单击 TableAdapter，然后选择添加查询](creating-a-data-access-layer-cs/_static/image38.png)

**图 14**:右键单击 TableAdapter，然后选择添加查询


我们首先提示您有关是否要使用的临时 SQL 语句或新的或现有的存储的过程访问数据库。 让我们选择使用同样的临时 SQL 语句。 接下来，我们会要求我们要使用哪些类型的 SQL 查询。 由于我们要返回属于指定类别的所有产品，因此我们想要编写**选择**语句返回的行。


[![选择创建的 SELECT 语句返回的行](creating-a-data-access-layer-cs/_static/image40.png)](creating-a-data-access-layer-cs/_static/image39.png)

**图 15**:选择创建**选择**语句的返回行 ([单击以查看实际尺寸的图像](creating-a-data-access-layer-cs/_static/image41.png))


下一步是定义用于访问数据的 SQL 查询。 由于我们要返回属于特定类别的那些产品，因此我将使用相同<strong>选择</strong>从语句<strong>GetProducts()</strong>，但将添加以下<strong>其中</strong>子句：<strong>其中 CategoryID = @CategoryID</strong> 。 <strong>@CategoryID</strong>参数到 TableAdapter 向导指示我们要创建的方法，将需要输入的参数的相应类型 （也就是说，可以为 null 的整数）。


[![输入查询以仅返回在指定的类别中的产品](creating-a-data-access-layer-cs/_static/image43.png)](creating-a-data-access-layer-cs/_static/image42.png)

**图 16**:输入查询以仅返回产品中指定的类别 ([单击此项可查看原尺寸图像](creating-a-data-access-layer-cs/_static/image44.png))


在最后一步我们可以选择一种数据访问模式来使用，以及自定义生成的方法的名称。 用于填充图案，让我们将名称更改为<strong>FillByCategoryID</strong> ，并返回数据表返回模式 (<strong>获取*X</strong>* 方法)，让我们使用<strong>GetProductsByCategoryID</strong>。


[![选择的 TableAdapter 方法的名称](creating-a-data-access-layer-cs/_static/image46.png)](creating-a-data-access-layer-cs/_static/image45.png)

**图 17**:选择的 TableAdapter 方法的名称 ([单击此项可查看原尺寸图像](creating-a-data-access-layer-cs/_static/image47.png))


完成向导后，数据集设计器包括新的 TableAdapter 方法。


![产品可以现在按类别查询](creating-a-data-access-layer-cs/_static/image48.png)

**图 18**:产品可以现在按类别查询


花些时间添加 **GetProductByProductID(*productID*)** 方法使用相同的技术。

这些参数化的查询可以直接从数据集设计器进行测试。 右键单击 TableAdapter 中的方法，并选择预览数据。 接下来，输入要使用的参数，并单击预览的值。


[![显示这些产品属于饮料类别](creating-a-data-access-layer-cs/_static/image50.png)](creating-a-data-access-layer-cs/_static/image49.png)

**图 19**:显示这些产品属于饮料类别 ([单击此项可查看原尺寸图像](creating-a-data-access-layer-cs/_static/image51.png))


与**GetProductsByCategoryID (*categoryID*)** DAL 中的方法，我们现在可以创建仅显示这些产品在指定的类别中的 ASP.NET 页。 下面的示例演示的所有产品饮料类别中具有**CategoryID**为 1。

Beverages.asp

[!code-aspx[Main](creating-a-data-access-layer-cs/samples/sample4.aspx)]

Beverages.aspx.cs

[!code-csharp[Main](creating-a-data-access-layer-cs/samples/sample5.cs)]


[![显示饮料类别中的这些产品](creating-a-data-access-layer-cs/_static/image53.png)](creating-a-data-access-layer-cs/_static/image52.png)

**图 20**:显示饮料类别中的这些产品 ([单击此项可查看原尺寸图像](creating-a-data-access-layer-cs/_static/image54.png))


## <a name="step-4-inserting-updating-and-deleting-data"></a>步骤 4：插入、 更新和删除数据

有两种模式通常用于插入、 更新和删除数据。 第一种模式，我将其称为数据库直接模式，包括创建方法，调用时，问题**插入**，**更新**，或**删除**命令对一条数据库记录的数据库。 若要插入、 更新或删除的值中，此类方法中的一系列相对应的标量值 （整数、 字符串、 布尔值、 Datetime，等） 通常传递。 例如，对于这种模式**产品**delete 方法需要整数参数中的表，该值指示**ProductID**要删除的记录，而 insert 方法将需要字符串为**ProductName**、 十进制用于**UnitPrice**，为一个整数**UnitsOnStock**，依次类推。


[![每个插入、 更新和删除请求发送到数据库立即](creating-a-data-access-layer-cs/_static/image56.png)](creating-a-data-access-layer-cs/_static/image55.png)

**图 21**:每个插入、 更新和删除请求发送到数据库立即 ([单击此项可查看原尺寸图像](creating-a-data-access-layer-cs/_static/image57.png))


其他模式，我将引用作为批更新模式，这是更新整个数据集、 DataTable 或 Datarow 的一种方法调用中的集合。 此模式与开发人员删除、 插入、 和修改数据表中的数据行，然后将这些数据行或 DataTable 传递给 update 方法。 此方法然后枚举传递中对 Datarow，确定是否它们已被修改、 添加或删除 (通过 DataRow [RowState 属性](https://msdn.microsoft.com/library/system.data.datarow.rowstate.aspx)值)，并发出相应的数据库请求，每个记录。


[![调用 Update 方法时，所有更改将与数据库都同步](creating-a-data-access-layer-cs/_static/image59.png)](creating-a-data-access-layer-cs/_static/image58.png)

**图 22**:调用 Update 方法时，所有更改将与数据库都同步 ([单击此项可查看原尺寸图像](creating-a-data-access-layer-cs/_static/image60.png))


TableAdapter 默认情况下，使用批更新模式，但也支持 DB 直接模式。 由于我们从高级属性选择"生成 Insert、 Update 和 Delete 语句"选项，创建我们 TableAdapter 时 **ProductsTableAdapter** 包含 **update （)** 方法，它实现批处理更新模式。 具体而言，TableAdapter 包含 **update （)** 类型化数据集、 强类型的数据表或一个或多个数据行可传递的方法。 如果保留"GenerateDBDirectMethods"复选框选中时首次创建 TableAdapter 的 DB 直接模式将还可通过实现 **Insert()** ， **update（)** ，和 **delete（)** 方法。

这两种数据修改模式使用 TableAdapter **InsertCommand**， **UpdateCommand**，和**DeleteCommand**属性来颁发其**插入**，**更新**，和**删除**命令到数据库。 可以检查和修改**InsertCommand**， **UpdateCommand**，并**DeleteCommand**单击数据集设计器中对 tableadapter，然后将属性到属性窗口中。 (请确保已选择 TableAdapter，并且**ProductsTableAdapter**对象是在属性窗口中的下拉列表中选择。)


[![TableAdapter 具有 InsertCommand、 UpdateCommand 和 DeleteCommand 属性](creating-a-data-access-layer-cs/_static/image62.png)](creating-a-data-access-layer-cs/_static/image61.png)

**图 23**:Tableadapter **InsertCommand**， **UpdateCommand**，并**DeleteCommand**属性 ([单击以查看实际尺寸的图像](creating-a-data-access-layer-cs/_static/image63.png))


若要检查或修改任何这些数据库命令属性，单击**CommandText**子属性，这将显示查询生成器。


[![在查询生成器中配置 INSERT、 UPDATE 和 DELETE 语句](creating-a-data-access-layer-cs/_static/image65.png)](creating-a-data-access-layer-cs/_static/image64.png)

**图 24**:配置**插入**，**更新**，并**删除**查询生成器中的语句 ([单击以查看实际尺寸的图像](creating-a-data-access-layer-cs/_static/image66.png))


下面的代码示例演示如何使用批处理更新模式翻倍的所有产品的数量以及库存数量或更少具有 25 个单位的价格：

[!code-csharp[Main](creating-a-data-access-layer-cs/samples/sample6.cs)]

以下代码演示了如何使用 DB 直接模式以编程方式删除某一特定产品，然后更新其中一个，以及如何将一个新：

[!code-csharp[Main](creating-a-data-access-layer-cs/samples/sample7.cs)]

## <a name="creating-custom-insert-update-and-delete-methods"></a>创建自定义插入、 更新和删除方法

**Insert （)**， **update （)**，并**delete （)** 方法创建的 DB 直接方法可以是有点麻烦，尤其是对拥有许多列的表。 查看上一代码示例中，没有 IntelliSense 的帮助并不特别清楚什么**产品**表的列映射到每个输入参数**update （)** 和**insert （)** 方法。 可能有我们仅希望更新单个列或两个，或者想要自定义**insert （)** 方法，将这样一来，该方法返回的值为新插入记录**标识**（自动递增）字段。

若要创建此类自定义的方法，返回到数据集设计器。 右键单击 TableAdapter，然后选择添加的查询，返回到 TableAdapter 向导。 在第二个屏幕上我们可以指示要创建查询的类型。 让我们创建的方法添加一个新产品，然后返回新添加的记录的值**ProductID**。 因此，选择创建**插入**查询。


[![创建一个方法用于将新行添加到产品表](creating-a-data-access-layer-cs/_static/image68.png)](creating-a-data-access-layer-cs/_static/image67.png)

**图 25**:创建一个方法来向其中添加新行**产品**表 ([单击以查看实际尺寸的图像](creating-a-data-access-layer-cs/_static/image69.png))


在下一个屏幕**InsertCommand**的**CommandText**出现。 通过此查询添加来扩充**选择作用域\_IDENTITY()** 在查询结束时，这将返回插入到的最后一个标识值**标识**同一作用域中的列。 (请参阅[技术文档](https://msdn.microsoft.com/library/ms190315.aspx)有关详细信息**作用域\_IDENTITY()** 以及为什么你可能希望对[使用作用域\_IDENTITY() 替代 @@IDENTITY](http://weblogs.sqlteam.com/travisl/archive/2003/10/29/405.aspx).)请确保您最终**插入**之前添加语句以分号**选择**语句。


[![增加要返回 scope_identity （） 值的查询](creating-a-data-access-layer-cs/_static/image71.png)](creating-a-data-access-layer-cs/_static/image70.png)

**图 26**:增强对返回的查询**作用域\_IDENTITY()** 值 ([单击以查看实际尺寸的图像](creating-a-data-access-layer-cs/_static/image72.png))


最后，将该新方法**InsertProduct**。


[![将新的方法名称设置为 InsertProduct](creating-a-data-access-layer-cs/_static/image74.png)](creating-a-data-access-layer-cs/_static/image73.png)

**图 27**:将新的方法名称设置为**InsertProduct** ([单击以查看实际尺寸的图像](creating-a-data-access-layer-cs/_static/image75.png))


当您返回到数据集设计器可以发现**ProductsTableAdapter**包含一个新的方法**InsertProduct**。 如果这种新方法没有在每个列的参数**产品**表中，您很可能忘记了终止**插入**用分号的语句。 配置**InsertProduct**方法并确保已将以分号分隔**插入**并**选择**语句。

默认情况下，insert 方法问题非查询方法，这意味着它们返回受影响的行数。 但是，我们想**InsertProduct**方法以返回由查询不受影响的行数返回的值。 若要实现此目的，调整**InsertProduct**方法的**ExecuteMode**属性设置为**标量**。


[![ExecuteMode 属性更改为标量](creating-a-data-access-layer-cs/_static/image77.png)](creating-a-data-access-layer-cs/_static/image76.png)

**图 28**:更改**ExecuteMode**属性设置为**标量**([单击以查看实际尺寸的图像](creating-a-data-access-layer-cs/_static/image78.png))


下面的代码演示此新**InsertProduct**中操作的方法：

[!code-csharp[Main](creating-a-data-access-layer-cs/samples/sample8.cs)]

## <a name="step-5-completing-the-data-access-layer"></a>步骤 5：完成数据访问层

请注意， **ProductsTableAdapters**类返回**CategoryID**并**SupplierID**中的值**产品**表，但不包括**CategoryName**中的列**类别**表或**CompanyName**从列**供应商**表，尽管这些可能是我们想要显示的产品信息时显示的列。 我们可以随着扩展 TableAdapter 的初始方法**GetProducts()**，以包括这两**CategoryName**并**CompanyName**列的值，这将更新若要包括这些新的列的强类型化的 DataTable。

这导致出现问题，但是，为 TableAdapter 的方法用于插入，更新和删除数据基于此初始方法。 幸运的是，自动生成的方法插入、 更新和删除不受影响的中的子查询**选择**子句。 通过处理添加到我们查询**类别**并**供应商**作为子查询，而非**加入**s，我们将避免无需重新编写这些方法用于修改数据。 右键单击**GetProducts()** 中的方法**ProductsTableAdapter**并选择配置。 然后，调整**选择**子句，因此它看起来类似于：

[!code-sql[Main](creating-a-data-access-layer-cs/samples/sample9.sql)]


[![SELECT 语句更新 GetProducts() 方法](creating-a-data-access-layer-cs/_static/image80.png)](creating-a-data-access-layer-cs/_static/image79.png)

**图 29**:更新**选择**语句**GetProducts()** 方法 ([单击以查看实际尺寸的图像](creating-a-data-access-layer-cs/_static/image81.png))


更新后**GetProducts()** 要使用此数据表将包含两个新列的新查询的方法：**CategoryName**并**供应商名称**。


![产品数据表具有两个新列](creating-a-data-access-layer-cs/_static/image82.png)

**图 30**:**产品**DataTable 具有两个新列


花一些时间来更新 **选择** 中的子句 **GetProductsByCategoryID (*categoryID*)** 以及方法。

如果更新**GetProducts()** **选择**使用**加入**语法数据集设计器将无法自动生成用于插入、 更新和删除方法数据库使用 DB 直接模式数据。 相反，您将必须手动创建它们更像我们一样**InsertProduct**在本教程前面的方法。 此外，手动将需要提供**InsertCommand**， **UpdateCommand**，并**DeleteCommand**属性值，如果你想要使用批更新模式。

## <a name="adding-the-remaining-tableadapters"></a>添加剩余的 Tableadapter

到现在为止，我们只介绍了使用单个数据库表到单个 TableAdapter。 但是，Northwind 数据库包含我们需要在 web 应用程序中使用的多个相关的表。 类型化数据集可以包含多个相关数据表。 因此，若要完成我们 DAL，我们需要将数据表添加我们将使用这些教程中的其他表。 若要将新的 TableAdapter 添加到类型化数据集，打开数据集设计器，在设计器中，右键单击并选择添加 / TableAdapter。 这将创建新的 DataTable 和 TableAdapter，并引导你完成本教程中前面部分中，我们探讨该向导。

需要几分钟才能创建以下 Tableadapter 和使用下面的查询的方法。 请注意，中的查询**ProductsTableAdapter**包括子查询中获取每个产品类别和供应商的名称。 此外，如果你已已之后，你已添加 **ProductsTableAdapter** 类的 **GetProducts()** 和 **GetProductsByCategoryID(*categoryID*)** 方法。

- **ProductsTableAdapter**

  - **GetProducts**: 

      [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample10.sql)]
  - **GetProductsByCategoryID**: 

      [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample11.sql)]
  - **GetProductsBySupplierID**: 

      [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample12.sql)]
  - **GetProductByProductID**: 

      [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample13.sql)]
- **CategoriesTableAdapter**

  - **GetCategories**: 

      [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample14.sql)]
  - **GetCategoryByCategoryID**: 

      [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample15.sql)]
- **SuppliersTableAdapter**

  - **GetSuppliers**: 

      [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample16.sql)]
  - **GetSuppliersByCountry**: 

      [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample17.sql)]
  - **GetSupplierBySupplierID**: 

      [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample18.sql)]
- **EmployeesTableAdapter**

  - **GetEmployees**: 

      [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample19.sql)]
  - **GetEmployeesByManager**: 

      [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample20.sql)]
  - **GetEmployeeByEmployeeID**: 

      [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample21.sql)]


[![数据集设计器后已添加四个 Tableadapter](creating-a-data-access-layer-cs/_static/image84.png)](creating-a-data-access-layer-cs/_static/image83.png)

**图 31**:数据集设计器后四个 Tableadapter 已添加 ([单击此项可查看原尺寸图像](creating-a-data-access-layer-cs/_static/image85.png))


## <a name="adding-custom-code-to-the-dal"></a>将自定义代码添加到 DAL

将 Tableadapter 和数据表添加到类型化数据集表示为 XML 架构定义文件 (**Northwind.xsd**)。 可以通过右键单击查看此架构信息**Northwind.xsd**文件在解决方案资源管理器中，并选择查看代码。


[![Northwinds 的 XML 架构定义 (XSD) 文件类型化数据集](creating-a-data-access-layer-cs/_static/image87.png)](creating-a-data-access-layer-cs/_static/image86.png)

**图 32**:Northwinds 类型化数据集的 XML 架构定义 (XSD) 文件 ([单击此项可查看原尺寸图像](creating-a-data-access-layer-cs/_static/image88.png))


此架构信息将转换为 C# 或 Visual Basic 代码在设计时在编译时或在运行时 （如果需要），此时您可以单步执行它调试器的情况。 若要查看此自动生成的代码下降到类视图和向下钻到 TableAdapter 或类型化数据集类。 如果没有看到类视图屏幕上，转到视图菜单，选择在这里，或按 Ctrl + Shift + C。 从类视图中可以看到属性、 方法和事件的类型化数据集和 TableAdapter 类。 若要查看特定方法的代码，双击类视图中的方法名称或右键单击它并选择转到定义。


![通过选择转到定义从类视图中检查自动生成的代码](creating-a-data-access-layer-cs/_static/image89.png)

**图 33**:通过选择转到定义从类视图中检查自动生成的代码


虽然自动生成的代码可节约了大量时间，该代码通常是非常通用，需要进行自定义以满足应用程序的独特需求。 扩展自动生成的代码的风险，是生成代码的工具可能会决定是时候"重新生成"，并覆盖你的自定义。 使用.NET 2.0 的新的分部类概念，很容易将类拆分到多个文件。 这使我们能够向自动生成的类中添加我们自己的方法、 属性和事件，而无需担心如何覆盖我们自定义项的 Visual Studio。

若要演示如何自定义 DAL，让我们添加**GetProducts()** 方法**SuppliersRow**类。 **SuppliersRow**类表示中的单个记录**供应商**表; 每个供应商可以提供程序零到许多产品，因此**GetProducts()** 将返回这些指定供应商的产品。 若要完成此创建新的类文件中**应用程序\_代码**名为的文件夹**SuppliersRow.cs**并添加以下代码：

[!code-csharp[Main](creating-a-data-access-layer-cs/samples/sample22.cs)]

此分部类指示编译器，当构建**Northwind.SuppliersRow**类，以包含**GetProducts()** 我们刚才定义的方法。 如果您生成项目，然后返回到类视图会看到**GetProducts()** 现在作为一种列出**Northwind.SuppliersRow**。


![GetProducts() 方法是现在的 Northwind.SuppliersRow 类的一部分](creating-a-data-access-layer-cs/_static/image90.png)

**图 34**:**GetProducts()** 方法是现在的一部分**Northwind.SuppliersRow**类


**GetProducts()** 方法现在可以用于枚举的一套产品特定供应商，如以下代码所示：

[!code-html[Main](creating-a-data-access-layer-cs/samples/sample23.html)]

此外可以在任何 ASP 中显示此数据。NET 的数据 Web 控件。 以下页面将 GridView 控件使用两个字段：

- 显示每个供应商的名称 BoundField 和
- 包含如何控件绑定到返回的结果为 TemplateField **GetProducts()** 每个供应商的方法。

我们将介绍如何在将来的教程中显示此类母版-详细信息报表。 现在，此示例旨在演示如何使用自定义的方法添加到**Northwind.SuppliersRow**类。

SuppliersAndProducts.aspx

[!code-aspx[Main](creating-a-data-access-layer-cs/samples/sample24.aspx)]

SuppliersAndProducts.aspx.cs

[!code-csharp[Main](creating-a-data-access-layer-cs/samples/sample25.cs)]


[![在左侧列中，在右侧及其产品列出供应商的公司名称](creating-a-data-access-layer-cs/_static/image92.png)](creating-a-data-access-layer-cs/_static/image91.png)

**图 35**:在左侧列中，在右侧及其产品列出供应商的公司名称 ([单击此项可查看原尺寸图像](creating-a-data-access-layer-cs/_static/image93.png))


## <a name="summary"></a>总结

当构建 web 应用程序创建 DAL 应是你第一步，在开始创建表示层之前。 使用 Visual Studio，创建基于类型化数据集的 DAL 是可以无需编写代码在 10-15 分钟内完成的任务。 下一步的教程将制作此 DAL。 在中[下一教程](creating-a-business-logic-layer-cs.md)我们将定义的业务规则的数量，并请参阅如何在单独的业务逻辑层中实现它们。

快乐编程 ！

## <a name="further-reading"></a>其他阅读材料

在本教程中讨论的主题的详细信息，请参阅以下资源：

- [构建使用强类型化的 Tableadapter 和 DataTables VS 2005 和 ASP.NET 2.0 中的 DAL](https://weblogs.asp.net/scottgu/435498)
- [设计数据层组件和层间传递数据](https://msdn.microsoft.com/library/ms978496.aspx)
- [生成与 Visual Studio 2005 数据集设计器的数据访问层](http://www.theserverside.net/articles/showarticle.tss?id=DataSetDesigner)
- [加密 ASP.NET 2.0 中的配置信息的应用程序](http://aspnet.4guysfromrolla.com/articles/021506-1.aspx)
- [TableAdapter 概述](https://msdn.microsoft.com/library/bz9tthwx.aspx)
- [使用类型化数据集](https://msdn.microsoft.com/library/esbykkzb.aspx)
- [使用 Visual Studio 2005 和 ASP.NET 2.0 中的强类型化数据访问](http://aspnet.4guysfromrolla.com/articles/020806-1.aspx)
- [如何扩展 TableAdapter 方法](https://blogs.msdn.com/vbteam/archive/2005/05/04/ExtendingTableAdapters.aspx)
- [从存储过程中检索标量数据](http://aspnet.4guysfromrolla.com/articles/062905-1.aspx)

### <a name="video-training-on-topics-contained-in-this-tutorial"></a>在本教程中包含的主题的视频培训

- [ASP.NET 应用程序中的数据访问层](../../../videos/data-access/adonet-data-services/data-access-layers-in-aspnet-applications.md)
- [如何手动将数据集绑定到数据网格](../../../videos/data-access/adonet-data-services/how-to-manually-bind-a-dataset-to-a-datagrid.md)
- [如何使用数据集和筛选器从 ASP 应用程序](../../../videos/data-access/adonet-data-services/how-to-work-with-datasets-and-filters-from-an-asp-application.md)

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)的七个部 asp/ASP.NET 书籍并创办了作者[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年以来一直致力于 Microsoft Web 技术。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 2.0 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，其中，请参阅[ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)。

## <a name="special-thanks-to"></a>特别感谢

很多有用的审阅者已评审本系列教程。 本教程中的潜在顾客审阅者已 Ron 绿色、 Hilton Giesenow、 Dennis Patterson、 Liz Shulok，Abel Gomez 和 Carlos Santos。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [下一页](creating-a-business-logic-layer-cs.md)

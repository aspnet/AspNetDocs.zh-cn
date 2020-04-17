---
uid: web-forms/overview/moving-to-aspnet-20/data-source-controls
title: 数据源控制 |微软文档
author: rick-anderson
description: ASP.NET 1.x 中的 DataGrid 控件标志着 Web 应用程序中数据访问的重大改进。 然而，它并不像它本来可以的那么用户友好。
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 78fd0e92-f9c6-4e96-a5e9-0375b307a828
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/data-source-controls
msc.type: authoredcontent
ms.openlocfilehash: 2b4302b509af57dc5d9db9de9ee824df767d0737
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81540215"
---
# <a name="data-source-controls"></a>数据源控件

由[微软](https://github.com/microsoft)

> ASP.NET 1.x 中的 DataGrid 控件标志着 Web 应用程序中数据访问的重大改进。 然而，它并不像它本来可以对用户友好。 它仍然需要大量的代码才能从中获得许多有用的功能。 这就是 1.x 中所有数据访问努力中的模型。

ASP.NET 1.x 中的 DataGrid 控件标志着 Web 应用程序中数据访问的重大改进。 然而，它并不像它本来可以对用户友好。 它仍然需要大量的代码才能从中获得许多有用的功能。 这就是 1.x 中所有数据访问努力中的模型。

ASP.NET 2.0 部分使用数据源控件解决了这个问题。 ASP.NET 2.0 中的数据源控件为开发人员提供了用于检索数据、显示数据和编辑数据的声明性模型。 数据源控件的目的是向数据绑定控件提供数据一致的表示形式，而不管数据源如何。 ASP.NET 2.0 中数据源控件的核心是 DataSourceControl 抽象类。 DataSourceControl 类提供了 IDataSource 接口和 IListSource 接口的基本实现，后者允许您将数据源控件指定为数据绑定控件的 DataSource（通过稍后讨论的新 DataSourceId 属性），并将其中的数据公开为列表。 数据源控件的每个数据列表都公开为 DataSourceView 对象。 IDataSource 接口提供了对 DataSourceView 实例的访问。 例如，GetViewNames 方法返回一个 ICollection，允许您枚举与特定数据源控件关联的 DataSourceViews，GetView 方法允许您按名称访问特定的 DataSourceView 实例。

数据源控件没有用户界面。 它们作为服务器控件实现，以便它们可以支持声明性语法，以便根据需要访问页面状态。 数据源控件不向客户端呈现任何 HTML 标记。

> [!NOTE]
> 稍后您将看到，使用数据源控件还可以获得缓存好处。

## <a name="storing-connection-strings"></a>存储连接字符串

在研究如何配置数据源控件之前，我们应该在有关连接字符串ASP.NET 2.0 中介绍新功能。 ASP.NET 2.0 在配置文件中引入了一个新部分，允许您轻松存储可在运行时动态读取的连接字符串。 连接&lt;字符串&gt;部分便于存储连接字符串。

下面的代码段添加了一个新的连接字符串。

[!code-xml[Main](data-source-controls/samples/sample1.xml)]

> [!NOTE]
> &lt;与 appSettings&gt;部分一样，&lt;连接字符串&gt;部分显示在配置文件中的&lt;system.web&gt;部分之外。

要使用此连接字符串，可以在设置服务器控件的 ConnectString 属性时使用以下语法。

[!code-aspx[Main](data-source-controls/samples/sample2.aspx)]

还可以&lt;加密连接&gt;字符串部分，以便不公开敏感信息。 这一能力将在后面的模块中介绍。

## <a name="caching-data-sources"></a>缓存数据源

每个 DataSourceControl 提供四个属性来配置缓存;启用缓存、缓存持续时间、缓存过期策略和缓存密钥依赖性。

## <a name="enablecaching"></a>启用缓存

启用缓存是一个布尔属性，用于确定是否为数据源控件启用缓存。

## <a name="cacheduration-property"></a>缓存持续时间属性

"缓存持续时间"属性设置缓存保持有效的秒数。 将此属性设置为**0**会导致缓存保持有效，直到显式失效。

## <a name="cacheexpirationpolicy-property"></a>缓存过期策略属性

缓存过期策略属性可以设置为**绝对**或**滑动**。 将其设置为"绝对"意味着缓存数据的最大时间是 CacheDuration 属性指定的秒数。 通过将它设置为"滑动"，执行每个操作时将重置过期时间。

## <a name="cachekeydependency-property"></a>缓存密钥依赖属性

如果为 CacheKey 依赖项属性指定了字符串值，ASP.NET将基于该字符串设置新的缓存依赖项。 这允许您通过简单地更改或删除 CacheKey 依赖项来显式使缓存无效。

**重要提示**：如果启用了模拟，并且对数据源和/或数据内容的访问基于客户端标识，则建议通过设置启用缓存设置为 False 来禁用缓存。 如果在此方案中启用了缓存，并且最初请求数据的用户以外的用户发出请求，则不会强制执行对数据源的授权。 数据将仅从缓存中提供。

## <a name="the-sqldatasource-control"></a>SqlDataSource 控件

SqlDataSource 控件允许开发人员访问存储在支持ADO.NET的任何关系数据库中的数据。 它可以使用 System.Data.SqlClient 提供程序访问 SQL Server 数据库、System.Data.OleDb 提供程序、系统.Data.Odbc 提供程序或 System.Data.OracleClient 提供程序来访问 Oracle。 因此，SqlDataSource 当然不仅用于访问 SQL Server 数据库中的数据。

为了使用 SqlDataSource，您只需为 ConnectString 属性提供一个值，并指定 SQL 命令或存储过程。 SqlDataSource 控件负责使用底层ADO.NET体系结构。 它打开连接，查询数据源或执行存储过程，返回数据，然后为您关闭连接。

> [!NOTE]
> 由于 DataSourceControl 类会自动为您关闭连接，因此它应该减少因数据库连接泄漏而生成的客户呼叫数。

下面的代码段使用存储在配置文件中的连接字符串将下拉列表控件绑定到 SqlDataSource 控件，如上所示。

[!code-aspx[Main](data-source-controls/samples/sample3.aspx)]

如上所述，SqlDataSource 的 DataSourceMode 属性指定数据源的模式。 在上面的示例中，数据源模式设置为数据阅读器。 在这种情况下，SqlDataSource 将使用仅行和只读游标返回 IDataReader 对象。 返回的指定类型的对象由所使用的提供程序控制。 在这种情况下，我使用的是 Web.config 文件的&lt;connectStrings&gt;部分中指定的 System.Data.SqlClient 提供程序。 因此，返回的对象将采用 SqlDataReader 类型。 通过指定 DataSet 的 DataSourceMode 值，数据可以存储在服务器上的 DataSet 中。 此模式允许您添加排序、分页等功能。如果我将 SqlDataSource 数据绑定到 GridView 控件，我会选择 DataSet 模式。 但是，在下拉列表的情况下，数据阅读器模式是正确的选择。

> [!NOTE]
> 缓存 SqlDataSource 或 AccessDataSource 时，必须将 DataSourceMode 属性设置为 DataSet。 如果使用 DataReader 的 DataSource 模式启用缓存，则会出现异常。

## <a name="sqldatasource-properties"></a>SqlDataSource 属性

以下是 SqlDataSource 控件的一些属性。

### <a name="cancelselectonnullparameter"></a>取消选择无效参数

布尔值，用于指定如果其中一个参数为空，是否取消选择命令。 默认值为 True。

### <a name="conflictdetection"></a>冲突检测

在多个用户可能同时更新数据源的情况下，冲突检测属性确定 SqlDataSource 控件的行为。 此属性计算为冲突选项枚举的值之一。 这些值是**比较所有值**和**覆盖更改**。 如果设置为"覆盖更改"，则最后一个将数据写入数据源的人员将覆盖任何以前的更改。 但是，如果冲突检测属性设置为比较 AllValue，则为 SelectCommand 返回的列创建参数，并创建参数以在每个列中保存原始值，从而允许 SqlDataSource 确定自执行 SelectCommand 以来值是否已更改。

### <a name="deletecommand"></a>删除命令

设置或获取从数据库中删除行时使用的 SQL 字符串。 这可以是 SQL 查询或存储过程名称。

### <a name="deletecommandtype"></a>删除命令类型

设置或获取删除命令的类型，SQL 查询（文本）或存储过程（存储过程）。

### <a name="deleteparameters"></a>删除参数

返回与 SqlDataSource 控件关联的 SqlDataSourceView 对象的 DeleteCommand 使用的参数。

### <a name="oldvaluesparameterformatstring"></a>旧值参数格式字符串

此属性用于指定原始值参数的格式，在冲突检测属性设置为比较AllValue的情况下。 默认值表示{0}原始值参数的名称与原始参数相同。 换句话说，如果字段名称为 EmployID，则原始值参数将为@EmployeeID。

### <a name="selectcommand"></a>SelectCommand

设置或获取用于从数据库中检索数据的 SQL 字符串。 这可以是 SQL 查询或存储过程名称。

### <a name="selectcommandtype"></a>选择命令类型

设置或获取选择命令的类型，SQL 查询（文本）或存储过程（存储过程）。

### <a name="selectparameters"></a>选择参数

返回与 SqlDataSource 控件关联的 SqlDataSource 对象的 SelectCommand 使用的参数。

### <a name="sortparametername"></a>排序参数名称

获取或设置在排序数据源控件检索的数据时使用的存储过程参数的名称。 仅当 SelectCommandType 设置为存储过程时才有效。

### <a name="sqlcachedependency"></a>SqlCache 依赖性

指定 SQL Server 缓存依赖项中使用的数据库和表的分号分隔字符串。 （SQL 缓存依赖项将在后面的模块中讨论。

### <a name="updatecommand"></a>更新命令

设置或获取更新数据库中的数据时使用的 SQL 字符串。 这可以是 SQL 查询或存储过程名称。

### <a name="updatecommandtype"></a>更新命令类型

设置或获取更新命令的类型，SQL 查询（文本）或存储过程（存储过程）。

### <a name="updateparameters"></a>更新参数

返回与 SqlDataSource 控件关联的 SqlDataSourceView 对象的 UpdateCommand 使用的参数。

## <a name="the-accessdatasource-control"></a>访问数据源控件

AccessDataSource 控件派生自 SqlDataSource 类，用于将数据绑定到 Microsoft Access 数据库。 AccessDataSource 控件的 ConnectString 属性是只读属性。 DataFile 属性使用"连接字符串"属性，而不是使用 ConnectString 属性来指向访问数据库，如下所示。

[!code-aspx[Main](data-source-controls/samples/sample4.aspx)]

AccessDataSource 将始终将基本 SqlDataSource 的提供程序名称设置为系统.Data.OleDb，并使用 Microsoft.Jet.OLEDB.4.0 OLE DB 提供程序连接到数据库。 不能使用 AccessDataSource 控件连接到受密码保护的访问数据库。 如果必须连接到受密码保护的数据库，则应使用 SqlDataSource 控件。

> [!NOTE]
> 存储在网站中的访问数据库应放在应用\_数据目录中。 ASP.NET不允许浏览此目录中的文件。 使用 Access 数据库时，您需要向应用\_数据目录授予进程帐户"读取和写入"权限。

## <a name="the-xmldatasource-control"></a>XmlDataSource 控件

XmlDataSource 用于将数据绑定 XML 数据到数据绑定控件。 您可以使用 DataFile 属性绑定到 XML 文件，也可以使用 Data 属性绑定到 XML 字符串。 XmlDataSource 将 XML 属性公开为可绑定字段。 如果需要绑定到未表示为属性的值，则需要使用 XSL 转换。 您还可以使用 XPath 表达式来筛选 XML 数据。

请考虑以下 XML 文件：

[!code-xml[Main](data-source-controls/samples/sample5.xml)]

请注意，XmlDataSource 使用*人员/人员*的 XPath 属性来仅对&lt;人员&gt;节点进行筛选。 然后，使用 DataTextField 属性将数据绑定到姓氏属性。

虽然 XmlDataSource 控件主要用于将数据绑定到只读的 XML 数据，但可以编辑 XML 数据文件。 请注意，在这种情况下，自动插入、更新和删除 XML 文件中的信息不会像在其他数据源控件中那样自动发生。 相反，您必须编写代码才能使用 XmlDataSource 控件的以下方法手动编辑数据。

### <a name="getxmldocument"></a>获取Xml文档

检索包含 XmlDataSource 检索的 XML 代码的 XmlDocument 对象。

### <a name="save"></a>保存

将内存中的 XmlDocument 保存回数据源。

请务必了解，仅满足以下两个条件时，Save 方法才能工作：

1. XmlDataSource 正在使用 DataFile 属性绑定到 XML 文件，而不是数据属性以绑定到内存中的 XML 数据。
2. 不会通过"转换"或"转换文件"属性指定转换。

另请注意，当多个用户同时调用 Save 方法时，可能会产生意外的结果。

## <a name="the-objectdatasource-control"></a>对象数据源控件

对于数据源控件直接与数据存储通信的两层应用程序而言，我们覆盖的数据源控件是绝佳的选择。 但是，许多实际应用程序是多层应用程序，其中数据源控件可能需要与业务对象通信，而业务对象又与数据层通信。 在这些情况下，ObjectDataSource 很好地填充了帐单。 ObjectDataSource 与源对象结合使用。 如果对象具有实例方法而不是静态方法（在 Visual Basic 中共享），则 ObjectDataSource 控件将创建源对象的实例，调用指定的方法，并释放对象实例。 因此，对象必须是无状态的。 也就是说，对象应在单个请求的范围内获取和释放所有必需的资源。 您可以通过处理 ObjectDataSource 控件的对象创建事件来控制源对象的创建方式。 您可以创建源对象的实例，然后将 ObjectDataSourceEventArgs 类的 ObjectInstance 属性设置为该实例。 ObjectDataSource 控件将使用在对象创建事件中创建的实例，而不是自行创建实例。

如果 ObjectDataSource 控件的源对象公开可调用以检索和修改数据的公共静态方法（在 Visual Basic 中共享），则 ObjectDataSource 控件将直接调用这些方法。 如果 ObjectDataSource 控件必须创建源对象的实例才能进行方法调用，则该对象必须包括一个不采用任何参数的公共构造函数。 当 ObjectDataSource 控件创建源对象的新实例时，它将调用此构造函数。

如果源对象不包含没有参数的公共构造函数，则可以创建源对象的实例，该实例将由 ObjectDataSource 控件在 ObjectCreate 事件中使用。

## <a name="specifying-object-methods"></a>指定对象方法

ObjectDataSource 控件的源对象可以包含任意数量的用于选择、插入、更新或删除数据的方法。 这些方法由基于方法名称的 ObjectDataSource 控件调用，使用 ObjectDataSource 控件的 SelectMethod、插入方法、更新方法或 DeleteMethod 属性标识。 源对象还可以包括可选的 SelectCount 方法，该方法由使用 SelectCountMethod 属性的 ObjectDataSource 控件标识，该方法返回数据源中对象总数的计数。 在调用 Select 方法以检索数据源中用于分页时的记录总数后，ObjectDataSource 控件将调用 SelectCount 方法。

## <a name="lab-using-data-source-controls"></a>使用数据源控件的实验室

## <a name="exercise-1---displaying-data-with-the-sqldatasource-control"></a>练习 1 - 使用 SqlDataSource 控件显示数据

以下练习使用 SqlDataSource 控件连接到北风数据库。 它假定您可以访问 SQL Server 2000 实例上的北风数据库。

1. 创建新的 ASP.NET 网站。
2. 添加新的 Web.config 文件。

    1. 右键单击解决方案资源管理器中的项目，然后单击"添加新项目"。
    2. 从模板列表中选择 Web 配置文件，然后单击"添加"。
3. 编辑&lt;连接字符串&gt;部分，如下所示： 

    [!code-aspx[Main](data-source-controls/samples/sample6.aspx)]
4. 切换到代码视图，并将连接String 属性和 SelectCommand 属性添加到&lt;asp：SqlDataSource&gt;控件，如下所示： 

    [!code-aspx[Main](data-source-controls/samples/sample7.aspx)]
5. 从"设计"视图中，添加新的 GridView 控件。
6. 从 GridView 任务菜单中的"选择数据源"下拉列表，选择 SqlDataSource1。
7. 右键单击 Default.aspx，然后从菜单中选择"在浏览器中查看"。 当提示保存时，单击"是"。
8. GridView 显示"产品"表中的数据。

## <a name="exercise-2---editing-data-with-the-sqldatasource-control"></a>练习 2 - 使用 SqlDataSource 控件编辑数据

下面的练习演示如何使用声明性语法对下拉列表控件进行数据绑定，并允许您编辑下拉列表控件中显示的数据。

1. 在"设计"视图中，从 Default.aspx 中删除 GridView 控件。 

    **重要提示**：将 SqlDataSource 控件保留在页面上。
2. 将下拉列表控件添加到 Default.aspx。
3. 切换到源视图。
4. 将 DataSourceId、数据文本字段和 DataValueField 属性添加到&lt;asp：下拉&gt;列表控件，如下所示： 

    [!code-aspx[Main](data-source-controls/samples/sample8.aspx)]
5. 保存默认.aspx 并在浏览器中查看它。 请注意，下拉列表包含来自北风数据库的所有产品。
6. 关闭浏览器。
7. 在 Default.aspx 的源视图中，在下拉列表控件下方添加新的 TextBox 控件。 将 TextBox 的 ID 属性更改为 txtProduct 名称。
8. 在"文本框"控件下，添加新的"按钮"控件。 将按钮的 ID 属性更改为 btnUpdate，将文本属性更改为 **"更新产品名称**"。
9. 在 Default.aspx 的源视图中，向 SqlDataSource 标记添加 UpdateCommand 属性和两个新的 Update 参数，如下所示： 

    [!code-aspx[Main](data-source-controls/samples/sample9.aspx)]

    > [!NOTE]
    > 请注意，此代码中添加了两个更新参数（产品名称和产品 ID）。 这些参数映射到 txtProduct 名称文本框的文本属性和 ddlProducts 下拉列表的"选定值"属性。
10. 切换到"设计"视图并双击"按钮"控件以添加事件处理程序。
11. 将以下代码添加到 btnUpdate\_单击代码： 

    [!code-csharp[Main](data-source-controls/samples/sample10.cs)]
12. 右键单击 Default.aspx 并选择在浏览器中查看它。 当提示保存所有更改时，单击"是"。
13. ASP.NET 2.0 部分类允许在运行时进行编译。 无需构建应用程序，以便看到代码更改生效。
14. 从下拉列表中选择产品。
15. 在 TextBox 中输入所选产品的新名称，然后单击"更新"按钮。
16. 产品名称在数据库中更新。

## <a name="exercise-3-using-the-objectdatasource-control"></a>练习 3 使用对象数据源控件

本练习将演示如何使用 ObjectDataSource 控件和源对象与 Northwind 数据库进行交互。

1. 右键单击解决方案资源管理器中的项目，然后单击"添加新项目"。
2. 在模板列表中选择"Web 窗体"。 将名称更改为对象.aspx，然后单击"添加"。
3. 右键单击解决方案资源管理器中的项目，然后单击"添加新项目"。
4. 在模板列表中选择类。 将类的名称更改为NorthwindData.cs，然后单击"添加"。
5. 当提示将类添加到应用\_代码文件夹时，单击"是"。
6. 将以下代码添加到NorthwindData.cs文件： 

    [!code-csharp[Main](data-source-controls/samples/sample11.cs)]
7. 将以下代码添加到对象的"源"视图. 

    [!code-aspx[Main](data-source-controls/samples/sample12.aspx)]
8. 保存所有文件和浏览对象.aspx。
9. 通过查看详细信息、编辑员工、添加员工和删除员工与界面进行交互。

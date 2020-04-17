---
uid: mvc/overview/older-versions-1/models-data/creating-model-classes-with-linq-to-sql-vb
title: 使用 LINQ 创建模型类到 SQL （VB） |微软文档
author: rick-anderson
description: 本教程的目的是解释为mVC应用程序创建模型类的方法ASP.NET。 在本教程中，您将了解如何构建模型 c...
ms.author: riande
ms.date: 10/07/2008
ms.assetid: a4a25a75-d71f-4509-98b4-df72e748985a
msc.legacyurl: /mvc/overview/older-versions-1/models-data/creating-model-classes-with-linq-to-sql-vb
msc.type: authoredcontent
ms.openlocfilehash: 1a6133227eedc8934af7bf872532ca667b97d0f8
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542698"
---
# <a name="creating-model-classes-with-linq-to-sql-vb"></a>使用 LINQ to SQL 创建模型类 (VB)

由[微软](https://github.com/microsoft)

[下载 PDF](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_10_VB.pdf)

> 本教程的目的是解释为mVC应用程序创建模型类的方法ASP.NET。 在本教程中，您将了解如何利用 Microsoft LINQ 到 SQL 构建模型类并执行数据库访问。

本教程的目的是解释为mVC应用程序创建模型类的方法ASP.NET。 在本教程中，您将了解如何利用 Microsoft LINQ 到 SQL 构建模型类并执行数据库访问。

在本教程中，我们将构建一个基本的 Movie 数据库应用程序。 我们从以最快、最简单的方式创建 Movie 数据库应用程序开始。 我们直接从控制器操作执行所有数据访问。

接下来，您将了解如何使用存储库模式。 使用存储库模式需要多一点工作。 但是，采用此模式的优点是，它使您能够构建能够适应更改且易于测试的应用程序。

## <a name="what-is-a-model-class"></a>什么是模型类？

MVC 模型包含 MVC 视图或 MVC 控制器中未包含的所有应用程序逻辑。 特别是，MVC 模型包含所有应用程序业务和数据访问逻辑。

您可以使用各种不同的技术来实现数据访问逻辑。 例如，您可以使用 Microsoft 实体框架、NHibernate、亚音速或ADO.NET类构建数据访问类。

在本教程中，我使用 LINQ 到 SQL 来查询和更新数据库。 LINQ 到 SQL 为您提供了一种非常简单的与 Microsoft SQL Server 数据库交互的方法。 但是，请务必了解，ASP.NET MVC 框架不以任何方式与 LINQ 绑定到 SQL。 ASP.NET MVC 与任何数据访问技术兼容。

## <a name="create-a-movie-database"></a>创建影片数据库

在本教程中，为了说明如何构建模型类，我们构建了一个简单的 Movie 数据库应用程序。 第一步是创建新数据库。 右键单击解决方案资源管理器\_窗口中的应用数据文件夹，然后选择菜单选项 **"添加，新项目**"。 选择 SQL Server 数据库模板，给它取名为 MoviesDB.mdf，然后单击 **"添加**"按钮（参见图 1）。

[![添加新的 SQL 服务器数据库](creating-model-classes-with-linq-to-sql-vb/_static/image2.png)](creating-model-classes-with-linq-to-sql-vb/_static/image1.png)

**图 01**： 添加新 SQL Server 数据库 （[单击以查看全尺寸图像](creating-model-classes-with-linq-to-sql-vb/_static/image3.png)）

创建新数据库后，可以通过双击应用\_数据文件夹中的 MoviesDB.mdf 文件来打开数据库。 双击 MoviesDB.mdf 文件将打开服务器资源管理器窗口（参见图 2）。

|   | 使用可视化 Web 开发人员时，服务器资源管理器窗口称为数据库资源管理器窗口。 |
|---|----------------------------------------------------------------------------------------------------|
|   |                                                                                                    |

[![使用服务器资源管理器窗口](creating-model-classes-with-linq-to-sql-vb/_static/image5.png)](creating-model-classes-with-linq-to-sql-vb/_static/image4.png)

**图 02**： 使用服务器资源管理器窗口 （[单击以查看全尺寸图像](creating-model-classes-with-linq-to-sql-vb/_static/image6.png)）

我们需要向数据库中添加一个表示我们电影的表。 右键单击"表"文件夹并选择菜单选项 **"添加新表**"。 选择此菜单选项将打开表设计器（参见图 3）。

[![使用服务器资源管理器窗口](creating-model-classes-with-linq-to-sql-vb/_static/image8.png)](creating-model-classes-with-linq-to-sql-vb/_static/image7.png)

**图 03**： 表设计器 （[单击以查看全尺寸图像](creating-model-classes-with-linq-to-sql-vb/_static/image9.png)）

我们需要将以下列添加到数据库表中：

| **列名** | **数据类型** | **允许 Null 值** |
| --- | --- | --- |
| ID | Int | False |
| 标题 | 恩瓦尔查尔 （200） | False |
| 导演 | 恩瓦尔查尔 （50） | False |

您需要对 Id 列执行两项特殊操作。 首先，您需要通过选择表设计器中的列并单击键的图标，将 Id 列标记为主键列。 LINQ 到 SQL 要求您在针对数据库执行插入或更新时指定主键列。

接下来，您需要通过将值"是"分配给 **"是标识"** 属性来将 Id 列标记为标识列（参见图 3）。 标识列是一列，每当向表添加新数据行时，将自动分配新编号。

进行这些更改后，将表与名称 tblMovie 保存。 您可以通过单击"保存"按钮保存表。

## <a name="create-linq-to-sql-classes"></a>创建 LINQ 到 SQL 类

我们的 MVC 模型将包含表示 tblMovie 数据库表的 LINQ 到 SQL 类。 创建这些 LINQ 到 SQL 类的最简单方法是右键单击"模型"文件夹，选择 **"添加、新建项目**"，选择 LINQ 到 SQL 类模板，为类指定名称 Movie.dbml，然后单击 **"添加**"按钮（参见图 4）。

[![将 LINQ 创建到 SQL 类](creating-model-classes-with-linq-to-sql-vb/_static/image11.png)](creating-model-classes-with-linq-to-sql-vb/_static/image10.png)

**图 04**： 创建 LINQ 到 SQL 类 （[单击以查看全尺寸图像](creating-model-classes-with-linq-to-sql-vb/_static/image12.png)）

在创建到 SQL 类的影片 LINQ 后，将立即出现对象关系设计器。 您可以将数据库表从服务器资源管理器窗口拖动到对象关系设计器上，以创建 LINQ 到表示特定数据库表的 SQL 类。 我们需要将 tblMovie 数据库表添加到对象关系设计器上（参见图 4）。

[![使用对象关系设计器](creating-model-classes-with-linq-to-sql-vb/_static/image14.png)](creating-model-classes-with-linq-to-sql-vb/_static/image13.png)

**图 05**：使用对象关系设计器 （[单击以查看全尺寸图像](creating-model-classes-with-linq-to-sql-vb/_static/image15.png)）

默认情况下，对象关系设计器创建与拖动到设计器的数据库表名称完全相同的类。 但是，我们不想调用我们的类 tblMovie。 因此，单击设计器中的类的名称并将类的名称更改为"Movie"。

最后，请记住单击 **"保存**"按钮（软盘的图片）以将 LINQ 保存到 SQL 类。 否则，对象关系设计器不会生成 LINQ 到 SQL 类。

## <a name="using-linq-to-sql-in-a-controller-action"></a>在控制器操作中使用 LINQ 到 SQL

现在，我们有了 LINQ 到 SQL 类，我们可以使用这些类从数据库中检索数据。 在本节中，您将学习如何直接在控制器操作中使用 LINQ 到 SQL 类。 我们将在 MVC 视图中显示 tblMovies 数据库表中的影片列表。

首先，我们需要修改 HomeController 类。 此类可以在应用程序的"控制器"文件夹中找到。 修改类，使其看起来像清单 1 中的类。

**清单1 |`Controllers\HomeController.vb`**

[!code-vb[Main](creating-model-classes-with-linq-to-sql-vb/samples/sample1.vb)]

清单 1 中的 Index（） 操作使用 LINQ 到 SQL 数据上下文类（MovieDataContext）来表示 MovieDB 数据库。 MoveDataContext 类由可视化工作室对象关系设计器生成。

对 DataContext 执行 LINQ 查询，以便从 tblMovies 数据库表中检索所有影片。 影片列表分配给名为影片的本地变量。 最后，影片列表通过视图数据传递到视图。

为了显示影片，我们接下来需要修改索引视图。 您可以在"视图"文件夹中找到"索引"视图。 更新索引视图，使其看起来像清单 2 中的视图。

**清单2 |`Views\Home\Index.aspx`**

[!code-aspx[Main](creating-model-classes-with-linq-to-sql-vb/samples/sample2.aspx)]

请注意，修改后的索引视图在视图顶部&lt;包含 %# 导入&gt;命名空间 % 指令。 此指令导入 MvcApplication1 命名空间。 我们需要这个命名空间，以便与视图中的模型类（尤其是 Movie 类）配合使用。

清单 2 中的视图包含一个 For Each 循环，该循环循环循环通过 ViewData.Model 属性表示的所有项。 为每个影片显示"标题"属性的值。

请注意，ViewData.Model 属性的值将转换为 IE500。 这是必要的，以循环浏览ViewData.Model的内容。 此处的另一个选项是创建强类型视图。 创建强类型视图时，将 ViewData.Model 属性转换为视图的代码后面类中的特定类型。

如果在修改 HomeController 类和索引视图后运行应用程序，则您将获得一个空白页。 您将获得空白页，因为 tblMovies 数据库表中没有影片记录。

为了将记录添加到 tblMovies 数据库表，请右键单击服务器资源管理器窗口中的 tblMovies 数据库表（可视化 Web 开发人员中的数据库资源管理器窗口），然后选择菜单选项 **"显示表数据**"。 您可以使用显示的网格插入影片记录（参见图 5）。

[![插入影片](creating-model-classes-with-linq-to-sql-vb/_static/image17.png)](creating-model-classes-with-linq-to-sql-vb/_static/image16.png)

**图 06**： 插入影片（[单击以查看全尺寸图像](creating-model-classes-with-linq-to-sql-vb/_static/image18.png)）

将一些数据库记录添加到 tblMovies 表并运行应用程序后，您将看到图 7 中的页面。 所有影片数据库记录都显示在项目符号列表中。

[![使用"索引"视图显示影片](creating-model-classes-with-linq-to-sql-vb/_static/image20.png)](creating-model-classes-with-linq-to-sql-vb/_static/image19.png)

**图 07**： 显示带有索引视图的影片（[单击以查看全尺寸图像](creating-model-classes-with-linq-to-sql-vb/_static/image21.png)）

## <a name="using-the-repository-pattern"></a>使用存储库模式

在上一节中，我们直接在控制器操作中使用 LINQ 到 SQL 类。 我们直接从索引（） 控制器操作中使用 MovieDataContext 类。 在简单的应用程序的情况下，这样做没有错。 但是，在控制器类中直接使用 LINQ 到 SQL 会在需要构建更复杂的应用程序时出现问题。

使用 LINQ 到控制器类中的 SQL 使将来很难切换数据访问技术。 例如，您可能决定从使用 Microsoft LINQ 切换到 SQL，转而使用 Microsoft 实体框架作为数据访问技术。 在这种情况下，您需要重写访问应用程序内数据库的每个控制器。

在控制器类中使用 LINQ 到 SQL 也会使应用程序生成单元测试变得困难。 通常，在执行单元测试时，您不希望与数据库进行交互。 您希望使用单元测试来测试应用程序逻辑，而不是数据库服务器。

为了构建一个更适应未来更改且更易于测试的 MVC 应用程序，应考虑使用存储库模式。 使用存储库模式时，将创建一个单独的存储库类，其中包含所有数据库访问逻辑。

创建存储库类时，将创建一个表示存储库类使用的所有方法的接口。 在控制器中，您可以根据接口而不是存储库编写代码。 这样，将来可以使用不同的数据访问技术实现存储库。

清单3中的接口名为 IMovieRepository，它表示名为 ListAll（） 的单个方法。

**清单3 |`Models\IMovieRepository.vb`**

[!code-vb[Main](creating-model-classes-with-linq-to-sql-vb/samples/sample3.vb)]

清单4中的存储库类实现了 IMovie存储库接口。 请注意，它包含一个名为 ListAll（） 的方法，对应于 IMovieRepository 接口所需的方法。

**清单4 |`Models\MovieRepository.vb`**

[!code-vb[Main](creating-model-classes-with-linq-to-sql-vb/samples/sample4.vb)]

最后，清单 5 中的电影控制器类使用存储库模式。 它不再直接使用 LINQ 到 SQL 类。

**清单5 |`Controllers\MoviesController.vb`**

[!code-vb[Main](creating-model-classes-with-linq-to-sql-vb/samples/sample5.vb)]

请注意，清单 5 中的 MoviesController 类有两个构造函数。 当应用程序运行时，将调用第一个构造函数，即无参数构造函数。 此构造函数创建 MovieRepository 类的实例并将其传递给第二个构造函数。

第二个构造函数具有单个参数：IMovie存储库参数。 此构造函数只需将参数的值分配给名为\_存储库的类级字段。

MoviesController 类正在利用称为依赖项注入模式的软件设计模式。 特别是，它使用名为构造函数依赖项注入的内容。 通过阅读马丁·福勒的以下文章，您可以阅读有关此模式的更多内容：

[http://martinfowler.com/articles/injection.html](http://martinfowler.com/articles/injection.html)

请注意，MovieController 类中的所有代码（第一个构造函数除外）与 IMovieRepository 接口而不是实际的 MovieRepository 类进行交互。 代码与抽象接口而不是接口的具体实现进行交互。

如果要修改应用程序使用的数据访问技术，只需使用使用替代数据库访问技术的类实现 IMovieRepository 接口即可。 例如，您可以创建实体框架电影存储库类或子声波电影存储库类。 由于控制器类是针对接口编程的，因此可以将 IMovieRepository 的新实现传递给控制器类，并且该类将继续工作。

此外，如果要测试 MovieController 类，则可以将假影片存储库类传递给电影控制器。 可以使用一个类实现 IMovieRepository 类，该类实际上不访问数据库，但包含 IMovieRepository 接口的所有必需方法。 这样，您可以单元测试 MoviesController 类，而无需实际访问实际数据库。

## <a name="summary"></a>总结

本教程的目的是演示如何利用 Microsoft LINQ 到 SQL 来创建 MVC 模型类。 我们研究了在mVC应用程序中显示数据库数据的两种策略ASP.NET。 首先，我们创建了 LINQ 到 SQL 类，并直接在控制器操作中使用这些类。 使用 LINQ 到控制器中的 SQL 类使您能够在 MVC 应用程序中快速轻松地显示数据库数据。

接下来，我们探索了一条稍微困难但绝对更良性的显示数据库数据的途径。 我们利用了存储库模式，将所有数据库访问逻辑放在一个单独的存储库类中。 在我们的控制器中，我们针对接口而不是具体类编写了所有代码。 存储库模式的优点是，它使我们能够在未来轻松更改数据库访问技术，并使我们能够轻松测试我们的控制器类。

> [!div class="step-by-step"]
> [上一页](creating-model-classes-with-the-entity-framework-vb.md)
> [下一页](displaying-a-table-of-database-data-vb.md)

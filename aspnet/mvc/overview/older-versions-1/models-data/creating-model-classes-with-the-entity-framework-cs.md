---
uid: mvc/overview/older-versions-1/models-data/creating-model-classes-with-the-entity-framework-cs
title: 使用实体框架 （C#） 创建模型类 |微软文档
author: rick-anderson
description: 在本教程中，您将了解如何将 ASP.NET MVC 与 Microsoft 实体框架一起使用。 您将了解如何使用实体向导创建ADO.NET实体 Da...
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 61644169-e8b1-45dd-bf96-9c2301b69879
msc.legacyurl: /mvc/overview/older-versions-1/models-data/creating-model-classes-with-the-entity-framework-cs
msc.type: authoredcontent
ms.openlocfilehash: 716d34167258b1005b25b1cd11bfaa6d80763320
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542659"
---
# <a name="creating-model-classes-with-the-entity-framework-c"></a>使用 Entity Framework 创建模型类 (C#)

由[微软](https://github.com/microsoft)

> 在本教程中，您将了解如何将 ASP.NET MVC 与 Microsoft 实体框架一起使用。 您将了解如何使用实体向导创建ADO.NET实体数据模型。 在本教程中，我们将构建一个 Web 应用程序，说明如何使用实体框架选择、插入、更新和删除数据库数据。

本教程的目的是说明如何在构建ASP.NET MVC 应用程序时使用 Microsoft 实体框架创建数据访问类。 本教程假定之前对 Microsoft 实体框架没有了解。 在本教程结束时，您将了解如何使用实体框架来选择、插入、更新和删除数据库记录。

Microsoft 实体框架是一个对象关系映射 （O/RM） 工具，使您能够从数据库自动生成数据访问层。 实体框架使您能够避免手动构建数据访问类的繁琐工作。

为了说明如何使用微软实体框架进行ASP.NET MVC，我们将构建一个简单的示例应用程序。 我们将创建一个影片数据库应用程序，使您能够显示和编辑影片数据库记录。

本教程假定您拥有 Visual Studio 2008 或带 Service Pack 1 的可视化 Web 开发人员 2008。 您需要服务包 1 才能使用实体框架。 您可以通过以下地址下载 Visual Studio 2008 服务包 1 或带服务包 1 的可视化 Web 开发人员：

> [https://www.asp.net/downloads/](https://www.asp.net/downloads)

> [!NOTE] 
> 
> ASP.NET MVC 和 Microsoft 实体框架之间没有基本联系。 实体框架有几个替代方法可用于mVCASP.NET。 例如，您可以使用其他 O/RM 工具（如 Microsoft LINQ 到 SQL、NHibernate 或 SubSonic）构建 MVC 模型类。

## <a name="creating-the-movie-sample-database"></a>创建影片示例数据库

影片数据库应用程序使用名为"Movie"的数据库表，其中包含以下列：

| 列名 | 数据类型 | 允许 Nulls？ | 是主键吗？ |
| --- | --- | --- | --- |
| ID | int | False | True |
| 标题 | 恩瓦尔查尔 （100） | False | False |
| 导演 | 恩瓦尔查尔 （100） | False | False |

您可以按照以下步骤将此表添加到ASP.NET MVC 项目中：

1. 右键单击"解决方案\_资源管理器"窗口中的应用数据文件夹，然后选择菜单选项 **"添加，新建项目"。**
2. 在 **"添加新项目"** 对话框中，选择**SQL Server 数据库**，为数据库指定名称 MoviesDB.mdf，然后单击"**添加**"按钮。
3. 双击 MoviesDB.mdf 文件以打开服务器资源管理器/数据库资源管理器窗口。
4. 展开 MoviesDB.mdf 数据库连接，右键单击"表"文件夹，然后选择菜单选项 **"添加新表**"。
5. 在表设计器中，添加 Id、标题和控制器列。
6. 单击 **"保存**"按钮（它有软盘的图标）以保存新表的名称"电影"。

创建"影片"数据库表后，应向该表添加一些示例数据。 右键单击"影片"表并选择菜单选项 **"显示表数据**"。 您可以将假影片数据输入显示的网格中。

## <a name="creating-the-adonet-entity-data-model"></a>创建ADO.NET实体数据模型

为了使用实体框架，您需要创建实体数据模型。 您可以使用可视化工作室*实体数据模型向导*从数据库自动生成实体数据模型。

执行以下步骤:

1. 右键单击"解决方案资源管理器"窗口中的"模型"文件夹，然后选择菜单选项 **"添加，新项目**"。
2. 在"**添加新项目"** 对话框中，选择"数据"类别（参见图 1）。
3. 选择**ADO.NET实体数据模型**模板，为实体数据模型指定名称"电影 DBModel.edmx"，然后单击 **"添加**"按钮。 单击 **"添加**"按钮将启动"数据模型向导"。
4. 在 **"选择模型内容"** 步骤中，选择"**从数据库生成**"选项，然后单击 **"下一步**"按钮（参见图 2）。
5. 在 **"选择数据连接**"步骤中，选择 MoviesDB.mdf 数据库连接，输入实体连接设置名称"电影 DB实体"，然后单击 **"下一步**"按钮（参见图 3）。
6. 在 **"选择数据库对象**"步骤中，选择"影片数据库"表并单击 **"完成"** 按钮（参见图 4）。

完成这些步骤后，将打开ADO.NET实体数据模型设计器（实体设计器）。

**图 1 = 创建新的实体数据模型**

![clip_image002](creating-model-classes-with-the-entity-framework-cs/_static/image1.jpg)

**图 2 = 选择模型内容步骤**

![clip_image004](creating-model-classes-with-the-entity-framework-cs/_static/image2.jpg)

**图 3 = 选择数据连接**

![clip_image006](creating-model-classes-with-the-entity-framework-cs/_static/image3.jpg)

**图 4 = 选择数据库对象**

![clip_image008](creating-model-classes-with-the-entity-framework-cs/_static/image4.jpg)

#### <a name="modifying-the-adonet-entity-data-model"></a>修改ADO.NET实体数据模型

创建实体数据模型后，可以使用实体设计器修改模型（参见图 5）。 您可以随时通过双击解决方案资源管理器窗口中的"模型"文件夹中的"电影 DBModel.edmx 文件"来打开实体设计器。

**图 5 = ADO.NET实体数据模型设计器**

![clip_image010](creating-model-classes-with-the-entity-framework-cs/_static/image5.jpg)

例如，可以使用实体设计器更改实体模型数据向导生成的类的名称。 向导创建了名为"电影"的新数据访问类。 换句话说，向导为类指定与数据库表相同的名称。 由于我们将使用此类来表示特定的"影片"实例，因此应将类从"影片"重命名为"影片"。

如果要重命名实体类，可以双击实体设计器中的类名称并输入新名称（参见图 6）。 或者，您可以在实体设计器中选择实体后，在"属性"窗口中更改实体的名称。

**图 6 = 更改实体名称**

![clip_image012](creating-model-classes-with-the-entity-framework-cs/_static/image6.jpg)

请记住，通过单击"保存"按钮（软盘的图标）进行修改后保存实体数据模型。 在后台，实体设计器生成一组 C# 类。 您可以通过从解决方案资源管理器窗口中打开MoviesDBModel.Designer.cs文件来查看这些类。

不要修改Designer.cs文件中的代码，因为下次使用实体设计器时，您的更改将被覆盖。 如果要扩展Designer.cs文件中定义的实体类的功能，则可以在单独的文件中创建*部分类*。

#### <a name="selecting-database-records-with-the-entity-framework"></a>使用实体框架选择数据库记录

让我们通过创建显示影片记录列表的页面开始构建影片数据库应用程序。 清单 1 中的主控制器公开名为 Index（） 的操作。 索引（） 操作利用实体框架从影片数据库表中返回所有影片记录。

**清单1 = 控制器\主控制器.cs**

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample1.cs)]

请注意，清单 1 中的控制器包括一个构造函数。 构造函数初始化名为\_db 的类级字段。 db\_字段表示由 Microsoft 实体框架生成的数据库实体。 db\_字段是实体设计器生成的 MoviesDBEntity 类的实例。

为了在主控制器中使用MoviesDBEntity类，必须导入 MovieEntityApp.models 命名空间 *（MVCProjectName*）。型号）。

db\_字段在 Index（） 操作中使用，以从"影片"数据库表中检索记录。 表达式\_db。MovieSet 表示"影片"数据库表中的所有记录。 ToList（） 方法用于将影片集转换为影片对象的泛型集合（列表&lt;影片）。&gt;

影片记录在 LINQ 到实体的帮助下检索。 清单 1 中的 Index（） 操作使用 LINQ*方法语法*来检索数据库记录集。 如果您愿意，可以使用 LINQ*查询语法*。 以下两个语句执行相同的操作：

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample2.cs)]

使用您认为最直观的 LINQ 语法（方法语法或查询语法）。 这两种方法在性能上没有差别 ，唯一的区别是风格。

清单 2 中的视图用于显示影片记录。

**清单 2 = 视图\home_Index.aspx**

[!code-aspx[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample3.aspx)]

清单 2 中的视图包含一个**foreach**循环，该循环循环循环遍历每个影片记录并显示影片记录的标题和导演属性的值。 请注意，每个记录旁边都会显示"编辑"和"删除"链接。 此外，视图底部还显示"添加影片"链接（参见图 7）。

**图 7 = 索引视图**

![clip_image014](creating-model-classes-with-the-entity-framework-cs/_static/image7.jpg)

索引视图是*键入的视图*。 索引视图包括一个&lt;%@&gt; Page % 指令，该指令具有*继承*属性，该属性将模型属性转换为影片对象（列表&lt;影片）的强力类型泛型列表集合。

## <a name="inserting-database-records-with-the-entity-framework"></a>将数据库记录插入实体框架

您可以使用实体框架轻松将新记录插入到数据库表中。 清单3包含添加到主控制器类的两个新操作，可用于将新记录插入到 Movie 数据库表中。

**清单3 = 控制器\主控制器.cs（添加方法）**

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample4.cs)]

第一个 Add（） 操作仅返回视图。 该视图包含用于添加新影片数据库记录的窗体（参见图 8）。 提交表单时，将调用第二个 Add（） 操作。

请注意，第二个 Add（） 操作用 AcceptVerbs 属性进行修饰。 仅当执行 HTTP POST 操作时，才能调用此操作。 换句话说，此操作只能在发布 HTML 窗体时调用。

第二个 Add（） 操作在 ASP.NET MVC TryUpdateModel（） 方法的帮助下创建实体框架影片类的新实例。 TryUpdateModel（） 方法获取传递给 Add（） 方法的窗体集合中的字段，并将这些 HTML 表单字段的值分配给 Movie 类。

使用实体框架时，在使用 TryUpdateModel 或 UpdateModel 方法更新实体类的属性时，必须提供属性的"白名单"。

接下来，Add（） 操作执行一些简单的表单验证。 该操作验证"标题"和"控制器"属性是否具有值。 如果存在验证错误，则会向 ModelState 添加验证错误消息。

如果没有验证错误，则在实体框架的帮助下，将新的影片记录添加到"电影"数据库表。 新记录将添加到数据库中，并带有以下两行代码：

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample5.cs)]

第一行代码将新的影片实体添加到实体框架正在跟踪的影片集中。 第二行代码将保存对被跟踪回基础数据库的"电影"所做的任何更改。

**图 8 = 添加视图**

![clip_image016](creating-model-classes-with-the-entity-framework-cs/_static/image8.jpg)

#### <a name="updating-database-records-with-the-entity-framework"></a>使用实体框架更新数据库记录

您可以采用几乎相同的方法，使用实体框架编辑数据库记录，就像我们刚才采用的方法插入新的数据库记录一样。 清单4包含两个名为 Edit（） 的新控制器操作。 第一个 Edit（） 操作返回用于编辑影片记录的 HTML 窗体。 第二个 Edit（） 操作尝试更新数据库。

**清单4 = 控制器\主控制器.cs（编辑方法）**

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample6.cs)]

第二个 Edit（） 操作首先从与正在编辑的影片的 ID 匹配的数据库检索影片记录。 以下 LINQ 到实体语句获取与特定 Id 匹配的第一个数据库记录：

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample7.cs)]

接下来，TryUpdateModel（） 方法用于将 HTML 表单字段的值分配给影片实体的属性。 请注意，提供了一个白名单，以指定要更新的确切属性。

接下来，执行一些简单的验证，以验证影片标题和导演属性是否具有值。 如果任一属性缺少值，则验证错误消息将添加到 ModelState 和 ModelState。IsValid 返回该值为 false。

最后，如果没有验证错误，则通过调用 SaveChanges（） 方法，将更新基础"电影"数据库表与任何更改。

编辑数据库记录时，需要将正在编辑的记录的 Id 传递给执行数据库更新的控制器操作。 否则，控制器操作将不知道要在基础数据库中更新哪个记录。 清单 5 中包含的"编辑"视图包含一个隐藏表单字段，该字段表示要编辑的数据库记录的 ID。

**清单5 = 视图\home_编辑.aspx**

[!code-aspx[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample8.aspx)]

## <a name="deleting-database-records-with-the-entity-framework"></a>使用实体框架删除数据库记录

本教程中需要处理的最终数据库操作是删除数据库记录。 您可以使用清单 6 中的控制器操作删除特定的数据库记录。

**清单6 -- [控制器]主控制器.cs（删除操作）**

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample9.cs)]

Delete（） 操作首先检索与传递给该操作的 ID 匹配的 Movie 实体。 接下来，通过调用 DeleteObject（） 方法后跟 SaveChanges（） 方法从数据库中删除影片。 最后，用户被重定向回索引视图。

## <a name="summary"></a>总结

本教程的目的是演示如何利用ASP.NET MVC 和 Microsoft 实体框架构建数据库驱动的 Web 应用程序。 您学习了如何构建一个应用程序，使您能够选择、插入、更新和删除数据库记录。

首先，我们讨论了如何使用实体数据模型向导从 Visual Studio 中生成实体数据模型。 接下来，您将学习如何使用 LINQ 到实体从数据库表中检索一组数据库记录。 最后，我们使用实体框架插入、更新和删除数据库记录。

> [!div class="step-by-step"]
> [下一页](creating-model-classes-with-linq-to-sql-cs.md)

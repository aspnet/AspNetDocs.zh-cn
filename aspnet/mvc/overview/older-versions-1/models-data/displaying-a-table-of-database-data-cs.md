---
uid: mvc/overview/older-versions-1/models-data/displaying-a-table-of-database-data-cs
title: 显示数据库数据表 （C#） |微软文档
author: rick-anderson
description: 在本教程中，我将演示显示一组数据库记录的两种方法。 我在 HTML ta...
ms.author: riande
ms.date: 10/07/2008
ms.assetid: d6e758b6-6571-484d-a132-34ee6c47747a
msc.legacyurl: /mvc/overview/older-versions-1/models-data/displaying-a-table-of-database-data-cs
msc.type: authoredcontent
ms.openlocfilehash: 3fca8ac9e9b4e549ca76ffa282cc03aa4cc50e88
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542049"
---
# <a name="displaying-a-table-of-database-data-c"></a>显示数据库数据表 (C#)

由[微软](https://github.com/microsoft)

[下载 PDF](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_11_CS.pdf)

> 在本教程中，我将演示显示一组数据库记录的两种方法。 我在 HTML 表中显示了两种格式化一组数据库记录的方法。 首先，我将演示如何直接在视图中设置数据库记录的格式。 接下来，我将演示如何在格式化数据库记录时利用部分。

本教程的目的是解释如何在mVC应用程序中显示ASP.NET数据库数据的 HTML 表。 首先，您将了解如何使用 Visual Studio 中包含的基架工具生成自动显示一组记录的视图。 接下来，您将学习如何在格式化数据库记录时使用部分模板。

## <a name="create-the-model-classes"></a>创建模型类

我们将从"电影"数据库表中显示记录集。 "影片"数据库表包含以下列：

<a id="0.3_table01"></a>

| **列名** | **数据类型** | **允许 Null 值** |
| --- | --- | --- |
| ID | Int | False |
| 标题 | 恩瓦尔查尔 （200） | False |
| 导演 | 恩瓦尔查尔 （50） | False |
| 发布日期 | DateTime | False |

为了在ASP.NET MVC 应用程序中表示"电影"表，我们需要创建一个模型类。 在本教程中，我们使用 Microsoft 实体框架创建模型类。

> [!NOTE] 
> 
> 在本教程中，我们使用 Microsoft 实体框架。 但是，请务必了解，您可以使用各种不同的技术与数据库进行交互，从ASP.NET MVC 应用程序（包括 LINQ 到 SQL、NHibernate 或ADO.NET）。

按照以下步骤启动实体数据模型向导：

1. 右键单击"解决方案资源管理器"窗口中的"模型"文件夹，然后选择菜单选项 **"添加、新建项目**"。
2. 选择 **"数据**"类别并选择**ADO.NET实体数据模型**模板。
3. 为数据模型指定名称 *"MoviesDBModel.edmx"，* 然后单击 **"添加**"按钮。

单击"添加"按钮后，将显示实体数据模型向导（参见图 1）。 按照以下步骤完成向导：

1. 在 **"选择模型内容"** 步骤中，选择"**从数据库生成**"选项。
2. 在 **"选择数据连接**"步骤中，使用*MoviesDB.mdf*数据连接和名称 *"电影 DB实体*"来设置连接设置。 单击 **“下一步”** 按钮。
3. 在 **"选择数据库对象**"步骤中，展开"表"节点，选择"影片"表。 输入命名空间*模型*，然后单击 **"完成"** 按钮。

[![将 LINQ 创建到 SQL 类](displaying-a-table-of-database-data-cs/_static/image1.jpg)](displaying-a-table-of-database-data-cs/_static/image1.png)

**图 01**： 创建 LINQ 到 SQL 类 （[单击以查看全尺寸图像](displaying-a-table-of-database-data-cs/_static/image2.png)）

完成实体数据模型向导后，将打开实体数据模型设计器。 设计器应显示影片实体（参见图 2）。

[![实体数据模型设计器](displaying-a-table-of-database-data-cs/_static/image2.jpg)](displaying-a-table-of-database-data-cs/_static/image3.png)

**图 02**： 实体数据模型设计器 （[单击以查看全尺寸图像](displaying-a-table-of-database-data-cs/_static/image4.png)）

在继续之前，我们需要作出一个改变。 实体数据向导生成一个名为 *"电影"* 的模型类，该类表示"影片"数据库表。 由于我们将使用"电影"类来表示特定影片，因此我们需要将类的名称修改为 *"电影*"而不是 *"电影*"（单数而不是复数）。

双击设计器表面上的类的名称，并将类的名称从"影片"更改为"影片"。 进行此更改后，单击 **"保存**"按钮（软盘的图标）以生成 Movie 类。

## <a name="create-the-movies-controller"></a>创建影片控制器

现在，我们有一种方法来表示我们的数据库记录，我们可以创建一个控制器，返回电影的集合。 在可视化工作室解决方案资源管理器窗口中，右键单击"控制器"文件夹并选择菜单选项 **"添加控制器**"（参见图 3）。

[![添加控制器菜单](displaying-a-table-of-database-data-cs/_static/image3.jpg)](displaying-a-table-of-database-data-cs/_static/image5.png)

**图 03**： 添加控制器菜单 （[单击以查看全尺寸图像](displaying-a-table-of-database-data-cs/_static/image6.png)）

出现 **"添加控制器"** 对话框时，输入控制器名称"电影控制器"（参见图 4）。 单击"**添加**"按钮以添加新控制器。

[![添加控制器对话框](displaying-a-table-of-database-data-cs/_static/image4.jpg)](displaying-a-table-of-database-data-cs/_static/image7.png)

**图 04**： 添加控制器对话框（[单击以查看全尺寸图像](displaying-a-table-of-database-data-cs/_static/image8.png)）

我们需要修改由 Movie 控制器公开的 Index（） 操作，以便它返回数据库记录集。 修改控制器，使其看起来像清单 1 中的控制器。

**清单1 = 控制器\电影控制器.cs**

[!code-csharp[Main](displaying-a-table-of-database-data-cs/samples/sample1.cs)]

在清单 1 中，电影 DB 实体类用于表示 MoviesDB 数据库。 要使用此类，您需要导入 MvcApplication1.模型命名空间，如下所示：

使用 Mvc应用程序1.模型;

表达式*实体。MovieSet.ToList（）* 从"影片"数据库表中返回所有影片集。

## <a name="create-the-view"></a>创建视图

在 HTML 表中显示一组数据库记录的最简单方法是利用 Visual Studio 提供的基架。

通过选择菜单选项 **"生成"、"生成解决方案**"来构建应用程序。 在打开 **"添加视图**"对话框之前，必须生成应用程序，否则数据类不会显示在对话框中。

右键单击索引（） 操作并选择菜单选项 **"添加视图**"（参见图 5）。

[![添加视图](displaying-a-table-of-database-data-cs/_static/image5.jpg)](displaying-a-table-of-database-data-cs/_static/image9.png)

**图 05**： 添加视图 （[单击以查看全尺寸图像](displaying-a-table-of-database-data-cs/_static/image10.png)）

在 **"添加视图"** 对话框中，选中标记为"**创建强类型视图"复选框**。 选择"影片"类作为**视图数据类**。 选择 *"列表*"作为**视图内容**（参见图 6）。 选择这些选项将生成显示影片列表的强类型视图。

[!["添加视图"对话框](displaying-a-table-of-database-data-cs/_static/image6.jpg)](displaying-a-table-of-database-data-cs/_static/image11.png)

**图 06**： 添加视图对话框（[单击以查看全尺寸图像](displaying-a-table-of-database-data-cs/_static/image12.png)）

单击"**添加**"按钮后，将自动生成清单 2 中的视图。 此视图包含遍遍遍电影集合并显示影片的每个属性所需的代码。

**清单 2 = 视图\影片_索引.aspx**

[!code-aspx[Main](displaying-a-table-of-database-data-cs/samples/sample2.aspx)]

您可以通过选择菜单选项 **"调试"、"开始调试**"（或点击 F5 键）来运行应用程序。 运行应用程序将启动 Internet 资源管理器。 如果您导航到 /Movie URL，您将看到图 7 中的页面。

[![电影表](displaying-a-table-of-database-data-cs/_static/image7.jpg)](displaying-a-table-of-database-data-cs/_static/image13.png)

**图 07**： 电影表（[单击以查看全尺寸图像](displaying-a-table-of-database-data-cs/_static/image14.png)）

如果您不喜欢图 7 中数据库记录网格的外观，则只需修改 Index 视图即可。 例如，您可以通过修改索引视图将*日期释放*标头更改为*发布日期释放*日期。

## <a name="create-a-template-with-a-partial"></a>创建带有部分的模板

当视图变得过于复杂时，最好开始将视图分解为部分视图。 使用部分使您的视图更易于理解和维护。 我们将创建一个部分，我们可以用作模板来格式化每个影片数据库记录。

按照以下步骤创建部分：

1. 右键单击"视图"+影片文件夹，然后选择菜单选项 **"添加视图**"。
2. 选中标记为"*创建部分视图 （.ascx）"的*复选框。
3. 命名部分*影片模板*。
4. 选中标记为"**创建强类型视图"的**复选框。
5. 选择"影片"作为*视图数据类*。
6. 选择"空"作为*视图内容*。
7. 单击"**添加**"按钮将部分添加到项目中。

完成这些步骤后，将"电影模板"部分修改为类似于清单 3。

**清单3 = 视图\电影_电影模板.ascx**

[!code-aspx[Main](displaying-a-table-of-database-data-cs/samples/sample3.aspx)]

清单3中的部分包含一行记录的模板。

清单4中修改后的索引视图使用影片模板部分。

**清单4 = 视图\影片_索引.aspx**

[!code-aspx[Main](displaying-a-table-of-database-data-cs/samples/sample4.aspx)]

清单 4 中的视图包含一个循环，该循环遍历所有影片。 对于每个影片，影片模板部分用于格式化影片。 通过调用 Render 部分（） 帮助器方法来呈现影片模板。

修改后的 Index 视图呈现的数据库记录的 HTML 表与同一个表。 但是，视图已大大简化。

Render部分（） 方法不同于大多数其他帮助器方法，因为它不返回字符串。 因此，必须使用&lt;% Html.render 部分（）;%&gt;而不是&lt;%= Html.render 部分（）;%&gt;.

## <a name="summary"></a>总结

本教程的目的是解释如何在 HTML 表中显示一组数据库记录。 首先，您学习了如何通过利用 Microsoft 实体框架从控制器操作返回一组数据库记录。 接下来，您学习了如何使用 Visual Studio 基架生成自动显示项目集合的视图。 最后，您学习了如何通过利用部分视图来简化视图。 您学习了如何使用部分作为模板，以便可以格式化每个数据库记录。

> [!div class="step-by-step"]
> [上一页](creating-model-classes-with-linq-to-sql-cs.md)
> [下一页](performing-simple-validation-cs.md)

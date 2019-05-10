---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part4
title: 创建数据库 |Microsoft Docs
author: shanselman
description: 这是介绍 ASP.NET MVC 的基础知识初学者教程。 创建一个简单的 web 应用程序读取和写入数据库中。
ms.author: riande
ms.date: 08/14/2010
ms.assetid: 742df67f-484d-4ef3-af6b-8c791e556b43
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part4
msc.type: authoredcontent
ms.openlocfilehash: 995db714ce6365415d06dc458aee84a31c7c8fd6
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/06/2019
ms.locfileid: "65117676"
---
# <a name="creating-a-database"></a>创建数据库

通过[Scott Hanselman](https://github.com/shanselman)

> 这是介绍 ASP.NET MVC 的基础知识初学者教程。 将创建一个简单的 web 应用程序读取和写入数据库中。 请访问[ASP.NET MVC 学习中心](../../../index.md)来查找其他 ASP.NET MVC 教程和示例。

在本部分中我们要创建新 SQL Express 数据库，我们将使用它来存储和检索电影数据。 从 Visual Web 开发人员 IDE 中，选择视图 |服务器资源管理器。 右键单击数据连接，然后单击添加连接...

![AddConnection](getting-started-with-mvc-part4/_static/image1.png)

在选择数据源对话框中，选择 Microsoft SQL Server 并选择继续。

![](getting-started-with-mvc-part4/_static/image2.png)

在添加连接对话框中，输入"。 \SQLEXPRESS"服务器名称，并输入"电影"作为新数据库的名称。

[![添加连接对话框](getting-started-with-mvc-part4/_static/image4.png)](getting-started-with-mvc-part4/_static/image3.png)

单击确定，并将你想要创建该数据库要求你。 选择是。

[![创建电影？](getting-started-with-mvc-part4/_static/image6.png)](getting-started-with-mvc-part4/_static/image5.png)

现在你已在服务器资源管理器中生成一个空数据库。

![添加新表](getting-started-with-mvc-part4/_static/image7.png)

右键单击表，然后单击添加表。 表设计器将显示。 添加 Id、 标题、 ReleaseDate、 Genre 和价格列。 右键单击 ID 列，然后单击设置 Primary Key。 下面是哪些我设计方面的问题如下所示。

[![数据库表编辑器](getting-started-with-mvc-part4/_static/image9.png)](getting-started-with-mvc-part4/_static/image8.png)

此外，选择 Id 列，并在下面的列属性下更改"标识规范"为"是"。

[![IsIdentity-列属性](getting-started-with-mvc-part4/_static/image11.png)](getting-started-with-mvc-part4/_static/image10.png)

获得其完成后，单击工具栏中的保存图标，或选择文件 |从菜单中，保存并命名为您的表"**电影**"（单数）。 我们有一个数据库和表 ！

[![选择名称](getting-started-with-mvc-part4/_static/image13.png)](getting-started-with-mvc-part4/_static/image12.png)

返回到服务器资源管理器和右键单击的 Movie 表，然后选择"显示表数据"。 输入几个电影，以便我们的数据库有一些数据。

[![数据库表格编辑](getting-started-with-mvc-part4/_static/image15.png)](getting-started-with-mvc-part4/_static/image14.png)

## <a name="creating-a-model"></a>创建模型

现在，切换回 IDE 右侧的解决方案资源管理器和右键单击模型文件夹并选择添加 |新项。

[![addnewmodelitem](getting-started-with-mvc-part4/_static/image17.png)](getting-started-with-mvc-part4/_static/image16.png)

我们将我们新的数据库中创建实体模型。 这会将一组类添加到我们的项目，以便轻松我们来查询和操作数据库中的数据。 选择对话框中，左侧的数据节点，然后选择 ADO.NET 实体数据模型项模板。 将其命名 Movies.edmx。

[![AddNewDataModel](getting-started-with-mvc-part4/_static/image19.png)](getting-started-with-mvc-part4/_static/image18.png)

单击"添加"按钮。 然后，这将启动"实体数据模型向导"。

在新弹出的对话框，从数据库中选择生成。 由于我们进行了数据库，我们只需要告诉我们新的数据库和其表的实体框架。 单击保存在我们的 web 应用程序的配置数据库连接下一步。 现在，检查表和电影复选框，并单击完成。

[![实体数据模型向导](getting-started-with-mvc-part4/_static/image21.png)](getting-started-with-mvc-part4/_static/image20.png)

现在，我们可以看到我们新的 Movie 表中实体框架设计器，并从代码访问它。

[![电影-Microsoft Visual Web Developer 2010 速成版](getting-started-with-mvc-part4/_static/image23.png)](getting-started-with-mvc-part4/_static/image22.png)

在设计图面上可以看到"Movie"类。 此类映射到在数据库中，"电影"表并在其中每个属性将映射到具有表的列。 "电影"类的每个实例将对应于"Movie"表中的行。

如果您不喜欢默认命名和映射实体框架使用的约定，可以使用实体框架设计器更改或自定义它们。 为此应用程序中，我们将使用默认值并只需将该文件作为-是。

现在，让我们使用一些真实数据 ！

> [!div class="step-by-step"]
> [上一页](getting-started-with-mvc-part3.md)
> [下一页](getting-started-with-mvc-part5.md)

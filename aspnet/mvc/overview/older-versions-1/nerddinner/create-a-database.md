---
uid: mvc/overview/older-versions-1/nerddinner/create-a-database
title: 创建数据库 | Microsoft Docs
author: rick-anderson
description: 步骤 2 显示了创建数据库的步骤，这些数据库包含我们 NerdDinner 应用程序的所有晚餐和 RSVP 数据。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 983f3ffa-08b8-4868-b8c9-aa34593fc683
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/create-a-database
msc.type: authoredcontent
ms.openlocfilehash: d0b87e4a6a27b37d2dbaa6d5b871da477b25586d
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541606"
---
# <a name="create-a-database"></a>创建数据库

由[微软](https://github.com/microsoft)

[下载 PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 这是一个免费的["NerdDinner"应用程序教程](introducing-the-nerddinner-tutorial.md)的第2步，它介绍了如何使用 ASP.NETmVC 1构建小型但完整的Web应用程序。
> 
> 步骤 2 显示了创建数据库的步骤，这些数据库包含我们 NerdDinner 应用程序的所有晚餐和 RSVP 数据。
> 
> 如果您使用的是ASP.NET MVC 3，我们建议您按照[MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC 音乐商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程进行操作。

## <a name="nerddinner-step-2-creating-the-database"></a>神经晚餐步骤 2：创建数据库

我们将使用数据库来存储我们 NerdDinner 应用程序的所有晚餐和 RSVP 数据。

以下步骤显示了使用免费 SQL Server Express 版本创建数据库（您可以使用[Microsoft Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)的 V2 轻松安装）。 我们将编写的所有代码都适用于 SQL Server Express 和完整 SQL Server。

### <a name="creating-a-new-sql-server-express-database"></a>创建新的 SQL Server Express 数据库

我们将从右键单击 Web 项目开始，然后选择 **"添加新&gt;项目"** 菜单命令：

![](create-a-database/_static/image1.png)

这将弹出可视化工作室的"添加新项目"对话框。 我们将按"数据"类别进行筛选，然后选择"SQL 服务器数据库"项模板：

![](create-a-database/_static/image2.png)

我们将命名要创建的 SQL Server Express 数据库"NerdDinner.mdf"，然后点击确定。 然后，Visual Studio 会询问我们是否要将此文件添加到我们的 @App\_数据目录（该目录已设置包含读取和写入安全 ACL）：

![](create-a-database/_static/image3.png)

我们将单击"是"，我们将创建新数据库并将其添加到解决方案资源管理器中：

![](create-a-database/_static/image4.png)

### <a name="creating-tables-within-our-database"></a>在我们的数据库中创建表

我们现在有一个新的空数据库。 让我们向它添加一些表。

为此，我们将导航到 Visual Studio 中的"服务器资源管理器"选项卡窗口，这使我们能够管理数据库和服务器。 存储在应用程序的 @App\_数据文件夹中的 SQL Server Express 数据库将自动显示在服务器资源管理器中。 我们可以选择使用"服务器资源管理器"窗口顶部的"连接到数据库"图标，将其他 SQL Server 数据库（本地数据库和远程数据库）添加到列表中：

![](create-a-database/_static/image5.png)

我们将向 NerdDinner 数据库添加两个表 - 一个用于存储我们的晚餐，另一个用于跟踪 RSVP 接受的接收。 我们可以通过右键单击数据库中的"表"文件夹并选择"添加新表"菜单命令来创建新表：

![](create-a-database/_static/image6.png)

这将打开一个表设计器，允许我们配置表的架构。 对于我们的"Dinners"表，我们将添加 10 列数据：

![](create-a-database/_static/image7.png)

我们希望"DinnerID"列是表的唯一主键。 我们可以通过右键单击"DinnerID"列并选择"设置主键"菜单项来配置此项：

![](create-a-database/_static/image8.png)

除了使 DinnerID 成为主键外，我们还希望将其配置为"标识"列，该列的值随着新数据行添加到表中而自动递增（这意味着第一个插入的 Dinner 行的 DinnerID 为 1，第二个插入的行的 DinnerID 为 2，等等）。

为此，我们可以选择"DinnerID"列，然后使用"列属性"编辑器将列上的"（即标识）"属性设置为"是"。 我们将使用标准标识默认值（从 1 开始，在每个新的 Dinner 行上增加 1）：

![](create-a-database/_static/image9.png)

然后，我们将通过键入 Ctrl-S 或使用 **"文件保存"&gt;** 菜单命令来保存我们的表。 这将提示我们命名表。 我们将将其命名为"晚餐"：

![](create-a-database/_static/image10.png)

然后，我们新的 Dinners 表将显示到服务器资源管理器中的数据库中。

然后，我们将重复上述步骤，并创建一个"RSVP"表。 此表包含 3 列。 我们将将 RsvpID 列设置为主键，并使其成为标识列：

![](create-a-database/_static/image11.png)

我们将保存它，并给它的名字"RSVP"。

### <a name="setting-up-a-foreign-key-relationship-between-tables"></a>设置表之间的外键关系

现在，我们的数据库中有两个表。 我们最后一个架构设计步骤是在这两个表之间建立"一对多"关系，以便我们可以将每个 Dinner 行与应用于它的零个或多个 RSVP 行相关联。 为此，我们将配置 RSVP 表的"DinnerID"列，以便与"Dinners"表中的"DinnerID"列具有外键关系。

为此，我们将在服务器资源管理器中双击表设计器中打开 RSVP 表。 然后，我们将选择其中的"DinnerID"列，右键单击，然后选择"关系..."上下文菜单命令：

![](create-a-database/_static/image12.png)

这将弹出一个对话框，我们可以用它来设置表之间的关系：

![](create-a-database/_static/image13.png)

我们将单击"添加"按钮以向对话框添加新关系。 添加关系后，我们将将属性网格中的"表和列规范"树视图节点扩展到对话框的右侧，然后单击"..."按钮右侧：

![](create-a-database/_static/image14.png)

单击"..."按钮将弹出另一个对话框，允许我们指定关系中涉及哪些表和列，并允许我们命名关系。

我们将主键表更改为"Dinners"，并选择"晚餐"表中的"DinnerID"列作为主键。 我们的 RSVP 表将是外键表和 RSVP。DinnerID 列将作为外键关联：

![](create-a-database/_static/image15.png)

现在，RSVP 表中的每一行都将与"晚餐"表中的一行相关联。 SQL Server 将为我们保持参考完整性 ， 并且阻止我们添加新的 RSVP 行，如果它不指向有效的 Dinner 行。 如果仍有 RSVP 行引用它，它也会阻止我们删除 Dinner 行。

### <a name="adding-data-to-our-tables"></a>将数据添加到我们的表

最后，让我们向"晚餐"表添加一些示例数据。 我们可以在服务器资源管理器中右键单击数据并选择"显示表数据"命令，将数据添加到表中：

![](create-a-database/_static/image16.png)

我们将添加几行 Dinner 数据，稍后在开始实现应用程序时可以使用这些数据：

![](create-a-database/_static/image17.png)

### <a name="next-step"></a>下一步

我们已经完成了数据库的创建。 现在，让我们创建模型类，可用于查询和更新它。

> [!div class="step-by-step"]
> [上一页](create-a-new-aspnet-mvc-project.md)
> [下一页](build-a-model-with-business-rule-validations.md)

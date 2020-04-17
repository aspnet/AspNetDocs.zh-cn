---
uid: mvc/overview/older-versions-1/contact-manager/iteration-1-create-the-application-cs
title: 迭代#1 = 创建应用程序 （C#） |微软文档
author: rick-anderson
description: 在第一次迭代中，我们以最简单的方式创建联系人管理器。 我们增加了对基本数据库操作的支持：创建、读取、更新和 D...
ms.author: riande
ms.date: 02/20/2009
ms.assetid: db0f160b-901c-46d3-865e-7ab6cd4ed68d
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-1-create-the-application-cs
msc.type: authoredcontent
ms.openlocfilehash: ecc3c1201c784e20c6b2601735bee3d4ce721f22
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542542"
---
# <a name="iteration-1--create-the-application-c"></a>迭代 1 – 创建应用程序 (C#)

由[微软](https://github.com/microsoft)

[下载代码](iteration-1-create-the-application-cs/_static/contactmanager_1_cs1.zip)

> 在第一次迭代中，我们以最简单的方式创建联系人管理器。 我们添加对基本数据库操作的支持：创建、读取、更新和删除 （CRUD）。

## <a name="building-a-contact-management-aspnet-mvc-application-vb"></a>构建 MVC 应用程序 （VB） ASP.NET联系人管理

在本系列教程中，我们从头到尾构建整个联系人管理应用程序。 通过联系人管理器应用程序，您可以存储联系人信息 （姓名、电话号码和电子邮件地址） 人员列表。

我们通过多次迭代构建应用程序。 每次迭代时，我们都会逐步改进应用程序。 此多迭代方法的目标是使您能够了解每次更改的原因。

- 迭代#1 - 创建应用程序。 在第一次迭代中，我们以最简单的方式创建联系人管理器。 我们添加对基本数据库操作的支持：创建、读取、更新和删除 （CRUD）。

- 迭代#2 - 使应用程序看起来不错。 在此迭代中，我们通过修改默认ASP.NET MVC 视图母版页和级联样式表来改进应用程序的外观。

- 迭代#3 - 添加表单验证。 在第三个迭代中，我们添加基本表单验证。 我们防止人们在未填写所需表单字段的情况下提交表单。 我们还验证电子邮件地址和电话号码。

- 迭代#4 - 使应用程序松散耦合。 在第四次迭代中，我们利用多种软件设计模式，使维护和修改联系人管理器应用程序变得更加容易。 例如，我们重构应用程序以使用存储库模式和依赖项注入模式。

- 迭代#5 - 创建单元测试。 在第五次迭代中，我们通过添加单元测试使应用程序更易于维护和修改。 我们模拟数据模型类，并为控制器和验证逻辑构建单元测试。

- 迭代#6 - 使用测试驱动开发。 在第六次迭代中，我们首先编写单元测试并针对单元测试编写代码，从而向应用程序添加新功能。 在此迭代中，我们添加联系人组。

- 迭代#7 - 添加Ajax功能。 在第七次迭代中，我们通过增加对Ajax的支持来提高应用程序的响应性和性能。

## <a name="this-iteration"></a>此迭代

在第一次迭代中，我们将构建基本应用程序。 目标是以最快、最简单的方式构建联系人管理器。 在以后的迭代中，我们改进了应用程序的设计。

联系人管理器应用程序是一个基本的数据库驱动应用程序。 您可以使用该应用程序创建新联系人、编辑现有联系人和删除联系人。

在此迭代中，我们完成以下步骤：

1. ASP.NET MVC 应用程序
2. 创建数据库以存储我们的联系人
3. 使用 Microsoft 实体框架为我们的数据库生成模型类
4. 创建控制器操作和视图，使我们能够列出数据库中的所有联系人
5. 创建控制器操作和视图，使我们能够在数据库中创建新联系人
6. 创建控制器操作和视图，使我们能够编辑数据库中的现有联系人
7. 创建控制器操作和视图，使我们能够删除数据库中的现有联系人

## <a name="software-prerequisites"></a>必备软件

在ASP.NET MVC 应用程序中，必须在您的计算机上安装 Visual Studio 2008 或 Visual Web 开发人员 2008（可视化 Web 开发人员是 Visual Studio 的免费版本，不包含 Visual Studio 的所有高级功能）。 您可以通过以下地址下载 Visual Studio 2008 试用版或可视化 Web 开发人员版本：

[https://www.asp.net/downloads/essential/](https://www.asp.net/downloads/essential)

> [!NOTE] 
> 
> 对于具有可视化 Web 开发人员ASP.NET MVC 应用程序，必须安装可视化 Web 开发人员服务包 1。 如果没有服务包 1，则无法创建 Web 应用程序项目。

ASP.NET MVC 框架。 可以从以下地址下载ASP.NET MVC 框架：

[https://www.asp.net/mvc](../../../index.md)

在本教程中，我们使用 Microsoft 实体框架访问数据库。 实体框架包含在 .NET 框架 3.5 服务包 1 中。 您可以通过以下位置下载此服务包：

[https://www.microsoft.com/downloads/details.aspx?familyid=ab99342f-5d1a-413d-8319-81da479ab0d7&amp;d斯普拉朗](https://www.microsoft.com/downloads/details.aspx?familyid=ab99342f-5d1a-413d-8319-81da479ab0d7&amp;displaylang=en)

作为逐个执行每个下载的替代方法，您可以利用 Web 平台安装程序 （Web PI）。 您可以通过以下地址下载 Web PI：

[https://www.asp.net/downloads/essential/](https://www.asp.net/downloads/essential)

## <a name="aspnet-mvc-project"></a>ASP.NET MVC 项目

ASP.NET MVC Web 应用程序项目。 启动可视化工作室并选择菜单选项**文件，新项目**。 将显示 **"新项目"** 对话框（参见图 1）。 选择**Web**项目类型和**ASP.NET MVC Web 应用程序**模板。 说出您的新项目*联系人管理器*，然后单击"确定"按钮。

请确保从 **"新项目"** 对话框右上角的下拉列表中选择了 .NET Framework 3.5。 否则，将不会显示ASP.NET MVC Web 应用程序模板。

[![“新建项目”对话框](iteration-1-create-the-application-cs/_static/image1.jpg)](iteration-1-create-the-application-cs/_static/image1.png)

**图 01**： 新项目对话框（[单击以查看全尺寸图像](iteration-1-create-the-application-cs/_static/image2.png)）

ASP.NET MVC 应用程序，将显示 **"创建单元测试项目**"对话框。 可以使用此对话框指示在创建ASP.NET MVC 应用程序时要创建单元测试项目并将其添加到解决方案中。 尽管我们在此迭代中不会构建单元测试，但应选择选项 **"是"，创建单元测试项目**，因为我们计划在以后的迭代中添加单元测试。 首次创建新的ASP.NET MVC 项目时添加测试项目比创建ASP.NET MVC 项目后添加测试项目要容易得多。

> [!NOTE] 
> 
> 由于可视化 Web 开发人员不支持测试项目，因此在使用可视化 Web 开发人员时，您不会获取"创建单元测试项目"对话框。

[![“新建项目”对话框](iteration-1-create-the-application-cs/_static/image2.jpg)](iteration-1-create-the-application-cs/_static/image3.png)

**图 02**： 创建单元测试项目对话框 （[单击以查看全尺寸图像](iteration-1-create-the-application-cs/_static/image4.png)）

ASP.NET MVC 应用程序显示在可视化工作室解决方案资源管理器窗口中（参见图 3）。 如果看不到"解决方案资源管理器"窗口，则可以通过选择菜单选项 **"视图"、"解决方案资源管理器**"来打开此窗口。 请注意，该解决方案包含两个项目：ASP.NET MVC 项目和测试项目。 mVCASP.NET项目命名为"联系人管理器"，测试项目命名为"联系人管理器"。

[![“新建项目”对话框](iteration-1-create-the-application-cs/_static/image3.jpg)](iteration-1-create-the-application-cs/_static/image5.png)

**图 03**： 解决方案资源管理器窗口 （[单击以查看全尺寸图像](iteration-1-create-the-application-cs/_static/image6.png)）

## <a name="deleting-the-project-sample-files"></a>删除项目示例文件

ASP.NET MVC 项目模板包括控制器和视图的示例文件。 在创建新ASP.NET MVC 应用程序之前，应删除这些文件。 您可以通过右键单击文件或文件夹并选择菜单选项 **"删除**"来删除解决方案资源管理器窗口中的文件和文件夹。

您需要从 ASP.NET MVC 项目中删除以下文件：

- [控制器]主控制器.cs

- [视图]主页\关于.aspx

- [视图]主页\索引.aspx

而且，您需要从测试项目中删除以下文件：

[控制器]主控制器测试.cs

## <a name="creating-the-database"></a>创建数据库

联系人管理器应用程序是数据库驱动的 Web 应用程序。 我们使用数据库来存储联系信息。

ASP.NET MVC 框架，包含任何现代数据库，包括 Microsoft SQL Server、Oracle、MySQL 和 IBM DB2 数据库。 在本教程中，我们使用 Microsoft SQL Server 数据库。 安装 Visual Studio 时，系统会提供安装 Microsoft SQL Server Express 的选项，这是 Microsoft SQL Server 数据库的免费版本。

通过右键单击解决方案资源管理器窗口中的应用\_数据文件夹并选择菜单选项 **"添加、新项目**"来创建新数据库。 在 **"添加新项目"** 对话框中，选择 **"数据**"类别和**SQL Server 数据库**模板（参见图 4）。 命名新数据库 ContactManagerDB.mdf，然后单击"确定"按钮。

[![“新建项目”对话框](iteration-1-create-the-application-cs/_static/image4.jpg)](iteration-1-create-the-application-cs/_static/image7.png)

**图04**：创建新的微软 SQL Server Express 数据库 （[单击以查看全尺寸图像](iteration-1-create-the-application-cs/_static/image8.png)）

创建新数据库后，数据库将显示在解决方案资源管理器窗口中的应用\_数据文件夹中。 双击 ContactManager.mdf 文件以打开服务器资源管理器窗口并连接到数据库。

> [!NOTE] 
> 
> 服务器资源管理器窗口称为数据库资源管理器窗口（对于 Microsoft 可视化 Web 开发人员）。

可以使用 Server 资源管理器窗口创建新的数据库对象，如数据库表、视图、触发器和存储过程。 右键单击"表"文件夹并选择菜单选项 **"添加新表**"。 将显示数据库表设计器（参见图 5）。

[![“新建项目”对话框](iteration-1-create-the-application-cs/_static/image5.jpg)](iteration-1-create-the-application-cs/_static/image9.png)

**图 05**： 数据库表设计器 （[单击以查看全尺寸图像](iteration-1-create-the-application-cs/_static/image10.png)）

我们需要创建一个包含以下列的表：

<a id="0.1_table01"></a>

| **列名** | **数据类型** | **允许 Null 值** |
| --- | --- | --- |
| ID | int | false |
| FirstName | nvarchar(50) | false |
| LastName | nvarchar(50) | false |
| 电话 | nvarchar(50) | false |
| 电子邮件 | nvarchar(255) | false |

第一列"Id"列是特殊的。 您需要将 Id 列标记为标识列和主键列。 通过展开列属性（查看图 6 的底部）向下滚动到标识规范属性，指示列是标识列。 将 **（是标识）** 属性设置为值**是**。

通过选择列并单击带有键图标的按钮，将列标记为主键列。 将列标记为主键列后，列旁边将显示一个键图标（参见图 6）。

完成表创建后，单击"保存"按钮（带有软盘图标的按钮）以保存新表。 为您的新表命名 *"联系人*"。

完成创建"联系人"数据库表后，应向该表添加一些记录。 右键单击服务器资源管理器窗口中的"联系人"表，然后选择菜单选项 **"显示表数据**"。 在显示的网格中输入一个或多个联系人。

## <a name="creating-the-data-model"></a>创建数据模型

ASP.NET MVC 应用程序由模型、视图和控制器组成。 我们首先创建一个模型类，该类表示我们在上一节中创建的"联系人"表。

在本教程中，我们使用 Microsoft 实体框架从数据库自动生成模型类。

> [!NOTE] 
> 
> ASP.NET MVC 框架不以任何方式绑定到 Microsoft 实体框架。 您可以将mVCASP.NET替代数据库访问技术（包括 NHibernate、LINQ 到 SQL 或ADO.NET） 使用。

按照以下步骤创建数据模型类：

1. 右键单击"解决方案资源管理器"窗口中的"模型"文件夹，然后选择"**添加新项目**"。 将显示 **"添加新项目"** 对话框（参见图 6）。
2. 选择 **"数据**"类别和**ADO.NET实体数据模型**模板。 命名数据模型*ContactManagerModel.edmx，* 然后单击 **"添加**"按钮。 将显示实体数据模型向导（参见图 7）。
3. 在 **"选择模型内容"** 步骤中，选择**从数据库中生成**（参见图 7）。
4. 在 **"选择数据连接**"步骤中，选择 ContactManagerDB.mdf 数据库，并输入实体连接设置的名称 *"联系人管理器数据库实体*"（参见图 8）。
5. 在 **"选择数据库对象**"步骤中，选择标记为表的复选框（参见图 9）。 数据模型将包括数据库中包含的所有表（只有一个，"联系人"表）。 输入命名空间*模型*。 单击"完成"按钮以完成向导。

[![“新建项目”对话框](iteration-1-create-the-application-cs/_static/image6.jpg)](iteration-1-create-the-application-cs/_static/image11.png)

**图 06**： 添加新项目对话框 （[单击以查看全尺寸图像](iteration-1-create-the-application-cs/_static/image12.png)）

[![“新建项目”对话框](iteration-1-create-the-application-cs/_static/image7.jpg)](iteration-1-create-the-application-cs/_static/image13.png)

**图 07**： 选择模型内容 （[单击以查看全尺寸图像](iteration-1-create-the-application-cs/_static/image14.png)）

[![“新建项目”对话框](iteration-1-create-the-application-cs/_static/image8.jpg)](iteration-1-create-the-application-cs/_static/image15.png)

**图 08**： 选择您的数据连接 （[单击以查看全尺寸图像](iteration-1-create-the-application-cs/_static/image16.png)）

[![“新建项目”对话框](iteration-1-create-the-application-cs/_static/image9.jpg)](iteration-1-create-the-application-cs/_static/image17.png)

**图 09**： 选择数据库对象 （[单击以查看全尺寸图像](iteration-1-create-the-application-cs/_static/image18.png)）

完成实体数据模型向导后，将显示实体数据模型设计器。 设计器显示与要建模的每个表对应的类。 您应该会看到一个名为"联系人"的类。

实体数据模型向导基于数据库表名称生成类名称。 您几乎总是需要更改向导生成的类的名称。 右键单击设计器中的"联系人"类，然后选择菜单选项 **"重命名**"。 将类的名称从"联系人"（复数）更改为"联系人"（单数）。 更改类名称后，类应如下所示 10。

[![“新建项目”对话框](iteration-1-create-the-application-cs/_static/image10.jpg)](iteration-1-create-the-application-cs/_static/image19.png)

**图10**： 联系人类 （[单击以查看全尺寸图像](iteration-1-create-the-application-cs/_static/image20.png)）

此时，我们创建了数据库模型。 我们可以使用 Contact 类来表示数据库中的特定联系人记录。

## <a name="creating-the-home-controller"></a>创建主控制器

下一步是创建我们的主控制器。 主控制器是在 mVC 应用程序中调用的默认控制器ASP.NET。

通过右键单击解决方案资源管理器窗口中的控制器文件夹并选择菜单选项 **"添加，控制器**"（参见图 11），创建主控制器类。 请注意，标记为"**添加创建、更新和详细信息方案"操作方法的**复选框。 在单击"**添加**"按钮之前，请确保选中此复选框。

[![“新建项目”对话框](iteration-1-create-the-application-cs/_static/image11.jpg)](iteration-1-create-the-application-cs/_static/image21.png)

**图11**： 添加主控制器 （[单击以查看全尺寸图像](iteration-1-create-the-application-cs/_static/image22.png)）

创建主控制器时，您将获得清单 1 中的类。

**清单1 - 控制器\主控制器.cs**

[!code-csharp[Main](iteration-1-create-the-application-cs/samples/sample1.cs)]

## <a name="listing-the-contacts"></a>列出联系人

为了在"联系人"数据库表中显示记录，我们需要创建一个索引（） 操作和索引视图。

主控制器已包含索引（） 操作。 我们需要修改此方法，以便它看起来像清单 2。

**清单2 - 控制器\主控制器.cs**

[!code-csharp[Main](iteration-1-create-the-application-cs/samples/sample2.cs)]

请注意，清单 2 中的主控制器类包含名为\_实体的专用字段。 实体\_字段表示数据模型中的实体。 我们使用\_实体字段与数据库通信。

Index（） 方法返回表示联系人数据库表中的所有联系人的视图。 表达式\_实体。联系人集.ToList（） 将联系人列表作为通用列表返回。

现在，我们已经创建了索引控制器，接下来我们需要创建索引视图。 在创建索引视图之前，请通过选择菜单选项 **"生成、生成解决方案**"来编译应用程序。 在添加视图之前，应始终编译项目，以便在 **"添加视图**"对话框中显示模型类列表。

通过右键单击 Index（） 方法并选择菜单选项 **"添加视图**"来创建索引视图（请参见图 12）。 选择此菜单选项将打开 **"添加视图"** 对话框（参见图 13）。

[![“新建项目”对话框](iteration-1-create-the-application-cs/_static/image12.jpg)](iteration-1-create-the-application-cs/_static/image23.png)

**图 12**： 添加索引视图 （[单击以查看全尺寸图像](iteration-1-create-the-application-cs/_static/image24.png)）

在 **"添加视图"** 对话框中，选中标记为"**创建强类型视图"复选框**。 选择"查看数据类联系人管理器.模型.联系人"和"查看内容列表"。 选择这些选项将生成显示联系人记录列表的视图。

[![“新建项目”对话框](iteration-1-create-the-application-cs/_static/image13.jpg)](iteration-1-create-the-application-cs/_static/image25.png)

**图 13**： 添加视图对话框 （[单击以查看全尺寸图像](iteration-1-create-the-application-cs/_static/image26.png)）

单击"**添加**"按钮时，将生成清单 3 中的索引视图。 请注意&lt;显示在文件顶部的&gt;%@ 页 % 指令。 &lt;索引视图从 ViewPage IE500"&lt;联系人管理器.模型.联系人&gt;&gt;类继承。 换句话说，视图中的 Model 类表示联系人实体的列表。

Index 视图的正文包含一个 foreach 循环，该循环通过模型类表示的每个联系人进行循环。 Contact 类的每个属性的值显示在 HTML 表中。

**清单 3 - 视图\home_Index.aspx（未修改）**

[!code-aspx[Main](iteration-1-create-the-application-cs/samples/sample3.aspx)]

我们需要对索引视图进行一次修改。 由于我们不是在创建"详细信息"视图，因此我们可以删除"详细信息"链接。 从索引视图查找和删除以下代码：

{ id}项。ID =）%&gt;

修改索引视图后，可以运行联系人管理器应用程序。 选择菜单选项"调试"、"开始调试"或"按 F5"。 首次运行应用程序时，您将获得图 14 中的对话框。 选择 **"修改 Web.config 文件以启用调试**"选项，然后单击"确定"按钮。

[![“新建项目”对话框](iteration-1-create-the-application-cs/_static/image14.jpg)](iteration-1-create-the-application-cs/_static/image27.png)

**图14**：启用调试 （[单击以查看全尺寸图像](iteration-1-create-the-application-cs/_static/image28.png)）

默认情况下，将返回索引视图。 此视图列出联系人数据库表中的所有数据（参见图 15）。

[![“新建项目”对话框](iteration-1-create-the-application-cs/_static/image15.jpg)](iteration-1-create-the-application-cs/_static/image29.png)

**图 15**： 索引视图 （[单击以查看全尺寸图像](iteration-1-create-the-application-cs/_static/image30.png)）

请注意，索引视图在视图底部包含标记为"新建"的链接。 在下一节中，您将了解如何创建新联系人。

## <a name="creating-new-contacts"></a>创建新联系人

为了使用户能够创建新的联系人，我们需要向主控制器添加两个 Create（） 操作。 我们需要创建一个 Create（） 操作，该操作返回 HTML 表单以创建新联系人。 我们需要创建第二个 Create（） 操作，以执行新联系人的实际数据库插入。

我们需要添加到主控制器的新 Create（） 方法包含在清单 4 中。

**清单4 - 控制器\主控制器.cs（使用创建方法）**

[!code-csharp[Main](iteration-1-create-the-application-cs/samples/sample4.cs)]

第一个 Create（） 方法可以使用 HTTP GET 调用，而第二个 Create（） 方法只能由 HTTP POST 调用。 换句话说，第二个 Create（） 方法只能在发布 HTML 窗体时调用。 第一个 Create（） 方法仅返回包含用于创建新联系人的 HTML 窗体的视图。 第二个 Create（） 方法更有趣：它将新的联系人添加到数据库中。

请注意，已修改第二个 Create（） 方法以接受 Contact 类的实例。 从 HTML 窗体发布的表单值由 ASP.NET MVC 框架自动绑定到此 Contact 类。 HTML 创建窗体中的每个窗体字段都分配给"联系人"参数的属性。

请注意，联系人参数用 [Bind] 属性进行修饰。 [绑定] 属性用于从绑定中排除联系人 Id 属性。 由于 Id 属性表示标识属性，因此我们不希望设置 Id 属性。

在 Create（） 方法的正文中，实体框架用于将新的联系人插入到数据库中。 新的联系人将添加到现有的联系人集，并调用 SaveChanges（） 方法将这些更改推送回基础数据库。

您可以通过右键单击两个 Create（） 方法之一并选择菜单选项 **"添加视图**"来生成用于创建新联系人的 HTML 表单（参见图 16）。

[![“新建项目”对话框](iteration-1-create-the-application-cs/_static/image16.jpg)](iteration-1-create-the-application-cs/_static/image31.png)

**图 16**： 添加创建视图 （[单击以查看全尺寸图像](iteration-1-create-the-application-cs/_static/image32.png)）

在 **"添加视图"** 对话框中，选择 **"联系人管理器.模型.联系人类"** 和"**创建**视图内容"选项（参见图 17）。 单击"**添加**"按钮时，将自动生成"创建"视图。

[![“新建项目”对话框](iteration-1-create-the-application-cs/_static/image17.jpg)](iteration-1-create-the-application-cs/_static/image33.png)

**图17**： 看到页面爆炸 （[单击以查看全尺寸图像](iteration-1-create-the-application-cs/_static/image34.png)）

"创建"视图包含 Contact 类的每个属性的表单字段。 "创建"视图的代码包含在清单 5 中。

**清单 5 - 视图\home_Create.aspx**

[!code-aspx[Main](iteration-1-create-the-application-cs/samples/sample5.aspx)]

修改 Create（） 方法并添加"创建"视图后，可以运行联系人经理应用程序并创建新联系人。 单击"**新建**"视图中显示的链接以导航到"创建"视图。 您应该在图 18 中看到视图。

[![“新建项目”对话框](iteration-1-create-the-application-cs/_static/image18.jpg)](iteration-1-create-the-application-cs/_static/image35.png)

**图 18**： 创建视图 （[单击以查看全尺寸图像](iteration-1-create-the-application-cs/_static/image36.png)）

## <a name="editing-contacts"></a>编辑联系人

添加用于编辑联系人记录的功能与添加创建新联系人记录的功能非常相似。 首先，我们需要向主控制器类添加两种新的 Edit 方法。 这些新的 Edit（） 方法包含在清单 6 中。

**清单6 - 控制器\主控制器.cs（使用编辑方法）**

[!code-csharp[Main](iteration-1-create-the-application-cs/samples/sample6.cs)]

第一个 Edit（） 方法由 HTTP GET 操作调用。 Id 参数传递给此方法，此方法表示要编辑的联系人记录的 ID。 实体框架用于检索与 Id 匹配的联系人。返回包含用于编辑记录的 HTML 窗体的视图。

第二个 Edit（） 方法执行对数据库的实际更新。 此方法接受 Contact 类的实例作为参数。 ASP.NET MVC 框架会自动将表单字段从"编辑"窗体绑定到此类。 请注意，在编辑联系人时，您没有包含 [Bind] 属性（我们需要 Id 属性的值）。

实体框架用于将修改后的联系人保存到数据库。 必须首先从数据库中检索原始联系人。 接下来，调用实体框架应用属性更改（） 方法来记录对联系人的更改。 最后，调用实体框架保存更改（） 方法来保留对基础数据库的更改。

您可以通过右键单击 Edit（） 方法并选择菜单选项"添加视图"来生成包含"编辑"窗体的视图。 在"添加视图"对话框中，选择 **"联系人管理器.模型.联系人类"** 和 **"编辑**视图"内容（参见图 19）。

[![“新建项目”对话框](iteration-1-create-the-application-cs/_static/image19.jpg)](iteration-1-create-the-application-cs/_static/image37.png)

**图 19**： 添加编辑视图 （[单击以查看全尺寸图像](iteration-1-create-the-application-cs/_static/image38.png)）

单击"添加"按钮时，将自动生成新的"编辑"视图。 生成的 HTML 窗体包含对应于 Contact 类的每个属性的字段（请参见清单 7）。

**清单7 - 视图\home_编辑.aspx**

[!code-aspx[Main](iteration-1-create-the-application-cs/samples/sample7.aspx)]

## <a name="deleting-contacts"></a>删除联系人

如果要删除联系人，则需要向主控制器类添加两个 Delete（） 操作。 第一个删除（） 操作显示删除确认表单。 第二个 Delete（） 操作执行实际删除。

> [!NOTE] 
> 
> 稍后，在迭代#7中，我们修改联系人管理器，以便它支持 Ajax 删除的一个步骤。

清单8中包含两种新的 Delete（） 方法。

**清单8 - 控制器\主控制器.cs（删除方法）**

[!code-csharp[Main](iteration-1-create-the-application-cs/samples/sample8.cs)]

第一个 Delete（） 方法返回一个确认表单，用于从数据库中删除联系人记录（参见图 20）。 第二个 Delete（） 方法对数据库执行实际删除操作。 从数据库检索原始联系人后，将调用实体框架 DeleteObject（） 和保存更改（）方法以执行数据库删除。

[![“新建项目”对话框](iteration-1-create-the-application-cs/_static/image20.jpg)](iteration-1-create-the-application-cs/_static/image39.png)

**图20**：删除确认视图 （[单击以查看全尺寸图像](iteration-1-create-the-application-cs/_static/image40.png)）

我们需要修改 Index 视图，以便它包含用于删除联系人记录的链接（参见图 21）。 您需要将以下代码添加到包含"编辑"链接的同一表单元格中：

Html.操作链接（=id_item。Id +） %&gt;

[![“新建项目”对话框](iteration-1-create-the-application-cs/_static/image21.jpg)](iteration-1-create-the-application-cs/_static/image41.png)

**图21**：索引视图与编辑链接 （[单击以查看全尺寸图像](iteration-1-create-the-application-cs/_static/image42.png)）

接下来，我们需要创建删除确认视图。 右键单击主控制器类中的 Delete（） 方法，然后选择菜单选项"添加视图"。 将显示"添加视图"对话框（参见图 22）。

与"列表"、"创建"和"编辑"视图的情况不同，"添加视图"对话框不包含创建"删除"视图的选项。 而是选择 **"联系人管理器.模型.联系人**数据类"和 **"空**视图"内容。 选择"空视图内容"选项需要我们自己创建视图。

[![“新建项目”对话框](iteration-1-create-the-application-cs/_static/image22.jpg)](iteration-1-create-the-application-cs/_static/image43.png)

**图22**：添加删除确认视图 （[单击以查看全尺寸图像](iteration-1-create-the-application-cs/_static/image44.png)）

"删除"视图的内容包含在清单 9 中。 此视图包含一个表单，该窗体确认是否应删除特定联系人（参见图 21）。

**清单 9 - 视图\home_Delete.aspx**

[!code-aspx[Main](iteration-1-create-the-application-cs/samples/sample9.aspx)]

## <a name="changing-the-name-of-the-default-controller"></a>更改默认控制器的名称

使用联系人的控制器类的名称名为 HomeController 类，这可能会让您烦恼。 控制器不应被命名为"联系人控制器"？

此问题很容易解决。 首先，我们需要重构主控制器的名称。 在 Visual Studio 代码编辑器中打开 HomeController 类，右键单击类的名称并选择菜单选项 **"重构"、"重命名**"。 选择此菜单选项将打开"重命名"对话框。

[![“新建项目”对话框](iteration-1-create-the-application-cs/_static/image23.jpg)](iteration-1-create-the-application-cs/_static/image45.png)

**图23**：重构控制器名称 （[单击以查看全尺寸图像](iteration-1-create-the-application-cs/_static/image46.png)）

[![“新建项目”对话框](iteration-1-create-the-application-cs/_static/image24.jpg)](iteration-1-create-the-application-cs/_static/image47.png)

**图24**：使用重命名对话框 （[单击以查看全尺寸图像](iteration-1-create-the-application-cs/_static/image48.png)）

如果重命名控制器类，Visual Studio 也会更新"视图"文件夹中文件夹的名称。 Visual Studio 会将 [视图]主页文件夹重命名为 [视图]联系人文件夹。

进行此更改后，应用程序将不再具有主控制器。 运行应用程序时，您将获得图 25 中的错误页。

[![“新建项目”对话框](iteration-1-create-the-application-cs/_static/image25.jpg)](iteration-1-create-the-application-cs/_static/image49.png)

**图25：** 无默认控制器（[单击以查看全尺寸图像](iteration-1-create-the-application-cs/_static/image50.png)）

我们需要更新 Global.asax 文件中的默认路由，以便使用联系人控制器而不是主控制器。 打开 Global.asax 文件并修改默认路由使用的默认控制器（请参见清单 10）。

**清单10 - Global.asax.cs**

[!code-csharp[Main](iteration-1-create-the-application-cs/samples/sample10.cs)]

进行这些更改后，联系人管理器将正确运行。 现在，它将使用联系人控制器类作为默认控制器。

## <a name="summary"></a>总结

在第一次迭代中，我们以尽可能快的方式创建了一个基本的联系人管理器应用程序。 我们利用 Visual Studio 自动为控制器和视图生成初始代码。 我们还利用实体框架自动生成数据库模型类。

目前，我们可以使用联系人管理器应用程序列出、创建、编辑和删除联系人记录。 换句话说，我们可以执行数据库驱动的 Web 应用程序所需的所有基本数据库操作。

不幸的是，我们的应用程序有一些问题。 首先，我犹豫地承认这一点，联系人管理器应用程序不是最有吸引力的应用程序。 它需要一些设计工作。 在下一次迭代中，我们将了解如何更改默认视图母版页和级联样式表，以改善应用程序的外观。

其次，我们尚未实现任何表单验证。 例如，没有任何措施可以阻止您提交"创建联系人表单"，而无需为任何表单字段输入值。 此外，您还可以输入无效的电话号码和电子邮件地址。 我们开始在迭代#3解决表单验证问题。

最后，最重要的是，无法轻松修改或维护联系人管理器应用程序的当前迭代。 例如，数据库访问逻辑直接烘焙到控制器操作中。 这意味着，如果不修改控制器，我们就无法修改数据访问代码。 在以后的迭代中，我们探索了可以实现的软件设计模式，以使联系人管理器对更改更具弹性。

> [!div class="step-by-step"]
> [下一页](iteration-2-make-the-application-look-nice-cs.md)

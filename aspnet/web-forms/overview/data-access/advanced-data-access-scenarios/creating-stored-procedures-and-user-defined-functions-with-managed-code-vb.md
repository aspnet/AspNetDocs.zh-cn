---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/creating-stored-procedures-and-user-defined-functions-with-managed-code-vb
title: 用托管代码 (VB) 创建存储过程和用户定义函数 |Microsoft Docs
author: rick-anderson
description: Microsoft SQL Server 2005 与 .NET 公共语言运行时集成，以允许开发人员通过托管代码创建数据库对象。 本教程 .。。
ms.author: riande
ms.date: 08/03/2007
ms.assetid: 8be9a51b-ea6b-46c7-bfa2-476d9b14c24c
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/creating-stored-procedures-and-user-defined-functions-with-managed-code-vb
msc.type: authoredcontent
ms.openlocfilehash: 30c37750d89ff3503ead32c0b2a9708b99d785ff
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045281"
---
# <a name="creating-stored-procedures-and-user-defined-functions-with-managed-code-vb"></a>使用托管代码创建存储过程和用户定义的函数 (VB)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_75_VB.zip) 或 [下载 PDF](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/datatutorial75vb1.pdf)

> Microsoft SQL Server 2005 与 .NET 公共语言运行时集成，以允许开发人员通过托管代码创建数据库对象。 本教程演示如何通过 Visual Basic 或 c # 代码创建托管存储过程和托管用户定义函数。 我们还会看到这些版本的 Visual Studio 如何允许你调试此类托管数据库对象。

## <a name="introduction"></a>简介

Microsoft SQL Server 2005 等数据库使用 [结构化查询语言 (t-sql) ](http://en.wikipedia.org/wiki/Transact-SQL) 来插入、修改和检索数据。 大多数数据库系统都包含用于对一系列 SQL 语句进行分组的构造，这些语句随后可以作为单个可重用单元执行。 存储过程是一个示例。 另一种是 *用户定义函数* (udf) ，这是我们将在步骤9中更详细地检查的构造。

SQL 的核心是设计用于处理数据集的。 `SELECT`、 `UPDATE` 和 `DELETE` 语句本质上适用于对应表中的所有记录，并且仅受其子句限制 `WHERE` 。 不过，许多语言功能都设计为一次处理一条记录和操作标量数据。 [ `CURSOR` 允许一](http://www.sqlteam.com/item.asp?ItemID=553)组一次遍历一组记录。 字符串操作功能 `LEFT` ，例如、 `CHARINDEX` 和 `PATINDEX` 处理标量数据。 SQL 还包括和等控制流 `IF` 语句 `WHILE` 。

在 Microsoft SQL Server 2005 之前，存储过程和 Udf 只能定义为 T-sql 语句的集合。 然而，SQL Server 2005 旨在提供与 [公共语言运行时 (CLR) ](https://msdn.microsoft.com/netframework/aa497266.aspx)（这是所有 .net 程序集使用的运行时）的集成。 因此，可以使用托管代码创建 SQL Server 2005 数据库中的存储过程和 Udf。 也就是说，可以在 Visual Basic 类中创建存储过程或 UDF 作为方法。 这使得这些存储过程和 Udf 能够利用 .NET Framework 中的功能以及您自己的自定义类中的功能。

在本教程中，我们将讨论如何创建托管存储过程和用户定义函数，以及如何将它们集成到 Northwind 数据库中。 让我们开始吧！

> [!NOTE]
> 托管数据库对象相对于其 SQL 对应项具有一些优势。 丰富的语言和熟悉程度以及重复使用现有代码和逻辑的功能具有主要优势。 但在处理不涉及多个过程逻辑的数据集时，托管数据库对象可能效率较低。 若要深入了解如何使用托管代码与 T-sql，请参阅 [使用托管代码创建数据库对象的优点](https://msdn.microsoft.com/library/k2e1fb36(VS.80).aspx)。

## <a name="step-1-moving-the-northwind-database-out-ofapp_data"></a>步骤1：将 Northwind 数据库移出`App_Data`

到目前为止，我们的所有教程都在 web 应用程序的文件夹中使用了 Microsoft SQL Server 2005 Express Edition 数据库文件 `App_Data` 。 将数据库置于 `App_Data` 简化的分发和运行这些教程，因为所有文件都位于一个目录内，并且不需要任何其他配置步骤来测试本教程。

但对于本教程，让我们将 Northwind 数据库移出， `App_Data` 并将其显式注册到 SQL Server 2005 Express Edition 的数据库实例。 虽然我们可以使用文件夹中的数据库执行本教程中的步骤 `App_Data` ，但通过使用 SQL Server 2005 Express Edition 数据库实例显式注册数据库，可以更简单一些步骤。

本教程的下载内容包含两个数据库文件 `NORTHWND.MDF` ，并 `NORTHWND_log.LDF` 放置在一个名为的文件夹中 `DataFiles` 。 如果与你自己的教程实现一起使用，请关闭 Visual Studio，并将 `NORTHWND.MDF` `NORTHWND_log.LDF` 网站 s 文件夹中的和文件移动 `App_Data` 到网站外部的文件夹中。 将数据库文件移到另一个文件夹后，需要向 SQL Server 2005 Express Edition 数据库实例注册 Northwind 数据库。 这可以通过 SQL Server Management Studio 来实现。 如果在计算机上安装了非 Express 版本的 SQL Server 2005，则很可能已经安装了 Management Studio。 如果计算机上只有 SQL Server 2005 Express Edition，请花点时间下载并安装 [Microsoft SQL Server Management Studio Express](https://www.microsoft.com/downloads/details.aspx?displaylang=en&amp;FamilyID=C243A5AE-4BD1-4E3D-94B8-5A0F62BF7796)。

启动 SQL Server Management Studio。 如图1所示，Management Studio 首先询问要连接到哪个服务器。 为 "服务器名称" 输入 localhost\SQLExpress，在 "身份验证" 下拉列表中选择 "Windows 身份验证"，然后单击 "连接"。

![连接到相应的数据库实例](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image1.png)

**图 1**：连接到相应的数据库实例

建立连接后，"对象资源管理器" 窗口将列出有关 SQL Server 2005 Express Edition 数据库实例的信息，其中包括数据库、安全信息、管理选项等。

需要在文件夹中附加 Northwind 数据库 `DataFiles` (或者将其移) 到 SQL Server 2005 Express Edition 数据库实例。 右键单击 "数据库" 文件夹，然后从上下文菜单中选择 "附加" 选项。 此时将显示 "附加数据库" 对话框。 单击 "添加" 按钮，向下钻取到相应的 `NORTHWND.MDF` 文件，然后单击 "确定"。 此时，屏幕应类似于图2。

[![连接到相应的数据库实例](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image3.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image2.png)

**图 2**：连接到相应的数据库实例 ([单击查看全尺寸图像](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image4.png)) 

> [!NOTE]
> Management Studio 通过 "附加数据库" 对话框连接到 SQL Server 2005 Express Edition 实例时，不允许向下钻取到用户配置文件目录，例如 "我的文档"。 因此，请确保将 `NORTHWND.MDF` 和文件放 `NORTHWND_log.LDF` 在非用户配置文件目录中。

单击 "确定" 按钮以附加该数据库。 "附加数据库" 对话框将关闭，对象资源管理器现在应列出刚刚连接的数据库。 Northwind 数据库可能有类似于的名称 `9FE54661B32FDD967F51D71D0D5145CC_LINE ARTICLES\DATATUTORIALS\VOLUME 3\CSHARP\73\ASPNET_DATA_TUTORIAL_75_CS\APP_DATA\NORTHWND.MDF` 。 右键单击数据库并选择 "重命名"，将数据库重命名为 Northwind。

![将数据库重命名为 Northwind](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image5.png)

**图 3**：将数据库重命名为 Northwind

## <a name="step-2-creating-a-new-solution-and-sql-server-project-in-visual-studio"></a>步骤2：在 Visual Studio 中创建新的解决方案和 SQL Server 项目

若要在 SQL Server 2005 中创建托管存储过程或 Udf，我们将在类中编写存储过程和 UDF 逻辑作为 Visual Basic 代码。 编写代码后，我们需要将此类编译为 (文件) 的程序集，将 `.dll` 程序集注册到 SQL Server 数据库，然后在数据库中创建指向程序集中相应方法的存储过程或 UDF 对象。 可以手动执行这些步骤。 我们可以在任何文本编辑器中创建代码，使用 Visual Basic 编译器 () 从命令行编译代码 `vbc.exe` ，使用 [`CREATE ASSEMBLY`](https://msdn.microsoft.com/library/ms189524.aspx) 命令或从 Management Studio 将其注册到数据库，并通过类似的方法添加存储过程或 UDF 对象。 幸运的是，Visual Studio 的专业版和团队系统版本包括自动执行这些任务的 SQL Server 项目类型。 在本教程中，我们将逐步介绍如何使用 SQL Server 项目类型创建托管存储过程和 UDF。

> [!NOTE]
> 如果你正在使用 Visual Web Developer 或 Visual Studio Standard edition，则必须改用手动方法。 步骤13详细说明了如何手动执行这些步骤。 我建议您在阅读步骤13之前先阅读第2步到第12步，因为这些步骤包括必须应用的重要 SQL Server 配置说明，而不考虑您使用的 Visual Studio 的版本。

首先打开 Visual Studio。 从 "文件" 菜单中，选择 "新建项目" 以显示 "新建项目" 对话框 (参见图 4) 。 向下钻取到数据库项目类型，然后从右侧列出的模板中，选择创建新的 SQL Server 项目。 我已经选择命名此项目 `ManagedDatabaseConstructs` 并将其放置在一个名为的解决方案中 `Tutorial75` 。

[![创建新的 SQL Server 项目](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image7.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image6.png)

**图 4**：创建新 SQL Server 项目 ([单击查看完全大小的图像](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image8.png)) 

单击 "新建项目" 对话框中的 "确定" 按钮，创建解决方案并 SQL Server 项目。

SQL Server 项目与特定数据库相关联。 因此，在创建新的 SQL Server 项目后，将立即要求您指定此信息。 图5显示了 "新建数据库引用" 对话框，该对话框已填充以指向我们在步骤1中的 SQL Server 2005 Express Edition 数据库实例中注册的 Northwind 数据库。

![将 SQL Server 项目与 Northwind 数据库相关联](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image9.png)

**图 5**：将 SQL Server 项目与 Northwind 数据库相关联

为了调试托管存储过程和我们将在此项目中创建的 Udf，需要为连接启用 SQL/CLR 调试支持。 将 SQL Server 项目与新数据库关联时 (如图5所示) ，Visual Studio 会询问我们是否要在连接时启用 SQL/CLR 调试 (参见图 6) 。 单击“是”。

![启用 SQL/CLR 调试](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image10.png)

**图 6**：启用 SQL/CLR 调试

此时，新的 SQL Server 项目已添加到解决方案中。 它包含一个名为 `Test Scripts` 的文件夹，其中包含一个名为的文件 `Test.sql` ，该文件用于调试在项目中创建的托管数据库对象。 我们将在步骤12中查看调试。

现在，我们可以将新的托管存储过程和 Udf 添加到此项目中，但在此之前，我们首先要在解决方案中包含现有的 web 应用程序。 从 "文件" 菜单中选择 "添加" 选项，然后选择 "现有网站"。 浏览到相应的网站文件夹，然后单击 "确定"。 如图7所示，这将更新解决方案以包含两个项目：网站和 `ManagedDatabaseConstructs` SQL Server 项目。

![解决方案资源管理器现在包括两个项目](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image11.png)

**图 7**：解决方案资源管理器现在包含两个项目

`NORTHWNDConnectionString`中的值 `Web.config` 当前引用 `NORTHWND.MDF` 文件夹中的文件 `App_Data` 。 由于已从中删除此数据库 `App_Data` 并在 SQL Server 2005 Express Edition 数据库实例中显式注册了该数据库，因此需要相应地更新 `NORTHWNDConnectionString` 值。 打开 `Web.config` 网站中的文件并更改值， `NORTHWNDConnectionString` 使连接字符串读取： `Data Source=localhost\SQLExpress;Initial Catalog=Northwind;Integrated Security=True` 。 进行此更改之后， `<connectionStrings>` 中的部分 `Web.config` 应如下所示：

[!code-xml[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample1.xml)]

> [!NOTE]
> 如 [前面的教程](debugging-stored-procedures-vb.md)中所述，当从客户端应用程序（如 ASP.NET 网站）调试 SQL Server 对象时，需要禁用连接池。 上面所示的连接字符串禁用连接池 ( `Pooling=false` ) 。 如果不打算从 ASP.NET 网站调试托管存储过程和 Udf，请启用连接池。

## <a name="step-3-creating-a-managed-stored-procedure"></a>步骤3：创建托管存储过程

若要将托管存储过程添加到 Northwind 数据库，我们首先需要创建存储过程作为 SQL Server 项目中的方法。 在解决方案资源管理器中，右键单击 `ManagedDatabaseConstructs` 项目名称，然后选择 "添加新项"。 此时将显示 "添加新项" 对话框，其中列出了可添加到项目中的托管数据库对象的类型。 如图8所示，这包括存储过程和用户定义的函数，等等。

首先，让我们添加一个存储过程，该存储过程只返回已停止使用的所有产品。 命名新的存储过程文件 `GetDiscontinuedProducts.vb` 。

[![添加名为 GetDiscontinuedProducts 的新存储过程](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image13.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image12.png)

**图 8**：添加名为 (的新存储过程 `GetDiscontinuedProducts.vb` [单击以查看全尺寸图像](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image14.png)) 

这将创建一个具有以下内容的新 Visual Basic 类文件：

[!code-vb[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample2.vb)]

请注意，存储过程是作为 `Shared` 类文件中名为的方法实现的 `Partial` `StoredProcedures` 。 此外， `GetDiscontinuedProducts` 方法使用[ `SqlProcedure` 特性](https://msdn.microsoft.com/library/microsoft.sqlserver.server.sqlprocedureattribute.aspx)进行修饰，后者将方法标记为存储过程。

下面的代码创建一个 `SqlCommand` 对象，并将其设置 `CommandText` 为一个 `SELECT` 查询，该查询将返回 `Products` 表中其字段等于1的产品的所有列 `Discontinued` 。 然后执行该命令，并将结果发送回客户端应用程序。 将此代码添加到 `GetDiscontinuedProducts` 方法。

[!code-vb[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample3.vb)]

所有托管数据库对象都有权访问表示调用方上下文的[ `SqlContext` 对象](https://msdn.microsoft.com/library/ms131108.aspx)。 `SqlContext`通过对象的[ `Pipe` 属性](https://msdn.microsoft.com/library/microsoft.sqlserver.server.sqlcontext.pipe.aspx)提供对该[ `SqlPipe` 对象](https://msdn.microsoft.com/library/microsoft.sqlserver.server.sqlpipe.aspx)的访问。 此 `SqlPipe` 对象用于在 SQL Server 数据库与调用应用程序之间运送信息。 顾名思义， [ `ExecuteAndSend` 方法](https://msdn.microsoft.com/library/microsoft.sqlserver.server.sqlpipe.executeandsend.aspx)会执行传入的 `SqlCommand` 对象，并将结果发送回客户端应用程序。

> [!NOTE]
> 托管数据库对象最适用于使用过程逻辑而不是基于集的逻辑的存储过程和 Udf。 过程逻辑涉及逐行处理数据集，或使用标量数据。 `GetDiscontinuedProducts`然而，我们刚刚创建的方法不涉及过程逻辑。 因此，它最好作为 T-sql 存储过程实现。 它作为托管存储过程来实现，以演示创建和部署托管存储过程所需的步骤。

## <a name="step-4-deploying-the-managed-stored-procedure"></a>步骤4：部署托管存储过程

完成此代码后，我们就可以将其部署到 Northwind 数据库。 部署 SQL Server 项目会将代码编译到一个程序集中，将该程序集注册到数据库，并在数据库中创建相应的对象，并将这些对象链接到该程序集中的适当方法。 部署选项执行的确切任务集在步骤13中更精确地拼写在一起。 右键单击 `ManagedDatabaseConstructs` "解决方案资源管理器中的项目名称，然后选择" 部署 "选项。 但是，部署会失败，并出现以下错误： "外部" 附近的语法不正确。 您可能需要将当前数据库的兼容级别设置为更高的值，以启用此功能。 请参阅存储过程的帮助 `sp_dbcmptlevel` 。

当尝试向 Northwind 数据库注册程序集时，会出现此错误消息。 为了向 SQL Server 2005 数据库注册程序集，数据库的兼容级别必须设置为90。 默认情况下，新的 SQL Server 2005 数据库的兼容级别为90。 但是，使用 Microsoft SQL Server 2000 创建的数据库的默认兼容级别为80。 由于 Northwind 数据库最初是 Microsoft SQL Server 2000 的数据库，因此其兼容性级别当前设置为80，因此需要增加到90才能注册托管数据库对象。

若要更新数据库的兼容级别，请在 Management Studio 中打开一个新查询窗口，然后输入：

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample4.sql)]

单击工具栏中的 "执行" 图标以运行上面的查询。

[![更新 Northwind 数据库的兼容级别](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image16.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image15.png)

**图 9**：更新 Northwind 数据库的兼容级别 ([单击查看全尺寸映像](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image17.png)) 

更新兼容级别后，重新部署 SQL Server 项目。 这一次应完成部署，而不会发生错误。

返回 SQL Server Management Studio，右键单击对象资源管理器中的 Northwind 数据库，然后选择 "刷新"。 接下来，向下钻取可编程性文件夹，然后展开 "程序集" 文件夹。 如图10所示，Northwind 数据库现在包含由项目生成的程序集 `ManagedDatabaseConstructs` 。

![现在，ManagedDatabaseConstructs 程序集已在 Northwind 数据库中注册](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image18.png)

**图 10**： `ManagedDatabaseConstructs` 程序集现在已注册到 Northwind 数据库

同时展开 "存储过程" 文件夹。 您将看到一个名为的存储过程 `GetDiscontinuedProducts` 。 此存储过程是由部署过程创建的，并指向 `GetDiscontinuedProducts` 程序集中的方法 `ManagedDatabaseConstructs` 。 `GetDiscontinuedProducts`执行存储过程时，该存储过程将执行 `GetDiscontinuedProducts` 方法。 由于这是一个托管存储过程，因此无法通过 Management Studio (对其进行编辑，因此，) 的存储过程名称旁边会有一个锁图标。

!["存储过程" 文件夹中列出了 GetDiscontinuedProducts 存储过程](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image19.png)

**图 11**： `GetDiscontinuedProducts` 存储过程在 "存储过程" 文件夹中列出

在我们可以调用托管存储过程之前，还必须解决一个障碍：数据库配置为禁止执行托管代码。 通过打开一个新的查询窗口并执行存储过程来验证这一点 `GetDiscontinuedProducts` 。 你将收到以下错误消息：已禁用 .NET Framework 中的用户代码的执行。 启用 "clr 已启用配置选项"。

若要检查 Northwind 数据库的配置信息，请 `exec sp_configure` 在 "查询" 窗口中输入并执行该命令。 这表明，clr enabled 设置当前设置为0。

[!["Clr 已启用" 设置当前设置为0](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image21.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image20.png)

**图 12**： "clr 已启用" 设置当前设置为 0 ([单击查看完全大小的图像](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image22.png)) 

请注意，图12中的每个配置设置都列出了四个值：最小值和最大值以及配置和运行值。 若要更新已启用 clr 的设置的配置值，请执行以下命令：

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample5.sql)]

如果你重新运行， `exec sp_configure` 你将看到上述语句将 "已启用 clr" 设置为 "1"，但运行值仍设置为0。 为了使此配置更改生效，需要执行命令，该[ `RECONFIGURE` 命令](https://msdn.microsoft.com/library/ms176069.aspx)会将运行值设置为当前配置值。 只需 `RECONFIGURE` 在查询窗口中输入，然后单击工具栏中的 "执行" 图标。 如果现在运行 `exec sp_configure` ，则会看到 clr 启用了设置的 "配置" 和 "运行值" 的值1。

完成 clr 已启用配置后，便可以运行托管 `GetDiscontinuedProducts` 存储过程了。 在查询窗口中，输入并执行命令 `exec` `GetDiscontinuedProducts` 。 调用存储过程会导致执行方法中的相应托管代码 `GetDiscontinuedProducts` 。 此代码发出一个 `SELECT` 查询以返回所有已停止的产品并将此数据返回到调用应用程序，该应用程序在此实例中 SQL Server Management Studio。 Management Studio 收到这些结果并将其显示在 "结果" 窗口中。

[![GetDiscontinuedProducts 存储过程返回所有停产的产品](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image24.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image23.png)

**图 13**： `GetDiscontinuedProducts` 存储过程返回所有停产的产品 ([单击查看全尺寸图像](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image25.png)) 

## <a name="step-5-creating-managed-stored-procedures-that-accept-input-parameters"></a>步骤5：创建接受输入参数的托管存储过程

我们在本教程中创建的许多查询和存储过程都使用了 *参数*。 例如，在 [为类型化数据集 tableadapter 教程创建新存储过程](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md) 中，我们创建了一个名为 `GetProductsByCategoryID` 的存储过程，该存储过程接受一个名为的输入参数 `@CategoryID` 。 然后，该存储过程返回其 `CategoryID` 字段与所提供参数的值匹配的所有产品 `@CategoryID` 。

若要创建接受输入参数的托管存储过程，只需在方法的定义中指定这些参数。 为了说明这一点，让我们将另一个托管存储过程添加到 `ManagedDatabaseConstructs` 名为的项目 `GetProductsWithPriceLessThan` 。 此托管存储过程将接受指定价格的输入参数，并将返回其 `UnitPrice` 字段小于参数 s 值的所有产品。

若要将新的存储过程添加到项目中，请右键单击 `ManagedDatabaseConstructs` 项目名称，然后选择添加新的存储过程。 命名文件 `GetProductsWithPriceLessThan.vb`。 正如我们在步骤3中看到的那样，这会创建一个新的 Visual Basic 类文件，其中包含类中的一个名为的方法 `GetProductsWithPriceLessThan` `Partial` `StoredProcedures` 。

更新 `GetProductsWithPriceLessThan` 方法的定义，使其接受 [`SqlMoney`](https://msdn.microsoft.com/library/system.data.sqltypes.sqlmoney.aspx) 名为的输入参数 `price` ，并编写执行和返回查询结果的代码：

[!code-vb[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample6.vb)]

`GetProductsWithPriceLessThan`方法的定义和代码与 `GetDiscontinuedProducts` 步骤3中创建的方法的定义和代码非常相似。 唯一的区别在于，该 `GetProductsWithPriceLessThan` 方法接受作为输入参数 (`price`) ， `SqlCommand` s 查询包含参数 (`@MaxPrice`) ，并向 s 集合添加了一个参数， `SqlCommand` 并将该变量的 `Parameters` 值赋值给了 `price` 。

添加此代码后，重新部署 SQL Server 项目。 接下来，返回到 SQL Server Management Studio 并刷新 "存储过程" 文件夹。 应该会看到一个新条目 `GetProductsWithPriceLessThan` 。 在查询窗口中，输入并执行命令 `exec GetProductsWithPriceLessThan 25` ，该命令将列出小于 $25 的所有产品，如图14所示。

[![显示 $25 下的产品](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image27.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image26.png)

**图 14**：显示 $25 下的产品 ([单击查看全尺寸图像](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image28.png)) 

## <a name="step-6-calling-the-managed-stored-procedure-from-the-data-access-layer"></a>步骤6：从数据访问层调用托管存储过程

此时，我们已将 `GetDiscontinuedProducts` 和 `GetProductsWithPriceLessThan` 托管存储过程添加到项目中 `ManagedDatabaseConstructs` ，并已向 Northwind SQL Server 数据库注册了这些过程。 我们还从 SQL Server Management Studio 调用这些托管存储过程 (参见图13和 14) 。 不过，为了让 ASP.NET 应用程序使用这些托管存储过程，我们需要将它们添加到体系结构中的数据访问和业务逻辑层。 在此步骤中，我们会将两个新方法添加到 `ProductsTableAdapter` `NorthwindWithSprocs` 类型化数据集中的中，这是最初在 [为类型化数据集 Tableadapter 教程创建新存储过程](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md) 中创建的。 在步骤7中，我们将向 BLL 添加相应的方法。

`NorthwindWithSprocs`在 Visual Studio 中打开类型化的数据集，并通过将新方法添加到指定的来开始 `ProductsTableAdapter` `GetDiscontinuedProducts` 。 若要将新方法添加到 TableAdapter，请在设计器中右键单击 TableAdapter 的名称，然后从上下文菜单中选择 "添加查询" 选项。

> [!NOTE]
> 由于我们已将 Northwind 数据库从 `App_Data` 文件夹移动到 SQL Server 2005 Express Edition 数据库实例，因此 Web.config 中的相应连接字符串进行更新以反映此更改。 在步骤2中，我们讨论了如何更新 `NORTHWNDConnectionString` 中的值 `Web.config` 。 如果忘记进行此更新，则会看到错误消息 "添加查询失败"。 `NORTHWNDConnectionString` `Web.config` 尝试将新方法添加到 TableAdapter 时，找不到对话框中对象的连接。 若要解决此错误，请单击 "确定"，然后 `Web.config` `NORTHWNDConnectionString` 根据步骤2中所述，单击并更新值。 然后尝试重新将方法添加到 TableAdapter。 这次应该不会出错。

添加新方法会启动 "TableAdapter 查询配置向导"，在过去的教程中已多次使用该向导。 第一个步骤要求我们指定 TableAdapter 应如何访问数据库：通过即席 SQL 语句或通过新的或现有的存储过程。 由于我们已使用数据库创建并注册了 `GetDiscontinuedProducts` 托管存储过程，因此请选择 "使用现有存储过程" 选项，然后单击 "下一步"。

[![选择 "使用现有存储过程" 选项](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image30.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image29.png)

**图 15**：选择 "使用现有存储过程" 选项 ([单击查看全尺寸图像](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image31.png)) 

下一个屏幕提示我们输入该方法将调用的存储过程。 `GetDiscontinuedProducts`从下拉列表中选择托管存储过程，然后单击 "下一步"。

[![选择 GetDiscontinuedProducts 托管存储过程](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image33.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image32.png)

**图 16**：选择 `GetDiscontinuedProducts` 托管存储过程 ([单击查看全尺寸图像](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image34.png)) 

然后，需要指定存储过程是返回行、单个值还是不返回任何内容。 由于 `GetDiscontinuedProducts` 返回一组停用的产品行，请选择第一个选项 ( 表格数据 ) 并单击 "下一步"。

[![选择表格数据选项](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image36.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image35.png)

**图 17**：选择 "表格数据" 选项 ([单击查看全尺寸图像](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image37.png)) 

最终的向导屏幕允许您指定所使用的数据访问模式和生成的方法的名称。 选中这两个复选框，并为方法 `FillByDiscontinued` 和命名 `GetDiscontinuedProducts` 。 单击“完成”以完成向导。

[![将方法命名为 FillByDiscontinued 和 GetDiscontinuedProducts](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image39.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image38.png)

**图 18**：命名方法 `FillByDiscontinued` ， `GetDiscontinuedProducts` ([单击以查看完全大小的图像](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image40.png)) 

重复上述步骤， `FillByPriceLessThan` `GetProductsWithPriceLessThan` 在中为 `ProductsTableAdapter` `GetProductsWithPriceLessThan` 托管存储过程创建名为和的方法。

图19显示了在将方法添加到的 `ProductsTableAdapter` `GetDiscontinuedProducts` 和 `GetProductsWithPriceLessThan` 托管存储过程后，数据集设计器的屏幕快照。

[![ProductsTableAdapter 包括此步骤中添加的新方法](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image42.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image41.png)

**图 19**： `ProductsTableAdapter` 包含在此步骤中添加的新方法 ([单击查看全尺寸图像](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image43.png)) 

## <a name="step-7-adding-corresponding-methods-to-the-business-logic-layer"></a>步骤7：将相应的方法添加到业务逻辑层

现在我们已将数据访问层更新为包含用于调用步骤4和5中添加的托管存储过程的方法，我们需要将相应的方法添加到业务逻辑层。 将以下两个方法添加到 `ProductsBLLWithSprocs` 类：

[!code-vb[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample7.vb)]

这两种方法只调用相应的 DAL 方法并返回 `ProductsDataTable` 实例。 `DataObjectMethodAttribute`每个方法上面的标记将导致这些方法包含在 ObjectDataSource 的 "配置数据源" 向导的 "选择" 选项卡的下拉列表中。

## <a name="step-8-invoking-the-managed-stored-procedures-from-the-presentation-layer"></a>步骤8：从表示层调用托管存储过程

随着业务逻辑和数据访问层的扩充，以支持调用 `GetDiscontinuedProducts` 和 `GetProductsWithPriceLessThan` 托管存储过程，现在我们可以通过 ASP.NET 页显示这些存储过程结果。

打开 `ManagedFunctionsAndSprocs.aspx` 文件夹中的页面 `AdvancedDAL` ，然后从 "工具箱" 中将一个 GridView 拖到设计器上。 将 GridView s `ID` 属性设置为， `DiscontinuedProducts` 并从其智能标记将其绑定到名为的新 ObjectDataSource `DiscontinuedProductsDataSource` 。 配置 ObjectDataSource 以便从类方法拉取其数据 `ProductsBLLWithSprocs` `GetDiscontinuedProducts` 。

[![将 ObjectDataSource 配置为使用 ProductsBLLWithSprocs 类](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image45.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image44.png)

**图 20**：配置 ObjectDataSource 以使用 `ProductsBLLWithSprocs` 类 ([单击查看完全大小的图像](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image46.png)) 

[![从 "选择" 选项卡的下拉列表中选择 "GetDiscontinuedProducts" 方法](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image48.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image47.png)

**图 21**： `GetDiscontinuedProducts` 从 "选择" 选项卡的下拉列表中选择方法 ([单击查看全尺寸图像](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image49.png)) 

由于此网格将用于显示产品信息，因此请将 "更新"、"插入" 和 "删除" 选项卡中的下拉列表设置为 "无 (") 然后单击 "完成"。

完成向导后，Visual Studio 将为中的每个数据字段自动添加 BoundField 或 CheckBoxField `ProductsDataTable` 。 请花点时间删除所有字段（ `ProductName` 和除外 `Discontinued` ），此时，GridView 和 ObjectDataSource 的声明性标记应如下所示：

[!code-aspx[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample8.aspx)]

请花点时间查看浏览器中的此页。 访问该页时，ObjectDataSource 会调用 `ProductsBLLWithSprocs` 类的 `GetDiscontinuedProducts` 方法。 正如我们在步骤7中看到的那样，此方法会向下调用 DAL 的 `ProductsDataTable` class `GetDiscontinuedProducts` 方法，该方法调用 `GetDiscontinuedProducts` 存储过程。 此存储过程是托管存储过程，可执行我们在步骤3中创建的代码，并返回废止的产品。

托管存储过程返回的结果由 DAL 打包到中 `ProductsDataTable` ，然后返回到 BLL，然后将其返回到在其中绑定到 GridView 并显示的表示层。 根据需要，该网格列出了已停止使用的产品。

[![已停止使用的产品](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image51.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image50.png)

**图 22**：列出了废止的产品 ([单击查看全尺寸图像](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image52.png)) 

为了进一步练习，请向页面添加一个文本框和另一个 GridView。 通过调用类 s 方法，使此 GridView 显示小于在文本框中输入的量的产品 `ProductsBLLWithSprocs` `GetProductsWithPriceLessThan` 。

## <a name="step-9-creating-and-calling-t-sql-udfs"></a>步骤9：创建和调用 T-sql Udf

用户定义的函数或 Udf 是数据库对象，它在编程语言中严格模拟函数的语义。 与 Visual Basic 中的函数一样，Udf 可以包含可变数量的输入参数，并返回特定类型的值。 UDF 可以返回标量数据-字符串、整数等，也可以是表格数据。 让我们快速了解两种类型的 Udf，从返回标量数据类型的 UDF 开始。

下面的 UDF 计算特定产品的清单的估计值。 它通过以下三种方式实现此目的：采用三个输入参数- `UnitPrice` `UnitsInStock` 特定产品的、和 `Discontinued` 值，并返回类型为的值 `money` 。 它通过将与相乘，来计算库存的估计值 `UnitPrice` `UnitsInStock` 。 对于停止项，此值将减半。

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample9.sql)]

将此 UDF 添加到数据库后，可以通过 Management Studio 依次展开可编程性文件夹、函数和标量值函数来找到该 UDF。 它可用于 `SELECT` 如下查询：

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample10.sql)]

我已经将 `udf_ComputeInventoryValue` UDF 添加到 Northwind 数据库中;图23显示了 `SELECT` 通过 Management Studio 查看的上述查询的输出。 另请注意，UDF 在对象资源管理器中的 "标量值函数" 文件夹下列出。

[![列出了每个产品的库存值](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image54.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image53.png)

**图 23**：列出了每个产品的库存值 ([单击查看全尺寸图像](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image55.png)) 

Udf 还可以返回表格数据。 例如，我们可以创建一个 UDF 来返回属于特定类别的产品：

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample11.sql)]

`udf_GetProductsByCategoryID`UDF 接受 `@CategoryID` 输入参数并返回指定查询的结果 `SELECT` 。 创建后，可以在 `FROM` 查询的 (或) 子句中引用此 UDF `JOIN` `SELECT` 。 下面的示例将返回 `ProductID` `ProductName` `CategoryID` 每个饮料的、和值。

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample12.sql)]

我已经将 `udf_GetProductsByCategoryID` UDF 添加到 Northwind 数据库中;图24显示了 `SELECT` 通过 Management Studio 查看的上述查询的输出。 可在对象资源管理器的 "表值函数" 文件夹中找到返回表格数据的 Udf。

[![为每个饮料列出 ProductID、ProductName 和类别名称](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image57.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image56.png)

**图 24**： `ProductID` 列出了 `ProductName` 每个饮料 (的、和，请 `CategoryID` [单击查看全尺寸图像](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image58.png)) 

> [!NOTE]
> 有关创建和使用 Udf 的详细信息，请查看 [用户定义函数的简介](http://www.sqlteam.com/item.asp?ItemID=1955)。 还应查看 [用户定义函数的优点和缺点](http://www.samspublishing.com/articles/article.asp?p=31724&amp;rl=1)。

## <a name="step-10-creating-a-managed-udf"></a>步骤10：创建托管 UDF

`udf_ComputeInventoryValue` `udf_GetProductsByCategoryID` 在上述示例中创建的和 Udf 是 t-sql 数据库对象。 SQL Server 2005 还支持托管 Udf，可将其添加到 `ManagedDatabaseConstructs` 项目中，就像步骤3和步骤5中的托管存储过程一样。 对于此步骤，请 `udf_ComputeInventoryValue` 在托管代码中实现 UDF。

若要将托管 UDF 添加到 `ManagedDatabaseConstructs` 项目中，请右键单击 "解决方案资源管理器中的项目名称，然后选择" 添加新项 "。 从 "添加新项" 对话框中选择用户定义的模板，并将新的 UDF 文件命名为 `udf_ComputeInventoryValue_Managed.vb` 。

[![向 ManagedDatabaseConstructs 项目添加一个新的托管 UDF](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image60.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image59.png)

**图 25**：向项目添加新的托管 UDF `ManagedDatabaseConstructs` ([单击查看全尺寸图像](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image61.png)) 

用户定义函数模板创建一个名为的 `Partial` 类 `UserDefinedFunctions` ，该方法的名称与类文件的名称相同 `udf_ComputeInventoryValue_Managed` ，在此实例中)  (。 此方法使用特性进行修饰，该[ `SqlFunction` 特性](https://msdn.microsoft.com/library/microsoft.sqlserver.server.sqlfunctionattribute.aspx)将方法标记为托管的 UDF。

[!code-vb[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample13.vb)]

`udf_ComputeInventoryValue`方法当前返回[ `SqlString` 对象](https://msdn.microsoft.com/library/system.data.sqltypes.sqlstring.aspx)，不接受任何输入参数。 我们需要更新方法定义，使其接受三个输入参数- `UnitPrice` 、 `UnitsInStock` 和 `Discontinued` -并返回一个 `SqlMoney` 对象。 用于计算库存值的逻辑与 T-sql UDF 中的逻辑相同 `udf_ComputeInventoryValue` 。

[!code-vb[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample14.vb)]

请注意，UDF 方法的输入参数为其对应的 SQL 类型： `SqlMoney` 对于 `UnitPrice` 字段，对于 [`SqlInt16`](https://msdn.microsoft.com/library/system.data.sqltypes.sqlint16.aspx) ，对于 `UnitsInStock` 和 [`SqlBoolean`](https://msdn.microsoft.com/library/system.data.sqltypes.sqlboolean.aspx) 为 `Discontinued` 。 这些数据类型反映了在表中定义的类型 `Products` ： `UnitPrice` 列的类型为 `money` 、类型为的 `UnitsInStock` 列 `smallint` 和类型为的 `Discontinued` 列 `bit` 。

代码首先创建一个 `SqlMoney` 名为的实例 `inventoryValue` ，并为其分配值0。 `Products`该表允许 `NULL` 和列中的数据库值 `UnitsInPrice` `UnitsInStock` 。 因此，我们需要首先检查这些值是否包含 `NULL` s，我们通过 `SqlMoney` 对象的[ `IsNull` 属性](https://msdn.microsoft.com/library/system.data.sqltypes.sqlmoney.isnull.aspx)来执行此操作。 如果 `UnitPrice` 和都 `UnitsInStock` 包含非 `NULL` 值，则我们会将计算 `inventoryValue` 为二者的乘积。 如果 `Discontinued` 为 true，则分该值。

> [!NOTE]
> `SqlMoney`对象只允许将两个 `SqlMoney` 实例相乘。 它不允许 `SqlMoney` 实例与原义浮点数相乘。 因此，分将 `inventoryValue` 其与值为0.5 的新 `SqlMoney` 实例相乘。

## <a name="step-11-deploying-the-managed-udf"></a>步骤11：部署托管 UDF

现在，已创建托管 UDF，接下来可以将其部署到 Northwind 数据库。 正如我们在步骤4中看到的那样，通过右键单击解决方案资源管理器中的项目名称，然后从上下文菜单中选择 "部署" 选项，可部署 SQL Server 项目中的托管对象。

部署项目后，返回到 SQL Server Management Studio 并刷新 "标量值函数" 文件夹。 现在应会看到两个条目：

- `dbo.udf_ComputeInventoryValue` -在步骤9中创建的 T-sql UDF 和
- `dbo.udf ComputeInventoryValue_Managed` -刚刚部署的步骤10中创建的托管 UDF。

若要测试此托管 UDF，请从 Management Studio 中执行以下查询：

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample15.sql)]

此命令使用托管 `udf ComputeInventoryValue_Managed` udf 而不是 T-sql `udf_ComputeInventoryValue` UDF，但输出相同。 请返回图23，查看 UDF 输出的屏幕截图。

## <a name="step-12-debugging-the-managed-database-objects"></a>步骤12：调试托管数据库对象

在 [调试存储过程](debugging-stored-procedures-vb.md) 教程中，我们讨论了三个用于通过 Visual Studio 调试 SQL Server 的选项：直接数据库调试、应用程序调试以及从 SQL Server 项目调试。 不能通过直接数据库调试来调试托管数据库对象，但可以从客户端应用程序进行调试，也可以直接从 SQL Server 项目进行调试。 但是，若要进行调试，SQL Server 2005 数据库必须允许 SQL/CLR 调试。 回忆一下，当我们首次创建项目时， `ManagedDatabaseConstructs` Visual Studio 会询问我们是否要启用 SQL/CLR 调试 (参见步骤2中的图 6) 。 可以通过右键单击 "服务器资源管理器" 窗口中的数据库来修改此设置。

![确保数据库允许 SQL/CLR 调试](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image62.png)

**图 26**：确保数据库允许 SQL/CLR 调试

假设我们想要调试 `GetProductsWithPriceLessThan` 托管存储过程。 首先，在方法的代码中设置断点 `GetProductsWithPriceLessThan` 。

[![在 GetProductsWithPriceLessThan 方法中设置断点](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image64.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image63.png)

**图 27**：在方法中设置断点 `GetProductsWithPriceLessThan` ([单击查看全尺寸图像](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image65.png)) 

首先，让我们看一下如何从 SQL Server 项目调试托管数据库对象。 由于我们的解决方案包括两个项目- `ManagedDatabaseConstructs` SQL Server 项目和我们的网站-为了从 SQL Server 项目进行调试，我们需要指示 Visual Studio 在 `ManagedDatabaseConstructs` 我们开始调试时启动 SQL Server 项目。 右键单击 " `ManagedDatabaseConstructs` 解决方案资源管理器中的项目，然后从上下文菜单中选择" 设为启动项目 "选项。

`ManagedDatabaseConstructs`从调试器启动项目时，它会执行文件中的 SQL 语句 `Test.sql` ，该文件位于 `Test Scripts` 文件夹中。 例如，若要测试 `GetProductsWithPriceLessThan` 托管存储过程，请将现有 `Test.sql` 文件内容替换为以下语句，该语句将调用 `GetProductsWithPriceLessThan` 托管存储过程，并传入 `@CategoryID` 14.95 值：

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample16.sql)]

在您在中输入上述脚本后 `Test.sql` ，请转到 "调试" 菜单，然后选择 "启动调试" 或通过点击工具栏上的 "绿色播放" 图标来启动调试。 这会生成解决方案中的项目，将托管数据库对象部署到 Northwind 数据库，然后执行该 `Test.sql` 脚本。 此时，将命中断点，我们可以单步执行 `GetProductsWithPriceLessThan` 方法，检查输入参数的值，等等。

[![命中了 GetProductsWithPriceLessThan 方法中的断点](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image67.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image66.png)

**图 28**： `GetProductsWithPriceLessThan` 已命中方法中的断点 ([单击查看全尺寸图像](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image68.png)) 

为了使 SQL 数据库对象可以通过客户端应用程序进行调试，必须将数据库配置为支持应用程序调试。 在服务器资源管理器中右键单击该数据库，并确保选中 "应用程序调试" 选项。 此外，我们还需要将 ASP.NET 应用程序配置为与 SQL 调试器集成，并禁用连接池。 [调试存储过程](debugging-stored-procedures-vb.md)教程的步骤2中详细讨论了这些步骤。

配置 ASP.NET 应用程序和数据库后，将 ASP.NET 网站设置为启动项目并启动调试。 如果访问的页面调用了具有断点的某个托管对象，则该应用程序将停止并将控制权转到调试器，在此，你可以单步执行代码，如图28所示。

## <a name="step-13-manually-compiling-and-deploying-managed-database-objects"></a>步骤13：手动编译和部署托管数据库对象

SQL Server 项目可以轻松地创建、编译和部署托管数据库对象。 遗憾的是，SQL Server 项目仅适用于 Visual Studio 的专业版和 Team Systems 版本。 如果你使用的是 Visual Studio 或 Visual Studio Standard Edition，并且想要使用托管数据库对象，则需要手动创建和部署它们。 这涉及四个步骤：

1. 创建一个文件，其中包含托管数据库对象的源代码。
2. 将对象编译到一个程序集中，
3. 向 SQL Server 2005 数据库注册程序集，并
4. 在 SQL Server 中创建一个指向程序集中相应方法的数据库对象。

为了说明这些任务，让我们创建一个新的托管存储过程，该存储过程 `UnitPrice` 将返回大于指定值的产品。 在计算机上创建一个名为的新文件 `GetProductsWithPriceGreaterThan.vb` ，并在该文件中输入以下代码 (你可以使用 Visual Studio、记事本或任何文本编辑器来完成此) ：

[!code-vb[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample17.vb)]

此代码与 `GetProductsWithPriceLessThan` 步骤5中创建的方法的代码几乎完全相同。 唯一的区别是查询中使用的方法名称、 `WHERE` 子句和参数名称。 返回到 `GetProductsWithPriceLessThan` 方法， `WHERE` 子句读取： `WHERE UnitPrice < @MaxPrice` 。 这里， `GetProductsWithPriceGreaterThan` 我们使用： `WHERE UnitPrice > @MinPrice` 。

现在，我们需要将此类编译为程序集。 在命令行中，导航到保存文件的目录， `GetProductsWithPriceGreaterThan.vb` 并使用 c # 编译器 (`csc.exe`) 将类文件编译为程序集：

[!code-console[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample18.cmd)]

如果包含 v 的文件夹 `bc.exe` 不在系统中 `PATH` ，则必须完全引用其路径， `%WINDOWS%\Microsoft.NET\Framework\version\` 如下所示：

[!code-console[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample19.cmd)]

[![将 GetProductsWithPriceGreaterThan 编译到程序集中](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image70.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image69.png)

**图 29**：编译 `GetProductsWithPriceGreaterThan.vb` 为程序集 ([单击查看全尺寸图像](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image71.png)) 

`/t`标志指定应将 Visual Basic 类文件编译为 DLL (而不是可执行的) 。 `/out`标志指定生成的程序集的名称。

> [!NOTE]
> `GetProductsWithPriceGreaterThan.vb`你还可以使用[Visual Basic 速成版](https://msdn.microsoft.com/vstudio/express/vb/)或在 Visual Studio Standard edition 中创建单独的类库项目，而不是从命令行编译类文件。 S ren Jacob Lauritsen 提供了这样一个 Visual Basic 速成版项目，其中包含用于 `GetProductsWithPriceGreaterThan` 存储过程的代码，以及在步骤3、5和10中创建的两个托管存储过程和 UDF。 "Ren s" 项目还包含添加相应数据库对象所需的 T-sql 命令。

将代码编译为程序集后，便可以在 SQL Server 2005 数据库中注册该程序集。 这可以通过 T-sql、使用命令 `CREATE ASSEMBLY` 或 SQL Server Management Studio 来执行。 让我们重点介绍如何使用 Management Studio。

在 Management Studio 中，展开 Northwind 数据库中的 "可编程性" 文件夹。 其中一个子文件夹是程序集。 若要手动向数据库添加新程序集，请右键单击 "程序集" 文件夹，然后从上下文菜单中选择 "新建程序集"。 此时将显示 "新建程序集" 对话框 (参见图 30) 。 单击 "浏览" 按钮，选择 `ManuallyCreatedDBObjects.dll` 刚编译的程序集，然后单击 "确定" 将程序集添加到数据库中。 不应 `ManuallyCreatedDBObjects.dll` 在对象资源管理器中看到该程序集。

[![将 ManuallyCreatedDBObjects.dll 程序集添加到数据库](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image73.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image72.png)

**图 30**：将 `ManuallyCreatedDBObjects.dll` 程序集添加到数据库 ([单击查看完全大小的图像](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image74.png)) 

![ManuallyCreatedDBObjects.dll 在对象资源管理器中列出](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image75.png)

**图 31**：在 `ManuallyCreatedDBObjects.dll` 对象资源管理器中列出了

虽然已将程序集添加到 Northwind 数据库，但我们尚未将存储过程与 `GetProductsWithPriceGreaterThan` 程序集中的方法相关联。 若要完成此操作，请打开新的查询窗口并执行以下脚本：

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample20.sql)]

这会在 Northwind 数据库中创建名为的新存储过程 `GetProductsWithPriceGreaterThan` ，并将其与类中的托管方法 (相关联，该存储过程位于 `GetProductsWithPriceGreaterThan` `StoredProcedures` 程序集 `ManuallyCreatedDBObjects`) 。

执行上述脚本后，刷新对象资源管理器中的 "存储过程" 文件夹。 应该会看到一个新的存储过程条目，该条目 `GetProductsWithPriceGreaterThan` 旁边有一个锁定图标。 若要测试此存储过程，请在 "查询" 窗口中输入并执行以下脚本：

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample21.sql)]

如图32所示，上述命令显示了大于 $24.95 的产品的信息 `UnitPrice` 。

[![ManuallyCreatedDBObjects.dll 在对象资源管理器中列出](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image77.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image76.png)

**图 32**： `ManuallyCreatedDBObjects.dll` 对象资源管理器中列出了 ([单击查看完全大小的图像](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image78.png)) 

## <a name="summary"></a>摘要

Microsoft SQL Server 2005 提供与公共语言运行时的集成 (CLR) ，这允许使用托管代码创建数据库对象。 以前，只能使用 T-sql 创建这些数据库对象，但现在可以使用诸如 Visual Basic 的 .NET 编程语言创建这些对象。 在本教程中，我们创建了两个托管存储过程和一个托管的用户定义函数。

Visual Studio s SQL Server 项目类型有助于创建、编译和部署托管数据库对象。 此外，它还提供丰富的调试支持。 但 SQL Server 项目类型仅适用于 Visual Studio 的专业版和 Team Systems 版本。 对于使用 Visual Web Developer 或 Visual Studio Standard Edition 的人员，创建、编译和部署步骤必须手动执行，如我们在步骤13中所述。

很高兴编程！

## <a name="further-reading"></a>深入阅读

有关本教程中讨论的主题的详细信息，请参阅以下资源：

- [用户定义函数的优点和缺点](http://www.samspublishing.com/articles/article.asp?p=31724&amp;rl=1)
- [在托管代码中创建 SQL Server 2005 对象](https://channel9.msdn.com/Showpost.aspx?postid=142413)
- [使用 SQL Server 2005 中的托管代码创建触发器](http://www.15seconds.com/issue/041006.htm)
- [如何：创建和运行 CLR SQL Server 存储过程](https://msdn.microsoft.com/library/5czye81z(VS.80).aspx)
- [如何：创建和运行 CLR SQL Server 用户定义函数](https://msdn.microsoft.com/library/w2kae45k(VS.80).aspx)
- [如何：编辑 `Test.sql` 脚本以运行 SQL 对象](https://msdn.microsoft.com/library/ms233682(VS.80).aspx)
- [用户定义函数简介](http://www.sqlteam.com/item.asp?ItemID=1955)
- [托管代码和 SQL Server 2005 (视频) ](https://channel9.msdn.com/Showpost.aspx?postid=142413)
- [Transact-sql 参考](https://msdn.microsoft.com/library/aa299742(SQL.80).aspx)
- [演练：在托管代码中创建存储过程](https://msdn.microsoft.com/library/zxsa8hkf(VS.80).aspx)

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的 [4GuysFromRolla.com](http://www.4guysfromrolla.com)，已在使用 Microsoft Web 技术，自1998开始。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是， [*在24小时内，sam ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以到达[ mitchell@4GuysFromRolla.com 。](mailto:mitchell@4GuysFromRolla.com) 或者，通过他的博客，可以找到 [http://ScottOnWriting.NET](http://ScottOnWriting.NET) 。

## <a name="special-thanks-to"></a>特别感谢

此教程系列由许多有用的审阅者查看。 本教程的潜在客户审阅者为 Jacob Lauritsen。 除了查看本文，S ren 还创建了本文中所述的 Visual c # Express Edition 项目，以便手动编译托管数据库对象。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在中放置一行[ mitchell@4GuysFromRolla.com 。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](debugging-stored-procedures-vb.md)

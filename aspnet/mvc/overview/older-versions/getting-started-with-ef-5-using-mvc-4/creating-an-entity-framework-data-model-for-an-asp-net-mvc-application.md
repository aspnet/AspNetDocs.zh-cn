---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application
title: 为 ASP.NET MVC 应用程序创建实体框架数据模型 (1 （共10个）) |Microsoft Docs
author: tdykstra
description: 本教程系列的较新版本适用于 Visual Studio 2013、实体框架6和 MVC 5。 Contoso 大学示例 web 应用程序 de .。。
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 4ba029b6-ee7c-4e45-a0e7-b703c37e5d9a
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 9d4eddd09410d102045271c2e4662e0b4177514c
ms.sourcegitcommit: b4cdcf246850751579e45da80c9780fe56330dd0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2021
ms.locfileid: "99985200"
---
# <a name="creating-an-entity-framework-data-model-for-an-aspnet-mvc-application-1-of-10"></a>为 ASP.NET MVC 应用程序创建实体框架数据模型 (1 （共10个）) 

作者： [Tom Dykstra](https://github.com/tdykstra)

> > [!NOTE] 
> > 
> > [本教程系列的较新版本](../../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)适用于 Visual Studio 2013、实体框架6和 MVC 5。
> 
> 
> Contoso 大学示例 web 应用程序演示了如何使用实体框架5和 Visual Studio 2012 创建 ASP.NET MVC 4 应用程序。 示例应用程序供一个虚构的 Contoso 大学网站使用。 它包括诸如学生入学、 课程创建和导师分配等功能。 本系列教程介绍了如何构建 Contoso 大学的示例应用程序。
> 
> ## <a name="code-first"></a>Code First
> 
> 可以通过三种方式使用实体框架中的数据： *Database First*、 *Model First* 和 *Code First*。 本教程适用于 Code First。 有关这些工作流之间的差异以及如何为你的方案选择最佳方案的指南的信息，请参阅 [实体框架开发工作流](https://msdn.microsoft.com/library/ms178359.aspx#dbfmfcf)。
> 
> ## <a name="mvc"></a>MVC
> 
> 示例应用程序是在 [ASP.NET MVC](../../../index.md)上构建的。 如果希望使用 ASP.NET Web 窗体模型，请参阅 [模型绑定和 Web 窗体](../../../../web-forms/overview/presenting-and-managing-data/model-binding/retrieving-data.md) 教程系列和 [ASP.NET 数据访问内容映射](../../../../whitepapers/aspnet-data-access-content-map.md)。
> 
> ## <a name="software-versions"></a>软件版本
> 
> | **教程中所示** | **还适用于** |
> | --- | --- |
> | Windows 8 | Windows 7 |
> | Visual Studio 2012 | Visual Studio 2012 Express for Web。 如果尚未安装 VS 2012 或 VS 2012 Express for Web，则 Windows Azure SDK 会自动安装此设置。 Visual Studio 2013 应可行，但本教程尚未使用它进行测试，某些菜单选项和对话框有所不同。 Windows azure [SDK 的 VS 2013 版本](https://go.microsoft.com/fwlink/p/?linkid=323510) 对于 windows azure 部署是必需的。 |
> | .NET 4.5 | 所显示的大部分功能都适用于 .NET 4，但有些功能不适用。 例如，EF 中的枚举支持需要 .NET 4.5。 |
> | 实体框架5 |  |
> | [Windows Azure SDK 2。1](https://go.microsoft.com/fwlink/p/?linkid=323511) | 如果你跳过 Windows Azure 部署步骤，则不需要 SDK。 发布新版本的 SDK 时，该链接将安装较新版本。 在这种情况下，你可能需要将一些说明调整为新的 UI 和功能。 |
> 
> ## <a name="questions"></a>问题
> 
> 如果你有与本教程不直接相关的问题，则可以将其发布到 [ASP.NET 实体框架论坛](https://forums.asp.net/1227.aspx)、 [实体框架和 LINQ to Entities 论坛](https://social.msdn.microsoft.com/forums/adodotnetentityframework/threads/)，或 [StackOverflow.com](http://stackoverflow.com/)。
> 
> ## <a name="acknowledgments"></a>致谢
> 
> 请参阅 "确认" 系列中的最后一个教程 [，并查看有关 VB 的注释](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#acknowledgments)。
> 
> ## <a name="original-version-of-the-tutorial"></a>教程的原始版本
> 
> [EF 4.1/MVC 3 电子书](https://social.technet.microsoft.com/wiki/contents/articles/11608.e-book-gallery-for-microsoft-technologies.aspx#GettingStartedwiththeEntityFramework4.1usingASP.NETMVC)中提供了本教程的原始版本。

## <a name="the-contoso-university-web-application"></a>Contoso 大学 Web 应用程序

你将在这些教程中学习构建一个简单的大学网站的应用程序。

用户可以查看和更新学生、 课程和教师信息。 以下是一些你即将创建的页面。

![Students_Index_page](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image1.png)

![](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image2.png)

本教程主要关注于如何使用 Entity Framework , 所以此站点的UI样式都是直接套用内置的模板。

## <a name="prerequisites"></a>先决条件

本教程中的说明和屏幕截图假设你使用的是 [Visual studio 2012](https://www.microsoft.com/visualstudio/eng/downloads) 或 [Visual studio 2012 Express for Web](https://go.microsoft.com/fwlink/?LinkID=275131)，其中安装了最新的更新和 Azure SDK for .Net，截止到7月2013。 可以通过以下链接获取所有这些内容：

[适用于 .NET 的 Azure SDK (Visual Studio 2012) ](https://go.microsoft.com/fwlink/?LinkId=254364)

如果安装了 Visual Studio，上面的链接将安装任何缺少的组件。 如果没有 Visual Studio，此链接将安装 Visual Studio 2012 Express for Web。 您可以使用 Visual Studio 2013，但某些必需的过程和屏幕会有所不同。

## <a name="create-an-mvc-web-application"></a>创建 MVC Web 应用程序

使用 **ASP.NET MVC 4 Web 应用程序** 模板打开 Visual Studio 并创建一个名为 "ContosoUniversity" 的新 c # 项目。 请确保目标 **.NET Framework 4.5** (你将使用 [ `enum` 属性](https://msdn.microsoft.com/data/hh859576.aspx)，这需要 .net 4.5) 。

![New_project_dialog_box](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image3.png)

在 " **新建 ASP.NET MVC 4 项目** " 对话框中，选择 " **Internet 应用程序** " 模板。

选择 " **Razor** " 视图引擎，并选中 " **创建单元测试项目** " 复选框。

单击“确定”。

![Project_template_options](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image4.png)

## <a name="set-up-the-site-style"></a>设置站点样式

通过几个简单的更改设置站点菜单、 布局和主页。

打开 *Views\Shared \\ _Layout*，并将该文件的内容替换为以下代码。 突出显示所作更改。

[!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample1.cshtml?highlight=5,15,25-28,43)]

此代码会更改以下内容：

- 将 "我的 ASP.NET MVC 应用程序" 和 "你的徽标" 的模板实例替换为 "Contoso 大学"。
- 添加几个操作链接，稍后将在本教程中使用。

在 *Views\Home\Index.cshtml* 中，将该文件的内容替换为以下代码，以消除有关 ASP.NET 和 MVC 的模板段落：

[!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample2.cshtml)]

在 *Controllers\HomeController.cs* 中，将 " `ViewBag.Message` 操作" 方法中的值更改 `Index` 为 "欢迎使用 Contoso 大学！"，如以下示例中所示：

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample3.cs?highlight=3)]

按 CTRL + F5 运行该站点。 你将看到带有主菜单的主页。

![Contoso_University_home_page](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image5.png)

## <a name="create-the-data-model"></a>创建数据模型

接下来你将创建 Contoso 大学应用程序的实体类。 你将从以下三个实体开始：

![Class_diagram](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image6.png)

`Student` 和 `Enrollment`实体之间是一对多的关系，`Course` 和`Enrollment` 实体之间也是一个对多的关系。 换而言之，一名学生可以修读任意数量的课程, 并且某一课程可以被任意数量的学生修读。

接下来，你将创建与这些实体对应的类。

> [!NOTE]
> 如果尝试在完成所有这些实体类的创建之前编译项目，将会出现编译器错误。

### <a name="the-student-entity"></a>Student 实体

![Student_entity](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image7.png)

在 " *模型* " 文件夹中，创建 *Student.cs* ，并将现有代码替换为以下代码：

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample4.cs)]

`StudentID` 属性将成为对应于此类的数据库表中的主键。 默认情况下，实体框架会将名为或类名为的属性解释 `ID`  `ID` 为主键。

`Enrollments` 属性是 *导航属性*。 导航属性中包含与此实体相关的其他实体。 在这种情况下， `Enrollments` 实体的属性 `Student` 将包含 `Enrollment` 与该实体相关的所有实体 `Student` 。 换言之，如果数据库中的给定 `Student` 行有两个相关 `Enrollment` 行 (包含其外键列中该学生的主键值的行 `StudentID`) ，则该 `Student` 实体的 `Enrollments` 导航属性将包含这两个 `Enrollment` 实体。

通常将导航属性定义为， `virtual` 以便可以利用某些实体框架功能，如 *延迟加载*。 稍后将在本系列的 " [读取相关数据](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) " 教程中介绍 (延迟加载。

如果导航属性可以具有多个实体 （如多对多或一对多关系），那么导航属性的类型必须是可以添加、 删除和更新条目的容器，如 `ICollection`。

### <a name="the-enrollment-entity"></a>注册实体

![Enrollment_entity](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image8.png)

在 *Models* 文件夹中，创建 *Enrollment.cs* 并且用以下代码替换现有代码：

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample5.cs)]

评分属性是一个 [枚举](https://msdn.microsoft.com/data/hh859576.aspx)。 `Grade` 声明类型后的`?`表示 `Grade` 属性可以为 [null](https://msdn.microsoft.com/library/2cf62fcy.aspx)。 Null 的级别不同于零级别，null 表示分数未知或尚未赋值。

`StudentID` 属性是一个外键，`Student` 是与其且对应的导航属性。 `Enrollment` 实体与一个 `Student` 实体相关联，因此该属性只包含单个 `Student` 实体 (与前面所看到的 `Student.Enrollments` 导航属性不同后，`Student`中可以容纳多个 `Enrollment` 实体)。

`CourseID` 属性是一个外键， `Course` 是与其对应的导航属性。 `Enrollment` 实体与一个 `Course` 实体相关联。

### <a name="the-course-entity"></a>Course 实体

![Course_entity](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image9.png)

在 " *模型* " 文件夹中，创建 *Course.cs*，并将现有代码替换为以下代码：

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample6.cs)]

`Enrollments` 属性是导航属性。 `Course` 实体可与任意数量的 `Enrollment` 实体相关。

我们将详细介绍 [[DatabaseGenerated](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.databasegeneratedattribute(v=vs.110).aspx) ([DatabaseGeneratedOption](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.databasegeneratedoption(v=vs.95).aspx)。下一教程中无) ] 特性。 简单来说，此特性让你能自行指定主键，而不是让数据库自动指定主键。

## <a name="create-the-database-context"></a>创建数据库上下文

为给定数据模型协调实体框架功能的主类是 *数据库上下文* 类。 可以通过从 [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=VS.103).aspx) 类派生来创建此类。 在该类中你可以指定数据模型中包含哪些实体。 你还可以定义某些 Entity Framework 行为。 在此项目中将数据库上下文类命名为 `SchoolContext`。

为数据访问层) 创建一个名为 *DAL* (的文件夹。 在该文件夹中，创建一个名为 *SchoolContext.cs* 的新类文件，并将现有代码替换为以下代码：

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample7.cs)]

此代码为每个实体集创建一个 [DbSet](https://msdn.microsoft.com/library/system.data.entity.dbset(v=VS.103).aspx) 属性。 在实体框架术语中， *实体集* 通常对应于数据库表， *实体* 对应于表中的行。

`modelBuilder.Conventions.Remove` [OnModelCreating](https://msdn.microsoft.com/library/system.data.entity.dbcontext.onmodelcreating(v=vs.103).aspx)方法中的语句阻止复数表名称。 如果未执行此操作，则生成的表将被命名为 `Students` 、 `Courses` 和 `Enrollments` 。 相反，表名称将为 `Student` 、 `Course` 和 `Enrollment` 。 开发者对表名称是否应为复数意见不一。 本教程使用单数形式，但重要的是，您可以选择您喜欢的任何形式，包括或省略此行代码。

## <a name="sql-server-express-localdb"></a>SQL Server Express LocalDB

[LocalDB](https://blogs.msdn.com/b/sqlexpress/archive/2011/07/12/introducing-localdb-a-better-sql-express.aspx) 是按需启动并在用户模式下运行的 SQL Server Express 数据库引擎的轻型版本。 LocalDB 在 SQL Server Express 的特殊执行模式下运行，该模式使您能够将数据库用作 *.mdf* 文件。 通常，LocalDB 数据库文件保存在 web 项目的 *应用程序 \_ 数据* 文件夹中。 使用 SQL Server Express 中的用户实例功能，还可以使用 *.mdf* 文件，但不推荐使用用户实例功能;因此，建议使用 LocalDB 来处理 *.mdf* 文件。

通常 SQL Server Express 不用于生产 web 应用程序。 不建议将 LocalDB 特别用于 web 应用程序，因为它不能与 IIS 一起使用。

在 Visual Studio 2012 及更高版本中，默认情况下使用 Visual Studio 安装 LocalDB。 在 Visual Studio 2010 及更早版本中，默认情况下，在 Visual Studio 中安装 SQL Server Express () 如果使用的是 Visual Studio 2010，则必须手动安装。

在本教程中，你将使用 LocalDB，以便可以将数据库以 *.mdf* 文件的形式存储在 *应用 \_ 数据* 文件夹中。 打开根 *Web.config* 文件，将新的连接字符串添加到 `connectionStrings` 集合中，如下面的示例中所示。  (确保更新根项目文件夹中的 *Web.config* 文件。 还有一个 *Web.config* 文件位于不需要更新的 *Views* 子文件夹中。 ) 

[!code-xml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample8.xml)]

默认情况下，实体框架会查找名称与 `DbContext` 此项目) 的类 (相同的连接字符串 `SchoolContext` 。 添加的连接字符串指定了位于 *应用 \_ 数据* 文件夹中名为 *ContosoUniversity* 的 LocalDB 数据库。 有关详细信息，请参阅 [SQL Server ASP.NET Web 应用程序的连接字符串](https://msdn.microsoft.com/library/jj653752.aspx)。

实际上不需要指定连接字符串。 如果你没有提供连接字符串，实体框架将为你创建一个;但是，数据库可能不在应用的 *应用 \_ 数据* 文件夹中。 有关将创建数据库的位置的信息，请参阅 [Code First 到新数据库](https://msdn.microsoft.com/data/jj193542)。

该 `connectionStrings` 集合还具有一个名为的连接字符串， `DefaultConnection` 用于成员资格数据库。 在本教程中，您不会使用成员资格数据库。 这两个连接字符串之间唯一的区别是数据库名称和 name 属性值。

## <a name="set-up-and-execute-a-code-first-migration"></a>设置并执行 Code First 迁移

首次开始开发应用程序时，数据模型会频繁更改，每次模型更改时，模型都不会与数据库同步。 您可以将实体框架配置为每次更改数据模型时自动删除并重新创建数据库。 这并不是在开发初期发生的问题，因为可以轻松地重新创建测试数据，但在将其部署到生产环境后，通常需要更新数据库架构，而不会删除数据库。 迁移功能使 Code First 可以更新数据库，而无需删除并重新创建数据库。 在新项目的开发周期初期，你可能想要使用 [DropCreateDatabaseIfModelChanges](https://msdn.microsoft.com/library/gg679604(v=vs.103).aspx) 在每次模型更改时，重新创建数据库并对其进行种子设定。 可以在部署应用程序时将其转换为迁移方法。 对于本教程，只需使用迁移。 有关详细信息，请参阅 [Code First 迁移](https://msdn.microsoft.com/data/jj591621) 和 [迁移 Screencast 系列](https://blogs.msdn.com/b/adonet/archive/2014/03/12/migrations-screencast-series.aspx)。

### <a name="enable-code-first-migrations"></a>启用 Code First 迁移

1. 在“工具”菜单中，单击“NuGet 包管理器”，然后单击“包管理器控制台”。

    ![Selecting_Package_Manager_Console](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image10.png)
2. 在 `PM>` 提示符下，输入以下命令：

    [!code-powershell[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample9.ps1)]

    ![启用-迁移命令](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image11.png)

    此命令将在 ContosoUniversity 项目中创建一个 " *迁移* " 文件夹，并在该文件夹中放入一个 *Configuration.cs* 文件，你可以编辑该文件来配置迁移。

    ![迁移文件夹](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image12.png)

    `Configuration`类包含一个 `Seed` 方法，该方法在数据库创建时调用，每次在数据模型更改后更新。

    [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample10.cs)]

    此方法的目的 `Seed` 是使你能够在 Code First 创建测试数据或更新该数据后将其插入到数据库中。

### <a name="set-up-the-seed-method"></a>设置种子方法

当 Code First 迁移创建数据库时， [Seed](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx) 方法将运行，并且每次将数据库更新到最新迁移时都会运行。 Seed 方法的用途是使你能够在应用程序首次访问数据库之前将数据插入表中。

在早期版本的 Code First 中，在发布迁移之前，通常会有 `Seed` 方法插入测试数据，因为在开发过程中每个模型更改都必须完全删除并从头开始重新创建。 在 Code First 迁移的情况下，在数据库更改后会保留测试数据，因此通常不需要在 [Seed](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx) 方法中包括测试数据。 事实上， `Seed` 如果您将使用迁移将数据库部署到生产环境，则不希望该方法插入测试数据，因为该 `Seed` 方法将在生产环境中运行。 在这种情况下，你希望 `Seed` 方法仅将你要在生产中插入的数据插入到数据库中。 例如， `Department` 当应用程序在生产中可用时，您可能希望数据库包括表中的实际部门名称。

对于本教程，你将使用迁移进行部署，但你的 `Seed` 方法将插入测试数据，以便更轻松地了解应用程序功能的工作方式，而无需手动插入大量数据。

1. 将 *Configuration.cs* 文件的内容替换为以下代码，该代码会将测试数据加载到新数据库中。 

    [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample11.cs)]

    [Seed](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx)方法采用数据库上下文对象作为输入参数，方法中的代码使用该对象将新实体添加到数据库中。 对于每个实体类型，代码将创建新实体的集合，将其添加到相应的 [DbSet](https://msdn.microsoft.com/library/system.data.entity.dbset(v=vs.103).aspx) 属性，然后将更改保存到数据库。 不需要在每个实体组后调用 [SaveChanges](https://msdn.microsoft.com/library/system.data.entity.dbcontext.savechanges(v=VS.103).aspx) 方法，这一点在此完成，但这样做可帮助您找到问题的根源（如果代码写入数据库时出现异常）。

    插入数据的某些语句使用 [AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) 方法执行 "upsert" 操作。 由于 `Seed` 方法在每次迁移时都运行，因此不能只插入数据，因为在第一个创建数据库的迁移之后，尝试添加的行已存在。 如果尝试插入已存在的行，"upsert" 操作将会阻止发生的错误，但会 ***覆盖*** 在测试应用程序时对数据所做的任何更改。 对于某些表中的测试数据，您可能不希望发生这种情况：在某些情况下，当您在测试时更改数据时，您希望在数据库更新后更改保持不变。 在这种情况下，需要执行条件插入操作：仅在不存在行时插入行。 Seed 方法使用这两种方法。

    传递给 [AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) 方法的第一个参数指定要用于检查行是否已存在的属性。 对于所提供的测试学生数据， `LastName` 属性可用于此目的，因为列表中的每个姓氏都是唯一的：

    [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample12.cs)]

    此代码假定姓氏是唯一的。 如果你手动添加了姓氏重复的学生，你将在下一次执行迁移时收到以下例外。

    序列包含多个元素

    有关方法的详细信息 `AddOrUpdate` ，请参阅 Julie Lerman 的博客上的 [EF 4.3 AddOrUpdate 方法](http://thedatafarm.com/blog/data-access/take-care-with-ef-4-3-addorupdate-method/) 。

    添加实体的代码 `Enrollment` 不使用 `AddOrUpdate` 方法。 它将检查实体是否已存在，如果实体不存在，则插入该实体。 此方法将保留在迁移运行时对注册等级所做的更改。 代码遍历列表中的每个成员 `Enrollment` [](https://msdn.microsoft.com/library/6sh2ey19.aspx) ，如果未在数据库中找到注册，则会将注册添加到数据库中。 第一次更新数据库时，该数据库将为空，因此将添加每个注册。

    [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample13.cs)]

    有关如何调试 `Seed` 方法以及如何处理冗余数据（如名为 "Alexander Carson" 的两名学生）的信息，请参阅 Rick Anderson 博客上的 [ (EF) Db 的种子设定和调试实体框架](https://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx) 。
2. 生成项目。

### <a name="create-and-execute-the-first-migration"></a>创建和执行第一次迁移

1. 在 "程序包管理器控制台" 窗口中，输入以下命令： 

    [!code-powershell[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample14.ps1)]

    ![](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image13.png)

    `add-migration`命令向迁移文件夹添加一个包含用于创建数据库的代码的 *[日期戳] \_ InitialCreate.cs* 文件。 第一个参数 (`InitialCreate)` 用于文件名，可以是任何所需的参数; 通常选择一个词或短语，用于汇总在迁移中所执行的操作。 例如，你可以命名以后的迁移 &quot; AddDepartmentTable &quot; 。

    ![具有初始迁移的迁移文件夹](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image14.png)

    `Up`类的方法 `InitialCreate` 创建与数据模型实体集相对应的数据库表，方法将 `Down` 删除这些表。 迁移调用 `Up` 方法为迁移实现数据模型更改。 输入用于回退更新的命令时，迁移调用 `Down` 方法。 以下代码显示了该文件的内容 `InitialCreate` ：

    [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample15.cs)]

    该 `update-database` 命令运行 `Up` 方法来创建数据库，然后运行 `Seed` 方法来填充数据库。

现在，已为你的数据模型创建了一个 SQL Server 的数据库。 数据库的名称为 *ContosoUniversity*， *.mdf* 文件位于项目的 *应用 \_ 数据* 文件夹中，因为这是在连接字符串中指定的内容。

您可以使用 **服务器资源管理器** 或 **SQL Server 对象资源管理器** (SSOX) 来查看 Visual Studio 中的数据库。 对于本教程，你将使用 **服务器资源管理器**。 在 Visual Studio Express 2012 for Web 中， **服务器资源管理器** 称为 **数据库资源管理器**。

1. 在 " **视图** " 菜单上，单击 **服务器资源管理器**。
2. 单击 " **添加连接** " 图标。

    ![](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image15.png)
3. 如果系统提示 " **选择数据源** " 对话框，请单击 " **Microsoft SQL Server**"，然后单击 " **继续**"。  
  
    ![](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image16.png)
4. 在 "**添加连接**" 对话框中，输入 **服务器名称** **(localdb) \v11.0** 。 在 " **选择或输入数据库名称**" 下，选择 " **ContosoUniversity"。**  
  
    ![](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image17.png)
5. 单击“确定” **。**
6. 展开 " **SchoolContext** "，然后展开 " **表**"。  
  
    ![](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image18.png)
7. 右键单击 **Student** 表，然后单击 " **显示表数据** "，查看已创建的列和插入到该表中的行。

    ![学生表](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image19.png)

## <a name="creating-a-student-controller-and-views"></a>创建学生控制器和视图

下一步是在应用程序中创建一个 ASP.NET MVC 控制器和一个可用于这些表的视图。

1. 若要创建 `Student` 控制器，请在 **解决方案资源管理器** 中右键单击 "**控制器**" 文件夹，选择 "**添加**"，然后单击 "**控制器**"。 在 " **添加控制器** " 对话框中，进行以下选择，然后单击 " **添加**"： 

   - 控制器名称： **StudentController**。
   - 模板： **包含读/写操作和视图的 MVC 控制器，使用实体框架**。
   - Model 类： **学生 (ContosoUniversity)**。  (如果未在下拉列表中看到此选项，请生成项目，然后重试。 ) 
   - 数据上下文类： **SchoolContext (ContosoUniversity)**。
   - 视图： **Razor (CSHTML)**。  (默认值。 ) 

     ![Add_Controller_dialog_box_for_Student_controller](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image20.png)
2. Visual Studio 将打开 *Controllers\StudentController.cs* 文件。 你会看到已创建实例化数据库上下文对象的类变量：

     [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample16.cs)]

     `Index`操作方法通过读取数据库上下文实例的属性，从 *学生* 实体集中获取学生列表 `Students` 。

     [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample17.cs)]

     *Student\Index.cshtml* 视图将此列表显示在表中：

     [!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample18.cshtml)]
3. 按 Ctrl+F5 运行项目。

     单击 " **学生** " 选项卡以查看该方法插入的测试数据 `Seed` 。

     ![学生索引页](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image21.png)

## <a name="conventions"></a>约定

为了使实体框架能够为你创建完整数据库而必须编写的代码量最少，因为使用了 *约定*，或者实体框架进行了假设。 其中一些已被注明：

- 实体类名称的复数形式用作表名称。
- 使用实体属性名作为列名。
- 命名为或 classname 的实体属性被 `ID`  `ID` 识别为主键属性。

您已看到，可以 (重写约定，例如，您指定了表名不应为复数) ，您将了解有关约定的详细信息，以及如何在本系列后面的 [创建更复杂的数据模型](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md) 教程中替代它们。 有关详细信息，请参阅 [Code First 约定](https://msdn.microsoft.com/data/jj679962)。

## <a name="summary"></a>总结

你现在已创建了一个使用实体框架和 SQL Server Express 来存储和显示数据的简单应用程序。 在以下教程中，你将了解如何执行基本的 CRUD (创建、读取、更新、删除) 操作。 你可以在此页的底部留下反馈。 请告诉我们你对此部分教程的理解，以及我们如何改进本教程。

可在 [ASP.NET 数据访问内容映射](../../../../whitepapers/aspnet-data-access-content-map.md)中找到指向其他实体框架资源的链接。

> [!div class="step-by-step"]
> [下一页](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)

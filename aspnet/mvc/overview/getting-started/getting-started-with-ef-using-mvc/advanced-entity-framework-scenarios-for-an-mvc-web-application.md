---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application
title: 教程：了解 MVC 5 Web 应用的高级 EF 方案
description: 本教程介绍了几个主题，这些主题可帮助你了解开发使用实体框架 Code First 的 ASP.NET web 应用程序的基础知识。
author: tdykstra
ms.author: riande
ms.date: 01/22/2019
ms.topic: tutorial
ms.assetid: f35a9b0c-49ef-4cde-b06d-19d1543feb0b
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application
msc.type: authoredcontent
ms.openlocfilehash: 2bfa4401c73b56be87502ffbb189abab3c59c226
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89044995"
---
# <a name="tutorial-learn-about-advanced-ef-scenarios-for-an-mvc-5-web-app"></a>教程：了解 MVC 5 Web 应用的高级 EF 方案

在上一教程中，您实现了每个层次结构一个表继承。 本教程介绍了几个主题，这些主题可帮助你了解开发使用实体框架 Code First 的 ASP.NET web 应用程序的基础知识。 前几部分都提供了分步说明，指导你完成代码并使用 Visual Studio 完成任务。下面的部分将介绍几个主题，其中包含简短的简介，并提供有关详细信息的资源链接。

对于大多数这些主题，你将使用已创建的页面。 若要使用原始 SQL 执行批量更新，您将创建一个新页，用于更新数据库中所有课程的信用额度：

![Update_Course_Credits_initial_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image1.png)

在本教程中，你将了解：

> [!div class="checklist"]
> * 执行原始 SQL 查询
> * 执行无跟踪查询
> * 检查发送到数据库的 SQL 查询

你还将了解：

> [!div class="checklist"]
> * 创建抽象层
> * 代理类
> * 自动脏值检测
> * 自动验证
> * 实体框架 Power Tools
> * 实体框架源代码

## <a name="prerequisite"></a>先决条件

* [实现继承](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="perform-raw-sql-queries"></a>执行原始 SQL 查询

实体框架 Code First API 包括使你能够将 SQL 命令直接传递到数据库的方法。 你有以下选择：

- 对于返回实体类型的查询，请使用 [DbSet. SqlQuery](https://msdn.microsoft.com/library/system.data.entity.dbset.sqlquery.aspx) 方法。 返回的对象必须是对象所需的类型 `DbSet` ，并且数据库上下文会自动跟踪这些对象，除非关闭跟踪。  (参见以下有关 [AsNoTracking](https://msdn.microsoft.com/library/system.data.entity.dbextensions.asnotracking.aspx) 方法的部分。 ) 
- 对于返回非实体类型的查询，请使用 [SqlQuery](https://msdn.microsoft.com/library/system.data.entity.database.sqlquery.aspx) 方法。 数据库上下文不会跟踪返回的数据，即使你使用该方法来检索实体类型也是如此。
- 将 [Database.ExecuteSqlCommand](https://msdn.microsoft.com/library/gg679456.aspx) 用于非查询命令。

使用 Entity Framework 的优点之一是它可避免你编写跟数据库过于耦合的代码 它会自动生成 SQL 查询和命令，使得你无需自行编写。 但在某些情况下，你需要运行已手动创建的特定 SQL 查询，并且这些方法使你能够处理此类异常。

在 Web 应用程序中执行 SQL 命令时，请务必采取预防措施来保护站点免受 SQL 注入攻击。 一种方法是使用参数化查询，确保不会将网页提交的字符串视为 SQL 命令。 在本教程中，将用户输入集成到查询中时会使用参数化查询。

### <a name="calling-a-query-that-returns-entities"></a>调用返回实体的查询

[DbSet &lt; &gt; TEntity](https://msdn.microsoft.com/library/gg696460.aspx)类提供一个方法，该方法可用于执行返回类型为的实体的查询 `TEntity` 。 若要查看其工作原理，请更改控制器的方法中的代码 `Details` `Department` 。

在 *DepartmentController.cs*中，在 `Details` 方法中，将 `db.Departments.FindAsync` 方法调用替换为 `db.Departments.SqlQuery` 方法调用，如以下突出显示的代码所示：

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample1.cs?highlight=8-14)]

为了验证新代码是否正常工作，请选择“院系”选项卡，然后选择其中某一院系的“详细信息” 。 确保所有数据都按预期方式显示。

### <a name="calling-a-query-that-returns-other-types-of-objects"></a>调用返回其他类型对象的查询

之前你在“关于”页面创建了一个学生统计信息网格，显示每个注册日期的学生数量。 在 *HomeController.cs* 中执行此操作的代码使用 LINQ：

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample2.cs)]

假设您要编写在 SQL 中直接检索此数据的代码，而不是使用 LINQ。 为此，您需要运行一个返回除 entity 对象之外的内容的查询，这意味着您需要使用 [SqlQuery](https://msdn.microsoft.com/library/system.data.entity.database.sqlquery(v=VS.103).aspx) 方法。

在 *HomeController.cs*中，将方法中的 LINQ 语句替换为 `About` SQL 语句，如以下突出显示的代码所示：

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample3.cs?highlight=3-18)]

运行 "关于" 页。 验证它是否显示与以前相同的数据。

### <a name="calling-an-update-query"></a>调用更新查询

假设 Contoso 大学管理员希望能够在数据库中执行大容量更改，如更改每个课程的信用额度。 如果该大学提供了大量课程，那么将所有课程作为实体来检索并单独更改就非常低效。 在本节中，您将实现一个网页，该网页使用户能够指定更改所有课程的信用额度的因素，并通过执行 SQL 语句进行更改 `UPDATE` 。 

在 *CourseController.cs*中， `UpdateCourseCredits` 为和添加方法 `HttpGet` `HttpPost` ：

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample4.cs)]

当控制器处理请求时 `HttpGet` ，变量中将不会返回任何内容 `ViewBag.RowsAffected` ，并且该视图将显示一个空的文本框和一个提交按钮。

单击 " **更新** " 按钮时，将 `HttpPost` 调用方法，并在 `multiplier` 文本框中输入值。 然后，该代码执行更新课程的 SQL，并将受影响的行数返回到变量中的视图 `ViewBag.RowsAffected` 。 当视图获取该变量中的值时，它将显示更新的行数，而不是文本框和提交按钮。

在 *CourseController.cs*中，右键单击其中一个 `UpdateCourseCredits` 方法，然后单击 " **添加视图**"。 此时将显示 " **添加视图** " 对话框。 保留默认值，然后选择 " **添加**"。

在 *Views\Course\UpdateCourseCredits.cshtml*中，将模板代码替换为以下代码：

[!code-cshtml[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample5.cshtml)]

通过选择**Courses**选项卡运行`UpdateCourseCredits`方法，然后在浏览器地址栏中 URL 的末尾添加"/ UpdateCourseCredits"到 (例如： `http://localhost:50205/Course/UpdateCourseCredits`)。 在文本框中输入数字：

![Update_Course_Credits_initial_page_with_2_entered](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image1.png)

单击“更新”。 你会看到受影响的行数。

单击“返回列表”可以查看课程列表，其中学分已替换为修改后的数字。

有关原始 SQL 查询的详细信息，请参阅 MSDN 上的 [原始 Sql 查询](https://msdn.microsoft.com/data/jj592907) 。

## <a name="no-tracking-queries"></a>非跟踪查询

当数据库上下文检索表行并创建表示它们的实体对象时，默认情况下，它会跟踪内存中的实体是否与数据库中的内容同步。 更新实体时，内存中的数据充当缓存并使用该数据。 在 Web 应用程序中，此缓存通常是不必要的，因为上下文实例通常生存期较短（创建新的实例并用于处理每个请求），并且通常在再次使用该实体之前处理读取实体的上下文。

您可以使用 [AsNoTracking](https://msdn.microsoft.com/library/gg679352(v=vs.103).aspx) 方法禁用内存中实体对象的跟踪。 可能想要执行的典型方案包括以下操作：

- 查询检索到关闭跟踪可能会明显提高性能的大量数据。
- 您希望附加实体以便对其进行更新，但您之前检索到不同用途的同一实体。 由于数据库上下文已跟踪了该实体，因此无法附加要更改的实体。 解决这种情况的一种方法是将 `AsNoTracking` 选项与前面的查询一起使用。

有关演示如何使用 [AsNoTracking](https://msdn.microsoft.com/library/gg679352(v=vs.103).aspx) 方法的示例，请参阅 [本教程的早期版本](../../older-versions/getting-started-with-ef-5-using-mvc-4/advanced-entity-framework-scenarios-for-an-mvc-web-application.md)。 此版本的教程不会在编辑方法中对已创建模型联编程序的实体设置修改标志，因此不需要 `AsNoTracking` 。

## <a name="examine-sql-sent-to-database"></a>检查发送到数据库的 SQL

有时能够以查看发送到数据库的实际 SQL 查询对于开发者来说是很有用的。 在前面的教程中，你已了解如何在侦听器代码中执行此操作;现在，你将看到一些无需编写侦听器代码即可执行此操作的方法。 若要尝试此操作，你将看到一个简单的查询，然后在你添加预先加载、筛选和排序选项时，查看该查询所发生的情况。

在 controller */CourseController*中，将 `Index` 方法替换为以下代码，以便暂时停止预先加载：

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample6.cs)]

现在，在语句上设置一个断点 `return` (F9，并将光标置于该行) 上。 按 **F5** 在调试模式下运行项目，然后选择 "课程索引" 页。 当代码到达断点时，检查 `sql` 变量。 你会看到发送到 SQL Server 的查询。 这是一个简单的 `Select` 语句。

[!code-json[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample7.sql)]

单击放大镜可查看 **文本可视化工具**中的查询。

![](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image10.png)

现在，你将向 "课程索引" 页添加一个下拉列表，以便用户可以筛选特定部门。 您将按标题对课程进行排序，并指定预先加载 `Department` 导航属性。

在 *CourseController.cs*中，将 `Index` 方法替换为以下代码：

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample8.cs)]

还原语句上的断点 `return` 。

方法接收参数中下拉列表的选定值 `SelectedDepartment` 。 如果未选择任何内容，则此参数将为 null。

将 `SelectList` 包含所有部门的集合传递给下拉列表的视图。 传递给 `SelectList` 构造函数的参数指定值字段名称、文本字段名称和选定项。

对于 `Get` 存储库的方法 `Course` ，代码指定筛选器表达式、排序顺序以及预先加载 `Department` 导航属性。 `true`如果未在下拉列表中选择任何内容，则筛选表达式始终返回 (即 `SelectedDepartment` 为 null) 。

在 *Views\Course\Index.cshtml*中，紧跟在开始 `table` 标记之前，添加以下代码以创建下拉列表和 "提交" 按钮：

[!code-cshtml[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample9.cshtml)]

仍设置断点后，运行 "课程索引" 页。 在代码第一次命中断点时继续，以便在浏览器中显示该页。 从下拉列表中选择一个部门，然后单击 " **筛选器**"。

这次，第一个断点将用于下拉列表的部门查询。 跳过该操作，并在 `query` 下一次代码到达断点时查看变量，以便查看 `Course` 查询现在的外观。 你将看到如下所示的内容：

[!code-sql[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample10.sql)]

您可以看到，该查询现在是一个 `JOIN` 查询，该查询将 `Department` 数据与 `Course` 数据一起加载，并且它包含一个 `WHERE` 子句。

删除 `var sql = courses.ToString()` 行。

## <a name="create-an-abstraction-layer"></a>创建抽象层

许多开发人员编写代码实现存储库和工作模式单元以作为使用 Entity Framework 代码的包装器。 这些模式用于在应用程序的数据访问层和业务逻辑层之间创建抽象层。 实现这些模式可让你的应用程序对数据存储介质的更改不敏感，而且很容易进行自动化单元测试和进行测试驱动开发 (TDD)。 不过，出于以下几个原因，编写附加代码来实现这些模式并非总是最佳选择：

- EF 上下文类可以为使用 EF 的数据库更新充当工作单位类。
- 对于使用 EF 进行的数据库更新，EF 上下文类可充当工作单元类。
- 实体框架6中引入的功能使得无需编写存储库代码即可更轻松地实现 TDD。

有关如何实现存储库和工作单元模式的详细信息，请参阅 [本系列教程的实体框架5版本](../../older-versions/getting-started-with-ef-5-using-mvc-4/implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md)。 有关在实体框架6中实现 TDD 的方式的信息，请参阅以下资源：

- [EF6 如何更轻松地启用模拟 Dbset](http://thedatafarm.com/data-access/how-ef6-enables-mocking-dbsets-more-easily/)
- [使用模拟框架进行测试](https://msdn.microsoft.com/data/dn314429)
- [用自己的测试进行测试双精度](https://msdn.microsoft.com/data/dn314431)

<a id="proxies"></a>

## <a name="proxy-classes"></a>代理类

如果实体框架创建实体实例 (例如，在执行查询) 时，它通常会将其创建为作为实体代理的动态生成的派生类型的实例。 例如，请参阅以下两个调试器映像。 在第一个图像中，你会看到在 `student` `Student` 实例化实体后，变量是预期类型。 在第二个图中，使用 EF 从数据库中读取 student 实体后，会看到代理类。

![代理类之前](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image12.png)

![代理类之后](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image13.png)

此代理类将重写实体的某些虚拟属性，以插入挂钩，以便在访问属性时自动执行操作。 此机制用于的一个函数是延迟加载。

大多数情况下，无需注意代理的这种使用，但有一些例外：

- 在某些情况下，你可能想要阻止实体框架创建代理实例。 例如，在序列化实体时，通常需要 POCO 类，而不是代理类。 避免序列化问题的一种方法是将数据传输对象序列化 (Dto) 而不是实体对象，如 [使用带有实体框架的 WEB API](../../../../web-api/overview/data/using-web-api-with-entity-framework/part-1.md) 教程中所示。 另一种方法是 [禁用代理创建](https://msdn.microsoft.com/data/jj592886.aspx)。
- 如果使用运算符实例化实体类 `new` ，则不会获得代理实例。 这意味着不会获得延迟加载和自动更改跟踪等功能。 这通常是正常的;通常不需要延迟加载，因为你要创建的是不在数据库中的新实体，并且如果你将实体显式标记为，则通常不需要更改跟踪 `Added` 。 但是，如果确实需要延迟加载并且需要更改跟踪，则可以使用类的 [create](https://msdn.microsoft.com/library/gg679504.aspx) 方法创建新的实体实例，其中包含代理 `DbSet` 。
- 你可能需要从代理类型获取实际的实体类型。 您可以使用类的 [GetObjectType](https://msdn.microsoft.com/library/system.data.objects.objectcontext.getobjecttype.aspx) 方法 `ObjectContext` 来获取代理类型实例的实际实体类型。

有关详细信息，请参阅 MSDN 上 [的使用代理](https://msdn.microsoft.com/data/JJ592886.aspx) 。

## <a name="automatic-change-detection"></a>自动脏值检测

Entity Framework 通过比较的实体的当前值与原始值来判断更改实体的方式 （因此需要发送更新到数据库）。 查询或附加该实体时会存储的原始值。 如下方法会导致自动脏值：

- `DbSet.Find`
- `DbSet.Local`
- `DbSet.Remove`
- `DbSet.Add`
- `DbSet.Attach`
- `DbContext.SaveChanges`
- `DbContext.GetValidationErrors`
- `DbContext.Entry`
- `DbChangeTracker.Entries`

如果正在跟踪大量实体，并且在循环中多次调用这些方法之一，则使用 [AutoDetectChangesEnabled](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.autodetectchangesenabled.aspx) 属性暂时关闭自动更改检测可能会显著提高性能。 有关详细信息，请参阅 MSDN 上的 [自动检测更改](https://msdn.microsoft.com/data/jj556205) 。

## <a name="automatic-validation"></a>自动验证

在调用方法时 `SaveChanges` ，默认情况下，实体框架在更新数据库之前验证所有已更改实体的所有属性中的数据。 如果已更新大量实体，并且已验证数据，则不需要执行此操作，并且可以通过暂时关闭验证来使保存更改的过程更少。 可以使用 [ValidateOnSaveEnabled](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.validateonsaveenabled.aspx) 属性执行此操作。 有关详细信息，请参阅 MSDN 上的 [验证](https://msdn.microsoft.com/data/gg193959) 。

## <a name="entity-framework-power-tools"></a>实体框架 Power Tools

[实体框架 Power Tools](https://marketplace.visualstudio.com/items?itemName=ErikEJ.EntityFramework6PowerToolsCommunityEdition) 是一个 Visual Studio 外接程序，用于创建这些教程中所示的数据模型图。 这些工具还可以执行其他功能，例如基于现有数据库中的表生成实体类，以便可以将数据库与 Code First 一起使用。 安装这些工具后，上下文菜单中将显示一些附加选项。 例如，在 **解决方案资源管理器**中右键单击上下文类时，将看到和 **实体框架** 选项。 这使您能够生成关系图。 使用时 Code First 无法更改关系图中的数据模型，但可以移动它们以使其更易于理解。

![EF 关系图](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image15.png)

## <a name="entity-framework-source-code"></a>实体框架源代码

[GitHub](https://github.com/aspnet/EntityFramework6)上提供了实体框架6的源代码。 您可以为 bug 提供文件，并且您可以向 EF 源代码提供您自己的增强功能。

尽管源代码已打开，但实体框架完全支持作为 Microsoft 产品。 Microsoft Entity Framework 团队将控制接受哪些贡献和测试所有的代码更改，以确保每个版本的质量。

## <a name="acknowledgments"></a>致谢

- Tom Dykstra 编写了本教程的原始版本，共同创作了 EF 5 更新，并编写了 EF 6 更新。 Tom 是 Microsoft Web 平台和工具内容团队的高级编程编写器。
- [Rick Anderson](https://blogs.msdn.com/b/rickandy/) (twitter [@RickAndMSFT](http://twitter.com/RickAndMSFT)) 完成了对 EF 5 和 MVC 4 的教程的大部分工作，并共同创作了 ef 6 更新。 Rick 是 Microsoft 的高级编程编写人员，侧重于 Azure 和 MVC。
- [Rowan 莎莎](http://www.romiller.com) 和实体框架团队的其他成员协助进行代码评审，并帮助调试在我们更新 EF 5 和 ef 6 教程时出现的许多迁移问题。

## <a name="troubleshoot-common-errors"></a>排查常见错误

### <a name="cannot-createshadow-copy"></a>无法创建/隐藏副本

错误消息：

> &lt; &gt; 如果文件已存在，则无法创建/卷影复制 "filename"。

解决方案

请等待几秒钟，然后刷新页面。

### <a name="update-database-not-recognized"></a>更新-无法识别数据库

PMC) 中的命令 (的错误消息 `Update-Database` ：

> 术语 "更新-数据库" 未被识别为 cmdlet、函数、脚本文件或可运行程序的名称。 检查名称的拼写，如果包含路径，请验证该路径是否正确，并重试。

解决方案

退出 Visual Studio。 重新打开项目，然后重试。

### <a name="validation-failed"></a>验证失败

PMC) 中的命令 (的错误消息 `Update-Database` ：

> 对一个或多个实体的验证失败。 有关更多详细信息，请参阅 "EntityValidationErrors" 属性。

解决方案

此问题的一个原因是在方法运行时出现验证错误 `Seed` 。 有关调试方法的提示，请参阅 [播种和调试实体框架 (EF) ](https://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx) 数据库 `Seed` 。

### <a name="http-50019-error"></a>HTTP 500.19 错误

错误消息：

> HTTP 错误 500.19-内部服务器错误无法访问请求的页面，因为该页的相关配置数据无效。

解决方案

获取此错误的一种方法是使用解决方案的多个副本，每个副本使用相同的端口号。 通常可以通过退出 Visual Studio 的所有实例，然后重新启动正在处理的项目，来解决此问题。 如果这不起作用，请尝试更改端口号。 右键单击项目文件，然后单击 "属性"。 选择 " **Web** " 选项卡，然后在 " **项目 Url** " 文本框中更改端口号。

### <a name="error-locating-sql-server-instance"></a>定位 SQL Server 实例出错

错误消息：

> 建立到 SQL Server 的连接时出现与网络相关或特定于实例的错误。 找不到或无法访问服务器。 请验证实例名称是否正确，SQL Server 是否已配置为允许远程连接。 （提供程序：SQL 网络接口，错误：26 - 定位指定服务器/实例出错）

解决方案

请检查连接字符串。 如果手动删除了数据库，请在构造字符串中更改数据库的名称。

## <a name="get-the-code"></a>获取代码

[下载完成的项目](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a>其他资源

 有关如何使用实体框架处理数据的详细信息，请参阅 [MSDN 上的 EF 文档页](https://msdn.microsoft.com/data/ee712907) 和 [ASP.NET 数据访问-建议的资源](../../../../whitepapers/aspnet-data-access-content-map.md)。

有关如何在生成 web 应用程序后对其进行部署的详细信息，请参阅 MSDN Library 中的 [ASP.NET Web 部署-推荐资源](../../../../whitepapers/aspnet-web-deployment-content-map.md) 。

有关与 MVC 相关的其他主题（例如身份验证和授权）的信息，请参阅 [ASP.NET MVC-推荐的资源](../recommended-resources-for-mvc.md)。

## <a name="next-steps"></a>后续步骤

在本教程中，你将了解：

> [!div class="checklist"]
> * 已执行原始 SQL 查询
> * 执行无跟踪查询
> * 已检查发送到数据库的 SQL 查询

还了解了：

> [!div class="checklist"]
> * 创建抽象层
> * 代理类
> * 自动脏值检测
> * 自动验证
> * 实体框架 Power Tools
> * 实体框架源代码

这将完成本系列教程，介绍如何在 ASP.NET MVC 应用程序中使用实体框架。 如果要了解有关 EF Database First 的信息，请参阅 DB 第一系列教程。
> [!div class="nextstepaction"]
> [实体框架 Database First](../database-first-development/setting-up-database.md)

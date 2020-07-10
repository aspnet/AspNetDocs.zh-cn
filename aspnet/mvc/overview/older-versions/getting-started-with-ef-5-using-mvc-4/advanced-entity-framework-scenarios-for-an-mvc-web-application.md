---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/advanced-entity-framework-scenarios-for-an-mvc-web-application
title: MVC Web 应用程序的高级实体框架方案 (10 个) |Microsoft Docs
author: tdykstra
description: Contoso 大学示例 web 应用程序演示如何使用实体框架 5 Code First 和 Visual Studio .。。
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 64906a1d-f734-41cf-9615-ee95f8740996
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/advanced-entity-framework-scenarios-for-an-mvc-web-application
msc.type: authoredcontent
ms.openlocfilehash: f8f079f6d8ea663c6888456be422a2bae93a4b87
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "86163421"
---
# <a name="advanced-entity-framework-scenarios-for-an-mvc-web-application-10-of-10"></a>MVC Web 应用程序的高级实体框架方案 (10 个) 

作者： [Tom Dykstra](https://github.com/tdykstra)

[下载完成的项目](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Contoso 大学示例 web 应用程序演示了如何使用实体框架 5 Code First 和 Visual Studio 2012 创建 ASP.NET MVC 4 应用程序。 若要了解教程系列，请参阅[本系列中的第一个教程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。 你可以从头开始学习本系列教程，也可以从此处[下载入门项目](building-the-ef5-mvc4-chapter-downloads.md)。
> 
> > [!NOTE] 
> > 
> > 如果遇到无法解决的问题，请[下载已完成的章节](building-the-ef5-mvc4-chapter-downloads.md)并尝试重现你的问题。 通常可以通过将代码与已完成的代码进行比较，查找问题的解决方案。 有关一些常见错误以及如何解决这些错误，请参阅[错误和解决方法。](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)

在上一教程中，你已实现了存储库和工作单元模式。 本教程包括以下主题：

- 执行原始 SQL 查询。
- 正在执行无跟踪查询。
- 检查发送到数据库的查询。
- 使用代理类。
- 禁用更改的自动检测。
- 保存更改时禁用验证。
- [错误和解决办法](#errors)

对于大多数这些主题，你将使用已创建的页面。 若要使用原始 SQL 执行批量更新，您将创建一个新页，用于更新数据库中所有课程的信用额度：

![Update_Course_Credits_initial_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image1.png)

若要使用无跟踪查询，你需要将新的验证逻辑添加到部门编辑页面：

![Department_Edit_page_with_duplicate_administrator_error_message](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image2.png)

## <a name="performing-raw-sql-queries"></a>执行原始 SQL 查询

实体框架 Code First API 包括使你能够将 SQL 命令直接传递到数据库的方法。 你有以下选择：

- 使用`DbSet.SqlQuery`返回实体类型的查询方法。 返回的对象必须是对象所需的类型 `DbSet` ，并且数据库上下文会自动跟踪这些对象，除非关闭跟踪。  (参见以下有关方法的部分 `AsNoTracking` 。 ) 
- `Database.SqlQuery`对于返回非实体类型的查询，请使用方法。 数据库上下文不会跟踪返回的数据，即使你使用该方法来检索实体类型也是如此。
- 将[Database.ExecuteSqlCommand](https://msdn.microsoft.com/library/gg679456(v=vs.103).aspx)用于非查询命令。

使用 Entity Framework 的优点之一是它可避免你编写跟数据库过于耦合的代码 它会自动生成 SQL 查询和命令，使得你无需自行编写。 但在某些情况下，你需要运行已手动创建的特定 SQL 查询，并且这些方法使你能够处理此类异常。

在 Web 应用程序中执行 SQL 命令时，请务必采取预防措施来保护站点免受 SQL 注入攻击。 一种方法是使用参数化查询，确保不会将网页提交的字符串视为 SQL 命令。 在本教程中，将用户输入集成到查询中时会使用参数化查询。

### <a name="calling-a-query-that-returns-entities"></a>调用返回实体的查询

假设您希望 `GenericRepository` 类提供附加的筛选和排序灵活性，而不需要使用其他方法创建派生类。 实现此目的的一种方法是添加接受 SQL 查询的方法。 然后，您可以在控制器中指定想要的任何类型的筛选或排序，如 `Where` 依赖于联接或子查询的子句。 在本节中，你将了解如何实现此类方法。

`GetWithRawSql`通过将以下代码添加到*GenericRepository.cs*，创建方法：

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample1.cs)]

在*CourseController.cs*中，从方法调用新方法 `Details` ，如以下示例中所示：

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample2.cs)]

在这种情况下，您可以使用 `GetByID` 方法，但使用 `GetWithRawSql` 方法来验证 `GetWithRawSQL` 方法是否有效。

运行 "详细信息" 页，验证 "选择查询是否有效" (选择 "**课程**" 选项卡，然后选择一个课程) 的**详细信息**。

![Course_Details_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image3.png)

### <a name="calling-a-query-that-returns-other-types-of-objects"></a>调用返回其他类型对象的查询

之前你在“关于”页面创建了一个学生统计信息网格，显示每个注册日期的学生数量。 在*HomeController.cs*中执行此操作的代码使用 LINQ：

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample3.cs)]

假设您要编写在 SQL 中直接检索此数据的代码，而不是使用 LINQ。 为此，您需要运行一个返回除 entity 对象之外的内容的查询，这意味着您需要使用 `Database.SqlQuery` 方法。

在*HomeController.cs*中，将方法中的 LINQ 语句替换 `About` 为以下代码：

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample4.cs)]

运行 "关于" 页。 显示的数据和之前一样。

![About_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image4.png)

### <a name="calling-an-update-query"></a>调用更新查询

假设 Contoso 大学管理员希望能够在数据库中执行大容量更改，如更改每个课程的信用额度。 如果该大学提供了大量课程，那么将所有课程作为实体来检索并单独更改就非常低效。 在本节中，您将实现一个网页，该网页允许用户指定更改所有课程的信用额度的因素，并通过执行 SQL 语句进行更改 `UPDATE` 。 网页的外观类似于下图：

![Update_Course_Credits_initial_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image5.png)

在上一教程中，你使用了通用存储库来读取和更新 `Course` 控制器中的实体 `Course` 。 对于此大容量更新操作，需要创建不在通用存储库中的新存储库方法。 为此，你将创建一个 `CourseRepository` 派生自类的专用类 `GenericRepository` 。

在*DAL*文件夹中，创建*CourseRepository.cs* ，并将现有代码替换为以下代码：

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample5.cs)]

在*UnitOfWork.cs*中，将 `Course` 存储库类型从更改 `GenericRepository<Course>` 为`CourseRepository:`

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample6.cs)]

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample7.cs)]

在*CourseController.cs*中，添加 `UpdateCourseCredits` 方法：

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample8.cs)]

此方法将用于 `HttpGet` 和 `HttpPost` 。 当该 `HttpGet` `UpdateCourseCredits` 方法运行时， `multiplier` 变量将为 null，并且该视图将显示一个空文本框和一个提交按钮，如上图所示。

单击 "**更新**" 按钮并运行该 `HttpPost` 方法时， `multiplier` 会在文本框中输入值。 然后，该代码调用存储库 `UpdateCourseCredits` 方法，该方法返回受影响的行数，该值存储在对象中 `ViewBag` 。 当视图接收到对象中受影响的行数时 `ViewBag` ，它将显示该数字，而不是文本框和提交按钮，如下图所示：

![Update_Course_Credits_rows_affected_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image6.png)

在 "更新课程信用额度" 页的*Views\Course*文件夹中创建视图：

![Add_View_dialog_box_for_Update_Course_Credits](https://asp.net/media/2578203/Windows-Live-Writer_Advanced-Entity-Framework-Scenarios-for-_CEF8_Add_View_dialog_box_for_Update_Course_Credits.png)

在*Views\Course\UpdateCourseCredits.cshtml*中，将模板代码替换为以下代码：

[!code-cshtml[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample9.cshtml)]

通过选择**Courses**选项卡运行`UpdateCourseCredits`方法，然后在浏览器地址栏中 URL 的末尾添加"/ UpdateCourseCredits"到 (例如： `http://localhost:50205/Course/UpdateCourseCredits`)。 在文本框中输入数字：

![Update_Course_Credits_initial_page_with_2_entered](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image7.png)

单击**Update**。 你会看到受影响的行数：

![Update_Course_Credits_rows_affected_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image8.png)

单击“返回列表”可以查看课程列表，其中学分已替换为修改后的数字。

![Courses_Index_page_showing_revised_credits](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image9.png)

有关原始 SQL 查询的详细信息，请参阅实体框架团队博客上的[原始 Sql 查询](https://blogs.msdn.com/b/adonet/archive/2011/02/04/using-dbcontext-in-ef-feature-ctp5-part-10-raw-sql-queries.aspx)。

## <a name="no-tracking-queries"></a>非跟踪查询

当数据库上下文检索数据库行并创建表示它们的实体对象时，默认情况下，它会跟踪内存中的实体是否与数据库中的实体同步。 更新实体时，内存中的数据充当缓存并使用该数据。 在 Web 应用程序中，此缓存通常是不必要的，因为上下文实例通常生存期较短（创建新的实例并用于处理每个请求），并且通常在再次使用该实体之前处理读取实体的上下文。

您可以使用方法指定上下文是否跟踪查询的实体对象 `AsNoTracking` 。 可能想要执行的典型方案包括以下操作：

- 此查询检索到关闭跟踪可能会明显提高性能的大量数据。
- 您希望附加实体以便对其进行更新，但您之前检索到不同用途的同一实体。 由于数据库上下文已跟踪了该实体，因此无法附加要更改的实体。 防止此情况发生的一种方法是将 `AsNoTracking` 选项与前面的查询一起使用。

在本部分中，你将实现用于阐释其中第二种情况的业务逻辑。 具体来说，您将强制实施一条业务规则，指出讲师不能是多个部门的管理员。

在*DepartmentController.cs*中，添加一个可从和方法调用的新方法， `Edit` `Create` 以确保没有两个部门具有相同的管理员：

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample10.cs)]

如果没有验证错误，请在方法的块中添加代码 `try` `HttpPost` `Edit` 以调用此新方法。 `try`该块现在类似于以下示例：

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample11.cs?highlight=9-12)]

运行 "部门编辑" 页，然后尝试将部门的管理员更改为已是其他部门的管理员的指导员。 你会收到预期的错误消息：

![Department_Edit_page_with_duplicate_administrator_error_message](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image10.png)

现在再次运行 "部门编辑" 页，此时更改**预算**金额。 单击 "**保存**" 时，会看到错误页：

![Department_Edit_page_with_object_state_manager_error_message](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image11.png)

异常错误消息为 " `An object with the same key already exists in the ObjectStateManager. The ObjectStateManager cannot track multiple objects with the same key.` "，原因如下：

- `Edit`方法调用 `ValidateOneAdministratorAssignmentPerInstructor` 方法，该方法检索将 Kim Abercrombie 作为其管理员的所有部门。 这会导致读取英语部门。 由于这是正在编辑的部门，因此不会报告任何错误。 但是，此读取操作的结果是，数据库上下文现在正在跟踪从数据库中读取的英语部门实体。
- 此 `Edit` 方法尝试 `Modified` 在由 MVC 模型联编程序创建的英语部门实体上设置标志，但这会失败，因为上下文已在跟踪英语部门的实体。

此问题的一种解决方法是使上下文不会跟踪由验证查询检索到的内存中部门实体。 执行此操作没有任何缺点，因为你不会更新此实体，也不会以一种可从其缓存在内存中的方式对其进行读取。

在*DepartmentController.cs*的方法中， `ValidateOneAdministratorAssignmentPerInstructor` 指定 no 跟踪，如下所示：

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample12.cs?highlight=4)]

重复尝试编辑部门的**预算**金额。 此操作成功后，站点会按预期方式返回到 "部门索引" 页，其中显示了修改后的预算值。

## <a name="examining-queries-sent-to-the-database"></a>检查发送到数据库的查询

有时能够以查看发送到数据库的实际 SQL 查询对于开发者来说是很有用的。 为此，可以在调试器中检查查询变量，或调用查询的 `ToString` 方法。 若要尝试此操作，你将看到一个简单的查询，然后在你添加预先加载、筛选和排序选项时，查看该查询所发生的情况。

在 controller */CourseController*中，将 `Index` 方法替换为以下代码：

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample13.cs?highlight=3)]

现在，在的*GenericRepository.cs*中设置一个断点，并在方法的语句上设置一个断点 `return query.ToList();` `return orderBy(query).ToList();` `Get` 。 在调试模式下运行项目，然后选择 "课程索引" 页。 当代码到达断点时，检查 `query` 变量。 你会看到发送到 SQL Server 的查询。 这是一个简单的 `Select` 语句：

[!code-json[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample14.json)]

![](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image12.png)

查询可能太长，无法在 Visual Studio 中的调试窗口中显示。 若要查看整个查询，可以复制变量值，并将其粘贴到文本编辑器中：

![Copy_value_of_variable_in_debug_mode](https://asp.net/media/2578239/Windows-Live-Writer_Advanced-Entity-Framework-Scenarios-for-_CEF8_Copy_value_of_variable_in_debug_mode_0902a2b1-b799-47a6-9b4b-f266c79d83c1.png)

现在，您将向 "课程索引" 页添加一个下拉列表，以便用户可以筛选特定部门。 您将按标题对课程进行排序，并指定预先加载 `Department` 导航属性。 在*CourseController.cs*中，将 `Index` 方法替换为以下代码：

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample15.cs)]

方法接收参数中下拉列表的选定值 `SelectedDepartment` 。 如果未选择任何内容，则此参数将为 null。

将 `SelectList` 包含所有部门的集合传递给下拉列表的视图。 传递给 `SelectList` 构造函数的参数指定值字段名称、文本字段名称和选定项。

对于 `Get` 存储库的方法 `Course` ，代码指定筛选器表达式、排序顺序以及预先加载 `Department` 导航属性。 `true`如果未在下拉列表中选择任何内容，则筛选表达式始终返回 (即 `SelectedDepartment` 为 null) 。

在*Views\Course\Index.cshtml*中，紧跟在开始 `table` 标记之前，添加以下代码以创建下拉列表和 "提交" 按钮：

[!code-cshtml[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample16.cshtml)]

在类中仍设置断点的情况 `GenericRepository` 下，运行 "课程索引" 页。 继续执行第两次：代码命中断点，以便在浏览器中显示该页。 从下拉列表中选择一个部门，然后单击 "**筛选器**"：

![Course_Index_page_with_department_selected](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image13.png)

这次，第一个断点将用于下拉列表的部门查询。 跳过该操作，并在 `query` 下一次代码到达断点时查看变量，以便查看 `Course` 查询现在的外观。 你将看到如下所示的内容：

[!code-json[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample17.json)]

您可以看到，该查询现在是一个 `JOIN` 查询，该查询将 `Department` 数据与 `Course` 数据一起加载，并且它包含一个 `WHERE` 子句。

<a id="proxyclasses"></a>

## <a name="working-with-proxy-classes"></a>使用代理类

如果实体框架创建实体实例 (例如，在执行查询) 时，它通常会将其创建为作为实体代理的动态生成的派生类型的实例。 此代理会重写实体的某些虚拟属性，以插入挂钩，以便在访问属性时自动执行操作。 例如，此机制用于支持关系的延迟加载。

大多数情况下，无需注意代理的这种使用，但有一些例外：

- 在某些情况下，你可能想要阻止实体框架创建代理实例。 例如，序列化非代理实例可能比序列化代理实例更有效。
- 如果使用运算符实例化实体类 `new` ，则不会获得代理实例。 这意味着不会获得延迟加载和自动更改跟踪等功能。 这通常是正常的;通常不需要延迟加载，因为你要创建的是不在数据库中的新实体，并且如果你将实体显式标记为，则通常不需要更改跟踪 `Added` 。 但是，如果确实需要延迟加载并且需要更改跟踪，则可以使用类的方法通过代理创建新的实体实例 `Create` `DbSet` 。
- 你可能需要从代理类型获取实际的实体类型。 您可以使用 `GetObjectType` 类的方法 `ObjectContext` 来获取代理类型实例的实际实体类型。

有关详细信息，请参阅在实体框架团队博客上使用[代理](https://blogs.msdn.com/b/adonet/archive/2011/02/02/using-dbcontext-in-ef-feature-ctp5-part-8-working-with-proxies.aspx)。

## <a name="disabling-automatic-detection-of-changes"></a>禁用更改的自动检测

Entity Framework 通过比较的实体的当前值与原始值来判断更改实体的方式 （因此需要发送更新到数据库）。 查询或附加实体时，会存储原始值。 如下方法会导致自动脏值：

- `DbSet.Find`
- `DbSet.Local`
- `DbSet.Remove`
- `DbSet.Add`
- `DbSet.Attach`
- `DbContext.SaveChanges`
- `DbContext.GetValidationErrors`
- `DbContext.Entry`
- `DbChangeTracker.Entries`

如果正在跟踪大量实体，并且在循环中多次调用这些方法之一，则使用[AutoDetectChangesEnabled](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.autodetectchangesenabled(VS.103).aspx)属性暂时关闭自动更改检测可能会显著提高性能。 有关详细信息，请参阅[自动检测更改](https://blogs.msdn.com/b/adonet/archive/2011/02/06/using-dbcontext-in-ef-feature-ctp5-part-12-automatically-detecting-changes.aspx)。

## <a name="disabling-validation-when-saving-changes"></a>保存更改时禁用验证

在调用方法时 `SaveChanges` ，默认情况下，实体框架在更新数据库之前验证所有已更改实体的所有属性中的数据。 如果已更新大量实体，并且已验证数据，则不需要执行此操作，并且可以通过暂时关闭验证来使保存更改的过程更少。 可以使用[ValidateOnSaveEnabled](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.validateonsaveenabled(VS.103).aspx)属性执行此操作。 有关详细信息，请参阅[验证](https://blogs.msdn.com/b/adonet/archive/2010/12/15/ef-feature-ctp5-validation.aspx)。

## <a name="summary"></a>摘要

这将完成本系列教程，介绍如何在 ASP.NET MVC 应用程序中使用实体框架。 可在[ASP.NET 数据访问内容映射](../../../../whitepapers/aspnet-data-access-content-map.md)中找到指向其他实体框架资源的链接。

有关如何在生成 web 应用程序后对其进行部署的详细信息，请参阅 MSDN Library 中的[ASP.NET 部署内容映射](https://msdn.microsoft.com/library/bb386521.aspx)。

有关与 MVC 相关的其他主题（如身份验证和授权）的信息，请参阅[Mvc 推荐资源](../../getting-started/recommended-resources-for-mvc.md)。

<a id="acknowledgments"></a>

## <a name="acknowledgments"></a>鸣谢

- Tom Dykstra 编写了本教程的原始版本，它是 Microsoft Web 平台和工具内容团队的高级编程编写者。
- [Rick Anderson](https://blogs.msdn.com/b/rickandy/) (twitter [@RickAndMSFT](http://twitter.com/RickAndMSFT)) 共同创作此教程，并为 EF 5 和 MVC 4 更新了大部分工作。 Rick 是 Microsoft 的高级编程编写人员，侧重于 Azure 和 MVC。
- [Rowan 莎莎](http://www.romiller.com)和实体框架团队的其他成员协助进行代码评审，并帮助调试在我们更新 EF 5 的教程时出现的许多迁移问题。

## <a name="vb"></a>VB

最初生成本教程时，我们提供了已完成下载项目的 c # 和 VB 版本。 通过此更新，我们将为每一章提供一个 c # 可下载项目，以便更轻松地开始使用序列中的任何位置，但由于存在时间限制，也不会为 VB 执行其他优先级操作。 如果使用这些教程生成 VB 项目，并愿意与他人共享，请告知我们。

<a id="errors"></a>

## <a name="errors-and-workarounds"></a>错误和解决方法

### <a name="cannot-createshadow-copy"></a>无法创建/隐藏副本

错误消息：

*如果文件已存在，则无法创建/影像复制 ' DotNetOpenAuth '。*

解决方案：

请等待几秒钟，然后刷新页面。

### <a name="update-database-not-recognized"></a>更新-无法识别数据库

错误消息：

*术语 "更新-数据库" 未被识别为 cmdlet、函数、脚本文件或可运行程序的名称。检查名称的拼写，如果包含路径，请验证路径是否正确，然后重试。* (*`Update-Database`* PMC 中的命令。 ) 

解决方案：

退出 Visual Studio。 重新打开项目，然后重试。

### <a name="validation-failed"></a>验证失败

错误消息：

*对一个或多个实体的验证失败。有关更多详细信息，请参阅 "EntityValidationErrors" 属性。*  (*`Update-Database`* PMC 中的命令。 ) 

解决方案：

此问题的一个原因是在方法运行时出现验证错误 `Seed` 。 有关调试方法的提示，请参阅[播种和调试实体框架 (EF) ](https://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx)数据库 `Seed` 。

### <a name="http-50019-error"></a>HTTP 500.19 错误

错误消息：

*HTTP 错误 500.19-内部服务器错误无法访问请求的页面，因为该页的相关配置数据无效。*

解决方案：

获取此错误的一种方法是使用解决方案的多个副本，每个副本使用相同的端口号。 通常可以通过退出 Visual Studio 的所有实例，然后重新启动正在处理的项目，来解决此问题。 如果这不起作用，请尝试更改端口号。 右键单击项目文件，然后单击 "属性"。 选择 " **Web** " 选项卡，然后在 "**项目 Url** " 文本框中更改端口号。

### <a name="error-locating-sql-server-instance"></a>定位 SQL Server 实例出错

错误消息：

*建立与 SQL Server 的连接时出现与网络相关或特定于实例的错误。找不到或无法访问服务器。请验证实例名称是否正确，以及 SQL Server 是否配置为允许远程连接。 (提供程序： SQL 网络接口，错误： 26-定位指定的服务器/实例时出错) *

解决方案：

检查连接字符串。 如果手动删除了数据库，请在构造字符串中更改数据库的名称。

> [!div class="step-by-step"]
> [上一页](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md)
> [下一页](building-the-ef5-mvc4-chapter-downloads.md)

---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application
title: 在 ASP.NET MVC 应用程序中实现存储库和工作单元模式 (9 of 10) |Microsoft Docs
author: tdykstra
description: Contoso 大学示例 web 应用程序演示如何使用实体框架 5 Code First 和 Visual Studio .。。
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 44761193-04ba-4990-9f90-145d3c10a716
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 03579bbaf454583543f09f68ac1b94a3b1ec0d92
ms.sourcegitcommit: d5049dfb08ff14872ba3b29a702e0589a776b430
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2021
ms.locfileid: "102194547"
---
# <a name="implementing-the-repository-and-unit-of-work-patterns-in-an-aspnet-mvc-application-9-of-10"></a>在 ASP.NET MVC 应用程序中实现存储库和工作单元模式 (9 of 10) 

作者： [Tom Dykstra](https://github.com/tdykstra)


> Contoso 大学示例 web 应用程序演示了如何使用实体框架 5 Code First 和 Visual Studio 2012 创建 ASP.NET MVC 4 应用程序。 若要了解教程系列，请参阅[本系列中的第一个教程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。
> 
> > [!NOTE] 
> > 
> > 如果遇到无法解决的问题，请 [下载已完成的章节](building-the-ef5-mvc4-chapter-downloads.md) 并尝试重现你的问题。 通常可以通过将代码与已完成的代码进行比较，查找问题的解决方案。 有关一些常见错误以及如何解决这些错误，请参阅 [错误和解决方法。](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)

在上一教程中，你使用了继承来减少 `Student` 和实体类中的多余代码 `Instructor` 。 在本教程中，你将看到一些使用存储库和适用于 CRUD 操作的工作单元模式的方法。 如前面的教程中所述，在这种情况下，你将使用已创建的页面而不是创建新页面来更改代码的工作方式。

## <a name="the-repository-and-unit-of-work-patterns"></a>存储库和工作单元模式

存储库和工作单元模式旨在创建数据访问层和应用程序的业务逻辑层之间的抽象层。 实现这些模式可让你的应用程序对数据存储介质的更改不敏感，而且很容易进行自动化单元测试和进行测试驱动开发 (TDD)。

在本教程中，您将为每个实体类型实现一个存储库类。 对于 `Student` 实体类型，你将创建一个存储库接口和一个存储库类。 当你在控制器中实例化存储库时，将使用接口，以使控制器接受对实现存储库接口的任何对象的引用。 当控制器在 web 服务器下运行时，它会收到与实体框架一起工作的存储库。 当控制器在单元测试类下运行时，它会收到一个存储库，该存储过程可用于轻松地操作测试（例如内存中集合）的数据。

稍后在本教程中，将使用多个存储库和 `Course` `Department` 控制器中的和实体类型的工作单元 `Course` 。 工作单元通过创建所有存储库的工作方式来协调多个存储库的工作。 如果希望能够执行自动单元测试，可以使用与存储库相同的方式为这些类创建和使用接口 `Student` 。 但是，为了简化本教程，你将创建并使用这些类，而无需使用接口。

下图显示了一种概念化控制器和上下文类之间的关系的方法，与根本不使用存储库或工作单元模式完全相同。

![Repository_pattern_diagram](https://asp.net/media/2578149/Windows-Live-Writer_8c4963ba1fa3_CE3B_Repository_pattern_diagram_1df790d3-bdf2-4c11-9098-946ddd9cd884.png)

不会在本系列教程中创建单元测试。 有关使用使用存储库模式的 MVC 应用程序的 TDD 简介，请参阅 [演练：将 TDD 与 ASP.NET MVC 配合使用](https://msdn.microsoft.com/library/ff847525.aspx)。 有关存储库模式的详细信息，请参阅以下资源：

- MSDN 上[的存储库模式](https://msdn.microsoft.com/library/ff649690.aspx)。
- Julie Lerman 的博客上的[敏捷实体框架4存储库](http://thedatafarm.com/blog/data-access/agile-entity-framework-4-repository-part-1-model-and-poco-classes/)系列。
- 在 Dan Wahlin 的博客上[快速生成 HTML5/JQuery 应用程序的帐户](https://weblogs.asp.net/dwahlin/archive/2011/08/15/building-the-account-at-a-glance-html5-jquery-application.aspx)。

> [!NOTE]
> 可以通过多种方法实现存储库和工作单元模式。 你可以使用或不带工作单位类的存储库类。 您可以为所有实体类型或每个类型分别实现一个存储库。 如果为每个类型实现一个类型，则可以使用单独的类、泛型基类和派生类，或者使用抽象基类和派生类。 你可以在存储库中包含业务逻辑，或将其限制为数据访问逻辑。 还可以通过使用 [IDbSet](https://msdn.microsoft.com/library/gg679233(v=vs.103).aspx) 接口（而不是实体集的 [DbSet](https://msdn.microsoft.com/library/system.data.entity.dbset(v=vs.103).aspx) 类型）将抽象层生成到数据库上下文类中。 本教程中所示的实现抽象层的方法是一个选项，而不是针对所有方案和环境的建议。

## <a name="creating-the-student-repository-class"></a>创建 Student Repository 类

在 *DAL* 文件夹中，创建一个名为 *IStudentRepository.cs* 的类文件，并将现有代码替换为以下代码：

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample1.cs)]

此代码声明一组典型的 CRUD 方法，其中包括两个读取方法：一个返回所有 `Student` 实体，另一个用于 `Student` 按 ID 查找单个实体。

在 *DAL* 文件夹中，创建一个名为 *StudentRepository.cs* 文件的类文件。 将现有代码替换为以下代码，用于实现 `IStudentRepository` 接口：

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample2.cs)]

数据库上下文是在类变量中定义的，并且构造函数要求调用对象传入上下文的实例：

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample3.cs)]

你可以在存储库中实例化新的上下文，但是，如果在一个控制器中使用了多个存储库，则每个存储库都将使用单独的上下文。 稍后你将在控制器中使用多个存储库 `Course` ，你将看到一个工作单元类如何确保所有存储库都使用同一上下文。

存储库实现 [IDisposable](https://msdn.microsoft.com/library/system.idisposable.aspx) ，并按照前面在控制器中看到的方式释放数据库上下文，并且它的 CRUD 方法会以您之前看到的相同方式调用数据库上下文。

## <a name="change-the-student-controller-to-use-the-repository"></a>更改学生控制器以使用存储库

在 *StudentController.cs* 中，将类中当前的代码替换为以下代码。 突出显示所作更改。

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample4.cs?highlight=13-18,44,75,77,102-103,120,137-138,159,172-174,186)]

控制器现在为实现接口的对象 `IStudentRepository` （而不是上下文类）声明类变量：

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample5.cs)]

默认 (无参数) 构造函数将创建一个新的上下文实例，而可选的构造函数允许调用方在上下文实例中传入。

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample6.cs)]

 (如果使用的是 *依赖关系注入* 或 DI，则不需要默认构造函数，因为 DI 软件将确保始终提供正确的存储库对象。 ) 

在 CRUD 方法中，现在将调用存储库，而不是上下文：

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample7.cs)]

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample8.cs)]

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample9.cs)]

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample10.cs)]

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample11.cs)]

现在， `Dispose` 方法会释放存储库，而不是上下文：

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample12.cs)]

运行站点并单击 " **学生** " 选项卡。

![Students_Index_page](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/_static/image1.png)

页面的外观和工作方式与您将代码更改为使用存储库之前的效果相同，并且其他学生页面也工作正常。 但是， `Index` 控制器方法进行筛选和排序的方式有很大的差异。 此方法的原始版本包含以下代码：

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample13.cs?highlight=1)]

更新的 `Index` 方法包含以下代码：

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample14.cs?highlight=1)]

仅突出显示的代码已更改。

在代码的原始版本中， `students` 类型化为 `IQueryable` 对象。 直到使用诸如这样的方法将查询转换为集合后，才会将其发送到数据库 `ToList` 中，这种情况在索引视图访问学生模型之前不会出现。 `Where`上面原始代码中的方法成为 `WHERE` 发送到数据库的 SQL 查询中的子句。 这反过来意味着，数据库仅返回选定的实体。 但是，在更改 `context.Students` 为 `studentRepository.GetStudents()` `students` 之后，该语句后的变量是 `IEnumerable` 包含数据库中所有学生的集合。 应用方法的最终结果 `Where` 是相同的，但现在工作是在 web 服务器上的内存中完成的，而不是在数据库中完成。 对于返回大量数据的查询，这可能会降低效率。

> [!TIP]
> 
> **IQueryable vs.IEnumerable**
> 
> 实现此存储库后，即使在 **搜索** 框中输入了内容，查询发送到 SQL Server 也会返回所有学生行，因为它不包含搜索条件：
> 
> ![](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/_static/image2.png)
> 
> [!code-sql[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample15.sql)]
> 
> 此查询将返回所有学生数据，因为存储库执行查询时未了解搜索条件。 在这种情况下，排序、应用搜索条件以及选择数据的子集以进行分页 (仅在此情况下才会显示3行) 在该集合中调用方法时在内存中完成 `ToPagedList` `IEnumerable` 。
> 
> 在之前版本的代码中 (在实现存储库之前) ，在应用搜索条件后，在对对象调用时，该查询才会发送到数据库 `ToPagedList` `IQueryable` 。
> 
> ![](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/_static/image3.png)
> 
> 当对某个对象调用 ToPagedList 时 `IQueryable` ，发送给 SQL Server 的查询将指定搜索字符串，因此，仅返回满足搜索条件的行，并且不需要在内存中执行任何筛选。
> 
> [!code-sql[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample16.sql)]
> 
>  (以下教程介绍了如何检查发送到 SQL Server 的查询。 ) 

以下部分演示如何实现存储库方法，使用这些方法可以指定数据库应执行此操作。

你现在已在控制器和实体框架数据库上下文之间创建了一个抽象层。 如果要使用此应用程序执行自动单元测试，可以在实现的单元测试项目中创建备用存储库类 `IStudentRepository` *。* 此 mock 存储库类可以操作内存中集合，而不是调用上下文来读取和写入数据，而是为了测试控制器函数。

## <a name="implement-a-generic-repository-and-a-unit-of-work-class"></a>实现一个通用存储库和一个工作单元类

为每个实体类型创建存储库类可能会导致大量冗余代码，并可能导致部分更新。 例如，假设您必须将两个不同的实体类型更新为同一事务的一部分。 如果每个都使用单独的数据库上下文实例，则可能会成功，而另一个可能会失败。 最大程度地减少冗余代码的一种方法是使用通用存储库，并确保所有存储库都使用相同的数据库上下文 (，从而协调所有更新) 使用工作单元。

在本教程的此部分中，你将创建一个 `GenericRepository` 类和一个 `UnitOfWork` 类，并在控制器中使用它们 `Course` 来访问 `Department` 和 `Course` 实体集。 如前文所述，若要使本教程的这一部分简单，你不会为这些类创建接口。 但是，如果您打算使用它们来促进 TDD，则通常使用与存储库相同的方式来实现这些接口 `Student` 。

### <a name="create-a-generic-repository"></a>创建通用存储库

在 *DAL* 文件夹中，创建 *GenericRepository.cs* ，并将现有代码替换为以下代码：

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample17.cs)]

为数据库上下文和存储库实例化的实体集声明类变量：

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample18.cs)]

构造函数接受数据库上下文实例并初始化实体集变量：

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample19.cs)]

`Get`方法使用 lambda 表达式来允许调用代码指定筛选条件，并使用一列来对结果进行排序，而字符串参数则允许调用方为预先加载提供以逗号分隔的导航属性列表：

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample20.cs)]

此代码 `Expression<Func<TEntity, bool>> filter` 意味着调用方将基于该类型提供 lambda 表达式 `TEntity` ，并且此表达式将返回一个布尔值。 例如，如果存储库是针对实体类型实例化的 `Student` ，则调用方法中的代码可能 `student => student.LastName == "Smith` &quot; 为参数指定 `filter` 。

此代码 `Func<IQueryable<TEntity>, IOrderedQueryable<TEntity>> orderBy` 还意味着调用方将提供 lambda 表达式。 但在这种情况下，表达式的输入是 `IQueryable` 该类型的对象 `TEntity` 。 表达式将返回该对象的有序版本 `IQueryable` 。 例如，如果存储库是针对实体类型实例化的 `Student` ，则调用方法中的代码可能 `q => q.OrderBy(s => s.LastName)` 为参数指定 `orderBy` 。

方法中的代码 `Get` 会创建一个 `IQueryable` 对象，然后应用筛选器表达式（如果有）：

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample21.cs)]

接下来，它会在分析以逗号分隔的列表后应用预先加载的表达式：

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample22.cs)]

最后，它将应用 `orderBy` 表达式（如果有）并返回结果; 否则返回无序查询的结果：

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample23.cs)]

当调用方法时 `Get` ，您可以对由方法返回的集合进行筛选和排序， `IEnumerable` 而不是为这些函数提供参数。 但排序和筛选工作就会在 web 服务器的内存中完成。 通过使用这些参数，可以确保由数据库而不是 web 服务器来完成工作。 一种替代方法是为特定实体类型创建派生类并添加专用 `Get` 方法，如 `GetStudentsInNameOrder` 或 `GetStudentsByName` 。 但是，在复杂应用程序中，这可能会导致大量的此类派生类和专用方法，这可能更适合维护。

`GetByID`、和方法中的代码 `Insert` 与在 `Update` 非泛型存储库中看到的代码类似。  (不会在签名中提供预先加载参数 `GetByID` ，因为不能使用方法进行预先加载 `Find` 。 ) 

为方法提供了两个重载 `Delete` ：

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample24.cs)]

其中一种方式可让你只传入要删除的实体的 ID，另一种是使用实体实例。 正如在 [处理并发](../../getting-started/getting-started-with-ef-using-mvc/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md) 教程中看到的那样，对于并发处理，需要一个 `Delete` 采用包含跟踪属性原始值的实体实例的方法。

此通用存储库将处理典型的 CRUD 要求。 当特定实体类型具有特殊要求（如更复杂的筛选或排序）时，可以创建一个具有该类型附加方法的派生类。

## <a name="creating-the-unit-of-work-class"></a>创建工作单元类

工作单元类可用于：确保在使用多个存储库时，它们共享单个数据库上下文。 这样一来，当工作单元完成时，你可以 `SaveChanges` 在该上下文实例上调用方法，并确保所有相关更改都将进行协调。 类所需的全部都是 `Save` 每个存储库的方法和属性。 每个存储库属性返回一个存储库实例，该实例已使用与其他存储库实例相同的数据库上下文实例实例化。

在 *DAL* 文件夹中，创建一个名为 *UnitOfWork.cs* 的类文件，并将模板代码替换为以下代码：

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample25.cs)]

此代码为数据库上下文和每个存储库创建类变量。 对于 `context` 变量，会实例化一个新上下文：

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample26.cs)]

每个存储库属性检查存储库是否已存在。 如果不是，则会实例化存储库，并传入上下文实例。 因此，所有存储库共享相同的上下文实例。

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample27.cs)]

`Save`方法调用 `SaveChanges` 数据库上下文。

与在类变量中实例化数据库上下文的任何类一样， `UnitOfWork` 类实现 `IDisposable` 并释放上下文。

### <a name="changing-the-course-controller-to-use-the-unitofwork-class-and-repositories"></a>更改课程控制器以使用 UnitOfWork 类和存储库

使用以下代码替换 *CourseController.cs* 中当前具有的代码：

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample28.cs?highlight=15,20,22,31,54-55,70,85-86,101-102,122-124,130)]

此代码将为类添加类变量 `UnitOfWork` 。  (如果使用的是接口，则不会在此处初始化变量;相反，您需要实现两个构造函数的模式，就像对存储库执行的操作一样 `Student` 。 ) 

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample29.cs)]

在类的其余部分中，对数据库上下文的所有引用都将替换为对相应存储库的引用，并使用 `UnitOfWork` 属性访问存储库。 `Dispose`方法释放 `UnitOfWork` 实例。

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample30.cs)]

运行站点并单击 " **课程** " 选项卡。

![Courses_Index_page](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/_static/image4.png)

页面的外观和工作方式与更改之前的效果相同，并且其他课程页面也相同。

## <a name="summary"></a>总结

现在，已实现存储库和工作单元模式。 已使用 lambda 表达式作为泛型存储库中的方法参数。 有关如何在对象中使用这些表达式的详细信息 `IQueryable` ，请参阅 MSDN Library 中的 [IQueryable (T) Interface () ](https://msdn.microsoft.com/library/bb351562.aspx) 。 在下一教程中，你将学习如何处理一些高级方案。

可在 [ASP.NET 数据访问内容映射](../../../../whitepapers/aspnet-data-access-content-map.md)中找到指向其他实体框架资源的链接。

> [!div class="step-by-step"]
> [上一页](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md)
> [下一页](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)

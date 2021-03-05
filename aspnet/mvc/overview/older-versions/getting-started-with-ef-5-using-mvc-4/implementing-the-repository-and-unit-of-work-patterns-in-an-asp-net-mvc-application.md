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
# <a name="implementing-the-repository-and-unit-of-work-patterns-in-an-aspnet-mvc-application-9-of-10"></a><span data-ttu-id="8158f-103">在 ASP.NET MVC 应用程序中实现存储库和工作单元模式 (9 of 10) </span><span class="sxs-lookup"><span data-stu-id="8158f-103">Implementing the Repository and Unit of Work Patterns in an ASP.NET MVC Application (9 of 10)</span></span>

<span data-ttu-id="8158f-104">作者： [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="8158f-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>


> <span data-ttu-id="8158f-105">Contoso 大学示例 web 应用程序演示了如何使用实体框架 5 Code First 和 Visual Studio 2012 创建 ASP.NET MVC 4 应用程序。</span><span class="sxs-lookup"><span data-stu-id="8158f-105">The Contoso University sample web application demonstrates how to create ASP.NET MVC 4 applications using the Entity Framework 5 Code First and Visual Studio 2012.</span></span> <span data-ttu-id="8158f-106">若要了解教程系列，请参阅[本系列中的第一个教程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。</span><span class="sxs-lookup"><span data-stu-id="8158f-106">For information about the tutorial series, see [the first tutorial in the series](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>
> 
> > [!NOTE] 
> > 
> > <span data-ttu-id="8158f-107">如果遇到无法解决的问题，请 [下载已完成的章节](building-the-ef5-mvc4-chapter-downloads.md) 并尝试重现你的问题。</span><span class="sxs-lookup"><span data-stu-id="8158f-107">If you run into a problem you can't resolve, [download the completed chapter](building-the-ef5-mvc4-chapter-downloads.md) and try to reproduce your problem.</span></span> <span data-ttu-id="8158f-108">通常可以通过将代码与已完成的代码进行比较，查找问题的解决方案。</span><span class="sxs-lookup"><span data-stu-id="8158f-108">You can generally find the solution to the problem by comparing your code to the completed code.</span></span> <span data-ttu-id="8158f-109">有关一些常见错误以及如何解决这些错误，请参阅 [错误和解决方法。](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)</span><span class="sxs-lookup"><span data-stu-id="8158f-109">For some common errors and how to solve them, see [Errors and Workarounds.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)</span></span>

<span data-ttu-id="8158f-110">在上一教程中，你使用了继承来减少 `Student` 和实体类中的多余代码 `Instructor` 。</span><span class="sxs-lookup"><span data-stu-id="8158f-110">In the previous tutorial you used inheritance to reduce redundant code in the `Student` and `Instructor` entity classes.</span></span> <span data-ttu-id="8158f-111">在本教程中，你将看到一些使用存储库和适用于 CRUD 操作的工作单元模式的方法。</span><span class="sxs-lookup"><span data-stu-id="8158f-111">In this tutorial you'll see some ways to use the repository and unit of work patterns for CRUD operations.</span></span> <span data-ttu-id="8158f-112">如前面的教程中所述，在这种情况下，你将使用已创建的页面而不是创建新页面来更改代码的工作方式。</span><span class="sxs-lookup"><span data-stu-id="8158f-112">As in the previous tutorial, in this one you'll change the way your code works with pages you already created rather than creating new pages.</span></span>

## <a name="the-repository-and-unit-of-work-patterns"></a><span data-ttu-id="8158f-113">存储库和工作单元模式</span><span class="sxs-lookup"><span data-stu-id="8158f-113">The Repository and Unit of Work Patterns</span></span>

<span data-ttu-id="8158f-114">存储库和工作单元模式旨在创建数据访问层和应用程序的业务逻辑层之间的抽象层。</span><span class="sxs-lookup"><span data-stu-id="8158f-114">The repository and unit of work patterns are intended to create an abstraction layer between the data access layer and the business logic layer of an application.</span></span> <span data-ttu-id="8158f-115">实现这些模式可让你的应用程序对数据存储介质的更改不敏感，而且很容易进行自动化单元测试和进行测试驱动开发 (TDD)。</span><span class="sxs-lookup"><span data-stu-id="8158f-115">Implementing these patterns can help insulate your application from changes in the data store and can facilitate automated unit testing or test-driven development (TDD).</span></span>

<span data-ttu-id="8158f-116">在本教程中，您将为每个实体类型实现一个存储库类。</span><span class="sxs-lookup"><span data-stu-id="8158f-116">In this tutorial you'll implement a repository class for each entity type.</span></span> <span data-ttu-id="8158f-117">对于 `Student` 实体类型，你将创建一个存储库接口和一个存储库类。</span><span class="sxs-lookup"><span data-stu-id="8158f-117">For the `Student` entity type you'll create a repository interface and a repository class.</span></span> <span data-ttu-id="8158f-118">当你在控制器中实例化存储库时，将使用接口，以使控制器接受对实现存储库接口的任何对象的引用。</span><span class="sxs-lookup"><span data-stu-id="8158f-118">When you instantiate the repository in your controller, you'll use the interface so that the controller will accept a reference to any object that implements the repository interface.</span></span> <span data-ttu-id="8158f-119">当控制器在 web 服务器下运行时，它会收到与实体框架一起工作的存储库。</span><span class="sxs-lookup"><span data-stu-id="8158f-119">When the controller runs under a web server, it receives a repository that works with the Entity Framework.</span></span> <span data-ttu-id="8158f-120">当控制器在单元测试类下运行时，它会收到一个存储库，该存储过程可用于轻松地操作测试（例如内存中集合）的数据。</span><span class="sxs-lookup"><span data-stu-id="8158f-120">When the controller runs under a unit test class, it receives a repository that works with data stored in a way that you can easily manipulate for testing, such as an in-memory collection.</span></span>

<span data-ttu-id="8158f-121">稍后在本教程中，将使用多个存储库和 `Course` `Department` 控制器中的和实体类型的工作单元 `Course` 。</span><span class="sxs-lookup"><span data-stu-id="8158f-121">Later in the tutorial you'll use multiple repositories and a unit of work class for the `Course` and `Department` entity types in the `Course` controller.</span></span> <span data-ttu-id="8158f-122">工作单元通过创建所有存储库的工作方式来协调多个存储库的工作。</span><span class="sxs-lookup"><span data-stu-id="8158f-122">The unit of work class coordinates the work of multiple repositories by creating a single database context class shared by all of them.</span></span> <span data-ttu-id="8158f-123">如果希望能够执行自动单元测试，可以使用与存储库相同的方式为这些类创建和使用接口 `Student` 。</span><span class="sxs-lookup"><span data-stu-id="8158f-123">If you wanted to be able to perform automated unit testing, you'd create and use interfaces for these classes in the same way you did for the `Student` repository.</span></span> <span data-ttu-id="8158f-124">但是，为了简化本教程，你将创建并使用这些类，而无需使用接口。</span><span class="sxs-lookup"><span data-stu-id="8158f-124">However, to keep the tutorial simple, you'll create and use these classes without interfaces.</span></span>

<span data-ttu-id="8158f-125">下图显示了一种概念化控制器和上下文类之间的关系的方法，与根本不使用存储库或工作单元模式完全相同。</span><span class="sxs-lookup"><span data-stu-id="8158f-125">The following illustration shows one way to conceptualize the relationships between the controller and context classes compared to not using the repository or unit of work pattern at all.</span></span>

![Repository_pattern_diagram](https://asp.net/media/2578149/Windows-Live-Writer_8c4963ba1fa3_CE3B_Repository_pattern_diagram_1df790d3-bdf2-4c11-9098-946ddd9cd884.png)

<span data-ttu-id="8158f-127">不会在本系列教程中创建单元测试。</span><span class="sxs-lookup"><span data-stu-id="8158f-127">You won't create unit tests in this tutorial series.</span></span> <span data-ttu-id="8158f-128">有关使用使用存储库模式的 MVC 应用程序的 TDD 简介，请参阅 [演练：将 TDD 与 ASP.NET MVC 配合使用](https://msdn.microsoft.com/library/ff847525.aspx)。</span><span class="sxs-lookup"><span data-stu-id="8158f-128">For an introduction to TDD with an MVC application that uses the repository pattern, see [Walkthrough: Using TDD with ASP.NET MVC](https://msdn.microsoft.com/library/ff847525.aspx).</span></span> <span data-ttu-id="8158f-129">有关存储库模式的详细信息，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="8158f-129">For more information about the repository pattern, see the following resources:</span></span>

- <span data-ttu-id="8158f-130">MSDN 上[的存储库模式](https://msdn.microsoft.com/library/ff649690.aspx)。</span><span class="sxs-lookup"><span data-stu-id="8158f-130">[The Repository Pattern](https://msdn.microsoft.com/library/ff649690.aspx) on MSDN.</span></span>
- <span data-ttu-id="8158f-131">Julie Lerman 的博客上的[敏捷实体框架4存储库](http://thedatafarm.com/blog/data-access/agile-entity-framework-4-repository-part-1-model-and-poco-classes/)系列。</span><span class="sxs-lookup"><span data-stu-id="8158f-131">[Agile Entity Framework 4 Repository](http://thedatafarm.com/blog/data-access/agile-entity-framework-4-repository-part-1-model-and-poco-classes/) series of posts on Julie Lerman's blog.</span></span>
- <span data-ttu-id="8158f-132">在 Dan Wahlin 的博客上[快速生成 HTML5/JQuery 应用程序的帐户](https://weblogs.asp.net/dwahlin/archive/2011/08/15/building-the-account-at-a-glance-html5-jquery-application.aspx)。</span><span class="sxs-lookup"><span data-stu-id="8158f-132">[Building the Account at a Glance HTML5/jQuery Application](https://weblogs.asp.net/dwahlin/archive/2011/08/15/building-the-account-at-a-glance-html5-jquery-application.aspx) on Dan Wahlin's blog.</span></span>

> [!NOTE]
> <span data-ttu-id="8158f-133">可以通过多种方法实现存储库和工作单元模式。</span><span class="sxs-lookup"><span data-stu-id="8158f-133">There are many ways to implement the repository and unit of work patterns.</span></span> <span data-ttu-id="8158f-134">你可以使用或不带工作单位类的存储库类。</span><span class="sxs-lookup"><span data-stu-id="8158f-134">You can use repository classes with or without a unit of work class.</span></span> <span data-ttu-id="8158f-135">您可以为所有实体类型或每个类型分别实现一个存储库。</span><span class="sxs-lookup"><span data-stu-id="8158f-135">You can implement a single repository for all entity types, or one for each type.</span></span> <span data-ttu-id="8158f-136">如果为每个类型实现一个类型，则可以使用单独的类、泛型基类和派生类，或者使用抽象基类和派生类。</span><span class="sxs-lookup"><span data-stu-id="8158f-136">If you implement one for each type, you can use separate classes, a generic base class and derived classes, or an abstract base class and derived classes.</span></span> <span data-ttu-id="8158f-137">你可以在存储库中包含业务逻辑，或将其限制为数据访问逻辑。</span><span class="sxs-lookup"><span data-stu-id="8158f-137">You can include business logic in your repository or restrict it to data access logic.</span></span> <span data-ttu-id="8158f-138">还可以通过使用 [IDbSet](https://msdn.microsoft.com/library/gg679233(v=vs.103).aspx) 接口（而不是实体集的 [DbSet](https://msdn.microsoft.com/library/system.data.entity.dbset(v=vs.103).aspx) 类型）将抽象层生成到数据库上下文类中。</span><span class="sxs-lookup"><span data-stu-id="8158f-138">You can also build an abstraction layer into your database context class by using [IDbSet](https://msdn.microsoft.com/library/gg679233(v=vs.103).aspx) interfaces there instead of [DbSet](https://msdn.microsoft.com/library/system.data.entity.dbset(v=vs.103).aspx) types for your entity sets.</span></span> <span data-ttu-id="8158f-139">本教程中所示的实现抽象层的方法是一个选项，而不是针对所有方案和环境的建议。</span><span class="sxs-lookup"><span data-stu-id="8158f-139">The approach to implementing an abstraction layer shown in this tutorial is one option for you to consider, not a recommendation for all scenarios and environments.</span></span>

## <a name="creating-the-student-repository-class"></a><span data-ttu-id="8158f-140">创建 Student Repository 类</span><span class="sxs-lookup"><span data-stu-id="8158f-140">Creating the Student Repository Class</span></span>

<span data-ttu-id="8158f-141">在 *DAL* 文件夹中，创建一个名为 *IStudentRepository.cs* 的类文件，并将现有代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="8158f-141">In the *DAL* folder, create a class file named *IStudentRepository.cs* and replace the existing code with the following code:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample1.cs)]

<span data-ttu-id="8158f-142">此代码声明一组典型的 CRUD 方法，其中包括两个读取方法：一个返回所有 `Student` 实体，另一个用于 `Student` 按 ID 查找单个实体。</span><span class="sxs-lookup"><span data-stu-id="8158f-142">This code declares a typical set of CRUD methods, including two read methods — one that returns all `Student` entities, and one that finds a single `Student` entity by ID.</span></span>

<span data-ttu-id="8158f-143">在 *DAL* 文件夹中，创建一个名为 *StudentRepository.cs* 文件的类文件。</span><span class="sxs-lookup"><span data-stu-id="8158f-143">In the *DAL* folder, create a class file named *StudentRepository.cs* file.</span></span> <span data-ttu-id="8158f-144">将现有代码替换为以下代码，用于实现 `IStudentRepository` 接口：</span><span class="sxs-lookup"><span data-stu-id="8158f-144">Replace the existing code with the following code, which implements the `IStudentRepository` interface:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample2.cs)]

<span data-ttu-id="8158f-145">数据库上下文是在类变量中定义的，并且构造函数要求调用对象传入上下文的实例：</span><span class="sxs-lookup"><span data-stu-id="8158f-145">The database context is defined in a class variable, and the constructor expects the calling object to pass in an instance of the context:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample3.cs)]

<span data-ttu-id="8158f-146">你可以在存储库中实例化新的上下文，但是，如果在一个控制器中使用了多个存储库，则每个存储库都将使用单独的上下文。</span><span class="sxs-lookup"><span data-stu-id="8158f-146">You could instantiate a new context in the repository, but then if you used multiple repositories in one controller, each would end up with a separate context.</span></span> <span data-ttu-id="8158f-147">稍后你将在控制器中使用多个存储库 `Course` ，你将看到一个工作单元类如何确保所有存储库都使用同一上下文。</span><span class="sxs-lookup"><span data-stu-id="8158f-147">Later you'll use multiple repositories in the `Course` controller, and you'll see how a unit of work class can ensure that all repositories use the same context.</span></span>

<span data-ttu-id="8158f-148">存储库实现 [IDisposable](https://msdn.microsoft.com/library/system.idisposable.aspx) ，并按照前面在控制器中看到的方式释放数据库上下文，并且它的 CRUD 方法会以您之前看到的相同方式调用数据库上下文。</span><span class="sxs-lookup"><span data-stu-id="8158f-148">The repository implements [IDisposable](https://msdn.microsoft.com/library/system.idisposable.aspx) and disposes the database context as you saw earlier in the controller, and its CRUD methods make calls to the database context in the same way that you saw earlier.</span></span>

## <a name="change-the-student-controller-to-use-the-repository"></a><span data-ttu-id="8158f-149">更改学生控制器以使用存储库</span><span class="sxs-lookup"><span data-stu-id="8158f-149">Change the Student Controller to Use the Repository</span></span>

<span data-ttu-id="8158f-150">在 *StudentController.cs* 中，将类中当前的代码替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="8158f-150">In *StudentController.cs*, replace the code currently in the class with the following code.</span></span> <span data-ttu-id="8158f-151">突出显示所作更改。</span><span class="sxs-lookup"><span data-stu-id="8158f-151">The changes are highlighted.</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample4.cs?highlight=13-18,44,75,77,102-103,120,137-138,159,172-174,186)]

<span data-ttu-id="8158f-152">控制器现在为实现接口的对象 `IStudentRepository` （而不是上下文类）声明类变量：</span><span class="sxs-lookup"><span data-stu-id="8158f-152">The controller now declares a class variable for an object that implements the `IStudentRepository` interface instead of the context class:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample5.cs)]

<span data-ttu-id="8158f-153">默认 (无参数) 构造函数将创建一个新的上下文实例，而可选的构造函数允许调用方在上下文实例中传入。</span><span class="sxs-lookup"><span data-stu-id="8158f-153">The default (parameterless) constructor creates a new context instance, and an optional constructor allows the caller to pass in a context instance.</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample6.cs)]

<span data-ttu-id="8158f-154"> (如果使用的是 *依赖关系注入* 或 DI，则不需要默认构造函数，因为 DI 软件将确保始终提供正确的存储库对象。 ) </span><span class="sxs-lookup"><span data-stu-id="8158f-154">(If you were using *dependency injection*, or DI, you wouldn't need the default constructor because the DI software would ensure that the correct repository object would always be provided.)</span></span>

<span data-ttu-id="8158f-155">在 CRUD 方法中，现在将调用存储库，而不是上下文：</span><span class="sxs-lookup"><span data-stu-id="8158f-155">In the CRUD methods, the repository is now called instead of the context:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample7.cs)]

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample8.cs)]

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample9.cs)]

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample10.cs)]

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample11.cs)]

<span data-ttu-id="8158f-156">现在， `Dispose` 方法会释放存储库，而不是上下文：</span><span class="sxs-lookup"><span data-stu-id="8158f-156">And the `Dispose` method now disposes the repository instead of the context:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample12.cs)]

<span data-ttu-id="8158f-157">运行站点并单击 " **学生** " 选项卡。</span><span class="sxs-lookup"><span data-stu-id="8158f-157">Run the site and click the **Students** tab.</span></span>

![Students_Index_page](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/_static/image1.png)

<span data-ttu-id="8158f-159">页面的外观和工作方式与您将代码更改为使用存储库之前的效果相同，并且其他学生页面也工作正常。</span><span class="sxs-lookup"><span data-stu-id="8158f-159">The page looks and works the same as it did before you changed the code to use the repository, and the other Student pages also work the same.</span></span> <span data-ttu-id="8158f-160">但是， `Index` 控制器方法进行筛选和排序的方式有很大的差异。</span><span class="sxs-lookup"><span data-stu-id="8158f-160">However, there's an important difference in the way the `Index` method of the controller does filtering and ordering.</span></span> <span data-ttu-id="8158f-161">此方法的原始版本包含以下代码：</span><span class="sxs-lookup"><span data-stu-id="8158f-161">The original version of this method contained the following code:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample13.cs?highlight=1)]

<span data-ttu-id="8158f-162">更新的 `Index` 方法包含以下代码：</span><span class="sxs-lookup"><span data-stu-id="8158f-162">The updated `Index` method contains the following code:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample14.cs?highlight=1)]

<span data-ttu-id="8158f-163">仅突出显示的代码已更改。</span><span class="sxs-lookup"><span data-stu-id="8158f-163">Only the highlighted code has changed.</span></span>

<span data-ttu-id="8158f-164">在代码的原始版本中， `students` 类型化为 `IQueryable` 对象。</span><span class="sxs-lookup"><span data-stu-id="8158f-164">In the original version of the code, `students` is typed as an `IQueryable` object.</span></span> <span data-ttu-id="8158f-165">直到使用诸如这样的方法将查询转换为集合后，才会将其发送到数据库 `ToList` 中，这种情况在索引视图访问学生模型之前不会出现。</span><span class="sxs-lookup"><span data-stu-id="8158f-165">The query isn't sent to the database until it's converted into a collection using a method such as `ToList`, which doesn't occur until the Index view accesses the student model.</span></span> <span data-ttu-id="8158f-166">`Where`上面原始代码中的方法成为 `WHERE` 发送到数据库的 SQL 查询中的子句。</span><span class="sxs-lookup"><span data-stu-id="8158f-166">The `Where` method in the original code above becomes a `WHERE` clause in the SQL query that is sent to the database.</span></span> <span data-ttu-id="8158f-167">这反过来意味着，数据库仅返回选定的实体。</span><span class="sxs-lookup"><span data-stu-id="8158f-167">That in turn means that only the selected entities are returned by the database.</span></span> <span data-ttu-id="8158f-168">但是，在更改 `context.Students` 为 `studentRepository.GetStudents()` `students` 之后，该语句后的变量是 `IEnumerable` 包含数据库中所有学生的集合。</span><span class="sxs-lookup"><span data-stu-id="8158f-168">However, as a result of changing `context.Students` to `studentRepository.GetStudents()`, the `students` variable after this statement is an `IEnumerable` collection that includes all students in the database.</span></span> <span data-ttu-id="8158f-169">应用方法的最终结果 `Where` 是相同的，但现在工作是在 web 服务器上的内存中完成的，而不是在数据库中完成。</span><span class="sxs-lookup"><span data-stu-id="8158f-169">The end result of applying the `Where` method is the same, but now the work is done in memory on the web server and not by the database.</span></span> <span data-ttu-id="8158f-170">对于返回大量数据的查询，这可能会降低效率。</span><span class="sxs-lookup"><span data-stu-id="8158f-170">For queries that return large volumes of data, this can be inefficient.</span></span>

> [!TIP]
> 
> <span data-ttu-id="8158f-171">**IQueryable vs.IEnumerable**</span><span class="sxs-lookup"><span data-stu-id="8158f-171">**IQueryable vs. IEnumerable**</span></span>
> 
> <span data-ttu-id="8158f-172">实现此存储库后，即使在 **搜索** 框中输入了内容，查询发送到 SQL Server 也会返回所有学生行，因为它不包含搜索条件：</span><span class="sxs-lookup"><span data-stu-id="8158f-172">After you implement the repository as shown here, even if you enter something in the **Search** box the query sent to SQL Server returns all Student rows because it doesn't include your search criteria:</span></span>
> 
> ![](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/_static/image2.png)
> 
> [!code-sql[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample15.sql)]
> 
> <span data-ttu-id="8158f-173">此查询将返回所有学生数据，因为存储库执行查询时未了解搜索条件。</span><span class="sxs-lookup"><span data-stu-id="8158f-173">This query returns all of the student data because the repository executed the query without knowing about the search criteria.</span></span> <span data-ttu-id="8158f-174">在这种情况下，排序、应用搜索条件以及选择数据的子集以进行分页 (仅在此情况下才会显示3行) 在该集合中调用方法时在内存中完成 `ToPagedList` `IEnumerable` 。</span><span class="sxs-lookup"><span data-stu-id="8158f-174">The process of sorting, applying search criteria, and selecting a subset of the data for paging (showing only 3 rows in this case) is done in memory later when the `ToPagedList` method is called on the `IEnumerable` collection.</span></span>
> 
> <span data-ttu-id="8158f-175">在之前版本的代码中 (在实现存储库之前) ，在应用搜索条件后，在对对象调用时，该查询才会发送到数据库 `ToPagedList` `IQueryable` 。</span><span class="sxs-lookup"><span data-stu-id="8158f-175">In the previous version of the code (before you implemented the repository), the query is not sent to the database until after you apply the search criteria, when `ToPagedList` is called on the `IQueryable` object.</span></span>
> 
> ![](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/_static/image3.png)
> 
> <span data-ttu-id="8158f-176">当对某个对象调用 ToPagedList 时 `IQueryable` ，发送给 SQL Server 的查询将指定搜索字符串，因此，仅返回满足搜索条件的行，并且不需要在内存中执行任何筛选。</span><span class="sxs-lookup"><span data-stu-id="8158f-176">When ToPagedList is called on an `IQueryable` object, the query sent to SQL Server specifies the search string, and as a result only rows that meet the search criteria are returned, and no filtering needs to be done in memory.</span></span>
> 
> [!code-sql[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample16.sql)]
> 
> <span data-ttu-id="8158f-177"> (以下教程介绍了如何检查发送到 SQL Server 的查询。 ) </span><span class="sxs-lookup"><span data-stu-id="8158f-177">(The following tutorial explains how to examine queries sent to SQL Server.)</span></span>

<span data-ttu-id="8158f-178">以下部分演示如何实现存储库方法，使用这些方法可以指定数据库应执行此操作。</span><span class="sxs-lookup"><span data-stu-id="8158f-178">The following section shows how to implement repository methods that enable you to specify that this work should be done by the database.</span></span>

<span data-ttu-id="8158f-179">你现在已在控制器和实体框架数据库上下文之间创建了一个抽象层。</span><span class="sxs-lookup"><span data-stu-id="8158f-179">You've now created an abstraction layer between the controller and the Entity Framework database context.</span></span> <span data-ttu-id="8158f-180">如果要使用此应用程序执行自动单元测试，可以在实现的单元测试项目中创建备用存储库类 `IStudentRepository` *。*</span><span class="sxs-lookup"><span data-stu-id="8158f-180">If you were going to perform automated unit testing with this application, you could create an alternative repository class in a unit test project that implements `IStudentRepository`*.*</span></span> <span data-ttu-id="8158f-181">此 mock 存储库类可以操作内存中集合，而不是调用上下文来读取和写入数据，而是为了测试控制器函数。</span><span class="sxs-lookup"><span data-stu-id="8158f-181">Instead of calling the context to read and write data, this mock repository class could manipulate in-memory collections in order to test controller functions.</span></span>

## <a name="implement-a-generic-repository-and-a-unit-of-work-class"></a><span data-ttu-id="8158f-182">实现一个通用存储库和一个工作单元类</span><span class="sxs-lookup"><span data-stu-id="8158f-182">Implement a Generic Repository and a Unit of Work Class</span></span>

<span data-ttu-id="8158f-183">为每个实体类型创建存储库类可能会导致大量冗余代码，并可能导致部分更新。</span><span class="sxs-lookup"><span data-stu-id="8158f-183">Creating a repository class for each entity type could result in a lot of redundant code, and it could result in partial updates.</span></span> <span data-ttu-id="8158f-184">例如，假设您必须将两个不同的实体类型更新为同一事务的一部分。</span><span class="sxs-lookup"><span data-stu-id="8158f-184">For example, suppose you have to update two different entity types as part of the same transaction.</span></span> <span data-ttu-id="8158f-185">如果每个都使用单独的数据库上下文实例，则可能会成功，而另一个可能会失败。</span><span class="sxs-lookup"><span data-stu-id="8158f-185">If each uses a separate database context instance, one might succeed and the other might fail.</span></span> <span data-ttu-id="8158f-186">最大程度地减少冗余代码的一种方法是使用通用存储库，并确保所有存储库都使用相同的数据库上下文 (，从而协调所有更新) 使用工作单元。</span><span class="sxs-lookup"><span data-stu-id="8158f-186">One way to minimize redundant code is to use a generic repository, and one way to ensure that all repositories use the same database context (and thus coordinate all updates) is to use a unit of work class.</span></span>

<span data-ttu-id="8158f-187">在本教程的此部分中，你将创建一个 `GenericRepository` 类和一个 `UnitOfWork` 类，并在控制器中使用它们 `Course` 来访问 `Department` 和 `Course` 实体集。</span><span class="sxs-lookup"><span data-stu-id="8158f-187">In this section of the tutorial, you'll create a `GenericRepository` class and a `UnitOfWork` class, and use them in the `Course` controller to access both the `Department` and the `Course` entity sets.</span></span> <span data-ttu-id="8158f-188">如前文所述，若要使本教程的这一部分简单，你不会为这些类创建接口。</span><span class="sxs-lookup"><span data-stu-id="8158f-188">As explained earlier, to keep this part of the tutorial simple, you aren't creating interfaces for these classes.</span></span> <span data-ttu-id="8158f-189">但是，如果您打算使用它们来促进 TDD，则通常使用与存储库相同的方式来实现这些接口 `Student` 。</span><span class="sxs-lookup"><span data-stu-id="8158f-189">But if you were going to use them to facilitate TDD, you'd typically implement them with interfaces the same way you did the `Student` repository.</span></span>

### <a name="create-a-generic-repository"></a><span data-ttu-id="8158f-190">创建通用存储库</span><span class="sxs-lookup"><span data-stu-id="8158f-190">Create a Generic Repository</span></span>

<span data-ttu-id="8158f-191">在 *DAL* 文件夹中，创建 *GenericRepository.cs* ，并将现有代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="8158f-191">In the *DAL* folder, create *GenericRepository.cs* and replace the existing code with the following code:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample17.cs)]

<span data-ttu-id="8158f-192">为数据库上下文和存储库实例化的实体集声明类变量：</span><span class="sxs-lookup"><span data-stu-id="8158f-192">Class variables are declared for the database context and for the entity set that the repository is instantiated for:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample18.cs)]

<span data-ttu-id="8158f-193">构造函数接受数据库上下文实例并初始化实体集变量：</span><span class="sxs-lookup"><span data-stu-id="8158f-193">The constructor accepts a database context instance and initializes the entity set variable:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample19.cs)]

<span data-ttu-id="8158f-194">`Get`方法使用 lambda 表达式来允许调用代码指定筛选条件，并使用一列来对结果进行排序，而字符串参数则允许调用方为预先加载提供以逗号分隔的导航属性列表：</span><span class="sxs-lookup"><span data-stu-id="8158f-194">The `Get` method uses lambda expressions to allow the calling code to specify a filter condition and a column to order the results by, and a string parameter lets the caller provide a comma-delimited list of navigation properties for eager loading:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample20.cs)]

<span data-ttu-id="8158f-195">此代码 `Expression<Func<TEntity, bool>> filter` 意味着调用方将基于该类型提供 lambda 表达式 `TEntity` ，并且此表达式将返回一个布尔值。</span><span class="sxs-lookup"><span data-stu-id="8158f-195">The code `Expression<Func<TEntity, bool>> filter` means the caller will provide a lambda expression based on the `TEntity` type, and this expression will return a Boolean value.</span></span> <span data-ttu-id="8158f-196">例如，如果存储库是针对实体类型实例化的 `Student` ，则调用方法中的代码可能 `student => student.LastName == "Smith` &quot; 为参数指定 `filter` 。</span><span class="sxs-lookup"><span data-stu-id="8158f-196">For example, if the repository is instantiated for the `Student` entity type, the code in the calling method might specify `student => student.LastName == "Smith`&quot; for the `filter` parameter.</span></span>

<span data-ttu-id="8158f-197">此代码 `Func<IQueryable<TEntity>, IOrderedQueryable<TEntity>> orderBy` 还意味着调用方将提供 lambda 表达式。</span><span class="sxs-lookup"><span data-stu-id="8158f-197">The code `Func<IQueryable<TEntity>, IOrderedQueryable<TEntity>> orderBy` also means the caller will provide a lambda expression.</span></span> <span data-ttu-id="8158f-198">但在这种情况下，表达式的输入是 `IQueryable` 该类型的对象 `TEntity` 。</span><span class="sxs-lookup"><span data-stu-id="8158f-198">But in this case, the input to the expression is an `IQueryable` object for the `TEntity` type.</span></span> <span data-ttu-id="8158f-199">表达式将返回该对象的有序版本 `IQueryable` 。</span><span class="sxs-lookup"><span data-stu-id="8158f-199">The expression will return an ordered version of that `IQueryable` object.</span></span> <span data-ttu-id="8158f-200">例如，如果存储库是针对实体类型实例化的 `Student` ，则调用方法中的代码可能 `q => q.OrderBy(s => s.LastName)` 为参数指定 `orderBy` 。</span><span class="sxs-lookup"><span data-stu-id="8158f-200">For example, if the repository is instantiated for the `Student` entity type, the code in the calling method might specify `q => q.OrderBy(s => s.LastName)` for the `orderBy` parameter.</span></span>

<span data-ttu-id="8158f-201">方法中的代码 `Get` 会创建一个 `IQueryable` 对象，然后应用筛选器表达式（如果有）：</span><span class="sxs-lookup"><span data-stu-id="8158f-201">The code in the `Get` method creates an `IQueryable` object and then applies the filter expression if there is one:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample21.cs)]

<span data-ttu-id="8158f-202">接下来，它会在分析以逗号分隔的列表后应用预先加载的表达式：</span><span class="sxs-lookup"><span data-stu-id="8158f-202">Next it applies the eager-loading expressions after parsing the comma-delimited list:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample22.cs)]

<span data-ttu-id="8158f-203">最后，它将应用 `orderBy` 表达式（如果有）并返回结果; 否则返回无序查询的结果：</span><span class="sxs-lookup"><span data-stu-id="8158f-203">Finally, it applies the `orderBy` expression if there is one and returns the results; otherwise it returns the results from the unordered query:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample23.cs)]

<span data-ttu-id="8158f-204">当调用方法时 `Get` ，您可以对由方法返回的集合进行筛选和排序， `IEnumerable` 而不是为这些函数提供参数。</span><span class="sxs-lookup"><span data-stu-id="8158f-204">When you call the `Get` method, you could do filtering and sorting on the `IEnumerable` collection returned by the method instead of providing parameters for these functions.</span></span> <span data-ttu-id="8158f-205">但排序和筛选工作就会在 web 服务器的内存中完成。</span><span class="sxs-lookup"><span data-stu-id="8158f-205">But the sorting and filtering work would then be done in memory on the web server.</span></span> <span data-ttu-id="8158f-206">通过使用这些参数，可以确保由数据库而不是 web 服务器来完成工作。</span><span class="sxs-lookup"><span data-stu-id="8158f-206">By using these parameters, you ensure that the work is done by the database rather than the web server.</span></span> <span data-ttu-id="8158f-207">一种替代方法是为特定实体类型创建派生类并添加专用 `Get` 方法，如 `GetStudentsInNameOrder` 或 `GetStudentsByName` 。</span><span class="sxs-lookup"><span data-stu-id="8158f-207">An alternative is to create derived classes for specific entity types and add specialized `Get` methods, such as `GetStudentsInNameOrder` or `GetStudentsByName`.</span></span> <span data-ttu-id="8158f-208">但是，在复杂应用程序中，这可能会导致大量的此类派生类和专用方法，这可能更适合维护。</span><span class="sxs-lookup"><span data-stu-id="8158f-208">However, in a complex application, this can result in a large number of such derived classes and specialized methods, which could be more work to maintain.</span></span>

<span data-ttu-id="8158f-209">`GetByID`、和方法中的代码 `Insert` 与在 `Update` 非泛型存储库中看到的代码类似。</span><span class="sxs-lookup"><span data-stu-id="8158f-209">The code in the `GetByID`, `Insert`, and `Update` methods is similar to what you saw in the non-generic repository.</span></span> <span data-ttu-id="8158f-210"> (不会在签名中提供预先加载参数 `GetByID` ，因为不能使用方法进行预先加载 `Find` 。 ) </span><span class="sxs-lookup"><span data-stu-id="8158f-210">(You aren't providing an eager loading parameter in the `GetByID` signature, because you can't do eager loading with the `Find` method.)</span></span>

<span data-ttu-id="8158f-211">为方法提供了两个重载 `Delete` ：</span><span class="sxs-lookup"><span data-stu-id="8158f-211">Two overloads are provided for the `Delete` method:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample24.cs)]

<span data-ttu-id="8158f-212">其中一种方式可让你只传入要删除的实体的 ID，另一种是使用实体实例。</span><span class="sxs-lookup"><span data-stu-id="8158f-212">One of these lets you pass in just the ID of the entity to be deleted, and one takes an entity instance.</span></span> <span data-ttu-id="8158f-213">正如在 [处理并发](../../getting-started/getting-started-with-ef-using-mvc/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md) 教程中看到的那样，对于并发处理，需要一个 `Delete` 采用包含跟踪属性原始值的实体实例的方法。</span><span class="sxs-lookup"><span data-stu-id="8158f-213">As you saw in the [Handling Concurrency](../../getting-started/getting-started-with-ef-using-mvc/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md) tutorial, for concurrency handling you need a `Delete` method that takes an entity instance that includes the original value of a tracking property.</span></span>

<span data-ttu-id="8158f-214">此通用存储库将处理典型的 CRUD 要求。</span><span class="sxs-lookup"><span data-stu-id="8158f-214">This generic repository will handle typical CRUD requirements.</span></span> <span data-ttu-id="8158f-215">当特定实体类型具有特殊要求（如更复杂的筛选或排序）时，可以创建一个具有该类型附加方法的派生类。</span><span class="sxs-lookup"><span data-stu-id="8158f-215">When a particular entity type has special requirements, such as more complex filtering or ordering, you can create a derived class that has additional methods for that type.</span></span>

## <a name="creating-the-unit-of-work-class"></a><span data-ttu-id="8158f-216">创建工作单元类</span><span class="sxs-lookup"><span data-stu-id="8158f-216">Creating the Unit of Work Class</span></span>

<span data-ttu-id="8158f-217">工作单元类可用于：确保在使用多个存储库时，它们共享单个数据库上下文。</span><span class="sxs-lookup"><span data-stu-id="8158f-217">The unit of work class serves one purpose: to make sure that when you use multiple repositories, they share a single database context.</span></span> <span data-ttu-id="8158f-218">这样一来，当工作单元完成时，你可以 `SaveChanges` 在该上下文实例上调用方法，并确保所有相关更改都将进行协调。</span><span class="sxs-lookup"><span data-stu-id="8158f-218">That way, when a unit of work is complete you can call the `SaveChanges` method on that instance of the context and be assured that all related changes will be coordinated.</span></span> <span data-ttu-id="8158f-219">类所需的全部都是 `Save` 每个存储库的方法和属性。</span><span class="sxs-lookup"><span data-stu-id="8158f-219">All that the class needs is a `Save` method and a property for each repository.</span></span> <span data-ttu-id="8158f-220">每个存储库属性返回一个存储库实例，该实例已使用与其他存储库实例相同的数据库上下文实例实例化。</span><span class="sxs-lookup"><span data-stu-id="8158f-220">Each repository property returns a repository instance that has been instantiated using the same database context instance as the other repository instances.</span></span>

<span data-ttu-id="8158f-221">在 *DAL* 文件夹中，创建一个名为 *UnitOfWork.cs* 的类文件，并将模板代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="8158f-221">In the *DAL* folder, create a class file named *UnitOfWork.cs* and replace the template code with the following code:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample25.cs)]

<span data-ttu-id="8158f-222">此代码为数据库上下文和每个存储库创建类变量。</span><span class="sxs-lookup"><span data-stu-id="8158f-222">The code creates class variables for the database context and each repository.</span></span> <span data-ttu-id="8158f-223">对于 `context` 变量，会实例化一个新上下文：</span><span class="sxs-lookup"><span data-stu-id="8158f-223">For the `context` variable, a new context is instantiated:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample26.cs)]

<span data-ttu-id="8158f-224">每个存储库属性检查存储库是否已存在。</span><span class="sxs-lookup"><span data-stu-id="8158f-224">Each repository property checks whether the repository already exists.</span></span> <span data-ttu-id="8158f-225">如果不是，则会实例化存储库，并传入上下文实例。</span><span class="sxs-lookup"><span data-stu-id="8158f-225">If not, it instantiates the repository, passing in the context instance.</span></span> <span data-ttu-id="8158f-226">因此，所有存储库共享相同的上下文实例。</span><span class="sxs-lookup"><span data-stu-id="8158f-226">As a result, all repositories share the same context instance.</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample27.cs)]

<span data-ttu-id="8158f-227">`Save`方法调用 `SaveChanges` 数据库上下文。</span><span class="sxs-lookup"><span data-stu-id="8158f-227">The `Save` method calls `SaveChanges` on the database context.</span></span>

<span data-ttu-id="8158f-228">与在类变量中实例化数据库上下文的任何类一样， `UnitOfWork` 类实现 `IDisposable` 并释放上下文。</span><span class="sxs-lookup"><span data-stu-id="8158f-228">Like any class that instantiates a database context in a class variable, the `UnitOfWork` class implements `IDisposable` and disposes the context.</span></span>

### <a name="changing-the-course-controller-to-use-the-unitofwork-class-and-repositories"></a><span data-ttu-id="8158f-229">更改课程控制器以使用 UnitOfWork 类和存储库</span><span class="sxs-lookup"><span data-stu-id="8158f-229">Changing the Course Controller to use the UnitOfWork Class and Repositories</span></span>

<span data-ttu-id="8158f-230">使用以下代码替换 *CourseController.cs* 中当前具有的代码：</span><span class="sxs-lookup"><span data-stu-id="8158f-230">Replace the code you currently have in *CourseController.cs* with the following code:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample28.cs?highlight=15,20,22,31,54-55,70,85-86,101-102,122-124,130)]

<span data-ttu-id="8158f-231">此代码将为类添加类变量 `UnitOfWork` 。</span><span class="sxs-lookup"><span data-stu-id="8158f-231">This code adds a class variable for the `UnitOfWork` class.</span></span> <span data-ttu-id="8158f-232"> (如果使用的是接口，则不会在此处初始化变量;相反，您需要实现两个构造函数的模式，就像对存储库执行的操作一样 `Student` 。 ) </span><span class="sxs-lookup"><span data-stu-id="8158f-232">(If you were using interfaces here, you wouldn't initialize the variable here; instead, you'd implement a pattern of two constructors just as you did for the `Student` repository.)</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample29.cs)]

<span data-ttu-id="8158f-233">在类的其余部分中，对数据库上下文的所有引用都将替换为对相应存储库的引用，并使用 `UnitOfWork` 属性访问存储库。</span><span class="sxs-lookup"><span data-stu-id="8158f-233">In the rest of the class, all references to the database context are replaced by references to the appropriate repository, using `UnitOfWork` properties to access the repository.</span></span> <span data-ttu-id="8158f-234">`Dispose`方法释放 `UnitOfWork` 实例。</span><span class="sxs-lookup"><span data-stu-id="8158f-234">The `Dispose` method disposes the `UnitOfWork` instance.</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample30.cs)]

<span data-ttu-id="8158f-235">运行站点并单击 " **课程** " 选项卡。</span><span class="sxs-lookup"><span data-stu-id="8158f-235">Run the site and click the **Courses** tab.</span></span>

![Courses_Index_page](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/_static/image4.png)

<span data-ttu-id="8158f-237">页面的外观和工作方式与更改之前的效果相同，并且其他课程页面也相同。</span><span class="sxs-lookup"><span data-stu-id="8158f-237">The page looks and works the same as it did before your changes, and the other Course pages also work the same.</span></span>

## <a name="summary"></a><span data-ttu-id="8158f-238">总结</span><span class="sxs-lookup"><span data-stu-id="8158f-238">Summary</span></span>

<span data-ttu-id="8158f-239">现在，已实现存储库和工作单元模式。</span><span class="sxs-lookup"><span data-stu-id="8158f-239">You have now implemented both the repository and unit of work patterns.</span></span> <span data-ttu-id="8158f-240">已使用 lambda 表达式作为泛型存储库中的方法参数。</span><span class="sxs-lookup"><span data-stu-id="8158f-240">You have used lambda expressions as method parameters in the generic repository.</span></span> <span data-ttu-id="8158f-241">有关如何在对象中使用这些表达式的详细信息 `IQueryable` ，请参阅 MSDN Library 中的 [IQueryable (T) Interface () ](https://msdn.microsoft.com/library/bb351562.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="8158f-241">For more information about how to use these expressions with an `IQueryable` object, see [IQueryable(T) Interface (System.Linq)](https://msdn.microsoft.com/library/bb351562.aspx) in the MSDN Library.</span></span> <span data-ttu-id="8158f-242">在下一教程中，你将学习如何处理一些高级方案。</span><span class="sxs-lookup"><span data-stu-id="8158f-242">In the next tutorial you'll learn how to handle some advanced scenarios.</span></span>

<span data-ttu-id="8158f-243">可在 [ASP.NET 数据访问内容映射](../../../../whitepapers/aspnet-data-access-content-map.md)中找到指向其他实体框架资源的链接。</span><span class="sxs-lookup"><span data-stu-id="8158f-243">Links to other Entity Framework resources can be found in the [ASP.NET Data Access Content Map](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="8158f-244">[上一页](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md)
> [下一页](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)</span><span class="sxs-lookup"><span data-stu-id="8158f-244">[Previous](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md)
[Next](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)</span></span>

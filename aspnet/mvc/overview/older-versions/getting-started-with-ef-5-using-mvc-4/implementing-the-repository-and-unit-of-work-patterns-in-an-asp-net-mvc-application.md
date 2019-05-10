---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application
title: 在 ASP.NET MVC 应用程序 (共 10 个 9) 中实现存储库和工作单元模式 |Microsoft Docs
author: tdykstra
description: Contoso 大学示例 web 应用程序演示如何创建使用 Entity Framework 5 Code First 和 Visual Studio 的 ASP.NET MVC 4 应用程序...
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 44761193-04ba-4990-9f90-145d3c10a716
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: d0d6c9dd5234c8085b5c1dea5552854486314010
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/06/2019
ms.locfileid: "65129774"
---
# <a name="implementing-the-repository-and-unit-of-work-patterns-in-an-aspnet-mvc-application-9-of-10"></a><span data-ttu-id="96470-103">在 ASP.NET MVC 应用程序 (共 10 个 9) 中实现存储库和工作单元模式</span><span class="sxs-lookup"><span data-stu-id="96470-103">Implementing the Repository and Unit of Work Patterns in an ASP.NET MVC Application (9 of 10)</span></span>

<span data-ttu-id="96470-104">通过[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="96470-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="96470-105">下载已完成的项目</span><span class="sxs-lookup"><span data-stu-id="96470-105">Download Completed Project</span></span>](http://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> <span data-ttu-id="96470-106">Contoso 大学示例 web 应用程序演示如何创建使用 Entity Framework 5 Code First 和 Visual Studio 2012 的 ASP.NET MVC 4 应用程序。</span><span class="sxs-lookup"><span data-stu-id="96470-106">The Contoso University sample web application demonstrates how to create ASP.NET MVC 4 applications using the Entity Framework 5 Code First and Visual Studio 2012.</span></span> <span data-ttu-id="96470-107">若要了解系列教程，请参阅[本系列中的第一个教程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。</span><span class="sxs-lookup"><span data-stu-id="96470-107">For information about the tutorial series, see [the first tutorial in the series](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span> <span data-ttu-id="96470-108">您可以从头开始的系列教程或[下载本章节的初学者项目](building-the-ef5-mvc4-chapter-downloads.md)并从这里开始。</span><span class="sxs-lookup"><span data-stu-id="96470-108">You can start the tutorial series from the beginning or [download a starter project for this chapter](building-the-ef5-mvc4-chapter-downloads.md) and start here.</span></span>
> 
> > [!NOTE] 
> > 
> > <span data-ttu-id="96470-109">如果遇到无法解决的问题[下载已完成的一章](building-the-ef5-mvc4-chapter-downloads.md)并尝试重现你的问题。</span><span class="sxs-lookup"><span data-stu-id="96470-109">If you run into a problem you can't resolve, [download the completed chapter](building-the-ef5-mvc4-chapter-downloads.md) and try to reproduce your problem.</span></span> <span data-ttu-id="96470-110">通过比较您的代码与已完成的代码，通常可以找到问题的解决方案。</span><span class="sxs-lookup"><span data-stu-id="96470-110">You can generally find the solution to the problem by comparing your code to the completed code.</span></span> <span data-ttu-id="96470-111">一些常见错误以及如何解决这些问题，请参阅[错误和解决方法。](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)</span><span class="sxs-lookup"><span data-stu-id="96470-111">For some common errors and how to solve them, see [Errors and Workarounds.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)</span></span>

<span data-ttu-id="96470-112">在上一教程中使用继承来减少冗余代码中的`Student`和`Instructor`实体类。</span><span class="sxs-lookup"><span data-stu-id="96470-112">In the previous tutorial you used inheritance to reduce redundant code in the `Student` and `Instructor` entity classes.</span></span> <span data-ttu-id="96470-113">在本教程中，您将看到的 CRUD 操作使用的存储库和工作单元模式的一些方法。</span><span class="sxs-lookup"><span data-stu-id="96470-113">In this tutorial you'll see some ways to use the repository and unit of work patterns for CRUD operations.</span></span> <span data-ttu-id="96470-114">如前面的教程中所示在此将更改你的代码适用于页你已创建而不是创建新的页的方式。</span><span class="sxs-lookup"><span data-stu-id="96470-114">As in the previous tutorial, in this one you'll change the way your code works with pages you already created rather than creating new pages.</span></span>

## <a name="the-repository-and-unit-of-work-patterns"></a><span data-ttu-id="96470-115">存储库和工作单元模式</span><span class="sxs-lookup"><span data-stu-id="96470-115">The Repository and Unit of Work Patterns</span></span>

<span data-ttu-id="96470-116">存储库和工作单元模式旨在创建数据访问层和应用程序的业务逻辑层之间的抽象层。</span><span class="sxs-lookup"><span data-stu-id="96470-116">The repository and unit of work patterns are intended to create an abstraction layer between the data access layer and the business logic layer of an application.</span></span> <span data-ttu-id="96470-117">实现这些模式可让你的应用程序对数据存储介质的更改不敏感，而且很容易进行自动化单元测试和进行测试驱动开发 (TDD)。</span><span class="sxs-lookup"><span data-stu-id="96470-117">Implementing these patterns can help insulate your application from changes in the data store and can facilitate automated unit testing or test-driven development (TDD).</span></span>

<span data-ttu-id="96470-118">在本教程中将实现每个实体类型的存储库类。</span><span class="sxs-lookup"><span data-stu-id="96470-118">In this tutorial you'll implement a repository class for each entity type.</span></span> <span data-ttu-id="96470-119">有关`Student`您将创建一个存储库接口和存储库类的实体类型。</span><span class="sxs-lookup"><span data-stu-id="96470-119">For the `Student` entity type you'll create a repository interface and a repository class.</span></span> <span data-ttu-id="96470-120">当你在控制器中实例化存储库时，您将使用接口，以便在控制器将接受任何实现存储库接口的对象的引用。</span><span class="sxs-lookup"><span data-stu-id="96470-120">When you instantiate the repository in your controller, you'll use the interface so that the controller will accept a reference to any object that implements the repository interface.</span></span> <span data-ttu-id="96470-121">当控制器在 web 服务器下运行时，它将接收适用于实体框架的存储库。</span><span class="sxs-lookup"><span data-stu-id="96470-121">When the controller runs under a web server, it receives a repository that works with the Entity Framework.</span></span> <span data-ttu-id="96470-122">当控制器在单元测试类下运行时，它将接收适用于您可以轻松地操作进行测试，例如内存中集合的方式存储的数据的存储库。</span><span class="sxs-lookup"><span data-stu-id="96470-122">When the controller runs under a unit test class, it receives a repository that works with data stored in a way that you can easily manipulate for testing, such as an in-memory collection.</span></span>

<span data-ttu-id="96470-123">本教程的后面将使用多个存储库和工作类的一个单元`Course`并`Department`中的实体类型`Course`控制器。</span><span class="sxs-lookup"><span data-stu-id="96470-123">Later in the tutorial you'll use multiple repositories and a unit of work class for the `Course` and `Department` entity types in the `Course` controller.</span></span> <span data-ttu-id="96470-124">单位工作类通过创建由所有这些共享的单个数据库上下文类协调多个存储库的工作。</span><span class="sxs-lookup"><span data-stu-id="96470-124">The unit of work class coordinates the work of multiple repositories by creating a single database context class shared by all of them.</span></span> <span data-ttu-id="96470-125">如果你想要能够执行自动化的单元测试，您可以创建并与你对相同的方式使用这些类的接口`Student`存储库。</span><span class="sxs-lookup"><span data-stu-id="96470-125">If you wanted to be able to perform automated unit testing, you'd create and use interfaces for these classes in the same way you did for the `Student` repository.</span></span> <span data-ttu-id="96470-126">但是，为了简化本教程，将创建和使用这些类没有接口。</span><span class="sxs-lookup"><span data-stu-id="96470-126">However, to keep the tutorial simple, you'll create and use these classes without interfaces.</span></span>

<span data-ttu-id="96470-127">下图显示了概念化控制器和到不在所有使用的存储库或工作单元模式进行比较的上下文类之间的关系的一种方法。</span><span class="sxs-lookup"><span data-stu-id="96470-127">The following illustration shows one way to conceptualize the relationships between the controller and context classes compared to not using the repository or unit of work pattern at all.</span></span>

![Repository_pattern_diagram](https://asp.net/media/2578149/Windows-Live-Writer_8c4963ba1fa3_CE3B_Repository_pattern_diagram_1df790d3-bdf2-4c11-9098-946ddd9cd884.png)

<span data-ttu-id="96470-129">在本系列教程中，不会创建单元测试。</span><span class="sxs-lookup"><span data-stu-id="96470-129">You won't create unit tests in this tutorial series.</span></span> <span data-ttu-id="96470-130">有关使用存储库模式的 MVC 应用程序使用 TDD 的介绍，请参阅[演练：ASP.NET MVC 中使用 TDD](https://msdn.microsoft.com/library/ff847525.aspx)。</span><span class="sxs-lookup"><span data-stu-id="96470-130">For an introduction to TDD with an MVC application that uses the repository pattern, see [Walkthrough: Using TDD with ASP.NET MVC](https://msdn.microsoft.com/library/ff847525.aspx).</span></span> <span data-ttu-id="96470-131">有关存储库模式的详细信息，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="96470-131">For more information about the repository pattern, see the following resources:</span></span>

- <span data-ttu-id="96470-132">[存储库模式](https://msdn.microsoft.com/library/ff649690.aspx)MSDN 上。</span><span class="sxs-lookup"><span data-stu-id="96470-132">[The Repository Pattern](https://msdn.microsoft.com/library/ff649690.aspx) on MSDN.</span></span>
- <span data-ttu-id="96470-133">[存储库和工作单元模式中使用 Entity Framework 4.0](https://blogs.msdn.com/b/adonet/archive/2009/06/16/using-repository-and-unit-of-work-patterns-with-entity-framework-4-0.aspx) Entity Framework 团队博客上。</span><span class="sxs-lookup"><span data-stu-id="96470-133">[Using Repository and Unit of Work patterns with Entity Framework 4.0](https://blogs.msdn.com/b/adonet/archive/2009/06/16/using-repository-and-unit-of-work-patterns-with-entity-framework-4-0.aspx) on the Entity Framework team blog.</span></span>
- <span data-ttu-id="96470-134">[敏捷的实体框架 4 存储库](http://thedatafarm.com/blog/data-access/agile-entity-framework-4-repository-part-1-model-and-poco-classes/)系列 Julie Lerman 的博客上的文章。</span><span class="sxs-lookup"><span data-stu-id="96470-134">[Agile Entity Framework 4 Repository](http://thedatafarm.com/blog/data-access/agile-entity-framework-4-repository-part-1-model-and-poco-classes/) series of posts on Julie Lerman's blog.</span></span>
- <span data-ttu-id="96470-135">[构建一个快速的 jQuery HTML5/应用程序的帐户](https://weblogs.asp.net/dwahlin/archive/2011/08/15/building-the-account-at-a-glance-html5-jquery-application.aspx)Dan Wahlin 的博客上。</span><span class="sxs-lookup"><span data-stu-id="96470-135">[Building the Account at a Glance HTML5/jQuery Application](https://weblogs.asp.net/dwahlin/archive/2011/08/15/building-the-account-at-a-glance-html5-jquery-application.aspx) on Dan Wahlin's blog.</span></span>

> [!NOTE]
> <span data-ttu-id="96470-136">有许多方法来实现存储库和工作单元模式。</span><span class="sxs-lookup"><span data-stu-id="96470-136">There are many ways to implement the repository and unit of work patterns.</span></span> <span data-ttu-id="96470-137">使用或不工作类的一个单元，可以使用存储库类。</span><span class="sxs-lookup"><span data-stu-id="96470-137">You can use repository classes with or without a unit of work class.</span></span> <span data-ttu-id="96470-138">您可以实现所有实体类型，或另一个用于每种类型的单个存储库。</span><span class="sxs-lookup"><span data-stu-id="96470-138">You can implement a single repository for all entity types, or one for each type.</span></span> <span data-ttu-id="96470-139">如果你实现一个用于每种类型，可以使用单独的类、 泛型基类和派生的类中，或一个抽象基类和派生的类。</span><span class="sxs-lookup"><span data-stu-id="96470-139">If you implement one for each type, you can use separate classes, a generic base class and derived classes, or an abstract base class and derived classes.</span></span> <span data-ttu-id="96470-140">可以在存储库中包括的业务逻辑，也可以限制对数据访问逻辑。</span><span class="sxs-lookup"><span data-stu-id="96470-140">You can include business logic in your repository or restrict it to data access logic.</span></span> <span data-ttu-id="96470-141">您可以生成一个抽象层到您的数据库上下文类使用[IDbSet](https://msdn.microsoft.com/library/gg679233(v=vs.103).aspx)而不是那里接口[DbSet](https://msdn.microsoft.com/library/system.data.entity.dbset(v=vs.103).aspx)的实体集的类型。</span><span class="sxs-lookup"><span data-stu-id="96470-141">You can also build an abstraction layer into your database context class by using [IDbSet](https://msdn.microsoft.com/library/gg679233(v=vs.103).aspx) interfaces there instead of [DbSet](https://msdn.microsoft.com/library/system.data.entity.dbset(v=vs.103).aspx) types for your entity sets.</span></span> <span data-ttu-id="96470-142">实现一个抽象层，在本教程中所示的方法是为您要考虑，不推荐用于所有方案和环境的一个选项。</span><span class="sxs-lookup"><span data-stu-id="96470-142">The approach to implementing an abstraction layer shown in this tutorial is one option for you to consider, not a recommendation for all scenarios and environments.</span></span>

## <a name="creating-the-student-repository-class"></a><span data-ttu-id="96470-143">创建 Student 存储库类</span><span class="sxs-lookup"><span data-stu-id="96470-143">Creating the Student Repository Class</span></span>

<span data-ttu-id="96470-144">在中*DAL*文件夹中，创建名为的类文件*IStudentRepository.cs*和现有代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="96470-144">In the *DAL* folder, create a class file named *IStudentRepository.cs* and replace the existing code with the following code:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample1.cs)]

<span data-ttu-id="96470-145">此代码声明了一组典型的 CRUD 方法，包括两种读取的方法 — 一个用于返回所有`Student`实体和一个查找单个`Student`实体的 id。</span><span class="sxs-lookup"><span data-stu-id="96470-145">This code declares a typical set of CRUD methods, including two read methods — one that returns all `Student` entities, and one that finds a single `Student` entity by ID.</span></span>

<span data-ttu-id="96470-146">在中*DAL*文件夹中，创建名为的类文件*StudentRepository.cs*文件。</span><span class="sxs-lookup"><span data-stu-id="96470-146">In the *DAL* folder, create a class file named *StudentRepository.cs* file.</span></span> <span data-ttu-id="96470-147">现有代码替换为以下代码，实现`IStudentRepository`接口：</span><span class="sxs-lookup"><span data-stu-id="96470-147">Replace the existing code with the following code, which implements the `IStudentRepository` interface:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample2.cs)]

<span data-ttu-id="96470-148">在类变量中，定义数据库上下文和构造函数需要调用对象上下文的实例中传递：</span><span class="sxs-lookup"><span data-stu-id="96470-148">The database context is defined in a class variable, and the constructor expects the calling object to pass in an instance of the context:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample3.cs)]

<span data-ttu-id="96470-149">无法实例化新的上下文中存储库，但如果您使用一个控制器中的多个存储库，每个将最终会有单独的上下文。</span><span class="sxs-lookup"><span data-stu-id="96470-149">You could instantiate a new context in the repository, but then if you used multiple repositories in one controller, each would end up with a separate context.</span></span> <span data-ttu-id="96470-150">稍后将使用多个存储库中的`Course`控制器，并且您将看到工作类的一个单元可以确保所有存储库使用相同的上下文。</span><span class="sxs-lookup"><span data-stu-id="96470-150">Later you'll use multiple repositories in the `Course` controller, and you'll see how a unit of work class can ensure that all repositories use the same context.</span></span>

<span data-ttu-id="96470-151">存储库中实现[IDisposable](https://msdn.microsoft.com/library/system.idisposable.aspx)并释放数据库上下文，如前面在控制器中看到以及其 CRUD 方法调用数据库上下文中是您在前面看到的相同。</span><span class="sxs-lookup"><span data-stu-id="96470-151">The repository implements [IDisposable](https://msdn.microsoft.com/library/system.idisposable.aspx) and disposes the database context as you saw earlier in the controller, and its CRUD methods make calls to the database context in the same way that you saw earlier.</span></span>

## <a name="change-the-student-controller-to-use-the-repository"></a><span data-ttu-id="96470-152">更改学生控制器，若要使用的存储库</span><span class="sxs-lookup"><span data-stu-id="96470-152">Change the Student Controller to Use the Repository</span></span>

<span data-ttu-id="96470-153">在中*StudentController.cs*，当前类中的代码替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="96470-153">In *StudentController.cs*, replace the code currently in the class with the following code.</span></span> <span data-ttu-id="96470-154">突出显示所作更改。</span><span class="sxs-lookup"><span data-stu-id="96470-154">The changes are highlighted.</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample4.cs?highlight=13-18,44,75,77,102-103,120,137-138,159,172-174,186)]

<span data-ttu-id="96470-155">控制器现在声明实现的对象的类变量`IStudentRepository`接口而不是上下文类：</span><span class="sxs-lookup"><span data-stu-id="96470-155">The controller now declares a class variable for an object that implements the `IStudentRepository` interface instead of the context class:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample5.cs)]

<span data-ttu-id="96470-156">默认 （无参数） 构造函数创建一个新的上下文实例，并可选的构造函数允许调用方将上下文实例中传递。</span><span class="sxs-lookup"><span data-stu-id="96470-156">The default (parameterless) constructor creates a new context instance, and an optional constructor allows the caller to pass in a context instance.</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample6.cs)]

<span data-ttu-id="96470-157">(如果已使用*依赖关系注入*，或 DI，无需使用默认构造函数因为 DI 软件可确保始终将提供正确的存储库对象。)</span><span class="sxs-lookup"><span data-stu-id="96470-157">(If you were using *dependency injection*, or DI, you wouldn't need the default constructor because the DI software would ensure that the correct repository object would always be provided.)</span></span>

<span data-ttu-id="96470-158">在 CRUD 方法中，而不是上下文现在称为存储库：</span><span class="sxs-lookup"><span data-stu-id="96470-158">In the CRUD methods, the repository is now called instead of the context:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample7.cs)]

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample8.cs)]

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample9.cs)]

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample10.cs)]

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample11.cs)]

<span data-ttu-id="96470-159">和`Dispose`方法立即释放而不是上下文的存储库：</span><span class="sxs-lookup"><span data-stu-id="96470-159">And the `Dispose` method now disposes the repository instead of the context:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample12.cs)]

<span data-ttu-id="96470-160">运行站点，并单击**学生**选项卡。</span><span class="sxs-lookup"><span data-stu-id="96470-160">Run the site and click the **Students** tab.</span></span>

![Students_Index_page](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/_static/image1.png)

<span data-ttu-id="96470-162">该页面看起来，并像以前那样之前更改代码以使用存储库，因此其他学生页面还运行相同工作方式相同。</span><span class="sxs-lookup"><span data-stu-id="96470-162">The page looks and works the same as it did before you changed the code to use the repository, and the other Student pages also work the same.</span></span> <span data-ttu-id="96470-163">但是，没有方法中的一个重要区别`Index`控制器方法的执行筛选和排序。</span><span class="sxs-lookup"><span data-stu-id="96470-163">However, there's an important difference in the way the `Index` method of the controller does filtering and ordering.</span></span> <span data-ttu-id="96470-164">此方法的原始版本包含以下代码：</span><span class="sxs-lookup"><span data-stu-id="96470-164">The original version of this method contained the following code:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample13.cs?highlight=1)]

<span data-ttu-id="96470-165">已更新`Index`方法包含以下代码：</span><span class="sxs-lookup"><span data-stu-id="96470-165">The updated `Index` method contains the following code:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample14.cs?highlight=1)]

<span data-ttu-id="96470-166">突出显示的代码已更改。</span><span class="sxs-lookup"><span data-stu-id="96470-166">Only the highlighted code has changed.</span></span>

<span data-ttu-id="96470-167">该代码中，在原始版本中`students`被类型化为`IQueryable`对象。</span><span class="sxs-lookup"><span data-stu-id="96470-167">In the original version of the code, `students` is typed as an `IQueryable` object.</span></span> <span data-ttu-id="96470-168">查询不会发送到数据库中，直到它被转换为使用一种方法，如集合`ToList`，直到索引视图访问学生模型，这就不会出现。</span><span class="sxs-lookup"><span data-stu-id="96470-168">The query isn't sent to the database until it's converted into a collection using a method such as `ToList`, which doesn't occur until the Index view accesses the student model.</span></span> <span data-ttu-id="96470-169">`Where`上面的原始代码中的方法将成为`WHERE`发送到数据库的 SQL 查询中的子句。</span><span class="sxs-lookup"><span data-stu-id="96470-169">The `Where` method in the original code above becomes a `WHERE` clause in the SQL query that is sent to the database.</span></span> <span data-ttu-id="96470-170">这反过来意味着只有所选的实体由数据库返回。</span><span class="sxs-lookup"><span data-stu-id="96470-170">That in turn means that only the selected entities are returned by the database.</span></span> <span data-ttu-id="96470-171">但是，由于更改而`context.Students`到`studentRepository.GetStudents()`，则`students`变量后此语句是`IEnumerable`集合，其中包括在数据库中的所有学生。</span><span class="sxs-lookup"><span data-stu-id="96470-171">However, as a result of changing `context.Students` to `studentRepository.GetStudents()`, the `students` variable after this statement is an `IEnumerable` collection that includes all students in the database.</span></span> <span data-ttu-id="96470-172">应用的最终结果`Where`方法相同，但现在在 web 服务器上而不是由数据库的内存中完成工作。</span><span class="sxs-lookup"><span data-stu-id="96470-172">The end result of applying the `Where` method is the same, but now the work is done in memory on the web server and not by the database.</span></span> <span data-ttu-id="96470-173">对于返回大量数据的查询，这可能效率很低。</span><span class="sxs-lookup"><span data-stu-id="96470-173">For queries that return large volumes of data, this can be inefficient.</span></span>

> [!TIP]
> 
> <span data-ttu-id="96470-174">**IQueryable vs。IEnumerable**</span><span class="sxs-lookup"><span data-stu-id="96470-174">**IQueryable vs. IEnumerable**</span></span>
> 
> <span data-ttu-id="96470-175">在实现存储库如下所示，即使输入中的某些内容后**搜索**框查询发送到 SQL Server 返回学生的所有行，因为它不包括您的搜索条件：</span><span class="sxs-lookup"><span data-stu-id="96470-175">After you implement the repository as shown here, even if you enter something in the **Search** box the query sent to SQL Server returns all Student rows because it doesn't include your search criteria:</span></span>
> 
> ![](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/_static/image2.png)
> 
> [!code-sql[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample15.sql)]
> 
> <span data-ttu-id="96470-176">因为存储库无需知道有关搜索条件执行查询，此查询返回的所有学生数据。</span><span class="sxs-lookup"><span data-stu-id="96470-176">This query returns all of the student data because the repository executed the query without knowing about the search criteria.</span></span> <span data-ttu-id="96470-177">排序、 应用搜索条件，并选择数据的子集，用于在内存中完成分页 （在这种情况下显示仅 3 行） 的过程更高版本时，`ToPagedList`上调用方法`IEnumerable`集合。</span><span class="sxs-lookup"><span data-stu-id="96470-177">The process of sorting, applying search criteria, and selecting a subset of the data for paging (showing only 3 rows in this case) is done in memory later when the `ToPagedList` method is called on the `IEnumerable` collection.</span></span>
> 
> <span data-ttu-id="96470-178">在上一版本中的代码 （在之前实现存储库），该查询不会发送到之前的数据库后应用的搜索条件，当`ToPagedList`上调用`IQueryable`对象。</span><span class="sxs-lookup"><span data-stu-id="96470-178">In the previous version of the code (before you implemented the repository), the query is not sent to the database until after you apply the search criteria, when `ToPagedList` is called on the `IQueryable` object.</span></span>
> 
> ![](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/_static/image3.png)
> 
> <span data-ttu-id="96470-179">当调用 ToPagedList 时`IQueryable`对象，发送到 SQL Server 的查询指定的搜索字符串，而作为结果返回符合搜索条件的行，并且没有筛选需要在内存中完成。</span><span class="sxs-lookup"><span data-stu-id="96470-179">When ToPagedList is called on an `IQueryable` object, the query sent to SQL Server specifies the search string, and as a result only rows that meet the search criteria are returned, and no filtering needs to be done in memory.</span></span>
> 
> [!code-sql[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample16.sql)]
> 
> <span data-ttu-id="96470-180">（以下教程介绍如何检查查询发送到 SQL Server。）</span><span class="sxs-lookup"><span data-stu-id="96470-180">(The following tutorial explains how to examine queries sent to SQL Server.)</span></span>

<span data-ttu-id="96470-181">以下部分介绍如何实现存储库方法，您可以指定应由数据库完成此工作。</span><span class="sxs-lookup"><span data-stu-id="96470-181">The following section shows how to implement repository methods that enable you to specify that this work should be done by the database.</span></span>

<span data-ttu-id="96470-182">你现在已创建的控制器和实体框架数据库上下文之间的抽象层。</span><span class="sxs-lookup"><span data-stu-id="96470-182">You've now created an abstraction layer between the controller and the Entity Framework database context.</span></span> <span data-ttu-id="96470-183">如果您将执行自动的单元测试与此应用程序，则可以创建备用存储库类中实现的单元测试项目`IStudentRepository` *。*</span><span class="sxs-lookup"><span data-stu-id="96470-183">If you were going to perform automated unit testing with this application, you could create an alternative repository class in a unit test project that implements `IStudentRepository`*.*</span></span> <span data-ttu-id="96470-184">而不是调用要读取和写入数据的上下文，此 mock 存储库类可能会为了测试控制器函数操作内存中集合。</span><span class="sxs-lookup"><span data-stu-id="96470-184">Instead of calling the context to read and write data, this mock repository class could manipulate in-memory collections in order to test controller functions.</span></span>

## <a name="implement-a-generic-repository-and-a-unit-of-work-class"></a><span data-ttu-id="96470-185">实现泛型存储库和单元的工作类</span><span class="sxs-lookup"><span data-stu-id="96470-185">Implement a Generic Repository and a Unit of Work Class</span></span>

<span data-ttu-id="96470-186">创建每个实体类型的存储库类可能会导致大量的冗余代码，并且它可能导致部分更新。</span><span class="sxs-lookup"><span data-stu-id="96470-186">Creating a repository class for each entity type could result in a lot of redundant code, and it could result in partial updates.</span></span> <span data-ttu-id="96470-187">例如，假设您需要更新在同一事务中的两个不同的实体类型。</span><span class="sxs-lookup"><span data-stu-id="96470-187">For example, suppose you have to update two different entity types as part of the same transaction.</span></span> <span data-ttu-id="96470-188">如果每个使用单独的数据库上下文实例，其中一个操作可能会成功和其他可能会失败。</span><span class="sxs-lookup"><span data-stu-id="96470-188">If each uses a separate database context instance, one might succeed and the other might fail.</span></span> <span data-ttu-id="96470-189">最大程度减少冗余代码的一种方法是使用泛型存储库，并确保一种方法，所有存储库可以使用相同的数据库上下文 （并因此协调所有更新） 是使用工作类的一个单元。</span><span class="sxs-lookup"><span data-stu-id="96470-189">One way to minimize redundant code is to use a generic repository, and one way to ensure that all repositories use the same database context (and thus coordinate all updates) is to use a unit of work class.</span></span>

<span data-ttu-id="96470-190">在本教程的本部分中，将创建`GenericRepository`类和一个`UnitOfWork`类，并使用它们在`Course`控制器同时访问`Department`和`Course`实体集。</span><span class="sxs-lookup"><span data-stu-id="96470-190">In this section of the tutorial, you'll create a `GenericRepository` class and a `UnitOfWork` class, and use them in the `Course` controller to access both the `Department` and the `Course` entity sets.</span></span> <span data-ttu-id="96470-191">如前面所述，为了简化本教程的此部分未创建这些类的接口。</span><span class="sxs-lookup"><span data-stu-id="96470-191">As explained earlier, to keep this part of the tutorial simple, you aren't creating interfaces for these classes.</span></span> <span data-ttu-id="96470-192">但如果要使用它们来促进 TDD，你将通常实现这些接口使用相同的方式`Student`存储库。</span><span class="sxs-lookup"><span data-stu-id="96470-192">But if you were going to use them to facilitate TDD, you'd typically implement them with interfaces the same way you did the `Student` repository.</span></span>

### <a name="create-a-generic-repository"></a><span data-ttu-id="96470-193">创建泛型存储库</span><span class="sxs-lookup"><span data-stu-id="96470-193">Create a Generic Repository</span></span>

<span data-ttu-id="96470-194">在中*DAL*文件夹中，创建*GenericRepository.cs*和现有代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="96470-194">In the *DAL* folder, create *GenericRepository.cs* and replace the existing code with the following code:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample17.cs)]

<span data-ttu-id="96470-195">为数据库上下文和存储库为实例化的实体集声明类变量：</span><span class="sxs-lookup"><span data-stu-id="96470-195">Class variables are declared for the database context and for the entity set that the repository is instantiated for:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample18.cs)]

<span data-ttu-id="96470-196">构造函数接受数据库上下文实例并初始化实体集变量：</span><span class="sxs-lookup"><span data-stu-id="96470-196">The constructor accepts a database context instance and initializes the entity set variable:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample19.cs)]

<span data-ttu-id="96470-197">`Get`方法使用 lambda 表达式来允许调用代码指定筛选条件和一个列，通过对结果进行排序和字符串参数允许调用方提供的预先加载导航属性的逗号分隔列表：</span><span class="sxs-lookup"><span data-stu-id="96470-197">The `Get` method uses lambda expressions to allow the calling code to specify a filter condition and a column to order the results by, and a string parameter lets the caller provide a comma-delimited list of navigation properties for eager loading:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample20.cs)]

<span data-ttu-id="96470-198">代码`Expression<Func<TEntity, bool>> filter`意味着调用方将提供 lambda 表达式基于`TEntity`类型和此表达式将返回一个布尔值。</span><span class="sxs-lookup"><span data-stu-id="96470-198">The code `Expression<Func<TEntity, bool>> filter` means the caller will provide a lambda expression based on the `TEntity` type, and this expression will return a Boolean value.</span></span> <span data-ttu-id="96470-199">例如，如果存储库为实例化`Student`实体类型，指定调用方法中的代码可能`student => student.LastName == "Smith`&quot;为`filter`参数。</span><span class="sxs-lookup"><span data-stu-id="96470-199">For example, if the repository is instantiated for the `Student` entity type, the code in the calling method might specify `student => student.LastName == "Smith`&quot; for the `filter` parameter.</span></span>

<span data-ttu-id="96470-200">代码`Func<IQueryable<TEntity>, IOrderedQueryable<TEntity>> orderBy`也意味着调用方将提供 lambda 表达式。</span><span class="sxs-lookup"><span data-stu-id="96470-200">The code `Func<IQueryable<TEntity>, IOrderedQueryable<TEntity>> orderBy` also means the caller will provide a lambda expression.</span></span> <span data-ttu-id="96470-201">但在这种情况下，该表达式的输入`IQueryable`对象`TEntity`类型。</span><span class="sxs-lookup"><span data-stu-id="96470-201">But in this case, the input to the expression is an `IQueryable` object for the `TEntity` type.</span></span> <span data-ttu-id="96470-202">该表达式将返回是有序的新版`IQueryable`对象。</span><span class="sxs-lookup"><span data-stu-id="96470-202">The expression will return an ordered version of that `IQueryable` object.</span></span> <span data-ttu-id="96470-203">例如，如果存储库为实例化`Student`实体类型，指定调用方法中的代码可能`q => q.OrderBy(s => s.LastName)`为`orderBy`参数。</span><span class="sxs-lookup"><span data-stu-id="96470-203">For example, if the repository is instantiated for the `Student` entity type, the code in the calling method might specify `q => q.OrderBy(s => s.LastName)` for the `orderBy` parameter.</span></span>

<span data-ttu-id="96470-204">中的代码`Get`方法创建`IQueryable`对象，然后应用筛选器表达式，如果有一个：</span><span class="sxs-lookup"><span data-stu-id="96470-204">The code in the `Get` method creates an `IQueryable` object and then applies the filter expression if there is one:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample21.cs)]

<span data-ttu-id="96470-205">接下来，它分析的以逗号分隔列表之后适用的预先加载表达式：</span><span class="sxs-lookup"><span data-stu-id="96470-205">Next it applies the eager-loading expressions after parsing the comma-delimited list:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample22.cs)]

<span data-ttu-id="96470-206">最后，它采用`orderBy`如果有一个表达式，并返回结果; 否则它返回从无序查询结果：</span><span class="sxs-lookup"><span data-stu-id="96470-206">Finally, it applies the `orderBy` expression if there is one and returns the results; otherwise it returns the results from the unordered query:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample23.cs)]

<span data-ttu-id="96470-207">当您调用`Get`方法，可以进行筛选和排序上`IEnumerable`而不是提供这些函数的参数的方法返回的集合。</span><span class="sxs-lookup"><span data-stu-id="96470-207">When you call the `Get` method, you could do filtering and sorting on the `IEnumerable` collection returned by the method instead of providing parameters for these functions.</span></span> <span data-ttu-id="96470-208">但排序和筛选工作然后将完成 web 服务器上的内存中。</span><span class="sxs-lookup"><span data-stu-id="96470-208">But the sorting and filtering work would then be done in memory on the web server.</span></span> <span data-ttu-id="96470-209">通过使用这些参数可确保工作都由数据库而不是 web 服务器完成。</span><span class="sxs-lookup"><span data-stu-id="96470-209">By using these parameters, you ensure that the work is done by the database rather than the web server.</span></span> <span data-ttu-id="96470-210">一种替代方法是创建特定实体类型的派生的类并添加专用`Get`方法，如`GetStudentsInNameOrder`或`GetStudentsByName`。</span><span class="sxs-lookup"><span data-stu-id="96470-210">An alternative is to create derived classes for specific entity types and add specialized `Get` methods, such as `GetStudentsInNameOrder` or `GetStudentsByName`.</span></span> <span data-ttu-id="96470-211">但是，在复杂的应用程序，这可能导致大量此类派生的类和专用的方法，这可能是更多的工作来维护。</span><span class="sxs-lookup"><span data-stu-id="96470-211">However, in a complex application, this can result in a large number of such derived classes and specialized methods, which could be more work to maintain.</span></span>

<span data-ttu-id="96470-212">中的代码`GetByID`， `Insert`，和`Update`方法是类似于在非泛型存储库中看到。</span><span class="sxs-lookup"><span data-stu-id="96470-212">The code in the `GetByID`, `Insert`, and `Update` methods is similar to what you saw in the non-generic repository.</span></span> <span data-ttu-id="96470-213">(不提供中的预先加载参数`GetByID`签名，因为不能与预先加载`Find`方法。)</span><span class="sxs-lookup"><span data-stu-id="96470-213">(You aren't providing an eager loading parameter in the `GetByID` signature, because you can't do eager loading with the `Find` method.)</span></span>

<span data-ttu-id="96470-214">为提供了两个重载`Delete`方法：</span><span class="sxs-lookup"><span data-stu-id="96470-214">Two overloads are provided for the `Delete` method:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample24.cs)]

<span data-ttu-id="96470-215">只需 ID 中的实体的要删除传递这些允许之一和一个采用实体实例。</span><span class="sxs-lookup"><span data-stu-id="96470-215">One of these lets you pass in just the ID of the entity to be deleted, and one takes an entity instance.</span></span> <span data-ttu-id="96470-216">中所示[处理并发](../../getting-started/getting-started-with-ef-using-mvc/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)教程中，并发处理，您需要`Delete`采用实体实例的方法包括跟踪属性的原始值。</span><span class="sxs-lookup"><span data-stu-id="96470-216">As you saw in the [Handling Concurrency](../../getting-started/getting-started-with-ef-using-mvc/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md) tutorial, for concurrency handling you need a `Delete` method that takes an entity instance that includes the original value of a tracking property.</span></span>

<span data-ttu-id="96470-217">此泛型存储库将处理典型 CRUD 要求。</span><span class="sxs-lookup"><span data-stu-id="96470-217">This generic repository will handle typical CRUD requirements.</span></span> <span data-ttu-id="96470-218">当特定实体类型具有特殊要求，如更复杂的筛选或排序，可以创建具有该类型的其他方法的派生的类。</span><span class="sxs-lookup"><span data-stu-id="96470-218">When a particular entity type has special requirements, such as more complex filtering or ordering, you can create a derived class that has additional methods for that type.</span></span>

## <a name="creating-the-unit-of-work-class"></a><span data-ttu-id="96470-219">创建工作类的单元</span><span class="sxs-lookup"><span data-stu-id="96470-219">Creating the Unit of Work Class</span></span>

<span data-ttu-id="96470-220">单位工作类提供一种用途： 若要确保使用多个存储库时，它们共享单一数据库上下文。</span><span class="sxs-lookup"><span data-stu-id="96470-220">The unit of work class serves one purpose: to make sure that when you use multiple repositories, they share a single database context.</span></span> <span data-ttu-id="96470-221">这样一来，完成的工作单元时可以调用`SaveChanges`上下文的该实例上的方法并确保所有相关的更改都将协调。</span><span class="sxs-lookup"><span data-stu-id="96470-221">That way, when a unit of work is complete you can call the `SaveChanges` method on that instance of the context and be assured that all related changes will be coordinated.</span></span> <span data-ttu-id="96470-222">类需要做的一切是`Save`方法和属性的每个存储库。</span><span class="sxs-lookup"><span data-stu-id="96470-222">All that the class needs is a `Save` method and a property for each repository.</span></span> <span data-ttu-id="96470-223">每个存储库属性将返回已作为其他存储库实例使用相同的数据库上下文实例实例化的存储库实例。</span><span class="sxs-lookup"><span data-stu-id="96470-223">Each repository property returns a repository instance that has been instantiated using the same database context instance as the other repository instances.</span></span>

<span data-ttu-id="96470-224">在中*DAL*文件夹中，创建名为的类文件*UnitOfWork.cs*和模板代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="96470-224">In the *DAL* folder, create a class file named *UnitOfWork.cs* and replace the template code with the following code:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample25.cs)]

<span data-ttu-id="96470-225">该代码创建数据库上下文和每个存储库的类变量。</span><span class="sxs-lookup"><span data-stu-id="96470-225">The code creates class variables for the database context and each repository.</span></span> <span data-ttu-id="96470-226">有关`context`实例化的变量时，新的上下文是：</span><span class="sxs-lookup"><span data-stu-id="96470-226">For the `context` variable, a new context is instantiated:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample26.cs)]

<span data-ttu-id="96470-227">每个存储库属性检查是否已存在存储库。</span><span class="sxs-lookup"><span data-stu-id="96470-227">Each repository property checks whether the repository already exists.</span></span> <span data-ttu-id="96470-228">如果没有，它实例化的存储库，在上下文实例中传递。</span><span class="sxs-lookup"><span data-stu-id="96470-228">If not, it instantiates the repository, passing in the context instance.</span></span> <span data-ttu-id="96470-229">因此，所有存储库共享相同的上下文实例。</span><span class="sxs-lookup"><span data-stu-id="96470-229">As a result, all repositories share the same context instance.</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample27.cs)]

<span data-ttu-id="96470-230">`Save`方法调用`SaveChanges`上的数据库上下文。</span><span class="sxs-lookup"><span data-stu-id="96470-230">The `Save` method calls `SaveChanges` on the database context.</span></span>

<span data-ttu-id="96470-231">与实例化类变量中的数据库上下文的任何类一样`UnitOfWork`类实现`IDisposable`和释放上下文。</span><span class="sxs-lookup"><span data-stu-id="96470-231">Like any class that instantiates a database context in a class variable, the `UnitOfWork` class implements `IDisposable` and disposes the context.</span></span>

### <a name="changing-the-course-controller-to-use-the-unitofwork-class-and-repositories"></a><span data-ttu-id="96470-232">更改为使用 UnitOfWork 类和存储库的课程控制器</span><span class="sxs-lookup"><span data-stu-id="96470-232">Changing the Course Controller to use the UnitOfWork Class and Repositories</span></span>

<span data-ttu-id="96470-233">当前包含的代码替换为*CourseController.cs*使用以下代码：</span><span class="sxs-lookup"><span data-stu-id="96470-233">Replace the code you currently have in *CourseController.cs* with the following code:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample28.cs?highlight=15,20,22,31,54-55,70,85-86,101-102,122-124,130)]

<span data-ttu-id="96470-234">此代码将添加一个类变量`UnitOfWork`类。</span><span class="sxs-lookup"><span data-stu-id="96470-234">This code adds a class variable for the `UnitOfWork` class.</span></span> <span data-ttu-id="96470-235">(如果在此处使用接口，则不会初始化变量此处; 相反，你会实施一种模式的两个构造函数，就像你对`Student`存储库。)</span><span class="sxs-lookup"><span data-stu-id="96470-235">(If you were using interfaces here, you wouldn't initialize the variable here; instead, you'd implement a pattern of two constructors just as you did for the `Student` repository.)</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample29.cs)]

<span data-ttu-id="96470-236">在类的其余部分，对数据库上下文的所有引用都替换为对相应的存储库的引用使用`UnitOfWork`属性来访问存储库。</span><span class="sxs-lookup"><span data-stu-id="96470-236">In the rest of the class, all references to the database context are replaced by references to the appropriate repository, using `UnitOfWork` properties to access the repository.</span></span> <span data-ttu-id="96470-237">`Dispose`方法会释放`UnitOfWork`实例。</span><span class="sxs-lookup"><span data-stu-id="96470-237">The `Dispose` method disposes the `UnitOfWork` instance.</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample30.cs)]

<span data-ttu-id="96470-238">运行站点，并单击**课程**选项卡。</span><span class="sxs-lookup"><span data-stu-id="96470-238">Run the site and click the **Courses** tab.</span></span>

![Courses_Index_page](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/_static/image4.png)

<span data-ttu-id="96470-240">该页面看起来，并像之前所做的更改，以及其他课程页也适用相同工作方式相同。</span><span class="sxs-lookup"><span data-stu-id="96470-240">The page looks and works the same as it did before your changes, and the other Course pages also work the same.</span></span>

## <a name="summary"></a><span data-ttu-id="96470-241">总结</span><span class="sxs-lookup"><span data-stu-id="96470-241">Summary</span></span>

<span data-ttu-id="96470-242">您现在已实现的存储库和工作单元模式。</span><span class="sxs-lookup"><span data-stu-id="96470-242">You have now implemented both the repository and unit of work patterns.</span></span> <span data-ttu-id="96470-243">您已经使用 lambda 表达式作为泛型存储库中的方法参数。</span><span class="sxs-lookup"><span data-stu-id="96470-243">You have used lambda expressions as method parameters in the generic repository.</span></span> <span data-ttu-id="96470-244">有关如何使用这些表达式的详细信息`IQueryable`对象，请参阅[IQueryable(T) 接口 (System.Linq)](https://msdn.microsoft.com/library/bb351562.aspx) MSDN 库中。</span><span class="sxs-lookup"><span data-stu-id="96470-244">For more information about how to use these expressions with an `IQueryable` object, see [IQueryable(T) Interface (System.Linq)](https://msdn.microsoft.com/library/bb351562.aspx) in the MSDN Library.</span></span> <span data-ttu-id="96470-245">在下一个教程中，您将了解如何处理一些高级的方案。</span><span class="sxs-lookup"><span data-stu-id="96470-245">In the next tutorial you'll learn how to handle some advanced scenarios.</span></span>

<span data-ttu-id="96470-246">其他实体框架资源的链接可在[ASP.NET 数据访问内容映射](../../../../whitepapers/aspnet-data-access-content-map.md)。</span><span class="sxs-lookup"><span data-stu-id="96470-246">Links to other Entity Framework resources can be found in the [ASP.NET Data Access Content Map](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="96470-247">[上一页](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md)
> [下一页](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)</span><span class="sxs-lookup"><span data-stu-id="96470-247">[Previous](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md)
[Next](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)</span></span>

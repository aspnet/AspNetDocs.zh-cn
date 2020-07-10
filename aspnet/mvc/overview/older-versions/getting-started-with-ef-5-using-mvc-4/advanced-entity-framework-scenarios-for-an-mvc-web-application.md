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
# <a name="advanced-entity-framework-scenarios-for-an-mvc-web-application-10-of-10"></a><span data-ttu-id="248d1-103">MVC Web 应用程序的高级实体框架方案 (10 个) </span><span class="sxs-lookup"><span data-stu-id="248d1-103">Advanced Entity Framework Scenarios for an MVC Web Application (10 of 10)</span></span>

<span data-ttu-id="248d1-104">作者： [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="248d1-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="248d1-105">下载完成的项目</span><span class="sxs-lookup"><span data-stu-id="248d1-105">Download Completed Project</span></span>](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> <span data-ttu-id="248d1-106">Contoso 大学示例 web 应用程序演示了如何使用实体框架 5 Code First 和 Visual Studio 2012 创建 ASP.NET MVC 4 应用程序。</span><span class="sxs-lookup"><span data-stu-id="248d1-106">The Contoso University sample web application demonstrates how to create ASP.NET MVC 4 applications using the Entity Framework 5 Code First and Visual Studio 2012.</span></span> <span data-ttu-id="248d1-107">若要了解教程系列，请参阅[本系列中的第一个教程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。</span><span class="sxs-lookup"><span data-stu-id="248d1-107">For information about the tutorial series, see [the first tutorial in the series](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span> <span data-ttu-id="248d1-108">你可以从头开始学习本系列教程，也可以从此处[下载入门项目](building-the-ef5-mvc4-chapter-downloads.md)。</span><span class="sxs-lookup"><span data-stu-id="248d1-108">You can start the tutorial series from the beginning or [download a starter project for this chapter](building-the-ef5-mvc4-chapter-downloads.md) and start here.</span></span>
> 
> > [!NOTE] 
> > 
> > <span data-ttu-id="248d1-109">如果遇到无法解决的问题，请[下载已完成的章节](building-the-ef5-mvc4-chapter-downloads.md)并尝试重现你的问题。</span><span class="sxs-lookup"><span data-stu-id="248d1-109">If you run into a problem you can't resolve, [download the completed chapter](building-the-ef5-mvc4-chapter-downloads.md) and try to reproduce your problem.</span></span> <span data-ttu-id="248d1-110">通常可以通过将代码与已完成的代码进行比较，查找问题的解决方案。</span><span class="sxs-lookup"><span data-stu-id="248d1-110">You can generally find the solution to the problem by comparing your code to the completed code.</span></span> <span data-ttu-id="248d1-111">有关一些常见错误以及如何解决这些错误，请参阅[错误和解决方法。](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)</span><span class="sxs-lookup"><span data-stu-id="248d1-111">For some common errors and how to solve them, see [Errors and Workarounds.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)</span></span>

<span data-ttu-id="248d1-112">在上一教程中，你已实现了存储库和工作单元模式。</span><span class="sxs-lookup"><span data-stu-id="248d1-112">In the previous tutorial you implemented the repository and unit of work patterns.</span></span> <span data-ttu-id="248d1-113">本教程包括以下主题：</span><span class="sxs-lookup"><span data-stu-id="248d1-113">This tutorial covers the following topics:</span></span>

- <span data-ttu-id="248d1-114">执行原始 SQL 查询。</span><span class="sxs-lookup"><span data-stu-id="248d1-114">Performing raw SQL queries.</span></span>
- <span data-ttu-id="248d1-115">正在执行无跟踪查询。</span><span class="sxs-lookup"><span data-stu-id="248d1-115">Performing no-tracking queries.</span></span>
- <span data-ttu-id="248d1-116">检查发送到数据库的查询。</span><span class="sxs-lookup"><span data-stu-id="248d1-116">Examining queries sent to the database.</span></span>
- <span data-ttu-id="248d1-117">使用代理类。</span><span class="sxs-lookup"><span data-stu-id="248d1-117">Working with proxy classes.</span></span>
- <span data-ttu-id="248d1-118">禁用更改的自动检测。</span><span class="sxs-lookup"><span data-stu-id="248d1-118">Disabling automatic detection of changes.</span></span>
- <span data-ttu-id="248d1-119">保存更改时禁用验证。</span><span class="sxs-lookup"><span data-stu-id="248d1-119">Disabling validation when saving changes.</span></span>
- [<span data-ttu-id="248d1-120">错误和解决办法</span><span class="sxs-lookup"><span data-stu-id="248d1-120">Errors and Work Arounds</span></span>](#errors)

<span data-ttu-id="248d1-121">对于大多数这些主题，你将使用已创建的页面。</span><span class="sxs-lookup"><span data-stu-id="248d1-121">For most of these topics, you'll work with pages that you already created.</span></span> <span data-ttu-id="248d1-122">若要使用原始 SQL 执行批量更新，您将创建一个新页，用于更新数据库中所有课程的信用额度：</span><span class="sxs-lookup"><span data-stu-id="248d1-122">To use raw SQL to do bulk updates you'll create a new page that updates the number of credits of all courses in the database:</span></span>

![Update_Course_Credits_initial_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image1.png)

<span data-ttu-id="248d1-124">若要使用无跟踪查询，你需要将新的验证逻辑添加到部门编辑页面：</span><span class="sxs-lookup"><span data-stu-id="248d1-124">And to use a no-tracking query you'll add new validation logic to the Department Edit page:</span></span>

![Department_Edit_page_with_duplicate_administrator_error_message](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image2.png)

## <a name="performing-raw-sql-queries"></a><span data-ttu-id="248d1-126">执行原始 SQL 查询</span><span class="sxs-lookup"><span data-stu-id="248d1-126">Performing Raw SQL Queries</span></span>

<span data-ttu-id="248d1-127">实体框架 Code First API 包括使你能够将 SQL 命令直接传递到数据库的方法。</span><span class="sxs-lookup"><span data-stu-id="248d1-127">The Entity Framework Code First API includes methods that enable you to pass SQL commands directly to the database.</span></span> <span data-ttu-id="248d1-128">你有以下选择：</span><span class="sxs-lookup"><span data-stu-id="248d1-128">You have the following options:</span></span>

- <span data-ttu-id="248d1-129">使用`DbSet.SqlQuery`返回实体类型的查询方法。</span><span class="sxs-lookup"><span data-stu-id="248d1-129">Use the `DbSet.SqlQuery` method for queries that return entity types.</span></span> <span data-ttu-id="248d1-130">返回的对象必须是对象所需的类型 `DbSet` ，并且数据库上下文会自动跟踪这些对象，除非关闭跟踪。</span><span class="sxs-lookup"><span data-stu-id="248d1-130">The returned objects must be of the type expected by the `DbSet` object, and they are automatically tracked by the database context unless you turn tracking off.</span></span> <span data-ttu-id="248d1-131"> (参见以下有关方法的部分 `AsNoTracking` 。 ) </span><span class="sxs-lookup"><span data-stu-id="248d1-131">(See the following section about the `AsNoTracking` method.)</span></span>
- <span data-ttu-id="248d1-132">`Database.SqlQuery`对于返回非实体类型的查询，请使用方法。</span><span class="sxs-lookup"><span data-stu-id="248d1-132">Use the `Database.SqlQuery` method for queries that return types that aren't entities.</span></span> <span data-ttu-id="248d1-133">数据库上下文不会跟踪返回的数据，即使你使用该方法来检索实体类型也是如此。</span><span class="sxs-lookup"><span data-stu-id="248d1-133">The returned data isn't tracked by the database context, even if you use this method to retrieve entity types.</span></span>
- <span data-ttu-id="248d1-134">将[Database.ExecuteSqlCommand](https://msdn.microsoft.com/library/gg679456(v=vs.103).aspx)用于非查询命令。</span><span class="sxs-lookup"><span data-stu-id="248d1-134">Use the [Database.ExecuteSqlCommand](https://msdn.microsoft.com/library/gg679456(v=vs.103).aspx) for non-query commands.</span></span>

<span data-ttu-id="248d1-135">使用 Entity Framework 的优点之一是它可避免你编写跟数据库过于耦合的代码</span><span class="sxs-lookup"><span data-stu-id="248d1-135">One of the advantages of using the Entity Framework is that it avoids tying your code too closely to a particular method of storing data.</span></span> <span data-ttu-id="248d1-136">它会自动生成 SQL 查询和命令，使得你无需自行编写。</span><span class="sxs-lookup"><span data-stu-id="248d1-136">It does this by generating SQL queries and commands for you, which also frees you from having to write them yourself.</span></span> <span data-ttu-id="248d1-137">但在某些情况下，你需要运行已手动创建的特定 SQL 查询，并且这些方法使你能够处理此类异常。</span><span class="sxs-lookup"><span data-stu-id="248d1-137">But there are exceptional scenarios when you need to run specific SQL queries that you have manually created, and these methods make it possible for you to handle such exceptions.</span></span>

<span data-ttu-id="248d1-138">在 Web 应用程序中执行 SQL 命令时，请务必采取预防措施来保护站点免受 SQL 注入攻击。</span><span class="sxs-lookup"><span data-stu-id="248d1-138">As is always true when you execute SQL commands in a web application, you must take precautions to protect your site against SQL injection attacks.</span></span> <span data-ttu-id="248d1-139">一种方法是使用参数化查询，确保不会将网页提交的字符串视为 SQL 命令。</span><span class="sxs-lookup"><span data-stu-id="248d1-139">One way to do that is to use parameterized queries to make sure that strings submitted by a web page can't be interpreted as SQL commands.</span></span> <span data-ttu-id="248d1-140">在本教程中，将用户输入集成到查询中时会使用参数化查询。</span><span class="sxs-lookup"><span data-stu-id="248d1-140">In this tutorial you'll use parameterized queries when integrating user input into a query.</span></span>

### <a name="calling-a-query-that-returns-entities"></a><span data-ttu-id="248d1-141">调用返回实体的查询</span><span class="sxs-lookup"><span data-stu-id="248d1-141">Calling a Query that Returns Entities</span></span>

<span data-ttu-id="248d1-142">假设您希望 `GenericRepository` 类提供附加的筛选和排序灵活性，而不需要使用其他方法创建派生类。</span><span class="sxs-lookup"><span data-stu-id="248d1-142">Suppose you want the `GenericRepository` class to provide additional filtering and sorting flexibility without requiring that you create a derived class with additional methods.</span></span> <span data-ttu-id="248d1-143">实现此目的的一种方法是添加接受 SQL 查询的方法。</span><span class="sxs-lookup"><span data-stu-id="248d1-143">One way to achieve that would be to add a method that accepts a SQL query.</span></span> <span data-ttu-id="248d1-144">然后，您可以在控制器中指定想要的任何类型的筛选或排序，如 `Where` 依赖于联接或子查询的子句。</span><span class="sxs-lookup"><span data-stu-id="248d1-144">You could then specify any kind of filtering or sorting you want in the controller, such as a `Where` clause that depends on a joins or a subquery.</span></span> <span data-ttu-id="248d1-145">在本节中，你将了解如何实现此类方法。</span><span class="sxs-lookup"><span data-stu-id="248d1-145">In this section you'll see how to implement such a method.</span></span>

<span data-ttu-id="248d1-146">`GetWithRawSql`通过将以下代码添加到*GenericRepository.cs*，创建方法：</span><span class="sxs-lookup"><span data-stu-id="248d1-146">Create the `GetWithRawSql` method by adding the following code to *GenericRepository.cs*:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample1.cs)]

<span data-ttu-id="248d1-147">在*CourseController.cs*中，从方法调用新方法 `Details` ，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="248d1-147">In *CourseController.cs*, call the new method from the `Details` method, as shown in the following example:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample2.cs)]

<span data-ttu-id="248d1-148">在这种情况下，您可以使用 `GetByID` 方法，但使用 `GetWithRawSql` 方法来验证 `GetWithRawSQL` 方法是否有效。</span><span class="sxs-lookup"><span data-stu-id="248d1-148">In this case you could have used the `GetByID` method, but you're using the `GetWithRawSql` method to verify that the `GetWithRawSQL` method works.</span></span>

<span data-ttu-id="248d1-149">运行 "详细信息" 页，验证 "选择查询是否有效" (选择 "**课程**" 选项卡，然后选择一个课程) 的**详细信息**。</span><span class="sxs-lookup"><span data-stu-id="248d1-149">Run the Details page to verify that the select query works (select the **Course** tab and then **Details** for one course).</span></span>

![Course_Details_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image3.png)

### <a name="calling-a-query-that-returns-other-types-of-objects"></a><span data-ttu-id="248d1-151">调用返回其他类型对象的查询</span><span class="sxs-lookup"><span data-stu-id="248d1-151">Calling a Query that Returns Other Types of Objects</span></span>

<span data-ttu-id="248d1-152">之前你在“关于”页面创建了一个学生统计信息网格，显示每个注册日期的学生数量。</span><span class="sxs-lookup"><span data-stu-id="248d1-152">Earlier you created a student statistics grid for the About page that showed the number of students for each enrollment date.</span></span> <span data-ttu-id="248d1-153">在*HomeController.cs*中执行此操作的代码使用 LINQ：</span><span class="sxs-lookup"><span data-stu-id="248d1-153">The code that does this in *HomeController.cs* uses LINQ:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample3.cs)]

<span data-ttu-id="248d1-154">假设您要编写在 SQL 中直接检索此数据的代码，而不是使用 LINQ。</span><span class="sxs-lookup"><span data-stu-id="248d1-154">Suppose you want to write the code that retrieves this data directly in SQL rather than using LINQ.</span></span> <span data-ttu-id="248d1-155">为此，您需要运行一个返回除 entity 对象之外的内容的查询，这意味着您需要使用 `Database.SqlQuery` 方法。</span><span class="sxs-lookup"><span data-stu-id="248d1-155">To do that you need to run a query that returns something other than entity objects, which means you need to use the `Database.SqlQuery` method.</span></span>

<span data-ttu-id="248d1-156">在*HomeController.cs*中，将方法中的 LINQ 语句替换 `About` 为以下代码：</span><span class="sxs-lookup"><span data-stu-id="248d1-156">In *HomeController.cs*, replace the LINQ statement in the `About` method with the following code:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample4.cs)]

<span data-ttu-id="248d1-157">运行 "关于" 页。</span><span class="sxs-lookup"><span data-stu-id="248d1-157">Run the About page.</span></span> <span data-ttu-id="248d1-158">显示的数据和之前一样。</span><span class="sxs-lookup"><span data-stu-id="248d1-158">It displays the same data it did before.</span></span>

![About_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image4.png)

### <a name="calling-an-update-query"></a><span data-ttu-id="248d1-160">调用更新查询</span><span class="sxs-lookup"><span data-stu-id="248d1-160">Calling an Update Query</span></span>

<span data-ttu-id="248d1-161">假设 Contoso 大学管理员希望能够在数据库中执行大容量更改，如更改每个课程的信用额度。</span><span class="sxs-lookup"><span data-stu-id="248d1-161">Suppose Contoso University administrators want to be able to perform bulk changes in the database, such as changing the number of credits for every course.</span></span> <span data-ttu-id="248d1-162">如果该大学提供了大量课程，那么将所有课程作为实体来检索并单独更改就非常低效。</span><span class="sxs-lookup"><span data-stu-id="248d1-162">If the university has a large number of courses, it would be inefficient to retrieve them all as entities and change them individually.</span></span> <span data-ttu-id="248d1-163">在本节中，您将实现一个网页，该网页允许用户指定更改所有课程的信用额度的因素，并通过执行 SQL 语句进行更改 `UPDATE` 。</span><span class="sxs-lookup"><span data-stu-id="248d1-163">In this section you'll implement a web page that allows the user to specify a factor by which to change the number of credits for all courses, and you'll make the change by executing a SQL `UPDATE` statement.</span></span> <span data-ttu-id="248d1-164">网页的外观类似于下图：</span><span class="sxs-lookup"><span data-stu-id="248d1-164">The web page will look like the following illustration:</span></span>

![Update_Course_Credits_initial_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image5.png)

<span data-ttu-id="248d1-166">在上一教程中，你使用了通用存储库来读取和更新 `Course` 控制器中的实体 `Course` 。</span><span class="sxs-lookup"><span data-stu-id="248d1-166">In the previous tutorial you used the generic repository to read and update `Course` entities in the `Course` controller.</span></span> <span data-ttu-id="248d1-167">对于此大容量更新操作，需要创建不在通用存储库中的新存储库方法。</span><span class="sxs-lookup"><span data-stu-id="248d1-167">For this bulk update operation, you need to create a new repository method that isn't in the generic repository.</span></span> <span data-ttu-id="248d1-168">为此，你将创建一个 `CourseRepository` 派生自类的专用类 `GenericRepository` 。</span><span class="sxs-lookup"><span data-stu-id="248d1-168">To do that, you'll create a dedicated `CourseRepository` class that derives from the `GenericRepository` class.</span></span>

<span data-ttu-id="248d1-169">在*DAL*文件夹中，创建*CourseRepository.cs* ，并将现有代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="248d1-169">In the *DAL* folder, create *CourseRepository.cs* and replace the existing code with the following code:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample5.cs)]

<span data-ttu-id="248d1-170">在*UnitOfWork.cs*中，将 `Course` 存储库类型从更改 `GenericRepository<Course>` 为`CourseRepository:`</span><span class="sxs-lookup"><span data-stu-id="248d1-170">In *UnitOfWork.cs*, change the `Course` repository type from `GenericRepository<Course>` to `CourseRepository:`</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample6.cs)]

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample7.cs)]

<span data-ttu-id="248d1-171">在*CourseController.cs*中，添加 `UpdateCourseCredits` 方法：</span><span class="sxs-lookup"><span data-stu-id="248d1-171">In *CourseController.cs*, add an `UpdateCourseCredits` method:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample8.cs)]

<span data-ttu-id="248d1-172">此方法将用于 `HttpGet` 和 `HttpPost` 。</span><span class="sxs-lookup"><span data-stu-id="248d1-172">This method will be used for both `HttpGet` and `HttpPost`.</span></span> <span data-ttu-id="248d1-173">当该 `HttpGet` `UpdateCourseCredits` 方法运行时， `multiplier` 变量将为 null，并且该视图将显示一个空文本框和一个提交按钮，如上图所示。</span><span class="sxs-lookup"><span data-stu-id="248d1-173">When the `HttpGet` `UpdateCourseCredits` method runs, the `multiplier` variable will be null and the view will display an empty text box and a submit button, as shown in the preceding illustration.</span></span>

<span data-ttu-id="248d1-174">单击 "**更新**" 按钮并运行该 `HttpPost` 方法时， `multiplier` 会在文本框中输入值。</span><span class="sxs-lookup"><span data-stu-id="248d1-174">When the **Update** button is clicked and the `HttpPost` method runs, `multiplier` will have the value entered in the text box.</span></span> <span data-ttu-id="248d1-175">然后，该代码调用存储库 `UpdateCourseCredits` 方法，该方法返回受影响的行数，该值存储在对象中 `ViewBag` 。</span><span class="sxs-lookup"><span data-stu-id="248d1-175">The code then calls the repository `UpdateCourseCredits` method, which returns the number of affected rows, and that value is stored in the `ViewBag` object.</span></span> <span data-ttu-id="248d1-176">当视图接收到对象中受影响的行数时 `ViewBag` ，它将显示该数字，而不是文本框和提交按钮，如下图所示：</span><span class="sxs-lookup"><span data-stu-id="248d1-176">When the view receives the number of affected rows in the `ViewBag` object, it displays that number instead of the text box and submit button, as shown in the following illustration:</span></span>

![Update_Course_Credits_rows_affected_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image6.png)

<span data-ttu-id="248d1-178">在 "更新课程信用额度" 页的*Views\Course*文件夹中创建视图：</span><span class="sxs-lookup"><span data-stu-id="248d1-178">Create a view in the *Views\Course* folder for the Update Course Credits page:</span></span>

![Add_View_dialog_box_for_Update_Course_Credits](https://asp.net/media/2578203/Windows-Live-Writer_Advanced-Entity-Framework-Scenarios-for-_CEF8_Add_View_dialog_box_for_Update_Course_Credits.png)

<span data-ttu-id="248d1-180">在*Views\Course\UpdateCourseCredits.cshtml*中，将模板代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="248d1-180">In *Views\Course\UpdateCourseCredits.cshtml*, replace the template code with the following code:</span></span>

[!code-cshtml[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample9.cshtml)]

<span data-ttu-id="248d1-181">通过选择**Courses**选项卡运行`UpdateCourseCredits`方法，然后在浏览器地址栏中 URL 的末尾添加"/ UpdateCourseCredits"到 (例如： `http://localhost:50205/Course/UpdateCourseCredits`)。</span><span class="sxs-lookup"><span data-stu-id="248d1-181">Run the `UpdateCourseCredits` method by selecting the **Courses** tab, then adding "/UpdateCourseCredits" to the end of the URL in the browser's address bar (for example: `http://localhost:50205/Course/UpdateCourseCredits`).</span></span> <span data-ttu-id="248d1-182">在文本框中输入数字：</span><span class="sxs-lookup"><span data-stu-id="248d1-182">Enter a number in the text box:</span></span>

![Update_Course_Credits_initial_page_with_2_entered](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image7.png)

<span data-ttu-id="248d1-184">单击**Update**。</span><span class="sxs-lookup"><span data-stu-id="248d1-184">Click **Update**.</span></span> <span data-ttu-id="248d1-185">你会看到受影响的行数：</span><span class="sxs-lookup"><span data-stu-id="248d1-185">You see the number of rows affected:</span></span>

![Update_Course_Credits_rows_affected_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image8.png)

<span data-ttu-id="248d1-187">单击“返回列表”可以查看课程列表，其中学分已替换为修改后的数字。</span><span class="sxs-lookup"><span data-stu-id="248d1-187">Click **Back to List** to see the list of courses with the revised number of credits.</span></span>

![Courses_Index_page_showing_revised_credits](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image9.png)

<span data-ttu-id="248d1-189">有关原始 SQL 查询的详细信息，请参阅实体框架团队博客上的[原始 Sql 查询](https://blogs.msdn.com/b/adonet/archive/2011/02/04/using-dbcontext-in-ef-feature-ctp5-part-10-raw-sql-queries.aspx)。</span><span class="sxs-lookup"><span data-stu-id="248d1-189">For more information about raw SQL queries, see [Raw SQL Queries](https://blogs.msdn.com/b/adonet/archive/2011/02/04/using-dbcontext-in-ef-feature-ctp5-part-10-raw-sql-queries.aspx) on the Entity Framework team blog.</span></span>

## <a name="no-tracking-queries"></a><span data-ttu-id="248d1-190">非跟踪查询</span><span class="sxs-lookup"><span data-stu-id="248d1-190">No-Tracking Queries</span></span>

<span data-ttu-id="248d1-191">当数据库上下文检索数据库行并创建表示它们的实体对象时，默认情况下，它会跟踪内存中的实体是否与数据库中的实体同步。</span><span class="sxs-lookup"><span data-stu-id="248d1-191">When a database context retrieves database rows and creates entity objects that represent them, by default it keeps track of whether the entities in memory are in sync with what's in the database.</span></span> <span data-ttu-id="248d1-192">更新实体时，内存中的数据充当缓存并使用该数据。</span><span class="sxs-lookup"><span data-stu-id="248d1-192">The data in memory acts as a cache and is used when you update an entity.</span></span> <span data-ttu-id="248d1-193">在 Web 应用程序中，此缓存通常是不必要的，因为上下文实例通常生存期较短（创建新的实例并用于处理每个请求），并且通常在再次使用该实体之前处理读取实体的上下文。</span><span class="sxs-lookup"><span data-stu-id="248d1-193">This caching is often unnecessary in a web application because context instances are typically short-lived (a new one is created and disposed for each request) and the context that reads an entity is typically disposed before that entity is used again.</span></span>

<span data-ttu-id="248d1-194">您可以使用方法指定上下文是否跟踪查询的实体对象 `AsNoTracking` 。</span><span class="sxs-lookup"><span data-stu-id="248d1-194">You can specify whether the context tracks entity objects for a query by using the `AsNoTracking` method.</span></span> <span data-ttu-id="248d1-195">可能想要执行的典型方案包括以下操作：</span><span class="sxs-lookup"><span data-stu-id="248d1-195">Typical scenarios in which you might want to do that include the following:</span></span>

- <span data-ttu-id="248d1-196">此查询检索到关闭跟踪可能会明显提高性能的大量数据。</span><span class="sxs-lookup"><span data-stu-id="248d1-196">The query retrieves such a large volume of data that turning off tracking might noticeably enhance performance.</span></span>
- <span data-ttu-id="248d1-197">您希望附加实体以便对其进行更新，但您之前检索到不同用途的同一实体。</span><span class="sxs-lookup"><span data-stu-id="248d1-197">You want to attach an entity in order to update it, but you earlier retrieved the same entity for a different purpose.</span></span> <span data-ttu-id="248d1-198">由于数据库上下文已跟踪了该实体，因此无法附加要更改的实体。</span><span class="sxs-lookup"><span data-stu-id="248d1-198">Because the entity is already being tracked by the database context, you can't attach the entity that you want to change.</span></span> <span data-ttu-id="248d1-199">防止此情况发生的一种方法是将 `AsNoTracking` 选项与前面的查询一起使用。</span><span class="sxs-lookup"><span data-stu-id="248d1-199">One way to prevent this from happening is to use the `AsNoTracking` option with the earlier query.</span></span>

<span data-ttu-id="248d1-200">在本部分中，你将实现用于阐释其中第二种情况的业务逻辑。</span><span class="sxs-lookup"><span data-stu-id="248d1-200">In this section you'll implement business logic that illustrates the second of these scenarios.</span></span> <span data-ttu-id="248d1-201">具体来说，您将强制实施一条业务规则，指出讲师不能是多个部门的管理员。</span><span class="sxs-lookup"><span data-stu-id="248d1-201">Specifically, you'll enforce a business rule that says that an instructor can't be the administrator of more than one department.</span></span>

<span data-ttu-id="248d1-202">在*DepartmentController.cs*中，添加一个可从和方法调用的新方法， `Edit` `Create` 以确保没有两个部门具有相同的管理员：</span><span class="sxs-lookup"><span data-stu-id="248d1-202">In *DepartmentController.cs*, add a new method that you can call from the `Edit` and `Create` methods to make sure that no two departments have the same administrator:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample10.cs)]

<span data-ttu-id="248d1-203">如果没有验证错误，请在方法的块中添加代码 `try` `HttpPost` `Edit` 以调用此新方法。</span><span class="sxs-lookup"><span data-stu-id="248d1-203">Add code in the `try` block of the `HttpPost` `Edit` method to call this new method if there are no validation errors.</span></span> <span data-ttu-id="248d1-204">`try`该块现在类似于以下示例：</span><span class="sxs-lookup"><span data-stu-id="248d1-204">The `try` block now looks like the following example:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample11.cs?highlight=9-12)]

<span data-ttu-id="248d1-205">运行 "部门编辑" 页，然后尝试将部门的管理员更改为已是其他部门的管理员的指导员。</span><span class="sxs-lookup"><span data-stu-id="248d1-205">Run the Department Edit page and try to change a department's administrator to an instructor who is already the administrator of a different department.</span></span> <span data-ttu-id="248d1-206">你会收到预期的错误消息：</span><span class="sxs-lookup"><span data-stu-id="248d1-206">You get the expected error message:</span></span>

![Department_Edit_page_with_duplicate_administrator_error_message](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image10.png)

<span data-ttu-id="248d1-208">现在再次运行 "部门编辑" 页，此时更改**预算**金额。</span><span class="sxs-lookup"><span data-stu-id="248d1-208">Now run the Department Edit page again and this time change the **Budget** amount.</span></span> <span data-ttu-id="248d1-209">单击 "**保存**" 时，会看到错误页：</span><span class="sxs-lookup"><span data-stu-id="248d1-209">When you click **Save**, you see an error page:</span></span>

![Department_Edit_page_with_object_state_manager_error_message](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image11.png)

<span data-ttu-id="248d1-211">异常错误消息为 " `An object with the same key already exists in the ObjectStateManager. The ObjectStateManager cannot track multiple objects with the same key.` "，原因如下：</span><span class="sxs-lookup"><span data-stu-id="248d1-211">The exception error message is "`An object with the same key already exists in the ObjectStateManager. The ObjectStateManager cannot track multiple objects with the same key.`" This happened because of the following sequence of events:</span></span>

- <span data-ttu-id="248d1-212">`Edit`方法调用 `ValidateOneAdministratorAssignmentPerInstructor` 方法，该方法检索将 Kim Abercrombie 作为其管理员的所有部门。</span><span class="sxs-lookup"><span data-stu-id="248d1-212">The `Edit` method calls the `ValidateOneAdministratorAssignmentPerInstructor` method, which retrieves all departments that have Kim Abercrombie as their administrator.</span></span> <span data-ttu-id="248d1-213">这会导致读取英语部门。</span><span class="sxs-lookup"><span data-stu-id="248d1-213">That causes the English department to be read.</span></span> <span data-ttu-id="248d1-214">由于这是正在编辑的部门，因此不会报告任何错误。</span><span class="sxs-lookup"><span data-stu-id="248d1-214">Because that's the department being edited, no error is reported.</span></span> <span data-ttu-id="248d1-215">但是，此读取操作的结果是，数据库上下文现在正在跟踪从数据库中读取的英语部门实体。</span><span class="sxs-lookup"><span data-stu-id="248d1-215">As a result of this read operation, however, the English department entity that was read from the database is now being tracked by the database context.</span></span>
- <span data-ttu-id="248d1-216">此 `Edit` 方法尝试 `Modified` 在由 MVC 模型联编程序创建的英语部门实体上设置标志，但这会失败，因为上下文已在跟踪英语部门的实体。</span><span class="sxs-lookup"><span data-stu-id="248d1-216">The `Edit` method tries to set the `Modified` flag on the English department entity created by the MVC model binder, but that fails because the context is already tracking an entity for the English department.</span></span>

<span data-ttu-id="248d1-217">此问题的一种解决方法是使上下文不会跟踪由验证查询检索到的内存中部门实体。</span><span class="sxs-lookup"><span data-stu-id="248d1-217">One solution to this problem is to keep the context from tracking in-memory department entities retrieved by the validation query.</span></span> <span data-ttu-id="248d1-218">执行此操作没有任何缺点，因为你不会更新此实体，也不会以一种可从其缓存在内存中的方式对其进行读取。</span><span class="sxs-lookup"><span data-stu-id="248d1-218">There's no disadvantage to doing this, because you won't be updating this entity or reading it again in a way that would benefit from it being cached in memory.</span></span>

<span data-ttu-id="248d1-219">在*DepartmentController.cs*的方法中， `ValidateOneAdministratorAssignmentPerInstructor` 指定 no 跟踪，如下所示：</span><span class="sxs-lookup"><span data-stu-id="248d1-219">In *DepartmentController.cs*, in the `ValidateOneAdministratorAssignmentPerInstructor` method, specify no tracking, as shown in the following:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample12.cs?highlight=4)]

<span data-ttu-id="248d1-220">重复尝试编辑部门的**预算**金额。</span><span class="sxs-lookup"><span data-stu-id="248d1-220">Repeat your attempt to edit the **Budget** amount of a department.</span></span> <span data-ttu-id="248d1-221">此操作成功后，站点会按预期方式返回到 "部门索引" 页，其中显示了修改后的预算值。</span><span class="sxs-lookup"><span data-stu-id="248d1-221">This time the operation is successful, and the site returns as expected to the Departments Index page, showing the revised budget value.</span></span>

## <a name="examining-queries-sent-to-the-database"></a><span data-ttu-id="248d1-222">检查发送到数据库的查询</span><span class="sxs-lookup"><span data-stu-id="248d1-222">Examining Queries Sent to the Database</span></span>

<span data-ttu-id="248d1-223">有时能够以查看发送到数据库的实际 SQL 查询对于开发者来说是很有用的。</span><span class="sxs-lookup"><span data-stu-id="248d1-223">Sometimes it's helpful to be able to see the actual SQL queries that are sent to the database.</span></span> <span data-ttu-id="248d1-224">为此，可以在调试器中检查查询变量，或调用查询的 `ToString` 方法。</span><span class="sxs-lookup"><span data-stu-id="248d1-224">To do this, you can examine a query variable in the debugger or call the query's `ToString` method.</span></span> <span data-ttu-id="248d1-225">若要尝试此操作，你将看到一个简单的查询，然后在你添加预先加载、筛选和排序选项时，查看该查询所发生的情况。</span><span class="sxs-lookup"><span data-stu-id="248d1-225">To try this out, you'll look at a simple query and then look at what happens to it as you add options such eager loading, filtering, and sorting.</span></span>

<span data-ttu-id="248d1-226">在 controller */CourseController*中，将 `Index` 方法替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="248d1-226">In *Controllers/CourseController*, replace the `Index` method with the following code:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample13.cs?highlight=3)]

<span data-ttu-id="248d1-227">现在，在的*GenericRepository.cs*中设置一个断点，并在方法的语句上设置一个断点 `return query.ToList();` `return orderBy(query).ToList();` `Get` 。</span><span class="sxs-lookup"><span data-stu-id="248d1-227">Now set a breakpoint in *GenericRepository.cs* on the `return query.ToList();` and the `return orderBy(query).ToList();` statements of the `Get` method.</span></span> <span data-ttu-id="248d1-228">在调试模式下运行项目，然后选择 "课程索引" 页。</span><span class="sxs-lookup"><span data-stu-id="248d1-228">Run the project in debug mode and select the Course Index page.</span></span> <span data-ttu-id="248d1-229">当代码到达断点时，检查 `query` 变量。</span><span class="sxs-lookup"><span data-stu-id="248d1-229">When the code reaches the breakpoint, examine the `query` variable.</span></span> <span data-ttu-id="248d1-230">你会看到发送到 SQL Server 的查询。</span><span class="sxs-lookup"><span data-stu-id="248d1-230">You see the query that's sent to SQL Server.</span></span> <span data-ttu-id="248d1-231">这是一个简单的 `Select` 语句：</span><span class="sxs-lookup"><span data-stu-id="248d1-231">It's a simple `Select` statement:</span></span>

[!code-json[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample14.json)]

![](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image12.png)

<span data-ttu-id="248d1-232">查询可能太长，无法在 Visual Studio 中的调试窗口中显示。</span><span class="sxs-lookup"><span data-stu-id="248d1-232">Queries can be too long to display in the debugging windows in Visual Studio.</span></span> <span data-ttu-id="248d1-233">若要查看整个查询，可以复制变量值，并将其粘贴到文本编辑器中：</span><span class="sxs-lookup"><span data-stu-id="248d1-233">To see the entire query, you can copy the variable value and paste it into a text editor:</span></span>

![Copy_value_of_variable_in_debug_mode](https://asp.net/media/2578239/Windows-Live-Writer_Advanced-Entity-Framework-Scenarios-for-_CEF8_Copy_value_of_variable_in_debug_mode_0902a2b1-b799-47a6-9b4b-f266c79d83c1.png)

<span data-ttu-id="248d1-235">现在，您将向 "课程索引" 页添加一个下拉列表，以便用户可以筛选特定部门。</span><span class="sxs-lookup"><span data-stu-id="248d1-235">Now you'll add a drop-down list to the Course Index page so that users can filter for a particular department.</span></span> <span data-ttu-id="248d1-236">您将按标题对课程进行排序，并指定预先加载 `Department` 导航属性。</span><span class="sxs-lookup"><span data-stu-id="248d1-236">You'll sort the courses by title, and you'll specify eager loading for the `Department` navigation property.</span></span> <span data-ttu-id="248d1-237">在*CourseController.cs*中，将 `Index` 方法替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="248d1-237">In *CourseController.cs*, replace the `Index` method with the following code:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample15.cs)]

<span data-ttu-id="248d1-238">方法接收参数中下拉列表的选定值 `SelectedDepartment` 。</span><span class="sxs-lookup"><span data-stu-id="248d1-238">The method receives the selected value of the drop-down list in the `SelectedDepartment` parameter.</span></span> <span data-ttu-id="248d1-239">如果未选择任何内容，则此参数将为 null。</span><span class="sxs-lookup"><span data-stu-id="248d1-239">If nothing is selected, this parameter will be null.</span></span>

<span data-ttu-id="248d1-240">将 `SelectList` 包含所有部门的集合传递给下拉列表的视图。</span><span class="sxs-lookup"><span data-stu-id="248d1-240">A `SelectList` collection containing all departments is passed to the view for the drop-down list.</span></span> <span data-ttu-id="248d1-241">传递给 `SelectList` 构造函数的参数指定值字段名称、文本字段名称和选定项。</span><span class="sxs-lookup"><span data-stu-id="248d1-241">The parameters passed to the `SelectList` constructor specify the value field name, the text field name, and the selected item.</span></span>

<span data-ttu-id="248d1-242">对于 `Get` 存储库的方法 `Course` ，代码指定筛选器表达式、排序顺序以及预先加载 `Department` 导航属性。</span><span class="sxs-lookup"><span data-stu-id="248d1-242">For the `Get` method of the `Course` repository, the code specifies a filter expression, a sort order, and eager loading for the `Department` navigation property.</span></span> <span data-ttu-id="248d1-243">`true`如果未在下拉列表中选择任何内容，则筛选表达式始终返回 (即 `SelectedDepartment` 为 null) 。</span><span class="sxs-lookup"><span data-stu-id="248d1-243">The filter expression always returns `true` if nothing is selected in the drop-down list (that is, `SelectedDepartment` is null).</span></span>

<span data-ttu-id="248d1-244">在*Views\Course\Index.cshtml*中，紧跟在开始 `table` 标记之前，添加以下代码以创建下拉列表和 "提交" 按钮：</span><span class="sxs-lookup"><span data-stu-id="248d1-244">In *Views\Course\Index.cshtml*, immediately before the opening `table` tag, add the following code to create the drop-down list and a submit button:</span></span>

[!code-cshtml[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample16.cshtml)]

<span data-ttu-id="248d1-245">在类中仍设置断点的情况 `GenericRepository` 下，运行 "课程索引" 页。</span><span class="sxs-lookup"><span data-stu-id="248d1-245">With the breakpoints still set in the `GenericRepository` class, run the Course Index page.</span></span> <span data-ttu-id="248d1-246">继续执行第两次：代码命中断点，以便在浏览器中显示该页。</span><span class="sxs-lookup"><span data-stu-id="248d1-246">Continue through the first two times that the code hits a breakpoint, so that the page is displayed in the browser.</span></span> <span data-ttu-id="248d1-247">从下拉列表中选择一个部门，然后单击 "**筛选器**"：</span><span class="sxs-lookup"><span data-stu-id="248d1-247">Select a department from the drop-down list and click **Filter**:</span></span>

![Course_Index_page_with_department_selected](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image13.png)

<span data-ttu-id="248d1-249">这次，第一个断点将用于下拉列表的部门查询。</span><span class="sxs-lookup"><span data-stu-id="248d1-249">This time the first breakpoint will be for the departments query for the drop-down list.</span></span> <span data-ttu-id="248d1-250">跳过该操作，并在 `query` 下一次代码到达断点时查看变量，以便查看 `Course` 查询现在的外观。</span><span class="sxs-lookup"><span data-stu-id="248d1-250">Skip that and view the `query` variable the next time the code reaches the breakpoint in order to see what the `Course` query now looks like.</span></span> <span data-ttu-id="248d1-251">你将看到如下所示的内容：</span><span class="sxs-lookup"><span data-stu-id="248d1-251">You'll see something like the following:</span></span>

[!code-json[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample17.json)]

<span data-ttu-id="248d1-252">您可以看到，该查询现在是一个 `JOIN` 查询，该查询将 `Department` 数据与 `Course` 数据一起加载，并且它包含一个 `WHERE` 子句。</span><span class="sxs-lookup"><span data-stu-id="248d1-252">You can see that the query is now a `JOIN` query that loads `Department` data along with the `Course` data, and that it includes a `WHERE` clause.</span></span>

<a id="proxyclasses"></a>

## <a name="working-with-proxy-classes"></a><span data-ttu-id="248d1-253">使用代理类</span><span class="sxs-lookup"><span data-stu-id="248d1-253">Working with Proxy Classes</span></span>

<span data-ttu-id="248d1-254">如果实体框架创建实体实例 (例如，在执行查询) 时，它通常会将其创建为作为实体代理的动态生成的派生类型的实例。</span><span class="sxs-lookup"><span data-stu-id="248d1-254">When the Entity Framework creates entity instances (for example, when you execute a query), it often creates them as instances of a dynamically generated derived type that acts as a proxy for the entity.</span></span> <span data-ttu-id="248d1-255">此代理会重写实体的某些虚拟属性，以插入挂钩，以便在访问属性时自动执行操作。</span><span class="sxs-lookup"><span data-stu-id="248d1-255">This proxy overrides some virtual properties of the entity to insert hooks for performing actions automatically when the property is accessed.</span></span> <span data-ttu-id="248d1-256">例如，此机制用于支持关系的延迟加载。</span><span class="sxs-lookup"><span data-stu-id="248d1-256">For example, this mechanism is used to support lazy loading of relationships.</span></span>

<span data-ttu-id="248d1-257">大多数情况下，无需注意代理的这种使用，但有一些例外：</span><span class="sxs-lookup"><span data-stu-id="248d1-257">Most of the time you don't need to be aware of this use of proxies, but there are exceptions:</span></span>

- <span data-ttu-id="248d1-258">在某些情况下，你可能想要阻止实体框架创建代理实例。</span><span class="sxs-lookup"><span data-stu-id="248d1-258">In some scenarios you might want to prevent the Entity Framework from creating proxy instances.</span></span> <span data-ttu-id="248d1-259">例如，序列化非代理实例可能比序列化代理实例更有效。</span><span class="sxs-lookup"><span data-stu-id="248d1-259">For example, serializing non-proxy instances might be more efficient than serializing proxy instances.</span></span>
- <span data-ttu-id="248d1-260">如果使用运算符实例化实体类 `new` ，则不会获得代理实例。</span><span class="sxs-lookup"><span data-stu-id="248d1-260">When you instantiate an entity class using the `new` operator, you don't get a proxy instance.</span></span> <span data-ttu-id="248d1-261">这意味着不会获得延迟加载和自动更改跟踪等功能。</span><span class="sxs-lookup"><span data-stu-id="248d1-261">This means you don't get functionality such as lazy loading and automatic change tracking.</span></span> <span data-ttu-id="248d1-262">这通常是正常的;通常不需要延迟加载，因为你要创建的是不在数据库中的新实体，并且如果你将实体显式标记为，则通常不需要更改跟踪 `Added` 。</span><span class="sxs-lookup"><span data-stu-id="248d1-262">This is typically okay; you generally don't need lazy loading, because you're creating a new entity that isn't in the database, and you generally don't need change tracking if you're explicitly marking the entity as `Added`.</span></span> <span data-ttu-id="248d1-263">但是，如果确实需要延迟加载并且需要更改跟踪，则可以使用类的方法通过代理创建新的实体实例 `Create` `DbSet` 。</span><span class="sxs-lookup"><span data-stu-id="248d1-263">However, if you do need lazy loading and you need change tracking, you can create new entity instances with proxies using the `Create` method of the `DbSet` class.</span></span>
- <span data-ttu-id="248d1-264">你可能需要从代理类型获取实际的实体类型。</span><span class="sxs-lookup"><span data-stu-id="248d1-264">You might want to get an actual entity type from a proxy type.</span></span> <span data-ttu-id="248d1-265">您可以使用 `GetObjectType` 类的方法 `ObjectContext` 来获取代理类型实例的实际实体类型。</span><span class="sxs-lookup"><span data-stu-id="248d1-265">You can use the `GetObjectType` method of the `ObjectContext` class to get the actual entity type of a proxy type instance.</span></span>

<span data-ttu-id="248d1-266">有关详细信息，请参阅在实体框架团队博客上使用[代理](https://blogs.msdn.com/b/adonet/archive/2011/02/02/using-dbcontext-in-ef-feature-ctp5-part-8-working-with-proxies.aspx)。</span><span class="sxs-lookup"><span data-stu-id="248d1-266">For more information, see [Working with Proxies](https://blogs.msdn.com/b/adonet/archive/2011/02/02/using-dbcontext-in-ef-feature-ctp5-part-8-working-with-proxies.aspx) on the Entity Framework team blog.</span></span>

## <a name="disabling-automatic-detection-of-changes"></a><span data-ttu-id="248d1-267">禁用更改的自动检测</span><span class="sxs-lookup"><span data-stu-id="248d1-267">Disabling Automatic Detection of Changes</span></span>

<span data-ttu-id="248d1-268">Entity Framework 通过比较的实体的当前值与原始值来判断更改实体的方式 （因此需要发送更新到数据库）。</span><span class="sxs-lookup"><span data-stu-id="248d1-268">The Entity Framework determines how an entity has changed (and therefore which updates need to be sent to the database) by comparing the current values of an entity with the original values.</span></span> <span data-ttu-id="248d1-269">查询或附加实体时，会存储原始值。</span><span class="sxs-lookup"><span data-stu-id="248d1-269">The original values are stored when the entity was queried or attached.</span></span> <span data-ttu-id="248d1-270">如下方法会导致自动脏值：</span><span class="sxs-lookup"><span data-stu-id="248d1-270">Some of the methods that cause automatic change detection are the following:</span></span>

- `DbSet.Find`
- `DbSet.Local`
- `DbSet.Remove`
- `DbSet.Add`
- `DbSet.Attach`
- `DbContext.SaveChanges`
- `DbContext.GetValidationErrors`
- `DbContext.Entry`
- `DbChangeTracker.Entries`

<span data-ttu-id="248d1-271">如果正在跟踪大量实体，并且在循环中多次调用这些方法之一，则使用[AutoDetectChangesEnabled](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.autodetectchangesenabled(VS.103).aspx)属性暂时关闭自动更改检测可能会显著提高性能。</span><span class="sxs-lookup"><span data-stu-id="248d1-271">If you're tracking a large number of entities and you call one of these methods many times in a loop, you might get significant performance improvements by temporarily turning off automatic change detection using the [AutoDetectChangesEnabled](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.autodetectchangesenabled(VS.103).aspx) property.</span></span> <span data-ttu-id="248d1-272">有关详细信息，请参阅[自动检测更改](https://blogs.msdn.com/b/adonet/archive/2011/02/06/using-dbcontext-in-ef-feature-ctp5-part-12-automatically-detecting-changes.aspx)。</span><span class="sxs-lookup"><span data-stu-id="248d1-272">For more information, see [Automatically Detecting Changes](https://blogs.msdn.com/b/adonet/archive/2011/02/06/using-dbcontext-in-ef-feature-ctp5-part-12-automatically-detecting-changes.aspx).</span></span>

## <a name="disabling-validation-when-saving-changes"></a><span data-ttu-id="248d1-273">保存更改时禁用验证</span><span class="sxs-lookup"><span data-stu-id="248d1-273">Disabling Validation When Saving Changes</span></span>

<span data-ttu-id="248d1-274">在调用方法时 `SaveChanges` ，默认情况下，实体框架在更新数据库之前验证所有已更改实体的所有属性中的数据。</span><span class="sxs-lookup"><span data-stu-id="248d1-274">When you call the `SaveChanges` method, by default the Entity Framework validates the data in all properties of all changed entities before updating the database.</span></span> <span data-ttu-id="248d1-275">如果已更新大量实体，并且已验证数据，则不需要执行此操作，并且可以通过暂时关闭验证来使保存更改的过程更少。</span><span class="sxs-lookup"><span data-stu-id="248d1-275">If you've updated a large number of entities and you've already validated the data, this work is unnecessary and you could make the process of saving the changes take less time by temporarily turning off validation.</span></span> <span data-ttu-id="248d1-276">可以使用[ValidateOnSaveEnabled](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.validateonsaveenabled(VS.103).aspx)属性执行此操作。</span><span class="sxs-lookup"><span data-stu-id="248d1-276">You can do that using the [ValidateOnSaveEnabled](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.validateonsaveenabled(VS.103).aspx) property.</span></span> <span data-ttu-id="248d1-277">有关详细信息，请参阅[验证](https://blogs.msdn.com/b/adonet/archive/2010/12/15/ef-feature-ctp5-validation.aspx)。</span><span class="sxs-lookup"><span data-stu-id="248d1-277">For more information, see [Validation](https://blogs.msdn.com/b/adonet/archive/2010/12/15/ef-feature-ctp5-validation.aspx).</span></span>

## <a name="summary"></a><span data-ttu-id="248d1-278">摘要</span><span class="sxs-lookup"><span data-stu-id="248d1-278">Summary</span></span>

<span data-ttu-id="248d1-279">这将完成本系列教程，介绍如何在 ASP.NET MVC 应用程序中使用实体框架。</span><span class="sxs-lookup"><span data-stu-id="248d1-279">This completes this series of tutorials on using the Entity Framework in an ASP.NET MVC application.</span></span> <span data-ttu-id="248d1-280">可在[ASP.NET 数据访问内容映射](../../../../whitepapers/aspnet-data-access-content-map.md)中找到指向其他实体框架资源的链接。</span><span class="sxs-lookup"><span data-stu-id="248d1-280">Links to other Entity Framework resources can be found in the [ASP.NET Data Access Content Map](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

<span data-ttu-id="248d1-281">有关如何在生成 web 应用程序后对其进行部署的详细信息，请参阅 MSDN Library 中的[ASP.NET 部署内容映射](https://msdn.microsoft.com/library/bb386521.aspx)。</span><span class="sxs-lookup"><span data-stu-id="248d1-281">For more information about how to deploy your web application after you've built it, see [ASP.NET Deployment Content Map](https://msdn.microsoft.com/library/bb386521.aspx) in the MSDN Library.</span></span>

<span data-ttu-id="248d1-282">有关与 MVC 相关的其他主题（如身份验证和授权）的信息，请参阅[Mvc 推荐资源](../../getting-started/recommended-resources-for-mvc.md)。</span><span class="sxs-lookup"><span data-stu-id="248d1-282">For information about other topics related to MVC, such as authentication and authorization, see the [MVC Recommended Resources](../../getting-started/recommended-resources-for-mvc.md).</span></span>

<a id="acknowledgments"></a>

## <a name="acknowledgments"></a><span data-ttu-id="248d1-283">鸣谢</span><span class="sxs-lookup"><span data-stu-id="248d1-283">Acknowledgments</span></span>

- <span data-ttu-id="248d1-284">Tom Dykstra 编写了本教程的原始版本，它是 Microsoft Web 平台和工具内容团队的高级编程编写者。</span><span class="sxs-lookup"><span data-stu-id="248d1-284">Tom Dykstra wrote the original version of this tutorial and is a senior programming writer on the Microsoft Web Platform and Tools Content Team.</span></span>
- <span data-ttu-id="248d1-285">[Rick Anderson](https://blogs.msdn.com/b/rickandy/) (twitter [@RickAndMSFT](http://twitter.com/RickAndMSFT)) 共同创作此教程，并为 EF 5 和 MVC 4 更新了大部分工作。</span><span class="sxs-lookup"><span data-stu-id="248d1-285">[Rick Anderson](https://blogs.msdn.com/b/rickandy/) (twitter [@RickAndMSFT](http://twitter.com/RickAndMSFT)) co-authored this tutorial and did most of the work updating it for EF 5 and MVC 4.</span></span> <span data-ttu-id="248d1-286">Rick 是 Microsoft 的高级编程编写人员，侧重于 Azure 和 MVC。</span><span class="sxs-lookup"><span data-stu-id="248d1-286">Rick is a senior programming writer for Microsoft focusing on Azure and MVC.</span></span>
- <span data-ttu-id="248d1-287">[Rowan 莎莎](http://www.romiller.com)和实体框架团队的其他成员协助进行代码评审，并帮助调试在我们更新 EF 5 的教程时出现的许多迁移问题。</span><span class="sxs-lookup"><span data-stu-id="248d1-287">[Rowan Miller](http://www.romiller.com) and other members of the Entity Framework team assisted with code reviews and helped debug many issues with migrations that arose while we were updating the tutorial for EF 5.</span></span>

## <a name="vb"></a><span data-ttu-id="248d1-288">VB</span><span class="sxs-lookup"><span data-stu-id="248d1-288">VB</span></span>

<span data-ttu-id="248d1-289">最初生成本教程时，我们提供了已完成下载项目的 c # 和 VB 版本。</span><span class="sxs-lookup"><span data-stu-id="248d1-289">When the tutorial was originally produced, we provided both C# and VB versions of the completed download project.</span></span> <span data-ttu-id="248d1-290">通过此更新，我们将为每一章提供一个 c # 可下载项目，以便更轻松地开始使用序列中的任何位置，但由于存在时间限制，也不会为 VB 执行其他优先级操作。</span><span class="sxs-lookup"><span data-stu-id="248d1-290">With this update we are providing a C# downloadable project for each chapter to make it easier to get started anywhere in the series, but due to time limitations and other priorities we did not do that for VB.</span></span> <span data-ttu-id="248d1-291">如果使用这些教程生成 VB 项目，并愿意与他人共享，请告知我们。</span><span class="sxs-lookup"><span data-stu-id="248d1-291">If you build a VB project using these tutorials and would be willing to share that with others, please let us know.</span></span>

<a id="errors"></a>

## <a name="errors-and-workarounds"></a><span data-ttu-id="248d1-292">错误和解决方法</span><span class="sxs-lookup"><span data-stu-id="248d1-292">Errors and Workarounds</span></span>

### <a name="cannot-createshadow-copy"></a><span data-ttu-id="248d1-293">无法创建/隐藏副本</span><span class="sxs-lookup"><span data-stu-id="248d1-293">Cannot create/shadow copy</span></span>

<span data-ttu-id="248d1-294">错误消息：</span><span class="sxs-lookup"><span data-stu-id="248d1-294">Error Message:</span></span>

<span data-ttu-id="248d1-295">*如果文件已存在，则无法创建/影像复制 ' DotNetOpenAuth '。*</span><span class="sxs-lookup"><span data-stu-id="248d1-295">*Cannot create/shadow copy 'DotNetOpenAuth.OpenId' when that file already exists.*</span></span>

<span data-ttu-id="248d1-296">解决方案：</span><span class="sxs-lookup"><span data-stu-id="248d1-296">Solution:</span></span>

<span data-ttu-id="248d1-297">请等待几秒钟，然后刷新页面。</span><span class="sxs-lookup"><span data-stu-id="248d1-297">Wait a few seconds and refresh the page.</span></span>

### <a name="update-database-not-recognized"></a><span data-ttu-id="248d1-298">更新-无法识别数据库</span><span class="sxs-lookup"><span data-stu-id="248d1-298">Update-Database not recognized</span></span>

<span data-ttu-id="248d1-299">错误消息：</span><span class="sxs-lookup"><span data-stu-id="248d1-299">Error Message:</span></span>

<span data-ttu-id="248d1-300">*术语 "更新-数据库" 未被识别为 cmdlet、函数、脚本文件或可运行程序的名称。检查名称的拼写，如果包含路径，请验证路径是否正确，然后重试。* (*`Update-Database`* PMC 中的命令。 ) </span><span class="sxs-lookup"><span data-stu-id="248d1-300">*The term 'Update-Database' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again.*(From the *`Update-Database`* command in the PMC.)</span></span>

<span data-ttu-id="248d1-301">解决方案：</span><span class="sxs-lookup"><span data-stu-id="248d1-301">Solution:</span></span>

<span data-ttu-id="248d1-302">退出 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="248d1-302">Exit Visual Studio.</span></span> <span data-ttu-id="248d1-303">重新打开项目，然后重试。</span><span class="sxs-lookup"><span data-stu-id="248d1-303">Reopen project and try again.</span></span>

### <a name="validation-failed"></a><span data-ttu-id="248d1-304">验证失败</span><span class="sxs-lookup"><span data-stu-id="248d1-304">Validation failed</span></span>

<span data-ttu-id="248d1-305">错误消息：</span><span class="sxs-lookup"><span data-stu-id="248d1-305">Error Message:</span></span>

<span data-ttu-id="248d1-306">*对一个或多个实体的验证失败。有关更多详细信息，请参阅 "EntityValidationErrors" 属性。*</span><span class="sxs-lookup"><span data-stu-id="248d1-306">*Validation failed for one or more entities. See 'EntityValidationErrors' property for more details.*</span></span> <span data-ttu-id="248d1-307"> (*`Update-Database`* PMC 中的命令。 ) </span><span class="sxs-lookup"><span data-stu-id="248d1-307">(From the *`Update-Database`* command in the PMC.)</span></span>

<span data-ttu-id="248d1-308">解决方案：</span><span class="sxs-lookup"><span data-stu-id="248d1-308">Solution:</span></span>

<span data-ttu-id="248d1-309">此问题的一个原因是在方法运行时出现验证错误 `Seed` 。</span><span class="sxs-lookup"><span data-stu-id="248d1-309">One cause of this problem is validation errors when the `Seed` method runs.</span></span> <span data-ttu-id="248d1-310">有关调试方法的提示，请参阅[播种和调试实体框架 (EF) ](https://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx)数据库 `Seed` 。</span><span class="sxs-lookup"><span data-stu-id="248d1-310">See [Seeding and Debugging Entity Framework (EF) DBs](https://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx) for tips on debugging the `Seed` method.</span></span>

### <a name="http-50019-error"></a><span data-ttu-id="248d1-311">HTTP 500.19 错误</span><span class="sxs-lookup"><span data-stu-id="248d1-311">HTTP 500.19 error</span></span>

<span data-ttu-id="248d1-312">错误消息：</span><span class="sxs-lookup"><span data-stu-id="248d1-312">Error Message:</span></span>

<span data-ttu-id="248d1-313">*HTTP 错误 500.19-内部服务器错误无法访问请求的页面，因为该页的相关配置数据无效。*</span><span class="sxs-lookup"><span data-stu-id="248d1-313">*HTTP Error 500.19 - Internal Server Error The requested page cannot be accessed because the related configuration data for the page is invalid.*</span></span>

<span data-ttu-id="248d1-314">解决方案：</span><span class="sxs-lookup"><span data-stu-id="248d1-314">Solution:</span></span>

<span data-ttu-id="248d1-315">获取此错误的一种方法是使用解决方案的多个副本，每个副本使用相同的端口号。</span><span class="sxs-lookup"><span data-stu-id="248d1-315">One way you can get this error is from having multiple copies of the solution, each of them using the same port number.</span></span> <span data-ttu-id="248d1-316">通常可以通过退出 Visual Studio 的所有实例，然后重新启动正在处理的项目，来解决此问题。</span><span class="sxs-lookup"><span data-stu-id="248d1-316">You can usually solve this problem by exiting all instances of Visual Studio, then restarting the project your working on.</span></span> <span data-ttu-id="248d1-317">如果这不起作用，请尝试更改端口号。</span><span class="sxs-lookup"><span data-stu-id="248d1-317">If that doesn't work, try changing the port number.</span></span> <span data-ttu-id="248d1-318">右键单击项目文件，然后单击 "属性"。</span><span class="sxs-lookup"><span data-stu-id="248d1-318">Right click on the project file and then click properties.</span></span> <span data-ttu-id="248d1-319">选择 " **Web** " 选项卡，然后在 "**项目 Url** " 文本框中更改端口号。</span><span class="sxs-lookup"><span data-stu-id="248d1-319">Select the **Web** tab and then change the port number in the **Project Url** text box.</span></span>

### <a name="error-locating-sql-server-instance"></a><span data-ttu-id="248d1-320">定位 SQL Server 实例出错</span><span class="sxs-lookup"><span data-stu-id="248d1-320">Error locating SQL Server instance</span></span>

<span data-ttu-id="248d1-321">错误消息：</span><span class="sxs-lookup"><span data-stu-id="248d1-321">Error Message:</span></span>

<span data-ttu-id="248d1-322">\*建立与 SQL Server 的连接时出现与网络相关或特定于实例的错误。找不到或无法访问服务器。请验证实例名称是否正确，以及 SQL Server 是否配置为允许远程连接。 (提供程序： SQL 网络接口，错误： 26-定位指定的服务器/实例时出错) \*</span><span class="sxs-lookup"><span data-stu-id="248d1-322">*A network-related or instance-specific error occurred while establishing a connection to SQL Server. The server was not found or was not accessible. Verify that the instance name is correct and that SQL Server is configured to allow remote connections. (provider: SQL Network Interfaces, error: 26 - Error Locating Server/Instance Specified)*</span></span>

<span data-ttu-id="248d1-323">解决方案：</span><span class="sxs-lookup"><span data-stu-id="248d1-323">Solution:</span></span>

<span data-ttu-id="248d1-324">检查连接字符串。</span><span class="sxs-lookup"><span data-stu-id="248d1-324">Check connection string.</span></span> <span data-ttu-id="248d1-325">如果手动删除了数据库，请在构造字符串中更改数据库的名称。</span><span class="sxs-lookup"><span data-stu-id="248d1-325">If you have manually deleted the database, change the name of the database in the construction string.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="248d1-326">[上一页](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md)
> [下一页](building-the-ef5-mvc4-chapter-downloads.md)</span><span class="sxs-lookup"><span data-stu-id="248d1-326">[Previous](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md)
[Next](building-the-ef5-mvc4-chapter-downloads.md)</span></span>

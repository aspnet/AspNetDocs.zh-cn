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
ms.openlocfilehash: d7cc83a5b78a60f575f5c3065079679189296a0c
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "86188665"
---
# <a name="tutorial-learn-about-advanced-ef-scenarios-for-an-mvc-5-web-app"></a><span data-ttu-id="65a15-103">教程：了解 MVC 5 Web 应用的高级 EF 方案</span><span class="sxs-lookup"><span data-stu-id="65a15-103">Tutorial: Learn about advanced EF Scenarios for an MVC 5 Web app</span></span>

<span data-ttu-id="65a15-104">在上一教程中，您实现了每个层次结构一个表继承。</span><span class="sxs-lookup"><span data-stu-id="65a15-104">In the previous tutorial you implemented table-per-hierarchy inheritance.</span></span> <span data-ttu-id="65a15-105">本教程介绍了几个主题，这些主题可帮助你了解开发使用实体框架 Code First 的 ASP.NET web 应用程序的基础知识。</span><span class="sxs-lookup"><span data-stu-id="65a15-105">This tutorial includes introduces several topics that are useful to be aware of when you go beyond the basics of developing ASP.NET web applications that use Entity Framework Code First.</span></span> <span data-ttu-id="65a15-106">前几部分都提供了分步说明，指导你完成代码并使用 Visual Studio 完成任务。下面的部分将介绍几个主题，其中包含简短的简介，并提供有关详细信息的资源链接。</span><span class="sxs-lookup"><span data-stu-id="65a15-106">The first few sections have step-by-step instructions that walk you through the code and using Visual Studio to complete tasks The sections that follow introduce several topics with brief introductions followed by links to resources for more information.</span></span>

<span data-ttu-id="65a15-107">对于大多数这些主题，你将使用已创建的页面。</span><span class="sxs-lookup"><span data-stu-id="65a15-107">For most of these topics, you'll work with pages that you already created.</span></span> <span data-ttu-id="65a15-108">若要使用原始 SQL 执行批量更新，您将创建一个新页，用于更新数据库中所有课程的信用额度：</span><span class="sxs-lookup"><span data-stu-id="65a15-108">To use raw SQL to do bulk updates you'll create a new page that updates the number of credits of all courses in the database:</span></span>

![Update_Course_Credits_initial_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image1.png)

<span data-ttu-id="65a15-110">在本教程中，你将了解：</span><span class="sxs-lookup"><span data-stu-id="65a15-110">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="65a15-111">执行原始 SQL 查询</span><span class="sxs-lookup"><span data-stu-id="65a15-111">Perform raw SQL queries</span></span>
> * <span data-ttu-id="65a15-112">执行无跟踪查询</span><span class="sxs-lookup"><span data-stu-id="65a15-112">Perform no-tracking queries</span></span>
> * <span data-ttu-id="65a15-113">检查发送到数据库的 SQL 查询</span><span class="sxs-lookup"><span data-stu-id="65a15-113">Examine SQL queries sent to database</span></span>

<span data-ttu-id="65a15-114">你还将了解：</span><span class="sxs-lookup"><span data-stu-id="65a15-114">You also learn about:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="65a15-115">创建抽象层</span><span class="sxs-lookup"><span data-stu-id="65a15-115">Creating an abstraction layer</span></span>
> * <span data-ttu-id="65a15-116">代理类</span><span class="sxs-lookup"><span data-stu-id="65a15-116">Proxy classes</span></span>
> * <span data-ttu-id="65a15-117">自动脏值检测</span><span class="sxs-lookup"><span data-stu-id="65a15-117">Automatic change detection</span></span>
> * <span data-ttu-id="65a15-118">自动验证</span><span class="sxs-lookup"><span data-stu-id="65a15-118">Automatic validation</span></span>
> * <span data-ttu-id="65a15-119">实体框架 Power Tools</span><span class="sxs-lookup"><span data-stu-id="65a15-119">Entity Framework Power Tools</span></span>
> * <span data-ttu-id="65a15-120">实体框架源代码</span><span class="sxs-lookup"><span data-stu-id="65a15-120">Entity Framework source code</span></span>

## <a name="prerequisite"></a><span data-ttu-id="65a15-121">先决条件</span><span class="sxs-lookup"><span data-stu-id="65a15-121">Prerequisite</span></span>

* [<span data-ttu-id="65a15-122">实现继承</span><span class="sxs-lookup"><span data-stu-id="65a15-122">Implementing Inheritance</span></span>](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="perform-raw-sql-queries"></a><span data-ttu-id="65a15-123">执行原始 SQL 查询</span><span class="sxs-lookup"><span data-stu-id="65a15-123">Perform raw SQL queries</span></span>

<span data-ttu-id="65a15-124">实体框架 Code First API 包括使你能够将 SQL 命令直接传递到数据库的方法。</span><span class="sxs-lookup"><span data-stu-id="65a15-124">The Entity Framework Code First API includes methods that enable you to pass SQL commands directly to the database.</span></span> <span data-ttu-id="65a15-125">你有以下选择：</span><span class="sxs-lookup"><span data-stu-id="65a15-125">You have the following options:</span></span>

- <span data-ttu-id="65a15-126">对于返回实体类型的查询，请使用[DbSet. SqlQuery](https://msdn.microsoft.com/library/system.data.entity.dbset.sqlquery.aspx)方法。</span><span class="sxs-lookup"><span data-stu-id="65a15-126">Use the [DbSet.SqlQuery](https://msdn.microsoft.com/library/system.data.entity.dbset.sqlquery.aspx) method for queries that return entity types.</span></span> <span data-ttu-id="65a15-127">返回的对象必须是对象所需的类型 `DbSet` ，并且数据库上下文会自动跟踪这些对象，除非关闭跟踪。</span><span class="sxs-lookup"><span data-stu-id="65a15-127">The returned objects must be of the type expected by the `DbSet` object, and they are automatically tracked by the database context unless you turn tracking off.</span></span> <span data-ttu-id="65a15-128"> (参见以下有关[AsNoTracking](https://msdn.microsoft.com/library/system.data.entity.dbextensions.asnotracking.aspx)方法的部分。 ) </span><span class="sxs-lookup"><span data-stu-id="65a15-128">(See the following section about the [AsNoTracking](https://msdn.microsoft.com/library/system.data.entity.dbextensions.asnotracking.aspx) method.)</span></span>
- <span data-ttu-id="65a15-129">对于返回非实体类型的查询，请使用[SqlQuery](https://msdn.microsoft.com/library/system.data.entity.database.sqlquery.aspx)方法。</span><span class="sxs-lookup"><span data-stu-id="65a15-129">Use the [Database.SqlQuery](https://msdn.microsoft.com/library/system.data.entity.database.sqlquery.aspx) method for queries that return types that aren't entities.</span></span> <span data-ttu-id="65a15-130">数据库上下文不会跟踪返回的数据，即使你使用该方法来检索实体类型也是如此。</span><span class="sxs-lookup"><span data-stu-id="65a15-130">The returned data isn't tracked by the database context, even if you use this method to retrieve entity types.</span></span>
- <span data-ttu-id="65a15-131">将[Database.ExecuteSqlCommand](https://msdn.microsoft.com/library/gg679456.aspx)用于非查询命令。</span><span class="sxs-lookup"><span data-stu-id="65a15-131">Use the [Database.ExecuteSqlCommand](https://msdn.microsoft.com/library/gg679456.aspx) for non-query commands.</span></span>

<span data-ttu-id="65a15-132">使用 Entity Framework 的优点之一是它可避免你编写跟数据库过于耦合的代码</span><span class="sxs-lookup"><span data-stu-id="65a15-132">One of the advantages of using the Entity Framework is that it avoids tying your code too closely to a particular method of storing data.</span></span> <span data-ttu-id="65a15-133">它会自动生成 SQL 查询和命令，使得你无需自行编写。</span><span class="sxs-lookup"><span data-stu-id="65a15-133">It does this by generating SQL queries and commands for you, which also frees you from having to write them yourself.</span></span> <span data-ttu-id="65a15-134">但在某些情况下，你需要运行已手动创建的特定 SQL 查询，并且这些方法使你能够处理此类异常。</span><span class="sxs-lookup"><span data-stu-id="65a15-134">But there are exceptional scenarios when you need to run specific SQL queries that you have manually created, and these methods make it possible for you to handle such exceptions.</span></span>

<span data-ttu-id="65a15-135">在 Web 应用程序中执行 SQL 命令时，请务必采取预防措施来保护站点免受 SQL 注入攻击。</span><span class="sxs-lookup"><span data-stu-id="65a15-135">As is always true when you execute SQL commands in a web application, you must take precautions to protect your site against SQL injection attacks.</span></span> <span data-ttu-id="65a15-136">一种方法是使用参数化查询，确保不会将网页提交的字符串视为 SQL 命令。</span><span class="sxs-lookup"><span data-stu-id="65a15-136">One way to do that is to use parameterized queries to make sure that strings submitted by a web page can't be interpreted as SQL commands.</span></span> <span data-ttu-id="65a15-137">在本教程中，将用户输入集成到查询中时会使用参数化查询。</span><span class="sxs-lookup"><span data-stu-id="65a15-137">In this tutorial you'll use parameterized queries when integrating user input into a query.</span></span>

### <a name="calling-a-query-that-returns-entities"></a><span data-ttu-id="65a15-138">调用返回实体的查询</span><span class="sxs-lookup"><span data-stu-id="65a15-138">Calling a Query that Returns Entities</span></span>

<span data-ttu-id="65a15-139">[DbSet &lt; &gt; TEntity](https://msdn.microsoft.com/library/gg696460.aspx)类提供一个方法，该方法可用于执行返回类型为的实体的查询 `TEntity` 。</span><span class="sxs-lookup"><span data-stu-id="65a15-139">The [DbSet&lt;TEntity&gt;](https://msdn.microsoft.com/library/gg696460.aspx) class provides a method that you can use to execute a query that returns an entity of type `TEntity`.</span></span> <span data-ttu-id="65a15-140">若要查看其工作原理，请更改控制器的方法中的代码 `Details` `Department` 。</span><span class="sxs-lookup"><span data-stu-id="65a15-140">To see how this works you'll change the code in the `Details` method of the `Department` controller.</span></span>

<span data-ttu-id="65a15-141">在*DepartmentController.cs*中，在 `Details` 方法中，将 `db.Departments.FindAsync` 方法调用替换为 `db.Departments.SqlQuery` 方法调用，如以下突出显示的代码所示：</span><span class="sxs-lookup"><span data-stu-id="65a15-141">In *DepartmentController.cs*, in the `Details` method, replace the `db.Departments.FindAsync` method call with a `db.Departments.SqlQuery` method call, as shown in the following highlighted code:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample1.cs?highlight=8-14)]

<span data-ttu-id="65a15-142">为了验证新代码是否正常工作，请选择“院系”选项卡，然后选择其中某一院系的“详细信息” 。</span><span class="sxs-lookup"><span data-stu-id="65a15-142">To verify that the new code works correctly, select the **Departments** tab and then **Details** for one of the departments.</span></span> <span data-ttu-id="65a15-143">确保所有数据都按预期方式显示。</span><span class="sxs-lookup"><span data-stu-id="65a15-143">Make sure all of the data displays as expected.</span></span>

### <a name="calling-a-query-that-returns-other-types-of-objects"></a><span data-ttu-id="65a15-144">调用返回其他类型对象的查询</span><span class="sxs-lookup"><span data-stu-id="65a15-144">Calling a Query that Returns Other Types of Objects</span></span>

<span data-ttu-id="65a15-145">之前你在“关于”页面创建了一个学生统计信息网格，显示每个注册日期的学生数量。</span><span class="sxs-lookup"><span data-stu-id="65a15-145">Earlier you created a student statistics grid for the About page that showed the number of students for each enrollment date.</span></span> <span data-ttu-id="65a15-146">在*HomeController.cs*中执行此操作的代码使用 LINQ：</span><span class="sxs-lookup"><span data-stu-id="65a15-146">The code that does this in *HomeController.cs* uses LINQ:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample2.cs)]

<span data-ttu-id="65a15-147">假设您要编写在 SQL 中直接检索此数据的代码，而不是使用 LINQ。</span><span class="sxs-lookup"><span data-stu-id="65a15-147">Suppose you want to write the code that retrieves this data directly in SQL rather than using LINQ.</span></span> <span data-ttu-id="65a15-148">为此，您需要运行一个返回除 entity 对象之外的内容的查询，这意味着您需要使用[SqlQuery](https://msdn.microsoft.com/library/system.data.entity.database.sqlquery(v=VS.103).aspx)方法。</span><span class="sxs-lookup"><span data-stu-id="65a15-148">To do that you need to run a query that returns something other than entity objects, which means you need to use the [Database.SqlQuery](https://msdn.microsoft.com/library/system.data.entity.database.sqlquery(v=VS.103).aspx) method.</span></span>

<span data-ttu-id="65a15-149">在*HomeController.cs*中，将方法中的 LINQ 语句替换为 `About` SQL 语句，如以下突出显示的代码所示：</span><span class="sxs-lookup"><span data-stu-id="65a15-149">In *HomeController.cs*, replace the LINQ statement in the `About` method with a SQL statement, as shown in the following highlighted code:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample3.cs?highlight=3-18)]

<span data-ttu-id="65a15-150">运行 "关于" 页。</span><span class="sxs-lookup"><span data-stu-id="65a15-150">Run the About page.</span></span> <span data-ttu-id="65a15-151">验证它是否显示与以前相同的数据。</span><span class="sxs-lookup"><span data-stu-id="65a15-151">Verify that it displays the same data it did before.</span></span>

### <a name="calling-an-update-query"></a><span data-ttu-id="65a15-152">调用更新查询</span><span class="sxs-lookup"><span data-stu-id="65a15-152">Calling an Update Query</span></span>

<span data-ttu-id="65a15-153">假设 Contoso 大学管理员希望能够在数据库中执行大容量更改，如更改每个课程的信用额度。</span><span class="sxs-lookup"><span data-stu-id="65a15-153">Suppose Contoso University administrators want to be able to perform bulk changes in the database, such as changing the number of credits for every course.</span></span> <span data-ttu-id="65a15-154">如果该大学提供了大量课程，那么将所有课程作为实体来检索并单独更改就非常低效。</span><span class="sxs-lookup"><span data-stu-id="65a15-154">If the university has a large number of courses, it would be inefficient to retrieve them all as entities and change them individually.</span></span> <span data-ttu-id="65a15-155">在本节中，您将实现一个网页，该网页使用户能够指定更改所有课程的信用额度的因素，并通过执行 SQL 语句进行更改 `UPDATE` 。</span><span class="sxs-lookup"><span data-stu-id="65a15-155">In this section you'll implement a web page that enables the user to specify a factor by which to change the number of credits for all courses, and you'll make the change by executing a SQL `UPDATE` statement.</span></span> 

<span data-ttu-id="65a15-156">在*CourseController.cs*中， `UpdateCourseCredits` 为和添加方法 `HttpGet` `HttpPost` ：</span><span class="sxs-lookup"><span data-stu-id="65a15-156">In *CourseController.cs*, add `UpdateCourseCredits` methods for `HttpGet` and `HttpPost`:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample4.cs)]

<span data-ttu-id="65a15-157">当控制器处理请求时 `HttpGet` ，变量中将不会返回任何内容 `ViewBag.RowsAffected` ，并且该视图将显示一个空的文本框和一个提交按钮。</span><span class="sxs-lookup"><span data-stu-id="65a15-157">When the controller processes an `HttpGet` request, nothing is returned in the `ViewBag.RowsAffected` variable, and the view displays an empty text box and a submit button.</span></span>

<span data-ttu-id="65a15-158">单击 "**更新**" 按钮时，将 `HttpPost` 调用方法，并在 `multiplier` 文本框中输入值。</span><span class="sxs-lookup"><span data-stu-id="65a15-158">When the **Update** button is clicked, the `HttpPost` method is called, and `multiplier` has the value entered in the text box.</span></span> <span data-ttu-id="65a15-159">然后，该代码执行更新课程的 SQL，并将受影响的行数返回到变量中的视图 `ViewBag.RowsAffected` 。</span><span class="sxs-lookup"><span data-stu-id="65a15-159">The code then executes the SQL that updates courses and returns the number of affected rows to the view in the `ViewBag.RowsAffected` variable.</span></span> <span data-ttu-id="65a15-160">当视图获取该变量中的值时，它将显示更新的行数，而不是文本框和提交按钮。</span><span class="sxs-lookup"><span data-stu-id="65a15-160">When the view gets a value in that variable, it displays the number of rows updated instead of the text box and submit button.</span></span>

<span data-ttu-id="65a15-161">在*CourseController.cs*中，右键单击其中一个 `UpdateCourseCredits` 方法，然后单击 "**添加视图**"。</span><span class="sxs-lookup"><span data-stu-id="65a15-161">In *CourseController.cs*, right-click one of the `UpdateCourseCredits` methods, and then click **Add View**.</span></span> <span data-ttu-id="65a15-162">此时将显示 "**添加视图**" 对话框。</span><span class="sxs-lookup"><span data-stu-id="65a15-162">The **Add View** dialog appears.</span></span> <span data-ttu-id="65a15-163">保留默认值，然后选择 "**添加**"。</span><span class="sxs-lookup"><span data-stu-id="65a15-163">Leave the defaults and select **Add**.</span></span>

<span data-ttu-id="65a15-164">在*Views\Course\UpdateCourseCredits.cshtml*中，将模板代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="65a15-164">In *Views\Course\UpdateCourseCredits.cshtml*, replace the template code with the following code:</span></span>

[!code-cshtml[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample5.cshtml)]

<span data-ttu-id="65a15-165">通过选择**Courses**选项卡运行`UpdateCourseCredits`方法，然后在浏览器地址栏中 URL 的末尾添加"/ UpdateCourseCredits"到 (例如： `http://localhost:50205/Course/UpdateCourseCredits`)。</span><span class="sxs-lookup"><span data-stu-id="65a15-165">Run the `UpdateCourseCredits` method by selecting the **Courses** tab, then adding "/UpdateCourseCredits" to the end of the URL in the browser's address bar (for example: `http://localhost:50205/Course/UpdateCourseCredits`).</span></span> <span data-ttu-id="65a15-166">在文本框中输入数字：</span><span class="sxs-lookup"><span data-stu-id="65a15-166">Enter a number in the text box:</span></span>

![Update_Course_Credits_initial_page_with_2_entered](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image1.png)

<span data-ttu-id="65a15-168">单击“更新”。</span><span class="sxs-lookup"><span data-stu-id="65a15-168">Click **Update**.</span></span> <span data-ttu-id="65a15-169">你会看到受影响的行数。</span><span class="sxs-lookup"><span data-stu-id="65a15-169">You see the number of rows affected.</span></span>

<span data-ttu-id="65a15-170">单击“返回列表”可以查看课程列表，其中学分已替换为修改后的数字。</span><span class="sxs-lookup"><span data-stu-id="65a15-170">Click **Back to List** to see the list of courses with the revised number of credits.</span></span>

<span data-ttu-id="65a15-171">有关原始 SQL 查询的详细信息，请参阅 MSDN 上的[原始 Sql 查询](https://msdn.microsoft.com/data/jj592907)。</span><span class="sxs-lookup"><span data-stu-id="65a15-171">For more information about raw SQL queries, see [Raw SQL Queries](https://msdn.microsoft.com/data/jj592907) on MSDN.</span></span>

## <a name="no-tracking-queries"></a><span data-ttu-id="65a15-172">非跟踪查询</span><span class="sxs-lookup"><span data-stu-id="65a15-172">No-tracking queries</span></span>

<span data-ttu-id="65a15-173">当数据库上下文检索表行并创建表示它们的实体对象时，默认情况下，它会跟踪内存中的实体是否与数据库中的内容同步。</span><span class="sxs-lookup"><span data-stu-id="65a15-173">When a database context retrieves table rows and creates entity objects that represent them, by default it keeps track of whether the entities in memory are in sync with what's in the database.</span></span> <span data-ttu-id="65a15-174">更新实体时，内存中的数据充当缓存并使用该数据。</span><span class="sxs-lookup"><span data-stu-id="65a15-174">The data in memory acts as a cache and is used when you update an entity.</span></span> <span data-ttu-id="65a15-175">在 Web 应用程序中，此缓存通常是不必要的，因为上下文实例通常生存期较短（创建新的实例并用于处理每个请求），并且通常在再次使用该实体之前处理读取实体的上下文。</span><span class="sxs-lookup"><span data-stu-id="65a15-175">This caching is often unnecessary in a web application because context instances are typically short-lived (a new one is created and disposed for each request) and the context that reads an entity is typically disposed before that entity is used again.</span></span>

<span data-ttu-id="65a15-176">您可以使用[AsNoTracking](https://msdn.microsoft.com/library/gg679352(v=vs.103).aspx)方法禁用内存中实体对象的跟踪。</span><span class="sxs-lookup"><span data-stu-id="65a15-176">You can disable tracking of entity objects in memory by using the [AsNoTracking](https://msdn.microsoft.com/library/gg679352(v=vs.103).aspx) method.</span></span> <span data-ttu-id="65a15-177">可能想要执行的典型方案包括以下操作：</span><span class="sxs-lookup"><span data-stu-id="65a15-177">Typical scenarios in which you might want to do that include the following:</span></span>

- <span data-ttu-id="65a15-178">查询检索到关闭跟踪可能会明显提高性能的大量数据。</span><span class="sxs-lookup"><span data-stu-id="65a15-178">A query retrieves such a large volume of data that turning off tracking might noticeably enhance performance.</span></span>
- <span data-ttu-id="65a15-179">您希望附加实体以便对其进行更新，但您之前检索到不同用途的同一实体。</span><span class="sxs-lookup"><span data-stu-id="65a15-179">You want to attach an entity in order to update it, but you earlier retrieved the same entity for a different purpose.</span></span> <span data-ttu-id="65a15-180">由于数据库上下文已跟踪了该实体，因此无法附加要更改的实体。</span><span class="sxs-lookup"><span data-stu-id="65a15-180">Because the entity is already being tracked by the database context, you can't attach the entity that you want to change.</span></span> <span data-ttu-id="65a15-181">解决这种情况的一种方法是将 `AsNoTracking` 选项与前面的查询一起使用。</span><span class="sxs-lookup"><span data-stu-id="65a15-181">One way to handle this situation is to use the `AsNoTracking` option with the earlier query.</span></span>

<span data-ttu-id="65a15-182">有关演示如何使用[AsNoTracking](https://msdn.microsoft.com/library/gg679352(v=vs.103).aspx)方法的示例，请参阅[本教程的早期版本](../../older-versions/getting-started-with-ef-5-using-mvc-4/advanced-entity-framework-scenarios-for-an-mvc-web-application.md)。</span><span class="sxs-lookup"><span data-stu-id="65a15-182">For an example that demonstrates how to use the [AsNoTracking](https://msdn.microsoft.com/library/gg679352(v=vs.103).aspx) method, see [the earlier version of this tutorial](../../older-versions/getting-started-with-ef-5-using-mvc-4/advanced-entity-framework-scenarios-for-an-mvc-web-application.md).</span></span> <span data-ttu-id="65a15-183">此版本的教程不会在编辑方法中对已创建模型联编程序的实体设置修改标志，因此不需要 `AsNoTracking` 。</span><span class="sxs-lookup"><span data-stu-id="65a15-183">This version of the tutorial doesn't set the Modified flag on a model-binder-created entity in the Edit method, so it doesn't need `AsNoTracking`.</span></span>

## <a name="examine-sql-sent-to-database"></a><span data-ttu-id="65a15-184">检查发送到数据库的 SQL</span><span class="sxs-lookup"><span data-stu-id="65a15-184">Examine SQL sent to database</span></span>

<span data-ttu-id="65a15-185">有时能够以查看发送到数据库的实际 SQL 查询对于开发者来说是很有用的。</span><span class="sxs-lookup"><span data-stu-id="65a15-185">Sometimes it's helpful to be able to see the actual SQL queries that are sent to the database.</span></span> <span data-ttu-id="65a15-186">在前面的教程中，你已了解如何在侦听器代码中执行此操作;现在，你将看到一些无需编写侦听器代码即可执行此操作的方法。</span><span class="sxs-lookup"><span data-stu-id="65a15-186">In an earlier tutorial you saw how to do that in interceptor code; now you'll see some ways to do it without writing interceptor code.</span></span> <span data-ttu-id="65a15-187">若要尝试此操作，你将看到一个简单的查询，然后在你添加预先加载、筛选和排序选项时，查看该查询所发生的情况。</span><span class="sxs-lookup"><span data-stu-id="65a15-187">To try this out, you'll look at a simple query and then look at what happens to it as you add options such eager loading, filtering, and sorting.</span></span>

<span data-ttu-id="65a15-188">在 controller */CourseController*中，将 `Index` 方法替换为以下代码，以便暂时停止预先加载：</span><span class="sxs-lookup"><span data-stu-id="65a15-188">In *Controllers/CourseController*, replace the `Index` method with the following code, in order to temporarily stop eager loading:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample6.cs)]

<span data-ttu-id="65a15-189">现在，在语句上设置一个断点 `return` (F9，并将光标置于该行) 上。</span><span class="sxs-lookup"><span data-stu-id="65a15-189">Now set a breakpoint on the `return` statement (F9 with the cursor on that line).</span></span> <span data-ttu-id="65a15-190">按**F5**在调试模式下运行项目，然后选择 "课程索引" 页。</span><span class="sxs-lookup"><span data-stu-id="65a15-190">Press **F5** to run the project in debug mode, and select the Course Index page.</span></span> <span data-ttu-id="65a15-191">当代码到达断点时，检查 `sql` 变量。</span><span class="sxs-lookup"><span data-stu-id="65a15-191">When the code reaches the breakpoint, examine the `sql` variable.</span></span> <span data-ttu-id="65a15-192">你会看到发送到 SQL Server 的查询。</span><span class="sxs-lookup"><span data-stu-id="65a15-192">You see the query that's sent to SQL Server.</span></span> <span data-ttu-id="65a15-193">这是一个简单的 `Select` 语句。</span><span class="sxs-lookup"><span data-stu-id="65a15-193">It's a simple `Select` statement.</span></span>

[!code-json[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample7.json)]

<span data-ttu-id="65a15-194">单击放大镜可查看**文本可视化工具**中的查询。</span><span class="sxs-lookup"><span data-stu-id="65a15-194">Click the magnifying glass to see the query in the **Text Visualizer**.</span></span>

![](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image10.png)

<span data-ttu-id="65a15-195">现在，你将向 "课程索引" 页添加一个下拉列表，以便用户可以筛选特定部门。</span><span class="sxs-lookup"><span data-stu-id="65a15-195">Now you'll add a drop-down list to the Courses Index page so that users can filter for a particular department.</span></span> <span data-ttu-id="65a15-196">您将按标题对课程进行排序，并指定预先加载 `Department` 导航属性。</span><span class="sxs-lookup"><span data-stu-id="65a15-196">You'll sort the courses by title, and you'll specify eager loading for the `Department` navigation property.</span></span>

<span data-ttu-id="65a15-197">在*CourseController.cs*中，将 `Index` 方法替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="65a15-197">In *CourseController.cs*, replace the `Index` method with the following code:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample8.cs)]

<span data-ttu-id="65a15-198">还原语句上的断点 `return` 。</span><span class="sxs-lookup"><span data-stu-id="65a15-198">Restore the breakpoint on the `return` statement.</span></span>

<span data-ttu-id="65a15-199">方法接收参数中下拉列表的选定值 `SelectedDepartment` 。</span><span class="sxs-lookup"><span data-stu-id="65a15-199">The method receives the selected value of the drop-down list in the `SelectedDepartment` parameter.</span></span> <span data-ttu-id="65a15-200">如果未选择任何内容，则此参数将为 null。</span><span class="sxs-lookup"><span data-stu-id="65a15-200">If nothing is selected, this parameter will be null.</span></span>

<span data-ttu-id="65a15-201">将 `SelectList` 包含所有部门的集合传递给下拉列表的视图。</span><span class="sxs-lookup"><span data-stu-id="65a15-201">A `SelectList` collection containing all departments is passed to the view for the drop-down list.</span></span> <span data-ttu-id="65a15-202">传递给 `SelectList` 构造函数的参数指定值字段名称、文本字段名称和选定项。</span><span class="sxs-lookup"><span data-stu-id="65a15-202">The parameters passed to the `SelectList` constructor specify the value field name, the text field name, and the selected item.</span></span>

<span data-ttu-id="65a15-203">对于 `Get` 存储库的方法 `Course` ，代码指定筛选器表达式、排序顺序以及预先加载 `Department` 导航属性。</span><span class="sxs-lookup"><span data-stu-id="65a15-203">For the `Get` method of the `Course` repository, the code specifies a filter expression, a sort order, and eager loading for the `Department` navigation property.</span></span> <span data-ttu-id="65a15-204">`true`如果未在下拉列表中选择任何内容，则筛选表达式始终返回 (即 `SelectedDepartment` 为 null) 。</span><span class="sxs-lookup"><span data-stu-id="65a15-204">The filter expression always returns `true` if nothing is selected in the drop-down list (that is, `SelectedDepartment` is null).</span></span>

<span data-ttu-id="65a15-205">在*Views\Course\Index.cshtml*中，紧跟在开始 `table` 标记之前，添加以下代码以创建下拉列表和 "提交" 按钮：</span><span class="sxs-lookup"><span data-stu-id="65a15-205">In *Views\Course\Index.cshtml*, immediately before the opening `table` tag, add the following code to create the drop-down list and a submit button:</span></span>

[!code-cshtml[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample9.cshtml)]

<span data-ttu-id="65a15-206">仍设置断点后，运行 "课程索引" 页。</span><span class="sxs-lookup"><span data-stu-id="65a15-206">With the breakpoint still set, run the Course Index page.</span></span> <span data-ttu-id="65a15-207">在代码第一次命中断点时继续，以便在浏览器中显示该页。</span><span class="sxs-lookup"><span data-stu-id="65a15-207">Continue through the first times that the code hits a breakpoint, so that the page is displayed in the browser.</span></span> <span data-ttu-id="65a15-208">从下拉列表中选择一个部门，然后单击 "**筛选器**"。</span><span class="sxs-lookup"><span data-stu-id="65a15-208">Select a department from the drop-down list and click **Filter**.</span></span>

<span data-ttu-id="65a15-209">这次，第一个断点将用于下拉列表的部门查询。</span><span class="sxs-lookup"><span data-stu-id="65a15-209">This time the first breakpoint will be for the departments query for the drop-down list.</span></span> <span data-ttu-id="65a15-210">跳过该操作，并在 `query` 下一次代码到达断点时查看变量，以便查看 `Course` 查询现在的外观。</span><span class="sxs-lookup"><span data-stu-id="65a15-210">Skip that and view the `query` variable the next time the code reaches the breakpoint in order to see what the `Course` query now looks like.</span></span> <span data-ttu-id="65a15-211">你将看到如下所示的内容：</span><span class="sxs-lookup"><span data-stu-id="65a15-211">You'll see something like the following:</span></span>

[!code-sql[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample10.sql)]

<span data-ttu-id="65a15-212">您可以看到，该查询现在是一个 `JOIN` 查询，该查询将 `Department` 数据与 `Course` 数据一起加载，并且它包含一个 `WHERE` 子句。</span><span class="sxs-lookup"><span data-stu-id="65a15-212">You can see that the query is now a `JOIN` query that loads `Department` data along with the `Course` data, and that it includes a `WHERE` clause.</span></span>

<span data-ttu-id="65a15-213">删除 `var sql = courses.ToString()` 行。</span><span class="sxs-lookup"><span data-stu-id="65a15-213">Remove the `var sql = courses.ToString()` line.</span></span>

## <a name="create-an-abstraction-layer"></a><span data-ttu-id="65a15-214">创建抽象层</span><span class="sxs-lookup"><span data-stu-id="65a15-214">Create an abstraction layer</span></span>

<span data-ttu-id="65a15-215">许多开发人员编写代码实现存储库和工作模式单元以作为使用 Entity Framework 代码的包装器。</span><span class="sxs-lookup"><span data-stu-id="65a15-215">Many developers write code to implement the repository and unit of work patterns as a wrapper around code that works with the Entity Framework.</span></span> <span data-ttu-id="65a15-216">这些模式用于在应用程序的数据访问层和业务逻辑层之间创建抽象层。</span><span class="sxs-lookup"><span data-stu-id="65a15-216">These patterns are intended to create an abstraction layer between the data access layer and the business logic layer of an application.</span></span> <span data-ttu-id="65a15-217">实现这些模式可让你的应用程序对数据存储介质的更改不敏感，而且很容易进行自动化单元测试和进行测试驱动开发 (TDD)。</span><span class="sxs-lookup"><span data-stu-id="65a15-217">Implementing these patterns can help insulate your application from changes in the data store and can facilitate automated unit testing or test-driven development (TDD).</span></span> <span data-ttu-id="65a15-218">不过，出于以下几个原因，编写附加代码来实现这些模式并非总是最佳选择：</span><span class="sxs-lookup"><span data-stu-id="65a15-218">However, writing additional code to implement these patterns is not always the best choice for applications that use EF, for several reasons:</span></span>

- <span data-ttu-id="65a15-219">EF 上下文类可以为使用 EF 的数据库更新充当工作单位类。</span><span class="sxs-lookup"><span data-stu-id="65a15-219">The EF context class itself insulates your code from data-store-specific code.</span></span>
- <span data-ttu-id="65a15-220">对于使用 EF 进行的数据库更新，EF 上下文类可充当工作单元类。</span><span class="sxs-lookup"><span data-stu-id="65a15-220">The EF context class can act as a unit-of-work class for database updates that you do using EF.</span></span>
- <span data-ttu-id="65a15-221">实体框架6中引入的功能使得无需编写存储库代码即可更轻松地实现 TDD。</span><span class="sxs-lookup"><span data-stu-id="65a15-221">Features introduced in Entity Framework 6 make it easier to implement TDD without writing repository code.</span></span>

<span data-ttu-id="65a15-222">有关如何实现存储库和工作单元模式的详细信息，请参阅[本系列教程的实体框架5版本](../../older-versions/getting-started-with-ef-5-using-mvc-4/implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md)。</span><span class="sxs-lookup"><span data-stu-id="65a15-222">For more information about how to implement the repository and unit of work patterns, see [the Entity Framework 5 version of this tutorial series](../../older-versions/getting-started-with-ef-5-using-mvc-4/implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md).</span></span> <span data-ttu-id="65a15-223">有关在实体框架6中实现 TDD 的方式的信息，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="65a15-223">For information about ways to implement TDD in Entity Framework 6, see the following resources:</span></span>

- [<span data-ttu-id="65a15-224">EF6 如何更轻松地启用模拟 Dbset</span><span class="sxs-lookup"><span data-stu-id="65a15-224">How EF6 Enables Mocking DbSets more easily</span></span>](http://thedatafarm.com/data-access/how-ef6-enables-mocking-dbsets-more-easily/)
- [<span data-ttu-id="65a15-225">使用模拟框架进行测试</span><span class="sxs-lookup"><span data-stu-id="65a15-225">Testing with a mocking framework</span></span>](https://msdn.microsoft.com/data/dn314429)
- [<span data-ttu-id="65a15-226">用自己的测试进行测试双精度</span><span class="sxs-lookup"><span data-stu-id="65a15-226">Testing with your own test doubles</span></span>](https://msdn.microsoft.com/data/dn314431)

<a id="proxies"></a>

## <a name="proxy-classes"></a><span data-ttu-id="65a15-227">代理类</span><span class="sxs-lookup"><span data-stu-id="65a15-227">Proxy classes</span></span>

<span data-ttu-id="65a15-228">如果实体框架创建实体实例 (例如，在执行查询) 时，它通常会将其创建为作为实体代理的动态生成的派生类型的实例。</span><span class="sxs-lookup"><span data-stu-id="65a15-228">When the Entity Framework creates entity instances (for example, when you execute a query), it often creates them as instances of a dynamically generated derived type that acts as a proxy for the entity.</span></span> <span data-ttu-id="65a15-229">例如，请参阅以下两个调试器映像。</span><span class="sxs-lookup"><span data-stu-id="65a15-229">For example, see the following two debugger images.</span></span> <span data-ttu-id="65a15-230">在第一个图像中，你会看到在 `student` `Student` 实例化实体后，变量是预期类型。</span><span class="sxs-lookup"><span data-stu-id="65a15-230">In the first image, you see that the `student` variable is the expected `Student` type immediately after you instantiate the entity.</span></span> <span data-ttu-id="65a15-231">在第二个图中，使用 EF 从数据库中读取 student 实体后，会看到代理类。</span><span class="sxs-lookup"><span data-stu-id="65a15-231">In the second image, after EF has been used to read a student entity from the database, you see the proxy class.</span></span>

![代理类之前](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image12.png)

![代理类之后](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image13.png)

<span data-ttu-id="65a15-234">此代理类将重写实体的某些虚拟属性，以插入挂钩，以便在访问属性时自动执行操作。</span><span class="sxs-lookup"><span data-stu-id="65a15-234">This proxy class overrides some virtual properties of the entity to insert hooks for performing actions automatically when the property is accessed.</span></span> <span data-ttu-id="65a15-235">此机制用于的一个函数是延迟加载。</span><span class="sxs-lookup"><span data-stu-id="65a15-235">One function this mechanism is used for is lazy loading.</span></span>

<span data-ttu-id="65a15-236">大多数情况下，无需注意代理的这种使用，但有一些例外：</span><span class="sxs-lookup"><span data-stu-id="65a15-236">Most of the time you don't need to be aware of this use of proxies, but there are exceptions:</span></span>

- <span data-ttu-id="65a15-237">在某些情况下，你可能想要阻止实体框架创建代理实例。</span><span class="sxs-lookup"><span data-stu-id="65a15-237">In some scenarios you might want to prevent the Entity Framework from creating proxy instances.</span></span> <span data-ttu-id="65a15-238">例如，在序列化实体时，通常需要 POCO 类，而不是代理类。</span><span class="sxs-lookup"><span data-stu-id="65a15-238">For example, when you're serializing entities you generally want the POCO classes, not the proxy classes.</span></span> <span data-ttu-id="65a15-239">避免序列化问题的一种方法是将数据传输对象序列化 (Dto) 而不是实体对象，如[使用带有实体框架的 WEB API](../../../../web-api/overview/data/using-web-api-with-entity-framework/part-1.md)教程中所示。</span><span class="sxs-lookup"><span data-stu-id="65a15-239">One way to avoid serialization problems is to serialize data transfer objects (DTOs) instead of entity objects, as shown in the [Using Web API with Entity Framework](../../../../web-api/overview/data/using-web-api-with-entity-framework/part-1.md) tutorial.</span></span> <span data-ttu-id="65a15-240">另一种方法是[禁用代理创建](https://msdn.microsoft.com/data/jj592886.aspx)。</span><span class="sxs-lookup"><span data-stu-id="65a15-240">Another way is to [disable proxy creation](https://msdn.microsoft.com/data/jj592886.aspx).</span></span>
- <span data-ttu-id="65a15-241">如果使用运算符实例化实体类 `new` ，则不会获得代理实例。</span><span class="sxs-lookup"><span data-stu-id="65a15-241">When you instantiate an entity class using the `new` operator, you don't get a proxy instance.</span></span> <span data-ttu-id="65a15-242">这意味着不会获得延迟加载和自动更改跟踪等功能。</span><span class="sxs-lookup"><span data-stu-id="65a15-242">This means you don't get functionality such as lazy loading and automatic change tracking.</span></span> <span data-ttu-id="65a15-243">这通常是正常的;通常不需要延迟加载，因为你要创建的是不在数据库中的新实体，并且如果你将实体显式标记为，则通常不需要更改跟踪 `Added` 。</span><span class="sxs-lookup"><span data-stu-id="65a15-243">This is typically okay; you generally don't need lazy loading, because you're creating a new entity that isn't in the database, and you generally don't need change tracking if you're explicitly marking the entity as `Added`.</span></span> <span data-ttu-id="65a15-244">但是，如果确实需要延迟加载并且需要更改跟踪，则可以使用类的[create](https://msdn.microsoft.com/library/gg679504.aspx)方法创建新的实体实例，其中包含代理 `DbSet` 。</span><span class="sxs-lookup"><span data-stu-id="65a15-244">However, if you do need lazy loading and you need change tracking, you can create new entity instances with proxies using the [Create](https://msdn.microsoft.com/library/gg679504.aspx) method of the `DbSet` class.</span></span>
- <span data-ttu-id="65a15-245">你可能需要从代理类型获取实际的实体类型。</span><span class="sxs-lookup"><span data-stu-id="65a15-245">You might want to get an actual entity type from a proxy type.</span></span> <span data-ttu-id="65a15-246">您可以使用类的[GetObjectType](https://msdn.microsoft.com/library/system.data.objects.objectcontext.getobjecttype.aspx)方法 `ObjectContext` 来获取代理类型实例的实际实体类型。</span><span class="sxs-lookup"><span data-stu-id="65a15-246">You can use the [GetObjectType](https://msdn.microsoft.com/library/system.data.objects.objectcontext.getobjecttype.aspx) method of the `ObjectContext` class to get the actual entity type of a proxy type instance.</span></span>

<span data-ttu-id="65a15-247">有关详细信息，请参阅 MSDN 上[的使用代理](https://msdn.microsoft.com/data/JJ592886.aspx)。</span><span class="sxs-lookup"><span data-stu-id="65a15-247">For more information, see [Working with Proxies](https://msdn.microsoft.com/data/JJ592886.aspx) on MSDN.</span></span>

## <a name="automatic-change-detection"></a><span data-ttu-id="65a15-248">自动脏值检测</span><span class="sxs-lookup"><span data-stu-id="65a15-248">Automatic change detection</span></span>

<span data-ttu-id="65a15-249">Entity Framework 通过比较的实体的当前值与原始值来判断更改实体的方式 （因此需要发送更新到数据库）。</span><span class="sxs-lookup"><span data-stu-id="65a15-249">The Entity Framework determines how an entity has changed (and therefore which updates need to be sent to the database) by comparing the current values of an entity with the original values.</span></span> <span data-ttu-id="65a15-250">查询或附加该实体时会存储的原始值。</span><span class="sxs-lookup"><span data-stu-id="65a15-250">The original values are stored when the entity is queried or attached.</span></span> <span data-ttu-id="65a15-251">如下方法会导致自动脏值：</span><span class="sxs-lookup"><span data-stu-id="65a15-251">Some of the methods that cause automatic change detection are the following:</span></span>

- `DbSet.Find`
- `DbSet.Local`
- `DbSet.Remove`
- `DbSet.Add`
- `DbSet.Attach`
- `DbContext.SaveChanges`
- `DbContext.GetValidationErrors`
- `DbContext.Entry`
- `DbChangeTracker.Entries`

<span data-ttu-id="65a15-252">如果正在跟踪大量实体，并且在循环中多次调用这些方法之一，则使用[AutoDetectChangesEnabled](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.autodetectchangesenabled.aspx)属性暂时关闭自动更改检测可能会显著提高性能。</span><span class="sxs-lookup"><span data-stu-id="65a15-252">If you're tracking a large number of entities and you call one of these methods many times in a loop, you might get significant performance improvements by temporarily turning off automatic change detection using the [AutoDetectChangesEnabled](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.autodetectchangesenabled.aspx) property.</span></span> <span data-ttu-id="65a15-253">有关详细信息，请参阅 MSDN 上的[自动检测更改](https://msdn.microsoft.com/data/jj556205)。</span><span class="sxs-lookup"><span data-stu-id="65a15-253">For more information, see [Automatically Detecting Changes](https://msdn.microsoft.com/data/jj556205) on MSDN.</span></span>

## <a name="automatic-validation"></a><span data-ttu-id="65a15-254">自动验证</span><span class="sxs-lookup"><span data-stu-id="65a15-254">Automatic validation</span></span>

<span data-ttu-id="65a15-255">在调用方法时 `SaveChanges` ，默认情况下，实体框架在更新数据库之前验证所有已更改实体的所有属性中的数据。</span><span class="sxs-lookup"><span data-stu-id="65a15-255">When you call the `SaveChanges` method, by default the Entity Framework validates the data in all properties of all changed entities before updating the database.</span></span> <span data-ttu-id="65a15-256">如果已更新大量实体，并且已验证数据，则不需要执行此操作，并且可以通过暂时关闭验证来使保存更改的过程更少。</span><span class="sxs-lookup"><span data-stu-id="65a15-256">If you've updated a large number of entities and you've already validated the data, this work is unnecessary and you could make the process of saving the changes take less time by temporarily turning off validation.</span></span> <span data-ttu-id="65a15-257">可以使用[ValidateOnSaveEnabled](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.validateonsaveenabled.aspx)属性执行此操作。</span><span class="sxs-lookup"><span data-stu-id="65a15-257">You can do that using the [ValidateOnSaveEnabled](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.validateonsaveenabled.aspx) property.</span></span> <span data-ttu-id="65a15-258">有关详细信息，请参阅 MSDN 上的[验证](https://msdn.microsoft.com/data/gg193959)。</span><span class="sxs-lookup"><span data-stu-id="65a15-258">For more information, see [Validation](https://msdn.microsoft.com/data/gg193959) on MSDN.</span></span>

## <a name="entity-framework-power-tools"></a><span data-ttu-id="65a15-259">实体框架 Power Tools</span><span class="sxs-lookup"><span data-stu-id="65a15-259">Entity Framework Power Tools</span></span>

<span data-ttu-id="65a15-260">[实体框架 Power Tools](https://marketplace.visualstudio.com/items?itemName=ErikEJ.EntityFramework6PowerToolsCommunityEdition)是一个 Visual Studio 外接程序，用于创建这些教程中所示的数据模型图。</span><span class="sxs-lookup"><span data-stu-id="65a15-260">[Entity Framework Power Tools](https://marketplace.visualstudio.com/items?itemName=ErikEJ.EntityFramework6PowerToolsCommunityEdition) is a Visual Studio add-in that was used to create the data model diagrams shown in these tutorials.</span></span> <span data-ttu-id="65a15-261">这些工具还可以执行其他功能，例如基于现有数据库中的表生成实体类，以便可以将数据库与 Code First 一起使用。</span><span class="sxs-lookup"><span data-stu-id="65a15-261">The tools can also do other function such as generate entity classes based on the tables in an existing database so that you can use the database with Code First.</span></span> <span data-ttu-id="65a15-262">安装这些工具后，上下文菜单中将显示一些附加选项。</span><span class="sxs-lookup"><span data-stu-id="65a15-262">After you install the tools, some additional options appear in context menus.</span></span> <span data-ttu-id="65a15-263">例如，在**解决方案资源管理器**中右键单击上下文类时，将看到和**实体框架**选项。</span><span class="sxs-lookup"><span data-stu-id="65a15-263">For example, when you right-click your context class in **Solution Explorer**, you see and **Entity Framework** option.</span></span> <span data-ttu-id="65a15-264">这使您能够生成关系图。</span><span class="sxs-lookup"><span data-stu-id="65a15-264">This gives you the ability to generate a diagram.</span></span> <span data-ttu-id="65a15-265">使用时 Code First 无法更改关系图中的数据模型，但可以移动它们以使其更易于理解。</span><span class="sxs-lookup"><span data-stu-id="65a15-265">When you're using Code First you can't change the data model in the diagram, but you can move things around to make it easier to understand.</span></span>

![EF 关系图](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image15.png)

## <a name="entity-framework-source-code"></a><span data-ttu-id="65a15-267">实体框架源代码</span><span class="sxs-lookup"><span data-stu-id="65a15-267">Entity Framework source code</span></span>

<span data-ttu-id="65a15-268">[GitHub](https://github.com/aspnet/EntityFramework6)上提供了实体框架6的源代码。</span><span class="sxs-lookup"><span data-stu-id="65a15-268">The source code for Entity Framework 6 is available at [GitHub](https://github.com/aspnet/EntityFramework6).</span></span> <span data-ttu-id="65a15-269">您可以为 bug 提供文件，并且您可以向 EF 源代码提供您自己的增强功能。</span><span class="sxs-lookup"><span data-stu-id="65a15-269">You can file bugs, and you can contribute your own enhancements to the EF source code.</span></span>

<span data-ttu-id="65a15-270">尽管源代码已打开，但实体框架完全支持作为 Microsoft 产品。</span><span class="sxs-lookup"><span data-stu-id="65a15-270">Although the source code is open, Entity Framework is fully supported as a Microsoft product.</span></span> <span data-ttu-id="65a15-271">Microsoft Entity Framework 团队将控制接受哪些贡献和测试所有的代码更改，以确保每个版本的质量。</span><span class="sxs-lookup"><span data-stu-id="65a15-271">The Microsoft Entity Framework team keeps control over which contributions are accepted and tests all code changes to ensure the quality of each release.</span></span>

## <a name="acknowledgments"></a><span data-ttu-id="65a15-272">鸣谢</span><span class="sxs-lookup"><span data-stu-id="65a15-272">Acknowledgments</span></span>

- <span data-ttu-id="65a15-273">Tom Dykstra 编写了本教程的原始版本，共同创作了 EF 5 更新，并编写了 EF 6 更新。</span><span class="sxs-lookup"><span data-stu-id="65a15-273">Tom Dykstra wrote the original version of this tutorial, co-authored the EF 5 update, and wrote the EF 6 update.</span></span> <span data-ttu-id="65a15-274">Tom 是 Microsoft Web 平台和工具内容团队的高级编程编写器。</span><span class="sxs-lookup"><span data-stu-id="65a15-274">Tom is a senior programming writer on the Microsoft Web Platform and Tools Content Team.</span></span>
- <span data-ttu-id="65a15-275">[Rick Anderson](https://blogs.msdn.com/b/rickandy/) (twitter [@RickAndMSFT](http://twitter.com/RickAndMSFT)) 完成了对 EF 5 和 MVC 4 的教程的大部分工作，并共同创作了 ef 6 更新。</span><span class="sxs-lookup"><span data-stu-id="65a15-275">[Rick Anderson](https://blogs.msdn.com/b/rickandy/) (twitter [@RickAndMSFT](http://twitter.com/RickAndMSFT)) did most of the work updating the tutorial for EF 5 and MVC 4 and co-authored the EF 6 update.</span></span> <span data-ttu-id="65a15-276">Rick 是 Microsoft 的高级编程编写人员，侧重于 Azure 和 MVC。</span><span class="sxs-lookup"><span data-stu-id="65a15-276">Rick is a senior programming writer for Microsoft focusing on Azure and MVC.</span></span>
- <span data-ttu-id="65a15-277">[Rowan 莎莎](http://www.romiller.com)和实体框架团队的其他成员协助进行代码评审，并帮助调试在我们更新 EF 5 和 ef 6 教程时出现的许多迁移问题。</span><span class="sxs-lookup"><span data-stu-id="65a15-277">[Rowan Miller](http://www.romiller.com) and other members of the Entity Framework team assisted with code reviews and helped debug many issues with migrations that arose while we were updating the tutorial for EF 5 and EF 6.</span></span>

## <a name="troubleshoot-common-errors"></a><span data-ttu-id="65a15-278">常见错误疑难解答</span><span class="sxs-lookup"><span data-stu-id="65a15-278">Troubleshoot common errors</span></span>

### <a name="cannot-createshadow-copy"></a><span data-ttu-id="65a15-279">无法创建/隐藏副本</span><span class="sxs-lookup"><span data-stu-id="65a15-279">Cannot create/shadow copy</span></span>

<span data-ttu-id="65a15-280">错误消息：</span><span class="sxs-lookup"><span data-stu-id="65a15-280">Error Message:</span></span>

> <span data-ttu-id="65a15-281">&lt; &gt; 如果文件已存在，则无法创建/卷影复制 "filename"。</span><span class="sxs-lookup"><span data-stu-id="65a15-281">Cannot create/shadow copy '&lt;filename&gt;' when that file already exists.</span></span>

<span data-ttu-id="65a15-282">解决方案</span><span class="sxs-lookup"><span data-stu-id="65a15-282">Solution</span></span>

<span data-ttu-id="65a15-283">请等待几秒钟，然后刷新页面。</span><span class="sxs-lookup"><span data-stu-id="65a15-283">Wait a few seconds and refresh the page.</span></span>

### <a name="update-database-not-recognized"></a><span data-ttu-id="65a15-284">更新-无法识别数据库</span><span class="sxs-lookup"><span data-stu-id="65a15-284">Update-Database not recognized</span></span>

<span data-ttu-id="65a15-285">PMC) 中的命令 (的错误消息 `Update-Database` ：</span><span class="sxs-lookup"><span data-stu-id="65a15-285">Error Message (from the `Update-Database` command in the PMC):</span></span>

> <span data-ttu-id="65a15-286">术语 "更新-数据库" 未被识别为 cmdlet、函数、脚本文件或可运行程序的名称。</span><span class="sxs-lookup"><span data-stu-id="65a15-286">The term 'Update-Database' is not recognized as the name of a cmdlet, function, script file, or operable program.</span></span> <span data-ttu-id="65a15-287">请检查名称的拼写，如果包含路径，请验证该路径是否正确，并重试。</span><span class="sxs-lookup"><span data-stu-id="65a15-287">Check the spelling of the name, or if a path was included, verify that the path is correct and try again.</span></span>

<span data-ttu-id="65a15-288">解决方案</span><span class="sxs-lookup"><span data-stu-id="65a15-288">Solution</span></span>

<span data-ttu-id="65a15-289">退出 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="65a15-289">Exit Visual Studio.</span></span> <span data-ttu-id="65a15-290">重新打开项目，然后重试。</span><span class="sxs-lookup"><span data-stu-id="65a15-290">Reopen project and try again.</span></span>

### <a name="validation-failed"></a><span data-ttu-id="65a15-291">验证失败</span><span class="sxs-lookup"><span data-stu-id="65a15-291">Validation failed</span></span>

<span data-ttu-id="65a15-292">PMC) 中的命令 (的错误消息 `Update-Database` ：</span><span class="sxs-lookup"><span data-stu-id="65a15-292">Error Message (from the `Update-Database` command in the PMC):</span></span>

> <span data-ttu-id="65a15-293">对一个或多个实体的验证失败。</span><span class="sxs-lookup"><span data-stu-id="65a15-293">Validation failed for one or more entities.</span></span> <span data-ttu-id="65a15-294">有关更多详细信息，请参阅 "EntityValidationErrors" 属性。</span><span class="sxs-lookup"><span data-stu-id="65a15-294">See 'EntityValidationErrors' property for more details.</span></span>

<span data-ttu-id="65a15-295">解决方案</span><span class="sxs-lookup"><span data-stu-id="65a15-295">Solution</span></span>

<span data-ttu-id="65a15-296">此问题的一个原因是在方法运行时出现验证错误 `Seed` 。</span><span class="sxs-lookup"><span data-stu-id="65a15-296">One cause of this problem is validation errors when the `Seed` method runs.</span></span> <span data-ttu-id="65a15-297">有关调试方法的提示，请参阅[播种和调试实体框架 (EF) ](https://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx)数据库 `Seed` 。</span><span class="sxs-lookup"><span data-stu-id="65a15-297">See [Seeding and Debugging Entity Framework (EF) DBs](https://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx) for tips on debugging the `Seed` method.</span></span>

### <a name="http-50019-error"></a><span data-ttu-id="65a15-298">HTTP 500.19 错误</span><span class="sxs-lookup"><span data-stu-id="65a15-298">HTTP 500.19 error</span></span>

<span data-ttu-id="65a15-299">错误消息：</span><span class="sxs-lookup"><span data-stu-id="65a15-299">Error Message:</span></span>

> <span data-ttu-id="65a15-300">HTTP 错误 500.19-内部服务器错误无法访问请求的页面，因为该页的相关配置数据无效。</span><span class="sxs-lookup"><span data-stu-id="65a15-300">HTTP Error 500.19 - Internal Server Error The requested page cannot be accessed because the related configuration data for the page is invalid.</span></span>

<span data-ttu-id="65a15-301">解决方案</span><span class="sxs-lookup"><span data-stu-id="65a15-301">Solution</span></span>

<span data-ttu-id="65a15-302">获取此错误的一种方法是使用解决方案的多个副本，每个副本使用相同的端口号。</span><span class="sxs-lookup"><span data-stu-id="65a15-302">One way you can get this error is from having multiple copies of the solution, each of them using the same port number.</span></span> <span data-ttu-id="65a15-303">通常可以通过退出 Visual Studio 的所有实例，然后重新启动正在处理的项目，来解决此问题。</span><span class="sxs-lookup"><span data-stu-id="65a15-303">You can usually solve this problem by exiting all instances of Visual Studio, then restarting the project you're working on.</span></span> <span data-ttu-id="65a15-304">如果这不起作用，请尝试更改端口号。</span><span class="sxs-lookup"><span data-stu-id="65a15-304">If that doesn't work, try changing the port number.</span></span> <span data-ttu-id="65a15-305">右键单击项目文件，然后单击 "属性"。</span><span class="sxs-lookup"><span data-stu-id="65a15-305">Right click on the project file and then click properties.</span></span> <span data-ttu-id="65a15-306">选择 " **Web** " 选项卡，然后在 "**项目 Url** " 文本框中更改端口号。</span><span class="sxs-lookup"><span data-stu-id="65a15-306">Select the **Web** tab and then change the port number in the **Project Url** text box.</span></span>

### <a name="error-locating-sql-server-instance"></a><span data-ttu-id="65a15-307">定位 SQL Server 实例出错</span><span class="sxs-lookup"><span data-stu-id="65a15-307">Error locating SQL Server instance</span></span>

<span data-ttu-id="65a15-308">错误消息：</span><span class="sxs-lookup"><span data-stu-id="65a15-308">Error Message:</span></span>

> <span data-ttu-id="65a15-309">建立到 SQL Server 的连接时出现与网络相关或特定于实例的错误。</span><span class="sxs-lookup"><span data-stu-id="65a15-309">A network-related or instance-specific error occurred while establishing a connection to SQL Server.</span></span> <span data-ttu-id="65a15-310">找不到或无法访问服务器。</span><span class="sxs-lookup"><span data-stu-id="65a15-310">The server was not found or was not accessible.</span></span> <span data-ttu-id="65a15-311">请验证实例名称是否正确，SQL Server 是否已配置为允许远程连接。</span><span class="sxs-lookup"><span data-stu-id="65a15-311">Verify that the instance name is correct and that SQL Server is configured to allow remote connections.</span></span> <span data-ttu-id="65a15-312">（提供程序：SQL 网络接口，错误：26 - 定位指定服务器/实例出错）</span><span class="sxs-lookup"><span data-stu-id="65a15-312">(provider: SQL Network Interfaces, error: 26 - Error Locating Server/Instance Specified)</span></span>

<span data-ttu-id="65a15-313">解决方案</span><span class="sxs-lookup"><span data-stu-id="65a15-313">Solution</span></span>

<span data-ttu-id="65a15-314">请检查连接字符串。</span><span class="sxs-lookup"><span data-stu-id="65a15-314">Check the connection string.</span></span> <span data-ttu-id="65a15-315">如果手动删除了数据库，请在构造字符串中更改数据库的名称。</span><span class="sxs-lookup"><span data-stu-id="65a15-315">If you have manually deleted the database, change the name of the database in the construction string.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="65a15-316">获取代码</span><span class="sxs-lookup"><span data-stu-id="65a15-316">Get the code</span></span>

[<span data-ttu-id="65a15-317">下载完成的项目</span><span class="sxs-lookup"><span data-stu-id="65a15-317">Download Completed Project</span></span>](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a><span data-ttu-id="65a15-318">其他资源</span><span class="sxs-lookup"><span data-stu-id="65a15-318">Additional resources</span></span>

 <span data-ttu-id="65a15-319">有关如何使用实体框架处理数据的详细信息，请参阅[MSDN 上的 EF 文档页](https://msdn.microsoft.com/data/ee712907)和[ASP.NET 数据访问-建议的资源](../../../../whitepapers/aspnet-data-access-content-map.md)。</span><span class="sxs-lookup"><span data-stu-id="65a15-319">For more information about how to work with data using the Entity Framework, see the [EF documentation page on MSDN](https://msdn.microsoft.com/data/ee712907) and [ASP.NET Data Access - Recommended Resources](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

<span data-ttu-id="65a15-320">有关如何在生成 web 应用程序后对其进行部署的详细信息，请参阅 MSDN Library 中的[ASP.NET Web 部署-推荐资源](../../../../whitepapers/aspnet-web-deployment-content-map.md)。</span><span class="sxs-lookup"><span data-stu-id="65a15-320">For more information about how to deploy your web application after you've built it, see [ASP.NET Web Deployment - Recommended Resources](../../../../whitepapers/aspnet-web-deployment-content-map.md) in the MSDN Library.</span></span>

<span data-ttu-id="65a15-321">有关与 MVC 相关的其他主题（例如身份验证和授权）的信息，请参阅[ASP.NET MVC-推荐的资源](../recommended-resources-for-mvc.md)。</span><span class="sxs-lookup"><span data-stu-id="65a15-321">For information about other topics related to MVC, such as authentication and authorization, see the [ASP.NET MVC - Recommended Resources](../recommended-resources-for-mvc.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="65a15-322">后续步骤</span><span class="sxs-lookup"><span data-stu-id="65a15-322">Next steps</span></span>

<span data-ttu-id="65a15-323">在本教程中，你将了解：</span><span class="sxs-lookup"><span data-stu-id="65a15-323">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="65a15-324">已执行原始 SQL 查询</span><span class="sxs-lookup"><span data-stu-id="65a15-324">Performed raw SQL queries</span></span>
> * <span data-ttu-id="65a15-325">执行无跟踪查询</span><span class="sxs-lookup"><span data-stu-id="65a15-325">Performed no-tracking queries</span></span>
> * <span data-ttu-id="65a15-326">已检查发送到数据库的 SQL 查询</span><span class="sxs-lookup"><span data-stu-id="65a15-326">Examined SQL queries sent to the database</span></span>

<span data-ttu-id="65a15-327">还了解了：</span><span class="sxs-lookup"><span data-stu-id="65a15-327">You also learned about:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="65a15-328">创建抽象层</span><span class="sxs-lookup"><span data-stu-id="65a15-328">Creating an abstraction layer</span></span>
> * <span data-ttu-id="65a15-329">代理类</span><span class="sxs-lookup"><span data-stu-id="65a15-329">Proxy classes</span></span>
> * <span data-ttu-id="65a15-330">自动脏值检测</span><span class="sxs-lookup"><span data-stu-id="65a15-330">Automatic change detection</span></span>
> * <span data-ttu-id="65a15-331">自动验证</span><span class="sxs-lookup"><span data-stu-id="65a15-331">Automatic validation</span></span>
> * <span data-ttu-id="65a15-332">实体框架 Power Tools</span><span class="sxs-lookup"><span data-stu-id="65a15-332">Entity Framework Power Tools</span></span>
> * <span data-ttu-id="65a15-333">实体框架源代码</span><span class="sxs-lookup"><span data-stu-id="65a15-333">Entity Framework source code</span></span>

<span data-ttu-id="65a15-334">这将完成本系列教程，介绍如何在 ASP.NET MVC 应用程序中使用实体框架。</span><span class="sxs-lookup"><span data-stu-id="65a15-334">This completes this series of tutorials on using the Entity Framework in an ASP.NET MVC application.</span></span> <span data-ttu-id="65a15-335">如果要了解有关 EF Database First 的信息，请参阅 DB 第一系列教程。</span><span class="sxs-lookup"><span data-stu-id="65a15-335">If you want to learn about EF Database First, see the DB First tutorial series.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="65a15-336">实体框架 Database First</span><span class="sxs-lookup"><span data-stu-id="65a15-336">Entity Framework Database First</span></span>](../database-first-development/setting-up-database.md)
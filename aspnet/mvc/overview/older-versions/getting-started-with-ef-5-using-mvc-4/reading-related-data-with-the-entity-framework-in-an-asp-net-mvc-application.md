---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
title: 使用 ASP.NET MVC 应用程序中的实体框架读取相关数据 (5/10) |Microsoft Docs
author: tdykstra
description: Contoso 大学示例 web 应用程序演示如何使用实体框架 5 Code First 和 Visual Studio .。。
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 0d6fb83b-71f7-425d-8dec-981197d7ec42
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 6a3a4978a718ba56446463373ad3525e8b6f0d4a
ms.sourcegitcommit: b4cdcf246850751579e45da80c9780fe56330dd0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2021
ms.locfileid: "99984838"
---
# <a name="reading-related-data-with-the-entity-framework-in-an-aspnet-mvc-application-5-of-10"></a><span data-ttu-id="12490-103">使用 ASP.NET MVC 应用程序中的实体框架读取相关数据 (第5个，共10个) </span><span class="sxs-lookup"><span data-stu-id="12490-103">Reading Related Data with the Entity Framework in an ASP.NET MVC Application (5 of 10)</span></span>

<span data-ttu-id="12490-104">作者： [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="12490-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

> <span data-ttu-id="12490-105">Contoso 大学示例 web 应用程序演示了如何使用实体框架 5 Code First 和 Visual Studio 2012 创建 ASP.NET MVC 4 应用程序。</span><span class="sxs-lookup"><span data-stu-id="12490-105">The Contoso University sample web application demonstrates how to create ASP.NET MVC 4 applications using the Entity Framework 5 Code First and Visual Studio 2012.</span></span> <span data-ttu-id="12490-106">若要了解教程系列，请参阅[本系列中的第一个教程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。</span><span class="sxs-lookup"><span data-stu-id="12490-106">For information about the tutorial series, see [the first tutorial in the series](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>
> 
> > [!NOTE] 
> > 
> > <span data-ttu-id="12490-107">如果遇到无法解决的问题，请 [下载已完成的章节](building-the-ef5-mvc4-chapter-downloads.md) 并尝试重现你的问题。</span><span class="sxs-lookup"><span data-stu-id="12490-107">If you run into a problem you can't resolve, [download the completed chapter](building-the-ef5-mvc4-chapter-downloads.md) and try to reproduce your problem.</span></span> <span data-ttu-id="12490-108">通常可以通过将代码与已完成的代码进行比较，查找问题的解决方案。</span><span class="sxs-lookup"><span data-stu-id="12490-108">You can generally find the solution to the problem by comparing your code to the completed code.</span></span> <span data-ttu-id="12490-109">有关一些常见错误以及如何解决这些错误，请参阅 [错误和解决方法。](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)</span><span class="sxs-lookup"><span data-stu-id="12490-109">For some common errors and how to solve them, see [Errors and Workarounds.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)</span></span>

<span data-ttu-id="12490-110">在上一教程中，你已完成 School 数据模型。</span><span class="sxs-lookup"><span data-stu-id="12490-110">In the previous tutorial you completed the School data model.</span></span> <span data-ttu-id="12490-111">在本教程中，您将读取并显示相关数据，即实体框架加载到导航属性中的数据。</span><span class="sxs-lookup"><span data-stu-id="12490-111">In this tutorial you'll read and display related data — that is, data that the Entity Framework loads into navigation properties.</span></span>

<span data-ttu-id="12490-112">下图是将会用到的页面。</span><span class="sxs-lookup"><span data-stu-id="12490-112">The following illustrations show the pages that you'll work with.</span></span>

![](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![Instructors_index_page_with_instructor_and_course_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

## <a name="lazy-eager-and-explicit-loading-of-related-data"></a><span data-ttu-id="12490-114">延迟、预先和显式加载相关数据</span><span class="sxs-lookup"><span data-stu-id="12490-114">Lazy, Eager, and Explicit Loading of Related Data</span></span>

<span data-ttu-id="12490-115">实体框架可以通过多种方式将相关数据加载到实体的导航属性中：</span><span class="sxs-lookup"><span data-stu-id="12490-115">There are several ways that the Entity Framework can load related data into the navigation properties of an entity:</span></span>

- <span data-ttu-id="12490-116">*延迟加载*。</span><span class="sxs-lookup"><span data-stu-id="12490-116">*Lazy loading*.</span></span> <span data-ttu-id="12490-117">首次读取实体时，不检索相关数据。</span><span class="sxs-lookup"><span data-stu-id="12490-117">When the entity is first read, related data isn't retrieved.</span></span> <span data-ttu-id="12490-118">然而，首次尝试访问导航属性时，会自动检索导航属性所需的数据。</span><span class="sxs-lookup"><span data-stu-id="12490-118">However, the first time you attempt to access a navigation property, the data required for that navigation property is automatically retrieved.</span></span> <span data-ttu-id="12490-119">这会导致向数据库发送多个查询，一个用于实体本身，每次必须检索到该实体的相关数据。</span><span class="sxs-lookup"><span data-stu-id="12490-119">This results in multiple queries sent to the database — one for the entity itself and one each time that related data for the entity must be retrieved.</span></span> 

    ![Lazy_loading_example](https://asp.net/media/2577850/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Lazy_loading_example_2c44eabb-5fd3-485a-837d-8e3d053f2c0c.png)
- <span data-ttu-id="12490-121">*预先加载*。</span><span class="sxs-lookup"><span data-stu-id="12490-121">*Eager loading*.</span></span> <span data-ttu-id="12490-122">读取该实体时，会同时检索相关数据。</span><span class="sxs-lookup"><span data-stu-id="12490-122">When the entity is read, related data is retrieved along with it.</span></span> <span data-ttu-id="12490-123">此时通常会出现单一联接查询，检索所有必需数据。</span><span class="sxs-lookup"><span data-stu-id="12490-123">This typically results in a single join query that retrieves all of the data that's needed.</span></span> <span data-ttu-id="12490-124">使用方法指定预先加载 `Include` 。</span><span class="sxs-lookup"><span data-stu-id="12490-124">You specify eager loading by using the `Include` method.</span></span>

    ![Eager_loading_example](https://asp.net/media/2577856/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Eager_loading_example_33f907ff-f0b0-4057-8e75-05a8cacac807.png)
- <span data-ttu-id="12490-126">*显式加载*。</span><span class="sxs-lookup"><span data-stu-id="12490-126">*Explicit loading*.</span></span> <span data-ttu-id="12490-127">这类似于延迟加载，只不过是在代码中显式检索相关数据;在访问导航属性时，不会自动发生此情况。</span><span class="sxs-lookup"><span data-stu-id="12490-127">This is similar to lazy loading, except that you explicitly retrieve the related data in code; it doesn't happen automatically when you access a navigation property.</span></span> <span data-ttu-id="12490-128">您可以通过获取实体的对象状态管理器项并为 `Collection.Load` 包含单个实体的属性调用集合或方法，手动加载相关数据 `Reference.Load` 。</span><span class="sxs-lookup"><span data-stu-id="12490-128">You load related data manually by getting the object state manager entry for an entity and calling the `Collection.Load` method for collections or the `Reference.Load` method for properties that hold a single entity.</span></span> <span data-ttu-id="12490-129"> (在以下示例中，如果要加载 "管理员" 导航属性，则应将替换 `Collection(x => x.Courses)` 为 `Reference(x => x.Administrator)` 。 ) </span><span class="sxs-lookup"><span data-stu-id="12490-129">(In the following example, if you wanted to load the Administrator navigation property, you'd replace `Collection(x => x.Courses)` with `Reference(x => x.Administrator)`.)</span></span>

    ![Explicit_loading_example](https://asp.net/media/2577862/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Explicit_loading_example_79d8c368-6d82-426f-be9a-2b443644ab15.png)

<span data-ttu-id="12490-131">因为它们不会立即检索属性值，所以延迟加载和显式加载也称为 *延迟加载*。</span><span class="sxs-lookup"><span data-stu-id="12490-131">Because they don't immediately retrieve the property values, lazy loading and explicit loading are also both known as *deferred loading*.</span></span>

<span data-ttu-id="12490-132">通常，如果您知道每个检索到的实体都需要相关数据，预先加载可提供最佳性能，因为发送到数据库的单个查询通常比检索的每个实体的单独查询更有效。</span><span class="sxs-lookup"><span data-stu-id="12490-132">In general, if you know you need related data for every entity retrieved, eager loading offers the best performance, because a single query sent to the database is typically more efficient than separate queries for each entity retrieved.</span></span> <span data-ttu-id="12490-133">例如，在上面的示例中，假设每个部门都有十个相关的课程。</span><span class="sxs-lookup"><span data-stu-id="12490-133">For example, in the above examples, suppose that each department has ten related courses.</span></span> <span data-ttu-id="12490-134">预先加载的示例只会导致单个 (联接) 查询，并单次往返到数据库。</span><span class="sxs-lookup"><span data-stu-id="12490-134">The eager loading example would result in just a single (join) query and a single round trip to the database.</span></span> <span data-ttu-id="12490-135">延迟加载和显式加载示例会导致对数据库进行11次查询和十一次往返。</span><span class="sxs-lookup"><span data-stu-id="12490-135">The lazy loading and explicit loading examples would both result in eleven queries and eleven round trips to the database.</span></span> <span data-ttu-id="12490-136">延迟较高时，额外往返数据库对性能尤为不利。</span><span class="sxs-lookup"><span data-stu-id="12490-136">The extra round trips to the database are especially detrimental to performance when latency is high.</span></span>

<span data-ttu-id="12490-137">另一方面，在某些情况下，延迟加载更为有效。</span><span class="sxs-lookup"><span data-stu-id="12490-137">On the other hand, in some scenarios lazy loading is more efficient.</span></span> <span data-ttu-id="12490-138">预先加载可能会导致生成非常复杂的联接，这 SQL Server 无法有效地处理。</span><span class="sxs-lookup"><span data-stu-id="12490-138">Eager loading might cause a very complex join to be generated, which SQL Server can't process efficiently.</span></span> <span data-ttu-id="12490-139">或者，如果需要只为正在处理的一组实体的子集访问实体的导航属性，则延迟加载可能会更好，因为预先加载将检索比你需要的更多的数据。</span><span class="sxs-lookup"><span data-stu-id="12490-139">Or if you need to access an entity's navigation properties only for a subset of a set of entities you're processing, lazy loading might perform better because eager loading would retrieve more data than you need.</span></span> <span data-ttu-id="12490-140">如果看重性能，那么最好测试两种方式的性能，以便做出最佳选择。</span><span class="sxs-lookup"><span data-stu-id="12490-140">If performance is critical, it's best to test performance both ways in order to make the best choice.</span></span>

<span data-ttu-id="12490-141">通常，仅当关闭延迟加载时才使用显式加载。</span><span class="sxs-lookup"><span data-stu-id="12490-141">Typically you'd use explicit loading only when you've turned lazy loading off.</span></span> <span data-ttu-id="12490-142">一种情况是，在序列化过程中应关闭延迟加载。</span><span class="sxs-lookup"><span data-stu-id="12490-142">One scenario when you should turn lazy loading off is during serialization.</span></span> <span data-ttu-id="12490-143">延迟加载和序列化不是很好，如果您不小心，在启用延迟加载的情况下，查询的数据可能比预期要大得多。</span><span class="sxs-lookup"><span data-stu-id="12490-143">Lazy loading and serialization don't mix well, and if you aren't careful you can end up querying significantly more data than you intended when lazy loading is enabled.</span></span> <span data-ttu-id="12490-144">序列化通常通过访问类型实例上的每个属性来工作。</span><span class="sxs-lookup"><span data-stu-id="12490-144">Serialization generally works by accessing each property on an instance of a type.</span></span> <span data-ttu-id="12490-145">属性访问会触发延迟加载，并且会序列化这些延迟加载的实体。</span><span class="sxs-lookup"><span data-stu-id="12490-145">Property access triggers lazy loading, and those lazy loaded entities are serialized.</span></span> <span data-ttu-id="12490-146">然后，序列化过程访问延迟加载的实体的每个属性，这可能会导致更多的延迟加载和序列化。</span><span class="sxs-lookup"><span data-stu-id="12490-146">The serialization process then accesses each property of the lazy-loaded entities, potentially causing even more lazy loading and serialization.</span></span> <span data-ttu-id="12490-147">若要防止此运行时链反应，请在序列化实体之前关闭延迟加载。</span><span class="sxs-lookup"><span data-stu-id="12490-147">To prevent this run-away chain reaction, turn lazy loading off before you serialize an entity.</span></span>

<span data-ttu-id="12490-148">默认情况下，数据库上下文类执行延迟加载。</span><span class="sxs-lookup"><span data-stu-id="12490-148">The database context class performs lazy loading by default.</span></span> <span data-ttu-id="12490-149">可以通过两种方式来禁用延迟加载：</span><span class="sxs-lookup"><span data-stu-id="12490-149">There are two ways to disable lazy loading:</span></span>

- <span data-ttu-id="12490-150">对于特定的导航属性，请 `virtual` 在声明属性时省略关键字。</span><span class="sxs-lookup"><span data-stu-id="12490-150">For specific navigation properties, omit the `virtual` keyword when you declare the property.</span></span>
- <span data-ttu-id="12490-151">对于所有导航属性，将设置 `LazyLoadingEnabled` 为 `false` 。</span><span class="sxs-lookup"><span data-stu-id="12490-151">For all navigation properties, set `LazyLoadingEnabled` to `false`.</span></span> <span data-ttu-id="12490-152">例如，你可以将以下代码放在上下文类的构造函数中：</span><span class="sxs-lookup"><span data-stu-id="12490-152">For example, you can put the following code in the constructor of your context class:</span></span> 

    [!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

<span data-ttu-id="12490-153">延迟加载可以屏蔽导致性能问题的代码。</span><span class="sxs-lookup"><span data-stu-id="12490-153">Lazy loading can mask code that causes performance problems.</span></span> <span data-ttu-id="12490-154">例如，如果代码不指定预先加载或显式加载，但处理大量实体，并且在每次迭代中使用多个导航属性，则可能会非常低效 (，因为对数据库) 的多次往返。</span><span class="sxs-lookup"><span data-stu-id="12490-154">For example, code that doesn't specify eager or explicit loading but processes a high volume of entities and uses several navigation properties in each iteration might be very inefficient (because of many round trips to the database).</span></span> <span data-ttu-id="12490-155">使用本地 SQL server 进行开发良好的应用程序在迁移到 Azure SQL 数据库时可能会遇到性能问题，因为这会增加延迟和延迟加载。</span><span class="sxs-lookup"><span data-stu-id="12490-155">An application that performs well in development using an on premise SQL server might have performance problems when moved to Azure SQL Database due to the increased latency and lazy loading.</span></span> <span data-ttu-id="12490-156">使用真实的测试负载分析数据库查询将有助于确定是否适合延迟加载。</span><span class="sxs-lookup"><span data-stu-id="12490-156">Profiling the database queries with a realistic test load will help you determine if lazy loading is appropriate.</span></span> <span data-ttu-id="12490-157">有关详细信息，请参阅 [揭密实体框架策略：加载相关数据](https://msdn.microsoft.com/magazine/hh205756.aspx) 和 [使用实体框架将网络延迟减少到 SQL Azure](https://msdn.microsoft.com/magazine/gg309181.aspx)。</span><span class="sxs-lookup"><span data-stu-id="12490-157">For more information see [Demystifying Entity Framework Strategies: Loading Related Data](https://msdn.microsoft.com/magazine/hh205756.aspx) and [Using the Entity Framework to Reduce Network Latency to SQL Azure](https://msdn.microsoft.com/magazine/gg309181.aspx).</span></span>

## <a name="create-a-courses-index-page-that-displays-department-name"></a><span data-ttu-id="12490-158">创建显示部门名称的课程索引页</span><span class="sxs-lookup"><span data-stu-id="12490-158">Create a Courses Index Page That Displays Department Name</span></span>

<span data-ttu-id="12490-159">`Course`实体包括一个导航属性，该属性包含将 `Department` 课程分配到的部门的实体。</span><span class="sxs-lookup"><span data-stu-id="12490-159">The `Course` entity includes a navigation property that contains the `Department` entity of the department that the course is assigned to.</span></span> <span data-ttu-id="12490-160">若要在课程列表中显示分配的部门的名称，需要 `Name` 从 `Department` 导航属性中的实体获取属性 `Course.Department` 。</span><span class="sxs-lookup"><span data-stu-id="12490-160">To display the name of the assigned department in a list of courses, you need to get the `Name` property from the `Department` entity that is in the `Course.Department` navigation property.</span></span>

<span data-ttu-id="12490-161">`CourseController` `Course` 使用之前对控制器执行的相同选项，为实体类型创建一个名为的控制器 `Student` ，如下图所示 (除了映像以外，上下文类位于 DAL 命名空间中，而不是模型命名空间) ：</span><span class="sxs-lookup"><span data-stu-id="12490-161">Create a controller named `CourseController` for the `Course` entity type, using the same options that you did earlier for the `Student` controller, as shown in the following illustration (except unlike the image, your context class is in the DAL namespace, not the Models namespace):</span></span>

![Add_Controller_dialog_box_for_Course_controller](https://asp.net/media/2577868/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Add_Controller_dialog_box_for_Course_controller_c167c11e-2d3e-4b64-a2b9-a0b368b8041d.png)

<span data-ttu-id="12490-163">打开 *Controllers\CourseController.cs* 并查看 `Index` 方法：</span><span class="sxs-lookup"><span data-stu-id="12490-163">Open *Controllers\CourseController.cs* and look at the `Index` method:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

<span data-ttu-id="12490-164">自动基架使用 `Include` 方法为 `Department` 导航属性指定了预先加载。</span><span class="sxs-lookup"><span data-stu-id="12490-164">The automatic scaffolding has specified eager loading for the `Department` navigation property by using the `Include` method.</span></span>

<span data-ttu-id="12490-165">打开 *Views\Course\Index.cshtml* ，并将现有代码替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="12490-165">Open *Views\Course\Index.cshtml* and replace the existing code with the following code.</span></span> <span data-ttu-id="12490-166">突出显示所作更改：</span><span class="sxs-lookup"><span data-stu-id="12490-166">The changes are highlighted:</span></span>

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cshtml?highlight=4,15,18,28-30)]

<span data-ttu-id="12490-167">已对基架代码进行了如下更改：</span><span class="sxs-lookup"><span data-stu-id="12490-167">You've made the following changes to the scaffolded code:</span></span>

- <span data-ttu-id="12490-168">将标题从 **索引** 更改为 **课程**。</span><span class="sxs-lookup"><span data-stu-id="12490-168">Changed the heading from **Index** to **Courses**.</span></span>
- <span data-ttu-id="12490-169">将行链接向左移动。</span><span class="sxs-lookup"><span data-stu-id="12490-169">Moved the row links to the left.</span></span>
- <span data-ttu-id="12490-170">在显示属性值的标题 **编号** 下添加了一列 `CourseID` 。</span><span class="sxs-lookup"><span data-stu-id="12490-170">Added a column under the heading **Number** that shows the `CourseID` property value.</span></span> <span data-ttu-id="12490-171">默认情况下 (，主键基架，因为它们对于最终用户没有意义。</span><span class="sxs-lookup"><span data-stu-id="12490-171">(By default, primary keys aren't scaffolded because normally they are meaningless to end users.</span></span> <span data-ttu-id="12490-172">但是，在这种情况下，主键是有意义的，并且您想要将其显示。 ) </span><span class="sxs-lookup"><span data-stu-id="12490-172">However, in this case the primary key is meaningful and you want to show it.)</span></span>
- <span data-ttu-id="12490-173">更改了 **DepartmentID** 的最后一个列标题， (外键的名称到 `Department`) 到 **部门** 的实体。</span><span class="sxs-lookup"><span data-stu-id="12490-173">Changed the last column heading from **DepartmentID** (the name of the foreign key to the `Department` entity) to **Department**.</span></span>

<span data-ttu-id="12490-174">请注意，对于最后一列，基架代码显示 `Name` `Department` 加载到导航属性中的实体的属性 `Department` ：</span><span class="sxs-lookup"><span data-stu-id="12490-174">Notice that for the last column, the scaffolded code displays the `Name` property of the `Department` entity that's loaded into the `Department` navigation property:</span></span>

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cshtml)]

<span data-ttu-id="12490-175">运行页面 (在 Contoso 大学主页上选择 " **课程** " 选项卡，) 查看具有部门名称的列表。</span><span class="sxs-lookup"><span data-stu-id="12490-175">Run the page (select the **Courses** tab on the Contoso University home page) to see the list with department names.</span></span>

![Courses_index_page_with_department_names](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

## <a name="create-an-instructors-index-page-that-shows-courses-and-enrollments"></a><span data-ttu-id="12490-177">创建显示课程和注册的讲师索引页面</span><span class="sxs-lookup"><span data-stu-id="12490-177">Create an Instructors Index Page That Shows Courses and Enrollments</span></span>

<span data-ttu-id="12490-178">在本部分中，你将为实体创建一个控制器和视图，以便 `Instructor` 显示 "讲师索引" 页：</span><span class="sxs-lookup"><span data-stu-id="12490-178">In this section you'll create a controller and view for the `Instructor` entity in order to display the Instructors Index page:</span></span>

![Instructors_index_page_with_instructor_and_course_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

<span data-ttu-id="12490-180">该页面通过以下方式读取和显示相关数据：</span><span class="sxs-lookup"><span data-stu-id="12490-180">This page reads and displays related data in the following ways:</span></span>

- <span data-ttu-id="12490-181">讲师列表显示实体中的相关数据 `OfficeAssignment` 。</span><span class="sxs-lookup"><span data-stu-id="12490-181">The list of instructors displays related data from the `OfficeAssignment` entity.</span></span> <span data-ttu-id="12490-182">`Instructor` 和 `OfficeAssignment` 实体之间存在一对零或一的关系。</span><span class="sxs-lookup"><span data-stu-id="12490-182">The `Instructor` and `OfficeAssignment` entities are in a one-to-zero-or-one relationship.</span></span> <span data-ttu-id="12490-183">将对实体使用预先加载 `OfficeAssignment` 。</span><span class="sxs-lookup"><span data-stu-id="12490-183">You'll use eager loading for the `OfficeAssignment` entities.</span></span> <span data-ttu-id="12490-184">如前所述，需要主表所有检索行的相关数据时，预先加载通常更有效。</span><span class="sxs-lookup"><span data-stu-id="12490-184">As explained earlier, eager loading is typically more efficient when you need the related data for all retrieved rows of the primary table.</span></span> <span data-ttu-id="12490-185">在这种情况下，你希望显示所有显示的讲师的办公室分配情况。</span><span class="sxs-lookup"><span data-stu-id="12490-185">In this case, you want to display office assignments for all displayed instructors.</span></span>
- <span data-ttu-id="12490-186">用户选择一名讲师时，显示相关 `Course` 实体。</span><span class="sxs-lookup"><span data-stu-id="12490-186">When the user selects an instructor, related `Course` entities are displayed.</span></span> <span data-ttu-id="12490-187">`Instructor` 和 `Course` 实体之间存在多对多关系。</span><span class="sxs-lookup"><span data-stu-id="12490-187">The `Instructor` and `Course` entities are in a many-to-many relationship.</span></span> <span data-ttu-id="12490-188">你将对 `Course` 实体及其相关实体使用预先加载 `Department` 。</span><span class="sxs-lookup"><span data-stu-id="12490-188">You'll use eager loading for the `Course` entities and their related `Department` entities.</span></span> <span data-ttu-id="12490-189">在这种情况下，延迟加载可能更高效，因为你只需要为所选指导员提供课程。</span><span class="sxs-lookup"><span data-stu-id="12490-189">In this case, lazy loading might be more efficient because you need courses only for the selected instructor.</span></span> <span data-ttu-id="12490-190">但此示例显示的是如何在本身就位于导航属性内的实体中预先加载导航属性。</span><span class="sxs-lookup"><span data-stu-id="12490-190">However, this example shows how to use eager loading for navigation properties within entities that are themselves in navigation properties.</span></span>
- <span data-ttu-id="12490-191">当用户选择某一课程时，将显示该 `Enrollments` 实体集中的相关数据。</span><span class="sxs-lookup"><span data-stu-id="12490-191">When the user selects a course, related data from the `Enrollments` entity set is displayed.</span></span> <span data-ttu-id="12490-192">`Course` 和 `Enrollment` 实体之间存在一对多的关系。</span><span class="sxs-lookup"><span data-stu-id="12490-192">The `Course` and `Enrollment` entities are in a one-to-many relationship.</span></span> <span data-ttu-id="12490-193">你将添加 `Enrollment` 实体及其相关实体的显式加载 `Student` 。</span><span class="sxs-lookup"><span data-stu-id="12490-193">You'll add explicit loading for `Enrollment` entities and their related `Student` entities.</span></span> <span data-ttu-id="12490-194"> (显式加载不是必需的，因为已启用延迟加载，但这会显示如何进行显式加载。 ) </span><span class="sxs-lookup"><span data-stu-id="12490-194">(Explicit loading isn't necessary because lazy loading is enabled, but this shows how to do explicit loading.)</span></span>

### <a name="create-a-view-model-for-the-instructor-index-view"></a><span data-ttu-id="12490-195">为讲师索引视图创建视图模型</span><span class="sxs-lookup"><span data-stu-id="12490-195">Create a View Model for the Instructor Index View</span></span>

<span data-ttu-id="12490-196">"讲师索引" 页显示三个不同的表。</span><span class="sxs-lookup"><span data-stu-id="12490-196">The Instructor Index page shows three different tables.</span></span> <span data-ttu-id="12490-197">因此将创建包含三个属性的视图模型，每个属性都包含一个表的数据。</span><span class="sxs-lookup"><span data-stu-id="12490-197">Therefore, you'll create a view model that includes three properties, each holding the data for one of the tables.</span></span>

<span data-ttu-id="12490-198">在 *viewmodel* 文件夹中，创建 *InstructorIndexData.cs* 并将现有代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="12490-198">In the *ViewModels* folder, create *InstructorIndexData.cs* and replace the existing code with the following code:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs)]

### <a name="adding-a-style-for-selected-rows"></a><span data-ttu-id="12490-199">添加所选行的样式</span><span class="sxs-lookup"><span data-stu-id="12490-199">Adding a Style for Selected Rows</span></span>

<span data-ttu-id="12490-200">若要标记所选的行，需要不同的背景色。</span><span class="sxs-lookup"><span data-stu-id="12490-200">To mark selected rows you need a different background color.</span></span> <span data-ttu-id="12490-201">若要为此 UI 提供样式，请将以下突出显示的代码添加 `/* info and errors */` 到 *Content\Site.css* 中的节，如下所示：</span><span class="sxs-lookup"><span data-stu-id="12490-201">To provide a style for this UI, add the following highlighted code to the section `/* info and errors */` in *Content\Site.css*, as shown below:</span></span>

[!code-css[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.css?highlight=2-5)]

### <a name="creating-the-instructor-controller-and-views"></a><span data-ttu-id="12490-202">创建讲师控制器和视图</span><span class="sxs-lookup"><span data-stu-id="12490-202">Creating the Instructor Controller and Views</span></span>

<span data-ttu-id="12490-203">创建一个 `InstructorController` 控制器，如下图所示：</span><span class="sxs-lookup"><span data-stu-id="12490-203">Create an `InstructorController` controller as shown in the following illustration:</span></span>

![Add_Controller_dialog_box_for_Instructor_controller](https://asp.net/media/2577909/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Add_Controller_dialog_box_for_Instructor_controller_f99c10aa-1efd-49d6-af1d-b00461616107.png)

<span data-ttu-id="12490-205">打开 *Controllers\InstructorController.cs* 并 `using` 为命名空间添加语句 `ViewModels` ：</span><span class="sxs-lookup"><span data-stu-id="12490-205">Open *Controllers\InstructorController.cs* and add a `using` statement for the `ViewModels` namespace:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

<span data-ttu-id="12490-206">方法中的基架代码 `Index` 仅为导航属性指定预先加载 `OfficeAssignment` ：</span><span class="sxs-lookup"><span data-stu-id="12490-206">The scaffolded code in the `Index` method specifies eager loading only for the `OfficeAssignment` navigation property:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

<span data-ttu-id="12490-207">将方法替换为 `Index` 以下代码，以加载其他相关数据并将其放入视图模型：</span><span class="sxs-lookup"><span data-stu-id="12490-207">Replace the `Index` method with the following code to load additional related data and put it in the view model:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

<span data-ttu-id="12490-208">该方法接受可选的路由数据 (`id`) 和查询字符串参数 (`courseID`) 提供选定讲师和所选课程的 ID 值，并将所有所需数据传递给视图。</span><span class="sxs-lookup"><span data-stu-id="12490-208">The method accepts optional route data (`id`) and a query string parameter (`courseID`) that provide the ID values of the selected instructor and selected course, and passes all of the required data to the view.</span></span> <span data-ttu-id="12490-209">参数由页面上的“选择”超链接提供。</span><span class="sxs-lookup"><span data-stu-id="12490-209">The parameters are provided by the **Select** hyperlinks on the page.</span></span>

> [!TIP]
> 
> <span data-ttu-id="12490-210">**路由数据**</span><span class="sxs-lookup"><span data-stu-id="12490-210">**Route data**</span></span>
> 
> <span data-ttu-id="12490-211">路由数据是模型绑定器在路由表中指定的 URL 段中找到的数据。</span><span class="sxs-lookup"><span data-stu-id="12490-211">Route data is data that the model binder found in a URL segment specified in the routing table.</span></span> <span data-ttu-id="12490-212">例如，默认路由指定 `controller` 、 `action` 和 `id` 段：</span><span class="sxs-lookup"><span data-stu-id="12490-212">For example, the default route specifies `controller`, `action`, and `id` segments:</span></span>
> 
> ```csharp
> routes.MapRoute(  
>  name: "Default",  
>  url: "{controller}/{action}/{id}",  
>  defaults: new { controller = "Home", action = "Index", id = UrlParameter.Optional }  
> );
> ```
> 
> <span data-ttu-id="12490-213">在下面的 URL 中，默认路由映射 `Instructor` 为 `controller` ， `Index` 作为 `action` 和1作为， `id` 它们是路由数据值。</span><span class="sxs-lookup"><span data-stu-id="12490-213">In the following URL, the default route maps `Instructor` as the `controller`, `Index` as the `action` and 1 as the `id`; these are route data values.</span></span>
> 
> `http://localhost:1230/Instructor/Index/1?courseID=2021`
> 
> <span data-ttu-id="12490-214">"？ courseID = 2021" 是一个查询字符串值。</span><span class="sxs-lookup"><span data-stu-id="12490-214">"?courseID=2021" is a query string value.</span></span> <span data-ttu-id="12490-215">如果将 `id` 作为查询字符串值传递，则模型绑定器也起作用：</span><span class="sxs-lookup"><span data-stu-id="12490-215">The model binder will also work if you pass the `id` as a query string value:</span></span>
> 
> `http://localhost:1230/Instructor/Index?id=1&CourseID=2021`
> 
> <span data-ttu-id="12490-216">这些 Url 是通过 `ActionLink` Razor 视图中的语句创建的。</span><span class="sxs-lookup"><span data-stu-id="12490-216">The URLs are created by `ActionLink` statements in the Razor view.</span></span> <span data-ttu-id="12490-217">在下面的代码中， `id` 参数与默认路由匹配，因此 `id` 添加到路由数据。</span><span class="sxs-lookup"><span data-stu-id="12490-217">In the following code, the `id` parameter matches the default route, so `id` is added to the route data.</span></span>
> 
> [!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cshtml)]
> 
> <span data-ttu-id="12490-218">在下面的代码中，与 `courseID` 默认路由中的参数不匹配，因此将其添加为查询字符串。</span><span class="sxs-lookup"><span data-stu-id="12490-218">In the following code, `courseID` doesn't match a parameter in the default route, so it's added as a query string.</span></span>
> 
> [!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cshtml)]

<span data-ttu-id="12490-219">代码先创建一个视图模型实例，并在其中放入讲师列表。</span><span class="sxs-lookup"><span data-stu-id="12490-219">The code begins by creating an instance of the view model and putting in it the list of instructors.</span></span> <span data-ttu-id="12490-220">此代码为 `Instructor.OfficeAssignment` 和导航属性指定预先加载 `Instructor.Courses` 。</span><span class="sxs-lookup"><span data-stu-id="12490-220">The code specifies eager loading for the `Instructor.OfficeAssignment` and the `Instructor.Courses` navigation property.</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cs?highlight=3-4)]

<span data-ttu-id="12490-221">第二 `Include` 种方法将加载课程，对于加载的每个课程，它会预先加载 `Course.Department` 导航属性。</span><span class="sxs-lookup"><span data-stu-id="12490-221">The second `Include` method loads Courses, and for each Course that is loaded it does eager loading for the `Course.Department` navigation property.</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cs)]

<span data-ttu-id="12490-222">如前所述，无需预先加载，但会执行此操作来提高性能。</span><span class="sxs-lookup"><span data-stu-id="12490-222">As mentioned previously, eager loading is not required but is done to improve performance.</span></span> <span data-ttu-id="12490-223">由于视图始终需要 `OfficeAssignment` 实体，因此在同一查询中提取该实体会更有效。</span><span class="sxs-lookup"><span data-stu-id="12490-223">Since the view always requires the `OfficeAssignment` entity, it's more efficient to fetch that in the same query.</span></span> <span data-ttu-id="12490-224">`Course` 在网页中选择了指导员时，实体是必需的，因此，只有在选择了不使用的课程时，预先加载才能比延迟加载更好。</span><span class="sxs-lookup"><span data-stu-id="12490-224">`Course` entities are required when an instructor is selected in the web page, so eager loading is better than lazy loading only if the page is displayed more often with a course selected than without.</span></span>

<span data-ttu-id="12490-225">如果选择了指导员 ID，则会从视图模型中的指导员列表中检索所选的指导员。</span><span class="sxs-lookup"><span data-stu-id="12490-225">If an instructor ID was selected, the selected instructor is retrieved from the list of instructors in the view model.</span></span> <span data-ttu-id="12490-226">然后，将 `Courses` `Course` 从该教师导航属性中的实体加载视图模型的属性 `Courses` 。</span><span class="sxs-lookup"><span data-stu-id="12490-226">The view model's `Courses` property is then loaded with the `Course` entities from that instructor's `Courses` navigation property.</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cs)]

<span data-ttu-id="12490-227">`Where`方法返回集合，但在此示例中，传递给该方法的条件仅导致 `Instructor` 返回单个实体。</span><span class="sxs-lookup"><span data-stu-id="12490-227">The `Where` method returns a collection, but in this case the criteria passed to that method result in only a single `Instructor` entity being returned.</span></span> <span data-ttu-id="12490-228">`Single`方法将集合转换为单个 `Instructor` 实体，这使你能够访问该实体的 `Courses` 属性。</span><span class="sxs-lookup"><span data-stu-id="12490-228">The `Single` method converts the collection into a single `Instructor` entity, which gives you access to that entity's `Courses` property.</span></span>

<span data-ttu-id="12490-229">当您知道集合将只有一个项时，对集合使用 [单个](https://msdn.microsoft.com/library/system.linq.enumerable.single.aspx) 方法。</span><span class="sxs-lookup"><span data-stu-id="12490-229">You use the [Single](https://msdn.microsoft.com/library/system.linq.enumerable.single.aspx) method on a collection when you know the collection will have only one item.</span></span> <span data-ttu-id="12490-230">`Single`如果传递给它的集合为空或有多个项，则该方法将引发异常。</span><span class="sxs-lookup"><span data-stu-id="12490-230">The `Single` method throws an exception if the collection passed to it is empty or if there's more than one item.</span></span> <span data-ttu-id="12490-231">替代项为 [SingleOrDefault](https://msdn.microsoft.com/library/bb342451.aspx)，如果集合为空，它将返回默认值 (`null` 在这种情况下) 。</span><span class="sxs-lookup"><span data-stu-id="12490-231">An alternative is [SingleOrDefault](https://msdn.microsoft.com/library/bb342451.aspx), which returns a default value (`null` in this case) if the collection is empty.</span></span> <span data-ttu-id="12490-232">但是，在这种情况下，仍会导致异常 (尝试查找 `Courses` 引用) 上的属性 `null` ，并且异常消息不会明确指出问题的原因。</span><span class="sxs-lookup"><span data-stu-id="12490-232">However, in this case that would still result in an exception (from trying to find a `Courses` property on a `null` reference), and the exception message would less clearly indicate the cause of the problem.</span></span> <span data-ttu-id="12490-233">调用 `Single` 方法时，还可以传递 `Where` 条件，而不是 `Where` 单独调用方法：</span><span class="sxs-lookup"><span data-stu-id="12490-233">When you call the `Single` method, you can also pass in the `Where` condition instead of calling the `Where` method separately:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cs)]

<span data-ttu-id="12490-234">而不是：</span><span class="sxs-lookup"><span data-stu-id="12490-234">Instead of:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cs)]

<span data-ttu-id="12490-235">接着，如果选择了课程，则从视图模型中的课程列表中检索所选课程。</span><span class="sxs-lookup"><span data-stu-id="12490-235">Next, if a course was selected, the selected course is retrieved from the list of courses in the view model.</span></span> <span data-ttu-id="12490-236">然后，将 `Enrollments` `Enrollment` 从该课程的导航属性中的实体加载视图模型的属性 `Enrollments` 。</span><span class="sxs-lookup"><span data-stu-id="12490-236">Then the view model's `Enrollments` property is loaded with the `Enrollment` entities from that course's `Enrollments` navigation property.</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cs)]

### <a name="modifying-the-instructor-index-view"></a><span data-ttu-id="12490-237">修改讲师索引视图</span><span class="sxs-lookup"><span data-stu-id="12490-237">Modifying the Instructor Index View</span></span>

<span data-ttu-id="12490-238">在 *Views\Instructor\Index.cshtml* 中，将现有代码替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="12490-238">In *Views\Instructor\Index.cshtml*, replace the existing code with the following code.</span></span> <span data-ttu-id="12490-239">突出显示所作更改：</span><span class="sxs-lookup"><span data-stu-id="12490-239">The changes are highlighted:</span></span>

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cshtml?highlight=1,4,18,22-27,29,43-48)]

<span data-ttu-id="12490-240">已对现有代码进行了如下更改：</span><span class="sxs-lookup"><span data-stu-id="12490-240">You've made the following changes to the existing code:</span></span>

- <span data-ttu-id="12490-241">将模型类更改为了 `InstructorIndexData`。</span><span class="sxs-lookup"><span data-stu-id="12490-241">Changed the model class to `InstructorIndexData`.</span></span>
- <span data-ttu-id="12490-242">将页标题从“索引”更改为了“讲师” 。</span><span class="sxs-lookup"><span data-stu-id="12490-242">Changed the page title from **Index** to **Instructors**.</span></span>
- <span data-ttu-id="12490-243">将行链接列向左移动。</span><span class="sxs-lookup"><span data-stu-id="12490-243">Moved the row link columns to the left.</span></span>
- <span data-ttu-id="12490-244">删除了 **FullName** 列。</span><span class="sxs-lookup"><span data-stu-id="12490-244">Removed the **FullName** column.</span></span>
- <span data-ttu-id="12490-245">添加了仅当不为 null 时才显示的 **Office** 列 `item.OfficeAssignment.Location` `item.OfficeAssignment` 。</span><span class="sxs-lookup"><span data-stu-id="12490-245">Added an **Office** column that displays `item.OfficeAssignment.Location` only if `item.OfficeAssignment` is not null.</span></span> <span data-ttu-id="12490-246"> (因为这是一对零或一关系，因此可能没有相关的 `OfficeAssignment` 实体。 ) </span><span class="sxs-lookup"><span data-stu-id="12490-246">(Because this is a one-to-zero-or-one relationship, there might not be a related `OfficeAssignment` entity.)</span></span> 

    [!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cshtml)]
- <span data-ttu-id="12490-247">添加了将动态添加 `class="selectedrow"` 到选定讲师的元素中的代码 `tr` 。</span><span class="sxs-lookup"><span data-stu-id="12490-247">Added code that will dynamically add `class="selectedrow"` to the `tr` element of the selected instructor.</span></span> <span data-ttu-id="12490-248">这将使用之前创建的 CSS 类设置所选行的背景色。</span><span class="sxs-lookup"><span data-stu-id="12490-248">This sets a background color for the selected row using the CSS class that you created earlier.</span></span> <span data-ttu-id="12490-249">在 `valign` 以下教程中，将多行列添加到表中时，属性 (将非常有用。 ) </span><span class="sxs-lookup"><span data-stu-id="12490-249">(The `valign` attribute will be useful in the following tutorial when you add a multi-row column to the table.)</span></span> 

    [!code-html[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.html)]
- <span data-ttu-id="12490-250">`ActionLink`在每行中的其他链接之前添加了一个新的标签 **选择**，这将导致所选的指导员 ID 发送到 `Index` 方法。</span><span class="sxs-lookup"><span data-stu-id="12490-250">Added a new `ActionLink` labeled **Select** immediately before the other links in each row, which causes the selected instructor ID to be sent to the `Index` method.</span></span>

<span data-ttu-id="12490-251">运行应用程序并选择 " **讲师** " 选项卡。 `Location` 当没有相关实体时，此页将显示相关实体的属性 `OfficeAssignment` 和一个空的表单元 `OfficeAssignment` 。</span><span class="sxs-lookup"><span data-stu-id="12490-251">Run the application and select the **Instructors** tab. The page displays the `Location` property of related `OfficeAssignment` entities and an empty table cell when there's no related `OfficeAssignment` entity.</span></span>

![Instructors_index_page_with_nothing_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)

<span data-ttu-id="12490-253">在 *Views\Instructor\Index.cshtml* 文件中，在 `table`) 文件末尾 (结束元素之后，添加以下突出显示的代码。</span><span class="sxs-lookup"><span data-stu-id="12490-253">In the *Views\Instructor\Index.cshtml* file, after the closing `table` element (at the end of the file), add the following highlighted code.</span></span> <span data-ttu-id="12490-254">选择指导员后，将显示与讲师相关的课程列表。</span><span class="sxs-lookup"><span data-stu-id="12490-254">This displays a list of courses related to an instructor when an instructor is selected.</span></span>

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cshtml?highlight=11-46)]

<span data-ttu-id="12490-255">此代码读取视图模型的 `Courses` 属性以显示课程列表。</span><span class="sxs-lookup"><span data-stu-id="12490-255">This code reads the `Courses` property of the view model to display a list of courses.</span></span> <span data-ttu-id="12490-256">它还提供了一个 `Select` 超链接，该超链接将所选课程的 ID 发送到 `Index` 操作方法。</span><span class="sxs-lookup"><span data-stu-id="12490-256">It also provides a `Select` hyperlink that sends the ID of the selected course to the `Index` action method.</span></span>

> [!NOTE]
> <span data-ttu-id="12490-257">*Css* 文件由浏览器进行缓存。</span><span class="sxs-lookup"><span data-stu-id="12490-257">The *.css* file is cached by browsers.</span></span> <span data-ttu-id="12490-258">如果在运行应用程序时看不到所做的更改，请执行硬刷新 (按住 CTRL 键的同时单击 " **刷新** " 按钮，或按 Ctrl + F5) 。</span><span class="sxs-lookup"><span data-stu-id="12490-258">If you don't see the changes when you run the application, do a hard refresh (hold down the CTRL key while clicking the **Refresh** button, or press CTRL+F5).</span></span>

<span data-ttu-id="12490-259">运行页面并选择一个指导员。</span><span class="sxs-lookup"><span data-stu-id="12490-259">Run the page and select an instructor.</span></span> <span data-ttu-id="12490-260">此时会出现一个网格，其中显示有分配给所选讲师的课程，且还显示有每个课程的分配系的名称。</span><span class="sxs-lookup"><span data-stu-id="12490-260">Now you see a grid that displays courses assigned to the selected instructor, and for each course you see the name of the assigned department.</span></span>

![Instructors_index_page_with_instructor_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

<span data-ttu-id="12490-262">在刚刚添加的代码块后，添加以下代码。</span><span class="sxs-lookup"><span data-stu-id="12490-262">After the code block you just added, add the following code.</span></span> <span data-ttu-id="12490-263">选择课程后，代码将显示参与课程的学生列表。</span><span class="sxs-lookup"><span data-stu-id="12490-263">This displays a list of the students who are enrolled in a course when that course is selected.</span></span>

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cshtml)]

<span data-ttu-id="12490-264">此代码读取 `Enrollments` 视图模型的属性，以显示课程中注册的学生列表。</span><span class="sxs-lookup"><span data-stu-id="12490-264">This code reads the `Enrollments` property of the view model in order to display a list of students enrolled in the course.</span></span>

<span data-ttu-id="12490-265">运行页面并选择一个指导员。</span><span class="sxs-lookup"><span data-stu-id="12490-265">Run the page and select an instructor.</span></span> <span data-ttu-id="12490-266">然后选择一门课程，查看参与的学生列表及其成绩。</span><span class="sxs-lookup"><span data-stu-id="12490-266">Then select a course to see the list of enrolled students and their grades.</span></span>

![Instructors_index_page_with_instructor_and_course_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

### <a name="adding-explicit-loading"></a><span data-ttu-id="12490-268">添加显式加载</span><span class="sxs-lookup"><span data-stu-id="12490-268">Adding Explicit Loading</span></span>

<span data-ttu-id="12490-269">打开 *InstructorController.cs* ，并查看方法如何 `Index` 获取所选课程的注册列表：</span><span class="sxs-lookup"><span data-stu-id="12490-269">Open *InstructorController.cs* and look at how the `Index` method gets the list of enrollments for a selected course:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample23.cs)]

<span data-ttu-id="12490-270">检索到讲师列表时，你为导航属性指定了预先加载， `Courses` 并为 `Department` 每个课程的属性指定了预先加载。</span><span class="sxs-lookup"><span data-stu-id="12490-270">When you retrieved the list of instructors, you specified eager loading for the `Courses` navigation property and for the `Department` property of each course.</span></span> <span data-ttu-id="12490-271">然后，将 `Courses` 集合放入视图模型，此时将 `Enrollments` 从该集合中的一个实体访问导航属性。</span><span class="sxs-lookup"><span data-stu-id="12490-271">Then you put the `Courses` collection in the view model, and now you're accessing the `Enrollments` navigation property from one entity in that collection.</span></span> <span data-ttu-id="12490-272">由于没有为导航属性指定预先加载 `Course.Enrollments` ，因此该属性中的数据将作为延迟加载的结果出现在页中。</span><span class="sxs-lookup"><span data-stu-id="12490-272">Because you didn't specify eager loading for the `Course.Enrollments` navigation property, the data from that property is appearing in the page as a result of lazy loading.</span></span>

<span data-ttu-id="12490-273">如果在不以任何其他方式更改代码的情况下禁用了延迟加载，则 `Enrollments` 无论该课程实际具有多少注册，属性都将为 null。</span><span class="sxs-lookup"><span data-stu-id="12490-273">If you disabled lazy loading without changing the code in any other way, the `Enrollments` property would be null regardless of how many enrollments the course actually had.</span></span> <span data-ttu-id="12490-274">在这种情况下，若要加载 `Enrollments` 属性，必须指定预先加载或显式加载。</span><span class="sxs-lookup"><span data-stu-id="12490-274">In that case, to load the `Enrollments` property, you'd have to specify either eager loading or explicit loading.</span></span> <span data-ttu-id="12490-275">您已经了解了如何执行预先加载。</span><span class="sxs-lookup"><span data-stu-id="12490-275">You've already seen how to do eager loading.</span></span> <span data-ttu-id="12490-276">若要查看显式加载的示例，请将方法替换 `Index` 为以下代码，以显式加载 `Enrollments` 属性。</span><span class="sxs-lookup"><span data-stu-id="12490-276">In order to see an example of explicit loading, replace the `Index` method with the following code, which explicitly loads the `Enrollments` property.</span></span> <span data-ttu-id="12490-277">更改的代码已突出显示。</span><span class="sxs-lookup"><span data-stu-id="12490-277">The code changed are highlighted.</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample24.cs?highlight=20-27)]

<span data-ttu-id="12490-278">获取所选 `Course` 实体后，新代码将显式加载该课程的 `Enrollments` 导航属性：</span><span class="sxs-lookup"><span data-stu-id="12490-278">After getting the selected `Course` entity, the new code explicitly loads that course's `Enrollments` navigation property:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample25.cs)]

<span data-ttu-id="12490-279">然后，它显式加载每个 `Enrollment` 实体的相关 `Student` 实体：</span><span class="sxs-lookup"><span data-stu-id="12490-279">Then it explicitly loads each `Enrollment` entity's related `Student` entity:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample26.cs)]

<span data-ttu-id="12490-280">请注意，使用 `Collection` 方法加载集合属性，但对于只包含一个实体的属性，则使用 `Reference` 方法。</span><span class="sxs-lookup"><span data-stu-id="12490-280">Notice that you use the `Collection` method to load a collection property, but for a property that holds just one entity, you use the `Reference` method.</span></span> <span data-ttu-id="12490-281">你现在可以运行讲师索引页面，并且你将看到页面上显示的内容没有任何区别，但你已更改数据的检索方式。</span><span class="sxs-lookup"><span data-stu-id="12490-281">You can run the Instructor Index page now and you'll see no difference in what's displayed on the page, although you've changed how the data is retrieved.</span></span>

## <a name="summary"></a><span data-ttu-id="12490-282">总结</span><span class="sxs-lookup"><span data-stu-id="12490-282">Summary</span></span>

<span data-ttu-id="12490-283">现在，你已使用了所有三种方法 (延迟、预先和显式) 将相关数据加载到导航属性。</span><span class="sxs-lookup"><span data-stu-id="12490-283">You've now used all three ways (lazy, eager, and explicit) to load related data into navigation properties.</span></span> <span data-ttu-id="12490-284">下一个教程将介绍如何更新相关数据。</span><span class="sxs-lookup"><span data-stu-id="12490-284">In the next tutorial you'll learn how to update related data.</span></span>

<span data-ttu-id="12490-285">可在 [ASP.NET 数据访问内容映射](../../../../whitepapers/aspnet-data-access-content-map.md)中找到指向其他实体框架资源的链接。</span><span class="sxs-lookup"><span data-stu-id="12490-285">Links to other Entity Framework resources can be found in the [ASP.NET Data Access Content Map](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="12490-286">[上一页](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md)
> [下一页](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)</span><span class="sxs-lookup"><span data-stu-id="12490-286">[Previous](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md)
[Next](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)</span></span>

---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application
title: 在 ASP.NET MVC 应用程序中实现与实体框架的继承 (8 of 10) |Microsoft Docs
author: tdykstra
description: Contoso 大学示例 web 应用程序演示如何使用实体框架 5 Code First 和 Visual Studio .。。
ms.author: riande
ms.date: 07/30/2013
ms.assetid: a5c3feff-5335-4cdd-a97d-f7a8785c2494
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: de86dd0d1a8e1b68d14971d328fe88a7fdb3e9b1
ms.sourcegitcommit: b4cdcf246850751579e45da80c9780fe56330dd0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2021
ms.locfileid: "99984734"
---
# <a name="implementing-inheritance-with-the-entity-framework-in-an-aspnet-mvc-application-8-of-10"></a><span data-ttu-id="9fab0-103">在 ASP.NET MVC 应用程序中实现与实体框架的继承 (第8项，共10个) </span><span class="sxs-lookup"><span data-stu-id="9fab0-103">Implementing Inheritance with the Entity Framework in an ASP.NET MVC Application (8 of 10)</span></span>

<span data-ttu-id="9fab0-104">作者： [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="9fab0-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

> <span data-ttu-id="9fab0-105">Contoso 大学示例 web 应用程序演示了如何使用实体框架 5 Code First 和 Visual Studio 2012 创建 ASP.NET MVC 4 应用程序。</span><span class="sxs-lookup"><span data-stu-id="9fab0-105">The Contoso University sample web application demonstrates how to create ASP.NET MVC 4 applications using the Entity Framework 5 Code First and Visual Studio 2012.</span></span> <span data-ttu-id="9fab0-106">若要了解教程系列，请参阅[本系列中的第一个教程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。</span><span class="sxs-lookup"><span data-stu-id="9fab0-106">For information about the tutorial series, see [the first tutorial in the series](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>
> 
> > [!NOTE] 
> > 
> > <span data-ttu-id="9fab0-107">如果遇到无法解决的问题，请 [下载已完成的章节](building-the-ef5-mvc4-chapter-downloads.md) 并尝试重现你的问题。</span><span class="sxs-lookup"><span data-stu-id="9fab0-107">If you run into a problem you can't resolve, [download the completed chapter](building-the-ef5-mvc4-chapter-downloads.md) and try to reproduce your problem.</span></span> <span data-ttu-id="9fab0-108">通常可以通过将代码与已完成的代码进行比较，查找问题的解决方案。</span><span class="sxs-lookup"><span data-stu-id="9fab0-108">You can generally find the solution to the problem by comparing your code to the completed code.</span></span> <span data-ttu-id="9fab0-109">有关一些常见错误以及如何解决这些错误，请参阅 [错误和解决方法。](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)</span><span class="sxs-lookup"><span data-stu-id="9fab0-109">For some common errors and how to solve them, see [Errors and Workarounds.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)</span></span>

<span data-ttu-id="9fab0-110">在上一教程中，您已处理并发异常。</span><span class="sxs-lookup"><span data-stu-id="9fab0-110">In the previous tutorial you handled concurrency exceptions.</span></span> <span data-ttu-id="9fab0-111">本教程将演示如何在数据模型中实现继承。</span><span class="sxs-lookup"><span data-stu-id="9fab0-111">This tutorial will show you how to implement inheritance in the data model.</span></span>

<span data-ttu-id="9fab0-112">在面向对象的编程中，可以使用继承来消除冗余代码。</span><span class="sxs-lookup"><span data-stu-id="9fab0-112">In object-oriented programming, you can use inheritance to eliminate redundant code.</span></span> <span data-ttu-id="9fab0-113">在本教程中，将更改 `Instructor` 和 `Student` 类，以便从 `Person` 基类中派生，该基类包含教师和学生所共有的属性（如 `LastName`）。</span><span class="sxs-lookup"><span data-stu-id="9fab0-113">In this tutorial, you'll change the `Instructor` and `Student` classes so that they derive from a `Person` base class which contains properties such as `LastName` that are common to both instructors and students.</span></span> <span data-ttu-id="9fab0-114">不会添加或更改任何网页，但会更改部分代码，并将在数据库中自动反映这些更改。</span><span class="sxs-lookup"><span data-stu-id="9fab0-114">You won't add or change any web pages, but you'll change some of the code and those changes will be automatically reflected in the database.</span></span>

## <a name="table-per-hierarchy-versus-table-per-type-inheritance"></a><span data-ttu-id="9fab0-115">每个层次结构一个表和每种类型一个表继承</span><span class="sxs-lookup"><span data-stu-id="9fab0-115">Table-per-Hierarchy versus Table-per-Type Inheritance</span></span>

<span data-ttu-id="9fab0-116">在面向对象的编程中，可以使用继承来更轻松地处理相关类。</span><span class="sxs-lookup"><span data-stu-id="9fab0-116">In object-oriented programming, you can use inheritance to make it easier to work with related classes.</span></span> <span data-ttu-id="9fab0-117">例如， `Instructor` `Student` 数据模型中的和类 `School` 共享若干属性，这将导致冗余代码：</span><span class="sxs-lookup"><span data-stu-id="9fab0-117">For example, the `Instructor` and `Student` classes in the `School` data model share several properties, which results in redundant code:</span></span>

![Student_and_Instructor_classes](https://asp.net/media/2578113/Windows-Live-Writer_58f5a93579b2_CC7B_Student_and_Instructor_classes_e7a32f99-8bc4-48ce-aeaf-216a18071a8b.png)

<span data-ttu-id="9fab0-119">假设想要消除由 `Instructor` 和`Student` 实体共享的属性的冗余代码。</span><span class="sxs-lookup"><span data-stu-id="9fab0-119">Suppose you want to eliminate the redundant code for the properties that are shared by the `Instructor` and `Student` entities.</span></span> <span data-ttu-id="9fab0-120">你可以创建 `Person` 只包含这些共享属性的基类，然后使 `Instructor` 和 `Student` 实体继承自该基类，如下图所示：</span><span class="sxs-lookup"><span data-stu-id="9fab0-120">You could create a `Person` base class which contains only those shared properties, then make the `Instructor` and `Student` entities inherit from that base class, as shown in the following illustration:</span></span>

![Student_and_Instructor_classes_deriving_from_Person_class](https://asp.net/media/2578119/Windows-Live-Writer_58f5a93579b2_CC7B_Student_and_Instructor_classes_deriving_from_Person_class_671d708c-cbb8-454a-a8f8-c2d99439acd9.png)

<span data-ttu-id="9fab0-122">有多种方法可以在数据库中表示此继承结构。</span><span class="sxs-lookup"><span data-stu-id="9fab0-122">There are several ways this inheritance structure could be represented in the database.</span></span> <span data-ttu-id="9fab0-123">您可能有一个 `Person` 表，其中包含有关学生和教师在单个表中的信息。</span><span class="sxs-lookup"><span data-stu-id="9fab0-123">You could have a `Person` table that includes information about both students and instructors in a single table.</span></span> <span data-ttu-id="9fab0-124">某些列可能仅适用于指导员 (`HireDate`) ，某些列仅适用于 () 的学生，其中一些是 `EnrollmentDate` () `LastName` `FirstName` 。</span><span class="sxs-lookup"><span data-stu-id="9fab0-124">Some of the columns could apply only to instructors (`HireDate`), some only to students (`EnrollmentDate`), some to both (`LastName`, `FirstName`).</span></span> <span data-ttu-id="9fab0-125">通常，您可以使用 *鉴别* 器列来指示每一行代表哪种类型。</span><span class="sxs-lookup"><span data-stu-id="9fab0-125">Typically, you'd have a *discriminator* column to indicate which type each row represents.</span></span> <span data-ttu-id="9fab0-126">例如，鉴别器列可能包含“Instructor”来指示教师，包含“Student”来指示学生。</span><span class="sxs-lookup"><span data-stu-id="9fab0-126">For example, the discriminator column might have "Instructor" for instructors and "Student" for students.</span></span>

![每 hierarchy_example 一个表](https://asp.net/media/2578125/Windows-Live-Writer_58f5a93579b2_CC7B_Table-per-hierarchy_example_244067cd-b451-4e9b-9595-793b9afca505.png)

<span data-ttu-id="9fab0-128">从单个数据库表生成实体继承结构这一模式称为 " *每个层次结构一个表* " (TPH) 继承。</span><span class="sxs-lookup"><span data-stu-id="9fab0-128">This pattern of generating an entity inheritance structure from a single database table is called *table-per-hierarchy* (TPH) inheritance.</span></span>

<span data-ttu-id="9fab0-129">另一种方法是使数据库看起来更像继承结构。</span><span class="sxs-lookup"><span data-stu-id="9fab0-129">An alternative is to make the database look more like the inheritance structure.</span></span> <span data-ttu-id="9fab0-130">例如，在表中只能有名称字段 `Person` ，并且具有 `Instructor` 具有日期字段的单独的和 `Student` 表。</span><span class="sxs-lookup"><span data-stu-id="9fab0-130">For example, you could have only the name fields in the `Person` table and have separate `Instructor` and `Student` tables with the date fields.</span></span>

![每 type_inheritance 一个表](https://asp.net/media/2578131/Windows-Live-Writer_58f5a93579b2_CC7B_Table-per-type_inheritance.png)

<span data-ttu-id="9fab0-132">为每个实体类创建数据库表的这种模式将 (TPT) 继承的 *每个类型* 都称为 table。</span><span class="sxs-lookup"><span data-stu-id="9fab0-132">This pattern of making a database table for each entity class is called *table per type* (TPT) inheritance.</span></span>

<span data-ttu-id="9fab0-133">TPH 继承模式通常比 TPT 继承模式提供更好实体框架的性能，因为 TPT 模式可能会导致复杂的联接查询。</span><span class="sxs-lookup"><span data-stu-id="9fab0-133">TPH inheritance patterns generally deliver better performance in the Entity Framework than TPT inheritance patterns, because TPT patterns can result in complex join queries.</span></span> <span data-ttu-id="9fab0-134">本教程将演示如何实现 TPH 继承。</span><span class="sxs-lookup"><span data-stu-id="9fab0-134">This tutorial demonstrates how to implement TPH inheritance.</span></span> <span data-ttu-id="9fab0-135">可以通过执行以下步骤来执行此操作：</span><span class="sxs-lookup"><span data-stu-id="9fab0-135">You'll do that by performing the following steps:</span></span>

- <span data-ttu-id="9fab0-136">创建一个 `Person` 类，并将 `Instructor` 和 `Student` 类更改为派生自 `Person` 。</span><span class="sxs-lookup"><span data-stu-id="9fab0-136">Create a `Person` class and change the `Instructor` and `Student` classes to derive from `Person`.</span></span>
- <span data-ttu-id="9fab0-137">向数据库上下文类添加模型到数据库的映射代码。</span><span class="sxs-lookup"><span data-stu-id="9fab0-137">Add model-to-database mapping code to the database context class.</span></span>
- <span data-ttu-id="9fab0-138">在 `InstructorID` `StudentID` 整个项目中更改和引用 `PersonID` 。</span><span class="sxs-lookup"><span data-stu-id="9fab0-138">Change `InstructorID` and `StudentID` references throughout the project to `PersonID`.</span></span>

## <a name="creating-the-person-class"></a><span data-ttu-id="9fab0-139">创建 Person 类</span><span class="sxs-lookup"><span data-stu-id="9fab0-139">Creating the Person Class</span></span>

 <span data-ttu-id="9fab0-140">注意：在你更新使用这些类的控制器之前，你将无法编译该项目。</span><span class="sxs-lookup"><span data-stu-id="9fab0-140">Note: You won't be able to compile the project after creating the classes below until you update the controllers that uses these classes.</span></span> 

<span data-ttu-id="9fab0-141">在 " *模型* " 文件夹中，创建 *Person.cs* ，并将模板代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="9fab0-141">In the *Models* folder, create *Person.cs* and replace the template code with the following code:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

<span data-ttu-id="9fab0-142">在 *Instructor.cs* 中， `Instructor` 从类派生类 `Person` ，并删除 "键" 和 "名称" 字段。</span><span class="sxs-lookup"><span data-stu-id="9fab0-142">In *Instructor.cs*, derive the `Instructor` class from the `Person` class and remove the key and name fields.</span></span> <span data-ttu-id="9fab0-143">代码将如下所示：</span><span class="sxs-lookup"><span data-stu-id="9fab0-143">The code will look like the following example:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

<span data-ttu-id="9fab0-144">对 *Student.cs* 进行类似的更改。</span><span class="sxs-lookup"><span data-stu-id="9fab0-144">Make similar changes to *Student.cs*.</span></span> <span data-ttu-id="9fab0-145">`Student`类将类似于以下示例：</span><span class="sxs-lookup"><span data-stu-id="9fab0-145">The `Student` class will look like the following example:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs)]

## <a name="adding-the-person-entity-type-to-the-model"></a><span data-ttu-id="9fab0-146">将 Person 实体类型添加到模型</span><span class="sxs-lookup"><span data-stu-id="9fab0-146">Adding the Person Entity Type to the Model</span></span>

<span data-ttu-id="9fab0-147">在 *SchoolContext.cs* 中， `DbSet` 为 `Person` 实体类型添加属性：</span><span class="sxs-lookup"><span data-stu-id="9fab0-147">In *SchoolContext.cs*, add a `DbSet` property for the `Person` entity type:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

<span data-ttu-id="9fab0-148">以上是 Entity Framework 配置每个层次结构一张表继承所需的全部操作。</span><span class="sxs-lookup"><span data-stu-id="9fab0-148">This is all that the Entity Framework needs in order to configure table-per-hierarchy inheritance.</span></span> <span data-ttu-id="9fab0-149">正如您所看到的，重新创建数据库时，它将具有一个 `Person` 表来代替 `Student` 和 `Instructor` 表。</span><span class="sxs-lookup"><span data-stu-id="9fab0-149">As you'll see, when the database is re-created, it will have a `Person` table in place of the `Student` and `Instructor` tables.</span></span>

## <a name="changing-instructorid-and-studentid-to-personid"></a><span data-ttu-id="9fab0-150">将 InstructorID 和 StudentID 更改为 PersonID</span><span class="sxs-lookup"><span data-stu-id="9fab0-150">Changing InstructorID and StudentID to PersonID</span></span>

<span data-ttu-id="9fab0-151">在 *SchoolContext.cs* 的 Instructor-Course 映射语句中，将更改 `MapRightKey("InstructorID")` 为 `MapRightKey("PersonID")` ：</span><span class="sxs-lookup"><span data-stu-id="9fab0-151">In *SchoolContext.cs*, in the Instructor-Course mapping statement, change `MapRightKey("InstructorID")` to `MapRightKey("PersonID")`:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs?highlight=4)]

<span data-ttu-id="9fab0-152">这不是必需的更改;它只更改多对多联接表中 InstructorID 列的名称。</span><span class="sxs-lookup"><span data-stu-id="9fab0-152">This change isn't required; it just changes the name of the InstructorID column in the many-to-many join table.</span></span> <span data-ttu-id="9fab0-153">如果将名称保留为 InstructorID，应用程序仍将正常工作。</span><span class="sxs-lookup"><span data-stu-id="9fab0-153">If you left the name as InstructorID, the application would still work correctly.</span></span> <span data-ttu-id="9fab0-154">下面是已完成的 *SchoolContext.cs*：</span><span class="sxs-lookup"><span data-stu-id="9fab0-154">Here is the completed *SchoolContext.cs*:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs?highlight=15,24)]

<span data-ttu-id="9fab0-155">接下来，需要在 `InstructorID` 项目中更改为和，并将其更改为在 " `PersonID` `StudentID` `PersonID` _Migrations \*" 文件夹的时间戳的迁移文件中。</span><span class="sxs-lookup"><span data-stu-id="9fab0-155">Next you need to change `InstructorID` to `PersonID` and `StudentID` to `PersonID` throughout the project ***except** _ in the time-stamped migrations files in the _Migrations* folder.</span></span> <span data-ttu-id="9fab0-156">为此，你将找到并仅打开需要更改的文件，然后对打开的文件执行全局更改。</span><span class="sxs-lookup"><span data-stu-id="9fab0-156">To do that you'll find and open only the files that need to be changed, then perform a global change on the opened files.</span></span> <span data-ttu-id="9fab0-157">应更改的 *迁移* 文件夹中的唯一文件是 *Migrations\Configuration.cs.*</span><span class="sxs-lookup"><span data-stu-id="9fab0-157">The only file in the *Migrations* folder you should change is *Migrations\Configuration.cs.*</span></span>

1. > [!IMPORTANT]
   > <span data-ttu-id="9fab0-158">首先，在 Visual Studio 中关闭所有打开的文件。</span><span class="sxs-lookup"><span data-stu-id="9fab0-158">Begin by closing all the open files in Visual Studio.</span></span>
2. <span data-ttu-id="9fab0-159">单击 " **查找并替换"--** 在 " **编辑** " 菜单中查找所有文件，然后搜索包含的项目中的所有文件 `InstructorID` 。</span><span class="sxs-lookup"><span data-stu-id="9fab0-159">Click **Find and Replace -- Find all Files** in the **Edit** menu, and then search for all files in the project that contain `InstructorID`.</span></span>  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)
3. <span data-ttu-id="9fab0-160">在 "**查找结果**" 窗口中打开每 \*\* 个文件 &lt; （在 "迁移" 文件夹中，"时间戳" &gt; _ \_ .cs \* 迁移文件除外），方法是双击每个文件对应一行。 </span><span class="sxs-lookup"><span data-stu-id="9fab0-160">Open each file in the **Find Results** window **_except_* _ the &lt;time-stamp&gt;_\_.cs* migration files in the *Migrations* folder, by double-clicking one line for each file.</span></span>  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)
4. <span data-ttu-id="9fab0-161">打开 " **在文件中替换** " 对话框，并将 " **查看** " 更改为 **所有打开的文档**。</span><span class="sxs-lookup"><span data-stu-id="9fab0-161">Open the **Replace in Files** dialog and change **Look in** to **All Open Documents**.</span></span>
5. <span data-ttu-id="9fab0-162">使用 " **在文件中替换** " 对话框可将所有更改 `InstructorID` 为 `PersonID.`</span><span class="sxs-lookup"><span data-stu-id="9fab0-162">Use the **Replace in Files** dialog to change all `InstructorID` to `PersonID.`</span></span>  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)
6. <span data-ttu-id="9fab0-163">查找项目中包含的所有文件 `StudentID` 。</span><span class="sxs-lookup"><span data-stu-id="9fab0-163">Find all the files in the project that contain `StudentID`.</span></span>
7. <span data-ttu-id="9fab0-164">在 "**查找结果**" 窗口中打开每 \*\* 个文件 &lt; （在 "迁移" 文件夹中，"时间戳" &gt; _ \_ \* .cs \* 迁移文件除外），方法是双击每个文件对应一行。 </span><span class="sxs-lookup"><span data-stu-id="9fab0-164">Open each file in the **Find Results** window **_except_* _ the &lt;time-stamp&gt;_\_\*.cs* migration files in the *Migrations* folder, by double-clicking one line for each file.</span></span>  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)
8. <span data-ttu-id="9fab0-165">打开 " **在文件中替换** " 对话框，并将 " **查看** " 更改为 **所有打开的文档**。</span><span class="sxs-lookup"><span data-stu-id="9fab0-165">Open the **Replace in Files** dialog and change **Look in** to **All Open Documents**.</span></span>
9. <span data-ttu-id="9fab0-166">使用 " **在文件中替换** " 对话框可以将所有更改 `StudentID` 为 `PersonID` 。</span><span class="sxs-lookup"><span data-stu-id="9fab0-166">Use the **Replace in Files** dialog to change all `StudentID` to `PersonID`.</span></span>   
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)
10. <span data-ttu-id="9fab0-167">生成项目。</span><span class="sxs-lookup"><span data-stu-id="9fab0-167">Build the project.</span></span>

<span data-ttu-id="9fab0-168"> (请注意，这说明了 `classnameID` 命名主键的模式的缺点。</span><span class="sxs-lookup"><span data-stu-id="9fab0-168">(Note that this demonstrates a *disadvantage* of the `classnameID` pattern for naming primary keys.</span></span> <span data-ttu-id="9fab0-169">如果已命名 primary keys ID 但未指定类名前缀，则现在 *不* 需要重命名。 ) </span><span class="sxs-lookup"><span data-stu-id="9fab0-169">If you had named primary keys ID without prefixing the class name, *no* renaming would be necessary now.)</span></span>

## <a name="create-and-update-a-migrations-file"></a><span data-ttu-id="9fab0-170">创建和更新迁移文件</span><span class="sxs-lookup"><span data-stu-id="9fab0-170">Create and Update a Migrations File</span></span>

<span data-ttu-id="9fab0-171">在 "包管理器控制台 (PMC") 中，输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="9fab0-171">In the Package Manager Console (PMC), enter the following command:</span></span>

`Add-Migration Inheritance`

<span data-ttu-id="9fab0-172">`Update-Database`在 PMC 中运行命令。</span><span class="sxs-lookup"><span data-stu-id="9fab0-172">Run the `Update-Database` command in the PMC.</span></span> <span data-ttu-id="9fab0-173">此时，该命令将失败，因为我们有迁移不知道如何处理的现有数据。</span><span class="sxs-lookup"><span data-stu-id="9fab0-173">The command will fail at this point because we have existing data that migrations doesn't know how to handle.</span></span> <span data-ttu-id="9fab0-174">收到以下错误：</span><span class="sxs-lookup"><span data-stu-id="9fab0-174">You get the following error:</span></span>

<span data-ttu-id="9fab0-175">*ALTER TABLE 语句与外键约束 "FK dbo" 冲突 \_ 。部 \_ dbo。Person \_ PersonID "。在表 "dbo" 的数据库 "ContosoUniversity" 中发生冲突。Person "，列" PersonID "。*</span><span class="sxs-lookup"><span data-stu-id="9fab0-175">*The ALTER TABLE statement conflicted with the FOREIGN KEY constraint "FK\_dbo.Department\_dbo.Person\_PersonID". The conflict occurred in database "ContosoUniversity", table "dbo.Person", column 'PersonID'.*</span></span>

<span data-ttu-id="9fab0-176">打开 *迁移 \& lt; timestamp &gt; \_ Inheritance.cs* ，并 `Up` 将方法替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="9fab0-176">Open *Migrations\&lt;timestamp&gt;\_Inheritance.cs* and replace the `Up` method with the following code:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs?highlight=25,29-40)]

<span data-ttu-id="9fab0-177">再次运行命令 `update-database`。</span><span class="sxs-lookup"><span data-stu-id="9fab0-177">Run the `update-database` command again.</span></span>

> [!NOTE]
> <span data-ttu-id="9fab0-178">迁移数据和进行架构更改时，可能会收到其他错误。</span><span class="sxs-lookup"><span data-stu-id="9fab0-178">It's possible to get other errors when migrating data and making schema changes.</span></span> <span data-ttu-id="9fab0-179">如果收到无法解决的迁移错误，可以继续学习本教程，方法是更改 *Web.config* 文件中的连接字符串或删除数据库。</span><span class="sxs-lookup"><span data-stu-id="9fab0-179">If you get migration errors you can't resolve, you can continue with the tutorial by changing the connection string in the *Web.config* file or deleting the database.</span></span> <span data-ttu-id="9fab0-180">最简单的方法是重命名 *Web.config* 文件中的数据库。</span><span class="sxs-lookup"><span data-stu-id="9fab0-180">The simplest approach is to rename the database in the *Web.config* file.</span></span> <span data-ttu-id="9fab0-181">例如，将 "数据库名称" 更改为 "CU 测试"， \_ 如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="9fab0-181">For example, change the database name to CU\_test as shown in the following example:</span></span>
> 
> [!code-xml[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.xml?highlight=1-2)]
> 
> <span data-ttu-id="9fab0-182">对于新数据库，没有要迁移的数据，并且 `update-database` 命令更有可能在没有错误的情况下完成。</span><span class="sxs-lookup"><span data-stu-id="9fab0-182">With a new database, there is no data to migrate, and the `update-database` command is much more likely to complete without errors.</span></span> <span data-ttu-id="9fab0-183">有关如何删除数据库的说明，请参阅 [如何从 Visual Studio 2012 中删除数据库](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/)。</span><span class="sxs-lookup"><span data-stu-id="9fab0-183">For instructions on how to delete the database, see [How to Drop a Database from Visual Studio 2012](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/).</span></span> <span data-ttu-id="9fab0-184">如果你使用此方法继续学习本教程，请跳过本教程末尾的部署步骤，因为部署的站点会在自动运行迁移时收到相同的错误。</span><span class="sxs-lookup"><span data-stu-id="9fab0-184">If you take this approach in order to continue with the tutorial, skip the deployment step at the end of this tutorial, since the deployed site would get the same error when it runs migrations automatically.</span></span> <span data-ttu-id="9fab0-185">如果要解决迁移错误，最佳资源是实体框架论坛或 StackOverflow.com 之一。</span><span class="sxs-lookup"><span data-stu-id="9fab0-185">If you want to troubleshoot a migrations error, the best resource is one of the Entity Framework forums or StackOverflow.com.</span></span>

## <a name="testing"></a><span data-ttu-id="9fab0-186">正在测试</span><span class="sxs-lookup"><span data-stu-id="9fab0-186">Testing</span></span>

<span data-ttu-id="9fab0-187">运行站点并尝试各种页面。</span><span class="sxs-lookup"><span data-stu-id="9fab0-187">Run the site and try various pages.</span></span> <span data-ttu-id="9fab0-188">一切都和以前一样。</span><span class="sxs-lookup"><span data-stu-id="9fab0-188">Everything works the same as it did before.</span></span>

<span data-ttu-id="9fab0-189">在 **服务器资源管理器中，** 展开 " **SchoolContext** " 和 "**表**"，你会看到 "学生 **" 表已** 替换 "**学生** **" 表。**</span><span class="sxs-lookup"><span data-stu-id="9fab0-189">In **Server Explorer,** expand **SchoolContext** and then **Tables**, and you see that the **Student** and **Instructor** tables have been replaced by a **Person** table.</span></span> <span data-ttu-id="9fab0-190">展开 " **人员** " 表，你会看到它包含所有在 " **学生** " 和 " **讲师** " 表中使用的列。</span><span class="sxs-lookup"><span data-stu-id="9fab0-190">Expand the **Person** table and you see that it has all of the columns that used to be in the **Student** and **Instructor** tables.</span></span>

![Server_Explorer_showing_Person_table](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

<span data-ttu-id="9fab0-192">右键单击 Person 表，然后单击“显示表数据”以查看鉴别器列。</span><span class="sxs-lookup"><span data-stu-id="9fab0-192">Right-click the Person table, and then click **Show Table Data** to see the discriminator column.</span></span>

![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

<span data-ttu-id="9fab0-193">下图说明了新的 School 数据库的结构：</span><span class="sxs-lookup"><span data-stu-id="9fab0-193">The following diagram illustrates the structure of the new School database:</span></span>

![School_database_diagram](https://asp.net/media/2578143/Windows-Live-Writer_58f5a93579b2_CC7B_School_database_diagram_6350a801-7199-413f-bbac-4a2009ed19d7.png)

## <a name="summary"></a><span data-ttu-id="9fab0-195">总结</span><span class="sxs-lookup"><span data-stu-id="9fab0-195">Summary</span></span>

<span data-ttu-id="9fab0-196">"每个层次结构一个表" 继承现在已为 `Person` 、 `Student` 和 `Instructor` 类实现。</span><span class="sxs-lookup"><span data-stu-id="9fab0-196">Table-per-hierarchy inheritance has now been implemented for the `Person`, `Student`, and `Instructor` classes.</span></span> <span data-ttu-id="9fab0-197">有关此和其他继承结构的详细信息，请参阅 Morteza Manavi 的博客上的 [继承映射策略](https://weblogs.asp.net/manavi/archive/2010/12/24/inheritance-mapping-strategies-with-entity-framework-code-first-ctp5-part-1-table-per-hierarchy-tph.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="9fab0-197">For more information about this and other inheritance structures, see [Inheritance Mapping Strategies](https://weblogs.asp.net/manavi/archive/2010/12/24/inheritance-mapping-strategies-with-entity-framework-code-first-ctp5-part-1-table-per-hierarchy-tph.aspx) on Morteza Manavi's blog.</span></span> <span data-ttu-id="9fab0-198">在下一教程中，你将看到实现存储库和工作单元模式的一些方式。</span><span class="sxs-lookup"><span data-stu-id="9fab0-198">In the next tutorial you'll see some ways to implement the repository and unit of work patterns.</span></span>

<span data-ttu-id="9fab0-199">可在 [ASP.NET 数据访问内容映射](../../../../whitepapers/aspnet-data-access-content-map.md)中找到指向其他实体框架资源的链接。</span><span class="sxs-lookup"><span data-stu-id="9fab0-199">Links to other Entity Framework resources can be found in the [ASP.NET Data Access Content Map](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="9fab0-200">[上一页](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)
> [下一页](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md)</span><span class="sxs-lookup"><span data-stu-id="9fab0-200">[Previous](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)
[Next](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md)</span></span>

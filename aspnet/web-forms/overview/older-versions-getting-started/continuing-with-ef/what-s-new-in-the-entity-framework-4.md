---
uid: web-forms/overview/older-versions-getting-started/continuing-with-ef/what-s-new-in-the-entity-framework-4
title: 什么是 Entity Framework 4.0 中的新增功能 |Microsoft Docs
author: tdykstra
description: 本系列教程以 Contoso University web 应用程序创建的与 Entity Framework 4.0 教程系列入门教程为基础。 我...
ms.author: riande
ms.date: 01/26/2011
ms.assetid: 393df4a8-b1db-44c4-9db7-2b533ca887d0
msc.legacyurl: /web-forms/overview/older-versions-getting-started/continuing-with-ef/what-s-new-in-the-entity-framework-4
msc.type: authoredcontent
ms.openlocfilehash: 0bc24a59e09728a5ecb6e18378c4cde0c8e046f2
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/09/2019
ms.locfileid: "59387446"
---
# <a name="whats-new-in-the-entity-framework-40"></a><span data-ttu-id="e5661-104">Entity Framework 4.0 的新增功能</span><span class="sxs-lookup"><span data-stu-id="e5661-104">What's New in the Entity Framework 4.0</span></span>

<span data-ttu-id="e5661-105">通过[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="e5661-105">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

> <span data-ttu-id="e5661-106">本系列教程为基础创建的 Contoso University web 应用程序[开始使用 Entity Framework](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md)系列教程。</span><span class="sxs-lookup"><span data-stu-id="e5661-106">This tutorial series builds on the Contoso University web application that is created by the [Getting Started with the Entity Framework](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md) tutorial series.</span></span> <span data-ttu-id="e5661-107">如果未完成之前的教程，作为本教程的起始点可以[下载应用程序](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a)，您已经创建的。</span><span class="sxs-lookup"><span data-stu-id="e5661-107">If you didn't complete the earlier tutorials, as a starting point for this tutorial you can [download the application](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a) that you would have created.</span></span> <span data-ttu-id="e5661-108">此外可以[下载应用程序](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa)由完整的系列教程。</span><span class="sxs-lookup"><span data-stu-id="e5661-108">You can also [download the application](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa) that is created by the complete tutorial series.</span></span> <span data-ttu-id="e5661-109">如果你有疑问的教程，您可以发布到[ASP.NET 实体框架论坛](https://forums.asp.net/1227.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e5661-109">If you have questions about the tutorials, you can post them to the [ASP.NET Entity Framework forum](https://forums.asp.net/1227.aspx).</span></span>


<span data-ttu-id="e5661-110">在上一教程中，您将看到一些用于使用实体框架的 web 应用程序的性能的方法。</span><span class="sxs-lookup"><span data-stu-id="e5661-110">In the previous tutorial you saw some methods for maximizing the performance of a web application that uses the Entity Framework.</span></span> <span data-ttu-id="e5661-111">本教程介绍了一些 Entity Framework 的版本 4 中的最重要新功能，而且它链接到提供的所有新功能的更完整介绍的资源。</span><span class="sxs-lookup"><span data-stu-id="e5661-111">This tutorial reviews some of the most important new features in version 4 of the Entity Framework, and it links to resources that provide a more complete introduction to all of the new features.</span></span> <span data-ttu-id="e5661-112">在本教程中突出显示的功能包括：</span><span class="sxs-lookup"><span data-stu-id="e5661-112">The features highlighted in this tutorial include the following:</span></span>

- <span data-ttu-id="e5661-113">外键关联。</span><span class="sxs-lookup"><span data-stu-id="e5661-113">Foreign-key associations.</span></span>
- <span data-ttu-id="e5661-114">正在执行用户定义的 SQL 命令。</span><span class="sxs-lookup"><span data-stu-id="e5661-114">Executing user-defined SQL commands.</span></span>
- <span data-ttu-id="e5661-115">模型优先开发。</span><span class="sxs-lookup"><span data-stu-id="e5661-115">Model-first development.</span></span>
- <span data-ttu-id="e5661-116">POCO 支持。</span><span class="sxs-lookup"><span data-stu-id="e5661-116">POCO support.</span></span>

<span data-ttu-id="e5661-117">此外，本教程将简要介绍*代码优先的开发*，实体框架的下一个版本中即将推出的功能。</span><span class="sxs-lookup"><span data-stu-id="e5661-117">In addition, the tutorial will briefly introduce *code-first development*, a feature that's coming in the next release of the Entity Framework.</span></span>

<span data-ttu-id="e5661-118">若要开始本教程，启动 Visual Studio 并打开在您使用在上一教程中的 Contoso University web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="e5661-118">To start the tutorial, start Visual Studio and open the Contoso University web application that you were working with in the previous tutorial.</span></span>

## <a name="foreign-key-associations"></a><span data-ttu-id="e5661-119">外键关联</span><span class="sxs-lookup"><span data-stu-id="e5661-119">Foreign-Key Associations</span></span>

<span data-ttu-id="e5661-120">Entity Framework 3.5 版包含导航属性，但它不在数据模型中包括外键属性。</span><span class="sxs-lookup"><span data-stu-id="e5661-120">Version 3.5 of the Entity Framework included navigation properties, but it didn't include foreign-key properties in the data model.</span></span> <span data-ttu-id="e5661-121">例如，`CourseID`并`StudentID`的列`StudentGrade`表将省略从`StudentGrade`实体。</span><span class="sxs-lookup"><span data-stu-id="e5661-121">For example, the `CourseID` and `StudentID` columns of the `StudentGrade` table would be omitted from the `StudentGrade` entity.</span></span>

[![I<span data-ttu-id="e5661-122">mage01]</span><span class="sxs-lookup"><span data-stu-id="e5661-122">mage01]</span></span>(what-s-new-in-the-entity-framework-4/_static/image2.png)](what-s-new-in-the-entity-framework-4/_static/image1.png)

<span data-ttu-id="e5661-123">这种方法的原因是，严格地说外, 键是物理实现细节，不属于概念数据模型中。</span><span class="sxs-lookup"><span data-stu-id="e5661-123">The reason for this approach was that, strictly speaking, foreign keys are a physical implementation detail and don't belong in a conceptual data model.</span></span> <span data-ttu-id="e5661-124">但是，在实践中，通常很容易地直接访问的外键时处理代码中的实体。</span><span class="sxs-lookup"><span data-stu-id="e5661-124">However, as a practical matter, it's often easier to work with entities in code when you have direct access to the foreign keys.</span></span>

<span data-ttu-id="e5661-125">有关如何外键的数据模型中的示例可以简化你的代码，请考虑如何你将获得了对代码*DepartmentsAdd.aspx*页，但它们没有。</span><span class="sxs-lookup"><span data-stu-id="e5661-125">For an example of how foreign keys in the data model can simplify your code, consider how you would have had to code the *DepartmentsAdd.aspx* page without them.</span></span> <span data-ttu-id="e5661-126">在中`Department`实体，`Administrator`属性是对应于一个外键`PersonID`中`Person`实体。</span><span class="sxs-lookup"><span data-stu-id="e5661-126">In the `Department` entity, the `Administrator` property is a foreign key that corresponds to `PersonID` in the `Person` entity.</span></span> <span data-ttu-id="e5661-127">若要建立新系和它的管理员之间的关联，您所要做已设置的值`Administrator`中的属性`ItemInserting`数据绑定控件的事件处理程序：</span><span class="sxs-lookup"><span data-stu-id="e5661-127">In order to establish the association between a new department and its administrator, all you had to do was set the value for the `Administrator` property in the `ItemInserting` event handler of the databound control:</span></span>

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample1.cs)]

<span data-ttu-id="e5661-128">不用数据模型中的外键，将处理`Inserting`事件的数据源控件，而不是`ItemInserting`数据绑定控件，以获取对实体本身的引用，该实体添加到实体集之前的事件。</span><span class="sxs-lookup"><span data-stu-id="e5661-128">Without foreign keys in the data model, you'd handle the `Inserting` event of the data source control instead of the `ItemInserting` event of the databound control, in order to get a reference to the entity itself before the entity is added to the entity set.</span></span> <span data-ttu-id="e5661-129">该引用后，你建立使用类似于下面的示例中的代码的关联：</span><span class="sxs-lookup"><span data-stu-id="e5661-129">When you have that reference, you establish the association using code like that in the following examples:</span></span>

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample2.cs)]

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample3.cs)]

<span data-ttu-id="e5661-130">正如您可以在实体框架团队看到[外键关联上的博客文章](https://blogs.msdn.com/b/efdesign/archive/2009/03/16/foreign-keys-in-the-entity-framework.aspx)，其他情况下，代码复杂性的区别是要多得多。</span><span class="sxs-lookup"><span data-stu-id="e5661-130">As you can see in the Entity Framework team's [blog post on Foreign Key associations](https://blogs.msdn.com/b/efdesign/archive/2009/03/16/foreign-keys-in-the-entity-framework.aspx), there are other cases where the difference in code complexity is much greater.</span></span> <span data-ttu-id="e5661-131">为了满足这些面向更愿意忍受为了代码较简单的概念数据模型中的实现详细信息的需求，实体框架将会提供的数据模型中包括外键的选项。</span><span class="sxs-lookup"><span data-stu-id="e5661-131">To meet the needs of those who prefer to live with implementation details in the conceptual data model for the sake of simpler code, the Entity Framework now gives you the option of including foreign keys in the data model.</span></span>

<span data-ttu-id="e5661-132">在实体框架术语中，如果数据模型中包括外键使用的*外键关联*，并且如果排除正在使用的外键*独立关联*。</span><span class="sxs-lookup"><span data-stu-id="e5661-132">In Entity Framework terminology, if you include foreign keys in the data model you're using *foreign key associations*, and if you exclude foreign keys you're using *independent associations*.</span></span>

## <a name="executing-user-defined-sql-commands"></a><span data-ttu-id="e5661-133">执行用户定义的 SQL 命令</span><span class="sxs-lookup"><span data-stu-id="e5661-133">Executing User-Defined SQL Commands</span></span>

<span data-ttu-id="e5661-134">在早期版本的实体框架中，没有简单方法来动态创建自己的 SQL 命令并运行它们。</span><span class="sxs-lookup"><span data-stu-id="e5661-134">In earlier versions of the Entity Framework, there was no easy way to create your own SQL commands on the fly and run them.</span></span> <span data-ttu-id="e5661-135">实体框架动态生成的 SQL 命令，或者您必须创建一个存储的过程并将其作为函数导入。</span><span class="sxs-lookup"><span data-stu-id="e5661-135">Either the Entity Framework dynamically generated SQL commands for you, or you had to create a stored procedure and import it as a function.</span></span> <span data-ttu-id="e5661-136">添加了版本 4`ExecuteStoreQuery`并`ExecuteStoreCommand`方法`ObjectContext`使你更轻松地直接向数据库传递任何查询的类。</span><span class="sxs-lookup"><span data-stu-id="e5661-136">Version 4 adds `ExecuteStoreQuery` and `ExecuteStoreCommand` methods the `ObjectContext` class that make it easier for you to pass any query directly to the database.</span></span>

<span data-ttu-id="e5661-137">假设 Contoso 大学管理员想要能够在数据库中执行大容量更改，而无需经历创建存储的过程并导入数据模型的过程。</span><span class="sxs-lookup"><span data-stu-id="e5661-137">Suppose Contoso University administrators want to be able to perform bulk changes in the database without having to go through the process of creating a stored procedure and importing it into the data model.</span></span> <span data-ttu-id="e5661-138">其第一个请求是用于将允许他们更改数据库中的所有课程的可修读人数的页面。</span><span class="sxs-lookup"><span data-stu-id="e5661-138">Their first request is for a page that lets them change the number of credits for all courses in the database.</span></span> <span data-ttu-id="e5661-139">在 web 页上，他们想要能够输入一个数字，以用于将的值相乘，每个`Course`行的`Credits`列。</span><span class="sxs-lookup"><span data-stu-id="e5661-139">On the web page, they want to be able to enter a number to use to multiply the value of every `Course` row's `Credits` column.</span></span>

<span data-ttu-id="e5661-140">创建新的页面，使用*Site.Master*母版页并将其命名*UpdateCredits.aspx*。</span><span class="sxs-lookup"><span data-stu-id="e5661-140">Create a new page that uses the *Site.Master* master page and name it *UpdateCredits.aspx*.</span></span> <span data-ttu-id="e5661-141">然后添加以下标记到`Content`名为控件`Content2`:</span><span class="sxs-lookup"><span data-stu-id="e5661-141">Then add the following markup to the `Content` control named `Content2`:</span></span>

[!code-aspx[Main](what-s-new-in-the-entity-framework-4/samples/sample4.aspx)]

<span data-ttu-id="e5661-142">此标记创建`TextBox`控制用户可以在其中输入乘数值，`Button`才能执行该命令中，单击控件和一个`Label`控件用于指示受影响的行数。</span><span class="sxs-lookup"><span data-stu-id="e5661-142">This markup creates a `TextBox` control in which the user can enter the multiplier value, a `Button` control to click in order to execute the command, and a `Label` control for indicating the number of rows affected.</span></span>

<span data-ttu-id="e5661-143">打开*UpdateCredits.aspx.cs*，并添加以下`using`语句，并为按钮的处理程序`Click`事件：</span><span class="sxs-lookup"><span data-stu-id="e5661-143">Open *UpdateCredits.aspx.cs*, and add the following `using` statement and a handler for the button's `Click` event:</span></span>

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample5.cs)]

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample6.cs)]

<span data-ttu-id="e5661-144">此代码执行 SQL`Update`命令在文本框中使用的值，并使用标签来显示受影响的行数。</span><span class="sxs-lookup"><span data-stu-id="e5661-144">This code executes the SQL `Update` command using the value in the text box and uses the label to display the number of rows affected.</span></span> <span data-ttu-id="e5661-145">运行该页面之前，请运行*Courses.aspx*页面以获取"before"图片的一些数据。</span><span class="sxs-lookup"><span data-stu-id="e5661-145">Before you run the page, run the *Courses.aspx* page to get a "before" picture of some data.</span></span>

[![I<span data-ttu-id="e5661-146">mage02]</span><span class="sxs-lookup"><span data-stu-id="e5661-146">mage02]</span></span>(what-s-new-in-the-entity-framework-4/_static/image4.png)](what-s-new-in-the-entity-framework-4/_static/image3.png)

<span data-ttu-id="e5661-147">运行*UpdateCredits.aspx*，作为乘数，输入"10"，然后单击**Execute**。</span><span class="sxs-lookup"><span data-stu-id="e5661-147">Run *UpdateCredits.aspx*, enter "10" as the multiplier, and then click **Execute**.</span></span>

[![I<span data-ttu-id="e5661-148">mage03]</span><span class="sxs-lookup"><span data-stu-id="e5661-148">mage03]</span></span>(what-s-new-in-the-entity-framework-4/_static/image6.png)](what-s-new-in-the-entity-framework-4/_static/image5.png)

<span data-ttu-id="e5661-149">运行*Courses.aspx*页上再次看到已更改的数据。</span><span class="sxs-lookup"><span data-stu-id="e5661-149">Run the *Courses.aspx* page again to see the changed data.</span></span>

[![I<span data-ttu-id="e5661-150">mage04]</span><span class="sxs-lookup"><span data-stu-id="e5661-150">mage04]</span></span>(what-s-new-in-the-entity-framework-4/_static/image8.png)](what-s-new-in-the-entity-framework-4/_static/image7.png)

<span data-ttu-id="e5661-151">(如果你想要在设置回其原始值的可修读人数*UpdateCredits.aspx.cs*更改`Credits * {0}`到`Credits / {0}`，然后重新运行页上，输入 10 与除数的符号。)</span><span class="sxs-lookup"><span data-stu-id="e5661-151">(If you want to set the number of credits back to their original values, in *UpdateCredits.aspx.cs* change `Credits * {0}` to `Credits / {0}` and re-run the page, entering 10 as the divisor.)</span></span>

<span data-ttu-id="e5661-152">有关执行查询，以在代码中定义的详细信息，请参阅[如何：针对数据源直接执行命令](https://msdn.microsoft.com/library/ee358769.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e5661-152">For more information about executing queries that you define in code, see [How to: Directly Execute Commands Against the Data Source](https://msdn.microsoft.com/library/ee358769.aspx).</span></span>

## <a name="model-first-development"></a><span data-ttu-id="e5661-153">模型优先开发</span><span class="sxs-lookup"><span data-stu-id="e5661-153">Model-First Development</span></span>

<span data-ttu-id="e5661-154">在这些演练将首先创建数据库和数据库结构所基于的数据模型，则生成。</span><span class="sxs-lookup"><span data-stu-id="e5661-154">In these walkthroughs you created the database first and then generated the data model based on the database structure.</span></span> <span data-ttu-id="e5661-155">Entity Framework 4 可以改为开始使用数据模型，生成基于数据模型结构的数据库。</span><span class="sxs-lookup"><span data-stu-id="e5661-155">In the Entity Framework 4 you can start with the data model instead and generate the database based on the data model structure.</span></span> <span data-ttu-id="e5661-156">如果要创建应用程序数据库已不存在，模型为先的方法，可创建实体和关系从概念上讲适合应用程序，而不需担心如何物理实现详细信息.</span><span class="sxs-lookup"><span data-stu-id="e5661-156">If you're creating an application for which the database doesn't already exist, the model-first approach enables you to create entities and relationships that make sense conceptually for the application, while not worrying about physical implementation details.</span></span> <span data-ttu-id="e5661-157">（也不例外仅通过初始阶段的开发，但是。</span><span class="sxs-lookup"><span data-stu-id="e5661-157">(This remains true only through the initial stages of development, however.</span></span> <span data-ttu-id="e5661-158">最终数据库将创建将生产数据，并且让模型中重新创建它将不再是实际;此时，您会回数据库为先的方法。）</span><span class="sxs-lookup"><span data-stu-id="e5661-158">Eventually the database will be created and will have production data in it, and recreating it from the model will no longer be practical; at that point you'll be back to the database-first approach.)</span></span>

<span data-ttu-id="e5661-159">在本教程的此部分中，将创建一个简单数据模型并从中生成数据库。</span><span class="sxs-lookup"><span data-stu-id="e5661-159">In this section of the tutorial, you'll create a simple data model and generate the database from it.</span></span>

<span data-ttu-id="e5661-160">在中**解决方案资源管理器**，右键单击*DAL*文件夹，然后选择**添加新项**。</span><span class="sxs-lookup"><span data-stu-id="e5661-160">In **Solution Explorer**, right-click the *DAL* folder and select **Add New Item**.</span></span> <span data-ttu-id="e5661-161">在中**添加新项**对话框中的**已安装的模板**选择**数据**，然后选择**ADO.NET 实体数据模型**模板.</span><span class="sxs-lookup"><span data-stu-id="e5661-161">In the **Add New Item** dialog box, under **Installed Templates** select **Data** and then select the **ADO.NET Entity Data Model** template.</span></span> <span data-ttu-id="e5661-162">将新文件命名*AlumniAssociationModel.edmx*然后单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="e5661-162">Name the new file *AlumniAssociationModel.edmx* and click **Add**.</span></span>

[![I<span data-ttu-id="e5661-163">mage06]</span><span class="sxs-lookup"><span data-stu-id="e5661-163">mage06]</span></span>(what-s-new-in-the-entity-framework-4/_static/image10.png)](what-s-new-in-the-entity-framework-4/_static/image9.png)

<span data-ttu-id="e5661-164">这将启动实体数据模型向导。</span><span class="sxs-lookup"><span data-stu-id="e5661-164">This launches the Entity Data Model Wizard.</span></span> <span data-ttu-id="e5661-165">在中**选择模型内容**步骤中，选择**空模型**，然后单击**完成**。</span><span class="sxs-lookup"><span data-stu-id="e5661-165">In the **Choose Model Contents** step, select **Empty Model** and then click **Finish**.</span></span>

[![I<span data-ttu-id="e5661-166">mage07]</span><span class="sxs-lookup"><span data-stu-id="e5661-166">mage07]</span></span>(what-s-new-in-the-entity-framework-4/_static/image12.png)](what-s-new-in-the-entity-framework-4/_static/image11.png)

<span data-ttu-id="e5661-167">**实体数据模型设计器**打开与空白设计图面。</span><span class="sxs-lookup"><span data-stu-id="e5661-167">The **Entity Data Model Designer** opens with a blank design surface.</span></span> <span data-ttu-id="e5661-168">拖动**实体**项从**工具箱**拖到设计图面。</span><span class="sxs-lookup"><span data-stu-id="e5661-168">Drag an **Entity** item from the **Toolbox** onto the design surface.</span></span>

[![I<span data-ttu-id="e5661-169">mage08]</span><span class="sxs-lookup"><span data-stu-id="e5661-169">mage08]</span></span>(what-s-new-in-the-entity-framework-4/_static/image14.png)](what-s-new-in-the-entity-framework-4/_static/image13.png)

<span data-ttu-id="e5661-170">更改从实体名称`Entity1`到`Alumnus`，更改`Id`属性名称设置为`AlumnusId`，并添加名为的新标量属性`Name`。</span><span class="sxs-lookup"><span data-stu-id="e5661-170">Change the entity name from `Entity1` to `Alumnus`, change the `Id` property name to `AlumnusId`, and add a new scalar property named `Name`.</span></span> <span data-ttu-id="e5661-171">若要添加新属性，您可以更改的名称后按 Enter`Id`列中，或右键单击该实体，然后选择**添加标量属性**。</span><span class="sxs-lookup"><span data-stu-id="e5661-171">To add new properties you can press Enter after changing the name of the `Id` column, or right-click the entity and select **Add Scalar Property**.</span></span> <span data-ttu-id="e5661-172">新的属性的默认类型是`String`，这样很好此简单演示，但当然可以更改中的数据类型等**属性**窗口。</span><span class="sxs-lookup"><span data-stu-id="e5661-172">The default type for new properties is `String`, which is fine for this simple demonstration, but of course you can change things like data type in the **Properties** window.</span></span>

<span data-ttu-id="e5661-173">创建相同的方式的另一个实体并将其命名`Donation`。</span><span class="sxs-lookup"><span data-stu-id="e5661-173">Create another entity the same way and name it `Donation`.</span></span> <span data-ttu-id="e5661-174">更改`Id`属性设置为`DonationId`并添加名为的标量属性`DateAndAmount`。</span><span class="sxs-lookup"><span data-stu-id="e5661-174">Change the `Id` property to `DonationId` and add a scalar property named `DateAndAmount`.</span></span>

[![I<span data-ttu-id="e5661-175">mage09]</span><span class="sxs-lookup"><span data-stu-id="e5661-175">mage09]</span></span>(what-s-new-in-the-entity-framework-4/_static/image16.png)](what-s-new-in-the-entity-framework-4/_static/image15.png)

<span data-ttu-id="e5661-176">若要添加这两个实体之间的关联，请右键单击`Alumnus`实体中，选择**添加**，然后选择**关联**。</span><span class="sxs-lookup"><span data-stu-id="e5661-176">To add an association between these two entities, right-click the `Alumnus` entity, select **Add**, and then select **Association**.</span></span>

[![I<span data-ttu-id="e5661-177">mage10]</span><span class="sxs-lookup"><span data-stu-id="e5661-177">mage10]</span></span>(what-s-new-in-the-entity-framework-4/_static/image18.png)](what-s-new-in-the-entity-framework-4/_static/image17.png)

<span data-ttu-id="e5661-178">中的默认值**添加关联**是您需要的对话框 （一个多，包括导航属性，包括外键），因此只需单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="e5661-178">The default values in the **Add Association** dialog box are what you want (one-to-many, include navigation properties, include foreign keys), so just click **OK**.</span></span>

[![I<span data-ttu-id="e5661-179">mage11]</span><span class="sxs-lookup"><span data-stu-id="e5661-179">mage11]</span></span>(what-s-new-in-the-entity-framework-4/_static/image20.png)](what-s-new-in-the-entity-framework-4/_static/image19.png)

<span data-ttu-id="e5661-180">在设计器添加一条关联连线和外键属性。</span><span class="sxs-lookup"><span data-stu-id="e5661-180">The designer adds an association line and a foreign-key property.</span></span>

[![I<span data-ttu-id="e5661-181">mage12]</span><span class="sxs-lookup"><span data-stu-id="e5661-181">mage12]</span></span>(what-s-new-in-the-entity-framework-4/_static/image22.png)](what-s-new-in-the-entity-framework-4/_static/image21.png)

<span data-ttu-id="e5661-182">现在你已准备好创建数据库。</span><span class="sxs-lookup"><span data-stu-id="e5661-182">Now you're ready to create the database.</span></span> <span data-ttu-id="e5661-183">右键单击设计图面，然后选择**根据模型生成数据库**。</span><span class="sxs-lookup"><span data-stu-id="e5661-183">Right-click the design surface and select **Generate Database from Model**.</span></span>

[![I<span data-ttu-id="e5661-184">mage13]</span><span class="sxs-lookup"><span data-stu-id="e5661-184">mage13]</span></span>(what-s-new-in-the-entity-framework-4/_static/image24.png)](what-s-new-in-the-entity-framework-4/_static/image23.png)

<span data-ttu-id="e5661-185">这将启动生成数据库向导。</span><span class="sxs-lookup"><span data-stu-id="e5661-185">This launches the Generate Database Wizard.</span></span> <span data-ttu-id="e5661-186">（如果看到警告，指示未映射实体，你可以忽略这些暂时。）</span><span class="sxs-lookup"><span data-stu-id="e5661-186">(If you see warnings that indicate that the entities aren't mapped, you can ignore those for the time being.)</span></span>

<span data-ttu-id="e5661-187">在中**选择数据连接**步骤中，单击**新的连接**。</span><span class="sxs-lookup"><span data-stu-id="e5661-187">In the **Choose Your Data Connection** step, click **New Connection**.</span></span>

[![I<span data-ttu-id="e5661-188">mage14]</span><span class="sxs-lookup"><span data-stu-id="e5661-188">mage14]</span></span>(what-s-new-in-the-entity-framework-4/_static/image26.png)](what-s-new-in-the-entity-framework-4/_static/image25.png)

<span data-ttu-id="e5661-189">在中**连接属性**对话框中选择本地 SQL Server Express 实例，数据库命名为`AlumniAssociation`。</span><span class="sxs-lookup"><span data-stu-id="e5661-189">In the **Connection Properties** dialog box, select the local SQL Server Express instance and name the database `AlumniAssociation`.</span></span>

[![I<span data-ttu-id="e5661-190">mage15]</span><span class="sxs-lookup"><span data-stu-id="e5661-190">mage15]</span></span>(what-s-new-in-the-entity-framework-4/_static/image28.png)](what-s-new-in-the-entity-framework-4/_static/image27.png)

<span data-ttu-id="e5661-191">单击**是**时，会询问你是否想要创建数据库。</span><span class="sxs-lookup"><span data-stu-id="e5661-191">Click **Yes** when you're asked if you want to create the database.</span></span> <span data-ttu-id="e5661-192">当**选择数据连接**再次显示步骤中，单击**下一步**。</span><span class="sxs-lookup"><span data-stu-id="e5661-192">When the **Choose Your Data Connection** step is displayed again, click **Next**.</span></span>

<span data-ttu-id="e5661-193">在中**摘要和设置**步骤中，单击**完成**。</span><span class="sxs-lookup"><span data-stu-id="e5661-193">In the **Summary and Settings** step, click **Finish**.</span></span>

[![I<span data-ttu-id="e5661-194">mage18]</span><span class="sxs-lookup"><span data-stu-id="e5661-194">mage18]</span></span>(what-s-new-in-the-entity-framework-4/_static/image30.png)](what-s-new-in-the-entity-framework-4/_static/image29.png)

<span data-ttu-id="e5661-195">一个 *.sql*创建为文件数据定义语言 (DDL) 命令，但命令尚未运行。</span><span class="sxs-lookup"><span data-stu-id="e5661-195">A *.sql* file with the data definition language (DDL) commands is created, but the commands haven't been run yet.</span></span>

[![I<span data-ttu-id="e5661-196">mage20]</span><span class="sxs-lookup"><span data-stu-id="e5661-196">mage20]</span></span>(what-s-new-in-the-entity-framework-4/_static/image32.png)](what-s-new-in-the-entity-framework-4/_static/image31.png)

<span data-ttu-id="e5661-197">使用一种工具，如**SQL Server Management Studio**运行该脚本并创建表，如可能在创建时已完成`School`数据库[入门教程系列中的第一个教程](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md).</span><span class="sxs-lookup"><span data-stu-id="e5661-197">Use a tool such as **SQL Server Management Studio** to run the script and create the tables, as you might have done when you created the `School` database for [the first tutorial in the Getting Started tutorial series](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md).</span></span> <span data-ttu-id="e5661-198">（除非您下载此数据库）。</span><span class="sxs-lookup"><span data-stu-id="e5661-198">(Unless you downloaded the database.)</span></span>

<span data-ttu-id="e5661-199">现在，您可以使用`AlumniAssociation`数据模型在您的 web 页你所用的相同方式`School`模型。</span><span class="sxs-lookup"><span data-stu-id="e5661-199">You can now use the `AlumniAssociation` data model in your web pages the same way you've been using the `School` model.</span></span> <span data-ttu-id="e5661-200">若要试用此项，向表中添加一些数据并创建一个网页，显示的数据。</span><span class="sxs-lookup"><span data-stu-id="e5661-200">To try this out, add some data to the tables and create a web page that displays the data.</span></span>

<span data-ttu-id="e5661-201">使用**服务器资源管理器**，添加以下行`Alumnus`和`Donation`表。</span><span class="sxs-lookup"><span data-stu-id="e5661-201">Using **Server Explorer**, add the following rows to the `Alumnus` and `Donation` tables.</span></span>

[![I<span data-ttu-id="e5661-202">mage21]</span><span class="sxs-lookup"><span data-stu-id="e5661-202">mage21]</span></span>(what-s-new-in-the-entity-framework-4/_static/image34.png)](what-s-new-in-the-entity-framework-4/_static/image33.png)

<span data-ttu-id="e5661-203">创建一个名为的新 web 页*Alumni.aspx* ，它使用*Site.Master*母版页。</span><span class="sxs-lookup"><span data-stu-id="e5661-203">Create a new web page named *Alumni.aspx* that uses the *Site.Master* master page.</span></span> <span data-ttu-id="e5661-204">添加到以下标记`Content`名为控件`Content2`:</span><span class="sxs-lookup"><span data-stu-id="e5661-204">Add the following markup to the `Content` control named `Content2`:</span></span>

[!code-aspx[Main](what-s-new-in-the-entity-framework-4/samples/sample7.aspx)]

<span data-ttu-id="e5661-205">此标记创建嵌套`GridView`控制，外部显示校友名称和内部显示捐赠日期和数量。</span><span class="sxs-lookup"><span data-stu-id="e5661-205">This markup creates nested `GridView` controls, the outer one to display alumni names and the inner one to display donation dates and amounts.</span></span>

<span data-ttu-id="e5661-206">打开*Alumni.aspx.cs*。</span><span class="sxs-lookup"><span data-stu-id="e5661-206">Open *Alumni.aspx.cs*.</span></span> <span data-ttu-id="e5661-207">添加`using`语句的数据访问层和外部的处理程序`GridView`控件的`RowDataBound`事件：</span><span class="sxs-lookup"><span data-stu-id="e5661-207">Add a `using` statement for the data access layer and a handler for the outer `GridView` control's `RowDataBound` event:</span></span>

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample8.cs)]

<span data-ttu-id="e5661-208">此代码 databinds 内部`GridView`控件并使用`Donations`导航属性的当前行`Alumnus`实体。</span><span class="sxs-lookup"><span data-stu-id="e5661-208">This code databinds the inner `GridView` control using the `Donations` navigation property of the current row's `Alumnus` entity.</span></span>

<span data-ttu-id="e5661-209">运行页。</span><span class="sxs-lookup"><span data-stu-id="e5661-209">Run the page.</span></span>

[![I<span data-ttu-id="e5661-210">mage22]</span><span class="sxs-lookup"><span data-stu-id="e5661-210">mage22]</span></span>(what-s-new-in-the-entity-framework-4/_static/image36.png)](what-s-new-in-the-entity-framework-4/_static/image35.png)

<span data-ttu-id="e5661-211">（注意：此页包含在可下载的项目中，但以使其起作用，您必须在数据库中创建本地 SQL Server Express 实例;在数据库中不包含作为 *.mdf*中的文件*应用\_数据*文件夹。)</span><span class="sxs-lookup"><span data-stu-id="e5661-211">(Note: This page is included in the downloadable project, but to make it work you must create the database in your local SQL Server Express instance; the database isn't included as an *.mdf* file in the *App\_Data* folder.)</span></span>

<span data-ttu-id="e5661-212">有关使用实体框架实体数据模型功能的详细信息，请参阅[Entity Framework 4 模型优先](https://msdn.microsoft.com/data/ff830362.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e5661-212">For more information about using the model-first feature of the Entity Framework, see [Model-First in the Entity Framework 4](https://msdn.microsoft.com/data/ff830362.aspx).</span></span>

## <a name="poco-support"></a><span data-ttu-id="e5661-213">POCO 支持</span><span class="sxs-lookup"><span data-stu-id="e5661-213">POCO Support</span></span>

<span data-ttu-id="e5661-214">当使用域驱动设计方法时，您设计数据类表示数据和与业务域相关的行为。</span><span class="sxs-lookup"><span data-stu-id="e5661-214">When you use domain-driven design methodology, you design data classes that represent data and behavior that's relevant to the business domain.</span></span> <span data-ttu-id="e5661-215">这些类应是独立于用来存储任何特定技术 （保留） 数据;换而言之，它们应*持久性未知*。</span><span class="sxs-lookup"><span data-stu-id="e5661-215">These classes should be independent of any specific technology used to store (persist) the data; in other words, they should be *persistence ignorant*.</span></span> <span data-ttu-id="e5661-216">此外，持久性无感知可以使一个类容易进行单元测试因为单元测试项目可以使用的任何持久性技术是最方便进行测试。</span><span class="sxs-lookup"><span data-stu-id="e5661-216">Persistence ignorance can also make a class easier to unit test because the unit test project can use whatever persistence technology is most convenient for testing.</span></span> <span data-ttu-id="e5661-217">Entity Framework 的早期版本提供对持久化透明的支持有限，因为实体类必须继承自`EntityObject`类，并因此包含大量特定于实体框架的功能。</span><span class="sxs-lookup"><span data-stu-id="e5661-217">Earlier versions of the Entity Framework offered limited support for persistence ignorance because entity classes had to inherit from the `EntityObject` class and thus included a great deal of Entity Framework-specific functionality.</span></span>

<span data-ttu-id="e5661-218">Entity Framework 4 引入了使用不继承的实体类的功能`EntityObject`类，并因此为持久性未知。</span><span class="sxs-lookup"><span data-stu-id="e5661-218">The Entity Framework 4 introduces the ability to use entity classes that don't inherit from the `EntityObject` class and therefore are persistence ignorant.</span></span> <span data-ttu-id="e5661-219">在实体框架的上下文中，通常称为类，如这*普通旧 CLR 对象*（POCO 或 Poco）。</span><span class="sxs-lookup"><span data-stu-id="e5661-219">In the context of the Entity Framework, classes like this are typically called *plain-old CLR objects* (POCO, or POCOs).</span></span> <span data-ttu-id="e5661-220">您可以手动编写的 POCO 类或可以自动生成基于现有数据模型使用由实体框架提供的文本模板转换工具包 (T4) 模板。</span><span class="sxs-lookup"><span data-stu-id="e5661-220">You can write POCO classes manually, or you can automatically generate them based on an existing data model using Text Template Transformation Toolkit (T4) templates provided by the Entity Framework.</span></span>

<span data-ttu-id="e5661-221">有关使用 Poco 实体框架中的详细信息，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="e5661-221">For more information about using POCOs in the Entity Framework, see the following resources:</span></span>

- <span data-ttu-id="e5661-222">[使用 POCO 实体](https://msdn.microsoft.com/library/dd456853.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e5661-222">[Working with POCO Entities](https://msdn.microsoft.com/library/dd456853.aspx).</span></span> <span data-ttu-id="e5661-223">这是 Poco，概述以及指向其他文档的更多详细信息的 MSDN 文档。</span><span class="sxs-lookup"><span data-stu-id="e5661-223">This is an MSDN document that's an overview of POCOs, with links to other documents that have more detailed information.</span></span>
- <span data-ttu-id="e5661-224">[演练：实体框架的 POCO 模板](https://blogs.msdn.com/b/adonet/archive/2010/01/25/walkthrough-poco-template-for-the-entity-framework.aspx)这是实体框架开发团队，其中包含指向其他有关 Poco 的博客文章的一篇博客文章。</span><span class="sxs-lookup"><span data-stu-id="e5661-224">[Walkthrough: POCO Template for the Entity Framework](https://blogs.msdn.com/b/adonet/archive/2010/01/25/walkthrough-poco-template-for-the-entity-framework.aspx) This is a blog post from the Entity Framework development team, with links to other blog posts about POCOs.</span></span>

## <a name="code-first-development"></a><span data-ttu-id="e5661-225">代码优先开发</span><span class="sxs-lookup"><span data-stu-id="e5661-225">Code-First Development</span></span>

<span data-ttu-id="e5661-226">Entity Framework 4 中的 POCO 支持仍需要创建数据模型，并链接到数据模型的实体类。</span><span class="sxs-lookup"><span data-stu-id="e5661-226">POCO support in the Entity Framework 4 still requires that you create a data model and link your entity classes to the data model.</span></span> <span data-ttu-id="e5661-227">实体框架的下一个版本将包含一个称为功能*代码优先的开发*。</span><span class="sxs-lookup"><span data-stu-id="e5661-227">The next release of the Entity Framework will include a feature called *code-first development*.</span></span> <span data-ttu-id="e5661-228">此功能，可使用实体框架使用自己的 POCO 类而无需使用数据模型设计器或数据模型 XML 文件。</span><span class="sxs-lookup"><span data-stu-id="e5661-228">This feature enables you to use the Entity Framework with your own POCO classes without needing to use either the data model designer or a data model XML file.</span></span> <span data-ttu-id="e5661-229">(因此，此选项也已调用*仅限代码的*;*代码优先*并*仅限代码的*都引用相同的实体框架功能。)</span><span class="sxs-lookup"><span data-stu-id="e5661-229">(Therefore, this option has also been called *code-only*; *code-first* and *code-only* both refer to the same Entity Framework feature.)</span></span>

<span data-ttu-id="e5661-230">有关使用开发的代码优先方法的详细信息，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="e5661-230">For more information about using the code-first approach to development, see the following resources:</span></span>

- <span data-ttu-id="e5661-231">[代码优先的开发使用 Entity Framework 4](https://weblogs.asp.net/scottgu/archive/2010/07/16/code-first-development-with-entity-framework-4.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e5661-231">[Code-First Development with Entity Framework 4](https://weblogs.asp.net/scottgu/archive/2010/07/16/code-first-development-with-entity-framework-4.aspx).</span></span> <span data-ttu-id="e5661-232">这是由 Scott Guthrie 介绍代码优先开发的博客文章。</span><span class="sxs-lookup"><span data-stu-id="e5661-232">This is a blog post by Scott Guthrie introducing code-first development.</span></span>
- [<span data-ttu-id="e5661-233">实体框架开发团队博客-文章标记的 CodeOnly</span><span class="sxs-lookup"><span data-stu-id="e5661-233">Entity Framework Development Team Blog - posts tagged CodeOnly</span></span>](https://blogs.msdn.com/b/efdesign/archive/tags/codeonly/)
- [<span data-ttu-id="e5661-234">实体框架开发团队博客-文章标记 Code First</span><span class="sxs-lookup"><span data-stu-id="e5661-234">Entity Framework Development Team Blog - posts tagged Code First</span></span>](https://blogs.msdn.com/b/efdesign/archive/tags/code+first/)
- [<span data-ttu-id="e5661-235">MVC Music 商店教程-第 4 部分：模型和数据访问</span><span class="sxs-lookup"><span data-stu-id="e5661-235">MVC Music Store tutorial - Part 4: Models and Data Access</span></span>](../../../../mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-4.md)
- [<span data-ttu-id="e5661-236">开始使用 MVC 3-第 4 部分：Entity Framework 代码优先开发</span><span class="sxs-lookup"><span data-stu-id="e5661-236">Getting Started with MVC 3 - Part 4: Entity Framework Code-First Development</span></span>](../../../../mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-model.md)

<span data-ttu-id="e5661-237">此外，生成类似于 Contoso 大学应用程序的应用程序的新 MVC 代码的第一个教程预计在 2011 年春季发布 [https://asp.net/entity-framework/tutorials](../../../../entity-framework.md)</span><span class="sxs-lookup"><span data-stu-id="e5661-237">In addition, a new MVC Code-First tutorial that builds an application similar to the Contoso University application is projected to be published in the spring of 2011 at [https://asp.net/entity-framework/tutorials](../../../../entity-framework.md)</span></span>

## <a name="more-information"></a><span data-ttu-id="e5661-238">详细信息</span><span class="sxs-lookup"><span data-stu-id="e5661-238">More Information</span></span>

<span data-ttu-id="e5661-239">这将完成到实体框架和此继续与实体框架教程系列中新增的概述。</span><span class="sxs-lookup"><span data-stu-id="e5661-239">This completes the overview to what's new in the Entity Framework and this Continuing with the Entity Framework tutorial series.</span></span> <span data-ttu-id="e5661-240">有关 Entity Framework 4，这里没有涉及的新功能的详细信息，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="e5661-240">For more information about new features in the Entity Framework 4 that aren't covered here, see the following resources:</span></span>

- <span data-ttu-id="e5661-241">[What's New in ADO.NET](https://msdn.microsoft.com/library/ex6y04yf.aspx) MSDN 上的 Entity Framework 版本 4 中的新增功能的主题。</span><span class="sxs-lookup"><span data-stu-id="e5661-241">[What's New in ADO.NET](https://msdn.microsoft.com/library/ex6y04yf.aspx) MSDN topic on new features in version 4 of the Entity Framework.</span></span>
- <span data-ttu-id="e5661-242">[宣布发布 Entity Framework 4](https://blogs.msdn.com/b/efdesign/archive/2010/04/12/announcing-the-release-of-entity-framework-4.aspx)版本 4 中的新增功能有关的实体框架开发团队的博客文章。</span><span class="sxs-lookup"><span data-stu-id="e5661-242">[Announcing the release of Entity Framework 4](https://blogs.msdn.com/b/efdesign/archive/2010/04/12/announcing-the-release-of-entity-framework-4.aspx) The Entity Framework development team's blog post about new features in version 4.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="e5661-243">上一个</span><span class="sxs-lookup"><span data-stu-id="e5661-243">Previous</span></span>](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application.md)

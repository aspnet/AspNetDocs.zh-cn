---
uid: mvc/overview/older-versions-1/models-data/creating-model-classes-with-the-entity-framework-cs
title: 使用实体框架 （C#） 创建模型类 |微软文档
author: rick-anderson
description: 在本教程中，您将了解如何将 ASP.NET MVC 与 Microsoft 实体框架一起使用。 您将了解如何使用实体向导创建ADO.NET实体 Da...
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 61644169-e8b1-45dd-bf96-9c2301b69879
msc.legacyurl: /mvc/overview/older-versions-1/models-data/creating-model-classes-with-the-entity-framework-cs
msc.type: authoredcontent
ms.openlocfilehash: 716d34167258b1005b25b1cd11bfaa6d80763320
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542659"
---
# <a name="creating-model-classes-with-the-entity-framework-c"></a><span data-ttu-id="b59ab-104">使用 Entity Framework 创建模型类 (C#)</span><span class="sxs-lookup"><span data-stu-id="b59ab-104">Creating Model Classes with the Entity Framework (C#)</span></span>

<span data-ttu-id="b59ab-105">由[微软](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="b59ab-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="b59ab-106">在本教程中，您将了解如何将 ASP.NET MVC 与 Microsoft 实体框架一起使用。</span><span class="sxs-lookup"><span data-stu-id="b59ab-106">In this tutorial, you learn how to use ASP.NET MVC with the Microsoft Entity Framework.</span></span> <span data-ttu-id="b59ab-107">您将了解如何使用实体向导创建ADO.NET实体数据模型。</span><span class="sxs-lookup"><span data-stu-id="b59ab-107">You learn how to use the Entity Wizard to create an ADO.NET Entity Data Model.</span></span> <span data-ttu-id="b59ab-108">在本教程中，我们将构建一个 Web 应用程序，说明如何使用实体框架选择、插入、更新和删除数据库数据。</span><span class="sxs-lookup"><span data-stu-id="b59ab-108">Over the course of this tutorial, we build a web application that illustrates how to select, insert, update, and delete database data by using the Entity Framework.</span></span>

<span data-ttu-id="b59ab-109">本教程的目的是说明如何在构建ASP.NET MVC 应用程序时使用 Microsoft 实体框架创建数据访问类。</span><span class="sxs-lookup"><span data-stu-id="b59ab-109">The goal of this tutorial is to explain how you can create data access classes using the Microsoft Entity Framework when building an ASP.NET MVC application.</span></span> <span data-ttu-id="b59ab-110">本教程假定之前对 Microsoft 实体框架没有了解。</span><span class="sxs-lookup"><span data-stu-id="b59ab-110">This tutorial assumes no previous knowledge of the Microsoft Entity Framework.</span></span> <span data-ttu-id="b59ab-111">在本教程结束时，您将了解如何使用实体框架来选择、插入、更新和删除数据库记录。</span><span class="sxs-lookup"><span data-stu-id="b59ab-111">By the end of this tutorial, you'll understand how to use the Entity Framework to select, insert, update, and delete database records.</span></span>

<span data-ttu-id="b59ab-112">Microsoft 实体框架是一个对象关系映射 （O/RM） 工具，使您能够从数据库自动生成数据访问层。</span><span class="sxs-lookup"><span data-stu-id="b59ab-112">The Microsoft Entity Framework is an Object Relational Mapping (O/RM) tool that enables you to generate a data access layer from a database automatically.</span></span> <span data-ttu-id="b59ab-113">实体框架使您能够避免手动构建数据访问类的繁琐工作。</span><span class="sxs-lookup"><span data-stu-id="b59ab-113">The Entity Framework enables you to avoid the tedious work of building your data access classes by hand.</span></span>

<span data-ttu-id="b59ab-114">为了说明如何使用微软实体框架进行ASP.NET MVC，我们将构建一个简单的示例应用程序。</span><span class="sxs-lookup"><span data-stu-id="b59ab-114">In order to illustrate how you can use the Microsoft Entity Framework with ASP.NET MVC, we'll build a simple sample application.</span></span> <span data-ttu-id="b59ab-115">我们将创建一个影片数据库应用程序，使您能够显示和编辑影片数据库记录。</span><span class="sxs-lookup"><span data-stu-id="b59ab-115">We'll create a Movie Database application that enables you to display and edit movie database records.</span></span>

<span data-ttu-id="b59ab-116">本教程假定您拥有 Visual Studio 2008 或带 Service Pack 1 的可视化 Web 开发人员 2008。</span><span class="sxs-lookup"><span data-stu-id="b59ab-116">This tutorial assumes that you have Visual Studio 2008 or Visual Web Developer 2008 with Service Pack 1.</span></span> <span data-ttu-id="b59ab-117">您需要服务包 1 才能使用实体框架。</span><span class="sxs-lookup"><span data-stu-id="b59ab-117">You need Service Pack 1 in order to use the Entity Framework.</span></span> <span data-ttu-id="b59ab-118">您可以通过以下地址下载 Visual Studio 2008 服务包 1 或带服务包 1 的可视化 Web 开发人员：</span><span class="sxs-lookup"><span data-stu-id="b59ab-118">You can download Visual Studio 2008 Service Pack 1 or Visual Web Developer with Service Pack 1 from the following address:</span></span>

> [https://www.asp.net/downloads/](https://www.asp.net/downloads)

> [!NOTE] 
> 
> <span data-ttu-id="b59ab-119">ASP.NET MVC 和 Microsoft 实体框架之间没有基本联系。</span><span class="sxs-lookup"><span data-stu-id="b59ab-119">There is no essential connection between ASP.NET MVC and the Microsoft Entity Framework.</span></span> <span data-ttu-id="b59ab-120">实体框架有几个替代方法可用于mVCASP.NET。</span><span class="sxs-lookup"><span data-stu-id="b59ab-120">There are several alternatives to the Entity Framework that you can use with ASP.NET MVC.</span></span> <span data-ttu-id="b59ab-121">例如，您可以使用其他 O/RM 工具（如 Microsoft LINQ 到 SQL、NHibernate 或 SubSonic）构建 MVC 模型类。</span><span class="sxs-lookup"><span data-stu-id="b59ab-121">For example, you can build your MVC Model classes using other O/RM tools such as Microsoft LINQ to SQL, NHibernate, or SubSonic.</span></span>

## <a name="creating-the-movie-sample-database"></a><span data-ttu-id="b59ab-122">创建影片示例数据库</span><span class="sxs-lookup"><span data-stu-id="b59ab-122">Creating the Movie Sample Database</span></span>

<span data-ttu-id="b59ab-123">影片数据库应用程序使用名为"Movie"的数据库表，其中包含以下列：</span><span class="sxs-lookup"><span data-stu-id="b59ab-123">The Movie Database application uses a database table named Movies that contains the following columns:</span></span>

| <span data-ttu-id="b59ab-124">列名</span><span class="sxs-lookup"><span data-stu-id="b59ab-124">Column Name</span></span> | <span data-ttu-id="b59ab-125">数据类型</span><span class="sxs-lookup"><span data-stu-id="b59ab-125">Data Type</span></span> | <span data-ttu-id="b59ab-126">允许 Nulls？</span><span class="sxs-lookup"><span data-stu-id="b59ab-126">Allow Nulls?</span></span> | <span data-ttu-id="b59ab-127">是主键吗？</span><span class="sxs-lookup"><span data-stu-id="b59ab-127">Is Primary Key?</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b59ab-128">ID</span><span class="sxs-lookup"><span data-stu-id="b59ab-128">Id</span></span> | <span data-ttu-id="b59ab-129">int</span><span class="sxs-lookup"><span data-stu-id="b59ab-129">int</span></span> | <span data-ttu-id="b59ab-130">False</span><span class="sxs-lookup"><span data-stu-id="b59ab-130">False</span></span> | <span data-ttu-id="b59ab-131">True</span><span class="sxs-lookup"><span data-stu-id="b59ab-131">True</span></span> |
| <span data-ttu-id="b59ab-132">标题</span><span class="sxs-lookup"><span data-stu-id="b59ab-132">Title</span></span> | <span data-ttu-id="b59ab-133">恩瓦尔查尔 （100）</span><span class="sxs-lookup"><span data-stu-id="b59ab-133">nvarchar(100)</span></span> | <span data-ttu-id="b59ab-134">False</span><span class="sxs-lookup"><span data-stu-id="b59ab-134">False</span></span> | <span data-ttu-id="b59ab-135">False</span><span class="sxs-lookup"><span data-stu-id="b59ab-135">False</span></span> |
| <span data-ttu-id="b59ab-136">导演</span><span class="sxs-lookup"><span data-stu-id="b59ab-136">Director</span></span> | <span data-ttu-id="b59ab-137">恩瓦尔查尔 （100）</span><span class="sxs-lookup"><span data-stu-id="b59ab-137">nvarchar(100)</span></span> | <span data-ttu-id="b59ab-138">False</span><span class="sxs-lookup"><span data-stu-id="b59ab-138">False</span></span> | <span data-ttu-id="b59ab-139">False</span><span class="sxs-lookup"><span data-stu-id="b59ab-139">False</span></span> |

<span data-ttu-id="b59ab-140">您可以按照以下步骤将此表添加到ASP.NET MVC 项目中：</span><span class="sxs-lookup"><span data-stu-id="b59ab-140">You can add this table to an ASP.NET MVC project by following these steps:</span></span>

1. <span data-ttu-id="b59ab-141">右键单击"解决方案\_资源管理器"窗口中的应用数据文件夹，然后选择菜单选项 **"添加，新建项目"。**</span><span class="sxs-lookup"><span data-stu-id="b59ab-141">Right-click the App\_Data folder in the Solution Explorer window and select the menu option **Add, New Item.**</span></span>
2. <span data-ttu-id="b59ab-142">在 **"添加新项目"** 对话框中，选择**SQL Server 数据库**，为数据库指定名称 MoviesDB.mdf，然后单击"**添加**"按钮。</span><span class="sxs-lookup"><span data-stu-id="b59ab-142">From the **Add New Item** dialog box, select **SQL Server Database**, give the database the name MoviesDB.mdf, and click the **Add** button.</span></span>
3. <span data-ttu-id="b59ab-143">双击 MoviesDB.mdf 文件以打开服务器资源管理器/数据库资源管理器窗口。</span><span class="sxs-lookup"><span data-stu-id="b59ab-143">Double-click the MoviesDB.mdf file to open the Server Explorer/Database Explorer window.</span></span>
4. <span data-ttu-id="b59ab-144">展开 MoviesDB.mdf 数据库连接，右键单击"表"文件夹，然后选择菜单选项 **"添加新表**"。</span><span class="sxs-lookup"><span data-stu-id="b59ab-144">Expand the MoviesDB.mdf database connection, right-click the Tables folder, and select the menu option **Add New Table**.</span></span>
5. <span data-ttu-id="b59ab-145">在表设计器中，添加 Id、标题和控制器列。</span><span class="sxs-lookup"><span data-stu-id="b59ab-145">In the Table Designer, add the Id, Title, and Director columns.</span></span>
6. <span data-ttu-id="b59ab-146">单击 **"保存**"按钮（它有软盘的图标）以保存新表的名称"电影"。</span><span class="sxs-lookup"><span data-stu-id="b59ab-146">Click the **Save** button (it has the icon of the floppy) to save the new table with the name Movies.</span></span>

<span data-ttu-id="b59ab-147">创建"影片"数据库表后，应向该表添加一些示例数据。</span><span class="sxs-lookup"><span data-stu-id="b59ab-147">After you create the Movies database table, you should add some sample data to the table.</span></span> <span data-ttu-id="b59ab-148">右键单击"影片"表并选择菜单选项 **"显示表数据**"。</span><span class="sxs-lookup"><span data-stu-id="b59ab-148">Right-click the Movies table and select the menu option **Show Table Data**.</span></span> <span data-ttu-id="b59ab-149">您可以将假影片数据输入显示的网格中。</span><span class="sxs-lookup"><span data-stu-id="b59ab-149">You can enter fake movie data into the grid that appears.</span></span>

## <a name="creating-the-adonet-entity-data-model"></a><span data-ttu-id="b59ab-150">创建ADO.NET实体数据模型</span><span class="sxs-lookup"><span data-stu-id="b59ab-150">Creating the ADO.NET Entity Data Model</span></span>

<span data-ttu-id="b59ab-151">为了使用实体框架，您需要创建实体数据模型。</span><span class="sxs-lookup"><span data-stu-id="b59ab-151">In order to use the Entity Framework, you need to create an Entity Data Model.</span></span> <span data-ttu-id="b59ab-152">您可以使用可视化工作室*实体数据模型向导*从数据库自动生成实体数据模型。</span><span class="sxs-lookup"><span data-stu-id="b59ab-152">You can take advantage of the Visual Studio *Entity Data Model Wizard* to generate an Entity Data Model from a database automatically.</span></span>

<span data-ttu-id="b59ab-153">执行以下步骤:</span><span class="sxs-lookup"><span data-stu-id="b59ab-153">Follow these steps:</span></span>

1. <span data-ttu-id="b59ab-154">右键单击"解决方案资源管理器"窗口中的"模型"文件夹，然后选择菜单选项 **"添加，新项目**"。</span><span class="sxs-lookup"><span data-stu-id="b59ab-154">Right-click the Models folder in the Solution Explorer window and select the menu option **Add, New Item**.</span></span>
2. <span data-ttu-id="b59ab-155">在"**添加新项目"** 对话框中，选择"数据"类别（参见图 1）。</span><span class="sxs-lookup"><span data-stu-id="b59ab-155">In the **Add New Item** dialog, select the Data category (see Figure 1).</span></span>
3. <span data-ttu-id="b59ab-156">选择**ADO.NET实体数据模型**模板，为实体数据模型指定名称"电影 DBModel.edmx"，然后单击 **"添加**"按钮。</span><span class="sxs-lookup"><span data-stu-id="b59ab-156">Select the **ADO.NET Entity Data Model** template, give the Entity Data Model the name MoviesDBModel.edmx, and click the **Add** button.</span></span> <span data-ttu-id="b59ab-157">单击 **"添加**"按钮将启动"数据模型向导"。</span><span class="sxs-lookup"><span data-stu-id="b59ab-157">Clicking the **Add** button launches the Data Model Wizard.</span></span>
4. <span data-ttu-id="b59ab-158">在 **"选择模型内容"** 步骤中，选择"**从数据库生成**"选项，然后单击 **"下一步**"按钮（参见图 2）。</span><span class="sxs-lookup"><span data-stu-id="b59ab-158">In the **Choose Model Contents** step, choose the **Generate from a database** option and click the **Next** button (see Figure 2).</span></span>
5. <span data-ttu-id="b59ab-159">在 **"选择数据连接**"步骤中，选择 MoviesDB.mdf 数据库连接，输入实体连接设置名称"电影 DB实体"，然后单击 **"下一步**"按钮（参见图 3）。</span><span class="sxs-lookup"><span data-stu-id="b59ab-159">In the **Choose Your Data Connection** step, select the MoviesDB.mdf database connection, enter the entities connection settings name MoviesDBEntities, and click the **Next** button (see Figure 3).</span></span>
6. <span data-ttu-id="b59ab-160">在 **"选择数据库对象**"步骤中，选择"影片数据库"表并单击 **"完成"** 按钮（参见图 4）。</span><span class="sxs-lookup"><span data-stu-id="b59ab-160">In the **Choose Your Database Objects** step, select the Movie database table and click the **Finish** button (see Figure 4).</span></span>

<span data-ttu-id="b59ab-161">完成这些步骤后，将打开ADO.NET实体数据模型设计器（实体设计器）。</span><span class="sxs-lookup"><span data-stu-id="b59ab-161">After you complete these steps, the ADO.NET Entity Data Model Designer (Entity Designer) opens.</span></span>

<span data-ttu-id="b59ab-162">**图 1 = 创建新的实体数据模型**</span><span class="sxs-lookup"><span data-stu-id="b59ab-162">**Figure 1 – Creating a new Entity Data Model**</span></span>

![clip_image002](creating-model-classes-with-the-entity-framework-cs/_static/image1.jpg)

<span data-ttu-id="b59ab-164">**图 2 = 选择模型内容步骤**</span><span class="sxs-lookup"><span data-stu-id="b59ab-164">**Figure 2 – Choose Model Contents Step**</span></span>

![clip_image004](creating-model-classes-with-the-entity-framework-cs/_static/image2.jpg)

<span data-ttu-id="b59ab-166">**图 3 = 选择数据连接**</span><span class="sxs-lookup"><span data-stu-id="b59ab-166">**Figure 3 – Choose Your Data Connection**</span></span>

![clip_image006](creating-model-classes-with-the-entity-framework-cs/_static/image3.jpg)

<span data-ttu-id="b59ab-168">**图 4 = 选择数据库对象**</span><span class="sxs-lookup"><span data-stu-id="b59ab-168">**Figure 4 – Choose Your Database Objects**</span></span>

![clip_image008](creating-model-classes-with-the-entity-framework-cs/_static/image4.jpg)

#### <a name="modifying-the-adonet-entity-data-model"></a><span data-ttu-id="b59ab-170">修改ADO.NET实体数据模型</span><span class="sxs-lookup"><span data-stu-id="b59ab-170">Modifying the ADO.NET Entity Data Model</span></span>

<span data-ttu-id="b59ab-171">创建实体数据模型后，可以使用实体设计器修改模型（参见图 5）。</span><span class="sxs-lookup"><span data-stu-id="b59ab-171">After you create an Entity Data Model, you can modify the model by taking advantage of the Entity Designer (see Figure 5).</span></span> <span data-ttu-id="b59ab-172">您可以随时通过双击解决方案资源管理器窗口中的"模型"文件夹中的"电影 DBModel.edmx 文件"来打开实体设计器。</span><span class="sxs-lookup"><span data-stu-id="b59ab-172">You can open the Entity Designer at any time by double-clicking the MoviesDBModel.edmx file contained in the Models folder within the Solution Explorer window.</span></span>

<span data-ttu-id="b59ab-173">**图 5 = ADO.NET实体数据模型设计器**</span><span class="sxs-lookup"><span data-stu-id="b59ab-173">**Figure 5 – The ADO.NET Entity Data Model Designer**</span></span>

![clip_image010](creating-model-classes-with-the-entity-framework-cs/_static/image5.jpg)

<span data-ttu-id="b59ab-175">例如，可以使用实体设计器更改实体模型数据向导生成的类的名称。</span><span class="sxs-lookup"><span data-stu-id="b59ab-175">For example, you can use the Entity Designer to change the names of the classes that the Entity Model Data Wizard generates.</span></span> <span data-ttu-id="b59ab-176">向导创建了名为"电影"的新数据访问类。</span><span class="sxs-lookup"><span data-stu-id="b59ab-176">The Wizard created a new data access class named Movies.</span></span> <span data-ttu-id="b59ab-177">换句话说，向导为类指定与数据库表相同的名称。</span><span class="sxs-lookup"><span data-stu-id="b59ab-177">In other words, the Wizard gave the class the very same name as the database table.</span></span> <span data-ttu-id="b59ab-178">由于我们将使用此类来表示特定的"影片"实例，因此应将类从"影片"重命名为"影片"。</span><span class="sxs-lookup"><span data-stu-id="b59ab-178">Because we will use this class to represent a particular Movie instance, we should rename the class from Movies to Movie.</span></span>

<span data-ttu-id="b59ab-179">如果要重命名实体类，可以双击实体设计器中的类名称并输入新名称（参见图 6）。</span><span class="sxs-lookup"><span data-stu-id="b59ab-179">If you want to rename an entity class, you can double-click on the class name in the Entity Designer and enter a new name (see Figure 6).</span></span> <span data-ttu-id="b59ab-180">或者，您可以在实体设计器中选择实体后，在"属性"窗口中更改实体的名称。</span><span class="sxs-lookup"><span data-stu-id="b59ab-180">Alternatively, you can change the name of an entity in the Properties window after selecting an entity in the Entity Designer.</span></span>

<span data-ttu-id="b59ab-181">**图 6 = 更改实体名称**</span><span class="sxs-lookup"><span data-stu-id="b59ab-181">**Figure 6 – Changing an entity name**</span></span>

![clip_image012](creating-model-classes-with-the-entity-framework-cs/_static/image6.jpg)

<span data-ttu-id="b59ab-183">请记住，通过单击"保存"按钮（软盘的图标）进行修改后保存实体数据模型。</span><span class="sxs-lookup"><span data-stu-id="b59ab-183">Remember to save your Entity Data Model after making a modification by clicking the Save button (the icon of the floppy disk).</span></span> <span data-ttu-id="b59ab-184">在后台，实体设计器生成一组 C# 类。</span><span class="sxs-lookup"><span data-stu-id="b59ab-184">Behind the scenes, the Entity Designer generates a set of C# classes.</span></span> <span data-ttu-id="b59ab-185">您可以通过从解决方案资源管理器窗口中打开MoviesDBModel.Designer.cs文件来查看这些类。</span><span class="sxs-lookup"><span data-stu-id="b59ab-185">You can view these classes by opening the MoviesDBModel.Designer.cs file from the Solution Explorer window.</span></span>

<span data-ttu-id="b59ab-186">不要修改Designer.cs文件中的代码，因为下次使用实体设计器时，您的更改将被覆盖。</span><span class="sxs-lookup"><span data-stu-id="b59ab-186">Don't modify the code in the Designer.cs file since your changes will be overwritten the next time you use the Entity Designer.</span></span> <span data-ttu-id="b59ab-187">如果要扩展Designer.cs文件中定义的实体类的功能，则可以在单独的文件中创建*部分类*。</span><span class="sxs-lookup"><span data-stu-id="b59ab-187">If you want to extend the functionality of the entity classes defined in the Designer.cs file then you can create *partial classes* in separate files.</span></span>

#### <a name="selecting-database-records-with-the-entity-framework"></a><span data-ttu-id="b59ab-188">使用实体框架选择数据库记录</span><span class="sxs-lookup"><span data-stu-id="b59ab-188">Selecting Database Records with the Entity Framework</span></span>

<span data-ttu-id="b59ab-189">让我们通过创建显示影片记录列表的页面开始构建影片数据库应用程序。</span><span class="sxs-lookup"><span data-stu-id="b59ab-189">Let's start building our Movie Database application by creating a page that displays a list of movie records.</span></span> <span data-ttu-id="b59ab-190">清单 1 中的主控制器公开名为 Index（） 的操作。</span><span class="sxs-lookup"><span data-stu-id="b59ab-190">The Home controller in Listing 1 exposes an action named Index().</span></span> <span data-ttu-id="b59ab-191">索引（） 操作利用实体框架从影片数据库表中返回所有影片记录。</span><span class="sxs-lookup"><span data-stu-id="b59ab-191">The Index() action returns all of the movie records from the Movie database table by taking advantage of the Entity Framework.</span></span>

<span data-ttu-id="b59ab-192">**清单1 = 控制器\主控制器.cs**</span><span class="sxs-lookup"><span data-stu-id="b59ab-192">**Listing 1 – Controllers\HomeController.cs**</span></span>

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample1.cs)]

<span data-ttu-id="b59ab-193">请注意，清单 1 中的控制器包括一个构造函数。</span><span class="sxs-lookup"><span data-stu-id="b59ab-193">Notice that the controller in Listing 1 includes a constructor.</span></span> <span data-ttu-id="b59ab-194">构造函数初始化名为\_db 的类级字段。</span><span class="sxs-lookup"><span data-stu-id="b59ab-194">The constructor initializes a class-level field named \_db.</span></span> <span data-ttu-id="b59ab-195">db\_字段表示由 Microsoft 实体框架生成的数据库实体。</span><span class="sxs-lookup"><span data-stu-id="b59ab-195">The \_db field represents the database entities generated by the Microsoft Entity Framework.</span></span> <span data-ttu-id="b59ab-196">db\_字段是实体设计器生成的 MoviesDBEntity 类的实例。</span><span class="sxs-lookup"><span data-stu-id="b59ab-196">The \_db field is an instance of the MoviesDBEntities class that was generated by the Entity Designer.</span></span>

<span data-ttu-id="b59ab-197">为了在主控制器中使用MoviesDBEntity类，必须导入 MovieEntityApp.models 命名空间 *（MVCProjectName*）。型号）。</span><span class="sxs-lookup"><span data-stu-id="b59ab-197">In order to use theMoviesDBEntities class in the Home controller, you must import the MovieEntityApp.Models namespace (*MVCProjectName*.Models).</span></span>

<span data-ttu-id="b59ab-198">db\_字段在 Index（） 操作中使用，以从"影片"数据库表中检索记录。</span><span class="sxs-lookup"><span data-stu-id="b59ab-198">The \_db field is used within the Index() action to retrieve the records from the Movies database table.</span></span> <span data-ttu-id="b59ab-199">表达式\_db。MovieSet 表示"影片"数据库表中的所有记录。</span><span class="sxs-lookup"><span data-stu-id="b59ab-199">The expression \_db.MovieSet represents all of the records from the Movies database table.</span></span> <span data-ttu-id="b59ab-200">ToList（） 方法用于将影片集转换为影片对象的泛型集合（列表&lt;影片）。&gt;</span><span class="sxs-lookup"><span data-stu-id="b59ab-200">The ToList() method is used to convert the set of movies into a generic collection of Movie objects (List&lt;Movie&gt;).</span></span>

<span data-ttu-id="b59ab-201">影片记录在 LINQ 到实体的帮助下检索。</span><span class="sxs-lookup"><span data-stu-id="b59ab-201">The movie records are retrieved with the help of LINQ to Entities.</span></span> <span data-ttu-id="b59ab-202">清单 1 中的 Index（） 操作使用 LINQ*方法语法*来检索数据库记录集。</span><span class="sxs-lookup"><span data-stu-id="b59ab-202">The Index() action in Listing 1 uses LINQ *method syntax* to retrieve the set of database records.</span></span> <span data-ttu-id="b59ab-203">如果您愿意，可以使用 LINQ*查询语法*。</span><span class="sxs-lookup"><span data-stu-id="b59ab-203">If you prefer, you can use LINQ *query syntax* instead.</span></span> <span data-ttu-id="b59ab-204">以下两个语句执行相同的操作：</span><span class="sxs-lookup"><span data-stu-id="b59ab-204">The following two statements do the very same thing:</span></span>

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample2.cs)]

<span data-ttu-id="b59ab-205">使用您认为最直观的 LINQ 语法（方法语法或查询语法）。</span><span class="sxs-lookup"><span data-stu-id="b59ab-205">Use whichever LINQ syntax – method syntax or query syntax – that you find most intuitive.</span></span> <span data-ttu-id="b59ab-206">这两种方法在性能上没有差别 ，唯一的区别是风格。</span><span class="sxs-lookup"><span data-stu-id="b59ab-206">There is no difference in performance between the two approaches – the only difference is style.</span></span>

<span data-ttu-id="b59ab-207">清单 2 中的视图用于显示影片记录。</span><span class="sxs-lookup"><span data-stu-id="b59ab-207">The view in Listing 2 is used to display the movie records.</span></span>

<span data-ttu-id="b59ab-208">**清单 2 = 视图\home_Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="b59ab-208">**Listing 2 – Views\Home\Index.aspx**</span></span>

[!code-aspx[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample3.aspx)]

<span data-ttu-id="b59ab-209">清单 2 中的视图包含一个**foreach**循环，该循环循环循环遍历每个影片记录并显示影片记录的标题和导演属性的值。</span><span class="sxs-lookup"><span data-stu-id="b59ab-209">The view in Listing 2 contains a **foreach** loop that iterates through each movie record and displays the values of the movie record's Title and Director properties.</span></span> <span data-ttu-id="b59ab-210">请注意，每个记录旁边都会显示"编辑"和"删除"链接。</span><span class="sxs-lookup"><span data-stu-id="b59ab-210">Notice that an Edit and Delete link is displayed next to each record.</span></span> <span data-ttu-id="b59ab-211">此外，视图底部还显示"添加影片"链接（参见图 7）。</span><span class="sxs-lookup"><span data-stu-id="b59ab-211">Furthermore, an Add Movie link appears at the bottom of the view (see Figure 7).</span></span>

<span data-ttu-id="b59ab-212">**图 7 = 索引视图**</span><span class="sxs-lookup"><span data-stu-id="b59ab-212">**Figure 7 – The Index view**</span></span>

![clip_image014](creating-model-classes-with-the-entity-framework-cs/_static/image7.jpg)

<span data-ttu-id="b59ab-214">索引视图是*键入的视图*。</span><span class="sxs-lookup"><span data-stu-id="b59ab-214">The Index view is a *typed view*.</span></span> <span data-ttu-id="b59ab-215">索引视图包括一个&lt;%@&gt; Page % 指令，该指令具有*继承*属性，该属性将模型属性转换为影片对象（列表&lt;影片）的强力类型泛型列表集合。</span><span class="sxs-lookup"><span data-stu-id="b59ab-215">The Index view includes a &lt;%@ Page %&gt; directive with an *Inherits* attribute that casts the Model property to a strongly typed generic List collection of Movie objects (List&lt;Movie).</span></span>

## <a name="inserting-database-records-with-the-entity-framework"></a><span data-ttu-id="b59ab-216">将数据库记录插入实体框架</span><span class="sxs-lookup"><span data-stu-id="b59ab-216">Inserting Database Records with the Entity Framework</span></span>

<span data-ttu-id="b59ab-217">您可以使用实体框架轻松将新记录插入到数据库表中。</span><span class="sxs-lookup"><span data-stu-id="b59ab-217">You can use the Entity Framework to make it easy to insert new records into a database table.</span></span> <span data-ttu-id="b59ab-218">清单3包含添加到主控制器类的两个新操作，可用于将新记录插入到 Movie 数据库表中。</span><span class="sxs-lookup"><span data-stu-id="b59ab-218">Listing 3 contains two new actions added to the Home controller class that you can use to insert new records into the Movie database table.</span></span>

<span data-ttu-id="b59ab-219">**清单3 = 控制器\主控制器.cs（添加方法）**</span><span class="sxs-lookup"><span data-stu-id="b59ab-219">**Listing 3 – Controllers\HomeController.cs (Add methods)**</span></span>

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample4.cs)]

<span data-ttu-id="b59ab-220">第一个 Add（） 操作仅返回视图。</span><span class="sxs-lookup"><span data-stu-id="b59ab-220">The first Add() action simply returns a view.</span></span> <span data-ttu-id="b59ab-221">该视图包含用于添加新影片数据库记录的窗体（参见图 8）。</span><span class="sxs-lookup"><span data-stu-id="b59ab-221">The view contains a form for adding a new movie database record (see Figure 8).</span></span> <span data-ttu-id="b59ab-222">提交表单时，将调用第二个 Add（） 操作。</span><span class="sxs-lookup"><span data-stu-id="b59ab-222">When you submit the form, the second Add() action is invoked.</span></span>

<span data-ttu-id="b59ab-223">请注意，第二个 Add（） 操作用 AcceptVerbs 属性进行修饰。</span><span class="sxs-lookup"><span data-stu-id="b59ab-223">Notice that the second Add() action is decorated with the AcceptVerbs attribute.</span></span> <span data-ttu-id="b59ab-224">仅当执行 HTTP POST 操作时，才能调用此操作。</span><span class="sxs-lookup"><span data-stu-id="b59ab-224">This action can be invoked only when performing an HTTP POST operation.</span></span> <span data-ttu-id="b59ab-225">换句话说，此操作只能在发布 HTML 窗体时调用。</span><span class="sxs-lookup"><span data-stu-id="b59ab-225">In other words, this action can only be invoked when posting an HTML form.</span></span>

<span data-ttu-id="b59ab-226">第二个 Add（） 操作在 ASP.NET MVC TryUpdateModel（） 方法的帮助下创建实体框架影片类的新实例。</span><span class="sxs-lookup"><span data-stu-id="b59ab-226">The second Add() action creates a new instance of the Entity Framework Movie class with the help of the ASP.NET MVC TryUpdateModel() method.</span></span> <span data-ttu-id="b59ab-227">TryUpdateModel（） 方法获取传递给 Add（） 方法的窗体集合中的字段，并将这些 HTML 表单字段的值分配给 Movie 类。</span><span class="sxs-lookup"><span data-stu-id="b59ab-227">The TryUpdateModel() method takes the fields in the FormCollection passed to the Add() method and assigns the values of these HTML form fields to the Movie class.</span></span>

<span data-ttu-id="b59ab-228">使用实体框架时，在使用 TryUpdateModel 或 UpdateModel 方法更新实体类的属性时，必须提供属性的"白名单"。</span><span class="sxs-lookup"><span data-stu-id="b59ab-228">When using the Entity Framework, you must supply a "white list" of properties when using the TryUpdateModel or UpdateModel methods to update the properties of an entity class.</span></span>

<span data-ttu-id="b59ab-229">接下来，Add（） 操作执行一些简单的表单验证。</span><span class="sxs-lookup"><span data-stu-id="b59ab-229">Next, the Add() action performs some simple form validation.</span></span> <span data-ttu-id="b59ab-230">该操作验证"标题"和"控制器"属性是否具有值。</span><span class="sxs-lookup"><span data-stu-id="b59ab-230">The action verifies that both the Title and Director properties have values.</span></span> <span data-ttu-id="b59ab-231">如果存在验证错误，则会向 ModelState 添加验证错误消息。</span><span class="sxs-lookup"><span data-stu-id="b59ab-231">If there is a validation error, then a validation error message is added to ModelState.</span></span>

<span data-ttu-id="b59ab-232">如果没有验证错误，则在实体框架的帮助下，将新的影片记录添加到"电影"数据库表。</span><span class="sxs-lookup"><span data-stu-id="b59ab-232">If there are no validation errors then a new movie record is added to the Movies database table with the help of the Entity Framework.</span></span> <span data-ttu-id="b59ab-233">新记录将添加到数据库中，并带有以下两行代码：</span><span class="sxs-lookup"><span data-stu-id="b59ab-233">The new record is added to the database with the following two lines of code:</span></span>

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample5.cs)]

<span data-ttu-id="b59ab-234">第一行代码将新的影片实体添加到实体框架正在跟踪的影片集中。</span><span class="sxs-lookup"><span data-stu-id="b59ab-234">The first line of code adds the new Movie entity to the set of movies being tracked by the Entity Framework.</span></span> <span data-ttu-id="b59ab-235">第二行代码将保存对被跟踪回基础数据库的"电影"所做的任何更改。</span><span class="sxs-lookup"><span data-stu-id="b59ab-235">The second line of code saves whatever changes have been made to the Movies being tracked back to the underlying database.</span></span>

<span data-ttu-id="b59ab-236">**图 8 = 添加视图**</span><span class="sxs-lookup"><span data-stu-id="b59ab-236">**Figure 8 – The Add view**</span></span>

![clip_image016](creating-model-classes-with-the-entity-framework-cs/_static/image8.jpg)

#### <a name="updating-database-records-with-the-entity-framework"></a><span data-ttu-id="b59ab-238">使用实体框架更新数据库记录</span><span class="sxs-lookup"><span data-stu-id="b59ab-238">Updating Database Records with the Entity Framework</span></span>

<span data-ttu-id="b59ab-239">您可以采用几乎相同的方法，使用实体框架编辑数据库记录，就像我们刚才采用的方法插入新的数据库记录一样。</span><span class="sxs-lookup"><span data-stu-id="b59ab-239">You can follow almost the same approach to edit a database record with the Entity Framework as the approach that we just followed to insert a new database record.</span></span> <span data-ttu-id="b59ab-240">清单4包含两个名为 Edit（） 的新控制器操作。</span><span class="sxs-lookup"><span data-stu-id="b59ab-240">Listing 4 contains two new controller actions named Edit().</span></span> <span data-ttu-id="b59ab-241">第一个 Edit（） 操作返回用于编辑影片记录的 HTML 窗体。</span><span class="sxs-lookup"><span data-stu-id="b59ab-241">The first Edit() action returns an HTML form for editing a movie record.</span></span> <span data-ttu-id="b59ab-242">第二个 Edit（） 操作尝试更新数据库。</span><span class="sxs-lookup"><span data-stu-id="b59ab-242">The second Edit() action attempts to update the database.</span></span>

<span data-ttu-id="b59ab-243">**清单4 = 控制器\主控制器.cs（编辑方法）**</span><span class="sxs-lookup"><span data-stu-id="b59ab-243">**Listing 4 – Controllers\HomeController.cs (Edit methods)**</span></span>

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample6.cs)]

<span data-ttu-id="b59ab-244">第二个 Edit（） 操作首先从与正在编辑的影片的 ID 匹配的数据库检索影片记录。</span><span class="sxs-lookup"><span data-stu-id="b59ab-244">The second Edit() action starts by retrieving the Movie record from the database that matches the Id of the movie being edited.</span></span> <span data-ttu-id="b59ab-245">以下 LINQ 到实体语句获取与特定 Id 匹配的第一个数据库记录：</span><span class="sxs-lookup"><span data-stu-id="b59ab-245">The following LINQ to Entities statement grabs the first database record that matches a particular Id:</span></span>

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample7.cs)]

<span data-ttu-id="b59ab-246">接下来，TryUpdateModel（） 方法用于将 HTML 表单字段的值分配给影片实体的属性。</span><span class="sxs-lookup"><span data-stu-id="b59ab-246">Next, the TryUpdateModel() method is used to assign the values of the HTML form fields to the properties of the movie entity.</span></span> <span data-ttu-id="b59ab-247">请注意，提供了一个白名单，以指定要更新的确切属性。</span><span class="sxs-lookup"><span data-stu-id="b59ab-247">Notice that a white list is supplied to specify the exact properties to update.</span></span>

<span data-ttu-id="b59ab-248">接下来，执行一些简单的验证，以验证影片标题和导演属性是否具有值。</span><span class="sxs-lookup"><span data-stu-id="b59ab-248">Next, some simple validation is performed to verify that both the Movie Title and Director properties have values.</span></span> <span data-ttu-id="b59ab-249">如果任一属性缺少值，则验证错误消息将添加到 ModelState 和 ModelState。IsValid 返回该值为 false。</span><span class="sxs-lookup"><span data-stu-id="b59ab-249">If either property is missing a value, then a validation error message is added to ModelState and ModelState.IsValid returns the value false.</span></span>

<span data-ttu-id="b59ab-250">最后，如果没有验证错误，则通过调用 SaveChanges（） 方法，将更新基础"电影"数据库表与任何更改。</span><span class="sxs-lookup"><span data-stu-id="b59ab-250">Finally, if there are no validation errors, then the underlying Movies database table is updated with any changes by calling the SaveChanges() method.</span></span>

<span data-ttu-id="b59ab-251">编辑数据库记录时，需要将正在编辑的记录的 Id 传递给执行数据库更新的控制器操作。</span><span class="sxs-lookup"><span data-stu-id="b59ab-251">When editing database records, you need to pass the Id of the record being edited to the controller action that performs the database update.</span></span> <span data-ttu-id="b59ab-252">否则，控制器操作将不知道要在基础数据库中更新哪个记录。</span><span class="sxs-lookup"><span data-stu-id="b59ab-252">Otherwise, the controller action will not know which record to update in the underlying database.</span></span> <span data-ttu-id="b59ab-253">清单 5 中包含的"编辑"视图包含一个隐藏表单字段，该字段表示要编辑的数据库记录的 ID。</span><span class="sxs-lookup"><span data-stu-id="b59ab-253">The Edit view, contained in Listing 5, includes a hidden form field that represents the Id of the database record being edited.</span></span>

<span data-ttu-id="b59ab-254">**清单5 = 视图\home_编辑.aspx**</span><span class="sxs-lookup"><span data-stu-id="b59ab-254">**Listing 5 – Views\Home\Edit.aspx**</span></span>

[!code-aspx[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample8.aspx)]

## <a name="deleting-database-records-with-the-entity-framework"></a><span data-ttu-id="b59ab-255">使用实体框架删除数据库记录</span><span class="sxs-lookup"><span data-stu-id="b59ab-255">Deleting Database Records with the Entity Framework</span></span>

<span data-ttu-id="b59ab-256">本教程中需要处理的最终数据库操作是删除数据库记录。</span><span class="sxs-lookup"><span data-stu-id="b59ab-256">The final database operation, which we need to tackle in this tutorial, is deleting database records.</span></span> <span data-ttu-id="b59ab-257">您可以使用清单 6 中的控制器操作删除特定的数据库记录。</span><span class="sxs-lookup"><span data-stu-id="b59ab-257">You can use the controller action in Listing 6 to delete a particular database record.</span></span>

<span data-ttu-id="b59ab-258">**清单6 -- [控制器]主控制器.cs（删除操作）**</span><span class="sxs-lookup"><span data-stu-id="b59ab-258">**Listing 6 -- \Controllers\HomeController.cs (Delete action)**</span></span>

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample9.cs)]

<span data-ttu-id="b59ab-259">Delete（） 操作首先检索与传递给该操作的 ID 匹配的 Movie 实体。</span><span class="sxs-lookup"><span data-stu-id="b59ab-259">The Delete() action first retrieves the Movie entity that matches the Id passed to the action.</span></span> <span data-ttu-id="b59ab-260">接下来，通过调用 DeleteObject（） 方法后跟 SaveChanges（） 方法从数据库中删除影片。</span><span class="sxs-lookup"><span data-stu-id="b59ab-260">Next, the movie is deleted from the database by calling the DeleteObject() method followed by the SaveChanges() method.</span></span> <span data-ttu-id="b59ab-261">最后，用户被重定向回索引视图。</span><span class="sxs-lookup"><span data-stu-id="b59ab-261">Finally, the user is redirected back to the Index view.</span></span>

## <a name="summary"></a><span data-ttu-id="b59ab-262">总结</span><span class="sxs-lookup"><span data-stu-id="b59ab-262">Summary</span></span>

<span data-ttu-id="b59ab-263">本教程的目的是演示如何利用ASP.NET MVC 和 Microsoft 实体框架构建数据库驱动的 Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="b59ab-263">The purpose of this tutorial was to demonstrate how you can build database-driven web applications by taking advantage of ASP.NET MVC and the Microsoft Entity Framework.</span></span> <span data-ttu-id="b59ab-264">您学习了如何构建一个应用程序，使您能够选择、插入、更新和删除数据库记录。</span><span class="sxs-lookup"><span data-stu-id="b59ab-264">You learned how to build an application that enables you to select, insert, update, and delete database records.</span></span>

<span data-ttu-id="b59ab-265">首先，我们讨论了如何使用实体数据模型向导从 Visual Studio 中生成实体数据模型。</span><span class="sxs-lookup"><span data-stu-id="b59ab-265">First, we discussed how you can use the Entity Data Model Wizard to generate an Entity Data Model from within Visual Studio.</span></span> <span data-ttu-id="b59ab-266">接下来，您将学习如何使用 LINQ 到实体从数据库表中检索一组数据库记录。</span><span class="sxs-lookup"><span data-stu-id="b59ab-266">Next, you learn how to use LINQ to Entities to retrieve a set of database records from a database table.</span></span> <span data-ttu-id="b59ab-267">最后，我们使用实体框架插入、更新和删除数据库记录。</span><span class="sxs-lookup"><span data-stu-id="b59ab-267">Finally, we used the Entity Framework to insert, update, and delete database records.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="b59ab-268">下一页</span><span class="sxs-lookup"><span data-stu-id="b59ab-268">Next</span></span>](creating-model-classes-with-linq-to-sql-cs.md)

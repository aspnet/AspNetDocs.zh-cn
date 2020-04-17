---
uid: mvc/overview/older-versions-1/models-data/displaying-a-table-of-database-data-cs
title: 显示数据库数据表 （C#） |微软文档
author: rick-anderson
description: 在本教程中，我将演示显示一组数据库记录的两种方法。 我在 HTML ta...
ms.author: riande
ms.date: 10/07/2008
ms.assetid: d6e758b6-6571-484d-a132-34ee6c47747a
msc.legacyurl: /mvc/overview/older-versions-1/models-data/displaying-a-table-of-database-data-cs
msc.type: authoredcontent
ms.openlocfilehash: 3fca8ac9e9b4e549ca76ffa282cc03aa4cc50e88
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542049"
---
# <a name="displaying-a-table-of-database-data-c"></a><span data-ttu-id="53c2d-104">显示数据库数据表 (C#)</span><span class="sxs-lookup"><span data-stu-id="53c2d-104">Displaying a Table of Database Data (C#)</span></span>

<span data-ttu-id="53c2d-105">由[微软](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="53c2d-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="53c2d-106">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="53c2d-106">Download PDF</span></span>](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_11_CS.pdf)

> <span data-ttu-id="53c2d-107">在本教程中，我将演示显示一组数据库记录的两种方法。</span><span class="sxs-lookup"><span data-stu-id="53c2d-107">In this tutorial, I demonstrate two methods of displaying a set of database records.</span></span> <span data-ttu-id="53c2d-108">我在 HTML 表中显示了两种格式化一组数据库记录的方法。</span><span class="sxs-lookup"><span data-stu-id="53c2d-108">I show two methods of formatting a set of database records in an HTML table.</span></span> <span data-ttu-id="53c2d-109">首先，我将演示如何直接在视图中设置数据库记录的格式。</span><span class="sxs-lookup"><span data-stu-id="53c2d-109">First, I show how you can format the database records directly within a view.</span></span> <span data-ttu-id="53c2d-110">接下来，我将演示如何在格式化数据库记录时利用部分。</span><span class="sxs-lookup"><span data-stu-id="53c2d-110">Next, I demonstrate how you can take advantage of partials when formatting database records.</span></span>

<span data-ttu-id="53c2d-111">本教程的目的是解释如何在mVC应用程序中显示ASP.NET数据库数据的 HTML 表。</span><span class="sxs-lookup"><span data-stu-id="53c2d-111">The goal of this tutorial is to explain how you can display an HTML table of database data in an ASP.NET MVC application.</span></span> <span data-ttu-id="53c2d-112">首先，您将了解如何使用 Visual Studio 中包含的基架工具生成自动显示一组记录的视图。</span><span class="sxs-lookup"><span data-stu-id="53c2d-112">First, you learn how to use the scaffolding tools included in Visual Studio to generate a view that displays a set of records automatically.</span></span> <span data-ttu-id="53c2d-113">接下来，您将学习如何在格式化数据库记录时使用部分模板。</span><span class="sxs-lookup"><span data-stu-id="53c2d-113">Next, you learn how to use a partial as a template when formatting database records.</span></span>

## <a name="create-the-model-classes"></a><span data-ttu-id="53c2d-114">创建模型类</span><span class="sxs-lookup"><span data-stu-id="53c2d-114">Create the Model Classes</span></span>

<span data-ttu-id="53c2d-115">我们将从"电影"数据库表中显示记录集。</span><span class="sxs-lookup"><span data-stu-id="53c2d-115">We are going to display the set of records from the Movies database table.</span></span> <span data-ttu-id="53c2d-116">"影片"数据库表包含以下列：</span><span class="sxs-lookup"><span data-stu-id="53c2d-116">The Movies database table contains the following columns:</span></span>

<a id="0.3_table01"></a>

| <span data-ttu-id="53c2d-117">**列名**</span><span class="sxs-lookup"><span data-stu-id="53c2d-117">**Column Name**</span></span> | <span data-ttu-id="53c2d-118">**数据类型**</span><span class="sxs-lookup"><span data-stu-id="53c2d-118">**Data Type**</span></span> | <span data-ttu-id="53c2d-119">**允许 Null 值**</span><span class="sxs-lookup"><span data-stu-id="53c2d-119">**Allow Nulls**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="53c2d-120">ID</span><span class="sxs-lookup"><span data-stu-id="53c2d-120">Id</span></span> | <span data-ttu-id="53c2d-121">Int</span><span class="sxs-lookup"><span data-stu-id="53c2d-121">Int</span></span> | <span data-ttu-id="53c2d-122">False</span><span class="sxs-lookup"><span data-stu-id="53c2d-122">False</span></span> |
| <span data-ttu-id="53c2d-123">标题</span><span class="sxs-lookup"><span data-stu-id="53c2d-123">Title</span></span> | <span data-ttu-id="53c2d-124">恩瓦尔查尔 （200）</span><span class="sxs-lookup"><span data-stu-id="53c2d-124">Nvarchar(200)</span></span> | <span data-ttu-id="53c2d-125">False</span><span class="sxs-lookup"><span data-stu-id="53c2d-125">False</span></span> |
| <span data-ttu-id="53c2d-126">导演</span><span class="sxs-lookup"><span data-stu-id="53c2d-126">Director</span></span> | <span data-ttu-id="53c2d-127">恩瓦尔查尔 （50）</span><span class="sxs-lookup"><span data-stu-id="53c2d-127">NVarchar(50)</span></span> | <span data-ttu-id="53c2d-128">False</span><span class="sxs-lookup"><span data-stu-id="53c2d-128">False</span></span> |
| <span data-ttu-id="53c2d-129">发布日期</span><span class="sxs-lookup"><span data-stu-id="53c2d-129">DateReleased</span></span> | <span data-ttu-id="53c2d-130">DateTime</span><span class="sxs-lookup"><span data-stu-id="53c2d-130">DateTime</span></span> | <span data-ttu-id="53c2d-131">False</span><span class="sxs-lookup"><span data-stu-id="53c2d-131">False</span></span> |

<span data-ttu-id="53c2d-132">为了在ASP.NET MVC 应用程序中表示"电影"表，我们需要创建一个模型类。</span><span class="sxs-lookup"><span data-stu-id="53c2d-132">In order to represent the Movies table in our ASP.NET MVC application, we need to create a model class.</span></span> <span data-ttu-id="53c2d-133">在本教程中，我们使用 Microsoft 实体框架创建模型类。</span><span class="sxs-lookup"><span data-stu-id="53c2d-133">In this tutorial, we use the Microsoft Entity Framework to create our model classes.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="53c2d-134">在本教程中，我们使用 Microsoft 实体框架。</span><span class="sxs-lookup"><span data-stu-id="53c2d-134">In this tutorial, we use the Microsoft Entity Framework.</span></span> <span data-ttu-id="53c2d-135">但是，请务必了解，您可以使用各种不同的技术与数据库进行交互，从ASP.NET MVC 应用程序（包括 LINQ 到 SQL、NHibernate 或ADO.NET）。</span><span class="sxs-lookup"><span data-stu-id="53c2d-135">However, it is important to understand that you can use a variety of different technologies to interact with a database from an ASP.NET MVC application including LINQ to SQL, NHibernate, or ADO.NET.</span></span>

<span data-ttu-id="53c2d-136">按照以下步骤启动实体数据模型向导：</span><span class="sxs-lookup"><span data-stu-id="53c2d-136">Follow these steps to launch the Entity Data Model Wizard:</span></span>

1. <span data-ttu-id="53c2d-137">右键单击"解决方案资源管理器"窗口中的"模型"文件夹，然后选择菜单选项 **"添加、新建项目**"。</span><span class="sxs-lookup"><span data-stu-id="53c2d-137">Right-click the Models folder in the Solution Explorer window and the select the menu option **Add, New Item**.</span></span>
2. <span data-ttu-id="53c2d-138">选择 **"数据**"类别并选择**ADO.NET实体数据模型**模板。</span><span class="sxs-lookup"><span data-stu-id="53c2d-138">Select the **Data** category and select the **ADO.NET Entity Data Model** template.</span></span>
3. <span data-ttu-id="53c2d-139">为数据模型指定名称 *"MoviesDBModel.edmx"，* 然后单击 **"添加**"按钮。</span><span class="sxs-lookup"><span data-stu-id="53c2d-139">Give your data model the name *MoviesDBModel.edmx* and click the **Add** button.</span></span>

<span data-ttu-id="53c2d-140">单击"添加"按钮后，将显示实体数据模型向导（参见图 1）。</span><span class="sxs-lookup"><span data-stu-id="53c2d-140">After you click the Add button, the Entity Data Model Wizard appears (see Figure 1).</span></span> <span data-ttu-id="53c2d-141">按照以下步骤完成向导：</span><span class="sxs-lookup"><span data-stu-id="53c2d-141">Follow these steps to complete the wizard:</span></span>

1. <span data-ttu-id="53c2d-142">在 **"选择模型内容"** 步骤中，选择"**从数据库生成**"选项。</span><span class="sxs-lookup"><span data-stu-id="53c2d-142">In the **Choose Model Contents** step, select the **Generate from database** option.</span></span>
2. <span data-ttu-id="53c2d-143">在 **"选择数据连接**"步骤中，使用*MoviesDB.mdf*数据连接和名称 *"电影 DB实体*"来设置连接设置。</span><span class="sxs-lookup"><span data-stu-id="53c2d-143">In the **Choose Your Data Connection** step, use the *MoviesDB.mdf* data connection and the name *MoviesDBEntities* for the connection settings.</span></span> <span data-ttu-id="53c2d-144">单击 **“下一步”** 按钮。</span><span class="sxs-lookup"><span data-stu-id="53c2d-144">Click the **Next** button.</span></span>
3. <span data-ttu-id="53c2d-145">在 **"选择数据库对象**"步骤中，展开"表"节点，选择"影片"表。</span><span class="sxs-lookup"><span data-stu-id="53c2d-145">In the **Choose Your Database Objects** step, expand the Tables node, select the Movies table.</span></span> <span data-ttu-id="53c2d-146">输入命名空间*模型*，然后单击 **"完成"** 按钮。</span><span class="sxs-lookup"><span data-stu-id="53c2d-146">Enter the namespace *Models* and click the **Finish** button.</span></span>

<span data-ttu-id="53c2d-147">[![将 LINQ 创建到 SQL 类](displaying-a-table-of-database-data-cs/_static/image1.jpg)](displaying-a-table-of-database-data-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="53c2d-147">[![Creating LINQ to SQL classes](displaying-a-table-of-database-data-cs/_static/image1.jpg)](displaying-a-table-of-database-data-cs/_static/image1.png)</span></span>

<span data-ttu-id="53c2d-148">**图 01**： 创建 LINQ 到 SQL 类 （[单击以查看全尺寸图像](displaying-a-table-of-database-data-cs/_static/image2.png)）</span><span class="sxs-lookup"><span data-stu-id="53c2d-148">**Figure 01**: Creating LINQ to SQL classes ([Click to view full-size image](displaying-a-table-of-database-data-cs/_static/image2.png))</span></span>

<span data-ttu-id="53c2d-149">完成实体数据模型向导后，将打开实体数据模型设计器。</span><span class="sxs-lookup"><span data-stu-id="53c2d-149">After you complete the Entity Data Model Wizard, the Entity Data Model Designer opens.</span></span> <span data-ttu-id="53c2d-150">设计器应显示影片实体（参见图 2）。</span><span class="sxs-lookup"><span data-stu-id="53c2d-150">The Designer should display the Movies entity (see Figure 2).</span></span>

<span data-ttu-id="53c2d-151">[![实体数据模型设计器](displaying-a-table-of-database-data-cs/_static/image2.jpg)](displaying-a-table-of-database-data-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="53c2d-151">[![The Entity Data Model Designer](displaying-a-table-of-database-data-cs/_static/image2.jpg)](displaying-a-table-of-database-data-cs/_static/image3.png)</span></span>

<span data-ttu-id="53c2d-152">**图 02**： 实体数据模型设计器 （[单击以查看全尺寸图像](displaying-a-table-of-database-data-cs/_static/image4.png)）</span><span class="sxs-lookup"><span data-stu-id="53c2d-152">**Figure 02**: The Entity Data Model Designer ([Click to view full-size image](displaying-a-table-of-database-data-cs/_static/image4.png))</span></span>

<span data-ttu-id="53c2d-153">在继续之前，我们需要作出一个改变。</span><span class="sxs-lookup"><span data-stu-id="53c2d-153">We need to make one change before we continue.</span></span> <span data-ttu-id="53c2d-154">实体数据向导生成一个名为 *"电影"* 的模型类，该类表示"影片"数据库表。</span><span class="sxs-lookup"><span data-stu-id="53c2d-154">The Entity Data Wizard generates a model class named *Movies* that represents the Movies database table.</span></span> <span data-ttu-id="53c2d-155">由于我们将使用"电影"类来表示特定影片，因此我们需要将类的名称修改为 *"电影*"而不是 *"电影*"（单数而不是复数）。</span><span class="sxs-lookup"><span data-stu-id="53c2d-155">Because we'll use the Movies class to represent a particular movie, we need to modify the name of the class to be *Movie* instead of *Movies* (singular rather than plural).</span></span>

<span data-ttu-id="53c2d-156">双击设计器表面上的类的名称，并将类的名称从"影片"更改为"影片"。</span><span class="sxs-lookup"><span data-stu-id="53c2d-156">Double-click the name of the class on the designer surface and change the name of the class from Movies to Movie.</span></span> <span data-ttu-id="53c2d-157">进行此更改后，单击 **"保存**"按钮（软盘的图标）以生成 Movie 类。</span><span class="sxs-lookup"><span data-stu-id="53c2d-157">After making this change, click the **Save** button (the icon of the floppy disk) to generate the Movie class.</span></span>

## <a name="create-the-movies-controller"></a><span data-ttu-id="53c2d-158">创建影片控制器</span><span class="sxs-lookup"><span data-stu-id="53c2d-158">Create the Movies Controller</span></span>

<span data-ttu-id="53c2d-159">现在，我们有一种方法来表示我们的数据库记录，我们可以创建一个控制器，返回电影的集合。</span><span class="sxs-lookup"><span data-stu-id="53c2d-159">Now that we have a way to represent our database records, we can create a controller that returns the collection of movies.</span></span> <span data-ttu-id="53c2d-160">在可视化工作室解决方案资源管理器窗口中，右键单击"控制器"文件夹并选择菜单选项 **"添加控制器**"（参见图 3）。</span><span class="sxs-lookup"><span data-stu-id="53c2d-160">Within the Visual Studio Solution Explorer window, right-click the Controllers folder and select the menu option **Add, Controller** (see Figure 3).</span></span>

<span data-ttu-id="53c2d-161">[![添加控制器菜单](displaying-a-table-of-database-data-cs/_static/image3.jpg)](displaying-a-table-of-database-data-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="53c2d-161">[![The Add Controller Menu](displaying-a-table-of-database-data-cs/_static/image3.jpg)](displaying-a-table-of-database-data-cs/_static/image5.png)</span></span>

<span data-ttu-id="53c2d-162">**图 03**： 添加控制器菜单 （[单击以查看全尺寸图像](displaying-a-table-of-database-data-cs/_static/image6.png)）</span><span class="sxs-lookup"><span data-stu-id="53c2d-162">**Figure 03**: The Add Controller Menu ([Click to view full-size image](displaying-a-table-of-database-data-cs/_static/image6.png))</span></span>

<span data-ttu-id="53c2d-163">出现 **"添加控制器"** 对话框时，输入控制器名称"电影控制器"（参见图 4）。</span><span class="sxs-lookup"><span data-stu-id="53c2d-163">When the **Add Controller** dialog appears, enter the controller name MovieController (see Figure 4).</span></span> <span data-ttu-id="53c2d-164">单击"**添加**"按钮以添加新控制器。</span><span class="sxs-lookup"><span data-stu-id="53c2d-164">Click the **Add** button to add the new controller.</span></span>

<span data-ttu-id="53c2d-165">[![添加控制器对话框](displaying-a-table-of-database-data-cs/_static/image4.jpg)](displaying-a-table-of-database-data-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="53c2d-165">[![The Add Controller dialog](displaying-a-table-of-database-data-cs/_static/image4.jpg)](displaying-a-table-of-database-data-cs/_static/image7.png)</span></span>

<span data-ttu-id="53c2d-166">**图 04**： 添加控制器对话框（[单击以查看全尺寸图像](displaying-a-table-of-database-data-cs/_static/image8.png)）</span><span class="sxs-lookup"><span data-stu-id="53c2d-166">**Figure 04**: The Add Controller dialog([Click to view full-size image](displaying-a-table-of-database-data-cs/_static/image8.png))</span></span>

<span data-ttu-id="53c2d-167">我们需要修改由 Movie 控制器公开的 Index（） 操作，以便它返回数据库记录集。</span><span class="sxs-lookup"><span data-stu-id="53c2d-167">We need to modify the Index() action exposed by the Movie controller so that it returns the set of database records.</span></span> <span data-ttu-id="53c2d-168">修改控制器，使其看起来像清单 1 中的控制器。</span><span class="sxs-lookup"><span data-stu-id="53c2d-168">Modify the controller so that it looks like the controller in Listing 1.</span></span>

<span data-ttu-id="53c2d-169">**清单1 = 控制器\电影控制器.cs**</span><span class="sxs-lookup"><span data-stu-id="53c2d-169">**Listing 1 – Controllers\MovieController.cs**</span></span>

[!code-csharp[Main](displaying-a-table-of-database-data-cs/samples/sample1.cs)]

<span data-ttu-id="53c2d-170">在清单 1 中，电影 DB 实体类用于表示 MoviesDB 数据库。</span><span class="sxs-lookup"><span data-stu-id="53c2d-170">In Listing 1, the MoviesDBEntities class is used to represent the MoviesDB database.</span></span> <span data-ttu-id="53c2d-171">要使用此类，您需要导入 MvcApplication1.模型命名空间，如下所示：</span><span class="sxs-lookup"><span data-stu-id="53c2d-171">To use this class, you need to import the MvcApplication1.Models namespace like this:</span></span>

<span data-ttu-id="53c2d-172">使用 Mvc应用程序1.模型;</span><span class="sxs-lookup"><span data-stu-id="53c2d-172">using MvcApplication1.Models;</span></span>

<span data-ttu-id="53c2d-173">表达式*实体。MovieSet.ToList（）* 从"影片"数据库表中返回所有影片集。</span><span class="sxs-lookup"><span data-stu-id="53c2d-173">The expression *entities.MovieSet.ToList()* returns the set of all movies from the Movies database table.</span></span>

## <a name="create-the-view"></a><span data-ttu-id="53c2d-174">创建视图</span><span class="sxs-lookup"><span data-stu-id="53c2d-174">Create the View</span></span>

<span data-ttu-id="53c2d-175">在 HTML 表中显示一组数据库记录的最简单方法是利用 Visual Studio 提供的基架。</span><span class="sxs-lookup"><span data-stu-id="53c2d-175">The easiest way to display a set of database records in an HTML table is to take advantage of the scaffolding provided by Visual Studio.</span></span>

<span data-ttu-id="53c2d-176">通过选择菜单选项 **"生成"、"生成解决方案**"来构建应用程序。</span><span class="sxs-lookup"><span data-stu-id="53c2d-176">Build your application by selecting the menu option **Build, Build Solution**.</span></span> <span data-ttu-id="53c2d-177">在打开 **"添加视图**"对话框之前，必须生成应用程序，否则数据类不会显示在对话框中。</span><span class="sxs-lookup"><span data-stu-id="53c2d-177">You must build your application before opening the **Add View** dialog or your data classes won't appear in the dialog.</span></span>

<span data-ttu-id="53c2d-178">右键单击索引（） 操作并选择菜单选项 **"添加视图**"（参见图 5）。</span><span class="sxs-lookup"><span data-stu-id="53c2d-178">Right-click the Index() action and select the menu option **Add View** (see Figure 5).</span></span>

<span data-ttu-id="53c2d-179">[![添加视图](displaying-a-table-of-database-data-cs/_static/image5.jpg)](displaying-a-table-of-database-data-cs/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="53c2d-179">[![Adding a view](displaying-a-table-of-database-data-cs/_static/image5.jpg)](displaying-a-table-of-database-data-cs/_static/image9.png)</span></span>

<span data-ttu-id="53c2d-180">**图 05**： 添加视图 （[单击以查看全尺寸图像](displaying-a-table-of-database-data-cs/_static/image10.png)）</span><span class="sxs-lookup"><span data-stu-id="53c2d-180">**Figure 05**: Adding a view ([Click to view full-size image](displaying-a-table-of-database-data-cs/_static/image10.png))</span></span>

<span data-ttu-id="53c2d-181">在 **"添加视图"** 对话框中，选中标记为"**创建强类型视图"复选框**。</span><span class="sxs-lookup"><span data-stu-id="53c2d-181">In the **Add View** dialog, check the checkbox labeled **Create a strongly-typed view**.</span></span> <span data-ttu-id="53c2d-182">选择"影片"类作为**视图数据类**。</span><span class="sxs-lookup"><span data-stu-id="53c2d-182">Select the Movie class as the **view data class**.</span></span> <span data-ttu-id="53c2d-183">选择 *"列表*"作为**视图内容**（参见图 6）。</span><span class="sxs-lookup"><span data-stu-id="53c2d-183">Select *List* as the **view content** (see Figure 6).</span></span> <span data-ttu-id="53c2d-184">选择这些选项将生成显示影片列表的强类型视图。</span><span class="sxs-lookup"><span data-stu-id="53c2d-184">Selecting these options will generate a strongly-typed view that displays a list of movies.</span></span>

<span data-ttu-id="53c2d-185">[!["添加视图"对话框](displaying-a-table-of-database-data-cs/_static/image6.jpg)](displaying-a-table-of-database-data-cs/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="53c2d-185">[![The Add View dialog](displaying-a-table-of-database-data-cs/_static/image6.jpg)](displaying-a-table-of-database-data-cs/_static/image11.png)</span></span>

<span data-ttu-id="53c2d-186">**图 06**： 添加视图对话框（[单击以查看全尺寸图像](displaying-a-table-of-database-data-cs/_static/image12.png)）</span><span class="sxs-lookup"><span data-stu-id="53c2d-186">**Figure 06**: The Add View dialog([Click to view full-size image](displaying-a-table-of-database-data-cs/_static/image12.png))</span></span>

<span data-ttu-id="53c2d-187">单击"**添加**"按钮后，将自动生成清单 2 中的视图。</span><span class="sxs-lookup"><span data-stu-id="53c2d-187">After you click the **Add** button, the view in Listing 2 is generated automatically.</span></span> <span data-ttu-id="53c2d-188">此视图包含遍遍遍电影集合并显示影片的每个属性所需的代码。</span><span class="sxs-lookup"><span data-stu-id="53c2d-188">This view contains the code required to iterate through the collection of movies and display each of the properties of a movie.</span></span>

<span data-ttu-id="53c2d-189">**清单 2 = 视图\影片_索引.aspx**</span><span class="sxs-lookup"><span data-stu-id="53c2d-189">**Listing 2 – Views\Movie\Index.aspx**</span></span>

[!code-aspx[Main](displaying-a-table-of-database-data-cs/samples/sample2.aspx)]

<span data-ttu-id="53c2d-190">您可以通过选择菜单选项 **"调试"、"开始调试**"（或点击 F5 键）来运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="53c2d-190">You can run the application by selecting the menu option **Debug, Start Debugging** (or hitting the F5 key).</span></span> <span data-ttu-id="53c2d-191">运行应用程序将启动 Internet 资源管理器。</span><span class="sxs-lookup"><span data-stu-id="53c2d-191">Running the application launches Internet Explorer.</span></span> <span data-ttu-id="53c2d-192">如果您导航到 /Movie URL，您将看到图 7 中的页面。</span><span class="sxs-lookup"><span data-stu-id="53c2d-192">If you navigate to the /Movie URL then you'll see the page in Figure 7.</span></span>

<span data-ttu-id="53c2d-193">[![电影表](displaying-a-table-of-database-data-cs/_static/image7.jpg)](displaying-a-table-of-database-data-cs/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="53c2d-193">[![A table of movies](displaying-a-table-of-database-data-cs/_static/image7.jpg)](displaying-a-table-of-database-data-cs/_static/image13.png)</span></span>

<span data-ttu-id="53c2d-194">**图 07**： 电影表（[单击以查看全尺寸图像](displaying-a-table-of-database-data-cs/_static/image14.png)）</span><span class="sxs-lookup"><span data-stu-id="53c2d-194">**Figure 07**: A table of movies([Click to view full-size image](displaying-a-table-of-database-data-cs/_static/image14.png))</span></span>

<span data-ttu-id="53c2d-195">如果您不喜欢图 7 中数据库记录网格的外观，则只需修改 Index 视图即可。</span><span class="sxs-lookup"><span data-stu-id="53c2d-195">If you don't like anything about the appearance of the grid of database records in Figure 7 then you can simply modify the Index view.</span></span> <span data-ttu-id="53c2d-196">例如，您可以通过修改索引视图将*日期释放*标头更改为*发布日期释放*日期。</span><span class="sxs-lookup"><span data-stu-id="53c2d-196">For example, you can change the *DateReleased* header to *Date Released* by modifying the Index view.</span></span>

## <a name="create-a-template-with-a-partial"></a><span data-ttu-id="53c2d-197">创建带有部分的模板</span><span class="sxs-lookup"><span data-stu-id="53c2d-197">Create a Template with a Partial</span></span>

<span data-ttu-id="53c2d-198">当视图变得过于复杂时，最好开始将视图分解为部分视图。</span><span class="sxs-lookup"><span data-stu-id="53c2d-198">When a view gets too complicated, it is a good idea to start breaking the view into partials.</span></span> <span data-ttu-id="53c2d-199">使用部分使您的视图更易于理解和维护。</span><span class="sxs-lookup"><span data-stu-id="53c2d-199">Using partials makes your views easier to understand and maintain.</span></span> <span data-ttu-id="53c2d-200">我们将创建一个部分，我们可以用作模板来格式化每个影片数据库记录。</span><span class="sxs-lookup"><span data-stu-id="53c2d-200">We'll create a partial that we can use as a template to format each of the movie database records.</span></span>

<span data-ttu-id="53c2d-201">按照以下步骤创建部分：</span><span class="sxs-lookup"><span data-stu-id="53c2d-201">Follow these steps to create the partial:</span></span>

1. <span data-ttu-id="53c2d-202">右键单击"视图"+影片文件夹，然后选择菜单选项 **"添加视图**"。</span><span class="sxs-lookup"><span data-stu-id="53c2d-202">Right-click the Views\Movie folder and select the menu option **Add View**.</span></span>
2. <span data-ttu-id="53c2d-203">选中标记为"*创建部分视图 （.ascx）"的*复选框。</span><span class="sxs-lookup"><span data-stu-id="53c2d-203">Check the checkbox labeled *Create a partial view (.ascx)*.</span></span>
3. <span data-ttu-id="53c2d-204">命名部分*影片模板*。</span><span class="sxs-lookup"><span data-stu-id="53c2d-204">Name the partial *MovieTemplate*.</span></span>
4. <span data-ttu-id="53c2d-205">选中标记为"**创建强类型视图"的**复选框。</span><span class="sxs-lookup"><span data-stu-id="53c2d-205">Check the checkbox labeled **Create a strongly-typed view**.</span></span>
5. <span data-ttu-id="53c2d-206">选择"影片"作为*视图数据类*。</span><span class="sxs-lookup"><span data-stu-id="53c2d-206">Select Movie as the *view data class*.</span></span>
6. <span data-ttu-id="53c2d-207">选择"空"作为*视图内容*。</span><span class="sxs-lookup"><span data-stu-id="53c2d-207">Select Empty as the *view content*.</span></span>
7. <span data-ttu-id="53c2d-208">单击"**添加**"按钮将部分添加到项目中。</span><span class="sxs-lookup"><span data-stu-id="53c2d-208">Click the **Add** button to add the partial to your project.</span></span>

<span data-ttu-id="53c2d-209">完成这些步骤后，将"电影模板"部分修改为类似于清单 3。</span><span class="sxs-lookup"><span data-stu-id="53c2d-209">After you complete these steps, modify the MovieTemplate partial to look like Listing 3.</span></span>

<span data-ttu-id="53c2d-210">**清单3 = 视图\电影_电影模板.ascx**</span><span class="sxs-lookup"><span data-stu-id="53c2d-210">**Listing 3 – Views\Movie\MovieTemplate.ascx**</span></span>

[!code-aspx[Main](displaying-a-table-of-database-data-cs/samples/sample3.aspx)]

<span data-ttu-id="53c2d-211">清单3中的部分包含一行记录的模板。</span><span class="sxs-lookup"><span data-stu-id="53c2d-211">The partial in Listing 3 contains a template for a single row of records.</span></span>

<span data-ttu-id="53c2d-212">清单4中修改后的索引视图使用影片模板部分。</span><span class="sxs-lookup"><span data-stu-id="53c2d-212">The modified Index view in Listing 4 uses the MovieTemplate partial.</span></span>

<span data-ttu-id="53c2d-213">**清单4 = 视图\影片_索引.aspx**</span><span class="sxs-lookup"><span data-stu-id="53c2d-213">**Listing 4 – Views\Movie\Index.aspx**</span></span>

[!code-aspx[Main](displaying-a-table-of-database-data-cs/samples/sample4.aspx)]

<span data-ttu-id="53c2d-214">清单 4 中的视图包含一个循环，该循环遍历所有影片。</span><span class="sxs-lookup"><span data-stu-id="53c2d-214">The view in Listing 4 contains a foreach loop that iterates through all of the movies.</span></span> <span data-ttu-id="53c2d-215">对于每个影片，影片模板部分用于格式化影片。</span><span class="sxs-lookup"><span data-stu-id="53c2d-215">For each movie, the MovieTemplate partial is used to format the movie.</span></span> <span data-ttu-id="53c2d-216">通过调用 Render 部分（） 帮助器方法来呈现影片模板。</span><span class="sxs-lookup"><span data-stu-id="53c2d-216">The MovieTemplate is rendered by calling the RenderPartial() helper method.</span></span>

<span data-ttu-id="53c2d-217">修改后的 Index 视图呈现的数据库记录的 HTML 表与同一个表。</span><span class="sxs-lookup"><span data-stu-id="53c2d-217">The modified Index view renders the very same HTML table of database records.</span></span> <span data-ttu-id="53c2d-218">但是，视图已大大简化。</span><span class="sxs-lookup"><span data-stu-id="53c2d-218">However, the view has been greatly simplified.</span></span>

<span data-ttu-id="53c2d-219">Render部分（） 方法不同于大多数其他帮助器方法，因为它不返回字符串。</span><span class="sxs-lookup"><span data-stu-id="53c2d-219">The RenderPartial() method is different than most of the other helper methods because it does not return a string.</span></span> <span data-ttu-id="53c2d-220">因此，必须使用&lt;% Html.render 部分（）;%&gt;而不是&lt;%= Html.render 部分（）;%&gt;.</span><span class="sxs-lookup"><span data-stu-id="53c2d-220">Therefore, you must call the RenderPartial() method using &lt;% Html.RenderPartial(); %&gt; instead of &lt;%= Html.RenderPartial(); %&gt;.</span></span>

## <a name="summary"></a><span data-ttu-id="53c2d-221">总结</span><span class="sxs-lookup"><span data-stu-id="53c2d-221">Summary</span></span>

<span data-ttu-id="53c2d-222">本教程的目的是解释如何在 HTML 表中显示一组数据库记录。</span><span class="sxs-lookup"><span data-stu-id="53c2d-222">The goal of this tutorial was to explain how you can display a set of database records in an HTML table.</span></span> <span data-ttu-id="53c2d-223">首先，您学习了如何通过利用 Microsoft 实体框架从控制器操作返回一组数据库记录。</span><span class="sxs-lookup"><span data-stu-id="53c2d-223">First, you learned how to return a set of database records from a controller action by taking advantage of the Microsoft Entity Framework.</span></span> <span data-ttu-id="53c2d-224">接下来，您学习了如何使用 Visual Studio 基架生成自动显示项目集合的视图。</span><span class="sxs-lookup"><span data-stu-id="53c2d-224">Next, you learned how to use Visual Studio scaffolding to generate a view that displays a collection of items automatically.</span></span> <span data-ttu-id="53c2d-225">最后，您学习了如何通过利用部分视图来简化视图。</span><span class="sxs-lookup"><span data-stu-id="53c2d-225">Finally, you learned how to simplify the view by taking advantage of a partial.</span></span> <span data-ttu-id="53c2d-226">您学习了如何使用部分作为模板，以便可以格式化每个数据库记录。</span><span class="sxs-lookup"><span data-stu-id="53c2d-226">You learned how to use a partial as a template so that you can format each database record.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="53c2d-227">[上一页](creating-model-classes-with-linq-to-sql-cs.md)
> [下一页](performing-simple-validation-cs.md)</span><span class="sxs-lookup"><span data-stu-id="53c2d-227">[Previous](creating-model-classes-with-linq-to-sql-cs.md)
[Next](performing-simple-validation-cs.md)</span></span>

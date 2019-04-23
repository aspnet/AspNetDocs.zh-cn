---
uid: mvc/overview/older-versions-1/models-data/creating-model-classes-with-linq-to-sql-vb
title: 使用 LINQ to SQL (VB) 创建模型类 |Microsoft Docs
author: microsoft
description: 本教程的目的是说明创建 ASP.NET MVC 应用程序的模型类的一种方法。 在本教程中，您将学习如何构建模型 c...
ms.author: riande
ms.date: 10/07/2008
ms.assetid: a4a25a75-d71f-4509-98b4-df72e748985a
msc.legacyurl: /mvc/overview/older-versions-1/models-data/creating-model-classes-with-linq-to-sql-vb
msc.type: authoredcontent
ms.openlocfilehash: 212287ea384cf54f9eda477e6f706637d10dd54a
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2019
ms.locfileid: "59419894"
---
# <a name="creating-model-classes-with-linq-to-sql-vb"></a><span data-ttu-id="0217a-104">使用 LINQ to SQL 创建模型类 (VB)</span><span class="sxs-lookup"><span data-stu-id="0217a-104">Creating Model Classes with LINQ to SQL (VB)</span></span>

<span data-ttu-id="0217a-105">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="0217a-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="0217a-106">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="0217a-106">Download PDF</span></span>](http://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_10_VB.pdf)

> <span data-ttu-id="0217a-107">本教程的目的是说明创建 ASP.NET MVC 应用程序的模型类的一种方法。</span><span class="sxs-lookup"><span data-stu-id="0217a-107">The goal of this tutorial is to explain one method of creating model classes for an ASP.NET MVC application.</span></span> <span data-ttu-id="0217a-108">在本教程中，您将学习如何生成模型的类和执行通过利用 Microsoft LINQ 到 SQL 数据库访问权限。</span><span class="sxs-lookup"><span data-stu-id="0217a-108">In this tutorial, you learn how to build model classes and perform database access by taking advantage of Microsoft LINQ to SQL.</span></span>


<span data-ttu-id="0217a-109">本教程的目的是说明创建 ASP.NET MVC 应用程序的模型类的一种方法。</span><span class="sxs-lookup"><span data-stu-id="0217a-109">The goal of this tutorial is to explain one method of creating model classes for an ASP.NET MVC application.</span></span> <span data-ttu-id="0217a-110">在本教程中，您将学习如何生成模型的类和执行通过利用 Microsoft LINQ 到 SQL 数据库访问权限。</span><span class="sxs-lookup"><span data-stu-id="0217a-110">In this tutorial, you learn how to build model classes and perform database access by taking advantage of Microsoft LINQ to SQL.</span></span>

<span data-ttu-id="0217a-111">在本教程中，我们构建一个基本的电影数据库应用程序。</span><span class="sxs-lookup"><span data-stu-id="0217a-111">In this tutorial, we build a basic Movie database application.</span></span> <span data-ttu-id="0217a-112">我们先创建电影数据库应用程序中的最快且最简单的方法可能。</span><span class="sxs-lookup"><span data-stu-id="0217a-112">We start by creating the Movie database application in the fastest and easiest way possible.</span></span> <span data-ttu-id="0217a-113">我们将执行我们的数据访问的所有直接从控制器操作。</span><span class="sxs-lookup"><span data-stu-id="0217a-113">We perform all of our data access directly from our controller actions.</span></span>

<span data-ttu-id="0217a-114">接下来，您将了解如何使用存储库模式。</span><span class="sxs-lookup"><span data-stu-id="0217a-114">Next, you learn how to use the Repository pattern.</span></span> <span data-ttu-id="0217a-115">使用存储库模式需要更多工作。</span><span class="sxs-lookup"><span data-stu-id="0217a-115">Using the Repository pattern requires a little more work.</span></span> <span data-ttu-id="0217a-116">但是，采用此模式的优点是它使你能够构建到自适应应用程序更改，可以轻松地测试。</span><span class="sxs-lookup"><span data-stu-id="0217a-116">However, the advantage of adopting this pattern is that it enables you to build applications that are adaptable to change and can be easily tested.</span></span>

## <a name="what-is-a-model-class"></a><span data-ttu-id="0217a-117">什么是 Model 类？</span><span class="sxs-lookup"><span data-stu-id="0217a-117">What is a Model Class?</span></span>

<span data-ttu-id="0217a-118">MVC 模型包含所有未包含在 MVC 视图或 MVC 控制器中的应用程序逻辑。</span><span class="sxs-lookup"><span data-stu-id="0217a-118">An MVC model contains all of the application logic that is not contained in an MVC view or MVC controller.</span></span> <span data-ttu-id="0217a-119">具体而言，MVC 模型包含的所有应用程序业务和数据访问逻辑。</span><span class="sxs-lookup"><span data-stu-id="0217a-119">In particular, an MVC model contains all of your application business and data access logic.</span></span>

<span data-ttu-id="0217a-120">可以使用各种不同的技术来实现数据访问逻辑。</span><span class="sxs-lookup"><span data-stu-id="0217a-120">You can use a variety of different technologies to implement your data access logic.</span></span> <span data-ttu-id="0217a-121">例如，您可以构建使用 Microsoft 实体框架、 NHibernate、 Subsonic 或 ADO.NET 类的数据访问类。</span><span class="sxs-lookup"><span data-stu-id="0217a-121">For example, you can build your data access classes using the Microsoft Entity Framework, NHibernate, Subsonic, or ADO.NET classes.</span></span>

<span data-ttu-id="0217a-122">在本教程中，我使用 LINQ to SQL 来查询和更新数据库。</span><span class="sxs-lookup"><span data-stu-id="0217a-122">In this tutorial, I use LINQ to SQL to query and update the database.</span></span> <span data-ttu-id="0217a-123">LINQ to SQL 提供的与 Microsoft SQL Server 数据库进行交互非常简单的方法。</span><span class="sxs-lookup"><span data-stu-id="0217a-123">LINQ to SQL provides you with a very easy method of interacting with a Microsoft SQL Server database.</span></span> <span data-ttu-id="0217a-124">但是，务必了解 ASP.NET MVC framework 不绑定到 LINQ to SQL 以任何方式。</span><span class="sxs-lookup"><span data-stu-id="0217a-124">However, it is important to understand that the ASP.NET MVC framework is not tied to LINQ to SQL in any way.</span></span> <span data-ttu-id="0217a-125">ASP.NET MVC 是与任何数据访问技术兼容。</span><span class="sxs-lookup"><span data-stu-id="0217a-125">ASP.NET MVC is compatible with any data access technology.</span></span>

## <a name="create-a-movie-database"></a><span data-ttu-id="0217a-126">创建电影数据库</span><span class="sxs-lookup"><span data-stu-id="0217a-126">Create a Movie Database</span></span>

<span data-ttu-id="0217a-127">在此教程--为了说明如何构建模型类-我们构建一个简单的电影数据库应用程序。</span><span class="sxs-lookup"><span data-stu-id="0217a-127">In this tutorial -- in order to illustrate how you can build model classes -- we build a simple Movie database application.</span></span> <span data-ttu-id="0217a-128">第一步是创建新的数据库。</span><span class="sxs-lookup"><span data-stu-id="0217a-128">The first step is to create a new database.</span></span> <span data-ttu-id="0217a-129">右键单击该应用\_在解决方案资源管理器窗口中，选择菜单选项的数据文件夹**添加、 新项**。</span><span class="sxs-lookup"><span data-stu-id="0217a-129">Right-click the App\_Data folder in the Solution Explorer window and select the menu option **Add, New Item**.</span></span> <span data-ttu-id="0217a-130">选择 SQL Server 数据库的模板，为其提供名称 MoviesDB.mdf，然后单击**添加**按钮 （请参见图 1）。</span><span class="sxs-lookup"><span data-stu-id="0217a-130">Select the SQL Server Database template, give it the name MoviesDB.mdf, and click the **Add** button (see Figure 1).</span></span>


<span data-ttu-id="0217a-131">[![添加新的 SQL Server 数据库](creating-model-classes-with-linq-to-sql-vb/_static/image2.png)](creating-model-classes-with-linq-to-sql-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="0217a-131">[![Adding a new SQL Server Database](creating-model-classes-with-linq-to-sql-vb/_static/image2.png)](creating-model-classes-with-linq-to-sql-vb/_static/image1.png)</span></span>

<span data-ttu-id="0217a-132">**图 01**:添加新的 SQL Server 数据库 ([单击此项可查看原尺寸图像](creating-model-classes-with-linq-to-sql-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="0217a-132">**Figure 01**: Adding a new SQL Server Database ([Click to view full-size image](creating-model-classes-with-linq-to-sql-vb/_static/image3.png))</span></span>


<span data-ttu-id="0217a-133">创建新的数据库后，可以通过双击 MoviesDB.mdf 文件在应用中的打开数据库\_数据文件夹。</span><span class="sxs-lookup"><span data-stu-id="0217a-133">After you create the new database, you can open the database by double-clicking the MoviesDB.mdf file in the App\_Data folder.</span></span> <span data-ttu-id="0217a-134">双击 MoviesDB.mdf 文件会打开服务器资源管理器窗口 （请参见图 2）。</span><span class="sxs-lookup"><span data-stu-id="0217a-134">Double-clicking the MoviesDB.mdf file opens the Server Explorer window (see Figure 2).</span></span>


|   | <span data-ttu-id="0217a-135">使用 Visual Web Developer 时，服务器资源管理器窗口称为数据库资源管理器窗口。</span><span class="sxs-lookup"><span data-stu-id="0217a-135">The Server Explorer window is called the Database Explorer window when using Visual Web Developer.</span></span> |
|---|----------------------------------------------------------------------------------------------------|
|   |                                                                                                    |

<span data-ttu-id="0217a-136">[![使用服务器资源管理器窗口](creating-model-classes-with-linq-to-sql-vb/_static/image5.png)](creating-model-classes-with-linq-to-sql-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="0217a-136">[![Using the Server Explorer window](creating-model-classes-with-linq-to-sql-vb/_static/image5.png)](creating-model-classes-with-linq-to-sql-vb/_static/image4.png)</span></span>

<span data-ttu-id="0217a-137">**图 02**:使用服务器资源管理器窗口 ([单击此项可查看原尺寸图像](creating-model-classes-with-linq-to-sql-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="0217a-137">**Figure 02**: Using the Server Explorer window ([Click to view full-size image](creating-model-classes-with-linq-to-sql-vb/_static/image6.png))</span></span>


<span data-ttu-id="0217a-138">我们需要将表添加到我们代表我们的电影的数据库。</span><span class="sxs-lookup"><span data-stu-id="0217a-138">We need to add one table to our database that represents our movies.</span></span> <span data-ttu-id="0217a-139">右键单击表文件夹，然后选择菜单选项**添加新表**。</span><span class="sxs-lookup"><span data-stu-id="0217a-139">Right-click the Tables folder and select the menu option **Add New Table**.</span></span> <span data-ttu-id="0217a-140">选择此菜单选项打开表设计器 （请参见图 3）。</span><span class="sxs-lookup"><span data-stu-id="0217a-140">Selecting this menu option opens the Table Designer (see Figure 3).</span></span>


<span data-ttu-id="0217a-141">[![使用服务器资源管理器窗口](creating-model-classes-with-linq-to-sql-vb/_static/image8.png)](creating-model-classes-with-linq-to-sql-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="0217a-141">[![Using the Server Explorer window](creating-model-classes-with-linq-to-sql-vb/_static/image8.png)](creating-model-classes-with-linq-to-sql-vb/_static/image7.png)</span></span>

<span data-ttu-id="0217a-142">**图 03**:表设计器 ([单击此项可查看原尺寸图像](creating-model-classes-with-linq-to-sql-vb/_static/image9.png))</span><span class="sxs-lookup"><span data-stu-id="0217a-142">**Figure 03**: The Table Designer ([Click to view full-size image](creating-model-classes-with-linq-to-sql-vb/_static/image9.png))</span></span>


<span data-ttu-id="0217a-143">我们需要向数据库表添加以下列：</span><span class="sxs-lookup"><span data-stu-id="0217a-143">We need to add the following columns to our database table:</span></span>

| <span data-ttu-id="0217a-144">**列名称**</span><span class="sxs-lookup"><span data-stu-id="0217a-144">**Column Name**</span></span> | <span data-ttu-id="0217a-145">**数据类型**</span><span class="sxs-lookup"><span data-stu-id="0217a-145">**Data Type**</span></span> | <span data-ttu-id="0217a-146">**允许 null 值**</span><span class="sxs-lookup"><span data-stu-id="0217a-146">**Allow Nulls**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0217a-147">Id</span><span class="sxs-lookup"><span data-stu-id="0217a-147">Id</span></span> | <span data-ttu-id="0217a-148">Int</span><span class="sxs-lookup"><span data-stu-id="0217a-148">Int</span></span> | <span data-ttu-id="0217a-149">False</span><span class="sxs-lookup"><span data-stu-id="0217a-149">False</span></span> |
| <span data-ttu-id="0217a-150">标题</span><span class="sxs-lookup"><span data-stu-id="0217a-150">Title</span></span> | <span data-ttu-id="0217a-151">Nvarchar(200)</span><span class="sxs-lookup"><span data-stu-id="0217a-151">Nvarchar(200)</span></span> | <span data-ttu-id="0217a-152">False</span><span class="sxs-lookup"><span data-stu-id="0217a-152">False</span></span> |
| <span data-ttu-id="0217a-153">主管</span><span class="sxs-lookup"><span data-stu-id="0217a-153">Director</span></span> | <span data-ttu-id="0217a-154">Nvarchar(50)</span><span class="sxs-lookup"><span data-stu-id="0217a-154">Nvarchar(50)</span></span> | <span data-ttu-id="0217a-155">False</span><span class="sxs-lookup"><span data-stu-id="0217a-155">False</span></span> |

<span data-ttu-id="0217a-156">需要两个特殊对执行的操作 Id 列。</span><span class="sxs-lookup"><span data-stu-id="0217a-156">You need to do two special things to the Id column.</span></span> <span data-ttu-id="0217a-157">首先，需要将 Id 列作为主键列标记通过在表设计器中选择列并单击密钥图标。</span><span class="sxs-lookup"><span data-stu-id="0217a-157">First, you need to mark the Id column as a primary key column by selecting the column in the Table Designer and clicking the icon of a key.</span></span> <span data-ttu-id="0217a-158">LINQ to SQL 要求您在执行插入或更新对数据库时指定主键列。</span><span class="sxs-lookup"><span data-stu-id="0217a-158">LINQ to SQL requires you to specify your primary key columns when performing inserts or updates against the database.</span></span>

<span data-ttu-id="0217a-159">接下来，需要将 Id 列标记为标识列中，通过是将值分配给**是标识**属性 （请参见图 3）。</span><span class="sxs-lookup"><span data-stu-id="0217a-159">Next, you need to mark the Id column as an Identity column by assigning the value Yes to the **Is Identity** property (see Figure 3).</span></span> <span data-ttu-id="0217a-160">标识列是自动分配新的数字，只要将新的数据行添加到表的列。</span><span class="sxs-lookup"><span data-stu-id="0217a-160">An Identity column is a column that is assigned a new number automatically whenever you add a new row of data to a table.</span></span>

<span data-ttu-id="0217a-161">进行这些更改后，请使用名称 tblMovie 保存该表。</span><span class="sxs-lookup"><span data-stu-id="0217a-161">After you make these changes, save the table with the name tblMovie.</span></span> <span data-ttu-id="0217a-162">您可以通过单击保存按钮保存表。</span><span class="sxs-lookup"><span data-stu-id="0217a-162">You can save the table by clicking the Save button.</span></span>

## <a name="create-linq-to-sql-classes"></a><span data-ttu-id="0217a-163">创建 LINQ to SQL 类</span><span class="sxs-lookup"><span data-stu-id="0217a-163">Create LINQ to SQL Classes</span></span>

<span data-ttu-id="0217a-164">我们的 MVC 模型将包含 LINQ to SQL 类表示 tblMovie 数据库表。</span><span class="sxs-lookup"><span data-stu-id="0217a-164">Our MVC model will contain LINQ to SQL classes that represent the tblMovie database table.</span></span> <span data-ttu-id="0217a-165">若要创建这些 LINQ to SQL 类的最简单方法是右键单击 Models 文件夹中，选择**添加、 新建项**，选择的 LINQ to SQL 类模板，为指定类名称 Movie.dbml，然后单击**添加**按钮 （请参见图 4）。</span><span class="sxs-lookup"><span data-stu-id="0217a-165">The easiest way to create these LINQ to SQL classes is to right-click the Models folder, select **Add, New Item**, select the LINQ to SQL Classes template, give the classes the name Movie.dbml, and click the **Add** button (see Figure 4).</span></span>


<span data-ttu-id="0217a-166">[![创建 LINQ to SQL 类](creating-model-classes-with-linq-to-sql-vb/_static/image11.png)](creating-model-classes-with-linq-to-sql-vb/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="0217a-166">[![Creating LINQ to SQL classes](creating-model-classes-with-linq-to-sql-vb/_static/image11.png)](creating-model-classes-with-linq-to-sql-vb/_static/image10.png)</span></span>

<span data-ttu-id="0217a-167">**图 04**:创建 LINQ to SQL 类 ([单击此项可查看原尺寸图像](creating-model-classes-with-linq-to-sql-vb/_static/image12.png))</span><span class="sxs-lookup"><span data-stu-id="0217a-167">**Figure 04**: Creating LINQ to SQL classes ([Click to view full-size image](creating-model-classes-with-linq-to-sql-vb/_static/image12.png))</span></span>


<span data-ttu-id="0217a-168">立即创建电影 LINQ to SQL 类后，将显示对象关系设计器。</span><span class="sxs-lookup"><span data-stu-id="0217a-168">Immediately after you create the Movie LINQ to SQL Classes, the Object Relational Designer appears.</span></span> <span data-ttu-id="0217a-169">可以将数据库表拖到对象关系设计器创建 LINQ to SQL 类表示特定的数据库表上服务器资源管理器窗口中。</span><span class="sxs-lookup"><span data-stu-id="0217a-169">You can drag database tables from the Server Explorer window onto the Object Relational Designer to create LINQ to SQL Classes that represent particular database tables.</span></span> <span data-ttu-id="0217a-170">我们需要添加到对象关系设计器上的 tblMovie 数据库表 （请参阅图 4）。</span><span class="sxs-lookup"><span data-stu-id="0217a-170">We need to add the tblMovie database table onto the Object Relational Designer (see Figure 4).</span></span>


<span data-ttu-id="0217a-171">[![使用对象关系设计器](creating-model-classes-with-linq-to-sql-vb/_static/image14.png)](creating-model-classes-with-linq-to-sql-vb/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="0217a-171">[![Using the Object Relational Designer](creating-model-classes-with-linq-to-sql-vb/_static/image14.png)](creating-model-classes-with-linq-to-sql-vb/_static/image13.png)</span></span>

<span data-ttu-id="0217a-172">**图 05**:使用对象关系设计器 ([单击此项可查看原尺寸图像](creating-model-classes-with-linq-to-sql-vb/_static/image15.png))</span><span class="sxs-lookup"><span data-stu-id="0217a-172">**Figure 05**: Using the Object Relational Designer ([Click to view full-size image](creating-model-classes-with-linq-to-sql-vb/_static/image15.png))</span></span>


<span data-ttu-id="0217a-173">默认情况下，对象关系设计器创建一个类具有与数据库表拖到设计器上完全相同的名称。</span><span class="sxs-lookup"><span data-stu-id="0217a-173">By default, the Object Relational Designer creates a class with the very same name as the database table that you drag onto the Designer.</span></span> <span data-ttu-id="0217a-174">但是，我们不想要调用我们类 tblMovie。</span><span class="sxs-lookup"><span data-stu-id="0217a-174">However, we don't want to call our class tblMovie.</span></span> <span data-ttu-id="0217a-175">因此，单击设计器中的类的名称，并将类的名称更改为电影。</span><span class="sxs-lookup"><span data-stu-id="0217a-175">Therefore, click the name of the class in the Designer and change the name of the class to Movie.</span></span>

<span data-ttu-id="0217a-176">最后，请记住单击**保存**按钮 （将软盘保存图片） 以保存 LINQ to SQL 类。</span><span class="sxs-lookup"><span data-stu-id="0217a-176">Finally, remember to click the **Save** button (the picture of the floppy) to save the LINQ to SQL Classes.</span></span> <span data-ttu-id="0217a-177">否则，不会通过对象关系设计器生成 LINQ to SQL 类。</span><span class="sxs-lookup"><span data-stu-id="0217a-177">Otherwise, the LINQ to SQL Classes won't be generated by the Object Relational Designer.</span></span>

## <a name="using-linq-to-sql-in-a-controller-action"></a><span data-ttu-id="0217a-178">在控制器操作中使用 LINQ to SQL</span><span class="sxs-lookup"><span data-stu-id="0217a-178">Using LINQ to SQL in a Controller Action</span></span>

<span data-ttu-id="0217a-179">现在，我们有我们 LINQ to SQL 类，我们可以使用这些类以从数据库检索数据。</span><span class="sxs-lookup"><span data-stu-id="0217a-179">Now that we have our LINQ to SQL classes, we can use these classes to retrieve data from the database.</span></span> <span data-ttu-id="0217a-180">在本部分中，您将了解如何使用 LINQ to SQL 类直接在控制器操作中。</span><span class="sxs-lookup"><span data-stu-id="0217a-180">In this section, you learn how to use LINQ to SQL classes directly within a controller action.</span></span> <span data-ttu-id="0217a-181">我们将一个 MVC 视图中显示 tblMovies 数据库表中的电影的列表。</span><span class="sxs-lookup"><span data-stu-id="0217a-181">We'll display the list of movies from the tblMovies database table in an MVC view.</span></span>

<span data-ttu-id="0217a-182">首先，我们需要修改 HomeController 类。</span><span class="sxs-lookup"><span data-stu-id="0217a-182">First, we need to modify the HomeController class.</span></span> <span data-ttu-id="0217a-183">可以在你的应用程序的控制器文件夹中找到此类。</span><span class="sxs-lookup"><span data-stu-id="0217a-183">This class can be found in the Controllers folder of your application.</span></span> <span data-ttu-id="0217a-184">修改类，以使它看起来像列表 1 中的类。</span><span class="sxs-lookup"><span data-stu-id="0217a-184">Modify the class so it looks like the class in Listing 1.</span></span>

<span data-ttu-id="0217a-185">**代码清单 1 – `Controllers\HomeController.vb`**</span><span class="sxs-lookup"><span data-stu-id="0217a-185">**Listing 1 – `Controllers\HomeController.vb`**</span></span>

[!code-vb[Main](creating-model-classes-with-linq-to-sql-vb/samples/sample1.vb)]

<span data-ttu-id="0217a-186">在列表 1 中的 index （） 操作使用 LINQ to SQL DataContext 类 (MovieDataContext) 来表示 MoviesDB 数据库。</span><span class="sxs-lookup"><span data-stu-id="0217a-186">The Index() action in Listing 1 uses a LINQ to SQL DataContext class (the MovieDataContext) to represent the MoviesDB database.</span></span> <span data-ttu-id="0217a-187">在 Visual Studio 对象关系设计器生成 MoveDataContext 类。</span><span class="sxs-lookup"><span data-stu-id="0217a-187">The MoveDataContext class was generated by the Visual Studio Object Relational Designer.</span></span>

<span data-ttu-id="0217a-188">对 DataContext tblMovies 数据库表中检索所有电影执行 LINQ 查询。</span><span class="sxs-lookup"><span data-stu-id="0217a-188">A LINQ query is performed against the DataContext to retrieve all of the movies from the tblMovies database table.</span></span> <span data-ttu-id="0217a-189">电影列表分配给一个名为电影的本地变量。</span><span class="sxs-lookup"><span data-stu-id="0217a-189">The list of movies is assigned to a local variable named movies.</span></span> <span data-ttu-id="0217a-190">最后，电影列表是通过传递给视图查看数据。</span><span class="sxs-lookup"><span data-stu-id="0217a-190">Finally, the list of movies is passed to the view through view data.</span></span>

<span data-ttu-id="0217a-191">为了显示电影，我们接下来需要修改索引视图。</span><span class="sxs-lookup"><span data-stu-id="0217a-191">In order to show the movies, we next need to modify the Index view.</span></span> <span data-ttu-id="0217a-192">可以在 Views\Home\ 文件夹中找到索引视图。</span><span class="sxs-lookup"><span data-stu-id="0217a-192">You can find the Index view in the Views\Home\ folder.</span></span> <span data-ttu-id="0217a-193">更新索引视图，使它看起来像列表 2 中的视图。</span><span class="sxs-lookup"><span data-stu-id="0217a-193">Update the Index view so that it looks like the view in Listing 2.</span></span>

<span data-ttu-id="0217a-194">**代码清单 2 – `Views\Home\Index.aspx`**</span><span class="sxs-lookup"><span data-stu-id="0217a-194">**Listing 2 – `Views\Home\Index.aspx`**</span></span>

[!code-aspx[Main](creating-model-classes-with-linq-to-sql-vb/samples/sample2.aspx)]

<span data-ttu-id="0217a-195">请注意，包含经过修改的索引视图&lt;%@ 导入命名空间 %&gt;指令在视图的顶部。</span><span class="sxs-lookup"><span data-stu-id="0217a-195">Notice that the modified Index view includes an &lt;%@ import namespace %&gt; directive at the top of the view.</span></span> <span data-ttu-id="0217a-196">此指令将导入 MvcApplication1 命名空间。</span><span class="sxs-lookup"><span data-stu-id="0217a-196">This directive imports the MvcApplication1 namespace.</span></span> <span data-ttu-id="0217a-197">若要使用模型类-具体而言，Movie 类-在视图中的，我们需要此命名空间。</span><span class="sxs-lookup"><span data-stu-id="0217a-197">We need this namespace in order to work with the model classes – in particular, the Movie class -- in the view.</span></span>

<span data-ttu-id="0217a-198">代码清单 2 中的视图包含一个 For Each 循环，循环访问所有由 ViewData.Model 属性表示的项。</span><span class="sxs-lookup"><span data-stu-id="0217a-198">The view in Listing 2 contains a For Each loop that iterates through all of the items represented by the ViewData.Model property.</span></span> <span data-ttu-id="0217a-199">Title 属性的值显示为每个电影。</span><span class="sxs-lookup"><span data-stu-id="0217a-199">The value of the Title property is displayed for each movie.</span></span>

<span data-ttu-id="0217a-200">请注意 ViewData.Model 属性的值被强制转换为 IEnumerable。</span><span class="sxs-lookup"><span data-stu-id="0217a-200">Notice that the value of the ViewData.Model property is cast to an IEnumerable.</span></span> <span data-ttu-id="0217a-201">这是必要的以遍历 ViewData.Model 的内容。</span><span class="sxs-lookup"><span data-stu-id="0217a-201">This is necessary in order to loop through the contents of ViewData.Model.</span></span> <span data-ttu-id="0217a-202">此处的另一个选项是创建强类型视图。</span><span class="sxs-lookup"><span data-stu-id="0217a-202">Another option here is to create a strongly-typed view.</span></span> <span data-ttu-id="0217a-203">创建强类型化视图时，转换为特定类型的 ViewData.Model 属性视图的代码隐藏类中。</span><span class="sxs-lookup"><span data-stu-id="0217a-203">When you create a strongly-typed view, you cast the ViewData.Model property to a particular type in a view's code-behind class.</span></span>

<span data-ttu-id="0217a-204">如果运行的应用程序后修改 HomeController 类和索引视图，则会收到一个空白页。</span><span class="sxs-lookup"><span data-stu-id="0217a-204">If you run the application after modifying the HomeController class and the Index view then you will get a blank page.</span></span> <span data-ttu-id="0217a-205">由于 tblMovies 数据库表中没有任何电影记录，你将获得一个空白页。</span><span class="sxs-lookup"><span data-stu-id="0217a-205">You'll get a blank page because there are no movie records in the tblMovies database table.</span></span>

<span data-ttu-id="0217a-206">若要将记录添加到 tblMovies 数据库表中，右键单击服务器资源管理器窗口 （在 Visual Web Developer 中的数据库资源管理器窗口） 中的 tblMovies 数据库表并选择菜单选项**显示表数据**。</span><span class="sxs-lookup"><span data-stu-id="0217a-206">In order to add records to the tblMovies database table, right-click the tblMovies database table in the Server Explorer window (Database Explorer window in Visual Web Developer) and select the menu option **Show Table Data**.</span></span> <span data-ttu-id="0217a-207">使用的网格中显示 （见图 5），可以将电影记录。</span><span class="sxs-lookup"><span data-stu-id="0217a-207">You can insert movie records by using the grid that appears (see Figure 5).</span></span>


<span data-ttu-id="0217a-208">[![插入电影](creating-model-classes-with-linq-to-sql-vb/_static/image17.png)](creating-model-classes-with-linq-to-sql-vb/_static/image16.png)</span><span class="sxs-lookup"><span data-stu-id="0217a-208">[![Inserting movies](creating-model-classes-with-linq-to-sql-vb/_static/image17.png)](creating-model-classes-with-linq-to-sql-vb/_static/image16.png)</span></span>

<span data-ttu-id="0217a-209">**图 06**:插入电影 ([单击此项可查看原尺寸图像](creating-model-classes-with-linq-to-sql-vb/_static/image18.png))</span><span class="sxs-lookup"><span data-stu-id="0217a-209">**Figure 06**: Inserting movies([Click to view full-size image](creating-model-classes-with-linq-to-sql-vb/_static/image18.png))</span></span>


<span data-ttu-id="0217a-210">将某些数据库记录添加到 tblMovies 表，并运行应用程序后，您将看到在图 7 中的页。</span><span class="sxs-lookup"><span data-stu-id="0217a-210">After you add some database records to the tblMovies table, and you run the application, you'll see the page in Figure 7.</span></span> <span data-ttu-id="0217a-211">项目符号列表中将显示所有电影数据库记录。</span><span class="sxs-lookup"><span data-stu-id="0217a-211">All of the movie database records are displayed in a bulleted list.</span></span>


<span data-ttu-id="0217a-212">[![显示与索引视图的电影](creating-model-classes-with-linq-to-sql-vb/_static/image20.png)](creating-model-classes-with-linq-to-sql-vb/_static/image19.png)</span><span class="sxs-lookup"><span data-stu-id="0217a-212">[![Displaying movies with the Index view](creating-model-classes-with-linq-to-sql-vb/_static/image20.png)](creating-model-classes-with-linq-to-sql-vb/_static/image19.png)</span></span>

<span data-ttu-id="0217a-213">**图 07**:显示与索引视图的电影 ([单击此项可查看原尺寸图像](creating-model-classes-with-linq-to-sql-vb/_static/image21.png))</span><span class="sxs-lookup"><span data-stu-id="0217a-213">**Figure 07**: Displaying movies with the Index view([Click to view full-size image](creating-model-classes-with-linq-to-sql-vb/_static/image21.png))</span></span>


## <a name="using-the-repository-pattern"></a><span data-ttu-id="0217a-214">使用存储库模式</span><span class="sxs-lookup"><span data-stu-id="0217a-214">Using the Repository Pattern</span></span>

<span data-ttu-id="0217a-215">在上一节中，我们使用 LINQ to SQL 类直接在控制器操作中。</span><span class="sxs-lookup"><span data-stu-id="0217a-215">In the previous section, we used LINQ to SQL classes directly within a controller action.</span></span> <span data-ttu-id="0217a-216">我们使用直接从 index （） 控制器操作 MovieDataContext 类。</span><span class="sxs-lookup"><span data-stu-id="0217a-216">We used the MovieDataContext class directly from the Index() controller action.</span></span> <span data-ttu-id="0217a-217">没有什么不妥执行此操作在简单的应用程序的情况下。</span><span class="sxs-lookup"><span data-stu-id="0217a-217">There is nothing wrong with doing this in the case of a simple application.</span></span> <span data-ttu-id="0217a-218">但是，在控制器类中直接使用 LINQ to SQL 的工作会产生问题时构建更复杂的应用程序所需。</span><span class="sxs-lookup"><span data-stu-id="0217a-218">However, working directly with LINQ to SQL in a controller class creates problems when you need to build a more complex application.</span></span>

<span data-ttu-id="0217a-219">使用 LINQ to SQL 是控制器类中难以在将来切换数据访问技术。</span><span class="sxs-lookup"><span data-stu-id="0217a-219">Using LINQ to SQL within a controller class makes it difficult to switch data access technologies in the future.</span></span> <span data-ttu-id="0217a-220">例如，您可能决定切换到使用作为数据访问技术的 Microsoft 实体框架使用 Microsoft LINQ to SQL。</span><span class="sxs-lookup"><span data-stu-id="0217a-220">For example, you might decide to switch from using Microsoft LINQ to SQL to using the Microsoft Entity Framework as your data access technology.</span></span> <span data-ttu-id="0217a-221">在这种情况下，你将需要重写访问该数据库在你的应用程序的每个控制器。</span><span class="sxs-lookup"><span data-stu-id="0217a-221">In that case, you would need to rewrite every controller that accesses the database within your application.</span></span>

<span data-ttu-id="0217a-222">控制器类中使用 LINQ to SQL 还使得难以构建你的应用程序的单元测试。</span><span class="sxs-lookup"><span data-stu-id="0217a-222">Using LINQ to SQL within a controller class also makes it difficult to build unit tests for your application.</span></span> <span data-ttu-id="0217a-223">通常情况下，您不想要执行单元测试时，与数据库交互。</span><span class="sxs-lookup"><span data-stu-id="0217a-223">Normally, you do not want to interact with a database when performing unit tests.</span></span> <span data-ttu-id="0217a-224">你想要使用你的单元测试来测试应用程序逻辑并不是你的数据库服务器。</span><span class="sxs-lookup"><span data-stu-id="0217a-224">You want to use your unit tests to test your application logic and not your database server.</span></span>

<span data-ttu-id="0217a-225">若要生成的 MVC 应用程序这是到未来的适应能力更强的更改和进行更轻松地测试，则应考虑使用存储库模式。</span><span class="sxs-lookup"><span data-stu-id="0217a-225">In order to build an MVC application that is more adaptable to future change and that can be more easily tested, you should consider using the Repository pattern.</span></span> <span data-ttu-id="0217a-226">当您使用的存储库模式时，您将创建包含所有数据库访问逻辑的一个独立的存储库类。</span><span class="sxs-lookup"><span data-stu-id="0217a-226">When you use the Repository pattern, you create a separate repository class that contains all of your database access logic.</span></span>

<span data-ttu-id="0217a-227">在创建存储库类，您将创建表示的所有存储库类使用的方法的接口。</span><span class="sxs-lookup"><span data-stu-id="0217a-227">When you create the repository class, you create an interface that represents all of the methods used by the repository class.</span></span> <span data-ttu-id="0217a-228">在你的控制器，您编写代码的依据而不是存储库的接口。</span><span class="sxs-lookup"><span data-stu-id="0217a-228">Within your controllers, you write your code against the interface instead of the repository.</span></span> <span data-ttu-id="0217a-229">这样一来，您可以实现在将来使用不同的数据访问技术的存储库。</span><span class="sxs-lookup"><span data-stu-id="0217a-229">That way, you can implement the repository using different data access technologies in the future.</span></span>

<span data-ttu-id="0217a-230">清单 3 中的接口名为 IMovieRepository，它表示名为 ListAll() 的单一方法。</span><span class="sxs-lookup"><span data-stu-id="0217a-230">The interface in Listing 3 is named IMovieRepository and it represents a single method named ListAll().</span></span>

<span data-ttu-id="0217a-231">**代码清单 3 – `Models\IMovieRepository.vb`**</span><span class="sxs-lookup"><span data-stu-id="0217a-231">**Listing 3 – `Models\IMovieRepository.vb`**</span></span>

[!code-vb[Main](creating-model-classes-with-linq-to-sql-vb/samples/sample3.vb)]

<span data-ttu-id="0217a-232">列表 4 中的存储库类实现 IMovieRepository 接口。</span><span class="sxs-lookup"><span data-stu-id="0217a-232">The repository class in Listing 4 implements the IMovieRepository interface.</span></span> <span data-ttu-id="0217a-233">请注意，它包含名为 ListAll() IMovieRepository 接口所需的方法对应的方法。</span><span class="sxs-lookup"><span data-stu-id="0217a-233">Notice that it contains a method named ListAll() that corresponds to the method required by the IMovieRepository interface.</span></span>

<span data-ttu-id="0217a-234">**列表 4 – `Models\MovieRepository.vb`**</span><span class="sxs-lookup"><span data-stu-id="0217a-234">**Listing 4 – `Models\MovieRepository.vb`**</span></span>

[!code-vb[Main](creating-model-classes-with-linq-to-sql-vb/samples/sample4.vb)]

<span data-ttu-id="0217a-235">最后，为 MoviesController 类列表 5 中的使用的存储库模式。</span><span class="sxs-lookup"><span data-stu-id="0217a-235">Finally, the MoviesController class in Listing 5 uses the Repository pattern.</span></span> <span data-ttu-id="0217a-236">它不能再使用 LINQ to SQL 类直接。</span><span class="sxs-lookup"><span data-stu-id="0217a-236">It no longer uses LINQ to SQL classes directly.</span></span>

<span data-ttu-id="0217a-237">**列表 5 – `Controllers\MoviesController.vb`**</span><span class="sxs-lookup"><span data-stu-id="0217a-237">**Listing 5 – `Controllers\MoviesController.vb`**</span></span>

[!code-vb[Main](creating-model-classes-with-linq-to-sql-vb/samples/sample5.vb)]

<span data-ttu-id="0217a-238">请注意，列表 5 中的为 MoviesController 类包含两个构造函数。</span><span class="sxs-lookup"><span data-stu-id="0217a-238">Notice that the MoviesController class in Listing 5 has two constructors.</span></span> <span data-ttu-id="0217a-239">第一个构造函数，无参数构造函数中，应用程序在运行时调用。</span><span class="sxs-lookup"><span data-stu-id="0217a-239">The first constructor, the parameterless constructor, is called when your application is running.</span></span> <span data-ttu-id="0217a-240">此构造函数创建 MovieRepository 类的实例，并将其传递给第二个构造函数。</span><span class="sxs-lookup"><span data-stu-id="0217a-240">This constructor creates an instance of the MovieRepository class and passes it to the second constructor.</span></span>

<span data-ttu-id="0217a-241">第二个构造函数具有单个参数： IMovieRepository 参数。</span><span class="sxs-lookup"><span data-stu-id="0217a-241">The second constructor has a single parameter: an IMovieRepository parameter.</span></span> <span data-ttu-id="0217a-242">此构造函数只需将参数的值分配给一个名为的类级字段\_存储库。</span><span class="sxs-lookup"><span data-stu-id="0217a-242">This constructor simply assigns the value of the parameter to a class-level field named \_repository.</span></span>

<span data-ttu-id="0217a-243">为 MoviesController 类利用称为依赖关系注入模式的软件设计模式。</span><span class="sxs-lookup"><span data-stu-id="0217a-243">The MoviesController class is taking advantage of a software design pattern called the Dependency Injection pattern.</span></span> <span data-ttu-id="0217a-244">具体而言，它使用称为构造函数依赖关系注入。</span><span class="sxs-lookup"><span data-stu-id="0217a-244">In particular, it is using something called Constructor Dependency Injection.</span></span> <span data-ttu-id="0217a-245">你可以阅读更多有关此模式通过阅读 Martin Fowler 的以下文章：</span><span class="sxs-lookup"><span data-stu-id="0217a-245">You can read more about this pattern by reading the following article by Martin Fowler:</span></span>

[http://martinfowler.com/articles/injection.html](http://martinfowler.com/articles/injection.html)

<span data-ttu-id="0217a-246">请注意，所有 （除了第一个构造函数） 为 MoviesController 类中的代码进行交互与 IMovieRepository 接口而不是实际 MovieRepository 类。</span><span class="sxs-lookup"><span data-stu-id="0217a-246">Notice that all of the code in the MoviesController class (with the exception of the first constructor) interacts with the IMovieRepository interface instead of the actual MovieRepository class.</span></span> <span data-ttu-id="0217a-247">与而不是接口的具体实现的抽象接口进行交互的代码。</span><span class="sxs-lookup"><span data-stu-id="0217a-247">The code interacts with an abstract interface instead of a concrete implementation of the interface.</span></span>

<span data-ttu-id="0217a-248">如果你想要修改应用程序使用的数据访问技术则可以只需实现使用备用数据库访问技术的类的 IMovieRepository 接口。</span><span class="sxs-lookup"><span data-stu-id="0217a-248">If you want to modify the data access technology used by the application then you can simply implement the IMovieRepository interface with a class that uses the alternative database access technology.</span></span> <span data-ttu-id="0217a-249">例如，可以创建 EntityFrameworkMovieRepository 类或 SubSonicMovieRepository 类。</span><span class="sxs-lookup"><span data-stu-id="0217a-249">For example, you could create an EntityFrameworkMovieRepository class or a SubSonicMovieRepository class.</span></span> <span data-ttu-id="0217a-250">由于控制器类针对接口进行编程，可以将 IMovieRepository 的新实现传递到控制器类和类将继续运行。</span><span class="sxs-lookup"><span data-stu-id="0217a-250">Because the controller class is programmed against the interface, you can pass a new implementation of IMovieRepository to the controller class and the class would continue to work.</span></span>

<span data-ttu-id="0217a-251">此外，如果你想要测试为 MoviesController 类，则可以为 MoviesController 传递假电影存储库类。</span><span class="sxs-lookup"><span data-stu-id="0217a-251">Furthermore, if you want to test the MoviesController class, then you can pass a fake movie repository class to the MoviesController.</span></span> <span data-ttu-id="0217a-252">您可以实现具有实际访问的数据库，但包含所有所需的 IMovieRepository 接口方法的类的 IMovieRepository 类。</span><span class="sxs-lookup"><span data-stu-id="0217a-252">You can implement the IMovieRepository class with a class that does not actually access the database but contains all of the required methods of the IMovieRepository interface.</span></span> <span data-ttu-id="0217a-253">这样一来，你可以无需实际访问的实际数据库单元测试为 MoviesController 类。</span><span class="sxs-lookup"><span data-stu-id="0217a-253">That way, you can unit test the MoviesController class without actually accessing a real database.</span></span>

## <a name="summary"></a><span data-ttu-id="0217a-254">总结</span><span class="sxs-lookup"><span data-stu-id="0217a-254">Summary</span></span>

<span data-ttu-id="0217a-255">本教程的目的是演示如何通过利用 Microsoft LINQ to SQL 创建 MVC 模型类。</span><span class="sxs-lookup"><span data-stu-id="0217a-255">The goal of this tutorial was to demonstrate how you can create MVC model classes by taking advantage of Microsoft LINQ to SQL.</span></span> <span data-ttu-id="0217a-256">在 ASP.NET MVC 应用程序中显示数据库数据的两种策略，我们探讨。</span><span class="sxs-lookup"><span data-stu-id="0217a-256">We examined two strategies for displaying database data in an ASP.NET MVC application.</span></span> <span data-ttu-id="0217a-257">首先，创建 LINQ to SQL 类，并使用直接在控制器操作中的类。</span><span class="sxs-lookup"><span data-stu-id="0217a-257">First, we created LINQ to SQL classes and used the classes directly within a controller action.</span></span> <span data-ttu-id="0217a-258">使用 LINQ to SQL 类在控制器内使你能够快速并轻松地在 MVC 应用程序中显示数据库数据。</span><span class="sxs-lookup"><span data-stu-id="0217a-258">Using LINQ to SQL classes within a controller enables you to quickly and easily display database data in an MVC application.</span></span>

<span data-ttu-id="0217a-259">接下来，我们探讨了显示数据库数据的稍微有些困难，但绝对更为良性的路径。</span><span class="sxs-lookup"><span data-stu-id="0217a-259">Next, we explored a slightly more difficult, but definitely more virtuous, path for displaying database data.</span></span> <span data-ttu-id="0217a-260">我们利用了存储库模式，并放在单独的存储库类中的所有我们数据库访问逻辑。</span><span class="sxs-lookup"><span data-stu-id="0217a-260">We took advantage of the Repository pattern and placed all of our database access logic in a separate repository class.</span></span> <span data-ttu-id="0217a-261">在我们控制器中，我们编写了所有我们针对而不是具体类的接口的代码。</span><span class="sxs-lookup"><span data-stu-id="0217a-261">In our controller, we wrote all of our code against an interface instead of a concrete class.</span></span> <span data-ttu-id="0217a-262">存储库模式的优点是它可让我们可以轻松地在将来更改数据库访问技术，并且它使我们能够轻松地测试了控制器类。</span><span class="sxs-lookup"><span data-stu-id="0217a-262">The advantage of the Repository pattern is that it enables us to easily change database access technologies in the future and it enables us to easily test our controller classes.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="0217a-263">[上一页](creating-model-classes-with-the-entity-framework-vb.md)
> [下一页](displaying-a-table-of-database-data-vb.md)</span><span class="sxs-lookup"><span data-stu-id="0217a-263">[Previous](creating-model-classes-with-the-entity-framework-vb.md)
[Next](displaying-a-table-of-database-data-vb.md)</span></span>

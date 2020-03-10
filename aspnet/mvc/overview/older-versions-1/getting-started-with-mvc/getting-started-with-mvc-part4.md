---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part4
title: 创建数据库 |Microsoft Docs
author: shanselman
description: 本教程介绍了 ASP.NET MVC 的基本知识。 创建一个从数据库中读取和写入数据的简单 web 应用程序。
ms.author: riande
ms.date: 08/14/2010
ms.assetid: 742df67f-484d-4ef3-af6b-8c791e556b43
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part4
msc.type: authoredcontent
ms.openlocfilehash: 995db714ce6365415d06dc458aee84a31c7c8fd6
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78469670"
---
# <a name="creating-a-database"></a><span data-ttu-id="d5c64-104">创建数据库</span><span class="sxs-lookup"><span data-stu-id="d5c64-104">Creating a Database</span></span>

<span data-ttu-id="d5c64-105">作者： [Scott Hanselman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="d5c64-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> <span data-ttu-id="d5c64-106">本教程介绍了 ASP.NET MVC 的基本知识。</span><span class="sxs-lookup"><span data-stu-id="d5c64-106">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="d5c64-107">你将创建一个简单的 web 应用程序，用于读取和写入数据库。</span><span class="sxs-lookup"><span data-stu-id="d5c64-107">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="d5c64-108">请访问[ASP.NET mvc 学习中心](../../../index.md)，查找其他 ASP.NET mvc 教程和示例。</span><span class="sxs-lookup"><span data-stu-id="d5c64-108">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>

<span data-ttu-id="d5c64-109">在本部分中，我们将创建一个新的 SQL Express 数据库，我们将使用它来存储和检索电影数据。</span><span class="sxs-lookup"><span data-stu-id="d5c64-109">In this section we are going to create a new SQL Express database that we'll use to store and retrieve our movie data.</span></span> <span data-ttu-id="d5c64-110">在 Visual Web Developer IDE 中，选择 "视图" |服务器资源管理器。</span><span class="sxs-lookup"><span data-stu-id="d5c64-110">From within the Visual Web Developer IDE, select View | Server Explorer.</span></span> <span data-ttu-id="d5c64-111">右键单击 "数据连接"，然后单击 "添加连接 ..."</span><span class="sxs-lookup"><span data-stu-id="d5c64-111">Right click on Data Connections and click Add Connection...</span></span>

![AddConnection](getting-started-with-mvc-part4/_static/image1.png)

<span data-ttu-id="d5c64-113">在 "选择数据源" 对话框中，选择 Microsoft SQL Server，然后选择 "继续"。</span><span class="sxs-lookup"><span data-stu-id="d5c64-113">In the Choose Data Source dialog, select Microsoft SQL Server and select Continue.</span></span>

![](getting-started-with-mvc-part4/_static/image2.png)

<span data-ttu-id="d5c64-114">在 "添加连接" 对话框中，输入 ".\SQLEXPRESS" 作为你的服务器名称，然后输入 "电影" 作为新数据库的名称。</span><span class="sxs-lookup"><span data-stu-id="d5c64-114">In the Add Connection dialog, enter ".\SQLEXPRESS" for your Server Name, and enter "Movies" as the name for your new database.</span></span>

<span data-ttu-id="d5c64-115">[!["添加连接" 对话框](getting-started-with-mvc-part4/_static/image4.png)](getting-started-with-mvc-part4/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="d5c64-115">[![Add Connection dialog](getting-started-with-mvc-part4/_static/image4.png)](getting-started-with-mvc-part4/_static/image3.png)</span></span>

<span data-ttu-id="d5c64-116">单击 "确定"，系统会询问您是否要创建该数据库。</span><span class="sxs-lookup"><span data-stu-id="d5c64-116">Click OK and you'll be asked if you want to create that database.</span></span> <span data-ttu-id="d5c64-117">选择 "是"。</span><span class="sxs-lookup"><span data-stu-id="d5c64-117">Select yes.</span></span>

<span data-ttu-id="d5c64-118">[![创建电影？](getting-started-with-mvc-part4/_static/image6.png)](getting-started-with-mvc-part4/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="d5c64-118">[![Create Movies?](getting-started-with-mvc-part4/_static/image6.png)](getting-started-with-mvc-part4/_static/image5.png)</span></span>

<span data-ttu-id="d5c64-119">现在，你已在服务器资源管理器中获取了一个空数据库。</span><span class="sxs-lookup"><span data-stu-id="d5c64-119">Now you've got an empty database in Server Explorer.</span></span>

![添加新表](getting-started-with-mvc-part4/_static/image7.png)

<span data-ttu-id="d5c64-121">右键单击表，然后单击 "添加表"。</span><span class="sxs-lookup"><span data-stu-id="d5c64-121">Right click on Tables and click Add Table.</span></span> <span data-ttu-id="d5c64-122">将显示表设计器。</span><span class="sxs-lookup"><span data-stu-id="d5c64-122">The Table Designer will appear.</span></span> <span data-ttu-id="d5c64-123">添加 Id、标题、ReleaseDate、流派和价格的列。</span><span class="sxs-lookup"><span data-stu-id="d5c64-123">Add columns for Id, Title, ReleaseDate, Genre, and Price.</span></span> <span data-ttu-id="d5c64-124">右键单击 ID 列，然后单击 "设置主键"。</span><span class="sxs-lookup"><span data-stu-id="d5c64-124">Right click on the ID column and click set Primary Key.</span></span> <span data-ttu-id="d5c64-125">我的设计区域如下所示。</span><span class="sxs-lookup"><span data-stu-id="d5c64-125">Here's what my design areas looks like.</span></span>

<span data-ttu-id="d5c64-126">[![数据库表编辑器](getting-started-with-mvc-part4/_static/image9.png)](getting-started-with-mvc-part4/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="d5c64-126">[![Database Table Editor](getting-started-with-mvc-part4/_static/image9.png)](getting-started-with-mvc-part4/_static/image8.png)</span></span>

<span data-ttu-id="d5c64-127">此外，选择 "Id" 列，然后在 "列属性" 下，将 "标识规范" 更改为 "是"。</span><span class="sxs-lookup"><span data-stu-id="d5c64-127">Also, select the Id column and under Column Properties below change "Identity Specification" to "Yes."</span></span>

<span data-ttu-id="d5c64-128">[![IsIdentity-列属性](getting-started-with-mvc-part4/_static/image11.png)](getting-started-with-mvc-part4/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="d5c64-128">[![IsIdentity - Column Properties](getting-started-with-mvc-part4/_static/image11.png)](getting-started-with-mvc-part4/_static/image10.png)</span></span>

<span data-ttu-id="d5c64-129">完成后，单击工具栏中的 "保存" 图标或选择 "文件" |从菜单中保存，并将表命名为 "**Movie**" （单数形式）。</span><span class="sxs-lookup"><span data-stu-id="d5c64-129">When you've got it done, click the Save icon in the toolbar or select File | Save from the menu, and name your table "**Movie**" (singular).</span></span> <span data-ttu-id="d5c64-130">我们已经有了一个数据库和一个表！</span><span class="sxs-lookup"><span data-stu-id="d5c64-130">We've got a database and a table!</span></span>

<span data-ttu-id="d5c64-131">[![选择名称](getting-started-with-mvc-part4/_static/image13.png)](getting-started-with-mvc-part4/_static/image12.png)</span><span class="sxs-lookup"><span data-stu-id="d5c64-131">[![Choose Name](getting-started-with-mvc-part4/_static/image13.png)](getting-started-with-mvc-part4/_static/image12.png)</span></span>

<span data-ttu-id="d5c64-132">返回服务器资源管理器，右键单击电影表，然后选择 "显示表数据"。</span><span class="sxs-lookup"><span data-stu-id="d5c64-132">Go back to Server Explorer and right click the Movie table, then select "Show Table Data."</span></span> <span data-ttu-id="d5c64-133">输入几个电影，以便我们的数据库具有一些数据。</span><span class="sxs-lookup"><span data-stu-id="d5c64-133">Enter a few movies so our database has some data.</span></span>

<span data-ttu-id="d5c64-134">[![数据库表编辑](getting-started-with-mvc-part4/_static/image15.png)](getting-started-with-mvc-part4/_static/image14.png)</span><span class="sxs-lookup"><span data-stu-id="d5c64-134">[![Database Table Editing](getting-started-with-mvc-part4/_static/image15.png)](getting-started-with-mvc-part4/_static/image14.png)</span></span>

## <a name="creating-a-model"></a><span data-ttu-id="d5c64-135">创建模型</span><span class="sxs-lookup"><span data-stu-id="d5c64-135">Creating a Model</span></span>

<span data-ttu-id="d5c64-136">现在，切换回 IDE 右端的解决方案资源管理器，右键单击 "模型" 文件夹，然后选择 "添加 |新建项。</span><span class="sxs-lookup"><span data-stu-id="d5c64-136">Now, switch back to the Solution Explorer on the right hand side of the IDE and right-click on the Models folder and select Add | New Item.</span></span>

<span data-ttu-id="d5c64-137">[![addnewmodelitem](getting-started-with-mvc-part4/_static/image17.png)](getting-started-with-mvc-part4/_static/image16.png)</span><span class="sxs-lookup"><span data-stu-id="d5c64-137">[![addnewmodelitem](getting-started-with-mvc-part4/_static/image17.png)](getting-started-with-mvc-part4/_static/image16.png)</span></span>

<span data-ttu-id="d5c64-138">我们将从新数据库创建实体模型。</span><span class="sxs-lookup"><span data-stu-id="d5c64-138">We're going to create an Entity Model from our new database.</span></span> <span data-ttu-id="d5c64-139">这会向项目中添加一组类，使我们可以轻松地查询和操作数据库中的数据。</span><span class="sxs-lookup"><span data-stu-id="d5c64-139">This will add a set of classes to our project that makes it easy for us to query and manipulate the data within our database.</span></span> <span data-ttu-id="d5c64-140">选择对话框左侧的 "数据" 节点，然后选择 "ADO.NET 实体数据模型项" 模板。</span><span class="sxs-lookup"><span data-stu-id="d5c64-140">Select the Data node on the left-hand side of the dialog, and then select the ADO.NET Entity Data Model item template.</span></span> <span data-ttu-id="d5c64-141">将其命名为 "电影"。</span><span class="sxs-lookup"><span data-stu-id="d5c64-141">Name it Movies.edmx.</span></span>

<span data-ttu-id="d5c64-142">[![AddNewDataModel](getting-started-with-mvc-part4/_static/image19.png)](getting-started-with-mvc-part4/_static/image18.png)</span><span class="sxs-lookup"><span data-stu-id="d5c64-142">[![AddNewDataModel](getting-started-with-mvc-part4/_static/image19.png)](getting-started-with-mvc-part4/_static/image18.png)</span></span>

<span data-ttu-id="d5c64-143">单击 "添加" 按钮。</span><span class="sxs-lookup"><span data-stu-id="d5c64-143">Click the "Add" button.</span></span> <span data-ttu-id="d5c64-144">然后，这将启动 "实体数据模型向导"。</span><span class="sxs-lookup"><span data-stu-id="d5c64-144">This will then launch the "Entity Data Model Wizard".</span></span>

<span data-ttu-id="d5c64-145">在弹出的新对话框中，选择 "从数据库生成"。</span><span class="sxs-lookup"><span data-stu-id="d5c64-145">In the new dialog that pops up, select Generate from Database.</span></span> <span data-ttu-id="d5c64-146">由于我们刚刚创建了一个数据库，因此，我们只需告诉实体框架我们的新数据库和表。</span><span class="sxs-lookup"><span data-stu-id="d5c64-146">Since we've just made a database, we'll only need to tell the Entity Framework about our new database and its table.</span></span> <span data-ttu-id="d5c64-147">单击 "下一步"，在 web 应用程序的配置中保存数据库连接。</span><span class="sxs-lookup"><span data-stu-id="d5c64-147">Click Next to save our database connection in our web application's configuration.</span></span> <span data-ttu-id="d5c64-148">现在，选中 "表和电影" 复选框，然后单击 "完成"。</span><span class="sxs-lookup"><span data-stu-id="d5c64-148">Now, check the Tables and Movie checkbox and click Finish.</span></span>

<span data-ttu-id="d5c64-149">[![实体数据模型向导](getting-started-with-mvc-part4/_static/image21.png)](getting-started-with-mvc-part4/_static/image20.png)</span><span class="sxs-lookup"><span data-stu-id="d5c64-149">[![Entity Data Model Wizard](getting-started-with-mvc-part4/_static/image21.png)](getting-started-with-mvc-part4/_static/image20.png)</span></span>

<span data-ttu-id="d5c64-150">现在，我们可以在 Entity Framework Designer 中看到新的电影表，并从代码访问它。</span><span class="sxs-lookup"><span data-stu-id="d5c64-150">Now we can see our new Movie table in the Entity Framework Designer and access it from code.</span></span>

<span data-ttu-id="d5c64-151">[![电影-Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part4/_static/image23.png)](getting-started-with-mvc-part4/_static/image22.png)</span><span class="sxs-lookup"><span data-stu-id="d5c64-151">[![Movies - Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part4/_static/image23.png)](getting-started-with-mvc-part4/_static/image22.png)</span></span>

<span data-ttu-id="d5c64-152">在设计图面上，您可以看到一个 "电影" 类。</span><span class="sxs-lookup"><span data-stu-id="d5c64-152">On the design surface you can see a "Movie" class.</span></span> <span data-ttu-id="d5c64-153">此类映射到数据库中的 "Movie" 表，其中的每个属性都映射到具有表的列。</span><span class="sxs-lookup"><span data-stu-id="d5c64-153">This class maps to the "Movie" table in our database, and each property within it maps to a column with the table.</span></span> <span data-ttu-id="d5c64-154">"Movie" 类的每个实例都对应于 "影片" 表中的一行。</span><span class="sxs-lookup"><span data-stu-id="d5c64-154">Each instance of a "Movie" class will correspond to a row within the "Movie" table.</span></span>

<span data-ttu-id="d5c64-155">如果你不喜欢实体框架使用的默认命名和映射约定，则可以使用实体框架设计器来更改或自定义它们。</span><span class="sxs-lookup"><span data-stu-id="d5c64-155">If you don't like the default naming and mapping conventions used by the Entity Framework, you can use the Entity Framework designer to change or customize them.</span></span> <span data-ttu-id="d5c64-156">对于此应用程序，我们将使用默认值，只需按原样保存文件。</span><span class="sxs-lookup"><span data-stu-id="d5c64-156">For this application we'll use the defaults and just save the file as-is.</span></span>

<span data-ttu-id="d5c64-157">现在，让我们处理一些真实的数据！</span><span class="sxs-lookup"><span data-stu-id="d5c64-157">Now, let's work with some real data!</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="d5c64-158">[上一页](getting-started-with-mvc-part3.md)
> [下一页](getting-started-with-mvc-part5.md)</span><span class="sxs-lookup"><span data-stu-id="d5c64-158">[Previous](getting-started-with-mvc-part3.md)
[Next](getting-started-with-mvc-part5.md)</span></span>

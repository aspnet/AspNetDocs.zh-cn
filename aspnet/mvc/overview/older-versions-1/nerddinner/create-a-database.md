---
uid: mvc/overview/older-versions-1/nerddinner/create-a-database
title: 创建数据库 | Microsoft Docs
author: rick-anderson
description: 步骤 2 显示了创建数据库的步骤，这些数据库包含我们 NerdDinner 应用程序的所有晚餐和 RSVP 数据。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 983f3ffa-08b8-4868-b8c9-aa34593fc683
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/create-a-database
msc.type: authoredcontent
ms.openlocfilehash: d0b87e4a6a27b37d2dbaa6d5b871da477b25586d
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541606"
---
# <a name="create-a-database"></a><span data-ttu-id="9ebe5-103">创建数据库</span><span class="sxs-lookup"><span data-stu-id="9ebe5-103">Create a Database</span></span>

<span data-ttu-id="9ebe5-104">由[微软](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="9ebe5-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="9ebe5-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="9ebe5-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="9ebe5-106">这是一个免费的["NerdDinner"应用程序教程](introducing-the-nerddinner-tutorial.md)的第2步，它介绍了如何使用 ASP.NETmVC 1构建小型但完整的Web应用程序。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-106">This is step 2 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="9ebe5-107">步骤 2 显示了创建数据库的步骤，这些数据库包含我们 NerdDinner 应用程序的所有晚餐和 RSVP 数据。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-107">Step 2 shows the steps to create the database holding all of the dinner and RSVP data for our NerdDinner application.</span></span>
> 
> <span data-ttu-id="9ebe5-108">如果您使用的是ASP.NET MVC 3，我们建议您按照[MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC 音乐商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程进行操作。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-2-creating-the-database"></a><span data-ttu-id="9ebe5-109">神经晚餐步骤 2：创建数据库</span><span class="sxs-lookup"><span data-stu-id="9ebe5-109">NerdDinner Step 2: Creating the Database</span></span>

<span data-ttu-id="9ebe5-110">我们将使用数据库来存储我们 NerdDinner 应用程序的所有晚餐和 RSVP 数据。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-110">We'll be using a database to store all of the Dinner and RSVP data for our NerdDinner application.</span></span>

<span data-ttu-id="9ebe5-111">以下步骤显示了使用免费 SQL Server Express 版本创建数据库（您可以使用[Microsoft Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)的 V2 轻松安装）。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-111">The steps below show creating the database using the free SQL Server Express edition (which you can easily install using V2 of the [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)).</span></span> <span data-ttu-id="9ebe5-112">我们将编写的所有代码都适用于 SQL Server Express 和完整 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-112">All of the code we'll write works with both SQL Server Express and the full SQL Server.</span></span>

### <a name="creating-a-new-sql-server-express-database"></a><span data-ttu-id="9ebe5-113">创建新的 SQL Server Express 数据库</span><span class="sxs-lookup"><span data-stu-id="9ebe5-113">Creating a new SQL Server Express database</span></span>

<span data-ttu-id="9ebe5-114">我们将从右键单击 Web 项目开始，然后选择 **"添加新&gt;项目"** 菜单命令：</span><span class="sxs-lookup"><span data-stu-id="9ebe5-114">We'll begin by right-clicking on our web project, and then select the **Add-&gt;New Item** menu command:</span></span>

![](create-a-database/_static/image1.png)

<span data-ttu-id="9ebe5-115">这将弹出可视化工作室的"添加新项目"对话框。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-115">This will bring up Visual Studio's "Add New Item" dialog.</span></span> <span data-ttu-id="9ebe5-116">我们将按"数据"类别进行筛选，然后选择"SQL 服务器数据库"项模板：</span><span class="sxs-lookup"><span data-stu-id="9ebe5-116">We'll filter by the "Data" category and select the "SQL Server Database" item template:</span></span>

![](create-a-database/_static/image2.png)

<span data-ttu-id="9ebe5-117">我们将命名要创建的 SQL Server Express 数据库"NerdDinner.mdf"，然后点击确定。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-117">We'll name the SQL Server Express database we want to create "NerdDinner.mdf" and hit ok.</span></span> <span data-ttu-id="9ebe5-118">然后，Visual Studio 会询问我们是否要将此文件添加到我们的 @App\_数据目录（该目录已设置包含读取和写入安全 ACL）：</span><span class="sxs-lookup"><span data-stu-id="9ebe5-118">Visual Studio will then ask us if we want to add this file to our \App\_Data directory (which is a directory already setup with both read and write security ACLs):</span></span>

![](create-a-database/_static/image3.png)

<span data-ttu-id="9ebe5-119">我们将单击"是"，我们将创建新数据库并将其添加到解决方案资源管理器中：</span><span class="sxs-lookup"><span data-stu-id="9ebe5-119">We'll click "Yes" and our new database will be created and added to our Solution Explorer:</span></span>

![](create-a-database/_static/image4.png)

### <a name="creating-tables-within-our-database"></a><span data-ttu-id="9ebe5-120">在我们的数据库中创建表</span><span class="sxs-lookup"><span data-stu-id="9ebe5-120">Creating Tables within our Database</span></span>

<span data-ttu-id="9ebe5-121">我们现在有一个新的空数据库。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-121">We now have a new empty database.</span></span> <span data-ttu-id="9ebe5-122">让我们向它添加一些表。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-122">Let's add some tables to it.</span></span>

<span data-ttu-id="9ebe5-123">为此，我们将导航到 Visual Studio 中的"服务器资源管理器"选项卡窗口，这使我们能够管理数据库和服务器。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-123">To do this we'll navigate to the "Server Explorer" tab window within Visual Studio, which enables us to manage databases and servers.</span></span> <span data-ttu-id="9ebe5-124">存储在应用程序的 @App\_数据文件夹中的 SQL Server Express 数据库将自动显示在服务器资源管理器中。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-124">SQL Server Express databases stored in the \App\_Data folder of our application will automatically show up within the Server Explorer.</span></span> <span data-ttu-id="9ebe5-125">我们可以选择使用"服务器资源管理器"窗口顶部的"连接到数据库"图标，将其他 SQL Server 数据库（本地数据库和远程数据库）添加到列表中：</span><span class="sxs-lookup"><span data-stu-id="9ebe5-125">We can optionally use the "Connect to Database" icon on the top of the "Server Explorer" window to add additional SQL Server databases (both local and remote) to the list as well:</span></span>

![](create-a-database/_static/image5.png)

<span data-ttu-id="9ebe5-126">我们将向 NerdDinner 数据库添加两个表 - 一个用于存储我们的晚餐，另一个用于跟踪 RSVP 接受的接收。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-126">We will add two tables to our NerdDinner database – one to store our Dinners, and the other to track RSVP acceptances to them.</span></span> <span data-ttu-id="9ebe5-127">我们可以通过右键单击数据库中的"表"文件夹并选择"添加新表"菜单命令来创建新表：</span><span class="sxs-lookup"><span data-stu-id="9ebe5-127">We can create new tables by right-clicking on the "Tables" folder within our database and choosing the "Add New Table" menu command:</span></span>

![](create-a-database/_static/image6.png)

<span data-ttu-id="9ebe5-128">这将打开一个表设计器，允许我们配置表的架构。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-128">This will open up a table designer that allows us to configure the schema of our table.</span></span> <span data-ttu-id="9ebe5-129">对于我们的"Dinners"表，我们将添加 10 列数据：</span><span class="sxs-lookup"><span data-stu-id="9ebe5-129">For our "Dinners" table we will add 10 columns of data:</span></span>

![](create-a-database/_static/image7.png)

<span data-ttu-id="9ebe5-130">我们希望"DinnerID"列是表的唯一主键。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-130">We want the "DinnerID" column to be a unique primary key for the table.</span></span> <span data-ttu-id="9ebe5-131">我们可以通过右键单击"DinnerID"列并选择"设置主键"菜单项来配置此项：</span><span class="sxs-lookup"><span data-stu-id="9ebe5-131">We can configure this by right-clicking on the "DinnerID" column and choosing the "Set Primary Key" menu item:</span></span>

![](create-a-database/_static/image8.png)

<span data-ttu-id="9ebe5-132">除了使 DinnerID 成为主键外，我们还希望将其配置为"标识"列，该列的值随着新数据行添加到表中而自动递增（这意味着第一个插入的 Dinner 行的 DinnerID 为 1，第二个插入的行的 DinnerID 为 2，等等）。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-132">In addition to making DinnerID a primary key, we also want configure it as an "identity" column whose value is automatically incremented as new rows of data are added to the table (meaning the first inserted Dinner row will have a DinnerID of 1, the second inserted row will have a DinnerID of 2, etc).</span></span>

<span data-ttu-id="9ebe5-133">为此，我们可以选择"DinnerID"列，然后使用"列属性"编辑器将列上的"（即标识）"属性设置为"是"。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-133">We can do this by selecting the "DinnerID" column and then use the "Column Properties" editor to set the "(Is Identity)" property on the column to "Yes".</span></span> <span data-ttu-id="9ebe5-134">我们将使用标准标识默认值（从 1 开始，在每个新的 Dinner 行上增加 1）：</span><span class="sxs-lookup"><span data-stu-id="9ebe5-134">We will use the standard identity defaults (start at 1 and increment 1 on each new Dinner row):</span></span>

![](create-a-database/_static/image9.png)

<span data-ttu-id="9ebe5-135">然后，我们将通过键入 Ctrl-S 或使用 **"文件保存"&gt;** 菜单命令来保存我们的表。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-135">We'll then save our table by typing Ctrl-S or by using the **File-&gt;Save** menu command.</span></span> <span data-ttu-id="9ebe5-136">这将提示我们命名表。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-136">This will prompt us to name the table.</span></span> <span data-ttu-id="9ebe5-137">我们将将其命名为"晚餐"：</span><span class="sxs-lookup"><span data-stu-id="9ebe5-137">We'll name it "Dinners":</span></span>

![](create-a-database/_static/image10.png)

<span data-ttu-id="9ebe5-138">然后，我们新的 Dinners 表将显示到服务器资源管理器中的数据库中。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-138">Our new Dinners table will then show up within our database in the server explorer.</span></span>

<span data-ttu-id="9ebe5-139">然后，我们将重复上述步骤，并创建一个"RSVP"表。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-139">We'll then repeat the above steps and create a "RSVP" table.</span></span> <span data-ttu-id="9ebe5-140">此表包含 3 列。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-140">This table with have 3 columns.</span></span> <span data-ttu-id="9ebe5-141">我们将将 RsvpID 列设置为主键，并使其成为标识列：</span><span class="sxs-lookup"><span data-stu-id="9ebe5-141">We will setup the RsvpID column as the primary key, and also make it an identity column:</span></span>

![](create-a-database/_static/image11.png)

<span data-ttu-id="9ebe5-142">我们将保存它，并给它的名字"RSVP"。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-142">We'll save it and give it the name "RSVP".</span></span>

### <a name="setting-up-a-foreign-key-relationship-between-tables"></a><span data-ttu-id="9ebe5-143">设置表之间的外键关系</span><span class="sxs-lookup"><span data-stu-id="9ebe5-143">Setting up a Foreign Key Relationship between Tables</span></span>

<span data-ttu-id="9ebe5-144">现在，我们的数据库中有两个表。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-144">We now have two tables within our database.</span></span> <span data-ttu-id="9ebe5-145">我们最后一个架构设计步骤是在这两个表之间建立"一对多"关系，以便我们可以将每个 Dinner 行与应用于它的零个或多个 RSVP 行相关联。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-145">Our last schema design step will be to setup a "one-to-many" relationship between these two tables – so that we can associate each Dinner row with zero or more RSVP rows that apply to it.</span></span> <span data-ttu-id="9ebe5-146">为此，我们将配置 RSVP 表的"DinnerID"列，以便与"Dinners"表中的"DinnerID"列具有外键关系。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-146">We will do this by configuring the RSVP table's "DinnerID" column to have a foreign-key relationship to the "DinnerID" column in the "Dinners" table.</span></span>

<span data-ttu-id="9ebe5-147">为此，我们将在服务器资源管理器中双击表设计器中打开 RSVP 表。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-147">To do this we'll open up the RSVP table within the table designer by double-clicking it in the server explorer.</span></span> <span data-ttu-id="9ebe5-148">然后，我们将选择其中的"DinnerID"列，右键单击，然后选择"关系..."上下文菜单命令：</span><span class="sxs-lookup"><span data-stu-id="9ebe5-148">We'll then select the "DinnerID" column within it, right-click, and choose the "Relationships…" context menu command:</span></span>

![](create-a-database/_static/image12.png)

<span data-ttu-id="9ebe5-149">这将弹出一个对话框，我们可以用它来设置表之间的关系：</span><span class="sxs-lookup"><span data-stu-id="9ebe5-149">This will bring up a dialog that we can use to setup relationships between tables:</span></span>

![](create-a-database/_static/image13.png)

<span data-ttu-id="9ebe5-150">我们将单击"添加"按钮以向对话框添加新关系。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-150">We'll click the "Add" button to add a new relationship to the dialog.</span></span> <span data-ttu-id="9ebe5-151">添加关系后，我们将将属性网格中的"表和列规范"树视图节点扩展到对话框的右侧，然后单击"..."按钮右侧：</span><span class="sxs-lookup"><span data-stu-id="9ebe5-151">Once a relationship has been added, we'll expand the "Tables and Column Specification" tree-view node within the property grid to the right of the dialog, and then click the "…" button to the right of it:</span></span>

![](create-a-database/_static/image14.png)

<span data-ttu-id="9ebe5-152">单击"..."按钮将弹出另一个对话框，允许我们指定关系中涉及哪些表和列，并允许我们命名关系。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-152">Clicking the "…" button will bring up another dialog that allows us to specify which tables and columns are involved in the relationship, as well as allow us to name the relationship.</span></span>

<span data-ttu-id="9ebe5-153">我们将主键表更改为"Dinners"，并选择"晚餐"表中的"DinnerID"列作为主键。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-153">We will change the Primary Key Table to be "Dinners", and select the "DinnerID" column within the Dinners table as the primary key.</span></span> <span data-ttu-id="9ebe5-154">我们的 RSVP 表将是外键表和 RSVP。DinnerID 列将作为外键关联：</span><span class="sxs-lookup"><span data-stu-id="9ebe5-154">Our RSVP table will be the foreign-key table, and the RSVP.DinnerID column will be associated as the foreign-key:</span></span>

![](create-a-database/_static/image15.png)

<span data-ttu-id="9ebe5-155">现在，RSVP 表中的每一行都将与"晚餐"表中的一行相关联。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-155">Now each row in the RSVP table will be associated with a row in the Dinner table.</span></span> <span data-ttu-id="9ebe5-156">SQL Server 将为我们保持参考完整性 ， 并且阻止我们添加新的 RSVP 行，如果它不指向有效的 Dinner 行。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-156">SQL Server will maintain referential integrity for us – and prevent us from adding a new RSVP row if it does not point to a valid Dinner row.</span></span> <span data-ttu-id="9ebe5-157">如果仍有 RSVP 行引用它，它也会阻止我们删除 Dinner 行。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-157">It will also prevent us from deleting a Dinner row if there are still RSVP rows referring to it.</span></span>

### <a name="adding-data-to-our-tables"></a><span data-ttu-id="9ebe5-158">将数据添加到我们的表</span><span class="sxs-lookup"><span data-stu-id="9ebe5-158">Adding Data to our Tables</span></span>

<span data-ttu-id="9ebe5-159">最后，让我们向"晚餐"表添加一些示例数据。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-159">Let's finish by adding some sample data to our Dinners table.</span></span> <span data-ttu-id="9ebe5-160">我们可以在服务器资源管理器中右键单击数据并选择"显示表数据"命令，将数据添加到表中：</span><span class="sxs-lookup"><span data-stu-id="9ebe5-160">We can add data to a table by right-clicking on it within the Server Explorer and choosing the "Show Table Data" command:</span></span>

![](create-a-database/_static/image16.png)

<span data-ttu-id="9ebe5-161">我们将添加几行 Dinner 数据，稍后在开始实现应用程序时可以使用这些数据：</span><span class="sxs-lookup"><span data-stu-id="9ebe5-161">We'll add a few rows of Dinner data that we can use later as we start implementing the application:</span></span>

![](create-a-database/_static/image17.png)

### <a name="next-step"></a><span data-ttu-id="9ebe5-162">下一步</span><span class="sxs-lookup"><span data-stu-id="9ebe5-162">Next Step</span></span>

<span data-ttu-id="9ebe5-163">我们已经完成了数据库的创建。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-163">We've finished creating our database.</span></span> <span data-ttu-id="9ebe5-164">现在，让我们创建模型类，可用于查询和更新它。</span><span class="sxs-lookup"><span data-stu-id="9ebe5-164">Let's now create model classes that we can use to query and update it.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="9ebe5-165">[上一页](create-a-new-aspnet-mvc-project.md)
> [下一页](build-a-model-with-business-rule-validations.md)</span><span class="sxs-lookup"><span data-stu-id="9ebe5-165">[Previous](create-a-new-aspnet-mvc-project.md)
[Next](build-a-model-with-business-rule-validations.md)</span></span>

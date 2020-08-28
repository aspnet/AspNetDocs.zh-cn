---
uid: mvc/overview/getting-started/introduction/adding-a-new-field
title: 添加新字段 |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 10/17/2013
ms.assetid: 4085de68-d243-4378-8a64-86236ea8d2da
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-a-new-field
msc.type: authoredcontent
ms.openlocfilehash: 7018de3eab9d7cced72c76d0b74a79f7c8154f9d
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045138"
---
# <a name="adding-a-new-field"></a><span data-ttu-id="3f66e-102">添加新字段</span><span class="sxs-lookup"><span data-stu-id="3f66e-102">Adding a New Field</span></span>

<span data-ttu-id="3f66e-103">作者： [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="3f66e-103">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[!INCLUDE [consider RP](~/includes/razor.md)]

<span data-ttu-id="3f66e-104">在本节中，您将使用 Entity Framework Code First 迁移将某些更改迁移到模型类，以便将更改应用到数据库。</span><span class="sxs-lookup"><span data-stu-id="3f66e-104">In this section you'll use Entity Framework Code First Migrations to migrate some changes to the model classes so the change is applied to the database.</span></span>

<span data-ttu-id="3f66e-105">默认情况下，当你使用实体框架 Code First 来自动创建数据库时（如在本教程前面的步骤中所做的那样），Code First 将向数据库中添加一个表，以帮助跟踪数据库的架构是否与生成它的模型类的架构同步。</span><span class="sxs-lookup"><span data-stu-id="3f66e-105">By default, when you use Entity Framework Code First to automatically create a database, as you did earlier in this tutorial, Code First adds a table to the database to help track whether the schema of the database is in sync with the model classes it was generated from.</span></span> <span data-ttu-id="3f66e-106">如果不同步，实体框架将引发错误。</span><span class="sxs-lookup"><span data-stu-id="3f66e-106">If they aren't in sync, the Entity Framework throws an error.</span></span> <span data-ttu-id="3f66e-107">这样，就可以更轻松地跟踪开发时的问题，否则，在运行时) 只会发现错误 (。</span><span class="sxs-lookup"><span data-stu-id="3f66e-107">This makes it easier to track down issues at development time that you might otherwise only find (by obscure errors) at run time.</span></span>

## <a name="setting-up-code-first-migrations-for-model-changes"></a><span data-ttu-id="3f66e-108">设置模型更改的 Code First 迁移</span><span class="sxs-lookup"><span data-stu-id="3f66e-108">Setting up Code First Migrations for Model Changes</span></span>

<span data-ttu-id="3f66e-109">导航到解决方案资源管理器。</span><span class="sxs-lookup"><span data-stu-id="3f66e-109">Navigate to Solution Explorer.</span></span> <span data-ttu-id="3f66e-110">右键单击 " *电影 .mdf* " 文件，然后选择 " **删除** " 以删除电影数据库。</span><span class="sxs-lookup"><span data-stu-id="3f66e-110">Right click on the *Movies.mdf* file and select **Delete** to remove the movies database.</span></span> <span data-ttu-id="3f66e-111">如果看不到 " *电影 .mdf* " 文件，请单击红色框中显示的 " **显示所有文件** " 图标。</span><span class="sxs-lookup"><span data-stu-id="3f66e-111">If you don't see the *Movies.mdf* file, click on the **Show All Files** icon shown below in the red outline.</span></span>

![](adding-a-new-field/_static/image1.png)

<span data-ttu-id="3f66e-112">生成应用程序，以确保没有任何错误。</span><span class="sxs-lookup"><span data-stu-id="3f66e-112">Build the application to make sure there are no errors.</span></span>

<span data-ttu-id="3f66e-113">在“工具”\*\*\*\* 菜单中，单击“NuGet 包管理器”\*\*\*\*，然后单击“包管理器控制台”\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="3f66e-113">From the **Tools** menu, click **NuGet Package Manager** and then **Package Manager Console**.</span></span>

![添加包手册](adding-a-new-field/_static/image2.png)

<span data-ttu-id="3f66e-115">在 " **程序包管理器控制台** " 窗口中，在 `PM>` 提示符处输入</span><span class="sxs-lookup"><span data-stu-id="3f66e-115">In the **Package Manager Console** window at the `PM>` prompt enter</span></span>

<span data-ttu-id="3f66e-116">启用-迁移-ContextTypeName MvcMovie. MovieDBContext</span><span class="sxs-lookup"><span data-stu-id="3f66e-116">Enable-Migrations -ContextTypeName MvcMovie.Models.MovieDBContext</span></span>

![](adding-a-new-field/_static/image3.png)

<span data-ttu-id="3f66e-117"> (上面显示的 "**启用-迁移**" 命令) 在新的*迁移*文件夹中创建*Configuration.cs*文件。</span><span class="sxs-lookup"><span data-stu-id="3f66e-117">The **Enable-Migrations** command (shown above) creates a *Configuration.cs* file in a new *Migrations* folder.</span></span>

![](adding-a-new-field/_static/image4.png)

<span data-ttu-id="3f66e-118">Visual Studio 将打开 *Configuration.cs* 文件。</span><span class="sxs-lookup"><span data-stu-id="3f66e-118">Visual Studio opens the *Configuration.cs* file.</span></span> <span data-ttu-id="3f66e-119">将 `Seed` *Configuration.cs* 文件中的方法替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="3f66e-119">Replace the `Seed` method in the *Configuration.cs* file with the following code:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample1.cs)]

<span data-ttu-id="3f66e-120">将鼠标悬停在下面的红色波浪线上 `Movie` ，并单击 `Show Potential Fixes` ，然后单击 " **使用** **MvcMovie"。**</span><span class="sxs-lookup"><span data-stu-id="3f66e-120">Hover over the red squiggly line under `Movie` and click `Show Potential Fixes` and then click **using** **MvcMovie.Models;**</span></span>

![](adding-a-new-field/_static/image5.png)

<span data-ttu-id="3f66e-121">这样做将添加以下 using 语句：</span><span class="sxs-lookup"><span data-stu-id="3f66e-121">Doing so adds the following using statement:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample2.cs)]

> [!NOTE]
> 
> <span data-ttu-id="3f66e-122">Code First 迁移将在 `Seed` 每次迁移后调用方法 (即，在包管理器控制台) 中调用 **更新数据库** ，此方法会更新已插入的行，如果它们尚不存在，则将其插入。</span><span class="sxs-lookup"><span data-stu-id="3f66e-122">Code First Migrations calls the `Seed` method after every migration (that is, calling **update-database** in the Package Manager Console), and this method updates rows that have already been inserted, or inserts them if they don't exist yet.</span></span>
> 
> <span data-ttu-id="3f66e-123">以下代码中的 [AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) 方法执行 "upsert" 操作：</span><span class="sxs-lookup"><span data-stu-id="3f66e-123">The [AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) method in the following code performs an "upsert" operation:</span></span>
> 
> [!code-csharp[Main](adding-a-new-field/samples/sample3.cs)]
> 
> <span data-ttu-id="3f66e-124">由于 [种子](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx) 方法随每个迁移一起运行，因此您不能只插入数据，因为在第一个创建数据库的迁移之后，您尝试添加的行将已存在。</span><span class="sxs-lookup"><span data-stu-id="3f66e-124">Because the [Seed](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx) method runs with every migration, you can't just insert data, because the rows you are trying to add will already be there after the first migration that creates the database.</span></span> <span data-ttu-id="3f66e-125">如果尝试插入已存在的行，"[upsert](http://en.wikipedia.org/wiki/Upsert)" 操作将会阻止发生的错误，但会覆盖在测试应用程序时对数据所做的任何更改。</span><span class="sxs-lookup"><span data-stu-id="3f66e-125">The "[upsert](http://en.wikipedia.org/wiki/Upsert)" operation prevents errors that would happen if you try to insert a row that already exists, but it overrides any changes to data that you may have made while testing the application.</span></span> <span data-ttu-id="3f66e-126">对于某些表中的测试数据，您可能不希望发生这种情况：在某些情况下，当您在测试时更改数据时，您希望在数据库更新后更改保持不变。</span><span class="sxs-lookup"><span data-stu-id="3f66e-126">With test data in some tables you might not want that to happen: in some cases when you change data while testing you want your changes to remain after database updates.</span></span> <span data-ttu-id="3f66e-127">在这种情况下，需要执行条件插入操作：仅在不存在行时插入行。</span><span class="sxs-lookup"><span data-stu-id="3f66e-127">In that case you want to do a conditional insert operation: insert a row only if it doesn't already exist.</span></span>   
> 
> <span data-ttu-id="3f66e-128">传递给 [AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) 方法的第一个参数指定要用于检查行是否已存在的属性。</span><span class="sxs-lookup"><span data-stu-id="3f66e-128">The first parameter passed to the [AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) method specifies the property to use to check if a row already exists.</span></span> <span data-ttu-id="3f66e-129">对于所提供的测试电影数据， `Title` 属性可用于此目的，因为列表中的每个标题都是唯一的：</span><span class="sxs-lookup"><span data-stu-id="3f66e-129">For the test movie data that you are providing, the `Title` property can be used for this purpose since each title in the list is unique:</span></span>
> 
> [!code-csharp[Main](adding-a-new-field/samples/sample4.cs)]
> 
> <span data-ttu-id="3f66e-130">此代码假设标题是唯一的。</span><span class="sxs-lookup"><span data-stu-id="3f66e-130">This code assumes that titles are unique.</span></span> <span data-ttu-id="3f66e-131">如果手动添加重复标题，则在下次执行迁移时，将会出现以下异常。</span><span class="sxs-lookup"><span data-stu-id="3f66e-131">If you manually add a duplicate title, you'll get the following exception the next time you perform a migration.</span></span>   
> 
> <span data-ttu-id="3f66e-132">*序列包含多个元素*</span><span class="sxs-lookup"><span data-stu-id="3f66e-132">*Sequence contains more than one element*</span></span>  
> 
> <span data-ttu-id="3f66e-133">有关 [AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) 方法的详细信息，请参阅 [使用 EF 4.3 AddOrUpdate 方法](http://thedatafarm.com/blog/data-access/take-care-with-ef-4-3-addorupdate-method/)。</span><span class="sxs-lookup"><span data-stu-id="3f66e-133">For more information about the [AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) method, see [Take care with EF 4.3 AddOrUpdate Method](http://thedatafarm.com/blog/data-access/take-care-with-ef-4-3-addorupdate-method/)..</span></span>

<span data-ttu-id="3f66e-134">**按 CTRL-SHIFT-B 生成项目。** (如果此时不生成，以下步骤将失败。 ) </span><span class="sxs-lookup"><span data-stu-id="3f66e-134">**Press CTRL-SHIFT-B to build the project.**(The following steps will fail if you don't build at this point.)</span></span>

<span data-ttu-id="3f66e-135">下一步是创建一个 `DbMigration` 用于初始迁移的类。</span><span class="sxs-lookup"><span data-stu-id="3f66e-135">The next step is to create a `DbMigration` class for the initial migration.</span></span> <span data-ttu-id="3f66e-136">此迁移创建新的数据库，这就是在上一步中删除了 *movie .mdf* 文件的原因。</span><span class="sxs-lookup"><span data-stu-id="3f66e-136">This migration creates a new database, that's why you deleted the *movie.mdf* file in a previous step.</span></span>

<span data-ttu-id="3f66e-137">在 " **程序包管理器控制台** " 窗口中，输入命令 `add-migration Initial` 以创建初始迁移。</span><span class="sxs-lookup"><span data-stu-id="3f66e-137">In the **Package Manager Console** window, enter the command `add-migration Initial` to create the initial migration.</span></span> <span data-ttu-id="3f66e-138">名称 "初始" 是任意名称，用于命名创建的迁移文件。</span><span class="sxs-lookup"><span data-stu-id="3f66e-138">The name "Initial" is arbitrary and is used to name the migration file created.</span></span>

![](adding-a-new-field/_static/image6.png)

<span data-ttu-id="3f66e-139">Code First 迁移在 " *迁移* " 文件夹中创建名为 *{日期戳} \_ Initial.cs* )  (的其他类文件，此类包含用于创建数据库架构的代码。</span><span class="sxs-lookup"><span data-stu-id="3f66e-139">Code First Migrations creates another class file in the *Migrations* folder (with the name *{DateStamp}\_Initial.cs* ), and this class contains code that creates the database schema.</span></span> <span data-ttu-id="3f66e-140">迁移文件名预先修复了时间戳，以帮助进行排序。</span><span class="sxs-lookup"><span data-stu-id="3f66e-140">The migration filename is pre-fixed with a timestamp to help with ordering.</span></span> <span data-ttu-id="3f66e-141">检查 *{日期戳} \_ Initial.cs* 文件，其中包含为 `Movies` 电影数据库创建表的说明。</span><span class="sxs-lookup"><span data-stu-id="3f66e-141">Examine the *{DateStamp}\_Initial.cs* file, it contains the instructions to create the `Movies` table for the Movie DB.</span></span> <span data-ttu-id="3f66e-142">在下面的说明中更新数据库时，此 *{日期戳} \_ Initial.cs* 文件将运行，并创建数据库架构。</span><span class="sxs-lookup"><span data-stu-id="3f66e-142">When you update the database in the instructions below, this *{DateStamp}\_Initial.cs* file will run and create the DB schema.</span></span> <span data-ttu-id="3f66e-143">然后， **Seed** 方法将运行以用测试数据填充数据库。</span><span class="sxs-lookup"><span data-stu-id="3f66e-143">Then the **Seed** method will run to populate the DB with test data.</span></span>

<span data-ttu-id="3f66e-144">在 " **包管理器控制台**" 中，输入 `update-database` 用于创建数据库的命令并运行 `Seed` 方法。</span><span class="sxs-lookup"><span data-stu-id="3f66e-144">In the **Package Manager Console**, enter the command `update-database` to create the database and run the `Seed` method.</span></span>

![](adding-a-new-field/_static/image7.png)

<span data-ttu-id="3f66e-145">如果您收到一条错误消息，指示表已存在并且无法创建，则可能是您在删除数据库之后和执行之前运行了该应用程序 `update-database` 。</span><span class="sxs-lookup"><span data-stu-id="3f66e-145">If you get an error that indicates a table already exists and can't be created, it is probably because you ran the application after you deleted the database and before you executed `update-database`.</span></span> <span data-ttu-id="3f66e-146">在这种情况下，请再次删除此 *电影 .mdf* 文件，然后重试该 `update-database` 命令。</span><span class="sxs-lookup"><span data-stu-id="3f66e-146">In that case, delete the *Movies.mdf* file again and retry the `update-database` command.</span></span> <span data-ttu-id="3f66e-147">如果仍出现错误，请删除 "迁移" 文件夹和内容，然后从本页顶部的说明开始 (*删除 ""* ，然后继续执行 "启用-迁移) 。</span><span class="sxs-lookup"><span data-stu-id="3f66e-147">If you still get an error, delete the migrations folder and contents then start with the instructions at the top of this page (that is delete the *Movies.mdf* file then proceed to Enable-Migrations).</span></span> <span data-ttu-id="3f66e-148">如果仍出现错误，请打开 SQL Server 对象资源管理器并从列表中删除数据库。</span><span class="sxs-lookup"><span data-stu-id="3f66e-148">If you still get an error, open SQL Server Object Explorer and remove the database from the list.</span></span>

<span data-ttu-id="3f66e-149">运行应用程序并导航到 */Movies* URL。</span><span class="sxs-lookup"><span data-stu-id="3f66e-149">Run the application and navigate to the */Movies* URL.</span></span> <span data-ttu-id="3f66e-150">将显示种子数据。</span><span class="sxs-lookup"><span data-stu-id="3f66e-150">The seed data is displayed.</span></span>

![](adding-a-new-field/_static/image8.png)

## <a name="adding-a-rating-property-to-the-movie-model"></a><span data-ttu-id="3f66e-151">向电影模型添加分级属性</span><span class="sxs-lookup"><span data-stu-id="3f66e-151">Adding a Rating Property to the Movie Model</span></span>

<span data-ttu-id="3f66e-152">首先将新的 `Rating` 属性添加到现有 `Movie` 类。</span><span class="sxs-lookup"><span data-stu-id="3f66e-152">Start by adding a new `Rating` property to the existing `Movie` class.</span></span> <span data-ttu-id="3f66e-153">打开 *Models\Movie.cs* 文件并添加 `Rating` 此属性，如下所示：</span><span class="sxs-lookup"><span data-stu-id="3f66e-153">Open the *Models\Movie.cs* file and add the `Rating` property like this one:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample5.cs)]

<span data-ttu-id="3f66e-154">完整的 `Movie` 类现在如以下代码所示：</span><span class="sxs-lookup"><span data-stu-id="3f66e-154">The complete `Movie` class now looks like the following code:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample6.cs?highlight=12)]

<span data-ttu-id="3f66e-155">按 Ctrl + Shift + B)  (生成应用程序。</span><span class="sxs-lookup"><span data-stu-id="3f66e-155">Build the application (Ctrl+Shift+B).</span></span>

<span data-ttu-id="3f66e-156">由于已将一个新字段添加到 `Movie` 类，因此还需要更新 "绑定" *白名单* ，以便包括此新属性。</span><span class="sxs-lookup"><span data-stu-id="3f66e-156">Because you've added a new field to the `Movie` class, you also need to update the binding *white list* so this new property will be included.</span></span> <span data-ttu-id="3f66e-157">更新的 `bind` 属性 `Create` 和 `Edit` 操作方法以包括 `Rating` 属性：</span><span class="sxs-lookup"><span data-stu-id="3f66e-157">Update the `bind` attribute for `Create` and `Edit` action methods to include the `Rating` property:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample7.cs?highlight=1)]

<span data-ttu-id="3f66e-158">还需要更新视图模板，以便在浏览器视图中显示、创建和编辑新的 `Rating` 属性。</span><span class="sxs-lookup"><span data-stu-id="3f66e-158">You also need to update the view templates in order to display, create and edit the new `Rating` property in the browser view.</span></span>

<span data-ttu-id="3f66e-159">打开 *\Views\Movies\Index.cshtml* 文件，并在 `<th>Rating</th>` " **Price** " 列后添加一个列标题。</span><span class="sxs-lookup"><span data-stu-id="3f66e-159">Open the *\Views\Movies\Index.cshtml* file and add a `<th>Rating</th>` column heading just after the **Price** column.</span></span> <span data-ttu-id="3f66e-160">然后在 `<td>` 模板末尾附近添加一个列，以呈现 `@item.Rating` 该值。</span><span class="sxs-lookup"><span data-stu-id="3f66e-160">Then add a `<td>` column near the end of the template to render the `@item.Rating` value.</span></span> <span data-ttu-id="3f66e-161">更新后的 *索引 cshtml* 视图模板如下所示：</span><span class="sxs-lookup"><span data-stu-id="3f66e-161">Below is what the updated *Index.cshtml* view template looks like:</span></span>

[!code-cshtml[Main](adding-a-new-field/samples/sample8.cshtml?highlight=31-33,52-54)]

<span data-ttu-id="3f66e-162">接下来，打开 *\Views\Movies\Create.cshtml* 文件并添加 `Rating` 具有以下突出显示的标记的字段。</span><span class="sxs-lookup"><span data-stu-id="3f66e-162">Next, open the *\Views\Movies\Create.cshtml* file and add the `Rating` field with the following highlighted markup.</span></span> <span data-ttu-id="3f66e-163">这将呈现一个文本框，以便您可以在创建新电影时指定级别。</span><span class="sxs-lookup"><span data-stu-id="3f66e-163">This renders a text box so that you can specify a rating when a new movie is created.</span></span>

[!code-cshtml[Main](adding-a-new-field/samples/sample9.cshtml?highlight=9-15)]

<span data-ttu-id="3f66e-164">现在，你已更新了应用程序代码以支持新 `Rating` 属性。</span><span class="sxs-lookup"><span data-stu-id="3f66e-164">You've now updated the application code to support the new `Rating` property.</span></span>

<span data-ttu-id="3f66e-165">运行应用程序并导航到 */Movies* URL。</span><span class="sxs-lookup"><span data-stu-id="3f66e-165">Run the application and navigate to the */Movies* URL.</span></span> <span data-ttu-id="3f66e-166">不过，当你执行此操作时，你将看到以下错误之一：</span><span class="sxs-lookup"><span data-stu-id="3f66e-166">When you do this, though, you'll see one of the following errors:</span></span>

![](adding-a-new-field/_static/image9.png)  
  
<span data-ttu-id="3f66e-167">创建数据库后，支持 "MovieDBContext" 上下文的模型已发生更改。</span><span class="sxs-lookup"><span data-stu-id="3f66e-167">The model backing the 'MovieDBContext' context has changed since the database was created.</span></span> <span data-ttu-id="3f66e-168">请考虑使用 Code First 迁移更新数据库 (https://go.microsoft.com/fwlink/?LinkId=238269) 。</span><span class="sxs-lookup"><span data-stu-id="3f66e-168">Consider using Code First Migrations to update the database (https://go.microsoft.com/fwlink/?LinkId=238269).</span></span>

![](adding-a-new-field/_static/image10.png)

<span data-ttu-id="3f66e-169">出现此错误的原因 `Movie` 是，应用程序中更新的模型类现在与现有数据库的表的架构不同 `Movie` 。</span><span class="sxs-lookup"><span data-stu-id="3f66e-169">You're seeing this error because the updated `Movie` model class in the application is now different than the schema of the `Movie` table of the existing database.</span></span> <span data-ttu-id="3f66e-170">（数据库表中没有 `Rating` 列。）</span><span class="sxs-lookup"><span data-stu-id="3f66e-170">(There's no `Rating` column in the database table.)</span></span>

<span data-ttu-id="3f66e-171">可通过几种方法解决此错误：</span><span class="sxs-lookup"><span data-stu-id="3f66e-171">There are a few approaches to resolving the error:</span></span>

1. <span data-ttu-id="3f66e-172">让 Entity Framework 自动丢弃，并基于新的模型类架构重新创建数据库。</span><span class="sxs-lookup"><span data-stu-id="3f66e-172">Have the Entity Framework automatically drop and re-create the database based on the new model class schema.</span></span> <span data-ttu-id="3f66e-173">在测试数据库上进行开发时，此方法在开发周期早期很方便；通过它可以一起快速改进模型和数据库架构。</span><span class="sxs-lookup"><span data-stu-id="3f66e-173">This approach is very convenient early in the development cycle when you are doing active development on a test database; it allows you to quickly evolve the model and database schema together.</span></span> <span data-ttu-id="3f66e-174">不过，缺点在于丢失了数据库中的现有数据，因此 *不* 希望在生产数据库上使用此方法！</span><span class="sxs-lookup"><span data-stu-id="3f66e-174">The downside, though, is that you lose existing data in the database — so you *don't* want to use this approach on a production database!</span></span> <span data-ttu-id="3f66e-175">使用初始值设定项，以使用测试数据自动设定数据库种子，这通常是开发应用程序的有效方式。</span><span class="sxs-lookup"><span data-stu-id="3f66e-175">Using an initializer to automatically seed a database with test data is often a productive way to develop an application.</span></span> <span data-ttu-id="3f66e-176">有关实体框架数据库初始值设定项的详细信息，请参阅 [ASP.NET MVC/实体框架教程](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。</span><span class="sxs-lookup"><span data-stu-id="3f66e-176">For more information on Entity Framework database initializers, see [ASP.NET MVC/Entity Framework tutorial](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>
2. <span data-ttu-id="3f66e-177">对现有数据库架构进行显式修改，使它与模型类相匹配。</span><span class="sxs-lookup"><span data-stu-id="3f66e-177">Explicitly modify the schema of the existing database so that it matches the model classes.</span></span> <span data-ttu-id="3f66e-178">此方法的优点是可以保留数据。</span><span class="sxs-lookup"><span data-stu-id="3f66e-178">The advantage of this approach is that you keep your data.</span></span> <span data-ttu-id="3f66e-179">可以手动或通过创建数据库更改脚本进行此更改。</span><span class="sxs-lookup"><span data-stu-id="3f66e-179">You can make this change either manually or by creating a database change script.</span></span>
3. <span data-ttu-id="3f66e-180">使用 Code First 迁移更新数据库架构。</span><span class="sxs-lookup"><span data-stu-id="3f66e-180">Use Code First Migrations to update the database schema.</span></span>

<span data-ttu-id="3f66e-181">本教程使用 Code First 迁移。</span><span class="sxs-lookup"><span data-stu-id="3f66e-181">For this tutorial, we'll use Code First Migrations.</span></span>

<span data-ttu-id="3f66e-182">更新种子方法，使其为新列提供一个值。</span><span class="sxs-lookup"><span data-stu-id="3f66e-182">Update the Seed method so that it provides a value for the new column.</span></span> <span data-ttu-id="3f66e-183">打开 Migrations\Configuration.cs 文件，并向每个电影对象添加分级字段。</span><span class="sxs-lookup"><span data-stu-id="3f66e-183">Open Migrations\Configuration.cs file and add a Rating field to each Movie object.</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample10.cs?highlight=6)]

<span data-ttu-id="3f66e-184">生成解决方案，然后打开 " **包管理器控制台** " 窗口，并输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="3f66e-184">Build the solution, and then open the **Package Manager Console** window and enter the following command:</span></span>

`add-migration Rating`

<span data-ttu-id="3f66e-185">`add-migration`命令告诉迁移框架检查当前的电影模型和当前的 MOVIE DB 架构，并创建将数据库迁移到新模型所需的代码。</span><span class="sxs-lookup"><span data-stu-id="3f66e-185">The `add-migration` command tells the migration framework to examine the current movie model with the current movie DB schema and create the necessary code to migrate the DB to the new model.</span></span> <span data-ttu-id="3f66e-186">名称 *级别* 是任意的，用于对迁移文件进行命名。</span><span class="sxs-lookup"><span data-stu-id="3f66e-186">The name *Rating* is arbitrary and is used to name the migration file.</span></span> <span data-ttu-id="3f66e-187">为迁移步骤使用有意义的名称会很有帮助。</span><span class="sxs-lookup"><span data-stu-id="3f66e-187">It's helpful to use a meaningful name for the migration step.</span></span>

<span data-ttu-id="3f66e-188">此命令完成后，Visual Studio 将打开定义新的派生类的类文件 `DbMigration` ，并在 `Up` 方法中可以看到创建新列的代码。</span><span class="sxs-lookup"><span data-stu-id="3f66e-188">When this command finishes, Visual Studio opens the class file that defines the new `DbMigration` derived class, and in the `Up` method you can see the code that creates the new column.</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample11.cs)]

<span data-ttu-id="3f66e-189">生成解决方案，然后 `update-database` 在 " **包管理器控制台** " 窗口中输入命令。</span><span class="sxs-lookup"><span data-stu-id="3f66e-189">Build the solution, and then enter the `update-database` command in the **Package Manager Console** window.</span></span>

<span data-ttu-id="3f66e-190">下图显示了 " **包管理器控制台** " 窗口中的输出 (日期戳预先计算的 *等级* 将不同。 ) </span><span class="sxs-lookup"><span data-stu-id="3f66e-190">The following image shows the output in the **Package Manager Console** window (The date stamp prepending *Rating* will be different.)</span></span>

![](adding-a-new-field/_static/image11.png)

<span data-ttu-id="3f66e-191">重新运行应用程序并导航到/Movies URL。</span><span class="sxs-lookup"><span data-stu-id="3f66e-191">Re-run the application and navigate to the /Movies URL.</span></span> <span data-ttu-id="3f66e-192">您可以看到新的 "分级" 字段。</span><span class="sxs-lookup"><span data-stu-id="3f66e-192">You can see the new Rating field.</span></span>

![](adding-a-new-field/_static/image12.png)

<span data-ttu-id="3f66e-193">单击 " **新建** " 链接以添加新电影。</span><span class="sxs-lookup"><span data-stu-id="3f66e-193">Click the **Create New** link to add a new movie.</span></span> <span data-ttu-id="3f66e-194">请注意，可以添加级别。</span><span class="sxs-lookup"><span data-stu-id="3f66e-194">Note that you can add a rating.</span></span>

![7_CreateRioII](adding-a-new-field/_static/image13.png)

<span data-ttu-id="3f66e-196">单击“创建”。 </span><span class="sxs-lookup"><span data-stu-id="3f66e-196">Click **Create**.</span></span> <span data-ttu-id="3f66e-197">现在电影列表中显示了新电影，其中包括评分：</span><span class="sxs-lookup"><span data-stu-id="3f66e-197">The new movie, including the rating, now shows up in the movies listing:</span></span>

![7_ourNewMovie_SM](adding-a-new-field/_static/image14.png)

<span data-ttu-id="3f66e-199">现在，项目正在使用迁移，因此在添加新字段或更新架构时，无需删除数据库。</span><span class="sxs-lookup"><span data-stu-id="3f66e-199">Now that the project is using migrations, you won't need to drop the database when you add a new field or otherwise update the schema.</span></span> <span data-ttu-id="3f66e-200">在下一部分中，我们将进行更多架构更改，并使用迁移来更新数据库。</span><span class="sxs-lookup"><span data-stu-id="3f66e-200">In the next section, we'll make more schema changes and use migrations to update the database.</span></span>

<span data-ttu-id="3f66e-201">还应将字段添加 `Rating` 到 "编辑"、"详细信息" 和 "删除" 视图模板。</span><span class="sxs-lookup"><span data-stu-id="3f66e-201">You should also add the `Rating` field to the Edit, Details, and Delete view templates.</span></span>

<span data-ttu-id="3f66e-202">您可以在 " **包管理器控制台** " 窗口中再次输入 "更新数据库" 命令，而不会运行任何迁移代码，因为该架构与该模型匹配。</span><span class="sxs-lookup"><span data-stu-id="3f66e-202">You could enter the "update-database" command in the **Package Manager Console** window again and no migration code would run, because the schema matches the model.</span></span> <span data-ttu-id="3f66e-203">但是，运行 "更新数据库" 将再次运行该 `Seed` 方法，如果更改了任何种子数据，则所做的更改将会丢失，因为 `Seed` 方法 upsert 数据。</span><span class="sxs-lookup"><span data-stu-id="3f66e-203">However, running "update-database" will run the `Seed` method again, and if you changed any of the Seed data, the changes will be lost because the `Seed` method upserts data.</span></span> <span data-ttu-id="3f66e-204">有关此方法的详细信息，请参阅 `Seed` Tom Dykstra 的热门 [ASP.NET MVC/实体框架教程](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。</span><span class="sxs-lookup"><span data-stu-id="3f66e-204">You can read more about the `Seed` method in Tom Dykstra's popular [ASP.NET MVC/Entity Framework tutorial](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>

<span data-ttu-id="3f66e-205">在本部分中，您将了解如何修改模型对象并使数据库与更改保持同步。</span><span class="sxs-lookup"><span data-stu-id="3f66e-205">In this section you saw how you can modify model objects and keep the database in sync with the changes.</span></span> <span data-ttu-id="3f66e-206">还了解了使用示例数据填充新创建的数据库的方法，以便可以试用方案。</span><span class="sxs-lookup"><span data-stu-id="3f66e-206">You also learned a way to populate a newly created database with sample data so you can try out scenarios.</span></span> <span data-ttu-id="3f66e-207">这只是 Code First 的简要介绍，请参阅为 [ASP.NET MVC 应用程序创建实体框架数据模型](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) ，以获取有关主题的更完整教程。</span><span class="sxs-lookup"><span data-stu-id="3f66e-207">This was just a quick introduction to Code First, see [Creating an Entity Framework Data Model for an ASP.NET MVC Application](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) for a more complete tutorial on the subject.</span></span> <span data-ttu-id="3f66e-208">接下来，让我们看看如何将更丰富的验证逻辑添加到模型类，并实现一些业务规则。</span><span class="sxs-lookup"><span data-stu-id="3f66e-208">Next, let's look at how you can add richer validation logic to the model classes and enable some business rules to be enforced.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="3f66e-209">[上一页](adding-search.md)
> [下一页](adding-validation.md)</span><span class="sxs-lookup"><span data-stu-id="3f66e-209">[Previous](adding-search.md)
[Next](adding-validation.md)</span></span>

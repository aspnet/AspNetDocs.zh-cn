---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-new-field
title: 将新字段添加到电影模型和表 (C#) |Microsoft Docs
author: Rick-Anderson
description: 本教程将讲述构建使用 Microsoft Visual Web Developer 2010 Express Service Pack 1，这是一个 ASP.NET MVC Web 应用程序的基础知识...
ms.author: riande
ms.date: 01/12/2011
ms.assetid: b4e76c1a-f66e-43a0-aa72-f39df79c07c1
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-new-field
msc.type: authoredcontent
ms.openlocfilehash: a06def9c434bd79d63bb74d105c1788e993e231a
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/09/2019
ms.locfileid: "59383852"
---
# <a name="adding-a-new-field-to-the-movie-model-and-table-c"></a><span data-ttu-id="c5ab5-103">向电影模型和表添加新字段 (C#)</span><span class="sxs-lookup"><span data-stu-id="c5ab5-103">Adding a New Field to the Movie Model and Table (C#)</span></span>

<span data-ttu-id="c5ab5-104">通过[Rick Anderson]((https://twitter.com/RickAndMSFT))</span><span class="sxs-lookup"><span data-stu-id="c5ab5-104">by [Rick Anderson]((https://twitter.com/RickAndMSFT))</span></span>

> > [!NOTE]
> > <span data-ttu-id="c5ab5-105">本教程中的更新的版本是可用[此处](../../../getting-started/introduction/getting-started.md)，它使用 ASP.NET MVC 5 和 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="c5ab5-105">An updated version of this tutorial is available [here](../../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="c5ab5-106">它是更安全、 更易于遵循，并演示更多的功能。</span><span class="sxs-lookup"><span data-stu-id="c5ab5-106">It's more secure, much simpler to follow and demonstrates more features.</span></span>
> 
> 
> <span data-ttu-id="c5ab5-107">本教程将讲述构建使用 Microsoft Visual Web Developer 2010 Express Service Pack 1，这是免费版本的 Microsoft Visual Studio 的 ASP.NET MVC Web 应用程序的基础知识。</span><span class="sxs-lookup"><span data-stu-id="c5ab5-107">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="c5ab5-108">在开始之前，请确保已安装以下列出的先决条件。</span><span class="sxs-lookup"><span data-stu-id="c5ab5-108">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="c5ab5-109">可以通过单击以下链接安装所有这些：[Web 平台安装程序](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="c5ab5-109">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="c5ab5-110">或者，可以单独安装系统必备组件，使用以下链接：</span><span class="sxs-lookup"><span data-stu-id="c5ab5-110">Alternatively, you can individually install the prerequisites using the following links:</span></span>
> 
> - [<span data-ttu-id="c5ab5-111">Visual Studio Web Developer Express SP1 必备组件</span><span class="sxs-lookup"><span data-stu-id="c5ab5-111">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="c5ab5-112">ASP.NET MVC 3 工具更新</span><span class="sxs-lookup"><span data-stu-id="c5ab5-112">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - <span data-ttu-id="c5ab5-113">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（运行时和工具支持）</span><span class="sxs-lookup"><span data-stu-id="c5ab5-113">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>
> 
> <span data-ttu-id="c5ab5-114">如果您使用 Visual Studio 2010 而不 Visual Web Developer 2010，请通过单击以下链接安装必备组件：[Visual Studio 2010 必备组件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="c5ab5-114">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>
> 
> <span data-ttu-id="c5ab5-115">可随附于此项目具有 C# 源代码的 Visual Web Developer 项目。</span><span class="sxs-lookup"><span data-stu-id="c5ab5-115">A Visual Web Developer project with C# source code is available to accompany this topic.</span></span> <span data-ttu-id="c5ab5-116">[下载 C# 版本](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)。</span><span class="sxs-lookup"><span data-stu-id="c5ab5-116">[Download the C# version](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span> <span data-ttu-id="c5ab5-117">如果您喜欢 Visual Basic，切换到[Visual Basic 版本](../vb/intro-to-aspnet-mvc-3.md)本教程。</span><span class="sxs-lookup"><span data-stu-id="c5ab5-117">If you prefer Visual Basic, switch to the [Visual Basic version](../vb/intro-to-aspnet-mvc-3.md) of this tutorial.</span></span>


<span data-ttu-id="c5ab5-118">在本部分将对模型类进行一些更改，并了解如何更新数据库架构以匹配的模型更改。</span><span class="sxs-lookup"><span data-stu-id="c5ab5-118">In this section you'll make some changes to the model classes and learn how you can update the database schema to match the model changes.</span></span>

## <a name="adding-a-rating-property-to-the-movie-model"></a><span data-ttu-id="c5ab5-119">向电影模型添加分级属性</span><span class="sxs-lookup"><span data-stu-id="c5ab5-119">Adding a Rating Property to the Movie Model</span></span>

<span data-ttu-id="c5ab5-120">首先，通过添加一个新`Rating`属性设置为现有`Movie`类。</span><span class="sxs-lookup"><span data-stu-id="c5ab5-120">Start by adding a new `Rating` property to the existing `Movie` class.</span></span> <span data-ttu-id="c5ab5-121">打开*Movie.cs*文件，并添加`Rating`如下属性：</span><span class="sxs-lookup"><span data-stu-id="c5ab5-121">Open the *Movie.cs* file and add the `Rating` property like this one:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample1.cs)]

<span data-ttu-id="c5ab5-122">完整`Movie`类现在看起来如以下代码：</span><span class="sxs-lookup"><span data-stu-id="c5ab5-122">The complete `Movie` class now looks like the following code:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample2.cs)]

<span data-ttu-id="c5ab5-123">重新编译应用程序中使用**调试** &gt;**构建电影**菜单命令。</span><span class="sxs-lookup"><span data-stu-id="c5ab5-123">Recompile the application using the **Debug** &gt;**Build Movie** menu command.</span></span>

<span data-ttu-id="c5ab5-124">现在，已更新`Model`类，您还需要更新 *\Views\Movies\Index.cshtml* 并 *\Views\Movies\Create.cshtml* 查看模板以支持新`Rating`属性。</span><span class="sxs-lookup"><span data-stu-id="c5ab5-124">Now that you've updated the `Model` class, you also need to update the *\Views\Movies\Index.cshtml* and *\Views\Movies\Create.cshtml* view templates in order to support the new `Rating` property.</span></span>

<span data-ttu-id="c5ab5-125">打开 *\Views\Movies\Index.cshtml* 文件，并添加`<th>Rating</th>`列标题之后**价格**列。</span><span class="sxs-lookup"><span data-stu-id="c5ab5-125">Open the *\Views\Movies\Index.cshtml* file and add a `<th>Rating</th>` column heading just after the **Price** column.</span></span> <span data-ttu-id="c5ab5-126">然后添加`<td>`快要结束的模板来呈现列`@item.Rating`值。</span><span class="sxs-lookup"><span data-stu-id="c5ab5-126">Then add a `<td>` column near the end of the template to render the `@item.Rating` value.</span></span> <span data-ttu-id="c5ab5-127">下面是哪些更新 *Index.cshtml* 视图模板如下所示：</span><span class="sxs-lookup"><span data-stu-id="c5ab5-127">Below is what the updated *Index.cshtml* view template looks like:</span></span>

[!code-cshtml[Main](adding-a-new-field/samples/sample3.cshtml)]

<span data-ttu-id="c5ab5-128">接下来，打开 *\Views\Movies\Create.cshtml* 文件，并添加以下标记窗体的结尾附近。</span><span class="sxs-lookup"><span data-stu-id="c5ab5-128">Next, open the *\Views\Movies\Create.cshtml* file and add the following markup near the end of the form.</span></span> <span data-ttu-id="c5ab5-129">这会使文本框中，以便创建新电影时，可以指定一个级别。</span><span class="sxs-lookup"><span data-stu-id="c5ab5-129">This renders a text box so that you can specify a rating when a new movie is created.</span></span>

[!code-cshtml[Main](adding-a-new-field/samples/sample4.cshtml)]

## <a name="managing-model-and-database-schema-differences"></a><span data-ttu-id="c5ab5-130">管理模型和数据库架构差异</span><span class="sxs-lookup"><span data-stu-id="c5ab5-130">Managing Model and Database Schema Differences</span></span>

<span data-ttu-id="c5ab5-131">现已更新以支持新的应用程序代码`Rating`属性。</span><span class="sxs-lookup"><span data-stu-id="c5ab5-131">You've now updated the application code to support the new `Rating` property.</span></span>

<span data-ttu-id="c5ab5-132">现在，运行该应用程序并导航到 */Movies* URL。</span><span class="sxs-lookup"><span data-stu-id="c5ab5-132">Now run the application and navigate to the */Movies* URL.</span></span> <span data-ttu-id="c5ab5-133">执行此操作，不过，将看到以下错误：</span><span class="sxs-lookup"><span data-stu-id="c5ab5-133">When you do this, though, you'll see the following error:</span></span>

![](adding-a-new-field/_static/image1.png)

<span data-ttu-id="c5ab5-134">之所以看到此错误，因为已更新`Movie`应用程序中的 model 类现在与不同的架构`Movie`现有数据库表。</span><span class="sxs-lookup"><span data-stu-id="c5ab5-134">You're seeing this error because the updated `Movie` model class in the application is now different than the schema of the `Movie` table of the existing database.</span></span> <span data-ttu-id="c5ab5-135">（数据库表中没有 `Rating` 列。）</span><span class="sxs-lookup"><span data-stu-id="c5ab5-135">(There's no `Rating` column in the database table.)</span></span>

<span data-ttu-id="c5ab5-136">默认情况下，当您使用 Entity Framework Code First 自动创建数据库，就像前面在本教程中，代码优先将表添加到数据库来帮助跟踪数据库的架构是否与从其中生成它的模型类同步。</span><span class="sxs-lookup"><span data-stu-id="c5ab5-136">By default, when you use Entity Framework Code First to automatically create a database, as you did earlier in this tutorial, Code First adds a table to the database to help track whether the schema of the database is in sync with the model classes it was generated from.</span></span> <span data-ttu-id="c5ab5-137">如果它们不同步，实体框架将引发错误。</span><span class="sxs-lookup"><span data-stu-id="c5ab5-137">If they aren't in sync, the Entity Framework throws an error.</span></span> <span data-ttu-id="c5ab5-138">这使得更轻松地在开发时，你可能会否则仅发现 （通过奇怪的错误） 在运行时跟踪问题。</span><span class="sxs-lookup"><span data-stu-id="c5ab5-138">This makes it easier to track down issues at development time that you might otherwise only find (by obscure errors) at run time.</span></span> <span data-ttu-id="c5ab5-139">同步检查功能是哪些因素会导致要显示的错误消息，你刚才看到的。</span><span class="sxs-lookup"><span data-stu-id="c5ab5-139">The sync-checking feature is what causes the error message to be displayed that you just saw.</span></span>

<span data-ttu-id="c5ab5-140">有两种方法解决此错误：</span><span class="sxs-lookup"><span data-stu-id="c5ab5-140">There are two approaches to resolving the error:</span></span>

1. <span data-ttu-id="c5ab5-141">让 Entity Framework 自动丢弃，并基于新的模型类架构重新创建数据库。</span><span class="sxs-lookup"><span data-stu-id="c5ab5-141">Have the Entity Framework automatically drop and re-create the database based on the new model class schema.</span></span> <span data-ttu-id="c5ab5-142">这种方法是非常方便时执行活动开发上测试数据库，因为它允许您一起快速改进模型和数据库架构。</span><span class="sxs-lookup"><span data-stu-id="c5ab5-142">This approach is very convenient when doing active development on a test database, because it allows you to quickly evolve the model and database schema together.</span></span> <span data-ttu-id="c5ab5-143">缺点，不过，是会丢失数据库中的现有数据，因此您 *不* 需要生产数据库上使用此方法 ！</span><span class="sxs-lookup"><span data-stu-id="c5ab5-143">The downside, though, is that you lose existing data in the database — so you *don't* want to use this approach on a production database!</span></span>
2. <span data-ttu-id="c5ab5-144">对现有数据库架构进行显式修改，使它与模型类相匹配。</span><span class="sxs-lookup"><span data-stu-id="c5ab5-144">Explicitly modify the schema of the existing database so that it matches the model classes.</span></span> <span data-ttu-id="c5ab5-145">此方法的优点是可以保留数据。</span><span class="sxs-lookup"><span data-stu-id="c5ab5-145">The advantage of this approach is that you keep your data.</span></span> <span data-ttu-id="c5ab5-146">可以手动或通过创建数据库更改脚本进行此更改。</span><span class="sxs-lookup"><span data-stu-id="c5ab5-146">You can make this change either manually or by creating a database change script.</span></span>

<span data-ttu-id="c5ab5-147">对于本教程中，我们将使用第一种方法，您必须 Entity Framework Code First 每当模型发生更改自动重新创建该数据库。</span><span class="sxs-lookup"><span data-stu-id="c5ab5-147">For this tutorial, we'll use the first approach — you'll have the Entity Framework Code First automatically re-create the database anytime the model changes.</span></span>

## <a name="automatically-re-creating-the-database-on-model-changes"></a><span data-ttu-id="c5ab5-148">自动重新创建模型的更改上的数据库</span><span class="sxs-lookup"><span data-stu-id="c5ab5-148">Automatically Re-Creating the Database on Model Changes</span></span>

<span data-ttu-id="c5ab5-149">让我们更新该应用程序，以便 Code First 自动删除并重新创建数据库，只要您更改应用程序的模型。</span><span class="sxs-lookup"><span data-stu-id="c5ab5-149">Let's update the application so that Code First automatically drops and re-creates the database anytime you change the model for the application.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="c5ab5-150">**警告**应该启用的自动删除并重新创建数据库，仅当你正在使用开发或测试数据库，这种方法和 *永远不会* 包含实际数据的生产数据库上。</span><span class="sxs-lookup"><span data-stu-id="c5ab5-150">**Warning** You should enable this approach of automatically dropping and re-creating the database only when you're using a development or test database, and *never* on a production database that contains real data.</span></span> <span data-ttu-id="c5ab5-151">使用生产服务器上可能会导致数据丢失。</span><span class="sxs-lookup"><span data-stu-id="c5ab5-151">Using it on a production server can lead to data loss.</span></span>


<span data-ttu-id="c5ab5-152">在中**解决方案资源管理器**，右键单击 *模型* 文件夹，选择**添加**，然后选择**类**。</span><span class="sxs-lookup"><span data-stu-id="c5ab5-152">In **Solution Explorer**, right click the *Models* folder, select **Add**, and then select **Class**.</span></span>

![](adding-a-new-field/_static/image2.png)

<span data-ttu-id="c5ab5-153">命名类"MovieInitializer"。</span><span class="sxs-lookup"><span data-stu-id="c5ab5-153">Name the class "MovieInitializer".</span></span> <span data-ttu-id="c5ab5-154">更新`MovieInitializer`类，以包含以下代码：</span><span class="sxs-lookup"><span data-stu-id="c5ab5-154">Update the `MovieInitializer` class to contain the following code:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample5.cs)]

<span data-ttu-id="c5ab5-155">`MovieInitializer`类指定应删除并自动重新创建如果发生变化的模型类使用该模型的数据库。</span><span class="sxs-lookup"><span data-stu-id="c5ab5-155">The `MovieInitializer` class specifies that the database used by the model should be dropped and automatically re-created if the model classes ever change.</span></span> <span data-ttu-id="c5ab5-156">该代码包括`Seed`方法，以便指定一些默认数据会自动向数据库添加任何时间它具有创建 （或重新创建）。</span><span class="sxs-lookup"><span data-stu-id="c5ab5-156">The code includes a `Seed` method to specify some default data to automatically add to the database any time it's created (or re-created).</span></span> <span data-ttu-id="c5ab5-157">这提供了有用的方式来使用填充数据库一些示例数据，而无需手动填充它每次进行更改的模型。</span><span class="sxs-lookup"><span data-stu-id="c5ab5-157">This provides a useful way to populate the database with some sample data, without requiring you to manually populate it each time you make a model change.</span></span>

<span data-ttu-id="c5ab5-158">现在，已定义`MovieInitializer`类，您需要其绑定，以便每次应用程序运行时，它检查是否不同于数据库中架构的模型类。</span><span class="sxs-lookup"><span data-stu-id="c5ab5-158">Now that you've defined the `MovieInitializer` class, you'll want to wire it up so that each time the application runs, it checks whether the model classes are different from the schema in the database.</span></span> <span data-ttu-id="c5ab5-159">如果是，您可以运行初始值设定项来重新创建数据库以匹配该模型，然后使用示例数据在数据库中填充。</span><span class="sxs-lookup"><span data-stu-id="c5ab5-159">If they are, you can run the initializer to re-create the database to match the model and then populate the database with the sample data.</span></span>

<span data-ttu-id="c5ab5-160">打开 *Global.asax* 文件的根目录处`MvcMovies`项目：</span><span class="sxs-lookup"><span data-stu-id="c5ab5-160">Open the *Global.asax* file that's at the root of the `MvcMovies` project:</span></span>

[![](adding-a-new-field/_static/image4.png)](adding-a-new-field/_static/image3.png)

<span data-ttu-id="c5ab5-161">*Global.asax* 文件包含的类定义整个应用程序项目，并包含`Application_Start`运行该应用程序首次启动时的事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="c5ab5-161">The *Global.asax* file contains the class that defines the entire application for the project, and contains an `Application_Start` event handler that runs when the application first starts.</span></span>

<span data-ttu-id="c5ab5-162">让我们来添加两个 using 语句的文件的顶部。</span><span class="sxs-lookup"><span data-stu-id="c5ab5-162">Let's add two using statements to the top of the file.</span></span> <span data-ttu-id="c5ab5-163">第一个引用实体框架命名空间，而第二个引用命名空间，我们`MovieInitializer`类生活：</span><span class="sxs-lookup"><span data-stu-id="c5ab5-163">The first references the Entity Framework namespace, and the second references the namespace where our `MovieInitializer` class lives:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample6.cs)]

<span data-ttu-id="c5ab5-164">然后找到`Application_Start`方法，并添加到调用`Database.SetInitializer`开头的方法，如下所示：</span><span class="sxs-lookup"><span data-stu-id="c5ab5-164">Then find the `Application_Start` method and add a call to `Database.SetInitializer` at the beginning of the method, as shown below:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample7.cs)]

<span data-ttu-id="c5ab5-165">`Database.SetInitializer`刚添加的语句指示的数据库由`MovieDBContext`应自动删除并重新创建如果不匹配的架构和数据库实例。</span><span class="sxs-lookup"><span data-stu-id="c5ab5-165">The `Database.SetInitializer` statement you just added indicates that the database used by the `MovieDBContext` instance should be automatically deleted and re-created if the schema and the database don't match.</span></span> <span data-ttu-id="c5ab5-166">如您所看到的它还会填充使用示例数据中指定的数据库和`MovieInitializer`类。</span><span class="sxs-lookup"><span data-stu-id="c5ab5-166">And as you saw, it will also populate the database with the sample data that's specified in the `MovieInitializer` class.</span></span>

<span data-ttu-id="c5ab5-167">关闭 *Global.asax* 文件。</span><span class="sxs-lookup"><span data-stu-id="c5ab5-167">Close the *Global.asax* file.</span></span>

<span data-ttu-id="c5ab5-168">重新运行该应用程序并导航到 */Movies* URL。</span><span class="sxs-lookup"><span data-stu-id="c5ab5-168">Re-run the application and navigate to the */Movies* URL.</span></span> <span data-ttu-id="c5ab5-169">应用程序启动时，它会检测模型结构不能再与数据库架构相匹配。</span><span class="sxs-lookup"><span data-stu-id="c5ab5-169">When the application starts, it detects that the model structure no longer matches the database schema.</span></span> <span data-ttu-id="c5ab5-170">自动重新创建数据库，以匹配新的模型结构，并填充该数据库示例电影：</span><span class="sxs-lookup"><span data-stu-id="c5ab5-170">It automatically re-creates the database to match the new model structure and populates the database with the sample movies:</span></span>

![7_MyMovieList_SM](adding-a-new-field/_static/image5.png)

<span data-ttu-id="c5ab5-172">单击**创建新**链接以添加新电影。</span><span class="sxs-lookup"><span data-stu-id="c5ab5-172">Click the **Create New** link to add a new movie.</span></span> <span data-ttu-id="c5ab5-173">请注意，您可以添加一个级别。</span><span class="sxs-lookup"><span data-stu-id="c5ab5-173">Note that you can add a rating.</span></span>

[![7<span data-ttu-id="c5ab5-174">_CreateRioII]</span><span class="sxs-lookup"><span data-stu-id="c5ab5-174">_CreateRioII]</span></span>(adding-a-new-field/_static/image7.png)](adding-a-new-field/_static/image6.png)

<span data-ttu-id="c5ab5-175">单击 **“创建”**。</span><span class="sxs-lookup"><span data-stu-id="c5ab5-175">Click **Create**.</span></span> <span data-ttu-id="c5ab5-176">新电影，包括分级，现在显示在列表的电影：</span><span class="sxs-lookup"><span data-stu-id="c5ab5-176">The new movie, including the rating, now shows up in the movies listing:</span></span>

[![7<span data-ttu-id="c5ab5-177">_ourNewMovie_SM]</span><span class="sxs-lookup"><span data-stu-id="c5ab5-177">_ourNewMovie_SM]</span></span>(adding-a-new-field/_static/image9.png)](adding-a-new-field/_static/image8.png)

<span data-ttu-id="c5ab5-178">在本部分中您将看到如何修改模型对象并使数据库所做的更改同步。</span><span class="sxs-lookup"><span data-stu-id="c5ab5-178">In this section you saw how you can modify model objects and keep the database in sync with the changes.</span></span> <span data-ttu-id="c5ab5-179">你还了解了一种方法来填充新创建的数据库使用示例数据，这样您可以试用方案。</span><span class="sxs-lookup"><span data-stu-id="c5ab5-179">You also learned a way to populate a newly created database with sample data so you can try out scenarios.</span></span> <span data-ttu-id="c5ab5-180">接下来，让我们看看如何将更丰富的验证逻辑添加到模型类并启用某些业务规则以强制实施。</span><span class="sxs-lookup"><span data-stu-id="c5ab5-180">Next, let's look at how you can add richer validation logic to the model classes and enable some business rules to be enforced.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="c5ab5-181">[上一页](examining-the-edit-methods-and-edit-view.md)
> [下一页](adding-validation-to-the-model.md)</span><span class="sxs-lookup"><span data-stu-id="c5ab5-181">[Previous](examining-the-edit-methods-and-edit-view.md)
[Next](adding-validation-to-the-model.md)</span></span>

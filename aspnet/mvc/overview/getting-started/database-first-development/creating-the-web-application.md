---
uid: mvc/overview/getting-started/database-first-development/creating-the-web-application
title: 教程：为第一种使用 ASP.NET MVC 的 EF 数据库中创建的 Web 应用程序和数据模型
description: 本教程重点介绍创建 web 应用程序，并生成基于数据库表的数据模型。
author: Rick-Anderson
ms.author: riande
ms.date: 01/28/2019
ms.topic: tutorial
ms.assetid: bc8f2bd5-ff57-4dcd-8418-a5bd517d8953
msc.legacyurl: /mvc/overview/getting-started/database-first-development/creating-the-web-application
msc.type: authoredcontent
ms.openlocfilehash: 30fd42be5677df6fa6ee0630914098c30d21385b
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/09/2019
ms.locfileid: "59404515"
---
# <a name="tutorial-create-the-web-application-and-data-models-for-ef-database-first-with-aspnet-mvc"></a><span data-ttu-id="9c2d8-103">教程：为第一种使用 ASP.NET MVC 的 EF 数据库中创建的 Web 应用程序和数据模型</span><span class="sxs-lookup"><span data-stu-id="9c2d8-103">Tutorial: Create the Web Application and Data Models for EF Database First with ASP.NET MVC</span></span>

 <span data-ttu-id="9c2d8-104">使用 MVC、 Entity Framework 和 ASP.NET 基架，可以创建提供接口的现有数据库的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="9c2d8-104">Using MVC, Entity Framework, and ASP.NET Scaffolding, you can create a web application that provides an interface to an existing database.</span></span> <span data-ttu-id="9c2d8-105">本系列教程演示了如何自动生成代码，使用户能够显示、 编辑、 创建和删除驻留在数据库表中的数据。</span><span class="sxs-lookup"><span data-stu-id="9c2d8-105">This tutorial series shows you how to automatically generate code that enables users to display, edit, create, and delete data that resides in a database table.</span></span> <span data-ttu-id="9c2d8-106">生成的代码对应于数据库表中的列。</span><span class="sxs-lookup"><span data-stu-id="9c2d8-106">The generated code corresponds to the columns in the database table.</span></span>

<span data-ttu-id="9c2d8-107">本教程重点介绍创建 web 应用程序，并生成基于数据库表的数据模型。</span><span class="sxs-lookup"><span data-stu-id="9c2d8-107">This tutorial focuses on creating the web application, and generating the data models based on your database tables.</span></span>

<span data-ttu-id="9c2d8-108">在本教程中，你将了解：</span><span class="sxs-lookup"><span data-stu-id="9c2d8-108">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9c2d8-109">创建 ASP.NET Web 应用</span><span class="sxs-lookup"><span data-stu-id="9c2d8-109">Create an ASP.NET web app</span></span>
> * <span data-ttu-id="9c2d8-110">生成模型</span><span class="sxs-lookup"><span data-stu-id="9c2d8-110">Generate the models</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9c2d8-111">系统必备</span><span class="sxs-lookup"><span data-stu-id="9c2d8-111">Prerequisites</span></span>

* [<span data-ttu-id="9c2d8-112">使用 Entity Framework 6 Database First 通过 MVC 5 入门</span><span class="sxs-lookup"><span data-stu-id="9c2d8-112">Getting started with Entity Framework 6 Database First using MVC 5</span></span>](setting-up-database.md)

## <a name="create-an-aspnet-web-app"></a><span data-ttu-id="9c2d8-113">创建 ASP.NET Web 应用</span><span class="sxs-lookup"><span data-stu-id="9c2d8-113">Create an ASP.NET web app</span></span>

<span data-ttu-id="9c2d8-114">在新的解决方案或与数据库项目相同的解决方案中，创建 Visual Studio 中的新项目，然后选择**ASP.NET Web 应用程序**模板。</span><span class="sxs-lookup"><span data-stu-id="9c2d8-114">In either a new solution or the same solution as the database project, create a new project in Visual Studio and select the **ASP.NET Web Application** template.</span></span> <span data-ttu-id="9c2d8-115">将项目命名**ContosoSite**。</span><span class="sxs-lookup"><span data-stu-id="9c2d8-115">Name the project **ContosoSite**.</span></span>

![创建项目](creating-the-web-application/_static/image1.png)

<span data-ttu-id="9c2d8-117">单击 **“确定”**。</span><span class="sxs-lookup"><span data-stu-id="9c2d8-117">Click **OK**.</span></span>

<span data-ttu-id="9c2d8-118">在新建 ASP.NET 项目窗口中，选择**MVC**模板。</span><span class="sxs-lookup"><span data-stu-id="9c2d8-118">In the New ASP.NET Project window, select the **MVC** template.</span></span> <span data-ttu-id="9c2d8-119">您可以清除**在云中托管**现在选项，因为你将部署到云的应用程序更高版本。</span><span class="sxs-lookup"><span data-stu-id="9c2d8-119">You can clear the **Host in the cloud** option for now because you will deploy the application to the cloud later.</span></span> <span data-ttu-id="9c2d8-120">单击**确定**创建应用程序。</span><span class="sxs-lookup"><span data-stu-id="9c2d8-120">Click **OK** to create the application.</span></span>

<span data-ttu-id="9c2d8-121">使用默认文件和文件夹创建项目。</span><span class="sxs-lookup"><span data-stu-id="9c2d8-121">The project is created with the default files and folders.</span></span>

<span data-ttu-id="9c2d8-122">在本教程中，将使用 Entity Framework 6。</span><span class="sxs-lookup"><span data-stu-id="9c2d8-122">In this tutorial, you will use Entity Framework 6.</span></span> <span data-ttu-id="9c2d8-123">可以通过管理 NuGet 包窗口在项目中，请仔细检查 Entity Framework 的版本。</span><span class="sxs-lookup"><span data-stu-id="9c2d8-123">You can double-check the version of Entity Framework in your project through the Manage NuGet Packages window.</span></span> <span data-ttu-id="9c2d8-124">如果有必要，请更新你的实体框架版本。</span><span class="sxs-lookup"><span data-stu-id="9c2d8-124">If necessary, update your version of Entity Framework.</span></span>

![显示版本](creating-the-web-application/_static/image3.png)

## <a name="generate-the-models"></a><span data-ttu-id="9c2d8-126">生成模型</span><span class="sxs-lookup"><span data-stu-id="9c2d8-126">Generate the models</span></span>

<span data-ttu-id="9c2d8-127">现在将从数据库表创建实体框架模型。</span><span class="sxs-lookup"><span data-stu-id="9c2d8-127">You will now create Entity Framework models from the database tables.</span></span> <span data-ttu-id="9c2d8-128">这些模型是将用于处理的数据的类。</span><span class="sxs-lookup"><span data-stu-id="9c2d8-128">These models are classes that you will use to work with the data.</span></span> <span data-ttu-id="9c2d8-129">每个模型反映数据库中的表，并包含对应于表中的列的属性。</span><span class="sxs-lookup"><span data-stu-id="9c2d8-129">Each model mirrors a table in the database and contains properties that correspond to the columns in the table.</span></span>

<span data-ttu-id="9c2d8-130">右键单击**模型**文件夹，然后选择**添加**并**新项**。</span><span class="sxs-lookup"><span data-stu-id="9c2d8-130">Right-click the **Models** folder, and select **Add** and **New Item**.</span></span>

<span data-ttu-id="9c2d8-131">在添加新项窗口中，选择**数据**的左窗格中并**ADO.NET 实体数据模型**从中间窗格中的选项。</span><span class="sxs-lookup"><span data-stu-id="9c2d8-131">In the Add New Item window, select **Data** in the left pane and **ADO.NET Entity Data Model** from the options in the center pane.</span></span> <span data-ttu-id="9c2d8-132">将新的模型文件**ContosoModel**。</span><span class="sxs-lookup"><span data-stu-id="9c2d8-132">Name the new model file **ContosoModel**.</span></span>

<span data-ttu-id="9c2d8-133">单击 **添加**。</span><span class="sxs-lookup"><span data-stu-id="9c2d8-133">Click **Add**.</span></span>

<span data-ttu-id="9c2d8-134">在实体数据模型向导中，选择**EF 设计器从数据库**。</span><span class="sxs-lookup"><span data-stu-id="9c2d8-134">In the Entity Data Model Wizard, select **EF Designer from database**.</span></span>

<span data-ttu-id="9c2d8-135">单击 **“下一步”**。</span><span class="sxs-lookup"><span data-stu-id="9c2d8-135">Click **Next**.</span></span>

<span data-ttu-id="9c2d8-136">如果必须在开发环境中定义的数据库连接，可能会看到其中一个预先选择这些连接。</span><span class="sxs-lookup"><span data-stu-id="9c2d8-136">If you have database connections defined within your development environment, you may see one of these connections pre-selected.</span></span> <span data-ttu-id="9c2d8-137">但是，你想要创建新的连接到在本教程的第一部分创建的数据库。</span><span class="sxs-lookup"><span data-stu-id="9c2d8-137">However, you want to create a new connection to the database you created in the first part of this tutorial.</span></span> <span data-ttu-id="9c2d8-138">单击**新的连接**按钮。</span><span class="sxs-lookup"><span data-stu-id="9c2d8-138">Click the **New Connection** button.</span></span>

<span data-ttu-id="9c2d8-139">在连接属性窗口中，提供了创建数据库时所在的本地服务器的名称 (在这种情况下 **(localdb) \ProjectsV13**)。</span><span class="sxs-lookup"><span data-stu-id="9c2d8-139">In the Connection Properties window, provide the name of the local server where your database was created (in this case **(localdb)\ProjectsV13**).</span></span> <span data-ttu-id="9c2d8-140">提供服务器名称后, 从可用数据库中选择 ContosoUniversityData。</span><span class="sxs-lookup"><span data-stu-id="9c2d8-140">After providing the server name, select the ContosoUniversityData from the available databases.</span></span>

![设置连接属性](creating-the-web-application/_static/image8.png)

<span data-ttu-id="9c2d8-142">单击 **“确定”**。</span><span class="sxs-lookup"><span data-stu-id="9c2d8-142">Click **OK**.</span></span>

<span data-ttu-id="9c2d8-143">此时将显示正确的连接属性。</span><span class="sxs-lookup"><span data-stu-id="9c2d8-143">The correct connection properties are now displayed.</span></span> <span data-ttu-id="9c2d8-144">可以在 Web.Config 文件中使用连接的默认名称。</span><span class="sxs-lookup"><span data-stu-id="9c2d8-144">You can use the default name for connection in the Web.Config file.</span></span>

<span data-ttu-id="9c2d8-145">单击 **“下一步”**。</span><span class="sxs-lookup"><span data-stu-id="9c2d8-145">Click **Next**.</span></span>

<span data-ttu-id="9c2d8-146">选择实体框架的最新版本。</span><span class="sxs-lookup"><span data-stu-id="9c2d8-146">Select the latest version of Entity Framework.</span></span>

<span data-ttu-id="9c2d8-147">单击 **“下一步”**。</span><span class="sxs-lookup"><span data-stu-id="9c2d8-147">Click **Next**.</span></span>

<span data-ttu-id="9c2d8-148">选择**表**来生成模型的所有三个表。</span><span class="sxs-lookup"><span data-stu-id="9c2d8-148">Select **Tables** to generate models for all three tables.</span></span>

<span data-ttu-id="9c2d8-149">单击 **“完成”**。</span><span class="sxs-lookup"><span data-stu-id="9c2d8-149">Click **Finish**.</span></span>

<span data-ttu-id="9c2d8-150">如果你收到一条安全警告，选择**确定**继续运行模板。</span><span class="sxs-lookup"><span data-stu-id="9c2d8-150">If you receive a security warning, select **OK** to continue running the template.</span></span>

<span data-ttu-id="9c2d8-151">从数据库表生成模型和关系图显示，其中显示的属性和表之间的关系。</span><span class="sxs-lookup"><span data-stu-id="9c2d8-151">The models are generated from the database tables, and a diagram is displayed that shows the properties and relationships between the tables.</span></span>

![模型的关系图](creating-the-web-application/_static/image11.png)

<span data-ttu-id="9c2d8-153">模型文件夹现在包括许多与从数据库生成的模型相关的新文件。</span><span class="sxs-lookup"><span data-stu-id="9c2d8-153">The Models folder now includes many new files related to the models that were generated from the database.</span></span>

<span data-ttu-id="9c2d8-154">**ContosoModel.Context.cs**文件包含的类的派生自**DbContext**类，并提供了用于每个对应于数据库表的 model 类属性。</span><span class="sxs-lookup"><span data-stu-id="9c2d8-154">The **ContosoModel.Context.cs** file contains a class that derives from the **DbContext** class, and provides a property for each model class that corresponds to a database table.</span></span> <span data-ttu-id="9c2d8-155">**Course.cs**， **Enrollment.cs**，并**Student.cs**文件包含表示数据库表的模型类。</span><span class="sxs-lookup"><span data-stu-id="9c2d8-155">The **Course.cs**, **Enrollment.cs**, and **Student.cs** files contain the model classes that represent the databases tables.</span></span> <span data-ttu-id="9c2d8-156">使用基架时，将使用上下文类和模型类。</span><span class="sxs-lookup"><span data-stu-id="9c2d8-156">You will use both the context class and the model classes when working with scaffolding.</span></span>

<span data-ttu-id="9c2d8-157">本教程前，生成项目。</span><span class="sxs-lookup"><span data-stu-id="9c2d8-157">Before proceeding with this tutorial, build the project.</span></span> <span data-ttu-id="9c2d8-158">在下一步部分中，将生成基于数据模型代码，但如果未生成项目，将无法工作部分。</span><span class="sxs-lookup"><span data-stu-id="9c2d8-158">In the next section, you will generate code based on the data models, but that section will not work if the project has not been built.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9c2d8-159">后续步骤</span><span class="sxs-lookup"><span data-stu-id="9c2d8-159">Next steps</span></span>

<span data-ttu-id="9c2d8-160">在本教程中，你将了解：</span><span class="sxs-lookup"><span data-stu-id="9c2d8-160">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9c2d8-161">创建 ASP.NET web 应用</span><span class="sxs-lookup"><span data-stu-id="9c2d8-161">Created an ASP.NET web app</span></span>
> * <span data-ttu-id="9c2d8-162">生成模型</span><span class="sxs-lookup"><span data-stu-id="9c2d8-162">Generated the models</span></span>

<span data-ttu-id="9c2d8-163">转到下一步的教程，了解如何创建生成基于数据模型的代码。</span><span class="sxs-lookup"><span data-stu-id="9c2d8-163">Advance to the next tutorial to learn how to create generate code based on the data models.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="9c2d8-164">生成视图</span><span class="sxs-lookup"><span data-stu-id="9c2d8-164">Generating views</span></span>](generating-views.md)

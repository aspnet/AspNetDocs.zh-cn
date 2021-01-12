---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-entity-framework-scaffolding-and-migrations
title: ASP.NET MVC 4 实体框架基架和迁移 |Microsoft Docs
author: rick-anderson
description: 如果你熟悉 ASP.NET MVC 4 控制器方法，或者已完成 &quot; 帮助程序、窗体和验证 &quot; Hands-On lab，你应该知道 .。。
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 093c1362-f10b-407c-a708-be370f4b62b0
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-entity-framework-scaffolding-and-migrations
msc.type: authoredcontent
ms.openlocfilehash: 58aafe862f56ab13bf5a6bf8908a3baf582a08ff
ms.sourcegitcommit: d4e2a07eeb2cdf19f0bfbfab4a469970bc7e1c99
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/12/2021
ms.locfileid: "98105268"
---
# <a name="aspnet-mvc-4-entity-framework-scaffolding-and-migrations"></a><span data-ttu-id="76bca-103">ASP.NET MVC 4 Entity Framework 基架和迁移</span><span class="sxs-lookup"><span data-stu-id="76bca-103">ASP.NET MVC 4 Entity Framework Scaffolding and Migrations</span></span>

<span data-ttu-id="76bca-104">由[Web 训练营团队](https://twitter.com/webcamps)使用</span><span class="sxs-lookup"><span data-stu-id="76bca-104">By [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="76bca-105">下载 Web 训练营培训工具包</span><span class="sxs-lookup"><span data-stu-id="76bca-105">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

<span data-ttu-id="76bca-106">如果你熟悉 ASP.NET MVC 4 控制器方法，或者已完成了 &quot; 帮助程序、窗体和验证 &quot; Hands-On 实验室，你应该注意到，许多用于创建、更新、列出和删除任何数据实体的逻辑都在整个应用程序中重复。</span><span class="sxs-lookup"><span data-stu-id="76bca-106">If you are familiar with ASP.NET MVC 4 controller methods, or have completed the &quot;Helpers, Forms and Validation&quot; Hands-On lab, you should be aware that much of the logic to create, update, list and remove any data entity is repeated throughout the application.</span></span> <span data-ttu-id="76bca-107">请不要说，如果您的模型有多个要操作的类，您可能会花费相当长的时间来编写 POST，并为每个实体操作以及每个视图获取操作方法。</span><span class="sxs-lookup"><span data-stu-id="76bca-107">Not to mention that, if your model has several classes to manipulate, you will be likely to spend a considerable time writing the POST and GET action methods for each entity operation, as well as each of the views.</span></span>

<span data-ttu-id="76bca-108">在此实验室中，您将学习如何使用 ASP.NET MVC 4 基架自动生成应用程序 CRUD 的基线 (创建、读取、更新和删除) 。</span><span class="sxs-lookup"><span data-stu-id="76bca-108">In this lab you will learn how to use the ASP.NET MVC 4 scaffolding to automatically generate the baseline of your application's CRUD (Create, Read, Update and Delete).</span></span> <span data-ttu-id="76bca-109">从一个简单的模型类开始，而无需编写一行代码，你将创建一个包含所有 CRUD 操作的控制器以及所有必要的视图。</span><span class="sxs-lookup"><span data-stu-id="76bca-109">Starting from a simple model class, and, without writing a single line of code, you will create a controller that will contain all the CRUD operations, as well as the all the necessary views.</span></span> <span data-ttu-id="76bca-110">生成并运行简单解决方案后，将生成应用程序数据库以及用于数据操作的 MVC 逻辑和视图。</span><span class="sxs-lookup"><span data-stu-id="76bca-110">After building and running the simple solution, you will have the application database generated, together with the MVC logic and views for data manipulation.</span></span>

<span data-ttu-id="76bca-111">此外，你将了解在整个应用程序中使用实体框架迁移执行模型更新的难易程度如何。</span><span class="sxs-lookup"><span data-stu-id="76bca-111">In addition, you will learn how easy it is to use Entity Framework Migrations to perform model updates throughout your entire application.</span></span> <span data-ttu-id="76bca-112">实体框架迁移，你可以在模型发生了简单的步骤之后修改数据库。</span><span class="sxs-lookup"><span data-stu-id="76bca-112">Entity Framework Migrations will let you modify your database after the model has changed with simple steps.</span></span> <span data-ttu-id="76bca-113">为此，你将能够更有效地构建和维护 web 应用程序，利用 ASP.NET MVC 4 的最新功能。</span><span class="sxs-lookup"><span data-stu-id="76bca-113">With all these in mind, you will be able to build and maintain web applications more efficiently, taking advantage of the latest features of ASP.NET MVC 4.</span></span>

> [!NOTE]
> <span data-ttu-id="76bca-114">所有示例代码和代码段都包含在 Web 训练营培训工具包中，可从 [Microsoft-Web/WebCampTrainingKit 版本](https://aka.ms/webcamps-training-kit)获取。</span><span class="sxs-lookup"><span data-stu-id="76bca-114">All sample code and snippets are included in the Web Camps Training Kit, available from at [Microsoft-Web/WebCampTrainingKit Releases](https://aka.ms/webcamps-training-kit).</span></span> <span data-ttu-id="76bca-115">[ASP.NET MVC 4 实体框架基架和迁移](https://github.com/Microsoft-Web/HOL-EntityFrameworkScaffoldingAndMigrations)中提供了此实验室特定的项目。</span><span class="sxs-lookup"><span data-stu-id="76bca-115">The project specific to this lab is available at [ASP.NET MVC 4 Entity Framework Scaffolding and Migrations](https://github.com/Microsoft-Web/HOL-EntityFrameworkScaffoldingAndMigrations).</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="76bca-116">目标</span><span class="sxs-lookup"><span data-stu-id="76bca-116">Objectives</span></span>

<span data-ttu-id="76bca-117">在本 Hands-On 实验室中，您将学习如何：</span><span class="sxs-lookup"><span data-stu-id="76bca-117">In this Hands-On Lab, you will learn how to:</span></span>

- <span data-ttu-id="76bca-118">将 ASP.NET 基架用于控制器中的 CRUD 操作。</span><span class="sxs-lookup"><span data-stu-id="76bca-118">Use ASP.NET scaffolding for CRUD operations in controllers.</span></span>
- <span data-ttu-id="76bca-119">使用实体框架迁移更改数据库模型。</span><span class="sxs-lookup"><span data-stu-id="76bca-119">Change the database model using Entity Framework Migrations.</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="76bca-120">必备知识</span><span class="sxs-lookup"><span data-stu-id="76bca-120">Prerequisites</span></span>

<span data-ttu-id="76bca-121">你必须具有以下项才能完成此实验室：</span><span class="sxs-lookup"><span data-stu-id="76bca-121">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="76bca-122">适用于 Web 或高级 ([的 Microsoft Visual Studio Express 2012](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web)阅读[附录 A](#AppendixA) ，以获取有关如何) 安装它的说明。</span><span class="sxs-lookup"><span data-stu-id="76bca-122">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix A](#AppendixA) for instructions on how to install it).</span></span>

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="76bca-123">设置</span><span class="sxs-lookup"><span data-stu-id="76bca-123">Setup</span></span>

<span data-ttu-id="76bca-124">**安装代码片段**</span><span class="sxs-lookup"><span data-stu-id="76bca-124">**Installing Code Snippets**</span></span>

<span data-ttu-id="76bca-125">为方便起见，你将通过此实验室管理的大部分代码都作为 Visual Studio code 片段提供。</span><span class="sxs-lookup"><span data-stu-id="76bca-125">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="76bca-126">若要安装代码段，请运行 **.\Source\Setup\CodeSnippets.vsi** 文件。</span><span class="sxs-lookup"><span data-stu-id="76bca-126">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="76bca-127">如果你不熟悉 Visual Studio Code 代码段，并且想要了解如何使用它们，则可以参考本文档中的附录 &quot; [B：使用代码片段](#AppendixB) &quot; 。</span><span class="sxs-lookup"><span data-stu-id="76bca-127">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix B: Using Code Snippets](#AppendixB)&quot;.</span></span>

---

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="76bca-128">练习</span><span class="sxs-lookup"><span data-stu-id="76bca-128">Exercises</span></span>

<span data-ttu-id="76bca-129">以下练习将 Hands-On 实验室：</span><span class="sxs-lookup"><span data-stu-id="76bca-129">The following exercise make up this Hands-On Lab:</span></span>

1. [<span data-ttu-id="76bca-130">将 ASP.NET MVC 4 基架用于实体框架迁移</span><span class="sxs-lookup"><span data-stu-id="76bca-130">Using ASP.NET MVC 4 Scaffolding with Entity Framework Migrations</span></span>](#Exercise1)

> [!NOTE]
> <span data-ttu-id="76bca-131">此练习附带了一个 **结束** 文件夹，其中包含在完成练习后应获得的结果解决方案。</span><span class="sxs-lookup"><span data-stu-id="76bca-131">This exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercise.</span></span> <span data-ttu-id="76bca-132">如果需要更多帮助，请使用此解决方案作为指导。</span><span class="sxs-lookup"><span data-stu-id="76bca-132">You can use this solution as a guide if you need additional help working through the exercise.</span></span>

<span data-ttu-id="76bca-133">完成本实验的估计时间： **30 分钟**</span><span class="sxs-lookup"><span data-stu-id="76bca-133">Estimated time to complete this lab: **30 minutes**</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Using_ASPNET_MVC_4_Scaffolding_with_Entity_Framework_Migrations"></a>
### <a name="exercise-1-using-aspnet-mvc-4-scaffolding-with-entity-framework-migrations"></a><span data-ttu-id="76bca-134">练习1：将 ASP.NET MVC 4 基架用于实体框架迁移</span><span class="sxs-lookup"><span data-stu-id="76bca-134">Exercise 1: Using ASP.NET MVC 4 Scaffolding with Entity Framework Migrations</span></span>

<span data-ttu-id="76bca-135">ASP.NET MVC 基架提供一种以标准化方式生成 CRUD 操作的快速方法，从而创建必要的逻辑来使应用程序与数据库层交互。</span><span class="sxs-lookup"><span data-stu-id="76bca-135">ASP.NET MVC scaffolding provides a quick way to generate the CRUD operations in a standardized way, creating the necessary logic that lets your application interact with the database layer.</span></span>

<span data-ttu-id="76bca-136">在此练习中，您将学习如何将 ASP.NET MVC 4 基架与 code first 一起使用以创建 CRUD 方法。</span><span class="sxs-lookup"><span data-stu-id="76bca-136">In this exercise, you will learn how to use ASP.NET MVC 4 scaffolding with code first to create the CRUD methods.</span></span> <span data-ttu-id="76bca-137">然后，你将学习如何使用实体框架迁移来更新数据库中应用更改的模型。</span><span class="sxs-lookup"><span data-stu-id="76bca-137">Then, you will learn how to update your model applying the changes in the database by using Entity Framework Migrations.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1-_Creating_a_new_ASPNET_MVC_4_project_using_Scaffolding"></a>
#### <a name="task-1--creating-a-new-aspnet-mvc-4-project-using-scaffolding"></a><span data-ttu-id="76bca-138">任务 1-使用基架创建新的 ASP.NET MVC 4 项目</span><span class="sxs-lookup"><span data-stu-id="76bca-138">Task 1- Creating a new ASP.NET MVC 4 project using Scaffolding</span></span>

1. <span data-ttu-id="76bca-139">如果尚未打开，请启动 **Visual Studio 2012**。</span><span class="sxs-lookup"><span data-stu-id="76bca-139">If not already open, start **Visual Studio 2012**.</span></span>
2. <span data-ttu-id="76bca-140">选择 **文件 |新项目**。</span><span class="sxs-lookup"><span data-stu-id="76bca-140">Select **File | New Project**.</span></span> <span data-ttu-id="76bca-141">在 "新建项目" 对话框的 " **Visual c #" 下，|Web** 部分，选择 " **ASP.NET MVC 4 Web 应用程序**"。</span><span class="sxs-lookup"><span data-stu-id="76bca-141">In the New Project dialog, under the **Visual C# | Web** section, select **ASP.NET MVC 4 Web Application**.</span></span> <span data-ttu-id="76bca-142">将项目命名为 " **MVC4andEFMigrations** "，并将 "位置" 设置为 " **Source\Ex1-UsingMVC4ScaffoldingEFMigrations** "。</span><span class="sxs-lookup"><span data-stu-id="76bca-142">Name the project to **MVC4andEFMigrations** and set the location to **Source\Ex1-UsingMVC4ScaffoldingEFMigrations** folder of this lab.</span></span> <span data-ttu-id="76bca-143">将 **解决方案名称** 设置为 " **开始** "，并确保选中 " **创建解决方案的目录** "。</span><span class="sxs-lookup"><span data-stu-id="76bca-143">Set the **Solution name** to **Begin** and ensure **Create directory for solution** is checked.</span></span> <span data-ttu-id="76bca-144">单击“确定”。</span><span class="sxs-lookup"><span data-stu-id="76bca-144">Click **OK**.</span></span>

    <span data-ttu-id="76bca-145">!["新建 ASP.NET MVC 4 项目" 对话框](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image1.png ""新建 ASP.NET MVC 4 项目" 对话框")</span><span class="sxs-lookup"><span data-stu-id="76bca-145">![New ASP.NET MVC 4 Project Dialog Box](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image1.png "New ASP.NET MVC 4 Project Dialog Box")</span></span>

    <span data-ttu-id="76bca-146">*"新建 ASP.NET MVC 4 项目" 对话框*</span><span class="sxs-lookup"><span data-stu-id="76bca-146">*New ASP.NET MVC 4 Project Dialog Box*</span></span>
3. <span data-ttu-id="76bca-147">在 " **新建 ASP.NET MVC 4 项目** " 对话框中，选择 " **Internet 应用程序** " 模板，并确保 **Razor** 为所选的 **视图引擎**。</span><span class="sxs-lookup"><span data-stu-id="76bca-147">In the **New ASP.NET MVC 4 Project** dialog box select the **Internet Application** template, and make sure that **Razor** is the selected **View engine**.</span></span> <span data-ttu-id="76bca-148">单击“确定”以创建该项目  。</span><span class="sxs-lookup"><span data-stu-id="76bca-148">Click **OK** to create the project.</span></span>

    <span data-ttu-id="76bca-149">![New ASP.NET MVC 4 Internet 应用程序](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image2.png "New ASP.NET MVC 4 Internet 应用程序")</span><span class="sxs-lookup"><span data-stu-id="76bca-149">![New ASP.NET MVC 4 Internet Application](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image2.png "New ASP.NET MVC 4 Internet Application")</span></span>

    <span data-ttu-id="76bca-150">*New ASP.NET MVC 4 Internet 应用程序*</span><span class="sxs-lookup"><span data-stu-id="76bca-150">*New ASP.NET MVC 4 Internet Application*</span></span>
4. <span data-ttu-id="76bca-151">在解决方案资源管理器中，右键单击 " **模型** "，然后选择 " **添加 |** 用于创建 (POCO) 的简单类人员的类。</span><span class="sxs-lookup"><span data-stu-id="76bca-151">In the Solution Explorer, right-click **Models** and select **Add | Class** to create a simple class person (POCO).</span></span> <span data-ttu-id="76bca-152">将其命名为 **Person** 并单击 **"确定"**。</span><span class="sxs-lookup"><span data-stu-id="76bca-152">Name it **Person** and click **OK**.</span></span>
5. <span data-ttu-id="76bca-153">打开 Person 类并插入以下属性。</span><span class="sxs-lookup"><span data-stu-id="76bca-153">Open the Person class and insert the following properties.</span></span>

    <span data-ttu-id="76bca-154"> (代码片段- *ASP.NET MVC 4 和实体框架 Ex1 Person Properties*) </span><span class="sxs-lookup"><span data-stu-id="76bca-154">(Code Snippet - *ASP.NET MVC 4 and Entity Framework Migrations - Ex1 Person Properties*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample1.cs)]
6. <span data-ttu-id="76bca-155">单击 " **生成" |生成解决方案** 以保存更改并生成项目。</span><span class="sxs-lookup"><span data-stu-id="76bca-155">Click **Build | Build Solution** to save the changes and build the project.</span></span>

    <span data-ttu-id="76bca-156">![构建应用程序](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image3.png "生成应用程序")</span><span class="sxs-lookup"><span data-stu-id="76bca-156">![Building the application](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image3.png "Building the application")</span></span>

    <span data-ttu-id="76bca-157">*生成应用程序*</span><span class="sxs-lookup"><span data-stu-id="76bca-157">*Building the Application*</span></span>
7. <span data-ttu-id="76bca-158">在解决方案资源管理器中，右键单击 "控制器" 文件夹，然后选择 " **添加 |控制器**。</span><span class="sxs-lookup"><span data-stu-id="76bca-158">In the Solution Explorer, right-click the controllers folder and select **Add | Controller**.</span></span>
8. <span data-ttu-id="76bca-159">将控制器命名为 " *PersonController* "，并完成具有以下值的 " **基架" 选项** 。</span><span class="sxs-lookup"><span data-stu-id="76bca-159">Name the controller *PersonController* and complete the **Scaffolding options** with the following values.</span></span>

   1. <span data-ttu-id="76bca-160">在 " **模板** " 下拉列表中，选择 **包含读/写操作和视图的 MVC 控制器，并使用实体框架** 选项。</span><span class="sxs-lookup"><span data-stu-id="76bca-160">In the **Template** drop-down list, select the **MVC controller with read/write actions and views, using Entity Framework** option.</span></span>
   2. <span data-ttu-id="76bca-161">在 " **模型类** " 下拉列表中，选择 **Person** 类。</span><span class="sxs-lookup"><span data-stu-id="76bca-161">In the **Model class** drop-down list, select the **Person** class.</span></span>
   3. <span data-ttu-id="76bca-162">在 "**数据上下文类**" 列表中，选择 " **&lt; 新建数据上下文 &gt; ...**"。</span><span class="sxs-lookup"><span data-stu-id="76bca-162">In the **Data Context class** list, select **&lt;New data context...&gt;**.</span></span> <span data-ttu-id="76bca-163">选择任意名称并单击 **"确定"**。</span><span class="sxs-lookup"><span data-stu-id="76bca-163">Choose any name and click **OK**.</span></span>
   4. <span data-ttu-id="76bca-164">在 " **视图** " 下拉列表中，确保选择 " **Razor** "。</span><span class="sxs-lookup"><span data-stu-id="76bca-164">In the **Views** drop-down list, make sure that **Razor** is selected.</span></span>

      <span data-ttu-id="76bca-165">![添加具有基架的人员控制器](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image4.png "添加具有基架的人员控制器")</span><span class="sxs-lookup"><span data-stu-id="76bca-165">![Adding the Person controller with scaffolding](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image4.png "Adding the Person controller with scaffolding")</span></span>

      <span data-ttu-id="76bca-166">*添加具有基架的人员控制器*</span><span class="sxs-lookup"><span data-stu-id="76bca-166">*Adding the Person controller with scaffolding*</span></span>
9. <span data-ttu-id="76bca-167">单击 " **添加** " 以创建具有基架的人员的新控制器。</span><span class="sxs-lookup"><span data-stu-id="76bca-167">Click **Add** to create the new controller for Person with scaffolding.</span></span> <span data-ttu-id="76bca-168">你现在已经生成控制器操作以及视图。</span><span class="sxs-lookup"><span data-stu-id="76bca-168">You have now generated the controller actions as well as the views.</span></span>

    <span data-ttu-id="76bca-169">![创建具有基架的人员控制器之后](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image5.png "创建具有基架的人员控制器之后")</span><span class="sxs-lookup"><span data-stu-id="76bca-169">![After creating the Person controller with scaffolding](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image5.png "After creating the Person controller with scaffolding")</span></span>

    <span data-ttu-id="76bca-170">*创建具有基架的人员控制器之后*</span><span class="sxs-lookup"><span data-stu-id="76bca-170">*After creating the Person controller with scaffolding*</span></span>
10. <span data-ttu-id="76bca-171">打开 **PersonController** 类。</span><span class="sxs-lookup"><span data-stu-id="76bca-171">Open **PersonController** class.</span></span> <span data-ttu-id="76bca-172">请注意，已自动生成完整的 CRUD 操作方法。</span><span class="sxs-lookup"><span data-stu-id="76bca-172">Notice that the full CRUD action methods have been generated automatically.</span></span>

   <span data-ttu-id="76bca-173">![在人员控制器中](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image6.png "在人员控制器中")</span><span class="sxs-lookup"><span data-stu-id="76bca-173">![Inside the Person controller](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image6.png "Inside the Person controller")</span></span>

   <span data-ttu-id="76bca-174">*在人员控制器中*</span><span class="sxs-lookup"><span data-stu-id="76bca-174">*Inside the Person controller*</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2-_Running_the_application"></a>
#### <a name="task-2--running-the-application"></a><span data-ttu-id="76bca-175">任务 2-运行应用程序</span><span class="sxs-lookup"><span data-stu-id="76bca-175">Task 2- Running the application</span></span>

<span data-ttu-id="76bca-176">此时，数据库尚未创建。</span><span class="sxs-lookup"><span data-stu-id="76bca-176">At this point, the database is not yet created.</span></span> <span data-ttu-id="76bca-177">在此任务中，您将首次运行应用程序并测试 CRUD 操作。</span><span class="sxs-lookup"><span data-stu-id="76bca-177">In this task, you will run the application for the first time and test the CRUD operations.</span></span> <span data-ttu-id="76bca-178">将随 Code First 动态创建数据库。</span><span class="sxs-lookup"><span data-stu-id="76bca-178">The database will be created on the fly with Code First.</span></span>

1. <span data-ttu-id="76bca-179">按 **F5** 运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="76bca-179">Press **F5** to run the application.</span></span>
2. <span data-ttu-id="76bca-180">在浏览器中，将 **/Person** 添加到 URL 以打开 Person 页面。</span><span class="sxs-lookup"><span data-stu-id="76bca-180">In the browser, add **/Person** to the URL to open the Person page.</span></span>

    <span data-ttu-id="76bca-181">![应用程序首次运行](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image7.png "应用程序首次运行")</span><span class="sxs-lookup"><span data-stu-id="76bca-181">![Application first run](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image7.png "Application first run")</span></span>

    <span data-ttu-id="76bca-182">*应用程序：首次运行*</span><span class="sxs-lookup"><span data-stu-id="76bca-182">*Application: first run*</span></span>
3. <span data-ttu-id="76bca-183">现在，你将浏览人员页面并测试 CRUD 操作。</span><span class="sxs-lookup"><span data-stu-id="76bca-183">You will now explore the Person pages and test the CRUD operations.</span></span>

    1. <span data-ttu-id="76bca-184">单击 " **新建** " 以添加新人员。</span><span class="sxs-lookup"><span data-stu-id="76bca-184">Click **Create New** to add a new person.</span></span> <span data-ttu-id="76bca-185">输入名字和姓氏，然后单击 " **创建**"。</span><span class="sxs-lookup"><span data-stu-id="76bca-185">Enter a first name and a last name and click **Create**.</span></span>

        <span data-ttu-id="76bca-186">![添加新人员](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image8.png "添加新人员")</span><span class="sxs-lookup"><span data-stu-id="76bca-186">![Adding a new person](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image8.png "Adding a new person")</span></span>

        <span data-ttu-id="76bca-187">*添加新人员*</span><span class="sxs-lookup"><span data-stu-id="76bca-187">*Adding a new person*</span></span>
    2. <span data-ttu-id="76bca-188">在用户的列表中，可以删除、编辑或添加项。</span><span class="sxs-lookup"><span data-stu-id="76bca-188">In the person's list, you can delete, edit or add items.</span></span>

        <span data-ttu-id="76bca-189">![人员列表](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image9.png "人员列表")</span><span class="sxs-lookup"><span data-stu-id="76bca-189">![person list](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image9.png "person list")</span></span>

        <span data-ttu-id="76bca-190">*人员列表*</span><span class="sxs-lookup"><span data-stu-id="76bca-190">*Person list*</span></span>
    3. <span data-ttu-id="76bca-191">单击 " **详细信息** " 打开人员的详细信息。</span><span class="sxs-lookup"><span data-stu-id="76bca-191">Click **Details** to open the person's details.</span></span>

        <span data-ttu-id="76bca-192">![人员的详细信息](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image10.png "人员的详细信息")</span><span class="sxs-lookup"><span data-stu-id="76bca-192">![Person's details](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image10.png "Person's details")</span></span>

        <span data-ttu-id="76bca-193">*人员的详细信息*</span><span class="sxs-lookup"><span data-stu-id="76bca-193">*Person's details*</span></span>
4. <span data-ttu-id="76bca-194">关闭浏览器并返回到 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="76bca-194">Close the browser and return to Visual Studio.</span></span> <span data-ttu-id="76bca-195">请注意，在整个应用程序中为 person 实体创建了整个 CRUD-从模型到视图-无需编写一行代码！</span><span class="sxs-lookup"><span data-stu-id="76bca-195">Notice that you have created the whole CRUD for the person entity throughout your application -from the model to the views- without having to write a single line of code!</span></span>

<a id="Ex1Task3"></a>

<a id="Task_3-_Updating_the_database_using_Entity_Framework_Migrations"></a>
#### <a name="task-3--updating-the-database-using-entity-framework-migrations"></a><span data-ttu-id="76bca-196">任务 3-使用实体框架迁移更新数据库</span><span class="sxs-lookup"><span data-stu-id="76bca-196">Task 3- Updating the database using Entity Framework Migrations</span></span>

<span data-ttu-id="76bca-197">在此任务中，您将使用实体框架迁移来更新数据库。</span><span class="sxs-lookup"><span data-stu-id="76bca-197">In this task you will update the database using Entity Framework Migrations.</span></span> <span data-ttu-id="76bca-198">通过使用实体框架迁移功能，您将发现更改模型并反映数据库中的更改是多么简单。</span><span class="sxs-lookup"><span data-stu-id="76bca-198">You will discover how easy it is to change the model and reflect the changes in your databases by using the Entity Framework Migrations feature.</span></span>

1. <span data-ttu-id="76bca-199">打开包管理器控制台。</span><span class="sxs-lookup"><span data-stu-id="76bca-199">Open the Package Manager Console.</span></span> <span data-ttu-id="76bca-200">选择“工具” > “NuGet 包管理器” > “包管理器控制台”。</span><span class="sxs-lookup"><span data-stu-id="76bca-200">Select **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>
2. <span data-ttu-id="76bca-201">在“包管理器控制台”中，输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="76bca-201">In the Package Manager Console, enter the following command:</span></span>

    <span data-ttu-id="76bca-202">PMC</span><span class="sxs-lookup"><span data-stu-id="76bca-202">PMC</span></span>

    [!code-powershell[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample2.ps1)]

    <span data-ttu-id="76bca-203">![启用迁移](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image11.png "启用迁移")</span><span class="sxs-lookup"><span data-stu-id="76bca-203">![Enabling Migrations](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image11.png "Enabling Migrations")</span></span>

    <span data-ttu-id="76bca-204">*启用迁移*</span><span class="sxs-lookup"><span data-stu-id="76bca-204">*Enabling migrations*</span></span>

    <span data-ttu-id="76bca-205">Enable-Migration 命令创建 **迁移** 文件夹，其中包含用于初始化数据库的脚本。</span><span class="sxs-lookup"><span data-stu-id="76bca-205">The Enable-Migration command creates the **Migrations** folder, which contains a script to initialize the database.</span></span>

    <span data-ttu-id="76bca-206">![迁移文件夹](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image12.png "迁移文件夹")</span><span class="sxs-lookup"><span data-stu-id="76bca-206">![Migrations folder](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image12.png "Migrations folder")</span></span>

    <span data-ttu-id="76bca-207">*迁移文件夹*</span><span class="sxs-lookup"><span data-stu-id="76bca-207">*Migrations folder*</span></span>
3. <span data-ttu-id="76bca-208">打开 "迁移" 文件夹中的 **Configuration.cs** 文件。</span><span class="sxs-lookup"><span data-stu-id="76bca-208">Open the **Configuration.cs** file in the Migrations folder.</span></span> <span data-ttu-id="76bca-209">找到类构造函数并将 **AutomaticMigrationsEnabled** 值更改为 *true*。</span><span class="sxs-lookup"><span data-stu-id="76bca-209">Locate the class constructor and change the **AutomaticMigrationsEnabled** value to *true*.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample3.cs)]
4. <span data-ttu-id="76bca-210">打开 Person 类并为人员的中间名添加一个属性。</span><span class="sxs-lookup"><span data-stu-id="76bca-210">Open the Person class and add an attribute for the person's middle name.</span></span> <span data-ttu-id="76bca-211">通过此新属性，您将更改模型。</span><span class="sxs-lookup"><span data-stu-id="76bca-211">With this new attribute, you are changing the model.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample4.cs)]
5. <span data-ttu-id="76bca-212">选择 **生成 |** 用于生成应用程序的菜单上的 "生成解决方案"。</span><span class="sxs-lookup"><span data-stu-id="76bca-212">Select **Build | Build Solution** on the menu to build the application.</span></span>

    <span data-ttu-id="76bca-213">![构建应用程序](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image13.png "生成应用程序")</span><span class="sxs-lookup"><span data-stu-id="76bca-213">![Building the application](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image13.png "Building the application")</span></span>

    <span data-ttu-id="76bca-214">*构建应用程序*</span><span class="sxs-lookup"><span data-stu-id="76bca-214">*Building the application*</span></span>
6. <span data-ttu-id="76bca-215">在“包管理器控制台”中，输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="76bca-215">In the Package Manager Console, enter the following command:</span></span>

    <span data-ttu-id="76bca-216">PMC</span><span class="sxs-lookup"><span data-stu-id="76bca-216">PMC</span></span>

    [!code-powershell[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample5.ps1)]

    <span data-ttu-id="76bca-217">此命令会在数据对象中查找更改，然后将添加必要的命令来相应地修改数据库。</span><span class="sxs-lookup"><span data-stu-id="76bca-217">This command will look for changes in the data objects, and then, it will add the necessary commands to modify the database accordingly.</span></span>

    <span data-ttu-id="76bca-218">![添加中间名](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image14.png "添加中间名")</span><span class="sxs-lookup"><span data-stu-id="76bca-218">![Adding a middle name](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image14.png "Adding a middle name")</span></span>

    <span data-ttu-id="76bca-219">*添加中间名*</span><span class="sxs-lookup"><span data-stu-id="76bca-219">*Adding a middle name*</span></span>
7. <span data-ttu-id="76bca-220"> (可选) 可以运行以下命令，以使用差异更新生成 SQL 脚本。</span><span class="sxs-lookup"><span data-stu-id="76bca-220">(Optional) You can run the following command to generate a SQL script with the differential update.</span></span> <span data-ttu-id="76bca-221">这将允许您手动更新数据库 (在这种情况下，不需要) 或应用其他数据库中的更改：</span><span class="sxs-lookup"><span data-stu-id="76bca-221">This will let you update the database manually (In this case it's not necessary), or apply the changes in other databases:</span></span>

    <span data-ttu-id="76bca-222">PMC</span><span class="sxs-lookup"><span data-stu-id="76bca-222">PMC</span></span>

    [!code-powershell[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample6.ps1)]

    <span data-ttu-id="76bca-223">![生成 SQL 脚本](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image15.png "生成 SQL 脚本")</span><span class="sxs-lookup"><span data-stu-id="76bca-223">![Generating a SQL script](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image15.png "Generating a SQL script")</span></span>

    <span data-ttu-id="76bca-224">*生成 SQL 脚本*</span><span class="sxs-lookup"><span data-stu-id="76bca-224">*Generating a SQL script*</span></span>

    <span data-ttu-id="76bca-225">![SQL 脚本更新](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image16.png "SQL 脚本更新")</span><span class="sxs-lookup"><span data-stu-id="76bca-225">![SQL Script update](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image16.png "SQL Script update")</span></span>

    <span data-ttu-id="76bca-226">*SQL 脚本更新*</span><span class="sxs-lookup"><span data-stu-id="76bca-226">*SQL Script update*</span></span>
8. <span data-ttu-id="76bca-227">在 "程序包管理器控制台" 中，输入以下命令以更新数据库：</span><span class="sxs-lookup"><span data-stu-id="76bca-227">In the Package Manager Console, enter the following command to update the database:</span></span>

    <span data-ttu-id="76bca-228">PMC</span><span class="sxs-lookup"><span data-stu-id="76bca-228">PMC</span></span>

    [!code-powershell[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample7.ps1)]

    <span data-ttu-id="76bca-229">![更新数据库](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image17.png "更新数据库")</span><span class="sxs-lookup"><span data-stu-id="76bca-229">![Updating the Database](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image17.png "Updating the Database")</span></span>

    <span data-ttu-id="76bca-230">*更新数据库*</span><span class="sxs-lookup"><span data-stu-id="76bca-230">*Updating the Database*</span></span>

    <span data-ttu-id="76bca-231">这 **将在 Person 表中** 添加 **MiddleName** 列以与 **Person** 类的当前定义匹配。</span><span class="sxs-lookup"><span data-stu-id="76bca-231">This will add the **MiddleName** column in the **People** table to match the current definition of the **Person** class.</span></span>
9. <span data-ttu-id="76bca-232">更新数据库后，右键单击 "控制器" 文件夹，然后选择 " **添加 |** 如果) ，控制器将再次添加人员控制器 (完成。</span><span class="sxs-lookup"><span data-stu-id="76bca-232">Once the database is updated, right-click the Controller folder and select **Add | Controller** to add the Person controller again (Complete with the same values).</span></span> <span data-ttu-id="76bca-233">这将更新添加新属性的现有方法和视图。</span><span class="sxs-lookup"><span data-stu-id="76bca-233">This will update the existing methods and views adding the new attribute.</span></span>

    <span data-ttu-id="76bca-234">![添加控制器更新](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image18.png "添加控制器更新")</span><span class="sxs-lookup"><span data-stu-id="76bca-234">![Adding a controller update](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image18.png "Adding a controller update")</span></span>

    <span data-ttu-id="76bca-235">*更新控制器*</span><span class="sxs-lookup"><span data-stu-id="76bca-235">*Updating the controller*</span></span>
10. <span data-ttu-id="76bca-236">单击“添加” 。</span><span class="sxs-lookup"><span data-stu-id="76bca-236">Click **Add**.</span></span> <span data-ttu-id="76bca-237">然后，选择 " **覆盖 PersonController.cs** 的值" 和 " **覆盖关联的视图** "，然后单击 **"确定"**。</span><span class="sxs-lookup"><span data-stu-id="76bca-237">Then, select the values **Overwrite PersonController.cs** and the **Overwrite associated views** and click **OK**.</span></span>

   ![添加控制器覆盖](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image19.png)

   <span data-ttu-id="76bca-239">*更新控制器*</span><span class="sxs-lookup"><span data-stu-id="76bca-239">*Updating the controller*</span></span>

<a id="Ex1Task4"></a>

<a id="Task4-_Running_the_application"></a>
#### <a name="task4--running-the-application"></a><span data-ttu-id="76bca-240">Task4-运行应用程序</span><span class="sxs-lookup"><span data-stu-id="76bca-240">Task4- Running the application</span></span>

1. <span data-ttu-id="76bca-241">按 **F5** 运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="76bca-241">Press **F5** to run the application.</span></span>
2. <span data-ttu-id="76bca-242">打开 **/Person**。</span><span class="sxs-lookup"><span data-stu-id="76bca-242">Open **/Person**.</span></span> <span data-ttu-id="76bca-243">请注意，数据已保留，而中间名称列已添加。</span><span class="sxs-lookup"><span data-stu-id="76bca-243">Notice that the data was preserved, while the middle name column was added.</span></span>

    <span data-ttu-id="76bca-244">![添加的中间名](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image20.png "添加的中间名")</span><span class="sxs-lookup"><span data-stu-id="76bca-244">![Middle Name added](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image20.png "Middle Name added")</span></span>

    <span data-ttu-id="76bca-245">*添加的中间名*</span><span class="sxs-lookup"><span data-stu-id="76bca-245">*Middle Name added*</span></span>
3. <span data-ttu-id="76bca-246">如果单击 " **编辑**"，则可以将中间名添加到当前用户。</span><span class="sxs-lookup"><span data-stu-id="76bca-246">If you click **Edit**, you will be able to add a middle name to the current person.</span></span>

    <span data-ttu-id="76bca-247">![中间名版本](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image21.png "中间名版本")</span><span class="sxs-lookup"><span data-stu-id="76bca-247">![Middle Name edition](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image21.png "Middle Name edition")</span></span>

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="76bca-248">总结</span><span class="sxs-lookup"><span data-stu-id="76bca-248">Summary</span></span>

<span data-ttu-id="76bca-249">在本 Hands-On 实验室中，你已学习了使用任何模型类通过 ASP.NET MVC 4 基架创建 CRUD 操作的简单步骤。</span><span class="sxs-lookup"><span data-stu-id="76bca-249">In this Hands-On lab, you have learned simple steps to create CRUD operations with ASP.NET MVC 4 Scaffolding using any model class.</span></span> <span data-ttu-id="76bca-250">然后，你已了解如何通过使用实体框架迁移，在应用程序中执行端到端更新（从数据库到视图）。</span><span class="sxs-lookup"><span data-stu-id="76bca-250">Then, you have learned how to perform an end to end update in your application -from the database to the views- by using Entity Framework Migrations.</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="76bca-251">附录 A：安装 Visual Studio Express 2012 for Web</span><span class="sxs-lookup"><span data-stu-id="76bca-251">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="76bca-252">你可以使用 Microsoft Web 平台安装程序安装 **Web Microsoft Visual Studio Express 2012** 或其他 &quot; Express &quot; 版本。 **[](https://www.microsoft.com/web/downloads/platform.aspx)**</span><span class="sxs-lookup"><span data-stu-id="76bca-252">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="76bca-253">以下说明将指导你完成使用 *Microsoft Web 平台安装程序* 安装 *Visual studio Express 2012 for Web* 的步骤。</span><span class="sxs-lookup"><span data-stu-id="76bca-253">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="76bca-254">转到 [https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)。</span><span class="sxs-lookup"><span data-stu-id="76bca-254">Go to [https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="76bca-255">或者，如果你已经安装了 Web 平台安装程序，则可以打开它并 &quot; <em>使用 WINDOWS Azure SDK 搜索产品 Visual Studio Express 2012 for Web</em> &quot; 。</span><span class="sxs-lookup"><span data-stu-id="76bca-255">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Windows Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="76bca-256">单击 " **立即安装**"。</span><span class="sxs-lookup"><span data-stu-id="76bca-256">Click on **Install Now**.</span></span> <span data-ttu-id="76bca-257">如果你没有 **Web 平台安装程序** ，则会重定向到 "下载并安装"。</span><span class="sxs-lookup"><span data-stu-id="76bca-257">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="76bca-258">**Web 平台安装程序** 打开后，单击 "**安装**" 以启动安装程序。</span><span class="sxs-lookup"><span data-stu-id="76bca-258">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="76bca-259">![安装 Visual Studio Express](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image22.png "安装 Visual Studio Express")</span><span class="sxs-lookup"><span data-stu-id="76bca-259">![Install Visual Studio Express](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image22.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="76bca-260">*安装 Visual Studio Express*</span><span class="sxs-lookup"><span data-stu-id="76bca-260">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="76bca-261">阅读所有产品的许可证和条款，单击 " **我接受** " 以继续。</span><span class="sxs-lookup"><span data-stu-id="76bca-261">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![接受许可条款](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image23.png)

    <span data-ttu-id="76bca-263">*接受许可条款*</span><span class="sxs-lookup"><span data-stu-id="76bca-263">*Accepting the license terms*</span></span>
5. <span data-ttu-id="76bca-264">等待下载和安装过程完成。</span><span class="sxs-lookup"><span data-stu-id="76bca-264">Wait until the downloading and installation process completes.</span></span>

    ![安装进度](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image24.png)

    <span data-ttu-id="76bca-266">*安装进度*</span><span class="sxs-lookup"><span data-stu-id="76bca-266">*Installation progress*</span></span>
6. <span data-ttu-id="76bca-267">安装完成后，单击 " **完成**"。</span><span class="sxs-lookup"><span data-stu-id="76bca-267">When the installation completes, click **Finish**.</span></span>

    ![安装完成](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image25.png)

    <span data-ttu-id="76bca-269">*安装完成*</span><span class="sxs-lookup"><span data-stu-id="76bca-269">*Installation completed*</span></span>
7. <span data-ttu-id="76bca-270">单击 " **退出** " 以关闭 Web 平台安装程序。</span><span class="sxs-lookup"><span data-stu-id="76bca-270">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="76bca-271">若要打开 Web Visual Studio Express，请在 "**开始**" 屏幕上，单击 "开始撰写 &quot; **VS Express** &quot; "，然后单击 " **VS Express for Web** " 磁贴。</span><span class="sxs-lookup"><span data-stu-id="76bca-271">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![VS Express for Web 磁贴](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image26.png)

    <span data-ttu-id="76bca-273">*VS Express for Web 磁贴*</span><span class="sxs-lookup"><span data-stu-id="76bca-273">*VS Express for Web tile*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Using_Code_Snippets"></a>
## <a name="appendix-b-using-code-snippets"></a><span data-ttu-id="76bca-274">附录 B：使用代码片段</span><span class="sxs-lookup"><span data-stu-id="76bca-274">Appendix B: Using Code Snippets</span></span>

<span data-ttu-id="76bca-275">使用代码片段，您可以随时获得所需的全部代码。</span><span class="sxs-lookup"><span data-stu-id="76bca-275">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="76bca-276">实验室文档将告诉你何时可以使用它们，如下图所示。</span><span class="sxs-lookup"><span data-stu-id="76bca-276">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="76bca-277">![使用 Visual Studio code 代码段将代码插入到项目中](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image27.png "使用 Visual Studio code 代码段将代码插入到项目中")</span><span class="sxs-lookup"><span data-stu-id="76bca-277">![Using Visual Studio code snippets to insert code into your project](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image27.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="76bca-278">*使用 Visual Studio code 代码段将代码插入到项目中*</span><span class="sxs-lookup"><span data-stu-id="76bca-278">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="76bca-279">\***使用键盘 (c # 仅) _ 添加代码片段**</span><span class="sxs-lookup"><span data-stu-id="76bca-279">\***To add a code snippet using the keyboard (C# only)** _</span></span>

1. <span data-ttu-id="76bca-280">将光标放在要插入代码的位置。</span><span class="sxs-lookup"><span data-stu-id="76bca-280">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="76bca-281">开始键入代码片段名称 (没有空格或连字符) 。</span><span class="sxs-lookup"><span data-stu-id="76bca-281">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="76bca-282">请注意，IntelliSense 显示匹配的代码段名称。</span><span class="sxs-lookup"><span data-stu-id="76bca-282">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="76bca-283">选择正确的代码段 (或保留键入内容，直到选择了整个代码段的名称) 。</span><span class="sxs-lookup"><span data-stu-id="76bca-283">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="76bca-284">按 Tab 键两次，将代码段插入到光标位置。</span><span class="sxs-lookup"><span data-stu-id="76bca-284">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="76bca-285">![开始键入代码片段名称](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image28.png "开始键入代码片段名称")</span><span class="sxs-lookup"><span data-stu-id="76bca-285">![Start typing the snippet name](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image28.png "Start typing the snippet name")</span></span>

<span data-ttu-id="76bca-286">_Start 键入代码片段名称 \*</span><span class="sxs-lookup"><span data-stu-id="76bca-286">_Start typing the snippet name\*</span></span>

<span data-ttu-id="76bca-287">![按 Tab 键以选择突出显示的代码段](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image29.png "按 Tab 键以选择突出显示的代码段")</span><span class="sxs-lookup"><span data-stu-id="76bca-287">![Press Tab to select the highlighted snippet](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image29.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="76bca-288">*按 Tab 键以选择突出显示的代码段*</span><span class="sxs-lookup"><span data-stu-id="76bca-288">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="76bca-289">![再次按 Tab 键，代码片段将展开](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image30.png "再次按 Tab 键，代码片段将展开")</span><span class="sxs-lookup"><span data-stu-id="76bca-289">![Press Tab again and the snippet will expand](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image30.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="76bca-290">*再次按 Tab 键，代码片段将展开*</span><span class="sxs-lookup"><span data-stu-id="76bca-290">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="76bca-291">\***若要使用鼠标 (c # 添加代码片段，请 Visual Basic 和 XML)** _ 1。</span><span class="sxs-lookup"><span data-stu-id="76bca-291">\***To add a code snippet using the mouse (C#, Visual Basic and XML)** _ 1.</span></span> <span data-ttu-id="76bca-292">右键单击要插入代码片段的位置。</span><span class="sxs-lookup"><span data-stu-id="76bca-292">Right-click where you want to insert the code snippet.</span></span>

1. <span data-ttu-id="76bca-293">依次选择 ""、"*插入代码段* **" 和 "我的代码片段"**。</span><span class="sxs-lookup"><span data-stu-id="76bca-293">Select _ *Insert Snippet*\* followed by **My Code Snippets**.</span></span>
2. <span data-ttu-id="76bca-294">通过单击从列表中选择相关的代码片段。</span><span class="sxs-lookup"><span data-stu-id="76bca-294">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="76bca-295">![右键单击要插入代码片段的位置，然后选择 "插入代码片段"](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image31.png "右键单击要插入代码片段的位置，然后选择 "插入代码片段"")</span><span class="sxs-lookup"><span data-stu-id="76bca-295">![Right-click where you want to insert the code snippet and select Insert Snippet](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image31.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="76bca-296">*右键单击要插入代码片段的位置，然后选择 "插入代码片段"*</span><span class="sxs-lookup"><span data-stu-id="76bca-296">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="76bca-297">![通过单击从列表中选择相关的代码片段](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image32.png "通过单击从列表中选择相关的代码片段")</span><span class="sxs-lookup"><span data-stu-id="76bca-297">![Pick the relevant snippet from the list, by clicking on it](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image32.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="76bca-298">*通过单击从列表中选择相关的代码片段*</span><span class="sxs-lookup"><span data-stu-id="76bca-298">*Pick the relevant snippet from the list, by clicking on it*</span></span>

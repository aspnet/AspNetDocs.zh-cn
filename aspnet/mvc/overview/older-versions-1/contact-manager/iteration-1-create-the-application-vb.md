---
uid: mvc/overview/older-versions-1/contact-manager/iteration-1-create-the-application-vb
title: 迭代 1 – 创建应用程序 (VB) |Microsoft Docs
author: microsoft
description: 在第一次迭代中，我们创建联系人管理器中的最简单方法可能。 我们将添加对基本数据库操作的支持：创建、 读取、 更新和 D....
ms.author: riande
ms.date: 02/20/2009
ms.assetid: 5b033582-1646-42c2-b20d-7edc8814e970
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-1-create-the-application-vb
msc.type: authoredcontent
ms.openlocfilehash: f1909279f36c0bd3bfb22fe7a892ef8cfad3052f
ms.sourcegitcommit: 289e051cc8a90e8f7127e239fda73047bde4de12
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2019
ms.locfileid: "58422865"
---
<a name="iteration-1--create-the-application-vb"></a><span data-ttu-id="dd74d-104">迭代 1 – 创建应用程序 (VB)</span><span class="sxs-lookup"><span data-stu-id="dd74d-104">Iteration #1 – Create the Application (VB)</span></span>
====================
<span data-ttu-id="dd74d-105">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="dd74d-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="dd74d-106">下载代码</span><span class="sxs-lookup"><span data-stu-id="dd74d-106">Download Code</span></span>](iteration-1-create-the-application-vb/_static/contactmanager_1_vb1.zip)

> <span data-ttu-id="dd74d-107">在第一次迭代中，我们创建联系人管理器中的最简单方法可能。</span><span class="sxs-lookup"><span data-stu-id="dd74d-107">In the first iteration, we create the Contact Manager in the simplest way possible.</span></span> <span data-ttu-id="dd74d-108">我们将添加对基本数据库操作的支持：创建、 读取、 更新和删除 (CRUD)。</span><span class="sxs-lookup"><span data-stu-id="dd74d-108">We add support for basic database operations: Create, Read, Update, and Delete (CRUD).</span></span>


## <a name="building-a-contact-management-aspnet-mvc-application-vb"></a><span data-ttu-id="dd74d-109">构建联系人管理 ASP.NET MVC 应用程序 (VB)</span><span class="sxs-lookup"><span data-stu-id="dd74d-109">Building a Contact Management ASP.NET MVC Application (VB)</span></span>

<span data-ttu-id="dd74d-110">在本系列教程，我们构建整个联系人管理应用程序从头到尾完成。</span><span class="sxs-lookup"><span data-stu-id="dd74d-110">In this series of tutorials, we build an entire Contact Management application from start to finish.</span></span> <span data-ttu-id="dd74d-111">联系人管理器应用程序，可存储联系人信息的名称，电话号码和电子邮件地址的人的列表。</span><span class="sxs-lookup"><span data-stu-id="dd74d-111">The Contact Manager application enables you to store contact information - names, phone numbers and email addresses - for a list of people.</span></span>

<span data-ttu-id="dd74d-112">我们通过多个迭代中生成应用程序。</span><span class="sxs-lookup"><span data-stu-id="dd74d-112">We build the application over multiple iterations.</span></span> <span data-ttu-id="dd74d-113">每次迭代时，我们逐渐提高应用程序。</span><span class="sxs-lookup"><span data-stu-id="dd74d-113">With each iteration, we gradually improve the application.</span></span> <span data-ttu-id="dd74d-114">此多个迭代方法的目标是帮助你了解每个更改的原因。</span><span class="sxs-lookup"><span data-stu-id="dd74d-114">The goal of this multiple iteration approach is to enable you to understand the reason for each change.</span></span>

- <span data-ttu-id="dd74d-115">迭代 1-创建应用程序。</span><span class="sxs-lookup"><span data-stu-id="dd74d-115">Iteration #1 - Create the application.</span></span> <span data-ttu-id="dd74d-116">在第一次迭代中，我们创建联系人管理器中的最简单方法可能。</span><span class="sxs-lookup"><span data-stu-id="dd74d-116">In the first iteration, we create the Contact Manager in the simplest way possible.</span></span> <span data-ttu-id="dd74d-117">我们将添加对基本数据库操作的支持：创建、 读取、 更新和删除 (CRUD)。</span><span class="sxs-lookup"><span data-stu-id="dd74d-117">We add support for basic database operations: Create, Read, Update, and Delete (CRUD).</span></span>

- <span data-ttu-id="dd74d-118">迭代 2 – 使应用程序看上去更美观。</span><span class="sxs-lookup"><span data-stu-id="dd74d-118">Iteration #2 - Make the application look nice.</span></span> <span data-ttu-id="dd74d-119">在此迭代中，我们通过修改默认 ASP.NET MVC 视图母版页和级联样式表提高应用程序的外观。</span><span class="sxs-lookup"><span data-stu-id="dd74d-119">In this iteration, we improve the appearance of the application by modifying the default ASP.NET MVC view master page and cascading style sheet.</span></span>

- <span data-ttu-id="dd74d-120">迭代 3-添加窗体验证。</span><span class="sxs-lookup"><span data-stu-id="dd74d-120">Iteration #3 - Add form validation.</span></span> <span data-ttu-id="dd74d-121">在第三个迭代中，我们将添加基本窗体验证。</span><span class="sxs-lookup"><span data-stu-id="dd74d-121">In the third iteration, we add basic form validation.</span></span> <span data-ttu-id="dd74d-122">我们阻止用户提交窗体而无法完成所需的窗体字段。</span><span class="sxs-lookup"><span data-stu-id="dd74d-122">We prevent people from submitting a form without completing required form fields.</span></span> <span data-ttu-id="dd74d-123">我们还验证电子邮件地址和电话号码。</span><span class="sxs-lookup"><span data-stu-id="dd74d-123">We also validate email addresses and phone numbers.</span></span>

- <span data-ttu-id="dd74d-124">迭代 4-使应用程序松散耦合。</span><span class="sxs-lookup"><span data-stu-id="dd74d-124">Iteration #4 - Make the application loosely coupled.</span></span> <span data-ttu-id="dd74d-125">在此第四个迭代中，我们将充分利用多个软件设计模式，以使其更轻松地监视和修改联系人管理器应用程序。</span><span class="sxs-lookup"><span data-stu-id="dd74d-125">In this fourth iteration, we take advantage of several software design patterns to make it easier to maintain and modify the Contact Manager application.</span></span> <span data-ttu-id="dd74d-126">例如，我们将重构应用程序以使用存储库模式和依赖关系注入模式。</span><span class="sxs-lookup"><span data-stu-id="dd74d-126">For example, we refactor our application to use the Repository pattern and the Dependency Injection pattern.</span></span>

- <span data-ttu-id="dd74d-127">迭代 5 — 创建单元测试。</span><span class="sxs-lookup"><span data-stu-id="dd74d-127">Iteration #5 - Create unit tests.</span></span> <span data-ttu-id="dd74d-128">在第五个迭代中，我们使我们的应用程序更轻松地监视和修改通过添加单元测试。</span><span class="sxs-lookup"><span data-stu-id="dd74d-128">In the fifth iteration, we make our application easier to maintain and modify by adding unit tests.</span></span> <span data-ttu-id="dd74d-129">我们模拟我们数据模型类，并生成为控制器和验证逻辑单元测试。</span><span class="sxs-lookup"><span data-stu-id="dd74d-129">We mock our data model classes and build unit tests for our controllers and validation logic.</span></span>

- <span data-ttu-id="dd74d-130">迭代 6-使用测试驱动的开发。</span><span class="sxs-lookup"><span data-stu-id="dd74d-130">Iteration #6 - Use test-driven development.</span></span> <span data-ttu-id="dd74d-131">在此第六个迭代中，我们将添加新功能到我们的应用程序通过首先编写单元测试并针对单元测试编写的代码。</span><span class="sxs-lookup"><span data-stu-id="dd74d-131">In this sixth iteration, we add new functionality to our application by writing unit tests first and writing code against the unit tests.</span></span> <span data-ttu-id="dd74d-132">在此迭代中，我们将添加联系人组。</span><span class="sxs-lookup"><span data-stu-id="dd74d-132">In this iteration, we add contact groups.</span></span>

- <span data-ttu-id="dd74d-133">迭代 7-添加 Ajax 功能。</span><span class="sxs-lookup"><span data-stu-id="dd74d-133">Iteration #7 - Add Ajax functionality.</span></span> <span data-ttu-id="dd74d-134">在第七个迭代中，我们通过添加对 Ajax 支持提高响应能力和我们的应用程序的性能。</span><span class="sxs-lookup"><span data-stu-id="dd74d-134">In the seventh iteration, we improve the responsiveness and performance of our application by adding support for Ajax.</span></span>

## <a name="this-iteration"></a><span data-ttu-id="dd74d-135">此迭代</span><span class="sxs-lookup"><span data-stu-id="dd74d-135">This Iteration</span></span>

<span data-ttu-id="dd74d-136">在此第一个迭代中，我们构建的基本应用程序。</span><span class="sxs-lookup"><span data-stu-id="dd74d-136">In this first iteration, we build the basic application.</span></span> <span data-ttu-id="dd74d-137">目标是尽可能最快且最简单方式构建联系人管理器。</span><span class="sxs-lookup"><span data-stu-id="dd74d-137">The goal is to build the Contact Manager in the fastest and simplest way possible.</span></span> <span data-ttu-id="dd74d-138">在更高版本迭代中，我们改进应用程序的设计。</span><span class="sxs-lookup"><span data-stu-id="dd74d-138">In later iterations, we improve the design of the application.</span></span>

<span data-ttu-id="dd74d-139">联系人管理器应用程序是一个基本的数据库驱动的应用程序。</span><span class="sxs-lookup"><span data-stu-id="dd74d-139">The Contact Manager application is a basic database-driven application.</span></span> <span data-ttu-id="dd74d-140">应用程序可用于创建新的联系人、 编辑现有联系人和删除联系人。</span><span class="sxs-lookup"><span data-stu-id="dd74d-140">You can use the application to create new contacts, edit existing contacts, and delete contacts.</span></span>

<span data-ttu-id="dd74d-141">在此迭代中，我们将完成以下步骤：</span><span class="sxs-lookup"><span data-stu-id="dd74d-141">In this iteration, we complete the following steps:</span></span>

1. <span data-ttu-id="dd74d-142">ASP.NET MVC 应用程序</span><span class="sxs-lookup"><span data-stu-id="dd74d-142">ASP.NET MVC application</span></span>
2. <span data-ttu-id="dd74d-143">创建一个数据库来存储我们的联系人</span><span class="sxs-lookup"><span data-stu-id="dd74d-143">Create a database to store our contacts</span></span>
3. <span data-ttu-id="dd74d-144">生成模型类，以便使用我们的 Microsoft 实体框架的数据库</span><span class="sxs-lookup"><span data-stu-id="dd74d-144">Generate a model class for our database with the Microsoft Entity Framework</span></span>
4. <span data-ttu-id="dd74d-145">创建控制器操作和视图，使我们能够列出所有数据库中的联系人</span><span class="sxs-lookup"><span data-stu-id="dd74d-145">Create a controller action and view that enables us to list all of the contacts in the database</span></span>
5. <span data-ttu-id="dd74d-146">创建控制器操作和视图，使我们能够在数据库中创建一个新的联系人</span><span class="sxs-lookup"><span data-stu-id="dd74d-146">Create controller actions and a view that enables us to create a new contact in the database</span></span>
6. <span data-ttu-id="dd74d-147">创建控制器操作和使我们能够编辑现有联系人数据库中的视图</span><span class="sxs-lookup"><span data-stu-id="dd74d-147">Create controller actions and a view that enables us to edit an existing contact in the database</span></span>
7. <span data-ttu-id="dd74d-148">创建控制器操作和使我们能够删除现有数据库中的联系人的视图</span><span class="sxs-lookup"><span data-stu-id="dd74d-148">Create controller actions and a view that enables us to delete an existing contact in the database</span></span>

## <a name="software-prerequisites"></a><span data-ttu-id="dd74d-149">软件必备项</span><span class="sxs-lookup"><span data-stu-id="dd74d-149">Software Prerequisites</span></span>

<span data-ttu-id="dd74d-150">在 ASP.NET MVC 应用程序中，您必须具有 Visual Studio 2008 或 （Visual Web Developer 不包含所有 Visual Studio 的高级功能的 Visual Studio 的免费版本) 在计算机上安装 Visual Web Developer 2008。</span><span class="sxs-lookup"><span data-stu-id="dd74d-150">In ASP.NET MVC applications, you must have either Visual Studio 2008 or Visual Web Developer 2008 installed on your computer (Visual Web Developer is a free version of Visual Studio that does not include all of the advanced features of Visual Studio).</span></span> <span data-ttu-id="dd74d-151">可以从以下地址下载是 Visual Studio 2008 试用版或 Visual Web Developer:</span><span class="sxs-lookup"><span data-stu-id="dd74d-151">You can download either the trial version of Visual Studio 2008 or Visual Web Developer from the following address:</span></span>

[https://www.asp.net/downloads/essential/](https://www.asp.net/downloads/essential)

> [!NOTE] 
> 
> <span data-ttu-id="dd74d-152">使用 Visual Web Developer 的 ASP.NET MVC 应用程序，您必须安装的 Visual Web Developer Service Pack 1。</span><span class="sxs-lookup"><span data-stu-id="dd74d-152">For ASP.NET MVC applications with Visual Web Developer, you must have Visual Web Developer Service Pack 1 installed.</span></span> <span data-ttu-id="dd74d-153">不带 Service Pack 1，无法创建 Web 应用程序项目。</span><span class="sxs-lookup"><span data-stu-id="dd74d-153">Without Service Pack 1, you cannot create Web Application Projects.</span></span>


<span data-ttu-id="dd74d-154">ASP.NET MVC 框架。</span><span class="sxs-lookup"><span data-stu-id="dd74d-154">ASP.NET MVC framework.</span></span> <span data-ttu-id="dd74d-155">您可以从以下地址下载 ASP.NET MVC framework:</span><span class="sxs-lookup"><span data-stu-id="dd74d-155">You can download the ASP.NET MVC framework from the following address:</span></span>

[https://www.asp.net/mvc](../../../index.md)

<span data-ttu-id="dd74d-156">在本教程中，我们可以使用 Microsoft Entity Framework 访问数据库。</span><span class="sxs-lookup"><span data-stu-id="dd74d-156">In this tutorial, we use the Microsoft Entity Framework to access a database.</span></span> <span data-ttu-id="dd74d-157">实体框架将附带.NET Framework 3.5 Service Pack 1。</span><span class="sxs-lookup"><span data-stu-id="dd74d-157">The Entity Framework is included with .NET Framework 3.5 Service Pack 1.</span></span> <span data-ttu-id="dd74d-158">可以从以下位置下载此 service pack:</span><span class="sxs-lookup"><span data-stu-id="dd74d-158">You can download this service pack from the following location:</span></span>

[<span data-ttu-id="dd74d-159">https://www.microsoft.com/downloads/details.aspx?familyid=ab99342f-5d1a-413d-8319-81da479ab0d7&amp;displaylang=en</span><span class="sxs-lookup"><span data-stu-id="dd74d-159">https://www.microsoft.com/downloads/details.aspx?familyid=ab99342f-5d1a-413d-8319-81da479ab0d7&amp;displaylang=en</span></span>](https://www.microsoft.com/downloads/details.aspx?familyid=ab99342f-5d1a-413d-8319-81da479ab0d7&amp;displaylang=en)

<span data-ttu-id="dd74d-160">为执行每个这些下载的替代方法，可以充分利用 Web 平台安装程序 (Web PI)。</span><span class="sxs-lookup"><span data-stu-id="dd74d-160">As an alternative to performing each of these downloads one by one, you can take advantage of the Web Platform Installer (Web PI).</span></span> <span data-ttu-id="dd74d-161">您可以从以下地址下载 Web PI:</span><span class="sxs-lookup"><span data-stu-id="dd74d-161">You can download the Web PI from the following address:</span></span>

[https://www.asp.net/downloads/essential/](https://www.asp.net/downloads/essential)

## <a name="aspnet-mvc-project"></a><span data-ttu-id="dd74d-162">ASP.NET MVC 项目</span><span class="sxs-lookup"><span data-stu-id="dd74d-162">ASP.NET MVC Project</span></span>

<span data-ttu-id="dd74d-163">ASP.NET MVC Web 应用程序项目。</span><span class="sxs-lookup"><span data-stu-id="dd74d-163">ASP.NET MVC Web Application Project.</span></span> <span data-ttu-id="dd74d-164">启动 Visual Studio 并选择菜单选项**文件，新的项目**。</span><span class="sxs-lookup"><span data-stu-id="dd74d-164">Launch Visual Studio and select the menu option **File, New Project**.</span></span> <span data-ttu-id="dd74d-165">**新的项目**对话框 （请参见图 1）。</span><span class="sxs-lookup"><span data-stu-id="dd74d-165">The **New Project** dialog appears (see Figure 1).</span></span> <span data-ttu-id="dd74d-166">选择**Web**项目类型和**ASP.NET MVC Web 应用程序**模板。</span><span class="sxs-lookup"><span data-stu-id="dd74d-166">Select the **Web** project type and the **ASP.NET MVC Web Application** template.</span></span> <span data-ttu-id="dd74d-167">为新项目命名*ContactManager* ，然后单击确定按钮。</span><span class="sxs-lookup"><span data-stu-id="dd74d-167">Name your new project *ContactManager* and click the OK button.</span></span>


<span data-ttu-id="dd74d-168">请确保你具有从顶部的下拉列表中选择的.NET Framework 3.5 角**新的项目**对话框。</span><span class="sxs-lookup"><span data-stu-id="dd74d-168">Make sure that you have .NET Framework 3.5 selected from the dropdown list at the top right of the **New Project** dialog.</span></span> <span data-ttu-id="dd74d-169">否则，不会出现的 ASP.NET MVC Web 应用程序模板。</span><span class="sxs-lookup"><span data-stu-id="dd74d-169">Otherwise, the ASP.NET MVC Web Application template won't appear.</span></span>


<span data-ttu-id="dd74d-170">[![新建项目对话框](iteration-1-create-the-application-vb/_static/image1.jpg)](iteration-1-create-the-application-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="dd74d-170">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image1.jpg)](iteration-1-create-the-application-vb/_static/image1.png)</span></span>

<span data-ttu-id="dd74d-171">**图 01**:新项目对话框 ([单击此项可查看原尺寸图像](iteration-1-create-the-application-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="dd74d-171">**Figure 01**: The New Project dialog([Click to view full-size image](iteration-1-create-the-application-vb/_static/image2.png))</span></span>


<span data-ttu-id="dd74d-172">ASP.NET MVC 应用程序**创建单元测试项目**此时将显示对话框。</span><span class="sxs-lookup"><span data-stu-id="dd74d-172">ASP.NET MVC application, the **Create Unit Test Project** dialog appears.</span></span> <span data-ttu-id="dd74d-173">可以使用此对话框以指示你想要创建并创建 ASP.NET MVC 应用程序时向你的解决方案添加单元测试项目。</span><span class="sxs-lookup"><span data-stu-id="dd74d-173">You can use this dialog to indicate that you want to create and add a unit test project to your solution when you create your ASP.NET MVC application.</span></span> <span data-ttu-id="dd74d-174">尽管我们不会生成此小版本中的单元测试，但应选择选项**可以，请创建单元测试项目**由于我们计划在后续迭代中添加单元测试。</span><span class="sxs-lookup"><span data-stu-id="dd74d-174">Although we won't be building unit tests in this iteration, you should select the option **Yes, create a unit test project** because we plan to add unit tests in a later iteration.</span></span> <span data-ttu-id="dd74d-175">首次创建新的 ASP.NET MVC 项目时添加的测试项目是比创建 ASP.NET MVC 项目后再添加一个测试项目容易得多。</span><span class="sxs-lookup"><span data-stu-id="dd74d-175">Adding a Test project when you first create a new ASP.NET MVC project is much easier than adding a Test project after the ASP.NET MVC project has been created.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="dd74d-176">Visual Web Developer 不支持测试项目，因为您无法获得创建单元测试项目对话框中，当使用 Visual Web Developer。</span><span class="sxs-lookup"><span data-stu-id="dd74d-176">Because Visual Web Developer does not support Test projects, you do not get the Create Unit Test Project dialog when using Visual Web Developer.</span></span>


<span data-ttu-id="dd74d-177">[![新建项目对话框](iteration-1-create-the-application-vb/_static/image2.jpg)](iteration-1-create-the-application-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="dd74d-177">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image2.jpg)](iteration-1-create-the-application-vb/_static/image3.png)</span></span>

<span data-ttu-id="dd74d-178">**图 02**:创建单元测试项目对话框 ([单击此项可查看原尺寸图像](iteration-1-create-the-application-vb/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="dd74d-178">**Figure 02**: The Create Unit Test Project dialog ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image4.png))</span></span>


<span data-ttu-id="dd74d-179">ASP.NET MVC 应用程序将显示在 Visual Studio 解决方案资源管理器窗口 （请参见图 3）。</span><span class="sxs-lookup"><span data-stu-id="dd74d-179">ASP.NET MVC application appears in the Visual Studio Solution Explorer window (see Figure 3).</span></span> <span data-ttu-id="dd74d-180">如果 don t 看到解决方案资源管理器窗口，然后通过选择菜单选项可打开此窗口**视图、 解决方案资源管理器**。</span><span class="sxs-lookup"><span data-stu-id="dd74d-180">If you don t see the Solution Explorer window then you can open this window by selecting the menu option **View, Solution Explorer**.</span></span> <span data-ttu-id="dd74d-181">请注意，该解决方案包含两个项目： 在 ASP.NET MVC 项目和测试项目。</span><span class="sxs-lookup"><span data-stu-id="dd74d-181">Notice that the solution contains two projects: the ASP.NET MVC project and the Test project.</span></span> <span data-ttu-id="dd74d-182">ASP.NET MVC 项目命名为 ContactManager 和测试项目命名为 ContactManager.Tests。</span><span class="sxs-lookup"><span data-stu-id="dd74d-182">The ASP.NET MVC project is named ContactManager and the Test project is named ContactManager.Tests.</span></span>


<span data-ttu-id="dd74d-183">[![新建项目对话框](iteration-1-create-the-application-vb/_static/image3.jpg)](iteration-1-create-the-application-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="dd74d-183">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image3.jpg)](iteration-1-create-the-application-vb/_static/image5.png)</span></span>

<span data-ttu-id="dd74d-184">**图 03**:解决方案资源管理器窗口 ([单击此项可查看原尺寸图像](iteration-1-create-the-application-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="dd74d-184">**Figure 03**: The Solution Explorer window ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image6.png))</span></span>


## <a name="deleting-the-project-sample-files"></a><span data-ttu-id="dd74d-185">删除项目示例文件</span><span class="sxs-lookup"><span data-stu-id="dd74d-185">Deleting the Project Sample Files</span></span>

<span data-ttu-id="dd74d-186">ASP.NET MVC 项目模板包括用于控制器和视图的示例文件。</span><span class="sxs-lookup"><span data-stu-id="dd74d-186">The ASP.NET MVC project template includes sample files for controllers and views.</span></span> <span data-ttu-id="dd74d-187">在创建新的 ASP.NET MVC 应用程序之前, 应删除这些文件。</span><span class="sxs-lookup"><span data-stu-id="dd74d-187">Before creating a new ASP.NET MVC application, you should delete these files.</span></span> <span data-ttu-id="dd74d-188">您可以删除文件和文件夹在解决方案资源管理器窗口中的右键单击文件或文件夹并选择菜单选项**删除**。</span><span class="sxs-lookup"><span data-stu-id="dd74d-188">You can delete files and folders in the Solution Explorer window by right-clicking a file or folder and selecting the menu option **Delete**.</span></span>

<span data-ttu-id="dd74d-189">需要从 ASP.NET MVC 项目中删除以下文件：</span><span class="sxs-lookup"><span data-stu-id="dd74d-189">You need to delete the following files from the ASP.NET MVC project:</span></span>

- <span data-ttu-id="dd74d-190">\Controllers\HomeController.vb</span><span class="sxs-lookup"><span data-stu-id="dd74d-190">\Controllers\HomeController.vb</span></span>

- <span data-ttu-id="dd74d-191">\Views\Home\About.aspx</span><span class="sxs-lookup"><span data-stu-id="dd74d-191">\Views\Home\About.aspx</span></span>

- <span data-ttu-id="dd74d-192">\Views\Home\Index.aspx</span><span class="sxs-lookup"><span data-stu-id="dd74d-192">\Views\Home\Index.aspx</span></span>

<span data-ttu-id="dd74d-193">并且，需要从测试项目中删除以下文件：</span><span class="sxs-lookup"><span data-stu-id="dd74d-193">And, you need to delete the following file from the Test project:</span></span>

<span data-ttu-id="dd74d-194">\Controllers\HomeControllerTest.vb</span><span class="sxs-lookup"><span data-stu-id="dd74d-194">\Controllers\HomeControllerTest.vb</span></span>

## <a name="creating-the-database"></a><span data-ttu-id="dd74d-195">创建数据库</span><span class="sxs-lookup"><span data-stu-id="dd74d-195">Creating the Database</span></span>

<span data-ttu-id="dd74d-196">联系人管理器应用程序是一个数据库驱动的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="dd74d-196">The Contact Manager application is a database-driven web application.</span></span> <span data-ttu-id="dd74d-197">我们使用数据库来存储联系人信息。</span><span class="sxs-lookup"><span data-stu-id="dd74d-197">We use a database to store the contact information.</span></span>

<span data-ttu-id="dd74d-198">使用包括 Microsoft SQL Server、 Oracle、 MySQL 和 IBM DB2 数据库的任何现代数据库在 ASP.NET MVC framework。</span><span class="sxs-lookup"><span data-stu-id="dd74d-198">The ASP.NET MVC framework with any modern database including Microsoft SQL Server, Oracle, MySQL, and IBM DB2 databases.</span></span> <span data-ttu-id="dd74d-199">在本教程中，我们使用 Microsoft SQL Server 数据库。</span><span class="sxs-lookup"><span data-stu-id="dd74d-199">In this tutorial, we use a Microsoft SQL Server database.</span></span> <span data-ttu-id="dd74d-200">在安装 Visual Studio，则会安装 Microsoft SQL Server Express 是免费版本的 Microsoft SQL Server 数据库的选项。</span><span class="sxs-lookup"><span data-stu-id="dd74d-200">When you install Visual Studio, you are provided with the option of installing Microsoft SQL Server Express which is a free version of the Microsoft SQL Server database.</span></span>

<span data-ttu-id="dd74d-201">通过右键单击该应用程序创建新的数据库\_在解决方案资源管理器窗口并选择菜单选项中的数据文件夹**添加、 新项**。</span><span class="sxs-lookup"><span data-stu-id="dd74d-201">Create a new database by right-clicking the App\_Data folder in the Solution Explorer window and selecting the menu option **Add, New Item**.</span></span> <span data-ttu-id="dd74d-202">在中**添加新项**对话框中，选择**数据**类别并**SQL Server 数据库**模板 （请参阅图 4）。</span><span class="sxs-lookup"><span data-stu-id="dd74d-202">In the **Add New Item** dialog, select the **Data** category and the **SQL Server Database** template (see Figure 4).</span></span> <span data-ttu-id="dd74d-203">命名新数据库 ContactManagerDB.mdf，然后单击确定按钮。</span><span class="sxs-lookup"><span data-stu-id="dd74d-203">Name the new database ContactManagerDB.mdf and click the OK button.</span></span>


<span data-ttu-id="dd74d-204">[![新建项目对话框](iteration-1-create-the-application-vb/_static/image4.jpg)](iteration-1-create-the-application-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="dd74d-204">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image4.jpg)](iteration-1-create-the-application-vb/_static/image7.png)</span></span>

<span data-ttu-id="dd74d-205">**图 04**:创建新的 Microsoft SQL Server Express 数据库 ([单击此项可查看原尺寸图像](iteration-1-create-the-application-vb/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="dd74d-205">**Figure 04**: Creating a new Microsoft SQL Server Express database ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image8.png))</span></span>


<span data-ttu-id="dd74d-206">创建新的数据库后，数据库会显示在应用中\_在解决方案资源管理器窗口中的数据文件夹。</span><span class="sxs-lookup"><span data-stu-id="dd74d-206">After you create the new database, the database appears in the App\_Data folder in the Solution Explorer window.</span></span> <span data-ttu-id="dd74d-207">双击 ContactManager.mdf 文件以打开服务器资源管理器窗口并连接到数据库。</span><span class="sxs-lookup"><span data-stu-id="dd74d-207">Double-click the ContactManager.mdf file to open the Server Explorer window and connect to the database.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="dd74d-208">服务器资源管理器窗口调用在 Microsoft Visual Web Developer 的情况下的数据库资源管理器窗口。</span><span class="sxs-lookup"><span data-stu-id="dd74d-208">The Server Explorer window is called the Database Explorer window in the case of Microsoft Visual Web Developer.</span></span>


<span data-ttu-id="dd74d-209">服务器资源管理器窗口可用于创建新的数据库对象，如数据库表、 视图、 触发器和存储的过程。</span><span class="sxs-lookup"><span data-stu-id="dd74d-209">You can use the Server Explorer window to create new database objects such as database tables, views, triggers, and stored procedures.</span></span> <span data-ttu-id="dd74d-210">右键单击表文件夹，然后选择菜单选项**添加新表**。</span><span class="sxs-lookup"><span data-stu-id="dd74d-210">Right-click the Tables folder and select the menu option **Add New Table**.</span></span> <span data-ttu-id="dd74d-211">数据库表设计器将显示 （请参见图 5）。</span><span class="sxs-lookup"><span data-stu-id="dd74d-211">The Database Table Designer appears (see Figure 5).</span></span>


<span data-ttu-id="dd74d-212">[![新建项目对话框](iteration-1-create-the-application-vb/_static/image5.jpg)](iteration-1-create-the-application-vb/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="dd74d-212">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image5.jpg)](iteration-1-create-the-application-vb/_static/image9.png)</span></span>

<span data-ttu-id="dd74d-213">**图 05**:数据库表设计器 ([单击此项可查看原尺寸图像](iteration-1-create-the-application-vb/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="dd74d-213">**Figure 05**: The Database Table Designer ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image10.png))</span></span>


<span data-ttu-id="dd74d-214">我们需要创建一个表格，包含以下列：</span><span class="sxs-lookup"><span data-stu-id="dd74d-214">We need to create a table that contains the following columns:</span></span>

<a id="0.2_table01"></a>


| <span data-ttu-id="dd74d-215">**列名称**</span><span class="sxs-lookup"><span data-stu-id="dd74d-215">**Column Name**</span></span> | <span data-ttu-id="dd74d-216">**数据类型**</span><span class="sxs-lookup"><span data-stu-id="dd74d-216">**Data Type**</span></span> | <span data-ttu-id="dd74d-217">**允许 null 值**</span><span class="sxs-lookup"><span data-stu-id="dd74d-217">**Allow Nulls**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="dd74d-218">Id</span><span class="sxs-lookup"><span data-stu-id="dd74d-218">Id</span></span> | <span data-ttu-id="dd74d-219">int</span><span class="sxs-lookup"><span data-stu-id="dd74d-219">int</span></span> | <span data-ttu-id="dd74d-220">False</span><span class="sxs-lookup"><span data-stu-id="dd74d-220">false</span></span> |
| <span data-ttu-id="dd74d-221">FirstName</span><span class="sxs-lookup"><span data-stu-id="dd74d-221">FirstName</span></span> | <span data-ttu-id="dd74d-222">nvarchar(50)</span><span class="sxs-lookup"><span data-stu-id="dd74d-222">nvarchar(50)</span></span> | <span data-ttu-id="dd74d-223">False</span><span class="sxs-lookup"><span data-stu-id="dd74d-223">false</span></span> |
| <span data-ttu-id="dd74d-224">LastName</span><span class="sxs-lookup"><span data-stu-id="dd74d-224">LastName</span></span> | <span data-ttu-id="dd74d-225">nvarchar(50)</span><span class="sxs-lookup"><span data-stu-id="dd74d-225">nvarchar(50)</span></span> | <span data-ttu-id="dd74d-226">False</span><span class="sxs-lookup"><span data-stu-id="dd74d-226">false</span></span> |
| <span data-ttu-id="dd74d-227">电话</span><span class="sxs-lookup"><span data-stu-id="dd74d-227">Phone</span></span> | <span data-ttu-id="dd74d-228">nvarchar(50)</span><span class="sxs-lookup"><span data-stu-id="dd74d-228">nvarchar(50)</span></span> | <span data-ttu-id="dd74d-229">False</span><span class="sxs-lookup"><span data-stu-id="dd74d-229">false</span></span> |
| <span data-ttu-id="dd74d-230">电子邮件</span><span class="sxs-lookup"><span data-stu-id="dd74d-230">Email</span></span> | <span data-ttu-id="dd74d-231">nvarchar(255)</span><span class="sxs-lookup"><span data-stu-id="dd74d-231">nvarchar(255)</span></span> | <span data-ttu-id="dd74d-232">False</span><span class="sxs-lookup"><span data-stu-id="dd74d-232">false</span></span> |


<span data-ttu-id="dd74d-233">第一列，Id 列中，比较特殊。</span><span class="sxs-lookup"><span data-stu-id="dd74d-233">The first column, the Id column, is special.</span></span> <span data-ttu-id="dd74d-234">您需要将 Id 列标记为标识列和主键列。</span><span class="sxs-lookup"><span data-stu-id="dd74d-234">You need to mark the Id column as an Identity column and a Primary Key column.</span></span> <span data-ttu-id="dd74d-235">您指示某一列为标识列展开列属性 （请查看底部的图 6），然后滚动到标识规范属性。</span><span class="sxs-lookup"><span data-stu-id="dd74d-235">You indicate that a column is an Identity column by expanding Column Properties (look at the bottom of Figure 6) and scrolling down to the Identity Specification property.</span></span> <span data-ttu-id="dd74d-236">设置 **（是标识）** 属性设置为值**是**。</span><span class="sxs-lookup"><span data-stu-id="dd74d-236">Set the **(Is Identity)** property to the value **Yes**.</span></span>

<span data-ttu-id="dd74d-237">通过选择列并单击带有密钥的图标的按钮可将列标记为 Primary Key 列中。</span><span class="sxs-lookup"><span data-stu-id="dd74d-237">You mark a column as a Primary Key column by selecting the column and clicking the button with the icon of a key.</span></span> <span data-ttu-id="dd74d-238">某列标记为 Primary Key 列后，列的旁边会显示密钥的一个图标 （请参阅图 6）。</span><span class="sxs-lookup"><span data-stu-id="dd74d-238">After a column is marked as a Primary Key column, an icon of a key appears next to the column (see Figure 6).</span></span>

<span data-ttu-id="dd74d-239">完成创建表后，单击保存按钮 （带有软盘图标的按钮） 以保存新表。</span><span class="sxs-lookup"><span data-stu-id="dd74d-239">After you finish creating the table, click the Save button (the button with an icon of a floppy) to save the new table.</span></span> <span data-ttu-id="dd74d-240">将新表命名*联系人*。</span><span class="sxs-lookup"><span data-stu-id="dd74d-240">Give your new table the name *Contacts*.</span></span>

<span data-ttu-id="dd74d-241">之后创建的联系人数据库表的完成，应将某些记录添加到表中。</span><span class="sxs-lookup"><span data-stu-id="dd74d-241">After finish creating the Contacts database table, you should add some records to the table.</span></span> <span data-ttu-id="dd74d-242">右键单击服务器资源管理器窗口中的联系人表，然后选择菜单选项**显示表数据**。</span><span class="sxs-lookup"><span data-stu-id="dd74d-242">Right-click the Contacts table in the Server Explorer window and select the menu option **Show Table Data**.</span></span> <span data-ttu-id="dd74d-243">将显示为网格中输入一个或多个联系人。</span><span class="sxs-lookup"><span data-stu-id="dd74d-243">Enter one or more contacts in the grid that appears.</span></span>

## <a name="creating-the-data-model"></a><span data-ttu-id="dd74d-244">创建数据模型</span><span class="sxs-lookup"><span data-stu-id="dd74d-244">Creating the Data Model</span></span>

<span data-ttu-id="dd74d-245">ASP.NET MVC 应用程序包含的模型、 视图和控制器。</span><span class="sxs-lookup"><span data-stu-id="dd74d-245">The ASP.NET MVC application consists of Models, Views, and Controllers.</span></span> <span data-ttu-id="dd74d-246">我们首先创建一个表示联系人表，我们在上一节中创建的模型类。</span><span class="sxs-lookup"><span data-stu-id="dd74d-246">We start by creating a Model class that represents the Contacts table that we created in the previous section.</span></span>

<span data-ttu-id="dd74d-247">在本教程中，我们可以使用 Microsoft Entity Framework 自动从数据库生成模型类。</span><span class="sxs-lookup"><span data-stu-id="dd74d-247">In this tutorial, we use the Microsoft Entity Framework to generate a model class from the database automatically.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="dd74d-248">ASP.NET MVC 框架不依赖于 Microsoft Entity Framework 以任何方式。</span><span class="sxs-lookup"><span data-stu-id="dd74d-248">The ASP.NET MVC framework is not tied to the Microsoft Entity Framework in any way.</span></span> <span data-ttu-id="dd74d-249">可以使用备用数据库访问技术，包括 NHibernate、 LINQ to SQL 或 ADO.NET 使用 ASP.NET MVC。</span><span class="sxs-lookup"><span data-stu-id="dd74d-249">You can use ASP.NET MVC with alternative database access technologies including NHibernate, LINQ to SQL, or ADO.NET.</span></span>


<span data-ttu-id="dd74d-250">请执行以下步骤来创建数据模型类：</span><span class="sxs-lookup"><span data-stu-id="dd74d-250">Follow these steps to create the data model classes:</span></span>

1. <span data-ttu-id="dd74d-251">右键单击解决方案资源管理器窗口中的 Models 文件夹，然后选择**添加、 新项**。</span><span class="sxs-lookup"><span data-stu-id="dd74d-251">Right-click the Models folder in the Solution Explorer window and select **Add, New Item**.</span></span> <span data-ttu-id="dd74d-252">**添加新项**对话框 （请参见图 6）。</span><span class="sxs-lookup"><span data-stu-id="dd74d-252">The **Add New Item** dialog appears (see Figure 6).</span></span>
2. <span data-ttu-id="dd74d-253">选择**数据**类别和**ADO.NET 实体数据模型**模板。</span><span class="sxs-lookup"><span data-stu-id="dd74d-253">Select the **Data** category and the **ADO.NET Entity Data Model** template.</span></span> <span data-ttu-id="dd74d-254">命名你的数据模型*ContactManagerModel.edmx*然后单击**添加**按钮。</span><span class="sxs-lookup"><span data-stu-id="dd74d-254">Name your data model *ContactManagerModel.edmx* and click the **Add** button.</span></span> <span data-ttu-id="dd74d-255">实体数据模型向导将显示 （请参阅图 7）。</span><span class="sxs-lookup"><span data-stu-id="dd74d-255">The Entity Data Model wizard appears (see Figure 7).</span></span>
3. <span data-ttu-id="dd74d-256">在中**选择模型内容**步骤中，选择**从数据库生成**（请参阅图 7）。</span><span class="sxs-lookup"><span data-stu-id="dd74d-256">In the **Choose Model Contents** step, select **Generate from database** (see Figure 7).</span></span>
4. <span data-ttu-id="dd74d-257">在中**选择数据连接**步骤，选择 ContactManagerDB.mdf 数据库并输入名称*ContactManagerDBEntities* （请参阅图 8） 的实体连接设置。</span><span class="sxs-lookup"><span data-stu-id="dd74d-257">In the **Choose Your Data Connection** step, select the ContactManagerDB.mdf database and enter the name *ContactManagerDBEntities* for the Entity Connection Settings (see Figure 8).</span></span>
5. <span data-ttu-id="dd74d-258">在中**选择数据库对象**步骤中，选择标记为的表 （请参阅图 9） 复选框。</span><span class="sxs-lookup"><span data-stu-id="dd74d-258">In the **Choose Your Database Objects** step, select the checkbox labeled Tables (see Figure 9).</span></span> <span data-ttu-id="dd74d-259">数据模型将包括包含 （仅一个联系人表没有） 在数据库中的所有表。</span><span class="sxs-lookup"><span data-stu-id="dd74d-259">The data model will include all tables contained in your database (there is just one, the Contacts table).</span></span> <span data-ttu-id="dd74d-260">输入的命名空间*模型*。</span><span class="sxs-lookup"><span data-stu-id="dd74d-260">Enter the namespace *Models*.</span></span> <span data-ttu-id="dd74d-261">单击完成按钮以完成向导。</span><span class="sxs-lookup"><span data-stu-id="dd74d-261">Click the Finish button to complete the wizard.</span></span>


<span data-ttu-id="dd74d-262">[![新建项目对话框](iteration-1-create-the-application-vb/_static/image6.jpg)](iteration-1-create-the-application-vb/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="dd74d-262">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image6.jpg)](iteration-1-create-the-application-vb/_static/image11.png)</span></span>

<span data-ttu-id="dd74d-263">**图 06**:添加新项对话框 ([单击此项可查看原尺寸图像](iteration-1-create-the-application-vb/_static/image12.png))</span><span class="sxs-lookup"><span data-stu-id="dd74d-263">**Figure 06**: The Add New Item dialog ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image12.png))</span></span>


<span data-ttu-id="dd74d-264">[![新建项目对话框](iteration-1-create-the-application-vb/_static/image7.jpg)](iteration-1-create-the-application-vb/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="dd74d-264">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image7.jpg)](iteration-1-create-the-application-vb/_static/image13.png)</span></span>

<span data-ttu-id="dd74d-265">**图 07**:选择模型内容 ([单击此项可查看原尺寸图像](iteration-1-create-the-application-vb/_static/image14.png))</span><span class="sxs-lookup"><span data-stu-id="dd74d-265">**Figure 07**: Choose Model Contents ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image14.png))</span></span>


<span data-ttu-id="dd74d-266">[![新建项目对话框](iteration-1-create-the-application-vb/_static/image8.jpg)](iteration-1-create-the-application-vb/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="dd74d-266">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image8.jpg)](iteration-1-create-the-application-vb/_static/image15.png)</span></span>

<span data-ttu-id="dd74d-267">**图 08**:选择您的数据连接 ([单击此项可查看原尺寸图像](iteration-1-create-the-application-vb/_static/image16.png))</span><span class="sxs-lookup"><span data-stu-id="dd74d-267">**Figure 08**: Choose Your Data Connection ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image16.png))</span></span>


<span data-ttu-id="dd74d-268">[![新建项目对话框](iteration-1-create-the-application-vb/_static/image9.jpg)](iteration-1-create-the-application-vb/_static/image17.png)</span><span class="sxs-lookup"><span data-stu-id="dd74d-268">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image9.jpg)](iteration-1-create-the-application-vb/_static/image17.png)</span></span>

<span data-ttu-id="dd74d-269">**图 09**:选择数据库对象 ([单击此项可查看原尺寸图像](iteration-1-create-the-application-vb/_static/image18.png))</span><span class="sxs-lookup"><span data-stu-id="dd74d-269">**Figure 09**: Choose Your Database Objects ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image18.png))</span></span>


<span data-ttu-id="dd74d-270">完成实体数据模型向导后，将显示实体数据模型设计器。</span><span class="sxs-lookup"><span data-stu-id="dd74d-270">After you complete the Entity Data Model Wizard, the Entity Data Model Designer appears.</span></span> <span data-ttu-id="dd74d-271">在设计器为要建模的每个表显示相对应的类。</span><span class="sxs-lookup"><span data-stu-id="dd74d-271">The designer displays a class that corresponds to each table being modeled.</span></span> <span data-ttu-id="dd74d-272">应会看到一个名为联系人的类。</span><span class="sxs-lookup"><span data-stu-id="dd74d-272">You should see one class named Contacts.</span></span>

<span data-ttu-id="dd74d-273">实体数据模型向导将生成基于数据库表名称的类名称。</span><span class="sxs-lookup"><span data-stu-id="dd74d-273">The Entity Data Model wizard generates class names based on database table names.</span></span> <span data-ttu-id="dd74d-274">几乎总是需要更改由向导生成的类的名称。</span><span class="sxs-lookup"><span data-stu-id="dd74d-274">You almost always need to change the name of the class generated by the wizard.</span></span> <span data-ttu-id="dd74d-275">右键单击设计器中的联系人类，然后选择菜单选项**重命名**。</span><span class="sxs-lookup"><span data-stu-id="dd74d-275">Right-click the Contacts class in the designer and select the menu option **Rename**.</span></span> <span data-ttu-id="dd74d-276">将类的名称从联系人 （复数） 更改为联系人 （单数形式）。</span><span class="sxs-lookup"><span data-stu-id="dd74d-276">Change the name of the class from Contacts (plural) to Contact (singular).</span></span> <span data-ttu-id="dd74d-277">更改类名称后，此类应类似于图 10。</span><span class="sxs-lookup"><span data-stu-id="dd74d-277">After you change the class name, the class should appear like Figure 10.</span></span>


<span data-ttu-id="dd74d-278">[![新建项目对话框](iteration-1-create-the-application-vb/_static/image10.jpg)](iteration-1-create-the-application-vb/_static/image19.png)</span><span class="sxs-lookup"><span data-stu-id="dd74d-278">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image10.jpg)](iteration-1-create-the-application-vb/_static/image19.png)</span></span>

<span data-ttu-id="dd74d-279">**图 10**:Contact 类 ([单击此项可查看原尺寸图像](iteration-1-create-the-application-vb/_static/image20.png))</span><span class="sxs-lookup"><span data-stu-id="dd74d-279">**Figure 10**: The Contact class ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image20.png))</span></span>


<span data-ttu-id="dd74d-280">此时，我们创建了我们的数据库模型。</span><span class="sxs-lookup"><span data-stu-id="dd74d-280">At this point, we have created our database model.</span></span> <span data-ttu-id="dd74d-281">我们可以使用联系人类来表示数据库中的特定联系人记录。</span><span class="sxs-lookup"><span data-stu-id="dd74d-281">We can use the Contact class to represent a particular contact record in our database.</span></span>

## <a name="creating-the-home-controller"></a><span data-ttu-id="dd74d-282">创建主控制器</span><span class="sxs-lookup"><span data-stu-id="dd74d-282">Creating the Home Controller</span></span>

<span data-ttu-id="dd74d-283">下一步是创建我们的主控制器。</span><span class="sxs-lookup"><span data-stu-id="dd74d-283">The next step is to create our Home controller.</span></span> <span data-ttu-id="dd74d-284">主控制器是 ASP.NET MVC 应用程序中调用的默认控制器。</span><span class="sxs-lookup"><span data-stu-id="dd74d-284">The Home controller is the default controller invoked in an ASP.NET MVC application.</span></span>

<span data-ttu-id="dd74d-285">通过右键单击解决方案资源管理器窗口中的 Controllers 文件夹并选择菜单选项创建主页控制器类**添加、 控制器**（请参阅图 11）。</span><span class="sxs-lookup"><span data-stu-id="dd74d-285">Create the Home controller class by right-clicking the Controllers folder in the Solution Explorer window and selecting the menu option **Add, Controller** (see Figure 11).</span></span> <span data-ttu-id="dd74d-286">请注意，标记为复选框**添加用于创建、 更新和的详细信息方案的操作方法**。</span><span class="sxs-lookup"><span data-stu-id="dd74d-286">Notice the checkbox labeled **Add action methods for Create, Update, and Details scenarios**.</span></span> <span data-ttu-id="dd74d-287">请确保单击前确认已选中此复选框**添加**按钮。</span><span class="sxs-lookup"><span data-stu-id="dd74d-287">Make sure that this checkbox is checked before clicking the **Add** button.</span></span>


<span data-ttu-id="dd74d-288">[![新建项目对话框](iteration-1-create-the-application-vb/_static/image11.jpg)](iteration-1-create-the-application-vb/_static/image21.png)</span><span class="sxs-lookup"><span data-stu-id="dd74d-288">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image11.jpg)](iteration-1-create-the-application-vb/_static/image21.png)</span></span>

<span data-ttu-id="dd74d-289">**图 11**:添加主控制器 ([单击此项可查看原尺寸图像](iteration-1-create-the-application-vb/_static/image22.png))</span><span class="sxs-lookup"><span data-stu-id="dd74d-289">**Figure 11**: Adding the Home controller ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image22.png))</span></span>


<span data-ttu-id="dd74d-290">创建主控制器时，您在列表 1 中获取类。</span><span class="sxs-lookup"><span data-stu-id="dd74d-290">When you create the Home controller, you get the class in Listing 1.</span></span>

<span data-ttu-id="dd74d-291">**Listing 1 - Controllers\HomeController.vb**</span><span class="sxs-lookup"><span data-stu-id="dd74d-291">**Listing 1 - Controllers\HomeController.vb**</span></span>

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample1.vb)]

## <a name="listing-the-contacts"></a><span data-ttu-id="dd74d-292">列出联系人</span><span class="sxs-lookup"><span data-stu-id="dd74d-292">Listing the Contacts</span></span>

<span data-ttu-id="dd74d-293">若要显示的联系人数据库表中的记录，我们需要创建 index （） 操作和索引视图。</span><span class="sxs-lookup"><span data-stu-id="dd74d-293">In order to display the records in the Contacts database table, we need to create an Index() action and an Index view.</span></span>

<span data-ttu-id="dd74d-294">主控制器已包含 index （） 操作。</span><span class="sxs-lookup"><span data-stu-id="dd74d-294">The Home controller already contains an Index() action.</span></span> <span data-ttu-id="dd74d-295">我们需要修改此方法，使它看起来像列表 2。</span><span class="sxs-lookup"><span data-stu-id="dd74d-295">We need to modify this method so that it looks like Listing 2.</span></span>

<span data-ttu-id="dd74d-296">**Listing 2 - Controllers\HomeController.vb**</span><span class="sxs-lookup"><span data-stu-id="dd74d-296">**Listing 2 - Controllers\HomeController.vb**</span></span>

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample2.vb)]

<span data-ttu-id="dd74d-297">请注意，代码清单 2 中的主页控制器类包含一个名为的私有字段\_实体。</span><span class="sxs-lookup"><span data-stu-id="dd74d-297">Notice that the Home controller class in Listing 2 contains a private field named \_entities.</span></span> <span data-ttu-id="dd74d-298">\_实体字段表示的实体数据模型中。</span><span class="sxs-lookup"><span data-stu-id="dd74d-298">The \_entities field represents the entities from the data model.</span></span> <span data-ttu-id="dd74d-299">我们使用\_实体字段以与数据库通信。</span><span class="sxs-lookup"><span data-stu-id="dd74d-299">We use the \_entities field to communicate with the database.</span></span>

<span data-ttu-id="dd74d-300">Index （） 方法返回表示所有联系人联系人数据库表中的视图。</span><span class="sxs-lookup"><span data-stu-id="dd74d-300">The Index() method returns a view that represents all of the contacts from the Contacts database table.</span></span> <span data-ttu-id="dd74d-301">表达式\_实体。ContactSet.ToList() 泛型列表的形式返回联系人的列表。</span><span class="sxs-lookup"><span data-stu-id="dd74d-301">The expression \_entities.ContactSet.ToList() returns the list of contacts as a generic list.</span></span>

<span data-ttu-id="dd74d-302">现在，我们制作了索引控制器中，我们接下来需要创建索引视图。</span><span class="sxs-lookup"><span data-stu-id="dd74d-302">Now that we ve created the Index controller, we next need to create the Index view.</span></span> <span data-ttu-id="dd74d-303">在创建索引视图之前, 编译应用程序通过选择菜单选项**生成，生成解决方案**。</span><span class="sxs-lookup"><span data-stu-id="dd74d-303">Before creating the Index view, compile your application by selecting the menu option **Build, Build Solution**.</span></span> <span data-ttu-id="dd74d-304">始终应添加一个视图，以便模型类的列表中显示之前编译你的项目**添加视图**对话框。</span><span class="sxs-lookup"><span data-stu-id="dd74d-304">You should always compile your project before adding a view in order for the list of model classes to be displayed in the **Add View** dialog.</span></span>

<span data-ttu-id="dd74d-305">右键单击 index （） 方法并选择菜单选项创建索引视图**添加视图**（请参阅图 12）。</span><span class="sxs-lookup"><span data-stu-id="dd74d-305">You create the Index view by right-clicking the Index() method and selecting the menu option **Add View** (see Figure 12).</span></span> <span data-ttu-id="dd74d-306">选择此菜单选项将打开**添加视图**对话框 （请参阅图 13）。</span><span class="sxs-lookup"><span data-stu-id="dd74d-306">Selecting this menu option opens the **Add View** dialog (see Figure 13).</span></span>


<span data-ttu-id="dd74d-307">[![新建项目对话框](iteration-1-create-the-application-vb/_static/image12.jpg)](iteration-1-create-the-application-vb/_static/image23.png)</span><span class="sxs-lookup"><span data-stu-id="dd74d-307">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image12.jpg)](iteration-1-create-the-application-vb/_static/image23.png)</span></span>

<span data-ttu-id="dd74d-308">**图 12**:添加索引视图 ([单击此项可查看原尺寸图像](iteration-1-create-the-application-vb/_static/image24.png))</span><span class="sxs-lookup"><span data-stu-id="dd74d-308">**Figure 12**: Adding the Index view ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image24.png))</span></span>


<span data-ttu-id="dd74d-309">在中**添加视图**对话框中，选中复选框标记为**创建强类型化视图**。</span><span class="sxs-lookup"><span data-stu-id="dd74d-309">In the **Add View** dialog, check the checkbox labeled **Create a strongly-typed view**.</span></span> <span data-ttu-id="dd74d-310">选择视图数据类 ContactManager.Contact 和查看内容列表。</span><span class="sxs-lookup"><span data-stu-id="dd74d-310">Select the View data class ContactManager.Contact and the View content List.</span></span> <span data-ttu-id="dd74d-311">选择以下选项将生成一个视图，显示联系人记录的列表。</span><span class="sxs-lookup"><span data-stu-id="dd74d-311">Selecting these options generates a view that displays a list of Contact records.</span></span>


<span data-ttu-id="dd74d-312">[![新建项目对话框](iteration-1-create-the-application-vb/_static/image13.jpg)](iteration-1-create-the-application-vb/_static/image25.png)</span><span class="sxs-lookup"><span data-stu-id="dd74d-312">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image13.jpg)](iteration-1-create-the-application-vb/_static/image25.png)</span></span>

<span data-ttu-id="dd74d-313">**图 13**:添加视图对话框中 ([单击此项可查看原尺寸图像](iteration-1-create-the-application-vb/_static/image26.png))</span><span class="sxs-lookup"><span data-stu-id="dd74d-313">**Figure 13**: The Add View dialog ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image26.png))</span></span>


<span data-ttu-id="dd74d-314">当您单击**添加**生成按钮，清单 3 中的索引视图。</span><span class="sxs-lookup"><span data-stu-id="dd74d-314">When you click the **Add** button, the Index view in Listing 3 is generated.</span></span> <span data-ttu-id="dd74d-315">请注意&lt;%@ 页 %&gt;文件的顶部显示的指令。</span><span class="sxs-lookup"><span data-stu-id="dd74d-315">Notice the &lt;%@ Page %&gt; directive that appears at the top of the file.</span></span> <span data-ttu-id="dd74d-316">索引视图继承自 ViewPage&lt;IEnumerable&lt;ContactManager.Models.Contact&gt; &gt;类。</span><span class="sxs-lookup"><span data-stu-id="dd74d-316">The Index view inherits from the ViewPage&lt;IEnumerable&lt;ContactManager.Models.Contact&gt;&gt; class.</span></span> <span data-ttu-id="dd74d-317">换而言之，在视图模型类表示联系人实体的列表。</span><span class="sxs-lookup"><span data-stu-id="dd74d-317">In other words, the Model class in the view represents a list of Contact entities.</span></span>

<span data-ttu-id="dd74d-318">索引视图，正文将包含 foreach 循环循环访问每个 Model 类所表示的联系人。</span><span class="sxs-lookup"><span data-stu-id="dd74d-318">The body of the Index view contains a foreach loop that iterates through each of the contacts represented by the Model class.</span></span> <span data-ttu-id="dd74d-319">Contact 类的每个属性的值显示在 HTML 表。</span><span class="sxs-lookup"><span data-stu-id="dd74d-319">The value of each property of the Contact class is displayed within an HTML table.</span></span>

<span data-ttu-id="dd74d-320">**代码清单 3-Views\Home\Index.aspx （未修改）**</span><span class="sxs-lookup"><span data-stu-id="dd74d-320">**Listing 3 - Views\Home\Index.aspx (unmodified)**</span></span>

[!code-aspx[Main](iteration-1-create-the-application-vb/samples/sample3.aspx)]

<span data-ttu-id="dd74d-321">我们需要使索引视图到一处修改。</span><span class="sxs-lookup"><span data-stu-id="dd74d-321">We need to make one modification to the Index view.</span></span> <span data-ttu-id="dd74d-322">因为我们不创建详细信息视图，我们可以删除的详细信息链接。</span><span class="sxs-lookup"><span data-stu-id="dd74d-322">Because we are not creating a Details view, we can remove the Details link.</span></span> <span data-ttu-id="dd74d-323">找到并从索引视图中删除以下代码：</span><span class="sxs-lookup"><span data-stu-id="dd74d-323">Find and remove the following code from the Index view:</span></span>

<span data-ttu-id="dd74d-324">{.id = 项。Id}) %&gt;</span><span class="sxs-lookup"><span data-stu-id="dd74d-324">{.id = item.Id})%&gt;</span></span>

<span data-ttu-id="dd74d-325">修改索引视图后，可以运行联系人管理器应用程序。</span><span class="sxs-lookup"><span data-stu-id="dd74d-325">After you modify the Index view, you can run the Contact Manager application.</span></span> <span data-ttu-id="dd74d-326">选择启动调试菜单选项调试，或只需按 F5。</span><span class="sxs-lookup"><span data-stu-id="dd74d-326">Select the menu option Debug, Start Debugging or simply press F5.</span></span> <span data-ttu-id="dd74d-327">首次运行该应用程序，您会得到对话框图 14 中。</span><span class="sxs-lookup"><span data-stu-id="dd74d-327">The first time you run the application, you get the dialog in Figure 14.</span></span> <span data-ttu-id="dd74d-328">选择的选项**修改 Web.config 文件以启用调试**，然后单击确定按钮。</span><span class="sxs-lookup"><span data-stu-id="dd74d-328">Select the option **Modify the Web.config file to enable debugging** and click the OK button.</span></span>


<span data-ttu-id="dd74d-329">[![新建项目对话框](iteration-1-create-the-application-vb/_static/image14.jpg)](iteration-1-create-the-application-vb/_static/image27.png)</span><span class="sxs-lookup"><span data-stu-id="dd74d-329">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image14.jpg)](iteration-1-create-the-application-vb/_static/image27.png)</span></span>

<span data-ttu-id="dd74d-330">**图 14**:启用调试 ([单击此项可查看原尺寸图像](iteration-1-create-the-application-vb/_static/image28.png))</span><span class="sxs-lookup"><span data-stu-id="dd74d-330">**Figure 14**: Enabling debugging ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image28.png))</span></span>


<span data-ttu-id="dd74d-331">默认情况下返回索引视图。</span><span class="sxs-lookup"><span data-stu-id="dd74d-331">The Index view is returned by default.</span></span> <span data-ttu-id="dd74d-332">此视图将列出所有联系人数据库表中的数据 （请参阅图 15）。</span><span class="sxs-lookup"><span data-stu-id="dd74d-332">This view lists all of the data from the Contacts database table (see Figure 15).</span></span>


<span data-ttu-id="dd74d-333">[![新建项目对话框](iteration-1-create-the-application-vb/_static/image15.jpg)](iteration-1-create-the-application-vb/_static/image29.png)</span><span class="sxs-lookup"><span data-stu-id="dd74d-333">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image15.jpg)](iteration-1-create-the-application-vb/_static/image29.png)</span></span>

<span data-ttu-id="dd74d-334">**图 15**:索引视图 ([单击此项可查看原尺寸图像](iteration-1-create-the-application-vb/_static/image30.png))</span><span class="sxs-lookup"><span data-stu-id="dd74d-334">**Figure 15**: The Index view ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image30.png))</span></span>


<span data-ttu-id="dd74d-335">请注意，索引视图包含将标记为新创建的视图的底部的链接。</span><span class="sxs-lookup"><span data-stu-id="dd74d-335">Notice that the Index view includes a link labeled Create New at the bottom of the view.</span></span> <span data-ttu-id="dd74d-336">在下一步部分中，您将了解如何创建新的联系人。</span><span class="sxs-lookup"><span data-stu-id="dd74d-336">In the next section, you learn how to create new contacts.</span></span>

## <a name="creating-new-contacts"></a><span data-ttu-id="dd74d-337">创建新的联系人</span><span class="sxs-lookup"><span data-stu-id="dd74d-337">Creating New Contacts</span></span>

<span data-ttu-id="dd74d-338">若要使用户能够创建新的联系人，我们需要将两个 create （） 操作添加到 Home 控制器。</span><span class="sxs-lookup"><span data-stu-id="dd74d-338">To enable users to create new contacts, we need to add two Create() actions to the Home controller.</span></span> <span data-ttu-id="dd74d-339">我们需要创建一个返回 HTML 窗体创建一个新的联系人的 create （） 操作。</span><span class="sxs-lookup"><span data-stu-id="dd74d-339">We need to create one Create() action that returns an HTML form for creating a new contact.</span></span> <span data-ttu-id="dd74d-340">我们需要创建一个执行实际的数据库插入的新联系人的第二个 create （） 操作。</span><span class="sxs-lookup"><span data-stu-id="dd74d-340">We need to create a second Create() action that performs the actual database insert of the new contact.</span></span>

<span data-ttu-id="dd74d-341">列表 4 中包含我们需要将添加到 Home 控制器的新 create （） 方法。</span><span class="sxs-lookup"><span data-stu-id="dd74d-341">The new Create() methods that we need to add to the Home controller are contained in Listing 4.</span></span>

<span data-ttu-id="dd74d-342">**列表 4-Controllers\HomeController.vb （与创建的方法）**</span><span class="sxs-lookup"><span data-stu-id="dd74d-342">**Listing 4 - Controllers\HomeController.vb (with Create methods)**</span></span>

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample4.vb)]

<span data-ttu-id="dd74d-343">可以仅由 HTTP POST 调用的第二个 create （） 方法时，可以使用 HTTP GET 调用的第一个 create （） 方法。</span><span class="sxs-lookup"><span data-stu-id="dd74d-343">The first Create() method can be invoked with an HTTP GET while the second Create() method can be invoked only by an HTTP POST.</span></span> <span data-ttu-id="dd74d-344">换而言之，仅当发布 HTML 窗体时，可以调用第二个 create （） 方法。</span><span class="sxs-lookup"><span data-stu-id="dd74d-344">In other words, the second Create() method can be invoked only when posting an HTML form.</span></span> <span data-ttu-id="dd74d-345">第一个 create （） 方法只是返回一个包含用于创建新的联系人的 HTML 窗体视图。</span><span class="sxs-lookup"><span data-stu-id="dd74d-345">The first Create() method simply returns a view that contains the HTML form for creating a new contact.</span></span> <span data-ttu-id="dd74d-346">第二个 create （） 方法是更有意义： 它向数据库添加新联系人。</span><span class="sxs-lookup"><span data-stu-id="dd74d-346">The second Create() method is much more interesting: it adds the new contact to the database.</span></span>

<span data-ttu-id="dd74d-347">请注意，第二个 create （） 方法已被修改以接受 Contact 类的实例。</span><span class="sxs-lookup"><span data-stu-id="dd74d-347">Notice that the second Create() method has been modified to accept an instance of the Contact class.</span></span> <span data-ttu-id="dd74d-348">发布从 HTML 窗体的窗体值绑定到此 Contact 类的是 ASP.NET MVC 框架自动。</span><span class="sxs-lookup"><span data-stu-id="dd74d-348">The form values posted from the HTML form are bound to this Contact class by the ASP.NET MVC framework automatically.</span></span> <span data-ttu-id="dd74d-349">创建 HTML 窗体中的每个窗体字段分配给联系人参数的属性。</span><span class="sxs-lookup"><span data-stu-id="dd74d-349">Each form field from the HTML Create form is assigned to a property of the Contact parameter.</span></span>

<span data-ttu-id="dd74d-350">请注意，使用 [Bind] 属性修饰联系人参数。</span><span class="sxs-lookup"><span data-stu-id="dd74d-350">Notice that the Contact parameter is decorated with a [Bind] attribute.</span></span> <span data-ttu-id="dd74d-351">[Bind] 属性用于从绑定中排除的联系人 Id 属性。</span><span class="sxs-lookup"><span data-stu-id="dd74d-351">The [Bind] attribute is used to exclude the Contact Id property from binding.</span></span> <span data-ttu-id="dd74d-352">由于 Id 属性表示的标识属性，我们不想要设置的 Id 属性。</span><span class="sxs-lookup"><span data-stu-id="dd74d-352">Because the Id property represents an Identity property, we don t want to set the Id property.</span></span>

<span data-ttu-id="dd74d-353">在 create （） 方法的正文中，实体框架用于数据库中插入新的联系人。</span><span class="sxs-lookup"><span data-stu-id="dd74d-353">In the body of the Create() method, the Entity Framework is used to insert the new Contact into the database.</span></span> <span data-ttu-id="dd74d-354">新联系人添加到联系人的现有设置并调用 savechanges （） 方法来将这些更改推送回基础数据库。</span><span class="sxs-lookup"><span data-stu-id="dd74d-354">The new Contact is added to the existing set of Contacts and the SaveChanges() method is called to push these changes back to the underlying database.</span></span>

<span data-ttu-id="dd74d-355">您可以生成用于创建新的联系人，右键单击任意一种两个 create （） 方法并选择菜单选项的 HTML 窗体**添加视图**（请参阅图 16）。</span><span class="sxs-lookup"><span data-stu-id="dd74d-355">You can generate an HTML form for creating new Contacts by right-clicking either of the two Create() methods and selecting the menu option **Add View** (see Figure 16).</span></span>


<span data-ttu-id="dd74d-356">[![新建项目对话框](iteration-1-create-the-application-vb/_static/image16.jpg)](iteration-1-create-the-application-vb/_static/image31.png)</span><span class="sxs-lookup"><span data-stu-id="dd74d-356">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image16.jpg)](iteration-1-create-the-application-vb/_static/image31.png)</span></span>

<span data-ttu-id="dd74d-357">**图 16**:添加 Create 视图 ([单击此项可查看原尺寸图像](iteration-1-create-the-application-vb/_static/image32.png))</span><span class="sxs-lookup"><span data-stu-id="dd74d-357">**Figure 16**: Adding the Create view ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image32.png))</span></span>


<span data-ttu-id="dd74d-358">在中**添加视图**对话框中，选择**ContactManager.Contact**类并**创建**视图内容的选项 （请参阅图 17）。</span><span class="sxs-lookup"><span data-stu-id="dd74d-358">In the **Add View** dialog, select the **ContactManager.Contact** class and the **Create** option for view content (see Figure 17).</span></span> <span data-ttu-id="dd74d-359">当您单击**添加**按钮的创建自动生成视图。</span><span class="sxs-lookup"><span data-stu-id="dd74d-359">When you click the **Add** button, a Create view is generated automatically.</span></span>


<span data-ttu-id="dd74d-360">[![新建项目对话框](iteration-1-create-the-application-vb/_static/image17.jpg)](iteration-1-create-the-application-vb/_static/image33.png)</span><span class="sxs-lookup"><span data-stu-id="dd74d-360">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image17.jpg)](iteration-1-create-the-application-vb/_static/image33.png)</span></span>

<span data-ttu-id="dd74d-361">**图 17**:看到 explode 页面 ([单击此项可查看原尺寸图像](iteration-1-create-the-application-vb/_static/image34.png))</span><span class="sxs-lookup"><span data-stu-id="dd74d-361">**Figure 17**: Seeing a page explode ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image34.png))</span></span>


<span data-ttu-id="dd74d-362">创建视图包含的 Contact 类属性的每个窗体字段。</span><span class="sxs-lookup"><span data-stu-id="dd74d-362">The Create view contains form fields for each of the properties of the Contact class.</span></span> <span data-ttu-id="dd74d-363">列表 5 中包含创建视图的代码。</span><span class="sxs-lookup"><span data-stu-id="dd74d-363">The code for the Create view is included in Listing 5.</span></span>

<span data-ttu-id="dd74d-364">**Listing 5 - Views\Home\Create.aspx**</span><span class="sxs-lookup"><span data-stu-id="dd74d-364">**Listing 5 - Views\Home\Create.aspx**</span></span>

[!code-aspx[Main](iteration-1-create-the-application-vb/samples/sample5.aspx)]

<span data-ttu-id="dd74d-365">修改 create （） 方法并添加创建视图后，可以运行联系人管理器应用程序，并创建新的联系人。</span><span class="sxs-lookup"><span data-stu-id="dd74d-365">After you modify the Create() methods and add the Create view, you can run the Contact Manger application and create new contacts.</span></span> <span data-ttu-id="dd74d-366">单击**创建新**要导航到创建视图的索引视图中显示链接。</span><span class="sxs-lookup"><span data-stu-id="dd74d-366">Click the **Create New** link that appears in the Index view to navigate to the Create view.</span></span> <span data-ttu-id="dd74d-367">应会看到图 18 中的视图。</span><span class="sxs-lookup"><span data-stu-id="dd74d-367">You should see the view in Figure 18.</span></span>


<span data-ttu-id="dd74d-368">[![新建项目对话框](iteration-1-create-the-application-vb/_static/image18.jpg)](iteration-1-create-the-application-vb/_static/image35.png)</span><span class="sxs-lookup"><span data-stu-id="dd74d-368">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image18.jpg)](iteration-1-create-the-application-vb/_static/image35.png)</span></span>

<span data-ttu-id="dd74d-369">**图 18**:Create View ([单击此项可查看原尺寸图像](iteration-1-create-the-application-vb/_static/image36.png))</span><span class="sxs-lookup"><span data-stu-id="dd74d-369">**Figure 18**: The Create View ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image36.png))</span></span>


## <a name="editing-contacts"></a><span data-ttu-id="dd74d-370">编辑联系人</span><span class="sxs-lookup"><span data-stu-id="dd74d-370">Editing Contacts</span></span>

<span data-ttu-id="dd74d-371">添加编辑联系人记录的功能是非常类似于添加用于创建新联系人记录功能。</span><span class="sxs-lookup"><span data-stu-id="dd74d-371">Adding the functionality for editing a contact record is very similar to adding the functionality for creating new contact records.</span></span> <span data-ttu-id="dd74d-372">首先，我们需要将两个新的编辑方法添加到 Home 控制器类。</span><span class="sxs-lookup"><span data-stu-id="dd74d-372">First, we need to add two new Edit methods to the Home controller class.</span></span> <span data-ttu-id="dd74d-373">列表 6 中包含这些新的 edit （） 方法。</span><span class="sxs-lookup"><span data-stu-id="dd74d-373">These new Edit() methods are contained in Listing 6.</span></span>

<span data-ttu-id="dd74d-374">**代码清单 6-Controllers\HomeController.vb （与编辑方法）**</span><span class="sxs-lookup"><span data-stu-id="dd74d-374">**Listing 6 - Controllers\HomeController.vb (with Edit methods)**</span></span>

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample6.vb)]

<span data-ttu-id="dd74d-375">第一种 edit （） 方法调用的 HTTP GET 操作。</span><span class="sxs-lookup"><span data-stu-id="dd74d-375">The first Edit() method is invoked by an HTTP GET operation.</span></span> <span data-ttu-id="dd74d-376">Id 参数传递给此方法，它表示正在编辑的联系人记录 Id。</span><span class="sxs-lookup"><span data-stu-id="dd74d-376">An Id parameter is passed to this method which represents the Id of the contact record being edited.</span></span> <span data-ttu-id="dd74d-377">实体框架用于检索与 id 匹配的联系人返回一个包含 HTML 窗体以编辑记录视图。</span><span class="sxs-lookup"><span data-stu-id="dd74d-377">The Entity Framework is used to retrieve a contact that matches the Id. A view that contains an HTML form for editing a record is returned.</span></span>

<span data-ttu-id="dd74d-378">第二个 edit （） 方法来执行实际更新到数据库。</span><span class="sxs-lookup"><span data-stu-id="dd74d-378">The second Edit() method performs the actual update to the database.</span></span> <span data-ttu-id="dd74d-379">此方法作为参数接受 Contact 类的实例。</span><span class="sxs-lookup"><span data-stu-id="dd74d-379">This method accepts an instance of the Contact class as a parameter.</span></span> <span data-ttu-id="dd74d-380">ASP.NET MVC 框架将绑定窗体字段中编辑窗体到此类自动。</span><span class="sxs-lookup"><span data-stu-id="dd74d-380">The ASP.NET MVC framework binds the form fields from the Edit form to this class automatically.</span></span> <span data-ttu-id="dd74d-381">编辑的联系人 （我们需要 Id 属性的值） 时，请注意，您不 t 包括 [Bind] 属性。</span><span class="sxs-lookup"><span data-stu-id="dd74d-381">Notice that you don t include the[Bind] attribute when editing a Contact (we need the value of the Id property).</span></span>

<span data-ttu-id="dd74d-382">实体框架用于将已修改的联系人保存到数据库。</span><span class="sxs-lookup"><span data-stu-id="dd74d-382">The Entity Framework is used to save the modified Contact to the database.</span></span> <span data-ttu-id="dd74d-383">必须首先从数据库检索原始联系人。</span><span class="sxs-lookup"><span data-stu-id="dd74d-383">The original Contact must be retrieved from the database first.</span></span> <span data-ttu-id="dd74d-384">接下来，调用 Entity Framework ApplyPropertyChanges() 方法来记录对联系人的更改。</span><span class="sxs-lookup"><span data-stu-id="dd74d-384">Next, the Entity Framework ApplyPropertyChanges() method is called to record the changes to the Contact.</span></span> <span data-ttu-id="dd74d-385">最后，调用 Entity Framework savechanges （） 方法来保留对基础数据库的更改。</span><span class="sxs-lookup"><span data-stu-id="dd74d-385">Finally, the Entity Framework SaveChanges() method is called to persist the changes to the underlying database.</span></span>

<span data-ttu-id="dd74d-386">你可以生成包含右键单击 edit （） 方法并选择添加视图菜单选项编辑窗体的视图。</span><span class="sxs-lookup"><span data-stu-id="dd74d-386">You can generate the view that contains the Edit form by right-clicking the Edit() method and selecting the menu option Add View.</span></span> <span data-ttu-id="dd74d-387">在添加视图对话框中，选择**ContactManager.Models.Contact**类和**编辑**查看内容 （请参阅图 19）。</span><span class="sxs-lookup"><span data-stu-id="dd74d-387">In the Add View dialog, select the **ContactManager.Models.Contact** class and the **Edit** view content (see Figure 19).</span></span>


<span data-ttu-id="dd74d-388">[![新建项目对话框](iteration-1-create-the-application-vb/_static/image19.jpg)](iteration-1-create-the-application-vb/_static/image37.png)</span><span class="sxs-lookup"><span data-stu-id="dd74d-388">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image19.jpg)](iteration-1-create-the-application-vb/_static/image37.png)</span></span>

<span data-ttu-id="dd74d-389">**图 19**:添加一个编辑视图 ([单击此项可查看原尺寸图像](iteration-1-create-the-application-vb/_static/image38.png))</span><span class="sxs-lookup"><span data-stu-id="dd74d-389">**Figure 19**: Adding an Edit View ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image38.png))</span></span>


<span data-ttu-id="dd74d-390">当你单击添加按钮时，将自动生成新的编辑视图。</span><span class="sxs-lookup"><span data-stu-id="dd74d-390">When you click the Add button, a new Edit view is generated automatically.</span></span> <span data-ttu-id="dd74d-391">生成的 HTML 窗体包含对应于每个联系人类 （请参阅列表 7） 的属性的字段。</span><span class="sxs-lookup"><span data-stu-id="dd74d-391">The HTML form that is generated contains fields that correspond to each of the properties of the Contact class (see Listing 7).</span></span>

<span data-ttu-id="dd74d-392">**列表 7-Views\Home\Edit.aspx**</span><span class="sxs-lookup"><span data-stu-id="dd74d-392">**Listing 7 - Views\Home\Edit.aspx**</span></span>

[!code-aspx[Main](iteration-1-create-the-application-vb/samples/sample7.aspx)]

## <a name="deleting-contacts"></a><span data-ttu-id="dd74d-393">删除联系人</span><span class="sxs-lookup"><span data-stu-id="dd74d-393">Deleting Contacts</span></span>

<span data-ttu-id="dd74d-394">如果你想要删除的联系人，则需要将两个 delete （） 操作添加到 Home 控制器类。</span><span class="sxs-lookup"><span data-stu-id="dd74d-394">If you want to delete contacts then you need to add two Delete() actions to the Home controller class.</span></span> <span data-ttu-id="dd74d-395">第一个 delete （） 操作显示一个删除确认窗体。</span><span class="sxs-lookup"><span data-stu-id="dd74d-395">The first Delete() action displays a delete confirmation form.</span></span> <span data-ttu-id="dd74d-396">第二个 delete （） 操作执行实际删除。</span><span class="sxs-lookup"><span data-stu-id="dd74d-396">The second Delete() action performs the actual delete.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="dd74d-397">更高版本，在迭代 #7 中，我们修改联系人管理器，以便它支持 Ajax 删除一个步骤。</span><span class="sxs-lookup"><span data-stu-id="dd74d-397">Later, in Iteration #7, we modify the Contact Manager so that it supports a one step Ajax delete.</span></span>


<span data-ttu-id="dd74d-398">代码清单 8 中包含两个新 delete （） 方法。</span><span class="sxs-lookup"><span data-stu-id="dd74d-398">The two new Delete() methods are contained in Listing 8.</span></span>

<span data-ttu-id="dd74d-399">**代码清单 8-Controllers\HomeController.vb （删除方法）**</span><span class="sxs-lookup"><span data-stu-id="dd74d-399">**Listing 8 - Controllers\HomeController.vb (Delete methods)**</span></span>

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample8.vb)]

<span data-ttu-id="dd74d-400">第一个 delete （） 方法返回用于从数据库中删除联系人记录的确认窗体 （请参阅 Figure20）。</span><span class="sxs-lookup"><span data-stu-id="dd74d-400">The first Delete() method returns a confirmation form for deleting a contact record from the database (see Figure20).</span></span> <span data-ttu-id="dd74d-401">第二个 delete （） 方法执行实际删除操作针对的数据库。</span><span class="sxs-lookup"><span data-stu-id="dd74d-401">The second Delete() method performs the actual delete operation against the database.</span></span> <span data-ttu-id="dd74d-402">从数据库中检索原始联系人后，调用的实体框架 DeleteObject() 和 savechanges （） 方法来执行数据库删除。</span><span class="sxs-lookup"><span data-stu-id="dd74d-402">After the original contact has been retrieved from the database, the Entity Framework DeleteObject() and SaveChanges() methods are called to perform the database delete.</span></span>


<span data-ttu-id="dd74d-403">[![新建项目对话框](iteration-1-create-the-application-vb/_static/image20.jpg)](iteration-1-create-the-application-vb/_static/image39.png)</span><span class="sxs-lookup"><span data-stu-id="dd74d-403">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image20.jpg)](iteration-1-create-the-application-vb/_static/image39.png)</span></span>

<span data-ttu-id="dd74d-404">**图 20**:删除确认视图 ([单击此项可查看原尺寸图像](iteration-1-create-the-application-vb/_static/image40.png))</span><span class="sxs-lookup"><span data-stu-id="dd74d-404">**Figure 20**: The delete confirmation view ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image40.png))</span></span>


<span data-ttu-id="dd74d-405">我们需要修改索引视图，使其包含用于删除联系人记录 （请参阅图 21） 的链接。</span><span class="sxs-lookup"><span data-stu-id="dd74d-405">We need to modify the Index view so that it contains a link for deleting contact records (see Figure 21).</span></span> <span data-ttu-id="dd74d-406">需要将以下代码添加到同一个表包含的单元格的编辑链接：</span><span class="sxs-lookup"><span data-stu-id="dd74d-406">You need to add the following code to the same table cell that contains the Edit link:</span></span>

<span data-ttu-id="dd74d-407">{.id = 项。Id}) %&gt;</span><span class="sxs-lookup"><span data-stu-id="dd74d-407">{.id = item.Id})%&gt;</span></span>


<span data-ttu-id="dd74d-408">[![新建项目对话框](iteration-1-create-the-application-vb/_static/image21.jpg)](iteration-1-create-the-application-vb/_static/image41.png)</span><span class="sxs-lookup"><span data-stu-id="dd74d-408">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image21.jpg)](iteration-1-create-the-application-vb/_static/image41.png)</span></span>

<span data-ttu-id="dd74d-409">**图 21**:索引视图与编辑链接 ([单击此项可查看原尺寸图像](iteration-1-create-the-application-vb/_static/image42.png))</span><span class="sxs-lookup"><span data-stu-id="dd74d-409">**Figure 21**: Index view with Edit link ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image42.png))</span></span>


<span data-ttu-id="dd74d-410">接下来，我们需要创建删除确认视图。</span><span class="sxs-lookup"><span data-stu-id="dd74d-410">Next, we need to create the delete confirmation view.</span></span> <span data-ttu-id="dd74d-411">右键单击主页控制器类中的 delete （） 方法并选择添加视图菜单选项。</span><span class="sxs-lookup"><span data-stu-id="dd74d-411">Right-click the Delete() method in the Home controller class and select the menu option Add View.</span></span> <span data-ttu-id="dd74d-412">添加视图对话框中显示 （请参阅图 22）。</span><span class="sxs-lookup"><span data-stu-id="dd74d-412">The Add View dialog appears (see Figure 22).</span></span>

<span data-ttu-id="dd74d-413">与不同的列表、 创建和编辑视图中，在添加视图对话框中不包含创建删除视图的选项。</span><span class="sxs-lookup"><span data-stu-id="dd74d-413">Unlike in the case of the List, Create, and Edit views, the Add View dialog does not contain an option to create a Delete view.</span></span> <span data-ttu-id="dd74d-414">相反，选择**ContactManager.Models.Contact**数据类和**空**查看内容。</span><span class="sxs-lookup"><span data-stu-id="dd74d-414">Instead, select the **ContactManager.Models.Contact** data class and the **Empty** view content.</span></span> <span data-ttu-id="dd74d-415">选择空视图内容的选项都需要我们自己创建的视图。</span><span class="sxs-lookup"><span data-stu-id="dd74d-415">Selecting the Empty view content option will require us to create the view ourselves.</span></span>


<span data-ttu-id="dd74d-416">[![新建项目对话框](iteration-1-create-the-application-vb/_static/image22.jpg)](iteration-1-create-the-application-vb/_static/image43.png)</span><span class="sxs-lookup"><span data-stu-id="dd74d-416">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image22.jpg)](iteration-1-create-the-application-vb/_static/image43.png)</span></span>

<span data-ttu-id="dd74d-417">**图 22**:添加删除确认视图 ([单击此项可查看原尺寸图像](iteration-1-create-the-application-vb/_static/image44.png))</span><span class="sxs-lookup"><span data-stu-id="dd74d-417">**Figure 22**: Adding the delete confirmation view ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image44.png))</span></span>


<span data-ttu-id="dd74d-418">删除视图的内容包含在程序列表 9。</span><span class="sxs-lookup"><span data-stu-id="dd74d-418">The content of the Delete view is contained in Listing 9.</span></span> <span data-ttu-id="dd74d-419">此视图包含确认的窗体应为特定联系人是否删除 （请参阅图 21）。</span><span class="sxs-lookup"><span data-stu-id="dd74d-419">This view contains a form that confirms whether or not a particular contact should be deleted (see Figure 21).</span></span>

<span data-ttu-id="dd74d-420">**Listing 9 - Views\Home\Delete.aspx**</span><span class="sxs-lookup"><span data-stu-id="dd74d-420">**Listing 9 - Views\Home\Delete.aspx**</span></span>

[!code-aspx[Main](iteration-1-create-the-application-vb/samples/sample9.aspx)]

## <a name="changing-the-name-of-the-default-controller"></a><span data-ttu-id="dd74d-421">更改默认控制器的名称</span><span class="sxs-lookup"><span data-stu-id="dd74d-421">Changing the Name of the Default Controller</span></span>

<span data-ttu-id="dd74d-422">它可能会给您带来麻烦的我们的控制器类名称使用联系人名为 HomeController 类。</span><span class="sxs-lookup"><span data-stu-id="dd74d-422">It might bother you that the name of our controller class for working with contacts is named the HomeController class.</span></span> <span data-ttu-id="dd74d-423">不应将控制器命名为 ContactController？</span><span class="sxs-lookup"><span data-stu-id="dd74d-423">Shouldn't the controller be named ContactController?</span></span>

<span data-ttu-id="dd74d-424">此问题很容易修复。</span><span class="sxs-lookup"><span data-stu-id="dd74d-424">This issue is easy enough to fix.</span></span> <span data-ttu-id="dd74d-425">首先，我们需要重构的主控制器的名称。</span><span class="sxs-lookup"><span data-stu-id="dd74d-425">First, we need to refactor the name of the Home controller.</span></span> <span data-ttu-id="dd74d-426">Visual Studio 代码编辑器中打开 HomeController 类中，右键单击类的名称并选择菜单选项**重命名**。</span><span class="sxs-lookup"><span data-stu-id="dd74d-426">Open the HomeController class in the Visual Studio Code Editor, right click the name of the class and select the menu option **Rename**.</span></span> <span data-ttu-id="dd74d-427">选择此菜单选项打开重命名对话框。</span><span class="sxs-lookup"><span data-stu-id="dd74d-427">Selecting this menu option opens the Rename dialog.</span></span>


<span data-ttu-id="dd74d-428">[![新建项目对话框](iteration-1-create-the-application-vb/_static/image23.jpg)](iteration-1-create-the-application-vb/_static/image45.png)</span><span class="sxs-lookup"><span data-stu-id="dd74d-428">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image23.jpg)](iteration-1-create-the-application-vb/_static/image45.png)</span></span>

<span data-ttu-id="dd74d-429">**图 23**:重构的控制器的名称 ([单击此项可查看原尺寸图像](iteration-1-create-the-application-vb/_static/image46.png))</span><span class="sxs-lookup"><span data-stu-id="dd74d-429">**Figure 23**: Refactoring a controller name ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image46.png))</span></span>


<span data-ttu-id="dd74d-430">[![新建项目对话框](iteration-1-create-the-application-vb/_static/image24.jpg)](iteration-1-create-the-application-vb/_static/image47.png)</span><span class="sxs-lookup"><span data-stu-id="dd74d-430">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image24.jpg)](iteration-1-create-the-application-vb/_static/image47.png)</span></span>

<span data-ttu-id="dd74d-431">**图 24**:使用重命名对话框 ([单击此项可查看原尺寸图像](iteration-1-create-the-application-vb/_static/image48.png))</span><span class="sxs-lookup"><span data-stu-id="dd74d-431">**Figure 24**: Using the Rename dialog ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image48.png))</span></span>


<span data-ttu-id="dd74d-432">如果您重命名控制器类，Visual Studio 将更新视图文件夹中的文件夹的名称。</span><span class="sxs-lookup"><span data-stu-id="dd74d-432">If you rename your controller class, Visual Studio will update the name of the folder in the Views folder as well.</span></span> <span data-ttu-id="dd74d-433">Visual Studio 将重命名为 \Views\Contact 文件夹 \Views\Home 文件夹。</span><span class="sxs-lookup"><span data-stu-id="dd74d-433">Visual Studio will rename the \Views\Home folder to the \Views\Contact folder.</span></span>

<span data-ttu-id="dd74d-434">进行此更改后，你的应用程序将不再具有主控制器。</span><span class="sxs-lookup"><span data-stu-id="dd74d-434">After you make this change, your application will no longer have a Home controller.</span></span> <span data-ttu-id="dd74d-435">运行你的应用程序时，会图 25 中显示错误页。</span><span class="sxs-lookup"><span data-stu-id="dd74d-435">When you run your application, you'll get the error page in Figure 25.</span></span>


<span data-ttu-id="dd74d-436">[![新建项目对话框](iteration-1-create-the-application-vb/_static/image25.jpg)](iteration-1-create-the-application-vb/_static/image49.png)</span><span class="sxs-lookup"><span data-stu-id="dd74d-436">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image25.jpg)](iteration-1-create-the-application-vb/_static/image49.png)</span></span>

<span data-ttu-id="dd74d-437">**图 25**:没有默认控制器 ([单击此项可查看原尺寸图像](iteration-1-create-the-application-vb/_static/image50.png))</span><span class="sxs-lookup"><span data-stu-id="dd74d-437">**Figure 25**: No default controller ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image50.png))</span></span>


<span data-ttu-id="dd74d-438">我们需要更新使用而不是主控制器的联系控制器在 Global.asax 文件中的默认路由。</span><span class="sxs-lookup"><span data-stu-id="dd74d-438">We need to update the default route in the Global.asax file to use the Contact controller instead of the Home controller.</span></span> <span data-ttu-id="dd74d-439">打开 Global.asax 文件并修改默认控制器使用的默认路由 （请参阅代码清单 10）。</span><span class="sxs-lookup"><span data-stu-id="dd74d-439">Open the Global.asax file and modify the default controller used by the default route (see Listing 10).</span></span>

<span data-ttu-id="dd74d-440">**Listing 10 - Global.asax.vb**</span><span class="sxs-lookup"><span data-stu-id="dd74d-440">**Listing 10 - Global.asax.vb**</span></span>

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample10.vb)]

<span data-ttu-id="dd74d-441">进行这些更改后，联系人管理器将正常运行。</span><span class="sxs-lookup"><span data-stu-id="dd74d-441">After you make these changes, the Contact Manager will run correctly.</span></span> <span data-ttu-id="dd74d-442">现在，它将用作默认控制器 Contact 控制器类。</span><span class="sxs-lookup"><span data-stu-id="dd74d-442">Now, it will use the Contact controller class as the default controller.</span></span>

## <a name="summary"></a><span data-ttu-id="dd74d-443">总结</span><span class="sxs-lookup"><span data-stu-id="dd74d-443">Summary</span></span>

<span data-ttu-id="dd74d-444">在此第一次迭代中，我们创建一个基本的联系人管理器应用程序中的最快方法可能。</span><span class="sxs-lookup"><span data-stu-id="dd74d-444">In this first iteration, we created a basic Contact Manager application in the fastest way possible.</span></span> <span data-ttu-id="dd74d-445">我们可利用 Visual Studio 自动生成有关我们的控制器和视图的初始代码了。</span><span class="sxs-lookup"><span data-stu-id="dd74d-445">We took advantage of Visual Studio to generate the initial code for our controllers and views automatically.</span></span> <span data-ttu-id="dd74d-446">我们还利用了实体框架可以自动生成我们的数据库模型类。</span><span class="sxs-lookup"><span data-stu-id="dd74d-446">We also took advantage of the Entity Framework to generate our database model classes automatically.</span></span>

<span data-ttu-id="dd74d-447">目前，我们可以列出、 创建、 编辑和删除联系人与联系人管理器应用程序记录。</span><span class="sxs-lookup"><span data-stu-id="dd74d-447">Currently, we can list, create, edit, and delete contact records with the Contact Manager application.</span></span> <span data-ttu-id="dd74d-448">换而言之，我们可以执行所有数据库驱动的 web 应用程序所需的基本数据库操作。</span><span class="sxs-lookup"><span data-stu-id="dd74d-448">In other words, we can perform all of the basic database operations required by a database-driven web application.</span></span>

<span data-ttu-id="dd74d-449">遗憾的是，我们的应用程序有一些问题。</span><span class="sxs-lookup"><span data-stu-id="dd74d-449">Unfortunately, our application has some problems.</span></span> <span data-ttu-id="dd74d-450">第一，我不愿意再不得不承认，联系人管理器应用程序不是最具吸引力的应用程序。</span><span class="sxs-lookup"><span data-stu-id="dd74d-450">First and I hesitate to admit this, the Contact Manager application is not the most attractive application.</span></span> <span data-ttu-id="dd74d-451">它需要一些设计工作。</span><span class="sxs-lookup"><span data-stu-id="dd74d-451">It needs some design work.</span></span> <span data-ttu-id="dd74d-452">在下一个迭代中，我们将介绍如何更改默认视图母版页和级联样式表，以改善应用程序的外观。</span><span class="sxs-lookup"><span data-stu-id="dd74d-452">In the next iteration, we'll look at how we can change the default view master page and cascading style sheet to improve the appearance of the application.</span></span>

<span data-ttu-id="dd74d-453">其次，我们尚未实现任何窗体验证。</span><span class="sxs-lookup"><span data-stu-id="dd74d-453">Second, we have not implemented any form validation.</span></span> <span data-ttu-id="dd74d-454">例如，没有执行任何操作，以防用户提交创建联系人窗体而无需任何窗体字段输入值。</span><span class="sxs-lookup"><span data-stu-id="dd74d-454">For example, there is nothing to prevent you from submitting the Create contact form without entering values for any of the form fields.</span></span> <span data-ttu-id="dd74d-455">此外，可以输入无效的电话号码和电子邮件地址。</span><span class="sxs-lookup"><span data-stu-id="dd74d-455">Furthermore, you can enter invalid phone numbers and email addresses.</span></span> <span data-ttu-id="dd74d-456">我们首先来解决这个问题在迭代 #3 中的窗体验证。</span><span class="sxs-lookup"><span data-stu-id="dd74d-456">We start to tackle the problem of form validation in iteration #3.</span></span>

<span data-ttu-id="dd74d-457">最后，并最重要的是，联系人管理器应用程序的当前迭代无法轻松地修改或维护。</span><span class="sxs-lookup"><span data-stu-id="dd74d-457">Finally, and most importantly, the current iteration of the Contact Manager application cannot be easily modified or maintained.</span></span> <span data-ttu-id="dd74d-458">例如，数据库访问逻辑的控制器操作中已包含右。</span><span class="sxs-lookup"><span data-stu-id="dd74d-458">For example, the database access logic is baked right into the controller actions.</span></span> <span data-ttu-id="dd74d-459">这意味着，我们不能修改数据访问代码，而无需修改我们的控制器。</span><span class="sxs-lookup"><span data-stu-id="dd74d-459">This means that we cannot modify our data access code without modifying our controllers.</span></span> <span data-ttu-id="dd74d-460">在后续迭代中，我们将探讨我们可以实现以使联系人管理器更具弹性，若要更改的软件设计模式。</span><span class="sxs-lookup"><span data-stu-id="dd74d-460">In later iterations, we explore software design patterns that we can implement to make the Contact Manager more resilient to change.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="dd74d-461">[上一页](iteration-7-add-ajax-functionality-cs.md)
> [下一页](iteration-2-make-the-application-look-nice-vb.md)</span><span class="sxs-lookup"><span data-stu-id="dd74d-461">[Previous](iteration-7-add-ajax-functionality-cs.md)
[Next](iteration-2-make-the-application-look-nice-vb.md)</span></span>

---
uid: mvc/overview/older-versions-1/contact-manager/iteration-1-create-the-application-vb
title: 迭代#1 = 创建应用程序 （VB） |微软文档
author: rick-anderson
description: 在第一次迭代中，我们以最简单的方式创建联系人管理器。 我们增加了对基本数据库操作的支持：创建、读取、更新和 D...
ms.author: riande
ms.date: 02/20/2009
ms.assetid: 5b033582-1646-42c2-b20d-7edc8814e970
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-1-create-the-application-vb
msc.type: authoredcontent
ms.openlocfilehash: 235f6f8812a2f584de8e07dcf97d5c1712c51776
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542529"
---
# <a name="iteration-1--create-the-application-vb"></a><span data-ttu-id="ccc81-104">迭代 1 – 创建应用程序 (VB)</span><span class="sxs-lookup"><span data-stu-id="ccc81-104">Iteration #1 – Create the Application (VB)</span></span>

<span data-ttu-id="ccc81-105">由[微软](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="ccc81-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="ccc81-106">下载代码</span><span class="sxs-lookup"><span data-stu-id="ccc81-106">Download Code</span></span>](iteration-1-create-the-application-vb/_static/contactmanager_1_vb1.zip)

> <span data-ttu-id="ccc81-107">在第一次迭代中，我们以最简单的方式创建联系人管理器。</span><span class="sxs-lookup"><span data-stu-id="ccc81-107">In the first iteration, we create the Contact Manager in the simplest way possible.</span></span> <span data-ttu-id="ccc81-108">我们添加对基本数据库操作的支持：创建、读取、更新和删除 （CRUD）。</span><span class="sxs-lookup"><span data-stu-id="ccc81-108">We add support for basic database operations: Create, Read, Update, and Delete (CRUD).</span></span>

## <a name="building-a-contact-management-aspnet-mvc-application-vb"></a><span data-ttu-id="ccc81-109">构建 MVC 应用程序 （VB） ASP.NET联系人管理</span><span class="sxs-lookup"><span data-stu-id="ccc81-109">Building a Contact Management ASP.NET MVC Application (VB)</span></span>

<span data-ttu-id="ccc81-110">在本系列教程中，我们从头到尾构建整个联系人管理应用程序。</span><span class="sxs-lookup"><span data-stu-id="ccc81-110">In this series of tutorials, we build an entire Contact Management application from start to finish.</span></span> <span data-ttu-id="ccc81-111">通过联系人管理器应用程序，您可以存储联系人信息 （姓名、电话号码和电子邮件地址） 人员列表。</span><span class="sxs-lookup"><span data-stu-id="ccc81-111">The Contact Manager application enables you to store contact information - names, phone numbers and email addresses - for a list of people.</span></span>

<span data-ttu-id="ccc81-112">我们通过多次迭代构建应用程序。</span><span class="sxs-lookup"><span data-stu-id="ccc81-112">We build the application over multiple iterations.</span></span> <span data-ttu-id="ccc81-113">每次迭代时，我们都会逐步改进应用程序。</span><span class="sxs-lookup"><span data-stu-id="ccc81-113">With each iteration, we gradually improve the application.</span></span> <span data-ttu-id="ccc81-114">此多迭代方法的目标是使您能够了解每次更改的原因。</span><span class="sxs-lookup"><span data-stu-id="ccc81-114">The goal of this multiple iteration approach is to enable you to understand the reason for each change.</span></span>

- <span data-ttu-id="ccc81-115">迭代#1 - 创建应用程序。</span><span class="sxs-lookup"><span data-stu-id="ccc81-115">Iteration #1 - Create the application.</span></span> <span data-ttu-id="ccc81-116">在第一次迭代中，我们以最简单的方式创建联系人管理器。</span><span class="sxs-lookup"><span data-stu-id="ccc81-116">In the first iteration, we create the Contact Manager in the simplest way possible.</span></span> <span data-ttu-id="ccc81-117">我们添加对基本数据库操作的支持：创建、读取、更新和删除 （CRUD）。</span><span class="sxs-lookup"><span data-stu-id="ccc81-117">We add support for basic database operations: Create, Read, Update, and Delete (CRUD).</span></span>

- <span data-ttu-id="ccc81-118">迭代#2 - 使应用程序看起来不错。</span><span class="sxs-lookup"><span data-stu-id="ccc81-118">Iteration #2 - Make the application look nice.</span></span> <span data-ttu-id="ccc81-119">在此迭代中，我们通过修改默认ASP.NET MVC 视图母版页和级联样式表来改进应用程序的外观。</span><span class="sxs-lookup"><span data-stu-id="ccc81-119">In this iteration, we improve the appearance of the application by modifying the default ASP.NET MVC view master page and cascading style sheet.</span></span>

- <span data-ttu-id="ccc81-120">迭代#3 - 添加表单验证。</span><span class="sxs-lookup"><span data-stu-id="ccc81-120">Iteration #3 - Add form validation.</span></span> <span data-ttu-id="ccc81-121">在第三个迭代中，我们添加基本表单验证。</span><span class="sxs-lookup"><span data-stu-id="ccc81-121">In the third iteration, we add basic form validation.</span></span> <span data-ttu-id="ccc81-122">我们防止人们在未填写所需表单字段的情况下提交表单。</span><span class="sxs-lookup"><span data-stu-id="ccc81-122">We prevent people from submitting a form without completing required form fields.</span></span> <span data-ttu-id="ccc81-123">我们还验证电子邮件地址和电话号码。</span><span class="sxs-lookup"><span data-stu-id="ccc81-123">We also validate email addresses and phone numbers.</span></span>

- <span data-ttu-id="ccc81-124">迭代#4 - 使应用程序松散耦合。</span><span class="sxs-lookup"><span data-stu-id="ccc81-124">Iteration #4 - Make the application loosely coupled.</span></span> <span data-ttu-id="ccc81-125">在第四次迭代中，我们利用多种软件设计模式，使维护和修改联系人管理器应用程序变得更加容易。</span><span class="sxs-lookup"><span data-stu-id="ccc81-125">In this fourth iteration, we take advantage of several software design patterns to make it easier to maintain and modify the Contact Manager application.</span></span> <span data-ttu-id="ccc81-126">例如，我们重构应用程序以使用存储库模式和依赖项注入模式。</span><span class="sxs-lookup"><span data-stu-id="ccc81-126">For example, we refactor our application to use the Repository pattern and the Dependency Injection pattern.</span></span>

- <span data-ttu-id="ccc81-127">迭代#5 - 创建单元测试。</span><span class="sxs-lookup"><span data-stu-id="ccc81-127">Iteration #5 - Create unit tests.</span></span> <span data-ttu-id="ccc81-128">在第五次迭代中，我们通过添加单元测试使应用程序更易于维护和修改。</span><span class="sxs-lookup"><span data-stu-id="ccc81-128">In the fifth iteration, we make our application easier to maintain and modify by adding unit tests.</span></span> <span data-ttu-id="ccc81-129">我们模拟数据模型类，并为控制器和验证逻辑构建单元测试。</span><span class="sxs-lookup"><span data-stu-id="ccc81-129">We mock our data model classes and build unit tests for our controllers and validation logic.</span></span>

- <span data-ttu-id="ccc81-130">迭代#6 - 使用测试驱动开发。</span><span class="sxs-lookup"><span data-stu-id="ccc81-130">Iteration #6 - Use test-driven development.</span></span> <span data-ttu-id="ccc81-131">在第六次迭代中，我们首先编写单元测试并针对单元测试编写代码，从而向应用程序添加新功能。</span><span class="sxs-lookup"><span data-stu-id="ccc81-131">In this sixth iteration, we add new functionality to our application by writing unit tests first and writing code against the unit tests.</span></span> <span data-ttu-id="ccc81-132">在此迭代中，我们添加联系人组。</span><span class="sxs-lookup"><span data-stu-id="ccc81-132">In this iteration, we add contact groups.</span></span>

- <span data-ttu-id="ccc81-133">迭代#7 - 添加Ajax功能。</span><span class="sxs-lookup"><span data-stu-id="ccc81-133">Iteration #7 - Add Ajax functionality.</span></span> <span data-ttu-id="ccc81-134">在第七次迭代中，我们通过增加对Ajax的支持来提高应用程序的响应性和性能。</span><span class="sxs-lookup"><span data-stu-id="ccc81-134">In the seventh iteration, we improve the responsiveness and performance of our application by adding support for Ajax.</span></span>

## <a name="this-iteration"></a><span data-ttu-id="ccc81-135">此迭代</span><span class="sxs-lookup"><span data-stu-id="ccc81-135">This Iteration</span></span>

<span data-ttu-id="ccc81-136">在第一次迭代中，我们将构建基本应用程序。</span><span class="sxs-lookup"><span data-stu-id="ccc81-136">In this first iteration, we build the basic application.</span></span> <span data-ttu-id="ccc81-137">目标是以最快、最简单的方式构建联系人管理器。</span><span class="sxs-lookup"><span data-stu-id="ccc81-137">The goal is to build the Contact Manager in the fastest and simplest way possible.</span></span> <span data-ttu-id="ccc81-138">在以后的迭代中，我们改进了应用程序的设计。</span><span class="sxs-lookup"><span data-stu-id="ccc81-138">In later iterations, we improve the design of the application.</span></span>

<span data-ttu-id="ccc81-139">联系人管理器应用程序是一个基本的数据库驱动应用程序。</span><span class="sxs-lookup"><span data-stu-id="ccc81-139">The Contact Manager application is a basic database-driven application.</span></span> <span data-ttu-id="ccc81-140">您可以使用该应用程序创建新联系人、编辑现有联系人和删除联系人。</span><span class="sxs-lookup"><span data-stu-id="ccc81-140">You can use the application to create new contacts, edit existing contacts, and delete contacts.</span></span>

<span data-ttu-id="ccc81-141">在此迭代中，我们完成以下步骤：</span><span class="sxs-lookup"><span data-stu-id="ccc81-141">In this iteration, we complete the following steps:</span></span>

1. <span data-ttu-id="ccc81-142">ASP.NET MVC 应用程序</span><span class="sxs-lookup"><span data-stu-id="ccc81-142">ASP.NET MVC application</span></span>
2. <span data-ttu-id="ccc81-143">创建数据库以存储我们的联系人</span><span class="sxs-lookup"><span data-stu-id="ccc81-143">Create a database to store our contacts</span></span>
3. <span data-ttu-id="ccc81-144">使用 Microsoft 实体框架为我们的数据库生成模型类</span><span class="sxs-lookup"><span data-stu-id="ccc81-144">Generate a model class for our database with the Microsoft Entity Framework</span></span>
4. <span data-ttu-id="ccc81-145">创建控制器操作和视图，使我们能够列出数据库中的所有联系人</span><span class="sxs-lookup"><span data-stu-id="ccc81-145">Create a controller action and view that enables us to list all of the contacts in the database</span></span>
5. <span data-ttu-id="ccc81-146">创建控制器操作和视图，使我们能够在数据库中创建新联系人</span><span class="sxs-lookup"><span data-stu-id="ccc81-146">Create controller actions and a view that enables us to create a new contact in the database</span></span>
6. <span data-ttu-id="ccc81-147">创建控制器操作和视图，使我们能够编辑数据库中的现有联系人</span><span class="sxs-lookup"><span data-stu-id="ccc81-147">Create controller actions and a view that enables us to edit an existing contact in the database</span></span>
7. <span data-ttu-id="ccc81-148">创建控制器操作和视图，使我们能够删除数据库中的现有联系人</span><span class="sxs-lookup"><span data-stu-id="ccc81-148">Create controller actions and a view that enables us to delete an existing contact in the database</span></span>

## <a name="software-prerequisites"></a><span data-ttu-id="ccc81-149">必备软件</span><span class="sxs-lookup"><span data-stu-id="ccc81-149">Software Prerequisites</span></span>

<span data-ttu-id="ccc81-150">在ASP.NET MVC 应用程序中，必须在您的计算机上安装 Visual Studio 2008 或 Visual Web 开发人员 2008（可视化 Web 开发人员是 Visual Studio 的免费版本，不包含 Visual Studio 的所有高级功能）。</span><span class="sxs-lookup"><span data-stu-id="ccc81-150">In ASP.NET MVC applications, you must have either Visual Studio 2008 or Visual Web Developer 2008 installed on your computer (Visual Web Developer is a free version of Visual Studio that does not include all of the advanced features of Visual Studio).</span></span> <span data-ttu-id="ccc81-151">您可以通过以下地址下载 Visual Studio 2008 试用版或可视化 Web 开发人员版本：</span><span class="sxs-lookup"><span data-stu-id="ccc81-151">You can download either the trial version of Visual Studio 2008 or Visual Web Developer from the following address:</span></span>

[https://www.asp.net/downloads/essential/](https://www.asp.net/downloads/essential)

> [!NOTE] 
> 
> <span data-ttu-id="ccc81-152">对于具有可视化 Web 开发人员ASP.NET MVC 应用程序，必须安装可视化 Web 开发人员服务包 1。</span><span class="sxs-lookup"><span data-stu-id="ccc81-152">For ASP.NET MVC applications with Visual Web Developer, you must have Visual Web Developer Service Pack 1 installed.</span></span> <span data-ttu-id="ccc81-153">如果没有服务包 1，则无法创建 Web 应用程序项目。</span><span class="sxs-lookup"><span data-stu-id="ccc81-153">Without Service Pack 1, you cannot create Web Application Projects.</span></span>

<span data-ttu-id="ccc81-154">ASP.NET MVC 框架。</span><span class="sxs-lookup"><span data-stu-id="ccc81-154">ASP.NET MVC framework.</span></span> <span data-ttu-id="ccc81-155">可以从以下地址下载ASP.NET MVC 框架：</span><span class="sxs-lookup"><span data-stu-id="ccc81-155">You can download the ASP.NET MVC framework from the following address:</span></span>

[https://www.asp.net/mvc](../../../index.md)

<span data-ttu-id="ccc81-156">在本教程中，我们使用 Microsoft 实体框架访问数据库。</span><span class="sxs-lookup"><span data-stu-id="ccc81-156">In this tutorial, we use the Microsoft Entity Framework to access a database.</span></span> <span data-ttu-id="ccc81-157">实体框架包含在 .NET 框架 3.5 服务包 1 中。</span><span class="sxs-lookup"><span data-stu-id="ccc81-157">The Entity Framework is included with .NET Framework 3.5 Service Pack 1.</span></span> <span data-ttu-id="ccc81-158">您可以通过以下位置下载此服务包：</span><span class="sxs-lookup"><span data-stu-id="ccc81-158">You can download this service pack from the following location:</span></span>

[<span data-ttu-id="ccc81-159">https://www.microsoft.com/downloads/details.aspx?familyid=ab99342f-5d1a-413d-8319-81da479ab0d7&amp;d斯普拉朗</span><span class="sxs-lookup"><span data-stu-id="ccc81-159">https://www.microsoft.com/downloads/details.aspx?familyid=ab99342f-5d1a-413d-8319-81da479ab0d7&amp;displaylang=en</span></span>](https://www.microsoft.com/downloads/details.aspx?familyid=ab99342f-5d1a-413d-8319-81da479ab0d7&amp;displaylang=en)

<span data-ttu-id="ccc81-160">作为逐个执行每个下载的替代方法，您可以利用 Web 平台安装程序 （Web PI）。</span><span class="sxs-lookup"><span data-stu-id="ccc81-160">As an alternative to performing each of these downloads one by one, you can take advantage of the Web Platform Installer (Web PI).</span></span> <span data-ttu-id="ccc81-161">您可以通过以下地址下载 Web PI：</span><span class="sxs-lookup"><span data-stu-id="ccc81-161">You can download the Web PI from the following address:</span></span>

[https://www.asp.net/downloads/essential/](https://www.asp.net/downloads/essential)

## <a name="aspnet-mvc-project"></a><span data-ttu-id="ccc81-162">ASP.NET MVC 项目</span><span class="sxs-lookup"><span data-stu-id="ccc81-162">ASP.NET MVC Project</span></span>

<span data-ttu-id="ccc81-163">ASP.NET MVC Web 应用程序项目。</span><span class="sxs-lookup"><span data-stu-id="ccc81-163">ASP.NET MVC Web Application Project.</span></span> <span data-ttu-id="ccc81-164">启动可视化工作室并选择菜单选项**文件，新项目**。</span><span class="sxs-lookup"><span data-stu-id="ccc81-164">Launch Visual Studio and select the menu option **File, New Project**.</span></span> <span data-ttu-id="ccc81-165">将显示 **"新项目"** 对话框（参见图 1）。</span><span class="sxs-lookup"><span data-stu-id="ccc81-165">The **New Project** dialog appears (see Figure 1).</span></span> <span data-ttu-id="ccc81-166">选择**Web**项目类型和**ASP.NET MVC Web 应用程序**模板。</span><span class="sxs-lookup"><span data-stu-id="ccc81-166">Select the **Web** project type and the **ASP.NET MVC Web Application** template.</span></span> <span data-ttu-id="ccc81-167">说出您的新项目*联系人管理器*，然后单击"确定"按钮。</span><span class="sxs-lookup"><span data-stu-id="ccc81-167">Name your new project *ContactManager* and click the OK button.</span></span>

<span data-ttu-id="ccc81-168">请确保从 **"新项目"** 对话框右上角的下拉列表中选择了 .NET Framework 3.5。</span><span class="sxs-lookup"><span data-stu-id="ccc81-168">Make sure that you have .NET Framework 3.5 selected from the dropdown list at the top right of the **New Project** dialog.</span></span> <span data-ttu-id="ccc81-169">否则，将不会显示ASP.NET MVC Web 应用程序模板。</span><span class="sxs-lookup"><span data-stu-id="ccc81-169">Otherwise, the ASP.NET MVC Web Application template won't appear.</span></span>

<span data-ttu-id="ccc81-170">[![“新建项目”对话框](iteration-1-create-the-application-vb/_static/image1.jpg)](iteration-1-create-the-application-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="ccc81-170">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image1.jpg)](iteration-1-create-the-application-vb/_static/image1.png)</span></span>

<span data-ttu-id="ccc81-171">**图 01**： 新项目对话框（[单击以查看全尺寸图像](iteration-1-create-the-application-vb/_static/image2.png)）</span><span class="sxs-lookup"><span data-stu-id="ccc81-171">**Figure 01**: The New Project dialog([Click to view full-size image](iteration-1-create-the-application-vb/_static/image2.png))</span></span>

<span data-ttu-id="ccc81-172">ASP.NET MVC 应用程序，将显示 **"创建单元测试项目**"对话框。</span><span class="sxs-lookup"><span data-stu-id="ccc81-172">ASP.NET MVC application, the **Create Unit Test Project** dialog appears.</span></span> <span data-ttu-id="ccc81-173">可以使用此对话框指示在创建ASP.NET MVC 应用程序时要创建单元测试项目并将其添加到解决方案中。</span><span class="sxs-lookup"><span data-stu-id="ccc81-173">You can use this dialog to indicate that you want to create and add a unit test project to your solution when you create your ASP.NET MVC application.</span></span> <span data-ttu-id="ccc81-174">尽管我们在此迭代中不会构建单元测试，但应选择选项 **"是"，创建单元测试项目**，因为我们计划在以后的迭代中添加单元测试。</span><span class="sxs-lookup"><span data-stu-id="ccc81-174">Although we won't be building unit tests in this iteration, you should select the option **Yes, create a unit test project** because we plan to add unit tests in a later iteration.</span></span> <span data-ttu-id="ccc81-175">首次创建新的ASP.NET MVC 项目时添加测试项目比创建ASP.NET MVC 项目后添加测试项目要容易得多。</span><span class="sxs-lookup"><span data-stu-id="ccc81-175">Adding a Test project when you first create a new ASP.NET MVC project is much easier than adding a Test project after the ASP.NET MVC project has been created.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="ccc81-176">由于可视化 Web 开发人员不支持测试项目，因此在使用可视化 Web 开发人员时，您不会获取"创建单元测试项目"对话框。</span><span class="sxs-lookup"><span data-stu-id="ccc81-176">Because Visual Web Developer does not support Test projects, you do not get the Create Unit Test Project dialog when using Visual Web Developer.</span></span>

<span data-ttu-id="ccc81-177">[![“新建项目”对话框](iteration-1-create-the-application-vb/_static/image2.jpg)](iteration-1-create-the-application-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="ccc81-177">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image2.jpg)](iteration-1-create-the-application-vb/_static/image3.png)</span></span>

<span data-ttu-id="ccc81-178">**图 02**： 创建单元测试项目对话框 （[单击以查看全尺寸图像](iteration-1-create-the-application-vb/_static/image4.png)）</span><span class="sxs-lookup"><span data-stu-id="ccc81-178">**Figure 02**: The Create Unit Test Project dialog ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image4.png))</span></span>

<span data-ttu-id="ccc81-179">ASP.NET MVC 应用程序显示在可视化工作室解决方案资源管理器窗口中（参见图 3）。</span><span class="sxs-lookup"><span data-stu-id="ccc81-179">ASP.NET MVC application appears in the Visual Studio Solution Explorer window (see Figure 3).</span></span> <span data-ttu-id="ccc81-180">如果看不到"解决方案资源管理器"窗口，则可以通过选择菜单选项 **"视图"、"解决方案资源管理器**"来打开此窗口。</span><span class="sxs-lookup"><span data-stu-id="ccc81-180">If you don t see the Solution Explorer window then you can open this window by selecting the menu option **View, Solution Explorer**.</span></span> <span data-ttu-id="ccc81-181">请注意，该解决方案包含两个项目：ASP.NET MVC 项目和测试项目。</span><span class="sxs-lookup"><span data-stu-id="ccc81-181">Notice that the solution contains two projects: the ASP.NET MVC project and the Test project.</span></span> <span data-ttu-id="ccc81-182">mVCASP.NET项目命名为"联系人管理器"，测试项目命名为"联系人管理器"。</span><span class="sxs-lookup"><span data-stu-id="ccc81-182">The ASP.NET MVC project is named ContactManager and the Test project is named ContactManager.Tests.</span></span>

<span data-ttu-id="ccc81-183">[![“新建项目”对话框](iteration-1-create-the-application-vb/_static/image3.jpg)](iteration-1-create-the-application-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="ccc81-183">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image3.jpg)](iteration-1-create-the-application-vb/_static/image5.png)</span></span>

<span data-ttu-id="ccc81-184">**图 03**： 解决方案资源管理器窗口 （[单击以查看全尺寸图像](iteration-1-create-the-application-vb/_static/image6.png)）</span><span class="sxs-lookup"><span data-stu-id="ccc81-184">**Figure 03**: The Solution Explorer window ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image6.png))</span></span>

## <a name="deleting-the-project-sample-files"></a><span data-ttu-id="ccc81-185">删除项目示例文件</span><span class="sxs-lookup"><span data-stu-id="ccc81-185">Deleting the Project Sample Files</span></span>

<span data-ttu-id="ccc81-186">ASP.NET MVC 项目模板包括控制器和视图的示例文件。</span><span class="sxs-lookup"><span data-stu-id="ccc81-186">The ASP.NET MVC project template includes sample files for controllers and views.</span></span> <span data-ttu-id="ccc81-187">在创建新ASP.NET MVC 应用程序之前，应删除这些文件。</span><span class="sxs-lookup"><span data-stu-id="ccc81-187">Before creating a new ASP.NET MVC application, you should delete these files.</span></span> <span data-ttu-id="ccc81-188">您可以通过右键单击文件或文件夹并选择菜单选项 **"删除**"来删除解决方案资源管理器窗口中的文件和文件夹。</span><span class="sxs-lookup"><span data-stu-id="ccc81-188">You can delete files and folders in the Solution Explorer window by right-clicking a file or folder and selecting the menu option **Delete**.</span></span>

<span data-ttu-id="ccc81-189">您需要从 ASP.NET MVC 项目中删除以下文件：</span><span class="sxs-lookup"><span data-stu-id="ccc81-189">You need to delete the following files from the ASP.NET MVC project:</span></span>

- <span data-ttu-id="ccc81-190">[控制器]主控制器.vb</span><span class="sxs-lookup"><span data-stu-id="ccc81-190">\Controllers\HomeController.vb</span></span>

- <span data-ttu-id="ccc81-191">[视图]主页\关于.aspx</span><span class="sxs-lookup"><span data-stu-id="ccc81-191">\Views\Home\About.aspx</span></span>

- <span data-ttu-id="ccc81-192">[视图]主页\索引.aspx</span><span class="sxs-lookup"><span data-stu-id="ccc81-192">\Views\Home\Index.aspx</span></span>

<span data-ttu-id="ccc81-193">而且，您需要从测试项目中删除以下文件：</span><span class="sxs-lookup"><span data-stu-id="ccc81-193">And, you need to delete the following file from the Test project:</span></span>

<span data-ttu-id="ccc81-194">[控制器]主控制器测试.vb</span><span class="sxs-lookup"><span data-stu-id="ccc81-194">\Controllers\HomeControllerTest.vb</span></span>

## <a name="creating-the-database"></a><span data-ttu-id="ccc81-195">创建数据库</span><span class="sxs-lookup"><span data-stu-id="ccc81-195">Creating the Database</span></span>

<span data-ttu-id="ccc81-196">联系人管理器应用程序是数据库驱动的 Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="ccc81-196">The Contact Manager application is a database-driven web application.</span></span> <span data-ttu-id="ccc81-197">我们使用数据库来存储联系信息。</span><span class="sxs-lookup"><span data-stu-id="ccc81-197">We use a database to store the contact information.</span></span>

<span data-ttu-id="ccc81-198">ASP.NET MVC 框架，包含任何现代数据库，包括 Microsoft SQL Server、Oracle、MySQL 和 IBM DB2 数据库。</span><span class="sxs-lookup"><span data-stu-id="ccc81-198">The ASP.NET MVC framework with any modern database including Microsoft SQL Server, Oracle, MySQL, and IBM DB2 databases.</span></span> <span data-ttu-id="ccc81-199">在本教程中，我们使用 Microsoft SQL Server 数据库。</span><span class="sxs-lookup"><span data-stu-id="ccc81-199">In this tutorial, we use a Microsoft SQL Server database.</span></span> <span data-ttu-id="ccc81-200">安装 Visual Studio 时，系统会提供安装 Microsoft SQL Server Express 的选项，这是 Microsoft SQL Server 数据库的免费版本。</span><span class="sxs-lookup"><span data-stu-id="ccc81-200">When you install Visual Studio, you are provided with the option of installing Microsoft SQL Server Express which is a free version of the Microsoft SQL Server database.</span></span>

<span data-ttu-id="ccc81-201">通过右键单击解决方案资源管理器窗口中的应用\_数据文件夹并选择菜单选项 **"添加、新项目**"来创建新数据库。</span><span class="sxs-lookup"><span data-stu-id="ccc81-201">Create a new database by right-clicking the App\_Data folder in the Solution Explorer window and selecting the menu option **Add, New Item**.</span></span> <span data-ttu-id="ccc81-202">在 **"添加新项目"** 对话框中，选择 **"数据**"类别和**SQL Server 数据库**模板（参见图 4）。</span><span class="sxs-lookup"><span data-stu-id="ccc81-202">In the **Add New Item** dialog, select the **Data** category and the **SQL Server Database** template (see Figure 4).</span></span> <span data-ttu-id="ccc81-203">命名新数据库 ContactManagerDB.mdf，然后单击"确定"按钮。</span><span class="sxs-lookup"><span data-stu-id="ccc81-203">Name the new database ContactManagerDB.mdf and click the OK button.</span></span>

<span data-ttu-id="ccc81-204">[![“新建项目”对话框](iteration-1-create-the-application-vb/_static/image4.jpg)](iteration-1-create-the-application-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="ccc81-204">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image4.jpg)](iteration-1-create-the-application-vb/_static/image7.png)</span></span>

<span data-ttu-id="ccc81-205">**图04**：创建新的微软 SQL Server Express 数据库 （[单击以查看全尺寸图像](iteration-1-create-the-application-vb/_static/image8.png)）</span><span class="sxs-lookup"><span data-stu-id="ccc81-205">**Figure 04**: Creating a new Microsoft SQL Server Express database ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image8.png))</span></span>

<span data-ttu-id="ccc81-206">创建新数据库后，数据库将显示在解决方案资源管理器窗口中的应用\_数据文件夹中。</span><span class="sxs-lookup"><span data-stu-id="ccc81-206">After you create the new database, the database appears in the App\_Data folder in the Solution Explorer window.</span></span> <span data-ttu-id="ccc81-207">双击 ContactManager.mdf 文件以打开服务器资源管理器窗口并连接到数据库。</span><span class="sxs-lookup"><span data-stu-id="ccc81-207">Double-click the ContactManager.mdf file to open the Server Explorer window and connect to the database.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="ccc81-208">服务器资源管理器窗口称为数据库资源管理器窗口（对于 Microsoft 可视化 Web 开发人员）。</span><span class="sxs-lookup"><span data-stu-id="ccc81-208">The Server Explorer window is called the Database Explorer window in the case of Microsoft Visual Web Developer.</span></span>

<span data-ttu-id="ccc81-209">可以使用 Server 资源管理器窗口创建新的数据库对象，如数据库表、视图、触发器和存储过程。</span><span class="sxs-lookup"><span data-stu-id="ccc81-209">You can use the Server Explorer window to create new database objects such as database tables, views, triggers, and stored procedures.</span></span> <span data-ttu-id="ccc81-210">右键单击"表"文件夹并选择菜单选项 **"添加新表**"。</span><span class="sxs-lookup"><span data-stu-id="ccc81-210">Right-click the Tables folder and select the menu option **Add New Table**.</span></span> <span data-ttu-id="ccc81-211">将显示数据库表设计器（参见图 5）。</span><span class="sxs-lookup"><span data-stu-id="ccc81-211">The Database Table Designer appears (see Figure 5).</span></span>

<span data-ttu-id="ccc81-212">[![“新建项目”对话框](iteration-1-create-the-application-vb/_static/image5.jpg)](iteration-1-create-the-application-vb/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="ccc81-212">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image5.jpg)](iteration-1-create-the-application-vb/_static/image9.png)</span></span>

<span data-ttu-id="ccc81-213">**图 05**： 数据库表设计器 （[单击以查看全尺寸图像](iteration-1-create-the-application-vb/_static/image10.png)）</span><span class="sxs-lookup"><span data-stu-id="ccc81-213">**Figure 05**: The Database Table Designer ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image10.png))</span></span>

<span data-ttu-id="ccc81-214">我们需要创建一个包含以下列的表：</span><span class="sxs-lookup"><span data-stu-id="ccc81-214">We need to create a table that contains the following columns:</span></span>

<a id="0.2_table01"></a>

| <span data-ttu-id="ccc81-215">**列名**</span><span class="sxs-lookup"><span data-stu-id="ccc81-215">**Column Name**</span></span> | <span data-ttu-id="ccc81-216">**数据类型**</span><span class="sxs-lookup"><span data-stu-id="ccc81-216">**Data Type**</span></span> | <span data-ttu-id="ccc81-217">**允许 Null 值**</span><span class="sxs-lookup"><span data-stu-id="ccc81-217">**Allow Nulls**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ccc81-218">ID</span><span class="sxs-lookup"><span data-stu-id="ccc81-218">Id</span></span> | <span data-ttu-id="ccc81-219">int</span><span class="sxs-lookup"><span data-stu-id="ccc81-219">int</span></span> | <span data-ttu-id="ccc81-220">false</span><span class="sxs-lookup"><span data-stu-id="ccc81-220">false</span></span> |
| <span data-ttu-id="ccc81-221">FirstName</span><span class="sxs-lookup"><span data-stu-id="ccc81-221">FirstName</span></span> | <span data-ttu-id="ccc81-222">nvarchar(50)</span><span class="sxs-lookup"><span data-stu-id="ccc81-222">nvarchar(50)</span></span> | <span data-ttu-id="ccc81-223">false</span><span class="sxs-lookup"><span data-stu-id="ccc81-223">false</span></span> |
| <span data-ttu-id="ccc81-224">LastName</span><span class="sxs-lookup"><span data-stu-id="ccc81-224">LastName</span></span> | <span data-ttu-id="ccc81-225">nvarchar(50)</span><span class="sxs-lookup"><span data-stu-id="ccc81-225">nvarchar(50)</span></span> | <span data-ttu-id="ccc81-226">false</span><span class="sxs-lookup"><span data-stu-id="ccc81-226">false</span></span> |
| <span data-ttu-id="ccc81-227">电话</span><span class="sxs-lookup"><span data-stu-id="ccc81-227">Phone</span></span> | <span data-ttu-id="ccc81-228">nvarchar(50)</span><span class="sxs-lookup"><span data-stu-id="ccc81-228">nvarchar(50)</span></span> | <span data-ttu-id="ccc81-229">false</span><span class="sxs-lookup"><span data-stu-id="ccc81-229">false</span></span> |
| <span data-ttu-id="ccc81-230">电子邮件</span><span class="sxs-lookup"><span data-stu-id="ccc81-230">Email</span></span> | <span data-ttu-id="ccc81-231">nvarchar(255)</span><span class="sxs-lookup"><span data-stu-id="ccc81-231">nvarchar(255)</span></span> | <span data-ttu-id="ccc81-232">false</span><span class="sxs-lookup"><span data-stu-id="ccc81-232">false</span></span> |

<span data-ttu-id="ccc81-233">第一列"Id"列是特殊的。</span><span class="sxs-lookup"><span data-stu-id="ccc81-233">The first column, the Id column, is special.</span></span> <span data-ttu-id="ccc81-234">您需要将 Id 列标记为标识列和主键列。</span><span class="sxs-lookup"><span data-stu-id="ccc81-234">You need to mark the Id column as an Identity column and a Primary Key column.</span></span> <span data-ttu-id="ccc81-235">通过展开列属性（查看图 6 的底部）向下滚动到标识规范属性，指示列是标识列。</span><span class="sxs-lookup"><span data-stu-id="ccc81-235">You indicate that a column is an Identity column by expanding Column Properties (look at the bottom of Figure 6) and scrolling down to the Identity Specification property.</span></span> <span data-ttu-id="ccc81-236">将 **（是标识）** 属性设置为值**是**。</span><span class="sxs-lookup"><span data-stu-id="ccc81-236">Set the **(Is Identity)** property to the value **Yes**.</span></span>

<span data-ttu-id="ccc81-237">通过选择列并单击带有键图标的按钮，将列标记为主键列。</span><span class="sxs-lookup"><span data-stu-id="ccc81-237">You mark a column as a Primary Key column by selecting the column and clicking the button with the icon of a key.</span></span> <span data-ttu-id="ccc81-238">将列标记为主键列后，列旁边将显示一个键图标（参见图 6）。</span><span class="sxs-lookup"><span data-stu-id="ccc81-238">After a column is marked as a Primary Key column, an icon of a key appears next to the column (see Figure 6).</span></span>

<span data-ttu-id="ccc81-239">完成表创建后，单击"保存"按钮（带有软盘图标的按钮）以保存新表。</span><span class="sxs-lookup"><span data-stu-id="ccc81-239">After you finish creating the table, click the Save button (the button with an icon of a floppy) to save the new table.</span></span> <span data-ttu-id="ccc81-240">为您的新表命名 *"联系人*"。</span><span class="sxs-lookup"><span data-stu-id="ccc81-240">Give your new table the name *Contacts*.</span></span>

<span data-ttu-id="ccc81-241">完成创建"联系人"数据库表后，应向该表添加一些记录。</span><span class="sxs-lookup"><span data-stu-id="ccc81-241">After finish creating the Contacts database table, you should add some records to the table.</span></span> <span data-ttu-id="ccc81-242">右键单击服务器资源管理器窗口中的"联系人"表，然后选择菜单选项 **"显示表数据**"。</span><span class="sxs-lookup"><span data-stu-id="ccc81-242">Right-click the Contacts table in the Server Explorer window and select the menu option **Show Table Data**.</span></span> <span data-ttu-id="ccc81-243">在显示的网格中输入一个或多个联系人。</span><span class="sxs-lookup"><span data-stu-id="ccc81-243">Enter one or more contacts in the grid that appears.</span></span>

## <a name="creating-the-data-model"></a><span data-ttu-id="ccc81-244">创建数据模型</span><span class="sxs-lookup"><span data-stu-id="ccc81-244">Creating the Data Model</span></span>

<span data-ttu-id="ccc81-245">ASP.NET MVC 应用程序由模型、视图和控制器组成。</span><span class="sxs-lookup"><span data-stu-id="ccc81-245">The ASP.NET MVC application consists of Models, Views, and Controllers.</span></span> <span data-ttu-id="ccc81-246">我们首先创建一个模型类，该类表示我们在上一节中创建的"联系人"表。</span><span class="sxs-lookup"><span data-stu-id="ccc81-246">We start by creating a Model class that represents the Contacts table that we created in the previous section.</span></span>

<span data-ttu-id="ccc81-247">在本教程中，我们使用 Microsoft 实体框架从数据库自动生成模型类。</span><span class="sxs-lookup"><span data-stu-id="ccc81-247">In this tutorial, we use the Microsoft Entity Framework to generate a model class from the database automatically.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="ccc81-248">ASP.NET MVC 框架不以任何方式绑定到 Microsoft 实体框架。</span><span class="sxs-lookup"><span data-stu-id="ccc81-248">The ASP.NET MVC framework is not tied to the Microsoft Entity Framework in any way.</span></span> <span data-ttu-id="ccc81-249">您可以将mVCASP.NET替代数据库访问技术（包括 NHibernate、LINQ 到 SQL 或ADO.NET） 使用。</span><span class="sxs-lookup"><span data-stu-id="ccc81-249">You can use ASP.NET MVC with alternative database access technologies including NHibernate, LINQ to SQL, or ADO.NET.</span></span>

<span data-ttu-id="ccc81-250">按照以下步骤创建数据模型类：</span><span class="sxs-lookup"><span data-stu-id="ccc81-250">Follow these steps to create the data model classes:</span></span>

1. <span data-ttu-id="ccc81-251">右键单击"解决方案资源管理器"窗口中的"模型"文件夹，然后选择"**添加新项目**"。</span><span class="sxs-lookup"><span data-stu-id="ccc81-251">Right-click the Models folder in the Solution Explorer window and select **Add, New Item**.</span></span> <span data-ttu-id="ccc81-252">将显示 **"添加新项目"** 对话框（参见图 6）。</span><span class="sxs-lookup"><span data-stu-id="ccc81-252">The **Add New Item** dialog appears (see Figure 6).</span></span>
2. <span data-ttu-id="ccc81-253">选择 **"数据**"类别和**ADO.NET实体数据模型**模板。</span><span class="sxs-lookup"><span data-stu-id="ccc81-253">Select the **Data** category and the **ADO.NET Entity Data Model** template.</span></span> <span data-ttu-id="ccc81-254">命名数据模型*ContactManagerModel.edmx，* 然后单击 **"添加**"按钮。</span><span class="sxs-lookup"><span data-stu-id="ccc81-254">Name your data model *ContactManagerModel.edmx* and click the **Add** button.</span></span> <span data-ttu-id="ccc81-255">将显示实体数据模型向导（参见图 7）。</span><span class="sxs-lookup"><span data-stu-id="ccc81-255">The Entity Data Model wizard appears (see Figure 7).</span></span>
3. <span data-ttu-id="ccc81-256">在 **"选择模型内容"** 步骤中，选择**从数据库中生成**（参见图 7）。</span><span class="sxs-lookup"><span data-stu-id="ccc81-256">In the **Choose Model Contents** step, select **Generate from database** (see Figure 7).</span></span>
4. <span data-ttu-id="ccc81-257">在 **"选择数据连接**"步骤中，选择 ContactManagerDB.mdf 数据库，并输入实体连接设置的名称 *"联系人管理器数据库实体*"（参见图 8）。</span><span class="sxs-lookup"><span data-stu-id="ccc81-257">In the **Choose Your Data Connection** step, select the ContactManagerDB.mdf database and enter the name *ContactManagerDBEntities* for the Entity Connection Settings (see Figure 8).</span></span>
5. <span data-ttu-id="ccc81-258">在 **"选择数据库对象**"步骤中，选择标记为表的复选框（参见图 9）。</span><span class="sxs-lookup"><span data-stu-id="ccc81-258">In the **Choose Your Database Objects** step, select the checkbox labeled Tables (see Figure 9).</span></span> <span data-ttu-id="ccc81-259">数据模型将包括数据库中包含的所有表（只有一个，"联系人"表）。</span><span class="sxs-lookup"><span data-stu-id="ccc81-259">The data model will include all tables contained in your database (there is just one, the Contacts table).</span></span> <span data-ttu-id="ccc81-260">输入命名空间*模型*。</span><span class="sxs-lookup"><span data-stu-id="ccc81-260">Enter the namespace *Models*.</span></span> <span data-ttu-id="ccc81-261">单击"完成"按钮以完成向导。</span><span class="sxs-lookup"><span data-stu-id="ccc81-261">Click the Finish button to complete the wizard.</span></span>

<span data-ttu-id="ccc81-262">[![“新建项目”对话框](iteration-1-create-the-application-vb/_static/image6.jpg)](iteration-1-create-the-application-vb/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="ccc81-262">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image6.jpg)](iteration-1-create-the-application-vb/_static/image11.png)</span></span>

<span data-ttu-id="ccc81-263">**图 06**： 添加新项目对话框 （[单击以查看全尺寸图像](iteration-1-create-the-application-vb/_static/image12.png)）</span><span class="sxs-lookup"><span data-stu-id="ccc81-263">**Figure 06**: The Add New Item dialog ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image12.png))</span></span>

<span data-ttu-id="ccc81-264">[![“新建项目”对话框](iteration-1-create-the-application-vb/_static/image7.jpg)](iteration-1-create-the-application-vb/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="ccc81-264">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image7.jpg)](iteration-1-create-the-application-vb/_static/image13.png)</span></span>

<span data-ttu-id="ccc81-265">**图 07**： 选择模型内容 （[单击以查看全尺寸图像](iteration-1-create-the-application-vb/_static/image14.png)）</span><span class="sxs-lookup"><span data-stu-id="ccc81-265">**Figure 07**: Choose Model Contents ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image14.png))</span></span>

<span data-ttu-id="ccc81-266">[![“新建项目”对话框](iteration-1-create-the-application-vb/_static/image8.jpg)](iteration-1-create-the-application-vb/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="ccc81-266">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image8.jpg)](iteration-1-create-the-application-vb/_static/image15.png)</span></span>

<span data-ttu-id="ccc81-267">**图 08**： 选择您的数据连接 （[单击以查看全尺寸图像](iteration-1-create-the-application-vb/_static/image16.png)）</span><span class="sxs-lookup"><span data-stu-id="ccc81-267">**Figure 08**: Choose Your Data Connection ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image16.png))</span></span>

<span data-ttu-id="ccc81-268">[![“新建项目”对话框](iteration-1-create-the-application-vb/_static/image9.jpg)](iteration-1-create-the-application-vb/_static/image17.png)</span><span class="sxs-lookup"><span data-stu-id="ccc81-268">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image9.jpg)](iteration-1-create-the-application-vb/_static/image17.png)</span></span>

<span data-ttu-id="ccc81-269">**图 09**： 选择数据库对象 （[单击以查看全尺寸图像](iteration-1-create-the-application-vb/_static/image18.png)）</span><span class="sxs-lookup"><span data-stu-id="ccc81-269">**Figure 09**: Choose Your Database Objects ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image18.png))</span></span>

<span data-ttu-id="ccc81-270">完成实体数据模型向导后，将显示实体数据模型设计器。</span><span class="sxs-lookup"><span data-stu-id="ccc81-270">After you complete the Entity Data Model Wizard, the Entity Data Model Designer appears.</span></span> <span data-ttu-id="ccc81-271">设计器显示与要建模的每个表对应的类。</span><span class="sxs-lookup"><span data-stu-id="ccc81-271">The designer displays a class that corresponds to each table being modeled.</span></span> <span data-ttu-id="ccc81-272">您应该会看到一个名为"联系人"的类。</span><span class="sxs-lookup"><span data-stu-id="ccc81-272">You should see one class named Contacts.</span></span>

<span data-ttu-id="ccc81-273">实体数据模型向导基于数据库表名称生成类名称。</span><span class="sxs-lookup"><span data-stu-id="ccc81-273">The Entity Data Model wizard generates class names based on database table names.</span></span> <span data-ttu-id="ccc81-274">您几乎总是需要更改向导生成的类的名称。</span><span class="sxs-lookup"><span data-stu-id="ccc81-274">You almost always need to change the name of the class generated by the wizard.</span></span> <span data-ttu-id="ccc81-275">右键单击设计器中的"联系人"类，然后选择菜单选项 **"重命名**"。</span><span class="sxs-lookup"><span data-stu-id="ccc81-275">Right-click the Contacts class in the designer and select the menu option **Rename**.</span></span> <span data-ttu-id="ccc81-276">将类的名称从"联系人"（复数）更改为"联系人"（单数）。</span><span class="sxs-lookup"><span data-stu-id="ccc81-276">Change the name of the class from Contacts (plural) to Contact (singular).</span></span> <span data-ttu-id="ccc81-277">更改类名称后，类应如下所示 10。</span><span class="sxs-lookup"><span data-stu-id="ccc81-277">After you change the class name, the class should appear like Figure 10.</span></span>

<span data-ttu-id="ccc81-278">[![“新建项目”对话框](iteration-1-create-the-application-vb/_static/image10.jpg)](iteration-1-create-the-application-vb/_static/image19.png)</span><span class="sxs-lookup"><span data-stu-id="ccc81-278">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image10.jpg)](iteration-1-create-the-application-vb/_static/image19.png)</span></span>

<span data-ttu-id="ccc81-279">**图10**： 联系人类 （[单击以查看全尺寸图像](iteration-1-create-the-application-vb/_static/image20.png)）</span><span class="sxs-lookup"><span data-stu-id="ccc81-279">**Figure 10**: The Contact class ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image20.png))</span></span>

<span data-ttu-id="ccc81-280">此时，我们创建了数据库模型。</span><span class="sxs-lookup"><span data-stu-id="ccc81-280">At this point, we have created our database model.</span></span> <span data-ttu-id="ccc81-281">我们可以使用 Contact 类来表示数据库中的特定联系人记录。</span><span class="sxs-lookup"><span data-stu-id="ccc81-281">We can use the Contact class to represent a particular contact record in our database.</span></span>

## <a name="creating-the-home-controller"></a><span data-ttu-id="ccc81-282">创建主控制器</span><span class="sxs-lookup"><span data-stu-id="ccc81-282">Creating the Home Controller</span></span>

<span data-ttu-id="ccc81-283">下一步是创建我们的主控制器。</span><span class="sxs-lookup"><span data-stu-id="ccc81-283">The next step is to create our Home controller.</span></span> <span data-ttu-id="ccc81-284">主控制器是在 mVC 应用程序中调用的默认控制器ASP.NET。</span><span class="sxs-lookup"><span data-stu-id="ccc81-284">The Home controller is the default controller invoked in an ASP.NET MVC application.</span></span>

<span data-ttu-id="ccc81-285">通过右键单击解决方案资源管理器窗口中的控制器文件夹并选择菜单选项 **"添加，控制器**"（参见图 11），创建主控制器类。</span><span class="sxs-lookup"><span data-stu-id="ccc81-285">Create the Home controller class by right-clicking the Controllers folder in the Solution Explorer window and selecting the menu option **Add, Controller** (see Figure 11).</span></span> <span data-ttu-id="ccc81-286">请注意，标记为"**添加创建、更新和详细信息方案"操作方法的**复选框。</span><span class="sxs-lookup"><span data-stu-id="ccc81-286">Notice the checkbox labeled **Add action methods for Create, Update, and Details scenarios**.</span></span> <span data-ttu-id="ccc81-287">在单击"**添加**"按钮之前，请确保选中此复选框。</span><span class="sxs-lookup"><span data-stu-id="ccc81-287">Make sure that this checkbox is checked before clicking the **Add** button.</span></span>

<span data-ttu-id="ccc81-288">[![“新建项目”对话框](iteration-1-create-the-application-vb/_static/image11.jpg)](iteration-1-create-the-application-vb/_static/image21.png)</span><span class="sxs-lookup"><span data-stu-id="ccc81-288">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image11.jpg)](iteration-1-create-the-application-vb/_static/image21.png)</span></span>

<span data-ttu-id="ccc81-289">**图11**： 添加主控制器 （[单击以查看全尺寸图像](iteration-1-create-the-application-vb/_static/image22.png)）</span><span class="sxs-lookup"><span data-stu-id="ccc81-289">**Figure 11**: Adding the Home controller ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image22.png))</span></span>

<span data-ttu-id="ccc81-290">创建主控制器时，您将获得清单 1 中的类。</span><span class="sxs-lookup"><span data-stu-id="ccc81-290">When you create the Home controller, you get the class in Listing 1.</span></span>

<span data-ttu-id="ccc81-291">**清单1 - 控制器\主控制器.vb**</span><span class="sxs-lookup"><span data-stu-id="ccc81-291">**Listing 1 - Controllers\HomeController.vb**</span></span>

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample1.vb)]

## <a name="listing-the-contacts"></a><span data-ttu-id="ccc81-292">列出联系人</span><span class="sxs-lookup"><span data-stu-id="ccc81-292">Listing the Contacts</span></span>

<span data-ttu-id="ccc81-293">为了在"联系人"数据库表中显示记录，我们需要创建一个索引（） 操作和索引视图。</span><span class="sxs-lookup"><span data-stu-id="ccc81-293">In order to display the records in the Contacts database table, we need to create an Index() action and an Index view.</span></span>

<span data-ttu-id="ccc81-294">主控制器已包含索引（） 操作。</span><span class="sxs-lookup"><span data-stu-id="ccc81-294">The Home controller already contains an Index() action.</span></span> <span data-ttu-id="ccc81-295">我们需要修改此方法，以便它看起来像清单 2。</span><span class="sxs-lookup"><span data-stu-id="ccc81-295">We need to modify this method so that it looks like Listing 2.</span></span>

<span data-ttu-id="ccc81-296">**清单2 - 控制器\主控制器.vb**</span><span class="sxs-lookup"><span data-stu-id="ccc81-296">**Listing 2 - Controllers\HomeController.vb**</span></span>

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample2.vb)]

<span data-ttu-id="ccc81-297">请注意，清单 2 中的主控制器类包含名为\_实体的专用字段。</span><span class="sxs-lookup"><span data-stu-id="ccc81-297">Notice that the Home controller class in Listing 2 contains a private field named \_entities.</span></span> <span data-ttu-id="ccc81-298">实体\_字段表示数据模型中的实体。</span><span class="sxs-lookup"><span data-stu-id="ccc81-298">The \_entities field represents the entities from the data model.</span></span> <span data-ttu-id="ccc81-299">我们使用\_实体字段与数据库通信。</span><span class="sxs-lookup"><span data-stu-id="ccc81-299">We use the \_entities field to communicate with the database.</span></span>

<span data-ttu-id="ccc81-300">Index（） 方法返回表示联系人数据库表中的所有联系人的视图。</span><span class="sxs-lookup"><span data-stu-id="ccc81-300">The Index() method returns a view that represents all of the contacts from the Contacts database table.</span></span> <span data-ttu-id="ccc81-301">表达式\_实体。联系人集.ToList（） 将联系人列表作为通用列表返回。</span><span class="sxs-lookup"><span data-stu-id="ccc81-301">The expression \_entities.ContactSet.ToList() returns the list of contacts as a generic list.</span></span>

<span data-ttu-id="ccc81-302">现在，我们已经创建了索引控制器，接下来我们需要创建索引视图。</span><span class="sxs-lookup"><span data-stu-id="ccc81-302">Now that we ve created the Index controller, we next need to create the Index view.</span></span> <span data-ttu-id="ccc81-303">在创建索引视图之前，请通过选择菜单选项 **"生成、生成解决方案**"来编译应用程序。</span><span class="sxs-lookup"><span data-stu-id="ccc81-303">Before creating the Index view, compile your application by selecting the menu option **Build, Build Solution**.</span></span> <span data-ttu-id="ccc81-304">在添加视图之前，应始终编译项目，以便在 **"添加视图**"对话框中显示模型类列表。</span><span class="sxs-lookup"><span data-stu-id="ccc81-304">You should always compile your project before adding a view in order for the list of model classes to be displayed in the **Add View** dialog.</span></span>

<span data-ttu-id="ccc81-305">通过右键单击 Index（） 方法并选择菜单选项 **"添加视图**"来创建索引视图（请参见图 12）。</span><span class="sxs-lookup"><span data-stu-id="ccc81-305">You create the Index view by right-clicking the Index() method and selecting the menu option **Add View** (see Figure 12).</span></span> <span data-ttu-id="ccc81-306">选择此菜单选项将打开 **"添加视图"** 对话框（参见图 13）。</span><span class="sxs-lookup"><span data-stu-id="ccc81-306">Selecting this menu option opens the **Add View** dialog (see Figure 13).</span></span>

<span data-ttu-id="ccc81-307">[![“新建项目”对话框](iteration-1-create-the-application-vb/_static/image12.jpg)](iteration-1-create-the-application-vb/_static/image23.png)</span><span class="sxs-lookup"><span data-stu-id="ccc81-307">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image12.jpg)](iteration-1-create-the-application-vb/_static/image23.png)</span></span>

<span data-ttu-id="ccc81-308">**图 12**： 添加索引视图 （[单击以查看全尺寸图像](iteration-1-create-the-application-vb/_static/image24.png)）</span><span class="sxs-lookup"><span data-stu-id="ccc81-308">**Figure 12**: Adding the Index view ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image24.png))</span></span>

<span data-ttu-id="ccc81-309">在 **"添加视图"** 对话框中，选中标记为"**创建强类型视图"复选框**。</span><span class="sxs-lookup"><span data-stu-id="ccc81-309">In the **Add View** dialog, check the checkbox labeled **Create a strongly-typed view**.</span></span> <span data-ttu-id="ccc81-310">选择"查看数据类联系人管理器.联系人"和"查看内容列表"。</span><span class="sxs-lookup"><span data-stu-id="ccc81-310">Select the View data class ContactManager.Contact and the View content List.</span></span> <span data-ttu-id="ccc81-311">选择这些选项将生成显示联系人记录列表的视图。</span><span class="sxs-lookup"><span data-stu-id="ccc81-311">Selecting these options generates a view that displays a list of Contact records.</span></span>

<span data-ttu-id="ccc81-312">[![“新建项目”对话框](iteration-1-create-the-application-vb/_static/image13.jpg)](iteration-1-create-the-application-vb/_static/image25.png)</span><span class="sxs-lookup"><span data-stu-id="ccc81-312">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image13.jpg)](iteration-1-create-the-application-vb/_static/image25.png)</span></span>

<span data-ttu-id="ccc81-313">**图 13**： 添加视图对话框 （[单击以查看全尺寸图像](iteration-1-create-the-application-vb/_static/image26.png)）</span><span class="sxs-lookup"><span data-stu-id="ccc81-313">**Figure 13**: The Add View dialog ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image26.png))</span></span>

<span data-ttu-id="ccc81-314">单击"**添加**"按钮时，将生成清单 3 中的索引视图。</span><span class="sxs-lookup"><span data-stu-id="ccc81-314">When you click the **Add** button, the Index view in Listing 3 is generated.</span></span> <span data-ttu-id="ccc81-315">请注意&lt;显示在文件顶部的&gt;%@ 页 % 指令。</span><span class="sxs-lookup"><span data-stu-id="ccc81-315">Notice the &lt;%@ Page %&gt; directive that appears at the top of the file.</span></span> <span data-ttu-id="ccc81-316">&lt;索引视图从 ViewPage IE500"&lt;联系人管理器.模型.联系人&gt;&gt;类继承。</span><span class="sxs-lookup"><span data-stu-id="ccc81-316">The Index view inherits from the ViewPage&lt;IEnumerable&lt;ContactManager.Models.Contact&gt;&gt; class.</span></span> <span data-ttu-id="ccc81-317">换句话说，视图中的 Model 类表示联系人实体的列表。</span><span class="sxs-lookup"><span data-stu-id="ccc81-317">In other words, the Model class in the view represents a list of Contact entities.</span></span>

<span data-ttu-id="ccc81-318">Index 视图的正文包含一个 foreach 循环，该循环通过模型类表示的每个联系人进行循环。</span><span class="sxs-lookup"><span data-stu-id="ccc81-318">The body of the Index view contains a foreach loop that iterates through each of the contacts represented by the Model class.</span></span> <span data-ttu-id="ccc81-319">Contact 类的每个属性的值显示在 HTML 表中。</span><span class="sxs-lookup"><span data-stu-id="ccc81-319">The value of each property of the Contact class is displayed within an HTML table.</span></span>

<span data-ttu-id="ccc81-320">**清单 3 - 视图\home_Index.aspx（未修改）**</span><span class="sxs-lookup"><span data-stu-id="ccc81-320">**Listing 3 - Views\Home\Index.aspx (unmodified)**</span></span>

[!code-aspx[Main](iteration-1-create-the-application-vb/samples/sample3.aspx)]

<span data-ttu-id="ccc81-321">我们需要对索引视图进行一次修改。</span><span class="sxs-lookup"><span data-stu-id="ccc81-321">We need to make one modification to the Index view.</span></span> <span data-ttu-id="ccc81-322">由于我们不是在创建"详细信息"视图，因此我们可以删除"详细信息"链接。</span><span class="sxs-lookup"><span data-stu-id="ccc81-322">Because we are not creating a Details view, we can remove the Details link.</span></span> <span data-ttu-id="ccc81-323">从索引视图查找和删除以下代码：</span><span class="sxs-lookup"><span data-stu-id="ccc81-323">Find and remove the following code from the Index view:</span></span>

<span data-ttu-id="ccc81-324">{.id = 项。Id=）%&gt;</span><span class="sxs-lookup"><span data-stu-id="ccc81-324">{.id = item.Id})%&gt;</span></span>

<span data-ttu-id="ccc81-325">修改索引视图后，可以运行联系人管理器应用程序。</span><span class="sxs-lookup"><span data-stu-id="ccc81-325">After you modify the Index view, you can run the Contact Manager application.</span></span> <span data-ttu-id="ccc81-326">选择菜单选项"调试"、"开始调试"或"按 F5"。</span><span class="sxs-lookup"><span data-stu-id="ccc81-326">Select the menu option Debug, Start Debugging or simply press F5.</span></span> <span data-ttu-id="ccc81-327">首次运行应用程序时，您将获得图 14 中的对话框。</span><span class="sxs-lookup"><span data-stu-id="ccc81-327">The first time you run the application, you get the dialog in Figure 14.</span></span> <span data-ttu-id="ccc81-328">选择 **"修改 Web.config 文件以启用调试**"选项，然后单击"确定"按钮。</span><span class="sxs-lookup"><span data-stu-id="ccc81-328">Select the option **Modify the Web.config file to enable debugging** and click the OK button.</span></span>

<span data-ttu-id="ccc81-329">[![“新建项目”对话框](iteration-1-create-the-application-vb/_static/image14.jpg)](iteration-1-create-the-application-vb/_static/image27.png)</span><span class="sxs-lookup"><span data-stu-id="ccc81-329">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image14.jpg)](iteration-1-create-the-application-vb/_static/image27.png)</span></span>

<span data-ttu-id="ccc81-330">**图14**：启用调试 （[单击以查看全尺寸图像](iteration-1-create-the-application-vb/_static/image28.png)）</span><span class="sxs-lookup"><span data-stu-id="ccc81-330">**Figure 14**: Enabling debugging ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image28.png))</span></span>

<span data-ttu-id="ccc81-331">默认情况下，将返回索引视图。</span><span class="sxs-lookup"><span data-stu-id="ccc81-331">The Index view is returned by default.</span></span> <span data-ttu-id="ccc81-332">此视图列出联系人数据库表中的所有数据（参见图 15）。</span><span class="sxs-lookup"><span data-stu-id="ccc81-332">This view lists all of the data from the Contacts database table (see Figure 15).</span></span>

<span data-ttu-id="ccc81-333">[![“新建项目”对话框](iteration-1-create-the-application-vb/_static/image15.jpg)](iteration-1-create-the-application-vb/_static/image29.png)</span><span class="sxs-lookup"><span data-stu-id="ccc81-333">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image15.jpg)](iteration-1-create-the-application-vb/_static/image29.png)</span></span>

<span data-ttu-id="ccc81-334">**图 15**： 索引视图 （[单击以查看全尺寸图像](iteration-1-create-the-application-vb/_static/image30.png)）</span><span class="sxs-lookup"><span data-stu-id="ccc81-334">**Figure 15**: The Index view ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image30.png))</span></span>

<span data-ttu-id="ccc81-335">请注意，索引视图在视图底部包含标记为"新建"的链接。</span><span class="sxs-lookup"><span data-stu-id="ccc81-335">Notice that the Index view includes a link labeled Create New at the bottom of the view.</span></span> <span data-ttu-id="ccc81-336">在下一节中，您将了解如何创建新联系人。</span><span class="sxs-lookup"><span data-stu-id="ccc81-336">In the next section, you learn how to create new contacts.</span></span>

## <a name="creating-new-contacts"></a><span data-ttu-id="ccc81-337">创建新联系人</span><span class="sxs-lookup"><span data-stu-id="ccc81-337">Creating New Contacts</span></span>

<span data-ttu-id="ccc81-338">为了使用户能够创建新的联系人，我们需要向主控制器添加两个 Create（） 操作。</span><span class="sxs-lookup"><span data-stu-id="ccc81-338">To enable users to create new contacts, we need to add two Create() actions to the Home controller.</span></span> <span data-ttu-id="ccc81-339">我们需要创建一个 Create（） 操作，该操作返回 HTML 表单以创建新联系人。</span><span class="sxs-lookup"><span data-stu-id="ccc81-339">We need to create one Create() action that returns an HTML form for creating a new contact.</span></span> <span data-ttu-id="ccc81-340">我们需要创建第二个 Create（） 操作，以执行新联系人的实际数据库插入。</span><span class="sxs-lookup"><span data-stu-id="ccc81-340">We need to create a second Create() action that performs the actual database insert of the new contact.</span></span>

<span data-ttu-id="ccc81-341">我们需要添加到主控制器的新 Create（） 方法包含在清单 4 中。</span><span class="sxs-lookup"><span data-stu-id="ccc81-341">The new Create() methods that we need to add to the Home controller are contained in Listing 4.</span></span>

<span data-ttu-id="ccc81-342">**清单4 - 控制器\homeController.vb（使用创建方法）**</span><span class="sxs-lookup"><span data-stu-id="ccc81-342">**Listing 4 - Controllers\HomeController.vb (with Create methods)**</span></span>

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample4.vb)]

<span data-ttu-id="ccc81-343">第一个 Create（） 方法可以使用 HTTP GET 调用，而第二个 Create（） 方法只能由 HTTP POST 调用。</span><span class="sxs-lookup"><span data-stu-id="ccc81-343">The first Create() method can be invoked with an HTTP GET while the second Create() method can be invoked only by an HTTP POST.</span></span> <span data-ttu-id="ccc81-344">换句话说，第二个 Create（） 方法只能在发布 HTML 窗体时调用。</span><span class="sxs-lookup"><span data-stu-id="ccc81-344">In other words, the second Create() method can be invoked only when posting an HTML form.</span></span> <span data-ttu-id="ccc81-345">第一个 Create（） 方法仅返回包含用于创建新联系人的 HTML 窗体的视图。</span><span class="sxs-lookup"><span data-stu-id="ccc81-345">The first Create() method simply returns a view that contains the HTML form for creating a new contact.</span></span> <span data-ttu-id="ccc81-346">第二个 Create（） 方法更有趣：它将新的联系人添加到数据库中。</span><span class="sxs-lookup"><span data-stu-id="ccc81-346">The second Create() method is much more interesting: it adds the new contact to the database.</span></span>

<span data-ttu-id="ccc81-347">请注意，已修改第二个 Create（） 方法以接受 Contact 类的实例。</span><span class="sxs-lookup"><span data-stu-id="ccc81-347">Notice that the second Create() method has been modified to accept an instance of the Contact class.</span></span> <span data-ttu-id="ccc81-348">从 HTML 窗体发布的表单值由 ASP.NET MVC 框架自动绑定到此 Contact 类。</span><span class="sxs-lookup"><span data-stu-id="ccc81-348">The form values posted from the HTML form are bound to this Contact class by the ASP.NET MVC framework automatically.</span></span> <span data-ttu-id="ccc81-349">HTML 创建窗体中的每个窗体字段都分配给"联系人"参数的属性。</span><span class="sxs-lookup"><span data-stu-id="ccc81-349">Each form field from the HTML Create form is assigned to a property of the Contact parameter.</span></span>

<span data-ttu-id="ccc81-350">请注意，联系人参数用 [Bind] 属性进行修饰。</span><span class="sxs-lookup"><span data-stu-id="ccc81-350">Notice that the Contact parameter is decorated with a [Bind] attribute.</span></span> <span data-ttu-id="ccc81-351">[绑定] 属性用于从绑定中排除联系人 Id 属性。</span><span class="sxs-lookup"><span data-stu-id="ccc81-351">The [Bind] attribute is used to exclude the Contact Id property from binding.</span></span> <span data-ttu-id="ccc81-352">由于 Id 属性表示标识属性，因此我们不希望设置 Id 属性。</span><span class="sxs-lookup"><span data-stu-id="ccc81-352">Because the Id property represents an Identity property, we don t want to set the Id property.</span></span>

<span data-ttu-id="ccc81-353">在 Create（） 方法的正文中，实体框架用于将新的联系人插入到数据库中。</span><span class="sxs-lookup"><span data-stu-id="ccc81-353">In the body of the Create() method, the Entity Framework is used to insert the new Contact into the database.</span></span> <span data-ttu-id="ccc81-354">新的联系人将添加到现有的联系人集，并调用 SaveChanges（） 方法将这些更改推送回基础数据库。</span><span class="sxs-lookup"><span data-stu-id="ccc81-354">The new Contact is added to the existing set of Contacts and the SaveChanges() method is called to push these changes back to the underlying database.</span></span>

<span data-ttu-id="ccc81-355">您可以通过右键单击两个 Create（） 方法之一并选择菜单选项 **"添加视图**"来生成用于创建新联系人的 HTML 表单（参见图 16）。</span><span class="sxs-lookup"><span data-stu-id="ccc81-355">You can generate an HTML form for creating new Contacts by right-clicking either of the two Create() methods and selecting the menu option **Add View** (see Figure 16).</span></span>

<span data-ttu-id="ccc81-356">[![“新建项目”对话框](iteration-1-create-the-application-vb/_static/image16.jpg)](iteration-1-create-the-application-vb/_static/image31.png)</span><span class="sxs-lookup"><span data-stu-id="ccc81-356">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image16.jpg)](iteration-1-create-the-application-vb/_static/image31.png)</span></span>

<span data-ttu-id="ccc81-357">**图 16**： 添加创建视图 （[单击以查看全尺寸图像](iteration-1-create-the-application-vb/_static/image32.png)）</span><span class="sxs-lookup"><span data-stu-id="ccc81-357">**Figure 16**: Adding the Create view ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image32.png))</span></span>

<span data-ttu-id="ccc81-358">在 **"添加视图"** 对话框中，选择 **"联系人管理器.联系人"** 类和"创建视图内容 **"** 选项（参见图 17）。</span><span class="sxs-lookup"><span data-stu-id="ccc81-358">In the **Add View** dialog, select the **ContactManager.Contact** class and the **Create** option for view content (see Figure 17).</span></span> <span data-ttu-id="ccc81-359">单击"**添加**"按钮时，将自动生成"创建"视图。</span><span class="sxs-lookup"><span data-stu-id="ccc81-359">When you click the **Add** button, a Create view is generated automatically.</span></span>

<span data-ttu-id="ccc81-360">[![“新建项目”对话框](iteration-1-create-the-application-vb/_static/image17.jpg)](iteration-1-create-the-application-vb/_static/image33.png)</span><span class="sxs-lookup"><span data-stu-id="ccc81-360">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image17.jpg)](iteration-1-create-the-application-vb/_static/image33.png)</span></span>

<span data-ttu-id="ccc81-361">**图17**： 看到页面爆炸 （[单击以查看全尺寸图像](iteration-1-create-the-application-vb/_static/image34.png)）</span><span class="sxs-lookup"><span data-stu-id="ccc81-361">**Figure 17**: Seeing a page explode ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image34.png))</span></span>

<span data-ttu-id="ccc81-362">"创建"视图包含 Contact 类的每个属性的表单字段。</span><span class="sxs-lookup"><span data-stu-id="ccc81-362">The Create view contains form fields for each of the properties of the Contact class.</span></span> <span data-ttu-id="ccc81-363">"创建"视图的代码包含在清单 5 中。</span><span class="sxs-lookup"><span data-stu-id="ccc81-363">The code for the Create view is included in Listing 5.</span></span>

<span data-ttu-id="ccc81-364">**清单 5 - 视图\home_Create.aspx**</span><span class="sxs-lookup"><span data-stu-id="ccc81-364">**Listing 5 - Views\Home\Create.aspx**</span></span>

[!code-aspx[Main](iteration-1-create-the-application-vb/samples/sample5.aspx)]

<span data-ttu-id="ccc81-365">修改 Create（） 方法并添加"创建"视图后，可以运行联系人经理应用程序并创建新联系人。</span><span class="sxs-lookup"><span data-stu-id="ccc81-365">After you modify the Create() methods and add the Create view, you can run the Contact Manger application and create new contacts.</span></span> <span data-ttu-id="ccc81-366">单击"**新建**"视图中显示的链接以导航到"创建"视图。</span><span class="sxs-lookup"><span data-stu-id="ccc81-366">Click the **Create New** link that appears in the Index view to navigate to the Create view.</span></span> <span data-ttu-id="ccc81-367">您应该在图 18 中看到视图。</span><span class="sxs-lookup"><span data-stu-id="ccc81-367">You should see the view in Figure 18.</span></span>

<span data-ttu-id="ccc81-368">[![“新建项目”对话框](iteration-1-create-the-application-vb/_static/image18.jpg)](iteration-1-create-the-application-vb/_static/image35.png)</span><span class="sxs-lookup"><span data-stu-id="ccc81-368">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image18.jpg)](iteration-1-create-the-application-vb/_static/image35.png)</span></span>

<span data-ttu-id="ccc81-369">**图 18**： 创建视图 （[单击以查看全尺寸图像](iteration-1-create-the-application-vb/_static/image36.png)）</span><span class="sxs-lookup"><span data-stu-id="ccc81-369">**Figure 18**: The Create View ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image36.png))</span></span>

## <a name="editing-contacts"></a><span data-ttu-id="ccc81-370">编辑联系人</span><span class="sxs-lookup"><span data-stu-id="ccc81-370">Editing Contacts</span></span>

<span data-ttu-id="ccc81-371">添加用于编辑联系人记录的功能与添加创建新联系人记录的功能非常相似。</span><span class="sxs-lookup"><span data-stu-id="ccc81-371">Adding the functionality for editing a contact record is very similar to adding the functionality for creating new contact records.</span></span> <span data-ttu-id="ccc81-372">首先，我们需要向主控制器类添加两种新的 Edit 方法。</span><span class="sxs-lookup"><span data-stu-id="ccc81-372">First, we need to add two new Edit methods to the Home controller class.</span></span> <span data-ttu-id="ccc81-373">这些新的 Edit（） 方法包含在清单 6 中。</span><span class="sxs-lookup"><span data-stu-id="ccc81-373">These new Edit() methods are contained in Listing 6.</span></span>

<span data-ttu-id="ccc81-374">**清单6 - 控制器\主控制器.vb（使用编辑方法）**</span><span class="sxs-lookup"><span data-stu-id="ccc81-374">**Listing 6 - Controllers\HomeController.vb (with Edit methods)**</span></span>

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample6.vb)]

<span data-ttu-id="ccc81-375">第一个 Edit（） 方法由 HTTP GET 操作调用。</span><span class="sxs-lookup"><span data-stu-id="ccc81-375">The first Edit() method is invoked by an HTTP GET operation.</span></span> <span data-ttu-id="ccc81-376">Id 参数传递给此方法，此方法表示要编辑的联系人记录的 ID。</span><span class="sxs-lookup"><span data-stu-id="ccc81-376">An Id parameter is passed to this method which represents the Id of the contact record being edited.</span></span> <span data-ttu-id="ccc81-377">实体框架用于检索与 Id 匹配的联系人。返回包含用于编辑记录的 HTML 窗体的视图。</span><span class="sxs-lookup"><span data-stu-id="ccc81-377">The Entity Framework is used to retrieve a contact that matches the Id. A view that contains an HTML form for editing a record is returned.</span></span>

<span data-ttu-id="ccc81-378">第二个 Edit（） 方法执行对数据库的实际更新。</span><span class="sxs-lookup"><span data-stu-id="ccc81-378">The second Edit() method performs the actual update to the database.</span></span> <span data-ttu-id="ccc81-379">此方法接受 Contact 类的实例作为参数。</span><span class="sxs-lookup"><span data-stu-id="ccc81-379">This method accepts an instance of the Contact class as a parameter.</span></span> <span data-ttu-id="ccc81-380">ASP.NET MVC 框架会自动将表单字段从"编辑"窗体绑定到此类。</span><span class="sxs-lookup"><span data-stu-id="ccc81-380">The ASP.NET MVC framework binds the form fields from the Edit form to this class automatically.</span></span> <span data-ttu-id="ccc81-381">请注意，在编辑联系人时，您没有包含 [Bind] 属性（我们需要 Id 属性的值）。</span><span class="sxs-lookup"><span data-stu-id="ccc81-381">Notice that you don t include the[Bind] attribute when editing a Contact (we need the value of the Id property).</span></span>

<span data-ttu-id="ccc81-382">实体框架用于将修改后的联系人保存到数据库。</span><span class="sxs-lookup"><span data-stu-id="ccc81-382">The Entity Framework is used to save the modified Contact to the database.</span></span> <span data-ttu-id="ccc81-383">必须首先从数据库中检索原始联系人。</span><span class="sxs-lookup"><span data-stu-id="ccc81-383">The original Contact must be retrieved from the database first.</span></span> <span data-ttu-id="ccc81-384">接下来，调用实体框架应用属性更改（） 方法来记录对联系人的更改。</span><span class="sxs-lookup"><span data-stu-id="ccc81-384">Next, the Entity Framework ApplyPropertyChanges() method is called to record the changes to the Contact.</span></span> <span data-ttu-id="ccc81-385">最后，调用实体框架保存更改（） 方法来保留对基础数据库的更改。</span><span class="sxs-lookup"><span data-stu-id="ccc81-385">Finally, the Entity Framework SaveChanges() method is called to persist the changes to the underlying database.</span></span>

<span data-ttu-id="ccc81-386">您可以通过右键单击 Edit（） 方法并选择菜单选项"添加视图"来生成包含"编辑"窗体的视图。</span><span class="sxs-lookup"><span data-stu-id="ccc81-386">You can generate the view that contains the Edit form by right-clicking the Edit() method and selecting the menu option Add View.</span></span> <span data-ttu-id="ccc81-387">在"添加视图"对话框中，选择 **"联系人管理器.模型.联系人类"** 和 **"编辑**视图"内容（参见图 19）。</span><span class="sxs-lookup"><span data-stu-id="ccc81-387">In the Add View dialog, select the **ContactManager.Models.Contact** class and the **Edit** view content (see Figure 19).</span></span>

<span data-ttu-id="ccc81-388">[![“新建项目”对话框](iteration-1-create-the-application-vb/_static/image19.jpg)](iteration-1-create-the-application-vb/_static/image37.png)</span><span class="sxs-lookup"><span data-stu-id="ccc81-388">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image19.jpg)](iteration-1-create-the-application-vb/_static/image37.png)</span></span>

<span data-ttu-id="ccc81-389">**图 19**： 添加编辑视图 （[单击以查看全尺寸图像](iteration-1-create-the-application-vb/_static/image38.png)）</span><span class="sxs-lookup"><span data-stu-id="ccc81-389">**Figure 19**: Adding an Edit View ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image38.png))</span></span>

<span data-ttu-id="ccc81-390">单击"添加"按钮时，将自动生成新的"编辑"视图。</span><span class="sxs-lookup"><span data-stu-id="ccc81-390">When you click the Add button, a new Edit view is generated automatically.</span></span> <span data-ttu-id="ccc81-391">生成的 HTML 窗体包含对应于 Contact 类的每个属性的字段（请参见清单 7）。</span><span class="sxs-lookup"><span data-stu-id="ccc81-391">The HTML form that is generated contains fields that correspond to each of the properties of the Contact class (see Listing 7).</span></span>

<span data-ttu-id="ccc81-392">**清单7 - 视图\home_编辑.aspx**</span><span class="sxs-lookup"><span data-stu-id="ccc81-392">**Listing 7 - Views\Home\Edit.aspx**</span></span>

[!code-aspx[Main](iteration-1-create-the-application-vb/samples/sample7.aspx)]

## <a name="deleting-contacts"></a><span data-ttu-id="ccc81-393">删除联系人</span><span class="sxs-lookup"><span data-stu-id="ccc81-393">Deleting Contacts</span></span>

<span data-ttu-id="ccc81-394">如果要删除联系人，则需要向主控制器类添加两个 Delete（） 操作。</span><span class="sxs-lookup"><span data-stu-id="ccc81-394">If you want to delete contacts then you need to add two Delete() actions to the Home controller class.</span></span> <span data-ttu-id="ccc81-395">第一个删除（） 操作显示删除确认表单。</span><span class="sxs-lookup"><span data-stu-id="ccc81-395">The first Delete() action displays a delete confirmation form.</span></span> <span data-ttu-id="ccc81-396">第二个 Delete（） 操作执行实际删除。</span><span class="sxs-lookup"><span data-stu-id="ccc81-396">The second Delete() action performs the actual delete.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="ccc81-397">稍后，在迭代#7中，我们修改联系人管理器，以便它支持 Ajax 删除的一个步骤。</span><span class="sxs-lookup"><span data-stu-id="ccc81-397">Later, in Iteration #7, we modify the Contact Manager so that it supports a one step Ajax delete.</span></span>

<span data-ttu-id="ccc81-398">清单8中包含两种新的 Delete（） 方法。</span><span class="sxs-lookup"><span data-stu-id="ccc81-398">The two new Delete() methods are contained in Listing 8.</span></span>

<span data-ttu-id="ccc81-399">**清单8 - 控制器\主控制器.vb（删除方法）**</span><span class="sxs-lookup"><span data-stu-id="ccc81-399">**Listing 8 - Controllers\HomeController.vb (Delete methods)**</span></span>

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample8.vb)]

<span data-ttu-id="ccc81-400">第一个 Delete（） 方法返回一个确认表单，用于从数据库中删除联系人记录（参见图 20）。</span><span class="sxs-lookup"><span data-stu-id="ccc81-400">The first Delete() method returns a confirmation form for deleting a contact record from the database (see Figure20).</span></span> <span data-ttu-id="ccc81-401">第二个 Delete（） 方法对数据库执行实际删除操作。</span><span class="sxs-lookup"><span data-stu-id="ccc81-401">The second Delete() method performs the actual delete operation against the database.</span></span> <span data-ttu-id="ccc81-402">从数据库检索原始联系人后，将调用实体框架 DeleteObject（） 和保存更改（）方法以执行数据库删除。</span><span class="sxs-lookup"><span data-stu-id="ccc81-402">After the original contact has been retrieved from the database, the Entity Framework DeleteObject() and SaveChanges() methods are called to perform the database delete.</span></span>

<span data-ttu-id="ccc81-403">[![“新建项目”对话框](iteration-1-create-the-application-vb/_static/image20.jpg)](iteration-1-create-the-application-vb/_static/image39.png)</span><span class="sxs-lookup"><span data-stu-id="ccc81-403">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image20.jpg)](iteration-1-create-the-application-vb/_static/image39.png)</span></span>

<span data-ttu-id="ccc81-404">**图20**：删除确认视图 （[单击以查看全尺寸图像](iteration-1-create-the-application-vb/_static/image40.png)）</span><span class="sxs-lookup"><span data-stu-id="ccc81-404">**Figure 20**: The delete confirmation view ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image40.png))</span></span>

<span data-ttu-id="ccc81-405">我们需要修改 Index 视图，以便它包含用于删除联系人记录的链接（参见图 21）。</span><span class="sxs-lookup"><span data-stu-id="ccc81-405">We need to modify the Index view so that it contains a link for deleting contact records (see Figure 21).</span></span> <span data-ttu-id="ccc81-406">您需要将以下代码添加到包含"编辑"链接的同一表单元格中：</span><span class="sxs-lookup"><span data-stu-id="ccc81-406">You need to add the following code to the same table cell that contains the Edit link:</span></span>

<span data-ttu-id="ccc81-407">{.id = 项。Id=）%&gt;</span><span class="sxs-lookup"><span data-stu-id="ccc81-407">{.id = item.Id})%&gt;</span></span>

<span data-ttu-id="ccc81-408">[![“新建项目”对话框](iteration-1-create-the-application-vb/_static/image21.jpg)](iteration-1-create-the-application-vb/_static/image41.png)</span><span class="sxs-lookup"><span data-stu-id="ccc81-408">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image21.jpg)](iteration-1-create-the-application-vb/_static/image41.png)</span></span>

<span data-ttu-id="ccc81-409">**图21**：索引视图与编辑链接 （[单击以查看全尺寸图像](iteration-1-create-the-application-vb/_static/image42.png)）</span><span class="sxs-lookup"><span data-stu-id="ccc81-409">**Figure 21**: Index view with Edit link ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image42.png))</span></span>

<span data-ttu-id="ccc81-410">接下来，我们需要创建删除确认视图。</span><span class="sxs-lookup"><span data-stu-id="ccc81-410">Next, we need to create the delete confirmation view.</span></span> <span data-ttu-id="ccc81-411">右键单击主控制器类中的 Delete（） 方法，然后选择菜单选项"添加视图"。</span><span class="sxs-lookup"><span data-stu-id="ccc81-411">Right-click the Delete() method in the Home controller class and select the menu option Add View.</span></span> <span data-ttu-id="ccc81-412">将显示"添加视图"对话框（参见图 22）。</span><span class="sxs-lookup"><span data-stu-id="ccc81-412">The Add View dialog appears (see Figure 22).</span></span>

<span data-ttu-id="ccc81-413">与"列表"、"创建"和"编辑"视图的情况不同，"添加视图"对话框不包含创建"删除"视图的选项。</span><span class="sxs-lookup"><span data-stu-id="ccc81-413">Unlike in the case of the List, Create, and Edit views, the Add View dialog does not contain an option to create a Delete view.</span></span> <span data-ttu-id="ccc81-414">而是选择 **"联系人管理器.模型.联系人**数据类"和 **"空**视图"内容。</span><span class="sxs-lookup"><span data-stu-id="ccc81-414">Instead, select the **ContactManager.Models.Contact** data class and the **Empty** view content.</span></span> <span data-ttu-id="ccc81-415">选择"空视图内容"选项需要我们自己创建视图。</span><span class="sxs-lookup"><span data-stu-id="ccc81-415">Selecting the Empty view content option will require us to create the view ourselves.</span></span>

<span data-ttu-id="ccc81-416">[![“新建项目”对话框](iteration-1-create-the-application-vb/_static/image22.jpg)](iteration-1-create-the-application-vb/_static/image43.png)</span><span class="sxs-lookup"><span data-stu-id="ccc81-416">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image22.jpg)](iteration-1-create-the-application-vb/_static/image43.png)</span></span>

<span data-ttu-id="ccc81-417">**图22**：添加删除确认视图 （[单击以查看全尺寸图像](iteration-1-create-the-application-vb/_static/image44.png)）</span><span class="sxs-lookup"><span data-stu-id="ccc81-417">**Figure 22**: Adding the delete confirmation view ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image44.png))</span></span>

<span data-ttu-id="ccc81-418">"删除"视图的内容包含在清单 9 中。</span><span class="sxs-lookup"><span data-stu-id="ccc81-418">The content of the Delete view is contained in Listing 9.</span></span> <span data-ttu-id="ccc81-419">此视图包含一个表单，该窗体确认是否应删除特定联系人（参见图 21）。</span><span class="sxs-lookup"><span data-stu-id="ccc81-419">This view contains a form that confirms whether or not a particular contact should be deleted (see Figure 21).</span></span>

<span data-ttu-id="ccc81-420">**清单 9 - 视图\home_Delete.aspx**</span><span class="sxs-lookup"><span data-stu-id="ccc81-420">**Listing 9 - Views\Home\Delete.aspx**</span></span>

[!code-aspx[Main](iteration-1-create-the-application-vb/samples/sample9.aspx)]

## <a name="changing-the-name-of-the-default-controller"></a><span data-ttu-id="ccc81-421">更改默认控制器的名称</span><span class="sxs-lookup"><span data-stu-id="ccc81-421">Changing the Name of the Default Controller</span></span>

<span data-ttu-id="ccc81-422">使用联系人的控制器类的名称名为 HomeController 类，这可能会让您烦恼。</span><span class="sxs-lookup"><span data-stu-id="ccc81-422">It might bother you that the name of our controller class for working with contacts is named the HomeController class.</span></span> <span data-ttu-id="ccc81-423">控制器不应被命名为"联系人控制器"？</span><span class="sxs-lookup"><span data-stu-id="ccc81-423">Shouldn't the controller be named ContactController?</span></span>

<span data-ttu-id="ccc81-424">此问题很容易解决。</span><span class="sxs-lookup"><span data-stu-id="ccc81-424">This issue is easy enough to fix.</span></span> <span data-ttu-id="ccc81-425">首先，我们需要重构主控制器的名称。</span><span class="sxs-lookup"><span data-stu-id="ccc81-425">First, we need to refactor the name of the Home controller.</span></span> <span data-ttu-id="ccc81-426">在 Visual Studio 代码编辑器中打开 HomeController 类，右键单击类的名称并选择菜单选项 **"重命名**"。</span><span class="sxs-lookup"><span data-stu-id="ccc81-426">Open the HomeController class in the Visual Studio Code Editor, right click the name of the class and select the menu option **Rename**.</span></span> <span data-ttu-id="ccc81-427">选择此菜单选项将打开"重命名"对话框。</span><span class="sxs-lookup"><span data-stu-id="ccc81-427">Selecting this menu option opens the Rename dialog.</span></span>

<span data-ttu-id="ccc81-428">[![“新建项目”对话框](iteration-1-create-the-application-vb/_static/image23.jpg)](iteration-1-create-the-application-vb/_static/image45.png)</span><span class="sxs-lookup"><span data-stu-id="ccc81-428">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image23.jpg)](iteration-1-create-the-application-vb/_static/image45.png)</span></span>

<span data-ttu-id="ccc81-429">**图23**：重构控制器名称 （[单击以查看全尺寸图像](iteration-1-create-the-application-vb/_static/image46.png)）</span><span class="sxs-lookup"><span data-stu-id="ccc81-429">**Figure 23**: Refactoring a controller name ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image46.png))</span></span>

<span data-ttu-id="ccc81-430">[![“新建项目”对话框](iteration-1-create-the-application-vb/_static/image24.jpg)](iteration-1-create-the-application-vb/_static/image47.png)</span><span class="sxs-lookup"><span data-stu-id="ccc81-430">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image24.jpg)](iteration-1-create-the-application-vb/_static/image47.png)</span></span>

<span data-ttu-id="ccc81-431">**图24**：使用重命名对话框 （[单击以查看全尺寸图像](iteration-1-create-the-application-vb/_static/image48.png)）</span><span class="sxs-lookup"><span data-stu-id="ccc81-431">**Figure 24**: Using the Rename dialog ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image48.png))</span></span>

<span data-ttu-id="ccc81-432">如果重命名控制器类，Visual Studio 也会更新"视图"文件夹中文件夹的名称。</span><span class="sxs-lookup"><span data-stu-id="ccc81-432">If you rename your controller class, Visual Studio will update the name of the folder in the Views folder as well.</span></span> <span data-ttu-id="ccc81-433">Visual Studio 会将 [视图]主页文件夹重命名为 [视图]联系人文件夹。</span><span class="sxs-lookup"><span data-stu-id="ccc81-433">Visual Studio will rename the \Views\Home folder to the \Views\Contact folder.</span></span>

<span data-ttu-id="ccc81-434">进行此更改后，应用程序将不再具有主控制器。</span><span class="sxs-lookup"><span data-stu-id="ccc81-434">After you make this change, your application will no longer have a Home controller.</span></span> <span data-ttu-id="ccc81-435">运行应用程序时，您将获得图 25 中的错误页。</span><span class="sxs-lookup"><span data-stu-id="ccc81-435">When you run your application, you'll get the error page in Figure 25.</span></span>

<span data-ttu-id="ccc81-436">[![“新建项目”对话框](iteration-1-create-the-application-vb/_static/image25.jpg)](iteration-1-create-the-application-vb/_static/image49.png)</span><span class="sxs-lookup"><span data-stu-id="ccc81-436">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image25.jpg)](iteration-1-create-the-application-vb/_static/image49.png)</span></span>

<span data-ttu-id="ccc81-437">**图25：** 无默认控制器（[单击以查看全尺寸图像](iteration-1-create-the-application-vb/_static/image50.png)）</span><span class="sxs-lookup"><span data-stu-id="ccc81-437">**Figure 25**: No default controller ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image50.png))</span></span>

<span data-ttu-id="ccc81-438">我们需要更新 Global.asax 文件中的默认路由，以便使用联系人控制器而不是主控制器。</span><span class="sxs-lookup"><span data-stu-id="ccc81-438">We need to update the default route in the Global.asax file to use the Contact controller instead of the Home controller.</span></span> <span data-ttu-id="ccc81-439">打开 Global.asax 文件并修改默认路由使用的默认控制器（请参见清单 10）。</span><span class="sxs-lookup"><span data-stu-id="ccc81-439">Open the Global.asax file and modify the default controller used by the default route (see Listing 10).</span></span>

<span data-ttu-id="ccc81-440">**清单10 - 全局.asax.vb**</span><span class="sxs-lookup"><span data-stu-id="ccc81-440">**Listing 10 - Global.asax.vb**</span></span>

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample10.vb)]

<span data-ttu-id="ccc81-441">进行这些更改后，联系人管理器将正确运行。</span><span class="sxs-lookup"><span data-stu-id="ccc81-441">After you make these changes, the Contact Manager will run correctly.</span></span> <span data-ttu-id="ccc81-442">现在，它将使用联系人控制器类作为默认控制器。</span><span class="sxs-lookup"><span data-stu-id="ccc81-442">Now, it will use the Contact controller class as the default controller.</span></span>

## <a name="summary"></a><span data-ttu-id="ccc81-443">总结</span><span class="sxs-lookup"><span data-stu-id="ccc81-443">Summary</span></span>

<span data-ttu-id="ccc81-444">在第一次迭代中，我们以尽可能快的方式创建了一个基本的联系人管理器应用程序。</span><span class="sxs-lookup"><span data-stu-id="ccc81-444">In this first iteration, we created a basic Contact Manager application in the fastest way possible.</span></span> <span data-ttu-id="ccc81-445">我们利用 Visual Studio 自动为控制器和视图生成初始代码。</span><span class="sxs-lookup"><span data-stu-id="ccc81-445">We took advantage of Visual Studio to generate the initial code for our controllers and views automatically.</span></span> <span data-ttu-id="ccc81-446">我们还利用实体框架自动生成数据库模型类。</span><span class="sxs-lookup"><span data-stu-id="ccc81-446">We also took advantage of the Entity Framework to generate our database model classes automatically.</span></span>

<span data-ttu-id="ccc81-447">目前，我们可以使用联系人管理器应用程序列出、创建、编辑和删除联系人记录。</span><span class="sxs-lookup"><span data-stu-id="ccc81-447">Currently, we can list, create, edit, and delete contact records with the Contact Manager application.</span></span> <span data-ttu-id="ccc81-448">换句话说，我们可以执行数据库驱动的 Web 应用程序所需的所有基本数据库操作。</span><span class="sxs-lookup"><span data-stu-id="ccc81-448">In other words, we can perform all of the basic database operations required by a database-driven web application.</span></span>

<span data-ttu-id="ccc81-449">不幸的是，我们的应用程序有一些问题。</span><span class="sxs-lookup"><span data-stu-id="ccc81-449">Unfortunately, our application has some problems.</span></span> <span data-ttu-id="ccc81-450">首先，我犹豫地承认这一点，联系人管理器应用程序不是最有吸引力的应用程序。</span><span class="sxs-lookup"><span data-stu-id="ccc81-450">First and I hesitate to admit this, the Contact Manager application is not the most attractive application.</span></span> <span data-ttu-id="ccc81-451">它需要一些设计工作。</span><span class="sxs-lookup"><span data-stu-id="ccc81-451">It needs some design work.</span></span> <span data-ttu-id="ccc81-452">在下一次迭代中，我们将了解如何更改默认视图母版页和级联样式表，以改善应用程序的外观。</span><span class="sxs-lookup"><span data-stu-id="ccc81-452">In the next iteration, we'll look at how we can change the default view master page and cascading style sheet to improve the appearance of the application.</span></span>

<span data-ttu-id="ccc81-453">其次，我们尚未实现任何表单验证。</span><span class="sxs-lookup"><span data-stu-id="ccc81-453">Second, we have not implemented any form validation.</span></span> <span data-ttu-id="ccc81-454">例如，没有任何措施可以阻止您提交"创建联系人表单"，而无需为任何表单字段输入值。</span><span class="sxs-lookup"><span data-stu-id="ccc81-454">For example, there is nothing to prevent you from submitting the Create contact form without entering values for any of the form fields.</span></span> <span data-ttu-id="ccc81-455">此外，您还可以输入无效的电话号码和电子邮件地址。</span><span class="sxs-lookup"><span data-stu-id="ccc81-455">Furthermore, you can enter invalid phone numbers and email addresses.</span></span> <span data-ttu-id="ccc81-456">我们开始在迭代#3解决表单验证问题。</span><span class="sxs-lookup"><span data-stu-id="ccc81-456">We start to tackle the problem of form validation in iteration #3.</span></span>

<span data-ttu-id="ccc81-457">最后，最重要的是，无法轻松修改或维护联系人管理器应用程序的当前迭代。</span><span class="sxs-lookup"><span data-stu-id="ccc81-457">Finally, and most importantly, the current iteration of the Contact Manager application cannot be easily modified or maintained.</span></span> <span data-ttu-id="ccc81-458">例如，数据库访问逻辑直接烘焙到控制器操作中。</span><span class="sxs-lookup"><span data-stu-id="ccc81-458">For example, the database access logic is baked right into the controller actions.</span></span> <span data-ttu-id="ccc81-459">这意味着，如果不修改控制器，我们就无法修改数据访问代码。</span><span class="sxs-lookup"><span data-stu-id="ccc81-459">This means that we cannot modify our data access code without modifying our controllers.</span></span> <span data-ttu-id="ccc81-460">在以后的迭代中，我们探索了可以实现的软件设计模式，以使联系人管理器对更改更具弹性。</span><span class="sxs-lookup"><span data-stu-id="ccc81-460">In later iterations, we explore software design patterns that we can implement to make the Contact Manager more resilient to change.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="ccc81-461">[上一页](iteration-7-add-ajax-functionality-cs.md)
> [下一页](iteration-2-make-the-application-look-nice-vb.md)</span><span class="sxs-lookup"><span data-stu-id="ccc81-461">[Previous](iteration-7-add-ajax-functionality-cs.md)
[Next](iteration-2-make-the-application-look-nice-vb.md)</span></span>

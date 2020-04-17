---
uid: mvc/overview/older-versions-1/contact-manager/iteration-6-use-test-driven-development-cs
title: 迭代#6 = 使用测试驱动开发 （C#） |微软文档
author: rick-anderson
description: 在第六次迭代中，我们首先编写单元测试并针对单元测试编写代码，从而向应用程序添加新功能。 在此迭代中,...
ms.author: riande
ms.date: 02/20/2009
ms.assetid: 013c3c26-7dc3-41d1-8064-f233c86008b5
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-6-use-test-driven-development-cs
msc.type: authoredcontent
ms.openlocfilehash: d0e8f30a075cc79c7410ffe1b8bf02da2bd44443
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542321"
---
# <a name="iteration-6--use-test-driven-development-c"></a><span data-ttu-id="0ea89-104">迭代 6 – 使用测试驱动开发 (C#)</span><span class="sxs-lookup"><span data-stu-id="0ea89-104">Iteration #6 – Use test-driven development (C#)</span></span>

<span data-ttu-id="0ea89-105">由[微软](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="0ea89-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="0ea89-106">下载代码</span><span class="sxs-lookup"><span data-stu-id="0ea89-106">Download Code</span></span>](iteration-6-use-test-driven-development-cs/_static/contactmanager_6_cs1.zip)

> <span data-ttu-id="0ea89-107">在第六次迭代中，我们首先编写单元测试并针对单元测试编写代码，从而向应用程序添加新功能。</span><span class="sxs-lookup"><span data-stu-id="0ea89-107">In this sixth iteration, we add new functionality to our application by writing unit tests first and writing code against the unit tests.</span></span> <span data-ttu-id="0ea89-108">在此迭代中，我们添加联系人组。</span><span class="sxs-lookup"><span data-stu-id="0ea89-108">In this iteration, we add contact groups.</span></span>

## <a name="building-a-contact-management-aspnet-mvc-application-c"></a><span data-ttu-id="0ea89-109">构建联系人管理ASP.NET MVC 应用程序 （C#）</span><span class="sxs-lookup"><span data-stu-id="0ea89-109">Building a Contact Management ASP.NET MVC Application (C#)</span></span>

<span data-ttu-id="0ea89-110">在本系列教程中，我们从头到尾构建整个联系人管理应用程序。</span><span class="sxs-lookup"><span data-stu-id="0ea89-110">In this series of tutorials, we build an entire Contact Management application from start to finish.</span></span> <span data-ttu-id="0ea89-111">通过联系人管理器应用程序，您可以存储联系人信息 （姓名、电话号码和电子邮件地址） 人员列表。</span><span class="sxs-lookup"><span data-stu-id="0ea89-111">The Contact Manager application enables you to store contact information - names, phone numbers and email addresses - for a list of people.</span></span>

<span data-ttu-id="0ea89-112">我们通过多次迭代构建应用程序。</span><span class="sxs-lookup"><span data-stu-id="0ea89-112">We build the application over multiple iterations.</span></span> <span data-ttu-id="0ea89-113">每次迭代时，我们都会逐步改进应用程序。</span><span class="sxs-lookup"><span data-stu-id="0ea89-113">With each iteration, we gradually improve the application.</span></span> <span data-ttu-id="0ea89-114">此多迭代方法的目标是使您能够了解每次更改的原因。</span><span class="sxs-lookup"><span data-stu-id="0ea89-114">The goal of this multiple iteration approach is to enable you to understand the reason for each change.</span></span>

- <span data-ttu-id="0ea89-115">迭代#1 - 创建应用程序。</span><span class="sxs-lookup"><span data-stu-id="0ea89-115">Iteration #1 - Create the application.</span></span> <span data-ttu-id="0ea89-116">在第一次迭代中，我们以最简单的方式创建联系人管理器。</span><span class="sxs-lookup"><span data-stu-id="0ea89-116">In the first iteration, we create the Contact Manager in the simplest way possible.</span></span> <span data-ttu-id="0ea89-117">我们添加对基本数据库操作的支持：创建、读取、更新和删除 （CRUD）。</span><span class="sxs-lookup"><span data-stu-id="0ea89-117">We add support for basic database operations: Create, Read, Update, and Delete (CRUD).</span></span>

- <span data-ttu-id="0ea89-118">迭代#2 - 使应用程序看起来不错。</span><span class="sxs-lookup"><span data-stu-id="0ea89-118">Iteration #2 - Make the application look nice.</span></span> <span data-ttu-id="0ea89-119">在此迭代中，我们通过修改默认ASP.NET MVC 视图母版页和级联样式表来改进应用程序的外观。</span><span class="sxs-lookup"><span data-stu-id="0ea89-119">In this iteration, we improve the appearance of the application by modifying the default ASP.NET MVC view master page and cascading style sheet.</span></span>

- <span data-ttu-id="0ea89-120">迭代#3 - 添加表单验证。</span><span class="sxs-lookup"><span data-stu-id="0ea89-120">Iteration #3 - Add form validation.</span></span> <span data-ttu-id="0ea89-121">在第三个迭代中，我们添加基本表单验证。</span><span class="sxs-lookup"><span data-stu-id="0ea89-121">In the third iteration, we add basic form validation.</span></span> <span data-ttu-id="0ea89-122">我们防止人们在未填写所需表单字段的情况下提交表单。</span><span class="sxs-lookup"><span data-stu-id="0ea89-122">We prevent people from submitting a form without completing required form fields.</span></span> <span data-ttu-id="0ea89-123">我们还验证电子邮件地址和电话号码。</span><span class="sxs-lookup"><span data-stu-id="0ea89-123">We also validate email addresses and phone numbers.</span></span>

- <span data-ttu-id="0ea89-124">迭代#4 - 使应用程序松散耦合。</span><span class="sxs-lookup"><span data-stu-id="0ea89-124">Iteration #4 - Make the application loosely coupled.</span></span> <span data-ttu-id="0ea89-125">在第四次迭代中，我们利用多种软件设计模式，使维护和修改联系人管理器应用程序变得更加容易。</span><span class="sxs-lookup"><span data-stu-id="0ea89-125">In this fourth iteration, we take advantage of several software design patterns to make it easier to maintain and modify the Contact Manager application.</span></span> <span data-ttu-id="0ea89-126">例如，我们重构应用程序以使用存储库模式和依赖项注入模式。</span><span class="sxs-lookup"><span data-stu-id="0ea89-126">For example, we refactor our application to use the Repository pattern and the Dependency Injection pattern.</span></span>

- <span data-ttu-id="0ea89-127">迭代#5 - 创建单元测试。</span><span class="sxs-lookup"><span data-stu-id="0ea89-127">Iteration #5 - Create unit tests.</span></span> <span data-ttu-id="0ea89-128">在第五次迭代中，我们通过添加单元测试使应用程序更易于维护和修改。</span><span class="sxs-lookup"><span data-stu-id="0ea89-128">In the fifth iteration, we make our application easier to maintain and modify by adding unit tests.</span></span> <span data-ttu-id="0ea89-129">我们模拟数据模型类，并为控制器和验证逻辑构建单元测试。</span><span class="sxs-lookup"><span data-stu-id="0ea89-129">We mock our data model classes and build unit tests for our controllers and validation logic.</span></span>

- <span data-ttu-id="0ea89-130">迭代#6 - 使用测试驱动开发。</span><span class="sxs-lookup"><span data-stu-id="0ea89-130">Iteration #6 - Use test-driven development.</span></span> <span data-ttu-id="0ea89-131">在第六次迭代中，我们首先编写单元测试并针对单元测试编写代码，从而向应用程序添加新功能。</span><span class="sxs-lookup"><span data-stu-id="0ea89-131">In this sixth iteration, we add new functionality to our application by writing unit tests first and writing code against the unit tests.</span></span> <span data-ttu-id="0ea89-132">在此迭代中，我们添加联系人组。</span><span class="sxs-lookup"><span data-stu-id="0ea89-132">In this iteration, we add contact groups.</span></span>

- <span data-ttu-id="0ea89-133">迭代#7 - 添加Ajax功能。</span><span class="sxs-lookup"><span data-stu-id="0ea89-133">Iteration #7 - Add Ajax functionality.</span></span> <span data-ttu-id="0ea89-134">在第七次迭代中，我们通过增加对Ajax的支持来提高应用程序的响应性和性能。</span><span class="sxs-lookup"><span data-stu-id="0ea89-134">In the seventh iteration, we improve the responsiveness and performance of our application by adding support for Ajax.</span></span>

## <a name="this-iteration"></a><span data-ttu-id="0ea89-135">此迭代</span><span class="sxs-lookup"><span data-stu-id="0ea89-135">This Iteration</span></span>

<span data-ttu-id="0ea89-136">在 Contact Manager 应用程序的上一次迭代中，我们创建了单元测试，为我们的代码提供一个安全网。</span><span class="sxs-lookup"><span data-stu-id="0ea89-136">In the previous iteration of the Contact Manager application, we created unit tests to provide a safety net for our code.</span></span> <span data-ttu-id="0ea89-137">创建单元测试的动机是使我们的代码对更改更具弹性。</span><span class="sxs-lookup"><span data-stu-id="0ea89-137">The motivation for creating the unit tests was to make our code more resilient to change.</span></span> <span data-ttu-id="0ea89-138">通过单元测试，我们可以愉快地对我们的代码进行任何更改，并立即知道我们是否破坏了现有功能。</span><span class="sxs-lookup"><span data-stu-id="0ea89-138">With unit tests in place, we can happily make any change to our code and immediately know whether we have broken existing functionality.</span></span>

<span data-ttu-id="0ea89-139">在此迭代中，我们将单元测试用于完全不同的目的。</span><span class="sxs-lookup"><span data-stu-id="0ea89-139">In this iteration, we use unit tests for an entirely different purpose.</span></span> <span data-ttu-id="0ea89-140">在此迭代中，我们将单元测试用作称为*测试驱动开发*的应用程序设计理念的一部分。</span><span class="sxs-lookup"><span data-stu-id="0ea89-140">In this iteration, we use unit tests as part of an application design philosophy called *test-driven development*.</span></span> <span data-ttu-id="0ea89-141">练习测试驱动开发时，首先编写测试，然后针对测试编写代码。</span><span class="sxs-lookup"><span data-stu-id="0ea89-141">When you practice test-driven development, you write tests first and then write code against the tests.</span></span>

<span data-ttu-id="0ea89-142">更确切地说，在练习测试驱动开发时，在创建代码时完成三个步骤（红色/绿色/重构）：</span><span class="sxs-lookup"><span data-stu-id="0ea89-142">More precisely, when practicing test-driven development, there are three steps that you complete when creating code (Red/ Green/Refactor):</span></span>

1. <span data-ttu-id="0ea89-143">编写失败的单元测试（红色）</span><span class="sxs-lookup"><span data-stu-id="0ea89-143">Write a unit test that fails (Red)</span></span>
2. <span data-ttu-id="0ea89-144">编写通过单元测试的代码（绿色）</span><span class="sxs-lookup"><span data-stu-id="0ea89-144">Write code that passes the unit test (Green)</span></span>
3. <span data-ttu-id="0ea89-145">重构代码（重构）</span><span class="sxs-lookup"><span data-stu-id="0ea89-145">Refactor your code (Refactor)</span></span>

<span data-ttu-id="0ea89-146">首先，编写单元测试。</span><span class="sxs-lookup"><span data-stu-id="0ea89-146">First, you write the unit test.</span></span> <span data-ttu-id="0ea89-147">单元测试应表达您希望代码如何的行为的意图。</span><span class="sxs-lookup"><span data-stu-id="0ea89-147">The unit test should express your intention for how you expect your code to behave.</span></span> <span data-ttu-id="0ea89-148">首次创建单元测试时，单元测试应失败。</span><span class="sxs-lookup"><span data-stu-id="0ea89-148">When you first create the unit test, the unit test should fail.</span></span> <span data-ttu-id="0ea89-149">测试应失败，因为您尚未编写满足测试的任何应用程序代码。</span><span class="sxs-lookup"><span data-stu-id="0ea89-149">The test should fail because you have not yet written any application code that satisfies the test.</span></span>

<span data-ttu-id="0ea89-150">接下来，您只编写足够的代码，以便单元测试通过。</span><span class="sxs-lookup"><span data-stu-id="0ea89-150">Next, you write just enough code in order for the unit test to pass.</span></span> <span data-ttu-id="0ea89-151">目标是以最懒、最懒、最快的方式编写代码。</span><span class="sxs-lookup"><span data-stu-id="0ea89-151">The goal is to write the code in the laziest, sloppiest and fastest possible way.</span></span> <span data-ttu-id="0ea89-152">不应浪费时间考虑应用程序的体系结构。</span><span class="sxs-lookup"><span data-stu-id="0ea89-152">You should not waste time thinking about the architecture of your application.</span></span> <span data-ttu-id="0ea89-153">相反，您应该专注于编写满足单元测试表达的意图所需的最小代码量。</span><span class="sxs-lookup"><span data-stu-id="0ea89-153">Instead, you should focus on writing the minimal amount of code necessary to satisfy the intention expressed by the unit test.</span></span>

<span data-ttu-id="0ea89-154">最后，在编写了足够的代码后，您可以退后一步考虑应用程序的整体体系结构。</span><span class="sxs-lookup"><span data-stu-id="0ea89-154">Finally, after you have written enough code, you can step back and consider the overall architecture of your application.</span></span> <span data-ttu-id="0ea89-155">在此步骤中，您利用软件设计模式（如存储库模式）重写（重构）代码，以便代码更可维护。</span><span class="sxs-lookup"><span data-stu-id="0ea89-155">In this step, you rewrite (refactor) your code by taking advantage of software design patterns -- such as the repository pattern -- so that your code is more maintainable.</span></span> <span data-ttu-id="0ea89-156">您可以在此步骤中无所畏惧地重写代码，因为单元测试涵盖了您的代码。</span><span class="sxs-lookup"><span data-stu-id="0ea89-156">You can fearlessly rewrite your code in this step because your code is covered by unit tests.</span></span>

<span data-ttu-id="0ea89-157">实践测试驱动开发会带来许多好处。</span><span class="sxs-lookup"><span data-stu-id="0ea89-157">There are many benefits that result from practicing test-driven development.</span></span> <span data-ttu-id="0ea89-158">首先，测试驱动的开发迫使您专注于实际需要编写的代码。</span><span class="sxs-lookup"><span data-stu-id="0ea89-158">First, test-driven development forces you to focus on code that actually needs to be written.</span></span> <span data-ttu-id="0ea89-159">由于您始终专注于编写足够的代码以通过特定的测试，因此您无法游荡到杂草中，并编写大量永远不会使用的代码。</span><span class="sxs-lookup"><span data-stu-id="0ea89-159">Because you are constantly focused on just writing enough code to pass a particular test, you are prevented from wandering into the weeds and writing massive amounts of code that you will never use.</span></span>

<span data-ttu-id="0ea89-160">其次，"测试第一"设计方法迫使您从如何使用代码的角度编写代码。</span><span class="sxs-lookup"><span data-stu-id="0ea89-160">Second, a "test first" design methodology forces you to write code from the perspective of how your code will be used.</span></span> <span data-ttu-id="0ea89-161">换句话说，在练习测试驱动开发时，您会不断从用户的角度编写测试。</span><span class="sxs-lookup"><span data-stu-id="0ea89-161">In other words, when practicing test-driven development, you are constantly writing your tests from a user perspective.</span></span> <span data-ttu-id="0ea89-162">因此，测试驱动的开发可以产生更清洁、更易懂的 API。</span><span class="sxs-lookup"><span data-stu-id="0ea89-162">Therefore, test-driven development can result in cleaner and more understandable APIs.</span></span>

<span data-ttu-id="0ea89-163">最后，测试驱动的开发迫使您编写单元测试，作为编写应用程序的正常过程的一部分。</span><span class="sxs-lookup"><span data-stu-id="0ea89-163">Finally, test-driven development forces you to write unit tests as part of the normal process of writing an application.</span></span> <span data-ttu-id="0ea89-164">随着项目截止时间的临近，测试通常是窗口外的第一件事。</span><span class="sxs-lookup"><span data-stu-id="0ea89-164">As a project deadline approaches, testing is typically the first thing that goes out the window.</span></span> <span data-ttu-id="0ea89-165">另一方面，在实践测试驱动开发时，您更有可能对编写单元测试具有道德性，因为测试驱动开发使单元测试成为构建应用程序过程的核心。</span><span class="sxs-lookup"><span data-stu-id="0ea89-165">When practicing test-driven development, on the other hand, you are more likely to be virtuous about writing unit tests because test-driven development makes unit tests central to the process of building an application.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="0ea89-166">要了解有关测试驱动开发的更多内容，我建议您阅读 Michael Feathers 的书，**以有效使用旧代码**。</span><span class="sxs-lookup"><span data-stu-id="0ea89-166">To learn more about test-driven development, I recommend that you read Michael Feathers book **Working Effectively with Legacy Code**.</span></span>

<span data-ttu-id="0ea89-167">在此迭代中，我们将向联系人管理器应用程序添加新功能。</span><span class="sxs-lookup"><span data-stu-id="0ea89-167">In this iteration, we add a new feature to our Contact Manager application.</span></span> <span data-ttu-id="0ea89-168">我们添加对联系人组的支持。</span><span class="sxs-lookup"><span data-stu-id="0ea89-168">We add support for Contact Groups.</span></span> <span data-ttu-id="0ea89-169">您可以使用"联系人组"将联系人组织到"业务"和"朋友"组等类别中。</span><span class="sxs-lookup"><span data-stu-id="0ea89-169">You can use Contact Groups to organize your contacts into categories such as Business and Friend groups.</span></span>

<span data-ttu-id="0ea89-170">我们将遵循测试驱动开发过程，将这项新功能添加到我们的应用程序中。</span><span class="sxs-lookup"><span data-stu-id="0ea89-170">We'll add this new functionality to our application by following a process of test-driven development.</span></span> <span data-ttu-id="0ea89-171">我们将首先编写单元测试，并针对这些测试编写所有代码。</span><span class="sxs-lookup"><span data-stu-id="0ea89-171">We'll write our unit tests first and we'll write all of our code against these tests.</span></span>

## <a name="what-gets-tested"></a><span data-ttu-id="0ea89-172">测试内容</span><span class="sxs-lookup"><span data-stu-id="0ea89-172">What Gets Tested</span></span>

<span data-ttu-id="0ea89-173">正如我们在上一次迭代中讨论的那样，您通常不会为数据访问逻辑或视图逻辑编写单元测试。</span><span class="sxs-lookup"><span data-stu-id="0ea89-173">As we discussed in the previous iteration, you typically do not write unit tests for data access logic or view logic.</span></span> <span data-ttu-id="0ea89-174">您不会为数据访问逻辑编写单元测试，因为访问数据库的操作相对较慢。</span><span class="sxs-lookup"><span data-stu-id="0ea89-174">You don t write unit tests for data access logic because accessing a database is a relatively slow operation.</span></span> <span data-ttu-id="0ea89-175">您不为视图逻辑编写单元测试，因为访问视图需要旋转 Web 服务器，这是一个相对较慢的操作。</span><span class="sxs-lookup"><span data-stu-id="0ea89-175">You don t write unit tests for view logic because accessing a view requires spinning up a web server which is a relatively slow operation.</span></span> <span data-ttu-id="0ea89-176">除非测试可以快速一遍又一遍地执行，否则不应编写单元测试</span><span class="sxs-lookup"><span data-stu-id="0ea89-176">You shouldn't write a unit test unless the test can be executed over and over again very fast</span></span>

<span data-ttu-id="0ea89-177">由于测试驱动开发由单元测试驱动，所以我们最初侧重于编写控制器和业务逻辑。</span><span class="sxs-lookup"><span data-stu-id="0ea89-177">Because test-driven development is driven by unit tests, we focus initially on writing controller and business logic.</span></span> <span data-ttu-id="0ea89-178">我们避免触摸数据库或视图。</span><span class="sxs-lookup"><span data-stu-id="0ea89-178">We avoid touching the database or views.</span></span> <span data-ttu-id="0ea89-179">在本教程结束之前，我们不会修改数据库或创建视图。</span><span class="sxs-lookup"><span data-stu-id="0ea89-179">We won't modify the database or create our views until the very end of this tutorial.</span></span> <span data-ttu-id="0ea89-180">我们从可以测试的内容开始。</span><span class="sxs-lookup"><span data-stu-id="0ea89-180">We start with what can be tested.</span></span>

## <a name="creating-user-stories"></a><span data-ttu-id="0ea89-181">创建用户情景</span><span class="sxs-lookup"><span data-stu-id="0ea89-181">Creating User Stories</span></span>

<span data-ttu-id="0ea89-182">练习测试驱动开发时，您总是从编写测试开始。</span><span class="sxs-lookup"><span data-stu-id="0ea89-182">When practicing test-driven development, you always start by writing a test.</span></span> <span data-ttu-id="0ea89-183">这立即提出了一个问题：你如何决定先写什么测试？</span><span class="sxs-lookup"><span data-stu-id="0ea89-183">This immediately raises the question: How do you decide what test to write first?</span></span> <span data-ttu-id="0ea89-184">要回答这个问题，你应该编写一组[**用户情景**](http://en.wikipedia.org/wiki/User_stories)。</span><span class="sxs-lookup"><span data-stu-id="0ea89-184">To answer this question, you should write a set of [**user stories**](http://en.wikipedia.org/wiki/User_stories).</span></span>

<span data-ttu-id="0ea89-185">用户情景是软件要求的非常简短（通常是一个句子）描述。</span><span class="sxs-lookup"><span data-stu-id="0ea89-185">A user story is a very brief (usually one sentence) description of a software requirement.</span></span> <span data-ttu-id="0ea89-186">它应该是从用户的角度编写的对需求的非技术描述。</span><span class="sxs-lookup"><span data-stu-id="0ea89-186">It should be a non-technical description of a requirement written from a user perspective.</span></span>

<span data-ttu-id="0ea89-187">以下是描述新的联系人组功能所需的功能的用户情景集：</span><span class="sxs-lookup"><span data-stu-id="0ea89-187">Here s the set of user stories that describe the features required by the new Contact Group functionality:</span></span>

1. <span data-ttu-id="0ea89-188">用户可以查看联系人组的列表。</span><span class="sxs-lookup"><span data-stu-id="0ea89-188">User can view a list of contact groups.</span></span>
2. <span data-ttu-id="0ea89-189">用户可以创建新的联系人组。</span><span class="sxs-lookup"><span data-stu-id="0ea89-189">User can create a new contact group.</span></span>
3. <span data-ttu-id="0ea89-190">用户可以删除现有的联系人组。</span><span class="sxs-lookup"><span data-stu-id="0ea89-190">User can delete an existing contact group.</span></span>
4. <span data-ttu-id="0ea89-191">创建新联系人时，用户可以选择联系人组。</span><span class="sxs-lookup"><span data-stu-id="0ea89-191">User can select a contact group when creating a new contact.</span></span>
5. <span data-ttu-id="0ea89-192">用户可以在编辑现有联系人时选择联系人组。</span><span class="sxs-lookup"><span data-stu-id="0ea89-192">User can select a contact group when editing an existing contact.</span></span>
6. <span data-ttu-id="0ea89-193">联系人组列表显示在"索引"视图中。</span><span class="sxs-lookup"><span data-stu-id="0ea89-193">A list of contact groups is displayed in the Index view.</span></span>
7. <span data-ttu-id="0ea89-194">当用户单击联系人组时，将显示匹配联系人的列表。</span><span class="sxs-lookup"><span data-stu-id="0ea89-194">When a user clicks a contact group, a list of matching contacts is displayed.</span></span>

<span data-ttu-id="0ea89-195">请注意，客户完全可以理解此用户情景列表。</span><span class="sxs-lookup"><span data-stu-id="0ea89-195">Notice that this list of user stories is completely understandable by a customer.</span></span> <span data-ttu-id="0ea89-196">没有提到技术实施细节。</span><span class="sxs-lookup"><span data-stu-id="0ea89-196">There is no mention of technical implementation details.</span></span>

<span data-ttu-id="0ea89-197">在构建应用程序的过程中，用户情景集可能会变得更加精细。</span><span class="sxs-lookup"><span data-stu-id="0ea89-197">While in the process of building your application, the set of user stories can become more refined.</span></span> <span data-ttu-id="0ea89-198">您可以将用户情景分解为多个情景（要求）。</span><span class="sxs-lookup"><span data-stu-id="0ea89-198">You might break a user story into multiple stories (requirements).</span></span> <span data-ttu-id="0ea89-199">例如，您可能决定创建新的联系人组应涉及验证。</span><span class="sxs-lookup"><span data-stu-id="0ea89-199">For example, you might decide that creating a new contact group should involve validation.</span></span> <span data-ttu-id="0ea89-200">提交没有名称的联系人组应返回验证错误。</span><span class="sxs-lookup"><span data-stu-id="0ea89-200">Submitting a contact group without a name should return a validation error.</span></span>

<span data-ttu-id="0ea89-201">创建用户情景列表后，即可编写第一个单元测试。</span><span class="sxs-lookup"><span data-stu-id="0ea89-201">After you create a list of user stories, you are ready to write your first unit test.</span></span> <span data-ttu-id="0ea89-202">我们将首先创建用于查看联系人组列表的单位测试。</span><span class="sxs-lookup"><span data-stu-id="0ea89-202">We'll start by creating a unit test for viewing the list of contact groups.</span></span>

## <a name="listing-contact-groups"></a><span data-ttu-id="0ea89-203">列出联系人组</span><span class="sxs-lookup"><span data-stu-id="0ea89-203">Listing Contact Groups</span></span>

<span data-ttu-id="0ea89-204">我们的第一个用户故事是，用户应该能够查看联系人组的列表。</span><span class="sxs-lookup"><span data-stu-id="0ea89-204">Our first user story is that a user should be able to view a list of contact groups.</span></span> <span data-ttu-id="0ea89-205">我们需要用测试来表达这个故事。</span><span class="sxs-lookup"><span data-stu-id="0ea89-205">We need to express this story with a test.</span></span>

<span data-ttu-id="0ea89-206">通过右键单击 ContactManager.测试项目中的控制器文件夹、选择 **"添加、新建测试**"并选择单元测试模板来创建新**的单元测试**（参见图 1）。</span><span class="sxs-lookup"><span data-stu-id="0ea89-206">Create a new unit test by right-clicking the Controllers folder in the ContactManager.Tests project, selecting **Add, New Test**, and selecting the **Unit Test** template (see Figure 1).</span></span> <span data-ttu-id="0ea89-207">GroupControllerTest.cs为新单元测试命名，然后单击 **"确定**"按钮。</span><span class="sxs-lookup"><span data-stu-id="0ea89-207">Name the new unit test GroupControllerTest.cs and click the **OK** button.</span></span>

<span data-ttu-id="0ea89-208">[![添加组控制器测试单元测试](iteration-6-use-test-driven-development-cs/_static/image1.jpg)](iteration-6-use-test-driven-development-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="0ea89-208">[![Adding the GroupControllerTest unit test](iteration-6-use-test-driven-development-cs/_static/image1.jpg)](iteration-6-use-test-driven-development-cs/_static/image1.png)</span></span>

<span data-ttu-id="0ea89-209">**图 01**： 添加组控制器测试单元测试（[单击以查看全尺寸图像](iteration-6-use-test-driven-development-cs/_static/image2.png)）</span><span class="sxs-lookup"><span data-stu-id="0ea89-209">**Figure 01**: Adding the GroupControllerTest unit test([Click to view full-size image](iteration-6-use-test-driven-development-cs/_static/image2.png))</span></span>

<span data-ttu-id="0ea89-210">我们的第一个单元测试包含在清单 1 中。</span><span class="sxs-lookup"><span data-stu-id="0ea89-210">Our first unit test is contained in Listing 1.</span></span> <span data-ttu-id="0ea89-211">此测试验证组控制器的 Index（） 方法是否返回一组组。</span><span class="sxs-lookup"><span data-stu-id="0ea89-211">This test verifies that the Index() method of the Group controller returns a set of Groups.</span></span> <span data-ttu-id="0ea89-212">测试验证在视图数据中返回组的集合。</span><span class="sxs-lookup"><span data-stu-id="0ea89-212">The test verifies that a collection of Groups is returned in view data.</span></span>

<span data-ttu-id="0ea89-213">**清单 1 - 控制器\组控制器测试.cs**</span><span class="sxs-lookup"><span data-stu-id="0ea89-213">**Listing 1 - Controllers\GroupControllerTest.cs**</span></span>

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample1.cs)]

<span data-ttu-id="0ea89-214">当您首次在 Visual Studio 中键入清单 1 中的代码时，您将获得大量红色波浪线。</span><span class="sxs-lookup"><span data-stu-id="0ea89-214">When you first type the code in Listing 1 in Visual Studio, you'll get a lot of red squiggly lines.</span></span> <span data-ttu-id="0ea89-215">我们尚未创建组控制器或组类。</span><span class="sxs-lookup"><span data-stu-id="0ea89-215">We have not created the GroupController or Group classes.</span></span>

<span data-ttu-id="0ea89-216">此时，我们甚至不能构建应用程序，因此无法执行第一个单元测试。</span><span class="sxs-lookup"><span data-stu-id="0ea89-216">At this point, we can t even build our application so we can t execute our first unit test.</span></span> <span data-ttu-id="0ea89-217">很好</span><span class="sxs-lookup"><span data-stu-id="0ea89-217">That s good.</span></span> <span data-ttu-id="0ea89-218">这算作一个失败的测试。</span><span class="sxs-lookup"><span data-stu-id="0ea89-218">That counts as a failing test.</span></span> <span data-ttu-id="0ea89-219">因此，我们现在有权开始编写应用程序代码。</span><span class="sxs-lookup"><span data-stu-id="0ea89-219">Therefore, we now have permission to start writing application code.</span></span> <span data-ttu-id="0ea89-220">我们需要编写足够的代码来执行我们的测试。</span><span class="sxs-lookup"><span data-stu-id="0ea89-220">We need to write enough code to execute our test.</span></span>

<span data-ttu-id="0ea89-221">清单 2 中的组控制器类包含通过单元测试所需的最小代码。</span><span class="sxs-lookup"><span data-stu-id="0ea89-221">The Group controller class in Listing 2 contains the bare minimum of code required to pass the unit test.</span></span> <span data-ttu-id="0ea89-222">Index（） 操作返回静态编码的组列表（组类在清单 3 中定义）。</span><span class="sxs-lookup"><span data-stu-id="0ea89-222">The Index() action returns a statically coded list of Groups (the Group class is defined in Listing 3).</span></span>

<span data-ttu-id="0ea89-223">**清单2 - 控制器\组控制器.cs**</span><span class="sxs-lookup"><span data-stu-id="0ea89-223">**Listing 2 - Controllers\GroupController.cs**</span></span>

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample2.cs)]

<span data-ttu-id="0ea89-224">**清单3 - 模型_组.cs**</span><span class="sxs-lookup"><span data-stu-id="0ea89-224">**Listing 3 - Models\Group.cs**</span></span>

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample3.cs)]

<span data-ttu-id="0ea89-225">将 GroupController 和组类添加到项目中后，我们的第一个单元测试将成功完成（参见图 2）。</span><span class="sxs-lookup"><span data-stu-id="0ea89-225">After we add the GroupController and Group classes to our project, our first unit test completes successfully (see Figure 2).</span></span> <span data-ttu-id="0ea89-226">我们已经做了通过考试所需的最低工作。</span><span class="sxs-lookup"><span data-stu-id="0ea89-226">We have done the minimum work required to pass the test.</span></span> <span data-ttu-id="0ea89-227">是时候庆祝了。</span><span class="sxs-lookup"><span data-stu-id="0ea89-227">It is time to celebrate.</span></span>

<span data-ttu-id="0ea89-228">[![成功！](iteration-6-use-test-driven-development-cs/_static/image2.jpg)](iteration-6-use-test-driven-development-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="0ea89-228">[![Success!](iteration-6-use-test-driven-development-cs/_static/image2.jpg)](iteration-6-use-test-driven-development-cs/_static/image3.png)</span></span>

<span data-ttu-id="0ea89-229">**图02：** 成功！（[单击以查看全尺寸图像](iteration-6-use-test-driven-development-cs/_static/image4.png)）</span><span class="sxs-lookup"><span data-stu-id="0ea89-229">**Figure 02**: Success!([Click to view full-size image](iteration-6-use-test-driven-development-cs/_static/image4.png))</span></span>

## <a name="creating-contact-groups"></a><span data-ttu-id="0ea89-230">创建联系人组</span><span class="sxs-lookup"><span data-stu-id="0ea89-230">Creating Contact Groups</span></span>

<span data-ttu-id="0ea89-231">现在，我们可以转到第二个用户情景。</span><span class="sxs-lookup"><span data-stu-id="0ea89-231">Now we can move on to the second user story.</span></span> <span data-ttu-id="0ea89-232">我们需要能够创建新的联系组。</span><span class="sxs-lookup"><span data-stu-id="0ea89-232">We need to be able to create new contact groups.</span></span> <span data-ttu-id="0ea89-233">我们需要用测试来表达这个意图。</span><span class="sxs-lookup"><span data-stu-id="0ea89-233">We need to express this intention with a test.</span></span>

<span data-ttu-id="0ea89-234">清单4中的测试验证，使用新组调用 Create（） 方法会将组添加到 Index（） 方法返回的组列表中。</span><span class="sxs-lookup"><span data-stu-id="0ea89-234">The test in Listing 4 verifies that calling the Create() method with a new Group adds the Group to the list of Groups returned by the Index() method.</span></span> <span data-ttu-id="0ea89-235">换句话说，如果我创建了一个新组，那么我应该能够从 Index（） 方法返回的组列表中恢复新组。</span><span class="sxs-lookup"><span data-stu-id="0ea89-235">In other words, if I create a new group then I should be able to get the new Group back from the list of Groups returned by the Index() method.</span></span>

<span data-ttu-id="0ea89-236">**清单4 - 控制器\组控制器测试.cs**</span><span class="sxs-lookup"><span data-stu-id="0ea89-236">**Listing 4 - Controllers\GroupControllerTest.cs**</span></span>

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample4.cs)]

<span data-ttu-id="0ea89-237">清单4中的测试使用新的联系人组调用组控制器 Create（） 方法。</span><span class="sxs-lookup"><span data-stu-id="0ea89-237">The test in Listing 4 calls the Group controller Create() method with a new contact Group.</span></span> <span data-ttu-id="0ea89-238">接下来，测试验证调用组控制器 Index（） 方法返回视图中的新组数据。</span><span class="sxs-lookup"><span data-stu-id="0ea89-238">Next, the test verifies that calling the Group controller Index() method returns the new Group in view data.</span></span>

<span data-ttu-id="0ea89-239">清单 5 中修改后的组控制器包含通过新测试所需的最小更改。</span><span class="sxs-lookup"><span data-stu-id="0ea89-239">The modified Group controller in Listing 5 contains the bare minimum of changes required to pass the new test.</span></span>

<span data-ttu-id="0ea89-240">**清单5 - 控制器\组控制器.cs**</span><span class="sxs-lookup"><span data-stu-id="0ea89-240">**Listing 5 - Controllers\GroupController.cs**</span></span>

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample5.cs)]

## <a name="the-group-controller-in-listing-5-has-a-new-create-action-this-action-adds-a-group-to-a-collection-of-groups-notice-that-the-index-action-has-been-modified-to-return-the-contents-of-the-collection-of-groups"></a><span data-ttu-id="0ea89-241">清单 5 中的组控制器具有新的 Create（） 操作。</span><span class="sxs-lookup"><span data-stu-id="0ea89-241">The Group controller in Listing 5 has a new Create() action.</span></span> <span data-ttu-id="0ea89-242">此操作将组添加到组的集合中。</span><span class="sxs-lookup"><span data-stu-id="0ea89-242">This action adds a Group to a collection of Groups.</span></span> <span data-ttu-id="0ea89-243">请注意，已修改 Index（） 操作以返回组集合的内容。</span><span class="sxs-lookup"><span data-stu-id="0ea89-243">Notice that the Index() action has been modified to return the contents of the collection of Groups.</span></span>

<span data-ttu-id="0ea89-244">再次，我们执行了通过单元测试所需的最低工作量。</span><span class="sxs-lookup"><span data-stu-id="0ea89-244">Once again, we have performed the bare minimum amount of work required to pass the unit test.</span></span> <span data-ttu-id="0ea89-245">对组控制器进行这些更改后，所有单元测试都通过。</span><span class="sxs-lookup"><span data-stu-id="0ea89-245">After we make these changes to the Group controller, all of our unit tests pass.</span></span>

## <a name="adding-validation"></a><span data-ttu-id="0ea89-246">添加验证</span><span class="sxs-lookup"><span data-stu-id="0ea89-246">Adding Validation</span></span>

<span data-ttu-id="0ea89-247">在用户情景中未明确说明此要求。</span><span class="sxs-lookup"><span data-stu-id="0ea89-247">This requirement was not stated explicitly in the user story.</span></span> <span data-ttu-id="0ea89-248">但是，要求集团有名称是合理的。</span><span class="sxs-lookup"><span data-stu-id="0ea89-248">However, it is reasonable to require that a Group have a name.</span></span> <span data-ttu-id="0ea89-249">否则，将联系人组织到组中将不是很有用。</span><span class="sxs-lookup"><span data-stu-id="0ea89-249">Otherwise, organizing contacts into Groups would not be very useful.</span></span>

<span data-ttu-id="0ea89-250">清单6包含表示此意图的新测试。</span><span class="sxs-lookup"><span data-stu-id="0ea89-250">Listing 6 contains a new test that expresses this intention.</span></span> <span data-ttu-id="0ea89-251">此测试验证尝试创建组而不提供名称会导致模型状态的验证错误消息。</span><span class="sxs-lookup"><span data-stu-id="0ea89-251">This test verifies that attempting to create a Group without supplying a name results in a validation error message in model state.</span></span>

<span data-ttu-id="0ea89-252">**清单6 - 控制器\组控制器测试.cs**</span><span class="sxs-lookup"><span data-stu-id="0ea89-252">**Listing 6 - Controllers\GroupControllerTest.cs**</span></span>

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample6.cs)]

<span data-ttu-id="0ea89-253">为了满足此测试，我们需要向组类添加 Name 属性（请参阅清单 7）。</span><span class="sxs-lookup"><span data-stu-id="0ea89-253">In order to satisfy this test, we need to add a Name property to our Group class (see Listing 7).</span></span> <span data-ttu-id="0ea89-254">此外，我们需要向组控制器的 Create（） 操作添加一点验证逻辑（参见清单 8）。</span><span class="sxs-lookup"><span data-stu-id="0ea89-254">Furthermore, we need to add a tiny bit of validation logic to our Group controller s Create() action (see Listing 8).</span></span>

<span data-ttu-id="0ea89-255">**清单7 - 模型_组.cs**</span><span class="sxs-lookup"><span data-stu-id="0ea89-255">**Listing 7 - Models\Group.cs**</span></span>

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample7.cs)]

<span data-ttu-id="0ea89-256">**清单8 - 控制器\组控制器.cs**</span><span class="sxs-lookup"><span data-stu-id="0ea89-256">**Listing 8 - Controllers\GroupController.cs**</span></span>

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample8.cs)]

<span data-ttu-id="0ea89-257">请注意，组控制器 Create（） 操作现在同时包含验证和数据库逻辑。</span><span class="sxs-lookup"><span data-stu-id="0ea89-257">Notice that the Group controller Create() action now contains both validation and database logic.</span></span> <span data-ttu-id="0ea89-258">目前，组控制器使用的数据库仅包含内存中的集合。</span><span class="sxs-lookup"><span data-stu-id="0ea89-258">Currently, the database used by the Group controller consists of nothing more than an in-memory collection.</span></span>

## <a name="time-to-refactor"></a><span data-ttu-id="0ea89-259">重构时间</span><span class="sxs-lookup"><span data-stu-id="0ea89-259">Time to Refactor</span></span>

<span data-ttu-id="0ea89-260">红色/绿色/重构的第三步是重构部分。</span><span class="sxs-lookup"><span data-stu-id="0ea89-260">The third step in Red/Green/Refactor is the Refactor part.</span></span> <span data-ttu-id="0ea89-261">此时，我们需要从代码中退后一步，考虑如何重构应用程序以改进其设计。</span><span class="sxs-lookup"><span data-stu-id="0ea89-261">At this point, we need to step back from our code and consider how we can refactor our application to improve its design.</span></span> <span data-ttu-id="0ea89-262">重构阶段是我们认真思考实现软件设计原则和模式的最佳方式的阶段。</span><span class="sxs-lookup"><span data-stu-id="0ea89-262">The Refactor stage is the stage at which we think hard about the best way of implementing software design principles and patterns.</span></span>

<span data-ttu-id="0ea89-263">我们可以自由地修改我们的代码，我们选择以任何方式改进代码的设计。</span><span class="sxs-lookup"><span data-stu-id="0ea89-263">We are free to modify our code in any way that we choose to improve the design of the code.</span></span> <span data-ttu-id="0ea89-264">我们有一个单元测试安全网，以防止我们破坏现有功能。</span><span class="sxs-lookup"><span data-stu-id="0ea89-264">We have a safety net of unit tests that prevent us from breaking existing functionality.</span></span>

<span data-ttu-id="0ea89-265">现在，从良好的软件设计来看，我们的集团控制器是一团糟。</span><span class="sxs-lookup"><span data-stu-id="0ea89-265">Right now, our Group controller is a mess from the perspective of good software design.</span></span> <span data-ttu-id="0ea89-266">组控制器包含一堆的验证和数据访问代码。</span><span class="sxs-lookup"><span data-stu-id="0ea89-266">The Group controller contains a tangled mess of validation and data access code.</span></span> <span data-ttu-id="0ea89-267">为了避免违反单一责任原则，我们需要将这些关注分为不同的类别。</span><span class="sxs-lookup"><span data-stu-id="0ea89-267">To avoid violating the Single Responsibility Principle, we need to separate these concerns into different classes.</span></span>

<span data-ttu-id="0ea89-268">我们的重构组控制器类包含在清单 9 中。</span><span class="sxs-lookup"><span data-stu-id="0ea89-268">Our refactored Group controller class is contained in Listing 9.</span></span> <span data-ttu-id="0ea89-269">控制器已修改为使用 ContactManager 服务层。</span><span class="sxs-lookup"><span data-stu-id="0ea89-269">The controller has been modified to use the ContactManager service layer.</span></span> <span data-ttu-id="0ea89-270">这与我们与联系人控制器一起使用的服务层相同。</span><span class="sxs-lookup"><span data-stu-id="0ea89-270">This is the same service layer that we use with the Contact controller.</span></span>

<span data-ttu-id="0ea89-271">清单10包含添加到 ContactManager 服务层以支持验证、列出和创建组的新方法。</span><span class="sxs-lookup"><span data-stu-id="0ea89-271">Listing 10 contains the new methods added to the ContactManager service layer to support validating, listing, and creating groups.</span></span> <span data-ttu-id="0ea89-272">IContactManager 服务接口已更新，以包括新方法。</span><span class="sxs-lookup"><span data-stu-id="0ea89-272">The IContactManagerService interface was updated to include the new methods.</span></span>

<span data-ttu-id="0ea89-273">清单11包含一个新的 FakeContactManagerManager存储库类，该类实现了 IContactManagerRepository 接口。</span><span class="sxs-lookup"><span data-stu-id="0ea89-273">Listing 11 contains a new FakeContactManagerRepository class that implements the IContactManagerRepository interface.</span></span> <span data-ttu-id="0ea89-274">与同时实现 IContactManagerRepository 接口的实体联系人管理器存储库类不同，我们新的 FakeContactManagerManagerRepository 类不与数据库通信。</span><span class="sxs-lookup"><span data-stu-id="0ea89-274">Unlike the EntityContactManagerRepository class that also implements the IContactManagerRepository interface, our new FakeContactManagerRepository class does not communicate with the database.</span></span> <span data-ttu-id="0ea89-275">FakeContactManagerManagerRepository 类使用内存中集合作为数据库的代理。</span><span class="sxs-lookup"><span data-stu-id="0ea89-275">The FakeContactManagerRepository class uses an in-memory collection as a proxy for the database.</span></span> <span data-ttu-id="0ea89-276">我们将在单元测试中将此类用作假存储库层。</span><span class="sxs-lookup"><span data-stu-id="0ea89-276">We'll use this class in our unit tests as a fake repository layer.</span></span>

<span data-ttu-id="0ea89-277">**清单 9 - 控制器\组控制器.cs**</span><span class="sxs-lookup"><span data-stu-id="0ea89-277">**Listing 9 - Controllers\GroupController.cs**</span></span>

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample9.cs)]

<span data-ttu-id="0ea89-278">**清单 10 - 控制器\联系管理器服务.cs**</span><span class="sxs-lookup"><span data-stu-id="0ea89-278">**Listing 10 - Controllers\ContactManagerService.cs**</span></span>

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample10.cs)]

<span data-ttu-id="0ea89-279">**清单11 - 控制器\假联系人管理器存储库.cs**</span><span class="sxs-lookup"><span data-stu-id="0ea89-279">**Listing 11 - Controllers\FakeContactManagerRepository.cs**</span></span>

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample11.cs)]

<span data-ttu-id="0ea89-280">修改 IContactManager 存储库界面需要用于在实体联系人管理器存储库类中实现 CreateGroup（） 和列表组（）方法。</span><span class="sxs-lookup"><span data-stu-id="0ea89-280">Modifying the IContactManagerRepository interface requires use to implement the CreateGroup() and ListGroups() methods in the EntityContactManagerRepository class.</span></span> <span data-ttu-id="0ea89-281">最懒惰和最快的方法是添加如下所示的存根方法：</span><span class="sxs-lookup"><span data-stu-id="0ea89-281">The laziest and fastest way to do this is to add stub methods that look like this:</span></span>   

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample12.cs)]

<span data-ttu-id="0ea89-282">最后，对应用程序设计的这些更改要求我们对单元测试进行一些修改。</span><span class="sxs-lookup"><span data-stu-id="0ea89-282">Finally, these changes to the design of our application require us to make some modifications to our unit tests.</span></span> <span data-ttu-id="0ea89-283">现在，在执行单元测试时，我们需要使用假联系人管理器存储库。</span><span class="sxs-lookup"><span data-stu-id="0ea89-283">We now need to use the FakeContactManagerRepository when performing the unit tests.</span></span> <span data-ttu-id="0ea89-284">更新后的 GroupControllerTest 类包含在清单 12 中。</span><span class="sxs-lookup"><span data-stu-id="0ea89-284">The updated GroupControllerTest class is contained in Listing 12.</span></span>

<span data-ttu-id="0ea89-285">**清单12 - 控制器\组控制器测试.cs**</span><span class="sxs-lookup"><span data-stu-id="0ea89-285">**Listing 12 - Controllers\GroupControllerTest.cs**</span></span>

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample13.cs)]

<span data-ttu-id="0ea89-286">在我们进行所有这些更改后，我们再次通过所有单元测试。</span><span class="sxs-lookup"><span data-stu-id="0ea89-286">After we make all of these changes, once again, all of our unit tests pass.</span></span> <span data-ttu-id="0ea89-287">我们已经完成了整个红色/绿色/重构周期。</span><span class="sxs-lookup"><span data-stu-id="0ea89-287">We have completed the entire cycle of Red/Green/Refactor.</span></span> <span data-ttu-id="0ea89-288">我们已经实现了前两个用户情景。</span><span class="sxs-lookup"><span data-stu-id="0ea89-288">We have implemented the first two user stories.</span></span> <span data-ttu-id="0ea89-289">现在，我们支持用户情景中表达的要求单元测试。</span><span class="sxs-lookup"><span data-stu-id="0ea89-289">We now have supporting unit tests for the requirements expressed in the user stories.</span></span> <span data-ttu-id="0ea89-290">实现其余用户情景涉及重复相同的红色/绿色/重构周期。</span><span class="sxs-lookup"><span data-stu-id="0ea89-290">Implementing the remainder of the user stories involves repeating the same cycle of Red/Green/Refactor.</span></span>

## <a name="modifying-our-database"></a><span data-ttu-id="0ea89-291">修改我们的数据库</span><span class="sxs-lookup"><span data-stu-id="0ea89-291">Modifying our Database</span></span>

<span data-ttu-id="0ea89-292">不幸的是，尽管我们满足了单元测试表达的所有要求，但我们的工作并没有完成。</span><span class="sxs-lookup"><span data-stu-id="0ea89-292">Unfortunately, even though we have satisfied all of the requirements expressed by our unit tests, our work is not done.</span></span> <span data-ttu-id="0ea89-293">我们仍然需要修改我们的数据库。</span><span class="sxs-lookup"><span data-stu-id="0ea89-293">We still need to modify our database.</span></span>

<span data-ttu-id="0ea89-294">我们需要创建新的组数据库表。</span><span class="sxs-lookup"><span data-stu-id="0ea89-294">We need to create a new Group database table.</span></span> <span data-ttu-id="0ea89-295">执行以下步骤:</span><span class="sxs-lookup"><span data-stu-id="0ea89-295">Follow these steps:</span></span>

1. <span data-ttu-id="0ea89-296">在"服务器资源管理器"窗口中，右键单击"表"文件夹并选择菜单选项 **"添加新表**"。</span><span class="sxs-lookup"><span data-stu-id="0ea89-296">In the Server Explorer window, right-click the Tables folder and select the menu option **Add New Table**.</span></span>
2. <span data-ttu-id="0ea89-297">输入下表设计器中描述的两列。</span><span class="sxs-lookup"><span data-stu-id="0ea89-297">Enter the two columns described below in the Table Designer.</span></span>
3. <span data-ttu-id="0ea89-298">将 Id 列标记为主键和标识列。</span><span class="sxs-lookup"><span data-stu-id="0ea89-298">Mark the Id column as a primary key and Identity column.</span></span>
4. <span data-ttu-id="0ea89-299">单击软盘的图标，保存具有名称组的新表。</span><span class="sxs-lookup"><span data-stu-id="0ea89-299">Save the new table with the name Groups by clicking the icon of the floppy.</span></span>

<a id="0.11_table01"></a>

| <span data-ttu-id="0ea89-300">**列名**</span><span class="sxs-lookup"><span data-stu-id="0ea89-300">**Column Name**</span></span> | <span data-ttu-id="0ea89-301">**数据类型**</span><span class="sxs-lookup"><span data-stu-id="0ea89-301">**Data Type**</span></span> | <span data-ttu-id="0ea89-302">**允许 Null 值**</span><span class="sxs-lookup"><span data-stu-id="0ea89-302">**Allow Nulls**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ea89-303">ID</span><span class="sxs-lookup"><span data-stu-id="0ea89-303">Id</span></span> | <span data-ttu-id="0ea89-304">int</span><span class="sxs-lookup"><span data-stu-id="0ea89-304">int</span></span> | <span data-ttu-id="0ea89-305">False</span><span class="sxs-lookup"><span data-stu-id="0ea89-305">False</span></span> |
| <span data-ttu-id="0ea89-306">“属性”</span><span class="sxs-lookup"><span data-stu-id="0ea89-306">Name</span></span> | <span data-ttu-id="0ea89-307">nvarchar(50)</span><span class="sxs-lookup"><span data-stu-id="0ea89-307">nvarchar(50)</span></span> | <span data-ttu-id="0ea89-308">False</span><span class="sxs-lookup"><span data-stu-id="0ea89-308">False</span></span> |

<span data-ttu-id="0ea89-309">接下来，我们需要从"联系人"表中删除所有数据（否则，我们将无法在"联系人"和"组"表之间创建关系）。</span><span class="sxs-lookup"><span data-stu-id="0ea89-309">Next, we need to delete all of the data from the Contacts table (otherwise, we won't be able to create a relationship between the Contacts and Groups tables).</span></span> <span data-ttu-id="0ea89-310">执行以下步骤:</span><span class="sxs-lookup"><span data-stu-id="0ea89-310">Follow these steps:</span></span>

1. <span data-ttu-id="0ea89-311">右键单击"联系人"表并选择菜单选项 **"显示表数据**"。</span><span class="sxs-lookup"><span data-stu-id="0ea89-311">Right-click the Contacts table and select the menu option **Show Table Data**.</span></span>
2. <span data-ttu-id="0ea89-312">删除所有行。</span><span class="sxs-lookup"><span data-stu-id="0ea89-312">Delete all of the rows.</span></span>

<span data-ttu-id="0ea89-313">接下来，我们需要定义组数据库表和现有联系人数据库表之间的关系。</span><span class="sxs-lookup"><span data-stu-id="0ea89-313">Next, we need to define a relationship between the Groups database table and the existing Contacts database table.</span></span> <span data-ttu-id="0ea89-314">执行以下步骤:</span><span class="sxs-lookup"><span data-stu-id="0ea89-314">Follow these steps:</span></span>

1. <span data-ttu-id="0ea89-315">双击服务器资源管理器窗口中的"联系人"表以打开表设计器。</span><span class="sxs-lookup"><span data-stu-id="0ea89-315">Double-click the Contacts table in the Server Explorer window to open the Table Designer.</span></span>
2. <span data-ttu-id="0ea89-316">向名为 GroupId 的"联系人"表添加新整数列。</span><span class="sxs-lookup"><span data-stu-id="0ea89-316">Add a new integer column to the Contacts table named GroupId.</span></span>
3. <span data-ttu-id="0ea89-317">单击"关系"按钮以打开"外键关系"对话框（参见图 3）。</span><span class="sxs-lookup"><span data-stu-id="0ea89-317">Click the Relationship button to open the Foreign Key Relationships dialog (see Figure 3).</span></span>
4. <span data-ttu-id="0ea89-318">单击“添加”按钮。</span><span class="sxs-lookup"><span data-stu-id="0ea89-318">Click the Add button.</span></span>
5. <span data-ttu-id="0ea89-319">单击"表和列规范"按钮旁边的省略号按钮。</span><span class="sxs-lookup"><span data-stu-id="0ea89-319">Click the ellipsis button that appears next to the Table and Columns Specification button.</span></span>
6. <span data-ttu-id="0ea89-320">在"表和列"对话框中，选择组作为主键表，选择 Id 作为主键列。</span><span class="sxs-lookup"><span data-stu-id="0ea89-320">In the Tables and Columns dialog, select Groups as the primary key table and Id as the primary key column.</span></span> <span data-ttu-id="0ea89-321">选择"联系人"作为外键表，将 GroupId 作为外键列（参见图 4）。</span><span class="sxs-lookup"><span data-stu-id="0ea89-321">Select Contacts as the foreign key table and GroupId as the foreign key column (see Figure 4).</span></span> <span data-ttu-id="0ea89-322">单击“确定”按钮。</span><span class="sxs-lookup"><span data-stu-id="0ea89-322">Click the OK button.</span></span>
7. <span data-ttu-id="0ea89-323">在 **"插入"和"更新规范"** 下，选择**删除规则**的值 **"级联**"。</span><span class="sxs-lookup"><span data-stu-id="0ea89-323">Under **INSERT and UPDATE Specification**, select the value **Cascade** for **Delete Rule**.</span></span>
8. <span data-ttu-id="0ea89-324">单击"关闭"按钮以关闭"外键关系"对话框。</span><span class="sxs-lookup"><span data-stu-id="0ea89-324">Click the Close button to close the Foreign Key Relationships dialog.</span></span>
9. <span data-ttu-id="0ea89-325">单击"保存"按钮将更改保存到"联系人"表。</span><span class="sxs-lookup"><span data-stu-id="0ea89-325">Click the Save button to save the changes to the Contacts table.</span></span>

<span data-ttu-id="0ea89-326">[![创建数据库表关系](iteration-6-use-test-driven-development-cs/_static/image3.jpg)](iteration-6-use-test-driven-development-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="0ea89-326">[![Creating a database table relationship](iteration-6-use-test-driven-development-cs/_static/image3.jpg)](iteration-6-use-test-driven-development-cs/_static/image5.png)</span></span>

<span data-ttu-id="0ea89-327">**图 03**： 创建数据库表关系 （[单击以查看全尺寸图像](iteration-6-use-test-driven-development-cs/_static/image6.png)）</span><span class="sxs-lookup"><span data-stu-id="0ea89-327">**Figure 03**: Creating a database table relationship ([Click to view full-size image](iteration-6-use-test-driven-development-cs/_static/image6.png))</span></span>

<span data-ttu-id="0ea89-328">[![指定表关系](iteration-6-use-test-driven-development-cs/_static/image4.jpg)](iteration-6-use-test-driven-development-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="0ea89-328">[![Specifying table relationships](iteration-6-use-test-driven-development-cs/_static/image4.jpg)](iteration-6-use-test-driven-development-cs/_static/image7.png)</span></span>

<span data-ttu-id="0ea89-329">**图 04**：指定表关系（[单击以查看全尺寸图像](iteration-6-use-test-driven-development-cs/_static/image8.png)）</span><span class="sxs-lookup"><span data-stu-id="0ea89-329">**Figure 04**: Specifying table relationships([Click to view full-size image](iteration-6-use-test-driven-development-cs/_static/image8.png))</span></span>

### <a name="updating-our-data-model"></a><span data-ttu-id="0ea89-330">更新我们的数据模型</span><span class="sxs-lookup"><span data-stu-id="0ea89-330">Updating our Data Model</span></span>

<span data-ttu-id="0ea89-331">接下来，我们需要更新数据模型以表示新的数据库表。</span><span class="sxs-lookup"><span data-stu-id="0ea89-331">Next, we need to update our data model to represent the new database table.</span></span> <span data-ttu-id="0ea89-332">执行以下步骤:</span><span class="sxs-lookup"><span data-stu-id="0ea89-332">Follow these steps:</span></span>

1. <span data-ttu-id="0ea89-333">双击"模型"文件夹中的 ContactManagerModel.edmx 文件以打开实体设计器。</span><span class="sxs-lookup"><span data-stu-id="0ea89-333">Double-click the ContactManagerModel.edmx file in the Models folder to open the Entity Designer.</span></span>
2. <span data-ttu-id="0ea89-334">右键单击"设计器"曲面，然后从数据库中选择菜单选项 **"更新模型**"。</span><span class="sxs-lookup"><span data-stu-id="0ea89-334">Right-click the Designer surface and select the menu option **Update Model from Database**.</span></span>
3. <span data-ttu-id="0ea89-335">在"更新向导"中，选择"组"表并单击"完成"按钮（参见图 5）。</span><span class="sxs-lookup"><span data-stu-id="0ea89-335">In the Update Wizard, select the Groups table and click the Finish button (see Figure 5).</span></span>
4. <span data-ttu-id="0ea89-336">右键单击"组实体"并选择菜单选项 **"重命名**"。</span><span class="sxs-lookup"><span data-stu-id="0ea89-336">Right-click the Groups entity and select the menu option **Rename**.</span></span> <span data-ttu-id="0ea89-337">将*组*实体的名称更改为*组*（单数）。</span><span class="sxs-lookup"><span data-stu-id="0ea89-337">Change the name of the *Groups* entity to *Group* (singular).</span></span>
5. <span data-ttu-id="0ea89-338">右键单击显示在"联系人"实体底部的"组导航属性"。</span><span class="sxs-lookup"><span data-stu-id="0ea89-338">Right-click the Groups navigation property that appears at the bottom of the Contact entity.</span></span> <span data-ttu-id="0ea89-339">将*组*导航属性的名称更改为*组*（单数）。</span><span class="sxs-lookup"><span data-stu-id="0ea89-339">Change the name of the *Groups* navigation property to *Group* (singular).</span></span>

<span data-ttu-id="0ea89-340">[![从数据库更新实体框架模型](iteration-6-use-test-driven-development-cs/_static/image5.jpg)](iteration-6-use-test-driven-development-cs/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="0ea89-340">[![Updating an Entity Framework model from the database](iteration-6-use-test-driven-development-cs/_static/image5.jpg)](iteration-6-use-test-driven-development-cs/_static/image9.png)</span></span>

<span data-ttu-id="0ea89-341">**图 05**：从数据库更新实体框架模型（[单击以查看全尺寸图像](iteration-6-use-test-driven-development-cs/_static/image10.png)）</span><span class="sxs-lookup"><span data-stu-id="0ea89-341">**Figure 05**: Updating an Entity Framework model from the database([Click to view full-size image](iteration-6-use-test-driven-development-cs/_static/image10.png))</span></span>

<span data-ttu-id="0ea89-342">完成这些步骤后，数据模型将同时表示"联系人"和"组"表。</span><span class="sxs-lookup"><span data-stu-id="0ea89-342">After you complete these steps, your data model will represent both the Contacts and Groups tables.</span></span> <span data-ttu-id="0ea89-343">实体设计器应显示两个实体（参见图 6）。</span><span class="sxs-lookup"><span data-stu-id="0ea89-343">The Entity Designer should show both entities (see Figure 6).</span></span>

<span data-ttu-id="0ea89-344">[![实体设计器显示组和联系人](iteration-6-use-test-driven-development-cs/_static/image6.jpg)](iteration-6-use-test-driven-development-cs/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="0ea89-344">[![Entity Designer displaying Group and Contact](iteration-6-use-test-driven-development-cs/_static/image6.jpg)](iteration-6-use-test-driven-development-cs/_static/image11.png)</span></span>

<span data-ttu-id="0ea89-345">**图 06**： 实体设计器显示组和联系人（[单击以查看全尺寸图像](iteration-6-use-test-driven-development-cs/_static/image12.png)）</span><span class="sxs-lookup"><span data-stu-id="0ea89-345">**Figure 06**: Entity Designer displaying Group and Contact([Click to view full-size image](iteration-6-use-test-driven-development-cs/_static/image12.png))</span></span>

### <a name="creating-our-repository-classes"></a><span data-ttu-id="0ea89-346">创建我们的存储库类</span><span class="sxs-lookup"><span data-stu-id="0ea89-346">Creating our Repository Classes</span></span>

<span data-ttu-id="0ea89-347">接下来，我们需要实现我们的存储库类。</span><span class="sxs-lookup"><span data-stu-id="0ea89-347">Next, we need to implement our repository class.</span></span> <span data-ttu-id="0ea89-348">在此迭代过程中，我们在编写代码以满足单元测试的同时，向 IContactManagerRepository 界面添加了几种新方法。</span><span class="sxs-lookup"><span data-stu-id="0ea89-348">Over the course of this iteration, we added several new methods to the IContactManagerRepository interface while writing code to satisfy our unit tests.</span></span> <span data-ttu-id="0ea89-349">IContactManager存储库界面的最终版本包含在清单14中。</span><span class="sxs-lookup"><span data-stu-id="0ea89-349">The final version of the IContactManagerRepository interface is contained in Listing 14.</span></span>

<span data-ttu-id="0ea89-350">**清单14 - 型号\IContactManagerRepository.cs**</span><span class="sxs-lookup"><span data-stu-id="0ea89-350">**Listing 14 - Models\IContactManagerRepository.cs**</span></span>

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample14.cs)]

<span data-ttu-id="0ea89-351">我们实际上尚未实现与使用联系人组相关的任何方法。</span><span class="sxs-lookup"><span data-stu-id="0ea89-351">We haven't actually implemented any of the methods related to working with contact groups.</span></span> <span data-ttu-id="0ea89-352">目前，实体联系人管理器存储库类具有 IContactManagerRepository 界面中列出的每个联系人组方法的存根方法。</span><span class="sxs-lookup"><span data-stu-id="0ea89-352">Currently, the EntityContactManagerRepository class has stub methods for each of the contact group methods listed in the IContactManagerRepository interface.</span></span> <span data-ttu-id="0ea89-353">例如，ListGroups（） 方法当前如下所示：</span><span class="sxs-lookup"><span data-stu-id="0ea89-353">For example, the ListGroups() method currently looks like this:</span></span>

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample15.cs)]

<span data-ttu-id="0ea89-354">存根方法使我们能够编译应用程序并通过单元测试。</span><span class="sxs-lookup"><span data-stu-id="0ea89-354">The stub methods enabled us to compile our application and pass the unit tests.</span></span> <span data-ttu-id="0ea89-355">但是，现在是时候实际实现这些方法了。</span><span class="sxs-lookup"><span data-stu-id="0ea89-355">However, now it is time to actually implement these methods.</span></span> <span data-ttu-id="0ea89-356">实体联系人管理器存储库类的最终版本包含在清单 13 中。</span><span class="sxs-lookup"><span data-stu-id="0ea89-356">The final version of the EntityContactManagerRepository class is contained in Listing 13.</span></span>

<span data-ttu-id="0ea89-357">**清单13 - 模型_实体联系人管理器存储库.cs**</span><span class="sxs-lookup"><span data-stu-id="0ea89-357">**Listing 13 - Models\EntityContactManagerRepository.cs**</span></span>

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample16.cs)]

### <a name="creating-the-views"></a><span data-ttu-id="0ea89-358">创建视图</span><span class="sxs-lookup"><span data-stu-id="0ea89-358">Creating the Views</span></span>

<span data-ttu-id="0ea89-359">使用默认ASP.NET视图引擎时，ASP.NET MVC 应用程序。</span><span class="sxs-lookup"><span data-stu-id="0ea89-359">ASP.NET MVC application when you use the default ASP.NET view engine.</span></span> <span data-ttu-id="0ea89-360">因此，您不会创建视图以响应特定的单元测试。</span><span class="sxs-lookup"><span data-stu-id="0ea89-360">So, you don t create views in response to a particular unit test.</span></span> <span data-ttu-id="0ea89-361">但是，由于没有视图的应用程序将毫无用处，因此，如果不创建和修改 Contact Manager 应用程序中的视图，我们就无法完成此迭代。</span><span class="sxs-lookup"><span data-stu-id="0ea89-361">However, because an application would be useless without views, we can t complete this iteration without creating and modifying the views contained in the Contact Manager application.</span></span>

<span data-ttu-id="0ea89-362">我们需要创建以下用于管理联系人组的新视图（参见图 7）：</span><span class="sxs-lookup"><span data-stu-id="0ea89-362">We need to create the following new views for managing contact groups (see Figure 7):</span></span>

- <span data-ttu-id="0ea89-363">视图_组\索引.aspx - 显示联系人组列表</span><span class="sxs-lookup"><span data-stu-id="0ea89-363">Views\Group\Index.aspx - Displays list of contact groups</span></span>
- <span data-ttu-id="0ea89-364">视图\组\删除.aspx - 显示用于删除联系人组的确认表单</span><span class="sxs-lookup"><span data-stu-id="0ea89-364">Views\Group\Delete.aspx - Displays confirmation form for deleting a contact group</span></span>

<span data-ttu-id="0ea89-365">[![组索引视图](iteration-6-use-test-driven-development-cs/_static/image7.jpg)](iteration-6-use-test-driven-development-cs/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="0ea89-365">[![The Group Index view](iteration-6-use-test-driven-development-cs/_static/image7.jpg)](iteration-6-use-test-driven-development-cs/_static/image13.png)</span></span>

<span data-ttu-id="0ea89-366">**图 07**： 组索引视图（[单击以查看全尺寸图像](iteration-6-use-test-driven-development-cs/_static/image14.png)）</span><span class="sxs-lookup"><span data-stu-id="0ea89-366">**Figure 07**: The Group Index view([Click to view full-size image](iteration-6-use-test-driven-development-cs/_static/image14.png))</span></span>

<span data-ttu-id="0ea89-367">我们需要修改以下现有视图，以便它们包括联系人组：</span><span class="sxs-lookup"><span data-stu-id="0ea89-367">We need to modify the following existing views so that they include contact groups:</span></span>

- <span data-ttu-id="0ea89-368">视图\Home_Create.aspx</span><span class="sxs-lookup"><span data-stu-id="0ea89-368">Views\Home\Create.aspx</span></span>
- <span data-ttu-id="0ea89-369">视图\主页\编辑.aspx</span><span class="sxs-lookup"><span data-stu-id="0ea89-369">Views\Home\Edit.aspx</span></span>
- <span data-ttu-id="0ea89-370">视图\主页\索引.aspx</span><span class="sxs-lookup"><span data-stu-id="0ea89-370">Views\Home\Index.aspx</span></span>

<span data-ttu-id="0ea89-371">通过查看本教程附带的 Visual Studio 应用程序，可以查看修改后的视图。</span><span class="sxs-lookup"><span data-stu-id="0ea89-371">You can see the modified views by looking at the Visual Studio application that accompanies this tutorial.</span></span> <span data-ttu-id="0ea89-372">例如，图 8 说明了联系人索引视图。</span><span class="sxs-lookup"><span data-stu-id="0ea89-372">For example, Figure 8 illustrates the Contact Index view.</span></span>

<span data-ttu-id="0ea89-373">[![联系人索引视图](iteration-6-use-test-driven-development-cs/_static/image8.jpg)](iteration-6-use-test-driven-development-cs/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="0ea89-373">[![The Contact Index view](iteration-6-use-test-driven-development-cs/_static/image8.jpg)](iteration-6-use-test-driven-development-cs/_static/image15.png)</span></span>

<span data-ttu-id="0ea89-374">**图 08**： 联系人索引视图（[单击以查看全尺寸图像](iteration-6-use-test-driven-development-cs/_static/image16.png)）</span><span class="sxs-lookup"><span data-stu-id="0ea89-374">**Figure 08**: The Contact Index view([Click to view full-size image](iteration-6-use-test-driven-development-cs/_static/image16.png))</span></span>

## <a name="summary"></a><span data-ttu-id="0ea89-375">总结</span><span class="sxs-lookup"><span data-stu-id="0ea89-375">Summary</span></span>

<span data-ttu-id="0ea89-376">在此迭代中，我们遵循测试驱动的开发应用程序设计方法，向 Contact Manager 应用程序添加了新功能。</span><span class="sxs-lookup"><span data-stu-id="0ea89-376">In this iteration, we added new functionality to our Contact Manager application by following a test-driven development application design methodology.</span></span> <span data-ttu-id="0ea89-377">我们首先创建一组用户情景。</span><span class="sxs-lookup"><span data-stu-id="0ea89-377">We started by creating a set of user stories.</span></span> <span data-ttu-id="0ea89-378">我们创建了一组单元测试，这些测试对应于用户情景表达的要求。</span><span class="sxs-lookup"><span data-stu-id="0ea89-378">We created a set of unit tests that corresponds to the requirements expressed by the user stories.</span></span> <span data-ttu-id="0ea89-379">最后，我们编写的代码足够满足单元测试表达的要求。</span><span class="sxs-lookup"><span data-stu-id="0ea89-379">Finally, we wrote just enough code to satisfy the requirements expressed by the unit tests.</span></span>

<span data-ttu-id="0ea89-380">完成编写足够的代码以满足单元测试表达的要求后，我们更新了数据库和视图。</span><span class="sxs-lookup"><span data-stu-id="0ea89-380">After we finished writing enough code to satisfy the requirements expressed by the unit tests, we updated our database and views.</span></span> <span data-ttu-id="0ea89-381">我们将新的组表添加到我们的数据库中，并更新了实体框架数据模型。</span><span class="sxs-lookup"><span data-stu-id="0ea89-381">We added a new Groups table to our database and updated our Entity Framework Data Model.</span></span> <span data-ttu-id="0ea89-382">我们还创建并修改了一组视图。</span><span class="sxs-lookup"><span data-stu-id="0ea89-382">We also created and modified a set of views.</span></span>

<span data-ttu-id="0ea89-383">在下一次迭代（最后迭代）中，我们重写应用程序以利用Ajax。</span><span class="sxs-lookup"><span data-stu-id="0ea89-383">In the next iteration -- the final iteration -- we rewrite our application to take advantage of Ajax.</span></span> <span data-ttu-id="0ea89-384">通过使用Ajax，我们将提高联系人管理器应用程序的响应性和性能。</span><span class="sxs-lookup"><span data-stu-id="0ea89-384">By taking advantage of Ajax, we'll improve the responsiveness and performance of the Contact Manager application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="0ea89-385">[上一页](iteration-5-create-unit-tests-cs.md)
> [下一页](iteration-7-add-ajax-functionality-cs.md)</span><span class="sxs-lookup"><span data-stu-id="0ea89-385">[Previous](iteration-5-create-unit-tests-cs.md)
[Next](iteration-7-add-ajax-functionality-cs.md)</span></span>

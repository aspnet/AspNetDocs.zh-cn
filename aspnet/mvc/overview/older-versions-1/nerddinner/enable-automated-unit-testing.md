---
uid: mvc/overview/older-versions-1/nerddinner/enable-automated-unit-testing
title: 启用自动单元测试 |微软文档
author: rick-anderson
description: 步骤 12 演示如何开发一套自动单元测试，以验证我们的 NerdDinner 功能，这将让我们有信心进行更改...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: a19ff2ce-3f7e-4358-9a51-a1403da9c63e
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/enable-automated-unit-testing
msc.type: authoredcontent
ms.openlocfilehash: 7fe84efd9e4cc359c19d5ab9e22c579b80207e9c
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541463"
---
# <a name="enable-automated-unit-testing"></a><span data-ttu-id="c052f-103">启用自动单元测试</span><span class="sxs-lookup"><span data-stu-id="c052f-103">Enable Automated Unit Testing</span></span>

<span data-ttu-id="c052f-104">由[微软](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="c052f-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="c052f-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="c052f-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="c052f-106">这是一个免费的["NerdDinner"应用程序教程](introducing-the-nerddinner-tutorial.md)的第12步，它介绍了如何使用 ASP.NETmVC 1构建小型但完整的Web应用程序。</span><span class="sxs-lookup"><span data-stu-id="c052f-106">This is step 12 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="c052f-107">步骤 12 演示如何开发一套自动单元测试，以验证我们的 NerdDinner 功能，这将让我们有信心在未来对应用程序进行更改和改进。</span><span class="sxs-lookup"><span data-stu-id="c052f-107">Step 12 shows how to develop a suite of automated unit tests that verify our NerdDinner functionality, and which will give us the confidence to make changes and improvements to the application in the future.</span></span>
> 
> <span data-ttu-id="c052f-108">如果您使用的是ASP.NET MVC 3，我们建议您按照[MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC 音乐商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程进行操作。</span><span class="sxs-lookup"><span data-stu-id="c052f-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-12-unit-testing"></a><span data-ttu-id="c052f-109">神经晚餐步骤 12：单元测试</span><span class="sxs-lookup"><span data-stu-id="c052f-109">NerdDinner Step 12: Unit Testing</span></span>

<span data-ttu-id="c052f-110">让我们开发一套自动单元测试，以验证我们的 NerdDinner 功能，这将让我们有信心在未来对应用程序进行更改和改进。</span><span class="sxs-lookup"><span data-stu-id="c052f-110">Let's develop a suite of automated unit tests that verify our NerdDinner functionality, and which will give us the confidence to make changes and improvements to the application in the future.</span></span>

### <a name="why-unit-test"></a><span data-ttu-id="c052f-111">为什么选择单元测试？</span><span class="sxs-lookup"><span data-stu-id="c052f-111">Why Unit Test?</span></span>

<span data-ttu-id="c052f-112">在一天早上上班时，你突然闪现出一些关于你正在处理的应用程序的灵感。</span><span class="sxs-lookup"><span data-stu-id="c052f-112">On the drive into work one morning you have a sudden flash of inspiration about an application you are working on.</span></span> <span data-ttu-id="c052f-113">您意识到，您可以实现一个更改，这将使应用程序显著更好地。</span><span class="sxs-lookup"><span data-stu-id="c052f-113">You realize there is a change you can implement that will make the application dramatically better.</span></span> <span data-ttu-id="c052f-114">它可能是清理代码、添加新功能或修复 Bug 的重构。</span><span class="sxs-lookup"><span data-stu-id="c052f-114">It might be a refactoring that cleans up the code, adds a new feature, or fixes a bug.</span></span>

<span data-ttu-id="c052f-115">当你到达计算机时，您面临的问题是"进行这种改进有多安全？</span><span class="sxs-lookup"><span data-stu-id="c052f-115">The question that confronts you when you arrive at your computer is – "how safe is it to make this improvement?"</span></span> <span data-ttu-id="c052f-116">如果做出改变有副作用或破坏某些东西呢？</span><span class="sxs-lookup"><span data-stu-id="c052f-116">What if making the change has side effects or breaks something?</span></span> <span data-ttu-id="c052f-117">更改可能很简单，只需几分钟即可实现，但如果手动测试所有应用程序方案需要数小时，该怎么办？</span><span class="sxs-lookup"><span data-stu-id="c052f-117">The change might be simple and only take a few minutes to implement, but what if it takes hours to manually test out all of the application scenarios?</span></span> <span data-ttu-id="c052f-118">如果您忘记覆盖场景，而损坏的应用程序投入生产，该怎么办？</span><span class="sxs-lookup"><span data-stu-id="c052f-118">What if you forget to cover a scenario and a broken application goes into production?</span></span> <span data-ttu-id="c052f-119">做出这种改进真的值得付出所有努力吗？</span><span class="sxs-lookup"><span data-stu-id="c052f-119">Is making this improvement really worth all the effort?</span></span>

<span data-ttu-id="c052f-120">自动单元测试可以提供一个安全网，使您能够持续增强应用程序，并避免害怕您正在处理的代码。</span><span class="sxs-lookup"><span data-stu-id="c052f-120">Automated unit tests can provide a safety net that enables you to continually enhance your applications, and avoid being afraid of the code you are working on.</span></span> <span data-ttu-id="c052f-121">通过自动测试来快速验证功能，使您能够自信地编写代码，并使您能够做出改进，否则您可能觉得这样做并不自在。</span><span class="sxs-lookup"><span data-stu-id="c052f-121">Having automated tests that quickly verify functionality enables you to code with confidence – and empower you to make improvements you might otherwise not have felt comfortable doing.</span></span> <span data-ttu-id="c052f-122">它们还有助于创建更可维护且使用寿命更长的解决方案，从而获得更高的投资回报。</span><span class="sxs-lookup"><span data-stu-id="c052f-122">They also help create solutions that are more maintainable and have a longer lifetime - which leads to a much higher return on investment.</span></span>

<span data-ttu-id="c052f-123">ASP.NET MVC 框架使单元测试应用程序功能变得简单自然。</span><span class="sxs-lookup"><span data-stu-id="c052f-123">The ASP.NET MVC Framework makes it easy and natural to unit test application functionality.</span></span> <span data-ttu-id="c052f-124">它还支持测试驱动开发 （TDD） 工作流，支持基于测试优先的开发。</span><span class="sxs-lookup"><span data-stu-id="c052f-124">It also enables a Test Driven Development (TDD) workflow that enables test-first based development.</span></span>

### <a name="nerddinnertests-project"></a><span data-ttu-id="c052f-125">内德晚餐.测试项目</span><span class="sxs-lookup"><span data-stu-id="c052f-125">NerdDinner.Tests Project</span></span>

<span data-ttu-id="c052f-126">当我们在本教程开始时创建 NerdDinner 应用程序时，系统会提示我们进行一个对话框，询问我们是否希望创建一个单元测试项目以配合应用程序项目：</span><span class="sxs-lookup"><span data-stu-id="c052f-126">When we created our NerdDinner application at the beginning of this tutorial, we were prompted with a dialog asking whether we wanted to create a unit test project to go along with the application project:</span></span>

![](enable-automated-unit-testing/_static/image1.png)

<span data-ttu-id="c052f-127">我们保留了"是，创建一个单元测试项目"单选按钮 -导致"NerdDinner.Test"项目被添加到我们的解决方案中：</span><span class="sxs-lookup"><span data-stu-id="c052f-127">We kept the "Yes, create a unit test project" radio button selected – which resulted in a "NerdDinner.Tests" project being added to our solution:</span></span>

![](enable-automated-unit-testing/_static/image2.png)

<span data-ttu-id="c052f-128">NerdDinner.测试项目引用 NerdDinner 应用程序项目程序集，并使我们能够轻松地向其添加自动测试，以验证应用程序功能。</span><span class="sxs-lookup"><span data-stu-id="c052f-128">The NerdDinner.Tests project references the NerdDinner application project assembly, and enables us to easily add automated tests to it that verify the application functionality.</span></span>

### <a name="creating-unit-tests-for-our-dinner-model-class"></a><span data-ttu-id="c052f-129">为我们的晚餐模型类创建单元测试</span><span class="sxs-lookup"><span data-stu-id="c052f-129">Creating Unit Tests for our Dinner Model Class</span></span>

<span data-ttu-id="c052f-130">让我们向 NerdDinner.测试项目添加一些测试，以验证我们在构建模型层时创建的 Dinner 类。</span><span class="sxs-lookup"><span data-stu-id="c052f-130">Let's add some tests to our NerdDinner.Tests project that verify the Dinner class we created when we built our model layer.</span></span>

<span data-ttu-id="c052f-131">我们将首先在我们的测试项目中创建一个名为"模型"的新文件夹，我们将在这里放置与模型相关的测试。</span><span class="sxs-lookup"><span data-stu-id="c052f-131">We'll start by creating a new folder within our test project called "Models" where we'll place our model-related tests.</span></span> <span data-ttu-id="c052f-132">然后，我们将右键单击该文件夹并选择 **"添加-&gt;新测试"** 菜单命令。</span><span class="sxs-lookup"><span data-stu-id="c052f-132">We'll then right-click on the folder and choose the **Add-&gt;New Test** menu command.</span></span> <span data-ttu-id="c052f-133">这将弹出"添加新测试"对话框。</span><span class="sxs-lookup"><span data-stu-id="c052f-133">This will bring up the "Add New Test" dialog.</span></span>

<span data-ttu-id="c052f-134">我们将选择创建"单元测试"并将其命名为"DinnerTest.cs"：</span><span class="sxs-lookup"><span data-stu-id="c052f-134">We'll choose to create a "Unit Test" and name it "DinnerTest.cs":</span></span>

![](enable-automated-unit-testing/_static/image3.png)

<span data-ttu-id="c052f-135">当我们单击"ok"按钮 Visual Studio 会向项目添加（并打开）DinnerTest.cs文件时：</span><span class="sxs-lookup"><span data-stu-id="c052f-135">When we click the "ok" button Visual Studio will add (and open) a DinnerTest.cs file to the project:</span></span>

![](enable-automated-unit-testing/_static/image4.png)

<span data-ttu-id="c052f-136">默认的 Visual Studio 单元测试模板内有一堆样板代码，我觉得有点乱。</span><span class="sxs-lookup"><span data-stu-id="c052f-136">The default Visual Studio unit test template has a bunch of boiler-plate code within it that I find a little messy.</span></span> <span data-ttu-id="c052f-137">让我们清理它，以便只包含以下代码：</span><span class="sxs-lookup"><span data-stu-id="c052f-137">Let's clean it up to just contain the code below:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample1.cs)]

<span data-ttu-id="c052f-138">上面的 DinnerTest 类上的 [TestClass] 属性将其标识为包含测试的类以及可选的测试初始化和拆解代码。</span><span class="sxs-lookup"><span data-stu-id="c052f-138">The [TestClass] attribute on the DinnerTest class above identifies it as a class that will contain tests, as well as optional test initialization and teardown code.</span></span> <span data-ttu-id="c052f-139">我们可以通过在其中添加具有 [TestMethod] 属性的公共方法来定义其中的测试。</span><span class="sxs-lookup"><span data-stu-id="c052f-139">We can define tests within it by adding public methods that have a [TestMethod] attribute on them.</span></span>

<span data-ttu-id="c052f-140">下面是我们将添加的两个测试中的第一个，即锻炼我们的晚餐课程。</span><span class="sxs-lookup"><span data-stu-id="c052f-140">Below are the first of two tests we'll add that exercise our Dinner class.</span></span> <span data-ttu-id="c052f-141">第一个测试验证，如果新晚餐的创建没有正确设置所有属性，则我们的晚餐无效。</span><span class="sxs-lookup"><span data-stu-id="c052f-141">The first test verifies that our Dinner is invalid if a new Dinner is created without all properties being set correctly.</span></span> <span data-ttu-id="c052f-142">第二个测试验证我们的晚餐是否有效，当晚餐具有具有有效值的所有属性设置时：</span><span class="sxs-lookup"><span data-stu-id="c052f-142">The second test verifies that our Dinner is valid when a Dinner has all properties set with valid values:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample2.cs)]

<span data-ttu-id="c052f-143">您在上面会注意到我们的测试名称非常明确（而且有些详细）。</span><span class="sxs-lookup"><span data-stu-id="c052f-143">You'll notice above that our test names are very explicit (and somewhat verbose).</span></span> <span data-ttu-id="c052f-144">我们这样做是因为我们可能最终创建数百或数千个小测试，我们希望能够轻松快速确定每个测试程序的意图和行为（尤其是在查看测试运行程序中的失败列表时）。</span><span class="sxs-lookup"><span data-stu-id="c052f-144">We are doing this because we might end up creating hundreds or thousands of small tests, and we want to make it easy to quickly determine the intent and behavior of each of them (especially when we are looking through a list of failures in a test runner).</span></span> <span data-ttu-id="c052f-145">测试名称应以测试的功能命名。</span><span class="sxs-lookup"><span data-stu-id="c052f-145">The test names should be named after the functionality they are testing.</span></span> <span data-ttu-id="c052f-146">上面我们使用的是"名词\_应该\_动词"命名模式。</span><span class="sxs-lookup"><span data-stu-id="c052f-146">Above we are using a "Noun\_Should\_Verb" naming pattern.</span></span>

<span data-ttu-id="c052f-147">我们使用"AAA"测试模式构建测试，该模式代表"安排、操作、断言"：</span><span class="sxs-lookup"><span data-stu-id="c052f-147">We are structuring the tests using the "AAA" testing pattern – which stands for "Arrange, Act, Assert":</span></span>

- <span data-ttu-id="c052f-148">排列：设置正在测试的装置</span><span class="sxs-lookup"><span data-stu-id="c052f-148">Arrange: Setup the unit being tested</span></span>
- <span data-ttu-id="c052f-149">操作：锻炼被测试的单位并捕获结果</span><span class="sxs-lookup"><span data-stu-id="c052f-149">Act: Exercise the unit under test and capture results</span></span>
- <span data-ttu-id="c052f-150">断言：验证行为</span><span class="sxs-lookup"><span data-stu-id="c052f-150">Assert: Verify the behavior</span></span>

<span data-ttu-id="c052f-151">当我们编写测试时，我们希望避免让单个测试执行太多操作。</span><span class="sxs-lookup"><span data-stu-id="c052f-151">When we write tests we want to avoid having the individual tests do too much.</span></span> <span data-ttu-id="c052f-152">相反，每个测试应只验证一个概念（这将使确定故障原因变得更加容易）。</span><span class="sxs-lookup"><span data-stu-id="c052f-152">Instead each test should verify only a single concept (which will make it much easier to pinpoint the cause of failures).</span></span> <span data-ttu-id="c052f-153">一个好的准则是尝试每个测试只有一个断言语句。</span><span class="sxs-lookup"><span data-stu-id="c052f-153">A good guideline is to try and only have a single assert statement for each test.</span></span> <span data-ttu-id="c052f-154">如果在测试方法中有多个断言语句，请确保它们都用于测试同一概念。</span><span class="sxs-lookup"><span data-stu-id="c052f-154">If you have more than one assert statement in a test method, make sure they are all being used to test the same concept.</span></span> <span data-ttu-id="c052f-155">如有疑问，再做一次测试。</span><span class="sxs-lookup"><span data-stu-id="c052f-155">When in doubt, make another test.</span></span>

### <a name="running-tests"></a><span data-ttu-id="c052f-156">正在运行测试</span><span class="sxs-lookup"><span data-stu-id="c052f-156">Running Tests</span></span>

<span data-ttu-id="c052f-157">Visual Studio 2008 专业版（和更高版本）包括一个内置测试运行程序，可用于在 IDE 中运行 Visual Studio 单元测试项目。</span><span class="sxs-lookup"><span data-stu-id="c052f-157">Visual Studio 2008 Professional (and higher editions) includes a built-in test runner that can be used to run Visual Studio Unit Test projects within the IDE.</span></span> <span data-ttu-id="c052f-158">我们可以选择解决方案菜单**中的"&gt;测试-&gt;运行-所有测试**"命令（或键入 Ctrl R，A）来运行我们所有的单元测试。</span><span class="sxs-lookup"><span data-stu-id="c052f-158">We can select the **Test-&gt;Run-&gt;All Tests in Solution** menu command (or type Ctrl R, A) to run all of our unit tests.</span></span> <span data-ttu-id="c052f-159">或者，我们可以将光标定位到特定的测试类或测试方法中，并使用**当前上下文菜单中的&gt;测试运行&gt;测试**命令（或键入 Ctrl R、T）来运行单元测试的子集。</span><span class="sxs-lookup"><span data-stu-id="c052f-159">Or alternatively we can position our cursor within a specific test class or test method and use the **Test-&gt;Run-&gt;Tests in Current Context** menu command (or type Ctrl R, T) to run a subset of the unit tests.</span></span>

<span data-ttu-id="c052f-160">让我们将光标定位在 DinnerTest 类中，并键入"Ctrl R，T"以运行我们刚刚定义的两个测试。</span><span class="sxs-lookup"><span data-stu-id="c052f-160">Let's position our cursor within the DinnerTest class and type "Ctrl R, T" to run the two tests we just defined.</span></span> <span data-ttu-id="c052f-161">当我们执行此操作时，Visual Studio 中将显示一个"测试结果"窗口，我们将看到其中列出的测试运行结果：</span><span class="sxs-lookup"><span data-stu-id="c052f-161">When we do this a "Test Results" window will appear within Visual Studio and we'll see the results of our test run listed within it:</span></span>

![](enable-automated-unit-testing/_static/image5.png)

<span data-ttu-id="c052f-162">*注意：默认情况下，VS 测试结果窗口不显示"类名称"列。您可以通过在"测试结果"窗口中右键单击并使用"添加/删除列"菜单命令来添加此内容。*</span><span class="sxs-lookup"><span data-stu-id="c052f-162">*Note: The VS test results window does not show the Class Name column by default. You can add this by right-clicking within the Test Results window and using the Add/Remove Columns menu command.*</span></span>

<span data-ttu-id="c052f-163">我们的两个测试只用了一小部分时间就可以运行了，正如您所看到的，它们都通过了。</span><span class="sxs-lookup"><span data-stu-id="c052f-163">Our two tests took only a fraction of a second to run – and as you can see they both passed.</span></span> <span data-ttu-id="c052f-164">现在，我们可以通过创建验证特定规则验证的其他测试来扩展它们，并涵盖我们添加到 Dinner 类的两种帮助方法 - IsUserHost（） 和 IsUser 注册（）。</span><span class="sxs-lookup"><span data-stu-id="c052f-164">We can now go on and augment them by creating additional tests that verify specific rule validations, as well as cover the two helper methods - IsUserHost() and IsUserRegistered() – that we added to the Dinner class.</span></span> <span data-ttu-id="c052f-165">为 Dinner 类提供所有这些测试将使将来向该课程添加新业务规则和验证变得更加简单和安全。</span><span class="sxs-lookup"><span data-stu-id="c052f-165">Having all these tests in place for the Dinner class will make it much easier and safer to add new business rules and validations to it in the future.</span></span> <span data-ttu-id="c052f-166">我们可以将新的规则逻辑添加到 Dinner，然后在几秒钟内验证它是否没有破坏我们以前的任何逻辑功能。</span><span class="sxs-lookup"><span data-stu-id="c052f-166">We can add our new rule logic to Dinner, and then within seconds verify that it hasn't broken any of our previous logic functionality.</span></span>

<span data-ttu-id="c052f-167">请注意，使用描述性测试名称如何便于快速了解每个测试正在验证的内容。</span><span class="sxs-lookup"><span data-stu-id="c052f-167">Notice how using a descriptive test name makes it easy to quickly understand what each test is verifying.</span></span> <span data-ttu-id="c052f-168">我建议使用 **"工具-&gt;选项"** 菜单命令，打开测试工具-&gt;测试执行配置屏幕，并选中"双击失败或不确定的单位测试结果显示测试中的失败点"复选框。</span><span class="sxs-lookup"><span data-stu-id="c052f-168">I recommend using the **Tools-&gt;Options** menu command, opening the Test Tools-&gt;Test Execution configuration screen, and checking the "Double-clicking a failed or inconclusive unit test result displays the point of failure in the test" checkbox.</span></span> <span data-ttu-id="c052f-169">这将允许您双击测试结果窗口中的故障，并立即跳转到断言失败。</span><span class="sxs-lookup"><span data-stu-id="c052f-169">This will allow you to double-click on a failure in the test results window and jump immediately to the assert failure.</span></span>

### <a name="creating-dinnerscontroller-unit-tests"></a><span data-ttu-id="c052f-170">创建晚餐控制器单元测试</span><span class="sxs-lookup"><span data-stu-id="c052f-170">Creating DinnersController Unit Tests</span></span>

<span data-ttu-id="c052f-171">现在，让我们创建一些单元测试，以验证我们的 DinnersController 功能。</span><span class="sxs-lookup"><span data-stu-id="c052f-171">Let's now create some unit tests that verify our DinnersController functionality.</span></span> <span data-ttu-id="c052f-172">我们将从右键单击测试项目中的"控制器"文件夹开始，然后选择 **"&gt;新增测试"** 菜单命令。</span><span class="sxs-lookup"><span data-stu-id="c052f-172">We'll start by right-clicking on the "Controllers" folder within our Test project and then choose the **Add-&gt;New Test** menu command.</span></span> <span data-ttu-id="c052f-173">我们将创建一个"单元测试"并将其命名为"DinnersControllerTest.cs"。</span><span class="sxs-lookup"><span data-stu-id="c052f-173">We'll create a "Unit Test" and name it "DinnersControllerTest.cs".</span></span>

<span data-ttu-id="c052f-174">我们将创建两种测试方法，以验证 DinnersController 上的细节（） 操作方法。</span><span class="sxs-lookup"><span data-stu-id="c052f-174">We'll create two test methods that verify the Details() action method on the DinnersController.</span></span> <span data-ttu-id="c052f-175">第一个将验证在请求现有晚餐时是否返回了视图。</span><span class="sxs-lookup"><span data-stu-id="c052f-175">The first will verify that a View is returned when an existing Dinner is requested.</span></span> <span data-ttu-id="c052f-176">第二个将验证在请求不存在的晚餐时是否返回"未找到"视图：</span><span class="sxs-lookup"><span data-stu-id="c052f-176">The second will verify that a "NotFound" view is returned when a non-existent Dinner is requested:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample3.cs)]

<span data-ttu-id="c052f-177">上述代码编译干净。</span><span class="sxs-lookup"><span data-stu-id="c052f-177">The above code compiles clean.</span></span> <span data-ttu-id="c052f-178">但是，当我们运行测试时，它们都失败：</span><span class="sxs-lookup"><span data-stu-id="c052f-178">When we run the tests, though, they both fail:</span></span>

![](enable-automated-unit-testing/_static/image6.png)

<span data-ttu-id="c052f-179">如果我们查看错误消息，我们将看到测试失败的原因是因为我们的 DinnersRepository 类无法连接到数据库。</span><span class="sxs-lookup"><span data-stu-id="c052f-179">If we look at the error messages, we'll see that the reason the tests failed was because our DinnersRepository class was unable to connect to a database.</span></span> <span data-ttu-id="c052f-180">我们的 NerdDinner 应用程序使用连接字符串到本地 SQL Server Express 文件，该文件位于\_NerdDinner 应用程序项目的 #App 数据目录下。</span><span class="sxs-lookup"><span data-stu-id="c052f-180">Our NerdDinner application is using a connection-string to a local SQL Server Express file which lives under the \App\_Data directory of the NerdDinner application project.</span></span> <span data-ttu-id="c052f-181">由于我们的 NerdDinner.测试项目编译并运行在不同的目录中，然后以应用程序项目运行，因此连接字符串的相对路径位置不正确。</span><span class="sxs-lookup"><span data-stu-id="c052f-181">Because our NerdDinner.Tests project compiles and runs in a different directory then the application project, the relative path location of our connection-string is incorrect.</span></span>

<span data-ttu-id="c052f-182">*我们可以*通过将 SQL Express 数据库文件复制到测试项目来解决此问题，然后在测试项目的 App.config 中向它添加适当的测试连接字符串。</span><span class="sxs-lookup"><span data-stu-id="c052f-182">We *could* fix this by copying the SQL Express database file to our test project, and then add an appropriate test connection-string to it in the App.config of our test project.</span></span> <span data-ttu-id="c052f-183">这将使上述测试解除阻止并运行。</span><span class="sxs-lookup"><span data-stu-id="c052f-183">This would get the above tests unblocked and running.</span></span>

<span data-ttu-id="c052f-184">但是，使用真实数据库的单位测试代码带来了许多挑战。</span><span class="sxs-lookup"><span data-stu-id="c052f-184">Unit testing code using a real database, though, brings with it a number of challenges.</span></span> <span data-ttu-id="c052f-185">具体来说：</span><span class="sxs-lookup"><span data-stu-id="c052f-185">Specifically:</span></span>

- <span data-ttu-id="c052f-186">它显著减慢了单元测试的执行时间。</span><span class="sxs-lookup"><span data-stu-id="c052f-186">It significantly slows down the execution time of unit tests.</span></span> <span data-ttu-id="c052f-187">运行测试所需的时间越长，执行测试的可能性就越小。</span><span class="sxs-lookup"><span data-stu-id="c052f-187">The longer it takes to run tests, the less likely you are to execute them frequently.</span></span> <span data-ttu-id="c052f-188">理想情况下，您希望单元测试能够在几秒钟内运行，并且让它像编译项目一样自然地完成。</span><span class="sxs-lookup"><span data-stu-id="c052f-188">Ideally you want your unit tests to be able to be run in seconds – and have it be something you do as naturally as compiling the project.</span></span>
- <span data-ttu-id="c052f-189">它在测试中使设置和清理逻辑复杂化。</span><span class="sxs-lookup"><span data-stu-id="c052f-189">It complicates the setup and cleanup logic within tests.</span></span> <span data-ttu-id="c052f-190">您希望每个单元测试都隔离并独立于其他测试（没有副作用或依赖项）。</span><span class="sxs-lookup"><span data-stu-id="c052f-190">You want each unit test to be isolated and independent of others (with no side effects or dependencies).</span></span> <span data-ttu-id="c052f-191">在对真实数据库工作时，您必须注意状态并在测试之间重置它。</span><span class="sxs-lookup"><span data-stu-id="c052f-191">When working against a real database you have to be mindful of state and reset it between tests.</span></span>

<span data-ttu-id="c052f-192">让我们来看看一种称为"依赖注入"的设计模式，它可以帮助我们解决这些问题，并避免使用真实数据库作为测试的需要。</span><span class="sxs-lookup"><span data-stu-id="c052f-192">Let's look at a design pattern called "dependency injection" that can help us work around these issues and avoid the need to use a real database with our tests.</span></span>

### <a name="dependency-injection"></a><span data-ttu-id="c052f-193">依赖关系注入</span><span class="sxs-lookup"><span data-stu-id="c052f-193">Dependency Injection</span></span>

<span data-ttu-id="c052f-194">现在，晚餐控制器与晚餐存储库类紧密地"耦合"。</span><span class="sxs-lookup"><span data-stu-id="c052f-194">Right now DinnersController is tightly "coupled" to the DinnerRepository class.</span></span> <span data-ttu-id="c052f-195">"耦合"是指类显式依赖于另一个类才能工作的情况：</span><span class="sxs-lookup"><span data-stu-id="c052f-195">"Coupling" refers to a situation where a class explicitly relies on another class in order to work:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample4.cs)]

<span data-ttu-id="c052f-196">由于 DinnerRepository 类需要访问数据库，因此 DinnersController 类在 DinnerRepository 上的紧密耦合依赖关系最终要求我们有一个数据库才能测试 DinnersController 操作方法。</span><span class="sxs-lookup"><span data-stu-id="c052f-196">Because the DinnerRepository class requires access to a database, the tightly coupled dependency the DinnersController class has on the DinnerRepository ends up requiring us to have a database in order for the DinnersController action methods to be tested.</span></span>

<span data-ttu-id="c052f-197">我们可以采用称为"依赖注入"的设计模式来克服这一问题，这种方法在使用依赖项（如提供数据访问的存储库类）中不再隐式创建。</span><span class="sxs-lookup"><span data-stu-id="c052f-197">We can get around this by employing a design pattern called "dependency injection" – which is an approach where dependencies (like repository classes that provide data access) are no longer implicitly created within classes that use them.</span></span> <span data-ttu-id="c052f-198">相反，依赖项可以显式传递给使用构造函数参数使用它们的类。</span><span class="sxs-lookup"><span data-stu-id="c052f-198">Instead, dependencies can be explicitly passed to the class that uses them using constructor arguments.</span></span> <span data-ttu-id="c052f-199">如果使用接口定义依赖项，则我们可以灵活地通过单元测试方案的"假"依赖项实现。</span><span class="sxs-lookup"><span data-stu-id="c052f-199">If the dependencies are defined using interfaces, we then have the flexibility to pass in "fake" dependency implementations for unit test scenarios.</span></span> <span data-ttu-id="c052f-200">这使我们能够创建实际上不需要访问数据库的特定于测试的依赖项实现。</span><span class="sxs-lookup"><span data-stu-id="c052f-200">This enables us to create test-specific dependency implementations that do not actually require access to a database.</span></span>

<span data-ttu-id="c052f-201">为了看到此操作，让我们使用 DinnersController 实现依赖项注入。</span><span class="sxs-lookup"><span data-stu-id="c052f-201">To see this in action, let's implement dependency injection with our DinnersController.</span></span>

#### <a name="extracting-an-idinnerrepository-interface"></a><span data-ttu-id="c052f-202">提取 IDinner 存储库界面</span><span class="sxs-lookup"><span data-stu-id="c052f-202">Extracting an IDinnerRepository interface</span></span>

<span data-ttu-id="c052f-203">我们的第一步是创建一个新的 IDinnerRepository 接口，该接口封装了控制器检索和更新 Dinner 所需的存储库合同。</span><span class="sxs-lookup"><span data-stu-id="c052f-203">Our first step will be to create a new IDinnerRepository interface that encapsulates the repository contract our controllers require to retrieve and update Dinners.</span></span>

<span data-ttu-id="c052f-204">我们可以手动定义此接口协定，通过右键单击 #Model 文件夹，然后选择 **"添加-&gt;新项目"** 菜单命令并创建名为 IDinnerRepository.cs的新接口。</span><span class="sxs-lookup"><span data-stu-id="c052f-204">We can define this interface contract manually by right-clicking on the \Models folder, and then choosing the **Add-&gt;New Item** menu command and creating a new interface named IDinnerRepository.cs.</span></span>

<span data-ttu-id="c052f-205">或者，我们可以使用内置于 Visual Studio 专业版（和更高版本）的重构工具，从现有的 DinnerRepository 类中自动提取和创建我们的界面。</span><span class="sxs-lookup"><span data-stu-id="c052f-205">Alternatively we can use the refactoring tools built-into Visual Studio Professional (and higher editions) to automatically extract and create an interface for us from our existing DinnerRepository class.</span></span> <span data-ttu-id="c052f-206">要使用 VS 提取此接口，只需将光标放在 DinnerRepository 类的文本编辑器中，然后右键单击并选择 **"重构-&gt;提取界面"** 菜单命令：</span><span class="sxs-lookup"><span data-stu-id="c052f-206">To extract this interface using VS, simply position the cursor in the text editor on the DinnerRepository class, and then right-click and choose the **Refactor-&gt;Extract Interface** menu command:</span></span>

![](enable-automated-unit-testing/_static/image7.png)

<span data-ttu-id="c052f-207">这将启动"提取接口"对话框，并提示我们创建接口的名称。</span><span class="sxs-lookup"><span data-stu-id="c052f-207">This will launch the "Extract Interface" dialog and prompt us for the name of the interface to create.</span></span> <span data-ttu-id="c052f-208">它将默认为 IDinnerRepository，并自动选择现有 DinnerRepository 类上的所有公共方法以添加到接口：</span><span class="sxs-lookup"><span data-stu-id="c052f-208">It will default to IDinnerRepository and automatically select all public methods on the existing DinnerRepository class to add to the interface:</span></span>

![](enable-automated-unit-testing/_static/image8.png)

<span data-ttu-id="c052f-209">当我们单击"确定"按钮时，Visual Studio 将为我们的应用程序添加新的 IDinnerRepository 界面：</span><span class="sxs-lookup"><span data-stu-id="c052f-209">When we click the "ok" button, Visual Studio will add a new IDinnerRepository interface to our application:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample5.cs)]

<span data-ttu-id="c052f-210">我们现有的 DinnerRepository 类将被更新，以便实现接口：</span><span class="sxs-lookup"><span data-stu-id="c052f-210">And our existing DinnerRepository class will be updated so that it implements the interface:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample6.cs)]

#### <a name="updating-dinnerscontroller-to-support-constructor-injection"></a><span data-ttu-id="c052f-211">更新晚餐控制器以支持构造函数注入</span><span class="sxs-lookup"><span data-stu-id="c052f-211">Updating DinnersController to support constructor injection</span></span>

<span data-ttu-id="c052f-212">现在，我们将更新 DinnersController 类以使用新接口。</span><span class="sxs-lookup"><span data-stu-id="c052f-212">We'll now update the DinnersController class to use the new interface.</span></span>

<span data-ttu-id="c052f-213">目前，晚餐控制器是硬编码的，因此其"晚餐存储库"字段始终是一个晚餐存储库类：</span><span class="sxs-lookup"><span data-stu-id="c052f-213">Currently DinnersController is hard-coded such that its "dinnerRepository" field is always a DinnerRepository class:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample7.cs)]

<span data-ttu-id="c052f-214">我们将更改它，以便"晚餐存储库"字段是 IDinner 存储库类型，而不是晚餐存储库。</span><span class="sxs-lookup"><span data-stu-id="c052f-214">We'll change it so that the "dinnerRepository" field is of type IDinnerRepository instead of DinnerRepository.</span></span> <span data-ttu-id="c052f-215">然后，我们将添加两个公共 DinnersController 构造函数。</span><span class="sxs-lookup"><span data-stu-id="c052f-215">We'll then add two public DinnersController constructors.</span></span> <span data-ttu-id="c052f-216">其中一个构造函数允许将 IDinnerRepository 作为参数传递。</span><span class="sxs-lookup"><span data-stu-id="c052f-216">One of the constructors allows an IDinnerRepository to be passed as an argument.</span></span> <span data-ttu-id="c052f-217">另一个是使用我们现有的 DinnerRepository 实现的默认构造函数：</span><span class="sxs-lookup"><span data-stu-id="c052f-217">The other is a default constructor that uses our existing DinnerRepository implementation:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample8.cs)]

<span data-ttu-id="c052f-218">由于默认情况下ASP.NET MVC 使用默认构造函数创建控制器类，因此运行时的 DinnersController 将继续使用 DinnerRepository 类来执行数据访问。</span><span class="sxs-lookup"><span data-stu-id="c052f-218">Because ASP.NET MVC by default creates controller classes using default constructors, our DinnersController at runtime will continue to use the DinnerRepository class to perform data access.</span></span>

<span data-ttu-id="c052f-219">但是，我们现在可以更新我们的单元测试，以便使用参数构造函数在"假"晚餐存储库实现中传递。</span><span class="sxs-lookup"><span data-stu-id="c052f-219">We can now update our unit tests, though, to pass in a "fake" dinner repository implementation using the parameter constructor.</span></span> <span data-ttu-id="c052f-220">此"假"晚餐存储库不需要访问真实数据库，而是使用内存中的示例数据。</span><span class="sxs-lookup"><span data-stu-id="c052f-220">This "fake" dinner repository will not require access to a real database, and instead will use in-memory sample data.</span></span>

#### <a name="creating-the-fakedinnerrepository-class"></a><span data-ttu-id="c052f-221">创建假晚餐存储库类</span><span class="sxs-lookup"><span data-stu-id="c052f-221">Creating the FakeDinnerRepository class</span></span>

<span data-ttu-id="c052f-222">让我们创建一个假晚餐存储库类。</span><span class="sxs-lookup"><span data-stu-id="c052f-222">Let's create a FakeDinnerRepository class.</span></span>

<span data-ttu-id="c052f-223">我们将首先在我们的NerdDinner.测试项目中创建一个"Fakes"目录，然后向它添加新的FakeDinnerRepository类（右键单击该文件夹并选择 **"添加-&gt;新类**"）：</span><span class="sxs-lookup"><span data-stu-id="c052f-223">We'll begin by creating a "Fakes" directory within our NerdDinner.Tests project and then add a new FakeDinnerRepository class to it (right-click on the folder and choose **Add-&gt;New Class**):</span></span>

![](enable-automated-unit-testing/_static/image9.png)

<span data-ttu-id="c052f-224">我们将更新代码，以便 FakeDinnerRepository 类实现 IDinnerRepository 接口。</span><span class="sxs-lookup"><span data-stu-id="c052f-224">We'll update the code so that the FakeDinnerRepository class implements the IDinnerRepository interface.</span></span> <span data-ttu-id="c052f-225">然后，我们可以右键单击它并选择"实现接口 IDinnerRepository"上下文菜单命令：</span><span class="sxs-lookup"><span data-stu-id="c052f-225">We can then right-click on it and choose the "Implement interface IDinnerRepository" context menu command:</span></span>

![](enable-automated-unit-testing/_static/image10.png)

<span data-ttu-id="c052f-226">这将导致 Visual Studio 自动将所有 IDinnerRepository 接口成员添加到我们的 FakeDinnerRepository 类，并包含默认的"存分之外"实现：</span><span class="sxs-lookup"><span data-stu-id="c052f-226">This will cause Visual Studio to automatically add all of the IDinnerRepository interface members to our FakeDinnerRepository class with default "stub out" implementations:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample9.cs)]

<span data-ttu-id="c052f-227">然后，我们可以更新 FakeDinnerRepository 实现，以处理作为构造函数参数传递给&lt;它的&gt;内存中列表晚餐集合：</span><span class="sxs-lookup"><span data-stu-id="c052f-227">We can then update the FakeDinnerRepository implementation to work off of an in-memory List&lt;Dinner&gt; collection passed to it as a constructor argument:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample10.cs)]

<span data-ttu-id="c052f-228">我们现在有一个假的 IDinnerRepository 实现，它不需要数据库，而是可以处理存储中晚餐对象列表。</span><span class="sxs-lookup"><span data-stu-id="c052f-228">We now have a fake IDinnerRepository implementation that does not require a database, and can instead work off an in-memory list of Dinner objects.</span></span>

#### <a name="using-the-fakedinnerrepository-with-unit-tests"></a><span data-ttu-id="c052f-229">将假晚餐存储库与单元测试一起使用</span><span class="sxs-lookup"><span data-stu-id="c052f-229">Using the FakeDinnerRepository with Unit Tests</span></span>

<span data-ttu-id="c052f-230">让我们返回到由于数据库不可用而较早失败的 DinnersController 单元测试。</span><span class="sxs-lookup"><span data-stu-id="c052f-230">Let's return to the DinnersController unit tests that failed earlier because the database wasn't available.</span></span> <span data-ttu-id="c052f-231">我们可以更新测试方法，使用以下代码将填充在内存中晚餐数据样本的假晚餐存储库更新给 DinnersController：</span><span class="sxs-lookup"><span data-stu-id="c052f-231">We can update the test methods to use a FakeDinnerRepository populated with sample in-memory Dinner data to the DinnersController using the code below:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample11.cs)]

<span data-ttu-id="c052f-232">现在，当我们运行这些测试时，它们都通过了：</span><span class="sxs-lookup"><span data-stu-id="c052f-232">And now when we run these tests they both pass:</span></span>

![](enable-automated-unit-testing/_static/image11.png)

<span data-ttu-id="c052f-233">最重要的是，它们只需一小部分秒才能运行，并且不需要任何复杂的设置/清理逻辑。</span><span class="sxs-lookup"><span data-stu-id="c052f-233">Best of all, they take only a fraction of a second to run, and do not require any complicated setup/cleanup logic.</span></span> <span data-ttu-id="c052f-234">我们现在可以单元测试所有我们的 DinnersController 操作方法代码（包括列表、分页、详细信息、创建、更新和删除），而无需连接到真正的数据库。</span><span class="sxs-lookup"><span data-stu-id="c052f-234">We can now unit test all of our DinnersController action method code (including listing, paging, details, create, update and delete) without ever needing to connect to a real database.</span></span>

| <span data-ttu-id="c052f-235">**侧主题：依赖项注入框架**</span><span class="sxs-lookup"><span data-stu-id="c052f-235">**Side Topic: Dependency Injection Frameworks**</span></span> |
| --- |
| <span data-ttu-id="c052f-236">执行手动依赖项注入（如上所示）工作正常，但随着应用程序中依赖项和组件数量的增加，维护起来确实变得更加困难。</span><span class="sxs-lookup"><span data-stu-id="c052f-236">Performing manual dependency injection (like we are above) works fine, but does become harder to maintain as the number of dependencies and components in an application increases.</span></span> <span data-ttu-id="c052f-237">.NET 存在多个依赖项注入框架，可帮助提供更多依赖项管理灵活性。</span><span class="sxs-lookup"><span data-stu-id="c052f-237">Several dependency injection frameworks exist for .NET that can help provide even more dependency management flexibility.</span></span> <span data-ttu-id="c052f-238">这些框架有时也称为"控制反转"（IoC） 容器，它们提供了机制，支持在运行时指定依赖项并将其传递给对象（通常使用构造函数注入）的额外配置支持级别。</span><span class="sxs-lookup"><span data-stu-id="c052f-238">These frameworks, also sometimes called "Inversion of Control" (IoC) containers, provide mechanisms that enable an additional level of configuration support for specifying and passing dependencies to objects at runtime (most often using constructor injection).</span></span> <span data-ttu-id="c052f-239">.NET 中一些较流行的 OSS 依赖项注入 / IOC 框架包括：AutoFac、Ninject、Spring.NET、结构映射和温莎。</span><span class="sxs-lookup"><span data-stu-id="c052f-239">Some of the more popular OSS Dependency Injection / IOC frameworks in .NET include: AutoFac, Ninject, Spring.NET, StructureMap, and Windsor.</span></span> <span data-ttu-id="c052f-240">ASP.NET MVC 公开扩展 API，使开发人员能够参与控制器的解析和实例化，并使依赖项注入/IoC 框架能够安全地集成到此过程中。</span><span class="sxs-lookup"><span data-stu-id="c052f-240">ASP.NET MVC exposes extensibility APIs that enable developers to participate in the resolution and instantiation of controllers, and which enables Dependency Injection / IoC frameworks to be cleanly integrated within this process.</span></span> <span data-ttu-id="c052f-241">使用 DI/IOC 框架还将使我们能够从 DinnersController 中删除默认构造函数 ， 这将完全消除它和 DinnerRepository 之间的耦合。</span><span class="sxs-lookup"><span data-stu-id="c052f-241">Using a DI/IOC framework would also enable us to remove the default constructor from our DinnersController – which would completely remove the coupling between it and the DinnerRepository.</span></span> <span data-ttu-id="c052f-242">我们不会使用依赖注入/IOC框架与我们的NerdDinner应用程序。</span><span class="sxs-lookup"><span data-stu-id="c052f-242">We won't be using a dependency injection / IOC framework with our NerdDinner application.</span></span> <span data-ttu-id="c052f-243">但是，如果NerdDinner代码库和功能的增长，我们可以考虑未来的问题。</span><span class="sxs-lookup"><span data-stu-id="c052f-243">But it is something we could consider for the future if the NerdDinner code-base and capabilities grew.</span></span> |

### <a name="creating-edit-action-unit-tests"></a><span data-ttu-id="c052f-244">创建编辑操作单元测试</span><span class="sxs-lookup"><span data-stu-id="c052f-244">Creating Edit Action Unit Tests</span></span>

<span data-ttu-id="c052f-245">现在，让我们创建一些单元测试，以验证 DinnersController 的编辑功能。</span><span class="sxs-lookup"><span data-stu-id="c052f-245">Let's now create some unit tests that verify the Edit functionality of the DinnersController.</span></span> <span data-ttu-id="c052f-246">我们将首先测试我们的编辑操作的 HTTP-GET 版本：</span><span class="sxs-lookup"><span data-stu-id="c052f-246">We'll start by testing the HTTP-GET version of our Edit action:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample12.cs)]

<span data-ttu-id="c052f-247">我们将创建一个测试，以验证在请求有效晚餐时，由 DinnerFormViewModel 对象支持的视图是否呈现回：</span><span class="sxs-lookup"><span data-stu-id="c052f-247">We'll create a test that verifies that a View backed by a DinnerFormViewModel object is rendered back when a valid dinner is requested:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample13.cs)]

<span data-ttu-id="c052f-248">但是，当我们运行测试时，我们会发现它失败，因为当 Edit 方法访问User.Identity.Name属性以执行 Dinner.Is托管By（） 检查时，将引发一个空引用异常。</span><span class="sxs-lookup"><span data-stu-id="c052f-248">When we run the test, though, we'll find that it fails because a null reference exception is thrown when the Edit method accesses the User.Identity.Name property to perform the Dinner.IsHostedBy() check.</span></span>

<span data-ttu-id="c052f-249">控制器基类上的 User 对象封装有关登录用户的详细信息，并在运行时创建控制器时由ASP.NET MVC 填充。</span><span class="sxs-lookup"><span data-stu-id="c052f-249">The User object on the Controller base class encapsulates details about the logged-in user, and is populated by ASP.NET MVC when it creates the controller at runtime.</span></span> <span data-ttu-id="c052f-250">由于我们在 Web 服务器环境之外测试 DinnersController，所以未设置用户对象（因此为空引用异常）。</span><span class="sxs-lookup"><span data-stu-id="c052f-250">Because we are testing the DinnersController outside of a web-server environment, the User object isn't set (hence the null reference exception).</span></span>

### <a name="mocking-the-useridentityname-property"></a><span data-ttu-id="c052f-251">模拟User.Identity.Name属性</span><span class="sxs-lookup"><span data-stu-id="c052f-251">Mocking the User.Identity.Name property</span></span>

<span data-ttu-id="c052f-252">模拟框架使我们能够动态创建支持测试的从属对象的假版本，从而使测试更容易。</span><span class="sxs-lookup"><span data-stu-id="c052f-252">Mocking frameworks make testing easier by enabling us to dynamically create fake versions of dependent objects that support our tests.</span></span> <span data-ttu-id="c052f-253">例如，我们可以在"编辑"操作测试中使用模拟框架动态创建一个用户对象，我们的 DinnersController 可用于查找模拟用户名。</span><span class="sxs-lookup"><span data-stu-id="c052f-253">For example, we can use a mocking framework in our Edit action test to dynamically create a User object that our DinnersController can use to lookup a simulated username.</span></span> <span data-ttu-id="c052f-254">这将避免在运行测试时引发空引用。</span><span class="sxs-lookup"><span data-stu-id="c052f-254">This will avoid a null reference from being thrown when we run our test.</span></span>

<span data-ttu-id="c052f-255">有许多 .NET 模拟框架可用于ASP.NET MVC（您可以在此处查看它们的列表： [http://www.mockframeworks.com/](http://www.mockframeworks.com/)</span><span class="sxs-lookup"><span data-stu-id="c052f-255">There are many .NET mocking frameworks that can be used with ASP.NET MVC (you can see a list of them here: [http://www.mockframeworks.com/](http://www.mockframeworks.com/)).</span></span> <span data-ttu-id="c052f-256">为了测试我们的NerdDinner应用程序，我们将使用一个开源模拟框架，称为"Moq"，可以从免费下载[http://www.mockframeworks.com/moq](http://www.mockframeworks.com/moq)。</span><span class="sxs-lookup"><span data-stu-id="c052f-256">For testing our NerdDinner application we'll use an open source mocking framework called "Moq", which can be downloaded for free from [http://www.mockframeworks.com/moq](http://www.mockframeworks.com/moq).</span></span>

<span data-ttu-id="c052f-257">下载后，我们将在 NerdDinner.测试项目中向 Moq.dll 程序集添加参考：</span><span class="sxs-lookup"><span data-stu-id="c052f-257">Once downloaded, we'll add a reference in our NerdDinner.Tests project to the Moq.dll assembly:</span></span>

![](enable-automated-unit-testing/_static/image12.png)

<span data-ttu-id="c052f-258">然后，我们将向测试类添加"创建 DinnerSControllerA（用户名）"帮助器方法，该方法以用户名作为参数，然后"模拟"DinnersController 实例上的User.Identity.Name属性：</span><span class="sxs-lookup"><span data-stu-id="c052f-258">We'll then add a "CreateDinnersControllerAs(username)" helper method to our test class that takes a username as a parameter, and which then "mocks" the User.Identity.Name property on the DinnersController instance:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample14.cs)]

<span data-ttu-id="c052f-259">上面，我们使用 Moq 创建一个模拟对象，该对象伪造了控制器上下文对象（ASP.NET MVC 传递给控制器类以公开运行时对象（如用户、请求、响应和会话）。</span><span class="sxs-lookup"><span data-stu-id="c052f-259">Above we are using Moq to create a Mock object that fakes a ControllerContext object (which is what ASP.NET MVC passes to Controller classes to expose runtime objects like User, Request, Response, and Session).</span></span> <span data-ttu-id="c052f-260">我们在 Mock 上调用"setupGet"方法，以指示 ControllerContext 上的HttpContext.User.Identity.Name属性应返回我们传递给帮助器方法的用户名字符串。</span><span class="sxs-lookup"><span data-stu-id="c052f-260">We are calling the "SetupGet" method on the Mock to indicate that the HttpContext.User.Identity.Name property on ControllerContext should return the username string we passed to the helper method.</span></span>

<span data-ttu-id="c052f-261">我们可以模拟任意数量的控制器上下文属性和方法。</span><span class="sxs-lookup"><span data-stu-id="c052f-261">We can mock any number of ControllerContext properties and methods.</span></span> <span data-ttu-id="c052f-262">为了说明这一点，我还为 Request.Is 验证属性添加了 SetupGet（） 调用（下面测试实际上不需要它，但这有助于说明如何模拟请求属性）。</span><span class="sxs-lookup"><span data-stu-id="c052f-262">To illustrate this I've also added a SetupGet() call for the Request.IsAuthenticated property (which isn't actually needed for the tests below – but which helps illustrate how you can mock Request properties).</span></span> <span data-ttu-id="c052f-263">完成后，我们将控制器上下文模拟的实例分配给 DinnersController，我们的帮助器方法返回。</span><span class="sxs-lookup"><span data-stu-id="c052f-263">When we are done we assign an instance of the ControllerContext mock to the DinnersController our helper method returns.</span></span>

<span data-ttu-id="c052f-264">现在，我们可以编写使用此帮助器方法测试涉及不同用户的编辑方案的单位测试：</span><span class="sxs-lookup"><span data-stu-id="c052f-264">We can now write unit tests that use this helper method to test Edit scenarios involving different users:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample15.cs)]

<span data-ttu-id="c052f-265">现在，当我们运行测试时，他们通过：</span><span class="sxs-lookup"><span data-stu-id="c052f-265">And now when we run the tests they pass:</span></span>

![](enable-automated-unit-testing/_static/image13.png)

### <a name="testing-updatemodel-scenarios"></a><span data-ttu-id="c052f-266">测试更新模型（）方案</span><span class="sxs-lookup"><span data-stu-id="c052f-266">Testing UpdateModel() scenarios</span></span>

<span data-ttu-id="c052f-267">我们创建了涵盖"编辑"操作的 HTTP-GET 版本的测试。</span><span class="sxs-lookup"><span data-stu-id="c052f-267">We've created tests that cover the HTTP-GET version of the Edit action.</span></span> <span data-ttu-id="c052f-268">现在，让我们创建一些测试来验证编辑操作的 HTTP-POST 版本：</span><span class="sxs-lookup"><span data-stu-id="c052f-268">Let's now create some tests that verify the HTTP-POST version of the Edit action:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample16.cs)]

<span data-ttu-id="c052f-269">我们支持此操作方法的有趣新测试方案是它在 Controller 基类上使用 UpdateModel（） 帮助器方法。</span><span class="sxs-lookup"><span data-stu-id="c052f-269">The interesting new testing scenario for us to support with this action method is its usage of the UpdateModel() helper method on the Controller base class.</span></span> <span data-ttu-id="c052f-270">我们使用此帮助器方法将表单发布值绑定到我们的 Dinner 对象实例。</span><span class="sxs-lookup"><span data-stu-id="c052f-270">We are using this helper method to bind form-post values to our Dinner object instance.</span></span>

<span data-ttu-id="c052f-271">下面是两个测试，它们演示如何为 UpdateModel（） 帮助器方法提供表单发布值。</span><span class="sxs-lookup"><span data-stu-id="c052f-271">Below are two tests that demonstrates how we can supply form posted values for the UpdateModel() helper method to use.</span></span> <span data-ttu-id="c052f-272">我们将通过创建和填充 FormCollection 对象来执行此操作，然后将其分配给控制器上的"ValueProvider"属性。</span><span class="sxs-lookup"><span data-stu-id="c052f-272">We'll do this by creating and populating a FormCollection object, and then assign it to the "ValueProvider" property on the Controller.</span></span>

<span data-ttu-id="c052f-273">第一个测试验证在成功保存浏览器时是否重定向到详细信息操作。</span><span class="sxs-lookup"><span data-stu-id="c052f-273">The first test verifies that on a successful save the browser is redirected to the details action.</span></span> <span data-ttu-id="c052f-274">第二个测试验证，当发布无效输入时，操作会再次用错误消息重新显示编辑视图。</span><span class="sxs-lookup"><span data-stu-id="c052f-274">The second test verifies that when invalid input is posted the action redisplays the edit view again with an error message.</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample17.cs)]

### <a name="testing-wrap-up"></a><span data-ttu-id="c052f-275">测试总结</span><span class="sxs-lookup"><span data-stu-id="c052f-275">Testing Wrap-Up</span></span>

<span data-ttu-id="c052f-276">我们介绍了单元测试控制器类中涉及的核心概念。</span><span class="sxs-lookup"><span data-stu-id="c052f-276">We've covered the core concepts involved in unit testing controller classes.</span></span> <span data-ttu-id="c052f-277">我们可以使用这些技术轻松创建数百个简单的测试，以验证我们应用程序的行为。</span><span class="sxs-lookup"><span data-stu-id="c052f-277">We can use these techniques to easily create hundreds of simple tests that verify the behavior of our application.</span></span>

<span data-ttu-id="c052f-278">由于我们的控制器和模型测试不需要真正的数据库，因此它们非常快速且易于运行。</span><span class="sxs-lookup"><span data-stu-id="c052f-278">Because our controller and model tests do not require a real database, they are extremely fast and easy to run.</span></span> <span data-ttu-id="c052f-279">我们将能够在数秒内执行数百个自动测试，并立即获得反馈，了解我们所做的更改是否违反了某些内容。</span><span class="sxs-lookup"><span data-stu-id="c052f-279">We'll be able to execute hundreds of automated tests in seconds, and immediately get feedback as to whether a change we made broke something.</span></span> <span data-ttu-id="c052f-280">这将有助于我们有信心不断改进、重构和改进我们的应用程序。</span><span class="sxs-lookup"><span data-stu-id="c052f-280">This will help provide us the confidence to continually improve, refactor, and refine our application.</span></span>

<span data-ttu-id="c052f-281">我们将测试作为本章的最后一个主题进行介绍，但不是因为测试是您在开发过程结束时应该做的！</span><span class="sxs-lookup"><span data-stu-id="c052f-281">We covered testing as the last topic in this chapter – but not because testing is something you should do at the end of a development process!</span></span> <span data-ttu-id="c052f-282">相反，您应该在开发过程中尽早编写自动化测试。</span><span class="sxs-lookup"><span data-stu-id="c052f-282">On the contrary, you should write automated tests as early as possible in your development process.</span></span> <span data-ttu-id="c052f-283">这样做使您能够在开发时立即获得反馈，帮助您仔细考虑应用程序的用例方案，并指导您设计应用程序时要牢记干净的分层和耦合。</span><span class="sxs-lookup"><span data-stu-id="c052f-283">Doing so enables you to get immediate feedback as you develop, helps you think thoughtfully about your application's use case scenarios, and guides you to design your application with clean layering and coupling in mind.</span></span>

<span data-ttu-id="c052f-284">本书的后一章将讨论测试驱动开发 （TDD）以及如何将其与 mVC ASP.NET一起使用。</span><span class="sxs-lookup"><span data-stu-id="c052f-284">A later chapter in the book will discuss Test Driven Development (TDD), and how to use it with ASP.NET MVC.</span></span> <span data-ttu-id="c052f-285">TDD 是一种迭代编码实践，您首先编写生成的代码将满足的测试。</span><span class="sxs-lookup"><span data-stu-id="c052f-285">TDD is an iterative coding practice where you first write the tests that your resulting code will satisfy.</span></span> <span data-ttu-id="c052f-286">使用 TDD，您首先创建一个测试，以验证即将实现的功能。</span><span class="sxs-lookup"><span data-stu-id="c052f-286">With TDD you begin each feature by creating a test that verifies the functionality you are about to implement.</span></span> <span data-ttu-id="c052f-287">首先编写单元测试有助于确保您清楚地了解该功能及其应该如何工作。</span><span class="sxs-lookup"><span data-stu-id="c052f-287">Writing the unit test first helps ensure that you clearly understand the feature and how it is supposed to work.</span></span> <span data-ttu-id="c052f-288">只有在编写测试（并且已验证测试失败）后，您才会实现测试验证的实际功能。</span><span class="sxs-lookup"><span data-stu-id="c052f-288">Only after the test is written (and you have verified that it fails) do you then implement the actual functionality the test verifies.</span></span> <span data-ttu-id="c052f-289">由于您已经花时间考虑了该功能应该如何工作的用例，因此您将更好地了解这些要求以及如何最好地实现这些要求。</span><span class="sxs-lookup"><span data-stu-id="c052f-289">Because you've already spent time thinking about the use case of how the feature is supposed to work, you will have a better understanding of the requirements and how best to implement them.</span></span> <span data-ttu-id="c052f-290">完成实现后，您可以重新运行测试，并立即获得有关该功能是否正常工作的反馈。</span><span class="sxs-lookup"><span data-stu-id="c052f-290">When you are done with the implementation you can re-run the test – and get immediate feedback as to whether the feature works correctly.</span></span> <span data-ttu-id="c052f-291">我们将在第 10 章中介绍 TDD。</span><span class="sxs-lookup"><span data-stu-id="c052f-291">We'll cover TDD more in Chapter 10.</span></span>

### <a name="next-step"></a><span data-ttu-id="c052f-292">下一步</span><span class="sxs-lookup"><span data-stu-id="c052f-292">Next Step</span></span>

<span data-ttu-id="c052f-293">一些最后的总结评论。</span><span class="sxs-lookup"><span data-stu-id="c052f-293">Some final wrap up comments.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="c052f-294">[上一页](use-ajax-to-implement-mapping-scenarios.md)
> [下一页](nerddinner-wrap-up.md)</span><span class="sxs-lookup"><span data-stu-id="c052f-294">[Previous](use-ajax-to-implement-mapping-scenarios.md)
[Next](nerddinner-wrap-up.md)</span></span>

---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part2
title: 添加控制器 |Microsoft Docs
author: shanselman
description: 如果本教程可在此处使用 Visual Studio 2013，则为已更新的版本。 新教程使用 ASP.NET MVC 5，它对 t 。
ms.author: riande
ms.date: 08/14/2010
ms.assetid: ff03dcc0-da97-458d-838f-0823e7482642
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part2
msc.type: authoredcontent
ms.openlocfilehash: e2a298584473f57c2b14edf507f0f6886d906ea3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78437564"
---
# <a name="adding-a-controller"></a><span data-ttu-id="4896a-104">添加控制器</span><span class="sxs-lookup"><span data-stu-id="4896a-104">Adding a Controller</span></span>

<span data-ttu-id="4896a-105">作者： [Scott Hanselman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="4896a-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> > [!NOTE]
> > <span data-ttu-id="4896a-106">如果本教程可在[此处](../../getting-started/introduction/getting-started.md)使用[Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)，则为已更新的版本。</span><span class="sxs-lookup"><span data-stu-id="4896a-106">An updated version if this tutorial is available [here](../../getting-started/introduction/getting-started.md) using [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013).</span></span> <span data-ttu-id="4896a-107">新教程使用 ASP.NET MVC 5，这在本教程中提供了许多改进。</span><span class="sxs-lookup"><span data-stu-id="4896a-107">The new tutorial uses ASP.NET MVC 5, which provides many improvements over this tutorial.</span></span>
>
>
> <span data-ttu-id="4896a-108">本教程介绍了 ASP.NET MVC 的基本知识。</span><span class="sxs-lookup"><span data-stu-id="4896a-108">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="4896a-109">你将创建一个简单的 web 应用程序，用于读取和写入数据库。</span><span class="sxs-lookup"><span data-stu-id="4896a-109">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="4896a-110">请访问[ASP.NET mvc 学习中心](../../../index.md)，查找其他 ASP.NET mvc 教程和示例。</span><span class="sxs-lookup"><span data-stu-id="4896a-110">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>

<span data-ttu-id="4896a-111">MVC 代表模型、视图和控制器。</span><span class="sxs-lookup"><span data-stu-id="4896a-111">MVC stands for Model, View, Controller.</span></span> <span data-ttu-id="4896a-112">MVC 是用于开发应用程序的一种模式，因此，每个部件具有不同于另一个的责任。</span><span class="sxs-lookup"><span data-stu-id="4896a-112">MVC is a pattern for developing applications such that each part has a responsibility that is different from another.</span></span>

- <span data-ttu-id="4896a-113">模型：应用程序的数据</span><span class="sxs-lookup"><span data-stu-id="4896a-113">Model: The data of your application</span></span>
- <span data-ttu-id="4896a-114">视图：你的应用程序将用于动态生成 HTML 响应的模板文件。</span><span class="sxs-lookup"><span data-stu-id="4896a-114">Views: The template files your application will use to dynamically generate HTML responses.</span></span>
- <span data-ttu-id="4896a-115">控制器：用于处理对应用程序的传入 URL 请求、检索模型数据，然后指定用于向客户端呈现响应的视图模板的类。</span><span class="sxs-lookup"><span data-stu-id="4896a-115">Controllers: Classes that handle incoming URL requests to the application, retrieve model data, and then specify view templates that render a response back to the client</span></span>

<span data-ttu-id="4896a-116">我们将在本教程中介绍所有这些概念，并说明如何使用它们来生成应用程序。</span><span class="sxs-lookup"><span data-stu-id="4896a-116">We'll be covering all these concepts in this tutorial and show you how to use them to build an application.</span></span>

<span data-ttu-id="4896a-117">让我们通过右键单击 "解决方案资源管理器" 中的 "控制器" 文件夹，然后选择 "添加控制器" 来创建新的控制器。</span><span class="sxs-lookup"><span data-stu-id="4896a-117">Let's create a new controller by right-clicking the controllers folder in the solution Explorer and selecting Add Controller.</span></span>

<span data-ttu-id="4896a-118">[![AddControllerRightClick](getting-started-with-mvc-part2/_static/image2.png)](getting-started-with-mvc-part2/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="4896a-118">[![AddControllerRightClick](getting-started-with-mvc-part2/_static/image2.png)](getting-started-with-mvc-part2/_static/image1.png)</span></span>

<span data-ttu-id="4896a-119">将新控制器命名为 "HelloWorldController"，并单击 "添加"。</span><span class="sxs-lookup"><span data-stu-id="4896a-119">Name your new controller "HelloWorldController" and click Add.</span></span>

<span data-ttu-id="4896a-120">[![添加控制器对话框](getting-started-with-mvc-part2/_static/image4.png)](getting-started-with-mvc-part2/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="4896a-120">[![Add Controller Dialog](getting-started-with-mvc-part2/_static/image4.png)](getting-started-with-mvc-part2/_static/image3.png)</span></span>

<span data-ttu-id="4896a-121">请注意，在右侧的 "解决方案资源管理器中，已为你创建了一个名为 HelloWorldController.cs 的新文件，并且该文件现在已在**IDE**中打开。</span><span class="sxs-lookup"><span data-stu-id="4896a-121">Notice in the Solution Explorer on the right that a new file has been created for you called HelloWorldController.cs and that file is now opened in the **IDE**.</span></span>

<span data-ttu-id="4896a-122">[![HelloWorldControllerCode](getting-started-with-mvc-part2/_static/image6.png)](getting-started-with-mvc-part2/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="4896a-122">[![HelloWorldControllerCode](getting-started-with-mvc-part2/_static/image6.png)](getting-started-with-mvc-part2/_static/image5.png)</span></span>

<span data-ttu-id="4896a-123">在新的公共类 HelloWorldController 中创建两个新的方法。</span><span class="sxs-lookup"><span data-stu-id="4896a-123">Create two new methods that look like this inside of your new public class HelloWorldController.</span></span> <span data-ttu-id="4896a-124">作为示例，我们将直接从控制器返回 HTML 字符串。</span><span class="sxs-lookup"><span data-stu-id="4896a-124">We'll return a string of HTML directly from our controller as an example.</span></span>

[!code-csharp[Main](getting-started-with-mvc-part2/samples/sample1.cs)]

<span data-ttu-id="4896a-125">控制器名为 HelloWorldController，新方法称为 Index。</span><span class="sxs-lookup"><span data-stu-id="4896a-125">Your Controller is named HelloWorldController and your new Method is called Index.</span></span> <span data-ttu-id="4896a-126">再次运行应用程序，就像之前一样（单击 "播放" 按钮或按 F5 执行此操作）。</span><span class="sxs-lookup"><span data-stu-id="4896a-126">Run your application again, just as before (click the play button or press F5 to do this).</span></span> <span data-ttu-id="4896a-127">浏览器启动后，请将地址栏中的路径更改为 `http://localhost:xx/HelloWorld` 其中 xx 是计算机选择的数字。</span><span class="sxs-lookup"><span data-stu-id="4896a-127">Once your browser has started up, change the path in the address bar to `http://localhost:xx/HelloWorld` where xx is whatever number your computer has chosen.</span></span> <span data-ttu-id="4896a-128">现在，浏览器应类似于下面的屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="4896a-128">Now your browser should look like the screenshot below.</span></span> <span data-ttu-id="4896a-129">在上面的方法中，我们返回了传递到名为 "Content" 的方法中的字符串。</span><span class="sxs-lookup"><span data-stu-id="4896a-129">In our method above we returned a string passed into a method called "Content."</span></span> <span data-ttu-id="4896a-130">我们告诉系统只返回了一些 HTML，但确实返回了！</span><span class="sxs-lookup"><span data-stu-id="4896a-130">We told the system just returns some HTML, and it did!</span></span>

<span data-ttu-id="4896a-131">ASP.NET MVC 根据传入 URL 调用不同的控制器类（以及其中的不同操作方法）。</span><span class="sxs-lookup"><span data-stu-id="4896a-131">ASP.NET MVC invokes different Controller classes (and different Action methods within them) depending on the incoming URL.</span></span> <span data-ttu-id="4896a-132">ASP.NET MVC 使用的默认映射逻辑使用如下格式来控制运行的代码：</span><span class="sxs-lookup"><span data-stu-id="4896a-132">The default mapping logic used by ASP.NET MVC uses a format like this to control what code is run:</span></span>

<span data-ttu-id="4896a-133">/[Controller]/[ActionName]/[Parameters]</span><span class="sxs-lookup"><span data-stu-id="4896a-133">/[Controller]/[ActionName]/[Parameters]</span></span>

<span data-ttu-id="4896a-134">URL 的第一部分确定要执行的控制器类。</span><span class="sxs-lookup"><span data-stu-id="4896a-134">The first part of the URL determines the Controller class to execute.</span></span> <span data-ttu-id="4896a-135">因此，/HelloWorld 映射到 HelloWorldController 类。</span><span class="sxs-lookup"><span data-stu-id="4896a-135">So /HelloWorld maps to the HelloWorldController class.</span></span> <span data-ttu-id="4896a-136">URL 的第二部分确定要执行的类的操作方法。</span><span class="sxs-lookup"><span data-stu-id="4896a-136">The second part of the URL determines the Action method on the class to execute.</span></span> <span data-ttu-id="4896a-137">因此，/HelloWorld/Index 将导致 HelloWorldController 类的 Index （）方法执行。</span><span class="sxs-lookup"><span data-stu-id="4896a-137">So /HelloWorld/Index would cause the Index() method of the HelloWorldController class to execute.</span></span> <span data-ttu-id="4896a-138">请注意，我们只需要访问上面的/HelloWorld，而方法索引是隐含的。</span><span class="sxs-lookup"><span data-stu-id="4896a-138">Notice that we only had to visit /HelloWorld above and the method Index was implied.</span></span> <span data-ttu-id="4896a-139">这是因为，如果未显式指定一个名为 "Index" 的方法，则该方法将在控制器上调用。</span><span class="sxs-lookup"><span data-stu-id="4896a-139">This is because a method named "Index" is the default method that will be called on a controller if one is not explicitly specified.</span></span>

<span data-ttu-id="4896a-140">[![这是我的默认操作](getting-started-with-mvc-part2/_static/image8.png)](getting-started-with-mvc-part2/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="4896a-140">[![This is my default action](getting-started-with-mvc-part2/_static/image8.png)](getting-started-with-mvc-part2/_static/image7.png)</span></span>

<span data-ttu-id="4896a-141">现在，我们来访问 `http://localhost:xx/HelloWorld/Welcome.` 现在我们的欢迎方法已执行，并返回其 HTML 字符串。</span><span class="sxs-lookup"><span data-stu-id="4896a-141">Now, let's visit `http://localhost:xx/HelloWorld/Welcome.` Now our Welcome Method has executed and returned its HTML string.</span></span>

<span data-ttu-id="4896a-142">同样，/[控制器]/[ActionName]/[参数] 因此控制器为 HelloWorld，欢迎是在这种情况下的方法。</span><span class="sxs-lookup"><span data-stu-id="4896a-142">Again, /[Controller]/[ActionName]/[Parameters] so Controller is HelloWorld and Welcome is the Method in this case.</span></span> <span data-ttu-id="4896a-143">尚未完成参数。</span><span class="sxs-lookup"><span data-stu-id="4896a-143">We haven't done Parameters yet.</span></span>

<span data-ttu-id="4896a-144">[![这是 "欢迎操作" 方法](getting-started-with-mvc-part2/_static/image10.png)](getting-started-with-mvc-part2/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="4896a-144">[![This is the Welcome action method](getting-started-with-mvc-part2/_static/image10.png)](getting-started-with-mvc-part2/_static/image9.png)</span></span>

<span data-ttu-id="4896a-145">让我们略微修改示例，以便我们可以将中的某些信息从 URL 传递到控制器，例如：/HelloWorld/Welcome？ name = Scott&amp;numtimes = 4。</span><span class="sxs-lookup"><span data-stu-id="4896a-145">Let's modify our sample slightly so that we can pass some information in from the URL to our controller, for example like this: /HelloWorld/Welcome?name=Scott&amp;numtimes=4.</span></span> <span data-ttu-id="4896a-146">更改你的欢迎方法以包含两个参数，并按如下所示进行更新。</span><span class="sxs-lookup"><span data-stu-id="4896a-146">Change your Welcome method to include two parameters and update it like below.</span></span> <span data-ttu-id="4896a-147">请注意，我们使用了C#可选的参数功能，指示如果不传入参数，numTimes 应默认为1。</span><span class="sxs-lookup"><span data-stu-id="4896a-147">Note that we've used the C# optional parameter feature to indicate that the parameter numTimes should default to 1 if it's not passed in.</span></span>

[!code-csharp[Main](getting-started-with-mvc-part2/samples/sample2.cs)]

<span data-ttu-id="4896a-148">运行应用程序，并访问 `http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4` 根据需要更改 name 和 numtimes 的值。</span><span class="sxs-lookup"><span data-stu-id="4896a-148">Run your application and visit `http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4` changing the value of name and numtimes as you like.</span></span> <span data-ttu-id="4896a-149">系统自动将命名参数从地址栏中的查询字符串映射到方法中的参数。</span><span class="sxs-lookup"><span data-stu-id="4896a-149">The system automatically mapped the named parameters from your query string in the address bar to parameters in your method.</span></span>

<span data-ttu-id="4896a-150">在这两个示例中，控制器都在执行所有工作，并且已直接返回 HTML。</span><span class="sxs-lookup"><span data-stu-id="4896a-150">In both these examples the controller has been doing all the work, and has been returning HTML directly.</span></span> <span data-ttu-id="4896a-151">通常情况下，我们不希望控制器直接返回 HTML，因为这样做的代码会非常麻烦。</span><span class="sxs-lookup"><span data-stu-id="4896a-151">Ordinarily we don't want our Controllers returning HTML directly - since that ends up being very cumbersome to code.</span></span> <span data-ttu-id="4896a-152">我们通常会使用单独的视图模板文件来帮助生成 HTML 响应。</span><span class="sxs-lookup"><span data-stu-id="4896a-152">Instead we'll typically use a separate View template file to help generate the HTML response.</span></span> <span data-ttu-id="4896a-153">我们来看看如何实现此目的。</span><span class="sxs-lookup"><span data-stu-id="4896a-153">Let's look at how we can do this.</span></span> <span data-ttu-id="4896a-154">关闭浏览器并返回到 IDE。</span><span class="sxs-lookup"><span data-stu-id="4896a-154">Close your browser and return to the IDE.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="4896a-155">[上一页](getting-started-with-mvc-part1.md)
> [下一页](getting-started-with-mvc-part3.md)</span><span class="sxs-lookup"><span data-stu-id="4896a-155">[Previous](getting-started-with-mvc-part1.md)
[Next](getting-started-with-mvc-part3.md)</span></span>

---
uid: web-api/overview/older-versions/build-restful-apis-with-aspnet-web-api
title: 通过 ASP.NET Web API-ASP.NET 4.x 生成 RESTful Api
author: rick-anderson
description: 动手实验：使用 ASP.NET 4.x 中的 Web API 生成联系人管理器应用程序的简单 REST API。
ms.author: riande
ms.date: 02/18/2013
ms.custom: seoapril2019
ms.assetid: 87daa99f-3810-407e-b969-dd28a192959d
msc.legacyurl: /web-api/overview/older-versions/build-restful-apis-with-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 72ce313c380547f74d5dc17d1aefbf7cf2da4bea
ms.sourcegitcommit: d4e2a07eeb2cdf19f0bfbfab4a469970bc7e1c99
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/12/2021
ms.locfileid: "98105281"
---
# <a name="build-restful-apis-with-aspnet-web-api"></a><span data-ttu-id="1d5c0-103">通过 ASP.NET Web API 生成 RESTful Api</span><span class="sxs-lookup"><span data-stu-id="1d5c0-103">Build RESTful APIs with ASP.NET Web API</span></span>

<span data-ttu-id="1d5c0-104">由[Web 训练营团队](https://twitter.com/webcamps)使用</span><span class="sxs-lookup"><span data-stu-id="1d5c0-104">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

> <span data-ttu-id="1d5c0-105">动手实验：使用 ASP.NET 4.x 中的 Web API 生成联系人管理器应用程序的简单 REST API。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-105">Hands on lab: Use Web API in ASP.NET 4.x to build a simple REST API for a contact manager application.</span></span> <span data-ttu-id="1d5c0-106">你还将生成一个使用 API 的客户端。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-106">You will also build a client to consume the API.</span></span>

<span data-ttu-id="1d5c0-107">在最近几年中，它已变得清楚： HTTP 并非仅用于提供 HTML 页面。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-107">In recent years, it has become clear that HTTP is not just for serving up HTML pages.</span></span> <span data-ttu-id="1d5c0-108">它也是一个功能强大的平台，用于生成 Web Api，使用几个谓词 (GET、POST 等) 加上一些简单的概念，如 *uri* 和 *标头*。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-108">It is also a powerful platform for building Web APIs, using a handful of verbs (GET, POST, and so forth) plus a few simple concepts such as *URIs* and *headers*.</span></span> <span data-ttu-id="1d5c0-109">ASP.NET Web API 是一组可简化 HTTP 编程的组件。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-109">ASP.NET Web API is a set of components that simplify HTTP programming.</span></span> <span data-ttu-id="1d5c0-110">由于它是在 ASP.NET MVC 运行时的基础上构建的，因此 Web API 会自动处理 HTTP 的低级传输细节。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-110">Because it is built on top of the ASP.NET MVC runtime, Web API automatically handles the low-level transport details of HTTP.</span></span> <span data-ttu-id="1d5c0-111">同时，Web API 自然公开 HTTP 编程模型。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-111">At the same time, Web API naturally exposes the HTTP programming model.</span></span> <span data-ttu-id="1d5c0-112">事实上，Web API 的一个目标是 *不* 会抽象出 HTTP 的现实。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-112">In fact, one goal of Web API is to *not* abstract away the reality of HTTP.</span></span> <span data-ttu-id="1d5c0-113">因此，Web API 既灵活又易于扩展。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-113">As a result, Web API is both flexible and easy to extend.</span></span>  <span data-ttu-id="1d5c0-114">已证明 REST 体系结构样式是利用 HTTP 的有效方法，但它当然不是 HTTP 的唯一有效方法。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-114">The REST architectural style has proven to be an effective way to leverage HTTP - although it is certainly not the only valid approach to HTTP.</span></span> <span data-ttu-id="1d5c0-115">联系人管理器将公开 RESTful 以列出、添加和删除联系人，等等。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-115">The contact manager will expose the RESTful for listing, adding and removing contacts, among others.</span></span> 

<span data-ttu-id="1d5c0-116">此实验室需要基本了解 HTTP、REST，并假定你具有 HTML、JavaScript 和 jQuery 的基本工作知识。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-116">This lab requires a basic understanding of HTTP, REST, and assumes you have a basic working knowledge of HTML, JavaScript, and jQuery.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="1d5c0-117">ASP.NET 网站有一个专用于 ASP.NET Web API 框架的区域 [https://asp.net/web-api](https://asp.net/web-api) 。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-117">The ASP.NET Web site has an area dedicated to the ASP.NET Web API framework at [https://asp.net/web-api](https://asp.net/web-api).</span></span> <span data-ttu-id="1d5c0-118">此站点将继续提供与 Web API 相关的最新信息、示例和新闻，因此，如果想要深入了解如何创建可用于几乎任何设备或开发框架的自定义 Web Api，请经常查看。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-118">This site will continue to provide late-breaking information, samples, and news related to Web API, so check it frequently if you'd like to delve deeper into the art of creating custom Web APIs available to virtually any device or development framework.</span></span>
> > 
> > <span data-ttu-id="1d5c0-119">与 ASP.NET MVC 4 类似，ASP.NET Web API，在将服务层与控制器分离时具有很大的灵活性，使您可以很轻松地使用几个可用的依赖项注入框架。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-119">ASP.NET Web API, similar to ASP.NET MVC 4, has great flexibility in terms of separating the service layer from the controllers allowing you to use several of the available Dependency Injection frameworks fairly easy.</span></span> 
> 
> 
> <span data-ttu-id="1d5c0-120">所有示例代码和代码段都包含在 Web 训练营培训工具包中，可从获取 [https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409) 。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-120">All sample code and snippets are included in the Web Camps Training Kit, available at [https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409).</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="1d5c0-121">目标</span><span class="sxs-lookup"><span data-stu-id="1d5c0-121">Objectives</span></span>

<span data-ttu-id="1d5c0-122">在本动手实验中，您将了解如何：</span><span class="sxs-lookup"><span data-stu-id="1d5c0-122">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="1d5c0-123">实现 RESTful Web API</span><span class="sxs-lookup"><span data-stu-id="1d5c0-123">Implement a RESTful Web API</span></span>
- <span data-ttu-id="1d5c0-124">从 HTML 客户端调用 API</span><span class="sxs-lookup"><span data-stu-id="1d5c0-124">Call the API from an HTML client</span></span>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="1d5c0-125">必备知识</span><span class="sxs-lookup"><span data-stu-id="1d5c0-125">Prerequisites</span></span>

<span data-ttu-id="1d5c0-126">完成本动手实验需要以下各项：</span><span class="sxs-lookup"><span data-stu-id="1d5c0-126">The following is required to complete this hands-on lab:</span></span>

- <span data-ttu-id="1d5c0-127">适用于 Web 或高级 ([的 Microsoft Visual Studio Express 2012](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web)阅读[附录 B](#AppendixB) ，了解有关如何) 安装它的说明。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-127">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix B](#AppendixB) for instructions on how to install it).</span></span>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="1d5c0-128">设置</span><span class="sxs-lookup"><span data-stu-id="1d5c0-128">Setup</span></span>

<span data-ttu-id="1d5c0-129">**安装代码片段**</span><span class="sxs-lookup"><span data-stu-id="1d5c0-129">**Installing Code Snippets**</span></span>

<span data-ttu-id="1d5c0-130">为方便起见，你将通过此实验室管理的大部分代码都作为 Visual Studio code 片段提供。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-130">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="1d5c0-131">若要安装代码段，请运行 **.\Source\Setup\CodeSnippets.vsi** 文件。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-131">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="1d5c0-132">如果你不熟悉 Visual Studio Code 代码段，并且想要了解如何使用它们，则可以参考本文档中的附录 &quot; [A：使用代码片段](#AppendixA) &quot; 。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-132">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix A: Using Code Snippets](#AppendixA)&quot;.</span></span>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="1d5c0-133">练习</span><span class="sxs-lookup"><span data-stu-id="1d5c0-133">Exercises</span></span>

<span data-ttu-id="1d5c0-134">此动手实验包括以下练习：</span><span class="sxs-lookup"><span data-stu-id="1d5c0-134">This hands-on lab includes the following exercise:</span></span>

1. [<span data-ttu-id="1d5c0-135">练习1：创建 Read-Only Web API</span><span class="sxs-lookup"><span data-stu-id="1d5c0-135">Exercise 1: Create a Read-Only Web API</span></span>](#Exercise1)
2. [<span data-ttu-id="1d5c0-136">练习2：创建读/写 Web API</span><span class="sxs-lookup"><span data-stu-id="1d5c0-136">Exercise 2: Create a Read/Write Web API</span></span>](#Exercise2)
3. [<span data-ttu-id="1d5c0-137">练习3：使用 HTML 客户端中的 Web API</span><span class="sxs-lookup"><span data-stu-id="1d5c0-137">Exercise 3: Consume the Web API from an HTML Client</span></span>](#Exercise3)

> [!NOTE]
> <span data-ttu-id="1d5c0-138">每个练习都带有一个 **结束** 文件夹，其中包含在完成练习后应获得的结果解决方案。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-138">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="1d5c0-139">如果需要更多帮助，请使用此解决方案作为指导。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-139">You can use this solution as a guide if you need additional help working through the exercises.</span></span>

<span data-ttu-id="1d5c0-140">完成本实验的估计时间： **60 分钟**。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-140">Estimated time to complete this lab: **60 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Create_a_Read-Only_Web_API"></a>
### <a name="exercise-1-create-a-read-only-web-api"></a><span data-ttu-id="1d5c0-141">练习1：创建 Read-Only Web API</span><span class="sxs-lookup"><span data-stu-id="1d5c0-141">Exercise 1: Create a Read-Only Web API</span></span>

<span data-ttu-id="1d5c0-142">在此练习中，您将实现联系人管理器的只读 GET 方法。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-142">In this exercise, you will implement the read-only GET methods for the contact manager.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_the_API_Project"></a>
#### <a name="task-1---creating-the-api-project"></a><span data-ttu-id="1d5c0-143">任务 1-创建 API 项目</span><span class="sxs-lookup"><span data-stu-id="1d5c0-143">Task 1 - Creating the API Project</span></span>

<span data-ttu-id="1d5c0-144">在此任务中，你将使用新的 ASP.NET web 项目模板创建 Web API web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-144">In this task, you will use the new ASP.NET web project templates to create a Web API web application.</span></span>

1. <span data-ttu-id="1d5c0-145">运行 **Visual Studio 2012 Express For Web**，若要执行此操作，请单击 " **开始** "，然后键入 **VS Express for Web** 然后按 **enter**。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-145">Run **Visual Studio 2012 Express for Web**, to do this go to **Start** and type **VS Express for Web** then press **Enter**.</span></span>
2. <span data-ttu-id="1d5c0-146">从 " **文件** " 菜单中选择 " **新建项目**"。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-146">From the **File** menu, select **New Project**.</span></span> <span data-ttu-id="1d5c0-147">选择 **Visual c # |** "项目类型" 树视图中的 "web 项目类型"，然后选择 " **ASP.NET MVC 4 Web 应用程序** " 项目类型。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-147">Select the **Visual C# | Web** project type from the project type tree view, then select the **ASP.NET MVC 4 Web Application** project type.</span></span> <span data-ttu-id="1d5c0-148">将项目的 **名称** 设置为 *ContactManager* ，将 **解决方案名称** 设置为 " *开始*"，然后单击 **"确定"**。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-148">Set the project's **Name** to *ContactManager* and the **Solution name** to *Begin*, then click **OK**.</span></span>

    <span data-ttu-id="1d5c0-149">![创建新的 ASP.NET MVC 4.0 Web 应用程序项目](build-restful-apis-with-aspnet-web-api/_static/image1.png "创建新的 ASP.NET MVC 4.0 Web 应用程序项目")</span><span class="sxs-lookup"><span data-stu-id="1d5c0-149">![Creating a new ASP.NET MVC 4.0 Web Application Project](build-restful-apis-with-aspnet-web-api/_static/image1.png "Creating a new ASP.NET MVC 4.0 Web Application Project")</span></span>

    <span data-ttu-id="1d5c0-150">*创建新的 ASP.NET MVC 4.0 Web 应用程序项目*</span><span class="sxs-lookup"><span data-stu-id="1d5c0-150">*Creating a new ASP.NET MVC 4.0 Web Application Project*</span></span>
3. <span data-ttu-id="1d5c0-151">在 "ASP.NET MVC 4 项目类型" 对话框中，选择 " **WEB API** " 项目类型。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-151">In the ASP.NET MVC 4 project type dialog, select the **Web API** project type.</span></span> <span data-ttu-id="1d5c0-152">单击“确定”。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-152">Click **OK**.</span></span>

    <span data-ttu-id="1d5c0-153">![指定 Web API 项目类型](build-restful-apis-with-aspnet-web-api/_static/image2.png "指定 Web API 项目类型")</span><span class="sxs-lookup"><span data-stu-id="1d5c0-153">![Specifying the Web API project type](build-restful-apis-with-aspnet-web-api/_static/image2.png "Specifying the Web API project type")</span></span>

    <span data-ttu-id="1d5c0-154">*指定 Web API 项目类型*</span><span class="sxs-lookup"><span data-stu-id="1d5c0-154">*Specifying the Web API project type*</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Creating_the_Contact_Manager_API_Controllers"></a>
#### <a name="task-2---creating-the-contact-manager-api-controllers"></a><span data-ttu-id="1d5c0-155">任务 2-创建联系人管理器 API 控制器</span><span class="sxs-lookup"><span data-stu-id="1d5c0-155">Task 2 - Creating the Contact Manager API Controllers</span></span>

<span data-ttu-id="1d5c0-156">在此任务中，将创建 API 方法将驻留的控制器类。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-156">In this task, you will create the controller classes in which API methods will reside.</span></span>

1. <span data-ttu-id="1d5c0-157">从项目中删除 "**控制器**" 文件夹中名为 " **ValuesController.cs** " 的文件。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-157">Delete the file named **ValuesController.cs** within **Controllers** folder from the project.</span></span>
2. <span data-ttu-id="1d5c0-158">右键单击项目中的 " **控制器** " 文件夹，然后选择 " **添加 |** 上下文菜单中的 "控制器"。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-158">Right-click the **Controllers** folder in the project and select **Add | Controller** from the context menu.</span></span>

    <span data-ttu-id="1d5c0-159">![向项目添加新控制器](build-restful-apis-with-aspnet-web-api/_static/image3.png "向项目添加新控制器")</span><span class="sxs-lookup"><span data-stu-id="1d5c0-159">![Adding a new controller to the project](build-restful-apis-with-aspnet-web-api/_static/image3.png "Adding a new controller to the project")</span></span>

    <span data-ttu-id="1d5c0-160">*向项目添加新控制器*</span><span class="sxs-lookup"><span data-stu-id="1d5c0-160">*Adding a new controller to the project*</span></span>
3. <span data-ttu-id="1d5c0-161">在出现的 " **添加控制器** " 对话框中，从 "模板" 菜单中选择 " **空 API 控制器** "。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-161">In the **Add Controller** dialog that appears, select **Empty API Controller** from the Template menu.</span></span> <span data-ttu-id="1d5c0-162">将 controller 类命名为 **ContactController**。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-162">Name the controller class **ContactController**.</span></span> <span data-ttu-id="1d5c0-163">然后单击 " **添加"。**</span><span class="sxs-lookup"><span data-stu-id="1d5c0-163">Then, click **Add.**</span></span>

    <span data-ttu-id="1d5c0-164">![使用 "添加控制器" 对话框创建新的 Web API 控制器](build-restful-apis-with-aspnet-web-api/_static/image4.png "使用 "添加控制器" 对话框创建新的 Web API 控制器")</span><span class="sxs-lookup"><span data-stu-id="1d5c0-164">![Using the Add Controller dialog to create a new Web API controller](build-restful-apis-with-aspnet-web-api/_static/image4.png "Using the Add Controller dialog to create a new Web API controller")</span></span>

    <span data-ttu-id="1d5c0-165">*使用 "添加控制器" 对话框创建新的 Web API 控制器*</span><span class="sxs-lookup"><span data-stu-id="1d5c0-165">*Using the Add Controller dialog to create a new Web API controller*</span></span>
4. <span data-ttu-id="1d5c0-166">将以下代码添加到 **ContactController** 中。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-166">Add the following code to the **ContactController**.</span></span>

    <span data-ttu-id="1d5c0-167"> (代码片段- *WEB API Ex01-获取 API 方法*) </span><span class="sxs-lookup"><span data-stu-id="1d5c0-167">(Code Snippet - *Web API Lab - Ex01 - Get API Method*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample1.cs)]
5. <span data-ttu-id="1d5c0-168">按 **F5** 调试应用程序。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-168">Press **F5** to debug the application.</span></span> <span data-ttu-id="1d5c0-169">Web API 项目的默认主页应该会出现。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-169">The default home page for a Web API project should appear.</span></span>

    <span data-ttu-id="1d5c0-170">![ASP.NET Web API 应用程序的默认主页](build-restful-apis-with-aspnet-web-api/_static/image5.png "ASP.NET Web API 应用程序的默认主页")</span><span class="sxs-lookup"><span data-stu-id="1d5c0-170">![The default home page of an ASP.NET Web API application](build-restful-apis-with-aspnet-web-api/_static/image5.png "The default home page of an ASP.NET Web API application")</span></span>

    <span data-ttu-id="1d5c0-171">*ASP.NET Web API 应用程序的默认主页*</span><span class="sxs-lookup"><span data-stu-id="1d5c0-171">*The default home page of an ASP.NET Web API application*</span></span>
6. <span data-ttu-id="1d5c0-172">在 Internet Explorer 窗口中，按 **F12** 键打开 " **开发人员工具** " 窗口。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-172">In the Internet Explorer window, press the **F12** key to open the **Developer Tools** window.</span></span> <span data-ttu-id="1d5c0-173">单击 " **网络** " 选项卡，然后单击 " **开始捕获** " 按钮，开始将网络流量捕获到该窗口中。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-173">Click the **Network** tab, and then click the **Start Capturing** button to begin capturing network traffic into the window.</span></span>

    <span data-ttu-id="1d5c0-174">![打开 "网络" 选项卡并启动网络捕获](build-restful-apis-with-aspnet-web-api/_static/image6.png "打开 "网络" 选项卡并启动网络捕获")</span><span class="sxs-lookup"><span data-stu-id="1d5c0-174">![Opening the network tab and initiating network capture](build-restful-apis-with-aspnet-web-api/_static/image6.png "Opening the network tab and initiating network capture")</span></span>

    <span data-ttu-id="1d5c0-175">*打开 "网络" 选项卡并启动网络捕获*</span><span class="sxs-lookup"><span data-stu-id="1d5c0-175">*Opening the network tab and initiating network capture*</span></span>
7. <span data-ttu-id="1d5c0-176">在浏览器的地址栏中追加 **/api/contact** ，并按 enter。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-176">Append the URL in the browser's address bar with **/api/contact** and press enter.</span></span> <span data-ttu-id="1d5c0-177">传输详细信息将出现在 "网络捕获" 窗口中。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-177">The transmission details will appear in the network capture window.</span></span> <span data-ttu-id="1d5c0-178">请注意，响应的 MIME 类型为 **application/json**。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-178">Note that the response's MIME type is **application/json**.</span></span> <span data-ttu-id="1d5c0-179">这说明了默认输出格式为 JSON。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-179">This demonstrates how the default output format is JSON.</span></span>

    <span data-ttu-id="1d5c0-180">![在 "网络" 视图中查看 Web API 请求的输出](build-restful-apis-with-aspnet-web-api/_static/image7.png "在 "网络" 视图中查看 Web API 请求的输出")</span><span class="sxs-lookup"><span data-stu-id="1d5c0-180">![Viewing the output of the Web API request in the Network view](build-restful-apis-with-aspnet-web-api/_static/image7.png "Viewing the output of the Web API request in the Network view")</span></span>

    <span data-ttu-id="1d5c0-181">*在 "网络" 视图中查看 Web API 请求的输出*</span><span class="sxs-lookup"><span data-stu-id="1d5c0-181">*Viewing the output of the Web API request in the Network view*</span></span>

    > [!NOTE]
    > <span data-ttu-id="1d5c0-182">此时，Internet Explorer 10 的默认行为将询问用户是否想要保存或打开由 Web API 调用导致的流。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-182">Internet Explorer 10's default behavior at this point will be to ask if the user would like to save or open the stream resulting from the Web API call.</span></span> <span data-ttu-id="1d5c0-183">输出将是一个文本文件，其中包含 Web API URL 调用的 JSON 结果。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-183">The output will be a text file containing the JSON result of the Web API URL call.</span></span> <span data-ttu-id="1d5c0-184">不要取消对话框以便能够通过 "开发人员工具" 窗口监视响应的内容。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-184">Do not cancel the dialog in order to be able to watch the response's content through Developers Tool window.</span></span>
8. <span data-ttu-id="1d5c0-185">单击 " **中转到详细视图** " 按钮，查看有关此 API 调用响应的详细信息。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-185">Click the **Go to detailed view** button to see more details about the response of this API call.</span></span>

    <span data-ttu-id="1d5c0-186">![切换到详细视图](build-restful-apis-with-aspnet-web-api/_static/image8.png "切换到详细信息视图")</span><span class="sxs-lookup"><span data-stu-id="1d5c0-186">![Switch to Detailed View](build-restful-apis-with-aspnet-web-api/_static/image8.png "Switch to Details View")</span></span>

    <span data-ttu-id="1d5c0-187">*切换到详细视图*</span><span class="sxs-lookup"><span data-stu-id="1d5c0-187">*Switch to Detailed View*</span></span>
9. <span data-ttu-id="1d5c0-188">单击 " **响应正文** " 选项卡以查看实际的 JSON 响应文本。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-188">Click the **Response body** tab to view the actual JSON response text.</span></span>

    <span data-ttu-id="1d5c0-189">![查看网络监视器中的 JSON 输出文本](build-restful-apis-with-aspnet-web-api/_static/image9.png "查看网络监视器中的 JSON 输出文本")</span><span class="sxs-lookup"><span data-stu-id="1d5c0-189">![Viewing the JSON output text in the network monitor](build-restful-apis-with-aspnet-web-api/_static/image9.png "Viewing the JSON output text in the network monitor")</span></span>

    <span data-ttu-id="1d5c0-190">*查看网络监视器中的 JSON 输出文本*</span><span class="sxs-lookup"><span data-stu-id="1d5c0-190">*Viewing the JSON output text in the network monitor*</span></span>

<a id="Ex1Task3"></a>

<a id="Task_3_-_Creating_the_Contact_Models_and_Augment_the_Contact_Controller"></a>
#### <a name="task-3---creating-the-contact-models-and-augment-the-contact-controller"></a><span data-ttu-id="1d5c0-191">任务 3-创建联系人模型并增强联系人控制器</span><span class="sxs-lookup"><span data-stu-id="1d5c0-191">Task 3 - Creating the Contact Models and Augment the Contact Controller</span></span>

<span data-ttu-id="1d5c0-192">在此任务中，将创建 API 方法将驻留的控制器类。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-192">In this task, you will create the controller classes in which API methods will reside.</span></span>

1. <span data-ttu-id="1d5c0-193">右键单击 " **模型** " 文件夹，然后选择 " **添加 |类 ...** 从上下文菜单中。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-193">Right-click the **Models** folder and select **Add | Class...** from the context menu.</span></span>

    <span data-ttu-id="1d5c0-194">![向 web 应用程序添加新模型](build-restful-apis-with-aspnet-web-api/_static/image10.png "向 web 应用程序添加新模型")</span><span class="sxs-lookup"><span data-stu-id="1d5c0-194">![Adding a new model to the web application](build-restful-apis-with-aspnet-web-api/_static/image10.png "Adding a new model to the web application")</span></span>

    <span data-ttu-id="1d5c0-195">*向 web 应用程序添加新模型*</span><span class="sxs-lookup"><span data-stu-id="1d5c0-195">*Adding a new model to the web application*</span></span>
2. <span data-ttu-id="1d5c0-196">在 " **添加新项** " 对话框中，将新文件命名为 **Contact.cs** ，然后单击 " **添加"。**</span><span class="sxs-lookup"><span data-stu-id="1d5c0-196">In the **Add New Item** dialog, name the new file **Contact.cs** and click **Add.**</span></span>

    <span data-ttu-id="1d5c0-197">![创建新的 Contact 类文件](build-restful-apis-with-aspnet-web-api/_static/image11.png "创建新的 Contact 类文件")</span><span class="sxs-lookup"><span data-stu-id="1d5c0-197">![Creating the new Contact class file](build-restful-apis-with-aspnet-web-api/_static/image11.png "Creating the new Contact class file")</span></span>

    <span data-ttu-id="1d5c0-198">*创建新的 Contact 类文件*</span><span class="sxs-lookup"><span data-stu-id="1d5c0-198">*Creating the new Contact class file*</span></span>
3. <span data-ttu-id="1d5c0-199">将以下突出显示的代码添加到 **Contact** 类。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-199">Add the following highlighted code to the **Contact** class.</span></span>

    <span data-ttu-id="1d5c0-200"> (代码片段- *WEB API Ex01-Contact 类*) </span><span class="sxs-lookup"><span data-stu-id="1d5c0-200">(Code Snippet - *Web API Lab - Ex01 - Contact Class*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample2.cs)]
4. <span data-ttu-id="1d5c0-201">在 **ContactController** 类中，选择 **Get** 方法的 "方法定义" 中的单词 **字符串**，然后键入 "*联系人*"。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-201">In the **ContactController** class, select the word **string** in method definition of the **Get** method, and type the word *Contact*.</span></span> <span data-ttu-id="1d5c0-202">键入单词后，就会在 word **联系人** 的开头显示一个指示器。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-202">Once the word is typed in, an indicator will appear at the beginning of the word **Contact**.</span></span> <span data-ttu-id="1d5c0-203">按下 **Ctrl** 键并按句点 (。 ) 键，或使用鼠标单击图标以打开代码编辑器中的 "协助" 对话框，以自动填充 "模型" 命名空间的 **using** 指令。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-203">Either hold down the **Ctrl** key and press the period (.) key or click the icon using your mouse to open up the assistance dialog in the code editor, to automatically fill in the **using** directive for the Models namespace.</span></span>

    ![使用 Intellisense 帮助命名空间声明](build-restful-apis-with-aspnet-web-api/_static/image12.png)

    <span data-ttu-id="1d5c0-205">*使用 Intellisense 帮助命名空间声明*</span><span class="sxs-lookup"><span data-stu-id="1d5c0-205">*Using Intellisense assistance for namespace declarations*</span></span>
5. <span data-ttu-id="1d5c0-206">修改 **Get** 方法的代码，使其返回联系人模型实例的数组。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-206">Modify the code for the **Get** method so that it returns an array of Contact model instances.</span></span>

    <span data-ttu-id="1d5c0-207"> (代码片段- *WEB API Ex01-返回联系人列表*) </span><span class="sxs-lookup"><span data-stu-id="1d5c0-207">(Code Snippet - *Web API Lab - Ex01 - Returning a list of contacts*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample3.cs)]
6. <span data-ttu-id="1d5c0-208">按 **F5** 在浏览器中调试 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-208">Press **F5** to debug the web application in the browser.</span></span> <span data-ttu-id="1d5c0-209">若要查看对 API 的响应输出所做的更改，请执行以下步骤。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-209">To view the changes made to the response output of the API, perform the following steps.</span></span>

   1. <span data-ttu-id="1d5c0-210">打开浏览器后，如果开发人员工具尚未打开，请按 **F12** 。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-210">Once the browser opens, press **F12** if the developer tools are not open yet.</span></span>
   2. <span data-ttu-id="1d5c0-211">单击 " **网络** " 选项卡。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-211">Click the **Network** tab.</span></span>
   3. <span data-ttu-id="1d5c0-212">按 " **开始捕获** " 按钮。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-212">Press the **Start Capturing** button.</span></span>
   4. <span data-ttu-id="1d5c0-213">将 URL 后缀 **/api/contact** 添加到地址栏中的 url，然后按 **enter** 键。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-213">Add the URL suffix **/api/contact** to the URL in the address bar and press the **Enter** key.</span></span>
   5. <span data-ttu-id="1d5c0-214">按 " **中转到详细视图** " 按钮。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-214">Press the **Go to detailed view** button.</span></span>
   6. <span data-ttu-id="1d5c0-215">选择 " **响应正文** " 选项卡。应该会看到一个 JSON 字符串，表示联系人实例的序列化形式。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-215">Select the **Response body** tab. You should see a JSON string representing the serialized form of an array of Contact instances.</span></span>

      <span data-ttu-id="1d5c0-216">![复杂的 Web API 方法调用的 JSON 序列化输出](build-restful-apis-with-aspnet-web-api/_static/image13.png "复杂的 Web API 方法调用的 JSON 序列化输出")</span><span class="sxs-lookup"><span data-stu-id="1d5c0-216">![JSON serialized output of a complex Web API method call](build-restful-apis-with-aspnet-web-api/_static/image13.png "JSON serialized output of a complex Web API method call")</span></span>

      <span data-ttu-id="1d5c0-217">*复杂的 Web API 方法调用的 JSON 序列化输出*</span><span class="sxs-lookup"><span data-stu-id="1d5c0-217">*JSON serialized output of a complex Web API method call*</span></span>

<a id="Ex1Task4"></a>

<a id="Task_4_-_Extracting_Functionality_into_a_Service_Layer"></a>
#### <a name="task-4---extracting-functionality-into-a-service-layer"></a><span data-ttu-id="1d5c0-218">任务 4-将功能提取到服务层</span><span class="sxs-lookup"><span data-stu-id="1d5c0-218">Task 4 - Extracting Functionality into a Service Layer</span></span>

<span data-ttu-id="1d5c0-219">此任务将演示如何将功能提取到服务层，使开发人员可以轻松地将其服务功能与控制器层分开，从而实现实际执行工作的服务的可重用性。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-219">This task will demonstrate how to extract functionality into a Service layer to make it easy for developers to separate their service functionality from the controller layer, thereby allowing reusability of the services that actually do the work.</span></span>

1. <span data-ttu-id="1d5c0-220">在解决方案根文件夹中创建一个新文件夹并将其命名为 "it **服务**"。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-220">Create a new folder in the solution root and name it **Services**.</span></span> <span data-ttu-id="1d5c0-221">为此，请右键单击 " **ContactManager** 项目"，选择 "**添加**  |  " "**新建文件夹**"，将其命名为 "*服务*"。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-221">To do this, right-click **ContactManager** project, select **Add** | **New Folder**, name it *Services*.</span></span>

    <span data-ttu-id="1d5c0-222">![正在创建服务文件夹](build-restful-apis-with-aspnet-web-api/_static/image14.png "正在创建服务文件夹")</span><span class="sxs-lookup"><span data-stu-id="1d5c0-222">![Creating Services folder](build-restful-apis-with-aspnet-web-api/_static/image14.png "Creating Services folder")</span></span>

    <span data-ttu-id="1d5c0-223">*正在创建服务文件夹*</span><span class="sxs-lookup"><span data-stu-id="1d5c0-223">*Creating Services folder*</span></span>
2. <span data-ttu-id="1d5c0-224">右键单击 " **服务** " 文件夹，然后选择 " **添加 |类 ...** 从上下文菜单中。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-224">Right-click the **Services** folder and select **Add | Class...** from the context menu.</span></span>

    <span data-ttu-id="1d5c0-225">![将新类添加到服务文件夹](build-restful-apis-with-aspnet-web-api/_static/image15.png "将新类添加到服务文件夹")</span><span class="sxs-lookup"><span data-stu-id="1d5c0-225">![Adding a new class to the Services folder](build-restful-apis-with-aspnet-web-api/_static/image15.png "Adding a new class to the Services folder")</span></span>

    <span data-ttu-id="1d5c0-226">*将新类添加到服务文件夹*</span><span class="sxs-lookup"><span data-stu-id="1d5c0-226">*Adding a new class to the Services folder*</span></span>
3. <span data-ttu-id="1d5c0-227">当 " **添加新项** " 对话框出现时，将新类命名为 **contacts.json** ，然后单击 " **添加**"。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-227">When the **Add New Item** dialog appears, name the new class **ContactRepository** and click **Add**.</span></span>

    <span data-ttu-id="1d5c0-228">![创建类文件以包含联系人存储库服务层的代码](build-restful-apis-with-aspnet-web-api/_static/image16.png "创建类文件以包含联系人存储库服务层的代码")</span><span class="sxs-lookup"><span data-stu-id="1d5c0-228">![Creating a class file to contain the code for the Contact Repository service layer](build-restful-apis-with-aspnet-web-api/_static/image16.png "Creating a class file to contain the code for the Contact Repository service layer")</span></span>

    <span data-ttu-id="1d5c0-229">*创建类文件以包含联系人存储库服务层的代码*</span><span class="sxs-lookup"><span data-stu-id="1d5c0-229">*Creating a class file to contain the code for the Contact Repository service layer*</span></span>
4. <span data-ttu-id="1d5c0-230">向 **ContactRepository.cs** 文件添加 using 指令以包括模型命名空间。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-230">Add a using directive to the **ContactRepository.cs** file to include the models namespace.</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample4.cs)]
5. <span data-ttu-id="1d5c0-231">将以下突出显示的代码添加到 **ContactRepository.cs** 文件，以实现 GetAllContacts 方法。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-231">Add the following highlighted code to the **ContactRepository.cs** file to implement GetAllContacts method.</span></span>

    <span data-ttu-id="1d5c0-232"> (代码片段- *WEB API Ex01-联系库*) </span><span class="sxs-lookup"><span data-stu-id="1d5c0-232">(Code Snippet - *Web API Lab - Ex01 - Contact Repository*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample5.cs)]
6. <span data-ttu-id="1d5c0-233">打开 **ContactController.cs** 文件（如果尚未打开）。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-233">Open the **ContactController.cs** file if it is not already open.</span></span>
7. <span data-ttu-id="1d5c0-234">将以下 using 语句添加到文件的命名空间声明部分。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-234">Add the following using statement to the namespace declaration section of the file.</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample6.cs)]
8. <span data-ttu-id="1d5c0-235">将以下突出显示的代码添加到 **ContactController.cs** 类，以添加一个私有字段以表示存储库的实例，以便其他类成员可以使用服务实现。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-235">Add the following highlighted code to the **ContactController.cs** class to add a private field to represent the instance of the repository, so that the rest of the class members can make use of the service implementation.</span></span>

    <span data-ttu-id="1d5c0-236"> (代码片段- *WEB API Ex01-联系控制器*) </span><span class="sxs-lookup"><span data-stu-id="1d5c0-236">(Code Snippet - *Web API Lab - Ex01 - Contact Controller*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample7.cs)]
9. <span data-ttu-id="1d5c0-237">更改 **Get** 方法，使其能够使用联系人存储库服务。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-237">Change the **Get** method so that it makes use of the contact repository service.</span></span>

    <span data-ttu-id="1d5c0-238"> (代码片段- *WEB API Ex01-通过存储库返回联系人列表*) </span><span class="sxs-lookup"><span data-stu-id="1d5c0-238">(Code Snippet - *Web API Lab - Ex01 - Returning a list of contacts via the repository*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample8.cs)]
10. <span data-ttu-id="1d5c0-239">在 **ContactController** 的 **Get** 方法定义中放置一个断点。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-239">Put a breakpoint on the **ContactController**'s **Get** method definition.</span></span>

   <span data-ttu-id="1d5c0-240">![向联系人控制器添加断点](build-restful-apis-with-aspnet-web-api/_static/image17.png "向联系人控制器添加断点")</span><span class="sxs-lookup"><span data-stu-id="1d5c0-240">![Adding breakpoints to the contact controller](build-restful-apis-with-aspnet-web-api/_static/image17.png "Adding breakpoints to the contact controller")</span></span>

   <span data-ttu-id="1d5c0-241">*向联系人控制器添加断点*</span><span class="sxs-lookup"><span data-stu-id="1d5c0-241">*Adding breakpoints to the contact controller*</span></span>
11. <span data-ttu-id="1d5c0-242">按 **F5** 运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-242">Press **F5** to run the application.</span></span>
12. <span data-ttu-id="1d5c0-243">当浏览器打开时，按 **F12** 打开开发人员工具。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-243">When the browser opens, press **F12** to open the developer tools.</span></span>
13. <span data-ttu-id="1d5c0-244">单击 " **网络** " 选项卡。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-244">Click the **Network** tab.</span></span>
14. <span data-ttu-id="1d5c0-245">单击 " **开始捕获** " 按钮。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-245">Click the **Start Capturing** button.</span></span>
15. <span data-ttu-id="1d5c0-246">在地址栏中附加带有后缀 **/api/contact** 的 URL，然后按 **enter** 加载 api 控制器。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-246">Append the URL in the address bar with the suffix **/api/contact** and press **Enter** to load the API controller.</span></span>
16. <span data-ttu-id="1d5c0-247">**Get** 方法开始执行时，Visual Studio 2012 应中断。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-247">Visual Studio 2012 should break once **Get** method begins execution.</span></span>

   <span data-ttu-id="1d5c0-248">![在 Get 方法内中断](build-restful-apis-with-aspnet-web-api/_static/image18.png "在 Get 方法内中断")</span><span class="sxs-lookup"><span data-stu-id="1d5c0-248">![Breaking within the Get method](build-restful-apis-with-aspnet-web-api/_static/image18.png "Breaking within the Get method")</span></span>

   <span data-ttu-id="1d5c0-249">*在 Get 方法内中断*</span><span class="sxs-lookup"><span data-stu-id="1d5c0-249">*Breaking within the Get method*</span></span>
17. <span data-ttu-id="1d5c0-250">按 F5 以继续操作。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-250">Press **F5** to continue.</span></span>
18. <span data-ttu-id="1d5c0-251">返回到 Internet Explorer （如果它尚未处于焦点上）。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-251">Go back to Internet Explorer if it is not already in focus.</span></span> <span data-ttu-id="1d5c0-252">请注意 "网络捕获" 窗口。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-252">Note the network capture window.</span></span>

    <span data-ttu-id="1d5c0-253">![Internet Explorer 中显示 Web API 调用结果的网络视图](build-restful-apis-with-aspnet-web-api/_static/image19.png "Internet Explorer 中显示 Web API 调用结果的网络视图")</span><span class="sxs-lookup"><span data-stu-id="1d5c0-253">![Network view in Internet Explorer showing results of the Web API call](build-restful-apis-with-aspnet-web-api/_static/image19.png "Network view in Internet Explorer showing results of the Web API call")</span></span>

    <span data-ttu-id="1d5c0-254">*Internet Explorer 中显示 Web API 调用结果的网络视图*</span><span class="sxs-lookup"><span data-stu-id="1d5c0-254">*Network view in Internet Explorer showing results of the Web API call*</span></span>
19. <span data-ttu-id="1d5c0-255">单击 " **中转到详细视图** " 按钮。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-255">Click the **Go to detailed view** button.</span></span>
20. <span data-ttu-id="1d5c0-256">单击 " **响应正文** " 选项卡。请注意 API 调用的 JSON 输出，以及它如何表示服务层检索到的两个联系人。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-256">Click the **Response body** tab. Note the JSON output of the API call, and how it represents the two contacts retrieved by the service layer.</span></span>

    <span data-ttu-id="1d5c0-257">![在 "开发人员工具" 窗口中查看 Web API 的 JSON 输出](build-restful-apis-with-aspnet-web-api/_static/image20.png "在 "开发人员工具" 窗口中查看 Web API 的 JSON 输出")</span><span class="sxs-lookup"><span data-stu-id="1d5c0-257">![Viewing the JSON output from the Web API in the developer tools window](build-restful-apis-with-aspnet-web-api/_static/image20.png "Viewing the JSON output from the Web API in the developer tools window")</span></span>

    <span data-ttu-id="1d5c0-258">*在 "开发人员工具" 窗口中查看 Web API 的 JSON 输出*</span><span class="sxs-lookup"><span data-stu-id="1d5c0-258">*Viewing the JSON output from the Web API in the developer tools window*</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Create_a_ReadWrite_Web_API"></a>
### <a name="exercise-2-create-a-readwrite-web-api"></a><span data-ttu-id="1d5c0-259">练习2：创建读/写 Web API</span><span class="sxs-lookup"><span data-stu-id="1d5c0-259">Exercise 2: Create a Read/Write Web API</span></span>

<span data-ttu-id="1d5c0-260">在此练习中，您将为联系人管理器实现 POST 和 PUT 方法，使其能够使用数据编辑功能。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-260">In this exercise, you will implement POST and PUT methods for the contact manager to enable it with data-editing features.</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_-_Opening_the_Web_API_Project"></a>
#### <a name="task-1---opening-the-web-api-project"></a><span data-ttu-id="1d5c0-261">任务 1-打开 Web API 项目</span><span class="sxs-lookup"><span data-stu-id="1d5c0-261">Task 1 - Opening the Web API Project</span></span>

<span data-ttu-id="1d5c0-262">在此任务中，你将准备好改进在练习1中创建的 Web API 项目，以便它可以接受用户输入。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-262">In this task, you will prepare to enhance the Web API project created in Exercise 1 so that it can accept user input.</span></span>

1. <span data-ttu-id="1d5c0-263">运行 **Visual Studio 2012 Express For Web**，若要执行此操作，请单击 " **开始** "，然后键入 **VS Express for Web** 然后按 **enter**。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-263">Run **Visual Studio 2012 Express for Web**, to do this go to **Start** and type **VS Express for Web** then press **Enter**.</span></span>
2. <span data-ttu-id="1d5c0-264">打开位于 **Source/Ex02-ReadWriteWebAPI/begin/** Folder 的 **begin** 解决方案。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-264">Open the **Begin** solution located at **Source/Ex02-ReadWriteWebAPI/Begin/** folder.</span></span> <span data-ttu-id="1d5c0-265">否则，你可以继续使用通过完成前一练习所获得的 **最终** 解决方案。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-265">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="1d5c0-266">如果你打开了提供的 **开始** 解决方案，则需要下载一些缺少的 NuGet 包，然后再继续。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-266">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="1d5c0-267">为此，请单击 " **项目** " 菜单并选择 " **管理 NuGet 包**"。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-267">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="1d5c0-268">在 " **管理 NuGet 包** " 对话框中，单击 " **还原** " 以下载缺少的包。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-268">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="1d5c0-269">最后，通过单击 "**生成**" "生成解决方案" 来生成解决方案  |  。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-269">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="1d5c0-270">使用 NuGet 的优点之一是，无需将所有库都送到项目中，从而减少了项目的大小。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-270">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="1d5c0-271">使用 NuGet 功能，通过指定 Packages.config 文件中的包版本，你将能够在首次运行项目时下载所有必需的库。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-271">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="1d5c0-272">这就是在从此实验室打开现有解决方案之后需要运行这些步骤的原因。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-272">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="1d5c0-273">打开 **Services/contacts.json** 文件。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-273">Open the **Services/ContactRepository.cs** file.</span></span>

<a id="Ex2Task2"></a>

<a id="Task_2_-_Adding_Data-Persistence_Features_to_the_Contact_Repository_Implementation"></a>
#### <a name="task-2---adding-data-persistence-features-to-the-contact-repository-implementation"></a><span data-ttu-id="1d5c0-274">任务 2-将 Data-Persistence 功能添加到联系人存储库实现</span><span class="sxs-lookup"><span data-stu-id="1d5c0-274">Task 2 - Adding Data-Persistence Features to the Contact Repository Implementation</span></span>

<span data-ttu-id="1d5c0-275">在此任务中，您将补充在练习1中创建的 Web API 项目的 Contacts.json 类，使其可以持久保存并接受用户输入和新的联系人实例。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-275">In this task, you will augment the ContactRepository class of the Web API project created in Exercise 1 so that it can persist and accept user input and new Contact instances.</span></span>

1. <span data-ttu-id="1d5c0-276">将以下常量添加到 **contacts.json** 类中，以表示在本练习后面的 web 服务器缓存项密钥名称。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-276">Add the following constant to the **ContactRepository** class to represent the name of the web server cache item key name later in this exercise.</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample9.cs)]
2. <span data-ttu-id="1d5c0-277">将构造函数添加到包含以下代码的 **contacts.json** 。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-277">Add a constructor to the **ContactRepository** containing the following code.</span></span>

    <span data-ttu-id="1d5c0-278"> (代码片段- *Ex02 联系存储库构造函数*) </span><span class="sxs-lookup"><span data-stu-id="1d5c0-278">(Code Snippet - *Web API Lab - Ex02 - Contact Repository Constructor*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample10.cs)]
3. <span data-ttu-id="1d5c0-279">修改 **GetAllContacts** 方法的代码，如下所示。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-279">Modify the code for the **GetAllContacts** method as demonstrated below.</span></span>

    <span data-ttu-id="1d5c0-280"> (代码片段- *WEB API Ex02-获取所有联系人*) </span><span class="sxs-lookup"><span data-stu-id="1d5c0-280">(Code Snippet - *Web API Lab - Ex02 - Get All Contacts*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample11.cs)]

    > [!NOTE]
    > <span data-ttu-id="1d5c0-281">此示例用于演示目的，并将 web 服务器的缓存用作存储介质，使多个客户端的值可以同时用于多个客户端，而不是使用会话存储机制或请求存储生存期。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-281">This example is for demonstration purposes and will use the web server's cache as a storage medium, so that the values will be available to multiple clients simultaneously, rather than use a Session storage mechanism or a Request storage lifetime.</span></span> <span data-ttu-id="1d5c0-282">可以使用实体框架、XML 存储或任何其他种类的 web 服务器缓存。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-282">One could use Entity Framework, XML storage, or any other variety in place of the web server cache.</span></span>
4. <span data-ttu-id="1d5c0-283">为 **contacts.json** 类实现一个名为 **SaveContact** 的新方法，以便保存联系人。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-283">Implement a new method named **SaveContact** to the **ContactRepository** class to do the work of saving a contact.</span></span> <span data-ttu-id="1d5c0-284">**SaveContact** 方法应采用单个 **Contact** 参数，并返回指示成功或失败的布尔值。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-284">The **SaveContact** method should take a single **Contact** parameter and return a Boolean value indicating success or failure.</span></span>

    <span data-ttu-id="1d5c0-285"> (代码片段- *WEB API Ex02-实现 SaveContact 方法*) </span><span class="sxs-lookup"><span data-stu-id="1d5c0-285">(Code Snippet - *Web API Lab - Ex02 - Implementing the SaveContact Method*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample12.cs)]

<a id="Exercise3"></a>

<a id="Exercise_3_Consume_the_Web_API_from_an_HTML_Client"></a>
### <a name="exercise-3-consume-the-web-api-from-an-html-client"></a><span data-ttu-id="1d5c0-286">练习3：使用 HTML 客户端中的 Web API</span><span class="sxs-lookup"><span data-stu-id="1d5c0-286">Exercise 3: Consume the Web API from an HTML Client</span></span>

<span data-ttu-id="1d5c0-287">在此练习中，您将创建一个 HTML 客户端来调用 Web API。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-287">In this exercise, you will create an HTML client to call the Web API.</span></span> <span data-ttu-id="1d5c0-288">此客户端将使用 JavaScript 简化与 Web API 的数据交换，并使用 HTML 标记在 web 浏览器中显示结果。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-288">This client will facilitate data exchange with the Web API using JavaScript and will display the results in a web browser using HTML markup.</span></span>

<a id="Ex3Task1"></a>

<a id="Task_1_-_Modifying_the_Index_View_to_Provide_a_GUI_for_Displaying_Contacts"></a>
#### <a name="task-1---modifying-the-index-view-to-provide-a-gui-for-displaying-contacts"></a><span data-ttu-id="1d5c0-289">任务 1-修改索引视图以提供用于显示联系人的 GUI</span><span class="sxs-lookup"><span data-stu-id="1d5c0-289">Task 1 - Modifying the Index View to Provide a GUI for Displaying Contacts</span></span>

<span data-ttu-id="1d5c0-290">在此任务中，您将修改 web 应用程序的默认索引视图，以支持在 HTML 浏览器中显示现有联系人列表的要求。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-290">In this task, you will modify the default Index view of the web application to support the requirement of displaying the list of existing contacts in an HTML browser.</span></span>

1. <span data-ttu-id="1d5c0-291">如果尚未打开，请打开 **Visual Studio 2012 Express For Web** 。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-291">Open **Visual Studio 2012 Express for Web** if it is not already open.</span></span>
2. <span data-ttu-id="1d5c0-292">打开位于 **Source/Ex03-ConsumingWebAPI/begin/** Folder 的 **begin** 解决方案。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-292">Open the **Begin** solution located at **Source/Ex03-ConsumingWebAPI/Begin/** folder.</span></span> <span data-ttu-id="1d5c0-293">否则，你可以继续使用通过完成前一练习所获得的 **最终** 解决方案。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-293">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="1d5c0-294">如果你打开了提供的 **开始** 解决方案，则需要下载一些缺少的 NuGet 包，然后再继续。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-294">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="1d5c0-295">为此，请单击 " **项目** " 菜单并选择 " **管理 NuGet 包**"。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-295">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="1d5c0-296">在 " **管理 NuGet 包** " 对话框中，单击 " **还原** " 以下载缺少的包。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-296">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="1d5c0-297">最后，通过单击 "**生成**" "生成解决方案" 来生成解决方案  |  。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-297">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="1d5c0-298">使用 NuGet 的优点之一是，无需将所有库都送到项目中，从而减少了项目的大小。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-298">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="1d5c0-299">使用 NuGet 功能，通过指定 Packages.config 文件中的包版本，你将能够在首次运行项目时下载所有必需的库。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-299">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="1d5c0-300">这就是在从此实验室打开现有解决方案之后需要运行这些步骤的原因。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-300">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="1d5c0-301">打开位于 **Views/Home** 文件夹中的 **索引 cshtml** 文件。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-301">Open the **Index.cshtml** file located at **Views/Home** folder.</span></span>
4. <span data-ttu-id="1d5c0-302">用 id **体** 替换 div 元素中的 HTML 代码，使其类似于以下代码。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-302">Replace the HTML code within the div element with id **body** so that it looks like the following code.</span></span>

    [!code-html[Main](build-restful-apis-with-aspnet-web-api/samples/sample13.html)]
5. <span data-ttu-id="1d5c0-303">在文件底部添加以下 Javascript 代码，以对 Web API 执行 HTTP 请求。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-303">Add the following Javascript code at the bottom of the file to perform the HTTP request to the Web API.</span></span>

    [!code-cshtml[Main](build-restful-apis-with-aspnet-web-api/samples/sample14.cshtml)]
6. <span data-ttu-id="1d5c0-304">打开 **ContactController.cs** 文件（如果尚未打开）。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-304">Open the **ContactController.cs** file if it is not already open.</span></span>
7. <span data-ttu-id="1d5c0-305">在 **ContactController** 类的 **Get** 方法上放置一个断点。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-305">Place a breakpoint on the **Get** method of the **ContactController** class.</span></span>

    <span data-ttu-id="1d5c0-306">![在 API 控制器的 Get 方法上放置断点](build-restful-apis-with-aspnet-web-api/_static/image21.png "在 API 控制器的 Get 方法上放置断点")</span><span class="sxs-lookup"><span data-stu-id="1d5c0-306">![Placing a breakpoint on the Get method of the API controller](build-restful-apis-with-aspnet-web-api/_static/image21.png "Placing a breakpoint on the Get method of the API controller")</span></span>

    <span data-ttu-id="1d5c0-307">*在 API 控制器的 Get 方法上放置断点*</span><span class="sxs-lookup"><span data-stu-id="1d5c0-307">*Placing a breakpoint on the Get method of the API controller*</span></span>
8. <span data-ttu-id="1d5c0-308">按 **F5** 运行项目。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-308">Press **F5** to run the project.</span></span> <span data-ttu-id="1d5c0-309">浏览器将加载 HTML 文档。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-309">The browser will load the HTML document.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1d5c0-310">确保浏览到应用程序的根 URL。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-310">Ensure that you are browsing to the root URL of your application.</span></span>
9. <span data-ttu-id="1d5c0-311">加载页面并执行 JavaScript 后，断点将被命中，代码执行将在控制器中暂停。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-311">Once the page loads and the JavaScript executes, the breakpoint will be hit and the code execution will pause in the controller.</span></span>

    <span data-ttu-id="1d5c0-312">![使用 VS Express for Web 调试到 Web API 调用](build-restful-apis-with-aspnet-web-api/_static/image22.png "使用 VS Express for Web 调试到 Web API 调用")</span><span class="sxs-lookup"><span data-stu-id="1d5c0-312">![Debugging into the Web API calls using VS Express for Web](build-restful-apis-with-aspnet-web-api/_static/image22.png "Debugging into the Web API calls using VS Express for Web")</span></span>

    <span data-ttu-id="1d5c0-313">*使用 Visual Studio 2012 Express for Web 调试到 Web API 调用*</span><span class="sxs-lookup"><span data-stu-id="1d5c0-313">*Debugging into the Web API call using Visual Studio 2012 Express for Web*</span></span>
10. <span data-ttu-id="1d5c0-314">删除断点，然后按 **F5** 或 "调试" 工具栏的 " **继续** " 按钮，继续在浏览器中加载视图。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-314">Remove the breakpoint and press **F5** or the debugging toolbar's **Continue** button to continue loading the view in the browser.</span></span> <span data-ttu-id="1d5c0-315">Web API 调用完成后，会在浏览器中看到从 Web API 调用返回的、显示为列表项的联系人。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-315">Once the Web API call completes you should see the contacts returned from the Web API call displayed as list items in the browser.</span></span>

    <span data-ttu-id="1d5c0-316">![在浏览器中显示为列表项的 API 调用结果](build-restful-apis-with-aspnet-web-api/_static/image23.png "在浏览器中显示为列表项的 API 调用结果")</span><span class="sxs-lookup"><span data-stu-id="1d5c0-316">![Results of the API call displayed in the browser as list items](build-restful-apis-with-aspnet-web-api/_static/image23.png "Results of the API call displayed in the browser as list items")</span></span>

    <span data-ttu-id="1d5c0-317">*在浏览器中显示为列表项的 API 调用结果*</span><span class="sxs-lookup"><span data-stu-id="1d5c0-317">*Results of the API call displayed in the browser as list items*</span></span>
11. <span data-ttu-id="1d5c0-318">停止调试。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-318">Stop debugging.</span></span>

<a id="Ex3Task2"></a>

<a id="Task_2_-_Modifying_the_Index_View_to_Provide_a_GUI_for_Creating_Contacts"></a>
#### <a name="task-2---modifying-the-index-view-to-provide-a-gui-for-creating-contacts"></a><span data-ttu-id="1d5c0-319">任务 2-修改索引视图以提供用于创建联系人的 GUI</span><span class="sxs-lookup"><span data-stu-id="1d5c0-319">Task 2 - Modifying the Index View to Provide a GUI for Creating Contacts</span></span>

<span data-ttu-id="1d5c0-320">在此任务中，您将继续修改 MVC 应用程序的索引视图。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-320">In this task, you will continue to modify the Index view of the MVC application.</span></span> <span data-ttu-id="1d5c0-321">将在 HTML 页中添加一个窗体，该页面将捕获用户输入并将其发送到 Web API 来创建新的联系人，并将创建新的 Web API 控制器方法以从 GUI 收集日期。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-321">A form will be added to the HTML page that will capture user input and send it to the Web API to create a new Contact, and a new Web API controller method will be created to collect date from the GUI.</span></span>

1. <span data-ttu-id="1d5c0-322">打开 **ContactController.cs** 文件。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-322">Open the **ContactController.cs** file.</span></span>
2. <span data-ttu-id="1d5c0-323">将新方法添加到名为 **Post** 的控制器类，如下面的代码所示。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-323">Add a new method to the controller class named **Post** as shown in the following code.</span></span>

    <span data-ttu-id="1d5c0-324"> (代码片段- *WEB API Ex03-Post 方法*) </span><span class="sxs-lookup"><span data-stu-id="1d5c0-324">(Code Snippet - *Web API Lab - Ex03 - Post Method*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample15.cs)]
3. <span data-ttu-id="1d5c0-325">在 Visual Studio 中打开 **索引 cshtml** 文件（如果尚未打开）。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-325">Open the **Index.cshtml** file in Visual Studio if it is not already open.</span></span>
4. <span data-ttu-id="1d5c0-326">将以下 HTML 代码添加到文件中，就在上一个任务中添加的未排序列表之后。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-326">Add the HTML code below to the file just after the unordered list you added in the previous task.</span></span>

    [!code-html[Main](build-restful-apis-with-aspnet-web-api/samples/sample16.html)]
5. <span data-ttu-id="1d5c0-327">在文档底部的脚本元素中，添加以下突出显示的代码以处理按钮单击事件，这会使用 HTTP POST 调用将数据发布到 Web API。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-327">Within the script element at the bottom of the document, add the following highlighted code to handle button-click events, which will post the data to the Web API using an HTTP POST call.</span></span>

    [!code-html[Main](build-restful-apis-with-aspnet-web-api/samples/sample17.html)]
6. <span data-ttu-id="1d5c0-328">在 **ContactController.cs** 中，将一个断点置于 **Post** 方法上。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-328">In **ContactController.cs**, place a breakpoint on the **Post** method.</span></span>
7. <span data-ttu-id="1d5c0-329">按 **F5** 在浏览器中运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-329">Press **F5** to run the application in the browser.</span></span>
8. <span data-ttu-id="1d5c0-330">在浏览器中加载页面后，键入新的联系人名称和 Id，并单击 " **保存** " 按钮。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-330">Once the page is loaded in the browser, type in a new contact name and Id and click the **Save** button.</span></span>

    <span data-ttu-id="1d5c0-331">![在浏览器中加载的客户端 HTML 文档](build-restful-apis-with-aspnet-web-api/_static/image24.png "在浏览器中加载的客户端 HTML 文档")</span><span class="sxs-lookup"><span data-stu-id="1d5c0-331">![The client HTML document loaded in the browser](build-restful-apis-with-aspnet-web-api/_static/image24.png "The client HTML document loaded in the browser")</span></span>

    <span data-ttu-id="1d5c0-332">*在浏览器中加载的客户端 HTML 文档*</span><span class="sxs-lookup"><span data-stu-id="1d5c0-332">*The client HTML document loaded in the browser*</span></span>
9. <span data-ttu-id="1d5c0-333">调试器窗口在 **Post** 方法中中断时，查看 **contact** 参数的属性。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-333">When the debugger window breaks in the **Post** method, take a look at the properties of the **contact** parameter.</span></span> <span data-ttu-id="1d5c0-334">值应与您在窗体中输入的数据匹配。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-334">The values should match the data you entered in the form.</span></span>

    <span data-ttu-id="1d5c0-335">![要从客户端发送到 Web API 的联系人对象](build-restful-apis-with-aspnet-web-api/_static/image25.png "要从客户端发送到 Web API 的联系人对象")</span><span class="sxs-lookup"><span data-stu-id="1d5c0-335">![The Contact object being sent to the Web API from the client](build-restful-apis-with-aspnet-web-api/_static/image25.png "The Contact object being sent to the Web API from the client")</span></span>

    <span data-ttu-id="1d5c0-336">*要从客户端发送到 Web API 的联系人对象*</span><span class="sxs-lookup"><span data-stu-id="1d5c0-336">*The Contact object being sent to the Web API from the client*</span></span>
10. <span data-ttu-id="1d5c0-337">在调试器中单步执行方法，直到创建了 **响应** 变量为止。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-337">Step through the method in the debugger until the **response** variable has been created.</span></span> <span data-ttu-id="1d5c0-338">在调试器的 " **局部变量** " 窗口中进行检查后，您将看到已设置所有属性。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-338">Upon inspection in the **Locals** window in the debugger, you'll see that all the properties have been set.</span></span>

   <span data-ttu-id="1d5c0-339">![在调试器中创建后的响应](build-restful-apis-with-aspnet-web-api/_static/image26.png "在调试器中创建后的响应")</span><span class="sxs-lookup"><span data-stu-id="1d5c0-339">![The response following creation in the debugger](build-restful-apis-with-aspnet-web-api/_static/image26.png "The response following creation in the debugger")</span></span>

   <span data-ttu-id="1d5c0-340">*在调试器中创建后的响应*</span><span class="sxs-lookup"><span data-stu-id="1d5c0-340">*The response following creation in the debugger*</span></span>
11. <span data-ttu-id="1d5c0-341">如果按 **F5** 或单击调试器中的 " **继续** "，请求将会完成。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-341">If you press **F5** or click **Continue** in the debugger the request will complete.</span></span> <span data-ttu-id="1d5c0-342">切换回浏览器后，会将新联系人添加到 **contacts.json** 实现存储的联系人列表中。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-342">Once you switch back to the browser, the new contact has been added to the list of contacts stored by the **ContactRepository** implementation.</span></span>

   <span data-ttu-id="1d5c0-343">![浏览器反映新联系人实例的创建成功](build-restful-apis-with-aspnet-web-api/_static/image27.png "浏览器反映新联系人实例的创建成功")</span><span class="sxs-lookup"><span data-stu-id="1d5c0-343">![The browser reflects successful creation of the new contact instance](build-restful-apis-with-aspnet-web-api/_static/image27.png "The browser reflects successful creation of the new contact instance")</span></span>

   <span data-ttu-id="1d5c0-344">*浏览器反映新联系人实例的创建成功*</span><span class="sxs-lookup"><span data-stu-id="1d5c0-344">*The browser reflects successful creation of the new contact instance*</span></span>

> [!NOTE]
> <span data-ttu-id="1d5c0-345">此外，你可以遵循 [附录 C：使用 Web 部署发布 ASP.NET MVC 4 应用程序](#AppendixC)，将此应用程序部署到 Azure。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-345">Additionally, you can deploy this application to Azure following [Appendix C: Publishing an ASP.NET MVC 4 Application using Web Deploy](#AppendixC).</span></span>

---

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="1d5c0-346">总结</span><span class="sxs-lookup"><span data-stu-id="1d5c0-346">Summary</span></span>

<span data-ttu-id="1d5c0-347">此实验室已向你介绍了新的 ASP.NET Web API 框架，以及如何使用框架实现 RESTful Web Api。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-347">This lab has introduced you to the new ASP.NET Web API framework and to the implementation of RESTful Web APIs using the framework.</span></span> <span data-ttu-id="1d5c0-348">从这里，你可以创建一个新的存储库，该存储库使用任意数量的机制和网络连接，而不是在此实验室中作为示例提供的简单数据。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-348">From here, you could create a new repository that facilitates data persistence using any number of mechanisms and wire that service up rather than the simple one provided as an example in this lab.</span></span> <span data-ttu-id="1d5c0-349">Web API 支持多种附加功能，例如，从以支持 HTTP 和 JSON 或 XML 的任何语言编写的非 HTML 客户端进行通信。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-349">Web API supports a number of additional features, such as enabling communication from non-HTML clients written in any language that supports HTTP and JSON or XML.</span></span> <span data-ttu-id="1d5c0-350">还可以在典型的 web 应用程序之外承载 Web API，还可以创建自己的序列化格式。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-350">The ability to host a Web API outside of a typical web application is also possible, as well as is the ability to create your own serialization formats.</span></span>

<span data-ttu-id="1d5c0-351">ASP.NET 网站有一个专用于 ASP.NET Web API 框架的区域 [[https://asp.net/web-api](https://asp.net/web-api)](https://asp.net/web-api) 。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-351">The ASP.NET Web site has an area dedicated to the ASP.NET Web API framework at [[https://asp.net/web-api](https://asp.net/web-api)](https://asp.net/web-api).</span></span> <span data-ttu-id="1d5c0-352">此站点将继续提供与 Web API 相关的最新信息、示例和新闻，因此，如果想要深入了解如何创建可用于几乎任何设备或开发框架的自定义 Web Api，请经常查看。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-352">This site will continue to provide late-breaking information, samples, and news related to Web API, so check it frequently if you'd like to delve deeper into the art of creating custom Web APIs available to virtually any device or development framework.</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Using_Code_Snippets"></a>
## <a name="appendix-a-using-code-snippets"></a><span data-ttu-id="1d5c0-353">附录 A：使用代码片段</span><span class="sxs-lookup"><span data-stu-id="1d5c0-353">Appendix A: Using Code Snippets</span></span>

<span data-ttu-id="1d5c0-354">使用代码片段，您可以随时获得所需的全部代码。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-354">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="1d5c0-355">实验室文档将告诉你何时可以使用它们，如下图所示。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-355">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="1d5c0-356">![使用 Visual Studio code 代码段将代码插入到项目中](build-restful-apis-with-aspnet-web-api/_static/image28.png "使用 Visual Studio code 代码段将代码插入到项目中")</span><span class="sxs-lookup"><span data-stu-id="1d5c0-356">![Using Visual Studio code snippets to insert code into your project](build-restful-apis-with-aspnet-web-api/_static/image28.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="1d5c0-357">*使用 Visual Studio code 代码段将代码插入到项目中*</span><span class="sxs-lookup"><span data-stu-id="1d5c0-357">*Using Visual Studio code snippets to insert code into your project*</span></span>

<a id="CodeSnippetUsingKeyBoard"></a>

<a id="To_add_a_code_snippet_using_the_keyboard_C_only"></a>
### <a name="to-add-a-code-snippet-using-the-keyboard-c-only"></a><span data-ttu-id="1d5c0-358">使用键盘 (仅限 c # 添加代码片段) </span><span class="sxs-lookup"><span data-stu-id="1d5c0-358">To add a code snippet using the keyboard (C# only)</span></span>

1. <span data-ttu-id="1d5c0-359">将光标放在要插入代码的位置。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-359">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="1d5c0-360">开始键入代码片段名称 (没有空格或连字符) 。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-360">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="1d5c0-361">请注意，IntelliSense 显示匹配的代码段名称。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-361">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="1d5c0-362">选择正确的代码段 (或保留键入内容，直到选择了整个代码段的名称) 。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-362">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="1d5c0-363">按 Tab 键两次，将代码段插入到光标位置。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-363">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

    <span data-ttu-id="1d5c0-364">![开始键入代码片段名称](build-restful-apis-with-aspnet-web-api/_static/image29.png "开始键入代码片段名称")</span><span class="sxs-lookup"><span data-stu-id="1d5c0-364">![Start typing the snippet name](build-restful-apis-with-aspnet-web-api/_static/image29.png "Start typing the snippet name")</span></span>

    <span data-ttu-id="1d5c0-365">*开始键入代码片段名称*</span><span class="sxs-lookup"><span data-stu-id="1d5c0-365">*Start typing the snippet name*</span></span>

    <span data-ttu-id="1d5c0-366">![按 Tab 键以选择突出显示的代码段](build-restful-apis-with-aspnet-web-api/_static/image30.png "按 Tab 键以选择突出显示的代码段")</span><span class="sxs-lookup"><span data-stu-id="1d5c0-366">![Press Tab to select the highlighted snippet](build-restful-apis-with-aspnet-web-api/_static/image30.png "Press Tab to select the highlighted snippet")</span></span>

    <span data-ttu-id="1d5c0-367">*按 Tab 键以选择突出显示的代码段*</span><span class="sxs-lookup"><span data-stu-id="1d5c0-367">*Press Tab to select the highlighted snippet*</span></span>

    <span data-ttu-id="1d5c0-368">![再次按 Tab 键，代码片段将展开](build-restful-apis-with-aspnet-web-api/_static/image31.png "再次按 Tab 键，代码片段将展开")</span><span class="sxs-lookup"><span data-stu-id="1d5c0-368">![Press Tab again and the snippet will expand](build-restful-apis-with-aspnet-web-api/_static/image31.png "Press Tab again and the snippet will expand")</span></span>

    <span data-ttu-id="1d5c0-369">*再次按 Tab 键，代码片段将展开*</span><span class="sxs-lookup"><span data-stu-id="1d5c0-369">*Press Tab again and the snippet will expand*</span></span>

<a id="CodeSnippetUsingMouse"></a>

<a id="To_add_a_code_snippet_using_the_mouse_C_Visual_Basic_and_XML"></a>
### <a name="to-add-a-code-snippet-using-the-mouse-c-visual-basic-and-xml"></a><span data-ttu-id="1d5c0-370">若要使用鼠标 (c # 中添加代码段，请 Visual Basic 和 XML) </span><span class="sxs-lookup"><span data-stu-id="1d5c0-370">To add a code snippet using the mouse (C#, Visual Basic and XML)</span></span>

1. <span data-ttu-id="1d5c0-371">右键单击要插入代码片段的位置。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-371">Right-click where you want to insert the code snippet.</span></span>
2. <span data-ttu-id="1d5c0-372">选择 " **插入** 代码片段"，然后选择 **"我的代码片段"**。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-372">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
3. <span data-ttu-id="1d5c0-373">通过单击从列表中选择相关的代码片段。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-373">Pick the relevant snippet from the list, by clicking on it.</span></span>

    <span data-ttu-id="1d5c0-374">![右键单击要插入代码片段的位置，然后选择 "插入代码片段"](build-restful-apis-with-aspnet-web-api/_static/image32.png "右键单击要插入代码片段的位置，然后选择 "插入代码片段"")</span><span class="sxs-lookup"><span data-stu-id="1d5c0-374">![Right-click where you want to insert the code snippet and select Insert Snippet](build-restful-apis-with-aspnet-web-api/_static/image32.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

    <span data-ttu-id="1d5c0-375">*右键单击要插入代码片段的位置，然后选择 "插入代码片段"*</span><span class="sxs-lookup"><span data-stu-id="1d5c0-375">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

    <span data-ttu-id="1d5c0-376">![通过单击从列表中选择相关的代码片段](build-restful-apis-with-aspnet-web-api/_static/image33.png "通过单击从列表中选择相关的代码片段")</span><span class="sxs-lookup"><span data-stu-id="1d5c0-376">![Pick the relevant snippet from the list, by clicking on it](build-restful-apis-with-aspnet-web-api/_static/image33.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

    <span data-ttu-id="1d5c0-377">*通过单击从列表中选择相关的代码片段*</span><span class="sxs-lookup"><span data-stu-id="1d5c0-377">*Pick the relevant snippet from the list, by clicking on it*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-b-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="1d5c0-378">附录 B：安装 Web Visual Studio Express 2012</span><span class="sxs-lookup"><span data-stu-id="1d5c0-378">Appendix B: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="1d5c0-379">你可以使用 Microsoft Web 平台安装程序安装 **Web Microsoft Visual Studio Express 2012** 或其他 &quot; Express &quot; 版本。 **[](https://www.microsoft.com/web/downloads/platform.aspx)**</span><span class="sxs-lookup"><span data-stu-id="1d5c0-379">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="1d5c0-380">以下说明将指导你完成使用 *Microsoft Web 平台安装程序* 安装 *Visual studio Express 2012 for Web* 的步骤。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-380">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="1d5c0-381">请参阅 [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169) 。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-381">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="1d5c0-382">或者，如果你已经安装了 Web 平台安装程序，则可以打开它，并 &quot; <em>使用 Azure SDK 搜索产品 Visual Studio Express 2012 for Web</em> &quot; 。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-382">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="1d5c0-383">单击 " **立即安装**"。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-383">Click on **Install Now**.</span></span> <span data-ttu-id="1d5c0-384">如果你没有 **Web 平台安装程序** ，则会重定向到 "下载并安装"。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-384">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="1d5c0-385">**Web 平台安装程序** 打开后，单击 "**安装**" 以启动安装程序。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-385">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="1d5c0-386">![安装 Visual Studio Express](build-restful-apis-with-aspnet-web-api/_static/image34.png "安装 Visual Studio Express")</span><span class="sxs-lookup"><span data-stu-id="1d5c0-386">![Install Visual Studio Express](build-restful-apis-with-aspnet-web-api/_static/image34.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="1d5c0-387">*安装 Visual Studio Express*</span><span class="sxs-lookup"><span data-stu-id="1d5c0-387">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="1d5c0-388">阅读所有产品的许可证和条款，单击 " **我接受** " 以继续。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-388">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![接受许可条款](build-restful-apis-with-aspnet-web-api/_static/image35.png)

    <span data-ttu-id="1d5c0-390">*接受许可条款*</span><span class="sxs-lookup"><span data-stu-id="1d5c0-390">*Accepting the license terms*</span></span>
5. <span data-ttu-id="1d5c0-391">等待下载和安装过程完成。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-391">Wait until the downloading and installation process completes.</span></span>

    ![安装进度](build-restful-apis-with-aspnet-web-api/_static/image36.png)

    <span data-ttu-id="1d5c0-393">*安装进度*</span><span class="sxs-lookup"><span data-stu-id="1d5c0-393">*Installation progress*</span></span>
6. <span data-ttu-id="1d5c0-394">安装完成后，单击 " **完成**"。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-394">When the installation completes, click **Finish**.</span></span>

    ![安装完成](build-restful-apis-with-aspnet-web-api/_static/image37.png)

    <span data-ttu-id="1d5c0-396">*安装完成*</span><span class="sxs-lookup"><span data-stu-id="1d5c0-396">*Installation completed*</span></span>
7. <span data-ttu-id="1d5c0-397">单击 " **退出** " 以关闭 Web 平台安装程序。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-397">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="1d5c0-398">若要打开 Web Visual Studio Express，请在 "**开始**" 屏幕上，单击 "开始撰写 &quot; **VS Express** &quot; "，然后单击 " **VS Express for Web** " 磁贴。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-398">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![VS Express for Web 磁贴](build-restful-apis-with-aspnet-web-api/_static/image38.png)

    <span data-ttu-id="1d5c0-400">*VS Express for Web 磁贴*</span><span class="sxs-lookup"><span data-stu-id="1d5c0-400">*VS Express for Web tile*</span></span>

<a id="AppendixC"></a>

<a id="Appendix_C_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-c-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="1d5c0-401">附录 C：使用 Web 部署发布 ASP.NET MVC 4 应用程序</span><span class="sxs-lookup"><span data-stu-id="1d5c0-401">Appendix C: Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

<span data-ttu-id="1d5c0-402">本附录将演示如何从 Azure 门户创建新网站，以及如何利用 Azure 提供的 Web 部署发布功能，发布通过实验室获取的应用程序。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-402">This appendix will show you how to create a new web site from the Azure Portal and publish the application you obtained by following the lab, taking advantage of the Web Deploy publishing feature provided by Azure.</span></span>

<a id="ApxCTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-azure-portal"></a><span data-ttu-id="1d5c0-403">任务 1-从 Azure 门户创建新网站</span><span class="sxs-lookup"><span data-stu-id="1d5c0-403">Task 1 - Creating a New Web Site from the Azure Portal</span></span>

1. <span data-ttu-id="1d5c0-404">请使用 [Azure 管理门户](https://manage.windowsazure.com/) ，并使用与你的订阅关联的 Microsoft 凭据登录。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-404">Go to the [Azure Management Portal](https://manage.windowsazure.com/) and sign in using the Microsoft credentials associated with your subscription.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1d5c0-405">借助 Azure，你可以免费托管10个 ASP.NET 的网站，然后随着流量的增长进行扩展。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-405">With Azure you can host 10 ASP.NET Web Sites for free and then scale as your traffic grows.</span></span> <span data-ttu-id="1d5c0-406">你可以在 [此处](https://aka.ms/aspnet-hol-azure)注册。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-406">You can sign up [here](https://aka.ms/aspnet-hol-azure).</span></span>

    <span data-ttu-id="1d5c0-407">![登录到 Microsoft Azure 门户](build-restful-apis-with-aspnet-web-api/_static/image39.png "登录到 Microsoft Azure 门户")</span><span class="sxs-lookup"><span data-stu-id="1d5c0-407">![Log on to Windows Azure portal](build-restful-apis-with-aspnet-web-api/_static/image39.png "Log on to Windows Azure portal")</span></span>

    <span data-ttu-id="1d5c0-408">*登录到门户*</span><span class="sxs-lookup"><span data-stu-id="1d5c0-408">*Log on to Portal*</span></span>
2. <span data-ttu-id="1d5c0-409">单击命令栏上的 " **新建** "。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-409">Click **New** on the command bar.</span></span>

    <span data-ttu-id="1d5c0-410">![创建新网站](build-restful-apis-with-aspnet-web-api/_static/image40.png "创建新网站")</span><span class="sxs-lookup"><span data-stu-id="1d5c0-410">![Creating a new Web Site](build-restful-apis-with-aspnet-web-api/_static/image40.png "Creating a new Web Site")</span></span>

    <span data-ttu-id="1d5c0-411">*创建新网站*</span><span class="sxs-lookup"><span data-stu-id="1d5c0-411">*Creating a new Web Site*</span></span>
3. <span data-ttu-id="1d5c0-412">单击 "**计算**  |  **网站"**。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-412">Click **Compute** | **Web Site**.</span></span> <span data-ttu-id="1d5c0-413">然后选择 " **快速创建** " 选项。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-413">Then select **Quick Create** option.</span></span> <span data-ttu-id="1d5c0-414">为新网站提供可用 URL，并单击 " **创建** 网站"。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-414">Provide an available URL for the new web site and click **Create Web Site**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1d5c0-415">Azure 是在云中运行的 web 应用程序的宿主，你可以控制和管理这些应用程序。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-415">Azure is the host for a web application running in the cloud that you can control and manage.</span></span> <span data-ttu-id="1d5c0-416">使用 "快速创建" 选项，可以从门户外部将已完成的 web 应用程序部署到 Azure。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-416">The Quick Create option allows you to deploy a completed web application to the Azure from outside the portal.</span></span> <span data-ttu-id="1d5c0-417">它不包括设置数据库的步骤。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-417">It does not include steps for setting up a database.</span></span>

    <span data-ttu-id="1d5c0-418">![使用“快速创建”创建新网站](build-restful-apis-with-aspnet-web-api/_static/image41.png "使用“快速创建”创建新网站")</span><span class="sxs-lookup"><span data-stu-id="1d5c0-418">![Creating a new Web Site using Quick Create](build-restful-apis-with-aspnet-web-api/_static/image41.png "Creating a new Web Site using Quick Create")</span></span>

    <span data-ttu-id="1d5c0-419">*使用“快速创建”创建新网站*</span><span class="sxs-lookup"><span data-stu-id="1d5c0-419">*Creating a new Web Site using Quick Create*</span></span>
4. <span data-ttu-id="1d5c0-420">请 **等到新网站创建完毕。**</span><span class="sxs-lookup"><span data-stu-id="1d5c0-420">Wait until the new **Web Site** is created.</span></span>
5. <span data-ttu-id="1d5c0-421">创建网站后，单击 " **URL** " 列下的链接。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-421">Once the Web Site is created click the link under the **URL** column.</span></span> <span data-ttu-id="1d5c0-422">检查新网站是否正常工作。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-422">Check that the new Web Site is working.</span></span>

    <span data-ttu-id="1d5c0-423">![浏览到新网站](build-restful-apis-with-aspnet-web-api/_static/image42.png "浏览到新网站")</span><span class="sxs-lookup"><span data-stu-id="1d5c0-423">![Browsing to the new web site](build-restful-apis-with-aspnet-web-api/_static/image42.png "Browsing to the new web site")</span></span>

    <span data-ttu-id="1d5c0-424">*浏览到新网站*</span><span class="sxs-lookup"><span data-stu-id="1d5c0-424">*Browsing to the new web site*</span></span>

    <span data-ttu-id="1d5c0-425">![网站正在运行](build-restful-apis-with-aspnet-web-api/_static/image43.png "网站正在运行")</span><span class="sxs-lookup"><span data-stu-id="1d5c0-425">![Web site running](build-restful-apis-with-aspnet-web-api/_static/image43.png "Web site running")</span></span>

    <span data-ttu-id="1d5c0-426">*网站正在运行*</span><span class="sxs-lookup"><span data-stu-id="1d5c0-426">*Web site running*</span></span>
6. <span data-ttu-id="1d5c0-427">返回到门户，并在 " **名称** " 列下单击网站的名称以显示管理页面。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-427">Go back to the portal and click the name of the web site under the **Name** column to display the management pages.</span></span>

    <span data-ttu-id="1d5c0-428">![打开网站管理页](build-restful-apis-with-aspnet-web-api/_static/image44.png "打开网站管理页")</span><span class="sxs-lookup"><span data-stu-id="1d5c0-428">![Opening the web site management pages](build-restful-apis-with-aspnet-web-api/_static/image44.png "Opening the web site management pages")</span></span>

    <span data-ttu-id="1d5c0-429">*打开网站管理页*</span><span class="sxs-lookup"><span data-stu-id="1d5c0-429">*Opening the Web Site management pages*</span></span>
7. <span data-ttu-id="1d5c0-430">在 " **仪表板** " 页的 " **速览** " 部分下，单击 " **下载发布配置文件** " 链接。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-430">In the **Dashboard** page, under the **quick glance** section, click the **Download publish profile** link.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1d5c0-431">*发布配置文件* 包含为每个已启用的发布方法将 web 应用程序发布到 Azure 所需的所有信息。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-431">The *publish profile* contains all of the information required to publish a web application to a Azure for each enabled publication method.</span></span> <span data-ttu-id="1d5c0-432">发布配置文件包含有连接到并且验证该发布方法启用的每个端点所需的 URL、用户凭据和数据库字符串。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-432">The publish profile contains the URLs, user credentials and database strings required to connect to and authenticate against each of the endpoints for which a publication method is enabled.</span></span> <span data-ttu-id="1d5c0-433">**Microsoft WebMatrix 2**、 **Microsoft Visual Studio Express for Web** 和 **Microsoft Visual Studio 2012** 支持读取发布配置文件，以便自动配置这些程序以将 Web 应用程序发布到 Azure。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-433">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** and **Microsoft Visual Studio 2012** support reading publish profiles to automate configuration of these programs for publishing web applications to Azure.</span></span>

    <span data-ttu-id="1d5c0-434">![下载网站发布配置文件](build-restful-apis-with-aspnet-web-api/_static/image45.png "下载网站发布配置文件")</span><span class="sxs-lookup"><span data-stu-id="1d5c0-434">![Downloading the web site publish profile](build-restful-apis-with-aspnet-web-api/_static/image45.png "Downloading the web site publish profile")</span></span>

    <span data-ttu-id="1d5c0-435">*下载网站发布配置文件*</span><span class="sxs-lookup"><span data-stu-id="1d5c0-435">*Downloading the Web Site publish profile*</span></span>
8. <span data-ttu-id="1d5c0-436">将发布配置文件下载到已知位置。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-436">Download the publish profile file to a known location.</span></span> <span data-ttu-id="1d5c0-437">在本练习中，你将了解如何使用此文件从 Visual Studio 将 web 应用程序发布到 Azure。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-437">Further in this exercise you will see how to use this file to publish a web application to Azure from Visual Studio.</span></span>

    <span data-ttu-id="1d5c0-438">![正在保存发布配置文件](build-restful-apis-with-aspnet-web-api/_static/image46.png "正在保存发布配置文件")</span><span class="sxs-lookup"><span data-stu-id="1d5c0-438">![Saving the publish profile file](build-restful-apis-with-aspnet-web-api/_static/image46.png "Saving the publish profile")</span></span>

    <span data-ttu-id="1d5c0-439">*正在保存发布配置文件*</span><span class="sxs-lookup"><span data-stu-id="1d5c0-439">*Saving the publish profile file*</span></span>

<a id="ApxCTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a><span data-ttu-id="1d5c0-440">任务 2-配置数据库服务器</span><span class="sxs-lookup"><span data-stu-id="1d5c0-440">Task 2 - Configuring the Database Server</span></span>

<span data-ttu-id="1d5c0-441">如果应用程序使用 SQL Server 数据库，则需要创建 SQL 数据库服务器。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-441">If your application makes use of SQL Server databases you will need to create a SQL Database server.</span></span> <span data-ttu-id="1d5c0-442">如果要部署不使用 SQL Server 的简单应用程序，则可以跳过此任务。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-442">If you want to deploy a simple application that does not use SQL Server you might skip this task.</span></span>

1. <span data-ttu-id="1d5c0-443">你将需要一个用于存储应用程序数据库的 SQL 数据库服务器。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-443">You will need a SQL Database server for storing the application database.</span></span> <span data-ttu-id="1d5c0-444">可以在 Azure 管理门户中的 **sql 数据库**  |  **服务器**  |  **的仪表板** 上查看订阅中的 sql 数据库服务器。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-444">You can view the SQL Database servers from your subscription in the Azure Management portal at **Sql Databases** | **Servers** | **Server's Dashboard**.</span></span> <span data-ttu-id="1d5c0-445">如果尚未创建服务器，可以使用命令栏上的 " **添加** " 按钮创建一个服务器。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-445">If you do not have a server created, you can create one using the **Add** button on the command bar.</span></span> <span data-ttu-id="1d5c0-446">记下 **服务器名称和 URL、管理员登录名和密码**，因为你将在后续任务中使用它们。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-446">Take note of the **server name and URL, administrator login name and password**, as you will use them in the next tasks.</span></span> <span data-ttu-id="1d5c0-447">请不要创建数据库，因为它将在后面的阶段创建。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-447">Do not create the database yet, as it will be created in a later stage.</span></span>

    <span data-ttu-id="1d5c0-448">![SQL 数据库服务器仪表板](build-restful-apis-with-aspnet-web-api/_static/image47.png "SQL 数据库服务器仪表板")</span><span class="sxs-lookup"><span data-stu-id="1d5c0-448">![SQL Database Server Dashboard](build-restful-apis-with-aspnet-web-api/_static/image47.png "SQL Database Server Dashboard")</span></span>

    <span data-ttu-id="1d5c0-449">*SQL 数据库服务器仪表板*</span><span class="sxs-lookup"><span data-stu-id="1d5c0-449">*SQL Database Server Dashboard*</span></span>
2. <span data-ttu-id="1d5c0-450">在下一任务中，您将从 Visual Studio 测试数据库连接，因此，需要在服务器的 **允许 IP 地址** 列表中包含本地 ip 地址。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-450">In the next task you will test the database connection from Visual Studio, for that reason you need to include your local IP address in the server's list of **Allowed IP Addresses**.</span></span> <span data-ttu-id="1d5c0-451">要执行此操作，请单击 " **配置**"，从 " **当前客户端 IP 地址** " 选择 ip 地址，并将其粘贴到 " **起始 Ip 地址** " 和 " **结束 ip 地址** " 文本框中，然后单击 " ![ 添加-客户端-IP 地址-确定" ](build-restful-apis-with-aspnet-web-api/_static/image48.png) 按钮。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-451">To do that, click **Configure**, select the IP address from **Current Client IP Address** and paste it on the **Start IP Address** and **End IP Address** text boxes and click the ![add-client-ip-address-ok-button](build-restful-apis-with-aspnet-web-api/_static/image48.png) button.</span></span>

    ![添加客户端 IP 地址](build-restful-apis-with-aspnet-web-api/_static/image49.png)

    <span data-ttu-id="1d5c0-453">*添加客户端 IP 地址*</span><span class="sxs-lookup"><span data-stu-id="1d5c0-453">*Adding Client IP Address*</span></span>
3. <span data-ttu-id="1d5c0-454">将 **客户端 Ip 地址** 添加到 "允许的 IP 地址" 列表中后，单击 " **保存** " 以确认更改。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-454">Once the **Client IP Address** is added to the allowed IP addresses list, click on **Save** to confirm the changes.</span></span>

    ![确认更改](build-restful-apis-with-aspnet-web-api/_static/image50.png)

    <span data-ttu-id="1d5c0-456">*确认更改*</span><span class="sxs-lookup"><span data-stu-id="1d5c0-456">*Confirm Changes*</span></span>

<a id="ApxCTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="1d5c0-457">任务 3-使用 Web 部署发布 ASP.NET MVC 4 应用程序</span><span class="sxs-lookup"><span data-stu-id="1d5c0-457">Task 3 - Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

1. <span data-ttu-id="1d5c0-458">返回到 ASP.NET MVC 4 解决方案。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-458">Go back to the ASP.NET MVC 4 solution.</span></span> <span data-ttu-id="1d5c0-459">在 **解决方案资源管理器** 中，右键单击网站项目，然后选择 " **发布**"。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-459">In the **Solution Explorer**, right-click the web site project and select **Publish**.</span></span>

    <span data-ttu-id="1d5c0-460">![发布应用程序](build-restful-apis-with-aspnet-web-api/_static/image51.png "发布应用程序")</span><span class="sxs-lookup"><span data-stu-id="1d5c0-460">![Publishing the Application](build-restful-apis-with-aspnet-web-api/_static/image51.png "Publishing the Application")</span></span>

    <span data-ttu-id="1d5c0-461">*发布网站*</span><span class="sxs-lookup"><span data-stu-id="1d5c0-461">*Publishing the web site*</span></span>
2. <span data-ttu-id="1d5c0-462">导入您在第一个任务中保存的发布配置文件。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-462">Import the publish profile you saved in the first task.</span></span>

    <span data-ttu-id="1d5c0-463">![导入发布配置文件](build-restful-apis-with-aspnet-web-api/_static/image52.png "导入发布配置文件")</span><span class="sxs-lookup"><span data-stu-id="1d5c0-463">![Importing the publish profile](build-restful-apis-with-aspnet-web-api/_static/image52.png "Importing the publish profile")</span></span>

    <span data-ttu-id="1d5c0-464">*导入发布配置文件*</span><span class="sxs-lookup"><span data-stu-id="1d5c0-464">*Importing publish profile*</span></span>
3. <span data-ttu-id="1d5c0-465">单击 " **验证连接**"。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-465">Click **Validate Connection**.</span></span> <span data-ttu-id="1d5c0-466">验证完成后，单击 " **下一步**"。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-466">Once Validation is complete click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1d5c0-467">验证完成后，"验证连接" 按钮旁边会出现一个绿色的复选标记。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-467">Validation is complete once you see a green checkmark appear next to the Validate Connection button.</span></span>

    <span data-ttu-id="1d5c0-468">![正在验证连接](build-restful-apis-with-aspnet-web-api/_static/image53.png "正在验证连接")</span><span class="sxs-lookup"><span data-stu-id="1d5c0-468">![Validating connection](build-restful-apis-with-aspnet-web-api/_static/image53.png "Validating connection")</span></span>

    <span data-ttu-id="1d5c0-469">*正在验证连接*</span><span class="sxs-lookup"><span data-stu-id="1d5c0-469">*Validating connection*</span></span>
4. <span data-ttu-id="1d5c0-470">在 " **设置** " 页的 " **数据库** " 部分下，单击数据库连接的文本框旁边的按钮， (**DefaultConnection**) 。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-470">In the **Settings** page, under the **Databases** section, click the button next to your database connection's textbox (i.e. **DefaultConnection**).</span></span>

    <span data-ttu-id="1d5c0-471">![Web 部署配置](build-restful-apis-with-aspnet-web-api/_static/image54.png "Web 部署配置")</span><span class="sxs-lookup"><span data-stu-id="1d5c0-471">![Web deploy configuration](build-restful-apis-with-aspnet-web-api/_static/image54.png "Web deploy configuration")</span></span>

    <span data-ttu-id="1d5c0-472">*Web 部署配置*</span><span class="sxs-lookup"><span data-stu-id="1d5c0-472">*Web deploy configuration*</span></span>
5. <span data-ttu-id="1d5c0-473">按如下所示配置数据库连接：</span><span class="sxs-lookup"><span data-stu-id="1d5c0-473">Configure the database connection as follows:</span></span>

   - <span data-ttu-id="1d5c0-474">在 " **服务器名称** " 中，键入您的 SQL 数据库服务器 URL，使用 *tcp：* prefix。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-474">In the **Server name** type your SQL Database server URL using the *tcp:* prefix.</span></span>
   - <span data-ttu-id="1d5c0-475">在 " **用户名** " 中键入服务器管理员登录名。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-475">In **User name** type your server administrator login name.</span></span>
   - <span data-ttu-id="1d5c0-476">在 " **密码** " 中键入服务器管理员登录密码。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-476">In **Password** type your server administrator login password.</span></span>
   - <span data-ttu-id="1d5c0-477">键入新的数据库名称，例如： *MVC4SampleDB*。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-477">Type a new database name, for example: *MVC4SampleDB*.</span></span>

     <span data-ttu-id="1d5c0-478">![正在配置目标连接字符串](build-restful-apis-with-aspnet-web-api/_static/image55.png "正在配置目标连接字符串")</span><span class="sxs-lookup"><span data-stu-id="1d5c0-478">![Configuring destination connection string](build-restful-apis-with-aspnet-web-api/_static/image55.png "Configuring destination connection string")</span></span>

     <span data-ttu-id="1d5c0-479">*正在配置目标连接字符串*</span><span class="sxs-lookup"><span data-stu-id="1d5c0-479">*Configuring destination connection string*</span></span>
6. <span data-ttu-id="1d5c0-480">。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-480">Then click **OK**.</span></span> <span data-ttu-id="1d5c0-481">系统提示创建数据库时，单击 **"是"**。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-481">When prompted to create the database click **Yes**.</span></span>

    <span data-ttu-id="1d5c0-482">![创建数据库](build-restful-apis-with-aspnet-web-api/_static/image56.png "创建数据库字符串")</span><span class="sxs-lookup"><span data-stu-id="1d5c0-482">![Creating the database](build-restful-apis-with-aspnet-web-api/_static/image56.png "Creating the database string")</span></span>

    <span data-ttu-id="1d5c0-483">*创建数据库*</span><span class="sxs-lookup"><span data-stu-id="1d5c0-483">*Creating the database*</span></span>
7. <span data-ttu-id="1d5c0-484">将用于连接到 Windows Azure 中的 SQL 数据库的连接字符串显示在 "默认连接" 文本框中。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-484">The connection string you will use to connect to SQL Database in Windows Azure is shown within Default Connection textbox.</span></span> <span data-ttu-id="1d5c0-485">然后单击“下一步”。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-485">Then click **Next**.</span></span>

    <span data-ttu-id="1d5c0-486">![指向 SQL 数据库的连接字符串](build-restful-apis-with-aspnet-web-api/_static/image57.png "指向 SQL 数据库的连接字符串")</span><span class="sxs-lookup"><span data-stu-id="1d5c0-486">![Connection string pointing to SQL Database](build-restful-apis-with-aspnet-web-api/_static/image57.png "Connection string pointing to SQL Database")</span></span>

    <span data-ttu-id="1d5c0-487">*指向 SQL 数据库的连接字符串*</span><span class="sxs-lookup"><span data-stu-id="1d5c0-487">*Connection string pointing to SQL Database*</span></span>
8. <span data-ttu-id="1d5c0-488">在 " **预览** " 页上，单击 " **发布**"。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-488">In the **Preview** page, click **Publish**.</span></span>

    <span data-ttu-id="1d5c0-489">![发布 web 应用程序](build-restful-apis-with-aspnet-web-api/_static/image58.png "发布 web 应用程序")</span><span class="sxs-lookup"><span data-stu-id="1d5c0-489">![Publishing the web application](build-restful-apis-with-aspnet-web-api/_static/image58.png "Publishing the web application")</span></span>

    <span data-ttu-id="1d5c0-490">*发布 web 应用程序*</span><span class="sxs-lookup"><span data-stu-id="1d5c0-490">*Publishing the web application*</span></span>
9. <span data-ttu-id="1d5c0-491">发布过程完成后，您的默认浏览器将打开已发布的网站。</span><span class="sxs-lookup"><span data-stu-id="1d5c0-491">Once the publishing process finishes, your default browser will open the published web site.</span></span>

    <span data-ttu-id="1d5c0-492">![发布到 Windows Azure 的应用程序](build-restful-apis-with-aspnet-web-api/_static/image59.png "发布到 Windows Azure 的应用程序")</span><span class="sxs-lookup"><span data-stu-id="1d5c0-492">![Application published to Windows Azure](build-restful-apis-with-aspnet-web-api/_static/image59.png "Application published to Windows Azure")</span></span>

    <span data-ttu-id="1d5c0-493">*已将应用程序发布到 Azure*</span><span class="sxs-lookup"><span data-stu-id="1d5c0-493">*Application published to Azure*</span></span>

---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-custom-action-filters
title: ASP.NET MVC 4 自定义操作筛选器 |Microsoft Docs
author: rick-anderson
description: ASP.NET MVC 提供操作筛选器，用于在调用操作方法之前或之后执行筛选逻辑。 操作筛选器是自定义属性。
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 969ab824-1b98-4552-81fe-b60ef5fc6887
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-custom-action-filters
msc.type: authoredcontent
ms.openlocfilehash: eaeb32180f79fabf557cbc38ff067eb26b47fea7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78468176"
---
# <a name="aspnet-mvc-4-custom-action-filters"></a><span data-ttu-id="bf36c-104">ASP.NET MVC 4 自定义操作筛选器</span><span class="sxs-lookup"><span data-stu-id="bf36c-104">ASP.NET MVC 4 Custom Action Filters</span></span>

<span data-ttu-id="bf36c-105">由[Web 训练营团队](https://twitter.com/webcamps)使用</span><span class="sxs-lookup"><span data-stu-id="bf36c-105">By [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="bf36c-106">下载 Web 训练营培训工具包</span><span class="sxs-lookup"><span data-stu-id="bf36c-106">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

<span data-ttu-id="bf36c-107">ASP.NET MVC 提供操作筛选器，用于在调用操作方法之前或之后执行筛选逻辑。</span><span class="sxs-lookup"><span data-stu-id="bf36c-107">ASP.NET MVC provides Action Filters for executing filtering logic either before or after an action method is called.</span></span> <span data-ttu-id="bf36c-108">操作筛选器是自定义属性，可提供声明性方法，以将操作前和操作后行为添加到控制器的操作方法。</span><span class="sxs-lookup"><span data-stu-id="bf36c-108">Action Filters are custom attributes that provide declarative means to add pre-action and post-action behavior to the controller's action methods.</span></span>

<span data-ttu-id="bf36c-109">在此动手实验中，你将在 MvcMusicStore 解决方案中创建自定义操作筛选器属性，以捕获控制器的请求并将站点的活动记录到数据库表中。</span><span class="sxs-lookup"><span data-stu-id="bf36c-109">In this Hands-on Lab you will create a custom action filter attribute into MvcMusicStore solution to catch controller's requests and log the activity of a site into a database table.</span></span> <span data-ttu-id="bf36c-110">你可以通过注入到任何控制器或操作来添加日志筛选器。</span><span class="sxs-lookup"><span data-stu-id="bf36c-110">You will be able to add your logging filter by injection to any controller or action.</span></span> <span data-ttu-id="bf36c-111">最后，您将看到显示访问者列表的日志视图。</span><span class="sxs-lookup"><span data-stu-id="bf36c-111">Finally, you will see the log view that shows the list of visitors.</span></span>

<span data-ttu-id="bf36c-112">此动手实验假设你具有**ASP.NET MVC**的基本知识。</span><span class="sxs-lookup"><span data-stu-id="bf36c-112">This Hands-on Lab assumes you have basic knowledge of **ASP.NET MVC**.</span></span> <span data-ttu-id="bf36c-113">如果你之前未使用过**ASP.NET mvc** ，则建议你浏览**ASP.NET mvc 4 基础**动手实验。</span><span class="sxs-lookup"><span data-stu-id="bf36c-113">If you have not used **ASP.NET MVC** before, we recommend you to go over **ASP.NET MVC 4 Fundamentals** Hands-on Lab.</span></span>

> [!NOTE]
> <span data-ttu-id="bf36c-114">所有示例代码和代码段都包含在 Web 训练营培训工具包中，可从[Microsoft-Web/WebCampTrainingKit 版本](https://aka.ms/webcamps-training-kit)获取。</span><span class="sxs-lookup"><span data-stu-id="bf36c-114">All sample code and snippets are included in the Web Camps Training Kit, available from at [Microsoft-Web/WebCampTrainingKit Releases](https://aka.ms/webcamps-training-kit).</span></span> <span data-ttu-id="bf36c-115">[ASP.NET MVC 4 自定义操作筛选器](https://github.com/Microsoft-Web/HOL-MVC4CustomActionFilters)中提供了此实验室特定的项目。</span><span class="sxs-lookup"><span data-stu-id="bf36c-115">The project specific to this lab is available at [ASP.NET MVC 4 Custom Action Filters](https://github.com/Microsoft-Web/HOL-MVC4CustomActionFilters).</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="bf36c-116">目标</span><span class="sxs-lookup"><span data-stu-id="bf36c-116">Objectives</span></span>

<span data-ttu-id="bf36c-117">在此动手实验中，您将学习如何：</span><span class="sxs-lookup"><span data-stu-id="bf36c-117">In this Hands-On Lab, you will learn how to:</span></span>

- <span data-ttu-id="bf36c-118">创建自定义操作筛选器特性来扩展筛选功能</span><span class="sxs-lookup"><span data-stu-id="bf36c-118">Create a custom action filter attribute to extend filtering capabilities</span></span>
- <span data-ttu-id="bf36c-119">通过注入到特定级别应用自定义筛选器属性</span><span class="sxs-lookup"><span data-stu-id="bf36c-119">Apply a custom filter attribute by injection to a specific level</span></span>
- <span data-ttu-id="bf36c-120">全局注册自定义操作筛选器</span><span class="sxs-lookup"><span data-stu-id="bf36c-120">Register a custom action filters globally</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="bf36c-121">系统必备</span><span class="sxs-lookup"><span data-stu-id="bf36c-121">Prerequisites</span></span>

<span data-ttu-id="bf36c-122">你必须具有以下项才能完成此实验室：</span><span class="sxs-lookup"><span data-stu-id="bf36c-122">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="bf36c-123">适用于 Web 或高级的[Microsoft Visual Studio Express 2012](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) （阅读[附录 A](#AppendixA)以获取有关如何安装的说明）。</span><span class="sxs-lookup"><span data-stu-id="bf36c-123">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix A](#AppendixA) for instructions on how to install it).</span></span>

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="bf36c-124">安装</span><span class="sxs-lookup"><span data-stu-id="bf36c-124">Setup</span></span>

<span data-ttu-id="bf36c-125">**安装代码片段**</span><span class="sxs-lookup"><span data-stu-id="bf36c-125">**Installing Code Snippets**</span></span>

<span data-ttu-id="bf36c-126">为方便起见，你将通过此实验室管理的大部分代码都作为 Visual Studio code 片段提供。</span><span class="sxs-lookup"><span data-stu-id="bf36c-126">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="bf36c-127">若要安装代码段，请运行 **.\Source\Setup\CodeSnippets.vsi**文件。</span><span class="sxs-lookup"><span data-stu-id="bf36c-127">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="bf36c-128">如果你不熟悉 Visual Studio Code 代码段，并且想要了解如何使用它们，则可以参考本文档中的附录[C： &quot;附录 C：&quot;的代码段](#AppendixC)。</span><span class="sxs-lookup"><span data-stu-id="bf36c-128">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix C: Using Code Snippets](#AppendixC)&quot;.</span></span>

---

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="bf36c-129">练习</span><span class="sxs-lookup"><span data-stu-id="bf36c-129">Exercises</span></span>

<span data-ttu-id="bf36c-130">此动手实验包括以下练习：</span><span class="sxs-lookup"><span data-stu-id="bf36c-130">This Hands-On Lab is comprised by the following exercises:</span></span>

1. [<span data-ttu-id="bf36c-131">练习1：记录操作</span><span class="sxs-lookup"><span data-stu-id="bf36c-131">Exercise 1: Logging actions</span></span>](#Exercise1)
2. [<span data-ttu-id="bf36c-132">练习2：管理多个操作筛选器</span><span class="sxs-lookup"><span data-stu-id="bf36c-132">Exercise 2: Managing Multiple Action Filters</span></span>](#Exercise2)

<span data-ttu-id="bf36c-133">完成本实验的估计时间： **30 分钟**。</span><span class="sxs-lookup"><span data-stu-id="bf36c-133">Estimated time to complete this lab: **30 minutes**.</span></span>

> [!NOTE]
> <span data-ttu-id="bf36c-134">每个练习都带有一个**结束**文件夹，其中包含在完成练习后应获得的结果解决方案。</span><span class="sxs-lookup"><span data-stu-id="bf36c-134">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="bf36c-135">如果需要更多帮助，请使用此解决方案作为指导。</span><span class="sxs-lookup"><span data-stu-id="bf36c-135">You can use this solution as a guide if you need additional help working through the exercises.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Logging_Actions"></a>
### <a name="exercise-1-logging-actions"></a><span data-ttu-id="bf36c-136">练习1：记录操作</span><span class="sxs-lookup"><span data-stu-id="bf36c-136">Exercise 1: Logging Actions</span></span>

<span data-ttu-id="bf36c-137">在此练习中，您将学习如何使用 ASP.NET MVC 4 筛选器提供程序创建自定义操作日志筛选器。</span><span class="sxs-lookup"><span data-stu-id="bf36c-137">In this exercise, you will learn how to create a custom action log filter by using ASP.NET MVC 4 Filter Providers.</span></span> <span data-ttu-id="bf36c-138">出于此目的，你需要将日志记录筛选器应用到 MusicStore 站点，该站点将记录所选控制器中的所有活动。</span><span class="sxs-lookup"><span data-stu-id="bf36c-138">For that purpose you will apply a logging filter to the MusicStore site that will record all the activities in the selected controllers.</span></span>

<span data-ttu-id="bf36c-139">筛选器将扩展**ActionFilterAttributeClass**并重写**OnActionExecuting**方法以捕获每个请求，然后执行日志记录操作。</span><span class="sxs-lookup"><span data-stu-id="bf36c-139">The filter will extend **ActionFilterAttributeClass** and override **OnActionExecuting** method to catch each request and then perform the logging actions.</span></span> <span data-ttu-id="bf36c-140">ASP.NET MVC **ActionExecutingContext**类将提供有关 HTTP 请求、执行方法、结果和参数的上下文信息 **。**</span><span class="sxs-lookup"><span data-stu-id="bf36c-140">The context information about HTTP requests, executing methods, results and parameters will be provided by ASP.NET MVC **ActionExecutingContext** class **.**</span></span>

> [!NOTE]
> <span data-ttu-id="bf36c-141">ASP.NET MVC 4 还具有可在不创建自定义筛选器的情况下使用的默认筛选器提供程序。</span><span class="sxs-lookup"><span data-stu-id="bf36c-141">ASP.NET MVC 4 also has default filters providers you can use without creating a custom filter.</span></span> <span data-ttu-id="bf36c-142">ASP.NET MVC 4 提供以下类型的筛选器：</span><span class="sxs-lookup"><span data-stu-id="bf36c-142">ASP.NET MVC 4 provides the following types of filters:</span></span>
> 
> - <span data-ttu-id="bf36c-143">**授权**筛选器，用于做出有关是否执行操作方法的安全决策，如执行身份验证或验证请求的属性。</span><span class="sxs-lookup"><span data-stu-id="bf36c-143">**Authorization** filter, which makes security decisions about whether to execute an action method, such as performing authentication or validating properties of the request.</span></span>
> - <span data-ttu-id="bf36c-144">**操作**筛选器，它将操作方法执行打包。</span><span class="sxs-lookup"><span data-stu-id="bf36c-144">**Action** filter, which wraps the action method execution.</span></span> <span data-ttu-id="bf36c-145">此筛选器可以执行其他处理，如向操作方法提供额外数据、检查返回值或取消操作方法的执行</span><span class="sxs-lookup"><span data-stu-id="bf36c-145">This filter can perform additional processing, such as providing extra data to the action method, inspecting the return value, or canceling execution of the action method</span></span>
> - <span data-ttu-id="bf36c-146">**结果**筛选器，用于包装 ActionResult 对象的执行。</span><span class="sxs-lookup"><span data-stu-id="bf36c-146">**Result** filter, which wraps execution of the ActionResult object.</span></span> <span data-ttu-id="bf36c-147">此筛选器可以对结果执行其他处理，如修改 HTTP 响应。</span><span class="sxs-lookup"><span data-stu-id="bf36c-147">This filter can perform additional processing of the result, such as modifying the HTTP response.</span></span>
> - <span data-ttu-id="bf36c-148">**异常**筛选器，如果在操作方法中的某个位置引发了未经处理的异常，则将执行该筛选器，从授权筛选器开始，到结果的执行结束。</span><span class="sxs-lookup"><span data-stu-id="bf36c-148">**Exception** filter, which executes if there is an unhandled exception thrown somewhere in action method, starting with the authorization filters and ending with the execution of the result.</span></span> <span data-ttu-id="bf36c-149">异常筛选器可用于执行诸如日志记录或显示错误页之类的任务。</span><span class="sxs-lookup"><span data-stu-id="bf36c-149">Exception filters can be used for tasks such as logging or displaying an error page.</span></span>
> 
> <span data-ttu-id="bf36c-150">有关筛选器提供程序的详细信息，请访问此 MSDN 链接：（[https://msdn.microsoft.com/library/dd410209.aspx](https://msdn.microsoft.com/library/dd410209.aspx)）。</span><span class="sxs-lookup"><span data-stu-id="bf36c-150">For more information about Filters Providers please visit this MSDN link: ([https://msdn.microsoft.com/library/dd410209.aspx](https://msdn.microsoft.com/library/dd410209.aspx)) .</span></span>

<a id="AboutLoggingFeature"></a>

<a id="About_MVC_Music_Store_Application_logging_feature"></a>
#### <a name="about-mvc-music-store-application-logging-feature"></a><span data-ttu-id="bf36c-151">关于 MVC 音乐商店应用程序日志记录功能</span><span class="sxs-lookup"><span data-stu-id="bf36c-151">About MVC Music Store Application logging feature</span></span>

<span data-ttu-id="bf36c-152">此音乐应用商店解决方案有一个新的用于站点日志记录的数据模型表**ActionLog**，其中包含以下字段：收到请求的控制器的名称，称为 "操作"、"客户端 IP" 和 "时间戳"。</span><span class="sxs-lookup"><span data-stu-id="bf36c-152">This Music Store solution has a new data model table for site logging, **ActionLog**, with the following fields: Name of the controller that received a request, Called action, Client IP and Time stamp.</span></span>

<span data-ttu-id="bf36c-153">![数据模型。ActionLog 表。](aspnet-mvc-4-custom-action-filters/_static/image1.png "数据模型。ActionLog 表。")</span><span class="sxs-lookup"><span data-stu-id="bf36c-153">![Data model. ActionLog table.](aspnet-mvc-4-custom-action-filters/_static/image1.png "Data model. ActionLog table.")</span></span>

<span data-ttu-id="bf36c-154">*数据模型-ActionLog 表*</span><span class="sxs-lookup"><span data-stu-id="bf36c-154">*Data model - ActionLog table*</span></span>

<span data-ttu-id="bf36c-155">此解决方案提供了可在**MvcMusicStores/Views/ActionLog**上找到的操作日志的 ASP.NET MVC 视图：</span><span class="sxs-lookup"><span data-stu-id="bf36c-155">The solution provides an ASP.NET MVC View for the Action log that can be found at **MvcMusicStores/Views/ActionLog**:</span></span>

<span data-ttu-id="bf36c-156">![操作日志视图](aspnet-mvc-4-custom-action-filters/_static/image2.png "操作日志视图")</span><span class="sxs-lookup"><span data-stu-id="bf36c-156">![Action Log view](aspnet-mvc-4-custom-action-filters/_static/image2.png "Action Log view")</span></span>

<span data-ttu-id="bf36c-157">*操作日志视图*</span><span class="sxs-lookup"><span data-stu-id="bf36c-157">*Action Log view*</span></span>

<span data-ttu-id="bf36c-158">使用此给定结构，所有工作都将重点放在中断控制器的请求并使用自定义筛选执行日志记录。</span><span class="sxs-lookup"><span data-stu-id="bf36c-158">With this given structure, all the work will be focused on interrupting controller's request and performing the logging by using custom filtering.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_a_Custom_Filter_to_Catch_a_Controllers_Request"></a>
#### <a name="task-1---creating-a-custom-filter-to-catch-a-controllers-request"></a><span data-ttu-id="bf36c-159">任务 1-创建自定义筛选器以捕获控制器的请求</span><span class="sxs-lookup"><span data-stu-id="bf36c-159">Task 1 - Creating a Custom Filter to Catch a Controller's Request</span></span>

<span data-ttu-id="bf36c-160">在此任务中，您将创建一个将包含日志记录逻辑的自定义筛选器属性类。</span><span class="sxs-lookup"><span data-stu-id="bf36c-160">In this task you will create a custom filter attribute class that will contain the logging logic.</span></span> <span data-ttu-id="bf36c-161">出于此目的，你将扩展 ASP.NET MVC **ActionFilterAttribute**类并实现接口**IActionFilter**。</span><span class="sxs-lookup"><span data-stu-id="bf36c-161">For that purpose you will extend ASP.NET MVC **ActionFilterAttribute** Class and implement the interface **IActionFilter**.</span></span>

> [!NOTE]
> <span data-ttu-id="bf36c-162">**ActionFilterAttribute**是所有属性筛选器的基类。</span><span class="sxs-lookup"><span data-stu-id="bf36c-162">The **ActionFilterAttribute** is the base class for all the attribute filters.</span></span> <span data-ttu-id="bf36c-163">它提供以下方法，以便在控制器操作的执行前后执行特定逻辑：</span><span class="sxs-lookup"><span data-stu-id="bf36c-163">It provides the following methods to execute a specific logic after and before controller action's execution:</span></span>
> 
> - <span data-ttu-id="bf36c-164">**OnActionExecuting**（ActionExecutingContext filterContext）：在调用操作方法之前。</span><span class="sxs-lookup"><span data-stu-id="bf36c-164">**OnActionExecuting**(ActionExecutingContext filterContext): Just before the action method is called.</span></span>
> - <span data-ttu-id="bf36c-165">**OnActionExecuted**（ActionExecutedContext filterContext）：调用操作方法并在执行结果之前（视图呈现之前）。</span><span class="sxs-lookup"><span data-stu-id="bf36c-165">**OnActionExecuted**(ActionExecutedContext filterContext): After the action method is called and before the result is executed (before view render).</span></span>
> - <span data-ttu-id="bf36c-166">**OnResultExecuting**（ResultExecutingContext filterContext）：在执行结果之前（视图呈现之前）。</span><span class="sxs-lookup"><span data-stu-id="bf36c-166">**OnResultExecuting**(ResultExecutingContext filterContext): Just before the result is executed (before view render).</span></span>
> - <span data-ttu-id="bf36c-167">**OnResultExecuted**（ResultExecutedContext filterContext）：执行结果后（呈现视图后）。</span><span class="sxs-lookup"><span data-stu-id="bf36c-167">**OnResultExecuted**(ResultExecutedContext filterContext): After the result is executed (after the view is rendered).</span></span>
> 
> <span data-ttu-id="bf36c-168">通过将这些方法中的任何方法重写到派生类中，你可以执行自己的筛选代码。</span><span class="sxs-lookup"><span data-stu-id="bf36c-168">By overriding any of these methods into a derived class, you can execute your own filtering code.</span></span>

1. <span data-ttu-id="bf36c-169">打开位于 **\Source\Ex01-LoggingActions\Begin**文件夹的 "**开始**" 解决方案。</span><span class="sxs-lookup"><span data-stu-id="bf36c-169">Open the **Begin** solution located at **\Source\Ex01-LoggingActions\Begin** folder.</span></span>

   1. <span data-ttu-id="bf36c-170">在继续之前，你将需要下载某些缺少的 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="bf36c-170">You will need to download some missing NuGet packages before you continue.</span></span> <span data-ttu-id="bf36c-171">为此，请单击 "**项目**" 菜单并选择 "**管理 NuGet 包**"。</span><span class="sxs-lookup"><span data-stu-id="bf36c-171">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="bf36c-172">在 "**管理 NuGet 包**" 对话框中，单击 "**还原**" 以下载缺少的包。</span><span class="sxs-lookup"><span data-stu-id="bf36c-172">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="bf36c-173">最后，通过单击 "**生成** | **生成解决方案**" 来生成解决方案。</span><span class="sxs-lookup"><span data-stu-id="bf36c-173">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="bf36c-174">使用 NuGet 的优点之一是，无需将所有库都送到项目中，从而减少了项目的大小。</span><span class="sxs-lookup"><span data-stu-id="bf36c-174">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="bf36c-175">使用 NuGet 功能，通过在包 .config 文件中指定包版本，你可以在首次运行项目时下载所有必需的库。</span><span class="sxs-lookup"><span data-stu-id="bf36c-175">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="bf36c-176">这就是在从此实验室打开现有解决方案之后需要运行这些步骤的原因。</span><span class="sxs-lookup"><span data-stu-id="bf36c-176">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
      > 
      > <span data-ttu-id="bf36c-177">有关详细信息，请参阅此文章： [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages)。</span><span class="sxs-lookup"><span data-stu-id="bf36c-177">For more information, see this article: [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages).</span></span>
2. <span data-ttu-id="bf36c-178">将新C#类添加到**Filters**文件夹，并将其命名为*CustomActionFilter.cs*。</span><span class="sxs-lookup"><span data-stu-id="bf36c-178">Add a new C# class into the **Filters** folder and name it *CustomActionFilter.cs*.</span></span> <span data-ttu-id="bf36c-179">此文件夹将存储所有自定义筛选器。</span><span class="sxs-lookup"><span data-stu-id="bf36c-179">This folder will store all the custom filters.</span></span>
3. <span data-ttu-id="bf36c-180">打开**CustomActionFilter.cs** ，并添加对**system.web**和**MvcMusicStore**命名空间的引用：</span><span class="sxs-lookup"><span data-stu-id="bf36c-180">Open **CustomActionFilter.cs** and add a reference to **System.Web.Mvc** and **MvcMusicStore.Models** namespaces:</span></span>

    <span data-ttu-id="bf36c-181">（代码段- *ASP.NET MVC 4 自定义操作筛选器-Ex1-CustomActionFilterNamespaces*）</span><span class="sxs-lookup"><span data-stu-id="bf36c-181">(Code Snippet - *ASP.NET MVC 4 Custom Action Filters - Ex1-CustomActionFilterNamespaces*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample1.cs)]
4. <span data-ttu-id="bf36c-182">从**ActionFilterAttribute**继承**CustomActionFilter**类，然后使**CustomActionFilter**类实现**IActionFilter**接口。</span><span class="sxs-lookup"><span data-stu-id="bf36c-182">Inherit the **CustomActionFilter** class from **ActionFilterAttribute** and then make **CustomActionFilter** class implement **IActionFilter** interface.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample2.cs)]
5. <span data-ttu-id="bf36c-183">使**CustomActionFilter**类重写方法**OnActionExecuting** ，并添加必要的逻辑来记录筛选器的执行。</span><span class="sxs-lookup"><span data-stu-id="bf36c-183">Make **CustomActionFilter** class override the method **OnActionExecuting** and add the necessary logic to log the filter's execution.</span></span> <span data-ttu-id="bf36c-184">为此，请在**CustomActionFilter**类中添加以下突出显示的代码。</span><span class="sxs-lookup"><span data-stu-id="bf36c-184">To do this, add the following highlighted code within **CustomActionFilter** class.</span></span>

    <span data-ttu-id="bf36c-185">（代码段- *ASP.NET MVC 4 自定义操作筛选器-Ex1-LoggingActions*）</span><span class="sxs-lookup"><span data-stu-id="bf36c-185">(Code Snippet - *ASP.NET MVC 4 Custom Action Filters - Ex1-LoggingActions*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample3.cs#Highlight)]

    > [!NOTE]
    > <span data-ttu-id="bf36c-186">**OnActionExecuting**方法正在使用**实体框架**来添加新的 ActionLog 寄存器。</span><span class="sxs-lookup"><span data-stu-id="bf36c-186">**OnActionExecuting** method is using **Entity Framework** to add a new ActionLog register.</span></span> <span data-ttu-id="bf36c-187">它使用来自**filterContext**的上下文信息创建并填充新的实体实例。</span><span class="sxs-lookup"><span data-stu-id="bf36c-187">It creates and fills a new entity instance with the context information from **filterContext**.</span></span>
    > 
    > <span data-ttu-id="bf36c-188">可在[msdn](https://msdn.microsoft.com/library/system.web.mvc.controllercontext.aspx)上阅读有关**ControllerContext**类的详细信息。</span><span class="sxs-lookup"><span data-stu-id="bf36c-188">You can read more about **ControllerContext** class at [msdn](https://msdn.microsoft.com/library/system.web.mvc.controllercontext.aspx).</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Injecting_a_Code_Interceptor_into_the_Store_Controller_Class"></a>
#### <a name="task-2---injecting-a-code-interceptor-into-the-store-controller-class"></a><span data-ttu-id="bf36c-189">任务 2-将代码侦听器注入到存储控制器类中</span><span class="sxs-lookup"><span data-stu-id="bf36c-189">Task 2 - Injecting a Code Interceptor into the Store Controller Class</span></span>

<span data-ttu-id="bf36c-190">在此任务中，你将通过将自定义筛选器注入到将记录的所有控制器类和控制器操作来添加该筛选器。</span><span class="sxs-lookup"><span data-stu-id="bf36c-190">In this task you will add the custom filter by injecting it to all controller classes and controller actions that will be logged.</span></span> <span data-ttu-id="bf36c-191">对于本练习，商店控制器类将有一个日志。</span><span class="sxs-lookup"><span data-stu-id="bf36c-191">For the purpose of this exercise, the Store Controller class will have a log.</span></span>

<span data-ttu-id="bf36c-192">调用注入的元素时，将运行来自**ActionLogFilterAttribute**自定义筛选器的方法**OnActionExecuting** 。</span><span class="sxs-lookup"><span data-stu-id="bf36c-192">The method **OnActionExecuting** from **ActionLogFilterAttribute** custom filter runs when an injected element is called.</span></span>

<span data-ttu-id="bf36c-193">还可以截获特定控制器方法。</span><span class="sxs-lookup"><span data-stu-id="bf36c-193">It is also possible to intercept a specific controller method.</span></span>

1. <span data-ttu-id="bf36c-194">在**MvcMusicStore\Controllers**中打开**StoreController** ，并添加对**筛选器**命名空间的引用：</span><span class="sxs-lookup"><span data-stu-id="bf36c-194">Open the **StoreController** at **MvcMusicStore\Controllers** and add a reference to the **Filters** namespace:</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample4.cs)]
2. <span data-ttu-id="bf36c-195">通过在类声明之前添加 **[CustomActionFilter]** 特性，将自定义筛选器**CustomActionFilter**注入到**StoreController**类中。</span><span class="sxs-lookup"><span data-stu-id="bf36c-195">Inject the custom filter **CustomActionFilter** into **StoreController** class by adding **[CustomActionFilter]** attribute before the class declaration.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample5.cs)]

   > [!NOTE]
   > <span data-ttu-id="bf36c-196">如果将筛选器注入控制器类中，则还会插入其所有操作。</span><span class="sxs-lookup"><span data-stu-id="bf36c-196">When a filter is injected into a controller class, all its actions are also injected.</span></span> <span data-ttu-id="bf36c-197">如果要仅对一组操作应用筛选器，则必须将 **[CustomActionFilter]** 注入到其中的每一个操作：</span><span class="sxs-lookup"><span data-stu-id="bf36c-197">If you would like to apply the filter only for a set of actions, you would have to inject **[CustomActionFilter]** to each one of them:</span></span>
   > 
   > [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample6.cs)]

<a id="Ex1Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a><span data-ttu-id="bf36c-198">任务 3-运行应用程序</span><span class="sxs-lookup"><span data-stu-id="bf36c-198">Task 3 - Running the Application</span></span>

<span data-ttu-id="bf36c-199">在此任务中，您将测试日志记录筛选器是否正常工作。</span><span class="sxs-lookup"><span data-stu-id="bf36c-199">In this task, you will test that the logging filter is working.</span></span> <span data-ttu-id="bf36c-200">您将启动该应用程序并访问应用商店，然后您将检查记录的活动。</span><span class="sxs-lookup"><span data-stu-id="bf36c-200">You will start the application and visit the store, and then you will check logged activities.</span></span>

1. <span data-ttu-id="bf36c-201">按 **F5** 运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="bf36c-201">Press **F5** to run the application.</span></span>
2. <span data-ttu-id="bf36c-202">浏览到 **/ActionLog**以查看日志视图初始状态：</span><span class="sxs-lookup"><span data-stu-id="bf36c-202">Browse to **/ActionLog** to see log view initial state:</span></span>

    <span data-ttu-id="bf36c-203">![页面活动之前的日志跟踪器状态](aspnet-mvc-4-custom-action-filters/_static/image3.png "页面活动之前的日志跟踪器状态")</span><span class="sxs-lookup"><span data-stu-id="bf36c-203">![Log tracker status before page activity](aspnet-mvc-4-custom-action-filters/_static/image3.png "Log tracker status before page activity")</span></span>

    <span data-ttu-id="bf36c-204">*页面活动之前的日志跟踪器状态*</span><span class="sxs-lookup"><span data-stu-id="bf36c-204">*Log tracker status before page activity*</span></span>

   > [!NOTE]
   > <span data-ttu-id="bf36c-205">默认情况下，它将始终显示检索菜单的现有流派时生成的一项。</span><span class="sxs-lookup"><span data-stu-id="bf36c-205">By default, it will always show one item that is generated when retrieving the existing genres for the menu.</span></span>
   > 
   > <span data-ttu-id="bf36c-206">为简单起见，我们将在每次运行应用程序时清理**ActionLog**表，因此它只显示每个特定任务验证的日志。</span><span class="sxs-lookup"><span data-stu-id="bf36c-206">For simplicity purposes we're cleaning up the **ActionLog** table each time the application runs so it will only show the logs of each particular task's verification.</span></span>
   > 
   > <span data-ttu-id="bf36c-207">你可能需要从会话中删除以下代码 **\_Start**方法（在**global.asax**类中），以便为在存储控制器中执行的所有操作保存历史日志。</span><span class="sxs-lookup"><span data-stu-id="bf36c-207">You might need to remove the following code from the **Session\_Start** method (in the **Global.asax** class), in order to save an historical log for all the actions executed within the Store Controller.</span></span>
   > 
   > [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample7.cs)]
3. <span data-ttu-id="bf36c-208">单击菜单中的某个**流派**，然后在其中执行一些操作，例如浏览可用的唱片集。</span><span class="sxs-lookup"><span data-stu-id="bf36c-208">Click one of the **Genres** from the menu and perform some actions there, like browsing an available album.</span></span>
4. <span data-ttu-id="bf36c-209">浏览到 **/ActionLog** ，如果日志为空，则按**F5**刷新页面。</span><span class="sxs-lookup"><span data-stu-id="bf36c-209">Browse to **/ActionLog** and if the log is empty press **F5** to refresh the page.</span></span> <span data-ttu-id="bf36c-210">检查是否跟踪了您的访问：</span><span class="sxs-lookup"><span data-stu-id="bf36c-210">Check that your visits were tracked:</span></span>

    <span data-ttu-id="bf36c-211">![已记录活动的操作日志](aspnet-mvc-4-custom-action-filters/_static/image4.png "已记录活动的操作日志")</span><span class="sxs-lookup"><span data-stu-id="bf36c-211">![Action log with activity logged](aspnet-mvc-4-custom-action-filters/_static/image4.png "Action log with activity logged")</span></span>

    <span data-ttu-id="bf36c-212">*已记录活动的操作日志*</span><span class="sxs-lookup"><span data-stu-id="bf36c-212">*Action log with activity logged*</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Managing_Multiple_Action_Filters"></a>
### <a name="exercise-2-managing-multiple-action-filters"></a><span data-ttu-id="bf36c-213">练习2：管理多个操作筛选器</span><span class="sxs-lookup"><span data-stu-id="bf36c-213">Exercise 2: Managing Multiple Action Filters</span></span>

<span data-ttu-id="bf36c-214">在本练习中，您将向 StoreController 类添加另一个自定义操作筛选器，并定义两个筛选器的执行顺序。</span><span class="sxs-lookup"><span data-stu-id="bf36c-214">In this exercise you will add a second Custom Action Filter to the StoreController class and define the specific order in which both filters will be executed.</span></span> <span data-ttu-id="bf36c-215">然后，您将更新代码以全局注册筛选器。</span><span class="sxs-lookup"><span data-stu-id="bf36c-215">Then you will update the code to register the filter Globally.</span></span>

<span data-ttu-id="bf36c-216">定义筛选器的执行顺序时，需要考虑不同的选项。</span><span class="sxs-lookup"><span data-stu-id="bf36c-216">There are different options to take into account when defining the Filters' execution order.</span></span> <span data-ttu-id="bf36c-217">例如，Order 属性和筛选器的作用域：</span><span class="sxs-lookup"><span data-stu-id="bf36c-217">For example, the Order property and the Filters' scope:</span></span>

<span data-ttu-id="bf36c-218">你可以为每个筛选器定义一个**范围**，例如，你可以将所有操作筛选器的范围限定为在**控制器范围**内运行，并将所有授权筛选器都指定为在**全局范围**内运行。</span><span class="sxs-lookup"><span data-stu-id="bf36c-218">You can define a **Scope** for each of the Filters, for example, you could scope all the Action Filters to run within the **Controller Scope**, and all Authorization Filters to run in **Global scope**.</span></span> <span data-ttu-id="bf36c-219">作用域具有定义的执行顺序。</span><span class="sxs-lookup"><span data-stu-id="bf36c-219">The scopes have a defined execution order.</span></span>

<span data-ttu-id="bf36c-220">此外，每个操作筛选器都具有 Order 属性，该属性用于确定筛选器范围内的执行顺序。</span><span class="sxs-lookup"><span data-stu-id="bf36c-220">Additionally, each action filter has an Order property which is used to determine the execution order in the scope of the filter.</span></span>

<span data-ttu-id="bf36c-221">有关自定义操作筛选器执行顺序的详细信息，请访问此 MSDN 文章：（[https://msdn.microsoft.com/library/dd381609(v=vs.98).aspx](https://msdn.microsoft.com/library/dd381609(v=vs.98).aspx)）。</span><span class="sxs-lookup"><span data-stu-id="bf36c-221">For more information about Custom Action Filters execution order, please visit this MSDN article: ([https://msdn.microsoft.com/library/dd381609(v=vs.98).aspx](https://msdn.microsoft.com/library/dd381609(v=vs.98).aspx)).</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_Creating_a_new_Custom_Action_Filter"></a>
#### <a name="task-1-creating-a-new-custom-action-filter"></a><span data-ttu-id="bf36c-222">任务1：创建新的自定义操作筛选器</span><span class="sxs-lookup"><span data-stu-id="bf36c-222">Task 1: Creating a new Custom Action Filter</span></span>

<span data-ttu-id="bf36c-223">在此任务中，您将创建一个新的自定义操作筛选器以注入到 StoreController 类中，了解如何管理筛选器的执行顺序。</span><span class="sxs-lookup"><span data-stu-id="bf36c-223">In this task, you will create a new Custom Action Filter to inject into the StoreController class, learning how to manage the execution order of the filters.</span></span>

1. <span data-ttu-id="bf36c-224">打开位于 **\Source\Ex02-ManagingMultipleActionFilters\Begin**文件夹的 "**开始**" 解决方案。</span><span class="sxs-lookup"><span data-stu-id="bf36c-224">Open the **Begin** solution located at **\Source\Ex02-ManagingMultipleActionFilters\Begin** folder.</span></span> <span data-ttu-id="bf36c-225">否则，你可以继续使用通过完成前一练习所获得的**最终**解决方案。</span><span class="sxs-lookup"><span data-stu-id="bf36c-225">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

    1. <span data-ttu-id="bf36c-226">如果你打开了提供的**开始**解决方案，则需要下载一些缺少的 NuGet 包，然后再继续。</span><span class="sxs-lookup"><span data-stu-id="bf36c-226">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="bf36c-227">为此，请单击 "**项目**" 菜单并选择 "**管理 NuGet 包**"。</span><span class="sxs-lookup"><span data-stu-id="bf36c-227">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
    2. <span data-ttu-id="bf36c-228">在 "**管理 NuGet 包**" 对话框中，单击 "**还原**" 以下载缺少的包。</span><span class="sxs-lookup"><span data-stu-id="bf36c-228">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
    3. <span data-ttu-id="bf36c-229">最后，通过单击 "**生成** | **生成解决方案**" 来生成解决方案。</span><span class="sxs-lookup"><span data-stu-id="bf36c-229">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

        > [!NOTE]
        > <span data-ttu-id="bf36c-230">使用 NuGet 的优点之一是，无需将所有库都送到项目中，从而减少了项目的大小。</span><span class="sxs-lookup"><span data-stu-id="bf36c-230">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="bf36c-231">使用 NuGet 功能，通过在包 .config 文件中指定包版本，你可以在首次运行项目时下载所有必需的库。</span><span class="sxs-lookup"><span data-stu-id="bf36c-231">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="bf36c-232">这就是在从此实验室打开现有解决方案之后需要运行这些步骤的原因。</span><span class="sxs-lookup"><span data-stu-id="bf36c-232">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
        > 
        > <span data-ttu-id="bf36c-233">有关详细信息，请参阅此文章： [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages)。</span><span class="sxs-lookup"><span data-stu-id="bf36c-233">For more information, see this article: [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages).</span></span>
2. <span data-ttu-id="bf36c-234">将新C#类添加到**Filters**文件夹，并将其命名为*MyNewCustomActionFilter.cs*</span><span class="sxs-lookup"><span data-stu-id="bf36c-234">Add a new C# class into the **Filters** folder and name it *MyNewCustomActionFilter.cs*</span></span>
3. <span data-ttu-id="bf36c-235">打开**MyNewCustomActionFilter.cs** ，并添加对**system.web**和**MvcMusicStore**命名空间的引用：</span><span class="sxs-lookup"><span data-stu-id="bf36c-235">Open **MyNewCustomActionFilter.cs** and add a reference to **System.Web.Mvc** and the **MvcMusicStore.Models** namespace:</span></span>

    <span data-ttu-id="bf36c-236">（代码段- *ASP.NET MVC 4 自定义操作筛选器-buildingappswithcachingservice-ex2-getproducts latency-cs-MyNewCustomActionFilterNamespaces*）</span><span class="sxs-lookup"><span data-stu-id="bf36c-236">(Code Snippet - *ASP.NET MVC 4 Custom Action Filters - Ex2-MyNewCustomActionFilterNamespaces*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample8.cs)]
4. <span data-ttu-id="bf36c-237">将默认类声明替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="bf36c-237">Replace the default class declaration with the following code.</span></span>

    <span data-ttu-id="bf36c-238">（代码段- *ASP.NET MVC 4 自定义操作筛选器-buildingappswithcachingservice-ex2-getproducts latency-cs-MyNewCustomActionFilterClass*）</span><span class="sxs-lookup"><span data-stu-id="bf36c-238">(Code Snippet - *ASP.NET MVC 4 Custom Action Filters - Ex2-MyNewCustomActionFilterClass*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample9.cs)]

    > [!NOTE]
    > <span data-ttu-id="bf36c-239">此自定义操作筛选器与您在上一练习中创建的筛选器几乎相同。</span><span class="sxs-lookup"><span data-stu-id="bf36c-239">This Custom Action Filter is almost the same than the one you created in the previous exercise.</span></span> <span data-ttu-id="bf36c-240">主要区别在于它具有使用此新类名称更新 *&quot;属性记录的&quot;* ，以标识注册了日志的筛选器。</span><span class="sxs-lookup"><span data-stu-id="bf36c-240">The main difference is that it has the *&quot;Logged By&quot;* attribute updated with this new class' name to identify which filter registered the log.</span></span>

<a id="Ex2Task2"></a>

<a id="Task_2_Injecting_a_new_Code_Interceptor_into_the_StoreController_Class"></a>
#### <a name="task-2-injecting-a-new-code-interceptor-into-the-storecontroller-class"></a><span data-ttu-id="bf36c-241">任务2：将新的代码侦听器注入到 StoreController 类</span><span class="sxs-lookup"><span data-stu-id="bf36c-241">Task 2: Injecting a new Code Interceptor into the StoreController Class</span></span>

<span data-ttu-id="bf36c-242">在此任务中，将新的自定义筛选器添加到 StoreController 类中，并运行解决方案来验证这两个筛选器如何协同工作。</span><span class="sxs-lookup"><span data-stu-id="bf36c-242">In this task, you will add a new custom filter into the StoreController Class and run the solution to verify how both filters work together.</span></span>

1. <span data-ttu-id="bf36c-243">打开位于**MvcMusicStore\Controllers**的**StoreController**类，并将新的自定义筛选器**MyNewCustomActionFilter**注入**StoreController**类，如下面的代码所示。</span><span class="sxs-lookup"><span data-stu-id="bf36c-243">Open the **StoreController** class located at **MvcMusicStore\Controllers** and inject the new custom filter **MyNewCustomActionFilter** into **StoreController** class like is shown in the following code.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample10.cs)]
2. <span data-ttu-id="bf36c-244">现在，运行应用程序，了解这两个自定义操作筛选器的工作原理。</span><span class="sxs-lookup"><span data-stu-id="bf36c-244">Now, run the application in order to see how these two Custom Action Filters work.</span></span> <span data-ttu-id="bf36c-245">为此，请按**F5**并等待，直到应用程序启动。</span><span class="sxs-lookup"><span data-stu-id="bf36c-245">To do this, press **F5** and wait until the application starts.</span></span>
3. <span data-ttu-id="bf36c-246">浏览到 **/ActionLog**以查看日志视图的初始状态。</span><span class="sxs-lookup"><span data-stu-id="bf36c-246">Browse to **/ActionLog** to see log view initial state.</span></span>

    <span data-ttu-id="bf36c-247">![页面活动之前的日志跟踪器状态](aspnet-mvc-4-custom-action-filters/_static/image5.png "页面活动之前的日志跟踪器状态")</span><span class="sxs-lookup"><span data-stu-id="bf36c-247">![Log tracker status before page activity](aspnet-mvc-4-custom-action-filters/_static/image5.png "Log tracker status before page activity")</span></span>

    <span data-ttu-id="bf36c-248">*页面活动之前的日志跟踪器状态*</span><span class="sxs-lookup"><span data-stu-id="bf36c-248">*Log tracker status before page activity*</span></span>
4. <span data-ttu-id="bf36c-249">单击菜单中的某个**流派**，然后在其中执行一些操作，例如浏览可用的唱片集。</span><span class="sxs-lookup"><span data-stu-id="bf36c-249">Click one of the **Genres** from the menu and perform some actions there, like browsing an available album.</span></span>
5. <span data-ttu-id="bf36c-250">检查此时间;您的访问被跟踪了两次：一次针对您在**StorageController**类中添加的每个自定义操作筛选器。</span><span class="sxs-lookup"><span data-stu-id="bf36c-250">Check that this time; your visits were tracked twice: once for each of the Custom Action Filters you added in the **StorageController** class.</span></span>

    <span data-ttu-id="bf36c-251">![已记录活动的操作日志](aspnet-mvc-4-custom-action-filters/_static/image6.png "已记录活动的操作日志")</span><span class="sxs-lookup"><span data-stu-id="bf36c-251">![Action log with activity logged](aspnet-mvc-4-custom-action-filters/_static/image6.png "Action log with activity logged")</span></span>

    <span data-ttu-id="bf36c-252">*已记录活动的操作日志*</span><span class="sxs-lookup"><span data-stu-id="bf36c-252">*Action log with activity logged*</span></span>
6. <span data-ttu-id="bf36c-253">关闭浏览器。</span><span class="sxs-lookup"><span data-stu-id="bf36c-253">Close the browser.</span></span>

<a id="Ex2Task3"></a>

<a id="Task_3_Managing_Filter_Ordering"></a>
#### <a name="task-3-managing-filter-ordering"></a><span data-ttu-id="bf36c-254">任务3：管理筛选器排序</span><span class="sxs-lookup"><span data-stu-id="bf36c-254">Task 3: Managing Filter Ordering</span></span>

<span data-ttu-id="bf36c-255">在此任务中，您将学习如何使用 Order 属性来管理筛选器的执行顺序。</span><span class="sxs-lookup"><span data-stu-id="bf36c-255">In this task, you will learn how to manage the filters' execution order by using the Order property.</span></span>

1. <span data-ttu-id="bf36c-256">打开位于**MvcMusicStore\Controllers**的**StoreController**类，并在这两个筛选器中指定**Order**属性，如下所示。</span><span class="sxs-lookup"><span data-stu-id="bf36c-256">Open the **StoreController** class located at **MvcMusicStore\Controllers** and specify the **Order** property in both filters like shown below.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample11.cs)]
2. <span data-ttu-id="bf36c-257">现在，请根据筛选器的 Order 属性值来验证执行筛选器的方式。</span><span class="sxs-lookup"><span data-stu-id="bf36c-257">Now, verify how the filters are executed depending on its Order property's value.</span></span> <span data-ttu-id="bf36c-258">你会发现具有最小顺序值（**CustomActionFilter**）的筛选器是执行的第一个筛选器。</span><span class="sxs-lookup"><span data-stu-id="bf36c-258">You will find that the filter with the smallest Order value (**CustomActionFilter**) is the first one that is executed.</span></span> <span data-ttu-id="bf36c-259">按**F5**并等待，直到应用程序启动。</span><span class="sxs-lookup"><span data-stu-id="bf36c-259">Press **F5** and wait until the application starts.</span></span>
3. <span data-ttu-id="bf36c-260">浏览到 **/ActionLog**以查看日志视图的初始状态。</span><span class="sxs-lookup"><span data-stu-id="bf36c-260">Browse to **/ActionLog** to see log view initial state.</span></span>

    <span data-ttu-id="bf36c-261">![页面活动之前的日志跟踪器状态](aspnet-mvc-4-custom-action-filters/_static/image7.png "页面活动之前的日志跟踪器状态")</span><span class="sxs-lookup"><span data-stu-id="bf36c-261">![Log tracker status before page activity](aspnet-mvc-4-custom-action-filters/_static/image7.png "Log tracker status before page activity")</span></span>

    <span data-ttu-id="bf36c-262">*页面活动之前的日志跟踪器状态*</span><span class="sxs-lookup"><span data-stu-id="bf36c-262">*Log tracker status before page activity*</span></span>
4. <span data-ttu-id="bf36c-263">单击菜单中的某个**流派**，然后在其中执行一些操作，例如浏览可用的唱片集。</span><span class="sxs-lookup"><span data-stu-id="bf36c-263">Click one of the **Genres** from the menu and perform some actions there, like browsing an available album.</span></span>
5. <span data-ttu-id="bf36c-264">检查这一次是否跟踪了你的访问是否按筛选器的订单值： **CustomActionFilter** logs ' 排序。</span><span class="sxs-lookup"><span data-stu-id="bf36c-264">Check that this time, your visits were tracked ordered by the filters' Order value: **CustomActionFilter** logs' first.</span></span>

    <span data-ttu-id="bf36c-265">![已记录活动的操作日志](aspnet-mvc-4-custom-action-filters/_static/image8.png "已记录活动的操作日志")</span><span class="sxs-lookup"><span data-stu-id="bf36c-265">![Action log with activity logged](aspnet-mvc-4-custom-action-filters/_static/image8.png "Action log with activity logged")</span></span>

    <span data-ttu-id="bf36c-266">*已记录活动的操作日志*</span><span class="sxs-lookup"><span data-stu-id="bf36c-266">*Action log with activity logged*</span></span>
6. <span data-ttu-id="bf36c-267">现在，您将更新筛选器的 order 值，并验证日志记录顺序如何变化。</span><span class="sxs-lookup"><span data-stu-id="bf36c-267">Now, you will update the Filters' order value and verify how the logging order changes.</span></span> <span data-ttu-id="bf36c-268">在**StoreController**类中，更新筛选器的 Order 值，如下所示。</span><span class="sxs-lookup"><span data-stu-id="bf36c-268">In the **StoreController** class, update the Filters' Order value like shown below.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample12.cs)]
7. <span data-ttu-id="bf36c-269">按**F5**再次运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="bf36c-269">Run the application again by pressing **F5**.</span></span>
8. <span data-ttu-id="bf36c-270">单击菜单中的某个**流派**，然后在其中执行一些操作，例如浏览可用的唱片集。</span><span class="sxs-lookup"><span data-stu-id="bf36c-270">Click one of the **Genres** from the menu and perform some actions there, like browsing an available album.</span></span>
9. <span data-ttu-id="bf36c-271">检查这一次， **MyNewCustomActionFilter**筛选器创建的日志会首先出现。</span><span class="sxs-lookup"><span data-stu-id="bf36c-271">Check that this time, the logs created by **MyNewCustomActionFilter** filter appears first.</span></span>

    <span data-ttu-id="bf36c-272">![已记录活动的操作日志](aspnet-mvc-4-custom-action-filters/_static/image9.png "已记录活动的操作日志")</span><span class="sxs-lookup"><span data-stu-id="bf36c-272">![Action log with activity logged](aspnet-mvc-4-custom-action-filters/_static/image9.png "Action log with activity logged")</span></span>

    <span data-ttu-id="bf36c-273">*已记录活动的操作日志*</span><span class="sxs-lookup"><span data-stu-id="bf36c-273">*Action log with activity logged*</span></span>

<a id="Ex2Task4"></a>

<a id="Task_4_Registering_Filters_Globally"></a>
#### <a name="task-4-registering-filters-globally"></a><span data-ttu-id="bf36c-274">任务4：全局注册筛选器</span><span class="sxs-lookup"><span data-stu-id="bf36c-274">Task 4: Registering Filters Globally</span></span>

<span data-ttu-id="bf36c-275">在此任务中，你将更新解决方案，以将新筛选器（**MyNewCustomActionFilter**）注册为全局筛选器。</span><span class="sxs-lookup"><span data-stu-id="bf36c-275">In this task, you will update the solution to register the new filter (**MyNewCustomActionFilter**) as a global filter.</span></span> <span data-ttu-id="bf36c-276">执行此操作后，在应用程序中执行的所有操作都将触发应用程序中执行的所有操作，而不仅是在上一个任务中的 StoreController 中执行。</span><span class="sxs-lookup"><span data-stu-id="bf36c-276">By doing this, it will be triggered by all the actions performed in the application and not only in the StoreController ones as in the previous task.</span></span>

1. <span data-ttu-id="bf36c-277">在**StoreController**类中，删除 [ **MyNewCustomActionFilter]** 属性和 **[CustomActionFilter]** 中的 order 属性。</span><span class="sxs-lookup"><span data-stu-id="bf36c-277">In **StoreController** class, remove **[MyNewCustomActionFilter]** attribute and the order property from **[CustomActionFilter]**.</span></span> <span data-ttu-id="bf36c-278">该元素应类似于：</span><span class="sxs-lookup"><span data-stu-id="bf36c-278">It should look like the following:</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample13.cs)]
2. <span data-ttu-id="bf36c-279">打开**global.asax**文件，并找到**应用程序\_Start**方法。</span><span class="sxs-lookup"><span data-stu-id="bf36c-279">Open **Global.asax** file and locate the **Application\_Start** method.</span></span> <span data-ttu-id="bf36c-280">请注意，每次应用程序启动时，都是通过调用**filterconfig.math**类中的**RegisterGlobalFilters**方法来注册全局筛选器。</span><span class="sxs-lookup"><span data-stu-id="bf36c-280">Notice that each time the application starts it is registering the global filters by calling **RegisterGlobalFilters** method within **FilterConfig** class.</span></span>

    <span data-ttu-id="bf36c-281">![在 global.asax 中注册全局筛选器](aspnet-mvc-4-custom-action-filters/_static/image10.png "在 global.asax 中注册全局筛选器")</span><span class="sxs-lookup"><span data-stu-id="bf36c-281">![Registering Global Filters in Global.asax](aspnet-mvc-4-custom-action-filters/_static/image10.png "Registering Global Filters in Global.asax")</span></span>

    <span data-ttu-id="bf36c-282">*在 global.asax 中注册全局筛选器*</span><span class="sxs-lookup"><span data-stu-id="bf36c-282">*Registering Global Filters in Global.asax*</span></span>
3. <span data-ttu-id="bf36c-283">在**应用\_启动**文件夹内打开**FilterConfig.cs**文件。</span><span class="sxs-lookup"><span data-stu-id="bf36c-283">Open **FilterConfig.cs** file within **App\_Start** folder.</span></span>
4. <span data-ttu-id="bf36c-284">使用 System.web 添加对的引用;使用 MvcMusicStore;名称.</span><span class="sxs-lookup"><span data-stu-id="bf36c-284">Add a reference to using System.Web.Mvc; using MvcMusicStore.Filters; namespace.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample14.cs)]
5. <span data-ttu-id="bf36c-285">Update **RegisterGlobalFilters**方法添加您的自定义筛选器。</span><span class="sxs-lookup"><span data-stu-id="bf36c-285">Update **RegisterGlobalFilters** method adding your custom filter.</span></span> <span data-ttu-id="bf36c-286">为此，请添加突出显示的代码：</span><span class="sxs-lookup"><span data-stu-id="bf36c-286">To do this, add the highlighted code:</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample15.cs)]
6. <span data-ttu-id="bf36c-287">按 F5 运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="bf36c-287">Run the application by pressing **F5**.</span></span>
7. <span data-ttu-id="bf36c-288">单击菜单中的某个**流派**，然后在其中执行一些操作，例如浏览可用的唱片集。</span><span class="sxs-lookup"><span data-stu-id="bf36c-288">Click one of the **Genres** from the menu and perform some actions there, like browsing an available album.</span></span>
8. <span data-ttu-id="bf36c-289">检查现在 **[MyNewCustomActionFilter]** 是否在 HomeController 和 ActionLogController 中注入。</span><span class="sxs-lookup"><span data-stu-id="bf36c-289">Check that now **[MyNewCustomActionFilter]** is being injected in HomeController and ActionLogController too.</span></span>

    <span data-ttu-id="bf36c-290">![已记录活动的操作日志](aspnet-mvc-4-custom-action-filters/_static/image11.png "已记录活动的操作日志")</span><span class="sxs-lookup"><span data-stu-id="bf36c-290">![Action log with activity logged](aspnet-mvc-4-custom-action-filters/_static/image11.png "Action log with activity logged")</span></span>

    <span data-ttu-id="bf36c-291">*已记录全局活动的操作日志*</span><span class="sxs-lookup"><span data-stu-id="bf36c-291">*Action log with global activity logged*</span></span>

> [!NOTE]
> <span data-ttu-id="bf36c-292">此外，还可以在[附录 B：使用 Web 部署发布 ASP.NET MVC 4 应用程序的](#AppendixB)Microsoft Azure 网站上部署此应用程序。</span><span class="sxs-lookup"><span data-stu-id="bf36c-292">Additionally, you can deploy this application to Windows Azure Web Sites following [Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy](#AppendixB).</span></span>

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="bf36c-293">摘要</span><span class="sxs-lookup"><span data-stu-id="bf36c-293">Summary</span></span>

<span data-ttu-id="bf36c-294">完成此动手实验后，你已了解如何扩展操作筛选器以执行自定义操作。</span><span class="sxs-lookup"><span data-stu-id="bf36c-294">By completing this Hands-On Lab you have learned how to extend an action filter to execute custom actions.</span></span> <span data-ttu-id="bf36c-295">还了解了如何将任何筛选器注入到页面控制器。</span><span class="sxs-lookup"><span data-stu-id="bf36c-295">You have also learned how to inject any filter to your page controllers.</span></span> <span data-ttu-id="bf36c-296">使用了以下概念：</span><span class="sxs-lookup"><span data-stu-id="bf36c-296">The following concepts were used:</span></span>

- <span data-ttu-id="bf36c-297">如何通过 ASP.NET MVC ActionFilterAttribute 类创建自定义操作筛选器</span><span class="sxs-lookup"><span data-stu-id="bf36c-297">How to create Custom Action filters with the ASP.NET MVC ActionFilterAttribute class</span></span>
- <span data-ttu-id="bf36c-298">如何将筛选器注入 ASP.NET MVC 控制器</span><span class="sxs-lookup"><span data-stu-id="bf36c-298">How to inject filters into ASP.NET MVC controllers</span></span>
- <span data-ttu-id="bf36c-299">如何使用 Order 属性管理筛选排序</span><span class="sxs-lookup"><span data-stu-id="bf36c-299">How to manage filter ordering using the Order property</span></span>
- <span data-ttu-id="bf36c-300">如何全局注册筛选器</span><span class="sxs-lookup"><span data-stu-id="bf36c-300">How to register filters globally</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="bf36c-301">附录 A：安装 Visual Studio Express 2012 for Web</span><span class="sxs-lookup"><span data-stu-id="bf36c-301">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="bf36c-302">您可以使用 **[Microsoft Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)** 为 Web 或其他 &quot;Express&quot; 版本安装**Microsoft Visual Studio Express 2012** 。</span><span class="sxs-lookup"><span data-stu-id="bf36c-302">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="bf36c-303">以下说明将指导你完成使用*Microsoft Web 平台安装程序*安装*Visual studio Express 2012 for Web*的步骤。</span><span class="sxs-lookup"><span data-stu-id="bf36c-303">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="bf36c-304">转到 [https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)。</span><span class="sxs-lookup"><span data-stu-id="bf36c-304">Go to [https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="bf36c-305">或者，如果你已经安装了 Web 平台安装程序，则可以打开它并<em>使用 Windows AZURE SDK&quot;搜索 Visual Studio Express 2012 For Web</em>的产品 &quot;。</span><span class="sxs-lookup"><span data-stu-id="bf36c-305">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Windows Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="bf36c-306">单击 "**立即安装**"。</span><span class="sxs-lookup"><span data-stu-id="bf36c-306">Click on **Install Now**.</span></span> <span data-ttu-id="bf36c-307">如果你没有**Web 平台安装程序**，则会重定向到 "下载并安装"。</span><span class="sxs-lookup"><span data-stu-id="bf36c-307">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="bf36c-308">**Web 平台安装程序**打开后，单击 "**安装**" 以启动安装程序。</span><span class="sxs-lookup"><span data-stu-id="bf36c-308">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="bf36c-309">![安装 Visual Studio Express](aspnet-mvc-4-custom-action-filters/_static/image12.png "安装 Visual Studio Express")</span><span class="sxs-lookup"><span data-stu-id="bf36c-309">![Install Visual Studio Express](aspnet-mvc-4-custom-action-filters/_static/image12.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="bf36c-310">*安装 Visual Studio Express*</span><span class="sxs-lookup"><span data-stu-id="bf36c-310">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="bf36c-311">阅读所有产品的许可证和条款，单击 "**我接受**" 以继续。</span><span class="sxs-lookup"><span data-stu-id="bf36c-311">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![接受许可条款](aspnet-mvc-4-custom-action-filters/_static/image13.png)

    <span data-ttu-id="bf36c-313">*接受许可条款*</span><span class="sxs-lookup"><span data-stu-id="bf36c-313">*Accepting the license terms*</span></span>
5. <span data-ttu-id="bf36c-314">等待下载和安装过程完成。</span><span class="sxs-lookup"><span data-stu-id="bf36c-314">Wait until the downloading and installation process completes.</span></span>

    ![安装进度](aspnet-mvc-4-custom-action-filters/_static/image14.png)

    <span data-ttu-id="bf36c-316">*安装进度*</span><span class="sxs-lookup"><span data-stu-id="bf36c-316">*Installation progress*</span></span>
6. <span data-ttu-id="bf36c-317">安装完成后，单击 "**完成**"。</span><span class="sxs-lookup"><span data-stu-id="bf36c-317">When the installation completes, click **Finish**.</span></span>

    ![安装完成](aspnet-mvc-4-custom-action-filters/_static/image15.png)

    <span data-ttu-id="bf36c-319">*安装完成*</span><span class="sxs-lookup"><span data-stu-id="bf36c-319">*Installation completed*</span></span>
7. <span data-ttu-id="bf36c-320">单击 "**退出**" 以关闭 Web 平台安装程序。</span><span class="sxs-lookup"><span data-stu-id="bf36c-320">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="bf36c-321">若要打开 Web Visual Studio Express，请在 "**开始**" 屏幕上，开始书写 &quot;**VS Express**&quot;，然后单击 " **VS Express for Web** " 磁贴。</span><span class="sxs-lookup"><span data-stu-id="bf36c-321">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![VS Express for Web 磁贴](aspnet-mvc-4-custom-action-filters/_static/image16.png)

    <span data-ttu-id="bf36c-323">*VS Express for Web 磁贴*</span><span class="sxs-lookup"><span data-stu-id="bf36c-323">*VS Express for Web tile*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-b-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="bf36c-324">附录 B：使用 Web 部署发布 ASP.NET MVC 4 应用程序</span><span class="sxs-lookup"><span data-stu-id="bf36c-324">Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

<span data-ttu-id="bf36c-325">本附录将演示如何从 Windows Azure 管理门户创建新的网站，以及如何利用 Microsoft Azure 提供的 Web 部署发布功能，发布通过实验室获取的应用程序。</span><span class="sxs-lookup"><span data-stu-id="bf36c-325">This appendix will show you how to create a new web site from the Windows Azure Management Portal and publish the application you obtained by following the lab, taking advantage of the Web Deploy publishing feature provided by Windows Azure.</span></span>

<a id="ApxBTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a><span data-ttu-id="bf36c-326">任务 1-从 Microsoft Azure 门户创建新网站</span><span class="sxs-lookup"><span data-stu-id="bf36c-326">Task 1 - Creating a New Web Site from the Windows Azure Portal</span></span>

1. <span data-ttu-id="bf36c-327">请使用[Windows Azure 管理门户](https://manage.windowsazure.com/)，并使用与你的订阅关联的 Microsoft 凭据登录。</span><span class="sxs-lookup"><span data-stu-id="bf36c-327">Go to the [Windows Azure Management Portal](https://manage.windowsazure.com/) and sign in using the Microsoft credentials associated with your subscription.</span></span>

    > [!NOTE]
    > <span data-ttu-id="bf36c-328">借助 Windows Azure，你可以免费托管10个 ASP.NET 的网站，然后随着流量的增长进行扩展。</span><span class="sxs-lookup"><span data-stu-id="bf36c-328">With Windows Azure you can host 10 ASP.NET Web Sites for free and then scale as your traffic grows.</span></span> <span data-ttu-id="bf36c-329">你可以在[此处](https://aka.ms/aspnet-hol-azure)注册。</span><span class="sxs-lookup"><span data-stu-id="bf36c-329">You can sign up [here](https://aka.ms/aspnet-hol-azure).</span></span>

    <span data-ttu-id="bf36c-330">![登录到 Windows Azure 门户](aspnet-mvc-4-custom-action-filters/_static/image17.png "登录到 Microsoft Azure 门户")</span><span class="sxs-lookup"><span data-stu-id="bf36c-330">![Log on to Windows Azure portal](aspnet-mvc-4-custom-action-filters/_static/image17.png "Log on to Windows Azure portal")</span></span>

    <span data-ttu-id="bf36c-331">*登录到 Windows Azure 管理门户*</span><span class="sxs-lookup"><span data-stu-id="bf36c-331">*Log on to Windows Azure Management Portal*</span></span>
2. <span data-ttu-id="bf36c-332">单击命令栏上的 "**新建**"。</span><span class="sxs-lookup"><span data-stu-id="bf36c-332">Click **New** on the command bar.</span></span>

    <span data-ttu-id="bf36c-333">![创建新网站](aspnet-mvc-4-custom-action-filters/_static/image18.png "创建新网站")</span><span class="sxs-lookup"><span data-stu-id="bf36c-333">![Creating a new Web Site](aspnet-mvc-4-custom-action-filters/_static/image18.png "Creating a new Web Site")</span></span>

    <span data-ttu-id="bf36c-334">*创建新网站*</span><span class="sxs-lookup"><span data-stu-id="bf36c-334">*Creating a new Web Site*</span></span>
3. <span data-ttu-id="bf36c-335">单击 "**计算** | **网站**"。</span><span class="sxs-lookup"><span data-stu-id="bf36c-335">Click **Compute** | **Web Site**.</span></span> <span data-ttu-id="bf36c-336">然后选择 "**快速创建**" 选项。</span><span class="sxs-lookup"><span data-stu-id="bf36c-336">Then select **Quick Create** option.</span></span> <span data-ttu-id="bf36c-337">为新网站提供可用 URL，并单击 "**创建**网站"。</span><span class="sxs-lookup"><span data-stu-id="bf36c-337">Provide an available URL for the new web site and click **Create Web Site**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="bf36c-338">Windows Azure 网站是在云中运行的 Web 应用程序的宿主，你可以控制和管理这些应用程序。</span><span class="sxs-lookup"><span data-stu-id="bf36c-338">A Windows Azure Web Site is the host for a web application running in the cloud that you can control and manage.</span></span> <span data-ttu-id="bf36c-339">使用 "快速创建" 选项，可以从门户外部将已完成的 web 应用程序部署到 Microsoft Azure 网站。</span><span class="sxs-lookup"><span data-stu-id="bf36c-339">The Quick Create option allows you to deploy a completed web application to the Windows Azure Web Site from outside the portal.</span></span> <span data-ttu-id="bf36c-340">它不包括设置数据库的步骤。</span><span class="sxs-lookup"><span data-stu-id="bf36c-340">It does not include steps for setting up a database.</span></span>

    <span data-ttu-id="bf36c-341">![使用 "快速创建" 创建新网站](aspnet-mvc-4-custom-action-filters/_static/image19.png "使用“快速创建”创建新网站")</span><span class="sxs-lookup"><span data-stu-id="bf36c-341">![Creating a new Web Site using Quick Create](aspnet-mvc-4-custom-action-filters/_static/image19.png "Creating a new Web Site using Quick Create")</span></span>

    <span data-ttu-id="bf36c-342">*使用 "快速创建" 创建新网站*</span><span class="sxs-lookup"><span data-stu-id="bf36c-342">*Creating a new Web Site using Quick Create*</span></span>
4. <span data-ttu-id="bf36c-343">请**等到新网站创建完毕。**</span><span class="sxs-lookup"><span data-stu-id="bf36c-343">Wait until the new **Web Site** is created.</span></span>
5. <span data-ttu-id="bf36c-344">创建网站后，单击 " **URL** " 列下的链接。</span><span class="sxs-lookup"><span data-stu-id="bf36c-344">Once the Web Site is created click the link under the **URL** column.</span></span> <span data-ttu-id="bf36c-345">检查新网站是否正常工作。</span><span class="sxs-lookup"><span data-stu-id="bf36c-345">Check that the new Web Site is working.</span></span>

    <span data-ttu-id="bf36c-346">![浏览到新网站](aspnet-mvc-4-custom-action-filters/_static/image20.png "浏览到新网站")</span><span class="sxs-lookup"><span data-stu-id="bf36c-346">![Browsing to the new web site](aspnet-mvc-4-custom-action-filters/_static/image20.png "Browsing to the new web site")</span></span>

    <span data-ttu-id="bf36c-347">*浏览到新网站*</span><span class="sxs-lookup"><span data-stu-id="bf36c-347">*Browsing to the new web site*</span></span>

    <span data-ttu-id="bf36c-348">![网站正在运行](aspnet-mvc-4-custom-action-filters/_static/image21.png "网站正在运行")</span><span class="sxs-lookup"><span data-stu-id="bf36c-348">![Web site running](aspnet-mvc-4-custom-action-filters/_static/image21.png "Web site running")</span></span>

    <span data-ttu-id="bf36c-349">*网站正在运行*</span><span class="sxs-lookup"><span data-stu-id="bf36c-349">*Web site running*</span></span>
6. <span data-ttu-id="bf36c-350">返回到门户，并在 "**名称**" 列下单击网站的名称以显示管理页面。</span><span class="sxs-lookup"><span data-stu-id="bf36c-350">Go back to the portal and click the name of the web site under the **Name** column to display the management pages.</span></span>

    <span data-ttu-id="bf36c-351">![打开网站管理页](aspnet-mvc-4-custom-action-filters/_static/image22.png "打开网站管理页")</span><span class="sxs-lookup"><span data-stu-id="bf36c-351">![Opening the web site management pages](aspnet-mvc-4-custom-action-filters/_static/image22.png "Opening the web site management pages")</span></span>

    <span data-ttu-id="bf36c-352">*打开网站管理页*</span><span class="sxs-lookup"><span data-stu-id="bf36c-352">*Opening the Web Site management pages*</span></span>
7. <span data-ttu-id="bf36c-353">在 "**仪表板**" 页的 "**速览**" 部分下，单击 "**下载发布配置文件**" 链接。</span><span class="sxs-lookup"><span data-stu-id="bf36c-353">In the **Dashboard** page, under the **quick glance** section, click the **Download publish profile** link.</span></span>

    > [!NOTE]
    > <span data-ttu-id="bf36c-354">*发布配置文件*包含为每个已启用的发布方法将 web 应用程序发布到 microsoft Azure 网站所需的所有信息。</span><span class="sxs-lookup"><span data-stu-id="bf36c-354">The *publish profile* contains all of the information required to publish a web application to a Windows Azure website for each enabled publication method.</span></span> <span data-ttu-id="bf36c-355">发布配置文件包含有连接到并且验证该发布方法启用的每个端点所需的 URL、用户凭据和数据库字符串。</span><span class="sxs-lookup"><span data-stu-id="bf36c-355">The publish profile contains the URLs, user credentials and database strings required to connect to and authenticate against each of the endpoints for which a publication method is enabled.</span></span> <span data-ttu-id="bf36c-356">**Microsoft WebMatrix 2**、 **Microsoft Visual Studio Express for Web**和**Microsoft Visual Studio 2012**支持读取发布配置文件，以便自动配置这些程序以将 Web 应用程序发布到 microsoft Azure 网站。</span><span class="sxs-lookup"><span data-stu-id="bf36c-356">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** and **Microsoft Visual Studio 2012** support reading publish profiles to automate configuration of these programs for publishing web applications to Windows Azure websites.</span></span>

    <span data-ttu-id="bf36c-357">![下载网站发布配置文件](aspnet-mvc-4-custom-action-filters/_static/image23.png "下载网站发布配置文件")</span><span class="sxs-lookup"><span data-stu-id="bf36c-357">![Downloading the web site publish profile](aspnet-mvc-4-custom-action-filters/_static/image23.png "Downloading the web site publish profile")</span></span>

    <span data-ttu-id="bf36c-358">*下载网站发布配置文件*</span><span class="sxs-lookup"><span data-stu-id="bf36c-358">*Downloading the Web Site publish profile*</span></span>
8. <span data-ttu-id="bf36c-359">将发布配置文件下载到已知位置。</span><span class="sxs-lookup"><span data-stu-id="bf36c-359">Download the publish profile file to a known location.</span></span> <span data-ttu-id="bf36c-360">在本练习中，您将了解如何使用此文件从 Visual Studio 将 web 应用程序发布到 Microsoft Azure 网站。</span><span class="sxs-lookup"><span data-stu-id="bf36c-360">Further in this exercise you will see how to use this file to publish a web application to a Windows Azure Web Sites from Visual Studio.</span></span>

    <span data-ttu-id="bf36c-361">![正在保存发布配置文件](aspnet-mvc-4-custom-action-filters/_static/image24.png "正在保存发布配置文件")</span><span class="sxs-lookup"><span data-stu-id="bf36c-361">![Saving the publish profile file](aspnet-mvc-4-custom-action-filters/_static/image24.png "Saving the publish profile")</span></span>

    <span data-ttu-id="bf36c-362">*正在保存发布配置文件*</span><span class="sxs-lookup"><span data-stu-id="bf36c-362">*Saving the publish profile file*</span></span>

<a id="ApxBTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a><span data-ttu-id="bf36c-363">任务 2-配置数据库服务器</span><span class="sxs-lookup"><span data-stu-id="bf36c-363">Task 2 - Configuring the Database Server</span></span>

<span data-ttu-id="bf36c-364">如果应用程序使用 SQL Server 数据库，则需要创建 SQL 数据库服务器。</span><span class="sxs-lookup"><span data-stu-id="bf36c-364">If your application makes use of SQL Server databases you will need to create a SQL Database server.</span></span> <span data-ttu-id="bf36c-365">如果要部署不使用 SQL Server 的简单应用程序，则可以跳过此任务。</span><span class="sxs-lookup"><span data-stu-id="bf36c-365">If you want to deploy a simple application that does not use SQL Server you might skip this task.</span></span>

1. <span data-ttu-id="bf36c-366">你将需要一个用于存储应用程序数据库的 SQL 数据库服务器。</span><span class="sxs-lookup"><span data-stu-id="bf36c-366">You will need a SQL Database server for storing the application database.</span></span> <span data-ttu-id="bf36c-367">可以在 Microsoft Azure 管理门户中的**sql** **数据库 | server** | **服务器的仪表板**上的 MICROSOFT Azure 管理门户中查看 sql 数据库服务器。</span><span class="sxs-lookup"><span data-stu-id="bf36c-367">You can view the SQL Database servers from your subscription in the Windows Azure Management portal at **Sql Databases** | **Servers** | **Server's Dashboard**.</span></span> <span data-ttu-id="bf36c-368">如果尚未创建服务器，可以使用命令栏上的 "**添加**" 按钮创建一个服务器。</span><span class="sxs-lookup"><span data-stu-id="bf36c-368">If you do not have a server created, you can create one using the **Add** button on the command bar.</span></span> <span data-ttu-id="bf36c-369">记下**服务器名称和 URL、管理员登录名和密码**，因为你将在后续任务中使用它们。</span><span class="sxs-lookup"><span data-stu-id="bf36c-369">Take note of the **server name and URL, administrator login name and password**, as you will use them in the next tasks.</span></span> <span data-ttu-id="bf36c-370">请不要创建数据库，因为它将在后面的阶段创建。</span><span class="sxs-lookup"><span data-stu-id="bf36c-370">Do not create the database yet, as it will be created in a later stage.</span></span>

    <span data-ttu-id="bf36c-371">![SQL 数据库服务器仪表板](aspnet-mvc-4-custom-action-filters/_static/image25.png "SQL 数据库服务器仪表板")</span><span class="sxs-lookup"><span data-stu-id="bf36c-371">![SQL Database Server Dashboard](aspnet-mvc-4-custom-action-filters/_static/image25.png "SQL Database Server Dashboard")</span></span>

    <span data-ttu-id="bf36c-372">*SQL 数据库服务器仪表板*</span><span class="sxs-lookup"><span data-stu-id="bf36c-372">*SQL Database Server Dashboard*</span></span>
2. <span data-ttu-id="bf36c-373">在下一任务中，您将从 Visual Studio 测试数据库连接，因此，需要在服务器的**允许 IP 地址**列表中包含本地 ip 地址。</span><span class="sxs-lookup"><span data-stu-id="bf36c-373">In the next task you will test the database connection from Visual Studio, for that reason you need to include your local IP address in the server's list of **Allowed IP Addresses**.</span></span> <span data-ttu-id="bf36c-374">为此，请单击 "**配置**"，从 "**当前客户端 IP 地址**" 中选择 IP 地址，并将其粘贴到 "**起始 Ip 地址**" 和 "**结束 ip 地址**" 文本框，然后单击 "![添加-客户端-IP 地址-](aspnet-mvc-4-custom-action-filters/_static/image26.png)" 按钮。</span><span class="sxs-lookup"><span data-stu-id="bf36c-374">To do that, click **Configure**, select the IP address from **Current Client IP Address** and paste it on the **Start IP Address** and **End IP Address** text boxes and click the ![add-client-ip-address-ok-button](aspnet-mvc-4-custom-action-filters/_static/image26.png) button.</span></span>

    ![添加客户端 IP 地址](aspnet-mvc-4-custom-action-filters/_static/image27.png)

    <span data-ttu-id="bf36c-376">*添加客户端 IP 地址*</span><span class="sxs-lookup"><span data-stu-id="bf36c-376">*Adding Client IP Address*</span></span>
3. <span data-ttu-id="bf36c-377">将**客户端 Ip 地址**添加到 "允许的 IP 地址" 列表中后，单击 "**保存**" 以确认更改。</span><span class="sxs-lookup"><span data-stu-id="bf36c-377">Once the **Client IP Address** is added to the allowed IP addresses list, click on **Save** to confirm the changes.</span></span>

    ![确认更改](aspnet-mvc-4-custom-action-filters/_static/image28.png)

    <span data-ttu-id="bf36c-379">*确认更改*</span><span class="sxs-lookup"><span data-stu-id="bf36c-379">*Confirm Changes*</span></span>

<a id="ApxBTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="bf36c-380">任务 3-使用 Web 部署发布 ASP.NET MVC 4 应用程序</span><span class="sxs-lookup"><span data-stu-id="bf36c-380">Task 3 - Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

1. <span data-ttu-id="bf36c-381">返回到 ASP.NET MVC 4 解决方案。</span><span class="sxs-lookup"><span data-stu-id="bf36c-381">Go back to the ASP.NET MVC 4 solution.</span></span> <span data-ttu-id="bf36c-382">在**解决方案资源管理器**中，右键单击网站项目，然后选择 "**发布**"。</span><span class="sxs-lookup"><span data-stu-id="bf36c-382">In the **Solution Explorer**, right-click the web site project and select **Publish**.</span></span>

    <span data-ttu-id="bf36c-383">![发布应用程序](aspnet-mvc-4-custom-action-filters/_static/image29.png "发布应用程序")</span><span class="sxs-lookup"><span data-stu-id="bf36c-383">![Publishing the Application](aspnet-mvc-4-custom-action-filters/_static/image29.png "Publishing the Application")</span></span>

    <span data-ttu-id="bf36c-384">*发布网站*</span><span class="sxs-lookup"><span data-stu-id="bf36c-384">*Publishing the web site*</span></span>
2. <span data-ttu-id="bf36c-385">导入您在第一个任务中保存的发布配置文件。</span><span class="sxs-lookup"><span data-stu-id="bf36c-385">Import the publish profile you saved in the first task.</span></span>

    <span data-ttu-id="bf36c-386">![导入发布配置文件](aspnet-mvc-4-custom-action-filters/_static/image30.png "导入发布配置文件")</span><span class="sxs-lookup"><span data-stu-id="bf36c-386">![Importing the publish profile](aspnet-mvc-4-custom-action-filters/_static/image30.png "Importing the publish profile")</span></span>

    <span data-ttu-id="bf36c-387">*导入发布配置文件*</span><span class="sxs-lookup"><span data-stu-id="bf36c-387">*Importing publish profile*</span></span>
3. <span data-ttu-id="bf36c-388">单击 "**验证连接**"。</span><span class="sxs-lookup"><span data-stu-id="bf36c-388">Click **Validate Connection**.</span></span> <span data-ttu-id="bf36c-389">验证完成后，单击 "**下一步**"。</span><span class="sxs-lookup"><span data-stu-id="bf36c-389">Once Validation is complete click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="bf36c-390">验证完成后，"验证连接" 按钮旁边会出现一个绿色的复选标记。</span><span class="sxs-lookup"><span data-stu-id="bf36c-390">Validation is complete once you see a green checkmark appear next to the Validate Connection button.</span></span>

    <span data-ttu-id="bf36c-391">![正在验证连接](aspnet-mvc-4-custom-action-filters/_static/image31.png "正在验证连接")</span><span class="sxs-lookup"><span data-stu-id="bf36c-391">![Validating connection](aspnet-mvc-4-custom-action-filters/_static/image31.png "Validating connection")</span></span>

    <span data-ttu-id="bf36c-392">*正在验证连接*</span><span class="sxs-lookup"><span data-stu-id="bf36c-392">*Validating connection*</span></span>
4. <span data-ttu-id="bf36c-393">在 "**设置**" 页的 "**数据库**" 部分下，单击数据库连接的文本框旁边的按钮（即**DefaultConnection**）。</span><span class="sxs-lookup"><span data-stu-id="bf36c-393">In the **Settings** page, under the **Databases** section, click the button next to your database connection's textbox (i.e. **DefaultConnection**).</span></span>

    <span data-ttu-id="bf36c-394">![Web 部署配置](aspnet-mvc-4-custom-action-filters/_static/image32.png "Web 部署配置")</span><span class="sxs-lookup"><span data-stu-id="bf36c-394">![Web deploy configuration](aspnet-mvc-4-custom-action-filters/_static/image32.png "Web deploy configuration")</span></span>

    <span data-ttu-id="bf36c-395">*Web 部署配置*</span><span class="sxs-lookup"><span data-stu-id="bf36c-395">*Web deploy configuration*</span></span>
5. <span data-ttu-id="bf36c-396">按如下所示配置数据库连接：</span><span class="sxs-lookup"><span data-stu-id="bf36c-396">Configure the database connection as follows:</span></span>

   - <span data-ttu-id="bf36c-397">在 "**服务器名称**" 中，键入您的 SQL 数据库服务器 URL，使用*tcp：* prefix。</span><span class="sxs-lookup"><span data-stu-id="bf36c-397">In the **Server name** type your SQL Database server URL using the *tcp:* prefix.</span></span>
   - <span data-ttu-id="bf36c-398">在 "**用户名**" 中键入服务器管理员登录名。</span><span class="sxs-lookup"><span data-stu-id="bf36c-398">In **User name** type your server administrator login name.</span></span>
   - <span data-ttu-id="bf36c-399">在 "**密码**" 中键入服务器管理员登录密码。</span><span class="sxs-lookup"><span data-stu-id="bf36c-399">In **Password** type your server administrator login password.</span></span>
   - <span data-ttu-id="bf36c-400">键入新的数据库名称。</span><span class="sxs-lookup"><span data-stu-id="bf36c-400">Type a new database name.</span></span>

     <span data-ttu-id="bf36c-401">![正在配置目标连接字符串](aspnet-mvc-4-custom-action-filters/_static/image33.png "正在配置目标连接字符串")</span><span class="sxs-lookup"><span data-stu-id="bf36c-401">![Configuring destination connection string](aspnet-mvc-4-custom-action-filters/_static/image33.png "Configuring destination connection string")</span></span>

     <span data-ttu-id="bf36c-402">*正在配置目标连接字符串*</span><span class="sxs-lookup"><span data-stu-id="bf36c-402">*Configuring destination connection string*</span></span>
6. <span data-ttu-id="bf36c-403">然后单击 **“确定”** 。</span><span class="sxs-lookup"><span data-stu-id="bf36c-403">Then click **OK**.</span></span> <span data-ttu-id="bf36c-404">系统提示创建数据库时，单击 **"是"** 。</span><span class="sxs-lookup"><span data-stu-id="bf36c-404">When prompted to create the database click **Yes**.</span></span>

    <span data-ttu-id="bf36c-405">![创建数据库](aspnet-mvc-4-custom-action-filters/_static/image34.png "创建数据库字符串")</span><span class="sxs-lookup"><span data-stu-id="bf36c-405">![Creating the database](aspnet-mvc-4-custom-action-filters/_static/image34.png "Creating the database string")</span></span>

    <span data-ttu-id="bf36c-406">*创建数据库*</span><span class="sxs-lookup"><span data-stu-id="bf36c-406">*Creating the database*</span></span>
7. <span data-ttu-id="bf36c-407">将用于连接到 Windows Azure 中的 SQL 数据库的连接字符串显示在 "默认连接" 文本框中。</span><span class="sxs-lookup"><span data-stu-id="bf36c-407">The connection string you will use to connect to SQL Database in Windows Azure is shown within Default Connection textbox.</span></span> <span data-ttu-id="bf36c-408">再单击 **“下一步”** 。</span><span class="sxs-lookup"><span data-stu-id="bf36c-408">Then click **Next**.</span></span>

    <span data-ttu-id="bf36c-409">![指向 SQL 数据库的连接字符串](aspnet-mvc-4-custom-action-filters/_static/image35.png "指向 SQL 数据库的连接字符串")</span><span class="sxs-lookup"><span data-stu-id="bf36c-409">![Connection string pointing to SQL Database](aspnet-mvc-4-custom-action-filters/_static/image35.png "Connection string pointing to SQL Database")</span></span>

    <span data-ttu-id="bf36c-410">*指向 SQL 数据库的连接字符串*</span><span class="sxs-lookup"><span data-stu-id="bf36c-410">*Connection string pointing to SQL Database*</span></span>
8. <span data-ttu-id="bf36c-411">在 "**预览**" 页上，单击 "**发布**"。</span><span class="sxs-lookup"><span data-stu-id="bf36c-411">In the **Preview** page, click **Publish**.</span></span>

    <span data-ttu-id="bf36c-412">![发布 web 应用程序](aspnet-mvc-4-custom-action-filters/_static/image36.png "发布 web 应用程序")</span><span class="sxs-lookup"><span data-stu-id="bf36c-412">![Publishing the web application](aspnet-mvc-4-custom-action-filters/_static/image36.png "Publishing the web application")</span></span>

    <span data-ttu-id="bf36c-413">*发布 web 应用程序*</span><span class="sxs-lookup"><span data-stu-id="bf36c-413">*Publishing the web application*</span></span>
9. <span data-ttu-id="bf36c-414">发布过程完成后，您的默认浏览器将打开已发布的网站。</span><span class="sxs-lookup"><span data-stu-id="bf36c-414">Once the publishing process finishes, your default browser will open the published web site.</span></span>

<a id="AppendixC"></a>

<a id="Appendix_C_Using_Code_Snippets"></a>
## <a name="appendix-c-using-code-snippets"></a><span data-ttu-id="bf36c-415">附录 C：使用代码片段</span><span class="sxs-lookup"><span data-stu-id="bf36c-415">Appendix C: Using Code Snippets</span></span>

<span data-ttu-id="bf36c-416">使用代码片段，您可以随时获得所需的全部代码。</span><span class="sxs-lookup"><span data-stu-id="bf36c-416">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="bf36c-417">实验室文档将告诉你何时可以使用它们，如下图所示。</span><span class="sxs-lookup"><span data-stu-id="bf36c-417">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="bf36c-418">![使用 Visual Studio code 代码段将代码插入到项目中](aspnet-mvc-4-custom-action-filters/_static/image37.png "使用 Visual Studio code 代码段将代码插入到项目中")</span><span class="sxs-lookup"><span data-stu-id="bf36c-418">![Using Visual Studio code snippets to insert code into your project](aspnet-mvc-4-custom-action-filters/_static/image37.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="bf36c-419">*使用 Visual Studio code 代码段将代码插入到项目中*</span><span class="sxs-lookup"><span data-stu-id="bf36c-419">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="bf36c-420">***使用键盘添加代码片段（C#仅限）***</span><span class="sxs-lookup"><span data-stu-id="bf36c-420">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="bf36c-421">将光标放在要插入代码的位置。</span><span class="sxs-lookup"><span data-stu-id="bf36c-421">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="bf36c-422">开始键入代码片段名称（不含空格或连字符）。</span><span class="sxs-lookup"><span data-stu-id="bf36c-422">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="bf36c-423">请注意，IntelliSense 显示匹配的代码段名称。</span><span class="sxs-lookup"><span data-stu-id="bf36c-423">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="bf36c-424">选择正确的代码段（或保留键入内容，直到选择了整个代码段的名称）。</span><span class="sxs-lookup"><span data-stu-id="bf36c-424">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="bf36c-425">按 Tab 键两次，将代码段插入到光标位置。</span><span class="sxs-lookup"><span data-stu-id="bf36c-425">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="bf36c-426">![开始键入代码片段名称](aspnet-mvc-4-custom-action-filters/_static/image38.png "开始键入代码片段名称")</span><span class="sxs-lookup"><span data-stu-id="bf36c-426">![Start typing the snippet name](aspnet-mvc-4-custom-action-filters/_static/image38.png "Start typing the snippet name")</span></span>

<span data-ttu-id="bf36c-427">*开始键入代码片段名称*</span><span class="sxs-lookup"><span data-stu-id="bf36c-427">*Start typing the snippet name*</span></span>

<span data-ttu-id="bf36c-428">![按 Tab 键以选择突出显示的代码段](aspnet-mvc-4-custom-action-filters/_static/image39.png "按 Tab 键以选择突出显示的代码段")</span><span class="sxs-lookup"><span data-stu-id="bf36c-428">![Press Tab to select the highlighted snippet](aspnet-mvc-4-custom-action-filters/_static/image39.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="bf36c-429">*按 Tab 键以选择突出显示的代码段*</span><span class="sxs-lookup"><span data-stu-id="bf36c-429">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="bf36c-430">![再次按 Tab 键，代码片段将展开](aspnet-mvc-4-custom-action-filters/_static/image40.png "再次按 Tab 键，代码片段将展开")</span><span class="sxs-lookup"><span data-stu-id="bf36c-430">![Press Tab again and the snippet will expand](aspnet-mvc-4-custom-action-filters/_static/image40.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="bf36c-431">*再次按 Tab 键，代码片段将展开*</span><span class="sxs-lookup"><span data-stu-id="bf36c-431">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="bf36c-432">***使用鼠标添加代码片段（C#、Visual Basic 和 XML）*** 2.</span><span class="sxs-lookup"><span data-stu-id="bf36c-432">***To add a code snippet using the mouse (C#, Visual Basic and XML)*** 1.</span></span> <span data-ttu-id="bf36c-433">右键单击要插入代码片段的位置。</span><span class="sxs-lookup"><span data-stu-id="bf36c-433">Right-click where you want to insert the code snippet.</span></span>

1. <span data-ttu-id="bf36c-434">选择 "**插入**代码片段"，然后选择 **"我的代码片段"** 。</span><span class="sxs-lookup"><span data-stu-id="bf36c-434">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
2. <span data-ttu-id="bf36c-435">通过单击从列表中选择相关的代码片段。</span><span class="sxs-lookup"><span data-stu-id="bf36c-435">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="bf36c-436">![右键单击要插入代码片段的位置，然后选择 "插入代码片段"](aspnet-mvc-4-custom-action-filters/_static/image41.png "右键单击要插入代码片段的位置，然后选择 "插入代码片段"")</span><span class="sxs-lookup"><span data-stu-id="bf36c-436">![Right-click where you want to insert the code snippet and select Insert Snippet](aspnet-mvc-4-custom-action-filters/_static/image41.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="bf36c-437">*右键单击要插入代码片段的位置，然后选择 "插入代码片段"*</span><span class="sxs-lookup"><span data-stu-id="bf36c-437">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="bf36c-438">![通过单击从列表中选择相关的代码片段](aspnet-mvc-4-custom-action-filters/_static/image42.png "通过单击从列表中选择相关的代码片段")</span><span class="sxs-lookup"><span data-stu-id="bf36c-438">![Pick the relevant snippet from the list, by clicking on it](aspnet-mvc-4-custom-action-filters/_static/image42.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="bf36c-439">*通过单击从列表中选择相关的代码片段*</span><span class="sxs-lookup"><span data-stu-id="bf36c-439">*Pick the relevant snippet from the list, by clicking on it*</span></span>

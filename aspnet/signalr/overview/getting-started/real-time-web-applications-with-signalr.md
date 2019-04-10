---
uid: signalr/overview/getting-started/real-time-web-applications-with-signalr
title: 动手实验：使用 SignalR 实时 Web 应用程序 |Microsoft Docs
author: bradygaster
description: 实时 Web 应用程序功能推送服务器端的情况下，实时连接的客户端到内容的功能。 对于 ASP.NET 开发人员，ASP...
ms.author: bradyg
ms.date: 07/16/2014
ms.assetid: ba07958c-42e1-4da0-81db-ba6925ed6db0
msc.legacyurl: /signalr/overview/getting-started/real-time-web-applications-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: 9904582450d4386ef8b8656078f6d40dbd1e10be
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/09/2019
ms.locfileid: "59412003"
---
# <a name="hands-on-lab-real-time-web-applications-with-signalr"></a><span data-ttu-id="513f1-104">动手实验：使用 SignalR 实现实时 Web 应用程序</span><span class="sxs-lookup"><span data-stu-id="513f1-104">Hands On Lab: Real-Time Web Applications with SignalR</span></span>


<span data-ttu-id="513f1-105">通过[Web 训练营团队](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="513f1-105">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

[<span data-ttu-id="513f1-106">下载 Web 训练营培训工具包，2015 年 10 月版本</span><span class="sxs-lookup"><span data-stu-id="513f1-106">Download Web Camps Training Kit, October 2015 Release</span></span>](https://github.com/Microsoft-Web/WebCampTrainingKit/releases/tag/v2015.10.13b)

> <span data-ttu-id="513f1-107">实时 Web 应用程序功能推送服务器端的情况下，实时连接的客户端到内容的功能。</span><span class="sxs-lookup"><span data-stu-id="513f1-107">Real-time Web applications feature the ability to push server-side content to the connected clients as it happens, in real-time.</span></span> <span data-ttu-id="513f1-108">面向 ASP.NET 开发人员**ASP.NET SignalR**是一个库，以将实时 web 功能添加到其应用程序。</span><span class="sxs-lookup"><span data-stu-id="513f1-108">For ASP.NET developers, **ASP.NET SignalR** is a library to add real-time web functionality to their applications.</span></span> <span data-ttu-id="513f1-109">它利用多个传输协议，会自动选择给定客户端和服务器的最佳可用的传输最佳的可用传输。</span><span class="sxs-lookup"><span data-stu-id="513f1-109">It takes advantage of several transports, automatically selecting the best available transport given the client and server's best available transport.</span></span> <span data-ttu-id="513f1-110">它利用**WebSocket**，一个 HTML5 API，使浏览器和服务器之间的双向通信。</span><span class="sxs-lookup"><span data-stu-id="513f1-110">It takes advantage of **WebSocket**, an HTML5 API that enables bi-directional communication between the browser and server.</span></span>
> 
> <span data-ttu-id="513f1-111">**SignalR**还执行服务器到客户端 RPC 提供简单、 高级 API （在客户端的浏览器从服务器端.NET 代码中调用 JavaScript 函数） 在 ASP.NET 应用程序，以及添加有用的挂钩，以便连接管理例如，连接/断开连接事件、 分组连接和授权。</span><span class="sxs-lookup"><span data-stu-id="513f1-111">**SignalR** also provides a simple, high-level API for doing server to client RPC (call JavaScript functions in your clients' browsers from server-side .NET code) in your ASP.NET application, as well as adding useful hooks for connection management, such as connect/disconnect events, grouping connections, and authorization.</span></span>
> 
> <span data-ttu-id="513f1-112">**SignalR**通过某些要求进行客户端和服务器之间的实时工作的传输的是一种抽象。</span><span class="sxs-lookup"><span data-stu-id="513f1-112">**SignalR** is an abstraction over some of the transports that are required to do real-time work between client and server.</span></span> <span data-ttu-id="513f1-113">一个**SignalR**连接为 HTTP，将启动，然后升级到**WebSocket**如果可用的连接。</span><span class="sxs-lookup"><span data-stu-id="513f1-113">A **SignalR** connection starts as HTTP, and is then promoted to a **WebSocket** connection if available.</span></span> <span data-ttu-id="513f1-114">**WebSocket**是用于的理想之选传输**SignalR**，因为这会导致服务器内存的最有效地使用具有最低的延迟，并且具有最基础的功能 (例如客户端之间的全双工通信和服务器），但它还具有最严格的要求：**WebSocket**要求要使用的服务器**Windows Server 2012**或**Windows 8**，连同 **.NET Framework 4.5**。</span><span class="sxs-lookup"><span data-stu-id="513f1-114">**WebSocket** is the ideal transport for **SignalR**, since it makes the most efficient use of server memory, has the lowest latency, and has the most underlying features (such as full duplex communication between client and server), but it also has the most stringent requirements: **WebSocket** requires the server to be using **Windows Server 2012** or **Windows 8**, along with **.NET Framework 4.5**.</span></span> <span data-ttu-id="513f1-115">如果不满足这些要求， **SignalR**将尝试使用其他传输，以使其连接 (如*Ajax 长轮询*)。</span><span class="sxs-lookup"><span data-stu-id="513f1-115">If these requirements are not met, **SignalR** will attempt to use other transports to make its connections (like *Ajax long polling*).</span></span>
> 
> <span data-ttu-id="513f1-116">**SignalR** API 包含客户端和服务器之间进行通信的两个模型：**持久连接**并**中心**。</span><span class="sxs-lookup"><span data-stu-id="513f1-116">The **SignalR** API contains two models for communicating between clients and servers: **Persistent Connections** and **Hubs**.</span></span> <span data-ttu-id="513f1-117">一个**连接**表示一个简单的终结点发送单一接收方组合在一起，或广播消息。</span><span class="sxs-lookup"><span data-stu-id="513f1-117">A **Connection** represents a simple endpoint for sending single-recipient, grouped, or broadcast messages.</span></span> <span data-ttu-id="513f1-118">一个**中心**是基于连接 API，从而使您的客户端和服务器直接相互调用方法的更多高级管道。</span><span class="sxs-lookup"><span data-stu-id="513f1-118">A **Hub** is a more high-level pipeline built upon the Connection API that allows your client and server to call methods on each other directly.</span></span>
> 
> ![SignalR 体系结构](real-time-web-applications-with-signalr/_static/image1.png)
> 
> <span data-ttu-id="513f1-120">将包含所有示例代码和代码段 Web 训练营培训工具包，2015 年 10 月版本中，可在[ https://github.com/Microsoft-Web/WebCampTrainingKit/releases/tag/v2015.10.13b ](https://github.com/Microsoft-Web/WebCampTrainingKit/releases/tag/v2015.10.13b)。</span><span class="sxs-lookup"><span data-stu-id="513f1-120">All sample code and snippets are included in the Web Camps Training Kit, October 2015 Release, available at [https://github.com/Microsoft-Web/WebCampTrainingKit/releases/tag/v2015.10.13b](https://github.com/Microsoft-Web/WebCampTrainingKit/releases/tag/v2015.10.13b).</span></span>  <span data-ttu-id="513f1-121">请注意，该页面上的安装程序链接不再有效;改为使用在资产部分下的某个链接。</span><span class="sxs-lookup"><span data-stu-id="513f1-121">Please note that the Installer link on that page no longer works; use one of the links under the Assets section instead.</span></span>

<a id="Overview"></a>
## <a name="overview"></a><span data-ttu-id="513f1-122">概述</span><span class="sxs-lookup"><span data-stu-id="513f1-122">Overview</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="513f1-123">目标</span><span class="sxs-lookup"><span data-stu-id="513f1-123">Objectives</span></span>

<span data-ttu-id="513f1-124">在本动手实验，您将学习如何：</span><span class="sxs-lookup"><span data-stu-id="513f1-124">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="513f1-125">从服务器中将通知发送到使用 SignalR 客户端。</span><span class="sxs-lookup"><span data-stu-id="513f1-125">Send notifications from server to client using SignalR.</span></span>
- <span data-ttu-id="513f1-126">SignalR 应用程序使用扩大**SQL Server**。</span><span class="sxs-lookup"><span data-stu-id="513f1-126">Scale Out your SignalR application using **SQL Server**.</span></span>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="513f1-127">系统必备</span><span class="sxs-lookup"><span data-stu-id="513f1-127">Prerequisites</span></span>

<span data-ttu-id="513f1-128">完成本动手实验需要以下：</span><span class="sxs-lookup"><span data-stu-id="513f1-128">The following is required to complete this hands-on lab:</span></span>

- <span data-ttu-id="513f1-129">[Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/)或更高版本</span><span class="sxs-lookup"><span data-stu-id="513f1-129">[Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/) or greater</span></span>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="513f1-130">安装</span><span class="sxs-lookup"><span data-stu-id="513f1-130">Setup</span></span>

<span data-ttu-id="513f1-131">若要运行本动手实验中练习，需要先设置你的环境。</span><span class="sxs-lookup"><span data-stu-id="513f1-131">In order to run the exercises in this hands-on lab, you will need to set up your environment first.</span></span>

1. <span data-ttu-id="513f1-132">打开 Windows 资源管理器窗口并浏览到本实验**源**文件夹。</span><span class="sxs-lookup"><span data-stu-id="513f1-132">Open a Windows Explorer window and browse to the lab's **Source** folder.</span></span>
2. <span data-ttu-id="513f1-133">右键单击**Setup.cmd** ，然后选择**以管理员身份运行**以启动将配置你的环境并安装本实验的 Visual Studio 代码段的安装过程。</span><span class="sxs-lookup"><span data-stu-id="513f1-133">Right-click **Setup.cmd** and select **Run as administrator** to launch the setup process that will configure your environment and install the Visual Studio code snippets for this lab.</span></span>
3. <span data-ttu-id="513f1-134">如果显示用户帐户控制对话框中，确认要继续执行的操作。</span><span class="sxs-lookup"><span data-stu-id="513f1-134">If the User Account Control dialog box is shown, confirm the action to proceed.</span></span>

> [!NOTE]
> <span data-ttu-id="513f1-135">请确保您运行安装程序之前已为此实验室的所有依赖项。</span><span class="sxs-lookup"><span data-stu-id="513f1-135">Make sure you have checked all the dependencies for this lab before running the setup.</span></span>


<a id="CodeSnippets"></a>
### <a name="using-the-code-snippets"></a><span data-ttu-id="513f1-136">使用代码片段</span><span class="sxs-lookup"><span data-stu-id="513f1-136">Using the Code Snippets</span></span>

<span data-ttu-id="513f1-137">在整个实验文档中，将指示您插入代码块。</span><span class="sxs-lookup"><span data-stu-id="513f1-137">Throughout the lab document, you will be instructed to insert code blocks.</span></span> <span data-ttu-id="513f1-138">为方便起见，此代码的大部分以 Visual Studio 代码段，可以在 Visual Studio 2013，为了避免必须手动添加访问从形式提供。</span><span class="sxs-lookup"><span data-stu-id="513f1-138">For your convenience, most of this code is provided as Visual Studio Code Snippets, which you can access from within Visual Studio 2013 to avoid having to add it manually.</span></span>

> [!NOTE]
> <span data-ttu-id="513f1-139">每个练习均附带位于中的开始解决方案**开始**本练习，您可以按照独立于其他每个练习的文件夹。</span><span class="sxs-lookup"><span data-stu-id="513f1-139">Each exercise is accompanied by a starting solution located in the **Begin** folder of the exercise that allows you to follow each exercise independently of the others.</span></span> <span data-ttu-id="513f1-140">请注意在练习期间添加的代码片段缺少这些开始解决方案中，并且可能无法工作，直到完成该练习。</span><span class="sxs-lookup"><span data-stu-id="513f1-140">Please be aware that the code snippets that are added during an exercise are missing from these starting solutions and may not work until you have completed the exercise.</span></span> <span data-ttu-id="513f1-141">在练习的源代码，您将发现**最终**包含具有无法完成相应练习中的步骤得到的代码的 Visual Studio 解决方案文件夹。</span><span class="sxs-lookup"><span data-stu-id="513f1-141">Inside the source code for an exercise, you will also find an **End** folder containing a Visual Studio solution with the code that results from completing the steps in the corresponding exercise.</span></span> <span data-ttu-id="513f1-142">如果您在演练本动手实验需要更多帮助，可以使用这些解决方案作为指南。</span><span class="sxs-lookup"><span data-stu-id="513f1-142">You can use these solutions as guidance if you need additional help as you work through this hands-on lab.</span></span>


---

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="513f1-143">练习</span><span class="sxs-lookup"><span data-stu-id="513f1-143">Exercises</span></span>

<span data-ttu-id="513f1-144">本动手实验包括以下练习：</span><span class="sxs-lookup"><span data-stu-id="513f1-144">This hands-on lab includes the following exercises:</span></span>

1. [<span data-ttu-id="513f1-145">使用 SignalR 的实时数据处理</span><span class="sxs-lookup"><span data-stu-id="513f1-145">Working with Real-Time Data Using SignalR</span></span>](#Exercise1)
2. [<span data-ttu-id="513f1-146">向外扩展使用的 SQL Server</span><span class="sxs-lookup"><span data-stu-id="513f1-146">Scaling Out Using SQL Server</span></span>](#Exercise2)

<span data-ttu-id="513f1-147">估计的时间才能完成此实验：**60 分钟**</span><span class="sxs-lookup"><span data-stu-id="513f1-147">Estimated time to complete this lab: **60 minutes**</span></span>

> [!NOTE]
> <span data-ttu-id="513f1-148">在首次启动 Visual Studio，您必须选择一个预定义的设置集合。</span><span class="sxs-lookup"><span data-stu-id="513f1-148">When you first start Visual Studio, you must select one of the predefined settings collections.</span></span> <span data-ttu-id="513f1-149">每个预定义的集合旨在符合特定的开发风格，并确定窗口布局、 编辑器行为、 IntelliSense 代码段和对话框选项。</span><span class="sxs-lookup"><span data-stu-id="513f1-149">Each predefined collection is designed to match a particular development style and determines window layouts, editor behavior, IntelliSense code snippets, and dialog box options.</span></span> <span data-ttu-id="513f1-150">此实验中的过程描述了完成给定的任务在 Visual Studio 中使用时所需的操作**常规开发设置**集合。</span><span class="sxs-lookup"><span data-stu-id="513f1-150">The procedures in this lab describe the actions necessary to accomplish a given task in Visual Studio when using the **General Development Settings** collection.</span></span> <span data-ttu-id="513f1-151">如果您为您的开发环境选择不同的设置集合，可能会中应考虑到的步骤有所不同。</span><span class="sxs-lookup"><span data-stu-id="513f1-151">If you choose a different settings collection for your development environment, there may be differences in the steps that you should take into account.</span></span>


<a id="Exercise1"></a>
### <a name="exercise-1-working-with-real-time-data-using-signalr"></a><span data-ttu-id="513f1-152">练习 1:使用 SignalR 的实时数据处理</span><span class="sxs-lookup"><span data-stu-id="513f1-152">Exercise 1: Working with Real-Time Data Using SignalR</span></span>

<span data-ttu-id="513f1-153">尽管聊天通常用作示例，您可以为一个整体很多更多的实时 Web 功能。</span><span class="sxs-lookup"><span data-stu-id="513f1-153">While chat is often used as an example, you can do a whole lot more with real-time Web functionality.</span></span> <span data-ttu-id="513f1-154">每当用户刷新网页可看到新数据或页面实现 Ajax 长轮询以检索新数据，可以使用 SignalR。</span><span class="sxs-lookup"><span data-stu-id="513f1-154">Any time a user refreshes a web page to see new data or the page implements Ajax long polling to retrieve new data, you can use SignalR.</span></span>

<span data-ttu-id="513f1-155">SignalR 支持**服务器推送**或**广播**功能; 它会自动处理的连接管理。</span><span class="sxs-lookup"><span data-stu-id="513f1-155">SignalR supports **server push** or **broadcasting** functionality; it handles connection management automatically.</span></span> <span data-ttu-id="513f1-156">在客户端-服务器通信的经典 HTTP 连接，为每个请求重新建立连接后但 SignalR 提供了客户端和服务器之间的持续性连接。</span><span class="sxs-lookup"><span data-stu-id="513f1-156">In classic HTTP connections for client-server communication, connection is re-established for each request, but SignalR provides persistent connection between the client and server.</span></span> <span data-ttu-id="513f1-157">在 SignalR 中的服务器代码调用中使用远程过程调用 (RPC) 的浏览器的客户端代码，而不是请求-响应模型如今我们知道。</span><span class="sxs-lookup"><span data-stu-id="513f1-157">In SignalR the server code calls out to a client code in the browser using Remote Procedure Calls (RPC), rather than the request-response model we know today.</span></span>

<span data-ttu-id="513f1-158">在此练习中，您将配置**极客测验**应用程序使用 SignalR 显示统计信息仪表板使用已更新的指标，而无需刷新整个页面。</span><span class="sxs-lookup"><span data-stu-id="513f1-158">In this exercise, you will configure the **Geek Quiz** application to use SignalR to display the Statistics dashboard with the updated metrics without the need to refresh the entire page.</span></span>

<a id="Ex1Task1"></a>
#### <a name="task-1--exploring-the-geek-quiz-statistics-page"></a><span data-ttu-id="513f1-159">任务 1 – 探索极客测验统计信息页</span><span class="sxs-lookup"><span data-stu-id="513f1-159">Task 1 – Exploring the Geek Quiz Statistics Page</span></span>

<span data-ttu-id="513f1-160">在此任务中，将通过应用程序并验证统计信息页上的显示方式，并可以如何改进信息的方式更新。</span><span class="sxs-lookup"><span data-stu-id="513f1-160">In this task, you will go through the application and verify how the statistics page is shown and how you can improve the way the information is updated.</span></span>

1. <span data-ttu-id="513f1-161">打开**Visual Studio Express 2013 for Web** ，然后打开**GeekQuiz.sln**解决方案位于**Source\Ex1 WorkingWithRealTimeData\Begin**文件夹。</span><span class="sxs-lookup"><span data-stu-id="513f1-161">Open **Visual Studio Express 2013 for Web** and open the **GeekQuiz.sln** solution located in the **Source\Ex1-WorkingWithRealTimeData\Begin** folder.</span></span>
2. <span data-ttu-id="513f1-162">按**F5**运行该解决方案。</span><span class="sxs-lookup"><span data-stu-id="513f1-162">Press **F5** to run the solution.</span></span> <span data-ttu-id="513f1-163">**登录**页应显示在浏览器中。</span><span class="sxs-lookup"><span data-stu-id="513f1-163">The **Log in** page should appear in the browser.</span></span>

    <span data-ttu-id="513f1-164">![运行解决方案](real-time-web-applications-with-signalr/_static/image2.png "运行解决方案")</span><span class="sxs-lookup"><span data-stu-id="513f1-164">![Running the solution](real-time-web-applications-with-signalr/_static/image2.png "Running the solution")</span></span>

    *<span data-ttu-id="513f1-165">运行解决方案</span><span class="sxs-lookup"><span data-stu-id="513f1-165">Running the solution</span></span>*
3. <span data-ttu-id="513f1-166">单击**注册**右上角的页后，可以在应用程序中创建新用户。</span><span class="sxs-lookup"><span data-stu-id="513f1-166">Click **Register** in the upper-right corner of the page to create a new user in the application.</span></span>

    <span data-ttu-id="513f1-167">![注册链接](real-time-web-applications-with-signalr/_static/image3.png "注册链接")</span><span class="sxs-lookup"><span data-stu-id="513f1-167">![Register link](real-time-web-applications-with-signalr/_static/image3.png "Register link")</span></span>

    *<span data-ttu-id="513f1-168">注册链接</span><span class="sxs-lookup"><span data-stu-id="513f1-168">Register link</span></span>*
4. <span data-ttu-id="513f1-169">在中**注册**页上，输入**用户名**并**密码**，然后单击**注册**。</span><span class="sxs-lookup"><span data-stu-id="513f1-169">In the **Register** page, enter a **User name** and **Password**, and then click **Register**.</span></span>

    <span data-ttu-id="513f1-170">![注册用户](real-time-web-applications-with-signalr/_static/image4.png "注册用户")</span><span class="sxs-lookup"><span data-stu-id="513f1-170">![Registering a user](real-time-web-applications-with-signalr/_static/image4.png "Registering a user")</span></span>

    *<span data-ttu-id="513f1-171">注册用户</span><span class="sxs-lookup"><span data-stu-id="513f1-171">Registering a user</span></span>*
5. <span data-ttu-id="513f1-172">应用程序注册新帐户和用户进行身份验证和重定向回到主页上显示的第一个测验问题。</span><span class="sxs-lookup"><span data-stu-id="513f1-172">The application registers the new account and the user is authenticated and redirected back to the home page showing the first quiz question.</span></span>
6. <span data-ttu-id="513f1-173">打开**统计信息**页上，在新窗口中，并将放**主页**页并**统计信息**页上的并排方案。</span><span class="sxs-lookup"><span data-stu-id="513f1-173">Open the **Statistics** page in a new window and put the **Home** page and **Statistics** page side-by-side.</span></span>

    <span data-ttu-id="513f1-174">![通过并行 windows](real-time-web-applications-with-signalr/_static/image5.png "端 windows 端")</span><span class="sxs-lookup"><span data-stu-id="513f1-174">![Side-by-side windows](real-time-web-applications-with-signalr/_static/image5.png "Side by side windows")</span></span>

    *<span data-ttu-id="513f1-175">通过并行 windows</span><span class="sxs-lookup"><span data-stu-id="513f1-175">Side-by-side windows</span></span>*
7. <span data-ttu-id="513f1-176">在中**主页**页上，通过单击某个选项来回答问题。</span><span class="sxs-lookup"><span data-stu-id="513f1-176">In the **Home** page, answer the question by clicking one of the options.</span></span>

    <span data-ttu-id="513f1-177">![回答问题](real-time-web-applications-with-signalr/_static/image6.png "回答问题")</span><span class="sxs-lookup"><span data-stu-id="513f1-177">![Answering a question](real-time-web-applications-with-signalr/_static/image6.png "Answering a question")</span></span>

    *<span data-ttu-id="513f1-178">回答问题</span><span class="sxs-lookup"><span data-stu-id="513f1-178">Answering a question</span></span>*
8. <span data-ttu-id="513f1-179">单击其中一个按钮后, 应显示答案。</span><span class="sxs-lookup"><span data-stu-id="513f1-179">After clicking one of the buttons, the answer should appear.</span></span>

    <span data-ttu-id="513f1-180">![问题回答正确](real-time-web-applications-with-signalr/_static/image7.png "正确回答的问题")</span><span class="sxs-lookup"><span data-stu-id="513f1-180">![Question answered correct](real-time-web-applications-with-signalr/_static/image7.png "Question answered correct")</span></span>

    *<span data-ttu-id="513f1-181">正确回答的问题</span><span class="sxs-lookup"><span data-stu-id="513f1-181">Question answered correctly</span></span>*
9. <span data-ttu-id="513f1-182">请注意统计信息页中提供的信息已过时。</span><span class="sxs-lookup"><span data-stu-id="513f1-182">Notice that the information provided in the Statistics page is outdated.</span></span> <span data-ttu-id="513f1-183">刷新页面才能看到更新后的结果。</span><span class="sxs-lookup"><span data-stu-id="513f1-183">Refresh the page in order to see the updated results.</span></span>

    <span data-ttu-id="513f1-184">![统计信息页面](real-time-web-applications-with-signalr/_static/image8.png "统计信息页")</span><span class="sxs-lookup"><span data-stu-id="513f1-184">![Statistics page](real-time-web-applications-with-signalr/_static/image8.png "Statistics page")</span></span>

    *<span data-ttu-id="513f1-185">统计信息页</span><span class="sxs-lookup"><span data-stu-id="513f1-185">Statistics page</span></span>*
10. <span data-ttu-id="513f1-186">返回到 Visual Studio 和停止调试。</span><span class="sxs-lookup"><span data-stu-id="513f1-186">Go back to Visual Studio and stop debugging.</span></span>

<a id="Ex1Task2"></a>
#### <a name="task-2--adding-signalr-to-geek-quiz-to-show-online-charts"></a><span data-ttu-id="513f1-187">任务 2 – 为极客测验以显示联机图表添加 SignalR</span><span class="sxs-lookup"><span data-stu-id="513f1-187">Task 2 – Adding SignalR to Geek Quiz to Show Online Charts</span></span>

<span data-ttu-id="513f1-188">在本任务中，将添加到解决方案的 SignalR，并将更新发送到客户端自动在新的答案发送到服务器时。</span><span class="sxs-lookup"><span data-stu-id="513f1-188">In this task, you will add SignalR to the solution and send updates to the clients automatically when a new answer is sent to the server.</span></span>

1. <span data-ttu-id="513f1-189">从**工具**在 Visual Studio 中，选择菜单**NuGet 包管理器**，然后单击**程序包管理器控制台**。</span><span class="sxs-lookup"><span data-stu-id="513f1-189">From the **Tools** menu in Visual Studio, select **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>
2. <span data-ttu-id="513f1-190">在中**程序包管理器控制台**窗口中，执行以下命令：</span><span class="sxs-lookup"><span data-stu-id="513f1-190">In the **Package Manager Console** window, execute the following command:</span></span>

    [!code-powershell[Main](real-time-web-applications-with-signalr/samples/sample1.ps1)]

    <span data-ttu-id="513f1-191">![SignalR 包安装](real-time-web-applications-with-signalr/_static/image9.png "SignalR 包安装")</span><span class="sxs-lookup"><span data-stu-id="513f1-191">![SignalR package installation](real-time-web-applications-with-signalr/_static/image9.png "SignalR package installation")</span></span>

    *<span data-ttu-id="513f1-192">SignalR 包安装</span><span class="sxs-lookup"><span data-stu-id="513f1-192">SignalR package installation</span></span>*

   > [!NOTE]
   > <span data-ttu-id="513f1-193">安装时**SignalR** NuGet 包版本 2.0.2 从全新的 MVC 5 应用程序，你将需要手动更新**OWIN**程序包更新到版本 2.0.1 （或更高版本） 安装 SignalR 之前。</span><span class="sxs-lookup"><span data-stu-id="513f1-193">When installing **SignalR** NuGet packages version 2.0.2 from a brand new MVC 5 application, you will need to manually update **OWIN** packages to version 2.0.1 (or higher) before installing SignalR.</span></span> <span data-ttu-id="513f1-194">若要执行此操作，可以执行以下脚本**程序包管理器控制台**:</span><span class="sxs-lookup"><span data-stu-id="513f1-194">To do this, you can execute the following script in the **Package Manager Console**:</span></span>
   > 
   > [!code-powershell[Main](real-time-web-applications-with-signalr/samples/sample2.ps1)]
   > 
   > <span data-ttu-id="513f1-195">在 SignalR 的未来版本中，将自动更新 OWIN 依赖项。</span><span class="sxs-lookup"><span data-stu-id="513f1-195">In a future release of SignalR, OWIN dependencies will be automatically updated.</span></span>
3. <span data-ttu-id="513f1-196">在中**解决方案资源管理器**，展开**脚本**文件夹，然后请注意，SignalR *js*文件已添加到解决方案。</span><span class="sxs-lookup"><span data-stu-id="513f1-196">In **Solution Explorer**, expand the **Scripts** folder and notice that the SignalR *js* files were added to the solution.</span></span>

    <span data-ttu-id="513f1-197">![SignalR JavaScript 引用](real-time-web-applications-with-signalr/_static/image10.png "SignalR JavaScript 引用")</span><span class="sxs-lookup"><span data-stu-id="513f1-197">![SignalR JavaScript references](real-time-web-applications-with-signalr/_static/image10.png "SignalR JavaScript references")</span></span>

    *<span data-ttu-id="513f1-198">SignalR JavaScript 引用</span><span class="sxs-lookup"><span data-stu-id="513f1-198">SignalR JavaScript references</span></span>*
4. <span data-ttu-id="513f1-199">在中**解决方案资源管理器**，右键单击**GeekQuiz**项目，选择**添加** | **新文件夹**，并将其命名**中心**。</span><span class="sxs-lookup"><span data-stu-id="513f1-199">In **Solution Explorer**, right-click the **GeekQuiz** project, select **Add** | **New Folder**, and name it **Hubs**.</span></span>
5. <span data-ttu-id="513f1-200">右键单击**中心**文件夹，然后选择**添加 |新项**。</span><span class="sxs-lookup"><span data-stu-id="513f1-200">Right-click the **Hubs** folder and select **Add | New Item**.</span></span>

    <span data-ttu-id="513f1-201">![添加新项](real-time-web-applications-with-signalr/_static/image11.png "添加新项")</span><span class="sxs-lookup"><span data-stu-id="513f1-201">![Add new item](real-time-web-applications-with-signalr/_static/image11.png "Add new item")</span></span>

    *<span data-ttu-id="513f1-202">添加新项</span><span class="sxs-lookup"><span data-stu-id="513f1-202">Add new item</span></span>*
6. <span data-ttu-id="513f1-203">在中**添加新项**对话框中，选择**Visual C# |Web |SignalR**的左窗格中，选择节点**SignalR Hub 类 (v2)** 在中心窗格中，将文件命名**StatisticsHub.cs**然后单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="513f1-203">In the **Add New Item** dialog box, select the **Visual C# | Web | SignalR** node in the left pane, select **SignalR Hub Class (v2)** from the center pane, name the file **StatisticsHub.cs** and click **Add**.</span></span>

    <span data-ttu-id="513f1-204">![添加新项对话框](real-time-web-applications-with-signalr/_static/image12.png "添加新项对话框")</span><span class="sxs-lookup"><span data-stu-id="513f1-204">![Add new item dialog box](real-time-web-applications-with-signalr/_static/image12.png "Add new item dialog box")</span></span>

    *<span data-ttu-id="513f1-205">添加新项对话框</span><span class="sxs-lookup"><span data-stu-id="513f1-205">Add new item dialog box</span></span>*
7. <span data-ttu-id="513f1-206">中的代码替换**StatisticsHub**用下面的代码的类。</span><span class="sxs-lookup"><span data-stu-id="513f1-206">Replace the code in the **StatisticsHub** class with the following code.</span></span>

    <span data-ttu-id="513f1-207">(代码段- *RealTimeSignalR-Ex1-StatisticsHubClass*)</span><span class="sxs-lookup"><span data-stu-id="513f1-207">(Code Snippet - *RealTimeSignalR - Ex1 - StatisticsHubClass*)</span></span>

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample3.cs)]
8. <span data-ttu-id="513f1-208">打开**Startup.cs** ，并在末尾添加以下行**配置**方法。</span><span class="sxs-lookup"><span data-stu-id="513f1-208">Open **Startup.cs** and add the following line at the end of the **Configuration** method.</span></span>

    <span data-ttu-id="513f1-209">(代码段- *RealTimeSignalR-Ex1-MapSignalR*)</span><span class="sxs-lookup"><span data-stu-id="513f1-209">(Code Snippet - *RealTimeSignalR - Ex1 - MapSignalR*)</span></span>

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample4.cs)]
9. <span data-ttu-id="513f1-210">打开**StatisticsService.cs**页内**服务**文件夹并添加以下 using 指令。</span><span class="sxs-lookup"><span data-stu-id="513f1-210">Open the **StatisticsService.cs** page inside the **Services** folder and add the following using directives.</span></span>

    <span data-ttu-id="513f1-211">(代码段- *RealTimeSignalR-Ex1-UsingDirectives*)</span><span class="sxs-lookup"><span data-stu-id="513f1-211">(Code Snippet - *RealTimeSignalR - Ex1 - UsingDirectives*)</span></span>

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample5.cs)]
10. <span data-ttu-id="513f1-212">若要通知连接的客户端的更新，请首先检索**上下文**当前连接对象。</span><span class="sxs-lookup"><span data-stu-id="513f1-212">To notify connected clients of updates, you first retrieve a **Context** object for the current connection.</span></span> <span data-ttu-id="513f1-213">**中心**对象包含用于将消息发送到单个客户端或广播到所有已连接的客户端的方法。</span><span class="sxs-lookup"><span data-stu-id="513f1-213">The **Hub** object contains methods to send messages to a single client or broadcast to all connected clients.</span></span> <span data-ttu-id="513f1-214">添加以下方法**StatisticsService**类广播的统计信息数据。</span><span class="sxs-lookup"><span data-stu-id="513f1-214">Add the following method to the **StatisticsService** class to broadcast the statistics data.</span></span>

    <span data-ttu-id="513f1-215">(代码段- *RealTimeSignalR-Ex1-NotifyUpdatesMethod*)</span><span class="sxs-lookup"><span data-stu-id="513f1-215">(Code Snippet - *RealTimeSignalR - Ex1 - NotifyUpdatesMethod*)</span></span>

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample6.cs)]

    > [!NOTE]
    > <span data-ttu-id="513f1-216">在上面的代码中，您将使用任意方法名称来在客户端上调用的函数 (即： *updateStatistics*)。</span><span class="sxs-lookup"><span data-stu-id="513f1-216">In the code above, you are using an arbitrary method name to call a function on the client (i.e.: *updateStatistics*).</span></span> <span data-ttu-id="513f1-217">您指定的方法名称被解释为动态对象，这意味着没有 IntelliSense 或它的编译时验证。</span><span class="sxs-lookup"><span data-stu-id="513f1-217">The method name that you specify is interpreted as a dynamic object, which means there is no IntelliSense or compile-time validation for it.</span></span> <span data-ttu-id="513f1-218">在运行时计算表达式。</span><span class="sxs-lookup"><span data-stu-id="513f1-218">The expression is evaluated at run time.</span></span> <span data-ttu-id="513f1-219">方法调用执行时，SignalR 将方法名称和参数值发送到客户端。</span><span class="sxs-lookup"><span data-stu-id="513f1-219">When the method call executes, SignalR sends the method name and the parameter values to the client.</span></span> <span data-ttu-id="513f1-220">如果客户端相匹配的名称，调用方法和参数值传递给它的方法。</span><span class="sxs-lookup"><span data-stu-id="513f1-220">If the client has a method that matches the name, that method is called and the parameter values are passed to it.</span></span> <span data-ttu-id="513f1-221">如果在客户端上不找到任何匹配的方法，则不会引发错误。</span><span class="sxs-lookup"><span data-stu-id="513f1-221">If no matching method is found on the client, no error is raised.</span></span> <span data-ttu-id="513f1-222">有关详细信息，请参阅[ASP.NET SignalR 中心 API 指南](../guide-to-the-api/hubs-api-guide-server.md)。</span><span class="sxs-lookup"><span data-stu-id="513f1-222">For more information, refer to [ASP.NET SignalR Hubs API Guide](../guide-to-the-api/hubs-api-guide-server.md).</span></span>
11. <span data-ttu-id="513f1-223">打开**TriviaController.cs**页内**控制器**文件夹并添加以下 using 指令。</span><span class="sxs-lookup"><span data-stu-id="513f1-223">Open the **TriviaController.cs** page inside the **Controllers** folder and add the following using directives.</span></span>

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample7.cs)]
12. <span data-ttu-id="513f1-224">将以下突出显示的代码添加到**Post**操作方法。</span><span class="sxs-lookup"><span data-stu-id="513f1-224">Add the following highlighted code to the **Post** action method.</span></span>

    <span data-ttu-id="513f1-225">(代码段- *RealTimeSignalR-Ex1-NotifyUpdatesCall*)</span><span class="sxs-lookup"><span data-stu-id="513f1-225">(Code Snippet - *RealTimeSignalR - Ex1 - NotifyUpdatesCall*)</span></span>

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample8.cs)]
13. <span data-ttu-id="513f1-226">打开**Statistics.cshtml**页内**视图 |主页**文件夹。</span><span class="sxs-lookup"><span data-stu-id="513f1-226">Open the **Statistics.cshtml** page inside the **Views | Home** folder.</span></span> <span data-ttu-id="513f1-227">找到**脚本**部分，并在部分的开头添加以下脚本引用。</span><span class="sxs-lookup"><span data-stu-id="513f1-227">Locate the **Scripts** section and add the following script references at the beginning of the section.</span></span>

    <span data-ttu-id="513f1-228">(代码段- *RealTimeSignalR-Ex1-SignalRScriptReferences*)</span><span class="sxs-lookup"><span data-stu-id="513f1-228">(Code Snippet - *RealTimeSignalR - Ex1 - SignalRScriptReferences*)</span></span>

    [!code-cshtml[Main](real-time-web-applications-with-signalr/samples/sample9.cshtml)]

    > [!NOTE]
    > <span data-ttu-id="513f1-229">当您将 SignalR 和其他脚本库添加到你的 Visual Studio 项目中时，包管理器可能会安装比本主题中所示的版本更新的 SignalR 脚本文件的版本。</span><span class="sxs-lookup"><span data-stu-id="513f1-229">When you add SignalR and other script libraries to your Visual Studio project, the Package Manager might install a version of the SignalR script file that is more recent than the version shown in this topic.</span></span> <span data-ttu-id="513f1-230">请确保在代码中的脚本引用与脚本库在项目中安装的版本匹配。</span><span class="sxs-lookup"><span data-stu-id="513f1-230">Make sure that the script reference in your code matches the version of the script library installed in your project.</span></span>
14. <span data-ttu-id="513f1-231">添加以下突出显示的代码连接到 SignalR 集线器的客户端并从中心接收新消息时更新统计信息数据。</span><span class="sxs-lookup"><span data-stu-id="513f1-231">Add the following highlighted code to connect the client to the SignalR hub and update the statistics data when a new message is received from the hub.</span></span>

    <span data-ttu-id="513f1-232">(Code Snippet - *RealTimeSignalR - Ex1 - SignalRClientCode*)</span><span class="sxs-lookup"><span data-stu-id="513f1-232">(Code Snippet - *RealTimeSignalR - Ex1 - SignalRClientCode*)</span></span>

    [!code-cshtml[Main](real-time-web-applications-with-signalr/samples/sample10.cshtml)]

    <span data-ttu-id="513f1-233">在此代码中，所以在创建集线器代理并注册事件处理程序以侦听的服务器发送的消息。</span><span class="sxs-lookup"><span data-stu-id="513f1-233">In this code, you are creating a Hub Proxy and registering an event handler to listen for messages sent by the server.</span></span> <span data-ttu-id="513f1-234">在这种情况下，侦听通过发送的消息*updateStatistics*方法。</span><span class="sxs-lookup"><span data-stu-id="513f1-234">In this case, you listen for messages sent through the *updateStatistics* method.</span></span>

<a id="Ex1Task3"></a>
#### <a name="task-3--running-the-solution"></a><span data-ttu-id="513f1-235">任务 3 – 运行解决方案</span><span class="sxs-lookup"><span data-stu-id="513f1-235">Task 3 – Running the Solution</span></span>

<span data-ttu-id="513f1-236">在本任务中，将运行解决方案，以验证使用回答新问题后 SignalR 自动更新统计信息视图。</span><span class="sxs-lookup"><span data-stu-id="513f1-236">In this task, you will run the solution to verify that the statistics view is updated automatically using SignalR after answering a new question.</span></span>

1. <span data-ttu-id="513f1-237">按**F5**运行该解决方案。</span><span class="sxs-lookup"><span data-stu-id="513f1-237">Press **F5** to run the solution.</span></span>

    > [!NOTE]
    > <span data-ttu-id="513f1-238">如果尚未登录到应用程序，使用在任务 1 中创建的用户登录。</span><span class="sxs-lookup"><span data-stu-id="513f1-238">If not already logged in to the application, log in with the user you created in Task 1.</span></span>
2. <span data-ttu-id="513f1-239">打开**统计信息**页上，在新窗口中，并将放**主页**页并**统计信息**页上的同时，就像在任务 1 中。</span><span class="sxs-lookup"><span data-stu-id="513f1-239">Open the **Statistics** page in a new window and put the **Home** page and **Statistics** page side-by-side as you did in Task 1.</span></span>
3. <span data-ttu-id="513f1-240">在中**主页**页上，通过单击某个选项来回答问题。</span><span class="sxs-lookup"><span data-stu-id="513f1-240">In the **Home** page, answer the question by clicking one of the options.</span></span>

    <span data-ttu-id="513f1-241">![回答另一个问题](real-time-web-applications-with-signalr/_static/image13.png "回答另一个问题")</span><span class="sxs-lookup"><span data-stu-id="513f1-241">![Answering another question](real-time-web-applications-with-signalr/_static/image13.png "Answering another question")</span></span>

    *<span data-ttu-id="513f1-242">回答另一个问题</span><span class="sxs-lookup"><span data-stu-id="513f1-242">Answering another question</span></span>*
4. <span data-ttu-id="513f1-243">单击其中一个按钮后, 应显示答案。</span><span class="sxs-lookup"><span data-stu-id="513f1-243">After clicking one of the buttons, the answer should appear.</span></span> <span data-ttu-id="513f1-244">请注意页面上的统计信息自动更新后回答这个问题，而无需刷新整个页面的更新信息。</span><span class="sxs-lookup"><span data-stu-id="513f1-244">Notice that the Statistics information on the page is updated automatically after answering the question with the updated information without the need to refresh the entire page.</span></span>

    <span data-ttu-id="513f1-245">![在应答后刷新统计信息页面](real-time-web-applications-with-signalr/_static/image14.png "答案后刷新统计信息页面")</span><span class="sxs-lookup"><span data-stu-id="513f1-245">![Statistics page refreshed after answer](real-time-web-applications-with-signalr/_static/image14.png "Statistics page refreshed after answer")</span></span>

    *<span data-ttu-id="513f1-246">刷新后答案的统计信息页</span><span class="sxs-lookup"><span data-stu-id="513f1-246">Statistics page refreshed after answer</span></span>*

<a id="Exercise2"></a>
### <a name="exercise-2-scaling-out-using-sql-server"></a><span data-ttu-id="513f1-247">练习 2:向外扩展使用的 SQL Server</span><span class="sxs-lookup"><span data-stu-id="513f1-247">Exercise 2: Scaling Out Using SQL Server</span></span>

<span data-ttu-id="513f1-248">Web 应用程序时，您通常可以之间*纵向*并*向外扩展*选项。</span><span class="sxs-lookup"><span data-stu-id="513f1-248">When scaling a web application, you can generally choose between *scaling up* and *scaling out* options.</span></span> <span data-ttu-id="513f1-249">*纵向扩展*意味着使用更大的服务器，具有更多的资源 （CPU、 RAM、 等） 时*横向扩展*意味着添加更多服务器来处理负载。</span><span class="sxs-lookup"><span data-stu-id="513f1-249">*Scale up* means using a larger server, with more resources (CPU, RAM, etc.) while *scale out* means adding more servers to handle the load.</span></span> <span data-ttu-id="513f1-250">后者的问题是，可以获取客户端路由到不同的服务器。</span><span class="sxs-lookup"><span data-stu-id="513f1-250">The problem with the latter is that the clients can get routed to different servers.</span></span> <span data-ttu-id="513f1-251">连接到一个服务器的客户端不会收到从另一台服务器发送的消息。</span><span class="sxs-lookup"><span data-stu-id="513f1-251">A client that is connected to one server will not receive messages sent from another server.</span></span>

<span data-ttu-id="513f1-252">通过使用名为的组件来解决这些问题*底板*、 邮件服务器之间进行转发。</span><span class="sxs-lookup"><span data-stu-id="513f1-252">You can solve these issues by using a component called *backplane*, to forward messages between servers.</span></span> <span data-ttu-id="513f1-253">使用启用了基架，每个应用程序实例将消息发送到底板，并底板将其转发到其他应用程序实例。</span><span class="sxs-lookup"><span data-stu-id="513f1-253">With a backplane enabled, each application instance sends messages to the backplane, and the backplane forwards them to the other application instances.</span></span>

<span data-ttu-id="513f1-254">目前有三种类型的 SignalR 的背板：</span><span class="sxs-lookup"><span data-stu-id="513f1-254">There are currently three types of backplanes for SignalR:</span></span>

- <span data-ttu-id="513f1-255">**Windows Azure 服务总线**。</span><span class="sxs-lookup"><span data-stu-id="513f1-255">**Windows Azure Service Bus**.</span></span> <span data-ttu-id="513f1-256">服务总线是允许组件将松散耦合的消息发送的消息传送基础结构。</span><span class="sxs-lookup"><span data-stu-id="513f1-256">Service Bus is a messaging infrastructure that allows components to send loosely coupled messages.</span></span>
- <span data-ttu-id="513f1-257">**SQL Server**。</span><span class="sxs-lookup"><span data-stu-id="513f1-257">**SQL Server**.</span></span> <span data-ttu-id="513f1-258">SQL Server 底板将消息写入 SQL 表。</span><span class="sxs-lookup"><span data-stu-id="513f1-258">The SQL Server backplane writes messages to SQL tables.</span></span> <span data-ttu-id="513f1-259">基架使用 Service Broker 为有效的消息传递。</span><span class="sxs-lookup"><span data-stu-id="513f1-259">The backplane uses Service Broker for efficient messaging.</span></span> <span data-ttu-id="513f1-260">但是，它还适用如果未启用 Service Broker。</span><span class="sxs-lookup"><span data-stu-id="513f1-260">However, it also works if Service Broker is not enabled.</span></span>
- <span data-ttu-id="513f1-261">**Redis**。</span><span class="sxs-lookup"><span data-stu-id="513f1-261">**Redis**.</span></span> <span data-ttu-id="513f1-262">Redis 是内存中键 / 值存储。</span><span class="sxs-lookup"><span data-stu-id="513f1-262">Redis is an in-memory key-value store.</span></span> <span data-ttu-id="513f1-263">Redis 支持发布/订阅 （"发布/订阅"） 模式，用于发送消息。</span><span class="sxs-lookup"><span data-stu-id="513f1-263">Redis supports a publish/subscribe ("pub/sub") pattern for sending messages.</span></span>

<span data-ttu-id="513f1-264">通过消息总线发送每条消息。</span><span class="sxs-lookup"><span data-stu-id="513f1-264">Every message is sent through a message bus.</span></span> <span data-ttu-id="513f1-265">消息总线实现[IMessageBus](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.imessagebus(v=vs.100).aspx)接口，它提供了发布/订阅抽象。</span><span class="sxs-lookup"><span data-stu-id="513f1-265">A message bus implements the [IMessageBus](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.imessagebus(v=vs.100).aspx) interface, which provides a publish/subscribe abstraction.</span></span> <span data-ttu-id="513f1-266">通过替换默认的工作的底板来**IMessageBus**设计为对该底板总线。</span><span class="sxs-lookup"><span data-stu-id="513f1-266">The backplanes work by replacing the default **IMessageBus** with a bus designed for that backplane.</span></span>

<span data-ttu-id="513f1-267">每个服务器实例连接到总线通过基架。</span><span class="sxs-lookup"><span data-stu-id="513f1-267">Each server instance connects to the backplane through the bus.</span></span> <span data-ttu-id="513f1-268">发送一条消息后，转到基架，并底板将其发送到每个服务器。</span><span class="sxs-lookup"><span data-stu-id="513f1-268">When a message is sent, it goes to the backplane, and the backplane sends it to every server.</span></span> <span data-ttu-id="513f1-269">当服务器从底板收到一条消息时，它会将消息存储在其本地缓存中。</span><span class="sxs-lookup"><span data-stu-id="513f1-269">When a server receives a message from the backplane, it stores the message in its local cache.</span></span> <span data-ttu-id="513f1-270">服务器然后将其本地缓存中的消息传送到客户端。</span><span class="sxs-lookup"><span data-stu-id="513f1-270">The server then delivers messages to clients from its local cache.</span></span>

<span data-ttu-id="513f1-271">有关 SignalR 基架的工作原理，阅读此详细信息[一文](../performance/scaleout-in-signalr.md)。</span><span class="sxs-lookup"><span data-stu-id="513f1-271">For more information about how the SignalR backplane works, read this [article](../performance/scaleout-in-signalr.md).</span></span>

> [!NOTE]
> <span data-ttu-id="513f1-272">有某些情况下，其中底板可能成为瓶颈。</span><span class="sxs-lookup"><span data-stu-id="513f1-272">There are some scenarios where a backplane can become a bottleneck.</span></span> <span data-ttu-id="513f1-273">下面是一些典型的 SignalR 方案：</span><span class="sxs-lookup"><span data-stu-id="513f1-273">Here are some typical SignalR scenarios:</span></span>
> 
> - <span data-ttu-id="513f1-274">[服务器广播](tutorial-server-broadcast-with-signalr.md)（例如，股票行情）：背板适合此方案中，因为服务器控制发送消息的速率。</span><span class="sxs-lookup"><span data-stu-id="513f1-274">[Server broadcast](tutorial-server-broadcast-with-signalr.md) (e.g., stock ticker): Backplanes work well for this scenario, because the server controls the rate at which messages are sent.</span></span>
> - <span data-ttu-id="513f1-275">[客户端到客户端](tutorial-getting-started-with-signalr.md)（如聊天）：在此方案中，基架可能如果成为瓶颈的消息数会随着客户端; 的数量也就是说，如果消息的速率增长按比例更多客户端加入。</span><span class="sxs-lookup"><span data-stu-id="513f1-275">[Client-to-client](tutorial-getting-started-with-signalr.md) (e.g., chat): In this scenario, the backplane might be a bottleneck if the number of messages scales with the number of clients; that is, if the rate of messages grows proportionally as more clients join.</span></span>
> - <span data-ttu-id="513f1-276">[高频率实时功能](tutorial-high-frequency-realtime-with-signalr.md)（例如，实时游戏）：基架不建议用于此方案。</span><span class="sxs-lookup"><span data-stu-id="513f1-276">[High-frequency realtime](tutorial-high-frequency-realtime-with-signalr.md) (e.g., real-time games): A backplane is not recommended for this scenario.</span></span>


<span data-ttu-id="513f1-277">在此练习中，您将使用**SQL Server**分发跨消息**极客测验**应用程序。</span><span class="sxs-lookup"><span data-stu-id="513f1-277">In this exercise, you will use **SQL Server** to distribute messages across the **Geek Quiz** application.</span></span> <span data-ttu-id="513f1-278">若要了解如何设置配置，但是，为了获取完整的效果单一测试计算机上运行这些任务，将需要 SignalR 应用程序部署到两个或多个服务器。</span><span class="sxs-lookup"><span data-stu-id="513f1-278">You will run these tasks on a single test machine to learn how to set up the configuration, but in order to get the full effect, you will need to deploy the SignalR application to two or more servers.</span></span> <span data-ttu-id="513f1-279">其中一台服务器，或单独的专用服务器上，还必须安装 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="513f1-279">You must also install SQL Server on one of the servers, or on a separate dedicated server.</span></span>

![向外扩展使用 SQL Server 关系图](real-time-web-applications-with-signalr/_static/image15.png)

<a id="Ex2Task1"></a>
#### <a name="task-1---understanding-the-scenario"></a><span data-ttu-id="513f1-281">任务 1-了解方案</span><span class="sxs-lookup"><span data-stu-id="513f1-281">Task 1 - Understanding the Scenario</span></span>

<span data-ttu-id="513f1-282">在本任务中，你将运行 2 个实例的**极客测验**模拟多个 IIS 实例在本地计算机上。</span><span class="sxs-lookup"><span data-stu-id="513f1-282">In this task, you will run 2 instances of **Geek Quiz** simulating multiple IIS instances on your local machine.</span></span> <span data-ttu-id="513f1-283">在此方案中，回答琐碎内容问题上一个应用程序时，更新不会在第二个实例统计信息页上收到通知。</span><span class="sxs-lookup"><span data-stu-id="513f1-283">In this scenario, when answering trivia questions on one application, update won't be notified on the statistics page of the second instance.</span></span> <span data-ttu-id="513f1-284">此模拟类似于你的应用程序多个实例部署的环境和使用负载均衡器与它们进行通信。</span><span class="sxs-lookup"><span data-stu-id="513f1-284">This simulation resembles an environment where your application is deployed on multiple instances and using a load balancer to communicate with them.</span></span>

1. <span data-ttu-id="513f1-285">打开**Begin.sln**解决方案位于**源/Ex2-ScalingOutWithSQLServer/开始**文件夹。</span><span class="sxs-lookup"><span data-stu-id="513f1-285">Open the **Begin.sln** solution located in the **Source/Ex2-ScalingOutWithSQLServer/Begin** folder.</span></span> <span data-ttu-id="513f1-286">加载后，您会发现上**服务器资源管理器**解决方案有两个项目具有相同结构但不同的名称。</span><span class="sxs-lookup"><span data-stu-id="513f1-286">Once loaded, you will notice on the **Server Explorer** that the solution has two projects with identical structures but different names.</span></span> <span data-ttu-id="513f1-287">这将模拟在本地计算机上运行同一应用程序的两个实例。</span><span class="sxs-lookup"><span data-stu-id="513f1-287">This will simulate running two instances of the same application on your local machine.</span></span>

    <span data-ttu-id="513f1-288">![开始解决方案模拟 2 个实例的极客测验](real-time-web-applications-with-signalr/_static/image16.png "开始模拟极客测验的 2 个实例的解决方案")</span><span class="sxs-lookup"><span data-stu-id="513f1-288">![Begin Solution Simulating 2 Instances of Geek Quiz](real-time-web-applications-with-signalr/_static/image16.png "Begin Solution Simulating 2 Instances of Geek Quiz")</span></span>

    *<span data-ttu-id="513f1-289">开始模拟极客测验的 2 个实例的解决方案</span><span class="sxs-lookup"><span data-stu-id="513f1-289">Begin Solution Simulating 2 Instances of Geek Quiz</span></span>*
2. <span data-ttu-id="513f1-290">打开解决方案的属性页上，右键单击解决方案节点并选择**属性**。</span><span class="sxs-lookup"><span data-stu-id="513f1-290">Open the properties page of the solution by right-clicking the solution node and selecting **Properties**.</span></span> <span data-ttu-id="513f1-291">下**启动项目**，选择**多个启动项目**并更改**操作**到这两个项目的值*启动*。</span><span class="sxs-lookup"><span data-stu-id="513f1-291">Under **Startup Project**, select **Multiple startup projects** and change the **Action** value for both projects to *Start*.</span></span>

    <span data-ttu-id="513f1-292">![启动多个项目](real-time-web-applications-with-signalr/_static/image17.png "启动多个项目")</span><span class="sxs-lookup"><span data-stu-id="513f1-292">![Starting Multiple Projects](real-time-web-applications-with-signalr/_static/image17.png "Starting Multiple Projects")</span></span>

    *<span data-ttu-id="513f1-293">启动多个项目</span><span class="sxs-lookup"><span data-stu-id="513f1-293">Starting Multiple Projects</span></span>*
3. <span data-ttu-id="513f1-294">按**F5**运行该解决方案。</span><span class="sxs-lookup"><span data-stu-id="513f1-294">Press **F5** to run the solution.</span></span> <span data-ttu-id="513f1-295">应用程序将启动的两个实例**极客测验**中不同的端口，模拟相同的应用程序的多个实例。</span><span class="sxs-lookup"><span data-stu-id="513f1-295">The application will launch two instances of **Geek Quiz** in different ports, simulating multiple instances of the same application.</span></span> <span data-ttu-id="513f1-296">将一个固定的左侧和右侧屏幕的其他浏览器。</span><span class="sxs-lookup"><span data-stu-id="513f1-296">Pin one of the browsers on left and the other on the right of your screen.</span></span> <span data-ttu-id="513f1-297">你的凭据进行登录或注册一个新用户。</span><span class="sxs-lookup"><span data-stu-id="513f1-297">Log in with your credentials or register a new user.</span></span> <span data-ttu-id="513f1-298">登录后，在左侧保留琐碎内容页并转到**统计信息**右侧上的浏览器中的页。</span><span class="sxs-lookup"><span data-stu-id="513f1-298">Once logged in, keep the Trivia page on the left and go to the **Statistics** page in the browser on the right.</span></span>

    ![极客测验并排显示](real-time-web-applications-with-signalr/_static/image18.png)

    *<span data-ttu-id="513f1-300">极客测验并排显示</span><span class="sxs-lookup"><span data-stu-id="513f1-300">Geek Quiz Side by Side</span></span>*

    ![在不同的端口的极客测验](real-time-web-applications-with-signalr/_static/image19.png)

    *<span data-ttu-id="513f1-302">在不同的端口的极客测验</span><span class="sxs-lookup"><span data-stu-id="513f1-302">Geek Quiz in Different Ports</span></span>*
4. <span data-ttu-id="513f1-303">左侧浏览器中启动回答的问题，您会注意**统计信息**不更新页面右侧的浏览器中。</span><span class="sxs-lookup"><span data-stu-id="513f1-303">Start answering questions in the left browser and you will notice that the **Statistics** page in the right browser is not being updated.</span></span> <span data-ttu-id="513f1-304">这是因为**SignalR**使用本地缓存，以将消息分配到其客户端和这种情况下可以模拟多个实例，因此它们之间不共享缓存。</span><span class="sxs-lookup"><span data-stu-id="513f1-304">This is because **SignalR** uses a local cache to distribute messages across their clients and this scenario is simulating multiple instances, therefore the cache is not shared between them.</span></span> <span data-ttu-id="513f1-305">你可以验证**SignalR**测试相同的步骤，但使用的单个应用程序是否工作。</span><span class="sxs-lookup"><span data-stu-id="513f1-305">You can verify that **SignalR** is working by testing the same steps but using a single app.</span></span> <span data-ttu-id="513f1-306">在以下任务将配置基架以在实例之间复制消息。</span><span class="sxs-lookup"><span data-stu-id="513f1-306">In the following tasks you will configure a backplane to replicate the messages across instances.</span></span>
5. <span data-ttu-id="513f1-307">返回到 Visual Studio 和停止调试。</span><span class="sxs-lookup"><span data-stu-id="513f1-307">Go back to Visual Studio and stop debugging.</span></span>

<a id="Ex2Task2"></a>
#### <a name="task-2--creating-the-sql-server-backplane"></a><span data-ttu-id="513f1-308">任务 2 – 创建 SQL Server 底板</span><span class="sxs-lookup"><span data-stu-id="513f1-308">Task 2 – Creating the SQL Server Backplane</span></span>

<span data-ttu-id="513f1-309">在此任务中，将创建的数据库，将充当为底板**极客测验**应用程序。</span><span class="sxs-lookup"><span data-stu-id="513f1-309">In this task, you will create a database that will serve as a backplane for the **Geek Quiz** application.</span></span> <span data-ttu-id="513f1-310">将使用**SQL Server 对象资源管理器**浏览你的服务器并初始化该数据库。</span><span class="sxs-lookup"><span data-stu-id="513f1-310">You will use **SQL Server Object Explorer** to browse your server and initialize the database.</span></span> <span data-ttu-id="513f1-311">此外，你将启用**Service Broker**。</span><span class="sxs-lookup"><span data-stu-id="513f1-311">Additionally, you will enable the **Service Broker**.</span></span>

1. <span data-ttu-id="513f1-312">在中**Visual Studio**，打开菜单**视图**，然后选择**SQL Server 对象资源管理器**。</span><span class="sxs-lookup"><span data-stu-id="513f1-312">In **Visual Studio**, open menu **View** and select **SQL Server Object Explorer**.</span></span>
2. <span data-ttu-id="513f1-313">通过右键单击连接到 LocalDB 实例**SQL Server**节点并选择**添加 SQL Server...** 选项。</span><span class="sxs-lookup"><span data-stu-id="513f1-313">Connect to your LocalDB instance by right-clicking the **SQL Server** node and selecting **Add SQL Server...** option.</span></span>

    <span data-ttu-id="513f1-314">![添加 SQL Server 实例](real-time-web-applications-with-signalr/_static/image20.png "添加 SQL Server 实例")</span><span class="sxs-lookup"><span data-stu-id="513f1-314">![Adding a SQL Server Instance](real-time-web-applications-with-signalr/_static/image20.png "Adding a SQL Server Instance")</span></span>

    *<span data-ttu-id="513f1-315">将 SQL Server 实例添加到 SQL Server 对象资源管理器</span><span class="sxs-lookup"><span data-stu-id="513f1-315">Adding a SQL Server instance to SQL Server Object Explorer</span></span>*
3. <span data-ttu-id="513f1-316">设置**服务器名称**到 *(localdb) \v11.0*并保留**Windows 身份验证**作为身份验证模式。</span><span class="sxs-lookup"><span data-stu-id="513f1-316">Set the **server name** to *(localdb)\v11.0* and leave **Windows Authentication** as your authentication mode.</span></span> <span data-ttu-id="513f1-317">单击**Connect**以继续。</span><span class="sxs-lookup"><span data-stu-id="513f1-317">Click **Connect** to continue.</span></span>

    <span data-ttu-id="513f1-318">![连接到 LocalDB](real-time-web-applications-with-signalr/_static/image21.png "连接到 LocalDB")</span><span class="sxs-lookup"><span data-stu-id="513f1-318">![Connecting to LocalDB](real-time-web-applications-with-signalr/_static/image21.png "Connecting to LocalDB")</span></span>

    *<span data-ttu-id="513f1-319">连接到 LocalDB</span><span class="sxs-lookup"><span data-stu-id="513f1-319">Connecting to LocalDB</span></span>*
4. <span data-ttu-id="513f1-320">现在，连接到 LocalDB 实例，需要创建将表示 SQL Server 底板 SignalR 的一个数据库。</span><span class="sxs-lookup"><span data-stu-id="513f1-320">Now that you are connected to your LocalDB instance, you will need to create a database that will represent the SQL Server backplane for SignalR.</span></span> <span data-ttu-id="513f1-321">若要执行此操作，右键单击**数据库**节点，然后选择**添加新的数据库**。</span><span class="sxs-lookup"><span data-stu-id="513f1-321">To do this, right-click the **Databases** node and select **Add New Database**.</span></span>

    <span data-ttu-id="513f1-322">![添加新的数据库](real-time-web-applications-with-signalr/_static/image22.png "添加新的数据库")</span><span class="sxs-lookup"><span data-stu-id="513f1-322">![Adding a new database](real-time-web-applications-with-signalr/_static/image22.png "Adding a new database")</span></span>

    *<span data-ttu-id="513f1-323">添加新的数据库</span><span class="sxs-lookup"><span data-stu-id="513f1-323">Adding a new database</span></span>*
5. <span data-ttu-id="513f1-324">将数据库名称设置为*SignalR*然后单击**确定**来创建它。</span><span class="sxs-lookup"><span data-stu-id="513f1-324">Set the database name to *SignalR* and click **OK** to create it.</span></span>

    <span data-ttu-id="513f1-325">![创建 SignalR 数据库](real-time-web-applications-with-signalr/_static/image23.png "创建 SignalR 数据库")</span><span class="sxs-lookup"><span data-stu-id="513f1-325">![Creating the SignalR database](real-time-web-applications-with-signalr/_static/image23.png "Creating the SignalR database")</span></span>

    *<span data-ttu-id="513f1-326">创建 SignalR 数据库</span><span class="sxs-lookup"><span data-stu-id="513f1-326">Creating the SignalR database</span></span>*

    > [!NOTE]
    > <span data-ttu-id="513f1-327">可以选择数据库的任意名称。</span><span class="sxs-lookup"><span data-stu-id="513f1-327">You can choose any name for the database.</span></span>
6. <span data-ttu-id="513f1-328">若要从底板更有效地接收更新，建议为数据库启用服务中介程序。</span><span class="sxs-lookup"><span data-stu-id="513f1-328">To receive updates more efficiently from the backplane, it is recommended to enable Service Broker for the database.</span></span> <span data-ttu-id="513f1-329">Service Broker 提供了对消息传送和队列在 SQL Server 中的本机支持。</span><span class="sxs-lookup"><span data-stu-id="513f1-329">Service Broker provides native support for messaging and queuing in SQL Server.</span></span> <span data-ttu-id="513f1-330">无需 Service Broker 还正常底板。</span><span class="sxs-lookup"><span data-stu-id="513f1-330">The backplane also works without Service Broker.</span></span> <span data-ttu-id="513f1-331">通过右键单击该数据库并选择打开一个新查询**新查询**。</span><span class="sxs-lookup"><span data-stu-id="513f1-331">Open a new query by right-clicking the database and select **New Query**.</span></span>

    <span data-ttu-id="513f1-332">![打开新查询](real-time-web-applications-with-signalr/_static/image24.png "打开新查询")</span><span class="sxs-lookup"><span data-stu-id="513f1-332">![Opening a New Query](real-time-web-applications-with-signalr/_static/image24.png "Opening a New Query")</span></span>

    *<span data-ttu-id="513f1-333">打开新查询</span><span class="sxs-lookup"><span data-stu-id="513f1-333">Opening a New Query</span></span>*
7. <span data-ttu-id="513f1-334">若要检查是否启用 Service Broker，请查询**是\_broker\_启用**中的列**sys.databases**目录视图。</span><span class="sxs-lookup"><span data-stu-id="513f1-334">To check whether Service Broker is enabled, query the **is\_broker\_enabled** column in the **sys.databases** catalog view.</span></span> <span data-ttu-id="513f1-335">在最近打开的查询窗口中执行以下脚本。</span><span class="sxs-lookup"><span data-stu-id="513f1-335">Execute the following script in the recently opened query window.</span></span>

    [!code-sql[Main](real-time-web-applications-with-signalr/samples/sample11.sql)]

    <span data-ttu-id="513f1-336">![查询服务代理状态](real-time-web-applications-with-signalr/_static/image25.png "查询服务代理状态")</span><span class="sxs-lookup"><span data-stu-id="513f1-336">![Querying the Service Broker Status](real-time-web-applications-with-signalr/_static/image25.png "Querying the Service Broker Status")</span></span>

    *<span data-ttu-id="513f1-337">查询服务代理状态</span><span class="sxs-lookup"><span data-stu-id="513f1-337">Querying the Service Broker Status</span></span>*
8. <span data-ttu-id="513f1-338">如果的值**是\_broker\_启用**您的数据库中的列&quot;0&quot;，使用以下命令来启用它。</span><span class="sxs-lookup"><span data-stu-id="513f1-338">If the value of the **is\_broker\_enabled** column in your database is &quot;0&quot;, use the following command to enable it.</span></span> <span data-ttu-id="513f1-339">替换 **&lt;YOUR DATABASE&gt;** 具有创建数据库时设置的名称 (例如：SignalR)。</span><span class="sxs-lookup"><span data-stu-id="513f1-339">Replace **&lt;YOUR-DATABASE&gt;** with the name you set when creating the database (e.g.: SignalR).</span></span>

    [!code-sql[Main](real-time-web-applications-with-signalr/samples/sample12.sql)]

    <span data-ttu-id="513f1-340">![启用 Service Broker](real-time-web-applications-with-signalr/_static/image26.png "启用 Service Broker")</span><span class="sxs-lookup"><span data-stu-id="513f1-340">![Enabling Service Broker](real-time-web-applications-with-signalr/_static/image26.png "Enabling Service Broker")</span></span>

    *<span data-ttu-id="513f1-341">启用 Service Broker</span><span class="sxs-lookup"><span data-stu-id="513f1-341">Enabling Service Broker</span></span>*

    > [!NOTE]
    > <span data-ttu-id="513f1-342">如果此查询出现死锁，请确保没有应用程序连接到数据库。</span><span class="sxs-lookup"><span data-stu-id="513f1-342">If this query appears to deadlock, make sure there are no applications connected to the DB.</span></span>

<a id="Ex2Task3"></a>
#### <a name="task-3--configuring-the-signalr-application"></a><span data-ttu-id="513f1-343">任务 3 – 配置 SignalR 应用程序</span><span class="sxs-lookup"><span data-stu-id="513f1-343">Task 3 – Configuring the SignalR Application</span></span>

<span data-ttu-id="513f1-344">在本任务中，您将配置**极客测验**连接到 SQL Server 背板。</span><span class="sxs-lookup"><span data-stu-id="513f1-344">In this task, you will configure **Geek Quiz** to connect to the SQL Server backplane.</span></span> <span data-ttu-id="513f1-345">首先，您将添加**SignalR.SqlServer** NuGet 包并设置的连接字符串到底板数据库。</span><span class="sxs-lookup"><span data-stu-id="513f1-345">You will first add the **SignalR.SqlServer** NuGet package and set the connection string to your backplane database.</span></span>

1. <span data-ttu-id="513f1-346">打开**程序包管理器控制台**从**工具** > **NuGet 包管理器**。</span><span class="sxs-lookup"><span data-stu-id="513f1-346">Open the **Package Manager Console** from **Tools** > **NuGet Package Manager**.</span></span> <span data-ttu-id="513f1-347">请确保**GeekQuiz**中选择项目**默认项目**下拉列表。</span><span class="sxs-lookup"><span data-stu-id="513f1-347">Make sure that **GeekQuiz** project is selected in the **Default project** drop-down list.</span></span> <span data-ttu-id="513f1-348">键入以下命令以安装**Microsoft.AspNet.SignalR.SqlServer** NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="513f1-348">Type the following command to install the **Microsoft.AspNet.SignalR.SqlServer** NuGet package.</span></span>

    [!code-powershell[Main](real-time-web-applications-with-signalr/samples/sample13.ps1)]
2. <span data-ttu-id="513f1-349">对项目重复上一步，但这一次**GeekQuiz2**。</span><span class="sxs-lookup"><span data-stu-id="513f1-349">Repeat the previous step but this time for project **GeekQuiz2**.</span></span>
3. <span data-ttu-id="513f1-350">若要配置 SQL Server 基架，请打开**Startup.cs**的文件**GeekQuiz**项目，然后将以下代码添加到**配置**方法。</span><span class="sxs-lookup"><span data-stu-id="513f1-350">To configure the SQL Server backplane, open the **Startup.cs** file of the **GeekQuiz** project and add the following code to the **Configure** method.</span></span> <span data-ttu-id="513f1-351">替换 **&lt;YOUR DATABASE&gt;** 与你创建 SQL Server 底板时所用的数据库名称。</span><span class="sxs-lookup"><span data-stu-id="513f1-351">Replace **&lt;YOUR-DATABASE&gt;** with your database name you used when creating the SQL Server backplane.</span></span> <span data-ttu-id="513f1-352">重复此步骤对于**GeekQuiz2**项目。</span><span class="sxs-lookup"><span data-stu-id="513f1-352">Repeat this step for the **GeekQuiz2** project.</span></span>

    <span data-ttu-id="513f1-353">(代码段- *RealTimeSignalR-Ex2-StartupConfiguration*)</span><span class="sxs-lookup"><span data-stu-id="513f1-353">(Code Snippet - *RealTimeSignalR - Ex2 - StartupConfiguration*)</span></span>

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample14.cs)]
4. <span data-ttu-id="513f1-354">现在，这两个项目配置为使用 SQL Server 底板，按**F5**同时运行它们。</span><span class="sxs-lookup"><span data-stu-id="513f1-354">Now that both projects are configured to use the SQL Server backplane, press **F5** to run them simultaneously.</span></span>
5. <span data-ttu-id="513f1-355">同样， **Visual Studio**将启动的两个实例**极客测验**中不同的端口。</span><span class="sxs-lookup"><span data-stu-id="513f1-355">Again, **Visual Studio** will launch two instances of **Geek Quiz** in different ports.</span></span> <span data-ttu-id="513f1-356">将一个浏览器固定到左侧和右侧屏幕的其他和您的凭据进行登录。</span><span class="sxs-lookup"><span data-stu-id="513f1-356">Pin one of the browsers on the left and the other on the right of your screen and log in with your credentials.</span></span> <span data-ttu-id="513f1-357">在左侧保留琐碎内容页并转到**统计信息**页面调入正确的浏览器。</span><span class="sxs-lookup"><span data-stu-id="513f1-357">Keep the Trivia page on the left and go to **Statistics** pagein the right browser.</span></span>
6. <span data-ttu-id="513f1-358">开始回答问题在左侧浏览器中。</span><span class="sxs-lookup"><span data-stu-id="513f1-358">Start answering questions in the left browser.</span></span> <span data-ttu-id="513f1-359">这一次，**统计信息**得益于底板更新页面。</span><span class="sxs-lookup"><span data-stu-id="513f1-359">This time, the **Statistics** page is updated thanks to the backplane.</span></span> <span data-ttu-id="513f1-360">应用程序之间切换 (**统计信息**现已在左侧，并**琐碎内容**位于右侧) 和重复执行测试以验证它是否正常工作的两个实例。</span><span class="sxs-lookup"><span data-stu-id="513f1-360">Switch between applications (**Statistics** is now on the left, and **Trivia** is on the right) and repeat the test to validate that it is working for both instances.</span></span> <span data-ttu-id="513f1-361">底板充当*共享缓存*的消息的每个连接的服务器，且每个服务器会将消息存储在其自己的本地缓存要分发到连接的客户端中。</span><span class="sxs-lookup"><span data-stu-id="513f1-361">The backplane serves as a *shared cache* of messages for each connected server, and each server will store the messages in their own local cache to distribute to connected clients.</span></span>
7. <span data-ttu-id="513f1-362">返回到 Visual Studio 和停止调试。</span><span class="sxs-lookup"><span data-stu-id="513f1-362">Go back to Visual Studio and stop debugging.</span></span>
8. <span data-ttu-id="513f1-363">SQL Server 底板组件会自动生成上指定的数据库所需的表。</span><span class="sxs-lookup"><span data-stu-id="513f1-363">The SQL Server backplane component automatically generates the necessary tables on the specified database.</span></span> <span data-ttu-id="513f1-364">在中**SQL Server 对象资源管理器**面板中，打开为基架创建的数据库 (例如：SignalR) 展开其表。</span><span class="sxs-lookup"><span data-stu-id="513f1-364">In the **SQL Server Object Explorer** panel, open the database you created for the backplane (e.g.: SignalR) and expand its tables.</span></span> <span data-ttu-id="513f1-365">你应该会看到以下表：</span><span class="sxs-lookup"><span data-stu-id="513f1-365">You should see the following tables:</span></span>

    ![基架生成的表](real-time-web-applications-with-signalr/_static/image27.png)

    *<span data-ttu-id="513f1-367">基架生成的表</span><span class="sxs-lookup"><span data-stu-id="513f1-367">Backplane Generated Tables</span></span>*
9. <span data-ttu-id="513f1-368">右键单击**SignalR.Messages\_0**表，然后选择**查看数据**。</span><span class="sxs-lookup"><span data-stu-id="513f1-368">Right-click the **SignalR.Messages\_0** table and select **View Data**.</span></span>

    ![查看 SignalR 基架消息表](real-time-web-applications-with-signalr/_static/image28.png)

    *<span data-ttu-id="513f1-370">查看 SignalR 基架消息表</span><span class="sxs-lookup"><span data-stu-id="513f1-370">View SignalR Backplane Messages Table</span></span>*
10. <span data-ttu-id="513f1-371">可以看到不同的消息发送到**中心**回答琐碎内容问题时。</span><span class="sxs-lookup"><span data-stu-id="513f1-371">You can see the different messages sent to the **Hub** when answering the trivia questions.</span></span> <span data-ttu-id="513f1-372">底板这些将消息分发到已连接的任何实例。</span><span class="sxs-lookup"><span data-stu-id="513f1-372">The backplane distributes these messages to any connected instance.</span></span>

    ![底板消息表](real-time-web-applications-with-signalr/_static/image29.png)

    *<span data-ttu-id="513f1-374">底板消息表</span><span class="sxs-lookup"><span data-stu-id="513f1-374">Backplane Messages Table</span></span>*

---

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="513f1-375">总结</span><span class="sxs-lookup"><span data-stu-id="513f1-375">Summary</span></span>

<span data-ttu-id="513f1-376">在本动手实验，您已了解如何添加**SignalR**在应用程序和发送通知从服务器到使用您连接的客户端**中心**。</span><span class="sxs-lookup"><span data-stu-id="513f1-376">In this hands-on lab, you have learned how to add **SignalR** to your application and send notifications from the server to your connected clients using **Hubs**.</span></span> <span data-ttu-id="513f1-377">此外，您学习了如何通过使用横向扩展你的应用程序*底板*组件时你的应用程序部署在多个 IIS 实例。</span><span class="sxs-lookup"><span data-stu-id="513f1-377">Additionally, you learned how to scale out your application by using a *backplane* component when your application is deployed in multiple IIS instances.</span></span>

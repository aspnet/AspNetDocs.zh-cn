---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/the-fix-it-sample-application
title: 附录： Fix It 示例应用程序 (用 Azure) 生成 Real-World 云应用 |Microsoft Docs
author: MikeWasson
description: 使用 Azure 电子书构建真实的云应用基于 Scott Guthrie 开发的演示文稿。 它介绍了13种模式和实践，
ms.author: riande
ms.date: 06/12/2014
ms.assetid: 1bc333c5-f096-4ea7-b170-779accc21c1a
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/the-fix-it-sample-application
msc.type: authoredcontent
ms.openlocfilehash: 53ae9633277b38f1d2c8a8bd43eaf0014da54c45
ms.sourcegitcommit: 4b78855427f1397df0a7be3559e04ec94a78c308
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/25/2020
ms.locfileid: "96151875"
---
# <a name="appendix-the-fix-it-sample-application-building-real-world-cloud-apps-with-azure"></a><span data-ttu-id="d5bff-104">附录： Fix It 示例应用程序 (用 Azure) 生成 Real-World 云应用</span><span class="sxs-lookup"><span data-stu-id="d5bff-104">Appendix: The Fix It Sample Application (Building Real-World Cloud Apps with Azure)</span></span>

<span data-ttu-id="d5bff-105">作者： [Mike Wasson](https://github.com/MikeWasson)， [Rick Anderson](https://twitter.com/RickAndMSFT)， [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="d5bff-105">by [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson](https://twitter.com/RickAndMSFT), [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="d5bff-106">下载 Fix It 项目</span><span class="sxs-lookup"><span data-stu-id="d5bff-106">Download The Fix It Project</span></span>](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)

> <span data-ttu-id="d5bff-107">**使用 Azure 电子书构建真实的云应用** 基于 Scott Guthrie 开发的演示文稿。</span><span class="sxs-lookup"><span data-stu-id="d5bff-107">The **Building Real World Cloud Apps with Azure** e-book is based on a presentation developed by Scott Guthrie.</span></span> <span data-ttu-id="d5bff-108">它介绍了可帮助你成功开发云的 web 应用的13种模式和实践。</span><span class="sxs-lookup"><span data-stu-id="d5bff-108">It explains 13 patterns and practices that can help you be successful developing web apps for the cloud.</span></span> <span data-ttu-id="d5bff-109">有关电子书的信息，请参阅 [第一章](introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="d5bff-109">For information about the e-book, see [the first chapter](introduction.md).</span></span>

<span data-ttu-id="d5bff-110">本附录介绍了如何通过 Azure 电子书构建实际的云应用程序，其中包含了有关可以下载的 Fix It 示例应用程序的其他信息：</span><span class="sxs-lookup"><span data-stu-id="d5bff-110">This appendix to the Building Real World Cloud Apps with Azure e-book contains the following sections that provide additional information about the Fix It sample application that you can download:</span></span>

- [<span data-ttu-id="d5bff-111">已知问题</span><span class="sxs-lookup"><span data-stu-id="d5bff-111">Known issues</span></span>](#knownissues)
- [<span data-ttu-id="d5bff-112">最佳实践</span><span class="sxs-lookup"><span data-stu-id="d5bff-112">Best practices</span></span>](#bestpractices)
- [<span data-ttu-id="d5bff-113">如何在本地计算机上从 Visual Studio 运行应用</span><span class="sxs-lookup"><span data-stu-id="d5bff-113">How to run the app from Visual Studio on your local computer</span></span>](#run-in-vs)
- [<span data-ttu-id="d5bff-114">如何使用 Windows PowerShell 脚本将基本应用部署到 Azure App Service Web 应用</span><span class="sxs-lookup"><span data-stu-id="d5bff-114">How to deploy the base app to Azure App Service Web Apps by using the Windows PowerShell scripts</span></span>](#deploybase)
- [<span data-ttu-id="d5bff-115">Windows PowerShell 脚本疑难解答</span><span class="sxs-lookup"><span data-stu-id="d5bff-115">Troubleshooting the Windows PowerShell scripts</span></span>](#troubleshooting)
- [<span data-ttu-id="d5bff-116">如何将具有队列处理的应用部署到 Azure App Service Web 应用和 Azure 云服务</span><span class="sxs-lookup"><span data-stu-id="d5bff-116">How to deploy the app with queue processing to Azure App Service Web Apps and an Azure Cloud Service</span></span>](#deployqueues)

<a id="knownissues"></a>
## <a name="known-issues"></a><span data-ttu-id="d5bff-117">已知问题</span><span class="sxs-lookup"><span data-stu-id="d5bff-117">Known issues</span></span>

<span data-ttu-id="d5bff-118">最初开发 Fix It 应用程序是为了尽可能简单地说明此电子书中介绍的一些模式。</span><span class="sxs-lookup"><span data-stu-id="d5bff-118">The Fix It app was originally developed in order to illustrate as simply as possible some of the patterns presented in this e-book.</span></span> <span data-ttu-id="d5bff-119">不过，由于电子书就是构建真实的应用程序，因此我们将修复它的代码放在评审和测试过程中，就像我们对发布的软件执行的操作一样。</span><span class="sxs-lookup"><span data-stu-id="d5bff-119">However, since the e-book is about building real-world apps, we subjected the Fix It code to a review and testing process similar to what we'd do for released software.</span></span> <span data-ttu-id="d5bff-120">我们发现了很多问题，与任何实际应用程序一样，其中一些问题已修复，其中一些问题已推迟到更高版本。</span><span class="sxs-lookup"><span data-stu-id="d5bff-120">We found a number of issues, and as with any real-world application, some of them we fixed and some of them we deferred to a later release.</span></span>

<span data-ttu-id="d5bff-121">下面的列表包含应在生产应用程序中解决的问题，但出于某种原因或者我们决定不在 Fix It 示例应用程序的初始版本中解决。</span><span class="sxs-lookup"><span data-stu-id="d5bff-121">The following list includes issues that should be addressed in a production application, but for one reason or another we decided not to address in the initial release of the Fix It sample application.</span></span>

### <a name="security"></a><span data-ttu-id="d5bff-122">安全性</span><span class="sxs-lookup"><span data-stu-id="d5bff-122">Security</span></span>

- <span data-ttu-id="d5bff-123">请确保不能向不存在的所有者分配任务。</span><span class="sxs-lookup"><span data-stu-id="d5bff-123">Ensure that you can't assign a task to a non-existent owner.</span></span>
- <span data-ttu-id="d5bff-124">确保您只能查看和修改您创建或分配给您的任务。</span><span class="sxs-lookup"><span data-stu-id="d5bff-124">Ensure that you can only view and modify tasks that you created or are assigned to you.</span></span>
- <span data-ttu-id="d5bff-125">将 HTTPS 用于登录页和身份验证 cookie。</span><span class="sxs-lookup"><span data-stu-id="d5bff-125">Use HTTPS for sign-in pages and authentication cookies.</span></span>
- <span data-ttu-id="d5bff-126">指定身份验证 cookie 的时间限制。</span><span class="sxs-lookup"><span data-stu-id="d5bff-126">Specify a time limit for authentication cookies.</span></span>

### <a name="input-validation"></a><span data-ttu-id="d5bff-127">输入验证</span><span class="sxs-lookup"><span data-stu-id="d5bff-127">Input validation</span></span>

<span data-ttu-id="d5bff-128">通常，生产应用执行的输入验证比 Fix It 应用要多。</span><span class="sxs-lookup"><span data-stu-id="d5bff-128">In general, a production app would do more input validation than the Fix It app.</span></span> <span data-ttu-id="d5bff-129">例如，允许上传的图像大小/图像文件大小应受限。</span><span class="sxs-lookup"><span data-stu-id="d5bff-129">For example, the image size / image file size allowed for upload should be limited.</span></span>

### <a name="administrator-functionality"></a><span data-ttu-id="d5bff-130">管理员功能</span><span class="sxs-lookup"><span data-stu-id="d5bff-130">Administrator functionality</span></span>

<span data-ttu-id="d5bff-131">管理员应该能够更改现有任务的所有权。</span><span class="sxs-lookup"><span data-stu-id="d5bff-131">An administrator should be able to change ownership on existing tasks.</span></span> <span data-ttu-id="d5bff-132">例如，如果启用了管理访问权限，则任务的创建者可能会离开公司，而不会有权维护该任务。</span><span class="sxs-lookup"><span data-stu-id="d5bff-132">For example, the creator of a task might leave the company, leaving no one with authority to maintain the task unless administrative access is enabled.</span></span>

### <a name="queue-message-processing"></a><span data-ttu-id="d5bff-133">队列消息处理</span><span class="sxs-lookup"><span data-stu-id="d5bff-133">Queue message processing</span></span>

<span data-ttu-id="d5bff-134">Fix It 应用中的队列消息处理设计为非常简单，以便以最少的代码说明以队列为中心的工作模式。</span><span class="sxs-lookup"><span data-stu-id="d5bff-134">Queue message processing in the Fix It app was designed to be simple in order to illustrate the queue-centric work pattern with a minimum amount of code.</span></span> <span data-ttu-id="d5bff-135">对于实际的生产应用程序而言，这种简单的代码将不能满足需要。</span><span class="sxs-lookup"><span data-stu-id="d5bff-135">This simple code would not be adequate for an actual production application.</span></span>

- <span data-ttu-id="d5bff-136">此代码不保证每个队列消息将最多处理一次。</span><span class="sxs-lookup"><span data-stu-id="d5bff-136">The code does not guarantee that each queue message will be processed at most once.</span></span> <span data-ttu-id="d5bff-137">当你从队列中获取消息时，有一个超时期限，在此期间，消息对其他队列侦听器不可见。</span><span class="sxs-lookup"><span data-stu-id="d5bff-137">When you get a message from the queue, there is a timeout period, during which the message is invisible to other queue listeners.</span></span> <span data-ttu-id="d5bff-138">如果在删除消息之前超时过期，则该消息将再次变为可见。</span><span class="sxs-lookup"><span data-stu-id="d5bff-138">If the timeout expires before the message is deleted, the message becomes visible again.</span></span> <span data-ttu-id="d5bff-139">因此，如果辅助角色实例花费很长时间来处理消息，则理论上可能会将同一消息处理两次，从而导致数据库中出现重复的任务。</span><span class="sxs-lookup"><span data-stu-id="d5bff-139">Therefore, if a worker role instance spends a long time processing a message, it is theoretically possible for the same message to get processed twice, resulting in a duplicate task in the database.</span></span> <span data-ttu-id="d5bff-140">有关此问题的详细信息，请参阅 [使用 Azure 存储队列](https://msdn.microsoft.com/library/ff803365.aspx#sec7)。</span><span class="sxs-lookup"><span data-stu-id="d5bff-140">For more information about this issue, see [Using Azure Storage Queues](https://msdn.microsoft.com/library/ff803365.aspx#sec7).</span></span>
- <span data-ttu-id="d5bff-141">通过批处理消息检索，队列轮询逻辑可能更具成本效益。</span><span class="sxs-lookup"><span data-stu-id="d5bff-141">The queue polling logic could be more cost-effective, by batching message retrieval.</span></span> <span data-ttu-id="d5bff-142">每次调用 [CloudQueue GetMessageAsync](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.getmessageasync.aspx)时，都会产生事务成本。</span><span class="sxs-lookup"><span data-stu-id="d5bff-142">Every time you call [CloudQueue.GetMessageAsync](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.getmessageasync.aspx), there is a transaction cost.</span></span> <span data-ttu-id="d5bff-143">相反，你可以调用 [CloudQueue. GetMessagesAsync](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.getmessagesasync.aspx) (记下复数的 ") ，这将在单个事务中获取多个消息。</span><span class="sxs-lookup"><span data-stu-id="d5bff-143">Instead, you can call [CloudQueue.GetMessagesAsync](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.getmessagesasync.aspx) (note the plural 's'), which gets multiple messages in a single transaction.</span></span> <span data-ttu-id="d5bff-144">Azure 存储队列的事务成本非常低，因此，对成本的影响在大多数情况下并不明显。</span><span class="sxs-lookup"><span data-stu-id="d5bff-144">The transaction costs for Azure Storage Queues are very low, so the impact on costs is not substantial in most scenarios.</span></span>
- <span data-ttu-id="d5bff-145">队列消息处理代码中的紧密循环导致 CPU 关联，这不会有效地利用多核 Vm。</span><span class="sxs-lookup"><span data-stu-id="d5bff-145">The tight loop in the queue message-processing code causes CPU affinity, which does not utilize multi-core VMs efficiently.</span></span> <span data-ttu-id="d5bff-146">更好的设计会使用任务并行并行运行多个异步任务。</span><span class="sxs-lookup"><span data-stu-id="d5bff-146">A better design would use task parallelism to run several async tasks in parallel.</span></span>
- <span data-ttu-id="d5bff-147">队列消息处理只包含基本异常处理。</span><span class="sxs-lookup"><span data-stu-id="d5bff-147">Queue message-processing has only rudimentary exception handling.</span></span> <span data-ttu-id="d5bff-148">例如，代码不处理 [病毒消息](https://msdn.microsoft.com/library/ms789028.aspx)。</span><span class="sxs-lookup"><span data-stu-id="d5bff-148">For example, the code doesn't handle [poison messages](https://msdn.microsoft.com/library/ms789028.aspx).</span></span> <span data-ttu-id="d5bff-149"> (当消息处理导致异常时，您必须记录错误并删除消息，否则辅助角色将尝试再次处理该消息，并且循环会无限期地继续。 ) </span><span class="sxs-lookup"><span data-stu-id="d5bff-149">(When message processing causes an exception, you have to log the error and delete the message, or the worker role will try to process it again, and the loop will continue indefinitely.)</span></span>

### <a name="sql-queries-are-unbounded"></a><span data-ttu-id="d5bff-150">未绑定 SQL 查询</span><span class="sxs-lookup"><span data-stu-id="d5bff-150">SQL queries are unbounded</span></span>

<span data-ttu-id="d5bff-151">当前 Fix It 代码对索引页的查询可能返回的行数没有限制。</span><span class="sxs-lookup"><span data-stu-id="d5bff-151">Current Fix It code places no limit on how many rows the queries for Index pages might return.</span></span> <span data-ttu-id="d5bff-152">如果将大量任务输入到数据库中，则收到的结果列表的大小可能会导致性能问题。</span><span class="sxs-lookup"><span data-stu-id="d5bff-152">If a large volume of tasks is entered into the database, the size of the resulting lists received could cause performance issues.</span></span> <span data-ttu-id="d5bff-153">解决方案是实现分页。</span><span class="sxs-lookup"><span data-stu-id="d5bff-153">The solution is to implement paging.</span></span> <span data-ttu-id="d5bff-154">有关示例，请参阅 [使用 ASP.NET MVC 应用程序中的实体框架进行排序、筛选和分页](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md)。</span><span class="sxs-lookup"><span data-stu-id="d5bff-154">For an example, see [Sorting, Filtering, and Paging with the Entity Framework in an ASP.NET MVC Application](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md).</span></span>

### <a name="view-models-recommended"></a><span data-ttu-id="d5bff-155">建议查看模型</span><span class="sxs-lookup"><span data-stu-id="d5bff-155">View models recommended</span></span>

<span data-ttu-id="d5bff-156">Fix It 应用使用 FixItTask 实体类在控制器和视图之间传递信息。</span><span class="sxs-lookup"><span data-stu-id="d5bff-156">The Fix It app uses the FixItTask entity class to pass information between the controller and the view.</span></span> <span data-ttu-id="d5bff-157">最佳做法是使用视图模型。</span><span class="sxs-lookup"><span data-stu-id="d5bff-157">A best practice is to use view models.</span></span> <span data-ttu-id="d5bff-158">域模型 (例如，FixItTask 实体类) 是围绕数据持久性所需要的内容设计的，而视图模型可用于数据显示。</span><span class="sxs-lookup"><span data-stu-id="d5bff-158">The domain model (e.g., the FixItTask entity class) is designed around what is needed for data persistence, while a view model can be designed for data presentation.</span></span> <span data-ttu-id="d5bff-159">有关详细信息，请参阅 [12 ASP.NET MVC 最佳实践](https://codeclimber.net.nz/archive/2009/10/27/12-asp.net-mvc-best-practices.aspx)。</span><span class="sxs-lookup"><span data-stu-id="d5bff-159">For more information, see [12 ASP.NET MVC Best Practices](https://codeclimber.net.nz/archive/2009/10/27/12-asp.net-mvc-best-practices.aspx).</span></span>

### <a name="secure-image-blob-recommended"></a><span data-ttu-id="d5bff-160">建议使用安全图像 blob</span><span class="sxs-lookup"><span data-stu-id="d5bff-160">Secure image blob recommended</span></span>

<span data-ttu-id="d5bff-161">Fix It 应用将上传的图像存储为公用，这意味着查找 URL 的任何人都可以访问这些图像。</span><span class="sxs-lookup"><span data-stu-id="d5bff-161">The Fix It app stores uploaded images as public, meaning that anyone who finds the URL can access the images.</span></span> <span data-ttu-id="d5bff-162">图像可以是安全的，而不是公共的。</span><span class="sxs-lookup"><span data-stu-id="d5bff-162">The images could be secured instead of public.</span></span>

### <a name="no-powershell-automation-scripts-for-queues"></a><span data-ttu-id="d5bff-163">没有用于队列的 PowerShell 自动化脚本</span><span class="sxs-lookup"><span data-stu-id="d5bff-163">No PowerShell automation scripts for queues</span></span>

<span data-ttu-id="d5bff-164">示例 PowerShell 自动化脚本只是为完全在 Azure App Service Web 应用中运行的基本版本的修补程序编写的。</span><span class="sxs-lookup"><span data-stu-id="d5bff-164">Sample PowerShell automation scripts were written only for the base version of Fix It that runs entirely in Azure App Service Web Apps.</span></span> <span data-ttu-id="d5bff-165">我们尚未提供用于设置和部署到 web 应用的脚本，以及队列处理所需的云服务环境。</span><span class="sxs-lookup"><span data-stu-id="d5bff-165">We haven't provided scripts for setting up and deploying to the web app plus Cloud Service environment required for queue processing.</span></span>

### <a name="special-handling-for-html-codes-in-user-input"></a><span data-ttu-id="d5bff-166">用户输入中 HTML 代码的特殊处理</span><span class="sxs-lookup"><span data-stu-id="d5bff-166">Special handling for HTML codes in user input</span></span>

<span data-ttu-id="d5bff-167">ASP.NET 通过在 "用户输入" 文本框中输入 script，来自动防止恶意用户可能尝试跨站点脚本攻击的多种方式。</span><span class="sxs-lookup"><span data-stu-id="d5bff-167">ASP.NET automatically prevents many ways in which malicious users might attempt cross-site scripting attacks by entering script in user input text boxes.</span></span> <span data-ttu-id="d5bff-168">`DisplayFor`用于显示任务标题和备注的 MVC 帮助器会自动对其发送到浏览器的值进行 HTML 编码。</span><span class="sxs-lookup"><span data-stu-id="d5bff-168">And the MVC `DisplayFor` helper used to display task titles and notes automatically HTML-encodes values that it sends to the browser.</span></span> <span data-ttu-id="d5bff-169">但在生产应用程序中，你可能需要采取其他措施。</span><span class="sxs-lookup"><span data-stu-id="d5bff-169">But in a production app you might want to take additional measures.</span></span> <span data-ttu-id="d5bff-170">有关详细信息，请参阅 [ASP.NET 中的请求验证](https://msdn.microsoft.com/library/hh882339.aspx)。</span><span class="sxs-lookup"><span data-stu-id="d5bff-170">For more information, see [Request Validation in ASP.NET](https://msdn.microsoft.com/library/hh882339.aspx).</span></span>

<a id="bestpractices"></a>
## <a name="best-practices"></a><span data-ttu-id="d5bff-171">最佳实践</span><span class="sxs-lookup"><span data-stu-id="d5bff-171">Best practices</span></span>

<span data-ttu-id="d5bff-172">下面是在代码评审和测试 Fix It 应用程序的原始版本中发现后修复的一些问题。</span><span class="sxs-lookup"><span data-stu-id="d5bff-172">Following are some issues that were fixed after being discovered in code review and testing of the original version of the Fix It app.</span></span> <span data-ttu-id="d5bff-173">其中一些原因是最初的编码员无法识别特定的最佳实践，只是因为代码是快速编写的，而不是用于发布的软件。</span><span class="sxs-lookup"><span data-stu-id="d5bff-173">Some were caused by the original coder not being aware of a particular best practice, some simply because the code was written quickly and wasn't intended for released software.</span></span> <span data-ttu-id="d5bff-174">我们将在此处列出问题，因为我们在此审查和测试中了解到的内容可能对也正在开发 web 应用的其他人员有所帮助。</span><span class="sxs-lookup"><span data-stu-id="d5bff-174">We're listing the issues here in case there's something we learned from this review and testing that might be helpful to others who are also developing web apps.</span></span>

### <a name="dispose-the-database-repository"></a><span data-ttu-id="d5bff-175">释放数据库存储库</span><span class="sxs-lookup"><span data-stu-id="d5bff-175">Dispose the database repository</span></span>

<span data-ttu-id="d5bff-176">`FixItTaskRepository`类必须释放实体框架 `DbContext` 实例。</span><span class="sxs-lookup"><span data-stu-id="d5bff-176">The `FixItTaskRepository` class must dispose the Entity Framework `DbContext` instance.</span></span> <span data-ttu-id="d5bff-177">为此，我们 `IDisposable` 在类中实现 `FixItTaskRepository` ：</span><span class="sxs-lookup"><span data-stu-id="d5bff-177">We did this by implementing `IDisposable` in the `FixItTaskRepository` class:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample1.cs)]

<span data-ttu-id="d5bff-178">请注意，AutoFac 将自动释放该 `FixItTaskRepository` 实例，因此我们不需要显式释放它。</span><span class="sxs-lookup"><span data-stu-id="d5bff-178">Note that AutoFac will automatically dispose the `FixItTaskRepository` instance, so we don't need to explicitly dispose it.</span></span>

<span data-ttu-id="d5bff-179">另一种方法是从中移除 `DbContext` 成员变量 `FixItTaskRepository` ，而在 `DbContext` 语句内的每个存储库方法中创建一个本地变量 `using` 。</span><span class="sxs-lookup"><span data-stu-id="d5bff-179">Another option is to remove the `DbContext` member variable from `FixItTaskRepository`, and instead create a local `DbContext` variable within each repository method, inside a `using` statement.</span></span> <span data-ttu-id="d5bff-180">例如：</span><span class="sxs-lookup"><span data-stu-id="d5bff-180">For example:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample2.cs)]

### <a name="register-singletons-as-such-with-di"></a><span data-ttu-id="d5bff-181">用 DI 注册单一实例</span><span class="sxs-lookup"><span data-stu-id="d5bff-181">Register singletons as such with DI</span></span>

<span data-ttu-id="d5bff-182">由于只 `PhotoService` 需要类和类的一个实例 `Logger` ，因此应将这些类注册为 *DependenciesConfig.cs* 中 [的依赖项注入的单一实例](https://code.google.com/p/autofac/wiki/InstanceScope)：</span><span class="sxs-lookup"><span data-stu-id="d5bff-182">Since only one instance of the `PhotoService` class and `Logger` class is needed, these classes should be [registered as single instances for dependency injection](https://code.google.com/p/autofac/wiki/InstanceScope) in *DependenciesConfig.cs*:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample3.cs?highlight=1,3)]

### <a name="security-dont-show-error-details-to-users"></a><span data-ttu-id="d5bff-183">安全性：不向用户显示错误详细信息</span><span class="sxs-lookup"><span data-stu-id="d5bff-183">Security: Don't show error details to users</span></span>

<span data-ttu-id="d5bff-184">原始的 Fix It 应用没有通用错误页，只是让所有异常向上冒泡到 UI，因此某些异常（如数据库连接错误）可能会导致在浏览器中显示完整的堆栈跟踪。</span><span class="sxs-lookup"><span data-stu-id="d5bff-184">The original Fix It app didn't have a generic error page and just let all exceptions bubble up to the UI, so some exceptions such as database connection errors could result in a full stack trace being displayed to the browser.</span></span> <span data-ttu-id="d5bff-185">详细的错误信息有时会有助于恶意用户的攻击。</span><span class="sxs-lookup"><span data-stu-id="d5bff-185">Detailed error information can sometimes facilitate attacks by malicious users.</span></span> <span data-ttu-id="d5bff-186">解决方案是记录异常详细信息，并向用户显示不包含错误详细信息的错误页。</span><span class="sxs-lookup"><span data-stu-id="d5bff-186">The solution is to log the exception details and display an error page to the user that doesn't include error details.</span></span> <span data-ttu-id="d5bff-187">Fix It 应用已经记录了日志，为了显示错误页面，我们添加到 `<customErrors mode=On>` 了 Web.config 文件中。</span><span class="sxs-lookup"><span data-stu-id="d5bff-187">The Fix It app was already logging, and in order to display an error page, we added `<customErrors mode=On>` in the Web.config file.</span></span>

[!code-xml[Main](the-fix-it-sample-application/samples/sample4.xml?highlight=2)]

<span data-ttu-id="d5bff-188">默认情况下，这会导致 *Views\Shared\Error.cshtml* 显示错误。</span><span class="sxs-lookup"><span data-stu-id="d5bff-188">By default this causes *Views\Shared\Error.cshtml* to be displayed for errors.</span></span> <span data-ttu-id="d5bff-189">你可以自定义 *错误* ，或创建你自己的错误页面视图并添加 `defaultRedirect` 属性。</span><span class="sxs-lookup"><span data-stu-id="d5bff-189">You can customize *Error.cshtml* or create your own error page view and add a `defaultRedirect` attribute.</span></span> <span data-ttu-id="d5bff-190">还可以为特定错误指定不同的错误页。</span><span class="sxs-lookup"><span data-stu-id="d5bff-190">You can also specify different error pages for specific errors.</span></span>

### <a name="security-only-allow-a-task-to-be-edited-by-its-creator"></a><span data-ttu-id="d5bff-191">安全性：仅允许由其创建者编辑任务</span><span class="sxs-lookup"><span data-stu-id="d5bff-191">Security: only allow a task to be edited by its creator</span></span>

<span data-ttu-id="d5bff-192">"仪表板索引" 页仅显示登录用户创建的任务，但恶意用户可能会创建一个 ID 为其他用户任务的 URL。</span><span class="sxs-lookup"><span data-stu-id="d5bff-192">The Dashboard Index page only shows tasks created by the logged-on user, but a malicious user could create a URL with an ID to another user's task.</span></span> <span data-ttu-id="d5bff-193">我们在 *DashboardController.cs* 中添加了代码，在这种情况下返回404：</span><span class="sxs-lookup"><span data-stu-id="d5bff-193">We added code in *DashboardController.cs* to return a 404 in that case:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample5.cs?highlight=9-14,24-29)]

### <a name="dont-swallow-exceptions"></a><span data-ttu-id="d5bff-194">不要吞并异常</span><span class="sxs-lookup"><span data-stu-id="d5bff-194">Don't swallow exceptions</span></span>

<span data-ttu-id="d5bff-195">最初的 Fix It 应用在记录由 SQL 查询引发的异常后，刚刚返回 null：</span><span class="sxs-lookup"><span data-stu-id="d5bff-195">The original Fix It app just returned null after logging an exception that resulted from a SQL query:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample6.cs?highlight=4)]

<span data-ttu-id="d5bff-196">这会使用户看起来像查询成功，但并不返回任何行。</span><span class="sxs-lookup"><span data-stu-id="d5bff-196">This would make it look to the user as if the query succeeded but just didn't return any rows.</span></span> <span data-ttu-id="d5bff-197">解决方法是在捕获和记录后重新引发异常：</span><span class="sxs-lookup"><span data-stu-id="d5bff-197">Solution is to re-throw the exception after catching and logging:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample7.cs)]

### <a name="catch-all-exceptions-in-worker-roles"></a><span data-ttu-id="d5bff-198">捕获辅助角色中的所有异常</span><span class="sxs-lookup"><span data-stu-id="d5bff-198">Catch all exceptions in worker roles</span></span>

<span data-ttu-id="d5bff-199">辅助角色中的任何未经处理的异常都将导致 VM 被回收，因此你希望在 try-catch 块中包装所有内容并处理所有异常。</span><span class="sxs-lookup"><span data-stu-id="d5bff-199">Any unhandled exceptions in a worker role will cause the VM to be recycled, so you want to wrap everything you do in a try-catch block and handle all exceptions.</span></span>

### <a name="specify-length-for-string-properties-in-entity-classes"></a><span data-ttu-id="d5bff-200">指定实体类中字符串属性的长度</span><span class="sxs-lookup"><span data-stu-id="d5bff-200">Specify length for string properties in entity classes</span></span>

<span data-ttu-id="d5bff-201">为了显示简单代码，修复 It 应用的原始版本未指定 FixItTask 实体字段的长度，因此，它们在数据库中定义为 varchar (max) 。</span><span class="sxs-lookup"><span data-stu-id="d5bff-201">In order to display simple code, the original version of the Fix It app didn't specify lengths for the fields of the FixItTask entity, and as a result they were defined as varchar(max) in the database.</span></span> <span data-ttu-id="d5bff-202">因此，UI 几乎可以接受任意数量的输入。</span><span class="sxs-lookup"><span data-stu-id="d5bff-202">As a result, the UI would accept almost any amount of input.</span></span> <span data-ttu-id="d5bff-203">指定长度会将应用于网页中的用户输入和数据库中的列大小的限制设置为：</span><span class="sxs-lookup"><span data-stu-id="d5bff-203">Specifying lengths sets limits that apply both to user input in the web page and column size in the database:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample8.cs?highlight=4,7,10,12,14)]

### <a name="mark-private-members-as-readonly-when-they-arent-expected-to-change"></a><span data-ttu-id="d5bff-204">当私有成员不应更改时将其标记为只读</span><span class="sxs-lookup"><span data-stu-id="d5bff-204">Mark private members as readonly when they aren't expected to change</span></span>

<span data-ttu-id="d5bff-205">例如，在的 `DashboardController` 类中创建了一个实例， `FixItTaskRepository` 但该实例不应更改，因此我们将其定义为 [readonly](https://msdn.microsoft.com/library/acdd6hb7.aspx)。</span><span class="sxs-lookup"><span data-stu-id="d5bff-205">For example, in the `DashboardController` class an instance of `FixItTaskRepository` is created and isn't expected to change, so we defined it as [readonly](https://msdn.microsoft.com/library/acdd6hb7.aspx).</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample9.cs?highlight=3)]

### <a name="use-listany-instead-of-listcount-gt-0"></a><span data-ttu-id="d5bff-206">使用列表。任何 ( # A1，而不是 list。计数 ( # A3 &gt; 0</span><span class="sxs-lookup"><span data-stu-id="d5bff-206">Use list.Any() instead of list.Count() &gt; 0</span></span>

<span data-ttu-id="d5bff-207">如果你只关心列表中的一个或多个项是否符合指定的条件，请使用 [Any](https://msdn.microsoft.com/library/bb534972.aspx) 方法，因为它会在找到符合条件的项后立即返回，而 `Count` 方法始终必须循环访问每个项。</span><span class="sxs-lookup"><span data-stu-id="d5bff-207">If you all you care about is whether one or more items in a list fit the specified criteria, use the [Any](https://msdn.microsoft.com/library/bb534972.aspx) method, because it returns as soon as an item fitting the criteria is found, whereas the `Count` method always has to iterate through every item.</span></span> <span data-ttu-id="d5bff-208">仪表板 *索引 cshtml* 文件最初具有以下代码：</span><span class="sxs-lookup"><span data-stu-id="d5bff-208">The Dashboard *Index.cshtml* file originally had this code:</span></span>

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample10.cshtml)]

<span data-ttu-id="d5bff-209">我们将其更改为：</span><span class="sxs-lookup"><span data-stu-id="d5bff-209">We changed it to this:</span></span>

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample11.cshtml?highlight=1)]

### <a name="generate-urls-in-mvc-views-using-mvc-helpers"></a><span data-ttu-id="d5bff-210">使用 MVC 帮助程序在 MVC 视图中生成 Url</span><span class="sxs-lookup"><span data-stu-id="d5bff-210">Generate URLs in MVC views using MVC helpers</span></span>

<span data-ttu-id="d5bff-211">对于主页上的 " **创建修复它** " 按钮，"修复 it 应用" 硬编码锚点元素：</span><span class="sxs-lookup"><span data-stu-id="d5bff-211">For the **Create a Fix It** button on the home page, the Fix It app hard coded an anchor element:</span></span>

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample12.cshtml)]

<span data-ttu-id="d5bff-212">对于类似的视图/操作链接，最好使用 [Url。操作](https://msdn.microsoft.com/library/system.web.mvc.urlhelper.action.aspx) HTML 帮助器，例如：</span><span class="sxs-lookup"><span data-stu-id="d5bff-212">For View/Action links like this it's better to use the [Url.Action](https://msdn.microsoft.com/library/system.web.mvc.urlhelper.action.aspx) HTML helper, for example:</span></span>

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample13.cshtml)]

### <a name="use-taskdelay-instead-of-threadsleep-in-worker-role"></a><span data-ttu-id="d5bff-213">使用任务延迟，而不是线程。辅助角色中的睡眠</span><span class="sxs-lookup"><span data-stu-id="d5bff-213">Use Task.Delay instead of Thread.Sleep in worker role</span></span>

<span data-ttu-id="d5bff-214">新项目模板 `Thread.Sleep` 为辅助角色提供示例代码，但导致线程进入睡眠状态可能导致线程池产生其他不必要的线程。</span><span class="sxs-lookup"><span data-stu-id="d5bff-214">The new-project template puts `Thread.Sleep` in the sample code for a worker role, but causing the thread to sleep can cause the thread pool to spawn additional unnecessary threads.</span></span> <span data-ttu-id="d5bff-215">可以通过使用 [Task](https://msdn.microsoft.com/library/hh139096.aspx) 来避免这种情况。</span><span class="sxs-lookup"><span data-stu-id="d5bff-215">You can avoid that by using [Task.Delay](https://msdn.microsoft.com/library/hh139096.aspx) instead.</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample14.cs?highlight=11)]

### <a name="avoid-async-void"></a><span data-ttu-id="d5bff-216">避免 async void</span><span class="sxs-lookup"><span data-stu-id="d5bff-216">Avoid async void</span></span>

<span data-ttu-id="d5bff-217">如果异步方法不需要返回值，则返回 `Task` 类型而不是 `void` 。</span><span class="sxs-lookup"><span data-stu-id="d5bff-217">If an async method doesn't need to return a value, return a `Task` type rather than `void`.</span></span>

<span data-ttu-id="d5bff-218">此示例来自 `FixItQueueManager` 类：</span><span class="sxs-lookup"><span data-stu-id="d5bff-218">This example is from the `FixItQueueManager` class:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample15.cs)]

<span data-ttu-id="d5bff-219">只应使用 `async void` 顶级事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="d5bff-219">You should use `async void` only for top-level event handlers.</span></span> <span data-ttu-id="d5bff-220">如果将方法定义为 `async void` ，则调用方不能 **等待** 方法或捕获该方法引发的任何异常。</span><span class="sxs-lookup"><span data-stu-id="d5bff-220">If you define a method as `async void`, the caller cannot **await** the method or catch any exceptions the method throws.</span></span> <span data-ttu-id="d5bff-221">有关详细信息，请参阅 [异步编程中的最佳做法](https://msdn.microsoft.com/magazine/jj991977.aspx)。</span><span class="sxs-lookup"><span data-stu-id="d5bff-221">For more information, see [Best Practices in Asynchronous Programming](https://msdn.microsoft.com/magazine/jj991977.aspx).</span></span>

### <a name="use-a-cancellation-token-to-break-from-worker-role-loop"></a><span data-ttu-id="d5bff-222">使用取消标记从辅助角色循环中断</span><span class="sxs-lookup"><span data-stu-id="d5bff-222">Use a cancellation token to break from worker role loop</span></span>

<span data-ttu-id="d5bff-223">通常，辅助角色上的 **Run** 方法包含无限循环。</span><span class="sxs-lookup"><span data-stu-id="d5bff-223">Typically, the **Run** method on a worker role contains an infinite loop.</span></span> <span data-ttu-id="d5bff-224">辅助角色停止时，将调用 [RoleEntryPoint](https://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstop.aspx) 方法。</span><span class="sxs-lookup"><span data-stu-id="d5bff-224">When the worker role is stopping, the [RoleEntryPoint.OnStop](https://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstop.aspx) method is called.</span></span> <span data-ttu-id="d5bff-225">应使用此方法取消在 **Run** 方法内完成的工作并正常退出。</span><span class="sxs-lookup"><span data-stu-id="d5bff-225">You should use this method to cancel the work that is being done inside the **Run** method and exit gracefully.</span></span> <span data-ttu-id="d5bff-226">否则，可能会在操作过程中终止进程。</span><span class="sxs-lookup"><span data-stu-id="d5bff-226">Otherwise, the process might be terminated in the middle of an operation.</span></span>

### <a name="opt-out-of-automatic-mime-sniffing-procedure"></a><span data-ttu-id="d5bff-227">选择退出自动 MIME 探查过程</span><span class="sxs-lookup"><span data-stu-id="d5bff-227">Opt out of Automatic MIME Sniffing Procedure</span></span>

<span data-ttu-id="d5bff-228">在某些情况下，Internet Explorer 报告 MIME 类型不同于 web 服务器指定的类型。</span><span class="sxs-lookup"><span data-stu-id="d5bff-228">In some cases, Internet Explorer reports a MIME type different than the type specified by the web server.</span></span> <span data-ttu-id="d5bff-229">例如，如果 Internet Explorer 在使用 HTTP 响应标头 Content （文本/无格式）传递的文件中查找 HTML 内容，则 Internet Explorer 会确定内容应呈现为 HTML。</span><span class="sxs-lookup"><span data-stu-id="d5bff-229">For instance, if Internet Explorer finds HTML content in a file delivered with the HTTP response header Content-Type: text/plain, Internet Explorer determines that the content should be rendered as HTML.</span></span> <span data-ttu-id="d5bff-230">遗憾的是，这种 "MIME 探查" 也可能导致承载不受信任的内容的服务器的安全问题。</span><span class="sxs-lookup"><span data-stu-id="d5bff-230">Unfortunately, this "MIME-sniffing" can also lead to security problems for servers hosting untrusted content.</span></span> <span data-ttu-id="d5bff-231">为了应对此问题，Internet Explorer 8 对 MIME 类型的确定代码进行了大量更改，并使应用程序开发人员可以 [选择退出 mime 探查](https://blogs.msdn.com/b/ie/archive/2008/07/02/ie8-security-part-v-comprehensive-protection.aspx)。</span><span class="sxs-lookup"><span data-stu-id="d5bff-231">To combat this problem, Internet Explorer 8 has made a number of changes to MIME-type determination code and allows application developers to [opt out of MIME-sniffing](https://blogs.msdn.com/b/ie/archive/2008/07/02/ie8-security-part-v-comprehensive-protection.aspx).</span></span> <span data-ttu-id="d5bff-232">下面的代码已添加到 *Web.config* 文件中。</span><span class="sxs-lookup"><span data-stu-id="d5bff-232">The following code was added to the *Web.config* file.</span></span>

[!code-xml[Main](the-fix-it-sample-application/samples/sample16.xml?highlight=2-7)]

### <a name="enable-bundling-and-minification"></a><span data-ttu-id="d5bff-233">启用捆绑和缩减</span><span class="sxs-lookup"><span data-stu-id="d5bff-233">Enable bundling and minification</span></span>

<span data-ttu-id="d5bff-234">当 Visual Studio 创建新的 web 项目时，默认情况下不启用 JavaScript 文件的绑定和缩减。</span><span class="sxs-lookup"><span data-stu-id="d5bff-234">When Visual Studio creates a new web project, bundling and minification of JavaScript files is not enabled by default.</span></span> <span data-ttu-id="d5bff-235">我们在 BundleConfig.cs 中添加了一行代码：</span><span class="sxs-lookup"><span data-stu-id="d5bff-235">We added a line of code in BundleConfig.cs:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample17.cs?highlight=9)]

### <a name="set-an-expiration-time-out-for-authentication-cookies"></a><span data-ttu-id="d5bff-236">设置身份验证 cookie 的过期超时</span><span class="sxs-lookup"><span data-stu-id="d5bff-236">Set an expiration time-out for authentication cookies</span></span>

<span data-ttu-id="d5bff-237">默认情况下，身份验证 cookie 在两周后过期。</span><span class="sxs-lookup"><span data-stu-id="d5bff-237">By default, authentication cookies expire in two weeks.</span></span> <span data-ttu-id="d5bff-238">更短的时间更安全。</span><span class="sxs-lookup"><span data-stu-id="d5bff-238">A shorter time is more secure.</span></span> <span data-ttu-id="d5bff-239">可以在 *StartupAuth.cs* 中更改此设置：</span><span class="sxs-lookup"><span data-stu-id="d5bff-239">You can change this setting in *StartupAuth.cs*:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample18.cs?highlight=4-5)]

<a id="run-in-vs"></a>
## <a name="how-to-run-the-app-from-visual-studio-on-your-local-computer"></a><span data-ttu-id="d5bff-240">如何在本地计算机上从 Visual Studio 运行应用</span><span class="sxs-lookup"><span data-stu-id="d5bff-240">How to run the app from Visual Studio on your local computer</span></span>

<span data-ttu-id="d5bff-241">可以通过两种方式来运行 Fix It 应用：</span><span class="sxs-lookup"><span data-stu-id="d5bff-241">There are two ways to run the Fix It app:</span></span>

- <span data-ttu-id="d5bff-242">运行将新任务直接写入 SQL 数据库的基本应用程序。</span><span class="sxs-lookup"><span data-stu-id="d5bff-242">Run the base application that writes new tasks directly to the SQL database.</span></span>
- <span data-ttu-id="d5bff-243">使用队列和后端服务运行应用程序以创建任务。</span><span class="sxs-lookup"><span data-stu-id="d5bff-243">Run the application using a queue plus a backend service to create tasks.</span></span> <span data-ttu-id="d5bff-244">队列模式在以 [队列为中心的工作模式](queue-centric-work-pattern.md)中进行了介绍。</span><span class="sxs-lookup"><span data-stu-id="d5bff-244">The queue pattern is described in the chapter [Queue-Centric Work Pattern](queue-centric-work-pattern.md).</span></span>

<a id="runbase"></a>
### <a name="run-the-base-application"></a><span data-ttu-id="d5bff-245">运行基本应用程序</span><span class="sxs-lookup"><span data-stu-id="d5bff-245">Run the base application</span></span>

1. <span data-ttu-id="d5bff-246">安装 [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)。</span><span class="sxs-lookup"><span data-stu-id="d5bff-246">Install [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017).</span></span>
2. <span data-ttu-id="d5bff-247">安装 [适用于 Visual Studio 的 AZURE SDK for .net](https://azure.microsoft.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="d5bff-247">Install the [Azure SDK for .NET for Visual Studio](https://azure.microsoft.com/downloads/).</span></span>
3. <span data-ttu-id="d5bff-248">从 [MSDN 代码库](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)下载 .zip 文件。</span><span class="sxs-lookup"><span data-stu-id="d5bff-248">Download the .zip file from the [MSDN Code Gallery](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4).</span></span>
4. <span data-ttu-id="d5bff-249">在文件资源管理器中，右键单击 .zip 文件并单击 "属性"，然后在属性窗口单击 "解除阻止"。</span><span class="sxs-lookup"><span data-stu-id="d5bff-249">In File Explorer, right-click the .zip file and click Properties, then in the Properties window click Unblock.</span></span>
5. <span data-ttu-id="d5bff-250">解压缩文件。</span><span class="sxs-lookup"><span data-stu-id="d5bff-250">Unzip the file.</span></span>
6. <span data-ttu-id="d5bff-251">双击 .sln 文件以启动 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="d5bff-251">Double-click the .sln file to launch Visual Studio.</span></span>
7. <span data-ttu-id="d5bff-252">从 " **工具** " 菜单中依次单击 " **NuGet 包管理器**" 和 " **程序包管理器控制台**"。</span><span class="sxs-lookup"><span data-stu-id="d5bff-252">From the **Tools** menu, click **NuGet Package Manager**, then **Package Manager Console**.</span></span>
8. <span data-ttu-id="d5bff-253">在包管理器控制台中 (PMC ") 中，单击" 还原 "。</span><span class="sxs-lookup"><span data-stu-id="d5bff-253">In the Package Manager Console (PMC), click Restore.</span></span>
9. <span data-ttu-id="d5bff-254">退出 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="d5bff-254">Exit Visual Studio.</span></span>
10. <span data-ttu-id="d5bff-255">启动 [Azure 存储模拟器](/azure/storage/common/storage-use-emulator)。</span><span class="sxs-lookup"><span data-stu-id="d5bff-255">Start the [Azure Storage Emulator](/azure/storage/common/storage-use-emulator).</span></span>
11. <span data-ttu-id="d5bff-256">重新启动 Visual Studio，并打开在上一步中关闭的解决方案文件。</span><span class="sxs-lookup"><span data-stu-id="d5bff-256">Restart Visual Studio, opening the solution file you closed in the previous step.</span></span>
12. <span data-ttu-id="d5bff-257">请确保将 Fix it 项目设置为启动项目，然后按 CTRL + F5 运行该项目。</span><span class="sxs-lookup"><span data-stu-id="d5bff-257">Make sure the FixIt project is set as the startup project, and then press CTRL+F5 to run the project.</span></span>

<a id="queueslocal"></a>
### <a name="run-the-application-with-queue-processing"></a><span data-ttu-id="d5bff-258">运行具有队列处理的应用程序</span><span class="sxs-lookup"><span data-stu-id="d5bff-258">Run the application with queue processing</span></span>

1. <span data-ttu-id="d5bff-259">按照 [运行基本应用程序](#runbase)的说明进行操作，然后关闭浏览器并关闭 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="d5bff-259">Follow the directions for [Run the base application](#runbase), and then close the browser and close Visual Studio.</span></span>
2. <span data-ttu-id="d5bff-260">以管理员权限启动 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="d5bff-260">Start Visual Studio with administrator privileges.</span></span> <span data-ttu-id="d5bff-261"> (你将使用 Azure 计算模拟器，并且需要管理员权限。 ) </span><span class="sxs-lookup"><span data-stu-id="d5bff-261">(You'll be using the Azure Compute Emulator, and that requires administrator privileges.)</span></span>
3. <span data-ttu-id="d5bff-262">在 *MyFixIt* 项目的应用程序 *Web.config* 文件中 (web 项目) ，将的值更改 `appSettings/UseQueues` 为 "true"：</span><span class="sxs-lookup"><span data-stu-id="d5bff-262">In the application *Web.config* file in the *MyFixIt* project (the web project), change the value of `appSettings/UseQueues` to "true":</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample19.cmd?highlight=3)]
4. <span data-ttu-id="d5bff-263">如果 [Azure 存储模拟器](https://msdn.microsoft.com/library/windowsazure/hh403989.aspx) 仍未运行，请重新启动。</span><span class="sxs-lookup"><span data-stu-id="d5bff-263">If the [Azure Storage Emulator](https://msdn.microsoft.com/library/windowsazure/hh403989.aspx) isn't still running, start it again.</span></span>
5. <span data-ttu-id="d5bff-264">同时运行 Fix it web 项目和 MyFixItCloudService 项目。</span><span class="sxs-lookup"><span data-stu-id="d5bff-264">Run the FixIt web project and the MyFixItCloudService project simultaneously.</span></span>

    <span data-ttu-id="d5bff-265">使用 Visual Studio：</span><span class="sxs-lookup"><span data-stu-id="d5bff-265">Using Visual Studio:</span></span>

   1. <span data-ttu-id="d5bff-266">按 **F5** 运行 fix it 项目。</span><span class="sxs-lookup"><span data-stu-id="d5bff-266">Press **F5** to run the FixIt project.</span></span>
   2. <span data-ttu-id="d5bff-267">在 **解决方案资源管理器** 中，右键单击 MyFixItCloudService 项目，然后单击 "**调试**" "  >  **启动新实例**"。</span><span class="sxs-lookup"><span data-stu-id="d5bff-267">In **Solution Explorer**, right-click the MyFixItCloudService project, and then click **Debug** > **Start New Instance**.</span></span>

    <span data-ttu-id="d5bff-268">使用 Visual Studio 2013 Express for Web：</span><span class="sxs-lookup"><span data-stu-id="d5bff-268">Using Visual Studio 2013 Express for Web:</span></span>

   3. <span data-ttu-id="d5bff-269">在解决方案资源管理器中，右键单击 Fix it 解决方案，然后选择 " **属性**"。</span><span class="sxs-lookup"><span data-stu-id="d5bff-269">In Solution Explorer, right-click the FixIt solution and select **Properties**.</span></span>
   4. <span data-ttu-id="d5bff-270">选择 **多个启动项目**。</span><span class="sxs-lookup"><span data-stu-id="d5bff-270">Select **Multiple Startup Projects**.</span></span>
   5. <span data-ttu-id="d5bff-271">在 MyFixIt 和 MyFixItCloudService 下的 " **操作** " 下拉列表中，选择 " **启动**"。</span><span class="sxs-lookup"><span data-stu-id="d5bff-271">In the **Action** dropdown list under MyFixIt and MyFixItCloudService, select **Start**.</span></span>
   6. <span data-ttu-id="d5bff-272">单击" **确定**"。</span><span class="sxs-lookup"><span data-stu-id="d5bff-272">Click **OK**.</span></span>
   7. <span data-ttu-id="d5bff-273">按 **F5** 运行这两个项目。</span><span class="sxs-lookup"><span data-stu-id="d5bff-273">Press **F5** to run both projects.</span></span>

      <span data-ttu-id="d5bff-274">运行 MyFixItCloudService 项目时，Visual Studio 将启动 Azure 计算模拟器。</span><span class="sxs-lookup"><span data-stu-id="d5bff-274">When you run the MyFixItCloudService project, Visual Studio starts the Azure Compute Emulator.</span></span> <span data-ttu-id="d5bff-275">根据防火墙配置，可能需要通过防火墙允许模拟器。</span><span class="sxs-lookup"><span data-stu-id="d5bff-275">Depending on your firewall configuration, you might need to allow the emulator through the firewall.</span></span>

<a id="deploybase"></a>
## <a name="how-to-deploy-the-base-app-to-azure-app-service-web-apps-by-using-the-windows-powershell-scripts"></a><span data-ttu-id="d5bff-276">如何使用 Windows PowerShell 脚本将基本应用部署到 Azure App Service Web 应用</span><span class="sxs-lookup"><span data-stu-id="d5bff-276">How to deploy the base app to Azure App Service Web Apps by using the Windows PowerShell scripts</span></span>

<span data-ttu-id="d5bff-277">为了说明 [自动完成所有](automate-everything.md) 模式，通过在 Azure 中设置环境并将项目部署到新环境的脚本提供了 Fix It 应用。</span><span class="sxs-lookup"><span data-stu-id="d5bff-277">To illustrate the [Automate Everything](automate-everything.md) pattern, the Fix It app is supplied with scripts that set up an environment in Azure and deploy the project to the new environment.</span></span> <span data-ttu-id="d5bff-278">以下说明介绍了如何使用这些脚本。</span><span class="sxs-lookup"><span data-stu-id="d5bff-278">The following instructions explain how to use the scripts.</span></span>

<span data-ttu-id="d5bff-279">如果要在 Azure 中运行而不使用队列，并且更改了在本地运行队列，请确保在继续执行以下说明之前，将 UseQueues appSetting 值设置回 false。</span><span class="sxs-lookup"><span data-stu-id="d5bff-279">If you want to run in Azure without using queues, and you made the changes to run locally with queues, make sure you set the UseQueues appSetting value back to false before proceeding with the following instructions.</span></span>

<span data-ttu-id="d5bff-280">这些说明假定你已在本地下载并运行 Fix It 解决方案，并且你有一个 Azure 帐户，或者你有权管理的 Azure 订阅。</span><span class="sxs-lookup"><span data-stu-id="d5bff-280">These instructions assume you have already downloaded and run the Fix It solution locally, and that you have an Azure account or have an Azure subscription that you are authorized to manage.</span></span>

1. <span data-ttu-id="d5bff-281">安装 **Azure PowerShell** 控制台。</span><span class="sxs-lookup"><span data-stu-id="d5bff-281">Install the **Azure PowerShell** console.</span></span> <span data-ttu-id="d5bff-282">有关说明，请参阅[如何安装和配置 Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-4.3.1)。</span><span class="sxs-lookup"><span data-stu-id="d5bff-282">For instructions, see [How to install and configure Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-4.3.1).</span></span>

    <span data-ttu-id="d5bff-283">此自定义控制台配置为使用 Azure 订阅。</span><span class="sxs-lookup"><span data-stu-id="d5bff-283">This customized console is configured to work with your Azure subscription.</span></span> <span data-ttu-id="d5bff-284">Azure 模块安装在 *Program Files* 目录中，并将在每次使用 Azure PowerShell 控制台时自动导入。</span><span class="sxs-lookup"><span data-stu-id="d5bff-284">The Azure module is installed in the *Program Files* directory and is automatically imported on every use of the Azure PowerShell console.</span></span>

    <span data-ttu-id="d5bff-285">如果希望在不同的主机程序中工作，如 Windows PowerShell ISE，请确保使用 [import-module](https://go.microsoft.com/fwlink/?LinkID=141553) cmdlet 导入 azure 模块，或使用 azure 模块中的命令来触发模块的自动导入。</span><span class="sxs-lookup"><span data-stu-id="d5bff-285">If you prefer to work in a different host program, such as Windows PowerShell ISE, be sure to use the [Import-Module](https://go.microsoft.com/fwlink/?LinkID=141553) cmdlet to import the Azure module or use a command in the Azure module to trigger automatic importing of the module.</span></span>
2. <span data-ttu-id="d5bff-286">通过 "以 **管理员身份运行** " 选项启动 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="d5bff-286">Start Azure PowerShell with the **Run as administrator** option.</span></span>
3. <span data-ttu-id="d5bff-287">运行 [set-executionpolicy](https://go.microsoft.com/fwlink/p/?linkid=293941) cmdlet 以将 Azure PowerShell 执行策略设置为 `RemoteSigned` 。</span><span class="sxs-lookup"><span data-stu-id="d5bff-287">Run the [Set-ExecutionPolicy](https://go.microsoft.com/fwlink/p/?linkid=293941) cmdlet to set the Azure PowerShell execution policy to `RemoteSigned`.</span></span> <span data-ttu-id="d5bff-288">输入 **"** 是" ("是") 完成策略更改。</span><span class="sxs-lookup"><span data-stu-id="d5bff-288">Enter **Y** (for Yes) to complete the policy change.</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample20.cmd)]

    <span data-ttu-id="d5bff-289">此设置允许您运行未进行数字签名的本地脚本。</span><span class="sxs-lookup"><span data-stu-id="d5bff-289">This setting enables you to run local scripts that aren't digitally signed.</span></span> <span data-ttu-id="d5bff-290"> (您还可以将执行策略设置为 `Unrestricted` ，这将不再需要取消阻止步骤，但出于安全原因，不建议这样做。 ) </span><span class="sxs-lookup"><span data-stu-id="d5bff-290">(You can also set the execution policy to `Unrestricted`, which would eliminate the need for the unblock step later, but this is not recommended for security reasons.)</span></span>
4. <span data-ttu-id="d5bff-291">运行 `Add-AzureAccount` cmdlet，为你的帐户设置具有凭据的 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="d5bff-291">Run the `Add-AzureAccount` cmdlet to set up PowerShell with credentials for your account.</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample21.cmd)]

    <span data-ttu-id="d5bff-292">这些凭据将在一段时间后过期，你必须重新运行 `Add-AzureAccount` cmdlet。</span><span class="sxs-lookup"><span data-stu-id="d5bff-292">These credentials expire after a period of time and you have to re-run the `Add-AzureAccount` cmdlet.</span></span> <span data-ttu-id="d5bff-293">在编写此电子书时，凭据过期前的时间限制为12小时。</span><span class="sxs-lookup"><span data-stu-id="d5bff-293">As this e-book is being written, the time limit before credentials expire is 12 hours.</span></span>
5. <span data-ttu-id="d5bff-294">如果有多个订阅，请使用 Select-AzureSubscription cmdlet 来指定要在其中创建测试环境的订阅。</span><span class="sxs-lookup"><span data-stu-id="d5bff-294">If you have multiple subscriptions, use the Select-AzureSubscription cmdlet to specify the subscription you want to create the test environment in.</span></span>
6. <span data-ttu-id="d5bff-295">使用和 cmdlet 导入同一 Azure 订阅的管理证书 `Get-AzurePublishSettingsFile` `Import-AzurePublishSettingsFile` 。</span><span class="sxs-lookup"><span data-stu-id="d5bff-295">Import a management certificate for the same Azure subscription by using the `Get-AzurePublishSettingsFile` and `Import-AzurePublishSettingsFile` cmdlets.</span></span> <span data-ttu-id="d5bff-296">其中的第一个 cmdlet 下载证书文件，并在第二个 cmdlet 中指定该文件的位置以将其导入。</span><span class="sxs-lookup"><span data-stu-id="d5bff-296">The first of these cmdlets downloads a certificate file, and in the second one you specify the location of that file in order to import it.</span></span> > [!IMPORTANT]
   > <span data-ttu-id="d5bff-297">将下载的文件保存在安全的位置，或在完成后将其删除，因为它包含可用于管理 Azure 服务的证书。</span><span class="sxs-lookup"><span data-stu-id="d5bff-297">Keep the downloaded file in a safe location or delete it when you're done with it, because it contains a certificate that can be used to manage your Azure services.</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample22.cmd)]

    <span data-ttu-id="d5bff-298">证书用于检测开发计算机的 IP 地址的 REST API 调用，以便在 SQL 数据库服务器上设置防火墙规则。</span><span class="sxs-lookup"><span data-stu-id="d5bff-298">The certificate is used for a REST API call that detects the development machine's IP address in order to set a firewall rule on the SQL Database server.</span></span>
7. <span data-ttu-id="d5bff-299">运行 ([Set-Location](https://go.microsoft.com/fwlink/p/?linkid=293912)别名为 `cd` 、 `chdir` 和 `sl`) ，以导航到包含脚本的目录。</span><span class="sxs-lookup"><span data-stu-id="d5bff-299">Run the [Set-Location](https://go.microsoft.com/fwlink/p/?linkid=293912) cmdlet (aliases are `cd`, `chdir`, and `sl`) to navigate to the directory that contains the scripts.</span></span> <span data-ttu-id="d5bff-300"> (它们位于 Fix It 解决方案文件夹中的 *Automation* 文件夹中。如果任何目录名称包含空格，则 ) 将路径放在引号中。</span><span class="sxs-lookup"><span data-stu-id="d5bff-300">(They're located in the *Automation* folder in the Fix It solution folder.) Put the path in quotes if any of the directory names contain spaces.</span></span> <span data-ttu-id="d5bff-301">例如，若要导航到该 `c:\Sample Apps\FixIt\Automation` 目录，可以输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="d5bff-301">For example, to navigate to the `c:\Sample Apps\FixIt\Automation` directory you could enter the following command:</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample23.cmd)]
8. <span data-ttu-id="d5bff-302">若要允许 Windows PowerShell 运行这些脚本，请使用 [取消阻止文件](https://go.microsoft.com/fwlink/p/?linkid=294021) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="d5bff-302">To allow Windows PowerShell to run these scripts, use the [Unblock-File](https://go.microsoft.com/fwlink/p/?linkid=294021) cmdlet.</span></span> <span data-ttu-id="d5bff-303"> (脚本被阻止，因为这些脚本是从 Internet 下载的。 ) </span><span class="sxs-lookup"><span data-stu-id="d5bff-303">(The scripts are blocked because they were downloaded from the Internet.)</span></span>

    > [!WARNING]
    > <span data-ttu-id="d5bff-304">安全性- `Unblock-File` 在任何脚本或可执行文件上运行之前，在记事本中打开文件，检查命令，并验证它们是否不包含任何恶意代码。</span><span class="sxs-lookup"><span data-stu-id="d5bff-304">Security - Before running `Unblock-File` on any script or executable file, open the file in Notepad, examine the commands, and verify that they do not contain any malicious code.</span></span>

    <span data-ttu-id="d5bff-305">例如，以下命令将 `Unblock-File` 对当前目录中的所有脚本运行 cmdlet。</span><span class="sxs-lookup"><span data-stu-id="d5bff-305">For example, the following command runs the `Unblock-File` cmdlet on all scripts in the current directory.</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample24.cmd)]
9. <span data-ttu-id="d5bff-306">若要创建基本 (的 web 应用，) 修复 It 应用，请运行环境创建脚本。</span><span class="sxs-lookup"><span data-stu-id="d5bff-306">To create the web app for the base (no queues processing) Fix It app, run the environment creation script.</span></span>

    <span data-ttu-id="d5bff-307">必需的 `Name` 参数指定数据库的名称，并且还用于该脚本创建的存储帐户。</span><span class="sxs-lookup"><span data-stu-id="d5bff-307">The required `Name` parameter specifies the name of the database and is also used for the storage account that the script creates.</span></span> <span data-ttu-id="d5bff-308">该名称在 azurewebsites.net 域中必须是全局唯一的。</span><span class="sxs-lookup"><span data-stu-id="d5bff-308">The name must be globally unique within the azurewebsites.net domain.</span></span> <span data-ttu-id="d5bff-309">如果指定的名称不是唯一的（例如 Fix it 或 Test (），甚至在示例中为) fixitdemo，则该 `New-AzureWebsite` cmdlet 将失败并出现内部错误，该错误会报告冲突。</span><span class="sxs-lookup"><span data-stu-id="d5bff-309">If you specify a name that is not unique, like Fixit or Test (or even as in the example, fixitdemo), the `New-AzureWebsite` cmdlet fails with an Internal Error that reports a conflict.</span></span> <span data-ttu-id="d5bff-310">此脚本将名称转换为全部小写，以符合 web 应用、存储帐户和数据库的名称要求。</span><span class="sxs-lookup"><span data-stu-id="d5bff-310">The script converts the name to all lower-case to comply with name requirements for web apps, storage accounts, and databases.</span></span>

    <span data-ttu-id="d5bff-311">必需的 `SqlDatabasePassword` 参数指定将为 SQL 数据库创建的管理员帐户的密码。</span><span class="sxs-lookup"><span data-stu-id="d5bff-311">The required `SqlDatabasePassword` parameter specifies the password for the admin account that will be created for SQL Database.</span></span> <span data-ttu-id="d5bff-312">请勿在密码 (中包含特殊 XML 字符 &amp; &lt; &gt; ，) 。</span><span class="sxs-lookup"><span data-stu-id="d5bff-312">Don't include special XML characters in the password (&amp; &lt; &gt; ;).</span></span> <span data-ttu-id="d5bff-313">这是编写脚本的方式的限制，而不是 Azure 的限制。</span><span class="sxs-lookup"><span data-stu-id="d5bff-313">This is a limitation of the way the scripts were written, not a limitation of Azure.</span></span>

    <span data-ttu-id="d5bff-314">例如，如果想要创建名为 "fixitdemo" 的 web 应用，并使用 "Passw0rd1" SQL Server 管理员密码，则可以输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="d5bff-314">For example, if you want to create a web app named "fixitdemo" and use a SQL Server administrator password of "Passw0rd1", you could enter the following command:</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample25.cmd)]

    <span data-ttu-id="d5bff-315">该名称在 azurewebsites.net 域中必须唯一，并且密码必须满足密码复杂性的 SQL 数据库要求。</span><span class="sxs-lookup"><span data-stu-id="d5bff-315">The name must be unique in the azurewebsites.net domain, and the password must meet SQL Database requirements for password complexity.</span></span> <span data-ttu-id="d5bff-316"> (示例 Passw0rd1 满足要求。 ) </span><span class="sxs-lookup"><span data-stu-id="d5bff-316">(The example Passw0rd1 does meet the requirements.)</span></span>

    <span data-ttu-id="d5bff-317">请注意，该命令以 ". \" 。</span><span class="sxs-lookup"><span data-stu-id="d5bff-317">Note that the command begins with ".\".</span></span> <span data-ttu-id="d5bff-318">为了帮助防止恶意脚本的执行，Windows PowerShell 要求你在运行脚本时提供脚本文件的完全限定路径。</span><span class="sxs-lookup"><span data-stu-id="d5bff-318">To help prevent malicious execution of scripts, Windows PowerShell requires that you provide the fully qualified path to the script file when you run a script.</span></span> <span data-ttu-id="d5bff-319">您可以使用点来指示当前目录 ( "。 \") 或提供完全限定的路径，例如：</span><span class="sxs-lookup"><span data-stu-id="d5bff-319">You can use a dot to indicate the current directory (".\") or provide the fully qualified path, such as:</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample26.cmd)]

    <span data-ttu-id="d5bff-320">有关该脚本的详细信息，请使用 `Get-Help` cmdlet。</span><span class="sxs-lookup"><span data-stu-id="d5bff-320">For more information about the script, use the `Get-Help` cmdlet.</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample27.cmd)]

    <span data-ttu-id="d5bff-321">你可以使用 `Detailed` `Full` Get-Help cmdlet 的、、 `Parameters` 和 `Examples` 参数来筛选返回的帮助。</span><span class="sxs-lookup"><span data-stu-id="d5bff-321">You can use the `Detailed`, `Full`, `Parameters`, and `Examples` parameters of the Get-Help cmdlet to filter the help that is returned.</span></span>

    <span data-ttu-id="d5bff-322">如果脚本失败或生成错误，如 "New-azurewebsite： Call Set-AzureSubscription 和 Select-AzureSubscription first"，则可能尚未完成 Azure PowerShell 的配置。</span><span class="sxs-lookup"><span data-stu-id="d5bff-322">If the script fails or generates errors, such as "New-AzureWebsite : Call Set-AzureSubscription and Select-AzureSubscription first," you might not have completed the configuration of Azure PowerShell.</span></span>

    <span data-ttu-id="d5bff-323">脚本完成后，可以使用 Azure 管理门户查看已创建的资源，如 " [自动执行所有](automate-everything.md) 操作" 一章中所示。</span><span class="sxs-lookup"><span data-stu-id="d5bff-323">After the script finishes, you can use the Azure Management Portal to see the resources that were created, as shown in the [Automate Everything](automate-everything.md) chapter.</span></span>
10. <span data-ttu-id="d5bff-324">若要将 Fix it 项目部署到新的 Azure 环境，请使用 *AzureWebsite.ps1* 脚本。</span><span class="sxs-lookup"><span data-stu-id="d5bff-324">To deploy the FixIt project to the new Azure environment, use the *AzureWebsite.ps1* script.</span></span> <span data-ttu-id="d5bff-325">例如：</span><span class="sxs-lookup"><span data-stu-id="d5bff-325">For example:</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample28.cmd)]

    <span data-ttu-id="d5bff-326">部署完成后，浏览器将打开，并在 Azure 中运行它。</span><span class="sxs-lookup"><span data-stu-id="d5bff-326">When deployment is done, the browser opens with Fix It running in Azure.</span></span>

<a id="troubleshooting"></a>
## <a name="troubleshooting-the-windows-powershell-scripts"></a><span data-ttu-id="d5bff-327">Windows PowerShell 脚本疑难解答</span><span class="sxs-lookup"><span data-stu-id="d5bff-327">Troubleshooting the Windows PowerShell scripts</span></span>

<span data-ttu-id="d5bff-328">运行这些脚本时遇到的最常见错误与权限有关。</span><span class="sxs-lookup"><span data-stu-id="d5bff-328">The most common errors encountered when running these scripts are related to permissions.</span></span> <span data-ttu-id="d5bff-329">请确保 `Add-AzureAccount` 和 `Import-AzurePublishSettingsFile` 已成功完成，并且已将其用于同一 Azure 订阅。</span><span class="sxs-lookup"><span data-stu-id="d5bff-329">Make sure that `Add-AzureAccount` and `Import-AzurePublishSettingsFile` were successful and that you used them for the same Azure subscription.</span></span> <span data-ttu-id="d5bff-330">即使 `Add-AzureAccount` 成功，您也可能需要重新运行它。</span><span class="sxs-lookup"><span data-stu-id="d5bff-330">Even if `Add-AzureAccount` was successful you might have to run it again.</span></span> <span data-ttu-id="d5bff-331">添加的权限将 `Add-AzureAccount` 在12小时后过期。</span><span class="sxs-lookup"><span data-stu-id="d5bff-331">The permissions added by `Add-AzureAccount` expire in 12 hours.</span></span>

### <a name="object-reference-not-set-to-an-instance-of-an-object"></a><span data-ttu-id="d5bff-332">对象引用未设置为某个对象的实例。</span><span class="sxs-lookup"><span data-stu-id="d5bff-332">Object reference not set to an instance of an object.</span></span>

<span data-ttu-id="d5bff-333">如果脚本返回错误，如 "对象引用未设置为对象的实例"，这意味着 Windows PowerShell 找不到要处理的对象 (这是 null 引用异常) ，请运行 `Add-AzureAccount` cmdlet，然后重试该脚本。</span><span class="sxs-lookup"><span data-stu-id="d5bff-333">If the script returns errors, such as "Object reference not set to an instance of an object," which means that Windows PowerShell can't find an object to process (this is a null reference exception), run the `Add-AzureAccount` cmdlet and try the script again.</span></span>

[!code-console[Main](the-fix-it-sample-application/samples/sample29.cmd)]

### <a name="internalerror-the-server-encountered-an-internal-error"></a><span data-ttu-id="d5bff-334">InternalError：服务器遇到内部错误。</span><span class="sxs-lookup"><span data-stu-id="d5bff-334">InternalError: The server encountered an internal error.</span></span>

<span data-ttu-id="d5bff-335">`New-AzureWebsite`如果名称在 azurewebsites.net 域中不唯一，则该 cmdlet 将返回内部错误。</span><span class="sxs-lookup"><span data-stu-id="d5bff-335">The `New-AzureWebsite` cmdlet returns an internal error when the name is not unique in the azurewebsites.net domain.</span></span> <span data-ttu-id="d5bff-336">若要解决此错误，请使用不同的名称值，该名称位于 *New-AzureWebsiteEnv.ps1* 的 name 参数中。</span><span class="sxs-lookup"><span data-stu-id="d5bff-336">To resolve the error, use a different value for the name, which is in the Name parameter of *New-AzureWebsiteEnv.ps1*.</span></span>

[!code-console[Main](the-fix-it-sample-application/samples/sample30.cmd)]

### <a name="restarting-the-script"></a><span data-ttu-id="d5bff-337">重新启动脚本</span><span class="sxs-lookup"><span data-stu-id="d5bff-337">Restarting the script</span></span>

<span data-ttu-id="d5bff-338">如果需要重新启动 *New-AzureWebsiteEnv.ps1* 脚本，因为它在打印 "脚本已完成" 消息之前失败，你可能想要删除该脚本在停止之前创建的资源。</span><span class="sxs-lookup"><span data-stu-id="d5bff-338">If you need to restart the *New-AzureWebsiteEnv.ps1* script because it failed before it printed the "Script is complete" message, you might want to delete resources that the script created before it stopped.</span></span> <span data-ttu-id="d5bff-339">例如，如果脚本已经创建了 ContosoFixItDemo web 应用，并使用同一名称再次运行该脚本，则该脚本将失败，因为该名称正在使用中。</span><span class="sxs-lookup"><span data-stu-id="d5bff-339">For example, if the script already created the ContosoFixItDemo web app and you run the script again with the same name, the script will fail because the name is in use.</span></span>

<span data-ttu-id="d5bff-340">若要确定脚本在停止之前创建了哪些资源，请使用以下 cmdlet：</span><span class="sxs-lookup"><span data-stu-id="d5bff-340">To determine which resources the script created before it stopped, use the following cmdlets:</span></span>

- `Get-AzureWebsite`
- `Get-AzureSqlDatabaseServer`
- <span data-ttu-id="d5bff-341">`Get-AzureSqlDatabase`：若要运行此 cmdlet，请通过管道将数据库服务器名称传递给 `Get-AzureSqlDatabase` ：   `Get-AzureSqlDatabaseServer | Get-AzureSqlDatabase.`</span><span class="sxs-lookup"><span data-stu-id="d5bff-341">`Get-AzureSqlDatabase`: To run this cmdlet, pipe the database server name to `Get-AzureSqlDatabase`:   `Get-AzureSqlDatabaseServer | Get-AzureSqlDatabase.`</span></span>

<span data-ttu-id="d5bff-342">若要删除这些资源，请使用以下命令。</span><span class="sxs-lookup"><span data-stu-id="d5bff-342">To delete these resources, use the following commands.</span></span> <span data-ttu-id="d5bff-343">请注意，如果删除数据库服务器，则会自动删除与该服务器关联的数据库。</span><span class="sxs-lookup"><span data-stu-id="d5bff-343">Note that if you delete the database server, you automatically delete the databases associated with the server.</span></span>

- `Get-AzureWebsite -Name <WebsiteName> | Remove-AzureWebsite`
- `Get-AzureSqlDatabase -Name <DatabaseName> -ServerName <DatabaseServerName> | Remove-SqlAzureDatabase`
- `Get-AzureSqlDatabaseServer | Remove-AzureSqlDatabaseServer`

<a id="deployqueues"></a>
## <a name="how-to-deploy-the-app-with-queue-processing-to-azure-app-service-web-apps-and-an-azure-cloud-service"></a><span data-ttu-id="d5bff-344">如何将具有队列处理的应用部署到 Azure App Service Web 应用和 Azure 云服务</span><span class="sxs-lookup"><span data-stu-id="d5bff-344">How to deploy the app with queue processing to Azure App Service Web Apps and an Azure Cloud Service</span></span>

<span data-ttu-id="d5bff-345">若要启用队列，请在 MyFixIt\Web.config 文件中进行以下更改。</span><span class="sxs-lookup"><span data-stu-id="d5bff-345">To enable queues, make the following change in the MyFixIt\Web.config file.</span></span> <span data-ttu-id="d5bff-346">在下 `appSettings` ，将的值更改 `UseQueues` 为 "true"：</span><span class="sxs-lookup"><span data-stu-id="d5bff-346">Under `appSettings`, change the value of `UseQueues` to "true":</span></span>

[!code-xml[Main](the-fix-it-sample-application/samples/sample31.xml)]

<span data-ttu-id="d5bff-347">然后，在 Azure App Service 中将 MVC 应用程序部署到 web 应用，如 [前文所](#deploybase)述。</span><span class="sxs-lookup"><span data-stu-id="d5bff-347">Then deploy the MVC application to an web app in Azure App Service, as described [earlier](#deploybase).</span></span>

<span data-ttu-id="d5bff-348">接下来，创建新的 Azure 云服务。</span><span class="sxs-lookup"><span data-stu-id="d5bff-348">Next, create a new Azure cloud service.</span></span> <span data-ttu-id="d5bff-349">Fix It 应用中包含的脚本不会创建或部署云服务，因此你必须使用 Azure 门户。</span><span class="sxs-lookup"><span data-stu-id="d5bff-349">The scripts included with the Fix It app do not create or deploy the cloud service, so you must use Azure portal for this.</span></span> <span data-ttu-id="d5bff-350">在门户中，单击 "**新建**  --  **计算**–**云服务**  --  " "**快速创建**"，然后输入 URL 和数据中心位置。</span><span class="sxs-lookup"><span data-stu-id="d5bff-350">In the portal, click **New** -- **Compute** – **Cloud Service** -- **Quick Create**, and then enter a URL and a data center location.</span></span> <span data-ttu-id="d5bff-351">使用在其中部署 web 应用的数据中心。</span><span class="sxs-lookup"><span data-stu-id="d5bff-351">Use the same data center where you deployed the web app.</span></span>

![](the-fix-it-sample-application/_static/image1.png)

<span data-ttu-id="d5bff-352">在部署云服务之前，需要更新一些配置文件。</span><span class="sxs-lookup"><span data-stu-id="d5bff-352">Before you can deploy the cloud service, you need to update some of the configuration files.</span></span>

<span data-ttu-id="d5bff-353">在 MyFixIt.WorkerRole\app.config 中的下 `connectionStrings` ，将连接字符串的值替换 `appdb` 为 SQL 数据库的实际连接字符串。</span><span class="sxs-lookup"><span data-stu-id="d5bff-353">In MyFixIt.WorkerRole\app.config, under `connectionStrings`, replace the value of the `appdb` connection string with the actual connection string for the SQL Database.</span></span> <span data-ttu-id="d5bff-354">可以从门户获取连接字符串。</span><span class="sxs-lookup"><span data-stu-id="d5bff-354">You can get the connection string from the portal.</span></span> <span data-ttu-id="d5bff-355">在门户中，单击 " **sql 数据库**" "appdb" "  -  **appdb**  -  **查看 ADO .net、ODBC、PHP 和 JDBC 的 sql 数据库连接字符串**"。</span><span class="sxs-lookup"><span data-stu-id="d5bff-355">In the portal, click **SQL Databases** - **appdb** - **View SQL Database connection strings for ADO .Net, ODBC, PHP, and JDBC**.</span></span> <span data-ttu-id="d5bff-356">复制 ADO.NET 连接字符串，并将值粘贴到 app.config 文件中。</span><span class="sxs-lookup"><span data-stu-id="d5bff-356">Copy the ADO.NET connection string and paste the value into the app.config file.</span></span> <span data-ttu-id="d5bff-357">\_用您的数据库密码替换 "{您在此处输入密码 \_ }"。</span><span class="sxs-lookup"><span data-stu-id="d5bff-357">Replace "{your\_password\_here}" with your database password.</span></span> <span data-ttu-id="d5bff-358"> (假设你使用脚本来部署 MVC 应用，则在脚本参数中指定了数据库密码 `SqlDatabasePassword` 。 ) </span><span class="sxs-lookup"><span data-stu-id="d5bff-358">(Assuming you used the scripts to deploy the MVC app, you specified the database password in the `SqlDatabasePassword` script parameter.)</span></span>

<span data-ttu-id="d5bff-359">结果应该如下所示：</span><span class="sxs-lookup"><span data-stu-id="d5bff-359">The result should look like the following:</span></span>

[!code-xml[Main](the-fix-it-sample-application/samples/sample32.xml)]

<span data-ttu-id="d5bff-360">在同一 MyFixIt.WorkerRole\app.config 文件中的下， `appSettings` 将 Azure 存储帐户的两个占位符值替换为。</span><span class="sxs-lookup"><span data-stu-id="d5bff-360">In the same MyFixIt.WorkerRole\app.config file, under `appSettings`, replace the two placeholder values for the Azure storage account.</span></span>

[!code-xml[Main](the-fix-it-sample-application/samples/sample33.xml?highlight=2-3)]

<span data-ttu-id="d5bff-361">可以从门户获取访问密钥。</span><span class="sxs-lookup"><span data-stu-id="d5bff-361">You can get the access key from the portal.</span></span> <span data-ttu-id="d5bff-362">请参阅 [如何管理存储帐户](https://docs.microsoft.com/azure/storage/common/storage-create-storage-account)。</span><span class="sxs-lookup"><span data-stu-id="d5bff-362">See [How To Manage Storage Accounts](https://docs.microsoft.com/azure/storage/common/storage-create-storage-account).</span></span>

<span data-ttu-id="d5bff-363">在 MyFixItCloudService\ServiceConfiguration.Cloud.cscfg 中，将相同的两个占位符值替换为 Azure 存储帐户。</span><span class="sxs-lookup"><span data-stu-id="d5bff-363">In MyFixItCloudService\ServiceConfiguration.Cloud.cscfg, replace the same two placeholders values for the Azure storage account.</span></span>

[!code-xml[Main](the-fix-it-sample-application/samples/sample34.xml?highlight=3)]

<span data-ttu-id="d5bff-364">现在，你已准备好部署云服务。</span><span class="sxs-lookup"><span data-stu-id="d5bff-364">Now you are ready to deploy the cloud service.</span></span> <span data-ttu-id="d5bff-365">在解决方案浏览器中，右键单击 MyFixItCloudService 项目，然后选择 " **发布**"。</span><span class="sxs-lookup"><span data-stu-id="d5bff-365">In Solution Explore, right-click the MyFixItCloudService project and select **Publish**.</span></span> <span data-ttu-id="d5bff-366">有关详细信息，请参阅[本教程](https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36)第2部分中的 "将[应用程序部署到 Azure](https://www.windowsazure.com/develop/net/tutorials/multi-tier-web-site/2-download-and-run/#deployAz)"。</span><span class="sxs-lookup"><span data-stu-id="d5bff-366">For more information, see "[Deploy the Application to Azure](https://www.windowsazure.com/develop/net/tutorials/multi-tier-web-site/2-download-and-run/#deployAz)", which is in part 2 of [this tutorial](https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36).</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="d5bff-367">上一页</span><span class="sxs-lookup"><span data-stu-id="d5bff-367">Previous</span></span>](more-patterns-and-guidance.md)

---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/the-fix-it-sample-application
title: 附录： 修复它示例应用程序（使用 Azure 构建真实世界的云应用程序） |微软文档
author: MikeWasson
description: 使用 Azure 电子书构建真实世界云应用基于 Scott Guthrie 开发的演示文稿。 它解释了13种模式和做法，他可以...
ms.author: riande
ms.date: 06/12/2014
ms.assetid: 1bc333c5-f096-4ea7-b170-779accc21c1a
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/the-fix-it-sample-application
msc.type: authoredcontent
ms.openlocfilehash: 896196bdb6a6b0d12a6c798ead510e37dd38a9fc
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675633"
---
# <a name="appendix-the-fix-it-sample-application-building-real-world-cloud-apps-with-azure"></a><span data-ttu-id="d10eb-104">附录：修复它示例应用程序（使用 Azure 构建真实世界的云应用程序）</span><span class="sxs-lookup"><span data-stu-id="d10eb-104">Appendix: The Fix It Sample Application (Building Real-World Cloud Apps with Azure)</span></span>

<span data-ttu-id="d10eb-105">由[迈克·瓦森](https://github.com/MikeWasson)，[里克·安德森](https://twitter.com/RickAndMSFT)，[汤姆·戴克斯特拉](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="d10eb-105">by [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson](https://twitter.com/RickAndMSFT), [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="d10eb-106">下载修复它项目</span><span class="sxs-lookup"><span data-stu-id="d10eb-106">Download The Fix It Project</span></span>](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)

> <span data-ttu-id="d10eb-107">使用 Azure 电子书**构建真实世界云应用**基于 Scott Guthrie 开发的演示文稿。</span><span class="sxs-lookup"><span data-stu-id="d10eb-107">The **Building Real World Cloud Apps with Azure** e-book is based on a presentation developed by Scott Guthrie.</span></span> <span data-ttu-id="d10eb-108">它解释了 13 种模式和做法，这些模式和做法可以帮助您成功开发云的 Web 应用。</span><span class="sxs-lookup"><span data-stu-id="d10eb-108">It explains 13 patterns and practices that can help you be successful developing web apps for the cloud.</span></span> <span data-ttu-id="d10eb-109">有关电子书的信息，请参阅[第一章](introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="d10eb-109">For information about the e-book, see [the first chapter](introduction.md).</span></span>

<span data-ttu-id="d10eb-110">使用 Azure 电子书构建真实世界云应用的此附录包含以下部分，这些部分提供有关"修复它"示例应用程序的其他信息，您可以下载：</span><span class="sxs-lookup"><span data-stu-id="d10eb-110">This appendix to the Building Real World Cloud Apps with Azure e-book contains the following sections that provide additional information about the Fix It sample application that you can download:</span></span>

- [<span data-ttu-id="d10eb-111">已知问题</span><span class="sxs-lookup"><span data-stu-id="d10eb-111">Known issues</span></span>](#knownissues)
- [<span data-ttu-id="d10eb-112">最佳做法</span><span class="sxs-lookup"><span data-stu-id="d10eb-112">Best practices</span></span>](#bestpractices)
- [<span data-ttu-id="d10eb-113">如何从本地计算机上的 Visual Studio 运行应用</span><span class="sxs-lookup"><span data-stu-id="d10eb-113">How to run the app from Visual Studio on your local computer</span></span>](#run-in-vs)
- [<span data-ttu-id="d10eb-114">如何使用 Windows PowerShell 脚本将基本应用部署到 Azure 应用服务 Web 应用</span><span class="sxs-lookup"><span data-stu-id="d10eb-114">How to deploy the base app to Azure App Service Web Apps by using the Windows PowerShell scripts</span></span>](#deploybase)
- [<span data-ttu-id="d10eb-115">对 Windows 电源外壳脚本进行故障排除</span><span class="sxs-lookup"><span data-stu-id="d10eb-115">Troubleshooting the Windows PowerShell scripts</span></span>](#troubleshooting)
- [<span data-ttu-id="d10eb-116">如何将具有队列处理的应用部署到 Azure 应用服务 Web 应用和 Azure 云服务</span><span class="sxs-lookup"><span data-stu-id="d10eb-116">How to deploy the app with queue processing to Azure App Service Web Apps and an Azure Cloud Service</span></span>](#deployqueues)

<a id="knownissues"></a>
## <a name="known-issues"></a><span data-ttu-id="d10eb-117">已知问题</span><span class="sxs-lookup"><span data-stu-id="d10eb-117">Known issues</span></span>

<span data-ttu-id="d10eb-118">Fix It 应用程序最初是为了尽可能简单地说明本电子书中介绍的一些模式而开发的。</span><span class="sxs-lookup"><span data-stu-id="d10eb-118">The Fix It app was originally developed in order to illustrate as simply as possible some of the patterns presented in this e-book.</span></span> <span data-ttu-id="d10eb-119">但是，由于电子书是关于构建真实世界的应用程序，因此我们进行了修复 It 代码的审核和测试过程，类似于我们为发布软件所做的操作。</span><span class="sxs-lookup"><span data-stu-id="d10eb-119">However, since the e-book is about building real-world apps, we subjected the Fix It code to a review and testing process similar to what we'd do for released software.</span></span> <span data-ttu-id="d10eb-120">我们发现了一些问题，与任何实际应用程序一样，我们修复了其中一些问题，其中一些问题被推迟到以后的版本中。</span><span class="sxs-lookup"><span data-stu-id="d10eb-120">We found a number of issues, and as with any real-world application, some of them we fixed and some of them we deferred to a later release.</span></span>

<span data-ttu-id="d10eb-121">以下列表包括应在生产应用程序中解决的问题，但由于以下原因，我们决定在 Fix It 示例应用程序的初始版本中不解决。</span><span class="sxs-lookup"><span data-stu-id="d10eb-121">The following list includes issues that should be addressed in a production application, but for one reason or another we decided not to address in the initial release of the Fix It sample application.</span></span>

### <a name="security"></a><span data-ttu-id="d10eb-122">安全性</span><span class="sxs-lookup"><span data-stu-id="d10eb-122">Security</span></span>

- <span data-ttu-id="d10eb-123">确保无法将任务分配给不存在的所有者。</span><span class="sxs-lookup"><span data-stu-id="d10eb-123">Ensure that you can't assign a task to a non-existent owner.</span></span>
- <span data-ttu-id="d10eb-124">确保只能查看和修改您创建或分配给您的任务。</span><span class="sxs-lookup"><span data-stu-id="d10eb-124">Ensure that you can only view and modify tasks that you created or are assigned to you.</span></span>
- <span data-ttu-id="d10eb-125">将 HTTPS 用于登录页面和身份验证 Cookie。</span><span class="sxs-lookup"><span data-stu-id="d10eb-125">Use HTTPS for sign-in pages and authentication cookies.</span></span>
- <span data-ttu-id="d10eb-126">指定身份验证 Cookie 的时间限制。</span><span class="sxs-lookup"><span data-stu-id="d10eb-126">Specify a time limit for authentication cookies.</span></span>

### <a name="input-validation"></a><span data-ttu-id="d10eb-127">输入验证</span><span class="sxs-lookup"><span data-stu-id="d10eb-127">Input validation</span></span>

<span data-ttu-id="d10eb-128">通常，生产应用执行比修复它应用更多的输入验证。</span><span class="sxs-lookup"><span data-stu-id="d10eb-128">In general, a production app would do more input validation than the Fix It app.</span></span> <span data-ttu-id="d10eb-129">例如，允许上载的图像大小/图像文件大小应加以限制。</span><span class="sxs-lookup"><span data-stu-id="d10eb-129">For example, the image size / image file size allowed for upload should be limited.</span></span>

### <a name="administrator-functionality"></a><span data-ttu-id="d10eb-130">管理员功能</span><span class="sxs-lookup"><span data-stu-id="d10eb-130">Administrator functionality</span></span>

<span data-ttu-id="d10eb-131">管理员应该能够更改现有任务的所有权。</span><span class="sxs-lookup"><span data-stu-id="d10eb-131">An administrator should be able to change ownership on existing tasks.</span></span> <span data-ttu-id="d10eb-132">例如，任务的创建者可能会离开公司，除非启用了管理访问，否则任何人都无权维护该任务。</span><span class="sxs-lookup"><span data-stu-id="d10eb-132">For example, the creator of a task might leave the company, leaving no one with authority to maintain the task unless administrative access is enabled.</span></span>

### <a name="queue-message-processing"></a><span data-ttu-id="d10eb-133">队列消息处理</span><span class="sxs-lookup"><span data-stu-id="d10eb-133">Queue message processing</span></span>

<span data-ttu-id="d10eb-134">修复 It 应用中的队列消息处理设计为简单，以便用最少的代码来说明以队列为中心的工作模式。</span><span class="sxs-lookup"><span data-stu-id="d10eb-134">Queue message processing in the Fix It app was designed to be simple in order to illustrate the queue-centric work pattern with a minimum amount of code.</span></span> <span data-ttu-id="d10eb-135">此简单代码不足以用于实际生产应用程序。</span><span class="sxs-lookup"><span data-stu-id="d10eb-135">This simple code would not be adequate for an actual production application.</span></span>

- <span data-ttu-id="d10eb-136">该代码不保证最多处理一次每个队列消息。</span><span class="sxs-lookup"><span data-stu-id="d10eb-136">The code does not guarantee that each queue message will be processed at most once.</span></span> <span data-ttu-id="d10eb-137">当您从队列中收到消息时，有一个超时期间，在此期间消息对其他队列侦听器不可见。</span><span class="sxs-lookup"><span data-stu-id="d10eb-137">When you get a message from the queue, there is a timeout period, during which the message is invisible to other queue listeners.</span></span> <span data-ttu-id="d10eb-138">如果超时在删除邮件之前过期，则消息将再次可见。</span><span class="sxs-lookup"><span data-stu-id="d10eb-138">If the timeout expires before the message is deleted, the message becomes visible again.</span></span> <span data-ttu-id="d10eb-139">因此，如果辅助角色实例花费很长时间来处理消息，则从理论上讲，同一消息可以处理两次，从而导致数据库中出现重复的任务。</span><span class="sxs-lookup"><span data-stu-id="d10eb-139">Therefore, if a worker role instance spends a long time processing a message, it is theoretically possible for the same message to get processed twice, resulting in a duplicate task in the database.</span></span> <span data-ttu-id="d10eb-140">有关此问题的详细信息，请参阅[使用 Azure 存储队列](https://msdn.microsoft.com/library/ff803365.aspx#sec7)。</span><span class="sxs-lookup"><span data-stu-id="d10eb-140">For more information about this issue, see [Using Azure Storage Queues](https://msdn.microsoft.com/library/ff803365.aspx#sec7).</span></span>
- <span data-ttu-id="d10eb-141">通过批处理消息检索，队列轮询逻辑可能更具成本效益。</span><span class="sxs-lookup"><span data-stu-id="d10eb-141">The queue polling logic could be more cost-effective, by batching message retrieval.</span></span> <span data-ttu-id="d10eb-142">每次调用[CloudQueue.GetMessageasync](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.getmessageasync.aspx)时，都会有一个交易成本。</span><span class="sxs-lookup"><span data-stu-id="d10eb-142">Every time you call [CloudQueue.GetMessageAsync](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.getmessageasync.aspx), there is a transaction cost.</span></span> <span data-ttu-id="d10eb-143">相反，您可以调用[CloudQueue.GetMessagesAsync（](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.getmessagesasync.aspx)请注意复数""），在单个事务中获取多条消息。</span><span class="sxs-lookup"><span data-stu-id="d10eb-143">Instead, you can call [CloudQueue.GetMessagesAsync](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.getmessagesasync.aspx) (note the plural 's'), which gets multiple messages in a single transaction.</span></span> <span data-ttu-id="d10eb-144">Azure 存储队列的事务成本非常低，因此在大多数情况下，对成本的影响并不大。</span><span class="sxs-lookup"><span data-stu-id="d10eb-144">The transaction costs for Azure Storage Queues are very low, so the impact on costs is not substantial in most scenarios.</span></span>
- <span data-ttu-id="d10eb-145">队列消息处理代码中的紧密循环会导致 CPU 关联性，而 CPU 关联性不会有效地利用多核 VM。</span><span class="sxs-lookup"><span data-stu-id="d10eb-145">The tight loop in the queue message-processing code causes CPU affinity, which does not utilize multi-core VMs efficiently.</span></span> <span data-ttu-id="d10eb-146">更好的设计将使用任务并行性并行运行多个异步任务。</span><span class="sxs-lookup"><span data-stu-id="d10eb-146">A better design would use task parallelism to run several async tasks in parallel.</span></span>
- <span data-ttu-id="d10eb-147">队列消息处理只有基本的异常处理。</span><span class="sxs-lookup"><span data-stu-id="d10eb-147">Queue message-processing has only rudimentary exception handling.</span></span> <span data-ttu-id="d10eb-148">例如，代码不处理[有害消息](https://msdn.microsoft.com/library/ms789028.aspx)。</span><span class="sxs-lookup"><span data-stu-id="d10eb-148">For example, the code doesn't handle [poison messages](https://msdn.microsoft.com/library/ms789028.aspx).</span></span> <span data-ttu-id="d10eb-149">（当消息处理导致异常时，您必须记录错误并删除消息，否则辅助角色将再次尝试处理该错误，并且循环将无限期地继续。</span><span class="sxs-lookup"><span data-stu-id="d10eb-149">(When message processing causes an exception, you have to log the error and delete the message, or the worker role will try to process it again, and the loop will continue indefinitely.)</span></span>

### <a name="sql-queries-are-unbounded"></a><span data-ttu-id="d10eb-150">SQL 查询未绑定</span><span class="sxs-lookup"><span data-stu-id="d10eb-150">SQL queries are unbounded</span></span>

<span data-ttu-id="d10eb-151">当前修复代码对索引页的查询可能返回的行数没有限制。</span><span class="sxs-lookup"><span data-stu-id="d10eb-151">Current Fix It code places no limit on how many rows the queries for Index pages might return.</span></span> <span data-ttu-id="d10eb-152">如果数据库中输入了大量任务，则接收的结果列表的大小可能会导致性能问题。</span><span class="sxs-lookup"><span data-stu-id="d10eb-152">If a large volume of tasks is entered into the database, the size of the resulting lists received could cause performance issues.</span></span> <span data-ttu-id="d10eb-153">解决方案是实现分页。</span><span class="sxs-lookup"><span data-stu-id="d10eb-153">The solution is to implement paging.</span></span> <span data-ttu-id="d10eb-154">例如，请参阅在[ASP.NET mVC 应用程序中使用实体框架对实体框架进行排序、筛选和分页](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md)。</span><span class="sxs-lookup"><span data-stu-id="d10eb-154">For an example, see [Sorting, Filtering, and Paging with the Entity Framework in an ASP.NET MVC Application](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md).</span></span>

### <a name="view-models-recommended"></a><span data-ttu-id="d10eb-155">查看推荐的模型</span><span class="sxs-lookup"><span data-stu-id="d10eb-155">View models recommended</span></span>

<span data-ttu-id="d10eb-156">修复它应用使用 FixItTask 实体类在控制器和视图之间传递信息。</span><span class="sxs-lookup"><span data-stu-id="d10eb-156">The Fix It app uses the FixItTask entity class to pass information between the controller and the view.</span></span> <span data-ttu-id="d10eb-157">最佳做法是使用视图模型。</span><span class="sxs-lookup"><span data-stu-id="d10eb-157">A best practice is to use view models.</span></span> <span data-ttu-id="d10eb-158">域模型（例如 FixItTask 实体类）是围绕数据持久性所需的内容设计的，而视图模型可以设计为数据表示。</span><span class="sxs-lookup"><span data-stu-id="d10eb-158">The domain model (e.g., the FixItTask entity class) is designed around what is needed for data persistence, while a view model can be designed for data presentation.</span></span> <span data-ttu-id="d10eb-159">有关详细信息，请参阅[12 ASP.NET MVC 最佳实践](https://codeclimber.net.nz/archive/2009/10/27/12-asp.net-mvc-best-practices.aspx)。</span><span class="sxs-lookup"><span data-stu-id="d10eb-159">For more information, see [12 ASP.NET MVC Best Practices](https://codeclimber.net.nz/archive/2009/10/27/12-asp.net-mvc-best-practices.aspx).</span></span>

### <a name="secure-image-blob-recommended"></a><span data-ttu-id="d10eb-160">建议使用安全映像 blob</span><span class="sxs-lookup"><span data-stu-id="d10eb-160">Secure image blob recommended</span></span>

<span data-ttu-id="d10eb-161">Fix It 应用将上传的图像存储为公共图像，这意味着找到 URL 的任何人都可以访问这些图像。</span><span class="sxs-lookup"><span data-stu-id="d10eb-161">The Fix It app stores uploaded images as public, meaning that anyone who finds the URL can access the images.</span></span> <span data-ttu-id="d10eb-162">图像可以保护而不是公开。</span><span class="sxs-lookup"><span data-stu-id="d10eb-162">The images could be secured instead of public.</span></span>

### <a name="no-powershell-automation-scripts-for-queues"></a><span data-ttu-id="d10eb-163">没有用于队列的 PowerShell 自动化脚本</span><span class="sxs-lookup"><span data-stu-id="d10eb-163">No PowerShell automation scripts for queues</span></span>

<span data-ttu-id="d10eb-164">示例 PowerShell 自动化脚本仅针对完全在 Azure 应用服务 Web 应用中运行的修复它的基本版本编写。</span><span class="sxs-lookup"><span data-stu-id="d10eb-164">Sample PowerShell automation scripts were written only for the base version of Fix It that runs entirely in Azure App Service Web Apps.</span></span> <span data-ttu-id="d10eb-165">我们没有提供用于设置和部署到 Web 应用以及队列处理所需的云服务环境的脚本。</span><span class="sxs-lookup"><span data-stu-id="d10eb-165">We haven't provided scripts for setting up and deploying to the web app plus Cloud Service environment required for queue processing.</span></span>

### <a name="special-handling-for-html-codes-in-user-input"></a><span data-ttu-id="d10eb-166">用户输入中 HTML 代码的特殊处理</span><span class="sxs-lookup"><span data-stu-id="d10eb-166">Special handling for HTML codes in user input</span></span>

<span data-ttu-id="d10eb-167">ASP.NET通过在用户输入文本框中输入脚本，自动防止恶意用户尝试跨站点脚本攻击的多种方式。</span><span class="sxs-lookup"><span data-stu-id="d10eb-167">ASP.NET automatically prevents many ways in which malicious users might attempt cross-site scripting attacks by entering script in user input text boxes.</span></span> <span data-ttu-id="d10eb-168">MVC`DisplayFor`帮助程序用于显示任务标题和注释，自动对其进行 HTML 编码它发送到浏览器的值。</span><span class="sxs-lookup"><span data-stu-id="d10eb-168">And the MVC `DisplayFor` helper used to display task titles and notes automatically HTML-encodes values that it sends to the browser.</span></span> <span data-ttu-id="d10eb-169">但在生产应用中，您可能需要采取其他措施。</span><span class="sxs-lookup"><span data-stu-id="d10eb-169">But in a production app you might want to take additional measures.</span></span> <span data-ttu-id="d10eb-170">有关详细信息，请参阅ASP.NET[中的请求验证](https://msdn.microsoft.com/library/hh882339.aspx)。</span><span class="sxs-lookup"><span data-stu-id="d10eb-170">For more information, see [Request Validation in ASP.NET](https://msdn.microsoft.com/library/hh882339.aspx).</span></span>

<a id="bestpractices"></a>
## <a name="best-practices"></a><span data-ttu-id="d10eb-171">最佳做法</span><span class="sxs-lookup"><span data-stu-id="d10eb-171">Best practices</span></span>

<span data-ttu-id="d10eb-172">以下是在修复 It 应用的原始版本的代码审查和测试中发现后修复的一些问题。</span><span class="sxs-lookup"><span data-stu-id="d10eb-172">Following are some issues that were fixed after being discovered in code review and testing of the original version of the Fix It app.</span></span> <span data-ttu-id="d10eb-173">有些是由于原始编码器不知道特定的最佳实践造成的，有些只是因为代码编写得很快，并非针对发布的软件。</span><span class="sxs-lookup"><span data-stu-id="d10eb-173">Some were caused by the original coder not being aware of a particular best practice, some simply because the code was written quickly and wasn't intended for released software.</span></span> <span data-ttu-id="d10eb-174">我们在这里列出问题，以防我们从这次审查和测试中学到的东西对正在开发 Web 应用程序的其他人有帮助。</span><span class="sxs-lookup"><span data-stu-id="d10eb-174">We're listing the issues here in case there's something we learned from this review and testing that might be helpful to others who are also developing web apps.</span></span>

### <a name="dispose-the-database-repository"></a><span data-ttu-id="d10eb-175">处置数据库存储库</span><span class="sxs-lookup"><span data-stu-id="d10eb-175">Dispose the database repository</span></span>

<span data-ttu-id="d10eb-176">类`FixItTaskRepository`必须释放实体框架`DbContext`实例。</span><span class="sxs-lookup"><span data-stu-id="d10eb-176">The `FixItTaskRepository` class must dispose the Entity Framework `DbContext` instance.</span></span> <span data-ttu-id="d10eb-177">我们通过在`FixItTaskRepository`类中实现`IDisposable`来实现此情况：</span><span class="sxs-lookup"><span data-stu-id="d10eb-177">We did this by implementing `IDisposable` in the `FixItTaskRepository` class:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample1.cs)]

<span data-ttu-id="d10eb-178">请注意，AutoFac 将自动释放`FixItTaskRepository`实例，因此我们不需要显式处置它。</span><span class="sxs-lookup"><span data-stu-id="d10eb-178">Note that AutoFac will automatically dispose the `FixItTaskRepository` instance, so we don't need to explicitly dispose it.</span></span>

<span data-ttu-id="d10eb-179">另一个选项是从 中删除`DbContext`成员变量`FixItTaskRepository`，而是在 语句内在每个`DbContext`存储库方法中创建一个`using`局部变量。</span><span class="sxs-lookup"><span data-stu-id="d10eb-179">Another option is to remove the `DbContext` member variable from `FixItTaskRepository`, and instead create a local `DbContext` variable within each repository method, inside a `using` statement.</span></span> <span data-ttu-id="d10eb-180">例如：</span><span class="sxs-lookup"><span data-stu-id="d10eb-180">For example:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample2.cs)]

### <a name="register-singletons-as-such-with-di"></a><span data-ttu-id="d10eb-181">使用 DI 注册单例</span><span class="sxs-lookup"><span data-stu-id="d10eb-181">Register singletons as such with DI</span></span>

<span data-ttu-id="d10eb-182">由于只需要`PhotoService`类和`Logger`类的一个实例，因此这些类应注册为*DependenciesConfig.cs*[中依赖项注入的单个实例](https://code.google.com/p/autofac/wiki/InstanceScope)：</span><span class="sxs-lookup"><span data-stu-id="d10eb-182">Since only one instance of the `PhotoService` class and `Logger` class is needed, these classes should be [registered as single instances for dependency injection](https://code.google.com/p/autofac/wiki/InstanceScope) in *DependenciesConfig.cs*:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample3.cs?highlight=1,3)]

### <a name="security-dont-show-error-details-to-users"></a><span data-ttu-id="d10eb-183">安全性：不向用户显示错误详细信息</span><span class="sxs-lookup"><span data-stu-id="d10eb-183">Security: Don't show error details to users</span></span>

<span data-ttu-id="d10eb-184">原始修复 It 应用没有通用错误页，只是让所有异常都冒泡到 UI 上，因此某些异常（如数据库连接错误）可能会导致向浏览器显示完整的堆栈跟踪。</span><span class="sxs-lookup"><span data-stu-id="d10eb-184">The original Fix It app didn't have a generic error page and just let all exceptions bubble up to the UI, so some exceptions such as database connection errors could result in a full stack trace being displayed to the browser.</span></span> <span data-ttu-id="d10eb-185">详细的错误信息有时可能促进恶意用户的攻击。</span><span class="sxs-lookup"><span data-stu-id="d10eb-185">Detailed error information can sometimes facilitate attacks by malicious users.</span></span> <span data-ttu-id="d10eb-186">解决方案是记录异常详细信息，并将错误页显示给不包含错误详细信息的用户。</span><span class="sxs-lookup"><span data-stu-id="d10eb-186">The solution is to log the exception details and display an error page to the user that doesn't include error details.</span></span> <span data-ttu-id="d10eb-187">修复它应用已经记录，为了显示错误页面，我们添加了`<customErrors mode=On>`Web.config 文件。</span><span class="sxs-lookup"><span data-stu-id="d10eb-187">The Fix It app was already logging, and in order to display an error page, we added `<customErrors mode=On>` in the Web.config file.</span></span>

[!code-xml[Main](the-fix-it-sample-application/samples/sample4.xml?highlight=2)]

<span data-ttu-id="d10eb-188">默认情况下，这将导致*显示视图\共享\Error.cshtml*以查找错误。</span><span class="sxs-lookup"><span data-stu-id="d10eb-188">By default this causes *Views\Shared\Error.cshtml* to be displayed for errors.</span></span> <span data-ttu-id="d10eb-189">您可以自定义*Error.cshtml*或创建自己的错误页面视图并添加`defaultRedirect`属性。</span><span class="sxs-lookup"><span data-stu-id="d10eb-189">You can customize *Error.cshtml* or create your own error page view and add a `defaultRedirect` attribute.</span></span> <span data-ttu-id="d10eb-190">您还可以为特定错误指定不同的错误页。</span><span class="sxs-lookup"><span data-stu-id="d10eb-190">You can also specify different error pages for specific errors.</span></span>

### <a name="security-only-allow-a-task-to-be-edited-by-its-creator"></a><span data-ttu-id="d10eb-191">安全性：仅允许其创建者编辑任务</span><span class="sxs-lookup"><span data-stu-id="d10eb-191">Security: only allow a task to be edited by its creator</span></span>

<span data-ttu-id="d10eb-192">"仪表板索引"页仅显示登录用户创建的任务，但恶意用户可以创建具有其他用户任务的 ID 的 URL。</span><span class="sxs-lookup"><span data-stu-id="d10eb-192">The Dashboard Index page only shows tasks created by the logged-on user, but a malicious user could create a URL with an ID to another user's task.</span></span> <span data-ttu-id="d10eb-193">我们*DashboardController.cs中*添加了代码，以在这种情况下返回 404：</span><span class="sxs-lookup"><span data-stu-id="d10eb-193">We added code in *DashboardController.cs* to return a 404 in that case:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample5.cs?highlight=9-14,24-29)]

### <a name="dont-swallow-exceptions"></a><span data-ttu-id="d10eb-194">不要吞咽异常</span><span class="sxs-lookup"><span data-stu-id="d10eb-194">Don't swallow exceptions</span></span>

<span data-ttu-id="d10eb-195">原始修复 It 应用在记录 SQL 查询产生的异常后刚刚返回 null：</span><span class="sxs-lookup"><span data-stu-id="d10eb-195">The original Fix It app just returned null after logging an exception that resulted from a SQL query:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample6.cs?highlight=4)]

<span data-ttu-id="d10eb-196">这将使用户看起来好像查询成功，但只是没有返回任何行。</span><span class="sxs-lookup"><span data-stu-id="d10eb-196">This would make it look to the user as if the query succeeded but just didn't return any rows.</span></span> <span data-ttu-id="d10eb-197">解决方案是在捕获和日志记录后重新引发异常：</span><span class="sxs-lookup"><span data-stu-id="d10eb-197">Solution is to re-throw the exception after catching and logging:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample7.cs)]

### <a name="catch-all-exceptions-in-worker-roles"></a><span data-ttu-id="d10eb-198">捕获辅助角色中的所有异常</span><span class="sxs-lookup"><span data-stu-id="d10eb-198">Catch all exceptions in worker roles</span></span>

<span data-ttu-id="d10eb-199">辅助角色中的任何未处理异常都将导致 VM 被回收，因此您希望在 try-catch 块中包装所有操作，并处理所有异常。</span><span class="sxs-lookup"><span data-stu-id="d10eb-199">Any unhandled exceptions in a worker role will cause the VM to be recycled, so you want to wrap everything you do in a try-catch block and handle all exceptions.</span></span>

### <a name="specify-length-for-string-properties-in-entity-classes"></a><span data-ttu-id="d10eb-200">指定实体类中字符串属性的长度</span><span class="sxs-lookup"><span data-stu-id="d10eb-200">Specify length for string properties in entity classes</span></span>

<span data-ttu-id="d10eb-201">为了显示简单代码，修复它应用的原始版本没有指定 FixItTask 实体字段的长度，因此在数据库中将其定义为 varchar（max）。</span><span class="sxs-lookup"><span data-stu-id="d10eb-201">In order to display simple code, the original version of the Fix It app didn't specify lengths for the fields of the FixItTask entity, and as a result they were defined as varchar(max) in the database.</span></span> <span data-ttu-id="d10eb-202">因此，UI 将接受几乎任何数量的输入。</span><span class="sxs-lookup"><span data-stu-id="d10eb-202">As a result, the UI would accept almost any amount of input.</span></span> <span data-ttu-id="d10eb-203">指定长度设置适用于网页中的用户输入和数据库中的列大小的限制：</span><span class="sxs-lookup"><span data-stu-id="d10eb-203">Specifying lengths sets limits that apply both to user input in the web page and column size in the database:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample8.cs?highlight=4,7,10,12,14)]

### <a name="mark-private-members-as-readonly-when-they-arent-expected-to-change"></a><span data-ttu-id="d10eb-204">当私人成员不需要更改时，将它们标记为只读</span><span class="sxs-lookup"><span data-stu-id="d10eb-204">Mark private members as readonly when they aren't expected to change</span></span>

<span data-ttu-id="d10eb-205">例如，在类中`DashboardController`，将创建`FixItTaskRepository`一个实例，并且不需要更改，所以我们将其定义为[只读](https://msdn.microsoft.com/library/acdd6hb7.aspx)。</span><span class="sxs-lookup"><span data-stu-id="d10eb-205">For example, in the `DashboardController` class an instance of `FixItTaskRepository` is created and isn't expected to change, so we defined it as [readonly](https://msdn.microsoft.com/library/acdd6hb7.aspx).</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample9.cs?highlight=3)]

### <a name="use-listany-instead-of-listcount-gt-0"></a><span data-ttu-id="d10eb-206">使用列表。任何（）而不是列表。计数（） &gt; 0</span><span class="sxs-lookup"><span data-stu-id="d10eb-206">Use list.Any() instead of list.Count() &gt; 0</span></span>

<span data-ttu-id="d10eb-207">如果您所关心的只是列表中的一个或多个项是否符合指定的条件，请使用[Any](https://msdn.microsoft.com/library/bb534972.aspx)方法，因为它在找到符合条件的项后立即返回，而`Count`该方法始终必须遍遍遍每个项。</span><span class="sxs-lookup"><span data-stu-id="d10eb-207">If you all you care about is whether one or more items in a list fit the specified criteria, use the [Any](https://msdn.microsoft.com/library/bb534972.aspx) method, because it returns as soon as an item fitting the criteria is found, whereas the `Count` method always has to iterate through every item.</span></span> <span data-ttu-id="d10eb-208">仪表板*索引.cshtml*文件最初具有以下代码：</span><span class="sxs-lookup"><span data-stu-id="d10eb-208">The Dashboard *Index.cshtml* file originally had this code:</span></span>

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample10.cshtml)]

<span data-ttu-id="d10eb-209">我们将其更改为：</span><span class="sxs-lookup"><span data-stu-id="d10eb-209">We changed it to this:</span></span>

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample11.cshtml?highlight=1)]

### <a name="generate-urls-in-mvc-views-using-mvc-helpers"></a><span data-ttu-id="d10eb-210">使用 MVC 帮助器在 MVC 视图中生成 URL</span><span class="sxs-lookup"><span data-stu-id="d10eb-210">Generate URLs in MVC views using MVC helpers</span></span>

<span data-ttu-id="d10eb-211">对于主页上的"**修复 It"** 按钮，"修复它"应用硬编码锚点元素：</span><span class="sxs-lookup"><span data-stu-id="d10eb-211">For the **Create a Fix It** button on the home page, the Fix It app hard coded an anchor element:</span></span>

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample12.cshtml)]

<span data-ttu-id="d10eb-212">对于像这样的视图/操作链接，最好使用[Url.Action](https://msdn.microsoft.com/library/system.web.mvc.urlhelper.action.aspx) HTML 帮助程序，例如：</span><span class="sxs-lookup"><span data-stu-id="d10eb-212">For View/Action links like this it's better to use the [Url.Action](https://msdn.microsoft.com/library/system.web.mvc.urlhelper.action.aspx) HTML helper, for example:</span></span>

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample13.cshtml)]

### <a name="use-taskdelay-instead-of-threadsleep-in-worker-role"></a><span data-ttu-id="d10eb-213">使用任务.延迟而不是线程.睡眠在辅助角色中</span><span class="sxs-lookup"><span data-stu-id="d10eb-213">Use Task.Delay instead of Thread.Sleep in worker role</span></span>

<span data-ttu-id="d10eb-214">新项目模板将工作角色的示例`Thread.Sleep`代码放入其中，但导致线程处于睡眠状态可能会导致线程池生成其他不必要的线程。</span><span class="sxs-lookup"><span data-stu-id="d10eb-214">The new-project template puts `Thread.Sleep` in the sample code for a worker role, but causing the thread to sleep can cause the thread pool to spawn additional unnecessary threads.</span></span> <span data-ttu-id="d10eb-215">您可以使用[Task.delay](https://msdn.microsoft.com/library/hh139096.aspx)来避免这种情况。</span><span class="sxs-lookup"><span data-stu-id="d10eb-215">You can avoid that by using [Task.Delay](https://msdn.microsoft.com/library/hh139096.aspx) instead.</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample14.cs?highlight=11)]

### <a name="avoid-async-void"></a><span data-ttu-id="d10eb-216">避免异步空隙</span><span class="sxs-lookup"><span data-stu-id="d10eb-216">Avoid async void</span></span>

<span data-ttu-id="d10eb-217">如果异步方法不需要返回值，则返回类型`Task`而不是`void`。</span><span class="sxs-lookup"><span data-stu-id="d10eb-217">If an async method doesn't need to return a value, return a `Task` type rather than `void`.</span></span>

<span data-ttu-id="d10eb-218">此示例来自类`FixItQueueManager`：</span><span class="sxs-lookup"><span data-stu-id="d10eb-218">This example is from the `FixItQueueManager` class:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample15.cs)]

<span data-ttu-id="d10eb-219">应仅对`async void`顶级事件处理程序使用。</span><span class="sxs-lookup"><span data-stu-id="d10eb-219">You should use `async void` only for top-level event handlers.</span></span> <span data-ttu-id="d10eb-220">如果将方法定义为`async void`，调用方无法**等待**该方法或捕获方法引发的任何异常。</span><span class="sxs-lookup"><span data-stu-id="d10eb-220">If you define a method as `async void`, the caller cannot **await** the method or catch any exceptions the method throws.</span></span> <span data-ttu-id="d10eb-221">有关详细信息，请参阅[异步编程中的最佳做法](https://msdn.microsoft.com/magazine/jj991977.aspx)。</span><span class="sxs-lookup"><span data-stu-id="d10eb-221">For more information, see [Best Practices in Asynchronous Programming](https://msdn.microsoft.com/magazine/jj991977.aspx).</span></span>

### <a name="use-a-cancellation-token-to-break-from-worker-role-loop"></a><span data-ttu-id="d10eb-222">使用取消令牌从辅助角色循环中断</span><span class="sxs-lookup"><span data-stu-id="d10eb-222">Use a cancellation token to break from worker role loop</span></span>

<span data-ttu-id="d10eb-223">通常，辅助角色上的**Run**方法包含无限循环。</span><span class="sxs-lookup"><span data-stu-id="d10eb-223">Typically, the **Run** method on a worker role contains an infinite loop.</span></span> <span data-ttu-id="d10eb-224">当辅助角色停止时，将调用[角色入口点.onStop](https://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstop.aspx)方法。</span><span class="sxs-lookup"><span data-stu-id="d10eb-224">When the worker role is stopping, the [RoleEntryPoint.OnStop](https://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstop.aspx) method is called.</span></span> <span data-ttu-id="d10eb-225">应使用此方法取消在**Run**方法内完成的工作并正常退出。</span><span class="sxs-lookup"><span data-stu-id="d10eb-225">You should use this method to cancel the work that is being done inside the **Run** method and exit gracefully.</span></span> <span data-ttu-id="d10eb-226">否则，进程可能在操作过程中终止。</span><span class="sxs-lookup"><span data-stu-id="d10eb-226">Otherwise, the process might be terminated in the middle of an operation.</span></span>

### <a name="opt-out-of-automatic-mime-sniffing-procedure"></a><span data-ttu-id="d10eb-227">选择退出自动 MIME 嗅探过程</span><span class="sxs-lookup"><span data-stu-id="d10eb-227">Opt out of Automatic MIME Sniffing Procedure</span></span>

<span data-ttu-id="d10eb-228">在某些情况下，Internet Explorer 报告 MIME 类型与 Web 服务器指定的类型不同。</span><span class="sxs-lookup"><span data-stu-id="d10eb-228">In some cases, Internet Explorer reports a MIME type different than the type specified by the web server.</span></span> <span data-ttu-id="d10eb-229">例如，如果 Internet Explorer 在使用 HTTP 响应标头内容类型：文本/纯文交付的文件中查找 HTML 内容，则 Internet Explorer 确定内容应呈现为 HTML。</span><span class="sxs-lookup"><span data-stu-id="d10eb-229">For instance, if Internet Explorer finds HTML content in a file delivered with the HTTP response header Content-Type: text/plain, Internet Explorer determines that the content should be rendered as HTML.</span></span> <span data-ttu-id="d10eb-230">遗憾的是，这种"MIME 嗅探"还可能导致托管不受信任的内容的服务器出现安全问题。</span><span class="sxs-lookup"><span data-stu-id="d10eb-230">Unfortunately, this "MIME-sniffing" can also lead to security problems for servers hosting untrusted content.</span></span> <span data-ttu-id="d10eb-231">为了解决这个问题，Internet Explorer 8 对 MIME 类型的确定代码进行了一些更改，并允许应用程序开发人员[选择退出 MIME 嗅探](https://blogs.msdn.com/b/ie/archive/2008/07/02/ie8-security-part-v-comprehensive-protection.aspx)。</span><span class="sxs-lookup"><span data-stu-id="d10eb-231">To combat this problem, Internet Explorer 8 has made a number of changes to MIME-type determination code and allows application developers to [opt out of MIME-sniffing](https://blogs.msdn.com/b/ie/archive/2008/07/02/ie8-security-part-v-comprehensive-protection.aspx).</span></span> <span data-ttu-id="d10eb-232">以下代码已添加到*Web.config 文件中*。</span><span class="sxs-lookup"><span data-stu-id="d10eb-232">The following code was added to the *Web.config* file.</span></span>

[!code-xml[Main](the-fix-it-sample-application/samples/sample16.xml?highlight=2-7)]

### <a name="enable-bundling-and-minification"></a><span data-ttu-id="d10eb-233">实现捆绑和最小化</span><span class="sxs-lookup"><span data-stu-id="d10eb-233">Enable bundling and minification</span></span>

<span data-ttu-id="d10eb-234">当 Visual Studio 创建新的 Web 项目时，默认情况下不会启用 JavaScript 文件的捆绑和小化。</span><span class="sxs-lookup"><span data-stu-id="d10eb-234">When Visual Studio creates a new web project, bundling and minification of JavaScript files is not enabled by default.</span></span> <span data-ttu-id="d10eb-235">我们在BundleConfig.cs中添加了一行代码：</span><span class="sxs-lookup"><span data-stu-id="d10eb-235">We added a line of code in BundleConfig.cs:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample17.cs?highlight=9)]

### <a name="set-an-expiration-time-out-for-authentication-cookies"></a><span data-ttu-id="d10eb-236">为身份验证 Cookie 设置过期超时</span><span class="sxs-lookup"><span data-stu-id="d10eb-236">Set an expiration time-out for authentication cookies</span></span>

<span data-ttu-id="d10eb-237">默认情况下，身份验证 Cookie 将在两周后过期。</span><span class="sxs-lookup"><span data-stu-id="d10eb-237">By default, authentication cookies expire in two weeks.</span></span> <span data-ttu-id="d10eb-238">更短的时间更安全。</span><span class="sxs-lookup"><span data-stu-id="d10eb-238">A shorter time is more secure.</span></span> <span data-ttu-id="d10eb-239">您可以在*StartupAuth.cs*中更改此设置：</span><span class="sxs-lookup"><span data-stu-id="d10eb-239">You can change this setting in *StartupAuth.cs*:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample18.cs?highlight=4-5)]

<a id="run-in-vs"></a>
## <a name="how-to-run-the-app-from-visual-studio-on-your-local-computer"></a><span data-ttu-id="d10eb-240">如何从本地计算机上的 Visual Studio 运行应用</span><span class="sxs-lookup"><span data-stu-id="d10eb-240">How to run the app from Visual Studio on your local computer</span></span>

<span data-ttu-id="d10eb-241">有两种方法可以运行修复它应用：</span><span class="sxs-lookup"><span data-stu-id="d10eb-241">There are two ways to run the Fix It app:</span></span>

- <span data-ttu-id="d10eb-242">运行将新任务直接写入 SQL 数据库的基本应用程序。</span><span class="sxs-lookup"><span data-stu-id="d10eb-242">Run the base application that writes new tasks directly to the SQL database.</span></span>
- <span data-ttu-id="d10eb-243">使用队列和后端服务运行应用程序以创建任务。</span><span class="sxs-lookup"><span data-stu-id="d10eb-243">Run the application using a queue plus a backend service to create tasks.</span></span> <span data-ttu-id="d10eb-244">队列模式在以[队列为中心的工作模式](queue-centric-work-pattern.md)一章中描述。</span><span class="sxs-lookup"><span data-stu-id="d10eb-244">The queue pattern is described in the chapter [Queue-Centric Work Pattern](queue-centric-work-pattern.md).</span></span>

<a id="runbase"></a>
### <a name="run-the-base-application"></a><span data-ttu-id="d10eb-245">运行基本应用程序</span><span class="sxs-lookup"><span data-stu-id="d10eb-245">Run the base application</span></span>

1. <span data-ttu-id="d10eb-246">安装[视觉工作室 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017).</span><span class="sxs-lookup"><span data-stu-id="d10eb-246">Install [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017).</span></span>
2. <span data-ttu-id="d10eb-247">为[.NET 安装用于视觉工作室的 Azure SDK。](https://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="d10eb-247">Install the [Azure SDK for .NET for Visual Studio](https://azure.microsoft.com/downloads/).</span></span>
3. <span data-ttu-id="d10eb-248">从[MSDN 代码库](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)下载 .zip 文件。</span><span class="sxs-lookup"><span data-stu-id="d10eb-248">Download the .zip file from the [MSDN Code Gallery](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4).</span></span>
4. <span data-ttu-id="d10eb-249">在"文件资源管理器"中，右键单击 .zip 文件并单击"属性"，然后在"属性"窗口中单击"取消阻止"。</span><span class="sxs-lookup"><span data-stu-id="d10eb-249">In File Explorer, right-click the .zip file and click Properties, then in the Properties window click Unblock.</span></span>
5. <span data-ttu-id="d10eb-250">解压缩文件。</span><span class="sxs-lookup"><span data-stu-id="d10eb-250">Unzip the file.</span></span>
6. <span data-ttu-id="d10eb-251">双击 .sln 文件以启动可视化工作室。</span><span class="sxs-lookup"><span data-stu-id="d10eb-251">Double-click the .sln file to launch Visual Studio.</span></span>
7. <span data-ttu-id="d10eb-252">在 **"工具"** 菜单中，单击**NuGet 包管理器**，然后单击**包管理器控制台**。</span><span class="sxs-lookup"><span data-stu-id="d10eb-252">From the **Tools** menu, click **NuGet Package Manager**, then **Package Manager Console**.</span></span>
8. <span data-ttu-id="d10eb-253">在包管理器控制台 （PMC） 中，单击"还原"。</span><span class="sxs-lookup"><span data-stu-id="d10eb-253">In the Package Manager Console (PMC), click Restore.</span></span>
9. <span data-ttu-id="d10eb-254">退出 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="d10eb-254">Exit Visual Studio.</span></span>
10. <span data-ttu-id="d10eb-255">启动[Azure 存储模拟器](/azure/storage/common/storage-use-emulator)。</span><span class="sxs-lookup"><span data-stu-id="d10eb-255">Start the [Azure storage emulator](/azure/storage/common/storage-use-emulator).</span></span>
11. <span data-ttu-id="d10eb-256">重新启动 Visual Studio，打开在上一步中关闭的解决方案文件。</span><span class="sxs-lookup"><span data-stu-id="d10eb-256">Restart Visual Studio, opening the solution file you closed in the previous step.</span></span>
12. <span data-ttu-id="d10eb-257">确保 FixIt 项目设置为启动项目，然后按 CTRL_F5 运行该项目。</span><span class="sxs-lookup"><span data-stu-id="d10eb-257">Make sure the FixIt project is set as the startup project, and then press CTRL+F5 to run the project.</span></span>

<a id="queueslocal"></a>
### <a name="run-the-application-with-queue-processing"></a><span data-ttu-id="d10eb-258">使用队列处理运行应用程序</span><span class="sxs-lookup"><span data-stu-id="d10eb-258">Run the application with queue processing</span></span>

1. <span data-ttu-id="d10eb-259">按照[运行基本应用程序](#runbase)的说明操作，然后关闭浏览器并关闭 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="d10eb-259">Follow the directions for [Run the base application](#runbase), and then close the browser and close Visual Studio.</span></span>
2. <span data-ttu-id="d10eb-260">使用管理员权限启动可视化工作室。</span><span class="sxs-lookup"><span data-stu-id="d10eb-260">Start Visual Studio with administrator privileges.</span></span> <span data-ttu-id="d10eb-261">（您将使用 Azure 计算模拟器，这需要管理员权限。</span><span class="sxs-lookup"><span data-stu-id="d10eb-261">(You'll be using the Azure compute emulator, and that requires administrator privileges.)</span></span>
3. <span data-ttu-id="d10eb-262">在*MyFixIt*项目中的应用程序*Web.config*文件中（Web 项目），将 的值`appSettings/UseQueues`更改为"true"：</span><span class="sxs-lookup"><span data-stu-id="d10eb-262">In the application *Web.config* file in the *MyFixIt* project (the web project), change the value of `appSettings/UseQueues` to "true":</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample19.cmd?highlight=3)]
4. <span data-ttu-id="d10eb-263">如果[Azure 存储模拟器](https://msdn.microsoft.com/library/windowsazure/hh403989.aspx)未运行，则重新启动它。</span><span class="sxs-lookup"><span data-stu-id="d10eb-263">If the [Azure storage emulator](https://msdn.microsoft.com/library/windowsazure/hh403989.aspx) isn't still running, start it again.</span></span>
5. <span data-ttu-id="d10eb-264">同时运行修复 It Web 项目和 MyFixIt云服务项目。</span><span class="sxs-lookup"><span data-stu-id="d10eb-264">Run the FixIt web project and the MyFixItCloudService project simultaneously.</span></span>

    <span data-ttu-id="d10eb-265">使用 Visual Studio：</span><span class="sxs-lookup"><span data-stu-id="d10eb-265">Using Visual Studio:</span></span>

   1. <span data-ttu-id="d10eb-266">按**F5**以运行 FixIt 项目。</span><span class="sxs-lookup"><span data-stu-id="d10eb-266">Press **F5** to run the FixIt project.</span></span>
   2. <span data-ttu-id="d10eb-267">在**解决方案资源管理器**中，右键单击 MyFixIt云服务项目，然后单击 **"调试** > **启动新实例**"。</span><span class="sxs-lookup"><span data-stu-id="d10eb-267">In **Solution Explorer**, right-click the MyFixItCloudService project, and then click **Debug** > **Start New Instance**.</span></span>

    <span data-ttu-id="d10eb-268">使用可视化工作室 2013 快速网页：</span><span class="sxs-lookup"><span data-stu-id="d10eb-268">Using Visual Studio 2013 Express for Web:</span></span>

   3. <span data-ttu-id="d10eb-269">在解决方案资源管理器中，右键单击 FixIt 解决方案并选择**属性**。</span><span class="sxs-lookup"><span data-stu-id="d10eb-269">In Solution Explorer, right-click the FixIt solution and select **Properties**.</span></span>
   4. <span data-ttu-id="d10eb-270">选择**多个启动项目**。</span><span class="sxs-lookup"><span data-stu-id="d10eb-270">Select **Multiple Startup Projects**.</span></span>
   5. <span data-ttu-id="d10eb-271">在 MyFixIt 和 MyFixIt云服务下的 **"操作**"下拉列表中，选择 **"开始**"。</span><span class="sxs-lookup"><span data-stu-id="d10eb-271">In the **Action** dropdown list under MyFixIt and MyFixItCloudService, select **Start**.</span></span>
   6. <span data-ttu-id="d10eb-272">单击“确定”。 </span><span class="sxs-lookup"><span data-stu-id="d10eb-272">Click **OK**.</span></span>
   7. <span data-ttu-id="d10eb-273">按 **F5** 运行这两个项目。</span><span class="sxs-lookup"><span data-stu-id="d10eb-273">Press **F5** to run both projects.</span></span>

      <span data-ttu-id="d10eb-274">运行 MyFixItCloud 服务项目时，Visual Studio 将启动 Azure 计算模拟器。</span><span class="sxs-lookup"><span data-stu-id="d10eb-274">When you run the MyFixItCloudService project, Visual Studio starts the Azure compute emulator.</span></span> <span data-ttu-id="d10eb-275">根据您的防火墙配置，您可能需要允许仿真器通过防火墙。</span><span class="sxs-lookup"><span data-stu-id="d10eb-275">Depending on your firewall configuration, you might need to allow the emulator through the firewall.</span></span>

<a id="deploybase"></a>
## <a name="how-to-deploy-the-base-app-to-azure-app-service-web-apps-by-using-the-windows-powershell-scripts"></a><span data-ttu-id="d10eb-276">如何使用 Windows PowerShell 脚本将基本应用部署到 Azure 应用服务 Web 应用</span><span class="sxs-lookup"><span data-stu-id="d10eb-276">How to deploy the base app to Azure App Service Web Apps by using the Windows PowerShell scripts</span></span>

<span data-ttu-id="d10eb-277">为了说明["自动执行所有内容"](automate-everything.md)模式，修复 It 应用附带了在 Azure 中设置环境并将项目部署到新环境的脚本。</span><span class="sxs-lookup"><span data-stu-id="d10eb-277">To illustrate the [Automate Everything](automate-everything.md) pattern, the Fix It app is supplied with scripts that set up an environment in Azure and deploy the project to the new environment.</span></span> <span data-ttu-id="d10eb-278">以下说明说明如何使用脚本。</span><span class="sxs-lookup"><span data-stu-id="d10eb-278">The following instructions explain how to use the scripts.</span></span>

<span data-ttu-id="d10eb-279">如果要在 Azure 中运行而不使用队列，并且所做的更改是为了在本地使用队列运行，请确保在继续执行以下说明之前将 Use队列应用设置值设置为 false。</span><span class="sxs-lookup"><span data-stu-id="d10eb-279">If you want to run in Azure without using queues, and you made the changes to run locally with queues, make sure you set the UseQueues appSetting value back to false before proceeding with the following instructions.</span></span>

<span data-ttu-id="d10eb-280">这些说明假定您已在本地下载并运行修复 It 解决方案，并且您具有 Azure 帐户或已授权管理的 Azure 订阅。</span><span class="sxs-lookup"><span data-stu-id="d10eb-280">These instructions assume you have already downloaded and run the Fix It solution locally, and that you have an Azure account or have an Azure subscription that you are authorized to manage.</span></span>

1. <span data-ttu-id="d10eb-281">安装**Azure PowerShell**控制台。</span><span class="sxs-lookup"><span data-stu-id="d10eb-281">Install the **Azure PowerShell** console.</span></span> <span data-ttu-id="d10eb-282">有关说明，请参阅[如何安装和配置 Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-4.3.1)。</span><span class="sxs-lookup"><span data-stu-id="d10eb-282">For instructions, see [How to install and configure Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-4.3.1).</span></span>

    <span data-ttu-id="d10eb-283">此自定义控制台配置为与 Azure 订阅配合使用。</span><span class="sxs-lookup"><span data-stu-id="d10eb-283">This customized console is configured to work with your Azure subscription.</span></span> <span data-ttu-id="d10eb-284">Azure 模块安装在 *"程序文件"* 目录中，并在每次使用 Azure PowerShell 控制台时自动导入。</span><span class="sxs-lookup"><span data-stu-id="d10eb-284">The Azure module is installed in the *Program Files* directory and is automatically imported on every use of the Azure PowerShell console.</span></span>

    <span data-ttu-id="d10eb-285">如果喜欢在不同的主机程序（如 Windows PowerShell ISE）中工作，请确保使用[导入模块](https://go.microsoft.com/fwlink/?LinkID=141553)cmdlet 导入 Azure 模块或使用 Azure 模块中的命令触发模块的自动导入。</span><span class="sxs-lookup"><span data-stu-id="d10eb-285">If you prefer to work in a different host program, such as Windows PowerShell ISE, be sure to use the [Import-Module](https://go.microsoft.com/fwlink/?LinkID=141553) cmdlet to import the Azure module or use a command in the Azure module to trigger automatic importing of the module.</span></span>
2. <span data-ttu-id="d10eb-286">使用 **"以管理员身份运行"** 选项启动 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="d10eb-286">Start Azure PowerShell with the **Run as administrator** option.</span></span>
3. <span data-ttu-id="d10eb-287">运行["设置执行策略](https://go.microsoft.com/fwlink/p/?linkid=293941)"cmdlet 以将 Azure PowerShell`RemoteSigned`执行策略设置为 。</span><span class="sxs-lookup"><span data-stu-id="d10eb-287">Run the [Set-ExecutionPolicy](https://go.microsoft.com/fwlink/p/?linkid=293941) cmdlet to set the Azure PowerShell execution policy to `RemoteSigned`.</span></span> <span data-ttu-id="d10eb-288">输入**Y（** 对于是）以完成策略更改。</span><span class="sxs-lookup"><span data-stu-id="d10eb-288">Enter **Y** (for Yes) to complete the policy change.</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample20.cmd)]

    <span data-ttu-id="d10eb-289">此设置使您能够运行未进行数字签名的本地脚本。</span><span class="sxs-lookup"><span data-stu-id="d10eb-289">This setting enables you to run local scripts that aren't digitally signed.</span></span> <span data-ttu-id="d10eb-290">（您还可以将执行策略设置为`Unrestricted`，这将在以后无需取消阻止步骤，但出于安全原因不建议这样做。</span><span class="sxs-lookup"><span data-stu-id="d10eb-290">(You can also set the execution policy to `Unrestricted`, which would eliminate the need for the unblock step later, but this is not recommended for security reasons.)</span></span>
4. <span data-ttu-id="d10eb-291">运行`Add-AzureAccount`cmdlet 以使用您的帐户凭据设置 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="d10eb-291">Run the `Add-AzureAccount` cmdlet to set up PowerShell with credentials for your account.</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample21.cmd)]

    <span data-ttu-id="d10eb-292">这些凭据将在一段时间后过期，您必须重新运行`Add-AzureAccount`cmdlet。</span><span class="sxs-lookup"><span data-stu-id="d10eb-292">These credentials expire after a period of time and you have to re-run the `Add-AzureAccount` cmdlet.</span></span> <span data-ttu-id="d10eb-293">在编写此电子书时，凭据过期前的时间限制为 12 小时。</span><span class="sxs-lookup"><span data-stu-id="d10eb-293">As this e-book is being written, the time limit before credentials expire is 12 hours.</span></span>
5. <span data-ttu-id="d10eb-294">如果您有多个订阅，请使用选择 Azure 订阅 cmdlet 指定要在 中创建测试环境的订阅。</span><span class="sxs-lookup"><span data-stu-id="d10eb-294">If you have multiple subscriptions, use the Select-AzureSubscription cmdlet to specify the subscription you want to create the test environment in.</span></span>
6. <span data-ttu-id="d10eb-295">使用`Get-AzurePublishSettingsFile`和`Import-AzurePublishSettingsFile`cmdlet 导入同一 Azure 订阅的管理证书。</span><span class="sxs-lookup"><span data-stu-id="d10eb-295">Import a management certificate for the same Azure subscription by using the `Get-AzurePublishSettingsFile` and `Import-AzurePublishSettingsFile` cmdlets.</span></span> <span data-ttu-id="d10eb-296">第一个 cmdlet 下载证书文件，在第二个 cmdlet 中，您可以指定该文件的位置以导入它。</span><span class="sxs-lookup"><span data-stu-id="d10eb-296">The first of these cmdlets downloads a certificate file, and in the second one you specify the location of that file in order to import it.</span></span> > [!IMPORTANT]
   > <span data-ttu-id="d10eb-297">将下载的文件保存在安全位置，或完成后将其删除，因为它包含可用于管理 Azure 服务的证书。</span><span class="sxs-lookup"><span data-stu-id="d10eb-297">Keep the downloaded file in a safe location or delete it when you're done with it, because it contains a certificate that can be used to manage your Azure services.</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample22.cmd)]

    <span data-ttu-id="d10eb-298">该证书用于 REST API 调用，该调用检测开发机的 IP 地址，以便在 SQL 数据库服务器上设置防火墙规则。</span><span class="sxs-lookup"><span data-stu-id="d10eb-298">The certificate is used for a REST API call that detects the development machine's IP address in order to set a firewall rule on the SQL Database server.</span></span>
7. <span data-ttu-id="d10eb-299">运行["设置位置](https://go.microsoft.com/fwlink/p/?linkid=293912)cmdlet"（别名为`cd``chdir``sl`和 ），以导航到包含脚本的目录。</span><span class="sxs-lookup"><span data-stu-id="d10eb-299">Run the [Set-Location](https://go.microsoft.com/fwlink/p/?linkid=293912) cmdlet (aliases are `cd`, `chdir`, and `sl`) to navigate to the directory that contains the scripts.</span></span> <span data-ttu-id="d10eb-300">（它们位于"修复它"解决方案文件夹中的*自动化*文件夹中。如果任何目录名称包含空格，则将路径放入引号中。</span><span class="sxs-lookup"><span data-stu-id="d10eb-300">(They're located in the *Automation* folder in the Fix It solution folder.) Put the path in quotes if any of the directory names contain spaces.</span></span> <span data-ttu-id="d10eb-301">例如，要导航到目录，`c:\Sample Apps\FixIt\Automation`可以输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="d10eb-301">For example, to navigate to the `c:\Sample Apps\FixIt\Automation` directory you could enter the following command:</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample23.cmd)]
8. <span data-ttu-id="d10eb-302">要允许 Windows PowerShell 运行这些脚本，请使用[取消阻止文件](https://go.microsoft.com/fwlink/p/?linkid=294021)cmdlet。</span><span class="sxs-lookup"><span data-stu-id="d10eb-302">To allow Windows PowerShell to run these scripts, use the [Unblock-File](https://go.microsoft.com/fwlink/p/?linkid=294021) cmdlet.</span></span> <span data-ttu-id="d10eb-303">（脚本被阻止，因为它们是从 Internet 下载的。</span><span class="sxs-lookup"><span data-stu-id="d10eb-303">(The scripts are blocked because they were downloaded from the Internet.)</span></span>

    > [!WARNING]
    > <span data-ttu-id="d10eb-304">安全性 -`Unblock-File`在运行任何脚本或可执行文件之前，在记事本中打开该文件，检查命令，并验证它们不包含任何恶意代码。</span><span class="sxs-lookup"><span data-stu-id="d10eb-304">Security - Before running `Unblock-File` on any script or executable file, open the file in Notepad, examine the commands, and verify that they do not contain any malicious code.</span></span>

    <span data-ttu-id="d10eb-305">例如，以下命令在当前目录中的所有脚本`Unblock-File`上运行 cmdlet。</span><span class="sxs-lookup"><span data-stu-id="d10eb-305">For example, the following command runs the `Unblock-File` cmdlet on all scripts in the current directory.</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample24.cmd)]
9. <span data-ttu-id="d10eb-306">要为基础创建 Web 应用（无队列处理）修复它应用，请运行环境创建脚本。</span><span class="sxs-lookup"><span data-stu-id="d10eb-306">To create the web app for the base (no queues processing) Fix It app, run the environment creation script.</span></span>

    <span data-ttu-id="d10eb-307">所需的`Name`参数指定数据库的名称，并且也用于脚本创建的存储帐户。</span><span class="sxs-lookup"><span data-stu-id="d10eb-307">The required `Name` parameter specifies the name of the database and is also used for the storage account that the script creates.</span></span> <span data-ttu-id="d10eb-308">名称在azurewebsites.net域中必须全局唯一。</span><span class="sxs-lookup"><span data-stu-id="d10eb-308">The name must be globally unique within the azurewebsites.net domain.</span></span> <span data-ttu-id="d10eb-309">如果指定的名称不唯一（如 Fixit 或 Test（甚至如示例中的 fixitdemo），`New-AzureWebsite`则 cmdlet 失败，并出现报告冲突的内部错误。</span><span class="sxs-lookup"><span data-stu-id="d10eb-309">If you specify a name that is not unique, like Fixit or Test (or even as in the example, fixitdemo), the `New-AzureWebsite` cmdlet fails with an Internal Error that reports a conflict.</span></span> <span data-ttu-id="d10eb-310">该脚本将名称转换为所有小写，以符合 Web 应用、存储帐户和数据库的名称要求。</span><span class="sxs-lookup"><span data-stu-id="d10eb-310">The script converts the name to all lower-case to comply with name requirements for web apps, storage accounts, and databases.</span></span>

    <span data-ttu-id="d10eb-311">所需`SqlDatabasePassword`参数指定将为 SQL 数据库创建的管理员帐户的密码。</span><span class="sxs-lookup"><span data-stu-id="d10eb-311">The required `SqlDatabasePassword` parameter specifies the password for the admin account that will be created for SQL Database.</span></span> <span data-ttu-id="d10eb-312">不要在密码中包含特殊的 XML 字符（;)。&amp; &lt; &gt;</span><span class="sxs-lookup"><span data-stu-id="d10eb-312">Don't include special XML characters in the password (&amp; &lt; &gt; ;).</span></span> <span data-ttu-id="d10eb-313">这是脚本编写方式的限制，而不是 Azure 的限制。</span><span class="sxs-lookup"><span data-stu-id="d10eb-313">This is a limitation of the way the scripts were written, not a limitation of Azure.</span></span>

    <span data-ttu-id="d10eb-314">例如，如果要创建名为"fixitdemo"的 Web 应用并使用 SQL Server 管理员密码"Passw0rd1"，则可以输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="d10eb-314">For example, if you want to create a web app named "fixitdemo" and use a SQL Server administrator password of "Passw0rd1", you could enter the following command:</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample25.cmd)]

    <span data-ttu-id="d10eb-315">名称在azurewebsites.net域中必须是唯一的，并且密码必须满足 SQL 数据库对密码复杂性的要求。</span><span class="sxs-lookup"><span data-stu-id="d10eb-315">The name must be unique in the azurewebsites.net domain, and the password must meet SQL Database requirements for password complexity.</span></span> <span data-ttu-id="d10eb-316">（示例 Passw0rd1 确实满足要求。</span><span class="sxs-lookup"><span data-stu-id="d10eb-316">(The example Passw0rd1 does meet the requirements.)</span></span>

    <span data-ttu-id="d10eb-317">请注意，该命令以"开头。\".</span><span class="sxs-lookup"><span data-stu-id="d10eb-317">Note that the command begins with ".\".</span></span> <span data-ttu-id="d10eb-318">为了帮助防止恶意执行脚本，Windows PowerShell 要求您在运行脚本时提供脚本文件的完全限定路径。</span><span class="sxs-lookup"><span data-stu-id="d10eb-318">To help prevent malicious execution of scripts, Windows PowerShell requires that you provide the fully qualified path to the script file when you run a script.</span></span> <span data-ttu-id="d10eb-319">可以使用点来指示当前目录 （"）。\"或提供完全限定的路径，例如：</span><span class="sxs-lookup"><span data-stu-id="d10eb-319">You can use a dot to indicate the current directory (".\") or provide the fully qualified path, such as:</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample26.cmd)]

    <span data-ttu-id="d10eb-320">有关脚本的详细信息，请使用`Get-Help`cmdlet。</span><span class="sxs-lookup"><span data-stu-id="d10eb-320">For more information about the script, use the `Get-Help` cmdlet.</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample27.cmd)]

    <span data-ttu-id="d10eb-321">您可以使用 获取帮助`Detailed` `Full`cmdlet 的 、`Parameters`和`Examples`参数来筛选返回的帮助。</span><span class="sxs-lookup"><span data-stu-id="d10eb-321">You can use the `Detailed`, `Full`, `Parameters`, and `Examples` parameters of the Get-Help cmdlet to filter the help that is returned.</span></span>

    <span data-ttu-id="d10eb-322">如果脚本失败或生成错误，例如"新建 Azure 网站：先调用集 Azure 订阅和选择 Azure 订阅"，则可能尚未完成 Azure PowerShell 的配置。</span><span class="sxs-lookup"><span data-stu-id="d10eb-322">If the script fails or generates errors, such as "New-AzureWebsite : Call Set-AzureSubscription and Select-AzureSubscription first," you might not have completed the configuration of Azure PowerShell.</span></span>

    <span data-ttu-id="d10eb-323">脚本完成后，可以使用 Azure 管理门户查看已创建的资源，如["自动所有内容"](automate-everything.md)章节所示。</span><span class="sxs-lookup"><span data-stu-id="d10eb-323">After the script finishes, you can use the Azure Management Portal to see the resources that were created, as shown in the [Automate Everything](automate-everything.md) chapter.</span></span>
10. <span data-ttu-id="d10eb-324">要将 FixIt 项目部署到新的 Azure 环境，请使用*Azure 网站.ps1*脚本。</span><span class="sxs-lookup"><span data-stu-id="d10eb-324">To deploy the FixIt project to the new Azure environment, use the *AzureWebsite.ps1* script.</span></span> <span data-ttu-id="d10eb-325">例如：</span><span class="sxs-lookup"><span data-stu-id="d10eb-325">For example:</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample28.cmd)]

    <span data-ttu-id="d10eb-326">部署完成后，浏览器将在 Azure 中运行修复它时打开。</span><span class="sxs-lookup"><span data-stu-id="d10eb-326">When deployment is done, the browser opens with Fix It running in Azure.</span></span>

<a id="troubleshooting"></a>
## <a name="troubleshooting-the-windows-powershell-scripts"></a><span data-ttu-id="d10eb-327">对 Windows 电源外壳脚本进行故障排除</span><span class="sxs-lookup"><span data-stu-id="d10eb-327">Troubleshooting the Windows PowerShell scripts</span></span>

<span data-ttu-id="d10eb-328">运行这些脚本时遇到的最常见的错误与权限有关。</span><span class="sxs-lookup"><span data-stu-id="d10eb-328">The most common errors encountered when running these scripts are related to permissions.</span></span> <span data-ttu-id="d10eb-329">确保 并`Add-AzureAccount``Import-AzurePublishSettingsFile`成功，并且将它们用于相同的 Azure 订阅。</span><span class="sxs-lookup"><span data-stu-id="d10eb-329">Make sure that `Add-AzureAccount` and `Import-AzurePublishSettingsFile` were successful and that you used them for the same Azure subscription.</span></span> <span data-ttu-id="d10eb-330">即使`Add-AzureAccount`成功，你也得再次运行它。</span><span class="sxs-lookup"><span data-stu-id="d10eb-330">Even if `Add-AzureAccount` was successful you might have to run it again.</span></span> <span data-ttu-id="d10eb-331">添加`Add-AzureAccount`的权限将在 12 小时内过期。</span><span class="sxs-lookup"><span data-stu-id="d10eb-331">The permissions added by `Add-AzureAccount` expire in 12 hours.</span></span>

### <a name="object-reference-not-set-to-an-instance-of-an-object"></a><span data-ttu-id="d10eb-332">对象引用未设置为某个对象的实例。</span><span class="sxs-lookup"><span data-stu-id="d10eb-332">Object reference not set to an instance of an object.</span></span>

<span data-ttu-id="d10eb-333">如果脚本返回错误（如"对象引用未设置为对象的实例"，这意味着 Windows PowerShell 找不到要处理的对象（这是空引用异常），请运行`Add-AzureAccount`cmdlet 并重试该脚本。</span><span class="sxs-lookup"><span data-stu-id="d10eb-333">If the script returns errors, such as "Object reference not set to an instance of an object," which means that Windows PowerShell can't find an object to process (this is a null reference exception), run the `Add-AzureAccount` cmdlet and try the script again.</span></span>

[!code-console[Main](the-fix-it-sample-application/samples/sample29.cmd)]

### <a name="internalerror-the-server-encountered-an-internal-error"></a><span data-ttu-id="d10eb-334">内部错误：服务器遇到内部错误。</span><span class="sxs-lookup"><span data-stu-id="d10eb-334">InternalError: The server encountered an internal error.</span></span>

<span data-ttu-id="d10eb-335">当`New-AzureWebsite`名称在azurewebsites.net域中不唯一时，cmdlet 返回内部错误。</span><span class="sxs-lookup"><span data-stu-id="d10eb-335">The `New-AzureWebsite` cmdlet returns an internal error when the name is not unique in the azurewebsites.net domain.</span></span> <span data-ttu-id="d10eb-336">要解决错误，请使用名称的其他值，该值位于*New-Azure网站Env.ps1*的名称参数中。</span><span class="sxs-lookup"><span data-stu-id="d10eb-336">To resolve the error, use a different value for the name, which is in the Name parameter of *New-AzureWebsiteEnv.ps1*.</span></span>

[!code-console[Main](the-fix-it-sample-application/samples/sample30.cmd)]

### <a name="restarting-the-script"></a><span data-ttu-id="d10eb-337">重新启动脚本</span><span class="sxs-lookup"><span data-stu-id="d10eb-337">Restarting the script</span></span>

<span data-ttu-id="d10eb-338">如果需要重新启动*New-Azure 网站Env.ps1*脚本，因为它在打印"脚本已完成"消息之前出现故障，则可能需要删除脚本在停止之前创建的资源。</span><span class="sxs-lookup"><span data-stu-id="d10eb-338">If you need to restart the *New-AzureWebsiteEnv.ps1* script because it failed before it printed the "Script is complete" message, you might want to delete resources that the script created before it stopped.</span></span> <span data-ttu-id="d10eb-339">例如，如果脚本已创建 ContosoFixItDemo Web 应用，并且您再次使用相同的名称运行脚本，则该脚本将失败，因为该名称正在使用中。</span><span class="sxs-lookup"><span data-stu-id="d10eb-339">For example, if the script already created the ContosoFixItDemo web app and you run the script again with the same name, the script will fail because the name is in use.</span></span>

<span data-ttu-id="d10eb-340">要确定脚本在停止之前创建的资源，请使用以下 cmdlet：</span><span class="sxs-lookup"><span data-stu-id="d10eb-340">To determine which resources the script created before it stopped, use the following cmdlets:</span></span>

- `Get-AzureWebsite`
- `Get-AzureSqlDatabaseServer`
- <span data-ttu-id="d10eb-341">`Get-AzureSqlDatabase`： 要运行此 cmdlet，请将数据库服务器`Get-AzureSqlDatabase`名称管道到 ：`Get-AzureSqlDatabaseServer | Get-AzureSqlDatabase.`</span><span class="sxs-lookup"><span data-stu-id="d10eb-341">`Get-AzureSqlDatabase`: To run this cmdlet, pipe the database server name to `Get-AzureSqlDatabase`:   `Get-AzureSqlDatabaseServer | Get-AzureSqlDatabase.`</span></span>

<span data-ttu-id="d10eb-342">要删除这些资源，请使用以下命令。</span><span class="sxs-lookup"><span data-stu-id="d10eb-342">To delete these resources, use the following commands.</span></span> <span data-ttu-id="d10eb-343">请注意，如果删除数据库服务器，则会自动删除与服务器关联的数据库。</span><span class="sxs-lookup"><span data-stu-id="d10eb-343">Note that if you delete the database server, you automatically delete the databases associated with the server.</span></span>

- `Get-AzureWebsite -Name <WebsiteName> | Remove-AzureWebsite`
- `Get-AzureSqlDatabase -Name <DatabaseName> -ServerName <DatabaseServerName> | Remove-SqlAzureDatabase`
- `Get-AzureSqlDatabaseServer | Remove-AzureSqlDatabaseServer`

<a id="deployqueues"></a>
## <a name="how-to-deploy-the-app-with-queue-processing-to-azure-app-service-web-apps-and-an-azure-cloud-service"></a><span data-ttu-id="d10eb-344">如何将具有队列处理的应用部署到 Azure 应用服务 Web 应用和 Azure 云服务</span><span class="sxs-lookup"><span data-stu-id="d10eb-344">How to deploy the app with queue processing to Azure App Service Web Apps and an Azure Cloud Service</span></span>

<span data-ttu-id="d10eb-345">要启用队列，请确保在 MyFixIt_Web.config 文件中进行以下更改。</span><span class="sxs-lookup"><span data-stu-id="d10eb-345">To enable queues, make the following change in the MyFixIt\Web.config file.</span></span> <span data-ttu-id="d10eb-346">在`appSettings`下，将`UseQueues`的值更改为"true"：</span><span class="sxs-lookup"><span data-stu-id="d10eb-346">Under `appSettings`, change the value of `UseQueues` to "true":</span></span>

[!code-xml[Main](the-fix-it-sample-application/samples/sample31.xml)]

<span data-ttu-id="d10eb-347">然后，将 MVC 应用程序部署到 Azure 应用服务中的 Web 应用，如[前面](#deploybase)所述。</span><span class="sxs-lookup"><span data-stu-id="d10eb-347">Then deploy the MVC application to an web app in Azure App Service, as described [earlier](#deploybase).</span></span>

<span data-ttu-id="d10eb-348">接下来，创建新的 Azure 云服务。</span><span class="sxs-lookup"><span data-stu-id="d10eb-348">Next, create a new Azure cloud service.</span></span> <span data-ttu-id="d10eb-349">修复 It 应用中包含的脚本不会创建或部署云服务，因此必须为此使用 Azure 门户。</span><span class="sxs-lookup"><span data-stu-id="d10eb-349">The scripts included with the Fix It app do not create or deploy the cloud service, so you must use Azure portal for this.</span></span> <span data-ttu-id="d10eb-350">在门户中，单击 **"新** -- **计算**+**云服务** -- **快速创建**"，然后输入 URL 和数据中心位置。</span><span class="sxs-lookup"><span data-stu-id="d10eb-350">In the portal, click **New** -- **Compute** – **Cloud Service** -- **Quick Create**, and then enter a URL and a data center location.</span></span> <span data-ttu-id="d10eb-351">使用部署 Web 应用的同一数据中心。</span><span class="sxs-lookup"><span data-stu-id="d10eb-351">Use the same data center where you deployed the web app.</span></span>

![](the-fix-it-sample-application/_static/image1.png)

<span data-ttu-id="d10eb-352">在部署云服务之前，需要更新某些配置文件。</span><span class="sxs-lookup"><span data-stu-id="d10eb-352">Before you can deploy the cloud service, you need to update some of the configuration files.</span></span>

<span data-ttu-id="d10eb-353">在 MyFixIt.WorkerRole_app.config`connectionStrings`中，在 下，`appdb`将连接字符串的值替换为 SQL 数据库的实际连接字符串。</span><span class="sxs-lookup"><span data-stu-id="d10eb-353">In MyFixIt.WorkerRole\app.config, under `connectionStrings`, replace the value of the `appdb` connection string with the actual connection string for the SQL Database.</span></span> <span data-ttu-id="d10eb-354">可以从门户获取连接字符串。</span><span class="sxs-lookup"><span data-stu-id="d10eb-354">You can get the connection string from the portal.</span></span> <span data-ttu-id="d10eb-355">在门户中，单击**ADO .Net、ODBC、PHP 和 JDBC 的** **SQL 数据库** - **appdb** - 视图 SQL 数据库连接字符串。</span><span class="sxs-lookup"><span data-stu-id="d10eb-355">In the portal, click **SQL Databases** - **appdb** - **View SQL Database connection strings for ADO .Net, ODBC, PHP, and JDBC**.</span></span> <span data-ttu-id="d10eb-356">复制ADO.NET连接字符串并将该值粘贴到 app.config 文件中。</span><span class="sxs-lookup"><span data-stu-id="d10eb-356">Copy the ADO.NET connection string and paste the value into the app.config file.</span></span> <span data-ttu-id="d10eb-357">将"此处的\_密码\_"替换为数据库密码。</span><span class="sxs-lookup"><span data-stu-id="d10eb-357">Replace "{your\_password\_here}" with your database password.</span></span> <span data-ttu-id="d10eb-358">（假设您使用脚本部署 MVC 应用，则可以在脚本参数中`SqlDatabasePassword`指定数据库密码。</span><span class="sxs-lookup"><span data-stu-id="d10eb-358">(Assuming you used the scripts to deploy the MVC app, you specified the database password in the `SqlDatabasePassword` script parameter.)</span></span>

<span data-ttu-id="d10eb-359">结果应如下所示：</span><span class="sxs-lookup"><span data-stu-id="d10eb-359">The result should look like the following:</span></span>

[!code-xml[Main](the-fix-it-sample-application/samples/sample32.xml)]

<span data-ttu-id="d10eb-360">在同一 MyFixIt.WorkerRole_app.config 文件下`appSettings`，替换 Azure 存储帐户的两个占位符值。</span><span class="sxs-lookup"><span data-stu-id="d10eb-360">In the same MyFixIt.WorkerRole\app.config file, under `appSettings`, replace the two placeholder values for the Azure storage account.</span></span>

[!code-xml[Main](the-fix-it-sample-application/samples/sample33.xml?highlight=2-3)]

<span data-ttu-id="d10eb-361">可以从门户获取访问密钥。</span><span class="sxs-lookup"><span data-stu-id="d10eb-361">You can get the access key from the portal.</span></span> <span data-ttu-id="d10eb-362">请参阅[如何管理存储帐户](https://docs.microsoft.com/azure/storage/common/storage-create-storage-account)。</span><span class="sxs-lookup"><span data-stu-id="d10eb-362">See [How To Manage Storage Accounts](https://docs.microsoft.com/azure/storage/common/storage-create-storage-account).</span></span>

<span data-ttu-id="d10eb-363">在 MyFixItCloudService 服务配置.Cloud.cscfg 中，替换 Azure 存储帐户的两个占位符值。</span><span class="sxs-lookup"><span data-stu-id="d10eb-363">In MyFixItCloudService\ServiceConfiguration.Cloud.cscfg, replace the same two placeholders values for the Azure storage account.</span></span>

[!code-xml[Main](the-fix-it-sample-application/samples/sample34.xml?highlight=3)]

<span data-ttu-id="d10eb-364">现在，您已准备好部署云服务。</span><span class="sxs-lookup"><span data-stu-id="d10eb-364">Now you are ready to deploy the cloud service.</span></span> <span data-ttu-id="d10eb-365">在"解决方案浏览"中，右键单击 MyFixIt云服务项目并选择 **"发布**"。</span><span class="sxs-lookup"><span data-stu-id="d10eb-365">In Solution Explore, right-click the MyFixItCloudService project and select **Publish**.</span></span> <span data-ttu-id="d10eb-366">有关详细信息，请参阅[本教程的第](https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36)2 部分中的"[将应用程序部署到 Azure"。](https://www.windowsazure.com/develop/net/tutorials/multi-tier-web-site/2-download-and-run/#deployAz)</span><span class="sxs-lookup"><span data-stu-id="d10eb-366">For more information, see "[Deploy the Application to Azure](https://www.windowsazure.com/develop/net/tutorials/multi-tier-web-site/2-download-and-run/#deployAz)", which is in part 2 of [this tutorial](https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36).</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="d10eb-367">上一步</span><span class="sxs-lookup"><span data-stu-id="d10eb-367">Previous</span></span>](more-patterns-and-guidance.md)

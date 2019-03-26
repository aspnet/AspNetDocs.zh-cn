---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/the-fix-it-sample-application
title: 附录：修复它示例应用程序 （构建实际云应用与 Azure） |Microsoft Docs
author: MikeWasson
description: 构建真实世界云应用与 Azure 的电子书基于由 Scott Guthrie 开发的演示文稿。 它还说明了 13 模式和实践可以他...
ms.author: riande
ms.date: 06/12/2014
ms.assetid: 1bc333c5-f096-4ea7-b170-779accc21c1a
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/the-fix-it-sample-application
msc.type: authoredcontent
ms.openlocfilehash: a73fac6107be45455465b506a019bcc9a41b1deb
ms.sourcegitcommit: 289e051cc8a90e8f7127e239fda73047bde4de12
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2019
ms.locfileid: "58425517"
---
<a name="appendix-the-fix-it-sample-application-building-real-world-cloud-apps-with-azure"></a><span data-ttu-id="25206-104">附录：修复它示例应用程序 （构建使用 Azure 的真实世界云应用程序）</span><span class="sxs-lookup"><span data-stu-id="25206-104">Appendix: The Fix It Sample Application (Building Real-World Cloud Apps with Azure)</span></span>
====================
<span data-ttu-id="25206-105">通过[Mike Wasson](https://github.com/MikeWasson)， [Rick Anderson]((https://twitter.com/RickAndMSFT))， [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="25206-105">by [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson]((https://twitter.com/RickAndMSFT)), [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="25206-106">下载该项目的修补程序</span><span class="sxs-lookup"><span data-stu-id="25206-106">Download The Fix It Project</span></span>](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)

> <span data-ttu-id="25206-107">**构建真实世界云应用，使用 Azure**电子书基于由 Scott Guthrie 开发的演示文稿。</span><span class="sxs-lookup"><span data-stu-id="25206-107">The **Building Real World Cloud Apps with Azure** e-book is based on a presentation developed by Scott Guthrie.</span></span> <span data-ttu-id="25206-108">它还说明了 13 模式和实践，从而帮助您获得成功开发适用于在云中的 web 应用。</span><span class="sxs-lookup"><span data-stu-id="25206-108">It explains 13 patterns and practices that can help you be successful developing web apps for the cloud.</span></span> <span data-ttu-id="25206-109">有关电子书的信息，请参阅[的第一章](introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="25206-109">For information about the e-book, see [the first chapter](introduction.md).</span></span>

<span data-ttu-id="25206-110">本附录的构建真实世界云应用与 Azure 的电子书包含以下各节提供有关 Fix It 示例应用程序，您可以下载的其他信息：</span><span class="sxs-lookup"><span data-stu-id="25206-110">This appendix to the Building Real World Cloud Apps with Azure e-book contains the following sections that provide additional information about the Fix It sample application that you can download:</span></span>

- [<span data-ttu-id="25206-111">已知的问题</span><span class="sxs-lookup"><span data-stu-id="25206-111">Known issues</span></span>](#knownissues)
- [<span data-ttu-id="25206-112">最佳做法</span><span class="sxs-lookup"><span data-stu-id="25206-112">Best practices</span></span>](#bestpractices)
- [<span data-ttu-id="25206-113">如何从 Visual Studio 在本地计算机上运行该应用程序</span><span class="sxs-lookup"><span data-stu-id="25206-113">How to run the app from Visual Studio on your local computer</span></span>](#run-in-vs)
- [<span data-ttu-id="25206-114">如何将基本应用程序部署到 Azure 应用服务 Web 应用，通过使用 Windows PowerShell 脚本</span><span class="sxs-lookup"><span data-stu-id="25206-114">How to deploy the base app to Azure App Service Web Apps by using the Windows PowerShell scripts</span></span>](#deploybase)
- [<span data-ttu-id="25206-115">Windows PowerShell 脚本故障排除</span><span class="sxs-lookup"><span data-stu-id="25206-115">Troubleshooting the Windows PowerShell scripts</span></span>](#troubleshooting)
- [<span data-ttu-id="25206-116">如何使用队列处理到 Azure 应用服务 Web 应用和 Azure 云服务部署应用程序</span><span class="sxs-lookup"><span data-stu-id="25206-116">How to deploy the app with queue processing to Azure App Service Web Apps and an Azure Cloud Service</span></span>](#deployqueues)

<a id="knownissues"></a>
## <a name="known-issues"></a><span data-ttu-id="25206-117">已知问题</span><span class="sxs-lookup"><span data-stu-id="25206-117">Known issues</span></span>

<span data-ttu-id="25206-118">Fix It 应用最初是为了说明尽可能简单地的一些模式显示此电子书中开发的。</span><span class="sxs-lookup"><span data-stu-id="25206-118">The Fix It app was originally developed in order to illustrate as simply as possible some of the patterns presented in this e-book.</span></span> <span data-ttu-id="25206-119">但是，由于电子书是有关构建实际的应用程序，我们受到 Fix It 代码评审和测试过程类似于我们对于发布的软件将执行操作。</span><span class="sxs-lookup"><span data-stu-id="25206-119">However, since the e-book is about building real-world apps, we subjected the Fix It code to a review and testing process similar to what we'd do for released software.</span></span> <span data-ttu-id="25206-120">我们发现许多问题，并且与任何实际的应用程序中，我们修复了其中一些，并且其中一些我们推迟到以后的版本。</span><span class="sxs-lookup"><span data-stu-id="25206-120">We found a number of issues, and as with any real-world application, some of them we fixed and some of them we deferred to a later release.</span></span>

<span data-ttu-id="25206-121">以下列表包含应解决的问题，在生产应用程序，但其中一个原因或另一个我们决定不修复它示例应用程序的初始版本中的地址。</span><span class="sxs-lookup"><span data-stu-id="25206-121">The following list includes issues that should be addressed in a production application, but for one reason or another we decided not to address in the initial release of the Fix It sample application.</span></span>

### <a name="security"></a><span data-ttu-id="25206-122">安全性</span><span class="sxs-lookup"><span data-stu-id="25206-122">Security</span></span>

- <span data-ttu-id="25206-123">请确保不能将任务分配给不存在的所有者。</span><span class="sxs-lookup"><span data-stu-id="25206-123">Ensure that you can't assign a task to a non-existent owner.</span></span>
- <span data-ttu-id="25206-124">确保你仅可以查看和修改的创建或分配给你的任务。</span><span class="sxs-lookup"><span data-stu-id="25206-124">Ensure that you can only view and modify tasks that you created or are assigned to you.</span></span>
- <span data-ttu-id="25206-125">针对登录页和身份验证 cookie 使用 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="25206-125">Use HTTPS for sign-in pages and authentication cookies.</span></span>
- <span data-ttu-id="25206-126">指定身份验证 cookie 的时间限制。</span><span class="sxs-lookup"><span data-stu-id="25206-126">Specify a time limit for authentication cookies.</span></span>

### <a name="input-validation"></a><span data-ttu-id="25206-127">输入的验证</span><span class="sxs-lookup"><span data-stu-id="25206-127">Input validation</span></span>

<span data-ttu-id="25206-128">一般情况下，像生产应用的详细信息输入验证比 Fix It 应用程序。</span><span class="sxs-lookup"><span data-stu-id="25206-128">In general, a production app would do more input validation than the Fix It app.</span></span> <span data-ttu-id="25206-129">例如，图像大小 / image 允许应限制上传的文件大小。</span><span class="sxs-lookup"><span data-stu-id="25206-129">For example, the image size / image file size allowed for upload should be limited.</span></span>

### <a name="administrator-functionality"></a><span data-ttu-id="25206-130">管理员功能</span><span class="sxs-lookup"><span data-stu-id="25206-130">Administrator functionality</span></span>

<span data-ttu-id="25206-131">管理员应能够在现有任务上更改所有权。</span><span class="sxs-lookup"><span data-stu-id="25206-131">An administrator should be able to change ownership on existing tasks.</span></span> <span data-ttu-id="25206-132">例如，一项任务的创建者可能会使公司，没有人留下颁发机构来维护任务，除非已启用的管理访问权限。</span><span class="sxs-lookup"><span data-stu-id="25206-132">For example, the creator of a task might leave the company, leaving no one with authority to maintain the task unless administrative access is enabled.</span></span>

### <a name="queue-message-processing"></a><span data-ttu-id="25206-133">处理队列消息</span><span class="sxs-lookup"><span data-stu-id="25206-133">Queue message processing</span></span>

<span data-ttu-id="25206-134">修复其应用中处理的队列消息被可简单，以便将阐释最少量的代码使用以队列为中心的工作模式。</span><span class="sxs-lookup"><span data-stu-id="25206-134">Queue message processing in the Fix It app was designed to be simple in order to illustrate the queue-centric work pattern with a minimum amount of code.</span></span> <span data-ttu-id="25206-135">此简单的代码并不是足够的实际的生产应用程序。</span><span class="sxs-lookup"><span data-stu-id="25206-135">This simple code would not be adequate for an actual production application.</span></span>

- <span data-ttu-id="25206-136">该代码不保证将最多一次处理每个队列消息。</span><span class="sxs-lookup"><span data-stu-id="25206-136">The code does not guarantee that each queue message will be processed at most once.</span></span> <span data-ttu-id="25206-137">如果从队列中获取一条消息，则超时期限，在此期间的消息是看不到其他队列侦听器。</span><span class="sxs-lookup"><span data-stu-id="25206-137">When you get a message from the queue, there is a timeout period, during which the message is invisible to other queue listeners.</span></span> <span data-ttu-id="25206-138">如果在超时到期之前删除该消息，消息将再次可见。</span><span class="sxs-lookup"><span data-stu-id="25206-138">If the timeout expires before the message is deleted, the message becomes visible again.</span></span> <span data-ttu-id="25206-139">因此，如果辅助角色实例花费很长时间处理消息，它是相同的消息得到处理两次，从理论上讲可能导致数据库中的重复任务。</span><span class="sxs-lookup"><span data-stu-id="25206-139">Therefore, if a worker role instance spends a long time processing a message, it is theoretically possible for the same message to get processed twice, resulting in a duplicate task in the database.</span></span> <span data-ttu-id="25206-140">有关此问题的详细信息，请参阅[使用 Azure 存储队列](https://msdn.microsoft.com/library/ff803365.aspx#sec7)。</span><span class="sxs-lookup"><span data-stu-id="25206-140">For more information about this issue, see [Using Azure Storage Queues](https://msdn.microsoft.com/library/ff803365.aspx#sec7).</span></span>
- <span data-ttu-id="25206-141">队列轮询逻辑可能是更具成本效益，批处理的消息检索。</span><span class="sxs-lookup"><span data-stu-id="25206-141">The queue polling logic could be more cost-effective, by batching message retrieval.</span></span> <span data-ttu-id="25206-142">每次调用[CloudQueue.GetMessageAsync](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.getmessageasync.aspx)，没有事务费用。</span><span class="sxs-lookup"><span data-stu-id="25206-142">Every time you call [CloudQueue.GetMessageAsync](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.getmessageasync.aspx), there is a transaction cost.</span></span> <span data-ttu-id="25206-143">相反，您可以调用[CloudQueue.GetMessagesAsync](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.getmessagesasync.aspx) (请注意复数形式的)，它将在单个事务中获取多个消息。</span><span class="sxs-lookup"><span data-stu-id="25206-143">Instead, you can call [CloudQueue.GetMessagesAsync](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.getmessagesasync.aspx) (note the plural 's'), which gets multiple messages in a single transaction.</span></span> <span data-ttu-id="25206-144">Azure 存储队列事务成本是非常低，因此对成本的影响不是大量在大多数情况下。</span><span class="sxs-lookup"><span data-stu-id="25206-144">The transaction costs for Azure Storage Queues are very low, so the impact on costs is not substantial in most scenarios.</span></span>
- <span data-ttu-id="25206-145">队列消息处理代码中的紧密循环会导致不有效地利用多核虚拟机的 CPU 关联。</span><span class="sxs-lookup"><span data-stu-id="25206-145">The tight loop in the queue message-processing code causes CPU affinity, which does not utilize multi-core VMs efficiently.</span></span> <span data-ttu-id="25206-146">更好的设计将使用任务并行度以并行方式运行多个异步任务。</span><span class="sxs-lookup"><span data-stu-id="25206-146">A better design would use task parallelism to run several async tasks in parallel.</span></span>
- <span data-ttu-id="25206-147">处理队列消息具有仅基本异常处理。</span><span class="sxs-lookup"><span data-stu-id="25206-147">Queue message-processing has only rudimentary exception handling.</span></span> <span data-ttu-id="25206-148">例如，代码不会处理[有害消息](https://msdn.microsoft.com/library/ms789028.aspx)。</span><span class="sxs-lookup"><span data-stu-id="25206-148">For example, the code doesn't handle [poison messages](https://msdn.microsoft.com/library/ms789028.aspx).</span></span> <span data-ttu-id="25206-149">（当消息处理导致异常时，必须记录错误并删除该消息或辅助角色将尝试再次对其进行处理和则循环将无限期地继续。）</span><span class="sxs-lookup"><span data-stu-id="25206-149">(When message processing causes an exception, you have to log the error and delete the message, or the worker role will try to process it again, and the loop will continue indefinitely.)</span></span>

### <a name="sql-queries-are-unbounded"></a><span data-ttu-id="25206-150">SQL 查询是不受限制</span><span class="sxs-lookup"><span data-stu-id="25206-150">SQL queries are unbounded</span></span>

<span data-ttu-id="25206-151">当前修复该代码对索引页的查询可能返回的行数没有限制。</span><span class="sxs-lookup"><span data-stu-id="25206-151">Current Fix It code places no limit on how many rows the queries for Index pages might return.</span></span> <span data-ttu-id="25206-152">如果大量的任务输入到数据库时，收到的生成列表的大小可能会导致性能问题。</span><span class="sxs-lookup"><span data-stu-id="25206-152">If a large volume of tasks is entered into the database, the size of the resulting lists received could cause performance issues.</span></span> <span data-ttu-id="25206-153">解决方案是实现分页。</span><span class="sxs-lookup"><span data-stu-id="25206-153">The solution is to implement paging.</span></span> <span data-ttu-id="25206-154">有关示例，请参阅[排序、 筛选和分页与 ASP.NET MVC 应用程序中的实体框架](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md)。</span><span class="sxs-lookup"><span data-stu-id="25206-154">For an example, see [Sorting, Filtering, and Paging with the Entity Framework in an ASP.NET MVC Application](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md).</span></span>

### <a name="view-models-recommended"></a><span data-ttu-id="25206-155">建议的视图模型</span><span class="sxs-lookup"><span data-stu-id="25206-155">View models recommended</span></span>

<span data-ttu-id="25206-156">Fix It 应用使用 FixItTask 实体类在控制器和视图之间传递信息。</span><span class="sxs-lookup"><span data-stu-id="25206-156">The Fix It app uses the FixItTask entity class to pass information between the controller and the view.</span></span> <span data-ttu-id="25206-157">一种最佳做法是使用视图模型。</span><span class="sxs-lookup"><span data-stu-id="25206-157">A best practice is to use view models.</span></span> <span data-ttu-id="25206-158">域模型 （例如，FixItTask 实体类） 被专为所需的数据暂留，尽管视图模型可供数据演示文稿。</span><span class="sxs-lookup"><span data-stu-id="25206-158">The domain model (e.g., the FixItTask entity class) is designed around what is needed for data persistence, while a view model can be designed for data presentation.</span></span> <span data-ttu-id="25206-159">有关详细信息，请参阅[12 ASP.NET MVC 最佳实践](http://codeclimber.net.nz/archive/2009/10/27/12-asp.net-mvc-best-practices.aspx)。</span><span class="sxs-lookup"><span data-stu-id="25206-159">For more information, see [12 ASP.NET MVC Best Practices](http://codeclimber.net.nz/archive/2009/10/27/12-asp.net-mvc-best-practices.aspx).</span></span>

### <a name="secure-image-blob-recommended"></a><span data-ttu-id="25206-160">建议的安全映像 blob</span><span class="sxs-lookup"><span data-stu-id="25206-160">Secure image blob recommended</span></span>

<span data-ttu-id="25206-161">修复其应用商店上传图像为公共的这意味着找到 URL 的任何人可以访问图像。</span><span class="sxs-lookup"><span data-stu-id="25206-161">The Fix It app stores uploaded images as public, meaning that anyone who finds the URL can access the images.</span></span> <span data-ttu-id="25206-162">而不是公用的方式保护映像。</span><span class="sxs-lookup"><span data-stu-id="25206-162">The images could be secured instead of public.</span></span>

### <a name="no-powershell-automation-scripts-for-queues"></a><span data-ttu-id="25206-163">队列没有 PowerShell 自动化脚本</span><span class="sxs-lookup"><span data-stu-id="25206-163">No PowerShell automation scripts for queues</span></span>

<span data-ttu-id="25206-164">Automation 示例 PowerShell 脚本是仅为修复它完全在 Azure 应用服务 Web 应用中运行的基础版本编写的。</span><span class="sxs-lookup"><span data-stu-id="25206-164">Sample PowerShell automation scripts were written only for the base version of Fix It that runs entirely in Azure App Service Web Apps.</span></span> <span data-ttu-id="25206-165">我们尚未提供用于设置和部署到 web 应用和云服务环境所需的队列处理的脚本。</span><span class="sxs-lookup"><span data-stu-id="25206-165">We haven't provided scripts for setting up and deploying to the web app plus Cloud Service environment required for queue processing.</span></span>

### <a name="special-handling-for-html-codes-in-user-input"></a><span data-ttu-id="25206-166">对用户输入中的 HTML 代码的特殊处理</span><span class="sxs-lookup"><span data-stu-id="25206-166">Special handling for HTML codes in user input</span></span>

<span data-ttu-id="25206-167">ASP.NET 自动防止恶意用户可能会通过在用户输入的文本框中输入脚本跨站点脚本攻击尝试在其中的许多方面。</span><span class="sxs-lookup"><span data-stu-id="25206-167">ASP.NET automatically prevents many ways in which malicious users might attempt cross-site scripting attacks by entering script in user input text boxes.</span></span> <span data-ttu-id="25206-168">和 MVC`DisplayFor`用来显示任务的帮助器标题和说明会自动进行 HTML 编码的值发送到浏览器。</span><span class="sxs-lookup"><span data-stu-id="25206-168">And the MVC `DisplayFor` helper used to display task titles and notes automatically HTML-encodes values that it sends to the browser.</span></span> <span data-ttu-id="25206-169">但在生产应用中，可能想要采取其他措施。</span><span class="sxs-lookup"><span data-stu-id="25206-169">But in a production app you might want to take additional measures.</span></span> <span data-ttu-id="25206-170">有关详细信息，请参阅[在 ASP.NET 请求验证](https://msdn.microsoft.com/library/hh882339.aspx)。</span><span class="sxs-lookup"><span data-stu-id="25206-170">For more information, see [Request Validation in ASP.NET](https://msdn.microsoft.com/library/hh882339.aspx).</span></span>

<a id="bestpractices"></a>
## <a name="best-practices"></a><span data-ttu-id="25206-171">最佳实践</span><span class="sxs-lookup"><span data-stu-id="25206-171">Best practices</span></span>

<span data-ttu-id="25206-172">以下是一些代码评审中发现和修复其应用程序的原始版本的测试已修复后的问题。</span><span class="sxs-lookup"><span data-stu-id="25206-172">Following are some issues that were fixed after being discovered in code review and testing of the original version of the Fix It app.</span></span> <span data-ttu-id="25206-173">一些而引起原始代码编写者不是特定的最佳做法，了解一些只因为代码快速写入，并且不适用于发布的软件。</span><span class="sxs-lookup"><span data-stu-id="25206-173">Some were caused by the original coder not being aware of a particular best practice, some simply because the code was written quickly and wasn't intended for released software.</span></span> <span data-ttu-id="25206-174">我们正在列出此处的问题，以防还有一些我们得出此评审和测试，可能有帮助的其他人也在开发 web 应用。</span><span class="sxs-lookup"><span data-stu-id="25206-174">We're listing the issues here in case there's something we learned from this review and testing that might be helpful to others who are also developing web apps.</span></span>

### <a name="dispose-the-database-repository"></a><span data-ttu-id="25206-175">释放数据库存储库</span><span class="sxs-lookup"><span data-stu-id="25206-175">Dispose the database repository</span></span>

<span data-ttu-id="25206-176">`FixItTaskRepository`类必须释放 Entity Framework`DbContext`实例。</span><span class="sxs-lookup"><span data-stu-id="25206-176">The `FixItTaskRepository` class must dispose the Entity Framework `DbContext` instance.</span></span> <span data-ttu-id="25206-177">我们是通过实现`IDisposable`在`FixItTaskRepository`类：</span><span class="sxs-lookup"><span data-stu-id="25206-177">We did this by implementing `IDisposable` in the `FixItTaskRepository` class:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample1.cs)]

<span data-ttu-id="25206-178">请注意，将自动释放 AutoFac`FixItTaskRepository`实例，因此我们无需显式释放。</span><span class="sxs-lookup"><span data-stu-id="25206-178">Note that AutoFac will automatically dispose the `FixItTaskRepository` instance, so we don't need to explicitly dispose it.</span></span>

<span data-ttu-id="25206-179">另一种方法是删除`DbContext`成员变量，从`FixItTaskRepository`，并改为创建一个本地`DbContext`变量在每个存储库方法中，内部`using`语句。</span><span class="sxs-lookup"><span data-stu-id="25206-179">Another option is to remove the `DbContext` member variable from `FixItTaskRepository`, and instead create a local `DbContext` variable within each repository method, inside a `using` statement.</span></span> <span data-ttu-id="25206-180">例如：</span><span class="sxs-lookup"><span data-stu-id="25206-180">For example:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample2.cs)]

### <a name="register-singletons-as-such-with-di"></a><span data-ttu-id="25206-181">这种情况下注册 DI 的单一实例</span><span class="sxs-lookup"><span data-stu-id="25206-181">Register singletons as such with DI</span></span>

<span data-ttu-id="25206-182">由于只有一个实例`PhotoService`类和`Logger`需要类时，这些类就[注册为单一实例的依赖项注入](https://code.google.com/p/autofac/wiki/InstanceScope)中*DependenciesConfig.cs*:</span><span class="sxs-lookup"><span data-stu-id="25206-182">Since only one instance of the `PhotoService` class and `Logger` class is needed, these classes should be [registered as single instances for dependency injection](https://code.google.com/p/autofac/wiki/InstanceScope) in *DependenciesConfig.cs*:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample3.cs?highlight=1,3)]

### <a name="security-dont-show-error-details-to-users"></a><span data-ttu-id="25206-183">安全性：不向用户显示错误详细信息</span><span class="sxs-lookup"><span data-stu-id="25206-183">Security: Don't show error details to users</span></span>

<span data-ttu-id="25206-184">Fix It 应用原始未包含常规错误页面，并只是让所有异常气泡至 UI，因此一些例外情况，例如数据库连接错误可能会导致显示在浏览器的完整堆栈跟踪。</span><span class="sxs-lookup"><span data-stu-id="25206-184">The original Fix It app didn't have a generic error page and just let all exceptions bubble up to the UI, so some exceptions such as database connection errors could result in a full stack trace being displayed to the browser.</span></span> <span data-ttu-id="25206-185">详细的错误消息有时可以方便地被恶意用户攻击。</span><span class="sxs-lookup"><span data-stu-id="25206-185">Detailed error information can sometimes facilitate attacks by malicious users.</span></span> <span data-ttu-id="25206-186">解决方案是记录异常详细信息并显示一个错误页面不包含错误详细信息的用户。</span><span class="sxs-lookup"><span data-stu-id="25206-186">The solution is to log the exception details and display an error page to the user that doesn't include error details.</span></span> <span data-ttu-id="25206-187">已记录 Fix It 应用，并为了显示一个错误页面，我们添加`<customErrors mode=On>`Web.config 文件中。</span><span class="sxs-lookup"><span data-stu-id="25206-187">The Fix It app was already logging, and in order to display an error page, we added `<customErrors mode=On>` in the Web.config file.</span></span>

[!code-xml[Main](the-fix-it-sample-application/samples/sample4.xml?highlight=2)]

<span data-ttu-id="25206-188">默认情况下这会导致*Views\Shared\Error.cshtml*若要显示的错误。</span><span class="sxs-lookup"><span data-stu-id="25206-188">By default this causes *Views\Shared\Error.cshtml* to be displayed for errors.</span></span> <span data-ttu-id="25206-189">你可以自定义*Error.cshtml*或创建你自己的错误页面视图，并添加`defaultRedirect`属性。</span><span class="sxs-lookup"><span data-stu-id="25206-189">You can customize *Error.cshtml* or create your own error page view and add a `defaultRedirect` attribute.</span></span> <span data-ttu-id="25206-190">此外可以指定不同的错误页面的特定错误。</span><span class="sxs-lookup"><span data-stu-id="25206-190">You can also specify different error pages for specific errors.</span></span>

### <a name="security-only-allow-a-task-to-be-edited-by-its-creator"></a><span data-ttu-id="25206-191">安全性： 仅允许由其创建者要编辑的任务</span><span class="sxs-lookup"><span data-stu-id="25206-191">Security: only allow a task to be edited by its creator</span></span>

<span data-ttu-id="25206-192">仪表板索引页仅显示任务创建的登录的用户，但恶意用户可以使用到另一个用户的任务的 ID 创建一个 URL。</span><span class="sxs-lookup"><span data-stu-id="25206-192">The Dashboard Index page only shows tasks created by the logged-on user, but a malicious user could create a URL with an ID to another user's task.</span></span> <span data-ttu-id="25206-193">我们添加了中的代码*DashboardController.cs*以这种情况下返回 404 错误：</span><span class="sxs-lookup"><span data-stu-id="25206-193">We added code in *DashboardController.cs* to return a 404 in that case:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample5.cs?highlight=9-14,24-29)]

### <a name="dont-swallow-exceptions"></a><span data-ttu-id="25206-194">不抑制异常</span><span class="sxs-lookup"><span data-stu-id="25206-194">Don't swallow exceptions</span></span>

<span data-ttu-id="25206-195">Fix It 应用原始只返回了 null 在日志中记录的 SQL 查询产生异常：</span><span class="sxs-lookup"><span data-stu-id="25206-195">The original Fix It app just returned null after logging an exception that resulted from a SQL query:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample6.cs?highlight=4)]

<span data-ttu-id="25206-196">这将使其呈现给用户，因为如果查询成功，但只是未返回任何行。</span><span class="sxs-lookup"><span data-stu-id="25206-196">This would make it look to the user as if the query succeeded but just didn't return any rows.</span></span> <span data-ttu-id="25206-197">解决方案是重新引发异常后捕获和日志记录：</span><span class="sxs-lookup"><span data-stu-id="25206-197">Solution is to re-throw the exception after catching and logging:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample7.cs)]

### <a name="catch-all-exceptions-in-worker-roles"></a><span data-ttu-id="25206-198">在辅助角色中捕捉所有异常</span><span class="sxs-lookup"><span data-stu-id="25206-198">Catch all exceptions in worker roles</span></span>

<span data-ttu-id="25206-199">在辅助角色中的任何未处理的异常会导致 VM 才能将回收，因此想要将所有内容包装在 try catch 块中执行操作和处理所有异常。</span><span class="sxs-lookup"><span data-stu-id="25206-199">Any unhandled exceptions in a worker role will cause the VM to be recycled, so you want to wrap everything you do in a try-catch block and handle all exceptions.</span></span>

### <a name="specify-length-for-string-properties-in-entity-classes"></a><span data-ttu-id="25206-200">在实体类中指定的字符串属性的长度</span><span class="sxs-lookup"><span data-stu-id="25206-200">Specify length for string properties in entity classes</span></span>

<span data-ttu-id="25206-201">若要显示简单的代码，请修复其应用程序的原始版本未指定 FixItTask 实体的字段长度并因此它们被定义为 varchar （max） 在数据库中。</span><span class="sxs-lookup"><span data-stu-id="25206-201">In order to display simple code, the original version of the Fix It app didn't specify lengths for the fields of the FixItTask entity, and as a result they were defined as varchar(max) in the database.</span></span> <span data-ttu-id="25206-202">因此，UI 将接受几乎任何数量的输入。</span><span class="sxs-lookup"><span data-stu-id="25206-202">As a result, the UI would accept almost any amount of input.</span></span> <span data-ttu-id="25206-203">将同时应用于用户的指定长度集限制输入中的网页和在数据库中的列大小：</span><span class="sxs-lookup"><span data-stu-id="25206-203">Specifying lengths sets limits that apply both to user input in the web page and column size in the database:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample8.cs?highlight=4,7,10,12,14)]

### <a name="mark-private-members-as-readonly-when-they-arent-expected-to-change"></a><span data-ttu-id="25206-204">将私有成员标记为 readonly，当它们不预期的更改时</span><span class="sxs-lookup"><span data-stu-id="25206-204">Mark private members as readonly when they aren't expected to change</span></span>

<span data-ttu-id="25206-205">例如，在`DashboardController`类的实例`FixItTaskRepository`创建，并且不更改，因此我们把它作为定义[readonly](https://msdn.microsoft.com/library/acdd6hb7.aspx)。</span><span class="sxs-lookup"><span data-stu-id="25206-205">For example, in the `DashboardController` class an instance of `FixItTaskRepository` is created and isn't expected to change, so we defined it as [readonly](https://msdn.microsoft.com/library/acdd6hb7.aspx).</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample9.cs?highlight=3)]

### <a name="use-listany-instead-of-listcount-gt-0"></a><span data-ttu-id="25206-206">使用列表。Any （)，而不是列表。Count （) &gt; 0</span><span class="sxs-lookup"><span data-stu-id="25206-206">Use list.Any() instead of list.Count() &gt; 0</span></span>

<span data-ttu-id="25206-207">如果您所有你关注的信息列表中的一个或多个项是否适合指定的条件，请使用[任何](https://msdn.microsoft.com/library/bb534972.aspx)方法，因为它返回立即找到适合条件的项，而`Count`方法始终必须循环访问通过每个项。</span><span class="sxs-lookup"><span data-stu-id="25206-207">If you all you care about is whether one or more items in a list fit the specified criteria, use the [Any](https://msdn.microsoft.com/library/bb534972.aspx) method, because it returns as soon as an item fitting the criteria is found, whereas the `Count` method always has to iterate through every item.</span></span> <span data-ttu-id="25206-208">在仪表板*Index.cshtml*文件最初具有此代码：</span><span class="sxs-lookup"><span data-stu-id="25206-208">The Dashboard *Index.cshtml* file originally had this code:</span></span>

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample10.cshtml)]

<span data-ttu-id="25206-209">我们将它更改为：</span><span class="sxs-lookup"><span data-stu-id="25206-209">We changed it to this:</span></span>

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample11.cshtml?highlight=1)]

### <a name="generate-urls-in-mvc-views-using-mvc-helpers"></a><span data-ttu-id="25206-210">在使用 MVC 帮助程序的 MVC 视图中生成的 Url</span><span class="sxs-lookup"><span data-stu-id="25206-210">Generate URLs in MVC views using MVC helpers</span></span>

<span data-ttu-id="25206-211">有关**创建 Fix It**按钮在主页上，修复其应用程序硬编码的定位点元素：</span><span class="sxs-lookup"><span data-stu-id="25206-211">For the **Create a Fix It** button on the home page, the Fix It app hard coded an anchor element:</span></span>

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample12.cshtml)]

<span data-ttu-id="25206-212">有关此类的视图/操作链接最好使用[Url.Action](https://msdn.microsoft.com/library/system.web.mvc.urlhelper.action.aspx) HTML 帮助器，例如：</span><span class="sxs-lookup"><span data-stu-id="25206-212">For View/Action links like this it's better to use the [Url.Action](https://msdn.microsoft.com/library/system.web.mvc.urlhelper.action.aspx) HTML helper, for example:</span></span>

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample13.cshtml)]

### <a name="use-taskdelay-instead-of-threadsleep-in-worker-role"></a><span data-ttu-id="25206-213">在辅助角色中使用而不是 Thread.Sleep 的 Task.Delay</span><span class="sxs-lookup"><span data-stu-id="25206-213">Use Task.Delay instead of Thread.Sleep in worker role</span></span>

<span data-ttu-id="25206-214">新项目模板将`Thread.Sleep`在示例代码辅助角色，而导致线程进入休眠状态可能会导致要生成其他不必要的线程的线程池。</span><span class="sxs-lookup"><span data-stu-id="25206-214">The new-project template puts `Thread.Sleep` in the sample code for a worker role, but causing the thread to sleep can cause the thread pool to spawn additional unnecessary threads.</span></span> <span data-ttu-id="25206-215">可以通过使用避免这[Task.Delay](https://msdn.microsoft.com/library/hh139096.aspx)相反。</span><span class="sxs-lookup"><span data-stu-id="25206-215">You can avoid that by using [Task.Delay](https://msdn.microsoft.com/library/hh139096.aspx) instead.</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample14.cs?highlight=11)]

### <a name="avoid-async-void"></a><span data-ttu-id="25206-216">避免 async void</span><span class="sxs-lookup"><span data-stu-id="25206-216">Avoid async void</span></span>

<span data-ttu-id="25206-217">如果异步方法不需要返回一个值，则返回`Task`类型而非`void`。</span><span class="sxs-lookup"><span data-stu-id="25206-217">If an async method doesn't need to return a value, return a `Task` type rather than `void`.</span></span>

<span data-ttu-id="25206-218">此示例摘自`FixItQueueManager`类：</span><span class="sxs-lookup"><span data-stu-id="25206-218">This example is from the `FixItQueueManager` class:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample15.cs)]

<span data-ttu-id="25206-219">应使用`async void`仅为顶级事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="25206-219">You should use `async void` only for top-level event handlers.</span></span> <span data-ttu-id="25206-220">如果定义一个方法作为`async void`，调用方不能**await**方法或捕获该方法将引发任何异常。</span><span class="sxs-lookup"><span data-stu-id="25206-220">If you define a method as `async void`, the caller cannot **await** the method or catch any exceptions the method throws.</span></span> <span data-ttu-id="25206-221">有关详细信息，请参阅[中的异步编程的最佳做法](https://msdn.microsoft.com/magazine/jj991977.aspx)。</span><span class="sxs-lookup"><span data-stu-id="25206-221">For more information, see [Best Practices in Asynchronous Programming](https://msdn.microsoft.com/magazine/jj991977.aspx).</span></span>

### <a name="use-a-cancellation-token-to-break-from-worker-role-loop"></a><span data-ttu-id="25206-222">使用取消标记来中断工作线程角色循环</span><span class="sxs-lookup"><span data-stu-id="25206-222">Use a cancellation token to break from worker role loop</span></span>

<span data-ttu-id="25206-223">通常情况下，**运行**辅助角色上的方法包含无限循环。</span><span class="sxs-lookup"><span data-stu-id="25206-223">Typically, the **Run** method on a worker role contains an infinite loop.</span></span> <span data-ttu-id="25206-224">辅助角色停止时， [RoleEntryPoint.OnStop](https://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstop.aspx)调用方法。</span><span class="sxs-lookup"><span data-stu-id="25206-224">When the worker role is stopping, the [RoleEntryPoint.OnStop](https://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstop.aspx) method is called.</span></span> <span data-ttu-id="25206-225">应使用此方法来取消内部完成工作**运行**方法并退出正常。</span><span class="sxs-lookup"><span data-stu-id="25206-225">You should use this method to cancel the work that is being done inside the **Run** method and exit gracefully.</span></span> <span data-ttu-id="25206-226">否则，进程可能正在操作终止。</span><span class="sxs-lookup"><span data-stu-id="25206-226">Otherwise, the process might be terminated in the middle of an operation.</span></span>

### <a name="opt-out-of-automatic-mime-sniffing-procedure"></a><span data-ttu-id="25206-227">选择禁用自动 MIME 探查过程</span><span class="sxs-lookup"><span data-stu-id="25206-227">Opt out of Automatic MIME Sniffing Procedure</span></span>

<span data-ttu-id="25206-228">在某些情况下，Internet Explorer 报告不同于由 web 服务器指定的类型的 MIME 类型。</span><span class="sxs-lookup"><span data-stu-id="25206-228">In some cases, Internet Explorer reports a MIME type different than the type specified by the web server.</span></span> <span data-ttu-id="25206-229">例如，如果 Internet Explorer 找到 HTML 内容传递使用 HTTP 响应标头的内容类型的文件中： text/plain Internet 资源管理器确定内容应呈现为 HTML。</span><span class="sxs-lookup"><span data-stu-id="25206-229">For instance, if Internet Explorer finds HTML content in a file delivered with the HTTP response header Content-Type: text/plain, Internet Explorer determines that the content should be rendered as HTML.</span></span> <span data-ttu-id="25206-230">遗憾的是，此"MIME 探查"可能也会导致服务器承载不受信任的内容的安全问题。</span><span class="sxs-lookup"><span data-stu-id="25206-230">Unfortunately, this "MIME-sniffing" can also lead to security problems for servers hosting untrusted content.</span></span> <span data-ttu-id="25206-231">若要克服此问题，Internet Explorer 8 对 MIME 类型确定代码中进行了大量更改，并允许应用程序开发人员[选择退出 MIME 探查](https://blogs.msdn.com/b/ie/archive/2008/07/02/ie8-security-part-v-comprehensive-protection.aspx)。</span><span class="sxs-lookup"><span data-stu-id="25206-231">To combat this problem, Internet Explorer 8 has made a number of changes to MIME-type determination code and allows application developers to [opt out of MIME-sniffing](https://blogs.msdn.com/b/ie/archive/2008/07/02/ie8-security-part-v-comprehensive-protection.aspx).</span></span> <span data-ttu-id="25206-232">以下代码添加到*Web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="25206-232">The following code was added to the *Web.config* file.</span></span>

[!code-xml[Main](the-fix-it-sample-application/samples/sample16.xml?highlight=2-7)]

### <a name="enable-bundling-and-minification"></a><span data-ttu-id="25206-233">启用捆绑和缩小</span><span class="sxs-lookup"><span data-stu-id="25206-233">Enable bundling and minification</span></span>

<span data-ttu-id="25206-234">当 Visual Studio 创建新的 web 项目时，默认情况下是未启用 JavaScript 文件的捆绑和缩小。</span><span class="sxs-lookup"><span data-stu-id="25206-234">When Visual Studio creates a new web project, bundling and minification of JavaScript files is not enabled by default.</span></span> <span data-ttu-id="25206-235">我们在 BundleConfig.cs 中添加一行代码：</span><span class="sxs-lookup"><span data-stu-id="25206-235">We added a line of code in BundleConfig.cs:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample17.cs?highlight=9)]

### <a name="set-an-expiration-time-out-for-authentication-cookies"></a><span data-ttu-id="25206-236">设置身份验证 cookie 的到期超时</span><span class="sxs-lookup"><span data-stu-id="25206-236">Set an expiration time-out for authentication cookies</span></span>

<span data-ttu-id="25206-237">默认情况下，身份验证 cookie 在两周后过期。</span><span class="sxs-lookup"><span data-stu-id="25206-237">By default, authentication cookies expire in two weeks.</span></span> <span data-ttu-id="25206-238">较短的时间会更加安全。</span><span class="sxs-lookup"><span data-stu-id="25206-238">A shorter time is more secure.</span></span> <span data-ttu-id="25206-239">可以更改此设置在*StartupAuth.cs*:</span><span class="sxs-lookup"><span data-stu-id="25206-239">You can change this setting in *StartupAuth.cs*:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample18.cs?highlight=4-5)]

<a id="run-in-vs"></a>
## <a name="how-to-run-the-app-from-visual-studio-on-your-local-computer"></a><span data-ttu-id="25206-240">如何从 Visual Studio 在本地计算机上运行该应用程序</span><span class="sxs-lookup"><span data-stu-id="25206-240">How to run the app from Visual Studio on your local computer</span></span>

<span data-ttu-id="25206-241">有两种方法来运行修复其应用：</span><span class="sxs-lookup"><span data-stu-id="25206-241">There are two ways to run the Fix It app:</span></span>

- <span data-ttu-id="25206-242">运行新任务将直接写入到 SQL 数据库的基本应用程序。</span><span class="sxs-lookup"><span data-stu-id="25206-242">Run the base application that writes new tasks directly to the SQL database.</span></span>
- <span data-ttu-id="25206-243">运行应用程序使用队列以及后端服务创建的任务。</span><span class="sxs-lookup"><span data-stu-id="25206-243">Run the application using a queue plus a backend service to create tasks.</span></span> <span data-ttu-id="25206-244">队列模式一章中所述[以队列为中心的工作模式](queue-centric-work-pattern.md)。</span><span class="sxs-lookup"><span data-stu-id="25206-244">The queue pattern is described in the chapter [Queue-Centric Work Pattern](queue-centric-work-pattern.md).</span></span>

<a id="runbase"></a>
### <a name="run-the-base-application"></a><span data-ttu-id="25206-245">运行基本的应用程序</span><span class="sxs-lookup"><span data-stu-id="25206-245">Run the base application</span></span>

1. <span data-ttu-id="25206-246">安装[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)。</span><span class="sxs-lookup"><span data-stu-id="25206-246">Install [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017).</span></span>
2. <span data-ttu-id="25206-247">安装[针对 Visual Studio 用于.NET 的 Azure SDK](https://azure.microsoft.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="25206-247">Install the [Azure SDK for .NET for Visual Studio](https://azure.microsoft.com/downloads/).</span></span>
3. <span data-ttu-id="25206-248">下载.zip 文件[MSDN 代码库](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)。</span><span class="sxs-lookup"><span data-stu-id="25206-248">Download the .zip file from the [MSDN Code Gallery](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4).</span></span>
4. <span data-ttu-id="25206-249">在文件资源管理器，右键单击.zip 文件并单击属性，然后在属性窗口中单击取消阻止。</span><span class="sxs-lookup"><span data-stu-id="25206-249">In File Explorer, right-click the .zip file and click Properties, then in the Properties window click Unblock.</span></span>
5. <span data-ttu-id="25206-250">将文件解压缩。</span><span class="sxs-lookup"><span data-stu-id="25206-250">Unzip the file.</span></span>
6. <span data-ttu-id="25206-251">双击.sln 文件以启动 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="25206-251">Double-click the .sln file to launch Visual Studio.</span></span>
7. <span data-ttu-id="25206-252">从**工具**菜单上，单击**NuGet 包管理器**，然后**程序包管理器控制台**。</span><span class="sxs-lookup"><span data-stu-id="25206-252">From the **Tools** menu, click **NuGet Package Manager**, then **Package Manager Console**.</span></span>
8. <span data-ttu-id="25206-253">在包管理器控制台 (PMC) 中，单击还原。</span><span class="sxs-lookup"><span data-stu-id="25206-253">In the Package Manager Console (PMC), click Restore.</span></span>
9. <span data-ttu-id="25206-254">退出 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="25206-254">Exit Visual Studio.</span></span>
10. <span data-ttu-id="25206-255">启动[Azure 存储模拟器](/azure/storage/common/storage-use-emulator)。</span><span class="sxs-lookup"><span data-stu-id="25206-255">Start the [Azure storage emulator](/azure/storage/common/storage-use-emulator).</span></span>
11. <span data-ttu-id="25206-256">重新启动 Visual Studio 中，打开上一步中要关闭的解决方案文件。</span><span class="sxs-lookup"><span data-stu-id="25206-256">Restart Visual Studio, opening the solution file you closed in the previous step.</span></span>
12. <span data-ttu-id="25206-257">请确保 fix It 项目设置为启动项目，然后按 CTRL + F5 以运行该项目。</span><span class="sxs-lookup"><span data-stu-id="25206-257">Make sure the FixIt project is set as the startup project, and then press CTRL+F5 to run the project.</span></span>

<a id="queueslocal"></a>
### <a name="run-the-application-with-queue-processing"></a><span data-ttu-id="25206-258">与队列处理运行应用程序</span><span class="sxs-lookup"><span data-stu-id="25206-258">Run the application with queue processing</span></span>

1. <span data-ttu-id="25206-259">遵循的指导[运行基本的应用程序](#runbase)，然后关闭浏览器并关闭 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="25206-259">Follow the directions for [Run the base application](#runbase), and then close the browser and close Visual Studio.</span></span>
2. <span data-ttu-id="25206-260">使用管理员权限启动 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="25206-260">Start Visual Studio with administrator privileges.</span></span> <span data-ttu-id="25206-261">（您将使用 Azure 计算仿真程序，并且需要管理员权限。）</span><span class="sxs-lookup"><span data-stu-id="25206-261">(You'll be using the Azure compute emulator, and that requires administrator privileges.)</span></span>
3. <span data-ttu-id="25206-262">在应用程序中*Web.config*中的文件*MyFixIt*项目 （web 项目） 中，更改的值`appSettings/UseQueues`为"true":</span><span class="sxs-lookup"><span data-stu-id="25206-262">In the application *Web.config* file in the *MyFixIt* project (the web project), change the value of `appSettings/UseQueues` to "true":</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample19.cmd?highlight=3)]
4. <span data-ttu-id="25206-263">如果[Azure 存储模拟器](https://msdn.microsoft.com/library/windowsazure/hh403989.aspx)不是仍在运行，重新启动它。</span><span class="sxs-lookup"><span data-stu-id="25206-263">If the [Azure storage emulator](https://msdn.microsoft.com/library/windowsazure/hh403989.aspx) isn't still running, start it again.</span></span>
5. <span data-ttu-id="25206-264">同时运行 FixIt web 项目和 MyFixItCloudService 项目。</span><span class="sxs-lookup"><span data-stu-id="25206-264">Run the FixIt web project and the MyFixItCloudService project simultaneously.</span></span>

    <span data-ttu-id="25206-265">使用 Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="25206-265">Using Visual Studio:</span></span>

   1. <span data-ttu-id="25206-266">按**F5**运行 fix It 项目。</span><span class="sxs-lookup"><span data-stu-id="25206-266">Press **F5** to run the FixIt project.</span></span>
   2. <span data-ttu-id="25206-267">在中**解决方案资源管理器**，右键单击 MyFixItCloudService 项目，然后单击**调试** > **启动新实例**。</span><span class="sxs-lookup"><span data-stu-id="25206-267">In **Solution Explorer**, right-click the MyFixItCloudService project, and then click **Debug** > **Start New Instance**.</span></span>

    <span data-ttu-id="25206-268">使用 Visual Studio 2013 Express for Web:</span><span class="sxs-lookup"><span data-stu-id="25206-268">Using Visual Studio 2013 Express for Web:</span></span>

   3. <span data-ttu-id="25206-269">在解决方案资源管理器，右键单击 fix It 解决方案，然后选择**属性**。</span><span class="sxs-lookup"><span data-stu-id="25206-269">In Solution Explorer, right-click the FixIt solution and select **Properties**.</span></span>
   4. <span data-ttu-id="25206-270">选择**多个启动项目**。</span><span class="sxs-lookup"><span data-stu-id="25206-270">Select **Multiple Startup Projects**.</span></span>
   5. <span data-ttu-id="25206-271">在中**操作**下 MyFixIt 和 MyFixItCloudService，下拉列表中的选择**启动**。</span><span class="sxs-lookup"><span data-stu-id="25206-271">In the **Action** dropdown list under MyFixIt and MyFixItCloudService, select **Start**.</span></span>
   6. <span data-ttu-id="25206-272">单击 **“确定”**。</span><span class="sxs-lookup"><span data-stu-id="25206-272">Click **OK**.</span></span>
   7. <span data-ttu-id="25206-273">按**F5**运行这两个项目。</span><span class="sxs-lookup"><span data-stu-id="25206-273">Press **F5** to run both projects.</span></span>

      <span data-ttu-id="25206-274">运行 MyFixItCloudService 项目时，Visual Studio 将启动 Azure 计算仿真程序。</span><span class="sxs-lookup"><span data-stu-id="25206-274">When you run the MyFixItCloudService project, Visual Studio starts the Azure compute emulator.</span></span> <span data-ttu-id="25206-275">根据您的防火墙配置，可能需要允许通过防火墙的仿真程序。</span><span class="sxs-lookup"><span data-stu-id="25206-275">Depending on your firewall configuration, you might need to allow the emulator through the firewall.</span></span>

<a id="deploybase"></a>
## <a name="how-to-deploy-the-base-app-to-azure-app-service-web-apps-by-using-the-windows-powershell-scripts"></a><span data-ttu-id="25206-276">如何将基本应用程序部署到 Azure 应用服务 Web 应用，通过使用 Windows PowerShell 脚本</span><span class="sxs-lookup"><span data-stu-id="25206-276">How to deploy the base app to Azure App Service Web Apps by using the Windows PowerShell scripts</span></span>

<span data-ttu-id="25206-277">为了说明[使一切自动化](automate-everything.md)模式，修复其应用程序提供的设置在 Azure 中的环境并将项目部署到新环境的脚本。</span><span class="sxs-lookup"><span data-stu-id="25206-277">To illustrate the [Automate Everything](automate-everything.md) pattern, the Fix It app is supplied with scripts that set up an environment in Azure and deploy the project to the new environment.</span></span> <span data-ttu-id="25206-278">下面的说明解释如何使用脚本。</span><span class="sxs-lookup"><span data-stu-id="25206-278">The following instructions explain how to use the scripts.</span></span>

<span data-ttu-id="25206-279">如果你想要在 Azure 中运行而无需使用队列，并且进行了更改后，若要使用队列在本地运行，请确保将 UseQueues appSetting 值设置回 false 之前继续执行下面的说明。</span><span class="sxs-lookup"><span data-stu-id="25206-279">If you want to run in Azure without using queues, and you made the changes to run locally with queues, make sure you set the UseQueues appSetting value back to false before proceeding with the following instructions.</span></span>

<span data-ttu-id="25206-280">这些说明假定您已经下载并本地运行时 Fix It 解决方案，并获得了 Azure 帐户，或具有 Azure 订阅有权管理。</span><span class="sxs-lookup"><span data-stu-id="25206-280">These instructions assume you have already downloaded and run the Fix It solution locally, and that you have an Azure account or have an Azure subscription that you are authorized to manage.</span></span>

1. <span data-ttu-id="25206-281">安装**Azure PowerShell**控制台。</span><span class="sxs-lookup"><span data-stu-id="25206-281">Install the **Azure PowerShell** console.</span></span> <span data-ttu-id="25206-282">有关说明，请参阅[如何安装和配置 Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-4.3.1)。</span><span class="sxs-lookup"><span data-stu-id="25206-282">For instructions, see [How to install and configure Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-4.3.1).</span></span>

    <span data-ttu-id="25206-283">此自定义的控制台配置为使用你的 Azure 订阅。</span><span class="sxs-lookup"><span data-stu-id="25206-283">This customized console is configured to work with your Azure subscription.</span></span> <span data-ttu-id="25206-284">在安装 Azure 模块*Program Files*目录并在每次使用 Azure PowerShell 控制台中自动导入。</span><span class="sxs-lookup"><span data-stu-id="25206-284">The Azure module is installed in the *Program Files* directory and is automatically imported on every use of the Azure PowerShell console.</span></span>

    <span data-ttu-id="25206-285">如果想要使用不同的主机程序，如 Windows PowerShell ISE 中，请务必使用[导入模块](https://go.microsoft.com/fwlink/?LinkID=141553)cmdlet 导入 Azure 模块或使用 Azure 模块中的命令来触发自动导入的模块。</span><span class="sxs-lookup"><span data-stu-id="25206-285">If you prefer to work in a different host program, such as Windows PowerShell ISE, be sure to use the [Import-Module](https://go.microsoft.com/fwlink/?LinkID=141553) cmdlet to import the Azure module or use a command in the Azure module to trigger automatic importing of the module.</span></span>
2. <span data-ttu-id="25206-286">启动 Azure PowerShell**以管理员身份运行**选项。</span><span class="sxs-lookup"><span data-stu-id="25206-286">Start Azure PowerShell with the **Run as administrator** option.</span></span>
3. <span data-ttu-id="25206-287">运行[Set-executionpolicy](https://go.microsoft.com/fwlink/p/?linkid=293941) cmdlet 来将 Azure PowerShell 执行策略设为`RemoteSigned`。</span><span class="sxs-lookup"><span data-stu-id="25206-287">Run the [Set-ExecutionPolicy](https://go.microsoft.com/fwlink/p/?linkid=293941) cmdlet to set the Azure PowerShell execution policy to `RemoteSigned`.</span></span> <span data-ttu-id="25206-288">输入**Y** （为否) 以完成策略更改。</span><span class="sxs-lookup"><span data-stu-id="25206-288">Enter **Y** (for Yes) to complete the policy change.</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample20.cmd)]

    <span data-ttu-id="25206-289">此设置，可运行本地未进行数字签名的脚本。</span><span class="sxs-lookup"><span data-stu-id="25206-289">This setting enables you to run local scripts that aren't digitally signed.</span></span> <span data-ttu-id="25206-290">(还可以设置执行策略为`Unrestricted`，这会消除对取消阻止步骤的需要更高版本，但不是建议这样做出于安全原因。)</span><span class="sxs-lookup"><span data-stu-id="25206-290">(You can also set the execution policy to `Unrestricted`, which would eliminate the need for the unblock step later, but this is not recommended for security reasons.)</span></span>
4. <span data-ttu-id="25206-291">运行`Add-AzureAccount`cmdlet 与你的帐户的凭据设置 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="25206-291">Run the `Add-AzureAccount` cmdlet to set up PowerShell with credentials for your account.</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample21.cmd)]

    <span data-ttu-id="25206-292">这些凭据在一段时间后过期，您必须重新运行`Add-AzureAccount`cmdlet。</span><span class="sxs-lookup"><span data-stu-id="25206-292">These credentials expire after a period of time and you have to re-run the `Add-AzureAccount` cmdlet.</span></span> <span data-ttu-id="25206-293">是在编写这本电子书，在凭据过期之前的时间限制为 12 小时。</span><span class="sxs-lookup"><span data-stu-id="25206-293">As this e-book is being written, the time limit before credentials expire is 12 hours.</span></span>
5. <span data-ttu-id="25206-294">如果你有多个订阅，请使用 Select-azuresubscription cmdlet 来指定想要创建测试环境中的订阅。</span><span class="sxs-lookup"><span data-stu-id="25206-294">If you have multiple subscriptions, use the Select-AzureSubscription cmdlet to specify the subscription you want to create the test environment in.</span></span>
6. <span data-ttu-id="25206-295">使用导入同一个 Azure 订阅的管理证书`Get-AzurePublishSettingsFile`和`Import-AzurePublishSettingsFile`cmdlet。</span><span class="sxs-lookup"><span data-stu-id="25206-295">Import a management certificate for the same Azure subscription by using the `Get-AzurePublishSettingsFile` and `Import-AzurePublishSettingsFile` cmdlets.</span></span> <span data-ttu-id="25206-296">这些 cmdlet 的第一个下载的证书文件，并为了将其导入在第二个指定该文件的位置。</span><span class="sxs-lookup"><span data-stu-id="25206-296">The first of these cmdlets downloads a certificate file, and in the second one you specify the location of that file in order to import it.</span></span> > [!IMPORTANT]
   > <span data-ttu-id="25206-297">将下载的文件保存在安全位置，或删除它完成后使用它，因为它包含可用于管理 Azure 服务的证书。</span><span class="sxs-lookup"><span data-stu-id="25206-297">Keep the downloaded file in a safe location or delete it when you're done with it, because it contains a certificate that can be used to manage your Azure services.</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample22.cmd)]

    <span data-ttu-id="25206-298">使用该证书才能设置 SQL 数据库服务器上的防火墙规则检测到开发计算机的 IP 地址的 REST API 调用。</span><span class="sxs-lookup"><span data-stu-id="25206-298">The certificate is used for a REST API call that detects the development machine's IP address in order to set a firewall rule on the SQL Database server.</span></span>
7. <span data-ttu-id="25206-299">运行[Set-location](https://go.microsoft.com/fwlink/p/?linkid=293912) cmdlet (别名`cd`， `chdir`，和`sl`) 若要导航到包含的脚本的目录。</span><span class="sxs-lookup"><span data-stu-id="25206-299">Run the [Set-Location](https://go.microsoft.com/fwlink/p/?linkid=293912) cmdlet (aliases are `cd`, `chdir`, and `sl`) to navigate to the directory that contains the scripts.</span></span> <span data-ttu-id="25206-300">(它们位于*自动化*Fix It 解决方案文件夹中的文件夹。)如果任何目录名称包含空格，请将路径用引号引起来。</span><span class="sxs-lookup"><span data-stu-id="25206-300">(They're located in the *Automation* folder in the Fix It solution folder.) Put the path in quotes if any of the directory names contain spaces.</span></span> <span data-ttu-id="25206-301">例如，若要导航到`c:\Sample Apps\FixIt\Automation`目录可以输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="25206-301">For example, to navigate to the `c:\Sample Apps\FixIt\Automation` directory you could enter the following command:</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample23.cmd)]
8. <span data-ttu-id="25206-302">若要允许 Windows PowerShell 以运行这些脚本，请使用[Unblock-file](https://go.microsoft.com/fwlink/p/?linkid=294021) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="25206-302">To allow Windows PowerShell to run these scripts, use the [Unblock-File](https://go.microsoft.com/fwlink/p/?linkid=294021) cmdlet.</span></span> <span data-ttu-id="25206-303">（脚本被阻止，因为它们从 Internet 下载。）</span><span class="sxs-lookup"><span data-stu-id="25206-303">(The scripts are blocked because they were downloaded from the Internet.)</span></span>

    > [!WARNING]
    > <span data-ttu-id="25206-304">安全性-然后再运行`Unblock-File`上任何脚本或可执行文件，在记事本中打开该文件、 检查命令，并验证它们是否包含任何恶意代码。</span><span class="sxs-lookup"><span data-stu-id="25206-304">Security - Before running `Unblock-File` on any script or executable file, open the file in Notepad, examine the commands, and verify that they do not contain any malicious code.</span></span>

    <span data-ttu-id="25206-305">例如，以下命令将运行`Unblock-File`cmdlet 在当前目录中的所有脚本。</span><span class="sxs-lookup"><span data-stu-id="25206-305">For example, the following command runs the `Unblock-File` cmdlet on all scripts in the current directory.</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample24.cmd)]
9. <span data-ttu-id="25206-306">若要创建适用于基 （未处理的队列） 的 web 应用修复其应用程序，请运行环境创建脚本。</span><span class="sxs-lookup"><span data-stu-id="25206-306">To create the web app for the base (no queues processing) Fix It app, run the environment creation script.</span></span>

    <span data-ttu-id="25206-307">所需`Name`参数指定的数据库的名称，还用于该脚本创建的存储帐户。</span><span class="sxs-lookup"><span data-stu-id="25206-307">The required `Name` parameter specifies the name of the database and is also used for the storage account that the script creates.</span></span> <span data-ttu-id="25206-308">名称必须全局唯一在 azurewebsites.net 域中。</span><span class="sxs-lookup"><span data-stu-id="25206-308">The name must be globally unique within the azurewebsites.net domain.</span></span> <span data-ttu-id="25206-309">如果指定的名称不是唯一的如 fix It 或测试 （或甚至是如下所示的示例中，fixitdemo） `New-AzureWebsite` cmdlet 失败并报告冲突发生内部错误。</span><span class="sxs-lookup"><span data-stu-id="25206-309">If you specify a name that is not unique, like Fixit or Test (or even as in the example, fixitdemo), the `New-AzureWebsite` cmdlet fails with an Internal Error that reports a conflict.</span></span> <span data-ttu-id="25206-310">该脚本将名称转换为全部小写，以符合的 web 应用、 存储帐户和数据库名称要求。</span><span class="sxs-lookup"><span data-stu-id="25206-310">The script converts the name to all lower-case to comply with name requirements for web apps, storage accounts, and databases.</span></span>

    <span data-ttu-id="25206-311">所需`SqlDatabasePassword`参数指定将为 SQL 数据库创建的管理员帐户的密码。</span><span class="sxs-lookup"><span data-stu-id="25206-311">The required `SqlDatabasePassword` parameter specifies the password for the admin account that will be created for SQL Database.</span></span> <span data-ttu-id="25206-312">不要在密码中包含特殊 XML 字符 (&amp; &lt; &gt; ;)。</span><span class="sxs-lookup"><span data-stu-id="25206-312">Don't include special XML characters in the password (&amp; &lt; &gt; ;).</span></span> <span data-ttu-id="25206-313">这是方法的 azure 的脚本编写的不属于限制的限制。</span><span class="sxs-lookup"><span data-stu-id="25206-313">This is a limitation of the way the scripts were written, not a limitation of Azure.</span></span>

    <span data-ttu-id="25206-314">例如，如果你想要创建名为"fixitdemo"的 web 应用和使用 SQL Server 管理员密码"Passw0rd1"，您可以输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="25206-314">For example, if you want to create a web app named "fixitdemo" and use a SQL Server administrator password of "Passw0rd1", you could enter the following command:</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample25.cmd)]

    <span data-ttu-id="25206-315">名称在 azurewebsites.net 域中，必须是唯一，并且密码必须满足密码复杂性的 SQL 数据库要求。</span><span class="sxs-lookup"><span data-stu-id="25206-315">The name must be unique in the azurewebsites.net domain, and the password must meet SQL Database requirements for password complexity.</span></span> <span data-ttu-id="25206-316">（示例 Passw0rd1 符合要求。）</span><span class="sxs-lookup"><span data-stu-id="25206-316">(The example Passw0rd1 does meet the requirements.)</span></span>

    <span data-ttu-id="25206-317">请注意，该命令将开始使用".\"。</span><span class="sxs-lookup"><span data-stu-id="25206-317">Note that the command begins with ".\".</span></span> <span data-ttu-id="25206-318">为了帮助防止恶意脚本的执行，Windows PowerShell 要求你运行脚本时提供的脚本文件的完全限定的路径。</span><span class="sxs-lookup"><span data-stu-id="25206-318">To help prevent malicious execution of scripts, Windows PowerShell requires that you provide the fully qualified path to the script file when you run a script.</span></span> <span data-ttu-id="25206-319">可以使用句点来指示当前目录 ("。\")或提供的完全限定的路径，例如：</span><span class="sxs-lookup"><span data-stu-id="25206-319">You can use a dot to indicate the current directory (".\") or provide the fully qualified path, such as:</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample26.cmd)]

    <span data-ttu-id="25206-320">有关脚本的详细信息，请使用`Get-Help`cmdlet。</span><span class="sxs-lookup"><span data-stu-id="25206-320">For more information about the script, use the `Get-Help` cmdlet.</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample27.cmd)]

    <span data-ttu-id="25206-321">可以使用`Detailed`， `Full`， `Parameters`，和`Examples`来筛选返回的帮助的 Get-help cmdlet 的参数。</span><span class="sxs-lookup"><span data-stu-id="25206-321">You can use the `Detailed`, `Full`, `Parameters`, and `Examples` parameters of the Get-Help cmdlet to filter the help that is returned.</span></span>

    <span data-ttu-id="25206-322">如果脚本失败或生成错误，例如"New-azurewebsite:首先，调用 Set-azuresubscription 和 Select-azuresubscription"可能未完成的 Azure PowerShell 配置。</span><span class="sxs-lookup"><span data-stu-id="25206-322">If the script fails or generates errors, such as "New-AzureWebsite : Call Set-AzureSubscription and Select-AzureSubscription first," you might not have completed the configuration of Azure PowerShell.</span></span>

    <span data-ttu-id="25206-323">在脚本完成后，可以使用 Azure 管理门户，查看已创建的资源，如中所示[使一切自动化](automate-everything.md)一章。</span><span class="sxs-lookup"><span data-stu-id="25206-323">After the script finishes, you can use the Azure Management Portal to see the resources that were created, as shown in the [Automate Everything](automate-everything.md) chapter.</span></span>
10. <span data-ttu-id="25206-324">若要将 fix It 项目部署到新的 Azure 环境中，使用*AzureWebsite.ps1*脚本。</span><span class="sxs-lookup"><span data-stu-id="25206-324">To deploy the FixIt project to the new Azure environment, use the *AzureWebsite.ps1* script.</span></span> <span data-ttu-id="25206-325">例如：</span><span class="sxs-lookup"><span data-stu-id="25206-325">For example:</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample28.cmd)]

    <span data-ttu-id="25206-326">完成部署后，浏览器打开与修复它在 Azure 中运行。</span><span class="sxs-lookup"><span data-stu-id="25206-326">When deployment is done, the browser opens with Fix It running in Azure.</span></span>

<a id="troubleshooting"></a>
## <a name="troubleshooting-the-windows-powershell-scripts"></a><span data-ttu-id="25206-327">Windows PowerShell 脚本故障排除</span><span class="sxs-lookup"><span data-stu-id="25206-327">Troubleshooting the Windows PowerShell scripts</span></span>

<span data-ttu-id="25206-328">运行这些脚本时遇到的最常见错误是与权限相关的。</span><span class="sxs-lookup"><span data-stu-id="25206-328">The most common errors encountered when running these scripts are related to permissions.</span></span> <span data-ttu-id="25206-329">请确保`Add-AzureAccount`和`Import-AzurePublishSettingsFile`已成功完成，并用于在同一 Azure 订阅。</span><span class="sxs-lookup"><span data-stu-id="25206-329">Make sure that `Add-AzureAccount` and `Import-AzurePublishSettingsFile` were successful and that you used them for the same Azure subscription.</span></span> <span data-ttu-id="25206-330">即使`Add-AzureAccount`已成功您可能需要重新运行。</span><span class="sxs-lookup"><span data-stu-id="25206-330">Even if `Add-AzureAccount` was successful you might have to run it again.</span></span> <span data-ttu-id="25206-331">通过添加权限`Add-AzureAccount`在 12 小时后过期。</span><span class="sxs-lookup"><span data-stu-id="25206-331">The permissions added by `Add-AzureAccount` expire in 12 hours.</span></span>

### <a name="object-reference-not-set-to-an-instance-of-an-object"></a><span data-ttu-id="25206-332">对象引用未设置为某个对象的实例。</span><span class="sxs-lookup"><span data-stu-id="25206-332">Object reference not set to an instance of an object.</span></span>

<span data-ttu-id="25206-333">如果该脚本返回错误，例如"对象引用未设置为对象的实例"这意味着 Windows PowerShell 找不到的对象 （这是 null 引用异常） 的过程，运行`Add-AzureAccount`cmdlet，然后重试该脚本。</span><span class="sxs-lookup"><span data-stu-id="25206-333">If the script returns errors, such as "Object reference not set to an instance of an object," which means that Windows PowerShell can't find an object to process (this is a null reference exception), run the `Add-AzureAccount` cmdlet and try the script again.</span></span>

[!code-console[Main](the-fix-it-sample-application/samples/sample29.cmd)]

### <a name="internalerror-the-server-encountered-an-internal-error"></a><span data-ttu-id="25206-334">InternalError:服务器遇到内部错误。</span><span class="sxs-lookup"><span data-stu-id="25206-334">InternalError: The server encountered an internal error.</span></span>

<span data-ttu-id="25206-335">`New-AzureWebsite`名称在 azurewebsites.net 域中不唯一时，cmdlet 将返回内部错误。</span><span class="sxs-lookup"><span data-stu-id="25206-335">The `New-AzureWebsite` cmdlet returns an internal error when the name is not unique in the azurewebsites.net domain.</span></span> <span data-ttu-id="25206-336">若要解决此错误，使用不同的值的名称，即 Name 参数中*新建 AzureWebsiteEnv.ps1*。</span><span class="sxs-lookup"><span data-stu-id="25206-336">To resolve the error, use a different value for the name, which is in the Name parameter of *New-AzureWebsiteEnv.ps1*.</span></span>

[!code-console[Main](the-fix-it-sample-application/samples/sample30.cmd)]

### <a name="restarting-the-script"></a><span data-ttu-id="25206-337">重新启动脚本</span><span class="sxs-lookup"><span data-stu-id="25206-337">Restarting the script</span></span>

<span data-ttu-id="25206-338">如果你需要重启*新建 AzureWebsiteEnv.ps1*脚本因为它不能打印的"脚本已完成"消息之前，你可能想要删除资源之前创建的脚本停止。</span><span class="sxs-lookup"><span data-stu-id="25206-338">If you need to restart the *New-AzureWebsiteEnv.ps1* script because it failed before it printed the "Script is complete" message, you might want to delete resources that the script created before it stopped.</span></span> <span data-ttu-id="25206-339">例如，如果该脚本创建 ContosoFixItDemo web 应用，并且具有相同名称重新运行该脚本，脚本将失败，因为名称正在使用中。</span><span class="sxs-lookup"><span data-stu-id="25206-339">For example, if the script already created the ContosoFixItDemo web app and you run the script again with the same name, the script will fail because the name is in use.</span></span>

<span data-ttu-id="25206-340">若要确定哪些资源停止之前创建的脚本，请使用以下 cmdlet:</span><span class="sxs-lookup"><span data-stu-id="25206-340">To determine which resources the script created before it stopped, use the following cmdlets:</span></span>

- `Get-AzureWebsite`
- `Get-AzureSqlDatabaseServer`
- <span data-ttu-id="25206-341">`Get-AzureSqlDatabase`：若要运行此 cmdlet，通过管道传递到的数据库服务器名称`Get-AzureSqlDatabase`:   `Get-AzureSqlDatabaseServer | Get-AzureSqlDatabase.`</span><span class="sxs-lookup"><span data-stu-id="25206-341">`Get-AzureSqlDatabase`: To run this cmdlet, pipe the database server name to `Get-AzureSqlDatabase`:   `Get-AzureSqlDatabaseServer | Get-AzureSqlDatabase.`</span></span>

<span data-ttu-id="25206-342">若要删除这些资源，请使用以下命令。</span><span class="sxs-lookup"><span data-stu-id="25206-342">To delete these resources, use the following commands.</span></span> <span data-ttu-id="25206-343">请注意，是否删除数据库服务器，则你会自动删除与服务器关联的数据库。</span><span class="sxs-lookup"><span data-stu-id="25206-343">Note that if you delete the database server, you automatically delete the databases associated with the server.</span></span>

- `Get-AzureWebsite -Name <WebsiteName> | Remove-AzureWebsite`
- `Get-AzureSqlDatabase -Name <DatabaseName> -ServerName <DatabaseServerName> | Remove-SqlAzureDatabase`
- `Get-AzureSqlDatabaseServer | Remove-AzureSqlDatabaseServer`

<a id="deployqueues"></a>
## <a name="how-to-deploy-the-app-with-queue-processing-to-azure-app-service-web-apps-and-an-azure-cloud-service"></a><span data-ttu-id="25206-344">如何使用队列处理到 Azure 应用服务 Web 应用和 Azure 云服务部署应用程序</span><span class="sxs-lookup"><span data-stu-id="25206-344">How to deploy the app with queue processing to Azure App Service Web Apps and an Azure Cloud Service</span></span>

<span data-ttu-id="25206-345">若要启用队列，请在 MyFixIt\Web.config 文件进行以下更改。</span><span class="sxs-lookup"><span data-stu-id="25206-345">To enable queues, make the following change in the MyFixIt\Web.config file.</span></span> <span data-ttu-id="25206-346">下`appSettings`，更改的值`UseQueues`为"true":</span><span class="sxs-lookup"><span data-stu-id="25206-346">Under `appSettings`, change the value of `UseQueues` to "true":</span></span>

[!code-xml[Main](the-fix-it-sample-application/samples/sample31.xml)]

<span data-ttu-id="25206-347">然后部署到 Azure 应用服务中的 web 应用的 MVC 应用程序，如所述[早期](#deploybase)。</span><span class="sxs-lookup"><span data-stu-id="25206-347">Then deploy the MVC application to an web app in Azure App Service, as described [earlier](#deploybase).</span></span>

<span data-ttu-id="25206-348">接下来，创建新的 Azure 云服务。</span><span class="sxs-lookup"><span data-stu-id="25206-348">Next, create a new Azure cloud service.</span></span> <span data-ttu-id="25206-349">修复其应用中包含的脚本不要创建或部署云服务，以便为此，必须使用 Azure 门户。</span><span class="sxs-lookup"><span data-stu-id="25206-349">The scripts included with the Fix It app do not create or deploy the cloud service, so you must use Azure portal for this.</span></span> <span data-ttu-id="25206-350">在门户中，单击**新建** -- **计算**–**云服务** -- **快速创建**，然后输入一个 URL和数据中心位置。</span><span class="sxs-lookup"><span data-stu-id="25206-350">In the portal, click **New** -- **Compute** – **Cloud Service** -- **Quick Create**, and then enter a URL and a data center location.</span></span> <span data-ttu-id="25206-351">使用同一数据中心部署 web 应用的位置。</span><span class="sxs-lookup"><span data-stu-id="25206-351">Use the same data center where you deployed the web app.</span></span>

![](the-fix-it-sample-application/_static/image1.png)

<span data-ttu-id="25206-352">部署云服务之前，你需要更新一些配置文件。</span><span class="sxs-lookup"><span data-stu-id="25206-352">Before you can deploy the cloud service, you need to update some of the configuration files.</span></span>

<span data-ttu-id="25206-353">在 MyFixIt.WorkerRole\app.config 下, `connectionStrings`，将的值为`appdb`使用 SQL 数据库的实际连接字符串的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="25206-353">In MyFixIt.WorkerRole\app.config, under `connectionStrings`, replace the value of the `appdb` connection string with the actual connection string for the SQL Database.</span></span> <span data-ttu-id="25206-354">可以从门户获取连接字符串。</span><span class="sxs-lookup"><span data-stu-id="25206-354">You can get the connection string from the portal.</span></span> <span data-ttu-id="25206-355">在门户中，单击**SQL 数据库** - **appdb** - **查看 SQL 数据库的 ADO.Net、 ODBC、 PHP 和 JDBC 连接字符串**。</span><span class="sxs-lookup"><span data-stu-id="25206-355">In the portal, click **SQL Databases** - **appdb** - **View SQL Database connection strings for ADO .Net, ODBC, PHP, and JDBC**.</span></span> <span data-ttu-id="25206-356">复制 ADO.NET 连接字符串并将值粘贴到 app.config 文件。</span><span class="sxs-lookup"><span data-stu-id="25206-356">Copy the ADO.NET connection string and paste the value into the app.config file.</span></span> <span data-ttu-id="25206-357">替换为"{你\_密码\_此处}"使用自己的数据库密码。</span><span class="sxs-lookup"><span data-stu-id="25206-357">Replace "{your\_password\_here}" with your database password.</span></span> <span data-ttu-id="25206-358">(假设您使用脚本来部署 MVC 应用程序，指定中的数据库密码`SqlDatabasePassword`脚本参数。)</span><span class="sxs-lookup"><span data-stu-id="25206-358">(Assuming you used the scripts to deploy the MVC app, you specified the database password in the `SqlDatabasePassword` script parameter.)</span></span>

<span data-ttu-id="25206-359">结果应如以下所示：</span><span class="sxs-lookup"><span data-stu-id="25206-359">The result should look like the following:</span></span>

[!code-xml[Main](the-fix-it-sample-application/samples/sample32.xml)]

<span data-ttu-id="25206-360">在同一个 MyFixIt.WorkerRole\app.config 文件中，在`appSettings`，两个占位符值替换为 Azure 存储帐户。</span><span class="sxs-lookup"><span data-stu-id="25206-360">In the same MyFixIt.WorkerRole\app.config file, under `appSettings`, replace the two placeholder values for the Azure storage account.</span></span>

[!code-xml[Main](the-fix-it-sample-application/samples/sample33.xml?highlight=2-3)]

<span data-ttu-id="25206-361">可以从门户获取的访问密钥。</span><span class="sxs-lookup"><span data-stu-id="25206-361">You can get the access key from the portal.</span></span> <span data-ttu-id="25206-362">请参阅[如何管理存储帐户](https://docs.microsoft.com/azure/storage/common/storage-create-storage-account)。</span><span class="sxs-lookup"><span data-stu-id="25206-362">See [How To Manage Storage Accounts](https://docs.microsoft.com/azure/storage/common/storage-create-storage-account).</span></span>

<span data-ttu-id="25206-363">在 MyFixItCloudService\ServiceConfiguration.Cloud.cscfg，将为 Azure 存储帐户中相同的两个占位符值。</span><span class="sxs-lookup"><span data-stu-id="25206-363">In MyFixItCloudService\ServiceConfiguration.Cloud.cscfg, replace the same two placeholders values for the Azure storage account.</span></span>

[!code-xml[Main](the-fix-it-sample-application/samples/sample34.xml?highlight=3)]

<span data-ttu-id="25206-364">现在已准备好部署云服务。</span><span class="sxs-lookup"><span data-stu-id="25206-364">Now you are ready to deploy the cloud service.</span></span> <span data-ttu-id="25206-365">在解决方案资源管理器，右键单击 MyFixItCloudService 项目并选择**发布**。</span><span class="sxs-lookup"><span data-stu-id="25206-365">In Solution Explore, right-click the MyFixItCloudService project and select **Publish**.</span></span> <span data-ttu-id="25206-366">有关详细信息，请参阅"[部署到 Azure 应用程序](https://www.windowsazure.com/develop/net/tutorials/multi-tier-web-site/2-download-and-run/#deployAz)"，这是中的第 2 部分[本教程](https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36)。</span><span class="sxs-lookup"><span data-stu-id="25206-366">For more information, see "[Deploy the Application to Azure](https://www.windowsazure.com/develop/net/tutorials/multi-tier-web-site/2-download-and-run/#deployAz)", which is in part 2 of [this tutorial](https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36).</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="25206-367">上一篇</span><span class="sxs-lookup"><span data-stu-id="25206-367">Previous</span></span>](more-patterns-and-guidance.md)

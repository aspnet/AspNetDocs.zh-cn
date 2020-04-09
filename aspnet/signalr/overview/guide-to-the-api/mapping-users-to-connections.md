---
uid: signalr/overview/guide-to-the-api/mapping-users-to-connections
title: 将信号R用户映射到连接 |微软文档
author: bradygaster
description: 本主题演示如何保留有关用户及其连接的信息。 帕特里克·弗莱彻帮助写了这个话题。 本主题中使用的软件版本...
ms.author: bradyg
ms.date: 12/30/2014
ms.assetid: f80c08b1-3f1f-432c-980c-c7b6edeb31b1
msc.legacyurl: /signalr/overview/guide-to-the-api/mapping-users-to-connections
msc.type: authoredcontent
ms.openlocfilehash: d55d40848e1e9d40570850c3552b225235c5e814
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675777"
---
# <a name="mapping-signalr-users-to-connections"></a><span data-ttu-id="703da-105">将 SignalR 用户映射到连接</span><span class="sxs-lookup"><span data-stu-id="703da-105">Mapping SignalR Users to Connections</span></span>

<span data-ttu-id="703da-106"> 作者 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="703da-106">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="703da-107">本主题演示如何保留有关用户及其连接的信息。</span><span class="sxs-lookup"><span data-stu-id="703da-107">This topic shows how to retain information about users and their connections.</span></span>
>
> <span data-ttu-id="703da-108">帕特里克·弗莱彻帮助写了这个话题。</span><span class="sxs-lookup"><span data-stu-id="703da-108">Patrick Fletcher helped write this topic.</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="703da-109">本主题中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="703da-109">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="703da-110">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="703da-110">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="703da-111">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="703da-111">.NET 4.5</span></span>
> - <span data-ttu-id="703da-112">信号R版本 2</span><span class="sxs-lookup"><span data-stu-id="703da-112">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="703da-113">本主题的早期版本</span><span class="sxs-lookup"><span data-stu-id="703da-113">Previous versions of this topic</span></span>
>
> <span data-ttu-id="703da-114">有关早期版本的 SignalR 的信息，请参阅[SignalR 旧版本](../older-versions/index.md)。</span><span class="sxs-lookup"><span data-stu-id="703da-114">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="703da-115">问题和评论</span><span class="sxs-lookup"><span data-stu-id="703da-115">Questions and comments</span></span>
>
> <span data-ttu-id="703da-116">请留下反馈，关于你喜欢本教程的方式，以及我们可以在页面底部的评论中改进什么。</span><span class="sxs-lookup"><span data-stu-id="703da-116">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="703da-117">如果您有与本教程没有直接关系的问题，您可以将它们发布到[ASP.NET SignalR 论坛](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com/)。</span><span class="sxs-lookup"><span data-stu-id="703da-117">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="introduction"></a><span data-ttu-id="703da-118">简介</span><span class="sxs-lookup"><span data-stu-id="703da-118">Introduction</span></span>

<span data-ttu-id="703da-119">连接到集线器的每个客户端传递一个唯一的连接 ID。您可以在中心上下文的属性中`Context.ConnectionId`检索此值。</span><span class="sxs-lookup"><span data-stu-id="703da-119">Each client connecting to a hub passes a unique connection id. You can retrieve this value in the `Context.ConnectionId` property of the hub context.</span></span> <span data-ttu-id="703da-120">如果应用程序需要将用户映射到连接 ID 并保留该映射，则可以使用以下方式之一：</span><span class="sxs-lookup"><span data-stu-id="703da-120">If your application needs to map a user to the connection id and persist that mapping, you can use one of the following:</span></span>

- [<span data-ttu-id="703da-121">用户 ID 提供程序（信号器 2）</span><span class="sxs-lookup"><span data-stu-id="703da-121">The User ID Provider (SignalR 2)</span></span>](#IUserIdProvider)
- <span data-ttu-id="703da-122">[内存中存储](#inmemory)，如字典</span><span class="sxs-lookup"><span data-stu-id="703da-122">[In-memory storage](#inmemory), such as a dictionary</span></span>
- [<span data-ttu-id="703da-123">每个用户的信号R组</span><span class="sxs-lookup"><span data-stu-id="703da-123">SignalR group for each user</span></span>](#groups)
- <span data-ttu-id="703da-124">[永久外部存储](#database)，如数据库表或 Azure 表存储</span><span class="sxs-lookup"><span data-stu-id="703da-124">[Permanent, external storage](#database), such as a database table or Azure table storage</span></span>

<span data-ttu-id="703da-125">本主题中显示了每个实现。</span><span class="sxs-lookup"><span data-stu-id="703da-125">Each of these implementations is shown in this topic.</span></span> <span data-ttu-id="703da-126">使用 类`OnConnected``OnDisconnected`的`OnReconnected`和 方法`Hub`来跟踪用户连接状态。</span><span class="sxs-lookup"><span data-stu-id="703da-126">You use the `OnConnected`, `OnDisconnected`, and `OnReconnected` methods of the `Hub` class to track the user connection status.</span></span>

<span data-ttu-id="703da-127">最适合您的应用程序的方法取决于：</span><span class="sxs-lookup"><span data-stu-id="703da-127">The best approach for your application depends on:</span></span>

- <span data-ttu-id="703da-128">托管应用程序的 Web 服务器数。</span><span class="sxs-lookup"><span data-stu-id="703da-128">The number of web servers hosting your application.</span></span>
- <span data-ttu-id="703da-129">是否需要获取当前连接的用户的列表。</span><span class="sxs-lookup"><span data-stu-id="703da-129">Whether you need to get a list of the currently connected users.</span></span>
- <span data-ttu-id="703da-130">在应用程序或服务器重新启动时是否需要保留组和用户信息。</span><span class="sxs-lookup"><span data-stu-id="703da-130">Whether you need to persist group and user information when the application or server restarts.</span></span>
- <span data-ttu-id="703da-131">调用外部服务器的延迟是否是一个问题。</span><span class="sxs-lookup"><span data-stu-id="703da-131">Whether the latency of calling an external server is an issue.</span></span>

<span data-ttu-id="703da-132">下表显示了哪种方法适用于这些注意事项。</span><span class="sxs-lookup"><span data-stu-id="703da-132">The following table shows which approach works for these considerations.</span></span>

|  | <span data-ttu-id="703da-133">多台服务器</span><span class="sxs-lookup"><span data-stu-id="703da-133">More than one server</span></span> | <span data-ttu-id="703da-134">获取当前连接用户的列表</span><span class="sxs-lookup"><span data-stu-id="703da-134">Get list of currently connected users</span></span> | <span data-ttu-id="703da-135">重新启动后保留信息</span><span class="sxs-lookup"><span data-stu-id="703da-135">Persist information after restarts</span></span> | <span data-ttu-id="703da-136">最佳性能</span><span class="sxs-lookup"><span data-stu-id="703da-136">Optimal performance</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="703da-137">用户 ID 提供程序</span><span class="sxs-lookup"><span data-stu-id="703da-137">UserID Provider</span></span> | ![](mapping-users-to-connections/_static/image1.png) |  |  | ![](mapping-users-to-connections/_static/image2.png) |
| <span data-ttu-id="703da-138">内存中</span><span class="sxs-lookup"><span data-stu-id="703da-138">In-memory</span></span> |  | ![](mapping-users-to-connections/_static/image3.png) |  | ![](mapping-users-to-connections/_static/image4.png) |
| <span data-ttu-id="703da-139">单用户组</span><span class="sxs-lookup"><span data-stu-id="703da-139">Single-user groups</span></span> | ![](mapping-users-to-connections/_static/image5.png) |  |  | ![](mapping-users-to-connections/_static/image6.png) |
| <span data-ttu-id="703da-140">永久外部</span><span class="sxs-lookup"><span data-stu-id="703da-140">Permanent, external</span></span> | ![](mapping-users-to-connections/_static/image7.png) | ![](mapping-users-to-connections/_static/image8.png) | ![](mapping-users-to-connections/_static/image9.png) |  |

<a id="IUserIdProvider"></a>

## <a name="iuserid-provider"></a><span data-ttu-id="703da-141">IUserID 提供商</span><span class="sxs-lookup"><span data-stu-id="703da-141">IUserID provider</span></span>

<span data-ttu-id="703da-142">此功能允许用户通过新接口 IUserIdProvider 指定用户 Id 基于 IRequest 的内容。</span><span class="sxs-lookup"><span data-stu-id="703da-142">This feature allows users to specify what the userId is based on an IRequest via a new interface IUserIdProvider.</span></span>

<span data-ttu-id="703da-143">**IUserId 提供商**</span><span class="sxs-lookup"><span data-stu-id="703da-143">**The IUserIdProvider**</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample1.cs)]

<span data-ttu-id="703da-144">默认情况下，将有一个使用用户`IPrincipal.Identity.Name`作为用户名的实现。</span><span class="sxs-lookup"><span data-stu-id="703da-144">By default, there will be an implementation that uses the user's `IPrincipal.Identity.Name` as the user name.</span></span> <span data-ttu-id="703da-145">要更改此项，请在应用程序启动`IUserIdProvider`时向全局主机注册实现：</span><span class="sxs-lookup"><span data-stu-id="703da-145">To change this, register your implementation of `IUserIdProvider` with the global host when your application starts:</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample2.cs)]

<span data-ttu-id="703da-146">从集线器中，您可以通过以下 API 向这些用户发送消息：</span><span class="sxs-lookup"><span data-stu-id="703da-146">From within a hub, you'll be able to send messages to these users via the following API:</span></span>

<span data-ttu-id="703da-147">**向特定用户发送消息**</span><span class="sxs-lookup"><span data-stu-id="703da-147">**Sending a message to a specific user**</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample3.cs?highlight=5)]

<a id="inmemory"></a>

## <a name="in-memory-storage"></a><span data-ttu-id="703da-148">内存中存储</span><span class="sxs-lookup"><span data-stu-id="703da-148">In-memory storage</span></span>

<span data-ttu-id="703da-149">以下示例演示如何在存储在内存中的字典中保留连接和用户信息。</span><span class="sxs-lookup"><span data-stu-id="703da-149">The following examples show how to retain connection and user information in a dictionary that is stored in memory.</span></span> <span data-ttu-id="703da-150">字典使用 存储`HashSet`连接 ID。在任何时候，用户都可以与 SignalR 应用程序建立多个连接。</span><span class="sxs-lookup"><span data-stu-id="703da-150">The dictionary uses a `HashSet` to store the connection id. At any time a user could have more than one connection to the SignalR application.</span></span> <span data-ttu-id="703da-151">例如，通过多个设备或多个浏览器选项卡连接的用户将具有多个连接 ID。</span><span class="sxs-lookup"><span data-stu-id="703da-151">For example, a user who is connected through multiple devices or more than one browser tab would have more than one connection id.</span></span>

<span data-ttu-id="703da-152">如果应用程序关闭，所有信息都将丢失，但在用户重新建立其连接时将重新填充该信息。</span><span class="sxs-lookup"><span data-stu-id="703da-152">If the application shuts down, all of the information is lost, but it will be re-populated as the users re-establish their connections.</span></span> <span data-ttu-id="703da-153">如果环境包含多个 Web 服务器，则内存中存储不起作用，因为每台服务器都将具有单独的连接集合。</span><span class="sxs-lookup"><span data-stu-id="703da-153">In-memory storage does not work if your environment includes more than one web server because each server would have a separate collection of connections.</span></span>

<span data-ttu-id="703da-154">第一个示例显示了管理用户映射到连接的类。</span><span class="sxs-lookup"><span data-stu-id="703da-154">The first example shows a class that manages the mapping of users to connections.</span></span> <span data-ttu-id="703da-155">哈希集的键将是用户名。</span><span class="sxs-lookup"><span data-stu-id="703da-155">The key for the HashSet will be the user's name.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample4.cs)]

<span data-ttu-id="703da-156">下一个示例演示如何使用中心的连接映射类。</span><span class="sxs-lookup"><span data-stu-id="703da-156">The next example shows how to use the connection mapping class from a hub.</span></span> <span data-ttu-id="703da-157">类的实例存储在变量名称`_connections`中。</span><span class="sxs-lookup"><span data-stu-id="703da-157">The instance of the class is stored in a variable name `_connections`.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample5.cs)]

<a id="groups"></a>

## <a name="single-user-groups"></a><span data-ttu-id="703da-158">单用户组</span><span class="sxs-lookup"><span data-stu-id="703da-158">Single-user groups</span></span>

<span data-ttu-id="703da-159">您可以为每个用户创建一个组，然后在您只想联系该用户时向该组发送消息。</span><span class="sxs-lookup"><span data-stu-id="703da-159">You can create a group for each user, and then send a message to that group when you want to reach only that user.</span></span> <span data-ttu-id="703da-160">每个组的名称是用户的名称。</span><span class="sxs-lookup"><span data-stu-id="703da-160">The name of each group is the name of the user.</span></span> <span data-ttu-id="703da-161">如果用户有多个连接，则每个连接 ID 将添加到用户的组中。</span><span class="sxs-lookup"><span data-stu-id="703da-161">If a user has more than one connection, each connection id is added to the user's group.</span></span>

<span data-ttu-id="703da-162">当用户断开连接时，不应手动从组中删除用户。</span><span class="sxs-lookup"><span data-stu-id="703da-162">You should not manually remove the user from the group when the user disconnects.</span></span> <span data-ttu-id="703da-163">此操作由 SignalR 框架自动执行。</span><span class="sxs-lookup"><span data-stu-id="703da-163">This action is automatically performed by the SignalR framework.</span></span>

<span data-ttu-id="703da-164">下面的示例演示如何实现单用户组。</span><span class="sxs-lookup"><span data-stu-id="703da-164">The following example shows how to implement single-user groups.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample6.cs)]

<a id="database"></a>

## <a name="permanent-external-storage"></a><span data-ttu-id="703da-165">永久外部存储</span><span class="sxs-lookup"><span data-stu-id="703da-165">Permanent, external storage</span></span>

<span data-ttu-id="703da-166">本主题演示如何使用数据库或 Azure 表存储来存储连接信息。</span><span class="sxs-lookup"><span data-stu-id="703da-166">This topic shows how to use either a database or Azure table storage for storing connection information.</span></span> <span data-ttu-id="703da-167">当您有多个 Web 服务器时，此方法有效，因为每个 Web 服务器都可以与同一数据存储库进行交互。</span><span class="sxs-lookup"><span data-stu-id="703da-167">This approach works when you have multiple web servers because each web server can interact with the same data repository.</span></span> <span data-ttu-id="703da-168">如果 Web 服务器停止工作或应用程序重新启动，则不`OnDisconnected`调用该方法。</span><span class="sxs-lookup"><span data-stu-id="703da-168">If your web servers stop working or the application restarts, the `OnDisconnected` method is not called.</span></span> <span data-ttu-id="703da-169">因此，数据存储库可能具有不再有效的连接 ID 记录。</span><span class="sxs-lookup"><span data-stu-id="703da-169">Therefore, it is possible that your data repository will have records for connection ids that are no longer valid.</span></span> <span data-ttu-id="703da-170">要清理这些孤立记录，您可能希望使在与您的应用程序相关的时间范围之外创建的任何连接无效。</span><span class="sxs-lookup"><span data-stu-id="703da-170">To clean up these orphaned records, you may wish to invalidate any connection that was created outside of a timeframe that is relevant to your application.</span></span> <span data-ttu-id="703da-171">本节中的示例包括用于跟踪创建连接时间的值，但不显示如何清理旧记录，因为您可能希望作为后台进程执行此操作。</span><span class="sxs-lookup"><span data-stu-id="703da-171">The examples in this section include a value for tracking when the connection was created, but do not show how to clean up old records because you may want to do that as background process.</span></span>

### <a name="database"></a><span data-ttu-id="703da-172">数据库</span><span class="sxs-lookup"><span data-stu-id="703da-172">Database</span></span>

<span data-ttu-id="703da-173">以下示例演示如何在数据库中保留连接和用户信息。</span><span class="sxs-lookup"><span data-stu-id="703da-173">The following examples show how to retain connection and user information in a database.</span></span> <span data-ttu-id="703da-174">您可以使用任何数据访问技术;但是，下面的示例演示如何使用实体框架定义模型。</span><span class="sxs-lookup"><span data-stu-id="703da-174">You can use any data access technology; however, the example below shows how to define models using Entity Framework.</span></span> <span data-ttu-id="703da-175">这些实体模型对应于数据库表和字段。</span><span class="sxs-lookup"><span data-stu-id="703da-175">These entity models correspond to database tables and fields.</span></span> <span data-ttu-id="703da-176">您的数据结构可能因应用程序的要求而有很大差异。</span><span class="sxs-lookup"><span data-stu-id="703da-176">Your data structure could vary considerably depending on the requirements of your application.</span></span>

<span data-ttu-id="703da-177">第一个示例演示如何定义可以与许多连接实体关联的用户实体。</span><span class="sxs-lookup"><span data-stu-id="703da-177">The first example shows how to define a user entity that can be associated with many connection entities.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample7.cs)]

<span data-ttu-id="703da-178">然后，从集线器，您可以使用下面显示的代码跟踪每个连接的状态。</span><span class="sxs-lookup"><span data-stu-id="703da-178">Then, from the hub, you can track the state of each connection with the code shown below.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample8.cs)]

<a id="azure"></a>
### <a name="azure-table-storage"></a><span data-ttu-id="703da-179">Azure 表存储</span><span class="sxs-lookup"><span data-stu-id="703da-179">Azure table storage</span></span>

<span data-ttu-id="703da-180">以下 Azure 表存储示例与数据库示例类似。</span><span class="sxs-lookup"><span data-stu-id="703da-180">The following Azure table storage example is similar to the database example.</span></span> <span data-ttu-id="703da-181">它不包括开始使用 Azure 表存储服务所需的所有信息。</span><span class="sxs-lookup"><span data-stu-id="703da-181">It does not include all of the information that you would need to get started with Azure Table Storage Service.</span></span> <span data-ttu-id="703da-182">有关详细信息，请参阅[如何使用 .NET 中的表存储](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/)。</span><span class="sxs-lookup"><span data-stu-id="703da-182">For information, see [How to use Table storage from .NET](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/).</span></span>

<span data-ttu-id="703da-183">下面的示例显示了用于存储连接信息的表实体。</span><span class="sxs-lookup"><span data-stu-id="703da-183">The following example shows a table entity for storing connection information.</span></span> <span data-ttu-id="703da-184">它按用户名对数据进行分区，并通过连接 ID 标识每个实体，以便用户可以随时具有多个连接。</span><span class="sxs-lookup"><span data-stu-id="703da-184">It partitions the data by user name, and identifies each entity by the connection id, so a user can have multiple connections at any time.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample9.cs)]

<span data-ttu-id="703da-185">在集线器中，您可以跟踪每个用户的连接状态。</span><span class="sxs-lookup"><span data-stu-id="703da-185">In the hub, you track the status of each user's connection.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample10.cs)]

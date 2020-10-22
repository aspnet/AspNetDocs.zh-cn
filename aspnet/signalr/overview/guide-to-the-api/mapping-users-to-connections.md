---
uid: signalr/overview/guide-to-the-api/mapping-users-to-connections
title: 将 SignalR 用户映射到连接 |Microsoft Docs
author: bradygaster
description: 本主题说明如何保留有关用户及其连接的信息。 Fletcher 帮助编写本主题。 本主题中使用的软件版本 .。。
ms.author: bradyg
ms.date: 12/30/2014
ms.assetid: f80c08b1-3f1f-432c-980c-c7b6edeb31b1
msc.legacyurl: /signalr/overview/guide-to-the-api/mapping-users-to-connections
msc.type: authoredcontent
ms.openlocfilehash: d55d40848e1e9d40570850c3552b225235c5e814
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345422"
---
# <a name="mapping-signalr-users-to-connections"></a><span data-ttu-id="77c09-105">将 SignalR 用户映射到连接</span><span class="sxs-lookup"><span data-stu-id="77c09-105">Mapping SignalR Users to Connections</span></span>

<span data-ttu-id="77c09-106"> 作者 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="77c09-106">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="77c09-107">本主题说明如何保留有关用户及其连接的信息。</span><span class="sxs-lookup"><span data-stu-id="77c09-107">This topic shows how to retain information about users and their connections.</span></span>
>
> <span data-ttu-id="77c09-108">Fletcher 帮助编写本主题。</span><span class="sxs-lookup"><span data-stu-id="77c09-108">Patrick Fletcher helped write this topic.</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="77c09-109">本主题中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="77c09-109">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="77c09-110">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="77c09-110">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="77c09-111">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="77c09-111">.NET 4.5</span></span>
> - <span data-ttu-id="77c09-112">SignalR 版本2</span><span class="sxs-lookup"><span data-stu-id="77c09-112">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="77c09-113">本主题的早期版本</span><span class="sxs-lookup"><span data-stu-id="77c09-113">Previous versions of this topic</span></span>
>
> <span data-ttu-id="77c09-114">有关早期版本的 SignalR 的信息，请参阅 [SignalR 旧版本](../older-versions/index.md)。</span><span class="sxs-lookup"><span data-stu-id="77c09-114">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="77c09-115">问题和注释</span><span class="sxs-lookup"><span data-stu-id="77c09-115">Questions and comments</span></span>
>
> <span data-ttu-id="77c09-116">请提供有关你喜欢本教程的方式的反馈，并在页面底部的评论中留下反馈。</span><span class="sxs-lookup"><span data-stu-id="77c09-116">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="77c09-117">如果你有与本教程不直接相关的问题，则可以将其发布到 [ASP.NET SignalR 论坛](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 或 [StackOverflow.com](http://stackoverflow.com/)。</span><span class="sxs-lookup"><span data-stu-id="77c09-117">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="introduction"></a><span data-ttu-id="77c09-118">简介</span><span class="sxs-lookup"><span data-stu-id="77c09-118">Introduction</span></span>

<span data-ttu-id="77c09-119">连接到中心的每个客户端传递唯一的连接 id。可以在中心上下文的属性中检索此值 `Context.ConnectionId` 。</span><span class="sxs-lookup"><span data-stu-id="77c09-119">Each client connecting to a hub passes a unique connection id. You can retrieve this value in the `Context.ConnectionId` property of the hub context.</span></span> <span data-ttu-id="77c09-120">如果你的应用程序需要将用户映射到连接 id 并保留该映射，则可以使用以下项之一：</span><span class="sxs-lookup"><span data-stu-id="77c09-120">If your application needs to map a user to the connection id and persist that mapping, you can use one of the following:</span></span>

- [<span data-ttu-id="77c09-121">用户 ID 提供程序 (SignalR 2) </span><span class="sxs-lookup"><span data-stu-id="77c09-121">The User ID Provider (SignalR 2)</span></span>](#IUserIdProvider)
- <span data-ttu-id="77c09-122">[内存中存储](#inmemory)，如字典</span><span class="sxs-lookup"><span data-stu-id="77c09-122">[In-memory storage](#inmemory), such as a dictionary</span></span>
- [<span data-ttu-id="77c09-123">每个用户的 SignalR 组</span><span class="sxs-lookup"><span data-stu-id="77c09-123">SignalR group for each user</span></span>](#groups)
- <span data-ttu-id="77c09-124">[永久、外部存储](#database)（如数据库表或 Azure 表存储）</span><span class="sxs-lookup"><span data-stu-id="77c09-124">[Permanent, external storage](#database), such as a database table or Azure table storage</span></span>

<span data-ttu-id="77c09-125">本主题中显示了每个实现。</span><span class="sxs-lookup"><span data-stu-id="77c09-125">Each of these implementations is shown in this topic.</span></span> <span data-ttu-id="77c09-126">使用类的 `OnConnected` 、 `OnDisconnected` 和 `OnReconnected` 方法 `Hub` 跟踪用户连接状态。</span><span class="sxs-lookup"><span data-stu-id="77c09-126">You use the `OnConnected`, `OnDisconnected`, and `OnReconnected` methods of the `Hub` class to track the user connection status.</span></span>

<span data-ttu-id="77c09-127">应用程序的最佳方法取决于：</span><span class="sxs-lookup"><span data-stu-id="77c09-127">The best approach for your application depends on:</span></span>

- <span data-ttu-id="77c09-128">承载应用程序的 web 服务器的数量。</span><span class="sxs-lookup"><span data-stu-id="77c09-128">The number of web servers hosting your application.</span></span>
- <span data-ttu-id="77c09-129">是否需要获取当前连接的用户的列表。</span><span class="sxs-lookup"><span data-stu-id="77c09-129">Whether you need to get a list of the currently connected users.</span></span>
- <span data-ttu-id="77c09-130">应用程序或服务器重新启动时是否需要保留组和用户信息。</span><span class="sxs-lookup"><span data-stu-id="77c09-130">Whether you need to persist group and user information when the application or server restarts.</span></span>
- <span data-ttu-id="77c09-131">调用外部服务器的延迟是否存在问题。</span><span class="sxs-lookup"><span data-stu-id="77c09-131">Whether the latency of calling an external server is an issue.</span></span>

<span data-ttu-id="77c09-132">下表显示了适用于这些注意事项的方法。</span><span class="sxs-lookup"><span data-stu-id="77c09-132">The following table shows which approach works for these considerations.</span></span>

|  | <span data-ttu-id="77c09-133">多个服务器</span><span class="sxs-lookup"><span data-stu-id="77c09-133">More than one server</span></span> | <span data-ttu-id="77c09-134">获取当前连接的用户的列表</span><span class="sxs-lookup"><span data-stu-id="77c09-134">Get list of currently connected users</span></span> | <span data-ttu-id="77c09-135">重新启动后保留信息</span><span class="sxs-lookup"><span data-stu-id="77c09-135">Persist information after restarts</span></span> | <span data-ttu-id="77c09-136">最佳性能</span><span class="sxs-lookup"><span data-stu-id="77c09-136">Optimal performance</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="77c09-137">UserID 提供程序</span><span class="sxs-lookup"><span data-stu-id="77c09-137">UserID Provider</span></span> | ![](mapping-users-to-connections/_static/image1.png) |  |  | ![](mapping-users-to-connections/_static/image2.png) |
| <span data-ttu-id="77c09-138">内存中</span><span class="sxs-lookup"><span data-stu-id="77c09-138">In-memory</span></span> |  | ![](mapping-users-to-connections/_static/image3.png) |  | ![](mapping-users-to-connections/_static/image4.png) |
| <span data-ttu-id="77c09-139">单用户组</span><span class="sxs-lookup"><span data-stu-id="77c09-139">Single-user groups</span></span> | ![](mapping-users-to-connections/_static/image5.png) |  |  | ![](mapping-users-to-connections/_static/image6.png) |
| <span data-ttu-id="77c09-140">永久、外部</span><span class="sxs-lookup"><span data-stu-id="77c09-140">Permanent, external</span></span> | ![](mapping-users-to-connections/_static/image7.png) | ![](mapping-users-to-connections/_static/image8.png) | ![](mapping-users-to-connections/_static/image9.png) |  |

<a id="IUserIdProvider"></a>

## <a name="iuserid-provider"></a><span data-ttu-id="77c09-141">IUserID 提供程序</span><span class="sxs-lookup"><span data-stu-id="77c09-141">IUserID provider</span></span>

<span data-ttu-id="77c09-142">此功能允许用户通过新的接口 IUserIdProvider 指定用户 Id 基于 IRequest 的内容。</span><span class="sxs-lookup"><span data-stu-id="77c09-142">This feature allows users to specify what the userId is based on an IRequest via a new interface IUserIdProvider.</span></span>

<span data-ttu-id="77c09-143">**IUserIdProvider**</span><span class="sxs-lookup"><span data-stu-id="77c09-143">**The IUserIdProvider**</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample1.cs)]

<span data-ttu-id="77c09-144">默认情况下，将有一个实现，该实现使用用户的 `IPrincipal.Identity.Name` 作为用户名。</span><span class="sxs-lookup"><span data-stu-id="77c09-144">By default, there will be an implementation that uses the user's `IPrincipal.Identity.Name` as the user name.</span></span> <span data-ttu-id="77c09-145">若要更改此操作，请在应用程序启动时，将的实现注册到 `IUserIdProvider` 全局主机：</span><span class="sxs-lookup"><span data-stu-id="77c09-145">To change this, register your implementation of `IUserIdProvider` with the global host when your application starts:</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample2.cs)]

<span data-ttu-id="77c09-146">从中心内，你将能够通过以下 API 向这些用户发送消息：</span><span class="sxs-lookup"><span data-stu-id="77c09-146">From within a hub, you'll be able to send messages to these users via the following API:</span></span>

<span data-ttu-id="77c09-147">**向特定用户发送消息**</span><span class="sxs-lookup"><span data-stu-id="77c09-147">**Sending a message to a specific user**</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample3.cs?highlight=5)]

<a id="inmemory"></a>

## <a name="in-memory-storage"></a><span data-ttu-id="77c09-148">内存中存储</span><span class="sxs-lookup"><span data-stu-id="77c09-148">In-memory storage</span></span>

<span data-ttu-id="77c09-149">下面的示例演示如何在存储在内存中的字典中保留连接和用户信息。</span><span class="sxs-lookup"><span data-stu-id="77c09-149">The following examples show how to retain connection and user information in a dictionary that is stored in memory.</span></span> <span data-ttu-id="77c09-150">字典使用 `HashSet` 来存储连接 id。用户随时可以与 SignalR 应用程序建立多个连接。</span><span class="sxs-lookup"><span data-stu-id="77c09-150">The dictionary uses a `HashSet` to store the connection id. At any time a user could have more than one connection to the SignalR application.</span></span> <span data-ttu-id="77c09-151">例如，通过多个设备或多个浏览器选项卡连接的用户将拥有多个连接 id。</span><span class="sxs-lookup"><span data-stu-id="77c09-151">For example, a user who is connected through multiple devices or more than one browser tab would have more than one connection id.</span></span>

<span data-ttu-id="77c09-152">如果应用程序关闭，所有信息都将丢失，但会在用户重新建立连接时重新填充。</span><span class="sxs-lookup"><span data-stu-id="77c09-152">If the application shuts down, all of the information is lost, but it will be re-populated as the users re-establish their connections.</span></span> <span data-ttu-id="77c09-153">如果你的环境包含多个 web 服务器，则内存中存储不起作用，因为每个服务器都有一个单独的连接集合。</span><span class="sxs-lookup"><span data-stu-id="77c09-153">In-memory storage does not work if your environment includes more than one web server because each server would have a separate collection of connections.</span></span>

<span data-ttu-id="77c09-154">第一个示例演示一个类，该类管理用户到连接的映射。</span><span class="sxs-lookup"><span data-stu-id="77c09-154">The first example shows a class that manages the mapping of users to connections.</span></span> <span data-ttu-id="77c09-155">HashSet 的密钥将是用户的名称。</span><span class="sxs-lookup"><span data-stu-id="77c09-155">The key for the HashSet will be the user's name.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample4.cs)]

<span data-ttu-id="77c09-156">下一个示例演示如何从集线器使用连接映射类。</span><span class="sxs-lookup"><span data-stu-id="77c09-156">The next example shows how to use the connection mapping class from a hub.</span></span> <span data-ttu-id="77c09-157">类的实例存储在变量名称中 `_connections` 。</span><span class="sxs-lookup"><span data-stu-id="77c09-157">The instance of the class is stored in a variable name `_connections`.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample5.cs)]

<a id="groups"></a>

## <a name="single-user-groups"></a><span data-ttu-id="77c09-158">单用户组</span><span class="sxs-lookup"><span data-stu-id="77c09-158">Single-user groups</span></span>

<span data-ttu-id="77c09-159">你可以为每个用户创建一个组，然后在你只需要访问该用户时向该组发送一条消息。</span><span class="sxs-lookup"><span data-stu-id="77c09-159">You can create a group for each user, and then send a message to that group when you want to reach only that user.</span></span> <span data-ttu-id="77c09-160">每个组的名称是用户的名称。</span><span class="sxs-lookup"><span data-stu-id="77c09-160">The name of each group is the name of the user.</span></span> <span data-ttu-id="77c09-161">如果用户有多个连接，则会将每个连接 id 添加到用户的组中。</span><span class="sxs-lookup"><span data-stu-id="77c09-161">If a user has more than one connection, each connection id is added to the user's group.</span></span>

<span data-ttu-id="77c09-162">用户断开连接时，不应手动将用户从组中删除。</span><span class="sxs-lookup"><span data-stu-id="77c09-162">You should not manually remove the user from the group when the user disconnects.</span></span> <span data-ttu-id="77c09-163">此操作由 SignalR 框架自动执行。</span><span class="sxs-lookup"><span data-stu-id="77c09-163">This action is automatically performed by the SignalR framework.</span></span>

<span data-ttu-id="77c09-164">下面的示例演示如何实现单用户组。</span><span class="sxs-lookup"><span data-stu-id="77c09-164">The following example shows how to implement single-user groups.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample6.cs)]

<a id="database"></a>

## <a name="permanent-external-storage"></a><span data-ttu-id="77c09-165">永久、外部存储</span><span class="sxs-lookup"><span data-stu-id="77c09-165">Permanent, external storage</span></span>

<span data-ttu-id="77c09-166">本主题说明如何使用数据库或 Azure 表存储来存储连接信息。</span><span class="sxs-lookup"><span data-stu-id="77c09-166">This topic shows how to use either a database or Azure table storage for storing connection information.</span></span> <span data-ttu-id="77c09-167">当你有多个 web 服务器时，这种方法可正常工作，因为每个 web 服务器可以与相同的数据存储库交互。</span><span class="sxs-lookup"><span data-stu-id="77c09-167">This approach works when you have multiple web servers because each web server can interact with the same data repository.</span></span> <span data-ttu-id="77c09-168">如果 web 服务器停止工作或重新启动应用程序，则 `OnDisconnected` 不会调用方法。</span><span class="sxs-lookup"><span data-stu-id="77c09-168">If your web servers stop working or the application restarts, the `OnDisconnected` method is not called.</span></span> <span data-ttu-id="77c09-169">因此，您的数据存储库可能会记录不再有效的连接 id。</span><span class="sxs-lookup"><span data-stu-id="77c09-169">Therefore, it is possible that your data repository will have records for connection ids that are no longer valid.</span></span> <span data-ttu-id="77c09-170">若要清理这些孤立记录，你可能希望使在与你的应用程序相关的时间范围之外创建的任何连接无效。</span><span class="sxs-lookup"><span data-stu-id="77c09-170">To clean up these orphaned records, you may wish to invalidate any connection that was created outside of a timeframe that is relevant to your application.</span></span> <span data-ttu-id="77c09-171">本节中的示例包含一个用于在创建连接时进行跟踪的值，但不显示如何清理旧记录，因为你可能想要将其作为后台进程执行。</span><span class="sxs-lookup"><span data-stu-id="77c09-171">The examples in this section include a value for tracking when the connection was created, but do not show how to clean up old records because you may want to do that as background process.</span></span>

### <a name="database"></a><span data-ttu-id="77c09-172">数据库</span><span class="sxs-lookup"><span data-stu-id="77c09-172">Database</span></span>

<span data-ttu-id="77c09-173">下面的示例演示如何在数据库中保留连接和用户信息。</span><span class="sxs-lookup"><span data-stu-id="77c09-173">The following examples show how to retain connection and user information in a database.</span></span> <span data-ttu-id="77c09-174">您可以使用任何数据访问技术;但下面的示例演示如何使用实体框架定义模型。</span><span class="sxs-lookup"><span data-stu-id="77c09-174">You can use any data access technology; however, the example below shows how to define models using Entity Framework.</span></span> <span data-ttu-id="77c09-175">这些实体模型对应于数据库表和字段。</span><span class="sxs-lookup"><span data-stu-id="77c09-175">These entity models correspond to database tables and fields.</span></span> <span data-ttu-id="77c09-176">根据应用程序的要求，数据结构可能会有很大的差别。</span><span class="sxs-lookup"><span data-stu-id="77c09-176">Your data structure could vary considerably depending on the requirements of your application.</span></span>

<span data-ttu-id="77c09-177">第一个示例演示如何定义可以与多个连接实体相关联的用户实体。</span><span class="sxs-lookup"><span data-stu-id="77c09-177">The first example shows how to define a user entity that can be associated with many connection entities.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample7.cs)]

<span data-ttu-id="77c09-178">然后，可以从中心跟踪每个连接的状态，如下所示。</span><span class="sxs-lookup"><span data-stu-id="77c09-178">Then, from the hub, you can track the state of each connection with the code shown below.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample8.cs)]

<a id="azure"></a>
### <a name="azure-table-storage"></a><span data-ttu-id="77c09-179">Azure 表存储</span><span class="sxs-lookup"><span data-stu-id="77c09-179">Azure table storage</span></span>

<span data-ttu-id="77c09-180">以下 Azure 表存储示例类似于数据库示例。</span><span class="sxs-lookup"><span data-stu-id="77c09-180">The following Azure table storage example is similar to the database example.</span></span> <span data-ttu-id="77c09-181">它不包含开始 Azure 表存储服务所需的所有信息。</span><span class="sxs-lookup"><span data-stu-id="77c09-181">It does not include all of the information that you would need to get started with Azure Table Storage Service.</span></span> <span data-ttu-id="77c09-182">有关信息，请参阅 [如何通过 .net 使用表存储](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/)。</span><span class="sxs-lookup"><span data-stu-id="77c09-182">For information, see [How to use Table storage from .NET](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/).</span></span>

<span data-ttu-id="77c09-183">下面的示例显示了用于存储连接信息的表实体。</span><span class="sxs-lookup"><span data-stu-id="77c09-183">The following example shows a table entity for storing connection information.</span></span> <span data-ttu-id="77c09-184">它按用户名对数据进行分区，并通过连接 id 识别每个实体，因此用户可随时拥有多个连接。</span><span class="sxs-lookup"><span data-stu-id="77c09-184">It partitions the data by user name, and identifies each entity by the connection id, so a user can have multiple connections at any time.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample9.cs)]

<span data-ttu-id="77c09-185">在中心，你可以跟踪每个用户的连接的状态。</span><span class="sxs-lookup"><span data-stu-id="77c09-185">In the hub, you track the status of each user's connection.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample10.cs)]

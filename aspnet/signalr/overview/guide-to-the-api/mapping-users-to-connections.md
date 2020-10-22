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
# <a name="mapping-signalr-users-to-connections"></a>将 SignalR 用户映射到连接

 作者 [Tom FitzMacken](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 本主题说明如何保留有关用户及其连接的信息。
>
> Fletcher 帮助编写本主题。
>
> ## <a name="software-versions-used-in-this-topic"></a>本主题中使用的软件版本
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - .NET 4.5
> - SignalR 版本2
>
>
>
> ## <a name="previous-versions-of-this-topic"></a>本主题的早期版本
>
> 有关早期版本的 SignalR 的信息，请参阅 [SignalR 旧版本](../older-versions/index.md)。
>
> ## <a name="questions-and-comments"></a>问题和注释
>
> 请提供有关你喜欢本教程的方式的反馈，并在页面底部的评论中留下反馈。 如果你有与本教程不直接相关的问题，则可以将其发布到 [ASP.NET SignalR 论坛](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 或 [StackOverflow.com](http://stackoverflow.com/)。

## <a name="introduction"></a>简介

连接到中心的每个客户端传递唯一的连接 id。可以在中心上下文的属性中检索此值 `Context.ConnectionId` 。 如果你的应用程序需要将用户映射到连接 id 并保留该映射，则可以使用以下项之一：

- [用户 ID 提供程序 (SignalR 2) ](#IUserIdProvider)
- [内存中存储](#inmemory)，如字典
- [每个用户的 SignalR 组](#groups)
- [永久、外部存储](#database)（如数据库表或 Azure 表存储）

本主题中显示了每个实现。 使用类的 `OnConnected` 、 `OnDisconnected` 和 `OnReconnected` 方法 `Hub` 跟踪用户连接状态。

应用程序的最佳方法取决于：

- 承载应用程序的 web 服务器的数量。
- 是否需要获取当前连接的用户的列表。
- 应用程序或服务器重新启动时是否需要保留组和用户信息。
- 调用外部服务器的延迟是否存在问题。

下表显示了适用于这些注意事项的方法。

|  | 多个服务器 | 获取当前连接的用户的列表 | 重新启动后保留信息 | 最佳性能 |
| --- | --- | --- | --- | --- |
| UserID 提供程序 | ![](mapping-users-to-connections/_static/image1.png) |  |  | ![](mapping-users-to-connections/_static/image2.png) |
| 内存中 |  | ![](mapping-users-to-connections/_static/image3.png) |  | ![](mapping-users-to-connections/_static/image4.png) |
| 单用户组 | ![](mapping-users-to-connections/_static/image5.png) |  |  | ![](mapping-users-to-connections/_static/image6.png) |
| 永久、外部 | ![](mapping-users-to-connections/_static/image7.png) | ![](mapping-users-to-connections/_static/image8.png) | ![](mapping-users-to-connections/_static/image9.png) |  |

<a id="IUserIdProvider"></a>

## <a name="iuserid-provider"></a>IUserID 提供程序

此功能允许用户通过新的接口 IUserIdProvider 指定用户 Id 基于 IRequest 的内容。

**IUserIdProvider**

[!code-csharp[Main](mapping-users-to-connections/samples/sample1.cs)]

默认情况下，将有一个实现，该实现使用用户的 `IPrincipal.Identity.Name` 作为用户名。 若要更改此操作，请在应用程序启动时，将的实现注册到 `IUserIdProvider` 全局主机：

[!code-csharp[Main](mapping-users-to-connections/samples/sample2.cs)]

从中心内，你将能够通过以下 API 向这些用户发送消息：

**向特定用户发送消息**

[!code-csharp[Main](mapping-users-to-connections/samples/sample3.cs?highlight=5)]

<a id="inmemory"></a>

## <a name="in-memory-storage"></a>内存中存储

下面的示例演示如何在存储在内存中的字典中保留连接和用户信息。 字典使用 `HashSet` 来存储连接 id。用户随时可以与 SignalR 应用程序建立多个连接。 例如，通过多个设备或多个浏览器选项卡连接的用户将拥有多个连接 id。

如果应用程序关闭，所有信息都将丢失，但会在用户重新建立连接时重新填充。 如果你的环境包含多个 web 服务器，则内存中存储不起作用，因为每个服务器都有一个单独的连接集合。

第一个示例演示一个类，该类管理用户到连接的映射。 HashSet 的密钥将是用户的名称。

[!code-csharp[Main](mapping-users-to-connections/samples/sample4.cs)]

下一个示例演示如何从集线器使用连接映射类。 类的实例存储在变量名称中 `_connections` 。

[!code-csharp[Main](mapping-users-to-connections/samples/sample5.cs)]

<a id="groups"></a>

## <a name="single-user-groups"></a>单用户组

你可以为每个用户创建一个组，然后在你只需要访问该用户时向该组发送一条消息。 每个组的名称是用户的名称。 如果用户有多个连接，则会将每个连接 id 添加到用户的组中。

用户断开连接时，不应手动将用户从组中删除。 此操作由 SignalR 框架自动执行。

下面的示例演示如何实现单用户组。

[!code-csharp[Main](mapping-users-to-connections/samples/sample6.cs)]

<a id="database"></a>

## <a name="permanent-external-storage"></a>永久、外部存储

本主题说明如何使用数据库或 Azure 表存储来存储连接信息。 当你有多个 web 服务器时，这种方法可正常工作，因为每个 web 服务器可以与相同的数据存储库交互。 如果 web 服务器停止工作或重新启动应用程序，则 `OnDisconnected` 不会调用方法。 因此，您的数据存储库可能会记录不再有效的连接 id。 若要清理这些孤立记录，你可能希望使在与你的应用程序相关的时间范围之外创建的任何连接无效。 本节中的示例包含一个用于在创建连接时进行跟踪的值，但不显示如何清理旧记录，因为你可能想要将其作为后台进程执行。

### <a name="database"></a>数据库

下面的示例演示如何在数据库中保留连接和用户信息。 您可以使用任何数据访问技术;但下面的示例演示如何使用实体框架定义模型。 这些实体模型对应于数据库表和字段。 根据应用程序的要求，数据结构可能会有很大的差别。

第一个示例演示如何定义可以与多个连接实体相关联的用户实体。

[!code-csharp[Main](mapping-users-to-connections/samples/sample7.cs)]

然后，可以从中心跟踪每个连接的状态，如下所示。

[!code-csharp[Main](mapping-users-to-connections/samples/sample8.cs)]

<a id="azure"></a>
### <a name="azure-table-storage"></a>Azure 表存储

以下 Azure 表存储示例类似于数据库示例。 它不包含开始 Azure 表存储服务所需的所有信息。 有关信息，请参阅 [如何通过 .net 使用表存储](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/)。

下面的示例显示了用于存储连接信息的表实体。 它按用户名对数据进行分区，并通过连接 id 识别每个实体，因此用户可随时拥有多个连接。

[!code-csharp[Main](mapping-users-to-connections/samples/sample9.cs)]

在中心，你可以跟踪每个用户的连接的状态。

[!code-csharp[Main](mapping-users-to-connections/samples/sample10.cs)]

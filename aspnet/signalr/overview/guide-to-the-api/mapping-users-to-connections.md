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
# <a name="mapping-signalr-users-to-connections"></a>将 SignalR 用户映射到连接

 作者 [Tom FitzMacken](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 本主题演示如何保留有关用户及其连接的信息。
>
> 帕特里克·弗莱彻帮助写了这个话题。
>
> ## <a name="software-versions-used-in-this-topic"></a>本主题中使用的软件版本
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - .NET 4.5
> - 信号R版本 2
>
>
>
> ## <a name="previous-versions-of-this-topic"></a>本主题的早期版本
>
> 有关早期版本的 SignalR 的信息，请参阅[SignalR 旧版本](../older-versions/index.md)。
>
> ## <a name="questions-and-comments"></a>问题和评论
>
> 请留下反馈，关于你喜欢本教程的方式，以及我们可以在页面底部的评论中改进什么。 如果您有与本教程没有直接关系的问题，您可以将它们发布到[ASP.NET SignalR 论坛](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com/)。

## <a name="introduction"></a>简介

连接到集线器的每个客户端传递一个唯一的连接 ID。您可以在中心上下文的属性中`Context.ConnectionId`检索此值。 如果应用程序需要将用户映射到连接 ID 并保留该映射，则可以使用以下方式之一：

- [用户 ID 提供程序（信号器 2）](#IUserIdProvider)
- [内存中存储](#inmemory)，如字典
- [每个用户的信号R组](#groups)
- [永久外部存储](#database)，如数据库表或 Azure 表存储

本主题中显示了每个实现。 使用 类`OnConnected``OnDisconnected`的`OnReconnected`和 方法`Hub`来跟踪用户连接状态。

最适合您的应用程序的方法取决于：

- 托管应用程序的 Web 服务器数。
- 是否需要获取当前连接的用户的列表。
- 在应用程序或服务器重新启动时是否需要保留组和用户信息。
- 调用外部服务器的延迟是否是一个问题。

下表显示了哪种方法适用于这些注意事项。

|  | 多台服务器 | 获取当前连接用户的列表 | 重新启动后保留信息 | 最佳性能 |
| --- | --- | --- | --- | --- |
| 用户 ID 提供程序 | ![](mapping-users-to-connections/_static/image1.png) |  |  | ![](mapping-users-to-connections/_static/image2.png) |
| 内存中 |  | ![](mapping-users-to-connections/_static/image3.png) |  | ![](mapping-users-to-connections/_static/image4.png) |
| 单用户组 | ![](mapping-users-to-connections/_static/image5.png) |  |  | ![](mapping-users-to-connections/_static/image6.png) |
| 永久外部 | ![](mapping-users-to-connections/_static/image7.png) | ![](mapping-users-to-connections/_static/image8.png) | ![](mapping-users-to-connections/_static/image9.png) |  |

<a id="IUserIdProvider"></a>

## <a name="iuserid-provider"></a>IUserID 提供商

此功能允许用户通过新接口 IUserIdProvider 指定用户 Id 基于 IRequest 的内容。

**IUserId 提供商**

[!code-csharp[Main](mapping-users-to-connections/samples/sample1.cs)]

默认情况下，将有一个使用用户`IPrincipal.Identity.Name`作为用户名的实现。 要更改此项，请在应用程序启动`IUserIdProvider`时向全局主机注册实现：

[!code-csharp[Main](mapping-users-to-connections/samples/sample2.cs)]

从集线器中，您可以通过以下 API 向这些用户发送消息：

**向特定用户发送消息**

[!code-csharp[Main](mapping-users-to-connections/samples/sample3.cs?highlight=5)]

<a id="inmemory"></a>

## <a name="in-memory-storage"></a>内存中存储

以下示例演示如何在存储在内存中的字典中保留连接和用户信息。 字典使用 存储`HashSet`连接 ID。在任何时候，用户都可以与 SignalR 应用程序建立多个连接。 例如，通过多个设备或多个浏览器选项卡连接的用户将具有多个连接 ID。

如果应用程序关闭，所有信息都将丢失，但在用户重新建立其连接时将重新填充该信息。 如果环境包含多个 Web 服务器，则内存中存储不起作用，因为每台服务器都将具有单独的连接集合。

第一个示例显示了管理用户映射到连接的类。 哈希集的键将是用户名。

[!code-csharp[Main](mapping-users-to-connections/samples/sample4.cs)]

下一个示例演示如何使用中心的连接映射类。 类的实例存储在变量名称`_connections`中。

[!code-csharp[Main](mapping-users-to-connections/samples/sample5.cs)]

<a id="groups"></a>

## <a name="single-user-groups"></a>单用户组

您可以为每个用户创建一个组，然后在您只想联系该用户时向该组发送消息。 每个组的名称是用户的名称。 如果用户有多个连接，则每个连接 ID 将添加到用户的组中。

当用户断开连接时，不应手动从组中删除用户。 此操作由 SignalR 框架自动执行。

下面的示例演示如何实现单用户组。

[!code-csharp[Main](mapping-users-to-connections/samples/sample6.cs)]

<a id="database"></a>

## <a name="permanent-external-storage"></a>永久外部存储

本主题演示如何使用数据库或 Azure 表存储来存储连接信息。 当您有多个 Web 服务器时，此方法有效，因为每个 Web 服务器都可以与同一数据存储库进行交互。 如果 Web 服务器停止工作或应用程序重新启动，则不`OnDisconnected`调用该方法。 因此，数据存储库可能具有不再有效的连接 ID 记录。 要清理这些孤立记录，您可能希望使在与您的应用程序相关的时间范围之外创建的任何连接无效。 本节中的示例包括用于跟踪创建连接时间的值，但不显示如何清理旧记录，因为您可能希望作为后台进程执行此操作。

### <a name="database"></a>数据库

以下示例演示如何在数据库中保留连接和用户信息。 您可以使用任何数据访问技术;但是，下面的示例演示如何使用实体框架定义模型。 这些实体模型对应于数据库表和字段。 您的数据结构可能因应用程序的要求而有很大差异。

第一个示例演示如何定义可以与许多连接实体关联的用户实体。

[!code-csharp[Main](mapping-users-to-connections/samples/sample7.cs)]

然后，从集线器，您可以使用下面显示的代码跟踪每个连接的状态。

[!code-csharp[Main](mapping-users-to-connections/samples/sample8.cs)]

<a id="azure"></a>
### <a name="azure-table-storage"></a>Azure 表存储

以下 Azure 表存储示例与数据库示例类似。 它不包括开始使用 Azure 表存储服务所需的所有信息。 有关详细信息，请参阅[如何使用 .NET 中的表存储](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/)。

下面的示例显示了用于存储连接信息的表实体。 它按用户名对数据进行分区，并通过连接 ID 标识每个实体，以便用户可以随时具有多个连接。

[!code-csharp[Main](mapping-users-to-connections/samples/sample9.cs)]

在集线器中，您可以跟踪每个用户的连接状态。

[!code-csharp[Main](mapping-users-to-connections/samples/sample10.cs)]

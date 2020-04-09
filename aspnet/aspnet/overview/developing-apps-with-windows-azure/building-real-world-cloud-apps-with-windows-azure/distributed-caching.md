---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/distributed-caching
title: 分布式缓存（使用 Azure 构建真实世界云应用） |微软文档
author: MikeWasson
description: 使用 Azure 电子书构建真实世界云应用基于 Scott Guthrie 开发的演示文稿。 它解释了13种模式和做法，他可以...
ms.author: riande
ms.date: 07/20/2015
ms.assetid: 406518e9-3817-49ce-8b90-e82bc461e2c0
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/distributed-caching
msc.type: authoredcontent
ms.openlocfilehash: 87a7516415895e761d1589fd459b93e5c15c0f85
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675657"
---
# <a name="distributed-caching-building-real-world-cloud-apps-with-azure"></a>分布式缓存（使用 Azure 构建真实世界云应用）

由[迈克·瓦森](https://github.com/MikeWasson)，[里克·安德森](https://twitter.com/RickAndMSFT)，[汤姆·戴克斯特拉](https://github.com/tdykstra)

[下载修复它项目](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)或[下载电子书](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> 使用 Azure 电子书**构建真实世界云应用**基于 Scott Guthrie 开发的演示文稿。 它解释了 13 种模式和做法，这些模式和做法可以帮助您成功开发云的 Web 应用。 有关电子书的信息，请参阅[第一章](introduction.md)。

上一章研究了瞬态故障处理，并提到缓存作为断路器策略。 本章提供了有关缓存的更多背景，包括何时使用它、使用它的常见模式以及如何在 Azure 中实现缓存。

## <a name="what-is-distributed-caching"></a>什么是分布式缓存

缓存通过将数据存储在内存中，提供对通常访问的应用程序数据的高吞吐量、低延迟访问。 对于云应用，最有用的缓存类型是分布式缓存，这意味着数据不是存储在单个 Web 服务器的内存上，而是存储在其他云资源上，缓存的数据可供应用程序的所有 Web 服务器（或应用程序使用的其他云 VM）使用。

![显示访问同一缓存服务器的多个 Web 服务器的图表](distributed-caching/_static/image1.png)

当应用程序通过添加或删除服务器进行扩展，或者当服务器由于升级或故障而更换时，缓存的数据仍可供运行该应用程序的每个服务器访问。

通过避免持久数据存储的高延迟数据访问，缓存可以显著提高应用程序的响应能力。 例如，从缓存检索数据比从关系数据库检索数据要快得多。

缓存的一个附带好处是减少了持久数据存储的流量，当持久数据存储需要数据出口费用时，这可能会导致更低的成本。

## <a name="when-to-use-distributed-caching"></a>何时使用分布式缓存

缓存最适合使用比写入数据更多的读取工作负荷，以及当数据模型支持用于在缓存中存储和检索数据的键/值组织时。 当应用程序用户共享大量常见数据时，它也更有用;例如，如果每个用户通常检索该用户独有的数据，则缓存不会提供尽可能多的好处。 缓存可能非常有益的一个示例是产品目录，因为数据不会频繁更改，并且所有客户都在查看相同的数据。

缓存的好处越来越可衡量，应用程序越扩展，持久数据存储的吞吐量限制和延迟延迟就对整体应用程序性能造成更大的限制。 但是，您可能出于其他原因实现缓存，而不是性能。 对于在向用户显示时不必完全最新的数据，缓存访问可以作为断路器，用于持久数据存储无响应或不可用时的数据。

## <a name="popular-cache-population-strategies"></a>流行的缓存填充策略

为了能够从缓存中检索数据，您必须先将其存储在该缓存中。 有几种策略用于将数据放入缓存中：

- 按需/缓存旁

    应用程序尝试从缓存中检索数据，当缓存没有数据（"错误"）时，应用程序将数据存储在缓存中，以便下次数据可用。 下次应用程序尝试获取相同的数据时，它会在缓存中找到它要查找的内容（"命中"）。 为了防止获取数据库中已更改的缓存数据，在更改数据存储时使缓存无效。
- 后台数据推送

    后台服务会定期将数据推送到缓存中，并且应用始终从缓存中拉出。 此方法非常适合不需要始终返回最新数据的高延迟数据源。
- 断路器

    应用程序通常直接与持久数据存储通信，但当持久数据存储存在可用性问题时，应用程序将从缓存中检索数据。 数据可能已使用缓存旁或后台数据推送策略放入缓存中。 这是一种故障处理策略，而不是性能增强策略。

为了保持缓存中的数据最新，可以在应用程序创建、更新或删除数据时删除相关的缓存条目。 如果应用程序有时可以获取稍微过时的数据，则可以依靠可配置的过期时间来设置缓存数据可能有多旧的限制。

您可以配置绝对过期（自创建缓存项以来的时间量）或滑动过期（自上次访问缓存项以来的时间量）。 当您依赖于缓存过期机制以防止数据变得过于陈旧时，将使用绝对过期。 在 Fix It 应用中，我们将手动驱逐陈旧的缓存项，我们将使用滑动过期来将最新的数据保存在缓存中。 无论您选择哪种过期策略，当达到缓存的内存限制时，缓存将自动驱逐最旧的（最近使用或 LRU）项目。

## <a name="sample-cache-aside-code-for-fix-it-app"></a>用于修复它应用的示例缓存旁代码

在以下示例代码中，在检索修复 It 任务时，我们首先检查缓存。 如果在缓存中找到任务，我们会返回它;如果任务在缓存中找到，则返回它。如果未找到，我们会从数据库中获取它并将其存储在缓存中。 要向`FindTaskByIdAsync`方法添加缓存所做的更改将突出显示。

[!code-csharp[Main](distributed-caching/samples/sample1.cs?highlight=5,9-11,13-15,19)]

更新或删除修复 It 任务时，必须使缓存的任务无效（删除）。 否则，将来尝试读取该任务将继续从缓存中获取旧数据。

[!code-csharp[Main](distributed-caching/samples/sample2.cs?highlight=7)]

这些示例说明了简单的缓存代码;缓存尚未在可下载的修复 It 项目中实现。

## <a name="azure-caching-services"></a>Azure 缓存服务

Azure 提供以下缓存服务[：Azure Redis 缓存](https://msdn.microsoft.com/library/dn690523.aspx)和[Azure 托管缓存](https://msdn.microsoft.com/library/dn386094.aspx)。 Azure Redis 缓存基于流行的[开源 Redis 缓存](http://redis.io/)，是大多数缓存方案的首选。

<a id="sessionstate"></a>
## <a name="aspnet-session-state-using-a-cache-provider"></a>使用缓存提供程序ASP.NET会话状态

如 Web[开发最佳实践章节](web-development-best-practices.md)所述，最佳做法是避免使用会话状态。 如果应用程序需要会话状态，则下一个最佳做法是避免默认内存中提供程序，因为这不会启用横向扩展（Web 服务器的多个实例）。 ASP.NET SQL Server 会话状态提供程序使在多个 Web 服务器上运行的站点能够使用会话状态，但与内存中提供程序相比，它会产生较高的延迟成本。 如果必须使用会话状态，则最佳解决方案是使用缓存提供程序，例如[Azure 缓存的会话状态提供程序](https://msdn.microsoft.com/library/windowsazure/gg185668.aspx)。

## <a name="summary"></a>总结

您已经看到 Fix It 应用如何实现缓存，以提高响应时间和可伸缩性，并使应用在数据库不可用时继续为读取操作响应。 [在下一章](queue-centric-work-pattern.md)中，我们将介绍如何进一步提高可伸缩性，并使应用继续对写入操作进行响应。

## <a name="resources"></a>资源

有关缓存的详细信息，请参阅以下资源。

文档

- [Azure 缓存](https://msdn.microsoft.com/library/gg278356.aspx)。 有关 Azure 缓存的官方 MSDN 文档。
- [微软模式和实践 - Azure 指南](https://msdn.microsoft.com/library/dn568099.aspx)。 请参阅缓存指南和缓存放置模式。
- [故障保护：弹性云体系结构指南](https://msdn.microsoft.com/library/windowsazure/jj853352.aspx)。 马克·默库里、乌尔里希·霍曼和安德鲁·汤希尔的白皮书。 请参阅有关缓存的部分。
- [Azure 云服务上大规模服务设计的最佳做法](https://msdn.microsoft.com/library/windowsazure/jj717232.aspx)。 W. 马克·西姆斯和迈克尔·托马斯的白皮书。 请参阅有关分布式缓存的部分。
- [分布式缓存在可伸缩性路径上](https://msdn.microsoft.com/magazine/dd942840.aspx)。 一篇较老的（2009）MSDN杂志文章，但一般对分布式缓存的清晰书面介绍;比故障安全和最佳实践白皮书的缓存部分更深入。

视频

- [故障安全：构建可扩展的、有弹性的云服务](https://channel9.msdn.com/Series/FailSafe)。 由乌尔里希·霍曼、马克·默库里和马克·西姆斯的九集系列。 提供如何构建云应用的 400 级视图。 本系列主要探讨理论和原因;有关更多如何使用的详细信息，请参阅马克·西姆斯的"建筑大"系列。 请参阅第 3 集的缓存讨论，从 1：24：14 开始。
- [构建大：从 Azure 客户那里吸取的教训 - 第 I 部分](https://channel9.msdn.com/Events/Build/2012/3-029)。西蒙·戴维斯讨论从46：00开始的分布式缓存。 类似于故障安全系列，但进入更多如何使用的详细信息。 该演示文稿于 2012 年 10 月 31 日提供，因此不包括 2013 年推出的 Azure 应用服务中的 Web 应用缓存服务。

代码示例

- [Azure 中的云服务基础知识](https://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649)。 实现分布式缓存的示例应用程序。 请参阅随附的博客文章["云服务基础知识 + 缓存基础知识](https://blogs.msdn.com/b/windowsazure/archive/2013/10/03/cloud-service-fundamentals-caching-basics.aspx)"。

> [!div class="step-by-step"]
> [上一页](transient-fault-handling.md)
> [下一页](queue-centric-work-pattern.md)

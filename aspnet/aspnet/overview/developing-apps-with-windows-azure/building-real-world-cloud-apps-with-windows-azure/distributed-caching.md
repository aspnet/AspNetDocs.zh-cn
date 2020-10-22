---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/distributed-caching
title: 分布式缓存 (用 Azure) 生成 Real-World 云应用 |Microsoft Docs
author: MikeWasson
description: 使用 Azure 电子书构建真实的云应用基于 Scott Guthrie 开发的演示文稿。 它介绍了13种模式和实践，
ms.author: riande
ms.date: 07/20/2015
ms.assetid: 406518e9-3817-49ce-8b90-e82bc461e2c0
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/distributed-caching
msc.type: authoredcontent
ms.openlocfilehash: 87a7516415895e761d1589fd459b93e5c15c0f85
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345517"
---
# <a name="distributed-caching-building-real-world-cloud-apps-with-azure"></a>分布式缓存 (用 Azure) 生成 Real-World 云应用

作者： [Mike Wasson](https://github.com/MikeWasson)， [Rick Anderson](https://twitter.com/RickAndMSFT)， [Tom Dykstra](https://github.com/tdykstra)

[下载 Fix It 项目](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) 或 [下载电子书](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> **使用 Azure 电子书构建真实的云应用**基于 Scott Guthrie 开发的演示文稿。 它介绍了可帮助你成功开发云的 web 应用的13种模式和实践。 有关电子书的信息，请参阅 [第一章](introduction.md)。

上一章介绍了暂时性故障处理，并将所述缓存视为断路器策略。 本章提供有关缓存的更多背景知识，包括何时使用它、使用它的常用模式，以及如何在 Azure 中实现它。

## <a name="what-is-distributed-caching"></a>什么是分布式缓存

缓存通过将数据存储在内存中，为经常访问的应用程序数据提供高吞吐量、低延迟的访问。 对于云应用，最有用的缓存类型为分布式缓存，这意味着，数据不会存储在单个 web 服务器的内存中，而是存储在其他云资源上，并且缓存数据可用于应用程序) 所使用的所有应用程序 web 服务器 (或其他云 Vm。

![显示访问同一缓存服务器的多个 web 服务器的图示](distributed-caching/_static/image1.png)

当应用程序通过添加或删除服务器进行缩放，或由于升级或故障而替换服务器时，每个运行应用程序的服务器都可以访问缓存的数据。

通过避免永久性数据存储的高延迟数据访问，缓存可以显著提高应用程序的响应能力。 例如，从缓存中检索数据比从关系数据库检索数据快得多。

缓存的一个优点是，将流量降低到持久数据存储，这可能会导致在发生永久性数据存储的数据传出费用时降低成本。

## <a name="when-to-use-distributed-caching"></a>何时使用分布式缓存

缓存最适用于比写入数据更多的应用程序工作负荷，以及当数据模型支持用于在缓存中存储和检索数据的键/值组织时。 当应用程序用户共享很多常见数据时，此方法也更有用。例如，如果每个用户通常检索特定于该用户的数据，则缓存不会提供很多好处。 缓存可能非常有用的示例是产品目录，因为数据不经常更改，并且所有客户都要查看相同的数据。

由于持久数据存储区的吞吐量限制和延迟延迟对应用程序性能的影响更大，因此缓存的优点会越来越大。 但是，你可能会出于其他原因而不是性能来实现缓存。 对于在向用户显示时不需要完全更新的数据，在永久数据存储无响应或不可用的情况下，缓存访问可用作断路器。

## <a name="popular-cache-population-strategies"></a>常用缓存填充策略

为了能够从缓存中检索数据，必须先将数据存储在此处。 有多个策略可用于在缓存中获取所需的数据：

- 按需/缓存

    应用程序尝试从缓存中检索数据，当缓存中没有数据 ("未命中" ) 时，应用程序将数据存储在缓存中，以便在下次可用时使用。 下次应用程序尝试获取相同数据时，它会在缓存中查找它要查找的内容， ("命中" ) 。 若要防止提取数据库中已更改的缓存数据，请在对数据存储进行更改时使缓存无效。
- 后台数据推送

    后台服务定期将数据推入缓存，应用始终从缓存中提取数据。 此方法非常适用于不要求始终返回最新数据的高延迟数据源。
- 断路器

    应用程序通常直接与永久性数据存储进行通信，但当永久性数据存储具有可用性问题时，应用程序将从缓存中检索数据。 数据可能已使用缓存留出或后台数据推送策略放入缓存中。 这是一种错误处理策略，而不是提高性能。

为了使缓存中的数据保持最新，可以在应用程序创建、更新或删除数据时删除相关的缓存条目。 如果您的应用程序有时会获得略微过期的数据，则可以依赖于可配置的过期时间来设置旧缓存数据的可以使用的限制。

你可以配置在创建缓存项后 (的绝对过期时间) 或可调过期时间， (自上次访问缓存项后) 的时间量。 当你根据缓存过期机制阻止数据变得太过时，将使用绝对过期。 在 Fix It 应用程序中，我们将手动逐出过时缓存项，并使用滑动过期将最新的数据保留在缓存中。 无论选择哪种过期策略，缓存在达到缓存的内存限制时，都将自动逐出最早 (最早使用或 LRU) 项。

## <a name="sample-cache-aside-code-for-fix-it-app"></a>示例缓存-用于修复 It 应用的代码

在下面的示例代码中，我们会在检索到 Fix It 任务时先检查缓存。 如果在缓存中找到该任务，则返回它;如果找不到，则从数据库获取该数据库，并将其存储在缓存中。 将突出显示将缓存添加到方法所做的更改 `FindTaskByIdAsync` 。

[!code-csharp[Main](distributed-caching/samples/sample1.cs?highlight=5,9-11,13-15,19)]

当你更新或删除 Fix It task 时，必须使 (删除) 缓存的任务无效。 否则，将来尝试读取该任务将继续获取缓存中的旧数据。

[!code-csharp[Main](distributed-caching/samples/sample2.cs?highlight=7)]

下面是用于阐释简单缓存代码的示例;在可下载的 Fix It 项目中未实现缓存。

## <a name="azure-caching-services"></a>Azure 缓存服务

Azure 提供以下缓存服务： [Azure Redis 缓存](https://msdn.microsoft.com/library/dn690523.aspx) 和 [azure 托管缓存](https://msdn.microsoft.com/library/dn386094.aspx)。 Azure Redis 缓存基于流行的 [开放源代码 Redis 缓存](http://redis.io/) ，是大多数缓存方案的第一种选择。

<a id="sessionstate"></a>
## <a name="aspnet-session-state-using-a-cache-provider"></a>使用缓存提供程序的 ASP.NET 会话状态

如 [web 开发最佳实践一章](web-development-best-practices.md)中所述，最佳做法是避免使用会话状态。 如果应用程序需要会话状态，则下一种最佳做法是避免默认的内存中提供程序，因为这不会启用 (多个 web 服务器实例) 。 ASP.NET SQL Server 的会话状态提供程序允许在多个 web 服务器上运行的站点使用会话状态，但与内存中提供程序相比，这会产生较高的延迟成本。 如果必须使用会话状态，最佳解决方案是使用缓存提供程序，例如 [Azure 缓存的会话状态提供程序](https://msdn.microsoft.com/library/windowsazure/gg185668.aspx)。

## <a name="summary"></a>总结

您已经了解了 Fix It 应用程序可以如何实现缓存，以便提高响应时间和伸缩性，并使应用程序在数据库不可用时继续响应读取操作。 在 [下一章](queue-centric-work-pattern.md) 中，我们将演示如何进一步提高可伸缩性，并使应用程序继续响应写入操作。

## <a name="resources"></a>资源

有关缓存的详细信息，请参阅以下资源。

文档

- [Azure 缓存](https://msdn.microsoft.com/library/gg278356.aspx)。 有关 Azure 中的缓存的官方 MSDN 文档。
- [Microsoft 模式和实践-Azure 指南](https://msdn.microsoft.com/library/dn568099.aspx)。 请参阅缓存指南和 Cache-Aside 模式。
- [防故障：弹性云体系结构的指南](https://msdn.microsoft.com/library/windowsazure/jj853352.aspx)。 白皮书 by Marc Mercuri、Ulrich Homann 和 Andrew Townhill。 请参阅有关缓存的部分。
- [在 Azure 云服务上设计 Large-Scale 服务的最佳实践](https://msdn.microsoft.com/library/windowsazure/jj717232.aspx)。 W. 通过标记 Simm 和 Michael Thomassy 的白皮书。 请参阅有关分布式缓存的部分。
- [可伸缩性的路径上的分布式缓存](https://msdn.microsoft.com/magazine/dd942840.aspx)。 更早的 (2009) MSDN 杂志文章，但在一般情况下编写了分布式缓存简介;与故障和最佳做法白皮书中的缓存部分相比，更深入。

视频

- [故障安全：构建可缩放且可复原的云服务](https://channel9.msdn.com/Series/FailSafe)。 九部分系列： Ulrich Homann、Marc Mercuri 和 Mark Simm。 显示了一个关于如何构建云应用程序的400级别视图。 此系列重点介绍理论和原因;有关详细操作方法的详细信息，请参阅通过标记 Simm 构建大系列。 请参阅从1:24:14 开始的剧集3中的缓存讨论。
- [构建大：从 Azure 客户那里学习的课程-第 I 部分](https://channel9.msdn.com/Events/Build/2012/3-029)。Simon Davies 讨论了从46:00 开始的分布式缓存。 与故障保护系列类似，但更详细地介绍了更多操作方法。 此演示已于2012年10月31日提供，因此它不会涵盖2013中引入 Azure App Service 的 Web 应用的缓存服务。

代码示例

- [Azure 中的云服务基础知识](https://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649)。 实现分布式缓存的示例应用程序。 请参阅随附的博客文章 [云服务基础知识-缓存基础知识](https://blogs.msdn.com/b/windowsazure/archive/2013/10/03/cloud-service-fundamentals-caching-basics.aspx)。

> [!div class="step-by-step"]
> [上一页](transient-fault-handling.md)
> [下一页](queue-centric-work-pattern.md)

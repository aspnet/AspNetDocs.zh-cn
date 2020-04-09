---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices
title: Web 开发最佳实践（使用 Azure 构建真实世界的云应用） |微软文档
author: MikeWasson
description: 使用 Azure 电子书构建真实世界云应用基于 Scott Guthrie 开发的演示文稿。 它解释了13种模式和做法，他可以...
ms.author: riande
ms.date: 06/12/2014
ms.assetid: 52d6c941-2cd9-442f-9872-2c798d6d90cd
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices
msc.type: authoredcontent
ms.openlocfilehash: dfd8a3ac2328d3f17dfbe36e68b37d181177b0f4
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675639"
---
# <a name="web-development-best-practices-building-real-world-cloud-apps-with-azure"></a>Web 开发最佳实践（使用 Azure 构建真实世界的云应用）

由[迈克·瓦森](https://github.com/MikeWasson)，[里克·安德森](https://twitter.com/RickAndMSFT)，[汤姆·戴克斯特拉](https://github.com/tdykstra)

[下载修复它项目](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)或[下载电子书](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> 使用 Azure 电子书**构建真实世界云应用**基于 Scott Guthrie 开发的演示文稿。 它解释了 13 种模式和做法，这些模式和做法可以帮助您成功开发云的 Web 应用。 有关电子书的信息，请参阅[第一章](introduction.md)。

前三种模式是关于建立敏捷开发过程;其余的是关于体系结构和代码的。 本文集了 Web 开发最佳实践集：

- 智能负载均衡器后面的[无状态 Web 服务器](#stateless)。
- [避免会话状态](#sessionstate)（或者无法避免，请使用分布式缓存而不是数据库）。
- [使用 CDN](#cdn)边缘缓存静态文件资产（图像、脚本）。
- [使用 .NET 4.5 的异步支持](#async)以避免阻塞呼叫。

这些实践适用于所有 Web 开发，不仅适用于云应用，而且对于云应用尤其重要。 它们协同工作，帮助您优化使用云环境提供的高度灵活的扩展。 如果不遵循这些做法，则在尝试扩展应用程序时将遇到限制。

<a id="stateless"></a>
## <a name="stateless-web-tier-behind-a-smart-load-balancer"></a>智能负载均衡器背后的无状态 Web 层

*无状态 Web 层*意味着您不将任何应用程序数据存储在 Web 服务器内存或文件系统中。 保持 Web 层无状态使您能够提供更好的客户体验并节省资金：

- 如果 Web 层是无状态的，并且位于负载均衡器后面，则可以通过动态添加或删除服务器来快速响应应用程序流量的变化。 在云环境中，只要您实际使用服务器资源，您只需为服务器资源付费，响应需求变化的能力就可以转化为巨大的节省。
- 无状态 Web 层在体系结构上比应用程序扩展要简单得多。 这还使您能够更快地响应扩展需求，并在此过程中在开发和测试上花费更少的资金。
- 云服务器（如本地服务器）需要偶尔进行修补和重新启动;如果 Web 层是无状态的，则当服务器暂时关闭时重新路由流量不会导致错误或意外行为。

大多数实际应用程序确实需要存储 Web 会话的状态;这里的要点不是将其存储在 Web 服务器上。 您可以通过其他方式存储状态，例如在 Cookie 中的客户端上，或者使用缓存提供程序将ASP.NET会话状态的进程服务器端存储在进程之外。 您可以将文件存储在[Windows Azure Blob 存储](unstructured-blob-storage.md)中，而不是本地文件系统。

如果 Web 层是无状态的，请参阅管理门户中的 Windows Azure 网站**缩放**选项卡，例如在 Windows Azure 网站中缩放应用程序是多么容易：

![“缩放”选项卡](web-development-best-practices/_static/image1.png)

如果要添加 Web 服务器，只需将实例计数滑块拖动到右侧即可。 将其设置为 5 并单击 **"保存**"，几秒钟内 Windows Azure 中将有 5 台 Web 服务器处理网站流量。

![五个实例](web-development-best-practices/_static/image2.png)

您可以同样轻松地将实例计数设置为 3 或向下设置为 1。 缩减规模时，可以立即开始节省资金，因为 Windows Azure 按分钟而不是按小时收费。

您还可以告诉 Windows Azure 根据 CPU 使用情况自动增加或减少 Web 服务器的数量。 在下面的示例中，当 CPU 使用率低于 60% 时，Web 服务器的数量将减少到至少 2，如果 CPU 使用率超过 80%，Web 服务器的数量将增加到最多 4 个。

![按 CPU 使用率进行缩放](web-development-best-practices/_static/image3.png)

或者，如果您知道您的网站只会在工作时间繁忙？ 您可以告诉 Windows Azure 在白天运行多个服务器，并减少到单个服务器晚上、晚上和周末。 以下一系列屏幕截图演示如何设置网站以在工作时间从上午 8 点到下午 5 点的工作时间运行一台服务器和 4 台服务器。

![按计划缩放](web-development-best-practices/_static/image4.png)

![设置计划时间](web-development-best-practices/_static/image5.png)

![日用时间表](web-development-best-practices/_static/image6.png)

![周末安排](web-development-best-practices/_static/image7.png)

![周末时间表](web-development-best-practices/_static/image8.png)

当然，所有这些都可以在脚本和门户中完成。

应用程序横向扩展的能力在 Windows Azure 中几乎是无限的，只要通过保持 Web 层处于无状态，避免动态添加或删除服务器 VM 的障碍。

<a id="sessionstate"></a>
## <a name="avoid-session-state"></a>避免会话状态

在实际云应用中避免存储某种形式的用户会话状态通常是不现实的，但某些方法相比其他方法而言，对性能和可伸缩性的影响更大。 如果需要存储状态，最佳解决方案是使状态量保持较小并将其存储在 Cookie 中。 如果这不可行，下一个最佳解决方案是使用ASP.NET会话状态与[分布式内存缓存的](distributed-caching.md#sessionstate)提供程序。 从性能和可伸缩性的角度来看，最差的解决方案是使用数据库支持的会话状态提供程序。

<a id="cdn"></a>
## <a name="use-a-cdn-to-cache-static-file-assets"></a>使用 CDN 缓存静态文件资产

CDN 是内容交付网络的首字母缩写词。 您将静态文件资产（如图像和脚本文件）提供给 CDN 提供程序，并且提供程序将这些文件缓存在世界各地的数据中心中，以便无论人们访问您的应用程序，他们都会得到相对快速的响应和低延迟的缓存资产。 这将加快站点的总体加载时间，并减少 Web 服务器上的负载。 如果要覆盖在地理位置广泛分布的受众，CDN 尤其重要。

Windows Azure 具有 CDN，您可以在在 Windows Azure 或任何 Web 托管环境中运行的应用程序中使用其他 CDN。

<a id="async"></a>
## <a name="use-net-45s-async-support-to-avoid-blocking-calls"></a>使用 .NET 4.5 的异步支持以避免阻塞呼叫

.NET 4.5 增强了 C# 和 VB 编程语言，以便以异步方式处理任务变得更加简单。 异步编程的好处并不仅仅针对并行处理情况，例如当您希望同时启动多个 Web 服务调用时。 它还使 Web 服务器能够在高负载条件下更高效、更可靠地执行。 Web 服务器只有数量有限的可用线程，并且在使用的所有线程时，在高负载条件下，传入请求必须等待，直到线程被释放。 如果应用程序代码不以异步方式处理数据库查询和 Web 服务调用等任务，则服务器在等待 I/O 响应时，许多线程会不必要地绑定起来。 这限制了服务器在高负载条件下可以处理的流量。 使用异步编程，等待 Web 服务或数据库返回数据的线程将被释放以服务新请求，直到收到数据。 在繁忙的 Web 服务器中，可以立即处理数百或数千个请求，否则等待释放线程。

如前所述，减少处理 Web 站点的 Web 服务器数量与增加网站数量一样简单。 因此，如果服务器可以实现更高的吞吐量，则不需要尽可能多的服务器，并且您可以降低成本，因为给定流量所需的服务器比否则的要少。

对 .NET 4.5 异步编程模型的支持包含在 Web 窗体、MVC 和 Web API 的 ASP.NET 4.5 中;在实体框架 6 和[Windows Azure 存储 API](https://blogs.msdn.com/b/windowsazurestorage/archive/2013/07/12/introducing-storage-client-library-2-1-rc-for-net-and-windows-phone-8.aspx)中。

### <a name="async-support-in-aspnet-45"></a>ASP.NET 4.5 中的异步支持

在 ASP.NET 4.5 中，不仅对异步编程的支持不仅添加到语言中，还添加到 MVC、Web 窗体和 Web API 框架中。 例如，ASP.NET MVC 控制器操作方法从 Web 请求接收数据并将数据传递到视图，然后创建要发送到浏览器的 HTML。 通常，操作方法需要从数据库或 Web 服务获取数据，以便将其显示在网页中或保存在网页中输入的数据。 在这些情况下，使操作方法变得异步：而不是返回*ActionResult*对象，而是返回*Task&lt;ActionResult&gt;* 并使用*异步*关键字标记该方法。 在方法内，当一行代码启动涉及等待时间的操作时，可以使用 await 关键字对其进行标记。

下面是调用数据库查询的存储库方法的简单操作方法：

[!code-csharp[Main](web-development-best-practices/samples/sample1.cs)]

下面是异步处理数据库调用的相同方法：

[!code-csharp[Main](web-development-best-practices/samples/sample2.cs?highlight=1,4)]

在封面下，编译器生成适当的异步代码。 当应用程序调用`FindTaskByIdAsync`时，ASP.NET发出`FindTask`请求，然后展开工作线程，使其可用于处理另一个请求。 完成`FindTask`请求后，将重新启动一个线程，以继续处理该调用后的代码。 在启动`FindTask`请求和返回数据之间的期间，您有一个线程可用于执行有用的工作，否则将捆绑等待响应。

异步代码存在一些开销，但在低负载条件下，开销可以忽略不计，而在高负载条件下，您可以处理等待可用线程的请求。

自 1.1 ASP.NET以来，可以进行此类异步编程，但编写起来很困难，容易出错，调试起来也很困难。 现在，我们已经在 ASP.NET 4.5 中简化了它的编码，因此没有理由不再这样做。

### <a name="async-support-in-entity-framework-6"></a>实体框架 6 中的异步支持

作为 4.5 中异步支持的一部分，我们为 Web 服务调用、套接字和文件系统 I/O 提供了异步支持，但 Web 应用程序最常见的模式是访问数据库，并且我们的数据库不支持异步。 现在实体框架 6 添加了对数据库访问的异步支持。

在实体框架 6 中，导致将查询或命令发送到数据库的所有方法都有异步版本。 此处的示例显示了*Find*方法的异步版本。

[!code-csharp[Main](web-development-best-practices/samples/sample3.cs?highlight=8)]

这种异步支持不仅适用于插入、删除、更新和简单查找，还适用于 LINQ 查询：

[!code-csharp[Main](web-development-best-practices/samples/sample4.cs?highlight=7,10)]

方法有一个版本`Async`，`ToList`因为在此代码中，该方法会导致查询发送到数据库。 `Where`和`OrderByDescending`方法仅配置查询，`ToListAsync`而 方法执行查询并将响应存储在变量中。 `result`

## <a name="summary"></a>总结

您可以在任何 Web 编程框架和任何云环境中实现此处概述的 Web 开发最佳实践，但我们在ASP.NET和 Windows Azure 中都有工具，以便轻松。 如果您遵循这些模式，您可以轻松地横向扩展 Web 层，并且会将开支降至最低，因为每台服务器将能够处理更多的流量。

[下一章](single-sign-on.md)将介绍云如何启用单一登录方案。

## <a name="resources"></a>资源

有关详细信息，请参阅以下资源。

无状态 Web 服务器：

- [微软模式和实践 - 自动缩放指南](https://msdn.microsoft.com/library/dn589774.aspx)。
- [在 Windows Azure 网站中禁用 ARR 的实例相关性](https://azure.microsoft.com/blog/2013/11/18/disabling-arrs-instance-affinity-in-windows-azure-web-sites/)。 Erez Benari 的博客文章解释了 Windows Azure 网站中的会话相关性。

Cdn：

- [故障安全：构建可扩展的、有弹性的云服务](https://channel9.msdn.com/Series/FailSafe)。 由乌尔里希·霍曼、马克·默库里和马克·西姆斯制作九集视频系列。 请参阅第 3 集中的 CDN 讨论，从 1：34：00 开始。
- [微软模式和实践静态内容托管模式](https://msdn.microsoft.com/library/dn589776.aspx)
- [CDN 评论](http://www.cdnreviews.com/). 许多 CDN 的概述。

异步编程：

- [在 mVC ASP.NET 中使用异步方法](../../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md)。 里克·安德森的教程。
- [具有异步和 Await 的异步编程（C# 和可视化基本）](https://msdn.microsoft.com/library/vstudio/hh191443.aspx)。 MSDN 白皮书解释了异步编程的基本原理、它在ASP.NET 4.5 中的工作方式以及如何编写代码来实现它。
- [实体框架异步查询和保存](https://msdn.microsoft.com/data/jj819165)
- [如何使用 async 构建ASP.NET Web 应用程序](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2013/DEV-B337#fbid=tgkT4SR_DK7)。 罗文·米勒的视频演示。 包括一个图形演示，演示异步编程如何在高负载条件下促进 Web 服务器吞吐量的大幅提升。
- [故障安全：构建可扩展的、有弹性的云服务](https://channel9.msdn.com/Series/FailSafe)。 由乌尔里希·霍曼、马克·默库里和马克·西姆斯制作九集视频系列。 有关异步编程对可伸缩性的影响的讨论，请参阅第 4 集和第 8 集。
- [在4.5ASP.NET使用异步方法的魔力加上一个重要的gotcha。](http://www.hanselman.com/blog/TheMagicOfUsingAsynchronousMethodsInASPNET45PlusAnImportantGotcha.aspx) 斯科特·汉瑟曼的博客文章，主要是关于在ASP.NET Web 表单应用程序中使用异步。

有关其他 Web 开发最佳实践，请参阅以下资源：

- [修复它示例应用程序 - 最佳实践](the-fix-it-sample-application.md#bestpractices)。 此电子书的附录列出了在 Fix It 应用程序中实现的一些最佳实践。
- [Web 开发人员清单](http://webdevchecklist.com/asp.net)

> [!div class="step-by-step"]
> [上一页](continuous-integration-and-continuous-delivery.md)
> [下一页](single-sign-on.md)

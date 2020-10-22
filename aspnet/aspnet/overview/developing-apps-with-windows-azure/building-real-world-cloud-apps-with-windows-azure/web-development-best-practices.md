---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices
title: 利用 Azure) 生成 Real-World 云应用 (的 Web 开发最佳做法 |Microsoft Docs
author: MikeWasson
description: 使用 Azure 电子书构建真实的云应用基于 Scott Guthrie 开发的演示文稿。 它介绍了13种模式和实践，
ms.author: riande
ms.date: 06/12/2014
ms.assetid: 52d6c941-2cd9-442f-9872-2c798d6d90cd
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices
msc.type: authoredcontent
ms.openlocfilehash: dfd8a3ac2328d3f17dfbe36e68b37d181177b0f4
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345509"
---
# <a name="web-development-best-practices-building-real-world-cloud-apps-with-azure"></a>利用 Azure) 生成 Real-World 云应用 (的 Web 开发最佳做法

作者： [Mike Wasson](https://github.com/MikeWasson)， [Rick Anderson](https://twitter.com/RickAndMSFT)， [Tom Dykstra](https://github.com/tdykstra)

[下载 Fix It 项目](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) 或 [下载电子书](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> **使用 Azure 电子书构建真实的云应用**基于 Scott Guthrie 开发的演示文稿。 它介绍了可帮助你成功开发云的 web 应用的13种模式和实践。 有关电子书的信息，请参阅 [第一章](introduction.md)。

前三种模式是设置敏捷开发过程，其余部分就是体系结构和代码。 这是 web 开发最佳实践的集合：

- 智能负载均衡器后的[无状态 web 服务器](#stateless)。
- [避免会话状态](#sessionstate) (或如果无法避免，则使用分布式缓存，而不是数据库) 。
- [使用 CDN](#cdn) 将静态文件资产 (映像、脚本) 进行边缘缓存。
- [使用 .net 4.5 的异步支持](#async) 来避免阻止调用。

这些做法对所有 web 开发都有效，而不仅仅适用于云应用程序，但对于云应用尤其重要。 它们协同工作，帮助你充分利用云环境提供的高度灵活的缩放。 如果不遵循这些做法，则在尝试扩展应用程序时，将会遇到限制。

<a id="stateless"></a>
## <a name="stateless-web-tier-behind-a-smart-load-balancer"></a>智能负载均衡器后的无状态 web 层

*无状态 web 层* 意味着不会将任何应用程序数据存储在 web 服务器内存或文件系统中。 使您的 web 层保持无状态，可以提供更好的客户体验并节省资金：

- 如果 web 层是无状态的，并且它位于负载均衡器后面，则可以通过动态添加或删除服务器来快速响应应用程序流量中的更改。 在你只需为服务器资源付费的云环境中，只要你实际使用这些资源，就可以对需求的更改进行响应，从而大大节省成本。
- 无状态的 web 层在体系结构上扩展应用程序的规模更简单。 这还使您能够更快地响应缩放需求，并花费更少的时间来处理过程中的开发和测试工作。
- 与本地服务器一样，云服务器需要进行修补并偶尔重新启动;如果 web 层是无状态的，则当服务器暂时停机时，重新路由流量不会导致错误或意外行为。

大多数实际应用程序都需要为 web 会话存储状态;此处的要点不是将它存储在 web 服务器上。 可以通过其他方式（例如，在 cookie 中的客户端或在 ASP.NET 会话状态下使用缓存提供程序的进程外服务器端）来存储状态。 你可以将文件存储在 [Microsoft Azure Blob 存储](unstructured-blob-storage.md) 中，而不是存储在本地文件系统中。

例如，如果你的 Web 层是无状态的，则在 Windows Azure 网站中缩放应用程序的方法会很简单，请在管理门户中查看 Microsoft Azure 网站的 " **缩放** " 选项卡：

![“缩放”选项卡](web-development-best-practices/_static/image1.png)

如果要添加 web 服务器，只需将 "实例计数" 滑块拖到右侧即可。 将其设置为5并单击 " **保存**"，在几秒内，Windows Azure 中的5个 web 服务器处理你的网站的流量。

![五个实例](web-development-best-practices/_static/image2.png)

可以轻松地将实例计数向下设置为3，或将其向下重新设置为1。 当你向后缩放时，将立即开始节省资金，因为 Windows Azure 会按分钟而不是按小时收费。

你还可以告诉 Windows Azure 根据 CPU 使用率自动增加或减少 web 服务器的数量。 在下面的示例中，当 CPU 使用率低于60% 时，web 服务器数将减少到最小2个，如果 CPU 使用率超过80%，则 web 服务器数将增加到最大值4。

![按 CPU 使用率缩放](web-development-best-practices/_static/image3.png)

或者，如果您知道您的网站在工作时间内只是繁忙吗？ 你可以让 Microsoft Azure 在白天运行多个服务器，并将其减少到单台服务器的夜晚、夜晚和周末。 以下一系列屏幕截图显示了如何将网站设置为在工作时间（从上午8点到下午5点）的工作时间内运行一台服务器。

![按计划缩放](web-development-best-practices/_static/image4.png)

![设置计划时间](web-development-best-practices/_static/image5.png)

![日间计划](web-development-best-practices/_static/image6.png)

![Weeknight 计划](web-development-best-practices/_static/image7.png)

![周末计划](web-development-best-practices/_static/image8.png)

当然，所有这些都可以在脚本和门户中完成。

在 Windows Azure 中，应用程序的横向扩展功能几乎不受限制，只要你通过使 web 层保持无状态来避免障碍动态添加或删除服务器 Vm。

<a id="sessionstate"></a>
## <a name="avoid-session-state"></a>避免会话状态

在实际云应用中避免存储某种形式的用户会话状态通常是不现实的，但某些方法相比其他方法而言，对性能和可伸缩性的影响更大。 如果需要存储状态，最佳解决方案是使状态量保持较小并将其存储在 Cookie 中。 如果这不可行，下一个最佳解决方案是将 ASP.NET 会话状态与提供程序配合使用 [，以便使用分布式的内存中缓存](distributed-caching.md#sessionstate)。 从性能和可伸缩性的角度来看，最差的解决方案是使用数据库支持的会话状态提供程序。

<a id="cdn"></a>
## <a name="use-a-cdn-to-cache-static-file-assets"></a>使用 CDN 缓存静态文件资产

CDN 是内容交付网络的首字母缩写词。 你向 CDN 提供程序提供静态文件资产（如图像和脚本文件），提供程序将这些文件缓存在世界各地的数据中心，以便在任何位置访问你的应用程序时，他们获得缓存资产的相对快速响应和低延迟。 这会加快站点的总体加载时间，并减少 web 服务器上的负载。 如果您要访问遍布各地的受众，Cdn 尤其重要。

Windows Azure 具有 CDN，你可以在 Windows Azure 中运行的应用程序或任何 web 宿主环境中使用其他 Cdn。

<a id="async"></a>
## <a name="use-net-45s-async-support-to-avoid-blocking-calls"></a>使用 .NET 4.5 的异步支持来避免阻塞调用

.NET 4.5 增强了 c # 和 VB 编程语言，使其更易于异步处理任务。 异步编程的优点不仅适用于并行处理的情况，例如，当你想要同时启动多个 web 服务调用时。 它还使 web 服务器能够在高负载条件下更有效、更可靠。 Web 服务器仅具有有限数量的可用线程，并且在高负载条件下，如果所有线程都在使用中，则传入的请求必须等待，直到释放线程。 如果你的应用程序代码不会以异步方式处理数据库查询和 web 服务调用等任务，则当服务器正在等待 i/o 响应时，很多线程将无法进行连接。 这会限制服务器在高负载情况下可以处理的流量量。 使用异步编程时，等待 web 服务或数据库返回数据的线程会被释放，以便在接收到的数据之前为新请求提供服务。 在繁忙的 web 服务器中，可以立即处理数百个或数千个请求，否则将会等待释放线程。

正如您前面所看到的那样，减少处理您的网站的 web 服务器的数量就变得非常简单。 因此，如果服务器可以获得更高的吞吐量，则不需要使用它们，并且可以降低开销，因为给定流量卷所需的服务器数比其他情况下更少。

针对 Web 窗体、MVC 和 Web API 的 ASP.NET 4.5 中包含对 .NET 4.5 异步编程模型的支持;在实体框架6中，在 [Windows Azure 存储 API](https://blogs.msdn.com/b/windowsazurestorage/archive/2013/07/12/introducing-storage-client-library-2-1-rc-for-net-and-windows-phone-8.aspx)中为。

### <a name="async-support-in-aspnet-45"></a>ASP.NET 4.5 中的异步支持

在 ASP.NET 4.5 中，对异步编程的支持不仅添加到语言，还添加到 MVC、Web 窗体和 Web API 框架。 例如，ASP.NET MVC 控制器操作方法接收来自 web 请求的数据，并将数据传递到一个视图，该视图随后会创建要发送到浏览器的 HTML。 操作方法通常需要从数据库或 web 服务获取数据，以便在网页中显示数据或保存在网页中输入的数据。 在这些情况下，可以轻松地将操作方法设为异步：返回*Task &lt; ActionResult &gt; *并使用*async*关键字标记该方法，而不是返回*ActionResult*对象。 在方法中，当代码行发出的操作涉及到等待时间时，你可以使用 await 关键字标记它。

下面是一个简单的操作方法，它为数据库查询调用存储库方法：

[!code-csharp[Main](web-development-best-practices/samples/sample1.cs)]

下面是异步处理数据库调用的相同方法：

[!code-csharp[Main](web-development-best-practices/samples/sample2.cs?highlight=1,4)]

在中，编译器将生成相应的异步代码。 当应用程序对进行调用时 `FindTaskByIdAsync` ，ASP.NET 将发出 `FindTask` 请求，然后展开工作线程，并使其可用于处理其他请求。 `FindTask`请求完成后，将重新启动一个线程以继续处理该调用之后发出的代码。 在 `FindTask` 启动请求和返回数据之间过渡的过程中，有一个线程可用于执行有用的工作，否则会将其绑定到等待响应。

对于异步代码存在一些开销，但在低负载情况下，这种开销可忽略不计，而在高负载情况下，你可以处理请求，否则将保留等待可用线程。

从 ASP.NET 1.1 开始，可以进行这种类型的异步编程，但难以编写、容易出错且难以调试。 现在，我们已在 ASP.NET 4.5 中为其简化了编码，因此没有理由再这样做。

### <a name="async-support-in-entity-framework-6"></a>实体框架6中的异步支持

作为4.5 的异步支持的一部分，我们提供了对 web 服务调用、套接字和文件系统 i/o 的异步支持，但最常见的 web 应用程序模式是命中数据库，我们的数据库不支持 async。 现在实体框架6添加了对数据库访问的异步支持。

在实体框架6中，导致将查询或命令发送到数据库的所有方法都具有异步版本。 此处的示例显示了 *Find* 方法的异步版本。

[!code-csharp[Main](web-development-best-practices/samples/sample3.cs?highlight=8)]

此异步支持不仅适用于插入、删除、更新和简单查找，它还适用于 LINQ 查询：

[!code-csharp[Main](web-development-best-practices/samples/sample4.cs?highlight=7,10)]

存在方法的 `Async` 版本， `ToList` 因为在此代码中，这是导致查询发送到数据库的方法。 `Where`和 `OrderByDescending` 方法仅配置查询，而 `ToListAsync` 方法执行查询，并将响应存储在 `result` 变量中。

## <a name="summary"></a>总结

你可以在任何 web 编程框架和任何云环境中实现此处所述的 web 开发最佳做法，但我们在 ASP.NET 和 Microsoft Azure 中提供了一些工具来使其变得简单。 如果遵循这些模式，则可以轻松地横向扩展 web 层，并最大限度地减少支出，因为每个服务器都能处理更多流量。

[下一章](single-sign-on.md)将介绍云如何启用单一登录方案。

## <a name="resources"></a>资源

有关详细信息，请参阅以下资源。

无状态 web 服务器：

- [Microsoft 模式和实践-自动缩放指南](https://msdn.microsoft.com/library/dn589774.aspx)。
- [在 Microsoft Azure 网站中禁用 ARR 的实例关联](https://azure.microsoft.com/blog/2013/11/18/disabling-arrs-instance-affinity-in-windows-azure-web-sites/)。 Erez Benari 的博客文章介绍了 Microsoft Azure 网站中的会话相关性。

CDN

- [故障安全：构建可缩放且可复原的云服务](https://channel9.msdn.com/Series/FailSafe)。 九部分视频系列： Ulrich Homann、Marc Mercuri 和 Mark Simm。 请参阅从1:34:00 开始的剧集3中的 CDN 讨论。
- [Microsoft 模式和实践静态内容托管模式](https://msdn.microsoft.com/library/dn589776.aspx)
- [CDN 审查](http://www.cdnreviews.com/)。 许多 Cdn 的概述。

异步编程：

- [在 ASP.NET MVC 4 中使用异步方法](../../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md)。 通过 Rick Anderson 教程。
- [采用 Async 和 Await 的异步编程 (c # 和 Visual Basic) ](https://msdn.microsoft.com/library/vstudio/hh191443.aspx)。 MSDN 白皮书，介绍异步编程的基本原理、它在 ASP.NET 4.5 中的工作原理，以及如何编写代码以实现它。
- [实体框架异步查询并保存](https://msdn.microsoft.com/data/jj819165)
- [如何使用 Async 构建 ASP.NET Web 应用程序](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2013/DEV-B337#fbid=tgkT4SR_DK7)。 Rowan 莎莎的视频演示。 提供了一个图形演示，说明在高负载条件下，异步编程如何有助于大幅增加 web 服务器吞吐量。
- [故障安全：构建可缩放且可复原的云服务](https://channel9.msdn.com/Series/FailSafe)。 九部分视频系列： Ulrich Homann、Marc Mercuri 和 Mark Simm。 有关异步编程对可伸缩性的影响的讨论，请参阅剧集4和剧集8。
- [使用 ASP.NET 4.5 中的异步方法和重要的难点的神奇之处](http://www.hanselman.com/blog/TheMagicOfUsingAsynchronousMethodsInASPNET45PlusAnImportantGotcha.aspx)。 Scott Hanselman 的博客文章，主要介绍了如何在 ASP.NET Web 窗体应用程序中使用 async。

有关其他 web 开发最佳做法，请参阅以下资源：

- [解决该问题的示例是应用程序的最佳做法](the-fix-it-sample-application.md#bestpractices)。 本电子书的附录列出了一些在 Fix It 应用程序中实现的最佳实践。
- [Web 开发人员清单](http://webdevchecklist.com/asp.net)

> [!div class="step-by-step"]
> [上一页](continuous-integration-and-continuous-delivery.md)
> [下一页](single-sign-on.md)

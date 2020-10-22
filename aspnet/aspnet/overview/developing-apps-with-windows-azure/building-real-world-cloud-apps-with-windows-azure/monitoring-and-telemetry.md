---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry
title: 通过 Azure) 生成 Real-World 云应用的监视和遥测 (|Microsoft Docs
author: MikeWasson
description: 使用 Azure 电子书构建真实的云应用基于 Scott Guthrie 开发的演示文稿。 它介绍了13种模式和实践，
ms.author: riande
ms.date: 07/09/2015
ms.assetid: 7e986ab5-6615-4638-add7-4614ce7b51db
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry
msc.type: authoredcontent
ms.openlocfilehash: f61810ea7b486b2fa0bbb234edea7541eedde835
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345572"
---
# <a name="monitoring-and-telemetry-building-real-world-cloud-apps-with-azure"></a>通过 Azure) 生成 Real-World 云应用的监视和遥测 (

作者： [Mike Wasson](https://github.com/MikeWasson)， [Rick Anderson](https://twitter.com/RickAndMSFT)， [Tom Dykstra](https://github.com/tdykstra)

[下载 Fix It 项目](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) 或 [下载电子书](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> **使用 Azure 电子书构建真实的云应用**基于 Scott Guthrie 开发的演示文稿。 它介绍了可帮助你成功开发云的 web 应用的13种模式和实践。 有关电子书的信息，请参阅 [第一章](introduction.md)。

许多人都依靠客户在其应用程序关闭时通知他们。 这并不是在任何地方都是最佳实践，尤其是在云中。 不能保证快速通知，并且在您收到通知时，您通常会获得有关发生的情况的最小或误导性数据。 使用良好的遥测和日志记录系统，你可以了解应用程序的进展情况，当发生问题时，你可以立即查明并提供有用的故障排除信息。

## <a name="buy-or-rent-a-telemetry-solution"></a>购买或出租遥测解决方案

> [!NOTE]
> 本文是在 [Application Insights](/azure/application-insights/app-insights-overview) 发布之前编写的。 Application Insights 是 Azure 上的遥测解决方案的首选方法。 有关详细信息，请参阅 [设置 ASP.NET 网站 Application Insights](/azure/application-insights/app-insights-asp-net) 。

云环境的优点之一就是可以很容易地购买或租借您的取胜方式。 遥测是一个示例。 如果没有太多的工作量，您可以非常经济高效地启动并运行非常好的遥测系统。 有很多与 Azure 集成的优秀合作伙伴，其中一些合作伙伴具有免费层–因此，无需获得基本的遥测数据。 下面只是 Azure 中当前可用的几个：

- [New Relic](http://newrelic.com/)
- [AppDynamics](http://www.appdynamics.com/)
- [Dynatrace](https://datamarket.azure.com/application/b4011de2-1212-4375-9211-e882766121ff)

[Microsoft System Center](http://www.petri.co.il/microsoft-system-center-introduction.htm#) 还包括监视功能。

我们将快速演练如何设置新的 Relic，以显示使用遥测系统的难易程度。

在 Azure 管理门户中，注册服务。 单击 " **新建**"，然后单击 " **应用商店**"。 此时将显示 " **选择外接程序** " 对话框。 向下滚动并单击 " **新 Relic**"。

![选择外接程序](monitoring-and-telemetry/_static/image1.png)

单击向右箭头，然后选择所需的服务层。 对于此演示，我们将使用免费层。

![个性化外接程序](monitoring-and-telemetry/_static/image2.png)

单击右箭头，确认 "购买"，新 Relic 现在显示为门户中的外接程序。

![查看购买](monitoring-and-telemetry/_static/image3.png)

![管理门户中的新 Relic 外接程序](monitoring-and-telemetry/_static/image4.png)

单击 " **连接信息**"，然后复制许可证密钥。

![连接信息](monitoring-and-telemetry/_static/image5.png)

在门户中转到 web 应用的 " **配置** " 选项卡，将 " **性能监视** " 设置为 " **外接程序**"，并将 " **选择外接程序** " 下拉列表设置为 " **新 Relic**"。 然后单击“保存”  。

!["配置" 选项卡中的新 Relic](monitoring-and-telemetry/_static/image6.png)

在 Visual Studio 中，在你的应用程序中安装新的 Relic NuGet 包。

!["配置" 选项卡中的开发人员分析](monitoring-and-telemetry/_static/image7.png)

将应用部署到 Azure 并开始使用它。 创建一些 Fix It 任务，为新的 Relic 提供一些活动来监视。

然后返回门户的 "**外接程序**" 选项卡中的 "**新 Relic** " 页，并单击 "**管理**"。 门户会使用单一登录进行身份验证，将你发送到新的 Relic 管理门户，因此你无需再次输入凭据。 "概述" 页提供各种性能统计信息。  (单击图像以查看 "概述" 页的完整大小。 ) 

[![新的 Relic 监视选项卡](monitoring-and-telemetry/_static/image9.png)](monitoring-and-telemetry/_static/image8.png)

下面只是几个可以看到的统计信息：

- 当天不同时间的平均响应时间。

    ![响应时间](monitoring-and-telemetry/_static/image10.png)
- 每分钟请求 (的吞吐量速率) 在一天的不同时间。

    ![吞吐量](monitoring-and-telemetry/_static/image11.png)
- 处理不同 HTTP 请求所用的服务器 CPU 时间。

    ![Web 事务时间](monitoring-and-telemetry/_static/image12.png)
- 在应用程序代码的不同部分中花费的 CPU 时间：

    ![跟踪详细信息](monitoring-and-telemetry/_static/image13.png)
- 历史性能统计信息。

    ![历史性能](monitoring-and-telemetry/_static/image14.png)
- 对外部服务的调用，例如 Blob 服务和有关服务的可靠性和响应能力的统计信息。

    ![外部服务](monitoring-and-telemetry/_static/image15.png)

    ![外部服务](monitoring-and-telemetry/_static/image16.png)

    ![外部服务](monitoring-and-telemetry/_static/image17.png)
- 有关世界上或在美国 web 应用流量中的位置的信息。

    ![地理位置](monitoring-and-telemetry/_static/image18.png)

您还可以设置报表和事件。 例如，你可以在任何时候开始看到错误，发送一封电子邮件以通知支持人员解决问题。

![报表](monitoring-and-telemetry/_static/image19.png)

新 Relic 只是遥测系统的一个示例;您也可以从其他服务获取所有这些。 云的优点是，无需编写任何代码，只需极少或无需支付费用，就可以很好地了解应用程序的使用情况以及客户实际遇到的情况。

<a id="log"></a>
## <a name="log-for-insight"></a>了解日志

遥测包是一个很好的第一步，但你仍需要检测自己的代码。 遥测服务会在出现问题时通知你，并告诉你客户遇到的问题，但它可能不会向你深入了解代码中的内容。

您不希望远程进入生产服务器来查看您的应用程序正在执行的操作。 这在您有一台服务器时可能是可行的，但如果您扩展到数百台服务器，并不知道您需要远程加入哪些服务器，那该怎么办呢？ 日志记录应提供足够的信息，使你不必远程进入生产服务器来分析和调试问题。 你应记录足够的信息，以便你可以仅通过日志隔离问题。

### <a name="log-in-production"></a>记录生产

许多人只是在出现问题时才会在生产环境中启用跟踪。 这可能会导致你发现问题的时间与获取有用的故障排除信息的时间之间存在巨大的延迟。 而且，您获取的信息对于间歇错误可能并不有用。

对于存储成本较低的云环境，我们建议您始终在生产中保留日志记录。 这样，当发生错误时，您已经记录了这些错误，您可以使用历史数据来帮助您分析随时间推移或在不同时间定期发生的问题。 你可以自动执行清除过程以删除旧的日志，但你可能会发现设置此类进程的开销要比保留日志的开销更高。

与所需的所有信息在出现问题时都可以使用的信息相同，因此，日志记录的增加费用也很简单。 如果有人告诉您在过去的一天的某个时间大约为8:00，但他们不记得此错误，您可以随时了解问题所在。

每个月不到 $4，你可以保留最多 50 gb 的日志，并且日志记录的性能影响很简单，因为为了避免性能瓶颈，请确保日志记录库是异步的。

### <a name="differentiate-logs-that-inform-from-logs-that-require-action"></a>区分从需要操作的日志中通知的日志

日志旨在通知 (我想要知道) 还是行动 (希望您) 执行一些操作。 请注意只为真正需要人员或自动化过程采取措施的问题编写 ACT 日志。 太多的 ACT 日志会产生干扰，需要过多的工作才能通过它来确定真正的问题。 如果 ACT 日志会自动触发一些操作，例如将电子邮件发送给支持人员，请避免通过单个问题来触发上千个这样的操作。

在 .NET System 诊断跟踪中，可以为日志分配错误、警告、信息和调试/详细级别。 你可以通过保留 ACT 日志的错误级别并使用通知日志的较低级别来区分操作与通知日志。

![日志记录级别](monitoring-and-telemetry/_static/image20.png)

### <a name="configure-logging-levels-at-run-time"></a>在运行时配置日志记录级别

尽管有必要在生产中始终启用日志记录，但另一种最佳做法是实现日志记录框架，使你能够在运行时调整要记录的详细信息级别，而无需重新部署或重新启动应用程序。 例如，在中使用跟踪功能时， `System.Diagnostics` 可以创建错误、警告、信息和调试/详细日志。 建议你始终将错误、警告和信息日志记录在生产中，并且你希望能够动态地添加调试/详细日志记录，以便根据具体情况进行故障排除。

Azure App Service 中的 Web Apps 内置了对将日志写入 `System.Diagnostics` 文件系统、表存储或 Blob 存储的支持。 可以为每个存储目标选择不同的日志记录级别，并且可以动态更改日志记录级别，而无需重新启动应用程序。 Blob 存储支持使你可以更轻松地在应用程序日志中运行 [HDInsight](https://docs.microsoft.com/azure/hdinsight/) 分析作业，因为 HDInsight 知道如何直接处理 Blob 存储。

### <a name="log-exceptions"></a>记录异常

不要只是放置 *异常。ToString ( * 日志记录代码中的 # B1。 这会留下上下文信息。 在出现 SQL 错误的情况下，它会遗漏 SQL 错误号。 对于所有例外，都要包含上下文信息、例外本身和内部异常，以确保提供故障排除所需的所有内容。 例如，上下文信息可能包括服务器名称、事务标识符和用户名 (，但不包括密码或任何机密！ ) 。

如果你依赖于每个开发人员来执行异常日志记录的正确操作，则其中一些功能不会。 若要确保每次都能以正确的方式进行处理，请将异常处理直接生成到记录器接口：将异常对象本身传递到记录器类，并在记录器类中正确地记录异常数据。

### <a name="log-calls-to-services"></a>记录对服务的调用

我们强烈建议您在每次应用程序调用服务时都编写日志，无论是在数据库中还是在 REST API 或任何外部服务时都是如此。 包括在日志中，不仅表示成功或失败，还包括每个请求花费的时间。 在云环境中，通常会看到与慢速停机相关的问题，而不是完全中断。 通常需要10毫秒的内容可能突然开始花费一秒钟。 当有人告诉你应用程序速度缓慢时，你希望能够查看新的 Relic 或你拥有的任何遥测服务并验证其体验，然后你希望能够查看自己的日志，以详细了解其速度缓慢的原因。

### <a name="use-an-ilogger-interface"></a>使用 ILogger 接口

创建生产应用程序时，我们建议您创建一个简单的 *ILogger* 接口，并在其中粘贴一些方法。 这样一来，以后就可以轻松地更改日志记录实现，无需完成所有代码即可执行此操作。 我们可以在 `System.Diagnostics.Trace` 整个 Fix It 应用程序中使用类，但我们会将其用于实现 *ILogger*的日志记录类中的涵盖范围内，并且我们将在整个应用程序中进行 *ILogger* 方法调用。

这样一来，如果你希望使日志更丰富，则可以将替换 [`System.Diagnostics.Trace`](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio#apptracelogs) 为所需的任何日志记录机制。 例如，随着应用程序的增长，你可能会决定要使用更全面的日志记录包，如 [NLog](http://nlog-project.org/) 或 [企业库日志记录应用程序块](https://msdn.microsoft.com/library/dn440731(v=pandp.60).aspx)。  ([Log4Net](http://logging.apache.org/log4net/) 是另一个热门日志记录框架，但它不会执行异步日志记录。 ) 

使用框架（如 NLog）的一个可能原因是有助于将日志记录输出划分为单独的高容量和高值数据存储。 这有助于有效地存储大量通知数据，无需对其执行快速查询，同时保持对 ACT 数据的快速访问。

### <a name="semantic-logging"></a>语义日志记录

若要以相对新的方式生成可以生成更有用的诊断信息的日志记录，请参阅 [企业库语义日志记录应用程序块 (楼板) ](http://convective.wordpress.com/2013/08/12/semantic-logging-application-block-slab/)。 在 .NET 4.5 中，楼板使用 [Windows 的事件跟踪](https://msdn.microsoft.com/library/windows/desktop/bb968803.aspx) (ETW) 和 [EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) 支持，使您能够创建更多结构化和可查询的日志。 为您记录的每种类型的事件定义一种不同的方法，这使您能够自定义您编写的信息。 例如，若要记录 SQL 数据库错误，可以调用 `LogSQLDatabaseError` 方法。 对于这种类型的异常，您知道某个关键信息是错误号，因此您可以在方法签名中包含一个错误号参数，并将错误号记录为您编写的日志记录中的单独字段。 由于数字在单独的字段中，因此你可以根据 SQL 错误号来更轻松、更可靠地获取报表，而不是将错误号连接到消息字符串。

## <a name="logging-in-the-fix-it-app"></a>在 Fix It 应用中登录

### <a name="the-ilogger-interface"></a>ILogger 接口

下面是 Fix It 应用中的 *ILogger* 接口。

[!code-csharp[Main](monitoring-and-telemetry/samples/sample1.cs)]

这些方法使你能够以 *系统诊断*支持的相同四个级别写入日志。 TraceApi 方法用于记录与延迟有关的外部服务调用。 您还可以添加一组用于调试/详细级别的方法。

### <a name="the-logger-implementation-of-the-ilogger-interface"></a>ILogger 接口的记录器实现

接口的实现非常简单。 基本上只需调入标准的 *系统诊断* 方法。 以下代码片段显示了所有三个信息方法，其中一个是其他方法。

[!code-csharp[Main](monitoring-and-telemetry/samples/sample2.cs)]

### <a name="calling-the-ilogger-methods"></a>调用 ILogger 方法

每当 Fix It 应用中的代码捕获异常时，它都会调用 *ILogger* 方法来记录异常详细信息。 每次调用数据库、Blob 服务或 REST API 时，它会在调用前启动秒表，并在服务返回时停止秒表，并记录有关成功或失败的信息。

请注意，日志消息包括类名称和方法名称。 最好确保日志消息能识别应用程序代码中写入它们的部分。

[!code-csharp[Main](monitoring-and-telemetry/samples/sample3.cs?highlight=6,14,20-21,25)]

现在，在每次 Fix It 应用程序调用 SQL 数据库时，都可以看到调用、调用它的方法，以及所花费的时间。

![日志中的 SQL 数据库查询](monitoring-and-telemetry/_static/image21.png)

![](monitoring-and-telemetry/_static/image22.png)

如果浏览日志，可以看到数据库调用所用的时间是可变的。 此信息可能非常有用：因为应用会记录所有这些信息，因此你可以分析数据库服务在一段时间内的性能。 例如，服务的时间可能很快，但请求可能会失败，或者响应可能会在一天的特定时段减慢。

您可以对 Blob 服务执行相同的操作，每次应用程序上传一个新文件时，都有一个日志，您可以确切地了解上传每个文件所需的时间。

![Blob 上传日志](monitoring-and-telemetry/_static/image23.png)

只需编写几行代码，就可以在每次调用服务时编写代码，并在有人指出他们遇到的问题时，确切地了解问题是什么，无论是错误还是只是运行缓慢。 您可以查明问题的根源，而无需远程登录到服务器，也无需在错误发生后启用日志记录，希望重新创建。

## <a name="dependency-injection-in-the-fix-it-app"></a>Fix It 应用中的依赖关系注入

您可能想知道上述示例中的存储库构造函数如何获取记录器接口实现：

[!code-csharp[Main](monitoring-and-telemetry/samples/sample4.cs?highlight=6)]

若要将接口连接到实现，应用将使用 [依赖关系注入](http://en.wikipedia.org/wiki/Dependency_injection) (DI) 与 [AutoFac](http://autofac.org/)。 通过 DI，你可以在代码中的多个位置使用基于接口的对象，并且只需在一个位置指定在实例化接口时使用的实现。 这样可以更轻松地更改实现：例如，你可能想要将系统诊断记录器替换为 NLog 记录器。 对于自动测试，可能需要替换记录器的模拟版本。

Fix It 应用程序使用所有存储库和所有控制器中的 DI。 控制器类的构造函数获取 *ITaskRepository* 接口，与存储库获取记录器接口的方式相同：

[!code-csharp[Main](monitoring-and-telemetry/samples/sample5.cs?highlight=5)]

应用使用 AutoFac DI 库自动为这些构造函数提供 *TaskRepository* 和 *记录器* 实例。

[!code-csharp[Main](monitoring-and-telemetry/samples/sample6.cs?highlight=8,10)]

此代码基本上指出：构造函数需要 *ILogger* 接口，在 *记录器* 类的实例中传递，并在需要 *IFixItTaskRepository* 接口时传入 *FixItTaskRepository* 类的实例。

[AutoFac](http://autofac.org/) 是可使用的许多依赖项注入框架之一。 另一个常用的是 [Unity](https://blogs.msdn.com/b/agile/archive/2013/08/20/new-guide-dependency-injection-with-unity.aspx)，Microsoft 模式和实践建议并支持此方法。

## <a name="built-in-logging-support-in-azure"></a>Azure 中的内置日志记录支持

在 Azure App Service 中，Azure 支持以下类型的 [Web 应用日志记录](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio)：

- 诊断跟踪 (你可以打开和关闭，并在不重新启动站点) 的情况下动态设置级别。
- Windows 事件。
- IIS 日志 (HTTP/FREB) 。

Azure 支持 [云服务中](https://docs.microsoft.com/azure/cloud-services/cloud-services-dotnet-diagnostics)的以下类型的日志记录：

- 诊断跟踪。
- 性能计数器。
- Windows 事件。
- IIS 日志 (HTTP/FREB) 。
- 自定义目录监视。

Fix It 应用使用诊断跟踪。 若要在 web 应用中启用系统诊断日志记录，只需在门户中翻转开关或调用 REST API。 在门户中，单击站点的 " **配置** " 选项卡，然后向下滚动查看 " **应用程序诊断** " 部分。 可以打开或关闭日志记录，并选择所需的日志记录级别。 可以让 Azure 将日志写入文件系统或存储帐户。

!["配置" 选项卡中的应用诊断和站点诊断](monitoring-and-telemetry/_static/image24.png)

在 Azure 中启用日志记录后，可以在 Visual Studio 的 "输出" 窗口中查看日志。

![流式传输日志菜单](http://wacomdpsstorage.blob.core.windows.net/articlesmedia/content-ppe.windowsazure.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/20140115062810/tws-viewlogsmenu.png)

![流式传输日志菜单](http://wacomdpsstorage.blob.core.windows.net/articlesmedia/content-ppe.windowsazure.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/20140115062810/tws-nologsyet.png)

你还可以将日志写入你的存储帐户，并使用可以访问 Azure 存储表服务的任何工具查看日志，例如 Visual Studio 中的 **服务器资源管理器** 或 [Azure 存储资源管理器](https://azure.microsoft.com/features/storage-explorer/)。

![服务器资源管理器中的日志](http://wacomdpsstorage.blob.core.windows.net/articlesmedia/content-ppe.windowsazure.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/20140115062810/tws-storagelogs.png)

## <a name="summary"></a>总结

实现现成的遥测系统非常简单，可以在自己的代码中检测日志记录，并在 Azure 中配置日志记录。 当你有生产问题时，遥测系统和自定义日志的组合将有助于你快速解决问题，然后这些问题才会成为客户的重大问题。

[下一章](transient-fault-handling.md)介绍如何处理暂时性错误，使它们不会成为必须调查的生产问题。

## <a name="resources"></a>资源

有关详细信息，请参阅以下资源。

文档主要介绍遥测：

- [Microsoft 模式和实践-Azure 指南](https://msdn.microsoft.com/library/dn568099.aspx)。 请参阅检测和遥测指南、服务计量指南、运行状况终结点监视模式和运行时重新配置模式。
- [云中的收缩：在 Azure 网站上启用新的 Relic 性能监视](http://www.hanselman.com/blog/PennyPinchingInTheCloudEnablingNewRelicPerformanceMonitoringOnWindowsAzureWebsites.aspx)。
- [在 Azure 云服务上设计 Large-Scale 服务的最佳实践](https://msdn.microsoft.com/library/windowsazure/jj717232.aspx)。 通过标记 Simm 和 Michael Thomassy 的白皮书。 请参阅遥测和诊断部分。
- [下一代开发 Application Insights](https://msdn.microsoft.com/magazine/dn683794.aspx)。 MSDN 杂志文章。

文档主要介绍日志记录：

- [语义日志记录应用程序块 (楼板) ](http://convective.wordpress.com/2013/08/12/semantic-logging-application-block-slab/)。 Neil Mackenzie 介绍了如何通过楼板进行语义日志记录。
- [创建具有语义日志记录的结构化和有意义的日志](https://channel9.msdn.com/Events/Build/2013/3-336)。  (视频) Julian Dominguez 介绍了如何通过楼板进行语义日志记录。
- [EF6 SQL 日志记录-第1部分：简单日志记录](http://blog.oneunicorn.com/2013/05/08/ef6-sql-logging-part-1-simple-logging/)。 Arthur Vickers 演示了如何记录由 EF 6 中实体框架执行的查询。
- [ASP.NET MVC 应用程序中的实体框架的连接复原和命令截获](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application.md)。 第四个系列系列教程中的第四部分介绍了如何使用 EF 6 命令侦听功能记录通过实体框架发送到数据库的 SQL 命令。
- [使用 c # 5.0 调用方信息特性改进日志记录](http://www.dotnetcurry.com/showarticle.aspx?ID=972)。 如何轻松记录调用方法的名称，而无需将其硬编码为文本或使用反射手动获取它。

文档主要介绍故障排除：

- [Azure 故障排除 &amp; 调试博客](https://blogs.msdn.com/b/kwill/)。
- [AzureTools – Azure 开发人员支持团队使用的诊断实用程序](https://blogs.msdn.com/b/kwill/archive/2013/08/26/azuretools-the-diagnostic-utility-used-by-the-windows-azure-developer-support-team.aspx?Redirected=true)。 介绍并提供可用于在 Azure VM 上下载和运行各种诊断和监视工具的工具的下载链接。 需要诊断特定 VM 上的问题时，此方法非常有用。
- [使用 Visual Studio 对 Azure App Service 中的 web 应用进行故障排除](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio)。 有关如何开始使用诊断跟踪和远程调试的分步教程。

视频：

- [故障安全：构建可缩放且可复原的云服务](https://channel9.msdn.com/Series/FailSafe)。 九部分系列： Ulrich Homann、Marc Mercuri 和 Mark Simm。 以一种易于访问且有趣的方式展示高级概念和体系结构原则，其中的情景从 Microsoft 客户顾问团队那里提取 (CAT) 体验与真实客户。 剧集4和9用于监视和遥测数据。 剧集9包括监视服务 MetricsHub、AppDynamics、New Relic 和 PagerDuty 的概述。
- [构建大：从 Azure 客户获得的课程-第二部分](https://channel9.msdn.com/Events/Build/2012/3-030)。 标记 Simm 讨论了如何针对故障进行设计并检测所有内容。 与故障保护系列类似，但更详细地介绍了更多操作方法。

代码示例：

- [Azure 中的云服务基础知识](https://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649)。 Microsoft Azure 客户咨询团队创建的示例应用程序。 演示了遥测和日志记录做法，如以下文章中所述。 该示例使用 [NLog](http://nlog-project.org/)实现应用程序日志记录。 相关文档，请参阅 [有关遥测和日志记录的四个 TechNet wiki 文章系列](https://social.technet.microsoft.com/wiki/contents/articles/17987.cloud-service-fundamentals.aspx#Telemetry_coming_soon)。

> [!div class="step-by-step"]
> [上一页](design-to-survive-failures.md)
> [下一页](transient-fault-handling.md)

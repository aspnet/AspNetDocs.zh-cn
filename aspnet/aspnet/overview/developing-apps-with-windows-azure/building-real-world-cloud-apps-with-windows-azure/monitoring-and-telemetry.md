---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry
title: 监视和遥测（使用 Azure 构建真实世界云应用） |微软文档
author: MikeWasson
description: 使用 Azure 电子书构建真实世界云应用基于 Scott Guthrie 开发的演示文稿。 它解释了13种模式和做法，他可以...
ms.author: riande
ms.date: 07/09/2015
ms.assetid: 7e986ab5-6615-4638-add7-4614ce7b51db
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry
msc.type: authoredcontent
ms.openlocfilehash: f61810ea7b486b2fa0bbb234edea7541eedde835
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675669"
---
# <a name="monitoring-and-telemetry-building-real-world-cloud-apps-with-azure"></a>监视和遥测（使用 Azure 构建真实世界云应用）

由[迈克·瓦森](https://github.com/MikeWasson)，[里克·安德森](https://twitter.com/RickAndMSFT)，[汤姆·戴克斯特拉](https://github.com/tdykstra)

[下载修复它项目](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)或[下载电子书](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> 使用 Azure 电子书**构建真实世界云应用**基于 Scott Guthrie 开发的演示文稿。 它解释了 13 种模式和做法，这些模式和做法可以帮助您成功开发云的 Web 应用。 有关电子书的信息，请参阅[第一章](introduction.md)。

很多人依靠客户来让他们知道他们的应用程序何时关闭了。 这不是任何地方的最佳实践，尤其是在云中。 不能保证快速通知，当您收到通知时，您通常会收到关于所发生的事情的最小或误导性数据。 有了良好的遥测和日志记录系统，您可以了解应用发生的情况，当出现问题时，您可以马上发现并处理有用的故障排除信息。

## <a name="buy-or-rent-a-telemetry-solution"></a>购买或租用遥测解决方案

> [!NOTE]
> 本文是在[应用程序见解](/azure/application-insights/app-insights-overview)发布之前编写的。 应用程序见解是 Azure 上遥测解决方案的首选方法。 有关详细信息[，请参阅为ASP.NET网站设置应用程序见解](/azure/application-insights/app-insights-asp-net)。

云环境的伟大之一是，它真的很容易购买或租出你的方式的胜利。 遥测就是一个例子。 无需大量精力，即可获得一个非常好的遥测系统启动和运行，非常经济。 有一群伟大的合作伙伴与 Azure 集成，其中一些合作伙伴具有免费层，因此您可以免费获取基本遥测数据。 以下是 Azure 上当前可用的少数功能：

- [New Relic](http://newrelic.com/)
- [AppDynamics](http://www.appdynamics.com/)
- [Dynatrace](https://datamarket.azure.com/application/b4011de2-1212-4375-9211-e882766121ff)

[微软系统中心](http://www.petri.co.il/microsoft-system-center-introduction.htm#)还包括监控功能。

我们将快速完成设置新遗物，以显示使用遥测系统是多么容易。

在 Azure 管理门户中，注册该服务。 单击 **"新建**"，然后单击"**存储**"。 将显示"**选择加载项**"对话框。 向下滚动并单击 **"新遗物**"。

![选择加载项](monitoring-and-telemetry/_static/image1.png)

单击右箭头并选择所需的服务层。 对于此演示，我们将使用免费套餐。

![个性化加载项](monitoring-and-telemetry/_static/image2.png)

单击右箭头，确认"购买"，新遗物现在显示在门户中的加载项中。

![审核购买](monitoring-and-telemetry/_static/image3.png)

![管理门户中的新遗物加载项](monitoring-and-telemetry/_static/image4.png)

单击 **"连接信息**"并复制许可证密钥。

![连接信息](monitoring-and-telemetry/_static/image5.png)

转到门户中的 Web 应用的 **"配置**"选项卡，将**性能监视**设置为 **"加载项**"，并将 **"选择加载项**"下拉列表设置为 **"新建"。** 然后单击"**保存**"。

![配置选项卡中的新遗物](monitoring-and-telemetry/_static/image6.png)

在可视化工作室中，在应用中安装新的遗物 NuGet 包。

![配置选项卡中的开发人员分析](monitoring-and-telemetry/_static/image7.png)

将应用部署到 Azure 并开始使用它。 创建一些修复它的任务，以提供一些活动，为新遗物监视。

然后返回门户**的"加载项**"选项卡中的 **"新遗物**"页，然后单击"**管理**"。 门户使用单一登录进行身份验证，将您发送到新文物管理门户，这样您就不必再次输入凭据。 "概述"页提供了各种性能统计信息。 （单击图像可查看概览页面全尺寸。

[![新的遗物监视选项卡](monitoring-and-telemetry/_static/image9.png)](monitoring-and-telemetry/_static/image8.png)

以下是一些可以查看的统计信息：

- 一天中不同时间的平均响应时间。

    ![响应时间](monitoring-and-telemetry/_static/image10.png)
- 一天中不同时间（以每分钟请求）的吞吐量率。

    ![吞吐量](monitoring-and-telemetry/_static/image11.png)
- 服务器 CPU 时间用于处理不同的 HTTP 请求。

    ![Web 事务时间](monitoring-and-telemetry/_static/image12.png)
- 在应用程序代码的不同部分花费的 CPU 时间：

    ![跟踪详细信息](monitoring-and-telemetry/_static/image13.png)
- 历史绩效统计信息。

    ![历史表现](monitoring-and-telemetry/_static/image14.png)
- 对外部服务的调用，如 Blob 服务，以及有关服务的可靠性和响应速度的统计信息。

    ![外部服务](monitoring-and-telemetry/_static/image15.png)

    ![外部服务](monitoring-and-telemetry/_static/image16.png)

    ![外部服务](monitoring-and-telemetry/_static/image17.png)
- 有关世界或美国 Web 应用流量来自何处的信息。

    ![地理位置](monitoring-and-telemetry/_static/image18.png)

您还可以设置报表和事件。 例如，您可以说，每当您开始看到错误时，请发送电子邮件提醒支持人员注意问题。

![报表](monitoring-and-telemetry/_static/image19.png)

新遗迹只是遥测系统的一个示例;您也可以从其他服务获得所有这些。 云的优点是，无需编写任何代码，只需支付极少或无费用，您突然可以获得有关应用程序如何使用以及客户实际体验的更多信息。

<a id="log"></a>
## <a name="log-for-insight"></a>记录洞察

遥测包是很好的第一步，但您仍必须检测自己的代码。 遥测服务告诉您何时出现问题，并告诉您客户正在经历什么，但可能无法让您深入了解代码中发生的情况。

您不希望远程到生产服务器以查看应用正在执行的操作。 当您有一台服务器时，这可能很实用，但是，当您已扩展到数百台服务器，而您不知道需要远程插入哪些服务器时，该怎么办？ 日志记录应提供足够的信息，您永远不必远程到生产服务器来分析和调试问题。 您应该记录足够的信息，以便仅通过日志隔离问题。

### <a name="log-in-production"></a>登录生产

只有当出现问题并且想要调试时，许多人才会在生产中打开跟踪。 这可以在您意识到问题的时间与获取有关问题的有用故障排除信息之间引入大量延迟。 您获得的信息可能对间歇性错误没有帮助。

在存储成本低廉的云环境中，我们建议始终在生产中保留日志记录。 这样，当错误发生时，您已经记录了它们，并且您拥有的历史数据可以帮助您分析随时间而发展或在不同的时间定期发生的问题。 您可以自动执行清除过程以删除旧日志，但您可能会发现设置此类进程比保留日志的成本更高。

与故障发生时所需的所有信息可用，可以节省的故障排除时间和资金，日志记录的额外成本微不足道。 然后，当有人告诉你，他们昨晚8点左右有一个随机错误，但他们不记得错误，你可以很容易找出问题是什么。

每月不到 4 美元，您可以保留 50 GB 的日志，只要牢记一件事，日志记录的性能影响就微不足道了--为了避免性能瓶颈，请确保日志记录库是异步的。

### <a name="differentiate-logs-that-inform-from-logs-that-require-action"></a>区分通知需要操作的日志

日志是用来通知（我想让你知道一些事情）或ACT（我希望你做点什么）。 小心只编写 ACT 日志，以便真正需要人员或自动过程才能采取行动的问题。 太多的 ACT 日志会产生噪音，需要太多的工作来筛选所有日志，以找到真正的问题。 如果您的 ACT 日志自动触发一些操作，例如向支持人员发送电子邮件，请避免让数千个此类操作由单个问题触发。

在 .NET System.诊断跟踪中，可以为日志分配错误、警告、信息和调试/详细级别。 您可以通过为 ACT 日志保留错误级别并使用较低级别的 INFORM 日志来区分 ACT 和 INFORM 日志。

![日志记录级别](monitoring-and-telemetry/_static/image20.png)

### <a name="configure-logging-levels-at-run-time"></a>在运行时配置日志记录级别

虽然在生产中始终启用日志记录是值得的，但另一个最佳做法是实现日志记录框架，使您能够在运行时调整要记录的详细级别，而无需重新部署或重新启动应用程序。 例如，当您在 中使用`System.Diagnostics`中的跟踪工具时，可以创建错误、警告、信息和调试/详细日志。 我们建议您始终在生产中记录错误、警告和信息日志，并且希望能够动态添加调试/详细日志记录，以便逐案进行故障排除。

Azure 应用服务中的 Web 应用具有将日志写入`System.Diagnostics`文件系统、表存储或 Blob 存储的内置支持。 您可以为每个存储目标选择不同的日志记录级别，并且无需重新启动应用程序即可动态更改日志记录级别。 Blob 存储支持使在应用程序日志上运行[HDInsight](https://docs.microsoft.com/azure/hdinsight/)分析作业变得更加容易，因为 HDInsight 知道如何直接处理 Blob 存储。

### <a name="log-exceptions"></a>记录异常

不要只是把*例外。日志记录代码中的 ToString（）。* 这样就排除了上下文信息。 在 SQL 错误的情况下，它忽略了 SQL 错误编号。 对于所有异常，请包括上下文信息、异常本身和内部异常，以确保提供故障排除所需的一切。 例如，上下文信息可能包括服务器名称、事务标识符和用户名（但不包括密码或任何机密！

如果您依赖每个开发人员在异常日志记录中做正确的事情，其中一些则不会。 为了确保每次都以正确的方式完成，请直接在记录器接口中生成异常处理：将异常对象本身传递给记录器类，并在记录器类中正确记录异常数据。

### <a name="log-calls-to-services"></a>记录对服务的调用

我们强烈建议您在每次应用调用服务时编写日志，无论是数据库还是 REST API 或任何外部服务。 不仅在日志中包括成功或失败的指示，还包括每个请求需要多长时间。 在云环境中，您经常会看到与慢速相关的问题，而不是完全的中断。 通常需要 10 毫秒的东西可能会突然开始需要一秒钟。 当有人告诉您你的应用很慢时，您希望能够查看 New Relic 或任何您拥有的遥测服务并验证其体验，然后您希望能够查看您自己的日志，以深入了解其速度缓慢的原因。

### <a name="use-an-ilogger-interface"></a>使用 ILogger 界面

我们建议您在创建生产应用程序时创建一个简单的*ILogger*界面，并在其中输入一些方法。 这样以后可以轻松地更改日志记录实现，并且不必遍通所有代码即可完成。 我们可以在整个 Fix `System.Diagnostics.Trace` It 应用中使用该类，但我们在实现*ILogger*的日志记录类中使用它，并且在整个应用程序中进行*ILogger*方法调用。

这样，如果您希望使日志记录更丰富，则可以使用所需的任何日志记录机制进行替换[`System.Diagnostics.Trace`](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio#apptracelogs)。 例如，随着应用的增长，您可能决定要使用更全面的日志记录包，如[NLog](http://nlog-project.org/)或[企业库日志记录应用程序块](https://msdn.microsoft.com/library/dn440731(v=pandp.60).aspx)。 [（Log4Net](http://logging.apache.org/log4net/)是另一个流行的日志记录框架，但它不执行异步日志记录。

使用 NLog 等框架的一个可能原因是为了方便将日志记录输出划分为单独的大容量和高价值数据存储。 这有助于您高效地存储大量不需要执行快速查询的 INFORM 数据，同时保持对 ACT 数据的快速访问。

### <a name="semantic-logging"></a>语义日志记录

有关可以生成更多有用诊断信息的日志记录的较新方法，请参阅[企业库语义日志记录应用程序块 （SLAB）。](http://convective.wordpress.com/2013/08/12/semantic-logging-application-block-slab/) SLAB 使用 .NET 4.5 中的 Windows （ETW）[事件跟踪](https://msdn.microsoft.com/library/windows/desktop/bb968803.aspx)和[事件源](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx)支持来创建更结构化和可查询的日志。 您可以为记录的每种类型的事件定义不同的方法，从而使您能够自定义写入的信息。 例如，要记录 SQL 数据库错误，可以调用方法`LogSQLDatabaseError`。 对于此类异常，您知道关键信息是错误编号，因此您可以在方法签名中包含错误编号参数，并将错误编号记录为您编写的日志记录中的单独字段。 由于该数字位于单独的字段中，因此，如果将错误编号串联到消息字符串中，则可以比您更容易、更可靠地获取基于 SQL 错误数的报告。

## <a name="logging-in-the-fix-it-app"></a>登录修复它应用

### <a name="the-ilogger-interface"></a>ILogger 接口

这里是*ILogger*界面在修复它应用程序。

[!code-csharp[Main](monitoring-and-telemetry/samples/sample1.cs)]

这些方法使您能够在系统支持的四个级别上写入日志 *。* TraceApi 方法用于记录具有延迟信息的外部服务调用。 您还可以为调试/详细级别添加一组方法。

### <a name="the-logger-implementation-of-the-ilogger-interface"></a>ILogger 接口的记录器实现

接口的实现非常简单。 它基本上只是调用标准*系统。* 以下代码段显示所有三种信息方法以及每个方法。

[!code-csharp[Main](monitoring-and-telemetry/samples/sample2.cs)]

### <a name="calling-the-ilogger-methods"></a>调用 ILogger 方法

每次修复 It 应用中的代码捕获异常时，它都会调用*ILogger*方法来记录异常详细信息。 每次调用数据库、Blob 服务或 REST API 时，它都会在调用之前启动秒表，在服务返回时停止秒表，并记录已用的时间以及有关成功或失败的信息。

请注意，日志消息包括类名称和方法名称。 最好确保日志消息标识应用程序代码的哪一部分编写了它们。

[!code-csharp[Main](monitoring-and-telemetry/samples/sample3.cs?highlight=6,14,20-21,25)]

因此，现在每次修复它应用调用 SQL 数据库时，您都可以看到调用、调用它的方法以及它到底花了多长时间。

![日志中的 SQL 数据库查询](monitoring-and-telemetry/_static/image21.png)

![](monitoring-and-telemetry/_static/image22.png)

如果浏览日志，可以看到数据库调用所采用的时间是可变的。 这些信息可能很有用：因为应用会记录所有这些，因此您可以分析数据库服务随时间变化的性能的历史趋势。 例如，服务在大部分时间中可能速度很快，但请求可能会失败，或者响应在一天中的某些时间可能会变慢。

您可以为 Blob 服务执行相同的操作 - 每次应用上载新文件时，都有一个日志，并且您可以准确查看上载每个文件所花的时间。

![Blob 上传日志](monitoring-and-telemetry/_static/image23.png)

每次调用服务时，只需多写几行代码，现在每当有人说他们遇到问题时，您就会确切知道问题所在，无论是错误，还是运行速度很慢。 您可以精确定位问题的根源，而无需远程插入服务器或在错误发生后打开日志记录，并希望重新创建它。

## <a name="dependency-injection-in-the-fix-it-app"></a>修复它应用中的依赖项注入

您可能想知道上面所示示例中的存储库构造函数如何获取记录器接口实现：

[!code-csharp[Main](monitoring-and-telemetry/samples/sample4.cs?highlight=6)]

要将接口连接到实现，应用程序使用[依赖项注入](http://en.wikipedia.org/wiki/Dependency_injection)（DI） 与[AutoFac](http://autofac.org/)。 DI 使您能够在整个代码的许多地方使用基于接口的对象，并且只需在一个位置指定在实例化接口时使用的实现。 这使得更改实现变得更加容易：例如，您可能希望将 System. 诊断记录器替换为 NLog 记录器。 或者对于自动测试，您可能需要替换记录器的模拟版本。

修复 It 应用程序在所有存储库和所有控制器中使用 DI。 控制器类的构造函数获取*ITaskRepository*接口的方式与存储库获取记录器接口的方式相同：

[!code-csharp[Main](monitoring-and-telemetry/samples/sample5.cs?highlight=5)]

该应用程序使用 AutoFac DI 库自动为这些构造函数提供*任务存储库*和*记录器*实例。

[!code-csharp[Main](monitoring-and-telemetry/samples/sample6.cs?highlight=8,10)]

此代码基本上表示，无论构造函数需要*ILogger*接口，在*记录器*类的实例中传递，每当它需要*IFixItTaskRepository*接口时，都会在*FixItTaskRepository*类的实例中传递。

[AutoFac](http://autofac.org/)是您可以使用的许多依赖项注入框架之一。 另一个受欢迎的是[Unity，](https://blogs.msdn.com/b/agile/archive/2013/08/20/new-guide-dependency-injection-with-unity.aspx)这是由微软模式和实践推荐和支持。

## <a name="built-in-logging-support-in-azure"></a>Azure 中的内置日志记录支持

Azure 支持 Azure[应用服务中的 Web 应用](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio)的以下类型的日志记录：

- 系统.诊断跟踪（您可以打开和关闭，并在不重新启动站点的情况下动态设置级别）。
- 窗口事件。
- IIS 日志 （HTTP/FREB）。

Azure 支持[云服务中的](https://docs.microsoft.com/azure/cloud-services/cloud-services-dotnet-diagnostics)以下类型的日志记录：

- 系统.诊断跟踪。
- 性能计数器。
- 窗口事件。
- IIS 日志 （HTTP/FREB）。
- 自定义目录监视。

修复它应用使用系统.诊断跟踪。 在 Web 应用中进行诊断日志记录只需在门户中翻转交换机或调用 REST API。" 在门户中，单击网站的 **"配置"** 选项卡，然后向下滚动以查看 **"应用程序诊断**"部分。 您可以打开或关闭日志记录，并选择所需的日志记录级别。 可以让 Azure 将日志写入文件系统或存储帐户。

!["配置"选项卡中的应用诊断和站点诊断](monitoring-and-telemetry/_static/image24.png)

在 Azure 中启用日志记录后，可以在可视化工作室输出窗口中看到日志的创建。

![流日志菜单](http://wacomdpsstorage.blob.core.windows.net/articlesmedia/content-ppe.windowsazure.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/20140115062810/tws-viewlogsmenu.png)

![流日志菜单](http://wacomdpsstorage.blob.core.windows.net/articlesmedia/content-ppe.windowsazure.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/20140115062810/tws-nologsyet.png)

您还可以将日志写入存储帐户，并使用可以访问 Azure 存储表服务的任何工具（如可视化工作室中的**服务器资源管理器**或[Azure 存储资源管理器](https://azure.microsoft.com/features/storage-explorer/)）查看日志。

![服务器资源管理器中的日志](http://wacomdpsstorage.blob.core.windows.net/articlesmedia/content-ppe.windowsazure.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/20140115062810/tws-storagelogs.png)

## <a name="summary"></a>总结

实现开箱即用的遥测系统、在您自己的代码中记录仪器并在 Azure 中配置日志记录非常简单。 当您遇到生产问题时，遥测系统和自定义日志的组合将帮助您快速解决问题，以免它们成为客户的主要问题。

[在下一章](transient-fault-handling.md)中，我们将介绍如何处理瞬态错误，以便它们不会成为您必须调查的生产问题。

## <a name="resources"></a>资源

有关详细信息，请参阅以下资源。

主要有关遥测的文档：

- [微软模式和实践 - Azure 指南](https://msdn.microsoft.com/library/dn568099.aspx)。 请参阅检测和遥测指南、服务计量指导、运行状况终结点监视模式和运行时重新配置模式。
- [云中的彭妮捏合：在 Azure 网站上启用新的遗物性能监视](http://www.hanselman.com/blog/PennyPinchingInTheCloudEnablingNewRelicPerformanceMonitoringOnWindowsAzureWebsites.aspx)。
- [Azure 云服务上大规模服务设计的最佳做法](https://msdn.microsoft.com/library/windowsazure/jj717232.aspx)。 马克·西姆斯和迈克尔·托马斯的白皮书。 请参阅遥测和诊断部分。
- [具有应用程序见解的下一代开发](https://msdn.microsoft.com/magazine/dn683794.aspx)。 MSDN 杂志文章。

主要有关日志记录的文档：

- [语义日志记录应用程序块 （SLAB）](http://convective.wordpress.com/2013/08/12/semantic-logging-application-block-slab/). 尼尔·麦肯齐介绍了使用SLAB进行语义日志记录的情况。
- [使用语义日志记录创建结构化和有意义的日志](https://channel9.msdn.com/Events/Build/2013/3-336)。 （视频）朱利安·多明格斯介绍了使用SLAB进行语义日志记录的情况。
- [EF6 SQL 日志记录 = 第 1 部分：简单日志记录](http://blog.oneunicorn.com/2013/05/08/ef6-sql-logging-part-1-simple-logging/)。 Arthur Vickers 演示如何记录在 EF 6 中实体框架执行的查询。
- [在 ASP.NETmVC应用程序中，与实体框架的连接恢复能力和命令拦截](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application.md)。 在由九部分组成的教程系列中，第四部分演示了如何使用 EF 6 命令拦截功能来记录实体框架发送到数据库的 SQL 命令。
- [使用 C# 5.0 调用方信息属性改进日志记录](http://www.dotnetcurry.com/showarticle.aspx?ID=972)。 如何轻松地将调用方法的名称记录到文本中，而无需将其硬编码为文本或使用反射来手动获取它。

主要有关故障排除的文档：

- [Azure 故障排除&amp;调试博客](https://blogs.msdn.com/b/kwill/)。
- [Azure 工具 – Azure 开发人员支持团队使用的诊断实用程序](https://blogs.msdn.com/b/kwill/archive/2013/08/26/azuretools-the-diagnostic-utility-used-by-the-windows-azure-developer-support-team.aspx?Redirected=true)。 介绍并提供可用于 Azure VM 以下载和运行各种诊断和监视工具的工具的下载链接。 当您需要诊断特定 VM 上的问题时非常有用。
- [使用可视化工作室在 Azure 应用服务中排除 Web 应用故障](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio)。 用于开始使用 System.诊断跟踪和远程调试的分步教程。

视频：

- [故障安全：构建可扩展的、有弹性的云服务](https://channel9.msdn.com/Series/FailSafe)。 由乌尔里希·霍曼、马克·默库里和马克·西姆斯的九集系列。 以一种非常易访问和有趣的方式展示高级概念和架构原则，从 Microsoft 客户咨询团队 （CAT） 与实际客户的经验中得出的故事。 第 4 和第 9 集是关于监视和遥测的。 第 9 集包括监控服务 MetricsHub、AppDynamics、新遗物和寻呼业务概述。
- [构建大：从 Azure 客户那里吸取的经验教训 - 第二部分](https://channel9.msdn.com/Events/Build/2012/3-030)。 马克·西姆斯谈论为故障设计和检测一切。 类似于故障安全系列，但进入更多如何使用的详细信息。

代码示例：

- [Azure 中的云服务基础知识](https://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649)。 由 Microsoft Azure 客户咨询团队创建的示例应用程序。 演示遥测和日志记录实践，如以下文章中所述。 该示例使用[NLog](http://nlog-project.org/)实现应用程序日志记录。 有关相关文档，请参阅[有关遥测和日志记录的四个 TechNet wiki 文章系列](https://social.technet.microsoft.com/wiki/contents/articles/17987.cloud-service-fundamentals.aspx#Telemetry_coming_soon)。

> [!div class="step-by-step"]
> [上一页](design-to-survive-failures.md)
> [下一页](transient-fault-handling.md)

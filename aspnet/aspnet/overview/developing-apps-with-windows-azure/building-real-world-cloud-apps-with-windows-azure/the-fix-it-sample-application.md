---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/the-fix-it-sample-application
title: 附录： 修复它示例应用程序（使用 Azure 构建真实世界的云应用程序） |微软文档
author: MikeWasson
description: 使用 Azure 电子书构建真实世界云应用基于 Scott Guthrie 开发的演示文稿。 它解释了13种模式和做法，他可以...
ms.author: riande
ms.date: 06/12/2014
ms.assetid: 1bc333c5-f096-4ea7-b170-779accc21c1a
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/the-fix-it-sample-application
msc.type: authoredcontent
ms.openlocfilehash: 896196bdb6a6b0d12a6c798ead510e37dd38a9fc
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675633"
---
# <a name="appendix-the-fix-it-sample-application-building-real-world-cloud-apps-with-azure"></a>附录：修复它示例应用程序（使用 Azure 构建真实世界的云应用程序）

由[迈克·瓦森](https://github.com/MikeWasson)，[里克·安德森](https://twitter.com/RickAndMSFT)，[汤姆·戴克斯特拉](https://github.com/tdykstra)

[下载修复它项目](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)

> 使用 Azure 电子书**构建真实世界云应用**基于 Scott Guthrie 开发的演示文稿。 它解释了 13 种模式和做法，这些模式和做法可以帮助您成功开发云的 Web 应用。 有关电子书的信息，请参阅[第一章](introduction.md)。

使用 Azure 电子书构建真实世界云应用的此附录包含以下部分，这些部分提供有关"修复它"示例应用程序的其他信息，您可以下载：

- [已知问题](#knownissues)
- [最佳做法](#bestpractices)
- [如何从本地计算机上的 Visual Studio 运行应用](#run-in-vs)
- [如何使用 Windows PowerShell 脚本将基本应用部署到 Azure 应用服务 Web 应用](#deploybase)
- [对 Windows 电源外壳脚本进行故障排除](#troubleshooting)
- [如何将具有队列处理的应用部署到 Azure 应用服务 Web 应用和 Azure 云服务](#deployqueues)

<a id="knownissues"></a>
## <a name="known-issues"></a>已知问题

Fix It 应用程序最初是为了尽可能简单地说明本电子书中介绍的一些模式而开发的。 但是，由于电子书是关于构建真实世界的应用程序，因此我们进行了修复 It 代码的审核和测试过程，类似于我们为发布软件所做的操作。 我们发现了一些问题，与任何实际应用程序一样，我们修复了其中一些问题，其中一些问题被推迟到以后的版本中。

以下列表包括应在生产应用程序中解决的问题，但由于以下原因，我们决定在 Fix It 示例应用程序的初始版本中不解决。

### <a name="security"></a>安全性

- 确保无法将任务分配给不存在的所有者。
- 确保只能查看和修改您创建或分配给您的任务。
- 将 HTTPS 用于登录页面和身份验证 Cookie。
- 指定身份验证 Cookie 的时间限制。

### <a name="input-validation"></a>输入验证

通常，生产应用执行比修复它应用更多的输入验证。 例如，允许上载的图像大小/图像文件大小应加以限制。

### <a name="administrator-functionality"></a>管理员功能

管理员应该能够更改现有任务的所有权。 例如，任务的创建者可能会离开公司，除非启用了管理访问，否则任何人都无权维护该任务。

### <a name="queue-message-processing"></a>队列消息处理

修复 It 应用中的队列消息处理设计为简单，以便用最少的代码来说明以队列为中心的工作模式。 此简单代码不足以用于实际生产应用程序。

- 该代码不保证最多处理一次每个队列消息。 当您从队列中收到消息时，有一个超时期间，在此期间消息对其他队列侦听器不可见。 如果超时在删除邮件之前过期，则消息将再次可见。 因此，如果辅助角色实例花费很长时间来处理消息，则从理论上讲，同一消息可以处理两次，从而导致数据库中出现重复的任务。 有关此问题的详细信息，请参阅[使用 Azure 存储队列](https://msdn.microsoft.com/library/ff803365.aspx#sec7)。
- 通过批处理消息检索，队列轮询逻辑可能更具成本效益。 每次调用[CloudQueue.GetMessageasync](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.getmessageasync.aspx)时，都会有一个交易成本。 相反，您可以调用[CloudQueue.GetMessagesAsync（](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.getmessagesasync.aspx)请注意复数""），在单个事务中获取多条消息。 Azure 存储队列的事务成本非常低，因此在大多数情况下，对成本的影响并不大。
- 队列消息处理代码中的紧密循环会导致 CPU 关联性，而 CPU 关联性不会有效地利用多核 VM。 更好的设计将使用任务并行性并行运行多个异步任务。
- 队列消息处理只有基本的异常处理。 例如，代码不处理[有害消息](https://msdn.microsoft.com/library/ms789028.aspx)。 （当消息处理导致异常时，您必须记录错误并删除消息，否则辅助角色将再次尝试处理该错误，并且循环将无限期地继续。

### <a name="sql-queries-are-unbounded"></a>SQL 查询未绑定

当前修复代码对索引页的查询可能返回的行数没有限制。 如果数据库中输入了大量任务，则接收的结果列表的大小可能会导致性能问题。 解决方案是实现分页。 例如，请参阅在[ASP.NET mVC 应用程序中使用实体框架对实体框架进行排序、筛选和分页](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md)。

### <a name="view-models-recommended"></a>查看推荐的模型

修复它应用使用 FixItTask 实体类在控制器和视图之间传递信息。 最佳做法是使用视图模型。 域模型（例如 FixItTask 实体类）是围绕数据持久性所需的内容设计的，而视图模型可以设计为数据表示。 有关详细信息，请参阅[12 ASP.NET MVC 最佳实践](https://codeclimber.net.nz/archive/2009/10/27/12-asp.net-mvc-best-practices.aspx)。

### <a name="secure-image-blob-recommended"></a>建议使用安全映像 blob

Fix It 应用将上传的图像存储为公共图像，这意味着找到 URL 的任何人都可以访问这些图像。 图像可以保护而不是公开。

### <a name="no-powershell-automation-scripts-for-queues"></a>没有用于队列的 PowerShell 自动化脚本

示例 PowerShell 自动化脚本仅针对完全在 Azure 应用服务 Web 应用中运行的修复它的基本版本编写。 我们没有提供用于设置和部署到 Web 应用以及队列处理所需的云服务环境的脚本。

### <a name="special-handling-for-html-codes-in-user-input"></a>用户输入中 HTML 代码的特殊处理

ASP.NET通过在用户输入文本框中输入脚本，自动防止恶意用户尝试跨站点脚本攻击的多种方式。 MVC`DisplayFor`帮助程序用于显示任务标题和注释，自动对其进行 HTML 编码它发送到浏览器的值。 但在生产应用中，您可能需要采取其他措施。 有关详细信息，请参阅ASP.NET[中的请求验证](https://msdn.microsoft.com/library/hh882339.aspx)。

<a id="bestpractices"></a>
## <a name="best-practices"></a>最佳做法

以下是在修复 It 应用的原始版本的代码审查和测试中发现后修复的一些问题。 有些是由于原始编码器不知道特定的最佳实践造成的，有些只是因为代码编写得很快，并非针对发布的软件。 我们在这里列出问题，以防我们从这次审查和测试中学到的东西对正在开发 Web 应用程序的其他人有帮助。

### <a name="dispose-the-database-repository"></a>处置数据库存储库

类`FixItTaskRepository`必须释放实体框架`DbContext`实例。 我们通过在`FixItTaskRepository`类中实现`IDisposable`来实现此情况：

[!code-csharp[Main](the-fix-it-sample-application/samples/sample1.cs)]

请注意，AutoFac 将自动释放`FixItTaskRepository`实例，因此我们不需要显式处置它。

另一个选项是从 中删除`DbContext`成员变量`FixItTaskRepository`，而是在 语句内在每个`DbContext`存储库方法中创建一个`using`局部变量。 例如：

[!code-csharp[Main](the-fix-it-sample-application/samples/sample2.cs)]

### <a name="register-singletons-as-such-with-di"></a>使用 DI 注册单例

由于只需要`PhotoService`类和`Logger`类的一个实例，因此这些类应注册为*DependenciesConfig.cs*[中依赖项注入的单个实例](https://code.google.com/p/autofac/wiki/InstanceScope)：

[!code-csharp[Main](the-fix-it-sample-application/samples/sample3.cs?highlight=1,3)]

### <a name="security-dont-show-error-details-to-users"></a>安全性：不向用户显示错误详细信息

原始修复 It 应用没有通用错误页，只是让所有异常都冒泡到 UI 上，因此某些异常（如数据库连接错误）可能会导致向浏览器显示完整的堆栈跟踪。 详细的错误信息有时可能促进恶意用户的攻击。 解决方案是记录异常详细信息，并将错误页显示给不包含错误详细信息的用户。 修复它应用已经记录，为了显示错误页面，我们添加了`<customErrors mode=On>`Web.config 文件。

[!code-xml[Main](the-fix-it-sample-application/samples/sample4.xml?highlight=2)]

默认情况下，这将导致*显示视图\共享\Error.cshtml*以查找错误。 您可以自定义*Error.cshtml*或创建自己的错误页面视图并添加`defaultRedirect`属性。 您还可以为特定错误指定不同的错误页。

### <a name="security-only-allow-a-task-to-be-edited-by-its-creator"></a>安全性：仅允许其创建者编辑任务

"仪表板索引"页仅显示登录用户创建的任务，但恶意用户可以创建具有其他用户任务的 ID 的 URL。 我们*DashboardController.cs中*添加了代码，以在这种情况下返回 404：

[!code-csharp[Main](the-fix-it-sample-application/samples/sample5.cs?highlight=9-14,24-29)]

### <a name="dont-swallow-exceptions"></a>不要吞咽异常

原始修复 It 应用在记录 SQL 查询产生的异常后刚刚返回 null：

[!code-csharp[Main](the-fix-it-sample-application/samples/sample6.cs?highlight=4)]

这将使用户看起来好像查询成功，但只是没有返回任何行。 解决方案是在捕获和日志记录后重新引发异常：

[!code-csharp[Main](the-fix-it-sample-application/samples/sample7.cs)]

### <a name="catch-all-exceptions-in-worker-roles"></a>捕获辅助角色中的所有异常

辅助角色中的任何未处理异常都将导致 VM 被回收，因此您希望在 try-catch 块中包装所有操作，并处理所有异常。

### <a name="specify-length-for-string-properties-in-entity-classes"></a>指定实体类中字符串属性的长度

为了显示简单代码，修复它应用的原始版本没有指定 FixItTask 实体字段的长度，因此在数据库中将其定义为 varchar（max）。 因此，UI 将接受几乎任何数量的输入。 指定长度设置适用于网页中的用户输入和数据库中的列大小的限制：

[!code-csharp[Main](the-fix-it-sample-application/samples/sample8.cs?highlight=4,7,10,12,14)]

### <a name="mark-private-members-as-readonly-when-they-arent-expected-to-change"></a>当私人成员不需要更改时，将它们标记为只读

例如，在类中`DashboardController`，将创建`FixItTaskRepository`一个实例，并且不需要更改，所以我们将其定义为[只读](https://msdn.microsoft.com/library/acdd6hb7.aspx)。

[!code-csharp[Main](the-fix-it-sample-application/samples/sample9.cs?highlight=3)]

### <a name="use-listany-instead-of-listcount-gt-0"></a>使用列表。任何（）而不是列表。计数（） &gt; 0

如果您所关心的只是列表中的一个或多个项是否符合指定的条件，请使用[Any](https://msdn.microsoft.com/library/bb534972.aspx)方法，因为它在找到符合条件的项后立即返回，而`Count`该方法始终必须遍遍遍每个项。 仪表板*索引.cshtml*文件最初具有以下代码：

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample10.cshtml)]

我们将其更改为：

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample11.cshtml?highlight=1)]

### <a name="generate-urls-in-mvc-views-using-mvc-helpers"></a>使用 MVC 帮助器在 MVC 视图中生成 URL

对于主页上的"**修复 It"** 按钮，"修复它"应用硬编码锚点元素：

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample12.cshtml)]

对于像这样的视图/操作链接，最好使用[Url.Action](https://msdn.microsoft.com/library/system.web.mvc.urlhelper.action.aspx) HTML 帮助程序，例如：

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample13.cshtml)]

### <a name="use-taskdelay-instead-of-threadsleep-in-worker-role"></a>使用任务.延迟而不是线程.睡眠在辅助角色中

新项目模板将工作角色的示例`Thread.Sleep`代码放入其中，但导致线程处于睡眠状态可能会导致线程池生成其他不必要的线程。 您可以使用[Task.delay](https://msdn.microsoft.com/library/hh139096.aspx)来避免这种情况。

[!code-csharp[Main](the-fix-it-sample-application/samples/sample14.cs?highlight=11)]

### <a name="avoid-async-void"></a>避免异步空隙

如果异步方法不需要返回值，则返回类型`Task`而不是`void`。

此示例来自类`FixItQueueManager`：

[!code-csharp[Main](the-fix-it-sample-application/samples/sample15.cs)]

应仅对`async void`顶级事件处理程序使用。 如果将方法定义为`async void`，调用方无法**等待**该方法或捕获方法引发的任何异常。 有关详细信息，请参阅[异步编程中的最佳做法](https://msdn.microsoft.com/magazine/jj991977.aspx)。

### <a name="use-a-cancellation-token-to-break-from-worker-role-loop"></a>使用取消令牌从辅助角色循环中断

通常，辅助角色上的**Run**方法包含无限循环。 当辅助角色停止时，将调用[角色入口点.onStop](https://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstop.aspx)方法。 应使用此方法取消在**Run**方法内完成的工作并正常退出。 否则，进程可能在操作过程中终止。

### <a name="opt-out-of-automatic-mime-sniffing-procedure"></a>选择退出自动 MIME 嗅探过程

在某些情况下，Internet Explorer 报告 MIME 类型与 Web 服务器指定的类型不同。 例如，如果 Internet Explorer 在使用 HTTP 响应标头内容类型：文本/纯文交付的文件中查找 HTML 内容，则 Internet Explorer 确定内容应呈现为 HTML。 遗憾的是，这种"MIME 嗅探"还可能导致托管不受信任的内容的服务器出现安全问题。 为了解决这个问题，Internet Explorer 8 对 MIME 类型的确定代码进行了一些更改，并允许应用程序开发人员[选择退出 MIME 嗅探](https://blogs.msdn.com/b/ie/archive/2008/07/02/ie8-security-part-v-comprehensive-protection.aspx)。 以下代码已添加到*Web.config 文件中*。

[!code-xml[Main](the-fix-it-sample-application/samples/sample16.xml?highlight=2-7)]

### <a name="enable-bundling-and-minification"></a>实现捆绑和最小化

当 Visual Studio 创建新的 Web 项目时，默认情况下不会启用 JavaScript 文件的捆绑和小化。 我们在BundleConfig.cs中添加了一行代码：

[!code-csharp[Main](the-fix-it-sample-application/samples/sample17.cs?highlight=9)]

### <a name="set-an-expiration-time-out-for-authentication-cookies"></a>为身份验证 Cookie 设置过期超时

默认情况下，身份验证 Cookie 将在两周后过期。 更短的时间更安全。 您可以在*StartupAuth.cs*中更改此设置：

[!code-csharp[Main](the-fix-it-sample-application/samples/sample18.cs?highlight=4-5)]

<a id="run-in-vs"></a>
## <a name="how-to-run-the-app-from-visual-studio-on-your-local-computer"></a>如何从本地计算机上的 Visual Studio 运行应用

有两种方法可以运行修复它应用：

- 运行将新任务直接写入 SQL 数据库的基本应用程序。
- 使用队列和后端服务运行应用程序以创建任务。 队列模式在以[队列为中心的工作模式](queue-centric-work-pattern.md)一章中描述。

<a id="runbase"></a>
### <a name="run-the-base-application"></a>运行基本应用程序

1. 安装[视觉工作室 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017).
2. 为[.NET 安装用于视觉工作室的 Azure SDK。](https://azure.microsoft.com/downloads/)
3. 从[MSDN 代码库](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)下载 .zip 文件。
4. 在"文件资源管理器"中，右键单击 .zip 文件并单击"属性"，然后在"属性"窗口中单击"取消阻止"。
5. 解压缩文件。
6. 双击 .sln 文件以启动可视化工作室。
7. 在 **"工具"** 菜单中，单击**NuGet 包管理器**，然后单击**包管理器控制台**。
8. 在包管理器控制台 （PMC） 中，单击"还原"。
9. 退出 Visual Studio。
10. 启动[Azure 存储模拟器](/azure/storage/common/storage-use-emulator)。
11. 重新启动 Visual Studio，打开在上一步中关闭的解决方案文件。
12. 确保 FixIt 项目设置为启动项目，然后按 CTRL_F5 运行该项目。

<a id="queueslocal"></a>
### <a name="run-the-application-with-queue-processing"></a>使用队列处理运行应用程序

1. 按照[运行基本应用程序](#runbase)的说明操作，然后关闭浏览器并关闭 Visual Studio。
2. 使用管理员权限启动可视化工作室。 （您将使用 Azure 计算模拟器，这需要管理员权限。
3. 在*MyFixIt*项目中的应用程序*Web.config*文件中（Web 项目），将 的值`appSettings/UseQueues`更改为"true"：

    [!code-console[Main](the-fix-it-sample-application/samples/sample19.cmd?highlight=3)]
4. 如果[Azure 存储模拟器](https://msdn.microsoft.com/library/windowsazure/hh403989.aspx)未运行，则重新启动它。
5. 同时运行修复 It Web 项目和 MyFixIt云服务项目。

    使用 Visual Studio：

   1. 按**F5**以运行 FixIt 项目。
   2. 在**解决方案资源管理器**中，右键单击 MyFixIt云服务项目，然后单击 **"调试** > **启动新实例**"。

    使用可视化工作室 2013 快速网页：

   3. 在解决方案资源管理器中，右键单击 FixIt 解决方案并选择**属性**。
   4. 选择**多个启动项目**。
   5. 在 MyFixIt 和 MyFixIt云服务下的 **"操作**"下拉列表中，选择 **"开始**"。
   6. 单击“确定”。 
   7. 按 **F5** 运行这两个项目。

      运行 MyFixItCloud 服务项目时，Visual Studio 将启动 Azure 计算模拟器。 根据您的防火墙配置，您可能需要允许仿真器通过防火墙。

<a id="deploybase"></a>
## <a name="how-to-deploy-the-base-app-to-azure-app-service-web-apps-by-using-the-windows-powershell-scripts"></a>如何使用 Windows PowerShell 脚本将基本应用部署到 Azure 应用服务 Web 应用

为了说明["自动执行所有内容"](automate-everything.md)模式，修复 It 应用附带了在 Azure 中设置环境并将项目部署到新环境的脚本。 以下说明说明如何使用脚本。

如果要在 Azure 中运行而不使用队列，并且所做的更改是为了在本地使用队列运行，请确保在继续执行以下说明之前将 Use队列应用设置值设置为 false。

这些说明假定您已在本地下载并运行修复 It 解决方案，并且您具有 Azure 帐户或已授权管理的 Azure 订阅。

1. 安装**Azure PowerShell**控制台。 有关说明，请参阅[如何安装和配置 Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-4.3.1)。

    此自定义控制台配置为与 Azure 订阅配合使用。 Azure 模块安装在 *"程序文件"* 目录中，并在每次使用 Azure PowerShell 控制台时自动导入。

    如果喜欢在不同的主机程序（如 Windows PowerShell ISE）中工作，请确保使用[导入模块](https://go.microsoft.com/fwlink/?LinkID=141553)cmdlet 导入 Azure 模块或使用 Azure 模块中的命令触发模块的自动导入。
2. 使用 **"以管理员身份运行"** 选项启动 Azure PowerShell。
3. 运行["设置执行策略](https://go.microsoft.com/fwlink/p/?linkid=293941)"cmdlet 以将 Azure PowerShell`RemoteSigned`执行策略设置为 。 输入**Y（** 对于是）以完成策略更改。

    [!code-console[Main](the-fix-it-sample-application/samples/sample20.cmd)]

    此设置使您能够运行未进行数字签名的本地脚本。 （您还可以将执行策略设置为`Unrestricted`，这将在以后无需取消阻止步骤，但出于安全原因不建议这样做。
4. 运行`Add-AzureAccount`cmdlet 以使用您的帐户凭据设置 PowerShell。

    [!code-console[Main](the-fix-it-sample-application/samples/sample21.cmd)]

    这些凭据将在一段时间后过期，您必须重新运行`Add-AzureAccount`cmdlet。 在编写此电子书时，凭据过期前的时间限制为 12 小时。
5. 如果您有多个订阅，请使用选择 Azure 订阅 cmdlet 指定要在 中创建测试环境的订阅。
6. 使用`Get-AzurePublishSettingsFile`和`Import-AzurePublishSettingsFile`cmdlet 导入同一 Azure 订阅的管理证书。 第一个 cmdlet 下载证书文件，在第二个 cmdlet 中，您可以指定该文件的位置以导入它。 > [!IMPORTANT]
   > 将下载的文件保存在安全位置，或完成后将其删除，因为它包含可用于管理 Azure 服务的证书。

    [!code-console[Main](the-fix-it-sample-application/samples/sample22.cmd)]

    该证书用于 REST API 调用，该调用检测开发机的 IP 地址，以便在 SQL 数据库服务器上设置防火墙规则。
7. 运行["设置位置](https://go.microsoft.com/fwlink/p/?linkid=293912)cmdlet"（别名为`cd``chdir``sl`和 ），以导航到包含脚本的目录。 （它们位于"修复它"解决方案文件夹中的*自动化*文件夹中。如果任何目录名称包含空格，则将路径放入引号中。 例如，要导航到目录，`c:\Sample Apps\FixIt\Automation`可以输入以下命令：

    [!code-console[Main](the-fix-it-sample-application/samples/sample23.cmd)]
8. 要允许 Windows PowerShell 运行这些脚本，请使用[取消阻止文件](https://go.microsoft.com/fwlink/p/?linkid=294021)cmdlet。 （脚本被阻止，因为它们是从 Internet 下载的。

    > [!WARNING]
    > 安全性 -`Unblock-File`在运行任何脚本或可执行文件之前，在记事本中打开该文件，检查命令，并验证它们不包含任何恶意代码。

    例如，以下命令在当前目录中的所有脚本`Unblock-File`上运行 cmdlet。

    [!code-console[Main](the-fix-it-sample-application/samples/sample24.cmd)]
9. 要为基础创建 Web 应用（无队列处理）修复它应用，请运行环境创建脚本。

    所需的`Name`参数指定数据库的名称，并且也用于脚本创建的存储帐户。 名称在azurewebsites.net域中必须全局唯一。 如果指定的名称不唯一（如 Fixit 或 Test（甚至如示例中的 fixitdemo），`New-AzureWebsite`则 cmdlet 失败，并出现报告冲突的内部错误。 该脚本将名称转换为所有小写，以符合 Web 应用、存储帐户和数据库的名称要求。

    所需`SqlDatabasePassword`参数指定将为 SQL 数据库创建的管理员帐户的密码。 不要在密码中包含特殊的 XML 字符（;)。&amp; &lt; &gt; 这是脚本编写方式的限制，而不是 Azure 的限制。

    例如，如果要创建名为"fixitdemo"的 Web 应用并使用 SQL Server 管理员密码"Passw0rd1"，则可以输入以下命令：

    [!code-console[Main](the-fix-it-sample-application/samples/sample25.cmd)]

    名称在azurewebsites.net域中必须是唯一的，并且密码必须满足 SQL 数据库对密码复杂性的要求。 （示例 Passw0rd1 确实满足要求。

    请注意，该命令以"开头。\". 为了帮助防止恶意执行脚本，Windows PowerShell 要求您在运行脚本时提供脚本文件的完全限定路径。 可以使用点来指示当前目录 （"）。\"或提供完全限定的路径，例如：

    [!code-console[Main](the-fix-it-sample-application/samples/sample26.cmd)]

    有关脚本的详细信息，请使用`Get-Help`cmdlet。

    [!code-console[Main](the-fix-it-sample-application/samples/sample27.cmd)]

    您可以使用 获取帮助`Detailed` `Full`cmdlet 的 、`Parameters`和`Examples`参数来筛选返回的帮助。

    如果脚本失败或生成错误，例如"新建 Azure 网站：先调用集 Azure 订阅和选择 Azure 订阅"，则可能尚未完成 Azure PowerShell 的配置。

    脚本完成后，可以使用 Azure 管理门户查看已创建的资源，如["自动所有内容"](automate-everything.md)章节所示。
10. 要将 FixIt 项目部署到新的 Azure 环境，请使用*Azure 网站.ps1*脚本。 例如：

    [!code-console[Main](the-fix-it-sample-application/samples/sample28.cmd)]

    部署完成后，浏览器将在 Azure 中运行修复它时打开。

<a id="troubleshooting"></a>
## <a name="troubleshooting-the-windows-powershell-scripts"></a>对 Windows 电源外壳脚本进行故障排除

运行这些脚本时遇到的最常见的错误与权限有关。 确保 并`Add-AzureAccount``Import-AzurePublishSettingsFile`成功，并且将它们用于相同的 Azure 订阅。 即使`Add-AzureAccount`成功，你也得再次运行它。 添加`Add-AzureAccount`的权限将在 12 小时内过期。

### <a name="object-reference-not-set-to-an-instance-of-an-object"></a>对象引用未设置为某个对象的实例。

如果脚本返回错误（如"对象引用未设置为对象的实例"，这意味着 Windows PowerShell 找不到要处理的对象（这是空引用异常），请运行`Add-AzureAccount`cmdlet 并重试该脚本。

[!code-console[Main](the-fix-it-sample-application/samples/sample29.cmd)]

### <a name="internalerror-the-server-encountered-an-internal-error"></a>内部错误：服务器遇到内部错误。

当`New-AzureWebsite`名称在azurewebsites.net域中不唯一时，cmdlet 返回内部错误。 要解决错误，请使用名称的其他值，该值位于*New-Azure网站Env.ps1*的名称参数中。

[!code-console[Main](the-fix-it-sample-application/samples/sample30.cmd)]

### <a name="restarting-the-script"></a>重新启动脚本

如果需要重新启动*New-Azure 网站Env.ps1*脚本，因为它在打印"脚本已完成"消息之前出现故障，则可能需要删除脚本在停止之前创建的资源。 例如，如果脚本已创建 ContosoFixItDemo Web 应用，并且您再次使用相同的名称运行脚本，则该脚本将失败，因为该名称正在使用中。

要确定脚本在停止之前创建的资源，请使用以下 cmdlet：

- `Get-AzureWebsite`
- `Get-AzureSqlDatabaseServer`
- `Get-AzureSqlDatabase`： 要运行此 cmdlet，请将数据库服务器`Get-AzureSqlDatabase`名称管道到 ：`Get-AzureSqlDatabaseServer | Get-AzureSqlDatabase.`

要删除这些资源，请使用以下命令。 请注意，如果删除数据库服务器，则会自动删除与服务器关联的数据库。

- `Get-AzureWebsite -Name <WebsiteName> | Remove-AzureWebsite`
- `Get-AzureSqlDatabase -Name <DatabaseName> -ServerName <DatabaseServerName> | Remove-SqlAzureDatabase`
- `Get-AzureSqlDatabaseServer | Remove-AzureSqlDatabaseServer`

<a id="deployqueues"></a>
## <a name="how-to-deploy-the-app-with-queue-processing-to-azure-app-service-web-apps-and-an-azure-cloud-service"></a>如何将具有队列处理的应用部署到 Azure 应用服务 Web 应用和 Azure 云服务

要启用队列，请确保在 MyFixIt_Web.config 文件中进行以下更改。 在`appSettings`下，将`UseQueues`的值更改为"true"：

[!code-xml[Main](the-fix-it-sample-application/samples/sample31.xml)]

然后，将 MVC 应用程序部署到 Azure 应用服务中的 Web 应用，如[前面](#deploybase)所述。

接下来，创建新的 Azure 云服务。 修复 It 应用中包含的脚本不会创建或部署云服务，因此必须为此使用 Azure 门户。 在门户中，单击 **"新** -- **计算**+**云服务** -- **快速创建**"，然后输入 URL 和数据中心位置。 使用部署 Web 应用的同一数据中心。

![](the-fix-it-sample-application/_static/image1.png)

在部署云服务之前，需要更新某些配置文件。

在 MyFixIt.WorkerRole_app.config`connectionStrings`中，在 下，`appdb`将连接字符串的值替换为 SQL 数据库的实际连接字符串。 可以从门户获取连接字符串。 在门户中，单击**ADO .Net、ODBC、PHP 和 JDBC 的** **SQL 数据库** - **appdb** - 视图 SQL 数据库连接字符串。 复制ADO.NET连接字符串并将该值粘贴到 app.config 文件中。 将"此处的\_密码\_"替换为数据库密码。 （假设您使用脚本部署 MVC 应用，则可以在脚本参数中`SqlDatabasePassword`指定数据库密码。

结果应如下所示：

[!code-xml[Main](the-fix-it-sample-application/samples/sample32.xml)]

在同一 MyFixIt.WorkerRole_app.config 文件下`appSettings`，替换 Azure 存储帐户的两个占位符值。

[!code-xml[Main](the-fix-it-sample-application/samples/sample33.xml?highlight=2-3)]

可以从门户获取访问密钥。 请参阅[如何管理存储帐户](https://docs.microsoft.com/azure/storage/common/storage-create-storage-account)。

在 MyFixItCloudService 服务配置.Cloud.cscfg 中，替换 Azure 存储帐户的两个占位符值。

[!code-xml[Main](the-fix-it-sample-application/samples/sample34.xml?highlight=3)]

现在，您已准备好部署云服务。 在"解决方案浏览"中，右键单击 MyFixIt云服务项目并选择 **"发布**"。 有关详细信息，请参阅[本教程的第](https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36)2 部分中的"[将应用程序部署到 Azure"。](https://www.windowsazure.com/develop/net/tutorials/multi-tier-web-site/2-download-and-run/#deployAz)

> [!div class="step-by-step"]
> [上一步](more-patterns-and-guidance.md)

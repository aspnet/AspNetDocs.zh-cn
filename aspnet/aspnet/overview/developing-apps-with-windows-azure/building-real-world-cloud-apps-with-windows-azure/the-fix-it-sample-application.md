---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/the-fix-it-sample-application
title: 附录： Fix It 示例应用程序 (用 Azure) 构建实际云应用 |Microsoft Docs
author: MikeWasson
description: 使用 Azure 电子书构建真实的云应用基于 Scott Guthrie 开发的演示文稿。 它介绍了13种模式和实践，
ms.author: riande
ms.date: 06/12/2014
ms.assetid: 1bc333c5-f096-4ea7-b170-779accc21c1a
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/the-fix-it-sample-application
msc.type: authoredcontent
ms.openlocfilehash: 549d1513279190ae5abe87c59a48e1caa1cfa5f7
ms.sourcegitcommit: feb88edfb01b32f6fc9488f0f0ddb3c5b34e6ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/21/2020
ms.locfileid: "88702928"
---
# <a name="appendix-the-fix-it-sample-application-building-real-world-cloud-apps-with-azure"></a>附录： Fix It 示例应用程序 (用 Azure) 构建实际云应用

作者： [Mike Wasson](https://github.com/MikeWasson)， [Rick Anderson](https://twitter.com/RickAndMSFT)， [Tom Dykstra](https://github.com/tdykstra)

[下载 Fix It 项目](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)

> **使用 Azure 电子书构建真实的云应用**基于 Scott Guthrie 开发的演示文稿。 它介绍了可帮助你成功开发云的 web 应用的13种模式和实践。 有关电子书的信息，请参阅 [第一章](introduction.md)。

本附录介绍了如何通过 Azure 电子书构建实际的云应用程序，其中包含了有关可以下载的 Fix It 示例应用程序的其他信息：

- [已知问题](#knownissues)
- [最佳做法](#bestpractices)
- [如何在本地计算机上从 Visual Studio 运行应用](#run-in-vs)
- [如何使用 Windows PowerShell 脚本将基本应用部署到 Azure App Service Web 应用](#deploybase)
- [Windows PowerShell 脚本疑难解答](#troubleshooting)
- [如何将具有队列处理的应用部署到 Azure App Service Web 应用和 Azure 云服务](#deployqueues)

<a id="knownissues"></a>
## <a name="known-issues"></a>已知问题

最初开发 Fix It 应用程序是为了尽可能简单地说明此电子书中介绍的一些模式。 不过，由于电子书就是构建真实的应用程序，因此我们将修复它的代码放在评审和测试过程中，就像我们对发布的软件执行的操作一样。 我们发现了很多问题，与任何实际应用程序一样，其中一些问题已修复，其中一些问题已推迟到更高版本。

下面的列表包含应在生产应用程序中解决的问题，但出于某种原因或者我们决定不在 Fix It 示例应用程序的初始版本中解决。

### <a name="security"></a>安全性

- 请确保不能向不存在的所有者分配任务。
- 确保您只能查看和修改您创建或分配给您的任务。
- 将 HTTPS 用于登录页和身份验证 cookie。
- 指定身份验证 cookie 的时间限制。

### <a name="input-validation"></a>输入验证

通常，生产应用执行的输入验证比 Fix It 应用要多。 例如，允许上传的图像大小/图像文件大小应受限。

### <a name="administrator-functionality"></a>管理员功能

管理员应该能够更改现有任务的所有权。 例如，如果启用了管理访问权限，则任务的创建者可能会离开公司，而不会有权维护该任务。

### <a name="queue-message-processing"></a>队列消息处理

Fix It 应用中的队列消息处理设计为非常简单，以便以最少的代码说明以队列为中心的工作模式。 对于实际的生产应用程序而言，这种简单的代码将不能满足需要。

- 此代码不保证每个队列消息将最多处理一次。 当你从队列中获取消息时，有一个超时期限，在此期间，消息对其他队列侦听器不可见。 如果在删除消息之前超时过期，则该消息将再次变为可见。 因此，如果辅助角色实例花费很长时间来处理消息，则理论上可能会将同一消息处理两次，从而导致数据库中出现重复的任务。 有关此问题的详细信息，请参阅 [使用 Azure 存储队列](https://msdn.microsoft.com/library/ff803365.aspx#sec7)。
- 通过批处理消息检索，队列轮询逻辑可能更具成本效益。 每次调用 [CloudQueue GetMessageAsync](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.getmessageasync.aspx)时，都会产生事务成本。 相反，你可以调用 [CloudQueue. GetMessagesAsync](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.getmessagesasync.aspx) (记下复数的 ") ，这将在单个事务中获取多个消息。 Azure 存储队列的事务成本非常低，因此，对成本的影响在大多数情况下并不明显。
- 队列消息处理代码中的紧密循环导致 CPU 关联，这不会有效地利用多核 Vm。 更好的设计会使用任务并行并行运行多个异步任务。
- 队列消息处理只包含基本异常处理。 例如，代码不处理 [病毒消息](https://msdn.microsoft.com/library/ms789028.aspx)。  (当消息处理导致异常时，您必须记录错误并删除消息，否则辅助角色将尝试再次处理该消息，并且循环会无限期地继续。 ) 

### <a name="sql-queries-are-unbounded"></a>未绑定 SQL 查询

当前 Fix It 代码对索引页的查询可能返回的行数没有限制。 如果将大量任务输入到数据库中，则收到的结果列表的大小可能会导致性能问题。 解决方案是实现分页。 有关示例，请参阅 [使用 ASP.NET MVC 应用程序中的实体框架进行排序、筛选和分页](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md)。

### <a name="view-models-recommended"></a>建议查看模型

Fix It 应用使用 FixItTask 实体类在控制器和视图之间传递信息。 最佳做法是使用视图模型。 域模型 (例如，FixItTask 实体类) 是围绕数据持久性所需要的内容设计的，而视图模型可用于数据显示。 有关详细信息，请参阅 [12 ASP.NET MVC 最佳实践](https://codeclimber.net.nz/archive/2009/10/27/12-asp.net-mvc-best-practices.aspx)。

### <a name="secure-image-blob-recommended"></a>建议使用安全图像 blob

Fix It 应用将上传的图像存储为公用，这意味着查找 URL 的任何人都可以访问这些图像。 图像可以是安全的，而不是公共的。

### <a name="no-powershell-automation-scripts-for-queues"></a>没有用于队列的 PowerShell 自动化脚本

示例 PowerShell 自动化脚本只是为完全在 Azure App Service Web 应用中运行的基本版本的修补程序编写的。 我们尚未提供用于设置和部署到 web 应用的脚本，以及队列处理所需的云服务环境。

### <a name="special-handling-for-html-codes-in-user-input"></a>用户输入中 HTML 代码的特殊处理

ASP.NET 通过在 "用户输入" 文本框中输入 script，来自动防止恶意用户可能尝试跨站点脚本攻击的多种方式。 `DisplayFor`用于显示任务标题和备注的 MVC 帮助器会自动对其发送到浏览器的值进行 HTML 编码。 但在生产应用程序中，你可能需要采取其他措施。 有关详细信息，请参阅 [ASP.NET 中的请求验证](https://msdn.microsoft.com/library/hh882339.aspx)。

<a id="bestpractices"></a>
## <a name="best-practices"></a>最佳做法

下面是在代码评审和测试 Fix It 应用程序的原始版本中发现后修复的一些问题。 其中一些原因是最初的编码员无法识别特定的最佳实践，只是因为代码是快速编写的，而不是用于发布的软件。 我们将在此处列出问题，因为我们在此审查和测试中了解到的内容可能对也正在开发 web 应用的其他人员有所帮助。

### <a name="dispose-the-database-repository"></a>释放数据库存储库

`FixItTaskRepository`类必须释放实体框架 `DbContext` 实例。 为此，我们 `IDisposable` 在类中实现 `FixItTaskRepository` ：

[!code-csharp[Main](the-fix-it-sample-application/samples/sample1.cs)]

请注意，AutoFac 将自动释放该 `FixItTaskRepository` 实例，因此我们不需要显式释放它。

另一种方法是从中移除 `DbContext` 成员变量 `FixItTaskRepository` ，而在 `DbContext` 语句内的每个存储库方法中创建一个本地变量 `using` 。 例如：

[!code-csharp[Main](the-fix-it-sample-application/samples/sample2.cs)]

### <a name="register-singletons-as-such-with-di"></a>用 DI 注册单一实例

由于只 `PhotoService` 需要类和类的一个实例 `Logger` ，因此应将这些类注册为*DependenciesConfig.cs*中[的依赖项注入的单一实例](https://code.google.com/p/autofac/wiki/InstanceScope)：

[!code-csharp[Main](the-fix-it-sample-application/samples/sample3.cs?highlight=1,3)]

### <a name="security-dont-show-error-details-to-users"></a>安全性：不向用户显示错误详细信息

原始的 Fix It 应用没有通用错误页，只是让所有异常向上冒泡到 UI，因此某些异常（如数据库连接错误）可能会导致在浏览器中显示完整的堆栈跟踪。 详细的错误信息有时会有助于恶意用户的攻击。 解决方案是记录异常详细信息，并向用户显示不包含错误详细信息的错误页。 Fix It 应用已经记录了日志，为了显示错误页面，我们添加到 `<customErrors mode=On>` 了 Web.config 文件中。

[!code-xml[Main](the-fix-it-sample-application/samples/sample4.xml?highlight=2)]

默认情况下，这会导致 *Views\Shared\Error.cshtml* 显示错误。 你可以自定义 *错误* ，或创建你自己的错误页面视图并添加 `defaultRedirect` 属性。 还可以为特定错误指定不同的错误页。

### <a name="security-only-allow-a-task-to-be-edited-by-its-creator"></a>安全性：仅允许由其创建者编辑任务

"仪表板索引" 页仅显示登录用户创建的任务，但恶意用户可能会创建一个 ID 为其他用户任务的 URL。 我们在 *DashboardController.cs* 中添加了代码，在这种情况下返回404：

[!code-csharp[Main](the-fix-it-sample-application/samples/sample5.cs?highlight=9-14,24-29)]

### <a name="dont-swallow-exceptions"></a>不要吞并异常

最初的 Fix It 应用在记录由 SQL 查询引发的异常后，刚刚返回 null：

[!code-csharp[Main](the-fix-it-sample-application/samples/sample6.cs?highlight=4)]

这会使用户看起来像查询成功，但并不返回任何行。 解决方法是在捕获和记录后重新引发异常：

[!code-csharp[Main](the-fix-it-sample-application/samples/sample7.cs)]

### <a name="catch-all-exceptions-in-worker-roles"></a>捕获辅助角色中的所有异常

辅助角色中的任何未经处理的异常都将导致 VM 被回收，因此你希望在 try-catch 块中包装所有内容并处理所有异常。

### <a name="specify-length-for-string-properties-in-entity-classes"></a>指定实体类中字符串属性的长度

为了显示简单代码，修复 It 应用的原始版本未指定 FixItTask 实体字段的长度，因此，它们在数据库中定义为 varchar (max) 。 因此，UI 几乎可以接受任意数量的输入。 指定长度会将应用于网页中的用户输入和数据库中的列大小的限制设置为：

[!code-csharp[Main](the-fix-it-sample-application/samples/sample8.cs?highlight=4,7,10,12,14)]

### <a name="mark-private-members-as-readonly-when-they-arent-expected-to-change"></a>当私有成员不应更改时将其标记为只读

例如，在的 `DashboardController` 类中创建了一个实例， `FixItTaskRepository` 但该实例不应更改，因此我们将其定义为 [readonly](https://msdn.microsoft.com/library/acdd6hb7.aspx)。

[!code-csharp[Main](the-fix-it-sample-application/samples/sample9.cs?highlight=3)]

### <a name="use-listany-instead-of-listcount-gt-0"></a>使用列表。任何 ( # A1，而不是 list。计数 ( # A3 &gt; 0

如果你只关心列表中的一个或多个项是否符合指定的条件，请使用 [Any](https://msdn.microsoft.com/library/bb534972.aspx) 方法，因为它会在找到符合条件的项后立即返回，而 `Count` 方法始终必须循环访问每个项。 仪表板 *索引 cshtml* 文件最初具有以下代码：

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample10.cshtml)]

我们将其更改为：

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample11.cshtml?highlight=1)]

### <a name="generate-urls-in-mvc-views-using-mvc-helpers"></a>使用 MVC 帮助程序在 MVC 视图中生成 Url

对于主页上的 " **创建修复它** " 按钮，"修复 it 应用" 硬编码锚点元素：

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample12.cshtml)]

对于类似的视图/操作链接，最好使用 [Url。操作](https://msdn.microsoft.com/library/system.web.mvc.urlhelper.action.aspx) HTML 帮助器，例如：

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample13.cshtml)]

### <a name="use-taskdelay-instead-of-threadsleep-in-worker-role"></a>使用任务延迟，而不是线程。辅助角色中的睡眠

新项目模板 `Thread.Sleep` 为辅助角色提供示例代码，但导致线程进入睡眠状态可能导致线程池产生其他不必要的线程。 可以通过使用 [Task](https://msdn.microsoft.com/library/hh139096.aspx) 来避免这种情况。

[!code-csharp[Main](the-fix-it-sample-application/samples/sample14.cs?highlight=11)]

### <a name="avoid-async-void"></a>避免 async void

如果异步方法不需要返回值，则返回 `Task` 类型而不是 `void` 。

此示例来自 `FixItQueueManager` 类：

[!code-csharp[Main](the-fix-it-sample-application/samples/sample15.cs)]

只应使用 `async void` 顶级事件处理程序。 如果将方法定义为 `async void` ，则调用方不能 **等待** 方法或捕获该方法引发的任何异常。 有关详细信息，请参阅 [异步编程中的最佳做法](https://msdn.microsoft.com/magazine/jj991977.aspx)。

### <a name="use-a-cancellation-token-to-break-from-worker-role-loop"></a>使用取消标记从辅助角色循环中断

通常，辅助角色上的 **Run** 方法包含无限循环。 辅助角色停止时，将调用 [RoleEntryPoint](https://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstop.aspx) 方法。 应使用此方法取消在 **Run** 方法内完成的工作并正常退出。 否则，可能会在操作过程中终止进程。

### <a name="opt-out-of-automatic-mime-sniffing-procedure"></a>选择退出自动 MIME 探查过程

在某些情况下，Internet Explorer 报告 MIME 类型不同于 web 服务器指定的类型。 例如，如果 Internet Explorer 在使用 HTTP 响应标头 Content （文本/无格式）传递的文件中查找 HTML 内容，则 Internet Explorer 会确定内容应呈现为 HTML。 遗憾的是，这种 "MIME 探查" 也可能导致承载不受信任的内容的服务器的安全问题。 为了应对此问题，Internet Explorer 8 对 MIME 类型的确定代码进行了大量更改，并使应用程序开发人员可以 [选择退出 mime 探查](https://blogs.msdn.com/b/ie/archive/2008/07/02/ie8-security-part-v-comprehensive-protection.aspx)。 下面的代码已添加到 *Web.config* 文件中。

[!code-xml[Main](the-fix-it-sample-application/samples/sample16.xml?highlight=2-7)]

### <a name="enable-bundling-and-minification"></a>启用捆绑和缩减

当 Visual Studio 创建新的 web 项目时，默认情况下不启用 JavaScript 文件的绑定和缩减。 我们在 BundleConfig.cs 中添加了一行代码：

[!code-csharp[Main](the-fix-it-sample-application/samples/sample17.cs?highlight=9)]

### <a name="set-an-expiration-time-out-for-authentication-cookies"></a>设置身份验证 cookie 的过期超时

默认情况下，身份验证 cookie 在两周后过期。 更短的时间更安全。 可以在 *StartupAuth.cs*中更改此设置：

[!code-csharp[Main](the-fix-it-sample-application/samples/sample18.cs?highlight=4-5)]

<a id="run-in-vs"></a>
## <a name="how-to-run-the-app-from-visual-studio-on-your-local-computer"></a>如何在本地计算机上从 Visual Studio 运行应用

可以通过两种方式来运行 Fix It 应用：

- 运行将新任务直接写入 SQL 数据库的基本应用程序。
- 使用队列和后端服务运行应用程序以创建任务。 队列模式在以 [队列为中心的工作模式](queue-centric-work-pattern.md)中进行了介绍。

<a id="runbase"></a>
### <a name="run-the-base-application"></a>运行基本应用程序

1. 安装 [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)。
2. 安装 [适用于 Visual Studio 的 AZURE SDK for .net](https://azure.microsoft.com/downloads/)。
3. 从 [MSDN 代码库](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)下载 .zip 文件。
4. 在文件资源管理器中，右键单击 .zip 文件并单击 "属性"，然后在属性窗口单击 "解除阻止"。
5. 解压缩文件。
6. 双击 .sln 文件以启动 Visual Studio。
7. 从 " **工具** " 菜单中依次单击 " **NuGet 包管理器**" 和 " **程序包管理器控制台**"。
8. 在包管理器控制台中 (PMC ") 中，单击" 还原 "。
9. 退出 Visual Studio。
10. 启动 [Azure 存储模拟器](/azure/storage/common/storage-use-emulator)。
11. 重新启动 Visual Studio，并打开在上一步中关闭的解决方案文件。
12. 请确保将 Fix it 项目设置为启动项目，然后按 CTRL + F5 运行该项目。

<a id="queueslocal"></a>
### <a name="run-the-application-with-queue-processing"></a>运行具有队列处理的应用程序

1. 按照 [运行基本应用程序](#runbase)的说明进行操作，然后关闭浏览器并关闭 Visual Studio。
2. 以管理员权限启动 Visual Studio。  (你将使用 Azure 计算模拟器，并且需要管理员权限。 ) 
3. 在*MyFixIt*项目的应用程序*Web.config*文件中 (web 项目) ，将的值更改 `appSettings/UseQueues` 为 "true"：

    [!code-console[Main](the-fix-it-sample-application/samples/sample19.cmd?highlight=3)]
4. 如果 [Azure 存储模拟器](https://msdn.microsoft.com/library/windowsazure/hh403989.aspx) 仍未运行，请重新启动。
5. 同时运行 Fix it web 项目和 MyFixItCloudService 项目。

    使用 Visual Studio：

   1. 按 **F5** 运行 fix it 项目。
   2. 在**解决方案资源管理器**中，右键单击 MyFixItCloudService 项目，然后单击 "**调试**" "  >  **启动新实例**"。

    使用 Visual Studio 2013 Express for Web：

   3. 在解决方案资源管理器中，右键单击 Fix it 解决方案，然后选择 " **属性**"。
   4. 选择 **多个启动项目**。
   5. 在 MyFixIt 和 MyFixItCloudService 下的 " **操作** " 下拉列表中，选择 " **启动**"。
   6. 单击 **“确定”** 。
   7. 按 **F5** 运行这两个项目。

      运行 MyFixItCloudService 项目时，Visual Studio 将启动 Azure 计算模拟器。 根据防火墙配置，可能需要通过防火墙允许模拟器。

<a id="deploybase"></a>
## <a name="how-to-deploy-the-base-app-to-azure-app-service-web-apps-by-using-the-windows-powershell-scripts"></a>如何使用 Windows PowerShell 脚本将基本应用部署到 Azure App Service Web 应用

为了说明 [自动完成所有](automate-everything.md) 模式，通过在 Azure 中设置环境并将项目部署到新环境的脚本提供了 Fix It 应用。 以下说明介绍了如何使用这些脚本。

如果要在 Azure 中运行而不使用队列，并且更改了在本地运行队列，请确保在继续执行以下说明之前，将 UseQueues appSetting 值设置回 false。

这些说明假定你已在本地下载并运行 Fix It 解决方案，并且你有一个 Azure 帐户，或者你有权管理的 Azure 订阅。

1. 安装 **Azure PowerShell** 控制台。 有关说明，请参阅[如何安装和配置 Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-4.3.1)。

    此自定义控制台配置为使用 Azure 订阅。 Azure 模块安装在 *Program Files* 目录中，并将在每次使用 Azure PowerShell 控制台时自动导入。

    如果希望在不同的主机程序中工作，如 Windows PowerShell ISE，请确保使用 [import-module](https://go.microsoft.com/fwlink/?LinkID=141553) cmdlet 导入 azure 模块，或使用 azure 模块中的命令来触发模块的自动导入。
2. 通过 "以 **管理员身份运行** " 选项启动 Azure PowerShell。
3. 运行 [set-executionpolicy](https://go.microsoft.com/fwlink/p/?linkid=293941) cmdlet 以将 Azure PowerShell 执行策略设置为 `RemoteSigned` 。 输入 **"** 是" ("是") 完成策略更改。

    [!code-console[Main](the-fix-it-sample-application/samples/sample20.cmd)]

    此设置允许您运行未进行数字签名的本地脚本。  (您还可以将执行策略设置为 `Unrestricted` ，这将不再需要取消阻止步骤，但出于安全原因，不建议这样做。 ) 
4. 运行 `Add-AzureAccount` cmdlet，为你的帐户设置具有凭据的 PowerShell。

    [!code-console[Main](the-fix-it-sample-application/samples/sample21.cmd)]

    这些凭据将在一段时间后过期，你必须重新运行 `Add-AzureAccount` cmdlet。 在编写此电子书时，凭据过期前的时间限制为12小时。
5. 如果有多个订阅，请使用 Get-azuresubscription cmdlet 来指定要在其中创建测试环境的订阅。
6. 使用和 cmdlet 导入同一 Azure 订阅的管理证书 `Get-AzurePublishSettingsFile` `Import-AzurePublishSettingsFile` 。 其中的第一个 cmdlet 下载证书文件，并在第二个 cmdlet 中指定该文件的位置以将其导入。 > [!IMPORTANT]
   > 将下载的文件保存在安全的位置，或在完成后将其删除，因为它包含可用于管理 Azure 服务的证书。

    [!code-console[Main](the-fix-it-sample-application/samples/sample22.cmd)]

    证书用于检测开发计算机的 IP 地址的 REST API 调用，以便在 SQL 数据库服务器上设置防火墙规则。
7. 运行 ([Set-Location](https://go.microsoft.com/fwlink/p/?linkid=293912)别名为 `cd` 、 `chdir` 和 `sl`) ，以导航到包含脚本的目录。  (它们位于 Fix It 解决方案文件夹中的 *Automation* 文件夹中。如果任何目录名称包含空格，则 ) 将路径放在引号中。 例如，若要导航到该 `c:\Sample Apps\FixIt\Automation` 目录，可以输入以下命令：

    [!code-console[Main](the-fix-it-sample-application/samples/sample23.cmd)]
8. 若要允许 Windows PowerShell 运行这些脚本，请使用 [取消阻止文件](https://go.microsoft.com/fwlink/p/?linkid=294021) cmdlet。  (脚本被阻止，因为这些脚本是从 Internet 下载的。 ) 

    > [!WARNING]
    > 安全性- `Unblock-File` 在任何脚本或可执行文件上运行之前，在记事本中打开文件，检查命令，并验证它们是否不包含任何恶意代码。

    例如，以下命令将 `Unblock-File` 对当前目录中的所有脚本运行 cmdlet。

    [!code-console[Main](the-fix-it-sample-application/samples/sample24.cmd)]
9. 若要创建基本 (的 web 应用，) 修复 It 应用，请运行环境创建脚本。

    必需的 `Name` 参数指定数据库的名称，并且还用于该脚本创建的存储帐户。 该名称在 azurewebsites.net 域中必须是全局唯一的。 如果指定的名称不是唯一的（例如 Fix it 或 Test (），甚至在示例中为) fixitdemo，则该 `New-AzureWebsite` cmdlet 将失败并出现内部错误，该错误会报告冲突。 此脚本将名称转换为全部小写，以符合 web 应用、存储帐户和数据库的名称要求。

    必需的 `SqlDatabasePassword` 参数指定将为 SQL 数据库创建的管理员帐户的密码。 请勿在密码 (中包含特殊 XML 字符 &amp; &lt; &gt; ，) 。 这是编写脚本的方式的限制，而不是 Azure 的限制。

    例如，如果想要创建名为 "fixitdemo" 的 web 应用，并使用 "Passw0rd1" SQL Server 管理员密码，则可以输入以下命令：

    [!code-console[Main](the-fix-it-sample-application/samples/sample25.cmd)]

    该名称在 azurewebsites.net 域中必须唯一，并且密码必须满足密码复杂性的 SQL 数据库要求。  (示例 Passw0rd1 满足要求。 ) 

    请注意，该命令以 ". \" 。 为了帮助防止恶意脚本的执行，Windows PowerShell 要求你在运行脚本时提供脚本文件的完全限定路径。 您可以使用点来指示当前目录 ( "。 \") 或提供完全限定的路径，例如：

    [!code-console[Main](the-fix-it-sample-application/samples/sample26.cmd)]

    有关该脚本的详细信息，请使用 `Get-Help` cmdlet。

    [!code-console[Main](the-fix-it-sample-application/samples/sample27.cmd)]

    您可以使用 `Detailed` `Full` get-help cmdlet 的、、 `Parameters` 和 `Examples` 参数来筛选返回的帮助。

    如果脚本失败或生成错误，如 "New-azurewebsite： Get-azuresubscription 和 Get-azuresubscription first"，则可能没有完成 Azure PowerShell 的配置。

    脚本完成后，可以使用 Azure 管理门户查看已创建的资源，如 " [自动执行所有](automate-everything.md) 操作" 一章中所示。
10. 若要将 Fix it 项目部署到新的 Azure 环境，请使用 *AzureWebsite.ps1* 脚本。 例如：

    [!code-console[Main](the-fix-it-sample-application/samples/sample28.cmd)]

    部署完成后，浏览器将打开，并在 Azure 中运行它。

<a id="troubleshooting"></a>
## <a name="troubleshooting-the-windows-powershell-scripts"></a>Windows PowerShell 脚本疑难解答

运行这些脚本时遇到的最常见错误与权限有关。 请确保 `Add-AzureAccount` 和 `Import-AzurePublishSettingsFile` 已成功完成，并且已将其用于同一 Azure 订阅。 即使 `Add-AzureAccount` 成功，您也可能需要重新运行它。 添加的权限将 `Add-AzureAccount` 在12小时后过期。

### <a name="object-reference-not-set-to-an-instance-of-an-object"></a>对象引用未设置为某个对象的实例。

如果脚本返回错误，如 "对象引用未设置为对象的实例"，这意味着 Windows PowerShell 找不到要处理的对象 (这是 null 引用异常) ，请运行 `Add-AzureAccount` cmdlet，然后重试该脚本。

[!code-console[Main](the-fix-it-sample-application/samples/sample29.cmd)]

### <a name="internalerror-the-server-encountered-an-internal-error"></a>InternalError：服务器遇到内部错误。

`New-AzureWebsite`如果名称在 azurewebsites.net 域中不唯一，则该 cmdlet 将返回内部错误。 若要解决此错误，请使用不同的名称值，该名称位于 *New-AzureWebsiteEnv.ps1*的 name 参数中。

[!code-console[Main](the-fix-it-sample-application/samples/sample30.cmd)]

### <a name="restarting-the-script"></a>重新启动脚本

如果需要重新启动 *New-AzureWebsiteEnv.ps1* 脚本，因为它在打印 "脚本已完成" 消息之前失败，你可能想要删除该脚本在停止之前创建的资源。 例如，如果脚本已经创建了 ContosoFixItDemo web 应用，并使用同一名称再次运行该脚本，则该脚本将失败，因为该名称正在使用中。

若要确定脚本在停止之前创建了哪些资源，请使用以下 cmdlet：

- `Get-AzureWebsite`
- `Get-AzureSqlDatabaseServer`
- `Get-AzureSqlDatabase`：若要运行此 cmdlet，请通过管道将数据库服务器名称传递给 `Get-AzureSqlDatabase` ：   `Get-AzureSqlDatabaseServer | Get-AzureSqlDatabase.`

若要删除这些资源，请使用以下命令。 请注意，如果删除数据库服务器，则会自动删除与该服务器关联的数据库。

- `Get-AzureWebsite -Name <WebsiteName> | Remove-AzureWebsite`
- `Get-AzureSqlDatabase -Name <DatabaseName> -ServerName <DatabaseServerName> | Remove-SqlAzureDatabase`
- `Get-AzureSqlDatabaseServer | Remove-AzureSqlDatabaseServer`

<a id="deployqueues"></a>
## <a name="how-to-deploy-the-app-with-queue-processing-to-azure-app-service-web-apps-and-an-azure-cloud-service"></a>如何将具有队列处理的应用部署到 Azure App Service Web 应用和 Azure 云服务

若要启用队列，请在 MyFixIt\Web.config 文件中进行以下更改。 在下 `appSettings` ，将的值更改 `UseQueues` 为 "true"：

[!code-xml[Main](the-fix-it-sample-application/samples/sample31.xml)]

然后，在 Azure App Service 中将 MVC 应用程序部署到 web 应用，如 [前文所](#deploybase)述。

接下来，创建新的 Azure 云服务。 Fix It 应用中包含的脚本不会创建或部署云服务，因此你必须使用 Azure 门户。 在门户中，单击 "**新建**  --  **计算**–**云服务**  --  " "**快速创建**"，然后输入 URL 和数据中心位置。 使用在其中部署 web 应用的数据中心。

![](the-fix-it-sample-application/_static/image1.png)

在部署云服务之前，需要更新一些配置文件。

在 MyFixIt.WorkerRole\app.config 中的下 `connectionStrings` ，将连接字符串的值替换 `appdb` 为 SQL 数据库的实际连接字符串。 可以从门户获取连接字符串。 在门户中，单击 " **sql 数据库**" "appdb" "  -  **appdb**  -  **查看 ADO .net、ODBC、PHP 和 JDBC 的 sql 数据库连接字符串**"。 复制 ADO.NET 连接字符串，并将值粘贴到 app.config 文件中。 \_用您的数据库密码替换 "{您在此处输入密码 \_ }"。  (假设你使用脚本来部署 MVC 应用，则在脚本参数中指定了数据库密码 `SqlDatabasePassword` 。 ) 

结果应该如下所示：

[!code-xml[Main](the-fix-it-sample-application/samples/sample32.xml)]

在同一 MyFixIt.WorkerRole\app.config 文件中的下， `appSettings` 将 Azure 存储帐户的两个占位符值替换为。

[!code-xml[Main](the-fix-it-sample-application/samples/sample33.xml?highlight=2-3)]

可以从门户获取访问密钥。 请参阅 [如何管理存储帐户](https://docs.microsoft.com/azure/storage/common/storage-create-storage-account)。

在 MyFixItCloudService\ServiceConfiguration.Cloud.cscfg 中，将相同的两个占位符值替换为 Azure 存储帐户。

[!code-xml[Main](the-fix-it-sample-application/samples/sample34.xml?highlight=3)]

现在，你已准备好部署云服务。 在解决方案浏览器中，右键单击 MyFixItCloudService 项目，然后选择 " **发布**"。 有关详细信息，请参阅[本教程](https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36)第2部分中的 "将[应用程序部署到 Azure](https://www.windowsazure.com/develop/net/tutorials/multi-tier-web-site/2-download-and-run/#deployAz)"。

> [!div class="step-by-step"]
> [上一页](more-patterns-and-guidance.md)

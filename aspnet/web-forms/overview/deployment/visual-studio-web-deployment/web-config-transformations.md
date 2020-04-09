---
uid: web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations
title: 使用可视化工作室ASP.NET Web 部署：Web.config 文件转换 |微软文档
author: tdykstra
description: 本教程系列介绍如何将ASP.NET Web 应用程序部署到 Azure 应用服务 Web 应用或第三方托管提供商（由 usin...
ms.author: riande
ms.date: 02/15/2013
ms.assetid: 5a2a927b-14cb-40bc-867a-f0680f9febd7
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations
msc.type: authoredcontent
ms.openlocfilehash: a9d39547c94a63003442ba6fe1257693dde24b05
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675747"
---
# <a name="aspnet-web-deployment-using-visual-studio-webconfig-file-transformations"></a>使用可视化工作室ASP.NET Web 部署：Web.config 文件转换

汤姆[·戴克斯特拉](https://github.com/tdykstra)

[下载初学者项目](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> 本教程系列介绍如何使用 Visual Studio 2012 或 Visual Studio 2010 将ASP.NET Web 应用程序部署到 Azure 应用服务 Web 应用或第三方托管提供商。 有关该系列的信息，请参阅[系列中的第一个教程](introduction.md)。

## <a name="overview"></a>概述

本教程介绍如何在将*Web.config 文件部署到*不同目标环境时自动执行更改 Web.config 文件的过程。 大多数应用程序在*Web.config 文件中*具有设置，在部署应用程序时必须不同。 自动进行这些更改的过程使每次部署时都不必手动执行这些更改，这非常繁琐且容易出错。

提醒：如果您收到错误消息或内容在浏览本教程时不起作用，请务必查看[故障排除页面](troubleshooting.md)。

## <a name="webconfig-transformations-versus-web-deploy-parameters"></a>Web.配置转换与 Web 部署参数

有两种方法可以自动更改*Web.config*文件设置的过程[：Web.config 转换](https://msdn.microsoft.com/library/dd465326.aspx)和[Web 部署参数](https://msdn.microsoft.com/library/ff398068.aspx)。 *Web.config*转换文件包含 XML 标记，用于指定在部署*Web.config*文件时如何更改该文件。 您可以为特定生成配置和特定发布配置文件指定不同的更改。 默认生成配置是调试和发布，您可以创建自定义生成配置。 发布配置文件通常对应于目标环境。 （您将了解有关在["作为测试环境"教程部署到 IIS](deploying-to-iis.md)中的发布配置文件的更多信息。

Web Deploy 参数可用于指定在部署期间必须配置的许多不同类型的设置，包括*Web.config 文件中*的设置。 当用于指定*Web.config*文件更改时，Web Deploy 参数的设置更为复杂，但在部署之前不知道要设置的值时，这些参数很有用。 例如，在企业环境中，您可以创建*部署包*并将其交给 IT 部门的人员以在生产中安装，并且此人必须能够输入您不知道的连接字符串或密码。

对于本教程系列介绍的方案，您事先知道必须对*Web.config*文件执行的所有操作，因此无需使用 Web Deploy 参数。 您将配置一些因所使用的生成配置而异的转换，以及一些因使用的发布配置文件而异的转换。

<a id="watransforms"></a>

## <a name="specifying-webconfig-settings-in-azure"></a>在 Azure 中指定 Web.配置设置

如果要更改的*Web.config*文件设置位于`<connectionStrings>`或`<appSettings>`元素中，并且如果要在 Azure 应用服务中部署到 Web 应用，则可以在部署期间自动更改另一个选项。 您可以在 Web 应用的管理门户页的 **"配置"** 选项卡中输入要在 Azure 中生效的设置（向下滚动到**应用设置**和**连接字符串**部分）。 部署项目时，Azure 会自动应用更改。 有关详细信息，请参阅[Windows Azure 网站：应用程序字符串和连接字符串的工作原理](https://blogs.msdn.com/b/windowsazure/archive/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work.aspx)。

## <a name="default-transformation-files"></a>默认转换文件

在**解决方案资源管理器**中，展开*Web.config*以查看*Web.Debug.config*和*Web.Release.config*为两个默认生成配置默认创建的转换文件。

![Web.config_transform_files](web-config-transformations/_static/image1.png)

您可以通过右键单击 Web.config 文件并从上下文菜单中选择 **"添加配置转换"** 来创建自定义生成配置的转换文件。 对于本教程，您不需要执行此操作，并且菜单选项已禁用，因为您尚未创建任何自定义生成配置。

稍后，您将再创建三个转换文件，每个文件用于测试、暂存和生产发布配置文件。 在发布配置文件转换文件中处理的设置的典型示例是 WCF 终结点，用于测试和生产。 在创建与它们一起的发布配置文件后，您将在以后的教程中创建发布配置文件转换文件。

## <a name="disable-debug-mode"></a>禁用调试模式

属性是依赖于生成配置而不是目标环境的设置示例`debug`。 对于发布生成，您通常希望禁用调试，而不管要部署到哪个环境。 因此，默认情况下，Visual Studio 项目模板创建*Web.Release.config*转换文件，这些转换`debug`文件的代码从`compilation`元素中删除该属性。 下面是默认的*Web.Release.config*：除了注释掉的一些示例转换代码外，它还在`compilation`元素中包括删除`debug`属性的代码：

[!code-xml[Main](web-config-transformations/samples/sample1.xml?highlight=18)]

该`xdt:Transform="RemoveAttributes(debug)"`属性指定您希望从已部署`debug`的`system.web/compilation`*Web.config*文件中的元素中删除该属性。 这将在每次部署发布版本时完成。

## <a name="limit-error-log-access-to-administrators"></a>限制对管理员的错误日志访问

如果应用程序运行时出现错误，应用程序将显示一个通用错误页，以代替系统生成的错误页，并且它使用[Elmah NuGet 包](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx)进行错误日志记录和报告。 应用程序`customErrors` *Web.config*文件中的元素指定错误页：

[!code-xml[Main](web-config-transformations/samples/sample2.xml)]

要查看错误页，请暂时将`mode``customErrors`元素的属性从"仅远程"更改为"打开"，并从 Visual Studio 运行应用程序。 通过请求无效 URL（如*学生xxx.aspx）* 导致错误。 您看到的不是 IIS 生成的"找不到资源"错误页，而是看到*泛错误Page.aspx*页面。

![错误页](web-config-transformations/_static/image2.png)

要查看错误日志，请将端口号后 URL 中的所有内容替换为*elmah.axd（* 例如`http://localhost:51130/elmah.axd`），然后按 Enter：

![ELMAH 页面](web-config-transformations/_static/image3.png)

完成后，不要忘记将`customErrors`元素设置为"仅远程"模式。

在开发计算机上，允许免费访问错误日志页很方便，但在生产中，这将存在安全风险。 对于生产站点，要添加一个授权规则，该规则限制管理员对错误日志的访问，并确保该限制在测试和暂存中也正常工作。 因此，这是每次部署发布生成时要实现的另一个更改，因此它属于*Web.Release.config*文件。

打开*Web.Release.config，* 并在结束`location``configuration`标记之前添加新元素，如下所示。

[!code-xml[Main](web-config-transformations/samples/sample3.xml?highlight=27-34)]

属性`Transform`值"Insert"会导致此`location`元素作为同级添加到*Web.config*文件中的任何`location`现有元素。 （已经有一个`location`元素指定**更新积分**页的授权规则。

现在，您可以预览转换，以确保正确编码它。

在**解决方案资源管理器**中，右键单击*Web.Release.config，* 然后单击 **"预览转换**"。

![预览转换菜单](web-config-transformations/_static/image4.png)

将打开一个页面，显示左侧的开发*Web.config*文件以及部署的*Web.config*文件在右侧的外观，并突出显示更改。

![调试转换预览](web-config-transformations/_static/image5.png)

![位置转换预览](web-config-transformations/_static/image6.png)

（在预览中，您可能会注意到一些未为这些更改编写转换的其他更改：这些更改通常涉及删除不影响功能的空白。

部署后测试站点时，还将进行测试以验证授权规则是否有效。

> [!NOTE] 
> 
> **安全说明**切勿在生产应用程序中向公众显示错误详细信息，也不要将该信息存储在公共位置。 攻击者可以使用错误信息来发现站点中的漏洞。 如果您在自己的应用程序中使用 ELMAH，请配置 ELMAH 以最大程度地降低安全风险。 本教程中的 ELMAH 示例不应视为推荐的配置。 这是一个示例，用于说明如何处理应用程序必须能够在 中创建文件的文件夹。 有关详细信息，请参阅保护[ELMAH 终结点](https://code.google.com/p/elmah/wiki/SecuringErrorLogPages)。

## <a name="a-setting-that-youll-handle-in-publish-profile-transformation-files"></a>在发布配置文件转换文件中要处理的设置

常见方案是具有在部署到的每个环境中必须不同的*Web.config*文件设置。 例如，调用 WCF 服务的应用程序在测试和生产环境中可能需要不同的终结点。 康托索大学的申请还包括这种设置。 此设置控制网站页面上的可见指示器，该指示器告诉您处于哪个环境，例如开发、测试或生产。 设置值确定应用程序是否会将"（Dev）"或"（测试）"追加到*Site.master*页中的主标题：

![环境指示器](web-config-transformations/_static/image7.png)

当应用程序在暂存或生产中运行时，环境指示器将被省略。

Contoso 大学网页读取在*Web.config* `appSettings`文件中设置的值，以便确定应用程序在以下环境中运行的环境：

[!code-xml[Main](web-config-transformations/samples/sample4.xml)]

在测试环境中的值应为"测试"，对于暂存和生产来说应为"Prod"。

转换文件中的以下代码将实现此转换：

[!code-xml[Main](web-config-transformations/samples/sample5.xml)]

`xdt:Transform`属性值"SetAttributes"表示此转换的目的是更改*Web.config*文件中现有元素的属性值。 `xdt:Locator`属性值"Match（键）"表示要修改的元素是其`key`属性与此处指定的`key`属性匹配的元素。 元素的唯一`add`其他属性是`value`，这就是将在部署的*Web.config 文件中*更改的内容。 `value`此处显示的代码会导致`Environment``appSettings`元素的属性设置为部署的*Web.config*文件中的"Test"。

此转换属于尚未创建的发布配置文件转换文件。 在为测试、暂存和生产环境创建发布配置文件时，您将创建和更新实现此更改的转换文件。 您将在[部署到 IIS](deploying-to-iis.md)并[部署到生产](deploying-to-production.md)教程中执行此操作。

> [!NOTE]
> 由于此设置位于`<appSettings>`元素中，因此在本主题前面介绍的 Azure 中，在 Azure 应用服务中部署到 Web 应用时，还有另一种用于指定转换的替代方法。请参阅[在本主题前面指定 Azure 中的 Web.config 设置](#watransforms)。

## <a name="setting-connection-strings"></a>设置连接字符串

尽管默认转换文件包含一个示例，其中演示如何更新连接字符串，但在大多数情况下，您不需要设置连接字符串转换，因为您可以在发布配置文件中指定连接字符串。 您将在[部署到 IIS](deploying-to-iis.md)并[部署到生产](deploying-to-production.md)教程中执行此操作。

## <a name="summary"></a>总结

现在，在创建发布配置文件之前，您已经尽可能多地使用*Web.config*转换，并且您已经看到了部署的 Web.config 文件中的内容的预览。

![位置转换预览](web-config-transformations/_static/image8.png)

在下面的教程中，您将处理需要设置项目属性的部署设置任务。

## <a name="more-information"></a>更多信息

有关本教程涵盖的主题的详细信息，请参阅在 Visual Studio 和 ASP.NET的 Web 部署内容映射中[使用 Web.config 转换来更改目标 Web.config 文件或 app.config 文件中的设置](https://go.microsoft.com/fwlink/p/?LinkId=282413#transforms)。

> [!div class="step-by-step"]
> [上一页](preparing-databases.md)
> [下一页](project-properties.md)

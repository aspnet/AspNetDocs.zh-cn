---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/displaying-a-custom-error-page-vb
title: 显示自定义错误页（VB） |Microsoft Docs
author: rick-anderson
description: 当 ASP.NET web 应用程序中出现运行时错误时，用户将看到什么？ 答案取决于网站 &lt;customErrors&gt; 配置 ...。
ms.author: riande
ms.date: 06/09/2009
ms.assetid: 14873c5d-81a9-455b-bd71-30fb555583e7
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/displaying-a-custom-error-page-vb
msc.type: authoredcontent
ms.openlocfilehash: 33367d5e3c4b5c8fa039ee20704054ba508e717a
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74614964"
---
# <a name="displaying-a-custom-error-page-vb"></a>显示自定义错误页 (VB)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](https://download.microsoft.com/download/1/0/C/10CC829F-A808-4302-97D3-59989B8F9C01/ASPNET_Hosting_Tutorial_11_VB.zip)或[下载 PDF](https://download.microsoft.com/download/5/C/5/5C57DB8C-5DEA-4B3A-92CA-4405544D313B/aspnet_tutorial11_CustomErrors_vb.pdf)

> 当 ASP.NET web 应用程序中出现运行时错误时，用户将看到什么？ 答案取决于网站 &lt;customErrors&gt; 配置的方式。 默认情况下，用户显示一个 proclaiming 的黄色屏幕，指出运行时错误。 本教程介绍如何自定义这些设置，以显示具的自定义错误页面，该页面与你的站点的外观匹配。

## <a name="introduction"></a>简介

在完美的世界中，不会出现运行时错误。 程序员将编写带有 bug 的代码，并提供可靠的用户输入验证，并且数据库服务器和电子邮件服务器等外部资源将永远不会脱机。 当然，事实错误是不可避免的。 .NET Framework 中的类通过引发异常来指示错误。 例如，调用 SqlConnection 对象的 Open 方法会建立与连接字符串所指定的数据库的连接。 但是，如果数据库关闭或连接字符串中的凭据无效，则 Open 方法会引发 `SqlException`。 可以通过使用 `Try/Catch/Finally` 块处理异常。 如果 `Try` 块内的代码引发异常，控制将被传输到相应的 catch 块，开发人员可在其中尝试从错误中恢复。 如果没有匹配的 catch 块，或者引发异常的代码不在 try 块中，则异常在 `Try/Catch/Finally` 块搜索中 percolates 调用堆栈。

如果在不进行处理的情况下，异常冒泡到 ASP.NET 运行时，则会引发[`HttpApplication` 类](https://msdn.microsoft.com/library/system.web.httpapplication.aspx)的[`Error` 事件](https://msdn.microsoft.com/library/system.web.httpapplication.error.aspx)，并显示配置的*错误页*。 默认情况下，ASP.NET 会显示一个错误页面，该页面称为 affectionately （YSOD）的[黄屏](http://en.wikipedia.org/wiki/Yellow_Screen_of_Death#Yellow)。 YSOD 有两个版本：一个用于显示异常详细信息、一个堆栈跟踪以及其他对开发人员调试应用程序有用的信息（请参阅**图 1**）;另一种情况只是指出存在运行时错误（参见**图 2**）。

异常详细信息 YSOD 对于调试应用程序的开发人员非常有用，但向最终用户显示 YSOD 为 tacky 和 unprofessional。 相反，应将最终用户转到一个错误页面，该页面使用描述此情况的更多用户友好 prose 维护站点的外观和感觉。 好消息是，创建此类自定义错误页非常简单。 本教程首先介绍 ASP。网络的不同错误页。 然后，该示例演示如何配置 web 应用程序，以便在遇到错误时向用户显示自定义错误页。

### <a name="examining-the-three-types-of-error-pages"></a>检查三种类型的错误页

当 ASP.NET 应用程序中出现未处理的异常时，将显示以下三种类型的错误页之一：

- 异常详细信息 "死亡错误" 页的黄色屏幕，
- 运行时错误的黄色屏幕出现死亡错误页面，或
- 自定义错误页

最熟悉的错误页开发人员是 YSOD 的异常详细信息。 默认情况下，此页将向本地访问的用户显示，因此，这是在开发环境中测试网站时出现错误时看到的页面。 顾名思义，异常详细信息 YSOD 提供有关异常的详细信息-类型、消息和堆栈跟踪。 此外，如果异常由 ASP.NET 页的代码隐藏类中的代码引发，并且如果将应用程序配置为进行调试，则异常详细信息 YSOD 还将显示这行代码（以及上面和下面的几行代码）。

**图 1**显示了异常详细信息 YSOD 页。 请注意浏览器地址窗口中的 URL： `http://localhost:62275/Genre.aspx?ID=foo`。 回忆一下，"`Genre.aspx`" 页将列出特定流派的书籍评论。 它要求通过 querystring 传递 `GenreId` 值（`uniqueidentifier`）;例如，用于查看小说评审的相应 URL 是 `Genre.aspx?ID=7683ab5d-4589-4f03-a139-1c26044d0146`。 如果非`uniqueidentifier` 值通过查询字符串（如 "foo"）传入，则会引发异常。

> [!NOTE]
> 若要在可供下载的演示 web 应用程序中重现此错误，可以直接访问 `Genre.aspx?ID=foo` 或单击 `Default.aspx`中的 "生成运行时错误" 链接。

请注意**图 1**中显示的异常信息。 页面顶部显示异常消息 "将字符串转换为 uniqueidentifier 时转换失败"。 还列出了 `System.Data.SqlClient.SqlException`的异常类型。 还有堆栈跟踪。

[![](displaying-a-custom-error-page-vb/_static/image2.png)](displaying-a-custom-error-page-vb/_static/image1.png)

**图 1**：异常详细信息 YSOD 包含有关异常的信息  
 （[单击以查看完全大小的映像](displaying-a-custom-error-page-vb/_static/image3.png)）

另一种类型的 YSOD 是运行时错误 YSOD，如**图 2**所示。 运行时错误 YSOD 通知访问者发生了运行时错误，但它不包含有关所引发异常的任何信息。 （但是，它还提供了有关如何通过修改 `Web.config` 文件来查看错误详细信息的说明，这是 YSOD 的外观 unprofessional 的一部分。）

默认情况下，会向远程访问的用户显示运行时错误 YSOD （通过 http://www.yoursite.com) ，如**图 2**： `http://httpruntime.web703.discountasp.net/Genre.aspx?ID=foo` 的浏览器地址栏中的 URL 出现。 存在两个不同的 YSOD 屏幕，因为开发人员对了解错误详细信息感兴趣，但不应在实时站点上显示此类信息，因为它可能会向访问你的网站.

> [!NOTE]
> 如果你正在使用并使用 DiscountASP.NET 作为你的 web 主机，你可能会注意到，访问实时站点时，YSOD 不会显示运行时错误。 这是因为，DiscountASP.NET 将其服务器配置为默认显示异常详细信息 YSOD。 好消息是，可以通过向 `Web.config` 文件添加 `<customErrors>` 节来覆盖此默认行为。 "配置显示的错误页" 部分详细介绍了 `<customErrors>` 部分。

[![](displaying-a-custom-error-page-vb/_static/image5.png)](displaying-a-custom-error-page-vb/_static/image4.png)

**图 2**：运行时错误 YSOD 不包括任何错误详细信息  
 （[单击以查看完全大小的映像](displaying-a-custom-error-page-vb/_static/image6.png)）

第三种类型的错误页是自定义错误页，这是你创建的网页。 自定义错误页的优点在于，您可以完全控制向用户显示的信息以及页面的外观;自定义错误页可以使用与其他页相同的母版页和样式。 "使用自定义错误页" 一节介绍了如何创建自定义错误页，并将其配置为在发生未经处理的异常时显示。 **图 3**提供此自定义错误页的抢先了解峰值。 正如您所看到的，"错误" 页的外观比图1和图2中所示的任何一个黄色屏幕都具有专业水准。

[![](displaying-a-custom-error-page-vb/_static/image8.png)](displaying-a-custom-error-page-vb/_static/image7.png)

**图 3**：自定义错误页提供更好的外观和感觉  
 （[单击以查看完全大小的映像](displaying-a-custom-error-page-vb/_static/image9.png)）

请花点时间检查**图 3**中的浏览器地址栏。 请注意，地址栏会显示自定义错误页（`/ErrorPages/Oops.aspx`）的 URL。 在图1和图2中，死机的黄色屏幕显示在错误源自的同一页中（`Genre.aspx`）。 自定义错误页通过 `aspxerrorpath` querystring 参数传递了错误的页的 URL。

## <a name="configuring-which-error-page-is-displayed"></a>配置显示的错误页

显示三个可能的错误页中的哪一种取决于两个变量：

- `<customErrors>` 部分中的配置信息，以及
- 用户是否正在本地或远程访问站点。

`Web.config` 中的[`<customErrors>` 节](https://msdn.microsoft.com/library/h0hfz6fc.aspx)包含两个特性，这些特性会影响显示的错误页： `defaultRedirect` 和 `mode`。 `defaultRedirect` 属性是可选项。 如果提供，它将指定自定义错误页的 URL，并指示应显示自定义错误页，而不是运行时错误 YSOD。 `mode` 属性是必需的，并接受以下三个值之一： `On`、`Off`或 `RemoteOnly`。 这些值具有以下行为：

- `On`-表示向所有访问者显示自定义错误页或运行时错误 YSOD，无论它们是本地的还是远程的。
- `Off`-指定是否向所有访问者显示异常详细信息，无论它们是本地还是远程。
- `RemoteOnly`-表示向远程访问者显示自定义错误页或运行时错误 YSOD，而异常详细信息 YSOD 显示给本地访问者。

除非另外指定，否则 ASP.NET 的行为就像您已将 mode 特性设置为 `RemoteOnly` 并且未指定 `defaultRedirect` 值。 换句话说，默认行为是向远程访问者显示运行时错误 YSOD 时向本地访问者显示异常详细信息 YSOD。 可以通过将 `<customErrors>` 部分添加到 web 应用程序的 `Web.config file.` 来覆盖此默认行为

## <a name="using-a-custom-error-page"></a>使用自定义错误页

每个 web 应用程序都应具有自定义错误页。 它为运行时错误 YSOD 提供更专业的替代方法，可以轻松创建和配置应用程序以使用自定义错误页，只需几分钟即可完成。 第一步是创建自定义错误页。 我已向书籍中添加了一个新文件夹，审阅名为 `ErrorPages` 的应用程序并将其添加到了名为 `Oops.aspx`的新 ASP.NET 页面。 让页面使用与站点上的其余页面相同的母版页，使其自动继承相同的外观。

[![](displaying-a-custom-error-page-vb/_static/image11.png)](displaying-a-custom-error-page-vb/_static/image10.png)

**图 4**：创建自定义错误页

接下来，花几分钟时间创建错误页面的内容。 我已经创建了一个简单的自定义错误页，其中包含一条消息，指示出现意外错误和指向网站主页的链接。

[![](displaying-a-custom-error-page-vb/_static/image13.png)](displaying-a-custom-error-page-vb/_static/image12.png)

**图 5**：设计自定义错误页  
 （[单击以查看完全大小的映像](displaying-a-custom-error-page-vb/_static/image14.png)）

完成错误页面后，将 web 应用程序配置为使用自定义错误页，而不是运行时错误 YSOD。 这是通过在 `<customErrors>` 节的 `defaultRedirect` 属性中指定错误页面的 URL 来实现的。 将以下标记添加到应用程序的 `Web.config` 文件：

[!code-xml[Main](displaying-a-custom-error-page-vb/samples/sample1.xml)]

上述标记将应用程序配置为向本地访问的用户显示异常详细信息，同时对这些用户使用自定义错误页 YSOD 进行远程访问。 若要查看此操作，请将你的网站部署到生产环境，然后访问具有无效 querystring 值的实时网站上的 "流派" 页。 应会看到自定义错误页（请参阅**图 3**）。

若要验证自定义错误页仅向远程用户显示，请访问开发环境中具有无效 querystring 的 `Genre.aspx` 页。 你仍应看到异常详细信息 YSOD （请参阅**图 1**）。 `RemoteOnly` 设置确保在生产环境中访问站点的用户可以看到自定义错误页，而在本地工作的开发人员仍可继续查看异常的详细信息。

## <a name="notifying-developers-and-logging-error-details"></a>通知开发人员和日志记录错误详细信息

开发环境中出现的错误是由其计算机上的开发人员导致的。 她在异常详细信息 YSOD 中显示了异常信息，她知道发生错误时，她执行了哪些步骤。 但在生产上发生错误时，开发人员不知道发生了错误，除非访问该站点的最终用户需要时间报告该错误。 即使用户退出向开发团队提醒开发团队发生了错误，但却不知道异常类型、消息和堆栈跟踪，这可能很难诊断错误的原因，让我们将其修复。

由于这些原因，生产环境中的任何错误都记录到某些持久性存储区（如数据库），这是非常重要的，因此，开发人员会收到此错误的警报。 自定义错误页可能看起来像是执行此日志记录和通知的好地方。 遗憾的是，自定义错误页不能访问错误详细信息，因此不能用于记录此信息。 好消息是，有多种方法可以截获错误详细信息和记录它们，接下来的三个教程将更详细地探讨此主题。

## <a name="using-different-custom-error-pages-for-different-http-error-statuses"></a>针对不同的 HTTP 错误状态使用不同的自定义错误页

当 ASP.NET 页引发异常且未进行处理时，异常 percolates 为 ASP.NET 运行时，这将显示配置的错误页。 如果请求进入 ASP.NET 引擎，但由于某种原因而无法处理该请求，可能是因为找不到请求的文件或已禁用对该文件的读取权限，则 ASP.NET 引擎会引发 `HttpException`。 此异常（如 ASP.NET 页面引发的异常）冒泡到运行时，导致显示相应的错误页。

对于生产环境中的 web 应用程序而言，这意味着，如果用户请求找不到的页面，则他们将看到自定义错误页。 **图 6**显示了这样一个示例。 由于请求是针对不存在的页（`NoSuchPage.aspx`），因此将引发 `HttpException` 并显示自定义错误页（请注意，`aspxerrorpath` querystring 参数中对 `NoSuchPage.aspx` 的引用）。

[![](displaying-a-custom-error-page-vb/_static/image16.png)](displaying-a-custom-error-page-vb/_static/image15.png)**图 6**： ASP.NET 运行时显示配置的错误页，以响应无效的请求  
 （[单击以查看完全大小的映像](displaying-a-custom-error-page-vb/_static/image17.png)） 

默认情况下，所有类型的错误都将导致显示相同的自定义错误页。 但是，您可以使用 `<customErrors>` 部分中 `<error>` 的子元素为特定的 HTTP 状态代码指定一个不同的自定义错误页。 例如，若要在具有 HTTP 状态代码404的 "找不到页" 错误事件中显示不同的错误页，请更新 `<customErrors>` 部分以包括以下标记：

[!code-xml[Main](displaying-a-custom-error-page-vb/samples/sample2.xml)]

进行此更改后，每当用户访问远程请求不存在的 ASP.NET 资源时，它们将被重定向到 `404.aspx` 自定义错误页，而不是 `Oops.aspx`。 如**图 7**所示，`404.aspx` 页可以包含比 "常规自定义错误" 页更具体的消息。

> [!NOTE]
> 请查看[404 错误页，进一步了解](http://www.smashingmagazine.com/2009/01/29/404-error-pages-one-more-time/)如何创建有效的404错误页。

[![](displaying-a-custom-error-page-vb/_static/image19.png)](displaying-a-custom-error-page-vb/_static/image18.png)**图 7**： "自定义404错误" 页显示更具针对性的消息，而不是 `Oops.aspx`  
 （[单击以查看完全大小的映像](displaying-a-custom-error-page-vb/_static/image20.png)） 

因为你知道只有当用户对找不到的页面发出请求时才到达 `404.aspx` 页面，因此你可以增强此自定义错误页，以包含可帮助用户解决此特定类型的错误的功能。 例如，您可以构建一个数据库表，该表将已知的错误 Url 映射到正确的 Url，然后让 `404.aspx` 自定义错误页对该表运行查询并建议用户尝试访问的页面。

> [!NOTE]
> 仅当对由 ASP.NET 引擎处理的资源发出请求时，才会显示自定义错误页。 如我们在[IIS 与 ASP.NET 开发服务器教程之间的核心差异](core-differences-between-iis-and-the-asp-net-development-server-vb.md)中所述，web 服务器可能会自行处理某些请求。 默认情况下，IIS web 服务器处理静态内容（如图像和 HTML 文件）的请求，而不会调用 ASP.NET 引擎。 因此，如果用户请求不存在的图像文件，则会返回 IIS 默认的404错误消息，而不是 ASP。NET 的已配置错误页。

## <a name="summary"></a>总结

当 ASP.NET 应用程序中发生未处理的异常时，用户将显示以下三个错误页之一：异常详细信息：绿色的黄屏;运行时错误黄色屏幕死亡;或自定义错误页。 显示哪一错误页取决于应用程序的 `<customErrors>` 配置以及用户是在本地还是远程访问。 默认行为是向本地访问者和运行时错误 YSOD 显示 YSOD 的异常详细信息。

尽管运行时错误 YSOD 从访问站点的用户中隐藏潜在的敏感错误信息，但它会从网站的外观和感觉中中断，并使应用程序出现错误。 更好的方法是使用自定义错误页，该页面需要创建和设计自定义错误页，并在 `<customErrors>` 节的 `defaultRedirect` 属性中指定其 URL。 甚至可以针对不同的 HTTP 错误状态使用多个自定义错误页。

自定义错误页是针对生产环境中网站的综合性错误处理策略的第一步。 警告开发人员出现错误并记录其详细信息也是重要的步骤。 接下来的三个教程探讨错误通知和日志记录的方法。

很高兴编程！

## <a name="further-reading"></a>其他阅读材料

有关本教程中讨论的主题的详细信息，请参阅以下资源：

- [错误页，一次](http://www.smashingmagazine.com/2009/01/29/404-error-pages-one-more-time/)
- [异常的设计准则](https://msdn.microsoft.com/library/ms229014.aspx)
- [用户友好的错误页](http://aspnet.4guysfromrolla.com/articles/090606-1.aspx)
- [处理和引发异常](https://msdn.microsoft.com/library/5b2yeyab.aspx)
- [正确使用 ASP.NET 中的自定义错误页](http://professionalaspnet.com/archive/2007/09/30/Properly-Using-Custom-Error-Pages-in-ASP.NET.aspx)

> [!div class="step-by-step"]
> [上一页](strategies-for-database-development-and-deployment-vb.md)
> [下一页](processing-unhandled-exceptions-vb.md)

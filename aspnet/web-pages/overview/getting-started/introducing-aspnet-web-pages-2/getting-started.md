---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/getting-started
title: 入门 | Microsoft Docs
author: Rick-Anderson
description: WebMatrix 不再建议作为 ASP.NET 网页的集成开发环境。 使用 Visual Studio 或 Visual Studio Code。 本指南 .。。
ms.author: riande
ms.date: 05/28/2015
ms.assetid: a36d3bdf-ef1b-47a4-b932-3a0cf4cad716
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/getting-started
msc.type: authoredcontent
ms.openlocfilehash: ac2111980e6393388a0530375fb9ef78dbbfaff6
ms.sourcegitcommit: 0cf7d06071a8ff986e6c028ac9daf0c0e7490412
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/23/2020
ms.locfileid: "85240763"
---
# <a name="getting-started"></a>入门

 作者 [Tom FitzMacken](https://github.com/tfitzmac)

[!INCLUDE[](~/includes/rp.md)]

> > [!NOTE] 
> > 
> > WebMatrix 不再建议作为 ASP.NET 网页的集成开发环境。 使用[Visual Studio](../program-asp-net-web-pages-in-visual-studio.md)或[Visual Studio Code](https://code.visualstudio.com/)。
> 
> 
> 本指南和应用程序提供 ASP.NET 网页（版本2或更高版本）和 Razor 语法（用于创建动态网站的轻型框架）的概述。 它还引入了 WebMatrix，这是用于创建页面和站点的工具。
> 
> **Level**： New to ASP.NET 网页。  
> **假定的技能**： HTML、基本级联样式表（CSS）。
> 
> 你将在该集的第一个教程中学习以下内容：
> 
> - 什么是 ASP.NET 网页技术，它的作用是什么。
> - WebMatrix 是什么。
> - 如何安装所有内容。
> - 如何使用 WebMatrix 创建网站。
>   
> 
> 介绍的功能/技术：
> 
> - Microsoft Web 平台安装程序。
> - WebMatrix.
> - *cshtml*页
>   
> 
> Mike Pope 最初编写本教程。 Tom FitzMacken 对 Microsoft WebMatrix 3 进行了更新。
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>本教程中使用的软件版本
> 
> 
> - ASP.NET 网页（Razor）2
> - WebMatrix 3

## <a name="what-should-you-know"></a>你应该知道哪些内容？

假设你熟悉以下内容：

- **HTML**。 不需要深入的专业技能。 我们不会解释 HTML，但也不会使用任何复杂的内容。 我们将提供 HTML 教程的链接，在这些教程中，我们认为它们非常有用。
- **级联样式表（CSS）**。 与 HTML 相同。
- **基本数据库思想**。 如果你使用了电子表格进行数据的排序和筛选，那么这就是我们通常为本教程设置的专业知识水平。

我们还假定你对学习基本编程感兴趣。 ASP.NET 网页使用称为 c # 的编程语言。 您无需在编程中使用任何背景，只需对其感兴趣。 如果你以前在网页中编写了任何 JavaScript，则会有许多背景知识。

请注意，如果你熟悉编程，你可能会发现，此教程最初会缓慢移动，同时我们会使新的程序员保持速度缓慢。 不过，在我们过去的几个教程中，将会有更少的基本编程说明，并将以更快的速度移动。

## <a name="what-do-you-need"></a>你需要什么？

以下是需要做好的准备：

- 运行 Windows 8、Windows 7、Windows Server 2008 或 Windows Server 2012 的计算机。
- 动态 internet 连接。
- 管理员权限（安装过程所必需的）。

## <a name="what-is-aspnet-web-pages"></a>什么是 ASP.NET 网页？

ASP.NET 网页是一个框架，可用于创建动态网页。 简单的 HTML 网页是静态的;其内容取决于页面中的固定 HTML 标记。 动态页面与使用 ASP.NET 网页创建的动态页面使你可以通过使用代码动态创建页面内容。

动态页面使你可以执行各种操作。 您可以使用窗体向用户提供输入，然后更改页面显示的内容或外观。 你可以从用户处获取信息，将其保存在数据库中，然后在以后列出。 你可以从你的站点发送电子邮件。 你可以与 web 上的其他服务（例如，映射服务）进行交互，并生成集成这些源中的信息的页面。

## <a name="what-is-webmatrix"></a>什么是 WebMatrix？

WebMatrix 是一种工具，可集成网页编辑器、数据库实用工具、用于测试页面的 web 服务器，以及用于将网站发布到 Internet 的功能。 WebMatrix 是免费的，易于安装和使用。 （它还适用于纯 HTML 页面以及 PHP 等其他技术。）

你实际上不*需要*使用 WebMatrix 来处理 ASP.NET 网页。 例如，您可以使用文本编辑器创建页面，并使用您有权访问的 web 服务器来测试页面。 不过，WebMatrix 使其变得非常简单，因此这些教程将在整个过程中使用 WebMatrix。

## <a name="about-these-tutorials"></a>关于这些教程

本教程集介绍了如何使用 ASP.NET 网页。 此介绍性教程集中有9个教程总计。 这是一系列教程集的一部分，可让你从 ASP.NET 网页初级网站创建真实的、具有专业外观的网站。

这首个教程集重点介绍了如何使用 ASP.NET 网页的基础知识。 完成此操作后，可以使用额外的教程集，该教程集选择该程序集的结尾，更深入地浏览网页。

我们特意了解更深入的说明。 无论何时，对于本教程，我们始终都选择最容易理解的方式。 稍后的教程集将深入了解更多，并显示更高效或更灵活的方法（也更有趣）。 但这些教程要求首先了解基础知识。

刚开始的教程集介绍了 ASP.NET 网页的这些功能：

- 简介并获取安装的所有内容。 （在阅读教程中。）
- ASP.NET 网页编程的基础知识。
- 创建数据库。
- 创建和处理用户输入窗体。
- 添加、更新和删除数据库中的数据。

## <a name="what-will-you-create"></a>你将创建哪些内容？

本教程集和后续教程将在网站上进行旋转，你可以在其中列出你喜欢的电影。 你将能够输入电影、进行编辑并列出它们。 下面是要在本教程集中创建的几个页面。 第一个示例显示要创建的电影列表页：

![显示电影列表的已完成影片应用](getting-started/_static/image1.png)

以下页面使你能够将新电影信息添加到你的网站：

![已完成显示 "添加电影" 页面的电影应用](getting-started/_static/image2.png)

后续教程将基于此集进行构建并添加更多功能，如上传图片、让用户登录、发送电子邮件以及与社交媒体集成。

## <a name="see-this-app-running-on-azure"></a>查看此应用在 Azure 上运行

要查看作为实时 web 应用运行的已完成站点吗？ 只需单击以下按钮，即可将应用程序的完整版本部署到 Azure 帐户。

[![](http://azuredeploy.net/deploybutton.png)](https://azuredeploy.net/?WT.mc_id=deploy_azure_aspnet&repository=https://github.com/tfitzmac/WebPagesMovies)

需要一个 Azure 帐户才能将此解决方案部署到 Azure。 如果还没有帐户，可以使用以下选项：

- [免费打开 Azure 帐户](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604)-获取可用来试用付费版 Azure 服务的信用额度，甚至在用完信用额度后，你仍可以保留帐户和使用免费的 azure 服务。
- [激活 msdn 订户权益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604)-msdn 订阅每月提供可用于付费 Azure 服务的信用额度。

## <a name="installing-everything"></a>安装一切

你可以使用 Microsoft 的 Web 平台安装程序安装所有内容。 实际上，你安装了安装程序，然后使用它来安装其他所有内容。

若要使用网页，至少需要安装 Windows XP SP3 或 Windows Server 2008 或更高版本。

在 ASP.NET 网站的 "网页"[页](../../../index.md)上，单击 "**安装**"。

![显示 " &quot; 安装 WebMatrix" 按钮的 ASP.NET 网站 &quot;](getting-started/_static/image3.png)

安装 WebMatrix 之前，系统会要求你接受许可条款和隐私声明。

![接受字词开始安装](getting-started/_static/image4.png)

单击 "**运行**" 以启动安装。 （如果要保存该安装程序，请单击 "**保存**"，然后从保存该安装程序的文件夹运行该安装程序。）

![](getting-started/_static/image5.png)

此时会显示 "Web 平台安装程序"，可以安装 WebMatrix 了。 单击“安装”。

![](getting-started/_static/image6.png)

安装过程将找出必须在计算机上安装的内容，然后启动该过程。 根据确切安装的内容，该过程可能需要几分钟到几分钟的时间。 选择 "**我接受**" 接受许可条款。

## <a name="hello-webmatrix"></a>你好，WebMatrix

完成后，安装过程可以自动启动 WebMatrix。 如果不是，在 Windows 中，从 "**开始**" 菜单启动 " **Microsoft WebMatrix**"。

首次启动 WebMatrix 时，有机会使用 Microsoft 帐户登录到 Microsoft Azure。 登录后，你将通过 Azure 接收10个免费的 web 应用。 这些免费的 web 应用提供了一种方便的方法来测试你的应用。 如果还没有 Azure 帐户，但有 MSDN 订阅，则可以[激活 msdn 订阅权益](https://www.windowsazure.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604)。 否则，只需花费几分钟就能创建一个免费试用帐户。 有关详细信息，请参阅 [Azure 免费试用](https://azure.microsoft.com/free/dotnet/)。

你现在无需登录即可继续学习本教程。 如果你现在不登录，则你仍可以选择在以后登录。 本系列教程的最后一个[主题](publishing.md)介绍如何将网站部署到 Azure;因此，您需要登录才能完成该主题。

此时，请用 Microsoft 帐户登录，或在右下角选择 "**不**是"。

![登录](getting-started/_static/image7.png)

首先，你将创建一个空白网站并添加一个页面。 在后面的教程中，你将使用一个内置的网站模板。

在 "开始" 窗口中，单击 "**新建**"。

![WebMatrix 启动屏幕](getting-started/_static/image8.png)

模板是为不同类型的网站预先构建的文件和页。 若要查看默认情况下可用的所有模板，请选择 "模板库" 选项。

![选择模板库](getting-started/_static/image9.png)

在 "**快速入门**" 窗口中，从**ASP.NET**组中选择 "**空站点**"，并将新站点命名为 "WebPagesMovies"。

![选定了空站点模板的 WebMatrix 快速入门窗口](getting-started/_static/image10.png)

单击“下一步”。

如果已登录到 Microsoft 帐户，则可以在 Azure 上创建网站。 根据你的站点的名称，建议默认名称**WebPagesMovies.azurewebsites.net** ;但是，感叹号表示此名称在 Windows Azure 上不可用。 为简单起见，请选择 "**跳过**" 以跳过在 Azure 上立即创建网站。 稍后在本系列中，我们会将该站点发布到 Azure。

![创建 azure 站点](getting-started/_static/image11.png)

WebMatrix 创建并打开站点：

![在 WebMatrix 中打开的新 WebPagesMovies 网站](getting-started/_static/image12.png)

顶部有一个快速访问工具栏和一个功能区。 左下角显示工作区选择器，可在其中切换任务（**站点**、**文件**、**数据库**、**报表**）。 右侧是编辑器和报表的内容窗格。 在底部，你将偶尔看到消息的通知栏。

完成这些教程后，你将了解有关 WebMatrix 及其功能的详细信息。

## <a name="creating-a-web-page"></a>创建网页

为了熟悉 WebMatrix 和 ASP.NET 网页，你将创建一个简单的页面。

在工作区选择器中，选择 "**文件**" 工作区。 使用此工作区可以处理文件和文件夹。 左窗格显示了站点的文件结构。 功能区更改为显示与文件相关的任务。

![WebMatrix 中的文件工作区](getting-started/_static/image13.png)

在功能区中，单击 "**新建**" 下的箭头，然后单击 "**新建文件**"。

![使用 &quot; 功能区中的 "新建" &quot; 命令创建新文件](getting-started/_static/image14.png)

WebMatrix 显示文件类型的列表。 选择 " **CSHTML**"，然后在 "**名称**" 框中，键入 "HelloWorld"。 CSHTML 页面是 ASP.NET 网页页面。

![创建名为 HelloWorld 的新 CSHTML 页](getting-started/_static/image15.png)

单击“确定”。

WebMatrix 创建页面并在编辑器中打开它。

![WebMatrix 编辑器中的新 "HelloWorld" 页](getting-started/_static/image16.png)

正如您所看到的，页面通常包含普通的 HTML 标记，其中顶部的块如下所示：

[!code-cshtml[Main](getting-started/samples/sample1.cshtml)]

这就是添加代码的，正如您很快所见。

请注意， &mdash; 元素名称、属性和文本以及顶部块的不同部分均采用不同的颜色。 这称为*语法突出显示*，使所有内容保持清晰。 这是一项功能，使用它可以轻松地在 WebMatrix 中使用网页。

为 `<head>` 和元素添加内容， `<body>` 如以下示例中所示。 （如果需要，可以只复制以下块，并将整个现有页面替换为此代码。）

[!code-cshtml[Main](getting-started/samples/sample2.cshtml)]

在快速访问工具栏或 "**文件**" 菜单中，单击 "**保存**"。

![WebMatrix 快速访问工具栏中的 "保存" 按钮](getting-started/_static/image17.png)

## <a name="testing-the-page"></a>测试页面

在 "**文件**" 工作区中，右键单击 " *HelloWorld* " 页，然后单击 "**在浏览器中启动**"。

![使用 WebMatrix 功能区中的 "运行" 按钮运行页面](getting-started/_static/image18.png)

WebMatrix 启动可用于在计算机上测试页面的内置 web 服务器（IIS Express）。 （无需在 WebMatrix 中 IIS Express，你必须将页面发布到 web 服务器上的某个位置，然后才能对其进行测试。）页面将显示在默认浏览器中。

![&quot;&quot;在浏览器中运行的 Hello World 页面](getting-started/_static/image19.png)

请注意，当你在 WebMatrix 中测试某个页面时，浏览器中的 URL 类似于 `http://localhost:33651/HelloWorld.cshtml.` 名称*localhost* ，这就是指本地服务器，这意味着该页由你自己的计算机上的 web 服务器提供服务。 如上所述，WebMatrix 包含一个名为 IIS Express 的 web 服务器程序，该程序在启动页面时运行。

*Localhost*后面的数字（例如*localhost： 33651*）是指计算机上的*端口号*。 这是 IIS Express 用于此特定网站的 "通道" 号。 创建站点时，从1024到65536的范围内随机选择端口号，而创建的每个站点都是不同的。 （测试自己的站点时，端口号几乎肯定会与33561不同。）通过为每个网站使用不同的端口，IIS Express 可以使其与你的站点直接通信。

稍后，当你将站点发布到公共 web 服务器时，你将不会再看到 URL 中的*localhost* 。 此时，您将看到更典型的 URL，例如 `http://myhostingsite/mywebsite/HelloWorld.cshtml` 或页面的任何内容。 你将在本系列教程的后面部分了解有关发布站点的详细信息。

## <a name="adding-some-server-side-code"></a>添加一些服务器端代码

关闭浏览器并返回到 WebMatrix 中的页面。

在代码块中添加一行，使其类似于以下代码：

[!code-cshtml[Main](getting-started/samples/sample3.cshtml)]

这只是一些 Razor 代码。 很明显，它会获取当前日期和时间，并将该值放入名为的*变量*中 `currentDateTime` 。 你将在下一教程中详细了解 Razor 语法。

在页面的正文中，在元素后面 `<p>Hello World!</p>` 添加以下内容：

[!code-html[Main](getting-started/samples/sample4.html)]

此代码将获取在顶部置于变量中的值 `currentDateTime` ，并将其插入到页面的标记中。 `@`字符标记页面中的 ASP.NET 网页代码。

再次运行页面（WebMatrix 会在运行页面之前保存更改）。 此时会在页面中看到日期和时间。

![&quot;&quot;在浏览器中运行的 Hello World 页面，其中包含动态生成的时间显示](getting-started/_static/image20.png)

稍等片刻，然后在浏览器中刷新页面。 更新日期和时间。

在浏览器中，查看页面源。 它类似于以下标记：

[!code-html[Main](getting-started/samples/sample5.html)]

请注意， `@{ }` 顶部的块不存在。 另请注意，"日期和时间" 显示将显示实际的字符串（ `1/18/2012 2:49:50 PM` 或任何内容），而不是 `@currentDateTime` 像在 *.* # 页中一样。 这里发生的情况是，当你运行页面时，ASP.NET 处理了标记为的所有代码（在此例中很少） `@` 。 此代码生成输出，并将输出插入到页面中。

## <a name="this-is-what-aspnet-web-pages-are-about"></a>这就是 ASP.NET 网页的内容

当你阅读该 ASP.NET 网页生成动态 Web 内容时，你在这里看到的就是这种想法。 刚创建的页面包含之前看到的相同 HTML 标记。 它还可以包含可执行各种任务的代码。 在此示例中，它是获取当前日期和时间的简单任务。 正如您所看到的，可以在页面中点播带有 HTML 的代码以生成输出。 当某个人请求浏览器中的*ASP.NET 页时*，会在该页面仍处于 web 服务器时对其进行处理。 ASP.NET 将代码（如果有）的输出作为 HTML 插入到页面中。 完成代码处理后，ASP.NET 会将生成的页发送到浏览器。 所有浏览器都是 HTML。 下面是一个关系图：

![ASP.NET 如何动态生成 HTML 的概念流](getting-started/_static/image21.png)

思路很简单，但代码可以执行很多有趣的任务，并且可以通过许多有趣的方式将 HTML 内容动态添加到页面中。 和 ASP.NET 页面（如任何*HTML 页面）* 也可以包含在浏览器中运行的代码（JavaScript 和 jQuery 代码）。 你将在本教程集中以及后续项目中浏览所有这些功能。

## <a name="coming-up-next"></a>下一步

在本系列的下一个教程中，您将探讨 ASP.NET 网页编程。

## <a name="additional-resources"></a>其他资源

[从头开始创建 ASP.NET 网站](https://www.microsoft.com/web/post/create-an-aspnet-website-from-scratch)。 本教程专门介绍如何使用 WebMatrix （不 ASP.NET 网页）。 本文更详细地介绍了 WebMatrix 的一些其他功能，我们不会在本教程集中介绍。

> [!div class="step-by-step"]
> [下一页](intro-to-web-pages-programming.md)

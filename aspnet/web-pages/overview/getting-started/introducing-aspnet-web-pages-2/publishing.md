---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/publishing
title: 简介 ASP.NET 网页-通过使用 WebMatrix 发布站点 |Microsoft Docs
author: Rick-Anderson
description: 本教程是介绍 ASP.NET 网页和 Microsoft WebMatrix 的教程集的最后一部分。 本文介绍了如何发布站点 t .。。
ms.author: riande
ms.date: 05/28/2015
ms.assetid: 7e85c70e-1a88-4408-8b3d-29611c7713ed
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/publishing
msc.type: authoredcontent
ms.openlocfilehash: a09339a833ea0b4a2d3c3a9323cce777577ea048
ms.sourcegitcommit: 0cf7d06071a8ff986e6c028ac9daf0c0e7490412
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/23/2020
ms.locfileid: "85240593"
---
# <a name="introducing-aspnet-web-pages---publishing-a-site-by-using-webmatrix"></a>简介 ASP.NET 网页-通过使用 WebMatrix 发布站点

 作者 [Tom FitzMacken](https://github.com/tfitzmac)

> 本教程是介绍 ASP.NET 网页和 Microsoft WebMatrix 的教程集的最后一部分。 本文介绍如何将站点发布到 Internet，以便其他人可以使用它。 它假定您已经完成了如何[为 ASP.NET 网页网站创建一致的外观](https://go.microsoft.com/fwlink/?LinkId=251585)。
> 
> 你将了解如何使用发布网站：
> 
> - Microsoft Azure
> - Web 托管公司

## <a name="about-publishing-your-site"></a>关于发布网站

至此，你已完成了本地计算机上的所有工作，包括测试页面。 若要运行你的<em>cshtml</em>页面，你使用了内置于 WebMatrix 的 web 服务器，即 IIS Express。 当然，除了您以外，没有人可以查看您创建的站点。 若要让其他人使用你的网站，你必须将其发布到 Internet。

如果你已经拥有公共 web 服务器的访问权限，则发布意味着你需要具有*云平台*或*托管提供程序*的帐户。 云平台（如 Microsoft Azure）为应用程序提供按需的基础结构。 托管提供商是拥有可公开访问的 web 服务器并且将为你的站点提供空间的公司。 对于大容量商业网站，托管计划每月从几个月（甚至免费）对小型站点运行一次，每月有数百美元的资金。

> [!NOTE]
> 你可能有权通过 internet 服务提供商（ISP）访问公共 web 服务器，你可以在家里获取 internet 服务。 但是，宿主提供程序必须支持 ASP.NET 网页。 许多 Isp 不是，但一定要进行检查。

在本教程中，我们将简要介绍如何发布。 提供所有内容的详细信息并不可行，因为每个托管提供程序的过程各不相同。 不过，您可以很好地了解该过程的工作方式。

本教程包含四个部分：

1. [设置默认页](#defaultpage)
2. 发布（选择以下项之一）  
 a. [将站点发布到 Microsoft Azure](#azure)  
 b. [将网站发布到 Web 托管公司](#host)
3. [更新实时站点：重新发布](#update)

<a id="defaultpage"></a>
## <a name="setting-up-the-default-page"></a>设置默认页

当用户导航到网站的基址时，将向用户显示站点的默认页面。 例如，将*Default.htm*设置为站点的默认页面时 `www.contoso.com` ，导航到与 `www.contoso.com` 导航到相同的页面 `www.contoso.com/Default.htm` 。

当前，你的网站使用**默认的. cshtml**作为默认页。 此页可用于你的默认页面，但在本教程中，你没有将任何内容添加到该页面，因此它将显示一个空白页面。 打开默认的 cshtml，并将内容替换为以下代码。

[!code-cshtml[Main](publishing/samples/sample1.cshtml)]

现在，你的网站已准备好进行发布。 首先，您将了解如何将网站部署到 Azure，以及如何将其部署到 web 托管公司。 这两个选项都适用于你的网站，你只需遵循一个部署选项。

<a id="azure"></a>
## <a name="publishing-your-site-to-microsoft-azure"></a>将站点发布到 Microsoft Azure

本教程将首先介绍如何将网站部署到 Microsoft Azure。 通过使用 Microsoft 帐户登录，你可以在 Azure 上创建最多10个免费网站。 这些免费网站提供了一种方便的方法来测试您的站点。 稍后，你始终可以删除此示例网站，以避免使用所有免费网站。 只需几分钟即可创建一个免费试用帐户。 有关详细信息，请参阅 [Azure 免费试用](https://azure.microsoft.com/free/dotnet/)。

在 WebMatrix 功能区中，单击 "**发布**" 按钮。

![WebMatrix 功能区中的 "发布" 按钮](publishing/_static/image1.png)

随即显示 "**发布网站**" 对话框。 如果尚未登录到 Microsoft 帐户，则对话框将包含 " **Azure 入门**" 链接。 单击此链接。

![发布你的网站](publishing/_static/image2.png)

如果尚未登录到 Microsoft 帐户，则会再次获得登录机会。 你必须登录到 Microsoft 帐户才能在 Azure 上发布你的网站。

![登录](publishing/_static/image3.png)

登录到 Microsoft 帐户后，该对话框包含用于在 Azure 上创建新网站或连接到 Azure 上的现有网站之一的链接。

![创建新站点](publishing/_static/image4.png)

选择 "**创建新站点**"。

如果你将项目命名为**WebPagesMovies**，则网站的默认名称将为**webpagesmovies.azurewebsites.net**。 此默认名称很可能不可用，如红色惊叹号所示。

![默认网站名称](publishing/_static/image5.png)

将 "站点名称" 更改为 "可用"，然后选择靠近你所在位置的位置。

![更改的站点名称](publishing/_static/image6.png)

单击“确定”。

WebMatrix performss 一种测试来确定服务器是否与站点兼容。

![兼容性测试](publishing/_static/image7.png)

选择“继续”。

将显示兼容性测试的结果。

![兼容性结果](publishing/_static/image8.png)

选择“继续”。

WebMatrix 显示将发布到站点的文件和数据库。 由于这是你首次发布网站，因此会列出所有文件。 您可以取消选中未准备好进行发布的文件。 在后续发布中，只显示已更改的文件。 请参阅[更新实时网站：重新发布](#update)。

![发布预览](publishing/_static/image9.png)

选择“继续”。

将站点部署到 Azure 之后，会显示一条消息，指示部署已完成。

![发布完成](publishing/_static/image10.png)

你的网站和数据库已发布到 Azure，现在可供公众使用。 单击消息中指示发布已完成的链接，此时将显示已部署的站点。 你或拥有 Internet 访问权限的任何人都可以添加或修改数据库中的记录。

![](publishing/_static/image11.png)

<a id="host"></a>
## <a name="publishing-your-site-to-a-web-hosting-company"></a>将网站发布到 Web 托管公司

如果决定不发布到 Azure，可以改为将网站发布到 web 托管公司。

单击 "**查找 web 托管**" 链接。

!["发布设置" 对话框中的 "查找 web 宿主" 按钮](publishing/_static/image12.png)

请访问 Microsoft 网站上的页面，其中列出了支持 ASP.NET 的托管提供商。

![列出托管提供商的 Microsoft 网站上的页面](publishing/_static/image13.png)

很明显，现在很难知道您可能需要的长期托管功能。 下面是几个需要注意的事项：

- 对于 WebPagesMovies 站点，无需为 SQL Server 提供单独的外接程序，这通常会产生额外的成本。 在您的网站中，您使用的是自包含 SQL Server Compact 版本。 但是，你可能需要 SQL Server 的访问权限，才能执行某些后续的网站工作。 如果你认为可能，请确保稍后可以添加 SQL Server 功能。
- 检查宿主提供程序是否支持 Web 部署发布协议。 您可以使用 FTP 协议进行发布，但使用 Web 部署更为方便。

某些站点提供免费试用期。 免费试用版是尝试发布和托管的好方法，同时你仍在使用 WebMatrix 和 ASP.NET 网页。

选择你喜欢的一个。 对于本教程，我们选择了 "DiscountASP.NET"，因为在创建本教程的过程中，该公司的促销活动允许用户在数月内免费托管站点。

> [!NOTE]
> 对于本教程，我们选择的托管提供商不应将其解释为对该公司的认可。 但我们必须选择一个用于说明，而 DiscountASP.NET 是支持 ASP.NET 网页的众多公司之一和发布的 Web 部署协议。

通常，在注册托管提供程序后，公司会向你发送一封电子邮件，其中包含用户名和密码、web 服务器的 URL 等。 如果托管公司支持 Web 部署协议，则他们可能会向您发送包含发布设置的文件，或让您下载一个文件。 发布设置文件简化了过程。

注册并准备好发布后，请单击 "WebMatrix" 功能区中的 "**发布**" 按钮。 随即显示 "**发布设置**" 对话框。

如果宿主提供程序发送了发布设置文件，请单击 "**导入发布设置**" 链接，然后导入该文件。 如果没有发布设置文件，请使用托管公司通过电子邮件发送给您的值填写字段。 完成后，"**发布设置**" 对话框如下所示：

![在 "发布设置" 对话框中填写的发布设置](publishing/_static/image14.png)

单击 "**验证连接**"。 如果一切正常，对话框将报告**成功连接**，这意味着它可以与宿主提供商的服务器进行通信。

![发布设置正确时的成功消息](publishing/_static/image15.png)

如果出现问题，WebMatrix 会尽力告诉您问题是什么：

![发布设置出现问题时出现错误消息](publishing/_static/image16.png)

单击“保存”**** 以保存设置。 WebMatrix 提供执行测试以确保它能够与宿主站点正确通信：

![用于执行发布过程测试的消息服务](publishing/_static/image17.png)

单击 **“是”** 。 WebMatrix 将一些示例文件上传到宿主提供程序。 兼容性测试完成后，WebMatrix 会报告结果：

![发布测试的结果](publishing/_static/image18.png)

如果已准备就绪，请继续操作，并单击 "**继续**" 以启动真实的发布过程。 WebMatrix 指出了站点中有哪些文件，并且这些文件已位于主机服务器上（目前为 "无"），并提供发布过程的预览：

![发布进程将上传的文件的预览](publishing/_static/image19.png)

要发布的文件的列表包含您创建的网页 *，如：* 此列表还包括已安装的帮助程序的文件、为数据库 SQL Server Compact 版本运行的文件等。 因此，初始发布过程可能很重要。

单击“继续” 。 WebMatrix 将文件复制到托管提供商的服务器。 完成后，会在状态栏中报告结果：

![发布过程成功完成后的状态栏消息](publishing/_static/image20.png)

若要查看实时网站，请单击状态栏中的链接。 将*电影*添加到 URL，你将看到你创建的 "*电影*" 文件：

![显示电影页面的实时站点](publishing/_static/image21.png)

<a id="update"></a>
## <a name="updating-the-live-site-republishing"></a>更新实时站点：重新发布

发布站点（到 Azure 或 web 托管公司）后， &mdash; 计算机上的版本和服务提供商的版本中都有两个副本。 你可能想要继续开发站点（如果没有其他任何内容，作为下一个教程集的一部分）。 当你执行此操作时，必须重新发布网站才能将更改从计算机复制到服务提供商。 WebMatrix 中的发布过程可以确定站点上已更改的文件，并仅发布这些文件。

若要查看重新发布的工作原理，请打开 "*电影*" 站点，进行一些小的更改，然后保存该文件。 例如，将标题更改为 `Movies - Updated` 。

单击功能区中的 "**发布**" 按钮。 WebMatrix 确定要更改的内容，并为你显示要发布的文件的预览。

![显示已更改的文件以进行重新发布的 "发布" 对话框](publishing/_static/image22.png)

> [!IMPORTANT] 
> 
> 默认情况下，WebMatrix 仅在第一次发布站点时发布数据库（*.sdf*文件）。 一旦你的网站发布并且用户与网站交互后，实时站点上的数据库通常会包含该站点的真实数据。 您必须小心地不要使用计算机上的 *.sdf*文件（通常只包含测试数据）来覆盖实时数据库。 这就是为什么会出现警告**发布将覆盖任何远程数据库**以及默认情况下清除*WebPagesMovies*的复选框的原因。

单击“继续” 。 WebMatrix 发布已更改的文件，并显示一条成功消息，就像第一次发布时所做的那样。

转到活动站点（如果它仍显示，你可以单击成功消息中的链接）并验证你的更改是否已发布。

> [!TIP] 
> 
> **远程编辑文件**
> 
> 作为更改站点和重新发布的替代方法，可以直接在 WebMatrix 中编辑远程文件。 在此方案中，你将打开服务提供商上的一个文件，WebMatrix 会下载该文件的副本供你编辑。 每次保存文件时，WebMatrix 都会将更改发送到站点。
> 
> 远程编辑是对您的实时网站进行更改的一种简单方法。 但是，以这种方式进行的更改不会与本地站点中的文件同步。 若要将本地文件与远程站点同步，可以下载远程文件。 除了反向，此过程的工作方式非常类似于发布。
> 
> 本文不会详细介绍 WebMatrix 的远程编辑和远程下载功能。 如果多人必须在不同计算机上的同一站点上工作，则它们非常有用。 有关详细信息，请参阅[使用 WebMatrix 2 Beta 发布和编辑远程站点](https://go.microsoft.com/fwlink/?LinkId=251591)。

## <a name="additional-resources"></a>其他资源

- [ASP.NET WebMatrix ASP.NET 网页论坛](https://forums.asp.net/1224.aspx/1?WebMatrix+and+ASP+NET+Web+Pages)，是提出问题并获得答案的好地方。

> [!div class="step-by-step"]
> [上一篇](layouts.md)

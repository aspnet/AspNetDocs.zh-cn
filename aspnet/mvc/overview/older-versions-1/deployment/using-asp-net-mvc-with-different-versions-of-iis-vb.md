---
uid: mvc/overview/older-versions-1/deployment/using-asp-net-mvc-with-different-versions-of-iis-vb
title: 将ASP.NET MVC 与不同版本的 IIS （VB） 使用 |微软文档
author: rick-anderson
description: 在本教程中，您将了解如何使用ASP.NET MVC 和 URL 路由，以及不同版本的 Internet 信息服务。 你学习不同的策略...
ms.author: riande
ms.date: 08/19/2008
ms.assetid: 1c1283b2-6956-4937-b568-d30de432ce23
msc.legacyurl: /mvc/overview/older-versions-1/deployment/using-asp-net-mvc-with-different-versions-of-iis-vb
msc.type: authoredcontent
ms.openlocfilehash: 5e04ae14026e6d5dd1e603be6c52ff6876a468cf
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541996"
---
# <a name="using-aspnet-mvc-with-different-versions-of-iis-vb"></a>通过不同版本的 IIS 使用 ASP.NET MVC (VB)

由[微软](https://github.com/microsoft)

> 在本教程中，您将了解如何使用ASP.NET MVC 和 URL 路由，以及不同版本的 Internet 信息服务。 您将学习将 ASP.NET MVC 与 IIS 7.0（经典模式）、IIS 6.0 和早期版本的 IIS 使用的不同策略。

ASP.NET MVC 框架依赖于ASP.NET路由来将浏览器请求路由到控制器操作。 为了利用ASP.NET路由，您可能需要在 Web 服务器上执行其他配置步骤。 这完全取决于互联网信息服务 （IIS） 的版本和应用程序的请求处理模式。

以下是不同版本的 IIS 的摘要：

- IIS 7.0（集成模式） - 无需特殊配置ASP.NET路由。
- IIS 7.0（经典模式） - 您需要执行特殊配置才能使用ASP.NET路由。
- IIS 6.0 或以下 - 您需要执行特殊配置才能使用ASP.NET路由。

最新版本的 IIS 版本为 7.5 版本（在 Win7 上）。 IIS 7 的 IIS 包含在 Windows 服务器 2008 和 VISTA/SP1 及更高版本中。 您还可以在 Vista 操作系统的任何版本上安装 IIS 7.0，但家庭基本版除外[https://technet.microsoft.com/library/cc731179%28WS.10%29.aspx](https://technet.microsoft.com/library/cc731179%28WS.10%29.aspx)（参见 ）。

IIS 7.0 支持两种处理请求的模式。 您可以使用集成模式或经典模式。 在集成模式下使用 IIS 7.0 时，无需执行任何特殊配置步骤。 但是，在经典模式下使用 IIS 7.0 时，您确实需要执行其他配置。

微软 Windows 服务器 2003 包括 IIS 6.0。 使用 Windows Server 2003 操作系统时，无法将 IIS 6.0 升级到 IIS 7.0。 使用 IIS 6.0 时，必须执行其他配置步骤。

微软视窗XP专业版包括IIS 5.1。 使用 IIS 5.1 时，必须执行其他配置步骤。

最后，微软 Windows 2000 和微软 Windows 2000 专业版包括 IIS 5.0。 使用 IIS 5.0 时，必须执行其他配置步骤。

## <a name="integrated-versus-classic-mode"></a>集成模式与经典模式

IIS 7.0 可以使用两种不同的请求处理模式处理请求：集成和经典。 集成模式提供更好的性能和更多功能。 经典模式包括向后兼容早期版本的 IIS。

请求处理模式由应用程序池确定。 通过确定与应用程序关联的应用程序池，可以确定特定 Web 应用程序正在使用哪种处理模式。 执行以下步骤:

1. 推出互联网信息服务管理器
2. 在"连接"窗口中，选择应用程序
3. 在"操作"窗口中，单击 **"基本设置"** 链接以打开"编辑应用程序"对话框（参见图 1）
4. 请注意所选的应用程序池。

默认情况下，IIS 配置为支持两个应用程序池：**默认AppPool**和**经典 .NET AppPool**。 如果选择了默认AppPool，则应用程序以集成的请求处理模式运行。 如果选择了经典 .NET AppPool，则应用程序以经典请求处理模式运行。

[![“新建项目”对话框](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image1.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image1.png)

**图1：** 检测请求处理模式（[单击以查看全尺寸图像](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image2.png)）

请注意，您可以在"编辑应用程序"对话框中修改请求处理模式。 单击"选择"按钮并更改与应用程序关联的应用程序池。 请注意，将ASP.NET应用程序从经典模式更改为集成模式时存在兼容性问题。 有关详细信息，请参阅以下文章：

- 将 ASP.NET 1.1 升级到 Windows Vista 和 Windows 服务器 2008 上的 IIS 7.0 --[https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008)

- ASP.NET与 IIS 7.0 集成 -[https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis)

如果ASP.NET应用程序正在使用 DefaultAppPool，则无需执行任何其他步骤，就可以使ASP.NET路由（因此ASP.NET MVC）正常工作。 但是，如果ASP.NET应用程序配置为使用经典 .NET AppPool，然后继续阅读，您还有更多工作要做。

## <a name="using-aspnet-mvc-with-older-versions-of-iis"></a>将ASP.NET MVC 与旧版本的 IIS 一起使用

如果您需要将 IIS 版本早于 IIS 7.0 的旧版本ASP.NET MVC 使用，或者需要在经典模式下使用 IIS 7.0，则有两个选项。 首先，您可以修改路由表以使用文件扩展名。 例如，您请求的 URL 不是 /Store/详细信息，而是请求 URL，如 /Store.aspx/详细信息。

第二个选项是创建称为*通配符脚本映射*的内容。 通配符脚本映射使您能够将每个请求映射到ASP.NET框架。

如果您无法访问 Web 服务器（例如，您的ASP.NET MVC 应用程序由 Internet 服务提供商托管），则需要使用第一个选项。 如果不想修改 URL 的外观，并且可以访问 Web 服务器，则可以使用第二个选项。

我们将在以下部分中详细介绍每个选项。

## <a name="adding-extensions-to-the-route-table"></a>向路由表添加扩展

获取ASP.NET路由以使用旧版本的 IIS 的最简单方法是修改 Global.asax 文件中的路由表。 清单1中的默认和未修改的 Global.asax 文件配置了一个名为"默认路由"的路由。

**清单1 - 全局.asax（未修改）**

[!code-vb[Main](using-asp-net-mvc-with-different-versions-of-iis-vb/samples/sample1.vb)]

通过清单 1 中配置的默认路由，您可以路由如下所示的 URL：

/首页/索引

/产品/详细信息/3

/Product

遗憾的是，旧版本的 IIS 不会将这些请求传递给ASP.NET框架。 因此，这些请求不会路由到控制器。 例如，如果您对 URL/Home/Index 发出浏览器请求，则将在图 2 中获取错误页。

[![“新建项目”对话框](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image2.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image3.png)

**图2**： 收到 404 未找到错误（[单击以查看全尺寸图像](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image4.png)）

较旧版本的 IIS 仅将某些请求映射到ASP.NET框架。 请求必须针对具有正确文件扩展名的 URL。 例如，对 /SomePage.aspx 的请求将映射到ASP.NET框架。 但是，对 /SomePage.htm 的请求没有。

因此，要使ASP.NET路由正常工作，我们必须修改默认路由，以便它包含映射到ASP.NET框架的文件扩展名。

这是使用名为 的`registermvc.wsf`脚本完成的。 它包含在 ASP.NET MVC 1 版本中`C:\Program Files\Microsoft ASP.NET\ASP.NET MVC\Scripts`，但截至 ASP.NET 2，此脚本已移动到 ASP.NET 期货，可在[http://aspnet.codeplex.com/releases/view/39978](http://aspnet.codeplex.com/releases/view/39978)。

执行此脚本会使用 IIS 注册新的 .mvc 扩展。 注册 .mvc 扩展名后，您可以在 Global.asax 文件中修改路由，以便路由使用 .mvc 扩展名。

清单2中修改后的 Global.asax 文件适用于旧版本的 IIS。

**清单 2 - 全局.asax（使用扩展修改）**

[!code-vb[Main](using-asp-net-mvc-with-different-versions-of-iis-vb/samples/sample2.vb)]

重要提示：请记住在更改 Global.asax 文件后再次构建ASP.NET MVC 应用程序。

清单2中全局.asax 文件有两个重要更改。 现在，全局.asax 中定义了两个路由。 默认路由（第一个路由）的 URL 模式现在如下所示：

{控制器}.mvc/{操作}/{id}

.mvc 扩展名的添加会更改ASP.NET路由模块截获的文件类型。 通过此更改，ASP.NET MVC 应用程序现在路由如下所示的请求：

/Home.mvc/指数/

/产品.mvc/细节/3

/产品.mvc/

第二个路由，根路由，是新的。 根路由的此 URL 模式是一个空字符串。 对于匹配针对应用程序根发出的请求，此路由是必需的。 例如，根路由将匹配如下所示的请求：

[http://www.YourApplication.com/](http://www.YourApplication.com/)

对路由表进行这些修改后，需要确保应用程序中的所有链接都与这些新 URL 模式兼容。 换句话说，请确保所有链接都包含 .mvc 扩展。 如果使用 Html.ActionLink（） 帮助器方法生成链接，则不需要进行任何更改。

您可以手动向 iIS 添加新扩展 ASP.NET，而不是使用 registermvc.wcf 脚本。 自行添加新扩展名时，请确保未选中标记为 **"验证该文件存在"复选框**。

## <a name="hosted-server"></a>托管服务器

您并不总是有权访问 Web 服务器。 例如，如果您使用 Internet 托管提供商托管ASP.NET MVC 应用程序，则不一定有权访问 IIS。

在这种情况下，应使用映射到ASP.NET框架的现有文件扩展名之一。 映射到ASP.NET的文件扩展名的示例包括 .aspx、.axd 和 .ashx 扩展名。

例如，清单 3 中修改的 Global.asax 文件使用 .aspx 扩展名而不是 .mvc 扩展名。

**清单 3 - 全局.asax（使用 .aspx 扩展修改）**

[!code-vb[Main](using-asp-net-mvc-with-different-versions-of-iis-vb/samples/sample3.vb)]

清单3中的 Global.asax 文件与以前的 Global.asax 文件完全相同，只是它使用 .aspx 扩展名而不是 .mvc 扩展名。 您不必在远程 Web 服务器上执行任何设置才能使用 .aspx 扩展。

## <a name="creating-a-wildcard-script-map"></a>创建通配符脚本映射

如果您不想修改ASP.NET MVC 应用程序的 URL，并且可以访问 Web 服务器，则有一个其他选项。 您可以创建通配符脚本映射，将所有请求映射到 Web 服务器ASP.NET框架。 这样，您可以使用默认ASP.NET MVC 路由表与 IIS 7.0（经典模式）或 IIS 6.0。

请注意，此选项会导致 IIS 拦截针对 Web 服务器的每个请求。 这包括对图像、经典 ASP 页面和 HTML 页面的请求。 因此，将通配符脚本映射启用ASP.NET确实会影响性能。

以下是为 IIS 7.0 启用通配符脚本映射的方式：

1. 在"连接"窗口中选择应用程序
2. 确保选择了 **"功能"** 视图
3. 双击 **"处理程序映射"** 按钮
4. 单击 **"添加通配符脚本映射"** 链接（参见图 3）
5. 输入 aspnet\_isapi.dll 文件的路径（可以从 PageHandlerFactory 脚本映射复制此路径）
6. 输入名称 MVC
7. 单击 **"确定"** 按钮

[![“新建项目”对话框](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image3.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image5.png)

**图 3**： 使用 IIS 7.0 创建通配符脚本映射（[单击以查看全尺寸图像](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image6.png)）

按照以下步骤创建具有 IIS 6.0 的通配符脚本映射：

1. 右键单击网站并选择"属性"
2. 选择**主目录**选项卡
3. 单击 **"配置"** 按钮
4. 选择 **"映射"** 选项卡
5. 单击 **"插入"** 按钮（参见图 4）
6. 将 aspnet\_isapi.dll 的路径粘贴到可执行字段（可以从 .aspx 文件的脚本映射中复制此路径）
7. 取消选中标记为 **"验证文件存在"复选框**
8. 单击 **"确定"** 按钮

[![“新建项目”对话框](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image4.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image7.png)

**图 4**： 使用 IIS 6.0 创建通配符脚本映射（[单击以查看全尺寸图像](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image8.png)）

启用通配符脚本映射后，需要修改 Global.asax 文件中的路由表，以便它包含根路由。 否则，当您请求应用程序的根页时，您将获得图 5 中的错误页。 您可以使用清单 4 中修改的 Global.asax 文件。

[![“新建项目”对话框](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image5.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image9.png)

**图 5**： 缺少根路由错误（[单击以查看全尺寸图像](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image10.png)）

**清单 4 - 全局.asax（使用根路由修改）**

[!code-vb[Main](using-asp-net-mvc-with-different-versions-of-iis-vb/samples/sample4.vb)]

为 IIS 7.0 或 IIS 6.0 启用通配符脚本映射后，可以发出适用于默认路由表的请求，如下所示：

/

/首页/索引

/产品/详细信息/3

/Product

## <a name="summary"></a>总结

本教程的目的是解释在使用旧版本的 IIS（或经典模式下的 IIS 7.0）时如何使用ASP.NET MVC。 我们讨论了使ASP.NET路由与旧版本的 IIS 配合使用的方法：修改默认路由表或创建通配符脚本映射。

第一个选项要求您修改ASP.NET MVC 应用程序中使用的 URL。 第一个选项的一个显著优点是，您不需要访问 Web 服务器来修改路由表。 这意味着，即使使用 internet 托管公司托管ASP.NET MVC 应用程序，您也可以使用此选项。

第二个选项是创建通配符脚本映射。 第二个选项的优点是不需要修改 URL。 第二个选项的缺点是它会影响ASP.NET MVC 应用程序的性能。

> [!div class="step-by-step"]
> [上一篇](using-asp-net-mvc-with-different-versions-of-iis-cs.md)

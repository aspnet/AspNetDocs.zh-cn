---
uid: mvc/overview/older-versions-1/nerddinner/create-a-new-aspnet-mvc-project
title: 创建新ASP.NET MVC 项目 |微软文档
author: rick-anderson
description: 步骤 1 演示如何将基本的 NerdDinner 应用程序结构放在原位。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 7e0e9928-8fdc-4b74-9882-55fac0976628
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/create-a-new-aspnet-mvc-project
msc.type: authoredcontent
ms.openlocfilehash: 240c8a04cec3c07f434182775d1c519aab029761
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541476"
---
# <a name="create-a-new-aspnet-mvc-project"></a>新建 ASP.NET MVC 项目

由[微软](https://github.com/microsoft)

[下载 PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 这是一个免费的["NerdDinner"应用程序教程](introducing-the-nerddinner-tutorial.md)的第 1 步，该教程演示如何使用 ASP.NET MVC 1 构建小型但完整的 Web 应用程序。
> 
> 步骤 1 演示如何将基本的 NerdDinner 应用程序结构放在原位。
> 
> 如果您使用的是ASP.NET MVC 3，我们建议您按照[MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC 音乐商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程进行操作。

## <a name="nerddinner-step-1-file-gtnew-project"></a>神经晚餐步骤 1： 文件&gt;- 新项目

我们将通过在 Visual Studio 2008 或免费的可视化 Web 开发人员 2008 Express 中选择 **"文件-&gt;新项目**"菜单项来开始我们的 NerdDinner 应用程序。

这将弹出"新项目"对话框。 要创建新ASP.NET MVC 应用程序，我们将选择对话框左侧的"Web"节点，然后在右侧选择"ASP.NET MVC Web 应用程序"项目模板：

![](create-a-new-aspnet-mvc-project/_static/image1.png)

*重要提示：请确保已下载并安装 ASP.NET MVC - 否则它不会显示在"新项目"对话框中。如果您尚未安装[Microsoft Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)的 V2（ASP.NET MVC 在"Web 平台-&gt;框架和运行时"部分中可用）。*

我们将命名要创建"NerdDinner"的新项目，然后单击"确定"按钮创建它。

当我们单击"OK"Visual Studio 时，将弹出一个附加对话框，提示我们为新应用程序选择创建单元测试项目。 此单元测试项目使我们能够创建自动测试，以验证应用程序的功能和行为（本教程稍后将介绍如何操作）。

![](create-a-new-aspnet-mvc-project/_static/image2.png)

上面对话框中的"测试框架"下拉列表填充了所有可用的ASP.NET MVC 单元测试项目模板安装在计算机上。 可以为 NUnit、MBUnit 和 XUnit 下载版本。 还支持内置的可视化工作室单元测试框架。

*注意：可视化工作室单元测试框架仅适用于 Visual Studio 2008 专业版和更高版本。如果您使用的是 VS 2008 标准版或可视化 Web 开发人员 2008 Express，则需要下载并安装 nUnit、MBUnit 或 XUnit 扩展，以便ASP.NET MVC 才能显示此对话框。如果没有安装任何测试框架，将不会显示该对话框。*

我们将为我们创建的测试项目使用默认的"NerdDinner.Test"名称，并使用"可视化工作室单元测试"框架选项。 当我们点击"ok"按钮 Visual Studio 将为我们创建一个解决方案，其中包含两个项目 - 一个用于我们的 Web 应用程序，一个用于我们的单元测试：

![](create-a-new-aspnet-mvc-project/_static/image3.png)

### <a name="examining-the-nerddinner-directory-structure"></a>检查 NerdDinner 目录结构

当您使用 Visual Studio 创建新ASP.NET MVC 应用程序时，它会自动向项目添加许多文件和目录：

![](create-a-new-aspnet-mvc-project/_static/image4.png)

默认情况下ASP.NET MVC 项目有六个顶级目录：

| **目录** | **目标** |
| --- | --- |
| **/控制器** | 放置处理 URL 请求的控制器类的位置 |
| **/型号** | 放置表示和操作数据的类的位置 |
| **/视图** | 放置负责呈现输出的 UI 模板文件的位置 |
| **/脚本** | 放置 JavaScript 库文件和脚本的位置 （.js） |
| **/内容** | 放置 CSS 和图像文件以及其他非动态/非 JavaScript 内容的位置 |
| **/应用程序\_数据** | 存储要读取/写入的数据文件的位置。 |

ASP.NET MVC 不需要此结构。 事实上，处理大型应用程序的开发人员通常会跨多个项目对应用程序进行分区，使其更易于管理（例如：数据模型类通常位于与 Web 应用程序不同的类库项目中）。 但是，默认项目结构确实提供了一个不错的默认目录约定，我们可以用它来保持应用程序问题清洁。

当我们展开 /控制器目录时，我们会发现 Visual Studio 默认为项目添加了两个控制器类 - 主控制器和帐户控制器：

![](create-a-new-aspnet-mvc-project/_static/image5.png)

当我们展开 /Views 目录时，我们会发现三个子目录 - /Home，//帐户和 /共享 - 以及其中的几个模板文件也添加到项目中，默认情况下：

![](create-a-new-aspnet-mvc-project/_static/image6.png)

当我们展开 /内容和 /脚本目录时，我们将找到一个 Site.css 文件，该文件用于设置网站上所有 HTML 的样式，以及可在应用程序中启用ASP.NET AJAX 和 jQuery 支持的 JavaScript 库：

![](create-a-new-aspnet-mvc-project/_static/image7.png)

当我们扩展 NerdDinner.测试项目时，我们将找到两个类，其中包含控制器类的单元测试：

![](create-a-new-aspnet-mvc-project/_static/image8.png)

Visual Studio 添加的这些默认文件为我们提供了工作应用程序的基本结构 - 完整的主页，关于页面，帐户登录/注销/注册页，和未处理的错误页面（所有有线和开箱即用）。

### <a name="running-the-nerddinner-application"></a>运行内德晚餐应用程序

我们可以通过选择**调试-&gt;启动调试**或**调试 -&gt;不调试菜单项来**运行项目：

![](create-a-new-aspnet-mvc-project/_static/image9.png)

这将启动 Visual Studio 附带的内置ASP.NET Web 服务器，并运行我们的应用程序：

![](create-a-new-aspnet-mvc-project/_static/image10.png)

以下是我们新项目的主页（URL："/"）运行时：

![](create-a-new-aspnet-mvc-project/_static/image11.png)

单击"关于"选项卡将显示一个有关页面（URL："/主页/关于"）：

![](create-a-new-aspnet-mvc-project/_static/image12.png)

单击右上角的"登录"链接将我们带到登录页面（URL："/帐户/登录"）

![](create-a-new-aspnet-mvc-project/_static/image13.png)

如果我们没有登录帐户，我们可以单击注册链接（URL："/帐户/注册"）创建一个：

![](create-a-new-aspnet-mvc-project/_static/image14.png)

在创建新项目时，默认情况下添加了实现上述主页、关于和注销/寄存器功能的代码。 我们将使用它作为应用程序的起点。

### <a name="testing-the-nerddinner-application"></a>测试内德晚餐应用程序

如果我们使用 Visual Studio 2008 的专业版或更高版本，我们可以在 Visual Studio 中使用内置单元测试 IDE 支持来测试项目：

![](create-a-new-aspnet-mvc-project/_static/image15.png)

选择上述选项之一将在 IDE 中打开"测试结果"窗格，并在新项目中包含的 27 个单元测试中提供通过/失败状态，这些测试涵盖内置功能：

![](create-a-new-aspnet-mvc-project/_static/image16.png)

在本教程的后面部分，我们将介绍有关自动测试的更多信息，并添加其他单元测试，这些测试涵盖了我们实现的应用程序功能。

### <a name="next-step"></a>下一步

现在，我们已经有了一个基本的应用程序结构。 现在，让我们[创建一个数据库来存储我们的应用程序数据](create-a-database.md)。

> [!div class="step-by-step"]
> [上一页](introducing-the-nerddinner-tutorial.md)
> [下一页](create-a-database.md)

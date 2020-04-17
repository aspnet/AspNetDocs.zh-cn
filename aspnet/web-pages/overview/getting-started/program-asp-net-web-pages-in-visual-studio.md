---
uid: web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
title: 使用可视化工作室编程ASP.NET网页 （Razor） |微软文档
author: Rick-Anderson
description: 本附录说明如何使用 Visual Studio 2010 或可视化 Web 开发人员 2010 Express 使用 Razor 语法对 ASP.NET 网页进行编程。
ms.author: riande
ms.date: 02/13/2014
ms.assetid: 0acfec5a-48f2-4766-a801-a0f426966f0a
msc.legacyurl: /web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
msc.type: authoredcontent
ms.openlocfilehash: e586a116fc48a797bdd40befad5851a548282ce6
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542893"
---
# <a name="programming-aspnet-web-pages-razor-using-visual-studio"></a>使用可视化工作室ASP.NET网页 （Razor） 编程

 作者 [Tom FitzMacken](https://github.com/tfitzmac)

> 本文介绍如何使用可视化工作室或可视化 Web 开发人员快速程序ASP.NET网页 （Razor） 网站。
>
> 学习内容
>
> - 您需要安装的内容（如果有的话）才能在 Visual Studio 版本中使用ASP.NET网页。
> - 如何向可视化 Web 开发人员 2010 Express 添加对ASP.NET网页的支持。
> - 如何使用 Visual Studio 中的功能使用ASP.NET Razor 页面，包括 IntelliSense 和调试器。
>
>
> ## <a name="software-versions-used-in-the-tutorial"></a>本教程中使用的软件版本
>
>
> - ASP.NET网页 （剃须刀） 3
> - Visual Studio 2013
> - Web矩阵 3
>
>
> 本教程还适用于ASP.NET网页 2、Visual Studio 2012、Visual Studio 2010 和 WebMatrix 2。

您可以使用 WebMatrix 或许多其他代码编辑器使用 Razor 语法对ASP.NET网页进行编程。 您还可以使用 Microsoft Visual Studio，这是一个功能齐全的集成开发环境 （IDE），它提供了一组功能强大的工具来创建多种类型的应用程序（而不仅仅是网站）。 要使用ASP.NET Razor 页面，您可以使用[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)。

Visual Studio 为使用 ASP.NET Razor 网页进行编程提供的两个特别有用的功能是：

- *内泰利感知*。 视觉工作室内置的 IntelliSense 功能比 WebMatrix 中的 IntelliSense 更为全面。
- *调试器*。 调试器允许您在程序运行时停止程序、检查变量和逐行执行代码，从而对代码进行故障排除。

## <a name="using-visual-studio-with-different-versions-of-aspnet-web-pages"></a>将视觉工作室与不同版本的ASP.NET网页使用

要在 Visual Studio 2017 中开发ASP.NET Web 应用，请安装**ASP.NET和 Web 开发**工作负载。

Visual Studio 2012 和 Visual Studio 2013 包括对ASP.NET网页的支持。 （安装 Visual Studio 时，将安装支持ASP.NET网页所需的软件包。

默认情况下，Visual Studio 2010 不包括对 ASP.NET 网页的支持。 要将 ASP.NET 网页与 Visual Studio 2010 一起使用，您必须安装ASP.NET MVC 软件包。 要获取 ASP.NET网页 2，请安装ASP.NET MVC 4。

下表总结了不同版本的 Visual Studio 中对 ASP.NET 网页的支持。

|  | Visual Studio 2010 | Visual Studio 2012 | Visual Studio 2013 |
| --- | --- | --- | --- |
| **ASP.NET 网页 2** | 安装ASP.NET MVC 4 | （包括） | （包括） |
| **ASP.NET 网页 3** |  | 通过 NuGet 更新到ASP.NET网页 3 | （包括） |

要使用 Visual Studio 2010，请参阅[在 Visual Studio 2010 中安装支持ASP.NET网页](#vs2010support)。

## <a name="launching-visual-studio-from-webmatrix"></a>从 WebMatrix 启动可视化工作室

如果您在 WebMatrix 中启动了一个项目，并希望切换到 Visual Studio，WebMatrix 提供了一个按钮，用于在 Visual Studio 中轻松打开项目。 您必须在计算机上安装 Visual Studio 才能启用此按钮。 下图显示了 WebMatrix 中的按钮。

![启动视觉工作室](program-asp-net-web-pages-in-visual-studio/_static/image1.png)

单击该按钮时，项目在可视化工作室中打开。 您可以在 WebMatrix 和 Visual Studio 之间来回切换，没有任何问题。 如果其他环境中的任何文件已更改，需要重新加载以获取最新更改，您将收到通知。

## <a name="creating-aspnet-razor-site-in-visual-studio"></a>在视觉工作室创建ASP.NET剃刀网站

要在视觉工作室中创建ASP.NET剃刀网站：

1. 打开 Visual Studio。
2. 在 **"文件**"菜单中，单击 **"新建网站**"。

    ![创建新网站](program-asp-net-web-pages-in-visual-studio/_static/image2.png)
3. 在 **"新建网站"** 对话框中，选择要使用的语言（可视 C# 或可视基本）。
4. 选择**ASP.NET网站（Razor）** 模板。

    ![剃须刀网站](program-asp-net-web-pages-in-visual-studio/_static/image3.png)
5. 单击 **“确定”** 。

新项目存在，并且填充了一些默认网页，以帮助您入门。

### <a name="using-intellisense"></a>Using IntelliSense

现在，您已经创建了一个网站，您可以看到 IntelliSense 在视觉工作室中是如何工作的。

1. 在您刚刚创建的网站中，打开*Default.cshtml*页面。
2. 在页面`<h3>`中的标记之后，键入`@ServerInfo.`（包括点）。 请注意 IntelliSense 如何在下拉列表中显示`ServerInfo`帮助程序的可用方法。

    ![intellisense](program-asp-net-web-pages-in-visual-studio/_static/image4.png)
3. 从`GetHtml`列表中选择方法，然后按 Enter。 IntelliSense 会自动填充该方法。 （与 C# 中的任何方法一样，必须在`()`方法之后添加字符。方法的`GetHtml`已完成代码类似于以下示例：

    [!code-cshtml[Main](program-asp-net-web-pages-in-visual-studio/samples/sample1.cshtml)]
4. 按 Ctrl+F5 以运行该页。 这是页面在浏览器中显示时的外观：

    ![浏览器中的默认页面](program-asp-net-web-pages-in-visual-studio/_static/image5.png)
5. 关闭浏览器。

### <a name="using-the-debugger"></a>使用调试器

1. 在*Default.cshtml*页面的顶部，以`Page.Title`开头的行后添加以下代码行：

    [!code-csharp[Main](program-asp-net-web-pages-in-visual-studio/samples/sample2.cs)]
2. 在代码左侧编辑器的灰色边距中，单击此新行的旁边以添加*断点*。 断点是一个标记，它告诉调试器在此时停止运行程序，以便您可以看到发生了什么。

    ![设置断点](program-asp-net-web-pages-in-visual-studio/_static/image6.png)
3. 删除对 方法的`ServerInfo.GetHtml`调用，并将调用添加到`@myTime`变量的位置。 此调用显示新代码行返回的当前时间值。
4. 按 F5 以在调试器中运行页面。 页面在您设置的断点上停止。 下图显示了具有断点（黄色）的编辑器中页面的外观。

    ![调试断点](program-asp-net-web-pages-in-visual-studio/_static/image7.png)
5. 在"调试"工具栏中，单击 **"进入"** 按钮（或按 F11）以运行下一行代码。 每次单击此按钮时，都会将执行提前到下一行代码。

    ![单步进入按钮](program-asp-net-web-pages-in-visual-studio/_static/image8.png)
6. 通过将鼠标指针放在变量`myTime`上或通过检查 **"局部变量**"和 **"调用堆栈**"窗口中显示的值来检查变量的值。 可视化工作室显示变量的值。

    ![显示时间值](program-asp-net-web-pages-in-visual-studio/_static/image9.png)
7. 检查完变量并单步执行代码后，按 F5 继续运行页面，而无需在每行停止。 完成所有代码后，浏览器将显示页面。

要了解有关调试器以及如何在 Visual Studio 中调试代码的信息，请参阅[演练：在可视化 Web 开发人员中调试网页](https://msdn.microsoft.com/library/z9e7w6cs.aspx)。

## <a name="using-razor-in-aspnet-mvc-projects-with-visual-studio"></a>使用 Razor 在 ASP.NET MVC 项目中使用 Visual Studio

Razor 语法还广泛用于ASP.NET MVC 项目中。 MVC 是构建动态网站的强大、基于模式的方法。 如果ASP.NET网页网站变得难以维护，您可能需要考虑将其转换为ASP.NET MVC 应用程序。 有关创建 MVC 应用程序的示例，请参阅[使用 mVC 5 ASP.NET 入门](../../../mvc/overview/getting-started/introduction/getting-started.md)。

<a id="vs2010support"></a>
## <a name="installing-support-for-aspnet-web-pages-in-visual-studio-2010"></a>2010 年在可视化工作室安装对 ASP.NET 网页的支持

本节演示如何安装 Visual Web 开发人员 Express 2010 和可视化工作室的ASP.NET网页工具。

1. 如果您还没有 Web 平台安装程序，请从以下 URL 下载它：

    [https://www.microsoft.com/web/downloads/platform.aspx](https://www.microsoft.com/web/downloads/platform.aspx)
2. 运行 Web 平台安装程序。
3. 单击"**产品**"选项卡。

    ![WebPI 产品选项卡](program-asp-net-web-pages-in-visual-studio/_static/image10.png)
4. 搜索**ASP.NET MVC 4（ASP.NET**网页 2），然后单击"**添加**"。 这些产品包括用于构建ASP.NET Razor 网站的视觉工作室工具。

    ![WebPi 安装选项](program-asp-net-web-pages-in-visual-studio/_static/image11.png)
5. 单击"**安装**"以完成安装。

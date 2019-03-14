---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-controller
title: 添加控制器 (C#) |Microsoft Docs
author: Rick-Anderson
description: 本教程将讲述构建使用 Microsoft Visual Web Developer 2010 Express 服务包 1，哪些 i 的 ASP.NET MVC Web 应用程序的基础知识...
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 0b8c56b5-fdf3-42dd-a866-98fbe0ab78a0
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-controller
msc.type: authoredcontent
ms.openlocfilehash: bef864829320ae17520adfb4bc49f582013614ce
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57036594"
---
<a name="adding-a-controller-c"></a>添加控制器 (C#)
====================
通过[Rick Anderson]((https://twitter.com/RickAndMSFT))

> > [!NOTE]
> > 本教程中的更新的版本是可用[此处](../../../getting-started/introduction/getting-started.md)，它使用 ASP.NET MVC 5 和 Visual Studio 2013。 它是更安全、 更易于遵循，并演示更多的功能。
> 
> 
> 本教程将讲述构建使用 Microsoft Visual Web Developer 2010 Express Service Pack 1，这是免费版本的 Microsoft Visual Studio 的 ASP.NET MVC Web 应用程序的基础知识。 在开始之前，请确保已安装以下列出的先决条件。 可以通过单击以下链接安装所有这些：[Web 平台安装程序](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。 或者，可以单独安装系统必备组件，使用以下链接：
> 
> - [Visual Studio Web Developer Express SP1 必备组件](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 工具更新](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（运行时和工具支持）
> 
> 如果您使用 Visual Studio 2010 而不 Visual Web Developer 2010，请通过单击以下链接安装必备组件：[Visual Studio 2010 必备组件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。
> 
> 可随附于此项目具有 C# 源代码的 Visual Web Developer 项目。 [下载 C# 版本](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)。 如果您喜欢 Visual Basic，切换到[Visual Basic 版本](../vb/intro-to-aspnet-mvc-3.md)本教程。


MVC 代表*模型-视图-控制器*。 MVC 是用于开发良好设计且易于维护的应用程序的模式。 基于 MVC 的应用程序包含：

- 控制器：处理应用程序，传入请求的类中检索模型数据，然后指定将响应返回到客户端的视图模板。
- 模型：类表示应用程序的数据和使用验证逻辑以强制实施针对这些数据的业务规则。
- 视图：你的应用程序使用动态生成 HTML 响应的模板文件。

我们将进行介绍本系列教程中的所有这些概念并说明如何使用它们来构建应用程序。

让我们首先创建一个控制器类。 在中**解决方案资源管理器**，右键单击*控制器*文件夹，然后选择**添加控制器**。

[![](adding-a-controller/_static/image2.png)](adding-a-controller/_static/image1.png)

命名新控制器"HelloWorldController"。 将保留为默认模板**空控制器**然后单击**添加**。

[![AddHelloWorldController](adding-a-controller/_static/image4.png)](adding-a-controller/_static/image3.png)

请注意，在**解决方案资源管理器**的一个新的文件具有已创建的名为*HelloWorldController.cs*。 该文件是在 IDE 中打开。

![](adding-a-controller/_static/image5.png)

内部`public class HelloWorldController`块中，创建两个方法，如以下代码所示。 控制器将返回 HTML 的字符串作为示例。

[!code-csharp[Main](adding-a-controller/samples/sample1.cs)]

名为你的控制器`HelloWorldController`和更高版本的第一个方法命名为`Index`。 让我们从浏览器调用它。 运行应用程序 （按 F5 或 Ctrl + F5）。 在浏览器中，将"HelloWorld"追加到地址栏中的路径。 (例如，在图中，其下方的`http://localhost:43246/HelloWorld.`) 在浏览器中的页将类似于以下屏幕截图。 在上述方法中，代码直接返回一个字符串。 你告诉系统只返回一些 HTML，并确实执行此操作 ！

![](adding-a-controller/_static/image6.png)

ASP.NET MVC 调用不同的控制器类 （和其中不同的操作方法），具体取决于传入的 URL。 使用 ASP.NET MVC 的默认映射逻辑使用如下格式来确定哪些代码以调用：

`/[Controller]/[ActionName]/[Parameters]`

URL 的第一个部分确定要执行的控制器类。 因此 */HelloWorld*映射到`HelloWorldController`类。 URL 的第二部分确定要执行的类上的操作方法。 因此 */HelloWorld/索引*会导致`Index`方法的`HelloWorldController`类来执行。 请注意，我们只需要浏览到 */HelloWorld*和`Index`默认情况下使用了方法。 这是因为方法命名为`Index`是如果有一个未显式指定调用在控制器的默认方法。

浏览到 `http://localhost:xxxx/HelloWorld/Welcome`。 `Welcome` 方法运行并返回字符串“这是 Welcome 操作方法...”。 默认 MVC 映射`/[Controller]/[ActionName]/[Parameters]`。 对于此 URL，采用 `HelloWorld` 控制器和 `Welcome` 操作方法。 目前尚未使用 URL 的 `[Parameters]` 部分。

![](adding-a-controller/_static/image7.png)

让我们这样可以将一些参数信息从 URL 传递给控制器稍微修改一下该示例 (例如， */HelloWorld/欢迎？ 名称 = Scott&amp;numtimes = 4*)。 更改你`Welcome`方法以包括两个参数，如下所示。 请注意，代码使用 C# 可选参数功能指示`numTimes`参数应默认为 1，如果为该参数不传递任何值。

[!code-csharp[Main](adding-a-controller/samples/sample2.cs)]

运行应用程序并浏览到示例 URL (`http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4)`。 可在 URL 中对 `name` 和 `numtimes` 使用其他值。 系统将自动映射到方法中的参数将命名的参数从地址栏中的查询字符串。

![](adding-a-controller/_static/image8.png)

在这些示例中这两个控制器始终执行 MVC 的"VC"部分，即，视图和控制器工作。 控制器将直接返回 HTML。 通常，您不希望控制器直接返回 HTML，因为这会变得非常麻烦的代码。 而是我们通常将使用单独的视图模板文件来帮助生成 HTML 响应。 让我们看如何实现这在下一步。

> [!div class="step-by-step"]
> [上一页](intro-to-aspnet-mvc-3.md)
> [下一页](adding-a-view.md)

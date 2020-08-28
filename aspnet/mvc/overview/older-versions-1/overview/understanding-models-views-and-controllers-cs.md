---
uid: mvc/overview/older-versions-1/overview/understanding-models-views-and-controllers-cs
title: '了解 (c # ) 的模型、视图和控制器 |Microsoft Docs'
author: StephenWalther
description: 对模型、视图和控制器的困惑？ 在本教程中，Stephen Walther 介绍了 ASP.NET MVC 应用程序的不同部分。
ms.author: riande
ms.date: 08/19/2008
ms.assetid: 87313792-0a96-4caf-89fc-1457d54e5c1e
msc.legacyurl: /mvc/overview/older-versions-1/overview/understanding-models-views-and-controllers-cs
msc.type: authoredcontent
ms.openlocfilehash: f4d069ddf30634dd6d632468d8e282bf5b2593d3
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045216"
---
# <a name="understanding-models-views-and-controllers-c"></a>了解模型、视图和控制器 (C#)

作者： [Stephen Walther](https://github.com/StephenWalther)

> 对模型、视图和控制器的困惑？ 在本教程中，Stephen Walther 介绍了 ASP.NET MVC 应用程序的不同部分。

本教程提供了 ASP.NET MVC 模型、视图和控制器的高级概述。 换句话说，它解释了 ASP.NET MVC 中的 M "，V" 和 C。

阅读本教程后，应了解 ASP.NET MVC 应用程序的不同部分如何协同工作。 还应了解 ASP.NET MVC 应用程序的体系结构如何与 ASP.NET Web 窗体应用程序或 Active Server Pages 应用程序不同。

## <a name="the-sample-aspnet-mvc-application"></a>示例 ASP.NET MVC 应用程序

用于创建 ASP.NET MVC Web 应用程序的默认 Visual Studio 模板包含一个非常简单的示例应用程序，可用于了解 ASP.NET MVC 应用程序的不同部分。 在本教程中，我们将利用这个简单的应用程序。

通过启动 Visual Studio 2008 并选择菜单选项文件，然后选择 "新建项目" (请参阅图 1) ，通过 MVC 模板创建新的 ASP.NET MVC 应用程序。 在 "新建项目" 对话框中，选择 "项目类型 (Visual Basic 或 c ) #" 下喜欢的编程语言，然后在 "模板" 下选择 " **ASP.NET MVC Web 应用程序** "。 单击“确定”按钮。

[!["新建项目" 对话框](understanding-models-views-and-controllers-cs/_static/image1.jpg)](understanding-models-views-and-controllers-cs/_static/image1.png)

**图 01**： "新建项目" 对话框 ([单击查看全尺寸图像](understanding-models-views-and-controllers-cs/_static/image2.png)) 

创建新的 ASP.NET MVC 应用程序时，将显示 " **创建单元测试项目** " 对话框 (参见图 2) 。 此对话框可用于在解决方案中创建单独的项目，用于测试 ASP.NET MVC 应用程序。 选择 " **否，不创建单元测试项目** "，然后单击 **"确定"** 按钮。

[!["创建单元测试" 对话框](understanding-models-views-and-controllers-cs/_static/image2.jpg)](understanding-models-views-and-controllers-cs/_static/image3.png)

**图 02**：创建单元测试对话框 ([单击查看全尺寸图像](understanding-models-views-and-controllers-cs/_static/image4.png)) 

创建新的 ASP.NET MVC 应用程序后。 "解决方案资源管理器" 窗口中会显示多个文件夹和文件。 特别是，您将看到三个名为 "模型"、"视图" 和 "控制器" 的文件夹。 正如您可能从文件夹名称中猜到的那样，这些文件夹包含用于实现模型、视图和控制器的文件。

如果展开 "控制器" 文件夹，应会看到名为 "AccountController.cs" 的文件和名为 "HomeController.cs" 的文件。 如果展开 "Views" 文件夹，应会看到名为 "帐户"、"家庭" 和 "共享" 的三个子文件夹。 如果你展开主文件夹，你将看到名为 "有关 .aspx 和 (的其他文件"。有关详细信息，请参阅图 3) 。 这些文件构成了默认 ASP.NET MVC 模板附带的示例应用程序。

[!["解决方案资源管理器" 窗口](understanding-models-views-and-controllers-cs/_static/image3.jpg)](understanding-models-views-and-controllers-cs/_static/image5.png)

**图 03**： "解决方案资源管理器" 窗口 ([单击以查看完全大小的图像](understanding-models-views-and-controllers-cs/_static/image6.png)) 

可以通过选择菜单选项 " **调试"、"启动调试**" 来运行示例应用程序。 也可以按 F5 键。

首次运行 ASP.NET 应用程序时，会出现图4中的对话框，建议你启用调试模式。 单击 "确定" 按钮，应用程序将运行。

[!["未启用调试" 对话框](understanding-models-views-and-controllers-cs/_static/image4.jpg)](understanding-models-views-and-controllers-cs/_static/image7.png)

**图 04**： "未启用调试" 对话框 ([单击查看全尺寸图像](understanding-models-views-and-controllers-cs/_static/image8.png)) 

运行 ASP.NET MVC 应用程序时，Visual Studio 会在 web 浏览器中启动该应用程序。 该示例应用程序仅包含两个页面： "索引" 页和 "关于" 页。 首次启动应用程序时，将显示 "索引" 页 (参见图 5) 。 通过单击应用程序右上角的菜单链接，可以导航到 "关于" 页。

[!["索引" 页](understanding-models-views-and-controllers-cs/_static/image10.png)](understanding-models-views-and-controllers-cs/_static/image9.png)

**图 05**：索引页 ([单击查看全尺寸图像](understanding-models-views-and-controllers-cs/_static/image11.png)) 

请注意浏览器地址栏中的 Url。 例如，单击 "关于" 菜单链接后，浏览器地址栏中的 URL 将更改为 **/Home/About**。

如果关闭浏览器窗口并返回到 Visual Studio，则将无法查找路径为 Home/About 的文件。 这些文件不存在。 这是如何实现的？

## <a name="a-url-does-not-equal-a-page"></a>URL 不等于页面

当您生成传统的 ASP.NET Web 窗体应用程序或 Active Server Pages 应用程序时，URL 和页面之间存在一对一的对应关系。 如果从服务器请求名为 SomePage 的页，则更好的做法是在磁盘上有一个名为 SomePage 的页面。 如果 SomePage 文件不存在，则会收到 "错误 **的 404-未找到页** " 错误。

相反，当你在浏览器的地址栏中键入的 URL 与在应用程序中找到的文件之间不存在任何关系。 在 ASP.NET MVC 应用程序中，URL 对应于控制器操作，而不是磁盘上的页面。

在传统的 ASP.NET 或 ASP 应用程序中，浏览器请求会映射到页面。 与此相反，在 ASP.NET MVC 应用程序中，浏览器请求映射到控制器操作。 ASP.NET Web 窗体应用程序以内容为中心。 相反，ASP.NET MVC 应用程序是以应用程序为中心的应用程序逻辑。

## <a name="understanding-aspnet-routing"></a>了解 ASP.NET 路由

浏览器请求通过名为 *ASP.NET 路由*的 ASP.NET 框架的功能映射到控制器操作。 ASP.NET MVC 框架使用 ASP.NET 路由将传入的请求 *路由* 到控制器操作。

ASP.NET 路由使用路由表来处理传入的请求。 当你的 web 应用程序首次启动时，将创建此路由表。 在 global.asax 文件中设置路由表。 默认 MVC global.asax 文件包含在列表1中。

**列表 1-global.asax**

[!code-csharp[Main](understanding-models-views-and-controllers-cs/samples/sample1.cs)]

ASP.NET 应用程序首次启动时，将 \_ 调用应用程序 ( # A1 方法。 在列表1中，此方法会调用 RegisterRoutes ( # A1 方法，RegisterRoutes ( # A3 方法会创建默认的路由表。

默认路由表包含一个路由。 此默认路由会将所有传入请求拆分为三个段 (URL 段是正斜杠) 之间的任何内容。 第一段映射到控制器名称，第二段映射到操作名称，最后一段映射到传递给名为 Id 的操作的参数。

以下列 URL 为例：

/Product/Details/3

此 URL 将分析为三个参数，如下所示：

控制器 = 产品

操作 = 详细信息

Id = 3

Global.asax 文件中定义的默认路由包含所有三个参数的默认值。 默认控制器为 Home，默认操作为 Index，默认 Id 为空字符串。 考虑到这些默认设置，请考虑如何分析以下 URL：

/Employee

此 URL 将分析为三个参数，如下所示：

控制器 = 员工

操作 = 索引

Id =

最后，如果在不提供任何 URL 的情况下打开 ASP.NET MVC 应用程序 (例如， `http://localhost`) 则会分析 URL，如下所示：

控制器 = Home

操作 = 索引

Id =

请求路由到 HomeController 类上 ( # A1 操作的索引。

## <a name="understanding-controllers"></a>了解控制器

控制器负责控制用户与 MVC 应用程序交互的方式。 控制器包含 ASP.NET MVC 应用程序的流控制逻辑。 控制器确定当用户发出浏览器请求时要向用户发送的响应。

控制器只是类 (例如，Visual Basic 或 c # 类) 。 示例 ASP.NET MVC 应用程序包含一个名为 HomeController.cs 的控制器，该控制器位于控制器文件夹中。 HomeController.cs 文件的内容将在列表2中重现。

**列表 2-HomeController.cs**

[!code-csharp[Main](understanding-models-views-and-controllers-cs/samples/sample2.cs)]

请注意，HomeController 有两个名为 Index ( 方法： # A1 和 ( # A3。 这两个方法对应于控制器公开的两个操作。 URL/Home/Index 调用 HomeController ( # A1 方法，URL/Home/About 调用 HomeController。关于 ( # A3 方法。

控制器中的任何公共方法都作为控制器操作公开。 需要小心。 这意味着，可以通过在浏览器中输入正确的 URL 来调用控制器中包含的任何公共方法。

## <a name="understanding-views"></a>了解视图

HomeController 类、索引 ( # A1 和 ( # A3 公开的两个控制器操作都返回视图。 视图包含 HTML 标记和发送到浏览器的内容。 当使用 ASP.NET MVC 应用程序时，视图等效于页面。

你必须在正确的位置创建视图。 HomeController ( # A1 操作返回位于以下路径的视图：

\Views\Home\Index.aspx

HomeController ( # A1 操作返回位于以下路径的视图：

\Views\Home\About.aspx

通常，如果要为控制器操作返回视图，则需要在 Views 文件夹中创建与控制器名称相同的子文件夹。 在子文件夹中，你必须创建一个与控制器操作同名的 .aspx 文件。

列表3中的文件包含有关 .aspx 视图的信息。

**列表 3-关于 .aspx**

[!code-aspx[Main](understanding-models-views-and-controllers-cs/samples/sample3.aspx)]

如果您忽略了列表3中的第一行，则视图的大多数其余部分都包含标准 HTML。 可以通过在此处输入所需的任何 HTML 来修改视图的内容。

视图非常类似于 Active Server Pages 或 ASP.NET Web Forms 中的页面。 视图可以包含 HTML 内容和脚本。 你可以采用最喜欢的 .NET 编程语言 (（例如，c # 或 Visual Basic .NET) 编写脚本。 使用脚本来显示动态内容（如数据库数据）。

## <a name="understanding-models"></a>了解模型

我们讨论了控制器，并讨论了视图。 我们需要讨论的最后一个主题是模型。 什么是 MVC 模型？

MVC 模型包含视图或控制器中未包含的所有应用程序逻辑。 模型应包含所有应用程序业务逻辑、验证逻辑和数据库访问逻辑。 例如，如果使用 Microsoft 实体框架来访问数据库，则需要在 "模型" 文件夹中创建实体框架类 (.edmx 文件) 。

视图应只包含与生成用户界面相关的逻辑。 控制器只应包含返回正确视图所需的最少逻辑，或将用户重定向到另一个操作 (流控制) 。 模型中应包含其他所有内容。

通常情况下，应尽量应对 fat 模型和瘦控制器。 控制器方法应只包含几行代码。 如果控制器操作太大，则应该考虑将逻辑移出到模型文件夹中的新类。

## <a name="summary"></a>摘要

本教程提供了 ASP.NET MVC web 应用程序的不同部分的简要概述。 你了解了 ASP.NET 路由如何将传入浏览器请求映射到特定控制器操作。 已了解控制器如何协调如何将视图返回到浏览器。 最后，您了解了模型如何包含应用程序业务、验证和数据库访问逻辑。

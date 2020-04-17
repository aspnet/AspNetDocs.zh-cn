---
uid: mvc/overview/older-versions-1/overview/asp-net-mvc-overview
title: ASP.NET MVC 概述 |微软文档
author: rick-anderson
description: 了解ASP.NET MVC 应用程序和 ASP.NET Web 窗体应用程序之间的差异。 了解如何决定何时构建ASP.NET MVC 应用程序。
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 2dcb44a4-5cbf-4d62-b363-718104082d86
msc.legacyurl: /mvc/overview/older-versions-1/overview/asp-net-mvc-overview
msc.type: authoredcontent
ms.openlocfilehash: 84810f168faa2e79a65ff3fb75e3654828bdb58f
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541008"
---
# <a name="aspnet-mvc-overview"></a>ASP.NET MVC 概述

由[微软](https://github.com/microsoft)

> 了解ASP.NET MVC 应用程序和 ASP.NET Web 窗体应用程序之间的差异。 了解如何决定何时构建ASP.NET MVC 应用程序。

模型-视图-控制器 (MVC) 体系结构模式将应用程序分成三个主要组件：模型、视图和控制器。 ASP.NET MVC 框架提供了ASP.NET Web 窗体模式的替代方法，用于创建基于 MVC 的 Web 应用程序。 ASP.NET MVC 框架是一个可测试性非常高的轻型演示框架，（与基于 Web 窗体的应用程序一样）它集成了现有的 ASP.NET 功能，如母版页和基于成员资格的身份验证。 MVC 框架在**System.Web.Mvc**命名空间中定义，是**System.Web**命名空间中一个基本的、受支持的一部分。   
  
MVC 是许多开发人员熟悉的标准设计模式。 一些类型的 Web 应用程序将得益于 MVC 框架。 一些类型将继续使用基于 Web 窗体和回发的传统 ASP.NET 应用程序模式。 其他类型的 Web 应用程序将结合这两种方法；这两种方法彼此互不包含。   
  
MVC 框架包括以下组件：

[![调用需要参数值的控制器操作](asp-net-mvc-overview/_static/image1.jpg)](asp-net-mvc-overview/_static/image1.png)

**图 01**： 调用需要参数值的控制器操作 （[单击以查看全尺寸图像](asp-net-mvc-overview/_static/image2.png)）

- **模型**。 模型对象是实现应用程序数据域逻辑的应用程序部分。 通常，模型对象会检索模型状态并将其存储在数据库中。 例如，Product 对象可能会从数据库中检索信息，对数据库进行操作，然后将更新的信息写回 SQL Server 中的 Product 表。

在小型应用程序中，模型通常是概念上的分离，而不是实际分离。 例如，如果应用程序只读取数据集并将其发送到视图，则应用程序没有物理模型层和相关类。 在这种情况下，数据集将承担模型对象的角色。

- **视图**. 视图是显示应用程序用户界面 （UI） 的组件。 通常，此 UI 是用模型数据创建的。 例如，产品表的编辑视图，该表根据 Products 对象的当前状态显示文本框、下拉列表和复选框。

- **控制器**. 控制器是处理用户交互、使用模型并最终选择要呈现的视图来显示 UI 的组件。 在 MVC 应用程序中，视图仅显示信息；控制器处理并响应用户输入和交互。 例如，控制器处理查询字符串值，并将这些值传递给模型，模型又通过使用这些值查询数据库。

MVC 模式可以帮助您创建使应用程序的不同方面（输入逻辑、业务逻辑和 UI 逻辑）分离的应用程序，同时可在这些元素之间提供松散耦合。 该模式指定每种逻辑在应用程序中应处的位置。 UI 逻辑位于视图中。 输入逻辑位于控制器中。 业务逻辑位于模型中。 在您生成应用程序时，通过使用这种分离方式，可以帮助您化繁为简，因为它可以使您侧重于一次实现应用程序的一个方面。 例如，您可以侧重于独立于业务逻辑的视图。   
  
使用 MVC 模式除了可以化繁为简外，还可以使应用程序的测试工作比基于 Web 窗体的 ASP.NET Web 应用程序的测试工作更加轻松。 例如，在基于 Web 窗体的 ASP.NET Web 应用程序中，单一类既用于显示输出又用于响应用户输入。 为基于 Web 窗体的 ASP.NET 应用程序编写自动化测试可能是一项复杂的工作，因为若要测试单个页面，您必须实例化应用程序中的页类、其所有子控件以及其他相关类。 因为为运行页面而实例化的类如此之多，所以可能难以编写专门侧重于应用程序单个部件的测试。 因此，与 MVC 应用程序测试相比，基于 Web 窗体的 ASP.NET 应用程序的测试更加难以实现。 而且，基于 Web 窗体的 ASP.NET 应用程序的测试需要 Web 服务器。 MVC 框架可使组件分离并大量使用接口，这样，便可以将单个组件与框架的其余部分分开进行测试。   
  
MVC 应用程序的这三个主要组件之间的松散耦合也可促进并行开发。 例如，一个开发人员可以处理视图，第二个开发人员可以处理控制器逻辑，第三个开发人员可以专注于模型中的业务逻辑。

## <a name="deciding-when-to-create-an-mvc-application"></a>决定何时创建 MVC 应用程序

您必须仔细考虑是使用 ASP.NET MVC 框架还是使用 ASP.NET Web 窗体模型来实现 Web 应用程序。 MVC 框架未取代 Web 窗体模型；您可以对 Web 应用程序使用任一框架。 （如果您具有现有的基于 Web 窗体的应用程序，则这些应用程序将完全按照它们一贯的方式继续工作。）   
  
在决定对特定网站使用 MVC 框架或 Web 窗体模型之前，请权衡各种方法的优点。

### <a name="advantages-of-an-mvc-based-web-application"></a>基于 MVC 的 Web 应用程序的优点

ASP.NET MVC 框架具有以下优点：

- 通过将应用程序分为模型、视图和控制器，化繁为简的工作更加轻松。
- 它不使用视图状态或基于服务器的窗体。 这使得 MVC 框架特别适合想要完全控制应用程序行为的开发人员。
- 它使用一种通过单一控制器处理 Web 应用程序请求的前端控制器模式。 这使您可以设计一个支持丰富路由基础结构的应用程序。 有关详细信息，请参阅 MSDN 网站上的[前控制器](https://go.microsoft.com/fwlink/?LinkId=106357 "前控制器")。
- 它为测试驱动的开发 (TDD) 提供了更好的支持。
- 它适用于需要对应用程序行为进行高度控制的开发人员和 Web 设计人员的大型团队支持的 Web 应用程序。

### <a name="advantages-of-a-web-forms-based-web-application"></a>基于 Web 窗体的 Web 应用程序的优点

基于 Web 窗体的框架具有以下优点：

- 它支持通过 HTTP 保留状态的事件模型，这有益于开发业务线 Web 应用程序。 基于 Web 窗体的应用程序提供了在数百个服务器控件中受支持的许多事件。
- 它使用页面控制器模式向单个页面添加功能。 有关详细信息，请参阅 MSDN 网站上的[页面控制器](https://go.microsoft.com/fwlink/?LinkId=106359 "页面控制器")。
- 它使用视图状态或基于服务器的窗体，这可以使管理状态信息更容易。
- 它非常适合想要利用大量组件快速开发应用程序的 Web 开发人员和设计人员的小型团队。
- 通常，应用程序开发不太复杂，因为组件 **（Page**类、控件等）集成紧密，通常需要比 MVC 模型更少的代码。

## <a name="features-of-the-aspnet-mvc-framework"></a>ASP.NET MVC 框架的功能

ASP.NET MVC 框架具有以下功能：

- 默认情况下，应用程序任务（输入逻辑、业务逻辑和 UI 逻辑）、可测试性和测试驱动开发 （TDD） 分离。 MVC 框架中的所有核心协定都基于接口并且可使用 mock 对象进行测试，mock 对象是模仿应用程序中实际对象的行为的模拟对象。 您可以对应用程序进行单元测试，而不必在 ASP.NET 进程中运行控制器，这使得单元测试既快速又灵活。 您可以使用任何与 .NET Framework 兼容的单元测试框架。
- 可扩展且可插入的框架。 设计 ASP.NET MVC 框架组件的目的是为了可以轻松地替换或自定义它们。 您可以插入自己的视图引擎、URL 路由策略、操作方法参数序列化以及其他组件。 ASP.NET MVC 框架还支持使用依赖项注入 (DI) 和控制反转 (IOC) 容器模型。 DI 允许您将对象注入到类中，而不是依赖类来创建对象本身。 IOC 指定某个对象是否需要其他对象，第一个对象应该从配置文件之类的外部源中获取第二个对象。 这样，测试会更加轻松。
- 强大的 URL 映射组件，允许您构建具有可理解和可搜索 URL 的应用程序。 URL 未必包含文件扩展名，并且旨在支持非常适合搜索引擎优化 (SEO) 和具象状态传输 (REST) 寻址的 URL 命名模式。
- 支持将现有 ASP.NET 页面（.aspx 文件）、用户控件（.ascx 文件）和母版页（.master 文件）标记文件中的标记用作视图模板。 您可以将现有ASP.NET功能与ASP.NET MVC 框架一起使用，例如嵌套母版页、内联表达式 （%=&lt;&gt;%）、声明性服务器控件、模板、数据绑定、本地化等。
- 支持现有 ASP.NET 功能。 ASP.NET MVC 允许您使用一些功能，如 Forms 身份验证和 Windows 身份验证、URL 授权、成员资格和角色、输出和数据缓存、会话和配置文件状态管理、运行状况监视、配置系统以及提供程序体系结构。
